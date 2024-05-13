# 
> 2018000模板


14. Path Dependence





No man ever steps in the same river twice, for it’s not the same river and he’s not the same man.

—Heraclitus



In this chapter, we cover models of path dependence. In any domain in which people base their behavior on the actions of others, be it international affairs, art, music, sports, business, religion, technology, or politics, we should expect some degree of path dependence. A college student’s choice of courses point her toward some career paths over others. An endorsement of a candidate may launch a political career. A friendship may lead to other social connections. The clothes we wear, the books we read, the movies we watch, and the activities that consume our time all exhibit some degree of path dependence.

Path dependence also exists on grander scales. Common-law rulings establish and reinforce precedents, influencing future rulings.1 Early institutional forms impact later institutional choices. The decision in the United States to provide health insurance through private firms resulted in a large private health insurance industry, health maintenance organizations, and a mix of public and private hospitals.2 Institutions also induce behavioral patterns, such as selfish or cooperative tendencies, that can in turn influence the efficacy of future institutions.3

In this chapter, we build dynamic urn models that produce sequences of outcomes that exhibit path dependence. These models extend the Bernoulli urn model by allowing the distribution of balls within the urn to change as a function of past outcomes. With these models to structure our thinking, we then provide a formal definition of path dependence and distinguish path-dependent outcomes from path-dependent equilibria. These formal definitions differentiate path dependence from tipping points, which are more abrupt changes in outcomes.

The chapter consists of four parts. The first two cover the Polya process and the balancing process. The Polya process assumes positive feedbacks and produces both path-dependent outcomes and equilibria. Many of the canonical examples of path dependence, including the growth of the QWERTY typewriter, are based on positive feedbacks, also known as increasing returns. The balancing process assumes negative feedbacks and produces path-dependent outcomes but not path-dependent equilibria. The third part defines a measure of path dependence based on entropy. The final section discusses further applications of the models.





Polya Process


The Polya process captures positive feedbacks using an extension of the Bernoulli urn model in which we add a ball to the urn that matches the ball chosen. This process generates outcome path dependence, where outcomes in each period depend on previous outcomes. It will also be true that the long-run distribution over outcomes—equilibrium path dependence—depends on outcomes.4 The distinction between these two types of path dependence will be central to what follows. A process that is equilibrium path dependent must be outcome path dependent. If outcomes in the long run depend on the path, then so must outcomes along the way. A process can be outcome path dependent but not equilibrium path dependent. What happens now could depend on the past, but the long-run equilibrium might be determined at the outset.





The Polya Process


An urn contains one white ball and one gray ball. Each period a ball is drawn randomly and returned to the urn along with an additional ball of the same color as the one drawn. The color of the ball drawn denotes the outcome.



The Polya process captures a variety of social and economic phenomena. A person’s choice of whether to learn to play tennis or racquetball could depend on the choices of others. A person might be more likely to choose tennis if more of her friends also choose tennis, as it increases her chances of finding a game. Similarly, a person’s decision about what type of software to buy, language to learn, or smart-phone to buy could also depend on earlier choices by friends. Similar logic also applies to choices by firms over which technological standards to adopt. They may base their choices on the actions of others.

The model captures these social influences by changing the distribution of balls. If gray balls represent people who choose tennis and white balls represent people who choose racquetball, then as more people choose tennis, the urn contains more gray balls, causing subsequent people to be more likely to choose tennis as well. This increasing pull toward the outcome that more people choose creates path dependence.





Figure 14.1: Outcomes Consisting of Two White Balls and One Gray Ball

We can derive two unexpected properties of the Polya process. First, any sequence with the same number of white outcomes occurs with equal probability. Second, every distribution of white and gray balls occurs with equal probability. The second property implies extreme path dependence. Anything can happen. Everything is equally likely. After 1,000 periods, the probability that the urn contains 40% white balls equals the probability that it contains 2% white balls.

To see why, consider all possible sequences of outcomes in the first three periods. The first period outcome is gray with probability . If so, we add a gray ball, increasing the probability that the second outcome will be gray to . If that outcome is also gray, we add a third gray ball, increasing the probability that the third outcome is gray to . It follows that the total probability of three gray balls (or three white balls) equals times times , which equals .

The three sequences in which the first three outcomes consist of two white balls and one gray ball are shown in figure 14.1. In the top row, the order of the outcomes is gray, white, and then white. The probability of this sequence is , as is the probability of other sequences. It follows that the probability of getting one of the three sequences equals . By symmetry, the probability of choosing two gray balls and one white ball also equals . Therefore, each set of outcomes—three white, three gray, two white and one gray, and two gray and one white—occurs with the same probability of . Moreover, sequences of two white and one gray also occurs with equal probability. Similar results can be shown for any number of periods.5

If we extend the Polya process to add balls of additional colors, extensions of both regularity properties still hold. Any proportion of the colors can arise and is equally probable. These results create a conundrum for producers of consumer products. Long-run consumer preferences for some product attributes may be random. Knowledge that an outcome cannot be predicted can still inform action. Ford would not want to build 40,000 yellow pickup trucks and later find that red emerged as the favorite color from a path-dependent process. The potential for unsold inventory in unwanted colors points to two potential actions. A company could construct its supply chain so that color choices come last; for example, a clothing company might wait to dye sweaters until popular colors become clearer. Or a company could choose to not give people a choice. Henry Ford offered his customers any color Model T they desired, so long as it was black. Apple did the same when it rolled out the first iPhone: you could get black, or, for the same price, you could get black.





The Balancing Process


Our second model, the balancing process, makes the opposite assumption of the Polya process. After drawing a ball of one color, we add a ball of the opposite color. If we draw white balls in the first two periods, the urn will contain three gray balls and only one white ball, resulting in a probability of drawing a gray ball. This process produces path-dependent outcomes, in that the likelihood of an outcome in any period depends on the history of past outcomes. However, it does not produce path-dependent equilibria. In the long run, the urn converges to equal proportions of each color ball.6





The Balancing Process


An urn contains one white ball and one gray ball. Each period a ball is drawn randomly and returned to the urn along with an additional ball of the color opposite to the color drawn. The color of the ball denotes the outcome.



The balancing process captures sequences of decisions or actions that include pressures toward equal allocation. Parents with two children may try to give equal time to each. Spending an afternoon with one child creates a desire to spend more time with the other child. The balancing process could even model organizational efforts to achieve equity. The International Olympic Committee (IOC) would like every region of the world to host games. In 2013, the IOC announced that Tokyo had been selected as the host city for the 2020 Summer Olympic and Paralympic Games. Two European cities, Istanbul and Madrid, lost. Four years later, the IOC awarded Paris the 2024 games and a North American city, Los Angeles, the 2028 games. Tokyo won the 2020 games in part on the strength of its proposal and in part because the Summer Games had not been held in Japan since 1964. Geographic fairness appears to exert sway. Europe, Asia and Oceania, and the Americas have hosted the games approximately equal numbers of times in the period following World War II. Europe has been awarded the games eight times, the Americas six times, and Asia and Oceania seven times.





Path Dependence or Tipping Point


Path dependence, a gradual effect on outcomes, differs from a tipping point, an abrupt change in outcomes. The growth of Microsoft provides a good example of path dependence. Founded in 1975, Microsoft developed interpreters for the BASIC computer language. In 1979, Microsoft inked a deal with International Business Machines (IBM) to provide the operating system for IBM’s personal computer. This deal set Microsoft on a path that transformed a company with forty employees into one of the most valuable companies in the world.

The IBM contract contributed to Microsoft’s upward path but did not guarantee long-term success. At the time, the personal computer market was small. The internet did not exist, nor did sophisticated word processing, business software, or video games. Moreover, the success of the personal computer depended in part on the DOS operating system that Microsoft developed. As the personal computer market grew, other companies developed software compatible with DOS, providing more positive feedbacks. These events—the success of DOS, the growth of the personal computer market, and the development of software running on the DOS platform—can be thought of as one color of ball being consistently drawn from the urn. Each outcome made the next more likely. The computer age may have been inevitable, but Microsoft’s central role and the growth of the personal computer represent one of many potential paths.

We can contrast the path dependence of Microsoft’s growth with the assassination of Archduke Franz Ferdinand on June 28, 1914, which many see as a tipping point that led to World War I. Six years prior to the assassination, Austria-Hungary had annexed Bosnia and Herzegovina. Among the Serbians unhappy with that development was Gavrilo Princip, who shot and killed Franz Ferdinand and his wife, Sophie. Austria-Hungary blamed Serbia, a near-inevitable reaction, and then turned to Germany’s Kaiser Wilhelm for assurance as they prepared for war against Serbia. Tensions escalated. Serbia had an alliance with Russia, which in turn had alliances with France and the United Kingdom. By August 2, Germany had declared war on France. On August 3, Belgium refused to grant Germany free passage into France, and full-scale war began. This vastly simplified version of events suggests that given the alliances, the killing of the archduke tipped the world toward war.

We can measure path dependence and tipping points through changes in the probabilities of the possible outcomes.7 For the Polya process, the initial probability distribution is uniform over all distributions in the urn. This is the maximum entropy distribution. As events unfold, the distribution slowly narrows, indicative of path dependence: what might happen changes as outcomes occur. The reduction in entropy is gradual. At a tipping point, the probability distribution changes abruptly. Entropy may fall quickly. Figure 14.2 demonstrates the difference in two processes, each with two possible outcomes. After an event occurs—the contract for Microsoft or the killing of the archduke—the probabilities of each change. Subsequent events also change the probabilities. The process with the tipping point has a sharp kink. The path-dependent process changes slowly.





Figure 14.2: A Tipping Point vs. Path Dependence





Further Applications


In real situations, path dependence may not be as extreme as in the Polya process. Nevertheless, we can infer from the model that when behavior has a large social component, almost anything can happen. On one college campus, most students may wear black winter parkas; on another, they may wear blue peacoats. Model thinking suggests that differences could be the result of social influence as much as distinct underlying preferences. That holds in any context where people choose among a fixed set of options and their choices depend on the choices made earlier by others. Examples include democratic elections, which movie to see, and which technology to purchase.

The model can be extended to allow social influence to vary by the alternative chosen. Vanilla ice cream may have a constant level of feedback. The more exotic green tea ice cream may generate more variation in feedback: a friend may not like it and discourage you from trying it, or a friend may love it and encourage you to order it. It can be shown that less variation in feedbacks increases the likelihood of choosing an outcome.8 The model can also be changed so that people differ in their susceptibility to social influence; some people give more or less weight to the balls added to the run.

In any variation of the model, we can measure (or estimate) the extent of path dependence and compare it to other versions. If the assumptions we make in constructing a model of new product introductions shows that outcomes depend on the early part of the path, then entering, intervening, or subsidizing early may be a good strategy. The model provides a logic for companies to rush their products to market or offer steep discounts to generate early adopters. Other assumptions may show that having the better product may matter more than entering early and that the better strategy is to focus on quality. By using models, we can identify the features relevant to a particular situation—the relative importance of individual preferences and social effects, the variation in feedbacks, and the relative differences in quality—and deploy that knowledge to inform strategy and guide data collection.

On a final note, the Polya process shows how positive feedbacks can produce path-dependent outcomes and equilibria. Path dependence arises in a far broader set of contexts. Some degree of path dependence (in outcomes if not equilibria) occurs whenever one action bumps into or interacts with future actions. That is true when making decisions on large public projects.9 The decision to build a park or a highway constrains future planning decisions. The extent of that path dependence generally will depend on the size of the project. Central Park has had a profound impact on how New York City has developed. While the Polya process reveals the core idea that interactions produce path dependence, we need more realistic models for that insight to guide action.





Value at Risk and Volatility


We can interpret the standard deviation in a time series of data as volatility. Investments in stocks, real estate, and privately held businesses all exhibit volatility. Value at risk (VaR) measures the probability of a loss of a given amount during a specific time period. An investment with a one-year 5% VaR of $10,000 has a 5% probability of losing more than $10,000 at the end of one year.10 Banks use VaR calculations to determine the amount of assets that must be kept on hand to avoid bankruptcy. For example, to secure an investment with a two-week 40% VaR of $100,000, an investor may be asked to hold $100,000 in cash.

If an investment follows a simple random walk with an increase or decrease of size M each period, then it has an N period 2.5% VaR of .11 Thus, an investment that randomly goes up or down $1,000 each day has a nine-day 2.5% VaR of $6,000, and a one-year 2.5% VaR of $38,000. Notice that VaR increases linearly in the size of the steps but that it increases like the square root of the number of periods. We can use the formula for VAR to explain why the FDIC only requires that banks hold around 2% of their assets in cash overnight, but banks require that consumers put down 20% deposits on houses. The duration on the overnight loans is one day. Home loans can last for over a decade. The square root of three thousand and sixty-five days is approximately sixty.

Here, we have assumed a normal random walk. Analysts calculating VaR often consider the past empirical distribution of returns. If the empirical distribution has a longer tail, that is, if it includes more large events, then VAR would increase as large events are more likely.

Though VaR originated in finance, the idea can be applied broadly. A nonprofit that operates a volunteer-led Saturday morning soup kitchen that requires twenty-five volunteers might want to know the likelihood of lacking sufficient volunteers. If the number of volunteers follows a simple random walk that increases or decreases by 1 each week, then using the formula for VaR above, and setting M = 1 and N = 52, we find a one-year 2.5% VaR of 15, implying the nonprofit has a 2.5% chance of a volunteer shortage.




