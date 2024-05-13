# 
> 2018000模板


2. Why Model?





Knowing reality means constructing systems of transformations that correspond, more or less adequately, to reality.

—Jean Piaget



In this chapter, we define types of models. Models are often described as simplifications of the world. They can be, but models can also take the form of analogies or be fictional worlds mined for ideas and insights. We also describe the uses of models. In school, we apply models to explain data. In practice, we can also use models to predict, design, and take actions. We can use models to explore ideas and possibilities. And we can use models to communicate ideas and understandings.

The value of models also resides in their ability to reveal conditions under which results hold. Most of what we know holds only in some cases: the square of the longest side of a triangle equals the sum of the squares of the other sides only if the longest side is opposite a right angle. Models reveal similar conditions for our intuitions. With models we can parse out when diseases spread, when markets work, when voting leads to good outcomes, and when crowds make accurate predictions. None of those is a sure thing.

This chapter consists of two parts. In the first, we describe the three types of models. In the second, we cover the uses of models: to reason, explain, design, communicate, act, predict, and explore. These form the acronym REDCAPE, a notso-subtle reminder that many-model thinking endows us with superpowers.1





Types of Models


When constructing a model, we take one of three approaches. We can aim for realism and follow an embodiment approach. Such models include the important parts and either strip away unnecessary dimensions and attributes or lump them together. Models of ecological glades, legislatures, and traffic systems take this approach, as do climate models and models of the brain. Or we can take an analogy approach and abstract from reality. We can model crime spreading like a disease and the taking of political positions as choices on a left-right continuum. The spherical cow is a favorite classroom example of the analogy approach: to make an estimate of the amount of leather in a cowhide, we assume a spherical cow. We do so because the integral tables in the back of calculus textbooks include tan(x) and cos(x) but not cow(x).2

While the embodiment approach stresses realism, the analogy approach tries to capture the essence of a process, system, or phenomenon. When a physicist assumes away friction but otherwise makes realistic assumptions, she takes the embodiment approach. When an economist represents competing firms as different species and defines product niches, she makes an analogy. She does so using a model developed to embody a different system. No bright line differentiates the embodiment approach from the analogy approach. Psychological models of learning that assign weights to alternatives lump together dopamine responses and other factors; they also invoke the analogy of a scale on which we balance alternatives.

A third approach, the alternative reality approach, purposely does not represent or capture reality. These models function as analytic and computational playgrounds in which we can explore possibilities. This approach allows us to discover general insights that apply outside our physical and social world. They help us to understand the implications of real-world constraints: What if energy could be sent safely and efficiently through the air? And they allow us to run impossible experiments: What if we tried to evolve a brain? This book contains a few such models, notably the Game of Life, which consists of a checkerboard whose squares are classified as either alive (black) or dead (white) that switch between alive and dead according to fixed rules. Though unrealistic, the model produces insights into self-organization, complexity, and, some argue, even life itself.

Whether embodying a more complex reality, creating an analogy, or building a made-up world for exploring ideas, a model must be communicable and tractable. We should be able to write the model in a formal language such as mathematics or computer code. When describing a model, we cannot toss out terms like beliefs or preferences without providing a formal description. Beliefs can be represented as a probability distribution over a set of events or priors. Preferences can be represented in several ways such as a ranking over a set of alternatives or as a mathematical function.

How tractable something is means how amenable it is to analysis. In the past, analysis relied on mathematical or logical reasoning. A modeler had to be able to prove each step in an argument. This constraint led to an aesthetic that valued stark models. English friar and theologian William of Ockham (1287–1347) wrote, “Plurality must never be posited without necessity.” Einstein summed up this principle, known as Ockham’s Razor, as follows: everything should be made as simple as possible, but not simpler. Today, when we run up against the constraint of analytic tractability, we can turn to computation. We can build elaborate models with many moving parts without concern for analytic tractability. Scientists take this approach when constructing models of the global climate, the brain, forest fires, and traffic. They still pay heed to Ockham’s advice, but recognize that “as simple as possible” might require a lot of moving parts.





The Seven Uses of Models


The academic literature describes dozens of uses of models. Here, we focus on seven categories of uses: to reason, explain, design, communicate, act, predict, and explore.





The Uses of Models (REDCAPE)


Reason: To identify conditions and deduce logical implications.

Explain: To provide (testable) explanations for empirical phenomena.

Design: To choose features of institutions, policies, and rules.

Communicate: To relate knowledge and understandings.

Act: To guide policy choices and strategic actions.

Predict: To make numerical and categorical predictions of future and unknown phenomena.

Explore: To investigate possibilities and hypotheticals.





REDCAPE: Reason


When constructing a model, we identify the most important actors and entities along with relevant characteristics. We then describe how those parts interact and aggregate, enabling us to derive what follows from what, and why. In doing so, we improve our reasoning. While what we can derive depends upon what we assume, we uncover more than tautologies. Rarely can we infer the full range of implications of our assumptions from inspection alone. We need formal logic. Logic also reveals impossibilities and possibilities. With it, we can derive precise and sometimes unexpected relationships. We can discover the conditionality of our intuitions.

Arrow’s theorem provides an example of how logic reveals impossibilities. The model addresses the question of whether individual preferences aggregate to form a collective preference. This model represents preferences as ordinal rankings over alternatives. If applied to five Italian restaurants, denoted by the letters A through E, the model allows any of the 120 orderings. Arrow required that the collective ordering be monotonic (if everyone ranks A above B, then so does the collective), independent of irrelevant alternatives (if no person’s relative rankings of A and B are unchanged but rankings of other alternatives change, then the order of A and B in the collective ranking does not change), and nondictatorial (no single person should decide the collective ordering). Arrow then proved that if any preferences are allowed, then no collective ordering necessarily exists.3

Logic can also reveal paradoxes. Using models we can show the possibility of each subpopulation containing a larger percentage of women than men but the total population containing a larger percentage of men, a phenomenon (Simpson’s paradox). This actually happened: 1973, the University of California, Berkeley, accepted a larger percentage of women in most departments. Overall, it accepted men at a higher rate. Models also show that it is possible for two losing bets, when played alternately, to produce a positive expected return (Parrondo’s paradox). With models, we can show that it is possible to add a node to a network and reduce the total length of the edges needed to connect all the nodes.4

We should not dismiss these examples as mathematical novelties. Each has practical applications: efforts to increase the population of women could backfire, combinations of losing investments could win, and the total length of a network of electric lines, pipelines, ethernet lines, or roads could be be reduced by adding more nodes.

Logic also uncovers mathematical relationships. Given Euclid’s axioms, a triangle can be uniquely determined by any two angles and a side, or by any two sides and an angle. With standard assumptions about consumer and firm behaviors, in markets with a large number of competing firms, price equals marginal cost. Some results are unexpected: among them the friendship paradox, which states that in any friendship network, on average, people’s friends have more friends than they do.

The paradox arises because highly popular people have more friends. Figure 2.1 shows Zachary’s Karate Network. The person represented by the dark circle has six friends, denoted by gray circles. His friends have nine friends on average. These people are represented by white circles. Over the entire network, twenty-nine of the thirty-four people have friends who are more popular than they are.5 Later we show that if we make a few more assumptions, most people’s friends will also be, on average, better-looking, kinder, richer, and smarter than they are.





Figure 2.1: The Friendship Paradox: A Person’s Friends Have More Friends

Last, and most important of all, logic reveals the conditionality of truths. A politician may claim that lowering income taxes increases government revenue by spurring economic growth. A rudimentary model in which revenue equals the tax rate times the income level proves that revenue increases only if the percentage growth in income exceeds the percentage cut in taxes.6 Thus, a 10% cut in income taxes increases revenue only if it causes income to grow by more than 10%. The politician’s logic only holds given certain conditions. Models identify those conditions.

The power of conditionality becomes evident when we contrast claims derived from models with narrative claims, even when the latter have empirical support. Consider the management proverb first things first: the idea that when facing multiple tasks, you should do the most important task first. This rule is also known as big rocks first, because when filling a bucket with rocks of various sizes, you should put the big rocks in first—if you put the little rocks in first, the big rocks will not fit.

The rule big rocks first, inferred from expert observation, may be a good rule most of the time, but it is unconditional. A model-based approach would make specific assumptions about the task and then derive an optimal rule. In the bin packing problem, a set of objects of various sizes (or weights) must be allocated into bins of finite capacity. The objective is to use as few bins as possible. Imagine, for example, you are packing up your apartment and putting everything into 2-foot-by-2-foot boxes. Ordering your possessions by size and putting each object in the first box with sufficient space (known as the first fit algorithm) turns out to be quite effective. Big rocks first works well. However, suppose that we consider a more complex task: allocating space on the International Space Station for research projects. Each project has a payload weight, a size, and power requirements along with demands on the astronauts’ time and cognitive abilities. Each also makes a potential scientific contribution. Even if we came up with some measure of bigness as a weighted average of these attributes, big rocks first would prove a poor rule given the dimensionality of interdependencies. More sophisticated algorithms and possibly market mechanisms would perform much better.7 Thus, under some conditions, big rocks first is a good rule. Under other conditions, it is not. With models, we can trace the boundaries of when we should place the big rocks first and when we should not.

Critics of formalism claim that models repackage what we already know, that they pour old wine into shiny mathematical bottles, that we do not need a model to know that two heads are better than one or that he who hesitates is lost. We can learn the value of commitment from reading of Odysseus tying himself to the mast. That criticism fails to recognize that inferences drawn from models take conditional forms: if condition A holds, then result B follows (e.g., if you are packing bins and size is the only constraint, pack the biggest objects first). Lessons drawn from literature or proverbial advice from great thinkers often provide no conditions. If we try to lead our lives or manage others by unconditional rules, we find ourselves lost in a sea of opposite proverbs. Are two heads better than one? Or, do too many cooks spoil the broth?

Proverb: Two heads are better than one

Opposite: Too many cooks spoil the broth

Proverb: He who hesitates is lost

Opposite: A stitch in time saves nine

Proverb: Tie yourself to the mast

Opposite: Keep your options open

Proverb: The perfect is the enemy of the good

Opposite: Do it well or not at all

Proverb: Actions speak louder than words

Opposite: The pen is mightier than the sword


While opposite proverbs abound, opposite theorems cannot. Within models, we make assumptions and prove theorems. Two theorems that disagree on the optimal action, make different predictions, or offer distinct explanations must make different assumptions.





REDCAPE: Explain


Models provide clear logical explanations for empirical phenomena. Economic models explain price movements and market shares. Physics models explain the rate of falling objects and the shape of trajectories. Biological models explain the distributions of species. Epidemiological models explain the speed and patterns of disease spread. Geophysical models explain the size distribution of earthquakes.

Models can explain point values and changes in their values. A model can explain the current price of pork belly futures and why prices rose over the past six months. A model can explain why a president appoints a moderate Supreme Court justice and why a candidate moves to the left or right. Models also explain shape: models of the diffusion of ideas, technologies, and diseases produce an S-shaped curve of adoption (or contagion).

The models we learn in physics, such as Boyle’s Law (a model stating that the pressure of oxygen times the volume equals a constant (PV = k)), explain phenomena unreasonably well.8 If we know the volume, we can estimate the constant k, and then explain or predict pressure P as a function of V and k. The model owes its accuracy to the fact that gases consist of simple parts that exist in large numbers and follow fixed rules: any two oxygen molecules placed in the identical situation follow the same physical laws. They exist in such large numbers that statistical averaging cancels out any randomness. Most social phenomena share none of these three attributes: social actors are heterogeneous, interact in small groups, and do not follow fixed rules. People also think. Even more problematic, people respond to social influences, meaning that behavioral variations may not cancel out. As a result, social phenomena are much less predictable than physical phenomena.9

The most effective models explain both straightforward outcomes and puzzling ones. Textbook models of markets can explain why an unanticipated increase in the demand for a normal good like shoes or potato chips increases the price in the short run, an intuitive result. These same models explain why in the long run, demand increases have less of an effect on price than the marginal cost of producing the good. Increases in demand can even produce reductions in price that result from increased returns to scale in production, a more surprising result. The same models can explain paradoxes such as why diamonds, which have little practical value, have high prices, but water, a necessity for survival, costs little.

As for the claim that models can explain anything: it is true, they can. However, a model-based explanation includes formal assumptions and explicit causal chains. Those assumptions and causal chains can be taken to data. A model that claims that high levels of criminal behavior can be explained by low probabilities of being caught can be tested.





REDCAPE: Design


Models aid in design by providing frameworks within which we can contemplate the implications of choices. Engineers use models to design supply chains. Computer scientists use models to design web protocols. Social scientists used models to design institutions.

In July 1993, a group of economists met at Caltech in Pasadena, California, to design an auction to allocate the electronic spectrum for cellular phones. In the past, the government had allocated spectrum rights to large companies for modest fees. A provision within the Omnibus Budget Reconciliation Act of 1993 allowed for auctioning the spectrum to raise money.

The radio signal from a tower covers a geographic range. Therefore, the government sought to sell licenses for specific regions: Western Oklahoma, Northern California, Massachusetts, Eastern Texas, and so on. This created a design challenge. The value of any given license for a company depended on the other licenses that company won. The license for Southern California would be worth more to a company that also owned the license for Northern California, for example. Economists refer to these interdependent valuations as externalities. The externalities had two main sources: construction and advertising. Holding neighboring licenses meant lower construction costs and the potential to exploit overlapping media markets.

The externalities created a problem with holding simultaneous auctions. A company trying to win a bundle of licenses might lose one license to another bidder and therefore lose the externalities. That company might then want to back out of its bids on other licenses. Sequential auctions had a different shortcoming. Bidders would underbid in early auctions to hedge against losing subsequent licenses.

A successful auction design had to be immune to strategic manipulation, generate efficient outcomes, and be comprehensible to participants. The economists used game theory models to analyze whether features could be exploited by strategic bidders, computer simulation models to compare the efficiency of various designs, and statistical models to choose parameters for experiments with real people. The final design, a multiple-round auction that allowed participants to back out of bids and prohibited sitting out early periods to mask intentions, proved successful. Over the past thirty years, the FCC has raised nearly $60 billion using this type of auction.10





REDCAPE: Communicate


By creating a common representation, models improve communication. Models require formal definitions of the relevant features and their relationships that we can then communicate with precision. The model F = MA relates three measurable quantities, force, mass, and acceleration, and does so in equation form. Each term is expressed in measurable units that can be communicated without fear of mis-interpretation. By comparison, the claim that “bigger, faster things generate more power” offers far less precision. Much can get lost in translation. Does bigger mean weight or size? Does faster mean velocity or acceleration? Does power mean energy or force? And how do bigger and faster combine to produce power? Attempts to formalize the claim could result in any of several forms: power could be written incorrectly as weight plus velocity (P = W + V), weight times velocity (P = WV), or weight plus acceleration (P = W + A).

When we formally define an abstract concept like political ideology using a reproducible methodology, those concepts take on some of the same features as physical qualities such as mass and acceleration. We can use a model to say that one politician is more liberal than another based on their voting records. We can then communicate that claim with precision. Liberalness is well defined and measurable. Someone can use the same method to compare other politicians. Of course, voting records may not be the only measure of liberalness. We might construct a second model that assigns ideologies based on textual analysis of speeches. With that model as well, we can communicate with clarity what we mean by more liberal.

Many underappreciate the impact of communication on progress. An idea that cannot be communicated is like a tree falling in a forest with no one around to notice it. The remarkable economic growth in the Age of Enlightenment was due in no small part to the transferability of knowledge, often in model form. In fact, the evidence suggests that the transferability of ideas may have contributed more to economic growth during that time than did levels of education: city-level growth in eighteenth-century France correlates more strongly with the number of subscriptions to Diderot’s Encyclopédie than with literacy rates.11





REDCAPE: Act


Francis Bacon wrote, “The great end of life is not knowledge but action.” Good actions require good models. Governments, corporations, and nonprofits all use models to guide actions. Whether it be raising or lowering prices, opening a new location, acquiring a company, offering universal health care, or funding an after-school program, decision-makers rely on models. On the most important actions, decision-makers use sophisticated models. Models are linked to data.

In 2008, as part of the Troubled Asset Relief Program (TARP), the Federal Reserve gave $182 billion in financial assistance to bail out the multinational insurance company American International Group (AIG). According to the US Department of the Treasury, the government chose to stabilize AIG “because its failure during the financial crisis would have had a devastating impact on our financial system and the economy.”12 The purpose of the bailout was not to save AIG but to prop up the entire financial system. Businesses fail every day, and the government does not intervene.13

The particular choices made within TARP were based on models. Figure 2.2 shows a version of a network model produced by the International Monetary Fund. The nodes (circles) represent financial institutions. The edges (the lines between the circles) represent correlations between the values of the holdings of those institutions. The color and width of an edge corresponds to the strength of the correlation between the institutions, with darker and thicker lines implying greater correlation.14

AIG occupies a central position in the network because it sold insurance to other firms. AIG held promises to pay other firms if those firms’ assets lost value. If prices fell, then AIG owed those firms money. By implication, if AIG failed, so too would the firms connected to AIG. A cascade of failures might ensue. By stabilizing AIG’s position, the government could prop up the market values of other firms in the network.15





Figure 2.2: Correlation Graph Between Financial Institutions

Figure 2.2 also helps to explain why the government let Lehman Brothers fail. Lehman did not occupy a central position in the network. We cannot rerun history, so we cannot know if the Federal Reserve took the correct action. We do know that the financial industry did not collapse as a result of Lehman’s failure. We also know that the government earned a $23 billion profit on its loan to AIG. So, we can infer that the policy choices—based on many-model thinking—were not a failure.

Models that guide action, such as policy models, often rely on data, but not all do. Most policy models also use mathematics, though that was not always true. In the past, policymakers built physical models as well. Phillips’s hydraulic model of the British economy was used to think through policy choices in the mid-twentieth century, and a physical model of San Francisco Bay was instrumental in the decision not to dam the bay for fresh water.16 The Mississippi River Basin Model Waterways Experiment Station, which covers nearly 200 acres near Clinton, Mississippi, is a miniature replica of the river’s basin built on a horizontal scale of 1:100. The model can test the upstream and downstream effects of building new dams and reservoirs. The released water follows the laws of physics within the physical structure. In these physical models, the entities themselves are analogs of the real world. The models are logical because they follow the laws of physics.

Our examples so far have considered organizations using models to act. People can do the same. When taking important actions in our personal lives, we should also use models. In deciding to purchase a home, take a new job, return to graduate school, or buy or lease a car, we can use models to guide our thinking. Those models may be qualitative rather than tied to data. Even in those cases, the models will oblige us to ask relevant questions.





REDCAPE: Predict


Models have long been used to predict. Weather forecasters, consultants, sports handicappers, and central bankers all predict using models. Police agencies and the intelligence community use models to predict criminal behavior. Epidemiologists use models to predict which strain of flu will be most widespread in the upcoming flu season. As data has become more available and granular, this use of models has grown. Twitter feeds and internet searches are used to predict consumer trends and social uprisings.

Models can predict individual events as well as general trends. On June 1, 2009, Air France flight AF 477, en route from Rio de Janeiro to Paris, crashed over the Atlantic. In the days following, rescuers found floating debris but could not locate the fuselage. By July, the batteries in the plane’s acoustic beacons were depleted, halting search efforts. A year later, a second search led by the Woods Hole Oceanographic Institution using US Navy side-scan sonar vessels and autonomous underwater vehicles also proved unsuccessful. The French Bureau d’Enquêtes et d’Analyses eventually turned to models. They applied probabilistic models to ocean currents and identified a small rectangular region as being most likely to contain the fuselage. Using the model’s prediction, searchers found the wreckage within a week.17

In the past, explanation and prediction tended to go hand in hand. Electrical engineering models that explain voltage patterns can also predict voltages. Spatial models that explain politicians’ past votes can also predict future votes. In perhaps the most famous example of applying an explanatory model to predict, the French mathematician Urbain Le Verrier applied the Newtonian laws created to explain planetary movements to evaluate the discrepancies in the orbit of Uranus. He discovered the orbits to be consistent with the presence of a large planet in the outer region of the solar system. On September 18, 1846, he sent his prediction to the Berlin Observatory. Five days later, astronomers located the planet Neptune exactly where Le Verrier had predicted it would be.

That said, prediction differs from explanation. A model can predict without explaining. Deep-learning algorithms can predict product sales, tomorrow’s weather, price trends, and some health outcomes, but they offer little in the way of explanation. Such models resemble bomb-sniffing dogs. Even though a dog’s olfactory system can determine whether a package contains explosives, we should not look to the dog for an explanation of why the bomb is there, how it works, or how to disarm it.

Note also that other models can explain but have little value as predictors. Plate tectonics models explain how earthquakes arise but do not predict when they occur. Dynamical systems models can explain hurricanes, but they cannot predict with much success when hurricanes will form or what paths they will take. And while ecology models can explain patterns of speciation, they cannot predict new types of species.18





REDCAPE: Explore


Last, we use models to explore intuitions and possibilities. These explorations can be policy-related: What if we make all city buses free? What if we let students choose which assignments determine their course grades? What if we put signs on people’s lawns showing their energy consumption? Each of these hypotheticals can be explored with models. We can also use models to explore unrealistic environments. What if Lamarck had been correct and acquired traits could be passed on to our offspring, so the children of parents with orthodontically corrected teeth would not need braces? What happens in such a world? Asking that question and exploring its implications can help to reveal the limits of evolutionary processes. Abandoning the constraints of reality can spur creativity. For this reason, advocates of the critical design movement engage in speculative fictions to generate new ideas.19

Exploration sometimes consists of comparing common assumptions across domains. To understand network effects, a modeler might begin a collection of stylized network structures and then ask whether and how network structure affects cooperation, disease spread, or social uprisings. Or a modeler might apply a collection of learning models to decisions, two-person games, and multiperson games. The purpose of these exercises is not to explain, predict, act, or design. It is to explore and learn.

When we apply a model in practice, we may use it in any of several ways. The same model may explain, predict, and guide action. As an example, on August 14, 2003, sagging trees leaning on power lines near Toledo, Ohio, created a localized power outage that spread when a software failure prevented an alarm from alerting technicians to redistribute power. Within a day, more than 50 million people in the northeastern United States and Canada had lost power. That same year, a storm knocked out a power line between Italy and Switzerland, leaving 60 million Europeans without power. Engineers and scientists turned to models that represent the power grid as a network. The models helped to explain how the failures occurred, offered predictions of regions where future failures might be likely, and also guided actions by identifying locations where new lines, transformers, and power supplies would enhance the robustness of the network. Putting one model to many uses will be a recurrent theme in this book. As we see next, one-to-many is a necessary complement to our central theme of applying many models to make sense of complex phenomena.




