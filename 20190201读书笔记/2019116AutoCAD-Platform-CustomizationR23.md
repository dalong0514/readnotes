## 记忆时间

2021-04-01

## 目录

Part II AutoLISP: Productivity through Programming

0206 —— Chapter 16: Creating and Modifying Graphical Objects

0207 —— Chapter 17: Creating and Modifying Nongraphical Objects

## 0206. Creating and Modifying Graphical Objects

The AutoLISP® programming language is great for creating and modifying objects. There are two types of objects that you can create or modify: graphical and nongraphical. Graphical objects are those that you can see and interact with in the drawing area, whether in model or paper space. Nongraphical objects are those that you don't create in the drawing area but that can affect the appearance of graphical objects. I discuss working with nongraphical objects in Chapter 17,「Creating and Modifying Nongraphical Objects.」

2『图形数据和非图形数据，做一张术语卡片。』——已完成

The command function is the most common method that AutoLISP programmers use to create and modify objects, but it isn't the most efficient when you are trying to modify individual properties of an object. Even creating lots of objects in the Autodesk® AutoCAD® program can be slower with the command function. Along with the command function, objects can be created and modified directly by setting property values as part of an entity data list. Extended data (XData) can also be attached to an object as a way to differentiate one object from another or, in some cases, to affect the way an object might look in the drawing area.

1-2『直接用 command，自己就遇到了瓶颈。1）确实效率低下。2）自动生成辅助流程组件，插进来的块，位置经常不是均匀的，目前一直找到不解决办法。正巧这里受到启发，改用直接创建实体数据的方法实现自动生成块。待实现。做一张任意卡片。（2020-10-29）』

### 6.1 Working with Entity Names and Dotted Pairs

Creating and modifying objects with AutoLISP requires the understanding of two concepts: entity names and entity data. Entity names, also known as enames, are numeric values that are assigned to graphical and nongraphical objects stored in a drawing. An ename is expressed as the ENAME data type in AutoLISP. When you want to access an object, you use an ename. After an ename has been obtained, you can then access the object's properties through its entity data list. An entity data list is a list that contains information about an object. In addition to modifying an object using an entity data list, you can create objects with entity data lists. I discuss how to create an object with an entity data list in the「Adding Objects to a Drawing」section, and how to get an ename for an object and the entity data list in the「Modifying Objects」section.

---

Recovering from a Daydream

It is Monday morning and you just got back from vacation. For the most part, you are still thinking about the great time you had with the family at the beach. Before you realize it, you have placed all your dimensions and hatch objects on an incorrect layer. Never fear—AutoLISP to the rescue. Using a few lines of AutoLISP code, you select the misplaced objects and move them onto the correct layer.

---

Each entity data list is made up of many smaller lists that describe the properties of an object. The smaller lists are value pairings commonly known as dotted pairs. They are called dotted pairs because a dot usually separates the key element from the value of the list. The key element is commonly a DXF group code (which is of the integer data type) and used to let AutoCAD know the type of data for the value in the dotted pair. Some DXF group codes have common uses, whereas others have a more general meaning. I discuss some DXF group codes during this chapter, but you will need to refer to the AutoCAD Help system for a listing of all supported DXF group codes by object.

The value of a dotted pair can be made up of more than one item. When a value contains more than one item, no dot is provided, as is the case with coordinate values. Here is an example of an entity data list for a circle:

```c
((-1. <Entity name: 7ff79b005dc0>) (0. "CIRCLE") 
 (330. <Entity name: 7ff79b0039f0>) (5. "1D4") (100. "AcDbEntity") 
 (67. 0) (410. "Model") (8. "0") (100. "AcDbCircle") 
 (10 0.0 0.0 0.0) (40. 0.875) (210 0.0 0.0 1.0))
```

The DXF group codes 10 and 40 are used to describe the circle. The DXF group code 10 represents the center point of the circle (10 0.0 0.0 0.0), whereas the DXF group code 40 represents the radius of the circle, which is set to a value of 0.875. Even though you can use the circle command to create a circle based on a diameter value, AutoCAD stores only the circle's radius as part of the drawing.

DXF group codes don't always have the same meaning. For example, the DXF group code 10 is used by both lines and circles, but for line objects the code represents the line's starting point, as shown in the following entity data list:

```c
((-1. <Entity name: 7ff79b005e00>) (0. "LINE") 
 (330. <Entity name: 7ff79b0039f0>) (5. "1D8") (100. "AcDbEntity") 
 (67. 0) (410. "Model") (8. "0") (100. "AcDbLine") 
 (10 0.0 5.0 0.0) (11 5.0 5.0 0.0) (210 0.0 0.0 1.0))
```

Table 16.1 lists some of the most common DXF group codes that are used by objects in a drawing. For additional information on DXF group codes, search on「DXF entities section」in the AutoCAD Help system.

Table 16.1 Common DXF group codes

|  DXF group code | Description  |
|---|---|
|  0 |  Specifies the object's type |
|  6 |  Specifies the linetype that an object is assigned; not used if the linetype is assigned by layer |
|  8 |  Specifies the layer on which an object is placed |
|  10 |  Specifies the start, center, elevation, or insertion point for many different objects |
|  11 |  Specifies the endpoint or direction vector for many different objects |
|  40 |  Specifies the radius for circles, height for text, and ratio between the major and minor axis of an ellipse |
|  62 |  Specifies the color that an object is assigned; not used if the color is assigned by layer |

---

Referencing Objects Using Handles

Enames aren't the only way you can reference an object in a drawing. When a drawing is closed and reopened, a new ename is assigned to each object in the drawing. However, each object created in a drawing is assigned a unique string value called a handle.

A handle is a hexadecimal number value that is unique for each object in a drawing and can be used to reference an object when the drawing is closed and reopened. While the same handle can be used in more than one drawing, the handle remains unique and unchanged for an object in a drawing. The handle of an object can be accessed from an object's entity data list; the dotted pair with the DXF group code 5 contains the object's handle.

3『「2019114Autolisp-Developers-GuideR00.md」

0306 任意卡——handle 与实体名之间的切换

直接在 CAD 里用 `list` 命令选中一个实体，在显示的信息里，句柄即为 handle。

1、通过实体名获取实体的 handle：借用任意卡 0303 里的信息，可以直接获取一个实体的数据信息，举个例子，里面的 `(5 . "59DAA")` 这个即为 handle。那么获取这个数据的办法就显而易见了，跟获取它的坐标 `(10 xx yy)`，图层 `(0 . "0")`，块名称 `(2 . "PipeArrowLeft")` 等等的信息一模一样。

```c
(cdr (assoc 5 (entget ename)))
```

2、通过 handle 获取实体名。

```c
(setq ename (handent "5a2"))
```

』

Handles are commonly used to export information about the objects in a drawing and process the information externally before using the information to update the objects in the drawing. The AutoLISP handent function accepts a string value that represents an object's handle in the drawing and returns the object's current ename. The following shows the syntax of the handent function:

```c
(handent handle)
```

The handle argument represents an object's handle and must be expressed as a string.

You can get an object's handle using the list command or the AutoLISP entget function, which I discuss later, in the「Modifying Objects」section. The following is an example that gets the entity name of the Block symbol table (or a different object in your drawings)—which has a handle of "1"—with the handent function:

```
(handent "1") 
<Entity name: 7ff79b003810>
```

---

#### 6.1.1 Creating a Dotted Pair

A dotted pair is a list that is created using the AutoLISP cons or quote (') function. When creating a dotted pair, you need to know two things: the key element and the value to be associated with the key element. Although the key element can be of any data type with the exception of a list, it is commonly either a string or integer. In entity data lists, the key element is an integer value that represents a DXF group code. The following shows the syntax of the cons function:

```c
(cons key atom)
```

The arguments are as follows: 1) key. The key argument represents the index or unique identifier for the dotted pair. 2) atom. The atom argument represents the value that you want to associate with the index or unique identifier specified by the key argument.

The following examples show how to create dotted pairs with the cons function, and the values that are returned:

```c
; Dotted pair with a system variable name as the key and its value 
(cons "cmdecho" 0) 
("cmdecho". 0) 

; DXF group code 10 with a coordinate value of 0.5,5.5,0 
(cons 10 (list 0.5 5.5 0.0)) 
(10 0.5 5.5 0.0) 

; DXF group code 40 with a value of 0.875 
(cons 40 0.875) 
(40. 0.875)
```

You can also use the quote function to create a dotted pair. The following examples show how to create dotted pairs with the quote function, and the values that are returned:

```c
; Dotted pair with a system variable name as the key and its value 
'("cmdecho". 0) 
("cmdecho". 0) 

; DXF group code 10 with a coordinate value of 0.5,5.5,0 
'(10 0.5 5.5 0.0) 
(10 0.5 5.5 0.0) 

; DXF group code 40 with a value of 0.875 
'(40. 0.875) 
(40. 0.875)
```

#### 6.1.2 Accessing the Elements of an Entity Data List and Dotted Pair

Accessing the elements of an entity data list and a dotted pair is like accessing the elements of a regular list. Although you can use many of the list-related functions that I discussed in Chapter 14,「Working with Lists,」the AutoLISP assoc function is one of the functions that is frequently used when working with an entity data list. The assoc function is used to return a dotted pair with a specific key element in an entity data list. The following shows the syntax of the assoc function:

```c
(assoc key edlist)
```

The arguments are as follows:

key. The key argument represents the key (left) element of a dotted pair and is used as a way to locate a dotted pair within the list specified by the edlist argument. This argument can be a string or integer value.

edlist. The edlist argument represents the list in which you want to look for a dotted pair that contains the key argument as the key element. The first matching dotted pair is returned.

Here is an example that shows how to return the first dotted pair in the entity data list that has a key (left) element of 40:

```c
; Returns the entity data list of the last object 
; added to the drawing, which is a circle in this example 
(setq ed (entget (entlast))) 
((-1. <Entity name: 7ff773005dc0>) (0. "CIRCLE") 
 (330. <Entity name: 7ff7730039f0>) (5. "1D4") (100. "AcDbEntity") 
 (67. 0) (410. "Model") (8. "0") (100. "AcDbCircle") 
 (10 5.0 6.5 0.0) (40. 2.0) (210 0.0 0.0 1.0)) 

; Returns the dotted pair with the key element of 40 in the entity data list 
(assoc 40 ed) 
(40. 2.0)
```

I explain the entlast and entget functions in the「Selecting an Individual Object」and「Updating an Object's Properties with an Entity Data List」sections later in this chapter. The AutoLISP car and cdr functions can also be helpful when working with dotted pairs. The car function returns the key element of a dotted pair and the cdr function returns the value.

```c
; Returns the key element of the dotted pair 
(car (assoc 40 ed)) 
40 

; Returns the value of the dotted pair 
(cdr (assoc 40 ed)) 
2.0
```

### 6.2 Adding Objects to a Drawing

Adding objects to a drawing can be done using standard AutoCAD commands with the command or entmake function. The entmake function accepts an entity data list that defines an object to be added to the drawing. All of the properties required to create an object must be contained in the entity data list; otherwise, the object won't be created. The properties required by the object are documented as part of the DXF Reference documentation in the AutoCAD Help system, but you might need to perform some trial and error to develop the proper entity data list that creates a new object.

---

Going Further without Commands

Do you find yourself avoiding tables even though your boss likes the look they provide in drawings? Do you wish tables were more efficient for the type of information you add to them? You're not alone. Most objects can be created and modified using commands at the Command prompt, but tables unfortunately are not among them. AutoLISP can help you out. The AutoCAD table command provides limited functionality to create a table, but it can't be used to populate or modify a table. Using AutoLISP, you can create a table using the entmake function while modifying and populating the table with the entget and entmod functions. Once again, with AutoLISP you have reclaimed part of your day for other tasks, such as working on additional projects or freeing up time to learn more about AutoLISP.

---

For some objects it's easier to determine which properties are required; for example, a circle requires a center point and radius whereas a line requires a start and endpoint. The best way to figure out which properties are required when creating an object is to create a new object in a drawing of the type you want to create with the entmake function. Once the object is created, enter the following code at the AutoCAD Command prompt to see the entity data list associated with the object:

```c
(entget (entlast))
```

For example, if you drew a circle with a center point of 5,6.5,0 and a radius of 2.0, the entity data list that is returned might look like this:

```c
((-1. <Entity name: 7ff773005dc0>) (0. "CIRCLE") 
 (330. <Entity name: 7ff7730039f0>) (5. "1D4") (100. "AcDbEntity") 
 (67. 0) (410. "Model") (8. "0") (100. "AcDbCircle") 
 (10 5.0 6.5 0.0) (40. 2.0) (210 0.0 0.0 1.0))
```

In the previous example, the DXF group codes –1, 5, and 330 were automatically generated and assigned to the object. Those DXF group codes shouldn't be part of the entity data list when you create a new object with the entmake function. Table 16.2 describes the DXF group codes –1, 5, and 330.

1-2『这里捡到金子了，教你如何获取用 entmake 函数新建一个实体对象需要哪些必要 `entity data list`。1）在 CAD 图纸里用普通命令画一个实体，或插入一个块实体。2）用命令 `(entget (entlast))` 查看刚刚生成的实体所包含的 `entity data list`。3）扣除掉 DXF group codes 为 -1、5 和 300 的这三个数据。

The DXF group codes 67, 410, 8, and 210 are optional; if they aren't provided as part of the entity data list, AutoCAD uses the current settings and context of the drawing to populate the values of the properties they represent. Table 16.3 describes the DXF group codes 67, 410, 8, and 210.

做一张主题卡片。』——已完成

Table 16.2 Automatically generated DXF group code values

|  DXF group code | Description  |
|---|---|
|  -1 |  Ename assigned to the object while the drawing is open in memory; the value changes each time the drawing is opened. |
|  5 |  Unique handle that is assigned to the object; it's a string value. |
|  330 |  Pointer to the owner of the object. |

After removing the DXF group codes that are automatically generated, the entity data list looks a bit less cluttered and easier to understand:

```c
((0. "CIRCLE") (100. "AcDbEntity") (67. 0) (410. "Model") (8. "0") 
 (100. "AcDbCircle") (10 5.0 6.5 0.0) (40. 2.0) (210 0.0 0.0 1.0))
```

The DXF group codes 67, 410, 8, and 210 are optional; if they aren't provided as part of the entity data list, AutoCAD uses the current settings and context of the drawing to populate the values of the properties they represent. Table 16.3 describes the DXF group codes 67, 410, 8, and 210.

Table 16.3 Optional DXF group code values

|  DXF group code | Description  |
|---|---|
|  67 |  Indicates that the object is in model space (0) or paper space (1) |
|  410 |  Named layout tab that the object exists on |
|  8 |  Layer in which the object is placed |
|  210 |  Extrusion direction of the object |

After removing the DXF group codes that are optional, the entity data list becomes even easier to understand:

```c
((0. "CIRCLE") (100. "AcDbEntity") (100. "AcDbCircle") (10 5.0 6.5 0.0) (40. 2.0))
```

The entity data list that now remains with the DXF group codes 0, 100, 10, and 40 represents the entity data needed to create a new circle with the entmake function. For additional information on DXF group code values, search on「DXF entities section」in the AutoCAD Help system. Table 16.4 describes the DXF group codes 0, 100, 10, and 40.

Table 16.4 Required DXF group code values

|  DXF group code | Description  |
|---|---|
|  0 |  Entity type. |
|  100 |  Sub/entity class that the object is based on. Not all objects require these values. If the object doesn't get created without them, add them to the entity data list and the object should be created. |
|  10 |  Center point of the circle. |
|  40 |  Radius of the circle. |

Once you have the entity data list that describes the object you want to create, it can then be passed to the entmake function. If the entmake function is able to successfully create the new object, an entity data list is returned. If not, nil is returned. The following shows the syntax of the entmake function:

```c
(entmake [entlist])
```

The entlist argument represents the entity data list of the object to be created, and it is an optional argument. The list must contain all required dotted pairs to define the object and its properties. The following examples show how to create an entity data list with the list and cons functions, and then use the resulting list to create an object with the enmake function:

```c
; Creates a new circle at 2.5,3.5 with a radius of 0.75 
(setq cenPt (list 2.5 3.5 0.0) rad 0.75) 
(entmake (list (cons 0 "CIRCLE") (cons 10 cenPt) (cons 40 rad))) 
; creates a new line from 0,0,0 to 2.5,3.5 
(setq startPt (list 0.0 0.0 0.0) endPt (list 2.5 3.5 0.0)) 
(entmake (list (cons 0 "LINE") (cons 10 startPt) (cons 11 endPt)))
```

Figure 16.1 shows the result of the two previous examples.

Remember that the quote (') function can't evaluate an atom, so you can't use variables in a list that is defined with the quote function. The following examples show how to create an entity data list with the quote function, and then use the resulting list to create an object with the entmake function:

```c
; Creates a new circle at 2.5,3.5 with a radius of 0.75 (entmake '((0. "CIRCLE") (10 2.5 3.5 0.0) (40. 0.75))) ; creates a new line from 0,0,0 to 2.5,3.5 (entmake '((0. "LINE") (10 0.0 0.0 0.0) (11 2.5 3.5 0.0)))
```

In addition to using the entmake function, you can create objects with the entmakex function. The difference between the entmake and entmakex function is that an owner isn't assigned to the object created with the entmakex function. Owner assignment primarily affects the creation of nongraphical objects, as all graphical objects are assigned to the current space or named layout.

WARNING: Objects created with the entmake and entmakex functions don't participate in undo recording like objects created with standard AutoCAD commands. Undo recording must be implemented in your function using the undo command, and its suboptions Begin and End. I provide an example of how to group functions into a single undo grouping in Chapter 19,「Catching and Handling Errors.」

TIP: Unless you need to drag an object onscreen, I recommend creating objects with the entmake function since it gives you greater control over the object being created. The entmake function (unlike commands executed with the command function) isn't affected by the current running object snap settings.

This exercise shows how to create a plan view of a machine screw with a slotted round head (see Figure 16.2):

1 Create a new drawing.

2 At the AutoCAD Command prompt, type the following and press Enter to create a new circle that has a center point of 0,0 and radius of 0.4075. 

```c
(entmake '((0. "CIRCLE") (10 0 0) (40. 0.4075)))
```

The dotted pair with the DXF group code 10 sets the center point of the circle, and the dotted pair with the DXF group code 40 sets the radius of the circle.

3 Type the following and press Enter to create the two lines that define the top and bottom of the slot in the head of the screw: 

```c
(entmake '((0. "LINE") (10 -0.18 0.0275) (11 0.18 0.0275))) 
(entmake '((0. "LINE") (10 -0.18 -0.0275) (11 0.18 -0.0275)))
```

The dotted pair with the DXF group code 10 sets the start point of the line, and the dotted pair with the DXF group code 11 sets the endpoint of the line.

4 Type the following and press Enter to create the two arcs that define the left and right edges of the slot in the head of the screw: 

```c
(entmake '((0. "ARC") (10 0.0032 0) (40. 0.1853) (50. 2.99261) (51. 3.29058))) 
(entmake '((0. "ARC") (10 -0.0032 0) (40. 0.1853) (50. 6.13431) (51. 0.148875)))
```

The dotted pair with the DXF group code 10 sets the center point, DXF group code 40 sets the radius, DXF group code 50 sets the start angle (in radians), and DXF group code 51 sets the end angle (in radians) for each arc.

Figure 16.2 Plan view of a #12-24 machine screw, slotted round head

### 6.3 Selecting Objects

AutoLISP enables you to step through the objects in a drawing or allow the user to interactively select one or more objects in the drawing area. Based on the selection technique used, an ename is returned; otherwise, a selection set (ssname) is returned that can contain one or more objects.

#### 6.3.1 Selecting an Individual Object

AutoLISP provides two different techniques that can be used to select an individual object within a drawing—through code or via user interaction. When you want to work with the most recent object or step through all of the objects in a drawing, you don't need any input from the user. The AutoLISP functions entlast and entnext can be used to get an individual object without any input from the user. If you do want to allow the user to interactively select an individual object, you can use the entsel and nentsel functions.

2『以上获取实体数据集的方式，做一张任意卡片。』

#### Selecting an Object through Code

The entlast function returns the entity name of the last graphical object added to a drawing and doesn't require any arguments. This function can be helpful in getting the entity name for a new object created with the entmake function.

```c
; Create an arc with a center point of -1,1, radius of 1.5, 
; a start angle of 315, and end angle of 135 
(entmake '((0. "ARC")(10 -1.0 1.0 0.0)(40. 1.5)(50. 5.49779)(51. 2.35619))) 
((0. "ARC") (10 -1.0 1.0 0.0) (40. 1.41421) (50. 5.49779) (51. 2.35619)) 
(setq entityName (entlast)) 
<Entity name: 7ff72292cc10>
```

The entnext function allows you to traverse a drawing from the first drawn to most recently added graphical object. When entnext is called without an argument, it returns the ename of the oldest graphical object in the drawing. If the function is passed a valid ename, the ename of the object drawn after the one passed to the function is returned. The following shows the syntax of the entnext function:

```c
(entnext [ename])
```

The ename argument is optional and represents the entity name of an object. The function returns the name of the next object in the drawing. When no ename argument is provided, the entity name of the first graphical object in the drawing is returned.

The following example code uses the entnext function to step through and list the type of each object in the current drawing:

```c
; Lists the DXF group code 0 value for each object in the drawing 
(defun c:listobjects ( / ) 
  (prompt "\nObjects in this drawing:") 
  (setq entityName (entnext)) 
  (while entityName 
    (prompt (strcat "\n" (cdr (assoc 0 (entget entityName))))) 
    (setq entityName (entnext entityName)) 
  ) 
  (princ) 
)

Objects in this drawing: 
CIRCLE 
DIMENSION 
DIMENSION 
INSERT 
ATTRIB 
SEQEND 
CIRCLE 
VIEWPORT 
VIEWPORT 
CIRCLE 
DIMENSION 
ARC
```

The previous example used the entget function to return an entity data list of an object. I explain how to use this function later, in the「Updating an Object's Properties with an Entity Data List」section.

1-2『这个例子看下来后，entlast、entnext 还有 entget 这几个函数结合起来可以做好多事，特别是 entnext 的用法灵活性很大。比如自动生成辅助流程里，又想到一个思路：1）先直接使用 entlast 获取图纸里的最后一个实体名保存下来。2）批量插入辅助流程组件块后，通过刚刚最后一个实体名外加 entnext 函数，可以获得所有批量插入的块的实体名列表。3）根据这个实体名列表批量修改属性值，这样又跟以前开发好的功能对接上了。把上面信息合并到「获取实体数据集的方式」任意卡里。』——已完成

#### Selecting an Object Interactively

The user can select a single object in the drawing area using the entsel and nentsel functions. The entsel function returns a list of two values: the entity name of the object selected and the center point of the pick box when the object was selected. nil is returned by the entsel function if an object isn't selected as the result of either the user picking in an empty area of the drawing or pressing Enter.

The nentsel function is similar to entsel except that nentsel allows you to select a subentity within an object, such as an old-style polyline, dimension, or block. When a subentity in an object is selected with the nentsel function, a list of four elements is returned (in this order): 1) The entity name of the subentity. 2) The point picked in the drawing. 3) A transformation matrix for the subentity. 4) The entity name of the parent object of the subentity.

The following shows the syntax of the entsel and nentsel functions:

```c
(entsel [prompt]) 
(nentsel [prompt])
```

The prompt argument is optional and represents the message (a string) that should be displayed to the user when they are asked to select an object. If a prompt is not provided, the default prompt message of Select object: is displayed. The following examples show how to select an object with the entsel function:

```c
; Prompts the user to select an individual object 
(setq entlist (entsel "\nSelect an object: ")) 
(<Entity name: 7ff72292cc10> (-0.75599 2.48144 0.0)) 

; Uses the car function to get the entity name returned by entsel 
(setq entityName (car entlist)) 
<Entity name: 7ff72292cc10> 

; Uses the cadr function to get the coordinate value returned by entsel 
(setq pickPoint (cadr entlist)) 
(-0.75599 2.48144 0.0)
```

#### 6.3.2 Working with Selection Sets

A selection set, sometimes known as a selection set name or ssname for short, is a temporary container that holds a reference to objects in a drawing. AutoLISP represents a selection set with the PICKFIRST data type. You get a selection set, commonly based on the objects in a drawing that the user wants to modify or interact with. For example, when you see the Select objects: prompt AutoCAD is asking you to select the objects in the drawing you want to work with and it gets a selection set containing the objects you selected in return.

In addition to getting a selection set based on user input, you can create a selection set manually and add objects to it. You might want to create a function that steps through a drawing and locates all the objects on a specific layer, and then returns a selection set that the next function can work with. Once a selection set is created, you can add additional objects or remove objects that don't meet the requirements you want to work with. A selection set makes it efficient to query and modify a large number of objects.

2『选择集的概念做一张术语卡片。』——已完成

#### Creating a Selection Set

The most common way to create a selection set is to simply prompt the user to select objects in the drawing. The entsel and nentsel functions allow you to select a single object, but typically you will want to allow the user to select more than one object at a time. The ssget function allows the user to interactively select objects in a drawing using the selection methods that are commonly available at the Select objects: prompt. The ssget function can also be used to create a selection set without any user input. The ssget function returns a PICKSET value if at least one object was selected or returns nil if no objects were selected.

NOTE: Unlike the entsel and nentsel functions, the ssget function doesn't have a prompt argument. If you want a lead-in to the Select objects: prompt that ssget displays, you will need to display one with the prompt or princ function.

The following shows the syntax of the ssget function:

```c
(ssget [method] [point1 [point2]] [points] [filter])
```

Here are the arguments:

method. The method argument is optional and represents the selection method that should be used to create the selection set. Many of the selection methods available are similar to those found at the Select objects: prompt, but additional ones are available from AutoLISP. Table 16.5 lists some of the common selection methods available; for a full list of options search on「ssget」in the AutoCAD Help system.

point1. The point1 argument is an optional point list that is used to select the topmost object in the draw order at the specified point. This argument is also used to specify the first corner of a crossing window or window selection.

point2. The point2 argument is an optional point list that is used to specify the second point for the crossing window or window selection.

points. The points argument is an optional list that contains several point lists; it is used to specify the points of a fence, crossing polygon, or window polygon selection.

filter. The filter argument is an optional association list that is similar to an entity data list, but it can also include comparison and grouping operators. Later in this chapter I explain how to create and use selection-set filters; see the sections「Filtering Selected Objects」and「Selecting Objects Based on XData.」

Table 16.5 ssget selection methods

|  Selection method | Description  |
|---|---|
|  C |  Crossing window selection |
|  CP |  Crossing polygon selection |
|  L |  Last object selection |
|  P |  Previous selection set |
|  W |  Window selectio |
|  WP |  Window polygon selection |
|  X |  All entities in the database; locked and frozen also |
|  :S |  Single object selection |
 
The following examples show how to select objects with the ssget function; the returned values will vary based on the drawing you have open. Open a drawing with some objects in it before trying these examples:

```c
; Freely lets the user to select objects 
(setq ss (ssget)) 
Select objects: Specify the first corner of the selection window Specify opposite corner: 
Specify a second point to define the selection window 
7 found Select objects: 
Press Enter to end object selection 
<Selection set: 4d> 

; Freely lets the user to select a single object 
(setq ssPt (ssget "_:S")) 
<Selection set: 1cd> 

; Selects the last object drawn at 0,0,0 
(setq ssPt (ssget '(0 0 0))) 
<Selection set: a9> 
1 found Select objects: 

; Selects all objects that intersect 0,0,0 and not just the topmost object 
(setq ssC (ssget "_C" '(0 0 0) '(0 0 0))) 
<Selection set: be> 
3 found Select objects: 

; Selects objects with fence selection crossing (0,0), (0,6), (12,9), and (12,0) 
(setq ssF (ssget "_F" '((0 0)(0 6)(12 9)(12 0))))
 <Selection set: 190>
```

TIP: A limited number of selection sets can exist in memory while a drawing remains open; a total of 128 selection sets can be active at one time—the number of selection sets that have been created and assigned to different variables without the variable being set back to nil. Once this limit is reached, no new selection sets can be created. I recommend defining any variables that are assigned a selection set as being local to a function, except when you may need to access a selection set across multiple functions. It is always better to pass values and selection sets to a function than to rely on global variables. If you use global variables for selection sets, you should set all variables to nil when they are no longer needed in order to remove them from memory.

The ssget function also supports implied selection with the I selection method. Just like many AutoCAD commands, such as move and copy, implied selection allows a user to select objects before starting your custom program. If no objects are selected when you use the statement `(ssget "_I")`, the ssget function returns nil. You can then test for the nil return value, and if nil is returned, you can prompt the user to select objects.

In addition to using the ssget function to get the objects selected with implied selection, you can use the ssgetfirst function to select objects that have their grips displayed. Grips are displayed only when no custom program or command is active and the user selects objects in the drawing area. The ssgetfirst function returns a list of two elements. The first element always returns nil in recent releases, but in earlier releases it returned a pickfirst value that represented the objects that displayed grips and weren't selected. The second element returns a pickfirst value that represents any objects that are currently selected and have their grips displayed. The ssgetfirst function doesn't accept any arguments.

While the ssgetfirst function is used to get objects that are currently selected and have their grips displayed, you can use the sssetfirst function to select and display the grips for specific objects. The following shows the syntax of the sssetfirst function:

```c
(sssetfirst gripset [pickset])
```

Here are the arguments:

gripset. The gripset argument no longer affects the outcome of the sssetfirst function. In earlier releases, this argument required a pickset value that would be used to display the grips of objects but not select them. In recent releases, nil should always pass this argument.

pickset. The pickset argument is optional and must be a pickfirst value that contains the objects that should be selected and have their grips displayed.

The following examples show how to select and display the grips for the last object in a drawing with the sssetfirst function:

```c
; Creates a line object that is drawn from 0,0 to -5,5 with a color of red 
(entmake '((0. "line")(10 0.0 0.0)(11 -5.0 5.0)(62. 1))) 
((0. "line") (10 0.0 0.0) (11 -5.0 5.0) (62 . 1)) 

; Displays grips for and selects the line that was added 
(sssetfirst nil (ssget "L")) 
(nil <Selection set: 353>) 

; Erases the object with grips displayed 
(command "._erase" (cadr (ssgetfirst)) "") 
nil
```

NOTE: The ssnamex function can be used to get information about how the objects in a selection set were added, as well as how the selection set was created. This includes selection sets created with the ssget, ssgetfirst, and ssadd functions. The value returned by the ssnamex function is a list. For more information on the ssnamex function, search on「ssnamex」in the AutoCAD Help system.

1『汇总：1）上面的有关 `ssgetfirst` 的代码没弄懂其应用场景。2）`ssnamex` 的应用场景也没 get 到，它跟 `ssname` 的功能有啥区别呢，看官方文档都是通过 index 获取一个选择集里某个实体对象的名称。（2020-10-30）』

#### Managing Objects in a Selection Set

After the user has been prompted to select objects, the resulting selection set can be revised by adding or removing objects. Objects that aren't in the selection set but are in the drawing can be added to the selection set using the ssadd function. If the user selected an object that shouldn't be in the selection set, it can be removed using the ssdel function. The ssadd and ssdel functions return the selection set that they are passed if the function was successful; otherwise, the function returns nil.

NOTE: In addition to adding objects to a selection set with the ssadd function, you can use the function to create a new selection set without user interaction.

Normally when an object is selected in the drawing, it is added to a selection set once, as duplicate entries aren't allowed. Before adding an object to a selection set with the ssadd function, you can determine if an object is already present in a selection set with the ssmemb function. Duplicate objects in a selection set isn't a problem, but it could cause an issue if your program is extracting information from a drawing or could result in your program taking longer to complete. The ssmemb function returns the ename of the object if it is present in the selection set; otherwise, the function returns nil. The following shows the syntax of the ssadd, ssdel, and ssmemb functions:

```c
(ssadd ename [ss]) 
(ssdel ename ss) 
(ssmemb ename ss)
```

The arguments are as follows:

ename. When used with the ssadd or ssdel function, the ename argument represents the entity name that should be added to or removed from the selection set. When used with the ssmemb function, the ename argument specifies a particular ename to check for in the selection set.

ss. When you want to add, remove, or check for the existence of an entity name in a selection set, the ss argument specifies the selection set for the operation. The ss argument is optional for the ssadd function.

The following examples show how to add and remove objects in a selection set using the ssadd, ssdel, and ssmemb functions:

```c
; Create a line object 
(entmake '((0. "line")(10 0.0 0.0)(11 -5.0 5.0)(62. 1))) 
((0. "line") (10 0.0 0.0) (11 -5.0 5.0) (62. 1)) 

; Add the line to the selection set 
(setq ss1 (ssadd (entlast) ss1)) 
<Selection set: a1> 

; Determine if the last graphical entity is in the selection set 
(ssmemb (entlast) ss1) 
<Entity name: 7ff6a1704f00> 

; Remove the last entity from the selection set 
(ssdel (entlast) ss1) 
<Selection set: a1> 

; Determine if the last graphical entity is in the selection set 
(ssmemb (entlast) ss1) 
nil
```

#### Stepping through a Selection Set

Selection sets contain the objects the user selected in the drawing for query or modification and might include one to several thousand objects. You can use the repeat or while looping functions in combination with the sslength and ssname functions to step through and access each object in a selection set. The sslength function returns the number of objects in a selection set as an integer, whereas the ssname function is used to return the entity name of an object located at a specific index within a selection set. The index of the first object in a selection set is 0. As part of a looping statement, you increment an integer value by 1 to get the next object until you reach the last object in the selection set. If an object isn't at the specified index in a selection set when using the ssname function, nil is returned. The following shows the syntax of the sslength function:

```c
(sslength ss)
```

The ss argument represents the selection set from which you want to get the number of objects.

The following shows the syntax of the ssname function:

```c
(ssname ss index)
```

Its arguments are as follows:

ss. The ss argument represents the selection set from which you want to get an entity name at a specific index.

index. The index argument represents the location within the selection set specified by the ss argument that has the object you want to get. 0 is the index of the first object in the selection set.

The following examples show how to get the number of objects in a selection set and get an object from a selection set with the sslength and ssname functions:

```c
; Get a selection set 
(setq ssNew (ssget)) 
Select objects: Specify the first corner of the object-selection window 
Specify opposite corner: Specify the other corner of the object-selection window 
9 found 
Select objects: Press Enter to end object selection 
<Selection set: 13> 

; Output the number of objects in a selection set 
(prompt (strcat "\nSelection set length: " 
(itoa (sslength ssNew))))(princ) 
Selection set length: 9 

; Get the entity name of the first object in the selection set 
(ssname ssNew 0) 
<Entity name: 7ff63f005d90>
```

This exercise shows how to create and step through a selection set:

1 Open a drawing with some objects, or create a new drawing and then add some objects to the drawing.

2 At the AutoCAD Command prompt, type the following and press Enter to create a selection set and assign it to the sset variable:

```c
(prompt "\nSelect objects to list: ") 
(setq sset (ssget))
```

3 Type the following and press Enter to create a new circle and then add the new circle to the selection set: 

```c
(entmake '((0. "circle") (10 0.0 0.0) (40. 2))) 
(if (= (ssmemb (entlast) sset) nil) 
  (setq sset (ssadd (entlast) sset)) 
)
```

While the circle shouldn't be part of the objects you selected, the code shows how to use a comparison to test the results of the ssmemb function. The new object is added only if it isn't already part of the selection set.

4 Type the following and press Enter to display the number of objects in the selection set:

```c
(prompt (strcat "\nObjects in selection set: " 
(itoa (sslength sset))))(princ)
```

5 Type the following and press Enter to change the color of each object in the selection set: 

```c
(setq cnt 0 clr 1) 
(while (> (sslength sset) cnt) 
  (command "._change" (ssname sset cnt) "" "_p" "_c" clr "") 
  (setq cnt (1+ cnt)) 
  (setq clr (1+ clr)) 
  (if (> clr 9) 
    (setq clr 1)
  ) 
)(princ)
```

The colors assigned to the objects range from ACI 1 through 9, and reset back to 1 when the counter reaches 10.

1『上面的代码目前没怎么看明白。（2020-10-30）』

#### 6.3.3 Filtering Selected Objects

When selecting objects with the ssget function, you can control which objects are added to the selection set. A selection filter allows you to select objects of a specific type or even objects with certain property values. Selection filters are made up of dotted pairs and are similar to an entity data list. For example, the following selection filter will select all circles on the layer holes:

```c
'((0 . "circle")(8 . "holes"))
```

As I mentioned earlier, the DXF group code 0 represents an object's name and the DXF group code 8 represents the name of the layer an object is placed on.

In addition to object names and properties, a selection filter can include logical grouping and comparison operators to create complex filters. Complex filters can be used to allow for the selection of several object types, such as both text and mtext objects, or allow for the selection of circles with a radius in a given range. Logical grouping and comparison operators are specified by string values with the DXF group code -4. For example, the following selection filter allows for the selection of circles with a radius in the range of 1 to 5:

```c
'((0 . "circle") 
  (-4 . "<and") 
    (-4. "<=") (40. 5.0) 
    (-4. ">=") (40. 1.0) 
  (-4. "and>")
)
```

Selection filters support four logical grouping operators: and, or, not, and xor. Each logical grouping operator used in a selection filter must have a beginning and an ending operator. Beginning operators start with the character `<` and ending operators end with the character `>`. In addition to logical operators, you can use seven different comparison operators in a selection filter to evaluate the value of a property: = (equal to), != (not equal to), < (less than), > (greater than), <= (less than or equal to), >= (greater than or equal to), and * (wildcard for string comparisons).

3『

自己数据流里筛选 SS 的代码：

```c
(defun GetAllInstrumentAndPipeSSUtils ()
  (setq ss (ssget "X" '((0 . "INSERT") 
        (-4 . "<OR")
          (2 . "InstrumentP")
          (2 . "InstrumentL")
          (2 . "InstrumentSIS")
          (2 . "PipeArrowLeft")
          (2 . "PipeArrowUp")
        (-4 . "OR>")
      )
    )
  )
)
```

』


After defining a selection filter, you then pass it to the filter argument of the ssget function. This exercise shows how to use selection filters with the ssget function:

1 Create a new drawing. Add some circles, arcs, and lines to the drawing.

2 At the AutoCAD Command prompt, type `(setq ssCircles (ssget '((0. "circle"))))` and press Enter.

3 At the Select objects: prompt, select all the objects in the drawing. Notice only the circles are highlighted. Press Enter to end object selection.

4 Type `(command "._change" ssCircles "" "_p" "_c" 1 "")` and press Enter to change the color of all circles to red.

5 At the AutoCAD Command prompt, type:

 ```c
 (setq ssArcsLines 
  (ssget '((-4 . "<or") (0 . "arc") (0 . "line") (-4 . "or>")))
)
 ``` 
 
 and press Enter. Select some of the lines and arcs in the drawing.

6 Type `(command "._change" ssArcsLines "" "_p" "_c" 3 "") `and press Enter to change the color of the selected objects to green.

TIP: On AutoCAD for Windows, you can use the filter command to create a filter selection and save it. Saving the filter adds it to the file named filter.nfl. You can use the AutoLISP statement `(findfile "filter.nfl")` to return the location of the file in the command-line window. Open the file with Notepad. The filter command writes the filter in two formats: as AutoLISP statements `(:ai_lisp)` and as a string description `(:ai_str)`. You can copy the AutoLISP statements that are created to define an object selection filter for use with the ssget function. Although this technique can help simplify the testing and creation of complex selection filters, it is undocumented and something I just figured out years ago when I first started learning AutoLISP.

1『上面的信息有待消化，没看明白。（2020-10-30）』

### 6.4 Modifying Objects

The majority of time spent on a design isn't related to creating new objects, but rather to modifying the objects that are already in a drawing. When you need to modify an object, you can use an AutoCAD command with the command function or directly with AutoLISP functions. Directly modifying an object provides you with more choices in the properties you can change and gives you more flexibility than using commands.

Modifying objects with AutoCAD commands is similar to creating new objects, with the exception of the way you pass objects to the command. Based on the command, you will need to pass one of the following to the Select object: or Select objects: prompt to select objects:

Entity Name (ename). An ename can be used when a command expects or you want to modify a single object.

Selection Set (ssname). An ssname can be used to pass several objects to a command that can modify one or more objects.

I explained how to select objects and work with selection sets in the「Selecting Objects」section earlier in this chapter.

The following are examples that demonstrate how to modify objects with AutoCAD commands:

```
; Changes the selected objects to the color red 
(prompt "\nSelect objects to change to red: ") 
(setq ss (ssget)) 
(command "._change" ss "" "_p" "_c" 1 "") 

; Scale the last graphical object by a user-defined base point and a factor of 2 
(command "._scale" (entlast) "" PAUSE 2)
```

In this section, I explain how to work with entity names and directly modify an object without using the command function. The properties of an object can be queried or edited one at a time, or you can manipulate several properties of an object by changing the entity data list that represents the object.

#### 6.4.1 Listing and Changing the Properties of an Object Directly

AutoLISP offers two different methods for modifying the properties of an object directly. The easier of the two methods is to use the object property functions that were introduced with AutoCAD 2012. These functions require less code than the legacy approach of getting and manipulating the entity data list of an object. The property-related functions are less cryptic than entity data list manipulation as well, because you don't need to understand the various DXF group codes associated with a specific object. The downside to these functions is that they work only with AutoCAD 2012 and later, so if you need to support an earlier release you will need to manipulate entity data lists (which I cover in the next section).

Table 16.6 lists the AutoLISP functions available in AutoCAD 2012 and later that can be used to list, get, and set the properties of an object.

|  Function | Description  |
|---|---|
|  dumpallproperties |  Returns all of the properties for the specified object |
|  getpropertyvalue |  Returns the current value of an object's property |
|  setpropertyvalue |  Assigns a value to an object's property |
|  ispropertyreadonly |  Returns T or nil based on whether an object property is read-only |

1-2『看到这里才知道，之前一直用的传统方法：通过实体名称结合 `entget` 函数获取实体的「数据集」，通过替换数据集里的「点对」来实现修改属性。原来还有第二种方法，直接用 autolisp 封装好的函数，前提是只支持 AutoCAD 2012 以后的，可以接受。修改实体数据的 2 种方法，做一张主题卡片。』——已完成

#### Listing Object Properties

The dumpallproperties function outputs the properties and their current values for an object to the command-line window. Some property values, such as StartPoint for a line or Position of a block reference, can be output as a single value or as three individual values. The following shows the syntax of the dumpallproperties function:

```c
(dumpallproperties ename [mode])
```

Its arguments are as follows:

ename. The ename argument represents the entity name of the object for which you want to list properties.

mode. The mode argument is optional and represents how data types such as AcGePoint3d and AcGeVector3d are output. When mode is 0, a property such as Center is displayed as a single entry and not separate entries for the X, Y, and Z values of a property. For example, the following output is of the center point for a circle that has X, Y, and Z components to the value. The output shows all three components as part of a single property named Center.

```
Center (type: AcGePoint3d) 
    (LocalName: Center X;Center Y;Center Z) = 0.000000 5.000000 0.000000
```

A value of 1 for mode displays each element of a value as separate entries. This is the default behavior when mode isn't provided. The following output is of the same center point as before, but notice all three components of the point are expressed as separate properties with unique names: Center/X, Center/Y, and Center/Z.

```c
Center/X (type: double) (LocalName: Center X) = 0.000000 
Center/Y (type: double) (LocalName: Center Y) = 5.000000 
Center/Z (type: double) (LocalName: Center Z) = 0.000000
```

The following examples show how to output the properties of an object with the dumpallproperties function:

```
; Properties are output as a single entry 
(dumpallproperties (entlast) 1) 

; Properties are output as separate entries 
(dumpallproperties (entlast))
```

Here is an example of the output created by the dumpallproperties function for a circle object. The output was generated with the expression `(dumpallproperties (entlast))`:

Now that you have seen an example output of an object with the dumpallproperties function, it is time to take a closer look at an individual property. The following line shows the Area property from the previous output. Table 16.7 explains the elements.

```
Area (type: double) (RO) (LocalName: Area) = 12.566371
```

NOTE: The data types that are listed by the dumpallproperties function aren't the same as those that you might be accustomed to for AutoLISP. For example, an AcString returns a string value, double is a real value, and AcDbObjectId is translated to an ename.

Table 16.7 dumpallproperties Area property description

|  Item | Description  |
|---|---|
|  Area |  The global name of the object's property. |
|  (type: double)  |  The data type for the value for the property. |
|  (RO) |  The property is read-only. |
|  (LocalName: Area) |  The local name of the object property. |
|  = 12.566371 | The value of the property. |

#### 6.4.2 Getting and Setting the Value of an Object Property

The getpropertyvalue and setpropertyvalue functions allow you to set an object's property. Use the dumpallproperties function on an ename to see the properties available for an object and the type of data that is expected. The following shows the syntax of the getpropertyvalue and setpropertyvalue functions:

```c
(getpropertyvalue ename property) 
(getpropertyvalue ename collection index subproperty) 

(setpropertyvalue ename property value) 
(setpropertyvalue ename collection index subproperty value)
```

Here are the arguments:

ename. The ename argument represents the entity name of the object for which you want to get or set a property value.

property. Use the property argument to specify a single-value property.

collection. Use the collection argument to specify a property that contains more than one value, such as vertices of a polyline.

index. Use the index argument to specify an item within a property collection.

subproperty. Use the subproperty argument to specify a subproperty within a property collection.

value. The value argument represents the value you want to assign the property.

The following examples show how to get and set the property values of a circle and a polyline with the getpropertyvalue and setpropertyvalue functions:

```c
; Creates a circle and polyline 
(command "._circle" "0,0" 1) 
(setq circ (entlast)) 
(command "._pline" "2,3" "1,4" "-3,-2" "") 
(setq pline (entlast)) 

; Outputs the radius of the circle 
(prompt (strcat "\nRadius: " (rtos (getpropertyvalue circ "radius")))) 
Radius: 1.0000nil 

; Outputs the last vertex of the polyline 
(prompt (strcat "\nVertex 3: " (vl-princ-to-string (getpropertyvalue pline "vertices" 2 "position")) )) 
Vertex 3: (-3.0 -2.0 0.0)nil 

; Changes the radius of the circle 
(setpropertyvalue circ "radius" 0.5) 
nil 

; Changes the position of the polyline's last vertex to the center of the circle 
(setq cenPt (getpropertyvalue circ "center")) 
(setpropertyvalue pline "vertices" 2 "position" cenPt) 
nil
```

1『上面的代码可以借鉴，实现直接修改块里面的属性值。待实现。（2020-10-30）』

Before you try to change a property value with setpropertyvalue, use the ispropertyreadonly function to determine if the property is read-only. ispropertyreadonly returns 1 if a property is read-only; 0 is returned when a property can be changed. The following shows the syntax of the ispropertyreadonly function:

```c
(ispropertyreadonly ename property) 
(ispropertyreadonly ename collection index subproperty)
```

The following examples show how to determine if a property for a line object is read-only with the ispropertyreadonly:

```c
; Creates a line 
(command "._line" "2,2" "5,6" "") 
(setq line (entlast)) 

; Tests to see if the Angle property is read-only 
(ispropertyreadonly line "angle") 
1 

; Tests to see if the StartPoint property is read-only 
(ispropertyreadonly line "startpoint")
0
```

This exercise shows how to modify the properties of a circle, line, and text object:

1 Create a new drawing.

2 Draw a circle (center at 4,5 and a radius of 3), a line (starts at -1,2 and ends at 8,15), and a single-line text object (insertion point of 0,0, a justification of middle center, a height of 4, and a value of A). The left side of Figure. 16.3 shows what the objects look like before they are modified.

3 At the AutoCAD Command prompt, type the following, pressing Enter after each line and selecting the object mentioned in the prompt:

```c
(setq circ (car (entsel "\nSelect circle: "))) 
(setq line (car (entsel "\nSelect line: "))) 
(setq text (car (entsel "\nSelect text: ")))
```

4 Type `(dumpallproperties circ 1)` and press Enter to display the properties of the circle. Do the same with the line and text variables.

5 Press F2 on Windows or Fn-F2 on Mac OS to expand the command-line window (or display the Text History window on Windows if the command-line window is docked). Review the properties and values of the objects.

6 Type the following and press Enter to change the circle's color to cyan, the line's color to blue, and the text's color to red:

```c
(setpropertyvalue circ "color" 4) 
(setpropertyvalue line "color" 5) 
(setpropertyvalue text "color" 1)
```

7 Type the following and press Enter to change the line's start point and the text's alignment point to the circle's center point:

```c
(setpropertyvalue line "startpoint" (getpropertyvalue circ "center")) 
(setpropertyvalue text "alignmentpoint" (getpropertyvalue circ "center"))
```

8 Type the following and press Enter to shorten the line so it intersects with the circle's radius:

```c
(setq ang (angle (getpropertyvalue line "startpoint") 
(getpropertyvalue line "endpoint") )) 
(setq newPt (polar (getpropertyvalue circ "center") ang (getpropertyvalue circ "radius") )) 
(setpropertyvalue line "startpoint" newPt)
```

Figure 16.3 Basics of a callout balloon

The three modified objects should now look like those on the right side of Figure 16.3.

#### 6.4.3 Updating an Object's Properties with an Entity Data List

Although the functions I mentioned in the previous section make working with object properties easier in recent releases, you should also understand how to modify the properties of an object with an entity data list. There are three main reasons why I recommend this:

1 Older programs modify objects using entity data lists; understanding how to update entity data lists will make it easier for you to update an existing program.

2 AutoCAD releases earlier than AutoCAD 2012 only support editing the properties of objects through entity data lists.

3 Entity data lists are used to create and define selection filters.

The entget function is used to return the entity data list of an object. Once you have an entity data list, you can then use the assoc function to locate the dotted pair that has the DXF group code as the key element you are interested in querying or modifying. After a dotted pair is retuned, you can then use the car function to get the key element of the list and the cdr function to get the value element of the dotted pair.

If you want to replace a dotted pair in an entity data list to change the value of a property, use the subst function. Then, after you update an entity data list, the changed entity data list must be committed to the object with the entmod function. After calling entmod, you should call the entupd function with the same object that was passed to the entget function to update the object's graphics onscreen.

The following shows the syntax of the entget, entmod, and entupd functions:

```c
(entget ename [apps]) 
(entmod ename) 
(entupd ename)
```

Here are the arguments:

ename. The ename argument specifies the entity name of the object you want update or to get an entity data list for.

apps. The apps argument is optional; it is a string value that specifies the application name of an extended data (XData) list that you want to retrieve. XData is custom information that can be attached to an object, such as a link to an external data source or date when an object was revised, and is similar to an entity data list associated with an ename. If an XData list with the application name is attached to the object, a list with both the entity data and XData is returned. Otherwise, just the entity data list for the object is returned. For more information on XData, see the「Extending the Information of an Object」section later in this chapter.

The following examples show how to get an entity data list with entget, modify an entity data list with entmod, and update an object in the drawing area with entupd:

```c
; Creates a new ellipse and gets the new object's entity name 
(entmake '((0. "ELLIPSE") (100. "AcDbEntity") (100. "AcDbEllipse") (10 6.0 2.0 0.0) (11 -4.0 0.0 0.0) (40. 0.5) (41. 0.0) (42. 6.28319))) 
(setq entityName (entlast)) 
<Entity name: 7ff6bc905dc0> 

; Gets the entity data list for the last object, which is the ellipse 
(setq entityData (entget entityName)) 
((-1. <Entity name: 7ff6bc905dc0>) (0. "ELLIPSE") (330. <Entity name: 7ff6bc9039f0>) (5. "1D4") (100. "AcDbEntity") (67. 0) (410. "Model") (8. "0") (100. "AcDbEllipse") (10 6.0 2.0 0.0) (11 -4.0 0.0 0.0) (210 0.0 0.0 1.0) (40. 0.5) (41. 0.0) (42. 6.28319)) 

; Gets the object's insertion/center point, center of the ellipse 
(setq dxfGroupCode10 (assoc 10 entityData)) 
(10 6.0 2.0 0.0) 

; Gets the object's color
; in this case nil is returned as a color isn't assigned 
(setq dxfGroupCode62 (assoc 62 entityData)) 
nil 

; Changes the object's center point to 0,0 
(setq entityData (subst '(10 0.0 0.0 0.0) dxfGroupCode10 entityData)) 
(10 6.0 2.0 0.0) 

; Appends a dotted pair to change the object's color 
(setq entityData (append entityData '((62. 3)))) 

; Modifies the object with the revised entity data list 
(entmod entityData) 
(entupd entityName)
```

1-2-3『

上面代码里，竟然可以通过扩展一个「点对值」达到修改颜色的目的，学到了，哈哈。下面的代码是数据流里修改块属性的逻辑，待重构。重构的时候正好结合作者的代码「Listing 16.1」。（2020-10-30）——未完成

```c
(defun ModifyPropertyValueByEntityName (entityNameList selectedName propertyValue / i ent blk entx propertyName)
  (setq i 0)
  (repeat (length entityNameList)
    ; get the entity information of the i(th) block
    (setq ent (entget (nth i entityNameList)))
    ; save the entity name of the i(th) block
    (setq blk (nth i entityNameList))
    ; get the property information
    (setq entx (entget (entnext (cdr (assoc -1 ent)))))
    (while (= "ATTRIB" (cdr (assoc 0 entx)))
      (setq propertyName (cdr (assoc 2 entx)))
      (if (= propertyName selectedName)
        (SwitchPropertyValueFromStringOrList propertyValue entx i)
      )
      ; get the next property information
      (setq entx (entget (entnext (cdr (assoc -1 entx)))))
    )
    (entupd blk)
    (setq i (+ 1 i))
  )
)

(defun SwitchPropertyValueFromStringOrList (propertyValue entx i / oldValue newValue)
  (setq oldValue (assoc 1 entx))
  (if (= (type propertyValue) 'list)
    (setq newValue (cons 1 (nth i propertyValue)))
    (setq newValue (cons 1 propertyValue))
  )
  (entmod (subst newValue oldValue entx))
)
```

』

Listing 16.1 is a set of two custom functions that simplify the process of updating an object using entity data lists and DXF group codes.

Listing 16.1: DXF helper functions

```c
; Listing 16.1: DXF helper functions
; Returns the value of the specified DXF group code for the supplied entity name
(defun Get-DXF-Value (entityName DXFcode / )
  (cdr (assoc DXFcode (entget entityName)))
)

; Sets the value of the specified DXF group code for the supplied entity name
(defun Set-DXF-Value (entityName DXFcode newValue / entityData newPropList
                                                    oldPropList)
  ; Get the entity data list for the object
  (setq entityData (entget entityName))

  ; Create the dotted pair for the new property value
  (setq newPropList (cons DXFcode newValue))
  (if (setq oldPropList (assoc DXFcode entityData))
    (setq entityData (subst newPropList oldPropList entityData))
    (setq entityData (append entityData (list newPropList)))
  )

  ; Update the object’s entity data list 
  (entmod entityData)

  ; Refresh the object on-screen
  (entupd entityName)
 
 ; Return the new entity data list
 entityData
)
```

The custom functions in Listing 16.1 are used in the next exercise. This exercise shows how to modify the properties of a circle, line, and text object:

1 Create a new drawing.

2 Use the appload command to load the `ch16_listings.lsp` file once it is downloaded from www.sybex.com/go/autocadcustomization.

3 Draw a circle (center at 4,5 and a radius of 3), a line (starts at -1,2 and ends at 8,15), and a single-line text object (insertion point of 0,0, a justification of middle center, a height of 4, and a value of A). Refer back to Figure 16.3; the left side shows what the objects look like before they are modified.

4 At the AutoCAD Command prompt, type the code in Listing 16.1. This will allow you to use the custom functions to make it easier to modify the properties of an object with an entity data list.

5 Type the following, pressing Enter after each line, and select the object mentioned in the prompt.

```c
(setq circ (car (entsel "\nSelect circle: "))) 
(setq line (car (entsel "\nSelect line: "))) 
(setq text (car (entsel "\nSelect text: ")))
```

6 Type `(dumpallproperties circ 1)` and press Enter to display the properties of the circle. Do the same with the line and text variables.

7 Press F2 on Windows or Fn-F2 on Mac OS to expand the command-line window (or display the Text History window on Windows if the command-line window is docked). Review the properties and values of the objects.

8 Type the following and press Enter to change the circle's color to cyan, the line's color to blue, and the text's color to red:

```c
(Set-DXF-Value circ 62 4) 
(Set-DXF-Value line 62 5) 
(Set-DXF-Value text 62 1)
```

9 Type the following and press Enter to change the line's start point and the text's alignment point to the circle's center point:

```c
(Set-DXF-Value line 10 (Get-DXF-Value circ 10)) 
(Set-DXF-Value text 11 (Get-DXF-Value circ 10))
```

10 Type the following and press Enter to shorten the line so it intersects with the circle's radius:

```c
(setq ang (angle (Get-DXF-Value line 10) (Get-DXF-Value line 11) )) 
(setq newPt (polar (Get-DXF-Value circ 10) ang (Get-DXF-Value circ 40) )) 
(Set-DXF-Value line 10 newPt)
```

The three modified objects should now look like those on the right side of Figure 16.3.

#### 6.4.4 Deleting an Object

An object that is no longer needed can be deleted from a drawing with the AutoLISP entdel function. Deleting an object from a drawing with the entdel function removes it from the display but doesn't remove the object from the drawing immediately. It flags an object for removal; the object is removed when the drawing is saved and then closed. You can use the entdel function a second time to restore the object while the drawing remains open. Using the AutoCAD u or undo command will also restore an object that was flagged for removal with the entdel function. Objects removed with the erase command can also be restored with the entdel function.

NOTE: The entdel function can be used to remove only graphical objects and objects associated with a dictionary, not symbol-table entries such as layers and block definitions. I discuss more about working with nongraphical objects in Chapter 17. The following shows the syntax of the entdel function:

```c
(entdel ename)
```

The ename argument represents the entity name of the object to flag for deletion or restore. The following examples show how to remove an object with the entdel function:

```c
; Gets the last object added to the drawing 
(setq en (entlast)) 
<Entity name: 7ff618a0be20> 

; Deletes the object assigned to the en variable 
(entdel en) 
<Entity name: 7ff618a0be20> ;

 Restores the object assigned to the en variable 
 (entdel en) 
 <Entity name: 7ff618a0be20>
```

#### 6.4.5 Highlighting Objects

Object highlighting is the feedback technique that AutoCAD uses to indicate which objects have been selected in the drawing area and are ready to be interacted with or modified. While highlighting is a great way to let a user know which objects will be modified, it can also impact the performance of a program when a large number of objects are selected. You can turn off general object-selection highlighting with the highlight system variable.

The AutoLISP redraw function, not the same as the redraw command, can be used to highlight individual objects. Highlighting generated by the redraw function can be undone, either with the redraw function or the AutoCAD regen command. In addition to highlighting an object, the redraw function can be used to temporarily hide and then redisplay an object. The following shows the syntax of the redraw function:

```c
(redraw [ename [mode]])
```

Here are the arguments:

ename .The ename argument represents the entity name of the object to highlight or display.

mode. The mode argument is an integer that specifies the highlight or display state of the object. Use the values 1 (show) and 2 (hide) to control the display of an object. The values 3 (on) and 4 (off) control the highlighting of the object.

The following examples show how to highlight and display an object with the redraw function:

```c
; Highlights the last graphical object in the drawing 
(redraw (entlast) 3) 

; Unighlights the object 
(redraw (entlast) 4) 

; Hides the object 
(redraw (entlast) 2) 

; Shows the object 
(redraw (entlast) 1)
```

### 6.5 Working with Complex Objects

Some objects in AutoCAD represent basic geometry such as circles and lines, whereas other objects are complex and made up of several objects. Complex objects require a bit more work to create and modify with AutoLISP. The two most common complex objects that you will find yourself working with are polylines and block references.

---

Thinking Ahead

Your boss comes to you and asks for a mock furniture layout for a new area in the office that your company is planning to renovate. Typically this is all handled by an outside firm, but your boss figures you can get the job done faster. After all, your boss is more concerned with getting the office layout completed than how to do the actual work.

Knowing that he's likely to ask for a layout of the whole floor—not just that small renovation area—you create blocks with attributes that allow you to get a quantity for each component. Instead of counting each component manually and then adding the component quantity to a table grid in the drawing, you automate the process. Using AutoLISP, you read the information from the attributes of each block and create an aggregated set of information that you use to create the table grid. Going forward, AutoLISP makes it easy to revise the table grid when your boss wants to change the layout at a later date.

---

#### 6.5.1 Creating and Modifying Polylines

AutoCAD drawings can contain two different types of polylines; old-style (legacy) and lightweight. Old-style polylines were the first type of polylines that were introduced in an early release of AutoCAD. An old-style polyline is composed of several objects: a main polyline object, vertex objects that define each vertex of the polyline, and a seqend object that defines the end of the polyline. Old-style polylines can be 2D or 3D and contain straight or curved segments.

Lightweight polylines, introduced with AutoCAD Release 14, take up less memory than old-style polylines but are 2D only. All 3D polylines are created using old-style polylines. Unlike old-style polylines, multiple objects aren't used to define a lightweight polyline. Most polylines created since AutoCAD Release 14 are most likely of the lightweight type. The plinetype system variable controls the type of polyline that is created with the pline command.

The following example creates an old-style polyline that has the coordinate values (0 0), (5 5), (10 5), and (10 0) with the entmake function:

```c
; Creates the base polyline object 
(entmake '((0. "POLYLINE") (100. "AcDbEntity") (100. "AcDb2dPolyline") (10 0.0 0.0 0.0) (70. 1))) 
((0. "POLYLINE") (100. "AcDbEntity") (100. "AcDb2dPolyline") (10 0.0 0.0 0.0) (70. 1)) 

; Adds the first vertex to the polyline at 0,0 
(entmake '((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 0.0 0.0 0.0) (91. 0) (70. 0) (50. 0.0))) 
((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 0.0 0.0 0.0) (91. 0) (70. 0) (50. 0.0)) 

; Adds the next vertex to the polyline at 5,5 
(entmake '((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 5.0 5.0 0.0) (91. 0) (70. 0) (50. 0.0))) 
((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 5.0 5.0 0.0) (91. 0) (70. 0) (50. 0.0)) 

; Adds the next vertex to the polyline at 10,5 
(entmake '((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 10.0 5.0 0.0) (91. 0) (70. 0) (50. 0.0))) 
((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 10.0 5.0 0.0) (91. 0) (70. 0) (50. 0.0)) 

; Adds the next vertex to the polyline at 10,0 
(entmake '((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 10.0 0.0 0.0) (91. 0) (70. 0) (50. 0.0))) 
((0. "VERTEX") (100. "AcDbEntity") (100. "AcDbVertex") (100. "AcDb2dVertex") (10 10.0 0.0 0.0) (91. 0) (70. 0) (50. 0.0)) 

; Adds the next vertex to the polyline at 10,0 
(entmake '((0. "SEQEND") (100. "AcDbEntity"))) 
((0. "SEQEND") (100. "AcDbEntity"))
```

When you want to modify an old-style polyline, get the polyline object and then use the entnext function to step to the first vertex until you get to the seqend object. Using a while looping statement is the best way to step through the drawing looking for each vertex of the polyline. Continue looping until you encounter a dotted pair with a DXF group code 0 and a value of "SEQEND".

Listing 16.2 is a custom function that demonstrates how to get each of the subobjects of an old-style polyline with the while function.

Listing 16.2: Listing subobjects of an old-style polyline

```c
; Listing 16.2: List subobjects of old-style polyline
(defun c:ListOSPolyline ( / entityName entityData dxfGroupCode0)
  ; Set PLINETYPE to 0 to create an old-style polyline with the PLINE command
  (setq entityName (car (entsel "\nSelect an old-style polyline: ")))
  (setq entityData (entget entityName))

  (if (= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) "POLYLINE")
    (progn
      (prompt (strcat "\n" dxfGroupCode0))
      (setq entityName (entnext entityName))
      (setq entityData (entget entityName))

      (while (/= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) "SEQEND")
        (prompt (strcat "\n" dxfGroupCode0))
        (prompt (strcat "\n" (vl-princ-to-string (assoc 10 entityData))))
        (setq entityName (entnext entityName))
        (setq entityData (entget entityName))
      )
    
      (prompt (strcat "\n" dxfGroupCode0))
    )
  )
 (princ)
)
```

The output generated by the custom ListOSPolyline function from Listing 16.2 will be similar to the following:

```c
POLYLINE 
VERTEX 
(10 0.0 0.0 0.0) 
VERTEX 
(10 5.0 5.0 0.0) 
VERTEX 
(10 10.0 5.0 0.0) 
VERTEX 
(10 10.0 0.0 0.0) 
SEQEND
```

For more information on the DXF entities polyline, vertex, and seqend, use the AutoCAD Help system. Search on the type of object you want to learn more about and be sure to include「DXF」as a keyword in the search. For example, the keyword search on the polyline object would be「polyline DXF.」

The following example creates a lightweight polyline that has the coordinate values (0 0), (5 5), (10 5), and (10 0) with the entmake function:

```c
; Create a polyline object drawn along the path (0 0), (5 5), (10 5), and (10 0) 
(entmake '((0. "LWPOLYLINE") (100. "AcDbEntity") (100. "AcDbPolyline") (90. 4) (70. 1) (43. 0) (10 0 0) (10 5 5) (10 10 5) (10 10 0))) 
((0. "LWPOLYLINE") (100. "AcDbEntity") (100. "AcDbPolyline") (90. 4) (70. 1) (43. 0) (10 0 0) (10 5 5) (10 10 5) (10 10 0))
```

The DXF group code 10 in the previous example appears multiple times in the entity data list. Each dotted pair with a DXF group code 10 represents a vertex in the polyline, and they appear in the order in which the polyline should be drawn. For more information on the lwpolyline DXF entity, search on「lwpolyline DXF」in the AutoCAD Help system.

The approaches to updating and querying an old-style and lightweight polyline vary, so you will need to handle each type using conditional statements in your programs. You can use the getpropertyvalue and setpropertyvalue functions to work with the Vertices property of both types of polylines to simplify the code you might need to write.

#### 6.5.2 Creating and Modifying with Block References

Block references are often misunderstood by new (and even experienced) AutoLISP developers. Blocks are implemented as two separate objects: block definitions and block references. Block definitions are nongraphical objects that are stored in a drawing and contain the geometry and attribute definitions that make up how the block should appear and behave in the drawing area. A block definition can also contain custom properties and dynamic properties.

---

Understanding Block Definitions and Block References

You can think of a block definition much like a cookie recipe. The recipe lists the ingredients that make up the cookie and explains how those ingredients are combined for a particular taste, but it doesn't control where the dough will be placed on the baking sheet or the size of the unbaked cookies. The placement and amount of the cookie dough on the sheet would be similar to a block reference in a drawing.

---

2『块定义和块参照，做一张术语卡片。』——已完成

A block reference displays an instance, not a copy, of the geometry from a block definition; the geometry exists only as part of the block definition, with the exception of attributes. Attribute definitions that are part of a block definition are added to a block reference as attributes unless the attribute definition is defined as a constant attribute. Constant attributes are parts of the geometry inherited from a block definition and aren't part of the block reference.

When creating a block reference with AutoLISP, as opposed to inserting it with the insert command, you are responsible for adding any attributes to the block reference that aren't designated as constant within the block definition. Like the old-style polyline, block references use the seqend object to designate the end of an insert object. Between the insert and seqend objects of a block reference are attrib objects that represent the attribute references that aren't set as constant and must be added to a block reference.

Since attributes must be added to a block reference, it is possible to have a block definition that contains attribute definitions and a block reference that points to that block definition without any attributes. It is also possible to have a block reference that has attributes attached to it and a block reference that doesn't have any attribute definitions.

The following code adds a block definition named RoomNum (see Figure 16.4) to a drawing that has a single attribute with the tag ROOM#:

```c
; Creates the block definition RoomNum 
(entmake (list (cons 0 "BLOCK") (cons 2 "roomnum") (cons 10 (list 18.0 9.0 0.0)) (cons 70 2))) 

; Creates the rectangle for around the block attribute 
(entmake (list (cons 0 "LWPOLYLINE") (cons 100 "AcDbEntity") (cons 100 "AcDbPolyline") 
  (cons 90 4) (cons 70 1) (cons 43 0) (cons 10 (list 0.0 0.0 0.0)) (cons 10 (list 36.0 0.0 0.0)) 
  (cons 10 (list 36.0 18.0 0.0)) (cons 10 (list 0.0 18.0 0.0)))
) 

; Adds the attribute definition 
(entmake (list (cons 0 "ATTDEF") (cons 100 "AcDbEntity") (cons 100 "AcDbText") 
  (cons 10 (list 18.0 9.0 0.0)) (cons 40 9.0) (cons 1 "L000") (cons 7 "Standard") 
  (cons 72 1) (cons 11 (list 18.0 9.0 0.0)) (cons 100 "AcDbAttributeDefinition") 
  (cons 280 0) (cons 3 "ROOM#") (cons 2 "ROOM#") (cons 70 0) (cons 74 2) (cons 280 1))
) 

; Ends block definition 
(entmake (list (cons 0 "ENDBLK")))
```

1『上面的是定义块属性，可以自己在图形界面里新建属性块，就如同在数据流模板里做的各个模块。（2020-10-30）』

Figure 16.4 RoomNum block reference inserted with AutoLISP

Once the block definition is created, you can then use the following code to add a block reference to a drawing based on a block named RoomNum:

```c
; Creates a block reference based on the block definition BlockNumber at 1.0,-0.5 
(entmake '((0. "INSERT")(100. "AcDbEntity")(100. "AcDbBlockReference") (66. 1) (2. "roomnum") (10 1.0 -0.5 0.0))) 
((0. "INSERT")(100. "AcDbEntity")(100. "AcDbBlockReference") (66. 1) (2. "RoomNum") (10 1.0 -0.5 0.0)) 

; Creates an attribute reference with the tag ROOM# and adds it to the block 
(entmake '((0. "ATTRIB") (100. "AcDbEntity") (100. "AcDbText") (10 0.533834 -0.7 0.0) 
  (40. 9.0) (1. "101") (7. "Standard") (71. 0) (72. 1) (11 1.0 -0.5 0.0) 
  (100. "AcDbAttribute") (280. 0) (2. "ROOM#") (70. 0) (74. 2) (280. 1))
) 
(entmake '((0. "ATTRIB") (100. "AcDbEntity") (100. "AcDbText") (10 0.533834 -0.7 0.0) 
  (40. 0.4) (1. "101") (7. "Standard") (71. 0) (72. 1) (11 1.0 -0.5 0.0) 
  (100. "AcDbAttribute") (280. 0) (2. "ROOM#") (70. 0) (74. 2) (280. 1))
) 

; Adds the end marker for the block reference 
(entmake ' ((0. "SEQEND") (100. "AcDbEntity"))) ((0. "SEQEND") (100. "AcDbEntity"))
```

If you want to extract the values of the attributes attached to a block, you must get the constant attribute values from the block definition and the nonconstant attribute values that are attached as part of the block reference. You use the entnext function to step through each object in a block definition and block reference, collecting information from the reference objects. All attribute definitions (attdef) or attribute reference (attrib) objects must be read until the last or seqend object is encountered.

Listing 16.3 shows a custom function that demonstrates how to step through a block reference and its block definition with the while function. You must load the custom functions in Listing 16.2 before executing the code in Listing 16.3. The code in Listing 16.2 and Listing 16.3 can be found in the `ch16_code_listings.lsp` file that is available for download from this book's website.

Listing 16.3: Listing attribute tags and values of a block

```c
; Listing 16.3: List attribute tags and values of a block
; Lists the attributes attached to a block reference and definition
(defun c:ListBlockAtts ( / entityName entityData dxfGroupCode0 blkName)

  ; Get a block reference
  (setq entityName (car (entsel "\nSelect a block reference: ")))
  (setq entityData (entget entityName))

  ; Check to see if the user selected a block reference
  (if (= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) "INSERT")
    (progn
      ; Output information about the block
      (prompt "\n*Block Reference*")
      (prompt (strcat "\n" dxfGroupCode0))
      (prompt (strcat "\nBlock name: " (setq blkName (cdr (assoc 2 entityData)))))

      ; Get the next object in the block, an attrib or seqend
      (setq entityName (entnext entityName))
      (setq entityData (entget entityName))

      ; Step through the attributes in the block reference
      (while (/= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) "SEQEND")
        (prompt (strcat "\n" dxfGroupCode0))
        (prompt (strcat "\nTag: " (cdr (assoc 2 entityData))))
        (prompt (strcat "\nValue: " (cdr (assoc 1 entityData))))
        (setq entityName (entnext entityName))
        (setq entityData (entget entityName))
      )
    
      (prompt (strcat "\n" dxfGroupCode0))

      ; Get the block definition
      (setq entityName (cdr (assoc -2 (tblsearch "block" blkName))))
      (setq entityData (entget entityName))

      (prompt "\n*Block Definition*")
      
      ; Step through the block definition and look for constant
      (while (/= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) nil)
        (if (and (= (setq dxfGroupCode0 (cdr (assoc 0 entityData))) "ATTDEF")
                (> (logand 2 (cdr (assoc 70 entityData))) 0)
          )
          (progn
            (prompt (strcat "\n" dxfGroupCode0))
            (prompt (strcat "\nTag: " (assoc 2 entityData)))
            (prompt (strcat "\nValue: " (assoc 1 entityData)))
          )
        )

        ; Get the next object
        (setq entityName (entnext entityName))
        (if entityName
          (setq entityData (entget entityName))
          (setq entityData nil)
        )
      )    
    )
  )
 (princ)
)
```

Here is an example of the output generated by the custom ListBlockAtts function:

```c
*Block Reference* 
INSERT Block name: RoomNumber 
ATTRIB Tag: ROOM# 
Value: 101 
SEQEND 
*Block Definition*
```

TIP: For more information on the DXF entities insert, attrib, and seqend, use the AutoCAD Help system. Search on the type of object you want to learn more about and be sure to include「DXF」as a keyword in the search. For example, the keyword search on the insert object would be「insert DXF.」

In addition to using entity data lists to query and modify block references, you can use the getpropertyvalue and setpropertyvalue functions. You learned about those functions in the「Listing and Changing the Properties of an Object Directly」section earlier in this chapter.

### 6.6 Extending an Object's Information

Each object in a drawing has a pre-established set of properties that define how that object should appear or behave. These properties are used to define the size of a circle or the location of a line within a drawing. Although you can't add a new property to an object with AutoLISP, you can append custom information to an object. The custom information that you can append to an object is known as extended data, or XData.

XData is structured similar to an entity data list except the values must be within a specific range of DXF group codes. Each XData list must contain an application name to identify one XData list from another since several XData lists can be attached to an object. After the application name, an XData list can contain any valid values and be of any type of data that AutoLISP supports.

The values in an XData list and what they represent is up to you, the creator of the data. Data in an XData list can be used to identify where an object should be placed or which layer it should be on, to store information about an external database record that is related to an object, or to build relationships between objects in a drawing. The way data is used or enforced is up to you as the programmer.

In addition to XData, graphical and nongraphical objects support what are known as extension dictionaries. Extension dictionaries are kind of like record tables that can be attached to an object. For example, you could store revision history of a drawing in an extension dictionary that is attached to model space, and then populate that information in the drawing's title block. I discuss creating custom dictionaries in Chapter 17.

2『 XData 做一张术语卡片。』——已完成

#### 6.6.1 Working with XData

Attaching XData to an object requires you to do some initial planning and perform several steps. The following outlines the steps that you must perform in order to attach an XData list to an object:

1 Define and register the application name to use.

2 Define the values that will make up the XData list.

3 Format the XData list; include a DXF group code -3, application name, and data values.

4 Get the entity name and entity data list of an object.

5 Append the XData list and update the object.

Prior to appending an XData list, you should check to see if the object already has one with the same application name attached to it. If that's the case, you should replace the current XData list with the new list. The following outlines the steps that you must perform in order to modify an XData list previously attached to an object:

1 Define the values that will make up the XData list.

2 Format the XData list; include a DXF group code -3, application name, and data values.

3 Get the entity name and entity data list of an object.

4 Check for an existing occurrence of an XData list for an object.

5 Substitute the current XData list attached to an object with the new XData list.

6 Update the object.

#### 6.6.2 Defining and Registering an Application Name

Before you can attach an XData list to an object, you must decide on an application name and then register that name with AutoCAD. The application name you choose should be unique to avoid conflicts with other XData lists. After an application name has been chosen, you register the name with the regapp function. The regapp function adds a new entry to the APPID symbol table and returns the name of the application if it is successfully registered. nil is returned if the application could not be registered or was already registered in the current drawing. You'll learn about symbol tables in Chapter 17. The following shows the syntax of the regapp function:

```c
(regapp appname)
```

The appname argument specifies a name for an application you want to register. The following example demonstrates how to register an application:

```c
; Registers the application named MyApp 
(setq appName "MyApp") 
(regapp appName)
```

#### 6.6.3 Attaching XData to an Object

Once you have defined an application name and registered it in a drawing, you can attach an XData list to an object within that drawing. An XData list is made up of two lists and has a total size limit of 16 KB per object (see the「Managing the Memory Used by XData for an Object」sidebar for information). The outer list contains a DXF group code -3 and an inner list that contains the application name and dotted pairs that represent the data values to store with the object. Each dotted pair contains a DXF group code that defines the type of data the pair represents and then the actual value of the pair.

DXF group codes used for dotted pairs in an XData list must be within the range of 1000 to 1071. Each DXF group code value in that range represents a different type of data, and you can use each DXF group code more than once in an XData list. Table 16.8 lists some of the commonly used DXF group codes for XData.

Table 16.8 XData-related DXF group codes

|  DXF group code | Description  |
|---|---|
|  1000  |  String value |
|  1001 |  Application name |
|  1010  |  3D point |
|  1040 |  Real numeric value |
|  1070 |  16-bit (unsigned or signed) integer value |
|  1071 |  32-bit signed integer value |

The following example is an XData list that contains the application name MyApp and two dotted pairs. The first dotted pair is a string `(DXF group code 1000)` with the value「My custom application,」and the second dotted pair is an integer (DXF group code 1070) with a value that represents the current date:

```c
(-3 ("MyApp" 
      (1000. "My custom application") 
      (1070. (fix (getvar "cdate")))
    )
)
```

The following AutoLISP statements were used to create the previous XData list:

```c
(setq appName "MyApp") 
(regapp "MyApp") 
(setq xdataList 
  (list -3 (list appName 
                 (cons 1000 "My custom application") 
                 (cons 1070 (fix (getvar "cdate")))))
)
```

1『这里意外收获，通过系统函数获取时间，这个时间可以做一个时间戳，当作数据的临时 ID，时间戳基本不会重复的。（2020-10-31）』

Once an XData list has been defined, it can be appended to an entity data list returned by the AutoLISP entget function with the append function. I explained how to append lists together in Chapter 14. After an XData list is appended to an entity data list, you use the entmod function to commit changes to the object and entupd to update the object in the drawing area. I explained the entmod and entupd functions earlier in this chapter. This exercise shows how to attach an XData list to a circle:

1 At the AutoCAD Command prompt, type the following and press Enter to register the MyApp application:

```c
(setq appName "MyApp") 
(regapp appName)
```

2 Type the following and press Enter to assign the XData list to the xdataList variable: 

```c
(setq xdataList 
  (list -3 (list appName 
                 (cons 1000 "My custom application") 
                 (cons 1070 (fix (getvar "cdate")))))
)
```

The XData list assigned to the xdataList variable is as follows:

```c
(-3 ("MyApp" (1000. "My custom application") (1070. 20140302)))
```

3 Type the following and press Enter to create a new circle: 

```c
(entmake (list (cons 0 "CIRCLE") (cons 10 (list 2 2 0)) (cons 40 1))) 
(setq circ (entlast))
```

A circle with the center point of 2,2 is created with a radius of 1, and the entity name of the new circle is assigned to the circ variable.

4 Type the following and press Enter to get the entity data list of the circle and assign it to the entData variable: 

```c
(setq entityData (entget circ))
```

The entity data list of the circle should be similar to the following:

```c
((-1. <Entity name: 7ff722905e90>) (0. "CIRCLE") (330. <Entity name: 7ff7229039f0>) (5. "1E1") (100. "AcDbEntity") (67. 0) (410. "Model") (8. "0") (100. "AcDbCircle") (10 2.0 2.0 0.0) (40. 1.0) (210 0.0 0.0 1.0))
```

5 Type the following and press Enter to append the lists in the entityData and xdataList variables: 

```c
(setq entityData (append entityData (list xdataList)))
```

The resulting list is assigned to the entityData variable and should look similar to the following:

```c
((-1. <Entity name: 7ff722905e50>) (0. "CIRCLE") (330. <Entity name: 7ff7229039f0>) (5. "1DD")(100. "AcDbEntity") (67. 0) (410. "Model") (8. "0")(100. "AcDbCircle") (10 2.0 2.0 0.0) (40. 1.0) (210 0.0 0.0 1.0)(-3 ("MyApp" (1000. "Drill_Hole") (1070. 20140302))))
```

6 Type the following and press Enter to commit the changes to the circle and update the circle's display: 

```c
(entmod entityData) 
(entupd circ)
```

The circle object won't look any different after the changes have been committed because the XData doesn't affect the appearance of the object. However, you can now differentiate this circle from those that might be created with the circle command. This makes it much easier to locate and update the radius of the circles that represent a drill hole in your drawing.

---

Managing the Memory Used by XData for an Object

Each object in a drawing can have a total of 16 KB worth of XData attached to it. The 16 KB total is for all XData attached to an object, and not just for one application. If the limit of XData is close and you attach additional XData that exceeds the limit, the XData won't be attached. AutoLISP provides two functions to help determine the size of the XData being attached to an object and the amount of space already being used by the XData attached to an object.

The two AutoLISP functions used to manage XData are as follows:

xdroom—Returns the space available, in bytes, for attaching new XData to an object. The function expects an entity name as its single argument.

xdsize—Returns the size of an XData list in bytes. The function expects a list as its single argument.

You should use these two functions to determine whether XData can be attached to an object.

---

#### 6.6.4 Querying and Modifying the XData Attached to an Object

XData that has been previously attached to an object can be queried and modified by following a process that is similar to the one used to attach XData to an object. The entget function, which I discussed earlier, is used to get the entity data list and any XData lists attached to an object. By default, the entget function only returns the entity data list for the entity name that it is passed. You use the optional appname argument of the entget function to return all of the XData lists attached to an object or the one associated with a specific application name.

For example, the following code returns the entity data list and XData list attached to an object with the application name of MyApp. If there is no XData list associated with the application name MyApp, only the entity data list for the object is returned.

```c
; Return the entity data list and xdata list 
(entget (entlast) '("MyApp"))
```

Using an asterisk instead of an actual application name returns the XData lists for all applications attached to an object, as shown here:

```c
; Return the entity data list and xdata list 
(entget (entlast) '("*"))
```

This exercise shows how to list the XData attached to a dimension with a dimension override:

1 At the AutoCAD Command prompt, type dli press Enter.

2 At the Specify first extension line origin or `<select object>`: prompt, specify a point in the drawing.

3 At the Specify second extension line origin: prompt, specify a second point in the drawing.

4 At the Specify dimension line location or [Mtext/Text/Angle/Horizontal/Vertical/Rotated]: prompt, specify a point in the drawing to place the linear dimension.

5 Select the linear dimension that you created, right-click, and then click Properties.

6 In the Properties palette (Windows) or Properties Inspector (Mac OS), click the Arrow 1 field under the Lines & Arrows section. Select None from the drop-down list. The first arrowhead of the linear dimension is suppressed as a result of a dimension override being created.

7 At the AutoCAD Command prompt, type `(assoc -3 (entget (car (entsel "\nSelect object with attached xdata: ")) '("*")))` and press Enter. Attaching an XData list to the linear dimension is how AutoCAD handles dimension overrides for individual dimensions. Here is what the XData list that was attached to the linear dimension as a result of changing the Arrow 1 property in step 6 looks like:

```c
(-3 ("ACAD" (1000. "DSTYLE") (1002. "{") (1070. 343) (1005. "2BE") (1070. 173) (1070. 1) (1070. 344) (1005. "0") (1002. "}")))
```

NOTE: I mentioned earlier that XData doesn't affect the appearance of an object, and that is still true even when used as we did in the previous exercise. XData itself doesn't affect the object, but AutoCAD does look for its own XData and uses it to control the way an object might be drawn. If you implement an application with the Autodesk® ObjectARX® application programming interface, you could use ObjectARX and XData to control how an object is drawn onscreen. You could also control the way an object looks using object overrules with Managed.NET and XData. ObjectARX and Managed.NET are the two advanced programming options that Autodesk supports for AutoCAD development. You can learn more about ObjectARX and Managed.NET at www.objectarx.com.

The entget function can be used to determine whether an XData list for a specific application is already attached to an object. If an XData list already exists for an object, you can then modify that list. Use the subst function to update or replace one XData list with another.

This exercise shows how to override the color assigned to dimension and extension lines, and restore the arrowhead for the dimension you created in the previous exercise:

1 At the AutoCAD Command prompt, type the following and press Enter:

```c
(setq entityName (car (entsel "\nSelect dimension: ")))
```

2 At the Select dimension: prompt, select the linear dimension created in the previous exercise.

3 At the AutoCAD Command prompt, type the following and press Enter to get the entity data list and XData list associated with an application named ACAD:

```c
(setq entityData (entget entityName '("ACAD")))
```

4 Type the following and press Enter to assign the xdataList variable with the new XData list to change the color of the dimension line to ACI 40 and the color of the extension line to ACI 200:

```c
(setq xdataList 
  '(-3 ("ACAD" (1000. "DSTYLE") (1002. "{") (1070. 177) (1070. 200) (1070. 176) (1070. 40) (1002. "}")))
)
```

5 Type the following and press Enter to check whether there is an XData list already attached to the object, and if so replace it with the new XData list:

```c
(if (/= (assoc -3 entityData) nil) 
  (setq entityData (subst xdataList (assoc -3 entityData) entityData)) 
)
```

6 Type the following and press Enter to update the linear dimension and commit the changes to the drawing: 

```c
(entmod entityData) 
(entupd entityName)
```

The colors of the lines in the dimension that are inherited from the dimension style are now overridden. This is similar to what happens when you select a dimension, right-click, and choose Precision.

1-2『上面介绍了修改 XData 的具体方法，以后要实现的一个重要功能需要借鉴里面的代码。管道号块的插入点结合多段线的坐标点（单一直线有 2 个 dxf code 为 10 的点、折一下的有 3 个点，折 2 下有 4 个点），给每个多段线打上管道号的标签，此标签存在 XData。反向再通过多段线给每个阀门（采用区域覆盖的块）打上管线号的标签。那么阀门和管线号的数据就关联上了，管段表和材料表就可以自动生成了，哈哈。做一张主题卡片。（2020-10-32）』

#### 6.6.5 Removing XData from an Object

XData can be removed from an object when it is no longer needed. You do so by replacing an existing XData list with an XData list that contains only an application name. When AutoCAD evaluates an XData list with only an application name and no values, it removes the XData list from the object. Here is an example of an XData list that can be used to remove the XData associated with the MyApp application:

```c
(-3 ("MyApp"))
```

The following example removes the XData list associated with an application named ACAD from a dimension, which removes all overrides assigned to the dimension:

```c
(defun c:RemoveDimOverride (/ entityName entityData) 
  (setq entityName (car (entsel "\nSelect dimension to remove overrides: "))) 
  (setq entityData (entget entityName '("ACAD"))) 
  (if (/= (assoc -3 entityData) nil) 
    (setq entityData (subst '(-3 ("ACAD")) (assoc -3 entityData) entityData)) 
  ) 
  (entmod entityData) 
  (entupd entityName) 
  (princ) 
)
```

#### 6.6.6 Selecting Objects Based on XData

You can use the XData attached to an object as a way to select or filter out specific objects with the ssget function. (I explained how to use the filter argument of the ssget function in the「Filtering Selected Objects」section earlier in this chapter.) If you want to filter on the XData attached to an object, you use the DXF group code -3 along with the application name from the XData list.

Here are two examples of the ssget function that use a selection filter to allow for the selection of objects that only have XData attached to them with a specific application name:

```c
; Selects objects containing xdata and with the application name MyApp. 
(ssget '((-3 ("MyApp")))) 

; Uses implied selection and selects objects with the application name ACAD. 
(ssget "_I" '((-3 ("ACAD"))))
```

### 6.7 Exercise: Creating, Querying, and Modifying Objects

In this section, you will continue to work with the drawplate function that was originally introduced in Chapter 12,「Understanding AutoLISP.」Along with working with the drawplate function, you will define a new function that will be used to create a bill of materials (BOM) for a furniture layout. The key concepts I cover in this exercise are as follows:

1 Creating and Modifying Objects without Commands AutoCAD commands make getting started with AutoLISP easier, but not all objects can be created from the Command prompt, nor can all the properties of an object be modified from the Command prompt. The entmake, entget, entmod, and entupd functions give you much greater control over the objects you are creating or modifying.

2 Creating Selection Sets Requesting objects from the user allows you to create custom functions that can modify select objects instead of all objects in a drawing.

3 Stepping Through Objects in a Selection Set Selection sets can contain one or several thousand objects. You must use a looping function, such as repeat or while, to step through and get each object in the selection set.

NOTE: The steps in this exercise depend on the completion of the steps in the「Exercise: Getting Input from the User to Draw the Plate」section of Chapter 15,「Requesting Input and Using Conditional and Looping Expressions.」If you didn't complete the steps, do so now or start with the `ch16_drawplate.lsp` and `ch16_utility.lsp` sample files available for download from www.sybex.com/go/autocadcustomization. These sample files should be placed in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the LSP files. Once the sample files are stored on your system, remove the characters `ch16_ from` the name of each file.

```c
; Draws a rectangular plate that is 5x2.75
(defun c:drawplate ( / pt1 pt2 pt3 pt4 width height insPt textValue
                       cenPt1 cenPt2 cenPt3 cenPt4 old_vars hole_list)

  ; Store and change the value of the system variables
  (setq old_vars (get-sysvars '("osmode" "clayer" "cmdecho")))
  (set-sysvars '("osmode" "clayer" "cmdecho") '(0 "0" 0))

  ; Create the layer named Plate or set it current
  (createlayer "Plate" 5)

  ; Define the width and height for the plate
  (if (= *drawplate_width* nil) 
    (setq *drawplate_width* 5.0)
  )
  (if (= *drawplate_height* nil) 
    (setq *drawplate_height* 2.75)
  )

  ; Get recently used values from the global variables
  (setq width *drawplate_width*)
  (setq height *drawplate_height*)

  ; Prompt the current values
  (prompt (strcat "\nCurrent width: "
		  (rtos *drawplate_width* 2)
		  "  Current height: "
		  (rtos *drawplate_height* 2)
    )
  )
  
  ; Setup default keywords
  (initget "Width Height")

  ; Continue to ask for input until a point is provided
  (while (/= (type
	       (setq basePt
		      (getpoint "\nSpecify base point for plate or [Width/Height]: "))
	     )
	     'LIST
	  ) 
    (cond
      ; Prompt for the width of the plate
      ((= basePt "Width") 
          (setq width (getdist (strcat "\nSpecify the width of the plate <"
			               (rtos *drawplate_width* 2) ">: ")))
          ; If nil is returned, use the previous value from the global variable
          (if (/= width nil) 
            (setq *drawplate_width* width)
          )
      )
      ; Prompt for the height of the plate
      ((= basePt "Height") 
          (setq height (getdist (strcat "\nSpecify the height of the plate <"
			                (rtos *drawplate_height* 2) ">: ")))
          ; If nil is returned, use the previous value from the global variable
          (if (/= height nil) 
            (setq *drawplate_height* height)
          )
      )
    )
    ; Setup default keywords again
    (initget "Width Height")
  )
  
  ; Set the coordinates to draw the rectangle
  (setq pt1 basePt
	;| lower-left corner  |;
        pt2 (list (+ (car basePt) width) (cadr basePt) 0)
	;| lower-right corner |;
        pt3 (list (+ (car basePt) width) (+ (cadr basePt) height) 0)
	;| upper-right corner |;
        pt4 (list (car basePt) (+ (cadr basePt) height) 0)
	;| upper-left corner  |;
  )

  ; Draw the rectangle
  (createrectangle pt1 pt2 pt3 pt4)

  ; Create the layer named Holes or set it current
  (createlayer "Holes" 1)

  ; Calculate the placement of the circle in the lower-left corner  
  ; Calculate a new point at 45 degrees and distance of 0.7071 from pt1
  (setq cenPt1 (polar pt1 (/ PI 4) 0.7071))

  ; Calculate the next point from cenPt along the same angle
  ; as the line drawn between pt1 and pt2, and 1 unit less
  ; than the distance between pt1 and pt2 
  (setq cenPt2 (polar cenPt1 (angle pt1 pt2) (- (distance pt1 pt2) 1)))

  ; Calculate the final two points based on cenPt1 and cenPt2
  (setq cenPt3 (polar cenPt2 (angle pt2 pt3) (- height 1))
        cenPt4 (polar cenPt1 (angle pt1 pt4) (- height 1)))
  
  ; Append all the calculated center points to a single list
  (setq hole_list (append (list cenPt1)
                          (list cenPt2)
                          (list cenPt3)
                          (list cenPt4)))

  ; Execute the createcircle function for each point
  ; list in the in the hole_list variable
  (foreach cenPt hole_list
    (createcircle cenPt 0.1875)
  )

  ; Set the insertion point for the text label
  (setq insPt (getpoint "\nSpecify label insertion point: "))

  ; Define the label to add
  (setq textValue (strcat "Plate Size: "
                          (vl-string-right-trim " .0" (rtos width 2 2))
                          "x"
                          (vl-string-right-trim " .0" (rtos height 2 2))
                  )
  )

  ; Create label
  (createlayer "Label" 7)
  (createtext insPt "_c" 0.5 0.0 textValue)

  ; Restore the value of the system variables
  (set-sysvars '("osmode" "clayer" "cmdecho") old_vars)

  ; Save previous values to global variables
  (setq *drawplate_width* width)
  (setq *drawplate_height* height)

 ; Exit "quietly"
 (princ)
)
```

#### 6.7.1 Revising the Functions in utility.lsp

The changes to the utility.lsp file replace the use of AutoCAD commands to create objects with the entmake function and entity data lists. With these changes, you don't need to worry about the current setting of the osmode and other drafting-related system variables. Creating objects with the entmake function also doesn't display Command prompt strings at the command-line window; such strings would need to be suppressed with the cmdecho system variable otherwise. Remember, if something happens to go wrong, the fewer system variables you have changed, the better off you and your end users are.

As you revise the functions, notice how easy it can be to change the underlying functionality of your programs when they are divided into several smaller functions. Smaller functions are easier not only to change, but to retest if a problem is encountered.

1『一直在贯彻这一思维，拆分成一个个功能单一的小函数。（2002-10-31）』

The following steps explain how to update the various functions in the utility.lsp file:

Open the utility.lsp file in Notepad on Windows or TextEdit on Mac OS. In the text editor area, update the createrectangle, createtext, and createcircle functions to match the following:

```c
; CreateLayer function creates/modifies a layer and expects to argument values.
(defun createlayer (name color / )
  (command "._-layer" "_m" name "_c" color "" "")
)

; Createrectangle function draws a four-sided closed object.
(defun createrectangle (pt1 pt2 pt3 pt4 /)
  (entmake (list (cons 0 "LWPOLYLINE") (cons 100 "AcDbEntity")
                 (cons 100 "AcDbPolyline") (cons 90 4) (cons 70 1) (cons 43 0)
                 (cons 10 pt1) (cons 10 pt2) (cons 10 pt3) (cons 10 pt4)))
)

; Createtext function creates a single line text object.
(defun createtext (insertionPoint alignment height rotation textString / )
  (entmake (list (cons 0 "TEXT") (cons 100 "AcDbEntity") (cons 100 "AcDbText")
                 (cons 10 insertionPoint) (cons 40 height) (cons 1 textString)
                 (cons 50 0.0) (cons 7 "Standard") (cons 72 1)
                 (cons 11 insertionPoint) (cons 100 "AcDbText") (cons 73 0)))
)

; Get-Sysvars function returns a list of the current values
; of the list of system variables it is passed.
; 
; Arguments:
;  sysvar-list - A list of system variables
; 
; Usage: (get-sysvars (list "clayer" "osmode"))
;
(defun get-sysvars (sysvar-list / values-list)
  ; Creates a new list based on the values of the
  ; system variables in sysvar-list
  (foreach sysvar sysvar-list
    ; Get the value of the system variable and add it to the list
    (setq values-list (append values-list (list (getvar sysvar))))
  )

 ; List to return
 values-list
)

; Set-Sysvars function sets the system variables in the
; sysvar-list to the values in values-list.
; 
; Arguments:
;  sysvar-list - A list of system variables
;  values-list - A list of values to set to the system variables
; 
; Usage: (set-sysvars (list "clayer" "osmode") (list "Plate" 0))
;
(defun set-sysvars (sysvar-list values-list / cnt)
  ; Set the counter to 0
  (setq cnt 0)
  ; Step through each variable and set its value.
  (foreach sysvar sysvar-list
    (setvar sysvar (nth cnt values-list))
    ; Increment the counter
    (setq cnt (1+ cnt))
  )
 (princ)
)

; CreateCircle function draws a circle object.
; 
; Arguments:
;  cenpt - A string or list that represents the center point of the circle
;  rad - A string, integer, or real number that represents the circle’s radius
; 
; Usage: (createcircle "0,0" 0.25)
;
(defun createcircle (cenpt rad / )
  (entmake (list (cons 0 "circle") (cons 10 cenpt) (cons 40 rad)))
)

; Returns the value of the specified DXF group code for the supplied entity name
(defun Get-DXF-Value (entityName DXFcode / )
  (cdr (assoc DXFcode (entget entityName)))
)

; Sets the value of the specified DXF group code for the supplied entity name
(defun Set-DXF-Value (entityName DXFcode newValue / entityData newPropList oldPropList)
  ; Get the entity data list for the object
  (setq entityData (entget entityName))

  ; Create the dotted pair for the new property value
  (setq newPropList (cons DXFcode newValue))
  (if (setq oldPropList (assoc DXFcode entityData))
    (setq entityData (subst newPropList oldPropList entityData))
    (setq entityData (append entityData (list newPropList)))
  )

  ; Update the object’s entity data list 
  (entmod entityData)

  ; Refresh the object on-screen
  (entupd entityName)
 
 ; Return the new entity data list
 entityData
)
```

Click File Save.

#### 6.7.2 Testing the Changes to the drawplate Function

Although the changes you made to the utility.lsp file weren't made directly to the drawplate function, drawplate uses the createrectangle, createtext, and createcircle functions to simplify its code. If the changes were made correctly to the utility.lsp file, you should see no differences in the objects created by the drawplate function when compared the one created in Chapter 15.

The following steps explain how to load the LSP files into AutoCAD and then start the drawplate function:

1 Start the appload command. Load the LSP files drawplate.lsp and utility.lsp. If the File Loading - Security Concerns message box is displayed, click Load.

2 At the Command prompt, type drawplate and press Enter.

3 Press F2 on Windows or Fn-F2 on Mac OS to expand the command-line window. The current width and height values for the plate are displayed in the command-line history.Current width: 5.0000 Current height: 2.7500

4 At the Specify base point for the plate or [Width/Height]: prompt, type w and press Enter.

5 At the Specify the width of the plate `<5.0000>`: prompt, type 3 and press Enter.

6 At the Specify base point for the plate or [Width/Height]: prompt, type h and press Enter.

7 At the Specify the height of the plate `<2.7500>`: prompt, type 4 and press Enter.

8 At the Specify base point for the plate or [Width/Height]: prompt, pick a point in the drawing area to draw the plate and holes based on the width and height values specified.

9 At the Specify label insertion point: prompt, pick a point in the drawing area below the plate to place the text label.

10 Zoom to the extents of the drawing. Figure 16.5 shows the completed plate.

Figure 16.5 The completed plate created using the updated utility functions

#### 6.7.3 Defining the New Get-DXF-Value and Set-DXF-Value Utility Functions

Modifying objects using entity data lists might seem confusing to you—and you aren't alone if you feel that way. Entity data lists can even be confusing to some of the most veteran programmers at times, as they are not used all the time. Most veteran programmers create utility functions that simplify the work.

In my personal utility library, I have two functions named Get-DXF-Value and Set-DXF-Values that can be used to manipulate entity data lists. The Get-DXF-Value function gets the value of a dotted pair based on a DXF group code in an entity data list, whereas Set-DXF-Values replaces a dotted pair or appends a new dotted pair in an entity data list. Set-DXF-Values can be used to construct an entity data list as well. The following steps explain how to define the Get-DXF-Value and Set-DXF-Values custom functions:

Open the utility.lsp file in Notepad on Windows or TextEdit on Mac OS, if it is not already open from the previous steps.

In the text editor area, position the cursor after the last expression in the file and press Enter twice. Then type the following:

```c
; Returns the value of the specified DXF group code for the supplied entity name
(defun Get-DXF-Value (entityName DXFcode / )
  (cdr (assoc DXFcode (entget entityName)))
)

; Sets the value of the specified DXF group code for the supplied entity name
(defun Set-DXF-Value (entityName DXFcode newValue / entityData newPropList oldPropList)
  ; Get the entity data list for the object
  (setq entityData (entget entityName))

  ; Create the dotted pair for the new property value
  (setq newPropList (cons DXFcode newValue))
  (if (setq oldPropList (assoc DXFcode entityData))
    (setq entityData (subst newPropList oldPropList entityData))
    (setq entityData (append entityData (list newPropList)))
  )

  ; Update the object’s entity data list 
  (entmod entityData)

  ; Refresh the object on-screen
  (entupd entityName)
 
 ; Return the new entity data list
 entityData
)
```

Click File Save.

#### 6.7.4 Moving Objects to Correct Layers

Not everyone will agree on the naming conventions, plot styles, and other various aspects of layers, but there are a few things drafters can agree on when it comes to layers—that objects should do the following: 1) Inherit their properties, for the most part, from the layers in which they are placed. 2)Only be placed on layer 0 when creating blocks.

While I would like to think all the drawings I've created are perfect, I know that rush deadlines or other distractions may have affected quality. Maybe the objects were placed on the wrong layer or maybe it wasn't my fault and standards simply changed during the course of a project. With AutoLISP, you can identify potential problems in a drawing to let the user know about them so they can be fixed, or you can make the changes using AutoLISP.

In these steps, you create a custom function named furnlayers that is used to identify objects by type and value to ensure they are placed on the correct layer. This is achieved using selection sets and entity data lists, along with looping and conditional statements. 

Create a new LSP file named furntools.lsp with Notepad on Windows or TextEdit on Mac OS. In the text editor area of the furntools.lsp file, type the following:

```c
; Moves objects to the correct layers based on a set of established rules
(defun c:FurnLayers ( / ssFurn cnt entityName entityData entityType) 

  ; Request the user to select objects
  (setq ssFurn (ssget))

  ; Proceed if ssFurn is not nil
  (if ssFurn
    (progn
      ; Set up the default counter
      (setq cnt 0)

      ; Step through each block in the selection set
      (while (> (sslength ssFurn) cnt)
        ; Get the entity name and entity data of the object
        (setq entityName (ssname ssFurn cnt)
              entityData (entget entityName)
              entityType (strcase (Get-DXF-Value entityName 0)))

	; Conditional statement used to branch based on object type
	(cond
	  ; If object is a block, continue
	  ((= entityType "INSERT")
            (cond
	      ; If the block name starts with RD or CD,
	      ; then place it on the surfaces layer
	      ((wcmatch (strcase (Get-DXF-Value entityName 2)) "RD*,CD*")
                (Set-DXF-Value entityName 8 "surfaces")
	      )
	      ; If the block name starts with PNL, PE, and PX,
	      ; then place it on the panels layer
	      ((wcmatch (strcase (Get-DXF-Value entityName 2)) "PNL*,PE*,PX*")
                (Set-DXF-Value entityName 8 "panels")
	      )
	      ; If the block name starts with SF,
	      ; then place it on the panels layer
	      ((wcmatch (strcase (Get-DXF-Value entityName 2)) "SF*")
                (Set-DXF-Value entityName 8 "storage")
	      )	      
	    )
	  )
	  ; If object is a dimension, continue
	  ((= entityType "DIMENSION")
	    ; Place the dimension on the dimensions layer
            (Set-DXF-Value entityName 8 "dimensions")
	  )
	)

        ; Increment the counter by 1
        (setq cnt (1+ cnt))
      )
    )
  )
 (princ)
)
```

#### 6.7.5 Creating a Basic Block Attribute Extraction Program

The designs you create take time and, based on the industry you are in, are often what is used to earn income for your company or even save money. Based on the types of objects in a drawing, you can step through a drawing and get attribute information from blocks or even geometric values such as lengths and radii of circles. You can use the objects in a drawing to estimate the potential cost of a project or even provide information to manufacturing.

In these steps, you create a custom function named furnbom that is used to get the values of two attributes (part and label) attached to a block. The attribute values are added to a list and then sorted using the acad_strlsort function. Once sorted, the list is then parsed and quantified into a new list, which is used to create the a BOM table made up of lines and text.

1 Open the furntools.lsp file with Notepad on Windows or TextEdit on Mac OS, if it is not already open. 

2 In the text editor area of the furntools.lsp file, type the following:

```c
; extAttsFurnBOM - Extracts, sorts, and quanitifies the attribute information
(defun extAttsFurnBOM (ssFurn / cnt preVal part label furnList)
  ; Set up the default counter
  (setq cnt 0)

  ; Step through each block in the selection set
  (while (> (sslength ssFurn) cnt)
    ; Get the entity name and entity data of the block
    (setq entityName (entnext (ssname ssFurn cnt)))
    (setq entityData (entget entityName))

    ; Step through the objects that appear after
    ; the block reference, looking for attributes
    (while (/= (cdr (assoc 0 entityData)) "SEQEND")
      ; Check to see which if the attribute tag is PART or TAG
      (cond
        ((= (strcase (Get-DXF-Value entityName 2)) "PART")
          (setq part (Get-DXF-Value entityName 1))
        )
        ((= (strcase (Get-DXF-Value entityName 2)) "LABEL")
          (setq label (Get-DXF-Value entityName 1))
        )
      )
      
      ; Get the next entity (attribute or sequence end)
      (setq entityName (entnext entityName))
      (setq entityData (entget entityName))
    )

    ; Add the part and label values to the list
    (setq furnList (append furnList
                           (list (strcat label "\t" part))
			   ))

    ; Increment the counter by 1
    (setq cnt (1+ cnt))
  )

  ; Sort the list of parts and labels
  (setq furnListSorted (acad_strlsort furnList))

  ; Reset and set variables that will be used in the looping statement
  (setq cnt 0
        furnList nil preVal nil)

  ; Quantify the list of parts and labels
  ; Step through each value in the sorted list
  (foreach val furnListSorted
    ; Check to see if the previous value is the same as the current value
    (if (or (= preVal val)(= preVal nil))
      (progn
        ; Increment the counter by 1
        (setq cnt (1+ cnt))
      )
      
      ; Values weren't the same, so record the quanity
      (progn
	
        ; Add the quanity and the value (part/label) to the final list
        (setq furnList (append furnList 
                           (list (list (itoa cnt)
                                 (substr preVal 1 (vl-string-search "\t" preVal))
                                 (substr preVal (+ (vl-string-search "\t" preVal) 2)))
                           )))
        ; Reset the counter
        (setq cnt 1)
      )
    )

    ; keep the previous value for comparison
    (setq preVal val)   
  )

  ; Add the quanity and the value (part/label) to the final list
  (setq furnList (append furnList 
                     (list (list (itoa cnt)
                           (substr preVal 1 (vl-string-search "\t" preVal))
                           (substr preVal (+ (vl-string-search "\t" preVal) 2)))
                     )))

  ; Return the quantified and control chracter delimated "\t"
  furnList
)


; Create the bill of materials table/grid
(defun tableFurnBOM (qtyList insPt / colWidths tableWidth rowHeight
                                     tableHeight headers textHeight
		                     col insText item insTextCol bottomRow)

  ; Define the sizes of the table and grid
  (setq colWidths (list 0 15 45 50)
        tableWidth 0
	row 1
	rowHeight 4
	tableHeight 0
	textHeight (- rowHeight 1))

  ; Get the table width by adding all column widths
  (foreach colWidth colWidths
    (setq tableWidth (+ colWidth tableWidth))
  )
  
  ; Define the standard table headers
  (setq headers (list "QTY" "LABELS" "PARTS"))

  ; Create the top of the table
  (entmake (list (cons 0 "LINE") (cons 10 insPt)
                 (cons 11 (polar insPt 0 tableWidth))))

  ; Get the bottom of the header row
  (setq bottomRow (polar insPt (* -1 (/ PI 2)) rowHeight))
  
  ; Add headers to the table
  (rowValuesFurnBOM headers bottomRow colWidths)

  ;; (setq tableHeight (+ tableHeight rowHeight))
  
  ; Step through each item in the list
  (foreach item qtyList
    (setq row (1+ row))
    (setq bottomRow (polar insPt (* -1 (/ PI 2)) (* row rowHeight)))
    (rowValuesFurnBOM item bottomRow colWidths)
  )

  ; Create the vertical lines for each column
  (setq colWidthTotal 0)
  (foreach colWidth colWidths
    ; Calculate the placement of each vertical line (left to right)
    (setq colWidthTotal (+ colWidth colWidthTotal))
    (setq colBasePt (polar insPt 0 colWidthTotal))

    ; Draw the vertical line
    (entmake (list (cons 0 "LINE") (cons 10 colBasePt)
                   (cons 11 (polar colBasePt (* -1 (/ PI 2))
                                   (distance insPt bottomRow)))))  
  )
)

(defun rowValuesFurnBOM (itemsList bottomRow colWidths / tableWidth)
  ; Calculate the insertion point for the header text
  (setq rowText (list (+ 0.5 (nth 0 bottomRow))
		      (+ 0.5 (nth 1 bottomRow))
		      (nth 2 bottomRow))
	tableWidth 0
  )

  ; Get the table width by adding all column widths
  (foreach colWidth colWidths
    (setq tableWidth (+ colWidth tableWidth))
  )

  ; Layout the text in each row
  (setq col 0 colWidthTotal 0)
  (foreach item itemsList
    ; Calculate the placement of each text object (left to right)
    (setq colWidthTotal (+ (nth col colWidths) colWidthTotal))
    (setq insTextCol (polar rowText 0 colWidthTotal))

    ; Draw the single-line text object
    (entmake (list (cons 0 "TEXT") (cons 100 "AcDbEntity") (cons 100 "AcDbText")
                   (cons 10 insTextCol) (cons 40 textHeight) (cons 1 item)
                   (cons 50 0.0) (cons 7 "Standard") (cons 11 insTextCol)
                   (cons 100 "AcDbText")))

    ; Create the top of the table
    (entmake (list (cons 0 "LINE") (cons 10 bottomRow)
                   (cons 11 (polar bottomRow 0 tableWidth))))

    ; Increment the counter
    (setq col (1+ col))
  )
)

; Extracts, aggregates, and counts attributes from the furniture blocks
(defun c:FurnBOM ( / ssFurn eaList) 

  ; Get the blocks to extract
  (setq ssFurn (ssget '((0 . "INSERT"))))

  ; Use the extAttsFurnBOM to extract and quanity the attributes in the blocks
  ; If ssFurn is not nil proceed
  (if ssFurn
    (progn
      ; Extract and quantify the parts in the drawing
      (setq eaList (extAttsFurnBOM ssFurn))

      ; Create the layer named BOM or set it current
      (createlayer "BOM" 8)

      ; Prompt the user for the point to create the BOM
      (setq insPt (getpoint "\nSpecify upper-left corner of BOM: "))

      ; Start the function that creates the table grid
      (tableFurnBOM eaList insPt)
    )
  )
 (princ)
)
```

3 Click File Save.

#### 6.7.6 Using the Functions in the furntools.lsp File

The functions you added to furntools.lsp leverage some of those defined in utility.lsp. These functions allow you to change the layers of objects in a drawing and extract information from the objects in a drawing as well. More specifically, they let you work with blocks that represent an office furniture layout.

Although you might be working in a civil engineering– or mechanical design–related field, these concepts can and do apply to the work you do—just in different ways. Instead of extracting information from a furniture block, you could get and set information in a title block, a callout, or even an elevation marker. Making sure a hatch is placed on the correct layers, along with dimensions, can improve the quality of output for the designs your company creates.

NOTE: The following steps require a drawing file named Ch16_Office_Layout.dwg. If you didn't download the sample files earlier, download them now from www.sybex.com/go/autocadcustomization. These sample files should be placed in the MyCustomFiles folder within the Documents (or My Documents) folder.

The following steps explain how to use the furnlayers function that is in the furntools.lsp file:

1 Open `Ch16_Office_Layout.dwg`. Figure 16.6 shows the office layout that is in the drawing.

2 Start the appload command. Load the LSP files furntools.lsp and utility.lsp. If the File Loading - Security Concerns message box is displayed, click Load.

3 At the Command prompt, type furnlayers and press Enter.

4 At the Select objects: prompt, select all the objects in the drawing and press Enter. The objects in the drawing are placed on the correct layers. Earlier the objects were placed on layer 0 and had a color of white (or black) based on the background color of the drawing area.

Figure 16.6 Office furniture layout

The following steps explain how to use the furnbom function that is in the furntools.lsp file:

1 Open the `Ch16_Office_Layout.dwg` if it is not open from the previous steps.

2 Load the furntools.lsp and utility.lsp files if you opened the drawing in step 1.

3 At the Command prompt, type furnbom and press Enter.

4 At the Select objects: prompt, select all the objects in the drawing. Don't press Enter yet. Notice that the dimension objects aren't highlighted. This is because the ssget function is only allowing block references (insert object types) to be selected as a result of the filter being applied.

5 Press Enter to end the object selection.

6 At the Specify upper-left corner of BOM: prompt, specify a point to the right of the furniture layout in the drawing. The BOM that represents the furniture blocks is placed in a table grid, as shown in Figure 16.7.

Figure 16.7 Bill of materials generated from the office furniture layout

# 0207. Creating and Modifying Nongraphical Objects

Nongraphical objects represent the block definitions, named styles, and other objects that are stored in a drawing but aren't present in model space or one of the named layouts. These objects can and typically do affect the display of graphical objects placed in model space or a named layout, though. While model space and named layouts are typically not thought of as nongraphical objects, they are. Model space is a special block definition, whereas a layout is an object that is based on a plot configuration — commonly called a page setup — with a reference to a block definition.

1-2『这里对模型空间（model space）以及布局（layout）定义很出乎意料，模型空间是一张特殊的块定义，布局是一个基于绘制设置的对象。做一张任意卡片。（2021-03-11）』

A drawing file can contain two types of nongraphical objects: symbol tables and named dictionaries. Symbol tables represent the original named objects that were available in the AutoCAD® R12 release and earlier ones. Support for named dictionaries was added with AutoCAD R13 to handle new and custom objects without the need for a new drawing file format. In this chapter, you will learn to create, manage, and use symbol table and dictionary entries.

1-2『symbol tables and named dictionaries，各做一张术语卡片。（2021-03-11）』

## 7.1 Working with Symbol Tables

Symbol tables are the oldest form of nongraphical objects used in drawing files and have been unchanged since AutoCAD R12. Although the features that use symbol tables have changed since AutoCAD R12, the additional information that those features use in later releases is attached as either XData or an extension dictionary on an entry or the symbol table.

1『原来 XData 是对 symbol tables 的替代。（2021-03-11）』

#### The Hidden Value of Nongraphical Objects

Have you opened a drawing from a client to find what seems like a spaghetti mess of layers, linetypes, and text styles that just don't work well with your standards? Maybe the Standard text style in the client's drawings uses a fixed height and different font than your company uses, which would affect the way your blocks and annotation might look like in the drawing. Using the AutoLISP® programming language, you can create or change nongraphical objects stored in symbol tables or dictionaries so they align with your company's standards. Aligning the standards in the drawings received from a client ensure that the objects you create and those in the drawings plot with a consistent appearance.

1『哇塞，这个超级有用，自动去校准修改「非图形」对象，比如字体、图层等，保证「图纸设置」一致，这章的信息对设计的「标准化」绝对有大用。（2021-03-11）』

For example, the transparency level and description of a layer is attached as XData to a layer table entry, and both layer states and filters are attached as extension dictionaries to the layer table. I covered XData in Chapter 16,「Creating and Modifying Graphical Objects」and will discuss dictionaries in the section「Working with Dictionaries」later in this chapter.

Table 17.1 lists the symbol-table names that are supported in all drawing files created with AutoCAD R12 and later.

Table 17.1 Symbol-table names

| Table name | Description |
| --- | --- |
| appid | Registered applications |
| block | Block definitions |
| dimstyle | Dimension styles |
| layer | Layers |
| ltype | Linetypes |
| style | Text styles |
| ucs | User coordinate systems |
| view | Named views |
| vport | Viewports |

### 7.1.1 Accessing and Stepping through Symbol Tables

AutoLISP provides three functions that allow you to access the entries of a symbol table or determine if a specific entry exists in a symbol table. The tblnext function returns either the first or next entry in a specified symbol table. The tblnext function is similar to the entnext function that I discussed in Chapter 16.

2『 `tblnext` 这个函数收录入主题卡片「函数收藏」。（2021-03-11）』—— 已完成

The following shows the syntax of the `tblnext` function:

```c
(tblnext sym_table [next])
```

Its arguments are as follows:

1 `sym_table`. The `sym_table` argument is a string used to specify the symbol table which you want to query, and it must be one of the values listed in the first column of Table 17.1.

2 next. The next argument is optional, and specifies whether you want to get the first entry of a symbol table or the next symbol-table entry after the previous entry that was returned. Use a value of T to return the first value. When no argument or nil is provided, an entity data list of the next symbol table entry is returned.

The following example code shows the `tblnext` function and the resulting list of layer names in a drawing:

```c
; Lists the layers in the drawing 
(defun c:listlayers ( / entityData) 
  (prompt "\nLayers in this drawing:") 
  (setq entityData (tblnext "layer" T)) 
  (while entityData 
    (prompt (strcat "\n" (cdr (assoc 2 entityData)))) 
    (setq entityData (tblnext "layer")) 
  ) 
  (princ) 
) 

Layers in this drawing: 
0 
Labels 
Panels 
Surfaces 
Storage 
Defpoints 
Dimensions 
BOM
```

To check for the existence of or get the entity data list of an entry in a symbol table, you can use the `tblsearch` function. If the name of the entry in the specified table exists, an entity data list is returned for the entry; otherwise, nil is returned. The `tblobjname` function can also be used to check for the existence of a symbol table entry, but unlike the `tblsearch` function, `tblobjname` returns the entity name (ename) of the entry if it is found; otherwise, it returns nil.

2『 `tblsearch` 和 `tblobjname` 这两个函数收录入主题卡片「函数收藏」。（2021-03-11）』—— 已完成

The following shows the syntax of the `tblsearch` and `tblobjname` functions:

```c
(tblsearch sym_table entry [next]) 
(tblobjname sym_table entry)
```

The arguments are as follows:

1 `sym_table`. The `sym_table` argument is a string that represents the symbol table you want to query, and it must be one of the values in the first column of Table 17.1.

2 entry. The entry argument is a string that represents the entry you want to check for in the symbol table specified by the `sym_table` argument.

3 next. The next argument is optional and represents whether the next call to tblnext uses the results of the `tblsearch` function to determine its starting entry. Use a value of T to not affect the next call of the `tblnext` function in the current drawing. When no argument or nil is provided, the `tblnext` function bases the entity it returns on the position of the entry provided by the entry argument.

Here are some examples of the `tblobjname` and `tblsearch` functions, and their results:

```c
; Get the entity data list for layer 0 
(tblsearch "layer" "0") 
((0. "LAYER") (2. "0") (70. 0) (62. 7) (6. "Continuous")) 
; Get the entity data list for the layer BOM 
(tblsearch "layer" "BOM") 
nil 
; Get the entity name of layer 0 
(tblobjname "layer" "0") 
<Entity name: 7ff6cde08900> 
; Get the entity name of the BOM layer 
(tblobjname "layer" "BOM") 
nil 
; Check for the existence of the BOM layer 
(if (tblobjname "layer" "BOM") 
  (alert "BOM layer already exists in the current drawing.") 
)
```

1-3『

看到上面的实例，才知道「图层」这种非图形对象，也是有 entity name，这个信息对自己非常重要，而且之前数据流实现核查是否有某个块时，用到了 `tblsearch` 这个函数。（2021-03-11）

```c
; 2021-03-03
(defun VerifyGsLcBlockByName (blockName /) 
  (if (= (tblsearch "BLOCK" blockName) nil) 
    (StealGsLcBlockByNameList (list blockName))
  )
)
```

```c
; 2021-03-03
(defun VerifyGsLcLayerByName (layerName /) 
  (if (= (tblsearch "LAYER" layerName) nil) 
    (StealGsLcLayerByNameList (list layerName))
  )
)
```

补充：通过上面的代码获取到实现判断图纸里是否有某个图层的另外一个实现途径（2021-03-30）：

```c
; Check for the existence of the BOM layer 
(if (tblobjname "layer" "BOM") 
  (alert "BOM layer already exists in the current drawing.") 
)
```

』

### 7.1.2 Adding and Modifying Entries in a Symbol Table

Most symbol table entries are inherited from the drawing template that was used to create a drawing file or are created as a result of inserting a block into a drawing. A drawing template should contain most of the layers, linetypes, and other nongraphical objects you might want to use in your drawing, but you can use AutoLISP to create and modify any additional system table entries you might need. The methods you use to create and modify nongraphical objects are the same as those for graphical objects (which I explained in Chapter 16).

The symbol table entries you create or modify should follow your company's established CAD standards or those of the industry in which you work. Modifying existing table entries should be done with care, because the changes you make could have an adverse effect on existing objects in a drawing. For example, changing the height of a text style could affect dimensions and tables in your drawing.

#### An Ounce of Prevention

It is 3:00 p.m., and your boss just let you know that a set of drawings needs to be sent out by 6:00 p.m. for an initial bid. You output all of the drawings, only to discover that objects in some of the drawings weren't placed on the correct layers and text styles don't use the correct fonts. Everyone decided to take a half day today because they have been working frantically for the past two weeks on this project. Getting the project across the finish line now rests on your shoulders. The drawings need to be sent out for the initial bid, but their current state is less than ideal for a first impression to the new client.

What to do?

Take a deep breath and channel your inner AutoLISP to create a program that can be executed in each drawing to change the text styles to use the correct fonts — one problem down. Now, on to the layer issues.

Using AutoLISP, you can verify whether the correct layer exists and, if not, create the new layer. With selection filters that you learned about in Chapter 16, you can select and move objects to their appropriate layers based on object type or current property values.

Now that the drawings have been fixed, you output the revised drawings with minutes to spare. This battle is won, but the war for CAD excellence is not over yet. Custom programs created with AutoLISP can help you to enforce CAD standards in your office. Using the programs you create, a drafter can focus more on the elements of a design and less on switching to the correct layer and style before adding new objects.

1『

看到上面的信息，想到更新一个 Symbol Table 对象的方法：获取到它的 entity data 后，用 `subst` 替换数据集，然后用函数 `entmod` 更新数据对象。下面代码供参考。（2021-03-11）

```c
(entmod (subst newValue oldValue entityData))

; Update the object’s entity data list 
(entmod entityData)
; Refresh the object on-screen
(entupd entityName)
```

这里无意中知道了 `(entupd entityName)` 的作用，类似于 `re` 命令，刷新数据对象。做一张任意卡片。（2021-03-30）

』

#### Adding an Entry

You can add a new style table entry using the appropriate AutoCAD command with the command function. For example, you can use the `-layer` command to create a new layer, `-block` to create a new block, or `-linetype` to create or load a linetype pattern.

As you learned in Chapter 16, you can use the command function with AutoCAD commands, but I recommend using the `entmake` or `entmakex` function to create new objects instead. Creating new objects with entity data lists gives you more control over the object that you create, but it requires you to learn the DXF group codes and values that each object expects. For information on the `entmake` and `entmakex` functions, see the「Adding Objects to a Drawing」section in Chapter 16.

TIP: You can use the `tblobjname` and entget functions to return the entity data list of an existing symbol table entry that you want to reproduce using AutoLISP. For example, `(entget (tblobjname "ltype" "center"))` returns the entity data list for the Center linetype if it is loaded in the current drawing.

1『这里提供了一个筛选特定图层的新路径，用 `tblobjname` 函数。之前已经实现的路径是判断一个数据对象的 DXF 号（数值 8）的值是否为某个图层字符。比较来看，`tblobjname` 函数更加抽象（高层）。（2021-03-11）补充：这个时间点才意识到，`ltype` 是只中心线那种线型。（2021-04-02）』

This next code example attempts to create a new layer named Centerlines with the linetype Center:

```c
(entmake (list (cons 0 "LAYER") (cons 100 "AcDbSymbolTableRecord") 
            (cons 100 "AcDbLayerTableRecord") (cons 2 "Centerlines") 
            (cons 70 0) (cons 62 3) (cons 6 "Center"))
) 
Error: Undefined line type Center in LayerTableRecord Centernil
```

An error message and nil is returned if the Center linetype doesn't exist in the drawing prior to creating the layer. Before you create symbol table entries, you must make sure that all of the objects they depend on are present in the drawing. For example, a linetype must exist in a drawing before a layer that uses the linetype can be created. The same is true of dimension styles; the text style and linetypes that a dimension style might reference must exist in the drawing before you create the dimension style.

1-3『目前使用的是 LeeMac 封装好的函数「202102StealV1-8.lsp」。实现从已有的图纸里「偷」各种「Symbol Table」。（2021-03-11）补充：这里反复提及一个思想，在用一个 `symbol table` 实体对象之前，必须要确认图纸里是不是已经有了这个实体对象。（2021-04-02）』

This example checks for the Center linetype and, if it doesn't exist, the linetype is created using the entmake function:

```c
(if (= (tblsearch "ltype" "center") nil) 
  (entmake (list (cons 0 "LTYPE")(cons 100 "AcDbSymbolTableRecord") 
    (cons 100 "AcDbLinetypeTableRecord") (cons 2 "CENTER") (cons 70 0) 
    (cons 3 "Center ____ _ ____ _ ____ _ ____ _ ____ _ ____") (cons 72 65) 
    (cons 73 4) (cons 40 2.0) (cons 49 1.25) (cons 74 0) (cons 49 -0.25) 
    (cons 74 0) (cons 49 0.25) (cons 74 0) (cons 49 -0.25) (cons 74 0)) ) 
) 

((0. "LTYPE") (100. "AcDbSymbolTableRecord") (100. "AcDbLinetypeTableRecord") 
(2. "CENTER") (70. 0) (3. "Center ____ _ ____ _ ____ _ ____ _ ____ _ ____") 
(72. 65) (73. 4) (40. 2.0) (49. 1.25) (74. 0) (49. -0.25) (74. 0) (49. 0.25) (74. 0) (49. -0.25) (74. 0))
```

Using the previous example, you can ensure that the Center linetype exists in the drawing before you try to create the Centerlines layer. Now if you try to create the Centerlines layer with the following example, the new layer is created since the Center linetype is defined in the drawing.

```c
(entmake (list (cons 0 "LAYER") (cons 100 "AcDbSymbolTableRecord") 
          (cons 100 "AcDbLayerTableRecord") (cons 2 "Centerlines") 
          (cons 70 0) (cons 62 3) (cons 6 "Center"))
) 
((0. "LAYER") (100. "AcDbSymbolTableRecord") (100. "AcDbLayerTableRecord") (2. "Centerlines") (70. 0) (62. 3) (6. "Center"))
```

Before creating a new symbol table entry with `entmake` or `entmakex`, you should verify that it doesn't already exist. If the symbol table entry already exists, entmake or entmakex will return nil. I also recommend checking the name of the symbol table entry you are trying to add with the `snvalid` function. The `snvalid` function verifies that the name doesn't contain any invalid characters and follows the naming rules based on the current value of the extnames system variable. For more information on the extnames system variable, see the AutoCAD Help system.

2『 `snvalid ` 这个函数收录入主题卡片「函数收藏」。（2021-03-11）』—— 已完成

The following shows the syntax of the snvalid function:

```c
(snvalid name [flag])
```

Here are its arguments:

1 name. The name argument is a string that represents the name of the symbol table entry you want to verify.

2 flag. The flag argument is an optional integer that determines whether the symbol table entry name can contain a vertical bar. 0 indicates that a vertical bar is not allowed, whereas 1 indicates that the vertical bar is a valid character as long as it isn't the first character in the entry name.

Here are some examples of using the snvalid function and the values that are returned:

```c
(snvalid "Centerlines") 
T 
(snvalid "Centerlines?") 
nil 
(snvalid "Detail|Centerlines" 0) 
nil 
(snvalid " Detail|Centerlines " 1) 
T
```

#### Modifying and Renaming an Entry

Symbol table entries can be modified and renamed using the same techniques that you learned in Chapter 16 for modifying graphical objects. You can use the AutoLISP functions listed in Table 17.2 to modify symbol table entries.

Table 17.2 Functions that can be used to modify symbol table entries

| Function name | Description |
| --- | --- |
| entget | Returns the entity data list for an object |
| entmod | Commits an entity data list to an object |
| dumpallproperties | Outputs the property names and their current values for an object |
| getpropertyvalue | Returns an object's property value |
| ispropertyreadonly | Determines whether an object's property is read-only |
| setpropertyvalue | Sets an object's property value |

When modifying symbol table entries, you should understand that not all entries can be renamed or modified. For example, you can modify layer 0 but you can't rename the layer. The layers that you create, with the exception of those in an attached external reference, can be modified and renamed. Table 17.3 lists the symbol table entries that you can't rename and/or modify.

Table 17.3 Symbol table entry name and modification limits

| Table name | Entry name | Description |
| --- | --- | --- |
| appid | Nothing specific | Entries can't be renamed, but they can be removed. |
| block | `*model_space` and `*paper_space` | Model space and paper space block definitions can't be renamed or removed. Drawings can have more than one paper space block; these additional blocks have a numeric suffix starting at 1. |
| dimstyle | standard | Can be modified but not renamed or removed. |
| layer | 0 | Can be modified but not renamed or removed. |
| ltype | continuous | Can't be modified, renamed, or removed. |
| style | standard | Can be modified but not renamed or removed. |
| ucs | `*active` | Can be modified but not renamed or removed. |
| vport | `*active` | Can be modified but not renamed or removed. |

Here's an example that shows how to rename a layer and its current color by using its entity data list. The name of a symbol table entry is designated with the dotted pair that has the DXF group code 2 key element.

```c
; Get the layer named "BOM" 
(setq entityName (tblobjname "layer" "BOM")) 
; Get the entity data for the layer 
(setq entityData (entget entityName)) 
; Rename the layer from "BOM" to "Bill of Materials" 
(setq entityData (subst (cons 2 "Bill of Materials") (assoc 2 entityData) entityData)) 
; Change the layers color to 5 
(setq entityData (subst (cons 62 5) (assoc 62 entityData) entityData)) 
; Update the layer 
(entmod entityData)
```

The following example renames the layer「Bill of Materials」back to「BOM」and changes the layer color to 8 with the `setpropertyvalue` function:

```c
; Get the layer named "Bill of Materials" 
(setq entityName (tblobjname "layer" "Bill of Materials")) 
; Rename the layer from "Bill of Materials" to "BOM" 
(setpropertyvalue entityName "name" "BOM") 
; Change the layer's color to 8 
(setpropertyvalue entityName "color" 8)
```

1『其实以后可以渐渐的改用 `setpropertyvalue` 去设置属性值，它更抽象高级。（2021-04-02）』

#### Using an Object

After a symbol table entry is created, you can use that entry in a number of ways based on the type of object it represents. The most common is to set it as current using a system variable before creating a new object so that the new object inherits the properties of the symbol table entry when possible. For example, you can use the clayer system variable to set the active layer in the drawing, or use celtype to indicate the linetype that new objects should inherit. You should refer to the setvar command and the AutoCAD Help system to identify the system variables your AutoCAD release supports and the properties they might affect.

In addition to system variables, you can change the name of a symbol table entry assigned to an object using entity data lists with the `entmod` function or directly with the `getpropertyvalue` and `setpropertyvalue` functions. If you created a new named view, you can use the `setview` function to set the view current in a viewport. For more information on the `setview` function, see the AutoCAD Help system.

#### Removing an Entry That Is No Longer Needed

Since the same techniques can be used to create and modify both graphical and symbol table entries, you might think that removing a symbol table entry and a graphical object would also be the same in AutoLISP. The `entdel` function is used to remove graphical objects, but it cannot be used to remove symbol table entries. This is one of the very few times that you can't use「classic」AutoLISP to do something. Instead of using a specific AutoLISP function, you must use the command function with the `-purge` command to remove a symbol-table object.

You can use the `tblobjname` and `tblsearch` functions to determine whether a specific symbol table entry exists in a drawing, and then use the `-purge` command to remove it. If the symbol table entry doesn't exist or cannot be removed because it is being used, the `-purge` command will end gracefully without any significant error messages that require user interaction to dismiss. Here's an example of how to remove a block named roomlabel from a drawing with the `-purge` command:

```c
(command "._-purge" "_b" "roomlabel" "_n")
```

NOTE: On Windows only, you can use the AutoLISP `vla-delete` function after loading the AutoCAD ActiveX/COM interface with the `vl-load-com` function. I discuss the basics of using ActiveX with AutoLISP in Chapter 22,「Working with ActiveX/COM Libraries (Windows only).」

1-2-3『

如何删除 `symbol table` 实体对象做一张主题卡片。

[PurgeAll Method (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-9FD38B4D-2554-419A-9A1F-916725A300F5)

通过这里的 purge 搜到了官方文档里的函数 `purgeAll`。这是目前自己急需的一个功能，设计流开发中，很多 `symbol table` 实体对象是通过无差别「偷」来的，但偷懒的很多图形模块很多没用上，是冗余的，那么就可以用这个功能函数自动清理掉。那么正好封装成公共函数。

```c
; 2021-04-02
(defun PurgeAllUtils (/ acadObj doc)
  ;; This example removes all unused named references from the database
  (setq acadObj (vlax-get-acad-object))
  (setq doc (vla-get-ActiveDocument acadObj))
  (vla-PurgeAll doc) 
)
```

』

### 7.1.3 Creating and Modifying Block Definitions

Although some symbol table entries can seem complex at first, blocks are probably at the top of the list when it comes to complexity. When you initially create a block entry, the block entry contains no graphical objects. You add graphical objects to a block entry similar to how you add objects to a drawing with the `entmake` or `entmakex` function.

A block definition has a beginning (header) of the block object type and an ending sequence of the endblk object type. The beginning sequence tells AutoCAD that a block definition is being created along with the following information (at minimum):

1 Block name (DXF group code 2).

2 Block-type flags as a bitcode (DXF group code 70).

3 Base point (DXF group code 10).

The block-type flag is typically set to a value of 0 (which indicates that the block doesn't contain attribute definitions or that all of the attribute definitions are constant) or to a value of 2 (which indicates that the block contains nonconstant attributes). Once the block definition is started, use the `entmake` or `entmakex` function to add objects to the block definition. You can't add an attribute reference (attrib) object to a block definition. Instead, add attribute definition (attdef) objects to a block definition. These are used to define the attribute references that should be added to a block reference when it is inserted into model space or paper space with the insert command.

Here's a basic representation of the entity data lists that you need to create to define a block without any attributes or graphical objects. Passing the entity data lists to the `entmake` function will create an empty block.

```c
; Start block definition 
((0. "BLOCK") (2. "some_block_name") (10 0.0 0.0 0.0) (70. 0)) 
; Objects here with entmake 
; End block definition 
((0. "ENDBLK"))
```

1-3『

数据流里生成「块参照」的代码示例。

```c
(defun GenerateBlockReference (insPt blockName blockLayer /) 
  (entmake 
    (list (cons 0 "INSERT") (cons 100 "AcDbEntity") (cons 67 0) (cons 410 "Model") (cons 8 blockLayer) (cons 100 "AcDbBlockReference") 
          (cons 66 1) (cons 2 blockName) (cons 10 insPt) (cons 41 1.0) (cons 42 1.0) (cons 43 1.0) (cons 50 0.0) (cons 70 0) (cons 71 0) 
          (cons 44 0.0) (cons 45 0.0) (cons 210 '(0.0 0.0 1.0))
    )
  ) 
  (princ)
)

; directionStatus: dxfcode 50; 0.0 Level - 1.57 Vertical
; hiddenStatus dxfcode 70; 0 可见 - 1 隐藏
; moveStatus: dxfcode 280; 1 固定 - 0 可移动
(defun GenerateCenterBlockAttribute (insPt propertyName propertyValue blockLayer textHeight directionStatus hiddenStatus moveStatus /)
  (entmake 
    (list (cons 0 "ATTRIB") (cons 100 "AcDbEntity") (cons 67 0) (cons 410 "Model") (cons 8 blockLayer) (cons 100 "AcDbText") 
          (cons 10 (MoveInsertPositionUtils insPt -5.8 0)) (cons 40 textHeight) (cons 1 propertyValue) (cons 50 directionStatus) 
          (cons 41 0.7) (cons 51 0.0) (cons 7 "DataFlow") (cons 71 0) (cons 72 1) (cons 11 insPt) (cons 210 '(0.0 0.0 1.0)) 
          (cons 100 "AcDbAttribute") (cons 280 0) (cons 2 propertyName) (cons 70 hiddenStatus) (cons 73 0) (cons 74 0) (cons 280 moveStatus)
    )
  )
  (princ)
)

; 2021-02-07
(defun GenerateOneFireFightElevation (insPt elevation textHeight /) 
  (GenerateBlockReference insPt "FireFightElevation" "DataflowFireFightElevation")
  (GenerateBlockAttribute (AddPositonOffSetUtils insPt '(-950 300 0)) "ELEVATION" elevation "0" textHeight)
  (entmake 
    (list (cons 0 "SEQEND") (cons 100 "AcDbEntity"))
  )
  (princ)
)
```

补充：前面一段文字里的信息比较密的。1）DXF 70，0 表示没有属性或属性值是常量。2 表示非常量的属性值。动态块感觉是用 2 做的，有待确认。2）属性参照是 attrib，属性定义是 attdef。联想到以前测试过的场景，后台自动生成块定义的时候就是要用 attdef，而目前图纸里生成一个块本质是属性只是引用的，所以用的是 attrib。（2021-04-02）

』

If you want to revise the content of a block definition (also known as redefining a block), there are a couple of different processes. Choose the process you need based on how the block definition should be revised:

1 Updating or Removing Objects. Step through the objects of a block definition when you need to change the properties of or remove an existing object in a block definition. Get the entity name of the block definition with the `tblobjname` function and step through the block definition with the entnext function. Change the objects in the block definition as you would those in a model space or paper space. Use the `entdel` function to remove objects from a block definition.

1『才意识到，也可以用 `tblobjname` 函数直接获取到 entity name，之前一直使用选择集过滤到想要的块，然后通过选择集来获取 entity name，现在又多个一种途径。（2021-03-11）』

2 Adding Objects. You must re-create the block definition by going through the process used to create the block. That is, to start the block definition, add the objects and then add the end block-definition marker. If you don't want to re-create all of the objects as part of the block definition, you can create a block reference in the drawing and explode it. Once it's exploded, you can add the new objects you want to add to the block in model space and then use the `-block` command to redefine the block definition.

1-2『看到上面的信息，刚刚生成的实体对象，获取其 entity name 得到选择集，再结合「`command` + `-block`」应该可以自动定义一个块。待测试实现。（2021-03-11）补充：完全可以实现，把建筑底部迁移到工艺布置图后，后台自动把建筑底部做成一个块。（2021-04-02）』—— 未完成

NOTE: On Windows only, you can use AutoLISP `vla-add<object>` functions to add objects directly to an existing block definition. I discuss the basics of using ActiveX with AutoLISP in Chapter 22.

1-2-3『

感觉通过上面的信息，可以获取到自动生成「块参照」的第三种实现路径。待研究。（2021-03-11）

补充：那是后的直觉果然是真的，上面实现自动生成块的方法是采用了 ActiveX。已经实现了。

```c
; 2021-03-08
(defun InsertBlockUtils (insPt blockName layerName propertyDictList / acadObj curDoc insertionPnt modelSpace blockRefObj blockAttributes)
  (setq acadObj (vlax-get-acad-object))
  (setq curDoc (vla-get-activedocument acadObj)) 
  (setq insertionPnt (vlax-3d-point insPt))
  (setq modelSpace (vla-get-ModelSpace curDoc))
  (setq blockRefObj (vla-InsertBlock modelSpace insertionPnt blockName 1 1 1 0))
  ;(vlax-dump-object blockRefObj T)
  (vlax-put-property blockRefObj 'Layer layerName)
  (setq blockAttributes (vlax-variant-value (vla-GetAttributes blockRefObj)))
  ; another method get the blockAttributes
  ;(setq blockAttributes (vlax-variant-value (vlax-invoke-method blockRefObj 'GetAttributes)))
  ;(vlax-safearray->list blockAttributes)
  ; setting block property value
  (mapcar '(lambda (x) 
            (vla-put-TextString (vlax-safearray-get-element blockAttributes (car x)) (cdr x))
          ) 
    propertyDictList
  ) 
  ;(vla-ZoomAll acadObj) 
  (princ)
)
```

总结一下目前已经掌握的自动生成块的方法：1）直接嫁接 CAD 原生命令，不推荐，数据多了会很慢。2）新建 entityData，在图纸里生成。3）ActiveX 方法。（2021-04-02）

』—— 已完成

In the following exercise, you'll create a new block definition and layer. The new block definition is named circ and it contains a single circle object with a base point of 0,0. The new layer is named hardware and has a color value of 3 (green).

1 Create a new drawing.

2 At the AutoCAD Command prompt, type the following and then press Enter to start the block definition for the circ block:

```c
(entmake (list (cons 0 "block")(cons 2 "circ") 
          (cons 10 (list 0.0 0.0 0.0))(cons 70 0))
)
```

3 Type the following and press Enter to add the circle at 0,0 with a radius of 2. The circle is placed on layer 0 so that it inherits the properties of the layer on which the block is placed.

```c
(entmake (list (cons 0 "circle")(cons 10 (list 0.0 0.0 0.0)) 
          (cons 40 2)(cons 8 "0"))
)
```

4 Type the following and press Enter to end the circ block definition:

```c
(entmake (list (cons 0 "endblk")))
```

5 Type the following and press Enter to create the layer named hardware with a color of 3 and a linetype of Continuous:

```c
(entmake (list (cons 0 "layer") (cons 100 "AcDbSymbolTableRecord") 
            (cons 100 "AcDbLayerTableRecord") (cons 2 "hardware") 
            (cons 70 0) (cons 62 3) (cons 6 "Continuous"))
)
```

6 Type the following and press Enter to set the hardware layer as current:

```c
(setvar "clayer" "hardware")
```

7 Type `insert` and press Enter to display the Insert (Windows) or Insert Block (Mac OS) dialog box.

8 When the Insert dialog box opens, click the Name drop-down list and select circ.

9 Deselect all the check boxes under the Insert Point, Scale, and Rotation sections. Click OK (Windows) or Insert (Mac OS) to insert the block into the drawing.

10 Zoom to the extents of the drawing.

11 Select the new object in the drawing. Right-click and choose Properties.

12 In the Properties palette (Windows) or Properties Inspector (Mac OS), you should notice that the object is a block named circ and that it has been placed on the hardware layer.

### 7.2 Working with Dictionaries

Dictionaries are used to store custom information and objects in a drawing and can be thought of as symbol tables 2.0. Dictionaries were introduced with AutoCAD R13 as a way to introduce new symbol tables like objects without the need to change the drawing file format with each release. Although there is only one type of dictionary in a drawing, dictionaries can be stored in two different ways: per drawing or per object.

The main dictionary of a drawing contains nested dictionaries that store multileader and table styles, and even the layouts used to output a drawing. Dictionaries attached to an object are known as extension dictionaries. Extension dictionaries are similar to XData but allow you to attach more information to a single object. AutoCAD uses extension dictionaries attached to the layer symbol table to store the information used for layer states and filters.

Custom dictionaries are great for storing custom program settings so that they persist across drawing sessions. You might also use a custom dictionary as a way to store drawing revision history or project information that can be used to track a drawing and populate a title block. In this section, you'll learn how to access, create, query, and modify information stored in a dictionary.

1『字典 dictionaries 做一张术语卡片。（2021-03-26）』—— 已完成

### 7.2.1 Accessing and Stepping through Dictionaries

The dictionary-related AutoLISP functions are similar to those used when working with symbol tables. Before you can access the entries in a dictionary, you must first get a dictionary. The `namedobjdict` function returns the entity name of the drawing's named-object dictionary. This is the main dictionary that contains all the dictionaries that aren't attached to an object as an extension dictionary. The `namedobjdict` function doesn't require any arguments.

Once you have the entity name of the named object dictionary, use the entget function to get an entity data list that contains the key entries and entity names for each dictionary. Each entry in the named object dictionary is represented by two dotted pairs. The first dotted pair represents the unique name of a dictionary and DXF group code 3. The second dotted pair contains the entity name for the dictionary and DXF group code 350.

Here's an example of an entity data list for a named object dictionary:

```c
((-1. <Entity name: 7ff6646038c0>) (0. "DICTIONARY") (330. <Entity name: 0>) 
(5. "C") (100. "AcDbDictionary") (280. 0) (281. 1) 
(3. "ACAD_COLOR") (350. <Entity name: 7ff664603c30>) 
(3. "ACAD_GROUP") (350. <Entity name: 7ff6646038d0>) 
(3. "ACAD_VISUALSTYLE") (350. <Entity name: 7ff6646039a0>) 
(3. "ACAD_MATERIAL") (350. <Entity name: 7ff664603c20>))
```

The third dictionary entry in the example entity data list is `(3. "ACAD_VISUALSTYLE") (350. <Entity name: 7ff6646039a0>)`, and this entry allows you to access the visual styles of the current drawing. The code in Listing 17.1 returns the entity name for a `ACAD_VISUALSTYLE` dictionary.

Listing 17.1: Custom function that returns the Visual Styles dictionary

```c
; Custom function that returns the entity name of a specific dictionary entry 
(defun GetDictionaryByKeyEntry (dictionaryEntity dKeyEntry / entityData dKeyEntry dEntityName cnt) 
  (setq entityData (entget dictionaryEntity)) 
  (setq dEntityName nil) 
  (setq cnt 0) 
  (while (and (= dEntityName nil)(< cnt (length entityData))) 
    (if (and (= (car (nth cnt entityData)) 3) 
             (= (cdr (nth cnt entityData)) dKeyEntry)) 
      (progn 
        (setq dEntityName (cdr (nth (1+ cnt) entityData))) 
      ) 
    ) 
    (setq cnt (1+ cnt)) 
  ) 
  dEntityName 
) 
; Example of using the custom function 
(GetDictionaryByKeyEntry (namedobjdict) "ACAD_VISUALSTYLE")
```

After you have the entity name for the dictionary you want to work with, you can use the `dictnext` function to return either the first or next item attached to the dictionary. The dictnext function is similar to the `tblnext` function, which I discussed earlier in this chapter. The following shows the syntax of the dictnext function:

```c
(dictnext ename [next])
```

Its arguments are as follows:

1 ename. The ename argument is an entity name that represents the dictionary you want to step through.

2 next. The next argument is optional, and it specifies whether you want to get the first entry of a dictionary or the entry after the one that was returned by the last use of the dictnext function. Use a value of T to return the entity name of the first entry in the dictionary. When no argument or nil is provided, the entity name of the next entry is returned.

The following example code uses the AutoLISP dictnext function and the GetDictionaryByKeyEntry function in Listing 17.1 to step through and list the names of each visual style in the drawing. The code is followed by an output listing from one of my drawings.

```c
; Lists the visual styles in the drawing 
(defun c:listvisualstyles ( / entityData dictionaryName) 
  (setq dictionaryName (GetDictionaryByKeyEntry (namedobjdict) "ACAD_VISUALSTYLE")) 
  (prompt "\nVisual styles in this drawing:") 
  (setq entityData (dictnext dictionaryName T)) 
  (while entityData 
    (prompt (strcat "\n" (cdr (assoc 2 entityData)))) 
    (setq entityData (dictnext dictionaryName)) 
  ) 
  (princ) 
) 

Visual styles in this drawing: 
2dWireframe
Basic 
Brighten 
ColorChange 
Conceptual 
Dim 
EdgeColorOff 
Facepattern 
Flat 
FlatWithEdges 
Gouraud 
GouraudWithEdges 
Hidden 
JitterOff 
Linepattern 
OverhangOff 
Realistic 
Shaded 
Shaded with edges 
Shades of Gray 
Sketchy 
Thicken 
Wireframe 
X-Ray
```

If you know (or want to check for the existence of) a key entry in a dictionary, you can use the `dictsearch` function. If the name of the key entry in the dictionary exists, the entity data list of the key entry is returned; otherwise, nil is returned. Here's an example of using the dictsearch function to get the entity data list associated with the `ACAD_TABLESTYLE` dictionary:

```c
(setq entityData (dictsearch (namedobjdict) "ACAD_TABLESTYLE")) 

((-1. <Entity name: 7ff664603ce0>) (0. "DICTIONARY") (5. "86") 
(102. "{ACAD_REACTORS") (330. <Entity name: 7ff6646038c0>) 
(102. "}") (330. <Entity name: 7ff6646038c0>) 
(100. "AcDbDictionary") (280. 0) (281. 1) (3. "Standard") 
(350. <Entity name: 7ff664603cf0>))
```

Once you have the entity data list for the dictionary, you can use the assoc function to get the dictionary's entity name, which is associated with the DXF group code –1. After you get the entity name for the dictionary, you can then pass it to the dictsearch function to locate a specific key entry in the dictionary. The following shows how to get the Standard table style entry from the entity data list of the `ACAD_TABLESTYLE` dictionary:

```c
(setq entityNameTS (cdr (assoc -1 entityData))) 
(setq entityDataTS (dictsearch entityNameTS "STANDARD")) 

((-1. <Entity name: 7ff664603cf0>) (0. "TABLESTYLE") (5. "87") 
(102. "{ACAD_XDICTIONARY") (360. <Entity name: 7ff664605340>) 
(102. "}") (102. "{ACAD_REACTORS") (330. <Entity name: 7ff664603ce0>) 
(102. "}") (330. <Entity name: 7ff664603ce0>) (100. "AcDbTableStyle") 
(280. 0) (3. "Standard") 
… 
(68. 0) (279. -2) (289. 1) (69. 0))
```

Here's the syntax of the dictsearch function:

```c
(dictsearch ename entry)
```

Its arguments are as follows:

1 ename. The ename argument is an entity name that represents the dictionary you want to query to check for the existence of the key entry specified by the entry argument.

2 entry. The entry argument is a string that represents the entry you want to check for in the dictionary specified by the ename argument.

NOTE: You can use the `layoutlist` function to get a list of the named layouts in the current drawing. For more information on this function, see the AutoCAD Help system.

### 7.2.2 Creating a Custom Dictionary

As I mentioned earlier, one of the benefits of dictionaries is that you can store custom information or settings related to the programs you create in a drawing. Before a custom dictionary can be used and entries added to it, it must first be created. The `entmakex` function, not entmake, is used to create a dictionary. Once created, the new dictionary can be attached to either the named object dictionary or an object as an extension dictionary. You attach the new dictionary to the drawing's named object dictionary with the dictadd function.

The following shows the syntax of the dictadd function:

```c
(dictadd ename key_entry dictionary)
```

Its arguments are as follows:

1 ename. The ename argument is an entity name that represents the object (named or object's extension dictionary). The dictionary that is specified by the dictionary argument is attached to the object.

2 `key_entry`. The `key_entry` argument is a string that represents the unique key entry name that you want to associate with the dictionary that is specified by the dictionary argument.

3 dictionary. The dictionary argument is an entity name that represents the dictionary that you want to attach to the entity name specified by the ename argument.

Here's an example that creates a dictionary named `MY_CUSTOM_DICTIONARY` and adds it to the named object dictionary:

```c
; Create dictionary object 
(setq entityName (entmakex (list (cons 0 "DICTIONARY") (cons 100 "AcDbDictionary")))) 
; Add the dictionary to the named object dictionary 
(setq newdictionary (dictadd (namedobjdict) "MY_CUSTOM_DICTIONARY" entityName))
```

1『可以把字典作为一个图纸的数据库。待实现。（2021-03-12）』

In addition to adding a dictionary to the named object dictionary that is returned by the `namedobjdict` function, you can create an extension dictionary on a graphical object. The extension dictionary is similar to the named object dictionary of a drawing, and it can hold nested dictionaries of extended records. I discuss extended records (Xrecords) in the next section.

This example adds an extension dictionary to the last object in a drawing:

```c
; Creates a new dictionary 
(setq dictionary (entmakex (list (cons 0 "DICTIONARY")(cons 100 "AcDbDictionary")))) 
; Entity Data list of the extension dictionary 
(setq exDictionary (list (cons 102 "{ACAD_XDICTIONARY") (cons 360 dictionary)(cons 102 "}"))) 
; Attach the extension dictionary to the last object 
(setq entityData (append (entget (entlast)) exDictionary)) 
(entmod entityData)
```

Once the extension dictionary is attached to the object, you can use the DXF group code 360 to get the entity name of the extension dictionary. With the entity name, you can then add dictionaries or Xrecords to the object's extension dictionary. This example gets the entity name of the extension dictionary attached to the last object in the drawing:

```c
(cdr (assoc 360 (entget (entlast))))
```

nil is returned if no extension dictionary has been added to the object.

### 7.2.3 Storing Information in a Custom Dictionary

After a custom dictionary has been created, you add entries to a custom dictionary using the `dictadd` function. Entries of a custom dictionary are often of the extended record (also known as an Xrecord) object type. An Xrecord is similar to XData and can be attached to an object, but it contains DXF group codes that are in the same range as graphical objects. You create an Xrecord with the `entmakex` function before attaching it to the dictionary.


The following code creates an Xrecord and attaches it to `MY_CUSTOM_DICTIONARY`, which can be created using the example from the previous section, with the XR1 key entry. The Xrecord contains a string (DXF group code 1), a coordinate value (DXF group code 10), and an integer (DXF group code 71).

```c
; Add the Xrecord to the dictionary 
(dictadd newdictionary "XR1" 
  (entmakex (list (cons 0 "XRECORD")(cons 100 "AcDbXrecord") 
                  (cons 1 "Custom string")(cons 10 (list 5.0 5.0 0.0)) (cons 71 11))
  )
)
```

If you need to make a change to the data contained in an Xrecord that has been attached to a dictionary, use the `dictsearch` function to get the entry's entity data list. The dotted pairs in the entity data list can be replaced with the assoc function as needed, just like updating a graphical object or symbol table entry. Entries can also be renamed from a custom dictionary; you'll learn how to rename and remove entries in the next section.

### 7.2.4 Managing Custom Dictionaries and Entries

After a dictionary or Xrecord object has been created and attached, you can change its key entry or remove it as needed. Although you can freely rename and remove the dictionaries and Xrecords you create, those created by AutoCAD can also be renamed and removed. I recommend being cautious about renaming or removing those created by AutoCAD, because doing so could cause problems. Not all dictionaries and objects attached to a dictionary can be removed since they may be referenced by other objects. When a dictionary is successfully renamed, the new name of the dictionary is returned (or nil is returned when the dictionary couldn't be renamed). Similarly, the ename of a dictionary is returned when a dictionary is removed or nil is returned if it couldn't be removed.

You can use the dictrename function to change the current key entry to a new key entry value. The dictremove function can be used to remove a dictionary or an entry in a dictionary. The following shows the syntax of the dictrename function:

```c
(dictrename ename old_key_entry new_key_entry)
```

Its arguments are as follows:

1 ename. The ename argument is an entity name that represents the dictionary or entry whose current key entry name (`old_key_entry` argument) you want to change to the new key entry name (`new_key_entry` argument).

2 `old_key_entry`. The `old_key_entry` argument is a string that represents the current unique key entry name associated with the dictionary or entry that is specified by the ename argument.

3 `new_key_entry`. The `new_key_entry` argument is a string that represents the new unique key entry name that should replace the key entry specified by the `old_key_entry` argument.

The following shows the syntax of the dictremove function:

```c
(dictremove ename key_entry)
```

Its arguments are as follows:

1 ename. The ename argument is an entity name that represents the dictionary that has the dictionary or entry you want to remove.

2 `key_entry`. The `key_entry` argument is a string that represents the unique key entry name of the dictionary or entry you want to remove from the object specified by the ename argument.

Here are examples that rename and remove a custom dictionary:

```c
; Renames the key entry of a dictionary 
(dictrename (namedobjdict) "MY_CUSTOM_DICTIONARY" "MY_DICTIONARY") 
; Removes the custom dictionary with the key entry "MY_DICTIONARY" 
(dictremove (namedobjdict) "MY_DICTIONARY")
```

## 7.3 Exercise: Creating and Incrementing Room Labels

In this section, you will create several new functions that will be used to define and insert room-label blocks into a drawing. Room labels are used to identify areas in architectural drawings, but the same concept can be applied to callouts in mechanical drawings.

As you insert a room label block with the custom program, a counter increments by 1 so you can place the next room label without having to manually enter a new value. Before the room-labeling program ends, the last calculated value is stored in a custom dictionary so it can be retrieved the next time the program is started (instead of using global variables). The key concepts covered in this exercise are as follows:

1 Creating and Modifying Symbol Table Entries. Symbol table entries in a drawing can affect the display of graphical objects in a drawing. Each drawing that you create contains a set number of symbol tables you can access using AutoLISP. You can then create or manipulate any of the entries that are in one of the symbol tables.

2 Using Symbol Table Entries. As new objects are created, you can assign the names of symbol table entries to various properties of an object so that it inherits the symbol table entries' properties. You can change the value associated with the DXF group code 8 of an object to move the object between layers, or even change the value associated to the DXF group code 2 of a block reference to change which block definition it inherits its geometry from.

1『这里提供了一个知识点：其实可以通过修改 DXF 为 2 的点值对（块名），来更新图形。块名可以理解为继承某个块定义的名片。（2021-04-03）』

3 Creating and Storing Information in a Custom Dictionary. Values assigned to variables in a drawing are temporary, but you can use custom dictionaries to persist values across drawing sessions. The values stored in a drawing can then be recovered by your programs after the drawing is closed and reopened, similar to how system variables work.

NOTE: The steps in this exercise depend on the completion of the steps in the「Exercise: Creating, Querying, and Modifying Objects」section of Chapter 16. If you didn't complete these exercises, do so now or start with the `ch17_building_plan.dwg` and `ch17_utility.lsp` sample files available for download from www.sybex.com/go/autocadcustomization. These sample files should be placed in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the LSP files. Once the files are stored on your system, remove `ch17_` from the name of the LSP file.

#### 7.3.1 Revising the createlayer Function in utility.lsp

The changes you will make to the utility.lsp file update the createlayer function so that the function checks to see if the layer already exists before it creates the layer, instead of the current behavior of automatically creating/modifying the layer. With these changes, the function checks for the existence of the layer with the `tblobjname` function and creates the new layer (if it doesn't already exist) using the entmake function.

The following steps explain how to update the various functions in the utility.lsp file:

1 Open the utility.lsp file in Notepad on Windows or TextEdit on Mac OS.

2 In the text editor area, update the createrlayer function to match the code that follows:

```c
; CreateLayer function creates a layer and 
; expects two argument values. 
(defun createlayer (name color / ) 
  (if (= (tblobjname "layer" name) nil) 
    (entmake (list (cons 0 "LAYER") (cons 100 "AcDbSymbolTableRecord") 
                   (cons 100 "AcDbLayerTableRecord") (cons 2 name) (cons 70 0) 
                   (cons 62 color) (cons 6 "Continuous"))
    ) 
  ) 
) 
```

3 Click File Save.

#### 7.3.2 Creating the Room Label Block Definition

Creating separate drawing files that your custom programs depend on has its advantages and disadvantages. The advantage of creating a separate drawing file is that you can use the AutoCAD user interface to create the block file. However, AutoCAD will need to know where the drawing file is stored so the custom program can use the file. The advantage of creating the block definition through code is that no separate drawing file needs to be maintained, making it easier to share your custom application with your clients or subcontractors.

In these steps, you create a custom function named `roomlabel_createblkdef` that will be used to create the block definition for the room label block if it doesn't already exist in the drawing.

1 Create a new LSP file named roomlabel.lsp using Notepad (on Windows) or TextEdit (on Mac OS).

2 In the text editor area of the roomlabel.lsp file, type the following:

```c
; Creates the block definition roomlabel 
(defun RoomLabel_CreateBlkDef ( / ) 
  (setvar "clayer" "0") 
  ; Start block definition 
  (entmake (list (cons 0 "BLOCK") (cons 2 "roomlabel") 
                 (cons 10 (list 18.0 9.0 0.0)) (cons 70 2))) 
  ; Create the rectangle for around the block attribute 
  (createrectangle (list 0.0 0.0 0.0) (list 36.0 0.0 0.0) (list 36.0 18.0 0.0) (list 0.0 18.0 0.0)) 
  ; Add the attribute definition 
  (entmake (list (cons 0 "ATTDEF") (cons 100 "AcDbEntity") 
                 (cons 8 "Plan_RoomLabel_Anno") (cons 100 "AcDbText") 
                 (cons 10 (list 18.0 9.0 0.0)) (cons 40 9.0) (cons 1 "L000") 
                 (cons 7 "Standard") (cons 72 1) (cons 11 (list 18.0 9.0 0.0)) 
                 (cons 100 "AcDbAttributeDefinition") (cons 280 0) 
                 (cons 3 "ROOM#") (cons 2 "ROOM#") (cons 70 0) (cons 74 2) (cons 280 1))) 
  ; End block definition 
  (entmake (list (cons 0 "ENDBLK"))) 
  (princ) 
)
```

3 Click File Save. The block definition that will be created when the code is executed is shown in Figure 17.1.

1-2『自动生成块参照之前已经学会了 2 种后台方法，而上面是自动生成块定义的实现，目前块定义是人工去做好，然后存放在一个图形 dwg 库里的。如果以后遇到要自动生成块定义的场景，可参考此处的代码。做一张主题卡片。（2021-04-03）』

Figure 17.1 RoomLabel block definition

#### 7.3.3 Inserting a Block Reference Based on the Room Label Block Definition

Once the block definition has been created and added to the block symbol table, it can be inserted into the drawing with the insert command or even used to define a block reference with the entmake function.

In the next exercise steps, you will create three custom functions: `addattrefs`, `changeattvalue`, and `roomlabel_insertblkref`. The `addattrefs` function is a helper function used to add attribute references to a block reference based on the attribute definitions that are part of a block definition. The `changeattvalue` function allows you to revise the insertion point and value of an attribute reference attached to a block reference based on the attribute's tag. The `roomlabel_insertblkref` function creates a block reference based on the RoomLabel block definition that we created with the `roomlabel_createblkdef` function.

1 Open the roomlabel.lsp file with Notepad (Windows) or TextEdit (Mac OS), if it is not already open.

2 In the text editor area of the roomlabel.lsp file, type the following:

```c
; Adds attribute references from a block definition to a block reference 
(defun AddAttRefs (blockName / entityName entityData) 
  ; Gets the entity name for the block definition 
  (setq entityName (tblobjname "block" blockName)) 
  ; Steps through the block definition 
  (while entityName 
    ; Gets the entity data list for the entity 
    (setq entityData (entget entityName)) 
    ; Checks to see if the entity is an attribute definition 
    (if (= (strcase (cdr (assoc 0 entityData))) "ATTDEF") 
      ; Checks to see if the attribute definition is constant or not 
      (if (/= (logand 2 (cdr (assoc 70 entityData)))) 
        (progn 
          ; Converts the object type from ATTDEF to ATTRIB 
          (setq entityData (subst (cons 0 "ATTRIB") (assoc 0 entityData) entityData)) 
          (setq entityData (subst (cons 100 "AcDbAttribute") (cons 100 "AcDbAttributeDefinition") entityData)) 
          ; Removes the Handle, entity name, and owner from 
          ; the entity data list 
          (foreach dxfGroupCode (list -1 5 330 3) ; 67 210 
            (setq list_begin (reverse (cdr (member (assoc dxfGroupCode entityData) (reverse entityData))))) 
            (setq list_end (cdr (member (assoc dxfGroupCode entityData) entityData))) 
            (setq entityData (append list_begin list_end)
          ) 
        ) 
        ; Creates the new attribute reference based on 
        ; the attribute definition 
        (entmake entityData) 
        ) 
      ) 
    ) 
    ; Gets the next block in the block definition 
    (setq entityName (entnext entityName))
  ) 
  (princ) 
) 

; Changes the value of an attribute reference in a block reference 
(defun ChangeAttValue (blkRefEntityName insPt attTag newValue / entityName entityData) 
  ; Gets the first object in a block reference 
  (setq entityName (entnext blkRefEntityName)) 
  ; Steps through the block reference 
  (while entityName 
    ; Gets the entity data list for the entity 
    (setq entityData (entget entityName)) 
    ; Checks to see if the entity is an attribute definition 
    (if (= (strcase (cdr (assoc 0 entityData))) "ATTRIB") 
      ; select attribute by attTag
      (if (= (strcase (cdr (assoc 2 entityData))) (strcase attTag)) 
        (progn 
          ; Update the attribute value 
          (entmod (setq entityData (subst (cons 1 newValue) (assoc 1 entityData) entityData))) 
          ; Changes the position of the attribute 
          (if (/= insPt nil) 
            (progn 
              (entmod (setq entityData (subst (cons 10 insPt) (assoc 10 entityData) entityData))) 
              (entmod (setq entityData (subst (cons 11 insPt) (assoc 11 entityData) entityData))) 
            ) 
          ) 
          (entupd entityName) 
        ) 
      ) 
    ) 
    ; Gets the next block in the block reference 
    (setq entityName (entnext entityName)) 
  ) 
  (princ) 
) 

; Creates the block definition roomlabel 
(defun RoomLabel_InsertBlkRef (insPoint labelValue / blkLayer) (setq blkLayer "Plan_RoomLabel_Anno") 
  ; Creates the "Plan_RoomLabel_Anno" layer 
  (createlayer blkLayer 150) 
  ; Checks to see if the block definition exists in the drawing; 
  ; if not, the block definition is added 
  (if (= (tblobjname "block" "roomlabel") nil) 
    (RoomLabel_CreateBlkDef) 
  ) 
  ; Creates the block reference 
  (entmake (list (cons 0 "INSERT") (cons 8 blkLayer) 
                 (cons 100 "AcDbEntity") (cons 100 "AcDbBlockReference") 
                 (cons 66 1) (cons 2 "roomlabel") (cons 10 insPoint))) 
  ; Adds the attribute references to the block reference 
  (AddAttRefs "roomlabel") 
  ; Ends block reference 
  (entmake (list (cons 0 "SEQEND") (cons 100 "AcDbEntity"))) 
  ; Changes the attribute value of the "ROOM#" 
  (ChangeAttValue (entlast) insPoint "ROOM#" labelValue) 
  (princ) 
)
```

3 Click File Save.

1『

原来定义块、插入块参照、修改块属性的借鉴代码是在这里，之前没找到。好在后来通过其他途径找到了实现方法，具体详见设计流源码。这几个功能是「基石」性技术。（2021-03-12）

补充：在 `AddAttRefs` 里收获的几个知识点：1）判断等式逻辑的简单写法：`(/= (logand 2 (cdr (assoc 70 entityData))))`。2）复制 entityData 时要去掉不要的 DXF 码（ -1 5 330 3），用过滤数组的函数比作者的实现更简洁，详见设计流里迁移建筑底图的代码。3）`while` 函数的使用场景很多的，脑子里要与这么跟弦。4）遍历获取块中各个属性的数据，关键函数是 `(entnext entityName)`。5）要记得先判断属性值的常量不可变还是可变的。（2021-04-03）

』

#### 7.3.4 Prompting the User for an Insertion Point and Room Number

Now that you have defined the functions for creating the block definition and inserting the block reference into a drawing, you need a function that prompts the user for input. The roomlabel function will allow the user to specify a point in the drawing, provide a new room number, or provide a new prefix. The roomlabel function uses the default number of 101 and a prefix of L.

As you use the `roomlabel` function, it creates and uses a custom dictionary named `My_Custom_Program_Settings` with an entry RoomLabel. If the RoomLabel entry exists, it writes the number and prefix of the last room label that you placed. Closing and reopening the drawing results in the program picking up where you left off.

In these steps, you'll create the custom function roomlabel that uses all the functions that you defined in this exercise to place a RoomLabel block each time you specify a point in the drawing:

1 Open the roomlabel.lsp file with Notepad (Windows) or TextEdit (Mac OS), if it is not already open.

2 In the text editor area of the roomlabel.lsp file, type the following:

```c
; Prompts the user for an insertion point and room number 
(defun c:RoomLabel ( / lastNumber lastPrefix entityName roomLabelEntry val newNumber newPrefix roomLabelEntry mySettings) 
  ; Gets the custom dictionary "My_Custom_Program_Settings" if it exists 
  (setq mySettings (cdr (assoc -1 (dictsearch (namedobjdict) "My_Custom_Program_Settings")))) 
  ; Defines initial values 
  (setq lastNumber 101 lastPrefix "L") 
  ; If the dictionary exists, gets the last used room number 
  (if (/= mySettings nil) 
    (progn 
      ; Gets the last room number from the "RoomLabel" key entry 
      (if (/= (setq roomLabelEntry (dictsearch mySettings "RoomLabel")) nil) 
        (progn 
          ; Gets the previously stored number and prefix 
          (setq lastNumber (cdr (assoc 71 roomLabelEntry))) 
          (setq lastPrefix (cdr (assoc 1 roomLabelEntry))) 
        ) ) 
    ) 
    (progn 
      ; Creates the new "My_Custom_Program_Settings" 
      (setq entityName (entmakex (list (cons 0 "DICTIONARY") (cons 100 "AcDbDictionary")))) 
      (setq mySettings (dictadd (namedobjdict) "My_Custom_Program_Settings" entityName)) 
    ) 
  ) 
  ; If no "RoomLabel" entry exists, creates one based on the defaults 
  (if (= roomLabelEntry nil) 
    (progn 
      (dictadd mySettings "RoomLabel" 
        (entmakex (list (cons 0 "XRECORD")(cons 100 "AcDbXrecord") (cons 1 lastPrefix)(cons 71 lastNumber)))) 
    ) 
  ) 
  ; Displays current values 
  (prompt (strcat "\nPrefix: " lastPrefix "\tNumber: " (itoa lastNumber))) 
  (initget "Number Prefix") 
  ; Prompts the user for an insertion point 
  (while (setq val (getpoint (strcat "\nSpecify point for room label (" lastPrefix (itoa lastNumber) ") or change [Number/Prefix]: "))) 
    ; Checks to see if the user provided a keyword or insertion point 
    ; User provided a string 
    (cond 
      ((= (type val) 'STR) 
        (if (= (strcase val) "NUMBER") 
          ; User specified to enter a number 
          (progn 
            (setq newNumber (getint (strcat "\nEnter new room number <" (itoa lastNumber) ">: "))) 
            (if newNumber (setq lastNumber newNumber)) 
          ) 
          ; User specified to enter a new prefix 
          (progn 
            (setq newPrefix (getstring (strcat "\nEnter new room number prefix <" lastPrefix ">: "))) 
            (if newPrefix (setq lastPrefix newPrefix)) 
          ) 
        ) 
      ) 
      ; User provided a point: insert room label block based on values 
      ((= (type val) 'LIST) 
        (RoomLabel_InsertBlkRef val (strcat lastPrefix (itoa lastNumber))) 
        ; Increments number by 1 
        (setq lastNumber (1+ lastNumber)) 
      ) 
    ) 
      ; Removes and re-creates the "RoomLabel" dictionary entry 
      (dictremove mySettings "RoomLabel") 
      (dictadd mySettings "RoomLabel" 
      (entmakex (list (cons 0 "XRECORD")(cons 100 "AcDbXrecord") (cons 1 lastPrefix)(cons 71 lastNumber)))) 
      ; Displays current values 
      (prompt (strcat "\nPrefix: " lastPrefix "\tNumber: " (itoa lastNumber))) 
      (initget "Number Prefix") 
  ) 
  (princ) 
)
```

3 Click File Save.

#### 7.3.5 Adding Room Labels to a Drawing

The roomlabel.lsp file contains the main roomlabel function, but some of the helper functions you defined in roomlabel.lsp use functions defined in the utility.lsp file.

NOTE: The following steps require a drawing file named `ch17_building_plan.dwg`. If you didn't download the sample files previously, download them now from this book's web page. Place these sample files in the MyCustomFiles folder within the Documents (or My Documents) folder.

The following steps explain how to use the roomlabel function that is in the roomlabel.lsp file:

1 Open `Ch17_Building_Plan.dwg`. Figure 17.2 shows the plan drawing of the office building.

2 Start the appload command. Load the LSP files roomlabel.lsp and utility.lsp. If the File Loading - Security Concerns message box is displayed, click Load.

3 At the Command prompt, type roomlabel then press Enter.

4 At the Specify point for room label (L101) or change [Number/Prefix]: prompt, specify a point inside the room in the lower-left corner of the building. The room-label definition block, `Plan_RoomLabel_Anno` layer, and `My_Custom_Program_Settings` custom dictionary are created the first time the roomlabel function is used. The RoomLabel block definition should look like Figure 17.3 when inserted into the drawing.

5 At the Specify point for room label (L101) or change [Number/Prefix]: prompt, type n and press Enter.

6 At the Enter new room number `<102>`: prompt, type 105 and press Enter.

7 At the Specify point for room label (L105) or change [Number/Prefix]: prompt, type p and press Enter.

8 At the Enter new room number prefix `<L>`: prompt, type R and press Enter.

9 At the Specify point for room label (R105) or change [Number/Prefix]: prompt, specify a point in the large open area in the middle of the building.

10 Press Enter to end roomlabel.

11 Save the drawing with the name RoomLabel Test.dwg , and then close the file.

12 Open RoomLabel Test.dwg, and load the roomlabel.lsp and utility.lsp files.

13 Start the roomlabel function. Press F2 on Windows or Fn-F2 on Mac OS. Notice the current values being used are 106 for the number and a prefix of R, which are the values you used before closing the drawing.

14 Add additional room labels and close the drawing when done.

Figure 17.2 Plan view of the office building

Figure 17.3 Inserted RoomLabel block