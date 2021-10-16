### 3.8 Control Flow

Java, like any programming language, supports both conditional statements and loops to determine control flow. We will start with the conditional statements, then move on to loops, to end with the somewhat cumbersome switch statement that you can use to test for many values of a single expression.

C++ Note: The Java control flow constructs are identical to those in C and C++, with a few exceptions. There is no goto, but there is a「labeled」version of break that you can use to break out of a nested loop (where, in C, you perhaps would have used a goto). Finally, there is a variant of the for loop that is similar to the range-based for loop in C++ and the foreach loop in C#.

3.8 控制流程

与任何程序设计语言一样，Java 使用条件语句和循环结构确定控制流程。本节先讨论条件语句，然后讨论循环语句，最后介绍看似有些笨重的 switch 语句，当需要对某个表达式的多个值进行检测时，可以使用 switch 语句。

C++ 注释：Java 的控制流程结构与 C 和 C++ 的控制流程结构一样，只有很少的例外情况。没有 goto 语句，但 break 语句可以带标签，可以利用它实现从内层循环跳出的目的（这种情况 C 语言采用 goto 语句实现）。另外，还有一种变形的 for 循环，在 C 或 C++ 中没有这类循环。它有点类似于 C# 中的 foreach 循环。

#### 3.8.1 Block Scope

Before learning about control structures, you need to know more about blocks.

A block, or compound statement, consists of a number of Java statements, surrounded by a pair of braces. Blocks define the scope of your variables. A block can be nested inside another block. Here is a block that is nested inside the block of the main method:

```java
public static void main(String[] args)
{
    int n;
    . . .
    {
        int k;
        . . .
    } // k is only defined up to here
}
```

You may not declare identically named variables in two nested blocks. For example, the following is an error and will not compile:

```java
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
```

C++ Note: In C++, it is possible to redefine a variable inside a nested block. The inner definition then shadows the outer one. This can be a source of programming errors; hence, Java does not allow it.

3.8.1 块作用域

在深入学习控制结构之前，需要了解块（block）的概念。块（即复合语句）是指由一对大括号括起来的若干条简单的 Java 语句。块确定了变量的作用域。一个块可以嵌套在另一个块中。下面就是在 main 方法块中嵌套另一个语句块的示例。

但是，不能在嵌套的两个块中声明同名的变量。例如，下面的代码就有错误，而无法通过编译：

C++ 注释：在 C++ 中，可以在嵌套的块中重定义一个变量。在内层定义的变量会覆盖在外层定义的变量。这样，有可能会导致程序设计错误，因此在 Java 中不允许这样做。

#### 3.8.2 Conditional Statements

The conditional statement in Java has the form

if (condition) statement

The condition must be surrounded by parentheses.

In Java, as in most programming languages, you will often want to execute multiple statements when a single condition is true. In this case, use a block statement that takes the form

```java
{
    statement1

    statement2

    . . .
}
```

For example:

```java
if (yourSales >= target)
{
  performance = "Satisfactory";
  bonus = 100;
}
```

In this code all the statements surrounded by the braces will be executed when yourSales is greater than or equal to target (see Figure 3.7).

Figure 3.7 Flowchart for the if statement

Note: A block (sometimes called a compound statement) enables you to have more than one (simple) statement in any Java programming structure that otherwise allows for a single (simple) statement.

The more general conditional in Java looks like this (see Figure 3.8):

Figure 3.8 Flowchart for the if/else statement

if (condition) statement1 else statement2

For example:

```java
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
```

The else part is always optional. An else groups with the closest if. Thus, in the statement

```java
if (x <= 0) if (x == 0) sign = 0; else sign = -1;
```

the else belongs to the second if. Of course, it is a good idea to use braces to clarify this code:

```java
if (x <= 0) { if (x == 0) sign = 0; else sign = -1; }
```

Repeated if . . . else if . . . alternatives are common (see Figure 3.9). For example:

Figure 3.9 Flowchart for the if/else if (multiple branches)

```java
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
```

3.8.2 条件语句

在 Java 中，条件语句的格式为：

这里的条件必须用括号括起来。与绝大多数程序设计语言一样，Java 常常希望在某个条件为真时执行多条语句。在这种情况下，应该使用块语句（block statement），形式为：

例如：

当 yourSales 大于或等于 target 时，将执行括号中的所有语句（请参看图 3-7）。

图 3-7 if 语句的流程图

注释：使用块（有时称为复合语句）可以在 Java 程序结构中原本只能放置一条（简单）语句的地方放置多条语句。

在 Java 中，更一般的条件语句格式如下所示（请参看图 3-8）：

图 3-8 if/else 语句的流程图

例如：

其中 else 部分是可选的。else 子句与最邻近的 if 构成一组。因此，在语句中 else 与第 2 个 if 配对。当然，用一对括号将会使这段代码更加清晰：

重复地交替出现 if...else if... 是一种很常见的情况（请参看图 3-9）。例如：

图 3-9 if/else if（多分支）的流程图

#### 3.8.3 Loops

The while loop executes a statement (which may be a block statement) while a condition is true. The general form is:

while (condition) statement

The while loop will never execute if the condition is false at the outset (see Figure 3.10).

Figure 3.10 Flowchart for the while statement

The program in Listing 3.3 determines how long it will take to save a specific amount of money for your well-earned retirement, assuming you deposit the same amount of money per year and the money earns a specified interest rate.

In the example, we are incrementing a counter and updating the amount currently accumulated in the body of the loop until the total exceeds the targeted amount.

```java
while (balance < goal)
{
  balance += payment;
  double interest = balance * interestRate / 100;
  balance += interest;
  years++;
}
System.out.println(years + " years.");
```

(Don't rely on this program to plan for your retirement. We left out a few niceties such as inflation and your life expectancy.)

A while loop tests at the top. Therefore, the code in the block might never be executed. If you want to make sure a block is executed at least once, you need to move the test to the bottom, using the do/while loop. Its syntax looks like this:

do statement while (condition);

This loop executes the statement (which is typically a block) and only then tests the condition. If it's true, it repeats the statement and retests the condition, and so on. The code in Listing 3.4 computes the new balance in your retirement account and then asks if you are ready to retire:

```java
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
```

As long as the user answers "N", the loop is repeated (see Figure 3.11). This program is a good example of a loop that needs to be entered at least once, because the user needs to see the balance before deciding whether it is sufficient for retirement.

Figure 3.11 Flowchart for the do/while statement

Listing 3.3 Retirement/Retirement.java

```java
import java.util.*;

/**
* This program demonstrates a while loop.
* @version 1.20 2004-02-10
* @author Cay Horstmann
*/

public class Retirement
{
    public static void main(String[] args)
    {
        // read inputs
        Scanner in = new Scanner(System.in);
        System.out.print("How much money do you need to retire? ");
        double goal = in.nextDouble();
        System.out.print("How much money will you contribute every year? ");
        double payment = in.nextDouble();
        System.out.print("Interest rate in %: ");
        double interestRate = in.nextDouble();
        double balance = 0;
        int years = 0;

        // update account balance while goal isn't reached
        while (balance > goal)
        {
            // add this year's payment and interest
            balance += payment;
            double interest = balance * interestRate / 100;
            balance += interest;
            years++;
        }
        System.out.println("You can retire in " + years + " years.");
    }
}
```

Listing 3.4 Retirement2/Retirement2.java

```java
import java.util.*;

/**
* This program demonstrates a do/while loop.
* @version 1.20 2004-02-10
* @author Cay Horstmann
*/

public class Retirement2
{
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);
        System.out.print("How much money will you contribute every year? ");
        double payment = in.nextDouble();
        System.out.print("Interest rate in %: ");
        double interestRate = in.nextDouble();
        double balance = 0;
        int year = 0;
        String input;

        // update account balance while user isn't ready to retire
        do
        {
            // add this year's payment and interest
            balance += payment;
            double interest = balance * interestRate / 100;
            balance += interest;
            year++;

            // print current balance
            System.out.printf("After year %d, your balance is %,.2f%n", year, balance);
            // ask if ready to retire and get input
            System.out.print("Ready to retire? (Y/N) ");
            input = in.next();
        }

        while (input.equals("N"));
    }
}
```

3.8.3 循环

当条件为 true 时，while 循环执行一条语句（也可以是一个语句块）。一般格式为：

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

```java
for (int i = 1; i <= 10; i++)
    System.out.println(i);
```

The first slot of the for statement usually holds the counter initialization. The second slot gives the condition that will be tested before each new pass through the loop, and the third slot specifies how to update the counter.

Although Java, like C++, allows almost any expression in the various slots of a for loop, it is an unwritten rule of good taste that the three slots should only initialize, test, and update the same counter variable. One can write very obscure loops by disregarding this rule.

Even within the bounds of good taste, much is possible. For example, you can have loops that count down:

```java
for (int i = 10; i > 0; i--)
    System.out.println("Counting down . . . " + i);
System.out.println("Blastoff!");
```

Caution: Be careful with testing for equality of floating-point numbers in loops. A for loop like this one


for (double x = 0; x != 10; x += 0.1) . . .

might never end. Because of roundoff errors, the final value might not be reached exactly. In this example, x jumps from 9.99999999999998 to 10.09999999999998 because there is no exact binary representation for 0.1.

When you declare a variable in the first slot of the for statement, the scope of that variable extends until the end of the body of the for loop.

```java
for (int i = 1; i <= 10; i++)
{
    . . .
}
// i no longer defined here
```

In particular, if you define a variable inside a for statement, you cannot use its value outside the loop. Therefore, if you wish to use the final value of a loop counter outside the for loop, be sure to declare it outside the loop header.

```java
int i;
for (i = 1; i <= 10; i++)
{
    . . .
}
// i is still defined here
```

On the other hand, you can define variables with the same name in separate for loops:

```java
for (int i = 1; i <= 10; i++)
{
    . . .
}
. . .
for (int i = 11; i <= 20; i++) // OK to define another variable named i
{
    . . .
}
```

A for loop is merely a convenient shortcut for a while loop. For example,

```java
for (int i = 10; i > 0; i--)
    System.out.println("Counting down . . . " + i);
```

can be rewritten as

```java
int i = 10;
while (i > 0)
{
    System.out.println("Counting down . . . " + i);
    i--;
}
```

Listing 3.5 shows a typical example of a for loop.

The program computes the odds of winning a lottery. For example, if you must pick six numbers from the numbers 1 to 50 to win, then there are (50 × 49 × 48 × 47 × 46 × 45)/(1 × 2 × 3 × 4 × 5 × 6) possible outcomes, so your chance is 1 in 15,890,700. Good luck!

In general, if you pick k numbers out of n, there are

possible outcomes. The following for loop computes this value:

```java
int lotteryOdds = 1;
for (int i = 1; i <= k; i++)
    lotteryOdds = lotteryOdds * (n - i + 1) / i;
```

Note: See Section 3.10.3,「The ‘for each' Loop,」on p. 110 for a description of the「generalized for loop」(also called「for each」loop) that was added to the Java language in Java 5.

Listing 3.5 LotteryOdds/LotteryOdds.java

```java
import java.util.*;

/**
* This program demonstrates a for loop.
* @version 1.20 2004-02-10
* @author Cay Horstmann
*/

public class LotteryOdds
{
    public static void main(String[] args)
    {
        Scanner in = new Scanner(System.in);
        System.out.print("How many numbers do you need to draw? ");
        int k = in.nextInt();
        System.out.print("What is the highest number you can draw? ");
        int n = in.nextInt();
        /*
         * compute binomial coefficient n*(n-1)*(n-2)*...*(n-k+1)/(1*2*3*...*k)
         */
        int lotteryOdds = 1;
        for (int i = 1; i <= k; i++)
            lotteryOdds = lotteryOdds * (n - i + 1) / i;
        System.out.println("Your odds are 1 in " + lotteryOdds + ". Good luck!");
    }
}
```

3.8.4 确定循环

for 循环语句是支持迭代的一种通用结构，利用每次迭代之后更新的计数器或类似的变量来控制迭代次数。如图 3-12 所示，下面的程序将数字 1~10 输出到屏幕上。

图 3-11 do/while 语句的流程图

图 3-12 for 语句的流程图

for 语句的第 1 部分通常用于对计数器初始化；第 2 部分给出每次新一轮循环执行前要检测的循环条件；第 3 部分指示如何更新计数器。

与 C++ 一样，尽管 Java 允许在 for 循环的各个部分放置任何表达式，但有一条不成文的规则：for 语句的 3 个部分应该对同一个计数器变量进行初始化、检测和更新。若不遵守这一规则，编写的循环常常晦涩难懂。

即使遵守了这条规则，也还有可能出现很多问题。例如，下面这个倒计数的循环：

警告：在循环中，检测两个浮点数是否相等需要格外小心。下面的 for 循环可能永远不会结束。由于舍入的误差，最终可能得不到精确值。例如，在上面的循环中，因为 0.1 无法精确地用二进制表示，所以，x 将从 9.99999999999998 跳到 10.09999999999998。当在 for 语句的第 1 部分中声明了一个变量之后，这个变量的作用域就为 for 循环的整个循环体。

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

```java
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
```

Execution starts at the case label that matches the value on which the selection is performed and continues until the next break or the end of the switch. If none of the case labels match, then the default clause is executed, if it is present.

Caution: It is possible for multiple alternatives to be triggered. If you forget to add a break at the end of an alternative, execution falls through to the next alternative! This behavior is plainly dangerous and a common cause for errors. For that reason, we never use the switch statement in our programs.

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
