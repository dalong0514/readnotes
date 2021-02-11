# 0301. What Do Samples Tell Us?

In this chapter you will:

Learn how and why we can generalize results from a sample to the population of interest.

Understand that results from different samples vary from each other, but that we can quantify this variability.

Understand what the statement「margin of error」means in poll results.

Case Study: Childhood Vaccinations

According to the Centers for Disease Control and Prevention (CDC), there were 349 confirmed cases of measles in 26 states and the District of Columbia. The 349 cases were the second highest to be reported in one year since measles was eliminated in the United States in 2000. (The 667 cases reported in 2014 were the highest.) As in previous years, the majority of people who got measles were unvaccinated. Vaccinating children against diseases like measles is controversial.

The debate about childhood vaccinations became a major news issue in late 2014 and early 2015 and continues to this day. As of 2019, California, Mississippi, and West Virginia are the only three states that do not allow exemptions for children to not be vaccinated for anything other than medical reasons. Other states allow exemptions for personal and religious beliefs. A Gallup Poll conducted from February 28–March 1, 2015, asked the following question:「How important is it that parents get their children vaccinated—extremely important, very important, somewhat important, or not at all important?」Gallup found that 54% of respondents said「extremely important」(down from 64% who responded to a similar 2001 Gallup Poll). Can we trust this conclusion?

Reading further, we find that Gallup talked with 1015 randomly selected adults to reach these conclusions. We’re happy Gallup chooses at random—we wouldn’t get unbiased information about the importance of childhood vaccinations by asking people attending a conference of the American Medical Association. However, the U.S. Census Bureau said that there were about 247 million adults in the United States in 2015. How can 1015 people, even a random sample of 1015 people, tell us about the opinions of 247 million people? Is 54% who feel that it is extremely important for parents to get their children vaccinated evidence that, in fact, the majority of Americans feel this way? By the end of this chapter, you will learn the answers to these questions.

The material in this chapter will provide you with the tools to address the Case Study and other statistical poll results you encounter.

From Sample to Population

Gallup’s 2015 finding that「a slight majority of Americans, 54%, say it is extremely important that parents get their children vaccinated」makes a claim about the population of 247 million American adults. But Gallup doesn’t know the truth about the entire population because we cannot obtain the opinions of all American adults. The poll contacted 1015 people and found that 54% of those contacted said it is extremely important for parents to vaccinate their children. Because the sample of 1015 people was chosen at random, it’s reasonable to think that they represent the entire population pretty well. So Gallup turns the fact that 54% of the sample feel childhood vaccinations are extremely important into an estimate that about 54% of all American adults feel childhood vaccinations are extremely important. This is a basic move in Statistics: use a fact about a sample to estimate the truth about the whole population. To think about such moves, we must be clear whether a number describes a sample or a population. See the key terms box for the vocabulary we use.

So parameter is to population as statistic is to sample. Want to estimate an unknown population parameter? Choose a sample from the population and use a statistic as your estimate. That’s what Gallup did.

Key Terms

A parameter is a number that describes the population. A parameter is a fixed number, but in practice we don’t know the actual value of this number because we cannot access the entire population.

A statistic is a number that describes a sample. The value of a statistic can be determined and is known once we have taken a sample, but its value can change from sample to sample. We often use a statistic to estimate an unknown parameter.

Example 1

Should children be vaccinated?

The proportion of all American adults who feel childhood vaccinations are extremely important is a parameter describing the population of 247 million adults. Call it p, for「proportion.」Alas, we do not know the numerical value of p. To estimate p, Gallup took a sample of 1015 adults. The proportion of the sample who favor such an amendment is a statistic. Call it read as「p-hat.」It happens that 548 of this sample of size 1015 said that they feel childhood vaccines are extremely important, so for this sample,

Because all American adults had the same chance to be among the chosen 1015, it seems reasonable to use the statistic as an estimate of the unknown parameter p. It’s a fact that 54% of the sample feel childhood vaccines are extremely important—we know because we asked them. We don’t know what percentage of all American adults feel this way, but we estimate that about 54% do.

Sampling Variability

If Gallup took a second random sample of 1015 adults, the new sample would have different people in it. It is almost certain that there would not be exactly 548 respondents who feel that childhood vaccines are extremely important. That is, the value of the statistic will vary from sample to sample. Could it happen that one random sample finds that 54% of American adults feel childhood vaccines are extremely important and a second random sample finds that only 41% feel the same? Random samples eliminate bias from the act of choosing a sample, but they can still be wrong because of the variability that results when we choose at random. If the variation when we take repeated samples from the same population is too great, we can’t trust the results of any one sample.

We are saved by the second great advantage of random samples. The first advantage is that choosing at random eliminates favoritism. That is, random sampling attacks bias. The second advantage is that if we took lots of random samples of the same size from the same population, the variation from sample to sample would follow a predictable pattern. This predictable pattern shows that results of bigger samples are less variable than the results of smaller samples.

Example 2

Lots and lots of samples

Here’s another big idea of Statistics: to see how trustworthy one sample is likely to be, ask what would happen if we took many samples from the same population. Let’s try it and see. Suppose that, in fact (unknown to Gallup), exactly 50% of all American adults feel childhood vaccines are extremely important. That is, the truth about the population is that . What if Gallup used the sample proportion from a simple random sample (SRS) of size 100 to estimate the unknown value of the population proportion ?

Figure 3.1 illustrates the process of choosing many samples of the same size and finding for each one. In the first sample, 56 of the 100 people felt childhood vaccines are extremely important so . Only 36 in the next sample felt childhood vaccines are extremely important, so for that sample . Choose 1000 samples and make a plot of the 1000 values of like the graph (called a histogram) at the right of Figure 3.1. The different values of the sample proportion run along the horizontal axis. The height of each bar shows how many of our 1000 samples gave the group of values on the horizontal axis covered by the bar. For example, in Figure 3.1 the bar covering the values between 0.40 and 0.42 has a height of slightly over 50. Thus, over 50 of our 1000 samples had values between 0.40 and 0.42.

Figure 3.1 The results of many SRSs have a regular pattern. Here, we draw 1000 SRSs of size 100 from the same population. The population proportion is . The sample proportions vary from sample to sample, but their values center at the truth about the population.

The approximate data of the graph is as follows: The values of sample proportion is represented along the horizontal axis and its values range from 0.35 to 0.65 at an interval of 0.05. The number of samples is represented along the vertical axis and its values range from 0 to 200 at an interval of 50. The bars are as follows: (0.40,50), (0.43,55), (0.45,48), (0.46,175), (0.47,150), (0.50,148), (0.53,53), (0.55,100), (0.56,100), (0.60,0.10), (0.63,0.02), and (0.65,0.01). To the left of the graph, the text is as follows: SRS n equals 100 p equals 0.56, SRS n equals 100, p equals 0.36, SRS n equals 100 p equals 0.61. An illustration shows a group of people representing the population. The formula below reads p equals 0.50.

Of course, Gallup interviewed 1015 people, not just 100. Figure 3.2 shows the results of 1000 SRSs, each of size 1015, drawn from a population in which the true (population) proportion is . Figures 3.1 and 3.2 are drawn on the same scale. Comparing them shows what happens when we increase the size of our samples from 100 to 1015.

Figure 3.2 Draw 1000 SRSs of size 1015 from the same population as in Figure 3.1. The 1000 values of the sample proportion are much less variable (spread out) than was the case for smaller samples.

The approximate data of the graph is as follows: The values of the sample proportion is represented along the horizontal axis and its values range from 0.35 to 0.65 at an interval of 0.05. The number of samples is represented along the vertical axis and its values range from 0 to 500 at an interval of 100. The bars are as follows: (0.46,25), (0.47,490), (0.50,493), and (0.53,25). To the left of the graph, text reads – SRS n equals 1015 p hat equals 0.509. SRS n equals 1015 p hat equals 0.525. SRS n equals 1015 p hat equals 0.479. An illustration shows a group of people representing the population. The formula below the illustration reads p hat equals 0.50.

Look carefully at Figures 3.1 and 3.2. We flow from the population, to many samples from the population, to the many values of from these many samples. Gather these values together and study the histograms that display them.

In both cases, the values of the sample proportion vary from sample to sample, but the values are centered at 0.5. Recall we are assuming that is the true population parameter. Some samples have a less than 0.5 and some greater, but there is no tendency to be always low or always high. That is, has no bias as an estimator of . This is true for both large and small samples.

The values of from samples of size 100 are much more variable than the values from samples of size 1015. In fact, 95% of our 1000 samples of size 1015 have a lying between 0.4692 and 0.5308. That’s within 0.0308 on either side of the population truth 0.5. Our samples of size 100, on the other hand, spread the middle 95% of their values between 0.40 and 0.60. That goes out 0.10 from the truth, about three times as far as the larger samples. So larger random samples have less variability than smaller samples.

The result is that we can rely on a sample of size 1015 to almost always give an estimate that is close to the truth about the population. Figure 3.2 illustrates this fact for just one value of the population proportion, but it is true for any population proportion. Samples of size 100, on the other hand, might give an estimate of 40% or 60% when the truth is 50%.

Thinking about Figures 3.1 and 3.2 helps us restate the idea of bias when we use a statistic like to estimate a parameter like . It also reminds us that variability matters as much as bias.

Two types of error in estimation

Bias is consistent, repeated deviation of the sample statistic from the population parameter in the same direction when we take many samples. In other words, bias is a systematic overestimate or underestimate of the population parameter.

Variability describes how the values of the sample statistic will vary when we take many samples. Large variability means that the result of sampling is not repeatable.

A good sampling method has both small bias and small variability.

We can think of the true value of the population parameter as the bull’s-eye on a target and of the sample statistic as an arrow fired at the bull’s-eye. Bias and variability describe what happens when an archer fires many arrows at the target. Bias means that the aim is off, and the arrows land consistently off the bull’s-eye in the same direction. The sample values do not center about the population value. Large variability means that repeated shots are widely scattered on the target. Repeated samples do not give similar results but differ widely among themselves. Figure 3.3 shows this target illustration of the two types of error.

Figure 3.3 Bias and variability in shooting arrows at a target. Bias means the archer systematically misses in the same direction. More variability means that the arrows are more scattered.

The first one has dots on the outermost circle, and is labelled ‘Large bias, small variability’. The second one has few dots at the inner circle, and is labelled ‘Small bias, large variability’. The third one has few dots in the outermost circle and outside the target, and is labelled ‘Large bias, large variability’. The fourth one has few dots at the core and is labelled ‘Small bias, small variability’.

Notice that small variability (repeated shots are close together) can accompany large bias (the arrows are consistently away from the bull’s-eye in one direction). And small bias (the arrows center on the bull’s-eye) can accompany large variability (repeated shots are widely scattered). A good sampling scheme, like a good archer, must have both small bias and small variability.

Managing bias and variability

To reduce bias, use random sampling. When we start with a list of the entire population, simple random sampling produces unbiased estimates: the values of a statistic computed from a simple random sample (SRS) neither consistently overestimate nor consistently underestimate the value of the population parameter.

To reduce the variability of an SRS, use a larger sample. You can make the variability as small as you want by taking a large enough sample.

In practice, Gallup takes only one sample. We don’t know how close to the truth an estimate from this one sample is because we don’t know what the truth about the population is. But large random samples almost always give an estimate that is close to the truth. Looking at the pattern of many samples shows how much we can trust the result of one sample.

Margin of Error and All That

The「margin of error」that sample surveys announce translates sampling variability of the kind pictured in Figures 3.1 and 3.2 into a statement of how much confidence we can have in the results of a survey. Let’s start with the kind of language we hear so often in the news.

What margin of error means

「Margin of error plus or minus 4 percentage points」is shorthand for this statement:

If we took many samples using the same method we used to get this one sample, 95% of the samples would give a result within plus or minus 4 percentage points of the truth about the population.

Note:「Margin of error」does not mean we made a mistake in our sampling methods; rather, it represents the natural sampling variability like that seen in Figures 3.1 and 3.2.

Take this step-by-step. A sample chosen at random will usually not estimate the truth about the population exactly. We need a margin of error to tell us how close our estimate comes to the truth. But we can’t be certain that the truth differs from the estimate by no more than the margin of error. Although 95% of all samples come this close to the truth, 5% miss by more than the margin of error. We don’t know the truth about the population, so we don’t know if our sample is one of the 95% that hit or one of the 5% that miss. We say we are 95% confident that the truth lies within the margin of error.

Example 3

Understanding the news

Here’s what the TV news announcer says:「A new Gallup Poll finds that a slight majority of 54% of American adults feel it is extremely important that parents vaccinate their children. The margin of error for the poll was 4 percentage points.」Plus or minus 4% starting at 54% is 50% to 58%. Most people think Gallup claims that the truth about the entire population lies in that range.

This is what the results from Gallup actually mean:「For results based on a sample of this size, one can say with 95% confidence that the error attributable to sampling and other random effects could be plus or minus 4 percentage points for American adults.」That is, Gallup tells us that the margin of error includes the truth about the entire population for only 95% of all its samples.「95% confidence」is shorthand for that. The news report left out the「95% confidence.」

Finding the margin of error exactly is a job for statisticians. You can, however, use a simple formula to get a rough idea of the size of a sample survey’s margin of error. The reasoning behind this formula and an exact calculation of the margin of error are discussed in Chapter 21. For now, we introduce a quick and approximate calculation for the margin of error.

A quick and approximate method for the margin of error

Use the sample proportion from a simple random sample of size to estimate an unknown population proportion . The margin of error for 95% confidence is approximately equal to .

Example 4

Calculating the margin of error

The Gallup Poll in Example 1 interviewed 1015 people. The margin of error for 95% confidence will be about

Gallup announced a margin of error of 4% and our quick and approximate method gave us 3.1%. Our quick and approximate method can disagree a bit with Gallup’s for two reasons. First, polls usually round their announced margin of error to a whole percent to keep their press releases simple. Second, our rough formula only works for an SRS. We will see in the next chapter that most national samples are more complicated than an SRS in ways that tend to slightly increase the margin of error. In fact, Gallup’s survey methods section for this particular poll included the statement,「Each sample of national adults includes a minimum quota of 50% cellphone respondents and 50% landline respondents, with additional minimum quotas by time zone within region. Landline and cellular telephone numbers are selected using random-digit-dial methods.」While these methods go beyond what we will study in the next chapter, the complexity of collecting a national sample increases the value of the margin of error.

Our quick and approximate method also reveals an important fact about how margins of error behave. Because the sample size appears in the denominator of the fraction, larger samples have smaller margins of error. We knew that. Because the formula uses the square root of the sample size, however, to cut the margin of error in half, we must use a sample four times as large.

Example 5

Margin of error: Impact of sample size

In Example 2, we compared the results of taking many SRSs of size and many SRSs of size from the same population. We found that the variability of the middle 95% of the sample results was about three times larger for the smaller samples.

Our quick formula estimates the margin of error for SRSs of size 1015 to be about 3.1%. The margin of error for SRSs of size 100 is about

Because 1015 is roughly 10 times 100 and the square root of 10 is 3.1, the margin of error is about three times larger for samples of 100 people than for samples of 1015 people.

Now it’s your turn

3.1 Drug abuse and families. In July 2018, the Gallup Poll asked a random sample of 1033 American adults,「Has drug abuse ever been a cause of trouble in your family?」The poll found that 30% of respondents said「yes,」a record high percentage since the question started being asked in 1995. What is the approximate margin of error for 95% confidence?

Confidence Statements

Here is Gallup’s conclusion about the views of American adults about vaccinating children in short form:「The poll found that a slight majority of Americans, 54%, feel it is extremely important to vaccinate children. We are 95% confident that the truth about all American adults is within plus or minus 4 percentage points of this sample result.」Here is an even shorter form:「We are 95% confident that between 50% and 58% of all American adults feel it is extremely important to vaccinate children.」These are confidence statements.

Key Terms

A confidence statement has two parts: a margin of error and a level of confidence. The margin of error says how close the sample statistic lies to the population parameter. The level of confidence says what percentage of all possible samples satisfy the margin of error.

A confidence statement is a fact about what happens in all possible samples and is used to say how much we can trust the result of one sample. The phrase「95% confidence」means「We used a sampling method that gives a result this close to the truth 95% of the time.」Here are some hints for interpreting confidence statements:

Statistics in Your World

The telemarketer’s pause People who do sample surveys hate telemarketing. We all get so many unwanted sales pitches by phone that many people hang up before learning that the caller is conducting a survey rather than selling vinyl siding. Here’s a tip. Both sample surveys and telemarketers dial telephone numbers at random. Telemarketers automatically dial many numbers, and their sellers come on the line only after you pick up the phone. Once you know this, the telltale「telemarketer’s pause」gives you a chance to hang up before the seller arrives. Sample surveys have a live interviewer on the line when you answer.

The conclusion of a confidence statement always applies to the population, not to the sample. We know exactly the opinions of the 1015 people in the sample, because Gallup interviewed them. The confidence statement uses the sample result to predict something about the population of all American adults.

Our conclusion about the population is never completely certain. Gallup’s sample might be one of the 5% that miss by more than 4 percentage points.

A sample survey can choose to use a confidence level other than 95%. The cost of higher confidence is a larger margin of error. For the same sample, a 99% confidence statement requires a larger margin of error than 95% confidence. If you are content with 90% confidence, you get in return a smaller margin of error. Remember that our quick and approximate method gives the margin of error only for 95% confidence.

It is usual to report the margin of error for 95% confidence. If a news report gives a margin of error but leaves out the confidence level, it’s pretty safe to assume 95% confidence.

Want a smaller margin of error with the same confidence? Take a larger sample. Remember that larger samples have less variability. You can get as small a margin of error as you want and still have high confidence by paying for a large enough sample.

Example 6

2016 election polls

In 2016, shortly before the presidential election, SurveyUSA, a polling organization, asked voters in several states who they would vote for. In Kansas they asked a random sample of 581 likely voters, and 47% said they would vote for Donald Trump and 36% said Hillary Clinton. SurveyUSA reported the margin of error to be plus or minus 4.1%. In Oregon they sampled 654 likely voters, and 38% said they would vote for Trump and 48% said Clinton. The margin of error was reported to be plus or minus 3.9%.

There you have it: the sample of likely voters in Oregon was slightly larger, so the margin of error for conclusions about voters in Oregon is slightly smaller (3.9% compared to 4.1%). We are 95% confident that between 34.1% (that’s 38% minus 3.9%) and 41.9% (that’s 38% plus 3.9%) of likely voters in Oregon would vote for Trump. Note that the actual 2016 election results for Oregon were 39.1% for Trump, which is within the margin of error.

Now it’s your turn

3.2 Drug abuse and families. In July 2018, the Gallup Poll asked a random sample of 1033 American adults,「Has drug abuse ever been a cause of trouble in your family?」The poll found that 30% of respondents said「yes,」a record high percentage since the question started being asked in 1995. Suppose that the sample size had been 4000 rather than 1033. Find the margin of error for 95% confidence for the larger sample. How does it compare with the margin of error for a sample of size 1033?

Sampling from Large Populations

Gallup’s sample of 1015 American adults was only 1 out of every 243,300 adults in the United States. Does it matter whether 1015 is 1-in-100 individuals in the population or 1-in-243,300? Read the box below to find out.

Population size doesn’t matter

The variability of a statistic from a random sample is essentially unaffected by the size of the population as long as the population is at least 20 times larger than the sample.

Why does the size of the population have little influence on the behavior of statistics from random samples? Imagine sampling soup by taking a spoonful from a pot. The spoon doesn’t know whether it is surrounded by a small pot or a large pot. As long as the pot of soup is well mixed (so that the spoon selects a「random sample」of the soup) and the spoonful is a small fraction of the total, the variability of the result depends only on the size of the spoon.

This is good news for national sample surveys like the Gallup Poll. A random sample of size 1000 or 2500 has small variability because the sample size is large. But remember that even a very large voluntary response sample or convenience sample is worthless because of bias. Taking a larger sample can never fix biased sampling methods.

However, the fact that the variability of a sample statistic depends on the size of the sample and not on the size of the population is bad news for anyone planning a sample survey in a university or a small city. For example, it takes just as large an SRS to estimate the proportion of Arizona State University undergraduate students who call themselves political conservatives as to estimate with the same margin of error the proportion of all adult U.S. residents who are conservatives. We can’t use a smaller SRS at Arizona State just because there are 59,200 Arizona State undergraduate students and over 252 million adults in the United States in 2017.

STATISTICAL CONTROVERSIES

Should Election Polls Be Banned?

Preelection polls tell us that Senator So-and-So is the choice of 55% of Michigan voters. The media love these polls. Statisticians don’t love them because elections often don’t go as forecasted, even when the polls use all the right statistical methods. Many people who respond to the polls change their minds before the election. Others say they are undecided. Still others say which candidate they favor but won’t bother to vote when the election arrives. Election forecasting is one of the less satisfactory uses of sample surveys because we must ask people now how they will vote in the future.

Exit polls, which interview voters as they leave the voting place, don’t have these problems. The people in the sample have just voted. A good exit poll, based on a national sample of election precincts, can often call a presidential election correctly long before the polls close. But, as was the case in the 2016 presidential election, exit polls can also fail to call the results correctly. These facts sharpen the debate over the political effects of election forecasts.

Can you think of good arguments against public preelection polls? Think about how these polls might influence voter turnout. Remember that voting ends in the East several hours before it ends in the West. What about arguments against exit polls?

What are arguments for preelection polls? Consider freedom of speech, for example. What about arguments for exit polls?

For some thought-provoking articles on polls, especially in light of the exit poll failures in the 2016 presidential election, see the following websites:

https://www.nytimes.com/2017/05/31/upshot/a-2016-review-why-key-state-polls-were-wrong-about-trump.html

http://www.pewresearch.org/fact-tank/2016/11/09/why-2016-election-polls-missed-their-mark/

https://www.cnn.com/election/2016/results/exit-polls

You may also go to www.google.com and search using key words「exit poll failures in the 2016 presidential election.」

Chapter 3 Summary and Exercises

Chapter 3: Statistics in Summary

The purpose of sampling is to use a sample to predict information about a population. We often use a sample statistic to estimate the value of a population parameter.

This chapter has one big idea: to describe how trustworthy a sample is, ask,「What would happen if we took a large number of samples from the same population?」If almost all samples would give a result close to the truth, we can trust our one sample even though we can’t be certain that it is close to the truth.

In planning a sample survey, first aim for small bias by using random sampling and avoiding bad sampling methods such as voluntary response. Next, choose a large enough random sample to reduce the variability of the result. Using a large random sample guarantees that almost all samples will give accurate results.

To say how accurate our conclusions about the population are, make a confidence statement. News reports often mention only the margin of error. Most often this margin of error is for 95% confidence. That is, if we chose many samples, the truth about the population would be within the margin of error 95% of the time. Remember that margin of error does not mean we made a mistake; it’s just due to variability from sample to sample.

We can roughly approximate the margin of error for 95% confidence based on a simple random sample of size by the formula . As this formula suggests, only the size of the sample, not the size of the population, matters. This is true as long as the population is much larger (at least 20 times larger) than the sample.

This chapter summary will help you evaluate the Case Study.

Link It

In Chapter 1 we introduced sample surveys as an important kind of observational study. In Chapter 2 we discussed both good and bad methods for taking a sample survey. Simple random sampling was introduced as a method that deliberately uses chance to produce unbiased data. This deliberate use of chance to produce data is one of the big ideas of statistics.

In this chapter we looked more carefully at how sample information is used to gain information about the population from which it is selected. The big idea is to ask what would happen if we used our method for selecting a sample to take many samples from the same population. If almost all would give results that are close to the truth, then we have a basis for trusting our sample.

In practice, how easy is it to take a simple random sample? What problems do we encounter when we attempt to take samples in the real world? This is the topic of the next chapter.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study that opened the chapter. Start by reviewing the Chapter Summary, then communicate clearly enough for any of your classmates to understand what you are saying.

In the Case Study at the beginning of the chapter, 54% of those surveyed in 2015 felt that it is extremely important to vaccinate children. The Gallup Poll stated that childhood vaccinations were considered to be extremely important by a slight majority (54%) of American adults. Is 54% evidence that, in fact, the majority of American adults in 2015 felt that childhood vaccinations are extremely important? Use what you have learned about how and why we can generalize results from a sample to the population of interest, that results from different samples vary from each other (but that we can quantify this variability), and what the statement「margin of error」means to answer this question. Your answer should be written so that someone who knows no Statistics will understand your reasoning.

In this chapter you have:

Learned how and why we can generalize results from a sample to the population of interest.

Understood that results from different samples vary from each other, but that we can quantify this variability.

Understood what the statement「margin of error」means in poll results that you see.

Online Resources

The video technology manuals explain how to select an SRS using JMP, Excel, R, Minitab, CrunchIt!, SPSS, and the TI 83/84.

The Statistical Applet, Simple Random Sample, can be used to select a simple random sample when the number of labels is 144 or less.

Check the Basics

For Exercise 3.1, see page 44; for Exercise 3.2, see page 46.

3.3 What’s the parameter? An online store contacts 1500 customers from its list of customers who have purchased in the last year and asks the customers if they are very satisfied with the store’s website. One thousand (1000) customers respond, and 696 of the 1000 say that they are very satisfied with the store’s website. The parameter is

the 69.6% of respondents who replied they are very satisfied with the store’s website.

the percentage of the 1500 customers contacted who would have replied they are very satisfied with the store’s website.

the percentage of all customers who purchased in the last year who would have replied they are very satisfied with the store’s website.

None of the above is the parameter.

3.4 What’s the statistic? A state representative wants to know how voters in his district feel about enacting a statewide smoking ban in all enclosed public places, including bars and restaurants. His staff mails a questionnaire to a simple random sample of 800 voters in his district. Of the 800 questionnaires mailed, 152 were returned. Of the 152 returned questionnaires, 101 support the enactment of a statewide smoking ban in all enclosed public places. The statistic is

Unable to be determined based on the information provided.

3.5 Decreasing sampling variability. You plan to take a sample of size 500 to estimate the proportion of students at your school who support having no classes and special presentations on Veteran’s Day. To be twice as accurate with your results, you should plan to sample how many students? (Hint: Use the quick and approximate method for the margin of error.)

125 students

250 students

1000 students

2000 students

3.6 What can we be confident about? A May 2015 University of Michigan C.S. Mott Children’s Hospital National Poll on Children’s Health reported that 90% of adults are concerned that powdered alcohol will be misused by people under age 21. The margin of error was reported to be 2 percentage points, and the level of confidence was reported to be 95%. This means that

we can be 95% confident that between 88% and 92% of adults are concerned that powdered alcohol will be misused by people under age 21.

we can be 95% confident that between 88% and 92% of adults who were surveyed are concerned that powdered alcohol will be misused by people under age 21.

we know that 90% of adults are concerned that powdered alcohol will be misused by people under age 21.

Both (a) and (b) are true.

3.7 Which is more accurate? The Pew Research Center Report entitled「How Americans value public libraries in their communities,」released December 11, 2013, asked a random sample of 6224 Americans aged 16 and over,「Have you used a Public Library in the last 12 months?」In the entire sample, 30% said「yes.」But only 17% of those in the sample over 65 years of age said「yes.」Which of these two sample percents will be more accurate as an estimate of the truth about the population?

The result for those over 65 is more accurate because it is easier to estimate a proportion for a small group of people.

The result for the entire sample is more accurate because it comes from a larger sample.

Both are equally accurate because both come from the same sample.

We cannot determine this because we do not know the percentage of those in the sample 65 years of age or younger who said「yes.」

Chapter 3 Exercises

3.8 The boldface number in the next paragraph is the value of either a parameter or a statistic. State which it is.

The Bureau of Labor Statistics announces that in July 2018 it interviewed all members of the labor force in a sample of 60,000 households; 3.9% of the people interviewed were unemployed.

3.9 Each boldface number in the next paragraph is the value of either a parameter or a statistic. In each case, state which it is.

According to The Independent, the final polls conducted in Great Britain prior to「Brexit」(Britain’s proposed exit from the European Union [EU]) indicated that the majority of voters would vote for Britain to stay part of the EU (and thus a minority would vote to leave). For example, the final online poll conducted by Populus indicated that only 45% of voters in Britain would vote to leave the EU. When all votes were tallied for the referendum, 52% of voters in Britain voted to leave the EU.

3.10 Each boldface number in the next paragraph is the value of either a parameter or a statistic. In each case, state which it is.

Voter registration records show that 25% of all voters in the United States are registered as Republicans. However, a national radio talk show host found that of 20 Americans who called the show recently, 60% were registered Republicans.

3.11 Each boldface number in the next paragraph is the value of either a parameter or a statistic. In each case, state which it is.

The National Health Interview Survey (NHIS) telephone survey is conducted annually in the United States. Of the first 100 numbers dialed, 55 numbers were for wireless telephones. This is not surprising because, as of the second half of 2016, 50.8% of all U.S. households had only wireless telephones.

3.12 A sampling experiment. Figures 3.1 and 3.2 show how the sample proportion behaves when we take many samples from the same population. You can follow the steps in this process on a small scale.

Figure 3.4 represents a small population. Each circle represents an adult. The white circles are people who favor a state constitutional amendment that would ban single-use plastic bags, and the colored circles are people who are opposed. You can check that 50 of the 100 circles are white, so in this population the proportion who favor an amendment is .

Figure 3.4 A population of 100 individuals for Exercise 3.12. Some individuals (white circles) favor a constitutional amendment and the others do not.

The circles are labeled 00, 01, , 99. Use line 101 of Table A to draw an SRS of size 4. What is the proportion of the people in your sample who favor a state constitutional amendment?

Take 9 more SRSs of size 4 (10 in all), using lines 102 to 110 of Table A, a different line for each sample. You now have 10 values of the sample proportion . Write down the 10 values you should now have of the sample proportion .

Because your samples have only 4 people, the only values can take are 0/4, 1/4, 2/4, 3/4, and 4/4. That is, is always 0, 0.25, 0.5, 0.75, or 1. Mark these numbers on a line and make a histogram of your 10 results by putting a bar above each number to show how many samples had that outcome.

Taking samples of size 4 from a population of size 100 is not a practical setting, but let’s look at your results anyway. How many of your 10 samples estimated the population proportion exactly correctly? Is the true value 0.5 in the center of your sample values? Explain why 0.5 would be in the center of the sample values if you took a large number of samples.

3.13 A sampling experiment. Let us illustrate sampling variability in a small sample from a small population. Ten of the 25 club members listed below are female. Their names are marked with asterisks in the list. The club chooses 5 members at random to receive free trips to the national convention.

Alonso Darwin Herrnstein Myrdal Vogt*

Binet* Epstein Jimenez* Perez* Went

Blumenbach Ferri Luo Spencer* Wilson

Chase* Gonzales* Moll* Thomson Yerkes

Chen* Gupta Morales* Toulmin Zimmer

Use the Simple Random Sample applet, other software, or a different part of Table A to draw 20 SRSs of size 5. Record the number of females in each of your samples. Make a histogram like that in Figure 3.1 to display your results. What is the average number of females in your 20 samples?

Do you think the club members should suspect discrimination if none of the 5 tickets go to women?

3.14 Another sampling experiment. Let us illustrate sampling variability in a small sample from a small population. Seven of the 20 college softball players listed below are in-state students. Their names are marked with asterisks in the list. The coach chooses 5 players at random to receive a new scholarship funded by alumni.

Betsa Blanco Christner Connell Driesenga*

Falk Garfinkel* Lawrence Montemarano Ramirez

Richvalsky* Romero Sbonek* Susalla* Swearingen

Sweet Swift* Vargas Wagner Wald*

Use the Simple Random Sample applet, other software, or a different part of Table A to draw 20 SRSs of size 5. Record the number of in-state students in each of your samples. Make a histogram like that in Figure 3.1 to display your results. What is the average number of in-state players in your 20 samples?

Do you think the college should suspect discrimination if none of the 5 scholarships go to in-state players?

3.15 Canada’s national health care. The Ministry of Health in the Canadian province of Ontario wants to know whether the national health care system is achieving its goals in the province. Much information about health care comes from patient records, but that source doesn’t allow us to compare people who use health services with those who don’t. So the Ministry of Health conducted the Ontario Health Survey, which interviewed a random sample of 61,239 people who live in the province of Ontario.

What is the population for this sample survey? What is the sample?

The survey found that 76% of males and 86% of females in the sample had visited a general practitioner at least once in the past year. Do you think these estimates are close to the truth about the entire population? Why?

3.16 Environmental problems. A Gallup Poll found that 62% of American adults「believe the U.S. government is not doing enough to protect the environment.」Gallup’s report said,「Results for this Gallup poll are based on telephone interviews conducted March 1–8, 2018, with a random sample of 1041 adults, aged 18 and older, living in all 50 U.S. states and the District of Columbia.」

What is the population for this sample survey? What is the sample?

The survey found that 57% of Republicans and those who lean Republican and 89% of Democrats and those who lean Democratic in the sample think the U.S. government should spend more money on developing solar and wind power. Do you think these estimates are close to the truth about the entire population? Explain your answer.

3.17 Bigger samples, please. Explain in your own words the advantages of bigger random samples in a sample survey.

3.18 Sampling variability. In thinking about Gallup’s sample of size 1015, we asked,「Could it happen that one random sample finds that 54% of adults feel that childhood vaccination is extremely important and a second random sample finds that only 42% favor one?」Look at Figure 3.2, which shows the results of 1000 samples of this size when the population truth is , or 50%. Would you be surprised if a sample from this population gave 54%? Would you be surprised if a sample gave 42%? Use Figure 3.2 to support your reasoning.

3.19 Health care cost. A November 2017 Gallup Poll of 1028 U.S. adults found that 627 are satisfied with the total cost they pay for their health care. The announced margin of error is percentage points. The announced confidence level is 95%.

What is the value of the sample proportion who say they are satisfied with the total cost they pay for their health care? Explain in words what the population parameter is in this setting.

Make a confidence statement about the parameter .

3.20 Bias and variability. Figure 3.5 shows the behavior of a sample statistic in many samples in four situations. These graphs are like those in Figures 3.1 and 3.2. That is, the heights of the bars show how often the sample statistic took various values in many samples from the same population. The true value of the population parameter is marked on each graph. Label each of the graphs in Figure 3.5 as showing high or low bias and as showing high or low variability.

Figure 3.5 Take many samples from the same population and make a histogram of the values taken by a sample statistic. Here are the results for four different sampling methods for Exercise 3.20.

The first histogram shows tightly packed bars, and two more bars, spaced away from the rest of the bars, with a space between them. The population parameter points at the space between the packed bars and the spaced bars. The second histogram shows tightly packed bars, the population parameters point at the packed bars. The third histogram shows sparse and loosely spaced bars with the population parameter pointing at one of the bars. The fourth histogram shows the population parameter pointing at a space on the left side of a set of tightly packed bars.

3.21 Is a larger sample size always better? A politician asked his constituents via a Facebook poll to help him decide how he should vote on a bill that would establish 150m Protester Exclusion Zones around abortion clinics in New South Wales, Australia. On his Facebook page, Philip Donato stated「I believe this is a matter of conscience and the views of my electorate should supersede my own.」

According to The Sydney Morning Herald, as of 1:00 P.M. on June 6, 2018, (the day before Donato’s Facebook poll closed), 74% of the 7700 poll voters supported the Protestor Exclusion Zones. Use our quick and approximate method to determine the margin of error for the poll results as of 1:00 P.M. on June 6, 2018.

After the poll closed, the final Facebook poll results had 78% of the 19,600 voters indicating support for the Protester Exclusion Zones. Use our quick and approximate method to determine the margin of error for the final Facebook poll results.

Using the information you calculated in parts (a) and (b), which snapshot of the poll do you think most accurately reflects the views of Donato’s constituents? Explain your answer.

Does your answer to part (c) change in light of the following comment that appeared in the Herald article by Labor MP Penny Sharpe:「I would encourage everyone in the Central West who thinks that women should be able to go to the doctor with privacy and without interference to support the poll and encourage Mr Donato to vote for the bill」? Explain why or why not.

Is it correct to say that, based on the final Facebook poll, we are 95% confident that 78% of all of Philip Donato’s constituents believe that Protester Exclusion Zones should be established in New South Wales? Explain your answer. Be careful not to confuse your personal opinion with the statistical issues.

3.22 Predict the election. Just before a presidential election, a national opinion poll increases the size of its weekly sample from the usual 1000 people to 4000 people. Does the larger random sample reduce the bias of the poll result? Does it reduce the variability of the result?

3.23 Take a bigger sample. A management student is planning a project on student attitudes toward part-time work while attending college. She develops a questionnaire and plans to ask 25 randomly selected students to fill it out. Her faculty adviser approves the questionnaire but suggests that the sample size be increased to at least 100 students. Why is the larger sample helpful? Back up your statement by using the quick and approximate method to estimate the margin of error for samples of size 25 and for samples of size 100.

3.24 Sampling in the states. An agency of the federal government plans to take an SRS of residents in each state to estimate the proportion of owners of real estate in each state’s population. The populations of the states range from about 563,600 people in Wyoming to about 37.3 million in California, according to the 2010 U.S. Census.

Will the variability of the sample proportion change from state to state if an SRS of size 2000 is taken in each state? Explain your answer.

Will the variability of the sample proportion change from state to state if an SRS of 1/10 of 1% (0.001) of the state’s population is taken in each state? Explain your answer.

3.25 Immigration poll. A June 2018 Gallup poll asked 1520 randomly selected American adults whether they felt immigration is a good thing or a bad thing for the United States. The poll found that 75% of the respondents said that immigration is a good thing for the United States.

The poll announced a margin of error of percentage points for 95% confidence in its conclusions. Make a 95% confidence statement about the percentage of all American adults who think immigration is a good thing for the United States.

Explain to someone who knows no Statistics why we can’t just say that 75% of all American adults think immigration is a good thing for the United States.

Now explain clearly what「95% confidence」means.

3.26 Legal immigration poll. The sample survey described in Exercise 3.25 asked 1520 randomly selected American adults about immigration in general and 755 randomly selected American adults about legal immigration. The poll announced a margin of error of percentage points for 95% confidence in conclusions about women. The margin of error for results concerning legal immigration was percentage points. Why is this larger than the margin of error for those asked about immigration in general?

3.27 Explaining confidence. A student reads that we are 90% confident that the average score of those of two or more races on the 2017 SAT is between 800 and 1410. Asked to explain the meaning of this statement, the student says,「90% of all those of two or more races have 2017 SAT scores between 800 and 1410.」Is the student right? Explain your answer.

3.28 The death penalty. In October 2017, the Gallup Poll asked a sample of 1028 U.S. adults,「Are you in favor of the death penalty for a person convicted of murder?」The proportion who said they were in favor was 55%.

Approximately how many of the 1028 people interviewed said they were in favor of the death penalty for a person convicted of murder?

Gallup says that the margin of error for this poll is percentage points. Explain to someone who knows no Statistics what「margin of error percentage points」means.

3.29 Find the margin of error. Example 6 tells us that a SurveyUSA Poll asked 581 likely voters in Kansas which presidential candidate they would vote for; 47% said they would vote for Donald Trump. Use the quick and approximate method to estimate the margin of error for conclusions about all likely voters in Kansas. How does your result compare with SurveyUSA’s margin of error given in Example 6?

3.30 Find the margin of error. Exercise 3.28 concerns a Gallup Poll sample of 1028 people. Use the quick and approximate method to estimate the margin of error for statements about the population of all U.S. adults. Is your result close to the margin of error announced by Gallup?

3.31 Find the margin of error. Exercise 3.15 describes a sample survey of 61,239 adults living in Ontario. Estimate the margin of error for conclusions having 95% confidence about the entire adult population of Ontario.

3.32 Belief in a higher power. A Pew Research Center Survey conducted in December 2017 reports that 32% of a sample of 4729 adults said they believe in a higher power or spiritual force in the universe other than the God of the Bible.

Use the quick and approximate method to estimate the margin of error for a random sample of this size.

Assuming that this was a random sample, make a confidence statement about the percentage of all adults who believe in a higher power or spiritual force in the universe other than the God of the Bible.

3.33 Legalizing marijuana. An April 2018 Quinnipiac University Poll surveyed 1193 American voters and found that 63% support legalizing marijuana in the United States, an increase of 2% from an August 2017 survey. Make a confidence statement about the percentage of all American voters who thought marijuana should be legalized in the United States, at the time the poll was taken. (Assume that this is an SRS, and use the quick and approximate method to find the margin of error.)

3.34 Moral uncertainty versus statistical uncertainty. In Exercise 3.33 and in the Case Study, we examined polls involving controversial issues, either from a moral or personal liberty perspective (we will call this「moral uncertainty」). In both polls, national opinion was divided, suggesting that there is considerable moral uncertainty regarding both issues. What was the margin of error (the「statistical uncertainty」) in both polls? Is it possible for issues with a high degree of moral uncertainty to have very little statistical uncertainty? Discuss.

3.35 Smaller margin of error. Exercise 3.28 describes an opinion poll that interviewed 1028 people. Suppose that you want a margin of error half as large as the one you found in that exercise. How many people must you plan to interview?

3.36 Satisfying Congress. Exercise 3.19 describes a sample survey of 1028 adults, with margin of error for 95% confidence.

A member of Congress thinks that 95% confidence is not enough. He wants to be 99% confident. How would the margin of error for 99% confidence based on the same sample compare with the margin of error for 95% confidence?

Another member of Congress is satisfied with 95% confidence, but she wants a smaller margin of error than percentage points. How can we get a smaller margin of error, still with 95% confidence?

3.37 The Current Population Survey. Though opinion polls usually make 95% confidence statements, some sample surveys use other confidence levels. The monthly unemployment rate, for example, is based on the Current Population Survey of about 60,000 households. The margin of error in the unemployment rate is announced as about two-tenths of 1 percentage point with 90% confidence. Would the margin of error for 95% confidence be smaller or larger? Why?

3.38 Detoxing from social media. The Harris Poll recently asked a sample of 2043 adults in the United States which social media app they found the hardest to stay away from. Forty-nine percent of respondents found Facebook the most difficult social media app to ignore. The last bit of information the Harris Poll shared in the same article mentioned that 31% of the poll respondents「grew anxious when they didn’t check social media regularly.」Write a short report of this finding, as if you were writing for a newspaper. Be sure to include a margin of error. Be careful not to confuse your personal opinion with the statistical findings.

3.39 Who is to blame? A May 2018 POLITICO/Morning Consult poll surveyed 1993 registered voters and asked who is to blame for mass shootings in the United States. Of the 1993 respondents, 1220 blame illegal gun dealers for mass shootings in the United States. Of the subset of 945 registered voters who were asked about treatment for mental illness, 489 said that they blame lack of access to treatment for mental illness for mass shootings in the United States.

The POLITICO/Morning Consult poll reported a margin of error of percentage points. Which of the two questions resulted in the margin of error of percentage points? What is the margin of error for the other question? Explain your answers.

3.40 Simulation. Random digits can be used to simulate the results of random sampling. Suppose that you are drawing simple random samples of size 25 from a large number of college students and that 20% of the students are unemployed during the summer. To simulate this SRS, generate 25 random digits using the Simple Random Sample applet or let 25 consecutive digits in Table A stand for the 25 students in your sample. The digits 0 and 1 stand for unemployed students, and other digits stand for employed students. This is an accurate imitation of the SRS because 0 and 1 make up 20% of the 10 equally likely digits.

Simulate the results of 50 samples by counting the number of 0s and 1s in the first 25 entries in each of the 50 repetitions of the Simple Random Sample applet or in each of the 50 rows of Table A. Make a histogram like that in Figure 3.1 to display the results of your 50 samples. Is the truth about the population (20% unemployed, or 5 in a sample of 25) near the center of your graph? What are the smallest and largest counts of unemployed students that you obtained in your 50 samples? What percentage of your samples had either 4, 5, or 6 unemployed?

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

案例分析

同性婚姻一直富有争议性，许多人基于宗教信仰表示反对。反对者认为同性婚姻破坏了传统的家庭和婚姻制度，支持者认为这涉及权利平等问题。2011 年 5 月，一项盖洛普民意调查提出问题：「你认为同性婚姻是否应该和传统婚姻一样得到法律认可？」从 2004 年开始，盖洛普每年都会进行这项调查，大多数调查对象（53%）认为「法律应该承认同性婚姻的合法性」。

2004 年 2 月，这个话题在美国成为重大新闻，受到全国人民的关注。在一些城市 —— 其中最知名的是旧金山市 —— 出现了同性婚礼，尽管这违反了该州的法律。小布什总统对此发表讲话说：「今天，我建议国会尽快通过并送交各州推行一项宪法修正案，该修正案承认和保护婚姻是男女双方以夫妻名义形成的联合体。」关于这项修正案，有多少人支持呢？一项从 2003 年 7 月到 2004 年 2 月进行的盖洛普民意调查提出问题：「你支持还是反对宪法修正案规定只有男女才能结婚，而不允许男同性恋者和女同性恋者建立婚姻关系？」该项调查发现，「支持该宪法修正案的人为 51%，略高于 45% 的反对者比例」。我们可以信任这个调查结果吗？

这是在随机访谈了 2527 名美国成年人后得出的结论。盖洛普公司采用了随机抽样的方式，与只访谈那些参加旧金山市同性婚礼的人相比，调查结果的偏差会更小。但是，美国人口普查局公布 2004 年美国的成年人口约为 2.2 亿名。在这种情况下从 2527 名成年人，哪怕是随机抽取的 2527 名成年人，真的可以了解到 2.2 亿人的意见吗？

51% 的支持率是否真能表明大多数美国人是支持该修正案的呢？2011 年 5 月的民意调查结果来自随机抽样的 1018 名成年人，这是否能说明当今的大多数美国人反对该修正案？在本章的结尾部分，你会找到这些问题的答案。

从样本到总体

2004 年的盖洛普调查发现「支持该宪法修正案的人为 51%，略高于反对者的比例」，这是针对约 2.2 亿的美国成年人得出的结论。但是，盖洛普公司并不知道这 2.2 亿人的真实想法。这项调查只访谈了 2527 人，发现其中有 51% 的人支持该宪法修正案。因为 2527 位成年人的样本是随机抽取的，我们有理由认为这个样本可以较好地代表总体，并估算出「所有成年人」中约有 51% 的人支持该修正案。这是统计领域的一种基本做法：用抽样调查的结论，当作对总体真实信息的估计。在讨论这个主题之前，必须先区分清楚哪个数字是描述样本的，哪个数字是描述总体的。

参数与统计量

参数（parameter）是描述总体的数字。参数是一个固定数值，但我们无法知道参数的实际值。

统计量（statistic）是描述样本的数字。一旦有了样本，统计量的值即可得知，如果换一个样本，统计量的值就可能有所改变。我们常用统计量来估计未知的参数。

所以，参数之于总体，相当于统计量之于样本。想要估计未知的参数，你只要从总体中选一个样本，用样本的统计量当作参数的估计值即可。盖洛普公司就是这么做的。

例 1 你支持宪法修正案吗？

所有支持该宪法修正案的调查对象的比例，就是描述约 2.2 亿美国成年人这一总体的参数。我们将其记作 p，意为「比例」（proportion）。可惜，我们无法知道它的确切数值。为了估算出 p 的值，盖洛普公司抽取了一个包含 2527 位成年人的样本。该样本中支持者的比例就是 p 的估计值，记作，读作「戴帽子的 p」。因为在 2527 人中有 1289 人支持修正案，所以对于这个样本

由于所有成年人都有同样的概率被选入 2527 人的样本，因此我们可以用统计量 = 0.51 作为未知参数 p 的估计值。样本中有 51% 的人支持修正案是一个事实，虽然我们不知道所有成年人中有多少人支持修正案，但我们可以通过 51% 做出估计。

样本统计量的变异性

如果盖洛普公司重新抽取一个 2527 人的随机样本，那么这个样本会包含与前一个样本不一样的人。几乎可以肯定的是，不会有 1289 人给出支持的答复。也就是说，统计量的值，会随着样本的改变而改变，因此可能会出现这样的情况：一个随机样本说有 51% 的美国成年人支持宪法修正案，而另一个随机样本说只有 37% 的人支持修正案。随机样本通过抽样方法来消除偏差，但由于随机选取的样本有变异性，所以调查结果可能还是不准确。如果从同一总体中重复抽样，但所得结果的变异性太大，我们就无法相信任何一个样本的结果了。

幸好，随机样本的第二大优点可以解决这个难题。它的第一大优点是，随机抽样可以消除偏差。它的第二大优点是，如果我们从同一个总体中重复抽取多个大小一样的随机样本，所有样本统计量的变异情况就会呈现遵循某种可预测的形态（pattern）。我们从这个可预测的形态可以得知，较大样本统计量的变异性，会小于较小样本统计量的变异性。

例 2 多个样本

统计学的另一个重要概念是：要知道一个样本有多可靠，就得问问如果我们从同一个总体中抽取多个样本，会出现什么情况。假设事实上（盖洛普公司并不知道）正好有 50% 的美国成年人支持这项宪法修正案。也就是说，总体的参数 p=0.5。如果盖洛普公司用大小为 100 的简单随机样本得出的来估算总体的 p，会怎么样？

图 3–1 表示抽取多个样本，计算每个样本的的过程。对于第一个样本，100 人中有 56 人支持修正案，因此 = 56/100=0.56。在下一个样本中，只有 36 人支持修正案，因此该样本的 = 0.36。选出 1000 个样本，将计算出的值绘制成图（柱状图），见图 3–1 右侧。图中横轴代表不同的值，柱形的高度代表 1000 个值中有多少个落在相应的横轴区间。例如，在图上，值为 0.40~0.42 的柱形高度略微超过 50，这意味着所有样本中有 50 个以上的样本的值为 0.40~0.42。

当然，盖洛普公司访谈了 2527 人，而不是 100 人。图 3–2 展示了 1000 个简单随机样本的结果，每个样本的数量为 2527 人，这些样本是从真实 p 值为 0.5 的总体中选取的。图 3–1 和图 3–2 绘图的比例尺是一样的，对比两幅图，我们可以看到当样本大小从 100 增加到 2527 时，发生了什么。

仔细看看图 3–1 和图 3–2。我们先从总体中抽出多个样本，然后得到许多值。根据这些值，我们可以画出柱状图。现在我们来研究一下这两个柱状图。

图 3–1 许多简单随机样本的结果放在一起，会呈现出某种有规则的形态。这幅图表现的是从同一总体中抽出 1000 个大小为 100 的随机样本的值的变异情况。总体的 p 值为 0.5。样本统计量会随着样本的变化而变化，但是值会落在以 p 值为中心的范围内

图 3–2 在同一个总体中选取 1000 个大小为 2527 的简单随机样本，由此得到的 1000 个值，和图 3–1 比起来，值的分布范围要窄得多

·对于上面这两种情况，样本的值会随着不同的样本而变化，但都以 0.5 为中心，0.5 是总体的 p 值。有些样本的值比 0.5 小，有些比 0.5 大，但并不会都比 0.5 大，或都比 0.5 小。

·大小为 100 的多个样本的值的分布情况，会比大小为 2527 的多个样本的值要分散得多。事实上，在大小为 2527 的 1000 个样本当中，有 95% 的值分布在 0.4805~0.5195 的区间内。也就是说，与 0.5 的差距在 ±0.0195 的范围内。而在大小为 100 的 1000 个样本中，有 95% 的值分散在 0.40~0.60 的范围内，与 0.5 有 ±0.1 的差距，约为大样本的 5 倍。所以，大样本统计量的变异性要比小样本小。

结论就是，我们可以信任一个大小为 2527 的样本，其统计量的值几乎总会很靠近总体的 p 值。

而大小为 100 的样本，在 p 值是 50% 的时候，有可能得出为 40% 或 60% 的估计值。

这让我们认识到，当我们用一个诸如的统计量，去估计诸如 p 的参数时，所谓的「偏差」（bias）是什么意思。同时，这也让我们明白，变异性的重要程度不亚于偏差。

估计时的两种误差

偏差指的是，当我们取多个样本时，它们的统计量朝同一个方向偏离总体的参数值。

变异性指的是，当我们取多个样本时，统计量的值的离散程度。变异性大，意味着不同样本的统计量可能差别也较大。一个好的抽样方法，其偏差与变异性都较小。

我们可以把总体参数的真实值想象成靶子的靶心，而把样本统计量想象成对着靶心射出的箭。偏差和变异性可被用来形容弓箭手对着靶子射了许多箭之后的状况。

偏差的意思是，射出的箭都朝着同一个方向偏离靶心，即样本统计量没有以总体参数值为中心点。变异性大的意思是，箭在靶子上很分散，即样本统计量并不接近，彼此间差异较大。

你有没有注意到，即使是小变异性（箭在靶子上都很接近），也可能有大偏差（箭都朝着同一个方向偏离靶心）；反之，即使偏差很小（箭以靶心为中心点分散），也可能有大变异性（箭在靶子上分布广）。好的抽样方法要像射箭能手一样，必须同时具备小偏差与小变异性。

图 3–3 射箭的偏差和变异性

如何处理偏差与变异性

减小偏差：用随机抽样的方法即可。先将总体找出来，再从中抽取简单随机样本，就会得到无偏估计值（unbiased estimate）。也就是说，用简单随机样本的统计量来估计总体的参数值，既不会总是高估，也不会总是低估。

减小变异性：用大一点儿的样本即可。只要样本足够大，变异性就会很小。

在实际做抽样调查的时候，盖洛普公司只会取一个样本。我们不知道从这个样本得到的总体参数估计值离真实值有多近，因为我们根本不知道总体参数的真实值是多少。但是，「只要是从大的随机样本得到的估计值，几乎总会比较接近真实值」。检视一下由多个样本的统计量构成的形态，我们就可以信任一个样本的调查结果。

误差范围

抽样调查报告的「误差范围」，其实是把我们在图 3–1 与图 3–2 中所看到的样本统计量的变异性，转换成一种关于调查结果的可信程度的叙述。

误差范围

「误差范围（margin of error）是 ±2%」的具体意思是：

如果我们用抽取这个样本所用的方法，去抽取多个样本，那么这些样本的统计量中有 95% 会在总体参数真实值的正负两个百分点的范围之内。

通常，一个随机样本的统计量，不会刚好等于总体参数的真实值。我们必须用一个误差范围来表示估计值距离真实值有多远，但是，我们又不能百分之百确定估计值和真实值的差距必定小于误差范围。所有样本的统计量中有 95% 距离真实值很近，而另外 5% 与真实值的差距则超过误差范围。我们并不知道总体的真实值是多少，所以我们也无法得知，到底样本的统计量是属于那 95%「射中」的样本统计量，还是 5%「脱靶」的样本统计量。因此，我们说我们有 95% 的把握认为真实值在误差范围内。

例 3 电视新闻

电视新闻播音员说：「最近发布的一项盖洛普民意调查发现，约有 51% 的美国成年人支持小布什总统关于婚姻的宪法修正案，反对同性婚姻。此次调查的误差范围是 ±2%。」51% 加减两个百分点，分别是 53% 和 49%，总体对该修正案的真正态度落在这个区间之内。

而盖洛普公司实际上说的是：「对于该抽样调查的结果，我们有 95% 的信心认为，由抽样或其他随机因素造成的误差，应该在正负两个百分点之间。」也就是说，该误差范围只适用于 95% 的样本统计量，「95% 的置信度」就是这种意思的简单表达，而新闻报道中把「95% 的置信度」漏掉了。

准确计算出误差范围是统计学家要做的事。但是，你可以用一个简单的公式，算出民意调查的误差范围大概有多大。这个公式将在第 21 章中讨论。

误差速算法

假设我们用一个大小为 n 的简单随机样本的统计量来估计未知的总体参数 p。如果置信度为 95%，那么误差大致为 1/。

例 4 误差是多少？

例 1 中的盖洛普民意调查访谈了 2527 人，对应 95% 的置信度，误差大约是：

盖洛普公司宣布的误差范围是 ±2%，这和我们用速算公式得出的结果一致。一般来说，我们用速算公式计算出的结果可能和盖洛普公司公布的结果有些差异，主要有两个原因：首先，盖洛普公司为了让新闻报道简单些，常常对结果进行四舍五入。其次，速算公式只适用于简单随机抽样。我们在下一章将会看到，大多数样本都比简单随机样本复杂，会略微增大误差范围。

我们的速算法还能反映出关于误差范围的重要信息。因为样本大小 n 出现在公式的分母当中，这意味着较大的样本就会有较小的误差范围。公式中用的是样本大小的平方根，所以想把误差范围减半，我们就需要用一个 4 倍大的样本。

例 5 误差范围和样本大小

在例 2 中，我们把从同一总体抽出的多个大小为 100 人的简单随机样本，和大小为 2527 人的简单随机样本的统计量做了比较。我们发现对于其中 95% 的样本来说，小样本的误差范围大约是大样本的 5 倍。

我们的速算公式算出的样本大小为 2527 人的简单随机样本的误差约为 2%，而样本大小为 100 人的简单随机样本的误差大约是

因为 2527 大约是 100 的 25 倍，25 的平方根是 5，因此 100 人样本的误差范围约为 2527 人样本的 5 倍。

练习

3.1 向富人征税。2011 年 4 月，盖洛普公司抽样调查了 1077 名成年人。「人们对于政府的职能有不同的看法。你认为我们的政府是否应该对富人征收重税，从而实现财富再分配？」该调查发现，有 47% 的调查对象同意对富人征收重税。在置信度为 95% 的情况下，该调查的误差范围是多大？

置信度说明

以下是盖洛普公司对于小布什总统提出的宪法修正案的精简结论：「调查发现只有 51% 的美国成年人支持该修正案。我们有 95% 的把握认为，所有美国成年人的真正态度会在这个结果的正负两个百分点的范围内。」还有一个更精简的说法：「我们有 95% 的把握认为，在所有成年人当中，有 49%~53% 的人支持该修正案。」这些都是置信度说明（confidence statement）。

置信度说明

置信度说明包含两个部分：误差范围与置信度（level of confidence）。误差范围告诉我们，样本统计量距离总体参数真实值有多远。置信度告诉我们，所有样本统计量中，满足该误差范围的样本统计量的百分比。

置信度说明反映的是一个事实，我们用它来表达对一个样本的结果有多大的信心。「95% 的置信度」的意思是，「我们所用的抽样方法，有 95% 的概率可以得到与总体的真实值这么接近的结果」。以下是对如何解读置信度说明的一些提示：

·置信度说明永远是针对总体而不是样本。我们可以确切地知道样本中 2527 名成年人的情况，因为盖洛普调查访谈了他们。置信度说明是根据样本的结果来对「所有成年人」这个总体做出的结论。

·我们对总体所做出的结论不可能完全正确。盖洛普公司调查所用的样本有可能是误差超过两个百分点的 5% 的样本之一。

·抽样调查也可以选择 95% 之外的置信度。选择较高置信度的代价是较大的误差范围。对于同一个样本来说，99% 置信度的抽样调查的误差范围，比 95% 置信度的抽样调查要大。如果你对 95% 置信度就很满足了，得到的回馈就是较小的误差范围。记住，我们的速算法计算的就是 95% 置信度的抽样调查的误差范围。

·报告误差范围时，使用 95% 置信度是很普遍的做法。如果一则新闻报道中只说明了误差范围而没有置信度，把置信度视为 95% 是很稳妥的做法。

·你想在同样的置信度条件下，缩小误差范围吗？取一个大一点儿的样本就行了。你应该还记得较大的样本有较小的变异性吧。只要你愿意付出取足够大的样本的代价，就可以减小误差范围，同时保持高置信度。

知识普及 如何辨识推销电话

做抽样调查的人痛恨电话推销。我们都接过令人厌烦的推销商品的电话，以至于很多人在还没搞清楚对方不是在卖东西，而是在做抽样调查之前，就已经挂了电话。我们在这里教你一个分辨两者的诀窍。抽样调查员和电话推销员都会随机选择要拨打的电话号码，但是电话推销员会使用自动拨号系统同时打多个电话，在你接起电话之后，推销员才会开始说话。如果你在接起电话后对方暂时无回应，你就可以在推销员拿起话机之前挂掉电话。而抽样调查员打来的电话在你接听的那一刻，就已经有调查员在电话另一端等候了。

例 6 2008 年大选民意调查

2008 年，就在总统选举前不久，民意调查机构美国调查（Survey USA）询问了一些州的选民打算把选票投给谁。在佛罗里达州，他们随机访谈了 691 名可能的投票人。50% 的人回答将投给巴拉克·奥巴马，47% 的人说将投给约翰·麦凯恩。美国调查报告说误差范围是 ±3.8%。在佐治亚州，他们抽样访谈了 547 名可能的投票人，43% 的人说会投给奥巴马，51% 的人说会投给麦凯恩，误差范围是 ±4.3%。

你可以看到，佐治亚州的可能投票人的样本较小，所以结果的误差范围也比较大。我们有 95% 的把握认为，佐治亚州有 38.7%（43% 减去 4.3%）~47.3%（43% 加上 4.3%）的可能投票人会支持奥巴马。请注意，2008 总统选举中，佐治亚州实际投给奥巴马的选票比例是 47%，的确处在这个误差范围之内。

练习

3.2 向富人征税。2011 年 4 月，盖洛普民意调查抽样调查了 1077 名成年人。「人们对于政府的职能有不同看法。你认为，我们的政府是否应该对富人征收重税，实现财富再分配？」该调查发现，有 47% 的调查对象同意对富人征收重税。假设样本的大小为 4000 人而不是 1077 人，请计算在置信度为 95% 的情况下的误差范围，并将其与样本大小为 1077 人的误差范围做比较。

总体的大小

盖洛普公司抽出的包含 2527 名成年人的样本，相当于在美国成年人当中，从每 82700 人中抽出 1 人。该调查结果与在总体当中从每 100 人中抽出 1 人，还是从每 82700 人中抽出 1 人有关吗？

总体大小无关紧要

一个随机样本统计量的变异性，并不受总体大小的影响，只要总体至少比样本大 100 倍。

对随机样本统计量的变异性，为什么总体的大小影响很小呢？想象一下，假设我们从已收获的玉米中抽样，把勺子插进玉米粒当中。勺子并不知道它是在一袋玉米当中，还是在一卡车的玉米当中。如果玉米混合得很均匀（如此一来，勺子舀出来的玉米就是随机样本），样本统计量的变异性就只与勺子的大小有关。

这对于像盖洛普公司开展的全国性抽样调查来说是一个好消息。一个大小为 1000 或 2500 的随机样本，因为样本够大，所以变异性小。但是，自愿回应调查的样本或任意样本有偏差，所以样本再大也没用。也就是说，在这种情况下，即使样本很大也不能消除偏差。

然而，样本统计量的变异性是由样本的大小决定的，而不是由总体的大小决定的，对任何计划在一所大学里或一个小城中做抽样调查的人来说，这可能就是坏消息了。举例来说，不管是要估计俄亥俄大学中在政治方面属于保守派的学生比例，还是要估计美国所有成年人中的保守派人士的比例，只要两者要求同样的误差范围，就得抽取一样大的简单随机样本。即使俄亥俄大学只有 4.9 万名学生，而 2009 年美国的成年人口超过 2.32 亿，也不意味着在俄亥俄大学中可以抽取一个较小的简单随机样本。

【统计学中的争议】美国总统大选的民意调查是否应被禁止？

「选前民意调查」（preelection poll）告诉我们，俄亥俄州的选民中有 58% 的人支持某位参议员。媒体很欢迎这类民意调查，但统计学家可不喜欢它们，因为即使调查过程完全使用正确的统计方法，实际投票结果也常和民意调查的结果相左。接受访谈的人中有许多在选举前改变了主意，或到选举日那天根本不去投票。美国总统大选调查是抽样调查中结果不太理想的一种，因为我们必须「现在」问选民，「未来」他要投票给谁。

在投票者离开投票站时进行的「出口民调」（exit poll），就不存在上述问题。样本中的人，都是刚刚投过票的人。好的出口民调的样本是从全美国的选区中抽出来的，常常可以在距离投票结束还有很长时间时，就能准确预测出美国总统大选的结果。但是，以 2004 年总统大选为例，出口民调也可能得出错误的结论。这使得关于是否应开展美国总统大选民意调查的争论变得更加激烈了。

你能想出更好的反对进行选前民意调查的理由吗？考虑一下这些民意调查将会怎样影响选民的行为。对于出口民调，你有什么看法？要知道，美国东岸的选举结果会比西岸早几个小时出来。

有关美国总统大选民意调查的一些发人深思的文章，特别是有关预测 2004 年选举结果失败的出口民调的文章，参见以下网址：

• www.washingtongpost.com/wp-dyn/articles/A47000-2004Nov12_2.html。

• www.washingtongpost.com/wp-dyn/articles/A64906-2004Nov20.html。

• www.edisonresearch.com/exit_poll.faq.php。

• http://thehill.com/opinion/columnists/dick-morris/4723-those-faulty-exit-polls-were-sabotage。

你也可以在谷歌网站（www.google.com）检索关键字「exit poll failures in the 2014 presidential elction」（2014 年总统大选出口调查失败）。

小结

本章要点

·抽样的目的是要从样本中获得有关总体的信息。我们通常用样本统计量来估计总体参数的值。

·本章讲述了一个重要概念。要描述一个样本是否值得信任，只要问：「如果我们从同一个总体抽取多个样本，会发生什么情况？」假设几乎所有样本得出的结果都接近真实值，那么即使我们不确定样本的结果是否接近真实值，也可以对这个样本有信心。

·在策划一项抽样调查的时候，首先，要减少偏差，使用随机抽样的方法，而舍弃像自愿回应这类糟糕的抽样方法。其次，抽取的样本数量要足够大，才能减小统计量的变异性。只要使用足够大的随机样本，就能保证几乎所有样本都能得出接近真实值的结果。

·要表达我们对总体所做出的结论的精确程度，可以用置信度说明。新闻报道中往往只提到误差范围，该误差范围大多数情况下是针对 95% 置信度而言的。也就是说，如果我们抽出多个样本，则总体的真实值会落在误差范围之内的概率是 95%。

·对于大小为 n 的简单随机样本，在置信度为 95% 的情况下，我们可以用 1 / 这个公式来计算误差范围。这个公式似乎表明，重要的是样本的大小，而不是总体的大小。只要总体比样本大很多（至少大 100 倍），这一个原则就永远为真。

在第 1 章，我们介绍了抽样调查是一种重要的观察研究。在第 2 章，我们讨论了抽样调查的好的方法和不好的方法。简单随机抽样的方法被引入，它是一种能够巧妙地利用随机性产生无偏差数据的方法，这是统计学中的一个重要概念。

在本章中，我们更详细地探讨了如何通过样本信息获得总体的信息。关键在于如果我们从同一个总体中取出多个样本，会发生什么情况。如果所有样本都给出非常接近真实值的结果，我们就可以相信样本。

在实践中，选取一个简单随机样本到底是容易还是难呢？我们在现实世界中抽取样本时，会碰到什么问题？这是下一章要讲的内容。

案例分析与评估

在本章开头的那个案例里，在 2004 年的一项盖洛普民意调查中，有 51% 的调查对象支持小布什提出的宪法修正案，反对同性婚姻。51% 的支持率是否意味着 2004 年时大多数美国成年人支持该修正案？2011 年的盖洛普民意调查表明，大多数（53%）的调查对象反对这项修正案，这是否意识着 2011 年时大多数美国成年人反对该修正案？用本章所学的知识回答这两个问题。你可以将答案写下来，以便没有学过统计学的人能了解你的推理过程。

练习

3.1 见本书第 51 页。

3.2 见本书第 54 页。

3.3 下面的黑体数字是参数还是统计量？美国劳工部宣布，在上个月调查了 60000 个住户样本中所有属于劳动人口的人，其中有 9.7% 的人失业。

3.4 下面的黑体数字是参数还是统计量？一辆满载滚珠轴承的货车，平均直径是 2.503 厘米，在买主对整批货的可接受范围之内。检查者从这批货中抽验 100 个滚珠轴承，得到的平均直径是 2.515 厘米，超过买主的可接受范围，所以整批滚珠轴承被买主退货了。

3.5 下面的黑体数字是参数还是统计量？选民登记记录显示，费城选民中有 15.4% 的人为共和党人。然而，该市的一个电台脱口秀节目发现，在最近致电给他们的 20 位本地居民中，有 60% 的人为共和党人。

3.6 下面的黑体数字是参数还是统计量？一个全国性民意调查机构利用一种随机拨号装置，拨打全国的住宅电话。在最先拨打的 100 个号码当中，有 32 个是未登记的。这并不令人惊讶，因为全美国有 34% 的住宅电话，没有被住宅电话号码随机抽样调查抽中。

3.7 抽取多个样本实验。图 3–1 和图 3–2 显示出，当我们从同一个总体抽取多个样本时，样本统计量的情况。你可以依照同样的步骤，做一个小型实验。

图 3–4 当中是一个小型总体，其中每一个圆圈代表一个成年人。白色圆圈代表赞成小布什提出的宪法修正案的人，而灰色圆圈代表持反对意见的人。你可以数一下，在总共 100 个圆圈当中，有 50 个是白色的，所以在这个总体当中，支持者的比例是 p=50/100=0.5。

（a）圆圈上面有从 00、01 到 99 的编号。用表 A 从第 101 行开始抽出大小为 4 的简单随机样本。在你的样本当中，赞成修正案的人的比例是多少？

（b）再取 9 个大小为 4 的简单随机样本（总共有 10 个简单随机样本），这次用表 A 的第 102 行到第 110 行抽取样本，每一行对应一个样本。这样一来，你就有 10 个样本的值了，将这 10 个值写下来。

（c）因为你的样本里面只有 4 个人，所以可能的值只有 0/4、1/4、2/4、3/4 及 4/4，也就是必定是 0、0.25、0.5、0.75 或 1 中的一个。在一条直线上把这些数字标示出来，并且用这 10 个数字做出一个柱状图，做法是在每个数字上画一条垂直的线段，线段的长度就是结果等于该数字的样本个数。

（d）从一个大小为 100 的总体中抽取一个大小为 4 的样本，当然不是一个很实际的做法，但不管怎样，我们还是来看看你的结果。在你的 10 个样本当中，有几个把总体参数值（p=0.5）估计得完全正确？对于你所有的样本统计量来说，总体参数的真实值 0.5 是不是大致在中间的位置？说明一下在抽取多个样本的情况下，为什么 0.5 会在所有样本统计值的中间位置。

图 3–4 练习 3.7 中总体的 100 个个体，一些个体（白色圆圈）支持修正案，而另一些个体则持反对意见

3.8 抽取多个样本的实验。我们用小总体当中的小样本，来说明样本统计量的变异性。下列 25 位俱乐部会员当中有 10 位是女性，她们的名字旁边标记了星号。俱乐部要随机选出 5 位会员，为他们免费提供去参加全国大会的机会。

阿隆索 达尔文 赫恩斯坦 迈杜 沃格特 *

比奈特 * 爱泼斯坦 希门尼斯 * 佩雷斯 * 温特

布鲁门巴赫 费里 罗 斯宾塞 * 威尔逊

蔡斯 * 冈萨雷斯 * 莫尔 * 汤姆森 耶基斯

陈 * 古普塔 莫拉莱斯 * 图尔明 齐默

（a）抽取 20 个大小为 5 的简单随机样本，每次都用表 A 的不同行。把每个样本当中的女性人数记录下来，并画一个像图 3–1 中的柱状图来呈现你的结果。在你的 20 个样本中，女性人数平均是几个人？

（b）如果 5 个免费机会中没有一个是给女性会员的，你觉得俱乐部会员应不应该怀疑这其中有性别歧视的成分？

3.9 加拿大的全民医疗系统。加拿大安大略省的卫生部门想知道，全民医疗系统在该省有没有起到应有的作用。有关医疗系统的信息，大部分来自病人的病历，但是掌握该信息的单位不准我们用那些资料来对使用医疗系统和不使用医疗系统的人做出比较。所以，该卫生部门进行了一项安大略省健康调查，访问了 61239 个住在安大略省的人。

（a）这项抽样调查的总体是什么？样本是什么？

（b）调查发现，在过去的一年当中，样本中有 76% 的男性与 86% 的女性至少去看了一次全科医生。你认为样本的统计量会不会接近总体参数的真实值？为什么？

3.10 抽取大样本。在抽样调查中使用大的随机样本有什么好处，请说明。

3.11 样本统计量的变异性。在讨论盖洛普民意调查的大小为 2527 人的样本时，我们曾问过这个问题：「可不可能有一个随机样本说有 51% 的美国成年人支持宪法修正案，而另一个随机样本却说只有 37% 的人支持修正案呢？」看一下图 3–2，它显示的是当总体参数的真实值是 0.5，也就是 50% 的时候，从 1000 个大小为 2527 的样本得到的结果的分布情况。如果从这个总体抽出的一个样本的结果是 51%，你会不会觉得惊讶？如果有个样本的结果是 37%，你会不会感到惊讶？

3.12 医疗保健费用满意度。2011 年 11 月盖洛普公司进行了一项针对 1012 位美国成年人的调查，结果显示有 607 人对于他们支付的医疗保健费用表示满意。报告的这项结果的误差范围为 ±4%，置信度是 95%。

（a）对于医疗保健费用表示满意的人的样本统计量的值是多少？请说明这道题的总体参数 p 指的是什么？

（b）给参数 p 提供一个置信度说明。

3.13 偏差和变异性。图 3–5 中的柱状图，显示出在 4 种不同的情况下，抽取多个样本所得到的样本统计量的值及其分布情况。这些图类似于图 3–1 和图 3–2 中的柱状图。也就是说，柱形的高度代表当从同一个总体中抽取多个样本时，有多少个样本的统计量值会落在柱形的范围内。总体参数的真实值也标示在图上。把图 3–5 中的每个图，依大偏差或小偏差，以及大变异性或小变异性进行归类。

图 3–5 从同一总体中抽取多个样本，并根据不同样本统计量的值所绘制的柱状图。这 4 个图对应的是 4 种不同抽样方法所得的结果

3.14 大样本总是更好吗？2004 年 2 月，《今日美国》做了一项在线调查。浏览该报网站的人被问到这样一个问题：「美国是否应该通过一项禁止同性婚姻的宪法修正案？」访客可以点击按钮作答。截至 2004 年 2 月 25 日下午 3 点 30 分，访客中有 68.61% 的人投反对票，有 31.39% 的人投赞成票。该项调查共有 63046 次投票记录。使用我们的速算公式，我们可以得出这个大小的样本在 95% 的置信度下的误差范围约为 ±0.4%。我们是否可以说，根据《今日美国》的在线调查，我们有 95% 的把握认为，有 68.61%±0.4% 的美国成年人反对美国通过一项禁止同性婚姻的宪法修正案？请解释你的理由。注意，不要将个人意见和统计问题混杂在一起。

3.15 预测选举结果。在一次美国总统大选之前，一项全国性的民意调查把每周抽样的样本大小从通常的 1000 人增加到 4000 人。这个大的随机样本能否把调查结果的偏差降低？是否会减少调查结果的变异性？

3.16 抽取大样本。一个管理专业的学生计划做一份调查报告，主题是大学生对于上大学期间打工的看法。她设计好一份问卷，并计划随机选取 25 位学生填写问卷。她的导师认可了她的问卷，但建议她把样本大小增加到至少 100 人。为什么大一点儿的样本比较好？用速算公式分别计算当样本大小为 25 和 100 时的误差，以此来支持你的说法。

3.17 在美国各州抽样。美国联邦政府的一个委托单位计划在每一个州的居民当中抽取简单随机样本，用于估计每一个州中拥有房产的居民的比例。各州当中居民人数最少的是怀俄明州（544000 人），最多的是加利福尼亚州（3700 万人）。

（a）如果在每个州中抽取一个大小为 2000 人的简单随机样本，各州样本统计量的变异性会不会不同？为什么？

（b）如果在每个州中抽取全州人口的 1% 作为简单随机样本，各州样本统计量的变异性会不会不同？为什么？

3.18 对女性做民意调查。《纽约时报》为了对某些女性话题做民意调查，从全美（阿拉斯加和夏威夷除外）随机抽取了 1025 位女性进行访谈。调查发现，有 47% 的女性说她们没有足够的个人时间。

（a）调查结果表明，在 95% 的置信度下误差范围为 ±3%。对于所有女性中觉得个人时间不够的人的比例，做出置信度说明。

（b）向某个完全不懂统计学的人解释，为什么我们不能说「全部女性当中有 47% 的人觉得个人时间不够」。

（c）解释 95% 置信度是什么意思。

3.19 佐格比民调（Zogby Poll）。佐格比民调在解释其调查结果的精确程度时这样说道：「误差范围是 ±1.2%。佐格比民调的抽样方法和加权计算程序也通过其政治民意调查得到验证，即该机构 95% 以上的调查结果处于选举日实际结果的正负 1% 的区间内。」佐格比民调所说的「该机构 95% 以上的调查结果处于选举日实际结果的正负 1% 的区间内」，是什么意思？

3.20 对男性和女性做抽样调查。练习 3.18 中描述的抽样调查，除了访谈了 1025 位女性之外，也访问了 472 位随机选出的男性。调查报告中关于女性的结论，宣称在 95% 置信度下误差范围是 ±3%。而关于男性的结论，误差范围是 ±5%。为什么男性的误差范围比女性的误差范围大？

3.21 解释置信度。一位学生读到以下叙述：我们有 95% 的把握认为，美国年轻人在「全国教育进展评估」（National Assessment of Educational Progress）中定量部分（quantitative part）的平均分数，将在 267.8~276.2。有人要求这位学生说明这段叙述的意义，学生回答道：「在所有年轻人当中，有 95% 的人所得分数将在 267.8~276.2。」这个回答正确吗？

3.22 死刑。2011 年 10 月，盖洛普民意调查访谈了 1005 位成年人，问他们「你支持对谋杀犯判处死刑吗」。赞成者的比例是 61%。

（a）在受访的 1005 人当中，有多少人支持对谋杀犯判处死刑？

（b）盖洛普公司说这次调查的误差范围是 ±4%，请你向一个不懂统计学的人解释一下「误差范围是 ±4%」是什么意思。

3.23 计算误差范围。例 6 告诉我们，「美国调查」访谈了 547 位佐治亚州的选民，问他们会投票给哪位总统候选人，结果有 51% 的人说会支持约翰·麦凯恩。用速算公式计算一下，对所有佐治亚州选民做出结论时的误差范围是多少？你的结果和例 6 中「美国调查」的误差范围相比有何差别？

3.24 计算误差范围。练习 3.22 考虑的是 1005 人的样本。用速算公式计算一下，如果对美国所有成年人做出结论，其误差范围会是多少？你的结果和盖洛普公司公布的 ±4% 的误差范围接近吗？

3.25 计算误差范围。练习 3.9 谈到了一项针对住在安大略省的 61239 位成年人展开的抽样调查。若要对安大略省的全体成年人做出结论，在 95% 的置信度下误差范围大约是多少？

3.26 对上帝的信仰。2011 年 5 月盖洛普公司所做的一项调查显示，在 509 位成年人的样本中，有 92% 的人说他们信仰上帝。

（a）用速算公式计算一下，这样的样本，其误差范围是多少。

（b）假设这是一个随机样本，请你对所有成年人中信仰上帝的比例，做出置信度说明。

3.27 堕胎。2011 年的一项哈里斯调查访谈了 2362 名成年人，发现有 1110 人允许在「某种情况下」堕胎，这比 2009 年下降了 6 个百分点。请你对所有人允许在「某种情况下」堕胎的比例做出置信度说明。（假设这是一个简单随机抽样，用速算法计算误差范围。）

3.28 道德的不确定性和统计的不确定性。在练习 3.27、案例分析与评估中，我们讨论了关于相互矛盾的道德观念的民意调查。在两个调查中，全国的民意是不一致的，表明这两件事存在相当大的「道德的不确定性」。在这两个抽样调查中，误差范围（统计的不确定性）是多大？是否有可能存在具有大的道德不确定性，却具有小的统计不确定性的事情？

3.29 缩小误差范围。练习 3.22 里谈到一项对 1005 位成年人做的抽样调查，假设你希望其误差范围只有练习中的一半大，那么你应该走访多少人？

3.30 取悦国会。练习 3.12 谈到一项对 1012 位成年人做的抽样调查，其置信度为 95%，误差范围为 ±4%。

（a）有位美国国会议员认为 95% 置信度还不够，他希望达到 99% 的置信度。对同一个样本来说，99% 置信度下的误差范围和 95% 置信度下的误差范围，有何差别？

（b）另一位国会议员觉得 95% 置信度已经足够好了，但她想要更小的误差范围。我们怎样做才可以维持 95% 的置信度，并且得到较小的误差范围？

3.31 失业率。虽然民意调查通常的置信度都是 95%，但也有抽样调查采用其他的置信度。举例来说，美国的每月失业率是根据当前人口调查走访的约 60000 个住户得来的。随着失业率一起公布的误差范围，大约是 ±0.2%，置信度为 90%。相较之下，95% 置信度下的误差范围会更小还是更大？为什么？

3.32 华尔街人士。2011 年 4 月，一项哈里斯调查访谈了一个包含 1010 位美国成年人的随机样本，问他们是否同意以下说法：「大部分华尔街人士在认为自己能赚到钱的同时也能逃脱惩罚时，愿意去违法。」结果表明有 677 人对此表示赞同。请你对这项调查结果写一个简短的报告，不要忘了说明误差范围。注意，别把个人意见与统计结果混淆在一起。

3.33 该向谁问责？2009 年 2 月由纽约州波基普西的玛利斯特学院公众意见研究所做的一项民意调查，访谈了包含 2071 位美国成年人的一个随机样本，问他们「谁或者什么应为公司的成功或失败负责」。调查对象中有 70% 的人将公司的成败归因于高层管理人员的决策。该项调查又向 110 名公司管理人员问了同样的问题，其中有 88% 的人认为最高管理层应为公司的成败负责。

玛利斯特学院报告说，其中一项抽样调查的误差范围是 ±9%，而另一个是 ±2.5%。你认为哪个抽样调查的误差范围是 ±9%，为什么？

3.34 模拟（Simulation）。随机数字可被用来模拟随机抽样的结果。假设你要从一个包含许多名大学生的总体里面，抽取一个大小为 25 的简单随机样本，总体当中有 20% 的学生在暑假期间没工作。要用随机数字模拟这个简单随机样本的话，我们可以用从表 A 当中任一处开始的连续 25 个数字，来代表我们抽取的样本中的学生。用 0 和 1 这两个数字代表没工作的学生，其他数字代表有工作的学生。这样的设计是对我们的简单随机样本的一个正确的模拟，因为 0 和 1 这两个数字在所有 10 个被选中的概率相同的数字当中占 20%。

按照以下步骤来模拟 50 个随机样本的结果，将表 A 中共 50 行中的每一行的前 25 个数字当作一个样本，数一数每个样本当中 0 和 1 共有几个。把 50 个样本的结果，用像图 3–1 那样的柱状图展示出来。总体参数的真实值（也就是未工作学生的比例，即 20%），是不是几乎位于你的柱状图的中间位置？在你的 50 个样本当中，未工作的学生人数最大是多少，最小是多少？在你的样本里面，有 4、5 或 6 个学生没工作的样本数量，占 50 个样本的百分比是多少？

3.35 网上练习。浏览 www.gallup.com 并阅读首页文章。点击 More 按钮，这篇文章会告诉你在 95% 置信度下误差范围是多大？

3.36 网上练习。点击 http://media.gallup.com/PDF/FAQ/HowArePolls.pdf，这篇文章给出了盖洛普公司对于为何小样本可以给出关于大总体的可靠结论的解释。这篇文章是怎样解释 95% 置信度的？