## 记忆时间

## 目录

0101 Nuts And Bolts

0201 Univeral Building Blocks

0301 Programming

## 0101. Nuts And Bolts

When I was a child, I read a story about a boy who built a robot out of parts he found lying around a junkyard. The boy's robot could move, talk, and think, just like a person, and it became his friend. For some reason, I found the idea of building a robot very appealing, so I decided to build one myself. I remember collecting body parts — tubes for the arms and legs, motors for the muscles, lightbulbs for the eyes, and a big paint can for the head — in the full and optimistic expectation that after they were assembled and the contraption was plugged in, I would end up with a working mechanical man.

After nearly electrocuting myself a few times, I began to get my parts to move, light up, and make noises. I felt I was making progress. I began to understand how to construct movable joints for the arms and legs. But something even more important was beginning to dawn on me: I didn't have the slightest idea how to control the motors and the lights, and I realized that something was missing in my knowledge of how robots worked. I now have a name for what was missing: it's called computation. Back then, I called it「thinking,」and I saw that I didn't have a clue about how to get something to think. It seems obvious to me now that computation is the hardest part of building a mechanical man, but as a child this came as a surprise.

基础知识

小时候，我读过这样一个故事，一个男孩用从垃圾场收集的零件组装出了一个机器人，这个机器人可以像人一样走路、说话和思考，并成为男孩的朋友。不知何故，我被制造机器人的想法深深地吸引了，因此决定也动手组装一个。我对当时收集各部位零件的情景还记忆犹新：用管子作四肢，马达作肌肉，灯泡作眼睛，油漆桶作脑袋。我满怀希望地期待当自己完成组装、插上电源之后，就能拥有一个正常运作的机器人。

在经历了几次严重的触电事故后，我的机器人终于可以移动和发光了，而且还会发出「嗡嗡」的声音。我感觉自己有所长进，而且我还懂得了如何为四肢制造活动关节。不过，当时我面临的最大问题是，该如何控制那些马达和灯泡。后来，我意识到自己是对机器人的工作原理缺乏了解，而现在，我知道当时缺乏的知识是什么了 —— 计算，当时我称之为「思维」，我毫不知晓如何才能让某个物体具备思维能力。现在，我清楚地知道，计算才是制造机器人最难的部分，而当时还是小孩的我很难意识到这一点。

### 1.1 Boolean Logic

Fortunately, the first book I ever read on the subject of computation was a classic. My father was an epidemiologist, and we were living in Calcutta at the time. Books in English were hard to come by, but in the library of the British consulate I found a dusty copy of a book written by the nineteenth-century logician George Boole. The title of the book was what attracted me: An Investigation of the Laws of Thought. This grabbed my imagination. Could there really be laws that governed thought? In the book, Boole tried to reduce the logic of human thought to mathematical operations. Although he did not really explain human thinking, Boole demonstrated the surprising power and generality of a few simple types of logical operations. He invented a language for describing and manipulating logical statements and determining whether or not they are true. The language is now called Boolean algebra.

Boolean algebra is similar to the algebra you learned in high school, except that the variables in the equations represent logic statements instead of numbers. Boole's variables stand for propositions that are either true or false, and the symbols XXXX represent the logical operations And, Or, and Not. For example, the following is a Boolean algebraic equation.

1『

原书中的公式用 PHP 代码表示的话（2021-06-08）：

```php
!(A||B) = !A && !B
```

』

This particular equation, called De Morgan's theorem (after Boole's colleague Augustus De Morgan), says that if neither A nor B is true, then both A and B must be false. The variables A and B can represent any logical (that is, true or false) statement. This particular equation is obviously correct, but Boolean algebra also allows much more complex logical statements to be written down and proved or disproved.

Boole's work found its way into computer science through the master's thesis of a young engineering student at the Massachusetts Institute of Technology named Claude Shannon. Shannon is best known for having invented a branch of mathematics called information theory , which defines the measure of information we call a bit. Inventing the bit was an impressive accomplishment, but what Shannon did with Boolean logic was at least as important to the science of computation. With these two pieces of work, Shannon laid the foundation for the developments that were to occur in the field of computing for the next fifty years.

Shannon was interested in building a machine that could play chess — and more generally in building mechanisms that imitated thought. In 1940, he published his master's thesis, which was titled「A Symbolic Analysis of Relay Switching Circuits.」In it, he showed that it was possible to build electrical circuits equivalent to expressions in Boolean algebra. In Shannon's circuits, switches that were open or closed corresponded to logical variables of Boolean algebra that were true or false. Shannon demonstrated a way of converting any expression in Boolean algebra into an arrangement of switches. The circuit would establish a connection if the statement was true and break the connection if it was false. The implication of this construction is that any function capable of being described as a precise logical statement can be implemented by an analogous system of switches.

Rather than presenting the detailed formalisms developed by Boole and Shannon, I will give an example of their application in the design of a very simple kind of computing device, a machine that plays the game of tic-tac-toe. This machine is much simpler than a general-purpose computer, but it demonstrates two principles that are important in any type of computer. It shows how a task can be reduced to logical functions and how such functions can be implemented as a circuit of connected switches. I actually built a tic-tac-toe machine out of lights and switches shortly after I read Boole's book in Calcutta, and this was my introduction to computer logic. Later, when I was an undergraduate at MIT, Claude Shannon became a friend and teacher, and I discovered that he, too, had used lights and switches to build a machine that could play tic-tac-toe.

As most readers know, the game is played on a 3 × 3 square grid. Players take turns marking the squares, one player using an X , the other an O. The first player to place three symbols in a row (horizontally, vertically, or diagonally) wins the game. Young children enjoy tic-tac-toe because it seems to offer limitless possible strategies for winning. Eventually they realize that only a small number of patterns can occur, and the game consequently loses its charm: once both players learn the patterns, each game invariably ends in a tie. Tic-tac-toe is a good example of a computation precisely because it wavers on this line between the complex and the simple. Crossing that line is what computation is all about. Computation is about performing tasks that seem to be complex (like winning a game of tic-tac-toe) by breaking them down into simple operations (like closing a switch).

In tic-tac-toe, the situations that occur are few enough so that it's practical to write them all down, and therefore to build the correct response in every case into the machine. We can use a simple two-step process for designing the machine: first , reduce the play to a series of cases defining the correct response to each pattern of moves; second , convert those cases into electrical circuits by wiring the switches to recognize the pattern and indicate the appropriate response.

One way to proceed would be to write down every conceivable arrangment of X's and O's which could be placed on the grid and then decide how the computer would play in each instance. Since each of the nine squares has three possible states ( X , O, and blank), there are 3^9 (or 19,683) ways to fill the grid. But most of these patterns would never occur in the course of a game. A better method of listing the possibilities is to draw up a game tree  — a configuration that traces every possible line of play. The game tree starts with a blank grid at the root and has a branch for every possible alternative line of play, determined by the move of the human player. (The tree does not need to branch when the machine plays, because the response of the machine to any given move is always predetermined.) Figure 1 shows a small part of such a tree. For every possible move made by X , the human player, there is a predetermined O response to be made by the machine. (For some strange reason, computer scientists always draw trees upside-down, with the「root」at the top.)

FIGURE 1 Part of a game tree for tic-tac-toe

The tree in Figure 1 illustrates the strategy that I always use in tic-tac-toe: I play in the center whenever I can. The machine's moves are determined by the human player's moves, which vastly reduces the number of possibilities to be considered. A full game tree, showing what the machine should do in every situation, has about five hundred or six hundred branches, the exact number depending on the details of strategy. Following the tree will cause the machine to win, or at least tie, every game. The rules of the game are built into the responses, so by following the tree the machine will always obey the rules. From this game tree, we can write down specifications that say exactly when the machine should play in any particular position. These specifications constitute the Boolean logic of the machine.

Once we have defined the desired behavior, we can translate that behavior into electrical circuits built out of batteries, wires, switches, and lights. The basic circuit in the machine is the same circuit used in a flashlight: when the switch is pressed down — that is, closed — the light goes on, because a complete path has been formed between the bulb and the battery. (The connections to the battery are indicated by the + and − signs.) Most important, these switches can be wired either in series or in parallel. For instance, we can put two switches together in series to make a light that works only when both switches are closed. This circuit implements one of the basic switching functions of the computer — the「logic block」known as the And function, so called because the bulb lights only when the first and the second switches are closed. Switches connected in parallel form the Or function, which connects the circuit (and thus lights the bulb) whenever either or both of the switches are closed (see Figure 2 ).

These simple patterns of serial and parallel wiring can be used in combinations to form connections that follow various logical rules. In the tic-tac-toe machine, chains of switches connected in series are used to detect patterns, and these chains are connected in parallel to lights, so that several patterns can light the same bulb — that is, produce the same response from the machine.

FIGURE 2 Switches in series and parallel

The tic-tac-toe machine I built has four banks of nine switches each, and each switch corresponds to one of the nine squares on the tic-tac-toe grid. It also has nine lightbulbs, arranged in the pattern of a tic-tac-toe board. The machine, which always plays first, makes its moves by lighting a bulb. The human player moves by closing a switch — using the first bank of switches to make his first move, the second bank for his second move, and so on. In my version, the machine always begins by playing in the upper left corner of the board, a scheme that reduces the number of cases considerably. The human player responds by closing one of the switches in the first bank (say, the one corresponding to the center square in the grid), and the game proceeds. The machine's strategy is embodied in the wiring between the switches and the lights.

The wiring that produces the machine's first response is easy (see Figure 3 ). Each switch in the first bank is connected to a light that corresponds to the machine's reply. For instance, a play in the center causes a response in the lower right, so the center switch is wired to the lower-right light. Since my machine always responds in the center square if it can, most of the first bank of switches is wired in parallel to the middle light.

FIGURE 3 Several different patterns that produce the same response

Each pattern for the second round of play depends on the human player's first and second moves. To recognize this combination of human moves, the corresponding switches are wired in series. For example, if the player's first move is in the center and second move in the upper right, the machine is then supposed to respond by playing in the lower left. This pattern is accomplished by wiring the center switch in the first bank in series with the upper-right switch in the second bank (「if center and upper-right squares are filled, then...」), with the chain of two switches being connected to the lightbulb in the lower left. Each parallel connection to a bulb specifies a different combination that will cause the bulb to light (「this move or that move will provoke this response」). Whenever it was necessary to use the same switch in two different circuits, I used a「double throw」switch — two switches mechanically linked to the same button, so that they switch together — which allows the same move to be part of two different patterns. The wiring of the third and fourth banks of switches follows the same principle, but there are even more combinations. As you can imagine, the wiring gets complicated, even though the principles are simple. There are fewer choices open on the grid, but the chains of switches are longer.

The tic-tac-toe machine I built has about a hundred and fifty switches. This seemed like a lot to me at the time (I made the switches out of wood and nails), but the computer chips I design today have millions of switches, most of them connected in patterns very similar to those used in the tic-tac-toe machine. Most modern computers use a different kind of electrical switch — a transistor, which I will describe later — but the basic notion of connecting switches in series to produce the And function and connecting switches in parallel to produce the Or function is exactly the same.

While the logic of the tic-tac-toe machine is similar to the logic of a computer, there are several important differences. One is that the tic-tac-toe machine has no notion of events happening sequentially in time; therefore, the entire sequence of the game — that is, the entire game tree — must be determined in advance. This is cumbersome enough where tic-tac-toe is concerned and practically impossible for a more complicated game, like chess, or even checkers. Modern computers are very good at playing checkers and pretty good at playing chess (see chapter 5 ), because in place of the predetermined game tree they use a different method — one that involves examining patterns sequentially in time.

Another difference between the tic-tac-toe machine and a general-purpose computer is that the tic-tac-toe machine can perform only one function. The「program」of the machine is built into its wiring. The tic-tac-toe machine has no software.

布尔逻辑

幸运的是，我读的第一本有关计算机的书是一本经典之作。我的父亲是一位流行病学家，那时我们居住在加尔各答，很难读到英文著作。在英国领事馆的图书室里，我找到了一本表面布满灰尘的书，作者是 19 世纪的逻辑学家乔治·布尔（George Boole），书名为《思维规律的研究》（An Investigation of the Laws of Thought）。这个书名立刻吸引了我，令我心驰神往，难道真的存在支配思维的法则吗？在这本书中，布尔试图将人类的思维逻辑简化为数学运算。他虽然没有真正解释清楚人类的思维过程，但道出了简单的逻辑运算的惊人力量和普适性。他还发明了一种语言，可以用来描述和处理逻辑陈述，以及判定这些陈述的真假。这种语言现在被称为布尔代数（Boolean algebra）。

布尔代数与我们在高中所学的代数相似，差别仅在于等式中的变量所代表的东西从数字变成了逻辑命题。布尔变量代表非真即假的命题，符号∧、∨、¬ 分别代表「与」「或」「非」逻辑运算。例如下列的布尔代数方程：

¬（A∨B）=（¬ A）∧（¬ B）

这个方程被称为德·摩根定律，是以布尔的同事奥古斯都·德·摩根（Augustus De Morgan）的名字命名的，其含义为：如果 A 和 B 无一为真，则两者皆必然为假。变量 A 和 B 可以表示任意非真即假的逻辑命题。显然，这个方程是成立的。不过，布尔代数还能写出更加复杂的逻辑命题，并能进行证明和反证。

麻省理工学院曾有一位年轻的工程学硕士，他通过一篇论文将布尔的理论引入了计算机科学领域，使其大放异彩，这位学生名叫克劳德·香农（Claude Shannon）。香农最广为人知的成就是创立了信息论，信息论是数学的一个分支，这门分支定义了我们称为「二进制位」（又叫比特）的信息度量单位。二进制位概念的提出是一项了不起的成就。对于计算科学来说，香农利用布尔逻辑所做的工作也同样重要。香农的这两项成就为之后 50 年计算机科学的发展奠定了基础。

香农曾致力于创造一台会下国际象棋的机器，更确切地说是一台能模拟人类思维的机器。1940 年，他在硕士论文《继电器与开关电路的符号分析》（A Symbolic Analysis of Relay Switching Circuits）中表明，构建一个与布尔代数方程完全等价的电路是可能的。在香农设计的电路中，开关的开启和关闭对应着布尔代数逻辑变量值的真与假。香农提出了一种方法，可以将布尔代数方程转化为开关组合。当命题为真时，电路建立连接，当命题为假时，电路则断开连接。这种方法意味着，任何能由布尔逻辑命题精确描述的功能都可用类似的开关系统来实现。

与其详述布尔和香农建立的理论框架，我们不如举例来说明其理论在实际中的应用，以我设计的一台井字游戏机为例。虽然相比于通用的计算机，这个游戏机非常简单，但它体现了对所有计算机来说都非常重要的两大原理：如何将一项任务转化为一系列逻辑函数，以及如何用由开关连接起来的电路实现这些函数。当我读完布尔的书之后，就用灯泡和开关搭建了一个井字游戏机，这是我对计算机逻辑的初次涉猎。后来，我去了麻省理工学院读本科，香农成了我的良师益友。我惊奇地发现，他也曾用灯泡和开关搭建过井字游戏机。

大多数读者都知道，井字游戏在一个 3×3 的方格棋盘中进行。游戏双方轮流在方格中标注符号，如果一位玩家使用符号「X」，另一位则使用符号「O」，而率先使三个符号连成一行（水平、垂直或者对角）的玩家即可获胜。小孩子之所以喜欢玩井字游戏，是因为这个游戏似乎有无数种获胜的方法。不过，他们最终都会意识到，能赢得棋局的模式只有为数不多的几种，此时这个游戏对他们来说就会变得索然无味。一旦玩家双方都掌握了游戏套路，每场游戏都将以平局结束。井字游戏很好地说明了计算的本质，其难度介于复杂和简单之间。计算就是跨过复杂和简单之间的分界线，去完成复杂的任务，实现方法就是通过将看似复杂的任务（如赢得井字游戏）分解为简单的操作（如关闭开关）。

1-3『学 React 时，官方给的第一个实现例子就是井字棋游戏。（2021-10-10）』

在井字游戏中，可能会出现的棋局模式并不多，完全可以将它们都列举出来，再将每种棋局的正确走法输入游戏机中。我们可以通过两个简单的步骤来设计这个游戏机：首先，将游戏转化为所有可能的棋局，每种棋局都根据具体的模式制定出正确的走法；然后，将每种走法转化为由开关连接的电路，使其能识别出棋局模式，并做出正确的反应。

还有一种方法是，列举出由符号「X」和「O」在方格棋盘中组成的所有可能的棋局模式，再确定计算机在每种情况下的走法。在 3×3 的方格棋盘中，每一格都有 3 种可能的状态（X、O 和空白），因此共有 3^9（或 19 683）种不同的棋局。不过，在玩游戏的过程中，大多数棋局是永远不会出现的。利用博弈树（game tree）的方法，我们可以更好地列举出各种可能性，这种方法足以描绘出所有可能发生的棋局路线图。博弈树从一个空白的根节点开始，下面的每条分支代表一种可能的游戏进程，游戏进程由人类玩家的下棋步骤决定。当轮到机器下棋时，博弈树并不会分叉，因为机器的走法都是预先设定好的。图 1-1 展示了博弈树的一部分。无论人类玩家在哪个方格中标出「X」，机器都会按事先设定好的走法标上「O」。说来也怪，计算机科学家经常将博弈树倒置，即将根节点画在顶部。

这棵博弈树反映了我在井字游戏中经常采用的一种策略 —— 尽可能占据方格棋盘上的中心格。人类玩家的下棋步骤决定了机器的下棋步骤，这大大减少了需要考虑的可能情况。一棵显示机器在各种情况下走法的完整博弈树大约有 500-600 个分支，确切的分支数量取决于所采取的下棋策略。如果机器按照博弈树指定的策略下棋，那么它每盘游戏都可以获胜，或者至少下成平局。由于游戏规则已经被编入了机器的走法之中，因此只要机器按照博弈树的步骤下棋，就不会违反游戏规则。依据博弈树，我们可以写出机器在所有棋局下的标准走法，这些标准走法便构成了机器的布尔逻辑。

一旦我们定义了想实现的机器行为，就可以将这种行为转化为由电池、电线、开关和灯泡组成的电路。机器的基本电路与手电筒的电路原理并无不同：当按下开关，即闭合电路时，灯泡会亮起，因为此时灯泡和电池之间形成了一条完整的通路（电池的两极分别用符号「+」和「-」来表示）。更为重要的是，这些开关可以通过串联或者并联的方式相连。例如，我们可以将两个开关串联在一起，在这种情况下，只有当两个开关都闭合时，灯泡才会亮起。通过这种电路，我便可实现计算机的一种基本的开关功能 ——「与」功能，之所以这样称呼它，是因为只有当第一个开关「与」和第二个开关「与」同时闭合时，灯泡才会亮起；同理可得，如果开关采用并联的方式，则可以实现「或」功能，即当其中一个「或」两个开关闭合时，电路就会连通，灯泡会亮起来（见图 1-2）。

将简单的串联电路和并联电路组合起来，便可以实现各种具有不同逻辑规则的连接。在井字游戏机中，一个串联的开关可用于识别一种棋局模式，而不同的串联开关可以通过并联的方式与灯泡相连，所以当几组串联开关通过并联的方式连接后，这些串联开关所代表的棋局模式就会点亮同一盏灯泡，也就是说，机器在这些情况下会采用相同的走法。

我设计的井字游戏机有 4 组开关，每组分别有 9 个开关，每个开关对应九方格棋盘上的一格。同时，游戏机中的 9 个灯泡按照井字棋盘那样排列。游戏设定由机器先走，且每走一步就点亮与之对应的灯泡。人类玩家每走一步就合上一个开关，走第一步棋使用第一个开关组，走第二步棋使用第二个开关组，依此类推。在我设计的这款游戏机中，机器总是先从棋盘左上角开始走第一步棋，这种开局方式可以大大减少所需考虑的可能情况。人类玩家接着可以合上第一组开关中的某个开关，比如合上对应棋盘中心格的开关，作为第一步棋，这样游戏就能持续进行下去了。这些开关和灯泡组成的电路构成了机器的游戏策略。

使机器对第一步棋做出反应的线路十分简单（见图 1-3）。将第一组开关中的每个开关都连接至对应的灯泡，灯泡代表的就是机器需要走的那一步棋。例如，如果人类玩家第一步棋走在棋盘中心格，机器就会走右下格，那么中心格的开关就要连接至右下角的灯泡。由于我设计的机器一有可能便以走中心格作为首选，因此第一组开关中的大多数开关都会与棋盘中心格的灯泡并联。

机器第二轮的走法取决于人类玩家走的第一步和第二步。为了识别出人类玩家的多轮下棋步骤，相应的开关采取串联的方式。例如，如果人类玩家的第一步棋走中心格，第二步棋走右上格，那么机器就会走左下格。这种棋局模式可以通过这种方法实现：将第一组开关中代表中心格的开关与第二组开关中代表右上格的开关串联（这表示「如果中心格和右上格都由人类玩家标上了符号，那么应该……」），再将这两个开关的开关链与代表左下格的灯泡相连。每组与灯泡相连且互为并行关系的开关链分别表示能使灯亮起来的不同下棋步骤，即「如果人类玩家的走法属于这些步骤中的任何一种，机器都会采取同样的应对方式」。如果两条不同的电路需要使用同一个开关，我便会安装一个「双闸开关」，即以机械的方式连接至同一按钮的两个开关，使它们能实现同步切换，这样便可以将同一步棋纳入两个不同的棋局模式之中。第三组和第四组开关的连接方式遵循同样的原则，但它们形成的下棋步骤更多。你可能会想到，虽然原理很简单，但线路会变得越来越复杂，棋盘中可供选择的方格会越来越少，但开关链条会越变越长。

我设计的井字游戏机大约有 150 个开关，它们由木头和钉子制成，对于当时的我来说这是一组很庞大的数字。然而现在，我设计的计算机芯片中的开关数目高达数百万个，大多数开关的连接模式与井字游戏机中的模式非常相似。虽然大多数现代计算机都采用了一种不同类型的电子开关 —— 晶体管，但基本的设计理念是一样的：用串联开关实现逻辑「与」的功能，用并联开关实现逻辑「或」的功能。

虽然从逻辑上来说，井字游戏机与通用计算机具有相似性，但两者也存在一些重要区别。第一个区别是，井字游戏机对按时间顺序发生的事件毫无概念。因此，我们必须事先设定好游戏中所有事件的发生顺序，即先设定好整个博弈树。对于井字棋而言，设计博弈树的工作已经很复杂了，更不用说更为复杂的游戏了，比如国际象棋、跳棋等，这种方法几乎是行不通的。现代计算机非常善于玩跳棋，也善于玩国际象棋（见第 5 章），这是因为它们放弃了预先设定博弈树的方法，而是采取了一种按时间顺序依次识别棋局模式的方法。

井字游戏机与通用计算机的第二个重要区别是，前者只能执行单一的任务，其「程序」完全内置于线路中。换句话说，井字游戏机中没有任何软件。

### 1.2 Bits and Logic Blocks

As I noted in the Introduction, there is no reason the tic-tac-toe machine (or any other computer) has to be built out of electrical switches. A computer can represent information using electrical currents, fluid pressures, or even chemical reactions. Whether you build a computer out of transistors, hydraulic valves, or a chemistry set, the principles on which it operates are much the same. The key idea of the tic-tac-toe machine is that the And function is implemented by connecting two switches in series and the Or function is implemented by connecting two switches in parallel, but there are many other ways to implement And and Or.

Here I must pause to mention the bit. The smallest「difference that makes a difference」(to use Bateson's phrase again) is a difference that splits all signals into two distinct classes. In the tic-tac-toe machine, the two classes are「current flowing」and「no current flowing.」By convention, we call the two possible classes 1 and 0. These are just names; we could as easily call them True and False , or Alice and Bob. Even the choice of which class is called 0 and which is called 1 is arbitrary. A signal that can carry one of two different messages (like 1 or 0) is called a binary signal, or a bit. A computer uses combinations of bits to represent all kinds of sets of alternatives — different moves in tic-tac-toe, say, or different colors to be displayed on a screen. Since the convention is to designate the bits by 1's and 0's, people often think of these bit patterns as numbers, hence the old chestnut「The computer does everything with numbers.」But this convention is simply a way of thinking about what's going on. If we had named the two possible messages conveyed by the bit the letters X and Y, people would be saying,「The computer does everything with letters.」The more accurate statement is「The computer represents numbers, letters, and everything else with patterns of bits.」

FIGURE 4 Mechanical implementation of the OR function

Instead of using the flow of electricity to represent a bit, we could have used mechanical motion. Figure 4 shows how the Or function is implemented using a technology that represents 1 by sliding a stick to the right. As long as both the A and the B input sticks stay to the left, representing 0, then the spring will keep the output stick pushed to the left, but if either input stick slides to the right, then the output stick will slide to the right also. The object in Figure 5 computes another useful function, that of inversion: The inverter turns every signal into its opposite: for example, it turns a push to the right into a pull to the left, and vice versa.

These And, Or , and Invert functions are logic blocks , and they can be connected in order to create other functions. For instance, the output of an Or block can be connected to an Invert block to create a Nor function: the Nor  output will be a 1 when neither of its inputs is 1. In another example (using De Morgan's theorem), we can make an And block by connecting two Invert blocks to the inputs of an Or block and connecting a third Invert block to the output (see Figure 6 ). These four work together to implement the And function, so the final output is 1 only when both the inputs are 1.

FIGURE 5 Mechanical inverter

Early computing devices were made with mechanical components. In the seventeenth century, Blaise Pascal built a mechanical adding machine, which inspired both Gottfried Wilhelm Leibniz and the English polymath Robert Hooke to build improved machines that could multiply, divide, and even take square roots. These machines were not programmable, but in 1833 another Englishman, the mathematician and inventor Charles Babbage, designed and partially constructed a programmable mechanical computer. Even as late as my own childhood in the sixties, most arithmetic calculators were mechanical. I've always liked these mechanical machines, because you can see what's happening, which is not the case with electronic computers. When I'm designing an electronic computer chip, I imagine the operation of the circuits as moving mechanical parts.

FIGURE 6 An And block constructed by connecting an Or block to inverters

二进制位和逻辑块

正如我在前言中提到的，构建井字游戏机或者任何其他类型的计算机并非一定要使用电子开关。计算机可以使用电流、液压或者化学反应来表示信息。无论你采用晶体管、液压阀，还是化学装置来构建计算机，其背后的工作原理大致相同。井字游戏机的关键逻辑是：通过串联的两个开关来实现逻辑「与」的功能，通过并联的两个开关来实现逻辑「或」的功能。当然，实现这两种功能的方法还有很多。

关于计算机工作原理的介绍，我们需暂停一下，先来了解一下二进制位的概念。最小的「非同小可的差异」（借用贝特森的说法）将所有信号分成截然不同的两类。在井字游戏机中，这两类信号分别是「电流流通」和「电流不通」。按照惯例，我们将这两类信号分别称为 1 和 0。1 和 0 只是形式上的名称，我们也可以称其为真和假，或者爱丽丝和鲍勃。至于命名哪种类型的信号为 1、哪种类型的信号为 0，则是任意的。如果一个信号携带两种信息之一（比如 1 或 0），我们称其为二进制信号或者一个二进制位。计算机采用若干个二进制位的组合来表示各种可选方案，比如井字游戏中不同的走法，或者显示屏上的不同颜色。按照惯例，二进制位用 1 和 0 来表示，人们常将二进制位组视为数字，因此才有这样的打趣，「计算机利用数字完成所有的工作」。然而，这个惯例只是思考问题的一种方式而已，如果我们将二进制位传递的两种信息命名为字母 X 和 Y，那么人们也许会说「计算机利用字母完成所有的工作」。因此，更准确的说法应该是：「计算机利用二进制位组表示数字、字母以及所有的一切。」

除了电流外，我们也可以采取机械运动的方式来表示二进制位。图 1-4 说明了如何借助这种方法实现「或」功能 —— 滑杆向右移动表示输入 1。当输入杆 A 和 B 都保持在左侧时，表示两个输入都为 0，这时输出杆由于受到弹簧向左的推力而保持原位不动；当任何一个输入杆向右移动时，输出杆就会因受力而移至右侧。图 1-5 中的装置实现了另一种逻辑功能，即「非」功能。这种装置可以将所有输入的信号转换成与之相反的信号，例如，它能将左边的输入杆转换成右边的输出杆，反之亦然。

图 1-5 用以实现「非」功能的机械式取反器

「与」「或」「非」功能被统称为逻辑块，将它们组合起来就能实现其他逻辑功能。例如，将「或」逻辑块的输出和「非」逻辑块的输入相连，便可以实现「或非」功能，即当两个输入都不为 1 时，「或非」的输出才为 1。再举一个例子（应用德·摩根定律），将两个「非」逻辑块的输出分别连接至一个「或」逻辑块的输入，再将此逻辑块的输出连接至第三个「非」逻辑块的输入（见图 1-6），那么这 4 个逻辑块就共同实现了逻辑「与」的功能，即当两个输入都为 1 时，最后的输出才是 1。

三个「非」逻辑块的输入（见图 1-6），那么这 4 个逻辑块就共同实现了逻辑「与」的功能，即当两个输入都为 1 时，最后的输出才是 1。

图 1-6 一个「或」逻辑块和若干「非」逻辑块组成一个「与」逻辑块

早期的计算器是由机械部件制造成的。17 世纪，法国数学家布莱士·帕斯卡（Blaise Pascal）制造出了一台机械加法器，这让德国自然科学家戈特弗里德·威廉·莱布尼茨（Gottfried Wilhelm Leibniz）和英国博学家罗伯特·胡克（Robert Hooke）深受启发，他们改良了这台加法器，使其可以运算乘法和除法，甚至可以求取平方根。不过，这些机器都是不可编程的。到了 1833 年，英国数学家、发明家查尔斯·巴贝奇（Charles Babbage）设计并参与制造了一台可编程的机械式计算机。实际上，在我的童年时期，即 20 世纪 60 年代，大多数算术计算器都是机械式的。我非常喜欢这些机械式计算机，因为里面的运作过程能被清楚地看到，这一点是电子计算机无法实现的。当我设计电子计算机芯片时，会将电路想象成移动的机械部件。

### 1.3 The Fluid Computer

The picture I have in my mind when I design a logic circuit is of hydraulic valves. A hydraulic valve is like a switch that controls and is controlled by the flow of water. Each valve has three connections: the input, the output, and the control. Pressure on the control connection pushes on a piston that turns off the water flow from input to output. Figure 7 shows a circuit for the Or function, built out of hydraulic valves.

In this circuit, water pressure is used to distinguish between the two possible signals. Notice that in a hydraulic valve the control pipe can affect the output pipe but the output pipe cannot affect the control pipe. This restriction establishes a forward flow of information through the switch; in a sense, it establishes a direction in time. Also, since the valve is either open or closed, it serves an additional function of amplification , which allows the strength of the signal to be restored to its maximum value at every stage. Even if the input is a little low on pressure — because it goes through a long, thin pipe, say, or because of a leak — the output will always be at full pressure thanks to the on/off operation of the valve. This is the fundamental difference between digital and analog: A digital valve is either on or off; an analog valve, like your kitchen faucet, can be anything in between. In the hydraulic computer, all that is required of the input signal is that it be strong enough to move the valve. In this case, the difference that makes a difference is the difference in water pressure sufficient to switch the valve on. And since a weakened signal entering an input will still produce a full-strength output, we can connect thousands of layers of logic, the output of one layer controlling the next, without worrying about a gradual decrease in pressure. The output of each gate will always be at full pressure.

FIGURE 7 An Or block built with hydraulic valves

This type of design is called restoring logic , and the example in hydraulic technology is particularly interesting, because it corresponds almost exactly to the logic used in modern electronic computers. The water pressure in the pipes is analogous to the voltage on the wires, and the hydraulic valve is analogous to the metal-oxide transistor. The control, input, and output connections on the valve correspond closely to the three connections (called gate, source , and drain ) on a transistor. The analogy between water valves and transistors is so exact that you could translate the design for a modern microprocessor directly into a design for a hydraulic computer. To do so, you would need to look at the pattern of wires on the silicon chip under a microscope and then bend a set of pipes into the same shapes as the wires on the chip and connect them in exactly the same pattern. In place of each transistor, you would use a hydraulic valve. The pipe that corresponds to the power-supply voltage on your chip would be connected to a pressurized water supply, and the pipe that corresponds to the ground connection could empty down a drain.

To use the hydraulic computer, you would have to connect hydraulic equivalents of its inputs and outputs — you would need to build a hydraulic keyboard, a hydraulic display, hydraulic memory chips, and so on — but if you did all this, it would go through exactly the same switching events as the electronic chip. Of course, the hydraulic computer would be much slower than your latest microprocessor (to say nothing of larger), because water pressure travels down pipes much more slowly than electricity travels down wires. As to the size: Since the modern microchip has several million transistors, its hydraulic equivalent would require several million valves. A transistor in a chip is about a millionth of a meter across; a hydraulic valve is about 10 centimeters on a side. If the pipes scale proportionally, then the hydraulic computer would cover about a square kilometer with pipes and valves. From an airplane, it would look roughly the same as the electronic chip does under a microscope.

When I design a computer chip, I draw lines on a computer screen, and the pattern is reduced (in a process analogous to photographic reduction) and etched onto a chip of silicon. The lines on the screen are my pipes and valves. Actually, most computer designers don't even bother drawing lines; instead, they specify the connections between Ands and Ors and let a computer work out the details of placement and geometry of the switches. Most of time, they forget about the technology and concentrate on the function. I do this, too, sometimes, but I still prefer to draw my own shapes. Whenever I design a chip, the first thing I want to do is look at it under a microscope — not because I think I can learn something new by looking at it but because I am always fascinated by how a pattern can create reality.

液压计算机

设计逻辑电路时，我脑海中会浮现出液压阀的影子。液压阀类似于一个既能控制水流也能被水流控制的开关。液压阀具有三个连接点：输入、输出和控制端。控制端连接处的液压推动活塞向前，从而阻断从输入端到输出端的水流。图 1-7 表示的是一个由液压阀构建成的「或」逻辑块。

图 1-7 用液压阀构建成的「或」逻辑块

在这个管路中，液压用于区分两种不同类型的信号。值得注意的是，液压阀中的控制管会影响输出管，但反之则不然。这个限制条件确立了信息可通过开关向前流动。从某种意义上来说，它实现了一种时间维度上的单向性。而且，由于液压阀只能处于打开或关闭的状态，它还具有放大的功能，即使信号的强度在每个阶段都能保持在最大值。得益于液压阀的开／关功能，即使输入的液压很小（这可能是因为液体经过了一根细长的管道或者管道存在泄漏），输出的液压依然能达到最大值。这就是数字开关和模拟开关的根本区别：数字开关要么开启，要么关闭，而模拟开关就像厨房的水龙头一样有各种调节值，可以位于两者间的任意位置。在液压计算机中，输入信号的压力必须足够强，这样才能打开液压阀。在这种情况下，「非同小可的差异」就是液压足以或者不足以将阀门打开的水压差。由于输入的微弱信号仍然能产生足够强度的输出，因此，我们可以将数以千计的逻辑管道连接起来，并用一个逻辑管道的输出控制下一个逻辑管道，而不必担心管道液压会逐渐降低，因为每个阀门输出的液压仍将保持在最大值。

这类设计被称为复原逻辑（restoring logic）。关于液压技术的例子尤为有趣，因为它与现代计算机采用的逻辑几乎完全相同。管道中的液压类似于电路中的电压，液压阀类似于金属氧化物制成的晶体管。液压阀中的控制、输入和输出分别对应晶体管中的栅极、源极、漏极。液压阀与晶体管的工作原理非常相似，我们完全可以将现代微处理器的设计直接转化为液压计算机的设计。为了完成这种转化，你需要通过显微镜观察硅基芯片上的线路布局，然后按照线路摆放好管道，再按线路原样将其连接起来；同时，用液压阀替代芯片上的晶体管。芯片上的电路与供电电源相连，因此与之对应的管道应该连接至可以增压的水源处；芯片上有电路接地，而与之对应的管道应该能将积水排空。

若想使用这台液压计算机，你还需要将输入和输出的液压部件连接起来，这就需要建造一个液压式键盘、一个液压式显示器以及液压式存储芯片等，如果这一切都完成了，液压计算机便能完全复现电子芯片中所有开关的动作。当然，由于液压在管道中的传播速度比电路中电流的速度慢很多，因此液压计算机的运行速度要比你最新的微处理器慢得多，更不用说大型机算机了。从体积上来说，现代微芯片上容纳了数百万个晶体管，与之对应的液压计算机则需要数百万个阀门，芯片上晶体管的长度只有百万分之一米，而一个液压阀的边长就在 10 厘米左右。如果管道也按此比例布置，那么由液压阀和管道组成的液压计算机的占地将达到 1 平方千米。从飞机上来看，这台液压计算机与你在显微镜下看到的芯片的大小相当。

当我设计计算机芯片时，首先会利用计算机绘制出设计图，然后将这些图案缩小，再蚀刻在硅芯片上。屏幕上呈现的线路就相当于管道和液压阀。事实上，绝大多数计算机设计者都不必为画图劳心费神，他们只需指定逻辑块（「或」「与」等）之间的连接关系，后续诸如逻辑块的位置和开关的几何布线等细节性工作都可交由计算机来处理。在多数情况下，设计者都会专注于功能设计，而将画线工艺置之于脑后。我虽然有时也会这样做，但还是更喜欢亲手画设计图。每当我设计完一款芯片时，想做的第一件事就是利用显微镜来观察它。我这么做并非因为能从观察中获取新知识，而是着迷于感受芯片上的图案是如何缔造出现实的。

1-3『专注与功能设计而非具体怎么话设计图，跟目前设计流模块库要实现的目的是一样一样的，比如氢化反应模块，专注与功能设计（选择哪些功能组件）而非具体如何画图。（2021-10-10）』

### 1.4 Tinker Toys

Except for the miracle of reduction, there is no special reason to build computers with silicon technology. Building a computer out of any technology requires a large supply of only two kinds of elements: switches and connectors. The switch is a steering element (the hydraulic valve, or the transistor), which can combine multiple signals into a single signal. Ideally, the switch should be asymmetrical, so that the input signal affects the output signal but not vice versa, and it should have a restoring quality, so that a weak or degraded input signal will not result in a degraded output. The second element, the connector, is the wire or pipe that carries a signal between switches. This connecting element must have the ability to branch, so that a single output can feed many inputs. These are the only two elements necessary to build a computer. Later we will introduce one more element — a register, for storing information — but this can be constructed of the same steering and connecting components.

FIGURE 8 Tinker Toy computer

I have never built a hydraulic computer, but once, with some friends, I did construct a computer out of sticks and strings. The pieces came from a children's construction set called Tinker Toys. Readers may remember this as a set of cylindrical wooden sticks that fit into fat little wooden hubs with holes in them. The logic of my Tinker Toy computer worked much like that shown in Figure 8. Like the switches-and-lights computer, the Tinker Toy computer played tic-tac-toe. It never lost. The computer was a lot of trouble to make, requiring tens of thousands of pieces from more than a hundred Tinker Toy「Giant Engineer」construction sets, and the finished product (now sitting in the Computer Museum in Boston, Massachusetts) looks incomprehensibly complex. Yet the principles on which it operates are just the simple combination of And and Or functions described above.

The big mistake I made in designing the Tinker Toy computer is that I did not use restoring logic  — that is, there was no amplification from one stage of logic to the next. The implementation of the logic was based on sticks pressing against sticks, in a design similar to the one illustrated in figure 4. Because of this design choice, all the force required to move the hundreds of elements in the machine had to be supplied by the press of the input switch. The accumulated force tended to stretch the strings that transmitted the motion, and because there was no restoration at each stage, the errors caused by the stretching accumulated from one logic element to the next. Unless the strings were constantly tuned, the machine would make mistakes.

I constructed a later version of the Tinker Toy computer which fixed the problem, but I never forgot the lesson of that first machine: the implementation technology must produce perfect outputs from imperfect inputs, nipping small errors in the bud. This is the essence of digital technology, which restores signals to near perfection at every stage. It is the only way we know — at least, so far — for keeping a complicated system under control.

万能工匠 —— 积木

除了神奇的微缩功能以外，采用硅芯片技术制造计算机并无其他特殊之处。无论采取何种技术，建造一台计算机只需两种大批量的元件：开关和连接器。开关是一种控向元件（比如液压阀、晶体管等），它可以将多个信号融合成一种信号。在理想的情况下，开关应该是非对称的，即输入信号能够影响输出信号，反之则不然。此外，开关应该具有复原的性质，这样当输入信号减弱时，就不会导致输出信号也随之减弱。连接器是一种能够在开关之间传输信号的电路或者管道，且必须具备分支转向的功能，这样才能将单个输出送至多个输入。建造一台计算机只需这两种元件便足矣。下文我们还将介绍一种元件 —— 寄存器，这是一种能存储信息的装置，它也可以由开关和连接器组装而成。

我虽然从未建造过液压计算机，但曾与同事一起用木棒和绳子组装过计算机。我们所用的材料来自一种名为「万能工匠」的儿童积木玩具。这些圆柱体木棒能够插入带孔的木质圆环中。与用开关和灯泡组成的游戏机一样，积木计算机也会玩井字游戏，并且还从未输过。建造这样的计算机可谓困难重重，因为所需的积木套件超过百套，其中的零件数目更是高达数万。目前，这台计算机的成品陈列于波士顿市计算机博物馆中。虽然它的复杂度足以令人瞠目结舌，但其所依赖的工作原理仍旧很简单，不过是上面提到的「与」功能和「或」功能的各种简单组合。

我在设计这台积木计算机时犯下了一个大错，那就是没有采用复原逻辑，也就是说，某一逻辑块与下一级逻辑块之间没有放大功能。我设计的逻辑功能是通过木棒之间的推动实现的，类似于图 1-4 中所使用的方法。这种设计方法决定了驱动计算机中数以百计元件的所有动力都来自输入开关的动力。累积的动力会将传递逻辑动能的绳索拉得非常紧。由于每个逻辑块之间没有放大功能，因此，由拉紧的绳索引起的偏差将会在逻辑块之间不断累积，除非不断地调整绳索，否则机器一定会出故障。

为了解决这个问题，我又建造了一台积木计算机。我从未忘记第一台计算机的教训：采用的技术必须能从不完善的输入中产生完善的输出，并将微小的误差消除在萌芽阶段。数字技术的真正精髓在于：每一级都能将信号复原并保持在完善的状态。目前为止，这是我们所知道的控制复杂系统的唯一方法。

### 1.5 Free to Worry about the Difference that makes a Diffierence

Naming the two signals in computer logic 0 and 1 is an example of functional abstraction. It lets us manipulate information without worrying about the details of its underlying representation. Once we figure out how to accomplish a given function, we can put the mechanism inside a「black box,」or a「building block」and stop thinking about it. The function embodied by the building block can be used over and over, without reference to the details of what's inside. This process of functional abstraction is a fundamental in computer design — not the only way to design complicated systems but the most common way (later, I'll describe an alternate method). Computers are built up of a hierarchy of such functional abstractions, each one embodied in a building block. The blocks that perform functions are hooked together to implement more complex functions, and these collections of blocks in turn become the new building blocks for the next level.

This hierarchical structure of abstraction is our most powerful tool in understanding complex systems, because it lets us focus on a single aspect of a problem at a time. For instance, we can talk about Boolean functions like And and Or in the abstract, without worrying about whether they are built out of electrical switches or sticks and strings or water-operated valves. For most purposes, we can forget about technology. This is wonderful, because it means that almost everything we say about computers will be true even when transistors and silicon chips become obsolete.

不必担忧那些非同小可的差异

将计算机逻辑的两种信号命名为 0 和 1，这是功能抽象原理的一个范例。这样，我们在处理信息时就无须考虑信号所代表的底层事物的具体细节。一旦我们掌握了如何实现某个给定的功能，就可以将实现机制放入一个「黑箱」或「构件」中，然后不再考虑它。我们可以不断反复使用构件中封装好的功能，而无须理会其内部的细节。这种功能抽象的过程是计算机设计的一项基本原则，它虽然不是设计复杂系统的唯一方法，却是最通用的一种方法（我还将在后文介绍另一种方法）。计算机的功能抽象层次结构是这样建造的：每种功能抽象都由一种构件体现。将具备某些功能的逻辑块互连起来便能实现更为复杂的功能，而这些逻辑块组合又会成为下一个层次的新构件。

这种功能抽象的层次结构是我们理解复杂系统的最有力的工具，有了它，我们每次只需关注一个方面的问题。例如，当我们在讨论抽象的「与」和「或」等布尔功能时，不必考虑这些逻辑功能是由电子开关、木棍和绳索，还是液压阀构成的。在大多数情况下，我们无须探讨技术问题。这是一个绝妙的方法，因为这意味着，即使晶体管和硅芯片等技术有一天会被淘汰，但对于计算机来说，我们所论述的一切将依然基本正确。

## 0201. Univeral Building Blocks

F rom now on, we can forget about wires and switches and work with the abstraction of logic blocks operating on 1's and 0's, a simple step that allows us to pass from the realm of engineering into the realm of mathematics. This is the most abstract chapter in the book; it will show you how the methods used to construct a tic-tac-toe machine can be used to construct almost any function. In it, we'll define a powerful set of building blocks: logical functions and finite-state machines. With these elements, it's easy to build a computer.

通用构件

关于线路和开关的介绍，我们先放到一边，接下来，我们从工程领域进入数学领域，探讨一下以 0 和 1 的形式运作的逻辑块的抽象原理。本章的内容是这本书最为抽象的一章，我将会向大家展示如何以建造井字游戏机的方法实现任何一种功能。我们还将定义一组功能强大的构件：逻辑功能和有限状态机。利用这些工具，我们可以轻松地构建出一台计算机。

### 2.1 Logical Funcitons

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

对于 n 个输入的二进制功能来说，其输入信号的可能组合共有 2^n 种。在一些情况下，我们不必费力将它们全部列举出来，因为某些输入组合我们无须去考虑。例如，当我们梳理井字游戏机的功能时，不会去考虑人类玩家同时走所有方格的情况。游戏规则禁止这种走法，因此我们不必为这种输入组合设定对应的输出。通过连接「与」「或」「非」等逻辑块，我们可以组合出各种复杂的逻辑块。在绘制连接图时，通常有三种不同形状的图例来表示这三类逻辑块（见图 2-1）。逻辑块左边的连线表示输入，右边的连线表示输出。图 2-2 描述了用一对两个输入的「或」逻辑块组合成一个三个输入的「或」逻辑块的过程。如果三个输入中有任意一个为 1，则这个逻辑功能的输出就为 1。我们可以用类似的方式将若干「与」逻辑块组合成一个多输入的「与」逻辑块。

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

计算机可以通过二进制位的组合表示任何信号，所需的二进制位数目取决于需要区分的信号的数目。例如，对于一台处理各类字符的计算机而言，5 个二进制位的输入信号可以表示 32 种不同的可能性（2^5=32）。计算机中用字符操作的功能有时会采用这种编码方式，不过它们更多地采用 7 个或者 8 个二进制位表示字母、标点符号、数字等。大多数现代计算机都采用一种标准的编码方式，即 ASCII 编码，其全称为美国国家信息交换标准码（American Standard Code for Information Interchange，简称 ASCII）。在 ASCII 编码中，1000001 表示大写字母 A，1000010 表示大写字母 B，依此类推。当然，也可以采用其他编码方式。

大多数计算机都有一种或多种表示数字的编码方式，最为常见的是以 2 为基的数字编码方式，在这种表示方法中，序列 0000000 表示十进制数 0，序列 0000001 表示十进制数 1，依此类推。我们常用 32 位或者 64 位来描述计算机，这两个数字代表计算机电路表示数字时同时处理的二进制位的数目：一台 32 位的计算机使用 32 位表示一个以 2 为基的数字。虽然以 2 为基的数字系统是一种通用惯例，但这并不意味着必须采用这种方式。而且，出于各种原因，许多采用这种方式的计算机也会采用其他的数字表示方式。比如，许多计算机会采用一种略微不同的方式来表示负数，并且会用一种称为浮点数（floating point）的数字来表示带小数点的数字。小数点在浮点数中的位置可以左右「浮动」，因此一定数目的位数可以表示很大范围的数值。为了简化执行算术运算的线路逻辑，以及更方便地转换数字表示形式，我们一般会采取与之对应的数字表示形式。

由于布尔逻辑可以实现所有的逻辑功能，因此采用任何表示形式的二进制数都可以构建出能够执行加法、乘法等运算的逻辑块。例如，如果我们要在一台 8 位计算机中构建一个能完成数字加法运算的逻辑块，那么这个 8 位加法逻辑块必须具有 16 个输入信号（每个加数都有 8 个输入信号）和 8 个输出信号作为加法的和。由于每个数字都由 8 个二进制位来表示，因此存在 256 种组合，每种组合代表不同的数字。例如，我们能用这些组合表示 0～255 的数，或者 -100～154 的数。若想定义加法块的功能，只需先写出加法表，然后根据所选择的表示形式将表中的数字转化为由 1 和 0 组成的数字串，最后再用前面描述的方法将 1 和 0 组成的数字串转换为对应的「与」「或」逻辑块。

如果在上述的逻辑块中再添加两个控制输入，我们便可以构建出能同时完成加法、减法、乘法和除法运算的逻辑块。这两个附加的控制输入用于指定要执行的运算类型。例如，对于表中控制输入为 01 的每一行，我们可以将其输出定义为两个输入数字的和；对于表中控制输入为 10 的每一行，我们可以将其输出定义为两个输入数字的乘积，依此类推。大多数计算机都有这类逻辑块，常常被称为运算器（arithmetic unit）。

依据上述方法来组合「与」「或」逻辑块，我们便可以实现任何一种逻辑功能。不过，这虽然是一种可行的方法，但不是最有效的。通过巧妙的设计，我们可以采用比上述方法所需构件更少的方法来搭建线路，而且，还可以采用其他类型的构件，或者将输入至输出的线路延迟时间减至最低程度。在设计逻辑功能的过程中，我们通常会碰到一些典型的难题：如何用「与」逻辑块和「非」逻辑块构建出「或」逻辑块？（这个很简单）如何用一组「或」逻辑块和「与」逻辑块以及两个「非」逻辑块实现一个具有三个「非」逻辑块的功能？（这个比较困难，但可以实现。）在计算机设计过程中，我们经常会遇到这类难题，不过，这也正是使设计过程变得有趣的地方。

### 2.2 Finite-State Machines

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

2『这里才算是自己第一次弄懂有限状态机的概念，做一张术语卡片。（2021-10-10）』—— 已完成

密码锁就是一个简单的有限状态机。密码锁的状态是输入锁中的数字序列的总体。密码锁不会记住先前输入的所有数字，只需记住最近一次输入的数字，并且知道这些数字组成的序列何时可以打开密码锁。更简单的有限状态机是伸缩式圆珠笔，它只有两种状态 —— 伸出和缩进，并且圆珠笔会记住按钮被按了奇数次还是偶数次。所有有限状态机都具有一组固定的可能状态集合、一组可改变状态的允许输入集合（例如，按下圆珠笔按钮，向密码锁中输入数字等），以及一组可能的输出集合（例如，圆珠笔笔尖的伸出和缩进，打开密码锁等），这些输出只取决于状态，而状态又只取决于过去的输入序列。

有限状态机的另外一个简单范例是计数器，例如旋转门上安装的计数器可以记录通过的人数。每当有人通过这个旋转门时，计数器的状态就会更新一次。这种计数器的状态是有限的，因为它能记录的数位是有限的。当它的计数值达到最大值时，比如最大数值为 999，再进一个人便会更新为零。汽车的行驶里程表的工作原理也与之类似。我曾经开过一辆老式的出租车，其里程表读数为 70 000，但我搞不清楚这辆车到底行驶了 70 000 英里（1 英里约为 1.6 千米）、170 000 英里，还是 270 000 英里。因为这个里程表只有 100 000 种状态。对这个里程表而言，上述历史记录都是一样的。正是出于这个原因，数学家通常会将一种状态定义为「一些等值历史的集合」。

其他常见的有限状态机还包括交通信号灯、电梯按钮等。在这些有限状态机中，状态序列是由内置的时钟和输入按钮共同决定的，这些输入按钮包括人行道上设置的「行人」按钮和电梯中的「呼救」及「楼层选择」按钮。有限状态机下一时刻的状态不仅取决于前一时刻的状态，还取决于输入按钮的信号。在有限状态机中，状态之间的转换由一组固定的规则来确定，通过简单的状态图，我们可以表示出状态的转换过程。图 2-5 展示了交通信号灯的状态图，当按下「行人」按钮后，两个方向都亮起红灯。图中每个信号灯图示表示一种状态，每一个箭头表示状态之间的转换，而状态的转换取决于「行人」按钮是否被按下。

为了存储有限状态机的状态，我们还需要引入一种用于存储二进制位的构件 —— 寄存器（register）。一个 n 位的寄存器具有 n 个输入和 n 个输出，以及一个额外的时序输入，这个时序输入能够告知寄存器更新状态的时间。存储新信息的过程就是将状态「写入」寄存器的过程。当时序信号传递到寄存器，通知其「写入」一种新状态时，寄存器便会根据输入信号改变其状态。寄存器的输出始终与寄存器的内部状态同步。寄存器有很多种实现方式，其中一种是通过布尔逻辑块来控制状态信息，使其在一个闭合圈中不断循环。电子计算机通常采用这种寄存器，这也是当计算机的电源被中断时经常丢失正在处理的信息的原因。

图 2-6 中的有限状态机由一个布尔逻辑块和一个寄存器连接而成。有限状态机将布尔逻辑块的输出「写入」寄存器，以此完成状态的更新；然后，布尔逻辑块根据寄存器的当前状态和当前的输入来计算下一个状态；接下来，计算出的状态值会在下一个周期被「写入」寄存器。上述过程会随着每一个周期重复进行下去。

图 2-6 逻辑块和寄存器连接成的有限状态机

有限状态机的功能可以通过这样一个表来表示：表中每种状态和每种输入信号与下一个状态相对应。例如，我们可以通过表 2-5 来表示交通信号灯控制器的运算过程。

表 2-5 交通信号灯的状态表

实现有限状态机的第一步是建立这样的表格，第二步是为每种状态设定不同的二进制位组。交通信号灯控制器共有 5 种状态，这就需要使用三个二进制位来表示。由于每增加一个二进制位就能使状态数目翻倍，故 n 个二进制位最多能存储 2^n 种状态。将上表中的所有状态都替换为二进制位组之后，就能将此表转化为由布尔逻辑实现的功能。

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

## 0301. Programming

T he magic of a computer lies in its ability to become almost anything you can imagine, as long as you can explain exactly what that is. The hitch is in explaining what you want. With the right programming, a computer can become a theater, a musical instrument, a reference book, a chess opponent. No other entity in the world except a human being has such an adaptable, universal nature. Ultimately all these functions are implemented by the Boolean logic blocks and finite-state machines described in the previous chapter, but the human computer programmer rarely thinks about these elements; instead, programmers work with a more convenient tool called a programming language.

Just as Boolean logic and finite-state machines are the building blocks of computer hardware, a programming language is a set of building blocks for constructing computer software. Like a human language, a programming language has a vocabulary and a grammar, but unlike a human language there is an exact meaning in the programming language for every word and sentence. Most programming languages are universal, in the same sense that Boolean logic is universal: they can be used to describe anything a computer can do. Anyone who has ever written a program — or debugged a program — knows that telling a computer what you want it to do is not as easy as it sounds. Every detail of the computer's desired operation must be precisely described. For instance, if you tell an accounting program to bill your clients for the amount that each owes, then the computer will send out a weekly bill for `$`0.00 to clients who owe nothing. If you tell the computer to send a threatening letter to clients who have not paid, then clients who owe nothing will receive threatening letters until they send in payments of $0.00. Avoiding this kind of misunderstanding is what computer programming is all about. The programmer's art is the art of saying exactly what you want. In this example, it means making a distinction between clients who have not sent in any money and clients who actually owe money. To paraphrase Mark Twain, the difference between the right program and the almost-right program is like the difference between lightning and a lightning bug — the difference is just a bug.

A skilled programmer is like a poet who can put into words those ideas that others find inexpressible. If you are a poet, you assume a certain amount of shared knowledge and experience on the part of your reader. The knowledge and experience that the programmer and the computer have in common is the meaning of the programming language. How the computer「knows」the meaning of the programming language will be described later; first, we will discuss the grammar, vocabulary, and idioms of such languages.

计算机的神奇之处在于，只要你能精确地描述出你所想象的东西，计算机就能将其变幻出来。问题的关键在于，如何描述你所想要的东西。只要程序编写正确，计算机就能摇身一变，成为一家剧院、一件乐器、一本参考书，甚至成为一名国际象棋高手。除了人类以外，世界上没有任何实体能拥有如此高的适应性和通用性。这些功能的实现离不开布尔逻辑块和有限状态机。不过，程序员通常不会考虑这些因素，而是会借助一种更为便捷的工具来实现所需的功能，那就是编程语言。

正如布尔逻辑块和有限状态机是计算机硬件的通用构件，编程语言是计算机软件的通用构件。与人类语言一样，编程语言也具有自身的词汇和语法。不过，不同于人类的语言，编程语言中的每个词汇和语句的含义具有唯一性。正如布尔逻辑具有通用性，大多数编程语言也是如此：它们可以用来描述计算机能做的所有事情。所有编写过或者调试过程序的人都知道，让计算机完成交给它的任务绝非易事，你必须精确地描述出计算机所要操作的所有细节。例如，如果你让记账程序将顾客的欠款以账单的形式寄给他们，那么那些从未赊账的顾客每周也会收到金额为 0 美元的账单。如果你让计算机给那些没有付款的顾客寄去一封催款通知，那么那些没有任何欠款的顾客也会收到金额为 0 美元的催款通知。所谓计算机编程，就是要避免以上这类错误。所谓编程艺术，就是将心中所想精确地告知计算机的艺术。在这个例子中，程序员需要让程序区分出欠款但未还款的顾客和未欠款的顾客。借用马克·吐温的话来说就是，正确的程序和几乎正确的程序之间的差异就像闪电和闪电虫之间的差异，差异本身就是一个问题。

技艺精湛的程序员就诗人一样，能将别人无法形容的思想付诸文字。如果你是一位诗人，就能和读者共享某些知识和体验。程序员和计算机之间共享的知识和体验就是编程语言的含义。我们将会在后文探讨计算机是如何「获知」编程语言所表达的含义的，接下来先讨论编程语言的语法、词汇和常用语。

### 3.1 Talking to The Computer

There are many different programming languages. The main reasons for this diversity are history, habit, and taste, but different programming languages also exist because they are good at describing different kinds of things. Each language has its own syntax. You need to learn the syntax in order to write the language, but (like spelling and punctuation in a human language) syntax is not fundamental to the meaning or the expressive power of the language. What is important to the expressive power of the language is the vocabulary — the so-called primitives of the language — and the way the primitives can be combined to define new concepts.

Programming languages describe the manipulation of data, and one way in which these languages differ is in the kinds of data they can manipulate. The earliest computer languages were designed primarily to manipulate numbers and sequences of characters. Latter-day programming languages can manipulate words, pictures, sounds, and even other computer programs. But no matter what sort of data the language is designed to handle, it typically provides a way of reading the data's elements into the computer, taking the data apart, putting them together, modifying them, comparing them, and giving them names.

It's probably easier to illustrate these abstractions by describing a particular computer language — I've chosen Logo, which was designed by the educator and mathematician Seymour Papert as a computer language for children. Children can write programs in Logo which create and manipulate pictures, words, numbers, and sounds. Although the language is simple enough to be used by a ten-year-old, it embodies many of the features of the most sophisticated computer languages, including the ability to write programs that manipulate other programs. Logo is also an extensible language — that is, you can use Logo to define new words in Logo.

One of the simplest types of programs to write in Logo is a procedure for drawing a picture. You do this by giving directions to an imaginary turtle that lives on the screen. The turtle serves as a pen, moving around on the screen and leaving lines behind it. When the computer starts up, the turtle is found at the center of the screen, facing upward. If the child types the command FORWARD 10, the turtle takes ten steps forward — that is, upward — drawing a line ten units long. The number 10 following the FORWARD command is called a parameter; in this case, the parameter tells the turtle how many steps to take. To draw a line in a different direction, the child must turn the turtle. The command RIGHT 45 will point the turtle 45 degrees (another parameter) to the right from its last heading. The next FORWARD command, with its parameter, will then draw a line in the new direction.

The child can use commands like FORWARD, BACKWARD, RIGHT, and LEFT to move the turtle around the screen and draw pictures, but this involves a lot of typing and soon becomes tedious. What makes the language interesting is its ability to define new words: for example, here's how the child could teach the turtle (program the computer) to draw a square:

```
TO SQUARE

FORWARD 10

RIGHT 90

FORWARD 10

RIGHT 90

FORWARD 10

RIGHT 90

FORWARD 10

END
```

FIGURE 18 A square

Having defined the word「square,」the child can then draw a square with ten units on a side simply by typing a new command: SQUARE. (Needless to say, the name「square」is arbitrary; the child could just as well have called the procedure BOX or XYZ and the turtle would do exactly the same thing. When children discover this, they often enjoy「fooling」the computer — for instance, calling the procedure that draws a square TRIANGLE, and vice versa.)

Once the word「square」has been defined, it becomes part of the computer's vocabulary and can then be used to define other words. For example,

```
TO WINDOW

SQUARE

SQUARE

SQUARE

SQUARE

END
```

Each square will be drawn in a different place, because the procedure for drawing the square leaves the turtle rotated 90 degrees. In computer terms, SQUARE is a subroutine of the program WINDOW, which calls it. The subroutine SQUARE, in turn, is defined using the primitives FORWARD and RIGHT. User-defined words in Logo can take parameters, too. For instance, a child can specify various sizes of square by specifying what parameter determines the length of each side.

```
TO SQUARE :SIZE

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

END
```

FIGURE 19 A window, made of four squares

The colon in front of the command SIZE is an example of syntax. In Logo, the colon indicates that the word that follows is the name of a parameter, representing something else — in this case, the number to be supplied each time we「call」the subroutine named SQUARE. When SQUARE is defined this way, the command SQUARE 15 will tell the computer to draw a square fifteen units on a side. The parameter name SIZE is, again, an arbitrary name and has meaning only within the definition of SQUARE: if all five occurrences of SIZE were replaced with X, say, the subroutine would do exactly the same thing.

FIGURE 20 A design, drawing in progress

There are other ways of writing a subroutine to draw a square. For instance, you can instruct the turtle to turn left four times, or to go backward four times. What's interesting is that it doesn't matter how SQUARE is defined; all that matters is what the subroutine draws and where it leaves the turtle. Other programs can call the SQUARE no matter how it is defined and whether or not it is a user-defined word or one of the language's primitives. In extending the language, the programmer uses the power of functional abstraction to create new building blocks.

One of the tricks that Logo-using children discover is that they can insert a word inside its own definition, a practice known as recursion. For instance, a child might generate a circular design consisting of many rotated squares, as follows:

```
TO DESIGN

SQUARE

RIGHT 10

DESIGN

END
```

The computer follows the DESIGN command by drawing a square, then turning the turtle 10 degrees and drawing another「design」in the same way. In this case, the recursive definition of「design」has a problem: it goes on forever. Each time the computer responds to the DESIGN command it draws a square, and then it must go on to another design, and on and on ad infinitum — rather as in the story of the guru who claimed that the earth was sitting on the back of (as it happens) a giant turtle.「And what is the turtle sitting on?」asked a student.「Another turtle,」replied the guru.「And that turtle?」asked the student, beginning to grow skeptical.「It's no use asking,」said the guru.「It's turtles all the way down.」

The computer, in drawing the design, goes through the same process that human beings go through in trying to imagine the infinite stack of giant turtles, but the computer is not smart enough to notice that it's not getting anywhere. It will not halt until it is interrupted — an example of a common sort of program behavior called an infinite loop. Programmers often create infinite loops accidentally, and (as we shall see) it can be extremely difficult to predict when such loops will occur. This particular infinite loop is easily avoided by writing the program with a parameter specifying how many squares to draw.

```
TO DESIGN :NUMBER

SQUARE

RIGHT 10

IF :NUMBER = 1 STOP ELSE DESIGN :NUMBER −1

END
```

Thus defined, the DESIGN subroutine will do one of two things, depending on whether its parameter is 1 or some higher number. DESIGN 1 will draw just one square, but DESIGN 5, say, will draw a square, rotate, and then draw a DESIGN 4. DESIGN 4 will draw a square and then a DESIGN 3, and so on down to DESIGN 1, which will draw a square and stop.

This kind of recursive definition with a changing parameter is useful for producing anything that has a self-similar structure. A picture that contains a picture of itself is an example of a recursive, self-similar structure; such structures are commonly known as fractals. In the real world, self-similar structures don't go on forever: for instance, each branch of a tree looks a lot like a smaller tree, and each of these smaller branches has branches that look like still smaller trees. This recursion goes on for several levels, but eventually the branches are so small that they do not have branches of their own.

A recursive Logo program for drawing a tree is shown below. This may give you some idea of how a computer program can contain an element of poetry — although in this case the theme is somewhat obscured by the details of positioning the turtle and bringing it back to the starting point. Here's a rough translation of what the program says:「A big tree is a stick with two smaller trees on top, but a little tree is just a stick.」The picture produced by the tree program is shown next to it.

```
TO TREE :SIZE

FORWARD :SIZE

IF :SIZE <1 STOP ELSE TWO-TREES SIZE/2

BACK :SIZE

END

FIGURE 21

A tree

TO TWO-TREES :SIZE

LEFT 45

TREE :SIZE

RIGHT 90

TREE :SIZE

LEFT 45

END
```

This technique of defining things recursively turns out to be very powerful. Many of the types of data we like to manipulate — in particular, computer programs themselves — have recursive structures. Recursive definitions are extremely convenient for specifying operations on recursive data. The typical recursive definition has two parts — the first part describes what is to happen in a particular simple case, and the second describes how a more complex case can be reduced to something simpler. In the recursive tree, for example, the simple case is the tree smaller than 1 and the more complex case is the tree composed of a trunk and two small trees.

Another example is the definition of a palindrome, which we can define as follows: A word is a palindrome if it has less than two letters (the simple case) or if its first and last letter are the same and the letters in the middle form a palindrome (the recursive step). The simplest way to write a Logo program for recognizing palindromes would be to use this recursive definition.

There are many other computer languages: LISP, Ada, FORTRAN, C, ALGOL, and the like; most of the names are obscure acronyms (such as FORTRAN, for FORmula TRANslation, and LISP, for LISt Processing). Although these languages differ from Logo in details of vocabulary and syntax, they can all express the same kinds of procedures. Some, like FORTRAN, are limited in their ability to define operations recursively or to manipulate non-numerical data. Others, like C and LISP, allow the programmer to manipulate the underlying bits representing the data, which gives the programmer more power — and more opportunity to make mistakes. In C, for example, it's perfectly possible to multiply two alphabetic characters; the result of this nonsensical operation will depend on the binary representation used by the machine. Languages like LISP offer the abstract as well as the lower-level functions. As a friend of mine, the computer scientist Guy Steele, once put it,「LISP is a high-level language, but you can still feel the bits sliding between your toes.」

More recently, a new generation of languages has begun to emerge. These languages — Small-Talk, C++, Java — are object-oriented. They treat a data structure — for instance, a picture to be drawn on the screen — as an「object」with its own internal state, such as where it is to be drawn or what color it is. These objects can receive instructions from other objects. To understand why this is useful, imagine that you are writing a program for a video game involving bouncing balls. Each ball on the screen is defined as a different object. The program specifies rules of behavior that tell the object how to draw itself on the screen, move, bounce, and interact with other objects in the game. Each ball will exhibit similar behavior, but each will be in a slightly different state, because each will be in its own position on the screen and will have its own color, velocity, size, and so forth.

The most important advantage of an object-oriented programming language is that the objects — for instance, various objects in a video game — can be specified independently and then combined to create new programs. Writing a new object-oriented program sometimes feels a bit like throwing a bunch of animals into a cage and watching what happens. The behavior of the program emerges , as a result of the interactions of the programmed objects. For this reason, as well as the fact that object-oriented languages are relatively new, you might think twice about one for writing a safety-critical system that flies an airplane.

Learning a programming language is not nearly as difficult as learning a natural human language. Generally, once you have learned two or three, you can pick up others in a matter of a few hours, since the syntax is relatively simple and the vocabularies are rarely more than a few hundred words. But, as is true of a human language, there's a big difference between being able to understand the language and being able to write it well. Every computer language has its Shakespeares, and it is a joy to read their code. A well-written computer program possesses style, finesse, even humor — and a clarity that rivals the best prose.

与计算机对话

编程语言的种类有很多，这种现象主要是由历史、习惯和品味等因素引起的。此外，不同编程语言善于描述不同类型的事物，这也是存在多种编程语言的原因之一。每种编程语言都有自己的语法。只有掌握了编程语法之后，我们才能编写程序，编程语法就如同人类语言中的拼写和标点。不过，对于编程语言的含义和表达来说，语法并非关键所在，更为重要的是词汇，也叫语言的原语（primitive），以及将这些原语组合形成新概念的方法。

所有的编程语言都会对所处理的数据进行描述，它们之间的区别在于各自所能处理的数据类型是不同的。最早的编程语言主要用于处理数字和字符串，之后的编程语言可以处理文字、图像、声音，甚至其他计算机程序。不过，无论编程语言被用于处理何种数据类型，它通常都会提供一种方式来读取、分离、整合、修改、计算和命名数据。

为了更形象地说明上述的抽象概念，我们以一个具体的计算机编程语言为例 ——Logo 语言。这种编程语言是由教育学家、数学家西摩·帕佩特（Seymour Papert）专为儿童设计的，可以用于编写程序来创建和处理图片、文字、数字和声音等。对于 10 岁的孩子来说，这种编程语言虽然十分简单，但同样具有最复杂的计算机编程语言的许多功能，比如编写可以控制其他程序的程序。Logo 语言还是一种可扩展语言，也就是说，你可以通过 Logo 原语定义新的词语。

海龟绘图程序是用 Logo 语言编写的最简单的程序之一。你可以给屏幕上的海龟下达指令，这只海龟就如同一支画笔，在屏幕上留下移动轨迹。当程序启动后，海龟头部朝上且位于屏幕中央。如果小孩输入指令「FORWARD10」，海龟就会向前迈出 10 步，也就是说，向上画出一条长度为 10 个单位的直线。「FORWARD」指令后面的数字 10 被称为参数。在这个例子中，参数规定了海龟应该往前走多少步。为了在不同的方向上画出直线，小孩必须调整海龟的前进方向。指令「RIGHT45」会使海龟自原来的朝向向右转 45 度（这也是一个参数）。如果再输入一个带参数的指令「FORWARD」，海龟就会在新方向上画出一条直线（见图 3-1）。

图 3-1 海龟绘图程序

当小孩输入「FORWARD」「BACKWARD」「RIGHT」「LEFT」等指令时，海龟就会在屏幕上依次向上、下、右、左移动，画出各种图像。然而，这样的操作需要输入大量指令，很快就会使人感到枯燥乏味。Logo 语言有趣的地方在于，它能够定义新指令。例如，小孩可以利用如下指令教会海龟（即为计算机写程序）画出一个正方形（见图 3-2）。

在定义完「正方形」这个词之后，小孩子只需输入新指令「SQUARE」（正方形），海龟便能画出一个边长为 10 个单位的正方形。毋庸讳言，指令「SQUARE」可被改为其他任意名字。即使小孩将指令命名为「箱子」或者「XYZ」，海龟还是会完成一模一样的动作。当小孩发现这一点后，会经常「戏耍」计算机取乐。比如，将画正方形的指令命名为「TIANGLE」（三角形），反之亦然。

一旦定义了「SQUARE」这个词，它就成了计算机词汇库中的一员，我们就可以用它来定义新指令，例如可以用它来定义「WINDOW」，即窗户（见图 3-3）。

根据以上这些指令，海龟便会绘制出位于不同位置的 4 个正方形，因为每画完一个正方形，海龟会旋转 90 度。用计算机术语来说，「SQUARE」是程序「WINDOW」的一个子程序，后者调用了前者，而子程序「SQUARE」又是基于原语「RIGHT」和「FORWARD」定义出来的。用户自定义的指令也带有参数。比如，小孩可以设定正方形的边长，并画出不同大小的正方形。

在上述指令中，冒号是 Logo 语言的语法之一，表示其后紧跟的词是一个参数的名称，而且这个词表示的含义与冒号前的词有所不同。在这个例子中，冒号是指调用「SQUARE」子程序时所提供的一个参与值。当定义好「SQUARE」之后，指令「SQUARE15」会指示计算机画出一个边长为 15 个单位的正方形。同样，这里的参数名称「SIZE」也是任取的，但它只有在指令「SQUARE」中才有意义。如果上述指令中的「SIZE」被字母「X」替代，那么这个子程序的功能将与原先完全相同。

编写正方形的子程序不止一种。例如，我们可以命令海龟向左转 4 次或者向后转 4 次来画出一个正方形。有趣的是，「SQUARE」指令的定义方式并不重要，它所绘制的内容以及将海龟置于何处才是关键所在。无论「SQUARE」是如何被定义的，以及它是否属于用户自定义的指令或者程序原语之一，其他程序都能调用这个指令。在扩展编程语言的过程中，程序员可以通过功能抽象的方法来创造新的构件。

在学习 Logo 语言时，小孩还会发现一个诀窍，那就是在指令的定义中插入这个指令本身，这被称为递归。例如，小孩可以设计出一个由许多旋转的正方形组成的循环指令：「DESIGN」，即设计（见图 3-4）。

图 3-4 指令「DESIGN」的执行过程

当计算机接收到指令「DESIGN」后，首先会画出一个正方形，然后将海龟右转 10 度，并以同样的方式执行下一个指令「DESIGN」。在这种情况下，指令「DESIGN」的递归定义存在一个问题：它将会永远地执行下去。计算机每次接收到指令「DESIGN」后都会画出一个正方形，然后执行下一个指令「DESIGN」，这是一个不断循环往复的过程。一位智者曾说：「地球驮在一只巨大的海龟的背上。」「那么是什么支撑着这只海龟呢？」有一个学生提出了疑问。「另一只海龟。」大师答道。「那么又是什么支撑着这一只海龟呢？」学生又问道。「这种追问没有意义，」大师说道，「海龟下面永远是海龟。」

计算机执行指令「DESIGN」的过程，就如同无穷多个巨大的海龟堆叠在一起的情形，因为计算机不够智能，它无法预知这是一个永无止境的过程。在这个程序被中断之前，它会一直运行下去。这个例子反映了计算机程序的一种常见特征 —— 无限循环。在通常情况下，程序员一不留神就会让程序陷入无限循环，而提前预判出何时会出现这种循环，则极其困难（我们会在后面章节详细讨论这一点）。不过，若想避免这种情况也不难，只要在程序中增加一个用于指定正方形数目的参数即可。

通过上面的定义，「DESIGN」程序会根据参数是否为 1 或者大于 1 来执行如下两项操作中的一个。指令「DESIGN1」只会画出一个正方形，而指令「DESIGN5」会先画出一个正方形，然后旋转，再执行指令「DESIGN4」。指令「DESIGN4」也会先画出一个正方形，然后再执行指令「DESIGN3」，以此类推，直至执行完指令「DESIGN1」，程序才终止。

这种带可变参数的递归定义可用于生成具有自相似结构的对象。一张包含自身图像的图像就是一种具有自相似结构的示例。这类结构通常被称为分形（fractal）。在现实世界中，自相似结构不会永远递归下去。例如，虽然树的每个分支看起来像一棵较小的树，而且这些分支的分支看起来像更小的树，但这种递归过程只会重复几次，最终的分支会非常小，不会再产生新的分支。

图 3-5 表示的是可以绘制树的递归 Logo 程序。这个程序会让你体验到计算机程序中蕴含的诗意，即屏幕上移动的海龟及其最后返回起点的画图方式在一定程度上模糊了这一主题。这段程序表达的大致意思是：「大树，一个上面长出两棵小树的主干；小树，一个主干而已。」

图 3-5　用递归 Logo 程序绘制的树

这种递归定义事物的技术具有很强大的功能。我们要处理的许多数据类型都具有递归结构，尤其是计算机程序本身。递归定义十分便于描述递归数据运算。典型的递归定义包含两个部分：第一部分描述了简单情形的运算，第二部分描述了如何将复杂的情形转化为更简单的情形。例如，在递归树的例子中，最简单的情形是参数小于 1 时的树，复杂的情形则是由树干和两个分支组成的树。

回文的定义是递归定义的另一个例子，其定义为：如果某个词的字母数少于两个，或者这个词的首字母和尾字母相同，且中间字母也是回文（递归定义），那么这个词就是回文。若想编写 Logo 程序来识别回文，最简单的方法就是使用这种递归定义。

计算机编程语言还包括 LISP、Ada、FORTRAN、C、ALGOL 等语言，其中大多数名称源于英文首字母的缩写。例如，FORTRAN 是 FORmula TRANslation 的缩写，LISP 是 LIST Processing 的缩写。尽管这些编程语言在词汇和语法等细节上与 Logo 语言有所不同，但它们都可以定义相同类型的程序。有些编程语言在定义递归运算和处理非数值数据方面的能力有所欠缺，例如 FORTRAN。有些编程语言允许程序员直接处理二进制表示的数据，这赋予了程序员更大的权力，但同时也增加了犯错误的可能性，比如 C 和 LISP。例如，在 C 语言中，虽然将两个字符变量相乘是可行的，但这一操作不具有实际意义，其结果取决于计算机使用的二进制编码方式。像 LISP 这样的编程语言不仅具备低级功能，还具备抽象功能。计算机学者盖伊·斯蒂尔（Guy Steele）曾说过：「LISP 是一种高级编程语言，不过，你依然可以在指尖间感受到滑动的二进制位。」

新一代编程语言已经崭露头角，它们都是面向对象的，比如 Small-Talk、C++、Java。这些编程语言都将数据结构当作一个具有自身内部状态的「对象」，例如将在屏幕上绘制的图片，这些内部状态包含图片的位置、颜色等属性。这些对象可以接收来自其他对象的指令。我们通过下面这个例子来了解这种方法的有效性。假设你正在编写一款涉及弹跳球的图示游戏，屏幕上的每个球都被定义为不同的对象。该程序规定了弹跳球的行为准则，并明确了对象如何在屏幕上显示、移动、反弹，以及与游戏中其他对象交互。每个球虽然会呈现出相似的行为模式，但所处的状态略有不同，这是因为每个球在屏幕中有其自身的位置、颜色、速度、大小等。

面向对象的编程语言最突出的优点是：对象可以被单独定义并组合成新程序，如图示游戏中的各种对象。编写一个面向对象的新程序的过程，就如同将一群动物关进一个笼子中，并观察发生的事情。编程对象之间的交互作用造就了程序的行为。由于这个原因，加上面向对象的编程语言相对较新，因此你在用它编写安全第一的飞机自动驾驶系统时，要三思而行。

学习编程语言并不像学习人类语言那样困难。一般来说，一旦你学会了两三门编程语言，就能在几小时内掌握其他的编程语言。这其中的原因在于，编程语言的语法相对简单，词汇量很少超过几百个单词。不过，就像学习人类语言一样，理解了编程语言并不意味着就能将其用于实践。每种计算机编程语言的领域都有相应的大师，阅读这些大师的代码是一种享受。写得好的代码自有其风格和技巧，甚至幽默，也可能具有优美散文般的清澈明朗。

### 3.2 Making the Connection

How can finite-state machines be used to carry out instructions written in a language like Logo? To answer this question, we go back to a more detailed level of discussion, involving Boolean logic. There are three major steps in this connection between finite-state machines and Logo: first , we will see how a finite-state machine can be extended, by adding a storage device called a memory , which will allow the machine to store the definitions of what it's asked to do; second , we will see how this extended machine can follow instructions written in machine language , a simple language that specifies the machine's operations; and third , we will see how machine language can instruct the machine to interpret the programming language — for instance, Logo. The rest of the chapter describes how all this works in some detail — far more detail than is strictly necessary to understand the rest of the book. The reader should not feel compelled to understand every step. The important thing to appreciate is how the layers of functional abstraction build upon one another, as is summarized in the last paragraph of the chapter.

A computer is just a special type of finite-state machine connected to a memory. The computer's memory — in effect, an array of cubbyholes for storing data — is built of registers , like the registers that hold the states of finite-state machines. Each register holds a pattern of bits called a word , which can be read (or written) by the finite-state machine. The number of bits in a word varies from computer to computer, but in a modern microprocessor (as I write this) it is usually eight, sixteen, or thirty-two bits. (Word sizes will probably grow with improvement in technology.) A typical memory will have millions or even billions of these registers, each holding a single word. Only one of the registers in the memory is accessed at a time — that is, only the data in one of the memory registers will be read or written on each cycle of the finite-state machine. Each register in the memory has a different address  — a pattern of bits by means of which you can access it — so registers are referred to as locations in memory. The memory contains Boolean logic blocks, which decode the address and select the location for reading or writing. If data are to be written at this memory location, these logic blocks store the new data into the addressed register. If the register is to be read, the logic blocks steer the data from the addressed register to the memory's output, which is connected to the input of the finite-state machine.

Some of the words stored in the memory represent data to be operated upon, like numbers and letters. Others represent instructions that tell the machine what sequence of operations to perform. The instructions are stored in machine language, which, as noted, is much simpler than a typical programming language. Machine language is interpreted directly by the finite-state machine. In the type of computer we will describe, each instruction in machine language is stored in a single word of memory, and a sequence of instructions is stored in a block of sequentially numbered memory locations. These sequences of machine-language instructions are the simplest kind of software within the computer.

The finite-state machine repeatedly executes the following sequence of operations: (1) read an instruction from the memory, (2) execute the operation specified by that instruction, and (3) calculate the address of the next instruction. The sequence of states necessary to do this is built into the Boolean logic of the machine, and the instructions themselves are specific patterns of bits — patterns that cause the finite-state machine to perform various operations on the data in the memory. For instance, the Add instruction is a unique pattern of bits that specifies which two registers in the memory are to be added together. Upon recognizing this pattern, the finite-state machine will go through a sequence of states that cause it to read the memory locations to be summed, add the numbers together, and write the sum back to the memory.

FIGURE 22

Finite-state machine connected to a memory

There are two basic types of instructions in most computers: processing instructions and control instructions. The processing instructions move data to and from the memory and combine them to perform arithmetic and logical functions. The addresses of the memory locations, or registers, are specified by the processing instructions. Typically, these instructions refer to only a few registers directly; other registers are referenced indirectly, because their addresses are stored in other registers. For example, a Move instruction might move the data in register 1 to the address specified in register 2. If register 2 holds a pattern of bits that specifies the number 1,234, then the data will be moved to register 1,234. Other processing instructions combine data among the memory registers. There are also instructions to perform Boolean functions — And, Or, or Invert — on the patterns of bits in the registers.

The control instructions determine the address of the next instruction to be fetched; this address is stored in a special register called the program counter. Normally, instructions are fetched sequentially from successive memory locations, so the address in the program counter increases by 1 after each successive instruction. Control instructions allow some other number to be loaded into the program counter, thereby affecting the sequence to be executed. The simplest control instruction is the Jump instruction, which stores a specified address in the program counter so that the next instruction will be fetched from that address. A variation of the Jump instruction is a conditional Jump , which loads the program counter with a different address only when a specified condition has been met — such as the patterns in two registers being the same. If the condition is not met, then the conditional Jump will have no effect and the next instruction will be fetched sequentially.

If the same sequence of instructions needs to be executed over and over repeatedly, then a conditional Jump can be used at the end of the sequence to move the program counter back to the beginning as many times as is necessary. This operation is called a loop , and we saw an example of it in the description of programming in Logo. The execution of the sequence will be repeated until the condition on which the jump depends is no longer satisfied. If a set of instructions is to be repeated ten times, say, one of the memory registers can be used to count the number of iterations of the loop.

Exactly which instructions a computer recognizes varies from computer to computer. Computer designers can (and do) spend years arguing about what makes an optimal instruction set. A typical argument is over the comparative merits of a reduced instruction set computer (RISC), which uses a simple, minimal set of instructions, and a complex instruction set computer (CISC), which employs a rich, complex, and powerful set of instructions. This argument has little import to the programmer, however, since any reasonable instruction set can simulate any other. Historically, the commercial success of one or another sort of computer seems to have had almost nothing to do with the complexity of the instruction set or any other detail of internal design. In fact, some of the most successful computers — such as the microprocessors used in most personal computers — are generally regarded by computer designers as having poorly designed instruction sets. The details of machine design are of little importance to the users of the machines.

One reason the complexity of the instruction set doesn't much matter has to do with the subroutines. Subroutines allow sequences of instructions to be used over and over from many places within the program. In effect, the subroutine-calling convention allows the programmer to define new instructions by using sequences of other instructions. The program accesses a subroutine by using a Jump instruction to load the program counter with the address of the subroutine; but before doing so, the computer saves the previous contents of the program counter in a special memory location. At the end of the subroutine, another instruction reads this return address and jumps back to the location from which the subroutine was called.

This process of subroutine calling can work recursively, in the sense that subroutine sequences may have jumps to other subroutines within them, and so on. A subroutine can even call itself, in a recursively defined function. In order to keep track of this nesting of subroutines, the computer needs a systematic way of storing the return addresses, so that it will know where to return when each subroutine is completed. It cannot just store all the return addresses in the same special location, because when subroutines are nested, it needs to remember more than one return address. Normally, the computer stores return addresses in a group of sequential locations known as a stack. The most recent return address is stored at the「top of the stack.」The memory stack works just like a stack of dinner plates: items are always added or removed from the top — a last-in, first-out storage system that works perfectly for storing the return addresses of nested subroutines, because a subroutine is never finished until all of its nested subroutines are finished.

Some subroutines are so useful that they are always loaded into the computer. This set of subroutines is called the operating system. Useful operating-system subroutines include those that write or read characters typed on the keyboard, or that draw lines on the screen, or otherwise interact with the user. The computer's operating system determines most of the look and feel of the interface to the user. It also governs the interface between the computer and whatever program is being run, since the operating system's subroutines provide the program with a set of operations that are richer and more complex than the machine-language instructions.

In fact, as long as the same pattern of bits produces the same effect, the programmer doesn't care whether a function is implemented by the computer hardware or by the operating-system software. The same program operating on two different types of computers might in one case perform an arithmetical operation in the hardware and in the other perform it by means of an operating-system subroutine. Similarly, the operating system of one type of computer may allow it to emulate the entire instruction set of another type of computer. Computer manufacturers sometime use such emulation to make the newer model of their computers act like the earlier models, so that older software can run without modification.

The operating system normally includes all the subroutines that perform input/output — that is, operations allowing a program to interact with the outside world. This interaction is effected by connecting certain locations in the computer's memory to input devices such as a keyboard or a mouse and output devices such as a video display terminal. For example, the space bar on the keyboard might be wired to memory register 23, so that the data read from address 23 is 1 if the space bar is pressed and 0 if it is not. Another memory register might control the color displayed on a certain dot on the screen. If every dot on the screen displays data stored in a different memory location, the computer can draw any pattern on the screen just by writing the appropriate pattern into memory.

With the exception of its input/output mechanisms, the computer we've just described is simply a finite-state machine connected to a memory. Both these elements can be constructed entirely from registers and Boolean logic blocks, using the techniques described in chapters 1 and 2. The finite-state machine that controls the computer is complicated, but it is no different in principle from the finite-state machine that controls a traffic light. Designing the machine is simply a matter of going through the details of memory data, address, and state sequences for each instruction to be executed, and then converting this state table into Boolean logic. Recall that since both the finite-state machine and the memory are made of registers and blocks of logic, both can be implemented by a number of technologies: electronics, hydraulics, sliding sticks.

建立连接关系

如何使用有限状态机来执行用 Logo 等语言编写的指令呢？布尔逻辑能为这个问题提供答案。我们可以通过三个主要步骤在有限状态机和 Logo 程序之间建立连接。第一，给有限状态机加入一个名为内存的存储装置，它可以扩展有限状态机，这样，有限状态机就可以通知它存储要求完成的操作指令；第二，这个扩展后的有限状态机会执行用机器语言编写的指令，机器语言可以直接指定机器的动作；第三，机器语言将指导计算机解释编程语言（如 Logo）。本章的其余内容将会详细讲述上述过程是如何进行的，而且其详细程度将会远远超出理解本书其他内容之所需。因此，读者无须强迫自己理解所有的步骤，重要的是理解功能抽象的层次结构是如何构建起来的，本章最后一段总结了这一点。

实际上，计算机只是一种带有内存的特殊有限状态机（见图 3-6）。计算机的内存由寄存器构成，前者是用于存储数据的一列数组，就如同保存有限状态机状态的寄存器。每个寄存器保存一组二进制位，称为计算机字，有限状态机可以直接读取（或者写入）。一个计算机字包含的二进制位数因计算机而异，现代微处理器的二进制位数一般为 8 位、16 位或者 32 位。随着技术的进步，计算机的字长很可能会增加。常规的内存中包含的寄存器数目可达数百万甚至数十亿个，其中每个寄存器只存储一个计算机字。计算机每次只能访问内存中的一个寄存器，也就是说，有限状态机在每个周期中只能读取或者写入一个寄存器中的数据。内存中的每个寄存器都有一个不同的地址，即一组二进制位，用于存取寄存器，因此寄存器也被称为存储单元。内存中还包含布尔逻辑块，它们可以解码寄存器并选择数据读取或者写入的位置。如果在一个寄存器中写入数据，布尔逻辑块就会将新数据存储到该位置对应的寄存器中；如果要从寄存器中读取数据，这些布尔逻辑块就会将数据从该寄存器转移至内存的输出，该输出与有限状态机的输入相连。

图 3-6　与内存相连接的有限状态机

存储在内存中的某些计算机字都是将要被处理的数据，比如数字和字母，有些则是有限状态机将要执行的指令序列。这些指令以机器语言的形式存储，如上所述，它们比常规的编程语言简单得多。有限状态机可以直接翻译并执行机器语言。在这里所描述的计算机中，机器语言记录的每个指令都存储在内存的单独一个计算机字中，指令序列则存储在由按顺序编号的存储单元组成的块中，这些机器语言指令序列是计算机中最简单的一种软件。

有限状态机会反复执行这种运算序列：首先，从内存中读取一条指令；然后，执行这条指令规定的运算；最后，计算下一条指令的地址。有限状态机的布尔逻辑块中内置了执行该运算的状态序列。每个指令本身是一组具有特殊模式的二进制组，它们能驱动有限状态机对内存中的数据执行各种操作。比如，加法指令就是一类特殊的二进制组，它可以对内存中某两个寄存器的数据执行加法运算。在识别出加法指令后，有限状态机将会进行一系列状态转换，并完成这些运算：从内存地址中读取加数，然后对两个加数求和，最后将结果写回内存。

大多数计算机中的指令分为两种基本类型：处理指令和控制指令。处理指令可以从内存中读取和写入数据，并会组合数据以完成算术和逻辑运算。存储单元或者寄存器通常由处理指令来设定。通常而言，处理指令能够直接访问的寄存器只有少数几个，其余寄存器都是通过间接的方式被访问的，因为它们的地址存储在其他寄存器中。例如，一个 Move（传送）指令会将寄存器 1 中的数据移动至寄存器 2 所指定的地址。如果寄存器 2 存储的一组二进制位代表的数字为 1234，那么该数据就会被移动至寄存器 1234 中去。其他的处理指令也会将不同寄存器之间的数据组合起来。还有一些处理指令可以对寄存器中的二进制位组执行布尔运算，比如逻辑块「与」「或」「非」等。

控制指令确定了将取出的下一条指令的地址。该地址存储在被称为程序计数器的特殊寄存器中。在通常情况下，指令是按顺序从连续的存储单元中取出的。因此，每取出一个指令，程序计数器中的地址就会加 1。控制指令允许将其他数字加载至程序计数器中，进而改变将要执行的指令序列。最简单的控制指令是 Jump（转移）指令，它将特定的地址存入程序计数器中，然后从这个新地址中获取下一条指令。Jump 指令的变体为条件 Jump 指令，即只有当某个条件得到满足时，比如两个寄存器中的数据相等，才会将另一个地址写入程序计数器中。如果条件不满足，那么条件 Jump 指令就不会生效，下一条指令仍按原顺序获取。

如果需要反复执行相同的指令序列，则可以在指令序列结束时加入一个条件 Jump 指令，使程序计数器返回开始处，这样便可周而复始，执行任意多次。这种运算方式被称为循环，我们已经在介绍 Logo 编程语言时举过一例了。如果需要将指令序列重复执行 10 次，则可以用一个寄存器记录循环迭代的次数。

不同型号的计算机可以识别的指令有所不同。多年来，计算机设计者一直在争论，什么样的指令集最好。其争论的焦点在于以下两种指令集哪种的优点更明显。一种是精简指令集计算机（RISC），其指令集的功能比较简单，数目最少；另一种是复杂指令集计算机（CISC），其指令集的数目较多，功能强大且复杂。不过，关于这两种指令集的争论并不会影响到程序员的设计，因为任意一种合理的指令集都可以模拟出任何其他的指令集。从过往的经验来看，某种类型的计算机在商业上的成功似乎与其指令集的复杂度或内部设计细节没有关系。实际上，在计算机设计者看来，一些最成功的指令集设计得并不好，比如大多数个人计算机所用的微芯片。计算机的设计细节对计算机用户来说并不重要。

指令集的复杂度无关紧要的一个原因与子程序有关。子程序允许指令序列可以在程序的许多位置被反复使用。实际上，程序员可以通过调用子程序来使用其他指令序列定义新指令。程序通过 Jump 指令来调用子程序，这个 Jump 指令能够将子程序的地址写入程序计数器中；在此之前，计算机会预先将程序计数器中的原先内容保存至一个专门的内存地址中。当子程序结束后，另有一条指令会读取该返回地址，并转回至原程序调用时的位置。

调用子程序的这一过程可以递归执行，也就是说，子程序序列可包含转向自身中子程序的 Jump 指令，以此类推。在以递归方式定义的函数中，子程序甚至可以调用自己。为了跟踪子程序的嵌套调用过程，计算机需要一种保存返回地址的系统化方法，以便子程序在结束时知道返回的位置。然而，将所有返回地址保存在同一特殊位置并不可行，因为嵌套调用子程序时需要记录的返回地址不止一个。通常，计算机会将返回地址存储在一组被称为堆栈的连续地址中。最新的返回地址则存储在「栈顶」。内存堆栈的工作原理类似于一叠盘子，其添加和移除工作都在顶部进行。这是一种后进先出的存储系统，它完美地适配了嵌套子程序返回地址的存储过程，因为一个子程序在其所有嵌套子程序全部执行完毕之前是不会结束的。

有些子程序的作用不可或缺，因此一直装在计算机中。这类子程序的集合被称为操作系统。操作系统子程序的功能包含读取键盘上键入的字符、在屏幕上显示线条，以及与用户交互等。计算机的操作系统决定了用户界面的大部分外观和体验，它也是负责管理计算机与运行程序之间的接口，因为操作系统的子程序能给程序提供比机器语言指令更丰富、更复杂的操作集合。

实际上，只要相同的一组二进制位产生相同的效果，程序并不在乎功能实现的途径是计算机硬件还是操作系统（软件）。当同一个程序运行在两台不同类型的计算机上时，一台计算机可能通过硬件来完成运算，而另一台则通过操作系统来完成运算。同样，同一型号的计算机的操作系统可以模拟出另一种型号的计算机的所有指令集。计算机制造商有时会用这种模拟方法使新旧型号的计算机保持一致，这样就无须修改旧版软件，即可直接运行。

操作系统通常包括执行输入和输出功能的所有子程序，也就是说，程序通过这些功能与外界进行交互。通过将计算机内存中的某些地址与诸如键盘、鼠标等输入装置，以及诸如视频显示终端等输出装置相互连接起来，我们便可以实现这种交互功能。例如，如果键盘上的空格键与寄存器 23 相连，那么当按下空格键时，从寄存器 23 中读取到的数字是 1，反之则为 0。某个寄存器可能控制着屏幕上某一像素点的显示色。如果屏幕上每个点显示的颜色数据存储在不同的内存地址中，那么计算机只需向内存中写入合适的图像数据，即可在屏幕上显示与之对应的图案。

除了输入和输出机制之外，我们上面所讲的计算机只是一个简单的、与内存相连的有限状态机，完全可以借助第 1 章和第 2 章中提到的技术，用寄存器和布尔逻辑块组装而成。虽然控制计算机的有限状态机非常复杂，但从原理上来说，它与控制交通信号灯的有限状态机并无区别。计算机的设计就是去规划每一条指令涉及的内存数据、地址和状态序列等详细信息，然后用布尔逻辑实现这个状态表。有限状态机和内存都是由寄存器和逻辑块组成的，因此这两者都可以通过电子技术、液压技术和滑动杆等多种方法来实现。

### 3.3 Translation The Language

So we have established a chain of connections between the technology and the instructions. But how do the instructions execute a program written in a language — Logo, for instance —  when that language is written in words and the instructions are patterns of bits? The answer is that the necessary translation is performed by the computer itself.

The translation process performed by the computer is similar to the process that a patient, meticulous human translator would use to translate a document written in an unfamiliar language, given a dictionary written in the language itself. The human translator can look up the meaning of any unknown word in the dictionary, and if words in the dictionary definition are also unknown, these words can be looked up as well. This process continues until the translator reaches a definition couched in words whose meanings are known. In this analogy, the translator's (that is, the computer's) dictionary is the program, and the words known to the computer are the aforementioned primitives of the program language. These primitives are defined directly, as simple sequences of machine instructions. For instance, when the computer looks up the definition of the Logo language primitive FORWARD, it finds the sequence of machine instructions that will draw the appropriate line on the screen.

To understand how a computer translates Logo primitives into machine language, it is helpful to understand the conventions that a computer uses to represent the Logo programs within its memory. One way to store a Logo program in a computer's memory is as a sequence of characters in adjacent memory locations, with each character being stored at a single location. In its memory, the computer keeps a directory of the addresses of the instruction sequences corresponding to each command name. This directory is stored in memory as a list of names paired with their addresses. The computer is able to find the location of an object with a given name by searching the directory for the name and finding the corresponding address. When the computer is asked to execute a particular command, it looks up the name in the directory to find out where its definition is stored.

Some of this process of looking things up and finding the corresponding sequences of machine language can be done before the program is executed. This saves time, because if the program is going to be executed more than once, there's no point in looking up the same things over and over again. When most of the work of conversion is done beforehand, the translation process is called compilation , and the program that performs the compilation is called a compiler. If most of the work is done while the program is being executed, then the process is called interpretation, and the program is called an interpreter. There is no hard and fast line between the two.

翻译语言

到目前为止，我们已经在技术和指令之间建立了一系列连接。程序由词汇写成，指令由二进制位组构成。那么，在这种情况下，机器指令如何执行用编程语言（例如 Logo）编写的程序呢？答案在于计算机执行翻译的过程。

计算机执行翻译的过程和人类语言的翻译过程类似。假设有一名耐心细致的翻译员正在翻译一份用陌生的语言编写的文档，并且所使用的字典也是用这种陌生的语言编写的。当他碰到未知单词时，可以查询字典，如果在词语的定义中又碰到了未知单词，可以继续查询字典。这个过程可以持续地进行下去，直到这名翻译员能读懂定义中所有词语的含义。在这个例子中，翻译员的字典相当于计算机程序，计算机能读懂的词语则相当于前面我们提到的编程语言的原语。这些原语被直接定义为简单的机器指令序列。例如，当计算机查询 Logo 语言中「FORWARD」原语的定义时，就会找到可以在屏幕上画直线的机器指令序列。

若想了解计算机如何将 Logo 语言中的原语翻译成机器语言，你最好先了解一下计算机在内存中表示 Logo 程序的方法。在计算机内存中存储 Logo 程序的一种方法是，将程序字符存入一段连续的内存地址中，且每个内存地址中只存储一个字符。计算机内存中保存有一份对应于指令名称的指令序列的地址表。这份地址表存储于内存中，而且在地址表中，指令名称和指令序列是一一对应的。对于给定名称的指令，计算机可在表中查询该名，找到它的地址，进而找到具有此名的对象的存储单元。当计算机执行某个特定命令时，就会在地址表中查找这个命令的名称，并会找到其定义的存储地址。

在程序执行之前，计算机就可以完成查找程序对应的机器指令序列的过程。这一操作很节省时间，因为一个程序不只执行一次，同样的查询没有必要重复多次。如果大部分翻译工作在程序执行前便已完成，那么这类翻译就被称为编译，完成上述编译过程的程序被称为编译器。如果大部分翻译工作是边执行程序边进行的，那么这类翻译被称为解释，相应的程序被称为解释器。这两者之间并无一条明确的界线。

### 3.4 Welcome to The Hierarchy

We are now in a position to summarize how a computer works, from top to bottom. Most readers will have lost track of the details, but remember that it is not important to remember how every step works! The important thing to remember is the hierarchy of functional abstractions.

The work performed by the computer is specified by a program , which is written in a programming language. This language is converted to sequences of machine-language instructions by interpreters or compilers , via a predefined set of subroutines called the operating system. The instructions, which are stored in the memory of the computer, define the operations to be performed on data, which are also stored in the computer's memory. A finite-state machine fetches and executes these instructions. The instructions as well as the data are represented by patterns of bits. Both the finite-state machine and the memory are built of storage registers and Boolean logic blocks , and the latter are based on simple logical functions , such as And, Or , and Invert. These logical functions are implemented by switches , which are set up either in series or in parallel , and these switches control a physical substance, such as water or electricity, which is used to send one of two possible signals from one switch to another: 1 or 0. This is the hierarchy of abstraction that makes computers work.

层次结构

现在，我们可以对计算机的工作原理做一个完整的总结了。虽然大多数读者总是很容易忘却具体的细节，但对于计算机的工作原理来说，记住每个细节并无必要，重要的是记住功能抽象的层次结构。

程序规定了计算机执行的任务，前者是由编程语言编写的。通过一组被称为操作系统的预先定义好的子程序，解释器或者编译器会将编程语言转换为机器语言指令序列。这些指令序列存储于计算机的内存中，并且可以操作存储于内存中的数据。有限状态机可以读取并执行这些指令。这些指令和数据都以二进制位的形式存在。有限状态机和内存都由寄存器和布尔逻辑块构成，布尔逻辑块基于「与」「或」「非」这些简单的逻辑功能构建而成，而这些逻辑功能可以通过开关来实现。开关以串联或者并联的方式相连，控制着某种物理介质，比如水、电等，而这些物理介质在开关之间传递着两种可能的信号之一，即 1 或 0。这就是计算机得以运行的功能抽象的层次结构。