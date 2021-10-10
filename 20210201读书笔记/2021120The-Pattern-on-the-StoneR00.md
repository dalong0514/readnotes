## 记忆时间

## 卡片

书籍的中文名是《丹尼尔·希利斯讲计算机》，出版时间是 2021 年 1 月，个人觉得书名翻译的很不好，应该为《刻字石头上的魔法》，哈哈。（2021-10-10）

### 0101. 主题卡 —— 计算机本质基于的三大原则

印象：

1、第一原则。分层的思想，之前在书籍「计算机系统概论」以及万维钢精英日课里书籍「柏拉图与技术呆子」里都有涉及，从晶体管一步步往上抽象到应用软件，具体详见那边的信息。

2、第二原则。通用计算机思想，冯·诺依曼提出来的，具体可以看吴军的专栏「谷歌方法论」以及冯·诺依曼的 Paper。

3、第三原则。生物计算机思维，跟第一原则想法，计算机的实现从分层结构转为网络结构（复杂系统），从自上而下的设计转变为自下而上的涌现，也是目前作者研究的方向。

信息源自「Preface: Magic in the Stone」

This is the book I wish I had read when I first started learning about the field of computing. Unlike most books on computers — which are either about how to use them or about the technology out of which they're built (ROM, RAM, disk drives, and so on) — this is a book about ideas. It explains, or at least introduces, most of the important ideas in the field of computer science, including Boolean logic, finite-state machines, programming languages, compilers and interpreters, Turing universality, information theory, algorithms and algorithmic complexity, heuristics, uncomutable functions, parallel computing, quantum computing, neural networks, machine learning, and self-organizing systems. Anyone interested enough in computers to be reading this book will probably have encountered many of these ideas before, but outside of a formal education in computer science there are few opportunities to see how they all fit together. This book makes the connections — all the way from simple physical processes like the closing of a switch to the learning and adaptation exhibited by self-organizing parallel computers.

A few general themes underlie an exposition of the nature of computers: the first is the principle of functional abstraction , which leads to the aforementioned hierarchy of causes and effects. The structure of the computer is an example of the application of this principle — over and over again, at many levels. Computers are understandable because you can focus on what is happening at one level of the hierarchy without worrying about the details of what goes on at the lower levels. Functional abstraction is what decouples the ideas from the technology.

The second unifying theme is the principle of the universal computer  — the idea that there is really only one kind of computer, or, more precisely, that all kinds of computers are alike in what they can and cannot do. As near as we can tell, any computing device, whether it's built of transistors, sticks and strings, or neurons, can be simulated by a universal computer. This is a remarkable hypothesis: as I will explain, it suggests that making a computer think like a brain is just a matter of programming it correctly.

The third theme in this book, which won't be fully addressed until the last chapter, is in some sense the antithesis of the first. There may be an entirely new way of designing and programming computers — a way not based on the standard methods of engineering. This would be exciting, because the way we normally design systems begins to break down when the systems become too complicated. The very principles that enable us to design computers lead ultimately to a certain fragility and inefficiency. This weakness has nothing to do with any fundamental limitations of information-processing machines — it's a limitation of the hierarchical method of design. But what if instead we were to use a design process analogous to biological evolution — that is, a process in which the behaviors of the system emerge from the accumulation of many simple interactions, without any「top-down」control? A computing device designed by such an evolutionary process might exhibit some of the robustness and flexibility of a biological organism — at least, that's the hope. This approach is not yet well understood, and it may turn out to be impractical. It is the topic of my current research.

2『计算机本质基于的三大原则，做一张主题卡片。（2021-06-07）』

In an explanation of the nature of computers, there are some fundamentals that have to be dealt with before we can move on to the good stuff. The first two chapters introduce the fundamentals: Boolean logic, bits, and finite-state machines. The payoff is that by the end of chapter 3 you'll understand how computers work, top to bottom. This sets the stage for the exciting ideas about universal computing machines, which begin in chapter 4.

The philosopher Gregory Bateson once defined information as「the difference that makes a difference.」Another way of saying this is that information is in the distinctions we choose to make significant. In a primitive electrical calculator, say, information is indicated by light bulbs that go on or off depending on whether a current is flowing or not. The voltage of the signal doesn't matter, nor does the direction of current flow. All that matters is that a wire carries one of two possible signals, one of which causes a bulb to light. The distinction that we choose to make significant — the difference that makes a difference, in Bateson's phrase — is between current flowing and not flowing. Bateson's definition is a good one, but the phrase has always meant something more to me. In my lifetime of four decades, the world has been transformed. Most of the changes we've seen in business, politics, science, and philosophy in that time have been caused by, or enabled by, developments in information technology. A lot of things are different in the world today, but the difference that has made the difference has been computers.

These days, computers are popularly thought of as multimedia devices, capable of incorporating and combining all previous forms of media — text, graphics, moving pictures, sound. I think this point of view leads to an underestimation of the computer's potential. It is certainly true that a computer can incorporate and manipulate all other media, but the true power of the computer is that it is capable of manipulating not just the expression of ideas but also the ideas themselves. The amazing thing to me is not that a computer can hold the contents of all the books in a library but that it can notice relationships between the concepts described in the books — not that it can display a picture of a bird in flight or a galaxy spinning but that it can imagine and predict the consequences of the physical laws that create these wonders. The computer is not just an advanced calculator or camera or paintbrush; rather, it is a device that accelerates and extends our processes of thought. It is an imagination machine, which starts with the ideas we put into it and takes them farther than we ever could have taken them on our own.

### 0201. 术语卡 —— 有限状态机

信息源自「0201Univeral Building Blocks」

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

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 ——

### 0601. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## 再版前言 —— 计算机背后不曾改变的基本原理

本书初版问世很久之后，我的出版商惊讶地发现：它在当下仍然很受欢迎。这也是我有机会为本书写再版前言的原因。本书已被翻译为十几种语言，至今仍有众多读者。自本书问世以来，计算机技术及应用发生了天翻地覆的变化。不过本书并不着眼于计算机的具体技术及应用，而是关注计算机背后不曾改变的基本原理，这也是本书能持续热卖的关键所在。

我必须承认，令我感到诧异的不是在数字革命之初就已存在的那些关于计算机科学的原理如今依然很重要，而是迄今为止，几乎没有新的原理补充进来。10 多年过去了，虽然计算机技术及应用以及编程技术都取得了巨大进步，对社会产生的影响也远远超出了预言家的预期，但计算机背后的工作原理，即本书所阐述的关于计算机的概念，仍没有改变。我本来想利用再版的机会增添一些新内容，但令我感到吃惊的是，并无新的基本原理可供补充。

在目前的版本中，我选择性地删除了一些无须再费笔墨解释的概念。不过，这并非意味着这些内容是错误的。例如，在一个每天都享受云并行计算服务的读者看来，并行计算方面的内容并无新意。真正令人费解的是，为何 20 世纪有如此多的专家都坚信，并行计算机永远不会被投入使用。此外，如今的你们可能会对本书中有关人工智能的观点有所抵触，因为目前你们与智能机器相处得十分融洽。事实上，20 世纪时许多人对智能计算机的概念感到惶恐不安，比如，当计算机第一次击败人类国际象棋冠军时，许多人感到很沮丧。然而，过了不到 20 年，当计算机在一项流行的益智电视节目中再次击败人类冠军时，更多人开始为计算机鼓劲加油。从那时起，人们普遍将计算机视为助手而非威胁。

除了修订拼写错误之外，我尽可能地保持了本书初版的原汁原味，不去刻意提高文字的感性程度，实际上，感性是一种不断变化的浮动目标。与其紧跟必将过时的当下潮流，还不如让作品定格在某一时刻更为有趣。同时，本书写成于计算机科学发展历程中的一个特殊时期，虽然那时计算机已经显示出了足以改变我们生活的潜力，但这一切很大程度上还未实现。那时的计算机非常简单，以至于我对自己设计的计算机的每个晶体管和所编写的每行代码都了如指掌。不过，正如本书最后一章预期的那样，我们现在到达了一个临界点，即计算机系统的复杂度已经超出了任何人所能完全理解和掌握的程度。

关于未来的发展，本书提出了两个可能的方向。第一个是量子计算，正如书中所述，它具有巨大的潜力，但目前并无可行的实现方式。当我写下这句话时，现实情况仍是如此。从理论和技术方面来说，量子计算取得了巨大突破，但它们中的任何一个的计算速度都比不上传统计算机。正如本书初版所述，量子计算仍是「一个值得关注的领域」。本书预测的第二个可能方向是，计算机能像生物进化过程那样实现自我设计。目前，这个方向已经显现出了隐约的曙光，不过在很大程度上，它只是一个未实现的可能方案。目前，我们还缺乏相关理论来说明这个过程如何才能成为现实。我对未来发现这些新原理持乐观态度，期待能够在本书的后续版本中继续讨论。

## Preface: Magic in the Stone

I etch a pattern of geometric shapes onto a stone. To the uninitiated, the shapes look mysterious and complex, but I know that when arranged correctly they will give the stone a special power, enabling it to respond to incantations in a language no human being has ever spoken. I will ask the stone questions in this language, and it will answer by showing me a vision: a world created by my spell, a world imagined within the pattern on the stone.

A few hundred years ago in my native New England, an accurate description of my occupation would have gotten me burned at the stake. Yet my work involves no witchcraft; I design and program computers. The stone is a wafer of silicon, and the incantations are software. The patterns etched on the chip and the programs that instruct the computer may look complicated and mysterious, but they are generated according to a few basic principles that are easily explained.

Computers are the most complex objects we human beings have ever created, but in a fundamental sense they are remarkably simple. Working with teams of only a few dozen people, I have designed and built computers containing billions of active parts. The wiring diagram of one of these machines, if it were ever to be drawn, would fill all the books in a good-sized public library, and nobody would have the patience to scan the whole of it. Fortunately, such a diagram is unnecessary, because of the regularity of a computer's design. Computers are built up in a hierarchy of parts, with each part repeated many times over. All you need to understand a computer is an understanding of this hierarchy.

Another principle that makes computers easy to understand is the nature of the interactions among the parts. These interactions are simple and well-defined. They are also usually one-directional, so that the actions of the computer can be sorted neatly into causes and effects, making the inner workings of a computer more comprehensible than, say, the inner workings of an automobile engine or a radio. A computer has a lot more parts than a car or a radio does, but it's much simpler in the way the parts work together. A computer is not dependent so much on technology as on ideas.

Moreover, the ideas have almost nothing to do with the electronics out of which computers are built. Present-day computers are built of transistors and wires, but they could just as well be built, according to the same principles, from valves and water pipes, or from sticks and strings. The principles are the essence of what makes a computer compute. One of the most remarkable things about computers is that their essential nature transcends technology. That nature is what this book is about.

This is the book I wish I had read when I first started learning about the field of computing. Unlike most books on computers — which are either about how to use them or about the technology out of which they're built (ROM, RAM, disk drives, and so on) — this is a book about ideas. It explains, or at least introduces, most of the important ideas in the field of computer science, including Boolean logic, finite-state machines, programming languages, compilers and interpreters, Turing universality, information theory, algorithms and algorithmic complexity, heuristics, uncomutable functions, parallel computing, quantum computing, neural networks, machine learning, and self-organizing systems. Anyone interested enough in computers to be reading this book will probably have encountered many of these ideas before, but outside of a formal education in computer science there are few opportunities to see how they all fit together. This book makes the connections — all the way from simple physical processes like the closing of a switch to the learning and adaptation exhibited by self-organizing parallel computers.

A few general themes underlie an exposition of the nature of computers: the first is the principle of functional abstraction , which leads to the aforementioned hierarchy of causes and effects. The structure of the computer is an example of the application of this principle — over and over again, at many levels. Computers are understandable because you can focus on what is happening at one level of the hierarchy without worrying about the details of what goes on at the lower levels. Functional abstraction is what decouples the ideas from the technology.

The second unifying theme is the principle of the universal computer  — the idea that there is really only one kind of computer, or, more precisely, that all kinds of computers are alike in what they can and cannot do. As near as we can tell, any computing device, whether it's built of transistors, sticks and strings, or neurons, can be simulated by a universal computer. This is a remarkable hypothesis: as I will explain, it suggests that making a computer think like a brain is just a matter of programming it correctly.

The third theme in this book, which won't be fully addressed until the last chapter, is in some sense the antithesis of the first. There may be an entirely new way of designing and programming computers — a way not based on the standard methods of engineering. This would be exciting, because the way we normally design systems begins to break down when the systems become too complicated. The very principles that enable us to design computers lead ultimately to a certain fragility and inefficiency. This weakness has nothing to do with any fundamental limitations of information-processing machines — it's a limitation of the hierarchical method of design. But what if instead we were to use a design process analogous to biological evolution — that is, a process in which the behaviors of the system emerge from the accumulation of many simple interactions, without any「top-down」control? A computing device designed by such an evolutionary process might exhibit some of the robustness and flexibility of a biological organism — at least, that's the hope. This approach is not yet well understood, and it may turn out to be impractical. It is the topic of my current research.

2『计算机本质基于的三大原则，做一张主题卡片。（2021-06-07）』

In an explanation of the nature of computers, there are some fundamentals that have to be dealt with before we can move on to the good stuff. The first two chapters introduce the fundamentals: Boolean logic, bits, and finite-state machines. The payoff is that by the end of chapter 3 you'll understand how computers work, top to bottom. This sets the stage for the exciting ideas about universal computing machines, which begin in chapter 4.

The philosopher Gregory Bateson once defined information as「the difference that makes a difference.」Another way of saying this is that information is in the distinctions we choose to make significant. In a primitive electrical calculator, say, information is indicated by light bulbs that go on or off depending on whether a current is flowing or not. The voltage of the signal doesn't matter, nor does the direction of current flow. All that matters is that a wire carries one of two possible signals, one of which causes a bulb to light. The distinction that we choose to make significant — the difference that makes a difference, in Bateson's phrase — is between current flowing and not flowing. Bateson's definition is a good one, but the phrase has always meant something more to me. In my lifetime of four decades, the world has been transformed. Most of the changes we've seen in business, politics, science, and philosophy in that time have been caused by, or enabled by, developments in information technology. A lot of things are different in the world today, but the difference that has made the difference has been computers.

These days, computers are popularly thought of as multimedia devices, capable of incorporating and combining all previous forms of media — text, graphics, moving pictures, sound. I think this point of view leads to an underestimation of the computer's potential. It is certainly true that a computer can incorporate and manipulate all other media, but the true power of the computer is that it is capable of manipulating not just the expression of ideas but also the ideas themselves. The amazing thing to me is not that a computer can hold the contents of all the books in a library but that it can notice relationships between the concepts described in the books — not that it can display a picture of a bird in flight or a galaxy spinning but that it can imagine and predict the consequences of the physical laws that create these wonders. The computer is not just an advanced calculator or camera or paintbrush; rather, it is a device that accelerates and extends our processes of thought. It is an imagination machine, which starts with the ideas we put into it and takes them farther than we ever could have taken them on our own.

前言 —— 石头中的魔术

在一块石头上，我蚀刻了一系列几何图案，在外行看来，这些图案显得神秘而又复杂，但我清楚地知道，只要布局正确，这些图案就会赋予这块石头一种特殊的能力，即对人类从未说过的一种咒语做出回应。如果我用这种语言提问，石头便会应答：这是一个我用符咒创造的世界，一个在石头图案中想象的世界。

如果我在几百年前的老家新英格兰说出自己从事的职业，可能会被当作巫师送上火刑柱。实际上，我的工作和巫术没有任何关系，我从事的是计算机设计和编程，而上文提到的石头是硅晶片，符咒是软件程序。虽然蚀刻在芯片上的几何图案和指示计算机工作的程序看起来复杂且神秘，但根据一些基本的生成原理，我们很容易将其解释清楚。

虽然计算机是人类有史以来最复杂的人造物，但从基本原理上来说，它们又十分简单，仅有数十人的团队就能设计并制造出包含数十亿个零部件的各类计算机。如果将其中一台计算机的线路图在纸上画出来，那么所用的纸张便能塞满一座大型公共图书馆，没有人会有耐心将其浏览一遍。幸运的是，计算机的设计具有规律性，没有必要将线路图看一遍。计算机是由不同层次的部件构建起来的，而每一层次的部件都会被重复多次。只要理解了这些层次结构，你就能读懂计算机。

还有一个使计算机易于理解的原理，那就是其各部件之间交互作用的本质。这些交互作用很简单，而且定义明确，通常具有单向性，可以准确地排列成一系列因果关系，这使计算机内部的运行原理比汽车发动机或者收音机的运行原理更容易理解。虽然相比于汽车和收音机，计算机拥有更多零部件，但这些部件协同工作的方式非常简单。计算机更多依据的是概念，而非技术。

这些概念与组成计算机的电子元件没有任何关系。现代计算机由晶体管和电路组成，不过，根据同样的原理，计算机也可以由阀门和管道，或者棍棒和绳索搭建起来。这些原理是计算机能够进行计算的根本所在。计算机最引人称道的一点是，其本质远胜于技术，而本书就旨在介绍计算机的本质。

我多么希望在刚开始学习计算机这门学科时就能读到这样一本书。大多数计算机类书籍不是介绍计算机的使用方法，便是介绍具体的创造技术，比如只读存储器（ROM）、随机存储器（RAM）、磁盘驱动器等。这本书讨论的重点是「概念」，而且会介绍计算机科学领域的大多数重要概念，包括布尔逻辑、有限状态机、编程语言、编译程序和解释程序、图灵准则、信息论、算法及其复杂度、启发式方法、不可计算的函数、并行计算、量子计算、神经网络、机器学习和自组织系统等。对计算机感兴趣的读者可能已经听说过其中的许多概念，但对于非计算机专业出身的人来说，很难明白这些概念是如何结合在一起的。本书将会介绍这些关联 —— 从类似开关的闭合等简单的物理过程开始，一直深入到自组织并行计算机所呈现出来的学习和自适应能力。

计算机的本质基于几条基本原则。第一条原则是功能抽象原理（functional abstraction），它奠定了前文提到的因果关系层次结构。计算机的结构就是这一原理的应用范例，即许多层次结构能够被不断重复。计算机之所以易于理解，是因为你可以专注于某一层次结构发生的情况，而不必担心较低层次结构上发生的细节。功能抽象原理是使概念与技术脱离的关键。

第二条原则是通用计算机原理（universal computer），即所有的计算机都属于同一种类型，更确切地说，所有类型的计算机在能做和不能做哪些事上是相似的。我们也可以这样说，一台通用计算机能够模拟所有类型的计算机，无论其组成材料是晶体管、棍棒、绳索，还是神经元。这是一个非常重要的假设，它表明，制造一台能像大脑一样思考的计算机只是一个进行正确编程的问题，我将在后面详细解释这一点。

从某种意义上来说，第三条原则是第一条原则的对立面，我将在最后一章展开详述。也许存在一种全新的计算机设计和编程方式，它并不基于标准的工程设计方式。这一设想令人感到无比兴奋，因为当系统过于复杂时，常规的系统设计方式将不再有效。实际上，第一条原则会导致系统带有一定程度的脆弱性和低效性。这个缺点与信息处理器的基础性缺陷没有关系，而是层次设计方式的一个缺陷。那么，如果我们采用一种与生物进化相似的设计过程，情况会如何呢？在这个设计过程中，系统行为源自很多简单交互作用的累积，而非「自上而下」的控制。通过这种进化过程设计出来的计算机可能具有生物体的某些健壮性和适应性。至少，这是一种希望。我们还未完全参透这一设计方式，它也可能会被证明行不通。这是目前我研究的一个课题。

为了全面了解计算机的本质，我们需要先掌握一些基本知识，再研究深层次的内容。本书前两章将介绍以下基本内容：布尔逻辑、二进制和有限状态机。在读完第 3 章时，你便能自上而下地理解计算机的工作原理。这也为理解第 4 章的内容奠定了基础，第 4 章将介绍有关通用计算机的有趣概念。

哲学家格雷戈里·贝特森（Gregory Bateson）曾将信息定义为「非同小可的差异」。换句话说，信息存在于我们选择用来表示意义的差异之中。例如，在原始的电子计算器中，信息是以电流流通与否造成的灯的开启和关闭来表示的，而信号的电压和电流方向则无关紧要。这其中起关键作用的是一根能够传输两种可能的信号的线路，其中一种信号是让灯亮起。在这里，产生关键作用的差异之处，也就是贝特森所说的「非同小可的差异」，就是电流的流通与否。贝特森给出的定义很明确，这个定义于我而言有着更为丰富的含义。在短短几十年间，世界发生了翻天覆地的变化。信息技术的发展引发或者促成了我们在商业、政治、科学和哲学领域所目睹的许多变革。当今世界，许多事情已异于往昔，而这一非同小可的变化皆源自计算机。

人们普遍认为，计算机是一种能够融合文本、图像、动画、声音等所有已有形式的多媒体设备。然而我认为，这一观点低估了计算机的潜力。计算机当然能够综合处理各种形式的媒体，但其真正的威力是它不仅能处理概念的表示形式，而且能处理概念本身。计算机最令我震惊的地方不在于它能够储存图书馆中所有书籍的内容，而在于它能够识别并总结出书中所述的各种概念之间的关系；不在于它能展示出飞鸟或者星系自旋的图像，而在于它能猜想并预测出创造了这些奇迹的物理定律将会产生的结果。计算机不只是一台先进的计算器，或一架高级的照相机，或一支具有神奇功能的画笔，它更是一种能够加速和扩展思维过程的工具。计算机是一架富有想象力的机器，它从我们输入的概念演变为人类从未抵达的情境。