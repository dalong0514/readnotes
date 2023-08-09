## 0301. Basics of the AutoCAD .NET API (.NET)

To use the AutoCAD® .NET API effectively you should be familiar with the AutoCAD entities, objects, and features related to the tasks you want to automate. The greater your knowledge of an object's graphical and non-graphical properties, the easier it is for you to manipulate them through the AutoCAD .NET API.

### 3.1 Understand the AutoCAD Object Hierarchy (.NET)

An object is the main building block of the AutoCAD .NET API. Each exposed object represents a precise part of AutoCAD. There are many different types of objects in the AutoCAD .NET API. Some of the objects represented in the AutoCAD .NET API are:

Graphical objects such as lines, arcs, text, and dimensions

Style settings such as layers, linetypes, and dimension styles

Organizational structures such as layers, groups, and blocks

The drawing display such as view and viewport

Even the drawing and the AutoCAD application

The objects are structured in a hierarchical fashion, with the AutoCAD Application object at the root. This hierarchical structure is often referred to as the Object Model. The following illustration shows the basic relationships between the Application object and an entity that is in a BlockTableRecord, such as Model space. There are many more objects in the AutoCAD .NET API that are not represented here.

