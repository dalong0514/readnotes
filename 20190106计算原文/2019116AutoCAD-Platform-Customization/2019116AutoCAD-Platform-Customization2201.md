# 2201. Working with ActiveX/COM Libraries (Windows only)

The AutoLISP® functions you have learned up to this point have been, for the most part, platform neutral and are unofficially known as Classic AutoLISP or Core AutoLISP. Starting with the Autodesk® AutoCAD® 2000 program, AutoLISP saw an architecture change that allowed for the use of the Microsoft ActiveX technology. ActiveX is a technology that enables applications to communicate and exchange information. COM (Component Object Model) is a library of objects that let you make changes to or query exposed objects. COM is an example of ActiveX.

In this chapter, you will learn the basics of using ActiveX with AutoLISP and how to leverage the AutoCAD, Microsoft Windows, and Microsoft Office COM libraries. Although this chapter doesn't go into great depth, it will give you a starting point and a general understanding of the functions you need to become familiar with in order to use ActiveX and access COM libraries. The primary reasons to use COM are to monitor actions in AutoCAD with reactors, access external applications such as Microsoft Word or Excel, and work with complex objects, such as tables and multileaders.

Understanding the Basics of ActiveX

ActiveX is the technology that allows for the use of COM. It is often associated with Visual Basic for Applications (VBA) and Visual Basic (VB) scripting these days, but it can be used by many modern programming languages, such as VB.NET and C++. Although many people refer to ActiveX and COM as the same thing, they aren't. ActiveX is the technology that was developed by Microsoft to allow software developers to expose objects using COM, thereby letting programmers communicate with the programs in new ways.

In general, there are three concepts you need to understand about working with ActiveX in AutoLISP programs:

Classes, objects, and collections

Methods and properties

Variant and array data types

Accessing Classes, Objects, and Collections

Classes are the elements on which a COM library is built—think of them as a recipe. The AutoCAD COM library has classes for the AutoCAD application, a drawing (known as a document) file, and the graphical and nongraphical objects that are stored in a drawing. An object is an in-memory and unique instance of a class. Although a collection is also an object, it is a container for objects of the same type.

Working with Objects

The vla-object data type is used in AutoLISP to represent an object or collection. (You'll learn how to work with the AutoCAD COM library in the「Using the AutoCAD COM Library」section, and with the COM libraries related to Windows and Microsoft Office in the「Leveraging the Windows and Microsoft Office COM Libraries」section, later in this chapter.) Many of the objects you will want to work with can be accessed using properties and methods described in the next section. However, there are some objects that you must create or get an instance of before you can work with them.

For example, you can use the vlax-create-object function to create an instance of an application or secondary object that isn't accessible from an object that is already in memory. The vlax-get-object function can be used to get an instance of an object that is already in memory. When an object is in memory, it can be accessed and manipulated. The following shows the syntax of the vlax-create-object and vlax-get-object functions:

(vlax-create-object prog_id) (vlax-get-object prog_id)

The prog_id argument is a string that represents the program ID of the object you want to create or get. The program ID follows the syntax of vendor.component, and it can optionally have a version number as well, for a syntax of vendor.component.version. Typically, vendor is the name of the software or company that created the component, whereas component is commonly a class.

For example, if you wanted to create or check for an instance of AutoCAD you would use the program ID of AutoCAD.Application. The AutoCAD program ID optionally supports a version number that allows you to look for a specific AutoCAD release. The version number always consists of a major value, while some version numbers can contain both a major and a minor value. The major version of 19 is shared between AutoCAD 2013 and 2014, but if you want to refer to AutoCAD 2014 you use the minor number of 1. The program ID for AutoCAD 2014 is AutoCAD.Application.19.1. If you want to reference AutoCAD 2015, you use AutoCAD.Application.20 for the program ID. Refer to the AutoCAD Help system for the version number assigned to your AutoCAD installation.

The vlax-create-object and vlax-get-object functions return a vla-object if a new object is created or if an object with the program ID is already in memory; nil is returned if the object couldn't be created or retrieved from memory. The following shows how to create a new instance of the AutoCAD True Color (AcCmColor) and Microsoft Word (Application) objects. The AcCmColor object is used to manipulate the color value assigned to a drawing object.

; Creates an instance of an AutoCAD True Color object (setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) #<VLA-OBJECT IAcadAcCmColor 000000002dcdd650> ; Creates an instance of the most recently used Microsoft Word application (setq wordObj (vlax-create-object "Word.Application")) #<VLA-OBJECT _Application 000000002f1e3c78> ; Attempts to create an instance of the Microsoft Word 2010 application ; but the application is not installed on this workstation (setq wordObj (vlax-create-object "Word.Application.14")) nil ; Creates an instance of the Microsoft Word 2013 application; installed (setq wordObj (vlax-create-object "Word.Application.15")) #<VLA-OBJECT _Application 000000002f1e3b98>

The following shows how to get an instance of the Microsoft Word application that has already been started:

; Gets an instance of a non-version-specific release of the ; Microsoft Word application that is in memory (setq wordObj (vlax-get-object "Word.Application")) #<VLA-OBJECT _Application 000000000a92e568>

Although you can use the vlax-get-object function to get an instance of an object in memory, or create a new instance of an object with the vlax-create-object function, the vlax-get-or-create-object function combines the functionality of both. If an object already exists, vlax-get-or-create-object returns the object and, if not, a new instance of the object is created. vlax-get-or-create-object has the same syntax as vlax-create-object.

; Gets/creates an instance of the most recently used Microsoft Word application (setq wordObj (vlax-get-or-create-object "Word.Application")) #<VLA-OBJECT _Application 000000000a92e568>

When an object is created with the vlax-create-object or vlax-get-or-create-object function, it must be released from memory when it is no longer used. You use the vlax-release-object function to release an object; the function must be passed the value returned by the vlax-create-object or vlax-get-or-create-object function. The vlax-release-object function returns a random integer value that has no specific meaning if the value it was passed is a valid object; an error is returned if the value passed wasn't a valid object that could be released.

The following code shows how to release an object created with the vlax-create-object or vlax-get-or-create-object function:

(vlax-release-object wordObj) 0 (vlax-release-object cObj) ; error: null interface pointer: #<VLA-OBJECT 0000000000000000>

Working with Collections

Collections are objects that can be queried and modified using properties and methods, but they are also containers that hold similar objects. A collection fundamentally is similar to a symbol table; you can work with a symbol table and add new objects to it, but you can't create a new symbol table. All the collections that you need in order to work with AutoCAD objects are defined as part of the AutoCAD ActiveX API. For example, a Layers collection contains all of the Layer objects in a drawing, and a Documents collection contains all the open drawings (or Document objects) in the current AutoCAD session. You can get an object from a collection using the Item method, add a new object to a collection using the Add method, and remove an object from a collection using the Delete method.

If you want to step through a collection and perform a set of statements on each object, you can use the vlax-for AutoLISP function, which is similar to the foreach function. The following shows the syntax of the vlax-for function:

(vlax-for var coll [expressionN …])

Here are its arguments:

var The var argument specifies the user-defined variable, which you use to reference the current item of the coll argument as the collection is being stepped through.

coll The coll argument specifies a collection object of the vla-object data type, which should be stepped through one item at a time.

expressionN The expressionN argument represents the expressions that should be executed when each object in the coll argument is found. The object is located using the name in the var argument.

The following is an example of the vlax-for function that steps through the Layouts collection and returns the name of each layout in a drawing:

; Imports the functions for the AutoCAD COM library, ; if not already available (vl-load-com) ; Gets the current drawing (setq curDoc (vla-get-activedocument (vlax-get-acad-object))) ; Gets the Layouts collection (setq layouts (vla-get-layouts curDoc)) ; Creates a report header (prompt (strcat "\nLayouts count: " (itoa (vla-get-count layouts)))) (prompt "\nLayouts: ") ; Steps through the objects in the collection (vlax-for layout layouts (prompt (strcat "\n " (vla-get-name layout))) ) ; The output from the previous expressions Layouts count: 3 Layouts: Layout1 Layout2 Model

You can use the vlax-map-collection function to execute a single AutoLISP function on each object in a collection. The following shows the syntax of the vlax-map-collection function:

(vlax-map-collection coll 'func)

Here are its arguments:

coll The coll argument specifies the collection object, of the vla-object data type, that should be stepped through one item at a time.

‘func The func argument represents the function you want to execute on each object in the coll argument. An apostrophe must be placed in front of the function name to let AutoLISP know it is a value that should not be evaluated.

Specifying Properties and Invoking Methods

A class uses two different approaches to expose itself to a programming language such as AutoLISP or VBA: properties and methods. They are available when an instance of a class is created in memory as an object. Properties are used to describe and query the characteristics of an object. For example, the Length and TrueColor properties of a Line object are used to specify that line's length and color. Properties can be designated as read-only.

Methods are used to manipulate and perform an action on an object. ActiveX allows you to define two types of methods: subroutines and functions. Subroutines never return a value; functions can return a single value. For example, the Delete and Copy methods are used to remove or duplicate an object in a drawing. The Delete method doesn't return a value, whereas the Copy method returns a new instance of an object.

The objects in a COM library are typically unique, so the vlax-dump-object function can be used to list the properties and methods that a particular object supports. The following shows the syntax of the vlax-dump-object function:

(vlax-dump-object obj [flag])

Here are its arguments:

obj The obj argument is a value of the vla-object type, which is returned by a method or property, or is available as the var argument of the vlax-for function.

flag The flag argument is an optional argument that allows you to specify whether the returned output lists only the properties or the properties and methods supported by an object. A value of T returns both supported properties and methods, whereas no value or a value of nil returns only the supported properties.

Here's an example that shows how to list the properties and methods of an object with the vlax-dump-object function:

(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) #<VLA-OBJECT IAcadAcCmColor 000000002dcdd650> (vlax-dump-object clrObj T) ; IAcadAcCmColor: AutoCAD AcCmColor Interface ; Property values: ; Blue (RO) = 0 ; BookName (RO) = "" ; ColorIndex = 0 ; ColorMethod = 195 ; ColorName (RO) = "" ; EntityColor = -1023410176 ; Green (RO) = 0 ; Red (RO) = 0 ; Methods supported: ; Delete () ; SetColorBookColor (2) ; SetNames (2) ; SetRGB (3) T

(RO) after a property name indicates that the property is read-only and the value cannot be changed. The number in the parentheses after each method listed in the Methods supported section of the output indicates the number of arguments that the method expects; no number in the parentheses indicates the method doesn't accept any argument values.

Getting and Specifying the Value of an Object's Property

The vlax-get-property and vlax-put-property functions are used to query and set the values of an object property. The vlax-get-property function returns the current value of the object property; the vlax-put-property function returns nil if the value was successfully assigned to the object's property. When the value of a property is changed with the vlax-put-property function, the object is updated immediately. Refer to the COM library's documentation for the type of value that will be returned or that the property expects. See the section「Using the AutoCAD COM Library」to learn how to access information on the AutoCAD COM library help.

The following shows the syntax of the vlax-get-property and vlax-put-property functions:

(vlax-get-property obj 'prop) (vlax-put-property obj 'prop val)

Here are their arguments:

obj The obj argument is a value of the vla-object type, which is returned by a method or property, or is available as the var argument of the vlax-for function.

‘prop The prop argument specifies the name of the particular property you want to query or set. The property name must be prefixed with an apostrophe. An apostrophe must be placed in front of the property name to let AutoLISP know it is a value that should not be evaluated.

val The val argument specifies the new value to be assigned to the property.

Here are some examples that show how to get and set a property value of an object. In these examples, you work with the ColorMethod and ColorIndex properties of an AutoCAD True Color object:

(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) ; Sets the value of the ColorMethod property to acColorMethodByACI ; acColorMethodByACI indicates that the color should ; be based on an ACI color value (vlax-put-property clrObj 'ColorMethod acColorMethodByACI) nil ; Gets the current value of the ColorIndex property ; A value of 256 specifies that the color represents ByLayer (vlax-get-property clrObj 'ColorIndex) 256 ; Releases the AutoCAD True Color object because it was created with ; the vlax-create-object (vlax-release-object clrObj)

In the previous example, acColorMethodByACI is a constant variable value that is exposed as part of the AutoCAD COM library. This constant value tells AutoCAD you want to work with one of the standard 255 ACI colors, and not a True or Color Book color.

You can determine whether an object supports a specific property by using the vlax-property-available-p function. A value of T is returned if the object supports the specified property. The following shows the syntax of the vlax-property-available-p function. See the argument descriptions of the vlax-get-property function earlier in this section:

(vlax-property-available-p obj 'prop)

Invoking an Object Method

The vlax-invoke-method function is used to execute an object method and pass to that method any argument values that are expected. A value can be returned by the method through the executed vlax-invoke-method function or by reference to the variables passed to the method. Refer to the particular method's documentation for the type of values that can be passed or for an explanation of the values returned by the method. (See the section「Using the AutoCAD COM Library」later in this chapter to learn how to access information on the AutoCAD COM library help.)

The following shows the syntax of the vlax-invoke-method function:

(vlax-invoke-method obj 'method [argN …])

Here are its arguments:

obj The obj argument is a value of the vla-object type, which is returned by a method or property or is available as the var argument of the vlax-for function.

‘method The method argument is the name of the method you want to execute. The method name must be prefixed with an apostrophe. An apostrophe must be placed in front of the method name to let AutoLISP know it is a value that should not be evaluated.

argN The argN argument is the value(s) to be passed to the method. If the argument you specify is meant to return a value, that argument must be prefixed with an apostrophe. The documentation in the AutoCAD Help system for the method will let you know if a value is passed back to the variable specified as an argument instead of returned by the function. For example, the GetBoundingBox method returns values to its two arguments that represent the minimum and maximum extents of an object. The code statement would look similar to (vlax-invoke-method lineObj 'GetBoundingBox 'min 'max). See the AutoCAD COM library documentation for additional information.

Here is an example that shows how to invoke a method. This example sets the Red element of the RGB color to a value of 255 and the Blue and Green elements of the object to 0. The result would be a pure color of red if the color object was assigned to an object. The Red, Green, and Blue properties of an AutoCAD True Color object are read-only; the SetRGB method is used to assign new values to the three color elements of the object:

(setq clrObj (vlax-create-object (strcat "AutoCAD.AcCmColor." (substr (getvar "acadver") 1 2)))) (vlax-invoke-method clrObj 'SetRGB 255 0 0) nil (vlax-release-object clrObj)

You can determine whether an object supports a method by using the vlax-method-applicable-p function. A value of T is returned if the object does support the specified method. The following shows the syntax of the vlax-method-applicable-p function. The arguments are the same as described earlier in this section:

(vlax-method-applicable-p obj 'method)

Working with Variants and Arrays

vla-object isn't the only new data type that you will have to understand when working with ActiveX. Many methods and properties use what is known as a variant. The variant data type is the chameleon of data types; it can represent any supported data type. A variant in AutoLISP is represented by the vla-variant data type. Arrays are yet another type of data that you will need to become familiar with. An array is represented by the vla-array data type and is similar to the AutoLISP list data type.

Making Variants

Most properties and methods return or expect values of a specific type, but there will be times when you will need to assign a property or pass a method a variant value. Some data structures can represent multiple values, such as a point or Xdata, and in these situations the AutoCAD COM library is designed to return or accept a variant value. You define a variant by using the vlax-make-variant function.

The following shows the syntax of the vlax-make-variant function:

(vlax-make-variant [val [type]])

Here are its arguments:

val The val argument is the value to be assigned to the variant and is optional.

type The type argument is an optional integer that specifies the data type that the value should represent. As an alternative, you can use a constant variable value that has the same meaning. Table 22.1 lists some of the most common data types and the integer and constant variable values you can use. Refer to the vlax-make-variant topic in the AutoCAD Help system for more supported values.

Table 22.1 Common data types used with the vlax-make-variant function

Data type Integer value Constant variable value

Integer 2 vlax-vbInteger

Double 5 vlax-vbDouble

String 8 vlax-vbString

Here is an example that shows how to make a variant that holds an integer value of 5:

(setq var (vlax-make-variant 5 vlax-vbInteger)) #<variant 2 5>

When neither the val nor the type argument is provided to the vlax-make-variant function, an empty variant is returned. The value and type of a variant can be returned using the vlax-variant-value and vlax-variant-type functions. The value assigned to a variant can't be changed, but the data type a variant represents can be changed using the vlax-variant-change-type function, making it possible to change an integer to a double or string. For example, you might want to change an integer or double value to a string so that it can be displayed to the user as part of a message or prompt string.

The following shows the syntax of the vlax-variant-value, vlax-variant-type, and vlax-variant-change-type functions:

(vlax-variant-value variant) (vlax-variant-type variant) (vlax-variant-change-type variant type)

Defining Arrays

The array data type is similar to the AutoLISP list data type, but typically an array is made up of a specified number of elements. You will remember that a list can hold any number of elements. A common use for arrays with the AutoCAD COM library is to represent a point list. Arrays can also be used to pass multiple objects to a method or for times when you want to return more than one value from a custom function.

The vlax-make-safearray function is used to create a new array based on a specific data type and number of elements. The following shows the syntax of the vlax-make-safearray function:

(vlax-make-safearray type '(lbound. ubound) ['(lbound. ubound)])

Here are its arguments:

type The type argument is an integer or equivalent constant variable that represents the data type of the elements within the array. These are the same data types that the vlax-make-variant function supports. Refer to the vlax-make-safearray topic in the AutoCAD Help system for supported values.

'(lbound. ubound) The lbound part of the argument is an integer that represents the lower element of the array, typically 0. The ubound part of the argument is an integer that represents the upper element of the array. If you want to specify an array of three elements, set lbound to 0 and ubound to 2.

NOTE 22.1

The optional ['(lbound. ubound)] argument allows you to define a matrix. For information on matrices, see the vlax-tmatrix function in the AutoCAD Help system and the TransformBy method in the AutoCAD COM library.

Here are examples that define arrays:

; Array of three strings (setq arStrs (vlax-make-safearray vlax-vbString '(0. 2))) #<safearray…> ; 2D point (array of two doubles) (setq pt2D (vlax-make-safearray vlax-vbDouble '(0. 1))) #<safearray…>

After an array has been defined, you can add values to the elements within the array by using the vlax-safearray-put-element function. You can retrieve values within an array by using the vlax-safearray-get-element function.

The following shows the syntax of the vlax-safearray-put-element and vlax-safearray-get-element functions:

(vlax-safearray-put-element array idx val) (vlax-safearray-get-element array idx)

Here are its arguments:

array The array argument is a value of the vla-array data type, such as that returned by the vlax-make-safearray function.

idx The idx argument is an integer that represents an element within the array. The value cannot be less than the lower or greater than the upper element of the array.

val The val argument is the value that is to be assigned to the element in the array.

Here are examples that assign values to and get values from the arrays defined in the earlier examples:

; Assign strings to a three-element array (vlax-safearray-put-element arStrs 0 "Qty") "Qty" (vlax-safearray-put-element arStrs 1 "Model") "Model" (vlax-safearray-put-element arStrs 2 "Description") "Description" ; Assign double/real values to a two-element array (vlax-safearray-put-element pt2D 0 0.0) 0.0 (vlax-safearray-put-element pt2D 1 5.25) 5.25 ; Get the first element in an array (vlax-safearray-get-element pt2D 0) 0.0

To create a 2D or 3D point array, you can use the vlax-3d-point function. Or you can assign multiple values to an array based on the values of a list with the vlax-safearray-fill function. Here are examples that use the vlax-3d-point and vlax-safearray-fill functions:

; 2D point (setq pt2D (vlax-3d-point 0.0 5.25)) ; 3D point (setq pt3D (vlax-3d-point 0.0 5.25 1.0)) ; Adds three strings to a three-element array (vlax-safearray-fill arStrs '("Qty" "Model" "Description"))

Table 22.2 lists some additional functions that can be helpful when working with arrays. For more information on the functions mentioned in the table, see the AutoCAD Help system.

Table 22.2 Additional array functions

Function Description

vlax-safearray-type Returns an integer that represents the data type of the values contained in an array

vlax-safearray-get-dim Returns an integer that represents the number of elements in an array

vlax-safearray-get-l-bound Returns an integer that represents the index of the lower element in an array

vlax-safearray-get-u-bound Returns an integer that represents the index of the upper element in an array

vlax-safearray->list Returns a list containing the values of all elements in an array

Importing COM Libraries

Although you can access the properties and methods of an object using the functions covered in the「Specifying Properties and Invoking Methods」section, importing a COM library can make coding easier. When you import a COM library, that library defines an AutoLISP function for the properties and methods of each class in the library. The newly defined functions that result from importing a COM library reduce the amount of code that needs to be written.

For example, the vla-get-red function can be used instead of the vlax-get-property function to get the current value of the Red property of an AutoCAD True Color object. The same is true with methods; vla-delete is the equivalent of using the vlax-invoke-method function with the Delete method name as an argument. The following two code statements produce the same result:

(vlax-get-property clrObj 'Red) (vla-get-red clrObj)

The properties and methods exposed by the AutoCAD COM library can be imported into a current drawing with the vl-load-com function. However, if you want to import the functions of another COM library for use with AutoLISP you must use the vlax-import-type-library function. The vlax-import-type-library function returns T if the COM library was successfully imported. An error is returned if the COM library couldn't be imported.

The following shows the syntax of the vlax-import-type-library function:

(vlax-import-type-library :tlb-filename filename [:methods-prefix me_prefix :properties-prefix prop_prefix :constants-prefix con_prefix] )

Here are its arguments:

filename The filename argument represents the path to and the filename of the COM library to be imported.

me_prefix, prop_prefix, and con_prefix These arguments are optional strings that represent the prefix to be appended to the property, method, and constant names in the COM library being imported to ensure the names are unique from other imported libraries.

Here is an example that shows how to import the COM library for the Windows Shell object:

(vlax-import-type-library :tlb-filename "c:\\windows\\system32\\wshom.ocx" :methods-prefix "wshm-" :properties-prefix "wshp-" :constants-prefix "wshk-" )

Although you can import a COM library more than once, you should avoid doing so, since multiple imports can add to the time it takes for a custom function to execute. The following example shows how you can use a global variable to determine whether the COM library associated with the Windows Shell object has already been imported into the current session:

; Imports the Windows Host Scripting Library (if (= wshLibImported nil) (progn (vlax-import-type-library :tlb-filename "c:\\windows\\system32\\wshom.ocx" :methods-prefix "wshm-" :properties-prefix "wshp-" :constants-prefix "wshk-" ) (setq wshLibImported T) ) (princ) )

Using the AutoCAD COM Library

Once the AutoCAD COM library has been imported, you can use the newly exposed functions to do the following:

Access the objects associated with the AutoCAD application and current drawing

Get the graphical and nongraphical objects stored in the current drawing

Perform geometric calculations

Register reactors and monitor changes made to a drawing or actions performed by the user

TIP

Before you use the AutoCAD COM library, make sure that you execute the vl-load-com function to ensure the library has been imported.

The classes in the AutoCAD COM library are organized using a hierarchy. The AutoCAD application is at the top, followed by the drawings (or documents) opened, and then the objects in a drawing. Once you have a drawing object, you can then access the nongraphical objects stored in the drawing. Graphical objects that have been placed in model space or on a layout are accessed through the special named blocks *ModelSpace and *PaperSpace0 of, which are stored in the Blocks or Layouts collection. A drawing can contain more than one *PaperSpace block; each successive paper space block name in the drawing is incremented by 1.

NOTE 22.3

You can access the AutoCAD application object from most objects in the AutoCAD COM library by using the Application property, which can be accessed with the vla-get-application function.

You can learn about the classes in the AutoCAD COM library by using the AutoCAD Object Model in the AutoCAD Help system. The AutoCAD Object Model can be found by going to http://help.autodesk.com/view/ACD/2015/ENU/files/homepage_dev.htm and clicking the AutoCAD Object Model link. The AutoCAD Object Model (see Figure 22.1) shows the hierarchy of the AutoCAD COM library structure.

Figure 22.1 Hierarchy of the AutoCAD COM library

When you click the object model, the reference topic for the associated class/object opens. The Help reference page provides information on how an object can be created, along with the properties and methods supported by the object. The content is intended primarily for the VBA programmer, but it is still very useful if you're working with the AutoCAD COM library in AutoLISP.

For the most part, adding vla- as a prefix for a method name or vla-put- or vla-get- as a prefix for a property name is all that is needed to convert the information contained in the VBA documentation for use with AutoLISP. (Remember that you must use vl-load-com to ensure that the AutoCAD COM library has been imported before you can use it.) A majority of the reference topics for object properties and methods also contain example code for use with AutoLISP. You can copy and modify the example code as needed. The ActiveX Developer's Guide can also help you learn more about the AutoCAD COM library.

You can access both the ActiveX Reference and ActiveX Developer's topics by using the AutoCAD Object Library Reference and Developer's Guide links in the ActiveX/VBA section of the Developer homepage in the AutoCAD Help system.

TIP

When you are using the Visual LISP® Editor, you can highlight the name of an imported function in the editor window and press Ctrl+F1 to open the related topic in the ActiveX Reference. Using this approach, you open the acadauto.chm file to the topic that discusses the object, method, or property.

Accessing the AutoCAD Application and Current Drawing Objects

Once the AutoCAD COM library has been imported with the vl-load-com function, you can use the vlax-get-acad-object function to get the AcadApplication object that represents the AutoCAD application. As I mentioned earlier, the AutoCAD application object is the topmost object in the hierarchy that is the AutoCAD COM library. To learn which methods and properties an AcadApplication object supports, you can use the vlax-dump-object function with the value returned by the vlax-get-acad-object function. Here is an example that shows how to use the vlax-get-acad-object function:

; Gets the AutoCAD application object (setq acad (vlax-get-acad-object))

The AcadApplication object contains a property named ActiveDocument, which returns an AcadDocument object that represents the current drawing. Use the vla-get-activedocument function to get the current drawing object. Here is an example:

; Gets the current drawing (setq curDoc (vla-get-activedocument acad))

Working with Graphical and Nongraphical Objects in the Current Drawing

The graphical and nongraphical objects stored in a drawing can be accessed using ActiveX. As defined by the drawing architecture, all graphical objects are stored in a Block object and can be accessed from the Blocks collection. Model space and paper space are special types of Block objects that you can manipulate without performing any special operation. The Blocks collection is just one of several collections that allow you to create and access nongraphical objects in a drawing.

NOTE 22.5

The vla-object data type isn't compatible with the ename data type. You can convert vla-object values to an entity name (ename) by using the vlax-vla-object->ename function. The vlax-ename->vla-object function converts an ename to a vla-object data type. Additionally, you can use the vla-get-handle function to get an object's handle and then use the handent function to get an object's ename based on a valid handle. These functions are helpful if you are mixing the use of Classic AutoLISP functions that work with the ename data type, such as entget or ssname, and those used to work with objects of the AutoCAD COM library. Examples of these functions, with the exception of vlax-vla-object->ename, can be found in the ch22_mswin_office.lsp file, which you can download from this book's web page, www.sybex.com/go/autocadcustomization.

In the previous section, you learned how to get the object that represents the active document. The next example shows how to get the ModelSpace or PaperSpace object based on the active space. You can determine the correct active space by using the ActiveSpace property of the current document.

; Get a reference to the current space in AutoCAD (if (= (vla-get-activespace curDoc) acModelSpace) (setq space (vla-get-modelspace curDoc)) (setq space (vla-get-paperspace curDoc)) )

When you want to add an object, such as a Layer object, to a collection, you can use one of the many Add methods available through the AutoCAD COM library. The following exercise shows how to create a function that checks for the existence of a layer and that creates the layer if it's not found; it then sets the layer as current by using the AutoCAD COM library and ActiveX. The function is similar to the createlayer function that you defined in the utility.lsp file in the various exercises throughout this book.

Create a LSP file named ActiveX.lsp in the MyCustomFolders folder within the Documents (or My Documents) folder, or in the location you are using to store the LSP files.

In Notepad (Windows) or TextEdit (Mac OS), type the following in the text editor area:; Creates a new layer and/or sets a layer current (defun CreateLayer-ActiveX (lyrName layColor docObj / layerObj) (if (= (vl-catch-all-error-p (vl-catch-all-apply 'vla-item '((vla-get-layers docObj) "Hatch")) ) T ) (progn ; Creates the layer (setq layerObj (vla-add (vla-get-layers docObj) lyrName)) ; Sets the color of the layer (vla-put-color layerObj layColor) ) ) ; Sets the layer current (vla-put-activelayer docObj (vla-item (vla-get-layers docObj) lyrName)) (princ) )

Save the file and then load it into AutoCAD.

At the Command prompt, type the following to test the function:(setq acad (vlax-get-acad-object)) (setq curDoc (vla-get-activedocument acad)) (createlayer-activex "NewLayer" 4 curDoc)

A new layer named NewLayer is added to the drawing, assigned the color 4 (Cyan), and set as current. You can see that the new layer has been created by using the layer command and the Layer Properties Manager.

Adding graphical objects to a drawing with ActiveX is different from what you have done previously when using the command, entmake, and entmakex functions. When using ActiveX, you must specify where an object should be created—the methods of the AutoCAD COM library are not contextually driven. You must explicitly work in model space or paper space.

The following exercise defines a function that prompts the user for two points: the opposite corners of a rectangle. User input is handled using the methods available through the Utility object. The two points specified are used to define the four corners of a rectangle, by making an array of eight elements and then populating the XY pairs of each point defined for the rectangle. The array is used to specify the vertices of the lightweight polyline to add in the model space of the current drawing. Once the lightweight polyline is added, the Closed property is used to close the lightweight polyline.

Open the ActiveX.lsp file in Notepad (Windows) or TextEdit (Mac OS).

Click after the last closing parenthesis of the createlayer-activex function and press Enter twice.

In the text editor area, type the following:; Creates a rectangle on the Obj layer (defun c:DrawRectangle_ActiveX ( / docObj curLayer vPt1 vPt2 ptList lwPlineObj) ; Gets a reference to the current drawing (setq docObj (vla-get-activedocument (vlax-get-acad-object))) ; Gets the active layer (setq curLayer (vla-get-activelayer docObj)) ; Creates and/or sets the Obj layer current (CreateLayer-ActiveX "Obj" acGreen docObj) ; Prompts the user for a point (setq vPt1 (vla-getpoint (vla-get-utility docObj) nil "\nSpecify first corner: ")) ; Prompts the user for the opposite corner (setq vPt2 (vla-getcorner (vla-get-utility docObj) vPt1 "\nSpecify opposite corner: ")) ; Creates an array of four 2D points (setq ptList (vlax-make-safearray vlax-vbDouble '(0. 7))) (vlax-safearray-fill ptList (list ; Point 1 (vlax-safearray-get-element (vlax-variant-value vpt1) 0) (vlax-safearray-get-element (vlax-variant-value vpt1) 1) ; Point 2 (vlax-safearray-get-element (vlax-variant-value vpt1) 0) (vlax-safearray-get-element (vlax-variant-value vpt2) 1) ; Point 3 (vlax-safearray-get-element (vlax-variant-value vpt2) 0) (vlax-safearray-get-element (vlax-variant-value vpt2) 1) ; Point 4 (vlax-safearray-get-element (vlax-variant-value vpt2) 0) (vlax-safearray-get-element (vlax-variant-value vpt1) 1) ) ) ; Gets a reference to the current space in AutoCAD (if (= (vla-get-activespace docObj) acModelSpace) (setq space (vla-get-modelspace docObj)) (setq space (vla-get-paperspace docObj)) ) ; Draws the rectangle using a lightweight polyline (setq lwPlineObj (vla-addlightweightpolyline space ptList)) ; Closes the polyline (vla-put-closed lwPlineObj :vlax-true) ; Restores the previous active layer (vla-put-activelayer docObj curLayer) (princ) )

Save the file and then reload it into AutoCAD.

At the Command prompt, type drawrectangle_activex and press Enter to test the function.

At the Specify first corner: prompt, specify a point in the drawing area.

At the Specify opposite corner: prompt, specify a point in the drawing area that is the opposite corner of the rectangle.

A new layer named Obj is added to the drawing and a new lightweight polyline is drawn based on the points specified.

The completed exercise can be found in the ch22_activex_complete.lsp file, which you can download from this book's web page.

Monitoring Events with Reactors

Reactors allow you to monitor for events that occur in a drawing or an application and are one of the main advantages of using ActiveX with AutoLISP. Some of the events that you can monitor for include starting or ending of a command, attaching an Xref, or inserting a block. Using reactors, you can ensure certain objects are placed on a specific set of layers without needing to switch layers before creating an object.

In this exercise, you will create two custom functions that AutoCAD will call when a command is started, canceled, ends, or fails. You will be monitoring the hatch, bhatch, and gradient commands. When any one of those commands is started, AutoCAD sets the Hatch layer as current and restores the previous layer if the command ends, fails, or is canceled.

Open the ActiveX.lsp file in Notepad (Windows) or TextEdit (Mac OS).

Click after the last closing parenthesis of the drawrectangle_activex function and press Enter twice.

In the text editor area, type the following:; Register the Custom command reactors (if (= *rctCmds* nil) (setq *rctCmds* (vlr-command-reactor nil '((:vlr-commandCancelled. apc-cmdAbort) (:vlr-commandEnded. apc-cmdAbort) (:vlr-commandFailed. apc-cmdAbort) (:vlr-commandWillStart. apc-cmdStart) ) ) ) (princ) ) ; Custom function executed when a command is ; cancelled, ends, or fails (defun apc-cmdAbort (arg1 arg2) ; Restore the previous layer (if (/= *gClayer* nil) (setvar "clayer" *gClayer*) ) ; Clear the global variable (setq *gClayer* nil) (princ) ) ; Custom function executed when a command is started (defun apc-cmdStart (arg1 arg2 / docObj layerObj) ; Store the current layer (setq *gClayer* (getvar "clayer")) ; Get a reference to the current drawing (setq docObj (vla-get-activedocument (vlax-get-acad-object))) ; Check to see which command has been started (cond ; HATCH, BHATCH or GRADIENT command was started ((or (= (car arg2) "HATCH") (= (car arg2) "BHATCH") (= (car arg2) "GRADIENT") ) ; Create and/or set the Hatch layer current (CreateLayer-ActiveX "Hatch" acRed docObj) ) ) (princ) )

Save the file and then reload it into AutoCAD.

At the Command prompt, type drawrectangle-activex and press Enter.

Follow the prompts that are displayed.

At the Command prompt, type hatch and press Enter.

At the Pick internal point or [Select objects/Undo/seTtings]: prompt, specify a point inside the rectangle that was drawn in steps 4 and 5.

Press Enter to end the hatch command.

A new layer named Hatch is added to the drawing and the new hatch object is placed on that layer.

The completed exercise can be found in the ch22_activex_complete.lsp file, which you can download from this book's web page.

Learning about Other ActiveX-Related Functions

As I mentioned earlier, this chapter provides an introduction to the various concepts required to get started with ActiveX in AutoLISP. There is a wide range of additional AutoLISP functions that I wasn't able to cover in this chapter. The names of these functions begin with the prefixes vla-, vlax- , and vlr-. You can learn more about the functions in the AutoCAD Help system by browsing to http://help.autodesk.com/view/ACD/2015/ENU/files/homepage_dev.htm, clicking the Functions By Name And Feature Reference link, and then using the links in the Visual LISP Extensions for AutoLISP (Windows only) section.

Leveraging the Windows and Microsoft Office COM Libraries

The Microsoft ecosystem is full of hidden gems that can increase your productivity and improve everyday workflows. Many programs that are available for free or for purchase let you create proposals or manipulate information in a database, but Windows and Microsoft Office allow you to leverage what they do best by using the COM libraries that they expose. There aren't many companies that allow you to manipulate or access their programs programmatically like Microsoft does, so take advantage of these benefits whenever possible.

Using the COM libraries for Windows and Microsoft Office, you can accomplish the following:

Create desktop shortcuts, expand environment variables, or even launch an external application

Create and print documents using Microsoft Word

Create, manipulate, and print spreadsheets using Microsoft Excel

Create email messages and access contact lists using Microsoft Outlook

Access and manipulate data in a database using Microsoft Access

For specific information on each of these COM libraries, refer to the documentation that Microsoft publishes with Windows and the Microsoft Office application you are interested in working with. Your favorite Internet search engine will also be of help; search on the keywords「Windows Shell object documentation」or「Microsoft Office 2013 Release Developers」to get started.

Accessing the Windows Shell Object

The Windows Shell object is the graphical interface that you or the user interact with when accessing an application or the files stored on the workstation. With the Windows Shell object, you can take these actions:

Create shortcuts on the desktop or in a file folder

Access the files on your workstation or a removable/network drive

Launch an application or URL

Work with environment variables

You can create a reference to a Windows Shell object using the following code:

(vlax-create-object "WScript.Shell")

Don't forget to release an object returned by the vlax-create-object function from memory after you are done with it by using vlax-release-object. Here are two custom functions that demonstrate some of the functionality exposed by the Windows Shell object:

; Creates a new shortcut ; Usage: (CreateShortcut "c:\\mylink.lnk" "c:\\temp\\myfile.lsp") ; Revise "c:\\mylink.lnk" to a location for which you have write access and change ; "c:\\temp\\myfile.lsp" to a valid filename on your workstation. (defun CreateShortcut (lnkName Target / wshShell shortcut) ; Create a reference to Window Scripting Shell Object (setq wshShell (vlax-create-object "WScript.Shell")) ; Expand the string and any variables in the string (setq shortcut (vlax-invoke-method wshShell 'CreateShortcut lnkName)) (vlax-put-property shortcut 'TargetPath Target) (vlax-invoke-method shortcut 'Save) ; Release the Window Scripting Shell Object (vlax-release-object wshShell) (princ) ) ; Shows how to use expanding environment strings ; Usage: (ExpEnvStr "%TEMP%\\MYDATA") ; Results of sample: "C:\\Users\\Lee\\AppData\\Local\\Temp\\MYDATA" (defun ExpEnvStr (strVal / wshShell strValRet) ; Create a reference to Window Scripting Shell Object (setq wshShell (vlax-create-object "WScript.Shell")) ; Expand the string and any variables in the string (setq strValRet (vlax-invoke-method wshShell 'ExpandEnvironmentStrings strVal)) ; Release the Window Scripting Shell Object (vlax-release-object wshShell) strValRet )

Using the Correct Microsoft Office Release

Microsoft Office and AutoCAD are supported on both 32- and 64-bit platforms. However, Microsoft Office 32-bit can be installed on Windows 64-bit whereas AutoCAD 32-bit cannot. Many companies install only Microsoft Office 32-bit, because there is less support for 64-bit add-ons for Microsoft Office applications than for 32-bit add-ons. Although this typically isn't an issue, the problem comes when you try to use ActiveX to talk to any of the Microsoft Office applications from AutoCAD. AutoCAD 64-bit won't allow you to import/access 32-bit database drivers or COM libraries, so you need to make sure your workstation is configured correctly by having the proper release of Microsoft Office installed.

The following code helps you locate the Microsoft Office release that a user might have installed on their machine, whether they are using Office 32- or 64-bit. The code uses a function named expenvstr, which you saw in the「Leveraging the Windows and Microsoft Office COM Libraries」section.

; Checks for a specific version of Microsoft Office ; Microsoft Office 2013 - 15 ; Microsoft Office 2010 - 14 ; Microsoft Office 2007 - 12 ; Microsoft Office 2003 - 11 ; Microsoft Office 2000 - 10 (defun Get-MSOfficePath (ver / ) ; Office version (setq *MSOfficeVer* (itoa ver)) ; Office 32-bit path on Windows 64-bit (setq *MSOfficePathx86* (strcat (ExpEnvStr "%PROGRAMFILES(X86)%") "\\Microsoft Office\\Office" (itoa ver) ) ) ; Office path (Windows 32- or 64-bit) (setq *MSOfficePath* (strcat (ExpEnvStr "%PROGRAMFILES%") (cond ((= ver 15)(strcat "\\Microsoft Office " (itoa ver) "\\root\\Office" (itoa ver))) (strcat "\\Microsoft Office\\Office" (itoa ver)) ) ) ) ; Return 32-bit location first and then 64-bit (cond ((/= (findfile *MSOfficePath*) nil) (strcat *MSOfficePath* "\\") ) ((/= (findfile *MSOfficePathx86*) nil) (strcat *MSOfficePathx86* "\\") ) ("") ) ) ; Example of using the custom function (Get-MSOfficePath 15) "C:\\Program Files\\Microsoft Office 15\\root\\Office15\\"

Working with Microsoft Office

The Microsoft Word object allows you to create an instance of Microsoft Word, which can then be used to create or open a document. Once a document has been created or opened, you can step through and manipulate the content of the document or print the document to an available system printer.

A reference to a Microsoft Word object can be created using the following code:

(vlax-create-object "Word.Application")

If more than one version of Microsoft Office is installed, you can specify which release of the product to start by adding a version number to the program ID passed to the vlax-create-object function. For the available version numbers, see the「Using the Correct Microsoft Office Release」sidebar.

You can use the following code to create a reference to the Microsoft Excel object:

(vlax-create-object "Excel.Application")

You can find the custom functions that show how to work with the Microsoft Word and Excel objects in the ch22_mswin_office.lsp file that you can download from this book's web page. The LSP file contains the following custom functions:

createmsworddoc The createmsworddoc function creates a new Word document and saves it with the name ch22_apc_word_sample.doc to the MyCustomFiles folder. The new Word document file is populated with information about some of the nongraphical objects in the current drawing.

printmsworddoc The printmsworddoc function opens the ch22_apc_word_sample.doc file that was created with the createmsworddoc function and placed in the MyCustomFiles folder. The Word document file is then printed using the default system printer.

extractattributestoexcel The extractattributestoexcel function creates a new spreadsheet file named ch22_attributes.xls in the MyCustomFiles folder. The handle, tag, and text string for each attribute in the block references of the current drawing are extracted to columns and rows in the spreadsheet. Open the ch22_building_plan.dwg file in AutoCAD before executing the function.

updateattributesfromexcel The updateattributesfromexcel function reads the information from the spreadsheet file named ch22_attributes.xls in the MyCustomFiles folder. The extracted handle in the spreadsheet is used to get the attribute reference and then update the tag and text string value that is present in the spreadsheet. Since handles are unique to each drawing, you must open the original drawing that the attributes were extracted from. Make changes to the third column in the spreadsheet file, such as C2436 to CC2436, before opening the ch22_building_plan.dwg file in AutoCAD and executing the function.

Along with custom functions that work with Microsoft Word and Excel, there are also a few functions that demonstrate how to connect to a Microsoft Access database (MDB) file using Database Access Object (DAO) and ActiveX Data Object (ADO). The database library you use depends on which release of Office you are using. You can find two custom functions that access an MDB file in the ch22_mswin_office.lsp file that you can download from this book's web page.

The LSP file contains the following custom functions:

accessdatabasedao The accessdatabasedao function makes a connection to the Access database ch22_employees.mdb, located in the MyCustomFiles folder. Once a connection to the database is made, the records in the Employees table are read and modified. Use this function when working with Access 2007 and earlier.

accessdatabaseado The accessdatabaseado function makes a connection to the Access database ch22_employees.mdb, located in the MyCustomFiles folder. Once a connection to the database is made, the records in the Employees table are read and modified. Use this function when working with Access 2007 and later.
