Describe random phenomena by listing the possible outcomes and their associated probabilities.

Learn the basic rules that probabilities must obey.

Understand the relation between the odds of an event and the probability of an event.

Case Study: Super Bowl Probabilities

Shortly after the Philadelphia Eagles won Super Bowl 52, websites were already posting the probabilities of winning Super Bowl 53 for the various National Football League teams. These probabilities were updated regularly. Table 18.1 lists the probabilities posted on one website prior to the start of the 2018 season. These are perhaps best interpreted as personal probabilities. They are likely to change as the 2018 season progresses because the players on teams will change due to trades and injuries.

Table 18.1 Probabilities of winning Super Bowl 53

Team Probability Team Probability

New England Patriots 1/7 Los Angeles Chargers 1/34

Los Angeles Rams 1/11 Baltimore Ravens 1/34

Pittsburgh Steelers 1/11 Indianapolis Colts 1/34

Philadelphia Eagles 1/11 Jacksonville Jaguars 1/34

Minnesota Vikings 1/13 Tennessee Titans 1/41

Green Bay Packers 1/13 Detroit Lions 1/41

San Francisco 49ers 1/15 New York Giants 1/51

Houston Texans 1/17 Tampa Bay Buccaneers 1/51

New Orleans Saints 1/21 Arizona Cardinals 1/67

Dallas Cowboys 1/21 Chicago Bears 1/81

Denver Broncos 1/21 Washington Redskins 1/81

Atlanta Falcons 1/21 Cincinnati Bengals 1/81

Oakland Raiders 1/26 Buffalo Bills 1/81

Seattle Seahawks 1/29 Miami Dolphins 1/101

Carolina Panthers 1/29 Cleveland Browns 1/101

Kansas City Chiefs 1/34 New York Jets 1/101

Data from www.betvega.com/super-bowl-odds/ (opening probabilities for the 2018 season).

Because these are personal probabilities, are there any restrictions on the choices for the probabilities? In this chapter, we will answer this question. We will learn that probabilities must obey certain rules in order to make sense. By the end of this chapter, you will be able to assess whether the probabilities in Table 18.1 make sense.

Probability Models

Choose a woman aged 25 to 29 years old at random and record her marital status.「At random」means that we give every such woman the same chance to be the one we choose. That is, we choose a random sample of size 1. The probability of any marital status is just the proportion of all women aged 25 to 29 who have that status—if we chose many women, this is the proportion we would get. Here is the set of probabilities:

Marital status: Never married Married Widowed Divorced

Probability: 0.580 0.388 0.002 0.030

Statistics in Your World

Politically correct In 1950, the Russian mathematician B. V. Gnedenko (1912–1995) wrote a book, The Theory of Probability, that was popular around the world. The introduction contains a mystifying paragraph that begins,「We note that the entire development of probability theory shows evidence of how its concepts and ideas were crystallized in a severe struggle between materialistic and idealistic conceptions.」It turns out that「materialistic」is jargon for「Marxist-Leninist.」It was good for the health of Russian scientists in the Stalin era to add such statements to their books.

This table gives a probability model for drawing a young woman at random and finding out her marital status. It tells us what are the possible outcomes (there are only four) and it assigns probabilities to these outcomes. The probabilities here are the proportions of all women in each marital class. That makes it clear that the probability that a woman is not married is just the sum of the probabilities of the three classes of unmarried women:

Key Terms

A probability model for a random phenomenon describes all the possible outcomes and says how to assign probabilities to any collection of outcomes. We sometimes call a collection of outcomes an event.

As a shorthand, we often write for「the probability that the woman we choose is not married.」You see that our model does more than assign a probability to each individual outcome—we can find the probability of any collection of outcomes by adding up individual outcome probabilities.

Probability Rules

Because the probabilities in this example are just the proportions of all women who have each marital status, they follow rules that say how proportions behave. Here are some basic rules that any probability model must obey:

Any probability is a number between 0 and 1. Any proportion is a number between 0 and 1, so any probability is also a number between 0 and 1. An event with probability 0 never occurs, and an event with probability 1 occurs on every trial. An event with probability 0.5 occurs in half the trials in the long run.

The sum of probabilities of all possible outcomes must have probability 1. Because some outcome must occur on every trial, the sum of the probabilities for all possible outcomes must be exactly 1.

The probability that an event does not occur is 1 minus the probability that the event does occur. If an event occurs in (say) 70% of all trials, it fails to occur in the other 30%. The probability that an event occurs and the probability that it does not occur always add to 100%, or 1.

If two events have no outcomes in common, the probability that one or the other occurs is the sum of their individual probabilities. If one event occurs in 40% of all trials, a different event occurs in 25% of all trials, and the two can never occur together, then one or the other occurs on 65% of all trials because

Example 1

Marital status of young women

Look again at the probabilities for the marital status of young women. Each of the four probabilities is a number between 0 and 1. Their sum is

This assignment of probabilities satisfies Rules A and B. Any assignment of probabilities to all individual outcomes that satisfies Rules A and B is legitimate. That is, it makes sense as a set of probabilities. Rules C and D are then automatically true. Here is an example of the use of Rule C.

The probability that the woman we draw at random is not married is, by Rule C,

That is, if 38.8% are married, then the remaining 61.2% are not married. Rule D says that you can also find the probability that a randomly selected woman is not married by adding the probabilities of the three distinct ways of being not married, as we did earlier. This gives the same result.

Example 2

Rolling two dice

Rolling two dice is a common way to lose money in casinos. There are 36 possible outcomes when we roll two dice and record the up-faces in order (first die, second die). Figure 18.1 displays these outcomes. What probabilities should we assign?

Figure 18.1 The 36 possible outcomes from rolling two dice, Example 2.

The outcomes are as follows: (1, 1); (2, 1); (3, 1); (4, 1); (5, 1); (6, 1); (1, 2); (1, 2); (3, 2); (4, 2); (5, 2); (6, 2); (1, 3); (2, 3); (3, 3); (4, 3); (5, 3); (6, 3); (1, 4); (2, 4); (3, 4); (4, 4); (5, 4); (6, 4); (1, 5); (2, 5); (3, 5); (6, 5); (1, 6); (2, 6); (3, 6); (4, 6); (5, 6); and (6, 6).

Casino dice are carefully made. Their spots are not hollowed out, which would give the faces different weights, but are filled with white plastic of the same density as the red plastic of the body. For casino dice, it is reasonable to assign the same probability to each of the 36 outcomes in Figure 18.1. Because these 36 probabilities must have sum 1 (Rule B), each outcome must have probability or 1-in-36.

We are interested in the sum of the spots on the up-faces of the dice. What is the probability that this sum is 5? The event「roll a 5」contains four outcomes, and its probability is the sum of the probabilities of these outcomes:

Line 1: The equation reads, P of (roll a 5) equals P of one and four plus P of two and three plus P of three and two plus P of four and one.

Line 2: 1 over 36 plus 1 over 36 plus 1 over 36 plus 1 over 36.

Line 3: 4 over 36 equals 0.111

Now it’s your turn

18.1 Rolling dice. Suppose you roll two casino dice, as in Example 2. What is the probability that the sum of the spots on the up-faces is 7? 11? 7 or 11?

The rules tell us only what probability models make sense. They don’t tell us whether the probabilities are correct, that is, whether they describe what actually happens in the long run. The probabilities in Example 2 are correct for casino dice. Inexpensive dice with hollowed-out spots are not balanced, and this probability model does not describe their behavior.

What about personal probabilities? Because they are personal, can’t they be anything you want them to be? If your personal probabilities don’t obey Rules A and B, you are entitled to your opinion, but we can say that your personal probabilities are incoherent. That is, they don’t go together in a way that makes sense. So we usually insist that personal probabilities for all the outcomes of a random phenomenon obey Rules A and B. That is, the same rules govern both kinds of probability. For example, if you believe that the Philadelphia Eagles, the Los Angeles Rams, and the New England Patriots each have probability of 0.4 of winning Super Bowl LIII, your personal probabilities would not obey Rule B.

You now have enough information to read the「What’s the verdict?」story on page 441, and to answer the two questions.

Probability and Odds

Speaking of sports, many newspapers, magazines, and websites often give probabilities as betting odds. For example, at the end of February 2019, one website gave the betting odds of 4 to 9 that the Golden State Warriors would win the 2018–19 National Basketball Association finals. This means that a bet of $ will pay you $ if the team wins and cost you the $ you bet if the team loses. If this is a fair bet, you expect that in the long run you should break even, winning as much money as you lose. In particular, if you bet times, on average you should win $4 to 9 times and lose $ the other times. Thus, on average, if you bet times, you win of those bets. Odds of to therefore represent a probability of of winning.

More generally, betting odds take the form「 to .」Odds of to represent a probability of of winning.

As another example, on the web one can find the current odds of winning the next Super Bowl for each NFL team. We found a list of such odds at www.betvega.com/super-bowl-odds/. When we checked this website on December 5, 2018, the odds that the Los Angeles Rams would win Super Bowl 53 were 3-to-1. This corresponds to a probability of winning of The odds that the New York Jets would win Super Bowl 53 were 5000 to 1. This corresponds to a probability of

Probability Models for Sampling

Key Terms

The sampling distribution of a statistic tells us what values the statistic takes in repeated samples from the same population and how often it takes those values. We think of a sampling distribution as assigning probabilities to the values the statistic can take. Because there are usually many possible values, sampling distributions are often described by a density curve such as a Normal curve.

Choosing a random sample from a population and calculating a statistic such as the sample proportion is certainly a random phenomenon. The distribution of the statistic tells us what values it can take and how often it takes those values. That sounds a lot like a probability model.

Example 3

A sampling distribution

Take a simple random sample of 1004 adults. Ask each whether they feel childhood vaccinations are very important. The proportion who say Yes

is the sample proportion . Do this 1000 times and collect the 1000 sample proportions from the 1000 samples. The histogram in Figure 18.2 shows the distribution of 1000 sample proportions when the truth about the population is that 71% would agree that childhood vaccinations are important. The results of random sampling are of course random: we can’t predict the outcome of one sample, but the figure shows that the outcomes of many samples have a regular pattern.

Figure 18.2 The sampling distribution of a sample proportion from simple random samples of size 1004 drawn from a population in which 71% of the members would give positive answers, Example 3. The histogram shows the distribution from 1000 samples. The Normal curve is the ideal pattern that describes the results of a very large number of samples. (This figure was created using the Minitab software package.)

The horizontal axis represents Value of sample proportion with values ranging from 0.65 to 0.77 with an interval of 0.02. A bell-shaped curve starts from 0.65 and rises up to form a peak at 0.71 and gradually declines to end at point 0.77.

This repetition reminds us that the regular pattern of repeated random samples is one of the big ideas of statistics. The Normal curve in the figure is a good approximation to the histogram. The histogram is the result of these particular 1000 simple random samples (SRSs). Think of the Normal curve as the idealized pattern we would get if we kept on taking SRSs from this population forever. That’s exactly the idea of probability—the pattern we would see in the very long run. The Normal curve assigns probabilities to sample proportions computed from random samples.

This Normal curve has mean 0.710 and standard deviation about 0.014. The「95」part of the 68–95–99.7 rule says that 95% of all samples will give a falling within 2 standard deviations of the mean. That’s within 0.028 of 0.710, or between 0.682 and 0.738. We now have more concise language for this fact: the probability is 0.95 that between 68.2% and 73.8% of the people in a sample will say Yes. The word「probability」says we are talking about what would happen in the long run, in very many samples.

We note that of the 1000 SRSs, 94.3% of the sample proportions were between 0.682 and 0.738, which agrees quite well with the calculations based on the Normal curve. This confirms our assertion that the Normal curve is a good approximation to the histogram in Figure 18.2.

A statistic from a large sample has a great many possible values. Assigning a probability to each individual outcome worked well for four marital classes or 36 outcomes of rolling two dice but is awkward when there are thousands of possible outcomes. Example 3 uses a different approach: assign probabilities to intervals of outcomes by using areas under a Normal density curve. Density curves have area of 1 underneath them, which lines up nicely with total probability 1. The total area under the Normal curve in Figure 18.2 is 1, and the area between 0.682 and 0.738 is 0.95, which is the probability that a sample gives a result in that interval. When a Normal curve assigns probabilities, you can calculate probabilities from the 68–95–99.7 rule or from Table B of percentiles of Normal distributions. These probabilities satisfy Rules A through D.

Example 4

Do you approve of gambling?

An opinion poll asks an SRS of 501 teens,「Generally speaking, do you approve or disapprove of legal gambling or betting?」Suppose that, in fact, exactly 50% of all teens would say Approve if asked. (This is close to what polls show to be true.) The poll’s statisticians tell us that the sample proportion who say Approve will vary in repeated samples according to a Normal distribution with mean 0.5 and standard deviation about 0.022. This is the sampling distribution of the sample proportion .

The 68–95–99.7 rule says that the probability is 0.16 that the sample proportion is more than one standard deviation below the mean. The standard deviation in this case is 0.022 and the mean is 0.50, so this implies that the probability is 0.16 that the poll gets a sample in which fewer than 47.8% say Approve. Figure 18.3 shows how to get this result from the Normal curve of the sampling distribution.

Figure 18.3 The Normal sampling distribution, Example 4. Because 0.478 is one standard deviation below the mean, the area under the curve to the left of 0.478 is 0.16.

The graph shows a bell-shaped curve that starts from a point beyond 0.478 on the horizontal axis, has a positive slope and reaches a peak, and then gradually curves downward. The horizontal line has points at 0.478, 0.5, and 0.522. A vertical line starts at the point 0.478 on the horizontal axis and intersects the left side of the curve. This area is shaded and is labeled probability 0.16. A vertical line starts at point 0.522 on the horizontal axis and intersects the right side of the curve. The area under this region is labeled probability 0.16. The region enclosed by the curve between the points 0.478 and 0.522 is labeled Probability 0.68.

Now it’s your turn

18.2 Teen opinion poll. Refer to Example 4. Using the 68–95–99.7 rule, what is the probability that fewer than 54.4% say Yes?

Example 5

Using Normal percentiles*

What is the probability that the opinion poll in Example 4 will get a sample in which 52% or more say Yes? Because 0.52 is not 1, 2, or 3 standard deviations away from the mean, we can’t use the 68–95–99.7 rule. We will use Table B of percentiles of Normal distributions.

To use Table B, first turn the outcome into a standard score by subtracting the mean of the distribution and dividing by its standard deviation:

which we will round off to 0.9 in order to use Table B. Now look in Table B. A standard score of 0.9 is the 81.59 percentile of a Normal distribution. This means that the probability is 0.8159 that the poll gets a smaller result. By Rule C (or just the fact that the total area under the curve is 1), this leaves probability 0.1841 for outcomes with 52% or more answering Yes. Figure 18.4 shows the probabilities as areas under the Normal curve.

Figure 18.4 The Normal sampling distribution, Example 5. The outcome 0.52 has standard score 0.9, so Table B tells us that the area under the curve to the left of 0.52 is 0.8159.

The graph starts from a point a little bit away from the origin and curves upward on the left, and reaches a peak. It gradually declines toward the right and plateaus on the horizontal axis. The mid-point of the horizontal axis is labeled 0.5. A vertical line starts from the point 0.52 on the horizontal axis and meets the right inclination of the curve. The area under this region is shaded and labeled Probability 0.1841. The region between the left inclination of the curve and the vertical line, marked 0.52 is labeled Probability 0.8159.

*Example 5 is optional.

Chapter 18 Summary and Exercises

Chapter 18: Statistics in Summary

A probability model describes a random phenomenon by telling what outcomes are possible and how to assign probabilities to them.

There are two simple ways to give a probability model. The first assigns a probability to each individual outcome. These probabilities must be numbers between 0 and 1 (Rule A), and they must add to exactly 1 (Rule B). To find the probability of any event, add the probabilities of the outcomes that make up the event.

The second kind of probability model assigns probabilities as areas under a density curve, such as a Normal curve. The total probability is 1 because the total area under the curve is 1. This kind of probability model is often used to describe the sampling distribution of a statistic. This is the pattern of values of the statistic in many samples from the same population.

All legitimate assignments of probability, whether data based or personal, obey the same probability rules. So the mathematics of probability is always the same.

Odds of to that an event occurs correspond to a probability of

This chapter summary will help you evaluate the Case Study.

Link It

This chapter continues the discussion of probability that we began in Chapter 17. Here, we examine the formal mathematics of probability, embodied in probability models and probability rules. Probability models and rules provide the tools for describing and predicting the long-run behavior of random phenomena.

In this chapter, we also begin to formalize this process, first mentioned in Chapter 3, of using a statistic to estimate an unknown parameter. In particular, the sampling distribution will be the「probabilistic」tool we use to generalize from data produced by random samples and randomized comparative experiments to some wider population. Exactly how we do this will be the subject of Part IV.

Case Study Evaluated

Look again at Table 18.1, discussed in the Case Study that opened the chapter. Use what you have learned in this chapter to evaluate the Case Study. Start by reviewing the information in the Chapter Summary. Then answer the following questions about the Case Study in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying.

Do the probabilities in this table follow the rules given on page 427?

On some websites, the probabilities are given as betting odds of winning. If you are a bookie setting betting odds, should you set the odds so the corresponding probabilities, after converting odds to probabilities, sum to greater than 1, exactly 1, or less than 1? Discuss. (Hint: If you are a bookie, will you make more money if you set the betting odds so that the probabilities of winning are too high or are too low?)

In this chapter you have:

Described random phenomena using a probability model that lists the possible outcomes and their associated probabilities.

Learned the basic rules that probabilities must obey.

Understood the relation between the odds of an event and the probability of an event.

Online Resources

The Snapshots video, Probability, introduces the concepts of randomness, probability, and probability models in the context of some examples.

The StatBoards video, The Four Basic Probability Rules, discusses the basic probability rules in the context of some simple examples.

Check the Basics

For Exercise 18.1, see page 429; for Exercise 18.2, see page 433.

18.3 Probability models. A probability model describes a random phenomenon by telling us which of the following?

Whether we are using data-based or personal probabilities.

What outcomes are possible and how to assign probabilities to these outcomes.

Whether the probabilities of all outcomes sum to 1 or sum to a number different than 1.

All of the above.

18.4 Probability models. Which of the following is true of any legitimate probability model?

The probabilities of the individual outcomes must be numbers between 0 and 1, and they must sum to no more than 1.

The probabilities of the individual outcomes must be numbers between 0 and 1, and they must sum to at least 1.

The probabilities of the individual outcomes must be numbers between 0 and 1, and they must sum to exactly 1.

Probabilities can be computed using the Normal curve.

18.5 Density curves. Which of the following is true of density curves?

Areas under a density curve determine probabilities of outcomes.

The total area under a density curve is 1.

The Normal curve is a density curve.

All of the above are true.

18.6 Probability rules. To find the probability of any event,

add up the probabilities of the outcomes that make up the event.

use the probability of the outcome that best approximates the event.

assign it a random, but plausible, value between 0 and 1.

average together the personal probabilities of several experts.

18.7 Sampling distributions. The sampling distribution of a statistic is

the method of sampling used to obtain the data from which the statistic is computed.

the possible methods of computing a statistic from the data.

the pattern of the data from which the statistic is computed.

the pattern of values of the statistic in many samples from the same population.

Chapter 18 Exercises

18.8 Moving up. Sociologists studying social mobility in the United States find that the probability that someone who began their career in the bottom 10% of earnings remains in the bottom 10% 15 years later is 0.59. What is the probability that such a person moves to one of the higher income classes 15 years later?

18.9 Causes of death. Government data assign a single cause for each death that occurs in the United States. Data from 2016 show that the probability is 0.23 that a randomly chosen death was due to heart disease and 0.22 that it was due to cancer. What is the probability that a death was due either to heart disease or to cancer? What is the probability that the death was due to some other cause?

18.10 Land in Canada. Choose an acre of land in Canada at random. The probability is 0.38 that it is forest and 0.07 that it is agricultural.

What is the probability that the acre chosen is not forested?

What is the probability that it is either forest or agricultural?

What is the probability that a randomly chosen acre in Canada is something other than forest or agricultural?

18.11 Our favorite president. A 2018 poll by the Pew Research Survey Center interviewed a random sample of 2002 adult Americans. Those in the sample were asked which president has done the best job in their lifetime. Here are the results:

Outcome Probability

Barack Obama 0.31

Ronald Reagan 0.21

Bill Clinton 0.13

Donald Trump 0.10

Someone else ?

These proportions are probabilities for the random phenomenon of choosing an adult American at random and asking her or his opinion.

What must be the probability that the person chosen selects someone other than Barack Obama, Ronald Reagan, Bill Clinton, or Donald Trump? Why?

The event「I would select either Barack Obama or Ronald Reagan」contains the first two outcomes. What is its probability?

18.12 Rolling a die. Figure 18.5 displays several assignments of probabilities to the six faces of a die. We can learn which assignment is actually correct for a particular die only by rolling the die many times. However, some of the assignments are not legitimate assignments of probability. That is, they do not obey the rules. Which are legitimate and which are not? In the case of the illegitimate models, explain what is wrong.

Figure 18.5 Four probability models for rolling a die, Exercise 18.12.

The table has six rows and five columns. The column headers are as follows: Outcome, Model 1, Model 2, Model 3, and Model 4. The data given in the table are as follows:

Row 1: 1 die; 1 over 7; 1 over 3; 1 over 3; 1.

Row 1: 2 dice; 1 over 7; 1 over 6; 1 over 6; 1.

Row 1: 3 dice; 1 over 7; 1 over 6; 1 over 6; 2.

Row 1: 4 dice; 1 over 7; 0; 1 over 6; 1.

Row 1: 5 dice; 1 over 7; 1 over 6; 1 over 6; 1.

Row 1: 6 dice; 1 over 7; 1 over 6; 1 over 6; 2.

18.13 Political views of college students. Select a first-year college student at random and ask how they would characterize their political views. Here are the probabilities, based on proportions from a large sample survey in 2016 of first-year students:

Political view: Far left Liberal Middle of the road Conservative Far right

Probability: 0.04 0.31 0.43 0.20 0.02

What is the sum of these probabilities? Why do you expect the sum to have this value?

What is the probability that a randomly chosen first-year college student had political views that are not far left?

What is the probability that a first-year student had political views that are either conservative or far right?

18.14 Tetrahedral dice. Psychologists sometimes use tetrahedral dice to study our intuition about chance behavior. A tetrahedron (Figure 18.6) is a pyramid with four faces, each a triangle with all sides equal in length. Label the four faces of a tetrahedral die with one, two, three, and four spots. Give a probability model for rolling such a die and recording the number of spots on the down-face. Explain why you think your model is at least close to correct.

Figure 18.6 A tetrahedron. Exercises 18.14 and 18.16 concern dice with this shape.

18.15 Birth order. A couple plan to have three children. There are eight possible arrangements of girls and boys. For example, GGB means the first two children are girls and the third child is a boy. All eight arrangements are (approximately) equally likely.

Write down all eight arrangements of the sexes of three children. What is the probability of any one of these arrangements?

What is the probability that the couple’s children are two girls and one boy?

18.16 More tetrahedral dice. Tetrahedral dice are described in Exercise 18.14. Give a probability model for rolling two such dice. That is, write down all possible outcomes and give a probability to each. (Example 2 and Figure 18.1 may help you.) What is the probability that the sum of the down-faces is 5?

18.17 Roulette. A roulette wheel has 38 slots, numbered 0, 00, and 1 to 36. The slots 0 and 00 are colored green, 18 of the others are red, and 18 are black. The dealer spins the wheel and, at the same time, rolls a small ball along the wheel in the opposite direction. The wheel is carefully balanced so that the ball is equally likely to land in any slot when the wheel slows. Gamblers can bet on various combinations of numbers and colors.

What is the probability of any one of the 38 possible outcomes? Explain your answer.

If you bet on「red,」you win if the ball lands in a red slot. What is the probability of winning?

A friend tells you that the odds that a bet on「red」will win are 10 to 9. Is your friend correct? If not, what are the correct odds?

The slot numbers are laid out on a board on which gamblers place their bets. One column of numbers on the board contains all multiples of 3, that is, 3, 6, 9, … , 36. You place a「column bet」that wins if any of these numbers comes up. What is your probability of winning?

18.18 Colors of M&Ms. If you draw an M&M candy at random from a bag of the candies, the candy you draw will have one of six colors. The probability of drawing each color depends on the proportion of each color among all candies made.

Here are the probabilities of each color for a randomly chosen plain M&M produced at the New Jersey factory:

Color: Blue Orange Green Yellow Red Brown

Probability: 0.250 0.250 0.125 0.125 0.125 ?

What must be the probability of drawing a brown candy?

The probabilities for plain M&Ms produced at the Tennessee factory are a bit different. Here they are:

Color: Blue Orange Green Yellow Red Brown

Probability: 0.207 0.205 0.198 0.135 0.131 ?

What is the probability that an M&M chosen at random from the Tennessee factory is brown?

What is the probability that a plain M&M from the New Jersey factory is any of blue, yellow, or orange? What is the probability that a plain M&M from the Tennessee factory has one of these colors?

18.19 Legitimate probabilities? In each of the following situations, state whether or not the given assignment of probabilities to individual outcomes is legitimate, that is, whether it satisfies the rules of probability. If not, give specific reasons for your answer.

When a coin is spun, and

When two coins are tossed, and

Plain M&Ms have not always had the mixture of colors given in Exercise 18.18. In 1997, brown was the most popular color and had probability 0.30. Yellow and red each had probability 0.20. Orange, green, and blue each had probability 0.10.

18.20 Immigration. Suppose that 29% of all adult Americans think that the level of immigration to the United States should be decreased. An opinion poll interviews 1520 randomly chosen Americans and records the sample proportion who feel that the level of immigration to this country should be decreased. This statistic will vary from sample to sample if the poll is repeated. The sampling distribution is approximately Normal with mean 0.29 and standard deviation about 0.012. Sketch this Normal curve and use it to answer the following questions.

The mean of the population is 0.29. In what range will the middle 95% of all sample results fall?

What is the probability that the poll gets a sample in which fewer than 27.8% say the level of immigration to this country should be decreased?

18.21 Airplane safety. Suppose that 44% of all adults think that airline travel is safer than driving. An opinion poll plans to ask an SRS of 1021 adults about airplane safety. The proportion of the sample who think that airline travel is safer than driving will vary if we take many samples from this same population. The sampling distribution of the sample proportion is approximately Normal with mean 0.44 and standard deviation about 0.016. Sketch this Normal curve and use it to answer the following questions.

What is the probability that the poll gets a sample in which more than 40.8% of the people think that airline travel is safer than driving?

What is the probability of getting a sample that misses the truth (44%) by 3.2% or more?

18.22 Immigration (optional). In the setting of Exercise 18.20, what is the probability of getting a sample in which more than 30% of those sampled think that the level of immigration to this country should be decreased? (Use Table B.)

18.23 Airplane safety (optional). In the setting of Exercise 18.21, what is the probability of getting a sample in which more than 45% think that airline travel is safer than driving? (Use Table B.)

18.24 Do you jog? An opinion poll asks an SRS of 1500 adults,「Do you jog?」Suppose (as is approximately correct) that the population proportion who jog is In a large number of samples, the proportion who answer Yes will be approximately Normally distributed with mean 0.20 and standard deviation 0.01. Sketch this Normal curve and use it to answer the following questions.

What percentage of many samples will have a sample proportion who jog that is 0.20 or less? Explain clearly why this percentage is the probability that is 0.20 or less.

What is the probability that will take a value between 0.18 and 0.22? (Use the 68–95–99.7 rule.)

Now use Rule C to determine the following probability: what is the probability that does not lie between 0.18 and 0.22?

18.25 Applying to college. You ask an SRS of 1500 college students whether they applied for admission to any other college. Suppose that, in fact, 35% of all college students applied to colleges besides the one they are attending. (That’s close to the truth.) The sampling distribution of the proportion of your sample who say Yes is approximately Normal with mean 0.35 and standard deviation 0.01. Sketch this Normal curve and use it to answer the following questions.

Explain in simple language what the sampling distribution tells us about the results of our sample.

What percentage of many samples would have a larger than 0.37? (Use the 68–95–99.7 rule.) Explain in simple language why this percentage is the probability of an outcome larger than 0.37.

What is the probability that your sample will have a less than 0.33?

Use Rule D to answer the following question: what is the probability that your sample result will be either less than 0.33 or greater than 0.35?

18.26 Generating a sampling distribution. Let us illustrate the idea of a sampling distribution in the case of a very small sample from a very small population. The population is the scores of 10 students on an exam:

Student: 0 1 2 3 4 5 6 7 8 9

Score: 82 62 80 58 72 73 65 66 74 62

The parameter of interest is the mean score in this population. The sample is an SRS of size drawn from the population. Because the students are labeled 0 to 9, a single random digit from Table A chooses one student for the sample.

Find the mean of the 10 scores in the population. This is the population mean.

Use Table A, or software (see Example 3 in Chapter 2, page 25) to draw an SRS of size 4 from this population. Write the four scores in your sample and calculate the mean of the sample scores. This statistic is an estimate of the population mean.

Repeat this process 10 times using different parts of Table A or using software. Make a histogram of the 10 values of You are constructing the sampling distribution of Is the center of your histogram close to the population mean you found in part (a)?

18.27 Odds and personal probability. One way to determine your personal probability about an event is to ask what you would consider a fair bet that the event will occur. Suppose in August 2018 you believed it fair that a bet of $2 should win $10 if the Philadelphia Eagles win Super Bowl 53.

What does this bet say you believe the odds to be that the Philadelphia Eagles will win Super Bowl 53?

Convert the odds in part (a) to a probability. This would be your personal probability that the Philadelphia Eagles will win Super Bowl 53.

18.28 The addition rule (optional). Probability rule D states: If two events have no outcomes in common, the probability that one or the other occurs is the sum of their individual probabilities. This is sometimes called the addition rule for disjoint events. A more general form of the addition rule is: the probability that one or the other of two events occurs is the sum of their individual probabilities minus the probability that both occur. To verify this rule, suppose you roll two casino dice as in Example 2. Refer to the outcomes in Figure 18.1 to answer the following.

How many of the outcomes in Figure 18.1 have the sum of the spots on the up-faces equal to 6? What is the probability that the sum of the spots on the up-faces is 6?

How many of the outcomes in Figure 18.1 have at least one of the up-faces showing a single spot? What is the probability that at least one of the up-faces has only a single spot?

How many of the outcomes in Figure 18.1 have the sum of the spots on the up-faces equal to 6 and at least one of the up-faces showing a single spot? What is the probability that the sum of the spots on the up-faces is 6 and at least one of the up-faces has only a single spot?

How many of the outcomes in Figure 18.1 have either the sum of the spots on the up-faces equal to 6 or have at least one of the up-faces showing a single spot? What is the probability that the sum of the spots on the up-faces is either a 6 or at least one of the up-faces has a single spot?

The addition rule says that your answer to part (d) should be equal to the sum of your answers to parts (a) and (b) minus your answer to part (c). Verify that this is the case.

Note: The outcomes you were asked to count in part (c) are among those counted in parts (a) and (b). When we combine the outcomes in parts (a) and (b), we「double count」the outcomes in part (c). One of these「double counts」must be eliminated so that the combination corresponds to the outcomes in part (d). This is the reason that, in the addition rule, you subtract the probability that both occur from the sum of their individual probabilities.

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

What’s the Verdict?

On Tuesday, October 23, 2018, the Mega Millions lottery had a grand prize jackpot of $1.6 billion. This unusually large jackpot excited many people who would not normally buy tickets to play the game for the first time.

For the Mega Millions game, each player selects 6 numbers that they hope will match with those randomly selected by the company on the big night.

Figure 18.7 The odds of winning as posted on the Mega Millions website. Exercises WTV18.1 and WTV18.2.

The page has the ‘Mega Millions’ logo toward the top-left corner, followed by a navigation menu, and content of the website. A table shows the odds of winning in the center of the website.

According to the Mega Millions website: http://www.megamillions.com/how-to-play, the odds of winning the jackpot and some lesser prizes are listed below.

Questions

WTV18.1. Do you have a better chance of winning if you play the birthdates of everybody in your family instead of letting a machine at the convenience store where you purchase your ticket pick 6 random numbers for you? Why or why not?

WTV18.2. Make a valid probability model for all the possible outcomes and their probabilities (leave the probabilities as fractions). Don’t forget to include the possibility of not winning anything. Explain why this is a valid probability model.

CHAPTER 19 Simulation

In this chapter you will:

