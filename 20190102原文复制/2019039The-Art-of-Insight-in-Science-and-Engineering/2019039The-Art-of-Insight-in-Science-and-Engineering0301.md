## Part II Discarding complexity without losing information

You've divided your hard problems into manageable pieces. You've found transferable, reusable ideas. When these tools are not enough and problems are still too complex, you need to discard complexity — the theme of our next three tools. They help us discard complexity without losing information. If a system contains a symmetry (Chapter 3) — or what is closely related, it is subject to a conservation law — using the symmetry greatly simplifies the analysis. Alternatively, we often do not care about a part of an analysis, because it is the same for all the objects in the analysis. To ignore those parts, we use proportional reasoning (Chapter 4). Finally, we can ensure that our equations do not add apples to oranges. This simple idea — dimensional analysis (Chapter 5) — greatly shrinks the space of possible solutions and helps us master complexity.

第二篇 忽略复杂性且无信息丢失

你已经将你的难题分解成一些可以处理的部分。已经找到了可移植、可重复使用的概念。当这些工具还不够时，你需要认清并忽略复杂性 —— 这是我们接下来要讨论的 3 个工具的内容。这些工具将帮助我们在不丢失信息的情况下舍弃复杂性。如果一个体系具有对称性（第 3 章）—— 或与对称相关的性质，那么体系就会遵守某种守恒律 —— 利用对称性会大大简化分析。相应的，我们并不关心这个分析是针对哪一部分的，因为对所有部分的分析都是一样的。为了忽略那些相同的部分，只关注变化的部分，我们将使用正比分析（第 4 章）。最后，我们可以保证我们的方程不会把苹果和橘子加在一块儿。这个简单的概念 —— 量纲分析（第 5 章）—— 极大压缩了可能的解的空间，因而帮助我们把握住复杂性。

## 0301. Symmetry and conservation

3.1 Invariants

3.2 From invariant to symmetry operation

3.3 Physical symmetry

3.4 Box models and conservation

3.5 Drag using conservation of energy

3.6 Lift using conservation of momentum

3.7 Summary and further problems

The rain is pouring down and shelter is a few hundred yards away. Do you get less wet by running? On the one hand, running means less time for raindrops to hit you. On the other hand, running means that the raindrops come toward you more directly and therefore more rapidly. The resolution is not obvious — until you apply the new tool of this chapter: symmetry and conservation. (In Section 3.1.1, we'll resolve this run-in-the-rain question.) 

0301 对称性与守恒

大雨倾盆而下，避雨的地方在几百米之外。如果奔跑的话你会少淋湿些吗？一方面，你在雨中待的时间越少，那么被淋到的雨也越少。另一方面，跑的时候雨滴会更直接地打在身上。结论并不是那么明显 —— 直到你运用本章介绍的工具：对称性与守恒。（在章节 3.1.1，我们会讲解雨中跑问题。）

### 3.7 Summary and further problems

In the midst of change, find what does not change — the invariant or conserved quantity. Finding these quantities simplifies problems: We focus on the few quantities that do not change rather than on the many ways in which quantities do change. An instance of this idea with wide application is a box model, where what goes in must come out. By choosing suitable boxes, we could estimate rainfalls and drag forces, and understand lift.

Problem 3.37 Raindrop speed

Use the drag force 𝐹drag ∼ 𝜌𝐴cs𝑣2 to estimate the terminal speed of a typical raindrop with a diameter of 0.5 centimeters. How could you check the prediction?

Problem 3.38 Average value of sin squared

Use symmetry to find the average value of sin2𝑡 over the interval 𝑡 = [0, 𝜋].

Problem 3.39 Moment of inertia of a spherical shell

The moment of inertia of an object about an axis of rotation is axis

```
∑ 𝑚𝑖𝑑2𝑖,    (3.106)
```

summed over all mass points 𝑖, where 𝑑𝑖 is the distance of the r point from an axis of rotation. Use symmetry to find the moment of inertia of a spherical shell with mass 𝑚 and radius 𝑟 about an axis through its center. You shouldn't need to do any integrals!

Problem 3.40 Flying bicyclist

Estimate the wingspan a world-champion bicyclist would require in order to get enough lift for takeoff.

Problem 3.41 Maximum-gain frequency for a second-order system 

In this problem, you use symmetry to maximize LC the gain of an 𝐿𝑅𝐶 circuit or a spring–mass system with damping (using the analogy in Section 2.4.1). The gain 𝐺, which is the amplitude ratio Vout/Vin, depends on the signal's angular frequency 𝜔: 

where 𝑗 = −1, 𝜔0 is the natural frequency of the system, and 𝑄, the quality factor, is a dimensionless measure of the damping. Don't worry about where the gain formula comes from: You can derive it using the impedance method (Problem 2.22), but the purpose of this problem is to maximize its magnitude ∣𝐺(𝜔)∣. Do so by finding a symmetry operation on 𝜔 that leaves ∣𝐺(𝜔)∣ invariant.

Problem 3.42 Runway length

Estimate the runway length required by a 747 in order to take off.

Problem 3.43 Hovering versus flying

At what forward flight speed does the hummingbird of Section 3.6.1 require as much power to generate lift as it would to hover? How does this speed compare to its typical flight speed?

Problem 3.44 Resistive grid

In an infinite grid of 1-ohm resistors, what is the resistance measured across one resistor?

To measure resistance, an ohmmeter injects a current 𝐼 at one terminal (for simplicity, imagine that 𝐼 = 1 ampere). It removes the same current from the other terminal, and measures the resulting voltage difference 𝑉 between the terminals. The resistance is 𝑅 = 𝑉/𝐼.

Hint: Use symmetry. But it's still a hard problem!

Problem 3.45 Inertia tensor

Here is an inertia tensor (the generalization of moment of inertia) of a particular object, calculated in an ill-chosen (but Cartesian) coordinate system:

a. Change the coordinate system to a set of principal axes, where the inertia tensor has the diagonal form:

and give the principal moments of inertia 𝐼xx, 𝐼yy, and 𝐼zz. Hint: Which properties of a matrix are invariant when changing coordinate systems?

b. Give an example of an object with a similar inertia tensor. Rhetorical question: In which coordinate system is it easier to think of such an object?

This problem was inspired by a problem on the physics written qualifying exam during my days as a PhD student. The problem required diagonalizing an inertia tensor, and there was too little time to rederive or even apply the change-of-basis formulas. Time pressure sometimes pushes one toward better solutions!

Problem 3.46 Temperature distribution on an infinite sheet

On this infinite, uniform sheet, the 𝑥 axis is held at zero temperature, and the 𝑦 axis is held at unit temperature (𝑇 = 1). Find the temperature everywhere (except the origin!). Use Cartesian coordinates 𝑇(𝑥, 𝑦) or polar coordinates 𝑇(𝑟, 𝜃), whichever choice makes it easier to describe the temperature.

3.7 小结及进一步的问题

在变化的过程中，找出不变的量 —— 不变量或守恒量。找到这些不变量会简化问题，因为我们关注的是少数不变的量而不是很多以不同方式变化的量。这一想法具有广泛应用的例子就是黑箱模型，其中输入多少就必须输出多少。通过选择合适的黑箱，我们可以估算雨量、阻力和升力。

题 3.37 雨滴速度

利用阻力 F（阻力）～ ρAcsv^2，估算直径大约 0.5 厘米的典型雨滴的最终速度。如何验证你的结果？

题 3.38 正弦平方的平均值

利用对称性求 sin^(2)t 在间隔 t= [0, π] 的平均值。

题 3.39 球壳的转动惯量

物体绕轴转动的转动惯量为：

```
∑mid^(2)i 
```

对所有点 i 上的质量求和，其中 d，是点到转轴的距离。利用对称性求质量为 m，半径为 r 的球壳绕通过球心的转轴的转动惯量。你不需要做任何积分。

题 3.40 飞翔的自行车

估算一个自行车世界冠军为了得到足够的升力起飞所需的翼展是多少。

题 3.41 二阶系统的最大增益频率

在本题中，利用对称性求 LRC 电路或有阻尼的弹簧-质点系统（利用章节 2.4.1 的分析）的最大增益。增益 G 为振幅的比 Vout/Vin，取决于信号的角频率 w：

其中 j=√-1，w0 是系统的本征频率，Q 是品质因子，一个用来描写衰减的无量纲量。不用担心增益公式怎么来的：你可以利用阻抗法导出（题 2.21），但本题的目的是将增益的大小 |G(ω)| 最大化。通过找出使 G(ω) 不变的关于 ω 的对称操作来完成。

题 3.42 跑道长度

估算波音 747 飞机需要的跑道长度。

题 3.43 悬停与飞行

章节 3.6.1 中的蜂鸟需要多大的向前速度飞行以使其和悬停时的功率相同？这个速度与典型的飞行速度相比如何？

题 3.44 电阻网格的再分析

对于一个 1 欧姆电阻组成的无限网络，一个电阻两端测到的电阻是多大？为了测量这个阻值，欧姆表在一端注入电流 I（为简单起见，假定 I=1 安培）。从另一端引出电流，然后测量两端的电压差 V。电阻即 R=V/I。

提示：利用对称性，不过这是一个难题！

题 3.45 转动惯量张量

这是一个特殊物体的转动惯量张量（转动惯量的推广），是在一个没有选择好的坐标系内（但仍是笛卡尔坐标）计算的：

a）将坐标系变换到主轴，使得转动惯量张量是对角形式：

并给出主转动惯量 Ixx, Iyy 和 Izx。

提示：当进行坐标变换时，矩阵的什么性质是不变的？

b）给出具有类似转动惯量的具体物体的例子。或反过来问，在什么坐标系更容易考虑这样的物体？

这个问题来自我当年读研究生时博士资格考试的物理笔试中一个题目的启发。这个题目要求将转动惯量张量对角化，而当时已经没时间重新推导或应用基的变换公式。时间的压力有时候迫使我们寻找更好的解决方法！

题 3.46 无限大薄板的温度分布

对于均匀的无限大薄板，x 轴保持为零度，y 轴保持均匀的单位温度（T=1）。求出每一点（原点除外）T=0 的温度。使用笛卡尔坐标 T(x,y) 或极坐标 T(r,𝜃)，看哪种选择会使温度的描写更容易。

### 3.1 Invariants

We use symmetry and conservation whenever we find a quantity that, despite the surrounding complexity, does not change. This conserved quantity is called an invariant. Finding invariants simplifies many problems.

Our first invariant appeared unannounced in Section 1.2 when we estimated the carrying capacity of a lane of highway. The carrying capacity — the rate at which cars flow down the lane — depends on the separation between the cars and on their speed. We could have tried to estimate each quantity and then the carrying capacity. However, the separation between cars and the cars' speeds vary greatly, so these estimates are hard to make reliably.

Instead, we invoked the 2-second following rule. As long as drivers obey it, the separation between cars equals 2 seconds of driving. Therefore, one car flows by every 2 seconds — which is the lane's carrying capacity (in cars per time). By finding an invariant, we simplified a complex, changing process.

When there is change, look for what does not change! (This wisdom is from Arthur Engel's Problem-Solving Strategies [12].) 

#### 3.1.1 To run or walk in the rain?

We'll practice with this tool by deciding whether to run or walk in the rain.

It's pouring, your umbrella is sitting at home, and home lies a few hundred meters away.

To minimize how wet you become, should you run or walk?

Let's answer this question with three simplifications. First, assume that there is no wind, so the rain is falling vertically. Second, assume that the rain is steady. Third, assume that you are a thin sheet: You have zero thickness along the direction toward your house (this approximation was more valid in my youth). Equivalently, your head is protected by a waterproof cap, so you do not care whether raindrops hit your head. You try to minimize just the amount of water hitting your front.

Your only degree of freedom — the only parameter that you get to choose — is your speed. A high speed leaves you in the rain for less time. However, it also makes the rain come at you more directly (more horizontally). But what remains constant, independent of your speed, is the volume of air that you sweep out. Because the rain is steady, that volume contains a fixed number of raindrops, independent of your speed. Only these raindrops hit your front. Therefore, you get equally wet, no matter your speed.

This surprising conclusion is another application of the principle that when there is change, look for what does not change. Here, we could change our speed by choosing to walk or run. Yet no matter what our speed, we sweep out the same volume of air — our invariant.

Because the conclusion of this invariance analysis, that it makes no difference whether you walk or run, is surprising, you might still harbor a nag-ging doubt. Surely running in the rain, which we do almost as a reflex, provide some advantage over a leisurely stroll.

Is it irrational to run to avoid getting wet?

If you are infinitely thin, and are just a rectangle moving in the rain, then the preceding analysis applies: Whether you run or walk, your front will absorb the same number of raindrops. But most of us have a thickness, and the number of drops landing on our head depends on our speed. If your head is exposed and you care how many drops land on your head, then you should run. But if your head is covered, feel free to save your energy and enjoy the stroll. Running won't keep you any dryer.

#### 3.1.2 Tiling a mouse-eaten chessboard

Often a good way to practice a new tool is on a mathematical problem. Then we do not add the complexity of the physical world to the problem of learning a new tool. Here, therefore, is a mathematical problem: a solitaire game.

A mouse comes and eats two diagonally opposite corners out of a standard, 8 × 8 chessboard. We have a box of rectangular, 2 × 1 dominoes.

Can these dominoes tile the mouse-eaten chessboard? In other words, can we lay down the dominoes to cover every square exactly once (with no empty squares and no overlapping dominoes)?

Placing a domino on the board is one move in this solitaire game. For each move, you choose where to place the domino — so you have many choices at each move. The number of possible move sequences grows rapidly. Instead of examining all these sequences, we'll look for an invariant: a quantity unchanged by any move of the game.

Because each domino covers one white square and one black square, the following quantity 𝐼 is invariant (remains fixed): 

```
𝐼 = uncovered black squares − uncovered white squares. (3.1)
```

On a regular chess board, with 32 white squares and 32 black squares, the initial position has 𝐼 = 0. The nibbled board has two fewer black squares, so 𝐼 starts at 30 − 32 = −2. In the winning position, all squares are covered, so 𝐼 = 0. Because 𝐼 is invariant, we cannot win: The dominoes cannot tile the nibbled board.

Each move in this game changes the chessboard. By finding what does not change, an invariant, we simplified the analysis.

Invariants are powerful partly because they are abstractions. The details of the empty squares — their exact locations — lie below the abstraction barrier.

Above the barrier, we see only the excess of black over white squares. The abstraction contains all the information we need in order to know that we can never tile the chessboard.

Problem 3.1 Cube solitaire

A cube has numbers at each vertex; all vertices start at 0 except for the lower left corner, which starts at 1. The moves are all of the same form: Pick any edge and increment its two vertices by one. The goal of this solitaire game is to make all vertices multiples of 3.

For example, picking the bottom edge of the front face and then the bottom edge of the back face, makes the following sequence of cube configurations:

Although no configuration above wins the game, can you win with a different move sequence? If you can win, give a winning sequence. If you cannot win, prove that you cannot.

Hint: Create analogous but simpler versions of this game.

Problem 3.2 Triplet solitaire

Here is another solitaire game. Start with the triplet (3, 4, 5). At each move, choose any two of the three numbers. Call the choices 𝑎 and 𝑏. Then make the following replacements:

```
𝑎 ⟶ 0.8𝑎 − 0.6𝑏; (3.3)
𝑏 ⟶ 0.6𝑎 + 0.8𝑏.
```

Can you reach (4, 4, 4)? If you can, give a move sequence; otherwise, prove that it is impossible.

Problem 3.3 Triplet-solitaire moves as rotations in space 

At each step in triplet solitaire (Problem 3.2), there are three possible moves, depending on which pair of numbers from among 𝑎, 𝑏, and 𝑐 you choose to replace.

Describe each of the three moves as a rotation in space. That is, for each move, give the rotation axis and the angle of rotation.

Problem 3.4 Conical pendulum

Finding the period of a pendulum, even at small amplitudes, requires calculus because of the pendulum's varying speed.

When there is change, look for what does not change. Accordingly, Christiaan Huygens (1629–1695), called「the most inge-nious watchmaker of all time」[20, p. 79] by the great physicist Arnold Sommerfeld, analyzed the motion of a pendulum moving in a horizontal circle (a conical pendulum). Project-ing its two-dimensional motion onto a vertical screen produces one-dimensional pendulum motion; thus, the period of the two-dimensional motion is the same as the period of one-dimensional pendulum motion! Use that idea to find the period of a pendulum (without calculus!).

#### 3.1.3 Logarithmic scales

In the solitaire game in Section 3.1.2, a move covered two chessboard squares with a domino. In the game of understanding the world, a frequent move is changing the system of units. As in solitaire, ask,「When such a move is made, what is invariant?」As an example to crystallize our thinking, here are frequencies related to human hearing. Let's graph them using kilohertz (kHz) as the unit. The frequencies then arrange themselves as follows:

low end of hearing 20 Hz

piano middle C 262 Hz

highest piano C 4186 Hz

high end of hearing 20 kHz

Now let's change units from kilohertz to hertz (Hz) — and keep the 0, 10, and 20 labels at their current positions on the page. This change magnifies every spacing by a factor of 1000: The new 20 hertz is where 20 kilohertz was (about 4 inches or 10 centimeters to the right of the origin), and 20 kilohertz, the high end of human hearing, sits 100 meters to our right — far beyond the borders of the page. This new scale is not very useful.

However, we missed the chance to use an invariant: the ratio between frequencies. For example, the ratio between the upper end of human hearing (20 kilohertz) and middle C (262 hertz) is roughly 80. If we use a representation based on ratio rather than absolute difference, then the spacing between frequencies would not change even when we changed the unit.

We have such a representation: logarithms! On a logarithmic scale, a distance corresponds to a ratio rather than a difference. To see the contrast, let's place the numbers from 1 to 10 on a logarithmic scale.

The physical gap between 1 and 2 represents not their difference but rather their ratio, namely 2. According to my ruler, the gap is approximately 3.16

centimeters. Similarly, the physical gap between 2 and 3 — approximately 1.85 centimeters — represents the smaller ratio 1.5. In contrast to their relative positions on a linear scale, 2 and 3 on a logarithmic scale are closer than 1 and 2 are. On a logarithmic scale, 1 and 2 have the same separation as 2 and 4: Both gaps represent a ratio of 2 and therefore have the same physical size (3.16 centimeters).

Problem 3.5 Practice with ratio thinking

On a logarithmic scale, how does the physical gap between 2 and 8 compare to the gap between 1 and 2? Decide based on your understanding of ratios; then check your reasoning by measuring both gaps.

Problem 3.6 More practice with ratio thinking

Is the gap between 1 and 10 less than twice, equal to twice, or more than twice the gap between 1 and 3? Decide based on your understanding of ratios; then check your reasoning by measuring both gaps.

Problem 3.7 Moving along a logarithmic scale

On the logarithmic scale in the text, the gap between 2 and 3 is approximately 1.85 centimeters. Where do you land if you start at 6 and move 1.85 centimeters right-ward? Decide based on your understanding of ratios; then check your reasoning by using a ruler to find the new location.

Problem 3.8 Extending the scale to the right

On the logarithmic scale in the text, the gap between 1 and 10 is approximately 10.5 centimeters. If the scale were extended to include numbers up to 1000, how large would the gap between 10 and 1000 be?

Problem 3.9 Extending the scale to the left

If the logarithmic scale were extended to include numbers down to 0.01, how far to the left of 1 would you have to place 0.04?

On a logarithmic scale, the frequencies related to hearing arrange themselves as follows:

Changing the units to kilohertz just shifts all the frequencies, but leaves their relative positions invariant:

Problem 3.10 Acoustic energy fluxes

In acoustics, sound intensity is measured by energy flux, which is measured in decibels (dB) — a logarithmic representation of watts per square meter. On the decibel scale, 0 decibels corresponds to the reference level of 10−12 watts per square meter.

Every 10 decibels (or 1 bel) represents an increase in energy flux of a factor of 10 (thus, 20 decibels represents a factor-of-100 increase in energy flux).

a. How many watts per square meter is 60 decibels (the sound level of normal conversation)?

b. Place the following energy fluxes on a decibel scale: 10−9 watts per square meter (an empty church), 10−2 watts per square meter (front row at an orchestra concert), and 1 watt per square meter (painfully loud).

Logarithmic scales offer two benefits. First, as we saw explicitly, logarithmic scales incorporate invariance. The second benefit was only implicit in the previous discussion: Logarithmic scales, unlike linear scales, allow us to represent a huge range. For example, if we include power-line hum (50 or 60 hertz) on the linear frequency scale on p. 61, we can hardly distinguish its position from 0 kilohertz. The logarithmic scale has no problem.

In our fallen world, benefits usually conflict. One usually has to sacrifice one benefit for another (speed for accuracy or justice for mercy). With logarithmic scales, however, we can eat our cake and have it.

Problem 3.11 Labeling a logarithmic scale

Let's make a scale to represent sizes in the universe, from protons (10−15 meters) to galaxies (1030 meters), with people and bacteria in between. With such a large range, we should use a logarithmic scale for size 𝐿. Which one of these two ways of labeling the scale is correct, and which way is nonsense?

Logarithmic scales can make otherwise obscure symbolic calculations intuitive. An example is the geometric mean, which we used in Section 1.6 to make gut estimates:

```
estimate = √ lower bound × upper bound. (3.4)
```

Geometric means also occur in the physical world.

As you found in Problem 2.9, the distance 𝑑 to the horizon, as seen from a height ℎ above the Earth's surface, is

```
𝑑 ≈ √h𝐷 , (3.5)
```

where 𝐷 = 2𝑅Earth is the diameter of the Earth.

Imagine a lifeguard sitting with his or her eyes at a height ℎ = 4 meters above sea level. Then the distance to the horizon is:

To do the calculation, we convert 12 000 kilometers to 1.2 × 107 meters, calculate 4 × 1.2×107, and compute the square root: 

```
𝑑 ≈ 4 × 1.2×107 m ≈ 7000 m = 7 km. (3.7)
```

In this symbolic form with a square root, the calculation obscures the fundamental structure of the geometric mean. We first calculate ℎ𝐷, which is an area (and often contains, as it did here, a huge number). Then we take the square root to get back a distance. However, the area has nothing to do with the structure of the problem. It is merely a bookkeeping device.

Bookkeeping devices are useful; they are how you tell a computer what to calculate. However, to understand the calculation, we, as humans, should use a logarithmic scale to represent the distances. This scale captures the structure of the problem.

How can we describe the position of the geometric mean √h𝐷 ?

The first clue is that the geometric mean, because it is a mean, lies somewhere between ℎ and 𝐷. This property is not obvious from the calculation using the square root. To find where the geometric mean lies, mind the gaps. On a logarithmic scale, a gap right represents the ratio of its endpoints. As shown in the table, the left and right gaps represent the same ratio, namely 𝐷/ℎ! Therefore, on the logarithmic scale, the geometric mean lies exactly halfway between ℎ and 𝐷.

Based on this ratio representation, we can rephrase the geometric-mean calculation in a form that we can do mentally.

What distance is as large compared to 4 meters as 12 000 kilometers is compared to it?

For lack of imagination, my first guess is 1 kilometer. It's 12 000 times smaller than the diameter 𝐷 (which is 12 000 kilometers), but only 250 times larger than the height ℎ (4 meters). My guess of 1 kilometer is therefore somewhat too small.

How is a guess of 10 kilometers?

It's 2500 times larger than ℎ, but only 1200 times smaller than 𝐷. I overshot slightly. How about 7 kilometers? It's roughly 1750 times larger than 4 meters, and roughly 1700 times smaller than 12 000 kilometers. Those gaps are close to each other, so 7 kilometers is the approximate geometric mean.

Similarly, when we make gut estimates, we should place our lower and upper estimates on a logarithmic scale. Our best gut estimate is then their midpoint. What a simple picture!

Should all quantities be placed on a logarithmic scale?

No. An illustrative contrast is between size and position. Both quantities have the same units. But size ranges from 0 to ∞, whereas position ranges from −∞ to ∞. Position therefore cannot be placed on a logarithmic scale (where would you put −1 meter?). In contrast, size (a magnitude) belongs on a logarithmic scale. In general, location parameters, such as position, should not be placed on a logarithmic scale but magnitudes should.

3.1 不变量

当我们发现有一个量在复杂的环境中保持不变，我们就使用这个工具。这个守恒的量称为不变量。找到不变量会简化很多问题。

我们在章节 1.2 估算高速公路一个车道的运输能力时曾出现第一个不变量，但当时并未指出。运输能力 —— 即车道上运输车辆的通过率 —— 取决于运输车辆之间的间距和车辆的速度。我们已经可以估算这些量并得到运输能力。然而，车辆间距和车辆速度是不断变化的量，所以这些估算很难做到可靠。作为替代，我们使用了 2 秒跟随规则。只要驾驶员遵守这个规则，则在驾驶的时候车距就是 2 秒。因此，每辆车后面每隔 2 秒就会有一辆车这就是这个车道的运输能力（单位时间经过的车辆数）。通过找到一个不变量，我们简化了一个复杂多变的过程。每当出现变化的时候，就去找不变的东西！【这个聪明方法来自阿瑟·恩格尔（Arthur Engel）的《问题解决策略》（Problem-Solving Strategies）16 一书。】

3.1.1 下雨时是跑还是走？

我们将用这个工具来体验一下，在雨中应该走还是跑。下着倾盆大雨，你的伞在家里，而你的家在数百米之外。

➤ 为了使你最小限度的湿身，在雨中应该走还是跑？

让我们作三个简化之后再来回答这个问题。首先，假定没有风，因此雨滴都是垂直下落。其次，假定雨是恒定的。第三，假定你的身体是很薄的片状：在沿着到家的方向上没有厚度（这个近似在我年轻时更适用）。等价地说，你的头部被防水帽保护着，所以不用担心雨滴会打你头上。你试图尽可能减少打到你正面的雨滴总量。

你唯一的自由度 —— 你可以用来改变的唯一参数 —— 就是你的速度。高速可以让你在雨中停留较短的时间。然而，这也使雨滴更直接地打到你身上（更偏水平方向）。但有一个量是不变的，且与你的速度无关，即你扫过的空气体积。因为雨是恒定的，一定的体积包含的雨滴数是固定的，与你的速度无关。只有这些雨滴会打在你身体正面。因此，不管你速度多大，你湿身的程度是一样的。

这个令人惊讶的结论是「每当有变化时，就去寻找不变量」的原理的另一个应用。在这里，我们可以通过选择是走还是跑来改变速度。然而不管速度如何，我们将扫过相同的空气体积 —— 这是我们的不变量。

因为通过不变性分析得到的结论，即在雨中是走还是跑对湿身程度没有影响，是令人惊讶的，你可能对此还有一点点怀疑。当然，我们几乎会本能地选择在雨中跑，这的确会比在雨中悠闲地散步更优越。

为了避免湿身，在雨中跑是不理性的吗？

如果你是无限薄的，就像是一个矩形在雨中行进，那么前面的分析是适用的：不管你是走还是跑，你身体的正面吸收的雨滴数量是相同的。但大部分人是有一个厚度的，落在头上的雨滴数量和我们的速度有关。如果你的头是暴露的，那么你会在意有多少雨滴落在头上，这时你就应该跑。但如果你头上有覆盖，那你大可节省你的能量并享受你的漫步。跑步不会让你更干爽。

3.1.2 平铺一个老鼠啃过的棋盘

实践一个新工具的最佳方式通常是将其应用于一个数学问题。这样就不会将真实世界的复杂性添加到学习新工具的过程中。所以，下面就是一个数学问题：一个单人游戏。

一只老鼠啃掉了一个标准 8×8 棋盘的对角线上两端的 2 个格子。我们有一盒矩形的 2×1 的多米诺骨牌。

➤ 这些多米诺骨牌可以平铺这个被老鼠啃过的棋盘吗？换句话说，我们能否将骨牌覆盖整个棋盘的每一个格子（既没有空格，也没有重叠）？

将一块骨牌放在棋盘上是这个单人游戏的一步。对游戏的每一步，你可以选择将骨牌放在哪里 —— 所以在每一步你都有很多选择。可能的步骤的数量增加非常迅速。因此，我们要寻找不变量：一个在游戏的任何步骤中都不会变的量。

因为每个骨牌覆盖 1 个白格子和 1 个黑格子，下列的量 I 是不变的（保持恒定）：

```
I = 未覆盖的黑格子 - 未覆盖的白格子
```

一个规则的棋盘上，有 32 个白格子和 32 个黑格子，因此开始时有 I=0。啃过的棋盘少了两个黑格子，因此开始时有 I=30-32=-2。到游戏完成时，所有格子都被覆盖，所以 I=0。因为 I 是不变量，所以这个游戏不可能完成，即多米诺骨牌不可能平铺这个被啃过的棋盘。

不变量如此有威力的部分原因在于这是一种抽象。空格的细节 —— 即空格的准确位置 —— 并不构成抽象的障碍。跨过这个障碍，我们只看到黑格子超过白格子的数目就够了。这一抽象包含了我们所需要知道的所有信息，即我们永远不可能平铺这个棋盘。

题 3.1 立方体游戏

一个立方体的每个顶点都有一个数字，除了左下角的顶点从 1 开始外，所有顶点都从 0 开始。游 0 戏的每一步都是相同的：选取任何一条棱然后给棱 0 的两个顶点的数字各增加 1。游戏的目的是使所有顶点的数字都变成 3 的倍数。

比如，选取前面最下面的棱，然后再选取相对的底面另一条棱，得到下列立方体构型的序列：

尽管上述构型没有一个完成游戏，但你能否通过不同的步骤来完成这个游戏？如果你能够完成，给出完成游戏的步骤。如果不能，则证明游戏不可能完成。

提示：创建和此游戏类似的、但更简单的版本。

题 3.2 三数组游戏

这是另一个单人游戏。从一个三数组（3,4,5）出发，在每一步，选择其中任意两个数。将其叫作 a 和 b。然后做下列替换：

```
a=>0.8a-0.6b

b=>0.6a+0.8b
```

你能达到（4,4,4）吗？如果你能做到，给出步骤；否则，证明不可能做到。

题 3.3 三数组游戏看成空间的转动

在三数组游戏（题 3.2）中，根据在 3 个数 a, b 和 c 中选择哪两个数进行替换操作，会有 3 种可能的步骤。试将这 3 种方式用空间转动来描写，即对于每一种步骤，给出转动轴和转动角度。

题 3.4 圆锥摆

即使是小振幅，找出一个摆的周期也需要微积分，这是因为摆的速度不断变化。

任何时候当有变化发生时，就应该去寻找不变量。因此，被大物理学家索末菲 [1]（Arnold Sommerfeld）称为「所有时代最天才的钟表匠」的惠更斯 [2]（Christiaan Huygens）分析了在水平圆周上摆的运动（圆锥摆）：将这个二维运动投影到一个竖直的屏上就得到一个维摆的运动；这样，二维运动的周期就和一维摆的运动周期相同！利用这个想法找出摆的周期（不使用微积分！）。

1 德国物理学家，量子力学和原子物理学的先驱之一。—— 译者注

2 荷兰物理学家，光的波动理论奠基者。—— 译者注

3.1.3 对数比例

在章节 3.1.2 的游戏中，每一步都是用一个骨牌来覆盖棋盘的两个格子。在我们理解世界的游戏中，一个很常见的步骤是改变单位制。和游戏一样，我们要问，「当一个步骤进行时，什么量是不变的？」作为一个理清我们思路的例子，下面是与人类听觉相关的频率。我们首先用千赫兹（kHz）作为单位。频率的分布按下图排列：

听觉下限 —— 20Hz

钢琴中音 C —— 262Hz

钢琴高音 C —— 4186Hz

听觉上限 —— 20kHz

现在将单位从千赫兹变成赫兹（Hz），并保持点 0、10 和 20 在原图中标记的位置不变。这个变化将每个频率间隔放大了 1000 倍。如果原点保持固定，则 20 赫兹就到了原来 20 千赫兹的位置（大约在原点右侧 10 厘米处），然后 20 千赫兹，即人类听觉的频率上限，就到了右边 100 米的位置 —— 远远超出了页面的范围。这个新的标度可说是无用的。

幸运的是，这里有一个不变量：即频率的比。比如，人类听觉的频率上限（20 千赫兹）和中音 C（262 赫兹）的比大约是 80。如果我们使用一种基于比例而不是绝对差的表示，则当我们改变单位时，频率的间隔将不会变化。

我们已经有了这样的表示：对数！在对数比例尺上，间距对应的是比例，而不是差。为了对比，我们将 1 到 10 这些数标在对数比例尺上。

1 和 2 之间的实际间距表示的不是两个数的差而是两个数的比，即 2。按照我的标尺和画图程序所画的，这个间距大约是 3.16 厘米。类似地，2 和 3 之间的实际间距一大约 1.85 厘米 —— 表示的是较小的比 1.5。与在线性标尺上的相对位置不同，对数比例尺上 2 和 3 之间要比 1 和 2 之间靠得近些。在对数比例尺上，1 和 2 之间与 2 和 4 之间的间距相同：这两个间距都表示比例 2，因此具有相同的大小 3.16 厘米。

题 3.5 练习用比例来思考

在对数比例尺上，2 和 8 之间的实际间距与 1 和 2 之间的实际间距相比如何？在你对比例的理解基础上回答，然后通过测量这两个间隔的距离来验证你的分析。

题 3.6 更多用比例思考的练习

1 和 10 之间的间距是小于，等于还是大于 1 和 3 之间间距的 2 倍？在你对比例的理解基础上回答，然后通过测量这两个间隔的距离来验证你的分析。

题 3.7 对数比例尺上的移动

上面描述的对数比例尺上，2 和 3 之间的实际间距大约为 1.85 厘米。如果从 6 开始向右移动 1.85 厘米则会到达哪一点？在你对比例的理解基础上回答，然后通过使用标尺找到新的位置来验证你的分析。

题 3.8 将标尺向右扩展

上面描述的对数比例尺上，1 和 10 之间的实际间距大约为 10.5 厘米。如果标尺扩展到包含数字 1000，则 10 和 1000 之间的实际间距是多大？

题 3.9 将标尺向左扩展

如果对数比例尺扩展到包括数字小至 0.01，则在 1 的左边多远是 0.04 的位置？

在对数比例尺上，相应于听觉的频率分布如下图所示：

将单位改成千赫兹只是将所有频率平移，但相对位置没有变化。

题 3.10 声学能流

在声学中，声音强度用能流来衡量，其单位是分贝（B）瓦/ 米$^2$的对数。对于分贝标度，0 对应于 10$^-12$ 瓦/米$^2$的能流水平。每 10 分贝（1 贝尔）表示能流增加 10 倍。

a）60 分贝对应多少瓦/米$^2$（正常谈话的声音水平）？

b）将下列能流标在分贝标度尺上：10$^-9$ 瓦/米$^2$（空无一人的教堂），10$^-2$ 瓦/米$^2$（音乐会的前排位置），及 1 瓦/米$^2$（声音强得令人痛苦）。

对数标度有两个好处。1）我们已经明显看到，对数标度自然地将不变性包含在内了；2）这一好处隐含在前面的讨论中：与线性标度不同，对数标度可以表示巨大的范围。比如，要想在 63 页的线性标度上表示电力线的嗡嗡声频率（50-60 赫兹）位置，则几乎不可能将其与 0 千赫兹区别开来。而对数标度则毫无问题。

在我们这个世界，利益常常是彼此冲突的。我们通常不得不为了一个利益去牺牲另一个利益（速度相对于准确或者公正相对于怜悯）。利用对数标度，我们就可以鱼与熊掌兼得。

题 3.11 标记一个对数标度

我们来做一个标尺表示宇宙的大小，从质子（10$^-15$ 米）到星系（10$^30$ 米），其中包括人和细菌的尺度。对于如此巨大的范围，我们用长度为 L 的对数标度尺。下列两种标度方式哪一种是正确的，哪一种是没有意义的？

对数标度可以使得原先含糊的符号运算变得直观。几何平均就是一个例子，我们曾在章节 1.6 用来进行直觉估算：

```
估算值 =√下限 X 上限
```

几何平均也出现在现实世界中。正如在题 2.9 看到的，在地球表面高度为 h 的地方能看到的地平线的距离 d 为：

```
d≈√hD
```

其中 D=2R 地球为地球直径。假定有个救生员，其眼睛高度在海平面上 h=4 米处，则到地平线的距离为：

为了进行计算，我们将 12000 千米写成 1.2×10$^7$  米，计算 4×1.2×10$^7$，然后开方：

在这种形式下，计算模糊了几何平均的结构。我们首先计算 hD，这是一个面积（通常会包含巨大的数字，正如这个例子所示）。然后我们通过开方得到距离。但是，这个面积和问题的结构毫无关系，只是一个中间过程。

中间过程是有用的，这正是你要告诉计算机的计算过程。但为了理解这个计算，我们作为人类，应该使用对数标度来表示距离。这个标度抓住了问题的本质。

➤ 几何平均√hD 位于何处？

第一个线索，几何平均是一种平均，则一定位于 h 和 D 之间的某个位置。这个性质在用平方根计算时并不是那么明显。为了找到几何平均的位置，想一想间距。在对数标度上，间隔表示的是两个端点的比值。如表中所示，左边的间距和右边的间距表示的是同样的比值！因此，在对数标度上，几何平均正好位于 h 和 D 的中间。

基于这个比例表示，我们再强调一下：几何平均计算是一种可以心算的计算方式。

➤ 多大距离与 4 米的比正好是 12000 公里与其之比？

因为缺乏想象力，我首先猜测这个距离是 1 公里。它比地球直径 D（即 12000 公里）小 12000 倍，但只比高度 h（4 米）大 250 倍。我的 1 公里的猜测是太小了。

➤ 10 公里这个猜测怎么样？

这个距离比 h 大 2500 倍，但比 D 只小 1200 倍。又有点过头了。那 7 公里怎么样呢？这大约比 4 米大 1750 倍，大约比 12000 公里小 1700 倍。这两个间距非常接近，因此 7 公里是近似的几何平均。

```
√hD≈7km
```

因此，当我们进行直觉估算时，应该将上限和下限标记在对数标度上，则最好的直觉估算值就是二者的中点。这是多么简单的图像！

➤ 是否所有的量都应该标记在对数标度上？

答案是否定的。一个显而易见的对比是距离和位置。这两个量都有同样的单位。但距离的范围是从 0 到 ∞，然而位置的范围是从 -∞ 到 ∞。因而位置是无法标记在对数标度上的（你把一 1 米标在哪里呢？）。反之，距离（大小）可以标记在对数标度上。一般地，位置参数，如坐标不应该用对数标度来标记，而大小应该用对数标度来标记。

### 3.2 From invariant to symmetry operation

In the preceding examples, we knew the moves of the game and sought the invariant. In the mouse-eaten chessboard (Section 3.1.2), the moves are putting down a 2×1 domino on two adjacent empty squares. The invariant was the difference between empty black and white squares. Often, however, the benefit of invariants lies in the other direction: You know the invariant and seek the moves that preserve it. These moves are called the symmetry operations or simply the symmetries.

We'll first examine this idea in a familiar situation: converting units (Section 3.2.1). Then we'll practice it on a sum solved by the three-year-old Carl Friedrich Gauss (Section 3.2.2) and then by finding maxima and minima (Section 3.2.3).

#### 3.2.1 Converting units

We often convert a quantity from one unit system to another — for example, mass from English to metric units or prices from dollars to pounds or euros.

A useful physical conversion is writing energy density — energy divided by amount of stuff — in useful units. Let's start with the reasonable energy unit for a chemical bond, namely the electron volt or eV (Section 2.1). Then a useful unit for energy density is 

```
1 eV / molecule. (3.8)
```

This energy density is our invariant. As we convert from one unit system to another, our moves have to preserve the energy density.

What are the legal moves — the moves that preserve the energy density?

The legal moves are all ways of multiplying by:

(3.9)

Either quotient is a form of 1, because 1 mole is defined to be Avogadro's number of molecules, and Avogadro's number is 6×1023. I carefully wrote「1 mol」with the number rather than simply as「mol.」The more explicit form reminds us that「6×1023 molecules per mole」is shorthand for a quotient of two identical quantities: 6×1023 molecules and 1 mole.

Multiplying the energy density by the first form of 1 gives 1 eV:

(3.10)

(If we had multiplied by the second form of 1, the units of molecules would have become molecules squared instead of canceling. The strike-through lines help us check that we got the desired units.) The giant exponent makes this form almost meaningless. To improve it, let's multiply by another form of 1, based on the definition of an electron volt. Two forms of 1 are:

(3.11)

Multiplying by the first form of 1 gives:

(3.12)

(A more exact value is 96 kilojoules per mole.) In the United States, energies related to food are stated in Calories, also known as kilocalories (roughly 4.2 kilojoules). In calorie units, the useful energy-density unit is:

Which form is more meaningful: 23 kcal/mol or 23 kcal/mol?

The forms are mathematically equivalent: You can multiply by 23 before or after dividing by a mole. However, they are not psychologically equivalent. The first form builds the abstraction of kilocalories per mole, and then says,「Here are 23 of them.」In contrast, the second form gives us the energy for 1 mole, a human-sized amount. The second form is more meaningful.

Similarly, the speed of light 𝑐 is commonly quoted as (approximately) 

(3.14)

The psychologically fruitful alternative is

(3.15)

This form suggests that 300 million meters, at least for light, is the same as 1 second. With this idea, you can convert wavelength to frequency (Problem 3.14); with a slight extension, you can convert frequency to energy (Problem 3.15) and energy to temperature (Problem 3.16).

Problem 3.12 Absurd units

By multiplying by suitable forms of 1, convert 1 furlong per fortnight into meters per second.

Problem 3.13 Rainfall units

Rainfall, in nonmetric parts of the world, is sometimes measured in acre feet. By multiplying by suitable forms of 1, convert 1 acre foot to cubic meters. (One square mile is 640 acres.)

Problem 3.14 Converting wavelength to frequency

Convert green-light wavelength, 0.5 micrometers (0.5 μm), to a frequency in cycles per second (hertz or Hz).

Problem 3.15 Converting frequency to energy

Analogously to how you used the speed of light in Problem 3.14, use Planck's constant ℎ to convert the frequency of green light to an energy in joules (J) and in electron volts (eV). This energy is the energy of a green-light photon.

Problem 3.16 Converting energy to temperature

Use Boltzmann's constant 𝑘B to convert the energy of a green-light photon (Problem 3.15) to a temperature (in kelvin). This temperature, except for a factor of 3, is the surface temperature of the Sun!

Conversion factors need not be numerical. Insight often comes from symbolic factors. Here is an example from fluid flow. As we will derive in Section 5.3.2, the drag coefficient 𝑐d is defined as the dimensionless ratio:

(3.16)

where 𝜌 is the fluid density, 𝑣 is the speed of the object moving in the fluid, and 𝐴 is the object's cross-sectional area. To give this definition and ratio a physical interpretation, multiply it by 𝑑/𝑑, where 𝑑 is the distance that the object travels:

(3.17)

The numerator, 𝐹drag𝑑, is the work done or the energy consumed by drag.

In the denominator, the product 𝐴𝑑 is the volume of fluid displaced by the object, so 𝜌𝐴𝑑 is the corresponding mass of fluid. Therefore, the denominator is also

(3.18)

The object's speed 𝑣 is also approximately the speed given to the displaced fluid (which the object shoved it out of its way). Therefore, the denominator is roughly

(3.19)

This expression is the kinetic energy given to the displaced fluid. The drag coefficient is therefore roughly the ratio

(3.20)

My tenth-grade chemistry teacher, Mr. McCready, told us that unit conversion was the one idea that we should remember from the entire course.

Almost every problem in the chemistry textbook could be solved by unit conversion, which says something about the quality of the book but also about the power of the method.

3.2.2 Gauss's childhood sum

A classic example of going from the invariant to the symmetry is the following story of the young Carl Friedrich Gauss. Although maybe just a legend, the story is so instructive that it ought to be true. Once upon a time, when Gauss was 3 years old, his schoolteacher, wanting to occupy the students, assigned them to compute the sum

```
𝑆 = 1 + 2 + 3 + ⋯ + 100, (3.21)
```

and sat back to enjoy the break. In a few minutes, Gauss returned with an answer of 5050.

Was Gauss right? If so, how did he compute the sum so quickly?

Gauss saw that the sum — the invariant — is unchanged when the terms are added backward, from highest to lowest:

```
1 + 2 + 3 + ⋯ + 100 = 100 + 99 + 98 + ⋯ + 1. (3.22)
```

Then he added the two versions of the sum, the original and the reflected: 

(3.23)

In this form, 2𝑆 is easy to compute: It contains 100 copies of 101. Therefore, 2𝑆 = 100 × 101, and 𝑆 = 50 × 101 or 5050 — as the young Gauss claimed. He made the problem so simple by finding a symmetry: a transformation that preserved the invariant.

Problem 3.17 Number sum

Use Gauss's method to find the sum of the integers between 200 and 300 (inclusive).

Problem 3.18 Symmetry for algebra

Use symmetry to find the missing coefficients in the expansion of 

```
(𝑎 − 𝑏)3: (𝑎 − 𝑏)3 = 𝑎3 − 3𝑎2𝑏+? 𝑎𝑏2+? 𝑏3. (3.24)
```

Problem 3.19 Integrals

Evaluate these definite integrals. Hint: Use symmetry.

3.2.3 Finding maxima or minima

To practice finding the symmetry operation, we'll find the maximum of the function 6𝑥 − 𝑥2 without using calculus. Calculus is the elephant gun. It can solve many problems, but only after blasting them into the same form (smithereens). Avoiding calculus forces us to use more particular, but more subtle methods — such as symmetry. As Gauss did in summing 1 + 2 + ⋯ + 100, let's find a symmetry operation that preserves the essential feature of the problem — namely, the location of the maximum.

Symmetry implies moving around an object's pieces. Fortunately, our function 6𝑥 − 𝑥2 factors into pieces:

```
6𝑥 − 𝑥2 = 𝑥(6 − 𝑥). (3.25)
```

This form, along with the idea that multiplication is commutative, suggests the symmetry operation. For if the operation just swaps the two factors, replacing 𝑥(6 − 𝑥) with (6 − 𝑥)𝑥, it does not change the location of the maximum. (A parabola has exactly one maximum or minimum.) The symmetry operation that makes the swap is 

```
𝑥 ⟷ 6 − 𝑥. (3.26)
```

It turns 2 into 4 (and vice versa) and 1 into 5 (and vice versa). The only value unchanged (left invariant) by the symmetry operation is 𝑥 = 3. Therefore, 6𝑥 − 𝑥2 has its maximum at 𝑥 = 3.

Geometrically, the symmetry operation reflects the graph of 6𝑥 − 𝑥2 through the line 𝑥 = 3. By construction, this symmetry operation preserves the location of the maximum. Therefore, the maximum has to lie on the line 𝑥 = 3.

We could have found this maximum in several other ways, so the use of symmetry might seem superfluous or like overkill.

However, it warms us up for the following, more compli-x = 3

cated use. The energy required to fly has two pieces: generating lift, which requires an energy 𝐴/𝑣2, and fighting drag, which requires an energy 𝐵𝑣2. (𝐴 and 𝐵 are constants that we estimate in Sections 3.6.2 and 4.6.1.)

(3.27)

To minimize fuel consumption, planes choose their cruising speed to minimize 𝐸flight. More precisely, a cruising speed is selected, and the plane is designed so that this speed minimizes 𝐸flight.

In terms of the constants 𝐴 and 𝐵 , what speed minimizes 𝐸 flight?

Like the parabola 𝑥(6−𝑥), this energy has one extremum. For the parabola, the extremum was a maximum; here, it is a minimum. Also similar to the parabola, this energy has two pieces connected by a commutative operation. For the parabola, the operation was multiplication; here, it is addition.

Continuing the analogy, if we find a symmetry operation that transposes the two pieces, then the speed preserved by the operation will be the minimum-energy speed.

Finding this symmetry operation is hard to do in one gulp, because it must transpose 1/𝑣2 and 𝑣2 and transpose 𝐴 and 𝐵. These two difficulties suggest that we apply divide-and-conquer reasoning: Find a symmetry operation that transposes 1/𝑣2 and 𝑣2, and then modify so that it also transposes 𝐴 and 𝐵.

To transpose 1/𝑣2 and 𝑣2, the symmetry operation is the following:

```
𝑣 ⟷ 1𝑣. (3.28)
```

Now let's restore one of the two constants and modify Eflight the symmetry operation so that it transposes 𝐴/𝑣2 and Edrag

(3.29)

Now let's restore the second constant, 𝐵, and find the full symmetry operation that transposes 𝐴/𝑣2 and 𝐵𝑣2: 

(3.30)

Rewriting it as a replacement for 𝑣, the symmetry operation becomes 

(3.31)

This symmetry operation transposes the drag energy and lift energy, leaving the total energy 𝐸flight unchanged. Solving for the speed preserved by the symmetry operation gives us the minimum-energy speed: 

(3.32)

In Section 4.6.1, once we find 𝐴 and 𝐵 in terms of the characteristics of the air (its density) and the plane (such as its wingspan), we can estimate the minimum-energy (cruising) speeds of planes and birds.

Problem 3.20 Solving a quadratic equation using symmetry 

The equation 6𝑥−𝑥2 +7 = 0 has a solution at 𝑥 = −1. Without using the quadratic formula, find any other solutions.

3.2 从不变性到对称操作

在前面的例子中，我们知道游戏的玩法，然后寻找不变量。在被老鼠啃过的棋盘（章节 3.1.2）中，玩法是将一个 2×1 的骨牌放在两个相邻的空格上。不变量是黑空格数与白空格数之差。然而，通常不变量的好处是在另一个方面：你知道了不变量，然后寻找保持这个量不变的玩法。这些玩法称为对称操作，或简单地叫作对称。

我们将先在一个熟悉的情况下考察这个概念：单位转换（章节 3.2.1）。然后我们通过一个高斯 [1] 3 岁时解决的求和问题（章节 3.2.2）及寻找极大和极小问题（章节 3.2.3）来体验一下。

[1] 德国数学家，物理学家，近代数学奠基者之一。 —— 译者注

3.2.1 单位转换

我们常常把一个量从一个单位制转换到另一个单位制 —— 例如，质量用英制表示转换为用公制表示，或者价格从美元换成英镑或欧元。一个有用的例子是将能量密度（能量除以物质的量）以适合的单位表示。让我们首先对一个化学键用合理的能量单位表示，即电子伏或 eV（章节 2.1）。于是能量密度的单位是：

```
ev/分子
```

这个能量密度是我们的不变量。当我们从一个单位制转换到另一个单位制时，我们的所有操作必须保持能量密度不变。

➤ 什么操作是合法的操作，即保持能量密度不变的操作？

合法的操作就是用各种方式的 1 去乘 —— 比如，

这两个比例式都是 1 的一种形式，因为 1 摩尔定义为阿伏伽德罗常数个分子，而阿伏伽德罗常数为 6×10$^23$。我将分母仔细地写成包括数字的「1 摩尔」，而不是简单地写成摩尔。这个显式提醒我们，「6×10$^23$ 分子 / 摩尔」是两个相等量，即 6×10$^23$ 个分子和 1 摩尔之商的简化。

用第一种 1 的形式乘以能量密度得到：

（如果我们使用了第二种 1 的形式，则「分子」无法相互抵消而成了「分子^2」。斜线帮助我们看清所要得到的单位。）这个巨大的指数使得这个形式几乎没有什么意义。为了改进，让我们用基于电子伏定义的 1 的另一个形式来乘：

(3.11)

转换时将这个 1 包括进去后得到：

(3.12)

（更精确的值是 96 千焦 / 摩尔。) 在美国，与食物相关的能量用卡路里表示，也以千卡表示（粗略地等于 42 千焦）。用卡路里表示，能量单位是：

➤ 哪种形式更有意义，23（千卡/摩尔）还是 （23千卡）/摩尔？

数学上，这两种形式是等价的。你可以在除以 1 摩尔之前或之后乘以 23。但在感觉上并不一样。第一种形式建立了每摩尔和千卡数的关系，并且告诉我们「每摩尔是 23 千卡」。它将 23 与其自然的部分，即千卡这一单位分离。相反，第二种形式给出了 1 摩尔的能量，而 1 摩尔与人的大小可比拟，因而是更具有洞察力的形式。

类似地，通常光速 c 取为（近似地）：

```
3×10^8 m/s (3.14)
```

另一种感觉上更好的形式是：

```
c = (3x10^8m)/1s (3.15)
```

这个形式提示我们，至少对光而言，3 亿米的距离只是 1 秒钟而已。利用这个概念，可以将波长转换为频率（题 3.14）；稍微推广一下，可以将频率转换为能量（题 3.15）以及将能量转换为温度（题 3.16）。

题 3.12 荒谬的单位

通过乘 1 的适当形式，将 （1 弗隆）/（2 周）（1 弗隆约等于 201.168 米）转换为合理的单位（米 / 秒）。

题 3.13 雨量单位

在一些非公制国家，雨量常常用「英亩英尺」衡量。通过乘以 1 的适当形式，将 1 英亩英尺转换为米^3。

题 3.14 波长转换为频率

将绿光波长，0.5 微米，转换为频率（赫兹或 Hz）。

题 3.15 频率转换为能量

类似于你在题 3.14 中利用光速的方式，利用普朗克常数 h 将绿光频率转换为能量，并分别用焦耳（J）和电子伏（V）表示。这个能量就是绿光光子的能量。

题 3.16 能量转换为温度

利用玻尔兹曼常数 kB 将绿光光子的能量（题 3.15）转换为温度（用开尔文表示）。除因子 3，这个温度就是太阳表面的温度！

转换因子不一定是数值的。洞察常常来自符号因子。这是来自流体的一个例子。在章节 5.3.2 我们将导出作为无量纲比例的阻力系数 cd：

(3.16)

其中 ρ 是流体密度，v 是流体中物体的运动速度，A 是物体的横截面积。为了给这个定义和比例一个直观的解释，分子分母同乘 d，其中 d 为物体运动的距离：

分子（F阻力xd）是阻力做的功或消耗的能量。分母中 Ad 是物体在流体中移动时扫过的体积，所以 ρAd 就是相应的流体质量。因此，分母就是：

```
1/2 x 流体质量 x v^2 (3.18)
```

1『看到了流体力学里熟悉的公式：`1/2mv^2`。（2022-05-15）』

物体的速度。也近似是物体扫过的流体（即物体移动时扫过的流体）速度。因此，分母近似是：

```
1/2 × 流体质量 ×（流体速度）^2，（3.19) 
```

这就是物体扫过的流体动能。阻力系数因此近似就是下列比值：

```
cd ~ 阻力消耗的能量/转移给流体的能量 (3.20)
```

我十年级时的化学老师麦克里迪先生告诉我们，单位转换是我们在整个课程中应该记住的一个概念。化学教科书中几乎每个问题的求解都可能用到单位转换，这一方面说明了书的质量，另一方面也说明了这个方法的威力。

3.2.2 高斯儿时的求和

从不变量到对称性的一个典型例子是年幼的高斯的一则故事。尽管很可能是一个传说，但这个故事很有启发意义，理应是真实的。从前，当高斯 3 岁的时候，他的老师想让孩子们多打发点时间，就出了一道求和题目：

```
S=1+2+3+…+100, (3.21)
```

然后坐回去享受孩子们做题时的闲暇。过了几分钟，高斯拿着答案 5050 跑来了。

高斯是对的吗？如果是对的，那么他是如何这么快就得到答案的？

高斯在求和中看到某种不变性：如果把所有项颠倒，从最大加到最小，那么和是不变的，然后他把这两个和加起来 —— 原来的与颠倒顺序的：

```
1+2+3+. …+100=S

100+99+98+…+1=S

101+101+101+…+101-2S

(3.23)
```

利用这个形式，2S 容易计算：其包含 100 个 101。因此，2S=100×101。因此 S=50×101, 即 5050 —— 正如年幼的高斯所得到的。他通过发现的对称性将问题变得如此容易：即保持和不变的一个变换。

题 3.17 数字和

利用高斯的方法求 200 到 300（包含）之间自然数的和。

题 3.18 代数的对称性

利用对称性找出 (a-b)^3 展开式中缺失的系数：

```
(a-b)^3=a^3-3a^2b+?ab^3+?b3 (3.24)
```

题 3.19 积分

计算下列定积分：

3.2.3 求极大和极小值

为了练习寻找对称操作，我们不用微积分来求函数 6x-x^2 的极大值。微积分是一件利器，可以解决许多问题，但前提是需要将问题化为相同的形式（小碎片）。避免使用微积分迫使我们使用更特别的，但也是更精致的方法 —— 比如对称性。正如高斯在求和 1+2+…+100 时做的，我们来找一个对称操作使其保持问题的本质特征不变 —— 即极大的位置。

对称隐含了围绕物体各部分的运动。幸运的是，我们的函数 6x-x^2 可以因式分解为：

```
6x - x^2  = x(6-x) (3.25)
```

这个形式以及乘法可交换的性质，建议了一个对称操作。交换两个因子的操作，即将 x(6-x) 换成 (6-x)x，极值的位置是不变的。（一个抛物线有唯一的极大或极小值。）

交换的对称操作即：

```
x←→6-x (3.26)
```

这个操作将 2 变成 4（及相反），1 变成 5（及相反）。在对称操作下仅有的不变的量是 x=3。因此，6x-x^2 在 x=3 具有极大值。

从几何上来讲，对称操作关于直线 x=3 对极大值 6x-x$^2$ 的图形进行镜面反射。在这个变换中，对 6x-x$^2$ 称操作保持极大位置不变。因此，极大值必须位于直线 x=3 上。

我们可以有很多其他找极大值的方法，所以对称性的使用似乎是多余的或者是过分的。然而，这 x=3 是对我们下面在更复杂问题中应用对称性的一个预热。正如我们将在章节 4.6.1 研究飞行时所要学到的，飞行需要的能量有两部分，升力需要的能量是 A/v$^2$，阻力需要的能量是 Bv$^2$（A 和 B 都是常数，将在章节 4.6.1 中进行估算）：

(3.27)

为了最小化燃料消耗，飞机选择巡航速度来最小化 E 飞行。更精确点说，巡航速度先选择好，飞机特意设计成在这个速度下 E 飞行最小。

➤ 用 A 和 B 表示，多大的速度最小化 E 飞行？

类似抛物线 x(6-x)，这个能量只有一个极值。对于抛物线，极值是极大值，而这里的能量是极小值。同样类似抛物线，能量也是两项通过「一个可交换的操作」组合而成。对于抛物线，这个操作是乘法，这里是加法。继续类比，如果我们找到一个交换这两项的对称操作，则保持不变的速度就是能量取极小的速度。

想一下子找到对称操作是困难的，因为必须交换 1/v$^2$ 和 v$^2$ 及交换 A 和 B。这两个困难提示我们使用分而治之法：先找到交换 1/v$^2$ 和 v$^2$ 的对称操作，然后加以修正使其也交换 A 和 B。

为了交换 1/v$^2$ 和 v$^2$，对称操作就是：

(3.28)

现在我们恢复其中一个常数并将对称操作 E 飞行修改为交换 A/v$^2$ 和 v$^2$：

(3.29)

现在我们恢复第二个常数 B，找出完整的交换 A/v$^2$ 和 Bv$^2$ 的对称操作：

(3.30)

球（重新写成）的变换，对称操作变成：

(3.31)

这个对称操作交换了阻力能量和升力能量，保持总能量 E 飞行不变。解出使对称操作保持不变的速度就给出能量最小的速度：

(3.32)

在章节 4.6.1，一旦我们找到用空气特性（如密度）和飞机（如机翼）表示的 A 和 B，我们就能估算飞机和鸟的最节省能量的速度。

题 3.20 利用对称性求解二次方程

方程 6x-x^2+7=0 有一个解 x=-1。不用二次方程的求根公式，找出另一个解。

### 3.3 Physical symmetry

For a physical application of symmetry, imagine a uniform metal sheet, perhaps aluminum foil, cut into the shape of a regular pentagon. Imagine that to the edges are attached heat sources and sinks — big blocks of metal at a fixed temperature — in order to hold the edges at the temperatures marked on the figure. After we wait long enough, the temperature distribution in the pentagon stops changing (comes to equilibrium).

Once the pentagon temperature equilibrates, what is the temperature at its center?

A brute-force, analytic solution is difficult. Heat flow is described by the heat equation, a linear second-order partial-differential equation: 

```
𝜅∇2𝑇 = ∂𝑇/∂𝑡 (3.33)
```

where 𝑇 is the temperature as a function of position and time, and 𝜅 (kappa) is the thermal diffusivity (which we will study in more detail in Chapter 7).

But don't worry: You do not have to understand the equation, only that it is difficult to solve!

Once the temperature settles down, the time derivative becomes zero, and the equation simplifies to 𝜅∇2𝑇 = 0. However, even this simpler equation has solutions only for simple shapes, and the solutions are complicated. For example, the temperature distribution on the simpler square sheet is hardly intuitive (the figure shows contour lines spaced every 10∘). For a pentagon, the temperature distribution is worse. However, because the pentagon is regular, symmetry might make the solution flow.

What is a useful symmetry operation?

Nature, in the person of the heat equation, does not care about the direction of our coordinate system. Thus, rotating the pentagon about its center does not change the temperature at the center. Therefore, the following five orientations of the pentagon share the same central temperature: 

Like Gauss adding the two versions of his sum (Section 3.2.2), stack these sheets mentally and add the temperatures that lie on top of each other to make the temperature profile of a new super sheet (adding the temperatures is valid because the heat equation is linear).

(3.34)

Each super edge contains one 80∘ edge and four 10∘ edges, for a temperature of 120∘. The super sheet is a regular pentagon where all edges are at 120∘.

Therefore, the temperature throughout the sheet is 120∘ — including at the center. Because the symmetry operation has helped us construct a much easier problem, we did not have to solve the heat equation.

One more step tells us the temperature in the center of the original sheet.

The symmetry operation rotates the pentagon about its center; when the plates are stacked, the centers align. Each center then contributes one-fifth of the 120∘ in the center, so the original central temperature is 24∘.

To highlight the transferable ideas (abstractions), compare the symmetry solutions to Gauss's sum and to this temperature problem. First, both problems seem complicated. Gauss's sum has many terms, all different; the pentagon problem seems to require solving a difficult differential equation.

Second, both problems contain a symmetry operation. In Gauss's sum, the symmetry operation reversed the order of the terms; for the pentagon, the symmetry operation rotates it by 72∘. Finally, the symmetry operation leaves an important quantity unchanged. For Gauss's problem, this quantity is the sum; for the pentagon, it is the central temperature.

When there is change, look for what does not change. Look for invariants and the corresponding symmetries: the operations that preserve the invariants.

Problem 3.21 Symmetry solution for a square sheet

Here is the contour plot again of the temperature on a square sheet. The contour lines are separated by 10∘. Use that information to label the temperature of each contour line. Based on the symmetry reasoning, what should the temperature at the center of the square be? Is this predicted temperature consistent with what is shown in the contour plot?

Problem 3.22 Simulating the heat equation

Using symmetry, we showed that the temperature at the center of the pentagon is the average of the temperatures of the sides. Check the solution by simulating the heat equation with a pentagonal boundary.

Problem 3.23 Shortest bisecting path

What is the shortest path that bisects an equilateral triangle into two equal areas?

Here are three examples of bisecting paths:

To set your problem-solving gears in motion, first rank these three bisecting paths according to their lengths.

3.3 物理对称

对于对称性的物理应用，考虑一个均匀的金属片，也许是铝箔，切割成规则的五边形。每个边都连接一个热源 —— 如保持固定温度的大块金属 —— 以使每条边都保持在图示所标的温度。当我们等足够长的时间后，五边形的温度分布不再变化（达到平衡）。

➤ 一旦五边形的温度达到平衡，其中心温度是多少？

硬算的话，想得到解析解是困难的。热流是由热方程描写的，一个二阶偏微分方程：

其中 T 是温度，是时间和空间的函数，而 k 是热扩散系数（我们将在第 7 章进行更详细的研究）。但是别担心：你不必懂这个方程，只要知道方程很难解就行！

一旦温度分布确定了，时间导数就变成零了，方程就简化为 `k∆^2T=0`。然而，即使是这个简化的方程也只是在形状简单的情况下有解，并且解是复杂的。比如，比较简单的正方形薄片上的温度分布也是很不直观的（图示是每 10 的等温线）。对于五边形，温度分布更复杂。但是，因为五边形是规则的，对称性也许能得到热流解。

➤ 有用的对称操作是什么？

从热方程的角度来看，大自然不会偏爱坐标系的某个方向。于是，将五边形围绕中心旋转不会改变中心温度。因此，下列五边形的五个取向具有相同的中心温度。

正如高斯将两种求和形式相加一样（章节 3.2.2），将这些薄片人为叠在一起将每一点的温度相加得到整个超级薄片的温度分布（将各温度值相加是有效的，因为热方程是线性的）。

每条边包含一个 80° 的边和四条 10° 的边，即温度为 120°。这个超薄片是一个规则的五边形，每条边的温度都是 120°。因此，整个薄片的温度都是 120° —— 包括中心。因为对称操作已经帮我们构造了一个更为简单的问题，我们不需要去解热方程了。

最后一步告诉我们原来的薄片中心温度。对称操作将五边形围绕中心旋转，当薄片叠加时，中心也叠加。因此每个薄片的中心贡献 120° 的 1/5，所以，原来的薄片中心温度为 24°。

比较高斯求和与薄片温度分布问题的对称性求解方法。这个比较启发我们得到一些可移植的概念（抽象）。首先，两个问题第一眼看起来都很复杂。高斯求和有很多项，所有的项都不同；五边形问题看起来需要求解一个困难的微分方程。其次，两个问题都包含了一个对称操作。在高斯求和中，对称操作是将求和顺序颠倒；对于五边形，对称操作是围绕中心旋转 72°。最后，对称操作保持了一个重要的量不变。对于高斯求和，这个量就是和；对于五边形，这个量是中心温度。

发生任何变化时，寻找不变的量。寻找不变量及相应的对称性，即保持这个量不变的操作。

题 3.21 正方形薄片的对称解

如图是一个正方形薄片的等温线图。这些等温线彼此相差 10°。

利用这个性质标出每根等温线的温度。基于对称性分析，正方形中心温度应该是多少？这个预测的温度和等温线显示的温度一致吗？

题 3.22 模拟热方程

利用对称性，我们证明了五边形中心温度是边缘温度的平均。通过模拟五边形边界下的热方程来验证这个解。

题 3.23 最短等分线

将一个等边三角形分为两个相同面积的最短等分线是什么？下图是三个例子。

为了能让你解决问题的步伐进入轨道，首先将这三个例子按照等分线长度来排序。

### 3.4 Box models and conservation

Invariance underlies a powerful everyday abstraction: box models. We already made a box model in Section 3.1.1, to decide whether to run or walk in the rain. Now let's examine this method further. The simplest kind of box contains a fixed amount of stuff — perhaps the volume of fluid or the number of students at an ideal university (where every student graduates in a fixed time). Then what goes into the box must come out. This conclusion seems simple, even simplistic, but it has wide application.

#### 3.4.1 Supply and demand

For another example of a box model, return to our estimate of US oil usage (Section 1.4). The flow oil into the box — the push or the supply — is the imported and domestically produced oil. The flow out of the box — the pull or the demand — is the oil usage. The estimate, literally taken, asks for the supply (how much oil is imported and domestically produced). This estimate is difficult. Fortunately, as long as oil does not accumulate in the box (for example, as long as oil is not salted away in underground storage bunkers), then the amount of oil in the box is an invariant, so the supply equals the demand. To estimate the supply, we accordingly estimated the demand. This conservation reasoning is the basis of the following estimate of a market size.

How many taxis are there in Boston, Massachusetts?

For many car-free years, I lived in an old neighborhood of Boston. I often rode in taxis and wondered about the size of the taxi market — in particular, how many taxis there were. This number seemed hard to estimate, because taxis are scattered throughout the city and hard to count.

The box contains the available taxi driving (measured, for example, as time). It is supplied byaxi drivers. The demand is due to taxi users. As long as the supply and demand match, we can estimate the supply by estimating the demand.

For estimating the demand, the starting point is that Boston has roughly 500 000 residents. As a gut estimate, each resident uses maybe one taxi per month, for a 15-minute ride: Boston taxis are expensive; unless one doesn't own a car, it's hard to imagine using them more often than once a month or for longer than 15 minutes. Then the demand is about 105 hours of taxi driving per month:

(3.35)

How many taxi drivers will that many monthly hours support?

Taxi drivers work long shifts, maybe 60 hours per week. I'd guess that they carry passengers one-half of that time: 30 hours per week or roughly 100 hours per month. At that pace, 105 hours of monthly demand could be supplied by 1000 taxi drivers or, assuming each taxi is driven by one driver, by 1000 taxis.

What about tourists?

Tourists are very short-term Boston residents, mostly without cars. Tourists, although fewer than residents, use taxis more often and for longer than residents do. To include the tourist contribution to taxi demand, I'll simply double the previous estimate to get 2000 taxis.

This estimate can be checked reliably, because Boston is one of the United States cities where taxis may pick up passengers only with a special permit, the medallion. The number of medallions is strictly controlled, so medallions cost a fortune. For about 60 years, their number was restricted to 1525, until a 10-year court battle got the limit raised by 260, to about 1800.

The estimate of 2000 may seem more accurate than it deserves. However, chance favors the prepared mind. We prepared by using good tools: a box model and divide-and-conquer reasoning. In making your own estimates, have confidence in the tools, and expect your estimates to be at least half decent. You will thereby find the courage to start: Optimism oils the rails of estimation.

Problem 3.24 Differential equation for an RC circuit box

Explain how a box model leads to the differential Requation for the low-pass 𝑅𝐶 circuit of Section 2.4.4: 

(3.36)

(Almost every differential equation arises from a box or conservation argument.)

Problem 3.25 Boston taxicabs tree

Draw a divide-and-conquer tree for estimating the number of Boston taxicabs.

First draw it without estimates. Then include your estimates, and propagate the values toward the root.

Problem 3.26 Needles on a Christmas tree

Estimate the number of needles on a Christmas tree.

#### 3.4.2 Flux

Flows, such as the demand for oil or the supply of taxi cabs, are rates — an amount per time. Physical flows are also rates, but they live in a geometry. This embedding allows us to define a related quantity: flux.

(3.37)

For example, particle flux is the rate at which particles (say, molecules) pass through a surface perpendicular to the flow, divided by the area of the surface. Dividing by the surface area, an operation with no counterpart in nonphysical flows (for example, in the demand for taxicabs), makes flux more invariant and useful than rate. For if you double the surface area, you double the rate. This proportionality is not newsworthy, and usually doesn't add insight, only clutter. When there is change, look for what does not change: Even when the area changes, flux does not.

Problem 3.27 Rate versus amount

Explain why rate (amount per time) is more useful than amount.

Problem 3.28 What is current density?

What kind of flux (flux of what?) is current density (current per area)?

The definition of flux leads to a simple and important connection between flux and flow speed. Imagine a tube of stuff (for example, molecules) with cross-sectional area 𝐴. The stuff flows through the tube at a speed 𝑣.

In a time 𝑡 , how much stuff leaves the tube?

In the time 𝑡, the stuff in the shaded chunk, spanning a length 𝑣𝑡, leaves the tube. This chunk has volume 𝐴𝑣𝑡. The amount of stuff

(3.38)

The amount of stuff per volume, the density of stuff, occurs so often that it usually gets a special symbol. When the stuff is particles, the density is labeled 𝑛 for number density (in contrast to 𝑁 for the number itself). When the stuff is charge or mass, the density is labeled 𝜌.

From the amount of stuff, we can find the flux: 

(3.39)

The product 𝐴𝑡 cancels, leaving the general relation flux of stuff = density of stuff × flow speed.

(3.40)

As a particular example, when the stuff is charge (Problem 3.28), the flux of stuff becomes charge per time per area, which is current per area or current density. With that label for the flux, the general relation becomes current density

where 𝑣drift is the flow speed of the charge — which you will estimate in Problem 6.16 for electrons in a wire.

The general relation will be crucial in estimating the power required to fly (Section 3.6) and in understanding heat conduction (Section 7.4.2).

#### 3.4.3 Average solar flux

An important flux is energy flux: the rate at which energy passes through a surface, divided by the area of the surface. Here, rate means energy per time, or power. Therefore, energy flux is power per area. An energy flux essential to life is the solar flux: the solar power per area falling on Earth.

This flux drives most of our weather. At the top of the atmosphere, looking directly toward the sun, the flux is roughly 𝐹 = 1300 watts per square meter.

However, this flux is not evenly distributed over the surface of the earth.

The simplest reason is night and day. On the night side of the Earth, the solar flux is zero. More subtly, different latitudes have different solar fluxes: The equatorial regions are warmer than the poles because they receive more solar flux than the poles do.

What is the solar flux averaged over the whole Earth?

We can find the average flux using a box model (a conservation argument). Here is sunlight coming to the Earth (with parallel rays, because the Sun is so far away). Hold a disk with radius 𝑅Earth perpendicular to the sunlight so that it blocks all sunlight that the Earth otherwise would get. The disk absorbs a power that we can find from the energy flux: 

```
power = energy flux × area = 𝐹𝜋𝑅2Earth, (3.42)
```

where 𝐹 is the solar flux. Now spread this power over the whole Earth, which has surface area 4𝜋𝑅2Earth:

Because one-half of the Earth is in night, averaging over the night and day-light parts of the earth accounts for a factor of 2. Therefore, averaging over latitudes must account for another factor of 2 (Problem 3.29).

Problem 3.29 Averaging solar flux over all latitudes

Integrate the solar flux over the whole sunny side of the Earth, accounting for the varying angles between the incident sunlight and the surface. Check that the result agrees with the result of the box model.

The result is roughly 325 watts per square meter. This average flux slightly overestimates what the Earth receives at ground level, because not all of the 1300 watts per square meter hitting the top of the atmosphere reaches the surface. Roughly 30 percent gets reflected near the top of the atmosphere (by clouds). The surviving amount is about 1000 watts per square meter.

Averaged over the surface of the Earth, it becomes 250 watts per square meter (which then goes into the surface and the atmosphere), or approximately 𝐹/5, where 𝐹 is the flux at the top of the atmosphere.

#### 3.4.4 Rainfall

These 250 watts per square meter determine characteristics of our weather that are essential to life: the average surface temperature and the average rainfall. You get to estimate the surface temperature in Problem 5.43, once you learn the reasoning tool of dimensional analysis. Here, we will estimate the average rainfall.

If the box representing the atmosphere holds a fixed amount of water — and over a long timescale, the amount is constant (it is our invariant) — then what goes into the box must come out of the box.

The inflow is evaporation; the outflow is rain. Therefore, to estimate the rainfall, estimate the evaporation — which is produced by the solar flux.

How much rain falls on Earth?

Rainfall is measured as a height of water per time — typically, inches or millimeters per year. To estimate global average rainfall, convert the supply of solar energy to the supply of rainwater. In other words, convert power per area to height per time. The structure of the conversion is power

(3.44)

where ?/? represents the conversion factor that we need to determine. To find what this conversion factor represents, we multiply both sides by area per power. The result is

(3.45)

What physical quantity could this volume per energy be?

We are trying to determine the amount of rain, so the volume in the numerator must be the volume of rain. Evaporating the water requires energy, so the energy in the denominator must be the energy required to evaporate that much water. The conversion factor is then the reciprocal of the heat of vaporization of water 𝐿vap, but expressed as an energy per volume. In Section 1.7.3, we estimated 𝐿vap as an energy per mass. To make it an energy per volume, just multiply by a mass per volume — namely, by 𝜌water: energy

(3.46)

Our conversion factor, volume per energy, is the reciprocal, 1/𝜌water𝐿vap.

Our estimate for the average rainfall then becomes solar flux going to evaporate water

(3.47)

For the numerator, we cannot just use 𝐹, the full solar flux at the top of the atmosphere. Rather, the numerator incorporates several dimensionless ratios that account for the hoops through which sunlight must jump in order to reach the surface and evaporate water:

The product of these four factors is roughly 9 percent. With 𝐿vap = 2.2 × 106 joules per kilogram (which we estimated in Section 1.7.3), our rainfall estimate becomes roughly

(3.48)

The length in the numerator is tiny and hard to perceive. Therefore, the common time unit for rainfall is a year rather than a second. To convert the rainfall estimate to meters per year, multiply by

(about 64 inches per year). Not bad: Including all forms of falling water, such as snow, the world average is 0.99 meters per year — slightly higher over the oceans and slightly lower over land (where it is 0.72 meters per year). The moderate discrepancy between our estimate and the actual average arises because some sunlight warms water without evaporating it. To reflect this effect, our table on page 81 needs one more fraction (≈ 2/3).

Problem 3.30 Solar luminosity

Estimate the solar luminosity — the power output of the Sun (say, in watts) — based on the solar flux at the top of the Earth's atmosphere.

Problem 3.31 Total solar power falling on Earth

Estimate the total solar power falling on the Earth's surface. How does it compare to the world energy consumption?

Problem 3.32 Explaining the difference between ocean and land rainfall Why is the average rainfall over land lower than over the ocean?

#### 3.4.5 Residence times

Because of evaporation, the atmosphere contains a lot of water: roughly 1.3×1016 kilograms — as vapor, liquid, and solid. This mass tells us the residence time: how long a water molecule remains in the atmosphere before it falls back to the Earth as precipitation (the overall name for rain, snow, or hail). The estimate will illustrate a new way to use box models.

Here is the box representing the water in the atmosphere (assumed to need only one box). The box is filled by evaporation and emptied by rainfall.

Imagine that the box is a water hose holding a mass 𝑚water. How long does a water molecule take to get from one end of the hose to other? This time is the average time taken by a water molecule from evaporation until its return to the Earth as precipitation. In the box model, the time is the time to completely fill the box. This time constant, denoted 𝜏, is mass of water in the atmosphere

```
𝜏 = rate of inflow or outflow, as a mass per time (3.50)
```

The numerator is 𝑚water. For the denominator, we convert rainfall, which is a speed (for example, in meters per year), to a mass flow rate (mass per time). Let's name the rainfall speed 𝑣rainfall. The corresponding mass flux is, using our results from Section 3.4.2, 𝜌water𝑣rainfall: 

(3.51)

Flux is flow per area, so we multiply mass flux by the Earth's surface area 𝐴Earth to get the mass flow:

```
mass flow = 𝜌water𝑣rainfall 𝐴Earth. (3.52)
```

At this rate, the fill time is

(3.53)

There are two ways to evaluate this time: the direct but less insightful method, and the less direct but more insightful method. Let's first do the direct method, so that we at least have an estimate for 𝜏:

which is roughly 10 days. Therefore, after evaporating, water remains in the atmosphere for roughly 10 days.

For the less direct but more insightful method, notice which quantities are not reasonably sized — that is, not graspable by our minds — namely, 𝑚water and 𝐴Earth. But the combination 𝑚water/𝜌water𝐴Earth is reasonably sized:

(3.55)

This length, 2.5 centimeters, has a physical interpretation. If all water, snow, and vapor fell out of the atmosphere to the surface of the Earth, it would form an additional global ocean 2.5 centimeters deep.

Rainfall takes away 100 centimeters per year. Therefore, draining this ocean, with a 2.5-centimeter depth, requires 2.5×10−2 years or about 10 days. This time is, once again, the residence time of water in the atmosphere.

3.4 黑箱模型与守恒量

不变性背后隐含了一个有力的日常生活的抽象：黑箱模型。我们已经在章节 3.1.1 构造了一个黑箱模型，用以决定在雨中走还是跑。现在我们来进一步考察这个模型。最简单的黑箱包含一定量的物体或许是流体的体积，或者某个大学的学生数（每个学生都会在一个确定的年限之后毕业）。进入黑箱的所有东西都会从黑箱出来。这个结论似乎是简单的，甚至是最简单的，但却具有广泛的应用。通过将这个模型作为不变性原理的例子来研究，可以将模型和一般原理联系起来，从而帮助我们理解原理和模型。

3.4.1 供给与需求

黑箱模型的另一个例子，回想一下我们关于美国进口原油的估算（章节 14）。流进黑箱的 —— 推或者供供给 —— 是进口的原油。流出黑箱的 —— 拉或者需求 —— 是进口原油的使用量。表面上看，问题问的是供给（进口多少原油）。不幸的是，这个估算是困难的。但幸运的是，只要原油不在黑箱中累积（比如，只要原油不存放在地下储存桶中），则供给就等于需求。为了估算供给，我们转而来估算需求。这个想法是基于下面对市场大小的估算。

➤ 波士顿有多少出租车？

有很多年，我在波士顿附近的一个旧街区过着没车的、无忧无虑的生活。我常常坐在出租车里思考出租车市场的大小。出租车的供应量似乎很难估算，因为出租车都散在城市的各个角落，难以计数。但估算出租车的需求量会容易些。

出发点是波士顿大约有 500000 居民。直觉的估算，每个居民大约每个月会坐一次出租车，大约 15 分钟的车程：因为波士顿出租车很贵，除非自己没车，否则很难想象一个人会每月坐几次出租车或超过 15 分钟车程。需求量是大约每月 10 小时的出租车程：

➤ 那么需要多少出租车司机才能支撑这个需求量？

出租车司机工作时间很长，也许每周 60 小时。他们可能有一半的时间是载客的：即每周 30 小时，或大概每月 100 小时。按这样估算，每月 10$^5$ 小时的需求量可以由 1000 个出租车司机提供，或者，假定每辆出租车由一名司机驾驶，则需要 1000 辆出租车。

旅游者的贡献如何估算？

旅游者是非常短期的波士顿居民，大部分都没车。旅游者尽管数量比居民少，但比居民更多乘坐出租车，乘坐的时间也更长。为了将旅游者的贡献计入出租车的需求量，我将简单地将前面的估算加倍，得到 2000 辆出租车的结果。

这个估算可以用可靠的方法来验证，因为波士顿是出租车需要特别许可证（一个特殊的徽章）才可以搭载乘客的城市。发出的徽章数是严格控制的，所以这个徽章是很值钱的。在大约 60 年内，这个数字限制在 1525，直到一次 10 年的法庭辩论将上限增加了 260，总数达到了 1800。

2000 的估算值看起来比预想的要更精确。机会总是青睐有准备的大脑。我们用很好的工具做了准备：黑箱模型和分而治之法。在进行估算时，对工具要有信心，然后期待你的估算值至少能过得去。这样你就有勇气开始：优化对原油及铁路的估算。

题 3.24 RC 电路的微分方程

解释黑箱模型如何导致章节 2.4.4 的低通 RC 电路的微分方程：

（几乎每个微分方程都来自一个黑箱或一个守恒量。）

题 3.25 波士顿出租车树图

画出分而治之法的树图来估算波士顿出租车数量。首先画出没有估算值的。然后将你的估算值计入，并向上传递到树根。

题 3.26 圣诞树上的松针

估算圣诞树上的松针数。

3.4.2 流量

流量，比如说原油的需求量，或者出租车的供应量，都是某种速率 —— 即单位时间的量。物理的流量也是某种速率，但和几何尺度相关。这使得我们可以定义一个相关的、更加不变的量：通量。

```
物质的通量 = 速度/面积 = 物质的重量/面积 x 时间
```

比如，粒子通量是粒子（如分子）以某种速度垂直通过一个截面的流量，再除以截面的面积。除以面积这个做法，在非物理的流量（如出租车的需求量）中没有对应，使通量比流量更为有用。因为如果你将面积加倍，流量也加倍。这样的一种正比关系不仅没有什么价值，通常也不给人更多启发，只是增加了点杂乱。每当发生变化时，我们就应该寻找不变量：即使面积改变，通量也不会改变。

题 3.27 速率与总量

解释为何速率（单位时间内的量）比总量更有用。

题 3.28 什么是电流密度

什么类型的通量（什么量的通量）是电流密度？

通量的定义导致了通量和流体速度之间的一个简单而重要的联系。假设有一管物质（比如分子），其横截面积为 A。物质以速度 v 在管中流动。

➤ 在时间 t 内，有多少物质离开管子？

在时间 t 内，离开管子的物质位于阴影部分，长度为 vt。这一块的体积是 Avt。这部分体积内的物质一共有：

单位体积物质的量，即物质密度，经常出现因而通常需要一个特殊的符号来表示。当这些物质是粒子时，密度通常用 n 标记，表示数密度（与表示粒子数的 N 不同）。如果物质是电荷，密度就用 ρ 标记，表示电荷密度。

由物质的量，我们可得通量：

乘积 At 消去，留下一个一般的关系式：

```
物质通量 = 物质密度 × 流速 (3.40)
```

举一个特殊的例子，当物质是电荷时（题 3.28），通量变成单位时间单位面积的电荷，即单位面积的电流或电流密度。将这些量的标记用于上述通量，一般表达式变成：

```
电流密度 = 电荷密度 × 流速 (3.41)
```

其中 v 是电荷的速度 —— 这也是你在题 6.16 中要估算的电子在导线中的漂移速度。

这个一般关系在估算飞行（章节 3.6）所需要的能量和理解热传导时是至关重要的（章节 7.4.2）。

3.4.3 平均太阳通量

一个重要的通量是能量的通量：能量通过一个截面的速率除以截面的面积。这里，速率表示单位时间的能量或功率。因此，能流就是单位面积的功率。对生命非常重要的是太阳通量：即照射到地球表面单位面积的太阳功率。这个通量决定了我们大部分的气候。在大气层顶端，直接观察太阳的话，通量大约是 F=1300 瓦 / 米^2。

但是，这个通量并不是均匀地分布在整个地球表面的。最简单的原因就是白天和黑夜。地球处于黑夜的一边，太阳的通量是零。更复杂的是，不同的纬度具有不同的通量：赤道区域因为接收到更多的通量而比两极温暖。

➤ 整个地球的平均太阳通量是多少？

我们可以利用黑箱模型（守恒量的讨论）得到平均通量。下面是阳光入射到地球的示意图。（假定是平行光，因为太阳如此遥远。）用一个半径为 R 地球的盘子垂直阳光使其正好遮挡住地球。圆盘吸收的功率可以从能量通量得到：

```
功率 = 能流 x 面积 =  FπR地球（3.42）
```

其中 F 是太阳通量。现在将这个功率平均散布在整个地球表面，其表面积为 4πR^2：

因为地球的一半处于黑夜，对白天和黑夜的平均给出因子 2。因此，对不同纬度的平均一定给出了另一个因子 2（题 3.29）。

题 3.29 太阳通量对所有纬度的平均

考虑到入射光与表面夹角的变化，将通量对地球有阳光的表面进行积分。验证所得结果与黑箱模型结果一致。

这个结果大约是 325 瓦 / 米$2$。相对地球实际接收到的，这个结果稍微过高估算了点，因为并不是在大气层顶端的通量都能到达地球表面。大约 30% 会在大气层顶端被反射（如云）。剩下大约是 1000 瓦 / 米$2$。对地球表面平均，就变成 250 瓦 / 米$2$（这些就进入地面和空气中），或者大约是 F/5，其中 F 是大气层顶端的通量。

3.4.4 雨量

这每平方米 250 瓦的能量决定了对生命活动至关重要的气候特征：表面的平均温度和平均雨量。当你学到了量纲分析这个分析工具之后，你就可以在题 5.43 中估算表面温度。这里，我们将估算平均雨量。

如果这个黑箱代表含有一定量水分的大气 —— 经过足够长的时间后这个含量是常数，则进入黑箱的东西一定全部从黑箱出来。进入的是蒸发量；出来的是雨量。因此，要估算雨量，就要估算蒸发量 —— 这是由太阳通量产生的。

➤ 地球上的雨量有多少？

雨量是用单位时间水的高度来衡量的 —— 典型地，用英寸 / 年或米 / 年。为了估算雨量，要将太阳提供的能量转化为雨量。换言之，将单位面积的功率转化为单位时间的高度。转换的结构是：

(3.44)

其中 ?/? 表示未知的转换因子。为了找到这个转换因子所代表的量，我们两边同乘面积 / 功率。得到结果：

➤ 单位能量的体积可能是什么物理量？

我们在试图确定雨量，所以分子中的体积应该是雨量的体积。水的蒸发需要能量，所以分母中的能量应该是蒸发这些水量所需要的能量。转换因子因而是水蒸发热量 L 蒸发（单位体积所需能量）的倒数。在章节 1.7.3，我们估算了 L 蒸发，但是用单位质量的能量表示的。为了将其变成单位体积的能量，只需乘单位体积的质量这一因子 —— 即，乘以水的密度 ρ：

我们的转换因子，单位能量的体积，就是 1/（ρ水L蒸发）。我们对平均雨量的估算于是就变成：

对分子，我们不能就用 F，即大气层顶端总的太阳通量，而是需要考虑几个无量纲的比例因子，阳光必须克服这些因素才能到达地面并蒸发水量。

这四个因子的乘积大约为 9%。利用 L 蒸发 = 2.2×10$^6$ 焦耳 / 千克（我们在章节 1.7.3 估算的），我们对雨量的估算大约是：

分子中的长度太小了，很难感觉到。因此，通常用的时间单位是年降雨量而不是秒降雨量。为了将雨量的估算转换成米 / 年，乘以因子 1：

在非公制单位中，我们的估算大约是 64 英寸 / 年。包括所有形式的降水，比如下雪，全世界的平均年降水量是每年 0.99 米海上稍微高一点而陆地上稍微少一点（每年 0.72 米）。我们的估算和实际值的差异源于有部分通量只是加热水而并不用来蒸发水，因此在上述表格还应有一个因子，约为 2/3。

题 3.30 太阳光度

估算太阳光度即太阳的输出功率（基于大气层顶端的太阳通量来估算）。

题 3.31 太阳总功率

估算入射到地球的太阳总功率。与全世界的能量消耗相比如何？

题 3.32 解释海面和陆地降雨量的差别

为什么陆地的平均降雨量比海洋上的降雨量少？

3.4.5 滞留时间

由于蒸发，大气中含有很多水分：大约 1.3×10$^6$ 千克 —— 以水蒸气，液体和固体的形式存在。这个质量告诉我们滞留时间：即一个水分子在作为降水（对雨、雪、冰雹的总称）下落到地面之前在大气中停留多少时间。这个估算将会显示使用黑箱模型的新方式。

下面是表示大气水分的黑箱。黑箱被蒸发充满，然后通过降雨变空。

假设黑箱是包含质量 m 水的一段水龙带。水分子从水龙带的一端到另一端需要多长时间？这个时间是水分子从蒸发再通过降雨重新回到地球的平均时间。在这个模型中，这个时间就是将黑箱充满的时间。时间常数用 x 表示，即：

(3.50)

分子就是 m 水。至于分母，我们将雨量（这是一个速度，比如每年多少米）转换为质量流的速率（单位时间的质量）。我们令雨量速度为雨。则利用我们在章节 3.4.2 中的结果，相应的质量通量就是 ρ 水 v 雨：

```
质量通量 = 密度 x 流速 = ρ 水 v 雨 （3.51) 
```

通量是单位面积的流量，因此将质量通量乘以地球表面积 A 地球就得到质量流量：

```
质量流量 = ρ 水 v 雨 A 地球 （3.52） 
```

按这个速率，黑箱充满的时间为：

(3.53)

有两种方式来计算这个时间：较少洞察力的直接计算法；不那么直接但更具有洞察力的方法。我们首先用直接计算法，这样至少我们可以对 x 有个估算。

这大约是 10 天。因此，蒸发后，水在大气中大约会滞留 10 天。

关于不那么直接但更具有洞察力的方法，注意到有些量并不属于合理的尺度即不容易让我们的感觉把握，如水和 A 地球。但组合 m 水 / ρ 水 A 地球是在我们能感知的尺度内：

(3.55)

这个长度，2.5 厘米，可以有一个物理的解释。即如果大气中所有的水，包括雪、水蒸气等都降落到地球表面，则会形成一个 2.5 厘米深的海洋。

降雨每年带走 100 厘米。因此，将 2.5 厘米深的海洋排空，需要 2.5×10$^-2$ 年或大约 10 天。这个时间正是水在大气中的滞留时间。

### 3.5 Drag using conservation of energy

A box model will next help us estimate drag forces. Drag, one of the most difficult subjects in physics, is also one of the most important forces in everyday life. If it weren't for drag, bicycling, flying, and driving would be a breeze. Because of drag, locomotion requires energy. Rigorously calculating a drag force requires solving the Navier–Stokes equations: (𝐯⋅∇)𝐯 + ∂𝐯

∂𝑡 = −1𝜌∇𝑝 + 𝜈∇2𝐯.

(3.56)

They are coupled, nonlinear, partial-differential equations. You could read many volumes describing the mathematics to solve these equations. Even then, solutions are known only in a few circumstances — for example, a sphere moving slowly in a viscous fluid or moving at any speed in a nonviscous fluid. However, a nonviscous fluid — what Feynman [14, Section II-40-2], quoting John von Neumann, rightly disparages as「dry water」 — is particularly irrelevant to real life because viscosity is the cause of drag, so a zero-viscosity solution predicts zero drag! Using a box model and conservation of energy is a simple and insightful alternative.

3.5.1 Box model for drag

We will first estimate the energy lost to drag as an ob-Acs

v

ject moves through a fluid, as in Section 3.2.1. From the energy, we will find the drag force. To quantify the the d

problem, imagine pushing an object of cross-sectional area 𝐴cs at speed 𝑣 for a distance 𝑑. The object sweeps out a tube of fluid.

(The tube length 𝑑 is arbitrary, but it will cancel out of the force.) How much energy is consumed by drag?

Energy is consumed because the object gives kinetic energy to the fluid (say, water or air); viscosity, as we will model in Section 6.4.4, then turns this energy into heat. The kinetic energy depends on the mass of the fluid and on the speed it is given. The mass of fluid in the tube is 𝜌𝐴cs𝑑, where 𝜌 is the fluid density. The speed imparted to the fluid is roughly the speed of the object, which is 𝑣. Therefore, the kinetic energy given to the fluid is roughly 𝜌𝐴cs𝑣2𝑑:

𝐸kinetic ∼ 𝜌𝐴cs𝑑

⏟ × 𝑣2 = 𝜌𝐴cs𝑣2𝑑.

(3.57)

mass

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 85

This calculation ignores the factor of one-half in the definition of kinetic energy. However, the other approximations, such as assuming that only the swept-out fluid is affected or that all the swept-out fluid gets speed 𝑣, are at least as inaccurate. For this rough calculation, there is little point in including the factor of one-half.

This kinetic energy is roughly the energy converted into heat. Therefore, the energy lost to drag is roughly 𝜌𝐴cs𝑣2𝑑. The drag force is then given by energy lost to drag

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ = drag force

⏟⏟⏟⏟⏟ × distance

⏟⏟⏟⏟⏟ .

(3.58)

∼𝜌𝐴cs𝑣2𝑑

𝐹drag

𝑑

Now we can solve for the drag force:

𝐹drag ∼ 𝜌𝐴cs𝑣2.

(3.59)

As expected, the arbitrary distance 𝑑 has canceled out.

3.5.2 Testing the analysis with a home experiment To test this analysis, try the following home experiment. Photocopy or print this page at 200 percent enlargement (a factor of 2 larger in width and height), cut out the template, and tape the two straight edges together to make a cone:

⟶

(3.60)

3.5 cm

We could use many other shapes. However, a cone is easy to construct, and also falls without swishing back and forth (as a sheet of paper would) or flipping over (as long as you drop it point down).

We'll test the analysis by predicting the cone's terminal speed: that is, its steady speed while falling. When the cone is falling at this constant speed, its acceleration is zero, so the net force on it is, by Newton's second law, also zero. Thus, the drag force 𝐹drag equals the cone's weight 𝑚𝑔

(where 𝑚 is the cone's mass and 𝑔 is the gravitational acceleration): 𝜌air𝑣2𝐴cs ∼ 𝑚𝑔.

(3.61)

The terminal speed thus reveals the drag force. (Even though the drag force equals the weight, the left side is only an approximation to the drag force, so we connect the left and right sides with a single approximation sign ∼.) The terminal speed 𝑣term is then

𝑣term ∼

𝑚𝑔

𝐴

.

(3.62)

cs𝜌air

The mass of the cone is

𝑚 = 𝐴paper × areal density of paper.

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

(3.63)

𝜎paper

Here, 𝐴paper is the area of the cone template; and the areal density 𝜎paper, named in analogy to the regular (volume) density, is the mass per area of paper. Although areal density seems like a strange quantity to define, it is used worldwide to describe the「weight」of different papers.

The quotient 𝑚/𝐴cs contains the ratio 𝐴paper/𝐴cs. Rather than estimating both areas and finding their ratio, let's estimate the ratio directly.

How does the cross-sectional area 𝐴 cs compare to the area of the paper?

Because the cone's circumference is three-quarters of the circum-r

ference of the full circle, its cross-sectional radius is three-quar-co

ters of the radius 𝑟 of the template circle. Therefore, ne circumference

2

𝐴cs = 𝜋 (34𝑟) .

(3.64)

Because the template is three-quarters of a full circle, 𝐴paper = 34𝜋𝑟2.

(3.65)

The paper area has one factor of three-quarters, whereas the cross-sectional area has two factors of three-quarters, so 𝐴paper/𝐴cs = 4/3. Now 𝑣term simplifies as follows:

The only unfamiliar number is the areal density 𝜎paper, the mass per area of paper. Fortunately, areal density is used commercially, so most reams of printer paper state their areal density: typically, 80 grams per square meter.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 87

Is this 𝜎 paper consistent with the estimates for a dollar bill in Section 1.1?

There we estimated that the thickness 𝑡 of a dollar bill, or of paper in general, is approximately 0.01 centimeters. The regular (volume) density 𝜌 would then be 0.8 grams per cubic centimeter:

𝜎

g

𝜌

paper

paper =

𝑡 ≈ 80 g m−2 × 1 m2 = 0.8

10−2 cm 104 cm2

cm3 .

(3.67)

This density, slightly below the density of water, is a good guess for the density of paper, which originates as wood (which barely floats on water).

Therefore, our estimate in Section 1.1 is consistent with the proposed areal density of 80 grams per square meter.

After putting in the constants, the cone's terminal speed is predicted to be roughly 0.9 meters per second:

To test the prediction and, with it, the analysis justifying it, I held the cone slightly above my head, from about 2 meters high. After I let the cone go, it fell for almost exactly 2 seconds before it hit the ground — for a speed of roughly 1 meter per second, very close to the prediction. Box models and conservation triumph again!

3.5.3 Cycling

In introducing the analysis of drag, I said that drag is one of the most important physical effects in everyday life. Our analysis of drag will now help us understand the physics of a fantastically efficient form of locomotion — cycling (for its efficiency, see Problem 3.34).

What is the world-record cycling speed?

The first task is to define the kind of world record. Let's analyze cycling on level ground using a regular bicycle, even though faster speeds are possible riding downhill or on special bicycles. In bicycling, energy goes into rolling resistance, friction in the chain and gears, and air drag. The importance of drag rises rapidly with speed, due to the factor of 𝑣2 in the drag force, so at high-enough speeds drag is the dominant consumer of energy.

Therefore, let's simplify the analysis by assuming that drag is the only consumer of energy. At the maximum cycling speed, the power consumed by drag equals the maximum power that the rider can supply. The problem therefore divides into two estimates: the power consumed by drag (𝑃drag) and the power that an athlete can supply (𝑃athlete).

Power is force times velocity:

energy

power = time = force×distance

time

= force × velocity.

(3.69)

Therefore,

𝑃drag = 𝐹drag𝑣max ∼ 𝜌𝑣3𝐴cs.

(3.70)

Setting 𝑃drag = 𝑃athlete allows us to solve for the maximum speed: 1/3

𝑣max ∼ ( 𝑃athlete

𝜌

) ,

(3.71)

air 𝐴cs

where 𝐴cs is the cyclist's cross-sectional area. In Section 1.7.2, we estimated 𝑃athlete as 300 watts. To estimate the cross-sectional area, divide it into a width and a height. The width is a body width — say, 0.4 meters. A racing cyclist crouches, so the height is roughly 1 meter rather than a full 2 meters.

Then 𝐴cs is roughly 0.4 square meters.

Plugging in the numbers gives

1/3

𝑣max ∼ (

300 W

.

(3.72)

1 kg m−3 × 0.4 m2 )

That formula, with its mix of watts, meters, and seconds, looks suspicious. Are the units correct?

Let's translate a watt stepwise into meters, kilograms, and seconds, using the definitions of a watt, joule, and newton: kg m

W ≡ Js,

J ≡ N m,

N ≡ s2 .

(3.73)

The three definitions are represented in the next divide-and-conquer tree, one definition at each nonleaf node. Propagating the leaves toward the root gives us the following expression for the watt in terms of meters, kilograms, and seconds (the fundamental units in the SI system): kg m2

W ≡ s3 .

(3.74)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 89

The units in 𝑣max become

The kilograms cancel, as do the square meters. The cube root then contains only meters cubed over seconds cubed; therefore, the units for 𝑣max are meters per N

m

second.

kg m s−2

Let's estimate how many meters per second. Don't let the cube root frighten you into using a calculator. We kg

m

s−2

can do the arithmetic mentally, if we massage (adjust) the numbers slightly. If only the power were 400 watts (or instead the area were 0.3 square meters)! Instead of wishing, make it so — and don't worry about the loss of accuracy: Because we have neglected the drag coefficient, our speed will be approximate anyway. Then the cube root becomes an easy calculation:

300 400 W

1/3

𝑣

⎞

max ∼ ⎛

⎜

⎟ = (1000)1/3 m s−1 = 10 m s−1.

(3.76)

⎝1 kg m−3 × 0.4 m2 ⎠

In more familiar units, the record speed is 22 miles per hour or 36 kilometers per hour. As a comparison, the world 1-hour record — cycling as far as possible in 1 hour — is 49.7 kilometers or 30.9 miles, set in 2005 by Ondřej Sosenka. Our prediction, based on the conservation analysis of drag, is roughly 70 percent of the actual value.

How can such an estimate be considered useful?

High accuracy often requires analyzing and tracking many physical effects.

The calculations and bookkeeping can easily obscure the most important effect and its core idea, costing us insight and understanding. Therefore, almost everywhere in this book, the goal is an estimate within a factor of 2

or 3. That level of agreement is usually enough to convince us that our model contains the situation's essential features.

Here, our predicted speed is only 30 percent lower than the actual value, so our model of the energy cost of cycling must be broadly correct. Its main error arises from the factor of one-half that we ignored when estimating the drag force — as you can check by doing Problem 3.33.

3.5.4 Fuel efficiency of automobiles

Bicycles, in many places, are overshadowed by cars. From the analysis of drag, we can estimate the fuel consumption of a car (at highway speeds).

Most of the world measures fuel consumption in liters of fuel per 100 kilometers of driving. The United States uses the reciprocal quantity, fuel efficiency — distance per volume of fuel — measured in miles per US gallon. To develop unit flexibility, we'll do the calculation using both systems.

For a bicycle, we compared powers: the power consumed by drag with the power supplied by an athlete. For a car, we are interested in the fuel consumption, which is related to the energy contained in the fuel. Therefore, we need to compare energies. For cars traveling at highway speeds, most of the energy is consumed fighting drag. Therefore, the energy consumed by drag equals the energy supplied by the fuel.

Driving a distance 𝑑, which will be 100 kilometers, consumes an energy 𝐸drag ∼ 𝜌air𝑣2𝐴cs 𝑑.

(3.77)

The fuel provides an energy

𝐸fuel ∼ energy density

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × fuel mass

⏟⏟⏟⏟⏟ = ℰfuel 𝜌fuel𝑉fuel.

(3.78)

ℰfuel

𝜌fuel 𝑉fuel

Because 𝐸fuel ∼ 𝐸drag, the volume of fuel required is given by 𝐸

𝑉

drag

𝑣2𝐴cs

fuel ∼ 𝜌

∼ 𝜌air

𝑑.

(3.79)

fuelℰfuel

𝜌fuel ℰfuel

⏟⏟⏟⏟⏟⏟⏟

𝐴consumption

Because the left-hand side, 𝑉fuel, is a volume, the complicated factor in front of the travel distance 𝑑 must be an area. Let's make an abstraction by naming this area. Because it is proportional to fuel consumption, a self-documenting name is 𝐴consumption. Now let's estimate the quantities in it.

1. Density ratio 𝜌 air/𝜌 fuel. The density of gasoline is similar to the density of water, so the density ratio is roughly 10−3.

2. Speed 𝑣. A highway speed is roughly 100 kilometers per hour (60 miles per hour) or 30 meters per second. (A useful approximation for Americans is that 1 meter per second is roughly 2 miles per hour.) 3. Energy density ℰ fuel. We estimated this quantity Section 2.1 as roughly 10 kilocalories per gram or 40 megajoules per kilogram.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 91

4. Cross-sectional area 𝐴 cs. A car's cross section is about 2 me-car

ters across by 1.5 meters high, so 𝐴cs ∼ 3 square meters.

1.5 m

(cross section)

With these values,

2 m

𝑣2

𝐴cs

⏞⏞⏞⏞⏞

𝐴

103 m2 s−2 × 3 m2

⏞

consumption ∼ 10−3 ×

≈ 8×10−8 m2.

(3.80)

4×107 J kg−1

⏟⏟⏟⏟⏟⏟⏟

ℰfuel

To find the fuel consumption, which is the volume of fuel per 100 kilometers of driving, simply multiply 𝐴consumption by 𝑑 = 100 kilometers or 105 meters, and then convert to liters to get 8 liters per 100 kilometers: 𝑉fuel ≈ 8×10−8 m2

⏟⏟⏟⏟⏟⏟⏟ × 105 m

⏟ × 103 ℓ = 8 ℓ.

(3.81)

1m3

𝐴consumption

𝑑

For the fuel efficiency, we use 𝐴consumption in the form 𝑑 = 𝑉fuel/𝐴consumption to find the distance traveled on 1 gallon of fuel, converting the gallon to cubic meters:

𝑉fuel

1

⏞ g

⏞ allon

⏞⏞⏞

4 ℓ

10−3 m3

𝑑 ∼

×

×

= 5×104 m.

(3.82)

8×10−8 m2

⏟⏟⏟⏟⏟⏟⏟ 1 gallon

1 ℓ

𝐴consumption

The struck-through exponent of 3 in the m3 indicates that the cubic meters became linear meters, as a result of cancellation with the m2 in the 𝐴consumption. The resulting distance is 50 kilometers or 30 miles. The predicted fuel efficiency is thus roughly 30 miles per gallon.

This prediction is very close to the official values. For example, for new mid-size American cars (in 2013), fuel efficiencies of nonelectric vehicles range from 16 to 43 miles per gallon, with a mean and median of 30 miles per gallon (7.8 liters per 100 kilometers).

The fuel-efficiency and fuel-consumption predictions are far more accurate than we deserve, given the many approximations! For example, we ignored all energy losses except for drag. We also used a very rough drag force 𝜌air𝑣2𝐴cs, derived from a reasonable but crude conservation argument. Yet, like Pippi Longstocking, we came out right anyway.

What went right?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

92

3 Symmetry and conservation

The analysis neglects two important factors, so such accuracy is possible only if these factors cancel. The first factor is the dimensionless constant hidden in the single approximation sign of the drag force: 𝐹drag ∼ 𝜌air𝐴cs𝑣2.

(3.83)

Including the dimensionless prefactor (shown in gray), the drag force is 𝐹drag = 12𝑐d 𝜌air𝐴cs𝑣2,

(3.84)

where 𝑐d is the drag coefficient (introduced in Section 3.2.1). The factor of one-half comes from the one-half in the definition of kinetic energy. The drag coefficient is the remaining adjustment, and its origin is the subject of Section 5.3.2. For now, we need to know only that, for a typical car, 𝑐d ≈ 1/2.

Therefore, the dimensionless prefactor hidden in the single approximation sign is approximately 1/4.

Based on this more accurate drag force, will cars use more or less than 8 liters of fuel per 100 kilometers?

Including the 𝑐d/2 reduces the drag force and the fuel consumption by a factor of 4. Therefore, cars would travel 120 miles on 1 gallon of fuel or would consume only 2 liters per 100 kilometers. This more careful prediction is far too optimistic — and far worse than the original, simpler estimate.

What other effect did we neglect?

The engine efficiency — a typical combustion engine, whether gasoline or human, is only about 25 percent efficient: An engine extracts only one-quarter of the combustion energy in the fuel; the remaining three-quarters turns into heat without doing mechanical work. Including this factor increases our estimate of the fuel consumption by a factor of 4.

The engine efficiency and the more accurate drag force together give the following estimate of the fuel consumption, with the new effect in gray: 1

𝑉

2 𝑐d

fuel ≈ 0.25 × 𝜌air𝑣2𝐴cs

𝜌

𝑑.

(3.85)

fuelℰfuel

The 0.25 in the denominator, from the engine efficiency, cancels the 12𝑐d in the numerator. That is why our carefree estimate, which neglected both factors, was so accurate. The moral, which I intend only half jokingly: Neglect many factors, so that the errors can cancel one another out.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum 93

Problem 3.33

Adjusting the cycling record

Our estimate of the world 1-hour record as roughly 35 kilometers (Section 3.5.3) ignored the drag coefficient. For a bicyclist, 𝑐d ≈ 1. Will including the drag coefficient improve or worsen the prediction in comparison with the actual world record (roughly 50 kilometers)? Answer that question before making the new prediction!

What is the revised prediction?

Problem 3.34

Bicyclist fuel efficiency

What is the fuel consumption and efficiency of a bicyclist powered by peanut butter? Express your estimate as an efficiency (miles per gallon of peanut butter) and a consumption (liters of peanut butter per 100 kilometers). How does a bicycle compare with a car?

3.6 Lift using conservation of momentum

If drag is a drag, our next force, which is the companion to drag, should lift our spirits. Using conservation and box models, we will estimate the power required to generate lift. There are two main cases: hovering flight — for example, a hummingbird — and forward flight. Compared to forward flight, hovering flight has one fewer parameter (there is no forward velocity), so let's begin with its analysis, for a bird of mass 𝑚.

3.6.1 Hovering: Hummingbirds

How much power does a hummingbird require to hover?

box

Hovering demands power because a hummingbird has weight: The Earth, via the gravitational field, supplies the hummingbird bird

with downward momentum. The Earth therefore loses downward downward

momentum or, equivalently, acquires upward momentum. (Thus, momentum

the Earth accelerates upward toward the hummingbird, although earth

very, very slowly.) This flow of momentum can be tracked with a box model. Let's draw the box around the Earth–hummingbird system and imagine the system as the whole universe. The box contains a fixed (constant) amount of downward momentum, so the gravitational field can transfer downward momentum only within the box. In particular, the field transfers downward momentum from the Earth to the hummingbird. This picture is a fancy way of saying that the Earth exerts a downward force on the hummingbird, but the fancy way shows us what the hovering hummingbird must do to stay aloft.

box

If the hummingbird keeps this downward momentum, it would accumulate downward speed — and crash to the ground. Fortunately, the air

box has one more constituent: the fluid (air). The hummingbird gives the downward momentum to the air: It flaps its wings and sends air bird

downward. Lift, like drag, requires a fluid. (The air pushes down on the Earth, returning the downward momentum that the Earth lost via the gravitational field. Thus, the Earth does not accelerate.) earth

How much power is required to send air downward?

Power is force times speed. The force is the gravitational force 𝑚𝑔 that the hummingbird is unloading onto the air. Estimating the air's downward speed 𝑣𝑧 requires careful thought about the flow of momentum. The air carries the downward momentum supplied to the hummingbird. The momentum supply (a momentum rate or momentum per time) is area ∼ L2

the force 𝑚𝑔: Force is simply momentum per time. Because mo-vz

mentum flux is momentum per time per area, 𝑚𝑔 = momentum flux × area.

(3.86)

downward

mom. density

When we first studied flux, in Section 3.4.2, we derived that

∼ ρ airvz

flux of stuff = density of stuff × flow speed.

(3.87)

Because our stuff is momentum, this relation takes the particular form momentum flux = momentum density × flow speed.

(3.88)

Substituting this momentum flux into 𝑚𝑔 = momentum flux × area, 𝑚𝑔 = momentum density × flow speed × area.

(3.89)

Momentum density is momentum (𝑚air𝑣𝑧) per volume, so it is 𝜌air𝑣𝑧. The flow speed is 𝑣𝑧. Thus,

𝑚𝑔 = 𝜌air𝑣𝑧 × 𝑣𝑧 × area = 𝜌air𝑣2𝑧 × area.

(3.90)

To complete this equation, so that it gives us the downward velocity 𝑣𝑧, we need to estimate the area. It is the area over which the hummingbird directs air downward. It is roughly 𝐿2, where 𝐿 is the wingspan (wingtip to wingtip). Even though the wings do not fill that entire area, the relevant area is still 𝐿2, because the wings disturb air in a region whose size is comparable to their longest dimension. (For this reason, high-efficiency planes, such as gliders, have very long wings.)

Using 𝐿2 as the estimate for the area, we get 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum 95

𝑚𝑔 ∼ 𝜌air𝑣2𝑧𝐿2,

(3.91)

so the downward velocity is

𝑣𝑧 ∼

𝑚𝑔

𝜌air𝐿2 .

(3.92)

With this downward velocity and with the downward force 𝑚𝑔, the power 𝑃 (not to be confused with momentum!) is

𝑃 = 𝐹𝑣𝑧 ∼ 𝑚𝑔 𝑚𝑔

𝜌air𝐿2 .

(3.93)

Let's estimate this power for an actual hummingbird: the Calliope hummingbird, the smallest bird in North America. Its two relevant characteristics are the following:

wingspan 𝐿 ≈ 11 cm,

(3.94)

mass 𝑚 ≈ 2.5 g.

As the first step in estimating the hovering power, we'll estimate the downward air speed using our formula for 𝑣𝑧. The result is that, to stay aloft, the hummingbird sends air downward at roughly 1.3 meters per second: 𝑚𝑔

⏞⏞⏞⏞⏞⏞⏞

1/2

𝑣

2.5×10−2 N

⎞

𝑧 ∼ ⎛

⎜

⎟ ≈ 1.3 m s−1.

(3.95)

⎝ 1.2 kg m−3

⏟⏟⏟⏟⏟ × 1.2×10−2 m2

⏟⏟⏟⏟⏟⏟⏟⎠

𝜌air

𝐿2

The resulting power consumption is roughly 30 milliwatts: 𝑃 ∼ 2.5

⏟⏟×

⏟ 10−2

⏟⏟ N

⏟⏟ × 1.3 m s−1

⏟⏟⏟⏟⏟ ≈ 3

⏟×10−2

⏟⏟ W

⏟⏟ .

(3.96)

𝑚𝑔

𝑣𝑧

30 mW

(Because animal metabolism, like a car engine, is only about 25 percent efficient, the hummingbird needs to eat food at a rate corresponding to 120

milliwatts.)

This power seems small: Even an (incandescent) flashlight bulb, for example, requires a few watts. However, as a power per mass, it looks more significant:

𝑃𝑚 ∼ 3×10−2W ≈ 10 W

2.5×10−3 kg

kg.

(3.97)

In comparison, the world-champion cyclist Lance Armstrong, with one of the highest human power outputs, was measured to have a power output of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

96

3 Symmetry and conservation

7 watts per kilogram (Section 1.7.2). However, for a chemically unenhanced world-class athlete, 5 watts per kilogram is a more typical value. According to our estimates, hummingbird muscles should be twice as powerful as this world-class human value! Even for a small bird, hovering is hard work.

Problem 3.35

Fueling hovering

How much nectar must a hummingbird drink, as a fraction of its body mass, in order to hover for its working day (roughly 8 hours)? By mass, nectar is roughly 50 percent sugar.

Problem 3.36

Human hovering

How much power would a person have to put out in order to hover by flapping his or her arms?

3.6.2 Lift in forward flight

Now that we understand the fundamental mechanism wing

of lift — discarding downward momentum by giving it to the air — we are ready to study forward flight: the body

L

v

flight of a migrating bird or of a plane. Forward flight is more complicated than hovering because forward wing

flight has two velocities: the plane's forward velocity 𝑣 and the downward component 𝑣𝑧 of the air's velocity after passing around the wing. In forward flight, 𝑣𝑧 depends not only on the plane's weight and wingspan, but also on the plane's forward velocity.

To stay aloft, the plane, like the hummingbird, must deflect air downward.

air

wing

v

(side view)

vz

The wing does this magic using complicated fluid mechanics, but we need not investigate it. All the gymnastics are hidden in the box. We need just the downward velocity 𝑣𝑧 required to keep the plane aloft, and the power required to give the air that much downward velocity. The power is, as with hovering, 𝑚𝑔𝑣𝑧. However, the downward velocity 𝑣𝑧 is not the same as in hovering.

It is determined by a slightly different momentum-flow diagram. It shows the air flow before and after it meets the wing.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum

97

downward

mom. density

∼ ρ airvz

Before the air reaches the wing (the left tube), the air has zero downward momentum. As in the analysis of hovering flight, the Earth supplies downward momentum to the plane, which passes it onto the air. This downward momentum is carried away by the air after the wing (the right tube).

As with any flux, the rate of transfer of downward momentum is flux of downward momentum × area.

(3.98)

As in the analysis of the hummingbird, this rate must be 𝑚𝑔, so that the plane stays aloft. The first factor, the flux of downward momentum, is density of downward momentum × flow speed.

(3.99)

Therefore,

𝑚𝑔 = density of downward momentum × flow speed × area.

(3.100)

As in the analysis of hovering, the density of downward momentum is 𝜌𝑣𝑧.

In contrast to the analysis of hovering, where the stuff (downward momentum) is carried by the air moving downward, here the stuff is carried by air moving to the right. Thus, where the flow speed in hovering was the downward air speed 𝑣𝑧, in forward flight the flow speed is the forward velocity 𝑣.

As in the analysis of hovering, the relevant area is the squared wingspan 𝐿2, because the wings alter the airflow over a distance comparable to their longest dimension, which is their wingspan. You can see this effect in a NASA photograph of an airplane flying through a cloud of smoke. The giant swirl, known as the wake vortex, has a diameter comparable to the plane's wingspan. Large planes can generate vortices that flip over small planes. Thus, when coming in for landing, planes must maintain enough separation to give these vortices time to dissipate.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

98

3 Symmetry and conservation

With these estimates, the equation for 𝑣𝑧 becomes 𝑚𝑔

⏟ ∼

𝜌air𝑣𝑧

⏟

×

𝑣

⏟ × 𝐿2

⏟ .

(3.101)

transfer rate

downward-momentum density

flow speed

area

Now we can solve for the downward air speed: 𝑣𝑧 ∼ 𝑚𝑔

𝜌air𝑣𝐿2 .

(3.102)

Now we can estimate the power required to generate lift in forward flight: 𝑃 = force

⏟ × velocity

⏟⏟⏟⏟⏟ ∼ 𝑚𝑔 × 𝑚𝑔

𝜌

𝑚𝑔

𝑣

air𝑣𝐿2 = (𝑚𝑔)2

𝜌air𝑣𝐿2 .

(3.103)

𝑧

Here is a comparison of hovering and forward flight.

hovering

forward flight

deflection area

𝐿2

𝐿2

downward-momentum density

𝜌air𝑣𝑧

𝜌air𝑣𝑧

flow speed

𝑣𝑧

𝑣

downward-momentum flux

𝜌air𝑣2𝑧

𝜌air𝑣𝑧𝑣

downward-momentum flow 𝑚𝑔

𝜌air𝑣2𝑧𝐿2

𝜌air𝑣𝑧𝑣𝐿2

downward velocity 𝑣𝑧

𝑚𝑔/𝜌air𝐿2

𝑚𝑔/𝜌air𝑣𝐿2

power to generate lift (𝑚𝑔𝑣𝑧)

𝑚𝑔 𝑚𝑔/𝜌air𝐿2

(𝑚𝑔)2/𝜌air𝑣𝐿2

In contrast to hovering, in forward flight the power contains the forward velocity in the denominator — a location that would produce nonsense for hovering, where the forward velocity is zero.

As we did for hovering flight using the Calliope hummingbird, let's apply our knowledge of forward flight to an actual object. The object will be a Boeing 747-400 jumbo jet, and we will estimate the power that it requires in order to take off. A 747 has a wingspan 𝐿 of approximately 60 meters, and a maximum takeoff mass 𝑚 of approximately 4×105 kilograms (400 tons).

We'll estimate the power in two steps: the weight 𝑚𝑔 and then the downward air speed 𝑣𝑧. The weight is the easy step: It is just 4 × 106 newtons.

The downward air speed 𝑣𝑧 is 𝑚𝑔/𝜌air𝑣𝐿2. The only unknown quantity is the takeoff speed 𝑣. You can estimate it by estimating the plane's acceleration 𝑎 while taxiing on the runway and by estimating the duration of the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.7 Summary and further problems 99

acceleration. When I last flew on a 747, I measured the acceleration by suspending my key chain from a string and estimating the angle 𝜃 that it made with vertical (perpendicular to the ground). Then tan 𝜃 = 𝑎/𝑔. For small 𝜃, the relation simplifies to 𝑎/𝑔 ≈ 𝜃. I found 𝜃 ≈ 0.2, so the acceleration was about 0.2𝑔 or 2 meters per second per second. This acceleration lasted for about 40 seconds, giving a takeoff speed of 𝑣 ≈ 80 meters per second (180

miles per hour).

The resulting downward speed 𝑣𝑧 is roughly 12 meters per second: 𝑚𝑔

⏞⏞⏞⏞⏞

𝑣

4×106 N

𝑧 ∼

≈ 12 m s−1.

(3.104)

1.2 kg m−3

⏟⏟⏟⏟⏟ × 80 m s−1

⏟⏟⏟⏟⏟ × 3.6×103 m2

⏟⏟⏟⏟⏟⏟⏟

𝜌air

𝑣

𝐿2

Then the power required to generate lift is roughly 50 megawatts: 𝑃 ∼ 𝑚𝑔𝑣𝑧 ≈ 4×106 N × 12 m s−1 ≈ 5×107 W.

(3.105)

Let's see whether these estimates are reasonable. According to the plane's technical documentation, the 747-400's four engines together can provide roughly 1 meganewton of thrust. This thrust can accelerate the plane, with a mass of 4×105 kilograms, at 2.5 meters per second. This value is in good agreement with my estimate of 2 meters per second, made by suspending a key chain from a string and turning it into a plumb line.

As another check: At takeoff, when 𝑣 is roughly 80 meters per second, the meganewton of thrust corresponds to a power output 𝐹𝑣 of 80 megawatts.

This output is comparable to our estimate of 50 megawatts for the power to lift the plane off the ground. After liftoff, the engines use some of their power to lift the plane and some to accelerate the plane, because the plane still needs to reach its cruising speed of 250 meters per second.

Symmetry and conservation make even fluid dynamics tractable.