Learn a simple graphical method for summarizing important features of large data sets.

Case Study: Education and Income

Does education pay? We are told that people with more education earn more on average than people with less education. How much more? How can we answer this question?

Data on income can be found at the Census Bureau website. The data are estimates, for the year 2017, of the total incomes of 219,830,000 people aged 25 and older with earnings, and are based on the results of the Current Population Survey in 2018. The website gives the income distribution for each of several education categories. In particular, it gives the number of people in each of several education categories who earned between $1 and $2499, between $2500 and $4999, up to between $97,500 and $99,999, and $100,000 and over. That is a lot of information. A histogram could be used to display the data, but are there simple ways to summarize the information with just a few numbers that allow us to make sensible comparisons?

By the end of this chapter, using simple methods for summarizing large data sets, you will be able to provide an answer to whether education really pays.

Baseball has a rich tradition of using statistics to summarize and characterize the performance of players. In recent years, statistics have been used to evaluate player performance and potential to guide decisions about trades, when to replace the starting pitcher, and other coaching decisions. We begin by investigating ways to summarize the performance of the greatest home run hitters of all time.

In the summer of 2007, Barry Bonds shattered the career home run record, breaking the previous record set by Hank Aaron. Here are his home run counts for the years 1986 (his rookie year) to 2007 (his final season):

1986 1987 1988 1989 1990 1991 1992 1993 1994 1995 1996

16 25 24 19 33 25 34 46 37 33 42

1997 1998 1999 2000 2001 2002 2003 2004 2005 2006 2007

40 37 34 49 73 46 45 45 5 26 28

The stemplot in Figure 12.1 displays the data. The shape of the distribution is a bit irregular, but we see that it has one high outlier, and if we ignore this outlier, we might describe it as slightly skewed to the left with a single peak. The outlier is, of course, Bonds’s record season in 2001.

Figure 12.1 Stemplot of the number of home runs hit by Barry Bonds in his 22-year career.

The stem plot gives the following data:

Line 1: 0 | 5

Line 2: 1 | 6 9

Line 3: 2 | 4 5 5 6 8

Line 4: 3 | 3 3 4 4 7 7

Line 5: 4 | 0 2 5 5 6 6 9

Line 6: 5 | blank

Line 7: 6 | blank

Line 8: 7 | 3

An accompanying key reads, A stem of 1 and a leaf of 6 means 16 home runs.

A graph and a few words give a good description of Barry Bonds’s home run career. But words are less adequate to describe, for example, the incomes of people with a high school education. We need numbers that summarize the center and variability of a distribution.

Median and Quartiles

A simple and effective way to describe center and variability is to give the median and the quartiles. The median, denoted M, is the midpoint, the value that separates the smaller half of the observations from the larger half. The middle 50% of the observations fall between the first and third quartiles. The quartiles get their name because with the median they divide the observations into quarters—one-quarter of the observations lie below the first quartile, half lie below the median, and three-quarters lie below the third quartile. That’s the idea. To actually get numbers, we need a rule that makes the idea exact.

Example 1

Finding the median

We might compare Bonds’s career with that of Hank Aaron’s, the previous holder of the career record. Here are Aaron’s home run counts for his 23 years in baseball.

13 27 26 44 30 39 40 34 45 44 24 32

44 39 29 44 38 47 34 40 20 12 10

To find the median, first arrange them in order from smallest to largest:

10 12 13 20 24 26 27 29 30 32 34 34

38 39 39 40 40 44 44 44 44 45 47

The bold 34 is the center observation, with 11 observations to its left and 11 to its right. When the number of observations is odd (here ), there is always one observation in the center of the ordered list. This is the median,

How does this compare with Bonds’s record? Here are Bonds’s 22 home run counts, arranged in order from smallest to largest:

When is even, there is no one middle observation. But there is a middle pair—the bold 34 and 34 have 10 observations on either side. We take the median to be halfway between this middle pair. So Bonds’s median is

There is a fast way to locate the median in an ordered list: count up places from the beginning of the list. Try it. For Aaron, and so the median is the 12th entry in the ordered list. For Bonds, and This means「halfway between the 11th and 12th」entries, so is the average of these two entries. This「 rule」is especially handy when you have many observations. The median of incomes is halfway between the 23,470th and 23,471st in the ordered list. Be sure to note that does not give the median , just its position in the ordered list of observations.

The median

The median is the midpoint of a distribution, the number such that half the observations are smaller and the other half are larger. To find the median of a distribution:

Arrange all observations in order of size, from smallest to largest.

If the number of observations is odd, the median is the observation that lies in the center of the ordered list. Find the location of the median by counting observations up from the bottom of the list.

If the number of observations is even, the median is the average of the two center observations in the ordered list. The location of the median is again from the bottom of the list.

The Census Bureau website provides data on income inequality. For example, it tells us that in 2017, the median income of Hispanic households was $50,486. That’s helpful but incomplete. Do most Hispanic households earn close to this amount, or are the incomes widely variable? The simplest useful description of a distribution consists of both a measure of center and a measure of variability. If we choose the median (the midpoint) to describe center, the quartiles (in particular, the difference between the quartiles) provide natural descriptions of variability. Again, the idea is clear: find the points one-quarter and three-quarters up the ordered list of observations. Again, we need a rule to make the idea precise. The rule for calculating the quartiles uses the rule for the median.

The quartiles and

To calculate the quartiles:

Arrange the observations in increasing order and locate the median in the ordered list of observations. This「overall」median will either be one of the observations in the ordered list (if there are an odd number of observations) or a value between two of the observations in the ordered list (if there are an even number of observations).

The first quartile is the median of the observations whose position in the ordered list is to the left of the location of the overall median. The overall median is not included in the observations considered to be to the left of the overall median.

The third quartile is the median of the observations whose position in the ordered list is to the right of the location of the overall median. The overall median is not included in the observations considered to be to the right of the overall median.

Example 2

Finding the quartiles

Hank Aaron’s 23 home run counts are

Data reads as follows: 10 12 13 20 24 26 27 29 30 32 34 34 38 39 39 40 40 44 44 44 44 45 47

The first Quartile, represented by Q 1, points to 26; The third Quartile, represented by Q 3, points to 44 and the Medium, represented by M points to 34. Medium is printed in bold.

There is an odd number of observations, so the median is the one in the middle, the bold 34 in the list. To find the quartiles, ignore this central observation. The first quartile is the median of the 11 observations to the left of the bold 34 in the list. That’s the sixth, so The third quartile is the median of the 11 observations to the right of the bold 34. It is

Barry Bonds’s 22 home run counts are

Data reads as follows: 5 16 19 24 25 25 26 28 33 33 34 34 37 37 40 42 45 45 46 46 49 73

The first Quartile, represented by Q 1, points to 25; The third Quartile, represented by Q 3, points to 45 and the Medium, represented by M, points to the space between 34 and 34, both of which are in bold.

The median lies halfway between the middle pair. There are 11 observations to the left of this location. The first quartile is the median of these 11 numbers. That’s the sixth, so The third quartile is the median of the 11 observations to the right of the overall median’s location,

Now it’s your turn

12.1 Babe Ruth. Prior to Hank Aaron, Babe Ruth was the holder of the career record. Here are Ruth’s home run counts for his 22 years in Major League Baseball, arranged in order from smallest to largest:

0 2 3 4 6 11 22 25 29 34 35

41 41 46 46 46 47 49 54 54 59 60

Find the median, first quartile, and third quartile of these counts.

You can use the rule to locate the quartiles when there are many observations. The Census Bureau website tells us that there were 17,318,000 (rounded off to the nearest 1000) Hispanic households in the United States in 2017. If we ignore the roundoff, the median of these 17,318,000 incomes is halfway between the 8,659,000th and 8,659,001st in the list arranged in order from smallest to largest. So the first quartile is the median of the 8,659,000 incomes below this point in the list. Use the rule with to locate the quartile:

The average of the 4,329,500th and 4,329,501st incomes in the ordered list falls in the range $25,000 to $34,999 and we estimate the first quartile to be $26,681.

The third quartile is the median of the 8,659,000 incomes above the median. By the rule with 8,659,000, this will be the average of the 4,329,500th and 4,329,501st incomes above the median in the ordered list. We find that this falls in the range $75,000 to $99,999 and we estimate the third quartile to be $89,880.

In practice, people use statistical software to compute quartiles. Software can give results that differ from those you will obtain using the method described here. In fact, different software packages use slightly different rules for deciding how to divide the space between two adjacent values between which the quartile is believed to lie. We have chosen to select the point halfway between them, but other rules exist. Two different software packages can give two slightly different answers, depending on the rule employed.

The Five-Number Summary and Boxplots

The smallest and largest observations tell us little about the distribution as a whole, but they give information about the tails of the distribution that is missing if we know only the median and the quartiles. To get a quick summary of both center and variability, combine all five numbers.

Key Terms

The five-number summary of a distribution consists of the smallest observation, the first quartile, the median, the third quartile, and the largest observation, written in order from smallest to largest. In symbols, the five-number summary is

These five numbers offer a reasonably complete description of center and variability. The five-number summaries of home run counts are

10 26 34 44 47

for Aaron and

5 25 34 45 73

for Bonds. The five-number summary of a distribution leads to a new graph, the boxplot. Figure 12.2 shows boxplots for the home run comparison.

Figure 12.2 Boxplots comparing the yearly home run production of Barry Bonds and Hank Aaron.

The first plot represents Bonds. The block, which represents the quartile, is divided into two parts. The smaller part of the boxplot, starts from 27 home runs to 34 home runs; a line which marks the median, separates the smaller part of the box to the largest part on top of it. The larger part of the boxplot starts from 34 home runs to 45 home runs. A whisker above the plot ranges from 45 to 75 and a whisker beneath the plot ranges from 27 to 5.

The second plot represents Aaron. The smaller part of the boxplot representing Aaron, starts from 25 home runs to 34 home runs; a line which marks the median, separates the smaller part of the box to the largest part on top of it. The larger part of the boxplot starts from 34 home runs to 45 home runs. A whisker above the plot ranges from 45 to 50 and a whisker beneath the plot ranges from 34 to 10.

Key Terms

A boxplot is a graph of the five-number summary. A central box spans the quartiles.

A line in the box marks the median.

Lines extend from the box out to the smallest and largest observations.

You can draw boxplots either horizontally or vertically. Be sure to include a numerical scale in the graph. When you look at a boxplot, first locate the median, which marks the center of the distribution. Then look at the variability. The quartiles (more precisely, the difference between the two quartiles) show the variability of the middle half of the data, and the extremes (the smallest and largest observations) indicate the variability of the entire data set. We see from Figure 12.2 that Bonds’s usual performance, as indicated by the median and the box that marks the middle half of the distribution, is similar to that of Aaron. We also see that the distribution for Aaron is less variable than the distribution for Bonds.

Now it’s your turn

12.2 Babe Ruth. Here are Babe Ruth’s home run counts for his 22 years in Major League Baseball, arranged in order from smallest to largest:

0 2 3 4 6 11 22 25 29 34 35

41 41 46 46 46 47 49 54 54 59 60

Draw a boxplot of this distribution. How does it compare with those of Barry Bonds and Hank Aaron in Figure 12.2?

Because boxplots show less detail than histograms or stemplots, they are best used for side-by-side comparison of more than one distribution, as in Figure 12.2. For such small numbers of observations, a back-to-back stemplot is better yet (see Exercise 11.22, page 263). It would make clear, as the boxplot cannot, that Bonds’s record 73 home runs in 2001 is an outlier in his career. Let us look at an example where boxplots are more genuinely useful.

Example 3

Income inequality

To investigate income inequality, we compare annual household incomes of Hispanics, blacks, and whites. The Census Bureau website provides information on income distribution by race. Figure 12.3 compares the income distributions for Hispanics, blacks, and whites in 2017. This figure is a variation on the boxplot idea. The largest income among several million people will surely be very large. Figure 12.3 uses the 95% points (the values representing where the top 5% of annual incomes start) in the distributions instead of the single largest incomes. So, for example, the line above the box for the Hispanic group extends only to $180,012 rather than to the highest income. Many statistical software packages allow you to produce boxplots that suppress extreme values, but the rules for what constitutes an extreme value usually do not use the 95% point in the distribution instead of the single largest value.

Figure 12.3 Boxplots comparing the distributions of income among Hispanics, blacks, and whites. The ends of each plot are at 0 and at the 95% point in the distribution.

The vertical axis represents household income (in thousands of dollars) for all the three groups. The first plot represents Blacks. A central block, which represents the quartile, is divided into two parts. The smaller part of the boxplot representing Blacks, starts from 23 thousand dollars to 42 thousand dollars; a line which marks the median, separates the smaller part of the box to the largest part on top of it. The larger part of the boxplot starts from 42 thousand dollars to 80 thousand dollars. A whisker above the plot ranges from 80 thousand dollars to 175 thousand dollars and a whisker below the plot ranges from 23 thousand dollars to 0.

The second plot represents Hispanics. The smaller part of the boxplot, starts from 27 thousand dollars to 51 thousand dollars; a line which marks the median, separates the smaller part of the box to the largest part on top of it. The larger part of the boxplot starts from 51 thousand dollars to 95 thousand dollars. A whisker at the top of the plot ranges from 95 thousand dollars to 180 thousand dollars and a whisker below the plot ranges from 27 thousand dollars to 0.

The smaller part of the boxplot representing Whites , starts from 30 thousand dollars to 70 thousand dollars; a line which marks the median, separates the smaller part of the box to the largest part on top of it. The larger part of the boxplot starts from 70 thousand dollars to 125 thousand dollars. A whisker at the top of the plot ranges from 125 thousand dollars to 250 thousand dollars and a whisker at the bottom of the plot ranges from 30 thousand dollars to 0.

Figure 12.3 gives us a clear and simple visual comparison. We see that the median and middle half are slightly greater for Hispanics than for blacks and that for whites the median and middle half are greater than for both blacks and Hispanics. The income of the bottom 5% stays small because there are some people in each group with no income or even negative income, perhaps due to illness or disability. The 95% point, marking off the top 5% of incomes, is greater for whites than for either blacks or Hispanics, and the 95% point of incomes for Hispanics is greater than for blacks. Overall, incomes for whites tend to be larger than those for Hispanics and blacks, highlighting racial inequities in income.

Figure 12.3 also illustrates how boxplots often indicate the symmetry or skewness of a distribution. In a symmetric distribution, the first and third quartiles are equally distant from the median. In most distributions that are skewed to the right, on the other hand, the third quartile will be farther above the median than the first quartile is below it. The extremes behave the same way. Even with the top 5% not present, we can see the right-skewness of incomes for all three races.

STATISTICAL CONTROVERSIES

Income Inequality

During the prosperous 1980s and 1990s, the incomes of all American households went up, but the gap between rich and poor grew. Figures 12.4 and 12.5 give two views of increasing inequality. Figure 12.4 is a line graph of household income, in dollars adjusted to have the same buying power every year. The lines show the 20th and 80th percentiles of income, which mark off the bottom fifth and the top fifth of households. The 80th percentile (up 66% between 1967 and 2017) is pulling away from the 20th percentile (up about 28%).

Figure 12.4 The change over time of two points in the distribution of incomes for American households. Eighty percent of households have incomes below the 80th percentile, and 20% have incomes below the 20th percentile. In 2017, the 20th percentile was $24,638, and the 80th percentile was $126,855.

The line representing the 20th percentile starts at 20,000 dollars of household income in 1965 and maintains approximately the same value beyond the year 2015. The line representing the 80th percentile starts at 75,000 dollars of household income in 1965 and gradually rises to 120,000 dollars in 1997 and ends at 130,000 dollars beyond the year 2015.

Figure 12.5 The change over time of the shares of total household income that go to the highest-income 20% and to the lowest-income 20% of households. In 2017, the top 20% of households received 52% of all income.

The line representing the bottom 20 percent starts at 4 percent of income in 1965 and maintains approximately the same value beyond the year 2015. The line representing the top 20 percent starts at 43 percent of total income in 1965 and slightly rises to 52 percent beyond the year 2015.

Figure 12.5 looks at the share of all income that goes to the top fifth and the bottom fifth. The bottom fifth’s share has drifted down, to 3.1% of all income in 2017. The share of the top fifth grew to 52% (up 18.1% between 1967 and 2017). Although not displayed in the figures, the share of the top 5% grew even faster, from 17.2% in 1967 to 22.3% of the income of all households in the country in 2017. This is a 29.7% increase between 1967 and 2017. Income inequality in the United States is greater than in other developed nations and has been increasing.

Are these numbers cause for concern? And do they accurately reflect the disparity between the wealthy and the poor? For example, as people get older, their income increases. Perhaps these numbers reflect only the disparity between younger and older wage earners. What do you think?

Software packages often produce boxplots using a more complicated rule than we have described here. These may look different than those we have displayed. See the「Notes and Data Sources」for a brief discussion of these more complicated rules.

Mean and Standard Deviation

The five-number summary is not the most common numerical description of a distribution. That distinction belongs to the combination of the mean to measure center and the standard deviation to measure variability. The mean is familiar—it is the ordinary average of the observations. The idea of the standard deviation is to give the average distance of observations from the mean. The「average distance」in the standard deviation is found in a rather obscure way. We will give the details, but you may want to just think of the standard deviation as「average distance from the mean」and leave the details to your calculator.

Mean and standard deviation

The mean (pronounced「x-bar」) of a set of observations is their arithmetic average. To find the mean of observations, add the values and divide by

The standard deviation measures the average distance of the observations from their mean. It is calculated by finding an average of the squared distances and then taking the square root. To find the standard deviation of observations:

Find the distance of each observation from the mean and square each of these distances.

Average the squared distances by dividing their sum by This average squared distance is called the variance.

The standard deviation is the square root of this average squared distance.

Example 4

Finding the mean and standard deviation

The numbers of home runs Barry Bonds hit in his 22 major league seasons are

16 25 24 19 33 25 34 46 37 33 42

40 37 34 49 73 46 45 45 5 26 28

To find the mean of these observations,

Figure 12.6 Barry Bonds’s home run counts, Example 4, with their mean and the distance of one observation from the mean indicated. Think of the standard deviation as an average of these distances.

The horizontal axis represents the homeruns in a season, and has values from 0 to 80, in increments of 10. A line which represents observation originates from 16 on the horizontal axis and a line which represents the mean originates from 34.6 on the horizontal axis. A double headed arrow marking the distance between observation and mean is labeled Distance equals negative 18.6.

A dot plot marks the following data:

6 runs: 1; 16 runs: 1; 18 runs: 1; 24 runs: 1; 25 runs: 2; 26 runs: 1; 28 runs: 1; 34 runs: 2; 34 runs: 2; 36 runs: 2; 40 runs: 1; 42 runs: 1; 45 runs: 2; 46 runs: 2; 49 runs: 1; 73 runs: 1.

Figure 12.6 displays the data as points above the number line, with their mean marked by a vertical line. The arrow shows one of the distances from the mean. The idea behind the standard deviation is to average the 22 distances. To find the standard deviation by hand, you can use a table layout:

Observation Squared distance from mean

16

25

⋮

28

The average is

Notice that we「average」by dividing by one less than the number of observations. Finally, the standard deviation is the square root of this number:

In practice, you can key the data into your calculator and hit the mean key and the standard deviation key. Or you can enter the data into a spreadsheet or other software to find and . It is usual, for good but somewhat technical reasons, to average the squared distances by dividing their total by rather than by . Many calculators have two standard deviation buttons, giving you a choice between dividing by and dividing by Be sure to choose

Now it’s your turn

12.3 Hank Aaron. Here are Aaron’s home run counts for his 23 years in baseball.

13 27 26 44 30 39 40 34 45 44 24 32

44 39 29 44 38 47 34 40 20 12 10

Find the mean and standard deviation of the number of home runs Aaron hit in each season of his career. How do the mean and median compare?

More important than the details of the calculation are the properties that show how the standard deviation measures variability.

Properties of the standard deviation

measures variability about the mean Use to describe the variability of a distribution only when you use to describe the center.

only when there is no variability. This happens only when all observations have the same value. So standard deviation zero means no variability at all. Otherwise, As the observations become more variable about their mean, gets larger.

Example 5

Investing 101

We have discussed examples about income. Here is an example about what to do with it once you’ve earned it. One of the first principles of investing is that taking more risk brings higher returns, at least on the average in the long run. People who work in finance define risk as the variability of returns from an investment (greater variability means higher risk) and measure risk by how unpredictable the return on an investment is. A bank account that is insured by the government and has a fixed rate of interest has no risk—its return is known exactly. Stock in a new company may soar one week and plunge the next. It has high risk because you can’t predict what it will be worth when you want to sell.

Investors should think statistically. You can assess an investment by thinking about the distribution of (say) yearly returns. That means asking about both the center and the variability of the pattern of returns. Only naive investors look for a high average return without asking about risk, that is, about how variable the returns are. Financial experts use the mean and standard deviation to describe returns on investments. The standard deviation was long considered too complicated to mention to the public, but now you will find standard deviations appearing regularly in mutual funds reports.

Here by way of illustration are the means and standard deviations of the yearly returns on three investments over the second half of the twentieth century (the 50 years from 1950 to 1999):

Investment Mean return Standard deviation

Treasury bills 5.34% 2.96%

Treasury bonds 6.12% 10.73%

Common stocks 14.62% 16.32%

You can see that risk (variability) goes up as the mean return goes up, just as financial theory claims. Treasury bills and bonds are ways of loaning money to the U.S. government. Treasury bills are paid back in 1 year, so their return changes from year to year depending on interest rates. Bonds are 30-year loans. They are riskier because the value of a bond you own will drop if interest rates go up. Stocks are even riskier. They give higher returns (on the average in the long run) but at the cost of lots of sharp ups and downs along the way. As the stemplot in Figure 12.7 shows, stocks went up by as much as 50% and down by as much as 26% in 1 year during the 50 years covered by our data.

Figure 12.7 Stemplot of the yearly returns on common stocks for the 50 years 1950–1999, Example 5. The returns are rounded to the nearest whole percent. The stems are 10s of percents and the leaves are single percents.

The stem plot gives the following data:

Line 1: negative 2 | 6

Line 2: negative 1 | 5 0 0

Line 3: negative 0 | 9 8 7 5 3

Line 4: 0 | 0 1 1 4 5 6 7 7 8

Line 5: 1 | 0 1 2 2 4 5 6 7 7 8

Line 6: 2 | 0 1 2 2 3 3 4 4 7 9 9

Line 7: 3 | 0 2 2 2 2 3 7 8

Line 8: 4 | 3

Line 9: 5 | 0

An accompanying key reads, A stem of negative 1 and a leaf of 5 means negative 15 percent.

Choosing Numerical Descriptions

The five-number summary is easy to understand and is the best short description for most distributions. The mean and standard deviation are harder to understand but are more common. How can we decide which of these two descriptions of center and variability to use? Let’s start by comparing the mean and the median.「Midpoint」and「arithmetic average」are both reasonable ideas for describing the center of a set of data, but they are different ideas with different uses. The most important distinction is that the mean (the average) is strongly influenced by a few extreme observations and the median (the midpoint) is not.

Example 6

Mean versus median

Table 12.1 gives the approximate salaries (in millions of dollars) of the 18 members of the Los Angeles Lakers basketball team for the 2018–2019 season. You can calculate that the mean is million and that the median is million. No wonder professional basketball players have big houses.

Table 12.1 Salaries of the Los Angeles Lakers, 2018–2019 season

Player Salary ($) Player Salary ($)

LeBron James 35.7 million Moritz Wagner 1.8 million

Luoi Deng 18.0 million Kyle Kuzma 1.7 million

Kentavious Caldwell-Pope 12.0 million Josh Hart 1.7 million

Rajon Rondo 9.0 million Ivica Zubac 1.5 million

Lonzo Ball 7.5 million Isaac Bonga 1.0 million

Brandom Ingram 5.8 million Joel Berry II 0.8 million

Lance Stephenson 4.4 million Jeffrey Carroll 0.8 million

Michael Beasley 3.5 million Alex Caruso 0.1 million

JaVale McGee 2.4 million Travis Wear 0.1 million

Data from www.spotrac.com/nba/rankings/base/los-angeles-lakers.

Why is the mean so much higher than the median? Figure 12.8 is a stemplot of the salaries, with millions as stems. The distribution is skewed to the right and there is one very high outlier. The very high salary of LeBron James pulls up the sum of the salaries and so pulls up the mean. If we drop the outlier, the mean for the other 17 players is only $4.2 million. The median doesn’t change nearly as much: it drops from $2.1 million to $1.8 million.

We can make the mean as large as we like by just increasing LeBron James’s salary. The mean will follow one outlier up and up. But to the median, LeBron’s salary just counts as one observation at the upper end of the distribution. Moving it from $35.7 million to $357 million would not change the median at all.

Figure 12.8 Stemplot of the salaries of Los Angeles Lakers players, from Table 12.1.

The stem plot gives the following data:

Line 0: 1 | 1 1 8 8

Line 1: 1 | 0 5 7 7 8

Line 2: 2 | 4

Line 3: 3 | 5

Line 4: 4 | 4

Line 5: 5 | 8

Line 6: 6 | Blank

Line 7: 7 | 5

Line 8: 8 | Blank

Line 9: 9 | 0

Line 10: 10| Blank

Line 11: 11| Blank

Line 12: 12| 0

Line 13: 13| Blank

Line 14: 14| Blank

Line 15: 15| 7

Line 16: 16| Blank

Line 17: 17| Blank

Line 18: 18| 0

Line 19: 19| Blank

Line 20: 20| Blank

Line 21: 21| Blank

Line 22: 22| Blank

Line 23: 23| Blank

Line 24: 24| Blank

Line 25: 25| Blank

Line 26: 26| Blank

Line 27: 27| Blank

Line 28: 28| Blank

Line 29: 29| Blank

Line 30: 30| Blank

Line 31: 31| Blank

Line 32: 32| Blank

Line 33: 33| Blank

Line 34: 34| Blank

Line 35: 35| 7

An accompanying key reads, A stem of 1 and a leaf of 4 means 1.4 million dollars.

Statistics in Your World

Poor New York? Is New York a rich state? New York’s mean income per person ranks sixth among the states, right up there with its rich neighbors Connecticut and New Jersey, which rank second and fourth. But while Connecticut and New Jersey rank ninth and eighth in median household income, New York stands 22nd. What’s going on? Just another example of mean versus median. New York has many very highly paid people, who pull up its mean income per person. But it also has a higher proportion of poor households than do Connecticut and New Jersey, and this brings the median down. New York is not a rich state—it’s a state with extremes of wealth and poverty.

The mean and median of a symmetric distribution are close to each other. In fact, and are exactly equal if the distribution is exactly symmetric. In skewed distributions, however, the mean runs away from the median toward the long tail. Many distributions of monetary values—incomes, house prices, wealth—are strongly skewed to the right. The mean may be much larger than the median. For example, we saw in Example 3 that the distribution of incomes for blacks, Hispanics, and whites is skewed to the right. The Census Bureau website gives the mean incomes for 2017 as $58,593 for blacks, $68,315 for Hispanics, and $93,453 for whites. Compare these with the corresponding medians of $40,258, $50,486, and $68,145. Because monetary data often have a few extremely high observations, descriptions of these distributions usually employ the median.

You should think about more than symmetry versus skewness when choosing between the mean and the median. The distribution of selling prices for homes in Middletown is no doubt skewed to the right—but if the Middletown City Council wants to estimate the total market value of all houses in order to set tax rates, the mean and not the median helps them out because the mean will be larger. (The total market value is just the number of houses times the mean market value and has no connection with the median.)

The standard deviation is pulled up by outliers or the long tail of a skewed distribution even more strongly than the mean. The standard deviation of the Lakers’ salaries is million for all 18 players and only million when the outlier is removed. The quartiles are much less sensitive to a few extreme observations. There is another reason to avoid the standard deviation in describing skewed distributions. Because the two sides of a strongly skewed distribution have different amounts of variability, no single number such as describes the variability well. The five-number summary, with its two quartiles and two extremes, does a better job. In most situations, it is wise to use and only for distributions that are roughly symmetric.

Choosing a summary

The mean and standard deviation are strongly affected by outliers or by the long tail of a skewed distribution. The median and quartiles are less affected.

The five-number summary is usually better than the mean and standard deviation for describing a skewed distribution or a distribution with outliers. Use and only for reasonably symmetric distributions that are free of outliers.

Why do we bother with the standard deviation at all? One answer appears in the next chapter: the mean and standard deviation are the natural measures of center and variability for an important kind of symmetric distribution, called the Normal distribution.

Remember that a graph gives the best overall picture of a distribution. Numerical measures of center and variability report specific facts about a distribution, but they do not describe its entire shape. Numerical summaries do not disclose the presence of multiple peaks or gaps, for example. Always start with a graph of your data.

Chapter 12 Summary and Exercises

Chapter 12: Statistics in Summary

If we have data on a single quantitative variable, we start with a histogram or stemplot to display the distribution. Then we include numbers to describe the center and variability of the distribution.

There are two common descriptions of center and variability: the five-number summary and the mean and standard deviation.

The five-number summary consists of the median M, the midpoint of the observations, to measure the center, the two quartiles and and the smallest and largest observations. The difference between and and the difference between the smallest and largest observations describes variability.

A boxplot is a graph of the five-number summary.

The mean is the average of the observations.

The standard deviation measures variability as a kind of average distance from the mean, so use it only with the mean. The variance is the square of the standard deviation.

The mean and standard deviation can be changed a lot by a few outliers. The mean and median are the same for symmetric distributions, but the mean moves farther toward the long tail of a skewed distribution.

In general, use the five-number summary to describe most distributions and the mean and standard deviation only for roughly symmetric distributions.

This chapter summary will help you evaluate the Case Study.

Link It

In Chapter 11, we discussed histograms and stemplots as graphical displays of the distribution of a single quantitative variable. We were interested in the shape, center, and variability of the distribution. In this chapter, we introduce numbers to describe the center and variability. For symmetric distributions, the mean and standard deviation are used to describe the center and variability. For distributions that are not roughly symmetric, we use the five-number summary to describe the center and variability.

In most of the examples, we used graphical displays and numbers to describe the distribution of data on a single quantitative variable. These data are typically a sample from some population. Thus, the numbers that describe features of the distribution are statistics as discussed in Chapter 3. In the next chapter, we begin to think about distributions of populations. Thus, the numbers that describe features of these distributions are parameters. In later chapters, we will use statistics to draw conclusions, or make inferences, about parameters. Drawing conclusions about parameters that describe the center of a distribution of a single quantitative variable will be an important type of inference.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study that opened the chapter. Start by reviewing the Chapter Summary. Then answer each of the following questions in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying.

Find the data on income by education at the Census Bureau website listed in the Notes and Data Sources section at the end of the book.

What are the median incomes for people 25 years old and older who are high school graduates only, have some college but no degree, have a bachelor’s degree, have a master’s degree, and have a doctorate degree? At the bottom of the table, you will find median earnings in dollars.

From the distribution given in the tables, can you find the (approximately) first and third quartiles?

Do people with more education earn more than people with less education? Discuss.

In this chapter you have:

Learned new methods to summarize large data sets with a few numbers such as the median, quartiles, mean, and standard deviation.

Understood how to interpret these new summary numbers as measures of the center and the variability of a distribution.

Learned a simple graphical method, the boxplot, for summarizing important features of large data sets.

Online Resources

The StatClips Examples videos, Summaries of Quantitative Data Example A, Example B, and Example C, describe how to compute the mean, standard deviation, and median of data.

The StatClips Examples video, Exploratory Pictures for Quantitative Data Example C, describes how to construct boxplots.

The Snapshots Video, Summarizing Quantitative Data, discusses the mean, standard deviation, and median of data, as well as stemplots, in the context of a real example.

Check the Basics

For Exercise 12.1, see page 271; for Exercise 12.2, see page 273; for Exercise 12.3, see page 279.

12.4 Mean The mean of the three numbers, 1, 2, and 15, is equal to

1.

2.

5.

6.

12.5 Median The median of the three numbers, 1, 2, and 15, is equal to

1.

2.

5.

6.

12.6 Standard deviation Which of the following statements is true of the standard deviation?

Removing an outlier will decrease the standard deviation.

Removing an outlier will increase the standard deviation.

It is the difference between the first and third quartile.

It is the difference between the minimum and maximum values.

12.7 The five-number summary Which of the following is a graph of the five-number summary?

A histogram

A stemplot

A boxplot

A bar graph

12.8 Describing distributions Which of the following should you use to describe a distribution that is skewed?

The five-number summary

The mean, the first quartile, and the third quartile

The mean and standard deviation

The median and standard deviation

Chapter 12 Exercises

12.9 Median income. You read that the median income of U.S. households in 2017 was $68,145. Explain in plain language what「the median income」is.

12.10 What’s the average? The Census Bureau website gives several choices for「average income」in its historical income data. In 2017, the median income of American households was $68,145. The mean household income was $93,453. The median income of families was $75,938, and the mean family income was $100,400. The Census Bureau says,「Households consist of all people who occupy a housing unit. The term ‘family’ refers to a group of two or more people related by birth, marriage, or adoption who reside together.」Explain carefully why mean incomes are higher than median incomes and why family incomes are higher than household incomes.

12.11 Rich magazine readers. Seattle Magazine reports that the average income of its readers is $240,000. Is the median wealth of these readers greater or less than $240,000? Why?

12.12 College tuition. Figure 11.7 (page 254) is a stemplot of the tuition charged by 114 colleges in Illinois. The stems are thousands of dollars and the leaves are hundreds of dollars. For example, the highest tuition is $53,600 and appears as leaf 6 on stem 53.

Find the five-number summary of Illinois college tuitions. You see that the stemplot already arranges the data in order.

Would the mean tuition be clearly smaller than the median, about the same as the median, or clearly larger than the median? Why?

12.13 Where are the young more likely to live? Figure 11.11 (page 258) is a stemplot of the percentage of residents aged 18 to 34 in each of the 50 states. The stems are whole percents and the leaves are tenths of a percent.

The shape of the distribution suggests that the mean will be about the same as the median. Why?

Find the mean and median of these data and verify that the mean and the median are similar.

12.14 Gas mileage. Table 11.2 (page 261) gives the highway gas mileages for some model year 2015 midsized cars.

Make a stemplot of these data if you did not do so in Exercise 11.13.

Find the five-number summary of gas mileages. Which cars are in the bottom quarter of gas mileages?

The stemplot shows a fact about the overall shape of the distribution that the five-number summary cannot describe. What is it?

12.15 Twins money. Table 11.4 (page 262) gives the salaries of the Minnesota Twins baseball team. What shape do you expect the distribution to have? Do you expect the mean salary to be close to the median, clearly higher, or clearly lower? Verify your choices by making a graph and calculating the mean and median.

12.16 The richest 5%. The distribution of individual incomes in the United States is strongly skewed to the right. In 2016, if we only look at the incomes of the top 5% of Americans, the mean and median incomes of the individuals in the top 5% were $215,000 and $375,000. Which of these numbers is the mean and which is the median? Explain your reasoning.

12.17 How many calories does a hot dog have? Consumer Reports magazine presented the following data on the number of calories in a hot dog for each of 17 brands of meat hot dogs:

173 191 182 190 172 147 146 139 175

136 179 153 107 195 135 140 138

Make a stemplot if you did not already do so in Exercise 11.19 (page 263), and find the five-number summary. The stemplot shows important facts about the distribution that the numerical summary does not tell us. What are these facts?

12.18 Returns on common stocks. Example 5 informs us that financial theory uses the mean and standard deviation to describe the returns on investments. Figure 11.13 (page 260) is a histogram of the returns of all New York Stock Exchange common stocks in one year. Are the mean and standard deviation suitable as a brief description of this distribution? Why?

12.19 The Super Bowl MVP. Figure 11.12 (page 259) is a histogram of the ages of players who have been named a Super Bowl Most Valuable Player (MVP) for the first 52 Super Bowl Games. The classes for Figure 11.12 are 22–23.5, 23.6–25, and so on.

What is the position of each number in the five-number summary in a list of 52 observations arranged from smallest to largest?

Even without the actual data, you can use your answer to (a) and the histogram to give the five-number summary approximately. Do this. About how old must an MVP be in order to be in the top quarter?

12.20 The statistics of writing style. Here are data on the percentages of words of 1 to 15 letters used in articles in Popular Science magazine. Exercise 11.16 (page 261) asked you to make a histogram of these data.

Length: 1 2 3 4 5 6 7 8

Percent: 3.6 14.8 18.7 16.0 12.5 8.2 8.1 5.9

Length: 9 10 11 12 13 14 15

Percent: 4.4 3.6 2.1 0.9 0.6 0.4 0.2

Find the five-number summary of the distribution of word lengths from this table.

12.21 Immigrants in the eastern states. Here are the number of legal immigrants (in thousands) who settled in each state east of the Mississippi River in 2017:

Alabama 3.8 New Hampshire 2.3

Connecticut 11.9 New Jersey 54.4

Delaware 2.2 New York 139.4

Florida 127.6 North Carolina 21.1

Georgia 26.2 Ohio 16.9

Illinois 40.5 Pennsylvania 27.8

Indiana 10.1 Rhode Island 4.1

Kentucky 7.5 South Carolina 5.0

Maine 1.6 Tennessee 9.8

Maryland 25.1 Vermont 0.8

Massachusetts 37.0 Virginia 29.5

Michigan 18.9 West Virginia 0.8

Mississippi 1.8 Wisconsin 6.7

Make a graph of the distribution. Describe its overall shape and any outliers. Then choose and calculate a suitable numerical summary.

12.22 Immigrants in the eastern states. New York and Florida are high outliers in the distribution of the previous exercise. Find the mean and the median for these data with and without New York and Florida. Which measure changes more when we omit the outliers?

12.23 State SAT scores. Figure 12.9 is a histogram of the average scores on the SAT Mathematics exam for college-bound senior students in the 50 states and the District of Columbia in 2018. The distinctive overall shape of this distribution implies that a single measure of center such as the mean or the median is of little value in describing the distribution. Explain why this is true.

Figure 12.9 Histogram of the average scores on the SAT Mathematics exam for college-bound senior students in the 50 states and the District of Columbia in 2018, Exercise 12.23.

Data in the histogram are as follows:

State average, 460 to 480; Number of students, Blank

State average, 480 to 500; Number of students, 5.8

State average, 500 to 520; Number of students, 5.8

State average, 520 to 540; Number of students, 9.8

State average, 540 to 560; Number of students, 8.4

State average, 560 to 580; Number of students, 4.5

State average, 580 to 600; Number of students, 2

State average, 600 to 620; Number of students, 4.5

State average, 620 to 640; Number of students, 4.5

State average, 640 to 660; Number of students, 3

All the data given is approximate.

12.24 Highly paid athletes. A news article reported that of the 446 players on National Basketball Association rosters in 2015, only 146 made more than $5 million. The article also stated that the average NBA salary in 2015 was $5.2 million. Was $5.2 million the mean or median salary for NBA players? How do you know?

12.25 Mean or median? Which measure of center, the mean or the median, should you use in each of the following situations? Why?

Middletown is considering imposing an income tax on citizens. The city government wants to know the average income of citizens so that it can estimate the total tax base.

In a study of the standard of living of typical families in Middletown, a sociologist estimates the average family income in that city.

12.26 Mean or median? You are planning a party and want to know how many cans of soda to buy. A genie offers to tell you either the mean number of cans guests will drink or the median number of cans. Which measure of center should you ask for? Why? To make your answer concrete, suppose there will be 30 guests and the genie will tell you either cans or cans. Which of these two measures would best help you determine how many cans you should have on hand?

12.27 State SAT scores. We want to compare the distributions of average SAT Math and Evidence-Based Reading and Writing (ERW) scores for the states and the District of Columbia. We enter these data into a computer with the names SATM for Math scores and SATERW for Evidence-Based Reading and Writing scores. Below is output from the statistical software package Minitab. (Other software produces similar output. Some software uses rules for finding the quartiles that differ slightly from ours. So software may not give exactly the answer you would get by hand.)

Use this output to make boxplots of SAT Math and Evidence-Based Reading and Writing scores for the states. Briefly compare the two distributions in words.

The data are as follows:

Variable: SATM; N:51; Mean: 557.25; Median: 547.00; StDev: 48.89; Minimum: 480.00; Maximum: 655.00; Q1: 521.00; Q3: 606.00.

Variable: SATERW; N:51; Mean: 567.29; Median: 552.00; StDev: 45.32; Minimum: 497.00; Maximum: 643.00; Q1: 535.00; Q3: 618.00.

12.28 Do SUVs waste gas? Table 11.2 (page 261) gives the highway fuel consumption (in miles per gallon) for 31 model year 2015 midsized cars. You found the five-number summary for these data in Exercise 12.14. Here are the highway gas mileages for 26 four-wheel-drive model year 2015 sport utility vehicles:

Model

mpg

BMW X5 xdrive35i 27

Chevrolet Tahoe K1500 22

Chevrolet Traverse 23

Dodge Durango 24

Ford Expedition 20

Ford Explorer 23

GMC Acadia 23

GMC Yukon 22

Infiniti QX80 19

Jeep Grand Cherokee 20

Land Rover LR4 19

Land Rover Range Rover 23

Land Rover Range Rover Sport 19

Lexus GX460 20

Lexus LX570 17

Lincoln Navigator 20

Lincoln MKT 23

Mercedes-Benz ML250 Bluetec 4matic 29

Mercedes-Benz G63 AMG 14

Nissan Armada 18

Nissan Pathfinder Hybrid 27

Porsche Cayenne S 24

Porsche Cayenne Turbo 21

Toyota Highlander 24

Toyota Land Cruiser Wagon 18

Toyota 4Runner 21

Give a graphical and numerical description of highway fuel consumption for SUVs. What are the main features of the distribution?

Make boxplots to compare the highway fuel consumption of the midsize cars in Table 11.2 and SUVs. What are the most important differences between the two distributions?

12.29 How many calories in a hot dog? Some people worry about how many calories they consume. Consumer Reports magazine, in a story on hot dogs, measured the calories in 20 brands of beef hot dogs, 17 brands of meat hot dogs, and 17 brands of poultry hot dogs. Here is computer output describing the beef hot dogs,

the meat hot dogs,

and the poultry hot dogs,

(Some software uses rules for finding the quartiles that differ slightly from ours. So software may not give exactly the answer you would get by hand.) Use this information to make boxplots of the calorie counts for the three types of hot dogs. Write a brief comparison of the distributions. Will eating poultry hot dogs usually lower your calorie consumption compared with eating beef or meat hot dogs? Explain.

12.30 Finding the standard deviation. The level of various substances in the blood influences our health. Here are measurements of the level of phosphate in the blood of a patient, in milligrams of phosphate per deciliter of blood, made on six consecutive visits to a clinic:

5.6 5.2 4.6 4.9 5.7 6.4

A graph of only six observations gives little information, so we proceed to compute the mean and standard deviation.

Find the mean from its definition. That is, find the sum of the six observations and divide by 6.

Find the standard deviation from its definition. That is, find the distance of each observation from the mean, square the distances, then calculate the standard deviation. Example 4 shows the method.

Now enter the data into your calculator and use the mean and standard deviation keys to obtain and . Do the results agree with your hand calculations?

12.31 What s measures. Use a calculator to find the mean and standard deviation of these two sets of numbers:

4 2 4 2 4 2

5 5 5 1 1 1

Which data set is more variable?

12.32 What s measures. Add 2 to each of the numbers in data set (a) in the previous exercise. The data are now 6 4 6 4 6 4.

Use a calculator to find the mean and standard deviation and compare your answers with those for data set part (a) in the previous exercise. How does adding 2 to each number change the mean? How does it change the standard deviation?

Without doing the calculation, what would happen to and if we added 10 to each value in data set part (a) of the previous exercise? (This exercise demonstrates that the standard deviation measures only variability about the mean and ignores changes in where the data are centered.)

12.33 Cars and SUVs. Use the mean and standard deviation to compare the gas mileages of mid-size cars (Table 11.2, page 261) and SUVs (Exercise 12.28). Do these numbers catch the main points of your more detailed comparison in Exercise 12.28?

12.34 A contest. This is a standard deviation contest. You must choose four numbers from the whole numbers 0 to 9, with repeats allowed.

Choose four numbers that have the smallest possible standard deviation.

Choose four numbers that have the largest possible standard deviation.

Is more than one choice correct in either (a) or (b)? Explain.

12.35 and are not enough. The mean and standard deviation measure center and variability but are not a complete description of a distribution. Data sets with different shapes can have the same mean and standard deviation. To demonstrate this fact, use your calculator to find and for these two small data sets. Then make a stemplot of each and comment on the shape of each distribution.

Data A: 9.14 8.14 8.74 8.77 9.26 8.10

Data B: 6.58 5.76 7.71 8.84 8.47 7.04

Data A: 6.13 3.10 9.13 7.26 4.74

Data B: 5.25 5.56 7.91 6.89 12.50

12.36 Raising pay. A school system employs teachers at salaries between $40,000 and $70,000. The teachers’ union and the school board are negotiating the form of next year’s increase in the salary schedule. Suppose that every teacher is given a flat $3000 raise.

How much will the mean salary increase? The median salary?

Will a flat $3000 raise increase the variability as measured by the distance between the quartiles? Explain.

Will a flat $3000 raise increase the variability as measured by the standard deviation of the salaries? Explain.

12.37 Raising pay. Suppose that the teachers in the previous exercise each receive a 5% raise. The amount of the raise will vary from $2000 to $3500, depending on present salary. Will a 5% across-the-board raise increase the variability of the distribution as measured by the distance between the quartiles? Do you think it will increase the standard deviation? Explain your reasoning.

12.38 Making colleges look good. Colleges announce an「average」SAT score for their entering freshmen. Usually the college would like this「average」to be as high as possible. A New York Times article noted,「Private colleges that buy lots of top students with merit scholarships prefer the mean, while open-enrollment public institutions like medians.」Use what you know about the behavior of means and medians to explain these preferences.

12.39 What graph to draw? We now understand three kinds of graphs to display distributions of quantitative variables: histograms, stemplots, and boxplots. Give an example (just words, no data) of a situation in which you would prefer that graphing method.

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

CHAPTER 13 Normal Distributions

In this chapter you will:

