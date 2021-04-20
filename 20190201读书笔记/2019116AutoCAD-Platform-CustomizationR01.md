## 记忆时间

## 0107. 主题卡 —— 函数收藏

信息源自「2019116AutoCAD-Platform-Customization0210.md」：

### 01. 求余数（rem）

NOTE: Dividing a number by 0 causes an error and returns this message: `; error: divide by zero`. If the error is not handled, the custom function that contains the error is terminated. You can use the `vl-catch-all-apply` function to keep the function from being terminated. I discuss the `vl-catch-all-apply` function in Chapter 19,「Catching and Handling Errors.」

When dividing numbers, you can use the AutoLISP `rem` function to return the remainder of the first number after it has been divided by all the other numbers supplied to the function. The `rem` function can take any number of numeric values; the function returns 0 when no values are passed to it. The following demonstrates the rem function:

```c
(/ 10.0 3) 
3.33333 
(rem 10.0 3.0) 
1.0
```

### 02. 求最大公约数（gcd）

AutoLISP includes a function named `gcd` that can be used to return the greatest common denominator of two integer values. The gcd function requires two integer values, and it returns an integer that represents the greatest common denominator of the provided values. Here are two examples:

1-2『这不是就是求最大公约数嘛，数学应用很广的，以后应该可以用到。函数 rem 和 gcd 收录进主题卡片「函数收藏」中。（2021-03-06）』—— 已完成

```c
(gcd 5 2) 
1 
(gcd 54 81) 
27
```

### 03. 求最大最小值函数（min and max）

The min and max functions accept any integer or real numeric values. The min function returns the smallest numeric value from those that are passed to it, whereas the max function returns the largest numeric value. A real value is returned by the function, except when the function is passed only integer values — in that case, an integer value is returned. If no numeric value is passed to either function, 0 is returned. The following are examples of the min and max functions:

```c
(min 9 1 1976 0.25 100 -25) 
-25.0
(max 9 1 1976 0.25 100 -25) 
1976.0 
(max 9 1 1976 100 -25) 
1976
```

### 04. 判断负值、判断零值（minusp and zerop）

The minusp and zerop functions accept an integer or real numeric value. The minusp function returns T if the value that it was passed is negative, or it returns nil if the value was positive. The zerop function also returns T or nil; T is returned if the value passed is equal to 0. The zerop function can help you avoid dividing a number by 0 or seeing if a system variable is set to 0. The following are examples of the minusp and zerop functions:

```c
(minusp 25) 
nil 
(minusp -25) 
T 
(zerop 25) 
nil 
(zerop 0) 
T
```

For more information on the minusp and zerop functions, see the AutoCAD Help system.

2『求最大最小值函数、判断负值、判断零值函数，收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

### 05. 高阶数学函数

In addition to basic math functions, AutoLISP offers a range of advanced math functions that aren't used as frequently. These advanced functions allow you to work with angular, exponential, natural logarithm, or square root numeric values. AutoLISP supports the advanced math functions listed in Table 13.1.

1-2『真没想到，autolisp 里原生数学函数这么丰富。这些高阶函数都收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

Table 13.1 AutoLISP advanced math functions

| Function | Description |
| --- | --- |
| sin | Returns the sine of an angular value expressed in radians. |
| atan | Calculates the arctangent of an angular value expressed in radians. |
| cos | Returns the cosine of an angular value expressed in radians. |
| exp | Returns a numeric value that has been raised to its natural antilogarithm. |
| expt | Returns a numeric value after it has been raised by a specified power. |
| log | Calculates the natural logarithm of a numeric value. |
| sqrt | Gets the square root of a numeric value. |
| - | - |

For more information on these functions, see the AutoCAD Help system.

### 06. logior and logand

Because a bit-coded value is represented by the integer data type, you can use the `+` and `–` functions to add or remove a bit value for the overall sum of a bit-coded value. AutoLISP also provides several useful functions that you can use when working with bit-coded values. The logior and logand functions help combine several bit-coded values and determine whether a bit is part of a bit-coded value. Let's take a closer look at the logior and logand functions.

2『函数 logior、函数 logand，收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

1 logior. The logior function allows you to combine several bits into a single bit-coded value and ensures that a bit is added only once to the resulting bit-coded value. Although you can use the `+` function to add several bits together, that function simply adds several values together and returns the resulting value, which might return a bit-coded value with a different meaning. For example, the bits 1 and 4 are equal to the bit-coded value of 5:

```c
; Final result is a bit-coded value of the bits 1 and 4 
(logior 1 4) 
5 
; Final result is an integer of 5 
(+ 1 4) 
5
```

2 logand. The logand function is used to determine whether a specific bit or bit-coded value is part of another bit-coded value. This type of comparison in a program can be helpful when you need to handle specific conditions in the AutoCAD environment, such as making sure that the current layer is not frozen or locked when you're creating or selecting objects, or making sure a specific running object snap is set. Here is the syntax of the logand function:

1-2『这里提供了实现自动锁图层的实现线索，待研究。之前开发建筑底图迁移功能时，已经通过 activeX 实现了，这里的信息如果实现，应该是另外一条途径。（2021-03-06）』

The following examples use the logand function to determine if a bit is common with the provided bits or bit-coded values. Bit 2 represents the MIDpoint running object snap; a bit-coded value of 12 represents the CENter and QUAdrant running object snaps; and the bit-coded value of 34 represents the running object snaps MIDpoint and INTersection. The first example returns 0 because the bit 2 value is not part of the bit-coded value 12 (bit codes 4 and 8), whereas 2 is returned for the second example because bit 2 is part of the bit-coded value of 34 (bit codes 1, 2, and 32).

```c
; Returns 0 because no bit codes are in 
; common with the two numbers 
(logand 2 12) 
0 
; Returns 2 because it is the common bit code 
; in common with both numbers 
(logand 2 34) 
2s
```

### 07. 取负数

`˜` (Bitwise NOT). The `˜` (bitwise NOT) function accepts a bit (integer) value and converts it into a binary number before performing a bitwise negation. The negation changes any 1 in the binary value to a 0, and any 0 to a 1. For example, an integer value of 32 expressed as a binary value is as follows:

The binary value is read from lower right to upper left. When the ˜ (bitwise NOT) function is applied to a bit value of 32, it becomes a bit value of -33 and is expressed as the binary value:

The following is an example of the ˜ (bitwise NOT) function:

```c
(˜ 32) 
-33
```

2『竟然还有这个取负数的函数，这样以后不用自己用 0 减生成负数了。收录进主题卡片「函数收藏」。（2021-03-06）这里的取负数不是自己想要的负数，它多减了 1，后来自己封装了一个取负数的公共函数，因为这个功能太常用了。（2021-04-19）』—— 已完成

### 08. 布尔函数

boole. The AutoLISP boole function is used to perform a Boolean operation on two bit-coded (integer) values. The Boolean operations that can be performed are `AND(1)`, `XOR(6)`, `OR(7)`, and `NOR(8)`. For example, the AND Boolean operation can be used to see which bits are common between two bit-coded values. If an AND Boolean operation is performed on the bit-coded values 55 and 4135, a bit-coded value of 39 is returned.

The following is an example of the boole function:

```c
(boole 1 55 4135) 
39
```

1-2『选择器过滤条件的实现，底层原理应该靠的就是它，但目前没吃透。收录进主题卡片「函数收藏」。（2021-03-06』—— 已完成

### 09. 剔除字符串中特定的字符

Although the substr function is very helpful in pulling a string apart, it is not the most efficient function to use if you need to remove or trim specific characters from the left or right ends of a string. The AutoLISP `vl-string-trim`, `vl-string-left-trim`, and `vl-string-right-trim` functions are better suited to trimming specific characters, such as extra spaces or zeroes, from the ends of a string. The `vl-string-trim` function trims both ends of a string, whereas the `vl-string-left-trim` and `vl-string-right-trim` functions trim only the left and right ends of a string, respectively. Characters that are part of the `character_set` argument are trimmed from the respective ends of the string until a character that isn't a part of the `character_set` argument is encountered.

1『每个语言都看到这 3 个剔除函数，底层的实现原理应该都一样。每个语言都有说明应用场景肯定多。（2021-03-06）』

The following shows the syntax of the `vl-string-trim`, `vl-string-left-trim`, and `vl-string-right-trim` functions:

```c
(vl-string-trim character_set string) 
(vl-string-left-trim character_set string) 
(vl-string-right-trim character_set string)
```

### 10. 各数据类型间转化

[帮助 | Conversion Functions Reference (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-5BDBD4BC-289E-4A49-9BB9-DF6A6147E0FC)

1、整数转字符串。

[帮助 | rtos (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-D03ABBC2-939A-44DB-8C93-FC63B64DE4A2)

2、整数转浮点数。

[帮助 | float (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-93808F66-808C-49F7-9303-F12C55296080)

Returns the conversion of a number into a real number.

Signature:

```
(float number)
```

number, Type: Integer or Real. A numeric value.

Return Values. Type: Real. The real number derived from number.

Examples

```
(float 3)
3.0

(float 3.75)
3.75
```

3、各个类型的数据转为字符串。

结果转为字符串（Evaluating Values to Strings）

When working with strings, you may also want to concatenate a numeric value as part of a prompt string or response to the user. Before you can concatenate a nonstring value to a string, you must convert the nonstring value to a string. The quickest way to do so is to use the AutoLISP `vl-princ-to-string` and `vl-prin1-to-string` functions.

The difference between the two functions is how quotation marks, backslashes, and other control characters are represented in the string that is returned. The `vl-prin1-to-string` function expands all control characters, whereas the `vl-princ-to-string` function doesn't. For more information on control characters that can be used in strings, search on the keywords「control characters」in the AutoCAD Help system.

The following shows the syntax of the `vl-princ-to-string` and `vl-prin1-to-string` functions:

```c
(vl-princ-to-string atom) 
(vl-prin1-to-string atom)
```

The atom argument represents the expression, variable, or value that should be converted to and returned as a string. The following are examples of the `vl-princ-to-string` and `vl-prin1-to-string` functions, and the values that are returned:

```c
(vl-princ-to-string 1.25) 
"1.25" 
(vl-princ-to-string (findfile (strcat (getvar "PROGRAM") ".exe"))) 
"C:\\Program Files\\Autodesk\\AutoCAD 2014\\acad.exe" 
(vl-prin1-to-string 1.25) 
"1.25" 
(vl-prin1-to-string (findfile (strcat (getvar "PROGRAM") ".exe"))) 
"\"C:\\\\Program Files\\\\Autodesk\\\\AutoCAD 2014\\\\acad.exe\""
```

[帮助 | vl-princ-to-string (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-33B0CA43-84F2-46DE-88BE-8FFF22C83FAD)

Returns the string representation of LISP data as if it were output by the princ function

Signature:

```
(vl-princ-to-string data)
```

data. Type: Integer, Real, String, List, Ename (entity name), T, or nil. Any AutoLISP data.

Return Values. Type: String. A string containing the printed representation of data as if displayed by princ.

Examples:

```
(vl-princ-to-string "abc")
"abc"

(vl-princ-to-string "c:\\acadwin")
"C:\\ACADWIN"

(vl-princ-to-string 'my-var)
"MY-VAR"
```

1『在 CAD 里测试了，转字符串的时候并没有被转为大写字母字符串。（2021-04-19）』

4、浮点数转整数。

[帮助 | fix (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-93B5F13B-348E-49E0-A116-0861684506D5)

[帮助 | Arithmetic Functions Reference (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-FC14467C-63B9-4400-8C6A-266D21C846AE)

Returns the conversion of a real number into the nearest smaller integer.

Signature:

```
(fix number)
```

number. Type: Integer or Real. A numeric value.

Return Values. Type: Integer. The integer derived from number.

If number is larger than the largest possible integer (+2,147,483,647 or -2,147,483,648 on a 32-bit platform), fix returns a truncated real (although integers transferred between AutoLISP and AutoCAD are restricted to 16-bit values).

Remarks: The fixfunction truncates number to the nearest integer by discarding the fractional portion.

Examples:

```
(fix 3)
3

(fix 3.7)
3
```

5、字符串转浮点数。

[帮助 | atof (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-8618A388-E4CF-40E1-813B-057367DD1840)

6、字符串转整数。

[帮助 | atoi (AutoLISP) | Autodesk](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-20EF237C-7079-4E29-860C-B8531D6C7F36)

### 11. 创建获取 ActiveX 对象

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

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

### 12. 批量处理 collections 数据集的函数（vlax-for 和 vlax-map-collection）

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

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

### 13. 查看 collections 对象的属性和方法

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

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

』—— 已完成

```c
(vlax-dump-object obj [flag])
```

Here are its arguments:

1 obj. The obj argument is a value of the vla-object type, which is returned by a method or property, or is available as the var argument of the vlax-for function.

2 flag. The flag argument is an optional argument that allows you to specify whether the returned output lists only the properties or the properties and methods supported by an object. A value of T returns both supported properties and methods, whereas no value or a value of nil returns only the supported properties.

Here's an example that shows how to list the properties and methods of an object with the `vlax-dump-object` function:

(RO) after a property name indicates that the property is read-only and the value cannot be changed. The number in the parentheses after each method listed in the Methods supported section of the output indicates the number of arguments that the method expects; no number in the parentheses indicates the method doesn't accept any argument values.

### 14. 获取和修改 collections 对象的属性和方法

信息源自「2019116AutoCAD-Platform-Customization0212.md」：

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

### 15. 调用 collections 对象的方法

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

### 16. 定义 ActiveX 体系中的变体（Variants）

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

### 17. 定义 ActiveX 体系中的数组（Arrays）

Arrays

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

补充：正好后面有相关的信息。（2021-03-07）

Although you can access the properties and methods of an object using the functions covered in the「Specifying Properties and Invoking Methods」section, importing a COM library can make coding easier. When you import a COM library, that library defines an AutoLISP function for the properties and methods of each class in the library. The newly defined functions that result from importing a COM library reduce the amount of code that needs to be written.

For example, the `vla-get-red` function can be used instead of the `vlax-get-property` function to get the current value of the Red property of an AutoCAD True Color object. The same is true with methods; `vla-delete` is the equivalent of using the `vlax-invoke-method` function with the Delete method name as an argument. The following two code statements produce the same result:

```c
(vlax-get-property clrObj 'Red) 
(vla-get-red clrObj)
```

1-3『这里的信息正好解答了之前的疑惑，为啥修改块属性值有 2 种实现方式。原来官方文档里的方法是「importing a COM library」。补充到前面的「函数收藏」主题卡片里。（2021-03-07）』

』

### 18. 导入 COM library

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

### 19. 获取 Symbol Tables

源自「2019116AutoCAD-Platform-Customization0217.md」：

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

### 20. 检测 Symbol Tables

源自「2019116AutoCAD-Platform-Customization0217.md」：

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

』

### 21. snvalid

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