# 
> 2018000模板



29. Opioids, Inequality, and Humility



Everything is complicated; if that were not so, life and poetry and everything else would be a bore.

—Wallace Stevens



In this final chapter, we apply many-model thinking to two salient policy issues: the opioid epidemic and economic inequality. We show how by engaging multiple models, we can better reason through these issues and better communicate why both have proven so difficult to solve. We can also see how, particularly in the case of opioids, experts might have used multiple models to anticipate the crisis before it occurred. That said, we do not want to oversell the potential for models to avoid disaster. Our treatment of the opioid epidemic is superficial, meant only as a template for how to apply many models when reasoning through a proposed policy or action. We do not gather data or calibrate any models. Rather, we apply the models qualitatively to gain insights.

Our analysis of income inequality, on the other hand, includes more detail and connects more tightly to the academic literature. It represents the other extreme of many-model thinking, where we deeply engage a variety of models. In both cases, thinking with many models makes us more knowledgeable and wiser. The chapter concludes with a brief comment on the need for humility. Models can make us wiser, but complex systems by definition are difficult to predict and understand. We will make mistakes. And we can learn from those mistakes to become even wiser.





Many Models and the Opioid Epidemic


To give some sense of the scale of the opioid epidemic in 2015, in the state of Massachusetts over 4% of the population above age 11 had an opioid use disorder according to one estimate. Nationwide, in 2016, doctors wrote more than 200 million prescriptions for opioids, between 10 and 12 million people misused opioids, over 2 million people were classified as having an opioid use disorder, and more than 30,000 people died from opioid-related causes.

The primary reason that so many opioids were prescribed was that they work: they reduce pain. Given the 100 million Americans with chronic pain, opioids had an enormous potential market. The danger with opioids was, of course, the potential for people to become addicted. To make sense of how opioids received approval and how the epidemic arose, we apply four models to generate some core intuitions as to how the crisis came to be.

The first model, the multi-armed bandit model, explains why opioids were approved for use. When seeking drug approval, a pharmaceutical company runs clinical trials to demonstrate drug efficacy and a lack of deleterious side effects. We can model a clinical trial as a multi-armed bandit problem where one arm corresponds to prescribing the new drug and the other arm corresponds to a placebo or the existing drug.





A Model of Opioid Approval


Multi-Armed Bandit Model

To demonstrate their efficacy, opioids were tested against placebos. In clinical trials, patients were randomly assigned to take either opioids or a placebo. The assignment of the opioid can be modeled as one arm of a two-armed bandit and the placebo as the other arm. At the end of treatment, each trial is classified as a success or a failure. Clinical tests found that patients who received opioids experienced (statistically) significantly less pain. Tests on patients who had hip replacements, dental surgery, and cancer treatments all found that opioids outperform placebos.



With any drug, the potential for addiction is a concern. Tests showed that a small percentage of patients, fewer than 1%, became addicted, allowing the drug to be approved. those tests did not take into account the possibility that doctors would write longer prescriptions, in some cases a month’s supply. The longer an individual takes opioids, the more likely that person becomes addicted. Empirical addiction rates exceeded 2.5% for patients with longer prescriptions. The Markov model shown in the box below shows how an increase in those rates from 1% to 2.5% can increase the equilibrium number of addicts 5-fold.

The model’s transition probabilities are only loosely calibrated to data. We are using the model to build intuition for how a relatively small rate of addiction can lead to a large number of addicts. By experimenting with the model, we find that if we lower the probability of leaving the addict state and increase the probability of moving from the no-pain state to the opioid state, then the proportion of addicts can increase dramatically. If, for example, we lower the transition from addict to no pain to 1% in the second model, the proportion of addicts increases to 35%. One implication of this type of model thinking has been that some health care providers, such as Blue Cross, now limit the number of pills a doctor can prescribe. In addition, some states, including the State of Michigan, have passed laws restricting the number of pills in a single prescription.





Transition-to-Addiction Model


Markov Model

A three-state Markov model reveals a nonlinear relationship between transitions to addiction and overall addiction rates. The model’s states represent people not in pain, people using opioids, and addicts. We estimate the transition probabilities between those states, which we represent as arrows. The model on the left assumes that 1% of of people who use opioids become addicted and that 10% of addicts revert to the no-pain state. It also assumes that 20% of the people in the no-pain state become opioid users. In equilibrium, only 2.2% of the population are addicts. To account for longer prescriptions, the model on the left assumes that 2.5% of people who use opioids become addicted and that 5% of addicts revert to the no-pain state. It also assumes that 20% of the people in the no-pain state become opioid users. Now, in equilibrium, 10% of the population are addicts.1





Our third model relies on systems dynamics. This model, like the Markov model, assumes that there are people in pain, people who use opioids, and people no longer in pain. Rather than write transition probabilities between these states, however, it imagines a flow from people in pain to opioid use to people not in pain. More elaborate systems dynamics models can include sources for other drug providers, and allow for movements between opioid and heroin users. In addition, a richer model could include heterogenous types of potential users. The fact that people who suffer from anxiety and depression are more likely to become addicted could therefore be included in the model.2





Paths to Heroin Addiction


Systems Dynamics Model

A population of people in pain produces opioid users and addicts. People on opioids flow into the no-pain state and also flow into the addict state. Addicts, in turn, can become heroin users. One reason that people use heroin is that they can no longer get opioids. Thus, as the flow of opioids increases, so does the number of heroin users.





A possible final model, which we do not write down formally, relies on social networks to explain why maps of per-capita opioid use show clustering in rural counties. From our analysis of the square root rules, we know that smaller populations should have higher variation. (Recall the example of the best and worst performing schools being small.) Higher use in rural areas could also be due to doctors writing longer prescriptions for rural patients who live farther from pharmacies. Those explanations aside, the clustering exceeds what would occur randomly.

Clustering could arise if people provide or sell opioids to neighbors. Unlike used furniture, which people can sell by placing ads, opioids most often sell through personal connections. A model of opioid selling would assume a social network of family and friends within which people distribute opioids. Such a model would produce the local clusters of opioid abusers seen in data.3





Figure 29.1: Income Shares of the Top 0.1% 1916–2010. Source: Piketty 2011.





Many Models of Inequality


Our final many-model exercise delves relatively deep and wide into the causes of economic inequality. We undertake this effort for three reasons. First, inequality is one of the most important policy issues of our time. Income and wealth correlate with human flourishing. Higher-income individuals enjoy better health, longer life expectancy, and higher life satisfaction and happiness. Those at the bottom of the income distribution experience higher rates of homicide, divorce, mental illness, and anxiety.4 We must be careful not to confuse correlation with causation: a substantial part of this correlation can be explained by the fact that healthier, happier people earn more money. Nevertheless, almost all studies show a connection between income and flourishing. No one prefers to be poorer. Second, we have a plethora of models of inequality written by a diversely tooled collection of economists, sociologists, political scientists, and even physicists and biologists. Third, we have abundant data on income and wealth within and across countries. We have both current data and time series stretching back hundreds of years.

We start by summarizing some empirical regularities. First, in all countries at all times, the distribution of income has an elongated tail, with many low-income people and a small percentage of people who earn large incomes. Historically, income distributions were calibrated to lognormal distribution or Pareto distributions. Recently, more granular data reveals the tail to be longer than lognormal, though not quite that described by a power law. Wealth distribution is similarly skewed.

Second, within most developed countries, income and wealth inequality, however measured, have been rising in recent decades. Current levels of income and wealth inequality in the United States approach those of the Gilded Age. Shifts in entire distributions can be hard to discern, so, following convention, we describe those shifts with respect to the share of income that goes to the upper tail of the distribution. Figure 29.1 shows how the top 0.1% has increased its share of income. The share of income to the top 0.1% of families fell steadily through 1950, and remained stable at less than 4% until around 1980, when it began to climb. In 2018, the proportion of total wealth own by these super rich was around 10%.

Third, globally, the number of people living in poverty has dropped precipitously. We should see no logical contradiction in these opposing trends. Fast-rising incomes in poor countries reduce cross-country differences and more than offset within-country increases in inequality. Our model of group selection produced similar effects. The growth in the number of altruistic communities outpaced the trend toward selfishness within each community.

Inequality has multiple, interwoven causes. Economic forces, sociological trends, exercises of political power, and the weight of history all contribute to disparities. Thus, as Steven Durlauf points out, we should not try to explain the levels or trends in disparities with a single equation. Nor should we base policy on one.5 We must be nuanced in our thinking. The processes concentrating wealth and income in the top 1% or top 0.1% may be unrelated to the forces trapping the bottom 20% in a cycle of poverty. To understand the disparate causes, we need many models.

We start by describing models that explain the changing distribution of income. Income has four sources: wages and salaries, business income, capital income, and capital gains. The relative sizes of those shares varies with income level. Low-income people earn few capital gains or capital income. Many of the highest earners receive substantial income from every category. They earn income from wages, businesses, and capital.

Our first model extends the Cobb-Douglas production model to include two types of labor: educated and uneducated. The wage paid to a type of labor depends on the relative supply of that type and on technology.6 This model explains the recent rise in inequality based on supply and demand. During the 1950s, the rise in manufacturing increased demand for uneducated workers. At the same time, increased college enrollments due in part to the GI Bill increased the supply of educated workers. In the 1980s, decreased incentives to attend college slowed the growth in the number of college graduates, and a subsequent inflow of immigrants with low education levels increased the supply of low-skilled workers. At the same time, technological changes—the rise of automated manufacturing and the transition to a more digital economy—increased the relative value of educated workers, and their rising wages reflected this value.

Time series data on average incomes by education level fit this model reasonably well. For this reason, many economists rely on the model to guide policy. The model advocates increasing access to education, as that will depress the wages of educated workers and reduce inequality. This model explains broad trends well, but it cannot explain the increase in variation within each income class.





Technology and Human Capital Model


Growth Model

Output depends on physical capital (K), educated labor (S), and uneducated labor (U) as follows:

Output = AKαSβ Uγ

The parameters A, α, β, and γ capture the technology and the relative value of the three types of labor. The relative market wage for high- and low-skilled workers is:7





Cause of inequality: Technological changes that favor educated workers increase β and decrease γ. These changes, along with increases in the supply of low-skilled workers, increase inequality.



The next model, the positive feedback model, can explain the increased variation within professions. It focuses on the tail of the distribution and, in particular, on entrepreneurs. In 2011, entrepreneurs made up 70% of the 400 wealthiest individuals in the United States.8 The model assumes that technologies—the internet and smartphones in particular—have made us more connected and more influenced by the choices of others.9 A person buying wireless stereo speakers can read reviews online and select “the best” from among a dozen choices. In the past, that person might have had a single option at her local stereo store. Now, a person who twists her knee can search the web and learn the identity of her favorite athlete’s doctor. That behavior creates a positive feedback and more inequality. We model socially influenced economic choices by reframing the preferential attachment model as a model that links positive feedbacks to talent.

Though the positive feedbacks model cannot be fitted to time series data with the same fidelity as the previous technology model, we can look to experiments to see how feedbacks contribute to inequality. Recall the music lab experiments described in Chapter 6. College students sampled and downloaded music under two treatments. In the first treatment, subjects could not see what music others had downloaded. This treatment captures the pre-internet world. In the second treatment, subjects could see the download numbers for each song. In the treatment without social information, no song receives more than two hundred downloads and only one song receives fewer than thirty. When people can see downloads, one song receives more than three hundred downloads and over half receive fewer than thirty. Information and social influence amplify the Matthew effect. The rich get even richer, and the poor become relatively poorer.





Positive Feedbacks to Talent


Preferential Attachment Model

There exist N producers, and each begins with zero sales. The first consumer buys from a random producer with zero sales, giving that producer positive sales. Each subsequent consumer with probability p buys from a producer with zero sales and with probability (1 − p) buys from a producer with positive sales. When buying from a producer with positive sales, a customer selects randomly, with the probability of choosing a particular producer that is proportional to that producer’s sales.

Cause of inequality: Increased connectedness increases social influences, creating a positive feedback.



We can apply that same logic to the economy writ large.10 The potential for positive feedbacks through social networks to contribute to inequality depends in part on the nature of what people buy. Weightless goods such as movie and music downloads, web applications, and some technologies can be scaled quickly, if not immediately. Tractors, cars, and washing machines cannot be duplicated by clicking on an icon. So while a new smartphone application can scale up with little to no capital outlay, a best-selling car cannot. As a benchmark, in May 2015, Volvo announced that it would build its S60 sedan in South Carolina. The company broke ground on the plant in September 2015 with the expectation that the first cars would roll off the line in late 2018.

Our next model applies the spatial voting model to explain the rise in CEO pay, which is not determined by social forces. In 2012, the average income of a CEO at a Fortune 500 company exceeded $10 million, or roughly 300 times the average pay of a worker. By comparison, in 1966, the CEO made only about 25 times the average worker’s salary. CEOs in other countries earn much less. In Japan, CEOs earn about 10 times what the average worker does. In Canada and throughout Europe, CEOs earn approximately 20 times the pay of the average worker.

At most companies, the CEO’s pay is set by a compensation committee consisting of members of the board of directors. That pay includes salary, bonuses, and stock options. The people who determine the pay of CEOs are often other CEOs. They have an incentive for the pay of other CEOs to be high in order to drive up their own pay. We can use the spatial model to represent the preferences of the compensation committee. According to the spatial model, the salary will be set at the median voter’s preferences. The difference in CEO pay by country can be explained by the composition of boards and the compensation committees. In Germany, boards of directors include workers, who prefer that the CEO be paid less.





CEO Political Capture


Spatial Voting Model

CEO pay is determined by a vote of a compensation committee. In the United States, compensation committees include many current and former CEOs, who prefer higher pay, as well as compensation experts (X). Other countries include workers (W) on compensation committees, resulting in a median voter who prefers much lower pay.





Cause of inequality: CEOs determine their own pay through capture. Increases in the pay of any one CEO shifts preferences toward higher pay for all CEOs.



The model explains the rise in CEO pay based on the preferences of board members about what appropriate CEO pay should be. Here we can refer back to multiple models of value. It could be that the preferences of compensation committee members rely on model based thinking informed by data. However, those preferences might also be socially constructed or part of an elaborate log roll, in which CEOs vote to raise one another’s pay.

Our next model of income inequality comes from Thomas Piketty’s best-selling book Capital in the Twenty-First Century. This is less a model than an observation that the rate of return on capital exceeds the growth rate of capital. When that holds, the portion of income that high-income individuals receive from returns on capital will increase over time. By constructing more elaborate versions of the growth models from Chapter 8, it can be shown that the return to capital should always exceed the rate of growth in the broader economy. Over the long haul, an economy might grow at less than 2% or 3%, but returns to capital may be more than double that.

It follows that in an economy that consists of workers who earn wages and capitalists who earn income from rents, the share of income going to capitalists will increase. To be a bit more formal, the rate at which capital increases will depend on three rates: the consumption rate, the tax rate, and the return on capital. Consumption depends on the level of capital. A person with little capital will consume a large percentage of her income. A person who owns a substantial amount of capital will consume a small percentage of her income. As shown formally in the box below, if we make the consumption level constant, the consumption rate will equal that amount divided by the level of capital. Thus, wealthier people will consume at a lower rate making it more likely that their net capital increases.





Rent-from-Capital Model (Piketty)


Rule of 72

The economy consists of workers and capitalists. The wages of workers increase at a rate g, the growth rate in the economy. The capitalists have wealth Wt at time t and earn return r (net of taxes) and consume a constant amount A. The income of capitalists will increase faster than that of workers if and only if





Cause of inequality: In a market economy, the rate of return on capital exceeds the overall rate of growth (r > g). Capitalists with large accumulations of wealth spend a small proportion of their income from capital on consumption, so their share of total income increases over time.



To see how the difference in rates produces inequality, we can apply the rule of 72. If initially the incomes of workers equal those of capitalists and wages grow at 2% while capital grows at 6%, then in thirty-six years wages double but income from capital increases 8-fold. Within seventy-two years, capitalists earn sixty-four times the income of workers.

Piketty applies this model to explain long-term trends in inequality of both income and wealth. The model calibrates remarkably well with three centuries of data from France and England. The model also sheds light on patterns of inequality over the past century in the United States and Europe, in which the two world wars destroyed capital stocks in Europe, evening out the income and capital distributions there. One reason the model fits the data as well as it does is that it omits two effects that cancel out. By excluding entrepreneurs, the model understates inequality. In assuming that all succeeding generations of capitalists invest wisely—not all do—the model overstates capital accumulations contribution to inequality. The creation of a new class of rich individuals and the loss of an old class of rich individuals need not balance out. A more granular model would include movement in and out of the wealthy class.

That caveat aside, the model’s implication is that so long as capital increases, capitalists earn an increasing portion of the economic pie. If we keep applying the rule of 72, we find that the income of the capitalists eventually dwarfs that of the workers. The problem of capital accumulation has a straightforward solution: impose a wealth tax. That may not be politically possible. As an alternative, we might wait for a war or revolution to redistribute wealth by force or for some technological breakthroughs that produces a new set of wealthy capitalists.

Our next two models give priority to sociological forces. Both also have strong empirical support. The first explains rising inequality based on assortative mating. A family’s income depends on the incomes of both partners. If a low-income person marries a high-income person, then that marriage will contribute toward equalizing income distributions. If high-income people marry other high earners, then income disparities will increase. Most people marry at an age when a potential partner’s lifetime income cannot be known with certainty. People do know the education level and general health of potential partners and get signals of their ambitions. Evidence shows that as men and women become more educated and earn higher incomes—refer back to the technology and human capital model—they choose life partners who also have higher education levels.

The increase in inequality results from the following factors. First, women increasingly earn college degrees. Second, relative income increases with education level. Third, educated men and women prefer educated partners. It follows that families with two educated people will be more likely to have two high incomes contributing to household-level income inequality. The logic is airtight. The only question concerns the size of the effect.11

Sociologists calibrate the model by categorizing people into five education levels: dropout, high school, some college, college degree, and postgraduate. They then calculate the average income for each education level and fit the data for the number of marriages between each pair of education levels, resulting in a crude approximation of the impact of assortative mating.





Assortative Mating


Sorting Model and Categories

Each individual has an education level: {1, 2, 3, 4, 5} where 1 = dropout, 2 = high school diploma, 3 = some college, 4 = college degree, and 5 = postgraduate.

Let P(m, j) and P(w, j) denote the probability that a man and woman have education level j. Income(g, l) equals the (estimated) income of a person of gender g and income level l. Household income for a couple consisting of a man with education level lM and a woman with education level lW earns the following estimated household income:12

Income(M, lM) + Income(W, lW)

Cause of inequality: Increases in the number of educated women, increased pay for workers with higher levels of education, and assortative mating (the tendency for people to marry others of the same income level) result in an increase in household-level income inequality.



Had marriages been random rather than assortative, income inequality would be much less. One study finds that inequality as measured by the Gini coefficient, a common measure of inequality, would have decreased by 25%.13

Our next model analyzes movements between income categories using a Markov model. It categorizes people (or households) by income level: high, upper middle, lower middle, and low. Each category contains one-fourth of the distribution. Given a time period—it could be a year, a decade, or a generation—we can then estimate the transition probabilities between income categories to capture mobility.





Intergeneration Income (Wealth) Dynamics


Markov Model

The population can be divided into four income (or wealth) categories with equal numbers of people. We can estimate the transition probability that an individual (or family) in one category moves to another category within a generation, as shown in the figure below. More equal transition probabilities correspond to greater social mobility.





Transition Probabilities Between Income Levels

Cause of inequality: Social skills, tacit knowledge, attitudes toward risk and education, and bequests reduce mobility between income classes.



If there were no stickiness across generations, then the income of the child of a high-income parent would be equally likely to belong to any of the four income classes—all of the transition probabilities equal . In the most extreme case of no mobility, transition probabilities would consist of only 1s along the diagonal. Empirical estimates suggest that the reality lies between these extremes.

We can run experiments by taking 100 randomly selected low- or high-income families and computing the probability distribution of incomes in subsequent generations. Using the probabilities shown in the box, the children of high-income parents have a 60% chance of being high-income and only a 5% chance of being low-income. The grandchildren of the high-income parent have less than a 43% chance of being high-income and more than a 10% chance of being low-income.14

The income dynamics model also serves as a baseline from which to evaluate the causes of income mobility. We might use a linear model to estimate a child’s income as a function of parental wealth, parental income, and parental ability levels (assuming we had data). The Piketty model would imply a positive coefficient on parental wealth. The ability-based model would imply a positive coefficient on parental ability given that there exists some correlation between parental ability and ability of offspring.

Note that determining the coefficient on parental income requires data on the income of each child and each parent. Scholars have individual-level income data only for the past few decades. In The Son Also Rises, Gregory Clark (2014) found a novel solution to the problem of lack of data: he relies on surnames. He calculates the average income of everyone named, say, Thatcher, in 1888 and compares this to the average income of everyone named Thatcher in 1917. The thirty-year increment represents the length of a work life. He finds substantial correlation across surnames’ average incomes, suggesting a lack of income mobility.

This type of model allows us to identify racial differences in intergenerational transfers. African Americans exhibit less persistence of wealth at the top of the income distribution and more persistence at the low end. A wealthy African American will be less likely to have wealthy children, and a poor African American will be more likely to have poor children.15

Our last model based on neighborhood effects, Durlauf’s persistent inequality model, leverages the empirical regularity that people segregate by income category—that is, high-income people live in communities with other high-income people and low-income people live near low-income people. Segregation by income produces economic, sociological, and psychological externalities that reduce mobility. In the model, an individual’s income depends on ability, educational spending, and spillovers.

The educational attribute captures public spending on education, which empirically correlates with average income: high-income locations spend more on education than low-income locations, resulting in better educational outcomes and higher incomes for children in high-income neighborhoods.

The spillover term can be interpreted as socially transmitted knowledge of appropriate tools to acquire. Here we can link Durlauf’s model to how people who live in high-income communities gain awareness of appropriate tools. We can also link the model to our network model and the strength of weak ties phenomenon: people who live in high-income communities will be connected indirectly to more people with access to economically valuable information. This will produce a positive feedback on income.

We can also interpret the spillover as socially transmitted behaviors, such as the number of hours spent studying or working. If income includes a random component, then a person in a low-income community will see (correctly) a low return to time spent on self-improvement. Relatedly, the spillover could include psychological attributes—a positive or negative outlook on life, a feeling of safety, or a belief in oneself.





Persistent Inequality (Durlauf)


Schelling Segregation Model + Local Majority Model

Individuals belong to income classes and segregate residentially by income. Individuals allocate a portion of their income to education, resulting in positive spillovers that increase with community income level. The future income of a child living in community C depends on her innate ability, spending on education, and spillovers. The contributions of education and spillovers depend on the level of income within the community, IC.

IncomeC = F(ability, education(IC), spillover(IC))

Cause of inequality: Children who grow up in low-income neighborhoods receive fewer educational opportunities and economic spillovers.



In the complete model, Durlauf solves for equilibrium levels of educational spending and derives conditions in which persistent inequality arises. That inequality results from what he calls poverty traps. Individuals living in low-income communities lack the educational resources and levels of spillovers necessary to earn high incomes regardless of their ability levels. Durlauf’s model can help to explain the enormous racial gaps in income levels. African Americans disproportionately live in poor neighborhoods, and as a result, they may become trapped in low income trajectories because of a lack of resources.

These various models describe distinct causes of income inequality. In a sense, each is correct, but, as we know, each model is also wrong. Empirically, the models differ in how much and what part of the variation in income they can explain. For the upper end of the income distribution, the empirical evidence most strongly supports the models that rely on technological change.16 For over twenty years, the IRS has tracked the highest 400 incomes. Those at the top of the distribution come from technology, mass retail, and finance, three industries that can scale quickly. That high growth rate could stem from winner-take-all markets for search engines (Google) or social networking sites (Facebook). These models tell us little about the lower end of the income distribution. Nor do they say much about income mobility, or explain why CEO pay in the United States far exceeds that in other countries.

To explain these other features of the data, we need the other models, such as the income mobility model, Durlauf’s persistent inequality model, and the spatial voting model. By constructing a dialogue between multiple models and data, we come away with a deep, multifaceted understanding of the causes of inequality. We identify multiple processes that produce and maintain inequality and see how they overlap and intersect. Our understanding of the complexity of inequality and the self-reinforcing causal forces that sustain it should make us dubious of quick fixes. Reducing inequality will require concentrated efforts on multiple fronts.





Into the World


We have just learned how by applying many models as an ensemble we can explicate the multiple causes of the opioid epidemic and income equality and reveal the limits of any one framing. Were we policymakers, we could fit some of these models to data to gauge effect sizes. We could then run natural experiments to help us guide policy choices based on what we have learned.

We could also take the many model approach to any number of social challenge including reversing trends in obesity, improving school performance, mitigating climate change, managing water resources, and improving international relations. In each case, even adding a single new model could have enormous consequences. Take for example the problem of predicting financial collapses. The United States Federal Reserve relies on traditional economic models using national accounting data on inflation, unemployment, and inventories. Those data suffer from lags. They are released weekly, quarterly, or annually. Those data also come from surveys, that is, samples of the entire economy.

Complexity scholar, J. Doyne Farmer argues for creating a second class of models based on real time data scraped from the web. These new models would rely on more granular, instantaneous data, and therefore differ from traditional models. Farmer argues that such models could prove much better than existing models. He may be right. Yet, these new models need not be more accurate to be of use in predicting and preventing financial disasters. Given the new models would use different data and rely on different assumptions, they would make different predictions. As we know from the diversity prediction theorem so long as the new models are not far less accurate, when combined with existing models, these new models would improve predictions. Policy makers, to use Farmer’s turn of phrase, would be more collectively aware.17

An executive might engage in a similar exercise when making a business decision. She could apply multiple models informed by data to decide on product attributes, time product launches, design compensation plans, construct supply chains, and forecast sales. Because each of these actions occurs within a complex system, any one model would be wrong. Many models would lead to better actions.

To sum up, when confronted with a choice, when asked to make a prediction, or when faced with a design challenge, we should take a many-model approach. Many-model thinking produces better performance than taking actions based on hunches and gut instincts. That said, we have no guarantee of success. Even with many models, we may not identify the most relevant logical chain. The domain of interest might be so complex that even ensembles of models can only explain a small portion of the variation.

The same holds when applying models to aid in design, we may find ourselves unable to construct useful abstractions. The simplicity of models may, in those cases, be their undoing. In the face of complexity, it is possible that we find models not up to the tasks of communicating ideas, making accurate predictions, or pointing us toward the best actions. Even our explorations with models may reveal little of value. In those instances, the REDCAPEs that the book has promised will not provide much lift. Nevertheless, even in those cases, we benefit from contemplating and applying many models. In doing so, we uncover interdependencies. We learn why a complex process can frustrate our attempts to understand, explain, or communicate.

Thus, we must maintain a degree of humility. Even aided by many models, our abilities to reason have limits. For that reason, we must remain curious. We must continue to build new models and to improve upon existing ones. If a model leaves out key features of the world—such as social influences, positive feedbacks, or cognitive biases—then we should build other models that include those features. By doing so, we can begin to discern when those attributes matter and how much. The fact that all models are wrong should not take the wind out of our sails but be seen as motivation for building a crowd of models capable of producing wisdom.

Last, we should seek joy in those efforts. Though the book has emphasized pragmatic aims—to become better thinkers, to be more effective at work, and to operate as more informed citizens of the world—it has also had an implicit goal of revealing the beauty of models and the fun of modeling. The practice of modeling can be a beautiful game. We make the assumptions, write the rules, and then play within those rules bound also by the laws of logic. Through our logical explorations, we improve ourselves and become wise. May we take that wisdom out into the world and help to change it in positive ways.





SCOTT E. PAGE is the Leonid Hurwicz Collegiate Professor of Complex Systems, Political Science, and Economics at the University of Michigan and an external faculty member of the Santa Fe Institute.

Photo Credit: Cooper Page



