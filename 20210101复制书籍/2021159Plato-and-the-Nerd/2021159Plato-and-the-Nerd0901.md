## 0901. Symbiosis

· · · in which I go beyond the countable world of computing and argue that computers are not universal machines and their real power comes from their partnership with humans. I explain the notion of a continuum, a concept that is out of reach for software and rejected by digital physics but seemingly essential for modeling the physical world; I argue that computers are co-evolving symbiotically with humans; and I examine the limitations of the formal models that underlie what computers do, showing that the partnership between humans and computers is much more powerful than either alone.

0901 共生关系

在本章，我会越过可数的计算世界，并论述计算机并非通用机器，以及它们真正的力量来自它们与人类的伙伴关系。我会解释连续统的概念，这是一个在软件中遥不可及且被数字物理学拒绝的概念，但其对于建模物理世界似乎又是必不可少的；我会说明计算机正在与人类一起共同进化；我还会分析作为计算机功能基础的形式化模型的局限性，并阐明人类与计算机之间的伙伴关系比单独的任何一方都要强大。

### 9.1 The Notion of a Continuum

In chapter 8 , I mentioned the continuum hypothesis, an unproven (and in some sense unprovable) assertion that the next larger infinite sets larger than the natural numbers ℕ have the same cardinality (size) as the set ℝ of real numbers. I also mentioned that ℝ has the same size as the set of all decision functions.

The word「continuum」in「continuum hypothesis」is an interesting and deeply philosophical one. What is a continuum? Intuitively, a continuum is a set where one can move「smoothly」from one element in the set to another in the set without having to pass through any values not in the set.

The set of real numbers is a continuum. Suppose I want to move from real number 3 to real number 4. Every number between 3 and 4 is a real number, so as I pass through all those numbers in between, I never leave the set of real numbers.

The set of rational numbers is not a continuum. Consider again moving from 3 to 4. The numbers 3 and 4 are both rational numbers, so they are in the set of rational numbers. But if I try to move smoothly from 3 to 4, I would have to pass through π ≈ 3.14159 · · · . However, π is not a rational number, so to move smoothly from 3 to 4, I have to leave the set of rational numbers. 1 The set of rational numbers is not a continuum. In fact, no countable set is a continuum. Because computers operate entirely within a realm of countable sets, continuums are out of reach for computers.

Now we can get philosophical. Do continuums exist in the physical world? Consider time as a set. Let's just focus on the possible times in one afternoon. Suppose it is now 3 PM, a member of that set. As I move from 3 PM to 4 PM, do I pass through any instants that are not times? I have to assume not. If I further assume that time progresses「smoothly,」then I would have to conclude that time is a continuum. Although most models in physics assume that time is a continuum, some modern physics contests this assumption.

The physicist John Archibald Wheeler, who coined the term「black hole」and was Bekenstein's PhD thesis advisor at Princeton, wrote the following:

Time, among all concepts in the world of physics, puts up the greatest resistance to being dethroned from [the] ideal continuum to the world of the discrete, of information, of bits. (Wheeler, 1986)

Wheeler can't see any way to handle time without continuums. Despite these reservations, Wheeler was a proponent of digital physics, which requires that continuums not exist in the physical world. Wheeler even coined the phrase「it from bit」to capture the essence of digital physics.

Space seems to similarly require a notion of a continuum. If I am standing at point x and I move to point y , do I pass through any points that are not in space? Do I move smoothly? Although my senses seem to indicate that I do, I cannot trust what my senses tell me when I am reasoning about time and space scales smaller than what my senses can perceive. Nevertheless, almost all of physics models space as a continuum. 2

Of course, we can now go down the rabbit hole to debate what「smoothly」means, but I will instead rest on centuries of tradition in science, where time and space are nearly universally modeled as continuums. At a minimum, we have to concede that modeling time and space as continuums has proved to be a useful paradigm indeed. These are just models, of course, so as we faithfully avoid confusing the map and territory, we cannot assert the existence of continuums in the physical world just because they are useful as models. However, the reason that they are useful as models is that these models provide simpler explanations of the physical world than models that reject continuums. Applying the principle of Occam's razor, attributed to William of Ockham (c. 1287–1347), an English Franciscan friar, scholastic philosopher, and theologian, when there are competing hypotheses, other things being equal, we should choose the simpler one.

We might just as well question whether the physical world has any intrinsic notion of integers or, more broadly, countable sets. Suppose I have two apples sitting in front of me. It certainly seems that these apples are distinct, individual, integral objects. From that observation, I can argue that integer arithmetic, like 1 + 1 = 2, is a physical reality. But is it? Some of the apple molecules have actually escaped into the air, so I can smell them. What if I take a knife and peel a bit off one apple? Do I still have two apples? What if a worm has eaten part of one? What if the two apples are touching one another? Where does one end and the other begin? Arguably, the notion that these apples are integers is confusing the map and the territory. To model them using integers is defensible on the grounds of its usefulness. The grocery store may count the apples in my basket to determine how much to charge me. But aren't integers here just a model? The grocery store could equally well charge me by their weight.

Leopold Kronecker, a nineteenth-century German mathematician, vehemently criticized Georg Cantor's work, famously stating,「God made the integers; the rest is the work of man.」If I substitute「nature」for「God,」then I would have to conclude that Kronecker could equally well have gotten it exactly backward! It is just as defensible to say,「Man made the integers; the rest is the work of God.」Software, one of the most remarkable human constructions ever, is all about integers and only about integers, and even then only about a tiny subset of all conceivable operations on integers. It is not unreasonable to expect the natural world to be vastly richer than that.

If we further assume that the statement「time is a continuum」is a Platonic truth about the physical world, then we have to assume that physical systems that deal with continuums exist. I am uncomfortable doing this because once again it risks confusing the map and the territory. The notion of a continuum is a mathematical model not a physical reality. But software systems also operate in the world of models not in the physical world. We know how to make physical machines (computers) that are faithful to the software model. Can we make physical machines that are faithful to models in a continuum? Yes, we can! Mechanical engineers, for example, do it all the time. My dishwasher is a machine that almost certainly is better modeled using continuums than restricting it to computation.

Computers have two key limitations. First, they operate only on digital data, limiting their domain to a countable set. Second, their operations are algorithmic, performed as a sequence of steps, where time is irrelevant. Unless you subscribe to a strong form of digital physics, the physical world has neither of these constraints. The models of resistors and inductors considered in chapter 2 , for example, have neither of these properties, yet these are arguably models of machines.

But all models are wrong, so it could be that the models we use for resistors and inductors are not only wrong in the ways I cited in chapter 2 but also wrong to be operating in a continuum and wrong because they do not describe the behavior algorithmically, as a sequence of steps. The digital physics advocates would have to conclude that these models are wrong in this way. To me, however, an algorithmic model of a resistor or an inductor operating on integers only would be cumbersome, useful only for computer simulation and opaque to people.

The fact that computers do not and cannot deal with continuums in no way proves that there are no machines that can deal with continuums. Moreover, continuums are not the only larger infinite sets bigger than the countable sets. Some sets are vastly larger than continuums, and other sets are vastly larger than those sets. Why would nature limit itself to the smallest of infinite sets? This notion seems so improbable that it requires compelling evidence before accepting it. I've already argued that because of the Shannon channel capacity theorem, we cannot obtain such evidence by empirical measurement. In the next section, I will argue that physical systems, including information-processing systems such as the human brain, are far more likely to be machines that deal with uncountable sets than they are to be computers.

9.1 连续统的概念

在第 8 章，我提到了连续统假设，这是一个未经证明（在某种意义上是不可证明的）的断言，即下一个大于自然数集合 N 的更大无限集合具有与实数集合 R 相同的势（大小）。我还提到，集合 R 的大小与所有决策函数的集合大小相同。

「连续统假设」中的「连续统」一词是一个有趣且具有深刻哲学含义的概念。那什么是连续统呢？直观地说，连续统是一个集合，在这个集合中，一个元素可以「连续地」过渡到该集合中的另一个元素，而不必传递任何集合之外的值。

实数集合是一个连续统。假设我想从实数 3 过渡到实数 4。3 到 4 之间的每个数字都是实数，所以当我经过中间所有这些数字的时候，我从没有离开实数的集合。

有理数集合不是连续统。如果我们再次考虑从 3 过渡到 4 的话，由于数字 3 和 4 都是有理数，所以它们在有理数集合中。但是，如果我试图从 3 连续地过渡到 4，我将不得不经过 π

≈ 3.14159 …。然而，π

不是一个有理数，所以，要想从 3 连续地过渡到 4，我就必须离开有理数集合。由此，有理数集合不是一个连续统。事实上，没有可数集合会是一个连续统。由于计算机完全在可数集合的范围内运行，因此连续统也就超出了计算机的范畴。

现在我们可以从哲学的角度谈谈这个问题。物理世界中存在连续统吗？我们来考虑可能的下午时间的集合。假设现在是下午 3 点，它是这个集合的一个元素。当时间从下午 3 点推移到下午 4 点的时候，我是否经过了任何非集合内元素的瞬间呢？我必须假设不是。如果我进一步假设时间的推移是「连续」的，那么我将不得不得出时间是一个连续统的结论。虽然物理学中的大多数模型都假定时间是一个连续统，但一些现代物理学对这一假设提出了质疑。

物理学家约翰·阿奇博尔德·惠勒是「黑洞」一词的创造者，也是贝肯斯坦在普林斯顿大学的博士论文导师，他写道：

在物理学世界的所有概念中，时间的概念对其自身从理想的连续统落入离散的、信息的、比特的世界产生了最大的阻力。（惠勒，1986）

惠勒不知道在没有连续统的情况下如何处理时间。尽管有这些保留的看法，但是，惠勒也是数字物理学的拥护者。数字物理学要求物理世界中不存在连续统。惠勒甚至创造了「万物源于比特（it from bit）」这个短语来捕捉数字物理学的本质。

空间似乎同样需要是一个连续统的概念。如果我站在 x

点，然后移动到 y

点，我会不会穿过一些不在空间中的点呢？我的移动是不是连续的呢？虽然我的感觉似乎表明是这样的，但当我正在推理的时间和空间的尺度小于我的感觉所能感知到的尺度时，我不能相信我的感觉告诉我的。然而，几乎所有的物理学都将空间建模为一个连续统。当然，我们现在可以深入讨论一下「连续」意味着什么。但是，我将以数百年发展的科学传统为基础，在这些科学传统中，时间和空间几乎普遍地被建模为连续统。至少，我们必须承认，将时间和空间建模为连续统已经被证明确实是一个非常有用的范式。当然，这些只是模型，所以当我们忠实地避免混淆地图和地域时，我们就不能仅仅因为这些连续统是有用的模型，就断言连续统在物理世界中是存在的。然而，它们作为模型之所以有用，是因为与拒绝连续统的模型相比，这些模型为物理世界提供了更简单的解释。运用英国方济各会修士、学者、哲学家和神学家奥卡姆的威廉（1287 —1347）提出的奥卡姆剃刀定律，那么，在出现相互竞争的假说时，在其他条件相同的情况下，我们应该选择更简单的那个。

我们也可能会质疑物理世界内在是否具有整数的概念，或者更广义地说，是可数集合的内在概念。假设我面前有两个苹果。当然，这两个苹果是不同的、独立的、完整的事物。针对这一观察，我可以说整数运算，如 1+1=2，是一个物理现实。但真的是这样吗？实际上，一些苹果分子已经逃逸到空气中，所以我能闻到它们的味道。假如我拿把刀削掉一点儿会怎么样？我还有两个苹果吗？如果被虫子吃掉了一小部分呢？如果这两个苹果碰在一起呢？两个苹果的界限在哪里？可以说，这两个苹果是整数的这一概念混淆了地图和地域的所指。用整数对它们进行建模是站得住脚的，因为它是有用的。杂货店的店员可能会数我篮子里的苹果，进而决定要收我多少钱。但这里的整数不就是一个模型吗？杂货店的店员也可以按苹果的重量向我收费。

19 世纪的德国数学家利奥波德·克罗内克强烈地批评了格奥尔格·康托尔的著作，他的名言是：「上帝创造了整数，其余的都是人类的杰作罢了。」如果我用「自然」代替「上帝」，那么我将不得不得出这样的结论，克罗内克同样可以把它颠倒过来！我们也可以说，「人类创造了整数，其余的都是上帝的杰作罢了」，这句话同样站得住脚。软件是人类有史以来最杰出的构造物之一，软件的一切就是关于整数且只是关于整数的，进而，甚至只是所有可以想到的整数操作的一个微小子集。我们有理由相信，自然世界要比这丰富得多。

如果我们进一步假设「时间是一个连续统」这一陈述是关于物理世界的柏拉图式真理，那么我们必须假定处理连续统的物理系统是存在的。这样做让我感到很不舒服，因为这样做有可能再次混淆地图和地域。连续统的概念是一个数学模型，而不是一个物理现实。但是，软件系统也在模型的世界中运行，而不是在物理世界中。我们知道如何使物理机器（计算机）符合于软件模型。那么，我们能制造出符合于连续统模型的物理机器吗？是的，我们可以做到！例如，机械工程师就一直在这样做。我的洗碗机是一台机器，几乎可以肯定的是，使用连续统对其建模要比将其限定为计算模型更好。

计算机有两个关键的限制。第一，它们只对数字数据进行操作，这会将它们的域限定在一个可数的集合上。第二，它们的操作是算法式的，以一系列步骤的形式执行，且与时间不相关。除非你采用一种强大的数字物理学形式，否则物理世界就没有上面这些约束。例如，第 2 章提到的电阻和电感模型就没有这些特性。然而，它们都可以说是机器的模型。

但是，所有的模型都是错误的，所以，我们使用的电阻与电感模型不仅在第 2 章中我的引用方式上可能是错误的，而且在一个连续统中的操作也可能是错误的。错误的原因在于，这些模型并没有将行为算法式地描述为一系列步骤。数字物理学的倡导者将不得不得出这样的结论 —— 这些模型在这方面是错误的。然而，对我来说，一个只能在整数上运作的电阻或电感的算法式模型一定会很麻烦，它只对计算机模拟有用，且对人不透明。

计算机不会也不可能处理连续统的事实，无法证明没有机器能够处理连续统。此外，连续统并不是唯一比可数集合更大的无限集合。有些集合要比连续统大得多，而另外一些集合又比这些集合大很多。为什么大自然会把自己限制在无限集合中最小的集合上呢？这一观点似乎不太可能，在接受它之前需要有令人信服的证据。我已经论证过，基于香农的信道容量定理，我们不可能通过实证测量来获得这样的证据。在下一节，我将讨论物理系统，包括像人类大脑这样的信息处理系统。相较而言，物理系统更可能是处理不可数集合的机器，而不是计算机。

### 9.2 The Impossible Becomes Possible

Consider a simple balloon. I can think of this balloon as a machine that outputs the circumference of a circle given its diameter. Suppose I inflate the ballon until it reaches a specific diameter d at its widest point. The balloon then exhibits a circumference at a cross-section at that widest point. The「input」to the machine is the diameter d , and the output is the circumference, which by the basic geometry of circles should come out to π × d . If I inflate the machine to a diameter of one foot, it calculates π.

The number π is not representable as a binary number with a finite number of bits. So a digital computer would have to run forever before it could produce as output a binary representation of π. As it happens, the number π is nevertheless「computable,」in that, given any positive integer n , a computer can calculate the n th digit of π. No computer can give us all the digits of π in finite time, but a computer can give us any arbitrary digit of a decimal or binary representation of π.

Equivalently, there is a finite program that, in effect, describes the infinite sequence of digits that constitute π. Because this finite program「describes」π, this infinite sequence is「describable」(by a finite description). However, there are many more real numbers where there is no computer program that can give us any arbitrary digit of the number. Gregory Chaitin, an Argentine-American mathematician who worked at IBM in New York and at the University of Auckland, New Zealand, developed a beautiful example of such a number, one that he called「Omega,」or Ω. Ω is a number between zero and one whose binary representation can be used to solve Turing's halting problem for a particular binary encoding of Turing machines. Specifically, if we know the first N bits of the binary representation of Ω, then we can determine for all valid programs of length up to N bits whether they halt. Because this question is known to be undecidable, no computer program can give us any arbitrary bit of the binary representation of Ω. 3

My balloon machine is not trying to calculate Ω, but it nevertheless does seem to do something no computer can do. Specifically, it outputs, all at once, a representation of π.

I'm sure that you are protesting now. Any reader who has persisted this far in this book is far too smart to be hoodwinked by this slight of hand. This argument has several problems. First, the circumference of the balloon will not be π because the balloon is not a Platonic Ideal. It has imperfections. The rubber is probably not perfectly uniform, so the balloon will not form a perfect circle. Thus, the circumference will be something other than π × d . In fact, if we are lucky, it could be 4 × Ω × d , in which case we have built a machine that calculates Ω.

Nevertheless, I stick to my guns. Yes, the balloon will not form a perfect circle, but it will form some shape. If we assume that this shape has a circumference, then it is likely that circumference will be a noncomputable multiple of the diameter. There are vastly more noncomputable numbers than computable numbers, so it would require digital physics to assume that the actual circumference of the balloon is a computable multiple of the diameter. I don't actually know what function the balloon realizes, but it seems that it most likely realizes a function that no digital computer can realize.

But wait. This argument has still more problems. Suppose that the input to the balloon machine is restricted to a countable set perhaps because we accept digital physics. Then the set of all possible outputs is also countable. We know from the arguments in the previous chapter that a union of two countable sets is still countable. Thus, if the inputs are countable, then the balloon machine is actually working only with countable sets.

Suppose that the balloon is perfect, in that given any input diameter d , its circumference will be exactly π × d . Then I can easily come up with a binary encoding that handles all the inputs and outputs of this machine if d comes from a countable set. For example, suppose that my binary encoding is such that any sequence of bits that begins with zero is interpreted as an integer, where the bits after the first zero directly encode that integer. For example, 00 means zero, 01 means one, 010 means two, 011 means three, and so on. Suppose further that in my binary encoding, any sequence of bits that begins with 1 is interpreted to mean π × n , where n is the binary number following the leading 1. For example, 10 means π × 0 = 0, 11 means π, 110 means 2π, and so on. I now have an encoding that a computer can use to realize the balloon machine.

Computer scientists make a distinction between syntax , the way things are written, and semantics , what things mean. A computer transforms bit patterns, operating only on syntax, and is restricted to a countable set of syntactic objects, bit sequences. However, a human looking at those bit sequences is not restricted to a countable number of interpretations of those objects. To interpret 110 to mean 2π is a human act not something the computer does. A human assigns semantics to the syntax 110. Bit sequences can mean integers, real numbers, text, anything, in fact. We can even encode emotions. I can declare that the bit sequence 01010 means「happy」and write a program that produces「happy」as its output. Does this mean that the computer is happy?

Semantics is an association between a set of syntactic objects, such as bit sequences, and a set of concepts. Numbers are concepts, so one possible semantic interpretation of a sequence of bits is as a binary number. However, many other interpretations are possible. In fact, there is no reason to assume that the number of possible interpretations is countable. What makes computers so effective, so useful to humans, is the many possible interpretations we can assign to bit sequences. The partnership of computers with humans is the real source of their power.

But what if humans are just computers? If we assume a strong form of digital physics, then this must be true, ultimately. Even if we do not assume digital physics, many smart people believe that the human mind is in fact software. Alan Turing was a strong advocate of this point of view. In this case, semantics must somehow be reducible to syntax, and the set of all semantic interpretations must be countable.

This idea brings us back to the question of whether it is possible to realize machines that do more than what Turing defined as「computation.」If it is not possible, then the human brain, a machine, must be performing computation. It must, therefore, be limited to operating within a countable world. But if it is possible, then the world is much richer, and there are no bounds to creativity.

Returning to our balloon machine, suppose that I inflate the balloon to a diameter of d = 1 foot. What is the output circumference from the machine? In fact, what is the input? How do we know it is exactly one foot? If we want numbers, then we have a problem that is potentially of the scale of the LIGO problem. Perhaps we write a proposal for $1.1 billion to the National Science Foundation to fund a research project to make this measurement. Presumably, if we get funded, we could enlist the 1,019 scientists and engineers who worked on the LIGO project to measure the diameter and circumference of the balloon to precisions much less than the diameter of a proton. But this is just representing the information in another form. The information is already represented in a perfectly adequate and much cheaper form in the balloon. But the problem with that form is that we humans don't know what the input is, what the output is, nor what function the machine computes!

It is easy to assign semantics to bit sequences. Suppose I declare that 010101 means「happy」and 111000 means「sunshine.」Suppose further I have a computer running a program that, given 111000 as input, produces 010101 as output. This computer outputs「happy」in response to the input「sunshine.」This is simply true by definition. However, the balloon machine is more problematic. I don't know the input, the output, or the function being computed.

What good is a machine if we can't know the function that it realizes? My claim is that we should not be surprised that we cannot know the function that it realizes. We might assume that to「know」the function means that we can describe that function in some mathematical or natural language. 4 Given any written mathematical or natural language, the vast majority of functions with numerical input and output are not describable in that language. This is because every description in any such language is a sequence of characters from a finite alphabet of characters, so the total number of such descriptions is countable. There are vastly more functions, so there can't possibly be descriptions for all of them in any one language. In fact, any language will only be able to describe a tiny subset of them, a countably infinite subset. Does a function need to be describable to be useful?

A car is a machine whose function is to carry me some distance. I don't need to measure that distance to make use of the machine. In fact, any measurement of the circumference of the balloon is simply putting the output information into another form. What's wrong with the original form given to me by the balloon? If I insist on writing the circumference down as a decimal number on paper, then I have already forced the problem into the realm of digital computers.

Moreover, if I assume that every measurement is noisy, then by Shannon's channel capacity theorem, equation (4) in chapter 7 , the measurement will only reveal a finite number of bits of information, even if the underlying physical system contains more information than that. But I don't need to measure or write down the distance that my car carries me to get value out of it. I don't need to measure or write down the circumference of the balloon to assert that the circumference has been produced by the balloon machine.

A rather simple and much more practical example of a machine that is not implementable in software is a simple inductor, described in chapter 2 . Assume that the input to the machine is the voltage and the output is the current. The relationship between the input and output is given by Faraday's law, equation (256) on page 43 . Under Faraday's law, this inductor implements a function that is not effectively computable and therefore not implementable in software. This is true simply because the input and output both exist in a continuum; even if the input is drawn from a countable set, under Faraday's law, the outputs over time have an uncountable number of values.

To assert that an inductor is not an information-processing machine, we could try to assert that it is invalid to represent information using a voltage or current. Because all computers represent information using voltages and currents, our whole world of information-processing machines would collapse. Or we could assert that a value in a continuum does not represent information because it cannot be encoded with a finite number of bits. As I explained in chapter 7 , it is perfectly valid to interpret a value from a continuum as information.

To assert that an inductor is actually a Turing computation, we would have to reject Faraday's law, start counting electrons, and discretize time. This will not lead to a useful model.

As I pointed out in chapter 2 , an inductor is not actually implementable. But just like my balloon, any physical device that I call an inductor is actually a machine that reacts to input voltage by producing a current. Just because I don't have an exact model for that machine doesn't mean the machine doesn't exist. It is an information-processing machine, I just don't know exactly what function it implements.

Even if I did know the input-output function that my machine implements, and even if I can arbitrarily closely approximate that function with a computer, I still cannot conclude that I've somehow captured all important properties of the machine. The relationships between the inputs and outputs may not be sufficient. I examine this issue next.

9.2 不可能成为可能

现在，来考虑一个非常简单的气球。我可以把这个气球想象成一台机器，它可以输出一个给定直径的周长。假设给气球充气，直到它最宽的点达到一个特定的直径 d

，然后在气球最宽处的横截面上得出一个周长。机器的「输入」是直径 d

，输出是周长。根据圆的基本几何特性，其周长应该等于 π

×d

。如果我将这个机器充气膨胀到 1 英尺的直径，它会计算出 π

的大小。

数字 π

不能用有限比特的二进制数表示。因此，一台数字计算机必须永远运行才能输出 π

的二进制表示。不管怎样，数字 π

仍然是「可计算的」，因为对于任何给定的正整数 n

，计算机可以计算出 π

的第 n

位数字。没有计算机能够在有限的时间内给出 π

的所有数字，但是一台计算机可以给出 π

的十进制或二进制表示的任意数字。

同样，实际上，存在一个可以描述构成 π

的无限数字序列的有限程序。因为这个有限程序「描述」了 π

，所以这个无限序列（通过有限的描述）

是「可描述的」。然而，还有更多的实数是没有计算机程序可以给出其任意数字的。阿根廷裔美国数学家格雷戈里·柴廷曾在纽约的 IBM 公司和新西兰的奥克兰大学工作，他开发了一个关于这个数字的优秀示例，并称其为「Omega」或 Ω。Ω 是一个处于 0 到 1 之间的数字，它的二进制表示可以用于解决图灵机的特定二进制编码的停机问题。具体来说，如果我们知道 Ω 的二进制表示的前 N

位，那么我们可以确定所有长度达到 N

位的有效程序是否会终止。因为这个问题已知是不可判定的，所以没有任何计算机程序可以给出 Ω 的二进制表示的任意比特。

我在前面提到的气球机器并不是想要计算 Ω。但是，无论如何它似乎确实做了计算机不能做的事情。具体来说，它立即输出了 π

的一个表示。

我相信，读者们现在要提出抗议了。那些耐着性子读到这里的读者都非常聪明，肯定不会为我的这些雕虫小技所蒙蔽。这个论点有几个问题。首先，气球的周长不会是 π

，因为气球不是柏拉图式的理想气球。它一定会有瑕疵。例如，制作气球的橡胶可能不是完全均匀的，气球并不会形成一个理想的圆。因此，气球最宽的横截面处的周长肯定不是 π

×d

。事实上，如果我们幸运的话，它可能是 4×Ω×d

，在这种情况下，我们已经建造了一台能够计算 Ω 的机器。

尽管如此，我还是要坚持自己的观点。的确，气球不会形成一个理想的圆，但它会形成某种形状。如果我们假设这个形状有一个周长，那么这个周长很可能是直径的不可计算的倍数。比起可计算数字来说，不可计算的数字要多得多，因此需要数字物理学来假设气球的实际周长是它的直径的可计算倍数。我不知道气球究竟实现了什么函数，但它似乎很可能实现了数字计算机无法实现的函数。

但是，请等一等，这个论点还有更多的问题需要探讨。假设气球机器的输入被限定在一个可数集合内，这么假设也许是因为我们接受了数字物理学，那么所有可能的输出集合也应该是可数的。从前一章的论证中我们知道，两个可数集合的并集仍然是可数的。因此，如果输入是可数的，那么气球机器实际上只能基于可数集合进行工作。

假设气球是理想的，在给定任何直径 d

的时候，它的周长将精确地为 π

×d

。如果 d

属于一个可数集合，那么我可以很容易地想出一个二进制编码来处理这台机器的所有输入和输出。例如，假设我的二进制编码是这样的，以零开头的任何比特序列都被解释为整数，其中第一个零之后的比特直接编码这个整数。例如，00 表示 0，01 表示 1，010 表示 2，011 表示 3，以此类推。进一步假设，在我的二进制编码中，以 1 开头的任何比特序列都被解释为 π

×n

，其中 n

是这个开头的 1 之后的二进制数。例如，10 表示 π

×0=0，11 表示 π

，110 表示 2π

，以此类推。现在，我拥有了一台可以用来实现气球机器编码的计算机。

计算机科学家区分了语法和语义，前者指事物的书写方式，后者指事物的意义。计算机转换比特模式，仅是对语法进行操作，且被限制在语法对象（比特序列）的可数集合中。然而，观察这些比特序列的人并不局限于对这些对象的可数的解释。将 110 解释为 2π

是人的行为，而不是计算机的行为。是人为语法 110 赋予了语义。实际上，比特序列可以表示整数、实数、文本或任何东西。我们甚至可以对情感进行编码。我可以声明，比特序列 01010 表示「快乐」，并编写一个产生并输出「快乐」的程序。但是，这是否就意味着计算机是快乐的呢？

语义是一个语法对象（如比特序列）集合和一个概念集合之间的关联。数字是概念，所以对比特序列的一种可能的语义解释是二进制数。然而，还可能会有许多其他的解释。事实上，并没有充分的理由假设可能的解释的数量是可计数的。使计算机如此有效、对人类如此有用的，是我们可以为比特序列指定许多可能的解释。计算机与人类的伙伴关系才是计算机的真正力量来源。

但是，如果人类就只是计算机呢？如果我们假定一种强大的数字物理学形式，那么人类就是计算机这一论断最终肯定是成立的。即使我们不假设数字物理学的合理性，许多聪明的人也相信人类的大脑实际上就是软件。艾伦·图灵是这一观点的坚定拥护者。在这种情况下，语义必须以某种方式简化为语法，并且所有语义解释的集合必须是可数的集合。

这个想法让我们再次回到之前的一个问题 —— 是否存在机器可以实现比图灵定义的「计算」函数更多的函数呢？如果这是不可能的，那么人类的大脑这台机器就必须执行计算。因此，它必须被限定在一个可数的世界里运行。但如果这是可能的，这个世界就会更加的丰富，而且创造力就会没有限制。

让我们再次回到气球机器。如果我把气球充气到直径 d

=1 英尺，那么这台机器输出的周长是多少？实际上，输入是什么呢？我们怎么知道直径正好是 1 英尺呢？如果我们想要一组数字，那么我们就有一个潜在的激光干涉引力波天文台规模的问题。也许我们会向美国国家科学基金会提交一份 11 亿美元的提案，以资助一个研究项目来进行这项测量。推测起来，如果我们得到了资助，就可以招募 1 019 名从事重力波测量的科学家和工程师来测量气球的直径与周长，其精确度远低于质子的直径。但是，这只是用另外一种形式来表示信息。这些信息已经在气球中以一种完全充分和特别经济的形式被表示出来。但这种形式的问题是，我们人类不知道输入是什么，输出是什么，也不知道这台机器会计算什么函数！

为比特序列指定相应的语义是很容易的，例如我宣布 010101 代表「快乐」，111000 代表「阳光」。我进一步假设，我有一台正在运行程序的计算机，给定输入 111000 时会输出 010101。这台计算机根据输入的「阳光」输出「快乐」。从定义上看，这是完全正确的。然而，气球机器的问题更大，因为我不知道输入、输出或正在计算的函数。

如果我们连一台机器最终能实现什么功能都不知道，那么它还有什么用呢？我的意思是说，我们不应该感到惊讶，因为我们确实不知道它要实现什么样的功能。我们也许可以假定，「知道」这个功能意味着，我们可以用某种数学或自然语言来描述该功能。我们需要考虑，任何书面的数学或自然语言可能都无法描述绝大多数具有数字输入和输出的功能。这是因为任何这样的语言中的每个描述都是由有限的字符组成的一个字符序列，因此这些描述的总数就是可数的。但是，还存在更多的功能，所以不可能用任何一种语言对所有函数进行描述。事实上，任何语言都只能描述它们的一个很小的子集，一个可数的无限子集。那么，一个功能是否需要是可描述的之后才能是有用的呢？

汽车是一种机器，其功能是载我移动一段距离。为了使用这台机器，我并不需要去测量那段距离的长度。事实上，对气球周长的任何测量都只是将输出信息转换成另一种形式而已。这个气球向我们提供的原始形式有什么问题？如果我坚持把周长作为一个十进制数写在纸上，那么我已经把这个问题强行带入数字计算机领域了。

此外，如果假设每个测量都是有噪声的，那么根据香农的信道容量定理 —— 第 7 章的方程（4）—— 可知，即使底层的物理系统包含更多的信息，测量也只会得出有限比特的信息。但是，我并不需要测量或写下我的车载我的距离，以由此获得价值。我也不需要测量或写下气球周长的数值，以断言这个周长是由气球机器产生的。

电感就是一个不能以软件实现的机器的极为简单且更为实际的例子，如第 2 章所述。假设机器的输入是电压，输出是电流。方程（256）所表示的法拉第定律给出了输入和输出之间的关系。按照法拉第定律，这个电感实现了一个不能有效计算的函数，因此无法在软件中被实现。事实确实如此，因为输入和输出都存在于一个连续统中。即使输入来自一个可数集合，根据法拉第定律，随着时间的推移，输出值的数量也会是不可数的。

要想断言电感不是信息处理机，我们可以尝试断言用电压或电流来表示信息是无效的。因为如果所有的计算机都用电压和电流来表达信息，我们整个信息处理机的世界就会崩溃。或者我们也可以断言，连续统中的一个值并不代表信息，因为它不能用有限数量的比特进行编码。正如我在第 7 章中解释过的，把连续统中的值解释为信息是完全有效的。

要断言电感实际上是图灵计算，我们就不得不拒绝法拉第定律，开始对电子计数并离散化时间。这种做法不会产生任何有用的模型。

正如我在第 2 章指出的，电感实际上是不可实现的。但就像我的气球一样，任何我称为电感的物理装置实际上就是一台机器，其以产生电流对输入电压做出反应。不能仅仅因为没有一台机器的精确模型就断言不存在这样的机器。它是一台信息处理机，我只是不能确切地知道它实现了什么功能。

即便我的确知道我的机器在执行输入 — 输出功能，即便我能够用计算机任意地逼近那个功能，我仍然不能得出结论 —— 我已经捕获了这台机器的所有重要属性。输入和输出的关系可能是不充分的。我将在下面的内容中研究这个问题。

### 9.3 Digital Psyche?

What good is a machine if we can't know its output or even the function that it computes? I will now give a real-world example of an extremely useful information-processing machine that has properties not observable from outside the machine and has functions that are probably not describable: the human brain. One of the functions that the brain performs is to create consciousness. I know this for a fact because I have a brain, and what we mean by「consciousness」is exactly what I experience as consciousness. In Searle's words,「the concept that names the phenomenon is itself a constituent of the phenomenon.」

However, the consciousness that my brain produces is not directly observable to anyone but me. It is a property of my brain, like the circumference of the balloon, and any attempt to externally measure it will fail to capture it. Regardless, I know for a fact that it exists, observable or not. I will not accept any argument that it does not exist. Cogito ergo sum ,「I think, therefore I am,」to quote the seventeenth-century French philosopher, mathematician, and scientist René Descartes. To deny that my consciousness exists would be to deny existence. If we deny that properties not externally observable are important, then we would be forced to conclude that consciousness is not an important property of the human brain. I'm not willing to do that.

Consciousness is one of many cognitive functions of the brain, along with understanding, reasoning, learning, sentience, and remembering. Of these functions, reasoning seems closest to computation. The human brain is clearly capable of some modest form of Turing computation. We can, in our heads, perform the same functions as the logic gates discussed in chapter 4 . We have memory, and we are able to follow recipes, step-by-step procedures, emulating a computer executing a program. But we are not actually good at this kind of computation, at least not when we are doing it consciously. A computer performs the logic functions of chapter 4 billions of time per second and stores billions of bytes in memory. We don't even come close.

The human brain does many things that we do not know to be Turing computation. Consider face recognition, something that computers are only now starting to get good at. The fact that computers are starting to excel at face recognition, natural language understanding, and speech recognition leads many engineers and scientists today to conclude that the human brain must be accomplishing these things by doing Turing computation. Is this a leap of faith?

Evidence indicates that the brain includes mechanisms that resemble digital computation. The pioneering work of Warren McCulloch and Walter Pitts in the 1940s showed that neurons operate discretely, with distinct and identifiable firings that have a binary nature. Either a firing occurs or it does not. McCulloch and Pitts argued that the behavior of any network of neurons could be exactly replicated by a very different network. They argued that functions of the neurons could be described in a propositional logic, and therefore any realization of the same logic would perform the same function that the neurons perform. If this is true, then, in theory, it should be possible to convey my consciousness to some physical machine other than my brain. It is debatable, however, that the logic in the neuron firings completely constitutes consciousness. McCulloch and Pitts' model, for example, assumes that the timing of the firings is irrelevant to the function they perform. This notion seems unlikely.

In the 1960s, the philosopher Hilary Putnam developed the idea that different structures could realize the same function, calling the principle「multiple realizability.」Bickle (2016) describes it this way:

In the philosophy of mind, the multiple realizability thesis contends that a single mental kind (property, state, event) can be realized by many distinct physical kinds.

Under this principle, mental states are not so much dependent on the hardware (the brain) in which they occur, in that other realizations of the same states would realize the same function. In other words, mental states are like software. Again, it is a stretch to conclude that these same states can be realized in a computer. This would require either that computers be universal information-processing machines or that the brain be limited to the same class of functions that computers can realize.

It may seem that the thesis of multiple realizability is reinforced by the distinctly digital encoding in DNA. DNA uses a base-four encoding rather than binary, but it is still digital. A DNA molecule consists of a pair of strands of nucleotides, where each nucleotide consists of one of four nucleobases. The digital genetic code is used to synthesize each new human, and that human realizes cognition. Does this mean that cognition is digitally encoded?

Your offspring may have eyes the color of yours, but they have entirely their own mind. As pointed out by George Dyson in Turing's Cathedral ,「the problem of self-reproduction is fundamentally a problem of communication, over a noisy channel, from one generation to the next」(Dyson, 2012, p. 287). Recall Shannon's channel capacity theorem from section 7.4 , equation (4), which states that a noisy channel can only communicate a finite number of bits of information per use of the channel. Given this limitation, there is no point in encoding more than a finite number of bits in the genetic material. The information would not get through the noisy channel anyway. There would be no point in a nondigital DNA.

Only features that can be encoded with a finite number of bits can be passed from generation to generation, according to the channel capacity theorem. If the mind, or features of the mind such as knowledge, wisdom, and our sense of self, cannot be encoded with a finite number of bits, then these features cannot be inherited by our offspring. It certainly appears that DNA does not encode the mind because the mind of your offspring is not your own or even a combination of those of both biological parents. An infant does not emerge with a fully developed mind. The mind emerges later.

If the mind requires mechanisms beyond digital for its operation and character, then the mind cannot be conveyed by any mechanism over a noisy channel. Your mind is entirely your own. Not only can it not be passed on to your offspring, it cannot be passed to anything. It will never reside in other hardware unless we invent a noiseless channel. Biological inheritance cannot provide a noiseless channel because if it did, there would be no mutation, there would be no evolution, there would be no humans, and we would have no minds at all. Genetic inheritance is, of necessity, digital, but minds are formed from more than genetics.

Although DNA is digital and encodes how to construct a brain, a mind does not arise from a brain alone, unless you take an untenably extreme position on the classic nature versus nurture debate. The formation of the mind is heavily influenced by the environment in which it forms, by language, by culture, and by education. Although the brain incorporates some binary operations, like computers, if timing matters, then even the binary reactions are not purely algorithmic, proceeding as a sequence of discrete step-by-step state changes, as in a computer. Finally, we just don't know enough about neurophysiological reactions to conclude that they are all purely binary and algorithmic. Consider the effects of drugs, noise, nutrition, and so on on the mind.

John Daugman, a computer science professor specializing in computer vision and pattern recognition at the University of Cambridge, documents a long history of technological metaphors for the brain dating back to the ancient Greeks:

Theorizing about brain and mind has been especially susceptible to sporadic reformulation in terms of the technological experience of the day. (Daugman, 2001)

He talks about「Freud's hydraulic construction of the unconscious」; clockwork metaphors in Descartes, Hobbes, and many other thinkers; and steam engine metaphors from various writers. The history, he says, is a「stumbling progression toward its inevitable culmination in today's understanding that the brain turns out to be a computer.」

Daugman then critiques researchers who「ask precisely that we not think of computation as just the contemporary metaphor, but instead that we adopt it as the literal description of brain function.」This converts the「enlivening effect of a new metaphor」into「the deadening effect of embracing one too literally or too ideologically or too long.」He concludes,

While the computational metaphor often seems to have the status of an established fact, it should be regarded as a hypothetical, and historical, conjecture about the brain.

…

Today's embrace of the computational metaphor in the cognitive and neural sciences is so widespread and automatic that it begins to appear less like an innovative leap than like a bandwagon phenomenon, of the sort often observed in the sociology and history of science. There is a tendency to rephrase every assertion about mind or brains in computational terms, even if it strains the vocabulary or requires the suspension of disbelief.

David Deutsch, a strong proponent of digital physics, also believes that software, as constructed today, will not achieve cognition, which he calls「artificial general intelligence」(AGI):

[AGI] cannot be programmed by any of the techniques that suffice for writing any other type of program. Nor can it be achieved merely by improving [the] performance [of programs] at tasks that they currently do perform, no matter by how much. (Deutsch, 2012)

Deutsch cites Watson, the IBM computer that defeated former Jeopardy champions Brad Rutter and Ken Jennings in 2011, stating that Watson was not「mimicking human thought processes.」He points out that「no Jeopardy answer will ever be published in a journal of new discoveries,」whereas, in principle, Rutter and Jennings are both capable of coming up with answers that can be so published. Deutsch also reaffirms my observation that cognition involves processes that are not externally observable, stating,「the relevant attributes of an AGI program do not consist only of the relationships between its inputs and outputs.」

But Deutsch is not saying that AGI is unachievable with computation. Rather, he is saying that we don't know how to achieve it using computation. In fact, Deutsch claims to have proved that AGI is, in principle, achievable by Church-Turing computation. His proof relies on the「quantum theory of computation」(more physics that is difficult to understand) to show that everything in the physical world「can, in principle, be emulated in arbitrarily fine detail by some program on a general-purpose computer」(emphasis added).

But if you assert that emulating something in「arbitrarily fine detail」is equivalent to actually achieving that something, then you would have to also assert that no meaningful difference exists between rational numbers and a continuum, despite Cantor's observation that there are vastly more real numbers than rational numbers. Given a randomly chosen real number, the probability that it is a rational number is zero, but you can arbitrarily closely approximate it with a rational number. 5 I believe a continuum is qualitatively different from a countable set. In chapter 10 , I will give simple examples of real systems where emulation in「arbitrarily fine detail」fails completely to capture essential features of the system.

Penrose, in The Emperor's New Mind , goes much further to argue that consciousness cannot be explained by the known laws of physics. Penrose argues that the mind is not algorithmic and must be somehow exploiting hitherto not-understood properties of quantum physics. I am making a less radical argument, in that I argue that the mind is not digital and algorithmic even if it can be fully explained using the known laws of physics.

Alan Turing postulated what is known as the「Turing test」for determining whether a computer program realizes a cognitive function. In this test, a human evaluator would observe natural-language conversations between another human and a computer that is programmed to generate human-like responses. The evaluator would be aware that one of the two partners is a computer but would not know which one. Turing said that if the evaluator cannot reliably tell the computer from the human, then the computer is said to have passed the test.

In chapter 11 , I will examine what passing the test can tell us broadly about the capabilities of computers. For now, it is evident that if consciousness is not externally observable, then the Turing test tells us nothing about whether a computer (or even a human) has consciousness.

The same questions arise with other brain functions, such as love, empathy, and understanding. Searle put forth a famous argument called the「Chinese room argument」: that no machine operating like a computer, following algorithmic step- by-step rules, can understand natural language.

The Chinese room argument goes like this. Assume that you know no Chinese, either written or spoken (I believe this is true of Searle, at least). You are locked in a room with a small window and a rule book. Someone outside the room, who does understand Chinese, hands you a stack of cards with Chinese characters on them. The cards tell a story in Chinese and then ask a question about the story. You pick up the first card and find in your rule book a matching symbol and a rule telling you what to do with the card. For example, you might put the card in a particular place on the table. You also have a supply of cards within the room, and occasionally the rule book will tell you to find a card in that supply and put it into a pile that you will then pass out through the window. You similarly go through all the cards that were given to you until the rule book tells you that you are done. You then pass the pile you constructed out the window.

Searle then asks a simple question: Did you understand the story? It's quite possible that the answer you gave to the question about the story would lead the external observer to conclude that in fact you did understand the story. However, Searle points out that there is no way you could come to that conclusion yourself.

In this scenario, you are acting exactly like a computer. The algorithmic computation that computers (and Turing machines) perform has exactly this nature. If you are the computer, then no matter how good your rule book is, and no matter how convincing your answers are, you have not achieved what we call「understanding.」We can even extend the thought experiment with an unbounded supply of paper with preprinted symbols, giving us a computer with unbounded memory, and the conclusion would not change.

Searle's argument created quite a firestorm of controversy. The community of researchers in artificial intelligence (AI) was not happy. Many counterarguments and counter-counterarguments ensued, some of them really quite entertaining. Google it.

My argument is different, but it leads me to believe that Searle's conclusion is probably right, even if you do not believe his argument. There are so many more functions than computations that it is unlikely any given function found in nature is actually performing Turing computations. There just aren't enough possible computations.

This is not to say that software cannot accomplish a great deal. Some people, such as the American computer scientist and futurist Ray Kurzweil, have predicted a「singularity,」a point at which a runaway effect takes over, where computers surpass the ability of humans to control or understand what they do. Kurzweil may be right. I hope not, but nothing that I say makes this impossible.

But I am saying that achieving human-like intelligence, what I call digital psyche and what Searle calls strong AI , using computers as we know them today is extremely improbable. I believe that we will never consider computers to be siblings, and we will never be able to upload our souls to them even if their capabilities eventually exceed those of the human brain in any or all dimensions. Of course, future forms of software and hardware may have entirely new properties, so I will not make any claims about what they can or cannot accomplish.

9.3 数字灵魂？

如果我们连一台机器的输出或者它要计算的功能都不清楚，那么我们又怎么知道这台机器到底好在哪里呢？现在我要给出一个真实世界里极其有用的信息处理机示例，它具有无法从外部观察到的特性，并且具有可能无法描述的一些功能，它就是人类的大脑。人类大脑的功能之一是产生意识。我很清楚这个事实，因为我也有大脑。我们所指的「意识」恰恰就是我以意识所体验的。用塞尔的话来说，「命名现象的概念本身就是这个现象的组成部分」。

然而，我的大脑所产生的意识，除了我自己，任何人都无法直接观察到。我的意识是我的大脑特有的产物，就如同气球的周长一样。任何想要从外部对它进行测量的努力都是徒劳的。无论我的意识能否被观察到，我都知道它是存在的。我不接受任何置疑它存在的观点。「我思故我在。」这是 17 世纪法国哲学家、数学家和科学家笛卡儿的名言。否认我的意识是存在的就是否认存在本身。如果我们否认外部无法观察到的属性是重要的这一观点，那么我们将被迫得出这样的结论 —— 意识不是大脑的重要属性。我并不乐意这样做。

意识与理解、推理、学习、知觉和记忆一样，是大脑诸多认知功能中的一个。在这些功能中，推理似乎最接近计算。很显然，人脑能够进行某种适度形式的图灵计算。在我们的头脑里，我们可以执行与第 4 章所讨论的逻辑门相同的功能。我们有记忆，并且我们能够按照逐步的方案执行，从而模拟一台执行程序的计算机。但是，我们实际上并不擅长这类计算，至少在我们有意识地这样做的时候并不擅长。一台计算机执行第 4 章提到的逻辑功能的速度是每秒钟 40 亿次，并存储数十亿字节。人类的大脑显然无法与之匹敌。

人类的大脑做了许多我们不知道是图灵计算的事情。以人脸识别为例，这是计算机现在才开始擅长做的事情。计算机在人脸识别、自然语言理解以及语音识别等方面的优势，使得今天的许多工程师和科学家得出这样一个结论：人类的大脑一定是通过执行图灵计算来完成这些工作的。这是一次信念的飞跃吗？

有证据证明，大脑中包含有类似数字计算的一些机制。沃伦·麦卡洛克和沃尔特·皮茨在 20 世纪 40 年代的开创性工作表明，基于具有二元性质的、不同且可识别的激发，神经元离散式地进行活动。这个二元性质在于，要么激发要么不激发。沃伦·麦卡洛克和沃尔特·皮茨认为，任何神经元网络的行为都可以通过完全不同的网络来精确复制。他们还认为，神经元的功能能够用命题逻辑进行描述，因此，同一个逻辑的任何实现都将会执行这些神经元所执行的相同功能。假如果真如此，那么从理论上讲，我的意识就有可能被传递给我的大脑之外的某台物理机器。然而，神经元激发的逻辑是否完全构成了意识，这还是值得商榷的。例如，沃伦·麦卡洛克和沃尔特·皮茨的模型假定这些激发的定时与它们执行的功能无关。这一想法似乎是不太可能的。

20 世纪 60 年代，哲学家希拉里·普特南提出了不同结构可以实现相同功能的观点，并称这一原理为「多重可实现性」。比克尔（2016）是这样进行描述的：

在心灵哲学中，多重可实现性论题认为，一个单一的精神类型（属性、状态、事件）可以由许多不同的物理类型来实现。

根据这一原理，一组精神状态并不那么依赖于它们所赖以发生的硬件（大脑），因为相同状态的其他实现也能实现相同的功能。换句话说，精神状态就类似于软件。同样，可以引申出这样的结论：这些相同的状态可以在计算机中被实现。这就要求计算机要么是通用信息处理机，要么要求大脑被限制在计算机能够实现的同一类功能上。

DNA（脱氧核糖核酸）中独特的数字编码似乎强化了多重可实现性这一论题。DNA 使用了四碱基编码，而不是二进制编码，但它仍然是数字化的。DNA 分子由一对核苷酸链组成，其中的每个核苷酸由四种碱基中的一种组成。数字遗传密码用于合成新的人类个体，并且使人类实现认知。那么，这是否意味着认知是用数字编码的？

你的后代可能和你拥有同样颜色的眼睛，但他们完全有自己的思想。正如乔治·戴森在《图灵的大教堂》一书中指出的那样，「自我复制的问题从根本上说是一个通信的问题，信息在一个有噪声的信道上，从一代到下一代」（戴森，2012:287）。现在我们回顾一下 7.4 节香农的信道容量定理，即方程（4），它指出一个有噪声的信道每次只能传递有限数量的比特信息。考虑这一限制，在遗传物质中编码超过有限数量的比特是没有意义的。原因在于，这些信息无论如何都不会通过有噪声的信道。非数字化的 DNA 没有任何意义。

根据信道容量定理，只有可以用有限数量的比特进行编码的那些特征才能代代相传。如果心智，或者诸如知识、智慧、自我意识之类的心智特征不能用有限的比特数编码，这些特征就不能被我们的后代继承。当然，DNA 不能编码心智，因为你后代的心智不是你的，甚至不是你亲生父母的心智的组合。刚出生的婴儿没有完全的心智，它是后来才慢慢出现的。

如果心智的运作和特性需要超越数字的机制，那么心智就不能通过任何有噪声的信道来传递。你的心智完全是你自己的，它不仅不能传递给你的后代，也不能传递给任何事物。除非我们能发明一个无噪声的信道，否则它将永远不会驻留在其他硬件中。生物遗传还不能提供一个无噪声的信道。因为如果真的能提供，那就不会有变异，不会有进化，不会有人类，我们也就根本没有思想了。基因遗传必然是数字化的，但是，心智的形成不仅仅来自遗传。

尽管 DNA 是数字化的，并对如何构建大脑进行了编码，但心智并不仅仅来自大脑，除非你在经典的先天与后天的辩论中采取了极端的立场。心智的形成很大程度上受到所处环境、语言、文化和教育的影响。尽管大脑包含了一些类似于计算机的二进制操作，但如果时间很重要的话，那么即使是二进制反应也不是纯算法式的，不像计算机那样，以逐步的离散状态变化序列的方式进行。最终，我们不得不说，我们对神经生理反应的了解还不够，还不能断定它们都是纯二进制的和算法式的。因为我们还有许多其他因素需要考虑，例如药物、噪声、营养等因素对心智的影响。

约翰·道格曼，剑桥大学专攻计算机视觉和模式识别的计算机科学教授，他在文中写道对大脑的技术性隐喻可以追溯到古希腊：

从当时的技术经验来看，关于大脑和心智的理论特别容易受到当时零星的重塑的影响。（道格曼，2001）

他谈到了「弗洛伊德关于无意识的液压式构建」，笛卡儿、霍布斯和许多其他思想家的钟表隐喻，以及来自不同作家的蒸汽机隐喻。他说，历史是「在今天理解了大脑原来是一台计算机之后，跌跌撞撞地走向必然的顶点的过程」。

然后，道格曼批评了一些研究人员，他们「明确要求我们不要仅仅将计算当作当代的隐喻，而是应该把它作为对大脑功能的文字性描述」。这一观点实际上将「新隐喻的激活效果」变成了「太字面、太意识形态或太长时间地拥抱一个隐喻所带来的弱化效果」，他得出如下结论：

虽然计算隐喻似乎通常具有一个已确定的事实地位，但它应该被看作关于大脑的一种假设性的、历史性的推测。

……

今天，在认知和神经科学中对计算隐喻的应用是如此广泛和自然，以至它看起来更像社会学和科学史中经常能看到的一种流行现象，而不像是一种创新性的飞跃。现在存在一种倾向 —— 用计算的术语重新表述每一种关于心智或大脑的每一个论断，即使有时候很难找到合适的字眼或者需要暂时放弃我们质疑的态度。

戴维·多伊奇是数字物理学的坚定拥护者，他也认为，今天构建的软件无法实现认知功能，他将其称为「通用人工智能」(AGI)：

通用人工智能尚无法用任何足以编写其他类型程序的技术来编程。也不能仅仅通过提高程序在当前执行的任务上的性能来实现，无论提高多少。（多伊奇，2012）

多伊奇以 IBM 公司的超级计算机沃森为例。沃森在 2011 年击败了美国智力竞赛节目《危险边缘》的前两届冠军布拉德·鲁特和肯·詹宁斯。他认为，沃森并没有「模仿人类的思维过程」。他指出，「任何《危险边缘》的答案都不会发表在发布新发现的杂志上」，而原则上，鲁特和詹宁斯都有能力提出可以被发表的答案。多伊奇重申了我的观察，即认知涉及不能从外部观察到的过程。他认为，「通用人工智能程序的相关属性不只是包含其输入和输出之间的关系」。

但是，多伊奇并不是说用计算就无法实现通用人工智能。相反，他是在说，我们不知道如何用计算来实现它。事实上，多伊奇声称已经证明了通用人工智能在原则上是可以通过丘奇 — 图灵计算来实现的。他的证明依赖于「量子计算理论」（很难理解的物理学理论），表明物理世界中的一切「原则上可以被一台通用计算机上的某个程序以任意精细的细节来模拟」。

但是如果你断言在「任意精细的细节」上模拟某个事物就等同于真正实现了它，那么你还必须断言有理数和连续统之间不存在意义上的任何区别，尽管康托尔观察到的实数比有理数要多得多。给定一个随机选取的实数，它是有理数的概率是零，但你可以用有理数任意地逼近它。我相信连续统与可数集合在性质上是不同的。在第 10 章，我将给出一些实际系统的简单示例，在这些系统中，「任意精细的细节」上的模拟根本无法完全捕捉到系统的本质特性。

在《皇帝新脑》一书中，彭罗斯更进一步论证了意识不能用已知的物理定律来解释。彭罗斯认为，心智不是算法式的，一定是在以某种方式利用量子物理学迄今为止尚不为人所知的特性。我正在提出一个不那么激进的论点，我认为心智不是数字化的和算法式的，即使它完全可以用已知的物理定律来解释。

艾伦·图灵提出了「图灵测试」，以确认一个计算机程序是否实现了认知功能。在这个测试中，人类评估者会观察另一个人和一台编程产生类似人类反应的计算机之间的自然语言对话。评估者会意识到这两个伙伴中的一个是一台计算机，但不知道哪一个是。图灵说，如果评估者不能确定地区分计算机和人，这台计算机就被认为通过了测试。

在第 11 章中，我将研究这个测试大致可以告诉我们关于计算机的什么能力。就目前而言，很明显，如果意识不是外部可观察到的，图灵测试就不能告诉我们计算机（甚至是人类）是否有意识。

同样的问题出现在大脑的其他功能上，例如爱、共情和理解。塞尔提出一个著名的论点，即「中文房间（或华语房间）论点」：没有一台像计算机那样按照算法逐步执行的规则进行操作的机器能够理解自然语言。

中文房间论点是这样的。假设你不懂中文，无论是书面语还是口语（我相信至少塞尔是这样的），你被锁在一间只有一扇小窗户和一本规则手册的房间里。房间外面有个懂中文的人，他递给你一摞上面有中文的卡片。这些卡片用中文讲述了一个故事，然后问一个关于这个故事的问题。你拿起第一张卡片，在你的规则手册中找到一个匹配的符号和一条规则，它们能告诉你如何处理这张卡片。例如，你可以将这张卡片放在桌子的某个特定位置。你的房间里也有一些卡片。规则手册偶尔也会告诉你，在这些卡片中找出一张卡片，然后把它放进你将从窗户递出去的一摞卡片里。同样，你会检查所有递给你的卡片，直到那规则手册告诉你任务已经完成了。然后你把自己的那一摞卡片递给窗外的那个人。

塞尔问了一个简单的问题：房间里的你明白这个故事吗？你对有关这个故事的问题的回答很可能会让外面的观察者得出这样的结论 —— 事实上你确实理解了这个故事。然而，塞尔指出，你自己是不可能得出那个结论的。

在这种情况下，你在房间里的行为完全像是一台计算机。计算机（和图灵机）所执行的算法式计算正是这种性质的。如果你就是这台计算机，那么无论你的规则手册有多好，不管你的答案有多么令人信服，你都没有达到我们所说的「理解」。我们甚至可以将这个思维实验进行拓展，方法是提供无限的带有预先印好符号的纸片，并给我们一台拥有无限内存的计算机，而结论仍然不会发生任何改变。

塞尔的论点引起了相当大的争议。人工智能（AI）领域的研究人员对此感到非常不满。随之而来的是很多抗辩和反抗辩，其中有些观点非常有趣。读者可以去谷歌上查一查。

我的论点有所不同，但它让我相信塞尔的结论可能是正确的，即使你不相信他的论点。功能比计算多得多，所以自然界中任何给定的功能并非都可以真正地执行图灵计算，因为确实没有足够多的可能的计算。

这并不是说软件无法完成大量的任务。有些人，例如美国计算机科学家和未来学家雷·库兹韦尔，已经预言了一个「奇点」，在这个点上，失控效应会占据主导地位。那时，计算机在控制或理解其行为方面将超过人类。库兹韦尔可能是对的。我希望不是，但我所说的一切都不会使这成为不可能。

然而，我要说的是，今天我们所知的计算机不可能实现类人的智能，也就是我所说的数字灵魂和塞尔所说的强人工智能。我相信我们永远不会把计算机当成我们的兄弟姐妹，我们永远无法将我们的灵魂上传到它们那里，即使有一天它们的能力最终能够在任何或所有维度上都超过人类的大脑。当然，未来的软件和硬件形式很可能会有全新的特性，所以我不能对它们能完成什么或不能完成什么做出任何的臆断。

### 9.4 Symbiotic Partnership

The idea of a human-like digital psyche, like digital physics, is a paradigm shift. Perhaps this one too is just waiting for the skeptics, like myself, to die out. Actually, I believe that if anything, it underestimates what we can and will do with computers. Forming them in our own image may have biblical appeal, but it is not likely to take full advantage of their complementary capabilities.

I've already mentioned that Google makes me smarter. So does Wikipedia. Sergey Brin, cofounder of Google, once said,「We want Google to be the third half of your brain」(Saint, 2010). What if what is really happening is a coevolution of man and machine, where each becomes more fit for survival or more likely to procreate because of the other?

Google and Wikipedia both do things that no human can do. They exist as data and software in vast server farms in the cloud, as we saw in chapter 5 . They have features of a life form, including, for example, the immune system in Wikipedia, where, like a lymphocyte, ClueBot NG kills vandalism, as we saw in chapter 1 . Even the Internet can repair itself, with its ability to route around damage. These machines have features of a nervous system, the「dreaming」that is indexing, organizing, and machine learning. Are we playing God, creating a new life form in our own image, or are we being played by a Darwinian evolution of a symbiotic new species? Are humans the purveyors of the「noisy channel」of mutation, facilitating sex between software beings by recombining and mutating programs into new ones, as described in chapter 5 ?

George Dyson, in Turing's Cathedral , raises this question of coevolution. He talks about Google's million-plus servers as a「collective, metazoan organism.」He points out that「the companies and individuals who nurture [these servers] are ever more richly rewarded in return」and「unemployment is pandemic among those not working on behalf of the machines.」However, it is not just the machines enslaving the humans. The humans are evolving too.「Facebook defines who we are, Amazon defines what we want, and Google defines what we think」(Dyson, 2012, pp.308, 325).

There is no question in my mind that humans are coevolving with computers. If computers and software form organisms, then they depend on us for their procreation. We provide the husbandry and serve as midwives. In exchange, we depend on them to manage our systems of finance, commerce, and transportation. More interesting, the machines make the humans more effective at the husbandry that spreads the software species. Elaborate software simulation of semiconductor physics leads to smaller and less power-hungry transistors. Computer-aided design software enables humans to design billion-transistor chips. Compilers translate human-readable code into machine-readable bits. Google makes it easier for humans to fix problems with the machines (just search for the error message), turning us into their own healing agent. And software innovations fuel the startup culture of Silicon Valley, where the software survives and evolves only if the company survives and evolves, and vice versa.

But it's not just humans making machines more effective. The machines are also making the humans more effective and survivable. Cars are learning to refuse to crash. Hearing aids, pacemakers, and insulin pumps compensate for failures in our bodies. Credit card companies' computers block fraudulent transactions, compensating for failures in our society. Data mining is starting to be able to detect the spreading of diseases, such as SARS and the zika virus. And Google makes it easier for your doctor to find cases that manifest the same combination of symptoms in a human pathology, turning computers into agents in our own healing. As Dyson observes,「[t]he Big Computer [is] doing everything in its power to make life as comfortable as possible for its human symbionts」(Dyson, 2012, p. 313)

Dyson goes further, raising a question that we cannot ignore:

Are we using digital computers to sequence, store, and better replicate our own genetic code, thereby optimizing human beings, or are digital computers optimizing our genetic code—and our way of thinking—so that we can better assist in replicating them? (Dyson, 2012, p. 311)

Here Dyson is asking about a purposefulness in computers. However, coevolution does not require teleology in nature, so why should it require it in this case?

Coevolution is happening, where computers and humans are both getting more capable. As with much symbiosis in nature, the partnership can empower both partners, even if the genetic manipulations that Dyson asks about do not occur. Wikipedia still makes me smarter, even if I am stuck with the DNA I was born with.

Doomsayers worry that humans will become unnecessary and the machines will dispose of or enslave us. That does not necessarily happen with symbiosis in nature, so why should it happen here? The fungus in lichen has not killed off the algae, even after millions of years. Instead, stronger connections and interdependencies between man and machine could create a more robust ecosystem, such as the notion of an interconnected「nature」that Andrea Wulf says was invented by Alexander von Humboldt ( chapter 2 ).

Evolution is a natural process. It is pointless to simply fear it, and if we understand what is happening, we can help guide it in desirable directions. Creating human-like digital psyches is, in my view, not a desirable direction. Fortunately, it is probably not even achievable, at least not with today's computer designs. Instead, the real power in the partnership between man and machine comes from their complementarity.

To understand that complementarity, we have to understand the fundamental strengths and limitations of both partners. Software is restricted to a formal, discrete, and algorithmic world. Humans connect to that world through the notion of semantics, where we assign meaning to bits. In the next section, I examine the fundamental limits of the world of software and how a partnership between humans and computers can overcome these limitations.

9.4 共生的伙伴关系

类人的数字灵魂这一想法，如数字物理学，实际上就是一种范式转换。也许，这个想法正等待着像我这样的怀疑论者消失。事实上，我相信它低估了我们可以以及将要用计算机做的事情。按照我们自己的形象塑造它们，可能具有《圣经》般的吸引力，因为上帝是按照他自己的形象塑造人类的。但是，想要充分利用它们的互补能力是不太可能的。

我提到过，谷歌让我更聪明，维基百科也是如此。谷歌的联合创始人谢尔盖·布林说过，「我们希望谷歌能够成为你的大脑的第三个组成部分」（塞因特，2010）。如果真正发生的是人与机器的共同进化，其中每一方都因为另一方的存在而变得更适合生存或更有可能繁衍后代，那该怎么办？

谷歌和维基百科都可以做人类无法做到的事情。正如我们在第 5 章中看到的那样，它们以数据和软件的形式存在于云那庞大的服务器群中。它们具有一种生命形态的特征，就像我们在第 1 章中看到的那样，在维基百科的免疫系统中，虚拟机器人 ClueBot NG 就像淋巴细胞一样能够迅速杀死恶意破坏者。甚至是互联网也有免疫系统，有能力通过路由绕过受损区域。这些机器都具有神经系统的特征，「做梦」就是索引、组织以及机器学习。难道我们是在扮演上帝的角色，按照我们自己的形象去创造一种新的生命体形式？或者，我们是在被达尔文式的共生新物种进化摆布？还是如同第 5 章所述，人类是一个变异的「噪声信道」的提供者，通过将程序重组和变异为新的软件促进软件生命之间的融合与进化？

乔治·戴森在《图灵的大教堂》一书提出共同进化的问题。他把谷歌的上百万台服务器说成是「群体的、多细胞动物的有机体」。他指出，「培育（这些服务器）的公司和个人都得到越来越丰厚的回报」，而「在那些不能利用机器来工作的人群当中，失业的情形是普遍存在的」。然而，不能简单地将这一切看作是机器对人类的奴役。其实人类在这个过程中也在进化。「脸书定义了我们是谁，亚马逊定义了我们想要什么，谷歌定义了我们的想法是什么。」（戴森，2012:308、325）

在我看来，毫无疑问，人类正在与计算机共同进化。如果计算机和软件形成了有机体，那么它们就会依赖于我们来繁衍后代。我们提供照料服务并充当助产士的角色。作为交换，我们依靠它们来管理我们的金融、商业和交通系统。更有趣的是，这些机器使人类在传播软件物种的「畜牧业」方面更加高效。对半导体物理进行详尽的软件模拟可以得到更小、更低功耗的晶体管。计算机辅助设计软件使人类能够设计具有以十亿计晶体管的芯片。编译器将人类可读的代码转换为机器可读的比特。谷歌使人类更容易修复机器出现的问题（只需要搜索错误信息），将我们变成了机器自己的治疗代理。软件创新推动了硅谷的创业文化。在硅谷，软件只有在公司生存和发展的情况下才能不断地生存和发展，反之亦然。

但是，不仅仅是人类使机器的工作更有效率了，这些机器也使人类的生活效率更高，生存能力更强。汽车正在学习避免撞车。助听器、心脏起搏器和胰岛素泵等装置都可以弥补我们身体上的缺陷。信用卡公司的计算机可以阻止欺诈性交易，从而减少或避免社会损失。数据挖掘开始能够检测疾病的传播，比如 SARS（重症急性呼吸综合征）和 ZIKA（寨卡病毒）。谷歌的搜索系统让你的医生更容易找到在人类病理中表现出相同症状组合的病例，将计算机转化为我们自己治疗中的代理。正如戴森观察到的那样，「大型计算机正在尽其所能，使人类共生体的生活尽可能舒适」（戴森，2012:313）。

戴森进一步提出一个我们不能忽视的问题：

我们利用数字计算机来排序、存储和更好地复制我们自己的遗传密码，从而优化人类，或者数字计算机正在优化我们的遗传密码和思维方式，以便我们能够在复制它们的过程中进行更好的协助？（戴森，2012:311）

实际上，戴森在这里问的是有关计算机的目的性的问题。然而，共同进化在本质上并不需要目的论，那么为什么在这种情况下却需要呢？

共同进化正在发生，在这个过程中，计算机和人类都变得越来越有能力。就像自然界中的许多共生关系一样，即便没有出现戴森所要求的基因操控，这种伙伴关系也能使合作方变得更强大。维基百科仍然会让我更聪明，即使我与生俱来的 DNA 并没有发生改变。末日预言者担心人类最终会变得无足轻重，总有一天，机器会取代或奴役我们。这种担心不一定会发生在自然界的共生关系之中，所以为什么要担心它会在人类与计算机的共生关系中发生呢？即使是历经了百万年，地衣中的真菌也没有杀死藻类。相反，人类与机器之间更强的联系和相互依赖可以创造出更强大的生态系统，例如，安德烈娅·武尔夫所说的互联的「大自然」的概念，这个概念是由亚历山大·冯·洪堡发明的（见第 2 章）。

进化是一个自然的过程。盲目地害怕这个过程是没有意义的。如果我们了解正在发生的事情，我们就可以引导它朝着理想的方向发展。在我看来，创造类人数字灵魂并不是一个理想的方向。幸运的是，这可能是无法实现的，至少用今天的计算机设计是不可能实现的。相反，促进人与机器伙伴关系的真正力量来自它们的互补性。

要理解这种互补性，我们就必须了解这两个伙伴的根本优势和局限性是什么。软件被限定在一个形式化的、离散的和算法式的世界里。人类通过语义的概念连接到那个世界。我们给比特赋予含义。在下一节中，我将探究软件世界的基本限制，以及人类与计算机之间的伙伴关系如何才能够克服这些限制。

### 9.5 Incompleteness

Software is limited to a countable, algorithmic world. Humans are not so limited and through the notion of semantics can leverage the countable world of software in an uncountable variety of ways. Limits still exist, however. Scientific thinking strives for rigor, with solid, provable foundations. Mathematics provides the structure for rigorous scientific thinking. However, it turns out that the very quest for rigor results in the same sort of incompleteness that Turing found in computation.

Kurt Gödel published his famous incompleteness theorems in 1931 when he was only 25 years old. His theorems put an end to a decades-long effort known as Hilbert's Program, after the German mathematician David Hilbert. Hilbert's Program, put forth by Hilbert around the turn of the twentieth century, was to put mathematics on a sound foundation as a formal language.

Stephen Hawking, who played a major role in the development of the Bekenstein bound and the digital physics agenda, in a wonderful lecture delivered through a speech synthesizer in 2002 (Hawking, 2002), cites Gödel's theorems. He claims that these theorems do more than just end Hilbert's Program, which pertains to mathematics; they may also end the positivist agenda in science, where every physical theory is a Platonic truth waiting to be discovered. He explains the positivist philosophy as follows:

In the standard positivist approach to the philosophy of science, physical theories live rent free in a Platonic heaven of ideal mathematical models. (Hawking, 2002)

He makes the connection to Gödel as follows:

What is the relation between Gödel's theorem and whether we can formulate the theory of the universe in terms of a finite number of principles? One connection is obvious. According to the positivist philosophy of science, a physical theory is a mathematical model. So if there are mathematical results that cannot be proved, there are physical problems that cannot be predicted.

As we will see, Gödel's theorems tell us that within any (consistent) formal system, some statements cannot be proven true or false. So Hawking is saying that, given some formalism for modeling the physical world, inevitably some statements within that formalism we cannot know to be true or false. Although this could be a huge disappointment to scientists striving for that ultimate goal, the grand unified theory, Hawking draws a more optimistic conclusion:

Some people will be very disappointed if there is not an ultimate theory that can be formulated as a finite number of principles. I used to belong to that camp, but I have changed my mind. I'm now glad that our search for understanding will never come to an end, and that we will always have the challenge of new discovery. Without it, we would stagnate.

With this conclusion, Hawking reaffirms my observation that scientists, like engineers, will never be finished. Although each formalism that we might come up with has its limitations, there is no end to the suite of possible formalisms. There will always be room for invention of new theories.

To understand Gödel's results, we need to first understand what Hawking is referring to as a formulation based on a「finite number of principles.」This depends on the idea of a formal language. Before explaining exactly what a formal language is, let me give a simple example, a language that I call X . As with any written natural language, sentences in a formal language are written down as a sequence of characters from an alphabet. X has a small alphabet, with just one letter, x . So the sentences expressible in this language are any sequence of x s, such as「 xxxx .」We can't say much in language X . If I had written this book in language X , then it would be boring indeed.

A formal language has a set of axioms, which are sentences that are by definition true in the language. X has just one axiom, which asserts that the sentence「 xx 」is true. In a formal language, you cannot argue with the axioms. They are true by definition. So it doesn't really matter whether you believe me when I say「 xx .」When I say「 xx 」in the language X , it is true. Don't argue.

A formal language has a set of inference rules, which can transform one or more true sentences into another true sentence. X has just one inference rule, which is that if some sentence S is true, then the new sentence Sx (just append an x to S ) is also true. For example, if「 xxx 」is true, then so is「 xxxx .」

What are the true sentences in X ? Well, that's an easy question. The true sentences are「 xx ,」「 xxx ,」「 xxxx ' and so on. The only sentence not known to be true is「 x ,」and perhaps the empty sentence, if that is included in the language.

Summarizing what we have so far, a formal language has an alphabet for forming sentences, a (preferably small) set of axioms, and a (preferably small) set of inference rules. That's all. More interesting formal languages will have a bigger alphabet, which might, for example, include the characters + and × to represent addition and multiplication of numbers. The inference rules could include, for example, basic rules of logic, such as,「If you know that at least one of sentences A and B is true, and you know that A is false, then you can conclude that B is true.」Almost all of mathematics is expressible within such formal languages, including mathematics that deals directly with continuums.

A formal language has a notion of a proof . A proof is a sequence of true sentences that demonstrate that a particular end sentence is true. The sequence starts with the axioms, which are assumed to be true, and follows with sentences constructed using the inference rules. The final sentence in the sequence is the sentence proved by the proof. Hilbert's Program sought a formal language that would prove all mathematical truths and have no contradictions (i.e., cannot prove any false sentences).

More precisely, a formal language is complete if every sentence in the language can be proved true or false. The language is consistent if no sentence can be proved both true and false. Hilbert sought a complete and consistent formal language for mathematics.

In X , every sentence with at least two x s has a proof. For example, the proof of the sentence「 xxxx ;' is the sequence of sentences (「 xx 」,「 xxx 」,「 xxxx 」). This is a proof because it starts with an axiom, ends with the sentence being proved, and uses inference rules to get from one sentence to the next. There is no way in X to construct a proof that a sentence with at least two x s is false, so X is consistent. Is it complete?

The sentence「 x 」has no proof, but there is also no proof that it is false. In fact, within the language X , I cannot make the sentence,「The sentence ‘ x ' is false.」The only sentences I can make are rather boring sentences, such as「 xxxxxxxx .」Therefore, this language cannot possibly have a proof that「 x 」is false. Thus, X is not complete unless I extend it with another axiom, that「 x 」is false or true. Within the language X , the sentence「 x 」is neither true nor false. I have to step outside the language X to assign a truth value to「 x .」

What does it mean for a sentence to be「true」if a formal language can have sentences that are neither true nor false? This question has vexed logicians for some time. One possible resolution to this conundrum is to equate the notion of「truth」with the existence of a proof. This is, in fact, a form of logic called「intuitionistic logic,」which ironically is not very intuitive. In intuitionistic logic, a sentence is true only if there is a proof that it is true, and it is false only if there is a proof that it is false. Under this logic, in X , the sentence「 x 」is neither true nor false. Intuitionistic logic rejects the「law of the excluded middle,」an axiom of classical logic that asserts that any sentence must be either true or false. It replaces this law with a constructive principle, which states that truth or falsehood are consequences of constructive demonstrations of that truth or falsehood.

Intuitionistic logic is a rather draconian solution to this problem. A more pragmatic approach is to simply accept that we will sometimes have to rely on certain sensible or self-evident statements as truths even if we have no proof for them. In other words, we may need to assume some elements of the Platonic Good.

Alfred Tarski, a Polish mathematician who later emigrated to the United States, showed in 1936 that no formal language rich enough to possibly satisfy Hilbert's Program could completely define its own notion of truth. In effect, to talk about the「truth」of some sentences in a formal language, you may have to step outside the formal language and use what Tarski called a「metalanguage.」This「undefinability of truth」is credited to Tarski, but really it was already present in Gödel's own results, so it might be more appropriate to credit Gödel for it. Nevertheless, Tarski made it explicit and widely known and understood, as much as such a concept can be understood.

Consider now the following sentence, which I will call「Gödel's sentence」:

「There is no proof for this sentence.」

Suppose this sentence can be made in some formal language (clearly X is not a rich enough language for this). If the sentence is true, then the language cannot be complete because there is at least one sentence, Gödel's sentence, that is true but has no proof. If the sentence is false, then the language cannot be consistent because if the sentence is false, then it has a proof, which means there is a proof for a false sentence. Hence, any formal language that can express Gödel's sentence cannot be both complete and consistent.

Note that I don't have to establish whether Gödel's sentence is true or false. That would require me to use a metalanguage, per Tarski. If the sentence is true, then the language is incomplete. If the sentence is false, then the language is inconsistent. Either way, I've shown that no language that can express Gödel's sentence can satisfy Hilbert's Program.

You've probably already noticed an obvious resolution to the conundrum raised by Gödel's sentence. Let's just avoid any language that can express Gödel's sentence! Are there such languages? Sure. X is such a language. But X can't satisfy Hilbert's Program because it can't express much math. Notice that it can express a little math. For example, I can interpret the sentence「 xxx 」to mean the natural number 3. So I can express all the natural numbers in X (I could interpret the empty sentence, which says nothing, as zero). But the language gives me no way to express, say,「 xxx + xx = xxxxx 」because the symbols + and = are not in the alphabet. The only sentences I can make in X are strings of x s.

Hilbert wouldn't be satisfied with X . Is there some other language that would have made him happy? Gödel, to the great disappointment of many optimistic mathematicians, showed that any formal language that is rich enough to describe addition and multiplication of natural numbers can in fact make Gödel's sentence or a sentence logically equivalent to it. Hence, any formal language that has the potential to address Hilbert's Program is either incomplete or inconsistent. This is Gödel's first theorem. Gödel's second theorem, also published in 1931, showed that no rich enough formal language can prove its own consistency. You have to step outside the language and use a metalanguage to construct any such proof.

Gödel's sentence may seem too clever, too cute, a parlor trick. The essence of Gödel's sentence is its self-reference. The sentence talks about itself, reminiscent of the self-scaffolding of software, human consciousness and self-awareness, and Searle's「the concept that names the phenomenon is itself a constituent of the phenomenon.」It suggests that formalisms capable of self-reference are all problematic. Hawking points out that such self-reference is also intrinsic in science because the humans who are building models of the physical world are part of that same physical world:

[W]e and our models are both part of the universe we are describing. Thus a physical theory is self-referencing, like in Gödel's theorem. One might therefore expect it to be either inconsistent or incomplete. The theories we have so far are both inconsistent and incomplete. (Hawking, 2002)

So this is not a parlor trick. It is quite fundamental.

I won't explain how Gödel proved his theorem, although it's an interesting subject. I've already risked losing too many readers. If you are interested in understanding this more deeply, I recommend Franzén (2005), which is informal and accessible. A more rigorous overview can be found in Raatikainen (2015). A delightful and witty exposition of the topic can be found in Gödel, Escher and Bach: An Eternal Golden Braid by Douglas Hofstadter (Hofstadter, 1979), which won a Pulitzer Prize.

Instead of giving you more detail on Gödel's theorems, I would like to consider their implications for modeling and software. In Gödel's formal languages, the set of all mathematical statements and the set of all proofs are countable sets, just like the set of all computer programs. Moreover, a「proof」in a formal language is a sequence of transformations of sentences, where each transformation is governed by a set of inference rules. This is conceptually close to what a computer does when it executes a program. In a computer, the sentences in the formal language are ultimately just sequences of bits, and the inference rules are the instructions in an instruction set architecture.

Given a finite alphabet, every sentence constructed as sequences of letters from that alphabet can be encoded as a sequence of bits. The original alphabet and sentence become semantic interpretations of the bit sequences. If each inference rule in a formal language is a computable function, then a proof is exactly an execution of a program. It has to terminate to be a proof, and therefore the existence of a proof and the halting problem are closely connected.

This is not just theory. Extremely useful computer programs, called「theorem provers,」take as input an encoding of a sentence in a formal language and attempt to apply the inference rules of the language backward until the program transforms the bit pattern into one or more axioms. If the program succeeds, then the program has constructed a proof. Gödel and Turing both showed, in different ways, that no such program can always succeed.

The formal languages considered by Gödel only permit us to make a countable number of mathematical sentences. Moreover, his incompleteness result only applies to formal languages that are rich enough to describe arithmetic on natural numbers , another countable set. If instead we look at formal languages that describe arithmetic on real numbers, then the theorems do not apply. Tarski showed in 1948 that a natural theory of real numbers that expresses addition and multiplication, the so-called theory of real closed fields (RCFs), is both complete and consistent (and also decidable, an even stronger property which asserts that the truth or falsehood of any statement can be determined by an effectively computable function). He also showed a theory of Euclidean geometry that is complete, consistent, and decidable.

Formal languages that talk about real numbers are better behaved than formal languages that talk about natural numbers. This notion perhaps further supports my suspicion that Kronecker got it backward when he ascribed the integers to God and the rest to man. It also supports my argument that when designing information-processing machines, we should not limit ourselves to software, which is forced to live within the world of natural numbers.

The number of sentences in any particular formal language is countable, but what about the number of possible formal languages? Given any formal language that fails to provide a proof for some proposition that we care about, we can always come up with a different formal language that does provide such a proof or even one that makes that proposition an axiom. Moreover, even if we restrict the alphabet to, say, zeros and ones, the number of possible semantic interpretations for formal languages is certainly not countable. However, like Kuhn's paradigms, distinct formal languages, particularly those with distinct semantics, are incommensurable. The sentences of one formal language cannot be evaluated through the lens of the other. Making comparisons across formal languages requires stepping outside these formal languages into a metalanguage. This is what we do when we assign semantics to a syntax. For example, if I interpret the sentence「 xxx 」in the language X to mean the natural number three, then I have assigned it a semantics. The language X has no notion of「three」and assigns no meaning to「 xxx 」except that it is true.

Turing computation is a formal language. The alphabet for this language has two letters, 0 and 1, and the sentences are sequences of bits. The semantics I assign to these bit sequences, however, is quite arbitrary. As I pointed out in section 9.2 , I could interpret the bit sequence 11 to mean π, although 11 is not a direct binary encoding of the number π. Hence, just as formal languages can talk about irrational numbers, so can computers, given a suitable semantic interpretation to the bit sequences. The partnership of computers with humans enables such semantic interpretation, and because the number of possible semantic interpretations is much larger than the countable number of formal sentences in any formal language, there is plenty of room for creativity.

Mathematical formal languages on real numbers are widely used by scientists and engineers to specify models. These models can be talking about systems whose behaviors involve uncountable sets, although the total number of sentences that can be formed in any formal language is countable. For example, Faraday's law, equation (256), specifies voltages and currents in a continuum, but the law can nevertheless be encoded in a formal language. In fact, we routinely use models that involve uncountable sets whenever we use a continuum in our models, for example, to model time or space. With suitably chosen semantic interpretations, these models can be manipulated by computers. However, the manipulations are meaningless without the semantic interpretation, so the partnership with humans becomes essential.

If the number of possible systems or behaviors in the physical world is uncountable, however, then given any one formal language and any one semantic interpretation, we can expect that most systems are indescribable . There just aren't enough sentences to describe more than a tiny subset. If nature is not constrained to give us only describable systems, then we should assume that with high probability any system found in nature will be indescribable by any particular formal language paired with a semantic interpretation.

Humans are not restricted to working only with one formal language and one semantic interpretation. It is true that given any formal language, such as the accepted language of mathematics based on Zermelo-Fraenkel set theory, we cannot construct more than a countable number of sentences. Yet we can invent new languages. In fact, we do this all the time. Every programming language is a formal language, and we keep coming up with new ones. We are free to assign semantic interpretations to sentences in any formal language. Although a computer produces only zeros and ones, we can interpret a string of zeros and ones to represent a sequence of letters from the alphabet forming sentences in a natural language. This book is produced on a computer, and formally the book is a sequence of zeros and ones, but only a human can give it meaning.

If our goal is engineering rather than science, then we do not need for our new languages to describe some preexisting physical system, such as human cognition. Rather we only need the language to be able to describe something useful or even just something beautiful or interesting. And we need the language to be implementable. We need to be able to find a physical realization that is reasonably faithful to the language. It need not be perfect. No computer is perfect.

Models are similar. They are expressed in a formal language. Speaking as an engineer, I need models to be understandable, and I need to be able to find physical systems that are reasonably faithful to my models. I do not need my models to be true. For example, I know we can make a pretty good balloon machine even if the circumference will never be exactly π × d , and we can make a pretty good inductor even if Faraday's law does not exactly describe its behavior.

Mathematical models are capable of describing behaviors that software cannot handle numerically, but by assigning semantic interpretations to the formal symbols manipulated by a computer, computers can help humans to use such models. Computers can, for example, sometimes prove theorems and symbolically solve mathematical equations involving real numbers. However, software is fundamentally limited to a countable world, and it is limited to processes that are algorithmic, following step-by-step procedures. If the physical world is not so limited, then there are machines that can perform functions that software cannot. I believe it is extremely unlikely that the physical world is so limited; thus, despite the amazing things we can do with software, we can't do everything, and even what we can do with software often requires a partnership with humans to give it any semantic meaning. Computers are not universal machines.

9.5 不完备性

软件被限制在一个可数的、算法式的世界里。但人类并没有那么受限制，并且通过语义的概念可以以不可数的各种方式来利用可数的软件世界。然而，这些限制仍然存在。因为科学思维力求严谨，必须建立在坚实的、可证明的基础之上。数学为严谨的科学思维提供了框架。然而，事实证明，正是对严谨性的追求产生了与图灵在计算中所发现的同样类型的不完备性问题。

1931 年，年仅 25 岁的库尔特·哥德尔发表了他著名的不完备性定理。他的定理结束了以德国数学家戴维·希尔伯特的名字命名的希尔伯特问题长达数十年的努力。希尔伯特问题是希尔伯特在 20 世纪初提出的，旨在把数学作为一种建立在坚实基础之上的正式语言。

斯蒂芬·霍金在贝肯斯坦上限以及数字物理学议题的发展中发挥了主要作用。2002 年，霍金通过一个语音合成器进行了一次精彩的演讲（霍金，2002）。在演讲中，霍金引用了哥德尔定理。他认为，这个定理不仅仅结束了与数学相关的希尔伯特问题，它们也可能会结束科学中的实证主义议题。在该议题中，每一个物理理论都是等待被发现的柏拉图式的真理。他对实证主义哲学做出如下解释：

在科学哲学的标准实证主义方法中，物理理论生活在柏拉图式的理想数学模型的天堂里。（霍金，2002）

他对哥德尔的观点做出如下评论：

哥德尔定理与我们能否用有限数量的原理来表述宇宙理论，这两者的联系是什么？其中的一种联系是显而易见的。根据实证主义科学哲学的观点，一个物理理论就是一个数学模型。因此，如果有一些数学结果是无法被证明的，就意味着有一些物理问题是无法被预测的。

正如我们将要看到的那样，哥德尔定理告诉我们，在任何（相容的）形式系统中，有些命题不能被证明为真或为假。所以霍金说，假定有一些建模物理世界的形式化体系，那么不可避免地，我们无法知道这些形式化体系中的某些说法为真还是为假。这个结论可能会让那些为了大统一理论这个终极目标而奋斗终生的科学家感到非常失望。但是，霍金还是给出如下这个更为乐观的结论：

如果没有一个能够用有限数量原则加以表述的终极理论，那么有些人一定会感到非常失望。我曾经属于那个阵营，但是，我已经改变了主意。我现在很高兴，我们对理解的追求永远不会终结，我们将永远面临新发现所带来的挑战。没有这样的追求和挑战，我们就会停滞不前。

霍金的这个结论，重申了我的观点 —— 科学家和工程师一样，他们的使命永远不会完结。虽然我们可以看出的每一种形式化体系都有其局限性，但是可能的形式化体系是层出不穷、没有尽头的。理论创新的空间永远存在。

要理解哥德尔的结论，我们首先需要理解霍金基于「有限数量原则」的表述是指什么。这依赖于形式语言的概念。在详细解释什么是形式语言之前，我先举一个简单的例子，一种被我称为 X

的语言。就像任何一种书面自然语言一样，形式语言中的句子就是一个字母表中的字符序列。X

语言有一个小的字母表，它只有一个字母 x

。因此，在这种语言中，可以表达的句子是 x

的任意序列，如「xxxx

」。我们不能用 X

语言进行太多的描述。如果我用 X

语言来写这本书，那么这本书的内容一定会无聊透顶。

一种形式语言会有一套公理，公理就是在语言中定义为真的命题。X

只有一个公理，它断言命题「xx

」为真。在一种形式语言中，你不能反对公理。因为从定义上讲，这些公理是真的。所以当我说「xx

」时，你是否相信我其实并不重要。但当我用 X

语言说「xx

」的时候，它就是真的。这一点请不要与我争论。

一种形式语言会有一套推理规则，它们可以将一个或多个为真的句子转换成另一个为真的句子。X

语言只有一个推理规则，即如果某个句子 S

为真，那么新的句子 Sx

（只是给 S

添加一个 x

）也为真。例如，如果「xxx

」为真，那么「xxxx

」也为真。

X

语言中为真的句子是什么？这个问题很简单。这些为真的句子有「xx

」「xxx

」「xxxx

」等等。唯一不知道是真是假的句子是「x

」，而且，如果语言中包含空句子，那么不知道是真是假的还有空句子。

我们来总结一下目前所掌握的内容：一种形式语言有一个组成句子的字母表，一组（最好是较小的）公理，和一组（最好是较小的）推理规则，这就是全部了。更有趣的形式语言将有一个更大的字母表，例如，可能包括表示数字加法和乘法的字符 + 和 ×。推理规则可以包括一些基本的逻辑规则，例如，「如果你知道句子 A

和 B

中至少有一个为真，并且你知道 A

是假的，那么你可以得出 B

为真的结论」。几乎所有的数学都可以用这种形式语言来表达，包括直接处理连续统的数学。

形式语言对证明有明确的概念。证明就是表明一个特定结束句子为真的一个真句序列。这个序列从假设为真的公理开始，然后是使用推理规则构造的句子。序列中的最后一个句子就是为该证明所证明的句子。希尔伯特问题的目的就是找到一种形式语言，它可以证明所有的数学真理且不存在矛盾（即不能证明那些为假的句子）。

更确切地说，如果一种形式语言中的每个命题都能被证明为真或者为假，那么这种语言就是完备的。如果没有一个命题能被证明既真又假，那么这种语言是相容的。希尔伯特恰恰是要寻找一种既完备又相容的数学形式语言。

在 X

语言中，每一个至少有两个 x

的句子都有一个证明。例如，句子「xxxx

」的证明是句子的序列（「xx

」「xxx

」「xxxx

」）。这是一个证明，因为它以一个公理开始，以一个被证明的句子结束，而且使用推理规则从一个句子推出下一个句子。然而，在 X

语言中无法构造出至少有两个 x

的句子为假的这样一个证明，所以 X

是相容的。但它是完备的吗？

句子「x

」没有任何证明，但也没有证据证明它为假。事实上，在 X

语言中，我无法构造出「句子‘x

'为假」这样的句子。我只会构造一些相当无聊的句子，如「xxxxxxx

」。

因此，这种语言不可能具有「x

」为假的证明。由此，X

是不完备的，除非我用另一个公理去扩展它，即「x

」是假或真。在 X

语言中，句子「x

」既非真也非假。我必须跳出 X

语言，给「x

」赋一个真值。

如果一种形式语言可能有一些既非真也非假的句子，那么一个句子为「真」意味着什么？这个问题已经困扰逻辑学家一段时间了。解决这一难题的一个可能途径是将「真理」的概念等同于存在一个证明。事实上，这是一种叫作「直觉逻辑」的逻辑形式。具有讽刺意味的是，这种逻辑形式并不十分符合直觉。在直觉逻辑中，一个句子只有在有证据证明它为真时才为真；只有在有证据证明它为假时才为假。在这种逻辑下，在 X

语言中，「x

」句子既非真又非假。直觉逻辑拒绝「排中律」，这是古典逻辑中的一种公理，它断言任何句子都必须要么为真要么为假。它以一项建设性原则取代了公理，该原则规定，真理或谬误是对那个真理或谬误进行有效证明的结果。

直觉逻辑是解决这一问题的一种相当严苛的方法。其实，我们可以采取一种更实用的方法，那就是简单地接受这样一个事实：我们有时也不得不以某些直觉或不言自明的命题作为真理，即使我们没有证据证明。换句话说，我们可能需要假设一些柏拉图式的善的元素。

后来移居美国的波兰裔数学家阿尔弗雷德·塔尔斯基在 1936 年指出，没有一种形式语言已经丰富到足以满足希尔伯特问题的要求，因为它无法完备地定义自己的真理概念。实际上，要谈论在一种形式语言中某些句子的「真理」，你可能必须先跳出该形式语言，并使用塔尔斯基所说的「元语言」。这种「真理的不确定性」被认为是塔尔斯基最先提出的观点，但实际上这个观点已经出现在哥德尔自己的研究结论中，因此将其归于哥德尔可能更适合。尽管如此，塔尔斯基还是明确了这一概念，并使它获得了更广泛的了解和理解。现在我们来看看下面这句话，我把它称为「哥德尔语句」：

这个句子没有证据证明。

假设这个语句可以用某种形式语言来表达（很显然，X

语言还不是一种足够丰富的语言）。如果这个语句为真，那么这种形式语言不可能是完备的，因为至少有一个语句，即哥德尔语句，为真且又没有证据证明。如果这个语句为假，那么这种形式语言不可能是相容的，因为如果这个语句是假的，那么它会有一个意味着这个语句为假的证明。因此，任何可以表达哥德尔语句的形式语言都不可能既是完备的又是相容的。

请注意，我并不需要确定哥德尔语句为真还是为假。按照塔尔斯基的说法，这需要我使用一种元语言。如果句子为真，那么语言是不完备的。如果句子为假，那么语言是不相容的。无论如何，我已经证明，没有一种可以表达哥德尔语句的语言可以满足希尔伯特问题。

显然，你可能已经注意到了，有一个办法可以解决哥德尔语句所引发的难题，那就是我们要尽量避免使用任何能够表达哥德尔语句的语言！那么，有这样的语言吗？当然有了。X

语言就是这样一种语言。但是 X

语言不能满足希尔伯特问题的要求，原因在于它对数学的表达太有限。请注意，它可以表示一小部分数学关系。例如，我可以把句子「xxx

」解释为自然数 3。所以我可以用 X

语言表示所有的自然数（我可以把这个空句子解释为零，因为其不表达任何意思）。但是这种语言让我无法表达诸如「xxx

+xx

=xxxxx

」这样的句子，因为符号 + 和 = 并不在其字母表中。在 X

语言中，我唯一能构造的句子只有 x

的字符串。

希尔伯特对 X

语言一定不会感到满意。那么还有什么别的语言能让他满意吗？令众多抱有乐观态度的数学家大失所望的是，哥德尔指出，任何足以描述自然数加法和乘法的形式语言，实际上都可以构造哥德尔语句或逻辑上与之等价的句子。因此，任何有潜力能够应对希尔伯特问题的形式语言要么是不完备的，要么是不相容的，这就是哥德尔第一定理。同样发表于 1931 年的哥德尔第二定理表明，没有一种形式语言足以证明它自身的相容性。你必须跳出该语言，并使用元语言来构造任何这样的证明。

哥德尔语句似乎很聪明、很可爱，像是一个小把戏。哥德尔语句的本质在于它的自我参照。这个语句描述了它自己，这使人们一下子想起了软件的自我支撑、人类的意识和自我意识，以及塞尔的「命名现象的概念本身就是这一现象的组成部分」等诸多观点。这表明，能够自我参照的形式化体系都是有问题的。霍金指出，这种自我参照也是科学所固有的，因为构建物理世界模型的人类也是同一个物理世界的一部分：

我们和我们所构建的模型都是我们所描述的宇宙的一部分。因此，物理理论就像哥德尔定理一样是自我参照的。由此，人们可能会认为它要么是不相容的，要么是不完备的。到目前为止，我们所掌握的理论既不相容，也不完备。（霍金，2002）

所以这不是一个小把戏，这是相当基本的。

虽然这是一个有趣的话题，但是我不会解释哥德尔如何证明了他的定理。由于这部分的内容有些过于专业，我已经在冒着失去更多读者的危险了。如果你有兴趣想更深入地理解这一点，我建议你去读一下弗兰森（2005）的书，他的书是非形式化且比较通俗易懂的。关于这个问题更为严谨的阐述，可以参考拉蒂凯宁（2015）的书。道格拉斯·侯世达（侯世达，1979）在《哥德尔 艾舍尔 巴赫 —— 集异璧之大成》一书中对这个话题进行了诙谐有趣的阐述，该书还获得了普利策图书奖。

我不想过多地谈论哥德尔定理的细节，我想谈谈这些定理对建模和软件的影响。在哥德尔的形式语言中，所有数学命题的集合和所有证明的集合都是可数集合，就像所有计算机程序的集合一样。此外，形式语言中的「证明」是一系列句子的转换，其中每个转换都受到一组推理规则的监督。这在概念上很接近计算机在执行程序时所做的事情。在计算机中，形式语言中的句子最终只是比特序列，推理规则就是指令集体系架构中的指令。

给定一个有限的字母表，每个以字母表中的字母序列构成的句子都可以被编码为比特序列。原有的字母和句子就变成了比特序列的语义解释。如果形式语言中每个推理规则都是可计算函数，那么一个证明过程正好是一个程序的一次执行。证明必须结束，因此，证明的存在性问题和停机问题密切相关。

这不仅仅是理论问题。被称为「定理证明器」的非常有用的计算机程序，可以以某种形式语言中一个句子的编码作为输入，并试图反向应用该语言的推理规则，直到程序将比特模式转换为一个或多个公理。如果这个程序成功了，那么该程序构造了一个证明。哥德尔和图灵都曾以不同的方式表明，没有能够永远成功的该类程序。

哥德尔考虑的形式语言只允许我们生成可数数量的数学句子。此外，他的不完备性理论仅适合于那些足以描述自然数（另一个可数集合）运算的形式语言。如果我们看到的是描述实数运算的形式语言，这些定理就不适用了。1948 年，塔尔斯基证明了表示加法和乘法的实数理论，即所谓实闭域理论（RCFs），是完备的和相容的（也是可判定的，具有一种更强的性质，其断言任何命题的真伪都可以由一个可有效计算函数来确定）。他还展示了欧几里得几何的一个完备、相容以及可判定的理论。

描述实数的形式语言比描述自然数的形式语言要表现得更好。这一观点或许进一步支持了我对克罗内克观点的怀疑，他认为上帝创造了整数，其余的东西则是人类自己发明的。我认为他的观点是一种倒退。同样，这也支撑了我的观点，在设计信息处理机时，我们不应该仅局限于软件，因为其只能在自然数的世界中得以存在。

对于任何特定的形式语言，其句子的数量一定是可数的。但可能的形式语言的数量又如何呢？如果任何形式语言都不能为我们所关心的某个命题提供证明，那么我们总是可以找出另一种不同的形式语言来提供这样的证明，甚至可以使这个命题成为公理。此外，即使我们将字母表限制为诸如 0 和 1，对形式语言而言，可能的语义解释的数量也一定是不可数的。然而，就像库恩的范式一样，不同的形式语言，特别是那些具有不同语义的语言之间，是不可通约的。一种形式语言的句子不能从另一种形式语言的视角去评价。跨形式语言的比较需要跳出这些形式语言，并转向使用元语言。这就是我们给一个语法赋予语义时要做的事情。例如，如果我将 X

语言中的句子「xxx

」解释为自然数 3，那么我已经给它赋予了一个语义。X

语言中并没有「3」的概念，而且，「xxx

」这个句子除了为真，其并没有被赋予任何含义。

图灵计算是一种形式语言。这种语言的字母表只有两个字母，0 和 1，所有的句子都是比特序列。然而，我给这些比特序列赋予的语义是非常随意的。正如我在 9.2 节中指出的那样，我可以将比特序列 11 解释为 π

，尽管 11 不是数字 π

的直接二进制编码。因此，正如形式语言可以描述无理数一样，计算机也可以做到这一点，给比特序列一个合适的语义解释。计算机与人类的伙伴关系使这种语义解释成为可能，而且由于在任何形式语言中，可能的语义数量要远远多于句子的可数数量，因此，其中存在着很大的创造空间。

在刻画模型的过程中，科学家和工程师广泛地使用了关于实数的数学形式语言。尽管在任何形式语言中，可以形成的句子的数量是可数的，但是这些模型可以用来描述行为包含不可数集合的系统。例如，法拉第定律方程（256），刻画了一个连续统中的电压和电流，但这个定律仍然可以用一种形式语言进行编码。事实上，当我们在模型中使用连续统时，我们经常使用包含不可数集合的模型，例如对时间或空间的建模。通过适当选择的语义解释，这些模型就可以被计算机操作。然而，如果没有对语义的解释，这些操作就毫无意义。因此，计算机与人类的伙伴共生关系变得至关重要。

然而，如果物理世界中可能存在的系统或行为的数量是不可数的，那么给定任何一种形式语言和任何一种语义解释，我们都可以预见大多数系统是无法被描述的。没有足够的句子来描述系统的一个微小子集。如果自然界不局限于只给出可描述的系统，那么我们应该假设，在自然界中发现的任何系统都有可能是任何特定的形式语言和语义解释所无法描述的。

人类并不局限于只使用一种形式语言和一种语义解释。的确，对于任何特定的形式语言，例如基于策梅洛 - 弗兰克尔集合论的数学语言，我们都只能构造出可数数量的句子。然而，我们可以发明新的语言。事实上，我们一直以来都是这样做的。每一种编程语言都是一种形式语言，我们不断地创造新的语言。我们可以对任何形式的语言中的句子进行任意的语义解释。尽管计算机只产生 0 和 1，但我们可以将一个 0 和 1 的串解释为自然语言中构成句子的字母表中的一个字母序列。我的这本书是在计算机上写成的，从形式上讲，这本书就是一个由 0 和 1 组成的序列。但是，只有人类才能赋予其意义。

如果我们的目标是工程而不是科学，那么我们不需要用新的语言来描述一些预先存在的物理系统，例如人类的认知。相反，我们只需要语言能够描述一些有用的东西，甚至只是一些优雅或有趣的东西。同时，我们需要该语言是可实现的。我们需要找到一种与该语言高度相符的物理实现。它不一定是完美的，也没有一台计算机是完美的。

模型是相似的，它们都基于某种形式语言来表达。作为一名工程师，我需要模型是可以被理解的，同时，我还需要和我所构建的模型高度相符的物理系统。我不需要我的模型是真实的。例如，我们都知道，我们可以制造一个很好的气球机器，即使周长永远不会是 π×d。另外，我们也可以制造出一个相当好的电感，即使法拉第定律无法精确地描述它的行为。

数学模型能够描述软件无法数字式地处理的行为，但是通过给计算机操作的形式化符号赋予语义解释，计算机就可以帮助人类使用这些模型。例如，计算机有时可以证明定理，并象征性地求解涉及实数的数学方程。然而，从根本上说，软件局限于一个可数的世界，它也局限于那些算法式的、逐步执行的过程。如果物理世界并非那么有限，有一些机器就可以执行软件无法执行的功能。我认为，物理世界如此有限是极不可能的。因此，尽管我们可以用软件做一些令人感到惊奇的事情，但无论如何我们都无法用它去做任何事情。甚至，我们可以用软件去做的事情往往需要与人类合作，才能赋予它任何的语义含义。换言之，计算机绝对不是通用机器。

__________

1 One way to construct the set of real numbers from the set of rational numbers is using the idea of a Dedekind cut, named after the German mathematician Richard Dedekind. A Dedekind cut is a partition of the set of rational numbers into two nonoverlapping subsets A and B , where all elements of A are less than all elements of B and A has no greatest element. The set of all such cuts can be put into a one-to-one correspondence with the real numbers and in fact can be taken to define the set of real numbers. The set B may or may not have a least element. If B has a least element, then the cut is put into correspondence with that least element, a rational number, and hence also a real number. If B has no least element, then the cut is put into correspondence with the unique irrational number that lies between A and B , in a sense filling the「gap」between them. This gap prevents the set of rational numbers from forming a continuum. It is remarkable that the number of such cuts, the cardinality of the set of Dedekind cuts, is vastly larger than the number of rational numbers, a result due to Cantor.

2 An exception is the holographic principle, a property of string theories and possibly of quantum gravity first proposed by the Dutch physicist Gerard 't Hooft. The holographic principle replaces the notion of three-dimensional space with lower dimensional surfaces and in at least one form replaces quantum theory with a new deterministic theory. There is quite a bit of controversy around this and related theories (Smolin, 2006).

3 For a wonderfully readable story about Ω, see Chaitin (2005).

4 The notion that「knowing」something is not the same as being able to describe it was immortalized in 1964 by United States Supreme Court Justice Potter Stewart who described his threshold test for obscenity in Jacobellis v. Ohio as,「I know it when I see it.」

5 See chapter 11 for a discussion of what it means for something to have probability zero.
