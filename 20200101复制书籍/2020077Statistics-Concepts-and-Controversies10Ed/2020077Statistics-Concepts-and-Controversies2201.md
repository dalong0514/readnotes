Learn how to conduct tests of significance for proportions and means.

Be able to interpret the results of a test of significance.

Be able to decide if an observed difference can plausibly be attributed to chance.

Case Study: Political Views

A May 1, 2017, article in Inside Higher Education reported that first-year college students are politically more divided than ever. What was the basis for this finding?

Every year since 1985, the Higher Education Research Institute at UCLA has conducted a survey of first-year college students. The 2016 survey involved a random sample of 137,456 full-time first-year students at 184 of the nation’s baccalaureate colleges and universities. An interesting finding from the 2016 survey was that the percentage of students who reported their political views as being「middle-of-the-road」was lower than it has ever been, at 42.3%. In 2015, a random sample of 141,189 first-year students from 199 colleges and universities was surveyed, and 44.9% of these students identified their political views as being「middle-of-the-road.」

The Inside Higher Education article included a quote from Kevin Eagan, the director of the Higher Education Research Institute and the lead author of the survey reports. Eagan noted that increased political activism among first-year students seemed to intensify in the months leading up to the 2016 presidential election, and the「2016 survey points to diversity and polarity of how college freshmen perceive their place in the current political landscape.」

The sample sizes for the 2015 and 2016 surveys are both quite large. Although different percentages were reported in 2015 and 2016, changes in the percentages are small. Could it be that the difference between the two samples is just due to the luck of the draw in randomly choosing the respondents?

The Reasoning of Statistical Tests of Significance

The local hot-shot playground basketball player claims to make 80% of his free throws.「Show me,」you say. He shoots 20 free throws and makes eight of them.「Aha,」you conclude,「if he makes 80%, he would almost never make as few as 8 of 20. So I don’t believe his claim.」That’s the reasoning of statistical tests of significance at the playground level: an outcome that is very unlikely if a claim is true is good evidence that the claim is not true.

Statistical inference uses data from a sample to draw conclusions about a population. So, once we leave the playground, statistical tests deal with claims about a population. Statistical tests ask if sample data give good evidence against a claim. A statistical test says,「If we took many samples and the claim were true, we would rarely get a result like this.」To get a numerical measure of how strong the sample evidence is, replace the vague term「rarely」by a probability. Here is an example of this reasoning at work.

Example 1

Is the coffee fresh?

People of taste are supposed to prefer fresh-brewed coffee to the instant variety. But, perhaps, many coffee drinkers just need their caffeine fix. A skeptic claims that coffee drinkers can’t tell the difference. Let’s do an experiment to test this claim.

Each of 50 subjects tastes two unmarked cups of coffee and says which he or she prefers. One cup in each pair contains instant coffee; the other, fresh-brewed coffee. The statistic that records the result of our experiment is the proportion of the sample who say they like the fresh-brewed coffee better. We find that 36 of our 50 subjects choose the fresh coffee. That is,

To make a point, let’s compare our outcome with another possible result. If only 28 of the 50 subjects like the fresh coffee better than instant coffee, the sample proportion is

Surely 72% is stronger evidence against the skeptic’s claim than 56%. But how much stronger? Is even 72% in favor in a sample convincing evidence that a majority of the population prefer fresh coffee? Statistical tests answer these questions. Here’s the answer in outline form:

The claim. The skeptic claims that coffee drinkers can’t tell fresh from instant so that only half will choose fresh-brewed coffee. That is, he claims that the population proportion is only 0.5. Suppose for the sake of argument that this claim is true.

The sampling distribution (from page 489). If the claim were true and we tested many random samples of 50 coffee drinkers, the sample proportion would vary from sample to sample according to (approximately) the Normal distribution with

and

Figure 22.1 displays this Normal curve.

Figure 22.1 The sampling distribution of the proportion of 50 coffee drinkers who prefer fresh-brewed coffee if the truth about all coffee drinkers is that 50% prefer fresh coffee, Example 1. The shaded area is the probability that the sample proportion is 56% or greater.

The horizontal axis with values 0.5, sample proportion p equals 0.56, and sampling proportion p equals 0.72. A vertical line is drawn at sample proportion p equals 0.56, and it touches the declining slope of the normal curve. A callout pointing to the incline portion of the normal curve reads, Sampling distribution of sampling proportion if p equals 0.5. A callout pointing to the right hand side of the vertical line, enclosed by the curve, reads, Area equals 0.2. A callout pointing to 0.73 on the horizontal axis reads, Area equals 0.001.

The data. Place the sample proportion on the sampling distribution. You see in Figure 22.1 that isn’t an unusual value, but that is unusual. We would rarely get 72% of a sample of 50 coffee drinkers preferring fresh-brewed coffee if only 50% of all coffee drinkers felt that way. So, the sample data do give evidence against the claim.

The probability. We can measure the strength of the evidence against the claim by a probability. What is the probability that a sample gives a this large or larger if the truth about the population is that ? If , this probability is the shaded area under the Normal curve in Figure 22.1. This area is 0.20. Our sample actually gave . The probability of getting a sample outcome this large is only 0.001, an area too small to see in Figure 22.1. An outcome that would occur just by chance in 20% of all samples is not strong evidence against the claim. But an outcome that would happen only 1 in 1000 times is good evidence.

Statistics in Your World

Gotcha! A tax examiner suspects that Ripoffs, Inc., is issuing phony checks to inflate its expenses and reduce the tax it owes. To learn the truth without examining every check, she boots up her computer. The first digits of real data follow well-known patterns that do not give digits 0 to 9 equal probabilities. If the check amounts don’t follow this pattern, she will investigate. Down the street, a hacker is probing a company’s computer files. He can’t read them because they are encrypted. But he may be able to locate the key to the encryption anyway—if it’s the only long string that really does give equal probability to all possible characters. Both the tax examiner and the hacker need a method for testing whether the pattern they are looking for is present.

Be sure you understand why this evidence is convincing. There are two possible explanations of the fact that 72% of our subjects prefer fresh to instant coffee:

The skeptic is correct , and by bad luck a very unlikely outcome occurred.

In fact, the population proportion favoring fresh coffee is greater than 0.5, so the sample outcome is about what would be expected.

We cannot be certain that Explanation 1 is untrue. Our taste test results could be due to chance alone. But the probability that such a result would occur by chance is so small (0.001) that we are quite confident that Explanation 2 is right.

Hypotheses and P-values

Tests of significance refine (and perhaps hide) this basic reasoning. In most studies, we hope to show that some definite effect is present in the population. In Example 1, we suspect that a majority of coffee drinkers prefer fresh-brewed coffee. A statistical test begins by supposing for the sake of argument that the effect we seek is not present. We then look for evidence against this supposition and in favor of the effect we hope to find. The first step in a test of significance is to state a claim that we will try to find evidence against.

Key Terms

The claim being tested in a statistical test is called the null hypothesis . The test is designed to assess the strength of the evidence against the null hypothesis. Usually, the null hypothesis is a statement of「no effect」or「no difference.」

The term「null hypothesis」is abbreviated and is read as「H-nought,」「H-oh,」and sometimes even「H-null.」It is a statement about the population and so must be stated in terms of a population parameter. In Example 1, the parameter is the proportion of all coffee drinkers who prefer fresh to instant coffee. The null hypothesis is

The statement we hope or suspect is true instead of is called the alternative hypothesis and is abbreviated . In Example 1, the alternative hypothesis is that a majority of the population favors fresh coffee. In terms of the population parameter, this is

Key Terms

The probability, computed assuming that is true, that the sample outcome would be as extreme or more extreme than the actually observed outcome is called the P-value of the test. The smaller the P-value is, the stronger is the evidence against provided by the data.

A significance test looks for evidence against the null hypothesis and in favor of the alternative hypothesis. The evidence is strong if the outcome we observe would rarely occur if the null hypothesis is true but is more probable if the alternative hypothesis is true. For example, it would be surprising to find 36 of 50 subjects favoring fresh coffee if, in fact, only half of the population feel this way. How surprising? A significance test answers this question by giving a probability: the probability of getting an outcome at least as extreme or more extreme than the actually observed outcome from what we would expect when is true. What counts as「at least as extreme or more extreme」depends on as well as . In the taste test, the probability we want is the probability that 36 or more of 50 subjects favor fresh coffee. If the null hypothesis is true, this probability is very small (0.001). That’s good evidence that the null hypothesis is not true.

In practice, most statistical tests are carried out by computer software that calculates the P-value for us. It is usual to report the P-value in describing the results of studies in many fields. You should, therefore, understand what P-values say even if you don’t do statistical tests yourself, just as you should understand what「95% confidence」means even if you don’t calculate your own confidence intervals.

Example 2

Working through college

Do college students work too much? According to a 2015 report from the Georgetown University Center on Education and the Workforce, 70% of college students in the United States have a full- or part-time job while enrolled in college. If we express 70% as a proportion, this means the claimed population proportion is An administrator from a local college questions the accuracy of this claim. In particular, she believes the true proportion of students at her college who have full- or part-time jobs while enrolled in college is different from 0.7. The administrator is able to survey a random sample of 325 students from her college, and she finds that 238 of these students have full- or part-time jobs. The sample proportion is

Is this evidence that the true population proportion is something different than 0.7? This is a job for a significance test.

The hypotheses. The null hypothesis says that the population proportion is The administrator believes that this value is incorrect, but she does not theorize ahead of time that the true value is higher than or lower than 0.7. She just believes the true population proportion is something different than 0.7, so the alternative hypothesis is just「the population proportion is not 0.7.」The two hypotheses are

The sampling distribution. If the null hypothesis is true, the sample proportion of college students who work full- or part-time has approximately the Normal distribution with

The data. Figure 22.2 shows this sampling distribution with the administrator’s sample outcome marked. The picture already suggests that this is not an unlikely outcome that would give strong evidence against the claim that .

Figure 22.2 The sampling distribution of the proportion of college students who report working full- or part-time, Example 2. The administrator’s sample result, 0.732, is marked.

The horizontal axis shows the values 0.7 and sampling proportion p equals 0.732. A vertical line is drawn at sampling proportion p equals 0.732, and it touches the negative slope of the normal curve. The area enclosed within the vertical line and the curve is shaded. A callout pointing to the incline portion of the bell curve reads, Sampling distribution of sampling proportion if p equals 0.7.

The P-value. How unlikely is an outcome as far from 0.7 as ? Because the alternative hypothesis allows to lie on either side of 0.7, values of far from 0.7 in either direction provide evidence against and in favor of . The P-value is, therefore, the probability that the observed lies as far from 0.7 in either direction as the observed . Figure 22.3 shows this probability as area under the Normal curve. It is .

Figure 22.3 The P-value for testing whether the proportion of college students who work full- or part-time is different than 0.7, Example 2. This is the probability, calculated assuming the null hypothesis is true, of a sample proportion as far or farther from 0.7 as the administrator’s sample result of 0.732.

The values on the horizontal axis are as follows: 0.668, 0.7, and 0.732. Two vertical lines are drawn at 0.668 and 0.732 respectively. A callout pointing to the areas enclosed by the curve and the line from 0.668 and the curve and the line from 0.732 reads. P value equals 0.19.

The conclusion. If the true population proportion is 0.7, the probability we would obtain a sample proportion this far or farther from 0.7 is 0.19. We therefore cannot reject the claim that 70% of college students work full- or part-time while attending college.

The alternative in Example 1 is a one-sided alternative because the effect we seek evidence for says that the population proportion is greater than one-half. The alternative in Example 2 is a two-sided alternative because we ask whether the population proportion p is different from 0.7. Whether the alternative is one-sided or two-sided determines whether sample results that are extreme in one direction or in both directions count as evidence against in favor of .

Now it’s your turn

22.1 Working full- or part-time. Suppose the college administrator was only able to survey a random sample of 50 students. She finds that 32 of these students report having a full- or part-time job. The sample proportion is

Is this evidence that the population proportion is not equal to 0.7? Formulate the hypotheses for an appropriate significance test and determine the sampling distribution of the sample proportion of students who work full- or part-time if the null hypothesis is true. As you are working through this problem, think about what you learned in Chapters 17 and 20 about the「law of large numbers.」Does it make sense that your sample proportion would be different with a smaller sample size?

Statistical Significance

Key Terms

If the P-value is as small or smaller than we say that the data are statistically significant at level .

We can decide in advance how much evidence against we will insist on. The way to do this is to say, before any data are collected, how small a P-value we require. The decisive value of is called the significance level. It is usual to write it as (the Greek letter alpha). If we choose , we are requiring that the data give evidence against so strong that it would happen no more than 5% of the time (one time in 20) when is true. If we choose , we are insisting on stronger evidence against evidence so strong that it would appear only 1% of the time (one time in 100) if is, in fact, true.

「Significant」in the statistical sense does not mean「important.」It means simply「not likely to happen just by chance.」We used these words in Chapter 5 (page 97). Now we have attached a number to statistical significance to say what「not likely」means. You will often see significance at level 0.01 expressed by the statement,「The results were significant .」Here, stands for the P-value.

One traditional level of significance to use is 0.05. The origins of this appear to trace back to British statistician and geneticist Sir Ronald A. Fisher. Fisher once wrote that it was convenient to consider sample statistics that are two or more standard deviations away from the mean as being significant. Of course, we don’t have to make use of traditional levels of significance such as 5% and 1%. The P-value is more informative because it allows us to assess significance at any level we choose. For example, a result with is significant at the level but not significant at the level. Nonetheless, the traditional significance levels are widely accepted guidelines for「how much evidence is enough.」We might say that indicates「some evidence」against the null hypothesis, is「moderate evidence,」and is「strong evidence.」Don’t take these guidelines too literally, however. We will say more about interpreting tests in Chapter 23.

Calculating P-values*

Key Terms

When conducting a statistical test of significance, the standard score that is computed based on the sample data is commonly referred to as a test statistic.

Finding the P-values we gave in Examples 1 and 2 requires doing Normal distribution calculations using Table B of Normal percentiles. That was optional reading in Chapter 13 (pages 304–306). In practice, software does the calculation for us, but here is an example that shows how to use Table B.

Example 3

Tasting coffee

The hypotheses. In Example 1, we want to test the hypotheses

Here, is the proportion of the population of all coffee drinkers who prefer fresh coffee to instant coffee.

The sampling distribution. If the null hypothesis is true, so that , we saw in Example 1 that follows a Normal distribution with mean 0.5 and standard deviation 0.0707.

The data. A sample of 50 people found that 36 preferred fresh coffee. The sample proportion is .

The P-value. The alternative hypothesis is one-sided on the high side. So, the P-value is the probability of getting an outcome at least as large as 0.72. Figure 22.1 displays this probability as an area under the Normal sampling distribution curve. To find any Normal curve probability, move to the standard scale. When we convert a sample statistic to a standard score when conducting a statistical test of significance, the standard score is commonly referred to as a test statistic. The test statistic for the outcome is

Table B says that standard score 3.1 is the 99.9 percentile of a Normal distribution. That is, the area under a Normal curve to the left of 3.1 (in the standard scale) is 0.999. The area to the right is therefore 0.001, and that is our P-value.

The conclusion. The small P-value means that these data provide very strong evidence that a majority of the population prefers fresh coffee.

Now it’s your turn

22.2 Working full- or part-time. Refer to Exercise 22.1 (page 519). The college administrator surveyed 50 students and observed that 32 of them worked full- or part-time, so the sample proportion is

Is this evidence that the population proportion is not equal to 0.7? For the hypotheses you formulated in Exercise 22.1, find the P-value based on the results of the survey of 50 students. Are the results significant at the 0.05 level?

*This section is optional.

Tests for a Population Mean*

The reasoning that leads to significance tests for hypotheses about a population mean follows the reasoning that leads to tests about a population proportion . The big idea is to use the sampling distribution that the sample mean would have if the null hypothesis were true. Locate the value of from your data on this distribution, and see if it is unlikely. A value of that would rarely appear if were true is evidence that is not true. The four steps are also similar to those in tests for a proportion. Here are two examples, the first one-sided and the second two-sided.

Example 4

Length of human pregnancies

Researchers have recently begun to question the actual length of a human pregnancy. According to a report published on August 6, 2013, although women are typically given a delivery date that is calculated as 280 days after the onset of their last menstrual period, only 4% of women deliver babies at 280 days. A more likely average time from ovulation to birth may be much less than 280 days. To test this theory, a random sample of 95 women with healthy pregnancies is monitored from ovulation to birth. The mean length of pregnancy is found to be days, with a standard deviation of days. Is this sample result good evidence that the mean length of a healthy pregnancy for all women is less than 280 days?

The hypotheses. The researcher’s claim is that the mean length of pregnancy is less than 280 days. That’s our alternative hypothesis, the statement we seek evidence for. The hypotheses are

The sampling distribution. If the null hypothesis is true, the sample mean has approximately the Normal distribution with mean and standard error

We once again use the sample standard deviation in place of the unknown population standard deviation .

The data. The researcher’s sample gave . The standard score, or test statistic, for this outcome is

That is, the sample result is about 4.85 standard errors below the mean we would expect if, on the average, healthy pregnancies lasted for 280 days.

The P-value. Figure 22.4 locates the sample outcome −4.85 (in the standard scale) on the Normal curve that represents the sampling distribution if is true. This curve has mean 0 and standard deviation 1 because we are using the standard scale. The P-value for our one-sided test is the area to the left of −4.85 under the Normal curve. Figure 22.4 indicates that this area is very small. The smallest value in Table B is −3.4 and Table B says that −3.4 is the 0.03 percentile, so the area to its left is 0.0003. Because −4.85 is smaller than −3.4, we know that the area to its left is smaller than 0.0003. Thus, our P-value is smaller than 0.0003.

Figure 22.4 The P-value for a one-sided test when the standard score for the sample mean is −4.85, Example 4.

The horizontal axis represents the values of x bar (standard scale). The values plotted are negative 4.85 and 0. A callout pointing at the bell curve reads, P value (area to the left of negative 4.85).

The conclusion. A P-value of less than 0.0003 is strong evidence that the mean length of a healthy human pregnancy is below the commonly reported length of 280 days.

Example 5

Time spent eating

The Bureau of Labor Statistics conducts the American Time Use Survey (ATUS). This survey is intended to provide nationally representative estimates of how, where, and with whom Americans spend their time, with approximately 26,400 households being surveyed each year since 2003. In 2017, it was reported that Americans spend an average of 1.24 hours per day eating and drinking. A researcher at a college campus in California conducts a survey of a random sample of 150 college students and finds that the average amount of time these students report eating and drinking per day is hours, with a standard deviation of hour. Is this evidence that the college students eat and drink, on average, a different amount of time each day when compared to the general population?

The hypotheses. The null hypothesis is「no difference」from the national mean. The alternative is two-sided because the researcher did not have a particular direction in mind before examining the data. So, the hypotheses about the unknown mean of the population are

The sampling distribution. If the null hypothesis is true, the sample mean has approximately the Normal distribution with mean and standard error

The data. The sample mean is . The standard score, or test statistic, for this outcome is

We know that an outcome one standard error away from the mean of a Normal distribution is not very surprising. The last step is to make this formal.

The P-value. Figure 22.5 locates the sample outcome 1 (in the standard scale) on the Normal curve that represents the sampling distribution if is true. The two-sided P-value is the probability of an outcome at least this far out in either direction. This is the shaded area under the curve. Table B says that a standard score of 1.0 is the 84.13 percentile of a Normal distribution. This means the area to the left of 1.0 in the Normal curve is 0.8413. The area to the right is, therefore, 0.1587. The area to the right of 1.0 and to the left of −1.0 is double this, or about 0.3174. This is our approximate P-value.

Figure 22.5 The P-value for a two-sided test when the standard score for the sample mean is −1, Example 5.

The horizontal axis represents values of x bar (standard scale). The values plotted are negative 1, 0, and 1. Two vertical lines are drawn at negative 1 and 1 that touch the incline and negative slope of the bell curve respectively.

The conclusion. The large P-value gives us no reason to think that the mean time spent eating and drinking per day among the California college students differs from the national average.

The test assumes that the 150 students in the sample are an SRS from the population of all college students. We should check this assumption by asking how the data were produced. If the data come from a survey conducted on one particular day, in one dining hall on campus, for example, the data are of little value for our purpose. It turns out that the researcher attempted to gather a random sample by using a computer program to randomly select names from a college directory. He then sent surveys out to those students who had been chosen to participate in this study of eating habits.

What if the researcher did not draw a random sample? You should be very cautious about inference based on nonrandom samples, such as convenience samples, or random samples with large nonresponse. Although it is possible for a convenience sample to be representative of the population and, hence, yield reliable inference, establishing this is not easy. You must be certain that the method for selecting the sample is unrelated to the quantity being measured. You must make a case that individuals are independent. You must use additional information to argue that the sample is representative. This can involve comparing other characteristics of the sample to known characteristics of the population. Is the proportion of men and women in the sample about the same as in the population? Is the racial composition of the sample about the same as in the population? What about the distribution of ages or other demographic characteristics? Even after arguing that your sample appears to be representative, the case is not as compelling as that for a truly random sample. You should proceed with caution.

Statistics in Your World

Catching cheaters Lots of students take a long multiple-choice exam. Can the computer that scores the exam also screen for papers that are suspiciously similar? Clever people have created a measure that takes into account not just identical answers, but the popularity of those answers and the total score on the similar papers as well. The measure has close to a Normal distribution, and the computer flags pairs of papers with a measure outside standard deviations as significant.

The data in Example 5 do not establish that the mean time spent eating and drinking for this sample of college students is 1.24 hours. We sought evidence that differed from 1.24 hours and failed to find convincing evidence. That is all we can say. No doubt the mean time spent eating and drinking among the entire college population is not exactly equal to 1.24 hours. A large enough sample would give evidence of the difference, even if it is very small.

Now it’s your turn

22.3 IQ scores. The mean IQ for the entire population in any age group is supposed to be 100. Suppose that we measure the IQ of 45 seventh-grade students in a Midwest school district and find a sample mean of 105.8 and sample standard deviation of 14.3. Treat the scores as if they were an SRS from all middle-school students in this district. Do the scores provide good evidence that the mean IQ of this population is not 100?

*This section is optional.

Chapter 22 Summary and Exercises

Chapter 22: Statistics in Summary

A confidence interval estimates an unknown parameter. A test of significance assesses the evidence for some claim about the value of an unknown parameter.

In practice, the purpose of a statistical test is to answer the question,「Could the effect we see in the sample just be an accident due to chance, or is it good evidence that the effect is really there in the population?」

Significance tests answer this question by giving the probability that a sample effect as large as the one we see in this sample would arise just by chance. This probability is the P-value. A small P-value says that our outcome is unlikely to happen just by chance.

To set up a test, state a null hypothesis that says the effect you seek is not present in the population. The alternative hypothesis says that the effect is present.

The P-value is the probability, calculated taking the null hypothesis to be true, of an outcome as extreme in the direction specified by the alternative hypothesis as the actually observed outcome.

A sample result is statistically significant at the 5% level (or at the 0.05 level) if it would occur just by chance no more than 5% of the time in repeated samples.

This chapter summary will help you evaluate the Case Study.

Link It

In this chapter, we discuss tests of significance, another type of statistical inference. The mathematics of probability, in particular the sampling distributions discussed in Chapter 18, provides the formal basis for a test of significance. The sampling distribution allows us to assess「probabilistically」the strength of evidence against a null hypothesis, through either a level of significance or a P-value. The goal of hypothesis testing, which is used to assess the evidence provided by data about some claim concerning a population, is different from the goal of confidence interval estimation, discussed in Chapter 21, which is used to estimate a population parameter.

Although we have applied the reasoning of tests of significance to population proportions and population means, the same reasoning applies to tests of significance for other population parameters, such as the correlation coefficient, in more advanced settings. In the next chapter, we provide more discussion of the practical interpretation of statistical tests.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study. Start by reviewing the Chapter Summary. Then answer each of the following questions in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying. Could the 2015 and 2016 random samples in the Higher Education Research Institute’s surveys of college freshmen differ by 44.9% versus 42.3% just by chance? Tests of significance can help answer these questions. In both cases, one finds that the P-values for the tests of whether two such random samples would differ by the amounts reported was less than 0.001.

Using language that can be understood by someone who knows no statistics, write a paragraph explaining what a P-value of less than 0.001 means in the context of the Higher Education Research Institute’s surveys of college freshmen.

Are the results of the study significant at the 0.05 level? At the 0.01 level? Explain.

In this chapter you have:

Learned how to conduct tests of significance for proportions and means.

Interpreted the results of tests of significance.

Determined how to decide if an observed difference can plausibly be attributed to chance.

Online Resources

The Snapshots Video, Hypothesis Tests, discusses the basic reasoning of tests of significance in the context of an example involving discrimination.

The StatClips Video, P-value Interpretation, discusses the interpretation of a P-value in the context of an example of a hypothesis test for a population mean.

Check the Basics

For Exercise 22.1, see page 519; for Exercise 22.2, see page 521; and for Exercise 22.3, see page 526.

22.4 Watching the news. In 2018, the Pew Research Center published a report in which it was claimed that 44% of adults in the United States prefer watching the news on television as opposed to reading it or listening to it on the radio. A researcher believes that significantly more than 44% of adults prefer watching the news on television. To test his theory, he obtains data from a random sample of 327 adults, and it is observed that 53% of this sample prefers watching the news on television. As a first step in conducting a statistical test of significance, the researcher will write a null hypothesis. In this example, the null hypothesis should be what?

22.5 College students and the Internet. It is reported that college students spend an average of 100 minutes per day on the Internet. An educational technologist disputes this claim and believes that college students spend more than an average of 100 minutes per day on the Internet. When a random sample of data is obtained and a statistical test of significance is conducted, it is observed that the P-value is 0.01. What is the correct decision to reach based on this P-value?

The data provide strong evidence that null hypothesis must be true.

The data provide strong evidence that the alternative hypothesis must be true.

The data provide strong evidence against the null hypothesis.

The data provide strong evidence against the alternative hypothesis.

22.6 Statistical significance. If the results of a statistical test are considered to be statistically significant, what does this mean?

The results are important.

The results are not likely to happen just by chance.

The P-value is large.

The alternative hypothesis is true.

22.7 Pulse rates. Suppose that a report by a leading medical organization claims that the healthy human heart beats an average of 72 times per minute. Advances in science have led some researchers to question if the healthy human heart beats an entirely different amount of time, on average, per minute. They obtain pulse rate data from a sample of 85 healthy adults and find the average number of heart beats per minute to be 76, with a standard deviation of 13. Before conducting a statistical test of significance, this outcome needs to be converted to a standard score, or a test statistic. What would that test statistic be?

0.3

−0.3

2.8

−2.8

Chapter 22 Exercises

22.8 Ethnocentrism. A social psychologist reports,「In our sample, ethnocentrism was significantly higher among church attenders than among nonattenders.」Explain to someone who knows no statistics what this means.

22.9 Students’ earnings. The financial aid office of a university asks a sample of students about their employment and earnings. The report says,「For academic year earnings, a significant difference was found between the sexes, with men earning more on average than women. No difference was found between the earnings of black and white students.」Explain both of these conclusions for the effects of sex and of race on mean earnings, in language understandable to someone who knows no statistics.

22.10 Diet and diabetes. Does eating more fiber reduce the blood cholesterol level of patients with diabetes? A randomized clinical trial compared normal and high-fiber diets. Here is part of the researchers’ conclusion:「The high-fiber diet reduced plasma total cholesterol concentrations by 6.7 percent , triglyceride concentrations by 10.2 percent , and very-low-density lipoprotein cholesterol concentrations by 12.5 percent .」A doctor who knows no statistics says that a drop of 6.7% in cholesterol isn’t a lot—maybe it’s just an accident due to the chance assignment of patients to the two diets. Explain in simple language how「」answers this objection.

22.11 Diet and bowel cancer. It has long been thought that eating a healthier diet reduces the risk of bowel cancer. A large study cast doubt on this advice. The subjects were 2079 people who had polyps removed from their bowels in the past six months. Such polyps may lead to cancer. The subjects were randomly assigned to a low-fat, high-fiber diet or to a control group in which subjects ate their usual diets. Did polyps reoccur during the next four years?

Outline the design of this experiment.

Surprisingly, the occurrence of new polyps「did not differ significantly between the two groups.」Explain clearly what this finding means.

22.12 Pigs and prestige in ancient China. It appears that pigs in Stone Age China were not just a source of food. Owning pigs was also a display of wealth. Evidence for this comes from examining burial sites. If the skulls of sacrificed pigs tend to appear along with expensive ornaments, that suggests that the pigs, like the ornaments, signal the wealth and prestige of the person buried. A study of burials from around 3500 B.C. concluded that「there are striking differences in grave goods between burials with pig skulls and burials without them… . A test indicates that the two samples of total artifacts are significantly different at the 0.01 level.」Explain clearly why「significantly different at the 0.01 level」gives good reason to think that there really is a systematic difference between burials that contain pig skulls and those that lack them.

22.13 Ancient Egypt. Settlements in Egypt before the time of the pharaohs are dated by measuring the presence of forms of carbon that decay over time. The first datings of settlements in the Nagada region used hair that had been excavated 60 years earlier. Now researchers have used newer methods and more recently excavated material. Do the dates differ? Here is the conclusion about one location:「There are two dates from Site KH6. Statistically, the two dates are not significantly different. They provide a weighted average corrected date of B.C.」Explain to someone interested in ancient Egypt but not interested in statistics what「not significantly different」means.

22.14 What’s a gift worth? Do people value gifts from others more highly than they value the money it would take to buy the gift? We would like to think so because we hope that「the thought counts.」A survey of 209 adults asked them to list three recent gifts and then asked,「Aside from any sentimental value, if, without the giver ever knowing, you could receive an amount of money instead of the gift, what is the minimum amount of money that would make you equally happy?」It turned out that most people would need more money than the gift cost to be equally happy. The magic words「significant 」appear in the report of this finding.

The sample consisted of students and staff in a graduate program and of「members of the general public at train stations and airports in Boston and Philadelphia.」The report says this sample is「not ideal.」What’s wrong with the sample?

In simple language, what does it mean to say that the sample thought their gifts were worth「significantly more」than their actual cost?

Now be more specific: what does「significant 」mean?

22.15 Attending church. A recent survey by a national polling firm finds that 39% of American adults say they attended religious services last week. There is reason to suspect this percentage is not accurate.

Why might we expect answers to a poll about attending religious services to overstate true church attendance?

You suspect strongly that the true percentage attending church in any given week is less than 39%. You plan to watch a random sample of adults and see whether or not they go to church. What are your null and alternative hypotheses? (Be sure to say in words what the population proportion is for your study.)

22.16 Body temperature. We have all heard that 98.6 degrees Fahrenheit (or 37 degrees Celsius) is「normal body temperature.」In fact, there is evidence that most people have a slightly lower body temperature. You plan to measure the body temperature of a random sample of people very accurately. You hope to show that a majority have temperatures lower than 98.6 degrees.

Say clearly what the population proportion stands for in this setting.

In terms of , what are your null and alternative hypotheses?

22.17 Unemployment. The national unemployment rate in a recent month was 5.1%. You think the rate may be different in your city, so you plan a sample survey that will ask the same questions as the Current Population Survey. To see if the local rate differs significantly from 5.1%, what hypotheses will you test?

22.18 Living on campus. A UCLA survey of college freshmen in the 2016–2017 academic year found that 74.8% of all first-year college students planned to live on campus. You wonder if this percentage is different at your school, but you have no idea whether it is higher or lower. You plan a sample survey of first-year students at your school. What hypotheses will you test to see if your school differs significantly from the UCLA survey result?

22.19 Do our athletes graduate? The National Collegiate Athletic Association (NCAA) requires colleges to report the graduation rates of their athletes. At one large university, 82% of all students who entered in 2012 graduated within six years. One hundred forty-nine of the 190 students who entered with athletic scholarships graduated. Consider these 190 as a sample of all athletes who will be admitted under present policies. Is there evidence that the percentage of athletes who graduate is less than 82%?

Explain in words what the parameter is in this setting.

What are the null and alternative hypotheses and ?

What is the numerical value of the sample proportion ? The P-value is the probability of what event?

The P-value is . Explain whether or not this P-value indicates there is some reason to think that graduation rates are lower among athletes than among all students.

22.20 AP courses. In 2016, 17.6% of first-year college students responding to a national survey said that they had not taken any Advanced Placement (AP) courses in high school. Administrators at a large state university believe that more than 17.6% of their first-year students have not taken any AP courses. They find that 46 of an SRS of 200 of the university’s first-year students said that they had not taken any AP courses in high school. Is the proportion of first-year students at this university who said they had not taken any AP courses significantly larger than the 2016 national value of 17.6%?

Explain in words what the parameter is in this setting.

What are the null and alternative hypotheses and ?

What is the numerical value of the sample proportion ? The P-value is the probability of what event?

The P-value is . Explain carefully why this evidence should lead administrators to reject .

22.21 Vote for the best face? We often judge other people by their faces. It appears that some people judge candidates for elected office by their faces. Psychologists showed head-and-shoulders photos of the two main candidates in 32 races for the U.S. Senate to many subjects (dropping subjects who recognized one of the candidates) to see which candidate was rated「more competent」based on nothing but the photos. On election day, the candidates whose faces looked more competent won 22 of the 32 contests. If faces don’t influence voting, half of all races in the long run should be won by the candidate with the better face. Is there evidence that the proportion of times the candidate with the better face wins is more than 50%?

Explain in words what the parameter is in this setting.

What are the null and alternative hypotheses and ?

What is the numerical value of the sample proportion ? The P-value is the probability of what event?

The P-value is . Explain carefully why this is reasonably good evidence that may not be true and that may be true.

22.22 Do our athletes graduate? Is the result of Exercise 22.19 statistically significant at the 10% level? At the 5% level?

22.23 AP courses. Is the result of Exercise 22.20 statistically significant at the 5% level? At the 1% level?

22.24 Vote for the best face? Is the result of Exercise 22.21 statistically significant at the 5% level? At the 1% level?

22.25 Significant at what level? Explain in plain language why a result that is significant at the 1% level must always be significant at the 5% level. If a result is significant at the 5% level, what can you say about its significance at the 1% level?

22.26 Significance means what? Asked to explain the meaning of「statistically significant at the level,」a student says:「This means that the probability that the null hypothesis is true is less than 0.05.」Is this explanation correct? Why or why not?

22.27 Finding a P-value by simulation. Is a new method of teaching reading to first-graders (Method B) more effective than the method now in use (Method A)? You design a matched pairs experiment to answer this question. You form 20 pairs of first-graders, with the two children in each pair carefully matched by IQ, socioeconomic status, and reading-readiness score. You assign at random one student from each pair to Method A. The other student in the pair is taught by Method B. At the end of first grade, all the children take a test to determine their reading skill. Assume that the higher the score on this test, the more proficient the student is at reading. Let stand for the proportion of all possible matched pairs of children for which the child taught by Method B has the higher score. Your hypotheses are

The result of your experiment is that Method B gave the higher score in 12 of the 20 pairs, or .

If is true, the 20 pairs of students are 20 independent trials with probability 0.5 that Method B「wins」each trial (is the more effective method). Explain how to use Table A to simulate these 20 trials if we assume for the sake of argument that is true.

Use Table A, starting at line 105, to simulate 10 repetitions of the experiment. Estimate from your simulation the probability that Method B will do better (be the more effective method) in 12 or more of the 20 pairs when is true. (Of course, 10 repetitions are not enough to estimate the probability reliably. Once you understand the idea, more repetitions are easy.)

Explain why the probability you simulated in part (b) is the P-value for your experiment. With enough patience, you could find all the P-values in this chapter by doing simulations similar to this one.

22.28 Finding a P-value by simulation. A classic experiment to detect extra-sensory perception (ESP) uses a shuffled deck of cards containing five suits (waves, stars, circles, squares, and crosses). As the experimenter turns over each card and concentrates on it, the subject guesses the suit of the card. A subject who lacks ESP has probability 1-in-5 of being right by luck on each guess. A subject who has ESP will be right more often. Julie is right in 5 of 10 tries. (Actual experiments use much longer series of guesses so that weak ESP can be spotted. No one has ever been right half the time in a long experiment!)

Give and for a test to see if this result is significant evidence that Julie has ESP.

Explain how to simulate the experiment if we assume for the sake of argument that is true.

Simulate 20 repetitions of the experiment; begin at line 121 of Table A.

The actual experimental result was 5 correct in 10 tries. What is the event whose probability is the P-value for this experimental result? Give an estimate of the P-value based on your simulation. How convincing was Julie’s performance?

The following exercises concern the optional section on calculating P-values. To carry out a test, complete the steps (hypotheses, sampling distribution, data, P-value, and conclusion) illustrated in Example 3.

22.29 AP courses. Return to the study in Exercise 22.20, which found that 46 of 200 first-year students said that they had not taken any AP courses in high school. Carry out the hypothesis test described in Exercise 22.20 and compute the P-value. How does your value compare with the value given in Exercise 22.20(d)?

22.30 Interpreting scatterplots. In 2014, the Pew Research Centers American Trends Panel sought to better understand what Americans know about science. It was observed that among a random selection of 3278 adults, 2065 adults could correctly interpret a scatterplot. Is this good evidence that more than 60% of Americans are able to correctly interpret scatterplots?

22.31 Side effects. An experiment on the side effects of pain relievers assigned arthritis patients to one of several over-the-counter pain medications. Of the 420 patients who took one brand of pain reliever, 21 suffered some「adverse symptom.」

If 10% of all patients suffer adverse symptoms, what would be the sampling distribution of the proportion with adverse symptoms in a sample of 420 patients?

Does the experiment provide strong evidence that fewer than 10% of patients who take this medication have adverse symptoms?

22.32 Do chemists have more girls? Some people think that chemists are more likely than other parents to have female children. (Perhaps chemists are exposed to something in their laboratories that affects the sex of their children.) The Washington State Department of Health lists the parents’ occupations on birth certificates. Between 1980 and 1990, 555 children were born to fathers who were chemists. Of these births, 273 were girls. During this period, 48.8% of all births in Washington State were girls. Is there evidence, at a significance level of 0.05, that the proportion of girls born to chemists is higher than the state proportion?

22.33 Speeding. It often appears that most drivers on the road are driving faster than the posted speed limit. Situations differ, of course, but here is one set of data. Researchers studied the behavior of drivers on a rural interstate highway in Maryland where the speed limit was 55 miles per hour. They measured speed with an electronic device hidden in the pavement and, to eliminate large trucks, considered only vehicles less than 20 feet long. They found that 5690 out of 12,931 vehicles were exceeding the speed limit. Is this good evidence, at a significance level of 0.05, that (at least in this location) fewer than half of all drivers are speeding?

The following exercises concern the optional section on tests for a population mean. To carry out a test, complete the steps illustrated in Example 4 or Example 5.

22.34 Student attitudes. The Survey of Study Habits and Attitudes (SSHA) is a psychological test that measures students’ study habits and attitudes toward school. Scores range from 0 to 200. The mean score for U.S. college students is about 115, and the standard deviation is about 30. A teacher suspects that older students have better attitudes toward school. She gives the SSHA to 25 students who are at least 30 years old. Assume that scores in the population of older students are Normally distributed with standard deviation . The teacher wants to test the hypotheses

What is the sampling distribution of the mean score of a sample of 25 older students if the null hypothesis is true? Sketch the density curve of this distribution. (Hint: Sketch a Normal curve first, then mark the axis using what you know about locating and on a Normal curve.)

Suppose that the sample data give . Mark this point on the axis of your sketch. In fact, the outcome was . Mark this point on your sketch. Using your sketch, explain in simple language why one outcome is good evidence that the mean score of all older students is greater than 115 and why the other outcome is not.

Shade the area under the curve that is the P-value for the sample result .

22.35 Mice in a maze. Experiments on learning in animals sometimes measure how long it takes mice to find their way through a maze. The mean time is 19 seconds for one particular maze. A researcher thinks that a loud noise will cause the mice to complete the maze faster. She measures how long each of several mice takes to find its way through a maze with a noise as a stimulus. What are the null hypothesis and alternative hypothesis ?

22.36 Response time. Last year, your company’s service technicians took an average of 2.5 hours to respond to trouble calls from business customers who had purchased service contracts. Do this year’s data show a significantly different average response time? What null and alternative hypotheses should you test to answer this question?

22.37 Testing a random number generator. Our statistical software has a「random number generator」that is supposed to produce numbers scattered at random from 0 to 1. If this is true, the numbers generated come from a population with . A command to generate 100 random numbers gives outcomes with and . Is this good evidence that the mean of all numbers produced by this software is not 0.5?

22.38 Will they charge more? A bank wonders whether omitting the annual credit card fee for customers who charge at least $3000 in a year will increase the amount charged on its credit cards. The bank makes this offer to an SRS of 400 of its credit card customers. It then compares how much these customers charge this year with the amount that they charged last year. The mean increase in the sample is $246, and the standard deviation is $112. Is there significant evidence at the 1% level that the mean amount charged increases under the no-fee offer? State and and carry out a significance test. Use significance level 0.01.

22.39 Bad weather, bad tip? People tend to be more generous after receiving good news. Are they less generous after receiving bad news? The average tip left by adult Americans is 20%. Give 20 patrons of a restaurant a message on their bill warning them that tomorrow’s weather will be bad and record the tip percentage they leave. Here are the tips as a percentage of the total bill:

18.0 19.1 19.2 18.8 18.4 19.0 18.5 16.1 16.8 18.2

14.0 17.0 13.6 17.5 20.0 20.2 18.8 18.0 23.2 19.4

Suppose that tip percentages are Normal with , and assume that the patrons in this study are a random sample of all patrons of this restaurant. Is there good evidence that the mean tip percentage for all patrons of this restaurant is less than 20 when they receive a message warning them that tomorrow’s weather will be bad? State and and carry out a significance test. Use significance level 0.05.

22.40 Why should the significance level matter? On June 15, 2005, an article by Lawrence K. Altman appeared in the New York Times. The title of the article was「Studies Rebut Earlier Report on Pledges of Virginity.」The article mentioned that in two studies conducted by the Heritage Foundation, it was observed that students who took virginity pledges engaged in fewer risky sexual behaviors and had lower rates of acquiring sexually transmitted diseases. These results were at odds with the results of earlier studies that focused on the same topic, but since each study used different methods of statistical analysis, direct comparisons among the studies was difficult. One particular criticism of the new study was that the result of a statistical test at a 0.10 level of significance was reported when journals generally use a lower level of 0.05. Why might this be a concern?

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e

CHAPTER 23 Use and Abuse of Statistical Inference

In this chapter you will:

