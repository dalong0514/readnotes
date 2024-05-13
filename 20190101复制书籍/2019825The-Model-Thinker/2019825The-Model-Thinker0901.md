# 
> 2018000模板






9. Models of Value and Power





Your value will be not what you know; it will be what you share.

—Ginni Rometty



In this chapter, we cover models that quantify the value and power of individual actors. Some cases are easy. When a group produces output equal to the sum of individual contributions, each individual’s value equals her contribution. When the collective output cannot be separated into individual components, such as when a team of computer programmers writes a software program or a group of entrepreneurs proposes creative uses for a new technology, assigning credit becomes difficult. Assigning power to political parties creates similar problems; the number of seats a party controls correlates with power, but not perfectly.

In this chapter, we define two measures of value and power: last-on-the-bus value, which equals an actor’s marginal contribution given that the group has already formed, and Shapley value, which equals an actor’s average marginal contribution across all possible sequences of adding people to a group. In a group of three people, we average a person’s added value when she joins the group first, second, and third. We define these measures within the structure of cooperative game models, which consist of a set of players along with a value function that assigns a collective payoff to every possible subset of the players.

The chapter consists of four parts. In the first part, we define cooperative game models, last-on-the-bus value, and Shapley value, and work through some examples. In the second part, we describe axiomatic foundations for the Shapley value. We show it to be the unique measure satisfying four conditions. One condition is that a player who never adds value must be assigned value zero. A second condition is that the sum of the player’s values must equal the total value of the game. In the third part, we apply Shapley value to a group performing a creative task. Each person thinks up ideas. We show how in this context, the measure produces an intuitive measure of value. In the fourth part, we consider the special case of applying the Shapley value to voting games. We use it to distinguish between voting power and vote percentage. We find that they need not always agree. A party might hold 20% of the seats and have no power in one case and a third of the total power in another.





Cooperative Games


A cooperative game consists of a set of players and a value function that assigns a value to every possible subset, often called a coalition, of players. Cooperative games are meant to capture collective work and joint projects. In the model, we assume that people participate so that we can focus attention on how to assign value to their participation.





Cooperative Games


A cooperative game consists of a set of N players and a value function that assigns a value to any subset S ⊆ N, V(S). These subsets are called coalitions. The value of the coalition consisting of no players equals zero, = 0; the value of all N players, V(N), equals the total value of the game.



In a cooperative game, a player’s last-on-the-bus (LOTB) value equals the value she adds if she is the last to join the group. LOTB values capture players’ values at the margin. If four people are hired to move a table, and moving the table produces a value of 10, and all four are needed, then each has a LOTB value of 10. If only three are required, then each has a LOTB value of zero. Notice that LOTB values need not sum to the total value of the game. In particular, if the value function exhibits diminishing returns to scale, then LOTB values sum to less than the total value, and if added values exhibit increasing returns to scale, then the sum of LOTB values exceeds the total value.

A player’s Shapley value equals her marginal contribution when she is added to a coalition averaged across all possible orderings in which the coalition of everyone forms. In other words, we imagine adding the players to the coalition in sequence and calculating a player’s added value for each sequence. Consider a small firm that operates in Spain and France and requires one French speaker and one Spanish speaker to conduct daily business. The firm has three employees: a Spanish speaker, a French speaker, and a bilingual person capable of speaking both French and Spanish.

Suppose that our cooperative game assigns a value of $1,200 to any set of workers capable of speaking French and Spanish. This amount equals the daily revenue of the firm if it is able to operate. If any two employees show up at the office, the third is not needed. Therefore, each player has an LOTB value of zero.

To compute the Shapley value for the French speaker, we consider all six orderings in which people could arrive to work. In only one of these orderings, the one in which the Spanish speaker arrives first and the French speaker arrives second, does the French speaker add value. Her Shapley value equals times $1,200, or $200. The Spanish speaker adds value only if he arrives second and the French speaker arrives first, so his Shapley value also equals $200. In the other four orderings, the bilingual person arrives either first or second and adds value. Her Shapley value therefore equals $800. The sum of the Shapley values equals $1,200, the total value of the game.





Shapley Value


Given a cooperative game {N, V}, the Shapley value is defined as follows: let O represent all N! orderings in which the N players could arrive and be added to a group. For each ordering in O, define the added value of player i to be the change in the value function that occurs when player i is added. Player i’s Shapley value equals the average of her added values over all orderings in O.



Now that we have the idea, we construct a more complicated example. Imagine a crew team that requires four rowers and a coxswain—a smaller person who manages the stroke rate and steers. Our crew team (the players in the cooperative game) consists of six individuals: five tall, powerful rowers and a smaller person who has been trained as a coxswain. To enter a race, the team needs four rowers and a coxswain. A team of five that includes the smaller, trained coxswain will be competitive and has value 10. A team of five rowers without the coxswain could enter a race, but would perform poorly because of the extra weight. We assign that team of five a value of 2.

To compute Shapley values, we imagine the players arriving in every possible order. If the smaller coxswain arrives first, second, third, or fourth, she adds no value. If she arrives fifth, which occurs one-sixth of the time, she adds value 10. If she arrives sixth, she replaces one of the rowers as coxswain and her added value equals 8. Averaging across all of these possibilities, we find the coxswain’s Shapley value equals 3.

Each rower adds value if and only if she arrives fifth, which occurs one-sixth of the time. If the coxswain has not arrived, the rower who arrives fifth adds value 2. If the coxswain has arrived, the rower adds value 10. Given the one-in-five chance the coxswain is last among the five other players, and the four-in-five chance the coxswain arrives among the first four, we arrive at a Shapley value of for each rower.1 Intuitively, the coxswain’s value should be more than the value of a single rower and, given that the rowers can compete, albeit poorly, without the coxswain, less than the combined value of all of the rowers. There are an infinite number of ways to assign values that satisfy those constraints. Shapley values assign specific values: 3 for the coxswain and 7 total for the five rowers.





Axiomatic Basis for the Shapley Value


We now describe a set of axioms that Shapley values uniquely satisfy. That result explains why we might privilege Shapley values over other possible measures. First, note that we calculate Shapley values by averaging a player’s marginal contribution across all possible orderings, so any player who never adds value has a Shapley value of zero. Moreover, any two identical players—that is, two players who, for each coalition, contribute the same amount—must be assigned the same Shapley value. And given that the sum of the added values equals the total value of the game for any ordering, Shapley values must also sum to the value of the game. These will be three of the four axioms. Notice that LOTB values satisfy the first two axioms but not the third.

To these three properties, we add a fourth, additivity, which requires that if the value function of a cooperative game can be decomposed into two value functions, each assigned to a different cooperative game, a person’s value in the combined game should equal the sum of her values in the two constituent games. A moment’s reflection reveals that Shapley value satisfies this property as well. That those four properties uniquely characterize the Shapley value is less obvious.

Showing that a measure uniquely satisfies a set of axioms places the measure on logical foundations. Without the axioms, a measure may be intuitive but could be seen as arbitrary, as one of several plausible measures. The theorem also tells us that if we choose any other measure, we must abandon one of the axioms. This does not mean that Shapley value is the only reasonable measure. Lloyd Shapley, an economist and mathematician, may have first written down the measure and only after the fact constructed axioms that it uniquely satisfies. Which came first is of little relevance. Even if the axioms had been backward-engineered, if we accept the axioms, we should embrace the measure. The appropriateness of the measure hinges on the reasonableness of the axioms. In this case, the first three are difficult to dispute. The fourth, additivity, though more complicated than the others, can be supported on the grounds that if it did not hold, players would have incentives to split up or form coalitions.





Shapley Value: Axiomatic Basis


The Shapley value uniquely satisfies the following axioms:

Zero property: If a player’s added value equals zero for any coalition, the player’s value equals zero.

Fairness/Symmetry: If two players have the same added value for any coalition, then those players have the same value.

Full allocation: The sum of the values of the players equals the total value of the game, V(N).

Additivity: Given two games defined over the same set of players with the value functions V and , the value of a player in the game (V + ) equals the sum of that player’s values in V and .





Shapley Values and the Alternative Uses Test


We now apply Shapley values to a cooperative game based on the alternative uses test. In the test, each person must come up with novel uses of a common object, such as a brick. The test measures a person’s creativity based on the number of uses or categories of uses that she generates. When we calculate Shapley values, we find that they produce an intuitive scoring rule.

Imagine three players, Arun, Betty, and Carlos, who each think up alternative uses for blockchain, a distributed ledger technology, shown in figure 9.1. Arun and Carlos each think of six ideas, giving each a creativity score of 6, and Betty thinks of seven, making her score 7. The group’s total creativity equals 9, as there are nine unique ideas. To compute the Shapley values, we could write down all six possible orders in which the group could form, give individuals credit only for unique ideas added to the group, and then average over all six cases. Or we can notice that when we are computing Shapley values, the probability of someone getting credit for an idea equals 1 divided by the number of people who propose the idea. Anyone who proposes a unique idea always receives full credit. In the figure, we denote those ideas, such as Arun’s idea of art transactions, in bold font. If two people think of an idea, each has a one-in-two chance of joining the group first. Similarly, if all three people think of an idea, each has a one-in-three chance of joining first. It follows that allocating credit equally among people who thought of an idea produces Shapley values. Thus, it is the unique way to assign values that satisfies the four axioms. These values show that Arun, though he did not have the most ideas, adds the most value.2





Figure 9.1: Shapley Values and the Alternative Uses Test





The Shapley-Shubik Index


We next apply Shapley values to a class of voting games. In a voting game, each player (representing a political party or official) controls a fixed number of seats or votes, and a majority of those seats or votes are necessary for taking an action. In voting games, the Shapley value is referred to as the Shapley-Shubik index of power.3 By calculating the index, we find there does not exist a direct translation between the percentage of seats (votes) a party controls and its power.

To compute power indices, we consider all possible orderings of parties being added to a coalition. If a party joins the coalition and creates a strict majority, the party’s added value equals 1. In those cases, the party is said to be pivotal. Otherwise, the party adds no value. Consider a parliament with 101 seats allocated across four political parties as follows: party A controls 40 seats, party B controls 39 seats, and parties C and D each control 11 seats. In this example, party A cannot be pivotal if it arrives first or last. If party A arrives second or third, it is always pivotal. Therefore, it has a power index of . If party B arrives first or last, it also adds no value. If B arrives second, it is pivotal only if party A arrived first. If party B arrives third, the only way that it can be pivotal is if party A arrives last. Each of those combinations of events also occurs with probability . Therefore, party B’s power index equals . Parties C and D are pivotal in a similar set of cases as party B. Neither can be pivotal if it arrives first. Each is pivotal if it arrives second only if party A arrived first. Each is also pivotal if it arrives third when party A arrives last. Thus, each of those parties also has a power index of .





Figure 9.2: The Disconnect Between Seats and Power

The example reveals a possible disconnect between the percentage of seats a party controls and its power. Parties A and B control almost identical numbers of seats, but A has three times the power of party B, which has no more power than party C or party D. Similar allocations of seats occur often in real-world parliamentary systems. As a result, parties with few seats can often control substantial power. Israel’s parliament, the Knesset, has 120 seats. In 2014, a coalition led by the Likud party had 43 seats. The opposition coalition had 59 seats (just shy of a majority), and an Orthodox coalition held eighteen seats. All three parties have the same Shapley-Shubik index. This does not mean that the small Orthodox parties have the same power in practice—all models are wrong. It does suggest that the Orthodox parties had more influence than would be anticipated from their seat count.

An even more stunning disconnect between seats and power occurred with the Nassau County Board of Supervisors in New York in the mid-1960s. At that time, the board consisted of six members, and each controlled votes proportional to the population of the districts she represented, as shown in figure 9.3. A majority vote required 58 or more of the 115 votes. Notice that any two of the three largest districts constituted a majority. It follows that the votes of the other three districts could never be pivotal. The other district representatives therefore had no power. The North Hempstead representative controlled 21 votes, more than 18% of the total yet could not influence a voting outcome.





Figure 9.3: Votes but No Power

The Shapley-Shubik index of power can be applied to any situation with unequal allocations of seats or votes, such as the European Union or the Electoral College. That does not mean that it is necessarily an appropriate measure in all cases. The fifty states can be arranged in 50! (3 × 1064) different orders. Given regional correlations in voter preferences, not all coalitions are possible. Mississippi may not be likely to form a coalition with New York. To make a more useful measure of power we would need to privilege some coalitions over others or rule out some coalitions altogether. Later in the book, we describe Myerson values, which allow us to do the latter, to rule out some coalitions.





Summary


An individual’s Shapley value corresponds to her average added contribution to coalitions as they form. It is a measure of added value. In voting games, Shapley value can also be interpreted as a measure of power. It may not always be the best measure of power. An individual’s LOTB value may be the better measure of power in situations where a group has already formed, as that measures how much each individual could extract through a threat to leave, assuming that threat is credible.

In those cases, the coalition wants to reduce LOTB values. Creating a coalition with a high value but low LOTB values can be accomplished by increasing the coalition size. Adding extras makes existing members expendable and drives their LOTB values to zero. We see this in practice. Employers hire excess workers to reduce worker power. Manufacturing firms rely on multiple competing suppliers of intermediate goods. Governments award contracts to keep multiple contractors in business.

The same intuition applies to the creation of coalitions in legislatures. Congressional lobbyists and party leaders want to pass legislation (an outcome of value) but restrict the power of individual representatives and senators.4 If a lobbyist makes contributions to the minimal number of representatives and senators necessary to win a vote, then each representative and senator has an enormous LOTB value. Any could switch his or her vote and flip the outcome of the bill. The lobbyist can reduce their LOTB values by buying a supermajority of representatives and senators. The same logic implies that a party that holds a slim majority may be difficult to lead. Every member has a large LOTB value. Within a strong majority, no representative or senator has much power.

If we broaden our perspective and contemplate power in the modern connected world, we find it useful to apply both LOTB values and Shapley values. The power of an individual, organization, corporation, government, or terrorist group depends partly on how much damage it could do by deviating from a cooperative regime (LOTB value). A sophisticated computer hacker, a person capable of destroying a substantial amount of wealth, has enormous power. This holds even though the hacker lacks the ability to add value.

In thinking about the value of corporations or other multinational organizations, Shapley value may be a better measure. In these cases, exit may not be a viable option. An energy company participates in an energy generation game, an energy distribution game, a real estate game, an environmental game, an employment game, and so on. The company’s total added value equals the sum of its added values across the various domains.

Thinking of power and value through the lens of cooperative game theory provides powerful, basic insights. It also points to where we should look next. In politics and business, not all coalitions are plausible. The model assumes that they are. A richer model would take into account the connectedness of the world. Consulting companies and financial firms buy software from tech companies. Tech companies and consulting companies invest and borrow through financial firms. And financial firms and tech companies hire consultants. Within those webs, each actor adds value and wields power. To calculate power in these settings requires models of networks, where we turn next.





