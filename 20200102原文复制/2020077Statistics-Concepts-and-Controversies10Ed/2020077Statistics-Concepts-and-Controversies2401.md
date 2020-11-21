Test if there is a relationship between two categorical variables.

Identify Simpson’s Paradox and understand how it occurs.

Case Study: Freedom of Speech and Political Beliefs

First Amendment rights have come to the forefront at colleges across the nation. A 2017 Gallup/Knight Foundation survey of 3014 college students examined student views on various aspects of the first amendment as well as other issues on college campuses across the United States.

Let’s look at the relationship between political party affiliation and views about freedom of speech. One question asked in the survey was,「Do you think freedom of speech is very secure, secure, threatened or very threatened in the country today?」Here is a two-way table that categorizes the 2990 students who have both a political party affiliation/lean and an opinion about free speech.

Freedom of speech Democrat Independent Republican Total

Very secure 183 20 98 301

Secure 1043 86 362 1491

Threatened 776 39 222 1037

Very threatened 112 14 35 161

Total 2114 159 717 2990

What does this table tell us about the relationship between political party affiliation and views about freedom of speech?

*This more advanced chapter is optional.

Two-Way Tables

Example 1

Racial differences in six-year graduation rates

One measurement of student success is the percent completing a bachelor’s degree within six years. The National Center for Education Statistics publishes reports annually. The following two-way table is representative of the percentages of students completing a bachelor’s degree within six years by race/ethnicity:

Race/ethnicity White Black Hispanic Asian American Indian/Alaska Native Two or more races Total

Graduated 6963 1063 1388 792 69 175 10,450

Did not graduate 3933 1614 1163 295 110 119 7234

Total 10,896 2667 2551 1087 179 294 17,684

How should we evaluate the information in this table?

Graduation status (completing a bachelor’s degree within six years or not) and race of students are both categorical variables. That is, they place individuals into categories but do not have numerical values that allow us to describe relationships by scatterplots, correlation, or regression lines. We can count the number of individuals in each category. To display relationships between two categorical variables, use a two-way table like the table of graduation status and race of applicants. Graduation status is the row variable because each row in the table describes one of the possible admission decisions for a student. Race is the column variable because each column describes one of the racial/ethnic groups. The entries in the table are the counts of students in each graduation status–by–race class.

How can we best grasp the information contained in this table? First, look at the distribution of each variable separately. The distribution of a categorical variable says how often each outcome occurred. The「Total」column at the right of the table contains the totals for each of the rows. These row totals give the distribution of graduation status for all students, for all racial/ethnic groups combined. The「Total」row at the bottom of the table gives the distribution of race for students, with both categories of graduation status (「Graduated」or「Did not graduate」) combined. It is often clearer to present these distributions using percentages. We might report the distribution of race as

Note that the percentages listed above total 99.9%, not 100%. This is another example of roundoff errors, which were introduced in Chapter 10.

The two-way table contains more information than the two distributions of graduation status alone and race alone. The nature of the relationship between graduation status and race cannot be deduced from the separate distributions but requires the full table. To describe relationships between categorical variables, calculate appropriate percentages from the counts given.

Example 2

Racial differences in six-year graduation rates, continued

Because there are only two categories of graduation status, we can see the relationship between race and graduation status by comparing the percentages of those who completed a bachelor’s degree within six years for each race:

Over 60% of the white students and more than 70% of the Asian students completed a bachelor’s degree within six years, but less than 40% of black students and American Indian/Alaska Native students completed a bachelor’s degree within six years.

In working with two-way tables, you must calculate lots of percentages. Here’s a tip to help decide what fraction gives the percentage you want. Ask,「What group represents the total that I want a percentage of?」The count for that group is the denominator of the fraction that leads to the percentage. In Example 2, we wanted the percentage of each racial/ethnic group who completed a bachelor’s degree within six years, so the counts of each race form the denominators.

Inference for a Two-Way Table

We often gather data and arrange them in a two-way table to see if two categorical variables are related to each other. The sample data are easy to investigate: turn them into percentages and look for an association between the row and column variables. Is the association in the sample evidence of an association between these variables in the entire population? Or could the sample association easily arise just from the luck of random sampling? This is a question for a significance test.

Example 3

Digital savviness and ability to distinguish facts in the news

Can you distinguish between fact and opinion in the news? A recent Pew Research Center study investigated the relationship between the ability to distinguish facts as facts (and opinions as opinions, but we leave that for you to investigate on your own) and various characteristics including age, education level, political awareness, and digital savviness. Respondents were American adults.

The following table of 1000 total respondents represents Pew’s findings. Here are the number of respondents and percentages who were able to identify all five factual statements as fact for three levels of digital savviness:

Digital savviness Number of respondents Number who got all five correct Percent correct

Very savvy 480 168 35.0

Somewhat savvy 350 70 20.0

Not savvy 170 22 12.9

The sample percentages of respondents who identified all five factual statements to be factual are quite different. In particular, the percentage of「very savvy」respondents who got all five correct was much higher than for the「somewhat savvy」and「not savvy」groups. Are these data good evidence that there is a relationship between digital savviness and ability to identify factual statements as factual in the population of all American adults?

The test that answers this question starts with a two-way table. Here’s the table for the data of Example 3:

Digital savviness All five correct Fewer than five correct Total

Very savvy 168 312 480

Somewhat savvy 70 280 350

Not savvy 22 148 170

Total 260 740 1000

Our null hypothesis, as usual, says that the level of digital savviness has no effect on the ability to identify all five factual statements as fact. That is, American adults do equally well regardless of their level of digital savviness. The differences in the sample are just the result of chance. Our null hypothesis is

There is no association between the digital savviness and whether or not a person can identify all five factual statements as fact in the population of American adults.

Expressing this hypothesis in terms of population parameters can be a bit complicated, so we will be content with the verbal statement. The alternative hypothesis just says,「Yes, there is some association between digital savviness and whether or not a person can identify all five factual statements as facts in the population of American adults.」The alternative doesn’t specify the nature of the relationship. It doesn’t say, for example,「Those who are more digitally savvy are better at identifying all five factual statements as fact.」

To test , we compare the observed counts in a two-way table with the expected counts, the counts we would expect—except for random variation—if were true. If the observed counts are far from the expected counts, that is evidence against . We can guess the expected counts for the study. In all, 260 of the 1000 respondents correctly identified all five factual statements as fact. That’s an overall success rate of 26%, because 260/1000 is 26%. If the null hypothesis is true, there is no difference among the levels of digital savviness. So we expect 26% of the respondents in each group to correctly identify all five factual statements as fact.

Key Terms

The expected count in any cell of a two-way table when is true is

Let’s classify a person who correctly identifies all five factual statements as fact as a「success」and a person who does not as a「failure.」There were 480 respondents in the very savvy group, so we expect successes and failures in this group. For the somewhat savvy group (350 respondents), we expect successes and failures. Finally, for the group of respondents who are not digitally savvy (170 respondents), we expect successes and failures.

If the groups had been the same size, the expected counts would be the same for each group. Fortunately, there is a rule that makes it easy to find expected counts. The expected count of successes in the very savvy group is

If the null hypothesis of no treatment differences is true, we expect 124.8 of the 480 digitally savvy respondents to succeed. That’s just what we calculated based on the percentages.

Now it’s your turn

24.1 Video-gaming and grades. The popularity of computer, video, online, and virtual reality games has raised concerns about their ability to negatively impact youth. Based on a recent survey, 1808 students ages 14 to 18 in Connecticut high schools were classified by their average grades and by whether they had or had not played such games. The following table summarizes the findings.

Grade Average

A’s and B’s C’s D’s and F’s

Played games 736 450 193

Never played games 205 144 80

Find the expected count of students with average grades of A’s and B’s who have played computer, video, online, or virtual reality games under the null hypothesis that there is no association between grades and game playing in the population of students. Assume that the sample was a random sample of students in Connecticut high schools.

The Chi-Square Test

To see if the data give evidence against the null hypothesis of「no relationship,」compare the counts in the two-way table with the counts we would expect if there really were no relationship. If the observed counts are far from the expected counts, that’s the evidence we were seeking. The significance test uses a statistic that measures how far apart the observed and expected counts are.

Key Terms

The chi-square statistic, denoted , is a measure of how far the observed counts in a two-way table are from the expected counts. The formula for the statistic is

The symbol means「sum over all cells in the table.」

The chi-square statistic is a sum of terms, one for each cell in the table. In Example 3, 168 of the very savvy group succeeded. The expected count for this cell is 124.8. So the term in the chi-square statistic contributed by this cell is

Example 4

Digital savviness and ability to distinguish facts in the news continued

Here are the observed and expected counts for Example 3 side by side:

Observed Expected

Success Failure Success Failure

Very savvy 168 312 124.8 355.2

Somewhat savvy 70 280 91.0 259.0

Not savvy 22 148 44.2 125.8

We can now find the chi-square statistic, adding six terms for the six contributing cells in the two-way table:

Now it’s your turn

24.2 Video-gaming and grades. The popularity of computer, video, online, and virtual reality games has raised concerns about their ability to negatively impact youth. Based on a recent survey, 1808 students ages 14 to 18 in Connecticut high schools were classified by their average grades and by whether they had or had not played such games. The following table summarizes the findings. The observed and expected counts are given side by side.

Observed Expected

A’s and B’s C’s D’s and F’s A’s and B’s C’s D’s and F’s

Played games 736 450 193 717.7 453.1 208.2

Never played games 205 144 80 223.3 140.9 64.8

Find the chi-square statistic.

The chi-square distributions

The sampling distribution of the chi-square statistic when the null hypothesis of no association is true is called a chi-square distribution.

The chi-square distributions are a family of distributions that take only nonnegative values and are skewed to the right. A specific chi-square distribution is specified by giving its degrees of freedom.

The chi-square test for a two-way table with rows and columns uses critical values from the chi-square distribution with degrees of freedom.

Because measures how far the observed counts are from what would be expected if were true, large values are evidence against . Is a large value? You know the drill: compare the observed value 41.82 against the sampling distribution that shows how would vary if the null hypothesis were true. This sampling distribution is not a Normal distribution. It is a right-skewed distribution that allows only nonnegative values because can never be negative. Moreover, the sampling distribution is different for two-way tables of different sizes. Facts about this distribution are found in the box on the left.

Statistics in Your World

More chi-square tests There are also chi-square tests for hypotheses more specific than「no relationship.」Place people in classes by social status, wait 10 years, then classify the same people again. The row and column variables are the classes at the two times. We might test the hypothesis that there has been no change in the overall distribution of social status. Or we might ask if elevations in status are balanced by matching moves down. These hypotheses can be tested by variations in the chi-square test.

Figure 24.1 shows the density curves for three members of the chi-square family of distributions. As the degrees of freedom (df) increase, the density curves become less skewed and larger values become more probable. We won’t find P-values as areas under a chi-square curve by hand, though software can do it for us. Table 24.1 is a shortcut. It shows how large the chi-square statistic must be in order to be significant at various levels. This isn’t as good as an actual P-value, but it is often good enough. Each number of degrees of freedom has a separate row in the table. We see, for example, that a chi-square statistic with 3 degrees of freedom is significant at the 5% level if it is greater than 7.81 and is significant at the 1% level if it is greater than 11.34.

Figure 24.1 The density curves for three members of the chi-square family of distributions. The sampling distributions of chi-square statistics belong to this family.

The density curves are labeled as follows: d times f equals 1, d times f equals 4, and d times f equals 8. The curve d times f equals 1, slopes drastically downwards. The curve d times f equals 4 is a left skewed curve that starts from the origin, rises up, and slopes down. The curve d times f equals 8 starts close to the origin, has a positive slope, peaks below the highest points of the other curves, and gradually slopes negatively.

Table 24.1 To be significant at level , a chi-square statistic must be larger than the table entry for

Significance Level

df 0.25 0.20 0.15 0.10 0.05 0.01 0.001

1 1.32 1.64 2.07 2.71 3.84 6.63 10.83

2 2.77 3.22 3.79 4.61 5.99 9.21 13.82

3 4.11 4.64 5.32 6.25 7.81 11.34 16.27

4 5.39 5.99 6.74 7.78 9.49 13.28 18.47

5 6.63 7.29 8.12 9.24 11.07 15.09 20.51

6 7.84 8.56 9.45 10.64 12.59 16.81 22.46

7 9.04 9.80 10.75 12.02 14.07 18.48 24.32

8 10.22 11.03 12.03 13.36 15.51 20.09 26.12

9 11.39 12.24 13.29 14.68 16.92 21.67 27.88

Example 5

Digital savviness and ability to distinguish facts in the news, conclusion

We have seen that higher levels of digital savviness are associated with more successes and fewer failures than lower levels of digital savviness. Comparing observed and expected counts gave the chi-square statistic . The last step is to assess significance.

The two-way table for Example 3 has 3 rows and 2 columns. That is, and . The chi-square statistic therefore has degrees of freedom

Look in the row of Table 24.1. We see that is larger than the critical value 9.21 required for significance at the level but smaller than the critical value 13.82 for . Example 3 shows a statistically significant relationship between digital savviness and ability to correctly identify five factual statements as facts.

The significance test says only that we have strong evidence of some association between digital savviness and success. We must look at the two-way table to see the nature of the relationship: more digital savviness appears to be related to a higher success rate.

Now it’s your turn

24.3 Video-gaming and grades. The popularity of computer, video, online, and virtual reality games has raised concerns about their ability to negatively impact youth. Based on a recent survey, 1808 students ages 14 to 18 in Connecticut high schools were classified by their average grades and by whether they had or had not played such games. The following table summarizes the findings. The observed and expected counts are given side by side.

Observed Expected

A’s and B’s C’s D’s and F’s A’s and B’s C’s D’s and F’s

Played games 736 450 193 717.7 453.1 208.2

Never played games 205 144 80 223.3 140.9 64.8

From these counts, we find that the chi-square statistic is 6.74. Does the study show that there is a statistically significant relationship between playing games and average grades? Use a significance level of 0.05.

Using the Chi-Square Test

Cell counts required for the chi-square test

You can safely use the chi-square test when no more than 20% of the expected counts are less than 5 and all individual expected counts are 1 or greater.

Like our test for a population proportion, the chi-square test uses some approximations that become more accurate as we take more observations. A rough rule for when it is safe to use this test is based on the expected counts.

Example 3 easily passes this「safety check」: the smallest expected cell count is 44.8, which means that no expected counts are less than 5. Here is a concluding example that outlines the examination of a two-way table.

Example 6

Do angry people have a greater incidence of heart disease?

People who get angry easily tend to have more heart disease. That’s the conclusion of a study that followed a random sample of 12,986 people from three locations for about 4 years. All subjects were free of heart disease at the beginning of the study. The subjects took the Spielberger Trait Anger Scale test, which measures how prone a person is to sudden anger. Here are data for the 8474 people in the sample who had normal blood pressure. CHD stands for「coronary heart disease.」This includes people who had heart attacks and those who needed medical treatment for heart disease.

Anger Score

Low Moderate High

Sample size 3110 4731 633

CHD count 53 110 27

CHD percent 1.7% 2.3% 4.3%

There is a clear trend: as the anger score increases, so does the percentage who suffer heart disease. Is this relationship between anger and heart disease statistically significant?

The first step is to write the data as a two-way table by adding the counts of subjects who did not suffer from heart disease. We also add the row and column totals, which we need to find the expected counts.

Low anger Moderate anger High anger Total

CHD 53 110 27 190

No CHD 3057 4621 606 8284

Total 3110 4731 633 8474

We can now follow the steps for a significance test, familiar from Chapter 22.

The hypotheses. The chi-square method tests these hypotheses: : no association between anger and CHD

: some association between anger and CHD

The sampling distribution. We will see that all the expected cell counts are larger than 5, so we can safely apply the chi-square test. The two-way table of anger versus CHD has two rows and three columns. We will use critical values from the chi-square distribution with degrees of freedom .

The data. First find the expected cell counts. For example, the expected count of high-anger people with CHD is

Here is the complete table of observed and expected counts side by side:

Observed Expected

Low Moderate High Low Moderate High

CHD 53 110 27 69.73 106.08 14.19

No CHD 3057 4621 606 3040.27 4624.92 618.81

Looking at these counts, we see that the high-anger group has more CHD than expected and the low-anger group has less CHD than expected. This is consistent with what the percentages in Example 6 show. The chi-square statistic is

In practice, statistical software can do all this arithmetic for you. Look at the six terms that we sum to get . Most of the total comes from just one cell: high-anger people have more CHD than expected.

Significance? Look at the line of Table 24.1. The observed chi-square is larger than the critical value 13.82 for . We have highly significant evidence that anger and heart disease are related. Statistical software can give the actual P-value. It is .

The conclusion. Can we conclude that proneness to anger causes heart disease? This is an observational study, not an experiment. It isn’t surprising to find that some lurking variables are confounded with anger. For example, people prone to anger are more likely than others to drink and smoke. The study report used advanced statistics to adjust for many differences among the three anger groups. The adjustments raised the P-value from to because the lurking variables explain some of the heart disease. This is still good evidence for a relationship if a significance level of 0.05 is used. Because the study started with a random sample of people who had no CHD and followed them forward in time, and because many lurking variables were measured and accounted for, it does give some evidence for causation. The next step might be an experiment that shows anger-prone people how to change. Will this reduce their risk of heart disease?

Simpson’s Paradox

As is the case with quantitative variables, the effects of lurking variables can change or even reverse relationships between two categorical variables. In the following example, we will find that sometimes a lurking variable might reverse the relationship of what we would expect to find in the data.

Example 7

Do medical helicopters save lives?

Accident victims are sometimes taken by helicopter from the accident scene to a hospital. Helicopters save time. Do they also save lives? Let’s compare the percentages of accident victims who die with helicopter evacuation and with the usual transport to a hospital by road. The numbers here are hypothetical, but they illustrate a phenomenon that often appears in real data.

Helicopter Road Total

Victim died 64 260 324

Victim survived 136 840 976

Total 200 1100 1300

We see that 32% (64 out of 200) of helicopter patients died, but only 24% (260 out of 1100) of the others died. That seems discouraging.

The explanation is that the helicopter is sent mostly to serious accidents, so that the victims transported by helicopter are more often seriously injured. They are more likely to die with or without helicopter evacuation. We will break the data down into a three-way table that classifies the data by the seriousness of the accident. We will present a three-way table as two or more two-way tables side by side, one for each value of the third variable. In this case there are two two-way tables, one for each method of evacuation:

Serious Accidents

Helicopter Road

Died 48 60

Survived 52 40

Total 100 100

Less Serious Accidents

Helicopter Road

Died 16 200

Survived 84 800

Total 100 1000

Inspect these tables to convince yourself that they describe the same 1300 accident victims as the original two-way table. For example, were moved by helicopter, and of these died.

Among victims of serious accidents, the helicopter saves 52% (52 out of 100) compared with 40% for road transport. If we look at less serious accidents, 84% of those transported by helicopter survive versus 80% of those transported by road. Both groups of victims have a higher survival rate when evacuated by helicopter.

How can it happen that the helicopter does better for both groups of victims but worse when all victims are combined? Look at the data: half the helicopter transport patients are from serious accidents, compared with only 100 of the 1100 road transport patients. So the helicopter carries patients who are more likely to die. The original two-way table did not take into account the seriousness of the accident and was therefore misleading. This is an example of Simpson’s paradox.

Key Terms

An association or comparison that holds for all of several groups can disappear or even reverse direction when the data are combined to form a single group. This situation is called Simpson’s paradox.

Simpson’s paradox is just an extreme form of the fact that observed associations can be misleading when there are lurking variables. Remember the caution from Chapter 15: beware the lurking variable.

Example 8

Discrimination in mortgage lending?

Studies of applications for home mortgage loans from banks show a strong racial pattern: banks reject a higher percentage of African American and Latinx (a person of Latin American origin or descent) applicants than white applicants. Over the past few years, lawsuits have been filed against major banks in California, Maryland, and Connecticut, to name a few states. One lawsuit against a bank for discrimination in lending in the Washington, D.C., area contended that the bank rejected 17.5% of African Americans but only 3.3% of whites.

The bank replies that lurking variables explain the difference in rejection rates. African Americans have (on the average) lower incomes, poorer credit records, and less secure jobs than whites. Unlike race, these are legitimate reasons to turn down a mortgage application. It is because these lurking variables are confounded with race, the bank says, that it rejects a higher percentage of African American applicants. It is even possible, thinking of Simpson’s paradox, that the bank accepts a higher percentage of African American applicants than of white applicants if we look at people with the same income and credit record.

Who is right? Both sides will hire statisticians to examine the effects of the lurking variables. Both sides will present statistical arguments supporting or refuting a charge of discrimination in lending. Unfortunately, there are no formal guidelines for how juries and judges are to assess statistical arguments. And juries and judges need not have any statistical expertise. Lurking variables and seeming paradoxes such as Simpson’s paradox make it difficult for even experts to determine the cause of the disparity in the rejection of mortgage applications. The court will eventually decide as best it can, but the decision may not be based on the statistical arguments.

Chapter 24 Summary and Exercises

Chapter 24: Statistics in Summary

Categorical variables classify individuals into groups. To display the relationship between two categorical variables, make a two-way table of counts for the groups. We describe the nature of an association between categorical variables by comparing selected percentages.

As always, lurking variables can make an observed association misleading. In some cases, an association that holds for every level of a lurking variable disappears or changes direction when we lump all levels together. This is Simpson’s paradox.

The chi-square test tells us whether an observed association in a two-way table is statistically significant. The chi-square statistic compares the counts in the table with the counts we would expect if there were no association between the row and column variables. The sampling distribution is not Normal. It is a new distribution, the chi-square distribution.

This chapter summary will help you evaluate the Case Study.

Link It

In Chapters 14 and 15, we considered relationships between two quantitative variables. In this chapter, we use two-way tables to describe relationships between two categorical variables. To explore relationships between two categorical variables, make a two-way table. Examine the distribution of each row (or each column). Differences in the patterns of the distributions suggest a relationship between the two variables. No change in these patterns suggests that there is no relationship.

As in Chapters 21, 22, and 23, we use formal statistical inference to decide if any difference in the observed patterns of the distributions is simply due to chance. We compare what we would expect cell counts to be based on the distribution of each variable separately with the cell counts actually observed. The chi-square test answers the question of whether differences in these cell counts could be due to chance.

As in Chapters 14 and 15, we must be careful not to assume that the patterns we observe would continue to hold for additional data or in a broader setting. Simpson’s paradox is an example of how such an assumption could mislead us. Simpson’s paradox occurs when the association or comparison that holds for all of several groups reverses direction when these groups are combined into a single group.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study that opened the chapter. Start by reviewing the Chapter Summary. Then answer each of the following questions in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying.

Here is the table that was presented in the Case Study at the beginning of this chapter:

Freedom of speech Democrat Independent Republican Total

Very secure 183 20 98 301

Secure 1043 86 362 1491

Threatened 776 39 222 1037

Very threatened 112 14 35 161

Total 2114 159 717 2990

What percentage of respondents are Independent?

What percentage of those who feel very secure about freedom of speech are Independent?

What percentage of those who feel secure about freedom of speech are Independent?

What percentage of those who feel threatened about freedom of speech are Independent?

What percentage of those who feel very threatened about freedom of speech are Independent?

Is there a statistically significant relationship between how a person feels about their freedom of speech and their political leaning? Assume a 5% significance level.

In this chapter you have:

Interpreted two-way tables.

Tested if there is a relationship between two categorical variables.

Identified Simpson’s paradox and understand how it occurs.

Online Resources

There are several StatTutor lessons that will help with your understanding of some of the details of the chi-square test. There is also a StatTutor lesson on Simpson’s paradox.

LearningCurve has good questions to check your understanding of the concepts.

Check the Basics

For Exercise 24.1, see page 564; for Exercise 24.2, see page 566; and for Exercise 24.3, see page 568.

The Pew Research Center conducts an annual Internet Project, which includes research related to social media. The following two-way table about the percent of U.S. adults who use Instagram is broken down by age and is based on data reported by Pew as of January 2018.

Use Instagram Yes No Total

Age 18–29 225 127 352

Age 30–49 211 317 528

Age 50–64 114 430 544

Age 52 477 529

Total 602 1351 1953

Exercises 24.4 to 24.8 are based on this table.

24.4 Instagram use. What percent of all respondents use Instagram?

11.5%

18.0%

30.8%

69.2%

24.5 Young adults who use Instagram. What percent of those age 18–29 use Instagram?

11.5%

18.0%

37.4%

63.9%

24.6 Older adults in the survey. What percent of all respondents were age 50–64?

5.8%

18.9%

21.0%

27.9%

24.7 Older adults who use Instagram. What percent of those age 50–64 use Instagram?

5.8%

18.9%

21.0%

27.9%

24.8 What does age have to do with it? Does it appear that there is a relationship between age and whether a person uses Instagram?

No, age should have nothing to do with whether a person uses Instagram.

No, the percentages of young adults and older adults who use Instagram are the same, which means there is no relationship.

Yes, older adults do not know how to use Instagram.

Yes, the percentages of young adults and older adults who use Instagram are not the same, which means there is some relationship.

Chapter 24 Exercises

24.9 Is astrology scientific? The University of Chicago’s General Social Survey (GSS) is one of the most important social science sample surveys in the United States. The GSS asked a random sample of adults their opinion about whether astrology is very or somewhat scientific or not at all scientific. Is belief that astrology is scientific related to the highest level of education earned? Here is a two-way table of counts for people in the 2016 sample who had three levels of educational achievement (High School (HS) Diploma, Bachelor’s Degree, Graduate or Professional Degree):

Degree Held

Opinion HS diploma Bachelor’s Graduate or professional

Not at all scientific 237 200 110

Very or somewhat scientific 170 60 38

Calculate percentages that describe the nature of the relationship between the highest level of education earned and the opinion about whether astrology is very scientific or somewhat sort of scientific or not at all scientific. Give a brief summary in words.

24.10 Weight-lifting injuries. Resistance training is a popular form of conditioning aimed at enhancing sports performance and is widely used among high school, college, and professional athletes, although its use for younger athletes is controversial. A random sample of 4111 patients between the ages of 8 and 30 admitted to U.S. emergency rooms with the injury code「weight lifting」was obtained. These injuries were classified as「accidental」if caused by a dropped weight or improper equipment use. The patients were also classified into the four age categories of 8 to 13 years, 14 to 18, 19 to 22, and 23 to 30. Here is a two-way table of the results:

Age Accidental Not accidental Total

8–13 295 102 397

14–18 655 916 1571

19–22 239 533 772

23–30 363 1008 1371

Total 1552 2559 4111

Calculate percentages that describe the nature of the relationship between age and whether the weight-lifting injuries were accidental or not. Give a brief summary in words.

24.11 Smoking by students and their families. How are the smoking habits of students related to the smoking habits of their close family members? Here is a two-way table from a survey of male students in six secondary schools in Malaysia:

Student smokes Student does not smoke

At least one close family member smokes 115 207

No close family member smokes 25 75

Write a brief answer to the question posed, including a comparison of selected percentages.

24.12 Smoking by parents of preschoolers. How are the smoking habits of parents of preschoolers related to the father’s highest degree earned? Here is a two-way table from a survey of the parents of preschoolers in Greece:

Both parents smoke One parent smokes Neither parent smokes

University education 42 68 90

Intermediate education 47 69 75

High school education 183 281 273

Primary education or none 69 73 62

Write a brief answer to the question posed, including a comparison of selected percentages.

24.13 Python eggs. How is the hatching of water python eggs influenced by the temperature of the snake’s nest? Researchers assigned newly laid eggs to one of three temperatures: hot, neutral (room temperature), or cold. Hot duplicates the extra warmth provided by the mother python, and cold duplicates the absence of the mother. Here are the data on the number of eggs and the number that hatched:

Eggs Hatched

Cold 27 16

Neutral 56 38

Hot 104 75

Make a two-way table of temperature by outcome (hatched or not).

Calculate the percentage of eggs in each group that hatched. The researchers anticipated that eggs would not hatch in the cold environment. Do the data support that anticipation? Assume a 5% significance level.

24.14 Firearm violence. Here are counts from a study of firearm violence reported in 2018 by the National Vital Statistics System. In particular, we will examine homicides and suicides and whether a firearm was involved.

Firearm No firearm Total

Homicides 14,415 4947 19,362

Suicides 22,938 22,027 44,965

Make a bar graph to compare whether a firearm was used in homicides and suicides. What does the graph suggest about homicides versus suicides?

Calculate the percentage of homicides and suicides in which firearms were used. Comment on your findings.

24.15 Who earns academic degrees? How do women and men compare in the pursuit of academic degrees? The table below presents counts (in thousands), as projected by the National Center for Education Statistics, of degrees that will be earned in 2026–2027 categorized by the level of the degree and the sex of the recipient.

Associate’s Bachelor’s Master’s Professional/Doctorate

Female 827 1207 557 109

Male 462 875 365 92

Total 1289 2082 922 191

How many total people are predicted to earn a degree in the 2026–2027 academic year?

How many people are predicted to earn associate’s degrees?

What percentage of each level of degree is predicted to be earned by women? Write a brief description of what the data show about the relationship between sex and degree level.

24.16 Smokers rate their health. The University of Michigan Health and Retirement Study (HRS) surveys more than 22,000 Americans over the age of 50 every 2 years. A subsample of the HRS participated in an Internet-based survey that collected information on a number of topical areas, including health (physical and mental health behaviors), psychosocial items, economics (income, assets, expectations, and consumption), and retirement. Two of the questions asked were:「Would you say your health is excellent, very good, good, fair, or poor?」and「Are you currently a cigarette smoker?」Here is the two-way table that summarizes the answers on these two questions:

Current Smoker

Health Yes No

Excellent 25 484

Very good 115 1557

Good 145 1309

Fair 90 545

Poor 29 11

Describe the differences between the distributions of health status for those who are and are not current smokers with percentages, with a graph, and in words.

24.17 Totals aren’t enough. Here are the row and column totals for a two-way table with two rows and two columns:

40

60

60 40 100

Find two different sets of counts , , , and for the body of the table that give these same totals. This shows that the relationship between two variables cannot be obtained from the two individual distributions of the variables because there is not a unique set of counts that gives the sample totals.

24.18 Airline flight delays. Here are the numbers of flights on time and delayed, for two airlines at four airports during a one-month period. Overall on-time percentages for each airline are often reported in the news. The airports that flights serve is a lurking variable that can make such reports misleading.

Alaska Airlines

American Airlines

On time Delayed On time Delayed

Los Angeles 1410 384 2690 817

Phoenix 154 32 3725 988

San Diego 595 139 532 221

Seattle 3994 2318 3702 2299

What percentage of all Alaska Airlines flights were delayed? What percentage of all American Airlines flights were delayed? These overall numbers are the numbers usually reported in the news.

Now find the percentage of delayed flights for Alaska Airlines at each of the four airports. Do the same for American Airlines.

American Airlines does worse at every one of the four airports, yet does better overall. That sounds impossible. Explain carefully, referring to the data, how this can happen. (The weather in Phoenix and Seattle lies behind this example of Simpson’s paradox.)

24.19 Bias in the jury pool? The New Zealand Department of Justice did a study of the composition of juries in court cases. Of interest was whether Maori, the indigenous people of New Zealand, were adequately represented in jury pools. Here are the results for two districts, Rotura and Nelson, in New Zealand (similar results were found in all districts):

Rotura

Maori Non-Maori

In jury pool 79 258

Not in jury pool 8810 23,751

Total 8889 24,009

Nelson

Maori Non-Maori

In jury pool 1 56

Not in jury pool 1328 32,602

Total 1329 32,658

Use these data to make a two-way table of race (Maori or non-Maori) versus jury pool status (In or Not in).

Show that Simpson’s paradox holds: a higher percentage of Maori are in the jury pool overall, but for both districts a higher percentage of non-Maori are in the jury pool.

Use the data to explain the paradox in language that a judge could understand.

24.20 Field goal shooting. Here are data on field goal shooting for two members of a men’s basketball team:

Jeremy Thomas

Harrison Greyson

Made Missed Made Missed

Two-pointers 4 2 77 45

Three-pointers 3 3 1 5

What percent of all field goal attempts did Jeremy Thomas make? What percent of all field goal attempts did Harrison Greyson make?

Now find the percent of all two-point field goals and all three-point field goals that Jeremy made. Do the same for Harrison.

Harrison had a lower percent for both types of field goals but had a better overall percent. That sounds impossible. Explain carefully, referring to the data, how this can happen.

24.21 Smokers rate their health. Exercise 24.16 gives the responses of a survey of 4310 Americans to questions about their health and whether they currently smoke cigarettes.

Do these data satisfy our guidelines for safe use of the chi-square test?

Is there a statistically significant relationship between the smoking status and opinions about health? Assume a 5% significance level.

24.22 Is astrology scientific? In Exercise 24.9, you described the relationship between belief that astrology is scientific and amount of higher education. Is the observed association between these variables statistically significant? To find out, proceed as follows:

Add the row and column totals to the two-way table in Exercise 24.9 and find the expected cell counts. Which observed counts differ most from the expected counts?

Find the chi-square statistic. Which cells contribute most to this statistic?

What are the degrees of freedom? Use Table 24.1 to say how significant the chi-square test is. Write a brief conclusion for your study.

24.23 Smoking by students and their families. In Exercise 24.11, you saw that there is an association between smoking by close family members and smoking by high school students. The students are more likely to smoke if a close family member smokes. We want to know whether this association is statistically significant.

State the hypotheses for the chi-square test. What do you think the population is?

Find the expected cell counts. Write a sentence that explains in simple language what「expected counts」are.

Find the chi-square statistic and its degrees of freedom. What is your conclusion about significance?

24.24 Python eggs. Exercise 24.13 presents data on the hatching of python eggs at three different temperatures. Does temperature have a significant effect on hatching? Write a clear summary of your work and your conclusion.

24.25 Stress and heart attacks. You read a newspaper article that describes a study of whether stress management can help reduce heart attacks. The 107 subjects all had reduced blood flow to the heart and so were at risk of a heart attack. They were assigned at random to three groups for the four-month study period. Subjects in the first group took a stress management program, while subjects in the second group participated in an exercise program. The remaining subjects did nothing aside from typical heart health care with their personal physicians. Over the three years following the four-month treatment programs, only 3 of the 33 subjects in the stress management group and 7 of the 34 subjects in the exercise group had heart attacks (fatal or non-fatal) or a surgical bypass or angioplasty, while 12 of the 40 subjects who received their typical care had heart attacks (fatal or non-fatal) or a surgical bypass or angioplasty.

Use the information in the news article to make a two-way table that describes the study results.

What are the success rates of the three treatments in preventing cardiac events?

Find the expected cell counts under the null hypothesis that there is no difference among the treatments. Verify that the expected counts meet our guideline for use of the chi-square test.

Is there a significant difference among the success rates for the three treatments?

24.26 Standards for child care. Do unregulated providers of child care in their homes follow different health and safety practices in different cities? A study looked at people who regularly provided care for someone else’s children in poor areas of three cities. The numbers who required medical releases from parents to allow medical care in an emergency were 42 of 73 providers in Newark, N.J.; 29 of 101 in Camden, N.J.; and 48 of 107 in South Chicago, Ill.

Use the chi-square test to see if there are significant differences among the proportions of child care providers who require medical releases in the three cities. What do you conclude?

How should the data be produced in order for your test to be valid? (In fact, the samples came in part from asking parents who were subjects in another study who provided their child care. The author of the study wisely did not use a statistical test. He wrote:「Application of conventional statistical procedures appropriate for random samples may produce biased and misleading results.」)

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

PART IV Review

