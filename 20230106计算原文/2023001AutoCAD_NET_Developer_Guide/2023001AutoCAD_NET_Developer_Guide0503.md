## 0501. Create and Edit AutoCAD Entities (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

### 5.2 Work With Selection Sets (.NET)

A selection set can consist of a single object, or it can be a more complex grouping: for example, the set of objects on a certain layer.

A selection set is typically created by requesting a user to select an object in the drawing area before a command is started through pick first selection or at the Select objects: prompt when a command is active. Selection sets are not persistent objects, if you need to maintain a selection set for use between multiple commands or future use, you will need to create a custom dictionary and record the ObjectIds found in the selection set as soft pointers in dictionary records.

As an alternatively to storing ObjectIds as soft pointers, you could store each objects handle in the dictionary. You would then use the Database.GetObjectId method to get an object's ObjectId from the stored handle.

Note: Whether you store an ObjectId as a soft pointer or a handle in a dictionary, you will want to make sure the object exists before accessing it.

Prompts and Selection Filters

The management of selection sets is split across multiple objects that are part of the Autodesk.AutoCAD.EditorInput namespace. You use the Editor object to prompt the user for a selection, and to perform the selection action. The PromptSelectionOptions object is used to configure the prompt that will be displayed to the user when the selection operation begins, and the SelectionFilter class can be used to filter a selection set by entity properties.

The PromptSelectionOptions class provides a SetKeywords method for specifying prompt keywords, as well as MessageForAdding and MessageForRemoval properties for configuring the prompt message. The SelectionFilter class accepts filter parameters in the form of an array of TypedValue objects, as described in the "ResultBuffer Data Type (.NET)" topic. Each TypedValue object represents a single filter condition. Any number of conditions may be specified for a selection.

When your application is ready to prompt for the selection, you call the GetSelection method on the Editor object. The Editor.GetSelection method exists in a number of overloaded versions. For a simple, unfiltered selection using the standard AutoCAD prompt, you use the no-parameter overload. For cases where you want to provide custom prompt messages, including keywords, you use an overload that accepts a PromptSelectionOptions object. To specify a filter, use an overload that accepts a SelectionFilter object.

Other selection methods cover the full range of selection modes available in the AutoCAD program. The Editor.SelectImplied method provides access to the implied, or pick-first, selection set. The Editor.SelectPrevious method returns the objects selected in the previous selection set. Methods such as SelectCrossingWindow and SelectFence let applications select entities by window, crossing, fence, and polygon.