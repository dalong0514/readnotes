## 记忆时间

## 目录

0801 函数

0901 类

1001 文件与异常

1101 测试代码

## 0801. 函数

在本章中，你学习了：如何编写函数，以及如何传递实参，让函数能够访问完成其工作所需的信息；如何使用位置实参和关键字实参，以及如何接受任意数量的实参；显示输出的函数和返回值的函数；如何将函数同列表、字典、if 语句和 while 循环结合起来使用。你还知道了如何将函数存储在被称为模块的独立文件中，让程序文件更简单、更易于理解。最后，你学习了函数编写指南，遵循这些指南可让程序始终结构良好，并对你和其他人来说易于阅读。

程序员的目标之一是，编写简单的代码来完成任务，而函数有助于你实现这样的目标。它们让你编写好代码块并确定其能够正确运行后，就可置之不理。确定函数能够正确地完成其工作后，你就可以接着投身于下一个编码任务。

函数让你编写代码一次后，想重用它们多少次就重用多少次。需要运行函数中的代码时，只需编写一行函数调用代码，就可让函数完成其工作。需要修改函数的行为时，只需修改一个代码块，而所做的修改将影响调用这个函数的每个地方。

使用函数让程序更容易阅读，而良好的函数名概述了程序各个部分的作用。相对于阅读一系列的代码块，阅读一系列函数调用让你能够更快地明白程序的作用。

函数还让代码更容易测试和调试。如果程序使用一系列的函数来完成其任务，而其中的每个函数都完成一项具体的工作，测试和维护起来将容易得多：你可编写分别调用每个函数的程序，并测试每个函数是否在它可能遇到的各种情形下都能正确地运行。经过这样的测试后你就能信心满满，深信你每次调用这些函数时，它们都将正确地运行。

### 8.1 定义函数

```py
❶ def greet_user():
❷ """显示简单的问候语"""
    ❸ print("Hello!")
❹ greet_user()
```

紧跟在 `def greet_user()`：后面的所有缩进行构成了函数体。❷ 处的文本是被称为文档字符串 （docstring）的注释，描述了函数是做什么的。文档字符串用三引号括起，Python 使用它们来生成有关程序中函数的文档。

在函数 `greet_user()` 的定义中，变量 username 是一个形参 —— 函数完成其工作所需的一项信息。在代码 greet_user('jesse') 中，值 'jesse' 是一个实参。实参是调用函数时传递给函数的信息。我们调用函数时，将要让函数使用的信息放在括号内。在 greet_user('jesse') 中，将实参 'jesse' 传递给了函数 greet\_user()，这个值被存储在形参 username 中。大家有时候会形参、实参不分，因此如果你看到有人将函数定义中的变量称为实参或将函数调用中的变量称为形参，不要大惊小怪。

1『函数体里面的是形参，外面传递的是实参；传递给函数的实参得是字符串，否则不认的。』

### 8.2 传递实参

鉴于函数定义中可能包含多个形参，因此函数调用中也可能包含多个实参。向函数传递实参的方式很多，可使用位置实参，这要求实参的顺序与形参的顺序相同；也可使用关键字实参，其中每个实参都由变量名和值组成；还可使用列表和字典。

你调用函数时，Python 必须将函数调用中的每个实参都关联到函数定义中的一个形参。为此，最简单的关联方式是基于实参的顺序。这种关联方式被称为位置实参。

关键字实参是传递给函数的「名称—值」对。你直接在实参中将名称和值关联起来了，因此向函数传递实参时不会混淆（不会得到名为 Hamster 的 harry 这样的结果）。关键字实参让你无需考虑函数调用中的实参顺序，还清楚地指出了函数调用中各个值的用途。

```py
describe_pet(animal_type='hamster', pet_name='harry')
describe_pet(pet_name='harry', animal_type='hamster')
```

编写函数时，可给每个形参指定默认值。在调用函数中给形参提供了实参时，Python 将使用指定的实参值；否则，将使用形参的默认值。因此，给形参指定默认值后，可在函数调用中省略相应的实参。使用默认值可简化函数调用，还可清楚地指出函数的典型用法。

```py
def describe_pet(pet_name, animal_type='dog'):
"""显示宠物的信息"""
	print("\nI have a " + animal_type + ".")
	print("My " + animal_type + "'s name is " + pet_name.title() + ".")
describe_pet(pet_name='willie')
```

请注意，在这个函数的定义中，修改了形参的排列顺序。由于给 animal_type 指定了默认值，无需通过实参来指定动物类型，因此在函数调用中只包含一个实参 —— 宠物的名字。然而，Python 依然将这个实参视为位置实参，因此如果函数调用中只包含宠物的名字，这个实参将关联到函数定义中的第一个形参。这就是需要将 pet_name（没有默认值的形参）放在形参列表开头的原因所在。

使用默认值时，在形参列表中必须先列出没有默认值的形参，再列出有默认值的实参。这让 Python 依然能够正确地解读位置实参。

1『函数定义里，必须把设有默认值的形参设置在后面，否者语法错误。』

### 8.3 返回值

函数并非总是直接显示输出，相反，它可以处理一些数据，并返回一个或一组值。函数返回的值被称为返回值。在函数中，可使用 return 语句将值返回到调用函数的代码行。返回值让你能够将程序的大部分繁重工作移到函数中去完成，从而简化主程序。

1『字符串的方法 title() 总是漏掉后面的 ()。』

有时候，需要让实参变成可选的，这样使用函数的人就只需在必要时才提供额外的信息。可使用默认值来让实参变成可选的。

然而，并非所有的人都有中间名，但如果你调用这个函数时只提供了名和姓，它将不能正确地运行。为让中间名变成可选的，可给实参 middle_name 指定一个默认值 —— 空字符串，并在用户没有提供中间名时不使用这个实参。为让 get\_formatted\_name() 在没有提供中间名时依然可行，可给实参 middle_name 指定一个默认值 —— 空字符串，并将其移到形参列表的末尾。

1『怪不得这个例子这么属性，后面单元测试那章里用的就是这个例子。』

函数可返回任何类型的值，包括列表和字典等较复杂的数据结构。例如，下面的函数接受姓名的组成部分，并返回一个表示人的字典：

可将函数同本书前面介绍的任何 Python 结构结合起来使用。例如，下面将结合使用函数 get\_formatted\_name() 和 while 循环，以更正规的方式问候用户。

我们添加了一条消息来告诉用户如何退出，然后在每次提示用户输入时，都检查他输入的是否是退出值，如果是，就退出循环。现在，这个程序将不断地问候，直到用户输入的姓或名为 'q'  为止：

```py
def get_formatted_name(first_name, last_name):
	"""返回整洁的姓名"""
	full_name = first_name + ' ' + last_name
	return full_name.title()
while True:
	print("\nPlease tell me your name:")
	print("(enter 'q' at any time to quit)")
	f_name = input("First name: ")
	if f_name == 'q':
	break
	l_name = input("Last name: ")
	if l_name == 'q':
	break
formatted_name = get_formatted_name(f_name, l_name)
print("\nHello, " + formatted_name + "!")
```

### 8.4 传递列表

你经常会发现，向函数传递列表很有用，这种列表包含的可能是名字、数字或更复杂的对象（如字典）。将列表传递给函数后，函数就能直接访问其内容。将列表传递给函数后，函数就可对其进行修改。在函数中对这个列表所做的任何修改都是永久性的，这让你能够高效地处理大量的数据。

1『将列表传递给函数，在函数里对列表进行修改。这个思路可以高效的处理大量数据。』

我们创建了一个未打印的设计列表，还创建了一个空列表，用于存储打印好的模型。接下来，由于我们已经定义了两个函数，因此只需调用它们并传入正确的实参即可。我们调用 print_models() 并向它传递两个列表；像预期的一样，print_models() 模拟打印设计的过程。接下来，我们调用 show_completed_models()，并将打印好的模型列表传递给它，让其能够指出打印了哪些模型。描述性的函数名让别人阅读这些代码时也能明白，虽然其中没有任何注释。

相比于没有使用函数的版本，这个程序更容易扩展和维护。如果以后需要打印其他设计，只需再次调用 print_models() 即可。如果我们发现需要对打印代码进行修改，只需修改这些代码一次，就能影响所有调用该函数的地方；与必须分别修改程序的多个地方相比，这种修改的效率更高。

这个程序还演示了这样一种理念，即每个函数都应只负责一项具体的工作。第一个函数打印每个设计，而第二个显示打印好的模型；这优于使用一个函数来完成两项工作。编写函数时，如果你发现它执行的任务太多，请尝试将这些代码划分到两个函数中。别忘了，总是可以在一个函数中调用另一个函数，这有助于将复杂的任务划分成一系列的步骤。

有时候，需要禁止函数修改列表。例如，假设像前一个示例那样，你有一个未打印的设计列表，并编写了一个将这些设计移到打印好的模型列表中的函数。你可能会做出这样的决定：即便打印所有设计后，也要保留原来的未打印的设计列表，以供备案。但由于你将所有的设计都移出了 unprinted_designs，这个列表变成了空的，原来的列表没有了。为解决这个问题，可向函数传递列表的副本而不是原件；这样函数所做的任何修改都只影响副本，而丝毫不影响原件。

虽然向函数传递列表的副本可保留原始列表的内容，但除非有充分的理由需要传递副本，否则还是应该将原始列表传递给函数，因为让函数使用现成列表可避免花时间和内存创建副本，从而提高效率，在处理大型列表时尤其如此。

1『禁止函数修改列表，可以通过传递列表的副本给函数而非其真身。』

### 8.5 传递任意数量的实参

有时候，你预先不知道函数需要接受多少个实参，好在 Python 允许函数从调用语句中收集任意数量的实参。例如，来看一个制作比萨的函数，它需要接受很多配料，但你无法预先确定顾客要多少种配料。下面的函数只有一个形参 *toppings，但不管调用语句提供了多少实参，这个形参都将它们统统收入囊中。

形参名 *toppings 中的星号让 Python 创建一个名为 toppings 的空元组，并将收到的所有值都封装到这个元组中。函数体内的 print 语句通过生成输出来证明 Python 能够处理使用一个值调用函数的情形，也能处理使用三个值来调用函数的情形。它以类似的方式处理不同的调用，注意，Python 将实参封装到一个元组中，即便函数只收到一个值也如此。

如果要让函数接受不同类型的实参，必须在函数定义中将接纳任意数量实参的形参放在最后。Python 先匹配位置实参和关键字实参，再将余下的实参都收集到最后一个形参中。例如，如果前面的函数还需要一个表示比萨尺寸的实参，必须将该形参放在形参 *toppings 的前面。

```py
def make_pizza(size, *toppings):
"""概述要制作的比萨"""
	print("\nMaking a " + str(size) +
		"-inch pizza with the following toppings:")
	for topping in toppings:
		print("- " + topping)
make_pizza(16, 'pepperoni')
make_pizza(12, 'mushrooms', 'green peppers', 'extra cheese')
```

有时候，需要接受任意数量的实参，但预先不知道传递给函数的会是什么样的信息。在这种情况下，可将函数编写成能够接受任意数量的「键-值」对 —— 调用语句提供了多少就接受多少。一个这样的示例是创建用户简介：你知道你将收到有关用户的信息，但不确定会是什么样的信息。在下面的示例中，函数 build_profile() 接受名和姓，同时还接受任意数量的关键字实参。

```py
def build_profile(first, last, **user_info):
	"""创建一个字典，其中包含我们知道的有关用户的一切"""
	profile = {}
	❶ profile['first_name'] = first
	profile['last_name'] = last
	❷ for key, value in user_info.items():
		profile[key] = value
	return profile
user_profile = build_profile('albert', 'einstein', location='princeton', field='physics')
print(user_profile)
```

函数 build_profile() 的定义要求提供名和姓，同时允许用户根据需要提供任意数量的「名称-值」对。形参 **user_info 中的两个星号让 Python 创建一个名为 user_info 的空字典，并将收到的所有「名称-值」对都封装到这个字典中。在这个函数中，可以像访问其他字典那样访问 user_info 中的「名称-值」对。

在 build_profile() 的函数体内，我们创建了一个名为 profile 的空字典，用于存储用户简介。在 ❶ 处，我们将名和姓加入到这个字典中，因为我们总是会从用户那里收到这两项信息。在 ❷ 处，我们遍历字典 user_info 中的「键-值」对，并将每个「键-值」对都加入到字典 profile 中。最后，我们将字典 profile 返回给函数调用行。

我们调用 build_profile()，向它传递名（'albert' ）、姓（'einstein' ）和两个「键-值」对（location='princeton' 和 field='physics' ），并将返回的 profile 存储在变量 user_profile 中，再打印这个变量。在这里，返回的字典包含用户的名和姓，还有求学的地方和所学专业。调用这个函数时，不管额外提供了多少个「键-值」对，它都能正确地处理。

1『注意，要传递的「键-值」对实参，键没有使用引号。』

编写函数时，你可以以各种方式混合使用位置实参、关键字实参和任意数量的实参。知道这些实参类型大有裨益，因为阅读别人编写的代码时经常会见到它们。要正确地使用这些类型的实参并知道它们的使用时机，需要经过一定的练习。就目前而言，牢记使用最简单的方法来完成任务就好了。你继续往下阅读，就会知道在各种情况下哪种方法的效率是最高的。

### 8.6 将函数存储在模块中

函数的优点之一是，使用它们可将代码块与主程序分离。通过给函数指定描述性名称，可让主程序容易理解得多。你还可以更进一步，将函数存储在被称为「模块」的独立文件中，再将模块导入到主程序中。import 语句允许在当前运行的程序文件中使用模块中的代码。

通过将函数存储在独立的文件中，可隐藏程序代码的细节，将重点放在程序的高层逻辑上。这还能让你在众多不同的程序中重用函数。将函数存储在独立文件中后，可与其他程序员共享这些文件而不是整个程序。知道如何导入函数还能让你使用其他程序员编写的函数库。

1『汇总：1）导入函数的方法有：导入整个模块、导入特定的函数、使用 as 给函数指定别名、使用 as 给模块指定别名、导入模块中的所有函数。2）导入整个模块：import pizza。3）使用 as 给模块指定别名：import pizza as piz。4）导入特定的函数：from pizza import make\_pizza。5）使用 as 给函数指定别名：from pizza import make\_pizza as mp。』

```py
import pizza
```

Python 读取这个文件时，代码行 import pizza 让 Python 打开文件 pizza.py，并将其中的所有函数都复制到这个程序中。你看不到复制的代码，因为这个程序运行时，Python 在幕后复制这些代码。你只需知道，在 making_pizzas.py 中，可以使用 pizza.py 中定义的所有函数。要调用被导入的模块中的函数，可指定导入的模块的名称 pizza 和函数名 make_pizza()，并用句点分隔它们（见❶）。这些代码的输出与没有导入模块的原始程序相同：

```py
module_name.function_name()
```

你还可以导入模块中的特定函数，这种导入方法的语法如下：

```py
from module_name import function_name
from module_name import function_name as piz
```

通过用逗号分隔函数名，可根据需要从模块中导入任意数量的函数。若使用这种语法，调用函数时就无需使用句点。由于我们在 import 语句中显式地导入了函数 make_pizza()，因此调用它时只需指定其名称。

你还可以给模块指定别名。通过给模块指定简短的别名（如给模块 pizza 指定别名 p ），让你能够更轻松地调用模块中的函数。相比于 pizza.make_pizza()，p.make_pizza() 更为简洁：

```py
import module_name as mn
```

import 语句中的星号让 Python 将模块 pizza 中的每个函数都复制到这个程序文件中。由于导入了每个函数，可通过名称来调用每个函数，而无需使用句点表示法。然而，使用并非自己编写的大型模块时，最好不要采用这种导入方法：如果模块中有函数的名称与你的项目中使用的名称相同，可能导致意想不到的结果：Python 可能遇到多个名称相同的函数或变量，进而覆盖函数，而不是分别导入所有的函数。

最佳的做法是，要么只导入你需要使用的函数，要么导入整个模块并使用句点表示法。这能让代码更清晰，更容易阅读和理解。这里之所以介绍这种导入方法，只是想让你在阅读别人编写的代码时，如果遇到类似于下面的 import 语句，能够理解它们。

### 8.7 函数编写指南

编写函数时，需要牢记几个细节。应给函数指定描述性名称，且只在其中使用小写字母和下划线。描述性名称可帮助你和别人明白代码想要做什么。给模块命名时也应遵循上述约定。

每个函数都应包含简要地阐述其功能的注释，该注释应紧跟在函数定义后面，并采用文档字符串格式。文档良好的函数让其他程序员只需阅读文档字符串中的描述就能够使用它：他们完全可以相信代码如描述的那样运行；只要知道函数的名称、需要的实参以及返回值的类型，就能在自己的程序中使用它。

给形参指定默认值时，等号两边不要有空格：

```py
def function_name(parameter_0, parameter_1='default value')
```

对于函数调用中的关键字实参，也应遵循这种约定：

```py
function_name(value_0, parameter_1='value')
```

[PEP 8 -- Style Guide for Python Code | Python.org](https://www.python.org/dev/peps/pep-0008/) 建议代码行的长度不要超过 79 字符，这样只要编辑器窗口适中，就能看到整行代码。如果形参很多，导致函数定义的长度超过了 79 字符，可在函数定义中输入左括号后按回车键，并在下一行按两次 Tab 键，从而将形参列表和只缩进一层的函数体区分开来。

所有的 import 语句都应放在文件开头，唯一例外的情形是，在文件开头使用了注释来描述整个程序。

1-2『 Python 编程规范汇总：1）函数名用小写单词加下划线（不同于 Java、PHP 中的驼峰命名）。2）定义函数，给形参指定默认值时，等号两边不要有空格。做一张主题卡片。』 —— 已完成

## 0901. 类

在本章中，你学习了：如何编写类；如何使用属性在类中存储信息，以及如何编写方法，以让类具备所需的行为；如何编写方法 \_\_init\_\_()，以便根据类创建包含所需属性的实例。你见识了如何修改实例的属性 —— 包括直接修改以及通过方法进行修改。你还了解了：使用继承可简化相关类的创建工作；将一个类的实例用作另一个类的属性可让类更简洁。

你了解到，通过将类存储在模块中，并在需要使用这些类的文件中导入它们，可让项目组织有序。你学习了 Python 标准库，并见识了一个使用模块 collections 中的 OrderedDict 类的示例。最后，你学习了编写类时应遵循的 Python 约定。

面向对象编程是最有效的软件编写方法之一。在面向对象编程中，你编写表示现实世界中的事物和情景的类，并基于这些类来创建对象。编写类时，你定义一大类对象都有的通用行为。基于类创建对象时，每个对象都自动具备这种通用行为，然后可根据需要赋予每个对象独特的个性。使用面向对象编程可模拟现实情景，其逼真程度达到了令你惊讶的地步。

根据类来创建对象被称为实例化，这让你能够使用类的实例。在本章中，你将编写一些类并创建其实例。你将指定可在实例中存储什么信息，定义可对这些实例执行哪些操作。你还将编写一些类来扩展既有类的功能，让相似的类能够高效地共享代码。你将把自己编写的类存储在模块中，并在自己的程序文件中导入其他程序员编写的类。

理解面向对象编程有助于你像程序员那样看世界，还可以帮助你真正明白自己编写的代码：不仅是各行代码的作用，还有代码背后更宏大的概念。了解类背后的概念可培养逻辑思维，让你能够通过编写程序来解决遇到的几乎任何问题。

随着面临的挑战日益严峻，类还能让你以及与你合作的其他程序员的生活更轻松。如果你与其他程序员基于同样的逻辑来编写代码，你们就能明白对方所做的工作；你编写的程序将能被众多合作者所理解，每个人都能事半功倍。

### 9.1 创建和使用类

使用类几乎可以模拟任何东西。下面来编写一个表示小狗的简单类 Dog —— 它表示的不是特定的小狗，而是任何小狗。对于大多数宠物狗，我们都知道些什么呢？它们都有名字和年龄；我们还知道，大多数小狗还会蹲下和打滚。由于大多数小狗都具备上述两项信息（名字和年龄）和两种行为（蹲下和打滚），我们的 Dog 类将包含它们。

```py
❶ class Dog():
	❷ """一次模拟小狗的简单尝试"""
	❸ def __init__(self, name, age):
	"""初始化属性name和age"""
		❹ self.name = name
		self.age = age
	❺ def sit(self):

	"""模拟小狗被命令时蹲下"""
		print(self.name.title() + " is now sitting.")
		
	def roll_over(self):
	"""模拟小狗被命令时打滚"""
		print(self.name.title() + " rolled over!")
```

根据约定，在 Python 中，首字母大写的名称指的是类。这个类定义中的括号是空的，因为我们要从空白创建这个类。在 ❷ 处，我们编写了一个文档字符串，对这个类的功能作了描述。

类中的函数称为方法 ；你前面学到的有关函数的一切都适用于方法，就目前而言，唯一重要的差别是调用方法的方式。❸ 处的方法 \_\_init\_\_() 是一个特殊的方法，每当你根据 Dog 类创建新实例时，Python 都会自动运行它。在这个方法的名称中，开头和末尾各有两个下划线，这是一种约定，旨在避免 Python 默认方法与普通方法发生名称冲突。

1『函数在类里面被称为「方法」。』

我们将方法 \_\_init\_\_() 定义成了包含三个形参：self 、name 和 age。在这个方法的定义中，形参 self 必不可少，还必须位于其他形参的前面。为何必须在方法定义中包含形参 self  呢？因为 Python 调用这个 \_\_init\_\_() 方法来创建 Dog 实例时，将自动传入实参 self。每个与类相关联的方法调用都自动传递实参 self，它是一个指向实例本身的引用，让实例能够访问类中的属性和方法。我们创建 Dog 实例时，Python 将调用 Dog 类的方法 \_\_init\_\_()。我们将通过实参向 Dog() 传递名字和年龄；self 会自动传递，因此我们不需要传递它。每当我们根据 Dog 类创建实例时，都只需给最后两个形参（name 和 age ）提供值。

1『这边的 self 类似于 JS 里的 this。』

❹处定义的两个变量都有前缀 self。以 self 为前缀的变量都可供类中的所有方法使用，我们还可以通过类的任何实例来访问这些变量。self.name = name 获取存储在形参 name 中的值，并将其存储到变量 name 中，然后该变量被关联到当前创建的实例。self.age = age 的作用与此类似。像这样可通过实例访问的变量称为属性。

Dog 类还定义了另外两个方法：sit() 和 `roll_over()`（见❺）。由于这些方法不需要额外的信息，如名字或年龄，因此它们只有一个形参 self。我们后面将创建的实例能够访问这些方法，换句话说，它们都会蹲下和打滚。当前，sit() 和 `roll_over()` 所做的有限，它们只是打印一条消息，指出小狗正蹲下或打滚。但可以扩展这些方法以模拟实际情况：如果这个类包含在一个计算机游戏中，这些方法将包含创建小狗蹲下和打滚动画效果的代码。如果这个类是用于控制机器狗的，这些方法将引导机器狗做出蹲下和打滚的动作。

```py
class Dog():
--snip--

❶ my_dog = Dog('willie', 6)
❷ print("My dog's name is " + my_dog.name.title() + ".")
❸ print("My dog is " + str(my_dog.age) + " years old.")
```

这里使用的是前一个示例中编写的 Dog 类。在 ❶ 处，我们让 Python 创建一条名字为 'willie' 、年龄为 6 的小狗。遇到这行代码时，Python 使用实参 'willie' 和 6 调用 Dog 类中的方法 \_\_init\_\_()。方法 \_\_init\_\_() 创建一个表示特定小狗的示例，并使用我们提供的值来设置属性 name 和 age。方法 \_\_init\_\_() 并未显式地包含 return 语句，但 Python 自动返回一个表示这条小狗的实例。我们将这个实例存储在变量 my_dog 中。在这里，命名约定很有用：我们通常可以认为首字母大写的名称（如 Dog ）指的是类，而小写的名称（如 my_dog ）指的是根据类创建的实例。

### 9.2 使用类和实例

```py
class Car():

def __init__(self, make, model, year):
"""初始化描述汽车的属性"""
self.make = make
self.model = model
self.year = year
❶ self.odometer_reading = 0

def get_descriptive_name(self):
"""返回整洁的描述性信息"""
long_name = str(self.year) + ' ' + self.make + ' ' + self.model
return long_name.title()

❷ def read_odometer(self):
"""打印一条指出汽车里程的消息"""
print("This car has " + str(self.odometer_reading) + " miles on it.")

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())
my_new_car.read_odometer()
```

现在，当 Python 调用方法 \_\_init\_\_() 来创建新实例时，将像前一个示例一样以属性的方式存储制造商、型号和生产年份。接下来，Python 将创建一个名为 odometer\_reading 的属性，并将其初始值设置为 0（见❶）。在 ❷ 处，我们还定义了一个名为 read\_odometer() 的方法，它让你能够轻松地获悉汽车的里程。

你可以使用类来模拟现实世界中的很多情景。类编写好后，你的大部分时间都将花在使用根据类创建的实例上。你需要执行的一个重要任务是修改实例的属性。你可以直接修改实例的属性，也可以编写方法以特定的方式进行修改。类中的每个属性都必须有初始值，哪怕这个值是 0 或空字符串。在有些情况下，如设置默认值时，在方法 \_\_init\_\_() 内指定这种初始值是可行的；如果你对某个属性这样做了，就无需包含为它提供初始值的形参。

可以以三种不同的方式修改属性的值：

1、直接通过实例进行修改。

```py
class Car():
--snip--

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())
❶ my_new_car.odometer_reading = 23
my_new_car.read_odometer()
```

2、通过方法进行设置。

```py
class Car():
--snip--

❶ def update_odometer(self, mileage):
    """将里程表读数设置为指定的值"""
    self.odometer_reading = mileage

my_new_car = Car('audi', 'a4', 2016)
print(my_new_car.get_descriptive_name())
❷ my_new_car.update_odometer(23)
my_new_car.read_odometer()
```

可对方法 update_odometer() 进行扩展，使其在修改里程表读数时做些额外的工作。下面来添加一些逻辑，禁止任何人将里程表读数往回调：

```py
class Car():
--snip--

def update_odometer(self, mileage):
    """
    将里程表读数设置为指定的值
    禁止将里程表读数往回调
    """
    ❶ if mileage >= self.odometer_reading:
        self.odometer_reading = mileage
    else:
        ❷ print("You can't roll back an odometer!")
```

3、通过方法对属性的值进行递增。

有时候需要将属性值递增特定的量，而不是将其设置为全新的值。假设我们购买了一辆二手车，且从购买到登记期间增加了 100 英里的里程，下面的方法让我们能够传递这个增量，并相应地增加里程表读数：

```py
class Car():
--snip--

    def update_odometer(self, mileage):
    --snip--
    
    ❶ def increment_odometer(self, miles):
        """将里程表读数增加指定的量"""
        self.odometer_reading += miles

❷ my_used_car = Car('subaru', 'outback', 2013)
print(my_used_car.get_descriptive_name())
❸ my_used_car.update_odometer(23500)
my_used_car.read_odometer()
❹ my_used_car.increment_odometer(100)
my_used_car.read_odometer()
```

### 9.3 继承

编写类时，并非总是要从空白开始。如果你要编写的类是另一个现成类的特殊版本，可使用继承。一个类继承另一个类时，它将自动获得另一个类的所有属性和方法；原有的类称为父类，而新类称为子类。子类继承了其父类的所有属性和方法，同时还可以定义自己的属性和方法。

```py
❶ class Car():
"""一次模拟汽车的简单尝试"""

    def __init__(self, make, model, year):
    self.make = make
    self.model = model
    self.year = year
    self.odometer_reading = 0
    
    def get_descriptive_name(self):
        long_name = str(self.year) + ' ' + self.make + ' ' + self.model
        return long_name.title()
    
    def read_odometer(self):
        print("This car has " + str(self.odometer_reading) + " miles on it.")
    
    def update_odometer(self, mileage):
        if mileage >= self.odometer_reading:
            self.odometer_reading = mileage
        else:
         print("You can't roll back an odometer!")
    
    def increment_odometer(self, miles):
        self.odometer_reading += miles

❷ class ElectricCar(Car):
    """电动汽车的独特之处"""
    ❸ def __init__(self, make, model, year):
        """初始化父类的属性"""
        ❹ super().__init__(make, model, year)

❺ my_tesla = ElectricCar('tesla', 'model s', 2016)
print(my_tesla.get_descriptive_name())
```

首先是 Car 类的代码（见❶）。创建子类时，父类必须包含在当前文件中，且位于子类前面。在 ❷ 处，我们定义了子类 ElectricCar。定义子类时，必须在括号内指定父类的名称。方法 \_\_init\_\_() 接受创建 Car 实例所需的信息（见❸）。

❹处的 super() 是一个特殊函数，帮助 Python 将父类和子类关联起来。这行代码让 Python调用 ElectricCar 的父类的方法 \_\_init\_\_()，让 ElectricCar 实例包含父类的所有属性。父类也称为超类 （superclass），名称 super 因此而得名。

为测试继承是否能够正确地发挥作用，我们尝试创建一辆电动汽车，但提供的信息与创建普通汽车时相同。在 ❺ 处，我们创建 ElectricCar 类的一个实例，并将其存储在变量 my_tesla 中。这行代码调用 ElectricCar 类中定义的方法 \_\_init\_\_()，后者让 Python 调用父类 Car 中定义的方法 \_\_init\_\_()。我们提供了实参 'tesla' 、'model s' 和 2016。

让一个类继承另一个类后，可添加区分子类和父类所需的新属性和方法。下面来添加一个电动汽车特有的属性（电瓶），以及一个描述该属性的方法。我们将存储电瓶容量，并编写一个打印电瓶描述的方法。

对于 ElectricCar 类的特殊化程度没有任何限制。模拟电动汽车时，你可以根据所需的准确程度添加任意数量的属性和方法。如果一个属性或方法是任何汽车都有的，而不是电动汽车特有的，就应将其加入到 Car 类而不是 ElectricCar 类中。这样，使用 Car 类的人将获得相应的功能，而 ElectricCar 类只包含处理电动汽车特有属性和行为的代码。

对于父类的方法，只要它不符合子类模拟的实物的行为，都可对其进行重写。为此，可在子类中定义一个这样的方法，即它与要重写的父类方法同名。这样，Python 将不会考虑这个父类方法，而只关注你在子类中定义的相应方法。假设 Car 类有一个名为 fill_gas_tank() 的方法，它对全电动汽车来说毫无意义，因此你可能想重写它。下面演示了一种重写方式。现在，如果有人对电动汽车调用方法 fill_gas_tank()，Python 将忽略 Car 类中的方法 fill_gas_tank()，转而运行上述代码。使用继承时，可让子类保留从父类那里继承而来的精华，并剔除不需要的糟粕。

1『可以用子类里的方法覆盖父类里同一个方法。』

使用代码模拟实物时，你可能会发现自己给类添加的细节越来越多：属性和方法清单以及文件都越来越长。在这种情况下，可能需要将类的一部分作为一个独立的类提取出来。你可以将大型类拆分成多个协同工作的小类。例如，不断给 ElectricCar 类添加细节时，我们可能会发现其中包含很多专门针对汽车电瓶的属性和方法。在这种情况下，我们可将这些属性和方法提取出来，放到另一个名为 Battery 的类中，并将一个 Battery 实例用作 ElectricCar 类的一个属性。

模拟较复杂的物件（如电动汽车）时，需要解决一些有趣的问题。续航里程是电瓶的属性还是汽车的属性呢？如果我们只需描述一辆汽车，那么将方法 get_range() 放在 Battery 类中也许是合适的；但如果要描述一家汽车制造商的整个产品线，也许应该将方法 get_range() 移到 ElectricCar 类中。在这种情况下，get_range() 依然根据电瓶容量来确定续航里程，但报告的是一款汽车的续航里程。我们也可以这样做：将方法 get_range() 还留在 Battery 类中，但向它传递一个参数，如 car_model ；在这种情况下，方法 get_range() 将根据电瓶容量和汽车型号报告续航里程。

这让你进入了程序员的另一个境界：解决上述问题时，你从较高的逻辑层面（而不是语法层面）考虑；你考虑的不是 Python，而是如何使用代码来表示实物。到达这种境界后，你经常会发现，现实世界的建模方法并没有对错之分。有些方法的效率更高，但要找出效率最高的表示法，需要经过一定的实践。只要代码像你希望的那样运行，就说明你做得很好！即便你发现自己不得不多次尝试使用不同的方法来重写类，也不必气馁；要编写出高效、准确的代码，都得经过这样的过程。

### 9.4 导入类

随着你不断地给类添加功能，文件可能变得很长，即便你妥善地使用了继承亦如此。为遵循 Python 的总体理念，应让文件尽可能整洁。为在这方面提供帮助，Python 允许你将类存储在模块中，然后在主程序中导入所需的模块。

在 ❶ 处，我们包含了一个模块级文档字符串，对该模块的内容做了简要的描述。你应为自己创建的每个模块都编写文档字符串。

1『三个双引号的即文档字符串。』

导入类是一种有效的编程方式。如果在这个程序中包含了整个 Car 类，它该有多长呀！通过将这个类移到一个模块中，并导入该模块，你依然可以使用其所有功能，但主程序文件变得整洁而易于阅读了。这还能让你将大部分逻辑存储在独立的文件中；确定类像你希望的那样工作后，你就可以不管这些文件，而专注于主程序的高级逻辑了。

虽然同一个模块中的类之间应存在某种相关性，但可根据需要在一个模块中存储任意数量的类。类 Battery 和 ElectricCar 都可帮助模拟汽车，因此下面将它们都加入模块 car.py 中。

可根据需要在程序文件中导入任意数量的类。如果我们要在同一个程序中创建普通汽车和电动汽车，就需要将 Car 和 ElectricCar 类都导入。

```py
❶ from car import Car, ElectricCar
❷ my_beetle = Car('volkswagen', 'beetle', 2016)
print(my_beetle.get_descriptive_name())
❸ my_tesla = ElectricCar('tesla', 'roadster', 2016)
print(my_tesla.get_descriptive_name())
```

在 ❶ 处从一个模块中导入多个类时，用逗号分隔了各个类。导入必要的类后，就可根据需要创建每个类的任意数量的实例。你还可以导入整个模块，再使用句点表示法访问需要的类。这种导入方法很简单，代码也易于阅读。由于创建类实例的代码都包含模块名，因此不会与当前文件使用的任何名称发生冲突。

1『类做成模块然后通过导入使用，如同方法做成模块。』

要导入模块中的每个类，可使用下面的语法：

```py
from module_name import *
```

不推荐使用上面的导入方式，其原因有二。

首先，如果只要看一下文件开头的 import 语句，就能清楚地知道程序使用了哪些类，将大有裨益；但这种导入方式没有明确地指出你使用了模块中的哪些类。这种导入方式还可能引发名称方面的困惑。如果你不小心导入了一个与程序文件中其他东西同名的类，将引发难以诊断的错误。这里之所以介绍这种导入方式，是因为虽然不推荐使用这种方式，但你可能会在别人编写的代码中见到它。

需要从一个模块中导入很多类时，最好导入整个模块，并使用 module_name.class_name 语法来访问类。这样做时，虽然文件开头并没有列出用到的所有类，但你清楚地知道在程序的哪些地方使用了导入的模块；你还避免了导入模块中的每个类可能引发的名称冲突。

有时候，需要将类分散到多个模块中，以免模块太大，或在同一个模块中存储不相关的类。将类存储在多个模块中时，你可能会发现一个模块中的类依赖于另一个模块中的类。在这种情况下，可在前一个模块中导入必要的类。例如，下面将 Car 类存储在一个模块中，并将 ElectricCar 和 Battery 类存储在另一个模块中。我们将第二个模块命名为 electric_car.py，并将 Battery 和 ElectricCar 类复制到这个模块中。ElectricCar 类需要访问其父类 Car，因此在 ❶ 处，我们直接将 Car 类导入该模块中。如果我们忘记了这行代码，Python 将在我们试图创建 ElectricCar 实例时引发错误。我们还需要更新模块 car，使其包含Car 类。

自定义工作流程。正如你看到的，在组织大型项目的代码方面，Python 提供了很多选项。熟悉所有这些选项很重要，这样你才能确定哪种项目组织方式是最佳的，并能理解别人开发的项目。

一开始应让代码结构尽可能简单。先尽可能在一个文件中完成所有的工作，确定一切都能正确运行后，再将类移到独立的模块中。如果你喜欢模块和文件的交互方式，可在项目开始时就尝试将类存储到模块中。先找出让你能够编写出可行代码的方式，再尝试让代码更为组织有序。

1『又见这种思维：先做出来，优化的事情后面再做。』

### 9.5 Python标准库

Python 标准库是一组模块，安装的 Python 都包含它。你现在对类的工作原理已有大致的了解，可以开始使用其他程序员编写好的模块了。可使用标准库中的任何函数和类，为此只需在程序开头包含一条简单的 import 语句。下面来看模块 collections 中的一个类 —— OrderedDict。

字典让你能够将信息关联起来，但它们不记录你添加「键-值」对的顺序。要创建字典并记录其中的「键-值」对的添加顺序，可使用模块 collections 中的 OrderedDict 类。OrderedDict 实例的行为几乎与字典相同，区别只在于记录了「键-值」对的添加顺序。

1『以后应该会有用到它的场景，哈哈。（2020-08-30）』

```py
❶ from collections import OrderedDict
❷ favorite_languages = OrderedDict()
❸ favorite_languages['jen'] = 'python'
favorite_languages['sarah'] = 'c'
favorite_languages['edward'] = 'ruby'
favorite_languages['phil'] = 'python'
❹ for name, language in favorite_languages.items():
print(name.title() + "'s favorite language is " +
language.title() + ".")
```

我们首先从模块 collections 中导入了 OrderedDict 类（见❶）。在 ❷ 处，我们创建了 OrderedDict 类的一个实例，并将其存储到 favorite_languages 中。请注意，这里没有使用花括号，而是调用 OrderedDict() 来创建一个空的有序字典，并将其存储在 favorite_languages 中。接下来，我们以每次一对的方式添加「名字-语言」对（见❸）。在 ❹ 处，我们遍历 favorite_languages，但知道将以添加的顺序获取调查结果。

1『注意，语句 ❸ 增加字典元素时，是用的方括号：favorite_language['dalong'] = 'python'，跟列表的语法一样，可以理解为加强版的列表。』

这是一个很不错的类，它兼具列表和字典的主要优点（在将信息关联起来的同时保留原来的顺序）。等你开始对关心的现实情形建模时，可能会发现有序字典正好能够满足需求。随着你对标准库的了解越来越深入，将熟悉大量可帮助你处理常见情形的模块。

Python Module of the Week ：要了解 Python 标准库，一个很不错的资源是网站 Python Module of the Week。请访问 http://pymotw.com/ 并查看其中的目录，在其中找一个你感兴趣的模块进行探索，或阅读模块 collections 和 random 的文档。

3『 [Python 3 Module of the Week — PyMOTW 3](https://pymotw.com/3/)』

### 9.6 类编码风格

你必须熟悉有些与类相关的编码风格问题，在你编写的程序较复杂时尤其如此。

1、类名应采用「驼峰命名法」，即将类名中的每个单词的首字母都大写，而不使用下划线。实例名和模块名都采用小写格式，并在单词之间加上下划线。

2、对于每个类，都应紧跟在类定义后面包含一个文档字符串。这种文档字符串简要地描述类的功能，并遵循编写函数的文档字符串时采用的格式约定。每个模块也都应包含一个文档字符串，对其中的类可用于做什么进行描述。

3、可使用空行来组织代码，但不要滥用。在类中，可使用一个空行来分隔方法；而在模块中，可使用两个空行来分隔类。

4、需要同时导入标准库中的模块和你编写的模块时，先编写导入标准库模块的 import 语句，再添加一个空行，然后编写导入你自己编写的模块的 import 语句。在包含多条 import 语句的程序中，这种做法让人更容易明白程序使用的各个模块都来自何方。

1-2『以上是 python 类的编码风格，一定要牢记，并添加进主题卡中。』

## 1001. 文件和异常

在本章中，你学习了：1）如何使用文件；2）如何一次性读取整个文件，以及如何以每次一行的方式读取文件的内容；3）如何写入文件，以及如何将文本附加到文件末尾；4）什么是异常以及如何处理程序可能引发的异常；5）如何存储 Python 数据结构，以保存用户提供的信息，避免用户每次运行程序时都需要重新提供。

在本章中，你将学习处理文件，让程序能够快速地分析大量的数据；你将学习错误处理，避免程序在面对意外情形时崩溃；你将学习异常，它们是 Python 创建的特殊对象，用于管理程序运行时出现的错误；你还将学习模块 json，它让你能够保存用户数据，以免在程序停止运行后丢失。

学习处理文件和保存数据可让你的程序使用起来更容易：用户将能够选择输入什么样的数据，以及在什么时候输入；用户使用你的程序做一些工作后，可将程序关闭，以后再接着往下做。学习处理异常可帮助你应对文件不存在的情形，以及处理其他可能导致程序崩溃的问题。这让你的程序在面对错误的数据时更健壮 —— 不管这些错误数据源自无意的错误，还是源自破坏程序的恶意企图。你在本章学习的技能可提高程序的适用性、可用性和稳定性。

### 10.1 从文件中读取数据

文本文件可存储的数据量多得难以置信：天气数据、交通数据、社会经济数据、文学作品等。每当需要分析或修改存储在文件中的信息时，读取文件都很有用，对数据分析应用程序来说尤其如此。例如，你可以编写一个这样的程序：读取一个文本文件的内容，重新设置这些数据的格式并将其写入文件，让浏览器能够显示这些内容。

要使用文本文件中的信息，首先需要将信息读取到内存中。为此，你可以一次性读取文件的全部内容，也可以以每次一行的方式逐步读取。

```py
with open('pi_digits.txt') as file_object:
    contents = file_object.read()
    print(contents)
```

在这个程序中，第 1 行代码做了大量的工作。我们先来看看函数 open()。要以任何方式使用文件 —— 哪怕仅仅是打印其内容，都得先打开文件，这样才能访问它。函数 open() 接受一个参数：要打开的文件的名称。Python 在当前执行的文件所在的目录中查找指定的文件。在这个示例中，当前运行的是 file_reader.py，因此 Python 在 file_reader.py 所在的目录中查找 pi_digits.txt。函数 open() 返回一个表示文件的对象。在这里，open('pi_digits.txt') 返回一个表示文件 pi_digits.txt 的对象；Python 将这个对象存储在我们将在后面使用的变量中。

关键字 with 在不再需要访问文件后将其关闭。在这个程序中，注意到我们调用了open()，但没有调用 close() ；你也可以调用 open() 和 close() 来打开和关闭文件，但这样做时，如果程序存在 bug，导致 close() 语句未执行，文件将不会关闭。这看似微不足道，但未妥善地关闭文件可能会导致数据丢失或受损。如果在程序中过早地调用 close()，你会发现需要使用文件时它已关闭 （无法访问），这会导致更多的错误。并非在任何情况下都能轻松确定关闭文件的恰当时机，但通过使用前面所示的结构，可让 Python去确定：你只管打开文件，并在需要时使用它，Python 自会在合适的时候自动将其关闭。

有了表示 pi_digits.txt 的文件对象后，我们使用方法 read() （前述程序的第 2 行）读取这个文件的全部内容，并将其作为一个长长的字符串存储在变量 contents 中。这样，通过打印 contents 的值，就可将这个文本文件的全部内容显示出来。

当你将类似 pi_digits.txt 这样的简单文件名传递给函数 open() 时，Python 将在当前执行的文件（即 .py 程序文件）所在的目录中查找文件。

根据你组织文件的方式，有时可能要打开不在程序文件所属目录中的文件。例如，你可能将程序文件存储在了文件夹 python_work 中，而在文件夹 python_work 中，有一个名为 text_files 的文件夹，用于存储程序文件操作的文本文件。虽然文件夹 text_files 包含在文件夹 python_work 中，但仅向 open() 传递位于该文件夹中的文件的名称也不可行，因为 Python 只在文件夹 python_work 中查找，而不会在其子文件夹 text_files 中查找。要让 Python 打开不与程序文件位于同一个目录中的文件，需要提供文件路径，它让 Python 到系统的特定位置去查找。

通过使用绝对路径，可读取系统任何地方的文件。就目前而言，最简单的做法是，要么将数据文件存储在程序文件所在的目录，要么将其存储在程序文件所在目录下的一个文件夹（如 text_files）中。

```py
❶ filename = 'pi_digits.txt'
❷ with open(filename) as file_object:
	❸ for line in file_object:
	print(line)
```

在 ❶ 处，我们将要读取的文件的名称存储在变量 filename 中，这是使用文件时一种常见的做法。由于变量 filename 表示的并非实际文件 —— 它只是一个让 Python 知道到哪里去查找文件的字符串，因此可轻松地将 'pi_digits.txt' 替换为你要使用的另一个文件的名称。调用 open() 后，将一个表示文件及其内容的对象存储到了变量 file_object 中（见❷）。这里也使用了关键字 with，让 Python 负责妥善地打开和关闭文件。为查看文件的内容，我们通过对文件对象执行循环来遍历文件中的每一行（见❸）。

使用关键字 with 时，open() 返回的文件对象只在 with 代码块内可用。如果要在 with 代码块外访问文件的内容，可在 with 代码块内将文件的各行存储在一个列表中，并在 with 代码块外使用该列表：你可以立即处理文件的各个部分，也可推迟到程序后面再处理。

```py
filename = 'pi_digits.txt'
with open(filename) as file_object:
    ❶ lines = file_object.readlines()
❷ for line in lines:
    print(line.rstrip())
```

❶处的方法 readlines() 从文件中读取每一行，并将其存储在一个列表中；接下来，该列表被存储到变量 lines 中；在 with 代码块外，我们依然可以使用这个变量。在 ❷ 处，我们使用一个简单的 for 循环来打印 lines 中的各行。由于列表 lines 的每个元素都对应于文件中的一行，因此输出与文件内容完全一致。

在变量 pi_string 存储的字符串中，包含原来位于每行左边的空格，为删除这些空格，可使用 strip() 而不是 rstrip()。

可使用方法 replace() 将字符串中的特定单词都替换为另一个单词。下面是一个简单的示例，演示了如何将句子中的 'dog' 替换为'cat' ：

### 10.2 写入文件

保存数据的最简单的方式之一是将其写入到文件中。通过将输出写入文件，即便关闭包含程序输出的终端窗口，这些输出也依然存在：你可以在程序结束运行后查看这些输出，可与别人分享输出文件，还可编写程序来将这些输出读取到内存中并进行处理。

```py
filename = 'programming.txt'
❶ with open(filename, 'w') as file_object:
	❷ file_object.write("I love programming.")
```

在这个示例中，调用 open() 时提供了两个实参（见❶）。第一个实参也是要打开的文件的名称；第二个实参（'w' ）告诉 Python，我们要以写入模式打开这个文件。打开文件时，可指定读取模式 （'r' ）、写入模式 （'w' ）、附加模式 （'a' ）或让你能够读取和写入文件的模式（'r+' ）。如果你省略了模式实参，Python 将以默认的只读模式打开文件。

如果你要写入的文件不存在，函数 open() 将自动创建它。然而，以写入（'w' ）模式打开文件时千万要小心，因为如果指定的文件已经存在，Python 将在返回文件对象前清空该文件。

在 ❷ 处，我们使用文件对象的方法 write() 将一个字符串写入文件。这个程序没有终端输出，但如果你打开文件 programming.txt，将看到其中包含如下一行内容：

像显示到终端的输出一样，还可以使用空格、制表符和空行来设置这些输出的格式。

如果你要给文件添加内容，而不是覆盖原有的内容，可以附加模式打开文件。你以附加模式打开文件时，Python 不会在返回文件对象前清空文件，而你写入到文件的行都将添加到文件末尾。如果指定的文件不存在，Python 将为你创建一个空文件。

1『默认写入模式是清空已有的数据，传入参数 'a' 后采用附加模式不会清空。由此联想到，数据写入 excel 时，是不是写入函数 save() 里除了文件参数，额外再传入一个参数即可实现不清空原始数据。有待验证。回复：数据流里实现的是直接读取已有的 excel 文件作为模板对象，再往里写数据。（2020-08-30）』

### 10.3 异常

Python 使用被称为异常的特殊对象来管理程序执行期间发生的错误。每当发生让 Python 不知所措的错误时，它都会创建一个异常对象。如果你编写了处理该异常的代码，程序将继续运行；如果你未对异常进行处理，程序将停止，并显示一个 traceback，其中包含有关异常的报告。

异常是使用 try-except 代码块处理的。try-except 代码块让 Python 执行指定的操作，同时告诉 Python 发生异常时怎么办。使用了 try-except 代码块时，即便出现异常，程序也将继续运行：显示你编写的友好的错误消息，而不是令用户迷惑的 traceback。

1『

在做设备表程序时得到一个经验：try 代码放在主函数里，不要放在函数体里。放函数体里的话相当于措施发生时重复处理了 2 次，反而过滤掉了错误，任何错误都显示不出来。

```py
try:
    df = getdata(path)
    totaldf = pd.concat([totaldf,df], ignore_index=True)
    # 每个设备表单独生成一张 csv 表单
    # df.to_csv(filename+'.csv', index=False, header=False)
    print(filename+': OK!')
except Exception as e:
    pass
    print(filename+': Do not get it!')
```

』

```py
try:
	print(5/0)
except ZeroDivisionError:
	print("You can't divide by zero!")
```

在上述 traceback 中，❶ 处指出的错误 ZeroDivisionError 是一个异常对象。Python 无法按你的要求做时，就会创建这种对象。在这种情况下，Python 将停止运行程序，并指出引发了哪种异常，而我们可根据这些信息对程序进行修改。下面我们将告诉 Python，发生这种错误时怎么办；这样，如果再次发生这样的错误，我们就有备无患了。

当你认为可能发生了错误时，可编写一个 try-except 代码块来处理可能引发的异常。你让 Python 尝试运行一些代码，并告诉它如果这些代码引发了指定的异常，该怎么办。我们将导致错误的代码行 print(5/0) 放在了一个 try 代码块中。如果 try 代码块中的代码运行起来没有问题，Python 将跳过 except 代码块；如果 try 代码块中的代码导致了错误，Python 将查找这样的 except  代码块，并运行其中的代码，即其中指定的错误与引发的错误相同。

在这个示例中，try 代码块中的代码引发了 ZeroDivisionError 异常，因此 Python 指出了该如何解决问题的 except 代码块，并运行其中的代码。这样，用户看到的是一条友好的错误消息，而不是 traceback：You can't divide by zero!

发生错误时，如果程序还有工作没有完成，妥善地处理错误就尤其重要。这种情况经常会出现在要求用户提供输入的程序中；如果程序能够妥善地处理无效输入，就能再提示用户提供有效输入，而不至于崩溃。

1『 bug 不可能完全消除，学会「管理」bug 才是正道。』

程序崩溃可不好，但让用户看到 traceback 也不是好主意。不懂技术的用户会被它们搞糊涂，而且如果用户怀有恶意，他会通过 traceback 获悉你不希望他知道的信息。例如，他将知道你的程序文件的名称，还将看到部分不能正确运行的代码。有时候，训练有素的攻击者可根据这些信息判断出可对你的代码发起什么样的攻击。

通过将可能引发错误的代码放在 try-except 代码块中，可提高这个程序抵御错误的能力。错误是执行除法运算的代码行导致的，因此我们需要将它放到 try-except 代码块中。这个示例还包含一个 else 代码块；依赖于 try 代码块成功执行的代码都应放到 else 代码块中：

```py
print("Give me two numbers, and I'll divide them.")
print("Enter 'q' to quit.")

while True:
    first_number = input("\nFirst number: ")
    if first_number == 'q':
        break
    second_number = input("Second number: ")
    ❶ try:
        answer = int(first_number) / int(second_number)
    ❷ except ZeroDivisionError:
        print("You can't divide by 0!")
    ❸ else:
        print(answer)
```

try-except-else 代码块的工作原理大致如下：Python 尝试执行 try 代码块中的代码；只有可能引发异常的代码才需要放在 try 语句中。有时候，有一些仅在 try 代码块成功执行时才需要运行的代码；这些代码应放在 else 代码块中。except 代码块告诉 Python，如果它尝试运行 try 代码块中的代码时引发了指定的异常，该怎么办。通过预测可能发生错误的代码，可编写健壮的程序，它们即便面临无效数据或缺少资源，也能继续运行，从而能够抵御无意的用户错误和恶意的攻击。

```py
try:
with open(filename) as f_obj:
	contents = f_obj.read()
except FileNotFoundError:
	msg = "Sorry, the file " + filename + " does not exist."
	print(msg)
```

处理 FileNotFoundError 异常。使用文件时，一种常见的问题是找不到文件：你要查找的文件可能在其他地方、文件名可能不正确或者这个文件根本就不存在。对于所有这些情形，都可使用 try-except 代码块以直观的方式进行处理。

下面来提取童话 Alice in Wonderland 的文本，并尝试计算它包含多少个单词。我们将使用方法 split()，它根据一个字符串创建一个单词列表。下面是对只包含童话名「Alice in Wonderland」的字符串调用方法 split() 的结果：

1『这里开始讲分析文本的知识了。』

方法 split() 以空格为分隔符将字符串分拆成多个部分，并将这些部分都存储到一个列表中。结果是一个包含字符串中所有单词的列表，虽然有些单词可能包含标点。为计算 Alice in Wonderland 包含多少个单词，我们将对整篇小说调用 split()，再计算得到的列表包含多少个元素，从而确定整篇童话大致包含多少个单词：

```py
filename = 'alice.txt'
try:
with open(filename) as f_obj:
	contents = f_obj.read()
except FileNotFoundError:
	msg = "Sorry, the file " + filename + " does not exist."
	print(msg)
else:
# 计算文件大致包含多少个单词
❶ words = contents.split()
❷ num_words = len(words)
❸ print("The file " + filename + " has about " + str(num_words) + " words.")
```

我们把文件 alice.txt 移到了正确的目录中，让 try 代码块能够成功地执行。在 ❶ 处，我们对变量 contents （它现在是一个长长的字符串，包含童话 Alice in Wonderland 的全部文本）调用方法 split()，以生成一个列表，其中包含这部童话中的所有单词。当我们使用 len() 来确定这个列表的长度时，就知道了原始字符串大致包含多少个单词（见❷）。在 ❸ 处，我们打印一条消息，指出文件包含多少个单词。这些代码都放在 else 代码块中，因为仅当 try 代码块成功执行时才执行它们。输出指出了文件 alice.txt 包含多少个单词。

使用多个文件：

```py
def count_words(filename):
	❶ """计算一个文件大致包含多少个单词"""
	try:
	with open(filename) as f_obj:
		contents = f_obj.read()
	except FileNotFoundError:
		msg = "Sorry, the file " + filename + " does not exist."
		print(msg)
	else:
	# 计算文件大致包含多少个单词
	words = contents.split()
	num_words = len(words)
	print("The file " + filename + " has about " + str(num_words) + " words.")
filename = 'alice.txt'
count_words(filename)
```

这些代码大都与原来一样，我们只是将它们移到了函数 count_words() 中，并增加了缩进量。修改程序的同时更新注释是个不错的习惯，因此我们将注释改成了文档字符串，并稍微调整了一下措辞（见❶）。现在可以编写一个简单的循环，计算要分析的任何文本包含多少个单词了。为此，我们将要分析的文件的名称存储在一个列表中，然后对列表中的每个文件都调用 count_words()。我们将尝试计算 Alice in Wonderland 、Siddhartha 、Moby Dick 和 Little Women 分别包含多少个单词，它们都不受版权限制。我故意没有将 siddhartha.txt 放到 word_count.py 所在的目录中，让你能够看到这个程序在文件不存在时处理得有多出色：

```py
def count_words(filename):
--snip--

filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
    count_words(filename)
```

在这个示例中，使用 try-except 代码块提供了两个重要的优点：1）避免让用户看到 traceback；2）让程序能够继续分析能够找到的其他文件。如果不捕获因找不到 siddhartha.txt 而引发的 FileNotFoundError 异常，用户将看到完整的 traceback，而程序将在尝试分析 Siddhartha 后停止运行 —— 根本不分析 Moby Dick 和 Little Women。

在前一个示例中，我们告诉用户有一个文件找不到。但并非每次捕获到异常时都需要告诉用户，有时候你希望程序在发生异常时一声不吭，就像什么都没有发生一样继续运行。要让程序在失败时一声不吭，可像通常那样编写 try 代码块，但在 except 代码块中明确地告诉 Python 什么都不要做。Python 有一个 pass 语句，可在代码块中使用它来让 Python 什么都不要做：

```py
def count_words(filename):
	"""计算一个文件大致包含多少个单词"""
	try:
		--snip--
	except FileNotFoundError:
	   ❶ pass
	else:
		--snip--

filenames = ['alice.txt', 'siddhartha.txt', 'moby_dick.txt', 'little_women.txt']
for filename in filenames:
    count_words(filename)
```

1『之前看爬虫书里的作者就是这么处理异常的，失败时一声不吭，哈哈。（2020-08-30）』

pass 语句还充当了占位符，它提醒你在程序的某个地方什么都没有做，并且以后也许要在这里做些什么。例如，在这个程序中，我们可能决定将找不到的文件的名称写入到文件 missing_files.txt 中。用户看不到这个文件，但我们可以读取这个文件，进而处理所有文件找不到的问题。

在什么情况下该向用户报告错误？在什么情况下又应该在失败时一声不吭呢？如果用户知道要分析哪些文件，他们可能希望在有文件没有分析时出现一条消息，将其中的原因告诉他们。如果用户只想看到结果，而并不知道要分析哪些文件，可能就无需在有些文件不存在时告知他们。向用户显示他不想看到的信息可能会降低程序的可用性。Python 的错误处理结构让你能够细致地控制与用户分享错误信息的程度，要分享多少信息由你决定。

编写得很好且经过详尽测试的代码不容易出现内部错误，如语法或逻辑错误，但只要程序依赖于外部因素，如用户输入、存在指定的文件、有网络链接，就有可能出现异常。凭借经验可判断该在程序的什么地方包含异常处理块，以及出现错误时该向用户提供多少相关的信息。

### 10.4 存储数据

很多程序都要求用户输入某种信息，如让用户存储游戏首选项或提供要可视化的数据。不管专注的是什么，程序都把用户提供的信息存储在列表和字典等数据结构中。用户关闭程序时，你几乎总是要保存他们提供的信息；一种简单的方式是使用模块 json 来存储数据。

模块 json 让你能够将简单的 Python 数据结构转储到文件中，并在程序再次运行时加载该文件中的数据。你还可以使用 json 在 Python 程序之间分享数据。更重要的是，JSON 数据格式并非 Python 专用的，这让你能够将以 JSON 格式存储的数据与使用其他编程语言的人分享。这是一种轻便格式，很有用，也易于学习。

JSON（JavaScript Object Notation）格式最初是为 JavaScript 开发的，但随后成了一种常见格式，被包括 Python 在内的众多语言采用。

我们来编写一个存储一组数字的简短程序，再编写一个将这些数字读取到内存中的程序。第一个程序将使用 json.dump() 来存储这组数字，而第二个程序将使用 json.load()。

1『 import json，json 是个标准模块。』

函数 json.dump() 接受两个实参：要存储的数据以及可用于存储数据的文件对象。下面演示了如何使用 json.dump() 来存储数字列表：

```py
import json

numbers = [2, 3, 5, 7, 11, 13]
❶ filename = 'numbers.json'
❷ with open(filename, 'w') as f_obj:
	❸ json.dump(numbers, f_obj)
```

我们先导入模块 json，再创建一个数字列表。在 ❶ 处，我们指定了要将该数字列表存储到其中的文件的名称。通常使用文件扩展名 .json 来指出文件存储的数据为 JSON 格式。接下来，我们以写入模式打开这个文件，让 json 能够将数据写入其中（见❷）。在 ❸ 处，我们使用函数 json.dump() 将数字列表存储到文件 numbers.json 中。

下面再编写一个程序，使用 json.load() 将这个列表读取到内存中：

```py
import json

❶ filename = 'numbers.json'
❷ with open(filename) as f_obj:
	❸ numbers = json.load(f_obj)
print(numbers)
```

在 ❶ 处，我们确保读取的是前面写入的文件。这次我们以读取方式打开这个文件，因为 Python 只需读取这个文件（见❷）。在 ❸ 处，我们使用函数 json.load() 加载存储在 numbers.json 中的信息，并将其存储到变量 numbers 中。最后，我们打印恢复的数字列表。

保存和读取用户生成的数据。对于用户生成的数据，使用 json 保存它们大有裨益，因为如果不以某种方式进行存储，等程序停止运行时用户的信息将丢失。下面来看一个这样的例子：用户首次运行程序时被提示输入自己的名字，这样再次运行程序时就记住他了。

```py
import json

❶ username = input("What is your name? ")
filename = 'username.json'
with open(filename, 'w') as f_obj:
    ❷ json.dump(username, f_obj)
    ❸ print("We'll remember you when you come back, " + username + "!")
```

在 ❶ 处，我们提示输入用户名，并将其存储在一个变量中。接下来，我们调用 json.dump()，并将用户名和一个文件对象传递给它，从而将用户名存储到文件中（见❷）。然后，我们打印一条消息，指出我们存储了他输入的信息（见❸）：

我们需要将这两个程序合并到一个程序（remember_me.py）中。这个程序运行时，我们将尝试从文件 username.json 中获取用户名，因此我们首先编写一个尝试恢复用户名的 try 代码块。如果这个文件不存在，我们就在 except 代码块中提示用户输入用户名，并将其存储在 username.json中，以便程序再次运行时能够获取它：

```py
import json

# 如果以前存储了用户名，就加载它
# 否则，就提示用户输入用户名并存储它

filename = 'username.json'
try:
    ❶ with open(filename) as f_obj:
        ❷ username = json.load(f_obj)
❸ except FileNotFoundError:
    ❹ username = input("What is your name? ")
    ❺ with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
        print("We'll remember you when you come back, " + username + "!")
else:
    print("Welcome back, " + username + "!")
```

这里没有任何新代码，只是将前两个示例的代码合并到了一个程序中。在 ❶ 处，我们尝试打开文件 username.json。如果这个文件存在，就将其中的用户名读取到内存中（见❷），再执行 else 代码块，即打印一条欢迎用户回来的消息。用户首次运行这个程序时，文件 username.json 不存在，将引发 FileNotFoundError 异常（见❸），因此 Python 将执行  except 代码块：提示用户输入其用户名（见❹），再使用json.dump() 存储该用户名，并打印一句问候语（见❺）。无论执行的是 except 代码块还是 else 代码块，都将显示用户名和合适的问候语。

你经常会遇到这样的情况：代码能够正确地运行，但可做进一步的改进 —— 将代码划分为一系列完成具体工作的函数。这样的过程被称为重构。重构让代码更清晰、更易于理解、更容易扩展。

1『又见重构，哈哈。（2020-08-30）』

要重构 remember_me.py，可将其大部分逻辑放到一个或多个函数中。remember_me.py 的重点是问候用户，因此我们将其所有代码都放到一个名为 greet\_user() 的函数中：

```py
import json

def greet_user():
    ❶ """问候用户，并指出其名字"""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        username = input("What is your name? ")
        with open(filename, 'w') as f_obj:
            json.dump(username, f_obj)
            print("We'll remember you when you come back, " + username + "!")
    else:
        print("Welcome back, " + username + "!")
    
greet_user()
```

考虑到现在使用了一个函数，我们删除了注释，转而使用一个文档字符串来指出程序是做什么的（见❶）。这个程序更清晰些，但函数 greet\_user() 所做的不仅仅是问候用户，还在存储了用户名时获取它，而在没有存储用户名时提示用户输入一个。下面来重构 greet\_user()，让它不执行这么多任务。为此，我们首先将获取存储的用户名的代码移到另一个函数中：

```py
import json

def get_stored_username():
    ❶ """如果存储了用户名，就获取它"""
    filename = 'username.json'
    try:
        with open(filename) as f_obj:
            username = json.load(f_obj)
    except FileNotFoundError:
        ❷ return None
    else:
        return username

def greet_user():
    """问候用户，并指出其名字"""
    username = get_stored_username()
    ❸ if username:
        print("Welcome back, " + username + "!")
    else:
        username = input("What is your name? ")
    filename = 'username.json'
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
        print("We'll remember you when you come back, " + username + "!")

greet_user()
```

新增的函数 get\_stored\_username() 目标明确，❶ 处的文档字符串指出了这一点。如果存储了用户名，这个函数就获取并返回它；如果文件 username.json 不存在，这个函数就返回 None （见❷）。这是一种不错的做法：函数要么返回预期的值，要么返回 None ；这让我们能够使用函数的返回值做简单测试。在 ❸ 处，如果成功地获取了用户名，就打印一条欢迎用户回来的消息，否则就提示用户输入用户名。

我们还需将 greet\_user() 中的另一个代码块提取出来：将没有存储用户名时提示用户输入的代码放在一个独立的函数中：


```py
import json

def get_stored_username():
    """如果存储了用户名，就获取它"""
    --snip--

def get_new_username():
    """提示用户输入用户名"""
    username = input("What is your name? ")
    filename = 'username.json'
    with open(filename, 'w') as f_obj:
        json.dump(username, f_obj)
    return username

def greet_user():
    """问候用户，并指出其名字"""
    username = get_stored_username()
    if username:
        print("Welcome back, " + username + "!")
    else:
        username = get_new_username()
    print("We'll remember you when you come back, " + username + "!")

greet_user()
```

在 remember\_me.py 的这个最终版本中，每个函数都执行单一而清晰的任务。我们调用 greet\_user()，它打印一条合适的消息：要么欢迎老用户回来，要么问候新用户。为此，它首先调用 get\_stored\_username()，这个函数只负责获取存储的用户名（如果存储了的话），再在必要时调用 get\_new\_username()，这个函数只负责获取并存储新用户的用户名。要编写出清晰而易于维护和扩展的代码，这种划分工作必不可少。

2『上面的重构例子需要好好研读。（2020-08-30）』 —— 未完成

## 1101. 测试代码

在本章中，你学习了：如何使用模块 unittest 中的工具来为函数和类编写测试；如何编写继承 unittest.TestCase 的类，以及如何编写测试方法，以核实函数和类的行为符合预期；如何使用方法 setUp() 来根据类高效地创建实例并设置其属性，以便在类的所有测试方法中都可使用它们。

测试是很多初学者都不熟悉的主题。作为初学者，并非必须为你尝试的所有项目编写测试；但参与工作量较大的项目时，你应对自己编写的函数和类的重要行为进行测试。这样你就能够更加确定自己所做的工作不会破坏项目的其他部分，你就能够随心所欲地改进既有代码了。如果不小心破坏了原来的功能，你马上就会知道，从而能够轻松地修复问题。相比于等到不满意的用户报告 bug 后再采取措施，在测试未通过时采取措施要容易得多。

如果你在项目中包含了初步测试，其他程序员将更敬佩你，他们将能够更得心应手地尝试使用你编写的代码，也更愿意与你合作开发项目。如果你要跟其他程序员开发的项目共享代码，就必须证明你编写的代码通过了既有测试，通常还需要为你添加的新行为编写测试。

请通过多开展测试来熟悉代码测试过程。对于自己编写的函数和类，请编写针对其重要行为的测试，但在项目早期，不要试图去编写全覆盖的测试用例，除非有充分的理由这样做。

编写函数或类时，还可为其编写测试。通过测试，可确定代码面对各种输入都能够按要求的那样工作。测试让你信心满满，深信即便有更多的人使用你的程序，它也能正确地工作。在程序中添加新代码时，你也可以对其进行测试，确认它们不会破坏程序既有的行为。程序员都会犯错，因此每个程序员都必须经常测试其代码，在用户发现问题前找出它们。

在本章中，你将学习如何使用 Python 模块 unittest 中的工具来测试代码。你将学习编写测试用例，核实一系列输入都将得到预期的输出。你将看到测试通过了是什么样子，测试未通过又是什么样子，还将知道测试未通过如何有助于改进代码。你将学习如何测试函数和类，并将知道该为项目编写多少个测试。

### 11.1 测试函数

函数 get\_formatted\_name() 将名和姓合并成姓名，在名和姓之间加上一个空格，并将它们的首字母都大写，再返回结果。为核实 get\_formatted\_name() 像期望的那样工作，我们来编写一个使用这个函数的程序。程序 names.py 让用户输入名和姓，并显示整洁的全名。这个程序从 name\_function.py 中导入 get\_formatted\_name()。用户可输入一系列的名和姓，并看到格式整洁的全名：

从上述输出可知，合并得到的姓名正确无误。现在假设我们要修改 get\_formatted\_name()，使其还能够处理中间名。这样做时，我们要确保不破坏这个函数处理只有名和姓的姓名的方式。为此，我们可以在每次修改 get\_formatted\_name() 后都进行测试：运行程序 names.py，并输入像 Janis Joplin 这样的姓名，但这太烦琐了。所幸 Python 提供了一种自动测试函数输出的高效方式。倘若我们对 get\_formatted\_name() 进行自动测试，就能始终信心满满，确信给这个函数提供我们测试过的姓名时，它都能正确地工作。

Python 标准库中的模块 unittest 提供了代码测试工具。单元测试用于核实函数的某个方面没有问题；测试用例是一组单元测试，这些单元测试一起核实函数在各种情形下的行为都符合要求。良好的测试用例考虑到了函数可能收到的各种输入，包含针对所有这些情形的测试。全覆盖式测试用例包含一整套单元测试，涵盖了各种可能的函数使用方式。对于大型项目，要实现全覆盖可能很难。通常，最初只要针对代码的重要行为编写测试即可，等项目被广泛使用时再考虑全覆盖。

创建测试用例的语法需要一段时间才能习惯，但测试用例创建后，再添加针对函数的单元测试就很简单了。要为函数编写测试用例，可先导入模块 unittest 以及要测试的函数，再创建一个继承 unittest.TestCase 的类，并编写一系列方法对函数行为的不同方面进行测试。下面是一个只包含一个方法的测试用例，它检查函数 get\_formatted\_name() 在给定名和姓时能否正确地工作：

1『

无意中发现在 vscode 里使用 jupyter-notebook 也超级方便，只需要新建文件 minitest.ipynb 即可，哈哈。（2020-08-18）

真实晕死，搞了半天才发现 unittest 是 Python 里的基础库，开始还在找第三方包安装。

[unittest --- 单元测试框架 — Python 3.8.5 文档](https://docs.python.org/zh-cn/3/library/unittest.html)

```py
import unittest

def get_formatted_name(first, last):
    full_name = first + ' ' + last
    return full_name.title()

class NamesTestCase(unittest.TestCase):
    def test_frist_last_name(self):
        formatted_name = get_formatted_name('feng', 'long')
        self.assertEqual(formatted_name, 'Feng Long')

if __name__ == '__main__':
    unittest.main()
```

』

首先，我们导入了模块 unittest 和要测试的函数 get\_formatted\_name()。在 ❶ 处，我们创建了一个名为 NamesTestCase 的类，用于包含一系列针对 get\_formatted\_name() 的单元测试。你可随便给这个类命名，但最好让它看起来与要测试的函数相关，并包含字样 Test。这个类必须继承 unittest.TestCase 类，这样 Python 才知道如何运行你编写的测试。

NamesTestCase 只包含一个方法，用于测试 get\_formatted\_name() 的一个方面。我们将这个方法命名为 `test_first_last_name()`，因为我们要核实的是只有名和姓的姓名能否被正确地格式化。我们运行 testname_function.py 时，所有以 test 打头的方法都将自动运行。在这个方法中，我们调用了要测试的函数，并存储了要测试的返回值。在这个示例中，我们使用实参 'janis' 和 'joplin' 调用 `get_formatted_name()`，并将结果存储到变量 formatted_name 中（见 ❷）。

在 ❸ 处，我们使用了 unittest 类最有用的功能之一：一个断言方法。断言方法用来核实得到的结果是否与期望的结果一致。在这里，我们知道 get\_formatted\_name() 应返回这样的姓名，即名和姓的首字母为大写，且它们之间有一个空格，因此我们期望 formatted_name 的值为 Janis Joplin。为检查是否确实如此，我们调用 unittest 的方法 assertEqual ()，并向它传递 formatted_name 和 'Janis Joplin'。代码行 self.assertEqual (formatted_name, 'Janis Joplin') 的意思是说：「将 formatted_name 的值同字符串 'Janis Joplin' 进行比较，如果它们相等，就万事大吉，如果它们不相等，跟我说一声！」

第 1 行的句点表明有一个测试通过了。接下来的一行指出 Python 运行了一个测试，消耗的时间不到 0.001 秒。最后的 OK 表明该测试用例中的所有单元测试都通过了。

上述输出表明，给定包含名和姓的姓名时，函数 get\_formatted\_name() 总是能正确地处理。修改 get\_formatted\_name() 后，可再次运行这个测试用例。如果它通过了，我们就知道在给定 Janis Joplin 这样的姓名时，这个函数依然能够正确地处理。

测试未通过时结果是什么样的呢？我们来修改 get\_formatted\_name()，使其能够处理中间名，但这样做时，故意让这个函数无法正确地处理像 Janis Joplin 这样只有名和姓的姓名。下面是函数 get\_formatted\_name() 的新版本，它要求通过一个实参指定中间名：

其中包含的信息很多，因为测试未通过时，需要让你知道的事情可能有很多。第 1 行输出只有一个字母 E （见 ❶），它指出测试用例中有一个单元测试导致了错误。接下来，我们看到 NamesTestCase 中的 test_first_last_name () 导致了错误（见❷）。测试用例包含众多单元测试时，知道哪个测试未通过至关重要。在 ❸ 处，我们看到了一个标准的 traceback，它指出函数调用 get\_formatted\_name ('janis', 'joplin') 有问题，因为它缺少一个必不可少的位置实参。

我们还看到运行了一个单元测试（见 ❹）。最后，还看到了一条消息，它指出整个测试用例都未通过，因为运行该测试用例时发生了一个错误（见❺）。这条消息位于输出末尾，让你一眼就能看到  ——  你可不希望为获悉有多少测试未通过而翻阅长长的输出。

测试未通过时怎么办呢？如果你检查的条件没错，测试通过了意味着函数的行为是对的，而测试未通过意味着你编写的新代码有错。因此，测试未通过时，不要修改测试，而应修复导致测试不能通过的代码：检查刚对函数所做的修改，找出导致函数行为不符合预期的修改。

在这个示例中，get\_formatted\_name() 以前只需要两个实参  ——  名和姓，但现在它要求提供名、中间名和姓。新增的中间名参数是必不可少的，这导致 get\_formatted\_name() 的行为不符合预期。就这里而言，最佳的选择是让中间名变为可选的。这样做后，使用类似于 Janis Joplin 的姓名进行测试时，测试就会通过了，同时这个函数还能接受中间名。下面来修改 get\_formatted\_name()，将中间名设置为可选的，然后再次运行这个测试用例。如果通过了，我们接着确认这个函数能够妥善地处理中间名。要将中间名设置为可选的，可在函数定义中将形参 middle 移到形参列表末尾，并将其默认值指定为一个空字符串。我们还要添加一个 if 测试，以便根据是否提供了中间名相应地创建姓名：

现在，测试用例通过了。太好了，这意味着这个函数又能正确地处理像 Janis Joplin 这样的姓名了，而且我们无需手工测试这个函数。这个函数很容易就修复了，因为未通过的测试让我们得知新代码破坏了函数原来的行为。

给定 get\_formatted\_name() 又能正确地处理简单的姓名后，我们再编写一个测试，用于测试包含中间名的姓名。为此，我们在 NamesTestCase 类中再添加一个方法：

我们将这个方法命名为 test_first_last_middle_name ()。方法名必须以 test_打头，这样它才会在我们运行 test_name_function.py 时自动运行。这个方法名清楚地指出了它测试的是 get\_formatted\_name() 的哪个行为，这样，如果该测试未通过，我们就会马上知道受影响的是哪种类型的姓名。在 TestCase 类中使用很长的方法名是可以的；这些方法的名称必须是描述性的，这才能让你明白测试未通过时的输出；这些方法由 Python 自动调用，你根本不用编写调用它们的代码。

为测试函数 get\_formatted\_name()，我们使用名、姓和中间名调用它（见 ❶），再使用 assertEqual () 检查返回的姓名是否与预期的姓名（名、中间名和姓）一致。我们再次运行 test_name_function.py 时，两个测试都通过了：

```py
import unittest

def get_formatted_name(first, last, middle=''):
    if middle:
        full_name = first + ' ' + middle + ' ' + last
    else:
        full_name = first + ' ' + last
    return full_name.title()

class NamesTestCase(unittest.TestCase):
    def test_frist_last_name(self):
        formatted_name = get_formatted_name('feng', 'long')
        self.assertEqual(formatted_name, 'Feng Long')
    
    def test_frist_last_middle_name(self):
        formattted_name = get_formatted_name('feng', 'long', 'da')
        self.assertEqual(formattted_name, 'Feng Da Long')

if __name__ == '__main__':
    unittest.main()
```

### 11.2 测试类

在本章前半部分，你编写了针对单个函数的测试，下面来编写针对类的测试。很多程序中都会用到类，因此能够证明你的类能够正确地工作会大有裨益。如果针对类的测试通过了，你就能确信对类所做的改进没有意外地破坏其原有的行为。

Python 在 unittest.TestCase 类中提供了很多断言方法。前面说过，断言方法检查你认为应该满足的条件是否确实满足。如果该条件确实满足，你对程序行为的假设就得到了确认，你就可以确信其中没有错误。如果你认为应该满足的条件实际上并不满足，Python 将引发异常。

表 11-1 描述了 6 个常用的断言方法。使用这些方法可核实返回的值等于或不等于预期的值、返回的值为 True 或 False 、返回的值在列表中或不在列表中。你只能在继承 unittest.TestCase 的类中使用这些方法，下面来看看如何在测试类时使用其中的一个。

类的测试与函数的测试相似  ——  你所做的大部分工作都是测试类中方法的行为，但存在一些不同之处，下面来编写一个类进行测试。来看一个帮助管理匿名调查的类：

这个类首先存储了一个你指定的调查问题（见 ❶），并创建了一个空列表，用于存储答案。这个类包含打印调查问题的方法（见 ❷）、在答案列表中添加新答案的方法（见 ❸）以及将存储在列表中的答案都打印出来的方法（见 ❹）。要创建这个类的实例，只需提供一个问题即可。有了表示调查的实例后，就可使用 `show_question()` 来显示其中的问题，可使用 `store_response()` 来存储答案，并使用 show_results() 来显示调查结果。为证明 AnonymousSurvey 类能够正确地工作，我们来编写一个使用它的程序：

这个程序定义了一个问题（"What language did you first learn to speak?" ），并使用这个问题创建了一个 AnonymousSurvey 对象。接下来，这个程序调用 show_question() 来显示问题，并提示用户输入答案。收到每个答案的同时将其存储起来。用户输入所有答案（输入 q 要求退出）后，调用 show_results() 来打印调查结果：

AnonymousSurvey 类可用于进行简单的匿名调查。假设我们将它放在了模块 survey 中，并想进行改进：让每位用户都可输入多个答案；编写一个方法，它只列出不同的答案，并指出每个答案出现了多少次；再编写一个类，用于管理非匿名调查。进行上述修改存在风险，可能会影响 AnonymousSurvey 类的当前行为。例如，允许每位用户输入多个答案时，可能不小心修改了处理单个答案的方式。要确认在开发这个模块时没有破坏既有行为，可以编写针对这个类的测试。

下面来编写一个测试，对 AnonymousSurvey 类的行为的一个方面进行验证：如果用户面对调查问题时只提供了一个答案，这个答案也能被妥善地存储。为此，我们将在这个答案被存储后，使用方法 assertIn() 来核实它包含在答案列表中：

我们首先导入了模块 unittest 以及要测试的类 AnonymousSurvey。我们将测试用例命名为 TestAnonymousSurvey，它也继承了 unittest.TestCase （见 ❶）。第一个测试方法验证调查问题的单个答案被存储后，会包含在调查结果列表中。对于这个方法，一个不错的描述性名称是 `test_store_single_response()`（见 ❷）。如果这个测试未通过，我们就能通过输出中的方法名得知，在存储单个调查答案方面存在问题。

要测试类的行为，需要创建其实例。在 ❸ 处，我们使用问题 "What language did you first learn to speak?" 创建了一个名为 my_survey 的实例，然后使用方法 store_response() 存储了单个答案 English。接下来，我们检查 English 是否包含在列表 my_survey.responses 中，以核实这个答案是否被妥善地存储了（见 ❹）。

这很好，但只能收集一个答案的调查用途不大。下面来核实用户提供三个答案时，它们也将被妥善地存储。为此，我们在 TestAnonymousSurvey 中再添加一个方法：

我们将这个方法命名为 test_store_three_responses()，并像 test_store_single_response() 一样，在其中创建一个调查对象。我们定义了一个包含三个不同答案的列表（见 ❶），再对其中每个答案都调用 store_response()。存储这些答案后，我们使用一个循环来确认每个答案都包含在 my_survey.responses 中（见 ❷）。我们再次运行 test_survey.py 时，两个测试（针对单个答案的测试和针对三个答案的测试）都通过了：

前述做法的效果很好，但这些测试有些重复的地方。下面使用 unittest 的另一项功能来提高它们的效率。

在前面的 test_survey.py 中，我们在每个测试方法中都创建了一个 AnonymousSurvey 实例，并在每个方法中都创建了答案。unittest.TestCase 类包含方法 setUp()，让我们只需创建这些对象一次，并在每个测试方法中使用它们。如果你在 TestCase 类中包含了方法 setUp()，Python 将先运行它，再运行各个以 test_ 打头的方法。这样，在你编写的每个测试方法中都可使用在方法 setUp() 中创建的对象了。

下面使用 setUp() 来创建一个调查对象和一组答案，供方法 test_store_single_response() 和 test_store_three_responses() 使用：

```py
import unittest

def get_formatted_name(first, last, middle=''):
    if middle:
        full_name = first + ' ' + middle + ' ' + last
    else:
        full_name = first + ' ' + last
    return full_name.title()

class NamesTestCase(unittest.TestCase):
    def test_first_last_name(self):
        formatted_name = get_formatted_name('feng', 'long')
        self.assertEqual(formatted_name, 'Feng Long')
    
    def test_first_last_middle_name(self):
        formattted_name = get_formatted_name('feng', 'long', 'da')
        self.assertEqual(formattted_name, 'Feng Da Long')

class AnonymousSurvey():
    def __init__(self, question):
        self.question = question
        self.responses = []
    
    def show_question(self):
        print(self.question)

    def store_response(self, new_response):
        self.responses.append(new_response)
    
    def show_results(self):
        print('Survey results: ')
        for response in self.responses:
            print('- ' + response)

class AnonymousSurveyTestCase(unittest.TestCase):
    def setUp(self):
        question = 'What language did you first learn to speak?'
        self.my_survey = AnonymousSurvey(question)
        self.responses = ['English', 'Spanish', 'Mandarin']

    def test_store_single_response(self):
        self.my_survey.store_response(self.responses[0])
        self.assertIn(self.responses[0], self.my_survey.responses)

    def test_store_three_responses(self):
        for response in self.responses:
            self.my_survey.store_response(response)
        for response in self.responses:
            self.assertIn(response, self.my_survey.responses)
    
if __name__ == '__main__':
    unittest.main()
```

方法 setUp() 做了两件事情：创建一个调查对象（见 ❶）；创建一个答案列表（见 ❷）。存储这两样东西的变量名包含前缀 self （即存储在属性中），因此可在这个类的任何地方使用。这让两个测试方法都更简单，因为它们都不用创建调查对象和答案。方法 `test_store_three_response()` 核实 self.responses 中的第一个答案  —— self.responses[0]  ——  被妥善地存储，而方法 `test_store_three_response() `核实 self.responses 中的全部三个答案都被妥善地存储。

再次运行 `test_survey.py` 时，这两个测试也都通过了。如果要扩展 AnonymousSurvey，使其允许每位用户输入多个答案，这些测试将很有用。修改代码以接受多个答案后，可运行这些测试，确认存储单个答案或一系列答案的行为未受影响。

测试自己编写的类时，方法 setUp() 让测试方法编写起来更容易：可在 `setUp()` 方法中创建一系列实例并设置它们的属性，再在测试方法中直接使用这些实例。相比于在每个测试方法中都创建实例并设置其属性，这要容易得多。

注意：运行测试用例时，每完成一个单元测试，Python 都打印一个字符：测试通过时打印一个句点；测试引发错误时打印一个 E ；测试导致断言失败时打印一个 F。这就是你运行测试用例时，在输出的第一行中看到的句点和字符数量各不相同的原因。如果测试用例包含很多单元测试，需要运行很长时间，就可通过观察这些结果来获悉有多少个测试通过了。