## Part I Organizing complexity

We cannot find much insight staring at a mess. We need to organize it. As an everyday example, when I look at my kitchen after a dinner party, I feel overwhelmed. It's late, I'm tired, and I dread that I will not get enough sleep. If I clean up in that scattered state of mind, I pick up a spoon here and a pot there, making little progress. However, when I remember that a large problem can be broken into smaller ones, calm and efficiency return.

I begin at one corner of the kitchen, clear its mess, and move to neighboring areas until the project is done. I divide and conquer (Chapter 1).

Once the dishes are clean, I resist the temptation to dump them into one big box. I separate pots from the silverware and, within the silverware, the forks from the spoons. These groupings, or abstractions (Chapter 2), make the kitchen easy to understand and use.

In problem solving, we organize complexity by using divide-and-conquer reasoning and by making abstractions. In Part I, you'll learn how.

to master complexity

organize it

discard it

Part I

Parts II, III

divide and

without losing information

losing information

conquer

abstraction

Part II

Part III



2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1Divide and conquer

1.1 Warming up

3

1.2 Rails versus roads

6

1.3 Tree representations

7

1.4 Demand-side estimates

10

1.5 Multiple estimates for the same quantity 16

1.6 Talking to your gut

17

1.7 Physical estimates

20

1.8 Summary and further problems

25

As imperial rulers knew, you need not conquer all your enemies at once.

Instead, conquer them one at a time. Break hard problems into manageable pieces. This process embodies our first reasoning tool: Divide and conquer!

1.1 Warming up

To show how to use divide-and-conquer reasoning, we'll apply it to increasingly complex problems that illustrate its essential features. So we start with an everyday estimate.

What is, roughly, the volume of a dollar bill?

Volumes are hard to estimate. However, we should still make a quick guess.

Even an inaccurate guess will help us practice courage and, when we compare the guess with a more accurate estimate, will help us calibrate our internal measuring rods. To urge me on, I often imagine a mugger who holds a knife at my ribs, demanding,「Your guess or your life!」Then I judge it likely that the volume of a dollar bill lies between 0.1 and 10 cubic centimeters.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4

1 Divide and conquer

This range is wide, spanning a factor of 100. In contrast, the dollar bill's width probably lies between 10 and 20 centimeters—a range of only a factor of 2. The volume range is wider than the width range because we have no equivalent of a ruler for volume; thus, volumes are less familiar than lengths. Fortunately, the volume of the dollar bill is the product of lengths.

volume = width × height × thickness.

(1.1)

6 cm

`$`1 bill

The harder volume estimate becomes three easier length estimates—the benefit of divide-and-conquer reasoning.

15 cm

The width looks like 6 inches, which is roughly 15 centimeters. The height looks like 2 or 3 inches, which is roughly 6 centimeters.

But before estimating the thickness, let's talk about unit systems.

Is it better to use metric or US customary units (such as inches, feet, and miles)?

Your estimates will be more accurate if you use the units most familiar to you. Raised in the United States, I judge lengths more accurately in inches, feet, and miles than in centimeters, meters, or kilometers. However, for calculations requiring multiplication or division—most calculations—I convert the customary units to metric (and often convert back to customary units at the end). But you may be fortunate enough to think in metric. Then you can estimate and calculate in a single unit system.

The third piece of the divide-and-conquer estimate, the thickness, is difficult to judge. A dollar bill is thin—paper thin.

But how thin is「paper thin」?

This thickness is too small to grasp and judge easily. However, a stack of several hundred bills would be graspable. Not having that much cash lying around, I'll use paper. A ream of paper, which has 500 sheets, is roughly 5 centimeters thick. Thus, one sheet of paper is roughly 0.01 centimeters thick. With this estimate for the thickness, the volume is approximately 1 cubic centimeter:

volume ≈ 15 cm

⏟ × 6 cm

⏟ × 0.01

⏟⏟ cm

⏟⏟⏟ ≈ 1 cm3.

(1.2)

width

height

thickness

Although a more accurate calculation could adjust for the fiber composition of a dollar bill compared to ordinary paper and might consider the roughness of the paper, these details obscure the main result: A dollar bill is 1 cubic centimeter pounded paper thin.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.1 Warming up

5

To check this estimate, I folded a dollar bill until my finger strength gave out, getting a roughly cubical packet with sides of approximately 1 centimeter—making a volume of approximately 1 cubic centimeter!

In the preceding analysis, you may have noticed the = and ≈ symbols and their slightly different use. Throughout this book, our goal is insight over accuracy. So we'll use several kinds of equality symbols to describe the accuracy of a relation and what it omits. Here is a table of the equality symbols, in descending order of completeness and often increasing order of usefulness.

≡

equality by definition

read as「is defined to be」

=

equality

「is equal to」

≈

equality except perhaps for a purely

「is approximately equal to」

numerical factor near 1

∼

equality except perhaps for a purely

「is roughly equal to」or

numerical factor

「is comparable to」

∝

equality except perhaps for a factor

「is proportional to」

that may have dimensions

As examples of the kinds of equality, for the circle below, 𝐴 = 𝜋𝑟2, and 𝐴 ≈ 4𝑟2, and 𝐴 ∼ 𝑟2. For the cylinder, 𝑉 ∼ ℎ𝑟2—which implies 𝑉 ∝ 𝑟2

and 𝑉 ∝ ℎ. In the 𝑉 ∝ ℎ form, the factor hidden in the ∝ symbol has dimensions of length squared.

area A

r

⎧ = 𝜋𝑟2

𝐴 {⎨

𝑉 ∝ { 𝑟2

{ ≈ 4𝑟2

⎩ ∼ 𝑟2

ℎ

Problem 1.1

Weight of a box of books

How heavy is a small moving-box filled with books?

Problem 1.2

Mass of air in your bedroom

Estimate the mass of air in your bedroom.

Problem 1.3

Suitcase of bills

In the movies, and perhaps in reality, cocaine and elections are bought with a suitcase of `$`100 bills. Estimate the dollar value in such a suitcase.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

6

1 Divide and conquer

Problem 1.4

Gold or bills?

As a bank robber sitting in the vault planning your getaway, do you fill your suitcase with gold bars or `$`100 bills? Assume first that how much you can carry is a fixed weight. Then redo your analysis assuming that how much you can carry is a fixed volume.

1.2 Rails versus roads

We are now warmed up and ready to use divide-and-conquer reasoning for more substantial estimates. Our next estimate, concerning traffic, comes to mind whenever I drive the congested roads to JFK Airport in New York City. The route goes on the Van Wyck Expressway, which was planned by Robert Moses. As Moses's biographer Robert Caro describes [6, pp. 904ff], when Moses was in charge of building the expressway, the traffic planners recommended that, in order to handle the expected large volume of traffic, the road include a train line to the then-new airport. Alternatively, if building the train track would be too expensive, they recommended that the city, when acquiring the land for the road, still take an extra 50 feet of width and reserve it as a median strip for a train line one day. Moses also rejected the cheaper proposal. Alas, only weeks after its opening, not long after World War Two, the rail-free highway had reached peak capacity.

Let's use our divide-and-conquer tool to compare, for rush-hour commut-ing, the carrying capacities of rail and road. The capacity is the rate at which passengers are transported; it is passengers per time. First we'll estimate the capacity of one lane of highway. We can use the 2-second-following rule taught in many driving courses. You are taught to leave 2 seconds of travel time between you and the car in front. When drivers follow this rule, a single lane of highway carries one car every 2 seconds. To find the carrying capacity, we also need the occupancy of each car. Even at rush hour, at least in the United States, each car carries roughly one person. (Taxis often have two people including the driver, but only one person is being transported to the destination.) Thus, the capacity is one person every 2 seconds. As an hourly rate, the capacity is 1800 people per hour: 1 person 3600 s

1800 people

×

=

.

(1.3)

2 s

1 hr

hr

The diagonal strike-through lines help us to spot which units cancel and to check that we end up with just the units that we want (people per hour).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.3 Tree representations 7

This rate, 1800 people per hour, is approximate, because the 2-second following rule is not a law of nature. The average gap might be 4 seconds late at night, 1 second during the day, and may vary from day to day or from highway to highway. But a 2-second gap is a reasonable compromise estimate. Replacing the complex distribution of following times with one time is an application of lumping—the tool discussed in Chapter 6. Organizing complexity almost always reduces detail. If we studied all highways at all times of day, the data, were we so unfortunate as to obtain them, would bury any insight.

How does the capacity of a single lane of highway compare with the capacity of a train line?

For the other half of the comparison, we'll estimate the rush-hour capacity of a train line in an advanced train system, say the French or German system.

As when we estimated the volume of a dollar bill (Section 1.1), we divide the estimate into manageable pieces: how often a train runs on the track, how many cars are in each train, and how many passengers are in each car. Here are my armchair estimates for these quantities, kept slightly conservative to avoid overestimating the train-line's capacity. A single train car, when full at rush hour, may carry 150 people. A rush-hour train may consist of 20 cars.

And, on a busy train route, a train may run every 10 minutes or six times per hour. Therefore, the train line's capacity is 18 000 people per hour: 150 people 20 cars 6 trains

18 000 people

×

×

=

.

(1.4)

car

train

hr

hr

This capacity is ten times the capacity of a single fast-flowing highway lane.

And this estimate is probably on the low side; Robert Caro [6, p. 901] gives an estimate of 40 000 to 50 000 people per hour. Using our lower rate, one train track in each direction could replace two highways even if each highway had five lanes in each direction.

1.3 Tree representations

Our estimates for the volume of a dollar bill (Section 1.1) and for the rail and highway capacities (Section 1.2) used the same method: dividing hard problems into smaller ones. However, the structure of the analysis is buried within the sentences, paragraphs, and pages. The sequential presentation hides the structure. Because the structure is hierarchical—big problems 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8

1 Divide and conquer

split, or branch, into smaller problems—its most compact representation is a tree. A tree representation shows us the analysis in one glance.

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

lar bill—the root—is 1 cubic centimeter.

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

Our analysis of the carrying capacity of highways and railways (Section 1.2) is an example of a frequent application of estimation in the social world—estimating the size of a market. The highway–railway comparison proceeded by estimating the transportation supply. In other problems, a more feasi-ble analysis is based on the complementary idea of estimating the demand.

Here is an example.

How much oil does the United States import (in barrels per year)?

The volume rate is enormous and therefore hard to picture. Divide-and-conquer reasoning will tame the complexity. Just keep subdividing until the quantities are no longer daunting.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.4 Demand-side estimates 11

Here, subdivide the demand—the consumption. We consume oil in so many ways; estimating the consumption in each pathway would take a long time without producing much insight. Instead, let's estimate the largest consumption—likely to be cars—then adjust for other uses and for overall consumption versus imports.

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

But don't do this estimate directly. It is more intuitive—that is, easier for our gut—to estimate first the ratio of car usage to other (noncar) usage. The ability to make such comparisons between disjoint sets, at least for physical objects, is hard wired in our brains and independent of the ability to count. Not least, it is not limited to humans. The female lions studied by Karen McComb and her colleagues [35] would judge the relative size of their troop and a group of lions intruding on their territory. The females would approach the intruders only when they outnumbered the intruders by a large-enough ratio, roughly a factor of 2.

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

This estimate is the first leaf. It implicitly assumes that the gasoline fraction in a barrel of oil is high enough to feed the cars. Fortunately, if this assumption were wrong, we would get warning. For if the fraction were too low, we would build our transportation infrastructure around other means of transport—such as trains powered by electricity generated by burning the nongasoline fraction in oil barrels. In this probably less-polluted world, we would estimate how much oil was used by trains.

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

the per-car usage. Both quantities are easier to estimate than the root. The number of cars is related to the US population—a familiar number if you live in the United States. The per-car usage is easier to estimate than is the total usage of all US

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

Therefore, a rough and simple estimate might be one car per person—far easier to picture than the total number of cars! Then 𝑁cars ≈ 3×108.

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

The first shock was the 9 in the 9 million. I assumed that it was the number of billions, and wondered how the estimate of 3 billion barrels could be a factor of 3 too small. The second shock was the「million」—how could the estimate be more than a factor of 100 too large? Then the「per day」

reassured me. As a yearly rate, 9.163 million barrels per day is 3.34 billion barrels per year—only 10 percent higher than our estimate. Divide and conquer triumphs!

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

In contrast, mindless redundancy offers little protection. If we check the calculation by adding the numbers from top to bottom again, we usually repeat any mistakes. Similarly, rereading written drafts usually means overlooking the same spelling, grammar, or logic faults. Instead, stuff the draft in a drawer for a week, then look at it; or ask a colleague or friend—in both cases, use fresh eyes.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

1.6 Talking to your gut

17

Reliability, in short, comes from intelligent redundancy.

This principle helps you make reliable estimates. First, use several methods to estimate the same quantity. Second, make the methods as different from one another as possible—for example, by using unrelated background knowledge. This approach to reliability is another example of divide-and-conquer reasoning: The hard problem of making a reliable estimate becomes several simpler subproblems, one per estimation method.

You saw an example in Section 1.1, where we estimated the volume of a dollar bill. The first method used divide-and-conquer reasoning based on the width, height, and thickness of the bill. The check was a comparison with a folded-up dollar bill. Both methods agreed on a volume of approximately 1 cubic centimeter—giving us confidence in the estimate.

For another example of using multiple methods, return to the estimate of the volume of an oil barrel (Section 1.4). We used a roadside asphalt barrel as a proxy for an oil barrel and estimated the volume of the roadside barrel. The result, 60 gallons, seemed plausible, but maybe oil barrels have a completely different size. One way to catch that kind of error is to use a different method for estimating the volume. For example, we might start with the cost of a barrel of oil—about `$`100 in 2013—and the cost of a gallon of gasoline—about `$`2.50 before taxes, or 1/40th of the cost of a barrel. If the markup on gasoline is not significant, then a barrel is roughly 40 gallons. Even with a markup, we can still say that a barrel is at least 40 gallons.

Because our two estimates, 60 gallons and > 40 gallons, roughly agree, our confidence in both increases. If they had contradicted each other, one or both would be wrong, and we would look for the mistaken assumption, for the incorrect arithmetic, or for a third method.

1.6 Talking to your gut

As you have seen in the preceding examples, divide-and-con-US population

quer estimates require reasonable estimates for the leaf quantities. To decide what is reasonable, you have to talk to your gut—what you will learn in this section. Talking to your gut feels strange at first, especially because science and engineer-population

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

To draw on its knowledge, ask it indirectly. Pick a particular population density—say, 100 people per square mile—and ask the gut for its opinion:

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

The geometric mean is the midpoint of the lower and upper bounds—but on a ratio or logarithmic scale, which is the scale built into our mental hardware. (For more about how we perceive quantity, see The Number Sense

[9].) The geometric mean is the correct mean when combining quantities produced by our mental hardware.

Here, the geometric mean is 30 people per square mile: a factor of 10 removed from either endpoint. Using that population density, US population ∼ 6×106 miles2 × 30

miles2 ≈ 2 × 108.

(1.18)

The actual population is roughly 3×108. The estimate based almost entirely on gut reasoning is within a factor of 1.5 of the actual population—a pleasantly surprising accuracy.

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

To estimate the salinity of seawater, which will later help you estimate the conductivity of seawater (Problem 8.10), do not ask your gut directly:「How do you feel about, say, 200 millimolar?」Although that kind of question worked for estimating population density (Section 1.6), here, unless you are a chemist, the answer will be:「I have no clue. What is a millimolar anyway? I have almost no experience of that unit.」Instead, offer your gut concrete data—for example, from a home experiment: adding salt to a cup of water until the mixture tastes as salty as the ocean.

This experiment can be a thought or a real experiment—another example of using multiple methods (Section 1.5). As a thought experiment, I ask my gut about various amounts of salt in a cup of water. When I propose adding 2 teaspoons, it responds,「Disgustingly salty!」At the lower end, when I propose adding 0.5 teaspoons, it responds,「Not very salty.」I'll use 0.5 and 2 teaspoons as the lower and upper endpoints of the range. Their midpoint, the estimate from the thought experiment, is 1 teaspoon per cup.

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

The actual salinity of the Earth's oceans is about 3.5 percent—very close to the estimate of 4 percent. The estimate is close despite the large number of assumptions and approximations—the errors have mostly canceled. Its accuracy should give you courage to perform home experiments whenever you need data for divide-and-conquer estimates.

Problem 1.9

Density of water

Estimate the density of water by asking your gut to estimate the mass of water in a cup measure (roughly one-quarter of a liter).

Problem 1.10

Density of salt

Estimate the density of salt using the volume and mass of a typical salt container that you find in a grocery store. This value should be more accurate than my gut estimate in Section 1.7.1 (which was 2 grams per cubic centimeter).

1.7.2 Human power output

Our second example of talking to your gut is an estimate of hu-power

man power output—a power that is useful in many estimates (for example, Problem 1.17). Energies and powers are good can-

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

Maintaining a power is harder than producing a quick burst. Therefore, the first adjustment factor, my steady power divided by my burst power, is somewhat smaller than 1—maybe 1/2 or 1/3. In contrast, an athlete's 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

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

The remaining leaf is the time: how long the climb took me. I made it in 6 seconds. In contrast, several students made it in 3.9 seconds—the power of youth! My mechanical power output was about 2000 joules per 6 seconds, or about 300 watts. (To check whether the estimate is reasonable, try Problem 1.12, where you estimate the typical human basal metabolism.) This burst power output should be close to the sustained power output of a trained athlete. And it is. As an example, in the Alpe d'Huez climb in the 1989 Tour de France, the winner—Greg LeMond, a world-class athlete—put out 394 watts (over a 42.5-minute period). The cyclist Lance Armstrong, during the time-trial stage during the Tour de France in 2004, generated even more: 495 watts (roughly 7 watts per kilogram). However, he publicly admitted to blood doping to enhance performance. Indeed, because of widespread doping, many cycling power outputs of the 1990s and 2000s are suspect; 400 watts stands as a legitimate world-class sustained power output.

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

Because water covers so much of the Earth and is such an important part of the atmosphere (clouds!), its heat of vaporization strongly affects our climate—whether through rainfall (Section 3.4.3) or air temperatures.

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

For the mass of the substance, choose an amount of water that is easy to imagine—ideally, an amount familiar from everyday life. Then your gut can help you make estimates. Because I often boil a few cups of water at a time, and each cup is few hundred milliliters, I'll imagine 1 liter or 1 kilogram of water.

The other leaf, the required energy, requires more thought. There is a common confusion about this energy that is worth discussing.

Is it the energy required to bring the water to a boil?

No: The energy has nothing to do with the energy required to bring the water to a boil! That energy is related to water's specific heat 𝑐p. The heat of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

24

1 Divide and conquer

vaporization depends on the energy needed to evaporate—boil away—the water, once it is boiling. (You compare these energies in Problem 5.61.) Energy subdivides into power times time (as when we es-heat of

vaporization

timated human power output in Section 1.7.2). Here, the power could be the power output of one burner; the time is the time to boil away the liter of water. To estimate these

−1

leaves, let's hold a gut conference.

energy

mass

For the time, my dialogue is as follows.

LB: How does 1 minute sound as a lower bound?

RB: Way too short—you've left boiling water on the stove unattended for longer without its boiling away!

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

My range is therefore 3…30 minutes. Its midpoint—the geometric mean of the endpoints—is about 10 minutes or 600 seconds.

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

This estimate agrees with the gut estimate, so both methods gain plausibility—which should give you confidence to use both methods for your own estimates. As a check, I looked at the circuit breaker connected to my range, and it is rated for 50 amperes. The range has four burners and an oven, so 15 amperes for one burner (at least, for the large burner) is plausible.

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

2Abstraction

2.1 Energy from burning hydrocarbons

28

2.2 Coin-flip game

31

2.3 Purpose of abstraction

34

2.4 Analogies

36

2.5 Summary and further problems

53

Divide-and-conquer reasoning, the tool introduced in Chapter 1, is powerful, but it is not enough by itself to organize the complexity of the world.

Try, for example, to manage the millions of files on a computer—even my laptop says that it has almost 3 million files. Without any organization, with all the files in one monster directory or folder, you could never find information that you need. However, simply using divide and conquer by dividing the files into groups—the first 100 files by date, the second 100 files by date, and so on—does not disperse the chaos. A better solution is to organize the millions of files into a hierarchy: as a tree of folders and subfolders. The elements in this hierarchy get names—for example,「photos of the children」or

「files for typesetting this book」—and these names guide us to the needed information.

Naming—or, more technically, abstraction—is our other tool for organizing complexity. A name or an abstraction gets its power from its reusability.

Without reusable ideas, the world would become unmanageably complicated. We might ask,「Could you, without tipping it over, move the wooden board glued to four thick sticks toward the large white plastic circle?」instead of,「Could you slide the chair toward the table?」The abstractions

「chair,」「slide,」and「table」compactly represent complex ideas and physical structures. (And even the complex question itself uses abstractions.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

28

2 Abstraction

Similarly, without good abstractions we could hardly calculate, and modern science and technology would be impossible. As an illustration, imagine the pain of the following calculation:

XXVII × XXXVI,

(2.1)

which is 27×36 in Roman numerals. The problem is not that the notation is unfamiliar, but rather that it is not based on abstractions useful for calculation. Not least, it does not lend itself to divide-and-conquer reasoning; for example, even though V (5) is a part of XXVII, V×XXXVI has no obvious answer. In contrast, our modern number system, based on the abstractions of place value and zero, makes the whole multiplication simple. Notations are abstractions, and good abstractions amplify our intelligence. In this chapter, we will practice making abstractions, discuss their high-level purpose, and continue to practice.

2.1 Energy from burning hydrocarbons

Our understanding of the world is built on layers of abstrac-fluid

tions. Consider the idea of a fluid. At the bottom of the abstraction hierarchy are the actors of particle physics: quarks and electrons. Quarks combine to build protons and neu-molecules

trons. Protons, neutrons, and electrons combine to build atoms. Atoms combine to build molecules. And large collec-atoms

tions of molecules act, under many conditions, like a fluid.

The idea of a fluid is a new unit of thought. It helps us understand diverse phenomena, without our having to calcu-protons,

electrons

late or even know how quarks and electrons interact to pro-neutrons

duce fluid behavior. As one consequence, we can describe the behavior of air and water using the same equations (the quarks

Navier–Stokes equations of fluid mechanics); we need only to use different values for the density and viscosity. Then atmospheric cyclones and water vortices, although they result from widely differing sets of quarks and electrons and their interactions, can be understood as the same phenomenon.

A similarly powerful abstraction is a chemical bond. We'll use this abstraction to estimate a quantity essential to our bodies and to modern society: the energy released by burning chains made of hydrogen and carbon atoms (hydrocarbons). A hydrocarbon can be abstracted as a chain of CH2 units: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.1 Energy from burning hydrocarbons 29

H

H

H

H

H

H

· · ·

C

C

C

C

C

C

· · ·

H

H

H

H

H

H

Burning a CH2 unit requires oxygen (O2) and releases carbon dioxide (CO2), water, and energy:

CH2 + 32O2 ⟶ CO2 + H2O + energy.

(2.2)

For a hydrocarbon with eight carbons—such as octane, a prime component of motor fuel—simply multiply this reaction by 8: (CH2)8 + 12 O2 ⟶ 8 CO2 + 8 H2O + lots of energy.

(2.3)

(The two additional hydrogens at the left and right ends of octane are not worth worrying about.)

How much energy is released by burning one CH2 unit?

To make this estimate, use the table of bond bond energy

energies. It gives the energy required to break kcal

kJ

eV

(not make) a chemical bond—for example, be-

( mol) (mol) (bond)

tween carbon and hydrogen. However, there

is no unique carbon–hydrogen (C–H) bond. C—H

99

414

4.3

The carbon–hydrogen bonds in methane are O—H

111

464

4.8

different from the carbon–hydrogen bonds in C—C

83

347

3.6

ethane. To make a reusable idea, we neglect C—O

86

360

3.7

those differences—placing them below our H—H

104

435

4.5

abstraction barrier—and make an abstraction C—N

73

305

3.2

called the carbon–hydrogen bond. So the ta- N—H

93

389

4.0

ble, already in its first column, is built on an O=O

119

498

5.2

abstraction.

C=O

192

803

8.3

The second gives the bond energy in kilo- C=C

146

611

6.3

calories per mole of bonds. A kilocalorie is N≡N

226

946

9.8

roughly 4000 joules, and a mole is Avogadro's number (6×1023) of bonds. The third column gives the energy in the SI units used by most of the world, kilojoules per mole. The final column gives the energy in electron volts (eV) per bond. An electron volt is 1.6×10−19 joules.

An electron volt is suited for measuring atomic energies, because most bond energies have an easy-to-grasp value of a few electron volts. I wish most of the world used this unit!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

30

2 Abstraction

Let's tabulate the energies in the combustion of one hydrocarbon unit.

H

O

H

O

bond energy

C

+ 32 × ⟶ C + O

(2.4)

kcal

kJ

O

( mol)

(mol)

H

O

H

The left side of the reaction has two carbon–hy- 1 × C—C

1 × 83

1 × 347

drogen bonds,

2 × C—H

2 × 99

2 × 414

1.5 oxygen–oxygen double bonds,

and one carbon–carbon bond (connecting the car- 1.5 × O=O

1.5 × 119

1.5 × 498

bon atom in the CH2 unit to the carbon atom in Total 460

1925

a neighboring unit). The total, 460 kilocalories or 1925 kilojoules per mole, is the energy required to break the bonds. It is an energy input, so it reduces the net combustion energy.

The right side has two carbon–oxygen double bonds bond energy

and two oxygen–hydrogen bonds. The total for the kcal

kJ

right side, 606 kilocalories or 2535 kilojoules per mole, ( mol) (mol)

is the energy released in forming these bonds. It is the energy produced, so it increases the net combustion 2 × C=O

2 × 192

2 × 803

energy.

2 × O—H

2 × 111

2 × 464

The net result is, per mole of CH2, an energy release of Total 606

2535

606 minus 460 kilocalories, or approximately 145 kilocalories (610 kilojoules). Equivalently, it is also about 6 electron volts per CH2 unit—about 1.5 chemical bonds' worth of energy. The combustion energy is also useful as an energy per mass rather than per mole. A mole of CH2 units weighs 14 grams. Therefore, 145 kilocalories per mole is roughly 10 kilocalories or 40 kilojoules per gram. This energy density is worth memorizing because it gives the energy released by burning oil and gasoline or by metabolizing fat (even though fat is not a pure hydrocarbon).

combustion energy

kcal

(

kcal

kJ

mol )

( g ) ( g )

hydrogen (H2)

68

34.0

142

methane (CH4)

213

13.3

56

gasoline (C8H18)

1303

11.5

48

stearic acid (C18H36O2)

2712

9.5

40

glucose (C6H12O6)

673

3.7

15

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.2 Coin-flip game

31

The preceding table, adapted from Oxford University's「Virtual Chemistry」

site, gives actual combustion energies for plant and animal fuel sources (with pure hydrogen included for fun). The penultimate entry, stearic acid, is a large component of animal fat; animals store energy in a substance with an energy density comparable to the energy density in gasoline—roughly 10 kilocalories or 40 kilojoules per gram. Plants, on the other hand, store energy in starch, which is a chain of glucose units; glucose has an energy density of only roughly 4 kilocalories per gram. This value, the energy density of food carbohydrates (sugars and starches), is also worth memorizing.

It is significantly lower than the energy density of fats: Eating fat fills us up much faster than eating starch does.

How can we explain the different plant and animal energy-storage densities?

Plants do not need to move, so the extra weight required by using lower-density energy storage is not so important. The benefit of the simpler glucose metabolic pathway outweighs the drawback of the extra weight. For animals, however, the large benefit of lower weight outweighs the metabolic complexity of burning fats.

Problem 2.1

Estimating the energy density of common foods In American schools, the traditional lunch is the peanut-butter-and-jelly sandwich.

Estimate the energy density in peanut butter and in jelly (or jam).

Problem 2.2

Peanut butter as fuel

If you could convert all the combustion energy in one tablespoon (15 grams) of peanut butter into mechanical work, how many flights of stairs could you climb?

Problem 2.3

Growth of grass

How fast does grass grow? Is the rate limited by rainfall or by sunlight?

2.2 Coin-flip game

The abstractions of atoms, bonds, and bond energies have been made for us by the development of science. But we often have to make new abstractions.

To develop this skill, we'll analyze a coin game where two players take turns flipping a (fair) coin; whoever first tosses heads wins.

What is the probability that the first player wins?

First get a feel for the game by playing it. Here is one round: TH. The first player missed the chance to win by tossing tails (T); but the second player tossed heads (H) and won.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

32

2 Abstraction

Playing many games might reveal a pattern to us or suggest how to com- 2 TH

pute the probability. However, playing many games by flipping a real 2 TH

coin becomes tedious. Instead, a computer can simulate the games, sub- 1 H

stituting pseudorandom numbers for a real coin. Here are several runs 2 TH

produced by a computer program. Each line begins with 1 or 2 to indicate 1 TTH

which player won the game; the rest of the line shows the coin tosses. In 2 TTTH

these ten iterations, each player won five times. A reasonable conjecture 2 TH

is that each player has an equal chance to win. However, this conjecture, 1 H

based on only ten games, cannot be believed too strongly.

1 H

1 H

Let's try 100 games. Now even counting the wins becomes tedious. My computer counted for me: 68 wins for player 1, and 32 wins for player 2.

The probability of player 1's winning now seems closer to 2/3 than to 1/2.

To find the exact value, let's diagram the game as a tree re-start

flecting the alternative endings of the game. Each layer represents one flip. The game ends at a leaf, when one player has tossed heads. The shaded leaves show the first player's wins—for example, after H, TTH, or TTTTH. The probabili-H

T

1/2

ties of these winning ways are 1/2 (for H), 1/8 (for TTH), and 1/32 (for TTTTH). The sum of all these winning probabilities is the probability of the first player's winning: 1

H

T

2 + 18 + 1

32 + ⋯.

(2.5)

1/4

To sum this infinite series without resorting to formulas, make an abstraction: Notice that the tree contains, one level down, a near copy of itself. (In this problem, the abstraction gets reused within the same problem. In computer science, such a H

. . .

1/8

structure is called recursive.) For if the first player tosses tails, the second player starts the game in the position of the first player, with the same probability of winning.

To benefit from this equivalence, let's name the reusable idea, namely the probability of the first player's winning, and call it 𝑝. The second player wins the game with probability 𝑝/2: The factor of 1/2 is the probability that the first player tosses tails; the factor of 𝑝 is the probability that the second player wins, given that the first player blew his chance by tossing tails on the first toss.

Because either the first or the second player wins, the two winning probabilities add to 1:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.2 Coin-flip game

33

𝑝

⏟

+

𝑝/2

⏟

= 1.

(2.6)

𝑃(first player wins)

𝑃(second player wins)

The solution is 𝑝 = 2/3, as suggested by the 100-game simulation. The benefit of the abstraction solution, compared to calculating the infinite probability sum explicitly, is insight. In the abstraction solution, the answer has to be what it is. It leaves almost nothing to remember. An amusing illustration of the same benefit comes from the problem of the fly that zooms back and forth between two approaching trains.

If the fly starts when the trains are 60 miles apart, each train travels at 20 miles per hour, and the fly travels at 30 miles per hour, how far does the fly travel, in total, before meeting its maker when the trains collide? (Apologies that physics problems are often so violent.)

Right after hearing the problem, John von Neumann, inventor of game theory and the modern computer, gave the correct distance.「That was quick,」

said a colleague.「Everyone else tries to sum the infinite series.」「What's wrong with that?」said von Neumann.「That's how I did it.」In Problem 2.7, you get to work out the infinite-series and the insightful solutions.

Problem 2.4

Summing a geometric series using abstraction Use abstraction to find the sum of the infinite geometric series 1 + 𝑟 + 𝑟2 + 𝑟3 + ⋯.

(2.7)

Problem 2.5

Using the geometric-series sum

Use Problem 2.4 to check that the probability of the first player's winning is 2/3: 𝑝 = 12 + 18 + 132 + ⋯ = 23.

(2.8)

Problem 2.6

Nested square roots

Evaluate these infinite mixes of arithmetic and square roots: 3 × 3 × 3 × 3 × ⋯ .

(2.9)

2 + 2 + 2 + 2 + ⋯ .

(2.10)

Problem 2.7

Two trains and a fly

Find the insightful and the infinite-series solution to the problem of the fly and the approaching trains (Section 2.2). Check that they give the same answer for the distance that the fly travels!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

34

2 Abstraction

Problem 2.8

Resistive ladder

In the following infinite ladder of 1-ohm resistors, what is the resistance between points A and B? This measurement is indicated by the ohmmeter connected between these points.

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

. . .

A

Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

. . .

. . .

B

2.3 Purpose of abstraction

The coin game (Section 2.2), like the geometric series (Problem 2.4) or the resistive ladder (Problem 2.8), contained a copy of itself. Noticing this reuse greatly simplified the analysis. Abstraction has a second benefit: giving us a high-level view of a problem or situation. Abstractions then show us structural similarities between seemingly disparate situations.

As an example, let's revisit the geometric mean, introduced in Section 1.6

to make gut estimates. The geometric mean of two nonnegative quantities 𝑎 and 𝑏 is defined as

geometric mean ≡ 𝑎𝑏 .

(2.11)

This mean is called the geometric mean because it has a pleasing geometric construction. Divide the diameter

√

of a circle into two lengths, 𝑎 and 𝑏, and inscribe a right ab

triangle whose hypotenuse is the diameter. The triangle's altitude is the geometric mean of 𝑎 and 𝑏.

a

b

This mean reappears in surprising places, including the beach. When you stand at the shore and look at the horizon, you are seeing a geometric mean. The distance to the horizon is the geometric mean of two important lengths in the problem (Problem 2.9).

For me, its most surprising appearance was in the「Programming and Problem-Solving Seminar」course taught by Donald Knuth [40] (who also created TEX, the typesetting system for this book). The course, taught as a series of two-week problems, helped first-year PhD students transition from undergraduate homework problems to PhD research problems. A homework problem requires perhaps 1 hour. A research problem requires, say, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.3 Purpose of abstraction 35

1000 hours: roughly a year of work, allowing for other projects. (A few problems stapled together become a PhD.) In the course, each 2-week module required about 30 hours—approximately the geometric mean of the two endpoints. The modules were just the right length to help us cross the bridge from homework to research.

Problem 2.9

Horizon distance

How far is the horizon when you are standing at the shore? Hint: It's farther for an adult than for a child.

Problem 2.10

Distance to a ship

Standing at the shore, you see a ship (drawn to scale) with a 10-meter mast sail into the distance and disappear from view. How far away was it when it disappeared?

As further evidence that the geometric mean is a useful abstraction, the idea appears even when there is no geometric construction to produce it, such as in making gut estimates. We used this method in Section 1.6 to estimate the population density and then the population of the United States. Let's practice by estimating the oil imports of the United States in barrels per year—without the divide-and-conquer reasoning of Section 1.4.

The method requires that the gut supply a lower and an upper bound. My gut reports back that it would feel fairly surprised if the imports were less than 10 million barrels per year. On the upper end, my gut would be fairly surprised if the imports were higher than 1 trillion barrels per year—a barrel is a lot of oil, and a trillion is a large number!

You might wonder how your gut too can come up with such large numbers and how you can have any confidence in them. Admittedly, I have practiced a lot. But you can practice too. The key is the practice effectively. First, have the courage to guess even when you feel anxious about it (I feel this anxiety still, so I practice this courage often). Second, compare your guess to values in which you can place more confidence—for example, to your own more careful estimates or to official values. The comparison helps calibrate your gut (your right brain) to these large magnitudes. You will find a growing and justified confidence in your judgment of magnitude.

My best guess for the amount is the geometric mean of the lower and upper estimates:

10 million × 1 trillion barrels

year .

(2.12)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

36

2 Abstraction

The result is roughly 3 billion barrels per year—close to the our estimate using divide and conquer and close to the true value. In contrast, the arithmetic mean would have produced an estimate of 500 billion barrels per year, which is far too high.

Problem 2.11

Arithmetic-mean–geometric-mean inequality Use the geometric construction for the geometric mean to show that the arithmetic mean of 𝑎 and 𝑏 (assumed to be nonnegative) is always greater than or equal to their geometric mean. When are the means equal?

Problem 2.12

Weighted geometric mean

A generalization of the arithmetic mean of 𝑎 and 𝑏 as (𝑎 + 𝑏)/2 is to give 𝑎 and 𝑏 unequal weights. What is the analogous generalization for a geometric mean?

(The weighted geometric mean shows up in Problem 6.29 when you estimate the contact time of a ball bouncing from a table.) 2.4 Analogies

Because abstractions are so useful, it is helpful to have methods for making them. One way is to construct an analogy between two systems. Each common feature leads to an abstraction; each abstraction connects our knowledge in one system to our knowledge in the other system. One piece of knowledge does double duty. Like a mental lever, analogy and, more generally, abstraction are intelligence amplifiers.

2.4.1 Electrical–mechanical analogies

An illustration with many abstractions on which we can practice is the analogy between a spring–mass system and an inductor–capacitor (𝐿𝐶) circuit.

L

Vin

Vout

k

m

↔

(2.13)

C

In the circuit, the voltage source—the 𝑉in on its left side—supplies a current that flows through the inductor (a wire wrapped around an iron rod) and capacitor (two metal plates separated by air). As current flows through the capacitor, it alters the charge on the capacitor. This「charge」is confusingly named, because the net charge on the capacitor remains zero. Instead, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

37

「charge」means that the two plates of the capacitor hold opposite charges, 𝑄 and −𝑄, with 𝑄 ≠ 0. The current changes 𝑄. The charges on the two plates create an electric field, which produces the output voltage 𝑉out equal to 𝑄/𝐶 (where 𝐶 is the capacitance).

For most of us, the circuit is less familiar than the spring–mass system.

However, by building an analogy between the systems, we transfer our understanding of the mechanical to the electrical system.

In the mechanical system, the fundamental variable spring

circuit

is the mass's displacement 𝑥. In the electrical sys- variable 𝑥

𝑄

tem, it is the charge 𝑄 on the capacitor. These vari- 1st derivative 𝑣

𝐼

ables are analogous so their derivatives should also 2nd derivative 𝑎

𝑑𝐼/𝑑𝑡

be analogous: Velocity (𝑣), the derivative of position, should be analogous to current (𝐼), the derivative of charge.

Let's build more analogy bridges. The derivative of velocity, which is the second derivative of position, is acceleration (𝑎). Therefore, the derivative of current (𝑑𝐼/𝑑𝑡) is the analog of acceleration. This analogy will be useful shortly when we find the circuit's oscillation frequency.

These variables describe the state of the systems and how that state changes: They are the kinematics. But without the causes of the motion—the dynamics—the systems remain lifeless. In the mechanical system, dynamics results from force, which produces acceleration: 𝑎 = 𝐹𝑚.

(2.14)

Acceleration is analogous to change in current 𝑑𝐼/𝑑𝑡, which is produced by applying a voltage to the inductor. For an inductor, the governing relation (analogous to Ohm's law for a resistor) is

𝑑𝐼

𝑑𝑡 = 𝑉𝐿 ,

(2.15)

where 𝐿 is the inductance, and 𝑉 is the voltage across the inductor. Based on the common structure of the two relations, force 𝐹 and voltage 𝑉 must be analogous. Indeed, they both measure effort: Force tries to accelerate the mass, and voltage tries to change the inductor current. Similarly, mass and inductance are analogous: Both measure resistance to the corresponding effort. Large masses are hard to accelerate, and large-𝐿 inductors resist changes to their current. (A mass and an inductor, in another similarity, both represent kinetic energy: a mass through its motion, and an inductor through the kinetic energy of the electrons making its magnetic field.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

38

2 Abstraction

Turning from the mass–inductor analogy, let's look at the spring–capacitor analogy. These components represent the potential energy in the system: in the spring through the energy in its compression or expansion, and in the capacitor through the electrostatic potential energy due to its charge.

Force tries to stretch the spring but meets a resistance 𝑘: The stiffer the spring (the larger its 𝑘), the harder it is to stretch.

𝑥 = 𝐹𝑘.

(2.16)

Analogously, voltage tries to charge the capacitor but meets a resistance 1/𝐶: The larger the value of 1/𝐶, the smaller the resulting charge.

𝑄 = 𝑉

1/𝐶.

(2.17)

Based on the common structure of the relations for 𝑥 and 𝑄, spring constant 𝑘 must be analogous to inverse capacitance 1/𝐶. Here are all our analogies.

mechanical

electrical

kinematics

fundamental variable

𝑥

𝑄

first derivative

𝑣

𝐼

second derivative

𝑎

𝑑𝐼/𝑑𝑡

dynamics

effort

𝐹

𝑉

resistance to effort (kinetic component)

𝑚

𝐿

resistance to effort (potential component)

𝑘

1/𝐶

From this table, we can read off our key result. Start with the natural (angular) frequency 𝜔 of a spring–mass system: 𝜔 = 𝑘/𝑚. Then apply the analogies. Mass 𝑚 is analogous to inductance 𝐿. Spring constant 𝑘 is analogous to inverse capacitance 1/𝐶. Therefore, 𝜔 for the 𝐿𝐶 circuit is 1/ 𝐿𝐶 : 𝜔 = 1/𝐶

𝐿 = 1 .

(2.18)

𝐿𝐶

Because of the analogy bridges, one formula, the natural frequency of a spring–mass system, does double duty. More generally, whatever we learn about one system helps us understand the other system. Because of the analogies, each piece of knowledge does double duty.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

39

2.4.2 Energy density in the gravitational field With the electrical–mechanical analogy as practice, let's try a less familiar analogy: between the electric and the gravitational field. In particular, we'll connect the energy densities (energy per volume) in the corresponding fields. An electric field 𝐸 represents an energy density of 𝜖0𝐸2/2, where 𝜖0 is the permittivity of free space appearing in the electrostatic force between two charges 𝑞1 and 𝑞2:

𝐹 = 𝑞1𝑞2

4𝜋𝜖0𝑟2.

(2.19)

Because electrostatic and gravitational forces are both inverse-square forces (the force is proportional to 1/𝑟2), the energy densities should be analogous.

Not least, there should be a gravitational energy density. But how is it related to the gravitational field?

To answer that question, our first step is to find the gravitational analog of the electric field. Rather than thinking of the electric field only as something electric, focus on the common idea of a field. In that sense, the electric field is the object that, when multiplied by the charge, gives the force: force = charge × field.

(2.20)

We use words rather than the normal symbols, such as 𝐸 for field or 𝑞 for charge, because the symbols might bind our thinking to particular cases and prevent us from climbing the abstraction ladder.

This verbal form prompts us to ask: What is gravitational charge? In electrostatics, charge is the source of the field. In gravitation, the source of the field is mass. Therefore, gravitational charge is mass. Because field is force per charge, the gravitational field strength is an acceleration: gravitational field = force

charge = force

mass = acceleration.

(2.21)

Indeed, at the surface of the Earth, the field strength is 𝑔, also called the acceleration due to gravity.

The definition of gravitational field is the first half of the puzzle (we are using divide-and-conquer reasoning again). For the second half, we'll use the field to compute the energy density. To do so, let's revisit the route from electric field to electrostatic energy density: 𝐸 → 12𝜖0𝐸2.

(2.22)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

40

2 Abstraction

With 𝑔 as the gravitational field, the analogous route is 𝑔 → 12 × something × 𝑔2,

(2.23)

where the「something」represents our ignorance of what to do about 𝜖0.

What is the gravitational equivalent of 𝜖0 ?

To find its equivalent, compare the simplest case in both worlds: the field of a point charge. A point electric charge 𝑞 produces a field 𝐸 = 1 𝑞

4𝜋𝜖0 𝑟2.

(2.24)

A point gravitational charge 𝑚 (a point mass) produces a gravitational field (an acceleration)

𝑔 = 𝐺𝑚

𝑟2 ,

(2.25)

where 𝐺 is Newton's constant.

The gravitational field has a similar structure to the electric field. Both are inverse-square forces, as expected. Both are proportional to the charge.

The difference is the constant of proportionality. For the electric field, it is 1/4𝜋𝜖0. For the gravitational field, it is simply 𝐺. Therefore, 𝐺 is analogous to 1/4𝜋𝜖0; equivalently, 𝜖0 is analogous to 1/4𝜋𝐺.

Then the gravitational energy density becomes 12 × 14𝜋𝐺 ×𝑔2 = 𝑔2

8𝜋𝐺.

(2.26)

We will use this analogy in Section 9.3.3 when we transfer our hard-won knowledge of electromagnetic radiation to understand the even more subtle physics of gravitational radiation.

Problem 2.13

Gravitational energy of the Sun

What is the energy in the gravitational field of the Sun? (Just consider the field outside the Sun.)

Problem 2.14

Pendulum period including buoyancy

The period of a pendulum in vacuum is (for small amplitudes) 𝑇 = 2𝜋 𝑙/𝑔 , where 𝑙 is the bob length and 𝑔 is the gravitational field strength. Now imagine the pendulum swinging in a fluid (say, air). By replacing 𝑔 with a modified value, include the effect of buoyancy in the formula for the pendulum period.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

41

Problem 2.15

Comparing field energies

Find the ratio of electrical to gravitational field energies in the fields produced by a proton.

2.4.3 Parallel combination

Analogies not only reuse work, they help us rewrite expressions in compact, insightful forms. An example is the idea of parallel combination. It appears in the analysis of the infinite resistive ladder of Problem 2.8.

the ladder all over again

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

. . .

A

Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

1 Ω

. . .

. . .

B

To find the resistance 𝑅 across the ladder (in other words, what the ohmmeter measures between the nodes A and B), you represent the entire ladder as a single resistor 𝑅. Then the whole ladder is 1 ohm in series with the parallel combination of 1 ohm and 𝑅:

1 Ω

R

=

(2.27)

1 Ω

R

The next step in finding 𝑅 usually invokes the parallel-resistance formula: that the resistance of 𝑅1 and 𝑅2 in parallel is 𝑅1𝑅2

𝑅

.

(2.28)

1 + 𝑅2

For our resistive ladder, the parallel combination of 1 ohm with the ladder is 1 ohm × 𝑅/(1 ohm + 𝑅). Placing this combination in series with 1 ohm gives a resistance

1 Ω + 1 Ω × 𝑅

1 Ω + 𝑅.

(2.29)

This recursive construction reproduces the ladder, only one unit longer. We therefore get an equation for 𝑅:

𝑅 = 1 Ω + 1 Ω × 𝑅

1 Ω + 𝑅.

(2.30)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

42

2 Abstraction

The (positive) solution is 𝑅 = (1 + 5)/2 ohms. The numerical part is the golden ratio 𝜙 (approximately 1.618). Thus, the ladder, when built with 1-ohm resistors, offers a resistance of 𝜙 ohms.

Although the solution is correct, it skips over a reusable idea: the parallel combination. To facilitate its reuse, let's name the idea with a notation: 𝑅1 ∥ 𝑅2.

(2.31)

This notation is self-documenting, as long as you recognize the symbol ∥

to mean「parallel,」a recognition promoted by the parallel bars. A good notation should help thinking, not hinder it by requiring us to remember how the notation works. With this notation, the equation for the ladder resistance 𝑅 is

𝑅 = 1 Ω + 1 Ω ∥ 𝑅

(2.32)

(the parallel-combination operator has higher priority than—is computed before—the addition). This expression more plainly reflects the structure of the system, and our reasoning about it, than does the version 𝑅 = 1 Ω + 1 Ω × 𝑅

1 Ω + 𝑅.

(2.33)

The ∥ notation organizes the complexity.

Once you name an idea, you find it everywhere. As a child, after my family bought a Volvo, I saw Volvos on every street. Similarly, we'll now look at examples of parallel combination far beyond the original appearance of the idea in circuits. For example, it gives the spring constant of two connected springs (Problem 2.16):

⏟⏟⏟⏟⏟⏟⏟ ⏟⏟⏟⏟⏟⏟⏟ = ⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

(2.34)

𝑘1

𝑘2

𝑘1∥ 𝑘2

Problem 2.16

Springs as capacitors

Using the analogy between springs and capacitors (discussed in Section 2.4.1), explain why springs in series combine using the parallel combination of their spring constants.

Another surprising example is the following spring–mass system with two masses:

k

m

M

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

43

The natural frequency 𝜔, expressed without our ∥ abstraction, is 𝜔 = 𝑘(𝑚 + 𝑀)

𝑚𝑀 .

(2.35)

This form looks complicated until we use the ∥ abstraction: 𝜔 =

𝑘

𝑚 ∥ 𝑀.

(2.36)

Now the frequency makes more sense. The two masses act like their parallel combination 𝑚 ∥ 𝑀:

k

m k M

The replacement mass 𝑚 ∥ 𝑀 is so useful that it has a special name: the reduced mass. Our abstraction organizes complexity by turning a three-component system (a spring and two masses) into a simpler two-component system.

In the spirit of notation that promotes insight, use lowercase (「small」) 𝑚 for the mass that is probably smaller, and uppercase (「big」) 𝑀 for the mass that is probably larger. Then write 𝑚 ∥ 𝑀 rather than 𝑀 ∥ 𝑚. These two forms produce the same result, but the 𝑚 ∥ 𝑀 order minimizes surprise: The parallel combination of 𝑚 and 𝑀 is smaller than either mass (Problem 2.17), so it is closer to 𝑚, the smaller mass, than to 𝑀. Writing 𝑚 ∥ 𝑀, rather than 𝑀 ∥ 𝑚, places the most salient information first.

Problem 2.17

Using the resistance analogy

By using the analogy with parallel resistances, explain why 𝑚 ∥ 𝑀 is smaller than 𝑚 and 𝑀.

Why do the two masses combine like resistors in parallel?

The answer lies in the analogy between mass and resistance. Resistance appears in Ohm's law:

voltage = resistance × current.

(2.37)

Voltage is an effort. Current, which results from the effort, is a flow. Therefore, the more general form—one step higher on the abstraction ladder—is effort = resistance × flow.

(2.38)

In this form, Newton's second law,

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

44

2 Abstraction

force = mass × acceleration,

(2.39)

identifies force as the effort, mass as the resistance, and acceleration as the flow.

Because the spring can wiggle either mass, just as current can flow through either of two parallel resistors, the spring feels a resistance equal to the parallel combination of the resistances—namely, 𝑚 ∥ 𝑀.

Problem 2.18

Three springs connected

What is the effective spring constant of three springs connected in a line, with spring constants 2, 3, and 6 newtons per meter, respectively?

2.4.4 Impedance as a higher-level abstraction Resistance, in the electrical sense, has appeared several times, and it underlies a higher-level abstraction: impedance. Impedance extends the idea of electrical resistance to capacitors and inductors. Capacitors and inductors, along with resistors, are the three linear circuit elements: In these elements, the connection between current and voltage is described by a linear equation: For resistors, it is a linear algebraic relation (Ohm's law); for capacitors or inductors, it is a linear differential equation.

Why should we extend the idea of resistance?

Resistors are easy to handle. When a circuit contains only resistors, we can immediately and completely describe how it behaves. In particular, we can write the voltage at any point in the circuit as a linear combination of the voltages at the source nodes. If only we could do the same when the circuit contains capacitors and inductors.

We can! Start with Ohm's law,

voltage

current = resistance,

(2.40)

and look at it in the higher-level and expanded form flow =

1

resistance × effort.

(2.41)

For a capacitor, flow will still be current. But we'll need to find the capacitive analog of effort. This analogy will turn out slightly different from the electrical–mechanical analogy between capacitance and spring constant 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

45

(Section 2.4.1), because now we are making an analogy between capacitors and resistors (and, eventually, inductors). For a capacitor, charge = capacitance × voltage.

(2.42)

To turn charge into current, we differentiate both sides to get current = capacitance × 𝑑(voltage)

𝑑𝑡

.

(2.43)

To make the analogy quantitative, let's apply to the capacitor the simI

plest voltage whose form is not altered by differentiation: V

C

𝑉 = 𝑉0 𝑒𝑗𝜔𝑡,

(2.44)

where 𝑉 is the input voltage, 𝑉0 is the amplitude, 𝜔 is the angular frequency, and 𝑗 is the imaginary unit −1. The voltage 𝑉 is a complex number; but the implicit understanding is that the actual voltage is the real part of this complex number. By finding how the current 𝐼 (the flow) depends on 𝑉 (the effort), we will extend the idea of resistance to a capacitor.

With this exponential form, how can we represent the more familiar oscillating voltages 𝑉1 cos 𝜔𝑡 or 𝑉1 sin 𝜔𝑡 , where 𝑉1 is a real voltage?

Start with Euler's relation:

𝑒𝑗𝜔𝑡 = cos 𝜔𝑡 + 𝑗 sin 𝜔𝑡.

(2.45)

To make 𝑉1 cos 𝜔𝑡, set 𝑉0 = 𝑉1 in 𝑉 = 𝑉0 𝑒𝑗𝜔𝑡. Then 𝑉 = 𝑉1(cos 𝜔𝑡 + 𝑗 sin 𝜔𝑡).

(2.46)

and the real part of 𝑉 is just 𝑉1 cos 𝜔𝑡.

Making 𝑉1 sin 𝜔𝑡 is more tricky. Choosing 𝑉0 = 𝑗𝑉1 almost works: 𝑉 = 𝑗𝑉1(cos 𝜔𝑡 + 𝑗 sin 𝜔𝑡) = 𝑉1(𝑗 cos 𝜔𝑡 − sin 𝜔𝑡).

(2.47)

The real part is −𝑉1 sin 𝜔𝑡, which is correct except for the minus sign. Thus, the correct amplitude is 𝑉0 = −𝑗𝑉1. In summary, our exponential form can compactly represent the more familiar sine and cosine signals.

With this exponential form, differentiation is simpler than with sines or cosines. Differentiating 𝑉 with respect to time just brings down a factor of 𝑗𝜔, but otherwise leaves the 𝑉0 𝑒𝑗𝜔𝑡 alone:

𝑑𝑉

𝑑𝑡 = 𝑗𝜔 × 𝑉0 𝑒𝑗𝜔𝑡

⏟ = 𝑗𝜔𝑉.

(2.48)

𝑉

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

46

2 Abstraction

With this changing voltage, the capacitor equation, current = capacitance × 𝑑(voltage)

𝑑𝑡

,

(2.49)

becomes

current = capacitance × 𝑗𝜔 × voltage.

(2.50)

Let's compare this form to its analog for a resistor (Ohm's law): current =

1

resistance × voltage.

(2.51)

Matching up the pieces, we find that a capacitor offers a resistance 𝑍𝐶 = 1

𝑗𝜔𝐶.

(2.52)

This more general resistance, which depends on the frequency, is called impedance and denoted 𝑍. (In the analogy of Section 2.4.1 between capacitors and springs, we found that capacitor offered a resistance to being charged of 1/𝐶. Impedance, the result of an analogy between capacitors and resistors, contains 1/𝐶 as well, but also contains the frequency in the 1/𝑗𝜔 factor.) Using impedance, we can describe what happens to any sinusoidal signal in a circuit containing capacitors. Our thinking is aided by the compact notation—the capacitive impedance 𝑍𝐶 (or even 𝑅𝐶). The notation hides the details of the capacitor differential equation and allows us to transfer our intuition about resistance and flow to a broader class of circuits.

Vin

Vout

The simplest circuit with resistors and capacitors is the R

so-called low-pass 𝑅𝐶 circuit. Not only is it the sim-C

plest interesting circuit, it will also be, thanks to further analogies, a model for heat flow. Let's apply the ground

impedance analogy to this circuit.

Vin

To help us make and use abstractions, let's imagine defocusing our eyes. Under blurry vision, the capacitor looks like a resistor that just R

happens to have a funny resistance 𝑅𝐶 = 1/𝑗𝜔𝐶. Now the entire cir-Vout

cuit looks just like a pure-resistance circuit. Indeed, it is the simplest RC

such circuit, a voltage divider. Its behavior is described by one number: the gain, which is the ratio of output to input voltage 𝑉

ground

out/𝑉in.

In the 𝑅𝐶 circuit, thought of as a voltage divider, capacitive resistance

gain = total resistance from 𝑉

.

(2.53)

in to ground =

𝑅𝐶

𝑅 + 𝑅𝐶

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

47

Because 𝑅𝐶 = 1/𝑗𝜔𝐶, the gain becomes

1

gain = 𝑗𝜔𝐶 .

(2.54)

𝑅 + 1

𝑗𝜔𝐶

After clearing the fractions by multiplying by 𝑗𝜔𝐶 in the numerator and denominator, the gain simplifies to

gain =

1

1 + 𝑗𝜔𝑅𝐶.

(2.55)

Why is the circuit called a low-pass circuit?

At high frequencies (𝜔 → ∞), the 𝑗𝜔𝑅𝐶 term in the denominator makes the gain zero. At low frequencies (𝜔 → 0), the 𝑗𝜔𝑅𝐶 term disappears and the gain is 1. High-frequency signals are attenuated by the circuit; low-frequency signals pass through mostly unchanged. This abstract, high-level description of the circuit helps us understand the circuit without our getting buried in equations. Soon we will transfer our understanding of this circuit to thermal systems.

The gain contains the circuit parameters as the product 𝑅𝐶. In the denominator of the gain, 𝑗𝜔𝑅𝐶 is added to 1; therefore, 𝑗𝜔𝑅𝐶, like 1, must have no dimensions. Because 𝑗 is dimensionless (is a pure number), 𝜔𝑅𝐶 must be itself dimensionless. Therefore, the product 𝑅𝐶 has dimensions of time.

This product is the circuit's time constant—usually denoted 𝜏.

The time constant has two physical interpretations. To construct them, we imagine charging the capacitor using a constant input voltage 𝑉0; eventually (after an infinite time), the capacitor charges up to the input voltage (𝑉out = 𝑉0) and holds a charge 𝑄 = 𝐶𝑉0. Then, at 𝑡 = 0, we make the input voltage zero by connecting the input to ground.

R

R

Vout

Vout

V0

C

C

ground

ground

𝑡 < 0

𝑡 ≥ 0

The capacitor discharges through the resistor, and its voltage decays exponentially:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

48

2 Abstraction

V0

t = 0

Vout

t = τ

V0/e

ground (V = 0)

τ

After one time constant 𝜏, the capacitor voltage falls by a factor of 𝑒 toward its final value—here, from 𝑉0 to 𝑉0/𝑒. The 1/𝑒 time is our first interpretation of the time constant. Furthermore, if the capacitor voltage had decayed at its initial rate (just after 𝑡 = 0), it would have reached zero voltage after one time constant 𝜏—the second interpretation of the time constant.

The time-constant abstraction hides—abstracts away—the details that produced it: here, electrical resistance and capacitance. Nonelectrical systems can also have a time constant but produce it by a different mechanism.

Our high-level understanding of time constants, because it is not limited to electrical systems, will help us transfer our understanding of the electrical low-pass filter to nonelectrical systems. In particular, we are now ready to understand heat flow in thermal systems.

Problem 2.19

Impedance of an inductor

An inductor has the voltage–current relation 𝑉 = 𝐿𝑑𝐼

𝑑𝑡 ,

(2.56)

where 𝐿 is the inductance. Find an inductor's frequency-dependent impedance 𝑍𝐿. After finding this impedance, you can analyze any linear circuit as if it were composed only of resistors.

2.4.5 Thermal systems

The 𝑅𝐶 circuit is a model for thermal systems—which are not obviously connected to circuits. In a thermal system, temperature difference, the analog of voltage difference, produces a current of energy. Energy current, in less fancy words, is heat flow. Furthermore, the current is proportional to the temperature difference—just as electric current is proportional to voltage difference. In both systems, flow is proportional to effort. Therefore, heat flow can be understood by using circuit analogies.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

49

walls

As an example, I often prepare a cup of tea but forget to Ttea

drink it while it is hot. Like a discharging capacitor, the Rt

tea slowly cools toward room temperature and becomes mug and

Ct

undrinkable. Heat flows out through the mug. Its walls tea

provide a thermal resistance; by analogy to an 𝑅𝐶 cir-Troom

cuit, let's denote the thermal resistance 𝑅t. The heat is stored in the water and mug, which form a heat reservoir. This reservoir, of heat rather than of charge, provides the thermal capacitance, which we denote 𝐶t. (Thus, the mug participates in the thermal resistance and capacitance.) Resistance and capacitance are transferable ideas.

The product 𝑅t𝐶t is, by analogy to the 𝑅𝐶 circuit, the thermal time constant 𝜏. To estimate 𝜏 with a home experiment (the method we used in Section 1.7), heat up a mug of tea; as it cools, sketch the temperature gap between the tea and room temperature. In my extensive experience of tea neglect, an enjoyably hot cup of tea becomes lukewarm in half an hour. To quantify these temperatures, enjoyably warm may be 130 ∘F (≈ 55 ∘C), room temperature is 70 ∘F (≈ 20 ∘C), and lukewarm may be 85 ∘F (≈ 30 ∘C).

130 ◦F (hot tea)

t = 0

0.5 hr

85 ◦F (lukewarm)

70 ◦F (room temperature)

Based on the preceding data, what is the approximate thermal time constant of the mug of tea?

In one thermal time constant, the temperature gap falls by a factor of 𝑒 (just as the voltage gap falls by a factor of 𝑒 in one electrical time constant). For my mug of tea, the temperature gap between the tea and the room started at 60 ∘F:

enjoyably warm

⏟⏟⏟⏟⏟⏟⏟⏟⏟ − room temperature

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ = 60 ∘F.

(2.57)

130 ∘F

70 ∘F

In the half hour while the tea cooled in the microwave, the temperature gap fell to 15 ∘F:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

50

2 Abstraction

lukewarm

⏟⏟⏟⏟⏟ − room temperature

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ = 15 ∘F.

(2.58)

85 ∘F

70 ∘F

Therefore, the temperature gap decreased by a factor of 4 in half an hour.

Falling by the canonical factor of 𝑒 (roughly 2.72) would require less time: perhaps 0.3 hours (roughly 20 minutes) instead of 0.5 hours. A more precise calculation would be to divide 0.5 hours by ln 4, which gives 0.36 hours.

However, there is little point doing this part of the calculation so precisely when the input data are far less precise. Therefore, let's estimate the thermal time constant 𝜏 as roughly 0.3 hours.

Using this estimate, we can understand what happens to the tea mug when, as it often does, it spends a lonely few days in the microwave, subject to the daily variations in room temperature. This analysis will become our model for the daily temperature variations in a house.

How does a teacup with 𝜏 ≈ 0.3 hours respond to daily temperature variations?

walls

First, set up the circuit analogy. The output signal is Troom Ttea

still the tea's temperature. The input signal is the (si-Rt

nusoidally) varying room temperature. However, mug and

Ct

the ground signal, which is our reference tempera-tea

ture, cannot also be the room temperature. Instead, Tavg

we need a constant reference temperature. The simplest choice is the average room temperature 𝑇avg. (After we have transferred this analysis to the temperature variation in houses, we'll see that the conclusion is the same even with a different reference temperature.) The gain connects the amplitudes of the output and input signals: amplitude of the output signal

gain = amplitude of the input signal = 1

1 + 𝑗𝜔𝜏 .

(2.59)

The input signal (room temperature) varies with a frequency 𝑓 of 1 cycle per day. Then the dimensionless parameter 𝜔𝜏 in the gain is roughly 0.1.

Here is that calculation:

𝑓

⏞ cy

⏞ cle

⏞⏞⏞

1 day

2𝜋 × 1 day × 0.3hr ×

≈ 0.1.

(2.60)

⏟⏟⏟⏟⏟⏟⏟ ⏟

24 hr

⏟

𝜔

𝜏

1

The system is driven by a low-frequency signal: 𝜔 is not large enough to make 𝜔𝜏 comparable to 1. As the gain expression reminds us, the mug of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.4 Analogies

51

tea is a low-pass filter for temperature variations. It transmits this low-frequency input temperature signal almost unchanged to the output—to the tea temperature. Therefore, the inside (tea) temperature almost exactly follows the outside (room) temperature.

walls

The opposite extreme is a house. Compared to Toutside Tinside

the mug, a house has a much higher mass and

therefore thermal capacitance. The resulting time house

constant 𝜏 = 𝑅t𝐶t is probably much longer for a house than for the mug. As an example, when

Tavg

I taught in sunny Cape Town, where houses are often unheated even in winter, the mildly insulated house where I stayed had a thermal time constant of approximately 0.5 days.

For this house the dimensionless parameter 𝜔𝜏 is much larger than it was for the tea mug. Here is the corresponding calculation.

𝑓

⏞ cy

⏞ cle

⏞⏞⏞

2𝜋 × 1 day × 0.5 days ≈ 3.

(2.61)

⏟⏟⏟⏟⏟⏟⏟ ⏟⏟⏟⏟⏟

𝜔

𝜏

What consequence does 𝜔𝜏 ≈ 3 have for the indoor temperature?

In the Cape Town winter, the outside temperature varied daily between 45 ∘F and 75 ∘F; let's also assume that it varied approximately sinusoidally.

This 30 ∘F peak-to-peak variation, after passing through the house low-pass filter, shrinks by a factor of approximately 3. Here is how to find that factor by estimating the magnitude of the gain.

amplitude of

∣gain∣ = ∣

𝑇inside

amplitude of 𝑇

∣ = ∣

1

outside

1 + 𝑗𝜔𝜏 ∣ .

(2.62)

(It is slightly confusing that the outside temperature is the input signal, and the inside temperature is the output signal!) Now plug in 𝜔𝜏 ≈ 3 to get

∣gain∣ ≈ ∣ 1

1 + 3𝑗∣ =

1

≈ 1

12 + 32

3.

(2.63)

In general, when 𝜔𝜏 ≫ 1, the magnitude of the gain is approximately 1/𝜔𝜏.

Therefore, the outside peak-to-peak variation of 30 ∘F becomes a smaller inside peak-to-peak variation of 10 ∘F. Here is a block diagram showing this effect of the house low-pass filter.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

52

2 Abstraction

house as a

30 ◦F

low-pass filter

10 ◦F

(2.64)

Our comfort depends not only on the temperature variation (I like a fairly steady temperature), but also on the average temperature.

What is the average temperature indoors?

It turns out that the average temperature indoors is equal to the average temperature outdoors! To see why, let's think carefully about the reference temperature (our thermal analog of ground). Before, in the analysis of the forgotten tea mug, our reference temperature was the average indoor temperature. Because we are now trying to determine this value, let's instead use a known convenient reference temperature—for example, the cool 10 ∘C, which makes for round numbers in Celsius or Fahrenheit (50 ∘F).

The input signal (the outside temperature) varied in winter between 45 ∘F

and 75 ∘F. Therefore, it has two pieces: (1) our usual varying signal with the 30 ∘F peak-to-peak variation, and (2) a steady signal of 10 ∘F.

75 ◦F

15 ◦F

60 ◦F

10 ◦F

60 ◦F

=

0 ◦F

+ 50◦F

(2.65)

(reference temp.)

45 ◦F

⏟⏟⏟⏟⏟⏟⏟⏟⏟

−15 ◦F

⏟⏟⏟⏟⏟⏟⏟⏟⏟

⏟⏟⏟⏟⏟⏟⏟⏟⏟

full signal

varying piece

steady piece

The steady signal is the difference between the average outside temperature of 60 ∘F and the reference signal of 50 ∘F.

Let's handle each piece in turn—we are using divide-and-conquer reasoning again. We just analyzed the varying piece: It passes through the house low-pass filter and, with 𝜔𝜏 ≈ 3, it shrinks significantly in amplitude. In contrast, the nonvarying part, which is the average outside temperature, has zero frequency by definition. Therefore, its dimensionless parameter 𝜔𝜏 is exactly 0. This signal passes through the house low-pass filter with a gain of 1. As a result, the average output signal (the inside temperature) is also 60 ∘F: the same steady 10 ∘F signal measured relative to the reference temperature of 50 ∘F.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.5 Summary and further problems 53

The 10 ∘F peak-to-peak inside-temperature amplitude is a variation around 60 ∘F. Therefore, the inside temperature varies between 55 ∘F and 65 ∘F

(13 ∘C to 18 ∘C). Indoors, when I am not often running or otherwise generating much heat, I feel comfortable at 68 ∘F (20 ∘C). So, as this circuit model of heat flow predicts, I wore a sweater day and night in the Cape Town house. (For more on using 𝑅𝐶 circuit analogies for building design, see the

「Design masterclass」article by Doug King [30].) Problem 2.20

When is the house coldest?

Based on the general form for the gain, 1/(1+𝑗𝜔𝜏), when in the day will the Cape Town house be the coldest, assuming that the outside is coldest at midnight?

2.5 Summary and further problems

Geometric means, impedances, low-pass filters—these ideas are all abstractions. An abstraction connects seemingly random details into a higher-level structure that allows us to transfer knowledge and insights. By building abstractions, we amplify our intelligence.

Indeed, each of our reasoning tools is an abstraction or reusable idea. In Chapter 1, for example, we learned how to split hard problems into tractable ones, and we named this process divide-and-conquer reasoning. Don't stop with this one process. Whenever you reuse an idea, identify the transferable process, and name it: Make an abstraction. With a name, you will recognize and reuse it.

Problem 2.21

From circles to spheres

In this problem, you first find the area of a circle from its circumference and then use analogous reasoning to find the volume of a sphere.

a. Divide a circle of radius 𝑟 into pie wedges. Then snip and unroll the circle: r

→

(2.66)

b b

· · ·

b

Use the unrolled picture and the knowledge that the circle's circumference is 2𝜋𝑟 to show that its area is 𝜋𝑟2.

b. Now extend the argument to a sphere of radius 𝑟: Find its volume given that its surface area is 4𝜋𝑟2. (This method was invented by the ancient Greeks.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

54

2 Abstraction

Problem 2.22

Gain of an LRC circuit

Use the impedance of an inductor (Problem 2.19) to L

C

find the gain of the classic 𝐿𝑅𝐶 circuit. In this con- Vin Vout

figuration, in which the output voltage measured R

across the resistor, is the circuit a low-pass filter, a high-pass filter, or a band-pass filter?

ground

Problem 2.23

Continued fraction

Evaluate the continued fraction

1 +

1

.

(2.67)

1 + 1

1+…

Compare this problem with Problem 2.8.

Problem 2.24

Exponent tower

Evaluate

2 2 2⋅⋅⋅.

(2.68)

Here, 𝑎𝑏𝑐 means 𝑎(𝑏𝑐).

Problem 2.25

Coaxial cable termination

In physics and electronics laboratories around the world, the favorite way to connect equipment and transmit signals is with coaxial cable. The standard coaxial cable, RG-58/U, has a capacitance per length of 100 picofarads per meter and an inductance per length of 0.29 microhenries per meter. It can be modeled as a long inductor–capacitor ladder:

L

L

L

L

C

C

C

. . .

C

What resistance 𝑅 placed at the end (in parallel with the last capacitor) makes the cable look like an infinitely long 𝐿𝐶 cable?

Problem 2.26

UNIX and Linux

Using Mike Gancarz's The UNIX Philosophy [17] and Linux and the Unix Philosophy [18], find examples of abstraction in the design and philosophy of the UNIX

and Linux operating systems.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

## Part II Discarding complexity without losing information

You've divided your hard problems into manageable pieces. You've found transferable, reusable ideas. When these tools are not enough and problems are still too complex, you need to discard complexity—the theme of our next three tools. They help us discard complexity without losing information. If a system contains a symmetry (Chapter 3)—or what is closely related, it is subject to a conservation law—using the symmetry greatly simplifies the analysis. Alternatively, we often do not care about a part of an analysis, because it is the same for all the objects in the analysis. To ignore those parts, we use proportional reasoning (Chapter 4). Finally, we can ensure that our equations do not add apples to oranges. This simple idea—dimensional analysis (Chapter 5)—greatly shrinks the space of possible solutions and helps us master complexity.

to master complexity

organize it

discard it

Part I

without losing information

losing information

1

2

Part II

Part III

symmetry and

proportional

dimensional

conservation

reasoning

analysis

6

7

8

9

3

4

5

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3

Symmetry and conservation

3.1 Invariants

57

3.2 From invariant to symmetry operation

66

3.3 Physical symmetry

73

3.4 Box models and conservation

75

3.5 Drag using conservation of energy

84

3.6 Lift using conservation of momentum

93

3.7 Summary and further problems
