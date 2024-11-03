## 记忆时间

## 卡片

### 0101. 主题卡 —— 电磁学里的两大核心概念通量和环流

信息原则「0101 Electromagnetism」

There are two mathematically important properties of a vector ﬁeld whichwe will use in our description of the laws of electricity from the ﬁeld point ofview. Suppose we imagine a closed surface of some kind and ask whether weare losing「something」from the inside; that is, does the ﬁeld have a quality of「outﬂow」? For instance, for a velocity ﬁeld we might ask whether the velocity isalways outward on the surface or, more generally, whether more ﬂuid ﬂows out(per unit time) than comes in. We call the net amount of ﬂuid going out throughthe surface per unit time the「ﬂux of velocity」through the surface. The ﬂowthrough an element of a surface is just equal to the component of the velocityperpendicular to the surface times the area of the surface. For an arbitrary closedsurface, the net outward ﬂow — or ﬂux — is the average outward normal componentof the velocity, times the area of the surface:

```
Flux = average normal component x surface area
```

In the case of an electric ﬁeld, we can mathematically deﬁne somethinganalogous to an outﬂow, and we again call it the ﬂux, but of course it is not theﬂow of any substance, because the electric ﬁeld is not the velocity of anything. Itturns out, however, that the mathematical quantity which is the average normalcomponent of the ﬁeld still has a useful signiﬁcance. We speak, then, of theelectric ﬂux — also deﬁned by Eq. (1.4). Finally, it is also useful to speak of theﬂux not only through a completely closed surface, but through any boundedsurface. As before, the ﬂux through such a surface is deﬁned as the averagenormal component of a vector times the area of the surface. These ideas areillustrated in Fig. 1-3.

Fig. 1-3. The ﬂux of a vector ﬁeldthrough a surface is deﬁned as the aver-age value of the normal component of thevector times the area of the surface.

There is a second property of a vector ﬁeld that has to do with a line, ratherthan a surface. Suppose again that we think of a velocity ﬁeld that describes theﬂow of a liquid. We might ask this interesting question: Is the liquid circulating?

By that we mean: Is there a net rotational motion around some loop? Supposethat we instantaneously freeze the liquid everywhere except inside of a tubewhich is of uniform bore, and which goes in a loop that closes back on itself asin Fig. 1-4. Outside of the tube the liquid stops moving, but inside the tube itmay keep on moving because of the momentum in the trapped liquid — that is,if there is more momentum heading one way around the tube than the other.We deﬁne a quantity called the circulation as the resulting speed of the liquid inthe tube times its circumference. We can again extend our ideas and deﬁne the「circulation」for any vector ﬁeld (even when there isn’t anything moving). Forany vector ﬁeld the circulation around any imagined closed curve is deﬁned asthe average tangential component of the vector (in a consistent sense) multipliedby the circumference of the loop (Fig. 1-5):

```
Circulation = average tangential component x distance around
```

You will see that this deﬁnition does indeed give a number which is proportionalto the circulation velocity in the quickly frozen tube described above.

With just these two ideas — ﬂux and circulation — we can describe all the lawsof electricity and magnetism at once. You may not understand the signiﬁcanceof the laws right away, but they will give you some idea of the way the physics ofelectromagnetism will be ultimately described.

Fig. 1-4. (a) The velocity ﬁeld in a liquid. Imagine a tube of uniform cross section that follows an arbitrary closed curve as in (b). If the liquid were suddenly frozen everywhere except inside the tube, the liquid in the tube would circulate as shown in (c).

1-3 矢量场的特征

矢量场在数学上有两个重要性质，我们将利用它们从场的观点来描述电学定律。若我们想象某种闭合面，并试问是否有「某种东西」从里面流失；这就是说，该场是否有一个「流出」的量？

例如，对于速度场，我们也许要问，该面上的速度是否总是向外，或更普遍地问，是否（每单位时间）流出的流体比流入的多。我们把单位时间流经该面的净流体量称为通过该面的「速度通量」。流经一个面积单元的流量恰好等于垂直该面积的速度分量乘以该面积。对于任一个闭合面，净流出量（或通量）等于速度向外的法向分量的平均值乘以该闭合曲面的面积：

```
通量 = 平均法向分量 x 曲面的面积
```

在电场的情况下，我们可以在数学上定义与流出量相类似的东西，又称作通量，但这当然不是任何物质的流动，因为电场并不是任何东西的速度。然而，事实证明，场法向分量的平均值这个数学上的量仍有其实用意义。于是，我们来谈谈电通量 一一 这也是由式 1.4 定义的。最后，不仅谈论通过一个完全闭合曲面的通量，而且还谈论通过任一个有边界的曲面的通量这也是很有用处的。综上所述，通过这样一个面的通量被定义为矢量的法向分量的平均值乘以该曲面的面积。这些概念如图 1-3 所示。

图 1-3 矢量场通过一个曲面的通量，定义为矢量的法向分量的平均值乘以该曲面的面积

矢量场还有第二个性质，它必须用一条曲线而不是用一个面才能得出。让我们再来回顾一下描写液体流动的速度场，也许会提出这样一个有趣的问题：该液体是否存在环流？我们所说的环流，是指是否有围绕某个环路的净旋转运动？

如图 1-4 所示，假定除在一条口径均匀的环状闭合管子里的液体外，液体突然处处都被冻结了。也就是说，管外的液体都停止了流动，但由于被禁锢的流体内存在着动量（这就是说，围绕管子沿一个方向的动量大于沿另一个方向的动量），所以管内的液体仍可继续流动。我们把管内液体的有效速率乘以该管周长这个量定义为环流。

我们再把上述概念加以引申，而定义任一矢量场的「环流」（即使没有任何东西在流动亦然）。对于任一矢量场，绕任一想象中的闭合曲线的环流可以定义为矢量（沿一致向指）的平均切向分量乘以该回路的周长（图 1-5），即：

```
环流 = 平均切向分量 x 绕行距离
```

你们将会看到，这一定义确实给出了一个正比于上述迅速被冻结的管子里的环流速度的数值。

图 1-4 (a）液体中的速度场；设想有截面均匀、按照图（b）所示的任一闭合曲线安放的管子；假如液体除管内的外，处处都被冻结，那么管里的液体便将按图（c）所示的那样循环流动

只要利用这两个概念 一一 通量与环流 一一 我们就能立即描述电学和磁学的所有定律。你可能不会一下子就理解其意义，但它们将给出有关电磁方面物理学基本描述方法的一些概念。

2『电磁学里的两大核心概念通量和环流。做一张主题卡片。（2022-05-17）』

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 —— 磁铁有磁场的原理

信息原则「0101 Electromagnetism」

简言之，电流和磁铁均会产生磁场。且慢！试问磁铁究竟是什么？如果磁场是由运动电荷产生的，那么，来自一块磁铁的磁场是否有可能也是由于电流的原因呢？看来的确是这样。我们可以将实验中的条形磁铁用一个导电线圈来代替，如图 1-9 所示。当电流通过线圈同时也有电流通过在线圈上面的那根直导线 一一 时，我们便会观察到导线的运动与以前用磁铁而不用线圈时完全一样。换言之，线圈里的电流模仿了一块磁铁。因此，看来一块磁铁的作用就如同它含有一种永恒的环行电流一样。事实上，我们可以用铁原子中的恒定电流来理解磁铁。在图 1-7 中，作用在磁铁上的力就是由式（1.1）中的第二项引起的。

究竟这些电流是从哪里来的呢？一种可能来自原子轨道中电子的运动。实际上虽然对于某些材料来说这是正确的，但对铁来说却是不正确的。一个电子，除了在原子中环行之外，还绕它本身的轴旋转 一一 有些像地球的自转 —— 正是由于自旋所产生的电流才为铁提供了磁场（我们说「有些像地球的自转」，是因为这一问题在量子力学中竟是那么奥妙，以致一些经典概念并不能真正恰当地描述这些事物）。在大多数物质中，有些电子这样自旋，另一些电子那样自旋，所以磁性互相抵消；可是在铁里 一一 由于某个我们将在以后加以讨论的神秘原因 一一 有许多电子却绕着它们的排列整齐的轴旋转着，这正是磁性的起源。

1『磁铁有磁场的原理，做一张信息数据卡片。』—— 已完成

### 0601. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

