# 
> 2018000模板


18. Systems Dynamics Models





The principles governing the behavior of systems are not widely understood.

—Jay Wright Forrester



In this chapter, we cover systems dynamics models.1 These models analyze systems with feedbacks and interdependencies. They are used to model ecologies and economies, supply chains and production processes. They improve our capacity to think through logical chains that include negative and positive feedbacks. A systems dynamics model consists of sources, sinks, stocks, flows, rates, and constants. Sources produce inputs into the system. Sinks absorb outputs. Stocks keep track of levels of variables, and flows capture feedbacks between levels of stocks. Rates and constants apply to the flows, which can be fixed or change over time.

Systems dynamics models can include both positive and negative feedbacks. Positive feedbacks, such as the Matthew effect covered in Chapter 6, occur when an increase in a variable or attribute produces an additional increase in that same variable. Success breeds success, sales lead to more sales, and, in the case of academic papers and patents, citations generate more citations.

Negative feedbacks dampen trends. We must be careful not to infer normative implications from the word negative. Negative feedbacks often produce desirable properties. They can prevent bubbles and crashes. When we eat, our brain receives signals to stop eating. When a company’s profits increase beyond normal economic returns, competitors enter, reducing those profits and preventing the company from exploiting customers. When a species proliferates, its members compete for food, reducing population growth. In each case, negative feedbacks contribute to system-level robustness.

Using systems dynamics models, we can often identify the causes of complexity. When a system includes both positive and negative feedbacks, it can produce complexity. That was true of the Game of Life in which existing cells caused new cells to come to life but overcrowding caused cells to die.





Figure 18.1: The Components of Systems Dynamics Models

Systems dynamics models that represent flows and stock levels as mathematical functions can be calibrated to explain past values of stocks, to predict future values, and to estimate the effects of an intervention. We can then use the models to explain, predict, and guide action. Systems dynamics models can also be qualitative. We can label each arrow with a plus or a minus to clarify logic.2

The remainder of the chapter consists of five parts. To introduce terminology, we build a qualitative model of a bakery. We then construct a predator-prey model based on the Lotka-Volterra equations. Our version assumes interacting populations of foxes and hares and embeds both negative and positive feedbacks. We next show how by using systems dynamics models we can anticipate vicious cycles. We then describe the WORLD3 model, a large model of the global economy. We conclude with a discussion of how systems dynamics models often produce counterintuitive results, which demonstrates the limits of human reasoning and the value of models as logical aids.





The Parts of a Systems Dynamics Model


A systems dynamics model consists of sources, sinks, stocks, and flows. A source produces a stock, the amount or level of some variable. A flow describes how the level of a stock changes. A sink catches the output of a flow from a stock. Sinks and sources are placeholders for processes not included in the model. The level of a stock changes over time based on sources and flows. In a systems dynamics model of an amusement park, for example, the number of people at the park (a stock) increases as people arrive (a source). The rate of increase could in turn depend on other parameters such as the weather, the amount of advertising, or the price of admission.





Figure 18.2: A Systems Dynamics Model of a Bakery

Systems dynamics models use the representational system shown in figure 18.1. Sources and sinks are represented by clouds. Stocks are represented by boxes, and flows by arrows identified by a plus or a minus sign. Variable flows are represented by inverted triangles and constant flows by circles bisected by the flow arrow. A positive arrow represents a positive feedback, where more begets more. A negative arrow represents a negative feedback from one variable to another.

To build familiarity, we first construct a basic systems dynamics model of a bakery that consists of a baker, bread, and customers. The baker makes bread and customers buy it. If the rate at which the baker produces bread exceeds the rate at which customers purchase bread, the stock of bread grows, and the bakery fills with bread. Alternatively, if the rate of sales exceeds the baker’s production rate, the bakery will perpetually sell out. To make the model more realistic, we can allow the baker to adjust the rate of bread production as a function of the stock of the bread as shown in figure 18.3, which includes a flow (an arrow) from the stock of bread to the rate at which the baker produces bread. We place a negative sign on the arrow to denote that the rate decreases as the stock of bread increases. If the adjustment rate is set properly, the model will produce an equilibrium where the rate at which loaves are baked equals the rate at which customers buy bread so that inventories equilibrate.

To make the model even more realistic, we can add a second stock, line, that equals the number of people waiting outside the bakery, as well as a second source, potentials, which adds people to the line. A short to moderate line may attract customers, while a long line could turn customers away. To capture the variable effect of the length of the line on the rate of arrival from the source, we write (+/ −) above the arrow. We also include a plus sign above the arrow from the stock of line to the rate at which customers buy bread, assuming that with more people in line, people decide faster.





Figure 18.3: A More Elaborate Model of the Bakery

This model could be calibrated to data. We could estimate the rates at which people join the line based on its length. The baker could then determine an optimal rate of adjustment for baking as a function of the stock of bread and the length of the line. That rate would provide a starting point from which a better rate might be learned. Even without calibration, the act of writing the model adds value. The baker realizes the importance of line length to his overall sales.





The Predator-Prey Model


We now introduce the predator-prey model, an ecological model that captures the relationship between the number of hares (the prey) and the number of foxes (the predator). The model include two positive feedbacks: hares produce hares, and foxes produce foxes. It also includes a negative feedback: foxes eat hares. The model assumes that if the level of hares is high, foxes produce more offspring. Figure 18.4 qualitatively represents these assumptions but does not quantify the relationships. From the figure we see that as the number of foxes increases, the number of hares decreases, which in turn results in fewer foxes. As the number of foxes falls, hares should proliferate, leading to more foxes. The logic suggests the possibility of a cycle, or perhaps an equilibrium. We cannot be sure.

To gain insight into what occurs, we need to construct a quantitative version of the model. We assume linear flows that depend on the stock levels. Absent any foxes, the number of hares grows at a fixed rate, and absent any hares, the number of foxes decreases at a fixed rate owing to a lack of food. The model will assume that the probability of a hare and a fox meeting is proportional to the number of foxes times the number of hares. To capture foxes eating hares when these interactions occur, we assume that foxes grow at a constant rate times that product and that hares decrease at a constant rate times that product. The resulting equations are known as the Lotka-Volterra equations.





Figure 18.4: A Systems Dynamics Model of the Predator-Prey Model





Lotka-Volterra Model


An ecosystem consist of H hares and F foxes. The population of hares grows at rate g and the population of foxes dies off at rate d. When hares and foxes meet, hares die off at rate a and foxes grow at rate b. These assumptions produce the following differential equations:3





These equations have an extinction equilibrium (F = H = 0), as well as an interior equilibrium given by the equations and .



The differential equations describe how the numbers of hares and foxes change over time. When the equations equal zero, the number of hares and foxes do not change and the system is in an equilibrium. One equilibrium, the extinction equilibrium, consists of no hares or foxes. Therefore, the model predicts that under some conditions, predator-prey relationships lead to the extinction of both species. That cannot occur in all cases; otherwise, no species would be left on earth.

The interior equilibrium contains positive numbers of foxes and hares. In that equilibrium, the number of foxes increases with the growth rate of hares and decreases if each interaction between a fox and a hare reduces the hare population at a faster rate. Both of those results are intuitive. If hares reproduce faster, the systems can support more foxes. And if each fox requires more hares to remain alive, the system can support fewer foxes. Both results align with our intuitions. We want such results: models should produce intuitive findings.

Models should also produce less intuitive findings, and this model does. It shows that the equilibrium number of foxes does not depend at all on the foxes’ rate of death. If foxes die at a faster rate, the equilibrium number of hares increases, and the remaining foxes have abundant food, meaning foxes grow at a faster rate. That faster growth rate of foxes exactly cancels out the foxes’ higher death rate.

Similar logic applies to the hare population. The equilibrium number of hares does not depend on the growth rate of hares or on the rate at which hares are consumed by foxes. The number of hares does depend on the rate at which foxes die and the rate at which foxes turn hares into more foxes. Our intuition fails us in these cases because we cannot think through the feedbacks. The direct effect of increasing the growth rate of hares is more hares. The indirect effect, more foxes, implies fewer hares. These two effects cancel out. Nonintuitive findings such as these are a hallmark of systems dynamics models. Our intuition fails because we latch onto direct effects and fail to think through the entire logical chain. Even if the direct effect of increasing (or decreasing) a rate or flow may be to increase (or decrease) a stock, the presence of systems effects in the form of positive and negative feedbacks means that other stocks will also change values, so the net effect of a change in a rate or flow may be reduced, canceled, or even reversed.

Using mathematics, we could show two equilibria for Lotka-Volterra equations. We do not know which, if either, of those equilibria would be realized. It is true that if the model starts at an equilibrium, then it will stay there. But until we run the model, we do not know if the equations will produce an equilibrium, a cycle, randomness, or complexity. All that we know is that an equilibrium exists.

Simulations of the equations produce lagged cycles. First one species becomes populous, then it reduces in number and the other species increases in number. Empirical studies show these cycles to be common. Figure 18.5 shows the number of wolves (predators) and moose (prey) on Isle Royale, a forty-five-mile-long island in Lake Superior, over a fifty-year period. Notice that species levels of predators and prey fluctuate with lagged cycles. The patterns are not as regular as those produced by the model as we should expect given that the model omits geography, other species, weather variation, and heterogeneity within the two species.





Figure 18.5: Wolves and Moose on Isle Royale, Michigan (isleroyalewolf.org)

This analysis of Lotka-Volterra equations reinforces our earlier observation that we should not conflate the existence of an equilibrium with its attainment. In this case, the system produces cycles and not the equilibrium. However, the dynamics cycle around the equilibrium. Thus, the equilibrium tells us, on average, the number of foxes and hares. It follows that our earlier counterintuitive result—that increasing the growth rate of foxes (or hares) has no effect on the equilibrium level of foxes (or hares)—still holds in the aggregate.





Using Systems Dynamics Models to Guide Action


Systems dynamics models can include both positive and negative feedback loops. Positive feedback loops can result in virtuous cycles, such as when increased trust between two countries leads to more trade, reduced military engagement, and, therefore, more trust. Positive feedback loops can also produce vicious cycles. A reduction in jobs in a region may result in less incentive for people to acquire skills, which may in turn induce firms to leave the region owing to a lack of qualified laborers, producing even less incentive for workers to acquire skills.

Systems dynamics models can help us anticipate vicious cycles. In 2008, many national economies were under severe financial stress. When asset prices fell, over-leveraged banks teetered on the edge of insolvency. Investors and depositors became concerned about the safety of their investments. Some countries, such as the United States, insure bank deposits up to a limit. Other countries, notably Australia, offered no deposit insurance.

To prevent a panic, Australia decided to introduce deposit insurance. The logic seems sound: insuring deposits prevents a run on banks. However, it considers only a part of the system. And in doing so, it suffers from a tragic flaw, which becomes obvious once we write down a systems dynamics model. In a model of a financial system, each bank (a stock) has some level of assets. Depositors put money into the banks and earn a return. The bank’s borrowers use that money to make investments. Deposit insurance guarantees the depositors’ money held in banks.

People also keep money in the stock market and in money market funds. Each type of investment is a stock. Once we start drawing the arrows—the flows between the boxes—the policy’s flaw becomes evident. The direct effect of the deposit insurance increases the safety of banks, making banks more attractive (arrow #1 in figure 18.6). It also makes the other types of investments less attractive. Imagine yourself as investor with money in both banks and money markets during a turbulent time. Your bank deposits are now insured. Your money market funds are not. The prudent action would be to increase bank deposits (arrow #2) and withdraw from money markets (arrow #3).

A vicious cycle ensues: the decrease in investments in money markets makes them riskier. That increased risk produces even more withdrawals from money markets, creating a positive feedback loop (circular path 4). Withdrawals beget increased risk, and risk begets more withdrawals, which in turn begets more risk. The policy appears all but certain to create a collapse of the money market industry, and it did. Within four days of insuring bank deposits, the government froze money market accounts, saving the industry from collapse, a decision with catastrophic consequences. Millions of retirees who relied on withdrawals from those accounts to pay for food, housing, and other essentials could not afford basic necessities.4

Though in retrospect, the vicious cycle seems obvious, we have no guarantee that if Australian policymakers had constructed a systems dynamics model they would have seen the consequences of their policy. However, the process of constructing the model would have revealed the effects of insuring bank deposits within the broader financial system and may have also made the ensuing vicious cycle evident. This example also demonstrates the limits of data. Data from other countries would have shown that insuring deposits stabilizes financial systems. However, in those countries the deposit insurance was not created during a crisis and would have been misleading.





The WORLD3 Model


We next consider a more elaborate systems dynamics model that covers the global economy, known as the WORLD3 model. The model originated in the 1970s and predicted the collapse of the world economy unless governments changed their growth and environmental policies.5 The WORLD3 model includes multiple interacting processes growing at different rates within a common framework, allowing policymakers to see interdependencies.6 Mainstream economists often dismiss the WORLD3 model as too complicated and as failing to take into account rational responses by economic actors.





Figure 18.6: A Systems Dynamics Model of a Financial System

The model assumes that population and economic output grow at fixed percentages each year and that economic output creates pollution. Over time, land becomes less productive, population levels exceed the economy’s ability to produce sufficient goods, and the world economy collapses. This prediction is reminiscent of the dire warnings of Malthus nearly two centuries earlier.

The model contains approximately 150 variables, 300 equations, and 500 parameters, including fertility rates, rates of economic growth, and rate of land use. To calibrate the model, these parameters’ rates of increase must be estimated from data. The WORLD3 model includes interactions among variables, implying that changes in multiple parameters will often produce nonlinear effects. Testing the robustness of the model therefore requires changing pairs and triplets of variables simultaneously. Five hundred parameters create more than 12,000 pairs and over 20 million triplets of parameters—far too many for anyone to analyze.

The model predicts population will fall to 4 billion in 2100. John Miller finds that by tweaking just two parameters, the fraction of industrial output allocated to consumption and the reproductive lifetime of females, nearly doubles the model’s predicted world population to 7.4 billion. The huge increase results from positive feedbacks. Longer reproductive life spans imply more children, who require more food. Increasing the share of output that goes to food allows more children to survive. The women who survive have longer reproductive life spans and more children. The result is massive population growth.7

The finding of a doubling in population from small parameter changes is troublesome. However, the fact that outcomes depend on parameters is not a weakness. To the contrary, the model was built to guide action, to help identify effective policies. For example, the model shows that reducing fertility rates, which in fact did occur, would reduce population growth. Moreover, in that the model was calibrated, it provided an estimate of how much population growth would be reduced. The model could then be included in an ensemble of models to produce more accurate predictions.

Over time the model’s original predictions have become less accurate, in part because rates of population growth have slowed as population has increased. They no longer match the model’s assumptions. This is the sort of adaptive response anticipated by economists.8 While proponents of the WORLD3 model accept this criticism, they hasten to point out that many of the model’s predictions, including those relating to economic growth and total world population, have been quite accurate. As to the reductions in fertility, advocates note that if the WORLD3 model played any part in its own undoing—if the WORLD3 model created an awareness of overpopulation and of the importance of the environment—they are happy to be wrong.





Summary


When constructing a systems dynamics model, we choose the key parts (the stocks), describe the relationships between those parts (the flows), and then simulate the model to discover the implications. These models differ from Markov models in that the rates (which play the role of transition probabilities) adjust. Therefore, the model does not necessarily go to an equilibrium. We have to run the model to see what will happen. In addition, because we do not have to solve for the outcome, we need not worry about the tractability of our assumptions.

Systems dynamics models can have many variables and can include any type of feedbacks between those variables. One can write models without them, but once the boxes defining the stocks have been drawn, a modeler almost cannot help but draw arrows between them. The modeler feels obliged to ask, “What other variables might be affected and how might changes in those variables feed back into the current model?” resulting in more elaborate models.

This flexibility can come at a cost: the more stocks and flows created, the less understandable the model becomes. The art of constructing a useful systems dynamics model lies in including just enough detail to reveal where our intuition fails but not so much detail that we create a morass as confusing as the real world. The most useful systems dynamics reside in that boundary. Those models can reveal unintended effects and contribute to better policy actions. As we just saw, even the best-intended policies, such as the Australian deposit insurance policy, can produce undesirable outcomes.

Systems dynamics models also show how negative feedback loops can limit the effect of interventions. Laws that mandate safety features on cars, such as antilock brakes or airbags, may cause people to drive more recklessly. Widening roads may cause more people to move to the suburbs, thus increasing congestion. Decreasing the nicotine in cigarettes may cause smokers to consume more cigarettes. Developing better treatments for sexually transmitted diseases such as HIV may make people more likely to engage in unsafe sex. The list goes on and on.9 Many of these negative feedbacks seem obvious in retrospect, but anticipating them ahead of time may not be. The act of writing down a qualitative systems dynamics model brings these feedback loops to light and makes us better thinkers.

The fact that systems dynamics models encourage us to include feedbacks is a strength of the approach. In 1696, England’s King William III introduced a homestead tax with a base rate of two shillings per house plus an additional fee based on the number of windows: houses with more than ten windows paid an additional four shillings, and houses with more than twenty paid an additional eight shillings. The king taxed windows because they are observable, can be objectively measured, and correlate with housing values. Had the king relied on assessments of property values, he would have invited favoritism and bribery. His window tax was such a good idea that over the next century, it spread to France, Spain, and Scotland. France did not get rid of its window tax (impôt sur les portes et fenêtres) until 1926.

As model thinkers, we would expect people, who are purposive and adaptive, to respond to the tax. They chose a variety of routes. Some people bricked up the windows on their existing houses. The window tax led architects to alter housing designs. Many middle-class homes built during the period of the tax lack second-story bedroom windows. One row of houses in Edinburgh featured no bedroom windows at all.10 Tax revenues fell. Campbell’s law held again: politicians created a measure and people found a way to skirt it. More elaborate systems dynamics model would include implications of the reduction in windows by adding arrows from the stock variable called windows to attributes such as the health of citizens, which would be reduced from a lack of fresh air and light.

The great value of systems dynamics models resides in part in their ability to help us reason through the effects of our actions. We can often think through the direct effects of policies. Taxing windows will raise revenue. Requiring antilock brakes will save lives. Though we cannot always anticipate every indirect effect—the positive and negative feedbacks, with models we can think more clearly and deeply through the implications of the feedbacks we do identify.




