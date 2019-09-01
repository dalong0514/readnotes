# 
> 2018000模板



17. Markov Models





History is a cyclic poem written by time upon the memories of man.

—Percy Bysshe Shelley



Markov models capture systems that transition probabilistically between a finite set of states. A political system might transition between democratic and dictatorial, a market between volatile and stable regimes, or a person between happy, contemplative, anxious, and sad. In a Markov model, the movements between states occur according to fixed probabilities. The probability that a country transitions from authoritarian to democratic in a given year might be 5%; the probability that a person transitions from anxious to tired within an hour may be 20%. If, in addition, the system can move from any one state to any other through a sequence of transitions and if there exists no simple cycle of back and forth, a Markov model attains a unique statistical equilibrium.

In a statistical equilibrium, individual entities continue to move between states but the probability distribution across the states remains fixed. A statistical equilibrium in a Markov model of ideology would allow for people to transition between liberal, conservative, and independent, but the proportions of people of each ideology would remain unchanged. When applied to a single entity, a statistical equilibrium means that long-run probability of the entity being in each state does not change. A person could be in a statistical equilibrium in which he is happy 60% of the time and sad 40% of the time. The person’s mental state could change from hour to hour, but his long-run distribution across those states does not.

The unique statistical equilibrium implies that long-run distributions of outcomes cannot depend on the initial state or on the path of events. In other words, initial conditions do not matter, and history does not matter. Nor can interventions that change the state matter. As time marches on, a process that satisfies the assumptions inexorably heads to its unique statistical equilibrium and then stays there. Here again, a model reveals conditional logic: if the world fits the assumptions of a Markov model, history does not matter in the long run. The Markov model does not say that history can never matter. First, the model allows for outcome path dependence—what happens next will depend on the current state. Second, it allows for history to model in the long run as well, but for that to be the case, one of the model’s assumptions must be violated.

Markov models have myriad applications. They can be used to interpret dynamic phenomena such as democratic transitions, buildups to war, and the success of drug interventions. They can also be used to rank webpages, academic journals, and sports teams. They can even be used to adjudicate authorship of books and articles. In this chapter, we cover each of these applications. We begin with two examples and then state a general theorem for a statistical equilibrium to exist. Then, in the third section, we turn to the applications. In the discussion at the end of the chapter, we reengage the question of how and when history matters in light of our knowledge of Markov models.





Two Examples


A Markov model consists of a set of states and transition probabilities between those states. In our first example, we characterize a person’s mood on a given day as either mentally engaged or bored. These are formally represented as the two states of the model. The transition probabilities then characterize the probability of moving between states. For example, as shown in the diagram below, we assume that when mentally engaged, a person has a 90% chance of remaining in that state and a 10% chance of becoming bored, and that when bored, a person has a 70% chance of remaining bored and a 30% chance of becoming mentally engaged.





Figure 17.1: A Markov Process

Suppose that these transition probabilities hold for 100 students taking a biology class. Initially half of the students are engaged and half are bored, as shown in 17.1. Applying the transition probabilities described above, we expect that on the next day, 5 (10%) of the mentally engaged students will become bored, and 15 (30%) of the bored students will become mentally engaged. This results in 60 mentally engaged students and 40 bored students. The day following that, 6 of the 60 mentally engaged students should become bored and 12 of the bored students should become mentally engaged, resulting in 66 mentally engaged students and 34 bored students. As we continue to apply the transition rules, the process converges to a statistical equilibrium with 75 mentally engaged students and 25 bored students. In that equilibrium, students continue to move between the two states but the number of students in each state does not change.

If instead the process begins with all 100 students mentally engaged, the next day only 90 students will be mentally engaged. On the following day, that number falls to 84. If we continue to iterate the process, we find that in the long run 75 students will be mentally engaged and 25 students will be bored. The model attains the same statistical equilibrium.

In our second example, we categorize countries into three states: free, partly free, or not free. Figure 17.2 shows the percentage of countries in each of the three categories over the thirty-five-year period ending in 2010 based on Freedom House data. The figure shows a clear trend toward increased democratization. Over the past thirty-five years, the percentage of free countries has risen by 20%. If that linear trend continues, by 2040 two-thirds of all countries would be free, and by 2080 eight out of nine countries would be free.

A Markov model leads to a different prediction. To make the predictions, we set the length of a period to five years and loosely calibrate transition probabilities based on the past data (see table 17.1).1





Table 17.1: Markov Transition Probabilities for Democratization

If we initialize the model using the percentages of countries in each category in 1975, the calibrated model (as we would expect) almost perfectly matches the 2010 distribution: 48% of countries are free, 31% are partly free, and 21% are not free. The actual percentages in 2010 were 46%, 30%, and 24%. If we continue to run the model, it predicts that in 2080, 62.5% of countries will be free, 25% partly free, and 12.5% not free.





Figure 17.2: Freedom House: % Free, Partly Free, and Not Free

The less rosy prediction of the Markov model stems from the fact that a linear projection fails to take into account that free countries can transition to being partly free and also to being not free. As more countries become free, the number of free countries becoming partly free increases. The reasons for this are manifold. For one, operating a democracy requires fiscal authority and institutions capable of implementing policies. To borrow the phrasing of Flores and Nooruddin, democracy may not easily take root in some places.2 In those places, we should expect transitions from free to partly free. The Markov model captures these.





The Perron-Frobenius Theorem


Both of our examples converge to unique statistical equilibria. That was not by chance. Any Markov model with a finite set of states, fixed transition probabilities between them, the potential to move from any state to any other in a series of transitions, and no fixed cycles between states converges to a unique equilibrium.

The theorem implies that if those four assumptions are satisfied, the initial state, history, and interventions that change the state cannot change the long-run equilibrium. If nations move between dictatorships and democracies according to fixed probabilities, then interventions that impose or encourage democracies in some countries have no long-term effects. If fluctuations in dominant political ideologies satisfy the assumptions, then history cannot influence the long-run distribution over ideologies. And if a person’s mental state can be represented as a Markov model, then words of encouragement or supportive gestures have no long-run impact.





Perron-Frobenius Theorem


A Markov process converges to a unique statistical equilibrium provided it satisfies four conditions:

Finite set of states: S = {1, 2,…, K}.

Fixed transition rule: The probabilities of moving between states are fixed, for example, the probability of transitioning from state A to state B equals P(A, B) in every period.

Ergodicity (state accessibility): The system can get from any state to any other through a series of transitions.

Noncyclic: The system does not produce a deterministic cycle through a sequence of states.



The takeaway from the theorem should not be that history cannot matter but that if history does matter, one of the model’s assumptions must be violated. Two assumptions—the finite number of states and no simple cycle—almost always hold. Ergodicity can be violated, as when allies go to war and cannot transition back to an alliance. Such examples notwithstanding, ergodicity generally holds as well.

That leaves the restriction to fixed transition probabilities between states as the assumption least likely to hold. Thus, the model says that when history matters, underlying structural forces must change transition probabilities (or change the set of states). Consider the challenge of helping families to escape poverty. The forces that create social inequality have proven immune to policy interventions.3 In Markov models interventions that change families’ states—such as special programs for underperforming students or a one-day food drive—can provide temporary boosts. They cannot change the long-run equilibrium. In contrast, interventions that provide resources and training that improve people’s ability to keep jobs, and therefore change their probabilities of moving from employed to unemployed, could change long-run outcomes. At a minimum, the model gives us a terminology—the distinction between states and transition probabilities—along with a logic to see the value of changing structural forces rather than the current state.





The Sales-Durability Paradox


The sales-durability paradox states that the prevalence of a product (or an idea) depends less on its relative sales than on its durability. Markov models can explain the paradox by letting states represent the proportion of people who own a type of good. Here, we consider two types of floor coverings: tile (the durable good) and linoleum (the good with higher sales). The paradox arises when the good with higher sales, in this case linoleum, is less prevalent.

In our model, we assume that linoleum outsells tile by a ratio of 3 to 1. To capture durability differences, we assume that each year 1 in 10 people replace their linoleum floors, while only 1 in 60 people replace their tile floors. The resulting Markov model has an equilibrium in which two-thirds of floors are tile.4

The same logic that underpins the sales-durability paradox explains the positive relationship between market share and brand loyalty (the likelihood that someone switches brands). If we write a Markov model, lower brand loyalty must imply lower market share in equilibrium because loyalty operates just like durability. This empirical regularity is known as the double jeopardy law. If you have low brand loyalty, you tend to have low sales.5





Markov: One-to-Many


Markov models can be applied in a variety of contexts. We can use them to model genetic drift between the four nucleic acids: adenine (A), cytosine (C), thymine (T), and guanine (G). If each nucleic acid has a small and equal probability of becoming one of the other three types, we can write a transition matrix for drift. We can use them to model health trajectories by letting states represent health categories such as excellent, moderate, and poor. The model can evaluate how interventions such as drug protocols, behavioral changes, and surgeries change the transition probabilities and equilibrium distributions over outcomes. Interventions that produce better equilibria—that is, more people in excellent health—merit pursuing.6

Markov models can also be used to identify patterns in international crises and distinguish between transitions that lead to war and those that produce peace and reconciliation.7 This application requires us to estimate two different models, one using cases where crises led to war, and one using cases in which reconciliation occurred prior to war. If the transition probabilities in the two models differ significantly, then we can compare existing patterns, such as bombing, hostage taking, no exchange of prisoners, and escalated posturing, and see which process better fits the data.

Using Markov models to discriminate between patterns in this way can adjudicate authorship controversies. Given an author’s known writings, we can estimate the probability that one word follows another. In the text of this book, the word “the” follows the word “for” four times as often as does the word “example.” We could represent that information as transition probabilities in a large matrix. The matrix for this book would look different than the matrix for a book written by someone else. If we were to construct separate word transition matrices for Melville, Morrison, and Mao, we would see differences in their transitions between word pairs.8

Using a technique like this, we can use models to aid in assigning authorship of the Federalist Papers—eighty-five essays written in 1787 and 1788 by Alexander Hamilton, John Jay, and James Madison to convince New Yorkers to support the United States Constitution. Each essay was signed with the pen name Publius. Though the authorship of most of the essays has been settled, several remain a matter of dispute. A Markov model assigns all of the disputed essays to James Madison.9 Hamilton or Jay could have written those essays, but if either did, he wrote in the style of Madison. A similar analysis of four discourses and twelve short unattributed essays discovered by Arlene Saxonhouse showed that at least three could be attributed to Hobbes with high probability.10 In neither of these cases does the model necessarily give the correct answer. The model produces knowledge. We rely on our wisdom to decide how to weigh this model against other models or intuition.

For our last application, we describe how Markov models were used to create Google’s original PageRank algorithm. PageRank transformed search on the World Wide Web.11 The World Wide Web consists of a network of websites connected by links. To estimate the importance of each site we could count the links to and from a site. In the network of sites in figure 17.3, sites B, C, and E each have two links, A has one link, and D has no links. This method provides a crude estimate of importance, but it has flaws. Sites B, C, and E all have two links, but site E seems more important than site B given its position in the network.

PageRank considers each site to be a state in a Markov model. It then assigns a positive transition probability between two sites if they share a link. For the moment, we assign equal probability to any link; that is, we assume that a searcher at A would be equally likely to move to B or E. If our searcher goes to E, she then alternates between C and E forever. Alternatively, if she chooses B, she goes to C, and again starts alternating between C and E. In fact, beginning at any site results in alternation between C and E. Again, C and E appear to be the most important sites. Unfortunately, this model does not fit two assumptions of the Perron-Frobenius theorem. The system cannot get from any site to any other: there is no way to get from C to D. In addition, the transition probabilities create a loop between C and E.





Figure 17.3: Linkages Between Sites on the World Wide Web





Figure 17.4: Adding in Random Movements Between Sites

To fix both problems, Google added in a small random probability of moving from any site to any other as shown in figure 17.4. The model now satisfies all assumptions of the theorem and has a unique statistical equilibrium. Sites can be ranked by their probabilities in that equilibrium. A searcher who begins at A will most likely end up at C or E within a few searches. Once there, she will bounce back and forth between those two sites until trying a random site. If she goes to A or D, the path back to C will most likely go through B or E. It follows that site B should have a higher ranking than A or D, but that all three should be unlikely. In the unique statistical equilibrium shown in figure 17.5, that happens to be the case. A, B, and D are all rarely visited, but B is the most visited of the three.





Figure 17.5: Statistical Equilibrium of PageRank Model

PageRank can be thought of as a combination of the random walk model and a Markov model. If we think of PageRank as an algorithm, we realize that we can use it to produce rankings of any network. We can let nodes represent baseball or soccer teams and transition probabilities denote the percentage of time that one team defeats another.12 If the teams play only once, the transition probabilities can be assigned based on margin of victory. The resulting ranking, though not definitive, complements subjective expert assessments. We can also use PageRank to compute species’ importance using food web data.13





Summary


Markov models describe dynamic systems that move between states according to fixed transition probabilities. If we additionally assume that the process can move between any two states and that the process does not produce a cycle, then a Markov model attains a unique statistical equilibrium. In the equilibrium people or entities move between states in such a way that the probability distribution across states does not change. It follows that as a process nears that equilibrium, the changes in the probabilities diminish. Represented as a graph, the slope of the curve flattens. Recall our earlier discussion of California’s population growth when we learned linear models. California’s population growth has slowed because as the population of California has grown, the number of people leaving California has increased. That result holds true even if the proportion of Californians leaving does not change.

When applying Markov models to explain phenomena or predict trends, a modeler’s selection of the states proves critical. The choice of states determines the transition probabilities between those states. A Markov model of drug addiction could assume two states: being a user or being clean. A more elaborate model might distinguish users by frequency of use. Regardless of the choice over states, if the four assumptions hold (and in this instance, the key test would be whether transition probabilities remain fixed), then the system will produce a unique statistical equilibrium. Any one-time change in the state of a system has at most a temporary effect. Reducing drug use in equilibrium would require changing transition probabilities.

Continuing with that same logic, we can infer that a one-day event to spur interest in education may lack meaningful impact. Volunteers coming into a community and cleaning up a park may produce few long-term benefits. Any one-time influx of money, regardless of its size, will dissipate in its effect unless it changes transition probabilities. In 2010, Mark Zuckerberg donated $100 million to the Newark, New Jersey, public schools, an amount that was matched by other donors. That one-shot donation, which amounted to approximately $6,000 per student, has produced few measurable effects on test scores.14

Markov models guide action by distinguishing between policies that change transition probabilities, which can have long-term effects, and those change the state and can only have short-term effects. If transition probabilities cannot be changed, then we must reset the state on a regular schedule to change outcomes. A person’s work life may create transition probabilities that lead toward competitive, selfish, and stressful mental states. Daily exercise, meditation, or religious practice may move a person into a more grateful, compassionate, and relaxed state to start each day. Weekends perform a similar function, as do regular date nights for married couples. Both temporarily move a person’s state away from the equilibrium.

Not every dynamic system satisfies the assumptions of the Markov model. For those that do not, history, interventions, and events can have long-term consequences. In the Polya process, outcomes change the long-run equilibrium. A large intervention or shock to a system can change transition probabilities or even the set of states. Major technological improvements such as the steam engine, electricity, the telegraph, or the internet change the set of possible states of the economy. Political and social movements that define new rights or create new policies also change the set of states. We might therefore think of history as a sequence of Markov models rather than as a single process moving toward an inevitable equilibrium.





Markov Decision Models


A Markov decision model amends a Markov model by including actions. An action generates a reward, which is conditional on the state and also affects the transition probabilities between states. Given the effect of an action on transition probabilities, the optimal action does not always maximize the immediate reward.

As an example, we consider students who have a choice between two actions: surfing the internet and studying. Surfing the internet always produces the same payoff. Studying produces a high payoff when the student is engaged and a low payoff when the student is bored. To add in the effect of actions on transition probabilities, we assume that a bored student who surfs the internet remains in the bored state and that an engaged student who surfs the internet becomes bored half of the time. A student who studies has a 75% chance of being mentally engaged in the next period regardless of her present state:

Actions: surf the internet (U), study (S)

States: bored (B), mentally engaged (E)

Reward Structure





Transition Mapping





A solution to a Markov decision problem consists of an action to be taken in each state. Myopic best response behavior, which we encountered earlier, selects the reward-maximizing action in each state. In the example, that corresponds to surfing when bored and studying when mentally engaged.

The myopic solution results in the student falling into the bored state. Once that occurs, she chooses to surf the internet and remains bored in all remaining periods. Thus, her long-run average reward equals 6. The always-study solution puts her in the engaged state 75% of the time and in the bored state 25% of the time, producing an average return of 7. This solution produces a higher average payoff because she is more often in the mentally engaged state.

As seen in this example, framing a choice as a Markov decision problem can produce better actions. By taking into account the consequences of an action on our state, we choose more wisely: Sleeping late produces a higher immediate reward than getting up early and exercising. Buying an expensive coffee produces a higher reward than making our own cup. Yet, in the long run we may be happier exercising and saving money on coffee. Did we need a model for this? We might have instead turned to Proverbs 21:17: “Whoever loves pleasure will be a poor man; he who loves wine and oil will not be rich.” That may be true, but had we turned to Ecclesiastes 8:15: “And I commend joy, for man has nothing better under the sun but to eat and drink and be joyful,” we would have found an opposite proverb. By embedding our choices within a Markov decision framework, we can use logic to decide which commonsensical advice makes sense in a given setting.



