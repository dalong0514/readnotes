## 1101. Probability and Possibility

· · · in which I consider the meaning of probability, which I argue is fundamentally a model of uncertainty about a system and not directly a model of that system; and in which I reconsider continuums and argue that probabilistic models over continuums reinforce the conclusion that digital physics is extremely unlikely.

1101 概率与可能性

在本章，我将探讨概率的含义，我认为概率在根本上是有关系统不确定性的模型，而不是一个系统的直接模型；我重新讨论了连续统的问题，并说明连续统上的概率模型会进一步强化数字物理学是极不可能的这一结论。

### 11.1 The Bayesians and the Frequentists

Scientists seek models of the physical world. Even if the physical world is actually deterministic, Laplace's agenda to explain the natural world with deterministic models is foiled by complexity, the incompleteness of determinism, the unpredictability of chaos, Wolpert's proof of the impossibility of Laplace's demon, or indeed all four. If we put aside the incompleteness of determinism (by disallowing models with discrete behaviors), then Laplace's agenda may still be alive but only as a philosophical question. It ceases to be a question of science or engineering because either the explainer (the demon) is impossible (per Wolpert) or any explanation has little or no predictive value due to chaos. Models without predictive value cannot be falsified and hence fail Popper's test for being scientific. Add to this Hawking's observation that Gödel's theorem implies that models of nature will never be complete and Turing's result that we cannot tell what some programs will do just by looking at the code, and it seems we have no choice but to accept uncertainty.

Note that we have to accept uncertainty even if we tenaciously cling to Einstein's「God does not play dice.」Regardless of whether the physical world has a phenomenon of random chance, our models cannot be certain. Once we have models that embrace uncertainty, those models will be robust to the philosophical question of whether chance exists in the physical world. The models will work whether it does or not.

Engineers, in contrast to scientists, seek physical realizations of models. In the previous chapter, I argued that determinism is a valuable property of models, and hence if we can find physical realizations that are faithful to deterministic models, we get a powerful partnership. However, there are limits to this approach, just as there are limits to the scientific use of deterministic models. In addition to the unpredictability of chaos, we can easily find ourselves in a situation where we just don't know enough about the physical realizations to be able to construct faithful deterministic models. In this situation, it is valuable to be able to explicitly model our lack of knowledge. This is what probabilistic models do.

Embracing uncertainty also gives us a way to manage complexity. Given any intrinsically complex system, such as the Airbus A350 considered in chapter 6 , even if we could construct a deterministic model of its behavior, that model would likely be incomprehensible. By embracing uncertainty, we change the goal. Instead of seeking certainty, we seek confidence.

But what is uncertainty, and how do we model it? Nondeterministic models give us a simple way to model uncertainty. We simply create models that have more than one allowed behavior. However, this is often too simple. Nondeterministic models, by themselves, give no indication about which of the allowed behaviors is more likely. In fact, they are missing a notion of likelihood altogether.

So now I could play a dirty trick on you. I could define randomness to be uncertainty, uncertainty to be likelihood, likelihood to be probability, and probability to be randomness. I could couch all that in fancy language so you don't even notice that it's circular. I could even throw the words「stochastic」and「measure」to lend gravitas, and you would still not know what I'm talking about. Instead, I'm going to be up front about it. Probability is circularly defined. It is an axiomatic formal system with solid, well-understood mathematical properties. It's only the interpretation, how to apply the model to the physical world, that is difficult.

Probability is a surprisingly controversial theory from a philosophical perspective, despite that it is well established and mature mathematically. One view, which happens to be my view, is that probability is a formal model for quantifying what we don't know. Perhaps the reason for the controversy is that any time we talk about what we don't know, we can't really know what we are talking about.

We can begin by understanding the distinction between nondeterminism, which talks only about possibilities , and probability, which attempts to quantify uncertainty. How uncertain are we actually? Connor, channeling Michel Serres, points out that the distinction between probability and possibility is arguably one of the many hard versus soft oppositions, as discussed in chapter 4 .

The gap between probability「uncertain but calculable」and possibility「certain but incalculable」is itself graspable only as another inflection of the hard and the soft. (Connor, 2009)

Probabilities quantify known unknowns. The unknown unknowns can only be handled with possibilities. Possibilities are modeled with nondeterminism, but to have a calculable theory of uncertainty, we need probabilities. For example, probability theory enables us to become more certain about something as we gather data while still preserving room for learning from still more data, leaving a residual uncertainty. The method for doing this is credited to Reverend Thomas Bayes, an eighteenth-century English statistician and theologian. Interestingly, the modern mathematical formulation is due to Laplace, who was apparently hedging his bets about whether his demon could actually remove all uncertainty.

I used probabilities in chapter 7 , where I talked about fair and unfair coins. In that chapter, the fair coin had a probability 0.5 of heads, whereas the unfair coin had a probability 0.9 of heads. What do these numbers really mean? In answering this question, we run amuck of a long-standing philosophical debate. Although experts in probability theory pretty much agree on the mathematical machinery that they use, they disagree on the basic meaning of these numbers. These experts fall into two camps: the frequentists and the Bayesians. In the Bayesian model, a probability is a quantified estimate of uncertainty. In the frequentist model, a probability is a statement about how repeated experiments are likely to turn out. Let me explain.

Consider the statement「the probability of heads is 0.5.」To a frequentist, this means「in repeated tosses of the coin, on average, half of the outcomes will be heads.」To a Bayesian, this same statement means「I have no idea whether a toss will yield heads or tails, so I have no reason to expect one outcome over the other.」The frequentist statement is about repeated independent experiments, whereas the Bayesian's statement is about uncertainty, about what we don't know.

Consider now the statement about the unfair coin,「the probability of heads is 0.9.」To a frequentist this means,「If I repeatedly toss the coin, on average, 9 out of 10 outcomes will be heads.」To a Bayesian this same statement means,「I believe strongly that a coin toss will very likely yield heads.」The number 0.9 is a quantification of the strength of this belief.

If you toss the unfair coin N times, both frequentists and Bayesians expect to see heads N × 0.9 times if N is large enough. This is an informal statement of a central tenet of probability called the law of large numbers . Specifically, this law asserts that for large enough N , the actual number of heads, call it M , will be close to N × 0.9. Here,「will be close to」means that the probability that M/N differs from 0.9 by more than some small number is very small. 1 Even more specifically,「very small」means that for any particular choice of , we can make this probability as small as we like by choosing a large enough N .

Despite the agreement between the frequentists and Bayesians about the law of large numbers, deep differences exist. The frequentists take the law of large numbers to be the essential definition of probability. A probability is exactly a statement about repeated experiments, no more, no less. A Bayesian, however, uses a probability as a measure of uncertainty, a subjective concept, and hence can interpret the probability to have meaning even if there is only one experiment.

Suppose you are tossing the unfair coin of chapter 7 , which has a probability of heads of 0.9. Suppose that your first toss of the unfair coin yields tails. I will be surprised. Suppose now that the second toss again yields tails. I will be even more surprised. Suppose the third toss again yields tails. Now I am astonished. The frequentists and Bayesians would agree that this sequence of events is extremely unlikely, and they both assign a probability of 0.1 × 0.1 × 0.1 = 0.001 (one in a thousand) to this outcome. Both would say,「Wow, that was really unlikely,」and they might suspect that something is amiss, but then they would part ways.

Both frequentists and Bayesians use probabilistic models to learn about the world. A frequentist might approach the coin conundrum by designing a scientific experiment to test the hypothesis that the coin you are tossing has a probability of heads of 0.9. He would call this hypothesis the「null hypothesis」and would then postulate an alternative hypothesis, for example, that the coin is actually a fair coin. 2 Then the experiment would begin. You would toss the coin once. Suppose it comes up heads. The frequentist would dispassionately observe that the probability of that occurrence was high, 0.9. Suppose the next toss yields tails. The frequentist would say,「Well, that was unlikely.」The probability that a single coin toss yields tails is 0.1, but more interestingly, in two repetitions of the experiment, we saw an outcome of tails. The probability of seeing at least one tail in two coin tosses is 0.1 × 0.9 + 0.9 × 0.1 + 0.1 × 0.1 = 0.19 (because there are three ways that could have happened).

This probability of 0.19, or 19%, is called a「 p -value.」It is a measure of the likelihood of seeing an observation at least as extreme as what was observed (one tail in two tosses) given the null hypothesis. The probability of 19% is small but not small enough to reject the null hypothesis. It could still be true that the coin is the unfair one.

The experiment would continue. You toss the coin again. Suppose it comes up tails again. We have now seen two tails in three coin tosses, which is quite unlikely if the coin is unfair in this way. Examining all the possible ways that three coin tosses could yield at least two tails, we come up with a p -value of 0.028, or 2.8%. The frequentist would now say,「Hmm… this p -value is below my threshold of 5% for rejecting the null hypothesis. I therefore conclude that the coin you are tossing is not the unfair coin I thought it was.」

The frequentist's approach to this problem is objective and scientific, in the sense of Popper. He formulated a hypothesis, designed an experiment to falsify it, and rejected the hypothesis when the data indicated that the hypothesis was likely false.

The Bayesian, however, would approach this same problem in quite a different way. She too would suspect that the coin you have tossed is not the unfair coin she thought it was. But she would start by quantifying her initial uncertainty. Let's suppose she sold you an unfair coin that has probability of heads of 0.9. She therefore believes that the coin you are tossing is very likely to be that particular unfair coin. She assigns a number to this belief, saying, for example, that she is 80% sure you are tossing the coin she sold you. This is a subjective judgement that she calls a prior probability . It is a measure of uncertainty prior to any observation of data.

Armed with this prior probability, the experiment begins. Suppose that your first coin toss comes up heads. The probability that the unfair coin comes up heads is 0.9, so she is not surprised. This seems to reinforce her prior probability. She now uses Bayes' formula, which gives her a specific way to update her prior probability, taking into account the new data.

Let U denote the assertion that the coin is the unfair coin she sold you. The Bayesian's prior probability is p ( U ) = 0.8. Let H denote the outcome that the coin toss yields heads. If the coin is unfair, then the probability of this outcome is written p ( H | U ) = 0.9, which is read「the probability is 0.9 of getting heads given that the coin is unfair.」Bayes' formula then gives our Bayesian a way to update her prior probability as follows:

The left side of this equation, p ( U | H ), is read「the probability that the coin is the unfair one given that a coin toss yielded heads.」This new probability is an updated belief called the posterior probability . It quantifies our uncertainty about whether the coin is the unfair one after observing data. Bayes' formula, therefore, gives us a systematic way to update our subjective beliefs upon making observations of the world.

We have enough information to calculate the numerator on the right side because we know that p ( H | U ) = 0.9 and p ( U ) = 0.8. The only hard part is the denominator, which is the probability of seeing heads regardless of whether the coin is unfair. This probability is a weighted average of probability of seeing heads if the coin is unfair (0.9) and the probability of seeing heads if the coin is fair (0.5), where the weights are the probability that the coin is unfair (0.8) and the probability that the coin is fair (0.2), respectively. So the denominator works out to 0.9 × 0.8 + 0.5 × 0.2 = 0.82.

Putting it all together, evaluating (2), our Bayesian calculates the posterior probability to be 0.878. She is now 87.8% sure that the coin is unfair. The observation of heads has strengthened her conviction that the coin is unfair. Before observing any data, she was 80% sure. Now she is 87.8% sure.

Let the experiment continue. Suppose that the next coin toss yields tails. This outcome is less likely under the assumption that the coin is unfair, so it should result in a lowered confidence that the coin is unfair. Our Bayesian will again apply Bayes' formula (2). She won't bore us with the details but reports that Bayes' formula gives us a new posterior probability of 0.59. She is now only 59% sure that the coin is unfair. Notice that the outcome of tails diminished her confidence by more than an outcome of heads reinforced her confidence. This is because an outcome of tails is much more unlikely than an outcome of heads, so observing this outcome carries more information. In fact, in chapter 7 , I showed how Shannon calculated that observing a tail carries about 22 times as much information as observing heads (3.32 bits vs. 0.15 bits), assuming the unfair coin. 3 Because there is more information in this observation, our Bayesian learns more and adjusts her prior probability more.

Continuing the experiment, suppose that the next coin toss again yields tails. Then by Bayes' formula, after observing this, our Bayesian will be only 22% sure that the coin is unfair. She now actually believes it is more likely that the coin is fair than unfair. The frequentist came to the same conclusion and rejected the hypothesis that the coin is unfair. But the frequentist had no mechanism to take into account the prior information that the Bayesian sold you an unfair coin. The frequentist's experiment is therefore more objective, but it also omits information that we actually have.

If we continue the experiment and observe yet another tail, our Bayesian will only be 5% sure that the coin is unfair. She is now quite sure that the coin is not the unfair coin she sold you. But it took more observations to reach that level of confidence because her prejudice had to be overcome by the data. The frequentist had no mechanism for taking into account that prejudice.

The Bayesian approach embraces subjectivity. This is consistent with an interpretation of probability as a measure of uncertainty rather than a measure of a percentage of outcomes of repeated experiments. Uncertainty is necessarily subjective. No objective physical reality can be uncertain about anything. The notion of uncertainty is a human cognitive notion.

The Bayesian interpretation of probability is completely invulnerable to the debate about whether the physical world is actually deterministic. If the world really is deterministic, then the frequentists are on a slippery slope. What does it mean to repeat an experiment? If the starting conditions of each repetition are the same and the world is deterministic, then the outcomes should also be the same. This makes the frequentist's experiment useless. So clearly the starting conditions need to be different. But how are they different? How much are they different? It seems that the variability of initial conditions would be the only source of differing outcomes, but the frequentist ignores this variability. Or is it just that the frequentist is uncertain about those starting conditions? But then, isn't the frequentist also faced with subjective uncertainty?

The frequentist interpretation of probability is problematic if you assume a deterministic physical world. The Bayesian interpretation is not. The Bayesian approach uses probability models to quantify uncertainty, and regardless of whether the physical world is deterministic, there is no shortage of uncertainty. Moreover, the Bayesian's approach systematizes learning , which is the process of reducing uncertainty. We can learn from data in less ad hoc ways. It's no wonder that the Bayesian approach dominates in the field of machine learning, where computer programs continually update probabilistic models of the world. The vandalism detector of Wikipedia that we saw in chapter 1 is an example of such a machine learning application.

Frequentists and Bayesians use pretty much the same mathematical framework, including Bayes' formula (2). Although their experimental methodology differs for the previous coin toss experiment, often they don't differ at all between the two camps. It is odd to see two major camps of intellectuals who disagree so fundamentally and yet almost always agree. It's like Dr. Seuss's The Butter Battle Book , where an arms race breaks out between two camps that differ only on which side the bread should be buttered on. The difference between the Bayesian and the frequentists is more philosophical, but at that level the difference is profound.

The Shannon notion of information dovetails nicely with the Bayesian interpretation. The intuitive notion of information is that it counters ignorance. Receiving information results in updating our model of the world or learning. The more information we receive, the more we update our model. If a toss of the unfair coin yields heads, then we are not surprised. This is what we expected. The information content is low (only 0.15 bits, as calculated in chapter 7 ). 4 So we don't update the model by much (80% to 87.8% in the earlier example). In contrast, if the toss yields tails, then we are a bit surprised. That was not a likely outcome, according to the probability of 0.1 that we assigned to it. The information content is higher (3.32 bits, as calculated in chapter 7 ). 5 We update the model by quite a bit more. If we fail to learn something from repeated observations of tails and fail to update our model, then we are just being stubborn and dogmatic.

In fact, Bayesian probability gives us a way to understand dogma. If I am initially absolutely sure that your coin is unfair, then my prior probability is p ( U ) = 1, and Bayes' formula provides no possibility for learning. In Bayes' formula (2), we will find that if p ( U ) = 1, then p ( H | U ) = p ( H ), so the posterior probability p ( U | H ) will equal the prior probability p ( U ). No matter what the outcome of coin tosses, Bayes' formula will not change our minds. Even Reverend Bayes cannot overcome stubborn dogmatism. If you are determined not to learn, then you won't learn, no matter what you observe in the world. Bayes' formula proves this.

Karl Popper, in The Logic of Scientific Discovery , objected strongly to the Bayesian approach (which he called the Laplacean approach). He argued that the Bayesian interpretation of probability is subjective, and subjectivity has no place in science.

It treats the degree of probability as a measure of the feelings of certainty or uncertainty, of belief or doubt, which may be aroused in us by certain assertions or conjectures. In connection with some nonnumerical statements, the word「probable」may be quite satisfactorily translated in this way; but an interpretation along these lines does not seem to me very satisfactory for numerical probability statements. (Popper, 1959, p. 135)

In other words, such「feelings」should not be assigned numbers. He then credits the English economist John Maynard Keynes, whose 1921 A Treatise on Probability refined Laplace's and Bayes' notion by interpreting a probability as a「degree of rational belief.」To Popper, this interpretation can more rationally be assigned a number, but it is still subjective. Popper minces no words in preferring the frequentists' approach, which he asserts is objective:

I declare my faith in an objective interpretation ; chiefly because I believe that only an objective theory can explain the application of the probability calculus within empirical science. (Popper, 1959, p. 137, emphasis in the original)

He then admits that「the subjective theory … is faced by fewer logical difficulties than is the objective theory,」but that this is because they are「non-empirical … they are tautologies.」It is a theory built on its own assumptions, like an axiomatic theory in mathematics. Popper declares this to be「utterly unacceptable.」

The frequentist perspective seems to have the advantage of better testability, appealing to Popper's preference for empirical methods. Specifically, a Bayesian approach always requires a prior probability, which is used without being tested. But instead of confirming or falsifying a hypothesis, a Bayesian will adjust the prior probability based on new evidence. How is this less empirical than the frequentist approach? A frequentist will treat repeated coin tosses as a scientific experiment designed to falsify the hypothesis that the coin is unfair. But when should falsification occur? When should the hypothesis be rejected? Frequentists use an ad hoc measure, where thresholds of 5% or 1% for the p -value are common. How is this less subjective? Even with the unfair coin, a string of tails is certainly possible. It's just not likely.

Bayes' rule provides a systematic way to learn from the observations. The Bayesian approach is consistent with the observation that all models are wrong and provides a way to improve the models. The objective approach only provides a way to reject the model, but as Kuhn points out, because all models are wrong, all hypotheses should be rejected. Nevertheless, even the frequentists aren't so rigorous and fall back on ad-hoc confidence measures such as thresholds for the p -value to determine when to reject a hypothesis.

Laplace distinctly adopted a subjective approach that Popper deems unacceptable, but this is actually a consistent position for Laplace to take. After all, Laplace believed in a deterministic world governed by deterministic models and predictable by his demon. In such a world, repeated experiments are pointless. But Laplace recognized that we don't know the initial conditions for the experiments exactly. We are uncertain about those conditions, and his probabilities model exactly that uncertainty, not some intrinsic chance in the world, where God plays dice.

The eighteenth-century Scottish philosopher David Hume supports Laplace's position (and likely influenced Laplace):

Though there be no such thing as Chance in the world; our ignorance of the real cause of any event has the same influence on the understanding, and begets a like species of belief or opinion.

There is certainly a probability, which arises from a superiority of chances on any side; and according as this superiority increases, and surpasses the opposite chances, the probability receives a proportionable increase, and begets still a higher degree of belief or assent to that side, in which we discover the superiority. [in An Enquiry Concerning Human Understanding ]

Popper's position, unlike Laplace's, emphasizes statistics rather than uncertainty. To Popper, probability is not about what we don't know but rather about aggregate behavior of large numbers of individually deterministic players. This point of view is nicely illustrated by his description of a waterfall:

Imagine a waterfall. We may discern some odd kind of regularity: the size of the currents composing the fall varies; and from time to time a splash is thrown off from the main stream; yet throughout all such variations a certain regularity is apparent which strongly suggests a statistical effect. Disregarding some unsolved problems of hydrodynamics (concerning the formation of vortices, etc.) we can, in principle, predict the path of any volume of water — say a group of molecules — with any desired degree of precision, if sufficiently precise initial conditions are given. Thus we may assume that it would be possible to foretell of any molecule, far above the waterfall, at which point it will pass over the edge, where it will reach bottom, etc. In this way the path of any number of particles may, in principle, be calculated; and given sufficient initial conditions we should be able, in principle, to deduce any one of the individual statistical fluctuations of the waterfall. (Popper, 1959, p. 202)

Popper accepts Laplace's deterministic world, but he really picked a difficult illustration. Models of fluid flow are notoriously chaotic (see figure 10.1 ), so Popper's「any desired degree of precision」is not really achievable, no matter how precise the initial conditions are. They would have to be perfect. So here we see starkly the debate. The Bayesian says that we don't know where the molecule will go (whether we can know is irrelevant) and uses probability to model that uncertainty. Popper says we can know, but we are interested in the aggregate behavior of many molecules, and we use probability to model the aggregate behavior.

Although both perspectives have merit, I personally find the Bayesian perspective more compelling for three reasons. First, the Bayesian approach embraces the notions of information and learning. In Popper's approach, any description of the aggregate behavior of deterministic molecules is either wrong or right, and it can be tested by observing the molecules in the waterfall. If through observation we find that our aggregate model is wrong, then we can update the model and try again. But that update (for Popper) must occur in a meta theory, outside the theory of probability, because probability does not model what we know and don't know, it just models aggregate behavior. The update of the model becomes subjective and possibly capricious because in principle the theory can't help us perform that update. It is ironic that many machine learning techniques used today, like those used in the vandalism detector of Wikipedia (see chapter 1 ), use Bayesian models. The irony is that machine learning algorithms are completely mechanized, operating without human intervention, and yet, according to Popper, they are subjective. It is hard to reconcile these observations.

Second, the Bayesian approach makes more sense when talking about rare events. A Bayesian can say something like,「The probability of a major earthquake in San Francisco in the next 30 years is 63%」(Field and Milner, 2008). I don't see how a frequentist could rationally make such a statement. For sure, such a statement is not falsifiable and is not a statement about aggregate behavior of many individually deterministic behaviors. 6 Such a statement, if it is backed up by rigorous research, reflects the aggregate opinion of many experts and the use of computer simulation models that are informed by prior experience with real earthquakes. However, there is nowhere near enough such prior experience to adopt a frequentist's interpretation of the probability. I nevertheless find statements about rare events useful (if scary). They quantify what we know and don't know, and reasoning about rare events is an essential part of engineering safety-critical systems, such as the Airbus A350.

Third and finally, I find the Bayesian perspective more compelling because it covers situations that seem to be simply not well handled by the frequentist interpretation. Suppose, for example, that a coin is flipped, but the outcome of the flip is obscured by a cup before you can observe it. What now is the probability that you will see heads when the cup is removed? No matter how many cup-removal experiments you perform, the outcome will always be the same, so it seems that the frequentist would have to say that the probability of heads is either zero or one, but we don't know which it is. The Bayesian, however, has no difficulty with this situation. The probability of observing heads is the same as it was before the coin was flipped.

11.1 贝叶斯学派和频率学派

科学家一直在寻找物理世界的模型。即使物理世界的确是确定性的，拉普拉斯试图以确定性的模型解释自然世界的议题也会由于复杂性、决定论的不完备性、混沌的不可预测性，以及沃尔珀特证明拉普拉斯妖的不可能性中的任意一个或者全部四个因素的出现而化为泡影。如果我们抛开决定论的不完备性（通过禁止具有离散行为的模型），那么拉普拉斯的议题仍然可能存在，但只能作为一个哲学问题来进行思考。它不再是一个科学或工程问题，因为要么解释者（恶魔）是不可能的（按照沃尔珀特的说法），要么任何解释都会由于混沌而几乎丧失预测价值。缺乏预测价值的模型不可能被证伪，因此它无法通过波普尔的科学检验。加上霍金的观察，哥德尔定理意味着自然界的模型永远不会是理想的，同时，图灵的结论表明，只是通过查看代码，我们无法了解某些程序的功能。这一切都似乎表明，我们别无选择，只能接受不确定性。

请读者们注意，即使我们坚信爱因斯坦的「上帝从不掷骰子」这一说法，我们也不得不接受不确定性的存在。无论物理世界是否存在随机现象，我们的模型都不可能是确定性的。一旦我们有了包含不确定性的模型，这些模型对物理世界中是否存在机会这一哲学问题就是有力的支撑。不管是否存在，这些模型都会发挥作用。

与科学家不同，工程师寻求模型的物理实现。在前一章的内容中，我认为确定性是模型的一个非常有价值的属性，因此，如果我们能够找到与确定性模型高度匹配的物理实现，就会得到一个强有力的伙伴关系。然而，这种方法也有其局限性，就像确定性模型的科学运用也有局限性一样。除了混沌的不可预见性，我们很容易发现自己处在这样的一种情况下：我们对物理实现的了解还不够，因此无法构建可信的确定性模型。在这种情况下，能够对我们所缺欠的知识进行明确建模仍然是很有价值的。这就是概率模型的作用。

拥抱不确定性也可以为我们提供一种应对复杂性的方法。来考虑任何本质上非常复杂的系统，例如第 6 章提到的空客 A350，即使我们能够构建一个确定性模型来描述它的行为，这个模型也很可能是不可理解的。如果我们能够认可系统存在的不确定性，那么我们会改变我们的目标。我们寻求的不再是确定性，而是可信度。

但什么是不确定性，我们又如何对其建模呢？非确定性模型给出了一种建模不确定性的简单方法。我们只需要创建具有多个被允许行为的模型就可以了。然而，这往往过于简单。非确定性模型本身并没有指明到底哪个被允许的行为更有可能发生。事实上，它们完全忽略了可能性的概念。

现在我可以在这里玩一个小戏法了。我可以将随机性定义为不确定性，然后将不确定性定义为可能性，再将可能性定义为概率，最后将概率定义为随机性。我可以用华丽的语言来描述它，这样你甚至不会注意到它是循环的。我甚至可以用「随机」和「测量」增加其分量，但你还是不知道我在说什么。当然，我不会这样做。相反，我会比较坦率地说，概率是被循环定义的。它是一个不证自明的公理系统，具有牢靠的、易于理解的数学性质。唯一需要说明的是，如何将其模型应用于物理世界，这是一个难题。

从哲学的角度来看，概率论是一套令人惊讶且有争议的理论，尽管它建立在数学之上且已发展成熟。我同意这样一个观点，即概率就是量化我们所不知道的事物的一个形式化模型。也许产生争论的原因在于，当我们在任何时候谈论我们所不知道的事物时，我们不能真正明白我们在谈论什么。

我们可以把如何理解不确定性（它只讨论可能性）和概率论（它试图量化不确定性）之间的差异作为切入点。我们到底有多么不确定呢？借用米歇尔·塞尔的观点，康纳指出，概率和可能性之间的区别是众多硬与软的对立关系中的一种，正如我们在第 4 章中讨论的那样。

概率表示「不确定但可计算」，而可能性表示「确定但不可计算」，我们只能将两者的差距视为硬与软的另外一种表现形式加以把握了。（康纳，2009）

概率用以量化已知的未知，而未知的未知只能用可能性来处理。可能性是用非确定性来建模的，但如果想要有一个可计算的不确定性理论，我们就需要概率。例如，概率论使我们在收集数据的时候，能够对某些事情更加确定，同时保留了从更多数据中学习的空间，并留下了剩余的不确定性。这一方法要归功于 18 世纪英国数理统计学家和神学家托马斯·贝叶斯。有趣的是，这个现代数学方法最早源于拉普拉斯，显然，他是在对冲他的「恶魔」是否能真正消除所有不确定性的赌注。

我在第 7 章使用了概率，当时我分析了均匀硬币和非均匀硬币的例子。在那一章中，均匀硬币正面朝上的概率为 0.5，而非均匀硬币正面朝上的概率为 0.9。这些数字的真正含义是什么？为了回答这个问题，我们先来看一场长期存在的哲学争论。虽然概率论的专家们对他们所使用的数学机制达成了很普遍的共识，但他们在这些数字的基本含义上仍然存在分歧。这些专家分为两大阵营：频率学派和贝叶斯学派。在贝叶斯学派的模型中，概率是对不确定性的量化估计。而在频率学派的模型中，概率是一种关于重复实验如何能够得出结果的表述。让我来具体解释一下。

我们来看「正面朝上的概率是 0.5」这个表述。对于频率学派，这意味着「在反复掷硬币的过程中，平均有一半的结果将是正面朝上」。而对于贝叶斯学派来说，同样的说法意味着「我不知道掷硬币的结果是正面还是背面朝上，所以我没有理由期待一种结果多于另一种结果」。频率学派的表述是关于重复的独立实验，而贝叶斯学派的表述是关于不确定性的，也就是关于我们所不知道的事物的。

现在我们来考虑关于非均匀硬币的表述，即「正面朝上的概率是 0.9」。对于一个频率论者，这意味着「如果我反复地掷这枚硬币，平均来说，10 个结果中会有 9 个是正面朝上的」。而对于一个贝叶斯论者来说，这个同样的说法表明，「我坚信掷硬币很有可能会出现正面朝上的情况」。0.9 这个数字量化了这种信念的强度。

如果你将这枚非均匀硬币掷 N

次，如果 N

是一个足够大的数值，那么频率学派和贝叶斯学派都将期望看到 N

×0.9 次正面朝上的结果。这是概率论中一个核心原则的非正式表述法，被称为大数定律。具体来说，这个定律断言，对于足够大的 N

，正面朝上的实际次数，记为 M

，将接近 N

×0.9。在这里，「将接近」意味着 M

/N

与 0.9 的差大于某个较小的数的概率非常小。更具体地说，「非常小」意味着对于任意特定值，我们可以通过选择一个足够大的 N

值来使这个概率尽可能地小。

尽管两个学派对大数定律的看法达成了一致，但是仍然存在着深层次的差异。频率学派认为，大数定律是概率的基本定义。概率就是关于重复实验的一种表述，仅此而已。然而，贝叶斯学派将概率作为不确定性的一种度量，它是一个主观概念，因此即使只有一次实验，也可以解释概率的意义。

假设你正在掷第 7 章所说的一枚非均匀硬币，其正面朝上的概率为 0.9。假设你第一次掷出的结果是背面朝上，我会对此感到惊讶。假设你第二次又掷出背面朝上的结果，我会感到更惊讶。假设第三次掷出的还是背面朝上，现在，我会惊讶至极。

频率学派和贝叶斯学派都认为这样的事件序列是极不可能发生的，他们都认为这个结果的概率是 0.1×0.1×0.1=0.001（千分之一）。两个学派都会说：「哇，那真的不太可能。」他们可能会怀疑有什么地方不对劲，但随后，他们还是会分道扬镳。

频率学派和贝叶斯学派都使用概率模型认知世界。一个频率论者可能会设计一项科学实验研究硬币难题，以检验你掷硬币时正面朝上的概率为 0.9 的假设。他将这一假设称为「零假设」，然后，再假定另一种假设，例如，硬币实际上是均匀的。之后，开始进行实验。假设结果是正面朝上。频率论者会冷静地观察到，发生这种情况的概率很高，是 0.9。假设下一次掷硬币的结果是背面朝上，频率论者则会说，「这不太可能」。掷一次硬币得出背面朝上的概率是 0.1，但更有趣的是，在两次重复的实验中，我们都看到了背面朝上的结果。在两次掷硬币的实验中，能看到至少一次背面朝上的概率为 0.1×0.9+0.9×0.1+0.1×0.1=0.19（因为有三种可能发生的结果）。

这种 0.19 或 19% 的概率被称为「p

值」。这是在给定零假设的前提下，对看到一个至少和所观察到的结果（两次掷硬币出现一次背面朝上）同样极端的可能性的度量。19% 的概率很小，但还不足以拒绝零假设。这枚硬币仍然可能是一枚非均匀的硬币。

继续进行实验。你再掷一次硬币。假设结果再次是背面朝上。那么，我们现在已经看到掷三次硬币出现两次背面朝上的结果。如果硬币是非均匀的，这样的结果应该不太可能。通过研究三次掷硬币至少出现两次背面朝上的所有可能性，我们得出 p

的值为 0.028，或者 2.8%。此时，频率论者会说：「嗯…… 这个 p

值低于我拒绝零假设的阈值 5%。因此，我得出结论是，你所掷的硬币不是我所认为的非均匀硬币。」

以波普尔的理论来看，这个频率论者对这个问题的处理方法是客观和科学的。他构造了一个假设，然后设计了一个实验来证伪它。当数据表明该假设很可能是错误的时候，他就会拒绝该假设。

然而，贝叶斯论者会以一种完全不同的方式来处理这个问题。她也会怀疑你掷的硬币不是她所认为的非均匀硬币。但她会从量化她最初的不确定性开始。假设她给你一枚非均匀硬币，其正面朝上的概率为 0.9。那么，她会认为你掷的硬币很可能就是那个特定的非均匀硬币。她先为这个信念赋一个值，例如，她认为有 80% 的把握认为你掷的是她原来给你的那枚硬币。这是一种主观判断，她将其称为先验概率。先验概率是在任何观测数据之前对不确定性的一种度量。

有了这个设定的先验概率，就可以开始实验了。假设第一次掷硬币的结果是正面朝上。因为这枚非均匀硬币正面朝上的概率是 0.9，所以贝叶斯论者并不会感到惊讶。这似乎恰恰加强了她的先验概率。她现在使用贝叶斯公式，这给了她一种特定的方法来使用这个新数据，并更新她的先验概率。

令 U

表示该硬币是她给你的非均匀硬币这一断言。这个贝叶斯先验概率为 p

(U

)=0.8。令 H

表示掷硬币得到正面朝上的结果。如果硬币是非均匀的，那么这个结果的概率是 p

(H

|U

)=0.9，意思是「假定该硬币是非均匀的，正面朝上的概率是 0.9」。然后，贝叶斯公式为贝叶斯论者给出了一种更新先验概率的方法，如下所示：

公式左边的 p

(U|H

) 表示「掷硬币得出正面朝上的结果时，该硬币为非均匀硬币的概率」。这种新的概率是一种被更新过的信念，被称为后验概率。它量化了我们在观测到数据之后关于硬币是否为非均匀硬币的不确定性。

因此，贝叶斯公式为我们提供了一种系统的方法来更新我们在观察世界时的主观信念。

我们有足够的信息来计算公式右侧分数的分子，因为我们知道 p

(H

|U

)=0.9，且 p

(U

)=0.8。唯一的难点是分母，它是硬币正面朝上的概率，无论硬币是否非均匀。这个概率就是掷非均匀硬币（0.9）时看到正面朝上的概率与掷均匀硬币（0.5）时看到正面朝上的概率的加权平均，其中权重分别为硬币为非均匀硬币的概率（0.8）和为均匀硬币的概率（0.2）。由此，分母为 0.9×0.8+0.5×0.2=0.82。

综合起来对公式（2）求值，贝叶斯论者计算出的后验概率为 0.878。也就是说，她有 87.8% 的把握确定这枚硬币是非均匀的。正面朝上的观察结果使她更加坚信该硬币是非均匀的。在观察任何数据之前，她有 80% 的把握。现在她有 87.8% 的把握了。

我们继续进行实验。假设下一次掷硬币的结果是背面朝上。然而，在假设该硬币非均匀的前提下，这一结果是不太可能发生的。因此，这个结果会导致对硬币是非均匀的信念的降低。我们的贝叶斯论者将再次运用贝叶斯公式（2）。她不会告诉我们令人厌烦的细节，但是会告诉我们，贝叶斯公式给出了一个新的后验概率为 0.59。也就是说，她现在只有 59% 的把握认为这枚硬币是非均匀的。请注意，背面朝上的结果对她信心的削弱大于正面朝上的结果对她信心的增强。这是因为，背面朝上的概率要比正面朝上的大得多，所以背面朝上的观察结果会携带更多的信息。事实上，在第 7 章中，我给出了硬币非均匀的情况下，香农如何计算出观察到硬币背面朝上所携带的信息是观察到正面朝上的 22 倍（3.32 比特对 0.15 比特）。因为这个观察带有更多的信息，也就是说，我们的贝叶斯论者了解到更多的信息，并且更多地调整了她的先验概率。

继续这个实验，假设下一次掷硬币再次出现背面朝上的结果。那么根据贝叶斯公式，在观察到这一点之后，我们的贝叶斯论者将只有 22% 的把握确信这个硬币是非均匀的。她现在实际上相信，这枚硬币更有可能是均匀的，而不是非均匀的。频率论者会得出同样的结论，并拒绝了硬币非均匀的假设。频率论者并没有任何机制去考虑贝叶斯论者给了你一枚非均匀硬币这样的先验信息。因此，频率论者的实验更加客观，但这个实验也忽略了我们实际拥有的信息。

如果我们继续实验，并再次观察到背面朝上的结果，我们的贝叶斯论者就只有 5% 的把握认为硬币是非均匀的。她现在很确定这枚硬币不是她给你的那枚非均匀硬币。但是，还是需要更多的观察才能达到这样的可信度，因为必须用数据才能消除她的偏见。然而，频率论者并没有考虑这种偏见的机制。

贝叶斯学派的方法具有主观性。这与将概率解释为不确定性的度量而非重复实验结果的百分比的度量是一致的。不确定性必然是主观的。不存在任何客观的物理现实，其关于任何事物都可能是不确定的。不确定性是人类认知范畴中的一种概念。

对于物理世界是否真是确定性的这一争论，贝叶斯学派对概率的解释是强有力的。如果世界真的是确定性的，那么频率学派的观点是站不住脚的。重复地进行一个实验到底意味着什么？

如果每一次重复实验的初始条件都是相同的且世界是确定性的，那么实验的结果应该是一样的，这就意味着这个频率论者的重复实验是毫无意义的。显然，每次重复实验的初始条件需要有所不同。但它们之间有什么差异？这种差异又有多大？初始条件上的差异性似乎是产生不同结果的唯一原因。可是，频率论者忽略了这种差异性。或者，只是说频率论者不能确定初始条件？但是，频率论者不也面临着主观的不确定性吗？

假设存在一个确定性的物理世界，那么频率学派对概率的解释就是有问题的，而贝叶斯学派的解释没有问题。贝叶斯学派使用概率模型来量化不确定性，无论物理世界是不是确定性的，不确定性都存在。此外，贝叶斯学派的方法将学习进行了系统化，这正是减少不确定性的过程。我们能够以不那么特别的方式从数据中学习。这样，贝叶斯学派的方法会在机器学习领域占据主导地位也就不足为奇了。在机器学习领域，计算机程序会不断更新世界的概率模型。我们在本书第 1 章看到的维基百科系统中的破坏行为检测器，就是这种机器学习应用的一个示例。

频率学派和贝叶斯学派使用了几乎相同的数学框架，其中包括贝叶斯公式（2）。虽然他们的实验方法与之前掷硬币的实验方法存在差异，但通常这两个阵营之间并没有什么不同。两大知识分子阵营之间的分歧如此之大，却几乎总是一致的，这一点让人感到奇怪。这就像苏斯博士的《黄油大战》一书描述的情形那样，两大阵营之间爆发了一场军备竞赛，但不同的只是应该往哪一边抹黄油。实际上，贝叶斯学派和频率学派之间的差异更为哲学，但在那个层次上，它们之间的差异是深刻的。

香农的信息概念与贝叶斯学派的解释非常吻合。直观概念是，信息对抗无知。接收信息才能不断地更新我们对世界建立的模型，或者进行学习。我们接收的信息越多，我们越能更新我们的模型。即便掷非均匀硬币出现了正面朝上的结果，我们也不会感到惊讶，因为这正是我们期待的结果之一。这个结果包含的信息量很少（按照第 7 章的计算，只有 0.15 比特）。这样来看，我们并不会对原来模型进行太多的更新（在之前的例子中，只是从 80% 增加到 87.8%）。相反，如果掷硬币后出现背面朝上的结果，那么我们会感到有点儿惊讶。因为根据我们预先的设想，出现这种结果的概率为 0.1，可以说，这是一个不太可能出现的结果。那么这个结果所包含的信息量更高（如第 7 章的计算，为 3.32 比特）。我们对模型进行了更多的更新。我们如果不能从反复观察到的硬币背面朝上的结果中学到一些东西，也不能更新我们的模型，我们就是教条和固执己见的。

事实上，贝叶斯学派的概率给了我们一种理解这种教条的方法。如果我一开始就绝对肯定硬币是非均匀的，那么我的先验概率会是 p

(U

)=1，贝叶斯公式就不可能用于学习。在贝叶斯公式（2）中，我们会看到，如果 p

(U

)=1，p

(H

|U

)=p

(H

)，那么后验概率 p

(U

|H

) 将等于先验概率 p

(U

)。无论掷硬币的结果如何，贝叶斯公式都不会改变我们的想法。即便是贝叶斯本人也不能克服顽固的教条主义。如果你下定决心不去学习，那么你便不会学习，无论你在世界上观察到了什么。贝叶斯公式恰恰证明了这一点。

在《科学发现的逻辑》一书中，卡尔·波普尔强烈反对贝叶斯学派的方法（他把这种方法称为拉普拉斯学派的方法）。他认为，贝叶斯学派对概率的解释是主观性的，而主观性在科学领域中并无地位。

该学派把可能性的程度当作一种衡量尺度，来衡量确定性或不确定性、信赖或怀疑的感觉，而这些感觉可能是由某些断言或猜想导致的。对于一些非数值型的表述而言，「可能」一词以这种方式加以解释可以令人相当满意。但在我看来，这样的解释对于数值型的概率表述似乎并不十分令人满意。（波普尔，1959:135）

换句话说，这样的「感觉」不应该被赋予数字。然后，波普尔将此归功于英国经济学家约翰·梅纳德·凯恩斯。凯恩斯在 1921 年出版的《概率论》一书中，将概率解释为「合理信念度」，完善了拉普拉斯和贝叶斯关于概率的概念。对于波普尔来说，这种解释可以更理性地赋予一个数字，但它仍然是主观的。波普尔毫不吝啬地表达了他对频率学派方法的偏爱，他断言该方法是客观的：

我声明我忠实于一个客观的解释；主要是因为我相信只有客观的理论才能解释概率微积分在经验科学中的应用。（波普尔，1959:137）

然后他承认，「主观理论…… 所面临的逻辑困难比客观理论要少一些」，但这是因为它们是「非经验性的…… 它们是恒真命题」。这是一个建立在自己假设基础之上的理论，就像数学中的公理论。波普尔宣称这是「完全不能接受的」。

频率学派的观点似乎具有更好的可测试性优势，迎合了波普尔对经验方法的偏好。具体来说，贝叶斯学派的方法总是需要一个先验概率，这个先验概率的使用并未经过测试。但是，贝叶斯学派将根据新的证据调整先验概率，而不是证明或证伪一个假设。

这种方法怎么会比频率学派的方法更缺乏经验性呢？一个频率论者会把反复掷硬币当作一项科学实验，目的是证伪硬币是非均匀的这一假设。但是对假设的证伪什么时候才能实现？什么时候应该拒绝这一假设？频率学派使用一种特殊的测量方法，其中 p

值的阈值通常为 5% 或 1%。这种方法怎么就不那么主观了？即使是非均匀的硬币，出现一连串背面朝上的结果也是有可能的，只是可能性不太大罢了。

贝叶斯公式提供了一种从观测数据中学习的系统化方法。这个贝叶斯方法恰恰印证了所有模型都是错误的这一观点，并提供了一种改进模型的方法。客观的方法只是提供一种拒绝模型的方法，但是正如库恩指出的，由于所有的模型都是错误的，所以所有的假设都应该被拒绝。即使如此，频率学派的方法也不是那么严格的，因为它依赖于特殊的置信度度量，例如 p

值的阈值，来决定何时拒绝一个假设。

拉普拉斯显然采取了波普尔认为不可接受的一种主观方法，但这实际上是拉普拉斯一贯坚持的立场。毕竟，拉普拉斯相信一个由确定性模型统治的确定性世界，而且这个世界可以由他的「恶魔」来预测。在这样的一个世界里，重复实验是毫无意义的。但是，拉普拉斯意识到，我们并不是非常清楚实验的初始条件。我们不太确定这些初始条件，而他的概率正是在建模这些不确定性，而不是在建模上帝掷骰子的世界中的某个固有机会。

18 世纪的苏格兰哲学家大卫·休谟支持拉普拉斯的立场（同时也可能影响了拉普拉斯）：

虽然世界上没有机会这种事物；我们对任何事件的真正原因的无知，也会对理解产生相同的影响，并产生一种类似的信念或观点。

当然有一种可能性，它产生于任何一方的机会优势；随着这种优势的增加，并且超过相反的可能性，这种可能性就会按比例增加，从而使我们发现优势的那一方得到了更大程度的信任和赞同。（选自《人类理解研究》）

与拉普拉斯不同，波普尔的观点强调统计而不是不确定性。对波普尔来说，概率并不是关于我们所不知道的情况的，而是有关大量确定性参与者个体的聚合行为。他对瀑布的描述很好地诠释了这一观点：

想象一个瀑布。我们可以看出某种奇怪的规律性：构成瀑布的水流大小各不相同；不时地会从主水流上溅出水花；然而，在所有这些变化中，有一种明显的规律性，它强烈地暗示了统计效应。不考虑流体动力学中那些尚未解决的问题（如漩涡的形成等），原则上说，如果给出足够精确的初始条件，我们就可以以任何期望的精度来预测任意体积的水 —— 或者一组分子 —— 的路径。因此，我们可以假设，有可能预测任何远在瀑布之上的分子的路径，它会在什么地方越过边缘，在什么地方到达底部，等等。用这种方法，原则上任何数量的粒子的路径都是可以计算的；如果给定了充分的初始条件，原则上我们应该能够推导出汇入瀑布的任何一个统计波动。（波普尔，1959:202）

波普尔接受了拉普拉斯的确定性世界，但他确实选择了一个难以解释的例子。流体流动的模型是非常混沌的（见图 10.1），因此，波普尔所说的「任意期望的精度」无法真正实现，无论初始条件多么精确。它们必须是完美的，所以，我们在这里可以看到明显的争论。贝叶斯学派会说，我们不知道分子会去向何处（我们能否知道是无关紧要的），我们只是使用概率来建模这种不确定性。波普尔说，我们可以知道，但是我们感兴趣的是许多分子的聚合行为，因此我们用概率来建模这种聚合行为。

虽然这两种观点都有优点，但是我个人认为贝叶斯学派的观点更有说服力，原因有三。首先，贝叶斯学派的方法包含了信息和学习的概念。在波普尔的方法中，对确定性分子聚集行为的任何描述要么是错误的要么是正确的，而且，这可以通过观察瀑布中的分子来检验。如果通过观察我们发现我们的聚合模型是错误的，那么我们可以更新模型，然后再次尝试。但是，这个更新（对于波普尔来说）必须发生在概率论之外的一个元理论中，因为概率并不会对我们所知道的和所不知道的事物进行建模，它只是对聚合行为进行建模。因此，模型的更新变得主观，而且可能反复无常，因为原则上讲，元理论不能帮助我们进行更新。具有讽刺意味的是，今天我们使用的许多机器学习技术，如在维基百科的破坏行为检测器中使用的技术（见第 1 章），使用的都是贝叶斯学派的模型。更具讽刺意味的是，这些机器学习算法是完全机械化的，是在没有人类干预的情况下运行的。然而，按照波普尔的说法，它们是主观性的。显然，我们很难调和这些观察及分析。

其次，贝叶斯学派的方法在讨论稀有事件的时候会更有意义。一个贝叶斯论者会说，「未来 30 年旧金山发生大地震的概率是 63%」（菲尔德和米尔纳，2008）。我认为一个频率论者不太会理性地做出这样的陈述。可以肯定的是，这样的说法是不可被证伪的，也不是关于许多不确定性个体行为的聚合行为的陈述。如果这样的说法能够得到严谨研究的支持，它就反映了许多专家的综合观点以及计算机模拟模型的使用情况，而这些模型是根据以往实际地震的经验得出的。然而，这样的先验经验还远远不够，不足以采用一个频率论者对概率所做出的解释。尽管如此，我发现对稀有事件的陈述依然是有用的（如果是令人恐慌的）。这些陈述量化了我们所知道的和不知道的事物，而且，对稀有事件的推理是安全关键工程系统的一个重要组成部分，例如空客 A350。

第三，也是最后一点，我发现贝叶斯学派的观点会更令人信服，原因在于它涵盖了那些频率学派的解释似乎无法很好进行处理的情况。

例如，假设掷出了一枚硬币，但在你能观察到它之前，掷硬币的结果被杯子挡住了。当杯子被移开时，你看到硬币正面朝上的概率是多少呢？不论你做了多少次移开杯子的实验，结果总是一样的，所以频率学派似乎不得不说硬币正面朝上的概率要么为 0 要么为 1，但我们不知道是哪一种。然而，贝叶斯学派解决这种情况并没有什么困难。他们认为观察到正面朝上的概率与掷硬币之前的情形是相同的。

### 11.2 Continuums, Again

So far, I have only considered probabilities of events with a finite number of possible outcomes. A coin toss yields either heads or tails. An earthquake either occurs or not. The real world, however, is often messier. A coin could get stuck in the mud and yield neither heads nor tails. Earthquakes are occurring all the time, although fortunately most of them are too small to feel. Many of the things we don't know have more than a finite number of possible outcomes. Probability theory needs some adaptation to reason about those.

Consider a thought experiment. Suppose you throw a dart and you measure the distance between where you are standing and where the dart lands. This process is physical, and I will define its「output」to be the final distance to the dart. Assume that distance is a continuum (see chapter 9 ), you can measure the distance precisely, and you measure the distance in inches as a real number. For example, the dart may land 120.5 inches away, which is 10 feet plus half an inch.

Now, what is the likelihood that the distance to the dart is an integer? Intuitively, I hope you see that this is extremely unlikely. In fact, with a reasonable probabilistic model of this process, the probability that the outcome is an integer is zero. There are vastly more noninteger distances than integer distances.

OK, you may say, let's measure the distance in millimeters instead of inches. What is the likelihood now that the distance is an integer? If the measurement is precise, then the probability will again be zero. There are still vastly more noninteger distances than integer distances. In fact, the probability of getting an integer will be zero for any precision of measurement.

However, things get even weirder. Suppose I throw the dart, and it lands at exactly 120.123 inches. Note that I do not require that we actually be able to measure this distance. The dart had to land somewhere, and some oracle knows that it landed at 120.123 inches, even if I don't know this. In a reasonable probabilistic model, the probability that the dart will land at 120.123 inches is zero. In fact, the probability that it will land at any specific distance is zero, and yet it lands somewhere. Wherever it lands has a probability of zero. Don't give up on probability yet. Bear with me.

For problems with a finite number of possible outcomes, such as a coin toss, a probability is a number between zero and one, where zero means that the event will not occur, and one means that it always occurs. With my dart experiment, we can no longer interpret a probability of zero to mean that the event will not occur. Under that interpretation, the dart could not land. It would have to remain suspended in mid air because every point where it could land has a probability of zero, but it does land.

Before I give you the details, let me point out a flaw in my argument already. I have asked you to imagine a physical scenario, that of throwing a dart, and use it to draw conclusions about a model, the model of distance measures in a continuum. I am asking you to confuse the map with the territory.

OK, we are going to have to pick one. Do we want to do this experiment in the physical world or in the world of models? If we do it in the physical world, then we face a number of difficulties. First, I asked you to measure the distance precisely . You can't do that in the physical world. Even the LIGO experiment makes imprecise measurements of distance, although through an extraordinary feat of engineering and a $1.1 billion investment, they have reduced the imprecision to much less than the diameter of a proton, but not to zero.

To avoid these difficulties, let's do the experiment in the world of models. Now it is a thought experiment. Now that we are in the world of models, we can assume that the dart has a distance, a real number, even if we can't measure it precisely.

The essential problem here is that distance to the dart has a truly vast number of possible values. In fact, it has an uncountably infinite number of possible values. But some values are more likely than others. It is unlikely that the dart will land one mile from me. It is also unlikely that it will land very close, say on my feet. How can we model this variability in likelihoods if all distances have a probability of zero?

In probability theory, the way this situation is handled is using a probability density rather than a probability. Specifically, I talk about the probability that the dart will land between 9 and 11 feet from me. Perhaps that probability is 0.68. A frequentist would interpret this to mean that in repeated dart throws, 68% will land between 9 and 11 feet. A Bayesian would interpret this as a belief that it is a bit more likely that the next throw will land between 9 and 11 feet than that it will land outside that range. Either way, I assign a probability to a range rather than to a particular number. Every individual number will have a probability of zero, but a range can have a probability bigger than zero.

A probability density function for our dart-throwing experiment is shown in figure 11.1 . That figure has a characteristic shape called a「bell curve,」which suggests that the dart is most likely to land in the vicinity of 10 feet because that is where the curve is highest. As we get farther away from 10 feet in either direction, the probability density decreases, but it actually never gets to zero. In such a curve, the area under the curve indicates the probability of landing within a range. For example, the area of the shaded region is about 0.68, indicating that there is a probability of 68% of landing between 9 and 11 feet. Notice that the value of the curve at a particular point is not the probability that the dart will land at that point. The probability of landing at any one point is zero. The probability of landing in a range is the area under the curve for that range.

Figure 11.1 Probability density function for the dart distance experiment.

Recall from chapter 7 that Shannon's model of information states that a rare event carries more information than a common event. If an event has a probability of zero, for example, the event that the dart lands at 120.123 inches, then an observation of that event carries an infinite amount of information, as measured in bits. Shannon nevertheless uses a finite number to model the information content in the dart throw. This finite number is a continuous entropy, which as I explained in section 7.4 does not measure information in bits. Continuous entropy is more like a probability density than a probability. We can interpret it as an information density, not as a measure of the information content (in bits) of an individual observation. This allows us to compare information densities, just as we can compare likelihoods. If the dart lands one mile from me rather than 10 feet, then it is a truly remarkable event, carrying quite a lot of information, although the probability of both outcomes is zero. Using densities allows me to make such comparisons.

The particular shape of the curve in figure 11.1 , the bell curve, is special in probability. Shannon's notion of entropy helps to explain why. The bell-shaped probability density function is called a「normal distribution」(presumably because it is more「normal」than abnormal distributions) or a「Gaussian distribution,」after the nineteenth-century German mathematician Carl Friedrich Gauss. As it happens, the normal distribution is the most random of all distributions that have a fixed mean and variance and no other constraints. 7 If you compare the entropy of two random variables with the same mean and variance, one with a normal distribution and the other with some other distribution, the one with the normal distribution has higher entropy and hence is more random.

11.2 再论连续统

迄今为止，我只考虑了出现有限数量可能结果的事件的概率。例如，掷硬币的结果要么正面朝上要么背面朝上，地震要么发生要么不发生。然而，现实世界往往更加混乱。一枚硬币可能会垂直陷在淤泥里，既不会正面朝上也不会背面朝上。地震时时刻刻都在发生，不过幸运的是，大多数地震都小得感觉不到。我们所不知道的许多事情都具有超过有限数量的可能结果。要想解释这些情形，就需要对概率论进行一些改造。

考虑一个思想实验。假设你投掷一枚飞镖，然后你要测量你站立的位置与飞镖落地的位置之间的距离。这是一个物理过程。我将它的「输出」定义为到飞镖的最终距离。假设这个距离是一个连续统（详见第 9 章）。你可以精确地测量出距离，并以英寸为单位的实数来度量距离。例如，飞镖可能在 120.5 英寸的位置落地。

现在，到飞镖的距离是整数的可能性有多大？凭直觉，我希望你明白这是不可能的。事实上，对于这个过程的一个合理的概率模型，结果是整数的概率是零。非整数的距离比整数距离要多得多。

好吧，也许你会说，让我们用毫米而不是英寸来测量距离。现在出现距离是整数的可能性又是多少呢？如果测量是精确的，那么这个概率将再次为零。非整数的距离仍然远远多于整数距离。事实上，对于任何精度的测量，得到一个整数的概率都是零。

然而，事情会变得更加奇怪。假设我投掷飞镖，它正好落在距离我 120.123 英寸的地方。请注意，我并不要求我们真的能够测量出这个距离。飞镖总得落在某个地方，某些神灵知道它落在距离我 120.123 英寸的地方，尽管我不知道。在一个合理的概率模型中，飞镖落在 120.123 英寸处的概率为零。事实上，它落在任何特定距离的概率都是零，但是它还是落在了某个地方。它落在任何地方的概率都为零。然而，我们还是不能放弃概率。现在请耐心地听我解释。

对于具有有限数量可能结果的问题，例如掷硬币，概率是 0 到 1 之间的一个数，其中 0 表示这个事件不会发生，而 1 意味着这个事件总是发生。在我的飞镖实验中，我们不能再将为 0 的概率解释为这个事件不会发生。因为根据这种解释，飞镖将无法落地。它必须一直悬停在半空中，因为它能落地的每个点的概率都是 0，但它确实落地了。

在我告诉你细节之前，让我先指出我的论点中的一个缺陷。我已经让你想象了一种物理场景 —— 投掷飞镖，然后用它来得出关于一个在连续统中测量距离的模型的一组结论。我正在让你把地图和地域混淆在一起。

好了，我们得挑一个实验方式。我们是想在物理世界还是模型世界中进行这个实验？如果我们选择在物理世界中做实验，那么我们会面临许多困难。首先，我要你精确地测量距离。而你无法在物理世界里做到精确测量。即使是激光干涉引力波天文台所做的实验也不能精确地测量距离，尽管通过卓越的工程技术以及 11 亿美元的投资，他们已经把测量距离的不精确程度降低到远远小于质子直径的程度，但仍然不能到零。

为了避免这些困难，让我们选择在模型的世界里做实验。现在，这就成了一个思想实验。我们当前身处一个模型的世界，我们可以假设飞镖有一个距离，是一个实数，即使我们不能精确地测量它。

这里的主要问题是，到飞镖的距离会有大量可能的值。事实上，它有无数可能的值。但有些值会比其他值更有可能。

飞镖不太可能落在距离我 1 英里的地方。它也不太可能落在距离我非常近的地方，例如落在我的脚上。如果所有距离的概率都为零，那么我们如何能够建模这些可能性中的变化性呢？

在概率论中，处理这种情况的方法是使用概率密度而不是概率。具体来说，我讲的是飞镖落在距离我 9~11 英尺内的概率。也许这个概率是 0.68。一个频率论者会把这个数值解释为：在反复投掷中，飞镖会落在 9 英尺到 11 英尺之间的可能性为 68%。一个贝叶斯论者则会将这个数解释为一种信念，即下一次投掷的飞镖落在 9 英尺到 11 英尺之间的可能性要大于落在这个范围之外的可能性。无论哪种方式，我都将为概率分配一个范围，而不是一个特定的数值。每个单个数值的概率都为零，但是一个范围的概率可能大于零。

我们投掷飞镖实验的概率密度函数如图 11.1 所示。这个图具有一个被称为「钟形曲线」的特殊形状，它表明飞镖最有可能落在 10 英尺附近，因为那是曲线最高的地方。在曲线的任何一个远离 10 英尺方向的过程中，概率密度都会逐渐减小，但实际上它永远不会为零。在这样的曲线中，曲线下的面积表示飞镖在一定范围内落地的概率。例如，阴影区域的面积约为 0.68，表明在 9 英尺到 11 英尺之间落地的概率为 68%。请注意，曲线在特定点上的值并不是飞镖在这一点落地的概率。飞镖在任何特定一点落地的概率都是零。在一个范围内落地的概率就是该范围内曲线下面区域的面积。

图 11.1 飞镖距离实验的概率密度函数。

回顾第 7 章的内容，香农的信息模型表明，一个稀有事件比一个普通事件携带更多的信息。如果一个事件的概率为零，例如飞镖落在 120.123 英寸处的事件，那么对该事件的一次观测将携带无限数量的以比特为单位的信息。尽管如此，香农仍然使用了一个有限的数字来建模投掷飞镖的信息量。这个有限的数字是一个连续熵，正如我在 7.4 节中所解释的，连续熵并不以比特为单位来度量信息。连续熵更像概率密度，而非概率。我们可以将其解释为一种信息密度，而不是单个观测的信息量（以比特为单位）的一种度量。这使得我们可以比较信息密度，就像我们可以比较可能性一样。如果飞镖落在离我 1 英里而不是 10 英尺的地方，那么这是一个非常值得关注的事件，它包含了相当多的信息，尽管这两种结果（落在 1 英里和落在 10 英尺的地方）的概率都为零。但是，概率密度的使用的确可以让我进行这样的比较。

图 11.1 所示曲线中的特殊形状，即钟形曲线，在概率中是非常特殊的。香农的熵的概念有助于解释其中的原因。钟形概率密度函数被称为「正态分布」（大概是因为它比异常分布更「正态」吧）或被称为「高斯分布」，以 19 世纪德国数学家卡尔·弗里德里希·高斯的名字命名。在具有固定均值和方差且没有其他约束的所有分布中，正态分布是最随机的。如果将均值和方差都相同的两个随机变量的熵进行比较，其中一个是正态分布，另一个是其他类型的分布，那么正态分布的熵更大，因而也更随机。

### 11.3 Impossibility and Improbability

In the dart thought experiment, when we toss the dart, it lands somewhere. The distance from me to where it lands is a random number selected from a continuum of possible distances. Assuming that distances form a continuum, the probability that any particular distance occurs is zero. However, a particular distance does occur. So in a continuum, a probability of zero does not indicate impossibility but rather indicates extreme improbability.

Now, risking confusing the map for the territory, if we assume that continuums exist in the physical world, then we would have to conclude that any particular thing that happens in the physical world has a probability of zero, at least according to the Bayesian model of probability. Perhaps this is fundamentally why precisely exact measurement of anything in the physical world is not possible. It would imply certainty about something that is extremely improbable. Under the Bayesian interpretation,「probability zero」means that we are almost certain that the event in question cannot occur. How could we have confidence in a measurement that reveals something that we are quite sure cannot have occurred? Probability theorists actually use such terminology, where they talk about something that will「almost surely」not occur, by which they mean it has a probability of zero, but it is still possible for it to occur.

Perhaps this is the biggest reason that the Bayesian interpretation of probability appeals to me so much more than the frequentist interpretation. All models are wrong, so certainty is unachievable. Nevertheless, some models are useful, and we use them to build confidence. Models and experiments can narrow our ignorance, but certainty is a fiction. We need to be open to continuing to learn. The Bayesian model gives us a systematic way to do that.

This is also why I do not believe that the digital physics explanation of the physical world is likely to be correct or useful (see chapter 8 ). Unless we believe that nature limits itself to countable sets, a postulate that is not testable, then the probability that any naturally occurring process is a computation is zero. It is not impossible, but it is extremely improbable. There are vastly many more processes than there are computations.

Human cognition is a naturally occurring physical process. This reasoning, therefore, leads to the conclusion that the probability that human cognition is computation is zero. There are so many fewer computations than physical processes that it is extremely unlikely that nature somehow ended up using only processes from the limited set that we call computation. It is not impossible, but it is extremely improbable.

So we should certainly not just assume that cognition is computation, as many people today do. Instead, we need evidence to support the claim. What kind of evidence? How much evidence? Bayes' formula provides guidance because it explains how to update our beliefs based on observations.

But Bayes' formula now presents us with a serious conundrum. Suppose that in equation (2) we let U represent the statement「cognition is achievable using computer programs.」Then the above cardinality reasoning seems to require us to assert that the prior probability p ( U ) is zero. If we take this to be the prior, then no observation H will result in any posterior probability p ( U | H ) that differs from zero. We are stuck with a dogmatic position that cognition is not computation, and no amount of evidence will change our minds.

I don't like dogma. Under the Bayesian interpretation, a prior probability is subjective. It is not derived from a formula or an experiment. If we have any doubt, therefore, we should not set the prior probability to zero. Based on my cardinality argument, however, it seems that our prior should be small. Because there are so many more physical processes than computations, it is unlikely but not impossible that cognition is computation. We might, for example, choose a prior of 1%, p ( U ) = 0.01. This says we believe there is a 1% chance that cognition is computation. What evidence then is required to convince us that cognition is actually computation? What observation H will yield a posterior p ( U | H ) greater than 50%, convincing us it is more likely that cognition is computation than that it is not?

Bayes' formula (2) states that our belief gets updated when we observe some experimental outcome H by multiplying our prior by 8

Let's call this quantity E the「evidence.」If E has a value larger than one, then it is evidence in favor of U . If E has a value smaller than one, then it is evidence against U . If E equals one, then it is no evidence at all because our posterior probability will be the same as the prior probability.

In section 9.3 , I considered whether the Turing test could help us determine whether a computer program has consciousness. I concluded in that section that if consciousness is not an externally observable property of the brain, then passing the Turing test provides no evidence of consciousness in a program. So if U is the postulate that a program has consciousness, and H is a passing of the Turing test, then it must be that p ( H | U )/ p ( H ) = 1 or equivalently that p ( H | U ) = p ( H ). What does this mean?

The quantity p ( H | U ) is the probability of passing the Turing test given that the program has consciousness, and p ( H ) is the probability of passing the Turing test regardless of whether the program has consciousness. Thus, for these two quantities to be equal, we just need it to be true that whether a computer program can pass the Turing test does not depend on whether the program has consciousness.

Indeed, many computer programs have been created that quite convincingly pass the Turing test, at least within limited domains. To my knowledge, none of the authors of these programs claims that their program has consciousness.

In a famous example, in the 1960s, the MIT computer scientist Joseph Weizenbaum wrote a computer program called ELIZA that was capable of engaging humans in a conversation. ELIZA would respond to humans in a manner bearing a remarkable resemblance to an empathic psychologist. Using a modern online implementation of ELIZA called「elizabot,」I had the following short conversation with ELIZA: 9

ELIZA: Please tell me what's been bothering you.

YOU: I think my computer is smarter than me.

ELIZA: Do computers worry you?

YOU: Yes

ELIZA: You are sure.

YOU: No, not really.

ELIZA: Are you saying no just to be negative?

ELIZA was the first example of programs that are now called「chatterbots.」Chatterbots are widely used for customer service call centers, airline reservation systems, toys (such as Hello Barbie ), and automated personal assistants such as Apple's Siri and Amazon's Echo. Malicious chatterbots appear in chat rooms for surreptitious advertising and to entice people to reveal personal information.

Weizenbaum claimed that ELIZA demonstrates that the appearance of human-like intelligence does not in fact imply the existence of human-like intelligence:

[M]achines are made to behave in wondrous ways, often sufficient to dazzle even the most experienced observer. But once a particular program is unmasked, once its inner workings are explained in language sufficiently plain to induce understanding, its magic crumbles away; it stands revealed as a mere collection of procedures, each quite comprehensible. The observer says to himself「I could have written that.」With that thought he moves the program in question from the shelf marked 「intelligent,」to that reserved for curios, fit to be discussed only with people less enlightened than he. (Weizenbaum, 1966)

Weizenbaum's goal with ELIZA was to demonstrate that the appearance of intelligence was easy to achieve and therefore should not be construed as evidence of real intelligence:

The object of this paper is to cause just such a reevaluation of the program about to be「explained.」Few programs ever needed it more. (Weizenbaum, 1966)

An aspect of Weizenbaum's statement is disturbing. He seems to be claiming that if a program is comprehensible, then it must not be intelligent. This implies that if intelligence is computation, then it must be a form of computation that we can't understand. Doesn't this in effect assert that we will never understand intelligence?

The notion of understanding human intelligence is self-referential because the process doing the understanding must itself be intelligent. This notion therefore is likely vulnerable to the sort of incompleteness that Gödel found in formal languages, Hawking applied to physics, and Wolpert found in Laplace's determinism. If this incompleteness is real and we will never fully understand intelligence, then Weizenbaum's criterion is valid, and we should dismiss intelligence in a program if we fully understand the program. However, I know from experience that it is not hard to write programs that nobody can fully understand. I've written quite a few myself, so this criterion is not really all that limiting. Certainly programs that exhibit digital chaos, as discussed in section 10.2 , have inexplicable behaviors.

So what kind of evidence is needed to convince us that cognition is computation? Assuming that our prior is low (e.g. p ( U ) = 0.01), then we need some sort of observation H , where the evidence E = p ( H | U )/ p ( H ) is much bigger than one. In other words, we need for p ( H | U ) to be much bigger than p ( H ). Hence, we need an observation H that is much more likely if U is true than if U is not true. To get us to a posterior of 50%, where it is equally likely that cognition is computation as that it is not, we need an observation H that is 50 times more likely if U is true than if U is not true. When the prior is small, the burden of proof is higher than if the prior is more moderate.

Alternatively, we can use many observations of weaker evidence. If the Turing test provides any evidence at all, it is at best weak evidence, where p ( H | U ) is only slightly larger than p ( H ). Equivalently, passing the Turing test is only slightly more likely if cognition is computation than if it is not. In the face of weak evidence, E is only slightly bigger than one, so if the prior is small, the posterior will still be small. It will take many instances of such weak evidence to overcome the small prior.

One alternative interpretation is that chatterbots approximate cognition, and as the software gets more sophisticated, the approximation gets arbitrarily close to actual cognition. Is getting arbitrarily close sufficient? I argued in section 9.3 that we cannot assume a close approximation of a process has the same properties as the process itself unless no significant difference is found between a continuum and a countable set. This observation is reinforced in section 10.3 , where a billiard ball thought experiment has the property that all close approximations of simultaneous collisions are deterministic but the actual simultaneous collisions are not. If a close approximation to cognition is not actually cognition, then it is easy to show that the Turing test provides no evidence that a program achieves cognition. Under these assumptions, we can, in principle, make a computer program where p ( H ) is as close as we like to p ( H | U ). As the program gets more sophisticated, the evidence for cognition E gets arbitrarily close to one, which is the value for no evidence at all.

So things don't look good for the claim that cognition is computation. If the Turing test can provide only weak evidence and the prior is low, then it will take a large number of observations to build support for this claim. If the Turing test provides no evidence, then what other experiment should we conduct to update our low prior probability that cognition is computation? The evidence is not there, so the claim that cognition is computation is ultimately faith based. A claim that cognition is computation amounts to an unreasonably high prior, given the cardinality argument and no effective method for updating the prior with experimental evidence. This is the essence of faith.

I'm an engineer not a scientist. My goal isn't to model the physical world or replicate natural processes such as human cognition. My goal instead is to make physical systems that do interesting and useful things. I believe we can do interesting things with computation even if we can't replicate human cognition. In fact, I will argue in the next chapter that we probably don't even want to replicate human cognition in computers. We can do many more useful things with computers that complement human capabilities. In chapter 9 , I argued that the concept of semantics makes the human-computer partnership powerful indeed. Digital technology, together with the stack of hardware and software paradigms that humans have constructed already, is a truly rich medium for modeling, even if the total number of such models is tiny compared with the possibilities. We know how to build faithful physical realizations for almost all of these models. Using Bayesian reasoning, we also know how to model what we don't know about these physical realizations. This gives us a truly expressive toolkit for creativity. I believe we have barely scratched the surface of what we can do with it.

11.3 不可能与不大可能

在飞镖的思想实验中，当我们投掷飞镖时，它必然会落在某个位置。从我到它落地位置的距离是从可能距离的连续统中选择的一个随机数。因为这些距离构成了一个连续统，所以，出现任何特定距离的概率都为零。然而，确实会存在一个特定的距离。所以在一个连续统中，为零的概率并非表示不可能，而是极不可能。

现在，冒着混淆地图与地域的风险，如果我们假设物理世界中存在连续统，那么我们必须得出这样一个结论，在物理世界中发生任何特定事情的概率都是零，至少贝叶斯学派的概率模型是这样的。也许这就是不可能对物理世界中的任何事物进行精确测量的根本原因。这将意味着一些极不可能的事情的确定性。根据贝叶斯学派的解释，「概率为零」意味着我们几乎可以肯定所讨论的事件不会发生。我们又怎么能对揭示了我们非常确定不可能发生的事情的测量充满信心呢？实际上，概率理论者使用概率为零这样的术语来表明他们所谈论的事情「几乎肯定」不会发生，他们的意思是它的概率为零，但它仍然有可能发生。也许这就是贝叶斯学派对概率的解释比频率学派的解释更吸引我的原因。所有模型都是有误差的，所以不可能实现确定性。然而，有些模型是有用的，我们可以用它们来增加可信度。模型和实验可以减少我们的无知，但确定性是虚构的。我们需要以开放的心态继续学习。可以说，贝叶斯学派的模型为我们提供了一种系统的方法。

这也是为什么我不相信物理世界的数字物理学解释可能是正确的或有用的观点（见第 8 章）。除非我们相信大自然将其自身限定在了一组可数集合中，这是一个不可测试的假设，那么任何自然发生的过程是一个计算的概率为零。这不是不可能的，而是极不可能的。因为自然界中存在着大量无法计算的过程。

人类的认知是一个自然发生的物理过程。由此推论，人类认知是计算的概率为零。计算比物理过程要少得多，因此，在某种程度上，自然界最终只使用我们称为计算的有限集合中的过程，这是极不可能的。还是那句话，这不是不可能，而是极其不可能。

因此，我们当然不应该仅仅假设认知就是计算，正如今天许多人所做的那样。相反，我们需要证据来支撑这种观点。我们需要什么样的证据？需要多少证据呢？贝叶斯公式为我们提供了指导，因为它解释了如何根据观察来更新我们的信念。

但是，贝叶斯公式现在给我们带来了一个严重的问题。假设在方程（2）中，我们让 U

表示「认知是可以用计算机程序实现的」这一命题。那么，之前势的推理似乎要求我们要断言先验概率 p

(U

) 为零。如果我们把这个当作先验概率，那么任何观测 H

都不会产生不等于零的后验概率 p

(U

|H

)。我们坚持一种有些固执的立场，即认知不是计算，再多的证据也不能改变我们的想法。

我本人并不喜欢固执。在贝叶斯学派的解释下，先验概率是主观的。它不是由公式或实验得出的。因此，如果我们有任何疑问，我们就不应将先验概率的值设为零。然而，基于我对势的论证，我们的先验概率似乎应该是比较小的。因为物理过程的数量要远多于计算，所以认知是计算的可能性不大，但也并非不可能。例如，我们可以选择先验概率为 1%，即 p

(U

)=0.01。这表示我们相信认知就是计算的可能性为 1%。那么需要用什么样的证据来说服我们认知实际上就是计算呢？什么样的观测 H

会产生一个大于 50% 的后验概率 p

(U

|H

)，使我们相信认知更有可能是计算呢？

贝叶斯公式（2）表明，当我们观测到某个实验结果 H

时，我们的信念通过将我们的先验概率与下式相乘而得到更新。我们把 E

称为「证据」。如果 E

的值大于 1，那么它是有利于 U

的证据。如果 E

的值小于 1，那么它是不利于 U

的证据。如果 E

等于 1，那么它根本不是证据，因为那样的话，我们的后验概率将与先验概率相同。

在 9.3 节中，我探究了图灵测试是否能够帮助我们确定一个计算机程序具有意识的问题。我在那一节中得出的结论是，如果意识不是大脑的一种外部可观察到的属性，那么即便通过了图灵测试，它也不能提供在程序中存在意识的证据。因此，如果 U

是程序具有意识的假设，H

是通过图灵测试的结果，那么必然有 p

(H

|U

)/p

(H

)=1，或者是，p

(H

|U

)=p

(H

)。这意味着什么？

假设程序是有意识的，p

(H

|U

) 这个量是通过图灵测试的概率，而 p

(H

) 表示不论程序是否有意识时通过图灵测试的概率。因此，要使这两个量相等，我们只需要这样一个命题成立，即一个计算机程序能否通过图灵测试并不取决于该程序是否拥有意识。

事实上，已经有许多可以令人满意地通过图灵测试的计算机程序被开发出来，至少在有限的领域内是这样的。据我所知，这些程序的设计者中尚无一人声称他们的程序是有意识的。

有这样一个著名的例子。20 世纪 60 年代，麻省理工学院的计算机科学家约瑟夫·魏泽堡编写了一个名为伊莉莎（ELIZA）的计算机程序，它能够与人进行对话。伊莉莎会以一种类似共情心理学家的交流方式回应人类。使用伊莉莎的一个最新版在线实现程序「elizabot

」，我与伊莉莎进行了如下简短的交谈：伊莉莎：请告诉我，什么事一直让你心烦？

你：我觉得我的计算机比我更聪明。

伊莉莎：计算机令你感到担心吗？

你：是的。

伊莉莎：你确定吗？

你：不，不太确定。

伊莉莎：你回答不仅是为了否定吗？

伊莉莎是现在被称为「聊天机器人」计算机程序的第一个示例。聊天机器人被广泛应用于客户服务呼叫中心、航空订票系统、玩具（如智能芭比娃娃玩具 Hello Barbie）以及自动个人助理软件（如苹果手机的 Siri 和亚马逊的 EcHo）。当然，恶意的聊天机器人也常常会出现在聊天室里，暗中投放广告，并诱使人们泄露个人信息。

魏泽堡声称，伊莉莎证明了类人智能的出现实际上并不意味着类人智能的存在：

机器被制造出来并以令人惊讶的方式运转，往往足以让最有经验的观察者觉得眼花缭乱。但是，一旦一个特定的程序被揭开了面纱，一旦它的内部运作原理能够被语言解释得足够清晰并让人们理解，它的魔力就会消失；它只不过是一些程序的集合，而其中的每个程序都非常容易理解。于是，观察者会自言自语地说：「我本可以写出这样的程序。」带着这样的想法，他将把这个有问题的程序从标有「智能」的架子移到保存老古董的架子上，以后只适合用来和不如他有见识的人进行讨论。（魏泽堡，1966）

魏泽堡研究伊莉莎是为了证明，智能的表象是很容易实现的，因此，其不应被解释为真正智能的证据：

本文的目的就是要对即将被「解释」的程序进行这样的重新评估。很少有程序需要被重新评估。（魏泽堡，1966）

魏泽堡的声明有一个令人感到不安的方面。他似乎要声明，如果一个程序是可以理解的，那么它一定不是智能的。这意味着，如果智能就是计算，那么它一定是一种我们无法理解的计算形式。这难道不是在断言，我们永远都无法理解智能吗？

理解人类智能的概念是自我参照的，因为进行理解的过程本身必须是智能的。因此，这一概念很容易受到哥德尔在形式语言中发现的那种不完备性的影响，霍金将其应用在物理学中，而沃尔珀特在拉普拉斯的决定论中也发现了这种不完备性。如果这种不完备性是成立的，且我们永远无法完全理解智能，那么魏泽堡的标准就是有效的，而且，我们如果完全理解了一个程序，我们就应该摒弃这个程序中的智能。然而，以我的经验来看，编写没有人能够完全理解的程序并不是一件难事，我自己就写了不少这样的程序。所以魏泽堡的标准并不是真正的限制。当然，正如 10.2 节所讨论的，呈现数字混沌的那些程序有着无法解释的行为。

那么，到底需要什么样的证据才能说服我们相信认知就是计算呢？假设我们的先验概率很小［如 p

(U

)=0.01］，那么我们需要某种观测 H

，其中证据 E

=p

(H

|U

)/p

(H

) 远大于 1。换句话说，我们需要 p

(H

|U

) 比 p

(H

) 大得多。因此，我们需要一个观测 H

，其在 U

为真时比 U

不为真时更可能出现。为了使我们得到一个 50% 的后验概率，即认知是计算的可能性与不是计算的可能性是一样的，我们就需要一个观测 H

，其在 U

为真时的可能性是 U

不为真时的 50 倍。当先验概率较小时，举证的责任比先验概率中等大小时要更高，。

或者，我们可以使用许多证据力度较弱的观测结果。如果图灵测试提供了任何证据，那么它们最好是较弱的证据，且 p

(H

|U

) 仅略大于 p

(H

)。同样，如果认知是计算时通过图灵测试的可能性只比不是计算时的可能性大了一些。在证据较弱的情况下，E

仅略大于 1，因此如果先验概率较小，那么后验概率也会较小。要克服先验概率较小的问题，就需要大量这样较弱的证据。

另一种解释是，聊天机器人近似于人类的认知能力，当软件变得越来越复杂时，它的认知功能会任意接近真实的认知能力。

那么，任意地接近就足够了吗？我已在 9.3 节中强调，除非在一个连续统和一个可数集合之间没有明显的差别，否则我们不能假定一个过程的近似具有与这个过程本身相同的特性。这一观点在 10.3 节得到强化，其中的桌球思想实验就具有这样的特性，即所有近似同时发生的碰撞都是确定性的，但实际中同时发生的碰撞却不是。如果对认知的一个近似实际上并不是认知，那么很容易证明图灵测试并没有提供任何证据来证明一个程序实现了认知。在这些假设之下，我们原则上可以设计一个计算机程序，从而让 p

(H

) 无限接近我们所期待的 p

(H

|U

)。随着程序变得越来越复杂，认知的证据 E

会无限接近 1，这个值根本无法提供任何证据。

显然，认知就是计算这一说法看起来并不乐观。如果图灵测试只能提供薄弱的证据，而且先验概率较小，我们就需要大量的观测结果来支持这个说法。如果图灵测试没有提供任何证据，那么我们还应该开展什么样的实验，以更新认知就是计算的较小先验概率呢？结论是，这样的证据是不存在的，因此，认知就是计算的说法最终是基于信念的。鉴于势的讨论以及没有以实验证据来更新先验概率的有效方法，认知就是计算这一主张等于设置了一个不合理的高先验概率。这就是信念的本质。

我是工程师，不是科学家。我的目标不是建模物理世界，或者复制诸如人类认知这样的自然过程。相反，我的目标是让物理系统做有趣的和有用的事情。我相信，即使我们不能复制人类的认知能力，我们也可以用计算做一些有趣的事情。我将在下一章中论证，我们可能甚至并不想在计算机上复制人类的认知。

我们可以用计算机做更多有用的事情来扩充人类的能力。在第 9 章中，我论证了语义学的概念确实使人与计算机之间的伙伴关系更加强大。即使与无限的可能性相比，这些模型的总数也很渺小。然而，数字技术，连同人类已经构建的硬件和软件范式的堆叠栈，是一个真正丰富的建模媒介，即使这样的模型总数与可能的模型数量相比还很小。我们知道如何为几乎所有这些模型建立高度匹配的物理实现。通过使用贝叶斯推理，我们也知道如何建模我们对这些物理实现所不了解的某些方面。这为我们提供了一个真正表达创造力的工具箱。我相信，到目前为止，我们对用它能做什么的认识还很肤浅。

__________

1 Nerds like to use the Greek letter (epsilon) for small differences. This even creeps into the vernacular, where a Nerd may assert, for example,「I am within epsilon of finishing this book.」

2 Actually, the alternative hypothesis could be much broader. It could be that the probability of heads is some unknown value less than 0.9. This hypothesis includes even the possibility that the coin is some other unfair coin, for example, one where the probability of heads is 0.1. This would not change the experiment or its conclusions in any way.

3 In chapter 7 , we assumed the coin was the unfair one. We can adjust the information content calculation to take into account that we are only 80% sure that the coin is unfair. With this adjustment, the probability of heads becomes p ( H ) = 0.82 instead of 0.9. The information content in an outcome of heads becomes 0.29 bits instead of 0.15. Correspondingly, the probability of tails becomes p ( T ) = 0.18 instead of 0.1, and the information content in observing tails drops from 3.32 bits to 2.47 bits.

4 Or 0.29 bits after adjusting the calculation to use the prior.

5 Or 2.47 bits after adjusting to use the prior.

6 Unless, I suppose, we adopt Everett's many worlds interpretation of quantum mechanics, which postulates that many worlds exist in parallel at the same time and in the same space as our own. Hence, there are many San Franciscos, some of which will have earthquakes and some of which will not. However, even that theory does not permit any observation of the many worlds, so it is still not falsifiable.

7 The mean, also called the expected value, is the center of mass of the probability density function. For a normal distribution, the mean is where the distribution peaks, or equivalently, the outcome where it is equally likely to get a result above as below it. For a frequentist, the mean is the average value of an infinite number of experimental outcomes. For a Bayesian, the term「expected value」makes more sense than average, as it captures the subjectivity of probabilities. The variance is the average (or expected value) of the square of the outcomes minus the mean. It measures how variable the outcomes are likely to be. If the variance is large, then many outcomes will be far from the mean, whereas if it is small, then most outcomes are close to the mean.

8 By Messerschmitt's law (see footnote on page 14 ), it doesn't matter what I write from here on. I am now truly feeling free.

9 http://www.masswerk.at/elizabot/

12
