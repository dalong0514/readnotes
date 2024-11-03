## 记忆时间

## 目录

0501 Adding Intelligence to Your Block

## 0501. Adding Intelligence to Your Block

There are two ways you can add intelligence to your block. You can use actions or constraints. Autodesk introduces 2D parametric design or constraints in AutoCAD 2010.

Dynamic Block is a very powerful feature. We can add flexibility to our blocks. Until this chapter, we use blocks for typical symbols. When we need a typical symbol with minor differences, we have to create another block.

With dynamic block, we can manage similar blocks in a single block definition. Let's take these blocks as an example. The blocks above are different door types. If we use regular block, we need to create four different blocks. With dynamic block, we only need to create one. We can create a dynamic block in block editor. First, we need to create a regular block, then modify it.

### 5.1 Using visibility states

Visibility state is the most basic functionality in a dynamic block. We simply define which objects are shown in different states.

Open file door-elevation.dwg. This file is included with this book. This file contains four blocks. They are door panel and three patterns for the door. Select door panel block then right-click your mouse. Click block editor from the context menu.

AutoCAD opens this block in block editor.

To manage dynamic block visibility, we need to add visibility parameter. Find it in parameters tab, block authoring palettes.

Alternatively, you can click the small arrow below parameters group. Find it in Ribbon => Block Editor tab => Action Parameters tab. Click the small arrow to expand the list. If you think authoring palette takes too much of your desktop real estate, you can access actions and parameters here.

Click visibility parameter and place it at the right bottom of your door. Press [enter] to accept 1 as default number of grips.

You may place it anywhere you want it to. However, make sure you can find it easily. I recommend you to place it at the right bottom of your door.

This parameter shows warning sign. It means this parameter is not finished yet. You have some tasks to make it works.

1『原来动态块里的感叹警号表示没完成的任务。（2021-05-27）』

Click visibility states button on your Ribbon => Visibility panel.

By default, we have one visibility state named VisibilityState0. Select it and click Rename button. Change its name to simple. We are going to use it for simple panel door.

You can rename visibility state by clicking the name once, click Rename button, or right click then choose rename state from the contextual menu. Similar like renaming file name in Windows Explorer.

Create three new visibility states. Give them name panel, panel glass, and glass. When you create a new state, leave it to the default setting. Just input the state name.

1『这里新建状态的时候选择第三个「在新状态中保持现有对象的可见性不变」。（2021-05-27）』

After you finish, select simple and click set to current. AutoCAD sets current visibility state to the last one you created. We start working on Simple state, so set it as current.

You should see the check mark next to the state name.

Click OK.

The warning sign disappears. However, it does not mean we are done. What you see now is a simple door. We saved it in the Simple state. Now we are going to set the other states.

Change current visibility state to the Panel. You can do it by switching from visibility panel in block editor contextual ribbon.

Activate insert block, select panel block from the list. Use the top left corner of the door as the insertion point.

We have defined how our door looks in panel state. You may draw more objects to define how your door panel will look like. Switch to the Simple state and back to panel state. Have you seen the difference?

Now change current state to panel glass. You should see the door revert to the empty simple door. Insert panel and glass block at the same insertion point. Do the same steps for the last block. Change visibility state to the Glass state and add the glass block.

You have defined all four visibility states. The door should look like in different states. Test it by switching between all state from the ribbon.

Save your block and close block editor. Test your block. Select single door block. It is the left most of your doors. Remember, we add visibility states and other blocks to this block. You may delete other blocks to avoid confusion.

You should see visibility control at the bottom right of your door, or wherever you put it in the making process. Click it and change the visibility state.

2『四个门的切换，要去实践一下。（2021-04-20）补充：作者的思路是在不同的状态里新画图形，还有一个方法个人觉得更好，把所有的状态图形都画好放在一起，然后再每个状态里选中不在此状态下的「对象」，右键 => 对象可见性 => 在当前状态下隐藏。还有一个更佳的操作，右上角有一个「可见性模式」，点一下后，之前在该模式下隐藏的对象也能「显示」出来，这样就能「所有」的对象了。而且让某个对象是否在该状态下可见也可以通过旁边的「使可见」、「使不可见」来调整，更方便。（2021-05-27）』

#### 5.1.1 Adding objects to current state

Open the block in block editor again. Set glass as the current state.

Draw a circle as a door handle. Don't worry about its size and location. It is not critical.

Change to the Simple state. The door handle disappears. It is because we draw it on glass state, so it only appears when we change current state to glass. This concept is similar to drawing on layers.

We want to make it appears in every state, so we have to adjust its property.

#### 5.1.2 Controlling visibility states

We can control visibility using these three buttons.

1 Click the left most button. It is visibility mode button. It shows invisible objects in this block. That includes objects that are in other states.

2 Click the second button. It is Make Visible button. If the visibility mode is off, your hidden objects will be temporarily shown here. Select the circle and press [enter] to end selection. Change visibility mode again.

3 Now we can see the door handle in this state.

Change current state to another state. Repeat the same process to make the handle appears in every state.

#### 5.1.3 Changing parameter name

This block works as expected. However, working with a complex dynamic block that has many parameters can be confusing. Instead of using default parameter name, it would be easier for us to recognize what does the parameter do. I recommend you to rename your parameters because we can also use it in data extraction.

Data extraction will be discussed later in this book.

We are still working in block editor. Select visibility parameter and change parameter name from properties palette. In this example, I use door type.

### 5.2 Using parameters and actions

Actions simulate what you do in AutoCAD. To modify objects in AutoCAD, we move, array, stretch, or rotate our objects. These actions are what we use to built a dynamic block. To make those actions work properly, we have to relate actions to parameters.

Let's take an example. If you want to rotate objects, in the dynamic block we use rotate action. AutoCAD knows we want to rotate the objects. However, AutoCAD needs more details.

To rotate objects, we need to define base point and angle. To do this, we use rotation parameter.

#### 5.2.1 Adding parameters

Let's create a simple block. We are going to create a concrete column. Create a rectangle 500x500mm. Add concrete hatch inside the rectangle. Make sure this hatch is associative. Create a block from the drawing, make the column center as the base point.

After you finish, open it in block editor. Rectangular columns in design have different sizes. Instead of creating each size in separate blocks, we make one block and add the ability to resize it in our drawing. How do we change the size of the column? We use the stretch command. Stretch allows us to change the column size along the horizontal axis and vertical axis.

Now we know what action we can use. What about parameter? Which parameter should we use? Stretch works with a linear parameter. Activate linear parameter.

Let's add the parameter to our rectangle sides. Snap to its corners to define which side we want to stretch. When you place the parameter, click bottom left point first. The first click defines base point for your linear parameters. As before, we can see the warning sign. We still have things to do.

Before we continue, open properties palette. Select distance1 parameter, and change the parameter name to b. Modify the number of grips to 1. Do the same with distance2. Change parameter name to h, and the number of grips to 1. We reduce the grips number because we only need to stretch it to one direction.

1-2『不把 number of grips 修改为 1，后果会咋样？有待验证。（2021-04-20）回复：现在算是知道夹点数（number of grips）的含义了，是有几个可显示的拉伸点的意思。（2021-05-27）』

If you do not click bottom left point first, then you may see the arrow disappear. This option will remove the 2nd arrow that you defined when placing parameter. You can also remove unnecessary arrow by selecting them and press delete.

#### 5.2.2 Link action to parameter

We placed parameters. Now we can add action and link it to our parameter.

Activate stretch action.

AutoCAD asks you to select a parameter. Select b parameter. Now AutoCAD knows which parameter to link with this action. Now we need to define which point to associate with this action. Move your pointer to the right side of this column. You should see red circle appears at the bottom right corner of our column. Click your mouse.

Next, we need to define our stretch frame. Defining stretch frame is similar to defining stretch frame when you stretch when modifying objects. Use image below as a reference. Select the rectangle and press [enter]. We are done with the first action.

Repeat the same process to add a stretch action for h parameter. Our finished block should look like below. You should see two stretch action icon near the arrows.

#### 5.2.3 Testing block

Let's test this block before we continue. Testing the block regularly after add a few actions is a good practice. Testing the block allows us to find what is wrong and quickly fix it. If you test it after you add many actions, it can be hard to trace your mistakes.

Click test block in AutoCAD ribbon. Now we are working in test block window. Click our block to select it. You can see arrows from actions we added before. Click the arrow and move your mouse away. This action resizes the column.

If your stretch actions do not work as you expected, you need to check your parameters and actions to see what's wrong. Click close test block window.

#### 5.2.4 Parameter properties

Now our stretch actions work. However, if you notice, it does not work as we need it. After we stretch it, our action shifts our insertion point. If we want to keep our base point at the center, we have to stretch it using the same value to opposite direction. This is not really what we want it to work, isn't it?

The other problem is we, and other users can stretch it to any size we want. This behavior is not right. We want this column to have a precise size. Moreover, we might want to limit its minimum and maximum size.

We are still working in block editor. If you already close block editor, select your block, right-click, then select Block Editor from the context menu.

#### 5.2.5 Linking stretch action to opposite direction

Open properties palette then select linear parameter. In the Properties palette, change the base location to the midpoint. By changing the base location to the midpoint, our parameter stretch in both directions just by using single action. This behavior can keep our insertion point at block center.

1『超级关键的知识点，change the base location to the midpoint，可以让动态块拉伸的时候是两个方向，这样可以保证拉伸的时候基点不变。这个设置，应用场景应该很多。（2021-04-20）回复：此时此刻看这里的信息才真有感觉，之前一直在找双向拉伸的实现方法，在哔哔哩哩上的教学视频上看到把线性参数的基点位置改为「中点」即可。想不到这里就有答案，第一次看的时候因为没具体场景没啥感觉，但当时的直觉蛮准的，知道这个是个关键知识点。（2021-05-27）』

The parameter stretches to both sides now, but we have to add one more action to stretch our object to the left. Add action like we did before, using b parameter.

This time you have to select the grip in object selection. Select the grip to make sure the arrow stays at the rectangle corner. If we do not include it, it still works properly. However, the arrow is not at the right position after we stretch it. To avoid confusion, you can simply select all objects in this exercise.

Now if we test this block, if you stretch it, you can see it resizes to both directions. Repeat the process for h parameter and add stretch action to the top of this column.

#### 5.2.6 Limiting size using list

Now we are going to limit the column size. Select b parameter again. In Properties palette, change dist type to list. By defining the distance type to list, we can limit the users only can select predefined distance.

After you change Dist type, click … button on the right side of dist value list field. You need to click the field first before the button appears. In opened dialog box, type distance you want to add to the list and press enter. Alternatively, you can click Add after each entry.

Repeat the same process to h parameter. Don't forget to test your block after you finish. You may add other sizes that you consider appropriate.

#### 5.2.7 Create a list of column size

By defining a list, we allow users to stretch column only to specific sizes. However, if they need to change both directions, they must stretch it twice. We can expand this capability further. Let's edit the block again in block editor.

Insert lookup parameter to your block. Again, we see the warning sign. We need to add lookup action. Insert it from your authoring palette. After you place lookup action, select the parameter. AutoCAD opens a dialog box like below.

1『看到增加「查询」动作了，很适合用于数量一定的「数据集」。（2021-05-27）』

Click add properties to associate this action to our linear parameters. Another dialog box opens. You should see b and h parameters here. Hold [ctrl] and click both of them. We are going to use them all. Make sure you select add input properties in property type.

Click OK.

Now we can set what types and sizes we want for our column. Below lookup properties, fill your column types. You can type C1, C2, C3... for this exercise. Click on the same row below b parameter and choose the C1 size. Do not forget to choose h value.

Set every column size as you many as need.

After you finish, click OK.

You may want to change the parameter name from lookup1 to something that makes more sense. Now save your block and test it.

Instead of stretching the column, you can choose it from the list. Using a list prevents users from placing nonstandard column size, and of course, it is faster than stretching it twice.