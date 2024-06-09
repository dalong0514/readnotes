Donald M. MacKay.(1969).2024041Information-Mechanism-and-Meaning.The M.I.T. Press => Preface

## Preface

In a day when it is hard enough in most fields of science to keep abreast of new and non-redundant literature, the publication of collected papers, like the estatc of holy matri- mony, is something not to be undertaken unadvisedly, lightly or wantonly'. In the present case it would not have been considered at all but for the kindly initiative of my respected friend Profcssor Roman Jakobson, whose persistent encourage- ment alone overcame that distaste which most of us feel for our ten- to twenty-year-old productions and brought this first volume to the point of no return. It is true that these exploratory papers were scattered among an unconscionably awkward selection of publications for anyone wanting to follow them up. On the other hand, as most of them were written for specific occasions, each of which demanded some rehearsal of points covered in earlier essays, the resulting repetitiveness presented a special problem. With occasional exceptions, redundancy could have bcen climinated only at the cost of mutilating individual papers. The solution adopted has been to leave almost all repetitive passages intact, offsetting in small print those that can be skipped without loss by readers of the earlier chapters. Where some comment has seemed necessary, by way of foreword or postscript to the original papers, the passages added have been italicized.

With the exception of Chapter 1 (written especially to sketch in the background of the prcsent collection) all the main text has already been published or broadcast over the past twenty years, and I am grateful to the following for permission to reprint:

British Broadcasting Corporation (Chapters 2, 3 and 4)

Josiah Macy Jr. Foundation (Chapter 5 and Appendix)

D. Reidel(Chapter 6)

Butterworths(Chapters 7, 8 and 12)

Harpcr and Row (Chapter 9)

The RAND Corporation(Chapters 10 and 11)

Verlag Friedr. Vieweg Son(Chapter 13)

Academic Press (Appendix)

Taylor and Francis (Appendix)

The collection proper falls into two parts, Part I consisting of three introductory broadcast talks and Part II a series of more technical papers. An explanatory survey of the termin- ology of information theory, prepared for the 1950 London Symposium on Information Theory, has been added as an Appendix. The author's first exploratory paper on Quantal Aspects of Scientific Information'(1950) has not been in- cluded, partly because its main points are covered in other papers reproduced here but also because I am now less satisfied with it than with any of the rest. Some extracts from this paper appear as part of a postscript to the Appendix, dealing in more detail with the logon-capacity of optical instruments.

It is a pleasure to express my thanks to a number of col- leagues whose comments have helped to shape the present collection, to Miss Margaret Steele for tireless secretarial assistance, and to my wife for the considerable labour of compiling the index.

D. M. MAcKAY

Keele, Staffordshire

December 1968 

前言

在如今的科学领域中，要跟上新的和非重复的文献已经非常困难，因此，出版收集的论文就像婚姻一样，不应该轻率、轻浮或任性地进行。在当前的情况下，这本书的出版完全是由于我尊敬的朋友 Roman Jakobson 教授的善意倡议。他的坚持和鼓励克服了我们大多数人对十到二十年前作品的厌恶，使得这本第一卷书的出版成为不可逆转的事实。确实，这些探索性论文分散在一些极不方便查阅的出版物中，对于任何想要继续研究它们的人来说都是如此。另一方面，由于大多数论文是为特定场合撰写的，每次都需要重述早期文章中涵盖的一些观点，因此产生的重复性带来了特殊问题。除非以牺牲个别论文为代价，否则冗余只能在偶尔的情况下被消除。我们采用的解决方案是几乎保留所有重复的段落，并用小字体偏移那些可以被早期章节读者跳过而不丢失内容的段落。如果某些评论作为对原始论文的前言或后记是必要的，添加的段落已用斜体表示。

除了第 1 章（特别撰写来概述本集背景）外，所有主要文本在过去二十年里已经发表或广播过，我感谢以下机构允许重新印刷：

英国广播公司（第 2、3、4 章）

Josiah Macy Jr. 基金会（第 5 章和附录）

D. Reidel（第 6 章）

Butterworths（第 7、8 和 12 章）

Harper and Row（第 9 章）

兰德公司（第 10 和 11 章）

Verlag Friedr. Vieweg Son（第 13 章）

学术出版社（附录）

Taylor and Francis（附录）

该文集主要分为两部分：第一部分包含三篇介绍性广播讲座，第二部分则是一系列更技术性的论文。我们还将 1950 年伦敦信息理论研讨会中准备的信息理论术语解释调查作为附录加入。虽然作者 1950 年的第一篇关于科学信息量子方面的探索性论文没有包含在内，但其主要观点已在其他论文中有所体现。此外，作者对这篇论文的满意度也不如其他作品。不过，这篇论文的一些摘录作为附录的附言出现，详细讨论了光学仪器的逻辑容量。

在此，我要感谢许多同事，他们的评论帮助塑造了这本文集。特别感谢 Margaret Steele 女士无私的秘书协助，以及我的妻子在编制索引方面的辛勤劳动。

D. M. MAcKAY

Keele, Staffordshire

1968 年 12 月

## Background

Towards the end of the Second World War, in the Ad- miralty's radar establishment, I found myself trying to follow the behaviour of electrical pulses over extremely short inter- vals of time. Inevitably, one came up against fundamental physical limits to the accuracy of measurement. Typically, these limits scemed to be related in a complementary way, so that one of them could be widened only at the expense of a narrowing of another. An increase in time-resolving power, for example, seemed always to be bought at the expense of a reduction in frequency-resolving power; an improvement in signal-to-noise ratio was often inseparable from a reduction in time-resolving power, and so on. The art of physical measurement seemed to be ultimately a matter of compro- mise, of choosing between reciprocally related uncertainties. I was struck by a possible analogy between this situation and the one in atomic physics expresscd by Heisenberg's well-known 'Principle of Uncertainty'. This statcs that the momentum (p) and position (g) of a particle can never be exactly determined at the same instant. The smaller the imprecision (Ap) in p, the larger must be the imprecision (Aq) in g, and vice versa. In fact, the product Ap × Ag can never be less than Planck's Constant h, the 'quantum of action'. Action (energy × time) is thus the fundamental physical quantity whose 'atomicity' underlies the compro- mise-relation expressed in Heisenberg's Principle.

It seemed natural to ask what would happen if one multi- plied together the reciprocally varying quantities in various compromise-relations of the sort I had encountered in experimental measurement. Perhaps these also might reflect the invariance of some fundamental 'quantum'. But a quantum of what? Tentatively, I called it a quantum of information. Multiplying together the conjugate pairs of uncertainty-limits mentioned, however, I found that they formed invariant products of not one but two distinct kinds. In one group, the product was a dimensionless number of order 1. In the other, it was a small quantity with the di- mensions of physical entropy. Each of these represented an irreducible limiting factor of experimentation, a "quantum' more fundamental than either of the two 'uncertainties' of which it was the product.

What then distinguishcd the two groups? It turned out to be something very simple. The first group of limits, which formed a dimensionless product, were calculable a priori (without reference to the measurement actually made), from a specification of the instrument. The second group, which formed products with the dimensions of entropy, could be calculated only a posteriori, from a specification of what was done with the instrument.

This was in 1945/46. In Autumn 1946 I moved to King's College, London, to teach physics, and a colleague on whom I tried out these notions suggested that there might be a link between my quanta of information' and the 'atomic propositions' postulated in Wittgenstein's famous Traclalus Logico-Philosophicus. Although in the analysis of ordinary language Wittgenstein himself had now repudiated the atomistic approach of the Tractatus,4º the field of scientific measurement seemed well suited to logical treatment on these lines; for it builds everything ideally upon simple assertions of what Eddington called 'coincidence-relations' and 'occupance-relations' between pointers and scales. At all events, it seemed worth while to explore the possibility that the 'quantization of information' I had stumbled upon in an experimental context was connected with the logical atomicity' of the statements that would ideally represent the outcome of the experiment. Was it possible that by analysing the logical rcquirements for the making of a scientific statement one might find a rational connection between the two kinds offquanta'?

As will appear later in this volume, it seemed that one might. A measurement could be thought of as a process in which elementary physical events, each of some prescribed minimal significance, are grouped into conceptually dis- tinguishable categories so as to delineate a certain form (for example, the image on a photographic plate or the wave form on an oscilloscope)with a given degree of precision. In principle, the notion was that each elementary event could justify the addition of one 'atomic fact' to the logical frame- work representing what took place in ultimate physical terms. For example, any observation pressed to its physical limits could be regarded as an occasion on which the thermo- dynamic balance of an instrument was disturbed to an extent that could be measured in units of physical entropy. Each of these units, then-suitably defined-could be considered to provide one elementary building-block for an abstract representation of what occurred, the total of such building- blocks being distributed among the various categories or degrees of freedom' made available by the instrumcnt, in much the same way as unit events are distributed among the columns of a histogram. Thus the 'informational effici- ency'of a given measurement could be estimated by the proportion of those elementary events involved that find themselves represented by atomic facts in a logically adequate statement of the result.

Here then was a possible clue to the meaning of my two kinds of 'quanta'. A scientific representation, viewed in this light, could have its 'size' specified in two complementary ways: (a)by enumerating its degrees of freedom, and (b) by enumerating its atomic facts. Correspondingly, a representa- tion could be augmented in two complementary ways: (a)by adding to its degrees of freedom or 'logical dimensionality' (number of logically distinguishable categories); (b)by adding to its total of atomic facts or 'weight of evidence'(number of elementary events represented). On inspection, it turned out that the two kinds of quantal limits found in physical measure- ment represented simply the minimal physical costs of aug- menting a representation by one unit of the corresponding kind. One could thus speak of a 'unit of information' in either sense as 'that which validates one elementary addition to a logical form representing the result'; but in the first case each unit would add one additional dimension (conceptual category), whereas in the second each unit would add one additional alomic fact. In order to avoid confusion it seemed appro- priate to distinguish the first as 'structural units' and the sccond as 'metrical units' of information.

It soon became clear that the idea of measuring information was not new. In 1946 Dennis Gabor, then with the B.T.H. Company in Rugby (England), published his classic paper6 entitled Theory of Communication', in which the Fouricr- transform theory used in wave-mechanics was applied to the frequency-time (f.1) domain of the communication engineer, with the suggestion that a signal occupying an elementary area of Af. At= could be regarded as a 'unit of information', which he termed a 'logon'. Much earlier, in 1935, the statistician R. A. Fisher had proposed a measure of the 'Information' in a statistical sample, which in the simplest case amounted to the reciprocal of the variance(see Appendix). It was far from obvious, on first encountering these dis- parate concepts, whether they could be fitted in any sensible way into the same framework; but on reflection it became apparent that they were in fact examples of 'structural'and 'metrical' measures, respectively. Gabor's logons, each occupy- ing an area Af. At=in the f.t plane, represented the logical dimensions of his communication signals. They belonged to the same family as the 'structural units' that occupy an analogous elementary area (the Airy disc) in the focal plane of a micro- scope, or of a radar aerial. It thus seemed appropriate, with Gabor's blessing, to give the term 'logon-content' a more general definition, as the measure of the logical dimensionality of representations of any form, whether spatial or temporal.

Fisher's measure, which is additive for averaged samples, invited an equally straightforward interpretation as an index of 'weight of evidence'. If we define (arbitrarily but reasonably) a unit or quantum of metrical information (termed a 'metron') as the weight of evidence that gives a probability of to the corresponding proposition, Fisher's 'amount of information' becomes simply proportional to the number of such units supplied by the evidence in question.

Gabor's and Fisher's measures of information were not, however, the only candidates in the field. In 1948, C. E. Shannon published his 'Mathematical Theory of Commu- nication',31 which proposed for communication signals a measure based on the statistical improbability of the signal. Since the logarithm of improbability is additive for indepen- dent signals, this obviously had attractive properties. The question was how it related to the 'structural' and ‘metrical' measures already in being. Not unnaturally, there was a strong tendency in the late forties to regard all these measures as rivals for a single title, or as suggesting rival concepts of 'information'. A further question was where, if anywhere, the notion of 'meaning' fitted into the scheme of things. Shannon's analysis of the 'amount of information' in a signal, which disclaimed explicitly any concern with its meaning, was widely misinterpreted to imply that the en- gineers had defined a concept of information per se that wasd totally divorced from that of meaning.

By the time I had plucked up enough courage to publish something on the subject,12 the outlines of a possible syn- thesis had begun to emerge, and this was given a trial airing in papers23 prepared for our first London Symposium on Information Theory in 1950. Although some aspects of these early explorations may be only of historical interest, a sample is reprinted as an Appendix at the end of the present collection.

Resurrecting and sorting over these twenty-year-old speculations, what strikes one most forcibly is the number of vaguely perceived lines of development, not all of them unpromising, that one has never followed up. The main deflecting factor, it must be confessed, was the lure of a new trail that originated in the conjunction of my interests in information theory and clectronic computation. If the concept of information had these dual aspects, the structural and the metrical, what kind of computing mechanism, one wondered, would be best adapted to handle the most general possible transformations of information? In particular, what sort of mechanism must the human brain be, in order to deal as it does with the sort of thing that information is?

Some attempts to wrestle with these problems will appear in a companion volume to the present collection. I mention them now because by the end of 1950 the challenge of the most complex of all computing mechanisms had become my focal interest. A year among neurophysiologists in the United States (1951) completed the transition process; and, for good or ill, most of my remaining half-baked ideas in the field of 'pure' information theory were Ieft to grow cold.

The bulk of the papers in the present volume were written after this change of research emphasis, and they reflect a corresponding preoccupation with information as represented and utilized in the brain and exchanged betwcen human beings, rather than as formalized in logical patterns of elementary propositions. I have not lost hope of a fruitful link between physical and logical atomism in fundamental physics, and it should perhaps be emphasized that the dis- crediting of logical atomism in the domain of ordinary language has done nothing to diminish its relevance to theoretical cosmology; but the pleasures of matchmaking in this area must be deferred, if not now left to others.

背景

第二次世界大战即将结束时，我在海军部的雷达研究机构工作，试图追踪电脉冲在极短时间内的行为。不可避免地，我遇到了测量精度上的基本物理限制。通常，这些限制以互补的方式相关，一个限制的放宽往往意味着另一个限制的收紧。例如，提高时间分辨率通常会降低频率分辨率；提高信噪比往往意味着降低时间分辨率，等等。物理测量的艺术最终似乎就是在这些互相制约的不确定性之间进行妥协。我发现这种情况与原子物理学中海森堡著名的「不确定性原理」有相似之处。该原理指出，粒子的动量（p）和位置（g）永远不能同时被精确定义。动量的不确定度（Δp）越小，位置的不确定度（Δg）就越大，反之亦然。事实上，Δp 和 Δg 的乘积永远不能小于普朗克常数 h，即「作用量子」。作用（能量 × 时间）因此成为基本的物理量，其「原子性」构成了海森堡原理所表达的妥协关系的基础。

很自然地想到问，如果将我在实验测量中遇到的各种折中关系中的互为倒数的量相乘会发生什么。也许这些也可能反映某种基本的「量子」的不变性。但是，究竟是什么的量子呢？我暂时称之为信息量子。然而，当我将提到的不确定性限度的共轭对偶相乘时，我发现它们形成的不是一种，而是两种不同类型的不变结果。在一组中，结果是一个数量级为 1 的无量纲数。在另一组中，它是具有物理熵维度的小量。每一个都代表实验中不可简化的限制因素，一种比其乘积的两个「不确定性」更基本的「量子」。

那么，是什么区分了这两组呢？结果很简单。第一组限制，形成无量纲产物的限制，可以先验地（无需参考实际测量）从仪器的规格计算出来。第二组，形成具有熵维度产物的限制，只能事后从仪器的使用规范计算出来。

这是在 1945/1946 年间。1946 年秋天，我搬到了伦敦的国王学院教授物理学。有一位同事听了我的想法后，建议我的「信息量子」可能与维特根斯坦在其著名的《逻辑哲学论》中提出的「原子命题」有关。虽然维特根斯坦在普通语言分析中已经否定了《逻辑哲学论》的原子主义方法，但科学测量领域似乎很适合按这种思路进行逻辑处理；因为它理想上是建立在 Eddington 所称的指针与刻度之间的「重合关系」和「占据关系」之上的简单断言基础上。不管怎样，探索我在实验中偶然发现的信息量子的「量子化」是否与这些理想陈述的逻辑原子性有关，显得很有价值。通过分析科学陈述的逻辑要求，有可能找到这两种「量子」之间的合理联系吗？

如本卷稍后所述，测量可以被视为一个过程，在这个过程中，每个基本物理事件（每个事件都有某种最低限度的重要性）被分类到不同的类别中，从而以某种精度描绘出特定形式（例如，摄影板上的图像或示波器上的波形）。原则上，每个基本事件都可以在最终物理术语的逻辑框架中增加一个「原子事实」。例如，当观察被推到物理极限时，可以认为仪器的热力学平衡被扰动到可以用物理熵单位测量的程度。每个这样的单位可以被视为抽象表示所发生事件的基本构件，这些构件分布在仪器提供的不同类别或自由度中，就像直方图中的单位事件分布在不同列中一样。因此，可以通过有多少基本事件被逻辑上充分的结果陈述中的原子事实所表示的比例来估计测量的「信息效率」。

这里可能是解释我所说的两种「量子」含义的线索。从这个角度看，科学表示的「大小」可以通过两种互补方式来确定：(a）枚举其自由度，和（b）枚举其基本事实。相应地，一个表示可以通过两种互补方式扩展：(a）增加其自由度或「逻辑维度」（即逻辑上可区分的类别的数量）；(b）增加其基本事实总数或「证据权重」（即代表的基本事件数量）。经过分析发现，物理测量中出现的两种量子极限实际上只是以最低物理成本增加一个单位表示的方式。因此，可以从任一角度谈论「信息单位」，它是「验证表示结果的逻辑形式的一个基本增加」；但在第一种情况下，每个单位增加一个额外的维度（概念类别），而在第二种情况下，每个单位增加一个额外的基本事实。为了避免混淆，我们将第一种称为「结构单位」，第二种称为「测量单位」。

很快就发现，测量信息的概念并不新鲜。1946 年，Dennis Gabor 在英国 Rugby 的 B.T.H. 公司工作时，发表了他的经典论文《通信理论》(Theory of Communication）[6]。在这篇论文中，他将波动力学中使用的 Fourier 变换理论应用于通信工程的频率-时间（f.t）域，并提出一个占据 Af.At 单位面积的信号可以被视为一个「信息单位」，他称之为「logon」。更早在 1935 年，统计学家 R.A. Fisher 提出了统计样本中「信息」的度量方法，在最简单情形下，这相当于方差的倒数（见附录）。最初接触这些不同概念时，很难看出它们能否整合到同一个框架中；但仔细思考后发现，它们实际上是「结构」和「度量」度量的例子。Gabor 的 logon，每个占据 f.t 平面中的面积 Af.At，代表了通信信号的逻辑维度。它们与显微镜焦平面或雷达天线焦平面中占据类似初级面积（艾里圆盘）的「结构单元」属于同一类。因此，在 Gabor 的认可下，将「logon 内容」一词赋予更广泛的定义，作为任何形式（无论是空间还是时间）表示的逻辑维度度量。

Fisher 的度量对于平均样本是可加的，可以简单地解释为「证据重量」的指标。如果我们（任意但合理地）定义度量信息单位或量子（称为「metron」）为赋予相应命题的概率的证据重量，那么 Fisher 的「信息量」就等同于证据提供的这些单位数量的总和。

Gabor 和 Fisher 的信息度量并不是该领域中唯一的候选者。1948 年，C.E. Shannon 发表了他的《通信的数学理论》31，该理论为通信信号提出了一种基于信号统计不可能性的度量。由于不可能性的对数对于独立信号是可加的，这显然具有吸引力。问题在于它如何与已经存在的「结构性」和「度量」度量联系起来。自然地，在四十年代后期，普遍倾向于将所有这些度量视为竞争同一个称号的对手，或者提出不同概念的「信息」。另一个问题是，「意义」的概念是否在整个框架中有适用的地方。Shannon 对信号中「信息量」的分析明确表示不关心其意义，这被广泛误解为工程师们定义了一种完全与意义无关的信息概念。

当我鼓起足够勇气在这个主题上发表一些内容时 12，可能的综合轮廓已经开始浮现，并在 1950 年我们首次伦敦信息理论研讨会的论文 23 中进行了试验。尽管这些早期探索的某些方面可能仅具有历史意义，但本合集的附录中重印了一些样本。

回顾这些二十年前的推测，最引人注意的是那些模糊感知的发展方向，虽然并不是所有都没有希望，但却从未被进一步探索。主要的原因是我被信息理论和电子计算结合的新方向所吸引。如果信息概念包含结构和度量两个方面，那么，什么样的计算机制最适合处理各种信息变换呢？特别是，人类大脑是如何处理信息的？

在本合集的伴随卷中会出现一些尝试解决这些问题的方法。我现在提到这些问题，是因为到 1950 年底，研究最复杂的计算机制已经成为我的主要兴趣。1951 年我在美国与神经生理学家共度的一年，完成了这一研究转变的过程；无论好坏，我在「纯」信息理论领域的大部分未成熟的想法都被搁置了。

本卷中的大部分论文都是在这一研究重点变化之后写的，主要关注信息在大脑中的表示和利用以及人类之间的信息交换，而不是形式化为基本命题的逻辑模式。我仍然希望能在基础物理学中找到物理和逻辑原子论之间的有益联系，尽管逻辑原子论在普通语言领域的失效并没有减少其在理论宇宙学中的相关性；不过，探索这个领域的乐趣可能需要推迟，或者留给其他人。

