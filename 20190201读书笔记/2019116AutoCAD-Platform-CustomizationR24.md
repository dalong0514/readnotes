## 记忆时间

## 目录

Part II AutoLISP: Productivity through Programming

0208 —— Chapter 18: Working with the Operating System and External Files

0209 —— Chapter 19: Catching and Handling Errors

0210 —— Chapter 20: Authoring, Managing, and Loading AutoLISP Programs

## 0208. Working with the Operating System and External Files

The AutoLISP® programming language can be used to reach beyond the boundaries of the Autodesk® AutoCAD® application window and objects in the current open drawing. Using AutoLISP, you can access settings managed by the operating system and installed applications on Windows or by the application-level settings of AutoCAD on both Windows and Mac OS. You can access operating system– and application-level settings from the Windows Registry. On Mac OS, you can access application-level settings for AutoCAD from the Plist (property list) files.

Along with accessing operating system and application settings, you can read and write ASCII (plain text) files that are stored on a local or network drive. You can use content in an ASCII file to populate project information in a title block or as a means to export information from a drawing. Exported information can be used to create or update objects in a drawing or to generate a quote based on the values of attributes in blocks placed within a drawing. In addition to reading and writing ASCII files, you can use AutoLISP to manage and get general information about the files and directories on a local or network drive. In this chapter, you'll learn to persist values between AutoCAD sessions, write to and read from external files, and work with files in the operating system.

## 0209. Catching and Handling Errors

## 0210. Authoring, Managing, and Loading AutoLISP Programs

Entering AutoLISP® expressions directly at the Autodesk® AutoCAD® Command prompt is a great way to start learning AutoLISP programming. However, if you want to use expressions multiple times or in different drawings, you will need to enter them over and over again.

Instead of entering AutoLISP expressions at the Command prompt, you can store them in an ASCII text file with a .lsp extension. In addition to entering AutoLISP expressions in a LSP file, you can add nonexecutable expressions known as comments, which allow you to make notes to yourself in the code. After you create a LSP file, you must load it into AutoCAD before any of the expressions stored in the file can be executed.

Before loading a LSP file, you need to let AutoCAD know where it is located and that the location it is stored in is safe to load executable (LSP/ARX/DVB) files from. Once AutoCAD knows where your LSP files are located, you can then load them manually as needed, automatically at startup, or on demand.

### 10.1 Storing AutoLISP Expressions

Although you can enter AutoLISP expressions at the AutoCAD Command prompt, as part of a script file, or as a command macro used in the user interface, the most common method is to type them into a text editor and store them in a LSP file. AutoLISP programs are commonly stored in LSP files, but they can also be stored in menu AutoLISP (MNL) files. Menu AutoLISP files have the .mnl file extension.

MNL files contain AutoLISP programs that are used by command macros defined in a CUI/CUIx file. When a CUI/CUIx file is loaded into AutoCAD, AutoCAD looks for and loads an MNL file with the same name as the CUI/CUIx file being loaded. For example, if the acad.cuix file is loaded, AutoCAD looks for and loads the acad.mnl file if a file named acad.mnl? is found within the support file search paths defined in the Options dialog box (Windows) or Application Preferences dialog box (Mac OS).

1『做一个同名文件（mnl）应该可以解决很多人无法自动加载的问题，但 mnl 文件也是纯文本，会暴露源码。（2021-03-02）』

NOTE: A LSP or MNL file must be saved to an ASCII text file, and it cannot include any special characters like a Rich Text or Microsoft Word document can.

Once a LSP file has been created, the code stored in the file can then be loaded into the AutoCAD program when it is needed. I discuss the text editors that can be used to create a LSP file in the next section, and you'll learn how to load a LSP file later, in the「Loading AutoLISP Files」section.

#### 10.1.1 Selecting an Editing Environment

You don't have to buy additional software to create and edit AutoLISP program files, regardless of whether you are using Windows or Mac OS. Any of the following applications can be used to create or edit AutoLISP expressions stored in a LSP or MNL file:

Notepad (Windows Only) Notepad allows you to create and edit plain ASCII text files and is installed with Windows. Although Notepad isn't designed specifically for AutoLISP programming, it is the choice of many veteran AutoLISP developers. Notepad is the application you will primarily use with this book if you are using AutoCAD on Windows.

Visual LISP® Editor (Windows Only) The Visual LISP Editor is a specialized development environment that is designed for working with AutoLISP programs stored in LSP or MNL files. This editor supports colored syntax and tools that help you identify missing parentheses. Additionally, this editor allows you to load, format, check, and debug AutoLISP programs. I cover the Visual LISP Editor and its features in Chapter 21,「Using the Visual LISP Editor (Windows only).」

TextEdit (Mac OS Only) TextEdit allows you to create and edit plain ASCII text files and is installed with Mac OS. Like Notepad on Windows, TextEdit isn't designed specifically for AutoLISP programming, but it does contain all the basic editing features you want in an editor. TextEdit is the application you will primarily use with this book if you are using AutoCAD on Mac OS.

Throughout most of this book, I focus primarily on the core concepts of the AutoLISP programming language; for that, I decided to keep things simple by using Notepad and TextEdit. However, once you are comfortable with AutoLISP and if you are on Windows, I strongly recommend that you eventually make the transition to the Visual LISP Editor. If you are on Mac OS, the Visual LISP Editor isn't available unless you install Windows and AutoCAD on Boot Camp or Parallels. If you do lots of AutoLISP development, the Visual LISP Editor can save you time writing and debugging.

1『作者写书的时候估计没有 VScode，用这个 IDE 不要太舒服。（2021-03-02）』

#### 10.1.2 Creating an AutoLISP File

As I previously mentioned, a LSP file is a plain ASCII text file. You can use Notepad on Windows or TextEdit on Mac OS to create a LSP file, but since both of these applications commonly are used to work with TXT files, you will need to be sure to add the .lsp file extension to the files you create with these applications. If you are on Windows and want to use the Visual LISP Editor, consult the instructions in Chapter 21 for creating a LSP file.

NOTE: The examples in this section assume that you created a folder named MyCustomFiles in your Documents (or My Documents) folder on your local drive. If you have not created this folder, do so now, or if you created the folder in a different location, be sure you adjust the steps accordingly.

The following exercise explains how to create an AutoLISP file named mylisp.lsp on Windows:

1 Do one of the following: 1) On Windows XP or Windows 7, click the Start button [All] Programs Accessories Notepad. 2) On Windows 8, on the Start Screen, type notepad and then click Notepad when it appears in the search results. 

2 In Notepad, click File Save As.

3 In the Save As dialog box, browse to the MyCustomFiles folder that you created under the Documents (or My Documents) folder, or to the location where you want to store the LSP file.

4 In the File Name text box, type mylisp.lsp.

5 Click the Save As Type drop-down list and select All Files (`*.*`).

6 Click the Encoding drop-down list and select ANSI. Click Save.

7 In the text editor area, type the following expressions.

```c
(defun c:MSG () (alert "First AutoLISP file.")) 
(prompt "\nVersion 1.0 – My AutoLISP Programs")
```

The AutoLISP alert function displays a message box; the prompt function displays a message at the AutoCAD Command prompt.

8 Click File Save.

NOTE: I discussed the AutoLISP alert and prompt functions in Chapter 15,「Requesting Input and Using Conditional and Looping Expressions.」

If you are running AutoCAD on Mac OS, use the following steps to create a LSP file named mylisp.lsp:

1 In the Mac OS Finder, click Go Applications. In the Finder window, double-click TextEdit.

2 In TextEdit, click TextEdit Preferences. In the Preferences dialog box, on the New Document tab click Plain Text and deselect Smart Quotes. Close the dialog box. If a document was open when you first started TextEdit, close it now. Changes to the settings affect only future documents, those you create or open after the changes were made.

3 Click File New to create a plain ASCII text file.

4 Click File Save and type mylisp.lsp in the Save As text box. From the sidebar on the left, click Documents MyCustomFiles, or browse to the location where you want to store the LSP file. Click Save.

5 If prompted to use the .lsp extension, click Use.Lsp.

6 In the text editor area, type the following expressions:

```
(defun c:MSG () (alert "First AutoLISP file.")) 
(prompt "\nVersion 1.0 – My AutoLISP Programs")
```

The AutoLISP alert function displays a message box; the prompt function displays a message at the AutoCAD Command prompt.

7 Click File Save.

After saving the file, you can load it into AutoCAD using one of the techniques explained in the section「Using the Load/Unload Applications Dialog Box to Load a LSP File」later in this chapter. Figure 20.1 shows the results of loading the mylisp.lsp file in AutoCAD and then executing the MSG function at the Command prompt.

Figure 20.1 Loading a custom program

#### 10.1.3 Editing an AutoLISP File

You can edit LSP files using any of the applications described in the section「Selecting an Editing Environment」or any other application that supports editing plain ASCII text files. If the .lsp file extension has been associated with an ASCII text editor, you can simply double-click the file to open it in the associated editor. When no editor is associated with the LSP file type and you double-click on a file of that type, you are prompted to select an editor to open the file. Associate an editor with the LSP file type and make the changes to the file. Save the file as a plain ASCII text file and reload it in AutoCAD to test the code changes in the file.

### 10.2 Writing Modular Code

When you first start writing AutoLISP programs, you may tend to create large self-contained functions. As you write, you will notice similarities in the functions that you create, whether it is creating or modifying graphical and nongraphical objects, or working with system variables.

Instead of writing large functions that contain every expression required to solve a problem or complete a task, I recommend breaking large functions into smaller, more manageable, task-oriented functions. By breaking your functions down, you gain the following benefits:

1 Code can be reused across many different functions, thereby reducing the size of your programs when they are loaded into memory.

2 Code can be revised to take advantage of newer techniques or desired code changes without having to make the same changes in one or many locations in a single file or across multiple files.

3 Potential errors in a function are easier to identify and fix because there are fewer expressions to debug and evaluate.

4 Smaller functions make great building blocks to introduce new functionality.

1『超级赞同作者的观点，做一个个功能单一的小函数。（2021-03-02）』

The following is an AutoLISP function containing expressions that create and set as current a new layer named Object (or set the layer as current if it already exists) and draws a rectangle that is 6 × 3 units using the AutoCAD line command:

```c
(defun c:drawrectangle ( / ) 
  (command "._-layer" "_m" "Object" "_c" 2 "" "") 
  (command "._line" '(0 0 0) '(6 0 0) '(6 3 0) '(0 3 0) "_c") 
)
```

1『在 CAD 里可以用原生命名 `-layer` 跟着步骤一步一步走，发现 `_c` 是设置图层的颜色，空字符串 `""` 对应于回车键。（2021-03-02）』

Layers are common nongraphical objects in a drawing that are used to organize and control the display of graphical objects, such as lines and circles. Since layers are so common, you might consider creating a set of functions that are used to create a new layer or set a layer as current instead of repeating the same expressions in each of your functions.

The following shows how you might break down the expressions in the drawrectangle function into two functions named createlayer and createrectangle. You can then reuse them in other custom functions.

```c
(defun createlayer (name color / ) 
  (command "._-layer" "_m" name "_c" color "" "") 
) 

(defun createrectangle (pt1 pt2 pt3 pt4 / ) 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
)
```

The revised drawrectangle function would look like this:

```c
(defun c:drawRectangle ( / ) 
  (createLayer "Object" 2) 
  (createRectangle '(0 0 0) '(6 0 0) '(6 3 0) '(0 3 0)) 
)
```

As I mentioned, creating smaller functions lets you reuse them fairly easily. The following shows a function named drawcircle that uses the function named createlayer to create and set a layer as current before drawing a circle:

```c
(defun c:drawcircle ( / ) 
  (createLayer "Object" 2) 
  (command "._circle" '(3 1.5 0) 1) 
)
```

The drawrectangle and drawcircle functions in the previous examples use the createlayer function. Since these functions reference the same createlayer function, any changes to the createlayer function affect both of the functions. For example, it isn't ideal to create a new layer or modify that layer if it already exists in a drawing when you might simply want to just set the layer as current. The following is a revised version of the createlayer function that first tests to see whether the layer exists using the AutoLISP functions tblsearch and if:

```c
(defun createlayer (name color / ) 
  (if (/= (tblsearch "layer" name) nil) 
    (setvar "clayer" name) 
    (command "._-layer" "_m" name "_c" color "" "") 
  ) 
)
```

If the layer already exists, it is set as current by assigning the name of the layer to the clayer system variable. If the layer doesn't exist in the drawing, it is then created and set as current. As you can see, proper planning of your code and using smaller functions makes it fairly easy to update your functions. I discuss the tblsearch function in Chapter 17,「Creating and Modifying Nongraphical Objects,」and the if function in Chapter 15.

1-3『

上面的源码意外收获的 2 个知识点（原生函数）。（2021-03-02）

[tblsearch (AutoLISP)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-2AEB84A6-E3D0-4DD9-A29C-54D4099ED925): Searches a symbol table for a symbol name.

[setvar (AutoLISP)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-B1CE1BFB-2448-47F1-95EC-10E9509F01FA): Sets an AutoCAD system variable to a specified value.

』

### 10.3 Adding Comments

As a veteran programmer of over 16 years, I can honestly say that I formed my fair share of bad habits early on when first learning to program. One of the habits that I had to correct was adding very few comments (or not adding any) to my code. Comments are nonexecutable expressions that are stored as part of a LSP file. The concept of comments is not specific to AutoLISP alone but is part of most modern programming languages. The syntax used to indicate a comment varies from language to language.

The following are common reasons why you might want to add comments to a LSP file:

1 To document when the file was created and who created it.

2 To maintain a history of changes made to the program — what changes were made, when, and by whom.

3 To indicate copyright or legal statements related to the code contained in the file.

4 To explain how to use a custom function — if any arguments are expected and the type of data they might expect.

5 To explain what a set of AutoLISP expressions might be doing — you might remember what expressions are used for today, but it can become more of a challenge to remember what they are doing months or years later.

6 To mask an AutoLISP expression that you currently don't want to execute — during testing or while making changes to a program, you might want to temporarily not execute an expression but want to keep the original expressions for historical purposes.

Comments in AutoLISP programs are typically denoted with the use of a semicolon and are referred to as the single-line comment style. Expressions and text to the right of the semicolon are not executed; this allows you to add comments on a line by themselves or even after an AutoLISP expression.

The following example demonstrates the use of the single-line comment style to add comments that explain the purpose of a function or what the expressions in the function are used for:

```c
; Createlayer function creates/modifies a layer and 
; expects two argument values. 
; 
; Arguments: 
; name – A string that represents the name of the layer to create or modify 
; color – A numeric value (1 – 255) that represents the color of the layer 
; 
; Usage: (createlayer "Doors" 2) 
(defun createlayer (name color / ) 
  ; Check to see if the layer exists before creating/modifying it 
  (if (= (tblsearch "layer" name) nil) 
    (command "._-layer" "_m" name "_c" color "" "") 
    (setvar "clayer" name) 
  ) 
)
```

The single-line comment style can also be used after an AutoLISP expression. The following demonstrates the use of comments after or before an AutoLISP expression:

```c
(defun c:drawplate ( / pt1 pt2 pt3 pt4) 
  ; Create the layer named Plate or set it current 
  (createlayer "Plate" 5) 
  ; Set the coordinates to draw the rectangle 
  (setq pt1 '(0 0 0)) ; lower-left corner 
  (setq pt2 '(5 0 0)) ; lower-right corner 
  (setq pt3 '(5 2.75 0)) ; upper-right corner 
  (setq pt4 '(0 2.75 0)) ; upper-left corner 
  ; Draw the rectangle 
  (createrectangle pt1 pt2 pt3 pt4) 
  ; Display message to the user 
  (prompt "\nRectangle drawn.") 
)
```

In the previous example, all of the comments provide information about an individual or set of AutoLISP expressions, with the exception of the last comment. The last comment is an AutoLISP expression that would normally be executed, but it won't be executed as part of the program because the expression is located to the right of the semicolon. This isn't the same situation with the comments placed after the AutoLISP expressions that define and assign values to the pt1, pt2, pt3, and pt4 user-defined variables since the semicolon is placed after each expression.

Although most comments will fit on a single line, there will be times when you might want to have a comment that spans more than one line. Such is the case with the comments that were shown before createlayer. Long comments that span multiple lines are often broken up into individual comments for readability, but this does require you to break a long line and place a semicolon in front of each individual line. However, there is a second comment style that you can use with longer comments or even inside an AutoLISP expression that might start and end on the same line. This second comment style is known as inline.

1『这里提供了一种写多行注释的约定，内联（inline），详见下文。（2021-03-02）』

The inline comment style starts and ends with a semicolon but also requires two pipe symbols (`|`), which are used to mark the beginning and end of the comment. Unlike the use of the semicolon by itself, which affects all the text after it on the same line, the expressions and text inside an inline comment are not executed but anything after it will be.

The following demonstrates the use of both the inline comment style and the single-line comment style:

```c
;| 
Createlayer function creates/modifies a layer and 
expects two argument values. 
Arguments: 
name – A string that represents the name of the layer to 
create or modify 
color – A numeric value (1 – 255) that represents the color 
of the layer 
Usage: (createlayer "Doors" 2) 
|; 
(defun createlayer (name color / ) 
  ; Check to see if the layer exists before creating/modifying it 
  (if (= (tblsearch "layer" name) nil) 
    (command "._-layer" "_m" name "_c" color "" "") 
    (setvar "clayer" name) 
  ) 
) 
(defun createrectangle (pt1 pt2 pt3 pt4 / ) 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
)
(defun c:drawplate ( / pt1 pt2 pt3 pt4) 
  ; Create or modify the layer named Plate (createlayer "Plate" 5) 
  ; Set the coordinates to draw the rectangle 
  (setq pt1 '(0 0 0) ;| lower-left corner |; ) 
  (setq pt2 '(5 0 0) ;| lower-right corner |; ) 
  (setq pt3 '(5 2.75 0) ;| upper-right corner |; ) 
  (setq pt4 '(0 2.75 0) ;| upper-left corner |; ) 
  ; Draw the rectangle 
  (createrectangle pt1 pt2 pt3 pt4) 
  ; Display message to the user 
  (prompt "\nRectangle drawn.") 
)
```

1-2-3『

自己在 CAD 里跑了下上面的源码，没问题，第一次知道多行注释可以这么写（`|`），很不错！这里还有一个很意外的收获，如何判断是否有某一个图层。那么同样的，应该可以判断某个块是否存在。待验证。做一张任意卡片。（2021-03-02）——已完成

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

』

NOTE: Single-line and inline comments are the primary comment styles used in a LSP file, but the Visual LISP Integrated Development Environment (VLIDE) does support a few additional comment styles. I discuss these comment styles in Chapter 21.

### 10.4 Undefining and Redefining Standard AutoCAD Commands

When you create custom functions, they typically introduce new functionality. However, you can also disable or override the functionality of a standard AutoCAD command using the undefine and redefine commands. When undefining commands, you want to make sure that you document this properly, as it can affect scripts, AutoLISP programs, menu macros, and much more. The documentation that you create should include comments in the LSP file that redefines the command, along with external documentation such as a ReadMe or Help file related to your custom programs.

The following example creates a user-defined function named explode, which prevents users from exploding a hatch or dimension object, and then undefines the standard AutoCAD explode command using the undefine command:

```c
; Create a new Explode function 
(defun c:explode ( / ss) 
  ; See if Pick First is enabled and if so, get the current objects 
  (if (> (getvar "pickfirst") 0) 
    (setq ss 
      (ssget "_I" '(
                     (-4. "<OR")
                      (0. "INSERT")
                      (0. "POLYLINE") 
                      (0. "LWPOLYLINE")
                     (-4. "OR>")
                   )
      )
    ) 
  ) 
  ; If objects were not selected, prompt now 
  (if (= ss nil) 
    (setq ss (ssget '((-4. "<OR")(0. "INSERT")(0. "POLYLINE") (0. "LWPOLYLINE")(-4. "OR>")))) 
  ) 
  ; Use current implementation of the Explode command 
  (initcommandversion 2) 
  ; If objects were selected, explode them 
  (if (/= ss nil) 
    (command "._explode" ss "") 
  ) 
(princ) 
) 
; Undefine the Explode command 
(command "._undefine" "explode")
```

1-3『

这里有 2 点收获。（2021-03-02）

1、语句 `(> (getvar "pickfirst") 0)` 应该可以获取当前已经选择的数据集，类似于 CAD 自带命名前加上选项 `P`，待验证。

[PickFirst Property (ActiveX)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-A6E39C97-5758-4B08-9258-4002659F6FC4)

2、语句 `(initcommandversion 2)` 实现：Forces the next command to run with the specified version.

[initcommandversion (AutoLISP)](https://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-6176FC98-DC5D-433E-8D76-F481BE68D46A)

』

A command is undefined in a drawing while it remains open after the use of the undefine command; the standard functionality of a command is restored when a drawing is created or opened. You can use the redefine command to restore an undefined command while a drawing remains open. Here is an example statement that restores the standard explode command, which was undefined in the previous example:

```c
(command "._redefine" "explode")
```

### 10.5 Defining a Startup Function

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

getvar — Returns the current value of a system variable.

setvar — Assigns a new value to a system variable.

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

### 10.6 Loading AutoLISP Files

AutoLISP programs that are stored in a LSP file must be loaded into AutoCAD before they can be used. A number of methods can be used to load a LSP file. These fall into one of two categories: manual or automatic. Most LSP files are loaded using one of the manual techniques.

#### 10.6.1 Manually Loading an AutoLISP File

AutoCAD is a graphics- and resource-intensive application, and it loads components into memory only as each is needed. LSP files are typically rather small in size, but loading a large number of them into AutoCAD can impact performance. For this reason, you should load a LSP file only as it is needed. Once a LSP file is loaded into memory, it is not removed from memory until you close AutoCAD or the drawing from which the LSP file was loaded.

Use the following techniques to manually load a LSP file into AutoCAD:

1 Load/Unload Applications Dialog Box (appload Command). The Load/Unload Applications dialog box allows you to browse to where your LSP files are stored and select which files you want to load. After selecting a LSP file, you click Load to load the file into memory. I explain how to load a LSP file with the Load/Unload Applications dialog box in the「Using the Load/Unload Applications Dialog Box to Load a LSP File」section later in this chapter.

2 Drag and Drop (Windows Only). LSP and other types of files can be dragged and dropped onto either the application or drawing windows of AutoCAD on Windows. When you drop a LSP file onto an open drawing window, AutoCAD loads the LSP file into memory for that drawing only.

1-2『长见识了，lsp 文件竟然可以直接拖进去。做一张任意卡片。（2021-03-02）』——已完成

3 AutoLISP load Function. The AutoLISP load function allows you to load a LSP file from a script file, from a command macro defined in a CUI/CUIx file, at the AutoCAD Command prompt, or even from another LSP file. When you use the load function, it searches the paths that are listed under the Support File Search Path node in the Options dialog box (Windows) or Application Preferences dialog box (Mac OS). You should avoid using absolute file paths with the load function; if your drive mappings or folder structure change, the LSP file will fail to load.

TIP: The load function can be used in a menu macro — applied to a ribbon or toolbar button on Windows or a toolset button or menu item on Mac OS — to load a LSP file and start a function from the AutoCAD user interface. I explained how to customize the user interface in Chapter 5,「Customizing the AutoCAD User Interface for Windows」and Chapter 6,「Customizing the AutoCAD User Interface for Mac.」

The following is an example of loading a LSP file named utility.lsp with the load function:

```c
(load "utility.lsp")
```

NOTE: LSP files that are loaded using one of the manual techniques described here are loaded only into the current drawing. You must load the LSP file into each and every drawing file where you want to use it. However, you can use the vl-load-all function to load a LSP file into all open and subsequently opened drawings for the current AutoCAD session.

1-3『

这里又意外解决一个老大难的问题，新打开的文件可以自动加载数据流的插件。补充进任意卡片「如何在一个 lsp 文件里调用另外一个 lsp 文件」。（2021-03-02）——已完成

单独新建了一个启动文件 `startdataflow.lsp`。

```c
(defun s::startup ()
  (vl-load-all "D:\\dataflowcad\\dataflow.VLX")
)
```

前面正好讲到，函数 `s::startup` 是可以自动加载的。

』

#### 10.6.2 Automatically Loading an AutoLISP File

Manually loading LSP files doesn't always create the best user experience, especially if you want certain functions to be available in each drawing file that is opened or created. Keep in mind, though, you don't want all of your LSP files to be loaded at startup because it takes away some of the computing resources from the operating system and AutoCAD.

You can use the following techniques to automatically load a LSP file into AutoCAD:

1 Startup Suite — `(appload Command)`. The Startup Suite is part of the Load/Unload Applications dialog box (appload command). When a LSP file is added to the Startup Suite, the file is loaded after a drawing is opened. Removing a file from the Startup Suite causes the file not to be loaded in any future drawings that are opened but does not unload it from any drawing files that the LSP file was loaded into during the current session. If you want to use the Startup Suite to load LSP files, you must add the files to the Startup Suite on each workstation and AutoCAD user profile. I discuss how to add LSP files to the Startup Suite in the「Using the Load/Unload Applications Dialog Box to Load a LSP File」section later in this chapter.

2 Specific File Naming. When you start AutoCAD or open a drawing, LSP files with specific names are automatically loaded if they are found in the support file search paths. Table 20.1 lists the filenames and order in which these files are loaded into AutoCAD (files are listed in the order they are loaded by AutoCAD; acad.rx is loaded first and then on down the list).

In addition to the files listed in Table 20.1, the LSP files you added to the Startup Suite in the Load/Unload Applications dialog box are loaded after each MNL file with the same name as a CUI/CUIx file being loaded into AutoCAD. After the files in the Startup Suite are loaded, the function `(s::startup)` is executed. The last file that is executed is the script file that is loaded with the /b or -b command-line switch. You learned about command-line switches in Chapter 4,「Manipulating the Drawing Environment.」

NOTE: On Windows, LSP files can also be loaded when a CUI/CUIx file is loaded. When a CUI/CUIx file is being edited with the Customize User Interface Editor (cui command), you can add LSP files to the LISP Files node.

3 AutoLISP autoload Function. The AutoLISP autoload function allows you to load a LSP file based on the use of a function defined with the C: prefix in the file. When you use the autoload function, it searches the paths that are listed under the Support File Search Path node in the Options dialog box (Windows) or Application Preferences dialog box (Mac OS) for the LSP file and then loads the file before executing the function. You should avoid using absolute file paths with the autoload function, because if your drive mappings or folder structure change, the LSP file will fail to load. The expressions that use the autoload function should be loaded at startup. Consider adding these expressions to a LSP file and loading the file using a file like acaddoc.lsp or an MNL file.

The following is an example that loads a LSP file named maincmds.lsp with the autoload function when either the drawrectangle, drawcircle, loadlayers, or inserttitleblock function is typed at the Command prompt by the user:

```c
(autoload "maincmds" '("drawrectangle" "drawcircle" "loadlayers" "inserttitleblock"))
```

4 Plug-in Bundles. Plug-in bundles allow you to load LSP and other custom files in AutoCAD 2013 or later. A plug-in bundle is a folder structure with a special name and metadata file that describes the files contained in the bundle. I discuss plug-in bundles in the「Defining a Plug-in Bundle」section later in this chapter.

Table 20.1 Automatically loaded LSP files

| Filename | Description |
| --- | --- |
| acad.rx | Lists each ObjectARX application (ARX) file that should be loaded. This file is not created by default; it is a file that you must create. Most ARX files are loaded on demand using special entries in the Windows Registry or property list (Plist) files on Mac OS. |
| acad`<release>`.lsp | A release-specific LSP file that is loaded once per AutoCAD session, at startup. `<release>` is a value that represents the release of AutoCAD. For example, AutoCAD 2015 looks for the file named acad2015.lsp, AutoCAD 2014 looks for the file named acad2014.lsp, AutoCAD 2013 looks for the file named acad2013.lsp, and so on. |
| acad.lsp |  A LSP file that is loaded once per AutoCAD session, at startup. If the acadlspasdoc system variable is set to 1, the file is loaded with each drawing just like acaddoc.lsp. The acad.lsp file must be created if you want to use it since it is not part of the AutoCAD installation. I discussed how to create a LSP file in the「Creating an AutoLISP File」section earlier in this chapter. |
| acad`<release>`doc.lsp | A release-specific LSP file that is loaded with each drawing file that is opened. `<release>` is a value that represents the release of AutoCAD. For example, AutoCAD 2015 looks for the file named acad2015doc.lsp, AutoCAD 2014 looks for the file named acad2014doc.lsp, AutoCAD 2013 looks for the file named acad2013doc.lsp, and so on. |
| acaddoc.lsp | A LSP file that is loaded with each drawing file that is opened. The file acaddoc.lsp must be created if you want to use it since it is not part of the AutoCAD installation. |
| `<filename>`.mnl | MNL files are associated with CUI/CUIx files that are used to define the AutoCAD user interface. When a CUI/CUIx file is loaded, AutoCAD looks for an MNL file with the same name and loads it if found. MNL files are loaded in the same order that CUI/CUIx files are. CUI/CUIx files are loaded in the order of partial files to the Main CUI/CUIx file, Main CUI/CUIx file, partial files to the Enterprise CUI/CUIx file, and then the Enterprise CUI/CUIx file. |

#### 10.6.3 Using the Load/Unload Applications Dialog Box to Load a LSP File

The Load/Unload Applications dialog box (appload command) is the easiest way to load a LSP file into AutoCAD on Windows or Mac OS. Many of the other methods provide better integration into a user's workflow, but they require you to define where the LSP files are located. I describe in the next section how to set up and identify the folders AutoCAD should look in for custom files.

The following steps explain how to load the mylisp.lsp file that you created in the「Creating an AutoLISP File」section earlier.

NOTE: If you did not complete the steps in the「Creating an AutoLISP File」section, you can use the `ch20_mylisp_complete.lsp` file that is part of the samples files for this book (available from this book's web page at www.sybex.com/go/autocadcustomization) that you copied to a folder named MyCustomFiles in your Documents (or My Documents) folder. Once the sample file is stored on your system, remove the characters ch20_ from the filename. If you placed the sample files in a different folder, you will need to make the appropriate changes to the file selected in step 2.

1 Do one of the following:

1.1) On the ribbon, click the Manage tab Customization panel Load Application (Windows).

1.2) On the menu bar, click Tools Load Application (Mac OS).

1.3) At the Command prompt, type appload and press Enter (Windows and Mac OS).

2 When the Load/Unload Applications dialog box (see Figure 20.2) opens, browse to the MyCustomFiles folder and select the mylisp.lsp file. Click Load.

TIP: If the Add To History check box is selected when you click Load, AutoCAD adds the selected file to a list box on the History tab. Click the History tab and then select the file you want to load. Then click Load to load the file.

3 If the File Loading — Security Concern message box is displayed, click Load. You'll learn which paths contain custom files that should be trusted in the「Identifying Trusted Locations」section and the sidebar「Restricting Custom Applications」later in this chapter.

4 Click Close to return to the drawing area.

5 At the Command prompt, type msg and press Enter. A message box with the text First AutoLISP file is displayed (see Figure 20.1).

6 Click OK to close the message box.

7 Press F2 on Windows or Fn-F2 on Mac OS. You should see the message Version 1.0 – My AutoLISP Programs displayed in the command-line window.

8 Create a new drawing.

9 At the Command prompt, type msg and press Enter. The message Unknown command "MSG". Press F1 for help. is displayed.

NOTE: If you are using AutoCAD 2014 or later, typing msg in step 9 might start the mspace or another command. If you don't see the Unknown command message, you will need to disable AutoCorrect. To disable AutoCorrect, at the AutoCAD Command prompt type -inputsearchoptions and press Enter. Then type r and press Enter. Type n and press Enter twice. Repeat step 9 and you should see the expected results.

Figure 20.2 Loading a custom program

You can use the following steps to add the LSP file named mylisp.lsp to the Startup Suite you created in the「Creating an AutoLISP File」section.

1 Do one of the following:

1.1) On the ribbon, click the Manage tab Customization panel Load Application (Windows).

1.2) On the menu bar, click Tools Load Application (Mac OS).

1.3) At the Command prompt, type appload and press Enter (Windows and Mac OS).

2 When the Load/Unload Applications dialog box opens, in the Startup Suite section, click Contents.

3 When the Startup Suite dialog box (see Figure 20.3) opens, click Add (Windows) or + (Mac OS).

4 In the Add File to Startup Suite dialog box, browse to the MyCustomFiles folder and select the mylisp.lsp file. Click Open.

5 In the Startup Suite dialog box, click Close.

6 In the Load/Unload Applications dialog box, click Close.

7 At the Command prompt, type msg and press Enter. A message box with the text First AutoLISP file is displayed.

8 Click OK to close the message box.

9 Create a new drawing.

10 At the Command prompt, type msg and press Enter. A message box with the text First AutoLISP file is displayed. This is expected because the mylisp.lsp file is loaded into the new drawing as a result of being added to the Startup Suite.

11 Click OK to close the message box.

Figure 20.3 Adding a LSP file to the Startup Suite

### 10.7 Managing the Locations of AutoLISP Files

The LSP files that you create or download from the Internet can be placed in any folder on your local or network drive. I recommend placing all your custom LSP files in a single folder on a network drive so they can be accessed by anyone in your company who might need them. You might consider using the name LSP Files or AutoLISP Files for the folder that contains your LSP files.

1『作者建议 lsp 文件放在远程的网盘，好主意。（2021-03-02）』

I also recommend marking any folder(s) that contains custom files on the network as read-only for everyone except for those designated to make updates to the files. Marking the folders as read-only helps prevent undesired or accidental changes. Chapter 10,「Using, Loading, and Managing Custom Files,」discussed file management.

Regardless of which folder name you use or where you choose to place your LSP files, you need to let AutoCAD know where these files are located. To do so, add each folder that contains LSP files to the Support File Search Path and Trusted Locations settings of the Options dialog box (Windows) or Application Preferences dialog box (Mac OS).

NOTE: The following sections assume you have created a folder named MyCustomFiles in the Documents (or My Documents) folder for the exercises and sample files that are part of this book. (If you haven't already, you can download the files from www.sybex.com/go/autocadcustomization.) If you placed the sample files in a different folder or are using your own folder, select that folder instead when prompted to browse to a folder as part of the steps.

#### 10.7.1 Specifying Support File Search Paths

The support file search paths are used by AutoCAD to locate custom files, such as those that contain block definitions, linetype patterns, and AutoLISP programs. Use the Options dialog box on Windows and the Application Preferences dialog box on Mac OS to add the folders that contain LSP files to the support file search paths of AutoCAD.

The following steps explain how to add the folder named MyCustomFiles to the support file search paths used by AutoCAD:

1 Click the Application menu button Options (or at the Command prompt, type options and press Enter).

2 When the Options dialog box opens, click the Files tab.

3 Select the Support File Search Path node. Click Add and then click Browse.

4 In the Browse For Folder dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents (or My Documents) folder, or browse to the folder that contains the LSP files.

5 Select the folder that contains your LSP files and click OK.

6 Click OK to save the changes to the Options dialog box.

If you are using AutoCAD on Mac OS, use these steps:

1 On the menu bar, click AutoCAD `<release>` Preferences (or at the Command prompt, type options and press Enter).

2 When the Application Preferences dialog box opens, click the Application tab.

3 Select the Support File Search Path node.

4 Near the bottom of the dialog box, click the plus sign (+).

5 In the Open dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents folder, or browse to the folder that contains the LSP files.

6 Select the folder that contains the LSP files and click Open.

7 Click OK to save the changes to the Application Preferences dialog box.

You can edit an existing folder in the Options or Application Preferences dialog box by expanding the Support File Search Path node and selecting the folder you want to edit. After selecting the folder to edit, click Browse in Windows or double-click the folder on Mac OS, and then select the new folder.

TIP: You can test to see whether AutoCAD can locate a file that might be in the support file search paths by using the AutoLISP findfile function. For example, type `(findfile "mylisp.lsp")` at the AutoCAD Command prompt to see if the file named mylisp.lsp is in one of the support file search paths. The location of the file is returned if it is found or nil if the file is not found.

It is possible with AutoLISP to get a listing of which folders have been added to the Support File Search Paths setting using the acadprefix system variable. The acadprefix system variable can return a listing of folders, but it doesn't allow you to update which folders should be used. However, you can use the ACAD environment variable to update which folders are used.

The following code shows an example of adding a folder named lsp files (which is at the root level of the C: drive on Windows) to the support file search paths using the ACAD environment variable:

```c
(setenv "ACAD" (strcat (getenv "ACAD") ";c:\\lsp files;"))
```

If you are using AutoCAD on Mac OS, the same sample would look like this:

```c
(setenv "ACAD" (strcat (getenv "ACAD") ";/lsp files;"))
```

You must place a semicolon before the location you are adding; including a semicolon after the location is not required. Typically, a semicolon is provided by AutoCAD after the last location, but you should check to see whether there is one. If you add the location with a semicolon before the path and a semicolon is provided by AutoCAD, resulting in back-to-back semicolons, the second semicolon is removed by AutoCAD.

NOTE: If the location added with the ACAD environment variable is invalid, AutoCAD doesn't remove the invalid location. You might receive a message when you make changes to the Options or Application Preferences dialog box. Although it is possible to add the same location more than once with the ACAD environment variable, AutoCAD removes the duplicate entries in most cases. You should avoid adding duplicate locations, since it can increase the time it takes AutoCAD to locate a file.

#### 10.7.2 Identifying Trusted Locations

If you are using AutoCAD 2013 SP1 or later on Windows or AutoCAD 2014 on Mac OS, when you try to load a LSP file, AutoCAD checks to see if that LSP file is being loaded from a trusted location. A folder that you identify as a trusted location contains LSP files that are safe to be loaded without user interaction. Any LSP file that isn't loaded from a trusted location results in the File Loading — Security Concern message box (see Figure 20.4) being displayed.

Figure 20.4 This security warning informs you of a LSP file being loaded from an untrusted location.

The File Loading — Security Concern message box indicates why it might not be a good idea to load the file if its origins aren't known. While the message box is displayed, the user can decide to either load or not load the file that AutoCAD is attempting to load. When adding new trusted locations, you want to make sure you limit the number of folders you trust, and those that are trusted should be marked as read-only to avoid the introduction of unknown LSP files to the folders. For more information on trusted paths, see the trustedpaths system variable in the AutoCAD Help system.

NOTE: A folder that you identify as a trusted location must also be listed in the Support File Search Paths setting of the Options or Application Preferences dialog box.

The following steps explain how to add the folder named MyCustomFiles to the trusted locations that AutoCAD can use to safely load LSP and other custom programs.

1 Click the Application menu button Options (or at the Command prompt, type options and press Enter).

2 When the Options dialog box opens, click the Files tab.

3 Select the Trusted Locations node and click Add, and then click Browse.

4 In the Browse For Folder dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents (or My Documents) folder, or browse to the folder that contains your LSP files.

5 Select the folder that contains your LSP files and click OK.

6 If the selected folder is not marked as read-only, the Trusted File Search Path — Security Concern dialog box is displayed. Click Continue to add the folder.

7 Click OK to save the changes to the Options dialog box.

If you are using AutoCAD on Mac OS, use these steps:

1 At the AutoCAD Command prompt, type `(setq mydocs (getvar "mydocumentsprefix"))` and press Enter. The location of the My Documents folder is assigned to the user-defined variable mydocs.

2 At the Command prompt, type `(setq trustedpath (strcat mydocs "/MyCustomFiles/"))` and press Enter. The path to the MyCustomFiles folder is assigned to the user-defined variable trustedpath. Use a different folder name or location here if the LSP files are stored in a different folder.

3 At the Command prompt, type `(setq trustedpaths (strcat (getvar "trustedpaths") ";" trustedpath ";"))` and press Enter. The path you provided and those that are already trusted are appended together and assigned to the user-defined variable trustedpaths.

4 At the Command prompt, type (setvar "trustedpaths" trustedpaths) and press Enter. The paths in the user-defined variable trustedpaths are assigned to the trustedpaths system variable.

You can also use these steps for adding a trusted location in AutoCAD on Mac OS with AutoCAD on Windows. Instead of using forward slashes in step 2, use two backward slashes to be consistent with the value returned by the mydocumentsprefix system variable in step 1. For step 2, you would type `(setq trustedpath (strcat mydocs "\\MyCustomFiles\\"))`.

TIP: You can test to see whether AutoCAD can locate a file in a trusted location by using the AutoLISP findtrustedfile function. For example, type `(findtrustedfile "mylisp.lsp")` at the AutoCAD Command prompt to see if the file named mylisp.lsp is in a trusted location and the AutoCAD support file search paths. The location of the file is returned if it is found or nil if the file is not found.

#### Restricting Custom Applications

Starting with AutoCAD 2013 SP1, Autodesk introduced some new security measures to help reduce potential threats or viruses that could affect AutoCAD and the drawing files you create. These security measures allow you to do the following:

1 Disable the loading of executable code when AutoCAD is started using the /nolisp (AutoCAD 2013 SP1 on Windows), /safemode (AutoCAD 2014 on Windows), or -safemode (AutoCAD 2014 on Mac OS) command-line switch.

2 Automatically load and execute specially named files: acad.lsp, acad.fas, acad.vlx, acaddoc.lsp, acaddoc.fas, acaddoc.vlx, and acad.dvb.

In AutoCAD 2014, you can use the secureload system variable to control whether AutoCAD will load files only from trusted locations or allow you to load custom files from any location. I recommend setting secureload to 2 and loading custom files only from a secure and trusted location. However, the default value of 1 for secureload is also fine since it displays a message box when AutoCAD tries to load a file from a nontrusted location. Don't set secureload to 0, thereby disabling the security feature, because it could result in your system loading a malicious program.

1『原来加载插件的信任等级有一个系统变量（secureload）。（2021-03-05）』

### 10.8 Deploying AutoLISP Files

Deployment is the process or processes used to allow others to access the LSP and custom files that you create. You might only need to worry about getting your files into the hands of those working at your company, but you might also want to send your files out to the subcontractors that your company works with. Sharing your custom files with subcontractors can help shorten turnaround times and makes it easier to share drawings back and forth.

Deploying custom programs internally and externally are similar processes, but you may encounter some issues. Here are some issues that you need to consider when you are ready to deploy LSP files to others, either internally or externally:

1 Locating. Any file or folder paths used in your LSP files should be dynamic and not static. Never assume that there will always be a C drive or a specific network drive and folder structure on the workstation on which the LSP files will be loaded. Your programs should be designed to look for any files it needs as part of the Support File Search Path setting in the Options or Application Preferences dialog box. You learned how to add a folder to the Support File Search Path setting in the「Managing the Locations of AutoLISP Files」section earlier in this chapter.

2 Naming. Autodesk recommends, although it is completely optional, adding a unique prefix to the beginning of your custom functions, even to global variables. This unique prefix will help you avoid potential conflicts when your LSP files are loaded into AutoCAD on a workstation that could have unknown custom programs loaded as well. For example, I use `hypr_ as` my prefix of choice (it's a shortened version of HyperPics). A function name of `c:drawplate` would become `c:hypr_drawplate`. You could then create a custom (CUI/CUIX) file that adds your functions to the user interface or an alias-like LSP file that makes it easier to access your functions. Though not necessary — nor does it stop others from using your prefix — you can register the prefix you want to use at usa.autodesk.com/adsk/servlet/index?id=1075006&siteID=123112.

1『上面的网站已经失效了。（2021-03-05）』

3 Testing. Testing is a must when you begin deploying your files. I can't overemphasize how important testing is when you deploy your LSP files. You want to make sure your programs execute as expected on various workstations running AutoCAD. I discuss some common testing techniques in Chapter 19,「Catching and Handling Errors.」

1『目前自己搭建了单元测试框架，但感觉 19 张的异常处理机制也有用，可以整合进来。（2021-03-05）』

4 Documenting. Documentation is a key element you should consider providing for those who will install or use your LSP files. You should offer some basic documentation so end users understand the functions that are exposed. Explain how to resolve any common problems they might have with your LSP files. I mention how to register help to custom functions in the「Implementing Help for Custom Functions」section later in this chapter.

5 Distributing. Make sure you have the rights to redistribute all support files that the LSP files might need. Typically, the only files that are commonly licensed are TrueType font (TTF) files, but licensing can extend to any files that you or your company have purchased or maybe even downloaded for free from the Internet.

1-2『可以通过这里的关键词搜搜如何做证书。（2021-03-04）』—— 未完成

6 Updating. Create a plan to keep files up to date. Updating is something you need to consider before you deploy your custom files the first time.

#### 10.8.1 Deployment Methods (Local vs. External)

Releasing custom and LSP files to others in your company is often fairly straightforward because the files were developed around a set of known conditions; where files are located and which files are available is known, along with how AutoCAD was installed and configured. Internally, you can simply push your files to a location on the network and configure AutoCAD to look for the files there, as you learned earlier, in the「Managing the Locations of AutoLISP Files」section.

Once you post the files, users can load them manually as they are needed, or you can use one of the methods from the section「Loading AutoLISP Files.」You can also create and post a CUI/CUIx file for AutoCAD to load so that the user can load and access the functions in the LSP files without understanding how to load a LSP file. You learned about customizing the user interface in Chapters 5 and 6.

1-2『可以试试把文件「dataflowStart.lsp」绑在 cuix 里，这样应该可以确保打开一个新 CAD 程序自动加载数据流。待验证。（2021-03-05）』—— 未完成

Once a user can access and load the LSP files, I recommend providing basic instructions or even an informal training session to help them use the custom programs that you created. Making it as easy as possible for users to learn your custom programs will go a long way — it can mean the difference between a successful or a failed deployment. If users are confused, they are less likely to embrace the custom programs and the benefits they provide.

If you plan to deploy your custom programs to individuals outside your company, ask yourself the following questions:

1 How will the user obtain your custom programs? Will you post them on a website or deliver them as an Autodesk® Exchange app that can be used with AutoCAD on Windows? Posting the files directly on a website does allow you to support both Windows and Mac OS.

2 How will the user set up your custom programs? If a utility is free, users are usually a little more open to doing some work to get it recognized and loaded into AutoCAD. However, if you are expecting a user to pay for a program, their expectations change and you should consider using a plug-in bundle or creating an installer to make the deployment as easy and as error-free as possible.

1-2『这里第一次看到付费的实现途径：plug-in bundle。待探索。（2021-03-05）』—— 未完成

3 How will the user get help or support when there is a problem? A website is often the best solution when it comes to providing troubleshooting information or explaining how to use a program since it can be updated frequently. However, not all users have access to the Internet from their workstation. As shocking as it might be, it is not uncommon to have no connection or a limited connection at some companies. The level of support and documentation that you provide should be a direct representation of how simple or complex a program is to learn, along with the fee you are charging. A simple program will commonly require far less documentation than one that offers a lot of functionality or is complex. Users often expect less documentation when a custom program is free compared to when they are paying for it.

You can use one of three main methods to deploy your custom programs externally (or even internally):

1 Manually. A manual deployment is conducted when a user follows a detailed set of written instructions that explain how to set up the folder structure necessary for your custom program and then configures AutoCAD to look for the custom programs. After creating the folder structure and copying the files, the user commonly adds the necessary folders to the AutoCAD Support File Search Path and Trusted Locations settings, as explained in the「Managing the Locations of AutoLISP Files」section earlier in this chapter. Then they load the LSP files as necessary, as discussed in the「Loading AutoLISP Files」section. This approach is used frequently for many free AutoLISP programs found on the Internet. Although this is a low-cost approach, it can be error prone and is not ideal when the program needs to be set up on dozens of workstations.

2 Plug-in Bundle. A plug-in bundle is a folder structure that contains a manifest file that defines all the files making up the bundle and how AutoCAD should load the files within the bundle. A bundle can contain LSP, CUIx, MNL, help/documentation, and many other types of files. Because the manifest file tells AutoCAD how to load the files contained in the bundle, you don't need to provide much in the form of instructions that explain how your custom programs need to be set up. To use a plug-in bundle, after you create the manifest file and set up the desired folder structure, you simply copy all folders and files that make up the bundle to the ApplicationAddins or ApplicationPlugins folder on each workstation the bundle should be available on. Plug-in bundles were first supported in AutoCAD 2013 on Windows and Mac OS, and you can develop them so that they work across multiple AutoCAD releases, AutoCAD-based products, and operating systems. You'll learn the basics of defining a plug-in bundle in the upcoming section,「Defining a Plug-in Bundle.」

3 Installer. An installer provides you with a professional-looking front end that can automate the same steps that a user might follow to manually set up your custom program. Many different types of applications are available that you can use to create an installer, such as InstallAware Studio, InstallShield, Setup Factory, and even Microsoft Visual Studio Professional or higher on Windows. If you are using Mac OS, you can use an application such as PackageMaker or Disk Utility. You can use an installer to copy and remove files related to a plug-in bundle, or you can design it to perform a variety of tasks that can help users configure AutoCAD. You can configure many installers to allow for maintenance releases or to provide a way for a user to upgrade an existing installation to a newer release.

NOTE: If you are using any of the specially named files — such as acad.lsp or acaddoc.lsp — that AutoCAD looks for at startup to load your custom LSP files, you will need to figure out a different way to get them loaded before deploying the files outside your company. You don't want to affect another company's custom programs when they try to use your custom programs, so consider using a bundle plug-in or CUI/CUIx with/without an MNL file to get your LSP files loaded into AutoCAD.

#### 10.8.2 Defining a Plug-in Bundle

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

#### 10.8.3 Implementing Help for Custom Functions

Earlier in this chapter, I discussed the importance of using comments to document the AutoLISP expressions that make up your custom functions and AutoLISP programs. In addition to comments, when you create new functionality using AutoLISP you should create documentation for the users; the importance of user documentation is often overlooked by developers. Documentation can range from being as basic as a few sentences to something that is much more comprehensive and explains how to use all the functions that are exposed as part of your LSP files when they are loaded.

The AutoLISP help and setfunhelp functions are used to access the AutoCAD Help facility. Based on the release or platform on which you are developing, these functions support some or all of the following file types:

1 HTM/HTML.

2 Plain ASCII text (TXT).

3 Microsoft Help (CHM) – Windows only.

4 WinHelp (HLP) – Windows only.

The following shows the syntax for the AutoLISP help function:

```c
(help [filename [help_topic [chm_window_cmd]]])
```

Its arguments are as follows:

filename. The filename argument is a string that represents the name of the HTM, HTML, CHM, HLP, or TXT file that is to be opened by the AutoCAD Help facility. You must specify both the filename and path. This argument is optional, and AutoCAD opens the Help system if it is not provided.

1 `help_topic`. The `help_topic` argument is a string that represents the standard AutoCAD Help topic to open or the topic file to open when a CHM file is specified by the filename argument. This argument is optional and only used when a CHM file is specified.

2 `chm_window_cmd`. The `chm_window_cmd` argument is an integer used to control the behavior of the HTML Help window that is opened for a CHM file. This argument is optional and available only when a CHM file is specified.

3 Here are some example expressions that demonstrate the use of the AutoLISP help function:

1『目前数据流的文档说明放在 web 端。（2021-03-05）』

```c
; Opens the AutoCAD Help system with no topic 
(help) 
; Opens the reference topic for the AutoCAD Rectang command 
(help "" "rectang") 
; Opens the specified URL in the system's default web browser 
(help "http://www.sybex.com/go/autocadcustomization") 
; Opens a local HTML file on Windows 
(help "C:\\Program Files\\Autodesk\\AutoCAD 2015\\Help\\augi.htm") 
; Opens a local HTML file on Mac OS 
(help "/Applications/Autodesk/AutoCAD 2015/AutoCAD 2015.app/Contents/Resources/ExtendedResources.htm") 
; Opens a CHM file named acadauto to the topic idh_lightweightpolyline_object 
(help "C:\\Program Files\\Common Files\\Autodesk Shared\\acadauto.chm" "idh_lightweightpolyline_object")
```

The following shows the syntax for the AutoLISP setfunhelp function:

```c
(setfunhelp function_name [filename [help_topic [chm_window_cmd]]])
```

Its arguments are as follows:

1 `function_name`. The `function_name` argument represents the user-defined function prefixed with C: with which you want to associate a help file or topic.

2 filename. The filename argument is a string that represents the name of the HTM, HTML, CHM, HLP, or TXT file that is to be opened by the AutoCAD Help facility. You must specify both the filename and path. This argument is optional, and AutoCAD opens the Help system if it is not provided.

3 `help_topic`. The `help_topic` argument is a string that represents the standard AutoCAD Help topic to open or the topic file to open when a CHM file is specified by the filename argument. This argument is optional and used only when a CHM file is specified.

4 `chm_window_cmd`. The `chm_window_cmd` argument is an integer used to control the behavior of the HTML Help window that is opened for a CHM file. This argument is optional and available only when a CHM file is specified.

Here are some examples that demonstrate the use of the AutoLISP setfunhelp function. These examples are based on the existence of an AutoLISP function named c:drawplate. When the c:drawplate function is active or its name is entered at the Command prompt, the topic associated with the function is displayed when the user presses F1.

```c
; Launches the the AutoCAD help system with no topic 
(setfunhelp "c:drawplate") 
; Opens the reference topic for the AutoCAD Rectang command 
(setfunhelp "c:drawplate" "" "rectang") 
; Opens the specified URL in the system's default web browser 
(setfunhelp "c:drawplate" "http://www.sybex.com/go/autocadcustomization") 
; Opens a local HTML file on Windows 
(setfunhelp "c:drawplate" "C:\\Program Files\\Autodesk\\AutoCAD 2015\\Help\\augi.htm") 
; Opens a local HTML file on Mac OS 
(setfunhelp "c:drawplate" "/Applications/Autodesk/AutoCAD 2015/ AutoCAD 2015.app/Contents/Resources/ExtendedResources.htm") 
; Opens a CHM file named acadauto to the topic idh_lightweightpolyline_object 
(setfunhelp "c:drawplate" "C:\\Program Files\\Common Files\\Autodesk Shared\\acadauto.chm" "idh_lightweightpolyline_object")
```

### 10.9 Exercise: Deploying the drawplate Function

In this section, you will continue to work with the drawplate function that was originally introduced in Chapter 12,「Understanding AutoLISP.」You worked with the drawplate function in Chapter 19 and added error handling and undo grouping to the function. The key concepts I cover in this exercise are as follows:

1 Identifying the Locations of Your LSP Files AutoCAD needs to know where your LSP files are so that it can locate them and know which locations are trusted.

2 Loading a LSP File on Demand and by Reference AutoLISP files should be loaded only as they are needed whenever possible to help save on system resources.

3 Connecting Custom Help Supporting basic help files is something many developers overlook, but this support can help give your programs a polished and professional look. Users also appreciate when there is some form of self-help that might aid them in solving a problem they are having or learning about a feature.

4 Creating and Deploying Plug-in Bundles Plug-in bundles can make deploying AutoLISP programs easier than having to set up support file search paths and trusted locations on multiple machines, and it allows you to support multiple releases of a program with much greater ease.

NOTE: The steps in this exercise depend on the completion of the steps in the「Exercise: Handling Errors in the drawplate Function」section of Chapter 19. If you didn't complete the steps, do so now or start with the `ch20_drawplate.lsp` and `ch20_utility.lsp` sample files available for download from www.sybex.com/go/autocadcustomization. You will also need the packagecontents.xml and drawplate.htm sample files. Place these sample files in the MyCustomFiles folder under the Documents (or My Documents) folder or in the location you are using to store the LSP files. Once you've stored the sample files on your system, remove the characters ch20_ from the name of each file.

#### 10.9.1 Loading the utility.lsp File by Reference

When an AutoLISP program relies on the functions defined in another LSP file, it is common practice to use the load function to ensure that the functions in the LSP file are made available. Up until now, you have been manually loading the utility.lsp file each time you wanted to use the functions that are defined in the file. The following steps explain how to load the utility.lsp file when drawplate.lsp is loaded into AutoCAD:

1 Open the drawplate.lsp file in Notepad on Windows or TextEdit on Mac OS.

2 In the text editor area, add the following before any other comments or AutoLISP expressions in the file:

```c
; Load the utility.lsp file 
(load "utility.lsp")
```

3 Click File Save.

NOTE: The load function can be used with a menu macro to load a LSP file from the AutoCAD user interface.

#### 10.9.2 Loading the drawplate.lsp File on Demand

Loading all your AutoLISP programs at startup is an option using load statements in a LSP file such as acad.lsp or acaddoc.lsp, but you should load only the files when they are needed. The autoload function is a way to inform AutoCAD that you have a set of custom functions that are standing by and ready for use. Instead of using multiple load statements in acad.lsp or acaddoc.lsp, I recommend using autoload statements to make your functions available and load the associated LSP file upon the function's first use.

In these steps, you create a new LSP file named myautoloader.lsp that will load the drawplate.lsp file when the user enters drawplate at the Command prompt:

1 Create a new LSP file named myautoloader.lsp with Notepad on Windows or TextEdit on Mac OS.

2 In the text editor area of the myautoloader.lsp file, type the following:

```c
; Demand loads the drawplate.lsp file 
(autoload "drawplate" '("drawplate"))
```

3 Click File Save.

NOTE: If your company doesn't already have an acad.lsp file, you could rename myautoloader.lsp to acad.lsp and let AutoCAD load the file automatically. Use the statement `(findfile "acad.lsp")` to determine whether a file named acad.lsp already exists in the support file search paths of your AutoCAD installation. If nil is returned, AutoCAD couldn't locate an instance of the acad.lsp file.

1『很赞，可以把自动加载数据流的语句直接放到文件「acad.lsp」里去。』

#### 10.9.3 Enabling Help Support for the drawplate Function

Providing basic help support for your programs can go a long way, especially if you leave the company someday or want to eventually sell your custom program.

In these steps, you enable contextual help for the drawplate function:

1 Open the drawplate.lsp file in Notepad on Windows or TextEdit on Mac OS, if it isn't open from the earlier exercise.

2 In the text editor area, scroll to the end of the file and add a few blank lines. Add the following to the end of the file: 

```c
; Register the help file for F1/contextual help support 
(setfunhelp "c:drawplate" (findfile "DrawPlate.htm"))
```

3 Click File Save.

#### 10.9.4 Configuring the AutoCAD Support and Trusted Paths

In order for the AutoLISP load and findfile functions to locate the files for your custom programs, AutoCAD needs to know where the files are located. To locate a custom file, AutoCAD uses the paths that have been added to the Support File Search Path and Trusted Locations settings in the Options dialog box (Windows) or the Application Preferences dialog box (Mac OS).

The following steps explain how to add the folder named MyCustomFiles to the support file search paths and trusted locations used by AutoCAD:

1 Click the Application menu button Options (or at the Command prompt, type options and press Enter).

2 When the Options dialog box opens, click the Files tab.

3 Select the Support File Search Path node. Click Add and then click Browse.

4 In the Browse For Folder dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents (or My Documents) folder, or browse to the folder that contains your LSP files.

5 Select the folder that contains your LSP files and click OK.

6 With the new path still highlighted, press F2. Press Ctrl+C, or right-click and choose Copy.

7 Select the Trusted Locations node. Click Add.

8 With focus on the in-place text editor, press Ctrl+V, or right-click and choose Paste. Then press Enter to accept the pasted path.

9 If the Trusted File Search Path — Security Concern message box appears, click Continue.

10 Click OK to save the changes to the Options dialog box.

If you are using AutoCAD on Mac OS, use these steps:

1 On the menu bar, click AutoCAD `<release>` Preferences (or at the Command prompt, type options and press Enter).

2 When the Application Preferences dialog box opens, click the Application tab.

3 Select the Support File Search Path node.

4 Near the bottom of the dialog box, click the plus sign (+).

5 In the Open dialog box, browse to the MyCustomFiles folder that you created for this book in the Documents folder, or browse to the folder that contains your customized files.

6 Select the folder that contains your customized files and click Open.

7 Click OK to save the changes to the Application Preferences dialog box.

WARNING: Executing the AutoLISP expressions in step 8 more than once will result in the folder being added multiple times to the Trusted Locations setting. You should make sure the folder you are adding is not already listed as part of the trustedpaths system variable. I don't know whether listing the folder more than once is a problem, but ideally you should not list the same folder multiple times.

8 At the Command prompt, type `(prompt (getvar "trustedpaths"))` and press Enter. If the MyCustomFiles folder or the location of the drawplate.lsp file is listed, type one of the following and press Enter:

```c
(setq trustedpath (strcat (getvar "trustedpaths") ";" (vl-filename-directory (findfile "drawplate.lsp")) "/;"))
```

or

```c
(setvar "trustedpaths" trustedpath)
```

#### 10.9.5 Testing the Deployment of the drawplate Function

The time has come to put in motion everything that you have done up to this point. You have added statements that load the utility.lsp file from drawplate.lsp, defined an autoloader program, enabled contextual help for the drawplate function, and configured the support file search and trusted location paths. It is now time to see all of it in action. If all goes well, it will feel like you are hearing the climax of a movement being played by an orchestra. If something doesn't go right, you will have that meh moment, but don't feel discouraged; we have all been there.

The following steps explain how to use the load function to add the myautoloader.lsp file into AutoCAD from the Command prompt. Once it's loaded, you will then start the drawplate function and test the help file with which it has been associated.

1 At the Command prompt, type `(load "myautoloader")` and press Enter. If you see the error message ; error: LOAD failed: "myautoloader", make sure that the file was placed in the MyCustomFiles folder and that the folder is part of the Support File Search Path setting. A return value of nil is expected by the load function.

2 Type drawplate and press Enter. You should see the familiar Specify base point for plate or [Width\Height]: prompt. Remember, you didn't load the drawplate.lsp or utility.lsp file yourself. You simply loaded myautoloader.lsp and it loaded drawplate.lsp when you started the drawplate function. Upon loading, the drawplate.lsp file then loaded utility.lsp.

3 With the drawplate function still active, press F1 on Windows or Fn-F1 on Mac OS. The custom help documentation associated with the drawplate function is shown. Figure 20.5 shows what the document looks like in the AutoCAD Help window on Windows. On Mac OS, the topic is opened in your system's default browser.

4 Press Esc to end the drawplate function.

Figure 20.5 Custom help for a custom function

1-2『直接在 CAD 里调帮助文档，也不错的，有时间可以实现看看。web 的文档优势在于能放的东西更多，比如视频动图。（2021-03-05）』—— 未完成

#### 10.9.6 Creating DrawPlate.bundle

Plug-in bundles are a relatively new concept in AutoCAD, but they make deploying your custom programs much easier. After all, a bundle is simply a folder structure that you can copy between machines no matter which operating system you are using. The following steps explain how to create a bundle named DrawPlate.bundle.

1 On Windows, do one of the following: 1) Launch Windows Explorer or File Explorer, depending on your version of the operating system. (Right-click the Windows Start button on Windows XP or Windows 7, or right-click in the lower-left corner of the screen on Windows 8. Click Windows Explorer or File Explorer.) 2) Browse to the MyCustomFiles folder under the Documents (or My Documents) folder. Right-click in an empty area and choose New Folder.

2 On Mac OS, do one of the following: 1) Launch Finder. (On the Desktop, click Go Documents.) 2)Browse to the MyCustomFiles folder under the Documents (or My Documents) folder. Click Settings (the gear icon) near the top center of the Finder window and choose New Folder.

3 Type DrawPlate.bundle and press Enter.

4 Do one of the following: 1) On Windows, double-click the DrawPlate.bundle folder. 2) On Mac OS, secondary-click DrawPlate.bundle and choose Show Package Contents.

5 Create a new folder under the DrawPlate.bundle folder and name the new folder Contents.

6 From the sample files that are available with this book and those that you created, copy the following files into the appropriate folder (see Table 20.2).

Table 20.2 Files for DrawPlate.bundle

| Filename | Folder |
| --- | --- | --- |
| packagecontents.xml | DrawPlate.bundle |
| utility.lsp | Contents |
| drawplate.lsp | Contents |
| drawplate.htm | Contents |

#### 10.9.7 Deploying and Testing the DrawPlate.bundle

Plug-in bundles must be placed within a specific folder before they can be used. You learned which folders a bundle can be placed in earlier, in the section「Defining a Plug-in Bundle.」The following steps explain how to deploy a bundle named DrawPlate.bundle on Windows:

1 In Windows Explorer or File Explorer, browse to the DrawPlate.bundle folder you created in the previous exercise.

2 Select the DrawPlate.bundle folder and right-click. Choose Copy.

3 In the Location/Address bar of Windows Explorer or File Explorer, type one of the following and press Enter:1)  On Windows XP, type %ALLUSERSPROFILE%\Application Data\Autodesk\ApplicationPlugIns. 2) On Windows 7 or Windows 8, type %ALLUSERSPROFILE%\Autodesk\ApplicationPlugIns.

4 Right-click in the file list and choose Paste.

The following steps explain how to deploy a bundle named DrawPlate.bundle on Mac OS:

1) In Finder, browse to the DrawPlate.bundle folder you created in the previous exercise.

2) Select the DrawPlate.bundle folder and secondary-click. Choose Copy「DrawPlate.bundle.」

3) In Finder, click Go Go To Folder, type /Applications/Autodesk/ApplicationAddIns , and click Go.

4) Secondary-click in the files list and choose Paste Item.

The following steps explain how to test DrawPlate.bundle:

1) In AutoCAD, create a new drawing.

2) At the Command prompt, type drawplate and press Enter.You should see the familiar Specify base point for plate or [Width\Height]: prompt. Before, you had to load the drawplate.lsp, utility.lsp, or myautoloader.lsp file to access the functionality.

3) Press Esc to end the drawplate function.

NOTE: If the drawplate function isn't available in the drawing, check the current value of the appautoload system variable. The appautoload system variable controls when a bundle should be loaded. The default value of the appautoload system variable is 14, which indicates a bundle should be loaded at startup, when a new drawing is opened, or when a new bundle has been added to one of the plug-in folders.