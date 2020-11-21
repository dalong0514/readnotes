Learn what statistical confidence and statistical significance do and do not mean.

Be able to identify abuses of statistical inference.

Case Study: Boys and Breakfast Cereal

Do the foods a woman eats prior to conceiving a baby have an effect on the sex of the baby? There is some debate about this. In 2008, the NewScientist published an article with the headline「Breakfast cereals boost chances of conceiving boys.」Other media outlets followed suit and published similar reports about the power of breakfast cereal. The reports described a research study conducted in Great Britain with a sample of 740 pregnant women. A total of 721 of these women gave a retrospective report of their typical diet in the year prior to the conception of their baby by completing a food frequency questionnaire. When the researchers analyzed data from the questionnaires, they found that of the 133 food items included on the questionnaire, breakfast cereal was the only item to be strongly associated with the sex of the baby, with those women who consumed more breakfast cereal producing a greater percentage of male infants than those women consuming less breakfast cereal.

Critics of the study were quick to point out that if there were 133 food items and possibly 133 hypothesis tests conducted, one of these tests was bound to produce a significant result just by chance alone, even if there is no impact of breakfast cereal on the sex of a baby. Why might this be the case? By the end of this chapter, you will be able to answer the question of why conducting multiple hypothesis tests in a single study can be problematic.

Using Inference Wisely

In previous chapters, we have met the two major types of statistical inference: confidence intervals and significance tests. We have, however, seen only two inference methods of each type, one designed for inference about a population proportion and the other designed for inference about a population mean . There are libraries of both books and software filled with methods for inference about various parameters in various settings. The reasoning of confidence intervals and significance tests remains the same, regardless of the method. The first step in using inference wisely is to understand your data and the questions you want to answer and fit the method to its setting. Here are some tips on inference, adapted to the settings we are familiar with.

The design of the data production matters.「Where do the data come from?」remains the first question to ask in any statistical study. Any inference method is intended for use in a specific setting. For our confidence interval and test for a proportion :

The data must be a simple random sample (SRS) from the population of interest. When you use these methods, you are acting as if the data are an SRS. In practice, it is often not possible to actually choose an SRS from the population. Your conclusions may then be open to challenge.

These methods are not correct for sample designs more complex than an SRS, such as stratified samples. There are other methods that fit these settings.

There is no correct method for inference from data haphazardly collected with bias of unknown size. Fancy formulas cannot rescue badly produced data.

Other sources of error, such as dropouts and nonresponse, are important. Remember that confidence intervals and tests use the data you collect and ignore these errors.

Example 1

The psychologist and the women’s studies professor

A psychologist is interested in how our visual perception can be fooled by optical illusions. Her subjects are students in Psychology 101 at her university. Most psychologists would agree that it’s safe to treat the students as an SRS of all people with normal vision. There is nothing special about being a student that changes visual perception.

A professor at the same university uses students in Women’s Studies 101 to examine attitudes toward violence against women and reproductive rights. Students as a group are younger than the adult population as a whole. Even among young people, students as a group come from more prosperous and better-educated homes. Even among students, this university isn’t typical of all campuses. Even on this campus, students in a women’s studies course may have opinions that are quite different from those of students who do not take Women’s Studies 101. The professor can’t reasonably act as if these students are a random sample from any population of interest other than students taking Women’s Studies 101 at this university during this term.

Statistics in Your World

Dropping out An experiment found that weight loss is significantly more effective than exercise for reducing high cholesterol and high blood pressure. The 170 subjects were randomly assigned to a weight-loss program, an exercise program, or a control group. Only 111 of the 170 subjects completed their assigned treatment, and the analysis used data from these 111. Did the dropouts create bias? Always ask about details of the data before trusting inference.

Know how confidence intervals behave. A confidence interval estimates the unknown value of a parameter and also tells us how uncertain the estimate is. All confidence intervals share these behaviors:

The confidence level says how often the method catches the true parameter when sampling many times. We never know whether this specific data set gives us an interval that contains the true value of the parameter. All we can say is that「we got this result from a method that works 95% of the time.」This data set might be one of the 5% that produce an interval that misses the true value of the parameter. If that risk is too high for you, use a 99% confidence interval.

High confidence is not free. A 99% confidence interval will be wider than a 95% confidence interval based on the same data. To be more confident, we must have more values to be confident about. There is a trade-off between how closely we can pin down the true value of the parameter (the precision of the confidence interval) and how confident we are that we have captured its true value.

Larger samples give narrower intervals. If we want high confidence and a narrow interval, we must take a larger sample. The width of our confidence interval for goes down by a factor of the square root of the sample size. To cut the interval in half, we must take four times as many observations. This is typical of many types of confidence intervals.

Know what statistical significance says. Many statistical studies hope to show that some claim is true. A clinical trial compares a new drug with a standard drug because the doctors hope that the health of patients given the new drug will improve. A psychologist studying gender differences suspects that women will do better than men (on average) on a test that measures social-networking skills. The purpose of significance tests is to weigh the evidence that the data give in favor of such claims. That is, a test helps us know if we have found what we were looking for.

To do this, we ask what would happen if the claim were not true. That’s the null hypothesis—no difference between the two drugs, no difference between women and men. A significance test answers only one question:「How strong is the evidence that the null hypothesis is not true?」A test answers this question by giving a P-value. The P-value tells us how likely data as or more extreme than ours would be if the null hypothesis were true. Data that are very unlikely and have a small P-value are good evidence that the null hypothesis is not true. We usually don’t know whether the hypothesis is true for this specific population. All we can say is that「data as or more extreme than these would occur only 5% of the time if the hypothesis were true.」

This kind of indirect evidence against the null hypothesis (and for the effect we hope to find) is less straightforward than a confidence interval. We will say more about tests in the next section.

Know what your methods require. Our significance test and confidence interval for a population proportion require that the population size be much larger than the sample size. They also require that the sample size itself be reasonably large so that the sampling distribution of the sample proportion is close to Normal. We have said little about the specifics of these requirements because the reasoning of inference is more important. Just as there are inference methods that fit stratified samples, there are methods that fit small samples and small populations. If you plan to use statistical inference in practice, you will need help from a statistician (or need to learn lots more statistics) to manage the details.

Most of us read about statistical studies more often than we actually work with data ourselves. Concentrate on the big issues, not on the details of whether the authors used exactly the right inference methods. Does the study ask the right questions? Where did the data come from? Do the results make sense? Does the study report confidence intervals so you can see both the estimated values of important parameters and how uncertain the estimates are? Does it report P-values to help convince you that findings are not just good luck?

The Woes of Significance Tests

The purpose of a significance test is usually to give evidence for the presence of some effect in the population. The effect might be a probability of heads different from one-half for a coin or a longer mean survival time for patients given a new cancer treatment. If the effect is large, it will show up in most samples—the proportion of heads among our tosses will be far from one-half, or the patients who get the new treatment will live much longer than those in the control group. Small effects, such as a probability of heads only slightly different from one-half, will often be hidden behind the chance variation in a sample. This is as it should be: big effects are easier to detect. That is, the P-value will usually be small when the population truth is far from the null hypothesis.

The「woes」of testing start with the fact that a test measures only the strength of evidence against the null hypothesis. It says nothing about how big or how important the effect we seek in the population really is. For example, our hypothesis might be「This coin is balanced.」We express this hypothesis in terms of the probability of getting a head as . No real coin is exactly balanced, so we know that this hypothesis is not exactly true. If this coin has probability of a head, we might say that, for practical purposes, it is balanced. A statistical test doesn’t think about「practical purposes.」It just asks if there is evidence that is not exactly equal to 0.5. The focus of tests on the strength of the evidence against an exact null hypothesis is the source of much confusion in using tests.

Pay particular attention to the size of the sample when you read the result of a significance test. Here’s why:

Larger samples make tests of significance more sensitive. If we toss a coin hundreds of thousands of times, a test of will often give a very low P-value when the truth for this coin is . The test is right—it found good evidence that really is not exactly equal to 0.5—but it has picked up a difference so small that it is of no practical interest. A finding can be statistically significant without being practically important.

On the other hand, tests of significance based on small samples are often not sensitive. If you toss a coin only 10 times, a test of will often give a large P-value even if the truth for this coin is . Again, the test is right—10 tosses are not enough to give good evidence against the null hypothesis. Lack of significance does not mean that there is no effect, only that we do not have good evidence for an effect. Small samples often miss important effects that are really present in the population. As cosmologist Martin Rees said,「Absence of evidence is not evidence of absence.」

Example 2

Antidepressants versus a placebo

Through a Freedom of Information Act request, two psychologists obtained 47 studies used by the U.S. Food and Drug Administration for approval of the six antidepressants prescribed most widely between 1987 and 1999. Overall, the psychologists found that there was a statistically significant difference in the effects of antidepressants compared with a placebo, with antidepressants being more effective. However, the psychologists went on to report that antidepressant pills worked 18% better than placebos, a statistically significant difference,「but not meaningful for people in clinical settings.」

Whatever the truth about the population, whether or , more observations allow us to estimate more closely. If is not 0.5, more observations will give more evidence of this, that is, a smaller P-value. Because statistical significance depends strongly on the sample size as well as on the truth about the population, statistical significance tells us nothing about how large or how practically important an effect is. Large effects (like when the null hypothesis is ) often give data that are insignificant if we take only a small sample. Small effects (like ) often give data that are highly significant if we take a large enough sample. Let’s return to a favorite example to see how significance changes with sample size.

Example 3

Count Buffon’s coin

The French naturalist Count Buffon (1707–1788) considered questions ranging from evolution to estimating the number「pi」and made it his goal to answer them. One question he explored was whether a「balanced」coin would come up heads half of the time when tossed. To investigate, Count Buffon tossed a coin 4040 times and got 2048 heads. His sample proportion of heads was

Is the Count’s coin balanced? Suppose we seek statistical significance at level 0.05. The hypotheses are

The test of significance works by locating the sample outcome on the sampling distribution that describes how would vary if the null hypothesis were true. Figure 23.1 illustrates this. It shows that the observed is not surprisingly far from 0.5 and, therefore, is not good evidence against the hypothesis that the true is 0.5. The P-value, which is 0.37, just makes this precise.

Figure 23.1 The sampling distribution of the proportion of heads in 4040 tosses of a coin if in fact the coin is balanced, for Example 3. Sample proportion 0.507 is not an unusual outcome.

The values on the horizontal axis are 0.5 and sampling proportion equals 0.507. A vertical line is drawn at sampling proportion equals 0.507 and it touches the negative slope of the normal curve. A callout pointing to the incline of the bell curve reads, Sampling distribution of sampling proportion if p equals 0.5.

Suppose that Count Buffon got the same result, , from tossing a coin 100,000 times. The sampling distribution of when the null hypothesis is true always has mean 0.5, but its standard deviation gets smaller as the sample size gets larger. Figure 23.2 displays the two sampling distributions, for and . The lower curve in this figure is the same Normal curve as in Figure 23.1, drawn on a scale that allows us to show the very tall and narrow curve for . Locating the sample outcome on the two curves, you see that the same outcome is more or less surprising depending on the size of the sample.

Figure 23.2 The two sampling distributions of the proportion of heads in 4040 and 100,000 tosses of a balanced coin, for Example 3. Sample proportion 0.507 is not unusual in 4040 tosses but is very unusual in 100,000 tosses.

A normal bell curve overlaps an elongated bell curve. The values on the horizontal axis are as follows: 0.5 and 0.507. A perpendicular line is drawn from 0.5 that touches the peak of both the normal curves. A callout pointing to the normal bell curve reads, n equals 4040. A callout pointing to the elongated bell curve reads, equals 100,000. A callout pointing to the vertical line from the point 0.507 reads, Is this outcome surprising?

The P-values are for and for . Imagine tossing a balanced coin 4040 times repeatedly. You will get a proportion of heads at least as far from one-half as Buffon’s 0.507 in about 37% of your repetitions. If you toss a balanced coin 100,000 times repeatedly, however, you will almost never (9 times in 1 million repeats) get an outcome as or more unbalanced than this.

The outcome is not evidence against the hypothesis that the coin is balanced if it comes up in 4040 tosses. It is completely convincing evidence if it comes up in 100,000 tosses.

Now it’s your turn

23.1 Weight loss. A company that sells a weight-loss program conducted a randomized experiment to determine whether people lost weight after eight weeks on the program. The company researchers report that, on average, the subjects in the study lost weight and that the weight loss was statistically significant with a P-value of 0.013. Do you find the results convincing? If so, why? If not, what additional information would you like to have?

The Advantages of Confidence Intervals

Beware the naked P-value

The P-value of a significance test depends strongly on the size of the sample, as well as on the truth about the population.

It is bad practice to report a naked P-value (a P-value by itself) without also giving the sample size and a statistic or statistics that describe the sample outcome.

Examples 2 and 3 suggest that we should not rely on significance alone in understanding a statistical study. In Example 3, just knowing that the sample proportion was helps a lot. You can decide whether this deviation from one-half is large enough to interest you. Of course, isn’t the exact truth about the coin, just the chance result of Count Buffon’s tosses. So a confidence interval, whose width shows how closely we can pin down the truth about the coin, is even more helpful. Here are the 95% confidence intervals for the true probability of a head , based on the two sample sizes in Example 3. You can check that the method of Chapter 21 gives these answers.

Number of tosses 95% confidence interval

Give a confidence interval

Confidence intervals are more informative than significance tests because they actually estimate a population parameter. They are also easier to interpret. It is good practice to give confidence intervals whenever possible.

The confidence intervals make clear what we know (with 95% confidence) about the true . The interval for 4040 tosses includes 0.5, so we are not confident that the coin is unbalanced. For 100,000 tosses, however, we are confident that the true lies between 0.504 and 0.510. In particular, we are confident that it is not 0.5.

Significance at the 5% Level Isn’t Magical

The purpose of a test of significance is to describe the degree of evidence provided by the sample against the null hypothesis. The P-value does this. But how small a P-value is convincing evidence against the null hypothesis? This depends mainly on two circumstances:

How plausible is ? If represents an assumption that the people you must convince have believed for years, strong evidence (small ) will be needed to persuade them.

What are the consequences of rejecting ? If rejecting in favor of means making an expensive changeover from one type of product packaging to another, you need strong evidence that the new packaging will boost sales.

These criteria are a bit subjective. Different people will often insist on different levels of significance. Giving the P-value allows each of us to decide individually if the evidence is sufficiently strong. But the level of significance that will satisfy us should be decided before calculating the P-value. Computing the P-value and then deciding that we are satisfied with a level of significance that is just slightly larger than this P-value is an abuse of significance testing.

Users of statistics have often emphasized standard levels of significance such as 10%, 5%, and 1%. For example, courts have tended to accept 5% as a standard in discrimination cases. This emphasis reflects the time when tables of critical values rather than computer software dominated statistical practice. The 5% level is particularly common. There is no sharp border between「significant」and「insignificant,」only increasingly strong evidence as the P-value decreases. There is no practical distinction between the P-values 0.049 and 0.051. It makes no sense to treat as a universal rule for what is significant.

STATISTICAL CONTROVERSIES

Should Hypothesis Tests Be Banned?

In January 2015, the editors of Basic and Applied Social Psychology (BASP) banned「null hypothesis significance testing procedures (NHSTP).」NHSTP is a fancy way to talk about the hypothesis testing we studied in Chapter 22. In addition to the ban on NHSTP, authors submitting articles to BASP must remove all test statistics, P-values, and statements about statistical significance from their manuscripts prior to publication. Confidence intervals, which we studied in Chapter 21, have also been banned from BASP.

What does BASP want to see from its future authors? According to the editorial,「BASP will require strong descriptive statistics, including effect sizes」and suggest using (but will not mandate) larger sample sizes than are typical in psychological research「because as the sample size increases, descriptive statistics become increasingly stable and sampling error is less of a problem.」

The editorial concludes with the editors stating that they hope other journals will join the BASP ban on NHSTP.

What is your reaction to the ban on hypothesis testing by BASP? How does the approach suggested by the editors compare with the practices that we have emphasized in this book?

Beware of Searching for Significance

Statistical significance ought to mean that you have found an effect that you were looking for. The reasoning behind statistical significance works well if you decide what effect you are seeking, design a study to search for it, and use a test of significance to weigh the evidence you get. In other settings, significance may have little meaning. Here is an example.

Example 4

Does your「sign」affect your health?

In June 2015, the Washington Post published an article that reported on researchers who examined the records of patients treated at the Columbia University Medical Center between 1900 and 2000. According to the article, the researchers examined the records of 1.75 million patients, and「using statistical analysis, [the researchers] combed through 1,688 different diseases and found 55 that had a correlation with birth month, including ADHD, reproductive performance, asthma, eyesight and ear infections.」Believers in astrology are vindicated! There is a relationship between your horoscope sign and your health. Or is there?

Before you base future decisions about your sign and your health on these findings, recall that results significant at the 5% level occur five times in 100 in the long run, even when is true. When you make dozens of tests at the 5% level, you expect a few of them to be significant by chance alone. That means that we would expect 5% of the 1688 different diseases, or about 84 diseases, to show some relationship with birth month, even when there is no association between any disease and birth month. Finding that 55 of the diseases had some relationship with birth month is actually less than we would expect if there was no relationship. The results are not surprising. Running one test and reaching the level is reasonably good evidence that you have found something. Running several dozen tests and reaching that level once or twice is not.

In Example 4, the researchers tested almost 1700 diseases and found 55 to have a relationship with birth month. Taking these results and saying that they are evidence of a relationship between your sign and your health is not appropriate. It is bad practice to confuse the roles of exploratory analysis of data (using graphs, tables, and summary statistics, like those discussed in Part II, to find suggestive patterns in data) and formal statistical inference. Finding statistical significance is not surprising if you use exploratory methods to examine many outcomes, choose the largest, and test to see if it is significantly larger than the others.

Searching data for suggestive patterns is certainly legitimate. Exploratory data analysis is an important part of statistics. But the reasoning of formal inference does not apply when your search for a striking effect in the data is successful. The remedy is clear. Once you have a hypothesis, design a study to search specifically for the effect you now think is there. If the result of this study is statistically significant, you have real evidence.

Now it’s your turn

23.2 Take me out to the ball game. A researcher compared a random sample of recently divorced men in a large city with a random sample of men from the same city who had been married at least 10 years and had never been divorced. The researcher measured 122 variables on each man and compared the two samples using 122 separate tests of significance. Only the variable measuring how often the men attended Major League Baseball games with their spouse was significant at the 1% level, with the married men attending a higher proportion of games with their spouse, on average, than the divorced men did while they were married. Is this strong evidence that attendance at Major League Baseball games improves the chance that a man will remain married? Discuss.

This might be a good place to read the「What’s the verdict?」story on page 557, and to answer the questions. This is a continuation of a story from the television series「Mythbusters」that you first examined in Chapter 6.

Inference as Decision*

Tests of significance were presented in Chapter 22 as methods for assessing the strength of evidence against the null hypothesis. The assessment is made by the P-value, which is the probability computed under the assumption that the null hypothesis is true. The alternative hypothesis (the statement we seek evidence for) enters the test only to help us see what outcomes count against the null hypothesis. Such is the theory of tests of significance as advocated by Sir Ronald A. Fisher, and as practiced by many users of statistics.

But we have also seen signs of another way of thinking in Chapter 22. A level of significance chosen in advance points to the outcome of the test as a decision. If the P-value is less than , we reject in favor of ; otherwise, we fail to reject . The transition from measuring the strength of evidence to making a decision is not a small step. It can be argued (and is argued by followers of Fisher) that making decisions is too grand a goal, especially in scientific inference. A decision is reached only after the evidence of many experiments is weighed, and indeed the goal of research is not「decision」but a gradually evolving understanding. Better that statistical inference should content itself with confidence intervals and tests of significance. Many users of statistics are content with such methods. It is rare (outside textbooks) to set up a level in advance as a rule for decision making in a scientific problem. More commonly, users think of significance at level 0.05 as a description of good evidence. This is made clearer by talking about P-values, and this newer language is spreading.

Yet there are circumstances in which a decision or action is called for as the end result of inference. Acceptance sampling is one such circumstance. The supplier of a product (for example, potatoes to be used to make potato chips) and the consumer of the product agree that each truckload of the product shall meet certain quality standards. When a truckload arrives, the consumer chooses a sample of the product to be inspected. On the basis of the sample outcome, the consumer will either accept or reject the truckload. Fisher agreed that this is a genuine decision problem. But he insisted that acceptance sampling is completely different from scientific inference. Other eminent statisticians have argued that if「decision」is given a broad meaning, almost all problems of statistical inference can be posed as problems of making decisions in the presence of uncertainty, We are not going to venture further into the arguments over how we ought to think about inference. We do want to show how a different concept—inference as decision—changes the ways of reasoning used in tests of significance.

Tests of significance focus attention on , the null hypothesis. If a decision is called for, however, there is no reason to single out . There are simply two alternatives, and we must accept one and reject the other. It is convenient to call the two alternatives and , but no longer has the special status (the statement we try to find evidence against) that it had in tests of significance. In the acceptance sampling problem, we must decide between

on the basis of a sample of the product. There is no reason to put the burden of proof on the consumer by accepting unless we have strong evidence against it. It is equally sensible to put the burden of proof on the producer by accepting unless we have strong evidence that the truckload meets standards. Producer and consumer must agree on where to place the burden of proof, but neither nor has any special status.

In a decision problem, we must give a decision rule—a recipe based on the sample that tells us what decision to make. Decision rules are expressed in terms of sample statistics, usually the same statistics we would use in a test of significance. In fact, we have already seen that a test of significance becomes a decision rule if we reject (accept ) when the sample statistics is statistically significant at level , and otherwise accept (reject ).

Suppose, then, that we use statistical significance at level as our criterion for decision. And suppose that the null hypothesis is really true. Then, sample outcomes significant at level will occur with probability . (That’s the definition of「significant at level 」; outcomes weighing strongly against occur with probability when is really true.) But now we make a wrong decision in all such outcomes, by rejecting when it is really true. That is, significance level now can be understood as the probability of a certain type of wrong decision.

Now requires equal attention. Just as rejecting (accepting ) when is really true is an error, so is accepting (rejecting ) when is really true. We can make two kinds of errors.

If we reject (accept ) when in fact is true, this is a Type I error.

If we accept (reject ) when in fact is true, this is a Type II error.

The possibilities are summed up in Figure 23.3. If is true, our decision is either correct (if we accept ) or is a Type I error. Only one error is possible at one time. Figure 23.4 applies these ideas to the acceptance sampling example.

Figure 23.3 Possible outcomes of a two-action decision problem.

Decision based on sample contains the categories Reject H 0 and Accept H 0, and Truth about the population contains the categories H 0 true and H a true.

The data read as follows.

Top-left corner: Reject H 0 and H 0 true: Type I error.

Top-right corner: Reject H 0 and H a true: Correct decision.

Bottom-left corner: Accept H 0 and H 0 true: Correct decision.

Bottom-right corner: Accept H 0 and H a true: Type II error.

Figure 23.4 Possible outcomes of an acceptance sampling decision.

Decision based on sample contains the categories Reject the truckload and Accept the truckload. And, Truth about the truckload contains the categories Does meet standards and Does not meet the standards.

The data read as follows.

Top-left corner: Reject the truckload and Does meet standards: Type I error.

Top-right corner: Reject the truckload and Does not meet standards: Correct decision.

Bottom-left corner: Accept the truckload and Does meet standards: Correct decision.

Bottom-right corner: Accept the truckload and Does not meet standards: Type II error.

So the significance level is the probability of a Type I error. In acceptance sampling, this is the probability that a good truckload will be rejected. The probability of a Type II error is the probability that a bad truckload will be accepted. A Type I error hurts the producer, while a Type II error hurts the consumer. Any decision rule is assessed in terms of the probabilities of the two types of error. This is in keeping with the idea that statistical inference is based on probability. We cannot (short of inspecting the whole truckload) guarantee that good lots will never be rejected and bad lots never accepted. But by random sampling and the laws of probability, we can say what the probabilities of both kinds of errors are. Because we can find out the monetary cost of accepting bad truckloads and rejecting good ones, we can determine how much loss the producer and consumer each will suffer in the long run from wrong decisions.

Advocates of decision theory argue that the kind of「economic」thinking natural in acceptance sampling applies to all inference problems. Even a scientific researcher decides whether to announce results, or to do another experiment, or to give up research as unproductive. Wrong decisions carry costs, though these costs are not always measured in dollars. A scientist suffers by announcing a false effect, and also by failing to detect a true effect. Decision theorists maintain that the scientist should try to give numerical weights (called utilities) to the consequences of the two types of wrong decision. Then the scientist can choose a decision rule with the error probabilities that reflect how serious the two kinds of error are. This argument has won favor where utilities are easily expressed in money. Decision theory is widely used by business in making capital investment decisions, for example. But scientific researchers have been reluctant to take this approach to statistical inference.

To sum up, in a test of significance, we focus on a single hypothesis and single probability (the P-value). The goal is to measure the strength of the sample evidence against . If the same inference problem is thought of as a decision problem, we focus on two hypotheses and give a rule for deciding between them based on sample evidence. Therefore, we must focus on two probabilities: the probabilities of the two types of error.

Such a clear distinction between the two types of thinking is helpful for understanding. In practice, the two approaches often merge, to the dismay of partisans of one or the other. We continued to call one of the hypotheses in a decision problem . In the common practice of testing hypotheses, we mix significance tests and decision rules as follows:

Choose as in a test of significance.

Think of the problem as a decision problem, so the probabilities of Type I and Type II errors are relevant.

Type I errors are usually more serious. So choose an (significance level), and consider only tests with probability of Type I error no greater than .

Among these tests, select one that makes the probability of a Type II error as small as possible. If this probability is too large, you will have to take a larger sample to reduce the chance of an error.

Testing hypotheses may seem to be a hybrid approach. It was, historically, the effective beginning of decision-oriented ideas in statistics. Hypothesis testing was developed by Jerzey Neyman* and Egon S. Pearson in the years 1928–1938. The decision theory approach came later (1940s) and grew out of the Neyman-Pearson ideas. Because decision theory in its pure form leaves you with two error probabilities and no simple rule on how to balance them, it has been used less often than tests of significance. Decision theory ideas have been applied in testing problems mainly by way of the Neyman-Pearson theory. That theory asks you to first choose , and the influence of Fisher often has led users of hypothesis testing comfortably back to or (and also back to the warnings in this chapter about this state of affairs). Fisher, who was exceedingly argumentative, violently attacked the Neyman-Pearson decision-oriented ideas, and the argument still continues.

*Neyman was born in 1894, and at the age of 85 was not only still alive but still scientifically active. In addition to developing the decision-oriented approach to testing, Neyman was also the chief architect of the theory of confidence intervals.

The reasoning of statistical inference is subtle, and the principles at issue are complex. We have (believe it or not) oversimplified the ideas of all the viewpoints mentioned and omitted several other viewpoints altogether. If you are feeling that you do not fully grasp all of the ideas of this chapter and of Chapter 22, you are in excellent company. Nonetheless, any user of statistics should make a serious effort to grasp the conflicting views on the nature of statistical inference. More than most other kinds of intellectual exercise, statistical inference can be done automatically, by recipe or by computer. These valuable shortcuts are of no worth without understanding. What Euclid said of his own science to King Ptolemy of Egypt long ago remains true of all knowledge:「There is no royal road to geometry.」

*This section is optional.

Chapter 23 Summary and Exercises

Chapter 23: Statistics in Summary

Statistical inference is less widely applicable than exploratory analysis of data. Any inference method requires the right setting—in particular, the right design for a random sample or randomized experiment.

Understanding the meaning of confidence levels and statistical significance helps prevent improper conclusions.

Increasing the number of observations has a straightforward effect on confidence intervals: the interval gets shorter for the same level of confidence.

Taking more observations usually decreases the P-value of a test when the truth about the population stays the same, making significance tests harder to interpret than confidence intervals.

A finding with a small P-value may not be practically interesting if the sample is large, and an important truth about the population may fail to be significant if the sample is small. Avoid depending on fixed significance levels such as 5% to make decisions.

If a test of significance is thought of as a decision problem, we focus on two hypotheses, and , and give a decision rule for deciding between them based on sample evidence. We can make two types of errors. If we reject (accept ) when in fact is true, this is a Type I error. If we accept (reject ) when in fact is true, this is a Type II error.

This chapter summary will help you evaluate the Case Study.

Link It

In Chapters 21 and 22, we introduced the basic reasoning behind statistical estimation and tests of significance. We applied this reasoning to the problem of making inferences about a population proportion and a population mean. In this chapter, we provided some cautions about confidence intervals and tests of significance. Some of these echo the statements made in Chapters 1 through 6 that where the data come from matters. Some cautions are based on the behavior of confidence intervals and significance tests. These cautions will help you evaluate studies that report confidence intervals or the results of a test of significance.

Case Study Evaluated

Use what you have learned in this chapter to evaluate the Case Study that opened the chapter. Start by reviewing the Chapter Summary. Then answer each of the following questions in complete sentences. Be sure to communicate clearly enough for any of your classmates to understand what you are saying. Out of 133 food items, breakfast cereal was the only item that was significantly related to the sex of a baby, with the sample of women who consumed more breakfast cereal having a greater percentage of male babies than the sample of women who consumed less breakfast cereal.

Why is it not surprising that 1 food item out of 133 food items was found to be related to the sex of a baby?

In the original research study, the researchers mention that because of the multiplicity of testing, they only considered results to be significant if the P-value was less than 0.01. Why is this important?

Why would it be problematic to rely on retrospective reports of what the women ate prior to conceiving their babies?

What are some other things that would be helpful to know about the methods used in the original research study? Please explain.

In this chapter you have:

Learned what statistical confidence and statistical significance do and do not mean.

Identified abuses of statistical inference.

Online Resources

There is a StatTutor lesson on Cautions about Significance Tests.

LearningCurve has good questions to check your understanding of the concepts.

Check the Basics

For Exercise 23.1, see page 542; and for Exercise 23.2, see page 545.

23.3 Finding statistical significance. If we conduct 100 hypothesis tests at the 5% level, how many of them would we expect to be statistically significant just by chance alone?

0

5

95

100

23.4 Width of a confidence interval. Suppose that the length of a confidence interval is 0.06 when the sample size is 400. To decrease the length of the confidence interval to 0.03, we should take a sample of size

100.

200.

800.

1600.

23.5 Practically significant? A new blend of gasoline costs $1.00 more per gallon than regular gasoline. Tests have shown that gas mileage with the new blend is statistically significantly higher than that of regular gasoline. The P-value was 0.004. A report about these results goes on to say that the new blend of gasoline increases gas mileage by 2 miles per gallon. Are these results practically significant?

No, because the P-value is small.

No, because a 2 mile-per-gallon increase is probably too small to justify an additional $1.00 per gallon.

Yes, because the P-value is small.

Yes, because a 2 mile-per-gallon increase is bigger than 0.

23.6 Practically significant? Brook conducted a study for a clothing company to determine if a rewards program caused customers to spend more. Brook found statistically significant results, with a P-value of 0.012. The average amount spent per order before the rewards program was $100, while the average amount spent per order after the rewards program was $223. Are these results practically significant?

No, because the P-value is small.

No, because an average increase of $123 per order is probably too small.

Yes, because the P-value is small.

Yes, because an average increase of $123 per order is more than twice the average amount spent per order before the rewards program.

23.7 Sacred significance level. A researcher decided prior to conducting research to use a 1% level of significance. The researcher finds a P-value of 0.027. Is it okay for the researcher to change the significance level to 5% to have statistically significant results?

No, because the significance level is set beforehand and should not be changed after the P-value has been calculated.

No, because the researcher obviously had a sample that was too small, and this is why she did not obtain significant results.

Yes, because it is okay to change the significance level after the P-value is calculated.

Yes, because the researcher should have chosen the 5% level in the first place.

Chapter 23 Exercises

23.8 A television poll. The Channel 13 news program conducts a call-in poll about the salaries of business executives. Of the 2372 callers, 1921 (or 81%) believe that business executives are vastly overpaid and that their pay should be substantially reduced. The station, following recommended practice, makes a confidence statement. They indicate that we can be 95% confident that the true proportion of citizens who believe business executives are overpaid and in need of a salary reduction is within 1.6% of the sample result. The confidence interval calculation is correct, but the conclusion is not justified. Why not?

23.9 Soccer salaries. Paris Saint-Germain, a French professional soccer team, led the 2015 ESPN/Sporting Intelligence Global Salary Survey with the largest payroll for all professional sports teams. A soccer fan looks up the salaries for all of the players on the 2015 Paris Saint-Germain team. Because the fan took a statistics course, the fan uses all of these salaries to get a 95% confidence interval for the mean salary for all 2015 Paris Saint-Germain players. This makes no sense. Why not?

23.10 How do we feel? A Gallup Poll taken in late October 2011 found that 58% of the SRS of American adults surveyed, reflecting on the day before they were surveyed, said they experienced a lot of happiness and enjoyment without a lot of stress and worry. The poll had a margin of sampling error of percentage points at 95% confidence. A news commentator at the time said the poll is surprising, given the current economic climate, in that it supports the notion that the majority of American adults are experiencing a lot of happiness and enjoyment without a lot of stress and worry. Why do you think the news commentator said this?

23.11 Legalizing marijuana. An October 2018 Gallup Poll found that 66% of the SRS of American adults surveyed support the legalization of marijuana in the United States. The poll had a margin of sampling error of percentage points at 95% confidence.

Why do the results of this survey suggest that a majority of American adults support the legalization of marijuana in the United States?

The survey was based on 1019 American adults. If we wanted the margin of sampling error to be percentage points at 95% confidence, how many Americans would need to be surveyed?

If Gallup chose to construct a 99% confidence interval rather than a 95% confidence interval, how would the margin of sampling error change?

23.12 How far do rich parents take us? How much education children get is strongly associated with the wealth and social status of their parents. In social science jargon, this is socioeconomic status (SES). But the SES of parents has little influence on whether children who have graduated from college go on to get more education. One study looked at whether college graduates took the graduate admissions tests for business, law, and other graduate programs. The effects of the parents’ SES on taking the LSAT test for law school were「both statistically insignificant and small.」

What does「statistically insignificant」mean?

Why is it important that the effects were small in size as well as insignificant?

23.13 Searching for ESP. A researcher looking for evidence of extrasensory perception (ESP) tests 200 subjects. Only one of these subjects does significantly better than random guessing.

Do the results of this study provide strong evidence that this person has ESP? Explain your answer.

What should the researcher now do to test whether the subject has ESP?

23.14 Are the drugs really effective? A March 29, 2012, article in the Columbus Dispatch reported that a former researcher at a major pharmaceutical company found that many basic studies on the effectiveness of new cancer drugs appeared to be unreliable. Among the studies the former researcher reviewed was one that had been published in a reputable journal. In this published study, a cancer drug was reported as having a statistically significant positive effect on treating cancer. For purposes of this problem, assume that statistically significant means significant at level 0.05.

Explain in language that is understandable to someone who knows no statistics what「statistically significant at level 0.05」means.

The former researcher interviewed the lead author of the published paper. The newspaper article reported that the lead author admitted that they had repeated their experiment six times and got a significant result only once but put it in the paper because it made the best story. In light of this admission, do you think that it is accurate to claim in their published study that the findings were significant at the 0.05 level? Explain your answer. (Note: A statistician can show that an event that has only probability 0.05 of occurring on any given trial will occur at least once in six trials with probability about 0.26.)

23.15 Comparing bottle designs. A company compares two designs for bottles of an energy drink by placing bottles with both designs on the shelves of several markets in a large city. Checkout scanner data on more than 10,000 bottles purchased show that more shoppers bought Design A than Design B. The difference is statistically significant . Can we conclude that consumers strongly prefer Design A? Explain your answer.

23.16 Color blindness in Africa. An anthropologist suspects that color blindness is less common in societies that live by hunting and gathering than in settled agricultural societies. He tests a number of adults in two populations in Africa, one of each type. The proportion of color-blind people is significantly lower in the hunter-gatherer population. What additional information would you want to help you decide whether you accept the claim about color blindness?

23.17 Blood types in Southeast Asia. One way to assess whether two human groups should be considered separate populations is to compare their distributions of blood types. An anthropologist finds significantly different proportions of the main human blood types (A, B, AB, O) in different tribes in central Malaysia. What other information would you want before you agree that these tribes are separate populations?

23.18 Why we seek significance. Asked why statistical significance appears so often in research reports, a student says,「Because saying that results are significant tells us that they cannot easily be explained by chance variation alone.」Do you think that this statement is essentially correct? Explain your answer.

23.19 What is significance good for? Which of the following questions does a test of significance answer?

Is the sample or experiment properly designed?

Is the observed effect due to chance?

Is the observed effect important?

23.20 What distinguishes those who have schizophrenia? Psychologists once measured 77 variables on a sample of people who had schizophrenia and a sample of people who did not have schizophrenia. They compared the two samples using 77 separate significance tests. Two of these tests were significant at the 5% level. Suppose that there is, in fact, no difference in any of the 77 variables between people who do and do not have schizophrenia in the adult population. That is, all 77 null hypotheses are true.

What is the probability that one specific test shows a difference that is significant at the 5% level?

Why is it not surprising that 2 of the 77 tests were significant at the 5% level?

23.21 Why are larger samples better? Statisticians prefer large samples. Describe briefly the effect of increasing the size of a sample (or the number of subjects in an experiment) on each of the following.

The margin of error of a 95% confidence interval.

The P-value of a test, when is false and all facts about the population remain unchanged as increases.

23.22 Is this convincing? You are planning to test a vaccine for a virus that now has no vaccine. Because the disease is usually not serious, you will expose 100 volunteers to the virus. After some time, you will record whether or not each volunteer has been infected.

Explain how you would use these 100 volunteers in a designed experiment to test the vaccine. Include all important details of designing the experiment (but don’t actually do any random allocation).

You hope to show that the vaccine is more effective than a placebo. State and . (Notice that this test compares two population proportions.)

The experiment gave a P-value of 0.15. Explain carefully what this means.

Your fellow researchers do not consider this evidence strong enough to recommend regular use of the vaccine. Do you agree?

The following two exercises are based on the optional section in this chapter.

23.23 In the courtroom. A criminal trial can be thought of as a decision problem, the two possible decisions being「guilty」and「not guilty.」Moreover, in a criminal trial there is a null hypothesis in the sense of an assertion that we will continue to hold until we have strong evidence against it. Criminal trials are, therefore, similar to hypothesis testing.

What are and in a criminal trial? Explain your choice of .

Describe in words the meaning of Type I error and Type II error in this setting, and display the possible outcomes in a diagram like Figures 23.3 and 23.4.

Suppose that you are a jury member. Having studied statistics, you think in terms of a significance level , the (subjective) probability of a Type I error. What considerations would affect your personal choice of ? (For example, would the difference between a charge of murder and a charge of shoplifting affect your personal ?)

23.24 Acceptance sampling. You are a consumer of potatoes in an acceptance sampling situation. Your acceptance sampling plan has probability 0.01 of passing a truckload of potatoes that does not meet quality standards. You might think that the truckloads that pass are almost all good. Alas, it is not so.

Explain why low probabilities of error cannot ensure that truckloads that pass are mostly good. (Hint: What happens if your supplier ships all bad truckloads?)

The paradox that most decisions can be correct (low error probabilities) and yet most truckloads that pass can be bad has important analogs in areas such as medical diagnosis. Explain why most conclusions that a patient has a rare disease can be false alarms even if the diagnostic system is correct 99% of the time.

The following exercises require carrying out the methods described in the optional sections of Chapters 21 and 22.

23.25 Liberal students. A national survey reports that the percentage of first-year college students who identify their political views as「liberal」is 31.3%. Believing that students at their college are less inclined to be「liberal,」a group of educators surveys a random sample of 125 students from their institution and finds that 27 of these students identify themselves as politically「liberal.」The proportion of students at this college who identified themselves as politically「liberal」is significantly lower than the 31.3% of all first-year students in the country who identify themselves in this way. Use the sample proportion to construct a 95% confidence interval. Does this interval include 31.3%? Explain why you are or are not surprised by this.

23.26 Do our athletes graduate? Return to the study in Exercise 22.19 (page 530), which found that 149 of 190 athletes admitted to a large university graduated within 6 years. This did not differ significantly from the 82% graduation rate for all students at the university.

It may be more informative to give a 95% confidence interval for the graduation rate of athletes. Construct this confidence interval.

Is the 82% graduation rate for all students included in your confidence interval? Explain why you are or are not surprised by this.

Suppose that 784 of an SRS of 1000 athletes admitted to a large university graduated within 6 years. In this situation, the results would differ significantly from the 82% graduation rate for all students at the university. Why are these results statistically significant when the sample proportion based on the sample of size 1000 and the sample proportion based on the sample of size 190 are both 0.784?

23.27 Holiday spending. A November 2018 Gallup Poll asked a random sample of 1037 American adults「Roughly how much money do you think you personally will spend on Christmas gifts this year?」The mean holiday spending estimate in the sample was . We will treat these data as an SRS from a Normally distributed population with standard deviation .

Give a 95% confidence interval for the mean holiday spending estimate based on these data.

The mean holiday spending estimate of included 17% of respondents who answered「No opinion.」This group includes those respondents who do not celebrate Christmas and thus reported $0. Do you trust the interval you computed in part (a) as a 95% confidence interval for the mean holiday spending estimate for all American adults? Why or why not?

23.28 Is it significant? Over several years and many thousands of students, 85% of the high school students in a large city have passed the competency test that is one of the requirements for a diploma. Now reformers claim that a new mathematics curriculum will increase the percentage who pass. A random sample of 1000 students follow the new curriculum. The school board wants to see an improvement that is statistically significant at the 5% level before it will adopt the new program for all students. If is the proportion of all students who would pass the exam if they followed the new curriculum, we must test

Suppose that 868 of the 1000 students in the sample pass the test. Show that this is not significant at the 5% level. (Follow the method of Example 3, page 521, in Chapter 22.)

Suppose that 869 of the 1000 students pass. Show that this is significant at the 5% level.

Is there a practical difference between 868 successes in 1000 tries and 869 successes? What can you conclude about the importance of a fixed significance level?

23.29 We like confidence intervals. The previous exercise compared significance tests about the proportion of all students who would pass a competency test, based on data showing that either 868 or 869 of an SRS of 1000 students passed. Give the 95% confidence interval for in both cases. The intervals make clear how uncertain we are about the true value of and how little difference there is between the two sample outcomes.

Exploring the Web

Access these exercises on the text website: macmillanlearning.com/scc10e.

What’s the Verdict?

In the Discovery Channel’s popular series Mythbusters, the hosts investigate common beliefs to determine whether there is evidence to verify them as true. In this segment, the hosts are investigating whether yawning is contagious.

https://www.discovery.com/tv-shows/mythbusters/videos/is-yawning-contagious

In Chapter 6, you examined issues regarding the design of the study. Here you will consider some of the conclusions made by the hosts of the show.

Questions

WTV23.1. The hosts reported that 29% of those who saw the yawn seed stimulus ended up yawning, and 25% of those who did not see the yawn seed stimulus yawned. One of the hosts says,「Well, it’s not dramatic, but it seems like it’s pretty good to me.」The hosts then agree that yawning is contagious. Did the hosts perform a test of statistical significance? Explain your answer.

WTV23.2. What would be the advantages of performing a test of statistical significance in this situation?

WTV23.3. Do you agree with the Mythbusters’ conclusion that yawning is contagious based on this evidence?

WTV23.4. What if the hosts had tested only two people–one in each group, with the yawn seed individual yawning and the no yawn seed individual not yawning? Would the results be more or less convincing?

WTV23.5. What if the hosts had tested 50,000 people and found the results of 25% and 29%? Would the results be more or less likely to be statistically significant?

WTV23.6. As mentioned in Chapter 6, Mythbusters recruited 50 people by posting an ad. Based on how the sample was selected, are these results likely to apply to the whole population? Why or why not?

What’s the verdict? Just looking at your sample statistics and seeing a small difference is not enough to say that the results are significant. Taking sampling variability into account and using a simple random sample are important when relating the results to the whole population.

CHAPTER 24 Two-Way Tables and the Chi-Square Test*

In this chapter you will:

Interpret two-way tables.

