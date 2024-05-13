## 0601. Controlling Block With Constraints


In the previous chapter, you learned how to create a dynamic block. Since AutoCAD 2010, Autodesk introduced the parametric capability in AutoCAD. We can use constraints to give our blocks intelligence like parameters and action we did before.

Parameters and actions in dynamic blocks allow you to modify block like when you do it in drawings.

You can stretch, move, or rotate your objects within a block.

Constraints in parametric work differently. Constraints give you the ability to control the geometry and object size. Parametric can be an option if you need to define size and relationship between geometry.

There are some good examples in AutoCAD tool palettes. Let's try a channel beam.

The way we can change the beam profile is different between parameters and actions.

Here, we define how an object relate to the other. Should it be parallel to adjacent line? What's the line length? Is the length relate to other objects length?

Parametric design has been used in the manufacturing industry for decades. Imagine if you have a standard part. It has the same geometry but has different sizes. It is a lot more complex than scaling that part!

We do not cover parametric design in details in this e-book. If you want to see about its capabilities, try these resources:

1. AutoCAD parametric design on YouTube by DSCOHN.

2. AutoCAD geometric constraints part 1 on Daily AutoCAD.

3. AutoCAD geometric constraints part 2 on Daily AutoCAD.

4. AutoCAD dimensional constraints part 1 on Daily AutoCAD.

5. AutoCAD dimensional constraints part 2 on Daily AutoCAD.

Using dimensional constraint

Let's do an exercise. Open window.dwg.

This drawing has one window block. We will add dimensional constraints so we can control the window size. The challenge here is we need to control glass panel, and windows frame as well. Using stretch actions are not a good option here. It may require many actions and can be very complicated.

Select the window block, right click and choose block editor from the contextual menu.

In your contextual ribbon, dimensional panel, activate linear dimension.

Add linear dimension like below.

After you click the points, you can type to change the constraint name and expression.

To accept default value now just press [enter]. You can modify the values later on properties palette.

Similar to parameters in the dynamic block before, we can change our window size by dragging it. This time, we want to control the sizes completely using a table.

While you select the parameter, change number of grips in properties palette to 0.

Add all constraints to control frame size as below. Don't forget to change the expression to 'frame'

parameter. By changing the expression to frame, it links to frame parameter we placed before, and take its value.

Add two more dimensional constraints to define window height and width.

* Previous dimensional constraints are hidden for visibility purpose.

Add more constraints to define panel sizes. We can make it possible to have different size for top and bottom panel by using a simple formula.

We allow users to change bottom panel height, and top panel adjusts automatically. We set frame between panels to fix size: 20mm.

Then top panel formula should be:

=(height-20-(2*frame))-bottom

See image below as a reference.

We have set all dimensional constraints. Let's test it.

Changing parameters value

Activate parameters manager.

You can see another palette opened. Notice that every dimensional constraint we created before are listed here.

Try to change width value to 400. Remember, you need to change it under expression column.

You may see a different result than what I have below, but you should see the same mess as I do. Change any other parameter to see how it works.

Dimensional constraints only move constraint points. If we only use dimensional constraint alone, it's hard to predict how it works.

To keep the window geometry, we have to use geometric constraints to tell AutoCAD how the objects relate to each other.

Click UNDO until you see the window to its original form before we change any parameter value.

Using geometric constraint

The first thing we have to do is lock a point as a fixed point. Insert a point using POINT command at 0,0.

Now lock the point using fix constraint. Activate the tool and select the point.

We use a fix object as a reference for other geometry.

Next, we want the windows corner point to always coincident with our reference point. Activate coincident constraint.

Click rectangle corner, then click the point. Now we have two geometry constraints in our block.

This constraint keeps our window at the reference point. We need it because we want full control of our base point.

Using Auto Constrain

You can try to apply all geometry constraints manually to this window. However, we are not focusing on constraints, so let's just use auto constrain and let AutoCAD automatically complete it.

Activate auto constrain.

Activate Auto Constrain, type S then [enter] to change the settings. Alternatively, you can press down arrow to activate it using the Dynamic Input.

In Auto Constrain settings dialog box, activate all constraints.

]

Click OK.

Auto Constrain is still active. Select all objects then press [enter] to end selection.

You should see all of the constraints applied by auto constrain.

If you do not see them, click show all in geometric constraints panel.

Hover your mouse pointer over an object. AutoCAD highlights all constraints that relate the object to other objects.

Let's test our window again. Change windows height, width, and panel size.

Do not change expressions that use formula or refer to other parameters.

Now it is much better. However, there is one more thing to fix.

The gap distance between panels is still not correct. We can fix this by adding one more dimensional constraint.

Add linear dimension and type gap=20 to change parameter name and value. Regardless the current gap was shown.

After you typed it, the geometry adjusts to the new value.

This window now should works.

Let's do a final modification to our parameter. In Parameters Manager Palette, find a parameter that defines our top panel height. Change 20 to gap, so we can control the size using the parameter.

Parametric blocks allow you to control objects by their sizes. Not by actions like what we do when drawing with AutoCAD. If you need to control objects by modifying them, then the dynamic block actions are more suitable.

Using block table

We can control object size using grips, but this time we use block table. It is very similar to the lookup

table; the only difference is block table is for the dimensional constraint.

Activate block table.

AutoCAD asks you to place the block table. Click somewhere below the base point.

Next, AutoCAD asks you to define the number of base point. Press [enter] to accept 1 as the default value.

AutoCAD opens a dialog box. Click add properties at the top right of this dialog box.

Another dialog box opened. Hold [ctrl] then click parameters name to select it. Select frame, height, width, bottom, and gap parameters.

Click OK.

Now click add user parameter to define our parameter.

In opened dialog box, fill type for parameters name, and change this parameter type to real.

Click OK.

Now we can add values to our table. Click in the cell to type your values.

In this example, I use 3 windows data. You can add more as necessary, for your exercise.

Click OK, then save your block. Close block editor.

Test your block by selecting it and click the down arrow. You can select windows type and change its size now.

If you see trailing zero in this selection, it is because it follows your decimal unit precision.

More about dynamic blocks

This part is the end of our dynamic block basic tutorial. There are many possibilities that you can do with it. You can find more examples in a later chapter in this e-book.

EXTRACTING DATA

We have done many things with our blocks. You may found it useful. However, there are more things you can do. By using blocks, it is not only you can finish your drawings faster. You can also generate reports from them quickly.

In this chapter, we extract data from our blocks.

Information in your blocks

We learned that we could add information to our blocks. How can we use it? We can extract the information and report them in a table.

There are data we can get from blocks. You need to know these data types so you can plan which information you should add to your blocks.

Attributes

We can add as many attributes as we want. If we have a door block, AutoCAD only recognize its name.

You can add more data such as manufacturer, fire rating, door accessories, and any other data that you consider important. We have done this earlier in this e-book.

Parameters

We can use parameters as information as well. In column example, we can stretch our column so we can have different sizes. We have b and h parameters to show the column size. Moreover, we also have column type from a lookup table.

We can extract these parameters to our table.

Using fields in Attributes

Fields are an extremely useful feature for automation. A sample of using fields is to put common data in title blocks. When your drawing information changed, the information can be automatically updated. We can use it for plot date, last saved, and other common information.

We can see more examples of fields in block samples later.

Using data extraction

Open data extraction.dwg. This building plan was created using blocks. Walls, doors, and windows are typical building elements. Therefore, we can consider to create them as a block and reuse them in our design process.

There are nothing special about the blocks. You should be able to create them after reading previous tutorials. You might want to examine them before you start using data extraction.

Let's activate data extraction. It is on Annotate tab, Tables panel.

Data extraction is a step-by-step wizard that we can follow easily. We start on the first page.

First page: Begin

In this page, you can start from scratch or select existing data extraction template. If you often create similar column schedule, then you can use it again later.

Because we never do it before, choose to create a new data extraction in this page.

Click next. AutoCAD asks you a file name to save our settings later. Give it name column schedule. Click save.

Second page: Define data source

Here, we can define if we want to extract data from all objects in the current drawing file, all objects in

multiple files, or extract data only from selected objects.

For this exercise, choose drawings/sheet set and activate include current drawing.

Third page: Select objects

AutoCAD displays ALL objects in your drawing on this page. We only want to create a schedule for the rectangular column. Uncheck everything except rectangular column.

Fourth page: Select properties

The next step is to define which properties we want to extract. We are only interested in getting column type and sizes. They are dynamic block properties. To shorten the list, uncheck everything in category filter (the right column) except for dynamic block.

There are only three properties listed after you filter objects: b, h, and column type. Check all of those properties.

Fifth page: Refine data

In this page, we can see the preview of our table. You can choose to go back and uncheck column you do not need and arrange the column sequence.

Drag column title to arrange them. Uncheck show name column.