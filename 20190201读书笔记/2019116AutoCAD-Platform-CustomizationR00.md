# 2019116AutoCAD-Platform-CustomizationR00

## 记忆时间

## 资源汇总

[HyperPics: Resources for the AutoCAD and AutoCAD LT Programs](http://www.hyperpics.com/)

## 卡片

### 0101. 主题卡 —— 封装判断数据类型的函数

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

1-2『完全可以自己做一些判断数据类型的函数，封装起来自己用，真切的感觉到，一切语法即为语法糖。封装判断数据类型的函数，做一张主题卡片。』—— 已完成

### 0102. 主题卡 —— 如何获取用 entmake 函数新建一个实体对象所需的参数

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

做一张主题卡片。』—— 已完成

### 0103. 主题卡 —— 修改实体数据的 2 种方法

AutoLISP offers two different methods for modifying the properties of an object directly. The easier of the two methods is to use the object property functions that were introduced with AutoCAD 2012. These functions require less code than the legacy approach of getting and manipulating the entity data list of an object. The property-related functions are less cryptic than entity data list manipulation as well, because you don't need to understand the various DXF group codes associated with a specific object. The downside to these functions is that they work only with AutoCAD 2012 and later, so if you need to support an earlier release you will need to manipulate entity data lists (which I cover in the next section).

Table 16.6 lists the AutoLISP functions available in AutoCAD 2012 and later that can be used to list, get, and set the properties of an object.

|  Function | Description  |
|---|---|
|  dumpallproperties |  Returns all of the properties for the specified object |
|  getpropertyvalue |  Returns the current value of an object's property |
|  setpropertyvalue |  Assigns a value to an object's property |
|  ispropertyreadonly |  Returns T or nil based on whether an object property is read-only |

1-2『看到这里才知道，之前一直用的传统方法：通过实体名称结合 `entget` 函数获取实体的「数据集」，通过替换数据集里的「点对」来实现修改属性。原来还有第二种方法，直接用 autolisp 封装好的函数，前提是只支持 AutoCAD 2012 以后的，可以接受。修改实体数据的 2 种方法，做一张主题卡片。』—— 已完成

### 0104. 主题卡 —— 获取并修改实体对象上的 XData

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

### 0105. 主题卡 —— 定位放大到一个特点的实体对象的坐标位置上

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

In AutoLISP you can define a special function named `s::startup`. This function is executed when you create or open a drawing in AutoCAD, as long as it has been defined in a loaded LSP file. Although more than one LSP file can contain an `s::startup` function, only the last loaded definition of the function is retained. The `s::startup` function is typically used to initialize system variables, insert title blocks, or draw and modify objects in the current drawing upon opening.

Here is an example of the `s::startup` function:

```c
(defun s::startup ( / old_attreq) 
  (setvar "osmode" 39) ; END, MID, CEN, and INT 
  (setvar "pickfirst" 1) 
  ; Create layer for title block 
  (command "._-layer" "_m" "titleblk" "_c" "7" "" "") 
  ; Insert title block at 0,0 
  (setq old_attreq (getvar "attreq")) 
  (setvar "attreq" 0) 
  (command "._insert" "tb-c_size" "0,0" "1" "1" "0") 
  (setvar "attreq" old_attreq) 
  ; zoom to extents 
  (command "._zoom" "_e")
)
```

1-2『

这里绝逼意外的挖了一个大宝藏：定位放大到一个特点的实体对象的坐标位置上。做一张主题卡片。（2021-03-02）

```c
(defun c:foo (/ ss) 
  (setq ss (ssget))
  (command "._zoom" "_o" ss "")
)
```

用原生命名 `._zoom` 实现的，借用选项对象（o），感觉选项窗口也可以实现。这个功能实现后，那么数据流里的任何数据，我都可以通过通配符去搜索匹配，然后放大定位到匹配到的实体对象上去。

另外的知识点：

1、系统变量 `osmode`，即「草图设置」里的对象捕捉设置值。

[Tutorial: Creating a New Custom Command and Controlling with System Variables (AutoLISP)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-1330DB99-DDFA-44D0-BDEB-676FF619EBE5)

Accessing and Setting System Variable Values

System variables control the behavior of commands, change the settings of the drawing environment, and specify the default property values of new objects and much more. You can query and set the value for a system variable using the following functions:

getvar - Returns the current value of a system variable.

setvar - Assigns a new value to a system variable.

The following explain how to get and set the value of the OSMODE (Object Snap mode) system variable:

1 At the Command prompt, enter:

```
(setq cur_osmode (getvar "osmode"))
```

The current value of the OSMODE system variable is returned and assigned to the user-defined variable of `cur_osmode`. While OSMODE returns an integer value, the value is the sum of multiple "bit-code" values. For example, the value 35 indicates that the Endpoint (1), Midpoint (2), and Intersection (32) running object snaps are enabled.

2 At the Command prompt, enter: osnap.

The Drafting Settings dialog box is displayed with the Object Snap tab current. This tab allows you to see which object snaps are enabled. The following image shows what the Drafting Settings dialog box looks like when the OSMODE system variable is set to a value of 35.

3 In the Drafting Settings dialog box, change which object snaps are current and click OK.

4 At the Command prompt, enter: 

```c
(getvar "osmode")
```

The current value of the OSMODE system variable is returned.

5 At the Command prompt, enter:

```c
(setvar "osmode" cur_osmode)
```

The value of the OSMODE system variable is restored to the value that was previously assigned to the user-defined variable `cur_osmode`.

6 Display the Drafting Settings dialog box again. You should see that the object snap settings have been restored.

Note: Before you make a change to the drawing environment, it is good practice to store the values of any system variables, and then restore them before your program ends.

2、修改系统环境变量值养成修改回原值的习惯。前面的备注（note）讲的就是这点，包括本书作者前面的例子里，有关「块」的系统变量 `attreq` 后面也改回去了。这个系统变量值以前用到过，插入块的命令是，如果改值为 0，就不会一个一个提示属性值。

』

### 0106. 主题卡 —— Defining a Plug-in Bundle

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

1-2『重点来了，实现付费的方法，意外收获，没想到在这里看到相关信息。插件式捆绑，做一张主题卡片。（2021-03-05）』—— 已完成

A plug-in bundle, as I previously mentioned, is one of the methods that can be used to deploy your LSP files. Fundamentally, a bundle is simply a folder structure with its topmost folder having `.bundle` appended to its name and a manifest file with the filename PackageContents.xml located in the topmost folder. You can use Windows Explorer or File Explorer on Windows, or Finder on Mac OS, to define and name the folder structure of a bundle. The PackageContents.xml file can be created with a plain ASCII text editor, such as Notepad on Windows or TextEdit on Mac OS.

The following is an example PackageContents.xml file that defines the contents of a bundle named DrawPlate.bundle that contains three files: a help file named DrawPlate.htm, and two LSP files named DrawPlate.lsp and Utility.lsp:

```
<?xml version="1.0" encoding="utf-8"?><!DOCTYPE component PUBLIC "-//JWS//DTD WileyML 20110801 Vers 3Gv2.0//EN" "Wileyml3gv20-flat.dtd">
  <Components Description="All OSs"> 
    <RuntimeRequirements OS="Win32|Win64|Mac" SeriesMin="R19.0" Platform="AutoCAD*" SupportPath="./Contents/" /> 
    <ComponentEntry Description="Main LSP file" AppName="DrawPlateMain" Version="1.0" ModuleName="./Contents/DrawPlate.lsp"> </ComponentEntry> 
    <ComponentEntry Description="Utility LSP file" AppName="UtilityFunctions" Version="1.0" ModuleName="./Contents/Utility.lsp"> </ComponentEntry> 
  </Components> 
</ApplicationPackage>
```

The folder structure of the bundle that the PackageContents.xml file refers to looks like this:

```
DrawPlate.bundle 
  PackageContents.xml 
  Contents 
    DrawPlate.lsp 
    DrawPlate.htm 
    Utility.lsp
```

I have provided the DrawPlate.bundle as part of the sample files for this book, but you will also learn how to create the DrawPlate.bundle yourself later in this chapter. To use the bundle with AutoCAD, copy the DrawPlate.bundle folder and all of its contents to one of the following locations so that all users can access the files:

```
%ALLUSERSPROFILE%\Application Data\Autodesk\ApplicationPlugIns (Windows XP)

%ALLUSERSPROFILE%\Autodesk\ApplicationPlugIns (Windows 7 or Windows 8)

/Applications/Autodesk/ApplicationAddIns (Mac OS)
```

If you want a bundle to be accessible only by a specific user, place that bundle into one of the following locations under that user's profile:

```
%APPDATA%\Autodesk\ApplicationPlugIns (Windows)

˜/Autodesk/ApplicationAddIns (Mac OS)
```

For additional information on the elements used to define a PackageContents.xml file, perform a search in the AutoCAD Help system on the keyword「PackageContents.xml.」

NOTE: The appautoload system variable controls when bundles are loaded into AutoCAD. By default, bundles are loaded at startup, when a new drawing is opened, and when a plug-in is added to the ApplicationPlugins or ApplicationAddIns folder. You can use the appautoloader command to list which bundles are loaded or reload all the bundles that are available to AutoCAD.

### 0107. 主题卡 —— 函数收藏

详见「2019116AutoCAD-Platform-CustomizationR01.md」。

### 0108. 主题卡 —— 常用 DXF 码

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

1、图层状态。

For example, the layer status property (DXF group code 70) of a layer is a bit-coded value that contains various flags used to specify whether the layer is frozen (1 bit), locked (4 bit), or dependent on an xref (16 bit). The osmode system variable is another example of a bit-coded value in AutoCAD. In the osmode system variable, the value indicates which running object snaps are currently enabled. Refer to the AutoCAD Help system to determine whether an object property or system variable is an integer or bit-coded value.

1『这里意外获取到，图层锁定状态的 DXF 码，哈哈。收入进主题卡片「常用 DXF 码」。（2021-03-06）』

### 0109. 主题卡 —— entity name 跟 vla-object 相互转换

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

The graphical and nongraphical objects stored in a drawing can be accessed using ActiveX. As defined by the drawing architecture, all graphical objects are stored in a Block object and can be accessed from the Blocks collection. Model space and paper space are special types of Block objects that you can manipulate without performing any special operation. The Blocks collection is just one of several collections that allow you to create and access nongraphical objects in a drawing.

NOTE 22.5: The vla-object data type isn't compatible with the ename data type. You can convert vla-object values to an entity name (ename) by using the `vlax-vla-object->ename` function. The `vlax-ename->vla-object` function converts an ename to a vla-object data type. Additionally, you can use the `vla-get-handle` function to get an object's handle and then use the handent function to get an object's ename based on a valid handle. These functions are helpful if you are mixing the use of Classic AutoLISP functions that work with the ename data type, such as entget or ssname, and those used to work with objects of the AutoCAD COM library. Examples of these functions, with the exception of `vlax-vla-object->ename`, can be found in the `ch22_mswin_office.lsp` file, which you can download from this book's web page, www.sybex.com/go/autocadcustomization.

1-2『大赞，entity name 跟 vla-object 之间可以相互转换，那么基本把之前学的操作 entity data 的知识可以直接跟现在操作 vla-object 打通掉。试场景自己选用哪条路径操作 CAD 里的数据。做一张主题卡片。（2021-03-07）』—— 已完成

In the previous section, you learned how to get the object that represents the active document. The next example shows how to get the ModelSpace or PaperSpace object based on the active space. You can determine the correct active space by using the ActiveSpace property of the current document.

```c
; Get a reference to the current space in AutoCAD 
(if (= (vla-get-activespace curDoc) acModelSpace) 
  (setq space (vla-get-modelspace curDoc)) 
  (setq space (vla-get-paperspace curDoc)) 
)
```

1『上面的方法可以判断，打开的图纸是在模型空间里还是布局空间里，常规都是模型空间里，此判断可以忽略。（2021-03-07）』

When you want to add an object, such as a Layer object, to a collection, you can use one of the many Add methods available through the AutoCAD COM library. The following exercise shows how to create a function that checks for the existence of a layer and that creates the layer if it's not found; it then sets the layer as current by using the AutoCAD COM library and ActiveX. The function is similar to the createlayer function that you defined in the utility.lsp file in the various exercises throughout this book.

### 0201. 术语卡 —— Dotted Pair

Dotted Pair. A dotted pair is a list of two values separated by a period. Dotted pairs are commonly used to represent property values for an object. The first value of a dotted pair is sometimes referred to as a DXF group code. For example, `(40 . 2.0)` represents the radius of a circle; DXF group code value 40 indicates the radius property, and 2.0 is the actual radius value for the circle. When you're assigning a dotted pair to a variable, either the pair must be preceded by an apostrophe, as in `(setq dxf_40 '(40 . 2))`, or you must use the AutoLISP cons function, as in `(setq dxf_40 (cons 40 2))`. You'll learn more about creating and manipulating dotted pairs in Chapter 16.

2『 Dotted Pair 做一张术语卡片。』—— 已完成

### 0202. 术语卡 —— XData

Each object in a drawing has a pre-established set of properties that define how that object should appear or behave. These properties are used to define the size of a circle or the location of a line within a drawing. Although you can't add a new property to an object with AutoLISP, you can append custom information to an object. The custom information that you can append to an object is known as extended data, or XData.

XData is structured similar to an entity data list except the values must be within a specific range of DXF group codes. Each XData list must contain an application name to identify one XData list from another since several XData lists can be attached to an object. After the application name, an XData list can contain any valid values and be of any type of data that AutoLISP supports.

The values in an XData list and what they represent is up to you, the creator of the data. Data in an XData list can be used to identify where an object should be placed or which layer it should be on, to store information about an external database record that is related to an object, or to build relationships between objects in a drawing. The way data is used or enforced is up to you as the programmer.

In addition to XData, graphical and nongraphical objects support what are known as extension dictionaries. Extension dictionaries are kind of like record tables that can be attached to an object. For example, you could store revision history of a drawing in an extension dictionary that is attached to model space, and then populate that information in the drawing's title block. I discuss creating custom dictionaries in Chapter 17.

2『 XData 做一张术语卡片。』—— 已完成

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

### 0203. 术语卡 —— 图形数据和非图形数据

The AutoLISP® programming language is great for creating and modifying objects. There are two types of objects that you can create or modify: graphical and nongraphical. Graphical objects are those that you can see and interact with in the drawing area, whether in model or paper space. Nongraphical objects are those that you don't create in the drawing area but that can affect the appearance of graphical objects. I discuss working with nongraphical objects in Chapter 17,「Creating and Modifying Nongraphical Objects.」

2『图形数据和非图形数据，做一张术语卡片。』—— 已完成

### 0204. 术语卡 —— Block Definitions and Block References

Block references are often misunderstood by new (and even experienced) AutoLISP developers. Blocks are implemented as two separate objects: block definitions and block references. Block definitions are nongraphical objects that are stored in a drawing and contain the geometry and attribute definitions that make up how the block should appear and behave in the drawing area. A block definition can also contain custom properties and dynamic properties.

Understanding Block Definitions and Block References. You can think of a block definition much like a cookie recipe. The recipe lists the ingredients that make up the cookie and explains how those ingredients are combined for a particular taste, but it doesn't control where the dough will be placed on the baking sheet or the size of the unbaked cookies. The placement and amount of the cookie dough on the sheet would be similar to a block reference in a drawing.

A block reference displays an instance, not a copy, of the geometry from a block definition; the geometry exists only as part of the block definition, with the exception of attributes. Attribute definitions that are part of a block definition are added to a block reference as attributes unless the attribute definition is defined as a constant attribute. Constant attributes are parts of the geometry inherited from a block definition and aren't part of the block reference.

1-3『块定义和块参照，对应于面向对象的类和对象，块参照是块定义的实例化。（2021-03-10）』

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

1『目前无法生成完整的块实体，生成的块只有参照没属性值。用 `entmake` 结合 `ATTRIB` 无效。（2020-10-30）补充：首先，用这种途径已经实现了生成块数据。其次，看到上面的信息后，对块定义和块参照、属性定义和属性参照的认识更深了。属性定义在 entity data 里对应于 attdef，属性参照在 entity data 里对应于 atttib。（2021-03-10）』

### 0205. 术语卡 —— 选择集

A selection set, sometimes known as a selection set name or ssname for short, is a temporary container that holds a reference to objects in a drawing. AutoLISP represents a selection set with the PICKFIRST data type. You get a selection set, commonly based on the objects in a drawing that the user wants to modify or interact with. For example, when you see the Select objects: prompt AutoCAD is asking you to select the objects in the drawing you want to work with and it gets a selection set containing the objects you selected in return.

In addition to getting a selection set based on user input, you can create a selection set manually and add objects to it. You might want to create a function that steps through a drawing and locates all the objects on a specific layer, and then returns a selection set that the next function can work with. Once a selection set is created, you can add additional objects or remove objects that don't meet the requirements you want to work with. A selection set makes it efficient to query and modify a large number of objects.

2『选择集的概念做一张术语卡片。』—— 已完成

### 0206. 术语卡 —— bit-coded values

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

Integer values can be used to represent what is known as a bit pattern or bit-coded value. A bit-coded value is the sum of one or more bits. A bit is a binary value; when one or more bits are combined they create a unique sum. AutoCAD uses bit-coded values for many different object properties (DXF group codes) and system variables.

2『这里的 bit-coded values 做一张术语卡片。（2021-03-06）』—— 已完成

For example, the layer status property (DXF group code 70) of a layer is a bit-coded value that contains various flags used to specify whether the layer is frozen (1 bit), locked (4 bit), or dependent on an xref (16 bit). The osmode system variable is another example of a bit-coded value in AutoCAD. In the osmode system variable, the value indicates which running object snaps are currently enabled. Refer to the AutoCAD Help system to determine whether an object property or system variable is an integer or bit-coded value.

Because a bit-coded value is represented by the integer data type, you can use the + and – functions to add or remove a bit value for the overall sum of a bit-coded value. AutoLISP also provides several useful functions that you can use when working with bit-coded values. The logior and logand functions help combine several bit-coded values and determine whether a bit is part of a bit-coded value. Let's take a closer look at the logior and logand functions.

3.1.8 Working with Bit-Coded Values

The following exercise demonstrates how to work with bit-coded values. You'll create a custom function that allows you to toggle the state of the INTersection object snap. The current running object snap modes are stored in the osmode system variable, which contains a bit-coded value. The INTersection object snap is represented by the bit code 32.

### 0207. 术语卡 —— Inline Variable Expansion

信息源自「2019116AutoCAD-Platform-Customization0203.md」：

Inline variable expansion is the process of defining a variable and then adding the name of the variable using the format `%VARIABLE_NAME%` (Windows) or `${VARIABLE_NAME}` (Mac OS) in a string. The name of the variable is then replaced with the variable's actual value when the expression containing the string is used. Inline variable expansion is not native functionality in AutoLISP, but it can be simulated. Inline variable expansion is supported by other programming languages and is often used with values that are defined by the operating system. Listing 13.1 in this section demonstrates one possible implementation of inline variable expansion in AutoLISP.

1『太惊喜了，autolisp 里竟然也能模拟内联变量，那种很常用的，嵌入在字符串里的变量，感谢作者的源码，哈哈。做一张术语卡片。（2021-03-06）』

Listing 13.1 is a custom function that mimics the use of inline variable expansion. When the function is executed, it attempts to match the text between % (percent) signs with a user-defined variable. If the variable is found, the inline variable is replaced by its current value.

Listing 13.1: The ExpandVariable function

```c
; Custom implementation of expanding variables in AutoLISP 
; To use: 
; 1. Define a variable with the setq function. 
; 2. Add the variable name with % symbols on both sides of the variable name. 
; For example, the variable named *program* would appear as %*program*% in the string. 
; 3. Use the function on the string that contains the variable. 
(defun expandvariableUtils (string / start_pos next_pos var2expand expand_var) 
  (while (wcmatch string "*%*%*") 
         (progn 
          (setq start_pos (1+ (vl-string-search "%" string))) 
          (setq next_pos (vl-string-search "%" string start_pos)) 
          (setq var2expand (substr string start_pos (- (+ next_pos 2) start_pos))) 
          (setq expand_var (vl-princ-to-string (eval (read (vl-string-trim "%" var2expand))))) 
          (if (/= expand_var nil) 
            (setq string (vl-string-subst expand_var var2expand string)) 
          ) 
         ) 
  ) 
  string 
) 

; Define a global variable and string to expand 
(setq *program* (getvar "PROGRAM") str2expand "PI=%PI% Program=%*program*%" ) 
; Execute the custom function to expand the variables defined in the string 
(expandvariable str2expand) 
"PI=3.14159 Program=acad"
```

### 0208. 术语卡 —— ActiveX/COM

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

The AutoLISP® functions you have learned up to this point have been, for the most part, platform neutral and are unofficially known as Classic AutoLISP or Core AutoLISP. Starting with the Autodesk® AutoCAD® 2000 program, AutoLISP saw an architecture change that allowed for the use of the Microsoft ActiveX technology. ActiveX is a technology that enables applications to communicate and exchange information. COM (Component Object Model) is a library of objects that let you make changes to or query exposed objects. COM is an example of ActiveX.

1『这里 ActiveX/COM 本质上是一个库，做一张术语卡片。（2021-03-06）』

In this chapter, you will learn the basics of using ActiveX with AutoLISP and how to leverage the AutoCAD, Microsoft Windows, and Microsoft Office COM libraries. Although this chapter doesn't go into great depth, it will give you a starting point and a general understanding of the functions you need to become familiar with in order to use ActiveX and access COM libraries. The primary reasons to use COM are to monitor actions in AutoCAD with reactors, access external applications such as Microsoft Word or Excel, and work with complex objects, such as tables and multileaders.

ActiveX is the technology that allows for the use of COM. It is often associated with Visual Basic for Applications (VBA) and Visual Basic (VB) scripting these days, but it can be used by many modern programming languages, such as VB.NET and C++. Although many people refer to ActiveX and COM as the same thing, they aren't. ActiveX is the technology that was developed by Microsoft to allow software developers to expose objects using COM, thereby letting programmers communicate with the programs in new ways.

In general, there are three concepts you need to understand about working with ActiveX in AutoLISP programs: 1) Classes, objects, and collections. 2) Methods and properties. 3) Variant and array data types.

### 0209. 术语卡 —— Collections

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

Collections are objects that can be queried and modified using properties and methods, but they are also containers that hold similar objects. A collection fundamentally is similar to a symbol table; you can work with a symbol table and add new objects to it, but you can't create a new symbol table. All the collections that you need in order to work with AutoCAD objects are defined as part of the AutoCAD ActiveX API. For example, a Layers collection contains all of the Layer objects in a drawing, and a Documents collection contains all the open drawings (or Document objects) in the current AutoCAD session. You can get an object from a collection using the Item method, add a new object to a collection using the Add method, and remove an object from a collection using the Delete method.

1-2『这里的 Collections 概念很重要的，而且获取到两个关键数据集：图层的 Collections、CAD 当前打开的图纸的 Collections。Collections 做一张术语卡片。（2021-03-06）』—— 已完成

If you want to step through a collection and perform a set of statements on each object, you can use the `vlax-for` AutoLISP function, which is similar to the `foreach` function. The following shows the syntax of the vlax-for function:

```c
(vlax-for var coll [expressionN …])
```

### 0210. 术语卡 —— Variants and Arrays

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

vla-object isn't the only new data type that you will have to understand when working with ActiveX. Many methods and properties use what is known as a variant. The variant data type is the chameleon of data types; it can represent any supported data type. A variant in AutoLISP is represented by the vla-variant data type. Arrays are yet another type of data that you will need to become familiar with. An array is represented by the vla-array data type and is similar to the AutoLISP list data type.

2『这里的 Variants and Arrays，做一张术语卡片。（2021-03-07）』—— 已完成

Most properties and methods return or expect values of a specific type, but there will be times when you will need to assign a property or pass a method a variant value. Some data structures can represent multiple values, such as a point or Xdata, and in these situations the AutoCAD COM library is designed to return or accept a variant value. You define a variant by using the `vlax-make-variant` function. The following shows the syntax of the `vlax-make-variant` function:

The array data type is similar to the AutoLISP list data type, but typically an array is made up of a specified number of elements. You will remember that a list can hold any number of elements. A common use for arrays with the AutoCAD COM library is to represent a point list. Arrays can also be used to pass multiple objects to a method or for times when you want to return more than one value from a custom function.

The `vlax-make-safearray` function is used to create a new array based on a specific data type and number of elements. The following shows the syntax of the `vlax-make-safearray` function:

### 0211. 术语卡 —— symbol tables

源自「2019116AutoCAD-Platform-Customization0217.md」：

A drawing file can contain two types of nongraphical objects: symbol tables and named dictionaries. Symbol tables represent the original named objects that were available in the AutoCAD® R12 release and earlier ones. Support for named dictionaries was added with AutoCAD R13 to handle new and custom objects without the need for a new drawing file format. In this chapter, you will learn to create, manage, and use symbol table and dictionary entries.

1-2『symbol tables and named dictionaries，各做一张术语卡片。（2021-03-11）』

Symbol tables are the oldest form of nongraphical objects used in drawing files and have been unchanged since AutoCAD R12. Although the features that use symbol tables have changed since AutoCAD R12, the additional information that those features use in later releases is attached as either XData or an extension dictionary on an entry or the symbol table.

1『原来 XData 是对 symbol tables 的替代。（2021-03-11）』

Have you opened a drawing from a client to find what seems like a spaghetti mess of layers, linetypes, and text styles that just don't work well with your standards? Maybe the Standard text style in the client's drawings uses a fixed height and different font than your company uses, which would affect the way your blocks and annotation might look like in the drawing. Using the AutoLIS® programming language, you can create or change nongraphical objects stored in symbol tables or dictionaries so they align with your company's standards. Aligning the standards in the drawings received from a client ensure that the objects you create and those in the drawings plot with a consistent appearance.

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

### 0212. 术语卡 —— named dictionaries

源自「2019116AutoCAD-Platform-Customization0217.md」：

### 0301. 任意卡 —— 生成 VLX 文件

VLX 文件是 LSP 文件编译后的成品文件。在 Visual LISP 编译器里，「文件 -> 生成应用程序 -> 新建应用程序向导」，按步骤一步步来。

### 0302. 任意卡 —— 数据存到公共变量（内存）

TIP: User-defined variables are normally accessible only from the drawing in which they are defined, but you can use the AutoLISP `vl-bb-ref` and `vl-bb-set` functions to define variables on what is known as the blackboard. The blackboard is a centralized location for defining variables that can be accessed from any open drawing. The AutoLISP vl-propagate function can also be used to define a variable with a specific value in all open drawings and any drawings that are subsequently opened in the AutoCAD session. You can learn more about these functions in the AutoCAD Help system.

1-2『上面的几个函数，可以实现把一些数据放到公共变量（内存）中，保证所有打开的图纸空间都可以访问到。这个可以帮助实现把数据从流程图迁移到设备布置图，功能待开发，哈哈。做一张任意卡片。（2020-10-08）回复：这个知识点确实很有用，目前准备用 `vl-bb-set` 和 `vl-bb-ref` 把流程图里的信息传递给布置图，对于复杂的逻辑，再结合读取本地数据库（直接以文本的形式存储）来实现。（2020-11-26）』—— 已完成

[About Sharing Data Between Namespaces (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-0C8F8E36-7C10-45C4-9EF6-C284E56A8EA2)

A namespace called the blackboard is used for communicating values across all namespaces. The blackboard namespace is not attached to any document or VLX application. You can set and reference variables in the blackboard from any document or VLX application. Use the vl-bb-set function to set a variable, and use vl-bb-ref to retrieve a variable's value.

For example, the following sets the foobar variable to a string in the blackboard namespace:

```c
(vl-bb-set 'foobar "Root toot toot")
```

The vl-bb-ref function returns the specified string. The following uses the vl-bb-ref function to retrieve the value of the foobar variable from the blackboard namespace:

```c
(vl-bb-ref 'foobar)
```

Setting or retrieving variable values in the blackboard namespace has no effect on variables of the same name in any other namespace.

vl-propagate. Copies the value of a variable into all open document namespaces (and sets its value in any subsequent drawings opened during the current AutoCAD session)

```c
(vl-propagate 'symbol)
```

函数 `vl-propagate` 相当于将一个变量直接变为「全图纸空间变量」。

### 0303. 任意卡 —— 宏命令里的悬停

When the command function is used, you can suspend the execution of an AutoLISP program and allow the user to provide input at the Command prompt. You use the predefined PAUSE variable or the "\\" ASCII character sequence to allow the user to provide a value. The following AutoLISP expression starts the circle command and then allows the user to specify a center point. Once a center point is specified, the circle's diameter is set to 3 units.

```c
(command "._circle" PAUSE "_d" 3)
```

2『宏命令里的悬停，做一张任意卡片。补充：用空字符串 `""` 也可以实现。（2021-03-02）补充：PAUSE 和空字符串应该是两个概念，PAUSE 参数间的衔接，空字符串是默认选项。（2021-03-12）』—— 已完成

### 0304. 任意卡 —— 自定义命令变为内置命令

TIP: Although custom AutoLISP functions that have the C: prefix aren't recognized as native AutoCAD commands, you can use the AutoLISP vlax-add-cmd and vlax-remove-cmd functions to register a custom AutoLISP function as a built-in AutoCAD command. (These functions are available only on Windows.) There are a couple reasons you might want to do so. The first is so that your custom functions trigger events or reactors related to when a command starts or ends. The other reason is so that your custom function can be called with the command or command-s function. You can learn more about these functions in the AutoCAD Help system.

2『自定义命令变为内置命令的实现手段，做一张任意卡片。』—— 已完成

### 0305. 任意卡 —— 函数以 princ 结尾的真正用途
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

### 0306. 任意卡 —— 调整窗口布局

Tiles are stacked vertically in a dialog box by default, unless you use what are called cluster tiles. Cluster tiles are used to group and align tiles in rows and columns. Tiles also support several attributes that help you control their size and alignment in a dialog box. In addition to cluster tiles and attributes, spacer tiles can be used to control the size and alignment of tiles. A spacer tile allows for the insertion of empty space between tiles in a dialog box.

1-2『调整窗口布局的几种方式汇总：1）用 cluster tiles 控制。2）用 tile 里的属性控制。3）用 spacer tiles 控制。做一张任意卡片。』—— 已完成

### 0307. 任意卡 —— 加载显示窗口的 2 种方法

You can create a DCL file with Notepad or the Visual LISP Editor; you follow the same process you use to create a LSP file. The only difference is that you specify a file extension of .dcl instead of .lsp. Once you create a DCL file, you can add a dialog box definition to the file. To see what the dialog box looks like, you must load the DCL file in the AutoCAD drawing environment and display it. There are two approaches available for viewing a DCL file. The first is to create an AutoLISP program that loads and displays the file; the other involves using the Visual LISP Editor. (The second approach eliminates the need to write any code.) I discuss how to load a DCL file and display a dialog box in the next section.

1『加载显示窗口（box）的 2 种方法，做一张任意卡片。』—— 已完成

回复：目前一直用的是第一种方法，即在 autolisp 里加载 dcl 文件。（2020-10-27）

### 0308. 任意卡 —— 通过特定的动作直接更新交互界面的下拉列表数据

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

1-2『目前还没想到，直接在交互界面里给下拉菜单添加元素的应用场景。回复：想到应用场景了，比如筛选选择集之后，将选集里的相关内容直接在交互界面上呈现出来，就跟 CAD 原生查询面板一样。（2020-10-09）回复：这个功能其实非常有用，比如想开发的功能，先根据某个属性值匹配通配符来筛选管道号块，筛出来的块只把属性值提取出来添加到这个列表让用户看到。第二部输入要替换的原字符以及新字符，这个功能一定要实现。（2020-10-10）做一张任意卡片。』—— 已完成

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

### 0309. 任意卡 —— 如何在一个 lsp 文件里调用另外一个 lsp 文件

直接在 lsp 里写加载语句 `(load "utility.lsp")`，然后在 CAD 里用命令 `appload` 同时加载这两个函数即可。

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

NOTE: LSP files that are loaded using one of the manual techniques described here are loaded only into the current drawing. You must load the LSP file into each and every drawing file where you want to use it. However, you can use the vl-load-all function to load a LSP file into all open and subsequently opened drawings for the current AutoCAD session.

1-3『

这里又意外解决一个老大难的问题，新打开的文件可以自动加载数据流的插件。补充进任意卡片「如何在一个 lsp 文件里调用另外一个 lsp 文件」。（2021-03-02）—— 已完成

单独新建了一个启动文件 `startdataflow.lsp`。

```c
(defun s::startup ()
  (vl-load-all "D:\\dataflowcad\\dataflow.VLX")
)
```

前面正好讲到，函数 `s::startup` 是可以自动加载的。

』

### 0310. 任意卡 —— 创建实体数据的 2 个方法

The command function is the most common method that AutoLISP programmers use to create and modify objects, but it isn't the most efficient when you are trying to modify individual properties of an object. Even creating lots of objects in the Autodesk® AutoCAD® program can be slower with the command function. Along with the command function, objects can be created and modified directly by setting property values as part of an entity data list. Extended data (XData) can also be attached to an object as a way to differentiate one object from another or, in some cases, to affect the way an object might look in the drawing area.

1-2『直接用 command，自己就遇到了瓶颈。1）确实效率低下。2）自动生成辅助流程组件，插进来的块，位置经常不是均匀的，目前一直找到不解决办法。正巧这里受到启发，改用直接创建实体数据的方法实现自动生成块。待实现。做一张任意卡片。（2020-10-29）回复：已经实现了，而且用起来真舒服，详见数据流的源码。（2020-11-26）补充：目前已习得通过 ActiveX 技术来生成 CAD 实体对象，详见数据流源码。（2021-03-22）』

Using AutoLISP, you can create a table using the entmake function while modifying and populating the table with the entget and entmod functions.

### 0311. 任意卡 —— 获取实体数据信息

除了用选择集的方式，先获得选择集，通过选择集获取各个实体的实体名，再通过实体名获得实体的数据集。也可以通过下面的方式直接获取实体数据集（直接用 `entlast` 和 `entnext` 这些函数获取实体名，然后调 `entget` 获取数据集）。两种方法的区别在于如何获得实体名，一个是靠用户选择（选择集），一个是全部在后台完成。（2020-11-26）

AutoLISP provides two different techniques that can be used to select an individual object within a drawing — through code or via user interaction. When you want to work with the most recent object or step through all of the objects in a drawing, you don't need any input from the user. The AutoLISP functions entlast and entnext can be used to get an individual object without any input from the user. If you do want to allow the user to interactively select an individual object, you can use the entsel and nentsel functions.

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

1-2『这个例子看下来后，entlast、entnext 还有 entget 这几个函数结合起来可以做好多事，特别是 entnext 的用法灵活性很大。比如自动生成辅助流程里，又想到一个思路：1）先直接使用 entlast 获取图纸里的最后一个实体名保存下来。2）批量插入辅助流程组件块后，通过刚刚最后一个实体名外加 entnext 函数，可以获得所有批量插入的块的实体名列表。3）根据这个实体名列表批量修改属性值，这样又跟以前开发好的功能对接上了。把上面信息合并到「获取实体数据集的方式」任意卡里。补充：还有一种思路，生成实体对象后直接用函数 `entlast` 获取其 entity name 存起来。（2021-03-12）』—— 已完成

### 0312. 任意卡 —— Controlling a Command's Version

Internally each standard AutoCAD command is assigned a new version number when a change is made that affects an AutoLISP program, script, or command macro. You use the initcommandversion function to control which version of a command is used by the next use of the command or command-s function. The initcommandversion function doesn't require a value, but when one is provided it must be an integer value that represents the version of the command you want to use.

The following example uses version 1 of the color command:

```c
(initcommandversion 1) 
(command "._color")
```

Version 1 of the color command displays options at the Command prompt; version 2 or later displays the Select Color dialog box instead. The -insert command is another command that is affected by the initcommandversion function. When using version 2 of the -insert command, the user can interact with the AutoCAD Properties palette in Windows while a preview of the block is being dragged in the drawing area.

1-2『真是巧了，昨天实现自动批量插入设备位号的时候才发现这个问题。当时是通过 `(setvar "ATTREQ" 1)` 实现插入块的时候交互输入属性值，插完后再将系统变量 ATTREQ 重置为 0。不过试验了下，改用 `(initcommandversion 2)` 实现了不了自动插入设备位号，目前原因不知。命令的版本号，做一张术语卡片。（2020-10-08）』—— 已完成

### 0313. 任意卡 —— 通过图层名判断是否存在该图层

源自「2019116AutoCAD-Platform-Customization0210.md」：

1-2-3『

自己在 CAD 里跑了下上面的源码，没问题，第一次知道多行注释可以这么写（`|`），很不错！这里还有一个很意外的收获，如何判断是否有某一个图层。那么同样的，应该可以判断某个块是否存在。待验证。做一张任意卡片。（2021-03-02）—— 已完成

```c
(defun createlayer (name color / ) 
  ; Check to see if the layer exists before creating/modifying it 
  (if (= (tblsearch "layer" name) nil) 
    (command "._-layer" "_m" name "_c" color "" "") 
    (setvar "clayer" name) 
  ) 
) 
```

[tblsearch (AutoLISP)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-2AEB84A6-E3D0-4DD9-A29C-54D4099ED925)

验证过了，按块名称搜索，可行。（2021-03-03）

```c
(tblsearch "BLOCK" "Centrifuge")
```

』

### 0314. 任意卡 —— 对模型空间（model space）以及布局（layout）的理解

源自「2019116AutoCAD-Platform-Customization0217.md」：

Nongraphical objects represent the block definitions, named styles, and other objects that are stored in a drawing but aren't present in model space or one of the named layouts. These objects can and typically do affect the display of graphical objects placed in model space or a named layout, though. While model space and named layouts are typically not thought of as nongraphical objects, they are. Model space is a special block definition, whereas a layout is an object that is based on a plot configuration — commonly called a page setup — with a reference to a block definition.

1-2『这里对模型空间（model space）以及布局（layout）定义很出乎意料，模型空间是一张特殊的块定义，布局是一个基于绘制设置的对象。做一张任意卡片。（2021-03-11）』

## Introduction

In 1996, Lee began learning the core concepts of customizing the AutoCAD user interface and AutoLISP. The introduction of VBA in AutoCAD R14 would once again redefine how Lee approached programming solutions for AutoCAD. VBA made it much easier to communicate with external databases and other applications that supported VBA. It transformed the way information could be moved between project management and manufacturing systems.

Not being content with VBA, in 1999 Lee attended his first Autodesk University and began to learn ObjectARX®. Autodesk University had a lasting impression on him. In 2001, he started helping as a lab assistant. He began presenting on customizing and programming AutoCAD at the event in 2004. Along the way he learned how to use the AutoCAD Managed.NET API.

Customization is one of the feature areas that sets AutoCAD apart from many other CAD programs. Even though the product can be used out of the box, configuring the user interface and modifying the support files that come with the product can greatly improve your productivity. By customizing AutoCAD, you can streamline product workflows and create new ones that are a better fit with the way your company works. These workflows might range from importing layers and styles into a drawing to the extraction of drawing-based information into a spreadsheet or database.

The AutoLISP programming language can be used to: Create custom functions that can be executed from the AutoCAD Command prompt; Create and manipulate graphical objects in a drawing, such as lines, circles, and arcs; Create and manipulate nongraphical objects in a drawing, such as layers, dimension styles, and named views; Perform mathematical and geometric calculations; Request input from or display messages to the user at the Command prompt; Interact with files and directories in the operating system; Read from and write to external files; Connect to applications that support ActiveX and COM; Display dialog boxes and get input from the end user.

AutoLISP code can be entered directly at the Command prompt or loaded using a LSP file. Once an AutoLISP program has been loaded, you can execute the custom functions from the Command prompt. Functions executed from the Command prompt can be similar to standard AutoCAD commands, but the programmer determines the prompts that should be displayed. It is also possible to use AutoLISP code with a command macro that is activated from the AutoCAD user interface or a tool on a tool palette.

1『 VBA 能实现的功能同上。追加：这里的宏 macro 跟原生 lisp 语言里的 macro 有啥联系？（2020-11-26）』

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

2『 16 和18 章里应该有，将数据导出的相关信息。结果发现 17 章里也有这方面的信息。最终竟然在第 3 章里找到解决办法，直接用命令 dataextraction 就可以提取块里面的属性信息，以 csv 或 txt 格式导出来。回复：用 dataextraction 很 low，而且中间步骤很多，现在已经实现了直接读写数据。（2020-11-26）』

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

1-2『这章感觉有直接定位到选定的实体对象位置的相关实现，待确认。（2020-11-26）补充：已经实现了。目前知道两种方法：1）选择集结合宏命令 ZOOM。2）用 ActiveX 方法 `(vla-ZoomAll acadObj)`，其中 acadObj 是一个 vla-object。（2021-03-12）』——未完成

Chapter 29: Annotating Objects In this chapter, you'll learn how to create and modify annotation objects. Typically, annotation objects are not part of the final product that is built or manufactured based on the design in the drawing. Rather, annotation objects are used to communicate the features and measurements of a design. Annotation can be a single line of text that is used as a callout for a leader, a dimension that indicates the distance between two drill holes, or a table that contains quantities and information about the windows and doors in a design.

1『 dimension 应该指标注线，那么开发标注线相关的功能可以去看 0209 章的内容。（2021-03-12）』

Chapter 30: Working with Blocks and External References In this chapter, you'll learn how to create, modify, and manage block definitions. Model space in a drawing is a special named block definition, so working with block definitions will feel familiar. Once you create a block definition, you will learn how to insert a block reference and work with attributes along with dynamic properties. You complete the chapter by learning how to work with externally referenced files.

1-2『上面这章应该有直接插入外部文件块的信息，待确认。（2020-11-26）补充：已经实现了，通过引用 Lee Mac 封装好的模块。（2021-03-12）』—— 已完成

Chapter 31: Outputting Drawings In this chapter, you will learn how to output the graphical objects in model space or on a named layout to a printer, plotter, or electronic file. Named layouts will be used to organize graphical objects for output, including title blocks, annotation, floating viewports, and many others. Floating viewports will be used to control the display of objects from model space on a layout at a specific scale. After you define and configure a layout, you learn to plot and preview a layout. The chapter wraps up with learning how to export and import file formats.

Chapter 32: Storing and Retrieving Custom Data In this chapter, you will learn how to store custom information in a drawing or in the Windows Registry. Using extended data (Xdata), you will be able to store information that can be used to identify a graphical object created by your program or define a link to a record in an external database. In addition to attaching information to an object, you can store data in a custom dictionary that isn't attached to a specific graphical object in a drawing. Both Xdata and custom dictionaries can be helpful in making information available between drawing sessions; the Windows Registry can persist data between sessions.

1『目前图纸里可以作为数据库的地方：字典、Xdata，还有上面信息提到的路径，待研读 32 章。（2021-03-12）』

Chapter 33: Modifying the Application and Working with Events In this chapter, you will learn how to customize and manipulate the AutoCAD user interface. You also learn how to load and access externally defined custom programs and work with events. Events allow you to respond to an action that is performed by the end-user or the AutoCAD application. There are three main types of events that you can respond to: application, document, and object.

Chapter 34: Creating and Displaying User Forms In this chapter, you will learn how to create and display user forms. User forms provide a more visual approach to requesting input from the user.

Chapter 35: Communicating with Other Applications In this chapter, you will learn how to work with libraries provided by other applications. These libraries can be used to access features of the Windows operating system, read and write content in an external text or XML file, and even work with the applications that make up Microsoft Office.

1-3『

这章涉及与其他 app 的交互，那么有提取 cad 数据直接进服务器的实现线索。（2020-06-25）

应该是可以实现的，找到了一些资料，还没来得及实操实现。（2021-03-12）


[已解决: access internet/ remote directory - Autodesk Community - AutoCAD](https://forums.autodesk.com/t5/visual-lisp-autolisp-and-general/access-internet-remote-directory/m-p/9383094#M397309)

[已解决: Make an API call with AutoLISP / VisualLISP - Autodesk Community - AutoCAD](https://forums.autodesk.com/t5/visual-lisp-autolisp-and-general/make-an-api-call-with-autolisp-visuallisp/td-p/9083202)

』

Chapter 36: Handling Errors and Deploying VBA Projects In this chapter, you will learn how to catch and handle errors that are caused by the incorrect use of a function or the improper handling of a value that is returned by a function. The Visual Basic Editor provides tools that allow you to debug code statements, evaluate values assigned to user-defined variables, identify where within a program an error has occurred, and determine how errors should be handled. The chapter wraps everything up with learning how to deploy a VBA project on other workstations for use by individuals at your company.

Bonus Chapter 1: Working with 2D Objects and Object Properties In this chapter, you build on the concepts covered in Chapter 27,「Creating and Modifying Drawing Objects.」You will learn to create additional types of 2D objects and use advanced methods of modifying objects, you also learn to work with complex 2D objects, such as regions and hatch fills. The management of layers and linetypes and the control of the appearance of objects are also covered.

Bonus Chapter 2: Modeling in 3D Space In this chapter, you learn to work with objects in 3D space, and 3D objects. 3D objects can be used to create a model of a drawing which can be used to help visualize a design or detect potential design problems. 3D objects can be viewed from different angles and used to generate 2D views of a model that can be used to create assembly directions or shop drawings.

Bonus Chapter 3: Development Resources In this chapter, you discover resources that can help expand the skills you develop from this book or locate an answer to a problem you might encounter. I cover development resources, places you might be able to obtain instructor-led training, and interact with fellow users on extending AutoCAD. The online resources sites listed cover general customization, AutoLISP, and VBA programming in AutoCAD.