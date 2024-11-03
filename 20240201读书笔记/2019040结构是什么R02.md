## 记忆时间

## 目录

0401 Designing for safety

0501 Strain energy and modern fracture mechanics

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

## 0501. Strain energy and modern fracture mechanics

— with a digression on bows, catapults and kangaroos

An unwise man doth not well consider this: and a fool doth not understand it. (Psalm 92)

As we said in the last chapter, it was the considerable achievement of the nineteenth-century mathematicians to find ways of calculating the distribution and the magnitude of the stresses in most kinds of structures in a rather broad, generalized or academic way. However, many practical engineers had not long come to terms with calculations of this kind before Inglis planted the seeds of doubt at the back of their minds. Using the elasticians' own algebraical methods, he pointed out that the existence of even a tiny unexpected defect or irregularity in an apparently safe structure would be able to cause an increase of local stress which might be greater than the accepted breaking stress of the material and so might be expected to cause the structure to break prematurely.

In fact, using Inglis's formula (p. 67), it is easy to calculate that, if you were to scratch a girder of the Forth railway bridge, moderately hard, with an ordinary sharp pin, the resulting stress concentration should be sufficient to cause the bridge to break and fall into the sea. Not only do bridges seldom fall down when they are scratched with pins, but all practical structures such as machinery and ships and aeroplanes are infested with stress concentrations caused by holes and cracks and notches which, in real life, are only rarely dangerous. In fact they generally do no harm at all. Every now and then, however, the structure does break; in which case there may be a very serious accident.

When the implications of Inglis's sums began to dawn upon engineers some fifty or sixty years ago, they were apt to dismiss the whole problem by invoking the 'ductility' of the metals which they were accustomed to use. Most ductile metals have a stress-strain curve which is shaped something like Figure 9, and it was commonly said that the overstressed metal at the tip of a crack simply flowed in a plastic sort of way and so relieved itself of any serious excess of stress. Thus, in effect, the sharp tip of the crack could be considered as 'rounded off' so that the stress concentration was reduced and safety was restored.

Like many official explanations, this one has the merit of being at least partly true, though in reality it is very far from being the whole story. In many cases the stress concentration is by no means fully relieved by the ductility of the metal, and the local stress does, in fact, quite often remain much higher than the commonly accepted 'breaking stress' of the material as determined from small specimens in the laboratory and incorporated in printed tables and reference books.

For many years, however, embarrassing speculations which were likely to undermine peoples' faith in the established methods of calculating the strength of structures were not encouraged. When I was a student Inglis's name was hardly ever mentioned and these doubts and difficulties were not much spoken about in polite engineering society. Pragmatically, this attitude could be partially justified, since, given a judiciously chosen factor of safety, the traditional approach to strength calculations – which virtually ignores stress concentrations – could generally be relied upon to predict the strength of most conventional metal structures. In fact it forms the basis of nearly all of the safety regulations which are imposed by governments and insurance companies today.

However, even in the best engineering circles, scandals occurred from time to time. In 1928, for instance, the White Star liner Majestic of 56,551 tons, which was then the largest and finest ship in the world, had an additional passenger lift installed. In the process rectangular holes, with sharp corners, were cut through several of the ship's strength decks. Somewhere between New York and Southampton, when the ship was carrying nearly 3,000 people, a crack started from one of these lift openings, ran to the rail, and proceeded down the side of the ship for many feet before it was stopped, fortuitously, by running into a port-hole. The liner reached Southampton safely and neither the passengers nor the press were told. By an extraordinary coincidence, very much the same thing happened to the second largest ship in the world, the American transatlantic liner Leviathan, at about the same time. Again the ship got safely into port and publicity was avoided. If the cracks had run a little further, so that these ships had actually broken in two at sea, the loss of life might have been severe.

Really spectacular accidents of this kind to large structures such as ships and bridges and oil-rigs became common only during and after the last war, and latterly they have been growing more, and not less, frequent. What has emerged rather painfully over a number of years – at a vast cost in life and property – is that, although the traditional view of elasticity as hammered out by Hooke and Young and Navier and by scores of nineteenth-century mathematicians is extremely useful and certainly ought not to be neglected or spurned, yet it is not really enough, by itself, to predict the failure of structures – especially large ones -with sufficient certainty.

如何同裂缝和应力集中共存 —— 弓、投石机和袋鼠

不智者不思虑之，愚顽者不了然之。

——《圣经·旧约全书·诗篇》（Psalm 92）

上一章我们说到，19 世纪的数学家取得的一项重大成就是，找到一种相当普适、一般化或学术化的方法，来计算大部分材料中的应力分布与大小。然而，在很多一线工程师接受这种计算方法后没多久，英格利斯就在他们心中播下了怀疑的种子。借助弹性研究者的代数化方法，他指出，在看似安全的材料中，即便存在微小的意外缺陷或不规则，也能导致局部应力的增长，一旦超过材料所能承受的断裂应力，就会导致材料断裂。

事实上，用英格利斯公式很容易算出，若用稍硬的普通尖钉去划福斯铁路桥的主梁，造成的应力集中足以导致这座桥断裂并坠入海中。但实际上，桥梁被钉子划后很少坍塌，而且所有像机械、船舶和飞机这样的实用结构，都不乏孔洞、裂缝和沟槽导致的应力集中，而它们在现实生活中很少发生危险。实际上，这些缺陷通常是完全无害的。只是，这些结构一旦发生断裂，就是非常严重的事故。

大约五六十年前，当工程师开始理解英格利斯公式的含义时，他们倾向于援引惯用的金属「延展性」来解决整个难题。大部分可延展金属的「应力–应变」曲线类似于图 5–9 所示，通俗地讲，在应力作用下金属裂缝尖端的流动方式与塑料类似，可缓解自身需承受的严重超量的应力。因此，裂缝尖端可被「四舍五入」，应力集中因此减少，而安全性得以恢复。

就像许多冠冕堂皇的解释一样，这种解释至少是部分正确的，尽管在现实中它远非故事的全部。在很多情境中，金属的延展性无法完全消除应力集中，局部应力远高于被普遍接受的材料的「断裂应力」，后者来自实验室中的小型样品，且被收录在印制的表格和工具书里。

然而多年来，令人尴尬的猜测并不受欢迎，它可能会打击人们对材料强度现有计算方法的信心。当我还是个学生时，英格利斯的名字几乎无人提及，满是客套话的工程领域也极少聊到这些疑虑和困难。说实话，这种态度也有其道理，因为既然有了审慎选择的安全系数，大部分常见金属结构的强度就都可以用传统办法估计，虽然它无形中忽略了应力集中。事实上，这种方法也是今天几乎所有政府和保险公司的强制性安全规章的基础。

但是，即使在最出色的工程领域，丑闻也时有发生。例如，1928 年竣工的排水量 56 551 吨的英国白星航运公司的雄伟号邮轮是当时世界上最大、最豪华的轮船，配备了专门的旅客电梯。在安装电梯的过程中，带尖锐边角的矩形孔穿透了船的几层强力甲板。当船行驶至纽约和南安普顿之间的某处时（当时船上载有近 3 000 人），一条裂缝从一部电梯的开口处延伸到栏杆处，又顺着船舷向下延伸了数英尺（1 英尺≈0.3 米），连接上一个孔道。这艘邮轮最终安全抵达南安普顿，无论乘客还是媒体都对此毫不知情。巧合的是，同样的事情几乎同时间也发生在世界第二大轮船 —— 美国跨大西洋邮轮利维坦号 —— 上。再一次，轮船安全抵港，而公众却被蒙在鼓里。如果裂缝延伸得再远一些，导致船在海上断成两截，那么人员伤亡可能会非常严重。

对船舶、桥梁和石油钻台等大型结构而言，这类惊人的事故的确只在「二战」以后才变得普遍，近年来它们越发频繁，而非越发罕见。多年来令人痛苦的悲剧 —— 生命和财产损失巨大 —— 频发，虽然胡克、托马斯·杨、纳维叶以及很多 19 世纪的数学家阐明的传统弹性理论非常有用且不应被忽视或唾弃，但其本身还不足以精确预测结构的失效，尤其是对大型结构而言。

### 5.1 The approach to structures through the concept of energy

I saw the different things you did,

But always you yourself you hid.

I felt you push, I heard you call,

I could not see yourself at alL.

R. L. Stevenson, A Child*s Garden of Verses

Until fairly recently elasticity was studied and taught in terms of stresses and strains and strength and stiffness, that is to say, essentially in terms of forces and distances. This is the way in which we have been considering it so far, and indeed I suppose that most of us find it easiest to think about the subject in this manner. However, the more one sees of Nature and technology, the more one comes to look at things in terms of energy. Such a way of thinking can be very revealing, and it is the basis of the modern approaches to the strength of materials and the behaviour of structures; that is, to the rather fashionable science of ' fracture mechanics'. This way of looking at things tells us a great deal, not only about why engineering structures break, but also about all sorts of other goings-on – in history and in biology, for instance.

It is a pity, therefore, that the whole idea of energy has been confused in many people's minds by the way in which the word is often used colloquially. Like 'stress' and 'strain', 'energy' is used to refer to a condition in human beings: in this case one which might be described as an officious tendency to rush about doing things and pestering other people. This use of the word has really only a tenuous connection with the precise, objective, physical quantity with which we are now concerned.

The scientific kind of energy with which we are dealing is officially defined as 'capacity for doing work', and it has the dimensions of 'force-multiplied-by-distance'. So, if you raise a weight of 10 pounds through a height of 5 feet, you will have to do 50 foot-pounds of work, as a result of which 50 foot-pounds of additional energy will be stored in the weight as what is called 'potential energy'. This potential energy is locked up, for the time being, in the system, but it can be released at will by allowing the weight to descend again. In doing so the released energy could be employed in performing 50 foot-pounds' worth of useful tasks, such as driving the mechanism of a clock or breaking the ice on a pond.

Energy can exist in a great variety of different forms – as potential energy, as heat energy, as chemical energy, as electrical energy and so on. In our material world, every single happening or event of whatever kind involves a conversion of energy from one into another of its many forms. In a physical sense that is what 'happenings' or 'events' are about. Such transformations of energy take place only according to certain closely defined rules, the chief of which is that you can't get something for nothing. Energy can neither be created nor destroyed, and so the total amount of energy which is present before and after any physical transaction will not be changed. This principle is called 'the conservation of energy'.

Thus energy may be regarded as the universal currency of the sciences, and we can often follow it through its various transformations by means of a sort of accounting procedure which can be highly informative. To do this, we need to use the right kind of units; and, rather predictably, the traditional units of energy are in a fine, rich state of muddle. Mechanical engineers have tended to use foot-pounds, physicists are addicted to ergs and electron-volts, chemists and dietitians like to use calories, but our gas bills come in therms and our electricity bills in kilowatt-hours. Naturally, all these are mutually convertible, but nowadays there is a good case for using the S I unit of energy, which is the Joule, that is the work done when one Newton acts through one metre.*

Although we can measure it in quite precise ways, many people find energy a more difficult idea to grasp than, say, force or distance. Like the wind in Stevenson's verse we can only apprehend it through its effects. Possibly for this reason the concept of energy came rather late into the scientific world, being introduced in its modern form by Thomas Young in 1807. The conservation of energy was not universally accepted until quite late in the nineteenth century, and it is really only since Einstein and the atom bomb that the enormous importance of energy as a unifying concept and as an underlying reality has been sufficiently appreciated.

There are, of course, a great many ways, chemical, electrical, thermal and so on, of storing energy until it is wanted. If we are going to use a mechanical means then we could use the method we have just been talking about, that is to say, the potential energy of a raised weight. However, this is rather a crude way of storing energy and, in practice, strain energy, the energy of a spring, is generally more useful and it has much more widespread applications in biology and engineering.

It is obvious that energy can be stored in a wound-up spring, but, as Hooke pointed out, official springs are only a special case of the behaviour of any solid when it is loaded. Thus every elastic material which is under stress contains strain energy, and it does not make much difference whether the stress is tensile or compres-sive.

If Hooke's law is obeyed, the stress in a material starts at zero and builds up to a maximum when the material is fully stretched. The strain energy per unit volume in the material will be the shaded area under the stress-strain diagram (Figure 1), which is

Figure 1. Strain energy = area under stress-strain curve = .

用能量解释结构

我看出你玩的花样，

但你总把自己隐藏。

我感受你的推搡，听到你的呼唤，

而你本身，我根本看不见。

—— 史蒂文森（R. L. Stevenson），《童诗园》（A Child's Garden of Verses）

直到最近，我们才用应力、应变、强度和刚度等术语研究和教授有关弹性的知识，也就是说，在本质上用到了力和距离。这就是到目前为止我们考虑该问题的方式，而且事实上，我想大多数人都觉得用这种方式思考该问题是最简单的。但是，人对大自然和工程技术领悟得越多，便越会从能量的角度来看待事物。这种思考方式颇具启发性，它是材料强度和结构行为的现代研究方法 ——「断裂力学」这门流行学科的基础。这种看待事物的方式告诉我们许多东西，不仅关乎工程结构为何会断裂，还关乎其他各种现象，例如历史现象和生物现象。

然而，令人遗憾的是，许多人头脑中关于能量的总体观念是含混不清的，这源于这个词常用的口语表达方式。就像应力和应变，能量一词也常被用来指代人的一种状态：一种风风火火且惹人厌烦的张扬个性。这个词的日常用法与我们现在所说的清晰客观的物理量之间只有一点儿联系。

能量的科学定义是「做功的能力」，用「力乘以距离」表示。因此，如果你将 10 磅的重量抬高 5 英尺，那么你就做了 50 英尺磅 [1] 的功，其结果是重物将获得 50 英尺磅的能量，即「势能」。势能暂时被锁在系统中，但它能通过重物的下降而被释放出来。这样的话，释放出的能量可被用来做 50 英尺磅的有用功，比如，驱动钟表的机械结构或者打破池塘的冰层。

能量会以不同的形式存在，比如势能、内能、化学能、电能等。在我们的材料世界里，一切活动都涉及能量从一种形式向另一种形式的转换。这样的能量转换只在某些严格规则的支配下才会发生，其中的首要规则便是不能无中生有。能量既不能被创造，也不会被消灭，其总量在任何过程的前后保持不变，这被称为「能量守恒定律」。

因此，能量可被视为科学的通货，我们常常可以借助能提供丰富信息的计量手段来追踪它的各种变换。为此，我们需要使用恰当的单位；不出所料，能量的传统单位处于各行其是的混乱状态。机械工程师习惯用英尺磅，物理学家偏爱尔格和电子伏特，化学家和营养学家喜欢用卡路里，天然气缴费账单用的是千卡，电费账单则用千瓦时。所有这些单位都可以互相换算，但国际上能量的通用单位为焦耳，即物体在 1 牛顿力的作用下经过 1 米的距离所做的功。[2]

虽然我们能用相当精确的方法去测量它，但许多人觉得能量是一个比力或距离等更难掌握的概念。就像史蒂文森诗歌里的风，我们只能通过它产生的效应来理解它。可能正是因为这个理由，能量的概念很晚才被引入科学界，其现代形式是托马斯·杨于 1807 年提出的。直到 19 世纪晚期，能量守恒定律才被普遍接受；在爱因斯坦和原子弹发明之后，能量作为一个统一概念和深层事实的极大重要性才得到充分的认可。

当然，在被需要之前，能量有许多存储方式，比如化学能、电能、热能等。如果我们打算运用机械手段，那么我们可以采取刚才说的方法，即提升重物得到势能。但是，这种储能方法相当简陋；在实践中，应变能（弹簧的能量）往往更有用，它在生物学和工程领域有着广泛的应用。

图 5–1 应变能 = 应力–应变曲线下方阴影区域的面积 = (1/2)se

1『原书中的这张图很形象，可以时不时去看看。（2021-06-20）』

显然，能量可以储存在一个绷紧的弹簧中，但正如胡克指出的那样，标准的弹簧只是任意负载固体行为的一个特例。因此，每一种处在应力作用下的弹性材料都有应变能，无论拉伸还是压缩，没有多大区别。

如果遵循胡克定律，材料中的应力将从 0 增加到完全拉伸状态的最大值。材料中单位体积的应变能等于「应力–应变」曲线中阴影区域的面积，即：

$$\frac{1}{2} × 应力 ×  应变 = \frac{1}{2} × s ×  e$$

[1] 1 英尺磅 ≈ 1.36 焦耳。—— 编者注

[2] 1 焦耳 = 107 尔格 ≈ 6.24×10^18 电子伏特 ≈0.738 英尺磅 ≈0.239 卡路里。注意，1 焦耳大约为一个普通苹果从一张普通桌子掉落到地面上释放的能量。

### 5.2 Cars, skiers and kangaroos

We are all of us familiar with strain energy in the springs of our car. In a vehicle with no springs there must be violent interchanges of potential and kinetic energy (energy of motion) every time a wheel passes over a bump. These energy changes are bad for the passengers and bad for the vehicle. Long ago some genius invented the spring, which is simply an energy reservoir which enables changes of potential energy to be stored temporarily as strain energy so as to smooth the ride and prevent the vehicle and its occupants from being racketed to bits.

Latterly engineers have spent a great deal of time and effort on the improvement of car suspensions, and no doubt they have been very clever about it. However, cars and lorries run on roads whose main purpose is, after all, to provide a smooth surface. The suspension of the car has only to even out the minor or residual bumps. The problem of designing a suspension for a car which had to be driven really fast across rough country would be a very difficult one. In order to store enough energy to cope with such a situation the steel springs would have to be very large and heavy and would in themselves constitute so much 'unsprung weight' that the whole project might prove to be impracticable.

Consider now the situation of a skier. In spite of the snow covering, most ski-runs are vastly more bumpy than any normal road. Even if a typical run could be covered with some effective non-skid surface, such as sand, so as to enable a car to go on it without slipping, any attempt to drive the car down the run at the speed of a fast skier – say 50 m.p.h. – would be suicidal, because the suspension would be completely inadequate to absorb the shocks. But, of course, this is exactly what the body of a skier has to do. In fact, much of this energy seems to be absorbed by the tendons in our legs, which, taken together probably weigh less than a pound.* Thus, if we are to ski fast without disaster or to perform other athletic feats, our tendons have to be able to store reliably and to give up again very large amounts of energy. This is partly what they are for.

Some approximate figures for the strain energy storage capabilities of various materials are given in Table 3. The relative efficiencies of natural materials and of metals may come as a surprise to engineers, and some light is thrown on the performance of skiers and other animals by the figures for tendon and steel. It will be seen that the strain energy storage per unit weight is about twenty times higher for tendon than it is for modern spring steels. Although, considered as devices for storing strain energy, skiers are more efficient than most machines, yet even a trained athlete cannot compete with a deer upon a hillside or a squirrel or a monkey in a tree. It might be interesting to know the percentage of the body weight given up to tendon in these animals, as compared with people.

Animals like kangaroos progress by bounding. At each landing, energy has to be stored in the creature's tendons, and I have been told by an Australian correspondent that the strain energy characteristics of kangaroo tendon are exceptionally good; but unfortunately I cannot quote any accurate figures. It occurs to me, however, that, if anyone should wish to revive the pogo-stick in a more efficient form, there would be a good deal to be said for making the spring from kangaroo tendon, or indeed from any form of tendon. Light aircraft, which have to be designed for bad landings on rough ground, often have their undercarriages sprung by means of rubber cords which have a strain energy capacity much better than that of steel springs, and are also better than tendon, though they are less durable.

TABLE 3 Approximate strain energy storage capacities of various solids

Besides its role in the suspensions of cars and aeroplanes and animals, strain energy plays an even more important part in the strength and fracture of all kinds of structures. However, before we pass on to the subject of fracture mechanics it may be worth spending a little time in discussing yet another application of strain energy, that is in weapons such as bows and catapults.

汽车、滑雪者和袋鼠

我们所有人都熟悉汽车弹簧中的应变能。车辆要是没了弹簧，每次车轮碾过路面隆起处时，势能和动能（运动的能量）肯定会剧烈地转化。这些能量转化对乘客和车辆来说都是有害的。很久以前，某位天才发明了弹簧，它不过是一个能量的储存库，能让势能的变化暂时以应变能的形式存储起来，以便行驶平稳，并防止车辆及其乘客被颠得散架。

最近，工程师花了大量时间和精力来改进汽车的减震悬架，毫无疑问，他们在这一点上非常高明。但是，供汽车行驶的道路，其主要作用是提供一个平滑的表面，汽车的悬架只需要缓冲轻微或残余的颠簸即可。为在山区快速行驶的汽车设计减震悬架，才是真正的难题。为了储存足够的能量以应付这种情况，钢制弹簧不得不做得既大又重，而它们本身就充当了很大一部分「簧下重量」，以致整个设计可能最终失败。

现在来考虑一下滑雪者的情况。尽管被雪覆盖，大部分滑雪道还是比任何正常道路都更颠簸。纵然一条典型的跑道可以被砂砾等有效防滑层覆盖，使得汽车能在上面不打滑地行驶，但任何人以速滑者的时速（比如 50 英里 / 小时）驾驶汽车沿滑雪道跑下去都无异于自杀，因为减震悬架根本不足以缓冲这些冲击。但是，这恰恰是滑雪者的躯体需要承受的。事实上，大部分能量似乎都被我们腿部的肌腱吸收了，加起来可能不到 1 磅。[3] 因此，如果我们在安全的前提下速滑或进行其他体育运动，我们的肌腱一定会存储并释放这些巨大的能量。在一定程度上，这也是它们存在的意义。

表 5–1 给出了各种固体材料应变能的存储能力近似值。天然材料和金属的相对储能效率可能会让工程师大吃一惊，滑雪者和其他动物的表现要受肌腱和钢材量值的影响。显然，肌腱单位质量的应变能存储能力约为现代弹簧钢的 20 倍。虽然以存储应变能的装置计，滑雪者比大部分机械都更有效率，但即便是受过训练的运动员也不能与山坡上的鹿、树上的松鼠或猴子相匹敌。相较于人，知道这些动物体内肌腱占体重的百分比可能会很有意思。

像袋鼠这样的动物借助跳跃前进，每次着地，能量就会存储在生物肌腱中。一位澳大利亚记者曾告诉我，袋鼠肌腱的应变能性能特别优良；遗憾的是，我没法引用任何准确的数据。但是，我灵机一动，想到如果任何人想要更有效地恢复弹簧单高跷的流行，用袋鼠肌腱或其他肌腱来制作弹簧，可以说是一个好的选择。轻型飞机的设计需要考虑在崎岖地面上着陆的问题，其起落架的安置通常要借助橡胶绳，尽管不怎么耐用，但橡胶绳的应变能性能远高于钢制弹簧和肌腱。

表 5–1 各种固体材料应变能的存储能力近似值

| 材料种类 | 工作应变（%）| 工作应力（psi）| 工作应力（MN/m2）| 存储的应变能（x10^6 J/m3）| 密度（kg/m3）| 存储的能量（J/Kg）|
| --- | --- | --- | --- | --- | --- | --- |
| 古代铁（Ancient iron） | 0.03 | 10,000 | 70 | 0.01 | 7800 | 1.3 |
| 现代弹簧钢（Modern spring steel） | 0.3 | 100,000 | 700 | 1.0 | 7,800 | 130 |
| 青铜（Bronze） | 0.3 | 60,000 | 400 | 0.6 | 8,700 | 70 |
| 紫衫木（Yew wood） | 0.9 | 18,000 | 120 | 0.5 | 600 | 900 |
| 肌腱（Tendon） | 8.0 | 10,000 | 70 | 2.8 | 1,100 | 2,500 |
| 角质（Horn） | 4.0 | 13,000 | 90 | 1.8 | 1,200 | 1,500 |
| 橡胶（Rubber） | 300 | 1,000 | 7 | 10.0 | 1,200 | 8,000 |

2『固体材料的应变能储存数据做一张信息数据卡片。（2021-06-20）』—— 已完成

除了在汽车减震悬架、飞机和动物中的作用，应变能在各种结构的强度和断裂现象中都扮演了很重要的角色。但是，在我们转入断裂力学这门学问之前，花点儿时间探讨应变能的另一些应用可能也是值得的，比如像弓和投石机这类武器中的应变能。

[3] 因为滑下坡时的人体耗氧量据说比其他任何活动都高，肌肉也必须消耗大量能量。但是，大部分被肌肉吸收的能量不可回收，因此以肌腱来存储弹性应变能无疑是首选。

### 5.3 Bows

I will bring you the great bow of the divine Odysseus, and whosoever shall most easily string the bow with his hands, and shoot through all the twelve axes, with him will I go and forsake this house, this house of my marriage, so beautiful and filled with fair things, which I think I shall yet remember, aye, in a dream.

Penelope, in Homer, Odyssey XXI

The bow is one of the most effective ways of storing the energy of human muscles and releasing it to propel a missile weapon. The English longbow, which did so much execution at Crecy (1346) and Agincourt (1415), was nearly always made from yew. Because yew timber has not much commercial value nowadays, little scientific work was done on it until recently. However, my colleague Dr Henry Blyth, who is doing research on ancient weapons, has ascertained that yew (Taxus baccata) has a fine-scale morphology which is rather different from other timbers and seems to be peculiarly adapted for storing strain energy. Thus yew probably really is better than other woods for making bows.

Contrary to popular belief, English longbows were not, as a rule, made from English yew-trees, whether grown in churchyards or elsewhere. Most English bows were made from Spanish yew and it was legally compulsory to import consignments of Spanish bow-staves with each shipment of Spanish wine. In fact the yew-tree grows well, not only in Spain, but all over the Mediterranean area. It is growing wild today among the ruins of Pompeii for instance. In spite of this, one seldom hears of the use of yew bows in Spain or in the Mediterranean countries, either during the Middle Ages or in antiquity. Their use was almost confined to England and France and, to some extent, Germany and the Low Countries. English depredations generally stopped somewhere around Burgundy and hardly ever spread south of the Alps or the Pyrenees.

Although these facts seem surprising at first sight, Henry Blyth points out that, because of its rather special constitution, the mechanical properties of yew deteriorate more rapidly with increasing temperature than do those of other timbers. A yew bow cannot be used reliably above 35° C. As a weapon it is therefore pretty well confined to cool climates and is unsuitable for use in the Mediterranean summer. Thus, although yew wood was used for arrows, it was seldom used for bows in Mediterranean countries.

For this reason what was called a 'composite' bow was developed in these countries. Such bows had a core of wood which, being near the middle of the thickness of the bow, was only lightly stressed. To this core was glued a tension surface made from dried tendon and a compression face made from horn. Both these materials are even better at storing energy than yew. Furthermore they retain their mechanical properties better than yew in hot weather. After all, an animal normally operates at about 37° C. In practice, tendon does not deteriorate appreciably below about 55° C. As against this, dried tendon slackens and behaves badly in damp weather.

Composite bows of this kind were used both in Turkey and elsewhere down to comparatively recent times. Lord Aberdeen (1784-1860), travelling to the Congress of Vienna in 1813, wrote of the use of Tartar troops, armed with what seem to have been composite bows, against the armies of Napoleon which were retreating through eastern Europe. There is a good deal of evidence that composite bows were better in many respects than the English longbow. However, whereas the longbow was essentially a cheap and simple weapon to manufacture, the composite bow was a much more sophisticated affair, and presumably expensive. Greek bows were composite bows, and the bow of Odysseus, like that of Philoctetes, seems to have been a pretty special job.

Which brings us back to the unfortunate Penelope and the task she set her suitors of stringing the bow of Odysseus. As we all know, this turned out to be beyond the strength of any of them, even the technically-minded Eurymachus: 'And now Eurymachus was handling the bow, warming it on this side and on that before the heat of the fire; yet even so he could not string it, and in his great heart he groaned mightily.' But after all, why bother? Why didn't the suitors, or Odysseus, or anybody else, just use a longer string?

The answer to this is 'for a very good scientific reason' – which is as follows. The energy which a man can put into a bow is limited by the characteristics of the human body. In practice, one can draw an arrow back about 0-6 metres (24 inches), and even a strong man cannot pull on the string with a force of more than about 350 Newtons (80 lb.). It follows that the available muscular energy must be around 0-6 metre × 350 Newtons, or about 210 Joules. This is the most that is available, and we want to store as much of it as possible as strain energy in the bow.

If we suppose that the bow is initially virtually unstressed and that the string is almost slack to begin with, then the archer starts to draw his arrow with a pull which is initially nearly zero, and he only works up to his greatest pull when the string reaches its maximum extension. This is expressed diagrammatically in Figure 2. In such a case, the energy put into the bow is the area of the triangle ABC, which cannot be more than half of the available energy, i.e. 105 Joules.

In practice the measured energy which was stored in an English longbow was a little less than this figure. However, Homer specifically says that the bow of Odysseus waspalintonos, that is, 'bent or stretched backwards'. In other words the bow was initially bent in the opposite or 'wrong' direction, so that considerable forced had to be applied to it before it could be strung.

Figure 2. Energy stored in bow = ½ × 0·6 × 350 = 105 Joules.*

When we bow is strung in this way the archer is no longer starting to draw the bow from an initial condition of zero stress and strain; and, by intelligent design, it is now possible to arrange for the force-extension diagram to look something like Figure 4.

Figure 3. Greek stringing bow (vase painting).

Figure 4. Why a bow is 'stretched backwards' orpalintonos. Energy stored in bow is now area A B C D ≈ 170 Joules.

The area A BCD under such a diagram is now a very much higher fraction of the total available -energy and might perhaps reach about 80 per cent of it. So it is possible that about 170 Joules of energy can now be stored in the bow, as against only about 105 Joules for the bow that is not palintonos. This is clearly a great improvement for the archer – quite apart from any advantage it might have had for Penelope.

In fact all bows are more or less pre-stressed, in the sense that some kind of effort is needed to string them. However, since the longbow is a 'self-bow', that is to say, it is made from a stave which has been split from a log of timber and is therefore initially nearly straight, the effect in this case was small. It is much easier to arrange for the best initial shape with a composite bow, and these had usually a very characteristic form, from which we get the shape of a 'Cupid's bow' (Figure 5).

Because the strain energy storage of horn and tendon, as materials, is better than that of yew, a composite bow can be made shorter and lighter than a wooden one. This is why we talk of a wooden bow as a 'long' bow. The composite bow could be made small enough to be used on horseback, as was indeed done by the Parthians and the Tartars. The Parthian bow was handy enough for the cavalrymen to be able to shoot backwards, as they retreated, at their Roman pursuers; from this we get the phrase 'a Parthian shot'.

Figure 5. Composite bow, unstrung and strung.

弓

我会把神圣的奥德修斯的大弓给你，无论是谁，只要能赤手为此弓上弦，射穿全部 12 个斧头，我就同他远走，舍弃这宫殿。我守护着婚姻的宫殿，它如此美丽，满室珍宝，我想我还是会记得它，是的，在梦里。

—— 荷马，《奥德赛》（Odyssey XXI）

弓是储存人体肌肉能量并释放该能量以驱动可投掷武器的最有效方式之一。英格兰长弓曾在克雷西战役（Crecy, 1346）和阿金库尔战役（Agincourt, 1415）中杀敌无数，它主要是用紫杉木制成的。因为紫杉木料今天已没有多少商业价值了，所以直到不久前，对它的科学研究还寥寥无几。然而，我的同事亨利·布莱思（Henry Blyth）博士正在研究古代兵器，他已弄清紫杉木具有精细尺度的形态学结构，与其他木料不同，它似乎特别适合存储应变能。因此，紫杉木可能的确比其他木材更适合用来制作弓。

与大众的印象相反，英格兰长弓通常并不是用在教堂墓地或别处生长的英格兰紫杉制作的。大部分英格兰长弓使用的是西班牙紫杉，西班牙制弓木料随西班牙葡萄酒进口是一种法定义务。事实上，优质的紫杉树不只生长在西班牙，整个地中海沿岸都遍布这种植物。例如，在今日庞贝古城的废墟中，紫杉正肆意生长着。尽管如此，无论是在中世纪还是古典时代，几乎没听说过西班牙或地中海沿岸国家使用紫杉木弓。这种弓的使用几乎仅限于英国和法国，在某种程度上，还包括德国和一些低地国家。英国人的劫掠范围通常止于勃艮第附近，几乎从未延伸到阿尔卑斯山或比利牛斯山以南地区。

虽然这些事实乍看之下似乎令人惊讶，但亨利·布莱思指出，因其相当特殊的构造，随着温度的升高，紫杉的机械性能比其他木材的机械性能退化得更快。一张紫杉木弓在 35 摄氏度以上就无法保持其可靠性了。作为一种武器，它因此仅适用于气候凉爽的环境，而不适宜在地中海地区的夏季使用。所以，紫杉木在地中海沿岸国家只会被用作箭杆，而罕被用作弓。

于是，复合弓便在这些国家发展起来。这种弓有一个木芯，位于弓最粗的中间部分，应力较小。木芯的外侧和内侧分别粘着一个由干燥肌腱制成的承张面和一个用角质做的承压面。这两种材料比紫杉更擅长储存能量。此外，在炎热的天气里，它们也能比紫杉更好地保持机械性能。毕竟，动物正常活动时的温度就在 37 摄氏度左右。在实践中，肌腱性能在 55 摄氏度以下都不会有明显的退化。相反，干燥肌腱在潮湿天气里会变得松弛，表现糟糕。

这种复合弓在土耳其和其他地方一直用到了相对晚近的时代。阿伯丁勋爵（Lord Aberdeen）1813 年出席维也纳会议时，曾记录过鞑靼军团装备了复合弓用以对抗经东欧撤退的拿破仑军队。大量证据表明，复合弓在很多方面皆优于英格兰长弓。但是，长弓本质上是一种廉价且做工简单的武器，而复合弓做起来则要复杂得多，想必价格不菲。希腊弓属于复合弓，而奥德修斯之弓就像菲罗克忒忒斯的弓一样，似乎是鬼斧神工之作。

让我们回到不幸的珀涅罗珀以及她为求亲者设置的为奥德修斯之弓上弦的挑战上来。众所周知，所有人都无能为力，即便是工于巧思的欧律马库斯：「现在欧律马库斯手握着弓，在火盆前反复烘烤它；但纵然如此，他也无法为之上弦，不免由衷叹息。」但是，何苦这么麻烦呢？这些求亲者、奥德修斯或其他人，为什么不找条更长的弓弦？

答案是「因为一个绝佳的科学理由」，如下所述。一个人能用于引弓的能量受制于其肌体特征。在实践中，人可以把箭矢朝后拉约 0.6 米（约合 24 英寸），即便是一个壮汉来拉弓弦，也没法使出超过 350 牛顿（约合 80 磅力）的力。由此可知，可用的肌肉能量一定约是 0.6 米 × 350 牛顿，约为 210 焦耳。这是可用能量的最大值，我们要尽可能多地将之储存于弓的应变能中。

我们假定弓最初是无应力的，弓弦开始几乎是松弛的，然后弓箭手用初始值几乎为零的力拉弓搭箭，只有当弓弦达到最大的伸长量时，他的拉力才会达到最大。图 5–2 形象地展示了这一点。在这种情境中，施予弓的能量为三角形 ABC 的面积，不超过可用能量的一半，即 105 焦耳。

在实践中，储存在英格兰长弓中的实测能量比图中的能量略低。但是，荷马曾说过，奥德修斯之弓是「向后弯曲或伸展的」。换言之，这种弓最初是朝相反或倒的方向弯曲的，以至于必须施加相当大的力才能给它上弦。

用这种方法给弓上弦时，弓箭手不再从应力和应变为零的初始状态开始拉弓。借助这种高明的设计，现在可以把力的拉伸图画成如图 5–4 所示的样子；图中 ABCD 区域的面积占总可用能量的比例要更高，可能会达到 80% 左右。所以，现在可能有约 170 焦耳的能量被存储在弓中，而不只是非反曲弓的 105 焦耳。这对弓箭手来说显然是一个重大改进，更不用说对珀涅罗珀的好处了。

图 5–2 弓中储存的能 = (1/2)×0.6×350=105 焦耳 [4]

图 5–3 希腊人给弓上弦（古希腊瓶饰画）

图 5–4 一张弓为什么要「向后伸展」。储存在弓中的能量为 ABCD 区域的面积，约为 170 焦耳

2『弓能储存的应变能数值，做一张信息数据卡片。（2021-06-20）』—— 已完成

事实上，所有弓或多或少都是有预应力的，其意义在于需要费些劲儿才能给它们上弦。但是，长弓属于「单弓」，即它是用一块制弓木料做成的；制弓木料是从一根原木上切割下来的，最初几乎是直的，在这种情况下预应力的效应会很小。用复合弓来设置最佳初始形状要容易得多，它们通常有非常独特的形状，「丘比特弓」（图 5–5）的形状就由此而来。

图 5–5 未上弦和已上弦的复合弓

因为角质和肌腱材料的应变能存储性能要优于紫杉木，所以复合弓比纯木制弓做得更短，也更轻。正因如此，我们把纯木制弓叫作长弓。复合弓可以小到便于人们在马背上使用，比如帕提亚人和鞑靼人做的弓。帕提亚弓很方便，允许骑兵在撤退时向后射击罗马追兵，「帕提亚射法」这个习语便由此而来。

[4] 当然，图 5–2 和图 5–4 只是示意图。拉力图一般不会是直线，但适用的原理都一样。

[5] 但弩的射速比不上手弓。例如，英格兰长弓每分钟可以射出 14 支箭，若集体使用，可形成非常可怕的箭云或箭幕。据计算，在阿金库尔战役中，约有 600 万支箭被射出。

### 5.4 Catapults

The greatest period of classical Greece came to an end when Athens fell in 404 B.C., and during the fourth century the Greek democratic governments declined and were superseded by dictatorships or 'tyrannies', which may have been more effective militarily, politically and economically. Both ashore and afloat the technology of warfare was changing, and the new rulers considered that there was a need for more modern and more mechanized weapons. Moreover, as the absolute masters of increasingly prosperous states, the dictators could well afford to pay the bills.

Development began in Greek Sicily. Dionysius I was a remarkable man who had risen from being a petty clerk in a government office to become Tyrant of Syracuse. During most of his reign, which lasted from 405 to 367 B.C., he made his country the leading power in Europe. As a part of his military programme he founded what was probably the first government research laboratory for weaponry, and for this establishment he recruited the best mathematicians and the best craftsmen from all over the Greek world.

The natural starting point for Dionysius's experts was the traditional composite hand-bow. If one mounts such a bow upon some kind of stock and arranges to draw the string by means of mechanical gearing or levers, then the bow itself can be made much stiffer and so be enabled to store and deliver several times as much energy. Thus we arrive at the cross-bow, whose missile can generally penetrate any practicable thickness of body-armour.* The cross-bow has remained in use, with only minor variations, down to the present time. It is said to be in use in Ulster today. However, it is curious that, as a weapon, it never seems to have played any really decisive military role.

Furthermore, the cross-bow is essentially an infantry or antipersonnel weapon and it never fulfilled the requirement for a weapon which could do worthwhile damage to the hulls of ships or to fixed fortifications. Although the Syracusans enlarged the cross-bow type of catapult and put it on a proper mounting, like a gun-mounting, there seem to be certain physical limitations to this line of development, and catapults of the bow type do not seem ever to have been powerful enough to breach the heavy masonry of fortresses.†

The next step was therefore to abandon the bow type of construction and to store the strain energy in twisted skeins of tendon,‡ much like the skeins of rubber cord which are used to drive model aeroplanes. In such a skein all the cords, that is, the whole of the tendon material, are being stretched in tension as the skein is twisted, so that as an energy storage device it is very effective indeed.

There are various ways in which skeins of tendon rope can be used in weaponry, but by far the best was the device known to the Greeks as the palintonon and to the Romans as the ballista. In this very lethal piece of artillery there were two vertical tendon springs, each of them twisted by means of a rigid arm or lever, something like a capstan bar (Figure 6). The ends of these two arms were joined by a heavy bowstring, and the whole device worked much after the fashion of a bow. Indeed it got its Greek name from the fact that, in their relaxed position, the two arms point forward, like the arms of a composite bow; and the catapult was strung (by means of a powerful winch) in much the same way as a bow. The missile, which was often a stone ball, was propelled down a track which also served to mount the windlass that was needed to operate the weapon, whose draw force might be as high as a hundred tons.

Figure 6. A sketch of what original Greek catapults may have looked like.

The Romans copied the Greek catapults and Vitruvius, who was an artillery officer under Julius Caesar, has left us a handbook on ballistae which makes interesting reading. These weapons were made in sizes which ranged from one throwing a 5 lb. (2 kg) missile to one throwing a 360 lb. (150 kg) one. The effective range of all sizes was about a quarter of a mile or 400 metres. The standard Roman siege ballista seems to have been one throwing a 90 lb. (40 kg) ball.

At the final, dramatic, siege of Carthage in 146 b.c. the Romans filled in part of the shallow lagoon which lies against the city wall and proceeded to breach the defences with catapults. Archaeologists have recovered no fewer than 6,000 stone balls, weighing 90 lb. each, from the site.

Although ship-mounted catapults were used by both Julius Caesar and Claudius to clear the beaches of ancient Britons during their assault-landings on this island, the catapult never became a really dangerous ship-to-ship weapon. It seems likely that a ballista big enough to sink a ship with a single shot would have had a rate of shooting too slow for it to have had much chance of hitting a moving vessel.

Catapults sometimes threw incendiary missiles, but fires could generally be put out quite easily in simple ships which were full of men. One ingenious admiral won a sea-battle in 184 B.C. by shooting at the enemy brittle pots filled with poisonous snakes, but this lead does not seem to have been followed up. On the whole, catapults were not a success at sea.

Nevertheless, the palintonon or ballista was a most effective device for land warfare, although its construction and maintenance were a very sophisticated business indeed, and the Roman artillery officers and N.C.O.s must have been highly competent people. With the passing of the Roman Empire and of Roman technology such weapons became impracticable and were forgotten.* Medieval siege-warfare was reduced to using the weight-catapult or 'trebuchet'.

This was a pendulum-like device using the potential energy of a raised weight. Even a large trebuchet was unlikely to involve raising more than say a ton (10,000 Newtons) through about 10 feet (3 metres). Thus the greatest potential energy stored probably did not much exceed 30,000 Joules. The same amount of strain energy could be stored in ten or twelve kilograms of tendon. Thus even a big trebuchet probably disposed of only about a tenth of the energy of the palintonon. Furthermore the efficiency of energy conversion seems to have been much lower. At its best the trebuchet could probably only make a nuisance of itself by lobbing big stones over a fortress wall; any assault upon heavy masonry would have been ineffectual.

Figure 7. The trebuchet or medieval weight-catapult – a most inefficient contrivance.

Regarded as machines for the conversion of energy, the bow and the palintonon both work on similar principles; it is not generally realized just how efficient an energy exchange mechanism is involved. In crude machines like the trebuchet, most of the energy which was available when the weapon was discharged went into accelerating the heavy lever or throwing-arm of the device and was ultimately lost in the necessary stop or braking system.

With a bow or a palintonon, when the bowstring is first released, some of the stored strain energy is communicated directly to the missile as kinetic energy. More of the available energy, however, is being used to accelerate the arms of the bow or the catapult, where it is temporarily stored as kinetic energy, much as it is in the trebuchet. In this case, though, as the discharge mechanism proceeds, the moving arms are slowed down, not by a fixed stop, but by the bowstring itself as it straightens and tautens. This further increases the tension in the string, enabling it to push yet harder on the missile and so speed it on its way. Thus, much of the kinetic energy stored in the arms is recovered.

Figure 8. Diagram of the mechanism of the palintonon or ballista.

(a) Ready to shoot. All the energy is stored in the tendon springs.

(b) Early stage of shooting operation. Heavy arms are being accelerated and so pick up much of the energy from the springs.

(c) Late stage of shooting operation. Heavy arms are being decelerated by increased tension in the string, and so their kinetic energy is transferred to the missile.

(d) Missile on its way, containing virtually all the energy which was stored in the system.

The mathematics of bows and catapults is difficult and, even when one has written down the equations of motion, they cannot be solved analytically. Fortunately, however, another colleague of mine, Dr Tony Pretlove, has been sufficiently interested in the problem to put the whole thing on a computer. It transpires that, rather surprisingly, the energy transfer process is in theory virtually 100 per cent efficient. In other words, practically the whole of the strain energy which was stored in the device can be converted into the kinetic energy of the missile. Therefore little energy is wasted or left behind to provide a recoil or to damage the weapon. In this respect, at least, bows and catapults are a great improvement on guns.

One consequence of these facts is, I think, fairly well known to most archers, at least in a practical sort of way. This is that one must never, never, never 'shoot' a bow or a catapult without a proper arrow or other appropriate missile. If this is attempted, then there is no safe way of getting rid of the stored strain energy, and, not only may the bow be broken, but the archer will very possibly be hurt as well.

投石机

古希腊最伟大的古典时代随着公元前 404 年雅典的陷落而落幕，公元前 4 世纪，雅典民选政府衰落，渐被独裁政权或「僭主暴政」所取代，后者在军事、政治和经济上或许更有效率。陆上和海上的作战技术也随之发生变化，新的统治者认为需要更新式和更机械化的武器。此外，作为日益富庶的城邦的绝对权威，独裁者完全负担得起这些开销。

希腊化的西西里开始崛起。狄奥尼西乌斯一世（Dionysius I）是个非凡之人，他从一个政府机构的小职员跃升为叙拉古的僭主。在其统治的大部分时间（前 405 年 — 前 367 年）里，他将自己的国家打造为欧洲的霸主。作为他军事计划的一部分，他创立了可能是世界上第一个官办的武器研究室，并为此从整个希腊世界招募来最好的学者和工匠。

对狄奥尼西乌斯的专家来说，传统的手弓是天然的起点。如果有人把这样的弓安在某种木制主干上，设法用机械传动装置或杠杆来拉弓弦，弓就会变得更强并因此储存和传递数倍之多的能量。由此我们得到了弩，其发射的弩箭一般能穿透任何实用护甲的厚度。[5] 直到现在，弩仍在使用，只是有些微小的变化。据说，如今乌尔斯特地区还在用它。但令人好奇的是，作为一种武器，它似乎从未真正起到任何决定性的军事作用。

此外，虽然弩本质上是一种步兵武器或杀伤性武器，但它从未达到对船体或固定防御工事造成有价值的伤害的要求。虽然叙拉古人造出了弓弩型投石机并把它像火炮一样架设起来，但是这条发展路线似乎受到某些物理限制，它似乎并未强大到足以攻破坚固的砌筑堡垒的程度。[6]

因此，下一步是放弃弓弩型构造并将应变能存储于缠绕的腱绳束中，[7] 后者很像用于驱动飞机模型的橡皮绳束。这样一束绳条，即整个腱绳束，在缠绕状态下被拉伸，使得它作为一种能量储存装置的确非常有效。

腱绳束在武器中有多种使用方式，但截至目前的最优方式是希腊投石机（palintonon，罗马人称其为 ballista）。在这种非常致命的弩炮上，有两块竖立的筋腱弹簧，各自借助刚性臂或杠杆缠绕，有点儿像绞盘杆（图 5–6）。两臂的末端由一条重弓弦连在一起，整个装置的工作原理在很大程度上与弓一致。的确，其希腊名称来源于这一事实：在松弛状态下，两臂向前，就像复合弓的弓臂；这种投石机上弦的方式（借助强大的绞盘）也和弓差不多。其投射物通常是一枚沿轨道推送的石制弹丸，操作武器所需的绞盘也安装在轨道上，其拉力可达 100 吨力（约为 9 800 牛）。

图 5–6 古希腊投石机简图

罗马人仿制了希腊投石机，米利乌斯·恺撒麾下的炮兵军官维特鲁威为我们留下了一本读起来很有趣的弩炮手册。这些武器制造规格的范围从每次投掷 5 磅（约 2 千克）弹丸到每次投掷 360 磅（约 150 千克）弹丸不等，所有规格的有效射程约为 1/4 英里或 400 米。标准的罗马攻城弩炮似乎可达到每次投掷 90 磅（约 40 千克）弹丸的水平。

公元前 146 年，在戏剧性的最后一次迦太基之围中，罗马人填平了部分紧靠城墙的浅滩潟湖，继而用投石机突破了城防。考古学家在遗址中找到 6 000 多枚石制弹丸，每个重达 90 磅。

虽然架设在军舰上的投石机被恺撒和尼禄在登陆作战时用于清理古代不列颠人的海滩布防，但是投石机从未成为一种真正危险的舰对舰武器。这很可能是因为，大到足以一次击沉一艘船的弩炮，射速太慢以至于无法命中一艘移动中的船。

投石机有时会投掷燃烧弹，但在满载乘员的简易船舶上，火势一般很容易被扑灭。一位高明的海军将领靠向敌人投射装满毒蛇的易碎陶罐，打赢了公元前 184 年的一场海战，但是这种战术似乎没有被推广。大体上讲，投石机并不适用于海战。

尽管如此，投石机仍是陆战最有效的装置，即便其建造和维护实际上是一项非常复杂的任务，而罗马炮兵军官和军士中肯定不乏高人。随着罗马帝国和罗马技艺的逝去，这些武器变得不再实用，逐渐被遗忘。[8] 中世纪的围城战降格为使用配重式投石机或抛石机。

图 5–7 抛石机或中世纪的配重式投石机 —— 最低效的发明

这种类似钟摆的装置，利用了重物被提升后具有的势能。即便是一台大型抛石机，也不太可能将超过 1 吨（相当于 10 000 牛顿）的弹丸提升约 10 英尺（3 米）。因此，储存的最大势能不可能超过 30 000 焦耳。等量的应变能可被储存在 10 或 20 千克的肌腱中，因而即使是一台大型抛石机，可能也只应付得了希腊投石机能量的 1/10 左右。此外，其能量转化效率似乎也低得多。抛石机即使调整到最佳状态，也只在将巨石抛过要塞城墙时，才会给敌人造成点儿麻烦，其对坚固砖石建筑的任何攻击都是无效的。

以能量转化机器视之，弓和希腊投石机都按照相似的原理运作；一般情况下，我们不会意识到一种能量转化机制的效率是多少。像抛石机这样的简陋机械，其大部分可用能量在武器发射时都被用来给该装置的配重杠杆或抛臂加速，最终耗散于必备的终止或制动系统。

对于一张弓或一架希腊投石机，当弓弦第一次释放时，其存储的一些应变能直接转化为弹丸的动能。但是，更多的可用能量则被用来加速弓臂或投石机臂，暂时储存为动能，就像在抛石机里一样。在这种情况下，虽然随发射机制的运作，运动的臂慢下来了，但不是靠固定的终止系统，而是借助拉直和绷紧的弓弦自身。这进一步增加了弦上张力，使之更努力地推送弹丸，令它加速并飞出。因此，大量存储于臂上的动能都被回收了。

给出弓和投石机的数理解释很难，即便写下运动方程，也没法算出解析解。但幸运的是，我的另一位同事托尼·普雷特拉夫（Tony Pretlove）博士对这个难题很感兴趣，将之全部输入计算机。结果相当令人惊讶，理论上其能量转化过程的效率几乎可达到 100%。换言之，存储于装置中的全部应变能几乎都可转化为弹丸的动能。因此，几乎没有能量被浪费或遗留，以产生后坐力或损坏武器。至少就这个方面而言，弓和投石机是枪炮史上的重大进步。

1、射击准备：所有能量储存于筋腱弹簧中。

2、射击操作前期：重臂被加速，从而自弹簧中获取大量能量。

3、射击操作后期：重臂因增加的弦上张力减速，其动能传递给了弹丸。

4、弹丸飞出，携带着储存在系统中的几乎所有能量。

图 5–8 希腊投石机工作机制示意图

1『上面的 4 个步骤要结合原图去看。（2021-06-20）』

我以为，从这些事实中得出的一个结论，至少在实践意义上对大部分弓箭手来说是熟知的。那就是，若没有适当的箭矢或其他合适的弹丸，你绝对不要「发射」一张弓或一架投石机，绝对不能。如果这么干，就无法安全消除存储的应变能，这样一来，不仅弓可能会损坏，弓箭手也极容易受伤。

[6] 最近在塞浦路斯库克里亚的发现表明，5 世纪时军用投石机就已存在，尽管关于它们的一切尚属未知。不管怎样，狄奥尼西乌斯的办法似乎是应对该难题的第一个「科学」途径。

[7] 这可能源自古代船舶使用的「西班牙绞盘」，见第 11 章。

[8] 在 1940 年的纳粹入侵恐慌中，英国的本土志愿军制造使用了两种罗马弩炮，旨在向德国坦克发射汽油弹。但是，这两种投石机的射程大约只有其古典原型的 1/4，它们的设计者很可能并没有仔细地研读维特鲁威的手册。

### 5.5 Resilience or bounciness

A wet sheet and a flowing sea,

A wind that follows fast

And fills the white and rustling sail

And bends the gallant mast.

Allan Cunningham, A Wet Sheet and a Flowing Sea

When Galileo settled down at Arcetri in 1633 to work on elasticity, one of the first questions he asked himself was ' What are the factors which affect the strength of a rope or a rod when it is pulled? Does the strength depend, for instance, upon the length of the rope?' Elementary experiments showed that the force or weight which is needed to break a uniform rope by pulling on it steadily is unaffected by how long it is. This result is what we should expect from common sense, but the news has been some time in getting around and one still meets quite a number of people who are convinced that a long piece of string is 'stronger' than a short one.

Of course these people are not just being silly, for it all depends on what you mean by 'stronger'. The steady force or pull required to break a long string will indeed be the same as that needed to break a short one, but the long string will stretch further before it breaks and it will therefore require more energy to break it, even though the force which is applied and the stress which is in the material remain the same. Put in a slightly different way, a long string will cushion a sudden blow by stretching elastically under the load, so that the transient forces and stresses which result are reduced. In other words it acts rather like the suspension of a car.

Thus in a situation where the load is jerky a long string may well be effectively 'stronger' than a short one. This is why the bodies of eighteenth-century carriages were frequently slung from the chassis by means of very long leather straps, which were better able than short ones to resist the jolts imposed by eighteenth-century roads. Again, anchor cables and tow ropes generally break, not from a steady load, but from sudden jerks, and so it is generally better to arrange for them to be as long as possible. Those who are liable to encounter large dry-docks or oil-rigs under tow at sea at night or in thick weather do well to bear in mind that each of the tugs is probably towing by means of nearly a mile of steel wire. These nautical processions therefore cover an enormous area of sea and can be terrifying to the casual seafarer.*

This quality of being able to store strain energy and deflect elastically under a load without breaking is called 'resilience', and it is a very valuable characteristic in a structure. Resilience may be defined as 'the amount of strain energy which can be stored in a structure without causing permanent damage to it'.

Of course, in order to get resilience, it is not necessary to use a very long rope, such as a wire cable. It is often convenient to use much shorter members, such as the helical springs which are used in the buffers of railway trains, or pads of soft material such as are used for ships' fenders, or materials of low Young's modulus, like the foamed rubbers or plastics which are often used for packaging delicate apparatus. Such things are frequently able to stretch or contract much more in relation to their length and so store more strain energy per unit volume. The excellence of the suspensions of skiers and animals is due, in part, to the comparatively low moduli and high extensions of tendon and other tissues.

On the other hand, although low stiffness and high extensibility promote energy absorption, and so make it more difficult to break a structure by means of a blow, it is only too easy to make a structure which is too floppy for its purpose. This usually limits the amount of resilience which can be designed into a structure. Things like aeroplanes and buildings and tools and weapons have to be pretty rigid in order to do their job. In this respect most structures have to be a compromise between stiffness and strength and resilience, and the achievement of the best compromise is likely to tax the skill of a designer severely.

The optimum condition may vary, not only between different types and classes of structures, but also between different parts of the same structure. In this respect Nature is at an advantage since she has at her disposal an enormous range of elastic properties in the different biological tissues. A simple but interesting example occurs in an ordinary spider's web. The web is subject to impact loads arising from flies blundering into it, and the energy of these blows must be absorbed by the resilience of the threads. It turns out that the long radial threads, which form the main load-carrying part of the structure, are three times as stiff as the shorter circumferential threads which have the duty of actually catching the flies.

Naturally, there are many other ways of storing strain energy and getting resilience than by using tension members, such as ropes or spider's threads, or compression members, such as railway buffers and ships' fenders. Any shape of structure which is capable of being deflected elastically will have much the same effect. Probably the commonest arrangement is to absorb energy by bending, like bows and gallant masts. This is what happens in plants and trees and in most car springs. High-quality swords are expected to be able to recover, elastically, after they have been bent so that the tip touches the hilt.

回弹性

湿漉漉的帆绳，流动的海，

海风刮得快，

鼓起白帆沙沙作响，

巨大的船桅被吹弯。

—— 艾伦·库宁汉姆（Allan Cunningham），

《湿漉漉的帆绳，流动的海》（A Wet Sheet and a Flowing Sea）

1633 年，当定居阿切特里的伽利略研究弹性时，他首先问自己的一个问题是：「绳或杆被拉扯时，影响其强度的因素有哪些？其强度是否取决于绳长等因素？」基础实验表明，平稳地拉断一条均质绳索需要的力或重量与绳索的长度无关。这应该是我们基于常识的预期结果，虽然这种说法已经流传了一段时间，但仍然有相当多的人深信长绳子比短绳子「更结实」。

当然，这些人并非愚蠢，因为一切都取决于你所谓的「更结实」是什么意思。拉断长绳所需的平稳的力或拉力的确和拉断短绳一样，但长绳在断裂前会伸展得更长，因此需要更多的能量，虽然施加的外力与材料的应力保持不变。从一个稍微不同的角度考虑，长绳会借助载荷作用下的弹性拉伸来缓冲受力突变，这样一来，其产生的瞬态外力和瞬态应力会变弱。换言之，它的作用有点儿像汽车的减震悬架。

在负载不稳定的情况下，长绳可能比短绳「更结实」。因此，18 世纪的马车车体常常用很长的皮带拴在底盘架上，长皮带比短皮带更能抵御 18 世纪道路上的颠簸。此外，锚索和纤绳常见的断裂不是来自稳定负载，而是源于猛然拉动，所以通常最好把它们设置得长一些。那些在夜间或恶劣天气容易碰上大型干船坞或海上拖曳式石油钻台的人务必牢记，每一艘拖船都可能携带着近 1 英里长的钢缆。因此，这些海上船队列往往会覆盖庞大的海域，这对偶尔出海的人来说是很恐怖的。[9]

这种能存储应变能并在载荷作用下做弹性挠变而不断裂的性质被称作「回弹性」，这是结构的一个非常有价值的特征。回弹性可被定义为，「储存于结构中而不对其造成永久损伤的应变能值」。

2『回弹力，做一张术语卡片。（2021-06-20）』—— 已完成

当然，为了获得回弹性，未必要用像钢缆这样的长绳索。用短的往往更方便些，比如用于铁道列车缓冲器的螺旋式弹簧，或者用于船舶护舷的软材料衬垫，或者常用于包装精密仪器的低杨氏模量材料，如泡沫橡胶或泡沫塑料等。这类材料往往能相对于其自身长度伸长或缩短更多，从而使单位体积存储更多的应变能。滑雪者和动物减震机制的优势部分应该归功于相对低的杨氏模量和肌腱等组织的相对大的伸展。

虽然低刚度和高延展性有助于能量吸收，从而使突变引发的结构破坏更不容易发生，但这很容易得到一个过于松软的结构。这常常限制了一个结构的设计回弹性。诸如飞机、建筑物、工具和武器等，为了发挥它们的作用，必须具备很大的刚性。就此而论，大部分结构不得不在刚度、强度和回弹性之间寻求折中，而达成最佳的平衡可能对设计师的技能要求颇高。

最佳情况可能各不相同，这种差异不仅存在于结构的不同类型和分级之间，也存在于同一结构的不同部分之间。就这一方面而言，大自然颇有优势，因为它可支配不同生物组织中的各种弹性。一个简单而有意思的例子就是普通的蜘蛛网。蜘蛛网受到误闯入苍蝇的载荷冲击，这些冲击的能量一定会被蛛丝的回弹吸收。结果是，构成该结构主要负载部分的放射状长蛛丝，其刚度是用于捕获苍蝇的更短的环状蛛丝的三倍。

当然，除了用绳索或蛛丝这样的承张构件或铁道缓冲器和船舶护舷这样的承压构件，还有很多其他方法可用来存储应变能和获得回弹性。所有可发生弹性挠变的结构，都会产生几乎一样的效应。或许最常见的办法就是通过弯曲吸收能量，比如弓和巨大的船桅。这就是在作物、树木和大部分车辆弹簧中发生的事情。那种弯曲到令剑尖触及剑柄后能弹性复原的剑，才称得上好剑。

[9] 实际上，锚索和纤绳的大部分回弹性都来自使它们下垂的自身重量。这是选择重缆或重链而非轻得多的有机绳索的原因之一。

### 5.6 Strain energy as the cause of tensile fracture

Starting aside like a broken bow.

Psalm 78

A reasonable amount of resilience is an essential quality in any structure; otherwise it would be unable to absorb the energy of a blow. Up to a point, the more resilient a structure is the better. Such highly sophisticated devices as the Viking ships and the American horse buggy were very flexible and resilient indeed. As long as they are not grossly overloaded, such structures will recover when the load is taken off and all will be well. However, if we do overload them, then of course sooner or later they will break.

Now to break any material in tension a crack must spread right across it. However, to create a new crack requires a supply of energy – as we shall shortly see – and this energy has to come from somewhere. As we have said, it is quite possible to break a bow by 'shooting' it without an arrow. What happens is that the strain energy which was stored in the bow can no longer be disposed of safely as kinetic energy in the arrow, and so some of it is employed in producing cracks within the material of the bow itself. In other words the bow has used its own strain energy to destroy itself. The broken bow is, however, only a special case of all kinds of fracture.

All elastic substances which are under load contain greater or less amounts of strain energy, and this strain energy is always potentially available for the self-destructive process which we call ' fracture'. In other words the stored-up strain energy or resilience may be used to pay the energy-price of propagating a crack through the structure and so causing it to break. In a resilient structure there may be a lot of strain energy around, and the same sort of energy which the Romans used to batter down the massive walls of Carthage can equally well be employed to enable a super-tanker to break herself into two halves.

According to the modern view of the subject, when we break a structure by loading it in tension, we ought not to regard fracture as being caused directly by the action of the applied load pulling on the chemical bonds between the atoms in the material. That is to say, it is not the consequence of the simple action of a tensile stress as the classical text-books would have us believe.* The direct result of increasing the load on the structure is only to cause more strain energy to be stored within its material. The sixty-four thousand dollar question whether the structure actually breaks at any particular juncture depends upon whether or not it is possible for this strain energy to be converted into fracture energy so as to create a new crack.

Modern fracture mechanics is therefore less concerned with forces and stresses than with how, why, where and when strain energy can be turned into fracture energy. Of course, in simple cases like ropes and rods the classical concept of a critical breaking stress is usually an adequate guide, but in large or complicated structures, such as bridges or ships or pressure vessels, it has proved to be a dangerous oversimplification, as we have seen. What comes out of recent theory is that, whether a structure is subjected to a sudden blow or to a steady load, tensile fracture depends chiefly upon:

The price in terms of energy which has to be paid in order to create a new crack.

The amount of strain energy which is likely to become available to pay this price.

The size and shape of the worst hole or crack or defect in the structure.

The fact that the amount of energy required to break any given cross-section of material varies very greatly indeed between different solids is easily confirmed, for instance by hitting first a glass jar and then a tin-can with a hammer. The quantity of energy required to break a given cross-section of a material defines its 'toughness, which is nowadays more often called its 'fracture energy' or 'work of fracture'. This property is quite different to and separate from the 'tensile strength' of the material, which is defined as the stress (not the energy) needed to break the solid. The toughness or work of fracture of a material has a very important effect upon the practical strength of a structure – especially a large one. For this reason we must spend a little time in talking about the work of fracture of various kinds of solids.

导致拉伸断裂的应变能

像一张断弓那样跳开。

——《圣经·旧约全书·诗篇》（Psalm 78）

合理的回弹性是任意结构的一个基本必备性质，否则，它就无法吸收突变作用的能量。在一定程度上，回弹性越好，结构越优良。维京战船和美式单驾马车等高度复杂的设备确实非常柔韧且回弹性好。只要没有严重超负荷，这类结构在卸下载荷后就会恢复原状且一切良好。但是，如果我们使其超负荷，它们迟早会被损坏。

现在要想破坏任何受拉伸作用的材料，一定要有条裂缝正好穿过它。但是，要生成新的裂缝需要能量的补充（我们马上就会看到），而且该能量必须来自别处。就像前文所说，在不搭箭的情况下「射击」，很可能会损坏一张弓。原因是，存储在弓中的应变能不再会安全地转化为箭矢的动能，以致其中一些作用在弓的材料内形成了裂缝。换句话说，弓用自己的应变能破坏了自身。然而，断弓只是各种断裂现象的一个特例。

所有负载的弹性材质都或多或少包含一些应变能，这种潜在的应变能总是可用于「断裂」这个自毁过程。换言之，存储的应变能或回弹性可被用来偿付能量的代价，以扩展出贯通并损坏结构的裂缝。在具有回弹性的结构中，可能遍布很多应变能，罗马人用来摧毁迦太基巨大城墙的那种能量同样可被用来将一艘超级油轮断成两截。

根据这门学问的现代观点，当用拉伸负载破坏结构时，我们不应该将断裂视为外加载荷作用于拉伸材料中的原子间化学键直接造成的，即它不是拉应力简单作用的后果，那是经典教科书的解释。[10] 事实上，增加结构负载的直接后果只是让更多的应变能存储于材料中。真正价值 64 000 美元 [11] 的问题是，结构是否真的会在任一特定时刻断裂，这取决于应变能是否可以转化为断裂能并产生新的裂缝。

因此，现代断裂力学对外力和应力的关注程度要低于应变能如何、为何、在何处及何时能转化为断裂能。当然，在绳和杆这样的简单情境中，临界断裂应力的经典概念通常可以作为一种合适的指导，但在桥梁、船舶或压力容器这样巨大或复杂的结构中，如我们所见，它被证实是一种危险的过度简化的方法。从新近理论得出的结论是，外力突变或负载稳定的结构是否发生拉伸断裂主要取决于以下三个因素：

1、为了产生新裂缝必须付出的能量代价。

2、有可能付出该代价的应变能值。

3、结构中最严重的孔洞、裂缝或缺陷的尺寸与形状。

对于不同的固体，破坏给定材料截面所需的能量值的差别很大，这个事实很容易得到确认，比如，用榔头先敲打一个玻璃瓶，再击打一个锡罐，结果差别就很大。韧度即指破坏给定材料截面所需的能量值，现在常被称作断裂能或断裂功。这种特性同材料的抗拉强度存在很大的差异和区别，其中抗拉强度是指破坏固体所需的应力（不是能量）。材料的韧度或断裂功对于一个结构的实际强度有非常重大的影响，尤其是对大型结构而言。为此，我们必须花点儿时间来谈谈各种固体的断裂功。

[10] 拉开原子实际所需的「真实」或理论最大拉应力的确非常强，远大于借助普通抗拉测试确定的「实际」强度。

[11] 1955 年，美国哥伦比亚广播公司（CBS）推出了一档知识竞赛节目，名为《64 000 美元的问题》。—— 编者注

### 5.7 Fracture energy or 'work of fracture'

Since, when a solid is broken in tension, at least one crack must be made to spread right across the material, so as to divide it into two parts, at least two new surfaces will have to be created which did not exist before fracture. In order to tear the material apart in this way and produce these new surfaces it is necessary to have broken all the chemical bonds which previously held the two surfaces together.

The quantity of energy which is needed to break most kinds of chemical bonds is well known – at least to chemists – and it turns out that, for most of the structural solids with which we are concerned in technology, the total energy needed to break all the bonds on any one plane or cross-section* is very much the same and does not differ widely from 1 Joule per square metre.

When we are dealing with the range of materials which are, rather understandably, called 'brittle solids' – which includes stone and brick and glass and pottery – this is nearly all the energy we have to provide in order to cause fracture. As a matter of fact, 1 J/m2 is really rather a pathetically small amount of energy. It is a sobering thought that, on the simplest theory, the strain energy which could be stored in one kilogram of tendon would 'pay' for the production of 2,500 square metres (over half an acre) of broken glass surface – which accounts for the effects of bulls in china-shops. This is why a bricklayer can break a brick neatly in half with a light tap from his trowel and it is why we have only to be a little clumsy in order to break a plate or a tumbler.

Naturally, this is the reason why, if we can possibly avoid it, we do not use 'brittle solids' in applications where they are in tension. These materials are brittle not, primarily, because they have low tensile strengths – that is to say they need a low force to break them – but rather because it needs only a low energy to break them.

The technical and biological materials which are actually used in tension, and used with comparative safety, all require a great deal more energy in order to produce a new fracture surface. In other words, the 'work of fracture' is very much higher – enormously higher – than is the case with brittle solids. For a practical tough material the work of fracture usually lies between 103 J/m2 and 106 J/m2. Thus the energy which is needed to cause fracture in wrought iron or mild steel may be about a million times as high as that needed to break the equivalent cross-section of glass or pottery, although the static tensile strengths of these materials are not very different. This is why a table of'tensile strengths', such as Table 2, (p. 56), can be a highly misleading document when it comes to the choice of a material for a particular service. It is also why the classical theory of elasticity, based mainly on forces and stresses, which has been laboriously evolved over hundreds of years – and still more laboriously taught to students – is really inadequate, by itself, to predict the behaviour of real materials and structures.

TABLE 4 Very approximate figures for the work of fracture and tensile strengths of some common solids

Although the detailed mechanisms whereby such enormous amounts of energy can be absorbed within tough materials as 'work of fracture' are often subtle and complicated, the broad principle is really very simple. In a 'brittle' solid the work done during fracture is virtually confined to that which is needed to break the chemical bonds at, or very near to, the new fracture surface. As we have seen, this energy is small and amounts only to about 1 J/m2. In a tough material, although the strength and the energy of any individual bond remains the same, the fine structure of the material is disturbed to a very much greater depth during the breaking process. In fact it may be disturbed to a depth of well over a centimetre: that is, to a depth of about 50 million atoms below the visible fracture surface. Thus if only one in fifty of these atomic bonds is broken during the process of disturbance then the work of fracture – the energy needed to produce the new surface – will be increased a millionfold, which, as we have seen, is about what really does happen. In this way molecules living deep within the interior of the material are able to absorb energy and to play their part in resisting fracture.

Figure 9. A typical stress-strain curve for a ductile metal such as mild steel. The shaded area is related to the work of fracture of the metal.

The high work of fracture of the soft metals is primarily due to the fact that these materials are 'ductile'. This means that, when they are pulled in tension, the stress-strain curve departs from Hooke's law at quite a moderate stress, after which the metal deforms plastically, rather like plasticine (Figure 9). When a rod or sheet of such a metal is broken in tension the material is pulled out before it breaks after the fashion of treacle or chewing gum; the broken ends will then be tapered or conical and will look rather like Figure 10. This form of fracture is often called 'necking'.

Figure 10. The work of fracture is proportional to the volume of metal plastically distorted, i.e. to the shaded area, and thus is roughly as t2. Hence the work of fracture of thin sheet may be very low.

Necking and similar forms of ductile fracture can take place because a great many of the innumerable layers of atoms in the metal crystals are enabled to slide over each other by means of what is called the 'dislocation mechanism'. Dislocations not only enable layers of atoms to slide over each other like a pack of cards but they also absorb energy – quite a lot of energy. The result of all this slipping and sliding and stretching in the crystals is that the metal is enabled to distort and a great deal of energy is got rid of.

The dislocation mechanism,* which was originally postulated by Sir Geoffrey Taylor in 1934, has been the subject of intensive academic research over the last thirty years. It turns out to be an extraordinarily subtle and complicated affair. What takes place inside so apparently simple a thing as a piece of metal seems to be quite as clever as many of the mechanisms in living biological tissues. Yet the funny thing is that this clever mechanism cannot possibly be purposive, if only because Nature has nothing, so to speak, to gain from it, since she never makes any structural use of metals, which very seldom occur native in the metallic state anyway. However this may be, dislocations in metals have been of enormous benefit to engineers and might almost have been invented for their benefit, since they not only result in metals being tough but also enable them to be forged and worked and hardened.

Artificial plastics and fibrous composites have other work of fracture mechanisms which are quite different from those in metals but which are fairly effective. Biological materials seem to have developed methods of achieving high works of fracture which are very cunning indeed. That in timber, for instance, is exceptionally efficient, and the work of fracture of wood is, weight for weight, better than that of most steels.†

Let us now go on to discuss how the strain energy in a resilient structure manages to get turned into work of fracture. If you like, what is the real reason why things break?

断裂能或断裂功

当一个固体在拉伸作用下断裂时，必须至少扩展出一条裂缝且正好贯穿材料以将其一分为二，这样至少会创造出两个在断裂前并不存在的新表面。为了用这种方法将材料撕开并生成这些新表面，需要破坏此前将两个表面结合在一起的全部化学键。

破坏大多数类型的化学键所需的能量值是众所周知的，至少对化学家来说如此。对于我们在技术上关心的大部分结构性固体，破坏任一平面或截面的所有化学键所需的总能量 [12] 大同小异，约为 1 焦耳 / 平方米。

2『自己学化工的竟然一点没概念，破坏任一平面或截面的所有化学键的所需的总能量，做一张信息数据卡片。（2021-06-21）』—— 已完成

当我们处理的材料属于相当易于理解的所谓「脆性固体」（包括石头、砖块、玻璃和陶）时，该数值近似等于使这些材料断裂所需的能量值。事实上，1 J/m2 的确是一个非常小的能量值。这是个发人深省的想法，基于最简单的理论，存储于 1 千克肌腱中的应变能足以为 2 500 平方米（超过半英亩）碎玻璃表面的生成「买单」，这充分说明了蛮牛冲进瓷器店的后果。正因如此，砖匠用他的瓦刀轻轻一敲就能利索地把砖块一分为二，而我们只要稍不小心就会磕破盘子或玻璃杯。

当然，这也是我们要尽可能避免在拉伸状况下使用「脆性固体」的原因。这些材料是脆的，并不是因为它们的抗拉强度很低（它们破坏自身只需要很小的力），而是因为它们破坏自身只需要很小的能量。

现实中，在拉伸情况下可相对安全使用的工艺材料和生物材料，全都需要更多的能量才能生成新的断面。换言之，断裂功要比脆性固体的强度大得多。对实用的韧性材料而言，断裂功常常介于 10^3 J/m2 到 10^6 J/m2 之间。因此，在锻铁或低碳钢中导致断裂所需的能量，可以达到破坏玻璃或陶的等效截面所需能量的 100 万倍左右，尽管这两类材料的静态抗拉强度没多大差别。这就是为什么如表 5–2 所示的「抗拉强度」在涉及为特定用途选择材料时便颇具误导性，这也是为什么主要基于外力和应力的经典弹性理论，历经数百年的艰辛演化和教学实践的检验，却不能只靠它来预测真实材料和结构的行为。

如此巨大的能量值可被坚韧材料吸收而成为「断裂功」，虽然其详细机制往往是微妙而复杂的，但其大致原理却非常简单。脆性固体在断裂过程中所做的功，实质上仅出于破坏新断面或相邻区域化学键的需要。如我们所见，该能量很小，仅为 1 J/m2 左右。在韧性材料中，即使任意单独化学键的强度和能量保持一致，在断裂过程中，扰动也会波及材料精细结构的极深处。事实上，扰动的深度可达 1 厘米以上，即可见断面以下约 5 000 万个原子的深度。因此，若只有 1/50 的原子间化学键在扰动过程中被破坏，那么断裂功 —— 产生新断面所需的能量 —— 会增加到百万倍，如我们所见，这正是真实发生的事情。材料内部深处的分子就是以这种方式吸收能量，并在抵抗断裂的过程中发挥作用的。

表 5–2 一些常见固体的断裂功和抗拉强度的近似值

| 材料种类 | 断裂功近似值 J/m2 | 抗拉强度近似值（理论上）MN/m2 |
| --- | --- | --- |
| 玻璃、陶（Glass, pottery） | 1-10 | 170 |
| 水泥、砖、石（Cement, brick, stone） | 3-40 | 4 |
| 聚酯和环氧树脂（Polyester and epoxy resins） | 100 | 50 |
| 尼龙、聚乙烯（Nylon, polythene） | 1000 | 150-600 |
| 骨骼、牙齿（Bones, teeth） | 1000 | 200 |
| 木材（Wood） | 10,000 | 100 |
| 低碳钢（Mild steel） | 100,000-1,000,000 | 400 |
| 高抗拉钢（High tensile steel） | 10,000 | 1,000 |

软金属的大断裂功主要归因于这些材料的可延展性。这意味着，当它们被拉伸时，其应力–应变曲线在较适中应力的作用下偏离了胡克定律，随后金属发生塑性形变，有点儿像橡皮泥（见图 5–9）。当这样的金属杆或金属片在拉伸作用下断裂时，材料在像糖浆或口香糖那样断裂之前就被拉开了；其断裂末端会逐渐变尖或呈锥状，如图 5–10 中所示。这种断裂形式常被称作「颈缩」。

颈缩及类似的延展性断裂之所以发生，是因为金属晶体中的大量原子层可借助「位错机制」相对滑动。位错不仅能让原子层像一副纸牌那样相对滑动，还能吸收相当多的能量。在晶体中，所有这些松动、滑动和拉伸的结果都是使金属变形并消耗大量能量。

图 5–9 低碳钢等可延展金属的典型「应力–应变」曲线。阴影区域的面积大小与金属断裂功有关

图 5–10 断裂功与金属发生塑性形变的体积（阴影区域）成正比，即大致与 t2 成正比。因此，薄金属片的断裂功可能非常小

位错机制最初是由杰弗里·泰勒爵士（Sir Geoffrey Taylor）于 1934 年提出的，近 30 年来一直是学术研究的热门课题。结果表明，这是件极其微妙而复杂的事情。像一块金属这样看似简单的东西内部发生的事情，似乎与活体生物组织中的很多机制一样巧妙。有趣的是，这种巧妙的机制不可能是有意为之；可以说大自然从中一无所获，它从未在任何结构上使用过金属，金属在任何天然情况下也极少以单质形态出现。不管怎样，金属中的位错对工程师大有裨益，而且可能就是因其好处才被创造出来，它们不仅会使金属变得坚韧，还能使它们可被锻造、加工和硬化。

人造塑料和纤维复合材料有其他断裂功机制，与金属存在很大不同，但相当有效。生物材料似乎已经演化出获得高断裂功的巧妙方法，比如，在木材中就格外有效。木头的断裂功在重量相同的条件下，要优于大部分钢材。

现在，让我们继续探讨回弹性结构中的应变能如何转化为断裂功。如果你乐意，也可以说成，让我们讨论一下东西损坏的真正原因是什么。

[12] 这通常和「自由表面能」是一样的，它与液体和固体的表面张力紧密相关，而且在材料科学方面的探讨中经常被提及。

### 5.8 Griffith – or how to live with cracks and stress concentrations

Ony rollin's better than pitchin' wi' superfeecial cracks in the tail-shaft.

Rudyard Kipling, Bread upon the Waters (1895)

As we said at the beginning of this chapter, all technological structures contain cracks and scratches and holes and other defects; ships and bridges and aircraft wings are liable to all sorts of accidental dents and abrasions and we have to learn to live with them as safely as may be, in spite of the fact that, according to Inglis, the local stress at many of these defects may be well above the official breaking stress of the material.

How and why we are generally able to live with these high stresses without catastrophe was propounded by A. A. Griffith (1893-1963) in a paper which he published in 1920, just twenty-five years after Kipling's splendid story about a crack. Since Griffith was only a young man in 1920, practically nobody paid any attention. In any case Griffith's approach to the whole problem of fracture by way of energy, rather than force and stress, was not only new at the time but was quite foreign to the climate of engineering thinking, then and for many years afterwards. Even nowadays too many engineers do not really understand what Griffith's theory is all about.

What Griffith was saying was this. Looked at from the energy point of view, Inglis's stress concentration is simply a mechanism (like a zip-fastener) for converting strain energy into fracture energy, just as an electric motor is simply a mechanism for converting electrical energy into mechanical work or a tin-opener is simply a mechanism for using muscular energy to cut through a tin. None of these mechanisms will work unless it is continually supplied with energy of the right sort. The stress concentration is quite good at its job but, if it is to keep on prising the atoms of a material apart, then it needs to be kept fed with strain energy. If the supply of strain energy dries up, the fracture process stops.

Now consider a piece of elastic material which is stretched and then clamped at both ends so that, for the present, no mechanical energy can get in or out. Thus we have a closed system containing just so much strain energy.

If a crack is to propagate through this stretched material then the necessary work of fracture will have to be paid for in energy and the terms are strictly cash. If, for convenience, we consider our specimen to be a plate of material one unit thick, then the energy bill will be WL where W = work of fracture and L = length of crack. Note that this is an energy debt, an item on the debit side of the energy account, although as a matter of fact no credit is given. This debit increases linearly or as the first power of the length, L, of the crack.

This energy has to be found immediately from internal resources, and since we are dealing with a closed system, it can only come from some relaxation of strain energy within the system. In other words, somewhere in the specimen the stress must be diminished.

This can occur because the crack will gape a little under stress and thus the material immediately behind the crack surfaces is relaxed (Figure 11). Roughly speaking, two triangular areas – which are shaded in the diagram – will give up strain energy. As one might expect, whatever the length, L, of the crack, these triangles will keep roughly the same proportions, and so their areas will increase as the square of the crack length, i.e. as L2. Thus the strain energy release will increase as L2.

Figure 11. 

(a) Unstrained material.

(b) Material strained and rigidly clamped. No energy can get in or out of the system.

(c) Clamped material is now cracked. Dotted areas relax and give up strain energy, which is now available to propagate the crack still further.

Thus the core of the whole Griffith principle is that, while the energy debt of the crack increases only as L, its energy credit increases as L2. The consequences of this are shown graphically in Figure 12. O A represents the increased energy requirement as the crack extends, and it is a straight line. OB represents the energy released as the crack propagates, and it is a parabola. The net energy balance is the sum of these two effects and is represented by OC.

Figure 12. Griffith energy release, or why things go pop.

Up to the point X the whole system is consuming energy; beyond point X energy begins to be released. It follows that there is a critical crack length, which we might refer to as Lgy which is called the 'critical Griffith crack length'. Cracks shorter than this are safe and stable and will not normally extend; cracks longer than Lg are self-propagating and very dangerous.* Such cracks spread faster and faster through the material and inevitably lead to an 'explosive', noisy and alarming failure. The structure will end with a bang, not a whimper, and very possibly with a funeral.

The most important consequence of all this is that, even if the local stress at the crack tip is very high – even if it is much higher than the 'official* tensile strength ofthe material – the structure is still safe and will not break so long as no crack or other opening is longer than the critical length Lg. It is this principle which gives us our main defence against undue alarm and despondency about Inglis's stress concentrations. This is why holes and cracks and scratches are not even more dangerous than they are.

Naturally we want to be able to calculate Lg numerically. As it turns out, for straightforward conditions, this is much simpler than we have any reasonable right to expect. Although the mathe-^ matical process by which Griffith got there might be regarded as slightly alarming, the actual finished result is disarmingly simple, indeed brilliantly simple, for

or, put algebraically,

where W = work of fracture in J/m2 for each surface

E = Young's modulus in Newtons/m2

s = average tensile stress in material near the crack (taking no account of stress concentrations) in New-tons/m2

Lg = critical crack length in metres.

(Caution, Newtons, not Meganewtons.)

So the length of a safe crack depends simply upon the ratio of the value of the work of fracture to that of the strain energy stored in the material – in other words it might be considered as inversely proportional to the 'resilience' In general, the higher the resilience the shorter the crack one can afford to put up with. This is another example of not being able to have things both ways.

As we have seen, rubber will store a great deal of strain energy. However, its work of fracture is quite low and so the critical crack length, Lg, for stretched rubber is quite short, usually a fraction of a millimetre. This is why, when we stick a pin into a blown-up balloon, it bursts with a very satisfactory pop. Thus, although rubber is highly resilient and will stretch a long way before it breaks, when it does break, it breaks in a brittle manner, very much like glass.

One solution to the problem of how to be resilient and also tough is that provided by cloth and basket-work and wooden ships and horse-drawn vehicles. In these things the joints are more or less loose and flexible and so energy is absorbed in friction -that is what all the squeaks are about. However, although hedges and birds' nests are pretty resistant to attack, this way of going about things is not often used by modern engineers, except perhaps in the case of car tyres, where the rubber is saved from being unduly brittle by the incorporation of canvas and cords.

It will be seen that Lg shortens very rapidly as the stress, s, increases. Thus, if we want to be able to accommodate a good long crack safely at a reasonably high stress, we need the highest possible value of W> the work of fracture, in a good stiff material, i.e. one with a high E. It is just because mild steel combines good work of fracture with high stiffness, and is also fairly cheap, that it is so widely used and so important economically and politically.

Although, as we shall see, there are a lot of snags about applying the Griffith equation, which we have just described, and we ought not to regard it as a sort of God-given answer to all design problems, it does in fact do a lot to clarify various structural situations which used to be very obscure and full of mumbo-jumbo.

For instance, instead of messing about with thoroughly bogus 'factors of safety', one can nowadays simply try to design a structure to accommodate a crack of pre-determined length without breaking. The crack length chosen has to be related to the size of the structure and also to the probable service and inspection conditions. Where human life is concerned it is clearly desirable that a 'safe' crack should be long enough to be visible to a bored and rather stupid inspector working in a bad light on a Friday afternoon.

In a really large structure, such as a ship or a bridge, we probably want to be able to put up with a crack at least 1-2 metres long with safety. If we suppose that we want to plan for a crack 1 metre long, then, making the rather conservative assumption that the work of fracture of the steel is 105 J/m2, we find that such a crack will be stable up to a stress of 110 MN/m2 or 15,000 p.s.i. However, if we want to play safer and plan for a crack 2 metres long, then we shall have to reduce the stress to about 80 MN/m2 or 11,000 p.s.i.

In fact 11,000 p.s.i. is just about the sort of stress to which large structures are often designed, and in mild steel this stress affords a factor of safety (strictly speaking, what is called a 'stress factor') of between five and six – for what that is worth. As an example of the sort of way this works out in practice, of 4,694 ships subjected to routine inspection in dock, 1,289, or just over a quarter, were found to have serious cracks in the main hull structure – after which, of course, remedial action was taken. The number which actually broke in two at sea, though still too high, was something like one in five hundred, a fairly small proportion. If these ships had been designed to a higher stress, or made of more brittle material, in most cases the cracks would not have been spotted before the ships broke at sea and were lost.

According to the pure and simple Griffith doctrine, a crack shorter than the critical length should not be able to extend at all, and therefore, since all cracks must start life by being short ones, nothing should ever break. In fact, of course, for all sorts of good reasons which are the affair of metallurgists and materials scientists, cracks of less than the critical length do manage to extend themselves, as we shall see in Chapter 15. However, the great point is that they generally do this so slowly that there should be plenty of time to spot them and do something about the situation.

Unfortunately things do not always work out quite that way. Professor J. F. C. Conn, who was Professor of Naval Architecture at Glasgow until recently, told me the story of a cook in a big freighter who was a little startled, when he went into his galley one morning to cook the breakfast, to find a large crack in the middle of the floor.

The cook sent for the Chief Steward, who came and looked at the crack and sent for the Chief Officer. The Chief Officer came and looked at the crack and sent for the Captain. The Captain came and looked at the crack and said 'Oh, that will be all right -and now can I have my breakfast?'

The cook, however, was of a scientific turn of mind, and, when he had disposed of breakfast, he got some paint and marked the end of the crack and painted the date against the mark. Next time the ship went through some bad weather the crack extended a few inches and the cook painted in a new mark and a new date. Being a conscientious man he did this several times.

When the ship eventually broke in two, the half which was salvaged and towed into port happened to be the side on which the cook had painted the dates, and this, Professor Conn told me, constitutes the best and most reliable record we have of the progress of a large crack of sub-critical length,

格里菲斯理论

对船尾推进轴来说，晃晃荡荡总比表面有裂缝好。

—— 鲁德亚德·吉卜林（Rudyard Kipling），《施面包于水上》（Bread upon the Waters，1895）

我在本章开头说过，所有工艺结构都包含裂缝、划痕、孔洞等缺陷，船舶、桥梁和机翼上容易产生各种各样的意外凹痕和磨损，而我们不得不学会尽可能安全地与之共存。但是按英格利斯的说法，其中很多缺陷处的局部应力可能已远超材料公认的断裂应力。

就在吉卡林讲述那个有关裂缝的精彩故事的 25 年后，格里菲斯（A. A. Griffith）在他于 1920 年发表的一篇论文中提出了一个问题：我们通常如何以及为何能与这些高应力在无灾变的情况下共存？因为格里菲斯当年只是个年轻人，所以几乎没人注意到他的研究。不管怎么说，格里菲斯处理断裂问题时用的是能量，而非外力和应力，这不仅在当时是新颖的，而且在此后多年间对工程思考的氛围来说也相当陌生。即便到今天，还有很多工程师不太明白格里菲斯的理论到底说了些什么。

2『格里菲斯理论，做一张术语卡片。（2021-06-21）』—— 已完成

格里菲斯说的是这样一件事。从能量的观点来看，英格利斯的应力集中不过是一种将应变能转化为断裂能的机制（好似一条拉链），就好比电动机不过是一台将电能转化为机械功的机器，或者罐头刀不过是用肌肉能量切开罐头的器械。这些机制本不会起作用，除非其持续获得合适的能量供应。应力集中发挥了很好的作用，但若要持续将材料中的原子分开，则需要应变能来维持。如果应变能的供应枯竭，断裂过程就会终止。

现在假设有一块弹性材料，拉伸后夹住它的两端，使其暂时没有机械能输入或输出。于是，我们便有了一个包含大量应变能的封闭系统。

如果一条裂缝扩展并贯穿了被拉伸的材料，那么必要的断裂功将不得不付出能量的代价，且仅限于现成的能量。为方便计算，假设我们的样品是一块单位厚度的材料板，那么要付出的能量为 WL，其中 W 为断裂功，L 为裂缝长度。注意，这是一个能量的负债，一项需记在借方的能量值，尽管事实上概不赊欠。这个借方额度的增长是线性的，或随裂缝长度 L 的一次幂的增加而增加。

这个能量需要立即从内部资源中获得，因为我们处理的是一个封闭的系统，它只能来源于系统内的应变能的释放。换言之，样品中某处的应力必须减小。

这是因为缝隙在应力的作用下会裂开一点儿，所以紧邻裂缝表面的材料是松弛的（见图 5–11）。大致说来，两个三角区域（图中阴影部分）会释放应变能。不出所料，不论裂缝长度 L 是多少，这些三角区域会大致保持同样的占比，其面积会随裂缝长度平方（L2）的增加而增加。因此，应变能的释放会随 L2 的增加而增加。

图 5–11 三张图表示如下：1）未应变的材料。2）材料产生应变并被紧紧夹住。该系统没有能量的输入或输出。3）被夹住的材料发生开裂。阴影区域变得松弛并释放应变能，可就此进一步扩展裂缝。

因此，格里菲斯理论的核心是，裂缝的能量负债只随 L 的增加而增加，而其能量的贷方额度随 L2 的增加而增加。这样的结果可由图 5–12 形象地表示出来。OA 表示随裂缝扩展而增加的能量需求，它是一条直线。OB 表示随裂缝扩展而产生的能量释放，它是一条抛物线。净能量衡算为这两种效应之和，用 OC 代表。

在到达 X 点之前，整个系统都在消耗能量；过了 X 点，能量开始被释放出来。由此可知，存在一个临界裂缝长度，我们把它记为 Lg，即「临界格里菲斯裂缝长度」。比这个长度短的裂缝是安全稳定的，且一般不会扩展；而比 Lg 长的裂缝则会自我扩展，且非常危险。[13] 这种裂缝在材料中会扩展得越来越快，不可避免地引发「爆炸性的」、吵闹的且令人惊慌的故障。这个结构的终结会伴随着一声巨响，而非一阵呜咽，而且很可能还有葬礼。

图 5–12 格里菲斯能量释放，或者东西爆裂的原因

这一切最重要的后果是，即使裂缝尖端的局部应力非常高，远高于材料「公认」的抗拉强度，该结构仍然是安全的，只要没有长于临界长度 Lg 的裂缝或其他开口，它就不会断裂。正是这个原理使我们不致陷入对英格利斯应力集中的过度恐慌和沮丧中，也使孔洞、裂缝和划痕并不像它们看起来的那么危险。

当然，我们仍希望算出 Lg 的数值。结果表明，在一目了然的情况下，这比我们的任何合理预期都简单得多。虽然格里菲斯的数学推导过程可能看起来有点儿吓人，但他实际得出的结论却非常简单，因为：

$$Lg = \frac{1}{π}×\frac{裂缝表面单位面积的断裂功}{材料单位体积储存的应变能}$$

或者，用代数方法表示为：

$$Lg=\frac{2WE}{πs^2}$$

注：因为应变能为 0.5se，且 E=s/e，所以应变能也可写成 s$^2$/2E

其中，W 是以 J/m2 为单位的裂缝表面断裂功，E 是以 N/m2 为单位的杨氏模量，s 是以 N/m2 为单位的裂缝附近材料的平均拉应力（不计应力集中），Lg 是以 m 为单位的临界裂缝长度。（注意，这时涉及的单位是牛顿，不是兆牛顿。）

所以，一条安全裂缝的长度仅取决于断裂功与材料中存储的应变能的比值。换言之，它与「回弹性」成反比。一般说来，回弹性越强，材料能承受的裂缝长度就越短。这是鱼与熊掌不可兼得的又一个例子。

如我们所见，橡胶会存储大量的应变能。然而，其断裂功相当低，且对被拉伸的橡胶而言，其临界裂缝长度 Lg 也相当短，通常不超过 1 毫米。这就是为什么当我们拿一根针戳一个鼓胀的气球时，它会砰的一声爆炸。因此，虽然橡胶的回弹性很强且在破裂前会伸展得很长，但到破裂之时，仍像玻璃那样脆弱。

如何使回弹性与坚韧兼得，解决这个难题的一个办法是由纺织物、编织物、木制船舶和马拉车辆提供的。这些东西的接合处或多或少是松动且柔韧的，故而能量可被摩擦吸收，这也是所有咯吱咯吱声的由来。但是，纵然篱笆和鸟巢的抗攻击性较强，这种方式也不常为现代工程师所用。汽车轮胎或许是一种例外情况，原材料中加入了帆布和线绳，可使轮胎的橡胶不至于太脆。

显然，随应力 s 的增长，Lg 会迅速缩短。因此，如果想在相当大的应力下安全地容纳一条长裂缝，那么在刚度良好（高 E）的材料中，我们需要尽可能大的断裂功 W。低碳钢因为兼具良好的断裂功和较高的刚度，并且相当廉价，所以获得了广泛的运用，具有很重要的经济和政治意义。

我们将会看到，虽然应用前文介绍的格里菲斯方程有许多障碍，我们也不应该视之为一种针对所有设计难题的天赐答案，但它确实为澄清曾经非常模糊且充斥着胡言乱语的各种结构状况做了很多贡献。

例如，今天的人不用再摆弄虚假的「安全系数」，就能简单地尝试设计出一个结构，使其容纳预设长度的裂缝而不断裂。选定的裂缝长度必须与结构的尺寸、可能的用途和检验环境相关。在关乎生命安全的地方，「安全」的裂缝显然要足够长，能让在周五下午的昏暗光线下心不在焉地工作的检验员看到。

在一个巨大的结构（譬如船舶或桥梁）中，为确保安全，我们可能需要它至少能承受 1-2 米长的裂缝。如果裂缝为 1 米长，我们保守地假设钢的断裂功是 105 J/m2，那么这样一条裂缝会一直保持稳定，直到应力达到 110 MN/m2 或 15 000 psi。然而，如果我们想要更安全，即裂缝为 2 米长，那么我们必须将应力减小到 80 MN/m2 或 11 000psi 左右。

事实上，11 000 psi 只是大型结构通常的设计承受应力，而在低碳钢中，这个应力的价值是提供 5-6 的安全系数（严格地讲，即所谓的「应力系数」）。作为在现实中解决问题的办法，在一次对码头进行的例行检查中，4 694 艘船中有 1 289 艘或者略多于 1/4 的船，其主体结构存在严重的裂缝 —— 当然，事后已做补救。而实际上在海上断成两截的船的数量，大约为每 500 艘中有一艘，这已是相当小的比例了，但仍旧损失惨重。如果这些船的设计承受应力更大，或者用更脆的材料制造，那么在大多数情况下，直到船舶在海上出事，裂缝都不会被发现。

按照纯粹且简单的格里菲斯理论，比临界长度短的裂缝根本无法扩展，而由于所有裂缝肯定都是从短的情况开始，所以断裂应该不会发生。事实上，源于冶金学家和材料学家想出的各种好理由，小于临界长度的裂缝仍可继续扩展，如我们将在第 15 章看到的那样。但是，重点在于它们通常扩展得非常慢，所以我们应该有足够的时间找出它们并做出补救。

不幸的是，事情并非一直如此。格拉斯哥的船舶工程教授康恩（J.F. C. Conn）最近给我讲述了一位厨师在一艘大货轮上被吓了一跳的故事。一天早上，这位厨师走进厨舱准备做早餐，却在地板中间发现了一条巨大的裂缝。这位厨师唤来客运主任，客运主任看后叫来了大副，大副看后又请来了船长。船长看了看裂缝说：「哦，没什么大不了的。现在我能吃早餐了吗？」

但是，厨师是个有科学家潜质的人，他吃完早餐后，便找来一些涂料在裂缝的末端做了标记，并在标记上写下了日期。下一次，当这艘船遇到坏天气时，裂缝又扩展了几英寸（1 英寸 = 2.54 厘米），厨师便涂上新标记，写下了新日期。作为一个有责任心的人，他如此做了几次。

当船最终断成两截后，厨师记录日期的那一半船体正好被打捞出水并拖回港口。康恩教授告诉我，这是对亚临界长度的巨大裂缝的扩展过程的最好和最可靠的记录。

[13] 也许有人认为 Lg 对应于图上的 OY，但稍想一下就会发现情况并非如此。我们需要将负的能量值 ZX 注入该系统以使裂缝继续扩展，它代表了安全边际或能量阈值（事实上，它才是真正的「安全系数」）。

### 5.9 'Mild' steel and 'high tensile' steel

When a structure fails or seems in danger of failing the natural instinct of the engineer may be to specify the use of a 'stronger' material: in the case of steel, what is known as a 'higher tensile' steel. With large structures this is generally a mistake, for it is clear that most of the strength, even of mild steel, is not really being used. This is because, as we have seen, the failure of a structure may be controlled, not by the strength, but by the brittleness of the material.

Although the measured value of the work of fracture does depend on the way in which the test is done, and it is difficult to get consistent figures, yet the toughness of most metals is undoubtedly reduced very greatly as the tensile strength increases. Figure 13 shows the sort of relationship which exists in simple carbon steels at room temperature.

It is quite easy, and not very expensive, to double the strength of mild steel by increasing the carbon content. If we do so, however, we may reduce the work of fracture by a factor of something like fifteen. In this case the critical crack length will be reduced in the same proportion – i.e. from 1 metre to 6 centimetres – at the same stress. However, if we double the working stress, which is presumably the object of the exercise, the critical crack length will be reduced by a factor of 15 × 22 = 60. So, if a safe crack was originally 1 metre long, it will now measure 1·5 centimetres – which would be thoroughly dangerous in a large structure.

Figure 13. The approximate relationship between tensile strength and work of fracture for some plain carbon steels. (By courtesy of Professor W. D. Biggs.)

With small components like bolts and crankshafts the situation is different, and it is meaningless to design for a crack a metre long. If we settle for an allowable crack length of, say, 1 centimetre, such a crack may be safe up to a stress of nearly 40,000 p.s.i. (280 MN/m2), and so there is a good case for using a high tensile material. Thus, one consequence of Griffith is that, on the whole, we can use high strength metals and high working stresses more safely in small structures than in large ones. The larger the structure the lower the stress which may have to be accepted in the interests of safety. This is one of the factors which tend to place a limit on the size of large ships and bridges.

The relationship between work of fracture and tensile strength which is sketched in Figure 13 is roughly true for simple commercial carbon steels. It is possible to get rather better combinations of strength and toughness by using 'alloy steels', that is, steels alloyed with elements other than carbon, but these are generally too expensive for large-scale construction. It is for these reasons that something like 98 per cent of all the steel which is made is 'mild steel', that is to say, a soft or ductile metal with a tensile strength of around 60,000 to 70,000 p.s.i. or 450 MN/m2.

低碳钢与高强度钢

当结构失效或看起来有失效的危险时，工程师的天然本能可能会促使他们使用「更强」的材料。对钢材来说，就是指高强度钢。但对大型结构来说，这通常是种错误的办法，因为很显然，大部分强度，甚至是低碳钢的强度，并没有真的被用上。正如我们所见，结构的失效是可控的，它靠的不是强度，而是材料的脆度。

2『结构的失效是可控的，它靠的不是强度，而是材料的脆度。直觉上这句话的信息很重要，做一张金句卡片。（2021-06-21）』—— 已完成

虽然断裂功的测量值取决于测试的方式，而且很难得到一致的数值，但是随着抗拉强度的提升，大部分金属的韧度无疑会急剧下降。图 5–13 给出了室温条件下普通碳素钢的断裂功和抗拉强度之间的关系。

通过增加碳含量来让低碳钢的强度翻倍，既简单也不贵。然而，若这么做，我们可能要将断裂功降为大约原来的 1/15。针对这种情况，相同应力条件下临界裂缝长度也会按同样的比例降低，即从 1 米缩短至 6 厘米。然而，如果我们把工作应力加倍，大概是出于实际的需要，临界裂缝长度会缩短为原来的 1/60。所以，若一条安全裂缝起初有 1 米长，现在就只有 1.5 厘米，这在大型结构中是非常危险的。

带螺栓和曲轴等小零件的情况则有所不同，考虑 1 米长裂缝的设计就变得没有意义了。如果允许的裂缝长度为 1 厘米，这样一条裂缝在应力接近 40 000 psi（280 MN/m2）之前都是安全的，所以使用高抗拉强度的材料是有益的。格里菲斯的一个推论是，大体上，我们在小型结构中使用高强度金属和大工作应力要比在大型结构中更安全。结构越大，为安全起见，可承受的应力就越小。这也是限制大型船舶和桥梁尺寸的因素之一。

图 5–13 某些普通碳素钢中抗拉强度和断裂功之间的近似关系（图片来源：Bycourtesy of Professor W. D. Biggs）

图 5–13 所示的断裂功和抗拉强度之间的关系，对普通的工业碳素钢而言大致是正确的。要获得更好的强度与韧度组合，可能得使用合金钢，即熔铸了非碳元素的钢，但这对大尺寸结构来说可能太贵了。正是基于这些原因，所有钢材中大约有 98% 是低碳钢，即抗拉强度约为 60 000~70 000 psi 或 450 MN/m2 的软金属或可延展金属。

### 5.10 On the brittleness of bones

Children, you are very little,

And your bones are very brittle;

If you would grow great and stately,

You must try to walk sedately.

R. L. Stevenson, A Child's Garden of Verses

But, of course, the bones of children are not very brittle,* and Stevenson was writing rather charming nonsense. In the embryo, bones begin as collagen, or gristle, which is strong and tough but not very stiff (Young's modulus about 600 MN/m2). As the foetus develops, the collagen is reinforced by fine inorganic fibres called osteones. These are formed chiefly from lime and phosphorus and have a chemical formula which approximates to 3Ca3(PO4)2. Ca(OH)2. In the fully reinforced bone the Young's modulus is increased about thirtyfold to a value of about 20,000 MN/m2. However, our bones do not become fully calcified until some considerable time after birth. Naturally, young children are mechanically vulnerable, but on the whole they tend to bounce rather than break, as one can see on any ski-slope.

However, all bones are relatively brittle compared with soft tissues, and their work of fracture seems to be less than that of wood. This brittleness limits the structural risks which a large animal can accept. As we have already pointed out in connection with ships and machinery, the length of the critical Griffith crack is an absolute, not a relative distance. That is to say, it is just the same for a mouse as it is for an elephant. Furthermore the strength and stiffness of bone are much the same in all animals. This being so, it rather looks as if the largest size of animal which can be regarded as moderately safe is somewhere round about the size of a man or a lion. A mouse or a cat or a reasonably fit man can jump off a table with impunity; it is distinctly doubtful if an elephant could. In fact, elephants have to be very careful; one seldom sees them gambolling or jumping over fences like lambs or dogs. Really large animals, like whales, stick pretty consistently to the sea. Horses seem to present an interesting case. Presumably the original small wild horses did not very often break their bones, but now that man has bred horses big enough to carry him without tiring, the wretched creatures always seem to be breaking their legs.

It is well known that old people are particularly liable to break their bones, and this is generally attributed to a progressive em-brittlement of bone with age. No doubt this embrittlement does play some part in causing these fractures, but it does not seem as if it were always the most important factor. As far as I know, there are no reliable data on the change of work of fracture of bone with age, but, since the tensile strength is only reduced by about 22 per cent between the ages of twenty-five and seventy-five, it does not look as if there were a very dramatic reduction. Professor J. P. Paul, of the University of Strathclyde, tells me that his researches seem to indicate that a more important cause of fracture in old people is the progressive loss of nervous control over the tensions in the muscles. A sudden alarm may cause a muscular contraction which is enough to break off the neck of the femur, for instance, without the patient having experienced any external blow. When this happens the patient naturally falls to the ground -perhaps on top of some obstacle-so that the fracture is blamed, wrongly, on the fall rather than on the muscular spasm. It is said that similar fracture can occur in the hind leg of certain African deer when they are startled by a lion.

1 1 Joule (1J) = 107 ergs = 0.734 foot-pound = 0.239 calories. Note that one Joule is roughly the energy with which an ordinary apple would hit the floor if it fell off an ordinary table.

2 Since the oxygen consumption of the body is said to be higher during down-hill ski-ing than in any other human activity, much energy must also be got rid of in the muscles. However, most of the energy absorbed by the muscles is irrecoverable, and so the elastic strain energy storage of the tendons is no doubt to be preferred.

3 Figures 2 and 4 are, of course, schematic. Generally the force-draw diagram will not be a straight line; but the same principle applies.

4 On the other hand the rate of shooting of a cross-bow cannot match that of a hand-bow. The English longbow, for instance, could discharge up to fourteen arrows a minute and thus, when used en masse, could put up a very formidable cloud or barrage of missiles. It is calculated that about six million arrows were shot at Agincourt.

5 Recent finds at Kouklia in Cyprus indicate the existence of military catapults during the fifth century, though nothing is known about them. In any case Dionysius's seems to have been the first 'scientific' approach to the problem.

6 These were probably derived from the 'Spanish windlass' used in ancient ships. See Chapter 11, p. 224.

7 During the 1940 invasion scare two versions of the Roman ballista were made for use by the Home Guard in England. These weapons were intended to project petrol bombs against German tanks. However, since the range of both of these catapults was only about a quarter of that of the classical prototypes, it seems likely that their designers had omitted to read Vitruvius sufficiently carefully.

8 Actually, much of the resilience of anchor cables and tow ropes comes from their own weight, which causes them to sag. This is one of the reasons for preferring heavy wire or chain to organic ropes, which are much lighter.

9 The 'true' or theoretical maximum tensile stress required actually to pull the atoms apart is very high indeed, far higher than the 'practical' strength determined by means of ordinary tensile tests. See The New Science of Strong Materials, Chapter 3.

10 This is often the same thing as the 'free surface energy', which is closely related to the surface tension of both liquids and solids, and which is frequently bandied about in discussions on materials science. See for instance, The New Science of Strong Materials, Chapter 3.

11 See The New Science of Strong Materials, Chapters 3 and 9, for an elementary account of the dislocation mechanism; for a fuller description see, for instance, The Mechanical Properties of Matter by Sir Alan Cottrell (John Wiley, 1964 etc.).

12 Again, see The New Science of Strong Materials (second edition), Chapter 8.

13 It might perhaps be supposed that Lg would correspond to O Y on the diagram, but a little thought will show that this is not the case. The negative amount of energy, ZX, which we have to feed into the system to get the crack going represents the margin of safety or threshold energy. (This is, in fact, the true 'factor of safety'.)

14 Because strain energy = ½ es, which can be written s2/2E, since E = s/e.

15 There are medical conditions where the bones of quite young people become very brittle, but this state of affairs is rare. An orthopaedic surgeon tells me that the causes are by no means understood.

骨骼的脆度

孩子们，小小的个儿，

脆脆的骨骼；

若要长得壮些，

务必走得慢些。

—— 史蒂文森，《童诗园》

当然，儿童的骨骼也没那么脆，[14] 史蒂文森不过是在文绉绉地胡扯。在胚胎阶段，骨骼一开始是胶原蛋白或软骨，强韧但刚度不太高（杨氏模量约为 600 MN/m2）。随着胎儿的发育，胶原蛋白靠骨单位这种精细的无机纤维加固。骨单位主要是由石灰和磷形成的，化学式近似为 3Ca3(PO4)2·Ca(OH)2。在完全加固的骨骼中，杨氏模量增长为原来的 30 倍左右，约为 20 000 MN/m2。但是，我们的骨骼在出生后的相当长时间里才会完全钙化。虽然年幼的孩子易受机械创伤，但大体上他们的骨骼更倾向于回弹而非断裂，就像在任何滑雪坡上可看到的那样。

同软组织相比，所有骨头都比较脆，它们的断裂功似乎比木材的还小。这种脆度限制了大型动物能承受的结构性风险。我们在探讨船舶和机械的相关方面时已经指出，临界格里菲斯裂缝长度是一个绝对而非相对的距离，即对老鼠和对大象来说它都是一样的。此外，所有动物骨骼的强度和刚度都差不多。如此看来，能被视为适度安全的最大动物体形似乎与人或狮子比较接近。老鼠、猫或健壮的人都能安然无恙地跳下桌子；但如果说一头大象也可以，显然很可疑。事实上，大象必须非常小心，很难见到它们像羔羊或小狗那样跳过篱笆。真正巨大的动物，像鲸鱼，始终待在海里。马似乎是个有趣的例子：据推测，原始的小型野马不常骨折，但现在人类驯养的马已经大到足以驮人而不知疲倦，这些可怜的动物似乎经常折断腿。

众所周知，老人特别容易骨折，这常常被归因于年龄增长带来的骨骼脆化。骨骼脆化无疑对骨折起到了推波助澜的作用，但它并非最重要的因素。据我所知，没有可靠的数据支持骨骼的断裂功随年龄变化的说法，而抗拉强度从 25 岁到 75 岁只下降了约 22%，看起来并不是大幅降低。思克莱德大学的保罗教授（J. P. Paul）告诉我，他的研究表明，老人骨折的一个更重要的诱因是逐渐失去了对肌肉拉伸的神经控制。比如，突发的惊吓可能导致肌肉收缩。当这种情况发生时，病人会倒在地上，或者倒在某些障碍物上，以至于骨折被错误地归咎于跌倒而不是肌肉痉挛。据说某些非洲的鹿被狮子吓一跳时，它们的后腿也会发生类似的骨折。

[14] 在有些医疗条件下，年轻人的骨骼变得非常脆，但这种情况很罕见。一位骨外科医生告诉我原因尚未知。