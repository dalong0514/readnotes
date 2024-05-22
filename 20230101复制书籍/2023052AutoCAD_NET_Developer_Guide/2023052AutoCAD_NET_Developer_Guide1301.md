## 1301. ResultBuffer Data Type (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

The ResultBuffer type is a class that mirrors the resbuf struct defined in the ObjectARX SDK. The resbuf struct provides a flexible container for AutoCAD-specific data.

An Autodesk.AutoCAD.DatabaseServices.ResultBuffer class object is used in much the same way as a resbuf chain. You define a ResultBuffer and populate it with a sequence of data pairs. Each pair contains a data type description and a value. In the managed API, these data pairs are instances of the Autodesk.AutoCAD.DatabaseServices.TypedValue class. This utility class serves the same purpose as the restype and resval members of the resbuf struct.

The TypedValue.TypeCode property is a 16-bit integer value that indicates the TypedValue.Value property's data type. Acceptable TypeCode values depend on the specific use of a ResultBuffer instance. For example, TypeCode values that are suitable for an xrecord definition are not necessarily appropriate for xdata. The Autodesk.AutoCAD.DatabaseServices.DxfCode enum defines codes that accurately describe the full range of possible ResultBuffer data types.

The TypedValue.Value property maps to an instance of System.Object, and theoretically may contain any type of data. However, the Value data must conform to the type indicated by TypeCode to guarantee usable results.

You can prepopulate a ResultBuffer by passing an array of TypedValue objects to its constructor, or you can construct an empty ResultBuffer and later call the ResultBuffer::Add() method to append new TypedValue objects. The following example shows a typical ResultBuffer constructor usage:

```cs
using (Xrecord rec = new Xrecord())
{
    rec.Data = new ResultBuffer(
        new TypedValue(Convert.ToInt32(DxfCode.Text), "This is a test"),
        new TypedValue(Convert.ToInt32(DxfCode.Int8), 0),
        new TypedValue(Convert.ToInt32(DxfCode.Int16), 1),
        new TypedValue(Convert.ToInt32(DxfCode.Int32), 2),
        new TypedValue(Convert.ToInt32(DxfCode.HardPointerId), db.BlockTableId),
        new TypedValue(Convert.ToInt32(DxfCode.BinaryChunk), new byte[] {0, 1, 2, 3, 4}),
        new TypedValue(Convert.ToInt32(DxfCode.ArbitraryHandle), db.BlockTableId.Handle),
        new TypedValue(Convert.ToInt32(DxfCode.UcsOrg),
        new Point3d(0, 0, 0)));
}
```
