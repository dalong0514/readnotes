# 0401. Introducing the Excel Object Model

In This Chapter: 1) Introducing the concept of objects. 2) Finding out about the Excel object hierarchy. 3) Understanding object collections. 4) Referring to specific objects in your VBA code. 5) Accessing or changing an object's properties. 6) Performing actions with an object's methods.

Everyone is familiar with the word object. Well, folks, forget the definition you think you know. In the world of programming, the word object has a different meaning. You often see it used as part of the expression object-oriented programming, or OOP for short. OOP is based on the idea that software deals with distinct objects that have attributes (or properties) and can be manipulated. These objects are not material things. Rather, they exist in the form of bits and bytes.

In this chapter, you'll be introduced to the Excel object model, which is a hierarchy of objects contained in Excel. By the time you finish this chapter, you'll have a pretty good feel for what OOP is all about — and why you need to understand this concept to become a VBA programmer. After all, Excel programming really boils down to manipulating the objects that make up Excel. It's as simple as that.

## 4.1 Excel Is an Object?

You've used Excel for quite a while, but you probably never thought of it as an object. The more you work with VBA, the more you view Excel in those terms. You'll understand that Excel is an object and that it contains other objects. Those objects, in turn, contain still more objects. In other words, VBA programming involves working with an object hierarchy.

At the top of this hierarchy is the Application object — in this case, Excel itself (the mother of all objects).

## 4.2 Climbing Down the Object Hierarchy

The Application object contains other objects. The following are some of the more useful objects contained in the Excel application: 1) Addin. 2) Window. 3) Workbook. 4) WorksheetFunction.

Each object contained in the Application object can contain other objects. For example, the following are some objects that can be contained in a Workbook object: 1) Chart (which is a chart sheet). 2) Name. 3) VBProject. 4) Window. 5) Worksheet.

In turn, each of these objects can contain still other objects. Consider a Worksheet object, which is contained in a Workbook object, which is contained in the Application object. Some of the objects that can be contained in a Worksheet object are: 1) Comment. 2) Hyperlink. 3) Name. 4) PageSetup. 5) PivotTable. 6) Range.

Put another way, if you want to do something with a range on a particular worksheet, you may find it helpful to visualize that range in the following manner:

Range => contained in Worksheet => contained in Workbook => contained in Excel

Is this beginning to make sense?

When you start digging around, you'll find that Excel has more objects than you can shake a stick at. Even power users can get overwhelmed. The good news is that you'll never have to actually deal with most of these objects. When you're working on a problem, you can just focus on a few relevant objects — which you can often discover by recording a macro.

## 4.3 Wrapping Your Mind around Collections

Collections are another key concept in VBA programming. A collection is a group of objects of the same type. And to add to the confusion, a collection is itself an object. Here are a few examples of commonly used collections:

1 Workbooks: A collection of all currently open Workbook objects.

2 Worksheets: A collection of all Worksheet objects contained in a particular Workbook object.

3 Charts: A collection of all Chart objects (chart sheets) contained in a particular Workbook object.

4 Sheets: A collection of all sheets (regardless of their type) contained in a particular Workbook object.

1-2『 Sheets 和 Worksheets 是 2 个对象集合，印象中 Sheets 的概念更大，Sheet 包含 Worksheet 对象。做一张任意卡片。（2021-04-22）』—— 已完成

You may notice that collection names are all plural, which makes sense.

「What are collections for?」you may rightfully ask. Well, for example, they're very useful when you want to work with not just one worksheet, but with a couple of them or all of them. As you'll see, your VBA code can loop through all members of a collection and do something to each one.

## 4.4 Referring to Objects

Referring to an object is important because you must identify the object that you want to work with. After all, VBA can't read your mind — yet.

You can work with an entire collection of objects in one fell swoop. More often, however, you need to work with a specific object in a collection (such as a particular worksheet in a workbook). To reference a single object from a collection, you put the object's name or index number in parentheses after the name of the collection, like this:

```c
Worksheets("Sheet1")
```

Notice that the sheet's name is in quotation marks. If you omit the quotation marks, Excel won't be able to identify the object (and will assume that it's a variable name). If you want to work with the first worksheet in the collection, you can also use the following reference:

```c
Worksheets(1)
```

In this case, the number is not in quotation marks. Bottom line? If you refer to an object by using its name, use quotation marks. If you refer to an object by using its index number, use a plain number without quotation marks. What about chart sheets? A chart sheet contains a single chart. It has a sheet tab, but it's not a worksheet. Well, as it turns out, the object model has a collection called Charts. This collection contains all the chart sheet objects in a workbook (and does not include charts embedded in a worksheet). And just to keep things logical, there's another collection called Sheets. The Sheets collection contains all sheets (worksheets and chart sheets) in a workbook. The Sheets collection is handy if you want to work with all sheets in a workbook and don't care if they are worksheets or chart sheets.

So, a single worksheet named Sheet1 is a member of two collections: the Worksheets collection and the Sheets collection. You can refer to it in either of two ways:

```c
Worksheets("Sheet1")
Sheets("Sheet1")
```

### 4.4.1 Navigating through the hierarchy

If you want to work with Excel objects, they are all under the Application object. So start by typing Application.

Every other object in Excel's object model is under the Application object. You get to these objects by moving down the hierarchy and connecting each object on your way with the dot (`.`) operator. To get to the Workbook object named Book1.xlsx, start with the Application object and navigate down to the Workbooks collection object:

```c
Application.Workbooks("Book1.xlsx")
```

To navigate to a specific worksheet, add a dot operator and access the Worksheets collection object:

```c
Application.Workbooks("Book1.xlsx").Worksheets(1)
```

Not far enough yet? If you really want to get the value from cell A1 on the first Worksheet of the Workbook named Book1.xlsx, you need to navigate one more level to the Range object:

```c
Application.Workbooks("Book1.xlsx").Worksheets(1).Range("A1").Value
```

When you refer to a Range object in this way, it's called a fully qualified reference. You've told Excel exactly which range you want, on which worksheet and in which workbook, and have left nothing to the imagination. Imagination is good in people but not so good in computer programs.

By the way, workbook names also have a dot to separate the filename from the extension (for example, Book1.xlsx). That's just a coincidence. The dot in a filename has nothing at all to do with the dot operator referred to a few paragraphs ago.

### 4.4.2 Simplifying object references

If you were required to fully qualify every object reference you make, your code would get quite long, and it might be more difficult to read. Fortunately, Excel provides some shortcuts that can improve the readability (and save you some typing). For starters, the Application object is always assumed. There are only a few cases when it makes sense to type it. Omitting the Application object reference shortens the example from the previous section to

```c
Workbooks("Book1.xlsx").Worksheets(1).Range("A1").Value
```

That’s a pretty good improvement. But wait, there’s more. If you’re sure that Book1. xlsx is the active workbook, you can omit that reference, too. Now you’re down to

```c
Worksheets(1).Range("A1").Value
```

Now you’re getting somewhere. Have you guessed the next shortcut? That’s right. If you know the first worksheet is the currently active worksheet, Excel assumes that reference and allows you to just type

```c
Range("A1").Value
```

Contrary to what some people may think, Excel does not have a Cell object. A cell is simply a Range object that consists of just one element.

2『 Excel 里没有 cell 对象，做一张数据信息卡片。（2021-04-22）』—— 已完成

The shortcuts described here are great, but they can also be dangerous. What if you only think Book1.xlsx is the active workbook? You could get an error, or worse, you could get the wrong value and not even realize it’s wrong. For that reason, it’s often best to fully qualify your object references.

Chapter 14 discusses the With-End With structure, which helps you fully qualify your references but also helps to make the code more readable and cuts down on the typing. The best of both worlds!

## 4.5 Diving into Object Properties and Methods

Although knowing how to refer to objects is important, you can’t do anything useful by simply referring to an object (as in the examples in the preceding sections). To accomplish anything meaningful, you must do one of two things:

Read or modify an object’s properties.

Specify a method of action to be used with an object.

ANOTHER SLANT ON MCPROPERTIES, AND MCOBJECTS, MCMETHODS

Here’s an analogy, comparing Excel to a fast-food chain, that may help you understand the relationships among objects, properties, and methods in VBA.

The basic unit of Excel is a Workbook object. In a fast-food chain, the basic unit is an individual restaurant. With Excel, you can add a workbook and close a workbook, and all the open workbooks are known as Workbooks (a collection of Workbook objects). Similarly, the management of a fast-food chain can add a restaurant and close a restaurant, and all the restaurants in the chain can be viewed as the Restaurants collection (a collection of Restaurant objects).

An Excel workbook is an object, but it also contains other objects such as worksheets, chart sheets, VBA modules, and so on. Furthermore, each object in a workbook can contain its own objects. For example, a Worksheet object can contain Range objects, PivotTable objects, Shape objects, and so on.

Continuing with the analogy, a fast-food restaurant (like a workbook) contains objects such as the Kitchen, DiningArea, and Tables (a collection). Furthermore, management can add or remove objects from the Restaurant object. For example, management may add more tables to the Tables collection. Each of these objects can contain other objects. For example, the Kitchen object has a Stove object, VentilationFan object, Chef object, Sink object, and so on.

So far, so good. This analogy seems to work.

Excel’s objects have properties. For example, a Range object has properties such as Value and Name, and a Shape object has properties such as Width, Height, and so on. Not surprisingly, objects in a fast-food restaurant also have properties. The Stove object, for example, has properties such as Temperature and NumberofBurners. The VentilationFan has its own set of properties (TurnedOn, RPM, and so on).

Besides properties, Excel’s objects also have methods, which perform an operation on an object. For example, the ClearContents method erases the contents of a Range object. An object in a fast-food restaurant also has methods. You can easily envision a ChangeThermostat method for a Stove object or a SwitchOn method for a VentilationFan object.

In Excel, methods sometimes change an object’s properties. The ClearContents method for a Range changes the Range’s Value property. Similarly, the ChangeThermostat method on a Stove object affects its Temperature property. With VBA, you can write procedures to manipulate Excel’s objects. In a fast-food restaurant, the management can give orders to manipulate the objects in the restaurants (“Turn the stove on and switch the ventilation fan to high”).

The next time you visit your favorite fast-food joint, just say, “Use the Grill method on a Burger object with the Onion property set to False.”

### 4.5.1 Object properties

Every object has properties. You can think of properties as attributes that describe the object. An object’s properties determine how it looks, how it behaves, and even whether it’s visible. Using VBA, you can do two things with an object’s properties: 1) Examine the current setting for a property. 2) Change the property’s setting.

For example, a single-cell Range object has a property called Value. The Value property stores the value contained in the cell. You can write VBA code to display the Value property, or you may write VBA code to set the Value property to a specific value. The following macro uses the VBA built-in MsgBox function to bring up a box that displays the value in cell A1 on Sheet1 of the active workbook (see Figure 4-1):

```c
Sub ShowValue() 
  Contents = Worksheets("Sheet1").Range("A1").Value 
  MsgBox Contents 
End Sub
```

FIGURE 4-1: This message box displays a Range object’s Value property.

By the way, MsgBox is a very useful function. You can use it to display results while Excel executes your VBA code. You find out more about this function in Chapter 15, so be patient (or just flip ahead and read all about it).

The code in the preceding example displays the current setting of a cell’s Value property. What if you want to change the setting for that property? The following macro changes the value in cell A1 by changing the cell’s Value property:

```c
Sub ChangeValue()
  Worksheets("Sheet1").Range("A1").Value = 994.92
End Sub
```

After Excel executes this procedure, cell A1 on Sheet1 of the active workbook contains the value 994.92. If the active workbook doesn’t have a sheet named Sheet1, the result of executing that macro is an error message. VBA just follows instructions, and it can’t work with a sheet that doesn’t exist.

Each object has its own set of properties, although some properties are common to many objects. For example, many (but not all) objects have a Visible property. Most objects also have a Name property.

Some object properties are read-only properties, which means that your code can get the property’s value, but it can’t change it. For example, the Application object has a property called Version that returns the version number of the Excel that’s running. You can’t change the Version property index; it’s read-only.

As mentioned earlier in this chapter, a collection is also an object. This means that a collection also has properties. For example, you can determine how many workbooks are open by accessing the Count property of the Workbooks collection. The following VBA procedure displays a message box that tells you how many workbooks are open:

```c
Sub CountBooks()
  MsgBox Workbooks.Count
End Sub
```

### 4.5.2 Object methods

In addition to properties, objects have methods. A method is an action you perform with an object. A method can change an object’s properties or make the object do something.

This simple example uses the ClearContents method on a Range object to erase the contents of 12 cells on the active sheet:

```c
Sub ClearRange()
  Range("A1:A12").ClearContents
End Sub
```

Some methods take one or more arguments. An argument is a value that further specifies the action to perform. You place the arguments for a method after the method, separated by a space. Multiple arguments are separated by a comma.

The following example activates Sheet1 (in the active workbook) and then copies the contents of cell A1 to cell B1 by using the Range object’s Copy method. In this example, the Copy method has one argument, which is the destination range for the copy operation:

```c
Sub CopyOne() 
  Worksheets("Sheet1").Activate Range("A1").Copy Range("B1") 
End Sub
```

Notice that the worksheet reference is omitted when referring to the Range objects. You can do this safely due to the statement to activate Sheet1 (using the Activate method).

Another way to specify an argument for a method is to use the official name of the argument followed by a colon and an equal sign. Using named arguments is optional, but doing so can often make your code easier to understand. The second statement in the CopyOne procedure could be written like this:

```c
Range("A1").Copy Destination:=Range("B1")
```

In Figure 4-2, notice the little prompt as the statement is being typed. That prompt shows the official name of the argument.

FIGURE 4-2: The VBE displays a list of arguments while you type.

Because a collection is also an object, collections have methods. The following macro uses the Add method for the Workbooks collection:

```c
Sub AddAWorkbook()
  Workbooks.Add
End Sub
```

As you may expect, this statement creates a new workbook. In other words, it adds a new workbook to the Workbooks collection. After you execute this macro, a fresh workbook is the active workbook.

### 4.5.3 Object events

This section briefly touches on one more topic that you need to know about: events. Objects respond to various events that occur. For example, when you’re working in Excel and you activate a different workbook, a Workbook Activate event occurs. You could, for example, have a VBA macro that is designed to execute whenever an Activate event occurs for a particular Workbook object.

Excel supports many events, but not all objects can respond to all events. And some objects don’t respond to any events. The only events you can use are those made available by the programmers of Microsoft Excel. The concept of an event becomes clear in Chapter 11 and also in Part 4.

## 4.6 Finding Out More

Consider yourself initiated into the wonderful world of objects, properties, methods, and events. You find out more about these concepts in the chapters that follow. If you just can’t get enough, you may also be interested in three other excellent tools:

VBA’s Help system The Object Browser Auto List Members

### 4.6.1 Using VBA’s Help system

The VBA Help system describes every object, property, and method available to you, and also provides sample code. This is an excellent resource for finding out about VBA, and it’s more comprehensive than any book on the market. But it’s also very boring to read.

If you’re using Excel 2013 or later, you must be connected to the Internet to use the VBA Help system (previous versions don’t have this requirement). You can, however, download the VBA Help system from Microsoft’s website. Do a web search for download excel vba documentation, and you’ll find it.

If you’re working in a VBA module and want information about a particular object, method, or property, move the cursor to the word you’re interested in and press F1. In a few seconds, you see the appropriate Help topic displayed in your web browser, complete with cross-references and perhaps even an example or two.

Figure 4-3 shows part of a screen from the VBA Help system — in this case, for a Worksheet object.

FIGURE 4-3: An example from VBA’s Help system.

### 4.6.2 Using the Object Browser

The VBE includes another tool known as the Object Browser. As the name implies, this tool lets you browse through the objects available to you. To access the Object Browser, press F2 when the VBE is active (or choose View ➪ Object Browser). You see a window like the one shown in Figure 4-4.

The drop-down list at the top contains a list of all currently available object libraries. Figure 4-4 shows All Libraries. If you want to browse through Excel’s objects, select Excel from the drop-down list.

FIGURE 4-4: Browsing for objects with the Object Browser.

The second drop-down list is where you enter a search string. For example, if you want to look at all Excel objects that deal with comments, type comment in the second field and click the Search button. (It has a pair of binoculars on it.) The Search Results window displays everything in the object library that contains the text comment. If you see something that looks like it may be of interest, select it and press F1 for more information online.

### 4.6.3 Automatically listing properties and methods

Chapter 3 introduces you to a handy feature called Auto List Members. This feature provides a list of properties and methods as you type. Figure 4-5 shows an example for the Workbooks collection.

FIGURE 4-5: The Auto List Members feature helps you identify properties and methods for an object.

After typing the dot after workbooks, the VBE volunteers to help by displaying a list of properties and methods for that collection. Typing the letter (like the letter c), narrows the list to items that begin with that letter. With each letter you type, the VBE further narrows the list of choices. Highlight the item you need, press Tab, and voilà! You’ve eliminated some typing — and also ensured that the property or method was spelled correctly.