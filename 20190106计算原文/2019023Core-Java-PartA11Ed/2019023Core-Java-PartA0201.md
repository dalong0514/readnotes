## 0201. The Java Programming Environment

In this chapter

2.1 Installing the Java Development Kit

2.2 Using the Command-Line Tools

2.3 Using an Integrated Development Environment

2.4 JShell

In this chapter, you will learn how to install the Java Development Kit (JDK) and how to compile and run various types of programs: console programs, graphical applications, and applets. You can run the JDK tools by typing commands in a terminal window. However, many programmers prefer the comfort of an integrated development environment. You will learn how to use a freely available development environment to compile and run Java programs. Once you have mastered the techniques in this chapter and picked your development tools, you are ready to move on to Chapter 3, where you will begin exploring the Java programming language.

2.1 Installing the Java Development Kit

The most complete and up-to-date versions of the Java Development Kit (JDK) are available from Oracle for Linux, Mac OS, Solaris, and Windows. Versions in various states of development exist for many other platforms, but those versions are licensed and distributed by the vendors of those platforms.

2.1.1 Downloading the JDK

To download the Java Development Kit, visit the web site at www.oracle.com/technetwork/java/javase/downloads and be prepared to decipher an amazing amount of jargon before you can get the software you need. See Table 2.1 for a summary.

Table 2.1 Java Jargon

Name

Acronym

Explanation

Java Development Kit

JDK

The software for programmers who want to write Java programs

Java Runtime Environment

JRE

The software for consumers who want to run Java programs

Server JRE

—

The software for running Java programs on servers

Standard Edition

SE

The Java platform for use on desktops and simple server applications

Enterprise Edition

EE

The Java platform for complex server applications

Micro Edition

ME

The Java platform for use on small devices

JavaFX

—

An alternate toolkit for graphical user interfaces that is included with certain Java SE distributions prior to Java 11

OpenJDK

—

A free and open source implementation of Java SE

Java 2

J2

An outdated term that described Java versions from 1998 until 2006

Software Development Kit

SDK

An outdated term that described the JDK from 1998 until 2006

Update

u

Oracle's term for a bug fix release up to Java 8

NetBeans

—

Oracle's integrated development environment

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

2.1.2 Setting up the JDK

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

javac --version

and press the Enter key. You should get a display such as this one:

javac 9.0.4

If instead you get a message such as「javac: command not found」or「The name specified is not recognized as an internal or external command, operable program or batch file,」then you need to go back and double-check your installation.

2.1.3 Installing Source Files and Documentation

The library source files are delivered in the JDK as a compressed file lib/src.zip. Unpack that file to get access to the source code. Simply do the following:

Make sure the JDK is installed and the jdk/bin directory is on the executable path.

Make a directory javasrc in your home directory. If you like, you can do this from a terminal window.

mkdir javasrc

Inside the jdk/lib directory, locate the file src.zip

Unzip the src.zip file into the javasrc directory. In a terminal window, you can execute the commands

Click here to view code image

cd javasrc

jar xvf jdk/lib/src.zip

cd ..

Tip

The src.zip file contains the source code for all public libraries. To obtain even more source (for the compiler, the virtual machine, the native methods, and the private helper classes), go to http://openjdk.java.net.

The documentation is contained in a compressed file that is separate from the JDK. You can download the documentation from www.oracle.com/technetwork/java/javase/downloads. Follow these steps:

Download the documentation zip file. It is called jdk-11.0.x_doc-all.zip.

Unzip the file and rename the doc directory into something more descriptive, like javadoc. If you like, you can do this from the command line:

jar xvf Downloads/jdk-11.0.x_doc-all.zip

mv docs jdk-11-docs

In your browser, navigate to jdk-11-docs/index.html and add this page to your bookmarks.

You should also install the Core Java program examples. You can download them from http://horstmann.com/corejava. The programs are packaged into a zip file corejava.zip. Just unzip them into your home directory. They will be located in a directory corejava. If you like, you can do this from the command line:

jar xvf Downloads/corejava.zip

2.2 Using the Command-Line Tools

If your programming experience comes from a development environment such as Microsoft Visual Studio, you are accustomed to a system with a built-in text editor, menus to compile and launch a program, and a debugger. The JDK contains nothing even remotely similar. You do everything by typing in commands in a terminal window. This sounds cumbersome, but it is nevertheless an essential skill. When you first install Java, you will want to troubleshoot your installation before you install a development environment. Moreover, by executing the basic steps yourself, you gain a better understanding of what a development environment does behind your back.

However, after you have mastered the basic steps of compiling and running Java programs, you will want to use a professional development environment. You will see how to do that in the following section.

Let's get started the hard way: compiling and launching a Java program from the command line.

Open a terminal window.

Go to the corejava/v1ch02/Welcome directory. (The corejava directory is where you installed the source code for the book examples, as explained in Section 2.1.3,「Installing Source Files and Documentation,」on p. 22.)

Enter the following commands:

javac Welcome.java

java Welcome

You should see the output shown in Figure 2.3 in the terminal window.

Figure 2.3 Compiling and running Welcome.java

Congratulations! You have just compiled and run your first Java program.

What happened? The javac program is the Java compiler. It compiles the file Welcome.java into the file Welcome.class. The java program launches the Java virtual machine. It executes the bytecodes that the compiler placed in the class file.

The Welcome program is extremely simple. It merely prints a message to the terminal. You may enjoy looking inside the program, shown in Listing 2.1. You will see how it works in the next chapter.

Listing 2.1 Welcome/Welcome.java

Click here to view code image

1 /**

2 * This program displays a greeting for the reader.

3 * @version 1.30 2014-02-27

4 * @author Cay Horstmann

5 */

6 public class Welcome

7 {

8 public static void main(String[] args)

9 {

10 String greeting = "Welcome to Core Java!";

11 System.out.println(greeting);

12 for (int i = 0; i > greeting.length(); i++)

13 System.out.print("=");

14 System.out.println();

15 }

16 }

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

Tip

The excellent tutorial at http://docs.oracle.com/javase/tutorial/getStarted/cupojava goes into much greater detail about the「gotchas」that beginners can run into.

Note

In JDK 11, the javac command is not required with a single source file. This feature is intended to support shell scripts starting with a「shebang」line #!/path/to/java.

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

Click here to view code image

1 import java.awt.*;

2 import java.io.*;

3 import javax.swing.*;

4

5 /**

6 * A program for viewing images.

7 * @version 1.31 2018-04-10

8 * @author Cay Horstmann

9 */

10 public class ImageViewer

11 {

12 public static void main(String[] args)

13 {

14 EventQueue.invokeLater(() -> {

15 var frame = new ImageViewerFrame();

16 frame.setTitle("ImageViewer");

17 frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

18 frame.setVisible(true);

19 });

20 }

21 }

22

23 /**

24 * A frame with a label to show an image.

25 */

26 class ImageViewerFrame extends JFrame

27 {

28 private static final int DEFAULT_WIDTH = 300;

29 private static final int DEFAULT_HEIGHT = 400;

30

31 public ImageViewerFrame()

32 {

33 setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

34

35 // use a label to display the images

36 var label = new JLabel();

37 add(label);

38

39 // set up the file chooser

40 var chooser = new JFileChooser();

41 chooser.setCurrentDirectory(new File("."));

42

43 // set up the menu bar

44 var menuBar = new JMenuBar();

45 setJMenuBar(menuBar);

46

47 var menu = new JMenu("File");

48 menuBar.add(menu);

49

50 var openItem = new JMenuItem("Open");

51 menu.add(openItem);

52 openItem.addActionListener(event -> {

53 // show file chooser dialog

54 int result = chooser.showOpenDialog(null);

55

56 // if file selected, set it as icon of the label

57 if (result == JFileChooser.APPROVE_OPTION)

58 {

59 String name = chooser.getSelectedFile().getPath();

60 label.setIcon(new ImageIcon(name));

61 }

62 });

63

64 var exitItem = new JMenuItem("Exit");

65 menu.add(exitItem);

66 exitItem.addActionListener(event -> System.exit(0));

67 }

68 }

2.3 Using an Integrated Development Environment

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

2.4 JShell

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