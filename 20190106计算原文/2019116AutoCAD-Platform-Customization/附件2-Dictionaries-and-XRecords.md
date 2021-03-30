# Dictionaries and XRecords

by Stig Madsen

[Dictionaries and XRecords | AfraLISP](https://www.afralisp.net/autolisp/tutorials/dictionaries-and-xrecords.php)

## 00. Introduction

Since the dawn of times we've had at least 10 options to save private data with an AutoCAD drawing. Those were and are the system variables USERI1-5 and USERR1-5 that holds integers and real numbers, respectively. The idea is OK but the variables are exposed for everyone to use and you shouldn't assume that your private data will stay intact. Somewhere around release 10 came XData (Extended Entity Data) which is a rather clever invention. With XData you can attach intelligent information to entities, and it works flawlessly. There aren't really drawbacks to the technique, but there are limitations that has to do with the amount and type of data you can attach.

During release 13 new forms of entities hit the deck in order to keep and maintain all sorts of data. Among those were Dictionaries and XRecords. Like XData, Dictionaries can be attached to any kind of entity and you can even attach XData to them. Additionally, with Dictionaries/Xrecords you can tell the drawing itself to keep your data because the drawing maintains a dictionary in which you can save all the data you want.

## 01. Dictionaries

So what is a Dictionary and how does it work? Instead of lengthy explanations, it'll be much easier to look at one of the many Dictionaries that AutoCAD itself uses. Later we''ll briefly look at how to make our own simple Dictionary, add an Xrecord to it and save them both with the drawing.

So, fire up AutoCAD and pay attention. As mentioned, the drawing maintains a Dictionary that is always present. This is known as the 'named object dictionary' (although I prefer the term 'main dictionary'). In VBA lingo it's a collection object and like all other collections it just holds a series of other objects. In VBA it is accessed through the document object and in AutoLISP it's accessed by one function only, NAMEDOBJDICT :

```
Command: (setq mainDict (namedobjdict))
<Entity name: 16a9860>
```

```
Command: (entget mainDict)
((-1 . <Entity name: 16a9860>) (0 ."DICTIONARY")
(330 . <Entity name: 0>) (5 . "C") (100 . "AcDbDictionary")
(280 . 0) (281 . 1) (3 . "ACAD_GROUP")(350 . <Entity name: 16a9868>)
(3 . "ACAD_LAYOUT") (350 . <Entity name: 16a98d0>)
(3 . "ACAD_MLINESTYLE") (350 . <Entity name: 16a98b8>)
(3 . "ACAD_PLOTSETTINGS") (350 . <Entity name: 16a98c8>)
(3 . "ACAD_PLOTSTYLENAME") (350 . <Entity name: 16a9870>))
```

By looking at the entity list of the main Dictionary, the most important thing about Dictionaries becomes clear: they are complete entities by themselves. They are not fragments of data attached to other entities like XData are.

However, the Dictionary itself is not where you will store your raw data, — it is merely a container for other objects that in turn can hold the data. The main dictionary above shows 5 such objects. Its components are given by a unique name in group 3. Corresponding entity names are given by groups 350 that follow, but when referencing an object in a Dictionary it should be done by name only. For example, to reference the "ACAD_MLINESTYLE" object, use DICTSEARCH :

```
Command: (setq mlineDict (dictsearch (namedobjdict) "ACAD_MLINESTYLE"))
((-1 . <Entity name: 16a98b8>) (0 . "DICTIONARY") (5 . "17")
(102 . "{ACAD_REACTORS") (330 . <Entity name: 16a9860>) (102 . "}")
(330 . <Entity name: 16a9860>) (100 . "AcDbDictionary") (280 . 0)
(281 . 1) (3 . "Standard") (350 . <Entity name: 16a98c0>))
```

This member of the main Dictionary is a Dictionary itself. It holds all the mline styles that are available. Any style that is created with MLSTYLE is added to the "ACAD_MLINESTYLE" Dictionary. To explore a specific style we have to dig deeper and because we are dealing with Dictionaries we can use DICTSEARCH again — this time by searching the recently returned Dictionary :

```
Command: (setq mlineStd (dictsearch (cdr (assoc -1 mlineDict)) "Standard"))
((-1 . <Entity name: 16a98c0>) (0 . "MLINESTYLE") (5 . "18")
(102 . "{ACAD_REACTORS") (330 . <Entity name: 16a98b8>) (102 . "}")
(330 . <Entity name: 16a98b8>) (100 . "AcDbMlineStyle") (2 . "STANDARD")
(70 . 0) (3 . "") (62 . 256) (51 . 1.5708) (52 . 1.5708) (71 . 2) (49 . 0.5)
(62 . 256) (6 . "BYLAYER") (49 . -0.5) (62 . 256) (6 . "BYLAYER"))
```

Now we are getting somewhere! All properties of the mline style "Standard" are exposed in all their glory. Feel free to look up all properties in the DXF Reference. Want to change the color of multilines? Just SUBSTitute group 62 and ENTMOD the style as usual :

```
Command: (entmod (subst (cons 62 2)(assoc 62 mlineStd) mlineStd))
((-1 . <Entity name: 16a98c0>) …etc… (62 . 2) …etc… (62 . 2) …etc…)
```

Ok, so a Dictionary is a container that can hold a number of objects. Why not use existing structures like symbol tables instead of complicating things? Many reasons, but two reasons come to mind. Symbol tables are maintained by the people who implemented them and to expand them to hold every possible custom object is not an option. Secondly, Dictionaries can be customized in a way that is not possible with symbol tables, and that opens a range of possibilities only limited by imagination.

Dictionaries and XRecords go hand in hand. Like Dictionaries, XRecords are handled as named objects and can be manipulated by the same functions that handle Dictionaries. In the following, we'll try to add our own Dictionary to the main dictionary. We will also create an XRecord to hold various informations and add it to our Dictionary.

1『这里慢慢有点懂 XRecord 和 Dictionaries 的关系了。Dictionaries 是容器，XRecord 可以帮数据然后加进 Dictionaries 里。（2021-03-28）』

When dealing with Dictionaries, at one point you will have to consider ownership. Which object is going to own the Dictionary? Will it hold generic data for your application or will it hold data that is specific for some entity or entities? In the first case you will probably use the main dictionary to save your data with the drawing. If your application is maintaining data for linetypes, you will probably add an extension dictionary to the linetype symbol table. Whatever the ownership, the Dictionary is initially created without ownership and for that purpose we'll use the function ENTMAKEX. It works like ENTMAKE, but it creates the entity without an owner — and it returns an entity name instead of an entity list. Let's make a function that adds our own Dictionary to the main dictionary. In this example we will name it "OUR_DICT" :

1『想要的东西来了。可以创建 2 类字典：1）全局性的，不属于任何实体对象，直接添加到 main dictionary。2）绑在实体对象上的字典。如何创建 2 类 dictionary，做一张主题卡片。（2021-03-28）』—— 已完成

```c
(defun get-or-create-Dict (/ adict)
  ;;test if "OUR_DICT" is already present in the main dictionary
  (if (not (setq adict (dictsearch (namedobjdict) "OUR_DICT")))
    ;;if not present then create a new one and set the main
    ;; dictionary as owner
    (progn
      (setq adict (entmakex '((0 . "DICTIONARY") (100 . "AcDbDictionary"))))
      ;;if succesfully created, add it to the main dictionary
      (if adict (setq adict (dictadd (namedobjdict) "OUR_DICT" adict)))
    )
    ;;if present then just return its entity name
    (setq adict (cdr (assoc -1 adict)))
  )
)
```

If you want to see what happens to the dictionary when added to an owner, then stop the routine right after ENTMAKEX and use ENTGET to investigate the newly created entity. Notice that the owner in group code 330 will not be specified. After using DICTADD the owner in group 330 will be the main dictionary.

Right now we have placed a Dictionary named "OUR_DICT" in the main dictionary. To check if it succeeded we can investigate the main dictionary :

```
Command: (entget (namedobjdict))
((-1 . <Entity name: 16a9860>) (0 . "DICTIONARY") …etc…
(3 . "ACAD_PLOTSTYLENAME") (350 . <Entity name: 16a9870>)
(3 . "OUR_DICT") (350 . <Entity name: 16a8da0>))
```

And there it is! But what good does it do us? It just sits there and doesn't hold any data. Well, let's say we want to save data for a routine that creates annotations — for example a text style, a layer name and a text height. Simple stuff, but it'll suffice for the purpose of illustration. With XRecords we can create an entity that can hold any possible data within the range of defined data types. Unlike XData it uses regular group codes to save data. All group codes (except internal data like code 5 and the negative codes) can be used. Of course, the data types that are defined for the specific group codes have to be respected. This means that, for example, a code 70 cannot hold anything else than a 16-bit integer and so on. Code values can be examined in the DXF Reference.

## 03. XRecords

An XRecord is created in much the same way as a Dictionary. First we'll see if it already exists, then create it without an owner with ENTMAKEX and lastly add it to our custom Dictionary. Again, we will name it in order to retrieve it by name. In this example it will be called "OUR_DICT". Both name and initial values are hardcoded into the function — in the real world we would probably make this a generic function and specify name and values as arguments.

```c
(defun get-or-make-Xrecord (/ adict anXrec)
  (cond
 
    ;;first get our dictionary. Notice that "OUR_DICT" will be created here in case it doesn't exist
    ((setq adict (get-or-create-Dict))
 
     (cond
 
       ;;if "OUR_DICT" is now valid then look for "OUR_VARS" Xrecord
       ((not (setq anXrec (dictsearch adict "OUR_VARS")))
 
        ;;if "OUR_VARS" was not found then create it
        (setq anXrec (entmakex '((0 . "XRECORD")
                                (100 . "AcDbXrecord")
                                (7 . "Arial")
                                (8 . "A09--T-")
                                (40 . 2.0)
                                )
                     )
        )
 
        ;;if creation succeeded then add it to our dictionary
        (if anXrec (setq anXrec (dictadd adict "OUR_VARS" anXrec)))
       )
 
       ;;if it's already present then just return its entity name
       (setq anXrec
 
        (cdr (assoc -1 (dictsearch adict "OUR_VARS")))
       )
     )
    )
  )
)
```

Now we have an XRecord that contains three different data: a text style name in group code 7, a layer name in group code 8 and a text height in group code 40. All codes are chosen with respect to normal convention, but any code that can be associated with the data type in question can be used. The structure from which to access our data will now be like this :

```
Named object dictionary      =  Dictionary (owner = the drawing)
  > OUR_DICT                 =  Dictionary (owner = named object dictionary)
      > OUR_VARS             =  Xrecord    (owner = OUR_DICT)
           (7 . "Arial")     =    Egenskab i Xrecord
           (8 . "A09-T-")    =    Egenskab i Xrecord
           (40 . 2.0)        =    Egenskab i Xrecord
```

The only thing that remains is to read the data :

```c
(defun getvars (/ vars varlist)
 
  ;;retrieve XRecord "OUR_VARS" from dictionary "OUR_DICT"
  ;;which in turn calls both functions above
  (setq vars (get-or-make-Xrecord))
 
  ;;if our Xrecord is found, then get values in group code 7, 8 and 40
  (cond (vars
         (setq varlist  (entget vars))
         (setq txtstyle (cdr (assoc 7 varlist)))
         (setq txtlayer (cdr (assoc 8 varlist)))
         (setq txtsize  (cdr (assoc 40 varlist)))
        )
 
        ;;otherwise return nil
        (T nil)
  )
)
```

Because of the naming scheme, Dictionaries work much like symbol tables in terms of accessing entries. In addition to DICTSEARCH there's also a function, DICTNEXT, to iterate through all entries in a Dictionary. It works like TBLNEXT — here shown by iterating through the main dictionary :

```
(defun C:LISTDICTS (/ maindict adict)
  (setq maindict (namedobjdict))
  (while (setq adict (dictnext maindict (not adict)))
    (princ (cdr (assoc -1 adict)))
    (princ (strcat "\t(type = " (cdr (assoc 0 adict)) ")\n")
    )
  )
  (princ)
 
)
```

```
Command: listdicts
      <Entity name: 185c0d0> (type = DICTIONARY)
      <Entity name: 185f4b8> (type = DICTIONARY)
      <Entity name: 185c0d8> (type = DICTIONARY)
      <Entity name: 185f4a8> (type = ACDBDICTIONARYWDFLT)
      <Entity name: 18c4320> (type = DICTIONARY)
      <Entity name: 18c3d10> (type = XRECORD)
```

There're also functions to rename a Dictionary, DICTRENAME, and to remove a Dictionary, DICTREMOVE. The latter simply removes its entry from the owner, or in other words: detaches it from the owner. It doesn't delete it unless the owner is "ACAD_GROUP" or "ACAD_MLINESTYLE". Sometimes when updating a Dictionary it's easier to remove/delete it and replace it with a new entry, but that will be for your pleasure to explore.

If you gained some understanding of Dictionaries and XRecords by now then I'll throw in a little assignment: Figure out how you can add the XRecord directly to the main dictionary without first creating a Dictionary!
