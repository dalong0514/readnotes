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

维基百科链接：有的话。找一个他的 TED 演讲，有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是在这个专栏的整个地图里，这一章节所在的节点。

### 2. 摘录及评论

1『自己的观点』

2『行动指南』

3『与其他知识的连接』

## 安装

国外的一个 PHP 教程网站：[Setting Up Project with PHP and MySQL Database - Tutorial Republic](https://www.tutorialrepublic.com/php-tutorial/php-get-started.php)

[vscode-php-debug/README.md at master · felixfbecker/vscode-php-debug](https://github.com/felixfbecker/vscode-php-debug/blob/master/README.md)

发现 docker 上也可以配置 php 环境：[Docker 安装 PHP | 菜鸟教程](https://www.runoob.com/docker/docker-install-php.html)

1、官网下载：[Download XAMPP](https://www.apachefriends.org/download.html)

2、应该是电脑里配套比较全，ProFTPD、Apache、MYSQL 都有，全绿灯通过。在「Volumes」里要点挂起「Mount」，然后点 export 可以进入 htdocs 文件夹，代码「test.php」放进去即可。

/Users/Daglas/.bitnami/stackman/machines/xampp/volumes/root/htdocs

/Users/Daglas/.bitnami/stackman/machines/xampp/volumes/root/htdocs/dashboard/phpinfo

3、浏览器里输入地址：http://192.168.64.2/2020011w3school/test.php 即可运行文件。

## 0101. 基础教程

### 01. PHP 简介

PHP 脚本在服务器上执行。

您应当具备的基础知识。在继续学习之前，您需要对下面的知识有基本的了解：HTML、CSS 和 JavaScript。如果您希望首先学习这些项目，请在我们的首页访问这些教程。

什么是 PHP？1）PHP 是 "PHP Hypertext Preprocessor" 的首字母缩略词。2）PHP 是一种被广泛使用的开源脚本语言。3）PHP 脚本在服务器上执行。4）PHP 没有成本，可供免费下载和使用。

PHP 是一门令人惊叹的流行语言！1）它强大到足以成为在网络上最大的博客系统的核心（WordPress）！2）它深邃到足以运行最大的社交网络（facebook）！3）而它的易用程度足以成为初学者的首选服务器端语言！

什么是 PHP 文件？1）PHP 文件能够包含文本、HTML、CSS 以及 PHP 代码。2）PHP 代码在服务器上执行，而结果以纯文本返回浏览器。2）PHP 文件的后缀是 ".php"

PHP 能够做什么？1）PHP 能够生成动态页面内容。2）PHP 能够创建、打开、读取、写入、删除以及关闭服务器上的文件。3）PHP 能够接收表单数据。4）PHP 能够发送并取回 cookies。5）PHP 能够添加、删除、修改数据库中的数据。6）PHP 能够限制用户访问网站中的某些页面。7）PHP 能够对数据进行加密。

通过 PHP，您可以不受限于只输出 HTML。您还能够输出图像、PDF 文件、甚至 Flash 影片。您也可以输出任何文本，比如 XHTML 和 XML。

为什么使用 PHP？1）PHP 运行于各种平台（Windows, Linux, Unix, Mac OS X 等等）。2）PHP 兼容几乎所有服务器（Apache, IIS 等等）。3）PHP 支持多种数据库。4）PHP 是免费的。请从官方 PHP 资源下载：www.php.net。5）PHP 易于学习，并可高效地运行在服务器端。

### 02. PHP 安装

我需要什么？如需开始使用 PHP，您可以：1）使用支持 PHP 和 MySQL 的 web 主机。2）在您的 PC 上安装 web 服务器，然后安装 PHP 和 MySQL。

使用支持 PHP 的 Web 主机。如果您的服务器支持 PHP，那么您无需做任何事情。只要创建 .php 文件，然后上传到 web 目录中即可。服务器会自动对它们进行解析。您无需编译或安装任何额外的工具。因为 PHP 是免费的，大多数 web 主机都支持 PHP。

在您的 PC 上运行 PHP。不过如果您的服务器不支持 PHP，那么您必须：1）安装 web 服务器。2）安装 PHP。3）安装数据库，比如 MySQL。官方的 PHP 网站 (PHP.net) 提供了 PHP 的安装说明：http://php.net/manual/zh/install.php。

1『使用 IDE「XAMPP」。』

### 03. PHP 语法

PHP 脚本在服务器上执行，然后向浏览器发送回纯 HTML 结果。基础 PHP 语法。PHP 脚本可放置于文档中的任何位置。PHP 脚本以 \<?php 开头，以?> 结尾。PHP 文件的默认文件扩展名是 ".php"。PHP 文件通常包含 HTML 标签以及一些 PHP 脚本代码。下面的例子是一个简单的 PHP 文件，其中包含了使用内建 PHP 函数 "echo" 在网页上输出文本 "Hello World!" 的一段 PHP 脚本。注释：PHP 语句以分号结尾（;）。PHP 代码块的关闭标签也会自动表明分号（因此在 PHP 代码块的最后一行不必使用分号）。

PHP 中的注释。PHP 代码中的注释不会被作为程序来读取和执行。它唯一的作用是供代码编辑者阅读。注释用于：1）使其他人理解您正在做的工作 —— 注释可以让其他程序员了解您在每个步骤进行的工作（如果您供职于团队）。2）提醒自己做过什么 —— 大多数程序员都曾经历过一两年后对项目进行返工，然后不得不重新考虑他们做过的事情。注释可以记录您在写代码时的思路。PHP 支持三种注释：

```
<!DOCTYPE html>
<html>
<body>

<?php
// 这是单行注释

# 这也是单行注释

/*
这是多行注释块
它横跨了
多行
*/
?>

</body>
</html>
```

PHP 大小写敏感。在 PHP 中，所有用户定义的函数、类和关键词（例如 if、else、echo 等等）都对大小写不敏感。在下面的例子中，所有这三条 echo 语句都是合法的（等价）；不过在 PHP 中，所有变量都对大小写敏感。在下面的例子中，只有第一条语句会显示 \$color 变量的值（这是因为 \$color、\$COLOR 以及 \$coLOR 被视作三个不同的变量）。

### 04. PHP 变量

变量是存储信息的容器：

```
<?php
$x=5;
$y=6;
$z=$x+$y;
echo $z;
?>
```

类似代数。在代数中我们使用字母（比如 x）来保存值（比如 5）。从上面的表达式 z=x+y，我们能够计算出 z 的值是 11。在 PHP 中，这三个字母被称为变量。注释：请把变量视为存储数据的容器。

PHP 变量。正如代数，PHP 变量可用于保存值（x=5）和表达式（z=x+y）。变量的名称可以很短（比如 x 和 y），也可以取更具描述性的名称（比如 carname、total_volume）。PHP 变量规则：变量以 \$ 符号开头，其后是变量的名称，变量名称必须以字母或下划线开头，变量名称不能以数字开头，变量名称只能包含字母数字字符和下划线（A-z、0-9 以及 _），变量名称对大小写敏感（\$y 与 \$Y 是两个不同的变量）。

注释：PHP 变量名称对大小写敏感！

创建 PHP 变量。PHP 没有创建变量的命令。变量会在首次为其赋值时被创建：

2『动态语言呗。』

```
<?php
$txt="Hello world!";
$x=5;
$y=10.5;
?>
```

以上语句执行后，变量 txt 会保存值 Hello world!，变量 x 会保存值 5，变量 y 会保存值 10.5。

注释：如果您为变量赋的值是文本，请用引号包围该值。

PHP 是一门类型松散的语言。在上面的例子中，请注意我们不必告知 PHP 变量的数据类型。PHP 根据它的值，自动把变量转换为正确的数据类型。在诸如 C 和 C++ 以及 Java 之类的语言中，程序员必须在使用变量之前声明它的名称和类型。

PHP 变量作用域。在 PHP 中，可以在脚本的任意位置对变量进行声明。变量的作用域指的是变量能够被引用 / 使用的那部分脚本。PHP 有三种不同的变量作用域：1）local（局部）。2）global（全局）。3）static（静态）。

Local 和 Global 作用域。函数之外声明的变量拥有 Global 作用域，只能在函数以外进行访问。函数内部声明的变量拥有 LOCAL 作用域，只能在函数内部进行访问。下面的例子测试了带有局部和全局作用域的变量：

```
<?php
$x=5; // 全局作用域

function myTest() {
  $y=10; // 局部作用域
  echo "<p>测试函数内部的变量：</p>";
  echo "变量 x 是：$x";
  echo "<br>";
  echo "变量 y 是：$y";
} 

myTest();

echo "<p>测试函数之外的变量：</p>";
echo "变量 x 是：$x";
echo "<br>";
echo "变量 y 是：$y";
?>
```

在上例中，有两个变量 \$x 和 \$y，以及一个函数 myTest ()。\$x 是全局变量，因为它是在函数之外声明的，而 \$y 是局部变量，因为它是在函数内声明的。如果我们在 myTest () 函数内部输出两个变量的值，\$y 会输出在本地声明的值，但是无法输出 \$x 的值，因为它在函数之外创建。然后，如果在 myTest () 函数之外输出两个变量的值，那么会输出 \$x 的值，但是不会输出 \$y 的值，因为它是局部变量，并且在 myTest () 内部创建。

注释：您可以在不同的函数中创建名称相同的局部变量，因为局部变量只能被在其中创建它的函数识别。PHP global 关键词。global 关键词用于在函数内访问全局变量。要做到这一点，请在（函数内部）变量前面使用 global 关键词：

```
<?php
$x=5;
$y=10;

function myTest() {
  global $x,$y;
  $y=$x+$y;
}

myTest();
echo $y; // 输出 15
?>
```

PHP 同时在名为 \$GLOBALS [index] 的数组中存储了所有的全局变量。下标存有变量名。这个数组在函数内也可以访问，并能够用于直接更新全局变量。上面的例子可以这样重写：

```
<?php
$x=5;
$y=10;

function myTest() {
  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
} 

myTest();
echo $y; // 输出 15
?>
```

PHP static 关键词。通常，当函数完成 / 执行后，会删除所有变量。不过，有时我需要不删除某个局部变量。实现这一点需要更进一步的工作。要完成这一点，请在您首次声明变量时使用 static 关键词：

```
<?php

function myTest() {
  static $x=0;
  echo $x;
  $x++;
}

myTest();
myTest();
myTest();

?>
```

然后，每当函数被调用时，这个变量所存储的信息都是函数最后一次被调用时所包含的信息。注释：该变量仍然是函数的局部变量。

### 05. PHP 5 echo 和 print 语句

在 PHP 中，有两种基本的输出方法：echo 和 print。在本教程中，我们几乎在每个例子中都会用到 echo 和 print。因此，本节为您讲解更多关于这两条输出语句的知识。PHP echo 和 print 语句。echo 和 print 之间的差异：1）echo —— 能够输出一个以上的字符串；2）print —— 只能输出一个字符串，并始终返回 1。提示：echo 比 print 稍快，因为它不返回任何值。

PHP echo 语句。echo 是一个语言结构，有无括号均可使用：echo 或 echo ()。显示字符串。下面的例子展示如何用 echo 命令来显示不同的字符串（同时请注意字符串中能包含 HTML 标记）：

```
<?php
echo "<h2>PHP is fun!</h2>";
echo "Hello world!<br>";
echo "I'm about to learn PHP!<br>";
echo "This", " string", " was", " made", " with multiple parameters.";
?>
```

2『经验证，\<br> 是换行的标签。』

显示变量。下面的例子展示如何用 echo 命令来显示字符串和变量：

```
<?php
$txt1="Learn PHP";
$txt2="W3School.com.cn";
$cars=array("Volvo","BMW","SAAB");

echo $txt1;
echo "<br>";
echo "Study PHP at $txt2";
echo "My car is a {$cars[0]}";
?>
```

PHP print 语句。print 也是语言结构，有无括号均可使用：print 或 print ()。

显示字符串。下面的例子展示如何用 print 命令来显示不同的字符串（同时请注意字符串中能包含 HTML 标记）：

```
<?php
print "<h2>PHP is fun!</h2>";
print "Hello world!<br>";
print "I'm about to learn PHP!";
?>
```

显示变量。下面的例子展示如何用 print 命令来显示字符串和变量：

```
<?php
$txt1="Learn PHP";
$txt2="W3School.com.cn";
$cars=array("Volvo","BMW","SAAB");

print $txt1;
print "<br>";
print "Study PHP at $txt2";
print "My car is a {$cars[0]}";
?>
```

2『print 不能同时显示多个字符串。』

### 06. PHP 数据类型

字符串、整数、浮点数、逻辑、数组、对象、NULL。PHP 字符串。字符串是字符序列，比如 "Hello world!"。字符串可以是引号内的任何文本。您可以使用单引号或双引号：

```
<?php 
$x = "Hello world!";
echo $x;
echo "<br>"; 
$x = 'Hello world!';
echo $x;
?>
```

PHP 整数。整数是没有小数的数字。整数规则：1）整数必须有至少一个数字（0-9）。2）整数不能包含逗号或空格。3）整数不能有小数点。4）整数正负均可。5）可以用三种格式规定整数：十进制、十六进制（前缀是 0x）或八进制（前缀是 0）。在下面的例子中，我们将测试不同的数字。PHP var_dump () 会返回变量的数据类型和值：

```
<?php 
$x = 5985;
var_dump($x);
echo "<br>"; 
$x = -345; // 负数
var_dump($x);
echo "<br>"; 
$x = 0x8C; // 十六进制数
var_dump($x);
echo "<br>";
$x = 047; // 八进制数
var_dump($x);
?>
```

PHP 浮点数。浮点数是有小数点或指数形式的数字。在下面的例子中，我们将测试不同的数字。PHP var_dump () 会返回变量的数据类型和值：

```
<?php 
$x = 10.365;
var_dump($x);
echo "<br>"; 
$x = 2.4e3;
var_dump($x);
echo "<br>"; 
$x = 8E-5;
var_dump($x);
?>
```

PHP 逻辑。逻辑是 true 或 false。逻辑常用于条件测试。您将在本教程稍后的章节学到更多有关条件测试的知识。

```
$x=true;
$y=false;
```

PHP 数组。数组在一个变量中存储多个值。在下面的例子中，我们将测试不同的数组。PHP var_dump () 会返回变量的数据类型和值。您将在本教程稍后的章节学到更多有关数组的知识。

```
<?php 
$cars=array("Volvo","BMW","SAAB");
var_dump($cars);
?>
```

PHP 对象。对象是存储数据和有关如何处理数据的信息的数据类型。在 PHP 中，必须明确地声明对象。首先我们必须声明对象的类。对此，我们使用 class 关键词。类是包含属性和方法的结构。然后我们在对象类中定义数据类型，然后在该类的实例中使用此数据类型：

```
<?php
class Car
{
  var $color;
  function Car($color="green") {
    $this->color = $color;
  }
  function what_color() {
    return $this->color;
  }
}
?>
```

您将在本教程稍后的章节学到更多有关对象的知识。PHP NULL 值。特殊的 NULL 值表示变量无值。NULL 是数据类型 NULL 唯一可能的值。NULL 值标示变量是否为空。也用于区分空字符串与空值数据库。可以通过把值设置为 NULL，将变量清空：

```
<?php
$x="Hello world!";
$x=null;
var_dump($x);
?>
```
### 07. PHP 字符串函数

PHP 字符串函数。字符串是字符序列，比如 "Hello world!"。PHP 字符串函数。在本节中，我们将学习常用的字符串操作函数。PHP strlen () 函数。strlen () 函数返回字符串的长度，以字符计。下例返回字符串 "Hello world!" 的长度：

```
<?php
echo strlen("Hello world!");
?>
```

提示：strlen () 常用于循环和其他函数，在确定字符串何时结束很重要时。（例如，在循环中，我们也许需要在字符串的最后一个字符之后停止循环）。对字符串中的单词计数。PHP str_word_count () 函数对字符串中的单词进行计数：

```
<?php
echo str_word_count("Hello world!"); // 输出 2
?>
```

反转字符串。PHP strrev () 函数反转字符串：

```
<?php
echo strrev("Hello world!"); // 输出 !dlrow olleH
?>
```

PHP strpos () 函数。strpos () 函数用于检索字符串内指定的字符或文本。如果找到匹配，则会返回首个匹配的字符位置。如果未找到匹配，则将返回 FALSE。下例检索字符串 "Hello world!" 中的文本 "world"：

```
<?php
echo strpos("Hello world!","world");
?>
```

提示：上例中字符串 "world" 的位置是 6。是 6（而不是 7）的理由是，字符串中首字符的位置是 0 而不是 1。替换字符串中的文本。PHP str_replace () 函数用一些字符串替换字符串中的另一些字符。下面的例子用 "Kitty" 替换文本 "world"：

```
<?php
echo str_replace("world", "Kitty", "Hello world!"); // 输出 Hello Kitty!
?>
```

如需完整的字符串函数参考手册，请访问我们的 PHP String 参考手册。这个手册提供了每个函数的简要描述和实例：[PHP 5 String 函数](https://www.w3school.com.cn/php/php_ref_string.asp)。

### 08. PHP 常量

常量类似变量，但是常量一旦被定义就无法更改或撤销定义。常量是单个值的标识符（名称）。在脚本中无法改变该值。有效的常量名以字符或下划线开头（常量名称前面没有 \$ 符号）。注释：与变量不同，常量贯穿整个脚本是自动全局的。设置 PHP 常量。如需设置常量，请使用 define () 函数 - 它使用三个参数：1）首个参数定义常量的名称。2）第二个参数定义常量的值。3）可选的第三个参数规定常量名是否对大小写不敏感。默认是 false。

下例创建了一个对大小写敏感的常量，值为 "Welcome to W3School.com.cn!"：

```
<?php
define("GREETING", "Welcome to W3School.com.cn!");
echo GREETING;
?>
```

下例创建了一个对大小写不敏感的常量，值为 "Welcome to W3School.com.cn!"：

```
<?php
define("GREETING", "Welcome to W3School.com.cn!", true);
echo greeting;
?>
```

常量是全局的。常量是自动全局的，而且可以贯穿整个脚本使用。下面的例子在函数内使用了一个常量，即使它在函数外定义：

```
<?php
define("GREETING", "Welcome to W3School.com.cn!");

function myTest() {
    echo GREETING;
}
 
myTest();
?>
```

### 09. PHP 运算符

PHP 运算符。本节展示了可用于 PHP 脚本中的各种运算符。1）PHP 算数运算符。下例展示了使用不同算数运算符的不同结果；2）PHP 赋值运算符。PHP 赋值运算符用于向变量写值。PHP 中基础的赋值运算符是 "="。这意味着右侧赋值表达式会为左侧运算数设置值。下例展示了使用不同赋值运算符的不同结果；3）PHP 字符串运算符。下例展示了使用字符串运算符的结果；4）PHP 递增 / 递减运算符。下例展示了使用不同递增 / 递减运算符的不同结果；5）PHP 比较运算符。PHP 比较运算符用于比较两个值（数字或字符串）。下例展示了使用某些比较运算符的不同结果；6）PHP 逻辑运算符；7）PHP 数组运算符；8）PHP 数组运算符用于比较数组。下例展示了使用不同数组运算符的不同结果：

```
<?php
$x = array("a" => "apple", "b" => "banana"); 
$y = array("c" => "orange", "d" => "peach"); 
$z = $x + $y; // $x 与 $y 的联合
var_dump($z);
var_dump($x == $y);
var_dump($x === $y);
var_dump($x != $y);
var_dump($x <> $y);
var_dump($x !== $y);
?>
```

### 10. PHP if...else...elseif 语句

PHP if...else...elseif 语句。条件语句用于基于不同条件执行不同的动作。PHP 条件语句。在您编写代码时，经常会希望为不同的决定执行不同的动作。您可以在代码中使用条件语句来实现这一点。在 PHP 中，我们可以使用以下条件语句：1）if 语句 —— 如果指定条件为真，则执行代码；2）if...else 语句 —— 如果条件为 true，则执行代码；如果条件为 false，则执行另一端代码；3）if...elseif....else 语句 —— 根据两个以上的条件执行不同的代码块；4）switch 语句 —— 选择多个代码块之一来执行。

PHP —— if 语句。if 语句用于在指定条件为 true 时执行代码。

```
if (条件) {
  当条件为 true 时执行的代码;
}
```

PHP - if...else 语句。请使用 if....else 语句在条件为 true 时执行代码，在条件为 false 时执行另一段代码。

```
if (条件) {
  条件为 true 时执行的代码;
} else {
  条件为 false 时执行的代码;
}
```

PHP - if...elseif....else 语句。请使用 if....elseif...else 语句来根据两个以上的条件执行不同的代码。

```
if (条件) {
  条件为 true 时执行的代码;
} elseif (condition) {
  条件为 true 时执行的代码;
} else {
  条件为 false 时执行的代码;
}
```

### 11. PHP Switch 语句

PHP Switch 语句。switch 语句用于基于不同条件执行不同动作。如果您希望有选择地执行若干代码块之一，请使用 Switch 语句。使用 Switch 语句可以避免冗长的 if..elseif..else 代码块。

```
switch (expression)
{
case label1:
  expression = label1 时执行的代码 ;
  break;  
case label2:
  expression = label2 时执行的代码 ;
  break;
default:
  表达式的值不等于 label1 及 label2 时执行的代码;
}
```

工作原理：1）对表达式（通常是变量）进行一次计算；2）把表达式的值与结构中 case 的值进行比较；3）如果存在匹配，则执行与 case 关联的代码；4）代码执行后，break 语句阻止代码跳入下一个 case 中继续执行；5）如果没有 case 为真，则使用 default 语句。

```
<?php
$favfruit="orange";

switch ($favfruit) {
   case "apple":
     echo "Your favorite fruit is apple!";
     break;
   case "banana":
     echo "Your favorite fruit is banana!";
     break;
   case "orange":
     echo "Your favorite fruit is orange!";
     break;
   default:
     echo "Your favorite fruit is neither apple, banana, or orange!";
}
?>
```

### 12. PHP while 循环

PHP while 循环在指定条件为 true 时执行代码块。PHP 循环。在您编写代码时，经常需要反复运行同一代码块。我们可以使用循环来执行这样的任务，而不是在脚本中添加若干几乎相等的代码行。在 PHP 中，我们有以下循环语句：1）while —— 只要指定条件为真，则循环代码块；2）do...while —— 先执行一次代码块，然后只要指定条件为真则重复循环；3）for —— 循环代码块指定次数；4）foreach —— 遍历数组中的每个元素并循环代码块。

PHP while 循环。只要指定的条件为真，while 循环就会执行代码块。

```
while (条件为真) {
  要执行的代码;
}
```

下例首先把变量 \$x 设置为 1（\$x=1）。然后执行 while 循环，只要 \$x 小于或等于 5。循环每运行一次，\$x 将递增 1：

```
<?php 
$x=1; 

while($x<=5) {
  echo "这个数字是：$x <br>";
  $x++;
} 
?>
```

PHP do...while 循环。do...while 循环首先会执行一次代码块，然后检查条件，如果指定条件为真，则重复循环。

```
do {
  要执行的代码;
} while (条件为真);
```

下面的例子首先把变量 \$x 设置为 1（\$x=1）。然后，do while 循环输出一段字符串，然后对变量 \$x 递增 1。随后对条件进行检查（\$x 是否小于或等于 5）。只要 \$x 小于或等于 5，循环将会继续运行：

```
<?php 
$x=1; 

do {
  echo "这个数字是：$x <br>";
  $x++;
} while ($x<=5);
?>
```

请注意，do while 循环只在执行循环内的语句之后才对条件进行测试。这意味着 do while 循环至少会执行一次语句，即使条件测试在第一次就失败了。下面的例子把 \$x 设置为 6，然后运行循环，随后对条件进行检查：

```
<?php 
$x=6;

do {
  echo "这个数字是：$x <br>";
  $x++;
} while ($x<=5);
?>
```

### 13. PHP for 循环

PHP for 循环执行代码块指定的次数。如果您已经提前确定脚本运行的次数，可以使用 for 循环。

```
for (init counter; test counter; increment counter) {
  code to be executed;
}
```

参数：1）init counter：初始化循环计数器的值；2）test counter：: 评估每个循环迭代。如果值为 TRUE，继续循环。如果它的值为 FALSE，循环结束；3）increment counter：增加循环计数器的值。下面的例子显示了从 0 到 10 的数字：

```
<?php 
for ($x=0; $x<=10; $x++) {
  echo "数字是：$x <br>";
} 
?>
```

PHP foreach 循环。foreach 循环只适用于数组，并用于遍历数组中的每个键 / 值对。

```
foreach ($array as $value) {
  code to be executed;
}
```

每进行一次循环迭代，当前数组元素的值就会被赋值给 \$value 变量，并且数组指针会逐一地移动，直到到达最后一个数组元素。下面的例子演示的循环将输出给定数组（\$colors）的值：

```
<?php 
$colors = array("red","green","blue","yellow"); 

foreach ($colors as $value) {
  echo "$value <br>";
}
?>
```

### 14. PHP 函数

PHP 的真正力量来自它的函数：它拥有超过 1000 个内建的函数。PHP 用户定义函数：1）除了内建的 PHP 函数，我们可以创建我们自己的函数。2）函数是可以在程序中重复使用的语句块。3）页面加载时函数不会立即执行。4）函数只有在被调用时才会执行。

在 PHP 创建用户定义函数。用户定义的函数声明以单词 "function" 开头：

```
function functionName() {
  被执行的代码;
}
```

注释：函数名能够以字母或下划线开头（而非数字）。函数名对大小写不敏感。提示：函数名应该能够反映函数所执行的任务。在下面的例子中，我们创建名为 "writeMsg ()" 的函数。打开的花括号（{）指示函数代码的开始，而关闭的花括号（}）指示函数的结束。此函数输出 "Hello world!"。如需调用该函数，只要使用函数名即可：

```
<?php
function sayHi() {
  echo "Hello world!";
}

sayhi(); // 调用函数
?>
```

PHP 函数参数。可以通过参数向函数传递信息。参数类似变量。参数被定义在函数名之后，括号内部。您可以添加任意多参数，只要用逗号隔开即可。下面的例子中的函数有一个参数（\$fname）。当调用 familyName () 函数时，我们同时要传递一个名字（例如 Bill），这样会输出不同的名字，但是姓氏相同：

```
<?php
function familyName($fname) {
  echo "$fname Zhang.<br>";
}

familyName("Li");
familyName("Hong");
familyName("Tao");
familyName("Xiao Mei");
familyName("Jian");
?>
```

下面的例子中的函数有两个参数（\$fname 和 \$year）：

```
<?php
function familyName($fname,$year) {
  echo "$fname Zhang. Born in $year <br>";
}

familyName("Li","1975");
familyName("Hong","1978");
familyName("Tao","1983");
?>
```

PHP 默认参数值。下面的例子展示了如何使用默认参数。如果我们调用没有参数的 setHeight () 函数，它的参数会取默认值；PHP 函数 —— 返回值。如需使函数返回值，请使用 return 语句。

```
<?php
function setHeight($minheight=50) {
  echo "The height is : $minheight <br>";
}

setHeight(350);
setHeight(); // 将使用默认值 50
setHeight(135);
setHeight(80);
?>
```

### 15. PHP 数组

数组能够在单独的变量名中存储一个或多个值。数组在单个变量中存储多个值：

```
<?php
$cars=array("porsche","BMW","Volvo");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
?>
```

什么是数组？数组是特殊的变量，它可以同时保存一个以上的值。如果您有一个项目列表（例如汽车品牌列表），在单个变量中存储这些品牌名称是这样的：

```
$cars1="porsche";
$cars2="BMW";
$cars3="Volvo";
```

不过，假如您希望对变量进行遍历并找出特定的那个值？或者如果您需要存储 300 个汽车品牌，而不是 3 个呢？解决方法是创建数组！数组能够在单一变量名中存储许多值，并且您能够通过引用索引号来访问某个值。在 PHP 中创建数组。在 PHP 中，array () 函数用于创建数组：

    array();

在 PHP 中，有三种数组类型：1）索引数组 —— 带有数字索引的数组；2）关联数组 —— 带有指定键的数组；3）多维数组 —— 包含一个或多个数组的数组。

PHP 索引数组。有两种创建索引数组的方法：1）索引是自动分配的（索引从 0 开始）：

    $cars=array("porsche","BMW","Volvo");

或者也可以手动分配索引：

```
$cars[0]="porsche";
$cars[1]="BMW";
$cars[2]="Volvo";
```

下面的例子创建名为 \$cars 的索引数组，为其分配三个元素，然后输出包含数组值的一段文本：

```
<?php
$cars=array("porsche","BMW","Volvo");
echo "I like " . $cars[0] . ", " . $cars[1] . " and " . $cars[2] . ".";
?>
```

获得数组的长度 —— count () 函数。count () 函数用于返回数组的长度（元素数）：

```
<?php
$cars=array("porsche","BMW","Volvo");
echo count($cars);
?>
```

遍历索引数组。如需遍历并输出索引数组的所有值，您可以使用 for 循环，就像这样：

```
<?php
$cars=array("porsche","BMW","Volvo");
$arrlength=count($cars);

for($x=0;$x<$arrlength;$x++) {
  echo $cars[$x];
  echo "<br>";
}
?>
```

PHP 关联数组。关联数组是使用您分配给数组的指定键的数组。有两种创建关联数组的方法：

    $age=array("Bill"=>"35","Steve"=>"37","Elon"=>"43");

或者：

```
$age['Bill']="63";
$age['Steve']="56";
$age['Elon']="47";
```

随后可以在脚本中使用指定键：

```
<?php
$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");
echo "Elon is " . $age['Elon'] . " years old.";
?>
```

遍历关联数组。如需遍历并输出关联数组的所有值，您可以使用 foreach 循环，就像这样：

```
<?php
$age=array("Bill"=>"63","Steve"=>"56","Elon"=>"47");

foreach($age as $x=>$x_value) {
  echo "Key=" . $x . ", Value=" . $x_value;
  echo "<br>";
}
?>
```

多维数组。我们将在 PHP 高级教程中讲解多维数组。如需完整的数组函数参考手册，请访问我们的 PHP 数组参考手册。该参考手册包含每个函数的简要描述、使用示例：[PHP Array 函数](https://www.w3school.com.cn/php/php_ref_array.asp)。

### 16. PHP 数组排序

数组中的元素能够以字母或数字顺序进行升序或降序排序。PHP —— 数组的排序函数。在本节中，我们将学习如下 PHP 数组排序函数：1）sort () —— 以升序对数组排序。2）rsort () —— 以降序对数组排序。3）asort () —— 根据值，以升序对关联数组进行排序。4）ksort () —— 根据键，以升序对关联数组进行排序。5）arsort () —— 根据值，以降序对关联数组进行排序。6）krsort () —— 根据键，以降序对关联数组进行排序。7）对数组进行升序排序 —— sort ()。

### 17. PHP 全局变量 —— 超全局变量

超全局变量在 PHP 4.1.0 中引入，是在全部作用域中始终可用的内置变量。PHP 全局变量 —— 超全局变量。PHP 中的许多预定义变量都是「超全局的」，这意味着它们在一个脚本的全部作用域中都可用。在函数或方法中无需执行 global \$variable; 就可以访问它们。这些超全局变量是：

```
$GLOBALS
$_SERVER
$_REQUEST
$_POST
$_GET
$_FILES
$_ENV
$_COOKIE
$_SESSION
```

\$GLOBALS —— 引用全局作用域中可用的全部变量。\$GLOBALS 这种全局变量用于在 PHP 脚本中的任意位置访问全局变量（从函数或方法中均可）。PHP 在名为 \$GLOBALS [index] 的数组中存储了所有全局变量。变量的名字就是数组的键。下面的例子展示了如何使用超级全局变量 \$GLOBALS：

```
<?php 
$x = 75; 
$y = 25;
 
function addition() { 
  $GLOBALS['z'] = $GLOBALS['x'] + $GLOBALS['y']; 
}
 
addition(); 
echo $z; 
?>
```

在上面的例子中，由于 z 是 \$GLOBALS 数组中的变量，因此在函数之外也可以访问它。

\$_SERVER 这种超全局变量保存关于报头、路径和脚本位置的信息。

下面的例子展示了如何使用 \$_SERVER 中的某些元素：

```
<?php 
echo $_SERVER['PHP_SELF'];
echo "<br>";
echo $_SERVER['SERVER_NAME'];
echo "<br>";
echo $_SERVER['HTTP_HOST'];
echo "<br>";
echo $_SERVER['HTTP_REFERER'];
echo "<br>";
echo $_SERVER['HTTP_USER_AGENT'];
echo "<br>";
echo $_SERVER['SCRIPT_NAME'];
?>
```

下表列出了您能够在 \$_SERVER 中访问的最重要的元素：

PHP \$_REQUEST 用于收集 HTML 表单提交的数据。

下面的例子展示了一个包含输入字段及提交按钮的表单。当用户通过点击提交按钮来提交表单数据时，表单数据将发送到 \<form> 标签的 action 属性中指定的脚本文件。在这个例子中，我们指定文件本身来处理表单数据。如果您需要使用其他的 PHP 文件来处理表单数据，请修改为您选择的文件名即可。然后，我们可以使用超级全局变量 \$_REQUEST 来收集 input 字段的值：

```
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>

<?php 
$name = $_REQUEST['fname']; 
echo $name; 
?>

</body>
</html>
```

PHP \$_POST 广泛用于收集提交 method="post" 的 HTML 表单后的表单数据。

\$_POST 也常用于传递变量。

下面的例子展示了一个包含输入字段和提交按钮的表单。当用户点击提交按钮来提交数据后，表单数据会发送到 \<form> 标签的 action 属性中指定的文件。在本例中，我们指定文件本身来处理表单数据。如果您希望使用另一个 PHP 页面来处理表单数据，请用更改为您选择的文件名。然后，我们可以使用超全局变量 \$_POST 来收集输入字段的值：

```
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
Name: <input type="text" name="fname">
<input type="submit">
</form>

<?php 
$name = $_POST['fname'];
echo $name; 
?>

</body>
</html>
```

PHP \$_GET 也可用于收集提交 HTML 表单 (method="get") 之后的表单数据。

\$_GET 也可以收集 URL 中的发送的数据。

假设我们有一张页面含有带参数的超链接：

```
<html>
<body>

<a href="test_get.php?subject=PHP&web=W3school.com.cn">测试 $GET</a>

</body>
</html>
```

当用户点击链接 "测试 \$GET"，参数 "subject" 和 "web" 被发送到 "test_get.php"，然后您就能够通过 \$_GET 在 "test_get.php" 中访问这些值了。

下面的例子是 "test_get.php" 中的代码：

```
<html>
<body>

<?php 
echo "在 " . $_GET['web'] . " 学习 " . $_GET['subject'];
?>

</body>
</html>
```

## 0401. PHP 数据库

PHP MySQL 连接数据库。连接到一个 MySQL 数据库。在您能够访问并处理数据库中的数据之前，您必须创建到达数据库的连接。在 PHP 中，这个任务通过 mysql_connect() 函数完成。

    mysql_connect(servername,username,password);

1）servername，可选。规定要连接的服务器。默认是 "localhost:3306"。2）username，可选。规定登录所使用的用户名。默认值是拥有服务器进程的用户的名称。3）password，可选。规定登录所用的密码。默认是 ""。

注释：虽然还存在其他的参数，但上面列出了最重要的参数。请访问 W3School 提供的 PHP MySQL 参考手册：[PHP MySQL 函数](https://www.w3school.com.cn/php/php_ref_mysql.asp)。

在下面的例子中，我们在一个变量中 (\$con) 存放了在脚本中供稍后使用的连接。如果连接失败，将执行 "die" 部分：

1『

一直连接不上 mysql，报错：Warning: mysqli::__construct(): (HY000/1045): Access denied for user 'dalong'@'localhost' (using password: YES) in /opt/lampp/htdocs/2020011w3school/0402mysql.php on line 7
连接失败: Access denied for user 'dalong'@'localhost' (using password: YES)

然后发现「菜鸟教程」里的资料更新，是 PHP7 的，按里面的源码来还是解决不了上面的问题。最后把 mysql 更新到了最新版，在安全设置里面选了允许匿名用户用空密码登录，然后采用匿名登录的方式才连接成功。后面数据库方面的资料就转战菜鸟那边。

』

## 02. PHP 表单

1『发现在 md 文件里可以显示基本的表单代码结果。』

### 01. PHP 表单处理

PHP 超全局变量 \$_GET 和 \$POST 用于收集表单数据（form-data）。PHP —— 一个简单的 HTML 表单。下面的例子显示了一个简单的 HTML 表单，它包含两个输入字段和一个提交按钮：

```
<html>
<body>

<form action="welcome.php" method="post">
Name: <input type="text" name="name"><br>
E-mail: <input type="text" name="email"><br>
<input type="submit">
</form>

</body>
</html>
```

当用户填写此表单并点击提交按钮后，表单数据会发送到名为 "welcome.php" 的 PHP 文件供处理。表单数据是通过 HTTP POST 方法发送的。如需显示出被提交的数据，您可以简单地输出（echo）所有变量。"welcome.php" 文件是这样的：

```
<html>
<body>

Welcome <?php echo $_POST["name"]; ?><br>
Your email address is: <?php echo $_POST["email"]; ?>

</body>
</html>
```

输出：

Welcome Bill

Your email address is Bill.Gates@example.com

1『点完提交后浏览器的地址就直接转到了 welcome.php 文件上，即「http://192.168.64.2/2020011w3school/welcome.php」。这里注意，文件名一定要是 welcome.php，因为 action 的属性是它。』

使用 HTTP GET 方法也能得到相同的结果：

```
<html>
<body>

<form action="welcome_get.php" method="get">
Name: <input type="text" name="name"><br>
E-mail: <input type="text" name="email"><br>
<input type="submit">
</form>

</body>
</html>
```

"welcome_get.php" 是这样的：

```
<html>
<body>

Welcome <?php echo $_GET["name"]; ?><br>
Your email address is: <?php echo $_GET["email"]; ?>

</body>
</html>
```

上面的代码很简单。不过，最重要的内容被漏掉了。您需要对表单数据进行验证，以防止脚本出现漏洞。注意：在处理 PHP 表单时请关注安全！本页未包含任何表单验证程序，它只向我们展示如何发送并接收表单数据。不过稍后的章节会为您讲解如何提高 PHP 表单的安全性！对表单进行适当的安全验证对于抵御黑客攻击和垃圾邮件非常重要！

GET vs. POST。GET 和 POST 都创建数组（例如，array( key => value, key2 => value2, key3 => value3, ...)）。此数组包含键/值对，其中的键是表单控件的名称，而值是来自用户的输入数据。GET 和 POST 被视作 \$_GET 和 \$POST。它们是超全局变量，这意味着对它们的访问无需考虑作用域 —— 无需任何特殊代码，您能够从任何函数、类或文件访问它们。

\$_GET 是通过 URL 参数传递到当前脚本的变量数组。

\$_POST 是通过 HTTP POST 传递到当前脚本的变量数组。

何时使用 GET？通过 GET 方法从表单发送的信息对任何人都是可见的（所有变量名和值都显示在 URL 中）。GET 对所发送信息的数量也有限制。限制在大约 2000 个字符。不过，由于变量显示在 URL 中，把页面添加到书签中也更为方便。GET 可用于发送非敏感的数据。

注释：绝不能使用 GET 来发送密码或其他敏感信息！

何时使用 POST？通过 POST 方法从表单发送的信息对其他人是不可见的（所有名称/值会被嵌入 HTTP 请求的主体中），并且对所发送信息的数量也无限制。此外 POST 支持高阶功能，比如在向服务器上传文件时进行 multi-part 二进制输入。不过，由于变量未显示在 URL 中，也就无法将页面添加到书签。

提示：开发者偏爱 POST 来发送表单数据。







