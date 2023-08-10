## 0501. Create and Edit AutoCAD Entities (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

You can create a range of objects, from simple lines and circles to spline curves, ellipses, and associative hatch areas. In general, you add objects to a BlockTableRecord object using the AppendEntity function. Once an object is created, you can change its properties such as layer, color, and linetype.

The drawing database is similar to other database programs, you can think of a Line object in Model space as table record and Model space as its database table. When working with a database, you must open and close records before working with them. The objects stored in the Database object are no different, you use the GetObject function to retrieve an object from the database and define how you want to work with the object.

### 5.1 Open and Close Objects (.NET)

Whether you are working with objects such as lines, circles and polyline or a symbol table and its records, you need to open the object for read or write. When querying an object you want to open the object for read, but if you are going to make changes to the object you will want to open it for write.

