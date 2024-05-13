# 
> 2018000模板



24. Mechanism Design



Institutions are designed to alter human behavior. To remain effective over time, institutions need to adapt to changes in the environment or the society the institution is meant to regulate.

—Jenna Bednar



In this chapter, we show how to use models to design political and economic institutions. An institution consists of a means through which people communicate information as well as a procedure for making decisions, reallocating resources, or producing outputs based on the information revealed. In markets, people and firms communicate through prices to execute trades and make production decisions. In hierarchies, people communicate through written language to organize work plans. And in democracies, people communicate preferences through votes. Voting rules then decide policies. Well-designed institutions induce communications and actions that produce desirable outcomes. Ineffective institutions do not.

In this chapter, we present a framework for modeling institutions known as mechanism design. This framework highlights four aspects of real institutions: information, what the participants know and should be revealed to them; incentives, the benefits and costs of taking particular actions; aggregation, how the individual actions translate into collective outcomes; and computational costs, the cognitive demand placed on participants.

The origins of mechanism design lie in the analysis of general questions about the allocation of goods, and in particular whether market mechanisms or central planning best allocates goods. Early models posited behavioral rules such as price-taking in a market or voting truthfully. The modeler then worked through the implications of those behaviors, for example, how they aggregated. That approach was abandoned in favor of one that assumed optimizing behavior, making the constructions amenable to game theoretic reasoning. Mechanism designers then solve for Nash equilibria and compare institutions based on rational behavior.

The framework has proved useful. It can be used to find flaws in existing rules and procedures, to explain why institutions succeed or fail, and to predict outcomes. It has also been used to design a variety of institutions, including the spectrum auctions described in Chapter 2, as well as many online markets, governmental voting systems, and even the procedures that allocate space for projects on space shuttle voyages.1

Our treatment consists of six parts. We first describe the mechanism design framework using the Mount-Reiter diagram. In the second part, we study the problem of three people choosing between two alternatives. In the third part, we analyze three auction mechanisms and find that all yield identical results. In the fourth part, we show that this was not a coincidence and describe a foundational result, the revenue equivalence theorem, which shows that any auction mechanism that satisfies certain assumptions produces the same outcome. In the fifth part, we compare a majority rule voting mechanism with a pivot mechanism as ways to decide on whether to undertake a public project. We conclude by broadening our discussion of mechanisms along the lines introduced in our criticism of Nash equilibria.





The Mount-Reiter Diagram


A mechanism consists of six parts: an environment (the relevant features of the world), a set of outcomes, a set of actions (called the message space), a behavioral rule that people follow to produce actions, an outcome function that maps the actions into outcomes, and a social choice correspondence that maps the environment into a set of hoped-for outcomes. The social choice correspondence commonly consists of either the outcome that maximizes the sum of the participants’ utilities or of the set of Pareto efficient allocations. An outcome is Pareto efficient if and only if no other outcome exists that everyone prefers. Pareto efficiency is a low bar.





Pareto Efficiency


Within a set of outcomes, an outcome is Pareto dominated if there exists an alternative that everyone prefers. All other outcomes are Pareto efficient.2



The Mount-Reiter diagram captures these essential parts of a mechanism graphically (figure 24.1). The diagram juxtaposes what we desire and what exists. Across the top, the social choice correspondence describes the outcomes that we normatively desire. Along the bottom, we have the mangle of reality. People apply their behavioral rules to send messages or take actions. An outcome function maps those actions into outcomes. Ideally, the lower, more complicated path on the bottom produces the same outcome as the top path, that is, the desired outcome.





Figure 24.1: The Mount-Reiter Diagram

Not all mechanisms succeed. For example, if the environment consisted of people with preferences for a public good, the social choice correspondence maps their preferences to the optimal level of that good. However, as we saw in Chapter 23, a voluntary contribution mechanism, in which people pay for as much of the public good as they desire, results in each person providing units of the public good rather than the optimal N units. When the outcome produced by the mechanism does not align with our objective, we say the mechanism fails to implement the social choice correspondence.

The list of properties that we would like a mechanism to satisfy varies by context. We describe five here. First, we would like the equilibrium outcome of the mechanism to agree with our social choice correspondence (Pareto efficiency). Second, ideally participants would apply dominant strategies, that is, their best actions would not depend on the actions of others. If so, we say that the efficient outcome is dominant strategy implementable. Third, we would not want to have to force people to participate in the mechanism (voluntary participation). Fourth, if the mechanism involves a transfer or payment of resources, we do not want to have to put in additional money or destroy resources (budget balance). Later in the chapter when we analyze mechanisms for deciding on a public project, we see that this may be difficult to satisfy. Last, in many cases, we desire truth-telling. We would like the messages that people send to reveal their true information or their true type. Game theorists call this incentive compatibility. In most cases of interest, no mechanism can satisfy all of these desiderata. Thus, one contribution of mechanism design has been in demonstrating what is possible and what is not.





Majority Rule and the Kingmaker Mechanism


The first class of environments that we consider consists of people voting on a joint action or piece of legislation. We consider three people, whom we call Uma, Vera, and Will, who want to see a movie together and must decide between an action movie, a drama, and a comedy. The same environment would apply to three members of the military deciding whether to attack their opponent, defend their position, or cede the land. In either interpretation, the environment consists of three people with preferences defined over three alternatives. We write preferences using orderings. The ordering action comedy drama corresponds to the action movie being most preferred, followed by the comedy and then the drama. We assume the following preference orderings:

Uma: action comedy drama

Vera: comedy drama action

Will: comedy drama action


In this example, we take the social choice correspondence to be the set of Pareto efficient choices. Given the assumed preferences, the comedy and the action movie are Pareto efficient. The drama is Pareto dominated by the comedy.

We first evaluate majority rule as a mechanism. In the case of a tie, we assume the choice is made randomly. If people vote sincerely, the comedy receives two votes. However, suppose that Vera and Will both believe that the other two people will be split between the drama and the action movie and each votes for the drama. Suppose also that voting is sequential. Vera votes first and selects the drama. Will votes second and does the same. Uma’s vote no longer matters, but suppose that to avoid conflict, she also votes for the drama. The three votes constitute a Nash equilibrium. No person has any incentive to change his or her vote. In this case, majority rule does not always implement a Pareto efficient outcome.

We next consider the kingmaker mechanism.3 In this mechanism, one person is randomly selected to be the kingmaker. The kingmaker then selects a “king,” who determines the group’s choice. If Will is the kingmaker, he must pick between Uma and Vera. Whomever he chooses becomes king, and that person then selects the movie.

If the person selected as king acts rationally, she will select her favorite movie. Therefore, the outcome will be Pareto efficient. For this reason, the kingmaker mechanism implements Pareto efficient outcomes. The mechanism has the added advantage that if any two people have the same favorite movie, the mechanism selects that outcome. To see the logic, once again, assume that Will is the kingmaker. If Uma and Vera prefer the same movie, then that movie will be selected regardless of Will’s choice of king. If, on the other hand, Will and Uma prefer the same movie, then Will should pick Uma.





Three Auctions


Now that we have a basic understanding of mechanisms, we turn to the study of auctions. Most of us have some familiarity with auctions owing to the prevalence of online marketplaces like eBay. Auctions are used in other settings as well, including government contracts, used car markets, and most web advertising. We restrict attention here to a single seller and many bidders. The object could be a house, a car, tickets to a soccer game, or a piece of art. We also assume that each bidder assigns a unique value to the object to rule out ties. The Pareto efficient outcomes are those in which the object goes to the bidder with the highest value. Any other outcome will be Pareto dominated by that outcome. We now compare three types of auctions: ascending-bid, first-price, and second-price auctions.





Ascending-Bid Auctions


In an ascending-bid auction, the auctioneer calls out a price. Any bidder willing to pay that price raises her hand. The auctioneer raises the price until only one bidder remains. That bidder then pays the price at which the second-to-last bidder lowered her hand. In an ascending-bid auction, a rational bidder remains in the auction until the price reaches her value. Dropping out before the price reaches her value creates the possibility of not winning the object at a price at a good price. Remaining in the auction after the price exceeds the bidder’s value means the bidder could win the object but pay more than her value, resulting in a net loss.

If all of the bidders act rationally, then the bidder with the highest value wins the object and pays a price equal to the second-highest bidder’s value. As an example, suppose that there exist three bidders with values $30, $60, and $80. When the price called out by the auctioneer exceeds $30, the first bidder exits the auction. When the price gets to $60, the second bidder exits. Therefore, the third bidder wins the auction and pays $60.4

In a second-price auction, each bidder submits a sealed bid. None of the other bidders see the amount. The object goes to the bidder who bids the largest amount. However, the bidder only pays an amount equal to the second-highest bid. The construction of the second-price auction makes telling the truth optimal. Imagine a bidder who values an object at $80 deciding how to bid in a second-price auction. We can assume that the other bidders have already submitted their bids. The bidder must consider three possible cases: the highest other bid could be less than $80, equal to $80, or more than $80. In each case, the bidder does best by reporting her true value for the object.

The logic becomes clearer when we work through an example. We will assume that the bidder’s value for the object is $80. We consider four cases for the highest submitted bids of the others: $70 (lower), $80 (equal), $85 (just above), or $90 (higher). Table 24.1 shows payoffs for five bid values ranging from $65 to $95.





Table 24.1: Net Payoff as a Function of Various Bids Given a Value of 80

As can be seen from the table, bidding 80 always gives at least as high a payoff as any other bid. Bidding her true value is always a best action (a dominant strategy). The same logic applies to all bidders, so all should bid their true values (the mechanism is incentive compatible). It follows that in a second-price auction, the bidder with the highest value wins the auction, and the amount paid equals the second-highest bidder’s value.

In a first-price auction, each participant submits a bid, and the highest bid wins, with the bidder paying an amount equal to that bid. As in a second-price auction, the bids are submitted simultaneously, so no one knows the others’ bids. A participant’s optimal bidding strategy in a first-price auction depends on the participant’s belief about the values (and therefore the likely bids) of the other bidders. We will assume that bidders do not know other bidders’ values but that they do have correct beliefs about the distribution over those values. To be specific, we assume that the bidders’ values are uniformly distributed between zero and $100 and that all of the bidders know this distribution. Bidders also know that all of the other bidders know this information as well.

Using calculus, we can show that if the values of bids are uniformly distributed and if all bidders bid optimally, then with two bidders each should bid half her true value, and with N bidders, each bidder should bid N−1

N of her value. A person in an auction with nineteen other people should therefore bid 95% of her true value. Given this bidding rule, the bidder with the highest value always wins the object. We can also show that the amount she pays equals the expected value of the second-highest bidder. Thus, the ascending-bid auction also produces an efficient outcome and the price corresponds to the expected value of the second-highest bidder.5

Prior to writing down the model, many of us would have had the insight that the more bidders in the auction, the more a person should bid. Without the math, we would not have known the equilibrium bidding rule. The model gives us an exact expression for how much a person should bid. The amount increases in the bidder’s value, which implies that the bidder with the highest value will win the auction, just as in the other two auction formats.





Revenue Equivalence Theorem


In each of the three auction formats, the bidder with the highest value wins. Therefore, all three mechanisms produce an efficient outcome. In addition, the expected amount paid by the winning bidder equals the value of the second-highest bidder. In other words, all three auctions produce the same expected revenue and allocate the object to the same person. That is remarkable. Even more remarkable, it can be shown that the winner and expected revenue are the same for any auction in which bidders act optimally, the highest bid wins the object, and a bidder with a value of zero receives no payoff. In other words, all auctions that satisfy those two conditions produce the same expected outcome, a result known as the revenue equivalence theorem.6





Revenue Equivalence Theorem


Any auction in which the bidders have independent private values drawn from a known, common distribution produces the same revenue to the seller and the same expected payoffs to the buyers if each bidder makes a bid that maximizes her expected payoff, the bidder with the highest bid always wins the object, and a bidder who has a value of zero has an expected payoff of zero.



The revenue equivalence theorem implies that an all-pay auction—in which every bidder, even the losing bidders, pays the amount of her bid—produces the same outcome as the second-price auction.7 Even a crazy design such as a third-price auction, where the highest bid wins and pays an amount equal to the third-highest bid, produces the same winner and same revenue. The revenue equivalence theorem does not imply that the auction rules do not matter. In an actual auction, bidders may not use optimal strategies, or, in a first-price auction, bidders may have different beliefs about the value distributions of other bidders. If either condition holds—non-optimizing bidders or diverse beliefs—then revenue could vary across the types of auctions. Empirical and experimental tests do show some differences in how auctions perform.

As would be expected from our discussion of when to expect rationality, the higher the stakes and the more sophisticated the bidders, the more likely it is that people act rationally. In online auctions for consumer goods, we might expect some people to follow rules of thumb or suffer from biases (such as bidding in increments of $10). In a multimillion-dollar oil lease auction, bidders probably have access to full information and the requisite skills.

Also, the type of auction could influence the number of bidders. In timber auctions, first-price auctions attract more small bidders than do ascending-bid auctions because small bidders have some chance of winning if the bigger bidders submit low bids. The small bidders have no chance in an ascending-bid auction, as the bigger firms can see the smaller firms’ bids and outbid them.8

Auctions also differ in the cognitive demands they place on participants. In some auctions, optimal behavior is easy to learn. In an ascending-bid auction, a bidder should remain in the auction until the price reaches her value. Other bidders not following optimal strategies could cause a bidder to have a higher or lower expected payoff, but they do not change the optimal strategy: a bidder should stay in as long as the price is less than her value. Similarly, in a second-price auction, a bidder should always follow the same strategy of bidding her true value. However, figuring out that truthful bidding is optimal requires multiple steps of logic.

Recall that dominant strategies are optimal regardless of the strategies of others. Both ascending-bid and second-price auctions have dominant strategies. First-price auctions do not. In a first-price auction, changes in the bidding strategy of one bidder can change the optimal strategy for another bidder. If one bidder always bids either zero or 50, then the other bidder should always bid either 1 or 51. There would be no reason to bid 60 or 70 as the winner would pay more for the object than necessary. Given the behavior of the other bidder, whenever a bid of 60 wins the auction, so does a bid of 51.

Even if an auction has a dominant strategy, not all dominant strategies are equally easy to deduce. In an ascending-bid auction, the strategy of staying in as long as the price is less than a bidder’s value requires a single step of reasoning: if the price is less than your value, buy it at this price. In the second-price auction, a bidder has to think through multiple contingencies to see that truthful revelation is optimal. Of course, once someone bids in several second-price auctions, she should learn that the optimal bid is to tell the truth.

A last feature to consider is whether the auction encourages non-optimal behavior. In first- and second-price auctions, bidders submit their bids without knowing others’ bids. In an ascending-bid auction, bidders can see the price rise and are aware of who remains in the bidding. This could cause a bidder to attach some value to winning and to overbid. Auctioneers in charity auctions try to raise bids by emotional appeals, perhaps by showing a video of children frolicking on new playground equipment that your bids will support.

The success of strategies depends on the sophistication of the bidders. It is difficult to imagine bidders in a timber auction being persuaded to bid more than their forecasted valuations. It is less difficult to imagine a person at a charity auction overbidding in light of the cause. Whether or not bidders change their values during the bidding process is a matter of conjecture. We need only recognize that it could happen. In first- and second-price auctions, bidders make a single bid, which allows no opportunity for emotional appeals during the auction.

Finally, in the first-price auction and the ascending-bid auction, the price equals the highest bid. In the second-price auction, it equals the second-highest bid. This leaves the appearance that the seller could have received a higher price and, in part, explains why governments do not use second-price auctions. Imagine the headline if a government received three bids for oil rights, one at $6 million, one at $8 million, and one at $12 million: “Government Gets $12 Million Bid but Sells Land for $8 Million.” Anyone who knows auction theory would know that had the government run a first-price auction or an ascending-bid auction, then the top bid would not have been $12 million. It would have been $8 million.

As has been highlighted throughout the book, formal models reveal conditions necessary for a result to hold. The revenue equivalence theorem does not say that all auction mechanisms produce the same outcome. It states that all auctions with optimizing bidders in which the highest bidder wins the object and a bidder with zero value has an expected payoff of zero are equivalent. A seller could raise more money by relaxing one of those three assumptions. A seller would have difficulty making people act against their self-interest, and she would also probably not be able to extract money from someone who does not value the good. This leaves as the only possibility not selling the object to the highest bidder. One way to do this is to not sell the good at all. If the seller knows the distribution of values, she could set a reserve price, a minimum bid. Under some conditions, this can increase her expected revenue. Suppose that seller is certain that the three bidders for an object have values of 5, 10, and 60. Using any of the three auctions above, the winner bids $60 and pays $10. The seller could earn higher revenue by imposing a reserve price of $60 and running a first-price auction.





Mechanisms for Deciding on a Public Project


We next compare two mechanisms for deciding whether to build a public project such as a school, a new highway, or a sports arena. We assume each person has an individual value from the project and that the project has a collective cost.





A Public Project Decision Problem


Let (V1, V2,···, VN) denote the monetary values that N people attach to a public project with cost C. The project should be undertaken if and only if

C < V1 + V2 + ··· + VN



We first consider the majority-vote equal sharing mechanism. In this mechanism, individuals vote whether to undertake the project. If a majority vote yes, the cost of the project is divided equally among the population.





Majority-Vote Equal Sharing


Individuals vote for or against undertaking the project. If a majority vote for the project, the project is undertaken and each pays a cost . As the following example shows, this mechanism can violate efficiency and voluntary participation.



We know from the spatial voting model that whether or not the project is undertaken depends on the preferences of the median voter. In this case, that will be the person with the median value for the public project. By construction, the mechanism satisfies the budget balance condition and incentive compatibility. However, the mechanism need not satisfy either efficiency or voluntary participation as can be seen in an example. Suppose that there exist three people with values $0, $120, and $150 for a public project that costs $300. The efficient outcome is that the project should not be undertaken because the total cost of $300 exceeds the sum of the individual values. However, given that costs will be split equally, each person votes on whether to undertake the project at a cost of $100 each. It follows that two of the three individuals will vote for the project, and it will be undertaken, the inefficient outcome. Moreover, the individual with value $0 receives a payoff of -$100, so the example also violates voluntary participation.

In our second mechanism, the pivot mechanism, each individual submits a valuation for the project. If the sum of the valuations exceeds the cost of the project, the project is undertaken. Otherwise it is not. The amount that the individual will be taxed equals the cost of the project minus the sum of all of the other individuals’ valuations. If the valuations of the other individuals exceed the cost of the project, the individual pays nothing.





The Pivot Mechanism


Individual i submits a valuation for a project of cost C. If the sum of the individual valuations exceeds the cost, then the project is undertaken.





Individual i pays no tax if and otherwise. The mechanism is incentive compatible (), efficient, and individually rational. It also implements the efficient outcome in dominant strategies. As the following example shows, this mechanism can violate budget balance:

Example: (V1, V2, V3) = (60, 120, 150) and C = 300.

The project should be undertaken given that 300 < 60 + 120 + 150. Individual 1 pays taxes of 30, the cost minus the sum of the other valuations (300 − 270); individual 2 pays taxes of 90; and individual 3 pays taxes of 120. The total taxes generated the sum of 240, less than the cost of the project.



This mechanism satisfies incentive compatibility by a logic similar to that of a second-price auction. Suppose that the project has a cost of $300 and that an individual values the project at $80. There are three cases to consider. If the other valuations sum to less than $220, the individual has no incentive to submit a value more than $80, as he would have to pay that amount. If, at the other extreme, the sum of the others’ valuations exceeds $300, then he pays nothing, and he could submit any valuation. If, though, the sum of the valuations of the others lies between $220 and $300, then if the individual submits a valuation of $80, he will pay $300 minus that sum and the project will be undertaken (the efficient outcome). He would not want to submit a valuation of, say, $70 because the sum of the other values could be $225 and his low valuation would prevent the project from being undertaken. Had he submitted a valuation of $80, it would have been undertaken at a cost to him of only $75.

Given that the pivot mechanism satisfies incentive compatibility, it follows that it also satisfies efficiency. The project is undertaken only if the sum of the valuations exceeds the cost. Note that because reporting one’s true value is a dominant strategy, the efficient outcome is also dominant-strategy implementable. Also, because each individual pays at most her value for the project, the mechanism satisfies voluntary participation. However, as shown in the box below, the mechanism need not produce a balanced budget. In fact, only in rare cases will it do so.

For the problem of deciding on a public project, no mechanism will satisfy every criterion we might desire. The fact that we can use models to prove that can save us a lot of time trying to do the impossible. Just as engineers do not waste time trying to build perpetual motion machines, mechanism designers do not seek incentive-compatible, individually rational, efficient, budget-balanced mechanisms for the public project problem. No such mechanism exists.

The pivot mechanism is about as good as we have, but it fails to satisfy budget balance. That problem cannot be fixed by raising the amount of taxes that people pay for the project, as that would make the mechanism no longer either incentive compatible or individually rational. Individuals would have an incentive to lie, and some might be asked to contribute more than their value for the project. One possible workaround is to raise taxes in some other way and to have a pool of money available for projects. That would itself create incentive issues, though not as directly. A better solution is to have some other source of money. For example, a university that both has a large central endowment and consists of colleges that have separate endowments could use this mechanism to decide whether to construct a new student union. Each college dean would have an incentive to truthfully reveal her value for the union and the university chancellor could make up for any shortfall. A business composed of subunits that have budget authority could do the same. A project to switch to a cloud-based system could be decided upon with the pivot mechanism, and any shortcoming could be covered by upper management.





Summary


The mechanism design framework enables us to compare mechanisms across a variety of criteria. Does a mechanism produce efficient outcomes? Do people tell the truth? Would people voluntarily participate? Does the mechanism produce a surplus or loss? Using the mechanism design framework, we can also derive what is possible. It may not be possible to satisfy all of the desired criteria within the same mechanism. In these cases, modelers become engineers. We use models to try to construct workable solutions.

As technology changes, so too can our mechanisms. Take, for example, the auctions used by internet search sites such as Google. Originally, Google charged a fixed price per thousand clicks. That mechanism was not optimal given changes in information technology that allowed Google to run millions of auctions simultaneously. By using auctions, Google increased its revenue, and it allocated ad space more efficiently. Google now uses a generalized second-price auction. Each bidder submits a per-click bid to advertise for a keyword—say mesothelioma, a cancer caused by exposure to asbestos. The highest bidder receives the first ad slot, the second-highest bidder receives the second slot, and the third-highest bidder receives the third slot. The prices they pay are determined as in the second-price auction.

Suppose that the top four bids are $10, $7, $6, and $3 per click. The third-highest bidder will pay a price equal to the bid of the fourth-highest bidder, $3. The second-highest bidder will pay a price equal to the bid of the third-highest bidder, $6. And the highest bidder will pay $7.9 After learning the valuations of advertisers, Google could have set a reserve price and raised even more money. But that outcome would not necessarily hold if the bidders knew this was Google’s plan. A bidder who thinks he is likely to be the high bidder would not want Google to know his valuation. Placing reserve prices would also harm Google’s reputation. A reserve price would be seen as non-cooperative behavior because Google cannot claim to have a reserve value for spots on a webpage. The top advertising slot on a keyword search has little value to Google unless it is sold. That is not true for someone selling a collection of vintage albums or a used car. Those items have values to their sellers, so a reserve price is justified. However, Google values its reputation, and setting a reserve price to extract more revenue might anger advertisers.

To summarize, mechanism design models can aid in the design of and choice among institutions. With them, we can deduce what is possible and not possible to implement. It may not be possible to construct a mechanism that produces efficient outcomes, induces people to tell the truth, and results in a balanced budget. If so, we should not waste time and effort trying to design the impossible. Better that we devote our energies to thinking through how best to trade off efficiency, truthful revelation, and a balanced budget

We can also use mechanism design to explore bigger questions, such as when we should use a market, when we should vote, when we should rely on a hierarchical mechanism, and when we should turn to a voluntary collective to allocate a resource or decide on an action.10 Each of these four institutions—markets, democracies, hierarchies, and collectives—functions well in some settings and not so well in others. For example, we would not want to vote on what goods people buy, nor would we want to use a market to decide on our political leaders.

Within society writ large as well as within an organization, we see each of these institutional forms. A university confronts a market for professors, relies on a democracy to hire faculty, assigns course assignments through a hierarchy, and develops strategic plans using collectives. Nonprofits, for-profits, and government agencies are also a mashup of these various institutional forms. Using the tools of mechanism design, we can formally compare how each of these institutions functions, and in doing so, make better assignments of institutions to tasks.




