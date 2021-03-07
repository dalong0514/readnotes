# 0212. Working with ActiveX/COM Libraries (Windows only)

The AutoLISP® functions you have learned up to this point have been, for the most part, platform neutral and are unofficially known as Classic AutoLISP or Core AutoLISP. Starting with the Autodesk® AutoCAD® 2000 program, AutoLISP saw an architecture change that allowed for the use of the Microsoft ActiveX technology. ActiveX is a technology that enables applications to communicate and exchange information. COM (Component Object Model) is a library of objects that let you make changes to or query exposed objects. COM is an example of ActiveX.

1『这里 ActiveX/COM 本质上是一个库，做一张术语卡片。（2021-03-06）』

In this chapter, you will learn the basics of using ActiveX with AutoLISP and how to leverage the AutoCAD, Microsoft Windows, and Microsoft Office COM libraries. Although this chapter doesn't go into great depth, it will give you a starting point and a general understanding of the functions you need to become familiar with in order to use ActiveX and access COM libraries. The primary reasons to use COM are to monitor actions in AutoCAD with reactors, access external applications such as Microsoft Word or Excel, and work with complex objects, such as tables and multileaders.

## 12.1 Understanding the Basics of ActiveX

ActiveX is the technology that allows for the use of COM. It is often associated with Visual Basic for Applications (VBA) and Visual Basic (VB) scripting these days, but it can be used by many modern programming languages, such as VB.NET and C++. Although many people refer to ActiveX and COM as the same thing, they aren't. ActiveX is the technology that was developed by Microsoft to allow software developers to expose objects using COM, thereby letting programmers communicate with the programs in new ways.

In general, there are three concepts you need to understand about working with ActiveX in AutoLISP programs: 1) Classes, objects, and collections. 2) Methods and properties. 3) Variant and array data types.

### 12.1.1 Accessing Classes, Objects, and Collections

Classes are the elements on which a COM library is built — think of them as a recipe. The AutoCAD COM library has classes for the AutoCAD application, a drawing (known as a document) file, and the graphical and nongraphical objects that are stored in a drawing. An object is an in-memory and unique instance of a class. Although a collection is also an object, it is a container for objects of the same type.

#### Working with Objects

The vla-object data type is used in AutoLISP to represent an object or collection. (You'll learn how to work with the AutoCAD COM library in the「Using the AutoCAD COM Library」section, and with the COM libraries related to Windows and Microsoft Office in the「Leveraging the Windows and Microsoft Office COM Libraries」section, later in this chapter.) Many of the objects you will want to work with can be accessed using properties and methods described in the next section. However, there are some objects that you must create or get an instance of before you can work with them.

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

1-2『测试过了，word 2016 版的 program ID 是 `Word.Application.16`。补充：后面的信息得知，其实没必要写版本号，直接 `Word.Application`。（2021-03-06）』

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

跑了下，完全没问题，获取到了 3 个布局的信息。这里可以深挖的信息量很多的：1）此时才了解到，一个实体对象其 DXF 码 410 的值「model」就是这里的「布局」名称。2）获取当前「活动」图纸的所有数据 `(vla-get-activedocument (vlax-get-acad-object))`，这个函数极其重要。3）里面涉及到很多函数可以去官方文档研读，而且可以顺藤摸瓜找到更多实用的函数。比如将函数 `vla-get-layouts` 更改为 `vla-get-blocks` 即可获取到所有块的数据。而且对象数据的全景图详见下面的官方文档链接，要反复研读。（2021-03-06）

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

### 12.1.2 Specifying Properties and Invoking Methods

A class uses two different approaches to expose itself to a programming language such as AutoLISP or VBA: properties and methods. They are available when an instance of a class is created in memory as an object. Properties are used to describe and query the characteristics of an object. For example, the Length and TrueColor properties of a Line object are used to specify that line's length and color. Properties can be designated as read-only.

Methods are used to manipulate and perform an action on an object. ActiveX allows you to define two types of methods: subroutines and functions. Subroutines never return a value; functions can return a single value. For example, the Delete and Copy methods are used to remove or duplicate an object in a drawing. The Delete method doesn't return a value, whereas the Copy method returns a new instance of an object.

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

### 12.1.3 Getting and Specifying the Value of an Object's Property

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

### 12.1.4 Invoking an Object Method

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

### 12.1.5 Working with Variants and Arrays

vla-object isn't the only new data type that you will have to understand when working with ActiveX. Many methods and properties use what is known as a variant. The variant data type is the chameleon of data types; it can represent any supported data type. A variant in AutoLISP is represented by the vla-variant data type. Arrays are yet another type of data that you will need to become familiar with. An array is represented by the vla-array data type and is similar to the AutoLISP list data type.

2『这里的 Variants and Arrays，做一张术语卡片。（2021-03-07）』—— 已完成

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
0.0 (vlax-safearray-put-element pt2D 1 5.25) 
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

## 12.2 Importing COM Libraries

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

## 12.3 Using the AutoCAD COM Library

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

### 12.3.1 Accessing the AutoCAD Application and Current Drawing Objects

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

### 12.3.2 Working with Graphical and Nongraphical Objects in the Current Drawing

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

### 12.3.3 Monitoring Events with Reactors

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

## 12.4 Leveraging the Windows and Microsoft Office COM Libraries

The Microsoft ecosystem is full of hidden gems that can increase your productivity and improve everyday workflows. Many programs that are available for free or for purchase let you create proposals or manipulate information in a database, but Windows and Microsoft Office allow you to leverage what they do best by using the COM libraries that they expose. There aren't many companies that allow you to manipulate or access their programs programmatically like Microsoft does, so take advantage of these benefits whenever possible.

Using the COM libraries for Windows and Microsoft Office, you can accomplish the following:

1 Create desktop shortcuts, expand environment variables, or even launch an external application.

2 Create and print documents using Microsoft Word.

3 Create, manipulate, and print spreadsheets using Microsoft Excel.

4 Create email messages and access contact lists using Microsoft Outlook.

5 Access and manipulate data in a database using Microsoft Access.

For specific information on each of these COM libraries, refer to the documentation that Microsoft publishes with Windows and the Microsoft Office application you are interested in working with. Your favorite Internet search engine will also be of help; search on the keywords「Windows Shell object documentation」or「Microsoft Office 2013 Release Developers」to get started.

### 12.4.1 Accessing the Windows Shell Object

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

### 12.4.2 Working with Microsoft Office

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