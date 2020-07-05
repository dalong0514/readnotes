# 2019114Autolisp-Developers-GuideR01

## 记忆时间

## 0105. Manipulate-AutoCAD-Objects

几种选择集列表（Selection Set Filter Lists）：1）过滤器列表里使用通配符。2）过滤 Extended Data 的选择集。3）过滤器列表里使用 Relational Tests。4）过滤器里用布尔逻辑运算。5）修改选择集（添加或删除选择集中的实体）。

AutoLISP 里有两类操作对象（objects）的函数，一是获取特定对象的实体名（entity name），二是获取或修改特定对象的实体数据（entity data）。获取对象 entity name 的函数有，entsel、nentsel、nentselp、entnext、entlast；增加实体用 entmake，增加复杂实体（complex entity）用多个 entmake；获取实体内部信息用函数 entget，entget 的传入参数是实体的 entity name，那么就可以用 entsel 获取；修改对象实体数据用 entmod；删除对象实体用 entdel。

修改实体数据的基本思路，通过 entget 获得实体的数据列表，直接通过 entmod 修改获取的数据列表，然后将修改后的数据列表传递进整个 CAD 数据库里。

```c
(setq ent (entlast))               ; Set ent to last entity.
(setq entl (entget ent))           ; Set entl to association list of last entity.
```

重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。

You can select and handle objects, and use their extended data. Most AutoLISP ® functions that handle selection sets and objects identify a set or an object by the entity name. For selection sets, which are valid only in the current session, the volatility of names poses no problem, but it does for objects because they are saved in the drawing database. An application that must refer to the same objects in the same drawing (or drawings) at different times can use the objects' handles.

1『处理的逻辑：要么是处理选择集，要么是处理特定的实体。』

AutoLISP uses symbol tables to maintain lists of graphic and non-graphic data related to a drawing, such as the layers, linetypes, and block definitions. Each symbol table entry has a related entity name and handle and can be manipulated in a manner similar to the way other AutoCAD ® entities are manipulated.

1『用 symbol tables 来定位要操作的实体。symbol table entry 也有跟普通实体一样的「实体名」和「头」。回复：感觉 symbol tables 就是 ctrl + I 出来的特性表格。』

### 5.1 About Selecting Objects and Selection Sets (AutoLISP)

Selection sets are groups of one or more selected objects (entities). You can interactively add objects to, remove objects from, or list objects in a selection set. The following example code uses the ssget function to return a selection set containing all the objects in a drawing.

```
(ssget "X")
```

AutoLISP provides a number of functions for handling selection sets. The following lists some of the functions available for working with selection sets: 

1. ssget - Prompts the user to select objects (entities), and returns a selection set; 

2. ssadd - Adds an object (entity) to a selection set, or creates a new selection set; 

3. ssdel - Removes an object (entity) from a selection set; 

4. ssname - Returns the object (entity) name of the indexed element of a selection set; 

5. sslength - Returns an integer containing the number of objects (entities) in a selection set.

1『获得选择集之后，需要靠 ssname，比如获取块选择集里第一个块的实体信息：「(setq ent (entget (ssname ss 0)))」』

The ssget function provides the most general means of creating a selection set. It can create a selection set in one of the following ways: 1) Explicitly specifying the objects to select, using the Last, Previous, Window, Implied, Window Polygon, Crossing, Crossing Polygon, or Fence options; 2) Specifying a single point; 3) Selecting all objects in the database; 4) Prompting the user to select objects. With any option, you can use filtering to specify a list of properties and conditions that the selected objects must match.

1『过滤器和选择集结合起来用。』

3『 ssget 的官方文档：[Pomoc: ssget (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-0F37CC5E-1559-4011-B8CF-A3BA0973B2C3)』

Note: Selection set and entity names do not remain the same between drawing sessions.

1『Selection set and entity names 即使是同一张图，也是在变的。』

The first argument to ssget is a string that describes which selection option to use. The next two arguments, pt1 and pt2, specify point values for the relevant options (they should be left out if they do not apply). A point list, pt-list, must be provided as an argument to the selection methods that allow selection by polygons (that is, Fence, Crossing Polygon, and Window Polygon). The last argument, filter-list, is optional. If filter-list is supplied, it specifies the list of entity field values used in filtering. For example, you can obtain a selection set that includes all objects of a given type, on a given layer, or of a given color. The following table shows examples of calls to ssget:

1『原文里有不少例子，利于理解。』

For example, Creates a selection set from the most recently created selection set:

```
(setq ss1 (ssget "P"))
```

1『 ssget 函数有 3 个形参，第一个形参是内置的参数，各个符号代表选择的方式，详见原文表；第二个形参是「点列表」，可以定选择集的范围；第三个形参是「过滤器」，可以用来过滤实体。』

When an application has finished using a selection set, it is important to release it from memory. This can be done by setting it to nil:

    (setq ss1 nil)

Remember: You can also release the memory used by the values stored in a variable by defining it as a local variable in a function.

Attempting to manage a large number of selection sets simultaneously is not recommended. An AutoLISP application cannot have more than 128 selection sets open at once. (The limit may be lower on your system.) When the limit is reached, AutoCAD will not create more selection sets. Keep a minimum number of sets open at a time, and set unneeded selection sets to nil as soon as possible. If the maximum number of selection sets is reached, you must call the gc function to free unused memory before another ssget will work.

1『要有选择集释放内存、变量释放内存（尽可能用局部变量）的概念。一张图纸里最多同时保存 128 个选择集（可能更少），在函数里用局部变量保存即可，函数调用结束后自动释放。』

### 5.1.1 About Selection Set Filter Lists (AutoLISP)

An entity filter list is an association list that uses DXF group codes in the same format as a list returned by entget.

1『

又见「DXF group codes」。选择集里的 DXF group codes 是通过 entget 函数获取的。比如下面，通过块名筛选出选择集，获取选择集里的第一个块实体的信息：

```
// insert 是块的 type
(setq ss (ssget "X" '((0 . "insert") (2 . "testblock"))))
(sslength ss)
(setq ent (entget (ssname ss 0)))

!ent
// out
((-1 . <图元名: 7ff47f6404d0>) (0 . "INSERT") (330 . <图元名: 7ff47f603820>) (5 . "A588D") (100 . "AcDbEntity") (67 . 0) (410 . "Model") (8 . "管道编号") (100 . "AcDbBlockReference") (66 . 1) (2 . "testblock") (10 16708.2 -17025.4 0.0) (41 . 1.0) (42 . 1.0) (43 . 1.0) (50 . 0.0) (70 . 0) (71 . 0) (44 . 0.0) (45 . 0.0) (210 0.0 0.0 1.0))
```

』

The ssget function recognizes all group codes except entity names (group code -1), handles (group code 5), and xdata (group codes greater than 1000). If an invalid group code is used in a filter-list, it is ignored by ssget. Use the group code -3 to search for objects with xdata. When a filter-list is provided as the last argument to ssget, the function scans the selected objects and creates a selection set containing the names of all main entities matching the specified criteria. The filter-list specifies which property (or properties) of the entities are to be checked and which values constitute a match.

For example, you can obtain a selection set that includes all objects of a given type, on a given layer, or of a given color. The following examples demonstrate different methods of using a filter-list with various object selection options.

If both the group code and the desired value are known, the list may be quoted as shown previously. If either is specified by a variable, the list must be constructed using the list and cons function. For example, the following code creates a selection set of all objects in the database that are on layer FLOOR3:

```c
(setq lay_name "FLOOR3")
(setq ss1
  (ssget "X"
    (list (cons 8 lay_name))
  )
)
```

1『 list(cons 8 lay_name) 等价于图里的表达式 '((8 . lay_name))』

If the filter-list specifies more than one property, an entity is included in the selection set only if it matches all specified conditions, as in the following example code:

```
(ssget "X" (list (cons 0 "CIRCLE")(cons 8 lay_name)(cons 62 3)))
```

This code selects only Circle objects on layer FLOOR3 that are colored green. This type of test performs a Boolean “AND” operation.

3『

[列表构造函数 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%88%97%E8%A1%A8%E6%A7%8B%E9%80%A0%E5%87%BD%E6%95%B8)

列表构造函数是用来构造列表的基本函数，在大多数 LISP 体系的计算机编程语言中，使用的函数名称是 cons。cons 构成了存放两个变量与其指针的内存物件，这个物件被称为 CONS 单元、非原子的 S 表达式或 cons 对。LISP 编程中表达要把 x 加入 y 的语法：(cons x y)，构造了一个新物件。产生的结果具备了左半部，称为 CAR（第一元素或暂存器位址的内容）；以及右半部称为 CDR（其余元素或递减暂存器的内容）。

以上约略与面向对象的构造器概念相关，即产生一个给定参数的新物件，而其与代数数据类型系统的构造函数，更密切相关。「cons」和诸如「cons onto」的词句，也是函数编程的通用术语。有时运算子有类似作用，特别是在列表处理的情况下，被读作「CONS」。（例如 ML，Scala，F＃和 Elm 编程的：运算符，或 Haskell 编程的：运算符，都是向列表的开头添加一个元素。）

使用。虽然 cons 单元可用于储存有序的数据对，但它们更常用于组合为更复杂的复合数据结构，特别是列表和二叉树；有序对。例如 LISP 表达式 (cons 1 2) 产生一个有序的单元，在左半部存放 1，而右半部存放 2。左右次序不能互换（(1 2) 跟 (2 1) 不同）。在 LISP 表示法中，(cons 1 2) 结果会印出如下。须注意 1 和 2 之间的句点；这个 S 表达式是特殊的「点对」（所谓的 cons 对），并不是普通的「列表」。

```
(1 . 2)
```

列表。列表 (42 69 613) 的 Cons 单元图，以 cons 构造函数写成：

```
(cons 42 (cons 69 (cons 613 nil)))
```

此外可用 list 函数写成：

```
(list 42 69 613)
```

LISP 编程中的列表实作在「cons 对」之上。具体地说，每个列表的结构都是：一个空列表 ()，通常被称为 nil 的特殊物件；一个 cons 单元，car 代表这列表的第一个元素，而 cdr 则是包含其余元素的一个子列表。这形成了简单基本的列表，而 cons，car 和 cdr 函数可以操作列表的内容。注意，nil 是个特殊的空列表，并不是「cons 对」。考虑元素为 1,2 和 3 的列表为例。这样的列表经由三个步骤产生：CONS 3 到 nil 空列表之上；CONS 2 到上一步的结果之上；CONS 1 到上一步的结果，产生最后的结果。这相当于单一表达式：

```
(cons 1 (cons 2 (cons 3 nil)))
```

或可用 list 函数节略如下：

```
(list 1 2 3)
```

最终结果是一个列表，形式如右：

```
(1 . (2 . (3 . nil)))
```

通常结果会被打印为：(1 2 3)，因此 cons 操作会在既有列表的最前头，添加一个元素。例如，如果 x 是上面定义的列表，那么 (cons 5 x) 将产生列表：(5 1 2 3) 。另一个有用的函数是 append，用于合并两个列表。

树。cons 也容易建构出在叶片中储存数据的二叉树。例如以下代码： (cons (cons 1 2) (cons 3 4)) 产生了一棵树：

```
((1 . 2) . (3 . 4))
```

技术上，前例中的列表（1 2 3）恰巧是不平衡的二叉树。要看到这点，只需重新排列图：

』

The ssget function filters a selection set by scanning the selected entities and comparing the fields of each main entity against the specified filtering list. If an entity's properties match all specified fields in the filtering list, it is included in the returned selection set. Otherwise, the entity is not included in the selection set. The ssget function returns nil if none of the selected entities match the specified filtering criteria.

Note: The meaning of certain group codes can differ from entity to entity, and not all group codes are present in all entities. If a particular group code is specified in a filter, entities not containing that group code are excluded from the selection set that ssget returns.

When ssget filters a selection set, the selected objects it retrieves might include entities from both paper space and model space. However, when the selection set is passed to an AutoCAD command, only entities from the space that is currently in effect are used. (The space to which an entity belongs is specified by the value of its 67 group code.)

1『实现选择哪个图纸空间里的实体，上面的信息以后应该可以用到。』

About Wild-Card Patterns in Selection Set Filter Lists (AutoLISP). Symbol names specified in filtering lists can include wild-card patterns. The wild-card patterns recognized by ssget are the same as those recognized by the wcmatch function. When filtering for anonymous blocks, you must precede the * character with a reverse single quotation mark ( ` ), also known as an escape character, because the * is read by ssget as a wild-card character. For example, you can retrieve an anonymous block named *U2 with the following:

    (ssget "X" '((2 . "`*U2")))

1『 wild-card 是指通配符。` 应该是转义用的；』

1『选择特定名称块的实现方式，mark 一下。可以用来提取块里的基本信息用，做设备表的一个环节；过滤器的形参必须是一个 list，'() 应该就是一个 list 的简要表达方式。所以这个表达式可以换一个方式：list(cons 2 "`*U2")。』

About Filtering for Extended Data in a Selection Set (AutoLISP). You can select all entities containing extended data for a particular application using the filter-list argument of ssget. The filter-list argument must be a list that contains -3 as its first element. The following example code selects all the objects in a drawing that include extended data for the "APPNAME" application:

    (ssget "X" '((-3 ("APPNAME"))))

1『「extended data」的概念；Group Code 为 -3，是指 APP: extended data (XDATA) sentinel (fixed)。』

You can also expand the scope of the filter to filter specific types of objects. The following example code selects all the circles in a drawing that include extended data for the "APPNAME" application:

    (ssget "X" '((0 . "CIRCLE") (-3 ("APPNAME"))))

If more than one application name is included in the -3 group's list, an AND operation is implied and the entity must contain extended data for all of the specified applications. So, the following statement would select all the objects with extended data for both the "APP1" and "APP2" applications:

    (ssget "X" '((-3 ("APP1")("APP2"))))

Wild-card matching is also permitted, so either of the following statements will select all the objects with extended data for either or both of these applications.

    (ssget "X" '((-3 ("APP[12]"))))
    (ssget "X" '((-3 ("APP1,APP2"))))

About Relational Tests in Filter Lists for Selection Sets (AutoLISP). Unless otherwise specified, an equivalency is implied for each item in the filter-list. For numeric group codes (integers, reals, points, and vectors), you can specify other relations by including a special -4 group code that specifies a relational operator. The value of a -4 group code is a string indicating the test operator to be applied to the next group in the filter-list. The following selects all circles with a radius (group code 40) greater than or equal to 2.0:

    (ssget "X" '((0 . "CIRCLE") (-4 . ">=") (40 . 2.0)))

3『group code 0, Text string indicating the entity type (fixed); group code -4, APP: conditional operator (used only with ssget); group code 40, Floating-point values. (text height, scale factors, and so on)』

The possible relational operators are shown in the following table. The use of relational operators depends on the kind of group code value you are testing:

1. All relational operators except for the bitwise operators ("&" and "&=") are valid for both real- and integer-valued groups.

2. The bitwise operators "&" and "&=" are valid only for integer-valued groups.

3. The bitwise AND, "&", is true if ((integer_group & filter) /= 0)—that is, if any of the bits set in the mask are also set in integer_group.

4. The bitwise masked equals, "&=", is true if ((integer_group & filter) = filter)—that is, if all bits set in the mask are also set in integer_group (other bits might be set in the integer_group but are not checked).

4. For point group codes, the X, Y, and Z tests can be combined into a single string, with each operator separated by commas (for example, ">,>,\*"). If an operator is omitted from the string (for example, "=,<>" leaves out the Z test), then the “anything goes” operator, "*", is assumed.

5. Direction vectors (group code 210) can be compared only with the operators "*", "=", and "!=" (or one of the equivalent “not equal” strings).

6. You cannot use the relational operators with string group codes; use wild-card tests instead.

About Logical Grouping of Selection Filter Tests (AutoLISP). You can define test groups with nested Boolean expressions to filter objects from a selection set created with ssget. The following table lists the grouping operators that you can use to filter selection sets:

1『过滤器里用布尔逻辑运算。』

The grouping operators are specified by -4 dxf group codes, like the relational operators. They are paired and must be balanced correctly in the filter list or the ssget call will fail.

```
(ssget "X"
  '(
    (-4 . "<OR")
      (-4 . "<AND")
        (0 . "CIRCLE")
        (40 . 1.0)
      (-4 . "AND>")
      (-4 . "<AND")
        (0 . "LINE")
        (8 . "ABC")
      (-4 . "AND>")
    (-4 . "OR>")
  )
)
```

This filter list allows the selection of all circles with a radius of 1.0 plus all lines on layer "ABC". The grouping operators are not case-sensitive; for example, you can specify "and>", "<or", instead of "AND>", "<OR". Grouping operators are not allowed within the -3 dxf group code. Multiple application names specified in a -3 dxf group code use an implied AND operator. If you want to test for extended data using other grouping operators, specify separate -3 dxf group codes and group them as desired.

The following example code demonstrates how to select all circles having extended data for either application "APP1" or "APP2" but not both:

```
(ssget "X"
  '((0 . "CIRCLE")
    (-4 . "<XOR")
      (-3 ("APP1"))
      (-3 ("APP2"))
    (-4 . "XOR>")
  )
)
```

You can simplify the coding of frequently used grouping operators by setting them equal to a symbol. The previous example could be rewritten as follows (notice that in this example you must explicitly quote each list):

```
(setq <xor '(-4 . "<XOR")
         xor> '(-4 . "XOR>"))

(ssget "X"
  (list
    '(0 . "CIRCLE")
    <xor
    '(-3 ("APP1"))
    '(-3 ("APP2"))
    xor>
  )
)
```

1『体现了「函数」封装思维。』

About Modifying Selection Sets (AutoLISP). Once a selection set has been created, you can add entities to it or remove entities from it with ssadd and ssdel. You can use the ssadd function to create a new selection set or add entities to an existing selection set. The following example code creates a selection set that includes the first and last entities in the current drawing (entnext and entlast):

```
(setq fname (entnext))                 ; Gets first entity in the drawing.
(setq lname (entlast))                 ; Gets last entity in the drawing.
(if (not fname)
  (princ "\nNo entities in drawing. ")
  (progn
    (setq ourset (ssadd fname))        ; Creates a selection set of the first entity.
    (ssadd lname ourset)               ; Adds the last entity to the selection set.
  )
)
```

The example runs correctly even if only one entity is in the database (in which case both entnext and entlast set their arguments to the same entity name). If ssadd is passed the name of an entity already in the selection set, it ignores the request and does not report an error. The following example code removes the first entity from the selection set created in the previous example:

    (ssdel fname ourset)

If there is more than one entity in the drawing (that is, if fname and lname are not equal), then the selection set ourset contains only lname, the last entity in the drawing. The function sslength returns the number of entities in a selection set, and ssmemb tests whether a particular entity is a member of a selection set. Finally, the function ssname returns the name of a particular entity in a selection set, using an index to the set (entities in a selection set are numbered from 0). The following example code shows calls to ssname:

```
(setq sset (ssget))                     ; Prompts the user to create a selection set.
(setq ent1 (ssname sset 0))             ; Gets the name of the first entity in sset.
(setq ent4 (ssname sset 3))             ; Gets the name of the fourth entity in sset.
(if (not ent4)
  (princ "\nNeed to select at least four entities. ")
)
(setq ilast (sslength sset))            ; Finds index of the last entity in sset.
(setq lastent (ssname sset (1- ilast)))     ; Gets the name of the last entity in sset.
```

Regardless of how entities are added to a selection set, the set never contains duplicate entities. If the same entity is added more than once, the later additions are ignored. Therefore, sslength accurately returns the number of distinct entities in the specified selection set.

1『选择集里是不会存在重复的实体的。』

About Passing Selection Sets Between AutoLISP and ObjectARX Applications (AutoLISP). When passing selection sets between AutoLISP and ObjectARX applications, the following should be observed: If a selection set is created in AutoLISP and stored in an AutoLISP variable, then overwritten by a value returned from an ObjectARX application, the original selection set is eligible for garbage collection (it is freed at the next automatic or explicit garbage collection).

This is true even if the value returned from the ObjectARX application was the original selection set. In the following example, if the adsfunc ObjectARX function returns the same selection set it was fed as an argument, then this selection set will be eligible for garbage collection even though it is still assigned to the same variable.

    (setq var1 (ssget))
    (setq var1 (adsfunc var1))

If you want the original selection set to be protected from garbage collection, then you must not assign the return value of the ObjectARX application to the AutoLISP variable that already references the selection set. Changing the previous example prevents the selection set referenced by var1 from being eligible for garbage collection.

    (setq var1 (ssget))
    (setq var2 (adsfunc var1))

About Object Handling (AutoLISP). AutoLISP provides functions for handling objects. The object-handling functions are organized into two categories: functions that retrieve the entity name of a particular object, and functions that retrieve or modify entity data. See Object-Handling Functions (AutoLISP) in AutoLISP Function Synopsis (AutoLISP), for a complete list of the object-handling functions.

1『AutoLISP 里有两类操作对象（objects）的函数：获取特定对象的实体名（entity name）；者获取或修改特定对象的实体数据（entity data）。』

About Accessing an Object’s Entity Name (AutoLISP). An AutoLISP routine must obtain an object’s entity name to make subsequent calls to the entity data or selection set functions. The entsel and nentsel functions prompt the user to interactively select an object in the drawing area and return not only the selected object’s entity name but additional information for the routine's use. 

1『提取 entity name 是很多操作的前提条件，可以用函数 entsel 和 nentsel  实现；nentsel 函数可以提取多段线和块这种复杂对象里的信息；entnext 函数默认参数是第一个实体的 entity name，如果传递给它一个实体的 entity name，那么返回的是该实体的下一个的 entity name；entlast 提取最后一个实体的 entity name，变相就是提取最近的实体信息，应该大有用处；提取对象 entity name 的函数汇总： entsel、nentsel、nentselp、entnext、entlast。』

The entsel function returns both the entity name of the object selected and the center of the pick box when the pointer button on the input device was clicked. Some entity operations require knowledge of the point by which the object was selected. Examples from the set of existing AutoCAD commands include: BREAK, TRIM, and EXTEND. 

The nentsel function returns the same information as the entsel function, except when a complex is selected such as a polyline or block. Both these functions accept keywords if they are preceded by a call to initget.

The entnext function retrieves entity names sequentially. If entnext is called with no arguments, it returns the name of the first entity in the drawing database. If its argument is the name of an entity in the current drawing, entnext returns the name of the succeeding entity. 

The entlast function retrieves the name of the last entity in the database. The last entity is the most recently created main entity, so entlast can be called to obtain the name of an entity that has just been created with a call to command.

You can set the entity name returned by entnext to the same variable name passed to this function. This “walks” a single entity name variable through the database, as shown in the following example code:

```
(setq one_ent (entnext))         ; Gets name of first entity.
(while one_ent
..
                                 ; Processes new entity.
.
(setq one_ent (entnext one_ent))
)                                ; Value of one_ent is now nil.
```

The following example code illustrates how ssadd can be used in conjunction with entnext to create selection sets and add members to an existing set.

```
(setq e1 (entnext))
(if (not e1)                           ; Sets e1 to name of first entity.
  (princ "\nNo entities in drawing. ")
  (progn
    (setq ss (ssadd))                  ; Sets ss to a null selection set.
    (ssadd e1 ss)                      ; Returns selection set ss with e1 added.
    (setq e2 (entnext e1))             ; Gets entity following e1.
    (ssadd e2 ss)                      ; Adds e2 to selection set ss.
  )
)
```

About Entity Context and Coordinate Transform Data (AutoLISP).  The nentsel and nentselp functions are similar to entsel, except they return two additional values to handle entities nested within block references. Another difference between these functions is that when the user responds to a nentsel call by selecting a complex entity or a complex entity is selected by nentselp, these functions return the entity name of the selected subentity and not the complex entity's header, as entsel does.

1『 nentsel、nentselp 函数与常规的 entsel 的区别在于，针对像「块」这种复杂的集合，它们返回的是块里面元素的 entity name，而 entsel 返回的是整个块的 entity name。』

For example, when the user selects a 3D polyline, nentsel returns a vertex subentity instead of the polyline header. You can retrieve the polyline header by making successive calls to entnext, stepping forward to the Seqend subentity, and then obtain the name of the header from the Deqend subentity's -2 dxf group code. The same applies when the user selects attributes in a nested block reference.

Selecting an attribute within a block reference returns the name of the attribute and the pick point. When the selected object is a component of a block reference other than an attribute, nentsel returns a list containing the following elements:

1. The selected entity's name.

2. A list containing the coordinates of the point used to pick the object.

3. The Model to World Transformation Matrix. This is a list consisting of four sublists, each of which contains a set of coordinates. This matrix can be used to transform the entity definition data points from an internal coordinate system called the model coordinate system (MCS), to the World Coordinate System (WCS). The insertion point of the block that contains the selected entity defines the origin of the MCS. The orientation of the UCS when the block is created determines the direction of the MCS axes.

4. A list containing the entity name of the block that contains the selected object. If the selected object is in a nested block (a block within a block), the list also contains the entity names of all blocks in which the selected object is nested, starting with the innermost block and continuing outward until the name of the block that was inserted in the drawing is reported.

The list returned from selecting a block with nentsel is summarized as follows:

```
(<Entity Name: ename1>   ; Name of entity.
  (Px Py Pz)             ; Pick point.
  ( (X0 Y0 Z0)           ; Model to World Transformation Matrix.
  (X1 Y1 Z1)
  (X2 Y2 Z2)
  (X3 Y3 Z3)
)
(<Entity name: ename2>   ; Name of most deeply nested block
  .                      ; containing selected object.
  ..
  <Entity name: enamen>) ; Name of outermost block
)                        ; containing selected object.
```

In the following example, create a block to use with the nentsel function. Use nentsel to select the lower-left side of the square.

    (setq ndata (nentsel))

This code sets ndata equal to a list similar to the following:

```
(<Entity Name: 400000a0>   ; Entity name.
  (6.46616 -1.0606 0.0)    ; Pick point.
  ((0.707107 0.707107 0.0) ; Model to World
  (-0.707107 0.707107 0.0) ; Transformation Matrix.
  (0.0 -0.0 1.0)
  (4.94975 4.94975 0.0)
)
  (<Entity name:6000001c>) ; Name of block containing
                           ; selected object.
)
```

Once you obtain the entity name and the Model to World Transformation Matrix, you can transform the entity definition data points from the MCS to the WCS. Use entget and assoc on the entity name to obtain the definition points expressed in MCS coordinates. The Model to World Transformation Matrix returned by nentsel is a 4×3 matrix—passed as an array of four points—that uses the convention that a point is a row rather than a column. The transformation is described by the following matrix multiplication:

The Mij, where 0 le; i, j le; 2, are the Model to World Transformation Matrix coordinates; X, Y, Z is the entity definition data point expressed in MCS coordinates, and X', Y', Z' is the resulting entity definition data point expressed in WCS coordinates. To transform a vector rather than a point, do not add the translation vector (M30 M31 M32 from the fourth column of the transformation matrix).

Note: This is the only AutoLISP function that uses a matrix of this type. The nentselp function is preferred to nentsel because it returns a matrix similar to those used by other AutoLISP, ObjectARX, and Managed .NET functions.

1『 nentselp 更适用于哪些含有矩阵属性信息的实体。』

Using the entity name previously obtained with nentsel, the following example illustrates how to obtain the MCS start point of a line (group code 10) contained in a block definition:

    (setq edata (assoc 10 (entget (car ndata))))

(10 -1.0 1.0 0.0)

The following statement stores the Model to World Transformation Matrix sublist in the symbol matrix; The following statement applies the transformation formula for X' to change the X coordinate of the start point of the line from an MCS coordinate to a WCS coordinate:

About Entity Data Functions (AutoLISP). The functions described in this section operate on entity data and can be used to modify the current drawing database.

About Adding an Entity without Using the Command Function (AutoLISP). An application can add an entity to the drawing database by calling the entmake function. Like that of entmod, the argument to entmake is a list whose format is similar to that returned by entget. The new entity that the list describes is appended to the drawing database (it becomes the last entity in the drawing). If the entity is a complex entity (an old-style polyline or a block), it is not appended to the database until it is complete.

The following example code creates a circle on the MYLAYER layer:

```
(entmake '((0 . "CIRCLE") ; Object type
  (8 . "MYLAYER")         ; Layer
  (10 5.0 7.0 0.0)        ; Center point
  (40 . 1.0)              ; Radius
))
```

The following entmake restrictions apply to all entities:

1. The first or second member in the list must specify the entity type. The type must be a valid DXF group code. If the first member does not specify the type, it can specify only the name of the entity: group -1 (the name is not saved in the database).

2. AutoCAD must recognize all objects that the entity list refers to. There is one exception: entmake accepts new layer names.

3. Any internal fields passed to entmake are ignored.

4. entmake cannot create viewport entities.

For entity types introduced in AutoCAD Release 13 and later releases, you must also specify subclass markers (DXF group code 100) when creating the entity. All AutoCAD entities have the AcDbEntity subclass marker, and this must be explicitly included in the entmake list. In addition, one or more subclass marker entries are required to identify the specific sub-entity type. These entries must follow group code 0 and must precede group codes that are specifically used to define entity properties in the entmake list. For example, the following is the minimum code required to create a MTEXT entity with entmake:

```
(entmake '(
  (0 . "MTEXT")
  (100 . "AcDbEntity") ; Required for all post-R12 entities.
  (8 . "ALAYER")
  (100 . "AcDbMText")  ; Identifies the entity as MTEXT.
  (10 4.0 4.0 0.0)
  (1 . "Some\\Ptext")
))
```

The following table identifies the entities that do not require subentity marker entries in the list passed to entmake:

About Creating Complex Entities without Using the Command Function (AutoLISP). Complex entities (an old-style polyline or a block) can be created by making multiple calls to entmake, using a separate call for each subentity.

When entmake first receives an initial component for a complex entity, it creates a temporary file in which to gather the definition data and extended data, if present. For each subsequent entmake call, the function checks if the temporary file exists. If it does, the new subentity is appended to the file. When the definition of the complex entity is complete (that is, when entmake receives an appropriate Seqend or Endblk subentity), the entity is checked for consistency; if valid, it is added to the drawing. The file is deleted when the complex entity is complete or when its creation has been canceled. You can cancel the creation of a complex entity by entering entmake with no arguments. This clears the temporary file and returns nil.

No portion of a complex entity is displayed in a drawing until its definition is complete; that is not until the final Seqend or Endblk subentity has been passed to entmake. The entlast function cannot retrieve the most recently created subentity for a complex entity that has not been completed.

As the previous paragraphs imply, entmake can construct only one complex entity at a time. If a complex entity is being created and entmake receives invalid data or an entity that is not an appropriate subentity, both the invalid entity and the entire complex entity are rejected.

Complex entities can exist in either model space or paper space, but not both. If you have changed the current space by invoking either of the AutoCAD MSPACE or PSPACE commands (with command) while a complex entity is being constructed, a subsequent call to entmake cancels the complex entity. This can also occur if the subentity has a 67 dxf group code whose value does not match the 67 dxf group code of the entity header.

Working with Polylines. The following example contains five calls to the entmake function which creates a single complex entity, an old-style polyline. The polyline has three vertices located at coordinates (1,1,0), (4,6,0), and (3,2,0), and has a linetype of DASHED and a color of BLUE. All other optional definition data assume default values.

Working with Blocks. Block definitions begin with a block entity and end with an Endblk subentity. Newly created blocks are automatically entered into the symbol table where they can be referenced. Block definitions cannot be nested, nor can they reference themselves. A block definition can contain references to other block definitions.

1『块是存在 symbol table 里的。』

Note: Before you use entmake to create a block, you should use tblsearch to ensure that the name of the new block is unique. The entmake function does not check for name conflicts in the block definitions table, so you could inadvertently redefine an existing block.

Block references can include an attributes-follow flag (dxf group code 66). If present and equal to 1, a series of attribute (Attrib) entities is expected to follow the Insert object. The attribute sequence is terminated by a Seqend subentity.

About Working With Blocks (AutoLISP). There is no direct method for an application to check whether a block listed in the BLOCK table is actually referenced by an insert object in the drawing. You can use the following code to scan the drawing for instances of a block reference; You must also scan each block definition for instances of nested blocks.

    (ssget "x" '((2 . "BLOCKNAME")))

About Anonymous Blocks (AutoLISP). The block definitions (BLOCK) table in a drawing can contain anonymous blocks (also known as unnamed blocks), that AutoCAD creates to support dynamic blocks, tables, hatch patterns, and associative dimensions.

The entmake function can create anonymous blocks other than \*Tnnn (tables), \*Dnnn (dimensions), and *Xnnn (hatch patterns). Unreferenced anonymous blocks are purged from the BLOCK definition table when a drawing is opened. Referenced anonymous blocks (those that have been inserted) are not purged. You can use entmake to create a block reference (insert object) to an anonymous block. (You cannot pass an anonymous block to the INSERT command.) Also, you can use entmake to redefine the block. You can modify the entities in a block (but not the block object itself) with entmod.

The name (dxf group code 2) of an anonymous block created by AutoLISP, ObjectARX, or Managed .NET has the form *Unnn, where nnn is a number generated by AutoCAD. Also, the low-order bit of an anonymous block's block type flag (dxf group code 70) is set to 1. When entmake creates a block whose name begins with * and whose anonymous bit is set, AutoCAD treats this as an anonymous block and assigns it a name. Any characters following the * in the name string passed to entmake are ignored.

Note: Anonymous block names do not remain constant. Although a referenced anonymous block becomes permanent, the numeric portion of its name can change between drawing sessions.

About Obtaining Entity Information (AutoLISP). The entget function returns the definition data of a specified entity as a list. Each item in the list is specified by a DXF group code. The first item in the list contains the entity's current name. An AutoLISP application can retrieve and output the definition data for the line by using the following example code:

```
(defun C:PRINTDXF ( )
  (setq ent (entlast))               ; Set ent to last entity.
  (setq entl (entget ent))           ; Set entl to association list of last entity.
  (setq ct 0)                        ; Set ct (a counter) to 0.
  (textpage)                         ; Switch to the text screen.
  (princ "\nentget of last entity:")
  (repeat (length entl)              ; Repeat for number of members in list:
    (print (nth ct entl))            ; Output a newline, then each list member.
    (setq ct (1+ ct))                ; Increments the counter by one.
  )
 (princ)                             ; Exit quietly.
)
```

This would output the following:

```
entget of last entity:
(-1 . <Entity name: 1bbd1c8>)
(0 . "LINE")
(330 . <Entity name: 1bbd0c8>)
(5 . "69")
(100 . "AcDbEntity")
(67 . 0)
(410 . "Model")
(8 . "0")
(100 . "AcDbLine")
(10 1.0 2.0 0.0)
(11 6.0 6.0 0.0)
(210 0.0 0.0 1.0)
```

1『上面的代码可以作为通用型函数，获取最近新建实体的一系列实体数据；变量 entl 是一个实体数据的集合体。』

The -1 item at the start of the list contains the name of the entity. The entmod function, which is described in this section, uses the name to identify the entity to be modified. The individual dotted pairs that represent the values can be extracted by using assoc with the cdr function.

Sublists for points are not represented as dotted pairs like the rest of the values returned. The convention is that the cdr of the sublist is the group code's value. Because a point is a list of two or three reals, the entire group is a three- (or four-) element list. The cdr of the group code value is the list representing the point, so the convention that cdr always returns the value is preserved.

The group codes for the components of the entity are those used by DXF. As with DXF, the entity header items (color, linetype, thickness, the attributes-follow flag, and the entity handle) are returned only if they have values other than the default. Unlike DXF, optional entity definition fields are returned whether or not they equal their defaults and whether or not associated X, Y, and Z coordinates are returned as a single point variable, rather than as separate X (10), Y (20), and Z (30) group codes.

All points associated with an object are expressed in terms of that object's Object Coordinate System (OCS). For point, line, 3D line, 3D face, 3D polyline, 3D mesh, and dimension objects, the OCS is equivalent to the WCS (the object points are World points). For all other objects, the OCS can be derived from the WCS and the object's extrusion direction (its 210 group code). When working with objects that are drawn using coordinate systems other than the WCS, you may need to convert the points to the WCS or to the current UCS by using the trans function.

When writing functions to process entity lists, make sure the function logic is independent of the order of the sublists; use assoc to guarantee this. The assoc function searches a list for a group code of a specified type. The following code returns the object type "LINE" (0) from the list entl.

```
(cdr (assoc 0 entl))
```

If the group code specified is not present in the list (or if it is not a valid group code), assoc returns nil.

Caution: Before performing an entget on vertex entities, you should read or write the polyline entity's header. If the most recently processed polyline entity is different from the one to which the vertex belongs, width information (the 40 and 41 group codes) can be lost.

About Modifying an Entity without the Command Function (AutoLISP). An entity can be modified directly by changing its entity list and posting the changes back to the database. The entmod function modifies an entity by passing it a list in the same format as a list returned by entget but with some of the entity group code values (presumably) modified by the application. This function complements entget. The primary mechanism by which an AutoLISP application updates the database is by retrieving an entity with entget, modifying its entity list, and then passing the list back to the database with entmod.

1『修改实体数据的基本思路，通过 entget 获得实体的数据列表，直接通过 entmod 修改获取的数据列表，然后将修改后的数据列表传递进整个 CAD 数据库里。』

The following example code retrieves the definition data of the first entity in the drawing and changes its layer property to MYLAYER.

```
(setq en (entnext))         ; Sets en to first entity name in the drawing.
(setq ed (entget en))       ; Sets ed to the entity data for entity name en.
(setq ed
  (subst (cons 8 "MYLAYER")
    (assoc 8 ed)            ; Changes the layer group in ed.
    ed                      ; to layer MYLAYER.
  )
)
(entmod ed)                 ; Modifies entity en's layer in the drawing.
```

There are restrictions on the changes to the database that entmod can make; entmod cannot change the following:

1. The entity's type or handle.

2. Internal fields. (Internal fields are the values that AutoCAD assigns to certain group codes: -2, entity name reference; -1, entity name; 5, entity handle.) Any attempt to change an internal field—for example, the main entity name in a Seqend subentity (group code -2)—is ignored.

3. Viewport entities. An attempt to change a viewport entity causes an error.

Other restrictions apply when modifying dimensions and hatch patterns. AutoCAD must recognize all objects (except layers) that the entity list refers to. The name of any text style, linetype, shape, or block that appears in an entity list must be defined in the current drawing before the entity list is passed to entmod. The one exception is that entmod accepts new layer names. If the entity list refers to a layer name that has not been defined in the current drawing, entmod creates a new layer. The attributes of the new layer are the standard default values used by the New option of the AutoCAD LAYER command.

1『通过 entmod 修改的数据列表，在传递进数据空间之前，里面的对象必须是全的，「层名」是唯一可以不在数据列表里的对象。』

The entmod function can modify subentities such as polyline vertices and block attributes. If you use entmod to modify an entity in a block definition, this affects all references to that block which exist in model space and paper space. Attributes, unless defined as constant, are not updated for each block reference that exists in a drawing. Also, entities in block definitions cannot be deleted by entdel.

About Deleting an Entity (AutoLISP). Entities can be deleted using the entdel function or AutoCAD ERASE command (with command). Entities are not purged from the database until the end of the current drawing session, so if the application calls entdel on an entity that was deleted during that session, the entity is undeleted. Attributes and old-style polyline vertices cannot be deleted independently of their parent entities. The entdel function and AutoCAD ERASE command only operate on main entities. If you need to delete an attribute or vertex, you can use the AutoCAD ATTEDIT or PEDIT commands with command.





About Entity Handles and Their Uses (AutoLISP). The handent function retrieves the name of an entity with a specific handle. As with entity names, handles are unique within a drawing. However, an entity's handle is constant throughout its life. AutoLISP applications that manipulate a specific database can use handent to obtain the current name of an entity they must use. You can use the AutoCAD LIST command to get the handle of a selected object. The following example code uses handent to obtain and display the entity name that is associated with the handle “5a2”.

1『重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。』

```
(if (not (setq e1 (handent "5a2")))
  (princ "\nNo entity with that handle exists. ")
  (princ e1)
)
```

In one particular editing session, this code might display the following:

<Entity name: 60004722>

In another editing session with the same drawing, the fragment might display an entirely different number. But in both cases the code would be accessing the same entity. The handent function has an additional use. Entities can be deleted from the database with entdel. The entities are not purged until the current drawing ends. This means that handent can recover the names of deleted entities, which can then be restored to the drawing by a second call to entdel.

Note: Handles are provided for block definitions, including subentities.

Entities in drawings that are cross-referenced by way of XREF Attach are not actually part of the current drawing; their handles are unchanged but cannot be accessed by handent. However, when drawings are combined by means of INSERT, INSERT *, XREF Bind (XBIND), or partial DXFIN, the handles of entities in the incoming drawing are lost, and incoming entities are assigned new handle values to ensure each handle in the current drawing remains unique.

About Entity Data Functions and the Graphics Screen (AutoLISP). Changes to the drawing made by the entity data functions are reflected on the graphics screen, provided the entity being deleted, undeleted, modified, or created is in an area and on a layer that is currently visible.

There is one exception; when entmod modifies a subentity, it does not update the image of the entire (complex) entity. If, for example, an application modifies 100 vertices of an old-style polyline with 100 calls to entmod, the time required to recalculate and redisplay the entire polyline is unacceptably slow. Instead, an application can perform a series of subentity modifications, and then redisplay the entire entity with a single call to the entupd function.

Consider the following; if the first entity in the current drawing is an old-style polyline with several vertices, the following code modifies the second vertex of the polyline and regenerates its display.

```
(setq e1 (entnext))    ; Sets e1 to the polyline's entity name.
(setq v1 (entnext e1)) ; Sets v1 to its first vertex.
(setq v2 (entnext v1)) ; Sets v2 to its second vertex.
(setq v2d (entget v2)) ; Sets v2d to the vertex data.
(setq v2d
  (subst
    '(10 1.0 2.0 0.0)
    (assoc 10 v2d)     ; Changes the vertex's location in v2d
    v2d                ; to point (1,2,0).
  )
)
(entmod v2d)           ; Moves the vertex in the drawing.
(entupd e1)            ; Regenerates the polyline entity e1.
```

The argument to entupd can specify either a main entity or a subentity. In either case, entupd regenerates the entire entity. Although its primary use is for complex entities, entupd can regenerate any entity in the current drawing.

Note: To ensure that all instances of the block references are updated, you must regenerate the drawing by invoking the AutoCAD REGEN command (with command). The entupd function is not sufficient if the modified entity is in a block definition.

1『用脚本修改块的信息后，还得在 CAD 里用命令 REGEN 更新一下。』

About Non-Graphical Object Handling (AutoLISP). A drawing database contains two types of non-graphical objects: dictionary and symbol table objects. Although there are similarities between these object types, they are handled differently. All object types are supported by the entget, entmod, entdel, and entmake functions, although object types individually dictate their participation in these functions and may refuse any or all processing. With respect to AutoCAD built-in objects, the rules apply for symbol tables and for dictionary objects.

All rules and restrictions that apply to graphical objects apply to non-graphical objects as well. Non-graphical objects cannot be passed to the entupd function. When using entmake, the object type determines where the object will reside. For example, if a layer object is passed to entmake, it automatically goes to the layer symbol table. If a graphical object is passed to entmake, it will reside in the current space (model or paper).

About Extended Data - Xdata (AutoLISP). Several AutoLISP functions are provided to handle extended data (xdata), which is created by routines written with AutoLISP, ObjectARX, or Managed .NET. If an entity contains xdata, it follows the entity's regular definition data. You can retrieve an entity's extended data by calling entget. The entget function retrieves an entity's regular definition data and the xdata for those applications specified in the entget call.

When xdata is retrieved with entget, the beginning of extended data is indicated by a -3 dxf group code. The -3 dxf group code is in a list that precedes the first 1001 dxf group code. The 1001 dxf group code contains the application name of the first application retrieved, as shown in the table and as described in the topics in this section.

Extended data consists of one or more 1001 group codes, each of which begin with a unique application name. The xdata groups returned by entget follow the definition data in the order in which they are saved in the database. Within each application's group, the contents, meaning, and organization of the data are defined by the application. AutoCAD maintains the information but does not use it. The table also shows that the group codes for xdata are in the range 1000-1071. Many of these group codes are for familiar data types, as follows:

About Registered Applications (AutoLISP). An application must register its name or names to be recognized by AutoCAD. Extended data must contain an application name before it can be attached to an entity and that application name must also exist in the APPID symbol table. Registration is done with the regapp function, which specifies a string to use as an application name. If it successfully adds the name to APPID, it returns the name of the application; otherwise it returns nil. A result of nil indicates that the name is already present in the symbol table. This is not an actual error condition but an expected return value, because the application name needs to be registered only once per drawing.

Before you register an application, you should first check to see if the name is not already in the APPID symbol table. If the name is not there, the application must register it. Otherwise, it can simply go ahead and attach the extended data to an entity for the application. The following example code demonstrates the typical use of regapp.

```
(setq appname "MYAPP_2356")                            ; Unique application name.
(if (tblsearch "appid" appname)                        ; Checks if already registered.
  (princ (strcat "\n" appname " already registered."))

  (if (= (regapp appname) nil)                         ; Some other problem.
    (princ (strcat "\nCan't register XDATA for " appname ". "))
  )
)
```

The regapp function provides a measure of security, but it cannot guarantee that two separate applications have not chosen the same name. One way of ensuring this is to adopt a naming scheme that uses the company or product name and a unique number (like your telephone number or the current date and time).
