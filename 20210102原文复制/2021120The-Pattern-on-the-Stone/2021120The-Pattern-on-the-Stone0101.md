# 0101. Nuts And Bolts

W hen I was a child, I read a story about a boy who built a robot out of parts he found lying around a junkyard. The boy's robot could move, talk, and think, just like a person, and it became his friend. For some reason, I found the idea of building a robot very appealing, so I decided to build one myself. I remember collecting body parts — tubes for the arms and legs, motors for the muscles, lightbulbs for the eyes, and a big paint can for the head — in the full and optimistic expectation that after they were assembled and the contraption was plugged in, I would end up with a working mechanical man.

After nearly electrocuting myself a few times, I began to get my parts to move, light up, and make noises. I felt I was making progress. I began to understand how to construct movable joints for the arms and legs. But something even more important was beginning to dawn on me: I didn't have the slightest idea how to control the motors and the lights, and I realized that something was missing in my knowledge of how robots worked. I now have a name for what was missing: it's called computation. Back then, I called it「thinking,」and I saw that I didn't have a clue about how to get something to think. It seems obvious to me now that computation is the hardest part of building a mechanical man, but as a child this came as a surprise.

基础知识

小时候，我读过这样一个故事，一个男孩用从垃圾场收集的零件组装出了一个机器人，这个机器人可以像人一样走路、说话和思考，并成为男孩的朋友。不知何故，我被制造机器人的想法深深地吸引了，因此决定也动手组装一个。我对当时收集各部位零件的情景还记忆犹新：用管子作四肢，马达作肌肉，灯泡作眼睛，油漆桶作脑袋。我满怀希望地期待当自己完成组装、插上电源之后，就能拥有一个正常运作的机器人。

在经历了几次严重的触电事故后，我的机器人终于可以移动和发光了，而且还会发出「嗡嗡」的声音。我感觉自己有所长进，而且我还懂得了如何为四肢制造活动关节。不过，当时我面临的最大问题是，该如何控制那些马达和灯泡。后来，我意识到自己是对机器人的工作原理缺乏了解，而现在，我知道当时缺乏的知识是什么了 —— 计算，当时我称之为「思维」，我毫不知晓如何才能让某个物体具备思维能力。现在，我清楚地知道，计算才是制造机器人最难的部分，而当时还是小孩的我很难意识到这一点。

## 1.1 Boolean Logic

Fortunately, the first book I ever read on the subject of computation was a classic. My father was an epidemiologist, and we were living in Calcutta at the time. Books in English were hard to come by, but in the library of the British consulate I found a dusty copy of a book written by the nineteenth-century logician George Boole. The title of the book was what attracted me: An Investigation of the Laws of Thought. This grabbed my imagination. Could there really be laws that governed thought? In the book, Boole tried to reduce the logic of human thought to mathematical operations. Although he did not really explain human thinking, Boole demonstrated the surprising power and generality of a few simple types of logical operations. He invented a language for describing and manipulating logical statements and determining whether or not they are true. The language is now called Boolean algebra.

Boolean algebra is similar to the algebra you learned in high school, except that the variables in the equations represent logic statements instead of numbers. Boole's variables stand for propositions that are either true or false, and the symbols , , and  represent the logical operations And, Or, and Not. For example, the following is a Boolean algebraic equation

This particular equation, called De Morgan's theorem (after Boole's colleague Augustus De Morgan), says that if neither A nor B is true, then both A and B must be false. The variables A and B can represent any logical (that is, true or false) statement. This particular equation is obviously correct, but Boolean algebra also allows much more complex logical statements to be written down and proved or disproved.

Boole's work found its way into computer science through the master's thesis of a young engineering student at the Massachusetts Institute of Technology named Claude Shannon. Shannon is best known for having invented a branch of mathematics called information theory , which defines the measure of information we call a bit. Inventing the bit was an impressive accomplishment, but what Shannon did with Boolean logic was at least as important to the science of computation. With these two pieces of work, Shannon laid the foundation for the developments that were to occur in the field of computing for the next fifty years.

Shannon was interested in building a machine that could play chess — and more generally in building mechanisms that imitated thought. In 1940, he published his master's thesis, which was titled「A Symbolic Analysis of Relay Switching Circuits.」In it, he showed that it was possible to build electrical circuits equivalent to expressions in Boolean algebra. In Shannon's circuits, switches that were open or closed corresponded to logical variables of Boolean algebra that were true or false. Shannon demonstrated a way of converting any expression in Boolean algebra into an arrangement of switches. The circuit would establish a connection if the statement was true and break the connection if it was false. The implication of this construction is that any function capable of being described as a precise logical statement can be implemented by an analogous system of switches.

Rather than presenting the detailed formalisms developed by Boole and Shannon, I will give an example of their application in the design of a very simple kind of computing device, a machine that plays the game of tic-tac-toe. This machine is much simpler than a general-purpose computer, but it demonstrates two principles that are important in any type of computer. It shows how a task can be reduced to logical functions and how such functions can be implemented as a circuit of connected switches. I actually built a tic-tac-toe machine out of lights and switches shortly after I read Boole's book in Calcutta, and this was my introduction to computer logic. Later, when I was an undergraduate at MIT, Claude Shannon became a friend and teacher, and I discovered that he, too, had used lights and switches to build a machine that could play tic-tac-toe.

As most readers know, the game is played on a 3 × 3 square grid. Players take turns marking the squares, one player using an X , the other an O. The first player to place three symbols in a row (horizontally, vertically, or diagonally) wins the game. Young children enjoy tic-tac-toe because it seems to offer limitless possible strategies for winning. Eventually they realize that only a small number of patterns can occur, and the game consequently loses its charm: once both players learn the patterns, each game invariably ends in a tie. Tic-tac-toe is a good example of a computation precisely because it wavers on this line between the complex and the simple. Crossing that line is what computation is all about. Computation is about performing tasks that seem to be complex (like winning a game of tic-tac-toe) by breaking them down into simple operations (like closing a switch).

In tic-tac-toe, the situations that occur are few enough so that it's practical to write them all down, and therefore to build the correct response in every case into the machine. We can use a simple two-step process for designing the machine: first , reduce the play to a series of cases defining the correct response to each pattern of moves; second , convert those cases into electrical circuits by wiring the switches to recognize the pattern and indicate the appropriate response.

One way to proceed would be to write down every conceivable arrangment of X's and O's which could be placed on the grid and then decide how the computer would play in each instance. Since each of the nine squares has three possible states ( X , O, and blank), there are 3 9 (or 19,683) ways to fill the grid. But most of these patterns would never occur in the course of a game. A better method of listing the possibilities is to draw up a game tree  — a configuration that traces every possible line of play. The game tree starts with a blank grid at the root and has a branch for every possible alternative line of play, determined by the move of the human player. (The tree does not need to branch when the machine plays, because the response of the machine to any given move is always predetermined.) Figure 1 shows a small part of such a tree. For every possible move made by X , the human player, there is a predetermined O response to be made by the machine. (For some strange reason, computer scientists always draw trees upside-down, with the「root」at the top.)

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

幸运的是，我读的第一本有关计算机的书是一本经典之作。我的父亲是一位流行病学家，那时我们居住在加尔各答，很难读到英文著作。在英国领事馆的图书室里，我找到了一本表面布满灰尘的书，作者是 19 世纪的逻辑学家乔治·布尔（George Boole），书名为《思维规律的研究》（An Investigation of the Laws of Thought

）。这个书名立刻吸引了我，令我心驰神往，难道真的存在支配思维的法则吗？在这本书中，布尔试图将人类的思维逻辑简化为数学运算。他虽然没有真正解释清楚人类的思维过程，但道出了简单的逻辑运算的惊人力量和普适性。他还发明了一种语言，可以用来描述和处理逻辑陈述，以及判定这些陈述的真假。这种语言现在被称为布尔代数（Boolean algebra）。

布尔代数与我们在高中所学的代数相似，差别仅在于等式中的变量所代表的东西从数字变成了逻辑命题。布尔变量代表非真即假的命题，符号∧、∨、¬ 分别代表「与」「或」「非」逻辑运算。例如下列的布尔代数方程：

¬（A∨B）=（¬ A）∧（¬ B）

这个方程被称为德·摩根定律，是以布尔的同事奥古斯都·德·摩根（Augustus De Morgan）的名字命名的，其含义为：如果 A 和 B 无一为真，则两者皆必然为假。变量 A 和 B 可以表示任意非真即假的逻辑命题。显然，这个方程是成立的。不过，布尔代数还能写出更加复杂的逻辑命题，并能进行证明和反证。

麻省理工学院曾有一位年轻的工程学硕士，他通过一篇论文将布尔的理论引入了计算机科学领域，使其大放异彩，这位学生名叫克劳德·香农（Claude Shannon）。香农最广为人知的成就是创立了信息论，信息论是数学的一个分支，这门分支定义了我们称为「二进制位」（又叫比特）的信息度量单位。二进制位概念的提出是一项了不起的成就。对于计算科学来说，香农利用布尔逻辑所做的工作也同样重要。香农的这两项成就为之后 50 年计算机科学的发展奠定了基础。

香农曾致力于创造一台会下国际象棋的机器，更确切地说是一台能模拟人类思维的机器。1940 年，他在硕士论文《继电器与开关电路的符号分析》（A Symbolic Analysis of Relay Switching Circuits）中表明，构建一个与布尔代数方程完全等价的电路是可能的。在香农设计的电路中，开关的开启和关闭对应着布尔代数逻辑变量值的真与假。香农提出了一种方法，可以将布尔代数方程转化为开关组合。当命题为真时，电路建立连接，当命题为假时，电路则断开连接。这种方法意味着，任何能由布尔逻辑命题精确描述的功能都可用类似的开关系统来实现。

与其详述布尔和香农建立的理论框架，我们不如举例来说明其理论在实际中的应用，以我设计的一台井字游戏机为例。虽然相比于通用的计算机，这个游戏机非常简单，但它体现了对所有计算机来说都非常重要的两大原理：如何将一项任务转化为一系列逻辑函数，以及如何用由开关连接起来的电路实现这些函数。当我读完布尔的书之后，就用灯泡和开关搭建了一个井字游戏机，这是我对计算机逻辑的初次涉猎。后来，我去了麻省理工学院读本科，香农成了我的良师益友。我惊奇地发现，他也曾用灯泡和开关搭建过井字游戏机。

大多数读者都知道，井字游戏在一个 3×3 的方格棋盘中进行。游戏双方轮流在方格中标注符号，如果一位玩家使用符号「X」，另一位则使用符号「O」，而率先使三个符号连成一行（水平、垂直或者对角）的玩家即可获胜。小孩子之所以喜欢玩井字游戏，是因为这个游戏似乎有无数种获胜的方法。不过，他们最终都会意识到，能赢得棋局的模式只有为数不多的几种，此时这个游戏对他们来说就会变得索然无味。一旦玩家双方都掌握了游戏套路，每场游戏都将以平局结束。井字游戏很好地说明了计算的本质，其难度介于复杂和简单之间。计算就是跨过复杂和简单之间的分界线，去完成复杂的任务，实现方法就是通过将看似复杂的任务（如赢得井字游戏）分解为简单的操作（如关闭开关）。

在井字游戏中，可能会出现的棋局模式并不多，完全可以将它们都列举出来，再将每种棋局的正确走法输入游戏机中。我们可以通过两个简单的步骤来设计这个游戏机：首先，将游戏转化为所有可能的棋局，每种棋局都根据具体的模式制定出正确的走法；然后，将每种走法转化为由开关连接的电路，使其能识别出棋局模式，并做出正确的反应。

还有一种方法是，列举出由符号「X」和「O」在方格棋盘中组成的所有可能的棋局模式，再确定计算机在每种情况下的走法。在 3×3 的方格棋盘中，每一格都有 3 种可能的状态（X、O 和空白），因此共有 39（或 19 683）种不同的棋局。不过，在玩游戏的过程中，大多数棋局是永远不会出现的。利用博弈树（game tree）的方法，我们可以更好地列举出各种可能性，这种方法足以描绘出所有可能发生的棋局路线图。博弈树从一个空白的根节点开始，下面的每条分支代表一种可能的游戏进程，游戏进程由人类玩家的下棋步骤决定。当轮到机器下棋时，博弈树并不会分叉，因为机器的走法都是预先设定好的。图 1-1 展示了博弈树的一部分。无论人类玩家在哪个方格中标出「X」，机器都会按事先设定好的走法标上「O」。说来也怪，计算机科学家经常将博弈树倒置，即将根节点画在顶部。

这棵博弈树反映了我在井字游戏中经常采用的一种策略 —— 尽可能占据方格棋盘上的中心格。人类玩家的下棋步骤决定了机器的下棋步骤，这大大减少了需要考虑的可能情况。一棵显示机器在各种情况下走法的完整博弈树大约有 500～600 个分支，确切的分支数量取决于所采取的下棋策略。如果机器按照博弈树指定的策略下棋，那么它每盘游戏都可以获胜，或者至少下成平局。由于游戏规则已经被编入了机器的走法之中，因此只要机器按照博弈树的步骤下棋，就不会违反游戏规则。依据博弈树，我们可以写出机器在所有棋局下的标准走法，这些标准走法便构成了机器的布尔逻辑。

一旦我们定义了想实现的机器行为，就可以将这种行为转化为由电池、电线、开关和灯泡组成的电路。机器的基本电路与手电筒的电路原理并无不同：当按下开关，即闭合电路时，灯泡会亮起，因为此时灯泡和电池之间形成了一条完整的通路（电池的两极分别用符号「+」和「-」来表示）。更为重要的是，这些开关可以通过串联或者并联的方式相连。例如，我们可以将两个开关串联在一起，在这种情况下，只有当两个开关都闭合时，灯泡才会亮起。通过这种电路，我便可实现计算机的一种基本的开关功能 ——「与」功能，之所以这样称呼它，是因为只有当第一个开关「与」和第二个开关「与」同时闭合时，灯泡才会亮起；同理可得，如果开关采用并联的方式，则可以实现「或」功能，即当其中一个「或」两个开关闭合时，电路就会连通，灯泡会亮起来（见图 1-2）。

将简单的串联电路和并联电路组合起来，便可以实现各种具有不同逻辑规则的连接。在井字游戏机中，一个串联的开关可用于识别一种棋局模式，而不同的串联开关可以通过并联的方式与灯泡相连，所以当几组串联开关通过并联的方式连接后，这些串联开关所代表的棋局模式就会点亮同一盏灯泡，也就是说，机器在这些情况下会采用相同的走法。

我设计的井字游戏机有 4 组开关，每组分别有 9 个开关，每个开关对应九方格棋盘上的一格。同时，游戏机中的 9 个灯泡按照井字棋盘那样排列。游戏设定由机器先走，且每走一步就点亮与之对应的灯泡。人类玩家每走一步就合上一个开关，走第一步棋使用第一个开关组，走第二步棋使用第二个开关组，依此类推。在我设计的这款游戏机中，机器总是先从棋盘左上角开始走第一步棋，这种开局方式可以大大减少所需考虑的可能情况。人类玩家接着可以合上第一组开关中的某个开关，比如合上对应棋盘中心格的开关，作为第一步棋，这样游戏就能持续进行下去了。这些开关和灯泡组成的电路构成了机器的游戏策略。

使机器对第一步棋做出反应的线路十分简单（见图 1-3）。将第一组开关中的每个开关都连接至对应的灯泡，灯泡代表的就是机器需要走的那一步棋。例如，如果人类玩家第一步棋走在棋盘中心格，机器就会走右下格，那么中心格的开关就要连接至右下角的灯泡。由于我设计的机器一有可能便以走中心格作为首选，因此第一组开关中的大多数开关都会与棋盘中心格的灯泡并联。

机器第二轮的走法取决于人类玩家走的第一步和第二步。为了识别出人类玩家的多轮下棋步骤，相应的开关采取串联的方式。例如，如果人类玩家的第一步棋走中心格，第二步棋走右上格，那么机器就会走左下格。这种棋局模式可以通过这种方法实现：将第一组开关中代表中心格的开关与第二组开关中代表右上格的开关串联（这表示「如果中心格和右上格都由人类玩家标上了符号，那么应该……」），再将这两个开关的开关链与代表左下格的灯泡相连。每组与灯泡相连且互为并行关系的开关链分别表示能使灯亮起来的不同下棋步骤，即「如果人类玩家的走法属于这些步骤中的任何一种，机器都会采取同样的应对方式」。如果两条不同的电路需要使用同一个开关，我便会安装一个「双闸开关」，即以机械的方式连接至同一按钮的两个开关，使它们能实现同步切换，这样便可以将同一步棋纳入两个不同的棋局模式之中。第三组和第四组开关的连接方式遵循同样的原则，但它们形成的下棋步骤更多。你可能会想到，虽然原理很简单，但线路会变得越来越复杂，棋盘中可供选择的方格会越来越少，但开关链条会越变越长。

我设计的井字游戏机大约有 150 个开关，它们由木头和钉子制成，对于当时的我来说这是一组很庞大的数字。然而现在，我设计的计算机芯片中的开关数目高达数百万个，大多数开关的连接模式与井字游戏机中的模式非常相似。虽然大多数现代计算机都采用了一种不同类型的电子开关 —— 晶体管，但基本的设计理念是一样的：用串联开关实现逻辑「与」的功能，用并联开关实现逻辑「或」的功能。

虽然从逻辑上来说，井字游戏机与通用计算机具有相似性，但两者也存在一些重要区别。第一个区别是，井字游戏机对按时间顺序发生的事件毫无概念。因此，我们必须事先设定好游戏中所有事件的发生顺序，即先设定好整个博弈树。对于井字棋而言，设计博弈树的工作已经很复杂了，更不用说更为复杂的游戏了，比如国际象棋、跳棋等，这种方法几乎是行不通的。现代计算机非常善于玩跳棋，也善于玩国际象棋（见第 5 章），这是因为它们放弃了预先设定博弈树的方法，而是采取了一种按时间顺序依次识别棋局模式的方法。

井字游戏机与通用计算机的第二个重要区别是，前者只能执行单一的任务，其「程序」完全内置于线路中。换句话说，井字游戏机中没有任何软件。

## 1.2 Bits and Logic Blocks

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

图 1-5　用以实现「非」功能的机械式取反器

「与」「或」「非」功能被统称为逻辑块，将它们组合起来就能实现其他逻辑功能。例如，将「或」逻辑块的输出和「非」逻辑块的输入相连，便可以实现「或非」功能，即当两个输入都不为 1 时，「或非」的输出才为 1。再举一个例子（应用德·摩根定律），将两个「非」逻辑块的输出分别连接至一个「或」逻辑块的输入，再将此逻辑块的输出连接至第三个「非」逻辑块的输入（见图 1-6），那么这 4 个逻辑块就共同实现了逻辑「与」的功能，即当两个输入都为 1 时，最后的输出才是 1。

三个「非」逻辑块的输入（见图 1-6），那么这 4 个逻辑块就共同实现了逻辑「与」的功能，即当两个输入都为 1 时，最后的输出才是 1。

图 1-6　一个「或」逻辑块和若干「非」逻辑块组成一个「与」逻辑块

早期的计算器是由机械部件制造成的。17 世纪，法国数学家布莱士·帕斯卡（Blaise Pascal）制造出了一台机械加法器，这让德国自然科学家戈特弗里德·威廉·莱布尼茨（Gottfried Wilhelm Leibniz）和英国博学家罗伯特·胡克（Robert Hooke）深受启发，他们改良了这台加法器，使其可以运算乘法和除法，甚至可以求取平方根。不过，这些机器都是不可编程的。到了 1833 年，英国数学家、发明家查尔斯·巴贝奇（Charles Babbage）设计并参与制造了一台可编程的机械式计算机。实际上，在我的童年时期，即 20 世纪 60 年代，大多数算术计算器都是机械式的。我非常喜欢这些机械式计算机，因为里面的运作过程能被清楚地看到，这一点是电子计算机无法实现的。当我设计电子计算机芯片时，会将电路想象成移动的机械部件。

## 1.3 The Fluid Computer

The picture I have in my mind when I design a logic circuit is of hydraulic valves. A hydraulic valve is like a switch that controls and is controlled by the flow of water. Each valve has three connections: the input, the output, and the control. Pressure on the control connection pushes on a piston that turns off the water flow from input to output. Figure 7 shows a circuit for the Or function, built out of hydraulic valves.

In this circuit, water pressure is used to distinguish between the two possible signals. Notice that in a hydraulic valve the control pipe can affect the output pipe but the output pipe cannot affect the control pipe. This restriction establishes a forward flow of information through the switch; in a sense, it establishes a direction in time. Also, since the valve is either open or closed, it serves an additional function of amplification , which allows the strength of the signal to be restored to its maximum value at every stage. Even if the input is a little low on pressure — because it goes through a long, thin pipe, say, or because of a leak — the output will always be at full pressure thanks to the on/off operation of the valve. This is the fundamental difference between digital and analog: A digital valve is either on or off; an analog valve, like your kitchen faucet, can be anything in between. In the hydraulic computer, all that is required of the input signal is that it be strong enough to move the valve. In this case, the difference that makes a difference is the difference in water pressure sufficient to switch the valve on. And since a weakened signal entering an input will still produce a full-strength output, we can connect thousands of layers of logic, the output of one layer controlling the next, without worrying about a gradual decrease in pressure. The output of each gate will always be at full pressure.

FIGURE 7 An Or block built with hydraulic valves

This type of design is called restoring logic , and the example in hydraulic technology is particularly interesting, because it corresponds almost exactly to the logic used in modern electronic computers. The water pressure in the pipes is analogous to the voltage on the wires, and the hydraulic valve is analogous to the metal-oxide transistor. The control, input, and output connections on the valve correspond closely to the three connections (called gate, source , and drain ) on a transistor. The analogy between water valves and transistors is so exact that you could translate the design for a modern microprocessor directly into a design for a hydraulic computer. To do so, you would need to look at the pattern of wires on the silicon chip under a microscope and then bend a set of pipes into the same shapes as the wires on the chip and connect them in exactly the same pattern. In place of each transistor, you would use a hydraulic valve. The pipe that corresponds to the power-supply voltage on your chip would be connected to a pressurized water supply, and the pipe that corresponds to the ground connection could empty down a drain.

To use the hydraulic computer, you would have to connect hydraulic equivalents of its inputs and outputs — you would need to build a hydraulic keyboard, a hydraulic display, hydraulic memory chips, and so on — but if you did all this, it would go through exactly the same switching events as the electronic chip. Of course, the hydraulic computer would be much slower than your latest microprocessor (to say nothing of larger), because water pressure travels down pipes much more slowly than electricity travels down wires. As to the size: Since the modern microchip has several million transistors, its hydraulic equivalent would require several million valves. A transistor in a chip is about a millionth of a meter across; a hydraulic valve is about 10 centimeters on a side. If the pipes scale proportionally, then the hydraulic computer would cover about a square kilometer with pipes and valves. From an airplane, it would look roughly the same as the electronic chip does under a microscope.

When I design a computer chip, I draw lines on a computer screen, and the pattern is reduced (in a process analogous to photographic reduction) and etched onto a chip of silicon. The lines on the screen are my pipes and valves. Actually, most computer designers don't even bother drawing lines; instead, they specify the connections between Ands and Ors and let a computer work out the details of placement and geometry of the switches. Most of time, they forget about the technology and concentrate on the function. I do this, too, sometimes, but I still prefer to draw my own shapes. Whenever I design a chip, the first thing I want to do is look at it under a microscope — not because I think I can learn something new by looking at it but because I am always fascinated by how a pattern can create reality.

液压计算机

设计逻辑电路时，我脑海中会浮现出液压阀的影子。液压阀类似于一个既能控制水流也能被水流控制的开关。液压阀具有三个连接点：输入、输出和控制端。控制端连接处的液压推动活塞向前，从而阻断从输入端到输出端的水流。图 1-7 表示的是一个由液压阀构建成的「或」逻辑块。

图 1-7　用液压阀构建成的「或」逻辑块

在这个管路中，液压用于区分两种不同类型的信号。值得注意的是，液压阀中的控制管会影响输出管，但反之则不然。这个限制条件确立了信息可通过开关向前流动。从某种意义上来说，它实现了一种时间维度上的单向性。而且，由于液压阀只能处于打开或关闭的状态，它还具有放大的功能，即使信号的强度在每个阶段都能保持在最大值。得益于液压阀的开／关功能，即使输入的液压很小（这可能是因为液体经过了一根细长的管道或者管道存在泄漏），输出的液压依然能达到最大值。这就是数字开关和模拟开关的根本区别：数字开关要么开启，要么关闭，而模拟开关就像厨房的水龙头一样有各种调节值，可以位于两者间的任意位置。在液压计算机中，输入信号的压力必须足够强，这样才能打开液压阀。在这种情况下，「非同小可的差异」就是液压足以或者不足以将阀门打开的水压差。由于输入的微弱信号仍然能产生足够强度的输出，因此，我们可以将数以千计的逻辑管道连接起来，并用一个逻辑管道的输出控制下一个逻辑管道，而不必担心管道液压会逐渐降低，因为每个阀门输出的液压仍将保持在最大值。

这类设计被称为复原逻辑（restoring logic）。关于液压技术的例子尤为有趣，因为它与现代计算机采用的逻辑几乎完全相同。管道中的液压类似于电路中的电压，液压阀类似于金属氧化物制成的晶体管。液压阀中的控制、输入和输出分别对应晶体管中的栅极、源极、漏极。液压阀与晶体管的工作原理非常相似，我们完全可以将现代微处理器的设计直接转化为液压计算机的设计。为了完成这种转化，你需要通过显微镜观察硅基芯片上的线路布局，然后按照线路摆放好管道，再按线路原样将其连接起来；同时，用液压阀替代芯片上的晶体管。芯片上的电路与供电电源相连，因此与之对应的管道应该连接至可以增压的水源处；芯片上有电路接地，而与之对应的管道应该能将积水排空。

若想使用这台液压计算机，你还需要将输入和输出的液压部件连接起来，这就需要建造一个液压式键盘、一个液压式显示器以及液压式存储芯片等，如果这一切都完成了，液压计算机便能完全复现电子芯片中所有开关的动作。当然，由于液压在管道中的传播速度比电路中电流的速度慢很多，因此液压计算机的运行速度要比你最新的微处理器慢得多，更不用说大型机算机了。从体积上来说，现代微芯片上容纳了数百万个晶体管，与之对应的液压计算机则需要数百万个阀门，芯片上晶体管的长度只有百万分之一米，而一个液压阀的边长就在 10 厘米左右。如果管道也按此比例布置，那么由液压阀和管道组成的液压计算机的占地将达到 1 平方千米。从飞机上来看，这台液压计算机与你在显微镜下看到的芯片的大小相当。

当我设计计算机芯片时，首先会利用计算机绘制出设计图，然后将这些图案缩小，再蚀刻在硅芯片上。屏幕上呈现的线路就相当于管道和液压阀。事实上，绝大多数计算机设计者都不必为画图劳心费神，他们只需指定逻辑块（「或」「与」等）之间的连接关系，后续诸如逻辑块的位置和开关的几何布线等细节性工作都可交由计算机来处理。在多数情况下，设计者都会专注于功能设计，而将画线工艺置之于脑后。我虽然有时也会这样做，但还是更喜欢亲手画设计图。每当我设计完一款芯片时，想做的第一件事就是利用显微镜来观察它。我这么做并非因为能从观察中获取新知识，而是着迷于感受芯片上的图案是如何缔造出现实的。

## 1.4 Tinker Toys

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

## 1.5 Free to Worry about the Difference that makes a Diffierence

Naming the two signals in computer logic 0 and 1 is an example of functional abstraction. It lets us manipulate information without worrying about the details of its underlying representation. Once we figure out how to accomplish a given function, we can put the mechanism inside a「black box,」or a「building block」and stop thinking about it. The function embodied by the building block can be used over and over, without reference to the details of what's inside. This process of functional abstraction is a fundamental in computer design — not the only way to design complicated systems but the most common way (later, I'll describe an alternate method). Computers are built up of a hierarchy of such functional abstractions, each one embodied in a building block. The blocks that perform functions are hooked together to implement more complex functions, and these collections of blocks in turn become the new building blocks for the next level.

This hierarchical structure of abstraction is our most powerful tool in understanding complex systems, because it lets us focus on a single aspect of a problem at a time. For instance, we can talk about Boolean functions like And and Or in the abstract, without worrying about whether they are built out of electrical switches or sticks and strings or water-operated valves. For most purposes, we can forget about technology. This is wonderful, because it means that almost everything we say about computers will be true even when transistors and silicon chips become obsolete.

不必担忧那些非同小可的差异

将计算机逻辑的两种信号命名为 0 和 1，这是功能抽象原理的一个范例。这样，我们在处理信息时就无须考虑信号所代表的底层事物的具体细节。一旦我们掌握了如何实现某个给定的功能，就可以将实现机制放入一个「黑箱」或「构件」中，然后不再考虑它。我们可以不断反复使用构件中封装好的功能，而无须理会其内部的细节。这种功能抽象的过程是计算机设计的一项基本原则，它虽然不是设计复杂系统的唯一方法，却是最通用的一种方法（我还将在后文介绍另一种方法）。计算机的功能抽象层次结构是这样建造的：每种功能抽象都由一种构件体现。将具备某些功能的逻辑块互连起来便能实现更为复杂的功能，而这些逻辑块组合又会成为下一个层次的新构件。

这种功能抽象的层次结构是我们理解复杂系统的最有力的工具，有了它，我们每次只需关注一个方面的问题。例如，当我们在讨论抽象的「与」和「或」等布尔功能时，不必考虑这些逻辑功能是由电子开关、木棍和绳索，还是液压阀构成的。在大多数情况下，我们无须探讨技术问题。这是一个绝妙的方法，因为这意味着，即使晶体管和硅芯片等技术有一天会被淘汰，但对于计算机来说，我们所论述的一切将依然基本正确。