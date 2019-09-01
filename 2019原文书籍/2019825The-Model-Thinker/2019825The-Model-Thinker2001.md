# 
> 2018000模板




20. Spatial and Hedonic Choice Models





Our theory is, if you need the user to tell you what you’re selling, then you don’t know what you’re selling, and it’s probably not going to be a good experience.

—Marissa Mayer



In this chapter, we cover models of individual choice over alternatives represented by their attributes. These models were developed to capture consumer choices. A person buying a house takes into account its square footage, the number of bedrooms and bathrooms, and the quality of construction. These can also be applied to college deans of admissions or hiring directors as they select among applicants or to voters as they decide between candidates. An admissions dean considers an applicant’s SAT scores, grade point average, and extracurriculars. A voter evaluates candidates based on their positions on education, infrastructure, crime, and taxes. In addition to helping us understand individual choices, these models provide insights into why we have the choices we do—for example, why we have so many choices of breakfast cereals.

In the models we cover, we characterize some attributes as spatial and others as hedonic. A spatial attribute, such as the color of a jacket or the thickness of a slice of bread, has no best value. Each individual prefers a particular amount of the attribute: a consumer of baby back ribs has a preferred level of spiciness, and an amateur downhill skier has a preferred angle of descent on a slope. The model assumes that the closer a product’s attributes are to a person’s ideal point, the more the person values the product. These ideal points vary across people: one person may prefer spicier ribs than another.

On hedonic attributes, more (or in some cases less) is always better. People prefer longer battery life in a smartphone, more square footage in a house, more durability in the soles of shoes, and better gas mileage in their cars. Most product choices are hybrids—they contain both spatial hedonic attributes. A car’s color will be a spatial attribute. Its gas mileage is a hedonic attribute.

Throughout the chapter, we assume that people choose the alternative that they value the most. We do this for reasons mentioned in Chapter 4, on modeling human behavior: rational behavior provides a benchmark, is analytically tractable, makes a unique prediction, and fits empirically when the situation is repeated and the stakes are large.

Models of spatial and hedonic competition are widely used in economics and political science in part because they can be taken to data.1 In this chapter, we get a hint of their applicability. We begin with a spatial model of product competition. We then apply the model to politics and show how it can be used to analyze status quo effects, agenda power, and the influence of veto players. We then cover the hedonic attribute model and a hybrid model to reveal insights into price competition. Along the way, we show how to take data to the models to infer the positions of candidates and judges based on their votes on bills and legal cases and to infer implicit prices for unpriced attributes such as cleaner air or a shorter commute.2





The Spatial Competition Model


The spatial competition model assumes alternatives defined by a set of attributes and consumers defined by ideal points. The simplest version of the model considers products with a single attribute. In Hotelling’s original spatial model, that attribute was geographic location.3





Figure 20.1: Hotelling’s Geographic Model of Ice Cream Vendors on a Beach

Hotelling’s model assumes a collection of consumers spread along a beach, represented by circles in figure 20.1, along with two ice cream vendors, denoted by A and B. Each customer buys one ice cream from the nearer vendor. The cut point is an equal distance between the two vendors and determines who buys from whom. The seven consumers to the left of the cut point buy from vendor A, and the six consumers to the right of the cut point buy from vendor B.

Given the idea of consumers preferring closer goods, we can reinterpret distance more abstractly. For example, we could imagine the ice cream vendors being in the same location but offering different levels of butterfat in their ice cream. The same figure can represent vendor B offering a creamier product than A. In the reinterpretation, the consumers’ locations are not physical position on the beach but preferred levels of butterfat.

We can again apply one-to-many model thinking and use this same model to analyze political competition. The Downsian model reinvents Hotelling’s geographic space as an ideological continuum from left to right. We can reinterpret figure 20.1 as follows: vendor A represents a liberal political candidate, vendor B a more conservative candidate, and the circles represent the ideological ideal points of voters. To extend the analogy, we assume voters prefer nearer candidates.

The shift from geographic locations of firms and product attributes to political ideologies involves a transition from physical attributes such as location and butterfat level to the more abstract concept of ideology. While we have clear measures of physical attributes, assigning ideologies requires a method for translating the actions of candidates into numbers. If the candidates have voting records, we can assign ideologies by first gathering all of the votes the candidate has cast. We should ignore all votes that lack an ideological component—unanimous proclamations establishing National Milk Day and the like. On all other votes, we can rely on expert opinion to assign a liberal position and a conservative position. A candidate’s spatial location on the interval can be set equal to the percentage of the time she votes the conservative position.4 A candidate who always takes the conservative position is placed to the far right. A candidate who votes conservative half of the time and liberal half of the time is placed in the center.

With this model, we can adjudicate claims that American political parties have become more ideologically distinct by empirical tests. One analysis, shown in figure 20.2, reveals a marked and increasing polarization of the average ideal points in each party. This does not prove that polarization has increased, but it provides evidence. The analysis also reveals that the polarization is mostly due to a Republican shift to the right.





Figure 20.2: Increasing Ideological Polarization in Congress





Increasing the Number of Attributes


The general spatial competition model includes an arbitrary number of attributes. A couch can be represented by physical dimensions: length, width, and depth, type of construction, and type of upholstery. The value (or utility) that a consumer obtains from a product depends on the product’s distance to her ideal point across these same dimensions. We can write this value function as a constant term minus the distance between the alternative and her ideal point.5





Spatial Competition Model


An alternative consists of N spatial attributes: = (a1, a2,···, aN).

An individual is represented by an ideal point: = (x1, x2,···, xN).

The payoff (utility) to an individual from an alternative equals

π(, ) = C − (x1 − a1)2 − (x2 − a2)2 −…− (xN − aN)2

where C > is a constant.

Example: = (3, 4, 6), = (2, 1, 8), C = 20:

π(, ) = 20 − (3 − 2)2 − (4 − 1)2 − (6 − 8)2 = 6



In the general spatial competition model, two chocolate bars might be represented by the percentages of cocoa and amounts of sugar they contain, as shown in figure 20.3. The cut line will be the perpendicular bisector of the line connecting the two products. Consumers with ideal points to the left of the cut line prefer A, and consumers to the right prefer B.6





Figure 20.3: Product Attributes of Two Chocolate Bars and the Cut Line

The model can also accommodate any number of products. To add a third chocolate bar, we add another point in attribute space. To determine which bar consumers buy, we then draw additional cut lines, as shown in figure 20.4. The multiple cut lines carve up the space of ideal points into three regions, known as Voronoi neighborhoods, that partition the space of ideal points based on their distances to the products.





Figure 20.4: A Spatial Model with Three Products (Voronoi Neighborhoods)





The Downsian Model of Spatial Competition


We next apply the model to explain candidate positioning. To do so, we assume vote-seeking candidates, who place primary emphasis on winning elections. We begin with an example to think through the incentives of candidates. Figure 20.5 shows two scenarios with thirteen voters and two candidates. Recall that voters prefer the nearer candidate. In the top diagram, the liberal candidate, denoted by L, receives five votes, while the conservative candidate, denoted by R, receives eight votes. In the lower diagram, the liberal candidate moves to the center, attracts seven votes, and wins the election.





Figure 20.5: Party Moving to Center to Win Election

The liberal candidate has an incentive to move to the center. By the same logic, so does the conservative candidate. The conservative candidate could move to the left, though remaining right of L, and also win. Continuing with this reasoning, the liberal candidate, L, could take a position even closer to the median voter’s ideal point. If we continue to apply this logic, we see that candidates should converge on that point. This result is known as the median voter theorem.

The median voter theorem can be interpreted in strong or weak form. In strong form, it implies candidates adopt identical positions at the median voter’s ideal point. That clearly does not hold empirically. In weak form, it implies that candidates have an incentive to move toward moderate positions. Empirical evidence suggests that this does happen. During the course of an election, candidates move toward the center. That movement need not be a mad rush. Candidates who possess ideological convictions or benefit from core supporters at the extremes will reposition with caution.

This model reduces each candidate and each voter to a single ideological point, a strong assumption. Czech writer and politician Václav Havel takes exception to one-dimensional ideological projections: “To wandering humankind, it [ideology] offers an immediately available home: all one has to do is accept it, and suddenly everything becomes clear once more, life takes on new meaning, and all mysteries, unanswered questions, anxiety, and loneliness vanish. Of course, one pays dearly for this low-rent home: the price is abdication of one’s own reason, conscience, and responsibility, for an essential aspect of this ideology is the consignment of reason and conscience to a higher authority.7” Havel makes a good point. We should not abdicate reason for ideology. Models provide us with tools to reason better. This particular model helps us to understand why politicians act as they do. Using data, we can determine the confidence of each politician’s placement on the left-right interval. A politician who always takes a moderate position can be placed in the middle of the interval with high confidence.

Incidentally, Havel’s denial that he can be reduced to a point could be tested with data. If his criticism holds, if we cannot pin down his ideology based on votes, we need not abandon the model. We could represent the uncertainty over Havel’s ideology by assigning him an interval rather than a point. Or, we could construct a time series of his measured ideology to see if he remains consistent. Studies of the ideological positions of Supreme Court justices show that some justices become more liberal as they spend more time on the bench.8

Last, we could increase the dimensionality of the model. A two-dimensional model could distinguish between social policies and fiscal policies. The model can then capture a politician who advocates liberal positions on social policies and conservative positions on fiscal policies. For the United States Congress, one dimension explains approximately 83% of the variation in votes. Adding a second dimension adds only another 4%.9

In addition to allowing us to model preferences with greater accuracy, adding dimensions also changes our theoretical findings. We start with a two-dimensional model. From the one-dimensional model, we know that if a candidate is not located at the median on either issue, then the other candidate could win an election by matching the first candidate’s position on one issue (thus making that issue irrelevant) and taking the median position on the other issue. Similarly, if one candidate takes the median position on one issue but does not on the second issue, then the other candidate could take the median position on both issues and win the election. It follows that the only position that has the possibility of not being beatable is the two-dimensional median. Figure 20.6 shows how the two-dimensional median, represented by a circle, can be defeated. If the square candidate positions to the left on issue one and to the right on issue two, she produces a cut line in which she wins three votes.

Building intuition from this example, we see that the two-dimensional median will be unbeatable only if voter ideal points are arranged such that fewer than half lie in every direction from the median, a condition called radial symmetry. Radial symmetry would be satisfied if voters’ ideal points were uniformly distributed across a disc or a square, a very strong assumption. This result, that any position can be defeated, is known as Plott’s no-winner result. It holds in two or more dimensions.10





Figure 20.6: The Two-Dimensional Median Loses to a Challenger

The difference in results is stark. A one-dimensional model implies that candidates position at the median. Higher-dimensional models imply that they should not. Which type of model do we believe? We should place complete faith in neither model, but instead gain insights from both. The one-dimensional model reveals a powerful incentive for vote-seeking candidates to move toward moderate policies. The higher-dimensional models demonstrate the limits to those incentives. No position guarantees a win, so we should not expect an equilibrium. We should instead expect complexity, an endless dance of competition for votes through coalition building.11





Status Quo Effects, Agenda Control, and Veto Players


We can also apply the Downsian model as a lens for interpreting the ideological dimensions of bills passed by committees, councils, legislatures, and presidential systems. Here again, the key will be to map pieces of legislation onto the same single ideological dimension as committee members. We consider three strategic effects here: the influence of current policy (status quo effects), the power of agenda control, and the effect of adding veto players.

Throughout, we rely on an example involving a committee of three people with ideal points at 40, 60, and 80, in which the committee member with an ideal point at 40 gets to propose a policy that must be approved by a majority. Figure 20.7 shows the effect of the status quo on final policy. If the status quo is at 80, she needs legislation that the median voter, the committee member at 60, prefers to the status quo. In this case, the median voter would accept a proposal at 40, the proposer’s ideal point, as it is just as good as the status quo.12 If we move the status quo to 70, the median voter would reject a proposal of 40. The proposer has to offer a policy at 50. Finally, if the status quo sits at the median voter’s ideal point of 60, the proposer has no power. We can thus draw the following inference: the proposer has the most power when the status quo has an extreme value.





Figure 20.7: The Effect of the Status Quo on Final Policy

This insight applies in any context where people vote and opinions can be mapped to one dimension. The head of a nonprofit making a proposal to her board of directors to increase spending on affordable housing efforts has little agenda power if current spending levels align with the wishes of her median board member. She can have power if current policies do not align with that board member’s ideal.

To show the power of proposing, we consider the case where the status quo sits at 70, shown in figure 20.8. The top diagram shows the previous case, where the proposer has an ideal point at 40 and proposes a policy at 50. The middle diagram shows the case in which the median voter can propose his ideal point of 60 and also obtain the vote of the committee member at 40. The bottom panel shows the case where the proposer has an ideal point of 80. She cannot offer a policy that both she and the median voter prefer to the status quo, so she accepts the status quo.

This exercise reveals the limit of proposer power. Legislation may move in the direction of the ideal point of the person in power, but as we have learned, the extent of that power will be mitigated by the representativeness of the status quo.13

Last, we can use this same model to consider multiple levels of government and an increased number of veto players. Here, we interpret the three committee members as the median voters in the House and the Senate, and the President. For legislation to pass, each of these three must prefer it over the status quo. In this scenario, each has veto power. Refer again to figure 20.8, where the status quo sits at 70. If all three voters must approve any change, then no proposal can defeat the status quo. Any policy to the left of 70 will be vetoed by the voter at 80. Any policy to the right of 80 will be vetoed by both of the other voters.14 If all three voters can veto legislation, there will be no new legislation unless the status quo lies outside the interval from 40 to 80—that is, if the current status quo is to the left or right of anyone’s ideal point. The model reveals a tight link between the number and ideological diversity of veto players and the extent of gridlock. That insight holds more generally. Organizations with diverse veto players will be unable to take action.





Figure 20.8: The Effect of the Proposer on Final Policy





The Hedonic Competition Model


The hedonic model of competition also represents the alternatives (typically products) by attributes. However, in this model, the attributes consist of quality, efficiency, or price, in which more (or, in the case of price, less) of the attribute is always preferred. To capture heterogeneity, the model allows individuals to attach different weights to the dimensions.

Using linear regression, we can infer implicit values for the attributes of goods using the hedonic competition model (also known as the Lancaster model). The application is straightforward. The model assumes the payoff to be a linear function of the product’s attributes and the person’s weights. If we have data on the selling prices of thousands of homes as well as the relevant attributes of those homes (square footage, number of bedrooms and bathrooms, quality of local schools, size of yard, and quality of construction), a regression will produce the average weight (in dollars) of each attribute for those people who bought the houses. This is known as hedonic regression.





Hedonic Competition Model


An alternative consists of N valence attributes: = (v1, v2,…, vN).

Individual preferences are captured by weights = (w1, w2,…, wN) assigned to the attributes.

The payoff (utility) to an individual from an alternative equals

π(, ) = w1 · v1 + w2 · v2 + ··· + wN · vN

.

Example: = (3, 1, 2), = (4, 2, 5):

π(, ) = 4 · 3 + 2 · 1 + 5 · 2 = 24

.



Some of those attributes, such as a swimming pool or a new kitchen, have market prices. As a check on the model, we can compare the estimated prices to the market costs. If the regression shows that a swimming pool adds $150,000 to the price of a house and swimming pools cost $15,000, we know the model is missing attributes. If the regression shows the added value to be only $8,000, then this likely means that people do not recover the full costs of adding pools.

Other attributes, such as the commute time from the house to the city center, do not have market prices. In those cases, the regression produces an implicit price for that attribute, and that implicit price can be informative. The table below shows hypothetical price data for six houses.





If we assume the houses are identical on all other attributes and we run a hedonic regression, we obtain the following equation:

Price ($) = 100(Square Ft) + 20,000(# Bedrooms) − 2000(Commute Time)

The regression equation estimates that people value each additional square foot at $100, each bedroom at $20,000, and each minute saved commuting at $2,000 over the period of home ownership. A person who lives in a house for twenty years spends 4,000 to 5,000 days commuting. If we take the lower number, each extra minute of daily commute time results in 4,000 minutes, or over 60 hours, commuting. The $2,000 estimate equates to around $30 an hour. In other words, people pay for proximity “as if” they are paying themselves $30 an hour to sit in traffic.15





A Hybrid Model of Product Competition


The spatial and hedonic models differ in how they represent preferences over attributes. In the spatial model of competition, each person has a preferred level of each attribute, and his value for an alternative increases as it gets nearer his ideal point on those dimensions. In the hedonic model, people prefer either more or less of each attribute.

Many of the choices we model—over consumer goods and services, ideal life partners, public policies, religions, and job applicants—include both spatial and hedonic attributes. We may each have our own preferred level of crispiness for french fries, yet we all prefer to pay less per serving. Crispiness is spatial. Price is hedonic. Employers likely differ in the personality characteristics they look for in potential employees. Some firms prefer extroverts. Others may prefer introverts. All firms prefer more honesty and integrity. Thus, personality type is a spatial attribute, while honesty is a hedonic attribute.

We can thus create a hybrid model in which the alternatives contain both spatial and hedonic attributes. This model can be used to analyze market entry, product differentiation, and the extent of price competition. If we return to our example of the chocolate bars, before choosing a new product’s attributes, an entrant might first place the three existing products in attribute space and then survey consumers to learn about the distribution of their ideal points. The entrant could then estimate the Voronoi neighborhoods for her proposed product. If that neighborhood contains few consumers, she should not expect substantial sales. Any entrepreneur considering entering a market can take this approach. A boot designer can plot existing designs of insulated boots, of which there may be dozens, and find that none come in shiny patent leather. Someone designing a smartphone app for making to-do lists can map the features of existing apps, measure total market demand, and project possible sales.

We can visualize a price reduction in the spatial model of competition as a movement of the cut line. Refer back to figure 20.3 showing the two chocolate bars. The cut line corresponds to the ideal points of consumers who are indifferent between A and B. If the firm producing B lowers its price, and if consumers prefer to pay less for candy bars, then this will shift the cut line toward A and increase B’s market share. We do not need the model to know that B lowering its price should increase its market share. We do need the model to estimate the magnitude of that effect. The key will be to distinguish between crowded markets, with a large number of products in a low-dimensional attribute space, and a sparse market, where there are few competitors. In a crowded market, each product has a small Voronoi neighborhood. In a sparse market, the Voronoi neighborhoods are huge.





Figure 20.9: Price Competition in Sparse and Crowded Markets

Price changes have different effects in the two types of markets. Figure 20.9 shows the effects of a hypothetical 10% price reduction in candy bar B, from $2.00 to $1.80. The diagram on the left shows a sparse market. Lowering the price for B shifts the cut line between product A and B and increases B’s market share from 50% to 54%, an 8% increase in B’s market share. The 10% price drop and 8% sales increase reduces revenue by 3%. Lowering prices would be a bad idea. The diagram on the right shows a crowded market with seven types of candy bars. Here, the price drop has a smaller effect on B’s absolute market share, an increase of 5% from 15% to 20%, but this 5% represents a larger proportional increase (33%) in B’s market share. The overall effect is a 20% increase in revenue.16 Thus, the model predicts stronger price competition in crowded markets than in sparse markets, and extreme competition for commodities: products that are indistinguishable, like crude oil, pork bellies, and red wheat #2. It predicts less price competition for high-end fashion goods, where designers can sustain substantial price markups because product dimensionality creates a sparse market.

This relationship between the number of attributes and the extent of price competition suggests that a good strategy would be to add new attributes. This would make the market more sparse, reduce price competition, and lead to higher profits. Even if that inference is correct, the strategy may be easier stated than accomplished. People must value the new attribute. For each successful attribute—cordless stereo speakers—one can find multiple failed attempts—Bic’s ill-fated disposable underwear.





Summary


The spatial model of competition, the hedonic model of competition, and a hybrid of the two provide a framework within which we can represent different products, political candidates, or even job applicants. These models can measure ideological positions, price implicit attributes, and evaluate potential market entry positions. They generate insights into how market competition creates an incentive for differentiation, how political competition creates an incentive for convergence, and how price competition should be more intense for products with fewer attributes.

In the models, we make rather strong and empirically dubious assumptions. For example, we assume that people do not change their preferences, and that they do not succumb to social pressures. If that were so, why do firms and politicians spend enormous amounts of money trying to change preferences? We could shrug off this criticism by referring again to Box’s dictum that all models are wrong.

We can also construct a more nuanced response that distinguishes between fundamental preferences, the outcomes that a person desires, and her instrumental preferences, the person’s preferences over the attributes that produce the fundamental outcomes. A student’s fundamental preferences may strike a balance between being popular, healthy, and scholarly. She may pursue these fundamental ends through instrumental actions—waking early, going to the juice bar, and completing her homework so as to have time to be social in the evenings. Her choice of the fruit shake helps her to achieve a fundamental preference for good health. It is an instrumental preference. If she comes across a scientific paper revealing the high sugar content in fruit shakes, she may switch to drinking water. If so, her instrumental preferences change even though her fundamental preferences do not. Once again, we see how a model is not an end in itself but provides an architecture to structure our thinking.





Many Models of Value


In a market economy, we can measure an individual’s value for a good by the price she is willing to pay. An individual might value a pastrami sandwich at $7, a painting by Goya at $3 million, and a one-acre lot in Ocala, Florida, at $75,000. Many economic models ignore the source of these valuations. George Stigler famously quoted the sensualist Mitya from Dostoyevsky’s The Brothers Karamazov, who said, “De gustibus non est disputandum” (In matters of taste, there can be no disputes). The models we cover say less about tastes than about how tastes translate to the monetary values people assign to goods.

Hedonic attribute model: This model explains a good’s value based on intrinsic attributes. Differences in valuations depend on different underlying preferences over the good’s attributes. These attributes could be the physical components of the good. A pastrami sandwich consists of rye bread, six ounces of pastrami, Swiss cheese, mustard, pickles, and onions. Its value can then be written as a weighted linear combination of those components. More elaborate hedonic models can include interaction terms. The pastrami may be even more valuable if served on grilled rye bread.

Coordination model: This model explains prices as socially constructed. The value of a Goya painting depends on what other people believe its value to be. Initially, people have beliefs or opinions about the value of the painting. They then interact with other people in their social network and update their beliefs. Two people could both set their values equal to the mean of their two values; one person could change her value to match the other’s value; or each person could move their valuation in the direction of the others. Given any of these three assumptions, valuations converge locally. People connected to one another will have similar valuations. The ultimate value assigned to a good will depend on the initial distribution of values, the social network, and the order in which pairings occurs.

Predictive models: This model explains prices as forecasts of future value. The value of the one-acre lot in Ocala, Bitcoin, or a stock depends on how much people will pay for them in the future. These valuations depend on predictive models, which in turn depend on attributes and categories. We might categorize Ocala as warm, low-tax, and inland. Variation in people’s valuations arises from different predictive models. Investors use multiple predictive models. These models may rely on attributes or, as in the case of valuing Bitcoin, also make assumptions about coordination.

These three models provide three distinct explanations for the value of a good. No one model will be best in all cases. Each will have cases where it works best. The models function as arrows in our quiver. The value of a pastrami sandwich most likely derives from its intrinsic properties. The value of the Goya painting may be largely socially constructed: a painting has value if people believe it has value. The price of the land in Florida likely depends on valuations derived from predictions of future real estate values.


