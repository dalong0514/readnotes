# 
> 2018000模板


21. Game Theory Models Times Three



Deductive reasoning travels from the most abstract to the least abstract. It begins with a set of axioms and uses the laws of logic and mathematics to manipulate them to form predictions about the world.

—Rachel Croson



Game theory models strategic interactions. Many of the models that follow, including our models of cooperation, signaling, mechanisms, and collection action, involve games. We do not take up the analysis of games in much depth because entire books are devoted to the subject. Our goal will be to provide a gentle introduction. To that end, we present examples of the three main classes of games: normal-form games, in which players choose from a discrete set of actions (typically two); sequential games, in which players choose actions sequentially; and continuous-action games, in which players can choose actions of any magnitude or effect size. These examples introduce the main concepts, help us to understand later models, and add value in their own right.

The remainder of the chapter has four parts. We begin by covering 2-by-2 zero-sum games. In a zero-sum game, each of two players chooses among two actions. No matter what actions the players choose, the amount won by one player is exactly offset by the losses of the other. We use zero-sum games to define the basic terminology of game theory, to distinguish between strategies and actions, and to introduce the concept of iterated elimination of dominated strategies. We then study the Market Entry Game, a sequential game, in which an entrant competes against an existing firm, and we replicate that game many times to create what is known as the chain store paradox. In the third part, we consider an effort game in which individuals choose effort levels to win a prize of a fixed amount. Increasing effort improves a player’s chances of winning the prize. The chapter concludes with a brief discussion of the value of game theory models generally.





Normal-Form Zero-Sum Games


In this section we analyze two-player normal-form zero-sum games. In both games, each player chooses an action and receives a payoff that depends on the player’s own action and the other player’s action. In addition, the players’ payoffs sum to zero. In the first game, Matching Pennies shown in figure 21.1, each player chooses one of two actions: heads or tails. The row player wants to match the other player’s choice, and the column player wants to mismatch. Payoffs are shown in the matrix below:





Figure 21.1: The Matching Pennies Game

A strategy is a rule for how to play the game. It could be a choice of a single action, a randomization between actions, or, as we see in the next section, a sequence of actions. A Nash equilibrium of a game is a pair of strategies such that each player’s strategy is optimal given the strategy of the other player. In Matching Pennies, in the unique equilibrium strategy both players randomize equally between the two actions. To prove randomization is an equilibrium, we need to show that if each player randomizes, the other player cannot do better than randomizing. This is straightforward. If the row player (actions and payoffs in bold) plays heads with probability and tails with probability , then the column player earns zero regardless of her action. Therefore, randomizing is also an optimal strategy for the column player. By symmetry, randomization is optimal for the row player as well.

This optimality of randomization has implications for behavior in strategic settings. Sports are zero-sum: one team (or player) wins and one loses. During penalty kicks, a striker wants to randomize between aiming for the left or right corner. In tennis, a server wants to randomize serving to the inside or outside. On fourth and goal in football, an offense wants to randomize between run and pass. In each case, the opponent also wants to randomize their planned responses. Any non-randomness can be exploited. The same holds in card games such as poker. A good poker player bluffs randomly. If she always bluffed, her opponents would learn her strategy and stay in the game. She would then lose every time she bluffed. Similarly, if she never bluffed, her opponents would learn to fold. Optimal bluffing makes her opponents uncertain whether to stay or fold.

In our second game, the Minimize Risk Game shown in figure 21.2 each player can take a risky action or a safe action. This is an asymmetric zero-sum game. The payoffs depend not just on the actions but also on which player takes which action. In this game, the row player has a dominant strategy to play safe. No matter what action the column player chooses, the row player earns a higher payoff by choosing safe. The column player does not have a dominant strategy. If the row player chooses risky, the column player should choose risky. If the row player chooses safe, the column player should choose safe.





Figure 21.2: The Minimize Risk Game

By thinking through the incentives for the row player, the column player can deduce that the row player will never choose risky because risky is dominated by safe. Therefore, the column player knows that the row player will choose safe. Given that, the column player should also choose safe. This type of reasoning in which one player rules out dominated strategies for the other player is known as iterative elimination of dominated strategies. In this game, using iterative elimination of dominated strategies shows that both players choosing safe is the unique Nash equilibrium.





Sequential Games


In a sequential game, players take actions in a specific order, as shown on a game tree, which consists of nodes and edges. Each node corresponds to a moment when a player must take an action. Each edge from that node denotes one of the possible actions. At the end branches of a game tree, we write the payoffs associated with following that path of actions. The game tree in figure 21.3 shows the Market Entry Game.





Figure 21.3: The Market Entry Game

The Market Entry Game involves two players: a potential entrant and an existing firm. If the entrant chooses not to enter the market (the left branch of the tree), it earns no payoff and the existing firm earns a profit of 5. If the entrant enters the market, the existing firm must choose between accepting the new entrant and seeing its profits fall from 5 to 2 or competing with the new firm and driving its profits to zero and the entrant’s profits negative. We assume the entrant’s profits to be negative because it has to pay for the cost of entering.

In a sequential game, a strategy corresponds to an action choice at each node. Suppose that the existing firm chooses to compete if the entrant enters. If the entrant knows this, the entrant would not enter, as doing so would produce negative profits. This set of actions, the entrant choosing to not enter and the existing firm planning to compete if the entrant did enter, are a Nash equilibrium. However, this is not the only Nash equilibrium, nor is it the most likely outcome. There is a second equilibrium in which the entrant chooses to enter the market and the existing firm accepts the entrants move and does not compete.

To select among these two equilibria, we apply a refinement criterion. In sequential games, a common refinement chooses the subgame perfect equilibrium. We solve for the subgame equilibrium using backward induction: we start at the end nodes and choose the optimal action at each. We then work backward up the game tree assuming that each player chooses the best action given the actions of the other player at subsequent nodes. In the Market Entry Game, we start at the end node for the existing firm. It has an optimal action: to accept. We then move up the game tree and see that the entrant has an optimal strategy to enter.

This game becomes even more interesting when replicated. Imagine that the firm exists in many markets. Perhaps it is a chain store with franchises in dozens of cities. Suppose also that there exists a sequence of potential entrants. The firm is going to play one Market Entry Game after another in sequence.

If the firm reasons using backward induction starting from the last market, it will accept the entrant in that last market, as that is the payoff maximizing action. Continuing with the same logic, the firm will accept the second-to-last entrant. It will also accept every other entrant. It follows that in the unique subgame perfect equilibrium of the sequence of games, all of the potential entrants choose to enter, and the firm accepts all of them.

Though entrance and acceptance in every market is the unique subgame perfect equilibrium. In practice, it may not occur. Imagine we are on the board of directors of the existing firm and we are confronting the first entrant, who (having studied game theory) enters the market. We may want to compete to try to deter entry in the other markets. Competing would be an intelligent strategy if it is credible, that is, if we can build a reputation as willing to compete. The outcome we hope to create differs from the subgame perfect equilibrium.

Game theorists refer to the disconnect in this game between what game theory predicts and what actual players would try to produce as the chain store paradox. It is one example where what game theory considers to be optimal behavior may not be the behavior chosen by a sophisticated player when the stakes are large. The example does not disprove game theory or undermine the rational choice assumption, so much as it reveals why we must always challenge assumptions.





Continuous Action Games


We now study a game in which players choose from a continuum of possible actions. In the game, actions correspond to effort levels. By choosing greater effort, a player increases her probability of winning a prize. This game allows us to model any number of players.

The derived expression for equilibrium effort reveals a number of insights. As we would expect, individual effort increases with the size of the prize. Also, in equilibrium, total effort will be less than the value of the prize. That too would be expected given that we assume players optimize. Players should put forth effort to win, but not an unreasonable amount.





The Effort Game


Each of N players chooses an effort level expressible in monetary terms to win a prize of value M. The probability that a player wins the prize equals her effort divided by the total effort of all players. If Ei equals the effort level of player i, her probability of winning is given by the following equation:1





Equilibrium:



We can see the effects on individual and total effort by increasing the number of players. Here, the findings are less intuitive. According to the model, individual players’ effort levels decrease but the total effort by all players increases. Thus, the model implies that efforts by organizers of research grant opportunities, architectural competitions, and essay contests to attract large numbers of entrants may, paradoxically, produce lower-quality winners because in the larger contests, participants have less incentive to put in effort.





Summary


We began this chapter by covering zero-sum games. These games assume no mutually beneficial combinations of actions. Any action that proves good for one player necessarily hurts another player. In a zero-sum decision, any action harms someone as much as it helps someone else. Taking money from one person and giving it to another is a zero-sum action. Many personal actions and policy choices are zero-sum in at least one dimension. We have only so many hours in the day, so much money to spend, and so many resources to allocate. That said, a zero-sum action in one dimension may not be zero-sum in another. A budget relocation could be zero-sum in monetary terms but positive or negative sum in terms of human happiness or fulfillment.

We should always explore whether a proposed policy change creates a zero sum game. For example, many people argue for school choice—giving parents the ability to choose the school their child will attend—because it increases competition. Market logic suggests that by being forced to compete, schools have incentives to improve quality.

However, schools only have an incentive to improve quality if excess capacity exists. Otherwise, school choice can create a zero-sum game among the students. Imagine a city with 10,000 students and 10 schools each with a capacity for 1,000 students. If the students rank the schools in the same order, spots in the best schools will have to be allocated by lottery. Those who win the lottery will go to better schools. Those who lose the lottery will go to worse schools, who remain in operation because of a lack of excess supply. Students are playing a zero-sum game. If new schools open, or if existing schools improve, the game is no longer zero-sum. Everyone can win.

Both the market and the zero-sum models provide insights. The market model reveals incentives for quality improvements and for the creation of new schools. The zero-sum model shows that school choice alone means that some students will gain while others lose. The relative weight we should place on each model depends on the context: Does sufficient excess capacity exist in the better schools so that they can absorb the additional students? Do schools have the resources and expertise to improve their quality? Will entrepreneurs create new schools? Does the transportation system enable students to get to multiple schools in order to create competition?

Our takeaway should be that neither of the two models gives us a correct answer, but each produces useful insights. School choice will create competition. It also creates a massive sorting problem with features of a zero-sum game. Whether the positive aspects of competition will outweigh the negative sorting costs depends on the context. We must array our lattice of models on the set of facts to make a good policy choice.





The Identification Problem


Data on people’s actions often reveals clustered behavior. Good students are more likely to be friends with other good students than with students who struggle. People who engage in criminal behavior are more likely to interact with other people who commit crimes than are people who do not commit crimes. Any number of social goods and ills—smoking, physical fitness, obesity, and even happiness—cluster in social networks. People also cluster by beliefs: Democrats cluster. Republicans cluster. Libertarians cluster.

We have two models that can explain clustering: peer effect models and sorting models. Peer effect models explain clustering with game theory. Individuals play a coordination game with their friends. In sorting models, people move to be near others who are like them. A cluster of good students could result from either students coordinating on a common behavior (peer effects) or arise because good students choose to hang out with one another (sorting). Given a snapshot of data, the two are indistinguishable.

Data: Students earn either high H or moderate M scores, with each being equally likely. Students belong to friendship cliques of size 4 with the following distribution: p({H, H, H, H}) = P({M, M, M, M}) = , p({H, H, H, M}) = P({M, M, M, H}) = , and p({H, H, M, M}) = 0.

Peer effect model: Students originally form random groups of size 4: p({H, H, H, H}) = P({M, M, M, M}) = , p({H, H, H, M}) = P({M, M, M, H}) = , and p({H, H, M, M}) = People who belong to groups consisting of only one type remain unchanged. A person who has the opposite type from everyone else switches type, so an {H, H, H, M} group becomes {H, H, H, H}. In groups with equal numbers of each type, one member switches type. The group {H, H, M, M} is equally likely to become {H, H, H, M} or {M, M, M, H}.

Sorting model: Students originally form random groups of size 4. In any group with two types, a person who has the opposite type as at least two other people switches groups with someone of the other type. It follows that {H, H, H, M} becomes {H, H, H, H} and {M, M, M, H} becomes {M, M, M, M}, and that any group of the form {H, H, M, M} is equally likely to become {H, H, H, M} or {M, M, M, H}.

Both models are consistent with the data, creating an identification problem. With only a snapshot of data, we cannot determine whether smoking, reading manga, or longboard skateboarding are peer effects or sorting. In some instances, we can reason through which model applies. The tendency for people to say “pop” in the Midwest and “soda” on the coasts is something that we can safely assume to be driven by peer effects—few people move to Boston so that they can refer to Coke as “soda.” On more important behaviors such as educational performance, drug use, obesity, and happiness, we need time series data to discern which model applies. By looking across time, we can discern if people change their behaviors to fit in with their friends (peer effect), or if they change their friends and retain their behaviors (sorting). In many cases of interest such as school performance, both effects may be in play.2


