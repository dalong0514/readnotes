for cells. Why do you need to know so much about Range objects? Because

much of the programming work you do in Excel focuses on Range objects.

A Quick Review

A  Range object represents a range contained in a Worksheet object. Range objects, like all other objects, have properties (which you can examine and sometimes

change) and methods (which perform actions on the object).

A Range object can be as small as a single cell (for example, B4) or as large as

every one of the 17,179,869,184 cells in a worksheet (A1:XFD1048576).

When you refer to a Range object, the address is always surrounded by double

quotes, like this:

Range("A1:C5")

CHAPTER 8  Working with Range Objects    115

If the range consists of one cell, you still need the quotes:

Range("K9")

If the range happens to have a name (created with Formulas

➪ Defined

Names ➪ Define Name ), you can refer to the range by its name (which is also in

quotes):

Range("PriceList")

Unless you tell Excel otherwise by qualifying the range reference, it assumes that

you’re referring to a range on the active worksheet. If anything other than a work-

sheet is active (such as a chart sheet), the range reference fails, and your macro

displays an error message and grinds to a screeching halt.

As shown in the following example, you can refer to a range outside the active

sheet by qualifying the range reference with a worksheet name from the active

workbook:

Worksheets("Sheet1").Range("A1:C5")

If you need to refer to a range in a different workbook (that is, any workbook other than the active workbook), you can use a statement like this:

Workbooks("Budget.xlsx").Worksheets("Sheet1").Range("A1:C5") A Range object can consist of one or more entire rows or columns. You can refer to

an entire row (in this case, row 3) by using syntax like this:

Range("3:3")

You can refer to an entire column (the fourth column in this example) like this:

Range("D:D")

In Excel, you select noncontiguous ranges by holding down Ctrl while selecting

various ranges with your mouse. Figure 8-1 shows a noncontiguous range selec-

tion. You shouldn’t be surprised that VBA also allows you to work with noncon-

tiguous ranges. The following expression refers to a two-area noncontiguous

range. Notice that a comma separates the two areas.

Range("A1:B8,D9:G16")

116    PART 3  Programming Concepts

FIGURE 8-1:

A noncontiguous

range selection.

Be aware that some methods and properties cause havoc with noncontiguous

ranges. You may have to process each area separately by using a loop.

Other Ways to Refer to a Range

The more you work with VBA, the more you realize that it’s a fairly well-conceived

language and is usually quite logical (despite what you may be thinking right

now). Often, VBA provides multiple ways to perform an action. You can choose the

most appropriate solution for your problem. This section discusses some of the

other ways to refer to a range.

This chapter barely scratches the surface for the Range object’s properties and

methods. As you work with VBA, you’ll probably need to access other properties

and methods. The Help system is the best place to find out about them, but it’s also a good idea to record your actions and examine the code Excel generates. You’re

probably getting tired of hearing that advice by now, but it really is good advice.

The Cells property

Rather than use the VBA Range keyword, you can refer to a range via the Cells

property.

Although Cells may seem like an object (or a collection), it’s really not. Rather,

Cells is a property that VBA evaluates. VBA then returns an object (more specifi-

cally, a Range object). If this seems strange, don’t worry. Even Microsoft appears

to be confused about this issue. In some earlier versions of Excel, the Cells prop-

erty was known as the Cells method. Regardless of what it is, just understand that

Cells is a handy way to refer to a range.

CHAPTER 8  Working with Range Objects    117

The Cells property takes two arguments: a row number and a column number.

Both of these arguments are numbers, even though you usually refer to columns

by using letters. For example, the following expression refers to cell C2 on Sheet2: Worksheets("Sheet2").Cells(2, 3)

You can also use the Cells property to refer to a multicell range. The following

example demonstrates the syntax you use:

Range(Cells(1, 1), Cells(10, 8))

This expression refers to an 80-cell range that extends from cell A1 (row 1, column

1) to cell H10 (row 10, column 8).

The following statements both produce the same result; they enter a value of 99

into a 10-by-8 range of cells. More specifically, these statements set the Value

property of the Range object:

Range("A1:H10").Value = 99

Range(Cells(1, 1), Cells(10, 8)).Value = 99

The advantage of using the Cells property to refer to ranges becomes apparent

when you use variables rather than actual numbers as the Cells arguments. And

things really start to click when you understand looping, which is in Chapter 10.

The Offset property

The Offset property provides another handy means for referring to ranges. This

property, which operates on a Range object and returns another Range object,

allows you to refer to a cell that is a particular number of rows and columns away

from another cell.

Like the Cells property, the Offset property takes two arguments. The first argu-

ment represents the number of rows to offset; the second represents the number

of columns to offset.

The following expression refers to a cell one row below cell A1 and two columns to

the right of cell A1. In other words, this refers to the cell commonly known as C2:

Range("A1").Offset(1, 2)

118    PART 3  Programming Concepts

The Offset property can also use negative arguments. A  negative row offset refers to a row above the range. A negative column offset refers to a column to the left of the range. The following example refers to cell A1:

Range("C2").Offset(-1, -2)

And as you may expect, you can use 0 as one or both of the arguments for Offset.

The following expression refers to cell A1:

Range("A1").Offset(0, 0)

Here’s a statement that inserts the time of day into the cell to the right of the

active cell:

ActiveCell.Offset(0,1) = Time

When you record a macro in relative mode, Excel uses the Offset property quite a

bit. Refer to Chapter 6 for an example.

The Offset property is most useful when you use variables rather than actual val-

ues for the arguments. Chapter 10 includes examples that demonstrate this.

Some Useful Range Object Properties

A Range object has dozens of properties. You can write VBA programs nonstop for

the next 12 months and never use them all. This section briefly describes some of

the most commonly used Range properties. For complete details, consult the Help

system in the VBE.

Some Range properties are  read-only properties, which means that your code can look at their values but can’t change them ("Look, but don’t touch"). For example, every Range object has an Address property, which holds the range’s address. You

can access this read-only property, but you can’t change it — which makes per-

fect sense when you think about it.

By the way, the examples that follow are typically statements rather than com-

plete procedures. If you’d like to try any of these (and you should), create a Sub

procedure to do so. Also, many of these statements work properly only if a work-

sheet is the active sheet.

CHAPTER 8  Working with Range Objects    119

The Value property

The Value property represents the value contained in a cell. It’s a read-write

property, so your VBA code can either read or change the value.

The following statement displays a message box that shows the value in cell A1 on

Sheet1:

MsgBox Worksheets("Sheet1").Range("A1").Value

It stands to reason that you can read the Value property only for a single-cell

Range object. For example, the following statement generates an error:

MsgBox Worksheets("Sheet1").Range("A1:C3").Value

You can, however, change the Value property for a range of any size. The following

statement enters the number 123 into each cell in a range:

Worksheets("Sheet1").Range("A1:C3").Value = 123

Value is the default property for a Range object. In other words, if you omit a

property for a Range, Excel uses its Value property. The following statements both

enter a value of 75 into cell A1 of the active worksheet:

Range("A1").Value = 75

Range("A1") = 75

ASSIGNING THE VALUES IN A MULTICELL

RANGE TO A VARIABLE

Even though you can read the Value property only for a single-cell Range object, you can assign the values in a multicell range to a variable, as long as the variable is a variant.

That’s because a variant can act like an array. Here’s an example:

Dim x As Variant

x = Range("A1:C3").Value

Then you can treat the x variable as though it were an array. This statement, for example, returns the value in cell B1:

MsgBox x(1, 2)

120    PART 3  Programming Concepts

The Text property

The Text property returns a string that represents the text as it’s displayed in

a cell — the formatted value. The Text property is read-only. Suppose that cell A1

contains the value 12.3 and is formatted to display two decimals and a dollar sign

($12.30). The following statement displays a message box containing $12.30:

MsgBox Worksheets("Sheet1").Range("A1").Text

But the next statement displays a message box containing 12.3:

MsgBox Worksheets("Sheet1").Range("A1").Value

If the cell contains a formula, the Text property returns the result of the formula.

If a cell contains text, the Text property and the Value property always return the

same thing, because text (unlike a number) can’t be formatted to display

differently.

The Count property

The Count property returns the number of cells in a range. It counts all cells, not

just the nonblank cells. Count is a read-only property, just as you would expect.

The following statement accesses a range’s Count property and displays the result

(9) in a message box:

MsgBox Range("A1:C3").Count

The Column and Row properties

The Column property returns the column number of a single-cell range. Its side-

kick, the Row property, returns the row number of a single-cell range. Both are

read-only properties. For example, the following statement displays 6 because

cell F3 is in the sixth column:

MsgBox Sheets("Sheet1").Range("F3").Column

The next expression displays 3 because cell F3 is in the third row:

MsgBox Sheets("Sheet1").Range("F3").Row

If the Range object consists of more than one cell, the Column property returns

the column number of the first column in the range, and the Row property returns

the row number of the first row in the range.

CHAPTER 8  Working with Range Objects    121

Don’t confuse the Column and Row properties with the Columns and Rows prop-

erties (discussed earlier in this chapter). The Column and Row properties return a

single value. The Columns and Rows properties, on the other hand, return a Range

object. What a difference an「s」makes.

The Address property

Address, a read-only property, displays the cell address for a Range object as an

absolute reference (a dollar sign before the column letter and before the row num-

ber). The following statement displays the message box shown in Figure 8-2:

MsgBox Range(Cells(1, 1), Cells(5, 5)).Address

FIGURE 8-2:

This message box

displays the

Address property

of a 5-by-5 range.

The HasFormula property

The HasFormula property (which is read-only) returns True if the single-cell

range contains a formula. It returns False if the cell contains something other

than a formula (or is empty). If the range consists of more than one cell, VBA

returns True only if all cells in the range contain a formula or False if all cells in the range don’t have a formula. The property returns Null if the range contains a

mixture of formulas and nonformulas. Null is kind of a no-man’s land: The

answer is neither True nor False, and any cell in the range may or may not have a

formula.

You need to be careful when you work with properties that can return Null. More

specifically, the only data type that can deal with Null is Variant.

122    PART 3  Programming Concepts

For example, assume that cell A1 contains a value and cell A2 contains a formula.

The following statements generate an error because the range doesn’t consist of

all formulas or all nonformulas:

Dim FormulaTest As Boolean

FormulaTest = Range("A1:A2").HasFormula

The Boolean data type can handle only True or False. Null causes Excel to com-

plain and display an error message. To fix this type of situation, the best thing to do is make sure that the FormulaTest variable is declared as a Variant rather than

as a Boolean. The following example uses VBA’s handy TypeName function (along

with an If-Then-Else construct) to determine the data type of the FormulaTest

variable. If the range has a mixture of formulas and nonformulas, the message

box displays  Mixed!  Otherwise, it displays  True or  False .

Sub CheckForFormulas()

Dim FormulaTest As Variant

FormulaTest = Range("A1:A2").HasFormula

If TypeName(FormulaTest) = "Null" Then

MsgBox "Mixed!"

Else

MsgBox FormulaTest

End If

End Sub

See Chapter 10 for more about using the If-Then-Else construct.

The Font property

As noted earlier in this chapter (see「The Cells property」), a property can return

an object. The Font property of a Range object is another example of that concept

at work. The Font property returns a Font object.

A Font object, as you may expect, has many accessible properties. To change some

aspect of a range’s font, you must first access the range’s Font object and then

manipulate the properties of that object. This may be confusing, but perhaps this

example will help.

The following statement uses the Font property of the Range object to return a

Font object. Then the Bold property of the Font object is set to True. In plain Eng-

lish, this statement makes the cell display in boldface:

Range("A1").Font.Bold = True

CHAPTER 8  Working with Range Objects    123

Truth is, you don’t really need to know that you’re working with a special Font object that’s contained in a Range object. As long as you use the proper syntax, it

works just fine. Often, recording your actions with the macro recorder tells you

everything you need to know about the proper syntax.

See Chapter 6 for more information about recording macros.

The Interior property

Here’s yet another example of a property that returns an object. A Range object’s

Interior property returns an Interior object (strange name, but that’s what it’s

called). This type of object referencing works the same way as the Font property

(described in the preceding section).

For example, the following statement changes the Color property of the Interior

object contained in the Range object:

Range("A1").Interior.Color = 8421504

In other words, this statement changes the cell’s background to middle gray. What’s

that? You didn’t know that 8421504 is middle gray? For some insights into Excel’s

wonderful world of color, see the nearby sidebar「A quick-and-dirty color primer.」

A QUICK-AND-DIRTY COLOR PRIMER

Before Excel 2007, Microsoft tried to convince us that 56 colors were good enough for a spreadsheet. But things have changed, and we can use more than 16 million colors in a workbook — 16,777,216 colors, to be exact.

Many objects have a Color property, and that property accepts color values that range from 0 to 16777215. Nobody can remember that many color values, so (fortunately)

there’s an easier way to specify colors: VBA’s RGB function. This function takes advantage of the fact that any of these 16 million colors can be represented by various levels of red, green, and blue. The three arguments in the RGB function correspond to the color’s red, green, and blue components, and each of these arguments can range from 0 to 255.

Note that 256 x 256 x 256 = 16,777,216 — which happens to be the number of colors.

Don’t you just love it when the math works out?

Here’s a statement that changes a cell’s background color to a random color:

Range("A1").Interior.Color = Int(16777216 * Rnd)

124    PART 3  Programming Concepts

Following are a few examples that use the RGB function to change a cell’s background color:

Range("A1").Interior.Color = RGB(0, 0, 0) 'black

Range("A1").Interior.Color = RGB(255, 0, 0) ' pure red

Range("A1").Interior.Color = RGB(0, 0, 255) ' pure blue

Range("A1").Interior.Color = RGB(198, 212, 60) ' ugly green

Range("A1").Interior.Color = RGB(128, 128, 128) ' middle gray

What’s the exact value of RGB(128, 128, 128)? This statement tells you that it’s 8421504: MsgBox RGB(128, 128, 128)

If you need to use standard colors, you may prefer to use one of the built-in color

constants: vbBlack, vbRed, vbGreen, vbYellow, vbBlue, vbMagenta, vbCyan, or vbWhite.

For example, the following statement makes cell A1 yellow:

Range("A1").Interior.Color = vbYellow

Excel 2007 also introduced  theme colors.  These are the colors that appear when you use color control such as the Fill Color control in the Font group of the Home tab. Try recording a macro while you change colors, and you’ll get something like this:

Range("A1").Interior.ThemeColor = xlThemeColorAccent4

Range("A1").Interior.TintAndShade = 0.399975585192419

Yep, two more color-related properties to deal with. Here, you have a theme color (the basic color, specified as a built-in constant), plus a「tint and shade」value that represents how dark or light the color is. TintAndShade values range from –1.0 to +1.0. Positive values of the TintAndShade property make the color lighter, and negative values

make the color darker. When you set a color by using the ThemeColor property, the

color changes if you apply a different document theme (by choosing Page Layout ➪

Themes ➪ Themes ).

The Formula property

The Formula property represents the formula in a cell. This is a read-write prop-

erty, so you can access it to either view the formula in a cell or insert a formula into a cell. For example, the following statement enters a SUM formula into cell A13:

Range("A13").Formula = "=SUM(A1:A12)"

Notice that the formula is a text string and is enclosed in quotation marks. Also

notice that the formula begins with an equal sign, as all formulas do.

CHAPTER 8  Working with Range Objects    125

If the formula itself contains quotation marks, things get a bit tricky. Say that you want to insert this formula by using VBA:

=SUM(A1:A12)&" Stores"

This formula displays a value followed by the word  Stores . To make this formula acceptable, you need to replace every quotation mark in the formula with two

quotation marks. Otherwise, VBA gets confused and claims that there’s a syntax

error (because there is!). So here’s a statement that enters a formula that contains quotes:

Range("A13").Formula = "=SUM(A1:A12)&"" Stores"""

By the way, you can access a cell’s Formula property even if the cell doesn’t have

a formula. If a cell has no formula, the Formula property returns the same as its

Value property.

If you need to know whether a cell has a formula, use the HasFormula property

(discussed earlier in this chapter).

Be aware that VBA「speaks」U.S. English. This means that to put a formula in a

cell, you must use the U.S. syntax. If you use a non-English version of Excel, read

up on the FormulaLocal property in the Help system.

The NumberFormat property

The NumberFormat property represents the number format (expressed as a text

string) of the Range object. This is a read-write property, so your VBA code can

either examine the number format or change it. The following statement changes

the number format of column A to a percentage with two decimal places:

Columns("A:A").NumberFormat = "0.00%"

Follow these steps to see a list of other number formats (better yet, turn on the

macro recorder while you do this):

1. Activate a worksheet.

2. Press Ctrl+1 to access the Format Cells dialog box.

3. Click the Number tab.

4. Select the Custom category to view and apply some additional number

format strings.

126    PART 3  Programming Concepts

Some Useful Range Object Methods

As you know, a VBA method performs an action. A Range object has dozens of

methods but, again, you won’t need most of these. In this section, you explore

some of the most commonly used Range object methods.

The Select method

Use the Select method to select a range of cells. The following statement selects a

range in the active worksheet:

Range("A1:C12").Select

Before selecting a range, it’s often a good idea to use one additional statement to

ensure that the correct worksheet is active. For example, if Sheet1 contains the

range you want to select, use the following statements to select the range:

Sheets("Sheet1").Activate

Range("A1:C12").Select

Contrary to what you may expect, the following statement generates an error if

Sheet1 is not already the active sheet. In other words, you must use two state-

ments rather than just one: one to activate the sheet and another to select the

range.

Sheets("Sheet1").Range("A1:C12").Select

If you use the GoTo method of the Application object to select a range, you can

forget about selecting the correct worksheet first. This statement activates Sheet1

and then selects the range:

Application.Goto Sheets("Sheet1").Range("A1:C12")

The GoTo method is the VBA equivalent of pressing F5 in Excel, which displays the

GoTo dialog box.

The Copy and Paste methods

You can perform copy and paste operations in VBA by using the Copy and Paste

methods. Note that two different objects come into play. The Copy method is applicable to the Range object, but the Paste method applies to the Worksheet

object. It actually makes sense: You copy a range and paste it to a worksheet.

CHAPTER 8  Working with Range Objects    127

This short macro (courtesy of the macro recorder) copies range A1:A12 and pastes it into the same worksheet, beginning at cell C1:

Sub CopyRange()

Range("A1:A12").Select

Selection.Copy

Range("C1").Select

ActiveSheet.Paste

End Sub

Notice that in the preceding example, the ActiveSheet object is used with the Paste

method. This is a special version of the Worksheet object that refers to the

currently active worksheet. Also notice that the macro selects the range before

copying it. However, you don’t have to select a range before doing something with

it. In fact, the following procedure accomplishes the same task as the preceding

example by using a single statement:

Sub CopyRange2()

Range("A1:A12").Copy Range("C1")

End Sub

This procedure takes advantage of the fact that the Copy method can use an argu-

ment that corresponds to the destination range for the copy operation. That’s

something that you can find out by checking with the Help system.

The Clear method

The Clear method deletes the contents of a range, plus all the cell formatting. For

example, if you want to zap everything in column D, the following statement does

the trick:

Columns("D:D").Clear

You should be aware of two related methods. The ClearContents method deletes

the contents of the range but leaves the formatting intact. The ClearFormats

method deletes the formatting in the range but not the cell contents.

The Delete method

Clearing a range differs from deleting a range. When you  delete a range, Excel shifts the remaining cells around to fill up the range you deleted.

128    PART 3  Programming Concepts

The following example uses the Delete method to delete row 6:

Rows("6:6").Delete

When you delete a range that’s not a complete row or column, Excel needs to

know how to shift the cells. (To see how this works, experiment with

Home ➪ Cells ➪ Delete ➪ Delete Cells in Excel.)

The following statement deletes a range and then fills the resulting gap by shift-

ing the other cells to the left:

Range("C6:C10").Delete xlToLeft

The Delete method uses an argument that indicates how Excel should shift the

remaining cells. In this case, the built-in constant (xlToLeft) is used for the

argument.

CHAPTER 8  Working with Range Objects    129

IN THIS CHAPTER

» Using functions to make your VBA

expressions more powerful

» Using the VBA built-in functions

» Using Excel worksheet functions in

your VBA code

» Writing custom functions

Chapter 9

Using VBA and

Worksheet Functions

