# 0201. Univeral Building Blocks

F rom now on, we can forget about wires and switches and work with the abstraction of logic blocks operating on 1's and 0's, a simple step that allows us to pass from the realm of engineering into the realm of mathematics. This is the most abstract chapter in the book; it will show you how the methods used to construct a tic-tac-toe machine can be used to construct almost any function. In it, we'll define a powerful set of building blocks: logical functions and finite-state machines. With these elements, it's easy to build a computer.

通用构件

关于线路和开关的介绍，我们先放到一边，接下来，我们从工程领域进入数学领域，探讨一下以 0 和 1 的形式运作的逻辑块的抽象原理。本章的内容是这本书最为抽象的一章，我将会向大家展示如何以建造井字游戏机的方法实现任何一种功能。我们还将定义一组功能强大的构件：逻辑功能和有限状态机。利用这些工具，我们可以轻松地构建出一台计算机。

## 2.1 Logical Funcitons

In constructing the tic-tac-toe machine, we began by writing the game tree, whch gave us a set of rules for generating the outputs from the inputs. This turns out to be a generally useful method of attack. Once we write down the rules that specify what outputs we want for each combination of inputs, we can build a device that implements these rules using And, Or , and Invert functions. The logic blocks And , Or , and Invert form a universal construction set , which can be used to implement any set of rules. (These primitive types of logic blocks are sometimes also called logic gates.)

This idea of a universal set of blocks is important: it means that the set is general enough to build anything. My favorite toy when I was a child was a set of interlocking plastic bricks called Lego blocks, with which I built all kinds of toys: cars, houses, spaceships, dinosaurs. I loved to play with these blocks, but they were not quite universal, since the only objects you could build with them had a certain squarish, stair-steppy look. Building something with a different shape — a cylinder or a sphere, for example — would require a new type of block. Eventually, I had to switch to another medium in order to build the things I wanted. But the And, Or , and Invert blocks of Boolean logic are a universal construction set for converting inputs to outputs. The best way to see how they form a universal set is to understand a general method for using them to implement rules. To start, we will consider binary rules — rules that specify inputs and outputs that are either 1 or 0. The tic-tac-toe machine is a good example of a function specified by binary rules, because the input switches and the output lights are either on or off — that is, either 1 or 0. (Later, we will discuss rules for handling letters, numbers, or even pictures and sounds as inputs and outputs.) Any set of binary rules can be completely specified by showing a table of the outputs for each possible combination of 1's and 0's on the inputs. For example, the rules for the Or function are specified by the following table:

The Invert function is specified by an even simpler table:

For a binary function with n inputs, there are 2 n possible combinations of input signals. Sometimes we won't bother to specify all of them, because we don't care about certain combinations of inputs. For example, in specifying the function performed by the tic-tac-toe machine, we don't care what happens if the human player plays in all squares simultaneously. This move would be disallowed, and we don't need to specify the function's output for this combination of inputs.

Complex logic blocks are constructed by connecting And, Or , and Invert blocks. In drawings of the connection pattern, the three blocks are conventionally represented by boxes of different shape (see Figure 9 ); the lines connecting on the left side represent inputs to the blocks, and the lines connecting on the right represent the output. Figure 10 shows how a pair of two-input Or blocks can be connected to form a three-input Or function; the output of this function will be 1 if any one of its three inputs is 1. It's also possible to string several And blocks together in a similar manner to make an And block with any number of inputs.

FIGURE 9 And, Or, and Invert Blocks

FIGURE 10 A three-input Or block made from a pair of two-input Or blocks

Figure 11 shows how an And block can be constructed by connecting an Inverter to the inputs and output of an Or block. (Here is De Morgan's theorem again.) The best way to get a feeling for how this works is to trace through the 1's and 0's for every combination of inputs. Notice that this illustration is essentially the same as Figure 6 in the previous chapter. It points up an interesting fact: we don't really need And blocks in our universal building set, because we can always construct them out of Or blocks and Inverters.

FIGURE 11 Making And out of Or

As in the tic-tac-toe playing machine, And blocks are used to detect each possible combination of inputs for which the output is 1, while Or blocks provide a roster of these combinations. For example, let's start with a simple function of three inputs. Imagine that we want to build a block that allows the three inputs to vote on the output. In this new block, majority wins — that is, the output will be 1 only if two or more of the inputs are 1.

Figure 12A shows how this function is implemented. An And block with the appropriate Invert blocks as input is used to recognize each combination of inputs for which the output is 1; these blocks are connected by an Or block, which produces the output. This strategy can be used to create any transformation of inputs to outputs:

Of course, this particular method of using a separate And gate to recognize each combination of inputs is not the only way to implement the function, and it is often not the simplest way. Figure 12B shows a simpler way to produce the majority function. The great thing about the method described is not that it produces the best implementation but that it always produces an implementation that works. The important conclusion to draw is that it is possible to combine And, Or , and Invert blocks to implement any binary function — that is, any function that can be specified by an input/output table of 0's and 1's.

Restricting the inputs and output to binary numbers is not really much of a restriction, because the combinations of 1's and 0's can be used to represent other things — letters, larger numbers, any entity that can be encoded. As an example of a nonbinary function, suppose we want to build a machine to act as a judge of the children's game of Scissors/Paper/Rock. This is a game for two players in which each chooses, in secret, one of three「weapons」 — scissors, paper, or rock. The rules are simple: scissors cuts paper, paper covers rock, rock crushes scissors. If the two children choose the same weapon, they tie. Rather than building a machine that plays the game (which would involve guessing which weapon the opponent is going to choose), we will build a machine that judges who wins. Here's the input/output table for the function that takes the choices as inputs and declares the winner as output. The table encodes the rules of the game:

FIGURE 12 How the voting function is implemented by And, Or, and Invert Blocks

The Scissors-Paper-Rock judging function is a combinational function, but it is not a binary function, since its inputs and output have more than two possible values. To implement this function as a combinational logic block, we must convert it to a function of 1's and 0's. This requires us to establish some convention for representing the inputs and outputs. A simple way to do this would be to use a separate bit for each of the possibilities. There would be three input signals for each weapon: a 1 on the first input represents Scissors , a 1 on the second input represents Rock , and a 1 on the third input represents Paper. Similarly, we could use separate output lines to represent a win for player A, a win for player B, or a tie. So the box would have six inputs and three outputs.

Using three input signals for each weapon is a perfectly good way to build the function, but if we were doing it inside a computer we would probably use some kind of encoding that required a smaller number of inputs and outputs. For example, we could use two bits for each input and use the combination 01 to represent Scissors , 10 to represent Paper , and 11 to represent Rock. We could similarly encode each of the possible outputs using two bits. This encoding would result in the simpler three-input/two-output table shown below:

Computers can use combinations of bits to represent anything; the number of bits depends on the number of messages that need to be distinguished. Imagine, for example, a computer that works with the letters of the alphabet. Five-bit input signals can represent thirty-two different possibilities (2 5 = 32). Functions within the computer that work on letters sometimes use such a code, although they more often use an encoding with seven or eight bits, to allow representation of capitals, punctuation marks, numerals, and so on. Most modern computers use the standard representation of alphabet letters called ASCII (an acronym for American Standard Code for Information Interchange). In ASCII, the sequence 1000001 represents the capital letter A, and 1000010 represents the capital B , and so on. The convention, of course, is arbitrary.

Most computers have one or more conventions for representing numbers. One of the most common is the base 2 representation of numbers, in which the bit sequence 0000000 represents zero, the sequence 0000001 represents the number 1, the sequence 0000010 represents 2, and so on. The description of computers as「64-bit」or「32-bit」indicates the number of bit positions in the representation used by the computer's circuits: a 32-bit computer uses a combination of thirty-two bits to represent a base-2 number. The base-2 number system is a common convention, but there is nothing that requires its use. Some computers don't use it at all, and most computers that do also represent numbers in other ways for various purposes. For instance, many computers use a slightly different convention for representing negative numbers and also have a convention called a floating point to represent numbers that have decimal points. (The position of the decimal point「floats」relative to the digits, so that a fixed number of digits can be used to represent a wide range of numbers.) The particular representation schemes are often chosen in such a way as to simplify the logic of the circuits that perform arithmetical operations, or to make it easy to convert from one representation to another.

Because any logical function can be implemented as a Boolean logic block, it is possible to build blocks that perform arithmetical operations like addition or multiplication by using numbers with any sort of representation. For instance, imagine that we want to build a functional block that will add numbers on an eight-bit computer. An eight-bit adder block must have sixteen input signals (eight for each of the numbers to be added), and eight output signals for the sum. Since each number is represented by eight bits, there are 256 possible combinations, and each can represent a different number. For example, we could use these combinations to represent the numbers between 0 and 255, or between −100 and +154. Defining the function of the block would be just a matter of writing down the addition table and then converting it to 1's and 0's, using the chosen representation. The table of 1's and 0's could then be converted to And and Or blocks by the methods described above.

By adding two more inputs to the block, we could use similar techniques to build a block that not only adds but also subtracts, multiplies, and divides. The two extra control inputs would specify which of these operations was to take place. For instance, on every line of the table where the control inputs were 01, we would specify the output to be the sum of the input numbers, whereas in every combination where the control inputs were 10, we would specify the outputs to be the product, and so on. Most computers have logical blocks of this type inside them called arithmetic units.

Combining Ands and Ors according to this strategy is one way to build any logical function, but it is not always the most efficient way. Often, by clever design, you can implement a circuit using far fewer building blocks than the preceding strategy requires. It may also be desirable to use other types of building blocks or to design circuits that minimize the delay from input to output. Here are some typical puzzles in logic design: How do you use And blocks and Inverters to construct Or blocks? (Easy.) How do you use a collection of And and Or blocks, plus only two Inverters , to construct the function of three Inverters? (Hard, but possible.) Puzzles like this come up in the course of designing a computer, which is part of what makes the process fun.

逻辑功能

在建造井字游戏机时，我们会先画出博弈树，以表示一组根据输入生成输出的规则。事实证明，这是一种行之有效的方法。一旦我们明确了规则，为不同输入指定与之对应的输出，就能用「与」「或」「非」等逻辑功能构建出可以实现这些规则的机器装置。「与」「或」「非」逻辑块构成了一组通用构件，它们可用于实现任何规则。这些基本逻辑块有时也被称为逻辑门（logic gate）。

通用的逻辑块这一概念十分重要，它意味着可以用其构建出任何东西。我小时候最喜欢的玩具是一种可拼接的乐高塑料块，我用它们组装出了汽车、房屋、太空飞船以及恐龙等各式各样的玩具。虽然我非常喜欢玩乐高积木，但它们的通用性不够好，因为用它们搭建出来的玩具外观只限于方形和阶梯形等形状。若想搭建诸如圆柱形和圆形等类似形状的玩具，就需要用新的积木类型。后来，为了搭建出想要的东西，我不得不借助于其他工具。布尔逻辑中的「与」「或」「非」等逻辑块是一种将输入转换为输出的通用构件。若想了解它们如何成为通用构件的原理，你最好先掌握利用构件实现规则的通用方法。

我们先来看一看二进制规则，这种规则指定的输入和输出为 1 或 0。井字游戏机是采用二进制规则来设定逻辑功能的一个范例，因为其中作为输入的开关和作为输出的灯泡只能处于开启或关闭的状态，也就是只能为 1 或 0。我们稍后将讨论输入和输出为字母、数字，甚至图片和声音的处理规则。对于输入为 1 和 0 的组合及其对应的输出，我们都可以通过表格来表示任意一组二进制规则。例如，「或」功能的二进制规则可以通过下表来表示（见表 2-1）。「非」功能的二进制规则的表格则更为简单（见表 2-2）。

表 2-1「或」功能的二进制规

表 2-2「非」功能的二进制规则

对于 n 个输入的二进制功能来说，其输入信号的可能组合共有 2n 种。在一些情况下，我们不必费力将它们全部列举出来，因为某些输入组合我们无须去考虑。例如，当我们梳理井字游戏机的功能时，不会去考虑人类玩家同时走所有方格的情况。游戏规则禁止这种走法，因此我们不必为这种输入组合设定对应的输出。通过连接「与」「或」「非」等逻辑块，我们可以组合出各种复杂的逻辑块。在绘制连接图时，通常有三种不同形状的图例来表示这三类逻辑块（见图 2-1）。逻辑块左边的连线表示输入，右边的连线表示输出。图 2-2 描述了用一对两个输入的「或」逻辑块组合成一个三个输入的「或」逻辑块的过程。如果三个输入中有任意一个为 1，则这个逻辑功能的输出就为 1。我们可以用类似的方式将若干「与」逻辑块组合成一个多输入的「与」逻辑块。

图 2-2 具有三个输入的「或」逻辑块的形成过程

在图 2-3 中，若干「非」逻辑块分别与一个「或」逻辑块的输入和输出相连，组合成一个「与」逻辑块（其依据的还是德·摩根定律）。若想了解其中的工作原理，最好的方法是研究每种输入组合下 1 和 0 背后的逻辑规律。值得注意的是，图 2-3 与第 1 章中的图 1-6 基本上是相同的。这揭示了一个有趣的事实：「与」逻辑块并不是通用构件中不可或缺的，我们可以通过「或」逻辑块和「非」逻辑块将其构建出来。

图 2-3 由「或」「非」逻辑块组成的「与」逻辑块

在井字游戏机中，「与」逻辑块用于识别输出为 1 时的各种可能的输入组合，而「或」逻辑块则将这些输入组合形成列表。我们以一种具有三个输入的逻辑块为例来说明。假设我们现在要构建一个由三个输入决定输出的逻辑块。这个逻辑块遵循少数服从多数的原则，也就是说，只有两个及两个以上的输入为 1 时，输出才会为 1（见图 2-4）。

图 2-4 通过「与」「或」「非」逻辑块实现投票表决功能

图 2-4A 显示了实现投票表决功能的过程。其中，若干「与」逻辑块和位于恰当位置的「非」逻辑块用于识别所有与输出 1 对应的输入组合，这些逻辑块共同连接至一个产出输出的「或」逻辑块上。通过这种策略，我们便能实现从输入到输出的任意形式的转换。

不过，这种利用单个「与」逻辑块识别单个输入组合的方法既不是实现投票表决功能的唯一方法，也不是最简单的方法。图 2-4B 提出的方案更为简单。这种设计方案的精妙之处不是它能得出最优的实现方式，而是它总能找到一种可行的实现方式。综上所述，我们可以得出一个重要结论：通过「与」「或」「非」等逻辑块的组合，我们可以实现任何二进制功能，即那些可以由 1 和 0 表示的输入／输出表所设定的功能。

实际上，将输入和输出设定为二进制数并不会带来太大的限制，因为 1 和 0 的数字组合可以表示许多事物，例如字母、更大的数字以及所有可编码的项。举一个非二进制功能的例子。假设我们要制造一台机器来充当石头／剪刀／布猜拳游戏的裁判，在这个儿童热衷于玩的游戏中，游戏双方会选择三种「武器」（石头、剪刀、布三种手势）中的一种。判断胜负的规则很简单：剪刀胜布，布胜石头，石头胜剪刀；如果双方选择的武器相同，则打成平手。我们并不需要制造一台会玩这种游戏的机器（因为这需要机器去猜测对手选择何种武器），而是制造一台能判断双方输赢的机器。下面是该功能的输入和输出表（见表 2-3），输入是双方的选择，而输出是获胜方，该表实现了对游戏规则的编码。

表 2-3 裁判功能的输入和输出表

这个猜拳游戏的裁判功能虽然是一个组合功能，但不是一个二进制功能，因为其输入和输出超过两种。若想通过组合逻辑块来实现这一功能，我们必须将它转换为一个由 1 和 0 表示的二进制功能。这就要求我们设定输入和输出的规则。有一种简单的方法是，使用一种二进制位表示一种可能性，即需要三个输入信号来表示每种武器：第一个输入信号为 1，表示剪刀；第二个输入信号为 1，表示石头；第三个输入信号为 1，表示布。同样，我们可以使用不同的输出信号来分别表示玩家 A 获胜、玩家 B 获胜或者平局。因此，逻辑块共有六个输入和三个输出。

为每种武器设定三个输入信号是实现裁判功能的非常有效的方法。不过，如果我们在计算机中实现这种功能，可能会使用输入和输出更少的编码方式。例如，我们可以使用两个二进制位来表示每种输入：用 01 组合表示剪刀，10 组合表示布，11 表示石头。同样，我们可以使用两个二进制位对每种输出进行编码，如表 2-4 所示，这种编码方式还可以简化为具有三个输入和两个输出的表。

表 2-4 裁判功能的二进制规则

计算机可以通过二进制位的组合表示任何信号，所需的二进制位数目取决于需要区分的信号的数目。例如，对于一台处理各类字符的计算机而言，5 个二进制位的输入信号可以表示 32 种不同的可能性（25=32）。计算机中用字符操作的功能有时会采用这种编码方式，不过它们更多地采用 7 个或者 8 个二进制位表示字母、标点符号、数字等。大多数现代计算机都采用一种标准的编码方式，即 ASCII 编码，其全称为美国国家信息交换标准码（American Standard Code for Information Interchange，简称 ASCII）。在 ASCII 编码中，1000001 表示大写字母 A，1000010 表示大写字母 B，依此类推。当然，也可以采用其他编码方式。

大多数计算机都有一种或多种表示数字的编码方式，最为常见的是以 2 为基的数字编码方式，在这种表示方法中，序列 0000000 表示十进制数 0，序列 0000001 表示十进制数 1，依此类推。我们常用 32 位或者 64 位来描述计算机，这两个数字代表计算机电路表示数字时同时处理的二进制位的数目：一台 32 位的计算机使用 32 位表示一个以 2 为基的数字。虽然以 2 为基的数字系统是一种通用惯例，但这并不意味着必须采用这种方式。而且，出于各种原因，许多采用这种方式的计算机也会采用其他的数字表示方式。比如，许多计算机会采用一种略微不同的方式来表示负数，并且会用一种称为浮点数（floating point）的数字来表示带小数点的数字。小数点在浮点数中的位置可以左右「浮动」，因此一定数目的位数可以表示很大范围的数值。为了简化执行算术运算的线路逻辑，以及更方便地转换数字表示形式，我们一般会采取与之对应的数字表示形式。

由于布尔逻辑可以实现所有的逻辑功能，因此采用任何表示形式的二进制数都可以构建出能够执行加法、乘法等运算的逻辑块。例如，如果我们要在一台 8 位计算机中构建一个能完成数字加法运算的逻辑块，那么这个 8 位加法逻辑块必须具有 16 个输入信号（每个加数都有 8 个输入信号）和 8 个输出信号作为加法的和。由于每个数字都由 8 个二进制位来表示，因此存在 256 种组合，每种组合代表不同的数字。例如，我们能用这些组合表示 0～255 的数，或者 - 100～154 的数。若想定义加法块的功能，只需先写出加法表，然后根据所选择的表示形式将表中的数字转化为由 1 和 0 组成的数字串，最后再用前面描述的方法将 1 和 0 组成的数字串转换为对应的「与」「或」逻辑块。

如果在上述的逻辑块中再添加两个控制输入，我们便可以构建出能同时完成加法、减法、乘法和除法运算的逻辑块。这两个附加的控制输入用于指定要执行的运算类型。例如，对于表中控制输入为 01 的每一行，我们可以将其输出定义为两个输入数字的和；对于表中控制输入为 10 的每一行，我们可以将其输出定义为两个输入数字的乘积，依此类推。大多数计算机都有这类逻辑块，常常被称为运算器（arithmetic unit）。

依据上述方法来组合「与」「或」逻辑块，我们便可以实现任何一种逻辑功能。不过，这虽然是一种可行的方法，但不是最有效的。通过巧妙的设计，我们可以采用比上述方法所需构件更少的方法来搭建线路，而且，还可以采用其他类型的构件，或者将输入至输出的线路延迟时间减至最低程度。在设计逻辑功能的过程中，我们通常会碰到一些典型的难题：如何用「与」逻辑块和「非」逻辑块构建出「或」逻辑块？（这个很简单）如何用一组「或」逻辑块和「与」逻辑块以及两个「非」逻辑块实现一个具有三个「非」逻辑块的功能？（这个比较困难，但可以实现。）在计算机设计过程中，我们经常会遇到这类难题，不过，这也正是使设计过程变得有趣的地方。

## 2.2 Finite-State Machines

The methods I've described can be used to implement any function that stays constant in time, but a more interesting class of functions are those that involve sequences in time. To handle such functions, we use a device called a finite-state machine. Finite-state machines can be used to implement time-varying functions — functions that depend not just on the current input but also on the previous history of inputs. Once you learn to recognize a finite-state machine, you'll notice them everywhere — in combination locks, ballpoint pens, even legal contracts. The basic idea of a finite-state machine is to combine a look-up table, constructed using Boolean logic, with a memory device. The memory is used to store a summary of the past, which is the state of the finite-state machine.

A combination lock is a simple example of a finite-state machine. The state of a combination lock is a summary of the sequence of numbers dialed into the lock. The lock doesn't remember all the numbers that have ever been dialed into it, but it does remember enough about the most recent numbers to know when they form the sequence that will open the lock. An even simpler example of a finite-state machine is the retractable ballpoint pen. This finite-state machine has two possible states — extended and retracted — and the pen remembers whether its button has been pressed an odd or an even number of times. All finite-state machines have a fixed set of possible states, a set of allowable inputs that change the state (clicking a pen's button, or dialing a number into a combination lock), and a set of possible outputs (retracting or extending the ballpoint, opening the lock). The outputs depend only on the state, which in turn depends only on the history of the sequence of inputs.

Another simple example of a finite-state machine is a counter, such as the tally counter on a turnstile indicating the number of people who have passed through. Each time a new person goes through, the counter's state is advanced by one. The counter is a finite state because it can only count up to a certain number of digits. When it reaches its maximum count — say, 999 — the next advance will cause it to return to zero. Odometers on automobiles work like this. I once drove an old Checker cab with an odometer that read 70,000, but I never knew if the cab had traveled 70,000 miles, 170,000 miles, or 270,000 miles, because the odometer had only 100,000 states; all those histories were equivalent as far as the odometer was concerned. This is why mathematicians often define a state as「a set of equivalent histories.」

Other familiar examples of finite-state machines include traffic lights and elevator-button panels. In these machines, the sequence of states is controlled by some combination of an internal clock and input buttons such as the「Walk」button at the crosswalk and the elevator call and floor-selection buttons. The next state of the machine depends not only on the previous state but also on the signals that come from the input button. The transition from one state to another is determined by a fixed set of rules, which can be summarized by a simple state diagram showing the transition between states. Figure 13 shows a state diagram for a traffic-light controller at an intersection where the light turns red in both directions after the Walk button is pressed. Each drawing of light represents a state and each arrow represents a transition between states. The transition depends on whether or not the「walk」button is pressed.

FIGURE 13 State diagram for a traffic-light controller

FIGURE 14 Finite-state machine, with logic block feeding register

To store the state of the finite-state machine, we need to introduce one last building block — a device called a register , which can be used to store bits. An n -bit register has n inputs and n outputs, plus an additional timing input that tells the register when to change state. Storing new information is called「writing」the state of the register. When the timing signal tells the register to write a new state, the register changes its state to match the inputs. The outputs of the register always indicate its current state. Registers can be implemented in many ways, one of which is to use a Boolean logic block to steer the state information around in a circle. This type of register is often used in electronic computers, which is why they lose track of what they're doing if their power is interrupted.

A finite-state machine consists of a Boolean logic block connected to a register, as shown in Figure 14. The finite-state machine advances its state by writing the output of the Boolean logic block into the register; the logic block then computes the next state, based on the input and the current state. This next state is then written into the register on the next cycle. The process repeats in every cycle.

The function of a finite-state machine can be specified by a table that shows, for every state and every input, the state that follows. For example, we can summarize the operation of the traffic-light controller by the following table:

The first step in implementing a finite-state machine is to generate such a table. The second step is to assign a different pattern of bits to each state. The five states of the traffic-light controller will require three bits. (Since each bit doubles the number of possible patterns, it is possible to store up to 2 n states using n bits.) By consistently replacing each word in the preceding table with a binary pattern, we can convert the table to a function that can be implemented with Boolean logic.

In the traffic-light system, a timer controls the writing of the register, which causes the state to change at regular intervals. Another example of a finite-state machine that advances its state at regular intervals is a digital clock. A digital clock with a seconds indicator can be in one of 24 × 60 × 60 = 86,400 possible display states — one for each second of the day. The timing mechanism within the clock causes it to advance its state exactly once per second. Many other types of digital computing devices, including most general-purpose computers, also advance their state at regular intervals, and the rate at which they advance is called the clock rate of the machine. Within a computer, time is not a continuous flow but a fixed sequence of transitions between states. The clock rate of the computer determines the rate of these transitions, hence the correspondence between physical and computational time. For instance, the laptop computer on which I am writing this book has a clock rate of 33 megahertz, which means that it advances its state at a rate of 33 million times per second. The computer would be faster if the clock rate were higher, but its speed is limited by the time required for information to propagate through the logic blocks to compute the next state. As technology improves, the logic tends to become faster and the clock rate increases. As I write these words, my computer is state-of-the-art, but by the time you read this book computers with 33 megahertz clock rates will probably be considered slow. This is one of the wonders of silicon technology: as we learn to make computers smaller and smaller, the logic becomes faster and faster.

One reason finite-state machines are so useful is that they can recognize sequences. Consider a combination lock that opens only when it is given the sequence 0–5–2. Such a lock, whether it is mechanical or electronic, is a finite-state machine with the state diagram shown in Figure 15.

A similar machine can be constructed to recognize any finite sequence. Finite-state machines can also be made to recognize sequences that match certain patterns. Figure 16 shows one that recognizes any sequence starting with a 1, followed by a sequence of any number of 0s, followed by a 3. Such a combination will unlock the door with the combination 1–0–3, or a combination such as 1–0–0–0–3, but not with the combination 1–0–2–3, which doesn't fit the pattern. A more complex finite-state machine could recognize a more complicated pattern, such as a misspelled word within a stream of text.

FIGURE 15 State diagram for a lock with combination 0-5-2

As powerful as they are, finite-state machines are not capable of recognizing all types of patterns in a sequence. For instance, it is impossible to build a finite-state machine that will unlock a lock whenever you enter any palindrome — a sequence that is the same forward and backward, like 3–2–1–1–2–3. This is because palindromes can be of any length, and to recognize the second half of a palindrome you need to remember every character in the first half. Since there are infinitely many possible first halves, this would require a machine with an infinite number of states.

A similar argument demonstrates the impossibility of building a finite-state machine that recognizes whether a given English sentence is grammatically correct. Consider the simple sentence「Dogs bite.」The meaning of this sentence can be changed by putting a qualifier between the noun and the verb; for instance,「Dogs that people annoy bite.」This sentence can in turn be modified by putting another phrase in the middle:「Dogs that people with dogs annoy bite.」Although the meaning of such sentences might be expressed more clearly, and although they become increasingly difficult to understand, they are grammatically correct. In principle, this process of nesting phrases inside of one another can go on forever, producing absurd sentences like「Dogs that dogs that dogs that dogs annoy ate bit bite.」Recognizing such a sentence as grammatically correct is impossible for a finite-state machine, and for exactly the same reason it's difficult for a person: you need a lot of memory to keep track of all those dogs. The fact that human beings seem to have trouble with the same kinds of sentences that stump finite-state machines has caused some people to speculate that we may have something like a finite-state machine inside our head for understanding language. As you will see in the next chapter, there are other types of computing devices that seem to fit even more naturally with the recursive structure of human grammar.

FIGURE 16 State diagram to recognize sequences like 1,0,3 and 1,0,0,0,:

I was introduced to finite-state machines by my mentor Marvin Minsky. He presented me with the following famous puzzle, called the firing squad problem : You are a general in charge of an extremely long line of soldiers in a firing squad. The line is too long for you to shout the order to「fire,」and so you must give your order to the first soldier in the line, and ask him to repeat to the next soldier and so on. The hard part is that all the soldiers in the line are supposed to fire at the same time. There is a constant drumbeat in the background; however, you can't even specify that the men should all fire after a certain number of beats, because you don't know how many soldiers are in the line. The problem is to get the entire line to fire simultaneously; you can solve it by issuing a complex set of orders which tells each soldier what to say to the soldiers on either side of him. In this problem, the soldiers are equivalent to a line of finite-state machines with each machine advancing its state by the same clock (the drumbeat), and each receiving input from the output of its immediate neighbors. The problem is therefore to design a line of identical finite-state machines that will produce the「fire」output at the same time in response to a command supplied at one end. (The finite-state machines at either end of the line are allowed to be different from the others.) I won't spoil the puzzle by giving away the solution, but it can be solved using finite-state machines that have only a few states.

Before showing you how Boolean logic and finite-state machines are combined to produce a computer, I'll skip ahead in this bottom-up description and tell you where we're going. The next chapter starts by setting out one of the highest levels of abstraction in the function of a computer, which is also the level at which most programmers interact with the machine.

有限状态机

前文介绍的方法可以用于实现不随时间发生变化，可随时执行的功能。不过，还有一类更有趣的功能，它是按时序来执行的。为了实现这种功能，我们需要用到一种被称为有限状态机的装置。有限状态机能够实现随时间变化的功能，这类功能的输出不仅取决于当前时刻的输入，还取决于先前输入的时序。一旦你掌握了有限状态机这个概念，便会发现它们无处不在 —— 密码锁、圆珠笔，甚至法律合同中都有它的影子。有限状态机由一个按布尔逻辑构成的查询表和一个存储器组合而成。存储器用于存储过去的历史记录，即有限状态机中的「状态」。

密码锁就是一个简单的有限状态机。密码锁的状态是输入锁中的数字序列的总体。密码锁不会记住先前输入的所有数字，只需记住最近一次输入的数字，并且知道这些数字组成的序列何时可以打开密码锁。更简单的有限状态机是伸缩式圆珠笔，它只有两种状态 —— 伸出和缩进，并且圆珠笔会记住按钮被按了奇数次还是偶数次。所有有限状态机都具有一组固定的可能状态集合、一组可改变状态的允许输入集合（例如，按下圆珠笔按钮，向密码锁中输入数字等），以及一组可能的输出集合（例如，圆珠笔笔尖的伸出和缩进，打开密码锁等），这些输出只取决于状态，而状态又只取决于过去的输入序列。

有限状态机的另外一个简单范例是计数器，例如旋转门上安装的计数器可以记录通过的人数。每当有人通过这个旋转门时，计数器的状态就会更新一次。这种计数器的状态是有限的，因为它能记录的数位是有限的。当它的计数值达到最大值时，比如最大数值为 999，再进一个人便会更新为零。汽车的行驶里程表的工作原理也与之类似。我曾经开过一辆老式的出租车，其里程表读数为 70 000，但我搞不清楚这辆车到底行驶了 70 000 英里（1 英里约为 1.6 千米）、170 000 英里，还是 270 000 英里。因为这个里程表只有 100 000 种状态。对这个里程表而言，上述历史记录都是一样的。正是出于这个原因，数学家通常会将一种状态定义为「一些等值历史的集合」。

其他常见的有限状态机还包括交通信号灯、电梯按钮等。在这些有限状态机中，状态序列是由内置的时钟和输入按钮共同决定的，这些输入按钮包括人行道上设置的「行人」按钮和电梯中的「呼救」及「楼层选择」按钮。有限状态机下一时刻的状态不仅取决于前一时刻的状态，还取决于输入按钮的信号。在有限状态机中，状态之间的转换由一组固定的规则来确定，通过简单的状态图，我们可以表示出状态的转换过程。图 2-5 展示了交通信号灯的状态图，当按下「行人」按钮后，两个方向都亮起红灯。图中每个信号灯图示表示一种状态，每一个箭头表示状态之间的转换，而状态的转换取决于「行人」按钮是否被按下。

为了存储有限状态机的状态，我们还需要引入一种用于存储二进制位的构件 —— 寄存器（register）。一个 n 位的寄存器具有 n 个输入和 n 个输出，以及一个额外的时序输入，这个时序输入能够告知寄存器更新状态的时间。存储新信息的过程就是将状态「写入」寄存器的过程。当时序信号传递到寄存器，通知其「写入」一种新状态时，寄存器便会根据输入信号改变其状态。寄存器的输出始终与寄存器的内部状态同步。寄存器有很多种实现方式，其中一种是通过布尔逻辑块来控制状态信息，使其在一个闭合圈中不断循环。电子计算机通常采用这种寄存器，这也是当计算机的电源被中断时经常丢失正在处理的信息的原因。

图 2-6 中的有限状态机由一个布尔逻辑块和一个寄存器连接而成。有限状态机将布尔逻辑块的输出「写入」寄存器，以此完成状态的更新；然后，布尔逻辑块根据寄存器的当前状态和当前的输入来计算下一个状态；接下来，计算出的状态值会在下一个周期被「写入」寄存器。上述过程会随着每一个周期重复进行下去。

图 2-6 逻辑块和寄存器连接成的有限状态机

有限状态机的功能可以通过这样一个表来表示：表中每种状态和每种输入信号与下一个状态相对应。例如，我们可以通过表 2-5 来表示交通信号灯控制器的运算过程。

表 2-5 交通信号灯的状态表

实现有限状态机的第一步是建立这样的表格，第二步是为每种状态设定不同的二进制位组。交通信号灯控制器共有 5 种状态，这就需要使用三个二进制位来表示。由于每增加一个二进制位就能使状态数目翻倍，故 n 个二进制位最多能存储 2n 种状态。将上表中的所有状态都替换为二进制位组之后，就能将此表转化为由布尔逻辑实现的功能。

在交通信号灯系统中，时序发生器控制着寄存器的读写操作，这使寄存器的状态按固定的时间间隔进行更新。时钟也是一种按时间间隔更新状态的有限状态机。一个精确到秒的时钟共有 24 x 60 x 60=86 400 种显示状态，也就是一天中的每一秒都对应着一种状态。时钟内部的时序机制保证它每秒钟更新一次状态。许多数字计算设备，包含绝大多数通用计算机，都在固定的时间间隔内更新状态，其状态更新频率被称为时钟频率（clock rate）。在计算机内，时间并不是连续的流，而是固定的状态转换序列。计算机的时钟频率决定了状态转换的频率，这是真实的物理时间和计算时间之间的对应关系。例如，我写这本书时用到的笔记本电脑的时钟频率是 33 兆赫兹，这意味着它在以每秒钟 3 300 万次的频率更新状态。如果时钟频率变得更高了，则这台电脑的运算速度会更快，不过当计算下一个状态时，运算速度会受到信息在逻辑块之间传递所耗的时间的限制。

随着技术的不断进步，逻辑运算的速度将会变得越来越快，时钟频率也会变得越来越高。虽然当我写下这些文字时，我电脑的时钟频率已经算是当前最高的了，但当你们读到这本书时，33 兆赫兹的时钟频率可能太慢了。这就是硅基技术创造的奇迹之一：计算机的体型越做越小，而其逻辑运算速度越来越快。

有限状态机之所以如此强大，原因之一是它们能够识别序列。例如对于某个密码锁来说，只有当输入序列为 0—5—2 时，密码锁才会打开。无论它是机械的还是电子的，这种锁都属于一种有限状态机，其状态图如图 2-7 所示。

有限状态机之所以如此强大，原因之一是它们能够识别序列。例如对于某个密码锁来说，只有当输入序列为 0—5—2 时，密码锁才会打开。无论它是机械的还是电子的，这种锁都属于一种有限状态机，其状态图如图 2-7 所示。

图 2-7 密码为 0—5—2 的密码锁的状态图

我们也可以制造出能识别出任意有限序列的有限状态机。此外，有限状态机还可以用于识别符合某些特定模式的序列。图 2-8 中的有限状态机可以识别出所有以 1 开头、中间为任意数目的 0，并以 3 结尾的序列。符合这种条件的组合都可以打开密码锁，比如 1—0—3 和 1—0—0—0—3，而序列 1—0—2—3 则无法打开密码锁，因为它不符合密码模式。更复杂的有限状态机能够识别更复杂的模式，例如识别出一段文字中拼写错误的单词。

图 2-8 识别序列 1—0—3 和 1—0—0—0—3 的状态图

有限状态机的功能虽然很强大，但不能识别出所有类型的序列模式。例如，我们无法搭建出一台能识别出所有回文密码的有限状态机，这里的回文密码是指从左向右读和从右向左读都一样的密码，比如 3—2—1—2—3。这是因为回文串可以是任意长度的字符串。为了识别出回文串的前半部分，你需要记住前半部分的每个字符。由于前半部分的数字组合有无数种，因此这就需要一个具有无数种状态的机器。

同理，我们也无法制造出能判断英文句子是否有语法错误的有限状态机。比如这个短句「Dogs bite」（狗咬人）。我们可以通过在名词和动词之间加入修饰词来改变这句话的含义，例如，「Dogs that people annoy bite」（被人惹怒的狗咬人）。我们还可以在这句话中间加入一个短语：「Dogs that people with dogs annoy bite」（被带狗的人惹怒的狗咬人）。虽然这些句子表达的含义更为清晰且更难理解，但从语法层面上来说，它们都是正确的。从原则上来说，我们可以在一个句子中不断嵌套词组，最终组成这样的句子：「Dogs that dogs that dogs that dogs annoy ate bit bite」。有限状态机无法判断这个句子的语法是否正确，实际上人类也很难做出判断，这背后的原因是相同的：需要厘清所有这些「dogs」的关系。有限状态机难以处理的语句也会难住人类，这一事实不禁让人推测：人类的大脑中是否也存在着类似于有限状态机的机制呢？正如你将在下一章中看到的，有些类型的计算装置似乎更适合处理人类语法中的递归结构。

第一个向我介绍有限状态机概念的人是我的导师马文·明斯基（Marvin Minsky）。他还曾向我阐述一个有名的难题，即行刑队问题。假设你是行刑场上的一位长官，手下有一组排成长队的士兵。由于士兵的队伍非常长，不是每一个士兵都能听到你口头传达的「开火」的命令，因此你只能给队伍中的第一个士兵下达命令，然后由他开始向旁边的士兵重复这个命令，依此类推。然而问题的难点在于，队列中的所有士兵必须同时开火。虽然士兵都可以听到节奏固定的鼓点声，但你无法规定在多少鼓点后所有士兵同时开火，因为你根本不知道有多少名士兵。因此，这个问题的关键在于，确保全体士兵同时开火。你可以通过这样的方法来解决该问题：设计一组复杂的指令，告知每个士兵应该向两边的人传递何种信息。这时，每个士兵就相当于一个有限状态机，其中每个有限状态机都需要根据相同的时钟（鼓点）来更新状态，并接受相邻邻居的输出作为各自的输入。现在的问题就在于，如何设计一排相同的有限状态机。当某一端的有限状态机收到相关命令后，所有有限状态机需要在同一时刻产生「开火」的输出（可以允许队伍两端的有限状态机异于其他位置的有限状态机）。这里我不便写出答案，不过可以告诉大家的是，利用若干个只具有少量状态的有限状态机便能解决这个难题。

在讲解如何将布尔逻辑和有限状态机结合起来并建造一台计算机之前，这里我只作自下而上的描述，指明一下途径和方向。下一章我将会介绍计算机功能中最为抽象的内容，大多数程序员都在这一级别与计算机交流。