## 0401. Control the AutoCAD Environment (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

This chapter describes the fundamentals for developing an application that runs in-process with AutoCAD. It explains many of the concepts to control and work effectively with the AutoCAD environment.

### 4.1 Control the Application Window (.NET)

The ability to control the Application window allows developers the flexibility to create effective and intelligent applications. There will be times when it is appropriate for your application to minimize the AutoCAD window, perhaps while your code is performing work in another application such as Microsoft® Excel®. Additionally, you will often want to verify the state of the AutoCAD window before performing such tasks as prompting for input from the user.

Using methods and properties found on the Application object, you can change the position, size, and visibility of the Application window. You can also use the WindowState property to minimize, maximize, and check the current state of the Application window.

Position and size the Application window

This example uses the Location and Size properties to position the AutoCAD Application window in the upper-left corner of the screen and size it to 400 pixels wide by 400 pixels high.

Note: The following examples require that the PresentationCore (PresentationCore.dll) library to be referenced to the project. Use the Add Reference dialog box and select PresentationCore from the .NET tab.

```cs
using System.Drawing;
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
 
[CommandMethod("PositionApplicationWindow")]
public static void PositionApplicationWindow()
{
    // Set the position of the Application window
    System.Windows.Point ptApp = new System.Windows.Point(0, 0);
    Autodesk.AutoCAD.ApplicationServices.Application.MainWindow.DeviceIndependentLocation = ptApp;

    // Set the size of the Application window
    System.Windows.Size szApp = new System.Windows.Size(400, 400);
    Autodesk.AutoCAD.ApplicationServices.Application.MainWindow.DeviceIndependentSize = szApp;
}
```

Minimize and maximize the Application window

Note: The following examples require that the PresentationCore (PresentationCore.dll) library to be referenced to the project. Use the Add Reference dialog box and select PresentationCore from the .NET tab.

```cs
using System.Drawing;
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.Windows;
 
[CommandMethod("MinMaxApplicationWindow")]
public static void MinMaxApplicationWindow()
{
    //Minimize the Application window
    Application.MainWindow.WindowState = Window.State.Minimized;


    System.Windows.Forms.MessageBox.Show("Minimized", "MinMax",
                System.Windows.Forms.MessageBoxButtons.OK,
                System.Windows.Forms.MessageBoxIcon.None,
                System.Windows.Forms.MessageBoxDefaultButton.Button1,
                System.Windows.Forms.MessageBoxOptions.ServiceNotification);

    //Maximize the Application window
    Application.MainWindow.WindowState = Window.State.Maximized;
    System.Windows.Forms.MessageBox.Show("Maximized", "MinMax");
}
```

Find the current state of the Application window

This example queries the state of the Application window and displays the state in a message box to the user.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.Windows;
 
[CommandMethod("CurrentWindowState")]
public static void CurrentWindowState()
{
    System.Windows.Forms.MessageBox.Show("The application window is " +
                                            Application.MainWindow.WindowState.ToString(), 
                                            "Window State");
}
```

Make the Application window invisible and visible

The following code uses the Visible property to make the AutoCAD application window invisible and then visible again.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.Windows;
 
[CommandMethod("HideWindowState")]
public static void HideWindowState()
{
    //Hide the Application window
    Application.MainWindow.Visible = false;
    System.Windows.Forms.MessageBox.Show("Invisible", "Show/Hide");

    //Show the Application window
    Application.MainWindow.Visible = true;
    System.Windows.Forms.MessageBox.Show("Visible", "Show/Hide");
}
```

