# 2019116AutoCAD-Platform-CustomizationR00

## 记忆时间

## 资源汇总

[HyperPics: Resources for the AutoCAD and AutoCAD LT Programs](http://www.hyperpics.com/)

## 卡片

### 0101. 主题卡——封装判断数据类型的函数

You can use the AutoLISP type function to identify the type of data retuned by a function or assigned to a variable. The following shows the syntax of the type function:

```c
(type value)
```

value. The value argument represents any valid atom; an AutoLISP expression, a value, or a variable.

The type function returns a symbol that can be used to determine if the value returned by a function or assigned to a variable is the type of data you are expecting. The following AutoLISP expressions define a custom function named IsString, which uses the type function to determine whether a value is of the string data type:

```c
(defun IsString (val / ) 
  (if (= (type val) 'STR) T nil) 
)
```

You can use the IsString function by entering it at the AutoCAD Command prompt or loading it as part of an AutoLISP (LSP) file. When the function is executed, it will return T if the value it is passed is a string data type or nil for all other data types. The following shows several examples of the IsString function along with the values they return:

```c
(IsString "2") 
// out 
T 

(IsString 2) 
// out
nil 

(IsString PAUSE) 
// out
T 

(IsString PI) 
// out
nil
```

1-2『完全可以自己做一些判断数据类型的函数，封装起来自己用，真切的感觉到，一切语法即为语法糖。封装判断数据类型的函数，做一张主题卡片。』——已完成

### 0102. 主题卡——如何获取用 entmake 函数新建一个实体对象所需的参数

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

The DXF group codes 67, 410, 8, and 210 are optional; if they aren't provided as part of the entity data list, AutoCAD uses the current settings and context of the drawing to populate the values of the properties they represent. Table 16.3 describes the DXF group codes 67, 410, 8, and 210.

After removing the DXF group codes that are optional, the entity data list becomes even easier to understand:

```c
((0. "CIRCLE") (100. "AcDbEntity") (100. "AcDbCircle") (10 5.0 6.5 0.0) (40. 2.0))
```

The entity data list that now remains with the DXF group codes 0, 100, 10, and 40 represents the entity data needed to create a new circle with the entmake function. For additional information on DXF group code values, search on「DXF entities section」in the AutoCAD Help system. Table 16.4 describes the DXF group codes 0, 100, 10, and 40.

Once you have the entity data list that describes the object you want to create, it can then be passed to the entmake function. If the entmake function is able to successfully create the new object, an entity data list is returned. If not, nil is returned. The following shows the syntax of the entmake function:

```c
(entmake [entlist])
```

The entlist argument represents the entity data list of the object to be created, and it is an optional argument. The list must contain all required dotted pairs to define the object and its properties. The following examples show how to create an entity data list with the list and cons functions, and then use the resulting list to create an object with the enmake function:

1-2『这里捡到金子了，教你如何获取用 entmake 函数新建一个实体对象需要哪些必要 `entity data list`。1）在 CAD 图纸里用普通命令画一个实体，或插入一个块实体。2）用命令 `(entget (entlast))` 查看刚刚生成的实体所包含的 `entity data list`。3）扣除掉 DXF group codes 为 -1、5 和 300 的这三个自动生成的数据。4）扣除一些可选数据。5）使用 entmake 函数创建。

先用半成品（command 实现）的命令，自动就生成一个块。然后再用 entlast 命令获取其数据信息。（2020-10-30）

做一张主题卡片。』——已完成

### 0103. 主题卡——修改实体数据的 2 种方法

AutoLISP offers two different methods for modifying the properties of an object directly. The easier of the two methods is to use the object property functions that were introduced with AutoCAD 2012. These functions require less code than the legacy approach of getting and manipulating the entity data list of an object. The property-related functions are less cryptic than entity data list manipulation as well, because you don't need to understand the various DXF group codes associated with a specific object. The downside to these functions is that they work only with AutoCAD 2012 and later, so if you need to support an earlier release you will need to manipulate entity data lists (which I cover in the next section).

Table 16.6 lists the AutoLISP functions available in AutoCAD 2012 and later that can be used to list, get, and set the properties of an object.

|  Function | Description  |
|---|---|
|  dumpallproperties |  Returns all of the properties for the specified object |
|  getpropertyvalue |  Returns the current value of an object's property |
|  setpropertyvalue |  Assigns a value to an object's property |
|  ispropertyreadonly |  Returns T or nil based on whether an object property is read-only |

1-2『看到这里才知道，之前一直用的传统方法：通过实体名称结合 `entget` 函数获取实体的「数据集」，通过替换数据集里的「点对」来实现修改属性。原来还有第二种方法，直接用 autolisp 封装好的函数，前提是只支持 AutoCAD 2012 以后的，可以接受。修改实体数据的 2 种方法，做一张主题卡片。』——已完成

### 0104. 主题卡——获取并修改实体对象上的 XData

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

This exercise shows how to list the XData attached to a dimension with a dimension override.

NOTE: I mentioned earlier that XData doesn't affect the appearance of an object, and that is still true even when used as we did in the previous exercise. XData itself doesn't affect the object, but AutoCAD does look for its own XData and uses it to control the way an object might be drawn. If you implement an application with the Autodesk® ObjectARX® application programming interface, you could use ObjectARX and XData to control how an object is drawn onscreen. You could also control the way an object looks using object overrules with Managed.NET and XData. ObjectARX and Managed.NET are the two advanced programming options that Autodesk supports for AutoCAD development. You can learn more about ObjectARX and Managed.NET at www.objectarx.com.

The entget function can be used to determine whether an XData list for a specific application is already attached to an object. If an XData list already exists for an object, you can then modify that list. Use the subst function to update or replace one XData list with another.

This exercise shows how to override the color assigned to dimension and extension lines, and restore the arrowhead for the dimension you created in the previous exercise.

1-2『上面介绍了修改 XData 的具体方法，以后要实现的一个重要功能需要借鉴里面的代码。管道号块的插入点结合多段线的坐标点（单一直线有 2 个 dxf code 为 10 的点、折一下的有 3 个点，折 2 下有 4 个点），给每个多段线打上管道号的标签，此标签存在 XData。反向再通过多段线给每个阀门（采用区域覆盖的块）打上管线号的标签。那么阀门和管线号的数据就关联上了，管段表和材料表就可以自动生成了，哈哈。做一张主题卡片。（2020-10-32）』

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

### 0201. 术语卡——Dotted Pair

Dotted Pair. A dotted pair is a list of two values separated by a period. Dotted pairs are commonly used to represent property values for an object. The first value of a dotted pair is sometimes referred to as a DXF group code. For example, `(40 . 2.0)` represents the radius of a circle; DXF group code value 40 indicates the radius property, and 2.0 is the actual radius value for the circle. When you're assigning a dotted pair to a variable, either the pair must be preceded by an apostrophe, as in `(setq dxf_40 '(40 . 2))`, or you must use the AutoLISP cons function, as in `(setq dxf_40 (cons 40 2))`. You'll learn more about creating and manipulating dotted pairs in Chapter 16.

2『 Dotted Pair 做一张术语卡片。』——已完成

### 0202. 术语卡——XData

Each object in a drawing has a pre-established set of properties that define how that object should appear or behave. These properties are used to define the size of a circle or the location of a line within a drawing. Although you can't add a new property to an object with AutoLISP, you can append custom information to an object. The custom information that you can append to an object is known as extended data, or XData.

XData is structured similar to an entity data list except the values must be within a specific range of DXF group codes. Each XData list must contain an application name to identify one XData list from another since several XData lists can be attached to an object. After the application name, an XData list can contain any valid values and be of any type of data that AutoLISP supports.

The values in an XData list and what they represent is up to you, the creator of the data. Data in an XData list can be used to identify where an object should be placed or which layer it should be on, to store information about an external database record that is related to an object, or to build relationships between objects in a drawing. The way data is used or enforced is up to you as the programmer.

In addition to XData, graphical and nongraphical objects support what are known as extension dictionaries. Extension dictionaries are kind of like record tables that can be attached to an object. For example, you could store revision history of a drawing in an extension dictionary that is attached to model space, and then populate that information in the drawing's title block. I discuss creating custom dictionaries in Chapter 17.

2『 XData 做一张术语卡片。』——已完成

Once you have defined an application name and registered it in a drawing, you can attach an XData list to an object within that drawing. An XData list is made up of two lists and has a total size limit of 16 KB per object (see the「Managing the Memory Used by XData for an Object」sidebar for information). The outer list contains a DXF group code -3 and an inner list that contains the application name and dotted pairs that represent the data values to store with the object. Each dotted pair contains a DXF group code that defines the type of data the pair represents and then the actual value of the pair.

DXF group codes used for dotted pairs in an XData list must be within the range of 1000 to 1071. Each DXF group code value in that range represents a different type of data, and you can use each DXF group code more than once in an XData list. Table 16.8 lists some of the commonly used DXF group codes for XData.

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

### 0203. 术语卡——图形数据和非图形数据

The AutoLISP® programming language is great for creating and modifying objects. There are two types of objects that you can create or modify: graphical and nongraphical. Graphical objects are those that you can see and interact with in the drawing area, whether in model or paper space. Nongraphical objects are those that you don't create in the drawing area but that can affect the appearance of graphical objects. I discuss working with nongraphical objects in Chapter 17,「Creating and Modifying Nongraphical Objects.」

2『图形数据和非图形数据，做一张术语卡片。』——已完成

### 0204. 术语卡——Block Definitions and Block References

Block references are often misunderstood by new (and even experienced) AutoLISP developers. Blocks are implemented as two separate objects: block definitions and block references. Block definitions are nongraphical objects that are stored in a drawing and contain the geometry and attribute definitions that make up how the block should appear and behave in the drawing area. A block definition can also contain custom properties and dynamic properties.

Understanding Block Definitions and Block References. You can think of a block definition much like a cookie recipe. The recipe lists the ingredients that make up the cookie and explains how those ingredients are combined for a particular taste, but it doesn't control where the dough will be placed on the baking sheet or the size of the unbaked cookies. The placement and amount of the cookie dough on the sheet would be similar to a block reference in a drawing.

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

1『目前无法生成完整的块实体，生成的块只有参照没属性值。用 `entmake` 结合 `ATTRIB` 无效。（2020-10-30）』

### 0205. 术语卡——选择集

A selection set, sometimes known as a selection set name or ssname for short, is a temporary container that holds a reference to objects in a drawing. AutoLISP represents a selection set with the PICKFIRST data type. You get a selection set, commonly based on the objects in a drawing that the user wants to modify or interact with. For example, when you see the Select objects: prompt AutoCAD is asking you to select the objects in the drawing you want to work with and it gets a selection set containing the objects you selected in return.

In addition to getting a selection set based on user input, you can create a selection set manually and add objects to it. You might want to create a function that steps through a drawing and locates all the objects on a specific layer, and then returns a selection set that the next function can work with. Once a selection set is created, you can add additional objects or remove objects that don't meet the requirements you want to work with. A selection set makes it efficient to query and modify a large number of objects.

2『选择集的概念做一张术语卡片。』——已完成

### 0301. 任意卡——生成 VLX 文件

VLX 文件是 LSP 文件编译后的成品文件。在 Visual LISP 编译器里，「文件 -> 生成应用程序 -> 新建应用程序向导」，按步骤一步步来。

### 0302. 任意卡——数据存到公共变量（内存）

TIP: User-defined variables are normally accessible only from the drawing in which they are defined, but you can use the AutoLISP vl-bb-ref and vl-bb-set functions to define variables on what is known as the blackboard. The blackboard is a centralized location for defining variables that can be accessed from any open drawing. The AutoLISP vl-propagate function can also be used to define a variable with a specific value in all open drawings and any drawings that are subsequently opened in the AutoCAD session. You can learn more about these functions in the AutoCAD Help system.

1-2『上面的几个函数，可以实现把一些数据放到公共变量（内存）中，保证所有打开的图纸空间都可以访问到。这个可以帮助实现把数据从流程图迁移到设备布置图，功能待开发，哈哈。做一张任意卡片。（2020-10-08）』——已完成

### 0303. 任意卡——宏命令里的悬停

When the command function is used, you can suspend the execution of an AutoLISP program and allow the user to provide input at the Command prompt. You use the predefined PAUSE variable or the "\\" ASCII character sequence to allow the user to provide a value. The following AutoLISP expression starts the circle command and then allows the user to specify a center point. Once a center point is specified, the circle's diameter is set to 3 units.

```c
(command "._circle" PAUSE "_d" 3)
```

2『宏命令里的悬停，做一张任意卡片。』——已完成

### 0304. 任意卡——自定义命令变为内置命令

TIP: Although custom AutoLISP functions that have the C: prefix aren't recognized as native AutoCAD commands, you can use the AutoLISP vlax-add-cmd and vlax-remove-cmd functions to register a custom AutoLISP function as a built-in AutoCAD command. (These functions are available only on Windows.) There are a couple reasons you might want to do so. The first is so that your custom functions trigger events or reactors related to when a command starts or ends. The other reason is so that your custom function can be called with the command or command-s function. You can learn more about these functions in the AutoCAD Help system.

2『自定义命令变为内置命令的实现手段，做一张任意卡片。』——已完成

### 0305. 任意卡——函数以 princ 结尾的真正用途
```c
; Safely divides two numbers 
; Checks to make sure that one or both of the numbers are not zero 
; (/s 0 2) 
(defun /s (num1 num2 / quotient) 
  (setq quotient 0) 
  (if (and 
        (not (zerop num1)) 
        (not (zerop num2)) 
      ) 
      (/ num1 num2)
      0
  )
) 

(/s 0 3) 
0
(/s 3 0) 
0
(/s 2 3) 
0 
(/s 2.0 3) 
0.666667
```

TIP: Using the AutoLISP princ function in the last statement of a custom AutoLISP function allows that function to「exit quietly」and not return a value. This technique is commonly used when a function's name is prefixed with c:. I cover the princ function in Chapter 15.

1『汇总：1）上面的写法更简洁，写条件语句的时候值得借鉴。2）算是搞明白函数结尾用 `(princ)` 的真正用途了，阻止返回最后一条语句返回的值。做一张任意卡片。（2020-10-08）』

### 0306. 任意卡——调整窗口布局

Tiles are stacked vertically in a dialog box by default, unless you use what are called cluster tiles. Cluster tiles are used to group and align tiles in rows and columns. Tiles also support several attributes that help you control their size and alignment in a dialog box. In addition to cluster tiles and attributes, spacer tiles can be used to control the size and alignment of tiles. A spacer tile allows for the insertion of empty space between tiles in a dialog box.

1-2『调整窗口布局的几种方式汇总：1）用 cluster tiles 控制。2）用 tile 里的属性控制。3）用 spacer tiles 控制。做一张任意卡片。』——已完成

### 0307. 任意卡——加载显示窗口的 2 种方法

You can create a DCL file with Notepad or the Visual LISP Editor; you follow the same process you use to create a LSP file. The only difference is that you specify a file extension of .dcl instead of .lsp. Once you create a DCL file, you can add a dialog box definition to the file. To see what the dialog box looks like, you must load the DCL file in the AutoCAD drawing environment and display it. There are two approaches available for viewing a DCL file. The first is to create an AutoLISP program that loads and displays the file; the other involves using the Visual LISP Editor. (The second approach eliminates the need to write any code.) I discuss how to load a DCL file and display a dialog box in the next section.

1『加载显示窗口（box）的 2 种方法，做一张任意卡片。』——已完成

回复：目前一直用的是第一种方法，即在 autolisp 里加载 dcl 文件。（2020-10-27）

### 0308. 任意卡——通过特定的动作直接更新交互界面的下拉列表数据

Populating the Items of a `list_box` or `popup_list` Tile.

The `list_box` and `popup_list` tiles allow the user to select one or more predefined values from a list. The items available in the list of the two tiles can be specified using the tile's list attribute or AutoLISP functions. The `start_list` function is used to assign, update, or replace the list of values applied to a `list_box` or `popup_list` tile. When a list can be modified, the `start_list` function returns the name of the list; otherwise the function returns nil, indicating the list isn't accessible for modification. Typically, a list isn't available for modification because you provided an incorrect key to the `start_list` function or the function was called before the execution of the `new_dialog` function.

The following shows the syntax of the `start_list` function:

```c
(start_list key [mode [idx]])
```

Here are its arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile you want to modify.

mode. The mode argument is an integer value that specifies how the list currently assigned to the tile can be modified. Table 23.9 describes each of the available modes.

idx. The idx argument is an integer value that specifies an item in the list. The item is used to indicate which item to change if the mode is set to 1; when the mode is set to 2, it indicates the starting item you want to begin appending new items to.

Table 23.9 describes the modification modes that can be used to edit a list.

|  Mode | Description  |
|---|---|
| 1 | Next call to `add_list` replaces the item indicated by the idx argument. |
| 2 | Next call to `add_list `appends a new item after the item indicated by the idx argument. If an index isn't provided, the new item is appended after the last item in the list. |
| 3 | Items in the list are cleared and a new item is appended. |

After a tile key, mode, and index have been specified with the `start_list` function, you can change or add new items with the `add_list` function. The `add_list` function accepts a single argument of a string value. This value is the text that will be displayed in the list of the `list_box` or `popup_list` tile. If the value is successfully added to the list, the string passed to the `add_list` function is returned; otherwise, nil is returned, indicating the item wasn't added.

Once you have modified a list, use the `end_list` function. The `end_list` ends the modification of the list that was started with the `start_list` function. The `end_list` function returns a value of nil regardless of whether the list was successfully modified.

1-2『目前还没想到，直接在交互界面里给下拉菜单添加元素的应用场景。回复：想到应用场景了，比如筛选选择集之后，将选集里的相关内容直接在交互界面上呈现出来，就跟 CAD 原生查询面板一样。（2020-10-09）回复：这个功能其实非常有用，比如想开发的功能，先根据某个属性值匹配通配符来筛选管道号块，筛出来的块只把属性值提取出来添加到这个列表让用户看到。第二部输入要替换的原字符以及新字符，这个功能一定要实现。（2020-10-10）做一张任意卡片。』——已完成

The following code shows how to replace and assign a list of two values to a `popup_list` tile with the key of `list_layers`. The `list_layers` key refers to the Layer To Place Object On `popup_list` tile of the `ex_createLabelObject` dialog definition you created in the「Creating and Previewing a Dialog in a DCL File」section.

```c
; Clear and replace the list of the popup_list 
(start_list "list_layers" 2) 
; Add two items that represent the layers to allow 
(add_list "A-Door") 
(add_list "A-Window") 
; End list modification (end_list)
```

NOTE: The `set_tile` and `mode_tile` functions shouldn't be executed between the use of the `start_list` and `end_list` functions. Execute the `start_list` and `end_list` functions before the `start_dialog` function to ensure that the list is updated before the dialog box is displayed.

1『注意几个函数的调用顺序。（2020-10-09）』

### 0309. 任意卡——如何在一个 lsp 文件里调用另外一个 lsp 文件

直接在 lsp 里写加载语句 `(load "utility.lsp")`，然后在 CAD 里用命令 `appload` 同时加载这两个函数即可。

### 0310. 任意卡——创建实体数据的 2 个方法

The command function is the most common method that AutoLISP programmers use to create and modify objects, but it isn't the most efficient when you are trying to modify individual properties of an object. Even creating lots of objects in the Autodesk® AutoCAD® program can be slower with the command function. Along with the command function, objects can be created and modified directly by setting property values as part of an entity data list. Extended data (XData) can also be attached to an object as a way to differentiate one object from another or, in some cases, to affect the way an object might look in the drawing area.

1-2『直接用 command，自己就遇到了瓶颈。1）确实效率低下。2）自动生成辅助流程组件，插进来的块，位置经常不是均匀的，目前一直找到不解决办法。正巧这里受到启发，改用直接创建实体数据的方法实现自动生成块。待实现。做一张任意卡片。（2020-10-29）』

Using AutoLISP, you can create a table using the entmake function while modifying and populating the table with the entget and entmod functions.

### 0311. 任意卡——获取实体数据信息

除了用选择集的方式，先获得选择集，通过选择集获取各个实体的实体名，再通过实体名获得实体的数据集。也可以通过下面的方式直接获取实体数据集。

AutoLISP provides two different techniques that can be used to select an individual object within a drawing—through code or via user interaction. When you want to work with the most recent object or step through all of the objects in a drawing, you don't need any input from the user. The AutoLISP functions entlast and entnext can be used to get an individual object without any input from the user. If you do want to allow the user to interactively select an individual object, you can use the entsel and nentsel functions.

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

### 0312. 任意卡——Controlling a Command's Version

Internally each standard AutoCAD command is assigned a new version number when a change is made that affects an AutoLISP program, script, or command macro. You use the initcommandversion function to control which version of a command is used by the next use of the command or command-s function. The initcommandversion function doesn't require a value, but when one is provided it must be an integer value that represents the version of the command you want to use.

The following example uses version 1 of the color command:

```c
(initcommandversion 1) 
(command "._color")
```

Version 1 of the color command displays options at the Command prompt; version 2 or later displays the Select Color dialog box instead. The -insert command is another command that is affected by the initcommandversion function. When using version 2 of the -insert command, the user can interact with the AutoCAD Properties palette in Windows while a preview of the block is being dragged in the drawing area.

1-2『真是巧了，昨天实现自动批量插入设备位号的时候才发现这个问题。当时是通过 `(setvar "ATTREQ" 1)` 实现插入块的时候交互输入属性值，插完后再将系统变量 ATTREQ 重置为 0。不过试验了下，改用 `(initcommandversion 2)` 实现了不了自动插入设备位号，目前原因不知。命令的版本号，做一张术语卡片。（2020-10-08）』——已完成

## Introduction

In 1996, Lee began learning the core concepts of customizing the AutoCAD user interface and AutoLISP. The introduction of VBA in AutoCAD R14 would once again redefine how Lee approached programming solutions for AutoCAD. VBA made it much easier to communicate with external databases and other applications that supported VBA. It transformed the way information could be moved between project management and manufacturing systems.

Not being content with VBA, in 1999 Lee attended his first Autodesk University and began to learn ObjectARX®. Autodesk University had a lasting impression on him. In 2001, he started helping as a lab assistant. He began presenting on customizing and programming AutoCAD at the event in 2004. Along the way he learned how to use the AutoCAD Managed.NET API.

Customization is one of the feature areas that sets AutoCAD apart from many other CAD programs. Even though the product can be used out of the box, configuring the user interface and modifying the support files that come with the product can greatly improve your productivity. By customizing AutoCAD, you can streamline product workflows and create new ones that are a better fit with the way your company works. These workflows might range from importing layers and styles into a drawing to the extraction of drawing-based information into a spreadsheet or database.

The AutoLISP programming language can be used to: Create custom functions that can be executed from the AutoCAD Command prompt; Create and manipulate graphical objects in a drawing, such as lines, circles, and arcs; Create and manipulate nongraphical objects in a drawing, such as layers, dimension styles, and named views; Perform mathematical and geometric calculations; Request input from or display messages to the user at the Command prompt; Interact with files and directories in the operating system; Read from and write to external files; Connect to applications that support ActiveX and COM; Display dialog boxes and get input from the end user.

AutoLISP code can be entered directly at the Command prompt or loaded using a LSP file. Once an AutoLISP program has been loaded, you can execute the custom functions from the Command prompt. Functions executed from the Command prompt can be similar to standard AutoCAD commands, but the programmer determines the prompts that should be displayed. It is also possible to use AutoLISP code with a command macro that is activated from the AutoCAD user interface or a tool on a tool palette.

1『 VBA 能实现的功能同上。』

VBA code statements are entered into the Visual Basic Editor and stored in a DVB file. Once a VBA project has been loaded, you can execute the macros through the Macros dialog box. Unlike standard AutoCAD commands, macros cannot be executed from the Command prompt, but once executed, a macro can prompt users for values at the Command prompt or with a user form. It is possible to execute a macro from a command macro that is activated with a command button displayed in the AutoCAD user interface or as a tool on a tool palette.

### Part I: AutoCAD Customization: Increasing Productivity through Personalization

Chapter 1: Establishing the Foundation for Drawing Standards In this chapter, you'll learn how to establish drawing standards. Drawing standards allow you to enforce consistency across multiple drawings. By enforcing a set of standards, you can easily share your drawings and make them look the same when plotting them.

Chapter 2: Working with Nongraphical Objects In this chapter, you'll learn how nongraphical objects affect display and output of objects in a drawing. Nongraphical objects such as layers and text styles make it easy to update the look of all the objects that reference them.

Chapter 3: Building the Real World One Block at a Time In this chapter, you'll learn how to create and manage blocks. Blocks allow you to logically create object groupings that can be used several times in the same drawing. For example, you could create a small assembly of parts and insert it more than once in a drawing. If the assembly changes, you just need to update the block and all instances of that block are changed.

Chapter 4: Manipulating the Drawing Environment In this chapter, you'll learn how to change the AutoCAD drawing environment. During start up, you can control several of the settings that affect the AutoCAD program. These settings can affect the display of the user interface, behavior of tools in the drawing environment, and where AutoCAD looks for support files.

Chapter 5: Customizing the AutoCAD User Interface for Windows In this chapter, you'll learn how to customize the elements and display of the AutoCAD user interface on Windows. The Customize User Interface (CUI) Editor allows you to create and manage the tools that are displayed by the AutoCAD user interface.

Chapter 6: Customizing the AutoCAD User Interface for Mac In this chapter, you'll learn how to customize the elements and display of the AutoCAD user interface on Mac OS. The Customize dialog box allows you to create and manage the tools displayed by the AutoCAD user interface.

Chapter 7: Creating Tools and Tool Palettes In this chapter, you'll learn how to create and customize tool palettes in AutoCAD on Windows. Tool palettes allow you to create a visual set of tools that can be used to insert blocks, start commands, or even hatch a closed area. Tool palettes are available on Windows only.

Chapter 8: Automating Repetitive Tasks In this chapter, you will learn how to create scripts and action macros to automate repetitive tasks. Script files and action macros allow you to combine multiple commands into simple logical sequences without needing to know a programming language. Action macros are supported on Windows only.

Chapter 9: Defining Shapes, Linetypes, and Hatch Patterns In this chapter, you will learn how to create custom shapes, linetypes, and hatch patterns that you can use to control the way line work appears in a drawing. The AutoCAD install provides a limited number of standard shapes, linetypes, and hatch patterns. You can extend the standard definitions by creating your own shapes, linetypes, and hatch patterns for use in your drawings.

Chapter 10: Using, Loading, and Managing Custom Files In this chapter, you will learn how to use, manage, and migrate custom files. After you have spent the time customizing AutoCAD, all you have left to do is deploy and manage your files.

### Part II: AutoLISP: Productivity through Programming

Chapter 11: Quick Start for New AutoLISP Programmers In this chapter, you'll get an introduction to the AutoLISP programming language. I begin by showing you how to enter AutoLISP expressions at the Command prompt and execute standard AutoCAD commands. After that, you are eased into some basic programming concepts that allow you to perform conditional tests and repeat expressions. The chapter wraps up with creating and loading an AutoLISP file into the AutoCAD program.

Chapter 12: Understanding AutoLISP In this chapter, you'll learn the fundamentals of the AutoLISP programming language. AutoLISP fundamentals include a look at the syntax and structure of an expression, how to use a function, and how to work with variables. Beyond just syntax and variables, you learn to use AutoCAD commands and group multiple AutoLISP expressions into custom functions.

Chapter 13: Calculating and Working with Values In this chapter, you'll learn to work with mathematical and string manipulation functions. Math functions allow you to perform basic and advanced calculations based on object values or a value that the user might provide, whereas string manipulation functions allow you to work with text-based values. Both numeric and textual values are used when creating or manipulating objects, adding annotations to a drawing, or displaying a message to the end user. Based on how the values are used, numeric values can be converted to strings and strings can be converted to numeric values.

Chapter 14: Working with Lists In this chapter, you'll learn to work with the list data type. Lists are used throughout AutoLISP to provide 2D or 3D coordinate values or to define an object stored in a drawing.

Chapter 15: Requesting Input, and Using Conditional and Looping Expressions In this chapter, you'll learn to request input from the user, use conditional statements, and repeat expressions. Requesting input allows you to get values from the user and then use those values to determine the end result of the program. Conditional statements enable a program to make choices based on known conditions in a drawing or input from a user. After you understand conditional statements, you will learn to use them in conjunction with looping expressions to execute a set of expressions until a condition is met.

Chapter 16: Creating and Modifying Graphical Objects In this chapter, you'll learn how to create, modify, and attach extended data to graphical objects using AutoCAD commands and AutoLISP functions. Graphical objects represent the drawing objects, such as a line, an arc, or a circle, that are displayed in model space or on a named layout. When modifying objects, you can choose to step through all the objects in a drawing or let the user select the objects to be modified. Extended data allows you to store information with an object that can be used to identify the objects your program creates or link objects to external database records.

Chapter 17: Creating and Modifying Nongraphical Objects In this chapter, you'll learn how to create and modify nongraphical objects using AutoCAD commands and AutoLISP functions. Nongraphical objects are used to control the appearance of graphical objects and store settings that affect the behavior of features in the AutoCAD program. Drawings support two different types of nongraphical objects: symbol table objects and dictionaries.

Chapter 18: Working with the Operating System and External Files In this chapter, you will learn how to work with settings and files stored outside of the AutoCAD program. Settings can be stored in the Windows Registry and Plist files on Mac OS, and they can be used to affect the behavior of the AutoCAD program or persist values for your custom programs between AutoCAD sessions. Files and folders stored in the operating system can be accessed and manipulated from the AutoCAD program, which allows you to set up project folders or populate project information in the title block of a drawing from an external file.

2『 16 和18 章里应该有，将数据导出的相关信息。结果发现 17 章里也有这方面的信息。最终竟然在第 3 章里找到解决办法，直接用命令 dataextraction 就可以提取块里面的属性信息，以 csv 或 txt 格式导出来。』

Chapter 19: Catching and Handling Errors In this chapter, you will learn how to catch and handle errors that are caused by an AutoLISP function and keep an AutoLISP program from terminating early. AutoLISP provides functions that allow you to trace a function, see arguments as they are passed, catch an error and determine how it should be handled, and group functions together so all the actions performed can be rolled back as a single operation.

Chapter 20: Authoring, Managing, and Loading AutoLISP Programs In this chapter, you will learn how to store AutoLISP code statements in a file, load and manage AutoLISP files, and deploy custom programs with plug-in bundles. Storing AutoLISP code in a file allows for its reuse in multiple drawings. When you load an AutoLISP file, all of the functions defined in the file are made available while the drawing remains open. Based on how you load or deploy an AutoLISP file, you might need to let the AutoCAD program know where your AutoLISP files are stored.

Chapter 21: Using the Visual LISP Editor (Windows only) In this chapter, you will learn how to use the Visual LISP® Editor. The editor provides tools for writing, formatting, validating, and debugging code in an AutoLISP file. Using the Visual LISP Editor, you can group AutoLISP files into project files, which make them easy to manage and compile. Compiling an AutoLISP file secures the source code contained in the file so that it can't be altered by others.

Chapter 22: Working with ActiveX/COM Libraries (Windows only) In this chapter, you will learn how to use ActiveX/COM libraries with AutoLISP. ActiveX provides access to additional functions, which allow for the creation and manipulation of drawing objects and AutoCAD application settings that aren't easily accessible with standard AutoLISP functions. External applications, such as Microsoft Word and Excel, can also be accessed from the AutoCAD program when using ActiveX.

Chapter 23: Implementing Dialog Boxes (Windows only) In this chapter, you will learn how to create and use dialog boxes with an AutoLISP program. Dialog boxes provide an alternative method of requesting input from the user and are implemented using Dialog Control Language (DCL).

### Part III: AutoCAD VBA: Programming with VBA and ActiveX (Windows only)

Chapter 24: Understanding the AutoCAD VBA Environment In this chapter, you'll get an introduction to the Visual Basic Editor. I begin by showing you how to verify whether the VBA environment for AutoCAD has been installed and, if not, how to install it. After that, you are eased into navigating the Visual Basic Editor and managing VBA programs. The chapter wraps up with learning how to execute macros and access the help documentation.

Chapter 25: Understanding Visual Basic for Applications In this chapter, you'll learn the fundamentals of the VBA programming language and how to work with objects. VBA fundamentals include a look at the syntax and structure of a statement, how to use a function, and how to work with variables. Beyond syntax and variables, you learn to group multiple statements into custom procedure.

Chapter 26: Interacting with the Application and Documents Objects In this chapter, you'll learn to work with the AutoCAD application and manage documents. Many of the tasks you perform with an AutoCAD VBA program require you to work with either the application or a document. For example, you can get the objects in a drawing and even access end-user preferences. Although you typically work with the current document, VBA allows you to work with all open documents and create new documents. From the current document, you can execute commands and work with system variables from within a VBA program, which allows you to leverage and apply your knowledge of working with commands and system variables.

Chapter 27: Creating and Modifying Drawing Objects In this chapter, you'll learn to create and modify graphical objects in model space with VBA. Graphical objects represent the drawing objects, such as a line, an arc, or a circle. The methods and properties of an object are used to modify and obtain information about the object. When working with the objects in a drawing, you can get a single object or step through all objects in a drawing.

Chapter 28: Interacting with the User and Controlling the Current View In this chapter, you'll learn to request input from an end-user and manipulate the current view of a drawing. Based on the values provided by the end-user, you can then determine the end result of the program. You can evaluate the objects created or consider how a drawing will be output, and use that information to create named views and adjust the current view in which objects are displayed.

Chapter 29: Annotating Objects In this chapter, you'll learn how to create and modify annotation objects. Typically, annotation objects are not part of the final product that is built or manufactured based on the design in the drawing. Rather, annotation objects are used to communicate the features and measurements of a design. Annotation can be a single line of text that is used as a callout for a leader, a dimension that indicates the distance between two drill holes, or a table that contains quantities and information about the windows and doors in a design.

Chapter 30: Working with Blocks and External References In this chapter, you'll learn how to create, modify, and manage block definitions. Model space in a drawing is a special named block definition, so working with block definitions will feel familiar. Once you create a block definition, you will learn how to insert a block reference and work with attributes along with dynamic properties. You complete the chapter by learning how to work with externally referenced files.

Chapter 31: Outputting Drawings In this chapter, you will learn how to output the graphical objects in model space or on a named layout to a printer, plotter, or electronic file. Named layouts will be used to organize graphical objects for output, including title blocks, annotation, floating viewports, and many others. Floating viewports will be used to control the display of objects from model space on a layout at a specific scale. After you define and configure a layout, you learn to plot and preview a layout. The chapter wraps up with learning how to export and import file formats.

Chapter 32: Storing and Retrieving Custom Data In this chapter, you will learn how to store custom information in a drawing or in the Windows Registry. Using extended data (Xdata), you will be able to store information that can be used to identify a graphical object created by your program or define a link to a record in an external database. In addition to attaching information to an object, you can store data in a custom dictionary that isn't attached to a specific graphical object in a drawing. Both Xdata and custom dictionaries can be helpful in making information available between drawing sessions; the Windows Registry can persist data between sessions.

Chapter 33: Modifying the Application and Working with Events In this chapter, you will learn how to customize and manipulate the AutoCAD user interface. You also learn how to load and access externally defined custom programs and work with events. Events allow you to respond to an action that is performed by the end-user or the AutoCAD application. There are three main types of events that you can respond to: application, document, and object.

Chapter 34: Creating and Displaying User Forms In this chapter, you will learn how to create and display user forms. User forms provide a more visual approach to requesting input from the user.

Chapter 35: Communicating with Other Applications In this chapter, you will learn how to work with libraries provided by other applications. These libraries can be used to access features of the Windows operating system, read and write content in an external text or XML file, and even work with the applications that make up Microsoft Office.

1『这章涉及与其他 app 的交互，那么有提取 cad 数据直接进服务器的实现线索。（2020-06-25）』

Chapter 36: Handling Errors and Deploying VBA Projects In this chapter, you will learn how to catch and handle errors that are caused by the incorrect use of a function or the improper handling of a value that is returned by a function. The Visual Basic Editor provides tools that allow you to debug code statements, evaluate values assigned to user-defined variables, identify where within a program an error has occurred, and determine how errors should be handled. The chapter wraps everything up with learning how to deploy a VBA project on other workstations for use by individuals at your company.

Bonus Chapter 1: Working with 2D Objects and Object Properties In this chapter, you build on the concepts covered in Chapter 27,「Creating and Modifying Drawing Objects.」You will learn to create additional types of 2D objects and use advanced methods of modifying objects, you also learn to work with complex 2D objects, such as regions and hatch fills. The management of layers and linetypes and the control of the appearance of objects are also covered.

Bonus Chapter 2: Modeling in 3D Space In this chapter, you learn to work with objects in 3D space, and 3D objects. 3D objects can be used to create a model of a drawing which can be used to help visualize a design or detect potential design problems. 3D objects can be viewed from different angles and used to generate 2D views of a model that can be used to create assembly directions or shop drawings.

Bonus Chapter 3: Development Resources In this chapter, you discover resources that can help expand the skills you develop from this book or locate an answer to a problem you might encounter. I cover development resources, places you might be able to obtain instructor-led training, and interact with fellow users on extending AutoCAD. The online resources sites listed cover general customization, AutoLISP, and VBA programming in AutoCAD.

## 0101. Establishing the Foundation for Drawing Standards

Well-established drawing standards ensure that your drawings all look the same when they are presented to the client, and they can make it easier to: Train new drafters and other professionals on your company's standards that use AutoCAD; Identify which drawing and externally referenced files are associated with a project; Determine the purpose of a named object in a drawing; Share project files with clients and contractors because your standards are well defined.

## 0103. Building the Real World One Block at a Time

定义块、修改块；提取块内的数据信息。

3『

在 18 章看到这么一段话。然后在 17 章里找到一小节「Creating the Room Label Block Definition」。

In Chapter 17, you created a set of functions that allowed you to extract the attributes of a block and then quantify the results before creating the BOM in the drawing. Here, you will create a function named furnbomexport that allows you to export the BOM data generated with the extAttsFurnBOM function output to an external file instead of adding it to the drawing as a table grid as you did with the furnbom function.

』

Instead of dedicating time to re-create the geometry each time, you can create the objects once and store them as a block definition. Block definitions are another type of nongraphical object that can be in a drawing, much like text and dimension styles.

3『[AutoCAD 2019 帮助: 关于定义块](http://help.autodesk.com/view/ACD/2019/CHS/?guid=GUID-F81D7F1E-1F0A-45AD-AC7E-891A85A0033A)』

In addition to geometric objects, block definitions can contain attribute definitions, which allow you to embed information into a block. The information stored in attributes can be extracted to an external file or added to a table in a drawing.

Block definitions must be defined in a drawing before you can create (or, as commonly known, insert) a block reference. A block reference object specifies where and how the objects from a block definition should be drawn onscreen or plotted. You typically create block definitions by first adding the geometry for your block in model space and then using the block command to define which objects will make up the block definition. AutoCAD also offers a special environment called the Block Editor (bedit command) for working with block definitions. Once a block definition is defined, you can use the insert command to create a block reference of a block definition. when defining a block you must consider the following:

1. Name . The name of a block definition is used to differentiate one from another; each block definition in a drawing must have a unique name. Drawings can easily contain hundreds and even thousands of block definitions. When naming block definitions, use descriptive names, but don't make them so long that the user must carefully read a sentence-long name. I discussed naming blocks and other nongraphical objects in Chapter 2,「Working with Nongraphical Objects.」

2. Base (or Insertion) . Point The base point for a block definition is similar to a drawing's origin. This point is used as a block reference's insertion point, the same point that is used to drag a preview of the block onscreen with the insert command. You typically specify the base point of a block on one of the objects in the block definition, such as an endpoint or intersection of two objects.

3. Objects. The objects that make up the block definition determine how the block references inserted into a drawing will look and behave. Objects within a drawing include geometry objects such as lines, circles, arcs, and even other blocks. Blocks can also include special objects known as attribute definitions, which allow you to add to a block information such as a project name or part number. I discuss attributes in the section「Embedding Information in a Block Definition with Attributes」later in this chapter.

Block definitions can contain attributes that allow you to add custom information to a block reference when it is inserted into a drawing. Using attributes allows you to use a single block definition but represent several items that might be the same size and a different color or style. A common use for attributes is to store project, date, and revision information in a title block, or a model number and description with a window or bolt block. After you insert a block reference with attributes, you can extract the values stored in the attributes to an external file or table object.

There are two types of attributes in a drawing. Those in a block definition are known as attribute definitions. The other type of attribute is known as an attribute reference, which can be found attached to a block reference that has been inserted into a drawing whose block definition contains attribute definitions.

1『两类属性，attribute definitions 和 attribute reference。』

You can create attribute definitions by using the Attribute Definition dialog box (attdef command). You can add an attribute definition to model space or paper space before you define your block definition by using the Block Definition (Windows) or Define Block (Mac OS) dialog box (block command), or after a block definition is created in the Block Editor (bedit command). The following steps explain how to add an attribute definition, whether you are working in the drawing window or the Block Editor:

Invisible: The attribute is invisible when a block reference is inserted into the drawing. All invisible attributes can be displayed by setting the attmode system variable to a value of 2;  Constant: The text string entered in the Value text box of the attribute is fixed and is the same for all block references that are inserted based on the block definition that contains this type of attribute;  Verify: You are prompted to verify the value of the attribute when the block reference is inserted.

Preset: The Default value is assigned to the attribute when the block reference is inserted, and you are not prompted to change the value. You can change the value using the attedit or eattedit command or the Properties palette (Windows) or Properties Inspector (Mac OS); Lock Position: Restricts the attribute from being moved using grips. This mode is helpful if you want to control the placement of an attribute with parameters and actions in a dynamic block.

NOTE: While AutoCAD remains open, the Mode options you choose are stored as a sum of different bitcode values in the aflags system variable. The value of aflags is used as the default option for the next attribute definition you create.

NOTE: When you are selecting objects to define a block definition, the order in which you select your attribute definitions affects how AutoCAD prompts for each attribute value. I recommend selecting all your graphical objects first, and then selecting each attribute definition in the order you want its value to be prompted for. Prompting order can have an impact on your block's usage with scripts, menu macros, and other custom programs. You can also change the prompting order of the attributes in a block by using the Block Attribute Manager (battman command).

1『这点很重要，定义块的时候，选择顺序先选图形元素，然后再选属性。作者的意思这对后面使用 autolisp 有好处。』

Just as it is not uncommon to make changes to the way a block looks over time, you might decide to update the attribute definitions in a block definition. There are a few things you need to consider when adding, modifying, or removing attribute definitions from a block definition. Although it is true that the geometry of a block definition is the same for each and every block reference that uses a specific block definition, the same is not true for attribute definitions and references unless all your attribute definitions are defined as Constant.

Some blocks based on the same block definition may not have all the attributes defined in that block definition. This situation often occurs when attributes in a block definition are updated but the block references themselves are not synchronized to include the same changes, or when a custom application has decided not to add an attribute reference to a block reference for some reason.

After you update the attributes of a block definition, you want to run the attredef or attsync command or use the Block Attribute Manager (battman command). These utilities synchronize the attribute definitions in a block definition with the attribute references in each of the block references that have been inserted in a drawing by adding and removing attributes as needed. Those attributes in the block reference that are contained in the block definition are not changed; their current values are retained.

The Block Attribute Manager (battman command) can also be helpful in updating the properties and prompting order of the attribute definitions in a block definition, as well as editing and removing attribute definitions. These three commands can also affect any formatting or property changes made to attributes in a block reference with the attedit and eattedit commands. If you need to just change the prompting order of the attributes within a block definition, you can use the battorder command while the block definition is open in the Block Editor (bedit command).

1『修改块属性可以用命令 attredef 或者 attsync。』

Using Fields with Attributes. Fields allow you to place information in your drawing based on a graphical or nongraphical drawing object, the current value of a system variable, a property of a sheet set or project, the current date or the date when the current drawing was created, and much more. Fields can be used to construct the string value of a single-line or multiline text object, which can be a standalone object or in another object such as a table or dimension. In addition to text objects, attributes can use fields to define the value that they hold. Use the following steps to define an attribute definition with a field:

2『 Fields 感觉是在定义属性时看到的「字段」，待确认。』

When you insert a block reference with an attribute, you can specify a field value in the Edit Attributes dialog box by right-clicking in the text box to the right of the attribute prompt and clicking Insert Field. You can edit an existing field by double-clicking the shaded text in the text box, or you can convert it to static text by selecting and right-clicking the shaded text that represents the field and clicking Convert Field To Text.

BlockPlaceholder Field Type. In AutoCAD on Windows while the Block Editor is active, you have access to an additional field type: BlockPlaceholder. The BlockPlaceholder field type allows you to access the properties of the block reference when it is placed in a drawing. For example, you could list the name of the block as part of a description in an attribute field or even access the current value of one of the parameters used for a custom dynamic property.

Dynamic properties when added to a block definition allow you to rotate, move, stretch, and perform other actions on the objects within a block reference. A block definition that contains dynamic properties is known as a dynamic block. Parameters and actions are used to implement dynamic properties. You can only add dynamic properties to a block definition using the Block Editor in AutoCAD on Windows. Although you can't create or modify dynamic properties in AutoCAD for Mac OS, you can insert blocks that have these properties already implemented.

When a block with dynamic properties is inserted into a drawing, additional grips are displayed for the block reference when it is selected. These additional grips allow you to interactively change the values of the custom actions rather than selecting values from a predefined list. Figure 3.7 shows a block reference selected in the drawing and a linear distance being modified with grips.

One of the benefits of using attributes with your blocks is that you can extract the information and then use it in your drawing or an external program. If all of your blocks contain attributes, you could generate a bill of materials on demand or even help prepare an estimate for a project. The attribute values and the properties of the blocks containing attributes can be extracted from a drawing using the Attribute Extraction dialog box (attext command) or Data Extraction Wizard (attext command) (in AutoCAD on Windows only) or by using the -attext command at the command prompt in AutoCAD both on Windows and Mac OS. The following steps explain how to extract the attributes from a drawing using the Data Extraction Wizard in AutoCAD on Windows:

1『 dataextraction 命令可以提取实体对象里的各个数据，可以筛选出块的属性信息，可以导出成 csv、txt 等格式。可以说这个命令可以满足我想要做数据分析所需的数据源了，哈哈；用命令 -attext 可以直接提取属性信息，但需要一个模板，没有 dataextraction 方便。』

NOTE: After you place a table using the Data Extraction Wizard, a Data Link icon that looks like two chain links appears in the application's status-bar tray. Right-click the icon or the table in the drawing, and click Update All Data Links to ensure the information displayed in the table is up to date.