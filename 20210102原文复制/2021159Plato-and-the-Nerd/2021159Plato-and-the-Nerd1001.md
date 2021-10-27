## 1001. Determinism

· · · in which I argue that determinism is a property of models not of the physical world; that determinism is an extremely valuable property, one that has historically delivered considerable payoffs in engineering and science; that deterministic models may not be usefully predictive because of chaos and complexity; that families of deterministic models that embrace both discrete and continuous behaviors are incomplete; and that nondeterministic models, used explicitly and judiciously, play an essential role in engineering.

1001 决定论

在本章，我将会讨论，确定性是模型的属性，而不是物理世界的属性；确定性是一种极具价值的属性，它在历史上为工程和科学都带来了可观的回报；由于混沌和复杂性，确定性模型无法有效地进行预测；包含离散和连续行为的确定性模型家族是不完备的；明智而审慎地使用非确定性模型会在工程中产生至关重要的作用。

### 10.1 Laplace's Demon

The previous three chapters show definitively that we cannot know everything. Of course, each of us already knew that about ourselves, but these results are more fundamental. They assert that not everything is knowable. If we limit our study to computational processes, those given algorithmically by software, then Turing's result shows that we cannot tell what some programs will do just by looking at the code. If we broaden our study to formal mathematical models, then Gödel's result shows that we will always be able to construct models that we cannot determine to be true or false (or, worse, that end up being both true and false). Moreover, cardinality arguments show that there are many more possible information-processing functions than there are computer programs, mathematical models, or even descriptions in any given language. Consequently, some functions are not computations, cannot be modeled mathematically, and cannot even be described (completely) in any language we have. Unless nature, for some inexplicable reason, limits itself to only the tiny subset of functions that are computable and describable in a language we have, nature will inevitably continue to throw things at us that we cannot understand. To a scientist, this may be frustrating, but to an engineer, it simply means that the horizon for creativity is infinitely far away. There are no bounds to what we can do because we can continue to invent new languages and formalisms, and because they will never be complete, we will never be finished.

Because we can't know everything, we need systematic ways to deal with uncertainty. In the next chapter, I will directly address how to model uncertainty with probabilities. Before we can do that, however, we need to address the question of whether uncertainty is caused by the limits of what we can know or some intrinsic randomness in the world or in our models of the world. Many of the mathematical models and computer programs that we construct are deterministic, which suggests that we should be able to know quite a bit about them unless they fall into the Turing and Gödel traps. Most computer programmers strive to avoid these traps, yielding understandable programs, and also to create deterministic programs. However, this notion of determinism is not a simple one. We can't confront uncertainty without first confronting determinism.

Determinism is a deceptively simple idea that has vexed thinkers for a long time. Broadly, determinism in the physical world is the principle that everything that happens is inevitable, preordained by some earlier state of the universe or by some deity. For centuries, philosophers have debated the implications of this principle, particularly insofar as it undermines the notion of free will. If the world is deterministic, then presumably we cannot be held individually accountable for our actions because they are preordained. 1

Determinism is quite a subtle concept, as is the notion of free will. John Earman, in his Primer on Determinism , admits defeat in getting a handle on the concept:

This is already enough to make strong the suspicion that a real understanding of determinism cannot be achieved without simultaneously constructing a comprehensive philosophy of science. Since I have no such comprehensive view to offer, I approach the task I have set myself with humility. And also with the cowardly resolve to issue disclaimers whenever the going gets too rough. But even in a cowardly approach, determinism wins our unceasing admiration in forcing to the surface many of the more important and intriguing issues in the length and breadth of the philosophy of science. (Earman, 1986, p. 21)

But Earman insists that「determinism is a doctrine about the nature of the world.」I will circumvent the most treacherous difficulties by instead adopting a principle that I first learned from the Austrian computer scientist Hermann Kopetz, who asserted that determinism is a property of models and not a property of the physical world. This thesis does not diminish my fascination with the deep questions that Earman addresses, but it certainly does make it easier to apply the concept of determinism to engineered systems.

As a property of models, determinism is relatively easy to define:

A model is deterministic if given an initial state of the model, and given all the inputs that are provided to the model, the model defines exactly one possible behavior .

In other words, a model is deterministic if it is not possible for it to react in two or more ways to the same conditions. Only one reaction is possible. In this definition, I have italicized words that must be defined within the modeling paradigm to complete the definition, specifically,「state,」「input,」and「behavior.」

For example, if the state of a particle is its position x ( t ) in a Euclidean space at a time t , where both time and space are continuums, and if the input F ( t ) is a force applied to the particle at each instant t , and the behavior is the motion of the particle through space, then Newton's second law, equation (4096), is a deterministic model.

Two useful variations of this idea are evident immediately. First, a model may not have any inputs, in which case it is called a「closed model.」For example, if we assume that the universe is everything there is, then any model of the universe cannot have any inputs. Nothing outside the universe exists to provide those inputs. A closed model is deterministic if given an initial state, exactly one behavior is possible.

Second, a deterministic model may be reversible. In this case, given the state of the model at any particular time, and given the inputs at all times (if there are any inputs), both the past and future of the model are uniquely defined. There is only one possible past and only one possible future. Put another way, in a closed reversible deterministic model, the behavior for all time is determined by the state at any one time.

One reason that this simple concept has been so problematic is that all too often, when speaking of determinism, the speaker is confusing the map for the territory. To even speak of determinism, we must define「input,」「state,」and「behavior.」How can we define these things for an actual physical system? Any way we define them requires constructing a model. Hence, an assertion about determinism will actually be an assertion about the model not about the thing being modeled. Only a model can be unambiguously deterministic, which underscores Earman's struggle to pin down the concept.

Consider that any given physical system inevitably has more than one valid model. For example, a particle to which we are applying a force exhibits deterministic motion under Newton's second law but not under quantum mechanics, where the position of the particle will be given probabilistically. However, under quantum mechanics, the evolution of the particle's wave function is deterministic, following the Schrödinger equation (I will say more about this later). If the「state」and「behavior」of our model are the wave function, then the model is deterministic. If instead the state and behavior are the particle's position, then the model is nondeterministic. It makes no sense to assign determinism as a property to the particle. It is a property of the model.

If I have a deterministic model that is faithful to some physical system, then this model may have a particularly valuable property: the model may predict how the system will evolve in time in reaction to some input stimulus. This predictive power of a deterministic model is a key reason to seek deterministic models.

We already know that some deterministic models are not predictable. For example, Turing showed that we cannot predict, for all computer programs, whether the program execution will halt for a particular input, even if the program is deterministic. It turns out that there are many more deterministic models that are also not predictable because of chaos and complexity.

In chapter 2 , I made a distinction between the engineering and scientific uses of models. An engineer seeks a physical system to match a model, whereas a scientist seeks a model to match a physical system. For these two uses, determinism plays different roles. For an engineer, the determinism of a model is useful because it facilitates building confidence in the model . In chapter 4 , I talked about logic gates as deterministic models of electrons sloshing around in silicon. The determinism of the logic gate model is valuable: it enables circuit designers to use Boolean algebra to build confidence in circuit designs that have billions of transistors. The model predicts behaviors perfectly , in that an engineer can determine how a logic gate model will react to any particular input, given any initial state.

Of course, the usefulness of the logic gate model also depends on our ability to build silicon structures that are extremely faithful to the model. We have learned to control the sloshing of electrons in silicon so that, with high confidence, a circuit will emulate the logic gate model billions of times per second and operate without error for years.

Herein lies an essential difference between science and engineering. To a scientist, for a deterministic model to be useful, it must faithfully describe the behavior of a given physical system. To an engineer, for a deterministic model to be useful, it must be possible to construct a physical system that is faithful to the model. In both cases,「faithful」means that the behaviors of the model and the physical system match to a high degree of accuracy. However, the goals are different, and therefore deterministic models will be useful to an engineer in situations where the same models are not useful to a scientist and vice versa.

Some of the most valuable engineering models are deterministic. In addition to logic gates, we also have digital machines, instruction set architectures, and programming languages, most of which are deterministic models. The Turing machines in chapter 8 are also deterministic. The determinism of all these models has proved extremely valuable historically. The information technology revolution is built on the determinism of these models.

For a scientist, fundamentally, when considering the use of deterministic models, it matters quite a lot whether the physical system being modeled is also deterministic. Is the sloshing of electrons in silicon deterministic? If only a model can be unambiguously deterministic, then how can we answer this question? The fact is that almost all established laws of physics are deterministic models, and most are also reversible. Ohm's law for resistors and Faraday's law for inductors from chapter 2 are both reversible deterministic models. For a resistor, if I define the input to be a voltage and the output to be the current, then Ohm's law gives me a deterministic model of a resistor. The model is described by equation (1024). Newton's laws of motion and Einstein's theories of relativity are deterministic. Interestingly, even basic laws used to study the thermodynamics of gasses such as Boyle's law and Charles' law are deterministic, although they do not require the underlying motion of gas molecules to be deterministic. They define state, input, and output in terms of pressure, temperature, and volume not in terms of positions and momentums of the gas molecules. Even quantum mechanics is almost entirely deterministic, in that the evolution of the wave function as defined by the Schrödinger equation is deterministic.

The question of whether the physical world is deterministic has remained unanswered for a long time. In the early 1800s, the French scientist Pierre-Simon Laplace made an argument for determinism in the universe. Laplace argued that if someone (a demon) were to know the precise location and velocity of every particle in the universe, then the past and future locations and velocities for each particle would be completely determined and could be calculated from the laws of classical mechanics (Laplace, 1901). Is this true?

As I've pointed out before, the laws of classical mechanics, such as Newton's second law, equation (4096), are wrong. They need to be adjusted using Einstein's relativity to be precise, although the imprecision will be insignificant for most applications of classical mechanics. Moreover, the notions of position and velocity that underly the notion of「state」in classical mechanics are undermined by quantum mechanics, although again only significantly at extremely small scales. If the question is the fundamental scientific question of whether the world is deterministic, then any imprecision, no matter how small, matters.

What about the probabilistic nature of the wave function in quantum mechanics? Does this undermine the idea of a deterministic universe? Stephen Hawking argues that it does not:

At first, it seemed that these hopes for a complete determinism would be dashed by the discovery early in the 20th century that events like the decay of radioactive atoms seemed to take place at random. It was as if God was playing dice, in Einstein's phrase. But science snatched victory from the jaws of defeat by moving the goal posts and redefining what is meant by a complete knowledge of the universe. (Hawking, 2002)

Hawking is referring to the fact that the Schrödinger equation, which describes how a wave function evolves in time, is deterministic.「In quantum theory, it turns out one doesn't need to know both the positions and the velocities [of the particles].」It is enough to know how the wave function evolves in time.

Although I can't possibly explain it fully (I'm not convinced that anyone can), it is worth a brief aside on wave functions because they represent the only established nondeterminism that I know of in widely accepted models of fundamental physics. In quantum mechanics, the position of a particle in space is not described simply as a point in a three-dimensional Euclidean geometry but rather by a wave function, a squiggle that changes shape and moves in space over time. The square of the value of the wave function at a point in space and time represents the relative probability of finding the particle at that position at that time. 2 The use of probabilities, a subtle concept that I discuss in chapter 11 , implies that the position of the particle is nondeterministic, and the wave function gives the relative likelihoods that an observer will find the particle at any particular point in space.

In 1926, Erwin Schrödinger, a Nobel Prize-winning Austrian physicist, published what is now a key centerpiece of quantum mechanics, the Schrödinger equation. This equation describes the evolution in time and space of the wave function, and as Hawking points out, that evolution is deterministic.

The wave function represents probabilities, and its interpretation is fraught with difficulties. In what is now called the Copenhagen interpretation, originally proposed in the years 1925 to 1927 by the Danish physicist Niels Bohr and the German physicist Werner Heisenberg, the state of a system continues to be defined by probabilities until an external observer observes the state, and only at that point do the probabilities influence the outcome. Prior to being observed, all possible outcomes represented by the probabilities continue to remain possible. This requires an「observer」who is somehow separate from the system and measures the position of the particle. The usual interpretation of a probability is that it specifies the likelihood of observing a particular outcome of an experiment. Under this interpretation, a probability makes sense only if the experiment is performed and the outcome is observed. How can any observer be separate from the physical system?

Schrödinger pointed out difficulties of the Copenhagen interpretation, famously illustrating them with what is now called「Schrödinger's cat.」In this thought experiment, a cat is locked in a chamber containing a mechanism that will release a poison if a particular radioactive atom decays, emitting radiation. The decay of a radioactive atom is governed by a wave function, so the decay event is governed by probabilities. The probabilities evolve deterministically according to the Schrödinger equation, but under the Copenhagen interpretation, no actual experiment governed by those probabilities occurs until an observer observes the system. Because all possibilities remain possible until an observer observes the system, Schrödinger argued that the cat must be both alive and dead until such observation occurs. Only then does it become one or the other.

These difficulties have led to endless debateabout the meaning of the wave function, with a variety of sometimes bizarre positions emerging. Some of these positions posit that the observer somehow lives outside of physics, that the observer is God, and that this observer is the essence of human cognition. In the 1950s, the physicist Hugh Everett III dispensed with the observer, bundling observer and observed under a single wave function that evolves deterministically under the Schrödinger equation. This view is often called the「many worlds」view because it can be interpreted to mean that all outcomes exist simultaneously in an infinite number of parallel universes. In this view, we can take the state of a system to be its wave function, and then quantum dynamics is deterministic.

So Laplace's question still stands, except that now we have to update it to consider the「state」of the system to be represented by its wave function not by the positions and velocities of its particles, and we have to account for the curvature of space time no matter how small. If we make these adjustments, is the resulting model of the universe deterministic? The question of whether the physical world itself is deterministic is probably unanswerable. 3 However, we can answer the question of whether any particular model of the universe is deterministic. We need to keep distinct the map and the territory.

In 2008, David Wolpert used Georg Cantor's diagonalization technique to prove that Laplace's demon cannot exist (Wolpert, 2008). His proof relies on the observation that such a demon, were it to exist, would have to exist in the very physical world that it predicts. This results in a self-referentiality that yields contradictions, not unlike Turing's undecidability discussed in chapter 8 and Gödel's incompleteness theorems discussed in chapter 9 . In fact, the result is a kind of essential incompleteness that must result from any deterministic model of the universe, similar to Hawking's observation quoted earlier. Binder (2008), in a review of Wolpert's work, observes poignantly,「It is possible, though, that these various theories, along with all that we have learned in physics and other scientific disciplines, will yet merge into the best science can do: a theory of almost everything.」That theory, incomplete as it is, today consists almost entirely of deterministic models.

These debates are fascinating and more philosophical than scientific, but they are largely irrelevant to the engineering use of models. The value of a deterministic logic gate model does not depend at all on whether the sloshing of electrons in silicon is deterministic. It depends only on whether we can build silicon structures that emulate the model with high confidence. We do not need and cannot achieve perfection. As Box and Draper say, all models are wrong, but some models are useful, and logic gates have proved extremely useful.

Although determinism can help predict how a system will evolve in time, I will show in section 10.2 that even a deterministic model may not predict future behavior well. It may be foiled by a phenomenon called chaos; by complexity, where it simply becomes impractical to compute the predictions; or even more simply by an accumulation of error. In such cases, nondeterministic models may become valuable.

Every model has a bounded regime of validity. Newton's laws are accurate at modest speeds and scales, but even a system that is well described by Newton's laws may evolve to be outside the regime of validity of the model. Suppose that we apply a modest constant force for a long time to an object in space. Then Newton's second law predicts that the velocity will grow without bound, eventually exceeding the speed of light, in violation of Einstein's special theory of relativity. Compared with an actual physical system, the error in the model's prediction will become arbitrarily large. Nevertheless, for a reasonably short time horizon, with small forces and large masses, Newton's second law will predict behavior extremely well, and such prediction is valuable. Similarly, Einstein's general theory of relativity explains gravity at large scales, whereas quantum mechanics explains interactions of matter at small scales, and attempts to unify these remain unsatisfactory.

Deterministic models may also be foiled by complexity. A classic example from thermodynamics is the pressure exhibited by a gas in a chamber. This can be modeled as collisions of individual molecules with each other and with the walls of the chamber. In Laplace's day, these collisions would have been governed by Newton's deterministic laws of motion, but such models are intractable. Any attempt to compute the individual motions of even a relatively small number of molecules under such laws of motion would overwhelm even the most powerful computers today. As a consequence, physicists consider these motions to be nondeterministic and rely on the statistics of large numbers of random events to exhibit behaviors that are well modeled deterministically by Boyle's and Charles' laws. The emergence of deterministic models from large numbers of nondeterministic behaviors is a consequence of the law of large numbers , considered in the next chapter. Our ability to model transistors as deterministic switches relies on similar statistical arguments.

Complex behaviors can arise from even simple models, which can exhibit a phenomenon called「chaos.」Interestingly, the inability to make predictions for chaotic models despite their determinism can actually be a valuable property. The technology of encryption, which obscures the content of messages, depends on both determinism (to ensure that the message can be decrypted by the intended recipient) and an inability to make predictions (to protect the message from eavesdroppers). Interestingly, although cryptographers today depend on deterministic models, they hope the physical world is actually nondeterministic and some form of「true randomness」can be tapped to make stronger encryption techniques. True randomness, it turns out, is extremely difficult to achieve.

A nondeterministic model may also lend itself to prediction, but instead of predicting a single behavior, it predicts a family of behaviors. Each behavior in the family is possible. A nondeterministic model of a coin toss, for example, simply states that both heads and tails are possible. A deterministic model of a coin toss remains elusive. Even if we laboriously construct one using some exact model of the shape and material properties of the coin and the surface on which it lands, the predictive value of the model would be poor because even the smallest error in our model could drastically change the outcome of a toss. Despite its uselessness, Karl Popper, high priest of scientific positivism, insists on such a model for the toss of a die:

One sometimes hears it said that the movements of the planets obey strict laws, whilst the fall of a die is fortuitous, or subject to chance. In my view the difference lies in the fact that we have so far been able to predict the movement of the planets successfully, but not the individual results of throwing dice. In order to deduce predictions one needs laws and initial conditions; if no suitable laws are available or if the initial conditions cannot be ascertained, the scientific way of predicting breaks down. In throwing dice, what we lack is, clearly, sufficient knowledge of initial conditions. With sufficiently precise measurements of initial conditions it would be possible to make predictions in this case also. (Popper, 1959, p. 198)

The root of this insistence is a firm belief in the determinism of the underlying physical system. However, predictions can only be made with models, and no such model will be faithful to the physical system in any useful way, so an irreconcilable gap remains here.

Regardless of whether the underlying physical world is deterministic, a nondeterministic model may be augmented with probabilities, which attach a measure of our uncertainty about the outcome. The unfair coin toss considered in chapter 7 , where we expect only 1 of 10 tosses to produce tails, can be modeled with probability 0.1 for tails and 0.9 for heads. I will explore probabilistic models in chapter 11 , but for now let's just focus on deterministic models.

10.1 拉普拉斯妖

之前的三章已经明确表明，我们不可能无所不知。当然，我们每个人都已经了解我们自身，但这些结果是根本性的。它们断言，并非一切都是可知的。如果我们把自己的研究仅仅局限于计算过程，也就是那些由软件以算法形式给出的过程，那么图灵的结果表明，我们不能仅仅通过查看代码来判断某些程序的功能是什么。如果我们把研究的范围扩展到形式化的数学模型，那么哥德尔的研究结果表明，我们总是能够构建我们无法确定为真或为假的模型（或者更糟的是，最终是既为真又为假的）。此外，势参数表明，可能的信息处理功能比计算机程序、数学模型甚至任何特定语言能给出的描述都要多。因此，有些功能是不可计算的，不能用数学的方式进行建模，甚至不能用我们所拥有的任何语言来（完全地）描述。除非大自然出于某种莫名其妙的原因，将自己局限于可计算的和我们的语言可描述的功能的极小子集，否则大自然将不可避免地继续向我们抛出一些我们无法理解的事物。对科学家来说，这可能是非常令人沮丧的事情。但对于工程师而言，这只是意味着创造力的空间是无限的。我们能做的事情是没有边界的，因为我们可以继续发明新的语言和形式化方法，而且，因为它们永远不会是完备的，所以我们永远不会停止。

因为我们无法知晓一切，所以我们需要系统的方法来应对不确定性。在下一章，我将直接讨论如何用概率来建模不确定性。然而，在我们能够做到这一点之前，我们先要解决这样一个问题，即不确定性是由我们知识的局限性造成的，还是由世界或我们的世界模型中的某种内在随机性造成的。我们所建立的许多数学模型和计算机程序都是确定性的，这意味着我们应该对它们有相当多的了解，除非它们落入图灵和哥德尔的陷阱。大多数计算机程序员都会努力避免落入这些陷阱，试图开发出可以理解的程序，同时也创建确定性的程序。然而，决定论的概念并不那么简单。我们只有首先面对决定论，然后才能面对不确定性。

决定论是一个看似简单的概念，却在长久以来一直困扰着思想家。从广义上讲，物理世界中的决定论是这样一种原则，即发生的一切都是不可避免的，是由宇宙的某些早期状态或某个神灵预先决定的。几个世纪以来，哲学家一直就这一学说的含义进行着争论，特别是在它削弱了自由意志的概念时。如果世界是确定性的，那么我们大概无法为自己的行为负责，因为它们是注定的。决定论是一个相当微妙的概念，就像自由意志的概念一样。约翰·厄尔曼在《决定论入门》一书中承认，他无法完全理解和把握这个概念：

这足以使人们产生强烈的怀疑，如果不同时构建一种全面的科学哲学，就不可能真正理解决定论。由于我无法提供如此全面的科学哲学观点，所以我不得不以谦卑的姿态来完成我为自己设定的任务。当情况变得过于艰难时，我会慎重地发表免责声明。但是，即使是采用慎重的方法，决定论把科学哲学的许多重要且非常有趣的问题揭示出来的过程，也赢得了我们持续的赞美。（厄尔曼，1986:21）

但是，厄尔曼坚持认为，「决定论是一种关于世界本质的学说」。在此，我想采取迂回的方式，先绕过最难走的荆棘之路，转而采用我第一次从奥地利计算机科学家赫尔曼·科佩茨那里学到的原则。科佩茨断言，确定性是模型的属性，而不是物理世界的属性。这个观点并没有减少我对厄尔曼所阐述的深层次问题的兴趣，但是，它的确使决定论的概念更容易应用到工程系统中。

作为模型的一种属性，确定性的定义相对容易：

在给定模型的初始状态且给定模型的所有输入时，如果该模型只定义了一种可能的行为，那么该模型是确定性的。

换句话说，如果一个模型不可能以两种或两种以上的方式对相同的条件做出反应，它就是确定性的。也就是说，它只会对此做出一种反应。在这个定义中，我用加粗的字体（必须在建模范式中定义的概念）来完成相关的定义，具体而言，就是「状态」、「输入」和「行为」。

例如，如果一个粒子在 t 时刻的状态是它在欧几里得空间中的位置 x（t），时间和空间都是连续统，同时，如果输入值 F（t）是在每一个时刻 t 施加给粒子的力，而且行为就是粒子在空间中的运动，那么，由牛顿第二定律可知，方程（4 096）就是一个确定性模型。

显然，这一思想立即会形成两个有用的变体。首先，模型可能没有任何输入，在这种情况下，它被称为「封闭模型」。例如，我们假设宇宙就是一切的存在，那么宇宙的任何模型都不可能有任何的输入。宇宙之外不存在任何事物提供这些输入。一个封闭模型是确定性的，换言之，给定一个初始状态，它只会有一种可能的行为。

其次，确定性模型可能是可逆的。在这种情况下，给定模型在任何特定时间的状态，以及在一切时间的输入（如果存在），那么该模型的过去和未来都会被唯一地定义，即该模型只有一个可能的过去和一个可能的未来。换句话说，在一个封闭的可逆确定性模型中，任何时刻的行为都是由该时刻的状态决定的。

这个简单的概念之所以如此成问题，原因之一就是 —— 在谈到确定性的时候，说话人常常将地图混淆为地域，即误将地图上的标记视为真正的地域。在提及确定性之前，我们必须先给出「输入」、「状态」和「行为」的定义。我们如何为一个实际的物理系统定义这些概念呢？不论以何种方式，我们都需要一个模型才能对它们进行定义。因此，关于确定性的断言实际上是关于模型的断言，而非关于被建模事物的断言。只有模型是确定性的，这一点毫无疑问。当然，这也凸显了厄尔曼为确定这一概念所做的努力。

考虑到任何给定的物理系统几乎总会有一个以上的有效模型。例如，在牛顿第二定律下，一个我们施加了力的粒子会表现出确定性的运动，而在量子力学下，粒子的位置是概率性的。然而，在量子力学下，粒子的波函数的演化是确定性的，其遵循薛定谔方程（又称薛定谔波动方程，我将在后面的内容中详细阐述）。如果一个模型的状态和行为是波动方程，那么这个模型是确定性的。相反，如果状态和行为是粒子的位置，那么模型是非确定性的。将确定性作为粒子的一种属性是完全没有意义的。可以说，确定性是模型的属性，而非粒子的属性。

如果我有一个与某个物理系统相符合的确定性模型，那么这个模型可能会有一条特别有价值的性质：该模型可以预测该系统在响应某些输入激励时将如何演化。确定性模型的这种预测能力，正是人们寻求确定性模型的一个关键原因。

我们已经知道有些确定性模型是不可预测的。例如，图灵证明，对于所有的计算机程序，即使一个程序是确定性的，我们也不能预测该程序对于特定的输入是否会终止。事实证明，由于混沌和复杂性，还有更多的确定性模型也都是不可预测的。

在第 2 章中，我对模型的工程应用和科学应用进行了区分。工程师寻找一个物理系统来匹配一个构建的模型，而科学家寻找一个模型来匹配一个物理系统。对于这两种用法，确定性的作用不同。对于工程师来说，模型的确定性是非常有用的，因为这有助于树立起该模型内在的可信度。在第 4 章中，我讨论了逻辑门作为硅材料中电子流动的确定性模型。逻辑门模型的确定性是有价值的：它使电路设计人员能够使用布尔代数，在拥有数十亿个晶体管的电路设计中建立起可信度。该模型完美地预测了电路的行为，因为在给定任何一个初始状态时，工程师都可以确定逻辑门模型将如何对任何特定的输入做出反应。

当然，逻辑门模型的有用性也取决于我们能否构造出与模型高度吻合的硅结构。我们已经掌握了如何控制硅材料中的电子流动，这样一来，在高可信度的支持下，一个电路就能以每秒数十亿次的速度模拟逻辑门模型，并在数年内无误差地工作。

这就是科学与工程的本质区别。对于科学家来说，要使一个确定性模型是有用的，该模型必须能够高度一致地刻画特定物理系统的行为。另一方面，对于工程师来说，要使确定性模型有用，必须有可能构建一个高度符合于该模型的物理系统。在这两种情况下，「高度符合」都意味着模型的行为与物理系统的行为高度匹配，只不过二者的目标不同。因此，情况往往是这样的：一些确定性模型对科学家而言是无用的，对工程师来讲却是有用的，反之亦然。

一些最有价值的工程模型都是确定性的。除了逻辑门，我们还有数字机器、指令集体系架构和编程语言，其中大多数都是确定性模型。第 8 章的图灵机也是确定性的，所有这些模型的确定性在历史上都被证明极具价值。信息技术革命正是建立在这些模型的确定性之上的。

从根本上说，当科学家考虑使用确定性模型的时候，被建模的物理系统是否也是确定性的就非常重要。那么硅材料中的电子流动是确定性的吗？如果只有一个模型可能明确是确定性的，那么我们又该如何回答这个问题？事实上，几乎所有已确立的物理定律都是确定性模型，而且它们中的大多数也是可逆的模型，例如，第 2 章用于电阻的欧姆定律和用于电感的法拉第定律都是可逆的确定性模型。对于一个电阻，如果我把输入定义为电压，将输出定义为电流，欧姆定律就给出了一个电阻的确定性模型，表示为方程（1 024）。牛顿的运动定律和爱因斯坦的相对论也是确定性的。有趣的是，就连用来研究气体热力学的基本定律，如玻意耳定律和查理定律，也都是确定性的，尽管它们并不要求气体分子的基本运动是确定性的。它们用压力、温度和体积来定义状态、输入和输出，而不是用气体分子的位置和动量来定义。甚至量子力学也几乎完全是确定性的，因为薛定谔方程所定义的波函数的演化是确定性的。

物理世界是不是确定性的这一问题长期以来一直没有答案。19 世纪初，法国科学家皮埃尔 — 西蒙·拉普拉斯提出了宇宙决定论的观点。拉普拉斯认为，如果有一个恶魔知道宇宙中每个粒子的精确位置和速度，那么每个粒子在过去和未来的位置与速度就可以完全被确定，并可以根据经典力学定律加以计算（拉普拉斯，1901）。然而，真是这样的吗？

正如我之前指出的，经典力学定律，如方程（4 096）所表示的牛顿第二运动定律是错误的。它们需要用爱因斯坦的相对论进行调整才能精确，尽管这种不精确对于大多数经典力学的应用来说是微不足道的。此外，在经典力学中作为「状态」概念基础的位置和速度这两个概念被量子力学破坏了，尽管这种破坏是极其微小的。如果关于世界是否是确定性的这个问题是一个根本性的科学问题，那么任何的不精确，无论多么微小，都是很重要的。

量子力学中波函数的概率性质是怎样的？这一性质是否会破坏宇宙决定论这一观点？斯蒂芬·霍金认为并非如此：

起初，这些对完全决定论的希望似乎会因为 20 世纪早期的一些发现而破灭，例如，人们发现放射性原子衰变这样的事件似乎是随机发生的。用爱因斯坦的话来说，就好像是上帝在掷骰子。但是，科学通过调整目标以及重新定义宇宙完整知识的内涵，从失败的绝境中夺取了胜利。（霍金，2002）

霍金所指的事实是，描述波函数如何随时间演化的薛定谔方程是确定性的。「在量子理论中，人们不需要同时知道（粒子的）位置和速度」，只需要知道波函数如何随时间演化就够了。

虽然我不可能完全解释上面霍金所讲的那段话（我相信没有人能够做到这一点），但我们还是值得对波函数做一个简短的讨论，因为在被广泛接受的基础物理模型中，它们代表了我所知道的唯一被确立的非确定性。在量子力学中，粒子在空间中的位置并非被简单地描述为欧几里得三维几何中的一个点，而是以一个波函数来描述的，它是一种随时间改变形状并在空间中移动的波形曲线。波函数在某个空间和时间点上的值的平方，表示粒子在那个时刻出现在那个位置上的相对概率。概率这一精妙概念（我将在第 11 章中进行讨论）的使用，意味着粒子的位置是不确定的，同时，波函数表示观察者在空间中任何特定点找到粒子的相对可能性。

1926 年，诺贝尔奖得主、奥地利物理学家埃尔温·薛定谔给出了薛定谔方程，它现在被认为是量子力学的核心。这个方程描述了波函数在时间和空间上的演化。正如霍金指出的那样，演化是确定性的。

波函数代表了概率，对这一点的解释一直非常困难。在丹麦物理学家尼尔斯·玻尔和德国物理学家沃纳·海森堡 1925 年至 1927 年提出的哥本哈根诠释中，他们认为，一个系统的状态是持续由概率来定义的，直到外部观察者观测到这个状态，并且只有在那个时刻概率才会影响结果。在被观测到之前，由概率表示的所有可能的结果仍然是可能的。这需要一个独立于该系统的「观察者」来测量粒子的位置。通常对概率的解释是，它表明了观测到某一实验的特定结果的可能性。在这种解释下，只有在进行了实验且结果被观测到时，概率才有意义。但是，如何才能使观察者从物理系统中分离出来呢？

薛定谔指出了哥本哈根诠释的诸多难点，并以著名的「薛定谔的猫」来进行说明。在这个思想实验中，一只猫被关在一个封闭的匣子里，且这个匣子里有这样一种装置，如果某个特定的放射性原子衰变并发出辐射，这个装置就会释放一种毒素。放射性原子的衰变是由波函数决定的，所以衰变事件由概率决定。这个概率根据薛定谔方程确定地演化，但在哥本哈根诠释下，在观察者观测这个系统之前，由这些概率决定的实际实验并不会发生。因为在观察者观测这个系统之前，所有的可能性都是可能的。所以薛定谔认为，在这种观测发生之前，猫必须处于活猫和死猫的叠加状态。只有这样，它才会变成一个或另一个。

这些困境导致了有关波函数含义的无休止争论，其中也不乏各种奇怪的观点。有些观点认为，观察者以某种方式存在于物理世界之外，观察者就是上帝，以及观察者就是人类认知的本质，等等。20 世纪 50 年代，物理学家休·艾弗雷特三世摒弃了观察者，并在一个在薛定谔方程下确定地演化的单波函数下进行观察。这种观点通常被称为「多世界」观点，因为它可以被解释为，所有结果同时存在于无数个平行宇宙中。在这个观点中，我们可以把一个系统的状态视为该系统的波函数，同时量子动力学是确定性的。

所以拉普拉斯的问题仍然存在，只是现在我们必须重新认识它。我们要考虑系统的「状态」是由其波函数表示的，而不是用其粒子的位置和速度来表示，而且，我们必须考虑时空的曲率，无论其有多小。如果我们做出这些调整，那么我们得到的宇宙模型是确定性的吗？物理世界本身是否具有确定性这个问题我们可能无法回答。然而，我们可以回答宇宙是否有某个特定的确定性模型这一问题。我们需要清楚地图和地域的区别。

2008 年，大卫·沃尔珀特使用格奥尔格·康托尔的对角化技术来证明拉普拉斯妖是不存在的（沃尔珀特，2008）。他的证明依赖于这样一种观点，如果这样的恶魔真的存在，那么它必须存在于它所预言的物理世界中。这导致了自相矛盾的自我参照，就像第 8 章讨论的图灵的不可判定性和第 9 章讨论的哥德尔的不完备性定理一样。事实上，这个结果是一种本质上的不完备性，它必然是由宇宙的任何确定性模型造成的，类似于之前引用的霍金的观点。在评论沃尔珀特的工作时，宾德尔（2008）尖锐地指出：「尽管如此，这些不同的理论，连同我们在物理学和其他科学学科中所学到的一切，仍有可能融合成科学所能做到的最好的东西：一个包罗万象的理论。」这一理论虽然不完整，但几乎包含了今天所有的确定性模型。

这些争论特别引人入胜，甚至比科学更富有哲理。但是，它们在很大程度上与模型的工程应用无关。确定性逻辑门模型的值，其实根本不取决于电子在硅材料中的流动是否是确定性的。它仅仅取决于我们能否构造出高可信地模拟该模型的硅结构。我们不需要也不可能达到完美。正如博克斯和德雷珀所说，所有的模型都是错误的，但是有些模型是有用的，而逻辑门已被证明是非常有用的模型。

尽管确定性可以帮助我们预测一个系统在一段时间内将如何演化，但我将在 10.2 节说明，即使一个确定性模型也可能无法很好地预测未来的行为。它们可能会被一种称为混沌的现象影响；由于复杂性，计算这些预测变得不切实际；或者更简单地说，是受累计误差的影响。在这种情况下，非确定性的模型可能会变得有价值。

每个模型都有一个有限的有效性范围。牛顿定律仅在适度的速度和尺度下是准确的。但即使是牛顿定律能够良好描述的系统也可能演化并超出该模型的有效性范围。假设我们对空间中的一个物体长时间施加一个适度的恒力，然后，牛顿第二定律预测速度将无限地增长，最终超过光速，显然，这会违反爱因斯坦的狭义相对论。与实际物理系统相比，模型的预测误差将变得任意大。然而，在一个相当短的时间范围内，在力小而质量大的情况下，牛顿第二定律能够非常好地预测运动的行为，而这样的预测是有价值的。同样，爱因斯坦的广义相对论在大尺度上解释了引力，而量子力学在小尺度上解释了物质的相互作用，但是想要将这些理论全部统一起来的尝试至今仍然不能令人满意。

确定性模型也可能被复杂性挫败。热力学中的一个经典例子是气体在腔室内所呈现的压力。这个现象可以被模拟为单个分子彼此的碰撞，以及分子与室壁的碰撞。在拉普拉斯的时代，这些碰撞本来是由牛顿的确定性运动定律控制的，但是这样的模型很难处理。在这样的运动定律下，即便是对相对较少的分子的个体运动行为进行计算也是很难实现的，这远远超出当今最强大计算机系统的算力。因此，物理学家认为这些运动是非确定性的，并且依赖于大量随机事件的统计数据来表现由玻意耳定律和查理定律确定地建模的那些行为。从大量的非确定性行为中得出确定性模型是遵循大数定律的结果，我将在下一章中进行讨论。我们将晶体管建模为确定性开关的能力依赖于类似的统计参数。

即使是简单的模型也可能产生复杂的行为，这可能会表现出一种被称为「混沌」的现象。有趣的是，尽管混沌模型的确定性实际上可能是一种有价值的特性，但还是无法对该类模型进行预测。以加密技术为例，它掩盖了信息的内容，这既依赖于确定性（确保消息可以由预设的接收方解密），也依赖于不能进行预测（保护信息不被窃听者窃取）。有趣的是，尽管今天的密码学家依赖于确定性模型，但他们希望物理世界实际上是非确定性的，可以利用某种形式的「真正随机性」来开发更强大的加密技术。事实证明，真正的随机性是极难实现的。

一个非确定性的模型可能有助于预测，但它预测的不是一个单个的行为，而是一系列行为。这一系列行为中的每一个行为都是可能的。例如，一个掷硬币的非确定性模型，简单地说，正面和背面朝上都是可能的。掷硬币的一个确定性模型仍然令人难以捉摸。即使我们用硬币的形状和材料特性以及它所掉落的表面的精确模型来费力地构建一个这样的模型，这个模型的预测值也会很差，因为即使我们的模型中只存在最小的误差，也会极大地改变掷硬币的结果。尽管毫无用处，可是作为科学实证主义的「大祭司」卡尔·波普尔坚持用这样的模型来掷骰子：

人们有时会听到这样的说法，行星的运动遵循严格的规律，而骰子的下落却是偶然的，或者是随机的。在我看来，区别在于我们迄今已能成功地预测行星的运行轨迹，却不能预测掷骰子的单个结果。为了推断预测结果，我们需要有一些定律和初始条件；如果没有可用的定律，或者初始条件无法确定，预测的科学方法就失效了。在掷骰子的时候，我们缺乏的显然正是对初始条件的充分了解。如果对初始条件进行足够精确的测量，在这种情况下也有可能做出预测。（波普尔，1959:198）

这种坚持的根源是对物理系统潜在确定性的坚定信念。然而，预测只能通过模型进行。可是，并没有这样一种会以任何有用的方式高度符合于这个物理系统的模型，因此，在物理系统与模型之间仍然存在着一个不可调和的差距。

不管潜在的物理世界是不是确定性的，一个非确定性模型都可以用概率来进行增强。换言之，它增加了我们对不确定的结果进行测量的可能性。第 7 章探讨过掷非均匀硬币的例子，我们预计掷 10 次硬币只会有 1 次是背面朝上，这样，这个例子就可以用背面朝上的概率 0.1 和正面朝上的概率 0.9 来建模。我将在第 11 章对概率模型进行讨论，但目前我们只关注确定性模型。

### 10.2 The Butterfly Effect

Studying atmospheric effects with the goal of being able to predict weather better, Edward Norton Lorenz came to a disheartening conclusion that prediction beyond a few days was simply not possible, despite that his models were deterministic. Working as a research meteorologist at MIT in the early 1960s, Lorenz was among the first to use well-developed mathematical models of convection and thermal effects in fluids to build computer simulations of weather. He noticed, however, that his models would yield radically different behaviors if he started the simulations with minutely different initial states.

[T]wo states differing by imperceptible amounts may eventually evolve into two considerably different states. If, then, there is any error whatever in observing the present state—and in any real system such errors seem inevitable—an acceptable prediction of an instantaneous state in the distant future may well be impossible. (Lorenz, 1963)

People later called this extreme sensitivity to initial conditions「the butterfly effect」after a metaphor put forth in the title of a talk by Lorenz, where the turbulence created in the air by the wing of a butterfly could cause a tornado. The butterfly wing changed the initial conditions just enough to make the difference between the tornado forming and the tornado not forming. The tornado would not have formed had the butterfly not flown.

Since the time of Lorenz's initial experiments, computers, mathematical models, and data gathered about weather have all improved by many orders of magnitude. Yet it is still true that predictions beyond about 14 days of weather patterns like rain and wind are not reliable. Indistinguishable initial conditions can lead to radically different weather.

A common feature of models that have such extreme sensitivity to initial conditions is that their behavior can appear random, capricious even. For this reason, the phenomenon is often called「chaos,」although the models are actually deterministic. Models of fluid flow, as occurs, for example, as air moves around on earth making weather, frequently exhibit chaos. These models can capture the general pattern of behavior of a system but not the details. The turbulence that you feel in an airplane, for example, has the character of highly random motion (see figure 10.1 ). Even the most detailed model will not be able to meaningfully predict that motion.

Even simple models can exhibit extreme sensitivity to initial conditions. Figure 10.2 shows the trajectory of a billiard ball on a table with a fixed circular obstacle in the middle. In this case, a small variation in the angle of the initial path of the ball eventually results in a completely different trajectory around the table. Although the starting trajectory of the ball on the left is almost imperceptibly different between the solid line and the dotted line, a radically different trajectory results.

Lorenz's studies of chaos all involved physical systems operating in a continuum of space and time. It turns out that purely digital systems can also exhibit chaotic behavior. The electrical engineer Solomon Wolf Golomb, whom we encountered in chapter 2 for his famous quote,「You will never strike oil by drilling through the map」(Golomb, 1971), figured out that surprisingly simple digital logic circuits could generate bit patterns that appeared to be random (Golomb, 1967).

I first learned about Golomb's「linear feedback shift registers」in the early 1980s when I was at Bell Labs designing modems, devices to transmit bit sequences over an ordinary telephone channel that had been designed to carry human voice signals not bit sequences. It turns out that modems behave much better on seemingly random bit sequences, where there are no repeating patterns. Golomb had figured a way to make almost any bit pattern look completely random using a simple logic circuit called a「scrambler.」The original bit sequence can be easily extracted using a similar logic circuit called a「descrambler」at the receiving end. I was so impressed with the elegant simplicity (and the Boolean algebra that could be used to analyze these circuits) that I made an oil painting with a scrambler circuit and LED lights embedded in the canvas (see figure 10.3 ). The LED lights exhibit a seemingly random pattern that repeats itself only every 14 hours. The circuit operates reliably to this day.

Figure 10.1

Turbulence in a vortex from the tip of an airplane wing tracked with the help of colored smoke. [Image by NASA Langley Research Center, released into the public domain.]

Pseudorandom patterns were also used in a much more serious art work shown in figure 10.4 , a light sculpture by the American artist Leo Villareal. The sculpture consists of 25,000 LED lights installed in 2013 on the San Franscisco Bay Bridge. The lights are controlled by a computer to create patterns that were designed to never repeat during the entire intended two-year lifetime of the installation.

Golomb's circuits generate pseudorandom bit sequences. They seem random but are not. They produce digital chaos. Pseudorandom bit sequences are central to simulation, computer games, cryptography, and even some art. In computer games, for example, they create an illusion of random things happening, whereas in fact the game is completely deterministic.

Figure 10.2

A billiard table with a fixed circular obstacle in the middle.

Figure 10.3

Pseudo Random, oil, TTL circuits, and LEDs on canvas, 1981, by the author.

Figure 10.4

The Bay Lights, light sculpture by Leo Villareal (2013).

In the early 1980s, Stephen Wolfram noticed a connection between Golomb's circuits and cellular automata. Cellular automata are simple digital models with a rectangular grid of bits, where each bit gets repeatedly updated by computing some logic function of the neighboring bits. A famous example of a cellular automaton is Conway's Game of Life, developed in 1970 by the British mathematician John Horton Conway. Conway's game is an astonishingly simple deterministic closed model that exhibits tantalizingly lifelike behavior. It captured the imagination of many people, including Wolfram, who devoted much of the rest of his career to studying cellular automata and related phenomena.

The game has a rectangular grid of cells that are either alive (shown as black squares) or dead (white squares). An initial state has some cells alive and some dead, as shown in figure 10.5 . At each step of the game, the cells are updated according to the following rules:

Any live cell with fewer than two live neighbors dies.

Any live cell with two or three live neighbors lives on to the next step.

Any live cell with more than three live neighbors dies.

Any dead cell with exactly three live neighbors becomes a live cell.

Conway metaphorically associated these rules with life, where underpopulation, overpopulation, and reproduction could all change the state of a cell. Despite the simple rules, the game exhibits surprisingly complex behavior. As the game proceeds, patterns may become stable, like the Block and Beehive shown in the figure, or they may move across the grid, as in the Spaceship. They can also oscillate between two repeating patterns, and they can exhibit seemingly random, chaotic behavior for quite a long time. It is mesmerizing to watch one of these games play out.

Figure 10.5

A snapshot of Conway's Game of Life.

Conway's game is purely digital, easily realized on a computer. The fact that such simple rules can exhibit such complex behavior inspired Wolfram, who in his 2002 book, A New Kind of Science , concludes that「all is computation」(Wolfram, 2002). More specifically, Wolfram postulates that all natural processes can be constructed out of simple rules, and the complexities arise because of the chaos that such rules can induce. He makes a compelling and engaging case, but of course the ultimate「truth」of such a postulate would depend on digital physics.

Despite chaos, many engineered systems are predictable with high confidence with time horizons of years. Transistors are good examples. Although any detailed model of the underlying motion of electrons in the silicon will be chaotic, the macroscopic behavior of a transistor is simple. It functions as a switch. A gasoline engine in a car is another example. The explosions in the cylinders are highly chaotic, but they reliably deliver controllable power to the powertrain. Harnessing chaos is a key goal of engineering and, if Wolfram is right, of nature as well.

10.2 蝴蝶效应

爱德华·诺顿·洛伦兹为了更好地预测天气研究了大气效应，并得出一个特别令人沮丧的结论，即尽管他构建的模型是确定性的，但是仍然无法预测几天以后的天气状况。20 世纪 60 年代初，洛伦兹是麻省理工学院的一名气象学家，他也是最早一批使用流体中先进的对流和热效应数学模型对天气状况进行计算机模拟的研究人员之一。然而，他注意到，如果他以差异微小的初始状态开始模拟，他的模型就会产生完全不同的预测结果。

两种差异甚微的状态最终可能演化成两种截然不同的状态。如果在观察当前状态时出现任何错误，即出现了任何实际系统中似乎都不可避免的错误，那么，对遥远未来的瞬时状态进行可接受的预测很可能是无法实现的。（洛伦兹，1963）

后来，人们把这种对初始条件的极度敏感性称为「蝴蝶效应」，这是洛伦兹在一次演讲的标题中给出的一个比喻，即蝴蝶的翅膀在空气中产生的气流可能会引发一场龙卷风。蝴蝶的翅膀改变了初始条件，这一改变足以造成龙卷风形成和没有形成之间的巨大差异。如果蝴蝶没有飞动，就可能不会形成龙卷风。

自洛伦兹最初的实验以来，计算机、数学模型以及天气数据收集等方面都有了很大的发展，提升了许多个数量级。然而，超过 14 天以上的天气情况（如降雨和风）预测仍然是不可靠的。不可区分的那些初始条件会导致完全不同的天气状况。

对初始条件极度敏感的模型都有一个共同的特点，它们的行为看起来是随机的，甚至是反复无常的。恰恰由于这个原因，这种现象通常被称为「混沌」，尽管这些模型实际上都是确定性的。流体流动的模型经常表现出混沌现象，例如，空气在地球上移动会形成各种不同的天气。这些模型只能捕捉到系统行为的一般模式，但无法捕捉到细节。例如，你在飞机上感觉到的气流就具有高度随机运动的特征（见图 10.1）。即使是最详尽的模型，也无法对这种运动做出有意义的预测。

即使是简单的模型也会对初始条件表现出极大的敏感性。图 10.2 给出了一个桌球在桌子上的运行轨迹，这个桌子的中间固定有一个圆形障碍物。在这种情况下，即使球的初始路线发生了一个微小的角度变化，最终也会导致球在桌子上出现完全不同的运行轨迹。虽然左边的球的起始轨迹在实线和虚线之间的差异几乎是不可察觉的，却产生了一个完全不同的轨迹。

▲图 10.1 在彩色烟雾的辅助下，飞机机翼尖端的涡流中的气流。（图片由美国国家航空航天局兰利研究中心提供，已公开。）

图 10.2 中间有固定圆形障碍物的球桌。

洛伦兹对混沌的全部研究都包含了在一个空间和时间连续统中运行的物理系统。事实证明，纯数字系统也会表现出混沌行为。我们在第 2 章中提到的电气工程师所罗门·沃尔夫·格伦布，他有一句名言是，「通过在地图上钻孔，你永远不会找到石油」（格伦布，1971）。他发现，简单的令人吃惊的数字逻辑电路可以产生看似随机的比特模式（格伦布，1967）。

我第一次了解格伦布的「线性反馈移位寄存器」是在 20 世纪 80 年代初，当时我还在贝尔实验室设计调制解调器。如我们所知，调制解调器是一种通过普通电话信道传输比特序列的设备，而电话信道被设计用来传输语音信号而不是比特序列。结果表明，调制解调器在没有重复模式的、看似随机的比特序列上表现得更好。格伦布想出一种方法，使用一种叫作「扰码器」的简单逻辑电路，让几乎所有的比特模式看起来都是完全随机的。在接收端可以使用一种类似的「解扰器」逻辑电路，就可以很容易地提取出原始的比特序列。我对这种方法优雅的简洁性（以及可以用来分析这些电路的布尔代数）印象深刻，于是我画了一幅油画，画布上画了一个扰码器电路和一个 LED 灯（见图 10.3）。LED 灯呈现出一种看似随机的模式，每 14 个小时重复一次。这个电路至今运行可靠。

伪随机模式也被用于一件更为严肃的艺术作品，如图 10.4 所示。这是一件由美国艺术家利奥·比利亚雷亚尔创作的灯光雕塑。这座灯光雕塑由 2013 年安装在旧金山海湾大桥上的 2.5 万盏 LED 灯组成。这些灯由一台计算机控制，它们能在安装的两年内呈现出不重复的灯光图案。

图 10.3 画布上的伪随机、燃油、晶体管逻辑（TTL）电路以及 LED 灯，由本书作者绘制，1981 年。

图 10.4 旧金山湾区灯光，灯光雕塑由利奥·比利亚雷亚尔创作（2013）。

格伦布的电路会产生伪随机的比特序列。它们看起来是随机的，但实际上并不是，它们会产生数字混乱。伪随机的比特序列是仿真、计算机游戏、密码学甚至一些艺术的核心。例如，在计算机游戏中，它们制造了一种事件随机发生的错觉，而事实上，游戏完全是确定性的。

20 世纪 80 年代初，史蒂芬·沃尔弗拉姆注意到格伦布的电路和元胞自动机之间存在联系。元胞自动机是一种简单的数字模型，其有一个矩形的比特网格，网格中的每个比特都通过计算相邻比特的某些逻辑函数反复更新。元胞自动机的一个著名示例是康威的「生命游戏」，该游戏是由英国数学家约翰·何顿·康威于 1970 年开发的。康威的游戏是一个非常简单的确定性封闭模型，它呈现的行为极为逼真生动。它激发了包括沃尔弗拉姆在内的许多人的丰富想象力。沃尔弗拉姆在他的职业生涯后期的大部分时间里都致力于研究元胞自动机及其相关现象。

这个游戏有一个矩形的元胞网格，这些元胞要么是活的（显示为黑色方块），要么是死的（显示为白色方块）。在初始状态中，有一些元胞是活的，一些元胞是死的，如图 10.5 所示。在游戏的每个步骤中，元胞都按照以下规则进行更新：

1. 任何一个活元胞，如果有少于两个活的相邻元胞，就会死亡。

2. 任何一个活元胞，如果有两个或三个活的相邻元胞，就会活到下一步。

3. 任何一个活元胞，如果有三个以上活的相邻元胞，就会死亡。

4. 任何一个死元胞，如果有三个活的相邻元胞，就会变成活元胞。

图 10.5 康威「生命游戏」场景的一个截图。

康威隐喻性地将这些规则与人类的生活联系在一起，人口不足、人口过剩和生命的繁殖都会改变元胞的状态。尽管规则很简单，但这个游戏表现出令人惊讶的复杂行为。随着游戏的进行，一些模式会像图中显示的「街区」和「蜂巢」一样变得比较稳定，或者它们可能会像「宇宙飞船」一样在网格中移动。它们也可以在两种重复模式之间来回摆动，而且它们可以在相当长的一段时间内表现出看似随机、混沌的行为。观赏这样的一种游戏是非常令人着迷的。

康威的游戏是纯数字化的，在计算机上很容易实现。如此简单的规则却可以呈现出如此复杂的行为，这一事实启发了沃尔弗拉姆的灵感。他在 2002 年出版的著作《一种新科学》（A New Kind of Science）中得出「一切都是计算」的结论。更确切地说，沃尔弗拉姆假设所有的自然过程都可以用简单的规则来构建，而复杂性的产生是由于这些规则会引起混乱。他给出一个引人注目且引人入胜的观点，当然，这种假设的终极「真理」将取决于数字物理学。

尽管存在一些混沌现象，但是许多工程系统在数年的时间范围里还是高度可预测的，晶体管的出现就是很好的例证。虽然建模硅材料中电子运动的任何详细模型都是混沌的，但是晶体管的宏观行为是简约的，它的功能就像一个开关。汽车的汽油发动机是另一个很好的例子。汽缸内的那些爆炸高度混乱，但它们的确为动力系统提供了可控的动力。对混沌的控制是工程中的一个关键目标。如果沃尔弗拉姆的观点是正确的，那么这也会是大自然的一个关键目标。

### 10.3 Incompleteness of Determinism

Laplace believed that nature can be fully described by deterministic models. Wolfram goes further and argues that nature behaves like computational models that are also deterministic. The set of deterministic computational models is much smaller than the set of deterministic models. The set of computational models excludes continuums, for example. So Wolfram's claim is more aggressive than Laplace's.

In both cases, the models may exhibit chaos, so they are capable of describing immensely complex behavior. But the chaos also limits the utility of the models as predictors, making Laplace's demon a difficult concept to accept. Nevertheless, the models are deterministic.

In Laplace's world, time and space are continuums through which objects move. In Wolfram's world, time and space are discrete grids of cells that are updated in a step-by-step fashion. What happens if we assume that the world has both kinds of behaviors, discrete and continuous? I will give a simple example that suggests that in such a world, determinism is incomplete. Specifically, a set of deterministic models that describes the world using a mixture of discrete and continuous behaviors has「holes」in it, situations that should be able to be modeled deterministically but cannot be. To patch these holes, we either have to disallow discrete behaviors altogether, asserting that they do not occur in the physical world, or we have to embrace digital physics and sacrifice almost all known physical models, including relativity and quantum mechanics, both of which model space and time as continuums.

As an example of a model with both continuous and discrete behaviors, consider the collisions of billiard balls, as shown in figure 10.6 . Suppose that the left ball is moving toward the right ball with momentum P and the right ball is sitting still, as illustrated in figure 10.6 (a). Assume that the surface is frictionless, so the momentum of each ball remains constant until a collision occurs. As long as no collision occurs, the behavior is continuous.

Suppose that we model a collision as a discrete event. That is, we assume that the collision occurs in an instant, having no duration in time. Such a model needs to determine the momentum of the balls after the collision as a function of their momentums before the collision.

Figure 10.6

Collision of ideal billiard balls on a frictionless surface.

Assume that the balls are ideally elastic , meaning that no kinetic energy is lost when they collide. In this case, Newton's laws require that both energy and momentum be conserved, in the sense that the total momentum and energy in the balls must be the same after the collision as before. 4 In the physical world, some of the kinetic energy will be converted to heat due to friction, but here we will assume that doesn't happen or that so little kinetic energy is lost that we can neglect it.

Assuming the masses are the same, there are two possible results from the collision that preserve both momentum and energy. One result is that the left ball passes right through the right ball without interacting with it. This outcome could happen, for example, if the ball were actually a neutrino rather than a billiard ball. However, for billiard balls, this outcome is extremely unlikely, so we are justified in rejecting this possibility. The only other result that conserves both momentum and energy is that the balls exchange momentums, as shown in figure 10.6 (c). The left ball is now still, and the right ball is moving away at the same velocity that the left ball was approaching before the collision.

Now suppose that the two balls have different masses. It turns out that in this case, there are still exactly two possible solutions, one where the left ball passes through the right ball and the other where they bounce. Let's again choose the more reasonable solution where they bounce. Because the masses are different, after the collision, both balls will be moving. If the left ball is heavier than the right, then they will both be moving to the right. If the left ball is lighter than the right, then they will be moving in opposite directions. In both cases, their speeds after the collision are uniquely determined by Newton's requirement that both momentum and energy be conserved. Hence, the model is deterministic.

If there are more than two balls, however, then the situation gets much more interesting. Consider a thought experiment where two billiard balls are approaching a third ball from opposite sides, as illustrated here 5 :

Assume that the center ball is sitting still and the two outer balls collide with the center ball at the same time. To keep things simple, let's start with the assumption that all three balls have the same mass. What will happen?

I hope you have enough practical experience with billiard balls that your intuition matches mine. I would expect in this situation that the two outer balls will bounce off the center one and move away from it at the same speed that they had been approaching it. Thus, after the collision, the situation will look like this:

But coming up with a discrete model that predicts this behavior turns out to not be so easy.

A first attempt will be to simply use the same technique that we used with two balls, where the balls exchange momentums when they collide. However, if the collisions are simultaneous, then the left and right balls will exchange momentums with the center ball at the same time, and these momentums will have opposite signs, canceling each other out. Thus, all three balls will suddenly stop. This solution fails to conserve both momentum and energy.

An alternative way to handle this situation is to treat the two simultaneous collisions as a sequence of two-ball collisions with no time elapsing between the collisions. As shown in figure 10.7 (b), when the collisions occur, we can arbitrarily pick one of the collisions to handle first, ignoring the other collision. Suppose we handle the left collision first, ignoring the right collision, as indicated in the figure. The left ball transfers its momentum P to the middle ball and stops. Without time elapsing, we find ourself in state (c) in the figure, where the middle and right balls are traveling toward one another and colliding. Now there is only one collision, so we handle it in (d), leaving us in state (e), where the balls have exchanged momentums. Again, without time elapsing, a new collision occurs, which we handle in (f), leaving us in state (g). After time elapses, we find ourselves in state (h), where the left and right balls are moving away from the center ball, which has not moved and remains still. This behavior is the one we expected intuitively, where the two balls are moving away at equal speeds after the collision.

In this solution, if the masses of the balls are all the same, then it does not matter which of the two collisions we handle first. Here comes the rub. If the masses of the balls are not the same, then the solutions are not the same. If we handle the left collision first, then we get one solution. If we handle the right collision first, then we get a different solution, with all three balls moving at different speeds.

Suppose, for example, that the center ball weighs twice as much as the left and right balls. To be concrete, let's suppose that the center ball weighs two kilograms and the outer balls weigh one kilogram each (these billiard balls are quite heavy, but nice round numbers make the math easier). Suppose that the left and right balls are approaching the center ball at one meter per second so that they collide simultaneously with the center ball. First, notice that this scenario is completely symmetric, and the same intuitive solution works, where the two outside balls bounce off the center one so that after the collision, they are moving away from the center ball at one meter per second, and the center ball remains still. This solution conserves both momentum and energy.

However, this is not the solution we get using the strategy shown in figure 10.7 . In that strategy, we handle the left collision first, and then without time elapsing, we handle the second and third collisions that result. I will spare you the nerd storm, but after the sequence of collisions in the figure, the left ball will be moving to the left at about 0.48 meters per second, the middle ball will also be moving to the left, but more slowly, at about 0.37 m/s, and the right ball will be moving to the right at about 1.22 m/s. If you do the math, you can verify that with this solution, both momentum and energy are conserved. 6 Notice that with this solution, the situation is no longer symmetric, although the starting state was symmetric.

So what happens if we handle the right collision first? In that case, we will end up with the mirror image asymmetric solution, where the middle ball is moving to the right. This solution also conserves momentum and energy.

We now have a real conundrum. We have three possible outcomes: a symmetric one derived intuitively and two mirror-image asymmetric ones derived using the strategy of figure 10.7 . Newton's laws give us no basis for preferring any one of these solutions. All three solutions, and many more, are consistent with Newton's laws. They all conserve momentum and energy. Because there is more than one allowed behavior, Newton's laws (with discrete collisions) result in a nondeterministic model.

How do we know which behavior will match some physical experiment? Here's where things get tricky. To conduct such an experiment, we will have to ensure that the collisions are actually simultaneous. This will be difficult to do (impossible, in fact, given quantum mechanical uncertainty principles). First, suppose that the collisions are not actually simultaneous but are just close in time. That is, one of the two outer balls collides with the center ball just before the other outer ball arrives. In this case, instead of a single collision among three balls, a sequence of collisions occurs between two balls. This makes the problem easier to solve because when only two balls are colliding, only one outcome after the collision is possible that conserves both momentum and energy (barring the tunneling outcome, where the balls pass through one another). Consequently, if the collisions are not simultaneous, the model remains deterministic. Only one final behavior is allowed by the model.

If the masses of the balls are different, then the behavior is different if the left ball collides first than if the right ball collides first. This will be true no matter how small the time is between collisions. Let's call the time of the left collision t L and the time of the right collision t R . Let the time difference be d = t L − t R . Consider a sequence of experiments where d is always positive (the right ball always collides first), and d approaches zero, getting smaller and smaller. As d gets close to zero, there will be little difference between the outcomes of these experiments. Changing d from, say, one nanosecond to 0.5 nanoseconds will not change the outcome much. Eventually, as d gets small, there is no significant difference between the experimental outcomes, so the sequence of experiments seem to be converging to behavior that should be the behavior when d = 0. 7 It would seem that the limiting behavior should be the one unique behavior when the collisions are simultaneous.

Figure 10.7

One of two orderings for handling collisions among three balls.

However, it is not. If we repeat the same sequence of experiments, but this time we require d to always be negative, then again we get a sequence of behaviors that are closer and closer together, and they appear to be converging to a behavior, but they do not converge to the same behavior as the previous sequence of experiments.

In the limiting case, when d reaches zero, the collisions become simultaneous. At this point, the behavior will depend on which sequence of experiments we are conducting, the one where d > 0 or the one where d < 0. These two sequences of experiments converge to different behaviors as d approaches zero. When the collisions become simultaneous, we have no basis for choosing between these two possible limiting cases, so we have to assume they are both possible. They both conserve momentum and energy.

In the single unique experiment where d is exactly zero, there is more than one possible outcome from the model, so the model is nondeterministic. However, if d is not zero, no matter how small it is, then the model is deterministic. A mathematician would call the set of all these deterministic models incomplete because this set does not contain its own limit points. In the limit, when d exactly hits zero, the model becomes nondeterministic. The set of deterministic models has a hole at exactly the point where d = 0.

Note that it will not do to just disallow d = 0 because to do so we would have to disallow t 1 and t 2 to vary smoothly. Assuming time is a continuum, as nearly all current models of physics do, t 1 can cross t 2 , in which case there is a point where t 1 = t 2 , and hence d = 0. Note that this point is even harder to avoid if we quantize time, as required by digital physics. However, we don't want to do that anyway because doing so sacrifices almost all of modern physics, including Newton's laws, the Schrödinger equation, and Einstein's relativity.

I argued in section 9.3 that a close approximation of a process does not have the same properties as the process unless no significant difference is found between a continuum and a countable set. This billiard ball thought experiment reinforces that arbitrarily close approximations can in fact be quite different from the real thing. If the「real thing」is simultaneous collisions, then this thought experiment shows that all arbitrarily close approximations to it are deterministic, but the real thing is not. Moreover, we can make two scenarios, one with d < 0 and one with d > 0, that are arbitrarily close to one another in all their parameters but that exhibit wildly different (but still deterministic) behaviors. We are forced to conclude that coming arbitrarily close, in「arbitrarily fine detail」in the words of Deutsch, does not achieve the「real thing.」In this billiard ball experiment, all close approximations of simultaneous collisions are deterministic, but the actual simultaneous collisions are not.

Any model for this physical system that treats the collisions discretely will suffer this problem. What exactly does it mean to treat the collisions discretely? In this case, it means that the model talks about time before and after the collision, but the collision itself does not occupy any time. It occurs instantaneously. An instant before the collision, we have a certain energy-momentum arrangement, and an instant after, we have another energy-momentum arrangement, and the model only requires that total energy and momentum are conserved.

An alternative is to not treat the collision as a discrete event. Instead of being instantaneous, it takes time. The collision starts when the molecules of the balls are close enough to begin to affect one another, and it ends when they have moved far enough apart that they no longer significantly affect one another. We can build this kind of model using either classical mechanics (Newton's laws) or quantum mechanics (using the Schrödinger equation) to describe the continuous evolution of a wave function. Both approaches will yield a model that is deterministic but extremely sensitive to initial conditions, and therefore chaotic.

The nondiscrete classical mechanics solution is reasonably easy to understand. Suppose the balls are ever so slightly springy. That is, when the molecules of one ball get close enough to those of the other ball to start interacting, the molecules of the balls get squished together, like a spring being compressed. The balls slow down. The spring compression temporarily converts kinetic energy to potential energy, so energy is still conserved. As the springs that are the balls compress, the motion of the balls slows until the balls stop. The springs then start to decompress, converting the potential energy back to kinetic energy and pushing the balls apart. A model like this is deterministic, but it is extremely sensitive to the initial positions, speeds, and springiness of the balls. If those are slightly off, then a radically different behavior will result.

So we have a choice. We can either accept a discrete model of the collisions, in which case we lose predictability to nondeterminism, or we can reject discreteness, constructing a detailed model of molecular interactions, in which case we lose predictability to chaos. In both cases, we lose predictability. The model that accepts discrete collisions is much simpler than the one that models molecular interactions, so it seems like the simpler model that admits nondeterminism is the better choice.

10.3 决定论的不完备性

拉普拉斯认为，大自然可以被确定性模型完全描述。沃尔弗拉姆更进一步认为，大自然的行为就像计算模型一样，也是确定性的。确定性计算模型的集合要比确定性模型的集合小得多。例如，计算模型的集合排除了连续统。因此，沃伍尔弗拉姆的观点比拉普拉斯的观点更激进。

在这两种情况下，模型都可能表现出混沌，因此它们都能够描述极其复杂的行为。但这些混沌也限制了模型作为预测器的效用，这使得拉普拉斯妖成为一个难以被接受的概念。但无论如何，这些模型是确定性的。

在拉普拉斯的世界里，时间和空间是连续统，物体在这些连续统中运动。在沃尔弗拉姆的世界里，时间和空间是离散的元胞网格，这些元胞以逐步的方式进行更新。如果我们假设世界有两种行为，离散的和连续的，那么将会发生什么？我举一个简单的例子来说明，在这样的世界里，决定论会是不完备的。具体来说，一组使用离散和连续混合行为来描述世界的确定性模型存在着「漏洞」，也就是应该能够确定地建模却无法做到的情形。要填补这些漏洞，我们必须完全排除离散行为，断言它们不会在物理世界出现。如果我们允许存在离散行为，那么势必要接受数字物理学。但是，这将付出巨大的代价，我们必须否认几乎所有已知的物理学模型，包括相对论和量子力学，因为这两种模型都将空间和时间建模为连续统。

以具有连续和离散行为的模型为例，我们来考虑如图 10.6 所示的桌球碰撞。假设左边的球是以动量 P

向右边的球移动，而右边的球静止不动，如图 10.6（a）所示。假设表面是无摩擦力的，所以每个球的动量保持不变，直到发生碰撞。显然，只要不发生碰撞，球的运动行为就是连续的。

假设我们将桌球的碰撞建模为一个离散事件。也就是说，我们假设碰撞只发生在一个瞬间，且没有持续时间。这种模型需要以碰撞前两个球的动量函数来确定碰撞之后这两个球的动量。

图 10.6 理想的桌球在无摩擦表面上的碰撞。

假设这些桌球都是理想弹性体，这意味着当它们碰撞时不会有动能损失。在这种情况下，牛顿定律要求能量和动量都是守恒的，碰撞后球的总动量和总能量必须与碰撞前相同。在物理世界中，一些动能会因摩擦而转化为热能，但这里我们假设这是不会发生的，或者动能的损失极其小，我们可以将其直接忽略掉。

假设两个球的质量相同，那么这种动量和能量都保持不变的碰撞会产生两种可能的结果。一个结果是，左边的球穿过右边的球，而没有与之产生相互作用。这个结果是有可能发生的，例如，这个球实际上是一个中微子而不是一个桌球。然而，对于桌球来说，这种结果是极不可能发生的，所以我们有充分的理由否定这种可能性。那么另一个唯一保持动量和能量的结果是两个球交换了动量，如图 10.6（c）所示，左边的球现在是静止的，右边的球则以与碰撞前左边球靠近时相同的速度在移动。

现在假设这两个球有不同的质量。在这种情况下，仍然会有两种可能的结果。一种是左边的球穿过右边的球，另一种是两球发生碰撞并弹开。让我们再次选择两个球弹开这一更为合理的结果。由于两个球的质量不同，发生碰撞之后，两个球都会移动。如果左边的球比右边的重，那么它们都会向右移动。如果左边的球比右边的轻，那么它们就会向相反的方向移动。在这两种情况下，它们在碰撞之后的速度是由牛顿的动量和能量守恒定律决定的。因此，该模型是确定性的。

然而，如果有两个以上的球，那么情况会变得更为有趣。让我们在头脑中思考一个思想实验，两个球正从相反的方向接近第三个球，如下图所示：

假设中间的球静止不动，两侧的两个球同时与中间的球发生碰撞。简单起见，我们假设三个球的质量相同。那么，此时会发生什么呢？

我希望你有足够丰富的打桌球实际经验，那样的话，你的直觉就和我的一样了。我的直觉认为，两侧的球碰撞中间的球之后，会分别以它们接近中间球时的速度向相反的方向弹出。因此，碰撞后的情况如下图所示：

但是，要想给出一个预测这一行为的离散模型并不那么容易。

第一个尝试是简单地使用上述相同的方法，我们使用两个球，且当它们碰撞时会交换动量。但是，如果左右两个球与中间的球的碰撞同时发生，那么这两个球将与中间的球同时交换动量。这两个动量大小相等、方向相反，从而相互抵消。因此，这三个球将会突然停止。然而，这个结果不能同时保持动量和能量的守恒。

处理这种情况的另一种方法是，将两个同时发生的碰撞视为两球碰撞的序列，且在两次碰撞之间没有时间的流逝，如图 10.7（a）所示。当碰撞发生时，我们可以先任意选择其中一个碰撞进行处理，而忽略另一个碰撞。假设我们先处理左边的碰撞，忽略右边的碰撞，如图 10.7（b）所示。左边的球把它的动量 P

传给中间的球，然后停止。在没有时间流逝的情况下，我们会发现现在处于（c）状态，中间的球和右边的球相向移动，并相互碰撞。现在只有一次碰撞，所以我们在（d）状态下对其进行处理，使球处于状态（e），这一状态下两个球交换了动量。同样，在没有时间流逝的情况下，会发生一次新的碰撞，我们在（f）状态下进行处理之后会处于（g）状态。在一段时间后，我们会发现这些球处于（h）状态，中间的球没有移动且保持静止，左边和右边的球从中间的球向两侧移开。这样的行为是我们直观的预期，即两个球在碰撞后以相同的速度移开。

中间的球向两侧移开。这样的行为是我们直观的预期，即两个球在碰撞后以相同的速度移开。

图 10.7 处理三个球之间碰撞的两种情形之一。

在这个解中，如果所有球的质量都是相同的，我们首先处理哪一次碰撞就无关紧要了。但是，麻烦来了。如果球的质量不一样，得出的解就不一样了。如果先处理左边的碰撞，我们就会得到一个解。如果先处理右边的碰撞，那么我们会得到一个不同的解，三个球会以不同的速度移动。

例如，假设中间球的重量是左边球和右边球的两倍。具体地说，假设中间球重 2 公斤，左边球和右边球分别重 1 公斤（这些球相当重，但这些漂亮的约整数会使计算更容易）。假设左边球和右边球分别以 1 米每秒的速度接近中间的球，因此它们将与中间球同时碰撞。首先，请注意，这个假设的场景是完全对称的，同时，直观的解也是适用的，即两个外侧的球在与中间球发生碰撞之后会向外弹开，并分别以每秒 1 米的速度离开中间球，而中间球保持静止不动。这个解同时保持了动量和能量的守恒。

但是，这并非使用图 10.7 所示的策略得出的解。在图 10.7 的策略中，我们首先处理的是左边球的碰撞，然后在没有时间流逝的情况下处理第二次和第三次碰撞。我不想让你继续忍受这场技术呆子的头脑风暴，但在发生了图中的碰撞序列之后，左边球将以大约每秒 0.48 米的速度向左移动，中间球也会向左移动，但其速度要慢一些，约为每秒 0.37 米，同时，右边球将以每秒大约 1.22 米的速度向右移动。如果你进行数学计算，就可以验证这个解，即动量和能量都是守恒的。[1]

请注意，在这个解中，尽管初始状态是对称的，但是结果不再是对称的。

那么，如果我们先处理右边球的碰撞会发生什么呢？在这种情况下，我们将得到一个镜像的不对称解，中间的球会向右移动。当然，这个解仍然保持了动量和能量的守恒。

我们现在有一个真正的难题。我们会有三种可能的结果：一种是由直觉得出的对称解，以及由图 10.7 的策略得出的两种镜像的不对称解。牛顿定律没有给我们提供选择任何一个解的理论依据。不只是这三种解，还有更多的解都符合牛顿定律，它们都遵守动量和能量守恒定律。由于存在不止一种可能的行为，牛顿定律（在离散碰撞的情形下）造成了一个非确定性模型。

我们如何才能知道哪种行为与某些物理实验相匹配？这就是问题变得棘手的地方。为了进行这样的实验，我们必须确保这些碰撞是同时发生的。实际上，我们很难做到（事实上，考虑到量子力学的非确定性原理，这是不可能的）。首先，假设这些碰撞实际上并非同时发生，只是在时间上非常接近。也就是说，两个外侧的球中的一个刚好在另一个球到达之前先与中间球发生碰撞。在这种情况下，这些碰撞并不是三个球之间的一次碰撞，而是这些球两两之间的一系列碰撞。这使得问题更容易解决了，因为只有两个球发生碰撞时，碰撞后只有一个结果就能够同时保持动量和能量的守恒（排除隧道穿越的结果，即两个球互相穿过对方）。因此，如果碰撞不是同时发生的，那么这个模型仍然是确定性的。该模型只允许一个最终的行为。

如果球的质量不同，左边球先碰撞和右边球先碰撞的运动行为就不同。不管这些碰撞的时间间隔有多短，得出的结果都是不同的。令左边碰撞的时间是 tL

，右边碰撞的时间为 tR

，其时间差为 d

=tL

-tR

。我们考虑要进行一系列实验，其中 d

总是为正（右边球总是先碰撞），且 d

越来越小趋近零。当 d

接近零时，这些实验的结果之间几乎没有差别。比如，将 d

从 1 纳秒改变为 0.5 纳秒并不会对结果形成太大的影响。最终，当 d

的值变小时，这些实验结果之间就不再有显著的差异。因此，实验的序列似乎收敛到了 d

=0 时的运动行为。似乎当碰撞同时发生时，极限的运动行为应该是唯一的运动行为。

然而，事实并非如此。如果我们重复相同序列的实验，但这一次我们设定 d

总为负，然后，我们再一次得到一个运动行为的序列，那么这些行为越来越接近在一起，它们似乎收敛到一个行为，但它们并不会收敛到与之前实验序列相同的运动行为。

在极限情况下，当 d

达到 0 时，碰撞会同时发生。此时的运动行为将取决于我们正在进行的实验序列，即 d>0 还是 d

<0。当 d

趋近 0 时，这两个实验序列会收敛于不同的运行行为。当碰撞同时发生时，我们没有任何依据能够在这两种极限情况之间进行选择，因此，我们必须假设它们都是可能的。它们都能保持动量和能量的守恒。

在 d

为零的唯一实验中，该模型会有不止一个可能的结果，因此该模型是非确定性的。然而，如果 d

不为 0，无论其值多小，该模型都是确定性的。数学家会称所有这些确定性模型的集合是不完备的，因为这个集合不包含它自己的极限点。在这个极限点，即当 d

正好达到 0 时，模型就变得不确定了。确定性模型的集合在 d

=0 时就有漏洞了。

请注意，仅是不允许 d

=0 还不够，因为要做到这一点，我们必须不允许 t

1

和 t

2

之间有连续变化。假设时间是一个连续统，就像目前所有的物理模型一样。t

1

可以跳过 t

2

，在这种情况下，会有一个点 t

1

=t

2

，由此 d

=0。请注意，如果按照数字物理学的要求将时间进行量化，那么这一点更难避免。然而，无论如何，我们都不想这样做，因为这样做就意味着几乎要放弃所有的现代物理学理论，包括牛顿定律、薛定谔方程和爱因斯坦的相对论。

我曾在 9.3 节中指出，一个过程的近似并不具备与实际过程相同的性质，除非连续统和可数集之间没有显著的差异。这个桌球思想实验强化了我的这个观点，即任意接近的近似可能与实际的事物存在着很大的不同。如果「实际事物」是同时发生的碰撞，那么这个思想实验表明，所有任意接近它的近似都是确定性的，但实际的事物并非如此。此外，我们还可以设定两种情形，一种是 d

<0，另一种是 d>0，它们的所有参数都彼此任意接近，但它们会给出截然不同（但仍然是确定性的）的运动行为。我们不得不得出这样的结论：用多伊奇的话说，就是对一个「实际事物」的「任意精细的接近」并不会达成这个事物」。在这个桌球实验中，同时发生的碰撞的所有近似都是确定性的，但在实际中同时发生的碰撞却不是。

如果离散地处理碰撞，这个物理系统的任何模型都会遇到这个问题。离散地处理碰撞到底是什么意思？在这种情况下，它意味着模型关注了碰撞前后的时间，但碰撞本身并不占用任何时间。也就是说，碰撞是瞬间发生的。在碰撞前的一瞬间，我们有一种确定的能量 — 动量排列，在碰撞后的一瞬间，我们有另一种能量 — 动量排列，而这个模型只要求总能量和总动量是守恒的。

另一种选择是不要将碰撞视为一个离散事件。它并非瞬间发生，而是占用了一定的时间。当球的分子足够接近并开始相互影响的时候，碰撞就开始了；而当它们之间的距离足够大且不再显著地互相影响时，碰撞就结束了。我们可以用经典力学（牛顿定律）或量子力学（薛定谔方程）来描述一个波函数的连续演化。这两种方法产生的模型都是确定性的，但对初始条件极其敏感，因此所产生的模型会是混沌的。

非离散的经典力学解是很容易理解的。假设这些球总是有一点儿弹性，也就是说，当一个球的分子与另一个球的分子足够接近并开始相互作用时，这些球的分子就会被挤压在一起，就像弹簧被压缩了一样。此时，球的移动速度会慢下来。压缩的分子暂时将动能转化为潜在的势能，因此能量仍然是守恒的。随着球的分子被不断压缩，球的运动会减慢，直到停止。然后压缩的分子开始释放压力，将势能转化为动能，并将球推开。这样的模型是确定性的，但是，它对球的初始位置、速度和弹性非常敏感。如果这些参数略有偏差，就都会产生完全不同的运动行为。

所以我们有这样一个选择。我们可以选择接受一个离散的碰撞模型，在这种情况下，我们会失去可预测性并陷入非确定性；或者，我们可以选择拒绝接受离散性，构建一个分子相互作用的精细模型，在这种情况下，我们将失去可预测性并陷入混沌。在这两种情况下，我们都失去了可预测性。然而，接受离散碰撞的模型比建模分子相互作用的模型要简单得多，所以采纳非确定性的模型似乎是更好的选择。

### 10.4 The Hard and the Soft of Determinism

Determinism focuses our attention on a single behavior, a single reaction, a single「right answer」to the question of how a system will react to a stimulus. As an intellectual tool, it is valuable. Being able to identify the「right answer」is essential to Popper's principle of falsifiability in science. An experiment falsifies a theory if its behavior deviates by more than measurement error from the right answer predicted by the theory.

In the complementary engineering use of models, a deterministic model defines the「correct behavior」of a system. Any physical system that deviates significantly from that correct behavior is a flawed implementation of the model. A clear definition of correct behavior is a principle that underlies all of digital technology. The very notion of「digital」discretizes the messy physical world, unambiguously differentiating zero and one, yes and no, right and wrong. It is the ultimate of Serres' hard versus soft.

However, we have to carefully avoid the tarpit that results when we conflate the map with the territory. Determinism is a clear and unambiguous property of models but a muddy and treacherous property of physical systems. Nearly all fundamental models in physics are deterministic, and the question remains open whether intrinsically nondeterministic behaviors are found in the physical world. This question is philosophical more than technical because any nondeterministic model of the physical world may simply reflect an unknown unknown, some hidden variable that determines the outcome but remains invisible to us. 8 Because our knowledge of the physical world can never be complete, as observed by Hawking, we can never definitively assert that the physical world is nondeterministic. Hidden variables or unknown laws of physics may later reveal themselves as our technology and ability to measure and observe the physical world improve.

Regardless of whether the physical world is deterministic, humans have learned to build physical devices, transistors, that exhibit behavior that is extraordinarily faithful to a discrete, digital, deterministic model. The transistors in your laptop computer can switch on and off billions of times per second and operate for years without deviating from the correct behavior defined by a deterministic model. Such fidelity to a deterministic model is unrivaled by any other human-created artifact.

Thus, determinism in models is valuable, but this does not in any way imply that engineers should forgo nondeterministic models. In fact, nondeterminism is an essential tool for overcoming the limitations of determinism. For example, if a deterministic model is too complex to analyze, a nondeterministic model may be more valuable. A nondeterministic model exhibits multiple behaviors, but if all of these behaviors are demonstrably acceptable, then a nondeterministic model is just as good for building confidence in a design.

Nondeterminism has also played a central role in the theory and practice of computer science, even though Turing machines and algorithms are usually deterministic. Concurrent software, where multiple programs execute simultaneously, can be extremely difficult or even impossible to model deterministically, for example.

Nondeterminism even plays a central role in one of the key open questions in computer science: whether P equals NP. This question was apparently first raised in a 1956 letter written by Kurt Gödel to John von Neumann. The question is whether it is always true that a problem where the solution is easy to check is also easy to solve. The「N」in「NP」stands for「nondeterministic,」but it would take us too far afield to fully explain this question here. If you are interested, Wikipedia has a nice article.

In science, the models of a theory must predict the behavior of a physical system, or else the theory is not falsifiable and therefore not scientific, according to Popper. However, deterministic models do not necessarily yield predictability. Deterministic models are often extremely sensitive to initial conditions, exhibiting chaos. Even purely discrete, digital, and computational deterministic models can exhibit extremely complex chaotic behaviors.

In engineering, in contrast to science, predictability may be less important than repeatability. Repeatability ensures that an engineered system will behave as designed, with high confidence. This is valuable even if the design is able to exhibit behaviors that are too complex to predict.

According to Wolfram, the ability that digital technologies have to exhibit extremely complex behaviors justifies a belief in a「new kind of physics」that models the physical world in a purely discrete, computational way. I have argued in chapter 8 that I find it extremely unlikely that nature limits itself to the small set of processes that are computational, but even if it doesn't, computational models of the physical world are still valuable. Simulation models of weather, for example, are deterministic, chaotic, discrete, and computational, and nevertheless do a remarkable job of predicting weather for at least a few days into the future. Even if their predictive value is limited, these models lend enormous insight into the processes of nature, even if the mechanisms of the model do not match the mechanisms of nature.

Perhaps more disturbing than chaos is the incompleteness of deterministic models. Any modeling framework rich enough to include Newton's laws of motion, if it also admits discrete behaviors, is incomplete. Therefore, the family of deterministic models has「holes,」limiting cases that cannot be modeled deterministically. The philosophical implications of this observation seem profound. It implies that models of the physical world that admit both discrete and continuous behaviors must also admit nondeterminism.

Both chaos and nondeterminism limit the predictive value of models. It appears that both chaos and nondeterminism are unavoidable. Because our ability to predict is limited, our vision of the future will always remain uncertain. Any rich enough modeling framework for practical usage is going to have to deal with uncertainty. In the next chapter, I examine how to confront and manage uncertainty.

10.4 决定论的硬和软

决定论把我们的注意力集中在以一个单一的行为、单一的反应和单一的「正确答案」，来回答一个系统将如何对一个激励做出反应的问题。作为一种知识工具，它是有价值的。对于波普尔的科学可证伪性原则而言，能够确定「正确答案」是至关重要的。如果一个理论的行为与该理论预测的正确答案的偏差超过了测量误差，那么这个实验就证伪了这个理论。

在模型的工程应用中，确定性的模型定义了系统的「正确行为」。任何明显偏离正确行为的物理系统都表明实现该系统的模型是有缺陷的。对正确行为进行明确定义是所有数字技术的基本原则。

「数字」的概念将混乱的物理世界离散化，明确地区分 0 和 1，是和否，对和错。这是塞尔硬和软这一观点的根本。

然而，当我们将地图与地域混为一谈时，我们必须小心避免落入由其带来的困境。确定性是模型所具有的一种清晰、明确的属性，却是物理系统的模糊和不可靠的属性。几乎所有的基本物理模型都是确定性的，然而，物理世界是否存在一些在本质上是非确定性的行为，这仍然是一个悬而未决的问题。这个问题与其说是技术上的，不如说是哲学上的，因为物理世界的任何非确定性模型都可能只是反映了一个未知的未知，反映了一些决定结果但对我们不可见的隐藏变量。正如霍金观察到的那样，我们对物理世界的认识永远不可能是完整的，因为我们永远无法肯定地断言物理世界是非确定性的。随着我们观测物理世界的技术与能力不断提高，隐藏变量或未知的物理定律可能会在将来显现出来。

不管物理世界是否是确定性的，人类已经学会了制造诸如晶体管等物理装置，它们表现出与离散的、数字化的确定性模型高度符合的行为。你的笔记本电脑中的晶体管每秒可以开关数十亿次，工作数年而不会出现偏离由确定性模型所定义的正确行为。这种与确定性模型的高符合度是人类创造的任何其他人工制品都无法比拟的。

因此，模型中的确定性是非常有价值的，但这并不意味着工程师应该放弃非确定性的模型。事实上，非确定性是克服确定性的局限性的重要工具。例如，如果一个确定性模型因为过于复杂而难以分析，那么非确定性模型可能会更有价值。一个非确定性模型可以呈现出多种行为，但如果所有这些行为被证明是可以接受的，那么一个非确定性的模型同样可以提高设计的可信度。

尽管图灵机和算法通常都是确定性的，但是，非确定性在计算机科学的理论和实践中同样发挥了核心作用。例如，并发软件，即多个程序同时执行，可能就很难甚至是不可能被确定性地建模。

非确定性在计算机科学一个悬而未决的关键问题上也扮演着核心角色：P

是否等于 NP

。这个问题似乎是在 1956 年库尔特·哥德尔写给约翰·冯·诺依曼的一封信中首次被提出的。这个问题是，一个答案容易验证的问题是否也容易被求解。「NP

」中的「N

」代表了「非确定性」，但是，我们无法在这里充分解释这个问题，这会把我们带得太远。如果你感兴趣，可以在维基百科上找到一篇很不错的文章。

根据波普尔的说法，在科学中，一个理论的模型必须预测一个物理系统的行为，否则该理论就是不可证伪的，因此也是不科学的。然而，确定性模型不一定产生可预测性。确定性模型往往对初始条件极为敏感，也常常表现出混沌现象。即使是纯离散的、数字的和计算的确定性模型，也可能表现出极其复杂的混沌行为。

与科学相反，在工程领域，可预测性可能不如可重复性重要。可重复性能够确保一个工程系统将严格按照所设计的那样运行，具有很高的可信度。即使该设计可能呈现出过于复杂而无法预测的行为，这也是有价值的。

根据沃尔弗拉姆的说法，数字技术必须展示极其复杂的行为的这种能力，证明了一种「新物理学」的信念是合理的。这种新物理学以一种纯离散的、计算的方式建模物理世界。我曾在第 8 章中指出，我发现自然界不太可能将自身局限于一个小的计算过程的集合。即使确实如此，物理世界的计算模型也是有价值的。例如，模拟天气的模型是确定性的、混沌的、离散的和计算性的，但是，这样的天气模拟模型至少在预测未来几天的天气状况方面表现出色。即使这些模型的预测价值是有限的，即使这些模型的机制不符合大自然的机制，这些模型也提供了洞察自然界中那些过程的巨大能力。

也许比起混沌，更令人不安的是确定性模型的不完备性。任何丰富到包含了牛顿运动定律的建模框架，如果它们允许离散行为，那么它们是不完备的。因此，这类确定性模型都存在「漏洞」，也就是不能被确定性建模的极限情况。这一观点的哲学意义似乎是深远的。这意味着，既允许离散行为又允许连续行为的物理世界模型也必须允许非确定性。

混沌和非确定性都限制了模型的预测价值。混沌和非确定性似乎都是不可避免的。由于我们的预测能力有限，所以我们对未来的看法总是不确定的。任何面向实际使用的、足够丰富的建模框架都必须处理不确定性。下一章我将探讨如何面对和管理不确定性。

[1] 碰撞后，该系统中的总动量为 - 0.48×1-0.37×2+1.22×1=0，与初始动量相同。碰撞后系统的总能量为（（-0.48) 2×1+(-0.37)2×2+(1.22)2×1)/2=1，与初始能量相同。


__________

1 Author and neuroscientist Sam Harris, in his short 2012 book Free Will , argues that even without determinism, free will does not exist. His argument is quite compelling but off topic for this book.

2 For the position of a particle, this is actually a probability density not a probability. The probability of finding the particle at any specific point in space and time is zero (see chapter 11 ).

3 For a concise summary of the various interpretations that have been put forth, see Hoefer (2016). For a more in-depth study of determinism in physical models, Earman's Primer on Determinism remains a good analysis of determinism in various physical theories (Earman, 1986).

4 The momentum of a ball is the product of its velocity and its mass. The energy of a ball is half of the product of the mass and the square of the velocity.

5 The details of this thought experiment are given in Lee (2016). I will spare you the nerd storm here, but if you want to check the conclusions, please see that article. Penrose (1989) also used multiball collisions to show that the notion of determinism even in classical mechanics is problematic. His examples are a bit more complicated because they occur in more dimensions.

6 The total momentum in the system after these collisions is −0.48 × 1 − 0.37 × 2 + 1.22 × 1 = 0, same as the starting momentum. The total energy in the system after the collisions is ((−0.48) 2 × 1 + (−0.37) 2 × 2 + (1.22) 2 × 1)/2 = 1, same as the starting energy.

7 Technically, such a sequence of experiments, where the difference between them becomes vanishingly small, is called a Cauchy sequence, after the French mathematician Augustin-Louis Cauchy. A space of models is said to be complete if every Cauchy sequence in the space converges to a model in the space. This space of deterministic models is incomplete, as proved in Lee (2016).

8 In quantum mechanics, Bell's theorem, named after the Irish physicist John Stewart Bell, uses quantum entanglement to rule out hidden variables as the source for experimentally observed randomness in quantum systems. Specifically, these experiments show that taking a measurement at one point in space can instantly affect the outcome of another experiment at a remote location, seemingly in violation of the speed-of-light limits on communication. Einstein called this property of quantum physics「spooky action at a distance.」Interestingly, although Bell's theorem seems to indicate that randomness in the physical world is real, an equally explanatory resolution is that the world is actually deterministic in an extremely strong way, where every particle carries with it since its inception all the outcomes of all possible measurements that might ever be taken on it any time in the future. Hence, even this result does not definitively prove that randomness is real in the world.
