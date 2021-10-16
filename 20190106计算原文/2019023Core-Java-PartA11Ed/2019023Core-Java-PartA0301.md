# 0301. Fundamental Programming Structures in Java

In this chapter:

3.1 A Simple Java Program

3.2 Comments

3.3 Data Types

3.4 Variables and Constants

3.5 Operators

3.6 Strings

3.7 Input and Output

3.8 Control Flow

3.9 Big Numbers

3.10 Arrays

At this point, we are assuming that you successfully installed the JDK and were able to run the sample programs that we showed you in Chapter 2. It's time to start programming. This chapter shows you how the basic programming concepts such as data types, branches, and loops are implemented in Java.

0301 Java 的基本程序设计结构

现在，假定已经成功地安装了 JDK，并且能够运行第 2 章中给出的示例程序。我们从现在开始将介绍 Java 应用程序设计。本章主要介绍程序设计的基本概念（如数据类型、分支以及循环）在 Java 中的实现方式。

非常遗憾，需要告诫大家，使用 Java 编写 GUI 应用程序并不是一件很容易的事情，编程者需要掌握很多相关的知识才能够创建窗口、添加文本框以及能响应的按钮等。介绍基于 GUI 的 Java 应用程序设计技术与本章将要介绍的程序设计基本概念相差甚远，因此本章给出的所有示例都是为了说明一些相关概念而设计的「玩具式」程序，它们仅仅使用终端窗口提供输入输出。

最后需要说明，对于一个有 C++ 编程经验的程序员来说，本章的内容只需要浏览一下，应该重点阅读散布在正文中的 C/C++ 注释。对于具有使用 VisualBasic 等其他编程背景的程序员来说，可能会发现其中的绝大多数概念都很熟悉，但是在语法上有比较大的差异，因此，需要非常仔细地阅读本章的内容。

## 3.1 A Simple Java Program

Let's look more closely at one of the simplest Java programs you can have—one that merely prints a message to console:

```java
public class FirstSample {

    public static void main(String[] args) {
	// write your code here
        System.out.println("We will not use 'Hello, World!'");
    }
}
```

It is worth spending all the time you need to become comfortable with the framework of this sample; the pieces will recur in all applications. First and foremost, Java is case sensitive. If you made any mistakes in capitalization (such as typing Main instead of main), the program will not run.

Now let's look at this source code line by line. The keyword public is called an access modifier; these modifiers control the level of access other parts of a program have to this code. We'll have more to say about access modifiers in Chapter 5. The keyword class reminds you that everything in a Java program lives inside a class. Although we will spend a lot more time on classes in the next chapter, for now think of a class as a container for the program logic that defines the behavior of an application. As mentioned in Chapter 1, classes are the building blocks with which all Java applications and applets are built. Everything in a Java program must be inside a class.

Following the keyword class is the name of the class. The rules for class names in Java are quite generous. Names must begin with a letter, and after that, they can have any combination of letters and digits. The length is essentially unlimited. You cannot use a Java reserved word (such as public or class) for a class name. (See the appendix for a list of reserved words.)

The standard naming convention (which we follow in the name FirstSample) is that class names are nouns that start with an uppercase letter. If a name consists of multiple words, use an initial uppercase letter in each of the words. (This use of uppercase letters in the middle of a word is sometimes called「camel case」or, self-referentially,「CamelCase」.

You need to make the file name for the source code the same as the name of the public class, with the extension .java appended. Thus, you must store this code in a file called FirstSample.java. (Again, case is important—don't use firstsample.java.)

If you have named the file correctly and not made any typos in the source code, then when you compile this source code, you end up with a file containing the bytecodes for this class. The Java compiler automatically names the bytecode file FirstSample.class and stores it in the same directory as the source file. Finally, launch the program by issuing the following command:

java FirstSample

(Remember to leave off the .class extension.) When the program executes, it simply displays the string We will not use 'Hello, World!' on the console.

When you use

java ClassName

to run a compiled program, the Java virtual machine always starts execution with the code in the main method in the class you indicate. (The term「method」is Java-speak for a function.) Thus, you must have a main method in the source of your class for your code to execute. You can, of course, add your own methods to a class and call them from the main method. (We cover writing your own methods in the next chapter.)

Note: According to the Java Language Specification, the main method must be declared public. (The Java Language Specification is the official document that describes the Java language. You can view or download it from http://docs.oracle.com/javase/specs.

However, several versions of the Java launcher were willing to execute Java programs even when the main method was not public. A programmer filed a bug report. To see it, visit http://bugs.java.com/bugdatabase/index.jsp and enter the Bug ID 4252539. In 1999, that bug was marked as「closed, will not be fixed.」A Sun engineer added an explanation that the Java Virtual Machine Specification (at http://docs.oracle.com/javase/specs/jvms/se8/html) does not mandate that main is public and that「fixing it will cause potential troubles.」Fortunately, sanity finally prevailed. The Java launcher in Java 1.4 and beyond enforces that the main method is public.

There are a couple of interesting aspects about this story. On the one hand, it is frustrating to have quality assurance engineers, who are often overworked and not always experts in the fine points of Java, make questionable decisions about bug reports. On the other hand, it is remarkable that Sun made the bug reports and their resolutions available for anyone to scrutinize, long before Java was open source. At one point, Sun even let programmers vote for their most despised bugs and used the vote counts to decide which of them would get fixed in the next JDK release.

Notice the braces { } in the source code. In Java, as in C/C++, braces delineate the parts (usually called blocks) in your program. In Java, the code for any method must be started by an opening brace { and ended by a closing brace }.

Brace styles have inspired an inordinate amount of useless controversy. We follow a style that lines up matching braces. As whitespace is irrelevant to the Java compiler, you can use whatever brace style you like. We will have more to say about the use of braces when we talk about the various kinds of loops.

For now, don't worry about the keywords static void—just think of them as part of what you need to get a Java program to compile. By the end of Chapter 4, you will understand this incantation completely. The point to remember for now is that every Java application must have a main method that is declared in the following way:

```Java
public class ClassName

{
    public static void main(String[] args)
    {
        program statements
    }
}
```

C++ Note: As a C++ programmer, you know what a class is. Java classes are similar to C++ classes, but there are a few differences that can trap you. For example, in Java all functions are methods of some class. (The standard terminology refers to them as methods, not member functions.) Thus, in Java you must have a shell class for the main method. You may also be familiar with the idea of static member functions in C++. These are member functions defined inside a class that do not operate on objects. The main method in Java is always static. Finally, as in C/C++, the void keyword indicates that this method does not return a value. Unlike C/C++, the main method does not return an「exit code」to the operating system. If the main method exits normally, the Java program has the exit code 0, indicating successful completion. To terminate the program with a different exit code, use the System.exit method.

Next, turn your attention to this fragment:

```java
{

    System.out.println("We will not use 'Hello, World!'");

}
```

Braces mark the beginning and end of the body of the method. This method has only one statement in it. As with most programming languages, you can think of Java statements as sentences of the language. In Java, every statement must end with a semicolon. In particular, carriage returns do not mark the end of a statement, so statements can span multiple lines if need be.

The body of the main method contains a statement that outputs a single line of text to the console.

Here, we are using the System.out object and calling its println method. Notice the periods used to invoke a method. Java uses the general syntax

```java
object.method(parameters)
```

as its equivalent of a function call.

In this case, we are calling the println method and passing it a string parameter. The method displays the string parameter on the console. It then terminates the output line, so that each call to println displays its output on a new line. Notice that Java, like C/C++, uses double quotes to delimit strings. (You can find more information about strings later in this chapter.)

Methods in Java, like functions in any programming language, can use zero, one, or more parameters (some programmers call them arguments). Even if a method takes no parameters, you must still use empty parentheses. For example, a variant of the println method with no parameters just prints a blank line. You invoke it with the call

```java
System.out.println();
```

Note: System.out also has a print method that doesn't add a newline character to the output. For example, System.out.print("Hello") prints Hello without a newline. The next output appears immediately after the letter o.

3.1 一个简单的 Java 应用程序

下面看一个最简单的 Java 应用程序，它只发送一条消息到控制台窗口中：

这个程序虽然很简单，但所有的 Java 应用程序都具有这种结构，还是值得花一些时间来研究。首先，Java 区分大小写。如果出现了大小写拼写错误（例如，将 main 拼写成 Main），程序将无法运行。

下面逐行地查看一下这段源代码。关键字 public 称为访问修饰符（accessmodifier），这些修饰符用于控制程序的其他部分对这段代码的访问级别。在第 5 章中将会更加详细地介绍访问修饰符的具体内容。关键字 class 表明 Java 程序中的全部内容都包含在类中。这里，只需要将类作为一个加载程序逻辑的容器，程序逻辑定义了应用程序的行为。在第 4 章中将会用大量的篇幅介绍 Java 类。正如第 1 章所述，类是构建所有 Java 应用程序和 applet 的构建块。Java 应用程序中的全部内容都必须放置在类中。

关键字 class 后面紧跟类名。Java 中定义类名的规则很宽松。名字必须以字母开头，后面可以跟字母和数字的任意组合。长度基本上没有限制。但是不能使用 Java 保留字（例如，public 或 class）作为类名（保留字列表请参看附录 A）。

标准的命名规范为（类名 FirstSample 就遵循了这个规范）：类名是以大写字母开头的名词。如果名字由多个单词组成，每个单词的第一个字母都应该大写（这种在一个单词中间使用大写字母的方式称为骆驼命名法。以其自身为例，应该写成 CamelCase）。

源代码的文件名必须与公共类的名字相同，并用 .java 作为扩展名。因此，存储这段源代码的文件名必须为 FirstSample.java（再次提醒大家注意，大小写是非常重要的，千万不能写成 firstsample.java）。

如果已经正确地命名了这个文件，并且源代码中没有任何录入错误，在编译这段源代码之后就会得到一个包含这个类字节码的文件。Java 编译器将字节码文件自动地命名为 FirstSample.class，并与源文件存储在同一个目录下。最后，使用下面这行命令运行这个程序：

（请记住，不要添加 .class 扩展名。）程序执行之后，控制台上将会显示「Wewill not use‘Hello，World'！」。

当使用：

运行已编译的程序时，Java 虚拟机将从指定类中的 main 方法开始执行（这里的「方法」就是 Java 中所说的「函数」），因此为了代码能够执行，在类的源文件中必须包含一个 main 方法。当然，也可以将用户自定义的方法添加到类中，并且在 main 方法中调用它们（第 4 章将讲述如何自定义方法）。

注释：根据 Java 语言规范，main 方法必须声明为 public（Java 语言规范是描述 Java 语言的官方文档。可以从网站 http://docs.oracle.com/javase/specs 上阅读或下载）。

不过，当 main 方法不是 public 时，有些版本的 Java 解释器也可以执行 Java 应用程序。有个程序员报告了这个 bug。如果感兴趣的话，可以在网站 http://bugs.java.com/bugdatabase/index.jsp 上输入 bug 号码 4252539 查看。这个 bug 被标明「关闭，不予修复。」Sun 公司的工程师解释说：Java 虚拟机规范（在 http://docs.oracle.com/javase/specs/jvms/se8/html）并没有要求 main 方法一定是 public，并且「修复这个 bug 有可能带来其他的隐患」。好在，这个问题最终得到了解决。在 Java SE 1.4 及以后的版本中强制 main 方法是 public 的。

从上面这段话可以发现一个问题的两个方面。一方面让质量保证工程师判断在 bug 报告中是否存在问题是一件很头痛的事情，这是因为其工作量很大，并且工程师对 Java 的所有细节也未必了解得很清楚。另一方面，Sun 公司在 Java 开源很久以前就把 bug 报告及其解决方案放到网站上让所有人监督检查，这是一种非常了不起的举动。某些情况下，Sun 甚至允许程序员为他们最厌恶的 bug 投票，并用投票结果来决定发布的下一个 JDK 版本将修复哪些 bug。

需要注意源代码中的括号 {}。在 Java 中，像在 C/C++ 中一样，用大括号划分程序的各个部分（通常称为块）。Java 中任何方法的代码都用「{」开始，用「}」结束。

大括号的使用风格曾经引发过许多无意义的争论。我们的习惯是把匹配的大括号上下对齐。不过，由于空白符会被 Java 编译器忽略，所以可以选用自己喜欢的大括号风格。在下面讲述各种循环语句时，我们还会详细地介绍大括号的使用。

我们暂且不去理睬关键字 static void，而仅把它们当作编译 Java 应用程序必要的部分就行了。在学习完第 4 章后，这些内容的作用就会揭晓。现在需要记住：每个 Java 应用程序都必须有一个 main 方法，其声明格式如下所示：

C++ 注释：作为一名 C++ 程序员，一定知道类的概念。Java 的类与 C++ 的类很相似，但还是有些差异会使人感到困惑。例如，Java 中的所有函数都属于某个类的方法（标准术语将其称为方法，而不是成员函数）。因此，Java 中的 main 方法必须有一个外壳类。读者有可能对 C++ 中的静态成员函数（staticmember functions）十分熟悉。这些成员函数定义在类的内部，并且不对对象进行操作。Java 中的 main 方法必须是静态的。最后，与 C/C++ 一样，关键字 void 表示这个方法没有返回值，所不同的是 main 方法没有为操作系统返回「退出代码」。如果 main 方法正常退出，那么 Java 应用程序的退出代码为 0，表示成功地运行了程序。如果希望在终止程序时返回其他的代码，那就需要调用 System.exit 方法。

接下来，研究一下这段代码：

一对大括号表示方法体的开始与结束，在这个方法中只包含一条语句。与大多数程序设计语言一样，可以将 Java 语句看成是这种语言的句子。在 Java 中，每个句子必须用分号结束。特别需要说明，回车不是语句的结束标志，因此，如果需要可以将一条语句写在多行上。

在上面这个 main 方法体中只包含了一条语句，其功能是：将一个文本行输出到控制台上。

在这里，使用了 System.out 对象并调用了它的 println 方法。注意，点号（·）用于调用方法。Java 使用的通用语法是：

```java
object.method(parameters)
```

这等价于函数调用。

在这个示例中，调用了 println 方法并传递给它一个字符串参数。这个方法将传递给它的字符串参数显示在控制台上。然后，终止这个输出行，使得每次调用 println 都会在新的一行上显示输出。需要注意一点，Java 与 C/C++ 一样，都采用双引号分隔字符串。（本章稍后将会详细地讲解有关字符串的知识）。

与其他程序设计语言中的函数一样，在 Java 的方法中，可以没有参数，也可以有一个或多个参数（有的程序员把参数叫做实参）。对于一个方法，即使没有参数也需要使用空括号。例如，不带参数的 println 方法只打印一个空行。使用下面的语句来调用：

```java
System.out.println();
```

注释：System.out 还有一个 print 方法，它在输出之后不换行。例如，System.out.print（"Hello"）打印「Hello」之后不换行，后面的输出紧跟在字母「o」之后。

### 3.2 Comments

Comments in Java, as in most programming languages, do not show up in the executable program. Thus, you can add as many comments as needed without fear of bloating the code. Java has three ways of marking comments. The most common form is a //. Use this for a comment that runs from the // to the end of the line.

```java
System.out.println("We will not use 'Hello, World!'"); // is this too cute?
```

When longer comments are needed, you can mark each line with a //, or you can use the /* and */ comment delimiters that let you block off a longer comment.

Finally, a third kind of comment is used to generate documentation automatically. This comment uses a /** to start and a */ to end. You can see this type of comment in Listing 3.1. For more on this type of comment and on automatic documentation generation, see Chapter 4.

Listing 3.1 FirstSample/FirstSample.java

```java
/**
 * This is the first sample program in Core Java Chapter 3
 * @version 1.01 1997-03-22
 * @author Gary Cornell
 */

public class FirstSample
{
    public static void main(String[] args)
    {
        System.out.println("We will not use 'Hello, World!'");
    }
}
```

Caution: `/* */` comments do not nest in Java. That is, you might not be able to deactivate code simply by surrounding it with /* and */ because the code you want to deactivate might itself contain a */ delimiter.

3.2 注释

与大多数程序设计语言一样，Java 中的注释也不会出现在可执行程序中。因此，可以在源程序中根据需要添加任意多的注释，而不必担心可执行代码会膨胀。在 Java 中，有 3 种标记注释的方式。

最常用的方式是使用 //，其注释内容从 // 开始到本行结尾。当需要长篇的注释时，既可以在每行的注释前面标记 //，也可以使用 /* 和 */ 将一段比较长的注释括起来。

最后，第 3 种注释可以用来自动地生成文档。这种注释以 /** 开始，以 */ 结束。请参见程序清单 3-1。有关这种注释的详细内容和自动生成文档的具体方法请参见第 4 章。

程序清单 3-1 FirstSample/FirstSample.java

警告：在 Java 中，/**/ 注释不能嵌套。也就是说，不能简单地把代码用 /* 和 */ 括起来作为注释，因为这段代码本身可能也包含一个 */。

### 3.3 Data Types

Java is a strongly typed language. This means that every variable must have a declared type. There are eight primitive types in Java. Four of them are integer types; two are floating-point number types; one is the character type char, used for code units in the Unicode encoding scheme (see Section 3.3.3,「The char Type,」on p. 46); and one is a boolean type for truth values.

Note: Java has an arbitrary-precision arithmetic package. However,「big numbers,」as they are called, are Java objects and not a primitive Java type. You will see how to use them later in this chapter.

3.3 数据类型

Java 是一种强类型语言。这就意味着必须为每一个变量声明一种类型。在 Java 中，一共有 8 种基本类型（primitive type），其中有 4 种整型、2 种浮点类型、1 种用于表示 Unicode 编码的字符单元的字符类型 char（请参见论述 char 类型的章节）和 1 种用于表示真值的 boolean 类型。

注释：Java 有一个能够表示任意精度的算术包，通常称为「大数值」（bignumber）。虽然被称为大数值，但它并不是一种新的 Java 类型，而是一个 Java 对象。本章稍后将会详细地介绍它的用法。

#### 3.3.1 Integer Types

The integer types are for numbers without fractional parts. Negative values are allowed. Java provides the four integer types shown in Table 3.1.

Table 3.1 Java Integer Types

| Type | Storage Requirement | Range (Inclusive) |
| --- | --- | --- |
| int | 4 bytes | –2,147,483,648 to 2,147,483,647 (just over 2 billion) |
| short | 2 bytes | –32,768 to 32,767 |
| long | 8 bytes | –9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| byte | 1 byte | –128 to 127 |

In most situations, the int type is the most practical. If you want to represent the number of inhabitants of our planet, you'll need to resort to a long. The byte and short types are mainly intended for specialized applications, such as low-level file handling, or for large arrays when storage space is at a premium.

Under Java, the ranges of the integer types do not depend on the machine on which you will be running the Java code. This alleviates a major pain for the programmer who wants to move software from one platform to another, or even between operating systems on the same platform. In contrast, C and C++ programs use the most efficient integer type for each processor. As a result, a C program that runs well on a 32-bit processor may exhibit integer overflow on a 16-bit system. Since Java programs must run with the same results on all machines, the ranges for the various types are fixed.

Long integer numbers have a suffix L or l (for example, 4000000000L). Hexadecimal numbers have a prefix 0x or 0X (for example, 0xCAFE). Octal numbers have a prefix 0 (for example, 010 is 8)—naturally, this can be confusing, so we recommend against the use of octal constants.

Starting with Java 7, you can write numbers in binary, with a prefix 0b or 0B. For example, 0b1001 is 9. Also starting with Java 7, you can add underscores to number literals, such as 1_000_000 (or 0b1111_0100_0010_0100_0000) to denote one million. The underscores are for human eyes only. The Java compiler simply removes them.

C++ Note: In C and C++, the sizes of types such as int and long depend on the target platform. On a 16-bit processor such as the 8086, integers are 2 bytes, but on a 32-bit processor like a Pentium or SPARC they are 4-byte quantities. Similarly, long values are 4-byte on 32-bit processors and 8-byte on 64-bit processors. These differences make it challenging to write cross-platform programs. In Java, the sizes of all numeric types are platform-independent.

Note that Java does not have any unsigned versions of the int, long, short,or byte types.

Note: If you work with integer values that can never be negative and you really need an additional bit, you can, with some care, interpret signed integer values as unsigned. For example, instead of having a byte value b represent the range from –128 to 127, you may want a range from 0 to 255. You can store it in a byte. Due to the nature of binary arithmetic, addition, subtraction, and multiplication will work provided they don't overflow. For other operations, call Byte.toUnsignedInt(b) to get an int value between 0 and 255, then process the integer value and cast back to byte. The Integer and Long classes have methods for unsigned division and remainder.

3.3.1 整型

整型用于表示没有小数部分的数值，它允许是负数。Java 提供了 4 种整型，具体内容如表 3-1 所示。

表 3-1 Java 整型

在通常情况下，int 类型最常用。但如果表示星球上的居住人数，就需要使用 long 类型了。byte 和 short 类型主要用于特定的应用场合，例如，底层的文件处理或者需要控制占用存储空间量的大数组。

在 Java 中，整型的范围与运行 Java 代码的机器无关。这就解决了软件从一个平台移植到另一个平台，或者在同一个平台中的不同操作系统之间进行移植给程序员带来的诸多问题。与此相反，C 和 C++ 程序需要针对不同的处理器选择最为高效的整型，这样就有可能造成一个在 32 位处理器上运行很好的 C 程序在 16 位系统上运行却发生整数溢出。由于 Java 程序必须保证在所有机器上都能够得到相同的运行结果，所以各种数据类型的取值范围必须固定。

长整型数值有一个后缀 L 或 l（如 4000000000L）。十六进制数值有一个前缀 0x 或 0X（如 0xCAFE）。八进制有一个前缀 0，例如，010 对应八进制中的 8。很显然，八进制表示法比较容易混淆，所以建议最好不要使用八进制常数。

从 Java 7 开始，加上前缀 0b 或 0B 就可以写二进制数。例如，0b1001 就是 9。另外，同样是从 Java 7 开始，还可以为数字字面量加下划线，如用 1_000_000（或 0b1111_0100_0010_0100_0000）表示一百万。这些下划线只是为了让人更易读。Java 编译器会去除这些下划线。

C++ 注释：在 C 和 C++ 中，int 和 long 等类型的大小与目标平台相关。在 8086 这样的 16 位处理器上整型数值占 2 字节；不过，在 32 位处理器（比如 Pentium 或 SPARC）上，整型数值则为 4 字节。类似地，在 32 位处理器上 long 值为 4 字节，在 64 位处理器上则为 8 字节。由于存在这些差别，这对编写跨平台程序带来了很大难度。在 Java 中，所有的数值类型所占据的字节数量与平台无关。

注意，Java 没有任何无符号（unsigned）形式的 int、long、short 或 byte 类型。

#### 3.3.2 Floating-Point Types

The floating-point types denote numbers with fractional parts. The two floating-point types are shown in Table 3.2.

Table 3.2 Floating-Point Types

| Type | Storage Requirement | Range |
| --- | --- | --- |
| float | 4 bytes | Approximately ±3.40282347E+38F (6–7 significant decimal digits) |
| double | 8 bytes | Approximately ±1.79769313486231570E+308 (15 significant decimal digits) |

The name double refers to the fact that these numbers have twice the precision of the float type. (Some people call these double-precision numbers.) The limited precision of float (6–7 significant digits) is simply not sufficient for many situations. Use float values only when you work with a library that requires them, or when you need to store a very large number of them.

Numbers of type float have a suffix F or f (for example, 3.14F). Floating-point numbers without an F suffix (such as 3.14) are always considered to be of type double. You can optionally supply the D or d suffix (for example, 3.14D).

Note: You can specify floating-point literals in hexadecimal. For example, 0.125 = 2–3 can be written as 0x1.0p-3. In hexadecimal notation, you use a p, not an e, to denote the exponent. (An e is a hexadecimal digit.) Note that the mantissa is written in hexadecimal and the exponent in decimal. The base of the exponent is 2, not 10.

All floating-point computations follow the IEEE 754 specification. In particular, there are three special floating-point values to denote overflows and errors:

Positive infinity

Negative infinity

NaN (not a number)

For example, the result of dividing a positive number by 0 is positive infinity. Computing 0/0 or the square root of a negative number yields NaN.

Note: The constants Double.POSITIVE_INFINITY, Double.NEGATIVE_INFINITY, and Double.NaN (as well as corresponding Float constants) represent these special values, but they are rarely used in practice. In particular, you cannot test

```java
if (x == Double.NaN) // is never true
```

to check whether a particular result equals Double.NaN. All「not a number」values are considered distinct. However, you can use the Double.isNaN method:

```java
if (Double.isNaN(x)) // check whether x is "not a number"
```

Caution

Floating-point numbers are not suitable for financial calculations in which roundoff errors cannot be tolerated. For example, the command System.out.println(2.0 - 1.1) prints 0.8999999999999999, not 0.9 as you would expect. Such roundoff errors are caused by the fact that floating-point numbers are represented in the binary number system. There is no precise binary representation of the fraction 1/10, just as there is no accurate representation of the fraction 1/3 in the decimal system. If you need precise numerical computations without roundoff errors, use the BigDecimal class, which is introduced later in this chapter.

3.3.2 浮点类型

浮点类型用于表示有小数部分的数值。在 Java 中有两种浮点类型，具体内容如表 3-2 所示。

表 3-2 浮点类型

double 表示这种类型的数值精度是 float 类型的两倍（有人称之为双精度数值）。绝大部分应用程序都采用 double 类型。在很多情况下，float 类型的精度很难满足需求。实际上，只有很少的情况适合使用 float 类型，例如，需要单精度数据的库，或者需要存储大量数据。

1『浮点数类型选 double 而非 float。（2021-10-16）』

float 类型的数值有一个后缀 F 或 f（例如，3.14F）。没有后缀 F 的浮点数值（如 3.14）默认为 double 类型。当然，也可以在浮点数值后面添加后缀 D 或 d（例如，3.14D）。

注释：可以使用十六进制表示浮点数值。例如，0.125=2^-3 可以表示成 0x1.0p-3。在十六进制表示法中，使用 p 表示指数，而不是 e。注意，尾数采用十六进制，指数采用十进制。指数的基数是 2，而不是 10。

所有的浮点数值计算都遵循 IEEE 754 规范。具体来说，下面是用于表示溢出和出错情况的三个特殊的浮点数值：1）正无穷大。2）负无穷大。3）NaN（不是一个数字）。

例如，一个正整数除以 0 的结果为正无穷大。计算 0/0 或者负数的平方根结果为 NaN。

注释：常量 Double.POSITIVE_INFINITY、Double.NEGATIVE_INFINITY 和 Double.NaN（以及相应的 Float 类型的常量）分别表示这三个特殊的值，但在实际应用中很少遇到。特别要说明的是，不能这样检测一个特定值是否等于 Double.NaN：

```java
if (x == Double.NaN) // is never true
```

所有「非数值」的值都认为是不相同的。然而，可以使用 Double.isNaN 方法：

```java
if (Double.isNaN(x)) // check whether x is "not a number"
```

警告：浮点数值不适用于无法接受舍入误差的金融计算中。例如，命令 System.out.println（2.0–1.1）将打印出 0.8999999999999999，而不是人们想象的 0.9。这种舍入误差的主要原因是浮点数值采用二进制系统表示，而在二进制系统中无法精确地表示分数 1/10。这就好像十进制无法精确地表示分数 1/3 一样。如果在数值计算中不允许有任何舍入误差，就应该使用 BigDecimal 类，本章稍后将介绍这个类。

#### 3.3.3 The char Type

The char type was originally intended to describe individual characters. However, this is no longer the case. Nowadays, some Unicode characters can be described with one char value, and other Unicode characters require two char values. Read the next section for the gory details.

Literal values of type char are enclosed in single quotes. For example, 'A' is a character constant with value 65. It is different from "A", a string containing a single character. Values of type char can be expressed as hexadecimal values that run from \u0000 to \uFFFF. For example, \u2122 is the trademark symbol (™) and \u03C0 is the Greek letter pi (π).

Besides the \u escape sequences, there are several escape sequences for special characters, as shown in Table 3.3. You can use these escape sequences inside quoted character literals and strings, such as '\u2122' or "Hello\n". The \u escape sequence (but none of the other escape sequences) can even be used outside quoted character constants and strings. For example,

Table 3.3 Escape Sequences for Special Characters

| Escape Sequence | Name | Unicode Value |
| --- | --- | --- |
| \b | Backspace | \u0008 |
| \t | Tab | \u0009 |
| \n | Linefeed | \u000a |
| \r | Carriage return | \u000d |
| \" | Double quote | \u0022 |
| \' | Single quote | \u0027 |
| \\ | Backslash | \u005c |

public static void main(String\u005B\u005D args)

is perfectly legal—\u005B and \u005D are the encodings for [ and ].

Caution: Unicode escape sequences are processed before the code is parsed. For example, "\u0022+\u0022" is not a string consisting of a plus sign surrounded by quotation marks (U+0022). Instead, the \u0022 are converted into " before parsing, yielding ""+"", or an empty string.

Even more insidiously, you must beware of \u inside comments. The comment

```java
// \u000A is a newline
```

yields a syntax error since \u000A is replaced with a newline when the program is read. Similarly, a comment

```java
// look inside c:\users
```

yields a syntax error because the \u is not followed by four hex digits.

3.3.3 char 类型

char 类型原本用于表示单个字符。不过，现在情况已经有所变化。如今，有些 Unicode 字符可以用一个 char 值描述，另外一些 Unicode 字符则需要两个 char 值。有关的详细信息请阅读下一节。

char 类型的字面量值要用单引号括起来。例如：'A' 是编码值为 65 所对应的字符常量。它与 "A" 不同，"A" 是包含一个字符 A 的字符串。char 类型的值可以表示为十六进制值，其范围从 \u0000 到 \Uffff。例如：\u2122 表示注册符号（TM），\u03C0 表示希腊字母 π。

除了转义序列 \u 之外，还有一些用于表示特殊字符的转义序列，请参看表 3-3。所有这些转义序列都可以出现在加引号的字符字面量或字符串中。例如，'\u2122' 或 "Hello\n"。转义序列 \u 还可以出现在加引号的字符常量或字符串之外（而其他所有转义序列不可以）。例如：

表 3-3 特殊字符的转义序列

就完全符合语法规则，\u005B 和 \u005D 是 [ 和 ] 的编码。

警告：Unicode 转义序列会在解析代码之前得到处理。例如，"\u0022+\u0022" 并不是一个由引号（U+0022）包围加号构成的字符串。实际上，\u0022 会在解析之前转换为 "，这会得到""+""，也就是一个空串。

更隐秘地，一定要当心注释中的 \u。注释：

```java
// look inside c:\users
```

会产生一个语法错误，因为读程序时 \u00A0 会替换为一个换行符。类似地，下面这个注释 也会产生一个语法错误，因为 \u 后面并未跟着 4 个十六进制数。

#### 3.3.4 Unicode and the char Type

To fully understand the char type, you have to know about the Unicode encoding scheme. Unicode was invented to overcome the limitations of traditional character encoding schemes. Before Unicode, there were many different standards: ASCII in the United States, ISO 8859-1 for Western European languages, KOI-8 for Russian, GB18030 and BIG-5 for Chinese, and so on. This caused two problems. First, a particular code value corresponds to different letters in the different encoding schemes. Second, the encodings for languages with large character sets have variable length: Some common characters are encoded as single bytes, others require two or more bytes.

Unicode was designed to solve these problems. When the unification effort started in the 1980s, a fixed 2-byte code was more than sufficient to encode all characters used in all languages in the world, with room to spare for future expansion—or so everyone thought at the time. In 1991, Unicode 1.0 was released, using slightly less than half of the available 65,536 code values. Java was designed from the ground up to use 16-bit Unicode characters, which was a major advance over other programming languages that used 8-bit characters.

Unfortunately, over time, the inevitable happened. Unicode grew beyond 65,536 characters, primarily due to the addition of a very large set of ideographs used for Chinese, Japanese, and Korean. Now, the 16-bit char type is insufficient to describe all Unicode characters.

We need a bit of terminology to explain how this problem is resolved in Java, beginning with Java 5. A code point is a code value that is associated with a character in an encoding scheme. In the Unicode standard, code points are written in hexadecimal and prefixed with U+, such as U+0041 for the code point of the Latin letter A. Unicode has code points that are grouped into 17 code planes. The first code plane, called the basic multilingual plane, consists of the「classic」Unicode characters with code points U+0000 to U+FFFF. Sixteen additional planes, with code points U+10000 to U+10FFFF, hold the supplementary characters.

The UTF-16 encoding represents all Unicode code points in a variable-length code. The characters in the basic multilingual plane are represented as 16-bit values, called code units. The supplementary characters are encoded as consecutive pairs of code units. Each of the values in such an encoding pair falls into a range of 2048 unused values of the basic multilingual plane, called the surrogates area (U+D800 to U+DBFF for the first code unit, U+DC00 to U+DFFF for the second code unit). This is rather clever, because you can immediately tell whether a code unit encodes a single character or it is the first or second part of a supplementary character. For example, (the mathematical symbol for the set of octonions, http://math.ucr.edu/home/baez/octonions) has code point U+1D546 and is encoded by the two code units U+D835 and U+DD46. (See https://tools.ietf.org/html/rfc2781 for a description of the encoding algorithm.)

In Java, the char type describes a code unit in the UTF-16 encoding.

Our strong recommendation is not to use the char type in your programs unless you are actually manipulating UTF-16 code units. You are almost always better off treating strings (which we will discuss in Section 3.6,「Strings,」on p. 62) as abstract data types.

3.3.4 Unicode 和 char 类型

要想弄清 char 类型，就必须了解 Unicode 编码机制。Unicode 打破了传统字符编码机制的限制。在 Unicode 出现之前，已经有许多种不同的标准：美国的 ASCII、西欧语言中的 ISO 8859-1、俄罗斯的 KOI-8、中国的 GB 18030 和 BIG-5 等。这样就产生了下面两个问题：一个是对于任意给定的代码值，在不同的编码方案下有可能对应不同的字母；二是采用大字符集的语言其编码长度有可能不同。例如，有些常用的字符采用单字节编码，而另一些字符则需要两个或更多个字节。

设计 Unicode 编码的目的就是要解决这些问题。在 20 世纪 80 年代开始启动设计工作时，人们认为两个字节的代码宽度足以对世界上各种语言的所有字符进行编码，并有足够的空间留给未来的扩展。在 1991 年发布了 Unicode 1.0，当时仅占用 65536 个代码值中不到一半的部分。在设计 Java 时决定采用 16 位的 Unicode 字符集，这样会比使用 8 位字符集的程序设计语言有很大的改进。

十分遗憾，经过一段时间，不可避免的事情发生了。Unicode 字符超过了 65536 个，其主要原因是增加了大量的汉语、日语和韩语中的表意文字。现在，16 位的 char 类型已经不能满足描述所有 Unicode 字符的需要了。

下面利用一些专用术语解释一下 Java 语言解决这个问题的基本方法。从 JavaSE 5.0 开始。码点（code point）是指与一个编码表中的某个字符对应的代码值。在 Unicode 标准中，码点采用十六进制书写，并加上前缀 U+，例如 U+0041 就是拉丁字母 A 的码点。Unicode 的码点可以分成 17 个代码级别（code plane）。第一个代码级别称为基本的多语言级别（basicmultilingual plane），码点从 U+0000 到 U+FFFF，其中包括经典的 Unicode 代码；其余的 16 个级别码点从 U+10000 到 U+10FFFF，其中包括一些辅助字符（supplementary character）。

UTF-16 编码采用不同长度的编码表示所有 Unicode 码点。在基本的多语言级别中，每个字符用 16 位表示，通常被称为代码单元（code unit）；而辅助字符采用一对连续的代码单元进行编码。这样构成的编码值落入基本的多语言级别中空闲的 2048 字节内，通常被称为替代区域（surrogate area）［U+D800~U+DBFF 用于第一个代码单元，U+DC00~U+DFFF 用于第二个代码单元］。这样设计十分巧妙，我们可以从中迅速地知道一个代码单元是一个字符的编码，还是一个辅助字符的第一或第二部分。例如，是八元数集（http://math.ucr.edu/home/baez/octonions）的一个数学符号，码点为 U+1D546，编码为两个代码单元 U+D835 和 U+DD46。（关于编码算法的具体描述见 http://en.wikipedia.org/wiki/UTF-16）。

在 Java 中，char 类型描述了 UTF-16 编码中的一个代码单元。

我们强烈建议不要在程序中使用 char 类型，除非确实需要处理 UTF-16 代码单元。最好将字符串作为抽象数据类型处理（有关这方面的内容将在 3.6 节讨论）。

#### 3.3.5 The boolean Type

The boolean type has two values, false and true. It is used for evaluating logical conditions. You cannot convert between integers and boolean values.

C++ Note: In C++, numbers and even pointers can be used in place of boolean values. The value 0 is equivalent to the bool value false, and a nonzero value is equivalent to true. This is not the case in Java. Thus, Java programmers are shielded from accidents such as

```java
if (x = 0) // oops... meant x == 0
```

In C++, this test compiles and runs, always evaluating to false. In Java, the test does not compile because the integer expression x = 0 cannot be converted to a boolean value.

3.3.5 boolean 类型

boolean（布尔）类型有两个值：false 和 true，用来判定逻辑条件。整型值和布尔值之间不能进行相互转换。

C++ 注释：在 C++ 中，数值甚至指针可以代替 boolean 值。值 0 相当于布尔值 false，非 0 值相当于布尔值 true。在 Java 中则不是这样。因此，Java 程序员不会遇到下述麻烦：

在 C++ 中这个测试可以编译运行，其结果总是 false。而在 Java 中，这个测试将不能通过编译，其原因是整数表达式 x=0 不能转换为布尔值。

### 3.4 Variables and Constants

As in every programming language, variables are used to store values. Constants are variables whose values don't change. In the following sections, you will learn how to declare variables and constants.

3.4 变量

#### 3.4.1 Declaring Variables

In Java, every variable has a type. You declare a variable by placing the type first, followed by the name of the variable. Here are some examples:

double salary;

int vacationDays;

long earthPopulation;

boolean done;

Notice the semicolon at the end of each declaration. The semicolon is necessary because a declaration is a complete Java statement, and all Java statements end in semicolons.

A variable name must begin with a letter and must be a sequence of letters or digits. Note that the terms「letter」and「digit」are much broader in Java than in most languages. A letter is defined as 'A'–'Z', 'a'–'z', '_', '$', or any Unicode character that denotes a letter in a language. For example, German users can use umlauts such as 'ä' in variable names; Greek speakers could use a π. Similarly, digits are '0'–'9' and any Unicode characters that denote a digit in a language. Symbols like '+' or '©' cannot be used inside variable names, nor can spaces. All characters in the name of a variable are significant and case is also significant. The length of a variable name is essentially unlimited.

Tip

If you are really curious as to what Unicode characters are「letters」as far as Java is concerned, you can use the isJavaIdentifierStart and isJavaIdentifierPart methods in the Character class to check.

Tip

Even though $ is a valid Java letter, you should not use it in your own code. It is intended for names that are generated by the Java compiler and other tools.

You also cannot use a Java reserved word as a variable name.

As of Java 9, a single underscore _ cannot be used as a variable name. A future version of Java may use _ as a wildcard symbol.

You can declare multiple variables on a single line:

```java
int i, j; // both are integers
```

However, we don't recommend this style. If you declare each variable separately, your programs are easier to read.

Note: As you saw, names are case sensitive, for example, hireday and hireDay are two separate names. In general, you should not have two names that only differ in their letter case. However, sometimes it is difficult to come up with a good name for a variable. Many programmers then give the variable the same name as the type, for example:

```java
Box box; // "Box" is the type and "box" is the variable name
```

Other programmers prefer to use an「a」prefix for the variable:

```java
Box aBox;
```

在 Java 中，每个变量都有一个类型（type）。在声明变量时，变量的类型位于变量名之前。这里列举一些声明变量的示例：

可以看到，每个声明以分号结束。由于声明是一条完整的 Java 语句，所以必须以分号结束。

变量名必须是一个以字母开头并由字母或数字构成的序列。需要注意，与大多数程序设计语言相比，Java 中「字母」和「数字」的范围更大。字母包括 'A'~'Z'、'a'~'z'、'_'、'$' 或在某种语言中表示字母的任何 Unicode 字符。例如，德国的用户可以在变量名中使用字母 'ä'；希腊人可以用 π。同样，数字包括 '0'~'9' 和在某种语言中表示数字的任何 Unicode 字符。但 '+' 和 '' 这样的符号不能出现在变量名中，空格也不行。变量名中所有的字符都是有意义的，并且大小写敏感。变量名的长度基本上没有限制。

提示：如果想要知道哪些 Unicode 字符属于 Java 中的「字母」，可以使用 Character 类的 isJavaIdentifierStart 和 isJavaIdentifierPart 方法来检查。

提示：尽管 $ 是一个合法的 Java 字符，但不要在你自己的代码中使用这个字符。它只用在 Java 编译器或其他工具生成的名字中。

另外，不能使用 Java 保留字作为变量名（请参看附录 A 中的保留字列表）。

可以在一行中声明多个变量：

不过，不提倡使用这种风格。逐一声明每一个变量可以提高程序的可读性。

注释：如前所述，变量名对大小写敏感，例如，hireday 和 hireDay 是两个不同的变量名。在对两个不同的变量进行命名时，最好不要只存在大小写上的差异。不过，在有些时候，确实很难给变量取一个好的名字。于是，许多程序员将变量名命名为类型名，例如：

还有一些程序员更加喜欢在变量名前加上前缀「a」：

#### 3.4.2 Initializing Variables

After you declare a variable, you must explicitly initialize it by means of an assignment statement—you can never use the value of an uninitialized variable. For example, the Java compiler flags the following sequence of statements as an error:

```java
int vacationDays;

System.out.println(vacationDays); // ERROR--variable not initialized
```

You assign to a previously declared variable by using the variable name on the left, an equal sign (=), and then some Java expression with an appropriate value on the right.

```java
int vacationDays;

vacationDays = 12;
```

You can both declare and initialize a variable on the same line. For example:

```java
int vacationDays = 12;
```

Finally, in Java you can put declarations anywhere in your code. For example, the following is valid code in Java:

```java
double salary = 65000.0;

System.out.println(salary);

int vacationDays = 12; // OK to declare a variable here
```

In Java, it is considered good style to declare variables as closely as possible to the point where they are first used.

Note: Starting with Java 10, you do not need to declare the types of local variables if they can be inferred from the initial value. Simply use the keyword var instead of the type:

Click here to view code image

```java
var vacationDays = 12; // vacationDays is an int

var greeting = "Hello"; // greeting is a String
```

We will start using this feature in the next chapter.

C++ Note: C and C++ distinguish between the declaration and definition of a variable. For example,

```java
int i = 10;
```

is a definition, whereas

```java
extern int i;
```

is a declaration. In Java, no declarations are separate from definitions.

3.4.2 变量初始化

声明一个变量之后，必须用赋值语句对变量进行显式初始化，千万不要使用未初始化的变量。例如，Java 编译器认为下面的语句序列是错误的：

要想对一个已经声明过的变量进行赋值，就需要将变量名放在等号（=）左侧，相应取值的 Java 表达式放在等号的右侧。

也可以将变量的声明和初始化放在同一行中。例如：

最后，在 Java 中可以将声明放在代码中的任何地方。例如，下列代码的书写形式在 Java 中是完全合法的：

在 Java 中，变量的声明尽可能地靠近变量第一次使用的地方，这是一种良好的程序编写风格。

C++ 注释：C 和 C++ 区分变量的声明与定义。例如：

是一个定义，而：

是一个声明。在 Java 中，不区分变量的声明与定义。

#### 3.4.3 Constants

In Java, you use the keyword final to denote a constant. For example:

Click here to view code image

public class Constants

{

public static void main(String[] args)

{

final double CM_PER_INCH = 2.54;

double paperWidth = 8.5;

double paperHeight = 11;

System.out.println("Paper size in centimeters: "

+ paperWidth * CM_PER_INCH + " by " + paperHeight * CM_PER_INCH);

}

}

The keyword final indicates that you can assign to the variable once, and then its value is set once and for all. It is customary to name constants in all uppercase.

It is probably more common in Java to create a constant so it's available to multiple methods inside a single class. These are usually called class constants. Set up a class constant with the keywords static final. Here is an example of using a class constant:

Click here to view code image

public class Constants2

{

public static final double CM_PER_INCH = 2.54;

public static void main(String[] args)

{

double paperWidth = 8.5;

double paperHeight = 11;

System.out.println("Paper size in centimeters: "

+ paperWidth * CM_PER_INCH + " by " + paperHeight * CM_PER_INCH);

}

}

Note that the definition of the class constant appears outside the main method. Thus, the constant can also be used in other methods of the same class. Furthermore, if the constant is declared, as in our example, public, methods of other classes can also use it—in our example, as Constants2.CM_PER_INCH.

C++ Note

const is a reserved Java keyword, but it is not currently used for anything. You must use final for a constant.

3.4.3 常量

在 Java 中，利用关键字 final 指示常量。例如：

关键字 final 表示这个变量只能被赋值一次。一旦被赋值之后，就不能够再更改了。习惯上，常量名使用全大写。

在 Java 中，经常希望某个常量可以在一个类中的多个方法中使用，通常将这些常量称为类常量。可以使用关键字 static final 设置一个类常量。下面是使用类常量的示例：

需要注意，类常量的定义位于 main 方法的外部。因此，在同一个类的其他方法中也可以使用这个常量。而且，如果一个常量被声明为 public，那么其他类的方法也可以使用这个常量。在这个示例中，Constants2.CM_PER-INCH 就是这样一个常量。

C++ 注释：const 是 Java 保留的关键字，但目前并没有使用。在 Java 中，必须使用 final 定义常量。

#### 3.4.4 Enumerated Types

Sometimes, a variable should only hold a restricted set of values. For example, you may sell clothes or pizza in four sizes: small, medium, large, and extra large. Of course, you could encode these sizes as integers 1, 2, 3, 4 or characters S, M, L, and X. But that is an error-prone setup. It is too easy for a variable to hold a wrong value (such as 0 or m).

You can define your own enumerated type whenever such a situation arises. An enumerated type has a finite number of named values. For example,

Click here to view code image

enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE };

Now you can declare variables of this type:

Size s = Size.MEDIUM;

A variable of type Size can hold only one of the values listed in the type declaration, or the special value null that indicates that the variable is not set to any value at all.

We discuss enumerated types in greater detail in Chapter 5.

### 3.5 Operators

Operators are used to combine values. As you will see in the following sections, Java has a rich set of arithmetic and logical operators and mathematical functions.

3.5 运算符

在 Java 中，使用算术运算符 +、-、*、/ 表示加、减、乘、除运算。当参与 / 运算的两个操作数都是整数时，表示整数除法；否则，表示浮点除法。整数的求余操作（有时称为取模）用 % 表示。例如，15/2 等于 7，15%2 等于 1，15.0/2 等于 7.5。

需要注意，整数被 0 除将会产生一个异常，而浮点数被 0 除将会得到无穷大或 NaN 结果。

注释：可移植性是 Java 语言的设计目标之一。无论在哪个虚拟机上运行，同一运算应该得到同样的结果。对于浮点数的算术运算，实现这样的可移植性是相当困难的。double 类型使用 64 位存储一个数值，而有些处理器使用 80 位浮点寄存器。这些寄存器增加了中间过程的计算精度。例如，以下运算：

很多 Intel 处理器计算 x*y，并且将结果存储在 80 位的寄存器中，再除以 z 并将结果截断为 64 位。这样可以得到一个更加精确的计算结果，并且还能够避免产生指数溢出。但是，这个结果可能与始终在 64 位机器上计算的结果不一样。因此，Java 虚拟机的最初规范规定所有的中间计算都必须进行截断。这种行为遭到了数值计算团体的反对。截断计算不仅可能导致溢出，而且由于截断操作需要消耗时间，所以在计算速度上实际上要比精确计算慢。为此，Java 程序设计语言承认了最优性能与理想结果之间存在的冲突，并给予了改进。在默认情况下，虚拟机设计者允许对中间计算结果采用扩展的精度。但是，对于使用 strictfp 关键字标记的方法必须使用严格的浮点计算来生成可再生的结果。例如，可以把 main 方法标记为

于是，在 main 方法中的所有指令都将使用严格的浮点计算。如果将一个类标记为 strictfp，这个类中的所有方法都要使用严格的浮点计算。

实际的计算方式将取决于 Intel 处理器的行为。在默认情况下，中间结果允许使用扩展的指数，但不允许使用扩展的尾数（Intel 芯片在截断尾数时并不损失性能）。因此，这两种方式的区别仅仅在于采用默认的方式不会产生溢出，而采用严格的计算有可能产生溢出。

如果没有仔细阅读这个注释，也没有什么关系。对大多数程序来说，浮点溢出不属于大问题。在本书中，将不使用 strictfp 关键字。

#### 3.5.1 Arithmetic Operators

The usual arithmetic operators +, -, *, / are used in Java for addition, subtraction, multiplication, and division. The / operator denotes integer division if both arguments are integers, and floating-point division otherwise. Integer remainder (sometimes called modulus) is denoted by %. For example, 15 / 2 is 7, 15 % 2 is 1, and 15.0 / 2 is 7.5.

Note that integer division by 0 raises an exception, whereas floating-point division by 0 yields an infinite or NaN result.

Note

One of the stated goals of the Java programming language is portability. A computation should yield the same results no matter which virtual machine executes it. For arithmetic computations with floating-point numbers, it is surprisingly difficult to achieve this portability. The double type uses 64 bits to store a numeric value, but some processors use 80-bit floating-point registers. These registers yield added precision in intermediate steps of a computation. For example, consider the following computation:

double w = x * y / z;

Many Intel processors compute x * y, leave the result in an 80-bit register, then divide by z, and finally truncate the result back to 64 bits. That can yield a more accurate result, and it can avoid exponent overflow. But the result may be different from a computation that uses 64 bits throughout. For that reason, the initial specification of the Java virtual machine mandated that all intermediate computations must be truncated. The numeric community hated it. Not only can the truncated computations cause overflow, they are actually slower than the more precise computations because the truncation operations take time. For that reason, the Java programming language was updated to recognize the conflicting demands for optimum performance and perfect reproducibility. By default, virtual machine designers are now permitted to use extended precision for intermediate computations. However, methods tagged with the strictfp keyword must use strict floating-point operations that yield reproducible results.

For example, you can tag main as

Click here to view code image

public static strictfp void main(String[] args)

Then all instructions inside the main method will use strict floating-point computations. If you tag a class as strictfp, then all of its methods must use strict floating-point computations.

The gory details are very much tied to the behavior of the Intel processors. In the default mode, intermediate results are allowed to use an extended exponent, but not an extended mantissa. (The Intel chips support truncation of the mantissa without loss of performance.) Therefore, the only difference between the default and strict modes is that strict computations may overflow when default computations don't.

If your eyes glazed over when reading this note, don't worry. Floating-point overflow isn't a problem that one encounters for most common programs. We don't use the strictfp keyword in this book.

#### 3.5.2 Mathematical Functions and Constants

The Math class contains an assortment of mathematical functions that you may occasionally need, depending on the kind of programming that you do.

To take the square root of a number, use the sqrt method:

Click here to view code image

double x = 4;

double y = Math.sqrt(x);

System.out.println(y); // prints 2.0

Note

There is a subtle difference between the println method and the sqrt method. The println method operates on the System.out object. But the sqrt method in the Math class does not operate on any object. Such a method is called a static method. You can learn more about static methods in Chapter 4.

The Java programming language has no operator for raising a quantity to a power: You must use the pow method in the Math class. The statement

double y = Math.pow(x, a);

sets y to be x raised to the power a (xa). The pow method's parameters are both of type double, and it returns a double as well.

The floorMod method aims to solve a long-standing problem with integer remainders. Consider the expression n % 2. Everyone knows that this is 0 if n is even and 1 if n is odd. Except, of course, when n is negative. Then it is -1. Why? When the first computers were built, someone had to make rules for how integer division and remainder should work for negative operands. Mathematicians had known the optimal (or「Euclidean」) rule for a few hundred years: always leave the remainder ≥ 0. But, rather than open a math textbook, those pioneers came up with rules that seemed reasonable but are actually inconvenient.

Consider this problem. You compute the position of the hour hand of a clock. An adjustment is applied, and you want to normalize to a number between 0 and 11. That is easy: (position + adjustment) % 12. But what if the adjustment is negative? Then you might get a negative number. So you have to introduce a branch, or use ((position + adjustment) % 12 + 12) % 12. Either way, it is a hassle.

The floorMod method makes it easier: floorMod(position + adjustment, 12) always yields a value between 0 and 11. (Unfortunately, floorMod gives negative results for negative divisors, but that situation doesn't often occur in practice.)

The Math class supplies the usual trigonometric functions:

Math.sin

Math.cos

Math.tan

Math.atan

Math.atan2

and the exponential function with its inverse, the natural logarithm, as well as the decimal logarithm:

Math.exp

Math.log

Math.log10

Finally, two constants denote the closest possible approximations to the mathematical constants π and e:

Math.PI

Math.E

Tip

You can avoid the Math prefix for the mathematical methods and constants by adding the following line to the top of your source file:

Click here to view code image

import static java.lang.Math.*;

For example:

Click here to view code image

System.out.println("The square root of \u03C0 is " + sqrt(PI));

We discuss static imports in Chapter 4.

Note

The methods in the Math class use the routines in the computer's floating-point unit for fastest performance. If completely predictable results are more important than performance, use the StrictMath class instead. It implements the algorithms from the「Freely Distributable Math Library」(www.netlib.org/fdlibm), guaranteeing identical results on all platforms.

Note

The Math class provides several methods to make integer arithmetic safer. The mathematical operators quietly return wrong results when a computation overflows. For example, one billion times three (1000000000 * 3) evaluates to -1294967296 because the largest int value is just over two billion. If you call Math.multiplyExact(1000000000, 3) instead, an exception is generated. You can catch that exception or let the program terminate rather than quietly continue with a wrong result. There are also methods addExact, subtractExact, incrementExact, decrementExact, negateExact, all with int and long parameters.

3.5.1 数学函数与常量

在 Math 类中，包含了各种各样的数学函数。在编写不同类别的程序时，可能需要的函数也不同。

要想计算一个数值的平方根，可以使用 sqrt 方法：

注释：println 方法和 sqrt 方法存在微小的差异。println 方法处理 System.out 对象。但是，Math 类中的 sqrt 方法处理的不是对象，这样的方法被称为静态方法。有关静态方法的详细内容请参看第 4 章。

在 Java 中，没有幂运算，因此需要借助于 Math 类的 pow 方法。语句：

将 y 的值设置为 x 的 a 次幂（xa）。pow 方法有两个 double 类型的参数，其返回结果也为 double 类型。

floorMod 方法的目的是解决一个长期存在的有关整数余数的问题。考虑表达式 n%2。所有人都知道，如果 n 是偶数，这个表达式为 0；如果 n 是奇数，表达式则为 1。当然，除非 n 是负数。如果 n 为负，这个表达式则为 - 1。为什么呢？设计最早的计算机时，必须有人制定规则，明确整数除法和求余对负数操作数该如何处理。数学家们几百年来都知道这样一个最优（或「欧几里德」）规则：余数总是要≥0。不过，最早制定规则的人并没有翻开数学书好好研究，而是提出了一些看似合理但实际上很不方便的规则。

下面考虑这样一个问题：计算一个时钟时针的位置。这里要做一个时间调整，而且要归一化为一个 0~11 之间的数。这很简单：（position+adjustment）%12。不过，如果这个调整为负会怎么样呢？你可能会得到一个负数。所以要引入一个分支，或者使用（（position+adjustment）%12+12）%12。不管怎样，总之都很麻烦。

floorMod 方法就让这个问题变得容易了：floorMod（position+adjustment，12）总会得到一个 0~11 之间的数。（遗憾的是，对于负除数，floorMod 会得到负数结果，不过这种情况在实际中很少出现。）

Math 类提供了一些常用的三角函数：

还有指数函数以及它的反函数 —— 自然对数以及以 10 为底的对数：

最后，Java 还提供了两个用于表示 π 和 e 常量的近似值：

提示：不必在数学方法名和常量名前添加前缀「Math」，只要在源文件的顶部加上下面这行代码就可以了。

例如：

在第 4 章中将讨论静态导入。

注释：在 Math 类中，为了达到最快的性能，所有的方法都使用计算机浮点单元中的例程。如果得到一个完全可预测的结果比运行速度更重要的话，那么就应该使用 StrictMath 类。它使用「自由发布的 Math 库」（fdlibm）实现算法，以确保在所有平台上得到相同的结果。有关这些算法的源代码请参看 www.netlib.org/fdlibm（当 fdlibm 为一个函数提供了多个定义时，StrictMath 类就会遵循 IEEE 754 版本，它的名字将以「e」开头）。

#### 3.5.3 Conversions between Numeric Types

It is often necessary to convert from one numeric type to another. Figure 3.1 shows the legal conversions.

Figure 3.1 Legal conversions between numeric types

The six solid arrows in Figure 3.1 denote conversions without information loss. The three dotted arrows denote conversions that may lose precision. For example, a large integer such as 123456789 has more digits than the float type can represent. When the integer is converted to a float, the resulting value has the correct magnitude but loses some precision.

Click here to view code image

int n = 123456789;

float f = n; // f is 1.23456792E8

When two values are combined with a binary operator (such as n + f where n is an integer and f is a floating-point value), both operands are converted to a common type before the operation is carried out.

If either of the operands is of type double, the other one will be converted to a double.

Otherwise, if either of the operands is of type float, the other one will be converted to a float.

Otherwise, if either of the operands is of type long, the other one will be converted to a long.

Otherwise, both operands will be converted to an int.

3.5.2 数值类型之间的转换

经常需要将一种数值类型转换为另一种数值类型。图 3-1 给出了数值类型之间的合法转换。

在图 3-1 中有 6 个实心箭头，表示无信息丢失的转换；有 3 个虚箭头，表示可能有精度损失的转换。例如，123456789 是一个大整数，它所包含的位数比 float 类型所能够表达的位数多。当将这个整型数值转换为 float 类型时，将会得到同样大小的结果，但却失去了一定的精度。

图 3-1 数值类型之间的合法转换

当使用上面两个数值进行二元操作时（例如 n+f，n 是整数，f 是浮点数），先要将两个操作数转换为同一种类型，然后再进行计算。

·如果两个操作数中有一个是 double 类型，另一个操作数就会转换为 double 类型。

·否则，如果其中一个操作数是 float 类型，另一个操作数将会转换为 float 类型。

·否则，如果其中一个操作数是 long 类型，另一个操作数将会转换为 long 类型。

·否则，两个操作数都将被转换为 int 类型。

#### 3.5.4 Casts

In the preceding section, you saw that int values are automatically converted to double values when necessary. On the other hand, there are obviously times when you want to consider a double as an integer. Numeric conversions are possible in Java, but of course information may be lost. Conversions in which loss of information is possible are done by means of casts. The syntax for casting is to give the target type in parentheses, followed by the variable name. For example:

double x = 9.997;

int nx = (int) x;

Now, the variable nx has the value 9 because casting a floating-point value to an integer discards the fractional part.

If you want to round a floating-point number to the nearest integer (which in most cases is a more useful operation), use the Math.round method:

double x = 9.997;

int nx = (int) Math.round(x);

Now the variable nx has the value 10. You still need to use the cast (int) when you call round. The reason is that the return value of the round method is a long, and a long can only be assigned to an int with an explicit cast because there is the possibility of information loss.

Caution

If you try to cast a number of one type to another that is out of range for the target type, the result will be a truncated number that has a different value. For example, (byte) 300 is actually 44.

C++ Note

You cannot cast between boolean values and any numeric type. This convention prevents common errors. In the rare case when you want to convert a boolean value to a number, you can use a conditional expression such as b ? 1 : 0.

3.5.5 Combining Assignment with Operators

There is a convenient shortcut for using binary operators in an assignment. For example,

x += 4;

is equivalent to

x = x + 4;

(In general, place the operator to the left of the = sign, such as *= or %=.)

Note

If the operator yields a value whose type is different from that of the left-hand side, then it is coerced to fit. For example, if x is an int, then the statement

x += 3.5;

is valid, setting x to (int)(x + 3.5).

3.5.6 Increment and Decrement Operators

Programmers, of course, know that one of the most common operations with a numeric variable is to add or subtract 1. Java, following in the footsteps of C and C++, has both increment and decrement operators: n++ adds 1 to the current value of the variable n, and n-- subtracts 1 from it. For example, the code

int n = 12;

n++;

changes n to 13. Since these operators change the value of a variable, they cannot be applied to numbers themselves. For example, 4++ is not a legal statement.

There are two forms of these operators; you've just seen the postfix form of the operator that is placed after the operand. There is also a prefix form, ++n. Both change the value of the variable by 1. The difference between the two appears only when they are used inside expressions. The prefix form does the addition first; the postfix form evaluates to the old value of the variable.

Click here to view code image

int m = 7;

int n = 7;

int a = 2 * ++m; // now a is 16, m is 8

int b = 2 * n++; // now b is 14, n is 8

We recommend against using ++ inside expressions because this often leads to confusing code and annoying bugs.

3.5.7 Relational and boolean Operators

Java has the full complement of relational operators. To test for equality, use a double equal sign, ==. For example, the value of

3 == 7

is false.

Use a != for inequality. For example, the value of

3 != 7

is true.

Finally, you have the usual < (less than), > (greater than), <= (less than or equal), and >= (greater than or equal) operators.

Java, following C++, uses && for the logical「and」operator and || for the logical「or」operator. As you can easily remember from the != operator, the exclamation point ! is the logical negation operator. The && and || operators are evaluated in「short circuit」fashion: The second argument is not evaluated if the first argument already determines the value. If you combine two expressions with the && operator,

expression1 && expression2

and the truth value of the first expression has been determined to be false, then it is impossible for the result to be true. Thus, the value for the second expression is not calculated. This behavior can be exploited to avoid errors. For example, in the expression

Click here to view code image

x != 0 && 1 / x > x + y // no division by 0

the second part is never evaluated if x equals zero. Thus, 1 / x is not computed if x is zero, and no divide-by-zero error can occur.

Similarly, the value of expression1 || expression2 is automatically true if the first expression is true, without evaluating the second expression.

Finally, Java supports the ternary ?: operator that is occasionally useful. The expression

Click here to view code image

condition ? expression1 : expression2

evaluates to the first expression if the condition is true, to the second expression otherwise. For example,

x < y ? x : y

gives the smaller of x and y.

3.5.8 Bitwise Operators

For any of the integer types, you have operators that can work directly with the bits that make up the integers. This means that you can use masking techniques to get at individual bits in a number. The bitwise operators are

Click here to view code image

& (「and」) | (「or」) ^ (「xor」) ~ (「not」)

These operators work on bit patterns. For example, if n is an integer variable, then

Click here to view code image

int fourthBitFromRight = (n & 0b1000) / 0b1000;

gives you a 1 if the fourth bit from the right in the binary representation of n is 1, and 0 otherwise. Using & with the appropriate power of 2 lets you mask out all but a single bit.

Note

When applied to boolean values, the & and | operators yield a boolean value. These operators are similar to the && and || operators, except that the & and | operators are not evaluated in「short circuit」fashion—that is, both arguments are evaluated before the result is computed.

There are also >> and << operators which shift a bit pattern right or left. These operators are convenient when you need to build up bit patterns to do bit masking:

Click here to view code image

int fourthBitFromRight = (n & (1 << 3)) >> 3;

Finally, a >>> operator fills the top bits with zero, unlike >> which extends the sign bit into the top bits. There is no <<< operator.

Caution

The right-hand argument of the shift operators is reduced modulo 32 (unless the left-hand argument is a long, in which case the right-hand argument is reduced modulo 64). For example, the value of 1 << 35 is the same as 1 << 3 or 8.

C++ Note

In C/C++, there is no guarantee as to whether >> performs an arithmetic shift (extending the sign bit) or a logical shift (filling in with zeroes). Implementors are free to choose whichever is more efficient. That means the C/C++ >> operator may yield implementation-dependent results for negative numbers. Java removes that uncertainty.

3.5.9 Parentheses and Operator Hierarchy

Table 3.4 shows the precedence of operators. If no parentheses are used, operations are performed in the hierarchical order indicated. Operators on the same level are processed from left to right, except for those that are right-associative, as indicated in the table. For example, && has a higher precedence than ||, so the expression

Table 3.4 Operator Precedence

Operators

Associativity

[] . () (method call)

Left to right

! ~ ++ -- + (unary) - (unary) () (cast) new

Right to left

* / %

Left to right

+ -

Left to right

<< >> >>>

Left to right

< <= > >= instanceof

Left to right

== !=

Left to right

&

Left to right

^

Left to right

|

Left to right

&&

Left to right

||

Left to right

?:

Right to left

= += -= *= /= %= &= |= ^= <<= >>= >>>=

Right to left

a && b || c

means

(a && b) || c

Since += associates right to left, the expression

a += b += c

means

a += (b += c)

That is, the value of b += c (which is the value of b after the addition) is added to a.

C++ Note

Unlike C or C++, Java does not have a comma operator. However, you can use a comma-separated list of expressions in the first and third slot of a for statement.

3.5.3 强制类型转换

在上一小节中看到，在必要的时候，int 类型的值将会自动地转换为 double 类型。但另一方面，有时也需要将 double 转换成 int。在 Java 中，允许进行这种数值之间的类型转换。当然，有可能会丢失一些信息。在这种情况下，需要通过强制类型转换（cast）实现这个操作。强制类型转换的语法格式是在圆括号中给出想要转换的目标类型，后面紧跟待转换的变量名。例如：

这样，变量 nx 的值为 9。强制类型转换通过截断小数部分将浮点值转换为整型。

如果想对浮点数进行舍入运算，以便得到最接近的整数（在很多情况下，这种操作更有用），那就需要使用 Math.round 方法：

现在，变量 nx 的值为 10。当调用 round 的时候，仍然需要使用强制类型转换（int）。其原因是 round 方法返回的结果为 long 类型，由于存在信息丢失的可能性，所以只有使用显式的强制类型转换才能够将 long 类型转换成 int 类型。

警告：如果试图将一个数值从一种类型强制转换为另一种类型，而又超出了目标类型的表示范围，结果就会截断成一个完全不同的值。例如，（byte）300 的实际值为 44。

C++ 注释：不要在 boolean 类型与任何数值类型之间进行强制类型转换，这样可以防止发生错误。只有极少数的情况才需要将布尔类型转换为数值类型，这时可以使用条件表达式 b？1：0。

3.5.4 结合赋值和运算符

可以在赋值中使用二元运算符，这是一种很方便的简写形式。例如，

等价于：

（一般地，要把运算符放在 = 号左边，如 *= 或 %=）。

注释：如果运算符得到一个值，其类型与左侧操作数的类型不同，就会发生强制类型转换。例如，如果 x 是一个 int，则以下语句

是合法的，将把 x 设置为（int）（x+3.5）。

3.5.5 自增与自减运算符

当然，程序员都知道加 1、减 1 是数值变量最常见的操作。在 Java 中，借鉴了 C 和 C++ 的做法，也提供了自增、自减运算符：n++ 将变量 n 的当前值加 1，n-- 则将 n 的值减 1。例如，以下代码：

将 n 的值改为 13。由于这些运算符会改变变量的值，所以它们的操作数不能是数值。例如，4++ 就不是一个合法的语句。

实际上，这些运算符有两种形式；上面介绍的是运算符放在操作数后面的「后缀」形式。还有一种「前缀」形式：++n。后缀和前缀形式都会使变量值加 1 或减 1。但用在表达式中时，二者就有区别了。前缀形式会先完成加 1；而后缀形式会使用变量原来的值。

建议不要在表达式中使用 ++，因为这样的代码很容易让人困惑，而且会带来烦人的 bug。

3.5.6 关系和 boolean 运算符

Java 包含丰富的关系运算符。要检测相等性，可以使用两个等号 ==。例如，的值为 false。另外可以使用！= 检测不相等。例如，

的值为 false。另外可以使用！= 检测不相等。例如，

的值为 true。

最后，还有经常使用的 <（小于）、>（大于）、<=（小于等于）和>=（大于等于）运算符。

Java 沿用了 C++ 的做法，使用 && 表示逻辑「与」运算符，使用 || 表示逻辑「或」运算符。从！= 运算符可以想到，感叹号！就是逻辑非运算符。&& 和 || 运算符是按照「短路」方式来求值的：如果第一个操作数已经能够确定表达式的值，第二个操作数就不必计算了。如果用 && 运算符合并两个表达式，

而且已经计算得到第一个表达式的真值为 false，那么结果就不可能为 true。因此，第二个表达式就不必计算了。可以利用这一点来避免错误。例如，在下面的表达式中：

如果 x 等于 0，那么第二部分就不会计算。因此，如果 x 为 0，也就不会计算 1/x，除以 0 的错误就不会出现。

类似地，如果第一个表达式为 true，expression1||expression2 的值就自动为 true，而无需计算第二个表达式。

最后一点，Java 支持三元操作符？：，这个操作符有时很有用。如果条件为 true，下面的表达式

就为第一个表达式的值，否则计算为第二个表达式的值。例如，

会返回 x 和 y 中较小的一个。

3.5.7 位运算符

处理整型类型时，可以直接对组成整型数值的各个位完成操作。这意味着可以使用掩码技术得到整数中的各个位。位运算符包括：

这些运算符按位模式处理。例如，如果 n 是一个整数变量，而且用二进制表示的 n 从右边数第 4 位为 1，则

会返回 1，否则返回 0。利用 & 并结合使用适当的 2 的幂，可以把其他位掩掉，而只保留其中的某一位。

注释：应用在布尔值上时，& 和 | 运算符也会得到一个布尔值。这些运算符与 && 和 || 运算符很类似，不过 & 和 | 运算符不采用「短路」方式来求值，也就是说，得到计算结果之前两个操作数都需要计算。

另外，还有 >> 和 << 运算符将位模式左移或右移。需要建立位模式来完成位掩码时，这两个运算符会很方便：

最后，>>> 运算符会用 0 填充高位，这与 >> 不同，它会用符号位填充高位。不存在 <<< 运算符。

警告：移位运算符的右操作数要完成模 32 的运算（除非左操作数是 long 类型，在这种情况下需要对右操作数模 64）。例如，1<<35 的值等同于 1<<3 或 8。

C++ 注释：在 C/C++ 中，不能保证 >> 是完成算术移位（扩展符号位）还是逻辑移位（填充 0）。实现者可以选择其中更高效的任何一种做法。这意味着 C/C++>> 运算符对于负数生成的结果可能会依赖于具体的实现。Java 则消除了这种不确定性。

3.5.8 括号与运算符级别

表 3-4 给出了运算符的优先级。如果不使用圆括号，就按照给出的运算符优先级次序进行计算。同一个级别的运算符按照从左到右的次序进行计算（除了表中给出的右结合运算符外。）例如，由于 && 的优先级比 || 的优先级高，所以表达式表 3-4 运算符优先级

等价于

又因为 += 是右结合运算符，所以表达式

等价于

也就是将 b+=c 的结果（加上 c 之后的 b）加到 a 上。

C++ 注释：与 C 或 C++ 不同，Java 不使用逗号运算符。不过，可以在 for 语句的第 1 和第 3 部分中使用逗号分隔表达式列表。

3.5.9 枚举类型

有时候，变量的取值只在一个有限的集合内。例如：销售的服装或比萨饼只有小、中、大和超大这四种尺寸。当然，可以将这些尺寸分别编码为 1、2、3、4 或 S、M、L、X。但这样存在着一定的隐患。在变量中很可能保存的是一个错误的值（如 0 或 m）。

针对这种情况，可以自定义枚举类型。枚举类型包括有限个命名的值。例如，

现在，可以声明这种类型的变量：

Size 类型的变量只能存储这个类型声明中给定的某个枚举值，或者 null 值，null 表示这个变量没有设置任何值。有关枚举类型的详细内容将在第 5 章介绍。

### 3.6 Strings

Conceptually, Java strings are sequences of Unicode characters. For example, the string "Java\u2122" consists of the five Unicode characters J, a, v, a, and ™. Java does not have a built-in string type. Instead, the standard Java library contains a predefined class called, naturally enough, String. Each quoted string is an instance of the String class:

Click here to view code image

String e = ""; // an empty string

String greeting = "Hello";

3.6 字符串

从概念上讲，Java 字符串就是 Unicode 字符序列。例如，串「Java\u2122」由 5 个 Unicode 字符 J、a、v、a 和 TM。Java 没有内置的字符串类型，而是在标准 Java 类库中提供了一个预定义类，很自然地叫做 String。每个用双引号括起来的字符串都是 String 类的一个实例：

#### 3.6.1 Substrings

You can extract a substring from a larger string with the substring method of the String class. For example,

Click here to view code image

String greeting = "Hello";

String s = greeting.substring(0, 3);

creates a string consisting of the characters "Hel".

Note

Like C and C++, Java counts code units and code points in strings starting with 0.

The second parameter of substring is the first position that you do not want to copy. In our case, we want to copy positions 0, 1, and 2 (from position 0 to position 2 inclusive). As substring counts it, this means from position 0 inclusive to position 3 exclusive.

There is one advantage to the way substring works: Computing the length of the substring is easy. The string s.substring(a, b) always has length b − a. For example, the substring "Hel" has length 3 − 0 = 3.

3.6.1 子串

String 类的 substring 方法可以从一个较大的字符串提取出一个子串。例如：

创建了一个由字符「Hel」组成的字符串。

substring 方法的第二个参数是不想复制的第一个位置。这里要复制位置为 0、1 和 2（从 0 到 2，包括 0 和 2）的字符。在 substring 中从 0 开始计数，直到 3 为止，但不包含 3。

substring 的工作方式有一个优点：容易计算子串的长度。字符串 s.substring（a，b）的长度为 b-a。例如，子串「Hel」的长度为 3-0=3。

#### 3.6.2 Concatenation

Java, like most programming languages, allows you to use + to join (concatenate) two strings.

Click here to view code image

String expletive = "Expletive";

String PG13 = "deleted";

String message = expletive + PG13;

The preceding code sets the variable message to the string "Expletivedeleted". (Note the lack of a space between the words: The + operator joins two strings in the order received, exactly as they are given.)

When you concatenate a string with a value that is not a string, the latter is converted to a string. (As you will see in Chapter 5, every Java object can be converted to a string.) For example,

Click here to view code image

int age = 13;

String rating = "PG" + age;

sets rating to the string "PG13".

This feature is commonly used in output statements. For example,

Click here to view code image

System.out.println("The answer is " + answer);

is perfectly acceptable and prints what you would expect (and with correct spacing because of the space after the word is).

If you need to put multiple strings together, separated by a delimiter, use the static join method:

Click here to view code image

String all = String.join(" / ", "S", "M", "L", "XL");

// all is the string "S / M / L / XL"

As of Java 11, there is a repeat method:

Click here to view code image

String repeated = "Java".repeat(3); // repeated is "JavaJavaJava"

3.6.2 拼接

与绝大多数的程序设计语言一样，Java 语言允许使用 + 号连接（拼接）两个字符串。

上述代码将「Expletivedeleted」赋给变量 message（注意，单词之间没有空格，+ 号按照给定的次序将两个字符串拼接起来）。

当将一个字符串与一个非字符串的值进行拼接时，后者被转换成字符串（在第 5 章中可以看到，任何一个 Java 对象都可以转换成字符串）。例如： rating 设置为「PG13」。这种特性通常用在输出语句中。例如：

这是一条合法的语句，并且将会打印出所希望的结果（因为单词 is 后面加了一个空格，输出时也会加上这个空格）。如果需要把多个字符串放在一起，用一个定界符分隔，可以使用静态 join 方法：

#### 3.6.3 Strings Are Immutable

The String class gives no methods that let you change a character in an existing string. If you want to turn greeting into "Help!", you cannot directly change the last positions of greeting into 'p' and '!'. If you are a C programmer, this can make you feel pretty helpless. How are we going to modify the string? In Java, it is quite easy: Concatenate the substring that you want to keep with the characters that you want to replace.

Click here to view code image

greeting = greeting.substring(0, 3) + "p!";

This declaration changes the current value of the greeting variable to "Help!".

Since you cannot change the individual characters in a Java string, the documentation refers to the objects of the String class as immutable. Just as the number 3 is always 3, the string "Hello" will always contain the code-unit sequence for the characters H, e, l, l, o. You cannot change these values. Yet you can, as you just saw, change the contents of the string variable greeting and make it refer to a different string, just as you can make a numeric variable currently holding the value 3 hold the value 4.

Isn't that a lot less efficient? It would seem simpler to change the code units than to build up a whole new string from scratch. Well, yes and no. Indeed, it isn't efficient to generate a new string that holds the concatenation of "Hel" and "p!". But immutable strings have one great advantage: The compiler can arrange that strings are shared.

To understand how this works, think of the various strings as sitting in a common pool. String variables then point to locations in the pool. If you copy a string variable, both the original and the copy share the same characters.

Overall, the designers of Java decided that the efficiency of sharing outweighs the inefficiency of string editing by extracting substrings and concatenating. Look at your own programs; we suspect that most of the time, you don't change strings—you just compare them. (There is one common exception—assembling strings from individual characters or from shorter strings that come from the keyboard or a file. For these situations, Java provides a separate class that we describe in Section 3.6.9,「Building Strings,」on p. 74.)

C++ Note

C programmers are generally bewildered when they see Java strings for the first time because they think of strings as arrays of characters:

char greeting[] = "Hello";

That is a wrong analogy: A Java string is roughly analogous to a char* pointer,

char* greeting = "Hello";

When you replace greeting with another string, the Java code does roughly the following:

char* temp = malloc(6);

strncpy(temp, greeting, 3);

strncpy(temp + 3, "p!", 3);

greeting = temp;

Sure, now greeting points to the string "Help!". And even the most hardened C programmer must admit that the Java syntax is more pleasant than a sequence of strncpy calls. But what if we make another assignment to greeting?

greeting = "Howdy";

Don't we have a memory leak? After all, the original string was allocated on the heap. Fortunately, Java does automatic garbage collection. If a block of memory is no longer needed, it will eventually be recycled.

If you are a C++ programmer and use the string class defined by ANSI C++, you will be much more comfortable with the Java String type. C++ string objects also perform automatic allocation and deallocation of memory. The memory management is performed explicitly by constructors, assignment operators, and destructors. However, C++ strings are mutable—you can modify individual characters in a string.

3.6.3 不可变字符串

String 类没有提供用于修改字符串的方法。如果希望将 greeting 的内容修改为「Help！」，不能直接地将 greeting 的最后两个位置的字符修改为‘p' 和‘！'。这对于 C 程序员来说，将会感到无从下手。如何修改这个字符串呢？在 Java 中实现这项操作非常容易。首先提取需要的字符，然后再拼接上替换的字符串：

上面这条语句将 greeting 当前值修改为「Help！」。

由于不能修改 Java 字符串中的字符，所以在 Java 文档中将 String 类对象称为不可变字符串，如同数字 3 永远是数字 3 一样，字符串「Hello」永远包含字符 H、e、l、l 和 o 的代码单元序列，而不能修改其中的任何一个字符。当然，可以修改字符串变量 greeting，让它引用另外一个字符串，这就如同可以将存放 3 的数值变量改成存放 4 一样。

这样做是否会降低运行效率呢？看起来好像修改一个代码单元要比创建一个新字符串更加简洁。答案是：也对，也不对。的确，通过拼接「Hel」和「p！」来创建一个新字符串的效率确实不高。但是，不可变字符串却有一个优点：编译器可以让字符串共享。

为了弄清具体的工作方式，可以想象将各种字符串存放在公共的存储池中。字符串变量指向存储池中相应的位置。如果复制一个字符串变量，原始字符串与复制的字符串共享相同的字符。

总而言之，Java 的设计者认为共享带来的高效率远远胜过于提取、拼接字符串所带来的低效率。查看一下程序会发现：很少需要修改字符串，而是往往需要对字符串进行比较（有一种例外情况，将来自于文件或键盘的单个字符或较短的字符串汇集成字符串。为此，Java 提供了一个独立的类，在 3.6.9 节中将详细介绍）。

C++ 注释：在 C 程序员第一次接触 Java 字符串的时候，常常会感到迷惑，因为他们总将字符串认为是字符型数组：

这种认识是错误的，Java 字符串大致类似于 char * 指针，

当采用另一个字符串替换 greeting 的时候，Java 代码大致进行下列操作：

的确，现在 greeting 指向字符串「Help！」。即使一名最顽固的 C 程序员也得承认 Java 语法要比一连串的 strncpy 调用舒适得多。然而，如果将 greeting 赋予另外一个值又会怎样呢？

这样做会不会产生内存遗漏呢？毕竟，原始字符串放置在堆中。十分幸运，Java 将自动地进行垃圾回收。如果一块内存不再使用了，系统最终会将其回收。

对于一名使用 ANSI C++ 定义的 string 类的 C++ 程序员，会感觉使用 Java 的 String 类型更为舒适。C++string 对象也自动地进行内存的分配与回收。内存管理是通过构造器、赋值操作和析构器显式执行的。然而，C++ 字符串是可修改的，也就是说，可以修改字符串中的单个字符。

#### 3.6.4 Testing Strings for Equality

To test whether two strings are equal, use the equals method. The expression

s.equals(t)

returns true if the strings s and t are equal, false otherwise. Note that s and t can be string variables or string literals. For example, the expression

"Hello".equals(greeting)

is perfectly legal. To test whether two strings are identical except for the upper/lowercase letter distinction, use the equalsIgnoreCase method.

"Hello".equalsIgnoreCase("hello")

Do not use the == operator to test whether two strings are equal! It only determines whether or not the strings are stored in the same location. Sure, if strings are in the same location, they must be equal. But it is entirely possible to store multiple copies of identical strings in different places.

Click here to view code image

String greeting = "Hello"; // initialize greeting to a string

if (greeting == "Hello") . . .

// probably true

if (greeting.substring(0, 3) == "Hel") . . .

// probably false

If the virtual machine always arranges for equal strings to be shared, then you could use the == operator for testing equality. But only string literals are shared, not strings that are the result of operations like + or substring. Therefore, never use == to compare strings lest you end up with a program with the worst kind of bug—an intermittent one that seems to occur randomly.

C++ Note: If you are used to the C++ string class, you have to be particularly careful about equality testing. The C++ string class does overload the == operator to test for equality of the string contents. It is perhaps unfortunate that Java goes out of its way to give strings the same「look and feel」as numeric values but then makes strings behave like pointers for equality testing. The language designers could have redefined == for strings, just as they made a special arrangement for +. Oh well, every language has its share of inconsistencies.

C programmers never use == to compare strings but use strcmp instead. The Java method compareTo is the exact analog of strcmp. You can use

Click here to view code image

if (greeting.compareTo("Hello") == 0) . . .

but it seems clearer to use equals instead.

3.6.4 检测字符串是否相等

可以使用 equals 方法检测两个字符串是否相等。对于表达式：

如果字符串 s 与字符串 t 相等，则返回 true；否则，返回 false。需要注意，s 与 t 可以是字符串变量，也可以是字符串字面量。例如，下列表达式是合法的：

要想检测两个字符串是否相等，而不区分大小写，可以使用 equalsIgnoreCase 方法。

一定不要使用 == 运算符检测两个字符串是否相等！这个运算符只能够确定两个字符串是否放置在同一个位置上。当然，如果字符串放置在同一个位置上，它们必然相等。但是，完全有可能将内容相同的多个字符串的拷贝放置在不同的位置上。

如果虚拟机始终将相同的字符串共享，就可以使用 == 运算符检测是否相等。但实际上只有字符串常量是共享的，而 + 或 substring 等操作产生的结果并不是共享的。因此，千万不要使用 == 运算符测试字符串的相等性，以免在程序中出现糟糕的 bug。从表面上看，这种 bug 很像随机产生的间歇性错误。

C++ 注释：对于习惯使用 C++ 的 string 类的人来说，在进行相等性检测的时候一定要特别小心。C++ 的 string 类重载了 == 运算符以便检测字符串内容的相等性。可惜 Java 没有采用这种方式，它的字符串「看起来、感觉起来」与数值一样，但进行相等性测试时，其操作方式又类似于指针。语言的设计者本应该像对 + 那样也进行特殊处理，即重定义 == 运算符。当然，每一种语言都会存在一些不太一致的地方。

C 程序员从不使用 == 对字符串进行比较，而使用 strcmp 函数。Java 的 compareTo 方法与 strcmp 完全类似，因此，可以这样使用：

不过，使用 equals 看起来更为清晰。

#### 3.6.5 Empty and Null Strings

The empty string "" is a string of length 0. You can test whether a string is empty by calling

if (str.length() == 0)

or

if (str.equals(""))

An empty string is a Java object which holds the string length (namely, 0) and an empty contents. However, a String variable can also hold a special value, called null, that indicates that no object is currently associated with the variable. (See Chapter 4 for more information about null.) To test whether a string is null, use

if (str == null)

Sometimes, you need to test that a string is neither null nor empty. Then use

Click here to view code image

if (str != null && str.length() != 0)

You need to test that str is not null first. As you will see in Chapter 4, it is an error to invoke a method on a null value.

3.6.5 空串与 Null 串空串

"" 是长度为 0 的字符串。可以调用以下代码检查一个字符串是否为空：

或

空串是一个 Java 对象，有自己的串长度（0）和内容（空）。不过，String 变量还可以存放一个特殊的值，名为 null，这表示目前没有任何对象与该变量关联（关于 null 的更多信息请参见第 4 章）。要检查一个字符串是否为 null，要使用以下条件：

有时要检查一个字符串既不是 null 也不为空串，这种情况下就需要使用以下条件：

首先要检查 str 不为 null。在第 4 章会看到，如果在一个 null 值上调用方法，会出现错误。

#### 3.6.6 Code Points and Code Units

Java strings are sequences of char values. As we discussed in Section 3.3.3,「The char Type,」on p. 46, the char data type is a code unit for representing Unicode code points in the UTF-16 encoding. The most commonly used Unicode characters can be represented with a single code unit. The supplementary characters require a pair of code units.

The length method yields the number of code units required for a given string in the UTF-16 encoding. For example:

Click here to view code image

String greeting = "Hello";

int n = greeting.length(); // is 5

To get the true length—that is, the number of code points—call

Click here to view code image

int cpCount = greeting.codePointCount(0, greeting.length());

The call s.charAt(n) returns the code unit at position n, where n is between 0 and s.length() – 1. For example:

Click here to view code image

char first = greeting.charAt(0); // first is 'H'

char last = greeting.charAt(4); // last is 'o'

To get at the ith code point, use the statements

Click here to view code image

int index = greeting.offsetByCodePoints(0, i);

int cp = greeting.codePointAt(index);

Why are we making a fuss about code units? Consider the sentence

is the set of octonions.

The character (U+1D546) requires two code units in the UTF-16 encoding. Calling

Click here to view code image

char ch = sentence.charAt(1)

doesn't return a space but the second code unit of . To avoid this problem, you should not use the char type. It is too low-level.

Note

Don't think that you can ignore exotic characters with code units above U+FFFF. Your emoji-loving users may put characters such as (U+1F37A, beer mug) into strings.

If your code traverses a string, and you want to look at each code point in turn, you can use these statements:

Click here to view code image

int cp = sentence.codePointAt(i);

if (Character.isSupplementaryCodePoint(cp)) i += 2;

else i++;

You can move backwards with the following statements:

Click here to view code image

i--;

if (Character.isSurrogate(sentence.charAt(i))) i--;

int cp = sentence.codePointAt(i);

Obviously, that is quite painful. An easier way is to use the codePoints method that yields a「stream」of int values, one for each code point. (We will discuss streams in Chapter 2 of Volume II.) You can just turn the stream into an array (see Section 3.10,「Arrays,」on p. 108) and traverse that.

Click here to view code image

int[] codePoints = str.codePoints().toArray();

Conversely, to turn an array of code points to a string, use a constructor. (We discuss constructors and the new operator in detail in Chapter 4.)

Click here to view code image

String str = new String(codePoints, 0, codePoints.length);

Note

The virtual machine does not have to implement strings as sequences of code units. In Java 9, strings that hold only single-byte code units use a byte array, and all others a char array.

3.6.6 码点与代码单元

Java 字符串由 char 值序列组成。从 3.3.3 节「char 类型」已经看到，char 数据类型是一个采用 UTF-16 编码表示 Unicode 码点的代码单元。大多数的常用 Unicode 字符使用一个代码单元就可以表示，而辅助字符需要一对代码单元表示。

length 方法将返回采用 UTF-16 编码表示的给定字符串所需要的代码单元数量。例如：

要想得到实际的长度，即码点数量，可以调用：

调用 s.charAt（n）将返回位置 n 的代码单元，n 介于 0~s.length（）-1 之间。例如：

要想得到第 i 个码点，应该使用下列语句

注释：类似于 C 和 C++，Java 对字符串中的代码单元和码点从 0 开始计数。为什么会对代码单元如此大惊小怪？请考虑下列语句：

使用 UTF-16 编码表示字符（U+1D546）需要两个代码单元。调用 返回的不是一个空格，而是的第二个代码单元。为了避免这个问题，不要使用 char 类型。这太底层了。如果想要遍历一个字符串，并且依次查看每一个码点，可以使用下列语句：

可以使用下列语句实现回退操作：

显然，这很麻烦。更容易的办法是使用 codePoints 方法，它会生成一个 int 值的「流」，每个 int 值对应一个码点。（流将在卷 Ⅱ 的第 2 章中讨论）。可以将它转换为一个数组（见 3.10 节），再完成遍历。

反之，要把一个码点数组转换为一个字符串，可以使用构造函数（我们将在第 4 章详细讨论构造函数和 new 操作符）。

#### 3.6.7 The String API

The String class in Java contains more than 50 methods. A surprisingly large number of them are sufficiently useful that we can imagine using them frequently. The following API note summarizes the ones we found most useful.

These API notes, found throughout the book, will help you understand the Java Application Programming Interface (API). Each API note starts with the name of a class, such as java.lang.String. (The significance of the so-called package name java.lang is explained in Chapter 4.) The class name is followed by the names, explanations, and parameter descriptions of one or more methods.

We typically do not list all methods of a particular class but select those that are most commonly used and describe them in a concise form. For a full listing, consult the online documentation (see Section 3.6.8,「Reading the Online API Documentation,」on p. 71).

We also list the version number in which a particular class was introduced. If a method has been added later, it has a separate version number.

java.lang.String 1.0

char charAt(int index)

returns the code unit at the specified location. You probably don't want to call this method unless you are interested in low-level code units.

int codePointAt(int index) 5

returns the code point that starts at the specified location.

int offsetByCodePoints(int startIndex, int cpCount) 5

returns the index of the code point that is cpCount code points away from the code point at startIndex.

int compareTo(String other)

returns a negative value if the string comes before other in dictionary order, a positive value if the string comes after other in dictionary order, or 0 if the strings are equal.

IntStream codePoints() 8

returns the code points of this string as a stream. Call toArray to put them in an array.

new String(int[] codePoints, int offset, int count) 5

constructs a string with the count code points in the array starting at offset.

boolean empty()

boolean blank() 11

returns true if the string is empty or consists of whitespace.

boolean equals(Object other)

returns true if the string equals other.

boolean equalsIgnoreCase(String other)

returns true if the string equals other, except for upper/lowercase distinction.

boolean startsWith(String prefix)

boolean endsWith(String suffix)

returns true if the string starts or ends with suffix.

int indexOf(String str)

int indexOf(String str, int fromIndex)

int indexOf(int cp)

int indexOf(int cp, int fromIndex)

returns the start of the first substring equal to the string str or the code point cp, starting at index 0 or at fromIndex, or -1 if str does not occur in this string.

int lastIndexOf(String str)

int lastIndexOf(String str, int fromIndex)

int lastindexOf(int cp)

int lastindexOf(int cp, int fromIndex)

returns the start of the last substring equal to the string str or the code point cp, starting at the end of the string or at fromIndex.

int length()

returns the number of code units of the string.

int codePointCount(int startIndex, int endIndex) 5

returns the number of code points between startIndex and endIndex – 1.

String replace(CharSequence oldString, CharSequence newString)

returns a new string that is obtained by replacing all substrings matching oldString in the string with the string newString. You can supply String or StringBuilder objects for the CharSequence parameters.

String substring(int beginIndex)

String substring(int beginIndex, int endIndex)

returns a new string consisting of all code units from beginIndex until the end of the string or until endIndex – 1.

String toLowerCase()

String toUpperCase()

returns a new string containing all characters in the original string, with uppercase characters converted to lowercase, or lowercase characters converted to uppercase.

String trim()

String strip() 11

returns a new string by eliminating all leading and trailing characters that are ≤ U+0020 (trim) or whitespace (strip) in the original string.

String join(CharSequence delimiter, CharSequence... elements) 8

returns a new string joining all elements with the given delimiter.

String repeat(int count) 11

returns a string that repeats this string count times.

Note

In the API notes, there are a few parameters of type CharSequence. This is an interface type to which all strings belong. You will learn about interface types in Chapter 6. For now, you just need to know that you can pass arguments of type String whenever you see a CharSequence parameter.

3.6.7 String API

Java 中的 String 类包含了 50 多个方法。令人惊讶的是绝大多数都很有用，可以设想使用的频繁非常高。下面的 API 注释汇总了一部分最常用的方法。

注释：可以发现，本书中给出的 API 注释会有助于理解 Java 应用程序编程接口（API）。每一个 API 的注释都以形如 java.lang.String 的类名开始。（java.lang 包的重要性将在第 4 章给出解释。）类名之后是一个或多个方法的名字、解释和参数描述。

在这里，一般不列出某个类的所有方法，而是选择一些最常用的方法，并以简洁的方式给予描述。完整的方法列表请参看联机文档（请参看 3.6.8 节）。

这里还列出了所给类的版本号。如果某个方法是在这个版本之后添加的，就会给出一个单独的版本号。

java.lang.string 1.0

·char charAt（int index）

返回给定位置的代码单元。除非对底层的代码单元感兴趣，否则不需要调用这个方法。

·int codePointAt（int index）5.0

返回从给定位置开始的码点。

·int offsetByCodePoints（int startIndex，int cpCount）5.0

返回从 startIndex 代码点开始，位移 cpCount 后的码点索引。

·int compareTo（String other）

按照字典顺序，如果字符串位于 other 之前，返回一个负数；如果字符串位于 other 之后，返回一个正数；如果两个字符串相等，返回 0。

·IntStream codePoints（）8

将这个字符串的码点作为一个流返回。调用 toArray 将它们放在一个数组中。

·new String（int[]codePoints，int offset，int count）5.0

用数组中从 offset 开始的 count 个码点构造一个字符串。

·boolean equals（Object other）

如果字符串与 other 相等，返回 true。·boolean equalsIgnoreCase（String other）如果字符串与 other 相等（忽略大小写），返回 true。

·boolean startsWith（String prefix）

·boolean endsWith（String suffix）

如果字符串以 suffix 开头或结尾，则返回 true。

·int index0f（String str）

·int index0f（String str，int fromIndex）

·int index0f（int cp）

·int index0f（int cp，int fromIndex）

返回与字符串 str 或代码点 cp 匹配的第一个子串的开始位置。这个位置从索引 0 或 fromIndex 开始计算。如果在原始串中不存在 str，返回 - 1。

·int lastIndex0f（String str）

·int lastIndex0f（String str，int fromIndex）

·int lastindex0f（int cp）

·int lastindex0f（int cp，int fromIndex）

返回与字符串 str 或代码点 cp 匹配的最后一个子串的开始位置。这个位置从原始串尾端或 fromIndex 开始计算。

·int length（）

返回字符串的长度。

·int codePointCount（int startIndex，int endIndex）5.0

返回 startIndex 和 endIndex-1 之间的代码点数量。没有配成对的代用字符将计入代码点。

·String replace（CharSequence oldString，CharSequence newString）

返回一个新字符串。这个字符串用 newString 代替原始字符串中所有的 oldString。可以用 String 或 StringBuilder 对象作为 CharSequence 参数。

·String substring（int beginIndex）

·String substring（int beginIndex，int endIndex）

返回一个新字符串。这个字符串包含原始字符串中从 beginIndex 到串尾或 endIndex–1 的所有代码单元。

·String toLowerCase（）

·String toUpperCase（）

返回一个新字符串。这个字符串将原始字符串中的大写字母改为小写，或者将原始字符串中的所有小写字母改成了大写字母。

·String trim（）返回一个新字符串。这个字符串将删除了原始字符串头部和尾部的空格。

·String join（CharSequence delimiter，CharSequence...elements）8

返回一个新字符串，用给定的定界符连接所有元素。

注释：在 API 注释中，有一些 CharSequence 类型的参数。这是一种接口类型，所有字符串都属于这个接口。第 6 章将介绍更多有关接口类型的内容。现在只需要知道只要看到一个 CharSequence 形参，完全可以传入 String 类型的实参。

#### 3.6.8 Reading the Online API Documentation

As you just saw, the String class has lots of methods. Furthermore, there are thousands of classes in the standard libraries, with many more methods. It is plainly impossible to remember all useful classes and methods. Therefore, it is essential that you become familiar with the online API documentation that lets you look up all classes and methods in the standard library. You can download the API documentation from Oracle and save it locally, or you can point your browser to http://docs.oracle.com/javase/9/docs/api.

As of Java 9, the API documentation has a search box (see Figure 3.2). Older versions have frames with lists of packages and classes. You can still get those lists by clicking on the Frames menu item. For example, to get more information on the methods of the String class, type「String」into the search box and select the type java.lang.String, or locate the link in the frame with class names and click it. You get the class description, as shown in Figure 3.3.

Figure 3.2 The Java API documentation

Figure 3.3 Class description for the String class

When you scroll down, you reach a summary of all methods, sorted in alphabetical order (see Figure 3.4). Click on any method name for a detailed description of that method (see Figure 3.5). For example, if you click on the compareToIgnoreCase link, you'll get the description of the compareToIgnoreCase method.

Figure 3.4 Method summary of the String class

Figure 3.5 Detailed description of a String method

Tip

If you have not already done so, download the JDK documentation, as described in Chapter 2. Bookmark the jdk-9-docs/index.html page in your browser right now.

3.6.8 阅读联机 API 文档

正如前面所看到的，String 类包含许多方法。而且，在标准库中有几千个类，方法数量更加惊人。要想记住所有的类和方法是一件不太不可能的事情。因此，学会使用在线 API 文档十分重要，从中可以查阅到标准类库中的所有类和方法。API 文档是 JDK 的一部分，它是 HTML 格式的。让浏览器指向安装 JDK 的 docs/api/index.html 子目录，就可以看到如图 3-2 所示的屏幕。

图 3-2 API 文档的三个窗格

可以看到，屏幕被分成三个窗框。在左上方的小窗框中显示了可使用的所有包。在它下面稍大的窗框中列出了所有的类。点击任何一个类名之后，这个类的 API 文档就会显示在右侧的大窗框中（请参看图 3-3）。例如，要获得有关 String 类方法的更多信息，可以滚动第二个窗框，直到看见 String 链接为止，然后点击这个链接。

图 3-3 String 类的描述

接下来，滚动右面的窗框，直到看见按字母顺序排列的所有方法为止（请参看图 3-4）。点击任何一个方法名便可以查看这个方法的详细描述（参见图 3-5）。例如，如果点击 compareToIgnoreCase 链接，就会看到 compareToIgnoreCase 方法的描述。

图 3-4 String 类方法的小结

图 3-5 String 方法的详细描述

提示：马上在浏览器中将 docs/api/index.html 页面建一个书签。

#### 3.6.9 Building Strings

Occasionally, you need to build up strings from shorter strings, such as keystrokes or words from a file. It would be inefficient to use string concatenation for this purpose. Every time you concatenate strings, a new String object is constructed. This is time consuming and wastes memory. Using the StringBuilder class avoids this problem.

Follow these steps if you need to build a string from many small pieces. First, construct an empty string builder:

Click here to view code image

StringBuilder builder = new StringBuilder();

Each time you need to add another part, call the append method.

Click here to view code image

builder.append(ch); // appends a single character

builder.append(str); // appends a string

When you are done building the string, call the toString method. You will get a String object with the character sequence contained in the builder.

Click here to view code image

String completedString = builder.toString();

Note

The StringBuilder class was introduced in Java 5. Its predecessor, StringBuffer, is slightly less efficient, but it allows multiple threads to add or remove characters. If all string editing happens in a single thread (which is usually the case), you should use StringBuilder instead. The APIs of both classes are identical.

The following API notes contain the most important methods for the StringBuilder class.

java.lang.StringBuilder 5

StringBuilder()

constructs an empty string builder.

int length()

returns the number of code units of the builder or buffer.

StringBuilder append(String str)

appends a string and returns this.

StringBuilder append(char c)

appends a code unit and returns this.

StringBuilder appendCodePoint(int cp)

appends a code point, converting it into one or two code units, and returns this.

void setCharAt(int i, char c)

sets the ith code unit to c.

StringBuilder insert(int offset, String str)

inserts a string at position offset and returns this.

StringBuilder insert(int offset, char c)

inserts a code unit at position offset and returns this.

StringBuilder delete(int startIndex, int endIndex)

deletes the code units with offsets startIndex to endIndex – 1 and returns this.

String toString()

returns a string with the same data as the builder or buffer contents.

3.6.9 构建字符串

有些时候，需要由较短的字符串构建字符串，例如，按键或来自文件中的单词。采用字符串连接的方式达到此目的效率比较低。每次连接字符串，都会构建一个新的 String 对象，既耗时，又浪费空间。使用 StringBuilder 类就可以避免这个问题的发生。如果需要用许多小段的字符串构建一个字符串，那么应该按照下列步骤进行。首先，构建一个空的字符串构建器：

当每次需要添加一部分内容时，就调用 append 方法。

在需要构建字符串时就调用 toString 方法，将可以得到一个 String 对象，其中包含了构建器中的字符序列。

注释：在 JDK5.0 中引入 StringBuilder 类。这个类的前身是 StringBuffer，其效率稍有些低，但允许采用多线程的方式执行添加或删除字符的操作。如果所有字符串在一个单线程中编辑（通常都是这样），则应该用 StringBuilder 替代它。这两个类的 API 是相同的。下面的 API 注释包含了 StringBuilder 类中的重要方法。

java.lang.StringBuilder 5.0

·StringBuilder（）构造一个空的字符串构建器。

·int length（）返回构建器或缓冲器中的代码单元数量。

·StringBuilder append（String str）追加一个字符串并返回 this。

·StringBuilder append（char c）追加一个代码单元并返回 this。

·StringBuilder appendCodePoint（int cp）追加一个代码点，并将其转换为一个或两个代码单元并返回 this。

·void setCharAt（int i，char c）将第 i 个代码单元设置为 c。

·StringBuilder insert（int offset，String str）在 offset 位置插入一个字符串并返回 this。

·StringBuilder insert（int offset，Char c）在 offset 位置插入一个代码单元并返回 this。

·StringBuilder delete（int startIndex，int endIndex）删除偏移量从 startIndex 到 - endIndex-1 的代码单元并返回 this。

·String toString（）返回一个与构建器或缓冲器内容相同的字符串。

### 3.7 Input and Output

To make our example programs more interesting, we want to accept input and properly format the program output. Of course, modern programs use a GUI for collecting user input. However, programming such an interface requires more tools and techniques than we have at our disposal at this time. Our first order of business is to become more familiar with the Java programming language, so we use the humble console for input and output.

3.7 输入输出

为了增加后面示例程序的趣味性，需要程序能够接收输入，并以适当的格式输出。当然，现代的程序都使用 GUI 收集用户的输入，然而，编写这种界面的程序需要使用较多的工具与技术，目前还不具备这些条件。主要原因是需要熟悉 Java 程序设计语言，因此只要有简单的用于输入输出的控制台就可以了。第 10 章～第 12 章将详细地介绍 GUI 程序设计。

#### 3.7.1 Reading Input

You saw that it is easy to print output to the「standard output stream」(that is, the console window) just by calling System.out.println. Reading from the「standard input stream」System.in isn't quite as simple. To read console input, you first construct a Scanner that is attached to System.in:

Click here to view code image

Scanner in = new Scanner(System.in);

(We discuss constructors and the new operator in detail in Chapter 4.) Now you can use the various methods of the Scanner class to read input. For example, the nextLine method reads a line of input.

Click here to view code image

System.out.print("What is your name? ");

String name = in.nextLine();

Here, we use the nextLine method because the input might contain spaces. To read a single word (delimited by whitespace), call

Click here to view code image

String firstName = in.next();

To read an integer, use the nextInt method.

Click here to view code image

System.out.print("How old are you? ");

int age = in.nextInt();

Similarly, the nextDouble method reads the next floating-point number.

The program in Listing 3.2 asks for the user's name and age and then prints a message like

Click here to view code image

Hello, Cay. Next year, you'll be 57

Finally, note the line

Click here to view code image

import java.util.*;

at the beginning of the program. The Scanner class is defined in the java.util package. Whenever you use a class that is not defined in the basic java.lang package, you need to use an import directive. We look at packages and import directives in more detail in Chapter 4.

Listing 3.2 InputTest/InputTest.java

Click here to view code image

1 import java.util.*;

2

3 /**

4 * This program demonstrates console input.

5 * @version 1.10 2004-02-10

6 * @author Cay Horstmann

7 */

8 public class InputTest

9 {

10 public static void main(String[] args)

11 {

12 Scanner in = new Scanner(System.in);

13

14 // get first input

15 System.out.print("What is your name? ");

16 String name = in.nextLine();

17

18 // get second input

19 System.out.print("How old are you? ");

20 int age = in.nextInt();

21

22 // display output on console

23 System.out.println("Hello, " + name + ". Next year, you'll be " + (age + 1));

24 }

25 }

Note

The Scanner class is not suitable for reading a password from a console since the input is plainly visible to anyone. Java 6 introduces a Console class specifically for this purpose. To read a password, use the following code:

Click here to view code image

Console cons = System.console();

String username = cons.readLine("User name: ");

char[] passwd = cons.readPassword("Password: ");

For security reasons, the password is returned in an array of characters rather than a string. After you are done processing the password, you should immediately overwrite the array elements with a filler value. (Array processing is discussed in Section 3.10,「Arrays,」on p. 108.)

Input processing with a Console object is not as convenient as with a Scanner.You must read the input a line at a time. There are no methods for reading individual words or numbers.

java.util.Scanner 5

Scanner(InputStream in)

constructs a Scanner object from the given input stream.

String nextLine()

reads the next line of input.

String next()

reads the next word of input (delimited by whitespace).

int nextInt()

double nextDouble()

reads and converts the next character sequence that represents an integer or floating-point number.

boolean hasNext()

tests whether there is another word in the input.

boolean hasNextInt()

boolean hasNextDouble()

tests whether the next character sequence represents an integer or floating-point number.

java.lang.System 1.0

static Console console() 6

returns a Console object for interacting with the user through a console window if such interaction is possible, null otherwise. A Console object is available for any program that is launched in a console window. Otherwise, the availability is system-dependent.

java.io.Console 6

static char[] readPassword(String prompt, Object... args)

static String readLine(String prompt, Object... args)

displays the prompt and reads the user input until the end of the input line. The args parameters can be used to supply formatting arguments, as described in the next section.

3.7.1 读取输入

前面已经看到，打印输出到「标准输出流」（即控制台窗口）是一件非常容易的事情，只要调用 System.out.println 即可。然而，读取「标准输入流」System.in 就没有那么简单了。要想通过控制台进行输入，首先需要构造一个 Scanner 对象，并与「标准输入流」System.in 关联。

（构造函数和 new 操作符将在第 4 章中详细地介绍。）现在，就可以使用 Scanner 类的各种方法实现输入操作了。例如，nextLine 方法将输入一行。

在这里，使用 nextLine 方法是因为在输入行中有可能包含空格。要想读取一个单词（以空白符作为分隔符），就调用 要想读取一个整数，就调用 nextInt 方法。

与此类似，要想读取下一个浮点数，就调用 nextDouble 方法。在程序清单 3-2 的程序中，询问用户姓名和年龄，然后打印一条如下格式的消息： 最后，在程序的最开始添加上一行：

Scanner 类定义在 java.util 包中。当使用的类不是定义在基本 java.lang 包中时，一定要使用 import 指示字将相应的包加载进来。有关包与 import 指示字的详细描述请参看第 4 章。

程序清单 3-2 InputTest/InputTest.java

注释：因为输入是可见的，所以 Scanner 类不适用于从控制台读取密码。Java SE 6 特别引入了 Console 类实现这个目的。要想读取一个密码，可以采用下列代码：

为了安全起见，返回的密码存放在一维字符数组中，而不是字符串中。在对密码进行处理之后，应该马上用一个填充值覆盖数组元素（数组处理将在 3.10 节介绍）。

采用 Console 对象处理输入不如采用 Scanner 方便。每次只能读取一行输入，而没有能够读取一个单词或一个数值的方法。

java.util.Scanner 5.0·Scanner（InputStream in）用给定的输入流创建一个 Scanner 对象。

·String nextLine（）读取输入的下一行内容。

·String next（）读取输入的下一个单词（以空格作为分隔符）。

·int nextInt（）

·double nextDouble（）

读取并转换下一个表示整数或浮点数的字符序列。

·boolean hasNext（）检测输入中是否还有其他单词。

·boolean hasNextInt（）

·boolean hasNextDouble（）检测是否还有表示整数或浮点数的下一个字符序列。

java.lang.System 1.0

·static Console console（）6

如果有可能进行交互操作，就通过控制台窗口为交互的用户返回一个 Console 对象，否则返回 null。对于任何一个通过控制台窗口启动的程序，都可使用 Console 对象。否则，其可用性将与所使用的系统有关。

java.io.Console 6·static char[]readPassword（String prompt，Object...args）

·static String readLine（String prompt，Object...args）显示字符串 prompt 并且读取用户输入，直到输入行结束。args 参数可以用来提供输入格式。有关这部分内容将在下一节中介绍。

#### 3.7.2 Formatting Output

You can print a number x to the console with the statement System.out.print(x). That command will print x with the maximum number of nonzero digits for that type. For example,

Click here to view code image

double x = 10000.0 / 3.0;

System.out.print(x);

prints

3333.3333333333335

That is a problem if you want to display, for example, dollars and cents.

In early versions of Java, formatting numbers was a bit of a hassle. Fortunately, Java 5 brought back the venerable printf method from the C library. For example, the call

Click here to view code image

System.out.printf("%8.2f", x);

prints x with a field width of 8 characters and a precision of 2 characters. That is, the printout contains a leading space and the seven characters

3333.33

You can supply multiple parameters to printf. For example:

Click here to view code image

System.out.printf("Hello, %s. Next year, you'll be %d", name, age);

Each of the format specifiers that start with a % character is replaced with the corresponding argument. The conversion character that ends a format specifier indicates the type of the value to be formatted: f is a floating-point number, s a string, and d a decimal integer. Table 3.5 shows all conversion characters.

Table 3.5 Conversions for printf

Conversion Character

Type

Example

d

Decimal integer

159

x

Hexadecimal integer

9f

o

Octal integer

237

f

Fixed-point floating-point

15.9

e

Exponential floating-point

1.59e+01

g

General floating-point (the shorter of e and f)

—

a

Hexadecimal floating-point

0x1.fccdp3

s

String

Hello

c

Character

H

b

boolean

true

h

Hash code

42628b2

tx or Tx

Date and time (T forces uppercase)

Obsolete, use the java.time classes instead—see Chapter 6 of Volume II

%

The percent symbol

%

n

The platform-dependent line separator

—

In addition, you can specify flags that control the appearance of the formatted output. Table 3.6 shows all flags. For example, the comma flag adds group separators. That is,

Table 3.6 Flags for printf

Flag

Purpose

Example

+

Prints sign for positive and negative numbers.

+3333.33

space

Adds a space before positive numbers.

| 3333.33|

0

Adds leading zeroes.

003333.33

-

Left-justifies field.

|3333.33 |

(

Encloses negative numbers in parentheses.

(3333.33)

,

Adds group separators.

3,333.33

# (for f format)

Always includes a decimal point.

3,333.

# (for x or o format)

Adds 0x or 0 prefix.

0xcafe

$

Specifies the index of the argument to be formatted; for example, %1$d %1$x prints the first argument in decimal and hexadecimal.

159 9F

<

Formats the same value as the previous specification; for example, %d %<x prints the same number in decimal and hexadecimal.

159 9F

Click here to view code image

System.out.printf("%,.2f", 10000.0 / 3.0);

prints

3,333.33

You can use multiple flags, for example "%,(.2f" to use group separators and enclose negative numbers in parentheses.

Note

You can use the s conversion to format arbitrary objects. If an arbitrary object implements the Formattable interface, the object's formatTo method is invoked. Otherwise, the toString method is invoked to turn the object into a string. We discuss the toString method in Chapter 5 and interfaces in Chapter 6.

You can use the static String.format method to create a formatted string without printing it:

Click here to view code image

String message = String.format("Hello, %s. Next year, you'll be %d", name, age);

In the interest of completeness, we briefly discuss the date and time formatting options of the printf method. For new code, you should use the methods of the java.time package described in Chapter 6 of Volume II. But you may encounter the Date class and the associated formatting options in legacy code. The format consists of two letters, starting with t and ending in one of the letters of Table 3.7; for example,

Table 3.7 Date and Time Conversion Characters

Conversion Character

Type

Example

c

Complete date and time

Mon Feb 09 18:05:19 PST 2015

F

ISO 8601 date

2015-02-09

D

U.S. formatted date (month/day/year)

02/09/2015

T

24-hour time

18:05:19

r

12-hour time

06:05:19 pm

R

24-hour time, no seconds

18:05

Y

Four-digit year (with leading zeroes)

2015

y

Last two digits of the year (with leading zeroes)

15

C

First two digits of the year (with leading zeroes)

20

B

Full month name

February

b or h

Abbreviated month name

Feb

m

Two-digit month (with leading zeroes)

02

d

Two-digit day (with leading zeroes)

09

e

Two-digit day (without leading zeroes)

9

A

Full weekday name

Monday

a

Abbreviated weekday name

Mon

j

Three-digit day of year (with leading zeroes), between 001 and 366

069

H

Two-digit hour (with leading zeroes), between 00 and 23

18

k

Two-digit hour (without leading zeroes), between 0 and 23

18

I

Two-digit hour (with leading zeroes), between 01 and 12

06

l

Two-digit hour (without leading zeroes), between 1 and 12

6

M

Two-digit minutes (with leading zeroes)

05

S

Two-digit seconds (with leading zeroes)

19

L

Three-digit milliseconds (with leading zeroes)

047

N

Nine-digit nanoseconds (with leading zeroes)

047000000

p

Morning or afternoon marker

pm

z

RFC 822 numeric offset from GMT

-0800

Z

Time zone

PST

s

Seconds since 1970-01-01 00:00:00 GMT

1078884319

Q

Milliseconds since 1970-01-01 00:00:00 GMT

1078884319047

Click here to view code image

System.out.printf("%tc", new Date());

prints the current date and time in the format

Click here to view code image

Mon Feb 09 18:05:19 PST 2015

As you can see in Table 3.7, some of the formats yield only a part of a given date—for example, just the day or just the month. It would be a bit silly if you had to supply the date multiple times to format each part. For that reason, a format string can indicate the index of the argument to be formatted. The index must immediately follow the %, and it must be terminated by a $. For example,

Click here to view code image

System.out.printf("%1$s %2$tB %2$te, %2$tY", "Due date:", new Date());

prints

Click here to view code image

Due date: February 9, 2015

Alternatively, you can use the < flag. It indicates that the same argument as in the preceding format specification should be used again. That is, the statement

Click here to view code image

System.out.printf("%s %tB %<te, %<tY", "Due date:", new Date());

yields the same output as the preceding statement.

Caution

Argument index values start with 1, not with 0: %1$. . . formats the first argument. This avoids confusion with the 0 flag.

You have now seen all features of the printf method. Figure 3.6 shows a syntax diagram for format specifiers.

Figure 3.6 Format specifier syntax

Note

The formatting of numbers and dates is locale-specific. For example, in Germany, the group separator is a period, not a comma, and Monday is formatted as Montag. Chapter 7 of Volume II shows how to control the international behavior of your applications.

3.7.2 格式化输出

可以使用 System.out.print（x）将数值 x 输出到控制台上。这条命令将以 x 对应的数据类型所允许的最大非 0 数字位数打印输出 x。例如：

打印

如果希望显示美元、美分等符号，则有可能会出现问题。在早期的 Java 版本中，格式化数值曾引起过一些争议。庆幸的是，Java SE5.0 沿用了 C 语言库函数中的 printf 方法。例如，调用 可以用 8 个字符的宽度和小数点后两个字符的精度打印 x。也就是说，打印输出一个空格和 7 个字符，如下所示：

在 printf 中，可以使用多个参数，例如：

每一个以 % 字符开始的格式说明符都用相应的参数替换。格式说明符尾部的转换符将指示被格式化的数值类型：f 表示浮点数，s 表示字符串，d 表示十进制整数。表 3-5 列出了所有转换符。

表 3-5 用于 printf 的转换符

另外，还可以给出控制格式化输出的各种标志。表 3-6 列出了所有的标志。例如，逗号标志增加了分组的分隔符。即表 3-6 用于 printf 的标志

打印

可以使用多个标志，例如，「%，（.2f」使用分组的分隔符并将负数括在括号内。

注释：可以使用 s 转换符格式化任意的对象。对于任意实现了 Formattable 接口的对象都将调用 formatTo 方法；否则将调用 toString 方法，它可以将对象转换为字符串。在第 5 章中将讨论 toString 方法，在第 6 章中将讨论接口。

可以使用静态的 String.format 方法创建一个格式化的字符串，而不打印输出：

基于完整性的考虑，下面简略地介绍 printf 方法中日期与时间的格式化选项。在新代码中，应当使用卷 Ⅱ 第 6 章中介绍的 java.time 包的方法。不过你可能会在遗留代码中看到 Date 类和相关的格式化选项。格式包括两个字母，以 t 开始，以表 3-7 中的任意字母结束。例如，

这条语句将用下面的格式打印当前的日期和时间：

从表 3-7 可以看到，某些格式只给出了指定日期的部分信息。例如，只有日期或月份。如果需要多次对日期操作才能实现对每一部分进行格式化的目的就太笨拙了。为此，可以采用一个格式化的字符串指出要被格式化的参数索引。索引必须紧跟在 % 后面，并以 $ 终止。例如，

表 3-7 日期和时间的转换符

打印

还可以选择使用 < 标志。它指示前面格式说明中的参数将被再次使用。也就是说，下列语句将产生与前面语句同样的输出结果：

提示：参数索引值从 1 开始，而不是从 0 开始，%1$... 对第 1 个参数格式化。这就避免了与 0 标志混淆。现在，已经了解了 printf 方法的所有特性。图 3-6 给出了格式说明符的语法图。

图 3-6 格式说明符语法

注释：许多格式化规则是本地环境特有的。例如，在德国，组分隔符是句号而不是逗号，Monday 被格式化为 Montag。在卷 Ⅱ 第 5 章中将介绍如何控制应用的国际化行为。

#### 3.7.3 File Input and Output

To read from a file, construct a Scanner object like this:

Click here to view code image

Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8);

If the file name contains backslashes, remember to escape each of them with an additional backslash: "c:\\mydirectory\\myfile.txt".

Note

Here, we specify the UTF-8 character encoding, which is common (but not universal) for files on the Internet. You need to know the character encoding when you read a text file (see Volume II, Chapter 2 for more information). If you omit the character encoding, then the「default encoding」of the computer running the Java program is used. That is not a good idea—the program might act differently depending on where it is run.

Now you can read from the file, using any of the Scanner methods that we already described.

To write to a file, construct a PrintWriter object. In the constructor, supply the file name and the character encoding:

Click here to view code image

PrintWriter out = new PrintWriter("myfile.txt", StandardCharsets.UTF_8);

If the file does not exist, it is created. You can use the print, println, and printf commands as you did when printing to System.out.

Caution

You can construct a Scanner with a string parameter, but the scanner interprets the string as data, not a file name. For example, if you call

Click here to view code image

Scanner in = new Scanner("myfile.txt"); // ERROR?

then the scanner will see ten characters of data: 'm', 'y', 'f', and so on. That is probably not what was intended in this case.

Note

When you specify a relative file name, such as "myfile.txt", "mydirectory/myfile.txt", or "../myfile.txt", the file is located relative to the directory in which the Java virtual machine was started. If you launched your program from a command shell, by executing

java MyProg

then the starting directory is the current directory of the command shell. However, if you use an integrated development environment, it controls the starting directory. You can find the directory location with this call:

Click here to view code image

String dir = System.getProperty("user.dir");

If you run into grief with locating files, consider using absolute path names such as "c:\\mydirectory\\myfile.txt" or "/home/me/mydirectory/myfile.txt".

As you saw, you can access files just as easily as you can use System.in and System.out. There is just one catch: If you construct a Scanner with a file that does not exist or a PrintWriter with a file name that cannot be created, an exception occurs. The Java compiler considers these exceptions to be more serious than a「divide by zero」exception, for example. In Chapter 7, you will learn various ways of handling exceptions. For now, you should simply tell the compiler that you are aware of the possibility of an「input/output」exception. You do this by tagging the main method with a throws clause, like this:

Click here to view code image

public static void main(String[] args) throws IOException

{

Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8);

. . .

}

You have now seen how to read and write files that contain textual data. For more advanced topics, such as dealing with different character encodings, processing binary data, reading directories, and writing zip files, turn to Chapter 2 of Volume II.

Note

When you launch a program from a command shell, you can use the redirection syntax of your shell and attach any file to System.in and System.out:

Click here to view code image

java MyProg < myfile.txt > output.txt

Then, you need not worry about handling the IOException.

java.util.Scanner 5

Scanner(Path p, String encoding)

constructs a Scanner that reads data from the given path, using the given character encoding.

Scanner(String data)

constructs a Scanner that reads data from the given string.

java.io.PrintWriter 1.1

PrintWriter(String fileName)

constructs a PrintWriter that writes data to the file with the given file name.

java.nio.file.Path

static Path of(String pathname) 11

constructs a Path from the given path name.

3.7.3 文件输入与输出

要想对文件进行读取，就需要一个用 File 对象构造一个 Scanner 对象，如下所示：

如果文件名中包含反斜杠符号，就要记住在每个反斜杠之前再加一个额外的反斜杠：「c：\\mydirectory\\myfile.txt」。

注释：在这里指定了 UTF-8 字符编码，这对于互联网上的文件很常见（不过并不是普遍适用）。读取一个文本文件时，要知道它的字符编码 —— 更多信息参见卷 Ⅱ 第 2 章。如果省略字符编码，则会使用运行这个 Java 程序的机器的「默认编码」。这不是一个好主意，如果在不同的机器上运行这个程序，可能会有不同的表现。

现在，就可以利用前面介绍的任何一个 Scanner 方法对文件进行读取。要想写入文件，就需要构造一个 PrintWriter 对象。在构造器中，只需要提供文件名：

如果文件不存在，创建该文件。可以像输出到 System.out 一样使用 print、println 以及 printf 命令。

警告：可以构造一个带有字符串参数的 Scanner，但这个 Scanner 将字符串解释为数据，而不是文件名。例如，如果调用：

这个 scanner 会将参数作为包含 10 个字符的数据：‘m'，‘y'，‘f' 等。在这个示例中所显示的并不是人们所期望的效果。

注释：当指定一个相对文件名时，例如，「myfile.txt」，「mydirectory/myfile.txt」或「../myfile.txt」，文件位于 Java 虚拟机启动路径的相对位置。如果在命令行方式下用下列命令启动程序：

启动路径就是命令解释器的当前路径。然而，如果使用集成开发环境，那么启动路径将由 IDE 控制。可以使用下面的调用方式找到路径的位置：

如果觉得定位文件比较烦恼，则可以考虑使用绝对路径，例如：「c：\\mydirectory\\myfile.txt」或者「/home/me/mydirectory/myfile.txt」。

正如读者所看到的，访问文件与使用 System.in 和 System.out 一样容易。要记住一点：如果用一个不存在的文件构造一个 Scanner，或者用一个不能被创建的文件名构造一个 PrintWriter，那么就会发生异常。Java 编译器认为这些异常比「被零除」异常更严重。在第 7 章中，将会学习各种处理异常的方式。现在，应该告知编译器：已经知道有可能出现「输入 / 输出」异常。这需要在 main 方法中用 throws 子句标记，如下所示：

现在读者已经学习了如何读写包含文本数据的文件。对于更加高级的技术，例如，处理不同的字符编码、处理二进制数据、读取目录以及写压缩文件，请参看卷 Ⅱ 第 2 章。

注释：当采用命令行方式启动一个程序时，可以利用 Shell 的重定向语法将任意文件关联到 System.in 和 System.out：

这样，就不必担心处理 IOException 异常了。

java.util.Scanner 5.0·Scanner（File f）构造一个从给定文件读取数据的 Scanner。

·Scanner（String data）构造一个从给定字符串读取数据的 Scanner。

构造一个从给定字符串读取数据的 Scanner。

java.io.PrintWriter 1.1·PrintWriter（String fileName）构造一个将数据写入文件的 PrintWriter。文件名由参数指定。

java.nio.file.Paths 7·static Path get（String pathname）根据给定的路径名构造一个 Path。

### 3.8 Control Flow

Java, like any programming language, supports both conditional statements and loops to determine control flow. We will start with the conditional statements, then move on to loops, to end with the somewhat cumbersome switch statement that you can use to test for many values of a single expression.

C++ Note

The Java control flow constructs are identical to those in C and C++, with a few exceptions. There is no goto, but there is a「labeled」version of break that you can use to break out of a nested loop (where, in C, you perhaps would have used a goto). Finally, there is a variant of the for loop that is similar to the range-based for loop in C++ and the foreach loop in C#.

3.8 控制流程

与任何程序设计语言一样，Java 使用条件语句和循环结构确定控制流程。本节先讨论条件语句，然后讨论循环语句，最后介绍看似有些笨重的 switch 语句，当需要对某个表达式的多个值进行检测时，可以使用 switch 语句。

C++ 注释：Java 的控制流程结构与 C 和 C++ 的控制流程结构一样，只有很少的例外情况。没有 goto 语句，但 break 语句可以带标签，可以利用它实现从内层循环跳出的目的（这种情况 C 语言采用 goto 语句实现）。另外，还有一种变形的 for 循环，在 C 或 C++ 中没有这类循环。它有点类似于 C# 中的 foreach 循环。

#### 3.8.1 Block Scope

Before learning about control structures, you need to know more about blocks.

A block, or compound statement, consists of a number of Java statements, surrounded by a pair of braces. Blocks define the scope of your variables. A block can be nested inside another block. Here is a block that is nested inside the block of the main method:

Click here to view code image

public static void main(String[] args)

{

int n;

. . .

{

int k;

. . .

} // k is only defined up to here

}

You may not declare identically named variables in two nested blocks. For example, the following is an error and will not compile:

Click here to view code image

public static void main(String[] args)

{

int n;

. . .

{

int k;

int n; // ERROR--can't redefine n in inner block

. . .

}

}

C++ Note

In C++, it is possible to redefine a variable inside a nested block. The inner definition then shadows the outer one. This can be a source of programming errors; hence, Java does not allow it.

3.8.1 块作用域

在深入学习控制结构之前，需要了解块（block）的概念。块（即复合语句）是指由一对大括号括起来的若干条简单的 Java 语句。块确定了变量的作用域。一个块可以嵌套在另一个块中。下面就是在 main 方法块中嵌套另一个语句块的示例。

但是，不能在嵌套的两个块中声明同名的变量。例如，下面的代码就有错误，而无法通过编译：

C++ 注释：在 C++ 中，可以在嵌套的块中重定义一个变量。在内层定义的变量会覆盖在外层定义的变量。这样，有可能会导致程序设计错误，因此在 Java 中不允许这样做。

#### 3.8.2 Conditional Statements

The conditional statement in Java has the form

if (condition) statement

The condition must be surrounded by parentheses.

In Java, as in most programming languages, you will often want to execute multiple statements when a single condition is true. In this case, use a block statement that takes the form

{

statement1

statement2

. . .

}

For example:

Click here to view code image

if (yourSales >= target)

{

performance = "Satisfactory";

bonus = 100;

}

In this code all the statements surrounded by the braces will be executed when yourSales is greater than or equal to target (see Figure 3.7).

Figure 3.7 Flowchart for the if statement

Note

A block (sometimes called a compound statement) enables you to have more than one (simple) statement in any Java programming structure that otherwise allows for a single (simple) statement.

The more general conditional in Java looks like this (see Figure 3.8):

Figure 3.8 Flowchart for the if/else statement

Click here to view code image

if (condition) statement1 else statement2

For example:

Click here to view code image

if (yourSales >= target)

{

performance = "Satisfactory";

bonus = 100 + 0.01 * (yourSales - target);

}

else

{

performance = "Unsatisfactory";

bonus = 0;

}

The else part is always optional. An else groups with the closest if. Thus, in the statement

Click here to view code image

if (x <= 0) if (x == 0) sign = 0; else sign = -1;

the else belongs to the second if. Of course, it is a good idea to use braces to clarify this code:

Click here to view code image

if (x <= 0) { if (x == 0) sign = 0; else sign = -1; }

Repeated if . . . else if . . . alternatives are common (see Figure 3.9). For example:

Figure 3.9 Flowchart for the if/else if (multiple branches)

Click here to view code image

if (yourSales >= 2 * target)

{

performance = "Excellent";

bonus = 1000;

}

else if (yourSales >= 1.5 * target)

{

performance = "Fine";

bonus = 500;

}

else if (yourSales >= target)

{

performance = "Satisfactory";

bonus = 100;

}

else

{

System.out.println("You're fired");

}

3.8.2 条件语句

在 Java 中，条件语句的格式为 这里的条件必须用括号括起来。与绝大多数程序设计语言一样，Java 常常希望在某个条件为真时执行多条语句。在这种情况下，应该使用块语句（block statement），形式为

例如：

当 yourSales 大于或等于 target 时，将执行括号中的所有语句（请参看图 3-7）。

图 3-7 if 语句的流程图

注释：使用块（有时称为复合语句）可以在 Java 程序结构中原本只能放置一条（简单）语句的地方放置多条语句。

在 Java 中，更一般的条件语句格式如下所示（请参看图 3-8）：

图 3-8 if/else 语句的流程图

例如：

其中 else 部分是可选的。else 子句与最邻近的 if 构成一组。因此，在语句

中 else 与第 2 个 if 配对。当然，用一对括号将会使这段代码更加清晰：

重复地交替出现 if...else if... 是一种很常见的情况（请参看图 3-9）。例如：

图 3-9 if/else if（多分支）的流程图

#### 3.8.3 Loops

The while loop executes a statement (which may be a block statement) while a condition is true. The general form is

Click here to view code image

while (condition) statement

The while loop will never execute if the condition is false at the outset (see Figure 3.10).

Figure 3.10 Flowchart for the while statement

The program in Listing 3.3 determines how long it will take to save a specific amount of money for your well-earned retirement, assuming you deposit the same amount of money per year and the money earns a specified interest rate.

In the example, we are incrementing a counter and updating the amount currently accumulated in the body of the loop until the total exceeds the targeted amount.

Click here to view code image

while (balance < goal)

{

balance += payment;

double interest = balance * interestRate / 100;

balance += interest;

years++;

}

System.out.println(years + " years.");

(Don't rely on this program to plan for your retirement. We left out a few niceties such as inflation and your life expectancy.)

A while loop tests at the top. Therefore, the code in the block might never be executed. If you want to make sure a block is executed at least once, you need to move the test to the bottom, using the do/while loop. Its syntax looks like this:

Click here to view code image

do statement while (condition);

This loop executes the statement (which is typically a block) and only then tests the condition. If it's true, it repeats the statement and retests the condition, and so on. The code in Listing 3.4 computes the new balance in your retirement account and then asks if you are ready to retire:

Click here to view code image

do

{

balance += payment;

double interest = balance * interestRate / 100;

balance += interest;

year++;

// print current balance

. . .

// ask if ready to retire and get input

. . .

}

while (input.equals("N"));

As long as the user answers "N", the loop is repeated (see Figure 3.11). This program is a good example of a loop that needs to be entered at least once, because the user needs to see the balance before deciding whether it is sufficient for retirement.

Figure 3.11 Flowchart for the do/while statement

Listing 3.3 Retirement/Retirement.java

Click here to view code image

1 import java.util.*;

2

3 /**

4 * This program demonstrates a while loop.

5 * @version 1.20 2004-02-10

6 * @author Cay Horstmann

7 */

8 public class Retirement

9 {

10 public static void main(String[] args)

11 {

12 // read inputs

13 Scanner in = new Scanner(System.in);

14

15 System.out.print("How much money do you need to retire? ");

16 double goal = in.nextDouble();

17

18 System.out.print("How much money will you contribute every year? ");

19 double payment = in.nextDouble();

20

21 System.out.print("Interest rate in %: ");

22 double interestRate = in.nextDouble();

23

24 double balance = 0;

25 int years = 0;

26

27 // update account balance while goal isn't reached

28 while (balance > goal)

29 {

30 // add this year's payment and interest

31 balance += payment;

32 double interest = balance * interestRate / 100;

33 balance += interest;

34 years++;

35 }

36

37 System.out.println("You can retire in " + years + " years.");

38 }

39 }

Listing 3.4 Retirement2/Retirement2.java

Click here to view code image

1 import java.util.*;

2

3 /**

4 * This program demonstrates a do/while loop.

5 * @version 1.20 2004-02-10

6 * @author Cay Horstmann

7 */

8 public class Retirement2

9 {

10 public static void main(String[] args)

11 {

12 Scanner in = new Scanner(System.in);

13

14 System.out.print("How much money will you contribute every year? ");

15 double payment = in.nextDouble();

16

17 System.out.print("Interest rate in %: ");

18 double interestRate = in.nextDouble();

19

20 double balance = 0;

21 int year = 0;

22

23 String input;

24

25 // update account balance while user isn't ready to retire

26 do

27 {

28 // add this year's payment and interest

29 balance += payment;

30 double interest = balance * interestRate / 100;

31 balance += interest;

32

33 year++;

34

35 // print current balance

36 System.out.printf("After year %d, your balance is %,.2f%n", year, balance);

37

38 // ask if ready to retire and get input

39 System.out.print("Ready to retire? (Y/N) ");

40 input = in.next();

41 }

42 while (input.equals("N"));

43 }

44 }

3.8.3 循环

当条件为 true 时，while 循环执行一条语句（也可以是一个语句块）。一般格式为

如果开始循环条件的值就为 false，则 while 循环体一次也不执行（请参看图 3-10）。

图 3-10 while 语句的流程图

程序清单 3-3 中的程序将计算需要多长时间才能够存储一定数量的退休金，假定每年存入相同数量的金额，而且利率是固定的。

程序清单 3-3 Retirement/Retirement.java

在这个示例中，增加了一个计数器，并在循环体中更新当前的累积数量，直到总值超过目标值为止。

（千万不要使用这个程序安排退休计划。这里忽略了通货膨胀和所期望的生活水准。）

while 循环语句首先检测循环条件。因此，循环体中的代码有可能不被执行。如果希望循环体至少执行一次，则应该将检测条件放在最后。使用 do/while 循环语句可以实现这种操作方式。它的语法格式为：

这种循环语句先执行语句（通常是一个语句块），再检测循环条件；然后重复语句，再检测循环条件，以此类推。在程序清单 3-4 中，首先计算退休账户中的余额，然后再询问是否打算退休：

只要用户回答「N」，循环就重复执行（见图 3-11）。这是一个需要至少执行一次的循环的很好示例，因为用户必须先看到余额才能知道是否满足退休所用。

程序清单 3-4 Retirement2/Retirement2.java

#### 3.8.4 Determinate Loops

The for loop is a general construct to support iteration controlled by a counter or similar variable that is updated after every iteration. As Figure 3.12 shows, the following loop prints the numbers from 1 to 10 on the screen:

Figure 3.12 Flowchart for the for statement

for (int i = 1; i <= 10; i++)

System.out.println(i);

The first slot of the for statement usually holds the counter initialization. The second slot gives the condition that will be tested before each new pass through the loop, and the third slot specifies how to update the counter.

Although Java, like C++, allows almost any expression in the various slots of a for loop, it is an unwritten rule of good taste that the three slots should only initialize, test, and update the same counter variable. One can write very obscure loops by disregarding this rule.

Even within the bounds of good taste, much is possible. For example, you can have loops that count down:

for (int i = 10; i > 0; i--)

System.out.println("Counting down . . . " + i);

System.out.println("Blastoff!");

Caution

Be careful with testing for equality of floating-point numbers in loops. A for loop like this one

Click here to view code image

for (double x = 0; x != 10; x += 0.1) . . .

might never end. Because of roundoff errors, the final value might not be reached exactly. In this example, x jumps from 9.99999999999998 to 10.09999999999998 because there is no exact binary representation for 0.1.

When you declare a variable in the first slot of the for statement, the scope of that variable extends until the end of the body of the for loop.

Click here to view code image

for (int i = 1; i <= 10; i++)

{

. . .

}

// i no longer defined here

In particular, if you define a variable inside a for statement, you cannot use its value outside the loop. Therefore, if you wish to use the final value of a loop counter outside the for loop, be sure to declare it outside the loop header.

Click here to view code image

int i;

for (i = 1; i <= 10; i++)

{

. . .

}

// i is still defined here

On the other hand, you can define variables with the same name in separate for loops:

Click here to view code image

for (int i = 1; i <= 10; i++)

{

. . .

}

. . .

for (int i = 11; i <= 20; i++) // OK to define another variable named i

{

. . .

}

A for loop is merely a convenient shortcut for a while loop. For example,

Click here to view code image

for (int i = 10; i > 0; i--)

System.out.println("Counting down . . . " + i);

can be rewritten as

Click here to view code image

int i = 10;

while (i > 0)

{

System.out.println("Counting down . . . " + i);

i--;

}

Listing 3.5 shows a typical example of a for loop.

The program computes the odds of winning a lottery. For example, if you must pick six numbers from the numbers 1 to 50 to win, then there are (50 × 49 × 48 × 47 × 46 × 45)/(1 × 2 × 3 × 4 × 5 × 6) possible outcomes, so your chance is 1 in 15,890,700. Good luck!

In general, if you pick k numbers out of n, there are

possible outcomes. The following for loop computes this value:

Click here to view code image

int lotteryOdds = 1;

for (int i = 1; i <= k; i++)

lotteryOdds = lotteryOdds * (n - i + 1) / i;

Note

See Section 3.10.3,「The ‘for each' Loop,」on p. 110 for a description of the「generalized for loop」(also called「for each」loop) that was added to the Java language in Java 5.

Listing 3.5 LotteryOdds/LotteryOdds.java

Click here to view code image

1 import java.util.*;

2 3 /**

4 * This program demonstrates a for loop.

5 * @version 1.20 2004-02-10

6 * @author Cay Horstmann

7 */

8 public class LotteryOdds

9 {

10 public static void main(String[] args)

11 {

12 Scanner in = new Scanner(System.in);

13

14 System.out.print("How many numbers do you need to draw? ");

15 int k = in.nextInt();

16

17 System.out.print("What is the highest number you can draw? ");

18 int n = in.nextInt();

19

20 /*

21 * compute binomial coefficient n*(n-1)*(n-2)*...*(n-k+1)/(1*2*3*...*k)

22 */

23

24 int lotteryOdds = 1;

25 for (int i = 1; i <= k; i++)

26 lotteryOdds = lotteryOdds * (n - i + 1) / i;

27

28 System.out.println("Your odds are 1 in " + lotteryOdds + ". Good luck!");

29 }

30 }

3.8.4 确定循环

for 循环语句是支持迭代的一种通用结构，利用每次迭代之后更新的计数器或类似的变量来控制迭代次数。如图 3-12 所示，下面的程序将数字 1~10 输出到屏幕上。

图 3-11 do/while 语句的流程图

图 3-12 for 语句的流程图

for 语句的第 1 部分通常用于对计数器初始化；第 2 部分给出每次新一轮循环执行前要检测的循环条件；第 3 部分指示如何更新计数器。

与 C++ 一样，尽管 Java 允许在 for 循环的各个部分放置任何表达式，但有一条不成文的规则：for 语句的 3 个部分应该对同一个计数器变量进行初始化、检测和更新。若不遵守这一规则，编写的循环常常晦涩难懂。

即使遵守了这条规则，也还有可能出现很多问题。例如，下面这个倒计数的循环：

警告：在循环中，检测两个浮点数是否相等需要格外小心。下面的 for 循环

可能永远不会结束。由于舍入的误差，最终可能得不到精确值。例如，在上面的循环中，因为 0.1 无法精确地用二进制表示，所以，x 将从 9.99999999999998 跳到 10.09999999999998。当在 for 语句的第 1 部分中声明了一个变量之后，这个变量的作用域就为 for 循环的整个循环体。

特别指出，如果在 for 语句内部定义一个变量，这个变量就不能在循环体之外使用。因此，如果希望在 for 循环体之外使用循环计数器的最终值，就要确保这个变量在循环语句的前面且在外部声明！

另一方面，可以在各自独立的不同 for 循环中定义同名的变量：

for 循环语句只不过是 while 循环的一种简化形式。例如，

可以重写为：

程序清单 3-5 给出了一个应用 for 循环的典型示例。这个程序用来计算抽奖中奖的概率。例如，如果必须从 1~50 之间的数字中取 6 个数字来抽奖，那么会有（50×49×48×47×46×45）/（1×2×3×4×5×6）种可能的结果，所以中奖的几率是 1/15890700。祝你好运！

程序清单 3-5 LotteryOdds/LotteryOdds.java

一般情况下，如果从 n 个数字中抽取 k 个数字，就可以使用下列公式得到结果。

下面的 for 循环语句计算了上面这个公式的值：

注释：3.10.1 节将会介绍「通用 for 循环」（又称为 for each 循环），这是 Java SE 5.0 新增加的一种循环结构。

#### 3.8.5 Multiple Selections–The switch Statement

The if/else construct can be cumbersome when you have to deal with multiple selections with many alternatives. Java has a switch statement that is exactly like the switch statement in C and C++, warts and all.

For example, if you set up a menu system with four alternatives like that in Figure 3.13, you could use code that looks like this:

Figure 3.13 Flowchart for the switch statement

Click here to view code image

Scanner in = new Scanner(System.in);

System.out.print("Select an option (1, 2, 3, 4) ");

int choice = in.nextInt();

switch (choice)

{

case 1:

. . .

break;

case 2:

. . .

break;

case 3:

. . .

break;

case 4:

. . .

break;

default:

// bad input

. . .

break;

}

Execution starts at the case label that matches the value on which the selection is performed and continues until the next break or the end of the switch. If none of the case labels match, then the default clause is executed, if it is present.

Caution

It is possible for multiple alternatives to be triggered. If you forget to add a break at the end of an alternative, execution falls through to the next alternative! This behavior is plainly dangerous and a common cause for errors. For that reason, we never use the switch statement in our programs.

If you like the switch statement better than we do, consider compiling your code with the -Xlint:fallthrough option, like this:

javac -Xlint:fallthrough Test.java

Then the compiler will issue a warning whenever an alternative does not end with a break statement.

If you actually want to use the fallthrough behavior, tag the surrounding method with the annotation @SuppressWarnings("fallthrough"). Then no warnings will be generated for that method. (An annotation is a mechanism for supplying information to the compiler or a tool that processes Java source or class files. We discuss annotations in detail in Chapter 8 of Volume II.)

A case label can be

A constant expression of type char, byte, short, or int

An enumerated constant

Starting with Java 7, a string literal

For example,

Click here to view code image

String input = . . .;

switch (input.toLowerCase())

{

case "yes": // OK since Java 7

. . .

break;

. . .

}

When you use the switch statement with enumerated constants, you need not supply the name of the enumeration in each label—it is deduced from the

Click here to view code image

Size sz = . . .;

switch (sz)

{

case SMALL: // no need to use Size.SMALL

. . .

break;

. . .

}

3.8.5 多重选择：switch 语句

在处理多个选项时，使用 if/else 结构显得有些笨拙。Java 有一个与 C/C++ 完全一样的 switch 语句。

例如，如果建立一个如图 3-13 所示的包含 4 个选项的菜单系统，可以使用下列代码：

图 3-13 switch 语句的流程图

switch 语句将从与选项值相匹配的 case 标签处开始执行直到遇到 break 语句，或者执行到 switch 语句的结束处为止。如果没有相匹配的 case 标签，而有 default 子句，就执行这个子句。

警告：有可能触发多个 case 分支。如果在 case 分支语句的末尾没有 break 语句，那么就会接着执行下一个 case 分支语句。这种情况相当危险，常常会引发错误。为此，我们在程序中从不使用 switch 语句。如果你比我们更喜欢 switch 语句，编译代码时可以考虑加上 - Xlint：fallthrough 选项，如下所示：

这样一来，如果某个分支最后缺少一个 break 语句，编译器就会给出一个警告消息。如果你确实正是想使用这种「直通式」（fallthrough）行为，可以为其外围方法加一个标注 @SuppressWarnings（"fallthrough"）。这样就不会对这个方法生成警告了。（标注是为编译器或处理 Java 源文件或类文件的工具提供信息的一种机制。我们将在卷 Ⅱ 的第 8 章详细讨论标注。）case 标签可以是：

·类型为 char、byte、short 或 int 的常量表达式。

·枚举常量。

·从 Java SE 7 开始，case 标签还可以是字符串字面量。例如：

当在 switch 语句中使用枚举常量时，不必在每个标签中指明枚举名，可以由 switch 的表达式值确定。例如：

3.8.6 中断控制流程语句

尽管 Java 的设计者将 goto 作为保留字，但实际上并没有打算在语言中使用它。通常，使用 goto 语句被认为是一种拙劣的程序设计风格。当然，也有一些程序员认为反对 goto 的呼声似乎有些过分（例如，Donald Knuth 就曾编著过一篇名为《Structured Programming with goto statements》的著名文章）。这篇文章说：无限制地使用 goto 语句确实是导致错误的根源，但在有些情况下，偶尔使用 goto 跳出循环还是有益处的。Java 设计者同意这种看法，甚至在 Java 语言中增加了一条带标签的 break，以此来支持这种程序设计风格。

下面首先看一下不带标签的 break 语句。与用于退出 switch 语句的 break 语句一样，它也可以用于退出循环语句。例如，

在循环开始时，如果 years>100，或者在循环体中 balance≥goal，则退出循环语句。当然，也可以在不使用 break 的情况下计算 years 的值，如下所示：

但是需要注意，在这个版本中，检测了两次 balance<goal。为了避免重复检测，有些程序员更加偏爱使用 break 语句。与 C++ 不同，Java 还提供了一种带标签的 break 语句，用于跳出多重嵌套的循环语句。有时候，在嵌套很深的循环语句中会发生一些不可预料的事情。此时可能更加希望跳到嵌套的所有循环语句之外。通过添加一些额外的条件判断实现各层循环的检测很不方便。

这里有一个示例说明了 break 语句的工作状态。请注意，标签必须放在希望跳出的最外层循环之前，并且必须紧跟一个冒号。

如果输入有误，通过执行带标签的 break 跳转到带标签的语句块末尾。对于任何使用 break 语句的代码都需要检测循环是正常结束，还是由 break 跳出。

注释：事实上，可以将标签应用到任何语句中，甚至可以应用到 if 语句或者块语句中，如下所示： 因此，如果希望使用一条 goto 语句，并将一个标签放在想要跳到的语句块之前，就可以使用 break 语句！当然，并不提倡使用这种方式。另外需要注意，只能跳出语句块，而不能跳入语句块。最后，还有一个 continue 语句。与 break 语句一样，它将中断正常的控制流程。continue 语句将控制转移到最内层循环的首部。例如：

如果 n<0，则 continue 语句越过了当前循环体的剩余部分，立刻跳到循环首部。如果将 continue 语句用于 for 循环中，就可以跳到 for 循环的「更新」部分。例如，下面这个循环：

如果将 continue 语句用于 for 循环中，就可以跳到 for 循环的「更新」部分。例如，下面这个循环：

如果 n<0，则 continue 语句跳到 count++ 语句。还有一种带标签的 continue 语句，将跳到与标签匹配的循环首部。

提示：许多程序员容易混淆 break 和 continue 语句。这些语句完全是可选的，即不使用它们也可以表达同样的逻辑含义。在本书中，将不使用 break 和 continue。

#### 3.8.6 Statements That Break Control Flow

Although the designers of Java kept goto as a reserved word, they decided not to include it in the language. In general, goto statements are considered poor style. Some programmers feel the anti-goto forces have gone too far (see, for example, the famous article of Donald Knuth called「Structured Programming with goto statements」). They argue that unrestricted use of goto is error-prone but that an occasional jump out of a loop is beneficial. The Java designers agreed and even added a new statement, the labeled break, to support this programming style.

Let us first look at the unlabeled break statement. The same break statement that you use to exit a switch can also be used to break out of a loop. For example:

Click here to view code image

while (years <= 100)

{

balance += payment;

double interest = balance * interestRate / 100;

balance += interest;

if (balance >= goal) break;

years++;

}

Now the loop is exited if either years > 100 occurs at the top of the loop or balance >= goal occurs in the middle of the loop. Of course, you could have computed the same value for years without a break, like this:

Click here to view code image

while (years <= 100 && balance < goal)

{

balance += payment;

double interest = balance * interestRate / 100;

balance += interest;

if (balance < goal)

years++;

}

But note that the test balance < goal is repeated twice in this version. To avoid this repeated test, some programmers prefer the break statement.

Unlike C++, Java also offers a labeled break statement that lets you break out of multiple nested loops. Occasionally something weird happens inside a deeply nested loop. In that case, you may want to break completely out of all the nested loops. It is inconvenient to program that simply by adding extra conditions to the various loop tests.

Here's an example that shows the break statement at work. Notice that the label must precede the outermost loop out of which you want to break. It also must be followed by a colon.

Click here to view code image

Scanner in = new Scanner(System.in);

int n;

read_data:

while (. . .) // this loop statement is tagged with the label

{

. . .

for (. . .) // this inner loop is not labeled

{

System.out.print("Enter a number >= 0: ");

n = in.nextInt();

if (n < 0) // should never happen—can't go on

break read_data;

// break out of read_data loop

. . .

}

}

// this statement is executed immediately after the labeled break

if (n < 0) // check for bad situation

{

// deal with bad situation

}

else

{

// carry out normal processing

}

If there is a bad input, the labeled break moves past the end of the labeled block. As with any use of the break statement, you then need to test whether the loop exited normally or as a result of a break.

Note

Curiously, you can apply a label to any statement, even an if statement or a block statement, like this:

Click here to view code image

label:

{

. . .

if (condition) break label; // exits block

. . .

}

// jumps here when the break statement executes

Thus, if you are lusting after a goto but you can place a block that ends just before the place to which you want to jump, you can use a break statement! Naturally, we don't recommend this approach. Note, however, that you can only jump out of a block, never into a block.

Finally, there is a continue statement that, like the break statement, breaks the regular flow of control. The continue statement transfers control to the header of the innermost enclosing loop. Here is an example:

Click here to view code image

Scanner in = new Scanner(System.in);

while (sum < goal)

{

System.out.print("Enter a number: ");

n = in.nextInt();

if (n < 0) continue;

sum += n; // not executed if n < 0

}

If n < 0, then the continue statement jumps immediately to the loop header, skipping the remainder of the current iteration.

If the continue statement is used in a for loop, it jumps to the「update」part of the for loop. For example:

Click here to view code image

for (count = 1; count <= 100; count++)

{

System.out.print("Enter a number, -1 to quit: ");

n = in.nextInt();

if (n < 0) continue;

sum += n; // not executed if n < 0

}

If n < 0, then the continue statement jumps to the count++ statement.

There is also a labeled form of the continue statement that jumps to the header of the loop with the matching label.

Tip

Many programmers find the break and continue statements confusing. These statements are entirely optional—you can always express the same logic without them. In this book, we never use break or continue.

### 3.9 Big Numbers

If the precision of the basic integer and floating-point types is not sufficient, you can turn to a couple of handy classes in the java.math package: BigInteger and BigDecimal. These are classes for manipulating numbers with an arbitrarily long sequence of digits. The BigInteger class implements arbitrary-precision integer arithmetic, and BigDecimal does the same for floating-point numbers.

Use the static valueOf method to turn an ordinary number into a big number:

Click here to view code image

BigInteger a = BigInteger.valueOf(100);

For longer numbers, use a constructor with a string parameter:

Click here to view code image

BigInteger reallyBig

= new BigInteger("222232244629420445529739893461909967206666939096499764990979600");

There are also constants BigInteger.ZERO, BigInteger.ONE, BigInteger.TEN, and, since Java 9, BigInteger.TWO.

Unfortunately, you cannot use the familiar mathematical operators such as + and * to combine big numbers. Instead, you must use methods such as add and multiply in the big number classes.

Click here to view code image

BigInteger c = a.add(b); // c = a + b

BigInteger d = c.multiply(b.add(BigInteger.valueOf(2))); // d = c * (b + 2)

C++ Note

Unlike C++, Java has no programmable operator overloading. There was no way for the programmers of the BigInteger class to redefine the + and * operators to give the add and multiply operations of the BigInteger classes. The language designers did overload the + operator to denote concatenation of strings. They chose not to overload other operators, and they did not give Java programmers the opportunity to overload operators in their own classes.

Listing 3.6 shows a modification of the lottery odds program of Listing 3.5, updated to work with big numbers. For example, if you are invited to participate in a lottery in which you need to pick 60 numbers out of a possible 490 numbers, you can use this program to tell you your odds of winning. They are 1 in 716395843461995557415116222540092933411717612789263493493351013459481104668848. Good luck!

The program in Listing 3.5 computed the statement

Click here to view code image

lotteryOdds = lotteryOdds * (n - i + 1) / i;

When big numbers are used, the equivalent statement becomes

Click here to view code image

lotteryOdds

= lotteryOdds.multiply(BigInteger.valueOf(n - i + 1)).divide(BigInteger.valueOf(i));

Listing 3.6 BigIntegerTest/BigIntegerTest.java

Click here to view code image

1 import java.math.*;

2 import java.util.*;

3

4 /**

5 * This program uses big numbers to compute the odds of winning the grand prize in a lottery.

6 * @version 1.20 2004-02-10

7 * @author Cay Horstmann

8 */

9 public class BigIntegerTest

10 {

11 public static void main(String[] args)

12 {

13 Scanner in = new Scanner(System.in);

14

15 System.out.print("How many numbers do you need to draw? ");

16 int k = in.nextInt();

17

18 System.out.print("What is the highest number you can draw? ");

19 int n = in.nextInt();

20

21 /*

22 * compute binomial coefficient n*(n-1)*(n-2)*...*(n-k+1)/(1*2*3*...*k)

23 */

24

25 BigInteger lotteryOdds = BigInteger.valueOf(1);

26

27 for (int i = 1; i <= k; i++)

28 lotteryOdds = lotteryOdds.multiply(BigInteger.valueOf(n - i + 1)).divide(

29 BigInteger.valueOf(i));

30

31 System.out.println("Your odds are 1 in " + lotteryOdds + ". Good luck!");

32 }

33 }

java.math.BigInteger 1.1

BigInteger add(BigInteger other)

BigInteger subtract(BigInteger other)

BigInteger multiply(BigInteger other)

BigInteger divide(BigInteger other)

BigInteger mod(BigInteger other)

returns the sum, difference, product, quotient, and remainder of this big integer and other.

BigInteger sqrt() 9

yields the square root of this BigInteger.

int compareTo(BigInteger other)

returns 0 if this big integer equals other, a negative result if this big integer is less than other, and a positive result otherwise.

static BigInteger valueOf(long x)

returns a big integer whose value equals x.

java.math.BigDecimal 1.1

BigDecimal add(BigDecimal other)

BigDecimal subtract(BigDecimal other)

BigDecimal multiply(BigDecimal other)

BigDecimal divide(BigDecimal other)

BigDecimal divide(BigDecimal other, RoundingMode mode) 5

returns the sum, difference, product, or quotient of this big decimal and other. The first divide method throws an exception if the quotient does not have a finite decimal expansion. To obtain a rounded result, use the second method. The mode RoundingMode.HALF_UP is the rounding mode that you learned in school: round down the digits 0 to 4, round up the digits 5 to 9. It is appropriate for routine calculations. See the API documentation for other rounding modes.

int compareTo(BigDecimal other)

returns 0 if this big decimal equals other, a negative result if this big decimal is less than other, and a positive result otherwise.

static BigDecimal valueOf(long x)

static BigDecimal valueOf(long x, int scale)

returns a big decimal whose value equals x or x / 10scale.

3.9 大数值

如果基本的整数和浮点数精度不能够满足需求，那么可以使用 java.math 包中的两个很有用的类：BigInteger 和 BigDecimal。这两个类可以处理包含任意长度数字序列的数值。BigInteger 类实现了任意精度的整数运算，BigDecimal 实现了任意精度的浮点数运算。

使用静态的 valueOf 方法可以将普通的数值转换为大数值： 遗憾的是，不能使用人们熟悉的算术运算符（如：+ 和 *）处理大数值。而需要使用大数值类中的 add 和 multiply 方法。

C++ 注释：与 C++ 不同，Java 没有提供运算符重载功能。程序员无法重定义 + 和 * 运算符，使其应用于 BigInteger 类的 add 和 multiply 运算。Java 语言的设计者确实为字符串的连接重载了 + 运算符，但没有重载其他的运算符，也没有给 Java 程序员在自己的类中重载运算符的机会。

程序清单 3-6 是对程序清单 3-5 中彩概率程序的改进，使其可以采用大数值进行运算。假设你被邀请参加抽奖活动，并从 490 个可能的数值中抽取 60 个，这个程序将会得到中彩概率 1/716395843461995557415116222540092933411717612789263493493351013459481104668848。祝你好运！

程序清单 3-6 BigIntegerTest/BigIntegerTest.java

在程序清单 3-5 中，用于计算的语句是 如果使用大数值，则相应的语句为：

API java.math.BigInteger 1.1

·BigInteger add（BigInteger other）

·BigInteger subtract（BigInteger other）

·BigInteger multiply（BigInteger other）

·BigInteger divide（BigInteger other）

·BigInteger mod（BigInteger other）

返回这个大整数和另一个大整数 other 的和、差、积、商以及余数。

·int compareTo（BigInteger other）如果这个大整数与另一个大整数 other 相等，返回 0；如果这个大整数小于另一个大整数 other，返回负数；否则，返回正数。

·static BigInteger valueOf（long x）返回值等于 x 的大整数。

返回值等于 x 的大整数。

java.math.BigInteger 1.1

·BigDecimal add（BigDecimal other）

·BigDecimal subtract（BigDecimal other）

·BigDecimal multiply（BigDecimal other）

·BigDecimal divide（BigDecimal other，RoundingMode mode）5.0

返回这个大实数与另一个大实数 other 的和、差、积、商。要想计算商，必须给出舍入方式（rounding mode）。RoundingMode.HALF_UP 是在学校中学习的四舍五入方式（即，数值 0 到 4 舍去，数值 5 到 9 进位）。它适用于常规的计算。有关其他的舍入方式请参看 API 文档。

·int compareTo（BigDecimal other）如果这个大实数与另一个大实数相等，返回 0；如果这个大实数小于另一个大实数，返回负数；否则，返回正数。

·static BigDecimal valueOf（long x）

·static BigDecimal valueOf（long x，int scale）

返回值为 x 或 x/10scale 的一个大实数。

### 3.10 Arrays

Arrays hold sequences of values of the same type. In the following sections, you will see how to work with arrays in Java.

#### 3.10.1 Declaring Arrays

An array is a data structure that stores a collection of values of the same type. You access each individual value through an integer index. For example, if a is an array of integers, then a[i] is the ith integer in the array.

Declare an array variable by specifying the array type—which is the element type followed by []—and the array variable name. For example, here is the declaration of an array a of integers:

int[] a;

However, this statement only declares the variable a. It does not yet initialize a with an actual array. Use the new operator to create the array.

Click here to view code image

int[] a = new int[100]; // or var a = new int[100];

This statement declares and initializes an array of 100 integers.

The array length need not be a constant: new int[n] creates an array of length n.

Once you create an array, you cannot change its length (although you can, of course, change an individual array element). If you frequently need to expand the length of arrays while your program is running, you should use array lists, which are covered in Chapter 5.

Note

You can define an array variable either as

int[] a;

or as

int a[];

Most Java programmers prefer the former style because it neatly separates the type int[] (integer array) from the variable name.

Java has a shortcut for creating an array object and supplying initial values:

Click here to view code image

int[] smallPrimes = { 2, 3, 5, 7, 11, 13 };

Notice that you do not use new with this syntax, and you don't specify the length.

A comma after the last value is allowed, which can be convenient for an array to which you keep adding values over time:

Click here to view code image

String[] authors = {

"James Gosling",

"Bill Joy",

"Guy Steele",

// add more names here and put a comma after each name

};

You can declare an anonymous array:

Click here to view code image

new int[] { 17, 19, 23, 29, 31, 37 }

This expression allocates a new array and fills it with the values inside the braces. It counts the number of initial values and sets the array size accordingly. You can use this syntax to reinitialize an array without creating a new variable. For example,

Click here to view code image

smallPrimes = new int[] { 17, 19, 23, 29, 31, 37 };

is shorthand for

Click here to view code image

int[] anonymous = { 17, 19, 23, 29, 31, 37 };

smallPrimes = anonymous;

Note

It is legal to have arrays of length 0. Such an array can be useful if you write a method that computes an array result and the result happens to be empty. Construct an array of length 0 as

new elementType[0]

or

new elementType[] {}

Note that an array of length 0 is not the same as null.


3.10 数组

数组是一种数据结构，用来存储同一类型值的集合。通过一个整型下标可以访问数组中的每一个值。例如，如果 a 是一个整型数组，a [i] 就是数组中下标为 i 的整数。

在声明数组变量时，需要指出数组类型（数据元素类型紧跟 []）和数组变量的名字。下面声明了整型数组 a：

不过，这条语句只声明了变量 a，并没有将 a 初始化为一个真正的数组。应该使用 new 运算符创建数组。

这条语句创建了一个可以存储 100 个整数的数组。数组长度不要求是常量：new int [n] 会创建一个长度为 n 的数组。

注释：可以使用下面两种形式声明数组

或

大多数 Java 应用程序员喜欢使用第一种风格，因为它将类型 int []（整型数组）与变量名分开了。这个数组的下标从 0~99（不是 1~100）。一旦创建了数组，就可以给数组元素赋值。例如，使用一个循环：

创建一个数字数组时，所有元素都初始化为 0。boolean 数组的元素会初始化为 false。对象数组的元素则初始化为一个特殊值 null，这表示这些元素（还）未存放任何对象。初学者对此可能有些不解。例如，

会创建一个包含 10 个字符串的数组，所有字符串都为 null。如果希望这个数组包含空串，可以为元素指定空串：

警告：如果创建了一个 100 个元素的数组，并且试图访问元素 a [100]（或任何在 0~99 之外的下标），程序就会引发「array index out of bounds」异常而终止执行。

要想获得数组中的元素个数，可以使用 array.length。例如，

一旦创建了数组，就不能再改变它的大小（尽管可以改变每一个数组元素）。如果经常需要在运行过程中扩展数组的大小，就应该使用另一种数据结构 —— 数组列表（array list）有关数组列表的详细内容请参看第 5 章。

#### 3.10.2 Accessing Array Elements

The array elements are numbered from 0 to 99 (and not 1 to 100). Once the array is created, you can fill the elements in an array, for example, by using a loop:

Click here to view code image

int[] a = new int[100];

for (int i = 0; i < 100; i++)

a[i] = i; // fills the array with numbers 0 to 99

When you create an array of numbers, all elements are initialized with zero. Arrays of boolean are initialized with false. Arrays of objects are initialized with the special value null, which indicates that they do not (yet) hold any objects. This can be surprising for beginners. For example,

Click here to view code image

String[] names = new String[10];

creates an array of ten strings, all of which are null. If you want the array to hold empty strings, you must supply them:

Click here to view code image

for (int i = 0; i < 10; i++) names[i] = "";

Caution

If you construct an array with 100 elements and then try to access the element a[100] (or any other index outside the range from 0 to 99), an「array index out of bounds」exception will occur.

To find the number of elements of an array, use array.length. For example:

Click here to view code image

for (int i = 0; i < a.length; i++)

System.out.println(a[i]);

#### 3.10.3 The「for each」Loop

Java has a powerful looping construct that allows you to loop through each element in an array (or any other collection of elements) without having to fuss with index values.

The enhanced for loop

Click here to view code image

for (variable : collection) statement

sets the given variable to each element of the collection and then executes the statement (which, of course, may be a block). The collection expression must be an array or an object of a class that implements the Iterable interface, such as ArrayList. We discuss array lists in Chapter 5 and the Iterable interface in Chapter 9.

For example,

Click here to view code image

for (int element : a)

System.out.println(element);

prints each element of the array a on a separate line.

You should read this loop as「for each element in a」. The designers of the Java language considered using keywords, such as foreach and in. But this loop was a late addition to the Java language, and in the end nobody wanted to break the old code that already contained methods or variables with these names (such as System.in).

Of course, you could achieve the same effect with a traditional for loop:

Click here to view code image

for (int i = 0; i < a.length; i++)

System.out.println(a[i]);

However, the「for each」loop is more concise and less error-prone, as you don't have to worry about those pesky start and end index values.

Note

The loop variable of the「for each」loop traverses the elements of the array, not the index values.

The「for each」loop is a pleasant improvement over the traditional loop if you need to process all elements in a collection. However, there are still plenty of opportunities to use the traditional for loop. For example, you might not want to traverse the entire collection, or you may need the index value inside the loop.

Tip

There is an even easier way to print all values of an array, using the toString method of the Arrays class. The call Arrays.toString(a) returns a string containing the array elements, enclosed in brackets and separated by commas, such as "[2, 3, 5, 7, 11, 13]". To print the array, simply call

Click here to view code image

System.out.println(Arrays.toString(a));

3.10.1 for each 循环

Java 有一种功能很强的循环结构，可以用来依次处理数组中的每个元素（其他类型的元素集合亦可）而不必为指定下标值而分心。

这种增强的 for 循环的语句格式为：

定义一个变量用于暂存集合中的每一个元素，并执行相应的语句（当然，也可以是语句块）。collection 这一集合表达式必须是一个数组或者是一个实现了 Iterable 接口的类对象（例如 ArrayList）。有关数组列表的内容将在第 5 章中讨论，有关 Iterable 接口的内容将在第 9 章中讨论。例如，

打印数组 a 的每一个元素，一个元素占一行。

这个循环应该读作「循环 a 中的每一个元素」（for each element in a）。Java 语言的设计者认为应该使用诸如 foreach、in 这样的关键字，但这种循环语句并不是最初就包含在 Java 语言中的，而是后来添加进去的，并且没有人打算废除已经包含同名（例如 System.in）方法或变量的旧代码。当然，使用传统的 for 循环也可以获得同样的效果：

但是，for each 循环语句显得更加简洁、更不易出错（不必为下标的起始值和终止值而操心）。

注释：for each 循环语句的循环变量将会遍历数组中的每个元素，而不需要使用下标值。如果需要处理一个集合中的所有元素，for each 循环语句对传统循环语句所进行的改进更是叫人称赞不已。然而，在很多场合下，还是需要使用传统的 for 循环。例如，如果不希望遍历集合中的每个元素，或者在循环内部需要使用下标值等。

提示：有个更加简单的方式打印数组中的所有值，即利用 Arrays 类的 toString 方法。调用 Arrays.toString（a），返回一个包含数组元素的字符串，这些元素被放置在括号内，并用逗号分隔，例如，「[2，3，5，7，11，13]」。要想打印数组，可以调用

3.10.2 数组初始化以及匿名数组

在 Java 中，提供了一种创建数组对象并同时赋予初始值的简化书写形式。下面是一个例子：

请注意，在使用这种语句时，不需要调用 new。甚至还可以初始化一个匿名的数组：

这种表示法将创建一个新数组并利用括号中提供的值进行初始化，数组的大小就是初始值的个数。使用这种语法形式可以在不创建新变量的情况下重新初始化一个数组。例如： 这是下列语句的简写形式：

注释：在 Java 中，允许数组长度为 0。在编写一个结果为数组的方法时，如果碰巧结果为空，则这种语法形式就显得非常有用。此时可以创建一个长度为 0 的数组：

注意，数组长度为 0 与 null 不同。

#### 3.10.4 Array Copying

You can copy one array variable into another, but then both variables refer to the same array:

Click here to view code image

int[] luckyNumbers = smallPrimes;

luckyNumbers[5] = 12; // now smallPrimes[5] is also 12

Figure 3.14 shows the result. If you actually want to copy all values of one array into a new array, use the copyOf method in the Arrays class:

Figure 3.14 Copying an array variable

Click here to view code image

int[] copiedLuckyNumbers = Arrays.copyOf(luckyNumbers, luckyNumbers.length);

The second parameter is the length of the new array. A common use of this method is to increase the size of an array:

Click here to view code image

luckyNumbers = Arrays.copyOf(luckyNumbers, 2 * luckyNumbers.length);

The additional elements are filled with 0 if the array contains numbers, false if the array contains boolean values. Conversely, if the length is less than the length of the original array, only the initial values are copied.

C++ Note

A Java array is quite different from a C++ array on the stack. It is, however, essentially the same as a pointer to an array allocated on the heap. That is,

Click here to view code image

int[] a = new int[100]; // Java

is not the same as

int a[100]; // C++

but rather

int* a = new int[100]; // C++

In Java, the [] operator is predefined to perform bounds checking. Furthermore, there is no pointer arithmetic—you can't increment a to point to the next element in the array.

3.10.3 数组拷贝

在 Java 中，允许将一个数组变量拷贝给另一个数组变量。这时，两个变量将引用同一个数组：

图 3-14 显示了拷贝的结果。如果希望将一个数组的所有值拷贝到一个新的数组中去，就要使用 Arrays 类的 copyOf 方法： 图 3-14 拷贝一个数组变量

第 2 个参数是新数组的长度。这个方法通常用来增加数组的大小：

如果数组元素是数值型，那么多余的元素将被赋值为 0；如果数组元素是布尔型，则将赋值为 false。相反，如果长度小于原始数组的长度，则只拷贝最前面的数据元素。

C++ 注释：Java 数组与 C++ 数组在堆栈上有很大不同，但基本上与分配在堆（heap）上的数组指针一样。也就是说，

不同于 而等同于

Java 中的 [] 运算符被预定义为检查数组边界，而且没有指针运算，即不能通过 a 加 1 得到数组的下一个元素。

#### 3.10.5 Command-Line Parameters

You have already seen one example of a Java array repeated quite a few times. Every Java program has a main method with a String[] args parameter. This parameter indicates that the main method receives an array of strings—namely, the arguments specified on the command line.

For example, consider this program:

Click here to view code image

public class Message

{

public static void main(String[] args)

{

if (args.length == 0 || args[0].equals("-h"))

System.out.print("Hello,");

else if (args[0].equals("-g"))

System.out.print("Goodbye,");

// print the other command-line arguments

for (int i = 1; i < args.length; i++)

System.out.print(" " + args[i]);

System.out.println("!");

}

}

If the program is called as

Click here to view code image

java Message -g cruel world

then the args array has the following contents:

Click here to view code image

args[0]: "-g"

args[1]: "cruel"

args[2]: "world"

The program prints the message

Click here to view code image

Goodbye, cruel world!

C++ Note

In the main method of a Java program, the name of the program is not stored in the args array. For example, when you start up a program as

Click here to view code image

java Message -h world

from the command line, then args[0] will be "-h" and not "Message" or "java".

3.10.6 Array Sorting

To sort an array of numbers, you can use one of the sort methods in the Arrays class:

Click here to view code image

int[] a = new int[10000];

. . .

Arrays.sort(a)

This method uses a tuned version of the QuickSort algorithm that is claimed to be very efficient on most data sets. The Arrays class provides several other convenience methods for arrays that are included in the API notes at the end of this section.

The program in Listing 3.7 puts arrays to work. This program draws a random combination of numbers for a lottery game. For example, if you play a「choose 6 numbers from 49」lottery, the program might print this:

Click here to view code image

Bet the following combination. It'll make you rich!

4

7

8

19

30

44

To select such a random set of numbers, we first fill an array numbers with the values 1, 2, . . ., n:

Click here to view code image

int[] numbers = new int[n];

for (int i = 0; i < numbers.length; i++)

numbers[i] = i + 1;

A second array holds the numbers to be drawn:

Click here to view code image

int[] result = new int[k];

Now we draw k numbers. The Math.random method returns a random floating-point number that is between 0 (inclusive) and 1 (exclusive). By multiplying the result with n, we obtain a random number between 0 and n – 1.

Click here to view code image

int r = (int) (Math.random() * n);

We set the ith result to be the number at that index. Initially, that is just r + 1, but as you'll see presently, the contents of the numbers array are changed after each draw.

Click here to view code image

result[i] = numbers[r];

Now we must be sure never to draw that number again—all lottery numbers must be distinct. Therefore, we overwrite numbers[r] with the last number in the array and reduce n by 1.

Click here to view code image

numbers[r] = numbers[n - 1];

n--;

The point is that in each draw we pick an index, not the actual value. The index points into an array that contains the values that have not yet been drawn.

After drawing k lottery numbers, we sort the result array for a more pleasing output:

Click here to view code image

Arrays.sort(result);

for (int r : result)

System.out.println(r);

Listing 3.7 LotteryDrawing/LotteryDrawing.java

Click here to view code image

1 import java.util.*;

2

3 /**

4 * This program demonstrates array manipulation.

5 * @version 1.20 2004-02-10

6 * @author Cay Horstmann

7 */

8 public class LotteryDrawing

9 {

10 public static void main(String[] args)

11 {

12 Scanner in = new Scanner(System.in);

13

14 System.out.print("How many numbers do you need to draw? ");

15 int k = in.nextInt();

16

17 System.out.print("What is the highest number you can draw? ");

18 int n = in.nextInt();

19

20 // fill an array with numbers 1 2 3 . . . n

21 int[] numbers = new int[n];

22 for (int i = 0; i < numbers.length; i++)

23 numbers[i] = i + 1;

24

25 // draw k numbers and put them into a second array

26 int[] result = new int[k];

27 for (int i = 0; i < result.length; i++)

28 {

29 // make a random index between 0 and n - 1

30 int r = (int) (Math.random() * n);

31

32 // pick the element at the random location

33 result[i] = numbers[r];

34

35 // move the last element into the random location

36 numbers[r] = numbers[n - 1];

37 n--;

38 }

39

40 // print the sorted array

41 Arrays.sort(result);

42 System.out.println("Bet the following combination. It'll make you rich!");

43 for (int r : result)

44 System.out.println(r);

45 }

46 }

java.util.Arrays 1.2

static String toString(xxx[] a) 5

returns a string with the elements of a, enclosed in brackets and delimited by commas. In this and the following methods, the component type xxx of the array can be int, long, short, char, byte, boolean, float, or double.

static xxx[] copyOf(xxx[] a, int end) 6

static xxx[] copyOfRange(xxx[] a, int start, int end) 6

returns an array of the same type as a, of length either end or end – start, filled with the values of a. If end is larger than a.length, the result is padded with 0 or false values.

static void sort(xxx[] a)

sorts the array, using a tuned QuickSort algorithm.

static int binarySearch(xxx[] a, xxx v)

static int binarySearch(xxx[] a, int start, int end, xxx v) 6

uses the binary search algorithm to search for the value v in the sorted array a. If v is found, its index is returned. Otherwise, a negative value r is returned; –r – 1 is the spot at which v should be inserted to keep a sorted.

static void fill(xxx[] a, xxx v)

sets all elements of the array to v.

static boolean equals(xxx[] a, xxx[] b)

returns true if the arrays have the same length and if the elements at corresponding indexes match.

3.10.4 命令行参数

前面已经看到多个使用 Java 数组的示例。每一个 Java 应用程序都有一个带 String arg [] 参数的 main 方法。这个参数表明 main 方法将接收一个字符串数组，也就是命令行参数。例如，看一看下面这个程序：

如果使用下面这种形式运行这个程序：

args 数组将包含下列内容：

这个程序将显示下列信息：

C++ 注释：在 Java 应用程序的 main 方法中，程序名并没有存储在 args 数组中。例如，当使用下列命令运行程序时

args [0] 是「-h」，而不是「Message」或「java」。

#### 3.10.7 Multidimensional Arrays

Multidimensional arrays use more than one index to access array elements. They are used for tables and other more complex arrangements. You can safely skip this section until you have a need for this storage mechanism.

Suppose you want to make a table of numbers that shows how much an investment of $10,000 will grow under different interest rate scenarios in which interest is paid annually and reinvested (Table 3.8).

Table 3.8 Growth of an Investment at Different Interest Rates

10%

11%

12%

13%

14%

15%

10,000.00

10,000.00

10,000.00

10,000.00

10,000.00

10,000.00

11,000.00

11,100.00

11,200.00

11,300.00

11,400.00

11,500.00

12,100.00

12,321.00

12,544.00

12,769.00

12,996.00

13,225.00

13,310.00

13,676.31

14,049.28

14,428.97

14,815.44

15,208.75

14,641.00

15,180.70

15,735.19

16,304.74

16,889.60

17,490.06

16,105.10

16,850.58

17,623.42

18,424.35

19,254.15

20,113.57

17,715.61

18,704.15

19,738.23

20,819.52

21,949.73

23,130.61

19,487.17

20,761.60

22,106.81

23,526.05

25,022.69

26,600.20

21,435.89

23,045.38

24,759.63

26,584.44

28,525.86

30,590.23

23,579.48

25,580.37

27,730.79

30,040.42

32,519.49

35,178.76

You can store this information in a two-dimensional array (matrix), which we call balances.

Declaring a two-dimensional array in Java is simple enough. For example:

double[][] balances;

You cannot use the array until you initialize it. In this case, you can do the initialization as follows:

Click here to view code image

balances = new double[NYEARS][NRATES];

In other cases, if you know the array elements, you can use a shorthand notation for initializing a multidimensional array without a call to new. For example:

Click here to view code image

int[][] magicSquare =

{

{16, 3, 2, 13},

{5, 10, 11, 8},

{9, 6, 7, 12},

{4, 15, 14, 1}

};

Once the array is initialized, you can access individual elements by supplying two pairs of brackets—for example, balances[i][j].

The example program stores a one-dimensional array interest of interest rates and a two-dimensional array balances of account balances, one for each year and interest rate. We initialize the first row of the array with the initial balance:

Click here to view code image

for (int j = 0; j < balances[0].length; j++)

balances[0][j] = 10000;

Then we compute the other rows, as follows:

Click here to view code image

for (int i = 1; i < balances.length; i++)

{

for (int j = 0; j < balances[i].length; j++)

{

double oldBalance = balances[i - 1][j];

double interest = . . .;

balances[i][j] = oldBalance + interest;

}

}

Listing 3.8 shows the full program.

Note

A「for each」loop does not automatically loop through all elements in a two-dimensional array. Instead, it loops through the rows, which are themselves one-dimensional arrays. To visit all elements of a two-dimensional array a, nest two loops, like this:

Click here to view code image

for (double[] row : a)

for (double value : row)

do something with value

Tip

To print out a quick-and-dirty list of the elements of a two-dimensional array, call

Click here to view code image

System.out.println(Arrays.deepToString(a));

The output is formatted like this:

Click here to view code image

[[16, 3, 2, 13], [5, 10, 11, 8], [9, 6, 7, 12], [4, 15, 14, 1]]

Listing 3.8 CompoundInterest/CompoundInterest.java

Click here to view code image

1 /**

2 * This program shows how to store tabular data in a 2D array.

3 * @version 1.40 2004-02-10

4 * @author Cay Horstmann

5 */

6 public class CompoundInterest

7 {

8 public static void main(String[] args)

9 {

10 final double STARTRATE = 10;

11 final int NRATES = 6;

12 final int NYEARS = 10;

13

14 // set interest rates to 10 . . . 15%

15 double[] interestRate = new double[NRATES];

16 for (int j = 0; j < interestRate.length; j++)

17 interestRate[j] = (STARTRATE + j) / 100.0;

18

19 double[][] balances = new double[NYEARS][NRATES];

20

21 // set initial balances to 10000

22 for (int j = 0; j < balances[0].length; j++)

23 balances[0][j] = 10000;

24

25 // compute interest for future years

26 for (int i = 1; i < balances.length; i++)

27 {

28 for (int j = 0; j < balances[i].length; j++)

29 {

30 // get last year's balances from previous row

31 double oldBalance = balances[i - 1][j];

32

33 // compute interest

34 double interest = oldBalance * interestRate[j];

35

36 // compute this year's balances

37 balances[i][j] = oldBalance + interest;

38 }

39 }

40

41 // print one row of interest rates

42 for (int j = 0; j < interestRate.length; j++)

43 System.out.printf("%9.0f%%", 100 * interestRate[j]);

44

45 System.out.println();

46

47 // print balance table

48 for (double[] row : balances)

49 {

50 // print table row

51 for (double b : row)

52 System.out.printf("%10.2f", b);

53

54 System.out.println();

55 }

56 }

57 }

3.10.6 多维数组

多维数组将使用多个下标访问数组元素，它适用于表示表格或更加复杂的排列形式。这一节的内容可以先跳过，等到需要使用这种存储机制时再返回来学习。

假设需要建立一个数值表，用来显示在不同利率下投资 $10，000 会增长多少，利息每年兑现，而且又被用于投资（见表 3-8）。表 3-8 不同利率下的投资增长情况

可以使用一个二维数组（也称为矩阵）存储这些信息。这个数组被命名为 balances。在 Java 中，声明一个二维数组相当简单。例如：

与一维数组一样，在调用 new 对多维数组进行初始化之前不能使用它。在这里可以这样初始化：

另外，如果知道数组元素，就可以不调用 new，而直接使用简化的书写形式对多维数组进行初始化。例如：

一旦数组被初始化，就可以利用两个方括号访问每个元素，例如，balances [i][j]。在示例程序中用到了一个存储利率的一维数组 interest 与一个存储余额的二维数组 balances。一维用于表示年，另一维用于表示利率，最初使用初始余额来初始化这个数组的第一行：

然后，按照下列方式计算其他行：

程序清单 3-8 给出了完整的程序。注释：for each 循环语句不能自动处理二维数组的每一个元素。它是按照行，也就是一维数组处理的。要想访问二维数组 a 的所有元素，需要使用两个嵌套的循环，如下所示：

提示：要想快速地打印一个二维数组的数据元素列表，可以调用： 输出格式为：

程序清单 3-8 CompoundInterest/CompoundInterest.java

3.10.7 不规则数组

到目前为止，读者所看到的数组与其他程序设计语言中提供的数组没有多大区别。但实际存在着一些细微的差异，而这正是 Java 的优势所在：Java 实际上没有多维数组，只有一维数组。多维数组被解释为「数组的数组。」

例如，在前面的示例中，balances 数组实际上是一个包含 10 个元素的数组，而每个元素又是一个由 6 个浮点数组成的数组（请参看图 3-15）。

图 3-15 一个二维数组

表达式 balances [i] 引用第 i 个子数组，也就是二维表的第 i 行。它本身也是一个数组，balances [i][j] 引用这个数组的第 j 项。由于可以单独地存取数组的某一行，所以可以让两行交换。

还可以方便地构造一个「不规则」数组，即数组的每一行有不同的长度。下面是一个典型的示例。在这个示例中，创建一个数组，第 i 行第 j 列将存放「从 i 个数值中抽取 j 个数值」产生的结果。

由于 j 不可能大于 i，所以矩阵是三角形的。第 i 行有 i+1 个元素（允许抽取 0 个元素，也是一种选择）。要想创建一个不规则的数组，首先需要分配一个具有所含行数的数组。

接下来，分配这些行。

在分配了数组之后，假定没有超出边界，就可以采用通常的方式访问其中的元素了。

程序清单 3-9 给出了完整的程序。C++ 注释：在 C++ 中，Java 声明 不同于

也不同于

也不同于

而是分配了一个包含 10 个指针的数组： 然后，指针数组的每一个元素被填充了一个包含 6 个数字的数组：

庆幸的是，当创建 new double [10][6] 时，这个循环将自动地执行。当需要不规则的数组时，只能单独地创建行数组。

程序清单 3-9 LotteryArray/LotteryArray.java

现在，已经看到了 Java 语言的基本程序结构，下一章将介绍 Java 中的面向对象的程序设计。

#### 3.10.8 Ragged Arrays

So far, what you have seen is not too different from other programming languages. But there is actually something subtle going on behind the scenes that you can sometimes turn to your advantage: Java has no multidimensional arrays at all, only one-dimensional arrays. Multidimensional arrays are faked as「arrays of arrays.」

For example, the balances array in the preceding example is actually an array that contains ten elements, each of which is an array of six floating-point numbers (Figure 3.15).

Figure 3.15 A two-dimensional array

The expression balances[i] refers to the ith subarray—that is, the ith row of the table. It is itself an array, and balances[i][j] refers to the jth element of that array.

Since rows of arrays are individually accessible, you can actually swap them!

Click here to view code image

double[] temp = balances[i];

balances[i] = balances[i + 1];

balances[i + 1] = temp;

It is also easy to make「ragged」arrays—that is, arrays in which different rows have different lengths. Here is the standard example. Let us make an array in which the element at row i and column j equals the number of possible outcomes of a「choose j numbers from i numbers」lottery.

Click here to view code image

1

1 1

1 2 1

1 3 3 1

1 4 6 4 1

1 5 10 10 5 1

1 6 15 20 15 6 1

As j can never be larger than i, the matrix is triangular. The ith row has i + 1 elements. (We allow choosing 0 elements; there is one way to make such a choice.) To build this ragged array, first allocate the array holding the rows:

Click here to view code image

int[][] odds = new int[NMAX + 1][];

Next, allocate the rows:

Click here to view code image

for (int n = 0; n <= NMAX; n++)

odds[n] = new int[n + 1];

Now that the array is allocated, we can access the elements in the normal way, provided we do not overstep the bounds:

Click here to view code image

for (int n = 0; n < odds.length; n++)

for (int k = 0; k < odds[n].length; k++)

{

// compute lotteryOdds

. . .

odds[n][k] = lotteryOdds;

}

Listing 3.9 gives the complete program.

C++ Note

In C++, the Java declaration

Click here to view code image

double[][] balances = new double[10][6]; // Java

is not the same as

Click here to view code image

double balances[10][6]; // C++

or even

Click here to view code image

double (*balances)[6] = new double[10][6]; // C++

Instead, an array of ten pointers is allocated:

Click here to view code image

double** balances = new double*[10]; // C++

Then, each element in the pointer array is filled with an array of six numbers:

Click here to view code image

for (i = 0; i < 10; i++)

balances[i] = new double[6];

Mercifully, this loop is automatic when you ask for a new double[10][6]. When you want ragged arrays, you allocate the row arrays separately.

Listing 3.9 LotteryArray/LotteryArray.java

Click here to view code image

1 /**

2 * This program demonstrates a triangular array.

3 * @version 1.20 2004-02-10

4 * @author Cay Horstmann

5 */

6 public class LotteryArray

7 {

8 public static void main(String[] args)

9 {

10 final int NMAX = 10;

11

12 // allocate triangular array

13 int[][] odds = new int[NMAX + 1][];

14 for (int n = 0; n <= NMAX; n++)

15 odds[n] = new int[n + 1];

16

17 // fill triangular array

18 for (int n = 0; n < odds.length; n++)

19 for (int k = 0; k < odds[n].length; k++)

20 {

21 /*

22 * compute binomial coefficient n*(n-1)*(n-2)*...*(n-k+1)/(1*2*3*...*k)

23 */

24 int lotteryOdds = 1;

25 for (int i = 1; i <= k; i++)

26 lotteryOdds = lotteryOdds * (n - i + 1) / i;

27

28 odds[n][k] = lotteryOdds;

29 }

30

31 // print triangular array

32 for (int[] row : odds)

33 {

34 for (int odd : row)

35 System.out.printf("%4d", odd);

36 System.out.println();

37 }

38 }

39 }

You have now seen the fundamental programming structures of the Java language. The next chapter covers object-oriented programming in Java.

3.10.5 数组排序

要想对数值型数组进行排序，可以使用 Arrays 类中的 sort 方法：

这个方法使用了优化的快速排序算法。快速排序算法对于大多数数据集合来说都是效率比较高的。Arrays 类还提供了几个使用很便捷的方法，在稍后的 API 注释中将介绍它们。

程序清单 3-7 中的程序用到了数组，它产生一个抽彩游戏中的随机数值组合。假如抽彩是从 49 个数值中抽取 6 个，那么程序可能的输出结果为：

要想选择这样一个随机的数值集合，就要首先将数值 1，2，…，n 存入数组 numbers 中：

而用第二个数组存放抽取出来的数值：

现在，就可以开始抽取 k 个数值了。Math.random 方法将返回一个 0 到 1 之间（包含 0、不包含 1）的随机浮点数。用 n 乘以这个浮点数，就可以得到从 0 到 n-1 之间的一个随机数。

下面将 result 的第 i 个元素设置为 numbers [r] 存放的数值，最初是 r+1。但正如所看到的，numbers 数组的内容在每一次抽取之后都会发生变化。现在，必须确保不会再次抽取到那个数值，因为所有抽彩的数值必须不相同。因此，这里用数组中的最后一个数值改写 number [r]，并将 n 减 1。

关键在于每次抽取的都是下标，而不是实际的值。下标指向包含尚未抽取过的数组元素。在抽取了 k 个数值之后，就可以对 result 数组进行排序了，这样可以让输出效果更加清晰：

程序清单 3-7 LotteryDrawing/LotteryDrawing.java

ava.util.Arrays 1.2

·static String toString（type [] a）5.0 返回包含 a 中数据元素的字符串，这些数据元素被放在括号内，并用逗号分隔。参数：a　类型为 int、long、short、char、byte、boolean、float 或 double 的数组。

·static type copyOf（type[]a，int length）6

·static type copyOfRange（type [] a，int start，int end）6 返回与 a 类型相同的一个数组，其长度为 length 或者 end-start，数组元素为 a 的值。参数：a　类型为 int、long、short、char、byte、boolean、float 或 double 的数组。start　起始下标（包含这个值）。end　终止下标（不包含这个值）。这个值可能大于 a.length。在这种情况下，结果为 0 或 false。length　拷贝的数据元素长度。如果 length 值大于 a.length，结果为 0 或 false；否则，数组中只有前面 length 个数据元素的拷贝值。

·static void sort（type [] a）采用优化的快速排序算法对数组进行排序。

参数：a　类型为 int、long、short、char、byte、boolean、float 或 double 的数组。·static int binarySearch（type [] a，type v）·static int binarySearch（type [] a，int start，int end，type v）6 采用二分搜索算法查找值 v。如果查找成功，则返回相应的下标值；否则，返回一个负数值 r。-r-1 是为保持 a 有序 v 应插入的位置。参数：a　类型为 int、long、short、char、byte、boolean、float 或 double 的有序数组。start　起始下标（包含这个值）。end　终止下标（不包含这个值）。v　同 a 的数据元素类型相同的值。·static void fill（type [] a，type v）将数组的所有数据元素值设置为 v。

参数：a　类型为 int、long、short、char、byte、boolean、float 或 double 的数组。v　与 a 数据元素类型相同的一个值。·static boolean equals（type [] a，type [] b）如果两个数组大小相同，并且下标相同的元素都对应相等，返回 true。参数：a、b　类型为 int、long、short、char、byte、boolean、float 或 double 的两个数组。
