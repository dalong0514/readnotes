Part I Organizing complexity

We cannot find much insight staring at a mess. We need to organize it. As an everyday example, when I look at my kitchen after a dinner party, I feel overwhelmed. It's late, I'm tired, and I dread that I will not get enough sleep. If I clean up in that scattered state of mind, I pick up a spoon here and a pot there, making little progress. However, when I remember that a large problem can be broken into smaller ones, calm and efficiency return.

I begin at one corner of the kitchen, clear its mess, and move to neighboring areas until the project is done. I divide and conquer (Chapter 1).

Once the dishes are clean, I resist the temptation to dump them into one big box. I separate pots from the silverware and, within the silverware, the forks from the spoons. These groupings, or abstractions (Chapter 2), make the kitchen easy to understand and use.

In problem solving, we organize complexity by using divide-and-conquer reasoning and by making abstractions. In Part I, you'll learn how.

## 0101. Divide and conquer

As imperial rulers knew, you need not conquer all your enemies at once.

Instead, conquer them one at a time. Break hard problems into manageable pieces. This process embodies our first reasoning tool: Divide and conquer!

### 1.1 Warming up

To show how to use divide-and-conquer reasoning, we'll apply it to increasingly complex problems that illustrate its essential features. So we start with an everyday estimate.

What is, roughly, the volume of a dollar bill?

Volumes are hard to estimate. However, we should still make a quick guess.

Even an inaccurate guess will help us practice courage and, when we compare the guess with a more accurate estimate, will help us calibrate our internal measuring rods. To urge me on, I often imagine a mugger who holds a knife at my ribs, demanding,「Your guess or your life!」Then I judge it likely that the volume of a dollar bill lies between 0.1 and 10 cubic centimeters.

This range is wide, spanning a factor of 100. In contrast, the dollar bill's width probably lies between 10 and 20 centimeters — a range of only a factor of 2. The volume range is wider than the width range because we have no equivalent of a ruler for volume; thus, volumes are less familiar than lengths. Fortunately, the volume of the dollar bill is the product of lengths.

volume = width × height × thickness. (1.1)

The harder volume estimate becomes three easier length estimates — the benefit of divide-and-conquer reasoning.

15 cm

The width looks like 6 inches, which is roughly 15 centimeters. The height looks like 2 or 3 inches, which is roughly 6 centimeters.

But before estimating the thickness, let's talk about unit systems.

Is it better to use metric or US customary units (such as inches, feet, and miles)?

Your estimates will be more accurate if you use the units most familiar to you. Raised in the United States, I judge lengths more accurately in inches, feet, and miles than in centimeters, meters, or kilometers. However, for calculations requiring multiplication or division — most calculations — I convert the customary units to metric (and often convert back to customary units at the end). But you may be fortunate enough to think in metric. Then you can estimate and calculate in a single unit system.

The third piece of the divide-and-conquer estimate, the thickness, is difficult to judge. A dollar bill is thin — paper thin.

But how thin is「paper thin」?

This thickness is too small to grasp and judge easily. However, a stack of several hundred bills would be graspable. Not having that much cash lying around, I'll use paper. A ream of paper, which has 500 sheets, is roughly 5 centimeters thick. Thus, one sheet of paper is roughly 0.01 centimeters thick. With this estimate for the thickness, the volume is approximately 1 cubic centimeter:

Although a more accurate calculation could adjust for the fiber composition of a dollar bill compared to ordinary paper and might consider the roughness of the paper, these details obscure the main result: A dollar bill is 1 cubic centimeter pounded paper thin.

To check this estimate, I folded a dollar bill until my finger strength gave out, getting a roughly cubical packet with sides of approximately 1 centimeter — making a volume of approximately 1 cubic centimeter!

In the preceding analysis, you may have noticed the = and ≈ symbols and their slightly different use. Throughout this book, our goal is insight over accuracy. So we'll use several kinds of equality symbols to describe the accuracy of a relation and what it omits. Here is a table of the equality symbols, in descending order of completeness and often increasing order of usefulness.

As examples of the kinds of equality, for the circle below, 𝐴 = 𝜋𝑟2, and 𝐴 ≈ 4𝑟2, and 𝐴 ∼ 𝑟2. For the cylinder, 𝑉 ∼ ℎ𝑟2 — which implies 𝑉 ∝ 𝑟2 and 𝑉 ∝ ℎ. In the 𝑉 ∝ ℎ form, the factor hidden in the ∝ symbol has dimensions of length squared.

Problem 1.1 Weight of a box of books

How heavy is a small moving-box filled with books?

Problem 1.2 Mass of air in your bedroom

Estimate the mass of air in your bedroom.

Problem 1.3 Suitcase of bills

In the movies, and perhaps in reality, cocaine and elections are bought with a suitcase of `$`100 bills. Estimate the dollar value in such a suitcase.

Problem 1.4 Gold or bills?

As a bank robber sitting in the vault planning your getaway, do you fill your suitcase with gold bars or `$`100 bills? Assume first that how much you can carry is a fixed weight. Then redo your analysis assuming that how much you can carry is a fixed volume.

### 1.2 Rails versus roads

We are now warmed up and ready to use divide-and-conquer reasoning for more substantial estimates. Our next estimate, concerning traffic, comes to mind whenever I drive the congested roads to JFK Airport in New York City. The route goes on the Van Wyck Expressway, which was planned by Robert Moses. As Moses's biographer Robert Caro describes [6, pp. 904ff], when Moses was in charge of building the expressway, the traffic planners recommended that, in order to handle the expected large volume of traffic, the road include a train line to the then-new airport. Alternatively, if building the train track would be too expensive, they recommended that the city, when acquiring the land for the road, still take an extra 50 feet of width and reserve it as a median strip for a train line one day. Moses also rejected the cheaper proposal. Alas, only weeks after its opening, not long after World War Two, the rail-free highway had reached peak capacity.

Let's use our divide-and-conquer tool to compare, for rush-hour commut-ing, the carrying capacities of rail and road. The capacity is the rate at which passengers are transported; it is passengers per time. First we'll estimate the capacity of one lane of highway. We can use the 2-second-following rule taught in many driving courses. You are taught to leave 2 seconds of travel time between you and the car in front. When drivers follow this rule, a single lane of highway carries one car every 2 seconds. To find the carrying capacity, we also need the occupancy of each car. Even at rush hour, at least in the United States, each car carries roughly one person. (Taxis often have two people including the driver, but only one person is being transported to the destination.) Thus, the capacity is one person every 2 seconds. As an hourly rate, the capacity is 1800 people per hour: 

The diagonal strike-through lines help us to spot which units cancel and to check that we end up with just the units that we want (people per hour).

This rate, 1800 people per hour, is approximate, because the 2-second following rule is not a law of nature. The average gap might be 4 seconds late at night, 1 second during the day, and may vary from day to day or from highway to highway. But a 2-second gap is a reasonable compromise estimate. Replacing the complex distribution of following times with one time is an application of lumping — the tool discussed in Chapter 6. Organizing complexity almost always reduces detail. If we studied all highways at all times of day, the data, were we so unfortunate as to obtain them, would bury any insight.

How does the capacity of a single lane of highway compare with the capacity of a train line?

For the other half of the comparison, we'll estimate the rush-hour capacity of a train line in an advanced train system, say the French or German system.

As when we estimated the volume of a dollar bill (Section 1.1), we divide the estimate into manageable pieces: how often a train runs on the track, how many cars are in each train, and how many passengers are in each car. Here are my armchair estimates for these quantities, kept slightly conservative to avoid overestimating the train-line's capacity. A single train car, when full at rush hour, may carry 150 people. A rush-hour train may consist of 20 cars.

And, on a busy train route, a train may run every 10 minutes or six times per hour. Therefore, the train line's capacity is 18 000 people per hour: 

This capacity is ten times the capacity of a single fast-flowing highway lane.

And this estimate is probably on the low side; Robert Caro [6, p. 901] gives an estimate of 40 000 to 50 000 people per hour. Using our lower rate, one train track in each direction could replace two highways even if each highway had five lanes in each direction.

### 1.3 Tree representations

Our estimates for the volume of a dollar bill (Section 1.1) and for the rail and highway capacities (Section 1.2) used the same method: dividing hard problems into smaller ones. However, the structure of the analysis is buried within the sentences, paragraphs, and pages. The sequential presentation hides the structure. Because the structure is hierarchical — big problems split, or branch, into smaller problems — its most compact representation is a tree. A tree representation shows us the analysis in one glance.

Here is the tree representation for the capacity capacity

of a train line. Unlike the biological variety, our trees stand on their head. Their roots, the goals, sit at the top of the tree. Their leaves, the small problems into which we have subdivided the

?? people

?? cars

?? trains

car

train

hour

goal, sit at the bottom. The orientation matches the way that we divide and conquer, filling the page downward as we subdivide.

In making this first tree, we haven't estimated capacity

the quantities themselves. We have only identified the quantities. The question marks remind us of our next step: to include estimates for the three leaves. These estimates were 150 people 150 people 20 cars

6 trains

car

train

hour

per car, 20 cars per train, and 6 trains per hour (giving the tree in the margin).

Then we multiplied the leaf values to propagate capacity

18 000 people/hour

the estimates upward from the leaves toward

the root. The result was 18 000 people per hour.

The completed tree shows us the entire estimate in one glance.

150 people

20 cars

6 trains

This train-capacity tree had the simplest possi-car

train

hour

ble structure with only two layers (the root layer and, as the second layer, the three leaves). The next level of complexity is a three-layer tree, which will represent our estimate for the volume of a dollar bill. It started as a two-layer tree with three leaves.

volume

width

height

thickness

Then it grew, because, unlike the width and height, the thickness was difficult to estimate just by looking at a dollar bill. Therefore, we divided that leaf into two easier leaves.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.3 Tree representations 9

The result is the tree in the margin. The thick-volume

ness leaf, which is the thickness per sheet, has split into (1) the thickness per ream and (2) the number of sheets per ream. The boxed

−1 on the line connecting the thickness to the width height

thickness

number of sheets per ream is a new and use-

ful notation. The −1 tells us the exponent to

−1

apply to that leaf value when we propagate it upward to the root.

thickness

?? sheets

ream

ream

Here is why I write the −1 as a full-sized number rather than a small superscript. Most of our estimates require multiplying several factors. The only question for each factor is,「With what exponent does this factor enter?」The number

−1 directly answers this「What exponent?」question. (To avoid cluttering the tree, we don't indicate the most-frequent exponent of 1.) This new subtree then represents the following equation for the thickness of one sheet:

−1

thickness = thickness

ream × (?? sheets

ream ) .

(1.5)

The −1 exponent allows, at the cost of a slight complication in the tree notation, the leaf to represent the number of sheets per ream rather than a less-familiar fraction, the number of reams per sheet.

Now we include our estimates for the leaf values. The width is 15 centimeters. The height is 6 centimeters. The thickness of a ream of paper is 5 centimeters. And a ream contains 500 sheets of paper. The result is the following tree.

volume

width

height

thickness

15 cm

6 cm

−1

5 cm thickness

500 sheets

ream

ream

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

10

1 Divide and conquer

Now we propagate the values to the root.

volume

1 cm3

The two bottommost leaves combine to tell

us that the thickness of one sheet is 10−2

centimeters. This thickness completes the

tree's second layer. In the second layer, the three nodes tell us that the volume of a dol- width height

thickness

15 cm

6 cm

10−2 cm

lar bill — the root — is 1 cubic centimeter.

With practice, you can read in this final tree

−1

all the steps of the analysis. The three nodes in the second layer show how the difficult

5 cm thickness

500 sheets

volume estimate was subdivided into three

ream

ream

easier estimates. That the width and height

remained leaves indicates that these two es-

timates felt reliable enough. In contrast, the two branches sprouting from the thickness indicate that the thickness was still hard to estimate, so we divided that estimate into two more-familiar quantities.

The tree encapsulates many paragraphs of analysis in a compact form, one that our minds can absorb in a single glance. Organizing complexity helps us build insight.

Problem 1.5

Tree for the suitcase of bills

Make a tree diagram for your estimate in Problem 1.3. Do it in three steps: (1) Draw the tree without any leaf estimates, (2) estimate the leaf values, and (3) propagate the leaf values upward to the root.

1.4 Demand-side estimates

Our analysis of the carrying capacity of highways and railways (Section 1.2) is an example of a frequent application of estimation in the social world — estimating the size of a market. The highway–railway comparison proceeded by estimating the transportation supply. In other problems, a more feasi-ble analysis is based on the complementary idea of estimating the demand.

Here is an example.

How much oil does the United States import (in barrels per year)?

The volume rate is enormous and therefore hard to picture. Divide-and-conquer reasoning will tame the complexity. Just keep subdividing until the quantities are no longer daunting.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.4 Demand-side estimates 11

Here, subdivide the demand — the consumption. We consume oil in so many ways; estimating the consumption in each pathway would take a long time without producing much insight. Instead, let's estimate the largest consumption — likely to be cars — then adjust for other uses and for overall consumption versus imports.

all usage

imports

imports = car usage ×

×

.

(1.6)

car usage

all usage

Here is the corresponding tree. The first fac-imports

tor, the most difficult of the three to estimate, will require us to sprout branches and make

a subtree. The second and third factors might be possible to estimate without subdividing.

all usage

imports

car usage

car usage

all usage

Now we must decide how to continue.

Should we keep subdividing until we've built the entire tree and only then estimate the leaves, or should we try to estimate these leaves and then subdivide what we cannot estimate?

It depends on one's own psychology. I feel anxious in the uncharted waters of a new estimate. Sprouting new branches before making any leaf estimates increases my anxiety. The tree might never stop sprouting branches and leaves, and I'll never estimate them all. Thus, I prefer to harvest my progress right away by estimating the leaves before sprouting new branches.

You should experiment to learn your psychology. You are your best problem-solving tool, and it is helpful to know your tools.

Because of my psychology, I'll first estimate a leaf quantity: all usage

car usage.

(1.7)

But don't do this estimate directly. It is more intuitive — that is, easier for our gut — to estimate first the ratio of car usage to other (noncar) usage. The ability to make such comparisons between disjoint sets, at least for physical objects, is hard wired in our brains and independent of the ability to count. Not least, it is not limited to humans. The female lions studied by Karen McComb and her colleagues [35] would judge the relative size of their troop and a group of lions intruding on their territory. The females would approach the intruders only when they outnumbered the intruders by a large-enough ratio, roughly a factor of 2.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

12

1 Divide and conquer

Other uses for oil include noncar modes of transport (trucks, trains, and planes), heating and cooling, and hydrocarbon-rich products such as fer-tilizer, plastics, and pesticides. In judging the relative importance of other uses compared to car usage, two arguments compete: (1) Other uses are so many and so significant, so they are much more important than car usage; and (2) cars are so ubiquitous and such an inefficient mode of transport, so car usage is much larger than other uses. To my gut, both arguments feel comparably plausible. My gut is telling me that the two categories have comparable usages:

other usage

car usage ≈ 1.

(1.8)

Based on this estimate, all usage (the sum of car and other usage) is roughly double the car usage:

all usage

car usage ≈ 2.

(1.9)

This estimate is the first leaf. It implicitly assumes that the gasoline fraction in a barrel of oil is high enough to feed the cars. Fortunately, if this assumption were wrong, we would get warning. For if the fraction were too low, we would build our transportation infrastructure around other means of transport — such as trains powered by electricity generated by burning the nongasoline fraction in oil barrels. In this probably less-polluted world, we would estimate how much oil was used by trains.

Returning to our actual world, let's estimate the second leaf: imports

all usage.

(1.10)

This adjustment factor accounts for the fact that only a portion of the oil consumed is imported.

What does your gut tell you for this fraction?

Again, don't estimate this fraction directly. Instead, to make a comparison between disjoint sets, first compare (net) imports with domestic production.

In estimating this ratio, two arguments compete. On the one hand, the US media report extensively on oil production in other countries, which suggests that oil imports are large. On the other hand, there is also extensive coverage of US production and frequent comparison with countries such as Japan that have almost no domestic oil. My resulting gut feeling is that the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.4 Demand-side estimates 13

categories are comparable and therefore that imports are roughly one-half of all usage:

imports

imports

domestic production ≈ 1

so

all usage ≈ 12.

(1.11)

This leaf, as well as the other adjustment factor, are dimensionless numbers.

Such numbers, the main topic of Chapter 5, have special value. Our percep-tual system is skilled at estimating dimensionless ratios. Therefore, a leaf node that is a dimensionless ratio probably does not need to be subdivided.

The tree now has three leaves. Having plausi-imports

ble estimates for two of them should give us courage to subdivide the remaining leaf, the total car usage, into easier estimates. That leaf will sprout its own branches and become an

all usage

imports

car usage

internal node.

car usage

all usage

2

0.5

How should we subdivide the car usage?

A reasonable subdivision is into the number of cars 𝑁cars and car usage

the per-car usage. Both quantities are easier to estimate than the root. The number of cars is related to the US population — a familiar number if you live in the United States. The per-car usage is easier to estimate than is the total usage of all US

Ncars

usage/car

cars. Our gut can more accurately judge human-scale quantities, such as the per-car usage, than it can judge vast numbers like the total usage of all US cars.

For the same reason, let's not estimate the number of cars Ncars

3 × 108

directly. Instead, subdivide this leaf into two leaves: 1. the number of people, and

2. the number of cars per person.

Npeople

cars/person

The first leaf is familiar, at least to residents of the United 3 × 108

1

States: 𝑁people ≈ 3×108.

The second leaf, cars per person, is a human-sized quantity.

In the United States, car ownership is widespread. Many adults own more than one car, and a cynic would say that even babies seem to own cars.

Therefore, a rough and simple estimate might be one car per person — far easier to picture than the total number of cars! Then 𝑁cars ≈ 3×108.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

14

1 Divide and conquer

The per-car usage can be subdivided into three usage/car

easier factors (leaves). Here are my estimates.

1. How many miles per car year? Used cars with

−

−

1

1

10 000 miles per year are considered low use

?? miles

?? miles

?? gallons

but are not rare. Thus, for a typical year of car year

gallon

barrel

driving, let's take a slightly longer distance: say, 20 000 miles or 30 000 kilometers.

2. How many miles per gallon? A typical car fuel efficiency is 30 miles per US gallon. In metric units, it is about 100 kilometers per 8 liters.

3. How many gallons per barrel? You might have seen barrels of asphalt along the side of the highway during road construction. Following our free-association tradition of equating the thickness of a sheet of paper and of a dollar bill, perhaps barrels of oil are like barrels of asphalt.

Their volume can be computed by divide-and-conquer reasoning. Just approximate the cylinder as a rectangular prism, estimate its three dimensions, and multiply: volume ∼ 1 m

⏟ × 0.5 m

⏟ × 0.5 m

⏟ = 0.25 m3.

(1.12)

height

width

depth

A cubic meter is 1000 liters or, using the conversion of 4 US gallons per liter, roughly 250 gallons. Therefore, 0.5 m

0.25 cubic meters is roughly 60 gallons. (The official volume of a barrel of oil is not too different at 42 gallons.) Multiplying these estimates, and not forgetting the effect of the two −1 exponents, we get approximately 10 barrels per car per year (also written as barrels per car year):

2×104 miles

1 gallon

1 barrel

10 barrels

×

×

≈

.

(1.13)

car year

30 miles 60 gallons

car year

In doing this calculation, first evaluate the units. The gallons and miles cancel, leaving barrels per year. Then evaluate the numbers. The 30 × 60 in the denominator is roughly 2000. The 2 × 104 from the numerator divided by the 2000 from the denominator produces the 10.

This estimate is a subtree in the tree representing total car usage. The car usage then becomes 3 billion barrels per year: 3×108 cars × 10 barrels = 3×109 barrels.

(1.14)

car year

year

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.4 Demand-side estimates 15

This estimate is itself a subtree in the tree imports

3 × 109 barrels

representing oil imports. Because the two

year

adjustment factors contribute a factor of

2 × 0.5, which is just 1, the oil imports are also 3 billion barrels per year.

Here is the full tree, which includes the

car usage

all usage

imports

subtree for the total car usage of oil:

3 × 109 barrels

car usage

all usage

year

2

0.5

imports

3 × 109 barrels

year

car usage

all usage

imports

3 × 109 barrels

car usage

all usage

year

2

0.5

usage/car

Ncars

10 barrels

3 × 108

car year

−1

−1

N

1 car

20 000 miles

30 miles

60 gallons

people

3 × 108

person

car year

gallon

barrel

height

width

depth

250 gallons

1 m

0.5 m

0.5 m

m3

Problem 1.6

Using metric units

As practice with metric units (if you grew up in a nonmetric land) or to make the results more familiar (if you grew up in a metric land), redo the calculation using the metric values for the volume of a barrel, the distance a car is driven per year, and the fuel consumption of a typical car.

How close is our estimate to official values?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

16

1 Divide and conquer

For the US oil imports, the US Department of Energy reports 9.163 million barrels per day (for 2010). When I first saw this value, my heart sank twice.

The first shock was the 9 in the 9 million. I assumed that it was the number of billions, and wondered how the estimate of 3 billion barrels could be a factor of 3 too small. The second shock was the「million」 — how could the estimate be more than a factor of 100 too large? Then the「per day」

reassured me. As a yearly rate, 9.163 million barrels per day is 3.34 billion barrels per year — only 10 percent higher than our estimate. Divide and conquer triumphs!

Problem 1.7

Fuel efficiency of a 747

Based on the cost of a long-distance plane ticket, estimate the following quantities: (a) the fuel efficiency of a 747, in passenger miles per gallon or passenger kilometers per liter; and (b) the volume of its fuel tank. Check your estimates against the technical data for a 747.

1.5 Multiple estimates for the same quantity After making an estimate, it is natural to wonder about how much confidence to place in it. Perhaps we made an embarrassingly large mistake. The best way to know is to estimate the same quantity using another method.

As an everyday example, let's observe how we add a list of numbers.

12

15

+18

(1.15)

We often add the numbers first from top to bottom. For 12 + 15 + 18, we calculate,「12 plus 15 is 27; 27 plus 18 is 45.」To check the result, we add the numbers in the reverse order, from bottom to top:「18 plus 15 is 33; 33 plus 12 is 45.」The two totals agree, so each is probably correct: The calculations are unlikely to contain an error of exactly the same amount. This kind of redundancy catches errors.

In contrast, mindless redundancy offers little protection. If we check the calculation by adding the numbers from top to bottom again, we usually repeat any mistakes. Similarly, rereading written drafts usually means overlooking the same spelling, grammar, or logic faults. Instead, stuff the draft in a drawer for a week, then look at it; or ask a colleague or friend — in both cases, use fresh eyes.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.6 Talking to your gut

17

Reliability, in short, comes from intelligent redundancy.

This principle helps you make reliable estimates. First, use several methods to estimate the same quantity. Second, make the methods as different from one another as possible — for example, by using unrelated background knowledge. This approach to reliability is another example of divide-and-conquer reasoning: The hard problem of making a reliable estimate becomes several simpler subproblems, one per estimation method.

You saw an example in Section 1.1, where we estimated the volume of a dollar bill. The first method used divide-and-conquer reasoning based on the width, height, and thickness of the bill. The check was a comparison with a folded-up dollar bill. Both methods agreed on a volume of approximately 1 cubic centimeter — giving us confidence in the estimate.

For another example of using multiple methods, return to the estimate of the volume of an oil barrel (Section 1.4). We used a roadside asphalt barrel as a proxy for an oil barrel and estimated the volume of the roadside barrel. The result, 60 gallons, seemed plausible, but maybe oil barrels have a completely different size. One way to catch that kind of error is to use a different method for estimating the volume. For example, we might start with the cost of a barrel of oil — about `$`100 in 2013 — and the cost of a gallon of gasoline — about `$`2.50 before taxes, or 1/40th of the cost of a barrel. If the markup on gasoline is not significant, then a barrel is roughly 40 gallons. Even with a markup, we can still say that a barrel is at least 40 gallons.

Because our two estimates, 60 gallons and > 40 gallons, roughly agree, our confidence in both increases. If they had contradicted each other, one or both would be wrong, and we would look for the mistaken assumption, for the incorrect arithmetic, or for a third method.

1.6 Talking to your gut

As you have seen in the preceding examples, divide-and-con-US population

quer estimates require reasonable estimates for the leaf quantities. To decide what is reasonable, you have to talk to your gut — what you will learn in this section. Talking to your gut feels strange at first, especially because science and engineer-population

area

density

ing are considered cerebral subjects. Let's therefore discuss how to hold the conversation. The example will be an estimate of the US population based on its area and population density. The 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

18

1 Divide and conquer

divide-and-conquer tree has two leaves. (In Section 6.3.1, you'll see a qualitatively different method, where the two leaves will be the number of US

states and the population of a typical state.) The area is the width times the height, so the area leaf US population

itself splits into two leaves. Estimating the width and height requires only a short dialogue with the gut, at least if you live in the United States. Its width is a 6-hour plane flight at 500 miles per hour, so about 3000 miles; population

area

density

and the height is, as a rough estimate, two-thirds of the width, or 2000 miles. Therefore, the area is 6 million square miles:

3000 miles × 2000 miles = 6×106 miles2.

(1.16)

width

height

In metric units, it is about 16 million square kilometers.

Estimating the population density requires talking to your gut. If you are like me you have little conscious knowledge of the population density. Your gut might know, but you cannot ask it directly. The gut is connected to the right brain, which doesn't have language. Although the right brain knows a lot about the world, it cannot answer with a value, only with a feeling.

To draw on its knowledge, ask it indirectly. Pick a particular population density — say, 100 people per square mile — and ask the gut for its opinion:

「O, my intuitive, insightful, introverted right brain: What do you think of 100 people per square mile for the population density?」A response, a gut feeling, will come back. Keep lowering the candidate value until the gut feeling becomes,「No, that value feels way too low.」

Here is the dialogue between my left brain (LB) and right brain (RB).

LB: What do you think of 100 people per square mile?

RB: That feels okay based on my experience growing up in the United States.

LB: I can probably support that feeling quantitatively. A square mile with 100

people means each person occupies a square whose side is 1/10th of a mile or 160 meters. Expressed in this form, does the population density feel okay?

RB: Yes, the large open spaces in the western states probably compensate for the denser regions near the coasts.

LB: Now I will lower the estimate by factors of 3 or 10 until you object strongly that the estimate feels too low. [A factor of 3 is roughly one-half of a factor of 10, because 3 × 3 ≈ 10. A factor of 3 is the next-smallest factor by which to move when a factor of 10 is too large a jump.] In that vein, what about an average population density of 10 people per square mile?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.6 Talking to your gut

19

RB: I feel uneasy. The estimate feels a bit low.

LB: I understand where you are coming from. That value may moderately overestimate the population density of farmland, but it probably greatly underestimates the population density in the cities. Because you are uneasy, let's move more slowly until you object strongly. How about 3 people per square mile?

RB: If the true value were lower than that, I'd feel fairly surprised.

LB: So, for the low end, I'll stop at 3 people per square mile. Now let's navigate to the upper end. You said that 100 people per square mile felt plausible. How do you feel about 300 people per square mile?

RB: I feel quite uneasy. That estimate feels quite high.

LB: I hear you. Your response reminds me that New Jersey and the Netherlands, both very densely populated, are at 1000 people per square mile, although I couldn't swear to this value. I cannot imagine packing the whole United States to a density comparable to New Jersey's. Therefore, let's stop here: Our upper endpoint is 300 people per square mile.

How do you make your best guess based on these two endpoints?

A plausible guess is to use their arithmetic mean, which is roughly 150 people per square mile. However, the right method is the geometric mean: best guess = lower endpoint × upper endpoint.

(1.17)

The geometric mean is the midpoint of the lower and upper bounds — but on a ratio or logarithmic scale, which is the scale built into our mental hardware. (For more about how we perceive quantity, see The Number Sense

[9].) The geometric mean is the correct mean when combining quantities produced by our mental hardware.

Here, the geometric mean is 30 people per square mile: a factor of 10 removed from either endpoint. Using that population density, US population ∼ 6×106 miles2 × 30

miles2 ≈ 2 × 108.

(1.18)

The actual population is roughly 3×108. The estimate based almost entirely on gut reasoning is within a factor of 1.5 of the actual population — a pleasantly surprising accuracy.

Problem 1.8

More gut estimates

By asking your gut to help you estimate the lower and upper endpoints, estimate (a) the height of a nearby tall tree that you can see, (b) the mass of a car, and (c) the number of water drops in a bathtub.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

20

1 Divide and conquer

1.7 Physical estimates

Your gut understands not only the social world but also the physical world.

If you trust its feelings, you can tap this vast reservoir of knowledge. For practice, we'll estimate the salinity of seawater (Section 1.7.1), human power output (Section 1.7.2), and the heat of vaporization of water (Section 1.7.3).

1.7.1 Salinity of seawater

To estimate the salinity of seawater, which will later help you estimate the conductivity of seawater (Problem 8.10), do not ask your gut directly:「How do you feel about, say, 200 millimolar?」Although that kind of question worked for estimating population density (Section 1.6), here, unless you are a chemist, the answer will be:「I have no clue. What is a millimolar anyway? I have almost no experience of that unit.」Instead, offer your gut concrete data — for example, from a home experiment: adding salt to a cup of water until the mixture tastes as salty as the ocean.

This experiment can be a thought or a real experiment — another example of using multiple methods (Section 1.5). As a thought experiment, I ask my gut about various amounts of salt in a cup of water. When I propose adding 2 teaspoons, it responds,「Disgustingly salty!」At the lower end, when I propose adding 0.5 teaspoons, it responds,「Not very salty.」I'll use 0.5 and 2 teaspoons as the lower and upper endpoints of the range. Their midpoint, the estimate from the thought experiment, is 1 teaspoon per cup.

I tested this prediction at the kitchen sink. With 1 teaspoon (5 milliliters) of salt, the cup of water indeed had the sharp, metallic taste of seawater that I have gulped after being knocked over by large waves. A cup of water is roughly one-fourth of a liter or 250 cubic centimeters. By mass, the resulting salt concentration is the following product: 1 tsp salt

1 cup water 5 cm3 salt

2 g salt

×

×

×

(1.19)

1 cup water

250 g water

1 tsp salt

1 cm3 salt.

⏟⏟⏟⏟⏟⏟⏟

𝜌salt

The density of 2 grams per cubic centimeter comes from my gut feeling that salt is a light rock, so it should be somewhat denser than water at 1 gram per cubic centimeter, but not too much denser. (For an alternative method, more accurate but more elaborate, try Problem 1.10.) Then doing the arithmetic gives a 4 percent salt-to-water ratio (by mass).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.7 Physical estimates

21

The actual salinity of the Earth's oceans is about 3.5 percent — very close to the estimate of 4 percent. The estimate is close despite the large number of assumptions and approximations — the errors have mostly canceled. Its accuracy should give you courage to perform home experiments whenever you need data for divide-and-conquer estimates.

Problem 1.9

Density of water

Estimate the density of water by asking your gut to estimate the mass of water in a cup measure (roughly one-quarter of a liter).

Problem 1.10

Density of salt

Estimate the density of salt using the volume and mass of a typical salt container that you find in a grocery store. This value should be more accurate than my gut estimate in Section 1.7.1 (which was 2 grams per cubic centimeter).

1.7.2 Human power output

Our second example of talking to your gut is an estimate of hu-power

man power output — a power that is useful in many estimates (for example, Problem 1.17). Energies and powers are good can-

−1

didates for divide-and-conquer estimates, because they are connected by the subdivision shown in the following equation and energy time

represented in the tree in the margin:

energy

power = time .

(1.20)

In particular, let's estimate the power that a trained athlete can generate for an extended time (not just during a few-seconds-long, high-power burst).

As a proxy for that power, I'll use my own burst power output with two adjustment factors:

athlete's steady power

my steady power

athlete's steady power

my burst power

my burst power

my steady power

Maintaining a power is harder than producing a quick burst. Therefore, the first adjustment factor, my steady power divided by my burst power, is somewhat smaller than 1 — maybe 1/2 or 1/3. In contrast, an athlete's 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

22

1 Divide and conquer

power output will be higher than mine, perhaps by a factor of 2 or 3: Even though I am sometimes known as the street-fighting mathematician [33], I am no athlete. Then the two adjustment factors roughly cancel, so my burst power should be comparable to an athlete's steady power.

To estimate my burst power, I performed a home experiment power

of running up a flight of stairs as quickly as possible. Determining the power output requires estimating an energy and

−1

a time:

energy

energy

time

power = time .

(1.21)

The energy, which is the change in my gravitational potential energy, itself subdivides into three factors: m

g

h

energy = mass

⏟ × gravity

⏟⏟⏟⏟⏟ × height.

⏟

(1.22)

𝑚

𝑔

ℎ

In the academic building at my university, a building with high ceilings and staircases, I bounded up a staircase three stairs at a 3.5 m

time. The staircase was about 12 feet or 3.5 meters high. Therefore, my mechanical energy output was roughly 2000 joules: 𝐸 ∼ 65 kg × 10 m s−2 × 3.5 m ∼ 2000 J.

(1.23)

(The units are fine: 1 J = 1 kg m2 s−2.)

The remaining leaf is the time: how long the climb took me. I made it in 6 seconds. In contrast, several students made it in 3.9 seconds — the power of youth! My mechanical power output was about 2000 joules per 6 seconds, or about 300 watts. (To check whether the estimate is reasonable, try Problem 1.12, where you estimate the typical human basal metabolism.) This burst power output should be close to the sustained power output of a trained athlete. And it is. As an example, in the Alpe d'Huez climb in the 1989 Tour de France, the winner — Greg LeMond, a world-class athlete — put out 394 watts (over a 42.5-minute period). The cyclist Lance Armstrong, during the time-trial stage during the Tour de France in 2004, generated even more: 495 watts (roughly 7 watts per kilogram). However, he publicly admitted to blood doping to enhance performance. Indeed, because of widespread doping, many cycling power outputs of the 1990s and 2000s are suspect; 400 watts stands as a legitimate world-class sustained power output.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.7 Physical estimates

23

Problem 1.11

Energy in a 9-volt battery

Estimate the energy in a 9-volt battery. Is it enough to launch the battery into orbit?

Problem 1.12

Basal metabolism

Based on our daily caloric consumption, estimate the human basal metabolism.

Problem 1.13

Energy measured in person flights of stairs How many flights of stairs can you climb using the energy in a stick (100 grams) of butter?

1.7.3 Heat of vaporization of water

Our final physical estimate concerns the most important liquid on Earth.

What is the heat of vaporization of water?

Because water covers so much of the Earth and is such an important part of the atmosphere (clouds!), its heat of vaporization strongly affects our climate — whether through rainfall (Section 3.4.3) or air temperatures.

Heat of vaporization is defined as a ratio:

heat of

vaporization

energy to evaporate a substance

amount of the substance

,

(1.24)

−1

where the amount of substance can be measured in moles, by volume, or (most commonly) by mass. energy to evaporate mass of the

The definition provides the structure of the tree a substance

substance

and of the estimate based on divide-and-conquer reasoning.

For the mass of the substance, choose an amount of water that is easy to imagine — ideally, an amount familiar from everyday life. Then your gut can help you make estimates. Because I often boil a few cups of water at a time, and each cup is few hundred milliliters, I'll imagine 1 liter or 1 kilogram of water.

The other leaf, the required energy, requires more thought. There is a common confusion about this energy that is worth discussing.

Is it the energy required to bring the water to a boil?

No: The energy has nothing to do with the energy required to bring the water to a boil! That energy is related to water's specific heat 𝑐p. The heat of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

24

1 Divide and conquer

vaporization depends on the energy needed to evaporate — boil away — the water, once it is boiling. (You compare these energies in Problem 5.61.) Energy subdivides into power times time (as when we es-heat of

vaporization

timated human power output in Section 1.7.2). Here, the power could be the power output of one burner; the time is the time to boil away the liter of water. To estimate these

−1

leaves, let's hold a gut conference.

energy

mass

For the time, my dialogue is as follows.

LB: How does 1 minute sound as a lower bound?

RB: Way too short — you've left boiling water on the stove unattended for longer without its boiling away!

burner

evaporation

power

time

LB: How about 3 minutes?

RB: That's on the low side. Maybe that's the lower bound.

LB: Okay. For the upper bound, how about 100 minutes?

RB: That time feels way too long. Haven't we boiled away pots of water in far less time?

LB: What about 30 minutes?

RB: That's long, but I wouldn't be shocked, only fairly surprised, if it took that long. It feels like the upper bound.

My range is therefore 3…30 minutes. Its midpoint — the geometric mean of the endpoints — is about 10 minutes or 600 seconds.

For variety, let's directly estimate the burner power, without estimating lower and upper bounds.

LB: How does 100 watts feel?

RB: Way too low: That's a lightbulb! If a lightbulb could boil away water so quickly, our energy troubles would be solved.

LB (feeling chastened): How about 1000 watts (1 kilowatt)?

RB: That's a bit low. A small appliance, such as a clothes iron, is already 1 kilowatt.

LB (raising the guess more slowly): What about 3 kilowatts?

RB: That burner power feels plausible.

Let's check this power estimate by subdividing power into two factors, voltage and current:

power = voltage × current.

(1.25)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.8 Summary and further problems 25

An electric stove requires a line voltage of 220 volts, even in the United States where most other appliances require only 110 volts. A standard fuse is about 15 amperes, which gives us an idea of a large current. If a burner corresponds to a standard fuse, a burner supplies roughly 3 kilowatts: 220 V × 15 A ≈ 3000 W.

(1.26)

This estimate agrees with the gut estimate, so both methods gain plausibility — which should give you confidence to use both methods for your own estimates. As a check, I looked at the circuit breaker connected to my range, and it is rated for 50 amperes. The range has four burners and an oven, so 15 amperes for one burner (at least, for the large burner) is plausible.

We now have values for all the leaf nodes. Prop-heat of vaporization

2 × 106 J

agating the values toward the root gives the heat kg

of vaporization (𝐿vap) as roughly 2 megajoules per kilogram:

power

time

−1

𝐿

3 kW

⏞ × 600s

⏞

vap ∼

energy

mass

1 kg

⏟

(1.27)

2 × 106 J

1 kg

mass

≈ 2×106 J kg−1.

The true value is about 2.2×106 joules per kilogram.

This value is one of the highest heats of vaporiza- burner power evaporation time

3 kW

10 min

tion of any liquid. As water evaporates, it carries away significant amounts of energy, making it an excellent coolant (Problem 1.17).

1.8 Summary and further problems

The main lesson that you should take away is courage: No problem is too difficult. We just use divide-and-conquer reasoning to dissolve difficult problems into smaller pieces. (For extensive practice, see the varied examples in the Guesstimation books [47 and 48].) This tool is a universal solvent for problems social and scientific.

Problem 1.14

Per-capita land area

Estimate the land area per person for the world, for your home country, and for your home state or province.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

26

1 Divide and conquer

Problem 1.15

Mass of the Earth

Estimate the mass of the Earth. Then look it up (p. xvii) to check your estimate.

Problem 1.16

Billion

How long would it take to count to a billion (109)?

Problem 1.17

Sweating

Estimate how much water you need to drink to replace water lost to evaporation, if you ride a bicycle vigorously for 1 hour. Represent your estimate as a divide-and-conquer tree. Hint: Humans are only about 25 percent efficient in generating mechanical work.

Problem 1.18

Pencil line

How long a line can you write with a pencil?

Problem 1.19

Pine needles

Estimate the number of needles on a pine tree.

Problem 1.20

Hairs

How many hairs are on your head?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae