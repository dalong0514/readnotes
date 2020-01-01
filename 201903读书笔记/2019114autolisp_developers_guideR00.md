## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 出生日期

用一句话描述你对这个大牛的印象。

#### 02. 贡献及经历

#### 03. 论文及书籍

#### 04. 演讲汇总

找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

1『自己的观点』

2『行动指南』

3『与其他知识的连接』

## 0104Communicate_With_AutoCAD.md



## 0105Manipulate_AutoCAD_Objects.md

You can select and handle objects, and use their extended data.

Most AutoLISP ® functions that handle selection sets and objects identify a set or an object by the entity name. For selection sets, which are valid only in the current session, the volatility of names poses no problem, but it does for objects because they are saved in the drawing database. An application that must refer to the same objects in the same drawing (or drawings) at different times can use the objects' handles.

1『处理的逻辑：要么是处理选择集，要么是处理特定的实体。』

AutoLISP uses symbol tables to maintain lists of graphic and non-graphic data related to a drawing, such as the layers, linetypes, and block definitions. Each symbol table entry has a related entity name and handle and can be manipulated in a manner similar to the way other AutoCAD ® entities are manipulated.

1『利用 symbol tables 来定位要操作的实体。』

Selection sets are groups of one or more selected objects (entities).

You can interactively add objects to, remove objects from, or list objects in a selection set. The following example code uses the ssget function to return a selection set containing all the objects in a drawing.

AutoLISP provides a number of functions for handling selection sets. The following lists some of the functions available for working with selection sets:

1. ssget - Prompts the user to select objects (entities), and returns a selection set.

2. ssadd - Adds an object (entity) to a selection set, or creates a new selection set.

3. ssdel - Removes an object (entity) from a selection set.

4. ssname - Returns the object (entity) name of the indexed element of a selection set.

5. sslength - Returns an integer containing the number of objects (entities) in a selection set.

The ssget function provides the most general means of creating a selection set. It can create a selection set in one of the following ways:

1. Explicitly specifying the objects to select, using the Last, Previous, Window, Implied, Window Polygon, Crossing, Crossing Polygon, or Fence options.

2. Specifying a single point.

3. Selecting all objects in the database.

4. Prompting the user to select objects.

With any option, you can use filtering to specify a list of properties and conditions that the selected objects must match.

Note: Selection set and entity names do not remain the same between drawing sessions.
















An application can add an entity to the drawing database by calling the entmake function.

Like that of entmod, the argument to entmake is a list whose format is similar to that returned by entget. The new entity that the list describes is appended to the drawing database (it becomes the last entity in the drawing). If the entity is a complex entity (an old-style polyline or a block), it is not appended to the database until it is complete.

The following example code creates a circle on the MYLAYER layer:

The following entmake restrictions apply to all entities:

1. The first or second member in the list must specify the entity type. The type must be a valid DXF group code. If the first member does not specify the type, it can specify only the name of the entity: group -1 (the name is not saved in the database).

2. AutoCAD must recognize all objects that the entity list refers to. There is one exception: entmake accepts new layer names.

3. Any internal fields passed to entmake are ignored.

4. entmake cannot create viewport entities.

For entity types introduced in AutoCAD Release 13 and later releases, you must also specify subclass markers (DXF group code 100) when creating the entity. All AutoCAD entities have the AcDbEntity subclass marker, and this must be explicitly included in the entmake list. In addition, one or more subclass marker entries are required to identify the specific sub-entity type. These entries must follow group code 0 and must precede group codes that are specifically used to define entity properties in the entmake list. For example, the following is the minimum code required to create a MTEXT entity with entmake:

2『好熟悉的 R12、R13 的信息，之前好多地方见过，去弄清楚各 CAD 版本号对应的 Rxx。』

The following table identifies the entities that do not require subentity marker entries in the list passed to entmake:

1『显然，这里面有「圆」CIRCLE。』

1『

这个章节里的 2 个源码好好看下。怎么创建「CIRCLE」实体，怎么创建「MTEXT」实体。想着参考「MTEXT」实体来创建「TEXT」实体，发现有问题，待解决。

解决办法，对象类型从 MTEXT 改为 TEXT，指定的实体从 AcDbMText 改为 AcDbText。解决办法的来源是在书籍「2019116AutoCAD_Platform_Customization.equb」里搜 AcDbText 关键词找到的。

```
(entmake '((0 . "TEXT");object style
  (100 . "AcDbEntity");required for all post-R12 entities
  (8 . "ALATER")	;layer
  (100 . "AcDbText")	;identifies the entity as TEXT
  (40 . 3.0)		;height
  (7 . "HZTXT")		;font style
  (10 4.0 12.0 0.0)	;insert point
  (1 . "hello dalong")))	;content
```

』

Complex entities (an old-style polyline or a block) can be created by making multiple calls to entmake, using a separate call for each subentity.

When entmake first receives an initial component for a complex entity, it creates a temporary file in which to gather the definition data and extended data, if present. For each subsequent entmake call, the function checks if the temporary file exists. If it does, the new subentity is appended to the file. When the definition of the complex entity is complete (that is, when entmake receives an appropriate Seqend or Endblk subentity), the entity is checked for consistency; if valid, it is added to the drawing. The file is deleted when the complex entity is complete or when its creation has been canceled. You can cancel the creation of a complex entity by entering entmake with no arguments. This clears the temporary file and returns nil.

No portion of a complex entity is displayed in a drawing until its definition is complete; that is not until the final Seqend or Endblk subentity has been passed to entmake. The entlast function cannot retrieve the most recently created subentity for a complex entity that has not been completed.

As the previous paragraphs imply, entmake can construct only one complex entity at a time. If a complex entity is being created and entmake receives invalid data or an entity that is not an appropriate subentity, both the invalid entity and the entire complex entity are rejected.

Complex entities can exist in either model space or paper space, but not both. If you have changed the current space by invoking either of the AutoCAD MSPACE or PSPACE commands (with command) while a complex entity is being constructed, a subsequent call to entmake cancels the complex entity. This can also occur if the subentity has a 67 dxf group code whose value does not match the 67 dxf group code of the entity header.

The following example contains five calls to the entmake function which creates a single complex entity, an old-style polyline. The polyline has three vertices located at coordinates (1,1,0), (4,6,0), and (3,2,0), and has a linetype of DASHED and a color of BLUE. All other optional definition data assume default values.

Note: For the previous example code to execute properly, the linetype DASHED must be loaded.

When defining dotted pairs, as in the above example, there must be a space on both sides of the dot. Otherwise, you will get an invalid dotted pair error message. If you want to use values stored in variables to create a dotted pair, you must use the list and cons functions instead of using the quote ( ‘ ) function.

For example, the following code sets the color and linetype for the polyline object from values to red and dashed using variables:

Old-style polyline entities always include a vertices-follow flag (also dxf group code 66). The value of this flag must be 1, and the flag must be followed by a sequence of vertex entities, terminated by a Seqend subentity.

1『Old-style polyline 的代码没有实现成功，问题待解决。』

Applications can represent polygons with an arbitrarily large number of sides in polyface meshes. However, the AutoCAD entity structure imposes a limit on the number of vertices that a given face entity can specify. You can represent more complex polygons by dividing them into triangular wedges. AutoCAD represents triangular wedges as four-vertex faces where two adjacent vertices have the same value. Their edges should be made invisible to prevent visible artifacts of this subdivision from being drawn. The AutoCAD PFACE command performs this subdivision automatically, but when applications generate polyface meshes directly, the applications must do this themselves.

The number of vertices per face is the key parameter in this subdivision process. The AutoCAD PFACEVMAX system variable provides an application with the number of vertices per face entity. This value is read-only and is set to 4.

Block definitions begin with a block entity and end with an Endblk subentity. Newly created blocks are automatically entered into the symbol table where they can be referenced. Block definitions cannot be nested, nor can they reference themselves. A block definition can contain references to other block definitions.

Note: Before you use entmake to create a block, you should use tblsearch to ensure that the name of the new block is unique. The entmake function does not check for name conflicts in the block definitions table, so you could inadvertently redefine an existing block.

Block references can include an attributes-follow flag (dxf group code 66). If present and equal to 1, a series of attribute (Attrib) entities is expected to follow the Insert object. The attribute sequence is terminated by a Seqend subentity.

There is no direct method for an application to check whether a block listed in the BLOCK table is actually referenced by an insert object in the drawing. You can use the following code to scan the drawing for instances of a block reference:

    (ssget "x" '((2 . "BLOCKNAME")))

You must also scan each block definition for instances of nested blocks.

The block definitions (BLOCK) table in a drawing can contain anonymous blocks (also known as unnamed blocks), that AutoCAD creates to support dynamic blocks, tables, hatch patterns, and associative dimensions.

The entmake function can create anonymous blocks other than * Tnnn (tables), * Dnnn (dimensions), and *Xnnn (hatch patterns). Unreferenced anonymous blocks are purged from the BLOCK definition table when a drawing is opened. Referenced anonymous blocks (those that have been inserted) are not purged. You can use entmake to create a block reference (insert object) to an anonymous block. (You cannot pass an anonymous block to the INSERT command.) Also, you can use entmake to redefine the block. You can modify the entities in a block (but not the block object itself) with entmod.

The name (dxf group code 2) of an anonymous block created by AutoLISP, ObjectARX, or Managed .NET has the form *Unnn, where nnn is a number generated by AutoCAD. Also, the low-order bit of an anonymous block's block type flag (dxf group code 70) is set to 1. When entmake creates a block whose name begins with * and whose anonymous bit is set, AutoCAD treats this as an anonymous block and assigns it a name. Any characters following the * in the name string passed to entmake are ignored.

Note: Anonymous block names do not remain constant. Although a referenced anonymous block becomes permanent, the numeric portion of its name can change between drawing sessions.

The entget function returns the definition data of a specified entity as a list. Each item in the list is specified by a DXF group code. The first item in the list contains the entity's current name.

The -1 item at the start of the list contains the name of the entity. The entmod function, which is described in this section, uses the name to identify the entity to be modified. The individual dotted pairs that represent the values can be extracted by using assoc with the cdr function.

Sublists for points are not represented as dotted pairs like the rest of the values returned. The convention is that the cdr of the sublist is the group code's value. Because a point is a list of two or three reals, the entire group is a three- (or four-) element list. The cdr of the group code value is the list representing the point, so the convention that cdr always returns the value is preserved.

The group codes for the components of the entity are those used by DXF. As with DXF, the entity header items (color, linetype, thickness, the attributes-follow flag, and the entity handle) are returned only if they have values other than the default. Unlike DXF, optional entity definition fields are returned whether or not they equal their defaults and whether or not associated X, Y, and Z coordinates are returned as a single point variable, rather than as separate X (10), Y (20), and Z (30) group codes.

All points associated with an object are expressed in terms of that object's Object Coordinate System (OCS). For point, line, 3D line, 3D face, 3D polyline, 3D mesh, and dimension objects, the OCS is equivalent to the WCS (the object points are World points). For all other objects, the OCS can be derived from the WCS and the object's extrusion direction (its 210 group code). When working with objects that are drawn using coordinate systems other than the WCS, you may need to convert the points to the WCS or to the current UCS by using the trans function.

When writing functions to process entity lists, make sure the function logic is independent of the order of the sublists; use assoc to guarantee this. The assoc function searches a list for a group code of a specified type. The following code returns the object type "LINE" (0) from the list entl.

    (cdr (assoc 0 entl))

If the group code specified is not present in the list (or if it is not a valid group code), assoc returns nil.

Caution: Before performing an entget on vertex entities, you should read or write the polyline entity's header. If the most recently processed polyline entity is different from the one to which the vertex belongs, width information (the 40 and 41 group codes) can be lost.

Entities can be deleted using the entdel function or AutoCAD ERASE command (with command).

Entities are not purged from the database until the end of the current drawing session, so if the application calls entdel on an entity that was deleted during that session, the entity is undeleted.

Attributes and old-style polyline vertices cannot be deleted independently of their parent entities. The entdel function and AutoCAD ERASE command only operate on main entities. If you need to delete an attribute or vertex, you can use the AutoCAD ATTEDIT or PEDIT commands with command.

An entity can be modified directly by changing its entity list and posting the changes back to the database.

The entmod function modifies an entity by passing it a list in the same format as a list returned by entget but with some of the entity group code values (presumably) modified by the application. This function complements entget. The primary mechanism by which an AutoLISP application updates the database is by retrieving an entity with entget, modifying its entity list, and then passing the list back to the database with entmod.

The following example code retrieves the definition data of the first entity in the drawing and changes its layer property to MYLAYER.

1『一个非常重要的关键点是，entity list 里各个属性对应的关键词，比如 "图层" 对应的是数字 8。』

There are restrictions on the changes to the database that entmod can make; entmod cannot change the following:

1. The entity's type or handle.

2. Internal fields. (Internal fields are the values that AutoCAD assigns to certain group codes: -2, entity name reference; -1, entity name; 5, entity handle.) Any attempt to change an internal field—for example, the main entity name in a Seqend subentity (group code -2)—is ignored.

3. Viewport entities. An attempt to change a viewport entity causes an error.

Other restrictions apply when modifying dimensions and hatch patterns.

AutoCAD must recognize all objects (except layers) that the entity list refers to. The name of any text style, linetype, shape, or block that appears in an entity list must be defined in the current drawing before the entity list is passed to entmod. The one exception is that entmod accepts new layer names. If the entity list refers to a layer name that has not been defined in the current drawing, entmod creates a new layer. The attributes of the new layer are the standard default values used by the New option of the AutoCAD LAYER command.

The entmod function can modify subentities such as polyline vertices and block attributes. If you use entmod to modify an entity in a block definition, this affects all references to that block which exist in model space and paper space. Attributes, unless defined as constant, are not updated for each block reference that exists in a drawing. Also, entities in block definitions cannot be deleted by entdel.

1『上面是有关块属性的信息，对后面要做的提前块内信息的操作应该很有用。』

The handent function retrieves the name of an entity with a specific handle.

As with entity names, handles are unique within a drawing. However, an entity's handle is constant throughout its life. AutoLISP applications that manipulate a specific database can use handent to obtain the current name of an entity they must use. You can use the AutoCAD LIST command to get the handle of a selected object.

The following example code uses handent to obtain and display the entity name that is associated with the handle “5a2”.

In another editing session with the same drawing, the fragment might display an entirely different number. But in both cases the code would be accessing the same entity.

The handent function has an additional use. Entities can be deleted from the database with entdel. The entities are not purged until the current drawing ends. This means that handent can recover the names of deleted entities, which can then be restored to the drawing by a second call to entdel.

Note: Handles are provided for block definitions, including subentities.

Entities in drawings that are cross-referenced by way of XREF Attach are not actually part of the current drawing; their handles are unchanged but cannot be accessed by handent. However, when drawings are combined by means of INSERT, INSERT *, XREF Bind (XBIND), or partial DXFIN, the handles of entities in the incoming drawing are lost, and incoming entities are assigned new handle values to ensure each handle in the current drawing remains unique.

Changes to the drawing made by the entity data functions are reflected on the graphics screen, provided the entity being deleted, undeleted, modified, or created is in an area and on a layer that is currently visible.

There is one exception; when entmod modifies a subentity, it does not update the image of the entire (complex) entity. If, for example, an application modifies 100 vertices of an old-style polyline with 100 calls to entmod, the time required to recalculate and redisplay the entire polyline is unacceptably slow. Instead, an application can perform a series of subentity modifications, and then redisplay the entire entity with a single call to the entupd function.

The argument to entupd can specify either a main entity or a subentity. In either case, entupd regenerates the entire entity. Although its primary use is for complex entities, entupd can regenerate any entity in the current drawing.

Note: To ensure that all instances of the block references are updated, you must regenerate the drawing by invoking the AutoCAD REGEN command (with command). The entupd function is not sufficient if the modified entity is in a block definition.

A drawing database contains two types of non-graphical objects: dictionary and symbol table objects.

Although there are similarities between these object types, they are handled differently. All object types are supported by the entget, entmod, entdel, and entmake functions, although object types individually dictate their participation in these functions and may refuse any or all processing. With respect to AutoCAD built-in objects, the rules apply for symbol tables and for dictionary objects.

All rules and restrictions that apply to graphical objects apply to non-graphical objects as well. Non-graphical objects cannot be passed to the entupd function. When using entmake, the object type determines where the object will reside. For example, if a layer object is passed to entmake, it automatically goes to the layer symbol table. If a graphical object is passed to entmake, it will reside in the current space (model or paper).

Several AutoLISP functions are provided to handle extended data (xdata), which is created by routines written with AutoLISP, ObjectARX, or Managed .NET.

If an entity contains xdata, it follows the entity's regular definition data. You can retrieve an entity's extended data by calling entget. The entget function retrieves an entity's regular definition data and the xdata for those applications specified in the entget call.

When xdata is retrieved with entget, the beginning of extended data is indicated by a -3 dxf group code. The -3 dxf group code is in a list that precedes the first 1001 dxf group code. The 1001 dxf group code contains the application name of the first application retrieved, as shown in the table and as described in the topics in this section.

1『dxf group code 实在是太重要了。』

Extended data consists of one or more 1001 group codes, each of which begin with a unique application name.

The xdata groups returned by entget follow the definition data in the order in which they are saved in the database. Within each application's group, the contents, meaning, and organization of the data are defined by the application. AutoCAD maintains the information but does not use it. The table also shows that the group codes for xdata are in the range 1000-1071. Many of these group codes are for familiar data types, as follows:

An application must register its name or names to be recognized by AutoCAD.

Extended data must contain an application name before it can be attached to an entity and that application name must also exist in the APPID symbol table. Registration is done with the regapp function, which specifies a string to use as an application name. If it successfully adds the name to APPID, it returns the name of the application; otherwise it returns nil. A result of nil indicates that the name is already present in the symbol table. This is not an actual error condition but an expected return value, because the application name needs to be registered only once per drawing.

Before you register an application, you should first check to see if the name is not already in the APPID symbol table. If the name is not there, the application must register it. Otherwise, it can simply go ahead and attach the extended data to an entity for the application.

An application can obtain the extended data (xdata) that it has attached to an entity with entget.

The entget function can return an entity’s definition data and the xdata for the applications it requests. It requires an additional argument, application, that specifies the application names. The names passed to entget must correspond to applications registered by a previous call to regapp; they can also contain wild-card characters.

By default, associative hatch patterns contain xdata. The following example code demonstrates the association list of this xdata. Before you can use the code, create a closed boundary and apply an associative hatch object to the boundary.

You can use extended data (xdata) to store any type of information you want on an entity.

The xdata attached to an entity might be a record in an external database, a date and time stamp when an entity was added or modified, or contain information that represents an item in the real-world such as a telephone or workstation. Since xdata is hidden from the user, it makes it harder to modify without using a custom application.

Note: Xdata attached to an entity is maintained when an object is copied in the current drawing or between drawings.

The following example code demonstrates the basics of attaching xdata to the last entity added to a drawing. Before executing the following example code, draw an entity (such as a line or a circle):

Extended data is limited to 16K per entity.

Because the xdata of an entity can be created and maintained by multiple applications, problems can result when the size of the xdata approaches its limit. The following functions can be used to help manage the memory that xdata occupies.

xdsize - Returns the amount of memory (in bytes) that the xdata in a list occupies.

xdroom - Returns the remaining number of free bytes that can still be appended to the entity.

The xdsize function can be slow when reading a large extended data list, so it is not recommended that you call it frequently. A better approach is to use it (in conjunction with xdroom) in an error handler. If a call to entmod fails, you can use xdsize and xdroom to find out whether the call failed because the entity did not have enough room for the xdata.

Extended data can contain handles (dxf group code 1005) to save relational structures within a drawing.

This allows you to build relationships between two or more entities by saving the handle of one object to another objects’s xdata. The handle can be retrieved later from the xdata and passed to handent to obtain the other entity. Because more than one entity can reference another, handles in xdata might not necessarily be unique. The AutoCAD AUDIT command does require that handles in extended data either be NULL or valid entity handles (within the current drawing). The best way to ensure that xdata entity handles are valid is to obtain a referenced entity's handle directly from its definition data by means of entget. The handle value is in dxf group code 5.

Xrecord objects are used to store and manage arbitrary data.

They are composed of DXF group codes with normal object group codes (that is, non-xdata group codes), ranging from 1 through 369 for supported ranges. These objects are similar in concept to xdata but are not limited by size or order.

The following code examples create and list xrecord data in a custom dictionary named XRECLIST.

AutoLISP provides functions for accessing symbol table and dictionary entries. Examples of the tblnext and tblsearch functions are provided in the following sections. For a complete list of the symbol table and dictionary access functions, see About Symbol Table and Dictionary-Handling Functions (AutoLISP) in the AutoLISP Function Synopsis (AutoLISP) topic.

For additional information on non-graphic objects see, About Non-Graphic Object Handling (AutoLISP).

Symbol tables are used to store non-graphical information in a drawing’s database. The symbol tables that exist in a drawing database are:

Symbol table entries can be manipulated using the following functions:

1. tblobjname - Returns the entity name of a specified symbol table entry.

2. tblsearch - Searches a symbol table for a symbol name.

3. tblnext - Returns the next item in a symbol table.

4. entdel - Deletes objects (entities) or restores previously deleted objects.

5. entget - Retrieves an object's (entity's) definition data list.

6. entmake - Creates a new entity in the drawing.

7. entmod - Modifies the definition data of an object (entity).

8. handent - Returns an object (entity) name based on its handle.

The following rules apply to symbol tables:

1. Symbol table entries can be created using entmake with a few restrictions, other than being valid record representations, and name conflicts can only occur in the VPORT table. *ACTIVE entries cannot be created.

2. Renaming symbol table entries to duplicate names is not acceptable, except for the VPORT symbol table.

3. Symbol table entries cannot be deleted with entdel.

4. The object states of symbol tables and symbol table entries may be accessed with entget by passing the entity name. The tblobjname function can be used to retrieve the entity name of a symbol table entry.

5. Symbol tables themselves cannot be created with entmake; however, symbol table entries can be created with entmake.

6. Handle group codes (5, 105) cannot be changed in entmod, nor specified in entmake.

7. Symbol table entries that are not in the APPID symbol table can have many of their fields modified with entmod. Modifying a symbol table record list must include its entity name, which can be obtained from entget but not from the tblsearch and tblnext functions. The 70 group code of symbol table entries is ignored in entmod and entmake operations.

The tblnext function sequentially scans symbol table entries, and the tblsearch function retrieves specific entries. Symbol table names are specified by strings. Both functions return lists with DXF group codes that are similar to the entity data returned by entget.

The first call to tblnext returns the first entry in the specified symbol table. Subsequent calls that specify the same table return successive entries, unless the second argument to tblnext (rewind) is nonzero, in which case tblnext returns the first entry again.

In the following example code, the function GETBLOCK retrieves the symbol table entry for the first block (if any) in the current drawing, and then displays it in a list format.

Entries retrieved from the BLOCK table contain a -2 group code that contains the name of the first entity in the block definition. If the block is empty, this is the name of the block's Endblk entity, which is never seen on occupied blocks. In a drawing with a single block named BOX, a call to GETBLOCK displays the following. (The name value varies from session to session.)

As with tblnext, the first argument to tblsearch is a string that names a symbol table, but the second argument is a string that names a particular symbol table entry in the table. If the symbol table entry is found, tblsearch returns its data. This function has a third argument, setnext, that you can use to coordinate operations with tblnext. If setnext is nil, the tblsearch call has no effect on tblnext, but if setnext is non-nil, the next call to tblnext returns the symbol table entry following the symbol table entry found by tblsearch.

The setnext option is useful when you are handling the VPORT symbol table, because all viewports in a particular viewport configuration have the same name (such as *ACTIVE). If the VPORT symbol table is accessed when the AutoCAD TILEMODE system variable is turned off, any changes have no visible effect until TILEMODE is turned on. Do not confuse VPORTS, which is described by the VPORT symbol table with paper space viewport entities.

A dictionary is a container object, similar to symbol tables.

Dictionaries are stored in the drawing’s named object dictionary, which is the root of all non-graphical objects in a drawing, or as an extension dictionary attached to an object. Each drawing can contain different dictionaries, so a routine should not expect that a specific dictionary might exist in a drawing. The dictionaries in a drawing’s named object dictionary can be accessed using namedobjdict, which returns an entity name. Use entget to access the entity list that represents all of the dictionaries in the drawing.

The following rules apply to dictionary objects:

1. Dictionary objects can be examined with entget and their xdata modified with entmod. Their entries cannot be altered with entmod. All access to their entries are made through the dictsearch and dictnext functions.

2. Dictionary entry contents cannot be modified through entmod, although xdata can be modified.

3. Dictionary entries that begin with ACAD* cannot be renamed.

Dictionary entries can be queried with the dictsearch and dictnext functions. Each dictionary entry consists of a text name key plus a hard ownership handle reference to the entry object. Dictionary entries may be removed by directly passing entry object names to the entdel function. The text name key uses the same syntax and valid characters as symbol table names. A key name can be changed using the dictrename function.

The following example code lists each of the dictionaries in the drawing’s named object dictionary and their entries:









