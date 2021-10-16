## 0201. The Java Programming Environment

In this chapter:

2.1 Installing the Java Development Kit

2.2 Using the Command-Line Tools

2.3 Using an Integrated Development Environment

2.4 JShell

In this chapter, you will learn how to install the Java Development Kit (JDK) and how to compile and run various types of programs: console programs, graphical applications, and applets. You can run the JDK tools by typing commands in a terminal window. However, many programmers prefer the comfort of an integrated development environment. You will learn how to use a freely available development environment to compile and run Java programs. Once you have mastered the techniques in this chapter and picked your development tools, you are ready to move on to Chapter 3, where you will begin exploring the Java programming language.

0201 Java 程序设计环境

本章主要介绍如何安装 Java 开发工具包（JDK）以及如何编译和运行不同类型的程序：控制台程序、图形化应用程序以及 applet。运行 JDK 工具的方法是在终端窗口中键入命令。然而，很多程序员更喜欢使用集成开发环境。为此，将在稍后介绍如何使用免费的开发环境编译和运行 Java 程序。尽管学起来很容易，但集成开发环境需要吞噬大量资源，编写小型程序时也比较烦琐。一旦掌握了本章的技术，并选定了自己的开发工具，就可以学习第 3 章，开始研究 Java 程序设计语言。

### 2.1 Installing the Java Development Kit

The most complete and up-to-date versions of the Java Development Kit (JDK) are available from Oracle for Linux, Mac OS, Solaris, and Windows. Versions in various states of development exist for many other platforms, but those versions are licensed and distributed by the vendors of those platforms.

2.1 安装 Java 开发工具包

Oracle 公司为 Linux、Mac OS X、Solaris 和 Windows 提供了 Java 开发工具包（JDK）的最新、最完整的版本。用于很多其他平台的版本仍处于多种不同的开发状态中，不过，这些版本都由相应平台的开发商授权并分发。

#### 2.1.1 Downloading the JDK

To download the Java Development Kit, visit the web site at www.oracle.com/technetwork/java/javase/downloads and be prepared to decipher an amazing amount of jargon before you can get the software you need. See Table 2.1 for a summary.

Table 2.1 Java Jargon

| Name | Acronym | Explanation |
| --- | --- | --- |
| Java Development Kit | JDK | The software for programmers who want to write Java programs |
| Java Runtime Environment | JRE | The software for consumers who want to run Java programs |
| Server JRE | — | The software for running Java programs on servers |
| Standard Edition | SE | The Java platform for use on desktops and simple server applications |
| Enterprise Edition | EE | The Java platform for complex server applications |
| Micro Edition | ME | The Java platform for use on small devices |
| JavaFX | — | An alternate toolkit for graphical user interfaces that is included with certain Java SE distributions prior to Java 11 |
| OpenJDK | — | A free and open source implementation of Java SE |
| Java 2 | J2 | An outdated term that described Java versions from 1998 until 2006 |
| Software Development Kit | SDK | An outdated term that described the JDK from 1998 until 2006 |
| Update | u | Oracle's term for a bug fix release up to Java 8 |
| NetBeans | — | Oracle's integrated development environment |

You already saw the abbreviation JDK for Java Development Kit. Somewhat confusingly, versions 1.2 through 1.4 of the kit were known as the Java SDK (Software Development Kit). You will still find occasional references to the old term. Up to Java 10, there is also a Java Runtime Environment (JRE) that contains only the virtual machine. That is not what you want as a developer. It is intended for end users who have no need for the compiler.

Next, you'll see the term Java SE everywhere. That is the Java Standard Edition, in contrast to Java EE (Enterprise Edition) and Java ME (Micro Edition).

You might run into the term Java 2 that was coined in 1998 when the marketing folks at Sun felt that a fractional version number increment did not properly communicate the momentous advances of JDK 1.2. However, since they had that insight only after the release, they decided to keep the version number 1.2 for the development kit. Subsequent releases were numbered 1.3, 1.4, and 5.0. The platform, however, was renamed from Java to Java 2. Thus, we had Java 2 Standard Edition Software Development Kit Version 5.0, or J2SE SDK 5.0.

Fortunately, in 2006, the numbering was simplified. The next version of the Java Standard Edition was called Java SE 6, followed by Java SE 7 and Java SE 8.

However, the「internal」version numbers are 1.6.0, 1.7.0, and 1.8.0. This minor madness finally ran its course with Java SE 9, when the version number became 9, and then 9.0.1. (Why not 9.0.0 for the initial version? To keep a modicum of excitement, the version number specification requires that trailing zeroes are dropped for the fleeting interval between a major release and its first security update.)

Note

For the remainder of the book, we will drop the「SE」acronym. When you see「Java 9」, that means「Java SE 9」.

Prior to Java 9, there were 32-bit and 64-bit versions of the Java Development Kit. The 32-bit versions are no longer developed by Oracle. You need to have a 64-bit operating system to use the Oracle JDK.

With Linux, you have a choice between an RPM file and a .tar.gz file. We recommend the latter—you can simply uncompress it anywhere you like.

Now you know how to pick the right JDK. To summarize:

You want the JDK (Java SE Development Kit), not the JRE.

Linux: Pick the .tar.gz version.

Accept the license agreement and download the file.

Note

Depending on the constellation of the planets, Oracle may offer you a bundle that contains both the Java Development Kit and the NetBeans integrated development environment. I suggest that you stay away from all bundles and install only the Java Development Kit at this time. If you later decide to use NetBeans, simply download it from http://netbeans.org.

2.1.1 下载 JDK

要想下载 Java 开发工具包，可以访问 Oracle 网站：www.oracle.com/technetwork/java/javase/downloads，在得到所需的软件之前必须弄清楚大量专业术语。请看表 2-1 的总结。

表 2-1 Java 术语

你已经看到，JDK 是 Java Development Kit 的缩写。有点混乱的是：这个工具包的版本 1.2-1.4 被称为 Java SDK（软件开发包，Software Development Kit）。在某些场合下，还可以看到这个过时的术语。另外，还有一个术语是 Java 运行时环境（JRE），它包含虚拟机但不包含编译器。这并不是开发者想要的环境，而是专门为不需要编译器的用户而提供。

接下来，Java SE 会大量出现，相对于 Java EE（Enterprise Edition）和 Java ME（MicroEdition），它是 Java 的标准版。

Java 2 这种提法始于 1998 年。当时 Sun 公司的销售人员感觉增加小数点后面的数值改变版本号并没有反映出 JDK 1.2 的重大改进。但是，由于在发布之后才意识到这个问题，所以决定开发工具包的版本号仍然沿用 1.2，接下来的版本是 1.3、1.4 和 5.0。但是，Java 平台被重新命名为 Java 2。因此，就有了 Java 2 Standard Edition Software Development Kit（Java 2 标准版软件开发包）的 5.0 版，即 J2SE SDK 5.0。幸运的是，2006 年版本号得到简化。Java 标准版的下一个版本取名为 Java SE 6，后来又有了 Java SE7 和 Java SE 8。不过，「内部」版本号分别是 1.6.0、1.7.0 和 1.8.0。

幸运的是，2006 年版本号得到简化。Java 标准版的下一个版本取名为 Java SE 6，后来又有了 Java SE7 和 Java SE 8。不过，「内部」版本号分别是 1.6.0、1.7.0 和 1.8.0。

当 Oracle 为解决一些紧急问题做出某些微小的版本改变时，将其称为更新。例如：Java SE 8u31 是 Java SE 8 的第 31 次更新，它的内部版本号是 1.8.0_31。更新不需要安装在前一个版本上，它会包含整个 JDK 的最新版本。另外，并不是所有更新都公开发布，所以如果「更新 31」之后没有「更新 32」，你也不用惊慌。

对于 Windows 或 Linux，需要在 x86（32 位）和 x64（64 位）版本之间做出选择。应当选择与你的操作系统体系结构匹配的版本。

对于 Linux，还可以在 RPM 文件和.tar.gz 文件之间做出选择。我们建议使用后者，可以在你希望的任何位置直接解压缩这个压缩包。现在你已经了解了如何选择适当的 JDK。下面做一个小结：

1、你需要的是 JDK（Java SE 开发包），而不是 JRE。

2、Windows 或 Linux：32 位选择 x86，64 位以 x64。

3、Linux：选择.tar.gz 版本。接受许可协议，然后下载文件。

注释：Oracle 提供了一个捆绑包，其中包含 Java 开发包（JDK）和 NetBeans 集成开发环境。建议现在不要安装任何捆绑包，而只需安装 Java 开发包。如果以后你打算使用 NetBeans，可以再从 http://netbeans.org 下载。

#### 2.1.2 Setting up the JDK

After downloading the JDK, you need to install it and figure out where it was installed—you'll need that information later.

Under Windows, launch the setup program. You will be asked where to install the JDK. It is best not to accept a default location with spaces in the path name, such as c:\Program Files\Java\jdk-11.0.x. Just take out the Program Files part of the path name.

On the Mac, run the installer. It installs the software into /Library/Java /JavaVirtualMachines/jdk-11.0.x.jdk/Contents/Home. Locate it with the Finder.

On Linux, simply uncompress the .tar.gz file to a location of your choice, such as your home directory or /opt. Or, if you installed from the RPM file, double-check that it is installed in /usr/java/jdk-11.0.x.

In this book, the installation directory is denoted as jdk. For example, when referring to the jdk/bin directory, I mean the directory with a name such as /opt/jdk-11.0.4/bin or c:\Java\jdk-11.0.4\bin.

When you install the JDK on Windows or Linux, you need to carry out one additional step: Add the jdk/bin directory to the executable path—the list of directories that the operating system traverses to locate executable files.

On Linux, add a line such as the following to the end of your ~/.bashrc or ~/.bash_profile file:

Click here to view code image

export PATH=jdk/bin:`$`PATH

Be sure to use the correct path to the JDK, such as /opt/jdk-11.0.4.

Under Windows 10, type「environment」into the search bar of the Windows Settings, and select「Edit environment variables for your account」(see Figure 2.1). An Environment Variables dialog should appear. (It may hide behind the Windows Settings dialog. If you can't find it anywhere, try running sysdm.cpl from the Run dialog that you get by holding down the Windows and R key at the same time, and then select the Advanced tab and click the Environment Variables button.) Locate and select a variable named Path in the User Variables list. Click the Edit button, then the New button, and add an entry with the jdk\bin directory (see Figure 2.2).

Figure 2.1 Setting system properties in Windows 10

Figure 2.2 Setting the Path environment variable in Windows 10

Save your settings. Any new「Command Prompt」windows that you start will have the correct path.

Here is how you test whether you did it right: Start a terminal window. Type the line

```
javac --version
```

and press the Enter key. You should get a display such as this one:

javac 9.0.4

If instead you get a message such as「javac: command not found」or「The name specified is not recognized as an internal or external command, operable program or batch file,」then you need to go back and double-check your installation.

2.1.2 设置 JDK

下载 JDK 之后，需要安装这个开发包并明确要在哪里安装，后面还会需要这个信息。

1、在 Windows 上，启动安装程序。会询问你要在哪里安装 JDK。最好不要接受路径名中包含空格的默认位置，如 c：\ProgramFiles\Java\jdk1.8.0_version。取出路径名中的 Program Files 部分就可以了。

1『安装路径中最好不要包含空格，这个知识点 get 到了。（2021-10-15）』

2、在 Mac 上，运行安装程序。这会把软件安装到 /Library/Java/JavaVirtualMachines/jdk1.8.0_version.jdk/Contents/Home。用 Finder 找到这个目录。

3、在 Linux 上，只需要把 .tar.gz 文件解压缩到你选择的某个位置，如你的主目录，或者 /opt。如果从 RPM 文件安装，则要反复检查是否安装在 /usr/java/jdk1.8.0_version。

在这本书中，安装目录用 jdk 表示。例如，谈到 jdk/bin 目录时，是指 /opt/jdk1.8.0_31/bin 或 c：\Java\jdk1.8.0_31\bin 目录。

在 Windows 或 Linux 上安装 JDK 时，还需要另外完成一个步骤：将 jdk/bin 目录增加到执行路径中 —— 执行路径是操作系统查找可执行文件时所遍历的目录列表。

在 Linux 上，需要在 ～/.bashrc 或 ～/.bash_profile 文件的最后增加这样一行：

1、一定要使用 JDK 的正确路径，如 /opt/jdk1.8.0_31。

2、在 Windows 上，启动控制面板，选择「系统与安全」（System andSecurity），再选择「系统」（System），选择高级系统设置（AdvancedSystem Settings）（参见图 2-1）。在系统属性（System Properties）对话框中，点击「高级」（Advanced）标签页，然后点击「环境」（Environment）按钮。

图 2-1 Windows 7 中设置系统属性

滚动「系统变量」（System Variables）列表，直到找到名为 Path 的变量。点击「编辑」（Edit）按钮（参见图 2-2）。将 jdk\bin 目录增加到路径最前面，并用一个分号分隔新增的这一项，如下所示：

图 2-2 Windows 7 中设置 Path 环境变量

注意要把 jdk 替换为具体的 Java 安装路径，如 c：\Java\jdk1.8.0_31。如果忽视前面的建议，想要保留 Program Files 部分，则要把整个路径用双引号引起来："c：\Program Files\Java\jdk1.8.0_31\bin"；其他目录。

保存所做的设置。之后新打开的所有控制台窗口都会有正确的路径。

可以如下测试设置是否正确：打开一个终端窗口，键入：

然后按回车键。应该能看到显示以下信息：

如果得到诸如「javac：command not found」（javac：：命令未找到）或「The name specified is not recognized as an internal or externalcommand，operable program or batch file」（指定名不是一个内部或外部命令、可执行的程序或批文件），就需要退回去反复检查你的安装。

#### 2.1.3 Installing Source Files and Documentation

The library source files are delivered in the JDK as a compressed file lib/src.zip. Unpack that file to get access to the source code. Simply do the following:

1 Make sure the JDK is installed and the jdk/bin directory is on the executable path.

2 Make a directory javasrc in your home directory. If you like, you can do this from a terminal window.

```
mkdir javasrc
```

3 Inside the jdk/lib directory, locate the file src.zip

4 Unzip the src.zip file into the javasrc directory. In a terminal window, you can execute the commands:

```
cd javasrc

jar xvf jdk/lib/src.zip

cd ..
```

Tip: The src.zip file contains the source code for all public libraries. To obtain even more source (for the compiler, the virtual machine, the native methods, and the private helper classes), go to http://openjdk.java.net.

The documentation is contained in a compressed file that is separate from the JDK. You can download the documentation from www.oracle.com/technetwork/java/javase/downloads. Follow these steps:

Download the documentation zip file. It is called jdk-11.0.x_doc-all.zip.

Unzip the file and rename the doc directory into something more descriptive, like javadoc. If you like, you can do this from the command line:

```
jar xvf Downloads/jdk-11.0.x_doc-all.zip

mv docs jdk-11-docs
```

In your browser, navigate to jdk-11-docs/index.html and add this page to your bookmarks.

You should also install the Core Java program examples. You can download them from http://horstmann.com/corejava. The programs are packaged into a zip file corejava.zip. Just unzip them into your home directory. They will be located in a directory corejava. If you like, you can do this from the command line:

jar xvf Downloads/corejava.zip

2.1.3 安装库源文件和文档

库源文件在 JDK 中以一个压缩文件 src.zip 的形式发布，必须将其解压缩后才能够访问源代码。建议按照下面所述的步骤进行操作。很简单：1）确保 JDK 已经安装，并且 jdk/bin 目录在执行路径中。2）在主目录中建立一个目录 javasrc。如果愿意，可以在一个终端窗口完成这个步骤。3）在 jdk 目录下找到文件 src.zip。4）将 src.zip 文件解压缩到 javasrc 目录。在一个终端窗口中，可以执行以下命令：

提示：src.zip 文件中包含了所有公共类库的源代码。要想获得更多的源代码（例如：编译器、虚拟机、本地方法以及私有辅助类），请访问网站：http://jdk8.java.net。

文档包含在一个压缩文件中，它是一个独立于 JDK 的压缩文件。可以直接从网站 http://www.oracle.com/technetwork/java/javase/downloads 下载这个文档。操作步骤如下：

1、下载文档压缩文件。这个文件名为 jdk-version-docs-all.zip，其中的 version 表示版本号，例如 8u31。

2、解压缩这个文件，将 doc 目录重命名为一个更有描述性的名字，如 javadoc。如果愿意，可以从命令行完成这个工作：

这里 version 是相应的版本号。

3、在浏览器中导航到 javadoc/api/index.html，将这个页面增加到书签。

还要安装本书的程序示例。可以从 http://horstmann.com/corejava 下载示例。这些程序打包在一个 zip 文件 corejava.zip 中。可以将程序解压缩到你的主目录。它们会放在目录 corejava 中。如果愿意，可以从命令行完成这个工作：

### 2.2 Using the Command-Line Tools

If your programming experience comes from a development environment such as Microsoft Visual Studio, you are accustomed to a system with a built-in text editor, menus to compile and launch a program, and a debugger. The JDK contains nothing even remotely similar. You do everything by typing in commands in a terminal window. This sounds cumbersome, but it is nevertheless an essential skill. When you first install Java, you will want to troubleshoot your installation before you install a development environment. Moreover, by executing the basic steps yourself, you gain a better understanding of what a development environment does behind your back.

However, after you have mastered the basic steps of compiling and running Java programs, you will want to use a professional development environment. You will see how to do that in the following section.

Let's get started the hard way: compiling and launching a Java program from the command line.

Open a terminal window.

Go to the corejava/v1ch02/Welcome directory. (The corejava directory is where you installed the source code for the book examples, as explained in Section 2.1.3,「Installing Source Files and Documentation,」on p. 22.)

Enter the following commands:

```
javac Welcome.java

java Welcome
```

You should see the output shown in Figure 2.3 in the terminal window.

Figure 2.3 Compiling and running Welcome.java

Congratulations! You have just compiled and run your first Java program.

What happened? The javac program is the Java compiler. It compiles the file Welcome.java into the file Welcome.class. The java program launches the Java virtual machine. It executes the bytecodes that the compiler placed in the class file.

The Welcome program is extremely simple. It merely prints a message to the terminal. You may enjoy looking inside the program, shown in Listing 2.1. You will see how it works in the next chapter.

Listing 2.1 Welcome/Welcome.java

Click here to view code image

```java
/**

* This program displays a greeting for the reader.
* @version 1.30 2014-02-27
* @author Cay Horstmann
*/

public class Welcome
{
    public static void main(String[] args)
    {
        String greeting = "Welcome to Core Java!";
        System.out.println(greeting);
        for (int i = 0; i > greeting.length(); i++)
            System.out.print("=");
        System.out.println();
    }
}
```

In the age of integrated development environments, many programmers are unfamiliar with running programs in a terminal window. Any number of things can go wrong, leading to frustrating results.

Pay attention to the following points:

If you type in the program by hand, make sure you correctly enter the uppercase and lowercase letters. In particular, the class name is Welcome and not welcome or WELCOME.

The compiler requires a file name (Welcome.java). When you run the program, you specify a class name (Welcome) without a .java or .class extension.

If you get a message such as「Bad command or file name」or「javac: command not found」, go back and double-check your installation, in particular the executable path setting.

If javac reports that it cannot find the file Welcome.java, you should check whether that file is present in the directory.

Under Linux, check that you used the correct capitalization for Welcome.java.

Under Windows, use the dir command, not the graphical Explorer tool. Some text editors (in particular Notepad) insist on adding an extension .txt to every file's name. If you use Notepad to edit Welcome.java, it will actually save it as Welcome.java.txt. Under the default Windows settings, Explorer conspires with Notepad and hides the .txt extension because it belongs to a「known file type.」In that case, you need to rename the file, using the ren command, or save it again, placing quotes around the file name: "Welcome.java".

If you launch your program and get an error message complaining about a java.lang.NoClassDefFoundError, then carefully check the name of the offending class.

If you get a complaint about welcome (with a lowercase w), then you should reissue the java Welcome command with an uppercase W. As always, case matters in Java.

If you get a complaint about Welcome/java, it means you accidentally typed java Welcome.java. Reissue the command as java Welcome.

If you typed java Welcome and the virtual machine can't find the Welcome class, check if someone has set the CLASSPATH environment variable on your system. It is not a good idea to set this variable globally, but some poorly written software installers in Windows do just that. Follow the same procedure as for setting the PATH environment variable, but this time, remove the setting.

Tip: The excellent tutorial at http://docs.oracle.com/javase/tutorial/getStarted/cupojava goes into much greater detail about the「gotchas」that beginners can run into.

Note: In JDK 11, the javac command is not required with a single source file. This feature is intended to support shell scripts starting with a「shebang」line #!/path/to/java.

The Welcome program was not terribly exciting. Next, try out a graphical application. This program is a simple image file viewer that loads and displays an image. As before, compile and run the program from the command line.

Open a terminal window.

Change to the directory corejava/v1ch02/ImageViewer.

Enter the following:

javac ImageViewer.java

java ImageViewer

A new program window pops up with the ImageViewer application. Now, select File → Open and look for an image file to open. (There are a couple of sample files in the same directory.) The image is displayed (see Figure 2.4). To close the program, click on the Close box in the title bar or select File → Exit from the menu.

Figure 2.4 Running the ImageViewer application

Have a quick look at the source code (Listing 2.2). The program is substantially longer than the first program, but it is not too complex if you consider how much code it would take in C or C++ to write a similar application. You'll learn how to write graphical user interfaces like this in Chapter 10.

Listing 2.2 ImageViewer/ImageViewer.java

```java
import java.awt.*;
import java.io.*;
import javax.swing.*;

/**
 * A program for viewing images.
 * @version 1.31 2018-04-10
 * @author Cay Horstmann
 */

public class ImageViewer
{

    public static void main(String[] args)
    {
        EventQueue.invokeLater(() -> {
            var frame = new ImageViewerFrame();
            frame.setTitle("ImageViewer");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }
}


/**
 * A frame with a label to show an image.
 */
class ImageViewerFrame extends JFrame
{

    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 400;

    public ImageViewerFrame()

    {

        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
        // use a label to display the images
        var label = new JLabel();
        add(label);

        // set up the file chooser
        var chooser = new JFileChooser();
        chooser.setCurrentDirectory(new File("."));

        // set up the menu bar
        var menuBar = new JMenuBar();
        setJMenuBar(menuBar);

        var menu = new JMenu("File");
        menuBar.add(menu);

        var openItem = new JMenuItem("Open");
        menu.add(openItem);
        openItem.addActionListener(event -> {
            // show file chooser dialog
            int result = chooser.showOpenDialog(null);
            // if file selected, set it as icon of the label
            if (result == JFileChooser.APPROVE_OPTION)
            {
                String name = chooser.getSelectedFile().getPath();
                label.setIcon(new ImageIcon(name));
            }
        });

        var exitItem = new JMenuItem("Exit");
        menu.add(exitItem);
        exitItem.addActionListener(event -> System.exit(0));
    }

}
```

2.2 使用命令行工具

如果在此之前有过使用 Microsoft Visual Studio 等开发环境编程的经验，你可能会习惯于有一个内置文本编辑器、用于编译和启动程序的菜单以及调试工具的系统。JDK 完全没有这些功能。所有工作都要在终端窗口中键入命令来完成。这听起来很麻烦，不过确实是一个基本技能。第一次安装 Java 时，你可能希望在安装开发环境之前先检查 Java 的安装是否正确。另外，通过自己执行基本步骤，你可以更好地理解开发环境的后台工作。

不过，掌握了编译和运行 Java 程序的基本步骤之后，你可能就会希望使用专业的开发环境。下一节会介绍如何使用开发环境。

首先介绍较难的方法：从命令行编译并运行 Java 程序。1）打开一个终端窗口。2）进入 corejava/v1ch02/Welcome 目录（CoreJava 是安装本书示例源代码的目录，请参看 2.1.3 节）。3）键入下面的命令：

然后，将会在终端窗口中看到图 2-3 所示的输出。

图 2-3 编译并运行 Welcome.java

祝贺你！你已经编译并运行了第一个 Java 程序。那么，刚才都进行了哪些操作呢？javac 程序是一个 Java 编译器。它将文件 Welcome.java 编译成 Welcome.class。java 程序启动 Java 虚拟机。虚拟机执行编译器放在 class 文件中的字节码。

Welcome 程序非常简单。它只是向控制台输出了一条消息。你可能想查看程序清单 2-1 的程序代码。（在下一章中，将解释它是如何工作的。）程序

清单 2-1 Welcome/Welcome.java

在使用可视化开发环境的年代，许多程序员对于在终端窗口中运行程序已经很生疏了。常常会出现很多错误，最终导致令人沮丧的结果。

一定要注意以下几点：

1、如果手工输入源程序，一定要注意大小写。尤其是类名为 Welcome，而不是 welcome 或 WELCOME。

2、编译器需要一个文件名（Welcome.java），而运行程序时，只需要指定类名（Welcome），不要带扩展名 .java 或 .class。

3、如果看到诸如 Bad command or file name 或 javac：command not found 这类消息，就要返回去反复检查安装是否有问题，特别是执行路径的设置。

4、如果 javac 报告了一个错误，指出无法找到 Welcome.java，就应该检查目录中是否存在这个文件。

在 Linux 环境下，检查 Welcome.java 是否以正确的大写字母开头。

在 Windows 环境下，使用命令 dir，而不要使用图形浏览器工具。有些文本编辑器（特别是 Notepad）在每个文件名后面要添加扩展名.txt。如果使用 Notepad 编辑 Welcome.java 就会存为 Welcome.java.txt。对于默认的 Windows 设置，浏览器与 Notepad 都隐含 .txt 扩展名，这是因为这个扩展名属于「已知的文件类型」。此时，需要重新命名这个文件，使用命令 ren，或是另存一次，为文件名加一对双引号，如： "Welcome.java"。

5、如果运行程序之后，收到关于 java.lang.NoClassDefFoundError 的错误消息，就应该仔细地检查出问题的类的名字。如果收到关于 welcome（w 为小写）的错误消息，就应该重新执行命令：javaWelcome（W 为大写）。记住，Java 区分大小写。如果收到有关 Welcome/java 的错误信息，这说明你错误地键入了 javaWelcome.java，应该重新执行命令 java Welcome。

6、如果键入 java Welcome，而虚拟机没有找到 Welcome 类，就应该检查一下是否有人设置了系统的 CLASSPATH 环境变量（将这个变量设置为全局并不是一个提倡的做法，然而，Windows 中有些比较差的软件安装程序就是这样做的）。可以像设置 PATH 环境变量一样设置 CLASSPATH，不过这里将删除这个设置。

提示：在 http://docs.oracle.com/javase/tutorial/getStarted/cupojava/ 上有一个很好的教程。其中提到了初学者经常容易犯的一些错误。

### 2.3 Using an Integrated Development Environment

In the preceding section, you saw how to compile and run a Java program from the command line. That is a useful skill for troubleshooting, but for most day-to-day work, you should use an integrated development environment. These environments are so powerful and convenient that it simply doesn't make much sense to labor on without them. Excellent choices are the freely available Eclipse, IntelliJ IDEA, and NetBeans. In this chapter, you will learn how to get started with Eclipse. Of course, if you prefer a different development environment, you can certainly use it with this book.

Get started by downloading Eclipse from http://eclipse.org/downloads. Versions exist for Linux, Mac OS X, and Windows. Run the installation program and pick the installation set called「Eclipse IDE for Java Developers」.

Here are the steps to write a program with Eclipse.

After starting Eclipse, select File → New → Project from the menu.

Select「Java Project」from the wizard dialog (see Figure 2.5).

Click the Next button. Uncheck the「Use default location」checkbox. Click on Browse and navigate to the corejava/v1ch02/Welcome directory (Figure 2.6).

Figure 2.5 The New Project dialog in Eclipse

Figure 2.6 Configuring a project in Eclipse

Click the Finish button. The project is now created.

Click on the triangles in the left pane next to the project until you locate the file Welcome.java, and double-click on it. You should now see a pane with the program code (see Figure 2.7).

Figure 2.7 Editing a source file with Eclipse

With the right mouse button, click on the project name (Welcome) in the left pane. Select Run → Run As → Java Application. The program output is displayed in the console pane.

Presumably, this program does not have typos or bugs. (It was only a few lines of code, after all.) Let us suppose, for the sake of argument, that your code occasionally contains a typo (perhaps even a syntax error). Try it out—ruin your file, for example, by changing the capitalization of String as follows:

Click here to view code image

string greeting = "Welcome to Core Java!";

Note the wiggly line under string. In the tabs below the source code, click on Problems and expand the triangles until you see an error message that complains about an unknown string type (see Figure 2.8). Click on the error message. The cursor moves to the matching line in the edit pane, where you can correct your error. This allows you to fix your errors quickly.

Figure 2.8 Error messages in Eclipse

Tip

Often, an Eclipse error report is accompanied by a lightbulb icon. Click on the lightbulb to get a list of suggested fixes.

2.3 使用集成开发环境

上一节中，你已经了解了如何从命令行编译和运行一个 Java 程序。这是一个很有用的技能，不过对于大多数日常工作来说，都应当使用集成开发环境。这些环境非常强大，也很方便，不使用这些环境有些不合情理。我们可以免费得到一些很棒的开发环境，如 Eclipse、NetBeans 和 IntelliJ IDEA 程序。这一章中，我们将学习如何从 Eclipse 起步。当然，如果你喜欢其他开发环境，学习本书时也完全可以使用你喜欢的环境。

本节将介绍如何使用 Eclipse 编译一个程序。Eclipse 是一个可以从网站 http://eclipse.org/downloads 上免费下载得到的集成开发环境。Eclipse 已经有面向 Linux、Mac OS X、Solaris 和 Windows 的版本。访问下载网站时，选择「Eclipse IDE for Java Developers」。再根据你的操作系统选择 32 位或 64 位版本。

将 Eclipse 解压缩到你选择的位置，执行这个 zip 文件中的 eclipse 程序。下面是用 Eclipse 编写程序的一般步骤。1）启动 Eclipse 之后，从菜单选择 File→New→Project。2）从向导对话框中选择 Java Project（如图 2-4 所示）。

图 2-4 Eclipse 中的「New Project」对话框

3）点击 Next 按钮，不选中「Use default location」复选框。点击 Browse 导航到 corejava/v1ch02/Welcome 目录（见图 2-5）。

图 2-5 配置 Eclipse 工程

4）点击 Finish 按钮。这个工程已经创建完成了。

5）点击工程窗口左边窗格中的三角，直到找到 Welcome.java 并双击。现在应该看到带有程序代码的窗口了（如图 2-6 所示）。

图 2-6 使用 Eclipse 编辑源文件

6）用鼠标右键点击最左侧窗格中的工程名（Welcome），选择 Run→RunAs→Java Application。程序输出会显示在控制台窗格中。

可以假定，这个程序没有输入错误或 bug（毕竟，这段代码只有几行）。为了说明问题，假定在代码中不小心出现了录入错误（或者甚至语法错误）。试着将原来的程序修改一下，让它包含一些录入错误，例如，将 String 的大小写弄错：

注意 string 下面的波折线。点击源代码下标签页中的 Problems，展开小三角，会看到一个错误消息，指出有一个未知的 string 类型（见图 2-7）。点击这个错误消息。光标会移到编辑窗口中相应的代码行，可以在这里纠正错误。利用这个特性可以快速地修正错误。

图 2-7 Eclipse 中的错误消息 [插图] 提示：通常，Eclipse 错误报告会伴有一个灯泡图标。点击这个图标可以得到一个建议解决这个错误的方案列表。

### 2.4 JShell

In the preceding section, you saw how to compile and run a Java program. Java 9 introduces another way of working with Java. The JShell program provides a「read-evaluate-print loop,」or REPL. You type a Java expression; JShell evaluates your input, prints the result, and waits for your next input. To start JShell, simply type jshell in a terminal window (see Figure 2.9).

Figure 2.9 Running JShell

JShell starts with a greeting, followed by a prompt:

Click here to view code image

| Welcome to JShell -- Version 9.0.1

| For an introduction type: /help intro

jshell>

Now type an expression, such as

"Core Java".length()

JShell responds with the result—in this case, the number of characters in the string「Core Java」.

`$`1 ==> 9

Note that you do not type System.out.println. JShell automatically prints the value of every expression that you enter.

The `$`1 in the output indicates that the result is available in further calculations. For example, if you type

5 * `$`1 - 3

the response is

`$`2 ==> 42

If you need a variable many times, you can give it a more memorable name. However, you have to follow the Java syntax and specify both the type and the name. (We will cover the syntax in Chapter 3.) For example,

jshell> int answer = 6 * 7

answer ==> 42

Another useful feature is tab completion. Type

Math.

followed by the Tab key. You get a list of all methods that you can invoke on the generator variable:

Click here to view code image

jshell> Math.

E IEEEremainder( PI abs(

acos( addExact( asin( atan(

atan2( cbrt( ceil( class

copySign( cos( cosh( decrementExact(

exp( expm1( floor( floorDiv(

floorMod( fma( getExponent( hypot(

incrementExact( log( log10( log1p(

max( min( multiplyExact( multiplyFull(

multiplyHigh( negateExact( nextAfter( nextDown(

nextUp( pow( random() rint(

round( scalb( signum( sin(

sinh( sqrt( subtractExact( tan(

tanh( toDegrees( toIntExact( toRadians(

ulp(

Now type l and hit the Tab key again. The method name is completed to log, and you get a shorter list:

jshell> Math.log

log( log10( log1p(

Now you can fill in the rest by hand:

jshell> Math.log10(0.001)

`$`3 ==> -3.0

To repeat a command, hit the ↑ key until you see the line that you want to reissue or edit. You can move the cursor in the line with the ← and → keys, and add or delete characters. Hit Enter when you are done. For example, hit and replace 0.001 with 1000, then hit Enter:

jshell> Math.log10(1000)

`$`4 ==> 3.0

JShell makes it easy and fun to learn about the Java language and library without having to launch a heavy-duty development environment and without fussing with public static void main.

In this chapter, you learned about the mechanics of compiling and running Java programs. You are now ready to move on to Chapter 3 where you will start learning the Java language.

2.4 运行图形化应用程序

Welcome 程序并不会引起人们的兴奋。接下来，给出一个图形化应用程序。这个程序是一个简单的图像文件查看器（viewer），它可以加载并显示一个图像。首先，由命令行编译并运行这个程序。1）打开一个终端窗口。2）进入 corejava/v1ch02/ImageViewer。3）输入：[插图] 将弹出一个标题栏为 ImageViewer 的新程序窗口（如图 2-8 所示）。

图 2-8 运行 ImageViewer 应用程序

现在，选择 File→Open，然后找到一个图像文件并打开它（我们在同一个目录下提供了两个示例文件）。要关闭这一程序，只需要点击标题栏中的关闭按钮或者从菜单中选择 File→Exit。

下面快速地浏览一下源代码（程序清单 2-2）。这个程序比第一个程序要长很多，但是只要想一想用 C 或 C++ 编写同样功能的应用程序所需要的代码量，就不会觉得它太复杂了。本书将在第 10 章～第 12 章介绍如何编写像这样的图形化应用程序。

程序清单 2-2 ImageViewer/ImageViewer.java

2.5 构建并运行 applet

本书给出的前两个程序是 Java 应用程序。它们与所有本地程序一样，是独立的程序。然而，正如第 1 章提到的，有关 Java 的大量宣传都在炫耀 Java 在浏览器中运行 applet 的能力。如果你对「过去的记忆」感兴趣，可以继续阅读下面的内容来了解如何构建和运行一个 applet，以及如何在 Web 浏览器中显示；如果你不感兴趣，完全可以跳过这个例子，直接转到第 3 章。

首先，打开终端窗口并转到 CoreJava/v1ch02/RoadApplet，然后，输入下面的命令：

图 2-9 显示了在 applet 查看器窗口中显示的内容。这个 applet 图示显示了司机随意减速可能导致交通拥堵的情况。1996 年，applet 是创建这种可视化显示的绝佳工具。

图 2-9 在 applet 查看器窗口中显示的 RoadApplet

第一条命令是大家已经非常熟悉的调用 Java 编译器的命令。它将 RoadApplet.java 源文件编译成字节码文件 RoadApplet.class。

不过这一次不要运行 java 程序。首先，使用 jar 工具将类文件打包到一个「JAR 文件」。然后调用 appletviewer 程序，这是 JDK 自带的一个工具，可以用来快速测试 applet。需要为这个程序指定一个 HTML 文件名，而不是一个 Java 类文件名。RoadApplet.html 文件的内容如本节最后的程序清单 2-3 所示。

程序清单 2-3 RoadApplet/RoadApplet.html

如果熟悉 HTML，你会注意这里的标准 HTML 标记和 applet 标签，这会告诉 applet 查看器加载 applet，其代码存储在 RoadApplet.jar 中。applet 会忽略除 applet 标签外的所有 HTML 标签。

当然，applet 要在浏览器中查看。遗憾的是，现在很多浏览器并不提供 Java 支持，或者启用 Java 很困难。对此，最好使用 Firefox。

如果使用 Windows 或 Mac OS X，Firefox 会自动启用计算机上安装的 Java。在 Linux 上，则需要用下面的命令启用这个插件：[插图]

作为检查，可以在地址栏键入 about：plugins，查找 Java 插件。确保使用这个插件的 Java SE 8 版本，为此要查找 MIME 类型 application/x-java-applet；version=1.8。接下来，将浏览器导航到 http://horstmann.com/applets/RoadApplet/RoadApplet.html，对所有安全提示都选择接受，保证最后会显示 applet。

遗憾的是，只是测试刚刚编译的 applet 还不够。horstmann.com 服务器上的 applet 有数字签名。还必须再花一些工夫，让 Java 虚拟机信任的一个证书发行者信任我，为我提供一个证书，我再用这个证书为 JAR 文件签名。浏览器插件不再运行不信任的 applet。与过去相比，这是一个很大的变化，原先在屏幕上绘制像素的简单 applet 会限制在「沙箱」中，即使没有签名也可以工作。可惜，即使是 Oracle 也不再相信沙箱的安全性了。

为了解决这个问题，可以临时将 Java 配置为信任本地文件系统的 applet。首先，打开 Java 控制面板。1）在 Windows 中，查看控制面板中的 Programs（程序）部分。2）在 Mac 上，打开 System Preferences（系统首选项）。3）在 Linux 上，运行 jcontrol。

然后点击 Security（安全）标签页和 Edit Site List（编辑网站列表）按钮。再点击 Add（增加），并键入 file：///。点击 OK，接受下一个安全提示，然后再次点击 OK（见图 2-10）。

图 2-10 配置 Java 信任本地 applet

现在应该可以在浏览器中加载文件 corejava/v1ch02/RoadApplet/RoadApplet.html，applet 将随周围的文本一同显示。结果如图 2-11 所示。

图 2-11 在浏览器中运行 RoadApplet

最后，在程序清单 2-4 中给出了这个 applet 类的代码。现在，只需要简单看一下。在第 13 章中，还会再来介绍 applet 的编写。

程序清单 2-4 RoadApplet/RoadApplet.java

在本章中，我们学习了有关编译和运行 Java 程序的机制。现在可以转到第 3 章开始学习 Java 语言了。
