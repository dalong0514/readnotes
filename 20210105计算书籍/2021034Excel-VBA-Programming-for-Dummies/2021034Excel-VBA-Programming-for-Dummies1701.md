the dialog box contains. Your VBA code then makes use of these responses

to determine which actions to take. You have quite a few controls at your disposal,

and this chapter tells you about them.

If you worked through the hands-on example in Chapter 16, you already have some experience with UserForm controls. This chapter fills in some of the gaps.

Getting Started with Dialog Box Controls

In this section, you explore how to add controls to a UserForm, give them mean-

ingful names, and adjust some of their properties.

Before you can do any of these things, you must have a UserForm, which you get

by choosing Insert ➪ UserForm in the VBE. When you add a UserForm, make sure

that the correct project is selected in the Project window (if more than one project is available).

CHAPTER 17  Using UserForm Controls    275

Adding controls

Oddly enough, the VBE doesn't have menu commands that allow you to add con-

trols to a dialog box. You must use the floating Toolbox (described in Chapter 16)

to add controls. Normally, the Toolbox pops up automatically when you activate a

UserForm in the VBE. If it doesn't, you can display the Toolbox by choosing View ➪ Toolbox.

Follow along to add a control to the UserForm:

1. Click the Toolbox tool that corresponds to the control you want to add.

2. Click in the UserForm, and drag to size and position the control.

Alternatively, you can simply drag a control from the Toolbox to the UserForm

to create a control with the default dimensions. Figure 17-1 shows a UserForm

that contains a few controls: Two OptionButtons (inside a Frame), a ComboBox,

a CheckBox, a ScrollBar, and a CommandButton.

FIGURE 17-1:

A UserForm in

the VBE, with a

few controls

added.

A UserForm may contain vertical and horizontal grid lines, which help align the

controls you add. When you add or move a control, it  snaps to the grid. If you don't like this feature, you can turn off the grids by following these steps:

1. Choose Tools  ➪ Options in the VBE.

2. In the Options dialog box, select the General tab.

3. Set your desired options in the Form Grid Settings section.

Introducing control properties

Every control that you add to a UserForm has properties that determine how the

control looks and behaves. You can change a control's properties at the following

two times:

276    PART 4  Communicating with Your Users

» At design time — when you're designing the UserForm. You do so manually,

using the Properties window.

» At runtime — while your macro is running. You do so by writing VBA code.

Changes made at runtime are always temporary; they're made to the copy of

the dialog box you're showing, not to the actual UserForm object you designed.

When you add a control to a UserForm, you almost always need to make some

design-time adjustments to its properties. You make these changes in the Proper-

ties window. (To display the Properties window, press F4.) Figure 17-2 shows the

Properties window, which displays properties for the object selected in the

UserForm — which happens to be a CheckBox control.

FIGURE 17-2:

Use the

Properties

window to make

design-time

changes to a

control's

properties.

To change a control's properties at runtime, you must write VBA code. For exam-

ple, you may want to hide a particular control when the user clicks a check box. In

such a case, you write code to change the control's Visible property.

Each control has its own set of properties. All controls, however, have some com-

mon properties, such as Name, Width, and Height. Table 17-1 lists some of the

common properties available for many controls.

When you select a control, that control's properties appear in the Properties window. To change a property, just select it in the Properties window and make

the change. Some properties give you some help. For example, if you need to

change the TextAlign property, the Properties window displays a drop-down list

that contains all valid property values, as shown in Figure 17-3.

CHAPTER 17  Using UserForm Controls    277

TABLE 17-1

Common Control Properties

Property

What It Affects

Accelerator

The letter underlined in the control's caption. The user presses this key in conjunction with the Alt key to select the control.

AutoSize

If True, the control resizes itself automatically based on the text in its caption.

BackColor

The control's background color.

BackStyle

The background style (transparent or opaque).

Caption

The text that appears on the control.

Left and Top

Values that determine the control's position.

Name

The control's name. By default, a control's name is based on the control type. You can change the name to any valid name, but each control's name must be unique within

the dialog box.

Picture

A graphics image to display. The image can be from a graphics file, or you can select the Picture property and paste an image that you copied to the Clipboard.

Value

The control's value.

Visible

If False, the control is hidden.

Width and Height

Values that determine the control's width and height.

FIGURE 17-3:

Change some

properties by

selecting from

a drop-down

list of valid

property values.

278    PART 4  Communicating with Your Users

Dialog Box Controls: The Details

The following sections introduce each type of control you can use in custom dialog

boxes and discuss some of the most useful properties. Not every property for every

control is included because that would require a book that's about four times as

thick (and it would be a very boring book).

The Help system for controls and properties is thorough. To find complete details

for a particular property, select the property in the Properties window and press F1.

All the examples in this section are available on this book's website.

CheckBox control

A CheckBox control is useful for getting a binary choice: yes or no, true or false, on or off, and so on. Figure 17-4 shows some examples of CheckBox controls.

FIGURE 17-4:

CheckBox

Controls in a

UserForm.

Following are a CheckBox control's most useful properties:

» Accelerator: A character that lets the user change the value of the control by using the keyboard. For example, if the accelerator is A, pressing Alt+A

changes the value of the CheckBox control (from checked to unchecked, or

from unchecked to checked). In the example shown in Figure 17-4, numbers

are the accelerators (Alt+1, Alt+2, and so on).

» ControlSource: The address of a worksheet cell that's linked to the CheckBox.

The cell displays TRUE if the control is checked and FALSE if the control is not

checked. This is optional. Most of the time, a CheckBox is not linked to a cell.

» Value: If True, the CheckBox has a check mark. If False, the CheckBox doesn't have a check mark.

Don't confuse CheckBox controls with OptionButton controls. They look similar,

but they're used for different purposes.

CHAPTER 17  Using UserForm Controls    279

ComboBox control

A ComboBox control is similar to a ListBox control (described later in the「ListBox

control」section). A ComboBox, however, is a drop-down control. Another differ-

ence is that the user may be allowed to enter a value that doesn't appear in the list of items. Figure 17-5 shows two ComboBox controls. The control on the right (for

the year) is being used, so it has dropped down to display its list of options.

FIGURE 17-5:

ComboBox

Controls in a

UserForm.

Following are some useful ComboBox control properties:

» ControlSource: A cell that stores the value selected in the ComboBox.

» ListRows: The number of items to display when the list drops down.

» ListStyle: The appearance of the list items.

» RowSource: A range address that contains the list of items displayed in the ComboBox.

» Style: Determines whether the control acts like a drop-down list or a

ComboBox. A drop-down list doesn't allow the user to enter a new value.

» Value: The text of the item selected by the user and displayed in the

ComboBox.

If your list of items isn't in a worksheet, you can add items to a ComboBox control

by using the AddItem method. More information on this method is in Chapter 18.

CommandButton control

CommandButton is just a common clickable button. It is of no use unless you pro-

vide an event-handler procedure to execute when the button is clicked. Figure 17-6

shows a dialog box with nine CommandButtons. Two of these buttons feature clip-

art images, which are added by copying the clip art and then pasting it into the

Picture field in the Properties window.

280    PART 4  Communicating with Your Users

FIGURE 17-6:

CommandButton

controls.

When a CommandButton is clicked, it executes an event-handler procedure with

a name that consists of the CommandButton's name, an underscore, and the word

Click. For example, if a CommandButton is named MyButton, clicking it executes

the macro named MyButton_Click. This macro is stored in the Code window for

the UserForm.

Following are some useful CommandButton control properties:

» Cancel: If True, pressing Esc executes the macro attached to the button. Only one of the form's buttons can have this option set to True.

» Default: If True, pressing Enter executes the macro attached to the button.

Again: Just one button can have this option set to True.

Frame control

A Frame control encloses other controls. You use it either for aesthetic purposes or to logically group a set of controls. A frame is particularly useful when the dialog box contains more than one set of OptionButton controls (see「OptionButton

control,」later in this chapter).

The following list describes some useful Frame control properties:

» BorderStyle: The frame's appearance.

» Caption: The text displayed at the top of the frame. The caption can be an

empty string if you don't want the control to display a caption.

Image control

An Image control displays an image. You may want to use an Image control to

display your company's logo in a dialog box. Figure 17-7 shows a dialog box with

an Image control that displays a photo of a cute little kitten.

CHAPTER 17  Using UserForm Controls    281

FIGURE 17-7:

An Image control

displays a photo.

The following list describes the most useful Image control properties:

» Picture: The graphics image that is displayed.

» PictureSizeMode: How the picture is displayed if the control size doesn't

match the image size.

When you click the Picture property, you're prompted for a filename. However,

the graphics image (after it's retrieved) is stored in the workbook. That way, if you distribute your workbook to someone else, you don't have to include a copy of the

graphics file.

Rather than retrieve the image from a file, you can copy and paste. To search the

web for images, activate Excel and choose Insert ➪ Illustrations ➪ Online Pictures,

and search for an image to place in your worksheet. Then select the image, and

press Ctrl+C to copy it to the Clipboard. Then activate your UserForm, click the

Image control, and select the Picture property in the Properties box. Press Ctrl+V

to paste the copied image. Then you can delete the image from the worksheet.

Some graphics images are very large and can make your workbook size increase

dramatically. For best results, use an image that's as small as possible.

Label control

A Label control simply displays text in your dialog box. Figure 17-8 shows a few

Label controls. As you can see, you have a great deal of control of the formatting

of a Label control.

282    PART 4  Communicating with Your Users

FIGURE 17-8:

Label controls

can take on lots

of different looks.

ListBox control

The ListBox control presents a list of items from which the user can choose one or

more. Figure 17-9 shows a dialog box with two ListBox controls.

FIGURE 17-9:

ListBox controls.

ListBox controls are very flexible. For example, you can specify a worksheet range

that holds the ListBox items, and the range can consist of multiple columns. Or

you can fill the ListBox with items by using VBA code.

If a ListBox isn't tall enough to display all the items in the list, a scroll bar appears so the user can scroll down to see more items.

The following list is a description of the most useful ListBox control properties:

» ControlSource: A cell that stores the value selected in the ListBox.

» IntegralHeight: This is True if the ListBox height adjusts automatically to display full lines of text when the list is scrolled vertically. If False, the ListBox may display partial lines of text when it is scrolled vertically. Note that when

CHAPTER 17  Using UserForm Controls    283

this property is True, the actual height of your ListBox may be slightly different,

when your UserForm is shown, from what you had set it originally. In other

words, the height may adjust to ensure that the last entry is entirely visible.

» ListStyle: The appearance of the list items.

» MultiSelect: Determines whether the user can select multiple items from

the list.

» RowSource: A range address that contains the list of items displayed in

the ListBox.

» Value: The text of the selected item in the ListBox.

If the ListBox has its MultiSelect property set to 1 or 2, the user can select multiple items in the ListBox. In such a case, you can't specify a ControlSource; you need

to write a macro that determines which items are selected. Chapter 18 demon-

strates how to do so.

MultiPage control

A MultiPage control allows you to create tabbed dialog boxes, like the Format Cells

dialog box (the one that appears when you press Ctrl+1 in Excel). Figure 17-10

shows an example of a custom dialog box that uses a MultiPage control. This

particular control has three pages, or tabs.

FIGURE 17-10:

Use a MultiPage

control to create

a tabbed

dialog box.

Descriptions of the most useful MultiPage control properties follow:

» Style: Determines the appearance of the control. The tabs can appear

normally (on the top), on the left, as buttons, or hidden (no tabs — your VBA

code determines which page is displayed).

284    PART 4  Communicating with Your Users

» Value: Determines which page or tab is displayed. A Value of 0 displays the first page, a Value of 1 displays the second page, and so on.

By default, a MultiPage control has two pages. To add pages, right-click a tab and

select New Page from the shortcut menu.

OptionButton control

OptionButtons are useful when the user needs to choose from a small number of

mutually exclusive items. OptionButtons are always used in groups of at least two.

Figure 17-11 shows two sets of OptionButtons, and each set is contained in a frame.

FIGURE 17-11:

Two sets of

OptionButton

controls, each

contained in a

Frame control.

The following is a description of the most useful OptionButton control properties:

» Accelerator: A letter that lets the user select the option by using the

keyboard. For example, if the accelerator for an option button is C,

pressing Alt+C selects the control.

» GroupName: A name that identifies an option button as being associated

with other option buttons with the same GroupName property.

» ControlSource: The worksheet cell that's linked to the option button.

The cell displays TRUE if the control is selected or FALSE if the control is

not selected.

» Value: If True, the OptionButton is selected. If False, the OptionButton is not selected.

If your dialog box contains more than one set of OptionButtons, you  must change the GroupName property for all OptionButtons in a particular set. Otherwise, all

OptionButtons become part of the same set. Alternatively, you can enclose each

set of OptionButtons in a Frame control, which automatically groups the Option-

Buttons in the frame.

CHAPTER 17  Using UserForm Controls    285

RefEdit control

In some cases, you may need the user to select a range of cells in order to pass a

valid range to your VBA code. Your procedures can then use the selected range for

some specific task. The RefEdit control is used when you need to let the user select a range in a worksheet. Figure 17-12 shows a UserForm with two RefEdit controls.

Its Value property holds the address of the selected range (as a text string).

FIGURE 17-12:

Two RefEdit

controls.

The RefEdit control sometimes causes trouble in more complex UserForms. For

best results, don't place a RefEdit control inside a Frame or MultiPage control.

ScrollBar control

When you add a ScrollBar control, you can make it horizontal or vertical. The ScrollBar control is similar to a SpinButton control (described later). The difference is that the user can drag the ScrollBar's button to change the control's value

in larger increments. Another difference is that when you click the up button on a

vertical ScrollBar, the value decreases — which is a bit counterintuitive. So a ScrollBar is not always a good substitute for a SpinButton.

Figure 17-13 shows a ScrollBar control with a horizontal orientation. Its Value property is displayed in a Label control placed below the ScrollBar control.

FIGURE 17-13:

A ScrollBar

control with a

Label control

below it.

286    PART 4  Communicating with Your Users

Following are the most useful properties of a ScrollBar control:

» Value: The control's current value.

» Min: The control's minimum value.

» Max: The control's maximum value.

» ControlSource: The worksheet cell that displays the control's value.

» SmallChange: The amount that the control's value is changed by a click.

» LargeChange: The amount that the control's value is changed by clicking

either side of the button.

The ScrollBar control is most useful for specifying a value that extends across a

wide range of possible values.

SpinButton control

The SpinButton control lets the user select a value by clicking the control, which

has two arrows (one to increase the value and the other to decrease the value).

Like a ScrollBar control, a SpinButton can be oriented either horizontally or verti-

cally. Figure 17-14 shows a dialog box that uses two vertically oriented SpinButton

controls. Each control is linked to the Label control on the right (by using VBA

procedures).

FIGURE 17-14:

SpinButton

controls.

The following descriptions explain the most useful properties of a SpinButton

control:

» Value: The control's current value.

» Min: The control's minimum value.

» Max: The control's maximum value.

CHAPTER 17  Using UserForm Controls    287

» ControlSource: The worksheet cell that displays the control's value.

» SmallChange: The amount that the control's value is changed by a click.

Usually, this property is set to 1, but you can make it any value.

If you use a ControlSource for a SpinButton, you should understand that the

worksheet is recalculated every time the control's value is changed. Therefore, if

the user changes the value from 0 to 12, the worksheet is calculated 12 times.

If your worksheet takes a long time to calculate, you may want to avoid using a

ControlSource to store the value.

TabStrip control

A TabStrip control is designed to navigate different sets of values using a single

page with the same set of controls. This control is rarely used, as the MultiPage

control provides a much easier way to achieve the same functionality. You can

effectively ignore it and use the MultiPage control instead.

TextBox control

A TextBox control lets the user enter text. Figure 17-15 shows a dialog box with

two TextBox controls.

FIGURE 17-15:

TextBox controls.

Following are the most useful TextBox control properties:

» AutoSize: If True, the control adjusts its size automatically, depending on the amount of text.

» ControlSource: The address of a cell that contains the text in the TextBox.

288    PART 4  Communicating with Your Users

» IntegralHeight: If True, the TextBox height adjusts automatically to display full lines of text when the list is scrolled vertically. If False, the TextBox may

display partial lines of text when it is scrolled vertically.

» MaxLength: The maximum number of characters allowed in the TextBox.

If 0, the number of characters is unlimited.

» MultiLine: If True, the TextBox can display more than one line of text.

» TextAlign: Determines how the text is aligned in the TextBox.

» WordWrap: Determines whether the control allows word wrap.

» ScrollBars: Determines the type of scroll bars for the control: horizontal, vertical, both, or none.

When you add a TextBox control, its WordWrap property is set to True, and its

MultiLine property is set to False. The net effect? Word wrap doesn't work! So

if you want the words to wrap in a TextBox control, make sure that you set the

MultiLine property to True.

ToggleButton control

A ToggleButton control has two states: on and off. Clicking the button toggles between these two states, and the button changes its appearance when clicked. Its

value is either True (pressed) or False (not pressed). Figure 17-16 shows a dialog

box with four ToggleButton controls. The top one is pressed.

FIGURE 17-16:

ToggleButton

controls.

Working with Dialog Box Controls

This section offers a few pointers on moving, resizing, and aligning dialog box

controls to get your UserForms looking just right.

CHAPTER 17  Using UserForm Controls    289

Moving and resizing controls

After you place a control in a dialog box, you can move it and resize it by using

standard mouse techniques. Or for precise control, you can use the Properties

window to enter a value for the control's Height, Width, Left, or Top property.

You can select multiple controls by Ctrl+clicking the controls. Or you can click and drag to 「lasso」 a group of controls. When multiple controls are selected, the Properties window displays only the properties common to all selected controls.

You can change those common properties, and the change is made to all controls

you select, which is much quicker than doing them one at a time.

A control can hide another control; in other words, you can stack one control on

top of another. Unless you have a good reason for doing so, make sure that you

don't overlap controls.

Aligning and spacing controls

The Format menu in the VBE window provides several commands to help you

precisely align and space the controls in a dialog box. Before you use these com-

mands, select the controls you want to work with. These commands are fairly

self-explanatory.

Figure 17-17 shows a dialog box with several CheckBox controls that are about to

be aligned.

FIGURE 17-17:

Choose

Format ➪ Align

to change

the alignment

of UserForm

controls.

When you select multiple controls, the last selected control appears with white

handles rather than the normal black handles. The control with the white handles

is the basis for aligning or resizing the other selected controls when you use the

Format menu.

290    PART 4  Communicating with Your Users

Accommodating keyboard users

Many users prefer to navigate through a dialog box by using the keyboard: Press-

ing Tab or Shift+Tab cycles through the controls, while pressing a hot key instantly activates a particular control.

To make sure that your dialog box works properly for keyboard users, you must be

mindful of two issues:

» Tab order

» Accelerator keys

Changing the tab order

The tab order determines the order in which the controls are activated when the

user presses Tab or Shift+Tab. It also determines which control has the initial

focus  — that is, which control is the active control when the dialog box first appears. For example, if a user is entering text in a TextBox, the TextBox has the

focus. If the user clicks an OptionButton, the OptionButton has the focus. The first control in the tab order has the focus when Excel first displays a dialog box.

To set the control tab order, choose View ➪ Tab Order. You can also right-click the

dialog box and choose Tab Order from the shortcut menu. In either case, Excel

displays the Tab Order dialog box, shown in Figure 17-18.

FIGURE 17-18:

The Tab Order

dialog box.

The Tab Order dialog box lists all the controls in the UserForm. The tab order in

the UserForm corresponds to the order of the items in the list. To change the tab

order of a control, select it in the list and then click the Move Up or Move Down

button. You can choose more than one control (click while pressing Shift or Ctrl)

and move them all at one time.

CHAPTER 17  Using UserForm Controls    291

Rather than use the Tab Order dialog box, you can set a control's position in the

tab order by using the Properties window. The first control in the tab order has

a TabIndex property of 0. If you want to remove a control from the tab order, set

its TabStop property to False.

Some controls (such as Frame or MultiPage controls) act as containers for other

controls. The controls inside a container control have their own tab order. To set

the tab order for a group of OptionButtons inside a Frame control, select the Frame

control before you choose the View ➪ Tab Order command.

Setting hot keys

Normally, you want to assign an accelerator key, or  hot key,  to dialog box controls. You do so by entering a letter for the Accelerator property in the Properties window. If a control doesn't have an Accelerator property (a TextBox, for example), you can still allow direct keyboard access to it by using a Label control. That is, assign an accelerator key to the Label and put the Label directly before the TextBox in the tab order.

Figure 17-19 shows a UserForm with three TextBoxes. The Labels that describe the

TextBoxes have accelerator keys, and each Label precedes its corresponding Text-

Box in the tab order. Pressing Alt+D, for example, activates the TextBox next to

the Department Label.

FIGURE 17-19:

Use Labels to

provide direct

access to controls

that don't have

accelerator keys.

Testing a UserForm

The VBE offers three ways to test a UserForm without calling it from a VBA procedure:

» Choose Run ➪ Run Sub/UserForm.

» Press F5.

» Click the Run Sub/UserForm button on the Standard toolbar.

292    PART 4  Communicating with Your Users

When a dialog box is displayed in this test mode, you can try the tab order and the accelerator keys.

Dialog Box Aesthetics

Dialog boxes can look good, bad, or somewhere in between. A good-looking dialog

box is easy on the eye, has nicely sized and aligned controls, and its function is

perfectly clear to the user. Bad-looking dialog boxes confuse the user, have

misaligned controls, and give the impression that the developer didn't have a plan

(or a clue).

Try to limit the number of controls on your form. If you do need many controls —

generally more than ten — consider using a MultiPage control to split the task the

user has to do into logical (and smaller) steps.

A good rule to follow is to try to make your dialog boxes look like the Excel built-in dialog boxes. As you gain more experience with dialog box construction, you can

duplicate almost all the features of the Excel dialog boxes.

CHAPTER 17  Using UserForm Controls    293

IN THIS CHAPTER

» Creating a dialog box: A hands-on

example

» Working with ListBox controls

» Letting the user select a range from a

UserForm

» Showing a progress indicator for

lengthy operations

» Creating a stay-on-top dialog box

» Displaying a chart in a UserForm

» Presenting a handy checklist for

creating dialog boxes

Chapter 18

UserForm Techniques

