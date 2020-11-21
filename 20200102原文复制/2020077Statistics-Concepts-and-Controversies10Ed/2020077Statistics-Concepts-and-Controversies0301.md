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

CHAPTER 4 Sample Surveys in the Real World

In this chapter you will:

