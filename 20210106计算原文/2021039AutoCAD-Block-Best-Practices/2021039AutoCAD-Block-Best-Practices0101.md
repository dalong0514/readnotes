## Preface

Block is one of the most important productivity tools in AutoCAD. By optimizing your blocks, you will find that AutoCAD is not just about drawing lines or just get the drawings done. You can draw lines fast, but productivity is beyond that. It is not just to get the drawings done.

You need to be able to modify drawings easily during the design process. You may be able to finish your drawing very quickly, but you may spend too much time when you are doing revisions. If you do, then you are not productive. Drawings also should provide necessary information. Furthermore, you will want to add some intelligence so that you can automate some process.

In this e-book, you can learn how to create, automate, and manage your blocks. We are not only discussing features, but we are also talking about productivity concept. Moreover, how you can use blocks to solve problems in AutoCAD.

Prerequisite: This e-book is intended for basic to intermediate AutoCAD users. However, I believe it can give some fresh information to veteran users. You have to at a minimum, know and able to use AutoCAD basic features.

The tutorial files: We include tutorial files with this e-book. Extract the zip file to a location you can access easily. When you find instruction to open a drawing file, you can find it in tutorial files folder.

Download the exercise file here: AutoCAD Block Best Practices tutorial files.

2『已下载书籍附件。（2021-04-20）』

Drawing units in this e-book: This e-book uses the metric unit. However, drawing unit should not be an issue. You do not draw many objects in the exercises. We focus more on productivity concept.

However, if this book instructs you to create a new file, create it using ISO template.

## 0101. The Block Basic

We all learned how to use AutoCAD from different resources. Not all of those resources include block in their learning material. At least I often do not find it in books from local publishers here. I also remember when I took an AutoCAD class; they do not teach me anything about the AutoCAD block. Probably because I only took a basic class.

I assume that this could happen to you too. So let's start this book from the basic of AutoCAD block.

If you already know how to create, insert, and modify the block, you may skip this chapter. However, I recommend you to at least skim through this chapter.

Block advantages

Why are we using blocks?

1. Blocks are single objects. If you have a complex drawing, selecting many lines, hatches, arc, and circles can be tedious and prone to mistakes. If you define them as a block, you can select them easier. You can also select multiple blocks with the same at once using filter or QSELECT.

2. When we update a block definition, it will also update all blocks with the same definition. This feature is very useful if you often need to change your symbol or a common design. However, if

you work in a team, you need to consider which part of your design should use XREF instead of

blocks.

3. You can save blocks in a separate file as reusable contents library. You easily reuse them later.

This technique will make your drawing process faster and also maintain drawing standard. You can share them for all AutoCAD users in your company, to make your drawing uniform between AutoCAD users.

4. Blocks can provide information. You can use that information and report them in a table. For example, the report can be a hole table (in the manufacturing industry), schedule or BOM, or points coordinate.

5. Autodesk has added many features related to blocks. Using dynamic blocks and annotative blocks can help to reduce tasks and confusion among users.

Creating Block

The most basic thing in learning block is to create and to use it. There are several ways to create a block.

The common way to create a block is by using create block tool. This tool is located in your ribbon, home tab, block panel.

You can also activate「create block」tool by using B then [enter] in command line or dynamic input

Let's try using this tool.

Open valve.dwg included with this e-book.

In this file, you can find a valve symbol. This valve is made from one polyline and two lines.

Activate「create block」tool. AutoCAD opens a dialog box.

There are several options available, but let's focus on field and buttons that are shown in the red rectangle.

To create a block, you have to define at least:

1. Block name

2. Base point of the block

3. Objects you want to add to the block.

Defining block name

You have to give a unique name to your block. Do not give the same name with existing block in your

drawing, unless you want to replace the definition. We can see how replacing definition affects your

drawing later.

Give this block name: gate flanged valve.

Type it in name field like shown above.

Defining block base point

A block base point is your reference point when you use it. For a valve, we use its center. It makes us easier to snap it to a pipe when we draw a P&ID diagram.

Click pick point button.

The block dialog is closed temporarily, allowing you to select a point. Snap to midpoint as shown below.

Block definition dialog is restored.

Defining objects

The last thing we need to do is to select objects. Click Select Objects button. This action also closes the dialog box temporarily.

Select all objects then press [enter] to end object selection and bring back block definition dialog box.

Now you should see the block preview on the right side of block name field.

Before we make the block, make sure open in block editor option is unchecked. We do not use block editor in basic block tutorial.

Now click OK in the dialog box. Save your file.

If you select the valve, now it is only one object. No longer consists of three objects. You can only see one grip: the block base point.

Inserting Block

We have created the valve block. Now let's use it.

You can insert your block by activating insert block tool. You can find it on AutoCAD ribbon> home tab> block panel.

Command alias for insert block is I then [enter]

Insert block definition in a file

After you activate the tool, you can see insert block dialog.

Your block name is in name drop down field. We only have one block here. When you have more block definitions in your file, you can see all the blocks in the list. You can choose which block you want to insert by clicking down arrow on the right side of the name field.

There are three options we can define here: insertion point, scale, and rotation. If you choose to activate

「specify insertion point」then you must set the value by clicking points on drawing area.

The common practice is we define insertion point by clicking a point on the screen. However, for scale and rotation would be easier if we set the value in this dialog box.

Let's try to insert it.

Check specify on-screen in insertion point section. Leave the check boxes unchecked for scale and rotation section.

Make sure scale set to 1 and rotation angle to 0. Click OK and click a point to place it. We only need to define one point because we already define scale and rotation in the dialog box.

Try to insert the block again. This time check「specify on screen」for scale and rotation angle. Examine how it works. Don't forget to check your Command Line to see what is AutoCAD asking you to do!

Inserting a file as a block

We can also insert a file into the current drawing. All objects in the drawing file will be converted into a single block. AutoCAD uses the file name as block name.

Open Valve – Gate Flange.dwg. The objects are the same with the previous file we used before. It has a polyline and a couple of lines. It is not a block yet.

One thing you should remember when inserting a file as a block. The drawing origin (0,0) is the block base point. You can see the UCS showing the block base point. If you want your base point somewhere else, move your objects.

Without making any changes, close this file. Click Cancel if AutoCAD asks you if you want to save it.

Create a new file, then activate insert block tool.

Click Browse button, then select valve – gate flange.dwg.

Click open. Now you can see the file name in block name field.

Place your block. Now select it to check if it is defined as a block.

Nested block

A nested block is a block with one or more block definition inside it.

Open kitchen.dwg. You can find it in provided files or sample file from AutoCAD installation. This file is a block library. There are several blocks inside it.

Close this file without saving it.

Create a new file, then insert kitchen.dwg as a block. Before you insert the file, examine that the block name field is empty.

The whole file becomes one block: kitchens. There are several blocks inside our kitchen block. This kitchen block is a nested block.

Activate insert block tool one more time. This time you can see not only kitchens block is listed here.

There are also all blocks in that file.

Inserting block from another file

Block definition is file specific. If you create a block in one file, you only have the block definition in that file. If you create a new drawing file, the block definition is not available there.

So how can we insert a block from another file? We learned that we could insert a file as a block. If there are several blocks inside the file, AutoCAD also imports all block definitions. You can delete the kitchens block and insert only block what you need. However, this is not a good practice. It brings many blocks that you do not need into that file.

A better way to import a block from other file is by using design center. You can open design center palette by accessing it from your Ribbon> View tab> Palettes panel.

You can also open it by typing ADCENTER from the Command Line or press [ctrl] + 2.

The Design Center looks and feels like Windows Explorer. You can see folders and file name in the left pane, and items inside the folder on the right pane. The difference is you can see what is inside a DWG

file. You can see blocks, dimension styles, layers, and other drawing styles.

If this is the first time you use Design Center, it should open sample files folder. If you do not see the sample files, navigate to C:\Program Files\AutoCAD xxxx\Sample\DesignCenter.

C is your drive letter where you install AutoCAD. Navigate to another drive if you do not install AutoCAD on C drive. XXXX is the AutoCAD version you have.

Browse and choose any DWG file. Click the + sign next to the file name to expand it. Find Blocks category. Click to select it.

The right pane now shows blocks preview. Find a block that you like, right click on that block. Click insert block in the context menu.

AutoCAD inserts your block into the current drawing.

You can also drag and drop the block to your drawing area.

This method inserts only the block you need, not all definition in the drawing.

Working with Units

Before we continue, let's discuss the relationship between drawing and block unit.

When we create a block, there is an option for your block unit.

By default, AutoCAD uses your drawing file unit. Many AutoCAD users do not concern about units, and this can make many problems in the future. If you have not taken this seriously, it is about time that you do.

AutoCAD does not understand real world measurement. When you create a drawing or a block, you need to tell AutoCAD what unit you are using. If you have a block drawn in inches, then you insert it to a drawing with the metric unit (mm), AutoCAD resize it as necessary.

You can convert it manually, but if you set it properly for every blocks and drawing, this can avoid unnecessary mistakes.

To prevent confusion in your drawing, start with an appropriate template. If you draw in metric, use ISO

template when you create a new drawing. Imperial users usually do not have this problem because AutoCAD uses the imperial unit as default.

Modifying Block

I consider block as reusable contents. I usually do not modify the block library, but I replace blocks in my drawing.

In real life, when I placed a chair in my room then I want a different model, I do not modify it. I replace it with a different model. The same concept applies to block. If you modify a block, you will have a different object with the same name. Modifying block can be confusing if you place standard parts/objects.

However, many AutoCAD users consider it as a benefit of using block. When you update a block definition, every block instance using the same definition is updated. So this is true if you draw a common design and define it as a block.

I suggest you modify block for these reasons:

1. The block needs correction/update. We usually modify a block in block library for this purpose, not only in the specific drawing.

2. The block defines a common design that we often modify during the design process. However, for standard parts (bolt, nuts, and other standard parts) avoid to modify it. You may need it in the future. Create new block then use the new one.

Disassemble and redefine block

This method is the only way we can do it in the past (in old AutoCAD version). We have to explode our block, make necessary changes, then create a block with the same name.

Let's open valve.dwg we used before. We have defined a block here. Use Copy tool and make several copies of your block. The number and locations of your blocks do not matter. We just want to see how modifying block affects your drawing.

Select a block, then explode it.

You can find explode on your Ribbon> Home tab> Modify panel.

Add two horizontal lines to this valve. Our engineers ask us to modify our block to make it clear where to connect their pipes to our valve.

Use image below as a reference.

We finished doing the changes. Activate「create block」. This time, we do not have to type block name.

Choose existing block name in the dropdown field.

Repeat the same process for creating AutoCAD block. After you recreate the block, AutoCAD shows a warning. The warning says our action will redefine existing block. It asks us to redefine or cancel the action. We do want to redefine it. Choose redefine.

Examine your drawing. You should see all of your blocks are now updated.

Using block editor