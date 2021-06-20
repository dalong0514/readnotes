## 记忆时间

## 目录

0301 The invention of stress and strain

0401 Designing for safety

## 0301. The invention of stress and strain

现在我们可以总结一下这一章的内容：

1、应力，它表示固体内某一点的原子因受载荷作用而被拉开或挤压的难度（即要施加多大的力）。

2、应变，它表示固体内某一点的原子被拉开或挤压的程度。

3、应力和应变不是一回事。

4、我们常常用材料的强度指代破坏它所需的应力。

5、杨氏模量，它表示材料有多强劲或松软。

6、强度和刚度也不是一回事。

引用《强材料新科学研究》中的一段文字：「饼干硬而弱，钢材硬且强，尼龙柔（低 E）且强，树莓果冻柔（低 E）且弱。这两种属性共同定义了固体，你也能用它们合理地评估新材料。」

对于上述种种，你也许会感到些许怀疑或困惑，但下面这件事可能会让你稍感安慰。不久前，我在剑桥大学花了整整一晚的时间，试图向两位举世闻名的科学巨擘解释应力、应变、强度和刚度之间的根本区别，因为他们准备向英国政府提议一个耗资巨大的项目。但是，我不清楚他们听明白了多少。

### 3.0

–or Baron Cauchy and the decipherment of Young’s modulus

What would life be without arithmetic, but a scene of horrors?

Rev. Sydney Smith, letter to a young lady, 22 July 1835

Apart from Newton and the prejudices of the eighteenth century, the main reason why the science of elasticity got stuck for so long was that the few scientists who did study it tried to deal with forces and deflections by considering the structure as a whole – as Hooke had done – rather than by analysing the forces and extensions which could be shown to exist at any given point within the material. All through the eighteenth century and well into the nineteenth, very clever men, such as Leonhard Euler (1707–83) and Thomas Young (1773–1829), performed what must appear to the modern engineer to be the most incredible intellectual contortions in their attempts to solve what now seem to us to be quite straightforward problems.

The concept of the elastic conditions at a specified point inside a material is the concept of stress and strain. These ideas were first put forward in a generalized form by Augustin Cauchy (1789–1857) in a paper to the French Academy of Sciences in 1822. This paper was perhaps the most important event in the history of elasticity since Hooke. After this, that science showed promise of becoming a practical tool for engineers rather than a happy hunting-ground for a few somewhat eccentric philosophers. From his portrait, painted at about this time, Cauchy looks rather a pert young man, but he was undoubtedly an applied mathematician of great ability.

When, eventually, English nineteenth-century engineers bothered to read what Cauchy had said on the subject, they found that, not only were the basic concepts of stress and strain really quite easy to understand, but, once they had been understood, the whole study of structures was much simplified. Nowadays these ideas can be understood by anybody,* and it is hard to account for the bewildered and even resentful attitude which is sometimes taken up by laymen when ‘stresses and strains' are mentioned. I once had a research student with a nice new degree in zoology who was so upset by the whole idea of stress and strain that she ran away from the university and hid herself. I still do not see why.

应力与应变 —— 柯西男爵与杨氏模量

生活中要是没了算术，将是多么恐怖的场景？

—— 西德尼·史密斯（Sydney Smith），引自 1835 年 7 月 22 日致一位年轻女士的信

弹性科学之所以长期停滞不前，除了因为牛顿与 18 世纪的偏见之外，还有一个主要原因，那就是少数研究它的科学家在尝试处理力和挠度的问题时将结构视为一个整体，就像胡克曾经做的那样，而非分析材料内任意一点上的力和伸长量。整个 18 世纪直至 19 世纪，莱昂哈德·欧拉（Leonhard Euler）和托马斯·杨（Thomas Young）等顶级智者，试图应对大多数现代工程师眼中最不可思议的智力挑战，解决我们今天看来一目了然的问题。

在材料内部，某一点的弹性状态指的就是应力和应变。奥古斯丁·柯西（Augustin Cauchy）在 1822 年提交给法兰西科学院的一篇论文中率先提出了这两个概念。这篇论文或许是自胡克以来弹性研究史上最重要的成果，此后这门学科逐渐成为工程师的实践工具，而不再只是几个蹩脚哲学家的消遣。根据大致绘于此时的肖像画，柯西看上去就像一个毛头小子，但毋庸置疑，他也是一位能力非凡的应用数学家。

2『应力和应变，做一张术语卡片。（2021-06-19）』

最终，19 世纪的英国工程师费尽心力去解读柯西在这个课题上的三言两语，他们发现，不仅应力和应变的基本概念非常容易理解，而且一旦理解了，关于结构的整个研究也变得非常简洁明了。如今，任何人都能理解这两个概念，[1] 所以提及「应力和应变」时，有些人仍会采取困惑甚至愤恨的态度，就让人很难理解了。我带过一个研究生，她当时刚获得动物学学位，但被应力和应变的整套观念弄得心烦意乱，以致逃离了大学。我至今仍搞不懂这是为什么。

[1] 显然，《牛津词典》除外。当然，在日常交流中，这两个词被用来描述人的精神状态，其含义似乎是一样的。但在自然科学中，这两个词的含义相当清晰，区别也相当明显。

### 3.1 Stress – which is not to be confused with strain

As it happened, Galileo himself very nearly stumbled upon the idea of stress. In the Two New Sciences, the book he wrote in his old age at Arcetri, he states very clearly that, other things being equal, a rod which is pulled in tension has a strength which is proportional to its cross-sectional area. Thus, if a rod of two square centimetres cross-section breaks at a pull of 1,000 kilograms, then one of four square centimetres cross-section will need a pull of 2,000 kilograms force in order to break it, and so on. That it should have taken nearly two hundred years to divide the breaking load by .the area of the fracture surface, so as to get what we should now call a ‘breaking stress' (in this case 500 kilograms per square centimetre) which might be applied to all similar rods made from the same material almost passes belief.

Cauchy perceived that this idea of stress can be used, not only to predict when a material will break, but also to describe the state of affairs at any point inside a solid in a much more general kind of way. In other words the ‘stress' in a solid is rather like the ‘pressure' in a liquid or a gas. It is a measure of how hard the atoms and molecules which make up the material are being pushed together or pulled apart as a result of external forces.

Thus, to say ‘The stress at that point in this piece of steel is 500 kilograms per square centimetre' is no more obscure or mysterious than to say ‘The pressure of the air in the tyres of my car is 2 kilograms per square centimetre – or 28 pounds per square inch.' However, although the concepts of pressure and stress are fairly closely comparable, we have to bear in mind that pressure acts in all three directions within a fluid while the stress in a solid is often a directional or one-dimensional affair. Or, at any rate, so we shall consider it for the present.

Numerically, the stress in any direction at a given point in a material is simply the force or load which happens to be acting in that direction at the point, divided by the area on which the force acts.* If we call the stress at a certain point s, then

$$Sress = s = \frac{load}{area} = \frac{P}{A}$$

where P = load or force and A is the area over which the force P can be considered as acting.

Figure 1. Stress in a bar under tension. (Compressive stress is exactly analogous.)

To revert to our brick, which we left in the last chapter hanging from its string. If the brick weighs 5 kilograms and the string has a cross-section of 2 square millimetres, then the brick pulls on the string with a force of 5 kilograms, and the stress in the string will be:

or, if we prefer it, 250 kilograms force per square centimetre or kgf/cm2.

如何区分应力与应变

事实上，伽利略差点儿就提出了应力的概念。他晚年在阿切特里创作的《两门新科学》（Two New Sciences）把这个问题论述得非常清楚：在其余因素都不变的情况下，拉伸状态下杆的强度与其横截面积成正比。因此，若一根横截面积为 2 平方厘米的杆在 1 000 千克配重的拉伸作用下断裂，那么横截面积为 4 平方厘米的杆则需要 2 000 千克配重的拉力才能让它断裂，以下类推。大概过了将近 200 年，人们用断裂载荷除以断口面积，得到了我们今天所谓的「断裂应力」（在这个情境中，断裂应力为 500 千克力 [2] / 平方厘米）。它适用于所有由同种材料制成的均质杆，这实在是太棒了。

柯西察觉到，这种应力的概念普遍适用，不仅可用来预测材料何时会断裂，还可以用来描述固体内任意点的状态。换句话说，固体中的应力有点儿像液体或气体中的压力，它度量的是构成材料的原子和分子在外力作用下聚集或分离的难度。

1『这个隐喻太赞了，「固体中的应力如同液体或气体中的压力，它度量的是构成材料的原子或分子在外力作用下聚集或分离的难度。」做一张金句卡片。（2021-06-19）』—— 已完成

因此，「这块钢中某点的应力为 500 千克力 / 平方厘米」与「我的汽车轮胎里的气压是 2 千克力 / 平方厘米或者 28 磅力 / 平方英寸」，这两种表述同样简单易懂。然而，尽管压力和应力的概念紧密相关，但我们需要牢记的一点是，流体中的压力作用在全部三个方向上，而固体中的应力通常是单向或一维的。不管怎样，我们下面来探讨一下。

定量地看，材料中某个点在任一方向上的应力等于沿该方向作用在该点上的力或载荷除以该力的作用面积。[3] 若我们设某点的应力为 s，则有：

$$应力 = s = \frac{荷载}{面积} = \frac{P}{A}$$

其中，P 为载荷或力，而 A 是 P 的作用面积（见图 3–1）。

回到我们上一章中提到的砖头例子。如果砖头重 5 千克，绳子的横截面积为 2 平方毫米，那么绳子的应力为：

或者，我们也可以把它写成 250 千克力 / 平方厘米（kgf/cm2）。

图 3–1 一根木棒在拉伸作用下的应力（挤压作用下的应力同理）

[2] 1 千克力指 1 千克物体所受的重力。—— 编者注

[3] 可是，一个「点」怎么会有「面积」呢？我们可以参考速度的类比：我们把单位时间经过的距离表示为速度，例如 100 英里 / 小时（约为 161 千米 / 小时），但我们通常关心的是某个无限短暂瞬间的速度。

### 3.2 Units of stress

This raises the vexed question of units of stress. Stress can be expressed in any units of force divided by any units of area – and it frequently is. To reduce the amount of confusion we shall stick to the following units in this book.

MEGANEWTONSPER SQUARE METRE: MN/m2. This is the SI unit. As most people know, the SI (System International) habit is to make the unit of force the Newton.

1-0 Newton = 0-102 kilograms force = 0-225 pounds force (roughly the weight of one apple).

1 Meganewton = one million Newtons, which is almost exactly 100 tons force.

POUNDS (FORCE) PER SQUARE INCH: p.s.i. This is the traditional unit in English-speaking countries, and it is still very widely used by engineers, especially in America. It is also in common use in a great many tables and reference books.

KILOGRAMS (FORCE) PER SQUARE CENTIMETRE: kgf/cm2 (sometimes kg/cm2). This is the unit in common use in Continental countries, including Communist ones.

FOR CONVERSION

Thus the stress in our piece of string, which we found to be 250 kgf/cm2, is also equal to 24-5 MN/m2 or 3,600 p.s.i. Since the calculation of stresses is not usually a very accurate business, there is no sense in fussing too much about very exact conversion factors.

It is worth repeating that it is important to realize that the stress in a material, like the pressure in a fluid, is a condition which exists at a point and it is not especially associated with any particular cross-sectional area, such as a square inch or a square centimetre or a square metre.

应力的单位

这就引出了应力的单位这个棘手的问题。应力可以表示为任意单位的力除以任意单位的横截面积，我们通常就是这样做的。为了避免混淆，我们在本书中统一使用以下单位。

兆牛顿 / 平方米（MN/m2）。这是一个国际单位制的单位。大部分人都知道，国际单位制中力的惯用单位是牛顿。

1.0 牛顿 = 0.102 千克力 = 0.225 磅力（差不多相当于一个苹果的重量）。

1『结构专业的人常说的受力多少牛每平米（KN/m2），原来来源于此，1KN/m2 差不多是每平方面积上荷载 102 公斤，醍醐灌顶啊。1 牛顿数值的记忆可以通过 1 公斤除以 9.81 算出来。另外：超级意外的是，1 牛顿的力竟然差不多是一个苹果的重量，跟牛顿被苹果砸中脑袋的故事「关联」上了，只是巧合么。（2021-06-19）』

1 兆牛顿 = 100 万牛顿，约等于 100 吨力。

磅（力）/ 平方英寸（psi）。这是一个传统的英制单位，仍被工程师广泛使用，尤其是在美国。它也常见于大量表格和工具书中。

千克（力）/ 平方厘米（kgf/cm2，有时也写作 kg/cm2）。这个单位常见于欧洲大陆国家。

单位间换算：

1 MN/m2=10.2 kgf/cm2=146 psi

1 psi=0.006 85 MN/m2=0.07 kgf/cm2

1 kgf/cm2=0.098 MN/m2=14.2 psi

所以，绳子的应力 250 kgf/cm2 约等于 24.5 MN/m2 或 3 600 psi。应力的计算通常不是一项精益求精的工作，过于追求换算精度实在没有必要。值得强调的是，材料中的应力就像流体中的压力，是某一点的状态，而与横截面积无关，不管它是 1 平方英寸（约为 6.45 平方厘米）、1 平方厘米，还是 1 平方米。

2『上面的信息全部补充进术语卡片「应力和应变」。（2021-06-19）』—— 已完成

### 3.3 Strain – which is not the same thing as stress

Just as stress tells us how hard – that is, with how much force – the atoms at any point in a solid are being pulled apart, so strain tells us how far they are being pulled apart – that is, by what proportion the bonds between the atoms are stretched.

Figure 2. Strain in a bar under tension. (Compressive strain is exactly analogous.)

Thus, if a rod which has an original length L is caused to stretch by an amount l by the action of a force on it, then the strain, or proportionate change of length, in the rod will be e, let us say, such that:

To return to our string, if the original length of the string was, say, 2 metres (or 200 cm), and the weight of the brick causes it to stretch by 1 centimetre, then the strain in the string is:

Engineering strains are usually quite small, and so engineers very often express strains as percentages, which reduces the opportunities for confusion with noughts and decimal points.

Like stress, strain is not associated with any particular length or cross-section or shape of material. It is also a condition at a point. Again, since we calculate strain by dividing one length by another length – i.e. the extension by the original length – strain is a ratio, which is to say a number, and it has no units, SI, British or anything else. All this applies just as much in compression, of course, as it does in tension.

什么是应变

应力表示的是固体中任意一点的原子被拉开有多难，即要用多大的力；而应变告诉我们能把它们拉开多远，也就是说，原子间化学键被拉伸多大的比例（见图 3–2）。

图 3–2 一根木棒在拉伸作用下的应变（挤压作用下的应变同理）

因此，如果一根原长为 L 的木棒在一个力的作用下被拉伸的长度为 l，那么这根木棒的应变或长度变化比为 e：

$$e = \frac{l}{L}$$

回到绳子的例子，如果绳的原长为 2 米（或 200 厘米），砖块的重量使它伸长了 1 厘米，那么绳子的应变为：

工程中的应变往往很小，所以工程师常用百分数表示应变，以降低数错零和弄错小数点位置的风险。

像应力一样，应变与材料的长度、横截面积或形状都无关，它只是某个点的状态。此外，因为我们计算应变时是用一个长度除以另一个长度 —— 伸长量除以原长，所以应变是一个比值，它没有单位，无论是在国际单位制、英制还是其他任何单位制中。当然，上述种种既适用于拉伸的情况，也适用于压缩的情况。

### 3.4 Young's modulus- or how stiff is this material?

As we have said, Hooke's law in its original form, though edifying, was the result of a rather inglorious muddle between the properties of materials and the behaviour of structures. This muddle arose mainly from the lack of the concepts of stress and strain, but we also have to bear in mind the difficulties which would have existed in the past in connection with testing materials.

Nowadays, when we want to test a material – as distinct from a structure – we generally make what is called a ‘test-piece' from it. The shapes of test-pieces may vary a good deal but usually they have a parallel stem, on which measurements can be made, and are provided with thickened ends by which they can be attached to the testing machine. An ordinary metal test-piece often looks like Figure 3.

Figure 3. A typical tensile test-piece.

Testing machines also vary a good deal in size and in design, but basically they are all mechanical devices for applying a measured load in tension or in compression.

The stress in the stem of the test-piece is obtained merely by dividing the load recorded at each stage on the dial of the machine by the area of its cross-section. The extension of the stem of the test-piece under load – and therefore the strain in the material – is usually measured by means of a sensitive device called an extensometer, which is clamped to two points on the stem.

With equipment of this kind it is generally quite easy to measure the stress and the strain which occur within a specimen of a material as we increase the load upon it. The relationship between stress and strain for that material is given by the graph of stress plotted against strain which we call the ‘stress-strain diagram'. This stress-strain diagram, which may look something like Figure 4, is very characteristic of any given material, and its shape is usually unaffected by the size of the test-piece which happens to have been used.

Figure 4. A typical ‘stress-strain diagram'.

When we come to plot the stress-strain diagram for metals and for a number of other common solids we are very apt to find that, at least for moderate stresses, the graph is a straight line. When this is so we speak of the material as ‘obeying Hooke's law' or sometimes of a ‘Hookean material'.

What we also find, however, is that the slope of the straight part of the graph varies greatly for different materials (Figure 5). It is clear that the slope of the stress-strain diagram measures how readily each material strains elastically under a given stress. In other words it is a measure of the elastic stiffness or floppiness of a given solid.

Figure 5. The slope of the straight part of the stress-strain diagram is characteristic of each different material. E, the Young's modulus of elasticity, represents this slope.

For any given material which obeys Hooke's law, the slope of the graph or the ratio of stress to strain will be constant. Thus for any particular material

Young's modulus is sometimes called ‘the elastic modulus' and sometimes ‘E', and is quite often spoken of as ‘stiffness' in ordinary technical conversation. The word ‘modulus', by the way, is Latin for ‘a little measure'.

Our string, it may be remembered, was strained 0-5 per cent or 0-005 by the weight of the brick, which imposed a stress of 24-5 MN/m2 or 3,600 p.s.i. The Young's modulus of the string is therefore

杨氏模量

我们说过，尽管胡克定律的原始形式颇具启发性，但却是混淆材料特性与结构行为的尴尬产物。这种混淆主要是由于未对应力和应变进行准确定义，但我们也不要忘记过去在测试材料方面遇到的困难。

今天，当我们测试一种材料（与测试一个结构不同）时，我们一般会制取一份所谓的「试样」。试样的形状可能各不相同，但它们通常都有一个平直的主体（可在其上做测试），还有更粗一些的末端（可用来与测试仪器连接）。普通的金属试样一般如图 3–3 所示。

图 3–3 一个典型的拉伸试样

测试仪器的尺寸和设计也各不相同，但基本上它们都是对试样施加载荷的机械装置。通过读取机器表盘上的载荷数，再除以横截面积，便可得到试样主体上的应力。我们通常会用引伸计这种灵敏的仪器在主体上夹取两点，进而测量在载荷作用下试样主体的伸长量以及材料的应变。

有了这种设备我们可以很容易地测量试样的应力和应变。材料应力和应变间的关系可以由「应力–应变」曲线呈现，如图 3–4 所示，它充分反映了给定材料的特征，其形状通常不受试样尺寸的影响。

图 3–4 典型的应力–应变曲线

如果我们为金属等常见固体材料绘制「应力–应变」曲线，就会很容易地发现，至少在应力适度的条件下，该曲线呈现为一条直线。这就是所谓的「遵循胡克定律」的材料，有时也叫「胡克材料」。然而，我们还发现，对于不同的材料，直线的斜率差别很大（见图 3–5）。显然，「应力–应变」曲线的斜率度量了该材料在给定应力下的弹性。换言之，它度量了给定固体的弹性刚度或弛度。

图 3–5 应力–应变曲线的直线部分的斜率表征了不同材料的不同弹性。斜率 E 表示的是杨氏模量

1『上面图里各个材料的弹性模量（刚度）：钢材 > 铝材 > 骨骼 > 木材。（2021-06-19）』

对于遵循胡克定律的给定材料，斜率或应力与应变之比为定值。杨氏模量有时也被称为「弹性模量」（elastic modulus），记作 E，在平常的技术交流中它往往会被说成是「刚度」。顺便说一下，「模量」（modulus）这个词在拉丁文中的意思是「一个小的度量尺寸」。

1-3『解惑了解惑了，之前竟然在其他人口里听到的某某材料的「刚度」，竟然就是弹性模量（杨氏模量），也即胡克定律里的那个斜率。太赞了。（2021-06-19）』

回想一下绳子的例子，在由砖头的重量产生的 24.5 MN/m2 或 3 600 psi 应力的影响下，产生了 0.5% 或 0.005 的应变。所以，绳子的杨氏模量为：4900 MN/m2。

### 3.5 Units of stiffness or Young's modulus

Since we are dividing a stress by a fraction, which is to say a number, which has no dimensions, Young's modulus has the same dimensions as a stress and is expressed in stress units, that is to say MN/m2, p.s.i. or kgf/cm2. Since, however, Young's modulus may be regarded as that stress which would double the length of the material (i.e. the stress at 100 per cent strain) – if the material did not break first – the numbers involved are often large, and some people find them difficult to visualize.

杨氏模量的单位

因为我们是用应力去除以一个无量纲的分数，所以杨氏模量与应力具有同样的量纲，即以应力的单位表示。但是，由于杨氏模量衡量的是将材料拉伸为原长的两倍时的应力（也就是百分之百应变时的应力，前提是该材料还未断裂），其数值往往很大，让人觉得难以想象。

### 3.6 Practical values of Young's modulus

The Young's moduli of a number of common biological and engineering materials are given in Table 1. Starting from the cuticle of the pregnant locust (which is low, but not very exceptionally low, for biological materials; the cuticle of the male locust and of the virgin female locust is a lot stiffer, by the way) the Young's moduli are arranged in ascending order all the way to diamond. It will be seen that the range of stiffness varies by about 6,000,000 to one. Which is a lot. We shall discuss why this should be so in Chapter 8.

It may be noticed that a good many common soft biological materials do not occur in this table. This is because their elastic behaviour does not obey Hooke's law, even approximately, so that it is really impossible to define a Young's modulus, at any rate in the terms we have been talking about. We shall come back to this sort of elasticity later on.

TABLE 1 Approximate Young's moduli of various solids

By courtesy of Dr Julian Vincent, Department of Zoology, University of Reading.

Young's modulus is nowadays regarded as a pretty fundamental concept; it thoroughly pervades engineering and materials science and is beginning to invade biology. Yet it took all of the first half of the nineteenth century for the penny to drop in the minds of engineers. This was partly due to sheer conservatism and partly due to the late arrival of any workable concept of stress and strain.

Given these ideas, few things are simpler or more obvious than Young's modulus; without them, the whole affair must have seemed impossibly difficult. Young, who was to play an important part in the decipherment of Egyptian hieroglyphics and who had one of the finest brains of his generation, obviously had a very severe intellectual struggle.

Working around the year 1800, he had to approach the problem by a route quite different from that which we have just used, and he considered the question in terms of what we should now call the Specific modulus', that is, by how much a column of a material might be expected to shorten under its own weight. Young's own definition of his modulus, published in 1807, is as follows: ‘The modulus of the elasticity of any substance is a column of the same substance, capable of producing a pressure on its base which is to the weight causing a certain degree of compression as the length of the substance is to the diminution of its length.'*

After which, Egyptian hieroglyphics must have appeared simple.

It was said of Young by one of his contemporaries that ‘His words were not those in familiar use, and the arrangement of his ideas seldom the same as those he conversed with. He was therefore worse calculated than any man I ever knew for the communication of knowledge.' All the same we have to realize that Young was wrestling with an idea that was scarcely capable of expression without the concepts of stress and strain, which did not come into use until fifteen or twenty years later. The modern definition of Young's modulus (E = stress/strain) was given in 1826 – three years before Young died – by the French engineer Navier (1785-1836). As the inventor of stress and strain, Cauchy was eventually made a baron by the French government. He seems to have deserved it.

常见材料的杨氏模量

常见生物材料和工程材料的杨氏模量值可见表 3–1：从怀孕蝗虫的表皮（其值很低，但对生物材料而言，不算特别低；顺便说一下，雄性蝗虫和雌性蝗虫幼虫的表皮都很强劲）起，杨氏模量按升序排列，直至钻石。我们将看到，在刚度变化区间内，上限与下限之比大到 6 000 000。我们将在第 8 章中探讨其中的原因。

表 3–1 各种固体的杨氏模量的近似值

| Material | Young's modulus (E) p.s.i. | Young's modulus (E) MN/m2 |
| --- | --- | --- |
| 怀孕蝗虫的表皮（Soft cuticle of pregnant locust*） | 30 | 0.2 |
| 橡胶（Rubber） | 1,000 | 7 |
| 鸡蛋壳膜（Shell membrane of egg） | 1,100- | 8 |
| 人体软骨（Human cartilage） | 3,500 | 24 |
| 人体肌腱（Human tendon） |  80,000 | 600 |
| 墙板（Wallboard） | 200,000 | 1,400 |
| 未加固的塑料、聚乙烯、尼龙（Unreinforced plastics, polythene, nylon） | 200,000 | 1,400 |
| 胶合板（Plywood） | 1,000,000 | 7,000 |
| 木材（顺纹）Wood (along grain) | 2,000,000 | 14,000 |
| 新鲜的骨头（Fresh bone） | 3,000,000 | 21,000 |
| 金属镁（Magnesium metal） | 6,000,000 | 42,000 |
| 普通玻璃（Ordinary glasses） | 10,000,000 | 70,000 |
| 铝合金（Aluminium alloys） | 10,000,000 | 70,000 |
| 黄铜和青铜（Brasses and bronzes） | 17,000,000 | 120,000 |
| 铁和钢（Iron and steel） | 30,000,000 | 210,000 |
| 氧化铝（蓝宝石）Aluminium oxide (sapphire) | 60,000,000 | 420,000 |
| 钻石（Diamond） | 170,000,000 | 1,200,000 |

2『各个材料的杨氏模量近似值，做一张信息数据卡片。（2021-06-19）』—— 已完成

表格来源：By courtesy of Dr Julian Vincent, Department of Zoology, University of Reading.

1-2『表里看到墙板的杨氏模量是 1400 MN/m2，相当于 142.8 吨/平，超级大，不过它是指把墙板拉伸至原来 2 倍所需的应力，那么我做关心的是一定厚度的墙板，能承受的最大荷载是多少呢。或者说，200mm 厚的楼板，应变是多少的时候会倒塌。目前想到的是：200mm 厚的楼板，应变 1mm 所需的应力为 0.714T（即 714 公斤）。正确的解答待以后确认。（2021-06-19）』—— 未完成

值得注意的是，许多常见的柔性生物材料都不在上表中。这是因为它们的弹性行为即便近似，也不遵循胡克定律，所以在我们使用的术语体系中，实在没法定义它们的杨氏模量。我们稍后再来讨论这类弹性问题。

如今，杨氏模量被视为一个相当基本的概念；它已完全渗入工程学与材料科学领域，并开始向生物学领域进军。然而，最初历经了整个 19 世纪上半叶的时间，这个概念才在工程师的脑海中留下了些许印象。部分原因在于纯粹的保守主义，还有部分原因是应力和应变的概念来得太迟了。

有了这些概念，杨氏模量就变得更简单也更直观了；离开了它们，有些东西理解起来将非常困难。托马斯·杨在对埃及象形文字的解读方面扮演了重要角色，他拥有同时代人中最聪慧的头脑，但也身陷一场最严酷的智力斗争之中。

1-3『上面提到的托马斯·杨原来就是破解古埃及文字的那个大牛啊，竟然是同一个人，太意外了，第一次知道他是在吴军的《信息论》专栏课里。（2021-06-19）』

1800 年前后，他用了一种与我们刚才介绍的截然不同的方法来应对这一难题，他依靠的是「比模量」的概念，即一段柱状材料在其自身重量的作用下会缩短多少。托马斯·杨于 1807 年给杨氏模量下了定义：「任意材料的弹性模量是指同一材料的一段柱体对其底部产生的压力与造成某一压缩量的重量之比等于该材料长度与长度缩短量之比。」[4]

相较而言，埃及象形文字也显得简单多了。

一位同时代的人这样评价托马斯·杨：「他的措辞不是人们惯用的，也常常词不达意。因此，在知识交流方面，他比我认识的任何人都逊色。」尽管如此，我们务必明白托马斯·杨是在缺少应变和应力的定义的前提下表述了一个极其复杂的概念，而那两个概念直到 15-20 年后才开始使用。法国工程师纳维叶（Navier）在 1826 年给出了杨氏模量的现代定义（E = 应力 / 应变），三年后托马斯·杨就去世了。作为应力和应变概念的提出者，柯西最终被法国政府授予男爵封号，他当之无愧。

[4] 尽管科学素为贵族大臣们所关注，且你的论文也颇受重视，但它太学究气了…… 简言之，就是太难以理解了。 —— 英国海军部致托马斯·杨函

### 3.7 Strength

It is necessary to avoid confusion between the strength of a structure and the strength of a material. The strength of a structure is simply the load (in pounds force or Newtons or kilograms force) which will just break the structure. This figure is known as the ‘breaking load', and it naturally applies only to some individual, specific structure.

The strength of a material is the stress (in p.s.i. or MN/m2 or kgf/cm2) required to break a piece of the material itself. It will generally be the same for all specimens of any given solid. We are most often concerned with the tensile strength of materials, which is sometimes called the ‘ultimate tensile stress' or U.T.S. This is usually determined by breaking small test-pieces in a testing machine. Naturally, the object of many strength calculations is to predict the strength of a structure from the known strength of its material.

TABLE 2 Approximate tensile strengths of various solids

The tensile strengths of a good many materials are given in Table 2. As with stiffness, it will be seen that the range of strengths in both biological and engineering solids is very wide indeed. For instance, the contrast between the weakness of muscle and the strength of tendon is striking, and this accounts for the very different cross-sections of muscles and their equivalent tendons. Thus the thick and sometimes bulging muscle in our calves transmits its tension to the bone of our heel, so that we can walk and jump, by means of the Achilles or calcaneal tendon, which, although it is pencil-thin, is generally quite adequate for the job. Again, we can see why engineers are unwise to put tensile forces on concrete unless that weak material is sufficiently reinforced with strong steel rods.

The strong metals are rather stronger, on the whole, than the strong non-metals. However, nearly all metals are considerably denser than most biological materials (steel has a specific gravity of 7-8, most zoological tissues about 1-1). Thus, strength for weight, metals are not too impressive when compared with plants and animals.

We might now sum up what has been said in this chapter: load

It expresses how hard (i.e. with how much force) the atoms at a point within a solid are being pulled apart or pushed together by a load.

It expresses how ./or the atoms at a point within a solid are being dragged apart or pushed together.

Stress is not the same thing as strain.

Strength. By the strength of a material we usually mean that stress which is needed to break it.

It expresses how stiff or how floppy a material is.

Strength is not the same thing as stiffness.

To quote from The New Science of Strong Materials: ‘A biscuit is stiff but weak, steel is stiff and strong, nylon is flexible (low E) and strong, raspberry jelly is flexible (low E) and weak. The two properties together describe a solid about as well as you can reasonably expect two figures to do.'

In case you should ever have felt any trace of doubt or confusion on these points, it might be of some comfort to know that, not so long ago, I spent a whole evening in Cambridge trying to explain to two scientists of really shattering eminence and worldwide fame the basic difference between stress and strain and strength and stiffness in connection with a very expensive project about which they were proposing to advise the government. I am still uncertain how far I was successful.

1 Except, apparently, the Oxford Dictionary, The words are used, of course, in casual conversation to describe the mental state of people and as if they meant the same thing. In physical science the meanings of the two words are quite clear and distinct.

2 How can a ‘point' have an ‘area'? Consider the analogy of speed: we express speed as the distance covered in a certain length of time, e.g. miles per hour, although we are concerned usually with the speed at any given -infinitely brief- moment.

3 Though science is much respected by their Lordships and your paper is much esteemed, it is too learned... in short it is not understood (Admiralty letter to Young).

结构强度与材料强度

切记不要把结构强度和材料强度混为一谈。结构强度是指破坏结构所需的载荷，以磅力、牛顿或千克力为单位。这个量度被称作「断裂载荷」，它仅适用于一些特殊的结构。

1-2『真实瞌睡了有人送枕头，这里的结构强度就解答了自己之前「200mm 楼面荷载」的疑问。结构强度和材料强度做一张术语卡片。（2021-06-19）』

材料强度是指破坏材料本身所需的应力，以 psi、MN/m2 或 kgf/cm2 为单位。对于某种固体，无论其样品形态如何，其材料强度一般都是相同的。我们最常关注的是材料的抗拉强度，有时也叫作「极限抗拉应力」，通常使用测试仪器拉断小型试样来确定。所以，我们往往会根据已知的材料强度来测算结构强度。

表 3–2 给出了很多材料的抗拉强度。与刚度一样，生物意义和工程意义上的固体，其强度的变化范围很广。例如，肌肉之弱和肌腱之强对比显著，这也可以解释为何肌肉及其等效肌腱的截面不同。当我们小腿肚上粗壮且时而凸起的肌肉将其紧张状态传递给脚后跟的骨头时，我们便能行走和跳跃，靠的就是跟腱，尽管它非常纤细，但足以胜任这项功能。此外，我们也将看到，为什么工程师在混凝土这种弱材料被强钢筋加固之前就贸然施加拉力，是一种不明智之举。

表 3–2 各种固体的抗拉强度的近似值

| Material | Tensile strength(p.s.i.) | ensile strength(MN/m2) |
| --- | --- | --- |
| 非金属（Non-metals） | - | - |
| 肌肉组织（新鲜但已死）Muscle tissue (fresh but dead) | 15 | 0.1 |
| 膀胱壁（新鲜但已死）Bladder wall | 34 | 0.2 |
| 胃壁（新鲜但已死）Stomach wall | 62 | 0.4 |
| 肠（新鲜但已死）Intestine | 70 | 0.5 |
| 动脉壁（新鲜但已死）Artery wall | 240 | 1.7 |
| 软骨（新鲜但已死）Cartilage | 430 | 3.0 |
| 水泥和混凝土（Cement and concrete） | 600 | 4.1 |
| 普通砖头（Ordinary brick） | 800 | 5.5 |
| 新鲜的皮肤（Fresh skin） | 1,500 | 10.3 |
| 鞣制皮革（Tanned leather） | 6,000 | 41.1 |
| 新鲜的肌腱（Fresh tendon） | 12,000 | 82 |
| 麻绳（Hemp rope） | 12,000 | 82 |
| 顺纹木材（风干）Wood (air dry): along grain | 15,000 | 103 |
| 横纹木材（风干）Wood (air dry): across grain | 500 | 3.5 |
| 新鲜的骨骼（Fresh bone） | 16,000 | 110 |
| 普通玻璃（Ordinary glass） |  5,000-25,000 | 35-175 |
| 人类毛发（Human hair） | 28,000 | 192 |
| 蜘蛛网（Spider's web） | 35,000 | 240 |
| 优质陶瓷（Good ceramics） |  5,000-50,000 | 35-350 |
| 蚕丝（Silk） | 50,000 | 350 |
| 棉纤维（Cotton fibre） | 50,000 | 350 |
| 肠线（Catgut ） | 50,000 | 350 |
| 亚麻（Flax） | 100,000 | 700 |
| 玻璃纤维塑料（Fibreglass plastics） | 50,000-150,000 | 350-1,050 |
| 碳纤维塑料（Carbon-fibre plastics） | 50,000-150,000 | 350-1,050 |
| 尼龙线（Nylon thread） | 150,000 | 1,050 |
| - | - | - |
| 金属（Metals） | - | - |
| 钢材（STEELS） | - | - |
| 钢琴丝（非常脆）Steel piano wire (very brittle) | 450,000 | 3,100 |
| 高强度工程钢（High tensile engineering steel） | 225,000 | 1,550 |
| 工业低碳钢（Commercial mild steel） | 60,000 | 400 |
| 锻铁（WROUGHT IRON） | - | - |
| 传统锻铁（Traditional） | 15,000-40,000 | 100-300 |
| 铸铁（CAST IRON） | - | - |
| 传统铸铁（非常脆）Traditional (very brittle) | 10,000-20,000 | 70-140 |
| 现代铸铁（Modern） | 20,000-40,000 | 140-300 |
| 其他金属（OTHER METALS） | - | - |
| 铸铝（Aluminium: cast） | 10,000 | 70 |
| 锻制铝合金（wrought alloys） | 20,000-80,000 | 140-600 |
| 紫铜（Copper） | 20,000 | 140 |
| 黄铜（Brasses） | 18,000-60,000 | 120-400 |
| 青铜（Bronzes） | 15,000-80,000 | 100-600 |
| 镁合金（Magnesium alloys） | 30,000-40,000 | 200-300 |
| 钛合金（Titanium alloys） | 100,000-200,000 | 700-1,400 |

2『各种固体的抗拉强度的近似值，做一张信息数据卡片。（2021-06-19）』—— 已完成

总的来说，强劲的金属比强劲的非金属的强度更大。但是，几乎所有金属又都比大多数生物材料致密得多（钢的比重为 7.8，而大部分的动物组织约为 1.1）。因此，考虑到重量因素，金属的强度相较于植物和动物，并不太突出。

## 0401. Designing for safety

— or can you really trust strength calculations?

That with music loud and long,

I would build that dome in air,

That sunny dome! Those caves of ice!

And all who heard should see them there,

And all should cry, Beware! Beware!

S. T. Coleridge, Kubla Khan

Naturally all this business about stresses and strains is only a means to an end; that is, to enable us to design safer and more effective structures and devices of one kind or another and to understand better how such things work.

Apparently Nature does not have to bother. The lilies of the field toil not, neither do they calculate, but they are probably excellent structures, and indeed Nature is generally a better engineer than man. For one thing she has more patience and, for another, her way of going about the design process is quite different.

In living creatures the broad general arrangement or lay-out of the parts is controlled during growth by the R N A-DNA mechanism – the famous ‘double helix' of Wilkins, Crick and Watson.* However, in each individual plant or animal, once the general arrangement has been achieved, there is a good deal of latitude about the structural details. Not only the thickness, but also the composition of each load-carrying component is determined, to a considerable extent, by the use which is actually made of it and by the forces which it has to resist during life.† Thus the proportions of a living structure tend to become optimized with regard to its strength. Nature seems to be a pragmatic rather than a mathematical designer; and, after all, bad designs can always be eaten by good ones.

Unfortunately, these design methods are not, as yet, available to human engineers, who are therefore driven to use either guesswork or calculation or, more often, some combination of the two. Both for safety and for economy it is clearly desirable to be able to predict how the various parts of an engineering structure will share the load between them and so to determine how thick or how thin they ought to be. Again, we generally want to know what deflections to expect when a structure is loaded, because it may be just as bad a thing for a structure to be too flexible as for it to be too weak,

设计的安全性 —— 裂缝是怎么出现的？

乐音高昂且悠扬，

伴我凌空筑此穹堂，

此穹堂之煌煌！彼幽穴之冰霜！

凡闻者必来此仰望，

凡见者必喟，提防！提防！

—— 柯勒律治（S. T. Coleridge），《忽必烈汗》（Kubla Khan）

当然，关乎应力和应变的种种只是达到目的的一种手段，帮助我们设计出更安全有效的结构和装置，以及更好地理解它们如何工作。

显然，大自然不必如此大费周章。田间百合本无心，也不必费神计算，但它们本身都是了不起的结构。实际上，大自然有时是比人类更高明的工程师。一方面，它有更多的耐心；另一方面，它对设计流程的处理方式独树一帜。

在生物体中，整体或局部的构造在生长期间受制于 RNA–DNA（核糖核酸–脱氧核糖核酸）机制，即威尔金斯（Wilkins）、克里克（Crick）和沃森（Watson）发现的著名的双螺旋结构。[1] 但是，对具体的植物或动物而言，整体构造一旦成形，其结构细节便五花八门。不仅要确定厚度，还要确定每个负载部位的安排，在很大程度上，这取决于其实际构成部分的运用及其生长中不得不对抗的力量。[2] 因此，生物结构的比例会随其强度而趋于优化。大自然似乎是一位追求实用而非数学化的设计师；毕竟，糟糕的设计总是会被优良的设计吃掉。

遗憾的是，这些设计方法到目前为止还未被人类工程师掌握，因此他们不得不借助猜测或计算，甚至双管齐下。出于安全性和经济性的考虑，我们总是期望能够预测一个工程结构的各部分如何分担它们之间的载荷，以确定它们应该有多厚。而且，我们通常想弄明白一个结构负载时的预期挠度，因为太柔或太弱都不好。

[1] The Double Helix, by James D. Watson, Weidenfeld & Nicolson, 1968.

[2] 这个过程也起着反作用；航天员在太空中经历一段时间的失重后，骨骼会因钙质流失而变得更脆弱。

### 4.1 French theory versus British pragmatism

Once the basic concepts of strength and stiffness had been stated and understood, a considerable number of mathematicians set themselves to devise techniques for analysing elastic systems operating in two and three dimensions, and they began to use these methods to examine the behaviour of many different shapes of structures under loads. It happened that, during the first half of the nineteenth century, most of these theoretical elasticians were Frenchmen. Although very possibly there is something about elasticity Which is peculiarly suited to the French temperament,* the practical encouragement for this research seems to have come, directly or indirectly, from Napoleon I and from the ficole Poly-technique, which was founded in 1794.

Because much of this work was abstract and mathematical it was not understood or generally accepted by most practising engineers until about 1850. This was especially the case in England and America, where practical men were regarded as greatly superior to ‘mere theoreticians'. And besides, one Englishman had always beaten three Frenchmen. Of the Scottish engineer, Thomas Telford (1757-1834), whose magnificent bridges we can still admire, it is related that:

He had a singular distaste for mathematical studies, and never even made himself acquainted with the elements of geometry; so remarkable indeed was this peculiarity that when we had occasion to recommend to him a young friend as a neophyte in his office, and founded our recommendation on his having distinguished himself in mathematics, he did not hesitate to say that he considered such acquirements as rather disqualifying than fitting him for the situation.

Telford, however, really was a great man, and, like Nelson, he tempered his confidence with an attractive humility. When the heavy chains for the Menai suspension bridge (Plate 11) had been hoisted successfully in the presence of a large crowd, Telford was discovered, away from the cheering spectators, giving thanks on his knees.†

Not all engineers were as inwardly humble as Telford, and Anglo-Saxon attitudes at this time were often tinged, not only with intellectual idleness, but also with arrogance. Even so, scepticism about the trustworthiness of strength calculations was not unjustified. We must be clear that what Telford and his colleagues were objecting to was not a numerate approach as such -they were at least as anxious as anybody else to know what forces were acting on their materials – but rather the means of arriving at these figures. They felt that theoreticians were too often blinded by the elegance of their methods to the neglect of their assumptions, so that they produced the right answer to the wrong sum. In other words, they feared that the arrogance of mathematicians might be more dangerous than the arrogance of pragmatists, who, after all, were more likely to have been chastened by practical experience.

Shrewd North-Country consulting engineers realized, as all successful engineers must, that when we analyse a situation mathematically, we are really making for ourselves an artificial working model of the thing we want to examine. We hope that this algebraical analogue or model will perform in a way which resembles the real thing sufficiently closely to widen our understanding and to enable us to make useful predictions.

With fashionable subjects like physics or astronomy the correspondence between model and reality is so exact that some people tend to regard Nature as a sort of Divine Mathematician. However attractive this doctrine may be to earthly mathematicians, there are some phenomena where it is wise to use mathematical analogies with great caution. The way of an eagle in the air; the way of a serpent upon a rock; the way of a ship in the midst of the sea and the way of a man with a maid are difficult to predict analytically. One does sometimes wonder how mathematicians ever manage to get married. After King Solomon had built his temple, he would probably have added that the way of a structure with a load has a good deal in common at least with ships and eagles.

The trouble with things like these is that many of the real situations which are apt to arise are so complicated that they cannot be fully represented by one mathematical model. With structures there are often several alternative possible modes of failure. Naturally the structure breaks in whichever of these ways turns out to be the weakest – which is too often the one which nobody had happened to think of, let alone do sums about.

A deep, intuitive appreciation of the inherent cussedness of materials and structures is one of the most valuable accomplishments an engineer can have. No purely intellectual quality is really a substitute for this. Bridges designed upon the best ‘modern' theories by Polytechniciens like Navier sometimes fell down. As far as I know, none of the hundreds of bridges and other engineering works which Telford built in the course of his long professional life ever gave serious trouble. Thus, during the period when French structural theory was outstanding, a great proportion of the railways and bridges on the Continent were being built by gritty and taciturn English and Scottish engineers who had little respect for the calculus.

法兰西的理性与不列颠的务实

一旦阐明和理解了强度和刚度的基本概念，很多数学家便着手研究关于二维和三维弹性系统的分析技术，并用这些方法检验各种形状的负载结构的行为。巧合的是，在 19 世纪上半叶，大部分研究这种理论的人都是法国人。尽管弹性这个话题可能尤其契合法兰西人的气质，[3] 但其实直接或间接促进这项研究的人是拿破仑一世（Napoleon I），以及创立于 1794 年的法国巴黎综合理工大学。

由于这项工作既抽象又与数学相关，所以直到 1850 年左右，它才被大部分执业工程师理解或接受。在英国和美国，情况尤其如此，人们认为实干家比「纯理论家」可靠得多。而且，「一个英国人能顶上三个法国人」。关于苏格兰工程师托马斯·特尔福德（Thomas Telford）—— 我们现在仍能欣赏到他设计的宏伟桥梁 —— 有这样的记载：

他特别厌恶数学研究，甚至连几何学的基础知识也不熟悉；这种做派实在是惊世骇俗，以至于当我们推荐一位在数学上表现很好的年轻朋友到他的办公室工作时，他竟然毫不犹豫地说那个人不符合他的要求。

然而，特尔福德确实是个了不起的人。像纳尔逊（Nelson）一样，他以一种迷人的谦逊锤炼自己的信心。当梅奈悬索桥（见插图 11）的沉重铁链在众人面前成功吊装时，特尔福德正在远离万众欢腾的地方跪地感恩。[4]

并非所有工程师都像特尔福德那样谦卑，在这个时代，大多数的盎格鲁-撒克逊人不仅懒于动脑，而且态度傲慢。即便如此，他们对强度计算可信度的怀疑也不是毫无道理。我们必须清楚，特尔福德和他的同行反对的并不是定量方法本身（他们至少和其他任何人一样，渴望弄明白是什么力作用在他们的材料上），而是得到这些数据的手段。他们觉得理论家常沉溺于方法之优雅，而忽略了他们是在做假设，以至于他们会基于错误的计算得出答案。换言之，他们担心数学家的傲慢可能比务实者的自负更危险，但归根结底，后者历经的实践磨炼更多。

英格兰北部那些精明的顾问工程师，就像所有成功的工程师一样意识到，当我们从数学角度分析一种情境时，我们其实是在人为制造一个关于我们要检验的东西的模型。我们希望，这个代数化的模拟或模型以一种足够接近实物的方式运作，以便拓宽我们的理解，使我们做出有用的预测。

随着物理学或天文学等学科的流行，模型与现实之间的精准对应使一些人逐渐将大自然视为某种神圣的数学家。无论这条教义多么吸引世俗数学家，在一些现象中，如履薄冰地运用数学类比才是明智之举。鹰翔空中，蛇伏石上，船行汪洋以及男女之间，都难以用解析方法做出预测。人们有时会纳闷数学家究竟是怎么结成婚的。所罗门王造好神殿后或许会补充说，一个结构负载的方式至少与船和鹰有很多共通之处。

这些事情的麻烦之处在于，许多经常出现的真实情况如此复杂，以至于不能完全用一个数学模型来表示。对于结构，常有几种可能的失败模式。当然，结构总会在其最弱的地方垮掉，而这个地方往往是人们没有想到的，更不用说做过计算了。

对材料和结构固有的强度做一番深刻且直观的评估，是一位工程师最有价值的成就之一。没有哪种纯粹的智慧能取而代之。就算是像纳维叶这样毕业于法国巴黎综合理工大学的人借助最好的「现代」理论设计的桥梁，有时也会倒塌。据我所知，在特尔福德漫长的职业生涯中，他建造的数百座桥梁及其他工程还没有出现大问题的。因此，在法式结构理论大放异彩的时期，欧洲大陆上的铁路和桥梁中有很大一部分是由埋头苦干且不懂微积分的英格兰和苏格兰工程师建造的。

[3] 法国的索菲·热尔曼（Sophie Germain）可能是唯一一位在弹性领域取得成就的女性。与此相关的是，这一时期最具高等教育背景和理论头脑的两位工程师 —— 马可·布鲁内尔爵士（Sir Marc Brunel）和他的儿子伊桑巴德·金德姆·布鲁内尔（Isambard Kingdom Brunel）都是法裔。

[4] 无视数学的英国传统靠 19 世纪一群杰出的工程师传承不绝，尤其是亨利·罗伊斯爵士（Sir Henry Royce），他造出了「世界上最好的轿车」。

### 4.2 Factors of safety and factors of ignorance

All the same, after about 1850 even British and American engineers did begin to do calculations about the strength of important structures, such as large bridges. They calculated the highest probable tensile stresses in the structure by the methods of the day, and they saw to it that these stresses were less than the official ‘tensile strength' of the material. To make quite sure, they made the highest calculated working stress much less – three or four or even seven or eight times less – than the strength of the material as determined by breaking a simple, smooth, parallel-stemmed test-piece.* This was called ‘applying a factor of safety'. Any attempt to save weight and cost by reducing the factor of safety was only too likely to lead to disaster.

Accidents were very apt to be put down as due to ‘defective material', and a few of them may have been. Metals, of course, do vary in strength between different samples, and there is always some risk of poor material being built into a structure. However, iron and steel usually vary in strength by only a few per cent and very, very rarely by anything like a factor of three or four, let alone seven or eight. Practically always discrepancies as big as this between the theoretical and the actual strengths are due to other causes; at some unknown place in the structure the real stress must be very much higher than the calculated stress, and thus the ‘factor of safety' is sometimes referred to as the ‘factor of ignorance'.

Nineteenth-century engineers usually made things which were subject to tension stresses, such as boilers and beams and ships, out of wrought iron or mild steel, which had, with some justice, the reputation of being ‘safe' materials. When a large factor of ignorance had been applied to the strength calculations, such structures often turned out to be quite satisfactory, although in fact accidents continued to occur fairly frequently.

Trouble became increasingly common with ships. The demand for speed and lightness led both the Admiralty and the shipbuilders into difficulties, since ships tended to break in two at sea although the highest calculated stresses seemed to be quite safe and moderate. In 1901, for instance, a brand-new turbine destroyer, H.M.S. Cobra, one of the fastest ships in the world, suddenly broke in two and sank in the North Sea in fairly ordinary weather. Thirty-six lives were lost. Neither the subsequent court martial nor the Admiralty Committee of Inquiry shed much light on the technical causes of the accident.

In 1903, therefore, the Admiralty made and published a number of experiments with a similar destroyer, H.M.S. Wolf at sea in rough weather. These showed that the stresses deduced from strain measurements made on the hull under real conditions were rather less than those calculated by the designers before the ship was built. Since both sets of stresses were far below the known ‘strength' of the steel from which the ship was constructed – the factor of safety being between five and six – these experiments were only moderately enlightening.

安全系数与无知系数

大约在 1850 年之后，即使是英国或美国工程师也开始计算大型桥梁等重要结构的强度了。他们用当时的方法估算出结构的最大拉应力，以确保这些应力小于材料额定的「抗拉强度」。为了做到万无一失，他们令算出的最大工作应力远远小于该材料的强度，取 1/3、1/4 甚至 1/7 或 1/8（材料的强度由拉断一个简单、光滑且主体平直的试样决定）。[5] 这就是所谓的「应用安全系数」。任何通过减小安全系数来节约重量和成本的尝试，都很有可能引发灾难。

2『安全系数和无知系数，做一张术语卡片。（2021-06-20）』—— 已完成

这类事故极易被归因于「材料缺陷」，少数几次确实是这样。当然，不同金属样品之间的强度差异很大，而且劣质材料确实会混入结构中。但是，钢铁的强度差异往往只有百分之几，3 倍或 4 倍实属罕见，更不用说 7 倍或 8 倍了。所以在实践中，理论强度和实际强度之间的差异往往是由其他原因造成的；在结构中的某些未知区域，真实的应力肯定比计算出的应力大得多，因此「安全系数」有时也被称为「无知系数」。

19 世纪的工程师经常用锻铁或低碳钢制造需承受拉应力的东西，比如锅炉、横梁和船舶，所以这些材料也拥有「安全」材料之誉。当我们在强度计算中引入一个较大的安全系数时，结果常常相当令人满意，但实际上事故仍然层出不穷。

船舶制造遇到的麻烦越来越多。对高航速和轻量化的要求使英国海军部和造船厂都陷入了困境，虽然算出的最大应力看似相当安全，但船舶在海上还是免不了被断成两截。例如，1901 年，当时世界上最快的舰艇之一 —— 一艘新式涡轮驱逐舰（英国皇家海军的眼镜蛇号），意外被断成两截，沉入了风平浪静的北海。这起事故造成 36 人丧生，但事后军事法庭和英国海军部调查委员会都没有详细披露造成此次事故的技术原因。

于是，海军部于 1903 年用类似的皇家海军狼号驱逐舰，在天气恶劣的海上做了一系列实验，并公布了结果。结果表明，真实条件下测量得出的船体应力比造船前设计师计算出来的结果小得多。因为两组应力都远低于已知的造船钢材的「强度」—— 安全系数为 5-6，所以这些实验都仅作为参考。

[5] 1910 年，在蒸汽机车的连杆设计中，安全因数至少要达到 18。

3『

[强度 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%BC%BA%E5%BA%A6)

极限抗拉强度是在外力作用下，材料抵抗破坏的能力 [1]，也可翻译为极限拉伸强度，简称强度。

根据外力的作用方式，有多种强度指标，如抗拉强度、抗弯强度、抗剪强度等。当材料承受拉力时，强度性能指标主要是屈服强度和抗拉强度。

注意强度和硬度是本质上不同的概念。玻璃等硬而脆的物质，虽然硬度大（变形与外力之比小）但强度小（在断裂之前能承受的总外力小）。对于同系列的金属，此二者可以有一定的对应关系。强度测量往往需要彻底毁坏材料，而硬度试验则毁坏较小或不毁坏。所以校定的硬度强度换算关系被用来由硬度推算强度。

金属材料的强度是金属材料的在外力作用下抵抗永久变形和断裂的能力。工程上常用来表示金属材料强度的指标有屈服强度和抗拉强度。

屈服强度是金属材料发生屈服现象时达到塑性变形发生而力不增加的应力点。

抗拉强度是指金属材料在拉断前所能承受的最大应力。

』

### 4.3 Stress concentrations – or how to start a crack

The first important step towards the understanding of problems of this kind was achieved, not by very expensive practical experiments on full-scale structures, but by theoretical analysis. In 1913 C. E. Inglis, who was later Professor of Engineering at Cambridge and was the very opposite of a ‘remote and ineffectual don', published a paper in the Transactions of the Institution of Naval Architects whose consequences and applications extend far beyond the strength of ships.

What Inglis said about elasticians was really very much what Lord Salisbury is supposed to have said about politicians, namely that it is a great mistake to use only small-scale maps. For nearly a century elasticians had been content to plot the distribution of stresses in broad, general or Napoleonic terms. Inglis showed that this approach can be relied on only when the material and the structure have smooth surfaces and no sudden changes of shape.

Geometrical irregularities, such as holes and cracks and sharp corners, which had previously been ignored, may raise the local stress – often only over a very small area – very dramatically indeed. Thus holes and notches may cause the stress in their immediate vicinity to be much higher than the breaking stress of the material, even when the general level of stress in the surrounding neighbourhood is low and, from general calculations, the structure might appear to be perfectly safe.

This fact had been known, of course, in a general kind of way, to the people who put the grooves in slabs of chocolate and to those who perforate postage stamps and other kinds of paper. A dressmaker cuts a ‘nick' in the selvedge of a piece of cloth before she tears it. Serious engineers, however, had not shown much interest in these fracture phenomena, which were not considered to belong to' proper' engineering.

Figure 1. Stress trajectories in a bar uniformly loaded in tension (a) without and (b) with a crack.

That almost any hole or crack or re-entrant in an otherwise continuous solid will cause a local increase of stress is easily explained. Figure la shows a smooth, uniform bar or plate of material, subject to a uniform tensile stress, s. The lines crossing the material represent what are called ‘stress trajectories', that is to say, typical paths by which the stress is handed on from one molecule to the next. In this case they are, of course, straight parallel lines, uniformly spaced.

If we now interrupt a number of these stress trajectories by making a cut or a crack or a hole in the material, then the forces which the trajectories represent have to be balanced and reacted in some way. What actually happens is more or less what one would expect; the forces have to go round the gap, and as they do so the stress trajectories are crowded together to a degree which depends chiefly upon the shape of the hole (Figure lb). In the case of a long crack, for instance, the crowding around the tip of the crack is often very severe. Thus in this immediate region there is more force per unit area and so the local stress is high (Plate 2).

Inglis was able to calculate the increase of stress which occurs at the tip of an elliptical hole in a solid which obeys Hooke's law.* Although his calculations are strictly true only for elliptical holes they apply with sufficient accuracy to openings of other shapes. Thus they apply not only to port-holes and doors and hatchways in ships and aeroplanes and similar structures but also to cracks and scratches and holes in all sorts of other materials and devices – to fillings in teeth, for example.

In terms of simple algebra what Inglis said was that, if we have a piece of material which is subject to a remotely applied stress s, and if we make a notch or a crack or a re-entrant of any kind in it having a length or depth L, and if this crack or re-entrant has a radius at the tip of r, then the stress at and very near to the tip is no longer s but is raised to:

For a semi-circular notch or a round hole (when r — L) the stress will thus have the value of 3s; but for openings like doors and hatchways, which often have sharp corners, r will be small and L large, and so the stress at the comers may be very high -quite high enough to account for ships breaking in two.

In the Wolf experiments, extensometers, or strain-gauges, were clamped to the ship's plating in various positions. By this means the extension or elastic movement of the steel plates could be read off. From this the strain – and thus the stress – in the steel was easily calculated. As it happened none of the extensometers was placed close to the corners of hatchways or other openings. If this had been done some very frightening readings would almost certainly have been obtained when the ship was plunging into a head sea in Portland Race.

When we turn from hatchways to cracks the situation is even worse, because, while cracks are often centimetres or even metres long, the radius of the tip of the crack may be of molecular dimensions – less than a millionth of a centimetre – so that is very large; thus the stress at the tip of the crack may well be a hundred or even a thousand times higher than the stress elsewhere in the material.

If Inglis's results had to be taken entirely at their face value it would scarcely be possible to make a safe tension structure at all. In fact the materials which are actually used in tension, metals, wood, rope, Fibreglass, textiles and most biological materials, are ‘ tough', which means, as we shall see in the next chapter, that they contain more or less elaborate defences against the effects of stress concentrations. However, even in the best and toughest of materials, this protection is only relative, and every tension structure is susceptible to some extent.

The ‘brittle solids', however, which are used in technology, like glass and stone and concrete, do not have these defences. In other words they correspond pretty closely to the assumptions which were made in Inglis's calculations. Moreover we do not need to put in stress-raising notches artificially in order to weaken these materials. Nature has already done this liberally, and real solids are nearly always full of all kinds of small holes and cracks and scratches, even before we begin to make a structure out of them.

For these reasons it is rash to use any of the brittle solids in situations where they may be subject to appreciable tension stresses. They are, of course, very widely used in masonry and for roads and so on where they are, at least officially, in compression. Where we cannot avoid a certain amount of tension, for instance in glass windows, we have to take care to keep the tensile stresses very small indeed and to use a large factor of safety.

In talking of stress concentrations we must note that weakening effects are not exclusively caused by holes and cracks and other deficiencies of material. One can also cause stress concentrations by adding material, if this induces a sudden local increase of stiffness. Thus if we put a new patch on an old garment or a thick plate of armour on the thin side of a warship, no good will come of it.*

The reason for this is that the stress trajectories are diverted just as much by an area which strains too little, such as a stiff patch, as they are by an area which strains too much, such as a hole. Anything which is, so to speak, elastically out of step with the rest of the structure will cause a stress concentration and may therefore be dangerous.

When we seek to ‘strengthen' something by adding extra material we have to be careful we do not in fact make it weaker. The inspectors employed by insurance companies and government departments who insist on pressure vessels and other structures being' strengthened' by the addition of extra gussets and webs are sometimes responsible, in my experience, for the very accidents which they have tried to prevent.

Nature is generally rather good at avoiding stress concentrations of this and other kinds. However, one would think that stress concentrations must be of significance in orthopaedic surgery, especially when the surgeon fits a stiff metal prosthesis to a relatively flexible bone.

NOTE. In Inglis's formula (p. 67) L is the length of a crack proceeding inwards from the surface, i.e. half the length of an internal crack.

1 See, for instance, The Double Helix, by James D. Watson, Weidenfeld & Nicolson, 1968.

2 The process also works in reverse; the bones of astronauts lose calcium and become weaker after a period of weightlessness in space.

3 Almost the only woman to have gained distinction in elasticity, Mademoiselle Sophie Germain (1776-1831), was French. It may be relevant that two of our most highly educated and theoretically-minded engineers during this period, Sir Marc Brunei (1769-1849) and his son, Isambard Kingdom Brunei (1806-59), were of French origin.

4 The British tradition of totally ignoring mathematics has been splendidly continued in the present century by a number of distinguished engineers, notably Sir Henry Royce, who did, after all, create the ‘best car in the world'.

5 Factors of safety as high as eighteen were used in the design of connecting-rods for steam locomotives at least as late as 1910.

6As a matter of fact the effect of a round hole in a plate under tension had been calculated by Kirsch in Germany in 1898 and that of an elliptical hole by Kolosoff in Russia in 1910, but, as far as I know, little notice was taken of these results in English shipbuilding circles.

7 'Partial strength produces general weakness' (Sir Robert Seppings (1767-1840), Surveyor of the Navy 1813-32).

裂缝是如何产生的

要理解这类问题，最重要的不是做耗资巨大的全尺寸结构实验，而是进行理论分析。1913 年，英格利斯（C. E. Inglis）—— 后来的剑桥工程学教授，与「坐而论道的教员」截然不同 —— 在《船舶工程师学会学报》上发表了一篇论文，引发了更广泛的讨论和应用，而不仅限于船舶的强度。

英格利斯希望告诉弹性研究者的事与索尔兹伯里勋爵（Lord Salisbury）对政客说的话几乎一样，即只用小比例地图是个严重的错误。近一个世纪以来，弹性研究者一直满足于用宽泛、大致或拿破仑式的术语绘制应力分布图。英格利斯表明，这种方法只适用于表面光滑且没有形状突变的材料和结构。

几何上的不规则性，比如孔洞、裂缝和尖锐边角，之前被忽视了，但实际上，它们会显著提高局部应力 —— 通常分布在一个非常小的区域内。因此，孔洞和沟槽可能导致其相邻区域的应力比该材料的断裂应力大得多，即便周边区域应力的总体水平很低且根据计算该结构可能是安全的。

当然，从某种意义上说，在巧克力块上刻槽及在邮票和其他纸张上打孔的人都知道这个事实。一个裁缝在撕开一块布之前，会先在其边缘剪出一个「口子」。然而，严肃的工程师对这类断裂现象没有多大兴趣，没有考虑将其归为「严格意义」上的工程学问题。

不连续固体中的任何孔洞、裂缝或凹陷，几乎都会导致局部应力的增加，这很容易解释。图 4–1（a）显示了一段光滑均匀的木棒受到一个均匀的拉应力 s 的作用。穿过材料的虚线表示所谓的「应力作用线」，即应力从一个分子传递到下一个分子的典型路径。当然，在这种情况下，它们是一组间隔均匀的平行线。

图 4–1 在均匀拉伸的载荷下，无裂缝（a）和有裂缝（b）的木条上的应力作用线

如果我们现在通过在材料上制造一个切口、裂缝或孔洞来阻碍某些应力作用线，这些作用线代表的力为保持平衡就需要以某种方式做出反应。实际发生的事情与人们想象的多少有些相同：力不得不绕过缺口，应力作用线的聚集程度主要取决于孔洞的形状［见图 4–1（b）］。例如，如果裂缝较长，那么裂缝尖端附近的应力作用线往往异常密集。因此在其相邻区域，单位面积上的力更大，局部应力也更大（插图 2）。

英格利斯算出了遵循胡克定律的固体上一个椭圆孔洞的尖端处的应力增加量。[6] 他的计算不只对椭圆孔洞是严格正确的，用于其他形状的开口也足够精确。因此，其结果不仅适用于船舶、飞机等类似结构中的舷孔、舱门和舱口，还可用于各种其他材料和装置中的裂缝、划痕和孔洞，例如牙齿填充物。

根据简单的代数运算，英格利斯说，若我们有一块材料受到远场应力 s 的作用，我们在其上制造一个任意形状、长度或深度为 L、尖端半径为 r 的沟槽、裂缝或凹陷，它的尖端及其相邻处的应力就不再是 s，而是增加为：

$$s(1+2\sqrt{\frac{L}{r}})$$

所以，对半圆沟槽或圆孔洞而言（r=L），其应力值为 3s；但对像舱门和舱口这样常有尖锐边角的开口来说，r 会很小而 L 会很大，所以边角处的应力可能非常大，足以让船舶断成两截。

在狼号驱逐舰实验中，引伸计或应变仪被夹在舰船镀层的不同位置。借助这些仪器，我们可以读出钢板的伸长量或弹性运动。据此，钢板的应变和应力就很容易计算出来了。巧合的是，没有一个引伸计被置于靠近舱口或其他开口的边角处。如果这样做，当船扎进波特兰岛大潮的浪头时，肯定能取得一些非常惊人的读数。

当我们从舱口转向裂缝时，情况变得更糟了，因为裂缝长度通常为厘米乃至米的量级，而其尖端半径可达到分子尺度 —— 小于百万分之一厘米，这使得 L/r 非常大。因此，裂缝尖端处的应力很可能是材料中其他地方应力的上百倍，甚至上千倍。

如果英格利斯的结果完全按其表面意义取值，那么我们根本不可能造出一个安全的承张结构。事实上，在拉伸状态下实际使用的材料，如金属、木材、绳索、玻璃纤维、织物以及大部分生物材料，都很坚韧。这意味着，它们或多或少会具备某种精妙的机制来抵御应力集中的效应，我们将在下一章中讨论这个问题。然而，即便在最好、最坚韧的材料中，这种防护也是相对的，而每种承张结构在某种程度上都是敏感的。

但是，像玻璃、石头和混凝土等「脆性固体」，则没有这种防护机制。换言之，它们相当符合英格利斯在计算中所做的假设。而且，我们不需要人为制造可增加应力的沟槽来弱化这些材料。大自然已经慷慨地为我们准备了，在我们用它们来搭建结构之前，真实的固体几乎总是遍布各种微小的孔洞、裂缝和划痕。

基于这些原因，在承受相当大的拉应力的情况下，使用任何脆性固体的行为都是轻率之举。当然，它们在砖石建筑、道路等领域应用广泛，但至少应在承压状态下。有时我们无法避免一定的张力，例如在玻璃窗中，我们既要小心维持非常小的拉应力，还得应用一个较大的安全系数。

谈到应力集中，我们务必注意，弱化效应并不完全是由孔洞、裂缝及其他材料缺陷造成的。附加材料也可以导致应力集中，前提是这样做诱发了局部刚度的突增。因此，如果我们在旧衣服上打块新补丁，或者在军舰的薄弱处加装护甲板，是不会有好结果的。[7]

原因在于，像强劲的补片这样小的应变区域造成的应力作用线转移，同像孔洞这样大的应变区域造成的应力作用线转移的效应差不多。可以说，弹性与结构的其余部分不协调的任何材料都会导致应力集中，并可能带来危险。

当我们试图通过附加材料来「强化」某物时，务必要小心，不要适得其反。据我的经验，受雇于保险公司和政府部门的检验员，若坚持通过安装加固件和加固套「强化」压力容器和其他结构，有时就可能引发他们试图防止的事故。大自然通常很擅长规避这种或那种应力集中。但是，有人认为应力集中对于骨科手术意义重大，尤其是在外科大夫把强劲的金属假体安装到柔韧的骨头上时。

（注：在英格利斯的公式中，L 是裂缝从材料表面向内延伸的长度，如果裂缝在材料内部，则取其长度的一半。）

[6] 事实上，在拉伸作用下一块板上的一个圆孔洞的应力效应，已由德国的基尔希（Kirsch）于 1898 年算出，而椭圆孔洞的应力效应已由俄国的克罗索夫（Kolosoff）于 1910 年算出。但据我所知，这些结果在英语区的船舶工业领域几乎没有引起注意。

[7] 1813-1832 年英国海军测量师罗伯特·赛平斯爵士（Sir Robert Seppings）曾说：「局部强化导致整体弱化。」