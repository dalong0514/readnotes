Click next to move to next page.

Page 6: Choose output

In this page, you can choose your output. We want to place this table in our drawing, but you may want to export it to an external file as well.

Click next to continue.

Page 7: Table style

Data extraction output is in a table format. You can choose existing table style or modify it as necessary

here. Standard style is already set for this tutorial.

Click setup table manually and enter your table title. Don't forget to check use property names as additional column headers.

Click next.

Page 8: Finish

There's nothing to do on page 8. It is just a confirmation page to place or export the data extraction.

Click Finish.

Put your table below the building plan.

For your exercise, try to extract door and windows schedule.

Updating data extraction

Have you tried to delete or add columns? Your table will not automatically update. Data extraction is recognized as an external reference. To update it, you can open external reference palette, right click the data extraction link and choose update data extraction.

You can detach data extraction to remove the link from your drawing to extraction setup. Your data extraction table is in your drawing, but no longer linked to data extraction.

This method only updates the table in your drawing. If you export it to XLS file, you need to regenerate the excel file.

It is quick and easy. Choose edit existing data extraction at the first page; the page 2-7 use our previous setup so we don't need to change them.

Linking data extraction to external excel file

In some cases, you use the same block with different ID. For example in schematic design. You can it may have many attributes, but they have the same value for identical ID. It does not make sense if you have to define price every time you place a component with the same ID. Remember, prices change regularly.

When it changed, you need to update every block attribute in your drawings!

You need to have Microsoft Excel installed on your computer to do this exercise The internal attribute is very useful if they have a unique value. However, if they have a common value, we better create an external excel file and link it to our data extraction.

You need to create an excel file that contains the data. In this sample, we still use column schedule. In your exercise files folder, you can find column data.xlsx.

It has column type as the identifier and data for each item. The material, Finish and Accessories for each column. We can link it to our data extraction.

First, detach data extraction from external reference palette. Delete our schedule table.

Activate data extraction, and choose Edit an existing data extraction. Browse and find our previous data extraction file.

Click next until you find page 5. At the right bottom of this page, click Link External Data.

We have not set up a data link, so the list is still empty. Click launch data link manager to create one.

Another dialog box is opened. Click Create a new Excel Data link.

Type column data when AutoCAD ask you for this data link name, then click OK to accept it.

In new data link setup dialog, browse and find column data.xlsx in your exercise folder.

Click OK to create the data link. Click OK again to go back to link external data dialog box.

Match data in your drawing and your Excel file (1). Choose column type in drawing data column and also column type in the external data column. You can check if the data in both columns are matched by clicking check match.

You can choose to exclude some columns from the external table here (2). You can see all column in Excel file is listed here.

MORE BLOCK BEST PRACTICES SAMPLES

Until this chapter, you have learned a lot about blocks. Let's explore some samples to give you some more perspective how using blocks can help.

You should already have some ideas how it can help you, but some more examples can give you a better idea of advanced uses of blocks.

Example 1: Building elements sample

In data extraction tutorial, you can find wall blocks and door blocks. If you are interested in learning how to create them, you can find it on CAD notes site:

1. Creating dynamic block for wall.

2. Creating dynamic block for door.

Example 2: Automatic Aligning Valve

We created a valve block in the first chapter. When we use it, we often need to rotate it for vertical alignment. After we placed it, we need to trim the pipe line.

We can add some actions to let the block automatically do this.

Alignment parameter

Open valve.dwg that contains your valve block. Open your valve in block editor.

Activate alignment parameter.

Place the alignment parameter at the insertion point. You can type 0,0 to do this or snap to the midpoint of our polyline.

Then type 100,0 to define alignment direction. Alternatively, click a point on the right side of the insertion point.

You have to place alignment parameter at the insertion point. Otherwise, it will not work.

You may want to save this block, close block editor and test it. Try to insert this valve and snap to a vertical line.

Wipeout

Wipeout is a nice trick to cover objects. It masks object below our valve, so we do not have to trim the pipe lines.

If you have a problem with Wipeout, you can use solid hatch as an alternative. I have seen some problems reported when we plot with wipeout.

See this article on CADnotes to see the details.

Open the valve in block editor again.

Activate wipeout from AutoCAD Ribbon> Home tab> Draw panel. You may need to expand your panel to see it.

Draw a rectangle using polygon tool from WIPEOUT command. It should cover your entire valve. Select the wipeout, right click. Choose draw order>send to back from the contextual menu.

Now we are done. Save this block and test it again.

Now this block is automatically aligned to vertical lines and 'trim' the lines where you place it.

You can turn off wipeout frame by activating wipeout command and choose frame from the options, instead of picking points.

Example 3: Foundation pile cap

In the previous example, we did a little trick so we can draw faster in schematic design. In this case, we add several reference points for reporting purpose. In basic block, we can only report its insertion point.

We add more points to report in our data extraction.

Open foundation pile cap.dwg from your exercise files. This drawing is pile cap with three piles. We want to extract the pile coordinates for setting up.

Add reference points

Add three points in the middle of our rectangle. These points are our attributes reference.

Hint: You can see points clearly by changing point style. Type DDPTYPE then [enter].

Adding attributes

Now add an attribute.

In attribute definition dialog box, check preset. We want AutoCAD to set this attribute value automatically, and we do not want users to change it. AutoCAD does not ask users to input this value if we activate preset. Also check invisible, because we do not want to show this attributes. This attribute is only for reporting purpose.

Fill attributes fields as necessary. For default value, type XY = then click insert field.

In opened dialog box, change field category to objects. We want to get properties from a point.

After you changed the field category, AutoCAD filters fields and show only objects fields. Choose Object from the list.

On the middle column, you need to choose which object to get the property. Click Select Object.

Pick the top most point. After you pick the point, AutoCAD updates the property list. Choose position.

This property is the point coordinate.

On the right column, now you should see how the properties are displayed. You can change the format and precision here.

Below, you can choose which value to show. Uncheck Z value. We only use this drawing in 2D, so we do not need the Z value.

Click OK to use this field. Click OK again to create the attribute. Place the attribute at the top of our pile cap.

Repeat the process for pile no.2 and 3.

Add one more attribute. Create a regular attribute as pile cap ID.

Create them as a block. You can use 0,0 as the block base point.

Now the block is ready. You can place the block to your foundation plan. You may create your own as exercise. Alternatively, you can use the one provided in final folder. Open foundation pile cap –

final.dwg. This file contains the same block in foundation plan.

Try to use data extraction to report all foundation coordinate. You can use my data extraction settings (included in exercise files) or try by your own.

Example 4: Coordinate label

This example is one of the most popular block tips in CADnotes. This tip is similar to pile cap foundation. Only here, we show the attribute to label the coordinate.

To add some style, we add a leader and add stretch action to allow users to move label position.

Create this block by your own. Use fields, so when you move the block, coordinate shown is updated automatically.

If you have a problem with it, you can refer to this post on CADnotes.

Example 5: Adjustable table length

This example is another exercise for you. This table also uses stretch action. We also add array action for the chair. So when users lengthen the table, the chairs are automatically added.

Again, try to create it by yourself. You can get the chair block from AutoCAD sample files.

You can find the finished block in sample folder.

MANAGING AND SHARING BLOCKS

You created great blocks. Now we need to manage them so our team and we can use it.

Managing block files

We need to save blocks in separate files. We can add all block definitions in a template, so when we create new files, they are already set. However, this is not recommended because it makes your files full of blocks that you do not use. It can make your files large and prone to corrupt. It is better only to insert blocks that you need.

Single block in single file

This method is common in the past, and many people still use this method. You have learned that you can draw in a file, then when you insert the file as a block, AutoCAD converts it into a block. To manage similar blocks, you can save them in a folder.

This method is preferred because it is easy to insert that file as a block when you create a simple AutoLISP program.

These are some examples how you can insert a file as a block using AutoLISP: 1. Block and conditional if: elevation label.

2. System variable and conditional COND: grid label.

Multiple blocks in single file

The better way to manage your blocks is to save all similar blocks in a single file. In AutoCAD, open the Design Center. You can see some sample files here.

They are block libraries. Each file has several blocks in the same category.

This method makes fewer files to manage. Using design center makes it very similar to managing a block in a single file. You can see the block and insert it to your drawings.

You can also easily create tool palettes from each file and use it to insert your blocks.

Creating and using tool palettes

What is a tool palette? Snipped from the help file:

Tool palettes are used to manage blocks, hatches, and other custom tools Block is not the only object it can handle. However, we only focus on blocks.

Adding blocks to tool palette

Palette is very useful and extremely easy to use. We can add an object to palette by drag it and drop it to the palette. You can create several palettes to separate blocks from different categories.

Let's create a new palette for this exercise.

Creating new palette

Open tool palette. Press [ctrl] + 2 if it hasn't opened. Right click anywhere in your palette. Choose new palette from the context menu.

If you have a problem using contextual menu, you can click the Properties button and choose new palette from the menu.

Give your palette name.

Open sample files or any file that has blocks in it. You can use a sample from design center or exercise from this e-book.

Click a block in your drawing once. This action selects the block. Now click selected block again and hold your mouse button. Drag it to your palette. You can see the block in your palette now. Very simple, isn't it?

Palette does not save your block definition. It only provides a link to the original file and a thumbnail. Do not delete your file that contains the block. If you do, you lose your blocks!

It is better to save it to a shared folder on your network.

Creating palette using Design Center

The previous method is easy. However, if you have hundreds of block, it can be a tedious task. The next method is another benefit of placing multiple blocks in a single file.

Open Design Center. Navigate to design center sample files. Refer to the folder location in design center dialog below.

Click the (+) sign to expand a file. Click block category to see the blocks. Right click on file name (or block category), and choose to create tool palette. AutoCAD creates a new palette, give it the same name as the file name. AutoCAD put all block definitions in that file to the new palette.

Creating palette group

We can use the palette to manage blocks in same categories. However, when we have dozens of palettes, it can be difficult to switch between palettes.

When we are doing a specific task, we can show only palettes we need, and hide the others. For example, when you are doing a civil drawing. You do not use architecture tools. Only civil drawing objects, annotations, and other that relate to your task. This reason is why we use Palette Group.

Right click your mouse above tool palettes and choose Customize Palette from the contextual menu.

Alternatively, you can access it through properties button.

There are already several palette groups available (2). See below annotation and design group. There are several palettes available. Activate the group.

You can do it by right click the group in Customize Palette dialog, and choose set current. Alternatively,

you can click Properties button above tool palette title, and choose from the list (3).

You can see only palettes in that particular group. Try to change current palette group to another group.

Examine what happened to your tool palette.

You can add a palette to a group by dragging it from left column (list of all available palette) to below a group folder. To remove it, you can drag a palette from the right column to the left. Alternatively, you can right-click a palette and choose remove from the contextual menu.

Sharing your blocks to your team

After you create your blocks, your need to consider how you should share it with your team. You can use your blocks as standard libraries. It is not a good practice if anyone in your company can create their blocks.

The best place to share your blocks is on your company server. You might need to ask IT department to create a shared folder for your team. You need to consider different permission for your users. CAD

managers should have administrative access because they need to update the blocks regularly. Your users only need read-only permission.

You can create and share tool palettes too. However, remember, tool palettes only point to the block location. So every user needs to be able to access the same path.

The easiest way to do it is to allow users to create their palette. They only need to find the block library on the server using design center. Then they can create palettes by a few clicks.

There are many ways to share your blocks.You can use AutoLISP or .NET programming if you are good at it. Find one that you think works best for you, and try not to overdo it and waste your time.

AFTER YOUR FINISH THIS BOOK

Blocks can significantly increase your productivity. Try to understand how it can work and how It can help in your daily tasks.

You may not use all of the features. Moreover, the samples in this e-book may not reflects your need in your industry. However, you should understand how blocks may help you, and implement it in your company.

If you have questions or want to discuss more blocks, you are welcome to discuss it on our support forum.

Here are how you can contact us:

1. Our Facebook page: http://www.facebook.com/CadNotes

2. Our Twitter page: http://twitter.com/CADnotes

3. Our Google+ page: http://google.com/+Cadnotestips

Document Outline

Preface Prerequisite

The tutorial files

Drawing units in this e-book

Table of Contents

The Block Basic Block advantages

Creating Block Defining block name

Defining block base point

Defining objects

Inserting Block Insert block definition in a file

Inserting a file as a block

Nested block

Inserting block from another file

Working with Units

Modifying Block Disassemble and redefine block

Using block editor

Replacing Block

Attaching Information to Block Creating attributes

Working with Block and Attributes Creating block

Inserting Block

Changing Attribute Value

Managing Attributes

Attributes to Reserve Space for Text Exercise: Create a room tag

Working with Layers in Block Layer 0 Layer properties override

ByBlock

Using other layers

Exercise Changing layers

Changing object properties

More layers practices

Annotative Block Understanding annotative block

Creating annotative block

Using annotative block

Adding intelligence to your block Using visibility states Adding objects to current state

Controlling visibility states

Changing parameter name

Using parameters and actions Adding parameters

Link action to parameter

Testing block

Parameter properties

Linking stretch action to opposite direction

Limiting size using list

Create a list of column size

Controlling block with constraints Using dimensional constraint Changing parameters value

Using geometric constraint

Using Auto Constrain

Using block table

More about dynamic blocks

Extracting Data Information in your blocks Attributes

Parameters

Using fields in Attributes

Using data extraction First page: Begin

Second page: Define data source

Third page: Select objects

Fourth page: Select properties

Fifth page: Refine data

Page 6: Choose output

Page 7: Table style

Page 8: Finish

Updating data extraction

Linking data extraction to external excel file

More Block Best Practices Samples Example 1: Building elements sample

Example 2: Automatic Aligning Valve Alignment parameter

Wipeout

Example 3: Foundation pile cap Add reference points

Adding attributes

Example 4: Coordinate label

Example 5: Adjustable table length

Managing and Sharing Blocks Managing block files Single block in single file

Multiple blocks in single file

Creating and using tool palettes Adding blocks to tool palette

Creating new palette

Creating palette using Design Center

Creating palette group

Sharing your blocks to your team

After your finish this book

