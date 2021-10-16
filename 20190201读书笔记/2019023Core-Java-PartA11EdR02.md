## 记忆时间

## 目录

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

```java
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
```

The keyword final indicates that you can assign to the variable once, and then its value is set once and for all. It is customary to name constants in all uppercase.

It is probably more common in Java to create a constant so it's available to multiple methods inside a single class. These are usually called class constants. Set up a class constant with the keywords static final. Here is an example of using a class constant:

```Java
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
```

Note that the definition of the class constant appears outside the main method. Thus, the constant can also be used in other methods of the same class. Furthermore, if the constant is declared, as in our example, public, methods of other classes can also use it—in our example, as Constants2.CM_PER_INCH.

C++ Note: const is a reserved Java keyword, but it is not currently used for anything. You must use final for a constant.

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

很多 Intel 处理器计算 x*y，并且将结果存储在 80 位的寄存器中，再除以 z 并将结果截断为 64 位。这样可以得到一个更加精确的计算结果，并且还能够避免产生指数溢出。但是，这个结果可能与始终在 64 位机器上计算的结果不一样。因此，Java 虚拟机的最初规范规定所有的中间计算都必须进行截断。这种行为遭到了数值计算团体的反对。截断计算不仅可能导致溢出，而且由于截断操作需要消耗时间，所以在计算速度上实际上要比精确计算慢。为此，Java 程序设计语言承认了最优性能与理想结果之间存在的冲突，并给予了改进。在默认情况下，虚拟机设计者允许对中间计算结果采用扩展的精度。但是，对于使用 strictfp 关键字标记的方法必须使用严格的浮点计算来生成可再生的结果。例如，可以把 main 方法标记为：

于是，在 main 方法中的所有指令都将使用严格的浮点计算。如果将一个类标记为 strictfp，这个类中的所有方法都要使用严格的浮点计算。

实际的计算方式将取决于 Intel 处理器的行为。在默认情况下，中间结果允许使用扩展的指数，但不允许使用扩展的尾数（Intel 芯片在截断尾数时并不损失性能）。因此，这两种方式的区别仅仅在于采用默认的方式不会产生溢出，而采用严格的计算有可能产生溢出。

如果没有仔细阅读这个注释，也没有什么关系。对大多数程序来说，浮点溢出不属于大问题。在本书中，将不使用 strictfp 关键字。

#### 3.5.1 Arithmetic Operators

The usual arithmetic operators +, -, *, / are used in Java for addition, subtraction, multiplication, and division. The / operator denotes integer division if both arguments are integers, and floating-point division otherwise. Integer remainder (sometimes called modulus) is denoted by %. For example, 15 / 2 is 7, 15 % 2 is 1, and 15.0 / 2 is 7.5.

Note that integer division by 0 raises an exception, whereas floating-point division by 0 yields an infinite or NaN result.

Note: One of the stated goals of the Java programming language is portability. A computation should yield the same results no matter which virtual machine executes it. For arithmetic computations with floating-point numbers, it is surprisingly difficult to achieve this portability. The double type uses 64 bits to store a numeric value, but some processors use 80-bit floating-point registers. These registers yield added precision in intermediate steps of a computation. For example, consider the following computation:

```java
double w = x * y / z;
```

Many Intel processors compute x * y, leave the result in an 80-bit register, then divide by z, and finally truncate the result back to 64 bits. That can yield a more accurate result, and it can avoid exponent overflow. But the result may be different from a computation that uses 64 bits throughout. For that reason, the initial specification of the Java virtual machine mandated that all intermediate computations must be truncated. The numeric community hated it. Not only can the truncated computations cause overflow, they are actually slower than the more precise computations because the truncation operations take time. For that reason, the Java programming language was updated to recognize the conflicting demands for optimum performance and perfect reproducibility. By default, virtual machine designers are now permitted to use extended precision for intermediate computations. However, methods tagged with the strictfp keyword must use strict floating-point operations that yield reproducible results.

For example, you can tag main as:

```java
public static strictfp void main(String[] args)
```

Then all instructions inside the main method will use strict floating-point computations. If you tag a class as strictfp, then all of its methods must use strict floating-point computations.

The gory details are very much tied to the behavior of the Intel processors. In the default mode, intermediate results are allowed to use an extended exponent, but not an extended mantissa. (The Intel chips support truncation of the mantissa without loss of performance.) Therefore, the only difference between the default and strict modes is that strict computations may overflow when default computations don't.

If your eyes glazed over when reading this note, don't worry. Floating-point overflow isn't a problem that one encounters for most common programs. We don't use the strictfp keyword in this book.

#### 3.5.2 Mathematical Functions and Constants

The Math class contains an assortment of mathematical functions that you may occasionally need, depending on the kind of programming that you do.

To take the square root of a number, use the sqrt method:

```java
double x = 4;

double y = Math.sqrt(x);

System.out.println(y); // prints 2.0
```

Note: There is a subtle difference between the println method and the sqrt method. The println method operates on the System.out object. But the sqrt method in the Math class does not operate on any object. Such a method is called a static method. You can learn more about static methods in Chapter 4.

The Java programming language has no operator for raising a quantity to a power: You must use the pow method in the Math class. The statement

```java
double y = Math.pow(x, a);
```

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

Tip: You can avoid the Math prefix for the mathematical methods and constants by adding the following line to the top of your source file:

```java
import static java.lang.Math.*;
```

For example:

```java
System.out.println("The square root of \u03C0 is " + sqrt(PI));
```

We discuss static imports in Chapter 4.

Note: The methods in the Math class use the routines in the computer's floating-point unit for fastest performance. If completely predictable results are more important than performance, use the StrictMath class instead. It implements the algorithms from the「Freely Distributable Math Library」(www.netlib.org/fdlibm), guaranteeing identical results on all platforms.

Note: The Math class provides several methods to make integer arithmetic safer. The mathematical operators quietly return wrong results when a computation overflows. For example, one billion times three (1000000000 * 3) evaluates to -1294967296 because the largest int value is just over two billion. If you call Math.multiplyExact(1000000000, 3) instead, an exception is generated. You can catch that exception or let the program terminate rather than quietly continue with a wrong result. There are also methods addExact, subtractExact, incrementExact, decrementExact, negateExact, all with int and long parameters.

3.5.2 数学函数与常量

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

```java
int n = 123456789;
float f = n; // f is 1.23456792E8
```

When two values are combined with a binary operator (such as n + f where n is an integer and f is a floating-point value), both operands are converted to a common type before the operation is carried out.

If either of the operands is of type double, the other one will be converted to a double.

Otherwise, if either of the operands is of type float, the other one will be converted to a float.

Otherwise, if either of the operands is of type long, the other one will be converted to a long.

Otherwise, both operands will be converted to an int.

3.5.3 数值类型之间的转换

经常需要将一种数值类型转换为另一种数值类型。图 3-1 给出了数值类型之间的合法转换。

在图 3-1 中有 6 个实心箭头，表示无信息丢失的转换；有 3 个虚箭头，表示可能有精度损失的转换。例如，123456789 是一个大整数，它所包含的位数比 float 类型所能够表达的位数多。当将这个整型数值转换为 float 类型时，将会得到同样大小的结果，但却失去了一定的精度。

图 3-1 数值类型之间的合法转换

当使用上面两个数值进行二元操作时（例如 n+f，n 是整数，f 是浮点数），先要将两个操作数转换为同一种类型，然后再进行计算。

1、如果两个操作数中有一个是 double 类型，另一个操作数就会转换为 double 类型。

2、否则，如果其中一个操作数是 float 类型，另一个操作数将会转换为 float 类型。

3、否则，如果其中一个操作数是 long 类型，另一个操作数将会转换为 long 类型。

4、否则，两个操作数都将被转换为 int 类型。

#### 3.5.4 Casts

In the preceding section, you saw that int values are automatically converted to double values when necessary. On the other hand, there are obviously times when you want to consider a double as an integer. Numeric conversions are possible in Java, but of course information may be lost. Conversions in which loss of information is possible are done by means of casts. The syntax for casting is to give the target type in parentheses, followed by the variable name. For example:

```java
double x = 9.997;
int nx = (int) x;
```

Now, the variable nx has the value 9 because casting a floating-point value to an integer discards the fractional part.

If you want to round a floating-point number to the nearest integer (which in most cases is a more useful operation), use the Math.round method:

```java
double x = 9.997;
int nx = (int) Math.round(x);
```

Now the variable nx has the value 10. You still need to use the cast (int) when you call round. The reason is that the return value of the round method is a long, and a long can only be assigned to an int with an explicit cast because there is the possibility of information loss.

Caution: If you try to cast a number of one type to another that is out of range for the target type, the result will be a truncated number that has a different value. For example, (byte) 300 is actually 44.

C++ Note: You cannot cast between boolean values and any numeric type. This convention prevents common errors. In the rare case when you want to convert a boolean value to a number, you can use a conditional expression such as b ? 1 : 0.

3.5.4 强制类型转换

在上一小节中看到，在必要的时候，int 类型的值将会自动地转换为 double 类型。但另一方面，有时也需要将 double 转换成 int。在 Java 中，允许进行这种数值之间的类型转换。当然，有可能会丢失一些信息。在这种情况下，需要通过强制类型转换（cast）实现这个操作。强制类型转换的语法格式是在圆括号中给出想要转换的目标类型，后面紧跟待转换的变量名。例如：

这样，变量 nx 的值为 9。强制类型转换通过截断小数部分将浮点值转换为整型。

如果想对浮点数进行舍入运算，以便得到最接近的整数（在很多情况下，这种操作更有用），那就需要使用 Math.round 方法：

现在，变量 nx 的值为 10。当调用 round 的时候，仍然需要使用强制类型转换（int）。其原因是 round 方法返回的结果为 long 类型，由于存在信息丢失的可能性，所以只有使用显式的强制类型转换才能够将 long 类型转换成 int 类型。

警告：如果试图将一个数值从一种类型强制转换为另一种类型，而又超出了目标类型的表示范围，结果就会截断成一个完全不同的值。例如，（byte）300 的实际值为 44。

C++ 注释：不要在 boolean 类型与任何数值类型之间进行强制类型转换，这样可以防止发生错误。只有极少数的情况才需要将布尔类型转换为数值类型，这时可以使用条件表达式 b?1:0。

#### 3.5.5 Combining Assignment with Operators

There is a convenient shortcut for using binary operators in an assignment. For example,

```java
x += 4;
```

is equivalent to

```java
x = x + 4;
```

(In general, place the operator to the left of the = sign, such as *= or %=.)

Note: If the operator yields a value whose type is different from that of the left-hand side, then it is coerced to fit. For example, if x is an int, then the statement

```java
x += 3.5;
```

is valid, setting x to (int)(x + 3.5).

3.5.4 结合赋值和运算符

可以在赋值中使用二元运算符，这是一种很方便的简写形式。例如，

等价于：

（一般地，要把运算符放在 = 号左边，如 *= 或 %=）。

注释：如果运算符得到一个值，其类型与左侧操作数的类型不同，就会发生强制类型转换。例如，如果 x 是一个 int，则以下语句

是合法的，将把 x 设置为（int）（x+3.5）。

#### 3.5.6 Increment and Decrement Operators

Programmers, of course, know that one of the most common operations with a numeric variable is to add or subtract 1. Java, following in the footsteps of C and C++, has both increment and decrement operators: n++ adds 1 to the current value of the variable n, and n-- subtracts 1 from it. For example, the code

```java
int n = 12;
n++;
```

changes n to 13. Since these operators change the value of a variable, they cannot be applied to numbers themselves. For example, 4++ is not a legal statement.

There are two forms of these operators; you've just seen the postfix form of the operator that is placed after the operand. There is also a prefix form, ++n. Both change the value of the variable by 1. The difference between the two appears only when they are used inside expressions. The prefix form does the addition first; the postfix form evaluates to the old value of the variable.

```java
int m = 7;
int n = 7;

int a = 2 * ++m; // now a is 16, m is 8
int b = 2 * n++; // now b is 14, n is 8
```

We recommend against using ++ inside expressions because this often leads to confusing code and annoying bugs.

3.5.6 自增与自减运算符

当然，程序员都知道加 1、减 1 是数值变量最常见的操作。在 Java 中，借鉴了 C 和 C++ 的做法，也提供了自增、自减运算符：n++ 将变量 n 的当前值加 1，n-- 则将 n 的值减 1。例如，以下代码：

将 n 的值改为 13。由于这些运算符会改变变量的值，所以它们的操作数不能是数值。例如，4++ 就不是一个合法的语句。

实际上，这些运算符有两种形式；上面介绍的是运算符放在操作数后面的「后缀」形式。还有一种「前缀」形式：++n。后缀和前缀形式都会使变量值加 1 或减 1。但用在表达式中时，二者就有区别了。前缀形式会先完成加 1；而后缀形式会使用变量原来的值。

建议不要在表达式中使用 ++，因为这样的代码很容易让人困惑，而且会带来烦人的 bug。

#### 3.5.7 Relational and boolean Operators

Java has the full complement of relational operators. To test for equality, use a double equal sign, ==. For example, the value of

```java
3 == 7
```

is false.

Use a != for inequality. For example, the value of

```java
3 != 7
```

is true.

Finally, you have the usual < (less than), > (greater than), <= (less than or equal), and >= (greater than or equal) operators.

Java, following C++, uses && for the logical「and」operator and || for the logical「or」operator. As you can easily remember from the != operator, the exclamation point ! is the logical negation operator. The && and || operators are evaluated in「short circuit」fashion: The second argument is not evaluated if the first argument already determines the value. If you combine two expressions with the && operator,

```java
expression1 && expression2
```

and the truth value of the first expression has been determined to be false, then it is impossible for the result to be true. Thus, the value for the second expression is not calculated. This behavior can be exploited to avoid errors. For example, in the expression

```java
x != 0 && 1 / x > x + y // no division by 0
```

the second part is never evaluated if x equals zero. Thus, 1 / x is not computed if x is zero, and no divide-by-zero error can occur.

Similarly, the value of expression1 || expression2 is automatically true if the first expression is true, without evaluating the second expression.

Finally, Java supports the ternary ?: operator that is occasionally useful. The expression

```java
condition ? expression1 : expression2
```

evaluates to the first expression if the condition is true, to the second expression otherwise. For example,

```java
x < y ? x : y
```

gives the smaller of x and y.

3.5.7 关系和 boolean 运算符

Java 包含丰富的关系运算符。要检测相等性，可以使用两个等号 ==。例如，

的值为 false。另外可以使用 != 检测不相等。例如，

的值为 true。

最后，还有经常使用的 <（小于）、>（大于）、<=（小于等于）和>=（大于等于）运算符。

Java 沿用了 C++ 的做法，使用 && 表示逻辑「与」运算符，使用 || 表示逻辑「或」运算符。从 != 运算符可以想到，感叹号 ！ 就是逻辑非运算符。&& 和 || 运算符是按照「短路」方式来求值的：如果第一个操作数已经能够确定表达式的值，第二个操作数就不必计算了。如果用 && 运算符合并两个表达式，

而且已经计算得到第一个表达式的真值为 false，那么结果就不可能为 true。因此，第二个表达式就不必计算了。可以利用这一点来避免错误。例如，在下面的表达式中：

如果 x 等于 0，那么第二部分就不会计算。因此，如果 x 为 0，也就不会计算 1/x，除以 0 的错误就不会出现。

类似地，如果第一个表达式为 true，`expression1 || expression2` 的值就自动为 true，而无需计算第二个表达式。

最后一点，Java 支持三元操作符 ?:，这个操作符有时很有用。如果条件为 true，下面的表达式：

就为第一个表达式的值，否则计算为第二个表达式的值。例如，

会返回 x 和 y 中较小的一个。

#### 3.5.8 Bitwise Operators

For any of the integer types, you have operators that can work directly with the bits that make up the integers. This means that you can use masking techniques to get at individual bits in a number. The bitwise operators are

```java
& ("and") | ("or") ^ ("xor") ~ ("not")
```

These operators work on bit patterns. For example, if n is an integer variable, then

```java
int fourthBitFromRight = (n & 0b1000) / 0b1000;
```

gives you a 1 if the fourth bit from the right in the binary representation of n is 1, and 0 otherwise. Using & with the appropriate power of 2 lets you mask out all but a single bit.

Note: When applied to boolean values, the & and | operators yield a boolean value. These operators are similar to the && and || operators, except that the & and | operators are not evaluated in「short circuit」fashion—that is, both arguments are evaluated before the result is computed.

There are also >> and << operators which shift a bit pattern right or left. These operators are convenient when you need to build up bit patterns to do bit masking:

```java
int fourthBitFromRight = (n & (1 << 3)) >> 3;
```

Finally, a >>> operator fills the top bits with zero, unlike >> which extends the sign bit into the top bits. There is no <<< operator.

Caution: The right-hand argument of the shift operators is reduced modulo 32 (unless the left-hand argument is a long, in which case the right-hand argument is reduced modulo 64). For example, the value of 1 << 35 is the same as 1 << 3 or 8.

C++ Note: In C/C++, there is no guarantee as to whether >> performs an arithmetic shift (extending the sign bit) or a logical shift (filling in with zeroes). Implementors are free to choose whichever is more efficient. That means the C/C++ >> operator may yield implementation-dependent results for negative numbers. Java removes that uncertainty.

3.5.8 位运算符

处理整型类型时，可以直接对组成整型数值的各个位完成操作。这意味着可以使用掩码技术得到整数中的各个位。位运算符包括：

这些运算符按位模式处理。例如，如果 n 是一个整数变量，而且用二进制表示的 n 从右边数第 4 位为 1，则：

会返回 1，否则返回 0。利用 & 并结合使用适当的 2 的幂，可以把其他位掩掉，而只保留其中的某一位。

注释：应用在布尔值上时，& 和 | 运算符也会得到一个布尔值。这些运算符与 && 和 || 运算符很类似，不过 & 和 | 运算符不采用「短路」方式来求值，也就是说，得到计算结果之前两个操作数都需要计算。

另外，还有 >> 和 << 运算符将位模式左移或右移。需要建立位模式来完成位掩码时，这两个运算符会很方便：

最后，>>> 运算符会用 0 填充高位，这与 >> 不同，它会用符号位填充高位。不存在 <<< 运算符。

警告：移位运算符的右操作数要完成模 32 的运算（除非左操作数是 long 类型，在这种情况下需要对右操作数模 64）。例如，1<<35 的值等同于 1<<3 或 8。

C++ 注释：在 C/C++ 中，不能保证 >> 是完成算术移位（扩展符号位）还是逻辑移位（填充 0）。实现者可以选择其中更高效的任何一种做法。这意味着 C/C++>> 运算符对于负数生成的结果可能会依赖于具体的实现。Java 则消除了这种不确定性。

#### 3.5.9 Parentheses and Operator Hierarchy

Table 3.4 shows the precedence of operators. If no parentheses are used, operations are performed in the hierarchical order indicated. Operators on the same level are processed from left to right, except for those that are right-associative, as indicated in the table. For example, && has a higher precedence than ||, so the expression

Table 3.4 Operator Precedence

| Operators | Associativity |
| --- | --- |
| [] . () (method call) | Left to right |
| ! ~ ++ -- + (unary) - (unary) () (cast) new | Right to left |
| * / % | Left to right |
| + - | Left to right |
| << >> >>> | Left to right |
| < <= > >= instanceof | Left to right |
| == != | Left to right |
| & | Left to right |
| ^ | Left to right |
| | | Left to right |
| && | Left to right |
| || | Left to right |
| ?: | Right to left |
| = += -= *= /= %= &= |= ^= <<= >>= >>>= | Right to left |

a && b

means

(a && b) || c

Since += associates right to left, the expression

a += b += c

means

a += (b += c)

That is, the value of b += c (which is the value of b after the addition) is added to a.

C++ Note: Unlike C or C++, Java does not have a comma operator. However, you can use a comma-separated list of expressions in the first and third slot of a for statement.

3.5.9 括号与运算符级别

表 3-4 给出了运算符的优先级。如果不使用圆括号，就按照给出的运算符优先级次序进行计算。同一个级别的运算符按照从左到右的次序进行计算（除了表中给出的右结合运算符外。）例如，由于 && 的优先级比 || 的优先级高，所以表达式表 3-4 运算符优先级：

等价于：

又因为 += 是右结合运算符，所以表达式：

等价于：

也就是将 b+=c 的结果（加上 c 之后的 b）加到 a 上。

C++ 注释：与 C 或 C++ 不同，Java 不使用逗号运算符。不过，可以在 for 语句的第 1 和第 3 部分中使用逗号分隔表达式列表。

3.5.10 枚举类型

有时候，变量的取值只在一个有限的集合内。例如：销售的服装或比萨饼只有小、中、大和超大这四种尺寸。当然，可以将这些尺寸分别编码为 1、2、3、4 或 S、M、L、X。但这样存在着一定的隐患。在变量中很可能保存的是一个错误的值（如 0 或 m）。

针对这种情况，可以自定义枚举类型。枚举类型包括有限个命名的值。例如，

现在，可以声明这种类型的变量：

Size 类型的变量只能存储这个类型声明中给定的某个枚举值，或者 null 值，null 表示这个变量没有设置任何值。有关枚举类型的详细内容将在第 5 章介绍。

### 3.6 Strings

Conceptually, Java strings are sequences of Unicode characters. For example, the string "Java\u2122" consists of the five Unicode characters J, a, v, a, and ™. Java does not have a built-in string type. Instead, the standard Java library contains a predefined class called, naturally enough, String. Each quoted string is an instance of the String class:

```java
String e = ""; // an empty string

String greeting = "Hello";
```

3.6 字符串

从概念上讲，Java 字符串就是 Unicode 字符序列。例如，字符串 "Java\u2122" 由 5 个 Unicode 字符 J、a、v、a 和 TM。Java 没有内置的字符串类型，而是在标准 Java 类库中提供了一个预定义类，很自然地叫做 String。每个用双引号括起来的字符串都是 String 类的一个实例：

#### 3.6.1 Substrings

You can extract a substring from a larger string with the substring method of the String class. For example,

```java
String greeting = "Hello";

String s = greeting.substring(0, 3);
```

creates a string consisting of the characters "Hel".

Note: Like C and C++, Java counts code units and code points in strings starting with 0.

The second parameter of substring is the first position that you do not want to copy. In our case, we want to copy positions 0, 1, and 2 (from position 0 to position 2 inclusive). As substring counts it, this means from position 0 inclusive to position 3 exclusive.

There is one advantage to the way substring works: Computing the length of the substring is easy. The string s.substring(a, b) always has length b − a. For example, the substring "Hel" has length 3 − 0 = 3.

3.6.1 子串

String 类的 substring 方法可以从一个较大的字符串提取出一个子串。例如：

创建了一个由字符 "Hel" 组成的字符串。

substring 方法的第二个参数是不想复制的第一个位置。这里要复制位置为 0、1 和 2（从 0 到 2，包括 0 和 2）的字符。在 substring 中从 0 开始计数，直到 3 为止，但不包含 3。

substring 的工作方式有一个优点：容易计算子串的长度。字符串 s.substring(a, b) 的长度为 b-a。例如，子串 "Hel" 的长度为 3-0=3。

#### 3.6.2 Concatenation

Java, like most programming languages, allows you to use + to join (concatenate) two strings.

```java
String expletive = "Expletive";

String PG13 = "deleted";

String message = expletive + PG13;
```

The preceding code sets the variable message to the string "Expletivedeleted". (Note the lack of a space between the words: The + operator joins two strings in the order received, exactly as they are given.)

When you concatenate a string with a value that is not a string, the latter is converted to a string. (As you will see in Chapter 5, every Java object can be converted to a string.) For example,

```java
int age = 13;

String rating = "PG" + age;
```

sets rating to the string "PG13".

This feature is commonly used in output statements. For example,

```java
System.out.println("The answer is " + answer);
```

is perfectly acceptable and prints what you would expect (and with correct spacing because of the space after the word is).

If you need to put multiple strings together, separated by a delimiter, use the static join method:

```java
String all = String.join(" / ", "S", "M", "L", "XL");

// all is the string "S / M / L / XL"
```

As of Java 11, there is a repeat method:

```java
String repeated = "Java".repeat(3); // repeated is "JavaJavaJava"
```

3.6.2 拼接

与绝大多数的程序设计语言一样，Java 语言允许使用 + 号连接（拼接）两个字符串。

上述代码将「Expletivedeleted」赋给变量 message（注意，单词之间没有空格，+ 号按照给定的次序将两个字符串拼接起来）。

当将一个字符串与一个非字符串的值进行拼接时，后者被转换成字符串（在第 5 章中可以看到，任何一个 Java 对象都可以转换成字符串）。例如： rating 设置为「PG13」。这种特性通常用在输出语句中。例如：

这是一条合法的语句，并且将会打印出所希望的结果（因为单词 is 后面加了一个空格，输出时也会加上这个空格）。如果需要把多个字符串放在一起，用一个定界符分隔，可以使用静态 join 方法：

#### 3.6.3 Strings Are Immutable

The String class gives no methods that let you change a character in an existing string. If you want to turn greeting into "Help!", you cannot directly change the last positions of greeting into 'p' and '!'. If you are a C programmer, this can make you feel pretty helpless. How are we going to modify the string? In Java, it is quite easy: Concatenate the substring that you want to keep with the characters that you want to replace.

```java
greeting = greeting.substring(0, 3) + "p!";
```

This declaration changes the current value of the greeting variable to "Help!".

Since you cannot change the individual characters in a Java string, the documentation refers to the objects of the String class as immutable. Just as the number 3 is always 3, the string "Hello" will always contain the code-unit sequence for the characters H, e, l, l, o. You cannot change these values. Yet you can, as you just saw, change the contents of the string variable greeting and make it refer to a different string, just as you can make a numeric variable currently holding the value 3 hold the value 4.

Isn't that a lot less efficient? It would seem simpler to change the code units than to build up a whole new string from scratch. Well, yes and no. Indeed, it isn't efficient to generate a new string that holds the concatenation of "Hel" and "p!". But immutable strings have one great advantage: The compiler can arrange that strings are shared.

To understand how this works, think of the various strings as sitting in a common pool. String variables then point to locations in the pool. If you copy a string variable, both the original and the copy share the same characters.

Overall, the designers of Java decided that the efficiency of sharing outweighs the inefficiency of string editing by extracting substrings and concatenating. Look at your own programs; we suspect that most of the time, you don't change strings—you just compare them. (There is one common exception—assembling strings from individual characters or from shorter strings that come from the keyboard or a file. For these situations, Java provides a separate class that we describe in Section 3.6.9,「Building Strings,」on p. 74.)

C++ Note: C programmers are generally bewildered when they see Java strings for the first time because they think of strings as arrays of characters:

```java
char greeting[] = "Hello";
```

That is a wrong analogy: A Java string is roughly analogous to a char* pointer,

```java
char* greeting = "Hello";
```

When you replace greeting with another string, the Java code does roughly the following:

```java
char* temp = malloc(6);

strncpy(temp, greeting, 3);

strncpy(temp + 3, "p!", 3);

greeting = temp;
```

Sure, now greeting points to the string "Help!". And even the most hardened C programmer must admit that the Java syntax is more pleasant than a sequence of strncpy calls. But what if we make another assignment to greeting?

```java
greeting = "Howdy";
```

Don't we have a memory leak? After all, the original string was allocated on the heap. Fortunately, Java does automatic garbage collection. If a block of memory is no longer needed, it will eventually be recycled.

If you are a C++ programmer and use the string class defined by ANSI C++, you will be much more comfortable with the Java String type. C++ string objects also perform automatic allocation and deallocation of memory. The memory management is performed explicitly by constructors, assignment operators, and destructors. However, C++ strings are mutable—you can modify individual characters in a string.

3.6.3 不可变字符串

String 类没有提供用于修改字符串的方法。如果希望将 greeting 的内容修改为 "Help!"，不能直接地将 greeting 的最后两个位置的字符修改为 "p" 和 "!"。这对于 C 程序员来说，将会感到无从下手。如何修改这个字符串呢？在 Java 中实现这项操作非常容易。首先提取需要的字符，然后再拼接上替换的字符串：

```java
greeting = greeting.substring(0, 3) + "p!";
```

上面这条语句将 greeting 当前值修改为 "Help!"。

由于不能修改 Java 字符串中的字符，所以在 Java 文档中将 String 类对象称为不可变字符串，如同数字 3 永远是数字 3 一样，字符串「Hello」永远包含字符 H、e、l、l 和 o 的代码单元序列，而不能修改其中的任何一个字符。当然，可以修改字符串变量 greeting，让它引用另外一个字符串，这就如同可以将存放 3 的数值变量改成存放 4 一样。

这样做是否会降低运行效率呢？看起来好像修改一个代码单元要比创建一个新字符串更加简洁。答案是：也对，也不对。的确，通过拼接「Hel」和「p!」来创建一个新字符串的效率确实不高。但是，不可变字符串却有一个优点：编译器可以让字符串共享。

为了弄清具体的工作方式，可以想象将各种字符串存放在公共的存储池中。字符串变量指向存储池中相应的位置。如果复制一个字符串变量，原始字符串与复制的字符串共享相同的字符。

总而言之，Java 的设计者认为共享带来的高效率远远胜过于提取、拼接字符串所带来的低效率。查看一下程序会发现：很少需要修改字符串，而是往往需要对字符串进行比较（有一种例外情况，将来自于文件或键盘的单个字符或较短的字符串汇集成字符串。为此，Java 提供了一个独立的类，在 3.6.9 节中将详细介绍）。

C++ 注释：在 C 程序员第一次接触 Java 字符串的时候，常常会感到迷惑，因为他们总将字符串认为是字符型数组：

这种认识是错误的，Java 字符串大致类似于 char * 指针，

当采用另一个字符串替换 greeting 的时候，Java 代码大致进行下列操作：

的确，现在 greeting 指向字符串 "Help!"。即使一名最顽固的 C 程序员也得承认 Java 语法要比一连串的 strncpy 调用舒适得多。然而，如果将 greeting 赋予另外一个值又会怎样呢？

这样做会不会产生内存遗漏呢？毕竟，原始字符串放置在堆中。十分幸运，Java 将自动地进行垃圾回收。如果一块内存不再使用了，系统最终会将其回收。

对于一名使用 ANSI C++ 定义的 string 类的 C++ 程序员，会感觉使用 Java 的 String 类型更为舒适。C++ string 对象也自动地进行内存的分配与回收。内存管理是通过构造器、赋值操作和析构器显式执行的。然而，C++ 字符串是可修改的，也就是说，可以修改字符串中的单个字符。

#### 3.6.4 Testing Strings for Equality

To test whether two strings are equal, use the equals method. The expression:

```java
s.equals(t)
```

returns true if the strings s and t are equal, false otherwise. Note that s and t can be string variables or string literals. For example, the expression

```java
"Hello".equals(greeting)
```

is perfectly legal. To test whether two strings are identical except for the upper/lowercase letter distinction, use the equalsIgnoreCase method.

```java
"Hello".equalsIgnoreCase("hello")
```

Do not use the == operator to test whether two strings are equal! It only determines whether or not the strings are stored in the same location. Sure, if strings are in the same location, they must be equal. But it is entirely possible to store multiple copies of identical strings in different places.

```java
String greeting = "Hello"; // initialize greeting to a string

if (greeting == "Hello") . . .

// probably true

if (greeting.substring(0, 3) == "Hel") . . .

// probably false
```

If the virtual machine always arranges for equal strings to be shared, then you could use the == operator for testing equality. But only string literals are shared, not strings that are the result of operations like + or substring. Therefore, never use == to compare strings lest you end up with a program with the worst kind of bug—an intermittent one that seems to occur randomly.

C++ Note: If you are used to the C++ string class, you have to be particularly careful about equality testing. The C++ string class does overload the == operator to test for equality of the string contents. It is perhaps unfortunate that Java goes out of its way to give strings the same「look and feel」as numeric values but then makes strings behave like pointers for equality testing. The language designers could have redefined == for strings, just as they made a special arrangement for +. Oh well, every language has its share of inconsistencies.

C programmers never use == to compare strings but use strcmp instead. The Java method compareTo is the exact analog of strcmp. You can use

```java
if (greeting.compareTo("Hello") == 0) . . .
```

but it seems clearer to use equals instead.

3.6.4 检测字符串是否相等

可以使用 equals 方法检测两个字符串是否相等。对于表达式：

如果字符串 s 与字符串 t 相等，则返回 true；否则，返回 false。需要注意，s 与 t 可以是字符串变量，也可以是字符串字面量。例如，下列表达式是合法的：

要想检测两个字符串是否相等，而不区分大小写，可以使用 equalsIgnoreCase 方法。

一定不要使用 == 运算符检测两个字符串是否相等！这个运算符只能够确定两个字符串是否放置在同一个位置上。当然，如果字符串放置在同一个位置上，它们必然相等。但是，完全有可能将内容相同的多个字符串的拷贝放置在不同的位置上。

1『不能用 == 来比较两个字符串是否相等。做一张任意卡片（2021-10-16）』—— 已完成

如果虚拟机始终将相同的字符串共享，就可以使用 == 运算符检测是否相等。但实际上只有字符串常量是共享的，而 + 或 substring 等操作产生的结果并不是共享的。因此，千万不要使用 == 运算符测试字符串的相等性，以免在程序中出现糟糕的 bug。从表面上看，这种 bug 很像随机产生的间歇性错误。

C++ 注释：对于习惯使用 C++ 的 string 类的人来说，在进行相等性检测的时候一定要特别小心。C++ 的 string 类重载了 == 运算符以便检测字符串内容的相等性。可惜 Java 没有采用这种方式，它的字符串「看起来、感觉起来」与数值一样，但进行相等性测试时，其操作方式又类似于指针。语言的设计者本应该像对 + 那样也进行特殊处理，即重定义 == 运算符。当然，每一种语言都会存在一些不太一致的地方。

C 程序员从不使用 == 对字符串进行比较，而使用 strcmp 函数。Java 的 compareTo 方法与 strcmp 完全类似，因此，可以这样使用：

不过，使用 equals 看起来更为清晰。

#### 3.6.5 Empty and Null Strings

The empty string "" is a string of length 0. You can test whether a string is empty by calling

```java
if (str.length() == 0)
```

or

```java
if (str.equals(""))
```

An empty string is a Java object which holds the string length (namely, 0) and an empty contents. However, a String variable can also hold a special value, called null, that indicates that no object is currently associated with the variable. (See Chapter 4 for more information about null.) To test whether a string is null, use

```java
if (str == null)
```

Sometimes, you need to test that a string is neither null nor empty. Then use

```java
if (str != null && str.length() != 0)
```

You need to test that str is not null first. As you will see in Chapter 4, it is an error to invoke a method on a null value.

3.6.5 空串与 Null 串空串

"" 是长度为 0 的字符串。可以调用以下代码检查一个字符串是否为空：

或：

空串是一个 Java 对象，有自己的串长度（0）和内容（空）。不过，String 变量还可以存放一个特殊的值，名为 null，这表示目前没有任何对象与该变量关联（关于 null 的更多信息请参见第 4 章）。要检查一个字符串是否为 null，要使用以下条件：

有时要检查一个字符串既不是 null 也不为空串，这种情况下就需要使用以下条件：

首先要检查 str 不为 null。在第 4 章会看到，如果在一个 null 值上调用方法，会出现错误。

#### 3.6.6 Code Points and Code Units

Java strings are sequences of char values. As we discussed in Section 3.3.3,「The char Type,」on p. 46, the char data type is a code unit for representing Unicode code points in the UTF-16 encoding. The most commonly used Unicode characters can be represented with a single code unit. The supplementary characters require a pair of code units.

The length method yields the number of code units required for a given string in the UTF-16 encoding. For example:

```java
String greeting = "Hello";
int n = greeting.length(); // is 5
```

To get the true length—that is, the number of code points—call

```java
int cpCount = greeting.codePointCount(0, greeting.length());
```

The call s.charAt(n) returns the code unit at position n, where n is between 0 and s.length() – 1. For example:

```java
char first = greeting.charAt(0); // first is 'H'
char last = greeting.charAt(4); // last is 'o'
```

To get at the ith code point, use the statements

```java
int index = greeting.offsetByCodePoints(0, i);
int cp = greeting.codePointAt(index);
```

Why are we making a fuss about code units? Consider the sentence

```
XXXX is the set of octonions.
```

The character (U+1D546) requires two code units in the UTF-16 encoding. Calling:

```java
char ch = sentence.charAt(1)
```

doesn't return a space but the second code unit of XXXX. To avoid this problem, you should not use the char type. It is too low-level.

Note: Don't think that you can ignore exotic characters with code units above U+FFFF. Your emoji-loving users may put characters such as (U+1F37A, beer mug) into strings.

If your code traverses a string, and you want to look at each code point in turn, you can use these statements:

```java
int cp = sentence.codePointAt(i);
if (Character.isSupplementaryCodePoint(cp)) i += 2;
else i++;
```

You can move backwards with the following statements:

```java
i--;
if (Character.isSurrogate(sentence.charAt(i))) i--;
int cp = sentence.codePointAt(i);
```

Obviously, that is quite painful. An easier way is to use the codePoints method that yields a「stream」of int values, one for each code point. (We will discuss streams in Chapter 2 of Volume II.) You can just turn the stream into an array (see Section 3.10,「Arrays,」on p. 108) and traverse that.

```java
int[] codePoints = str.codePoints().toArray();
```

Conversely, to turn an array of code points to a string, use a constructor. (We discuss constructors and the new operator in detail in Chapter 4.)

```java
String str = new String(codePoints, 0, codePoints.length);
```

Note: The virtual machine does not have to implement strings as sequences of code units. In Java 9, strings that hold only single-byte code units use a byte array, and all others a char array.

3.6.6 码点与代码单元

Java 字符串由 char 值序列组成。从 3.3.3 节「char 类型」已经看到，char 数据类型是一个采用 UTF-16 编码表示 Unicode 码点的代码单元。大多数的常用 Unicode 字符使用一个代码单元就可以表示，而辅助字符需要一对代码单元表示。

length 方法将返回采用 UTF-16 编码表示的给定字符串所需要的代码单元数量。例如：

要想得到实际的长度，即码点数量，可以调用：

调用 s.charAt(n) 将返回位置 n 的代码单元，n 介于 0~s.length()-1 之间。例如：

要想得到第 i 个码点，应该使用下列语句:

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

java.lang.String 1.0:

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

Note: In the API notes, there are a few parameters of type CharSequence. This is an interface type to which all strings belong. You will learn about interface types in Chapter 6. For now, you just need to know that you can pass arguments of type String whenever you see a CharSequence parameter.

3.6.7 String API

Java 中的 String 类包含了 50 多个方法。令人惊讶的是绝大多数都很有用，可以设想使用的频繁非常高。下面的 API 注释汇总了一部分最常用的方法。

注释：可以发现，本书中给出的 API 注释会有助于理解 Java 应用程序编程接口（API）。每一个 API 的注释都以形如 java.lang.String 的类名开始。（java.lang 包的重要性将在第 4 章给出解释。）类名之后是一个或多个方法的名字、解释和参数描述。

在这里，一般不列出某个类的所有方法，而是选择一些最常用的方法，并以简洁的方式给予描述。完整的方法列表请参看联机文档（请参看 3.6.8 节）。

这里还列出了所给类的版本号。如果某个方法是在这个版本之后添加的，就会给出一个单独的版本号。

java.lang.string 1.0:

char charAt(int index) 返回给定位置的代码单元。除非对底层的代码单元感兴趣，否则不需要调用这个方法。

int codePointAt(int index) 5.0 返回从给定位置开始的码点。

int offsetByCodePoints(int startIndex，int cpCount) 5.0 返回从 startIndex 代码点开始，位移 cpCount 后的码点索引。

int compareTo(String other) 按照字典顺序，如果字符串位于 other 之前，返回一个负数；如果字符串位于 other 之后，返回一个正数；如果两个字符串相等，返回 0。

IntStream codePoints() 8 将这个字符串的码点作为一个流返回。调用 toArray 将它们放在一个数组中。

new String(int[]codePoints，int offset，int count) 5.0 用数组中从 offset 开始的 count 个码点构造一个字符串。

boolean equals(Object other) 如果字符串与 other 相等，返回 true。

boolean equalsIgnoreCase(String other) 如果字符串与 other 相等（忽略大小写），返回 true。

boolean startsWith(String prefix)

boolean endsWith(String suffix)

如果字符串以 suffix 开头或结尾，则返回 true。

int index0f(String str)

int index0f(String str，int fromIndex)

int index0f(int cp)

int index0f(int cp，int fromIndex)

返回与字符串 str 或代码点 cp 匹配的第一个子串的开始位置。这个位置从索引 0 或 fromIndex 开始计算。如果在原始串中不存在 str，返回 -1。

int lastIndex0f(String str)

int lastIndex0f(String str，int fromIndex)

int lastindex0f(int cp)

int lastindex0f(int cp，int fromIndex)

返回与字符串 str 或代码点 cp 匹配的最后一个子串的开始位置。这个位置从原始串尾端或 fromIndex 开始计算。

int length() 返回字符串的长度。

int codePointCount(int startIndex，int endIndex) 5.0 返回 startIndex 和 endIndex-1 之间的代码点数量。没有配成对的代用字符将计入代码点。

String replace(CharSequence oldString，CharSequence newString) 返回一个新字符串。这个字符串用 newString 代替原始字符串中所有的 oldString。可以用 String 或 StringBuilder 对象作为 CharSequence 参数。

String substring(int beginIndex)

String substring(int beginIndex，int endIndex)

返回一个新字符串。这个字符串包含原始字符串中从 beginIndex 到串尾或 endIndex–1 的所有代码单元。

String toLowerCase()

String toUpperCase()

返回一个新字符串。这个字符串将原始字符串中的大写字母改为小写，或者将原始字符串中的所有小写字母改成了大写字母。

String trim() 返回一个新字符串。这个字符串将删除了原始字符串头部和尾部的空格。

String join(CharSequence delimiter，CharSequence...elements）8

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

Tip: If you have not already done so, download the JDK documentation, as described in Chapter 2. Bookmark the jdk-9-docs/index.html page in your browser right now.

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

Note: The StringBuilder class was introduced in Java 5. Its predecessor, StringBuffer, is slightly less efficient, but it allows multiple threads to add or remove characters. If all string editing happens in a single thread (which is usually the case), you should use StringBuilder instead. The APIs of both classes are identical.

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

StringBuilder() 构造一个空的字符串构建器。

int length() 返回构建器或缓冲器中的代码单元数量。

StringBuilder append(String str) 追加一个字符串并返回 this。

StringBuilder append(char c) 追加一个代码单元并返回 this。

StringBuilder appendCodePoint(int cp) 追加一个代码点，并将其转换为一个或两个代码单元并返回 this。

void setCharAt(int i，char c) 将第 i 个代码单元设置为 c。

StringBuilder insert(int offset，String str) 在 offset 位置插入一个字符串并返回 this。

StringBuilder insert(int offset，Char c) 在 offset 位置插入一个代码单元并返回 this。

StringBuilder delete(int startIndex，int endIndex) 删除偏移量从 startIndex 到 - endIndex-1 的代码单元并返回 this。

·String toString() 返回一个与构建器或缓冲器内容相同的字符串。

### 3.7 Input and Output

To make our example programs more interesting, we want to accept input and properly format the program output. Of course, modern programs use a GUI for collecting user input. However, programming such an interface requires more tools and techniques than we have at our disposal at this time. Our first order of business is to become more familiar with the Java programming language, so we use the humble console for input and output.

3.7 输入输出

为了增加后面示例程序的趣味性，需要程序能够接收输入，并以适当的格式输出。当然，现代的程序都使用 GUI 收集用户的输入，然而，编写这种界面的程序需要使用较多的工具与技术，目前还不具备这些条件。主要原因是需要熟悉 Java 程序设计语言，因此只要有简单的用于输入输出的控制台就可以了。第 10-12 章将详细地介绍 GUI 程序设计。

#### 3.7.1 Reading Input

You saw that it is easy to print output to the「standard output stream」(that is, the console window) just by calling System.out.println. Reading from the「standard input stream」System.in isn't quite as simple. To read console input, you first construct a Scanner that is attached to System.in:

```java
Scanner in = new Scanner(System.in);
```

(We discuss constructors and the new operator in detail in Chapter 4.) Now you can use the various methods of the Scanner class to read input. For example, the nextLine method reads a line of input.

```java
System.out.print("What is your name? ");
String name = in.nextLine();
```

Here, we use the nextLine method because the input might contain spaces. To read a single word (delimited by whitespace), call

```java
String firstName = in.next();
```

To read an integer, use the nextInt method.

```java
System.out.print("How old are you? ");
int age = in.nextInt();
```

Similarly, the nextDouble method reads the next floating-point number.

The program in Listing 3.2 asks for the user's name and age and then prints a message like

Hello, Cay. Next year, you'll be 57

Finally, note the line

```java
import java.util.*;
```

at the beginning of the program. The Scanner class is defined in the java.util package. Whenever you use a class that is not defined in the basic java.lang package, you need to use an import directive. We look at packages and import directives in more detail in Chapter 4.

Listing 3.2 InputTest/InputTest.java

```java
import java.util.*;
/**
 * This program demonstrates console input.
 * @version 1.10 2004-02-10
 * @author Cay Horstmann
 */

public class InputTest

{
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);
        // get first input
        System.out.print("What is your name? ");
        String name = in.nextLine();

        // get second input
        System.out.print("How old are you? ");
        int age = in.nextInt();

        // display output on console
        System.out.println("Hello, " + name + ". Next year, you'll be " + (age + 1));
    }

}
```

Note: The Scanner class is not suitable for reading a password from a console since the input is plainly visible to anyone. Java 6 introduces a Console class specifically for this purpose. To read a password, use the following code:

```java
Console cons = System.console();

String username = cons.readLine("User name: ");

char[] passwd = cons.readPassword("Password: ");
```

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

在这里，使用 nextLine 方法是因为在输入行中有可能包含空格。要想读取一个单词（以空白符作为分隔符），就调用：

要想读取一个整数，就调用 nextInt 方法。

与此类似，要想读取下一个浮点数，就调用 nextDouble 方法。在程序清单 3-2 的程序中，询问用户姓名和年龄，然后打印一条如下格式的消息：

最后，在程序的最开始添加上一行：

Scanner 类定义在 java.util 包中。当使用的类不是定义在基本 java.lang 包中时，一定要使用 import 指示字将相应的包加载进来。有关包与 import 指示字的详细描述请参看第 4 章。

程序清单 3-2 InputTest/InputTest.java

注释：因为输入是可见的，所以 Scanner 类不适用于从控制台读取密码。Java SE 6 特别引入了 Console 类实现这个目的。要想读取一个密码，可以采用下列代码：

为了安全起见，返回的密码存放在一维字符数组中，而不是字符串中。在对密码进行处理之后，应该马上用一个填充值覆盖数组元素（数组处理将在 3.10 节介绍）。

采用 Console 对象处理输入不如采用 Scanner 方便。每次只能读取一行输入，而没有能够读取一个单词或一个数值的方法。

java.util.Scanner 5.0

Scanner(InputStream in) 用给定的输入流创建一个 Scanner 对象。

String nextLine() 读取输入的下一行内容。

String next() 读取输入的下一个单词（以空格作为分隔符）。

int nextInt()

double nextDouble()

读取并转换下一个表示整数或浮点数的字符序列。

boolean hasNext() 检测输入中是否还有其他单词。

boolean hasNextInt()

boolean hasNextDouble()

检测是否还有表示整数或浮点数的下一个字符序列。

java.lang.System 1.0

static Console console() 6

如果有可能进行交互操作，就通过控制台窗口为交互的用户返回一个 Console 对象，否则返回 null。对于任何一个通过控制台窗口启动的程序，都可使用 Console 对象。否则，其可用性将与所使用的系统有关。

java.io.Console 6

static char[]readPassword(String prompt，Object...args)

static String readLine(String prompt，Object...args)

显示字符串 prompt 并且读取用户输入，直到输入行结束。args 参数可以用来提供输入格式。有关这部分内容将在下一节中介绍。

#### 3.7.2 Formatting Output

You can print a number x to the console with the statement System.out.print(x). That command will print x with the maximum number of nonzero digits for that type. For example,

```java
double x = 10000.0 / 3.0;
System.out.print(x);
```

prints

3333.3333333333335

That is a problem if you want to display, for example, dollars and cents.

In early versions of Java, formatting numbers was a bit of a hassle. Fortunately, Java 5 brought back the venerable printf method from the C library. For example, the call

```java
System.out.printf("%8.2f", x);
```

prints x with a field width of 8 characters and a precision of 2 characters. That is, the printout contains a leading space and the seven characters

3333.33

You can supply multiple parameters to printf. For example:

```java
System.out.printf("Hello, %s. Next year, you'll be %d", name, age);
```

Each of the format specifiers that start with a % character is replaced with the corresponding argument. The conversion character that ends a format specifier indicates the type of the value to be formatted: f is a floating-point number, s a string, and d a decimal integer. Table 3.5 shows all conversion characters.

Table 3.5 Conversions for printf

| Conversion Character | Type | Example |
| --- | --- | --- |
| d | Decimal integer | 159 |
| x | Hexadecimal integer | 9f |
| o | Octal integer | 237 |
| f | Fixed-point floating-point | 15.9 |
| e | Exponential floating-point | 1.59e+01 |
| g | General floating-point (the shorter of e and f) | — |
| a | Hexadecimal floating-point | 0x1.fccdp3 |
| s | String | Hello |
| c | Character | H |
| b | boolean | true |
| h | Hash code | 42628b2 |
| tx or Tx | Date and time (T forces uppercase) | Obsolete, use the java.time classes instead—see Chapter 6 of Volume II |
| % | The percent symbol | % |
| n | The platform-dependent line separator | — |

In addition, you can specify flags that control the appearance of the formatted output. Table 3.6 shows all flags. For example, the comma flag adds group separators. That is,

Table 3.6 Flags for printf

| Flag | Purpose | Example |
| --- | --- | --- |
| + | Prints sign for positive and negative numbers. | +3333.33 |
| space | Adds a space before positive numbers. | |
| 0 | Adds leading zeroes. | 003333.33 |
| - | Left-justifies field. | - |
| ( | Encloses negative numbers in parentheses. | (3333.33) |
| , | Adds group separators. | 3,333.33 |
| # (for f format) | Always includes a decimal point. | 3,333. |
| # (for x or o format) | Adds 0x or 0 prefix. | 0xcafe |
| $ | Specifies the index of the argument to be formatted; for example, %1$d %1$x prints the first argument in decimal and hexadecimal. | 159 9F |
| < | Formats the same value as the previous specification; for example, %d %<x prints the same number in decimal and hexadecimal. | 159 9F |

```java
System.out.printf("%,.2f", 10000.0 / 3.0);
```

prints

3,333.33

You can use multiple flags, for example "%,(.2f" to use group separators and enclose negative numbers in parentheses.

Note: You can use the s conversion to format arbitrary objects. If an arbitrary object implements the Formattable interface, the object's formatTo method is invoked. Otherwise, the toString method is invoked to turn the object into a string. We discuss the toString method in Chapter 5 and interfaces in Chapter 6.

You can use the static String.format method to create a formatted string without printing it:

```java
String message = String.format("Hello, %s. Next year, you'll be %d", name, age);
```

In the interest of completeness, we briefly discuss the date and time formatting options of the printf method. For new code, you should use the methods of the java.time package described in Chapter 6 of Volume II. But you may encounter the Date class and the associated formatting options in legacy code. The format consists of two letters, starting with t and ending in one of the letters of Table 3.7; for example,

Table 3.7 Date and Time Conversion Characters

```java
System.out.printf("%tc", new Date());
```

prints the current date and time in the format

Mon Feb 09 18:05:19 PST 2015

As you can see in Table 3.7, some of the formats yield only a part of a given date—for example, just the day or just the month. It would be a bit silly if you had to supply the date multiple times to format each part. For that reason, a format string can indicate the index of the argument to be formatted. The index must immediately follow the %, and it must be terminated by a $. For example,

```java
System.out.printf("%1$s %2$tB %2$te, %2$tY", "Due date:", new Date());
```

prints

Due date: February 9, 2015

Alternatively, you can use the < flag. It indicates that the same argument as in the preceding format specification should be used again. That is, the statement

```java
System.out.printf("%s %tB %<te, %<tY", "Due date:", new Date());
```

yields the same output as the preceding statement.

Caution: Argument index values start with 1, not with 0: %1$. . . formats the first argument. This avoids confusion with the 0 flag.

You have now seen all features of the printf method. Figure 3.6 shows a syntax diagram for format specifiers.

Figure 3.6 Format specifier syntax

Note: The formatting of numbers and dates is locale-specific. For example, in Germany, the group separator is a period, not a comma, and Monday is formatted as Montag. Chapter 7 of Volume II shows how to control the international behavior of your applications.

3.7.2 格式化输出

可以使用 System.out.print(x) 将数值 x 输出到控制台上。这条命令将以 x 对应的数据类型所允许的最大非 0 数字位数打印输出 x。例如：

如果希望显示美元、美分等符号，则有可能会出现问题。在早期的 Java 版本中，格式化数值曾引起过一些争议。庆幸的是，Java SE5.0 沿用了 C 语言库函数中的 printf 方法。例如，调用 可以用 8 个字符的宽度和小数点后两个字符的精度打印 x。也就是说，打印输出一个空格和 7 个字符，如下所示：

在 printf 中，可以使用多个参数，例如：

每一个以 % 字符开始的格式说明符都用相应的参数替换。格式说明符尾部的转换符将指示被格式化的数值类型：f 表示浮点数，s 表示字符串，d 表示十进制整数。表 3-5 列出了所有转换符。

表 3-5 用于 printf 的转换符

另外，还可以给出控制格式化输出的各种标志。表 3-6 列出了所有的标志。例如，逗号标志增加了分组的分隔符。即表 3-6 用于 printf 的标志：

可以使用多个标志，例如，「%，（.2f」使用分组的分隔符并将负数括在括号内。

注释：可以使用 s 转换符格式化任意的对象。对于任意实现了 Formattable 接口的对象都将调用 formatTo 方法；否则将调用 toString 方法，它可以将对象转换为字符串。在第 5 章中将讨论 toString 方法，在第 6 章中将讨论接口。

可以使用静态的 String.format 方法创建一个格式化的字符串，而不打印输出：

基于完整性的考虑，下面简略地介绍 printf 方法中日期与时间的格式化选项。在新代码中，应当使用卷 Ⅱ 第 6 章中介绍的 java.time 包的方法。不过你可能会在遗留代码中看到 Date 类和相关的格式化选项。格式包括两个字母，以 t 开始，以表 3-7 中的任意字母结束。例如，

这条语句将用下面的格式打印当前的日期和时间：

从表 3-7 可以看到，某些格式只给出了指定日期的部分信息。例如，只有日期或月份。如果需要多次对日期操作才能实现对每一部分进行格式化的目的就太笨拙了。为此，可以采用一个格式化的字符串指出要被格式化的参数索引。索引必须紧跟在 % 后面，并以 $ 终止。例如，

表 3-7 日期和时间的转换符

还可以选择使用 < 标志。它指示前面格式说明中的参数将被再次使用。也就是说，下列语句将产生与前面语句同样的输出结果：

提示：参数索引值从 1 开始，而不是从 0 开始，%1$... 对第 1 个参数格式化。这就避免了与 0 标志混淆。现在，已经了解了 printf 方法的所有特性。图 3-6 给出了格式说明符的语法图。

图 3-6 格式说明符语法

注释：许多格式化规则是本地环境特有的。例如，在德国，组分隔符是句号而不是逗号，Monday 被格式化为 Montag。在卷 Ⅱ 第 5 章中将介绍如何控制应用的国际化行为。

#### 3.7.3 File Input and Output

To read from a file, construct a Scanner object like this:

```java
Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8);
```

If the file name contains backslashes, remember to escape each of them with an additional backslash: "c:\\mydirectory\\myfile.txt".

Note: Here, we specify the UTF-8 character encoding, which is common (but not universal) for files on the Internet. You need to know the character encoding when you read a text file (see Volume II, Chapter 2 for more information). If you omit the character encoding, then the「default encoding」of the computer running the Java program is used. That is not a good idea—the program might act differently depending on where it is run.

Now you can read from the file, using any of the Scanner methods that we already described.

To write to a file, construct a PrintWriter object. In the constructor, supply the file name and the character encoding:

```java
PrintWriter out = new PrintWriter("myfile.txt", StandardCharsets.UTF_8);
```

If the file does not exist, it is created. You can use the print, println, and printf commands as you did when printing to System.out.

Caution: You can construct a Scanner with a string parameter, but the scanner interprets the string as data, not a file name. For example, if you call

```java
Scanner in = new Scanner("myfile.txt"); // ERROR?
```

then the scanner will see ten characters of data: 'm', 'y', 'f', and so on. That is probably not what was intended in this case.

Note: When you specify a relative file name, such as "myfile.txt", "mydirectory/myfile.txt", or "../myfile.txt", the file is located relative to the directory in which the Java virtual machine was started. If you launched your program from a command shell, by executing

java MyProg

then the starting directory is the current directory of the command shell. However, if you use an integrated development environment, it controls the starting directory. You can find the directory location with this call:

```java
String dir = System.getProperty("user.dir");
```

If you run into grief with locating files, consider using absolute path names such as "c:\\mydirectory\\myfile.txt" or "/home/me/mydirectory/myfile.txt".

As you saw, you can access files just as easily as you can use System.in and System.out. There is just one catch: If you construct a Scanner with a file that does not exist or a PrintWriter with a file name that cannot be created, an exception occurs. The Java compiler considers these exceptions to be more serious than a「divide by zero」exception, for example. In Chapter 7, you will learn various ways of handling exceptions. For now, you should simply tell the compiler that you are aware of the possibility of an「input/output」exception. You do this by tagging the main method with a throws clause, like this:

```java
public static void main(String[] args) throws IOException

{
    Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8);
    . . .
}
```

You have now seen how to read and write files that contain textual data. For more advanced topics, such as dealing with different character encodings, processing binary data, reading directories, and writing zip files, turn to Chapter 2 of Volume II.

Note: When you launch a program from a command shell, you can use the redirection syntax of your shell and attach any file to System.in and System.out:

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

```java
Scanner in = new Scanner(Path.of("myfile.txt"), StandardCharsets.UTF_8);
```

如果文件名中包含反斜杠符号，就要记住在每个反斜杠之前再加一个额外的反斜杠：`c：\\mydirectory\\myfile.txt`。

注释：在这里指定了 UTF-8 字符编码，这对于互联网上的文件很常见（不过并不是普遍适用）。读取一个文本文件时，要知道它的字符编码 —— 更多信息参见卷 Ⅱ 第 2 章。如果省略字符编码，则会使用运行这个 Java 程序的机器的「默认编码」。这不是一个好主意，如果在不同的机器上运行这个程序，可能会有不同的表现。

现在，就可以利用前面介绍的任何一个 Scanner 方法对文件进行读取。要想写入文件，就需要构造一个 PrintWriter 对象。在构造器中，只需要提供文件名：

```java
PrintWriter out = new PrintWriter("myfile.txt", StandardCharsets.UTF_8);
```

如果文件不存在，创建该文件。可以像输出到 System.out 一样使用 print、println 以及 printf 命令。

警告：可以构造一个带有字符串参数的 Scanner，但这个 Scanner 将字符串解释为数据，而不是文件名。例如，如果调用：

这个 scanner 会将参数作为包含 10 个字符的数据：‘m'，‘y'，‘f' 等。在这个示例中所显示的并不是人们所期望的效果。

注释：当指定一个相对文件名时，例如，「myfile.txt」，「mydirectory/myfile.txt」或「../myfile.txt」，文件位于 Java 虚拟机启动路径的相对位置。如果在命令行方式下用下列命令启动程序：

启动路径就是命令解释器的当前路径。然而，如果使用集成开发环境，那么启动路径将由 IDE 控制。可以使用下面的调用方式找到路径的位置：

如果觉得定位文件比较烦恼，则可以考虑使用绝对路径，例如：「c:\\mydirectory\\myfile.txt」或者「/home/me/mydirectory/myfile.txt」。

正如读者所看到的，访问文件与使用 System.in 和 System.out 一样容易。要记住一点：如果用一个不存在的文件构造一个 Scanner，或者用一个不能被创建的文件名构造一个 PrintWriter，那么就会发生异常。Java 编译器认为这些异常比「被零除」异常更严重。在第 7 章中，将会学习各种处理异常的方式。现在，应该告知编译器：已经知道有可能出现「输入 / 输出」异常。这需要在 main 方法中用 throws 子句标记，如下所示：

现在读者已经学习了如何读写包含文本数据的文件。对于更加高级的技术，例如，处理不同的字符编码、处理二进制数据、读取目录以及写压缩文件，请参看卷 Ⅱ 第 2 章。

注释：当采用命令行方式启动一个程序时，可以利用 Shell 的重定向语法将任意文件关联到 System.in 和 System.out：

这样，就不必担心处理 IOException 异常了。

java.util.Scanner 5.0

Scanner(File f) 构造一个从给定文件读取数据的 Scanner。

Scanner(String data) 构造一个从给定字符串读取数据的 Scanner。

构造一个从给定字符串读取数据的 Scanner。

java.io.PrintWriter 1.1

PrintWriter(String fileName) 构造一个将数据写入文件的 PrintWriter。文件名由参数指定。

java.nio.file.Paths 7

static Path get(String pathname) 根据给定的路径名构造一个 Path。
