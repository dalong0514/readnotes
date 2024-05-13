Compute the long-run average outcome of a random phenomenon with numerical outcomes.

Compare games of chance that have huge jackpots but small chances of winning with games with more modest jackpots but more reasonable chances of winning.

Case Study: Better Betting?

If you gamble, you care about how often you will win. The probability of winning tells you what proportion of a large number of bets will be winners. You care even more about how much you will win because winning a lot is better than winning a little.

There are a lot of ways to gamble. You can play games, like some of the multistate lotteries, that have enormous jackpots but very small probabilities of winning. You can play games like roulette for which the probability of winning is much larger than for a multistate lottery, but with smaller jackpots. Which is the better gamble: an enormous jackpot with extremely small odds or a modest jackpot with more reasonable odds? By the end of this chapter, you will be able to determine whether buying a multistate lottery ticket or simply playing red in roulette is a better bet.

Expected Values

Gambling on chance outcomes goes back to ancient times and has continued throughout history. Both public and private lotteries were common in the early years of the United States. After disappearing for a century or so, government-run gambling reappeared in 1964, when New Hampshire caused a furor by introducing a lottery to raise public revenue without raising taxes. The furor subsided quickly as larger states adopted the idea. Forty-two states and all Canadian provinces now sponsor lotteries. State lotteries made gambling acceptable as entertainment. Some form of legal gambling is allowed in 48 of the 50 states. More than half of all adult Americans have gambled legally. They spend more betting than on spectator sports, video games, theme parks, and movie tickets combined. If you are going to bet, you should understand what makes a bet good or bad. As our introductory Case Study says, we care about how much we win as well as about our probability of winning.

Example 1

The DC Lottery

Here is a simple lottery wager: the「Straight」from the DC-3 game of the DC Lottery offered by Washington, DC. You pay $1.00 and choose a three-digit number. The lottery chooses a three-digit winning number at random and pays you $500 if your number is chosen. Because there are 1000 three-digit numbers, you have probability 1-in-1000 of winning. Here is the probability model for your winnings:

Outcome: $0 $500

Probability: 0.999 0.001

What are your average winnings? The ordinary average of the two possible outcomes $0 and $500 is $250, but that makes no sense as the average winnings because $500 is much less likely than $0. In the long run, you win $500 once in every 1000 bets and $0 on the remaining 999 of 1000 bets. (Of course, if you play the game regularly, buying one ticket each time you play, after you have bought exactly 1000 DC-3 tickets, there is no guarantee that you will win exactly once. Probabilities are only long-run proportions.) Your long-run average winnings from a ticket are

or 50 cents. You see that in the long run the state pays out one-half of the money bet and keeps the other half.

Key Terms

The expected value of a random phenomenon that has numerical outcomes is found by multiplying each outcome by its probability and then adding all the products.

In symbols, if the possible outcomes are , , … , and their probabilities are , , … , , the expected value is

Here is a general definition of the kind of「average outcome」we used to evaluate the bets in Example 1.

An expected value is an average of the possible outcomes, but it is not an ordinary average in which all outcomes get the same weight. Instead, each outcome is weighted by its probability so that outcomes that occur more often get higher weights.

Example 2

The DC Lottery, continued

The Straight wager in Example 1 pays off if you match the three-digit winning number exactly. You can choose instead to make a $1 Straight/Box-6 way wager. You again choose a three-digit number, but you must choose one with all three digits different. You now have two ways to win. You win $290 if you exactly match the winning number, and you win $40 if your number has the same digits as the winning number, in any order. For example, if your number is 123, you win $290 if the winning number is 123 and $40 if the winning number is any of 132, 213, 231, 312, and 321. In the long run, you win $290 once every 1000 bets and $40 five times for every 1000 bets.

The probability model for the amount you win is

Outcome: $0 $40 $290

Probability: 0.994 0.005 0.001

The expected value is

We see that the Straight/Box-6 bet is a slightly worse bet than the Straight bet because the state pays out slightly less than half the money bet.

The DC Lottery is an example of one type of lottery game in that it pays a fixed amount for each type of bet. Other states pay off on the「pari-mutuel」system. New Jersey’s Pick 3 game is typical: the state pools the money bet and pays out half of it, equally divided among the winning tickets. You still have probability 1-in-1000 of winning a Straight bet, but the amount your number 123 wins depends both on how much was bet on Pick 3 that day and on how many other players chose the number 123. Without fixed amounts, we can’t find the expected value of today’s bet on 123, but one thing is constant: the state keeps half the money bet.

The idea of expected value as an average applies to random outcomes other than games of chance. It is used, for example, to describe the uncertain return from buying stocks or building a new factory. Here is a different example.

Example 3

How many vehicles per household?

What is the average number of motor vehicles in American households? The U.S. Energy Information Administration tells us that the distribution of vehicles per household (2017) is as follows:

Number of vehicles: 0 1 2 3 4 5 6

Proportion of households: 0.09 0.34 0.33 0.15 0.06 0.02 0.01

This is a probability model for choosing a household at random and counting its vehicles. (We ignored the very few households with more than six vehicles.) The expected value for this model is the average number of vehicles per household. This average is

expected value = (0)(0.09) (1)(0.34) (2)(0.33) (3)(0.15) (4)(0.06) (5)(0.02) (6)(0.01) = 1.85 vehicles per household

Now it’s your turn

20.1 Number of children. The Census Bureau gives this distribution for the number of a family household’s related children under the age of 18 in American households in 2016:

Number of children: 0 1 2 3 4

Proportion: 0.58 0.18 0.16 0.06 0.02

In this table, 4 actually represents 4 or more (the Census Bureau does not provide separate information on households with 5, 6, or more children under the age of 18). But for purposes of this exercise, assume that it means only households with exactly four children under the age of 18. This is also the probability distribution for the number of children under 18 in a randomly chosen household. The expected value of this distribution is the average number of children under 18 in a household. What is this expected value?

The Law of Large Numbers

Key Terms

According to the law of large numbers, if a random phenomenon with numerical outcomes is repeated many times independently, the mean of the actually observed outcomes approaches the expected value.

The definition of「expected value」says that it is an average of the possible outcomes, but an average in which outcomes with higher probability count more. We argued that the expected value is also the average outcome in another sense—it represents the long-run average we will actually see if we repeat a bet many times or choose many households at random. This is more than intuition. Mathematicians can prove, starting from just the basic rules of probability, that the expected value calculated from a probability model really is the「long-run average.」This famous fact is called the law of large numbers.

The law of large numbers is closely related to the idea of probability. In many independent repetitions, the proportion of each possible outcome will be close to its probability, and the average outcome obtained will be close to the expected value. These facts express the long-run regularity of chance events. They are the true version of the「law of averages,」as we mentioned in Chapter 17.

Statistics in Your World

Rigging the lottery We have all seen televised lottery drawings in which numbered balls bubble about and are randomly popped out by air pressure. How might we rig such a drawing? In 1980, the Pennsylvania lottery was rigged by the host and several stagehands. They injected paint into all balls bearing 8 of the 10 digits. This weighed them down and guaranteed that all 3 balls for the winning number would have the remaining two digits. The perps then bet on all combinations of these digits. When 6-6-6 popped out, they won $1.2 million. Yes, they were caught.

The law of large numbers explains why gambling, which is a recreation or an addiction for individuals, is a business for a casino. The「house」in a gambling operation is not gambling at all. The average winnings of a large number of customers will be quite close to the expected value. The house has calculated the expected value ahead of time and knows what its take will be in the long run. There is no need to load the dice or stack the cards to guarantee a profit. Casinos concentrate on inexpensive entertainment and cheap bus trips to keep the customers flowing in. If enough bets are placed, the law of large numbers guarantees the house a profit. Life insurance companies operate much like casinos—they bet that the people who buy insurance will not die. Some do die, of course, but the insurance company knows the probabilities and relies on the law of large numbers to predict the average amount it will have to pay out. Then the company sets its premiums high enough to guarantee a profit.

Thinking about Expected Values

As with probability, it is worth exploring a few fine points about expected values and the law of large numbers.

How large is a large number? The law of large numbers says that the actual average outcome of many trials gets closer to the expected value as more trials are made. It doesn’t say how many trials are needed to guarantee an average outcome close to the expected value. That depends on the variability of the random outcomes.

Statistics in Your World

High-tech gambling There are more than 700,000 slot machines in the United States. Once upon a time, you put in a coin and pulled the lever to spin three wheels, each with 20 symbols. No longer. Now the machines are video games with flashy graphics and outcomes produced by random number generators. Machines can accept many coins at once, can pay off on a bewildering variety of outcomes, and can be networked to allow common jackpots. Gamblers still search for systems, but in the long run, the random number generator guarantees the house its 5% profit.

The more variable the outcomes, the more trials are needed to ensure that the mean outcome is close to the expected value. Games of chance must be quite variable if they are to hold the interest of gamblers. Even a long evening in a casino has an unpredictable outcome. Gambles with extremely variable outcomes, like state lottos with their very large but very improbable jackpots, require impossibly large numbers of trials to ensure that the average outcome is close to the expected value. (The state doesn’t rely on the law of large numbers—most lotto payoffs, unlike casino games, use the pari-mutuel system. In a pari-mutuel system, payoffs and payoff odds are determined by the actual amounts bet. In state lottos, for example, the payoffs are determined by the total amount bet after the state removes its share. In horse racing, payoff odds are determined by the relative amounts bet on the different horses.)

Though most forms of gambling are less variable than the lotto, the practical answer to the applicability of the law of large numbers is that the expected value of the winnings for the house is positive and the house plays often enough to rely on it. Your problem is that the expected value of your winnings is negative. As a group, gamblers play as often as the house. Because their expected value is negative, as a group they lose money over time. However, this loss is not spread evenly among the many individual gamblers. Some win big, some lose big, and some break even. Much of the psychological allure of gambling is its unpredictability for the player. The business of gambling rests on the fact that the result is not unpredictable for the house.

STATISTICAL CONTROVERSIES

The State of Legalized Gambling

Most voters think that some forms of gambling should be legal, and the voting majority has its way: lotteries and casinos are common both in the United States and in other nations. The arguments in favor of allowing gambling are straightforward. Many people find betting entertaining and are willing to lose a bit of money in exchange for some excitement. Gambling doesn’t harm other people, at least not directly. A democracy should allow entertainment that a majority supports and that doesn’t do harm. State lotteries raise money for good causes such as education and are a kind of voluntary tax that no one is forced to pay.

These are some of the arguments for legalized gambling. What are some of the arguments against legalized gambling? Ask yourself, from which socioeconomic class do people who tend to play the lottery come, and hence who bears the burden for this「voluntary tax」? For more information, see the sources listed in the Notes and Data Sources at the end of this chapter.

Is there a winning system? Serious gamblers often follow a system of betting in which the amount bet on each play depends on the outcome of previous plays. You might, for example, double your bet on each spin of the roulette wheel until you win—or, of course, until your fortune is exhausted. Such a system tries to take advantage of the fact that you have a memory even though the roulette wheel does not. Can you beat the odds with a system? No. Mathematicians have established a stronger version of the law of large numbers that says that if you do not have an infinite fortune to gamble with, your average winnings (the expected value) remain the same as long as successive trials of the game (such as spins of the roulette wheel) are independent. Sorry.

You now have enough information to read the「What’s the verdict?」story on page 475, and to answer the six questions.

Finding Expected Values by Simulation

How can we calculate expected values in practice? You know the mathematical recipe, but that requires that you start with the probability of each outcome. Expected values that are too difficult to compute in this way can be found by simulation. The procedure is as before: give a probability model, use random digits to imitate it, and simulate many repetitions. By the law of large numbers, the average outcome of these repetitions will be close to the expected value.

Example 4

We want a girl, again

A couple plan to have children until they have a girl or until they have three children, whichever comes first. We simulated 10 repetitions of this scheme in Example 4 of Chapter 19 (page 450). There, we estimated the probability that they will have a girl among their children. Now we ask a different question: how many children, on the average, will couples who follow this plan have? That is, we want the expected number of children.

The simulation is exactly as before. The probability model says that the sexes of successive children are independent and that each child has probability 0.49 of being a girl. Here are our earlier simulation results—but rather than noting whether the couple did have a girl, we now record the number of children they have. Recall that a pair of digits simulates one child, with 00 to 48 (probability 0.49) standing for a girl.

6905 16 48 17 8717 40 9517 845340 648987 20

B G G G G B G G B G B B G B B B G

2 1 1 1 2 1 2 3 3 1

The mean number of children in these 10 repetitions is

We estimate that if many couples follow this plan, they will average 1.7 children each. This simulation is too short to be trustworthy. Math or a long simulation shows that the actual expected value is 1.77 children.

Now it’s your turn

20.2 Stephen Curry’s three-point shooting. Stephen Curry makes about 44% of the three-point shots that he attempts. On average, how many three-point shots must he take in a game before he makes his first shot? In other words, we want the expected number of shots he takes before he makes his first. Estimate this by using 10 simulations of sequences of shots, stopping when he makes his first. Use Example 4 to help you set up your simulation. What is your estimate of the expected value?

Chapter 20 Summary and Exercises

Chapter 20: Statistics in Summary

The expected value is found as an average of all the possible outcomes, each weighted by its probability.

When the outcomes are numbers, as in games of chance, we are often interested in the long-run average outcome. The law of large numbers says that the mean outcome in many repetitions eventually gets close to the expected value.

If you don’t know the outcome probabilities, you can estimate the expected value (along with the probabilities) by simulation.

This chapter summary will help you evaluate the Case Study.

Link It

In Chapter 17, we discussed the law of averages, both incorrect and correct interpretations. The correct interpretation is sometimes referred to as the law of large numbers. In this chapter, we formally state the law of averages and its relation to the expected value. Understanding the law of large numbers and expected values is helpful in understanding the behavior of games of chance, including state lotteries. Expected values provide a way you can compare games of chance with huge jackpots but small chances of winning with games with more modest jackpots but more reasonable chances of winning.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study that opened the chapter. Start by reviewing the Chapter Summary. Then answer each of the following questions in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying.

An American roulette wheel has 38 slots, of which 18 are black, 18 are red, and 2 are green. When the wheel is spun, the ball is equally likely to come to rest in any of the slots. A bet of $1 on red will win $2 (and you will also get back the $1 you bet) if the ball lands in a red slot. (When gamblers bet on red or black, the two green slots belong to the house.) Give a probability model for the winnings of a $1 bet on red and find the expected value of this bet.

The website for the Powerball lottery game gives the following table for the various prizes and the probability of winning:

Prize: Jackpot $1,000,000 $50,000 $100 $100

Probability: 1 in 292,201,338 1 in 11,688,054 1 in 913,129 1 in 36,525 1 in 14,494

Prize: $7 $7 $4 $4

Probability: 1 in 580 1 in 701 1 in 92 1 in 38

The jackpot always starts at $40 million for the cash payout for a $2 ticket and grows each time there is no winner. What is the expected value of a $2 bet when the jackpot is $40 million? If there are multiple winners, they share the jackpot, but for purposes of this problem, ignore this.

Do you think roulette or the Powerball is the better game to play? Discuss.

In this chapter you have:

Computed the long-run average outcome of a random phenomenon with numerical outcomes by computing the expected value.

Compared games of chance that have huge jackpots but small chances of winning with games with more modest jackpots but more reasonable chances of winning by comparing the expected value of the winnings.

Online Resources

LearningCurve has good questions to check your understanding of the concepts.

Check the Basics

For Exercise 20.1, see page 464; for Exercise 20.2, see page 468.

20.3 Expected value. Which of the following is true of the expected value of a random phenomenon?

It must be one of the possible outcomes.

It cannot be one of the possible outcomes because it is an average.

It can only be computed if the random phenomenon has numerical values.

It is the outcome that has the highest probability of occurring.

20.4 Expected value. The expected value of a random phenomenon that has numerical outcomes is

the outcome that occurs with the highest probability.

the outcome that occurs more often than not in a large number of trials.

the average of all possible outcomes.

the average of all possible outcomes, each weighted by its probability.

20.5 Expected value. You flip a coin for which the probability of heads is 0.5 and the probability of tails is 0.5. If the coin comes up heads, you win $1. Otherwise, you lose $1. The expected value of your winnings is

$0.

$1.

−$1.

$0.5.

20.6 The law of large numbers. The law of large numbers says that the mean outcome in many repetitions of a random phenomenon having numerical outcomes

gets close to the expected value as the number of repetitions increases.

goes to zero as the number of repetitions increases because, eventually, positive and negative outcomes balance.

increases steadily as the number of repetitions increases.

must always be a number between 0 and 1.

20.7 The law of large numbers. I simulate a random phenomenon that has numerical outcomes many, many times. If I average together all the outcomes I observe, this average

should be close to the probability of the random phenomenon.

should be close to the expected value of the random phenomenon.

should be close to the sampling distribution of the random phenomenon.

should be close to 0.5.

Chapter 20 Exercises

20.8 The numbers racket. Pick 3 lotteries (Example 1) copy the numbers racket, an illegal gambling operation common in the poorer areas of large cities. States usually justify their lotteries by donating a portion of the proceeds to education. One version of a numbers racket operation works as follows. You choose any one of the 1000 three-digit numbers 000 to 999 and pay your local numbers runner $1 to enter your bet. Each day, one three-digit number is chosen at random and pays off $600. What is the expected value of a bet on the numbers? Is the numbers racket more or less favorable to gamblers than the Pick 3 game in Example 1?

20.9 DC-4. The「Straight」DC-4 lottery game is much like the「Straight」DC-3 game of Example 1. Winning numbers for both are reported on television and in local newspapers. You pay $1.00 and pick a four-digit number. The state chooses a four-digit number at random and pays you $5000 if your number is chosen. What are the expected winnings from a $1.00 Straight DC-4 wager?

20.10 More DC-3. There are other elaborate versions of DC-3 (Example 2). In the $1 Straight-Box (3-way) bet, if you choose a number with two digits the same, for example, 112, you win $330 if the randomly chosen winning number is 112, and you win $80 if the winning number has the digits 1, 1, and 2 in any other order (there are 2 such other orders, namely 121 and 211). What is the expected amount you win?

20.11 More roulette. An American roulette wheel has 38 slots, of which 18 are black, 18 are red, and 2 are green. When the wheel is spun, the ball is equally likely to come to rest in any of the slots. Gamblers bet on roulette by placing chips on a table that lays out the numbers and colors of the 38 slots in the roulette wheel. The red and black slots are arranged on the table in three columns of 12 slots each. A $1 column bet wins $3 if the ball lands in one of the 12 slots in that column. What is the expected amount such a bet wins? If you did the Case Study Evaluated, is a column bet more or less favorable to a gambler than a bet on red or black (see Question 1 in the Case Study Evaluated on page 469)?

20.12 Making decisions. The psychologist Amos Tversky did many studies of our perception of chance behavior. In its obituary of Tversky, the New York Times cited the following example.

Tversky asked subjects to choose between two public health programs that affect 600 people. The first has probability 1/2 of saving all 600 and probability 1/2 that all 600 will die. The other is guaranteed to save exactly 400 of the 600 people. Find the expected number of people saved by the first program.

Tversky then offered a different choice. One program has probability 1/2 of saving all 600 and probability 1/2 of losing all 600, while the other is guaranteed to lose exactly 200 of the 600 lives. What is the difference between this choice and that in part (a)?

Given the options in part (a), most subjects choose the second program. Given the options in part (b), most subjects choose the first program. Do the subjects appear to use expected values in their choice? Why do you think the choices differ in parts (a) and (b)?

20.13 Making decisions. A six-sided die has two green and four red faces and is balanced so that each face is equally likely to come up. You must choose one of the following three sequences of colors:

RGRRR

RGRRRG

GRRRRR

Now start rolling the die. You will win $25 if the first rolls give the sequence you chose.

Which sequence has the highest probability? Why? (You can see which is most probable without actually finding the probabilities.) Because the $25 payoff is fixed, the most probable sequence has the highest expected value.

In a psychological experiment, 63% of 260 students who had not studied probability chose the second sequence. Based on the discussion of「myths about chance behavior」in Chapter 17, explain why most students did not choose the sequence with the best chance of winning.

20.14 Estimating sales. Gain Communications sells aircraft communications units. Next year’s sales depend on market conditions that cannot be predicted exactly. Gain follows the modern practice of using probability estimates of sales. The sales manager estimates next year’s sales as follows:

Units sold: 6,000 7,000 8,000 9,000 10,000

Probability: 0.1 0.2 0.4 0.2 0.1

These are personal probabilities that express the informed opinion of the sales manager. What is the sales manager’s expected value of next year’s sales?

20.15 Keno. Keno is a popular game in casinos. Balls numbered 1 to 80 are tumbled in a machine as the bets are placed, then 20 of the balls are chosen at random. Players select numbers by marking a card. Here are two of the simpler Keno bets. Give the expected winnings for each.

A $1 bet on「Mark 1 number」pays $3 if the single number you mark is one of the 20 chosen; otherwise, you lose your dollar.

A $1 bet on「Mark 2 numbers」pays $12 if both your numbers are among the 20 chosen. The probability of this is about 0.06. Is Mark 2 a more or a less favorable bet than Mark 1?

20.16 Rolling two dice. Example 2 of Chapter 18 (page 428) gives a probability model for rolling two casino dice and recording the number of spots on each of the two up-faces. That example also shows how to find the probability that the total number of spots showing is five. Follow that method to give a probability model for the total number of spots. The possible outcomes are 2, 3, 4, … , 12. Then use the probabilities to find the expected value of the total.

20.17 The Asian stochastic beetle. We met this insect in Exercise 19.21 (page 457). Females have this probability model for their number of female offspring:

Offspring: 0 1 2

Probability: 0.2 0.3 0.5

What is the expected number of female offspring?

Use the law of large numbers to explain why the population should grow if the expected number of female offspring is greater than 1 and die out if this expected value is less than 1.

20.18 An expected rip-off? A「psychic」runs the following ad in a magazine:

Expecting a baby? Renowned psychic will tell you the sex of the unborn child from any photograph of the mother. Cost, $20. Money-back guarantee.

This may be a profitable con game. Suppose that the psychic simply replies「boy」to all inquiries. In the worst case, everyone who has a girl will ask for her money back. Find the expected value of the psychic’s profit by filling in the table below.

Sex of child Probability The psychic’s profit

Boy 0.51

Girl 0.49

20.19 The Asian stochastic beetle again. In Exercise 20.17, you found the expected number of female offspring of the Asian stochastic beetle. Simulate the offspring of 100 beetles and find the mean number of offspring for these 100 beetles. Compare this mean with the expected value from Exercise 20.17. (The law of large numbers says that the mean will be very close to the expected value if we simulate enough beetles.)

20.20 Life insurance. You might sell insurance to a 20-year-old friend. The probability that a man aged 20 will die in the next year is about 0.0007. You decide to charge $2000 for a policy that will pay $1 million if your friend dies.

What is your expected profit on this policy?

Although you expect to make a good profit, you would be foolish to sell a single policy only to your friend. Why?

A life insurance company that sells thousands of policies, on the other hand, would do very well selling policies on exactly these same terms. Explain why.

20.21 Household size. The Census Bureau gives this distribution for the number of people in American households in 2016:

Family size: 1 2 3 4 5 6 7

Proportion: 0.28 0.35 0.15 0.13 0.06 0.02 0.01

(Note: In this table, 7 actually represents households of size 7 or greater. But for purposes of this exercise, assume that it means only households of size exactly 7.)

This is also the probability distribution for the size of a randomly chosen household. The expected value of this distribution is the average number of people in a household. What is this expected value?

Suppose you take a random sample of 1000 American households. About how many of these households will be of size 2? Sizes 3 to 7?

Based on your calculations in part (b), how many people are represented in your sample of 1000 households? (Hint: The number of individuals in your sample who live in households of size 7 is 7 times the number of households of size 7. Repeat this reasoning to determine the number of individuals in households of sizes 2 to 6. Add the results to get the total number of people represented in your sample.)

Calculate the probability distribution for the household size lived in by individual people. Describe the shape of this distribution. What does this shape tell you about household structure?

20.22 An easy A. The distribution of grades in an easy introductory statistics course is as follows:

Grade: A B C D F

Probability: 0.4 0.3 0.2 0.1 0.0

To calculate student grade point averages, grades are expressed in a numerical scale with A = 4, B = 3, and so on down to F = 0.

Find the expected value. This is the average grade in this course.

Explain how to simulate choosing students at random and recording their grades. Simulate 50 students and find the mean of their 50 grades. Compare this estimate of the expected value with the exact expected value from part (a). (The law of large numbers says that the estimate will be very accurate if we simulate a very large number of students.)

20.23 We really want a girl. Example 4 estimates the expected number of children a couple will have if they keep going until they get a girl or until they have three children. Suppose that they set no limit on the number of children but just keep going until they get a girl. Their expected number of children must now be higher than in Example 4. How would you simulate such a couple’s children? Simulate 25 repetitions. What is your estimate of the expected number of children?

20.24 Play this game, please. OK, friends, we’ve got a little deal for you. We have a fair coin (heads and tails each have probability 0.5). Toss it twice. If two heads come up, you win right there. If you get any result other than two heads, we’ll give you another chance: toss the coin twice more, and if you get two heads, you win. (Of course, if you fail to get two heads on the second try, we win.) Pay us a dollar to play. If you win, we’ll give you your dollar back plus another dollar.

Make a tree diagram for this game. Use the diagram to explain how to simulate one play of this game.

Your dollar bet can win one of two amounts: 0 if we win and $2 if you win. Simulate 50 plays, using Table A, starting at line 125. Use your simulation to estimate the expected value of the game.

20.25 A multiple-choice exam. Charlene takes a quiz with 10 multiple-choice questions, each with five answer choices. If she just guesses independently at each question, she has probability 0.20 of guessing right on each. Use simulation to estimate Charlene’s expected number of correct answers. (Simulate 20 repetitions.)

20.26 Repeating an exam. Exercise 19.19 (page 457) gives a model for up to three attempts at an exam in a self-paced course. In that exercise, you simulated 50 repetitions to estimate Elaine’s probability of passing the exam. Use those simulations (or do 50 new repetitions) to estimate the expected number of tries Elaine will make.

20.27 A common expected value. Here is a common setting that we simulated in Chapter 19: there are a fixed number of independent trials with the same two outcomes and the same probabilities on each trial. Tossing a coin, shooting basketball free throws, and observing the sex of newborn babies are all examples of this setting. Call the outcomes「hit」and「miss.」We can see what the expected number of hits should be. If Stephen Curry shoots 12 three-point shots and has probability 0.44 of making each one, the expected number of hits is 44% of 12, or 5.28. By the same reasoning, if we have trials with probability of a hit on each trial, the expected number of hits is . This fact can be proved mathematically. Can we verify it by simulation?

Simulate 10 tosses of a fair coin 50 times. (To do this quickly, use the first 10 digits in each of the 50 rows of Table A, with odd digits meaning a head and even digits a tail.) What is the expected number of heads by the formula? What is the mean number of heads in your 50 repetitions?

20.28 Casino winnings. What is a secret, at least to naive gamblers, is that in the real world, a casino does much better than expected values suggest. In fact, casinos keep a bit over 20% of the money gamblers spend on roulette chips. That’s because players who win keep on playing. Think of a player who gets back exactly 95% of each dollar bet. After one bet, he has 95 cents.

After two bets, how much does he have of his original dollar bet? (Hint: This will be 95% of the 95 cents he has after the first bet.)

After three bets, how much does he have of his original dollar bet?

Notice that the longer he keeps recycling his original dollar, the more of it the casino keeps. Real gamblers don’t get a fixed percentage back on each bet, but even the luckiest will lose his stake if he plays long enough. The casino keeps 5.3 cents of every individual one-dollar bet but a total of 20 cents of every dollar spent on betting (due to recycling of the original bet).

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

What’s the Verdict?

On Tuesday October 23, 2018, the Mega Millions lottery had a grand prize jackpot of $1.6 billion. This unusually large prize excited many people who would not normally buy tickets to play this lottery for the first time.

For the Mega Millions game, each player selects six numbers that they hope will match with those randomly selected by the company on the big night.

According to the Mega Millions website: http://www.megamillions.com/how-to-play , the odds of winning the jackpot and some lesser prizes are listed in Figure 18.7.

Questions

WTV20.1. Find the expected value for the outcome of playing one ticket (for now, ignore the cost of the ticket and ignore the possibility of multiple jackpot winners). Use the following table based on a jackpot of $1.6 billion.

Outcome: +$1,600,000,000 +$1,000,000

Probability: 1/302,575,350 1/12,607,306

Outcome: +$10,000 +$500 +$200

Probability: 1/931,001 1/38,792 1/14,547

Outcome: +$10 +$10 +$4 +$2 $0

Probability: 1/606 1/693 1/89 1/37 23/24

WTV20.2. If each lottery ticket costs $2, what is your expected value of the difference in your wallet? (Hint: You do not have to start over with a new table or long calculation. Use your previous expected value work and the new $2 ticket cost to do a simple calculation.)

WTV20.3. Using the expected value of the difference in your wallet, does this seem like a game that would favor you winning something? Why?

WTV20.4. Jackpots for the Mega Millions start at $40 million and grow each time there is no winner. What is the expected value in your wallet if the jackpot is $40 million? Repeat the calculations you did above for the $1.6 billion jackpot using the following table.

Outcome: +$40,000,000 +$1,000,000 +$10,000

Probability: 1/302,575,350 1/12,607,306 1/931,001

Outcome: +$500 +$200 +$10

Probability: 1/38,792 1/14,547 1/606

Outcome: +$10 +$4 +$2 $0

Probability: 1/693 1/89 1/37 23/24

WTV20.5. (This is a more challenging question.) What value does the jackpot need to be for the expected value in your wallet to be 0? (Ignore the possibility of splitting the jackpot if there are multiple winners.)

WTV20.6. Do you want to play the Mega Millions? Why or why not?

PART III Review

Some phenomena are random. That is, although their individual outcomes are unpredictable, there is a regular pattern in the long run. Gambling devices (rolling dice, spinning roulette wheels) and taking a simple random sample (SRS) are examples of random phenomena. Probability and expected value give us a language to describe randomness. Random phenomena are not haphazard or chaotic any more than random sampling is haphazard. Randomness is instead a kind of order in the world, a long-run regularity as opposed to either chaos or a determinism that fixes events in advance. Chapter 17 discusses the idea of randomness, Chapter 18 presents basic facts about probability, Chapter 19 shows how to use simulation to estimate probabilities, and Chapter 20 discusses expected values.

When randomness is present, probability answers the question,「How often in the long run?」and expected value answers the question,「How much on the average in the long run?」The two answers are connected because「expected value」is defined in terms of probabilities. Much work with probability starts with a probability model that assigns probabilities to the basic outcomes. Any such model must obey the rules of probability. Another example of a probability model uses a density curve such as a Normal curve to assign probabilities as areas under the curve. Personal probabilities express an individual’s judgment of how likely some event is. Personal probabilities for several possible outcomes must also follow the rules of probability if they are to be consistent with each other.

To calculate the probability of a complicated event without using complicated math, we can use random digits to simulate many repetitions. You can also find expected values by simulation. Chapter 19 shows how to do simulations. First, give a probability model for the outcomes, then assign random digits to imitate the assignment of probabilities. The table of random digits now imitates repetitions. Keep track of the proportion of repetitions on which an event occurs to estimate its probability. Keep track of the mean outcome to estimate an expected value.

Part III Summary and Exercises

PART III SUMMARY

Here are the most important skills you should have acquired after reading Chapters 17 through 20.

A. RANDOMNESS AND PROBABILITY

Recognize that some phenomena are random. Understand that probability describes the long-run regularity of random phenomena.

Understand the idea of the probability of an event as the proportion of times the event occurs in very many repetitions of a random phenomenon. Use the idea of probability as long-run proportion to think about probability.

Recognize that short runs of random phenomena do not display the regularity described by probability. Understand that randomness is unpredictable in the short run. Avoid seeking causal explanations for random occurrences.

B. PROBABILITY MODELS

Use basic probability facts to detect illegitimate assignments of probability: any probability must be a number between 0 and 1, and the sum of the probabilities assigned to all possible outcomes must be 1.

Use basic probability facts to find the probabilities of events that are formed from other events: the probability that an event does not occur is 1 minus its probability. If two events cannot occur at the same time, the probability that one or the other occurs is the sum of their individual probabilities.

When probabilities are assigned to individual outcomes, find the probability of an event by adding the probabilities of the outcomes that make it up.

When probabilities are assigned by a Normal curve, find the probability of an event by finding an area under the curve.

C. SIMULATION

Specify simple probability models that assign probabilities to each of several stages when the stages are independent of each other.

Assign random digits to simulate such models.

Estimate either a probability or an expected value by repeating a simulation many times.

D. EXPECTED VALUE

Understand the idea of expected value as the average of numerical outcomes in very many repetitions of a random phenomenon.

Find the expected value from a probability model that lists all outcomes and their probabilities (when the outcomes are numerical).

PART III REVIEW EXERCISES

Review exercises are short and straightforward exercises that help you solidify the basic ideas and skills in each part of this book. We have provided「hints」that indicate where you can find the relevant material for the odd-numbered problems.

III.1 What’s the probability? Find an online directory with at least 100 different phone numbers. Look at the last four digits of each telephone number, the digits that specify an individual number within an exchange given by the first three digits. Note the first of these four digits in each of the first 100 telephone numbers in the directory.

Three directories we found online were at education.ohio.gov/Contact/Phone-Directory, cityfone.lacity.org/department_drilldown.cfm?SECT=a, and www.somervillema.gov/staff-contact-directory. State government agencies often have directories with office phone numbers of employees. (If you happen to have access to a printed directory, you can use that instead of an online directory.)

How many of the digits are 1, 2, or 3? What is the approximate probability that the first of the four「individual digits」in a telephone number is 1, 2, or 3? (Hint: See page 407.)

If all 10 possible digits had the same probability, what would be the probability of getting a 1, 2, or 3? Based on your work in part (a), do you think the first of the four「individual digits」in telephone numbers is equally likely to be any of the 10 possible digits? (Hint: See page 427.)

III.2 Eye colors. Choose a person at random and record his or her eye colors. Here are the probabilities for each eye color:

Eye color: Brown Blue Hazel/amber Other

Probability: 0.7 0.1 0.1 ?

What must be the probability that a randomly chosen person has a color other than brown, blue, hazel, or amber?

To simulate the eye colors of randomly chosen people, how would you assign digits to represent the four types?

III.3 Grades in an economics course. Indiana University posts the grade distributions for its courses online. Students in Economics 201 in the spring 2018 semester received the following: 1% A+, 7% A, 8% A–, 8% B+, 16% B, 14% B–, 10% C+, 13% C, 6% C–, 5% D+, 4% D, 3% D–. Choose an Economics 201 student at random. The probabilities for the student’s grade are the following:

Grade A + A A – B+ B B–

Probability 0.01 0.07 0.08 0.08 0.16 0.14

Grade C+ C C– D+ D D– F

Probability 0.10 0.13 0.06 0.05 0.04 0.03 ?

What must be the probability of getting an F? (Hint: See page 427.)

To simulate the grades of randomly chosen students, how would you assign digits to represent the five possible outcomes listed? (Hint: See page 450.)

III.4 Eye colors. Tyra has amber eyes. What is the probability that one or more of Tyra’s six close friends has amber- or hazel-colored eyes? Using your work in Exercise III.2, simulate 10 repetitions and estimate this probability. (Your estimate from just 10 repetitions isn’t reliable, but you have shown in principle how to find the probability.)

III.5 Grades in an economics course. If you choose four students at random from all those who have taken the course described in Exercise III.3, what is the probability that all the students chosen got a B or better? Simulate 10 repetitions of this random choosing and use your results to estimate the probability. (Your estimate from only 10 repetitions isn’t reliable, but if you can do 10, you could do 10,000.) (Hint: See page 450.)

III.6 Grades in an economics course. Choose a student at random from the course described in Exercise III.3 and observe what grade that student earns (with A+ = 4.3, A = 4.0, A− = 3.7, B+ = 3.3, B = 3.0, B− = 2.7, C+ = 2.3, C = 2.0, C− = 1.7, D+ = 1.3, D = 1.0, D− = 0.7, and F = 0.0).

What is the expected grade of a randomly chosen student?

The expected grade is not one of the 12 grades possible for one student. Explain why your result nevertheless makes sense as an expected value.

III.7 Dice. What is the expected number of spots observed in rolling a carefully balanced die once? (Hint: See page 463.)

III.8 Profit from a risky investment. Rotter Partners is planning a major investment. The amount of profit is uncertain, but a probabilistic estimate gives the following distribution (in millions of dollars):

Profit: −1 0 1 2 3 5 20

Probability: 0.1 0.1 0.2 0.2 0.2 0.1 0.1

What is the expected value of the profit?

III.9 Poker. Deal a five-card poker hand from a shuffled deck. The probabilities of several types of hand are approximately as follows:

Hand: Worthless One pair Two pairs Better hands

Probability: 0.50 0.42 0.05 ?

What must be the probability of getting a hand better than two pairs? (Hint: See page 427.)

What is the expected number of hands a player is dealt before the first hand better than one pair appears? Explain how you would use simulation to answer this question, then simulate just two repetitions. (Hint: See page 450.)

III.10 How much education? The Census Bureau gives this distribution of the highest level of education attained for a randomly chosen American over 25 years old in 2014:

Education: Less than high school High school graduate College, no bachelor’s

Probability: 0.104 0.288 0.163

Education: Associate’s degree Bachelor’s degree Advanced degree

Probability: 0.103 0.213 0.129

How do you know that this is a legitimate probability model?

What is the probability that a randomly chosen person over age 25 has at least a high school education?

What is the probability that a randomly chosen person over age 25 has at least a bachelor’s degree?

III.11 Language study. Choose a student in grades K to 12 at random and ask if he or she is studying a language other than English. Here is the distribution of results:

Language: Spanish French German Chinese All others None

Probability: 0.136 0.024 0.006 0.004 0.026 0.804

Explain why this is a legitimate probability model. (Hint: See page 427.)

What is the probability that a randomly chosen student is studying a language other than English? (Hint: See page 427.)

What is the probability that a randomly chosen student is studying French, German, or Spanish? (Hint: See page 427.)

III.12 Choosing at random. Abby, Deborah, Mei-Ling, Sam, and Roberto work in a firm’s public relations office. Their employer must choose two of them to attend a conference in Paris. To avoid unfairness, the choice will be made by drawing two names from a hat. (This is an SRS of size 2.)

Write down all possible choices of two of the five names. These are the possible outcomes.

The random drawing makes all outcomes equally likely. What is the probability of each outcome?

What is the probability that Mei-Ling is chosen?

What is the probability that neither of the two men (Sam and Roberto) is chosen?

III.13 Languages in Canada. Canada has two official languages: English and French. Choose a resident of Quebec at random and ask,「What is your mother tongue?」Here is the distribution of responses, combining many separate languages from the province of Quebec:

Language: English French Other

Probability: 0.083 0.789 ?

What is the probability that a randomly chosen resident of Quebec’s mother tongue is either English or French? (Hint: See page 427.)

What is the probability that a randomly chosen resident of Quebec’s mother tongue is「Other」? (Hint: See page 427.)

III.14 Confidence in public schools. (From the news) A 2018 Gallup poll asked adult Americans how much confidence they had in the public schools. Assume that the results of the poll accurately reflect the opinions of all adult Americans. Here is the distribution of responses:

Response: Great deal Quite a lot Some Very little None

Probability: 0.12 0.17 0.44 0.25 ?

What is the probability that a randomly chosen adult American has no confidence in the public schools?

What is the probability that a randomly chosen adult American has a great deal or quite a lot of confidence in the public schools?

III.15 An IQ test. The Wechsler Adult Intelligence Scale (WAIS) is a common IQ test for adults. The distribution of WAIS scores for persons over 16 years of age is approximately Normal with mean 100 and standard deviation 15. Use the 68–95–99.7 rule to answer these questions.

What is the probability that a randomly chosen individual has a WAIS score of 115 or higher? (Hint: See page 432.)

In what range do the scores of the middle 95% of the adult population lie? (Hint: See page 432.)

III.16 Worrying about crime. How much do Americans worry about crime and violence? Suppose that 50% of all adults worry a great deal about crime and violence. (According to a 2018 sample survey that asked this question, 50% is about right.) A polling firm chooses an SRS of 1100 people. If they do this many times, the percentage of the sample who say they worry a great deal will vary from sample to sample following a Normal distribution with mean 50% and standard deviation 1.5%. Use the 68–95–99.7 rule to answer these questions.

What is the probability that one such sample gives a result within of the truth about the population?

What is the probability that one such sample gives a result within of the truth about the population?

III.17 An IQ test (optional). Use the information in Exercise III.15 and Table B at the end of this text to find the probability that a randomly chosen person has a WAIS score of 112 or higher. (Hint: See page 433.)

III.18 Worrying about crime (optional). Use the information in Exercise III.16 and Table B at the end of this text to find the probability that one sample misses the truth about the population by 2.5% or more. (This is the probability that the sample result is either less than 47.5% or greater than 52.5%.)

III.19 An IQ test (optional). How high must a person score on the WAIS test to be in the top 10% of all scores? Use the information in Exercise III.15 and Table B at the end of this text to answer this question. (Hint: See page 433.)

III.20 Models, legitimate and not. A bridge deck contains 52 cards, four of each of the 13 face values ace, king, queen, jack, ten, nine, … , two. You deal a single card from such a deck and record the face value of the card dealt. Give an assignment of probabilities to the possible outcomes that should be correct if the deck is thoroughly shuffled. Give a second assignment of probabilities that is legitimate (that is, obeys the rules of probability) but differs from your first choice. Then give a third assignment of probabilities that is not legitimate, and explain what is wrong with this choice.

III.21 Mendel’s peas. Gregor Mendel used garden peas in some of the experiments that revealed that inheritance operates randomly. The seed color of Mendel’s peas can be either green or yellow. Suppose we produce seeds by「crossing」two plants, both of which carry the G (green) and Y (yellow) genes. Each parent has probability 0.5 of passing each of its genes to a seed, independently of the other parent. A seed will be yellow unless both parents contribute the G gene. Seeds that get two G genes are green.

What is the probability that a seed from this cross will be green? Set up a simulation to answer this question, and estimate the probability from 25 repetitions. (Hint: See page 446.)

III.22 Predicting the winner. There are eight teams in the Eastern Division of the National Hockey League. Here’s one set of personal probabilities for next year’s Eastern Division champion: The Tampa Bay Lightning and the Toronto Maple Leafs have probability 0.3 of winning. The Ottawa Senators, the Detroit Red Wings, and the Florida Panthers, have no chance. That leaves three teams. The Boston Bruins, and the Montreal Canadiens both have the same probability of winning, but that probability is one-half that of the Buffalo Sabres. What probability does each of the eight teams have?

III.23 Selling cars. Bill sells new cars in a small town for a living. On a weekday afternoon, he will deal with one customer with probability 0.6, two customers with probability 0.3, and three customers with probability 0.1. Each customer has probability 0.2 of buying a car. Customers buy independently of each other.

Describe how you would simulate the number of cars Bill sells in an afternoon. You must first simulate the number of customers, then simulate the buying decisions of one, two, or three customers. Simulate one afternoon to demonstrate your procedure. (Hint: See page 450.)

PART PROJECTS

Projects are longer exercises that require gathering information or producing data and that emphasize writing a short essay to describe your work. Many are suitable for teams of students.

Access these projects on the text website: macmillanlearning.com/scc10e.

PART IV Inference

To infer is to draw a conclusion from evidence. Statistical inference draws a conclusion about a population from evidence provided by a sample. Drawing conclusions in mathematics is a matter of starting from a hypothesis and using logical argument to prove without doubt that the conclusion follows. Statistics isn’t like that. Statistical conclusions are uncertain because the sample isn’t the entire population. So statistical inference has to not only state conclusions but also say how uncertain they are. We use the language of probability to express uncertainty.

Because inference must both give conclusions and say how uncertain they are, it is the most technical part of statistics. Texts and courses intended to train people to do statistics spend most of their time on inference. Our aim in this book is to help you understand statistics, which takes less technique but often more thought. We will look only at a few basic techniques of inference. The techniques are simple, but the ideas are subtle, so prepare to think. To start, think about what you already know and don’t be too impressed by elaborate statistical techniques: even the fanciest inference cannot remedy basic flaws such as voluntary response samples or uncontrolled experiments.

CHAPTER 21 What Is a Confidence Interval?

In this chapter you will:

Learn how to construct confidence intervals for proportions and means.

Be able to interpret what confidence intervals represent.

Case Study: Social Media Use

What is the most popular social media platform? It might depend on who you ask. In 2018, the Pew Research Center published a report on social media use. To obtain their sample, random digit dialing was used. The sample included 2002 adults, 18 years of age or older, from across the United States. A total of 1502 survey respondents were interviewed on a cell phone, and the remaining 500 survey respondents were interviewed on a landline phone. Survey respondents were 18 years of age and older.

When asked which social media platforms they used, 75% of the 2002 survey respondents said they used YouTube. Facebook was used by 68% of the 2002 respondents, and over one-third, or 35%, of the survey respondents reported using Instagram. Snapchat (27%) and Twitter (24%) were used less often by all survey respondents. When results were broken down by age group, however, a different pattern of results emerged. Of the 201 survey respondents between the ages of 18 and 24 years, 94% reported using YouTube, 80% reported using Facebook, 71% reported using Instagram, 78% reported using Snapchat, and 45% reported using Twitter. We know these numbers won’t be exactly accurate for the entire population of 18- to 24-year-olds, but are they close? By the end of this chapter, you will be able to see how accurate numbers like 94%, 80%, 71%, 78%, and 45% are.

Estimating

Statistical inference draws conclusions about a population on the basis of data about a sample. One kind of conclusion answers questions like「What percentage of employed women have a college degree?」or「What is the mean survival time for patients with this type of cancer?」These questions ask about a number (a percentage, a mean) that describes a population. Numbers that describe a population are parameters. To estimate a population parameter, choose a sample from the population and use a statistic, a number calculated from the sample, as your estimate. Here’s an example.

Example 1

Graduation plans

The National Survey of Student Engagement (NSSE) is administered annually to first-year and senior undergraduate students across the United States and Canada. The purpose of the NSSE is to better understand the extent to which these students engage in educational practices associated with high levels of learning and development. In 2018, the NSSE was completed by students from 511 institutions of higher learning. One question graduating seniors were asked was「After graduation, what best describes your immediate plans?」Of the 23,915 seniors who answered this question, 5038 indicated they planned to go to graduate or professional school. Based on this information, what can we say about the percentage of all college seniors who plan to go to graduate or professional school?

Our population is college seniors who reside in the United States or Canada. The parameter is the proportion who plan to go to graduate or professional school.

Call this unknown parameter , for「proportion.」The statistic that estimates the parameter is the sample proportion

Key Terms

A 95% confidence interval is an interval calculated from sample data by a process that is guaranteed to capture the true population parameter in 95% of all samples.

A basic move in statistical inference is to use a sample statistic to estimate a population parameter. Once we have the sample in hand, we estimate that the proportion of all college seniors in the United States and Canada who plan to go to graduate or professional school is「about 21.1%」because the proportion in the sample was exactly 21.1%. We can only estimate that the truth about the population is「about」21.1% because we know that the sample result is unlikely to be exactly the same as the true population proportion. A confidence interval makes that「about」precise.

We will first calculate the interval for a population proportion, and then we will reflect on what we have done and generalize a bit.

Estimating with Confidence

We want to estimate the proportion of the individuals in a population who have some characteristic—they are employed or they approve of the president’s performance, for example. Let’s call the characteristic we are looking for a「success.」We use the proportion of successes in a simple random sample (SRS) to estimate the proportion of successes in the population. How good is the statistic as an estimate of the parameter ? To find out, we ask,「What would happen if we took many samples?」Well, we know that would vary from sample to sample. We also know that this sampling variability isn’t haphazard. It has a clear pattern in the long run, a pattern that is pretty well described by a Normal curve. The facts are given in the box at the below.

Sampling distribution of a sample proportion

The sampling distribution of a statistic is the distribution of values taken by the statistic in all possible samples of the same size from the same population.

Take an SRS of size from a large population that contains proportion of successes. Let be the sample proportion of successes,

Then, if the sample size is large enough:

The sampling distribution of is approximately Normal.

The mean of the sampling distribution of is .

The standard deviation of the sampling distribution of is

These facts can be proved by mathematics, so they are a solid starting point. Figure 21.1 summarizes them in a form that also reminds us that a sampling distribution describes the results of lots of samples from the same population.

Figure 21.1 Repeat many times the process of selecting an SRS of size from a population in which the proportion are successes. The values of the sample proportion of successes have this Normal sampling distribution.

An illustration of a group of people representing Population proportion p. Three arrows pointing from the illustration denote S R S size n gives p (proportion of successes). This is represented by a normal distribution bell curve on the right.

The horizontal axis represents values of p (proportion of successes). A perpendicular line is drawn from the horizontal axis to the peak of the normal curve. The point where the perpendicular line meets the horizontal axis is denoted as mean p. A line is drawn from the perpendicular line to the right portion of the curve and an equation pointing to the region enclosed denotes square root of p in terms of 1 minus p over n.

Example 2

More on graduation plans

Suppose, for example, that the truth is that 21.5% of college seniors in the United States and Canada plan to go to graduate or professional school. Then, in the setting of Example 1, . The NSSE sample of size would, if repeated many times, produce sample proportions that closely follow the Normal distribution with

and

The center of this Normal distribution is at the truth about the population. That’s in the absence of bias in random sampling once again. The standard error is small because the sample is quite large. So, almost all samples will produce a statistic that is close to the true . In fact, the 95 part of the 68–95–99.7 rule says that 95% of all sample outcomes will fall between

and

Figure 21.2 displays these facts.

Figure 21.2 Repeat many times the process of selecting an SRS of size 23,915 from a population in which the proportion are successes. The middle 95% of the values of the sample proportion will lie between 0.2097 and 0.2203.

The horizontal axis has values of the sample proportion ranging from 0.206 to 0.224 at intervals of 0.003. A bell curve is drawn. The text between 0.2097 and 0.2203 reads, 95 percent of all values of the sample proportion. Two perpendicular lines are drawn at 0.2097 and 0.2203.

Key Terms

The standard deviation of the sampling distribution of a sample statistic is commonly referred to as the standard error.

So far, we have just put numbers on what we already knew: we can trust the results of large random samples because almost all such samples give results that are close to the truth about the population. The numbers say that in 95% of all samples of size 23,915, the statistic and the parameter are within 0.0053 of each other. We can put this another way: 95% of all samples give an outcome such that the population truth is captured by the interval from to .

Statistics in Your World

Who is a smoker? When estimating a proportion , be sure you know what counts as a「success.」The news says that 20% of adolescents smoke. Shocking. It turns out that this is the percentage who smoked at least once in the past month. If we say that a smoker is someone who smoked in at least 20 of the past 30 days and smoked at least half a pack on those days, fewer than 4% of adolescents qualify.

The 0.0053 came from substituting into the formula for the standard error of . For any value of , the general fact is

When the population proportion has the value , 95% of all samples catch in the interval extending 2 standard errors on either side of .

That’s the interval

Is this the 95% confidence interval we want? Not quite. The interval can’t be found just from the data because the standard deviation involves the population proportion , and in practice, we don’t know . In Example 2, we used in the formula, but this may not be the true .

What can we do? Well, the standard deviation of the statistic , or the standard error, does depend on the parameter , but it doesn’t change a lot when changes. Go back to Example 2 and redo the calculation for other values of . Here’s the result:

Value of : 0.20 0.205 0.21 0.215 0.22

Standard error: 0.00259 0.00261 0.00263 0.00266 0.00268

95% confidence interval for a population proportion

Choose an SRS of size from a large population that contains an unknown proportion of successes. Call the proportion of successes in this sample . An approximate 95% confidence interval for the parameter is

We see that, if we guess a value of reasonably close to the true value, the standard error found from the guessed value will be close to the true value (or the true standard error). We know that, when we take a large random sample, the statistic is almost always close to the parameter . So, we will use as the guessed value of the unknown . Now we have an interval that we can calculate from the sample data.

Example 3

A confidence interval for graduation plans

The NSSE sample of 23,915 college seniors found that 5038 reported plans to go to graduate or professional school, giving a sample proportion . The 95% confidence interval for the proportion of all college seniors from the United States and Canada who plan to go to graduate or professional school is

Interpret this result as follows: we got this interval by using a procedure that catches the true unknown population proportion in 95% of all samples. The shorthand is that we are 95% confident that between 20.57% and 21.63% of all college seniors in the United States and Canada plan to go to graduate or professional school.

Now it’s your turn

21.1 Why do we turn to YouTube? A November 2018 Pew Research Center survey consisting of a random sample of 4594 adult Americans found that 51% reported using YouTube in order to figure out how to do things they haven’t done before. Find a 95% confidence interval for the proportion of all adult Americans who use YouTube to figure out how to do things they haven’t done before. How would you interpret this interval?

Understanding Confidence Intervals

Our 95% confidence interval for a population proportion has the familiar form

News reports of sample surveys, for example, usually give the estimate and the margin of error separately:「A new Gallup Poll shows that 65% of women favor new laws restricting guns. The margin of error is plus or minus four percentage points.」News reports usually leave out the level of confidence, although it is almost always 95%.

The next time you hear a report about the result of a sample survey, consider the following. If most confidence intervals reported in the media have a 95% level of confidence, then in about 1 in 20 reported poll results, the confidence interval does not contain the true value of the population proportion.

Key Terms

A level confidence interval for a parameter has two parts: An interval calculated from the data.

A confidence level , which gives the probability that the interval will capture the true parameter value in repeated samples.

A complete description of a confidence interval is given in the box at the right.

There are many recipes for statistical confidence intervals for use in many situations. Not all confidence intervals are expressed in the form「estimate margin of error.」Be sure you understand how to interpret a confidence interval. The interpretation is the same for any recipe, and you can’t use a calculator or a computer to do the interpretation for you.

Confidence intervals use the central idea of probability: ask what would happen if we repeated the sampling many times. The 95% in a 95% confidence interval is a probability, the probability that the method produces an interval that does capture the true parameter.

Example 4

How confidence intervals behave

The NSSE sample of 23,915 college seniors found that 5038 reported plans to go to graduate or professional school, so the sample proportion was

and the 95% confidence interval was

Draw a second sample from the same population. It finds that 4976 of its 23,915 respondents plan to go to graduate or professional school. For this sample,

Draw another sample. Now the count is 5503 and the sample proportion and confidence interval are

Keep sampling. Each sample yields a new estimate and a new confidence interval. If we sample forever, 95% of these intervals capture the true parameter. This is true no matter what the true value is. Figure 21.3 summarizes the behavior of the confidence interval in graphical form.

Figure 21.3 Repeated samples from the same population give different 95% confidence intervals, but 95% of these intervals capture the true population proportion .

Three arrows point from an illustration of a group of people representing the Population proportion p and read, S R S size 23,915 gives 0.211 plus or minus 0.0053, S R S size 23,915 gives 0.208 plus or minus 0.0052, S R S size 23,915 gives 0.230 plus or minus 0.0054. A curly bracket corresponding to the text denotes 95 percent of these intervals cover the true p.

Example 4 and Figure 21.3 remind us that repeated samples give different results and that we are guaranteed only that 95% of the samples give a correct result. On the assumption that two pictures are better than one, Figure 21.4 gives a different view of how confidence intervals behave. Figure 21.4 goes behind the scenes. The vertical line is the true value of the population proportion . The Normal curve at the top of the figure is the sampling distribution of the sample statistic , which is centered at the true . We are behind the scenes because, in real-world statistics, we usually don’t know .

Figure 21.4 Twenty-five samples from the same population give these 95% confidence intervals. In the long run, 95% of all such intervals cover the true population proportion, marked by the vertical line.

The horizontal axis represents values of p. A perpendicular line is drawn from the horizontal axis and touches the peak of the normal curve. The point where the perpendicular line meets the horizontal axis is labeled mean p. The bell curve represents sampling distribution of p. Below the normal distribution curve, twenty-five horizontal lines and a vertical line running through them represent 95 percent confidence intervals.

The 95% confidence intervals from 25 SRSs appear below the graph in Figure 21.4, one after the other. The central dots are the values of , the centers of the intervals. The arrows on either side span the confidence interval. In the long run, 95% of the intervals will capture the true and 5% will miss. Of the 25 intervals in Figure 21.4, there are 24 hits and 1 miss. (Remember that probability describes only what happens in the long run—we don’t expect exactly 95% of 25 intervals to capture the true parameter.)

Don’t forget that our interval is only approximately a 95% confidence interval. It isn’t exact for two reasons. The sampling distribution of the sample proportion isn’t exactly Normal. And we don’t get the standard deviation, or the standard error, of exactly right because we used in place of the unknown . We use a new estimate of the standard deviation of the sampling distribution every time, even though the true standard deviation never changes. Both of these difficulties go away as the sample size gets larger. So, our recipe is good only for large samples. What is more, the recipe assumes that the population is really big—at least 10 times the size of the sample. Professional statisticians use more elaborate methods that take the size of the population into account and work even for small samples. But our method works well enough for many practical uses. More important, it shows how we get a confidence interval from the sampling distribution of a statistic. That’s the reasoning behind any confidence interval.

More on Confidence Intervals for a Population Proportion*

We used the 95 part of the 68–95–99.7 rule to get a 95% confidence interval for the population proportion. Perhaps you think that a method that works 95% of the time isn’t good enough. You want to be 99% confident. For that, we need to mark off the central 99% of a Normal distribution. For any probability between 0 and 1, there is a number such that any Normal distribution has probability within standard deviations of the mean. Figure 21.5 shows how the probability and the number are related.

Figure 21.5 Critical values of the Normal distributions. In any Normal distribution, there is area (probability) under the curve between and standard deviations away from the mean.

The horizontal axis represents Standard deviations above and below the mean ranging from negative 3 to 3 at intervals of 1. A perpendicular dotted line is drawn from 0 on the horizontal axis and touches the peak of the normal curve. The area enclosed by the normal curve and the points from 0 to negative z asterisk is shaded and corresponding text that reads: Shaded area represents probability C. The area enclosed by the normal curve and the points from 0 to z asterisk reads, z asterisk standard deviations.

Table 21.1 gives the numbers for various choices of . For convenience, the table gives as a confidence level in percent. The numbers are called critical values of the Normal distributions. Table 21.1 shows that any Normal distribution has probability 99% within standard deviations of its mean. The table also shows that any Normal distribution has probability 95% within standard deviations of its mean. The 68–95–99.7 rule uses 2 in place of the critical value . That is good enough for practical purposes, but the table gives the more exact value.

Table 21.1 Critical values of the Normal distributions

Confidence level Critical value Confidence level Critical value

50% 0.67 90% 1.64

60% 0.84 95% 1.96

70% 1.04 99% 2.58

80% 1.28 99.9% 3.29

Confidence interval for a population proportion

Choose an SRS of size from a population of individuals of which proportion are successes. The proportion of successes in the sample is . When is large, an approximate level confidence interval for is

where is the critical value for probability from Table 21.1.

From Figure 21.5 we see that, with probability , the sample proportion takes a value within standard deviations of . That is just to say that, with probability , the interval extending standard deviations on either side of the observed captures the unknown . Using the estimated standard error of produces the formula for the confidence interval for a population proportion given in the box at the left.

Example 5

A 99% confidence interval

The NSSE sample of 23,915 college seniors found that 5038 reported plans to go to graduate or professional school. We want a 99% confidence interval for the proportion of all college seniors in the United States and Canada who plan to go to graduate or professional school. Table 21.1 says that for 99% confidence, we must go out standard deviations. Here are our calculations:

We are 99% confident that between 20.42% and 21.78% of all college seniors in the United States and Canada plan to go to graduate or professional school. Put differently, we got this range of percentages by using a method that gives a correct answer 99% of the time.

Compare Example 5 with the calculation of the 95% confidence interval in Example 3. The only difference is the use of the critical value 2.58 for 99% confidence in place of 2 for 95% confidence. That makes the margin of error for 99% confidence larger and the confidence interval wider. Higher confidence isn’t free—we pay for it with a wider interval. Figure 21.5 reminds us why this is true. To cover a higher percentage of the area under a Normal curve, we must go farther out from the center. Figure 21.6 compares the lengths of the 90%, 95%, and 99% confidence intervals.

Figure 21.6 The lengths of three confidence intervals for the graduation plans example. All three are centered at the estimate When the data and the sample size remain the same, higher confidence results in a larger margin of error.

Three lines are drawn. The first line ranges from 0.204 to 0.218 and is labeled 99 percent confidence. The second line, drawn above the first line, ranges from 0.206 to 0.217, and is labeled 95 percent confidence. The third line, drawn above the second line, ranges from 0.208 to 0.215 and is labeled 90 percent confidence. An arrow centered above the three lines reads, Sample proportion equals 0.211 is the estimate of the unknown population proportion.

Now it’s your turn

21.2 What is America’s most important problem? A July 2018 Gallup Poll consisting of a random sample of 1033 adult Americans found that 22% believe that immigration is the most important problem facing the nation. Find a 99% confidence interval for the proportion of all adult Americans who believe immigration is the most important problem facing the nation. How would you interpret this interval?

*This section is optional.

The Sampling Distribution of a Sample Mean*

Sampling distribution of a sample mean

Choose an SRS of size from a population in which individuals have mean and standard deviation . Let be the mean of the sample. Then:

The sampling distribution of is approximately Normal when the sample size is large.

The mean of the sampling distribution of is equal to .

The standard deviation or the standard error of the sampling distribution of is .

What is the mean number of hours your college’s first-year students study each week? What was their mean grade point average in high school? We often want to estimate the mean of a population. To distinguish the population mean (a parameter) from the sample mean , we write the population mean as (the Greek letter mu). We use the mean of an SRS to estimate the unknown mean of the population.

Like the sample proportion , the sample mean from a large SRS has a sampling distribution that is close to Normal. Because the sample mean of an SRS is an unbiased estimator of , the sampling distribution of has as its mean. The standard deviation, or standard error, of depends on the standard deviation of the population, which is usually written as (the Greek letter sigma). By mathematics, we can discover the facts given in the box at the left.

It isn’t surprising that the values that takes in many samples are centered at the true mean of the population. That’s the lack of bias in random sampling once again. The other two facts about the sampling distribution make precise two very important properties of the sample mean :

The mean of a number of observations is less variable than individual observations.

The distribution of a mean of a number of observations is more Normal than the distribution of individual observations.

Figure 21.7 illustrates the first of these properties. It compares the distribution of a single observation with the distribution of the mean of 10 observations. Both have the same center, but the distribution of is less spread out. In Figure 21.7, the distribution of individual observations is Normal. If that is true, then the sampling distribution of is exactly Normal for any size sample, not just approximately Normal for large samples. A remarkable statistical fact, called the central limit theorem, says that as we take more and more observations at random from any population, the distribution of the mean of these observations eventually gets close to a Normal distribution. (There are some technical qualifications to this big fact, but in practice, we can ignore them.) The central limit theorem lies behind the use of Normal sampling distributions for sample means.

Figure 21.7 The sampling distribution of the sample mean of 10 observations compared with the distribution of individual observations.

A normal bell curve representing 1 observation overlaps with an elongated bell curve representing x bar for 10 observations. A perpendicular line is drawn from the horizontal axis to the peak of the normal curves. A line is drawn to the right from the perpendicular line to the normal curve for 1 observation, which denotes the standard deviation sigma. A line is drawn to the right from the perpendicular line to the normal curve for 10 observations, which denotes the standard deviation sigma over the square root of 10.

Example 6

The central limit theorem in action

Figure 21.8 shows the central limit theorem in action. The top-left density curve describes individual observations from a population. It is strongly right-skewed. Distributions like this describe the time it takes to repair a household appliance, for example. Most repairs are quickly done, but some are lengthy.

Figure 21.8 The distribution of a sample mean becomes more Normal as the size of the sample increases. The distribution of individual observations is far from Normal. The distributions of means of 2, 10, and finally 25 observations move closer to the Normal shape.

The top-left density curve represents a mean of n equals 1 and is strongly right-skewed. The top-right density curve represents a mean of n equals 2 and is more skewed to the right. The bottom-left density curve represents a mean of n equals 10 and is somewhat skewed to the right. The bottom-right normal density curve represents a mean of n equals 25.

The other three density curves in Figure 21.8 show the sampling distributions of the sample means of 2, 10, and 25 observations from this population. As the sample size increases, the shape becomes more Normal. The mean remains fixed and the standard error decreases, following the pattern . The distribution for 10 observations is still somewhat skewed to the right but already resembles a Normal curve. The density curve for is yet more Normal. The contrast between the shapes of the population distribution and of the distribution of the mean of 10 or 25 observations is striking.

*This section is optional.

Confidence Intervals for a Population Mean*

Confidence interval for a population mean

Choose an SRS of size from a large population of individuals having mean . The mean of the sample observations is . When is reasonably large, an approximate level confidence interval for is

where is the critical value for confidence level from Table 21.1.

The standard error of depends on both the sample size and the standard deviation of individuals in the population. We know but not . When is large, the sample standard deviation is close to and can be used to estimate it, just as we use the sample mean to estimate the population mean . The estimated standard error of is, therefore, . Now we can find confidence intervals for following the same reasoning that led us to confidence intervals for a proportion . The big idea is that to cover the central area under a Normal curve, we must go out a distance on either side of the mean. Look again at Figure 21.5 to see how and are related.

The cautions we noted in estimating apply here as well. The recipe is valid only when an SRS is drawn and the sample size is reasonably large. How large is reasonably large? The answer depends upon the true shape of the population distribution. A sample size of is usually adequate unless there are extreme outliers or strong skewness. For clearly skewed distributions, a sample size of often suffices if there are no outliers.

The margin of error again decreases only at a rate proportional to as the sample size increases. And it bears repeating that and are strongly influenced by outliers. Inference using and is suspect when outliers are present. Always look at your data.

Example 7

NAEP quantitative scores

The National Assessment of Educational Progress (NAEP) includes a mathematics test for high school seniors. Scores on the test range from 0 to 300. Demonstrating the ability to use the Pythagorean theorem to determine the length of a hypotenuse is an example of the skills and knowledge associated with performance at the Basic level. An example of the knowledge and skills associated with the Proficient level is using trigonometric ratios to determine length.

In 2015, the NAEP randomly selected 13,200 seniors in high school who took the mathematics test. The mean mathematics score was and the standard deviation of their scores was . Assume that these 13,200 students were a random sample from the population of all 12th-graders. On the basis of this sample, what can we say about the mean score in the population of all 12th-grade students?

The 95% confidence interval for uses the critical value from Table 21.1. The interval is

We are 95% confident that the interval from 151.42 to 152.58 includes the mean score for all 12th-grade students.

Now it’s your turn

21.3 Running a mile. The manager at a large fitness center keeps track of the amount of time it takes a sample of 65 clients to run a mile. She finds that the mean time to run a mile in this sample is minutes and the standard deviation is minutes. Assuming the sample is a random sample of all clients at this particular fitness center, find a 95% confidence interval for , the unknown mean running time of all clients from the fitness center.

*This section is optional.

Chapter 21 Summary and Exercises

Chapter 21: Statistics in Summary

Statistical inference draws conclusions about a population on the basis of data from a sample. Because we don’t have data for the entire population, our conclusions are uncertain.

A confidence interval estimates an unknown parameter in a way that tells us how uncertain the estimate is. The interval itself says how closely we can pin down the unknown parameter. The confidence level is a probability that says how often in many samples the method would produce an interval that does catch the parameter. We find confidence intervals starting from the sampling distribution of a statistic, which shows how the statistic varies in repeated sampling.

The standard deviation of the sampling distribution of the sample statistic is commonly referred to as the standard error.

We estimate a population proportion using the sample proportion of an SRS from the population. Confidence intervals for are based on the sampling distribution of . When the sample size is large, this distribution is approximately Normal.

We estimate a population mean using the sample mean of an SRS from the population. Confidence intervals for are based on the sampling distribution of . When the sample size is large, the central limit theorem says that this distribution is approximately Normal. Although the details of the methods differ, inference about is quite similar to inference about a population proportion because both are based on Normal sampling distributions.

This chapter summary will help you evaluate the Case Study.

Link It

