# 
> 2018000模板




13. Random Walks





A drunk man will find his way home, but a drunk bird may get lost forever.

—Shizuo Kakutani



In this chapter, we learn two classic models from probability and statistics: the Bernoulli urn model and the random walk model.1 Both models describe random processes even if it may appear that they are producing complex structures. Randomness can be hard to discern without gathering data. We often think we see patterns in election outcomes, stock prices, and scoring in sporting events, but instead, to borrow Nassim Taleb’s lovely phrase, we are being fooled by randomness.2

The Bernoulli urn model describes random processes that produce discrete outcomes, like the flip of a coin or the roll of a die. Developed centuries ago to explain the odds of winning at gambling, it now occupies a central position in probability theory. The random walk model builds on that model by keeping running totals of the number of heads and tails. The model can capture the movement of particles in liquids and gases, the movement of animals in physical space, and growth in human height from birth to childhood.3

The chapter begins with brief coverage of the Bernoulli urn model along with an analysis of the length of streaks. We then describe the random walk model. We learn that one-dimensional and two-dimensional random walks return to their starting point infinitely often, while a three-dimensional random walk need not return home at all. We also learn that the time between returns to zero for a one-dimensional random walk will follow a power-law distribution. This finding, which we might be tempted to dismiss as a mathematical curiosity, can explain the life spans of species and firms. In the final section, we use the random walk model to evaluate the efficient market hypothesis and to determine the size of a network.





The Bernoulli Urn Model


The Bernoulli urn model consists of an urn containing gray and white balls. Draws from the urn represent the outcomes of random events. Each draw is independent of previous and future draws, so we can apply the law of large numbers: in the long run, the proportion of balls drawn of each color will converge to its proportion in the urn. That does not mean that a thousand draws from an urn containing seven white balls and three gray balls will produce exactly seven hundred white outcomes, only that the proportion of white balls will converge to 70%.4





Bernoulli Urn Model


Each period, a ball is randomly drawn from an urn containing G gray and W white balls. The outcome equals the ball’s color. The ball is returned to the urn prior to the next period’s draw. Let denote the proportion of gray balls. Given N draws, we can calculate the expected number of gray balls chosen, NG, and its standard deviation, σNG :





Outcomes in the Bernoulli urn model produce streaks of predictable lengths. In an urn with equal numbers of gray and white balls, the probability of drawing a white ball equals . The probability of drawing two consecutive white balls equals times . In general, if a proportion P of the balls in the urn are gray, the probability of drawing N consecutive white balls equals PN. By calculating probabilities, we can assess whether a streak was likely, amazing, or so improbable that we should expect fraud. When a basketball player makes a three-point shot nine times in a row, does he have a hot hand, or should we expect a random sequence of that length? The math shows that in a ten-year career, a good three-point shooter would be as likely as not to make nine in a row.5

We can make similar calculations to decide whether an investor has been lucky, good, or fraudulent. Berkshire Hathaway, the conglomerate run by Warren Buffett, outperformed the market forty-two out of fifty years from 1965 to 2014. A dollar invested in Berkshire Hathaway in 1964 was worth over $10,000 in 2016, while a dollar invested in the S&P 500 was worth about $23. If Berkshire had a 50% chance of beating the market, it should have outperformed the market twenty-five times during that fifty-year period, with a standard deviation of 3.5 years The actual number of years Berkshire beat the market lies about four standard deviations above the mean, a one-in-a-million event. We can rule out luck. Given that Berkshire reveals its investments, we can also rule out fraud. Bernie Madoff did not reveal his investments. His proclaimed streak of successes—decades of consecutive positive returns—was so unlikely that his clients should have demanded transparency.6





Random Walk Models


Our next model, the simple random walk model, builds on the Bernoulli urn model by keeping running totals of past outcomes. We set the initial value, the state of the model, to be zero. If we draw a white ball, we add 1 to the total. If we choose a gray ball, we subtract 1. The state of the model at any time equals the sum of the previous outcomes (i.e., the total number of white balls drawn minus the number of gray balls drawn).





A Simple Random Walk





where Vt denotes the value of the random walk at time t, V0 = 0 and R(-1, 1) is a random variable that is equally likely to equal -1 or 1. The expected value of a random walk in any period equals zero and has a standard deviation of , where t equals the number of periods.7



Figure 13.1 shows a simple random walk. The graph appears to have a pattern: a long downward trend followed by an upward trend and then a modest crash when the process crosses the zero line. That pattern happened by chance.

A simple random walk is both recurrent (it returns to zero infinitely often) and unbounded (it exceeds any positive or negative threshold). If we wait long enough, a random walk exceeds 10,000 and falls below negative 1 million. It also crosses zero infinitely often. In addition, the distribution of the number of steps required to return to zero satisfies a power law.8 Most returns to zero occur in a few steps. Half of all walks return in two steps. Other walks, though, take a long time to return. That must be true given the unboundedness of random walks. A walk that crosses a threshold of 1 million would requires more than 2 million steps to reach that value and then return back to zero.





Figure 13.1: Plot of a Simple Random Walk for 300 Periods

The power law distribution result has unexpected applications. If we model firms’ sales (or employees) as a random walk, firm life spans will be a power law. To be more precise, if we assume that when sales are strong, a firm adds an employee, that when sales are poor, a firm fires an employee, and that the firm closes when it no longer has employees, then the distribution of return times will equal the distribution of firm life spans, which will be a power-law distribution. And, to a first approximation, firm life spans are a power law.9 We can apply the same logic to predict the life spans of biological taxa (kingdom, phylum, class, order, family, genus, and species). If the number of members of a taxon follow a random walk—for example, if the number of species in a genus goes up and down randomly—the taxon sizes should satisfy a power law. Here again, data are supportive.10

We can apply the model as an analogy by thinking of the random walk as a glacier moving along the ground. That model would predict that the distribution of sizes of glacial lakes would satisfy a power-law distribution. Each time the glacier falls below the land mass’s surface and returns to the top, it creates a lake with a diameter that corresponds to the return time. Once again, data roughly align.11

The basic random walk model can be modified in several ways. We can create a normal random walk whose value in each period changes by an amount drawn from a normal distribution. A normal random walk will not return to zero exactly, though it will cross zero infinitely many times.

We can also make one outcome more likely than the other, producing a biased random walk. We can use biased random walks to predict the odds of winning in games of chance. In roulette, the probability of winning a bet on a red outcome equals .12 We can model the aggregate winnings (or losses) of a sequence of bets as a random walk that increases by 1 with probability (about 47.4%) and decreases by 1 with probability . After 100 bets, the expected losses are $5 with a standard deviation of $10. We can be 95% confident of losing no more than $25 and winning no more than $15. After 10,000 bets, expected losses equal $526 with a standard deviation of 100. Therefore, 95% of the time we lose between $325 and $725.13 Being ahead after10,000 equal bets is an event more than five standard deviations above the mean, a less than one-in-a-million possibility. It follows that to win at roulette, a person should make one big bet rather than many small bets.

Some sporting contests, such as basketball, can be modeled as two biased random walks. Each team has a probability of scoring on each trip down the court. That probability is estimated based on a profile of the team’s offensive abilities and the opposing team’s defensive abilities. We model a team’s trip down the court as a random event. Each team’s score corresponds to the value of its random walk. The team with the higher probability of scoring will be more likely to win. Analysis of data from the NBA reveals a close match to the model. Scoring deviates from random only when one team gains a huge lead, at which point the lead becomes more likely to decrease than increase. This phenomena could be explained by the winning team having less incentive to run up the score than the losing team has to make the score respectable.14

If we watch basketball, the outcomes seem far from random. Intelligent, athletic players run sophisticated offenses and make clutch plays. That is true, but the effects of effort may wash out. Extra effort to score on offense may be offset by extra effort on defense. A great steal may be wiped out by a player sprinting the length of the court to block a layup from behind. The model also suggests a strategy: stronger teams should speed up the game to create more possessions. Favored teams would rather spin the roulette wheel more often, as drift works to their advantage.

The simple random walk model takes place in a single dimension. We can also model higher-dimensional random walks. A two-dimensional random walk would begin at the origin in the plane, (0, 0), and then walk randomly to the north, south, east, or west in each period. A two-dimensional random walk resembles a squiggly line drawn on a sheet of paper. Two-dimensional random walks also satisfy recurrence and unboundedness. Random search will locate a lost earring in your living room. The mathematical fact of recurrence enables random foraging as a strategy for ants.15 If the two-dimensional random walk did not recur, ants would need more sophisticated internal maps or stronger pheromone trails to find their nests. In three dimensions, random walks do not satisfy recurrence. A fly skittering around a room and a molecule bouncing in the air return to their starting points a finite number of times—hence Kakutani’s quote about drunken men and drunken birds at the start of this chapter.16

The lack of recurrence of random walks provides yet another example how models can clarify our thinking. Intuition tells us that recurrence should occur less often as we add dimensions. Logic reveals an abrupt change. In one and two dimensions, a random walk returns to its origin infinitely many times. In three dimensions, it wanders off forever. To arrive at that type of result requires mathematics. Intuition alone will be insufficient.





Using Random Walks to Estimate Network Size


We can exploit the recurrence of low-dimensional random walks to estimate a network’s size. The method is straightforward. We select a node at random, start a random walk along the edges of the network, and keep track of how frequently it returns to the original node. The average time between returns correlates with the network’s size. To estimate the size of a social network, we could ask someone to name a friend, and then ask the friend to name a friend. We could continue that process and keep track of how often we return to the same person.





Figure 13.2: Random Walks on Networks

Figure 13.2 shows two networks. The network on the left has three nodes forming a triangle. The network on the right has six nodes forming two triangles. We can start a random walk on the left network at A. Suppose that it moves to B, then C, and back to A. The random walk returns to its starting point in three steps. On the network on the right, a random walk starting at D might follow a seven-step path F − G − H − F − E − F − D. If we repeat these experiments many times, the average return times on the network on the left will be shorter. Though unnecessary for small networks such as these, this method becomes useful on larger networks, like the World Wide Web or large email networks.





Random Walks and Efficient Markets


Stock prices prove to be nearly normal random walks with a positive drift to capture gains in the market. Many individual stock prices also are approximately random. Figure 13.3 shows the daily stock price data for Facebook for the year following its initial public offering on May 18, 2012. Facebook was offered at $42 per share. By June 1, 2012, the price had fallen to $28.89. One year later the price had fallen to $24.63. The figure also shows a random walk calibrated to have similar variation.





Figure 13.3: Facebook Daily Stock Price June 2012–June 2013 vs. a Random Walk

We can apply statistical tests to the sequence of Facebook share prices to see if it satisfies the assumptions of a normal random walk. First, the price should go up and down with equal probability. In the 249 trading days covered, Facebook’s stock price went down on 127 days, or 51% of the time. Second, in a random walk, the probability of an increase should be independent of an increase that occurred in the previous period. Facebook’s stock price moved in the same direction on consecutive days 54% of the time. Finally, the expected longest streak of moves in the same direction should be eight days. Facebook’s stock price went up on ten consecutive days once during this period. Overall, we cannot reject the claim that Facebook’s stock price is consistent with a normal random walk.

The same analysis can be done for daily prices in all stocks. To do so we must first subtract the mean upward trend in stock prices. Studies show that from the 1950s through the 1980s, daily stock prices had a slight positive correlation. After detrending, the probability of an increase following an increase exceeded . From 1980 onward, as investors became more sophisticated, the probability of an increase following an increase fell to 50%, consistent with a random walk. The reason stock prices might follow a random walk pattern is that smart investors identify and therefore eradicate patterns. For example, in the 1990s, analysts noticed that stock prices rose at the beginning of each year, a phenomenon called the January effect. Smart investors could buy stocks in December at low prices and sell them in January for a profit. If that strategy seems too good to be true, it is. If investors buy stocks in December, they raise prices, wiping out the January effect. We should not be surprised that the January effect no longer exists.

Economists draw an analogy between recognizable persistent patterns in market prices and hundred-dollar bills on the sidewalk. If someone sees a hundred-dollar bill, she picks it up. When she does, it goes away. The same logic applies to patterns in stock prices: if they exist, they go away. A market with smart investors will therefore contain few predictable price patterns. If prices exhibit no pattern, what remains must be a random walk (with the caveat that the general upward market trend must be subtracted away).

Paul Samuelson wrote an early model that produced a random walk. His model did not require that investors know the value of the stock in all future periods, only that they know the distribution. As Samuelson himself notes, “One should not read too much into the established theorem. It does not prove that actual competitive markets work well.”17 Samuelson’s reticence was not shared by everyone. Others extended this thinking to create the efficient market hypothesis, which states that at any moment in time the price of a stock captures all relevant information, and future prices must follow a random walk. The efficient market hypothesis rests on paradoxical logic.18 Determining an accurate price requires time and effort. A financial analyst must gather data and construct models. If prices followed a random walk, those activities would have no expected return. However, if no one expends effort to estimate prices, then prices will become inaccurate and the sidewalk will be covered in hundred-dollar bills. In brief, the Grossman and Stiglitz paradox states that if investors believe in the efficient market hypothesis, they stop analyzing, making markets inefficient. If investors believe the market is inefficient, then they perform analyses by applying models, making markets efficient.

In point of fact, price movements are rather close to random walks, although sophisticated statistical techniques do reveal short-run patterns.19 While there may be no hundred-dollar bills on the sidewalk, there are some four-leaf clovers in grassy fields that one can find by looking hard enough.

Critics of the hypothesis argue that some investors consistently win over longer periods than would be predicted by chance.20 Furthermore, prices could move randomly for some other reason, such as the aggregation of sophisticated trading rules. Day-to-day price volatility exceeds the amount of information that flows into markets, and the market takes huge jumps and dives when little of relevance appears to be happening in the wider world, suggesting the presence of bubbles. One person’s inconvenient facts can be another person’s “these caveats notwithstanding.” Yes, volatility is high, but small amounts of information can have large effects. And even though the market does takes big jumps and dives, the market could still follow a longer-tail random walk, where day-to-day movements come from a longer-tailed distribution.

Though it seems implausible to think that stock prices are accurate at all times, prices cannot diverge wildly from true values in the long run. We can see this by applying the rule of 72. If the economy grew by 3% per year, in half a century, the economy would increase 4-fold. If we go back to 1967, the United States GDP equaled about $4.2 trillion (in 2009 dollars). By 2017, GDP had increased to almost $17 trillion (in 2009 dollars), a 4-fold increase, exactly what we would expect given 3% growth. During that same period, the real value of stocks in the S&P 500 also increased about 4-fold. Had the stock market risen at 12% per year (in real dollars), then stock prices would have increased 256-fold, an impossibility.21

In the long run, assuming the efficient market hypothesis or something close to it is a reasonable assumption. In the short run, betting on prices correcting can be risky. The case of Long Term Capital Management (LTCM), a hedge fund whose board of directors included two Nobel Prize winners in economics, proves instructive. In 1996 and 1997, LTCM posted returns in excess of 40% in part by identifying inefficiencies and predicting the market would correct. In 1998, they noticed (correctly) that the price of Russian bonds was out of alignment with prices of US Treasury bonds. They bet big. However, a Russian default, the first since 1917, increased the misalignment in the short term. LTCM lost $4.6 billion and nearly caused a collapse of financial markets. Soon after LTCM was bailed out bond prices did align, though not soon enough. The lesson should be obvious: do not put too much faith in one model.





Summary


In this chapter, we learned the Bernoulli urn model and random walk model. We applied these models widely. We saw how to distinguish randomness from hot streaks, to develop strategies for gambling, to evaluate time series of stock prices, and to make sense of outcomes in basketball games. We also saw how to apply the power-law distribution of return times for a random walk to inform our understanding of the duration of firms and biological taxa.

From these applications, we see how the random walk model provides a useful frame for evaluating time series. We should not be fooled by a few years of success. It need not imply sustained excellence. In Good to Great: Why Some Companies Make the Leap and Others Don’t, one of the best-selling business books of all time, Jim Collins identified characteristics of consistently successful companies, such as having humble leaders, getting the right people on the team, and maintaining discipline (what Collins called “rinsing your cottage cheese” in homage to six-time Ironman triathlon champion Dave Scott’s habit of rinsing his cottage cheese to reduce the fat content). Collins singled out eleven great companies that kept to his principles. In the decade following the publication of his book, only one of the eleven produced strong growth. One was bought out. One was taken over by the government, and the other eight generated zero returns.

The fact that the great firms shared attributes does not imply that those attributes contribute to success. Perhaps the lowest-performing firms also share those attributes. Selecting the best firms and looking at their attributes is not model thinking. Model thinking would derive attributes that cause success, such as talented workers. It would then test those conclusions against data, and if possible look for natural experiments—instances where the relevant attributes change randomly. Other models, such as the dancing and rugged landscape models we cover in Chapter 28, call into question Collins’ core assumptions. If the economy is complex, traits that prove successful today need not work in the future. What creates great success now—big rocks first—may not be a good strategy in ten years. As a rule, we should apply many models before making broad pronouncements, lest we risk correspondingly large errors. We should also avoid being fooled by patterns. What appears to be a trend might well be random.




