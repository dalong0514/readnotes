# 0201. Attaching Information to Block

Now we know how to create a block. We are going further in this chapter to add information to our blocks. We add information to a block using block attributes.

You may consider attribute as a tag. Similar to you tag your belonging, tags give information to anyone who sees it.

Creating attributes

Open door.dwg. This file is a simple door for plan drawings. It is not a block yet. We are going to add information before we define it as a block.

We will add this information:

1. Door model

2. Door manufacturer

3. Door cost

Activate define attributes tool. You need to expand block panel to see it. Click block panel name (with a small arrow pointing down).

Now you should see the tool. Click the icon to activate it.

You can use ATTDEF in command line to activate it using command alias AutoCAD opens attribute definition dialog box. For now, let us focus on the highlighted area.

First, let's fill attribute section (1). There are three fields you must give input here.

1. Tag is a unique tag name. AutoCAD does not allow you to use space for the tag name. Also, when you use lowercase letters, AutoCAD converts it to uppercase after you create it.

2. Prompt is what users see when they insert the block. AutoCAD asks users what input by showing what you input here. Make sure the question is clear to avoid users providing incorrect data.

3. Default is default value given. If the most answer to this question is 'single panel door', then it makes sense to use it as default value.

We want this information invisible in our drawing. Just for reporting purpose. Check invisible in mode section (2).

Although we do not show the attributes, it is necessary to set text size properly. We may need to modify our block in block editor later. If we set it too small, we might not be able to see it. Change text height to 250. Click OK to finish attribute definition.

Place the attribute under your door.

Create two more attributes: DOOR_MANUFACTURER and DOOR_COST. Make them invisible as well.

Working with Block and Attributes

Creating block

We have finished creating attributes definitions, but we have not created our block yet. Creating a block with attributes is the same process as we did before. The difference is we need to select attributes individually. Selection sequence determines prompt sequence. The first attribute you select is asked first to the users.

Let's try it. Activate「create block」tool. Click select object from the dialog box. Select all doors object at once. Then select each attribute individually, from top to bottom.

After you finish selecting them, create the block. Don't forget to give your block name and set its base point.

If you have difficulties, refer to the previous chapter.

The first time we define a block with attributes, AutoCAD opens edit attribute dialog box.

Leave the values as they are. Click OK.

Inserting Block

We have our block definition. Now we can insert it. The process is the same as we did before.

After we place the block, we see AutoCAD asks us to provide data.

Remember the question and default value provided here? We made it before!

You can see the questions and fill the value on the command line. However, if you prefer to see a dialog box, change ATTDIA system variable to 1. It allows you to have the same dialog box like when you first created this block.

If you want to keep default value, just press [enter]. However, if you need to change it, type new value then press [enter].

Changing Attribute Value

If we need to modify the attribute values, can we do it later? Certainly, you can. We can use edit attributes tool.

You can activate this tool using EATTEDIT from command line OR double-click your block. The veteran users may prefer ATTEDIT or ATE. All of those tools allow you to modify block attributes.

Activate the tool, then select the block you want to edit.

AutoCAD opens a dialog box. Choose the tag in the list and change the value in value field (in red rectangle). After you finish, click OK.

Managing Attributes

We edited attributes value. How can we edit attribute properties?

There are two ways to do this:

1. Edit block in block editor. Select your attribute then change its properties in the Properties Palette.

2. Use manage attribute tool.

We learn about block editor later. This time we use manage attribute tool. You can activate this tool from Ribbon> Home tab> Block Panel.

You can activate「manage attribute」tool by typing BATTMAN then press [enter]

Do you remember when we created a block with attributes? I mentioned that the attributes selection

determines the questions sequence. We can arrange attributes sequence, by using this tool. You can press move up/move down to arrange them.

BATTMAN can remove or edit attribute properties too.

Try the following in manage attribute tool:

1. Select door manufacturer tag, and click move up.

2. Select door model tag and click edit. Uncheck the invisible option. You should see the changes on your screen. Your tag is now shown.

3. Click cancel in all dialog box, to close all dialog boxes.

Attributes to Reserve Space for Text

I believe that attributes were originally meant to add information to block. However, many AutoCAD

veterans use block attributes to preserve space for their text. Autodesk also provides some samples that use this method. So it is safe to assume this is a recommended practice.

This drawing title is using block attributes. You can see this sample in tool palettes.

The advantage of using block attributes for this purpose is to maintain the standard. If you defined view title, you could use it for every project. Because you created it once and simply reuse it, you can expect the appearance is the same for every drawing. The font type, font size, and all objects that create the view title are not different. You and your team can use the same block. All you need to do is insert it and change the value of the attribute.

Exercise: Create a room tag

Create a new file. Use acadiso.dwt as your template. Before we start to create our block, open text style dialog. Change standard text height to 200.

We are going to create a room tag. This room tag shows room name and room number.

Activate define attributes (ATTDEF). Set the definition like below.

Make sure the invisible option is disabled. We want this tag to appear in our drawing. Give appropriate tag name, prompt, and default value.

Change text justification to center. Do you see the text height field? Now it is disabled.

If we define text height in text style with 0, then we can change the value when we use it. However, we defined the value to 200 before. Then AutoCAD uses the value every time we use that text style.

Click OK and place your tag.

Create another attribute for the room number. Use the same settings. Don't forget to give it an appropriate name. Place it below the room name.

The last thing we need to do is to add a rectangle around the room number. Create a rectangle like this.

Create a rectangle that's enough to hold 3 characters inside it. Don't worry if the tag name looks beyond your rectangle. It is supposed to look like that now.

Create it as a block and try to insert it.

You may want to create different annotation block with attributes as exercise.

WORKING WITH LAYERS IN BLOCK

When we want to include objects into a block, we need to consider how we use layers. There are many benefits of using layers. In this chapter, we learn how we can use layers in blocks.

Block can contain objects on different layers. We mostly use Layer 0 as default layer for AutoCAD

blocks. We see how other layers work with the block layers.

Layer 0

If you have a simple block, then most likely you draw all objects on layer 0. Layer 0 is a default layer in AutoCAD. Every time you create a drawing file, you find this layer. We cannot delete this layer.

Most people suggest you create objects for a block on layer 0. They advise you to to create your objects on layer 0, then make them as a block. When you insert it on a different layer, it inherits the layer properties.

In most cases, it is a good suggestion. However, in some cases, you would want to cheat a little and use another layer. Like in drawings, managing layers can bring many benefits to us.

Layer properties override

Each layer has its properties. The properties are color, line weight, line type, and so on. If you set the layer properties to other than ByLayer, then when you insert the block, it keeps the properties that you set explicitly. This behavior applies if you use layer 0 and any other layers.

ByBlock

Another property you need to understand is ByBlock. Let's imagine block as a container. A block has several objects in it. Each object has its properties. Moreover, they may be on different layers.

If you set layer properties to ByLayer, it inherits layer properties. When you change the layer color, the color of the objects changes too.

When we set the object properties to ByBlock, then we make it to inherit the block properties. Regardless on which layer the objects are.

Using other layers

Why do we want to use another layer for our objects in blocks? The same reason why we use layers in our drawings.

Let's take this column as an example.

When we plot it in a relatively small scale, we want to show all the details like on the left image.

However, when we use the same column in a site plan, the hatch is too dense. We only see a black rectangle. It would make sense to hide the hatches.

Placing the hatch on the different layer allows us to do it.

Exercise

Let's do an exercise to understand this concept better. Create a new file; you may use any template to do this exercise.

In your new file, add three layers. Set contrast properties for each layer, especially color, line weight and line type.

Now create five circles. Give the circles number so we can recognize them. I place text numbers on layer 0.

Set these properties for the circles.

Circle

Layer

Color

Lineweight

1

0

ByLayer

ByLayer

2

0

ByBlock

ByBlock

3

0

Blue

0.5

4

Layer1

ByLayer

ByLayer

5

Layer1

ByBlock

ByBlock

You need to make sure show line weight in drafting settings is on. If you do not activate it, you cannot see the line weight difference.

Create a block from each circle. Circle no.1 is the block no. 1; circle no.2 is the block no.2, and so on.

You can open the file that I use in your exercise files> final folder. You may use it without creating your file. However, it is important for you to know how to make that particular block.

Changing layers

Select all circles then change their layer to Layer 2. You can see block 1, 2, and 5 now use layer color and line weight. However, block 3 and 4 are still using their properties.

That is easy to understand because we have overridden no. 3 and no.4 properties. They do not follow layer properties.

Changing object properties

Now select all blocks, override their color and line weight.

Use magenta for color and 2 for line weight.

You can see only block 2 and 5 are affected.

As we discussed before, this is because they use ByBlock properties. What we did was overridden block properties, so they follow new block properties regardless what layer they use. Now freeze Layer 1.

We can see block 4 and 5 disappeared because we created those objects on Layer 1.

Unfreeze layer 1 then freeze layer 2. Remember: we moved all blocks to layer 2.

What happen? All blocks disappear, includes block 4 and 5! So when we freeze layer 1, block 4 and 5

disappear. When we freeze layer 2, they also disappear!

The blocks work as a container. All of the containers are on layer 2. Hiding layer 2 hides the blocks and all objects inside it. Doesn't matter on what layer the objects inside our blocks.

Unfreeze layer 2. Try to change properties and layers until you understand how they work with blocks.

You may want to examine this behavior further by adding more objects on different layers on these blocks.

More layers practices

There are many benefits we can get by using layers. I mentioned that we could hide details for the column for example.

Another common use for layers in the block is to hide/show block tags. This door below has a tag on another layer, so you can hide/show it when you need to.

ANNOTATIVE BLOCK

One of my favorite features in AutoCAD is annotation scale. Let's cover what it has to do with AutoCAD

block.

We can use a block as an annotation. For example, view title and room tag we created before is an

annotation.

This block provides information with symbol and text. Our challenge in using annotation is we have to keep the annotation readable. When we draw on model space, annotation size for 1:100 obviously is different for 1:200.

Using layout/sheet gives us many benefits. At least there are 10 benefits of using layout. However, there are also downsides. A common practice when we use layout is to draw everything in model space, but place annotations in the layout.

1. When we need to show the same drawing in different viewports, then we need to draw several tags. When the design change, we need to change those tags. This process is tedious work and prone to mistakes. If we use annotation scale, we only need to update one.

2. When you need to move your viewport or pan your drawing within the viewport, your annotations does not move. You need to move the annotations manually.

Placing your annotation on model space eliminates these disadvantages. To have them appear with consistent size when we plot, we need to use annotation scale.

We do not cover annotation scale in this e-book. If you are interested in learning more about annotation scale, you can find more details here:

1. Introduction to annotation scale.

2. Controlling annotation scale further.

We are focusing on the block in this e-book, so we limit the tutorial to annotative block.

Understanding annotative block

AutoCAD provides some annotative block samples. Let's try then to understand how they work.

Open your tool palette if it's not opened yet. You can open it by pressing [ctrl] + 3.

In tool palettes, find annotation tab. Find 'callout bubble – metric'.

After you click it, you should see this dialog. Unless you already use it before and click don't show me this again. Click OK and accept the scale.

Insert the callout bubble to your drawing. It looks like a regular block, isn't it?

Hover your mouse pointer over it. The annotative block shows annotative symbol when your pointer is above an annotative block.

Try to hover your pointer above a regular block. See that there is no annotative symbol appears.

Examine AutoCAD status bar. By default, you should see AutoCAD is using 1:1 scale unless you changed active scale in the previous dialog box.

Change active scale to 2:1. You can change it from annotation scale list button on the right side of AutoCAD status bar.

Insert the same block again. You may do it using insert command and choose the block from the list, or click the same block from the tool palette. The results will be the same using both methods.

What do we get? The last block is a half size of the previous block!

Try to change it to 1:2 then try to insert block again. That is how annotative block works. AutoCAD

adjusts its size to fit current scale we are using.

Learn more about the annotative scale so you can work with it comfortably.

Creating annotative block

The idea of the annotative block is simple. When you use a certain scale, AutoCAD reads it and adjust block size as necessary. It makes your block has a consistent size in every plot scale you use. If you set the text to 2 mm height, then doesn't matter what scale you are using, AutoCAD plots it with 2 mm height.

Creating annotative block is similar to creating a regular block. Let's try to create one.

I recommend you to work at full scale when creating an annotative block. Draw it with plot size, and set the current scale to 1:1. If you want your text to plot at 2mm height, then place it using 2mm height.

1. Make sure we set the current scale to 1:1.

2. After you finished, create an attribute definition.

3. Fill tag, prompt and default value.

You do not have to check Annotative option in this dialog box. If you do, when you create an annotative block, AutoCAD sets it to not annotative automatically.

Finish your tag like below. You can use lines, polylines or polygon.

Create your block. The only difference between creating a regular block and an annotative block is you have to check Annotative option.

Click OK to define your block.

Using annotative block

Let's try to use this block. The one we convert before is already placed in 1:1 scale. Change current scale and insert your block.

Remember: change active scale first, then insert your block.

