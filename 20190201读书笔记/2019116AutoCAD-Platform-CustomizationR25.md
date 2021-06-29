## 记忆时间

## 目录

Part II AutoLISP: Productivity through Programming

0211 —— Chapter 21: Using the Visual LISP Editor (Windows only)

0212 —— Chapter 22: Working with ActiveX/COM Libraries (Windows only)

0213 —— Chapter 23: Implementing Dialog Boxes (Windows only)

## 0211. Using the Visual LISP Editor (Windows only)

1『目前用的是 VScode，感觉无需使用 Visual LISP Editor，此章节先忽略。（2021-03-07）』

## 0212. Working with ActiveX/COM Libraries (Windows only)

The AutoLISP® functions you have learned up to this point have been, for the most part, platform neutral and are unofficially known as Classic AutoLISP or Core AutoLISP. Starting with the Autodesk® AutoCAD® 2000 program, AutoLISP saw an architecture change that allowed for the use of the Microsoft ActiveX technology. ActiveX is a technology that enables applications to communicate and exchange information. COM (Component Object Model) is a library of objects that let you make changes to or query exposed objects. COM is an example of ActiveX.

1『这里 ActiveX/COM 本质上是一个库，做一张术语卡片。（2021-03-06）』

In this chapter, you will learn the basics of using ActiveX with AutoLISP and how to leverage the AutoCAD, Microsoft Windows, and Microsoft Office COM libraries. Although this chapter doesn't go into great depth, it will give you a starting point and a general understanding of the functions you need to become familiar with in order to use ActiveX and access COM libraries. The primary reasons to use COM are to monitor actions in AutoCAD with reactors, access external applications such as Microsoft Word or Excel, and work with complex objects, such as tables and multileaders.

### 12.1 Understanding the Basics of ActiveX

ActiveX is the technology that allows for the use of COM. It is often associated with Visual Basic for Applications (VBA) and Visual Basic (VB) scripting these days, but it can be used by many modern programming languages, such as VB.NET and C++. Although many people refer to ActiveX and COM as the same thing, they aren't. ActiveX is the technology that was developed by Microsoft to allow software developers to expose objects using COM, thereby letting programmers communicate with the programs in new ways.

In general, there are three concepts you need to understand about working with ActiveX in AutoLISP programs: 1) Classes, objects, and collections. 2) Methods and properties. 3) Variant and array data types.

#### 12.1.1 Accessing Classes, Objects, and Collections

Classes are the elements on which a COM library is built — think of them as a recipe. The AutoCAD COM library has classes for the AutoCAD application, a drawing (known as a document) file, and the graphical and nongraphical objects that are stored in a drawing. An object is an in-memory and unique instance of a class. Although a collection is also an object, it is a container for objects of the same type.

#### Working with Objects

The vla-object data type is used in AutoLISP to represent an object or collection. (You'll learn how to work with the AutoCAD COM library in the「Using the AutoCAD COM Library」section, and with the COM libraries related to Windows and Microsoft Office in the「Leveraging the Windows and Microsoft Office COM Libraries」section, later in this chapter.) Many of the objects you will want to work with can be accessed using properties and methods described in the next section. However, there are some objects that you must create or get an instance of before you can work with them.

2『之前没注意到的知识点：vla-object 要么是对象 object，要么是集合 collection。（2021-06-28）』

For example, you can use the `vlax-create-object` function to create an instance of an application or secondary object that isn't accessible from an object that is already in memory. The `vlax-get-object` function can be used to get an instance of an object that is already in memory. When an object is in memory, it can be accessed and manipulated. The following shows the syntax of the `vlax-create-object` and `vlax-get-object` functions:

```c
(vlax-create-object prog_id) 
(vlax-get-object prog_id)
```

The `prog_id` argument is a string that represents the program ID of the object you want to create or get. The program ID follows the syntax of vendor.component, and it can optionally have a version number as well, for a syntax of vendor.component.version. Typically, vendor is the name of the software or company that created the component, whereas component is commonly a class.

For example, if you wanted to create or check for an instance of AutoCAD you would use the program ID of AutoCAD.Application. The AutoCAD program ID optionally supports a version number that allows you to look for a specific AutoCAD release. The version number always consists of a major value, while some version numbers can contain both a major and a minor value. The major version of 19 is shared between AutoCAD 2013 and 2014, but if you want to refer to AutoCAD 2014 you use the minor number of 1. The program ID for AutoCAD 2014 is AutoCAD.Application.19.1. If you want to reference AutoCAD 2015, you use AutoCAD.Application.20 for the program ID. Refer to the AutoCAD Help system for the version number assigned to your AutoCAD installation.

The `vlax-create-object` and `vlax-get-object` functions return a vla-object if a new object is created or if an object with the program ID is already in memory; nil is returned if the object couldn't be created or retrieved from memory. The following shows how to create a new instance of the AutoCAD True Color (AcCmColor) and Microsoft Word (Application) objects. The AcCmColor object is used to manipulate the color value assigned to a drawing object.

```c
; Creates an instance of an AutoCAD True Color object 
(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) 
#<VLA-OBJECT IAcadAcCmColor 000000002dcdd650> 
; Creates an instance of the most recently used Microsoft Word application 
(setq wordObj (vlax-create-object "Word.Application")) 
#<VLA-OBJECT _Application 000000002f1e3c78> 
; Attempts to create an instance of the Microsoft Word 2010 application 
; but the application is not installed on this workstation 
(setq wordObj (vlax-create-object "Word.Application.14")) 
nil 
; Creates an instance of the Microsoft Word 2013 application
; installed 
(setq wordObj (vlax-create-object "Word.Application.15")) 
#<VLA-OBJECT _Application 000000002f1e3b98>
```

1-2『测试过了，word 2016 版的 program ID 是 `Word.Application.16`。补充：后面的信息得知，其实没必要写版本号，直接 `Word.Application`。（2021-03-06）补充：之前的理解有偏误，上面写版本号使用创建对象的函数 vlax-create-object，而下面不写版本号是直接获取电脑内存（默认 word 打开着）中，用的函数是vlax-get-object，两个函数不一样的。（2021-06-28）』

The following shows how to get an instance of the Microsoft Word application that has already been started:

```c
; Gets an instance of a non-version-specific release of the 
; Microsoft Word application that is in memory 
(setq wordObj (vlax-get-object "Word.Application")) 
#<VLA-OBJECT _Application 000000000a92e568>
```

Although you can use the `vlax-get-object` function to get an instance of an object in memory, or create a new instance of an object with the `vlax-create-object` function, the `vlax-get-or-create-object` function combines the functionality of both. If an object already exists, `vlax-get-or-create-object` returns the object and, if not, a new instance of the object is created. `vlax-get-or-create-object` has the same syntax as vlax-create-object.

```c
; Gets/creates an instance of the most recently used Microsoft Word application 
(setq wordObj (vlax-get-or-create-object "Word.Application")) 
#<VLA-OBJECT _Application 000000000a92e568>
```

1-2『 `vlax-get-or-create-object` 这个函数好用，录入主题卡「函数收藏」。（2021-03-06）』—— 已完成

When an object is created with the `vlax-create-object` or `vlax-get-or-create-object` function, it must be released from memory when it is no longer used. You use the `vlax-release-object` function to release an object; the function must be passed the value returned by the `vlax-create-object` or `vlax-get-or-create-object` function. The `vlax-release-object` function returns a random integer value that has no specific meaning if the value it was passed is a valid object; an error is returned if the value passed wasn't a valid object that could be released.

The following code shows how to release an object created with the `vlax-create-object` or `vlax-get-or-create-object` function:

```c
(vlax-release-object wordObj) 
0 
(vlax-release-object cObj) 
; error: null interface pointer: #<VLA-OBJECT 0000000000000000>
```

#### Working with Collections

Collections are objects that can be queried and modified using properties and methods, but they are also containers that hold similar objects. A collection fundamentally is similar to a symbol table; you can work with a symbol table and add new objects to it, but you can't create a new symbol table. All the collections that you need in order to work with AutoCAD objects are defined as part of the AutoCAD ActiveX API. For example, a Layers collection contains all of the Layer objects in a drawing, and a Documents collection contains all the open drawings (or Document objects) in the current AutoCAD session. You can get an object from a collection using the Item method, add a new object to a collection using the Add method, and remove an object from a collection using the Delete method.

1-2『这里的 Collections 概念很重要的，而且获取到两个关键数据集：图层的 Collections、CAD 当前打开的图纸的 Collections。Collections 做一张术语卡片。（2021-03-06）』—— 已完成

If you want to step through a collection and perform a set of statements on each object, you can use the `vlax-for` AutoLISP function, which is similar to the `foreach` function. The following shows the syntax of the vlax-for function:

```c
(vlax-for var coll [expressionN …])
```

Here are its arguments:

1 var. The var argument specifies the user-defined variable, which you use to reference the current item of the coll argument as the collection is being stepped through.

2 coll. The coll argument specifies a collection object of the vla-object data type, which should be stepped through one item at a time.

3 expressionN. The expressionN argument represents the expressions that should be executed when each object in the coll argument is found. The object is located using the name in the var argument.

The following is an example of the vlax-for function that steps through the Layouts collection and returns the name of each layout in a drawing:

```c
; Imports the functions for the AutoCAD COM library, 
; if not already available 
(vl-load-com) 

(defun c:foo (/ curDoc layouts)
  (setq curDoc (vla-get-activedocument (vlax-get-acad-object))) 
  ; Gets the Layouts collection 
  (setq layouts (vla-get-layouts curDoc)) 
  ; Creates a report header 
  (prompt (strcat "\nLayouts count: " (itoa (vla-get-count layouts)))) 
  (prompt "\nLayouts: ") 
  ; Steps through the objects in the collection 
  (vlax-for layout layouts 
    (prompt (strcat "\n " (vla-get-name layout))) 
  )
  (princ)
)

; The output from the previous expressions 
Layouts count: 3 
Layouts: 
	Layout1 
	Layout2 
	Model
```

1-3『

跑了下，完全没问题，获取到了 3 个布局的信息。这里可以深挖的信息量很多的：1）此时才了解到，一个实体对象其 DXF 码 410 的值「model」就是这里的「布局」名称。2）获取当前「活动」图纸的所有数据 `(vla-get-activedocument (vlax-get-acad-object))`，这个函数极其重要。3）里面涉及到很多函数可以去官方文档研读，而且可以顺藤摸瓜找到更多实用的函数。比如将函数 `vla-get-layouts` 更改为 `vla-get-blocks` 即可获取到所有块的数据。而且对象数据的全景图详见下面的官方文档链接，要反复研读。（2021-03-06）补充：还可以借助 VScode 里函数提示的功能，发掘更过类似于 `vla-get-layouts` 的函数。（2021-06-28）

[AutoLisp: Object Model (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-A809CD71-4655-44E2-B674-1FE200B9FE30)

全景图里每个图块可以点进去，比如「块」：

[AutoLisp:  Blocks Collection (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-E77CC5AD-74B8-472C-8270-32FD162D5653#GUID-E77CC5AD-74B8-472C-8270-32FD162D5653)

这里可以获取到块数据集（Blocks Collection）里的接口。

』

You can use the `vlax-map-collection` function to execute a single AutoLISP function on each object in a collection. The following shows the syntax of the `vlax-map-collection` function:

```c
(vlax-map-collection coll 'func)
```

Here are its arguments:

1 coll. The coll argument specifies the collection object, of the vla-object data type, that should be stepped through one item at a time.

2 ‘func. The func argument represents the function you want to execute on each object in the coll argument. An apostrophe must be placed in front of the function name to let AutoLISP know it is a value that should not be evaluated.

1『太赞了，及时雨啊，`vlax-map-collection` 对应于自己用的最多的函数 `mapcar`。（2021-03-06）』

#### 12.1.2 Specifying Properties and Invoking Methods

A class uses two different approaches to expose itself to a programming language such as AutoLISP or VBA: properties and methods. They are available when an instance of a class is created in memory as an object. Properties are used to describe and query the characteristics of an object. For example, the Length and TrueColor properties of a Line object are used to specify that line's length and color. Properties can be designated as read-only.

Methods are used to manipulate and perform an action on an object. ActiveX allows you to define two types of methods: subroutines and functions. Subroutines never return a value; functions can return a single value. For example, the Delete and Copy methods are used to remove or duplicate an object in a drawing. The Delete method doesn't return a value, whereas the Copy method returns a new instance of an object.

1-3『 subroutines and functions 的概念是 VBA 里的，好在自己懂 VBA，好亲切。（2021-06-28）』

The objects in a COM library are typically unique, so the `vlax-dump-object` function can be used to list the properties and methods that a particular object supports. The following shows the syntax of the `vlax-dump-object` function:

1-2-3『

哇塞，`vlax-dump-object` 这个函数太有用了。录入主题卡片「函数收藏」。（2021-03-06）

跑了下块数据集合的属性和方法。

```c
(defun c:foo (/ curDoc blocks)
  (setq curDoc (vla-get-activedocument (vlax-get-acad-object))) 
  ; Gets the blocks collection 
  (setq blocks (vla-get-blocks curDoc)) 
  ; Creates a report header 
  (vlax-dump-object blocks T)
  (princ)
)
```

输出：

```
; IAcadBlocks: 图形中所有块的集合
;特性值:
;   Application (RO) = #<VLA-OBJECT IAcadApplication 00007ff7e34a3f10>
;   Count (RO) = 30
;   Document (RO) = #<VLA-OBJECT IAcadDocument 0000020b095090a8>
;   Handle (RO) = "1"
;   HasExtensionDictionary (RO) = 0
;   ObjectID (RO) = 59
;   ObjectName (RO) = "AcDbBlockTable"
;   OwnerID (RO) = 0
;支持的方法:
;   Add (2)
;   Delete ()
;   GetExtensionDictionary ()
;   GetXData (3)
;   Item (1)
;   SetXData (2)
```

[AutoLisp: vlax-dump-object (AutoLISP/ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-BCE56B30-54A6-42F9-8910-81AF2B7B9AA8)

』—— 已完成

```c
(vlax-dump-object obj [flag])
```

Here are its arguments:

1 obj. The obj argument is a value of the vla-object type, which is returned by a method or property, or is available as the var argument of the vlax-for function.

2 flag. The flag argument is an optional argument that allows you to specify whether the returned output lists only the properties or the properties and methods supported by an object. A value of T returns both supported properties and methods, whereas no value or a value of nil returns only the supported properties.

Here's an example that shows how to list the properties and methods of an object with the `vlax-dump-object` function:

```c
(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) 
#<VLA-OBJECT IAcadAcCmColor 000000002dcdd650> 
(vlax-dump-object clrObj T) 
; IAcadAcCmColor: AutoCAD AcCmColor Interface 
; Property values: 
;   Blue (RO) = 0 
;   BookName (RO) = "" 
;   ColorIndex = 0 
;   ColorMethod = 195 
;   ColorName (RO) = "" 
;   EntityColor = -1023410176 
;   Green (RO) = 0 
;   Red (RO) = 0 
; Methods supported: 
;   Delete () 
;   SetColorBookColor (2) 
;   SetNames (2) 
;   SetRGB (3) 
T
```

(RO) after a property name indicates that the property is read-only and the value cannot be changed. The number in the parentheses after each method listed in the Methods supported section of the output indicates the number of arguments that the method expects; no number in the parentheses indicates the method doesn't accept any argument values.

1『之前还真没注意到这 2 个细节：1）RO 表示只读。2）方法后面的数字表示入参的数量。（2021-06-28）』

#### 12.1.3 Getting and Specifying the Value of an Object's Property

The `vlax-get-property` and `vlax-put-property` functions are used to query and set the values of an object property. The `vlax-get-property` function returns the current value of the object property; the `vlax-put-property` function returns nil if the value was successfully assigned to the object's property. When the value of a property is changed with the `vlax-put-property` function, the object is updated immediately. Refer to the COM library's documentation for the type of value that will be returned or that the property expects. See the section「Using the AutoCAD COM Library」to learn how to access information on the AutoCAD COM library help.

The following shows the syntax of the `vlax-get-property` and `vlax-put-property` functions:

```c
(vlax-get-property obj 'prop) 
(vlax-put-property obj 'prop val)
```

Here are their arguments:

1 obj. The obj argument is a value of the vla-object type, which is returned by a method or property, or is available as the var argument of the vlax-for function.

2 'prop. The prop argument specifies the name of the particular property you want to query or set. The property name must be prefixed with an apostrophe. An apostrophe must be placed in front of the property name to let AutoLISP know it is a value that should not be evaluated.

3 val. The val argument specifies the new value to be assigned to the property.

Here are some examples that show how to get and set a property value of an object. In these examples, you work with the ColorMethod and ColorIndex properties of an AutoCAD True Color object:

```c
(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) 
; Sets the value of the ColorMethod property to acColorMethodByACI 
; acColorMethodByACI indicates that the color should 
; be based on an ACI color value 
(vlax-put-property clrObj 'ColorMethod acColorMethodByACI) 
nil 
; Gets the current value of the ColorIndex property 
; A value of 256 specifies that the color represents ByLayer 
(vlax-get-property clrObj 'ColorIndex) 
256 
; Releases the AutoCAD True Color object because it was created with 
; the vlax-create-object 
(vlax-release-object clrObj)
```

In the previous example, acColorMethodByACI is a constant variable value that is exposed as part of the AutoCAD COM library. This constant value tells AutoCAD you want to work with one of the standard 255 ACI colors, and not a True or Color Book color.

You can determine whether an object supports a specific property by using the `vlax-property-available-p` function. A value of T is returned if the object supports the specified property. The following shows the syntax of the `vlax-property-available-p` function. See the argument descriptions of the `vlax-get-property` function earlier in this section:

```c
(vlax-property-available-p obj 'prop)
```

#### 12.1.4 Invoking an Object Method

The `vlax-invoke-method` function is used to execute an object method and pass to that method any argument values that are expected. A value can be returned by the method through the executed `vlax-invoke-method` function or by reference to the variables passed to the method. Refer to the particular method's documentation for the type of values that can be passed or for an explanation of the values returned by the method. (See the section「Using the AutoCAD COM Library」later in this chapter to learn how to access information on the AutoCAD COM library help.)

The following shows the syntax of the vlax-invoke-method function:

```c
(vlax-invoke-method obj 'method [argN …])
```

Here are its arguments:

1 obj. The obj argument is a value of the vla-object type, which is returned by a method or property or is available as the var argument of the vlax-for function.

2 ‘method. The method argument is the name of the method you want to execute. The method name must be prefixed with an apostrophe. An apostrophe must be placed in front of the method name to let AutoLISP know it is a value that should not be evaluated.

3 argN. The argN argument is the value(s) to be passed to the method. If the argument you specify is meant to return a value, that argument must be prefixed with an apostrophe. The documentation in the AutoCAD Help system for the method will let you know if a value is passed back to the variable specified as an argument instead of returned by the function. For example, the `GetBoundingBox` method returns values to its two arguments that represent the minimum and maximum extents of an object. The code statement would look similar to `(vlax-invoke-method lineObj 'GetBoundingBox 'min 'max)`. See the AutoCAD COM library documentation for additional information.

Here is an example that shows how to invoke a method. This example sets the Red element of the RGB color to a value of 255 and the Blue and Green elements of the object to 0. The result would be a pure color of red if the color object was assigned to an object. The Red, Green, and Blue properties of an AutoCAD True Color object are read-only; the SetRGB method is used to assign new values to the three color elements of the object:

```c
(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) 
(vlax-invoke-method clrObj 'SetRGB 255 0 0) 
nil 
(vlax-release-object clrObj)
```

You can determine whether an object supports a method by using the `vlax-method-applicable-p` function. A value of T is returned if the object does support the specified method. The following shows the syntax of the `vlax-method-applicable-p` function. The arguments are the same as described earlier in this section:

```c
(vlax-method-applicable-p obj 'method)
```

#### 12.1.5 Working with Variants and Arrays

vla-object isn't the only new data type that you will have to understand when working with ActiveX. Many methods and properties use what is known as a variant. The variant data type is the chameleon of data types; it can represent any supported data type. A variant in AutoLISP is represented by the vla-variant data type. Arrays are yet another type of data that you will need to become familiar with. An array is represented by the vla-array data type and is similar to the AutoLISP list data type.

2『这里的 Variants and Arrays，做一张术语卡片。（2021-03-07）补充：此时才意识到，Variants 和 Arrays 是跟 vla-object 同一个抽象层次的东西。（2021-06-28）』—— 已完成

#### Making Variants

Most properties and methods return or expect values of a specific type, but there will be times when you will need to assign a property or pass a method a variant value. Some data structures can represent multiple values, such as a point or Xdata, and in these situations the AutoCAD COM library is designed to return or accept a variant value. You define a variant by using the `vlax-make-variant` function. The following shows the syntax of the `vlax-make-variant` function:

```c
(vlax-make-variant [val [type]])
```

Here are its arguments:

1 val. The val argument is the value to be assigned to the variant and is optional.

2 type. The type argument is an optional integer that specifies the data type that the value should represent. As an alternative, you can use a constant variable value that has the same meaning. Table 22.1 lists some of the most common data types and the integer and constant variable values you can use. Refer to the `vlax-make-variant` topic in the AutoCAD Help system for more supported values.

Table 22.1 Common data types used with the vlax-make-variant function

| Data type | Integer value | Constant variable value |
| --- | --- | --- |
| Integer | 2 | vlax-vbInteger |
| Double | 5 | vlax-vbDouble |
| String | 8 | vlax-vbString |

Here is an example that shows how to make a variant that holds an integer value of 5:

```c
(setq var (vlax-make-variant 5 vlax-vbInteger)) #<variant 2 5>
```

When neither the val nor the type argument is provided to the `vlax-make-variant` function, an empty variant is returned. The value and type of a variant can be returned using the `vlax-variant-value` and `vlax-variant-type` functions. The value assigned to a variant can't be changed, but the data type a variant represents can be changed using the `vlax-variant-change-type` function, making it possible to change an integer to a double or string. For example, you might want to change an integer or double value to a string so that it can be displayed to the user as part of a message or prompt string.

The following shows the syntax of the `vlax-variant-value`, `vlax-variant-type`, and `vlax-variant-change-type` functions:

```c
(vlax-variant-value variant) 
(vlax-variant-type variant) 
(vlax-variant-change-type variant type)
```

#### Defining Arrays

The array data type is similar to the AutoLISP list data type, but typically an array is made up of a specified number of elements. You will remember that a list can hold any number of elements. A common use for arrays with the AutoCAD COM library is to represent a point list. Arrays can also be used to pass multiple objects to a method or for times when you want to return more than one value from a custom function.

The `vlax-make-safearray` function is used to create a new array based on a specific data type and number of elements. The following shows the syntax of the `vlax-make-safearray` function:

```c
(vlax-make-safearray type '(lbound. ubound) ['(lbound. ubound)])
```

Here are its arguments:

1 type. The type argument is an integer or equivalent constant variable that represents the data type of the elements within the array. These are the same data types that the `vlax-make-variant` function supports. Refer to the `vlax-make-safearray` topic in the AutoCAD Help system for supported values.

2 '(lbound. ubound). The lbound part of the argument is an integer that represents the lower element of the array, typically 0. The ubound part of the argument is an integer that represents the upper element of the array. If you want to specify an array of three elements, set lbound to 0 and ubound to 2.

1-3『

[AutoLiso: vlax-make-safearray (AutoLISP/ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-E0D40331-096B-4A52-A0D7-10204829C4A6)

修改块属性值的时候会用到的方法应该跟 `vlax-make-safearray` 有关：[AutoLisp: GetAttributes Method (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-3E8E1756-F45D-4CCE-838B-00FBC0374278)

```c
;; Change the value of the attribute
;; Note: There is no SetAttributes. Once you have the variant array, you have the objects.
;; Changing them changes the objects in the drawing.
(vla-put-TextString (vlax-safearray-get-element varAttributes 0) "NEW VALUE!")
```

』

NOTE 22.1: The optional `['(lbound. ubound)]` argument allows you to define a matrix. For information on matrices, see the `vlax-tmatrix` function in the AutoCAD Help system and the TransformBy method in the AutoCAD COM library.

Here are examples that define arrays:

```c
; Array of three strings 
(setq arStrs (vlax-make-safearray vlax-vbString '(0. 2))) 
#<safearray…> 
; 2D point (array of two doubles) 
(setq pt2D (vlax-make-safearray vlax-vbDouble '(0. 1))) 
#<safearray…>
```

After an array has been defined, you can add values to the elements within the array by using the `vlax-safearray-put-element` function. You can retrieve values within an array by using the `vlax-safearray-get-element` function.

The following shows the syntax of the `vlax-safearray-put-element` and `vlax-safearray-get-element` functions:

```c
(vlax-safearray-put-element array idx val) 
(vlax-safearray-get-element array idx)
```

Here are its arguments:

1 array. The array argument is a value of the vla-array data type, such as that returned by the `vlax-make-safearray` function.

2 idx. The idx argument is an integer that represents an element within the array. The value cannot be less than the lower or greater than the upper element of the array.

3 val. The val argument is the value that is to be assigned to the element in the array.

Here are examples that assign values to and get values from the arrays defined in the earlier examples:

```c
; Assign strings to a three-element array 
(vlax-safearray-put-element arStrs 0 "Qty") 
"Qty" 
(vlax-safearray-put-element arStrs 1 "Model") 
"Model" 
(vlax-safearray-put-element arStrs 2 "Description") 
"Description" 
; Assign double/real values to a two-element array 
(vlax-safearray-put-element pt2D 0 0.0) 
0.0 
(vlax-safearray-put-element pt2D 1 5.25) 
5.25 
; Get the first element in an array 
(vlax-safearray-get-element pt2D 0) 
0.0
```

To create a 2D or 3D point array, you can use the `vlax-3d-point` function. Or you can assign multiple values to an array based on the values of a list with the `vlax-safearray-fill` function. Here are examples that use the `vlax-3d-point` and `vlax-safearray-fill` functions:

```c
; 2D point 
(setq pt2D (vlax-3d-point 0.0 5.25)) 
; 3D point 
(setq pt3D (vlax-3d-point 0.0 5.25 1.0)) 
; Adds three strings to a three-element array 
(vlax-safearray-fill arStrs '("Qty" "Model" "Description"))
```

Table 22.2 lists some additional functions that can be helpful when working with arrays. For more information on the functions mentioned in the table, see the AutoCAD Help system.

Table 22.2 Additional array functions

| Function | Description |
| --- | --- |
| vlax-safearray-type | Returns an integer that represents the data type of the values contained in an array |
| vlax-safearray-get-dim  | Returns an integer that represents the number of elements in an array |
| vlax-safearray-get-l-bound | Returns an integer that represents the index of the lower element in an array |
| vlax-safearray-get-u-bound  | Returns an integer that represents the index of the upper element in an array |
| vlax-safearray->list | Returns a list containing the values of all elements in an array |

1-2-3『 

`vlax-safearray-get-l-bound`、`vlax-safearray-get-u-bound`、`vlax-safearray->list` 这三个函数，可以查看块的属性数据。趁此机会，一鼓作气实现了生成块后直接修改属性值（之前已经通过原始的 entityData 实现过，这里的方法更高层，即更抽象）。很舒服。（2021-03-07）

参考：

[AutoLisp: InsertBlock Method (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-17F86FDD-B7FC-4F43-9F16-B4958F73A66D)

[AutoLisp: GetAttributes Method (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-3E8E1756-F45D-4CCE-838B-00FBC0374278)

```c
; 2021-03-07
(defun InsertBlockUtils (insPt blockName layerName / acadObj curDoc insertionPnt modelSpace blockRefObj blockAttributes)
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
  (vla-put-TextString (vlax-safearray-get-element blockAttributes 1) "JC1101-50-2J1")
  ;(vla-ZoomAll acadObj) 
  (princ)
)
```

这里有个小细节，有两种方法可以获取块属性的数据：1）本书前面小结的信息，通过函数 `vlax-invoke-method` 调块对象的方法 `GetAttributes`。2）上面官方文档例子里的方法，直接用方法 `vla-GetAttributes`。最开始没成功实现，是误以为这里获取的数据就是块属性数据集，但它其实是一个「变体」数据类型，得通过方法 `(vlax-variant-value variant)` 获得的值才是自己想要的块属性数据（arrays）。（2021-03-07）

』

### 12.2 Importing COM Libraries

Although you can access the properties and methods of an object using the functions covered in the「Specifying Properties and Invoking Methods」section, importing a COM library can make coding easier. When you import a COM library, that library defines an AutoLISP function for the properties and methods of each class in the library. The newly defined functions that result from importing a COM library reduce the amount of code that needs to be written.

For example, the `vla-get-red` function can be used instead of the `vlax-get-property` function to get the current value of the Red property of an AutoCAD True Color object. The same is true with methods; `vla-delete` is the equivalent of using the `vlax-invoke-method` function with the Delete method name as an argument. The following two code statements produce the same result:

```c
(vlax-get-property clrObj 'Red) 
(vla-get-red clrObj)
```

1-3『这里的信息正好解答了之前的疑惑，为啥修改块属性值有 2 种实现方式。原来官方文档里的方法是「importing a COM library」。补充到前面的「函数收藏」主题卡片里。（2021-03-07）』

The properties and methods exposed by the AutoCAD COM library can be imported into a current drawing with the `vl-load-com` function. However, if you want to import the functions of another COM library for use with AutoLISP you must use the `vlax-import-type-library` function. The `vlax-import-type-library` function returns T if the COM library was successfully imported. An error is returned if the COM library couldn't be imported.

The following shows the syntax of the `vlax-import-type-library` function:

```c
(vlax-import-type-library :tlb-filename filename 
                          [:methods-prefix me_prefix 
                          :properties-prefix prop_prefix 
                          :constants-prefix con_prefix] 
)
```

Here are its arguments:

1 filename. The filename argument represents the path to and the filename of the COM library to be imported.

2 `me_prefix`, `prop_prefix`, and `con_prefix`. These arguments are optional strings that represent the prefix to be appended to the property, method, and constant names in the COM library being imported to ensure the names are unique from other imported libraries.

Here is an example that shows how to import the COM library for the Windows Shell object:

```c
(vlax-import-type-library :tlb-filename "c:\\windows\\system32\\wshom.ocx" 
                          :methods-prefix "wshm-" 
                          :properties-prefix "wshp-" 
                          :constants-prefix "wshk-" 
)
```

Although you can import a COM library more than once, you should avoid doing so, since multiple imports can add to the time it takes for a custom function to execute. The following example shows how you can use a global variable to determine whether the COM library associated with the Windows Shell object has already been imported into the current session:

```c
; Imports the Windows Host Scripting Library 
(if (= wshLibImported nil) 
  (progn 
    (vlax-import-type-library :tlb-filename "c:\\windows\\system32\\wshom.ocx" 
                              :methods-prefix "wshm-" 
                              :properties-prefix "wshp-" 
                              :constants-prefix "wshk-" ) 
    (setq wshLibImported T) 
  ) 
  (princ) 
)
```

1-2『

作者建议不要频繁的「COM library」，会减慢 CAD 运行的效率。这里也给出了解决方案，用一个全局变量做标记，其实这种场景其他地方也会遇到，这个做「标记」的方法很有借鉴意义。（2021-03-07）

```c
(if (= *comLibraryStatus* nil) 
  (progn 
    (vl-load-com)
    (setq *comLibraryStatus* T) 
  )
)
```

』

### 12.3 Using the AutoCAD COM Library

Once the AutoCAD COM library has been imported, you can use the newly exposed functions to do the following:

1 Access the objects associated with the AutoCAD application and current drawing.

2 Get the graphical and nongraphical objects stored in the current drawing.

3 Perform geometric calculations.

4 Register reactors and monitor changes made to a drawing or actions performed by the user.

1『上面的 4 个块功能都可以深挖，这里信息密度真大。（2021-03-07）』

TIP: Before you use the AutoCAD COM library, make sure that you execute the `vl-load-com` function to ensure the library has been imported.

The classes in the AutoCAD COM library are organized using a hierarchy. The AutoCAD application is at the top, followed by the drawings (or documents) opened, and then the objects in a drawing. Once you have a drawing object, you can then access the nongraphical objects stored in the drawing. Graphical objects that have been placed in model space or on a layout are accessed through the special named blocks `*ModelSpace` and `*PaperSpace0` of, which are stored in the Blocks or Layouts collection. A drawing can contain more than one `*PaperSpace` block; each successive paper space block name in the drawing is incremented by 1.

NOTE 22.3: You can access the AutoCAD application object from most objects in the AutoCAD COM library by using the Application property, which can be accessed with the `vla-get-application` function.

You can learn about the classes in the AutoCAD COM library by using the AutoCAD Object Model in the AutoCAD Help system. The AutoCAD Object Model can be found by going to http://help.autodesk.com/view/ACD/2015/ENU/files/homepage_dev.htm and clicking the AutoCAD Object Model link. The AutoCAD Object Model (see Figure 22.1) shows the hierarchy of the AutoCAD COM library structure.

Figure 22.1 Hierarchy of the AutoCAD COM library

3『新版：[AutoLisp: Object Model (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-A809CD71-4655-44E2-B674-1FE200B9FE30)。』

When you click the object model, the reference topic for the associated class/object opens. The Help reference page provides information on how an object can be created, along with the properties and methods supported by the object. The content is intended primarily for the VBA programmer, but it is still very useful if you're working with the AutoCAD COM library in AutoLISP.

For the most part, adding `vla-` as a prefix for a method name or `vla-put-` or `vla-get-` as a prefix for a property name is all that is needed to convert the information contained in the VBA documentation for use with AutoLISP. (Remember that you must use `vl-load-com` to ensure that the AutoCAD COM library has been imported before you can use it.) A majority of the reference topics for object properties and methods also contain example code for use with AutoLISP. You can copy and modify the example code as needed. The ActiveX Developer's Guide can also help you learn more about the AutoCAD COM library.

You can access both the ActiveX Reference and ActiveX Developer's topics by using the AutoCAD Object Library Reference and Developer's Guide links in the ActiveX/VBA section of the Developer homepage in the AutoCAD Help system.

TIP: When you are using the Visual LISP® Editor, you can highlight the name of an imported function in the editor window and press Ctrl+F1 to open the related topic in the ActiveX Reference. Using this approach, you open the acadauto.chm file to the topic that discusses the object, method, or property.

#### 12.3.1 Accessing the AutoCAD Application and Current Drawing Objects

Once the AutoCAD COM library has been imported with the `vl-load-com` function, you can use the `vlax-get-acad-object` function to get the AcadApplication object that represents the AutoCAD application. As I mentioned earlier, the AutoCAD application object is the topmost object in the hierarchy that is the AutoCAD COM library. To learn which methods and properties an AcadApplication object supports, you can use the `vlax-dump-object` function with the value returned by the `vlax-get-acad-object` function. Here is an example that shows how to use the `vlax-get-acad-object` function:

```c
; Gets the AutoCAD application object 
(setq acad (vlax-get-acad-object))
```

The AcadApplication object contains a property named ActiveDocument, which returns an AcadDocument object that represents the current drawing. Use the `vla-get-activedocument` function to get the current drawing object. Here is an example:

```c
; Gets the current drawing 
(setq curDoc (vla-get-activedocument acad))
```

#### 12.3.2 Working with Graphical and Nongraphical Objects in the Current Drawing

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

1 Create a LSP file named ActiveX.lsp in the MyCustomFolders folder within the Documents (or My Documents) folder, or in the location you are using to store the LSP files.

2 In Notepad (Windows) or TextEdit (Mac OS), type the following in the text editor area:

```c
; Creates a new layer and/or sets a layer current 
(defun CreateLayer-ActiveX (lyrName layColor docObj / layerObj) 
  (if (= (vl-catch-all-error-p (vl-catch-all-apply 'vla-item '((vla-get-layers docObj) "Hatch"))) T) 
    (progn 
      ; Creates the layer 
      (setq layerObj (vla-add (vla-get-layers docObj) lyrName)) 
      ; Sets the color of the layer 
      (vla-put-color layerObj layColor) 
    ) 
  ) 
  ; Sets the layer current 
  (vla-put-activelayer docObj (vla-item (vla-get-layers docObj) lyrName)) 
  (princ) 
)
```

3 Save the file and then load it into AutoCAD.

4 At the Command prompt, type the following to test the function:

```c
(setq acad (vlax-get-acad-object)) 
(setq curDoc (vla-get-activedocument acad)) 
(createlayer-activex "NewLayer" 4 curDoc)
```

A new layer named NewLayer is added to the drawing, assigned the color 4 (Cyan), and set as current. You can see that the new layer has been created by using the layer command and the Layer Properties Manager.

Adding graphical objects to a drawing with ActiveX is different from what you have done previously when using the command, entmake, and entmakex functions. When using ActiveX, you must specify where an object should be created — the methods of the AutoCAD COM library are not contextually driven. You must explicitly work in model space or paper space.

2『关键知识点：用 ActiveX 生成实体对象，一定要指定是加到「哪个」collection 里去。（2021-06-28）』

The following exercise defines a function that prompts the user for two points: the opposite corners of a rectangle. User input is handled using the methods available through the Utility object. The two points specified are used to define the four corners of a rectangle, by making an array of eight elements and then populating the XY pairs of each point defined for the rectangle. The array is used to specify the vertices of the lightweight polyline to add in the model space of the current drawing. Once the lightweight polyline is added, the Closed property is used to close the lightweight polyline.

1 Open the ActiveX.lsp file in Notepad (Windows) or TextEdit (Mac OS).

2 Click after the last closing parenthesis of the createlayer-activex function and press Enter twice.

3 In the text editor area, type the following:

```c
; Creates a rectangle on the Obj layer 
(defun c:DrawRectangle_ActiveX ( / docObj curLayer vPt1 vPt2 ptList lwPlineObj) 
  ; Gets a reference to the current drawing 
  (setq docObj (vla-get-activedocument (vlax-get-acad-object))) 
  ; Gets the active layer 
  (setq curLayer (vla-get-activelayer docObj)) 
  ; Creates and/or sets the Obj layer current 
  (CreateLayer-ActiveX "Obj" acGreen docObj) 
  ; Prompts the user for a point 
  (setq vPt1 (vla-getpoint (vla-get-utility docObj) nil "\nSpecify first corner: ")) 
  ; Prompts the user for the opposite corner 
  (setq vPt2 (vla-getcorner (vla-get-utility docObj) vPt1 "\nSpecify opposite corner: ")) 
  ; Creates an array of four 2D points 
  (setq ptList (vlax-make-safearray vlax-vbDouble '(0. 7))) 
  (vlax-safearray-fill ptList (list 
                                ; Point 1 
                                (vlax-safearray-get-element (vlax-variant-value vpt1) 0) 
                                (vlax-safearray-get-element (vlax-variant-value vpt1) 1) 
                                ; Point 2 
                                (vlax-safearray-get-element (vlax-variant-value vpt1) 0) 
                                (vlax-safearray-get-element (vlax-variant-value vpt2) 1) 
                                ; Point 3 
                                (vlax-safearray-get-element (vlax-variant-value vpt2) 0) 
                                (vlax-safearray-get-element (vlax-variant-value vpt2) 1) 
                                ; Point 4 
                                (vlax-safearray-get-element (vlax-variant-value vpt2) 0) 
                                (vlax-safearray-get-element (vlax-variant-value vpt1) 1) ) 
                              ) 
  ; Gets a reference to the current space in AutoCAD 
  (if (= (vla-get-activespace docObj) acModelSpace) 
    (setq space (vla-get-modelspace docObj)) 
    (setq space (vla-get-paperspace docObj)) 
  ) 
  ; Draws the rectangle using a lightweight polyline 
  (setq lwPlineObj (vla-addlightweightpolyline space ptList)) 
  ; Closes the polyline 
  (vla-put-closed lwPlineObj :vlax-true) 
  ; Restores the previous active layer 
  (vla-put-activelayer docObj curLayer) 
  (princ) 
)
```

1『体会到：1）生成块对象，ActiveX 比原生的数据集方便很多。2）但生成图形对象，原生的数据集又比 ActiveX 方便很多，哈哈。（2021-03-07）』

4 Save the file and then reload it into AutoCAD.

5 At the Command prompt, type `drawrectangle_activex` and press Enter to test the function.

6 At the Specify first corner: prompt, specify a point in the drawing area.

7 At the Specify opposite corner: prompt, specify a point in the drawing area that is the opposite corner of the rectangle. A new layer named Obj is added to the drawing and a new lightweight polyline is drawn based on the points specified.

The completed exercise can be found in the `ch22_activex_complete.lsp` file, which you can download from this book's web page.

#### 12.3.3 Monitoring Events with Reactors

1『之前一直想了解的「监听事件」相关知识来了。（2021-03-07）』

Reactors allow you to monitor for events that occur in a drawing or an application and are one of the main advantages of using ActiveX with AutoLISP. Some of the events that you can monitor for include starting or ending of a command, attaching an Xref, or inserting a block. Using reactors, you can ensure certain objects are placed on a specific set of layers without needing to switch layers before creating an object.

In this exercise, you will create two custom functions that AutoCAD will call when a command is started, canceled, ends, or fails. You will be monitoring the hatch, bhatch, and gradient commands. When any one of those commands is started, AutoCAD sets the Hatch layer as current and restores the previous layer if the command ends, fails, or is canceled.

1 Open the ActiveX.lsp file in Notepad (Windows) or TextEdit (Mac OS).

2 Click after the last closing parenthesis of the `drawrectangle_activex` function and press Enter twice.

3 In the text editor area, type the following:

```c
; Register the Custom command reactors 
(if (= *rctCmds* nil) 
  (setq *rctCmds* 
    (vlr-command-reactor nil 
      '((:vlr-commandCancelled. apc-cmdAbort) 
        (:vlr-commandEnded. apc-cmdAbort) 
        (:vlr-commandFailed. apc-cmdAbort) 
        (:vlr-commandWillStart. apc-cmdStart)) 
    ) 
  ) 
  (princ) 
) 
; Custom function executed when a command is 
; cancelled, ends, or fails 
(defun apc-cmdAbort (arg1 arg2) 
  ; Restore the previous layer 
  (if (/= *gClayer* nil) 
    (setvar "clayer" *gClayer*) 
  ) 
  ; Clear the global variable 
  (setq *gClayer* nil) 
  (princ) 
) 
; Custom function executed when a command is started 
(defun apc-cmdStart (arg1 arg2 / docObj layerObj) 
  ; Store the current layer 
  (setq *gClayer* (getvar "clayer")) 
  ; Get a reference to the current drawing 
  (setq docObj (vla-get-activedocument (vlax-get-acad-object))) 
  ; Check to see which command has been started 
  (cond 
    ; HATCH, BHATCH or GRADIENT command was started 
    ((or (= (car arg2) "HATCH") 
         (= (car arg2) "BHATCH") 
         (= (car arg2) "GRADIENT")) 
    ; Create and/or set the Hatch layer current 
    (CreateLayer-ActiveX "Hatch" acRed docObj)) 
  ) 
  (princ) 
)
```

4 Save the file and then reload it into AutoCAD.

5 At the Command prompt, type drawrectangle-activex and press Enter.

6 Follow the prompts that are displayed.

7 the Command prompt, type hatch and press Enter.

8 At the Pick internal point or [Select objects/Undo/seTtings]: prompt, specify a point inside the rectangle that was drawn in steps 4 and 5.

9 Press Enter to end the hatch command. A new layer named Hatch is added to the drawing and the new hatch object is placed on that layer.

The completed exercise can be found in the `ch22_activex_complete.lsp` file, which you can download from this book's web page.

#### Learning about Other ActiveX-Related Functions

As I mentioned earlier, this chapter provides an introduction to the various concepts required to get started with ActiveX in AutoLISP. There is a wide range of additional AutoLISP functions that I wasn't able to cover in this chapter. The names of these functions begin with the prefixes `vla-`, `vlax-` , and `vlr-`. You can learn more about the functions in the AutoCAD Help system by browsing to http://help.autodesk.com/view/ACD/2015/ENU/files/homepage_dev.htm, clicking the Functions By Name And Feature Reference link, and then using the links in the Visual LISP Extensions for AutoLISP (Windows only) section.

### 12.4 Leveraging the Windows and Microsoft Office COM Libraries

The Microsoft ecosystem is full of hidden gems that can increase your productivity and improve everyday workflows. Many programs that are available for free or for purchase let you create proposals or manipulate information in a database, but Windows and Microsoft Office allow you to leverage what they do best by using the COM libraries that they expose. There aren't many companies that allow you to manipulate or access their programs programmatically like Microsoft does, so take advantage of these benefits whenever possible.

1-3『作者的意思是 Microsoft Office COM Libraries 给开发者的权限很大，可以做很多事情。最近也在 GitHub 上找到一个操作 Excel 的三方库（github.autolisp => cathedral），需仔细研读。（2021-06-28）』

Using the COM libraries for Windows and Microsoft Office, you can accomplish the following:

1 Create desktop shortcuts, expand environment variables, or even launch an external application.

2 Create and print documents using Microsoft Word.

3 Create, manipulate, and print spreadsheets using Microsoft Excel.

4 Create email messages and access contact lists using Microsoft Outlook.

5 Access and manipulate data in a database using Microsoft Access.

For specific information on each of these COM libraries, refer to the documentation that Microsoft publishes with Windows and the Microsoft Office application you are interested in working with. Your favorite Internet search engine will also be of help; search on the keywords「Windows Shell object documentation」or「Microsoft Office 2013 Release Developers」to get started.

#### 12.4.1 Accessing the Windows Shell Object

The Windows Shell object is the graphical interface that you or the user interact with when accessing an application or the files stored on the workstation. With the Windows Shell object, you can take these actions:

1 Create shortcuts on the desktop or in a file folder.

2 Access the files on your workstation or a removable/network drive.

3 Launch an application or URL.

4 Work with environment variables.

You can create a reference to a Windows Shell object using the following code:

```c
(vlax-create-object "WScript.Shell")
```

Don't forget to release an object returned by the `vlax-create-object` function from memory after you are done with it by using `vlax-release-object`. Here are two custom functions that demonstrate some of the functionality exposed by the Windows Shell object:

```c
; Creates a new shortcut 
; Usage: (CreateShortcut "c:\\mylink.lnk" "c:\\temp\\myfile.lsp") 
; Revise "c:\\mylink.lnk" to a location for which you have write access and change 
; "c:\\temp\\myfile.lsp" to a valid filename on your workstation. 
(defun CreateShortcut (lnkName Target / wshShell shortcut) 
  ; Create a reference to Window Scripting Shell Object 
  (setq wshShell (vlax-create-object "WScript.Shell")) 
  ; Expand the string and any variables in the string 
  (setq shortcut (vlax-invoke-method wshShell 'CreateShortcut lnkName)) 
  (vlax-put-property shortcut 'TargetPath Target) 
  (vlax-invoke-method shortcut 'Save) 
  ; Release the Window Scripting Shell Object 
  (vlax-release-object wshShell) 
  (princ) 
) 
; Shows how to use expanding environment strings 
; Usage: (ExpEnvStr "%TEMP%\\MYDATA") 
; Results of sample: "C:\\Users\\Lee\\AppData\\Local\\Temp\\MYDATA" 
(defun ExpEnvStr (strVal / wshShell strValRet) 
  ; Create a reference to Window Scripting Shell Object 
  (setq wshShell (vlax-create-object "WScript.Shell")) 
  ; Expand the string and any variables in the string 
  (setq strValRet (vlax-invoke-method wshShell 'ExpandEnvironmentStrings strVal)) 
  ; Release the Window Scripting Shell Object 
  (vlax-release-object wshShell) 
  strValRet 
)
```

#### Using the Correct Microsoft Office Release

Microsoft Office and AutoCAD are supported on both 32- and 64-bit platforms. However, Microsoft Office 32-bit can be installed on Windows 64-bit whereas AutoCAD 32-bit cannot. Many companies install only Microsoft Office 32-bit, because there is less support for 64-bit add-ons for Microsoft Office applications than for 32-bit add-ons. Although this typically isn't an issue, the problem comes when you try to use ActiveX to talk to any of the Microsoft Office applications from AutoCAD. AutoCAD 64-bit won't allow you to import/access 32-bit database drivers or COM libraries, so you need to make sure your workstation is configured correctly by having the proper release of Microsoft Office installed.

The following code helps you locate the Microsoft Office release that a user might have installed on their machine, whether they are using Office 32- or 64-bit. The code uses a function named `expenvstr`, which you saw in the「Leveraging the Windows and Microsoft Office COM Libraries」section.

```c
; Checks for a specific version of Microsoft Office 
; Microsoft Office 2013 - 15 
; Microsoft Office 2010 - 14 
; Microsoft Office 2007 - 12 
; Microsoft Office 2003 - 11 
; Microsoft Office 2000 - 10 
(defun Get-MSOfficePath (ver / ) 
  ; Office version 
  (setq *MSOfficeVer* (itoa ver)) 
  ; Office 32-bit path on Windows 64-bit 
  (setq *MSOfficePathx86* 
    (strcat (ExpEnvStr "%PROGRAMFILES(X86)%") "\\Microsoft Office\\Office" (itoa ver)) 
  ) 
  ; Office path (Windows 32- or 64-bit) 
  (setq *MSOfficePath* 
    (strcat (ExpEnvStr "%PROGRAMFILES%") 
            (cond ((= ver 15)(strcat "\\Microsoft Office " (itoa ver) "\\root\\Office" (itoa ver))) 
              (strcat "\\Microsoft Office\\Office" (itoa ver))) 
    ) 
  ) 
  ; Return 32-bit location first and then 64-bit 
  (cond ((/= (findfile *MSOfficePath*) nil) (strcat *MSOfficePath* "\\") ) 
    ((/= (findfile *MSOfficePathx86*) nil) (strcat *MSOfficePathx86* "\\") ) 
    ("") 
  ) 
) 
; Example of using the custom function 
(Get-MSOfficePath 15) 
"C:\\Program Files\\Microsoft Office 15\\root\\Office15\\"
```

#### 12.4.2 Working with Microsoft Office

The Microsoft Word object allows you to create an instance of Microsoft Word, which can then be used to create or open a document. Once a document has been created or opened, you can step through and manipulate the content of the document or print the document to an available system printer.

A reference to a Microsoft Word object can be created using the following code:

```c
(vlax-create-object "Word.Application")
```

If more than one version of Microsoft Office is installed, you can specify which release of the product to start by adding a version number to the program ID passed to the `vlax-create-object` function. For the available version numbers, see the「Using the Correct Microsoft Office Release」sidebar.

You can use the following code to create a reference to the Microsoft Excel object:

```c
(vlax-create-object "Excel.Application")
```

You can find the custom functions that show how to work with the Microsoft Word and Excel objects in the `ch22_mswin_office.lsp` file that you can download from this book's web page. The LSP file contains the following custom functions:

1 `createmsworddoc`. The `createmsworddoc` function creates a new Word document and saves it with the name `ch22_apc_word_sample.doc` to the MyCustomFiles folder. The new Word document file is populated with information about some of the nongraphical objects in the current drawing.

2 `printmsworddoc`. The `printmsworddoc` function opens the `ch22_apc_word_sample.doc` file that was created with the `createmsworddoc` function and placed in the MyCustomFiles folder. The Word document file is then printed using the default system printer.

3 `extractattributestoexcel`. The `extractattributestoexcel` function creates a new spreadsheet file named `ch22_attributes.xls` in the MyCustomFiles folder. The handle, tag, and text string for each attribute in the block references of the current drawing are extracted to columns and rows in the spreadsheet. Open the `ch22_building_plan.dwg` file in AutoCAD before executing the function.

1-2『哎呦，上面的函数直接把块的数据导入到「正宗」excel 里，之前自己实现的仅仅是导入到纯文本 csv 中，纯文本是没格式的。上面作者给的样本源码需要好好研读一下。（2021-03-07）』—— 未完成

4 `updateattributesfromexcel`. The `updateattributesfromexcel` function reads the information from the spreadsheet file named `ch22_attributes.xls` in the MyCustomFiles folder. The extracted handle in the spreadsheet is used to get the attribute reference and then update the tag and text string value that is present in the spreadsheet. Since handles are unique to each drawing, you must open the original drawing that the attributes were extracted from. Make changes to the third column in the spreadsheet file, such as C2436 to CC2436, before opening the `ch22_building_plan.dwg` file in AutoCAD and executing the function.

Along with custom functions that work with Microsoft Word and Excel, there are also a few functions that demonstrate how to connect to a Microsoft Access database (MDB) file using Database Access Object (DAO) and ActiveX Data Object (ADO). The database library you use depends on which release of Office you are using. You can find two custom functions that access an MDB file in the `ch22_mswin_office.lsp` file that you can download from this book's web page.

1『意外收获，这里有如何直接跟 Microsoft 连接的信息。（2021-03-07）』

The LSP file contains the following custom functions:

1 `accessdatabasedao`. The `accessdatabasedao` function makes a connection to the Access database `ch22_employees.mdb`, located in the MyCustomFiles folder. Once a connection to the database is made, the records in the Employees table are read and modified. Use this function when working with Access 2007 and earlier.

2 `accessdatabaseado`. The `accessdatabaseado` function makes a connection to the Access database `ch22_employees.mdb`, located in the MyCustomFiles folder. Once a connection to the database is made, the records in the Employees table are read and modified. Use this function when working with Access 2007 and later.

## 0213. Implementing Dialog Boxes (Windows only)

The goal of any program should be to make end users be productive and feel empowered without getting in their way. Your decisions about the number of options and how they are presented can make or break a custom function. Include too many, and the user becomes frustrated while responding to prompts about options that aren't used frequently; too few, and the usefulness of the custom function suffers. Dialog boxes allow users to see values that might normally be hidden behind a set of prompts and provide input for only those options they are interested in changing. A dialog box can also be used to combine multiple functions into a single, easy-to-use interface.

1『上面的信息表示，A dialog box 真的可以做很多事情，哈哈。（2020-09-15）』

For example, consider the difference between the insert command, which displays the Insert dialog box, and the -insert command, which displays a series of options at the Command prompt. The insert command allows you to explode a block upon insert and use geographical data without affecting the prompt sequence or functionality of the -insert command. In this chapter, you will learn to implement dialog boxes for use with AutoLISP® programs.

### 13.1 What Is Dialog Control Language?

Dialog Control Language (DCL) is the technology used to lay out and design dialog boxes that can be used with AutoLISP programs. Support for DCL was originally added to Autodesk® AutoCAD® R11 and has remained essentially unchanged through AutoCAD 2015. Dialog boxes are defined and stored in ASCII text files with a .dcl extension. Once a DCL file has been created, AutoLISP can then load and display the dialog contained in the DCL file. After the dialog is displayed, AutoLISP is used to control what happens when the user clicks or otherwise manipulates the controls in the dialog box.

A DCL file can contain multiple dialog-box definitions. Each dialog box and control is defined through the use of a tile. The appearance of a tile is affected by what are known as attributes — think of attributes as the properties of a drawing object.

With the exception of the tile that defines the dialog box (the dialog tile), tiles typically start with a colon followed by the name of the tile type you want to place on the dialog box. The dialog tile must start with a user-defined name that is unique in the DCL file; this name is used to display the dialog box in the AutoCAD drawing environment. A pair of curly brackets that contain the attributes of the tile typically follows the name or type of a tile. Each attribute must end with a semicolon.

In addition to attributes, some tiles contain nested tiles, which are placed within a tile's curly brackets. Some tile names aren't followed by a pair of curly brackets because they don't support attributes; these tiles are known as subassemblies. Subassemblies help you implement standardized tile groupings. The OK and Cancel button tiles used in most dialogs created with DCL are examples of subassemblies.

1『语法汇总：1）各个 tile 是以冒号 `:` 开头的，无论是弹窗还是按钮之类的。2）tile 后面紧跟着 `{}`，跟对象语法一样，里面全是这个 tile 的属性，各个属性是以分号 `;` 结束的。不过有些 tile 不支持属性（被称为 subassemblies），那么后面就没有 `{}`。3）tile 里是可以嵌套 tile 的。（2020-10-08）』

Listing 23.1 shows an example of a dialog box definition that could be used as part of an alternative to the message box that is automatically displayed with the alert function. Remember, the alert function displays a message box with an OK button only.

Listing 23.1: Alternative message box

```c
/* Example message box Created on: 5/11/14 */ 
ex_alert : dialog { 
  label = "Title"; 
  key = "dlg_main"; 
  : text { 
    // Custom message 
    key = "msg"; 
    label = "Custom message here."; 
  } 
  ok_cancel; // Subassembly 
}
```

1『

在 lisp 文件里调用这个 box。

```c
; get the current file direction
(defun c:dcltest (/ dcl_id)
  (setq dcl_id (load_dialog (strcat "D:\\dataflowcad\\" "dataflow.dcl")))
  (if (not (new_dialog "ex_alert" dcl_id))
    (exit)
  )

  (start_dialog)
  (unload_dialog dcl_id)
)
```

』


Figure 23.1 shows what the alternative message box looks like when loaded into the AutoCAD drawing environment. A DCL file can also contain comments, which are prefixed with // or located between the character groupings /* and */. Both comment styles are shown in Listing 23.1.

---

#### Modernized DCL Alternatives

DCL has remained unchanged since AutoCAD R12, which is great from a compatibility perspective but not from a technology point of view. The controls that you can use on a dialog box defined with DCL will seem limited when you consider the countless controls that are available in Windows and Windows-based programs. Although the DCL that comes with AutoCAD is limited, there are a few alternatives that you can use to enrich the dialog boxes you create.

Here are the two DCL alternatives that I am aware of:

1 ObjectDCL — A technology that must be licensed from DuctiSoft ([ObjectDCL](http://objectdcl.com/))

2 OpenDCL — An open source application based on the ObjectDCL application; OpenDCL can be downloaded from [OpenDCL](https://opendcl.com/wordpress/).

1-2『感觉是捡到金子了，这 2 个做交互界面的工具太赞了，一定要去研读。（2020-10-08）』

ObjectDCL and OpenDCL allow you to implement modern Windows and third-party controls in an AutoLISP custom dialog box. You can use tree view, data grid, and HTML viewer controls, among many others. Both software solutions also provide WYSIWYG (what you see is what you get) design capabilities through their dialog-box editors.

AutoCAD Managed.NET and the ObjectARX APIs provide alternatives for creating custom AutoLISP functions that display custom dialog boxes created with Microsoft's Windows Presentation Foundation (WPF) and Microsoft Foundation Class (MFC). Developing your own dialog boxes using WPF and MFC can take additional time (compared to ObjectDCL or OpenDCL), but you own all the source code and don't need to worry about external dependencies.

---

### 13.2 Defining and Laying Out a Dialog Box

DCL files can be created and edited using Notepad, the Visual LISP® Editor, or whichever editor you are using for LSP files. Although you can use Notepad, the Visual LISP Editor offers a few advantages over Notepad for working with DCL files. It supports color syntax as it does with LSP files, but it also has a built-in DCL preview feature. Without the Visual LISP Editor's DCL preview feature, you must write an AutoLISP program that will at least load a DCL file and display a dialog box in the AutoCAD drawing environment to see the final appearance of a dialog box.

---

#### Simplifying User Interaction and Option Presentation

Have you ever sat and scratched your head in hopes of deciphering the options displayed as part of a prompt string for a command or custom function? Maybe you have tried to use a command that presented nested option prompts, and no matter how well you guessed, you got the wrong results. Both of these situations waste time. Fortunately, there is a solution to these problems and it is in the form of dialog boxes. Dialog boxes, or more specifically DCL in AutoLISP, can be used to improve users' experience by allowing them to follow a nonlinear workflow and provide only the information required to complete a task. Users can quickly scan and change values before completing a task. At the end of the day, a dialog box can help to reduce clicks, which means saving time — and time is money.

---

#### 13.2.1 Defining a Dialog

Each dialog box you define must contain a dialog tile. The attributes of a dialog tile are used to define the dialog's label (more commonly referred to as the title or caption), add a programmatic name known as a key, and set the tile that should have initial focus. The following shows the basic syntax of the dialog tile:

```c
dialog_name : dialog { 
  [attributes] 
  [tiles] 
}
```

Here are its arguments:

`dialog_name`. The `dialog_name` argument represents the name used to reference a dialog box within a DCL file. A DCL file can contain more than one dialog tile, but each must have a unique name. The same name can be used in different DCL files without any problems.

attributes. The attributes argument is a list of optional attributes that describe the dialog tile. An attribute consists of a name and value, separated by an equals sign, and ends with a semicolon. For example, `label = "Title";` specifies the use of the attribute named label and that it should be assigned the value of Title. See Table 23.1 for a list of the attributes that the dialog tile supports.

tiles. The tiles argument is a list of optional tiles that define the controls that you want to display in the dialog box. For information on the tiles that are available, see the「Adding Tiles」and「Grouping, Aligning, and Laying Out Tiles」sections later in this chapter.

Table 23.1 Common attributes used with the dialog tile

1 label. The title that is assigned to the dialog box.

2 value. Alternative to the title attribute. This attribute can be set only with the `set_tile` function. I discuss the `set_tile` function later in this chapter, in the「Setting the Default Value of an Interactive Tile」section.

3 `initial_focus`. The key assigned to the tile in the dialog tile that should have focus by default when the dialog box is displayed.

An example of a dialog tile was shown earlier in this chapter; see Listing 23.1 and Figure 23.1.

#### 13.2.2 Adding Tiles

A dialog box can contain a variety of tiles — commonly referred to as controls — that can be used to get input from the user. The tiles that are available for placement in a dialog box are common to many Windows dialog boxes. The following shows the basic syntax of a tile:

```c
: tile_name { 
  [attributes] 
}
```

Here are its arguments:

`tile_name`. `The tile_name` argument represents the name of the tile type to place in the dialog box. See Table 23.2 for the tile names that are supported.

attributes. The attributes argument is a list of optional attributes that describe the tile. An attribute consists of a name and value, separated by an equals sign, and ends with a semicolon. For example, `label = "Control1";` specifies the use of the attribute named label and that it should be assigned the value of Control1. See Table 23.3 for a list of the common attributes that tiles support.

Table 23.2 Interactive tiles available with the dialog tile

Table 23.2 lists and describes the interactive tiles that can be added to a dialog tile for getting input from the user when a dialog box is displayed.

1 button. Push or command button that, when clicked, executes a function.

2 `edit_box`. Free-form text box in which the user can enter an alphanumeric value.

3 image. Container that displays a slide image. The slide image can be a stand-alone SLB file or one from a compiled slide library SLD file.

4 `image_button`. Graphical button that displays a slide image that, when clicked, executes a function.

5 `list_box`. List box that contains a set of predefined items from which the user can select one or more items.

6 `popup_list`. Drop-down list that contains a set of predefined items from which the user can choose a single item.

7 `radio_button`. Option button that allows for a single choice among multiple option buttons.

8 slider. Scroll bar–like control that allows the user to specify a value within a specific range.

9 text. Label that displays information to the user or identifies the intention of a control.

10 toggle. Check-box button that allows for multiple choices.

Table 23.3 Common attributes used with control tiles

Table 23.3 lists and describes some of the most commonly used attributes to control the behavior of tiles other than a dialog tile.

|  Attribute | Supported Tile(s)  | Description   |
|---|---|---|
| action  |   All interactive tiles |  Function to be executed when the tile is clicked.  |
|  allow_accept | edit_box, image_button, and list_box  |  Activates the button that is specified with the is_default attribute. |
| edit_limit  | edit_box  |  Maximum number of characters that can be entered into the text box. |
| is_cancel  | button  | Indicates that the function associated with the button tile's action attribute should be executed when Esc is pressed.  |
| is_default  | button  | Indicates that the function associated with the button tile's action attribute should be executed when Enter is pressed.  |
|  is_enabled | All interactive  | control tiles Indicates that the tile is enabled or disabled.  |
| key  | All interactive  | control tiles Unique name used to programmatically reference the tile.  |
| label  | button, edit_box, list_box, popup_list, radio_button, text, and toggle  | Label that describes the intention of the tile and is displayed adjacent to the tile.  |
| list  | list_box and popup_list  | Items that are displayed and selectable by the user in the list. The character sequence \n is used to separate each item in the list.  |
| multiple_select  | list_box |  Indicates that the list supports multiple selections. |
|  value  | text_box and interactive tiles except button and image_button tiles  |  Current value of a tile. |

To see what values an attribute supports, search on the keywords「programmable dialog box reference」in the AutoCAD Help system. Search on the keywords「synopsis predefined attributes」in the AutoCAD Help system to see the other attributes that are available.

NOTE: All the tiles listed in Table 23.2 are interactive tiles, with the exceptions of the image and text tiles.

Listing 23.2 shows an example of a dialog box that contains a `popup_list`, two `radio_button` tiles, and a button tile. Figure 23.2 shows what the dialog box would look like if displayed in the AutoCAD drawing environment using AutoLISP.

Listing 23.2: Create Label Object dialog box

```c
/* Create label object */ 
ex_createLabelObject : dialog { 
  label = "Create Label Object"; 
  key = "dlg_layer"; 
  : popup_list { 
    // Drop-down list 
    key = "list_layers"; 
    label = "Layer to place object on"; 
  } 
  : radio_button { 
    // Circle 
    key = "opt_circle"; 
    label = "Circle"; 
  } 
  : radio_button { 
    // Octagon 
    key = "opt_octagon"; 
    label = "Octagon"; 
  } 
  : button { 
    // Create object button 
    key = "btn_create_object"; 
    action = "create_object"; 
    label = "Create"; 
    is_default = "true"; 
  }
  cancel_button; // Cancel only button 
}
```

1『

在 lisp 文件里调用这个 box。

```c
; get the current file direction
(defun c:dcltest (/ dcl_id)
  (setq dcl_id (load_dialog (strcat "D:\\dataflowcad\\" "dataflow.dcl")))
  (if (not (new_dialog "ex_createLabelObject" dcl_id))
    (exit)
  )

  (start_dialog)
  (unload_dialog dcl_id)
)
```

』

In addition to the tiles listed in Table 23.2, DCL makes use of tile subassemblies. Tile subassemblies are used to provide common arrangements of exit buttons. Table 23.4 shows several of the available tile subassemblies that can be used in a dialog tile. You can view the names of the subassemblies in the base.dcl file located in the AutoCAD Support folder. A subassembly ends with a semicolon, as shown in Listings 23.1 and 23.2. You can't change the attribute values of a subassembly provided by AutoCAD, but you can re-create a subassembly with different attribute values in your own DCL files. Use the syntax found in the base.dcl file as the basis for your new subassembly code. The base.dcl file can be found in the AutoCAD support-file search path by entering (findfile "base.dcl") at the Command prompt.

Table 23.4 Tile subassemblies

|  Tile Subassembly | Description  |
|---|---|
|  cancel_button |  Cancel only button |
| ok_button  |  OK only button  |
| ok_cancel  |  OK and Cancel buttons |
| ok_cancel_help_   | OK, Cancel, and Help buttons  |

#### 13.2.3 Grouping, Aligning, and Laying Out Tiles

Tiles are stacked vertically in a dialog box by default, unless you use what are called cluster tiles. Cluster tiles are used to group and align tiles in rows and columns. Tiles also support several attributes that help you control their size and alignment in a dialog box. In addition to cluster tiles and attributes, spacer tiles can be used to control the size and alignment of tiles. A spacer tile allows for the insertion of empty space between tiles in a dialog box.

1-2『调整窗口布局的几种方式汇总：1）用 cluster tiles 控制。2）用 tile 里的属性控制。3）用 spacer tiles 控制。做一张任意卡片。』 —  — 已完成

#### Grouping Tiles into Clusters

Grouping tiles into a cluster allows you to better control how they are aligned or organized in the dialog box, in addition to controlling which `radio_button` tiles are related to each other. A cluster tile must be used to restrict the choice of multiple `radio_button` tiles in a dialog box so only one option button can be selected at a time. Tiles can be grouped into columns and rows with or without a visual grouping box. Table 23.5 lists and describes the cluster tiles that can be used to group tiles.

Table 23.5 Cluster tiles

|  Tile Name | Description  |
|---|---|
| boxed_column  | Groups tiles into a column and draws a box with a label around the tiles.  |
|  boxed_radio_column | Groups related radio_button tiles into a column and draws a box with a label around the tiles; tiles are treated as exclusive to each other.  |
| boxed_radio_row  | Groups related radio_button tiles into a row and draws a box with a label around the tiles; tiles are treated as exclusive to each other.  |
| boxed_row  |  Groups tiles into a row and draws a box with a label around the tiles. |
| column   | Groups tiles into a column; no grouping box is drawn around the tiles.  |
|  radio_column | Groups related radio_button tiles into a column; tiles are treated as exclusive to each other. No grouping box is drawn around the tiles.  |
| radio_row  | Groups related radio_button tiles into a row; tiles are treated as exclusive to each other. No grouping box is drawn around the tiles.  |
| row  | Groups tiles into a row; no grouping box is drawn around the tiles.  |

Listing 23.3 shows a revised version of the DCL syntax shown in Listing 23.2. The revised syntax uses the `boxed_radio_column` and `row` cluster tiles to group tiles. Figure 23.3 shows what the dialog box would look like if displayed in the AutoCAD drawing environment using AutoLISP.

Listing 23.3: Create Label Object dialog box with cluster tiles

```c
/* Create label object */ 
ex_createLabelObject : dialog { 
  label = "Create Label Object"; 
  key = "dlg_layer"; 
  : popup_list { 
    // Drop-down list 
    key = "list_layers"; 
    label = "Layer to place object on"; 
  } 
  : boxed_radio_row { 
    label = "Shape"; 
    : radio_button { 
      // Circle 
      key = "opt_circle"; 
      label = "Circle"; 
      } 
    : radio_button { 
      // Octagon 
      key = "opt_octagon"; 
      label = "Octagon"; 
      } 
    } 
  
  : row { 
    : button { 
      // Create object button 
      key = "btn_create_object"; 
      action = "create_object"; 
      label = "Create"; 
      is_default = "true"; 
    } 
    cancel_button; 
  } 
}
```

#### Aligning and Sizing Tiles

When a dialog box is displayed, tiles have a default alignment and size assigned to them. In most cases, a tile's size is based on the label text that it is assigned, or the width of the dialog box or cluster tile that it is placed within. Table 23.6 describes the tile attributes that can be used to control the alignment and size of the tiles in a dialog tile.

Table 23.6 Attributes used with aligning and sizing tiles

|  Attribute | Supported Tile(s)  | Description   |
|---|---|---|
| alignment  | All tiles  | Horizontal or vertical alignment of a tile  |
| children_alignment |  column, row, boxed_row, boxed_column, boxed_radio_column, boxed_radio_row, radio_column, and radio_row  |  Overrides the horizontal or vertical alignment for all tiles contained in a cluster tile |
| children_fixed_height | column, row, boxed_row, boxed_column, boxed_radio_column, boxed_radio_row, radio_column, and radio_row  | Overrides the fixed height for all tiles contained in a cluster tile  |
| children_fixed_width | column, row, boxed_row, boxed_column, boxed_radio_column, boxed_radio_row, radio_column, and radio_row  |  Overrides the fixed width for all tiles contained in a cluster tile |
| edit_width |  edit_box and popup_list  |  Width of the input field, not the tile  |
| fixed_height  |  All tiles |  Absolute height of a tile  |
| fixed_width  |  All tiles  |  Absolute width of a tile  |
| height |   All tiles | Minimum height of a tile; might increase when the dialog box is displayed  |
| width |   All tiles |  Minimum width of a tile; might increase when the dialog box is displayed |

To see which values an attribute supports, search on the keywords「programmable dialog box reference」in the AutoCAD Help system.

In addition or as an alternative to using tile attributes, spacer tiles can be used to increase the space between tiles. Table 23.7 lists and describes the spacer tiles that can be used to align tiles and control tile size.

Table 23.7 Spacer tiles

|  Tile Name | Description  |
|---|---|
| spacer  | Inserts a gap of the specified size in the horizontal or vertical direction; the direction that the gap is created in is defined by how the tile is clustered with other tiles.  |
| spacer_0  | Inserts a gap that restricts the distribution or automatic resizing of tiles to the left or above the spacer tile.  |
| spacer_1  | Inserts a gap of one unit wide by one unit high.  |

Listing 23.4 shows a revised version of the DCL syntax shown in Listing 23.3. The revised syntax uses the `edit_width` attribute to size the `popup_list` tile, the `fixed_width` and alignment attributes on the row tile, the width attribute for the button tile, and a spacer tile to control the alignment and sizing of the tiles in the dialog box. Figure 23.4 shows what the dialog box would look like if displayed in the AutoCAD drawing environment using AutoLISP.

Listing 23.4: Aligning and sizing tiles in the Create Label Object dialog box

```c
/* Create label object */ 
ex_createLabelObject : dialog { 
  label = "Create Label Object"; 
  key = "dlg_layer"; 
  : popup_list { 
    // Drop-down list 
    edit_width = 10; 
    key = "list_layers"; 
    label = "Layer to place object on"; 
  } 
  : boxed_radio_row { 
    label = "Shape"; 
    : radio_button { 
      // Circle 
      key = "opt_circle"; 
      label = "Circle"; 
      } 
      : radio_button { 
        // Octagon 
        key = "opt_octagon"; 
        label = "Octagon"; 
      } 
  } 
  : row { 
    fixed_width = true; 
    alignment = right; 
    : button { 
      // Create object button 
      key = "btn_create_object"; 
      action = "create_object"; 
      label = "Create"; 
      is_default = "true"; 
      width = 12; 
    } 
    : spacer { 
      width = 1; 
    } 
    cancel_button; 
  }
}
```

#### 13.2.4 Creating and Previewing a Dialog in a DCL File

You can create a DCL file with Notepad or the Visual LISP Editor; you follow the same process you use to create a LSP file. The only difference is that you specify a file extension of .dcl instead of .lsp. Once you create a DCL file, you can add a dialog box definition to the file. To see what the dialog box looks like, you must load the DCL file in the AutoCAD drawing environment and display it. There are two approaches available for viewing a DCL file. The first is to create an AutoLISP program that loads and displays the file; the other involves using the Visual LISP Editor. (The second approach eliminates the need to write any code.) I discuss how to load a DCL file and display a dialog box in the next section.

1『加载显示窗口（box）的 2 种方法，做一张任意卡片。』 —  — 已完成

The Visual LISP Editor makes it easy to create, modify, and preview a DCL file. When a DCL file is open and in the current window of the editor, you can click Tools Interface Tools Preview in DCL Editor to preview the dialog box. A dialog box allows you to specify which dialog in the DCL file to preview. The Visual LISP Editor sends some AutoLISP code to the AutoCAD Command prompt and displays the dialog box. Click Cancel or another tile to close the dialog box and return to the Visual LISP Editor.

NOTE: The DCL Preview feature requires you to have full read/write access to the AutoCAD installation folder. If you don't have those permissions, you will need to request them from your company's IT department or adjust the permissions yourself using the User Account settings through the Windows Control Panel.

In this exercise, you will create a DCL file based on the dialog box defined in Listing 23.4 and then preview it using the Visual LISP Editor:

1 In AutoCAD, click the Manage tab Applications panel Visual LISP Editor.

2 In the Visual LISP Editor, click File New File.

3 Click File Save As.

4 In the Save-as dialog box, browse to the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store DCL files.

5 In the File Name text box, type ex_createLabelObject.

6 Click the Save As Type drop-down list and choose DCL Source Files.

7 Click Save.

8 In the text editor window, type the following:

```c
Listing 23.4
```

9 Click File Save.

10 Click Tools Interface Tools Preview DCL In Editor.

11 In the Enter The Dialog Name dialog box, click OK. That dialog box lists all the dialog-box definitions in the DCL file that is open in the editor.

12 Review the dialog box and click any control to return to the Visual LISP Editor. The dialog box you create should look like the one shown earlier, in Figure 23.4.

### 13.3 Loading and Displaying a Dialog Box

The Visual LISP Editor makes it easy to preview a dialog box, but it doesn't allow you to interact with the tiles on the dialog box. A DCL file must be loaded and displayed with AutoLISP to enable user interaction. When a dialog box is being loaded, you can set the initial values of each tile and specify the enabled state of each tile. If your dialog box contains any list\_box, popup\_list, image, or image\_button tiles, you might have to perform some initialization tasks for these tiles. (I cover those tasks in the「Initializing Tiles」section later in this chapter.)

#### 13.3.1 Loading and Unloading a DCL File

A DCL file must be loaded into the AutoCAD drawing environment before you can display one of the dialog-box definitions in the file. The `load_dialog` function loads a DCL file and returns a random integer value that represents a DCL file ID. A positive DCL file ID value indicates that the DCL file was located in the AutoCAD support-file search paths specified in the Options dialog box and was successfully loaded; a negative value notifies you that the DCL file wasn't located and loaded.

The following shows the syntax of the load_dialog function:

```c
(load_dialog dcl_filename)
```

The `dcl_filename` argument that the `load_dialog` function expects is a string that represents the path to and the filename of the DCL file you want to load. I recommend placing DCL files in the AutoCAD support-file search paths. When you do so, only the filename needs to be specified, making it easier to move the files on your network if needed.

Here is an example that loads a DCL file named ex\_createLabelObject.dcl with the load\_dialog function and the return of the DCL file ID, in this instance a value of 101. You should always store the DCL file ID in a variable so that you can display and unload a dialog box defined in the DCL file. The DCL file was created as part of the exercise in the「Creating and Previewing a Dialog in a DCL File」section earlier in this chapter.

```c
(setq id (load_dialog "ex_createLabelObject.dcl")) 
// out
101
```

The `unload_dialog` function unloads a dialog box definition from memory; the particular dialog is identified by the DCL file ID that was returned by the `load_dialog` function. The DCL file ID changes each time the DCL file is loaded, and the value returned should be stored in a variable until the dialog box is no longer needed in the current drawing session. A dialog box can be loaded more than once; each time a dialog box is loaded, a new instance of the dialog box is stored in memory until it is unloaded. The following shows the syntax of the `unload_dialog` function:

```c
(unload_dialog dcl_file_id)
```

The dcl\_file\_id argument that the `unload_dialog` function expects is the same value that was returned by the `load_dialog` function. The `unload_dialog` function always returns a value of nil, and that value has no significant meaning; successfully or unsuccessfully unloading the dialog box results in the same value of nil. Here is an example of the `unload_dialog` function:

```c
(unload_dialog id) 
// out
nil
```

#### 13.3.2 Displaying a Dialog

After a DCL file has been loaded, an instance of a dialog box contained in the loaded DCL file can be created and displayed with the `new_dialog` function. The `new_dialog` function is also used to specify a default action for all interactive tiles that don't have an action assigned to them, and the onscreen display location. The `new_dialog` function returns T if the dialog box was successfully created, or it returns nil if the dialog box couldn't be created. The following shows the syntax of the `new_dialog` function:

```c
(new_dialog dialog_name dcl_file_id [action [point]])
```

Here are its arguments:

1 dialog\_name. The dialog\_name argument is a case-sensitive string that specifies the unique name of the dialog to create an instance of from the DCL file specified by the dcl\_file\_id argument. The value must exactly match the name applied to the dialog tile and is case sensitive.

2 dcl\_file\_id. The dcl\_file\_id argument that the new\_dialog function expects is the value that was returned by the load\_dialog function.

3 action. The action argument is an optional string that represents an AutoLISP expression. This expression is applied to the action attribute of all interactive tiles that aren't assigned an action as part of the DCL file; the function is executed when the tile is clicked. Provide "" when you want to specify the point argument but no default action.

4 point. The point argument is an optional 2D point list that represents the onscreen location of the dialog box's upper-left corner. The dialog box is centered by default and can be specified with a value of ‘(-1 -1). The upper-left corner of the screen is 0,0.

Once an instance of a dialog box has been created with the `new_dialog` function, the `start_dialog` function must eventually be called. The `start_dialog` function informs AutoCAD that the dialog box is ready for user interaction. Before `start_dialog` is executed, you should make sure that all initial default values and enabled states have been specified. The next section explains how to set the default values for and specify the enabled state of tiles, as well as initialize lists and images.

The `start_dialog` function doesn't accept any arguments and returns a status value based on how the user exited the dialog box. A status value of 1 generally means the user clicked OK or a similar button, whereas a value of 0 indicates the user clicked Cancel or the Close button. The status value returned by a tile is determined by the value passed to the `done_dialog` function. I cover the `done_dialog` function later in this chapter, in the「Terminating or Closing a Dialog Box」section. You don't need to worry about executing the `done_dialog` function if you use one of the tile subassemblies that contains the OK or Cancel button mentioned earlier, in the「Adding Tiles」section.

The following example code shows how to load and unload a DCL file, and then create and display a dialog box. `ex_createLabelObject.dcl` is the name of the DCL file that will be loaded. The dialog box definition name is `ex_createLabelObject`. Although in this example the DCL file and dialog name are the same, they don't need to be. I recommend having one dialog box per DCL file and using the same name, but that is just a personal preference.

```c
; Define a function named createlabelobject 
(defun c:createlabelobject (/ dialog_name id) 
  (setq dialog_name "ex_createLabelObject") 
  ; Load the DCL file named ex_createLabelObject.dcl 
  (setq id (load_dialog (strcat dialog_name ".dcl"))) 
  ; Create a new instance of the dialog named ex_createLabelObject 
  ; in the center of the screen 
  (new_dialog dialog_name id "" '(-1 -1)) 
  ; Perform additional tasks here 
  ; 1. Set default values for tiles here with the set_tile function 
  ; 2. Set up lists and images here 
  ; 3. Assign actions here for tiles with the action_tile function 
  ; 4. Get information about a tile with get_tile as part of the 
  ;   action assigned with action_tile 
  ; 5. Terminate the dialog box with the done_dialog function as 
  ;   part of the action assigned with action_tile 
  ; Display the dialog box and get the exit status 
  (setq status (start_dialog)) 
  ; Unload the DCL file from memory 
  (unload_dialog id) 
  ; Display a custom message based on the exit status of the dialog 
  (if (= status 1) 
    (alert "User clicked Create.") 
    (alert "User clicked Cancel.") 
  ) (princ) 
)
```

#### 13.3.3 Initializing Tiles

You can manipulate the interactive tiles of a dialog tile in a DCL file once you create an instance of a dialog box in memory by using the `new_dialog` function. You use the value of the key attribute to reference a tile of a dialog box. Once you have a tile's key, you can set the default value of a tile, set the tile's enabled state, populate items in the list of a `list_box` or `popup_list` tile, or assign a slide to an image or `image_button` tile.

#### Setting the Default Value of an Interactive Tile

When you use a dialog box, have you ever noticed that it often remembers the previously entered values or that values change based on the controls you interact with? You can assign a default value to a tile by using the value attribute in a DCL file or change the default value before a dialog box is displayed by using the `set_tile` function.

I recommend setting the default value of a tile using the `set_tile` function, considering it is good practice to restore previously entered values each time the dialog box is redisplayed. The `set_tile` function can also be used to change the value of a tile when the user interacts with a tile while the dialog box is displayed. I discuss how to handle user interaction with tiles in the「Interacting with and Responding to a User」section later in this chapter.

The following shows the syntax of the set_tile function:

```c
(set_tile key val)
```

Here are its arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile you want to modify.

val. The val argument is the string value you want to assign to the tile. An alphanumeric string can be assigned to an `edit_box` tile, whereas an integer formatted as a string can be assigned to a `list_box`, `popup_list`, toggle, `radio_button`, or slider tile. The first item in the list of a `list_box` or `popup_list` tile is 0, the second is 1, and so on.

1『注意啊，tile 的值都是字符串。（2020-10-09）』

The following code shows how to set a value of 1, which means true, to a tile with the key of `opt_circle` using the `set_tile` function. The key `opt_circle` refers to the Circle `radio_button` tile of the `ex_createLabelObject` dialog definition you created in the「Creating and Previewing a Dialog in a DCL File」section.

```c
(set_tile "opt_circle" "1")
```

NOTE: The `set_tile` function can't be executed until after the `new_dialog` function has been executed. Execute the `set_tile` function before the `start_dialog` function to ensure that the tile is updated before the dialog box is displayed.

1『所以，设置默认值，应该在 `new_dialog` 之后以及 `start_dialog` 之前。（2020-10-09）』

#### Enabling and Disabling an Interactive Tile

The tiles of a dialog box are all enabled by default, meaning the user can click or enter text in any interactive tile of a dialog box. The `is_enabled` attribute of a tile controls the tile's default enabled state. When `is_enabled` is set to false, the user is unable to interact with the tile when the dialog box is displayed. The enabled state of a tile can be changed using the `mode_tile` function.

I recommend setting the enabled state of a tile using the mode_tile function and not the is_enabled attribute. The main reason for doing so is because the disabling of a tile is often based on the condition of other tiles or choices made by the user in the dialog box. I discuss how to handle user interaction with tiles in the「Interacting with and Responding to a User」section.

1『作者建议 `mode_tile` 来设置 tile 的激活状态，不用用 tile 自身的属性 `is_enabled` 来设置，记住这点。（2020-10-09）』

The following shows the syntax of the `mode_tile` function:

```c
(mode_tile key mode)
```

Here are its arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile you want to modify.

mode. The mode argument is an integer value that specifies the mode that should be applied to the tile. Table 23.8 lists the available modes that can be applied to a tile.

Table 23.8 Modes available for use with `the mode_tile` function

|  Mode | Description  |
|---|---|
| 0 | Enables an interactive tile |
| 1 | Disables an interactive tile |
| 2 | Sets focus to an interactive tile |
| 3 | Selects the text in an edit_box tile |
| 4 | Toggles highlighting for an image tile |

The following code shows how to disable and then enable a tile with the key of `opt_circle` using the `mode_tile` function. The key `opt_circle` refers to the Circle `radio_button` tile of the `ex_createLabelObject` dialog definition you created in the「Creating and Previewing a Dialog in a DCL File」section.

```c
; Disables tile 
(mode_tile "opt_circle" 1) 
; Enables tile 
(mode_tile "opt_circle" 0)
```

NOTE: The `mode_tile` function can't be executed until after the `new_dialog` function has been executed. Execute the `mode_tile` function before the `start_dialog` function to ensure that the tile is updated before the dialog box is displayed.

#### Populating the Items of a `list_box` or `popup_list` Tile

The `list_box` and `popup_list` tiles allow the user to select one or more predefined values from a list. The items available in the list of the two tiles can be specified using the tile's list attribute or AutoLISP functions. The `start_list` function is used to assign, update, or replace the list of values applied to a `list_box` or `popup_list` tile. When a list can be modified, the `start_list` function returns the name of the list; otherwise the function returns nil, indicating the list isn't accessible for modification. Typically, a list isn't available for modification because you provided an incorrect key to the `start_list` function or the function was called before the execution of the `new_dialog` function.

The following shows the syntax of the `start_list` function:

```c
(start_list key [mode [idx]])
```

Here are its arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile you want to modify.

mode. The mode argument is an integer value that specifies how the list currently assigned to the tile can be modified. Table 23.9 describes each of the available modes.

idx. The idx argument is an integer value that specifies an item in the list. The item is used to indicate which item to change if the mode is set to 1; when the mode is set to 2, it indicates the starting item you want to begin appending new items to.

Table 23.9 List-editing modes

Table 23.9 describes the modification modes that can be used to edit a list.

|  Mode | Description  |
|---|---|
| 1 | Next call to `add_list` replaces the item indicated by the idx argument. |
| 2 | Next call to `add_list `appends a new item after the item indicated by the idx argument. If an index isn't provided, the new item is appended after the last item in the list. |
| 3 | Items in the list are cleared and a new item is appended. |

After a tile key, mode, and index have been specified with the `start_list` function, you can change or add new items with the `add_list` function. The `add_list` function accepts a single argument of a string value. This value is the text that will be displayed in the list of the `list_box` or `popup_list` tile. If the value is successfully added to the list, the string passed to the `add_list` function is returned; otherwise, nil is returned, indicating the item wasn't added.

Once you have modified a list, use the `end_list` function. The `end_list` ends the modification of the list that was started with the `start_list` function. The `end_list` function returns a value of nil regardless of whether the list was successfully modified.

1-2『目前还没想到，直接在交互界面里给下拉菜单添加元素的应用场景。回复：想到应用场景了，比如筛选选择集之后，将选集里的相关内容直接在交互界面上呈现出来，就跟 CAD 原生查询面板一样。（2020-10-09）回复：这个功能其实非常有用，比如想开发的功能，先根据某个属性值匹配通配符来筛选管道号块，筛出来的块只把属性值提取出来添加到这个列表让用户看到。第二部输入要替换的原字符以及新字符，这个功能一定要实现。（2020-10-10）做一张任意卡片。』 —  — 已完成

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

#### Working with image and `image_button` Tiles

The image and `image_button` tiles allow you to display a slide in a frame or as a graphical button. Based on the image you want to display, you will need to use one of several AutoLISP functions to initialize the tile. In earlier AutoCAD releases, `image_button` tiles were used to display a preview of a block and then start an AutoLISP expression that would allow the insertion of the block. However, the relevance of the image and `image_button` tiles in a dialog box has diminished in recent releases with interfaces such as the ribbon and Tool Palettes window.

If you want to display a slide (SLD) file in a dialog definition with an image or `image_button` tile, you will want to explore the functions listed in Table 23.10. You can learn more about these functions in the AutoCAD Help system.

Table 23.10 AutoLISP functions used to work with image and `image_button` tiles

|  Function Name | Description  |
|---|---|
|  `dimx_tile` | Returns the width of an image or `image_button` tile  |
|  `dimy_tile` | Returns the height of an image or `image_button` tile  |
|  `end_image` | Ends the modification of the current image set by the `start_image` function  |
|  `fill_image` |  Draws a filled rectangle in the current image set by the `start_image` function  |
|  `slide_image`  | Displays a slide (SLD) file or a slide in a slide library (SLB) file in the current image  |
|  `start_image` |  Starts the modification of an image and sets it as the current image  |
|  `vector_image` |  Draws a vector in the current image set by the `start_image` function  |

### 13.3 Interacting with and Responding to a User

While a dialog box is displayed onscreen, the user is able to interact with the tiles that are enabled. As the user interacts with the tiles, the AutoLISP expressions assigned to the tile's action attribute are executed. The AutoLISP expressions can be used to get and set tile and attribute values, and to change the enabled state of a tile.

#### 13.3.1 Specifying the Action of a Tile

An interactive tile can be assigned an AutoLISP expression that is to be executed when the tile is clicked or interacted with. You use the action attribute in a DCL file to assign an AutoLISP expression to a tile or the `action_tile` function. As part of the AutoLISP expression, you can get information about the tile that is being interacted with by using several predefined variables. Table 23.11 lists the predefined variables that can be referenced by the AutoLISP expression assigned to a tile's action attribute.

NOTE: After you create an instance of a dialog box with the `new_dialog` function, you can assign a string value to a tile from the custom program with the `client_data_tile` function; this is in addition to the tile's value attribute. When the AutoLISP expressions assigned to the tile's action attribute are executed, you can reference this string value with the `$data` variable. For more information on the `client_data_tile` function, refer to the AutoCAD Help system.

1-2『直觉上 `client_data_tile` 这个函数非常有用，去深挖。目前的感觉是在外面用这个函数把外面的数据传递给 tile，然后再通过 tile 的内置变量 `$data` 提取出来，但为啥要绕一圈呢，肯定是有原因的。（2020-10-09）』 —  — 未完成

Table 23.11 Predefined variables that contain information about the current tile

|  Variable Name | Description  |
|---|---|
|  `$data` | Custom information assigned to a tile with the `client_data_tile` function.  |
|  `$key` | Key name assigned to the tile.  |
|  `$reason` | Callback reason based on the interaction performed by the user. Possible values are 1, 2, 3, or 4. 1 indicates the user has clicked or pressed Enter to activate a tile, 2 means the user exited an `edit_box` tile, 3 indicates the value of a slider tile has changed, and 4 is returned when a `list_box` or image tile is `double-clicked`.  |
|  `$value` | Current value of the tile.  |
|  `$x` | Coordinate value of an image along its x-axis when an `image_button` tile is clicked.  |
|  `$y` | Coordinate value of an image along its y-axis when an `image_button` tile is clicked.  |

 1『 `$reason` 这个内置变量感觉也有大用户。（2020-10-09）』

I recommend setting a tile's action using the `action_tile` function to give you the flexibility to dynamically change the AutoLISP expression that is assigned while the user is interacting with the dialog box. For example, you might want to assign a different action to a button tile based on the `radio_button` tile that the user chooses.

NOTE: By means of the action attribute or the `action_tile` function, an AutoLISP expression can be assigned to all tiles in a dialog box that don't have a specific expression assigned to them. This general action is assigned with the action argument of the `new_dialog` function mentioned earlier, in the「Displaying a Dialog」section.

The following shows the syntax of the `action_tile` function:

```c
(action_tile key expr)
```

Here are its arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile you want to modify.

expr. The expr argument is a string value that represents the AutoLISP expression that should be executed when the user interacts with the tile.

1『

这个地方的表达式也必要在字符串里。（2020-10-09）

```c
(defun modifyBlockProperty (tileName blockSSName / dcl_id property_name property_value status selectedName ss)
  (setq dcl_id (load_dialog (strcat "D:\\dataflowcad\\" "dataflow.dcl")))
  (if (not (new_dialog tileName dcl_id))
    (exit)
  )
  ; optional setting for the popup_list tile
  (set_tile "property_name" "0")
  ;the default value of input box
  (set_tile "property_value" "")
  (mode_tile "property_name" 2)
  (mode_tile "property_value" 2)
  (action_tile "property_name" "(setq property_name $value)")
  (action_tile "property_value" "(setq property_value $value)")
  (if (= nil property_name)
    (setq property_name "0")
  )

  (setq status (start_dialog))
  (unload_dialog dcl_id)
  
  (if (= status 1)
    (progn 
      (setq selectedName (GetPropertyName property_name blockSSName))
      (setq ss (GetBlockSS blockSSName))
      (ModifyPropertyValue ss selectedName property_value)
      (alert "更新数据成功")(princ)
    )
    ;(alert "取消选择")
  )
)
```

』

The following code shows how to assign the AutoLISP expression `(alert (strcat "Tile key: " $key))` to the tile with the key of `opt_circle` using the `action_tile` function. The key `opt_circle` refers to the Circle `radio_button` tile of the `ex_createLabelObject` dialog definition you created in the「Creating and Previewing a Dialog in a DCL File」section.

```c
(action_tile "opt_circle" "(alert (strcat \"Tile key: \" $key))")
```

1『注意啊，里面的双引号需要加转义字符。（2020-10-09）』

NOTE: Execute the `action_tile` function before the `start_dialog` function to ensure that the action is assigned to the tile before the dialog box is displayed.

#### 13.3.2 Getting Information about a Tile

When a user interacts with the tiles of a dialog box, you will commonly want to get the current value of one or all tiles before the dialog box is closed. The current value of the value attribute of a tile can be obtained using the `get_tile` function. If you want to get the value of an attribute other than value, you can use the `get_attr` function. The `get_tile` and `get_attr` functions return a string value.

NOTE: The `get_tile` and `get_attr` functions must be executed before the `done_dialog` function is called to terminate the dialog box. I discuss the `done_dialog` function in the next section.

1『感觉用 `get_tile` 获取内置变量 `$value` 可以解决之前遇到的一个 bug，下来列表默认不选的话返回 nil 的问题。待验证。（2020-10-09）』

The following shows the syntax of the `get_tile` and `get_attr` functions:

```c
(get_tile key) 
(get_attr key attr)
```

Here are their arguments:

key. The key argument is a string that specifies the value assigned to the key attribute of the tile to query.

attr. The attr argument is a string value that specifies the name of the attribute to query.

The following code shows how to get the current value of the tile with the key of `opt_circle` using the `get_tile` function, and get the items assigned to the list attribute of a `popup_list` tile with the key of `list_layers`. These tiles are part of the `ex_createLabelObject` dialog definition you created in the「Creating and Previewing a Dialog in a DCL File」section.

```c
; Gets the current value of the tile 
(get_tile "opt_circle") 
"1" 
; Gets the current value of the list attribute 
(get_attr "list_layers" "list") 
"A-Door\nA-Window"
```

1『通过这个例子就明白了 `attr` 指什么数据，就是 `list_box` tile 里 list 属性里的值，哈哈。（2020-10-09）』

#### 13.3.3 Terminating or Closing a Dialog Box

A dialog box must be terminated — or closed — when it is no longer needed and the end user wants to return to the drawing area. The `done_dialog` function is used to indicate that the dialog box can be terminated. You commonly add this function as the last part of the AutoLISP expression assigned to the action attribute of a button tile such as OK or Cancel that terminates a dialog box. Before `done_dialog` is executed, you want to make sure you get the value of any tiles or tile attribute values by using the `get_tile` or `get_attr` function.

NOTE: The OK and Cancel buttons defined in the predefined subassemblies automatically execute (done_dialog 1) and (done_dialog 0), respectively, when the button is clicked. `done_dialog` needs to be executed only for tiles that close a dialog box.

The `done_dialog` function returns a 2D point list that represents the current placement of the dialog box onscreen. You can store this value as part of the Windows Registry, and then, to restore the location the next time the dialog box is displayed, pass the 2D point list to the `new_dialog` function.

1『妙啊，做成第二个弹窗跟第一个一模一样的假象。（2020-10-09）』

The following shows the syntax of the `done_dialog` function:

```c
(done_dialog [status])
```

The status argument is an integer value that will be returned by the `start_dialog` function. Typically, 0 indicates that the user clicked Cancel or the dialog box was canceled, whereas 1 indicates that the user clicked OK or an equivalent tile. A value greater than 2 can be passed to the status argument.

The following code shows how to assign a custom action to the OK and Cancel buttons of a dialog box. The alert function is called before `done_dialog` to simply demonstrate that more than one AutoLISP function can be called from a tile's action.

```c
; Assign an action to the OK button 
(action_tile "accept" "(alert \"OK clicked.\")
(done_dialog 1)") 
; Assign an action to the Cancel button 
(action_tile "cancel" "(alert \"Cancel clicked.\")
(done_dialog 0)")
```

If you have more than one dialog box displayed, in the case of working with nested dialog boxes, the `term_dialog` function can be executed to close all open dialog boxes and return to the drawing area. The `term_dialog` function doesn't accept any argument values and always returns nil.

#### 13.3.4 Hiding a Dialog Box Temporarily

1『看到标题就知道是自己要找的功能了，哈哈。（2020-10-09）』

When getting input from the user with a dialog box, it isn't uncommon to allow the user to specify a point or select objects in the drawing area. Before a user can interact with the drawing area, the dialog box must be temporarily hidden. The concept of hiding a dialog box involves creating a dialog box with `new_dialog` and then starting user interaction with `start_dialog` in a looping expression that uses the while function. The `done_dialog` function is then used to terminate the dialog box. The status value passed to the `done_dialog` function is returned by the `start_dialog` function and used to exit or continue looping with the while function. The button that should hide the dialog box should use a status value greater than 2 to distinguish the status values returned by the OK or Cancel buttons.

The following DCL syntax defines a sample dialog box named `ch23_ex_hidden` that will be used to demonstrate hiding and showing a dialog box:

```c
ex_hidden : dialog
{
    label = "Hide/Show Example";
    key = "dlg_hide";
    : text
    {
        key = "msg";
        label = "Point: ";
    }
    : row {
        fixed_width = true;
        alignment = right;      
        : button {
            key = "btn_PickPoint";
            action = "pickPoint";
            label = "Pick Point";
            is_default = "true";
            width = 12;
        }
        : spacer { width = 1; }
        cancel_button;
    }
}
```

The following AutoLISP code defines a custom function named hiddendlg that loads the `ex_hidden.dcl` file and displays the `ch23_ex_hidden` dialog box:

```c
; Display the ex_hidden.dcl file
(defun c:hidden (/ dialog_name id status pt)
  (setq dialog_name "ch23_ex_hidden")

  ; Load the DCL file named ex_hidden.dcl
  (setq id (load_dialog (strcat dialog_name ".dcl")))
  
  (setq status 2)
  (while (>= status 2)

    ; Create the dialog box
    (new_dialog dialog_name id "" '(-1 -1))

    ; Added the actions to the Cancel and Pick Point button
    (action_tile "cancel" "(done_dialog 0)")
    (action_tile "btn_PickPoint" "(done_dialog 2)")

    ; Display the point value picked
    (if (/= pt nil)
      (set_tile "msg" (strcat "Point: "
                              (rtos (car pt)) ", "
                              (rtos (cadr pt)) ", "
                              (rtos (caddr pt))))
    )
    
    ; Check the status returned
    (if (= 2 (setq status (start_dialog)))
      (setq pt (getpoint "\nSpecify a point: "))
    )
  )

  ; Unload the dialog box
  (unload_dialog id)
 (princ)
)
```

1『上面的例子值得研读，好好模仿学习。（2020-10-09）』

NOTE: The sample DCL syntax and AutoLISP code can be found in the `ch23_ex_hidden.dcl` and `ch23_ex_hidden.lsp` files, which you can download from www.sybex.com/go/autocadcustomization. Place the files in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the LSP files. Load the LSP file and then enter hiddendlg at the Command prompt. Click the Pick Point button and specify a point in the drawing area to see the dialog box in action.

### 13.4 Exercise: Implementing a Dialog Box for the drawplate Function

In this section, you will create a DCL file that defines a dialog box for use with a version of the drawplate function that was originally introduced in Chapter 12,「Understanding AutoLISP.」The dialog box replaces the width and height prompts and adds an option that controls the creation of the label. The key concepts I cover in this exercise are as follows:

1 Creating a DCL File A DCL file is used to hold a dialog box definition that can be displayed with the AutoLISP programming language.

2 Displaying a Dialog Box A dialog box contained in a DCL file can be loaded and displayed in the AutoCAD drawing environment. Once the dialog box has been displayed, the user can interact with the tiles (or controls) on the dialog box. The choices a user makes can then be used to control the behavior and output of a custom program.

NOTE: The steps in this exercise depend on the completion of the steps in the「Exercise: Deploying the drawplate Function」section of Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs.」If you didn't complete the steps, do so now or start with the `ch23_drawplate.lsp` and `ch23_utility.lsp` sample files available for download from www.sybex.com/go/autocadcustomization. Place these sample files in the MyCustomFiles folder under the Documents (or My Documents) folder, or the location you are using to store the LSP files. Once the sample files are stored on your system, remove the characters `ch23_` from the name of each file.

#### 13.4.1 Creating the drawplate Dialog Box

Chapter 20 was the last chapter in which any changes were made to the drawplate function. At that time, the changes included loading the utility.lsp file and implementing custom help. Here you will create a DCL file named drawplate.dcl and then display it in the new version of the drawplate function.

The following steps explain how to create the DCL file for the drawplate function:

1 In AutoCAD, click the Manage tab Applications panel Visual LISP Editor.

2 In the Visual LISP Editor, click File New File.

3 Click File Save As.

4 In the Save-as dialog box, browse to the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store DCL files.

5 In the File Name text box, type drawplate.

6 Click the Save As Type drop-down list and choose DCL Source Files.

7 Click Save.

8 In the text editor window, type the following: souce code blow.

9 Click File Save.

10 Click Tools Interface Tools Preview DCL In Editor.

11 In the Enter The Dialog Name dialog box, choose drawplate and click OK.

12 Review the dialog box (see Figure 23.5), and click any control to return to the Visual LISP Editor.

Figure 23.5 New dialog box for the drawplate function

```c
/* Draw Plate dialog box Used by drawplate.lsp */ 
drawplate : dialog { 
  label = "Draw Plate"; 
  key = "dlg_drawplate"; 
  // Width text box 
  : edit_box { 
    edit_width = 10; 
    key = "txt_width"; 
    label = "Width"; 
  } 
  // Height text box 
  : edit_box { 
    edit_width = 10; 
    key = "txt_height"; 
    label = "Height"; 
  } 
  // Check box for controlling addition of label 
  : toggle { 
    key = "chk_label"; 
    label = " Add label"; 
  } 
  // Grouping for button tiles 
  : row { 
    fixed_width = true; 
    alignment = right; 
    // Create button 
    : button { 
      key = "btn_create_object"; 
      action = "create_object"; 
      label = "Create"; 
      is_default = "true"; 
      width = 12; 
    } 
    : spacer { width = 1; } 
    // Cancel button 
    cancel_button; 
  } 
}
```

#### 13.4.2 Renaming the Existing drawplate Function

AutoCAD has a few command-naming conventions, and one of those conventions includes prefixing command names with a hyphen. When an AutoCAD command displays a dialog box, often a second command has been created that carries the same name but is prefixed with a hyphen. Commands that are prefixed with a hyphen allow you to access most of the functionality of a dialog box from the Command prompt through a series of prompt options. Before implementing a new version of the drawplate function that displays a dialog box, you must rename the existing drawplate function to conform to the established AutoCAD command-naming standards.

1『上面有关「command-naming」的知识点直觉上很有用。（2020-10-10）』

The following steps explain how to rename the drawplate function to -drawplate:

1 In the Visual LISP Editor, click File Open File.

2 In the Open File To Edit/View dialog box, click the Files Of Type drop-down list, and choose Lisp Source Files.

3 Browse to and select the drawplate.lsp file and click Open.

4 In the text editor area, revise the boldface text:

```c
; Draws a rectangular plate that is 5x2.75 
(defun c:-drawplate ( / pt1 pt2 pt3 pt4 width height insPt textValue cenPt1 cenPt2 cenPt3 cenPt4 old_vars hole_list)
```

5 Revise the boldface text:

```c
; Register the help file for F1/contextual help support 
(if (findfile "DrawPlate.htm") 
  (setfunhelp "c:-drawplate" (findfile "DrawPlate.htm")) 
)
```

6 Click File Save.

#### 13.4.3 Defining a New drawplate Function

Now that you have renamed the existing drawplate function to `-drawplate` and defined the drawplate.dcl file, it is time to implement a new version of the drawplate function. The following steps explain how to add the new version of the drawplate function that will display the Draw Plate dialog box:

1 Open the Visual LISP Editor and the drawplate.lsp file if they are not currently open.

2 In the text editor area, scroll to the bottom of the file and add the following code: source code below.

3 Click File Save.

```c
; Load the utility.lsp file
(load "utility.lsp")

; Custom error handler with command functions
(defun err_drawplate (msg)
  (if (/= msg "Function cancelled")
    (alert (strcat "\nError: " msg))
  )

  (command "._undo" "_e")
  (command "._u")
  
  ; Restore previous error handler
  (setq *error* old_err)
 (princ)
)

; Draws a rectangular plate that is 5x2.75
(defun c:-drawplate ( / pt1 pt2 pt3 pt4 width height insPt textValue
                        cenPt1 cenPt2 cenPt3 cenPt4 old_vars hole_list)

  (setq old_err *error* *error* err_drawplate)

  ; Command function being used in custom error handler
  (*push-error-using-command*)

  (command "._undo" "_be")

  ; Store and change the value of the system variables
  (setq old_vars (get-sysvars '("osmode" "clayer" "cmdecho")))
  (set-sysvars '("osmode" "clayer" "cmdecho") '(0 "0" 0))

  ; Create the layer named Plate or set it current
  (createlayer "Plate" 5)
  (setvar "clayer" "Plate")

  ; Define the width and height for the plate
  (if (= *drawplate_width* nil)(setq *drawplate_width* 5.0))
  (if (= *drawplate_height* nil)(setq *drawplate_height* 2.75))

  ; Get recently used values from the global variables
  (setq width *drawplate_width*)
  (setq height *drawplate_height*)

  ; Prompt the current values
  (prompt (strcat "\nCurrent width: "
		  (rtos *drawplate_width* 2)
		  "  Current height: "
		  (rtos *drawplate_height* 2)))
  
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
          (if (/= width nil)(setq *drawplate_width* width))
      )

      ; Prompt for the height of the plate
      ((= basePt "Height")
          (setq height (getdist (strcat "\nSpecify the height of the plate <"
			                (rtos *drawplate_height* 2) ">: ")))

          ; If nil is returned, use the previous value from the global variable
          (if (/= height nil)(setq *drawplate_height* height))
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
  (setvar "clayer" "Holes")

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
  (setvar "clayer" "Label")
  (createtext insPt "_c" 0.5 0.0 textValue)

  ; Restore the value of the system variables
  (set-sysvars '("osmode" "clayer" "cmdecho") old_vars)

  ; Save previous values to global variables
  (setq *drawplate_width* width)
  (setq *drawplate_height* height)

  (command "._undo" "_e")

  ; Restore previous error handler
  (setq *error* old_err)

  ; End using *push-error-using-command*
  (*pop-error-mode*)

 ; Exit "quietly"
 (princ)
)

; Register the help file for F1/contextual help support
(if (findfile "DrawPlate.htm")
  (setfunhelp "c:-drawplate" (findfile "DrawPlate.htm"))
)

; Draws a rectangular plate and gets input from a dialog box
(defun c:drawplate ( / dialog_name id status pt1 pt2 pt3 pt4
                       width height label insPt textValue cenPt1
                       cenPt2 cenPt3 cenPt4 old_vars hole_list)

  ; Define the width, height, and label for the plate
  (if (= *drawplate_width* nil)(setq *drawplate_width* 5.0))
  (if (= *drawplate_height* nil)(setq *drawplate_height* 2.75))
  (if (= *drawplate_label* nil)(setq *drawplate_label* "1"))

  ; Get recently used values from the global variables
  (setq width *drawplate_width*)
  (setq height *drawplate_height*)
  (setq label *drawplate_label*)

  (setq dialog_name "drawplate")

  ; Load the DCL file named ex_hidden.dcl
  (setq id (load_dialog (strcat dialog_name ".dcl")))
  
  ; Create the dialog box
  (new_dialog dialog_name id "" '(-1 -1))

  ; Sets the default values of the width and height
  (set_tile "txt_width" (rtos width))
  (set_tile "txt_height" (rtos height))

  ; Set the default for the label
  (set_tile "chk_label" label)

  ; Added the actions to the Cancel and Create button
  (action_tile "cancel" "(done_dialog 0)")
  (action_tile "btn_create_object"
               "(setq width (atof (get_tile \"txt_width\")))
                (setq height (atof (get_tile \"txt_height\")))
                (setq label (get_tile \"chk_label\"))
                (done_dialog 1)"
  )

  (setq status (start_dialog))

  ; Unload the dialog box
  (unload_dialog id)

  ; Check the status returned
  (if (= status 1)
    (progn
      (setq old_err *error* *error* err_drawplate)

      ; Command function being used in custom error handler
      (*push-error-using-command*)

      ; Store and change the value of the system variables
      (setq old_vars (get-sysvars '("osmode" "clayer" "cmdecho")))
      (set-sysvars '("osmode" "clayer" "cmdecho") '(0 "0" 0))

      (command "._undo" "_be")
      
      ; Create the layer named Plate or set it current
      (createlayer "Plate" 5)
      (setvar "clayer" "Plate")

      (setq basePt (getpoint "\nSpecify base point for plate: "))

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
      (setvar "clayer" "Holes")

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

      (if (= "1" label)
        (progn
          ; Set the insertion point for the text label
          (setq insPt (getpoint "\nSpecify label insertion point: "))

          ; Define the label to add
          (setq textValue 
            (strcat "Plate Size: "
                    (vl-string-right-trim " .0" (rtos width 2 2))
                    "x"
                    (vl-string-right-trim " .0" (rtos height 2 2))
            )
          )

          ; Create label
          (createlayer "Label" 7)
          (setvar "clayer" "Label")
          (createtext insPt "_c" 0.5 0.0 textValue)
        )
      )

      ; Restore the value of the system variables
      (set-sysvars '("osmode" "clayer" "cmdecho") old_vars)

      ; Save previous values to global variables
      (setq *drawplate_width* width)
      (setq *drawplate_height* height)
      (setq *drawplate_label* label)

      (command "._undo" "_e")

      ; Restore previous error handler
      (setq *error* old_err)

      ; End using *push-error-using-command*
      (*pop-error-mode*)
    )
  )

 ; Exit "quietly"
 (princ)
)
```

#### 13.4.4 Testing the drawplate.lsp Changes

The following steps explain how to test the `-drawplate` function in the drawplate.lsp file:

1 Create a new drawing.

2 Start the appload command. Load the LSP files drawplate.lsp and utility.lsp. If the File Loading - Security Concern message box is displayed, click Load.

3 At the Command prompt, type `-drawplate` and press Enter.

4 At the Specify base point for the plate or `[Width/Height]: prompt`, type w and press Enter.

5 At the Specify the width of the plate `<5.0000>: prompt`, type 3 and press Enter.

6 At the Specify base point for the plate or `[Width/Height]: prompt`, type h and press Enter.

7 At the Specify the height of the plate `<2.7500>: prompt`, type 4 and press Enter.

8 At the Specify base point for the plate or `[Width/Height]: prompt`, pick a point in the drawing area to draw the plate and holes based on the width and height values specified.

9 At the Specify label insertion point: prompt, pick a point in the drawing area below the plate to place the text label. AutoCAD draws the completed plate, as expected.

1-2『如何在一个 lsp 文件里调用另外一个 lsp 文件。直接在 lsp 里写加载语句 `(load "utility.lsp")`，然后在 CAD 里用命令 `appload` 同时加载这两个函数即可。做一张任意卡片。』 —  — 已完成

The following steps explain how to test the revised version of the drawplate function:

1 At the Command prompt, type drawplate and press Enter. The Draw Plate dialog box is displayed and uses the width and height values specified by the -drawplate function.

2 In the Draw Plate dialog box, in the Width text box, enter 5.

3 In the Height text box, enter 5.

4 Clear the Add Label check box.

5 Click Create.

6 At the Specify base point for the plate or `[Width/Height]: prompt`, pick a point in the drawing area to draw the plate and holes based on the width and height values specified. AutoCAD draws the completed plate without the label, as expected.

7 At the Command prompt, type drawplate and press Enter.

8 In the Draw Plate dialog box, select Add Label.

9 Click Create, and specify the insertion point for the plate and label. AutoCAD draws the completed plate with a label this time.