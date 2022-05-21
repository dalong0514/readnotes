276

Our previous tool, lumping, helps us simplify by discarding less important information. Our next tool, probabilistic reasoning, helps us when our information is already incomplete—when we've discarded even the chance or the wish to collect the missing information.

7.1 Probability as degree of belief: Bayesian probability The essential concept in using probability to simplify the world is that probability is a degree of belief. Therefore, a probability is based on our knowledge, and it changes when our knowledge changes.

7.1.1 Is it my telephone number?

Here is an example from soon after I had moved to England. I was talking to a friend on the phone, of the old-fashioned variety with wires connecting it to the wall. David needed to call me back. However, having just moved to the apartment, I was unsure of my phone number; plus, for anyone used to American phone numbers, British phone numbers have a strange and hard-to-remember format. I had a reasonably likely guess, which I gave David so that he could call me back. After I hung up, I tested my guess by picking up my phone and dialing my guess—and got a busy signal.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

236

7 Probabilistic reasoning

Given this experimental evidence, how sure am I that the candidate number is my phone number? Quantitatively, what odds should I give?

This question makes no sense if probability is seen as long-run frequency.

In that view, the probability of a coin turning up heads is 1/2 because 1/2

is the limiting proportion of heads in an ever-longer series of tosses. However, for evaluating the plausibility of the phone number, this interpretation—called the frequentist interpretation—cannot apply, because there is no repeated experiment.

The frequentist interpretation gets stuck because it places probability in the physical system itself. The alternative—that probability reflects the incompleteness of our knowledge—is known as the Bayesian interpretation of probability. It is the interpretation suited for mastering complexity. A book-length discussion and application of this fundamental point is Edwin Jaynes's Probability Theory: The Logic of Science [26].

The Bayesian interpretation is based on one simple idea: A probability reflects our degree of belief in a hypothesis. Probabilities are therefore subjective: Someone with different knowledge will have different probabilities. Thus, by collecting evidence, our degrees of belief change. Evidence changes probabilities.

In the phone-number problem, what is the hypothesis and what is the evidence?

The hypothesis—often denoted 𝐻—is the statement about the world whose credibility we would like to judge. Here,

𝐻 ≡ My phone-number guess is correct.

(7.1)

The evidence—often denoted 𝐸 or 𝐷 (for data)—is the information that we collect, obtain, or learn and then use to judge the hypothesis. It augments our knowledge. Here, 𝐸 is the result of the experiment: 𝐸 ≡ Dialing my guess gave a busy signal.

(7.2)

Any hypothesis has an initial probability Pr (𝐻). This probability is called the prior probability, because it is the probability prior to, or before, incorporating the evidence. After learning the evidence 𝐸, the hypothesis has a new probability Pr (𝐻 ∣ 𝐸): the probability of the hypothesis 𝐻 given—that is, upon assuming—the evidence 𝐸. This probability is called the posterior probability, because it is the probability, or degree of belief, after including the evidence.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.1 Probability as degree of belief: Bayesian probability 237

The recipe for using evidence to update probabilities is Bayes' theorem: Pr (𝐻 ∣ 𝐸) ∝ Pr (𝐻) × Pr (𝐸 ∣ 𝐻).

(7.3)

The new factor, the probability Pr (𝐸 ∣ 𝐻)—the probability of the evidence given the hypothesis—is called the likelihood. It measures how well the candidate theory (the hypothesis) explains the evidence. Bayes' theorem then says that

posterior probability

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ ∝ prior probability

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × explanatory power.

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ (7.4)

Pr(𝐻 | 𝐸)

Pr(𝐻)

Pr(𝐸 | 𝐻)

(The constant of proportionality is chosen so that the posterior probabilities for all the competing hypotheses add to 1.) Both probabilities on the right are necessary. Without the likelihood, we could not change our probabilities. Without the prior probability, we would always prefer the hypothesis with the maximum likelihood, no matter how contrived or post hoc.

In a frequent use of Bayes' theorem, there are only two hypotheses, 𝐻 and its negation 𝐻. In this problem, 𝐻 is the statement that my guess is wrong.

With only two hypotheses, a compact form of Bayes' theorem uses odds instead of probabilities, thereby avoiding the constant of proportionality: Pr (𝐸 ∣ 𝐻)

posterior odds

⏟⏟⏟⏟⏟⏟⏟⏟⏟ = prior odds

⏟⏟⏟⏟⏟⏟⏟ ×

.

(7.5)

Pr (𝐸 ∣ 𝐻)

O(𝐻 | 𝐸)

O(𝐻)

The odds 𝑂 are related to the probability 𝑝 by 𝑂 = 𝑝/(1 − 𝑝). For example, a probability of 𝑝 = 2/3 corresponds to an odds of 2—often written as 2:1

and read as「2-to-1 odds.」

Problem 7.1

Converting probabilities to odds

Convert the following probabilities to odds: (a) 0.01, (b) 0.9, (c) 0.75, and (d) 0.3.

Problem 7.2

Converting odds to probabilities

Convert the following odds to probabilities: (a) 3, (b) 1/3, (c) 1:9, and (d) 4-to-1.

The ratio Pr (𝐸 ∣ 𝐻)/Pr (𝐸 ∣ 𝐻) is called the likelihood ratio. Its numerator measures how well the hypothesis 𝐻 explains the evidence 𝐸; its denominator measures how well the contrary hypothesis 𝐻 explains the same evidence. So their ratio measures the relative explanatory power of the two hypotheses. Bayes' theorem, in the odds form, is simple: updated odds = initial odds × relative explanatory power.

(7.6)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

238

7 Probabilistic reasoning

Let's use Bayes' theorem to judge my phone-number guess. Before the experiment, I was not too sure of the phone number; Pr (𝐻) is perhaps 1/2, making O(𝐻) = 1. In the likelihood ratio, the numerator Pr (𝐸 ∣ 𝐻) is the probability of getting a busy signal assuming (「given」) that my guess is correct. Because I would be dialing my own phone using my phone, I would definitely get a busy signal. Thus, Pr (𝐸 ∣ 𝐻) = 1: The hypothesis of a correct guess (𝐻) explains the data as well as possible.

The trickier estimate is the denominator Pr (𝐸 ∣ 𝐻): the probability of getting a busy signal assuming that my guess is incorrect. I'll assume that my guess is still a valid phone number (I nowadays rarely get the recorded mes-sage saying that I have dialed an invalid number). Then I would be dialing a random person's phone. Thus, Pr (𝐸 ∣ 𝐻) is the probability that a random valid phone is busy. It is probably similar to the fraction of the day that my own phone is busy. In my household, the phone is in use for 0.5 hours in a 24-hour day, and the busy fraction could be 0.5/24.

However, that estimate uses an overly long time, 24 hours, for the denominator. If I do the experiment at 3 am and my guess is wrong, I would wake up an innocent bystander. Furthermore, I am not often on the phone at 3 am. A more reasonable denominator is 10 hours (9 am to 7 pm), making the busy fraction and the likelihood Pr (𝐸 ∣ 𝐻) roughly 0.05. An incorrect guess (𝐻) is a lousy explanation for the data.

The relative explanatory power of 𝐻 and 𝐻, which is measured by the likelihood ratio, is roughly 20:

Pr (𝐸 ∣ 𝐻) ∼ 1

Pr (𝐸 ∣ 𝐻)

0.05 = 20.

(7.7)

Because the prior odds were 1 to 1, the updated, posterior odds are 20 to 1: posterior odds

⏟⏟⏟⏟⏟⏟⏟⏟⏟ = prior odds

⏟⏟⏟⏟⏟⏟⏟ × likelihood ratio

⏟⏟⏟⏟⏟⏟⏟⏟⏟ ∼ 20.

(7.8)

O(𝐻|𝐸)∼20

O(𝐻)∼1

Pr(𝐸 | 𝐻) / Pr(𝐸 | 𝐻) ∼ 20

My guess has become very likely—and it turned out to be correct.

Problem 7.3

PKU testing

In most American states and many countries, newborn babies are tested for the metabolic defect phenylketonuria (PKU). The prior odds of having PKU are about 1 in 10 000. The test gives a false-positive result 0.23 percent of the time; it gives a false-negative result 0.3 percent of the time. What are Pr (PKU ∣ positive test) and Pr (PKU ∣ negative test)?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.2 Plausible ranges: Why divide and conquer works 239

7.2 Plausible ranges: Why divide and conquer works The Bayesian understanding of probability as degree of belief will show us why divide-and-conquer reasoning (Chapter 1) works. We'll see how it increases our confidence in an estimate and decreases our uncertainty as we analyze a divide-and-conquer estimate in slow motion.

7.2.1 Land area of the United Kingdom

The estimate will be the land area of the United Kingdom, which is where I was born and later spent many years. So I have some implicit knowledge of the area, but I don't know it explicitly. The estimate therefore serves as a model for the common situation where we know more than we think we do and need to bring out and use that knowledge.

To make the initial estimate, the baseline against which to compare the divide-and-conquer estimate, I talk to my gut using the rubric of Section 1.6.

For the lower end of my range, 104 square kilometers feels right: I would be fairly surprised if the area were smaller. For the upper end, 107 square kilometers feels right: I would be fairly surprised if the area were larger.

Combining the endpoints, I would be mildly surprised if the area were smaller than 104 square kilometers or greater than 107 square kilometers.

The wide range, spanning three orders of magnitude, reflects the difficulty of estimating an area without using divide-and-conquer reasoning.

My confidence in the gut estimate is my probability for the hypothesis 𝐻: 𝐻 ≡ The UK's land area lies in the range 104…107 km2.

(7.9)

This probability assumes, or is based on, my background knowledge 𝐾: 𝐾 ≡ what I know about the area before using divide and conquer. (7.10) My confidence or degree of belief in the guess is the conditional probability Pr (𝐻 ∣ 𝐾): the probability that the area lies in the range, based on my knowledge before applying divide-and-conquer reasoning. Alas, no algorithm is known for computing a probability based on such complicated background information. The best that we can do is to introspect: to hold a further gut discussion. This discussion concerns not the area itself, but rather the degree of belief about the range 104…107 square kilometers.

My gut chose the range for which I would feel mild surprise, but not shock, to learn that the area lies outside it. The surprise implies that the probability Pr (𝐻 ∣ 𝐾) is larger than 1/2: If Pr (𝐻 ∣ 𝐾) were less than 1/2, I would be 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

240

7 Probabilistic reasoning

surprised to find the area inside the range. The mildness of the surprise suggests that Pr (𝐻 ∣ 𝐾) is not much larger than 1/2. The probability feels like 2/3. The corresponding odds are 2:1; I'd give 2-to-1 odds that the area lies within the plausible range. With a further assumption of symmetry, so that the area's falling below and above the range are equally likely, the plausible range represents the following probabilities: 104 km2

107 km2

plausible range

p ≈ 1/6

p ≈ 2/3

p ≈ 1/6

where the wavy lines at the ends indicate that the left and right ranges extend down to zero and up to infinity, respectively.

Now let's see how a divide-and-conquer estimate changes the plausible range. To make this estimate, lump the area into a rectangle with the same area and aspect ratio as the United Kingdom. My own best-guess rectangle is super-imposed on the map outline of the United Kingdom. Its area is the product of its width and height. Then the area estimate divides into two simpler estimates.

UK

1. Lumped width. Before I ask my gut for the plausible height

Ireland

range for the width, I prepare by reviewing my knowledge of the width. Crossing the United Kingdom in the south, say from London to Cornwall, takes maybe width

4 hours by car. But much of the United Kingdom is thinner, so the average, or lumped, width corresponds to maybe 3 hours of driving. My gut is content with the range 150…250 miles or 240…400 kilometers: 240 km

400 km

plausible range

p ≈ 1/6

p ≈ 2/3

p ≈ 1/6

On a logarithmic scale, which is the correct scale for positive quantities such as the width and height, the midpoint of the range is 240 × 400

or 310 kilometers. It is my best estimate of the width.

2. Lumped height. The train journey from London in the south of England to Edinburgh in Scotland, in the northern part of the United Kingdom, takes about 5 hours at, say, 80 miles per hour. In addition to these 400

miles, there's more latitude in Scotland north of Edinburgh and some in England south of London. Thus, my gut estimate for the height of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.2 Plausible ranges: Why divide and conquer works 241

the lumping rectangle is 500 miles. This distance is the midpoint of my plausible range for the height.

The estimate feels accurate to plus or minus 20 percent (roughly ±100

miles). On a logarithmic (or multiplicative) scale, the range would be roughly a factor of 1.2 on either side of midpoint: 420

⏟ … 600

⏟ miles.

(7.11)

500/1.2

500×1.2

(A more accurate value for 500/1.2 is 417, but there's little reason to strive for such accuracy when these endpoints are rough estimates anyway.) In metric units, the range is 670…960 kilometers, with a midpoint of 800 kilometers. Here is its probability interpretation: 670 km

960 km

plausible range

p ≈ 1/6

p ≈ 2/3

p ≈ 1/6

400 km

The next step is to combine the plausible ranges for the height and the width in order to make the plausible range for the area. A first Amax

approach, because the area is the product of the width and height, is simply to multiply the endpoints of the width and height ranges: 240km A

𝐴

min

min ≈ 240 km × 670 km ≈ 160 000 km2;

(7.12)

km

𝐴max ≈ 400 km × 960 km ≈ 380 000 km2.

960

km

The geometric mean (the midpoint) of these endpoints is 250 000

670

square kilometers.

Although reasonable, this approach overestimates the width of the plausible range—a mistake that we'll correct shortly. However, even this overestimated range spans only a factor of 2.4, whereas my starting range of 104…107 square kilometers spans a factor of 1000. Divide-and-conquer reasoning has significantly narrowed my plausible range by replacing a quantity about which I have vague knowledge, namely the area, with quantities about which I have more precise knowledge.

The second bonus is that subdividing into many quantities carries only a small penalty, smaller than suggested by simply multiplying the endpoints.

Multiplying the endpoints produces a range whose width is the product of the two widths. But this width assumes the worst. To see how, imagine an extreme case: estimating a quantity that is the product of ten independent factors, each of which you know to within a factor of 2 (in other words, each 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

242

7 Probabilistic reasoning

plausible range spans a factor of 4). Does the plausible range for the final quantity span a factor of 410 (approximately 106)? That conclusion is terribly pessimistic. More likely, several of the ten estimates will be too large and several will be too small, allowing many errors to cancel.

Correctly computing the plausible range for the area requires a complete probabilistic description of the plausible ranges for the width and height.

With it we could compute the probability of each possible product. That description is, somewhere, available to the person giving the range. But no one knows how to deduce such a complete set of probabilities based on the complex, diffuse, and seemingly contradictory information lodged in a human mind.

A simple solution is to specify a reasonable probability distribution. We'll use the log-normal distribution. This choice means that, on a logarithmic scale, the probability distribution is a normal distribution, also known as a Gaussian distribution.

Here's the log-normal distribution for my gut estimate of the height of the UK lumping rectangle. The horizontal axis is logarithmic: Distances correspond to ratios p ≈ 23

rather than differences. Therefore, 800 rather than 815

kilometers lies halfway between 670 and 960 kilometers.

670

800

960 h (km)

These endpoints are a factor of 1.2 smaller or larger than the midpoint. The peak at 800 kilometers reflects my belief that 800 kilometers is the best guess. The shaded area of 2/3 quantifies my confidence that the true height lies in the range 670…960 kilometers.

We use the log-normal distribution for several reasons. First, our mental hardware compares quantities using ratio rather than absolute difference.

(By「quantity,」I mean inherently positive values, such as distance, rather than signed values such as position.) In short, our hardware places quantities on a logarithmic scale. To represent our thinking, we therefore place the distribution on a logarithmic scale.

Second, the normal distribution, which has only two parameters (midpoint and width), is simple to describe. This simplicity helps us when we translate our internal gut knowledge into the distribution's parameters. From our gut estimates of the lower and upper endpoints, we just find the corresponding midpoint and width (on a logarithmic scale!): The midpoint is the geometric mean of the two endpoints, and the width is the square root of the ratio between the upper and lower endpoints.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.2 Plausible ranges: Why divide and conquer works 243

Third, normal distributions combine simply. When we add two quantities represented by a normal distribution, their sum is also represented by a normal distribution.

On the other hand, the normal distribution does not represent all aspects of our gut knowledge. In particular, the tails of the normal distribution are too thin, reflecting an unrealistically high confidence that our estimate does not contain a huge error. Fortunately, for our analyses, this problem is not so significant, because we will concern ourselves with the location and width of the central region, and not take the thin tails too seriously. With that caveat, we'll represent our plausible range as a normal distribution on a logarithmic scale: a log-normal distribution.

Here is the other log-normal distribution, for the width of the UK lumping rectangle. The shaded range is the so-called one-sigma range 𝜇−𝜎 to 𝜇+𝜎, where 𝜇 is the p ≈ 23

midpoint (here, 310 kilometers) and 𝜎 is the width, measured as a distance on a logarithmic scale. In a normal 240

310

400 w (km)

distribution, the one-sigma range contains 68 percent of the probability—conveniently close to 2/3. When we ask our plausible ranges to contain a 2/3 probability, we are estimating a one-sigma range.

The two log-normal distributions supply the probabilistic description required to combine the plausible ranges. The rules of probability theory (Problem 7.5) produce the following two-part recipe.

1. The midpoint of the plausible range for the area 𝐴 is the product of the midpoint of the plausible ranges for ℎ and 𝑤. Here, the height midpoint is 800 kilometers and the width midpoint is 310 kilometers, so the area midpoint is roughly 250 000 square kilometers: 800

⏟⏟ km

⏟⏟⏟ × 310

⏟⏟ km

⏟⏟⏟ ≈ 250 000 km2.

(7.13)

ℎ

𝑤

2. To compute the plausible range's width or half width, first express the individual half widths (the 𝜎 values) in logarithmic units. Convenient units include factors of 10, also known as bels, or the even-more-convenient decibels. A decibel, whose abbreviation is dB, is one-tenth of a factor of 10. Here is the conversion between a factor 𝑓 and decibels: number of decibels = 10 log10 𝑓.

(7.14)

For example, a factor of 3 is close to 5 decibels (because 3 is almost one-half of a power of ten), and a factor of 2 is almost exactly 3 decibels.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

244

7 Probabilistic reasoning

(These decibels are slightly more general than the acoustic decibels introduced in Problem 3.10: Acoustic decibels measure energy flux relative to a reference value, usually 10−12 watts per square meter. Both kinds of decibels measure factors of 10, but the decibels here have no implicit reference value.)

In decibels, bels, or any logarithmic unit, the half width (the 𝜎) of the product's range is the Pythagorean sum range

range

's

of the individual half widths (the

A's

𝜎 values). Using 𝜎

h

𝑥

of

of

to represent the half width of the plausible range for width

the quantity 𝑥, the recipe is

width

width of w's range

𝜎𝐴 = 𝜎2ℎ + 𝜎 2𝑤.

(7.15)

Let's apply this recipe to our example. The plausible range for the height (ℎ) was 800 kilometers give or take a factor of 1.2. On a logarithmic scale, distances are measured by ratios or factors, so think of a range as「give or take a factor of」rather than as「plus or minus」(a description that would be appropriate on a linear scale). A factor of 1.2 is about ±0.8 decibels: 10 log10 1.2 ≈ 0.8.

(7.16)

Therefore, 𝜎ℎ ≈ 0.8 decibels.

The plausible range for the width (𝑤) was roughly 310 kilometers give or take a factor of 1.3. A factor of 1.3 is ±1.1 decibels: 10 log10 1.3 ≈ 1.1.

(7.17)

Therefore, 𝜎𝑤 ≈ 1.1 decibels.

The Pythagorean sum of 𝜎ℎ and 𝜎𝑤 is approximately 1.4 decibels: 0.82 + 1.12 ≈ 1.4.

(7.18)

As a factor, 1.4 decibels is, coincidentally, approximately a factor of 1.4: 101.4/10 ≈ 1.4.

(7.19)

Because the midpoint of the plausible range is 250 000 kilometers, the UK

land area should be 250 000 square kilometers give or take a factor of 1.4.

Retaining a bit more accuracy, it is a factor of 1.37.

180

⏟⏟ 000

⏟⏟⏟ … 250

⏟⏟ 000

⏟⏟⏟ … 340

⏟⏟ 000

⏟⏟⏟ km2.

(7.20)

/1.37

midpoint

×1.37

As a probability bar, the range is

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.2 Plausible ranges: Why divide and conquer works 245

180 000 km2

250 000 km2

340 000 km2

p ≈ 1/6

p ≈ 2/3

p ≈ 1/6

The true area is 243 610 square kilometers. This area is comfortably in my predicted range and surprisingly close to the midpoint.

How surprising is the accuracy of the estimate?

The surprise can be quantified with a probability: the probability that the true value would be closer to the midpoint (the best estimate) than 243 610

square kilometers is. Here, 243 610 is 2.6 percent or a factor of 1.026 smaller than 250 000. The probability that the true value would be within a factor of 1.026 (on either side) of the midpoint is the tiny shaded region of the log-normal distribution.

180

250

340 A (103 km2)

The region is almost exactly a rectangle, so its area is approximately its height multiplied by its width. The height is the peak height of a normal distribution. In 𝜎 = 1 units (in dimensionless form), this height is 1/ 2𝜋 .

The width of the shaded region, also in 𝜎 = 1 units, is the ratio dB equivalent for a factor of

2 ×

1.026

dB equivalent for a factor of 1.37 ,

(7.21)

which is approximately 0.16. (The factor of 2 arises because the region extends equally on both sides of the peak.) Therefore, the shaded probability is approximately 0.16/ 2𝜋 or only 0.07. I am surprised, but encouraged, by the high accuracy of my estimate for the UK's land area. Once again, many individual errors—for example, in estimating journey times and speeds—have canceled out.

Problem 7.4

Volume of a room

Estimate the volume of your favorite room, comparing your plausible ranges before and after using divide-and-conquer reasoning.

Problem 7.5

Justifying the recipe for combining ranges Use Bayes' theorem to justify the recipe for combining plausible ranges.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

246

7 Probabilistic reasoning

Problem 7.6

Practice combining plausible ranges

You are trying to estimate the area of a rectangular field. Your plausible ranges for its width and length are 1…10 meters 10…100 meters, respectively.

a. What are the midpoints of the two plausible ranges?

b. What is the midpoint of the plausible range for the area?

c. What is the too-pessimistic range for the area, obtained by multiplying the corresponding endpoints?

d. What is the actual plausible range for the area, based on combining log-normal distributions? This range should be narrower than the pessimistic range in part (c)!

e. How do the results change if the ranges are instead 2…20 meters for the width and 20…200 meters for the length?

Problem 7.7

Area of A4 paper

If you have a sheet of standard European (A4) paper handy, either in reality or mentally, find your plausible range for its area 𝐴 by gut estimating its length and width (without using a ruler). Then compare your best estimate (the midpoint of your range) to the official area of A𝑛 paper, which is 2−𝑛 square meters.

Problem 7.8

Estimating a mass

In trying to estimate the mass of an object, your plausible range for its density is 1…5 grams per cubic centimeter and for its volume is 10…50 cubic centimeters.

What is (roughly) your plausible range for its mass?

Problem 7.9

Which is the wider range?

Suppose that your knowledge of the quantities 𝑎, 𝑏, and 𝑐 is given by these plausible ranges:

𝑎 = 1…10

𝑏 = 1…10

(7.22)

𝑐 = 1…10.

Which quantity—𝑎𝑏𝑐 or 𝑎2𝑏—has the wider plausible range?

Problem 7.10

Handling division

If a quantity 𝑎 has the plausible range 1…4, and the quantity 𝑏 has the plausible range 10…40, what are the plausible ranges for 𝑎𝑏 and for 𝑎/𝑏?

7.2.2 Finding one-sigma endpoints before the midpoint With our understanding of probability, we can explain two curious and seemingly arbitrary features of how we make gut estimates (Section 1.6).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.2 Plausible ranges: Why divide and conquer works 247

First, we learned not to ask our gut about its best estimate. Rather, we ask about its lower and upper endpoints, from which we find the best estimate as their midpoint. Second, in finding the endpoints, the standard we use is「mildly surprised」: We should be mildly surprised if the true value lies outside the endpoints. Quantitatively,「mild surprise」now means that the probability should 2/3 that the true value lies between the endpoints.

zero slope

The first feature, that we estimate the endpoints rather than the midpoint directly, is explained by the shape of the log-normal distribution. Imag-p ≈ 2

ine trying to locate its midpoint by offering your 3

gut candidate midpoints. The distribution is flat µ − σ

µ

µ + σ

at the midpoint, so the probability hardly varies as the candidates change. Thus, your gut will answer with almost identical sensations of ease over a wide range around the midpoint. As a result, you cannot easily extract a decent midpoint estimate.

The solution to this problem explains the second curious feature: why the plausible range should enclose a probability of 2/3. The solution is to estimate the location of the steepest places on the curve. Those spots are the points of maximum slope (in absolute value). Around these values, the probability changes most rapidly and so does the sensation of ease.

If we use the most convenient logarithmic units, max. slope

max. slope

where the midpoint 𝜇 is 0 and the half width 𝜎 is 1, then the log-normal distribution becomes the p ≈ 23

reasonably simple form

µ − σ

µ

µ + σ

𝑝(𝑥) = 1 𝑒−𝑥2/2,

(7.23)

2𝜋

where 𝑥 measures half widths away from the peak. Its slope 𝑝′(𝑥) is a maximum where the derivative of 𝑝′(𝑥), namely 𝑝″(𝑥), is zero. These points are also called the inflection or zero-curvature points. (Where the curvature is zero, the curve is straight, so the dashed tangent lines pass through it.) p0(x)

Ignoring dimensionless prefactors,

𝑝′(𝑥) ∼ −𝑥𝑒−𝑥2/2;

−1

0

+1

(7.24)

p00(x)

𝑝″(𝑥) ∼ (𝑥2 − 1)𝑒−𝑥2/2.

The second derivative is zero when 𝑥 = ±1. This value is expressed in the 𝜇 = 0, 𝜎 = 1 system of units. In the usual system, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

248

7 Probabilistic reasoning

𝑥 = ±1 means the one-sigma points 𝜇 ± 𝜎. So the points of maximum (absolute) slope—the points that our gut can most accurately estimate—are the one-sigma points! We find them first and then find their midpoint.

When we estimate a 2/3-probability range, we are finding a one-sigma range almost exactly: In a normal or log-normal distribution, the one-sigma range contains approximately 68 percent of the probability, which is almost exactly 2/3. For comparison, the two-sigma range contains approximately 95 percent of the probability, which is a popular number in statistical analysis. Therefore, you may also want to find your two-sigma range (Problem 7.11). However, the slope at the two-sigma points is approximately a factor of 2.2 smaller than the slope at the one-sigma endpoints, so the two-sigma range is somewhat harder to estimate than is the one-sigma range. To find the two-sigma range, first estimate the one-sigma range, and then double its width (on a log scale).

This analysis of plausible ranges concludes our introduction to probability and the probabilistic basis of divide-and-conquer reasoning. We have learned that probabilities result from the incompleteness of our knowledge, and how acquiring knowledge changes our probabilities. In the next sec-tions, we will use probability to master the complexity of systems with vast numbers of atoms and molecules, where complete knowledge would be impossible. The analysis begins with a special walk, the random walk.

Problem 7.11

Two-sigma range

My one-sigma range for the UK's land area is 180 000…340 000 square kilometers.

What is the two-sigma range?

Problem 7.12

Gold or banknotes?

Having broken into a bank vault, do you take the banknotes or the gold? Assume that your capacity to carry loot is limited by mass rather than by volume.

a. Estimate gold's value density (monetary value per mass)—for example, in dollars per gram. Give plausible ranges for your subestimates and find the resulting plausible range for the value density.

b. For your favorite banknote, give your plausible range for its value density and for the ratio

value density of gold

value density of the banknote .

(7.25)

c. Should you take the gold or the banknotes? Use a table of the normal distribution to evaluate the probability that your choice is correct.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 249

7.3 Random walks: Viscosity and heat flow The great mathematician George Pólya, later to become author of How to Solve It [38], was staying at a bed and breakfast in his adopted country of Switzerland and walking daily in the garden between its tall hedge rows.

He kept running into a newlywed couple taking their walk. Were they following him, or was it a mathematical necessity? From this question was born the study of random walks.

synaptic cleft

Random walks are everywhere. In the card game War, 20 nm

cards wander between two players, until one player gets the whole deck. How long does the game last, on average? A molecule of neurotransmitter is released vesicle

muscle

from a synaptic vesicle. It wanders in the 20-nanometer gap, the synaptic cleft, until it binds to a muscle cell; then your leg muscle twitches. How long does the molecule's journey take? On a winter day, you stand outside wearing only a thin layer of clothing, and your body heat wanders through the clothing. How much heat do you lose? And why do large organisms have circulatory systems?

Answering these questions requires understanding random walks.

7.3.1 Behavior of random walks: Lumping and probabilistic reasoning For our first random walk, imagine a perfume molecule wandering in a room, moving in a straight line until collisions with air molecules deflect it in a random direction. This randomness reflects our incomplete knowledge: Knowing the complete state of the colliding molecules, we could calculate their paths after the collision (at least, in classical physics). However, we do not have that knowledge and do not want it!

Even without that information, the random motion of one molecule is still complicated. The complexity arises from the generality—that the direction of travel and the distance between collisions can have any value. To simplify, we'll lump in several ways.

Distance. Let's assume that the molecule travels a typical, fixed distance between collisions. This distance is the mean free path 𝜆.

Direction. Let's assume that the molecule travels only along coordinate axes.

Let's also study only one-dimensional motion; thus, the molecule moves either left or right (with equal probability).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

250

7 Probabilistic reasoning

Time. Let's assume that the molecule travels at a typical, fixed speed 𝑣 and that every collision happens at regularly spaced clock ticks. These ticks are therefore separated by a characteristic time 𝜏 = 𝜆/𝑣. This time is called the mean free time.

In this heavily lumped, one-dimensional model, a molecule starts at an origin (𝑥 = 0) and wanders along a line. At each tick it moves left or right with probability 1/2 for each direction.

As time passes, the molecule spreads out. Actually, the molecule itself does not spread out! It has a particular position, but we just don't know it. What spreads out is our belief about the position. In the notation of probability theory, this belief is a set of probabilities—a probability distribution—based upon our knowledge of the molecule's starting position: Pr (molecule is at position 𝑥 at time 𝑡 ∣ it was at 𝑥 = 0 at 𝑡 = 0).

(7.26)

The changing beliefs are represented by a sequence of probability distributions, one for each time step. For example, at 2𝜏 (after two ticks), the molecule has probability 1/2 of being at the origin, by either going right then left or left then right. At 3𝜏, it has probability 0 of being at the origin (why?), but probability 3/8 of being at 𝑥 = +𝜆. To quantify the spread, which is shown in the following figure, we need an abstraction and a notation.

p = 1

1

1

1

2

2

2

3

3

1

1

8

8

4

4

1

1

8

8

0

− λ + λ

−2 λ 0 +2 λ

−3 λ − λ + λ +3 λ

At 𝑡 = 0

At 𝑡 = 𝜏

At 𝑡 = 2𝜏

At 𝑡 = 3𝜏

The position of the molecule will be 𝑥. Its expected position will be ⟨𝑥⟩.

The expected position is the weighted average of the possible positions, weighted by their probabilities. Both 𝑥 and ⟨𝑥⟩ are functions of time or, equivalently, of the number of ticks. However, because motion in each direction is equally likely, the expected position does not change (by symmetry).

So ⟨𝑥⟩, which starts at zero, remains zero.

A useful measure is the squared position 𝑥2—more useful because it is never negative, making moot the symmetry argument that made ⟨𝑥⟩ = 0.

Analogous to ⟨𝑥⟩, the expected or mean squared position ⟨𝑥2⟩ is the average of the possible values of 𝑥2, weighted by their probabilities.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 251

Let's see how ⟨𝑥2⟩ changes with time. At 𝑡 = 0, the only possibility is 𝑥 = 0, so ⟨𝑥2⟩𝑡=0 = 0. After one clock tick, at 𝑡 = 𝜏, the possibilities are also limited: 𝑥 = +𝜆 or −𝜆. In either case, 𝑥2 = 𝜆2. Therefore, ⟨𝑥2⟩𝑡=𝜏 = 𝜆2.

It may be the mark of a savage, in Pólya's phrase [37], to generalize a pattern from only two data points. So let's find 𝑡 = 2𝜏 and then guess a pattern. At 𝑡 = 2𝜏, the position 𝑥 could be −2𝜆, 0, or 𝜆, with probabilities 1/4, 1/2, and 1/4, respectively. The weighted average ⟨𝑥2⟩ is 2𝜆2:

⟨𝑥2⟩ = 14 × (−2𝜆)2 + 12 × (0𝜆)2 + 14 × (+2𝜆)2 = 2𝜆2.

(7.27)

The pattern seems to be

⟨𝑥2⟩𝑡=𝑛𝜏 = 𝑛𝜆2.

(7.28)

This conjecture is correct. (You can test it at 𝑡 = 3𝜏 and 4𝜏 in Problem 7.13.) Each step contributes the squared step size 𝜆2 to the squared spread ⟨𝑥2⟩.

We saw this pattern in Section 7.2.1, when we combined plausible ranges.

The half width of the plausible range for an area 𝐴 = ℎ𝑤 was given by 𝜎 2𝐴 = 𝜎2ℎ + 𝜎 2𝑤,

(7.29)

where 𝜎𝑥 is the half width of the plausible range for the quantity 𝑥. The half widths are step sizes in a random walk—random because the estimate is equally like to be an underestimate or an overestimate (representing step-ping left or right, respectively). Therefore, the half widths, like the step sizes in a random walk, add via their squares (「adding in quadrature」).

The number of ticks is 𝑛 = 𝑡/𝜏, so ⟨𝑥2⟩, which is 𝑛𝜆2, is also 𝑡𝜆2/𝜏. Thus,

⟨𝑥2⟩

𝑡 = 𝜆2

𝜏 .

(7.30)

As time marches on, ⟨𝑥2⟩/𝑡 remains 𝜆2/𝜏! The invariant 𝜆2/𝜏 is all that we need to know about the details of a random walk.

This abstraction is known as the diffusion con-

𝐷 (m2 s−1)

stant. It is usually denoted 𝐷 and has dimen- airmoleculesinair sions of L2T−1. The table gives useful approxi-1.5×10−5

perfume molecules in air

mate diffusion constants for a particle wander-10−6

small molecules in water

ing in three dimensions. In

10−9

𝑑 dimensions, the largemoleculesinwater

diffusion constant is defined with a dimension-10−10

less prefactor:

𝐷 = 1 𝜆2

𝑑 𝜏 .

(7.31)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

252

7 Probabilistic reasoning

Because 𝜆/𝜏 is the speed 𝑣 of the molecule between its randomizing collisions, a useful alternative form for estimating 𝐷 is 𝐷 = 1𝑑𝜆𝑣.

(7.32)

Problem 7.13

Testing the random-walk dispersion conjecture Make the probability distribution for the particle at 𝑡 = 3𝜏 and 𝑡 = 4𝜏, and compute each ⟨𝑥2⟩. Do your results confirm that ⟨𝑥2⟩𝑡=𝑛𝜏 = 𝑛𝜆2?

Problem 7.14

Higher dimensions

For a molecule starting at the origin and wandering in two dimensions, ⟨𝑟2⟩ = 𝑛𝜆2, where 𝑟2 = 𝑥2 + 𝑦2. Confirm this statement for 𝑡 = 0…3𝜏.

A random and a regular walk are analogous in having an invariant. For a regular walk, it is ⟨𝑥⟩/𝑡: the speed. For a random walk, it is ⟨𝑥2⟩/𝑡: the diffusion constant. (The diffusion constant is to a random walk as the speed is to a regular walk.) However, the two walks differ in a scaling exponent.

For a regular walk, ⟨𝑥⟩ ∝ 𝑡: The scaling exponent connecting position and time is 1. For a random walk, we'll use the rms (root-mean-square) position 𝑥rms ≡ ⟨𝑥2⟩

(7.33)

as a measure analogous to ⟨𝑥⟩ for a regular walk. Because ⟨𝑥2⟩ ∝ 𝑡, the rms position 𝑥rms is proportional to 𝑡1/2: In a random walk, the scaling exponent connecting position and time is only 1/2. This scaling exponent has profound effects on heat, drag, and diffusion.

As an example of the effect, let's apply our knowledge of diffusion and random walks to a familiar sit- bottle nose

uation. Across a room someone opens a bottle of perfume or, if your taste in problems is pessimistic, a lunch of leftover fish.

room size (L)

How long until odor molecules reach your nose?

As time passes, the molecule wanders farther afield, with its rms position growing proportional to 𝑡1/2. As a lumping approximation, imagine that the molecule is equally likely to be anywhere within a distance 𝑥rms of the source (the perfume bottle or leftover fish). For the molecule to have a significant probability to be at your nose, 𝑥rms should be comparable to the room size 𝐿. Because ⟨𝑥2⟩ = 𝐷𝑡, the condition is 𝐿2 ∼ 𝐷𝑡, and the required diffusion time is 𝑡 ∼ 𝐿2/𝐷. (For another derivation, see Problem 7.16.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 253

For perfume molecules diffusing in air, 𝐷 is roughly 10−6 square meters per second. For a 3-meter room, the diffusion time is roughly 4 months: 𝑡 ∼ 𝐿2

𝐷 ∼

(3 m)2

≈ 107 s ≈ 4 months.

(7.34)

10−6 m2 s−1

This estimate does not agree with experiment! After perhaps a minute, you'll notice the aroma, whether perfume or fish. Diffusion is too slow to explain why the odor molecules arrive so quickly. In reality, they make most of the journey using a regular walk: The small, unavoidable air currents in the room transport the molecules much farther and faster than diffusion can. The speedup is a consequence of the change in scaling exponent, from 1/2 (for random walks) to 1 (for regular walks).

Problem 7.15

Diffusion constant of air

Estimate the diffusion constant for air molecules diffusing in air by using 𝐷 ∼ 13 × mean free path × travel speed

(7.35)

and the mean free path of air molecules (Section 6.4.5). This value is also its thermal diffusivity 𝜅air and its kinematic viscosity 𝜈air!

Problem 7.16

Dimensional analysis for the diffusion time Use dimensional analysis to estimate the diffusion time 𝑡 based on 𝐿 (the relevant characteristic of the room) and 𝐷 (the characteristic of the random walk).

A similar estimate explains the existence of circulatory systems. Imagine an oxygen molecule diffusing through our body to a muscle cell, where its services are needed to burn glucose and produce energy. The diffusion distance (our body size) is 𝐿 ∼ 1 meter. The diffusion constant for an oxygen molecule in water (a small molecule in water) is roughly 10−9 square meters per second. The diffusion time is roughly 109 seconds or 30 years: 𝑡 ∼ 𝐿2

𝐷 ∼

(1 m)2

= 109 s ≈ 30 years.

(7.36)

10−9 m2 s−1

Over long distances—long compared to the mean free path 𝜆—diffusion is a slow method of transport! Large organisms, especially warm-blooded organisms with high metabolic rates, need another solution: a circulatory system. It transports oxygen much more efficiently than diffusion can, just as air currents do for perfume. The circulatory system, a branching network of ever-smaller capillaries, ends once the typical distance between the smallest capillaries and a cell is small enough for diffusion to be efficient.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

254

7 Probabilistic reasoning

Another biological example of short-distance diffusion is the gap between two neighboring neurons, called the synaptic cleft. Its width is only 𝐿 ∼

20 nanometers. Signals between neighboring nerve cells, or between a neuron and a muscle cell, travel chemically, as neurotransmitter molecules.

Let's estimate the diffusion time for a neurotransmitter molecule. A neurotransmitter is a large molecule, and it is diffusing in water, so 𝐷 ∼ 10−10

square meters per second. Its diffusion time is 4 microseconds: 𝑡 ∼ 𝐿2

𝐷 ∼ (2×10−8 m)2 = 4×10−6 s.

(7.37)

10−10 m2 s−1

Without a comparison, this time means little: We cannot say right away whether the time is long or short. However, because it is much smaller than the spike-timing accuracy of neurons (about 100 microseconds), the time to cross the synaptic cleft is small enough not to affect nerve-signal propagation. For transmitting signals between neighboring neurons, diffusion is an efficient and simple solution.

Problem 7.17

Probability of being at the origin

Pólya's analysis of his encounters with the newlywed couple required first finding the probability 𝑝𝑛 that a random walker is at the origin after 𝑛 clock ticks (𝑝0 = 1).

For a 𝑑-dimensional random walk, find the scaling exponent 𝛽(𝑑) in 𝑝𝑛 ∝ 𝑛𝛽(𝑑).

Problem 7.18

Expected number of visits to the origin

Using your result from Problem 7.17, estimate the expected number of visits a random walker in one and two dimensions makes to the origin (summed over all ticks 𝑛 ≥ 0). Thereby explain Pólya's theorem [36], that a random walker in one or two dimensions always returns to the origin. What makes a three-dimensional random walk different from one or two dimensions?

7.3.2 Types of diffusion constants

Because random walks are everywhere, there are several kinds of diffusion constants. They are named differently depending on what is diffusing, but they share the mathematics of the random walk. Therefore, they all have dimensions of length squared per time (L2T−1).

what is diffusing

name of diffusion constant

symbol

particles

diffusion constant

𝐷

energy (heat)

thermal diffusivity

𝜅

momentum

kinematic viscosity

𝜈

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 255

A handful of useful diffusion constants (for particles) were tabulated on page 251. To complement that table, here are a few useful, approximate thermal diffusivities and kinematic viscosities.

𝜅air

heat diffusing in air

1.5×10−5 m2 s−1

𝜈air

momentum diffusing in air

1.5×10−5

𝜅water

heat diffusing in water

1.5×10−7

𝜈water

momentum diffusing in water

1.0×10−6

In air, all three diffusion constants—𝐷 for molecules, 𝜅 for energy, and 𝜈 for momentum—are roughly 1.5 × 10−5 square meters per second. Their similarity is no coincidence. The same mechanism (diffusion of air molecules) transports molecules, energy, and momentum.

In water, however, the molecular diffusion constant 𝐷 is several orders of magnitude smaller than the heat- and momentum-diffusion constants (𝜅

and 𝜈, respectively). Even the momentum- and heat-diffusion constants differ roughly by a factor of 7. This dimensionless ratio, 𝜈/𝜅, is the Prandtl number 𝖯𝗋. For water, I usually remember 𝜈, because it is just a power of ten in SI units, and remember the Prandtl number—the lucky number 7—and use these values to reconstruct 𝜅.

7.3.3 Thermal diffusivities of liquids and solids The large discrepancy between the molecular and thermal diffusion constants in water indicates that our model for diffusion in water is not complete. The problem is not limited to water. If we had made a similar comparison for any solid, comparing the molecular and thermal diffusion constants (𝐷 and 𝜅), the discrepancy would have been even larger.

Indeed, in liquids and solids, in contrast to gases, heat is not transported by molecular motion. In a solid, the molecules sit at their sites in the lattice.

They vibrate but scarcely wander. In a liquid, molecules wander but only slowly. Their tight packing keeps the mean free path short and the diffusion constant small. Yet, as everyday experience and the large 𝜅/𝐷 ratio suggest, heat can travel quickly in liquids and solids. The reason is that heat is transported by miniature sound waves rather than by molecular motion. The sound waves are called phonons.

By analogy to photons, which represent the vibrations of the electromagnetic field, phonons represent the vibrations of the lattice entities (the atoms 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

256

7 Probabilistic reasoning

or molecules of the liquid or solid). One molecule vibrates, shaking the next molecule, which shakes the next molecule. This chain is the motion of a phonon. Phonons act like particles: They travel through the lattice, bouncing off impurities and other phonons. Like ordinary particles, they have a mean free path and a propagation speed. These properties of their random walk determine the thermal diffusivity:

𝜅 ≈ 13 × phonon mean free path × propagation speed.

(7.38)

The propagation speed is the speed of sound 𝑐s, because phonons are tiny sound waves (familiar sound waves contain many phonons, just as light beams contain many photons). Sound speeds in liquids and solids are much higher than the thermal speeds, so we already see one reason why 𝜅, the diffusion constant for heat, is larger than 𝐷, the diffusion constant for particles.

The mean free path 𝜆 measures how far a phonon travels before bouncing (or scattering) and heading off in a random direction. Let's write 𝜆 = 𝛽𝑎, where 𝑎 is the typical lattice spacing (3 ångströms) and 𝛽 is the number of lattice spacings that the phonon survives.

Then the thermal diffusivity becomes

𝜅 = 13𝑐s𝛽𝑎.

(7.39)

For water, our favorite substance, 𝑐s ∼ 1.5 kilometers per second (as you estimated in Problem 5.58). Then the predicted thermal diffusivity becomes 𝜅water ∼ 𝛽 × 1.5×10−7 m2 s−1.

(7.40)

Because the actual thermal diffusivity of water is 1.5 × 10−7 square meters per second, our estimate is exact if we use 𝛽 = 1. This choice is easy to interpret and remember: In water, the phonons travel roughly one lattice spacing before scattering in a random direction. This distance is so short because water molecules do not sit in an ordered lattice. Their disorder provides irregularities that scatter the phonons. (At the same time, this mean free path is much larger than the mean free path of tightly packed atoms or molecules, which move a fraction of an ångström before getting significantly deflected. Therefore, even in a liquid, 𝜅 is much larger than the molecular diffusion constant 𝐷.)

To estimate 𝜅 for a solid, let's use 𝜅water along with the scaling relation 𝜅 ∝ 𝜆𝑐s.

(7.41)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 257

In a typical solid, the sound speed 𝑐s is 5 kilometers per second—roughly a factor of 3 faster than in water. The mean free path 𝜆 is also longer than in the totally disordered lattice of a liquid. In a solid without too many lattice defects, and at room temperature, a phonon travels a few lattice spacings before scattering—compared to just one lattice spacing in water.

These two differences, each contributing a factor of 3, make the typical thermal diffusivity of a solid a factor of 10 larger than that of water: 𝜅solid ∼ 𝜅water × 10 ≈ 1.5×10−6 m2 s−1.

(7.42)

Rounded to 10−6 square meters per second, this value is our 𝜅 (m2 s−1)

canonical thermal diffusivity of a solid—for example, sand- Au stone or brick. The table also shows a new phenomenon: 1.3×10−4

Cu

For metals,

1.1×10−4

𝜅 is much larger than our canonical value. Al- Fe though a small discrepancy could be explained by a few 2.3×10−5

air

missing numerical factors, this significant discrepancy indi-1.9×10−5

sandstone

cates a missing piece in our model.

1.1×10−6

brick

0.5×10−6

Indeed, in metals, heat can also be carried by electron waves, glass 3.4×10−7

not just phonons (lattice waves). Electron waves travel much water 1.5×10−7

faster and farther than phonons. Their speed, known as pine 0.9×10−7

the Fermi velocity, is comparable to the orbital speed of an atom's outer-shell electron. As you found in Problem 5.36, for hydrogen this speed is 𝛼𝑐, where 𝛼 is the fine-structure constant (∼ 10−2) and 𝑐 is the speed of light. This speed, roughly 1000 kilometers per second, is much faster than any sound speed! As a result, the thermal diffusivity in metals is large. As you can see in the table, for a good conductor, such as copper or gold, 𝜅 ∼ 10−4 square meters per second.

7.3.3.1 Heating a skillet

To feel a thermal diffusivity, place a thin cast-iron skillet on a hot stove.

How long does it take for the top surface to feel hot?

The hot stove supplies blobs of heat (of energy) that wander back and forth: The heat blobs perform a random walk. In a random walk, a particle with diffusion constant 𝐷 wandering for a time 𝑡 reaches a distance 𝑧 ∼ 𝐷𝑡 ; we used this lumping model in Section 7.3.1 to estimate the diffusion time across a synaptic cleft. Here, the particle is a blob of heat, so the diffusion constant is 𝜅. Thus, the hot front reaches a distance 𝑧 ∼ 𝜅𝑡 into the skillet.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

258

7 Probabilistic reasoning

In this lumping picture, the temperature profile Tstove

is a rectangle with a moving right edge—representing the heat wave moving upward and into top

bottom

hot zone

the skillet. For my 1-centimeter-thick cast-iron skillet

skillet, the hot front should reach the top of the skillet

Troom

skillet in roughly 4 seconds:

√

z = 0

κ t

z = L

𝑡 ∼ 𝐿2

𝜅 ≈

(10−2 m)2

≈ 4 s.

(7.43)

Fe

2.3×10−5 m2 s−1

Don't try the following experiment at home. But for the sake of lumping and probabilistic reasoning, I set our flattest cast-iron skillet on a hot electric stove while touching the top surface. After 2 seconds, my finger involuntar-ily jumped off the skillet.

Tstove

The discrepancy of a factor of 2 between the predicted T(t)

feels very hot

and actual times is not bad considering the simplic-Thot

ity, or crudity, of the lumping approximations that it incorporates. However, there is a bigger discrepancy.

Troom

The model predicts that, for the first

place

4 seconds, the top onstove

of the skillet remains at room temperature. One feels nothing until, wham, the full temperature of the stove hits at 4 seconds.

Tstove

However, experience suggests that the skillet's temperature starts rising before the skillet becomes too T(t)

Thot

hot to touch, and then it monotonically approaches feels hot

the stove temperature—as sketched in the figure.

Troom

place

One reason for this discrepancy could be the skillet's on stove top surface. In our model, the skillet has only a bottom surface and is infinitely thick. The top surface might alter the heat flow. However, the infinite-slab assumption isn't the fundamental problem (correcting the assumption turns out to speed up the heating process by a factor of 2). Even if we fix it, the model would still make the bogus prediction of a sudden jump to the stove temperature. It's hard to believe after the exhortations on the power of lumping, but we have lumped too much.

To improve the model, let's incorporate a more realistic temperature profile. Beyond the canonical lumping shape of a rectangle, the next simplest shape is a triangle (the integral of a rectangle). We will therefore replace the rectangular temperature profile with a triangle having the same area as the rectangle. Because of the factor of 1/2 in the area of a triangle, the hot zone now extends to 2 𝜅𝑡 instead of to 𝜅𝑡 .

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 259

The area of the triangle is proportional to the heat Tstove transferred to the skillet. By matching the triangle's area to the rectangle's area, we preserve this top

bottom

integral quantity. When making lumping mod-

hot zone

skillet

els, preserving integral quantities is usually more skillet

Troom

robust than is preserving differential quantities

√

z = 0

2 κ t

(such as slope).

Tstove

In the triangular-lumping model, you feel

nothing until the tip of the triangle reaches Tskillet(t)

the top of the skillet. Because the triangu- (Tstove+Troom)/2

lar hot front extends a factor of 2 farther

than the rectangular hot front (2 𝜅𝑡 ver-

sus 𝜅𝑡 ), and because diffusion times are

Troom

proportional to distance squared, the re-

L2

L2

0

quired time falls by a factor of 4. Thus, it 4 κ

κ

falls from 4 seconds to 1 second. At 1 sec-

ond, the hot front arrives at the top of the skillet, which starts to feel warm.

Then the temperature slowly increases toward the stove temperature. This next-simplest model makes quite realistic predictions!

Problem 7.19

Cooling the Moon

How long does it take for the Moon, with a radius of 1.7 × 106 meters to cool significantly by heat diffusion through rock? Given that the Moon is now cold, what do you conclude about the mechanism of cooling?

Problem 7.20

Diffusion with a bit of drift: Breaking the bank at Monte Carlo You can play the card game blackjack such that your probability of winning a hand is 𝑝 = 0.51 and of losing is 1 − 𝑝 = 0.49. You start with 𝑁 betting units, the stake; and you bet 1 unit on each hand. The goal of this problem is to estimate the threshold 𝑁 such that you are more likely to break the bank than to lose the stake.

Let 𝑥𝑛 be your balance after the 𝑛th hand. Thus, 𝑥0 = 𝑁. Losing your stake (the 𝑁 units) corresponds to 𝑥 = 0. To estimate 𝑁, extend the random-walk model to account for drift: that the probabilities of moving left and right are not equal.

a. What is the symbolic expression for breaking the bank?

b. Sketch your expected balance ⟨𝑥⟩ versus the number of hands 𝑛 (on linear axes).

c. Sketch, on the same axes, the dispersion 𝑥rms versus 𝑛.

d. Explain graphically「a significant probability of breaking the bank.」

e. Thus, estimate the required stake 𝑁.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

260

7 Probabilistic reasoning

7.3.3.2 Baking

A skillet on a stove gets heated from one side. An equally important kind of cooking, and one that helps us practice and extend our lumping model of random walks, is heating from two sides: baking. As an example, imagine baking a slab of fish that is 𝐿 = 1 inch (2.5 centimeters) thick.

How long should it bake in the oven?

A first, and quick, analysis predicts 𝐿2/𝜅, the characteristic time for heat diffusion, where 𝜅 is the thermal diffusivity of water (organisms are mostly water). However, this simple model predicts an absurd time: 𝑡 ∼ 𝐿2

𝜅

≈

(2.5 cm)2

∼ 70 minutes.

(7.44)

water

1.5×10−3 cm2 s−1

After more than an hour in the oven, the fish will be so dry that it might catch fire, never mind not being edible. The model also ignores an important quantity: the oven temperature. Fixing this hole in the model will also improve the time estimate.

Why does the oven temperature matter?

The inside of the fish must get cooked, which means that the proteins dena-ture (lose their folded shape) and the fats and carbohydrates change their chemistry enough to become digestible. This process happens only if the food gets hot enough. Thus, a cold oven could not cook the fish, even after the fish reached oven temperature. What temperature is hot enough? From experience, a thin piece of meat on a hot skillet (at, say, 200 ∘C) cooks in less than a minute. At the other extreme, if the skillet is at 50 ∘C, unpleasantly hot to the touch but not much hotter than body temperature, the meat never cooks. A round, intermediate temperature of 100 ∘C, enough to boil water, should be enough to cook meat thoroughly.

oven at 180 ◦C

If we set the oven to, say, 180 ∘C, the fish will then be cooked once its center reaches the midpoint of the room fish starts at 20 ◦C

(

oven at 180 ◦C

20 ∘C) and oven temperatures, which is 100 ∘C. In this improved model of cooking, the interior of the fish starts at 𝑇room ≈ 20 ∘C, and the oven holds the top and bottom surfaces of the fish at 𝑇oven = 180 ∘C (360 ∘F). With this model, and using triangular temperature profiles, we will estimate the time required for the center of the fish to reach the midpoint temperature of 100 ∘C.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.3 Random walks: Viscosity and heat flow 261

Toven

Two triangular hot zones, one from each surface, move toward the center of the fish. Before the zones meet, the top

center of the fish, at 𝑧 = 𝐿/2, is cold (room temperature).

bottom

Troom

The fish, unless it is very fresh, is not ready to eat. But 0

L

L

2

soon the triangles will meet.

Toven

Each triangle extends a distance 2 𝜅𝑡 . They first meet (at 𝑥 = 𝐿/2) when 2 𝜅𝑡 = 𝐿/2. Thus, 𝑡meet ∼ 𝐿2/16𝜅.

top

From that moment, the center warms up as the triangle bottom

Troom

fronts overlap ever more. The fish is cooked when the cen-0

L

L

2

ter reaches the mean of the room and oven temperatures (which is 100 ∘C).

In dimensionless temperature units, where

T = 1

𝑇room corre-

sponds to 𝑇 = 0 and 𝑇oven to 𝑇 = 1, the cooking crite-1/2

top

rion is 𝑇 = 1/2. Each triangle wave therefore contributes T = 0

𝑇 = 1/4. The left triangle, representing the hot front in-0

L

L

2L

L

3

2

3

vading from the bottom surface, then passes through the points (𝑧 = 0, 𝑇 = 1) and (𝑧 = 𝐿/2, 𝑇 = 1/4). It reaches the 𝑧 axis (𝑇 = 0) when 𝑧 = 2𝐿/3. The corresponding triangle-zone diffusion time is given by 2 𝜅𝑡 = 2𝐿/3, whose solution is

𝑡cooked ∼ 𝐿2

9𝜅 .

(7.45)

For our 2.5-centimeter-thick fish, the time is roughly 7 minutes: 𝑡 ∼ 19 ×

(2.5 cm)2

∼ 7 minutes.

(7.46)

1.5×10−3 cm2 s−1

This estimate is reasonable. My experience is that a fish fillet of this thickness requires about 10 minutes in a hot oven to cook all the way through (and further baking only dries it out).

Problem 7.21

Baking too long

In the model of two approaching triangle hot fronts, the central temperature starts to rise at 𝑡 ∼ 𝐿2/16𝜅, and it reaches the halfway temperature at 𝑡cooked ∼ 𝐿2/9𝜅.

When does it reach the oven temperature? Sketch the central temperature versus time, labeling interesting values.

Problem 7.22

Cooking an egg

Baking a 6-kilogram turkey requires, from experience, 3 to 4 hours (you get to predict this time in Problem 7.34). Use proportional reasoning to estimate the time required to boil an egg.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

262

7 Probabilistic reasoning

7.3.4 Boundary layers

In cooking, the hot zone diffuses inward from the hot surface. For the most tangible example of this random walk, rub your finger on the blade of a (sta-tionary!) window fan. Your finger comes away dusty and leaves a dust-free streak on the blade. But why is any dust on the blade at all? When the fan was turning, why didn't the air streaming by the blade blow off the dust?

The answer lies in the concept of the boundary layer. For the cooking examples (Sections 7.3.3.1 and 7.3.3.2), this layer is the expanding hot zone. It arises from the boundary constraint (the temperature), which diffuses into the skillet or the fish. For the fan blade, the analogous constraint is that, next to the blade, the fluid has zero velocity with respect to the blade. The condition, called the no-slip boundary condition, has the justification that the fluid molecules next the surface get caught by the inevitable roughness at the surface. (For a historical and philosophical discussion of the subtleties of this boundary condition, see Michael Day's article on「The no-slip condition of fluid dynamics」[8].)

Starting at the blade surface, a zero-speed or, equivalently, zero-momentum zone diffuses into the fluid—just as the stove temperature diffuses into the skillet or the oven temperature into the fish fillet. After a growth time 𝑡, the zero-momentum front has diffused a distance 𝛿 ∼ 𝜈𝑡 , where 𝜈 is the diffusion constant for momentum (the kinematic viscosity). The distance 𝛿

is the boundary-layer thickness. Within the boundary layer, the fluid moves more slowly than the fluid in the free stream. Using a rectangular lumping picture, the fluid speed is zero within the layer and full speed outside it.

Therefore, dust particles entirely in the layer remain on the blade.

To estimate the boundary-layer thickness, imagine a window fan with a blade width 𝑙 and rotation speed 𝑣 at the widest part of the blade.

l

The growth time is 𝑡 ∼ 𝑙/𝑣. For a generic window fan sweeping out a diameter of 0.5 meters, the blade width 𝑙 may be roughly 0.15 meters.

If the fan rotates at roughly 15 revolutions per second or 𝜔 ∼ 100 ra-0.5 m

dians per second, the blade speed 𝑣 is 10 meters per second: 𝑣 ∼ 0.1 m

⏟ × 100 rad s−1

⏟⏟⏟⏟⏟⏟⏟ = 10 m s−1.

(7.47)

arc radius

𝜔

At this speed, the growth time 𝑡 is 0.015 seconds. In that time, the zero-momentum constraint diffuses roughly 0.5 millimeters from the fan blade: 𝛿 ∼ ( 0.15 cm2 s−1

⏟⏟⏟⏟⏟⏟⏟ × 0.015 s

⏟ )1/2 ≈ 0.05 cm.

(7.48)

𝜈air

𝑡

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 263

Dust particles that are significantly smaller than 0.5 millimeters feel no air flow (in this simplest lumping picture) and thus remain on the fan blade until your finger rubs them off. For the same reason (boundary layers), simply rinsing dirty dishes in water will not remove the thin layer of food next to the surface. Proper cleaning requires scrubbing (a sponge) or soap (which gets underneath the food oils).

Problem 7.23

Reynolds number in the boundary layer

Based on the boundary-layer thickness 𝛿 ∼ 𝜈𝑡 , estimate the Reynolds number in a boundary layer on an object of size 𝐿 (a length) moving in a fluid at speed 𝑣.

Problem 7.24

Turbulence in the boundary layer

At Reynolds numbers comparable to 1000, flows usually become turbulent. Use Problem 7.23 to estimate the main-flow Reynolds number at which the boundary layer becomes turbulent. For a smooth ball similar in size to a golf ball, what flow speed is required? Suggest an explanation for the dimples on golf balls.

7.4 Transport by random walks

When a hot-oven temperature front diffuses into a slab of fish or the no-slip, zero-momentum front diffuses into a fluid, it comes with a heat or momentum flow. With our random-walk model, we can estimate the magnitude of these flows, and thereby understand the drag forces on fog droplets and bacteria (Problem 7.26) and why we feel cold on a winter day without thick clothing (Section 7.4.4).

7.4.1 Diffusion speed

The essential property of a random walk is that the distance traveled is not proportional to the time, as it would be in a regular walk, but rather to the square root of the time. This change in scaling exponent means that the speed at which heat, momentum, or particles diffuse depends on the diffusion distance. When the distance is 𝐿, the diffusion time is 𝑡 ∼ 𝐿2/𝐷, where 𝐷 is the appropriate diffusion constant. Thus, the transport speed is comparable to 𝐷/𝐿:

𝑣 ∼ 𝐿𝑡 ∼ 𝐿 = 𝐷

𝐿2/𝐷

𝐿 .

(7.49)

This speed depends inversely on the distance. This scaling is consistent with our calculations showing that diffusion is a terribly slow means of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

264

7 Probabilistic reasoning

transport over long distances (for example, for perfume molecules diffusing across a room) but fast over short distances (for example, for neurotransmitter molecules diffusing across a synaptic cleft).

When the diffusing quantity is momentum, the appropriate diffusion constant is 𝜈, and the diffusion speed is 𝜈/𝐿. Thus, the Reynolds number, 𝑣flow𝐿/𝜈, is the ratio 𝑣flow/𝑣diffusion—for the same reason that it is the ratio of times 𝑡diffusion/𝑡flow (as you will find in Problem 7.32). Using the diffusion speed, we can estimate fluxes and flows.

7.4.2 Flux

Transport is measured by the flux:

flux of stuff = amount of stuff

area × time .

(7.50)

As we found in Section 3.4.2, the flux is also given by flux of stuff = stuff

volume × transport speed.

(7.51)

When the stuff travels by diffusion, the transport speed is the diffusion speed 𝐷/𝐿 (from Section 7.4.1). The resulting flux is flux of stuff ∼ stuff

volume × diffusion constant

distance

.

(7.52)

In symbols,

𝐹 ∼ 𝑛𝐷𝐿,

(7.53)

where 𝑛 is the concentration (stuff per volume), 𝐷 is the appropriate diffusion constant (depending on what is diffusing), and 𝐿 is the distance.

gap

An important application is diffusion across a gap. The gap could be a synaptic cleft, with a gap width 𝐿 ∼ 20 nanometers and F1→2

with different neurotransmitter concentrations on its two sides. n1

n2

Or it could be a shirt (𝐿 ∼ 2 millimeters) with different tempera-F2→1

tures—concentrations of energy—on the inside and outside. On one side, the density of stuff is 𝑛1; on the other side it is 𝑛2. Then L

there are two fluxes in the gap, left to right and right to left: 𝐹

𝐷

1→2 ∼ 𝑛1 𝐿

(7.54)

𝐹

𝐷

2→1 ∼ 𝑛2 𝐿 .

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 265

The net flux 𝐹 is their difference:

𝐹 ∼ (𝑛2 − 𝑛1)𝐷𝐿 = 𝐷𝑛2 − 𝑛1

𝐿 .

(7.55)

The concentration difference 𝑛2 − 𝑛1 divided by the gap size 𝐿 is an important abstraction: the concentration gradient. It measures how rapidly the concentration varies with distance. Using it, the flux becomes flux = diffusion constant × concentration gradient.

(7.56)

This result, called Fick's law, is exact (hence the equals sign instead of ∼).

In calculus form, the concentration gradient is Δ𝑛/Δ𝑥, so 𝐹 = 𝐷 Δ𝑛

Δ𝑥 .

(7.57)

If the diffusing stuff is particles, then the appropriate diffusion constant is just 𝐷, and the result can be used as is. If the diffusing stuff is momentum, then the diffusion constant is the kinematic viscosity 𝜈, and the flux is closely connected to a drag force (Problem 7.25).

Problem 7.25

Momentum flux produces drag

If the diffusing stuff is momentum, then the diffusion constant is the kinematic viscosity 𝜈, and the concentration gradient is the gradient of momentum density.

Thus, explain why Fick's law becomes

viscous stress = 𝜌𝜈 × velocity gradient,

(7.58)

where viscous stress is viscous force per area (𝜌𝜈 is the dynamic viscosity 𝜂).

Problem 7.26

Stokes drag

In this problem, you use momentum flux (Problem 7.25) to estimate the drag force on a sphere of radius 𝑟 in a flow at low Reynolds number (𝖱𝖾 ≪ 1). If 𝖱𝖾 ≪ 1, the boundary layer (Section 7.3.4)—the region over which the fluid velocity changes from zero to the free-stream velocity 𝑣—is comparable in thickness to 𝑟. Using that information, estimate the viscous drag force on the sphere.

If the diffusing stuff is heat (energy), the diffusion constant is the thermal diffusivity 𝜅, and the concentration gradient is the gradient of energy density. Thus, heat flux is

heat flux = thermal diffusivity × energy-density gradient.

(7.59)

To figure out the meaning of energy-density gradient, let's start with energy density itself, which is energy per volume. We usually measure it using temperature. Therefore, to make the eventual formula applicable, let's rewrite energy density in terms of temperature:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

266

7 Probabilistic reasoning

energy

energy

volume = volume × temperature × temperature.

(7.60)

The complicated quotient on the right splits into two simpler factors: energy

energy

volume × temperature = mass

volume × mass × temperature.

(7.61)

The first factor, mass per volume, is just the substance's density 𝜌. The second factor is called the specific heat 𝑐p. The most familiar specific heat is water's: 1 calorie per gram per ∘C. That is, raising 1 gram of water by 1 ∘C

requires 1 calorie (≈ 4 joules).

Using these abstractions,

energy

volume × temperature = 𝜌𝑐p,

(7.62)

To get energy density, or energy per volume, we multiply by temperature energy

volume = 𝜌𝑐p𝑇.

(7.63)

Now that we have energy density, we can find the energy-density gradient.

Because 𝜌 and 𝑐p are constants (at least for small temperature and position changes), any gradient of energy density is due to the temperature gradient Δ𝑇/Δ𝑥:

energy-density gradient = 𝜌𝑐p × temperature gradient.

(7.64)

Fick's law, when energy is the diffusing stuff, tells us that energy flux = thermal diffusivity × energy-density gradient, (7.65)

so

heat (energy) flux = 𝜅 × 𝜌𝑐p × temperature gradient.

(7.66)

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

energy-density gradient

The shaded combination 𝜌𝑐p𝜅 occurs in any heat flow driven by a temperature gradient. It is a powerful abstraction called the thermal conductivity 𝐾:

thermal conductivity = density × ( specific × ( thermal

. (7.67)

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ ⏟

heat )

⏟⏟⏟⏟⏟

diffusivity )

⏟⏟⏟⏟⏟⏟⏟

𝐾

𝜌

𝑐

𝜅

p

Thermal conductivity has dimensions of power per length per temperature, and is often quoted in units of watts per meter kelvin (W m−1 K−1). Using 𝐾, Fick's law for energy flux in terms of temperature gradient Δ𝑇/Δ𝑥 becomes 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 267

𝐹 = 𝐾 Δ𝑇

Δ𝑥 ,

(7.68)

where Δ𝑇 is the temperature difference, and Δ𝑥 is the gap size.

Now let's estimate a few important thermal conductivities in order to understand heat flow around us.

7.4.3 Thermal conductivity of air

To estimate our heat loss standing outside on a cold winter's day, we need to estimate the thermal conductivity of air.

Why do we estimate the thermal conductivity of air rather than of clothing?

The purpose of clothing is to trap air so that heat flows via conduction—that is, by diffusion—rather than via the faster process of convection. (If the perfume molecules of Section 7.3.1 could be similarly limited to diffusion, the perfume aromas would travel very slowly.) Because 𝐾 ≡ 𝜌𝑐p𝜅, estimating 𝐾 splits into three subproblems, one for each factor. The density of air 𝜌air is just 1.2 kilograms per cubic meter (slightly more accurate than 1 kilogram per cubic meter). The thermal diffusivity 𝜅air is 1.5×10−5 square meters per second.

The specific heat 𝑐p is not as familiar, but we can estimate it. As for water, it measures the thermal energy per mass per temperature: thermal energy

𝑐p = mass × temperature.

(7.69)

The thermal energy per particle is comparable to 𝑘B𝑇, where 𝑘B is Boltzmann's constant, so the energy per temperature is comparable to 𝑘B. Thus, 𝑐p ∼ 𝑘B

mass.

(7.70)

Our thermal energy, which is comparable to 𝑘B𝑇, is for one particle. The corresponding mass in the denominator is the mass of one particle, which is an air molecule.

To convert 𝑘B and the mass to human-sized values, we multiply each by Avogadro's number 𝑁A. Then we replace 𝑘B𝑁A with the universal gas constant 𝑅, and mass × 𝑁A with the molar mass 𝑚molar. The result is 𝑐p ∼

𝑘B𝑁A

molecular mass × 𝑁 = 𝑅 ,

(7.71)

A

𝑚molar

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

268

7 Probabilistic reasoning

where 𝑚molar is the molar mass of air.

This expression is correct except for a dimensionless prefactor. Air is mostly nitrogen, for which the prefactor is 7/2. This magic number can be made slightly less magical as follows:

7

spatial dimensions

2 =

2

+ rotational directions

2

+ 1.

(7.72)

Each spatial dimension contributes one 1/2 through a term in the translational kinetic energy of a nitrogen molecule; thus, the translational piece contributes 3/2 to the prefactor. Each rotational direction contributes a 1/2

through a term in the rotational energy of a nitrogen molecule. Because nitrogen is a linear molecule, there are only two rotational directions, so the rotational directions contribute 2/2 to the prefactor. If we stop here, at 5/2, we would have the prefactor to find 𝑐v, the specific heat while holding the volume constant. The final term, +1, accounts for the energy required to expand a gas as it is heated and held at constant pressure. Therefore, 𝑐p gets a prefactor of 7/2. (For a more detailed discussion of the reasoning behind this calculation, see the classic Gases, Liquids and Solids and Other States of Matter [43, pp. 106].)

Air is mostly diatomic nitrogen, so 𝑚molar is roughly 30 grams per mole.

Then 𝑐p is roughly 103 joules per kilogram kelvin: 𝑐p = 72 × 𝑅

𝑚

≈ 7

× 1 mol

≈ 103 J

molar

2 × 8 J

mol K

⏟ 3×10−2 kg

⏟⏟⏟⏟⏟ kg K.

(7.73)

𝑅

𝑚−1

molar

Putting together the three pieces,

𝐾air ≈ 1.2 kg m−3

⏟⏟⏟⏟⏟ ×103 J kg−1

⏟⏟⏟⏟⏟ ×1.5×10−5 m2 s−1

⏟⏟⏟⏟⏟⏟⏟⏟⏟ ≈ 0.02 W

m K.

(7.74)

𝜌air

𝑐p

𝜅air

Before using the thermal conductivity, let's try out the specific heat of air on an old method of air conditioning. One summer I lived in a tiny Manhattan apartment (30 square meters). Summers are hot in New York City, and the beautiful people flee for the cooler beach areas—cooler thanks partly to the high specific heat of water (Problem 7.27). Because of global warming and the old electrical wiring in the apartment building, too old to handle an air-conditioning unit, the apartment reached 30 ∘C at night. A friend who grew up before air conditioning suggested taking a wet sheet and using a fan to blow air past it.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 269

How much does this system cool the apartment?

As heat from the room air evaporates the water from the sheet, the room air cools, as if the room were sweating. The energy required to evaporate the water is

𝐸 = 𝑚water𝐿vap,

(7.75)

where 𝑚water is the mass of water held by the wet sheet and 𝐿vap is the heat of vaporization of water. This energy is the demand.

To lower the room's temperature by Δ𝑇 requires using up a thermal energy 𝐸 ∼ 𝜌air𝑉𝑐pΔ𝑇,

(7.76)

where 𝑉 is the volume of the room and 𝑐p is the specific heat of air. This energy is the supply.

Equating supply and demand gives an equation for Δ𝑇: 𝜌air𝑉𝑐pΔ𝑇 ∼ 𝑚water𝐿vap.

(7.77)

Its solution is

𝑚

Δ𝑇 ∼ water𝐿vap

𝜌

.

(7.78)

air𝑉𝑐p

Now we estimate and plug in the needed values. A typical room is roughly 3 meters high, so the apartment's volume was roughly 100 cubic meters: 𝑉 ∼ 30 m2

⏟ × 3 m

⏟ ≈ 100 m3.

(7.79)

area

height

To estimate 𝑚water, I imagined that the sheet was about as wet as it would be after coming out of the washing machine with its fast spin cycle. That mass feels like slightly more than 1 kilogram, so 𝑚water ∼ 1 kilogram. Finally, the heat of vaporization of water is about 2×106 joules per kilogram (as we estimated in Section 1.7.3 using a home experiment).

Putting in all the numbers, Δ𝑇 is about 20 ∘C (or 20 K): 𝑚

𝐿

water

vap

⏞⏞⏞⏞⏞⏞⏞

Δ𝑇 ∼

1 kg

⏞ × 2×106Jkg−1

= 20 K.

(7.80)

1 kg m−3

⏟⏟⏟⏟⏟ × 100 m3

⏟ × 103 J kg−1 K−1

⏟⏟⏟⏟⏟⏟⏟

𝜌air

𝑉

𝑐p

This change would have turned the hot 30 ∘C room into a cold 10 ∘C room, if the cooling had been 100-percent efficient. Because some heat comes from 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

270

7 Probabilistic reasoning

the walls (and from the fan motor), Δ𝑇 will be less than 20 ∘C—perhaps 10 ∘C, leaving the room at a pleasant and sleepable temperature of 20 ∘C.

This calculation shows not only that evaporative cooling is a reasonable method of air conditioning, but also that our estimate for the specific heat of air is reasonable.

Problem 7.27

Dimensionless specific heat of water

The specific heat per air molecule is 3.5𝑘B, so the dimensionless specific heat of air, measured relative to 𝑘B, is 3.5. What is the dimensionless specific heat of water?

7.4.4 Keeping warm on a cold day

Now we have assembled the pieces to understand why trapped air

(shirt)

we dress warmly on a cold day. Our starting point is the 0 ◦C

30 ◦C

winter

heat flux:

skin

∆x

air

𝐹 = 𝐾 Δ𝑇

Δ𝑥 ,

(7.81)

where Δ𝑇 = 𝑇2 − 𝑇1 is the temperature difference across a gap, Δ𝑥 is the gap size, and 𝐾 is the thermal conductivity of the gap material. Here, the gap material is air—the clothing serves to trap the air.

Let's say that the air outside is at 𝑇1 = 0 ∘C and that skin is at 𝑇2 = 30 ∘C

(slightly lower than the internal body temperature of 37 ∘C). Then Δ𝑇 =

30 K. Against the advice of your elders, you dress in a thin T-shirt—for decency, a very long one. A thin T-shirt has thickness Δ𝑥 of roughly 2 millimeters. With these parameters, the heat flux through the shirt becomes 300 watts per square meter:

Δ𝑇

𝐹 ≈ 0.02 W ×

30 K

⏞

= 300 W m−2.

(7.82)

⏟⏟ m

⏟ K

⏟⏟ 2

⏟×

⏟10−3

⏟ m

⏟⏟

𝐾air

Δ𝑥

Flux is power per area, so the energy flow—the power—is the flux times a person's surface area. A person is roughly 2 meters tall and 0.5 meters wide, with a front and a back, so the surface area is about 2 square meters.

Thus, the power (the energy outflow) is 600 watts.

Is this heat loss worrisome?

Even though 600 might seem like a large number, we cannot therefore conclude that 600 watts is a large heat loss: As we learned in Chapter 5, a 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 271

quantity with dimensions, such as heat flux, cannot be large or small on its own. It needs to be compared to a relevant quantity with the same dimensions. A relevant quantity is a normal human power output. When sitting around, a person produces 100 watts of heat; that's our basal metabolic rate. If 600 watts is escaping through your clothing, you are losing heat much faster than the basal metabolism is producing it. No wonder you feel so cold on a winter day wearing only a thin shirt and pants. Eventually, your core body temperature falls. Then essential chemical reactions in your body slow down, because the enzymes lose their shape optimized for body temperature and thereby become less efficient catalysts. Eventually you get hypothermia and, if it goes on too long, die.

One solution is to generate heat to make up the difference: by shivering or exercising. Cycling hard, which generates, say, 200 watts of mechanical power and another 600 watts of heat (thanks to the one-fourth metabolic efficiency), should be vigorous-enough exercise to keep you warm, even on a winter day in thin clothing.

Another simple solution is to dress warmly by putting on thick layers. Let's recalculate the power loss if you put on a jacket and thick pants, each 2 centimeters thick. We could redo the power calculation from scratch, but that approach is brute force. It is simpler to notice that the gap thickness Δ𝑥

has increased by a factor of 10, yet nothing else changed. Because flux is inversely proportional to the gap size, the flux and the power drop by the same factor of 10. Therefore, wearing thick clothing reduces the energy outflow to a manageable 60 watts—comparable to the basal metabolism. As a result, your body heat can keep you warm. Indeed, when wearing thick clothing, only areas exposed directly to cold air, such as your hands and face, feel cold. Those regions are protected by only a thin layer of still air (the boundary layer analyzed in Section 7.3.4).

A thick gap means a small heat flux: When it is cold, bundle up!

Problem 7.28

Thermal conductivity of helium gas

Estimate the thermal conductivity of helium at standard temperature and pressure.

The following fact will help you estimate the mean free path: The density of liquid helium is 125 grams per liter.

Problem 7.29

Comfortable outdoor temperature

You wear only that long thin T-shirt in which the winter temperature of 0 ∘C felt too cold. Estimate the outside temperature that would feel most comfortable.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

272

7 Probabilistic reasoning

7.4.5 Getting your clothes wet: More thermal conductivities If your thick warm coat gets wet, you feel very cold. Let's use our knowledge of heat flow to explain why the coat becomes so useless. As we know from Section 7.4.4, you feel cold when the dimensionless ratio energy flow through your coat

rate at which your body generates heat

(7.83)

is significantly larger than 1. The dry coat kept the energy flow (a power) comparable to the rate at which your body generated heat. Wetting the coat must increase the energy flow significantly. To see how, let's look again at the terms in the energy flow and apply proportional reasoning.

energy flow = area × 𝐾 Δ𝑇

Δ𝑥 .

(7.84)

⏟

flux

In comparing the wet to the dry coat, the area is unchanged. The temperature difference Δ𝑇 is also unchanged: It is still the 30 ∘C between skin temperature and winter-air temperature. The gap Δ𝑥, which is the thickness of the coat, is also unchanged.

The remaining possibility is that the thermal conductivity 𝐾 of the gap material has increased significantly. If so, the thermal conductivity of water must be much higher than the thermal conductivity of air. Rather than studying water directly, let's first estimate the thermal conductivity of nonmetallic solids. (Metals have an even higher thermal conductivity, as we will discuss after studying water.) Using that estimate, we will estimate the thermal conductivity of water.

The problem is again comparative (proportional reasoning): thermal conductivity of nonmetallic solids

thermal conductivity of air

.

(7.85)

The ratio breaks into three ratios, corresponding to the three factors in the thermal conductivity (divide-and-conquer reasoning): 𝐾 = density

⏟⏟⏟⏟⏟ × specific heat

⏟⏟⏟⏟⏟⏟⏟ × thermal diffusivity.

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

(7.86)

𝜌

𝑐p

𝜅

Rather than using these factors directly, let's remix the first two ( 𝜌𝑐p) into a more insightful combination. The specific heat itself is energy

𝑐p = mass × Δ𝑇 ,

(7.87)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 273

where Δ𝑇 is the temperature change.

Multiplying by the density 𝜌 points us toward an interpretation of 𝜌𝑐p: energy

energy

𝜌𝑐p = mass

v

×

=

⏟olume

⏟⏟⏟⏟

mass

⏟⏟⏟ ×

⏟Δ𝑇

⏟⏟⏟

volume × Δ𝑇 .

(7.88)

𝜌

𝑐p

On the right side, the ratio of energy to volume can be subdivided as energy

energy

−1

volume = mole × (volume

mole ) .

(7.89)

After all these reinterpretations, our remix of 𝜌𝑐p becomes energy

−1

𝜌𝑐p = mole × Δ𝑇 × (volume

mole ) .

(7.90)

The first factor is the molar specific heat; it is usually denoted 𝐶p (with a capital「𝐶」to distinguish it from the usual, per-mass specific heat 𝑐p). The volume per mole is also called the molar volume; it is usually denoted 𝑉m.

Therefore, 𝜌𝑐p = 𝐶p/𝑉m. Then the thermal conductivity becomes 𝐶

𝐾 = 𝜌𝑐

p

p𝜅 = 𝑉 𝜅.

(7.91)

m

In words, the thermal conductivity 𝐾 is

molar specific heat 𝐶p

molar volume 𝑉

× thermal diffusivity 𝜅.

(7.92)

m

This remix is more insightful than simply 𝜌𝑐p𝜅 because 𝐶p varies less between substances than 𝑐p does, and 𝑉m varies less between substances than 𝜌 does. The remixed form produces less quantity whiplash, in which the product swings wildly up and down as we include each factor. Another way to express the same advantage is that 𝐶p and 𝑉m are less correlated than are 𝜌 and 𝑐p; therefore, the remixed abstractions 𝐶p and 𝑉m offer more insight into the thermal properties of materials than do 𝑐p and 𝜌.

Using the remixed form, let's apply divide-and-conquer reasoning and estimate the ratio corresponding to each factor.

1. Ratio of molar specific heats 𝐶 p. For air, 𝐶p was 3.5𝑅. For most solids, whether metallic or nonmetallic, it is similar: 3𝑅 (where the 3 reflects the three spatial dimensions). Thus, this ratio is close to 1.

2. Ratio of molar volumes 𝑉 m. For any substance, 1 mole has a mass of 𝐴 grams, where 𝐴 is the dimensionless atomic mass (roughly, the number of protons and neutrons in the nucleus). Because a typical solid 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

274

7 Probabilistic reasoning

density is 𝐴 grams per 18 cubic centimeters (Section 6.4.1), the molar volume of the solid is 18 cubic centimeters per mole. In contrast, for air or any ideal gas (at standard temperature and pressure), 1 mole occupies 22 liters or 22 000 cubic centimeters. Thus, the ratio of molar volumes (solid to air) is 18/22 000 or roughly 10−3.

3. Ratio of thermal diffusivities 𝜅. From Section 7.3.3, this ratio is roughly 0.1: thermal diffusivity of nonmetallic solids

thermal diffusivity of air

≈ 10−6 m2 s−1

10−5 m2 s−1

(7.93)

= 0.1.

The ratio of thermal conductivities is the product of the three ratios. As long as we remember that the molar volume appears in the denominator (the thermal conductivity is inversely proportional to the molar volume), we get a ratio of 100:

𝐾nonmetallic solid

𝐾

∼ 1

⏟ × 103

⏟ × 10−1

⏟ = 102.

(7.94)

air

𝐶p ratio (𝑉m ratio)−1

𝜅 ratio

Thus, in contrast to the thermal conductivity of 0.02 watts per meter kelvin for air, the typical (nonmetallic) solid has a thermal conductivity of about 2 watts per meter kelvin.

Now let's use proportional reasoning to compare this thermal conductivity to the thermal conductivity of water, which is the gap material in your wet coat. We'll estimate 𝐾water/𝐾nonmetallic solid. The comparison has the same three ratios: molar specific heat, molar volume, and thermal diffusivity.

1. Ratio of molar specific heats 𝐶 p. We can find the specific heat of water from the definition of a calorie, as the energy required to raise 1 gram of water by 1 degree (celsius or kelvin). Thus, the regular specific heat is simple to state:

𝑐water

p

= 1 cal

g K .

(7.95)

The resulting molar specific heat is 72 joules per mole kelvin: 𝐶water

p

≈ 1 cal

g K × 4 J × 18 g = 72 J .

(7.96)

⏟

1 cal

⏟

mol

⏟

mol K

𝑐p

1

𝑚molar

The dimensionless specific heat 𝐶water

p

/𝑅 is therefore approximately 9

(as you found in Problem 7.27):

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.4 Transport by random walks 275

𝐶water

p

𝑅 ≈ 72 J mol−1 K−1 = 9.

(7.97)

8 J mol−1 K−1

For a nonmetallic solid, the dimensionless specific heat was only 3; it is a factor of 3 smaller than for water. Water stores heat very efficiently, which is why it is used as coolant fluid and why coastal weather is milder than inland weather. The ratio of molar specific heats is 3.

2. Ratio of molar volumes 𝑉 m. The molar volume of water, 18 cubic centimeters per mole, is identical to the canonical molar volume of a solid. Thus, the molar-volume ratio is 1.

3. Ratio of thermal diffusivities 𝜅. As we found in Section 7.3.3 by comparing phonon mean free paths and propagation speeds, the thermal diffusivity 𝜅water is roughly a factor of 10 smaller than the thermal diffusivity of a typical solid (10−7 compared to 10−6 square meters per second). Thus, the thermal-diffusivity ratio contributes a factor of 0.1.

These three ratios result in the following comparison: 𝐾water

𝐾

≈ 3

⏟ ×

1

⏟ × 0.1

⏟ ≈ 0.3.

(7.98)

nonmetallic solid

𝐶p ratio (𝑉m ratio)−1 𝜅 ratio

In absolute terms,

𝐾water ≈ 0.3 × 2 W

m K = 0.6 W

⏟

m K .

(7.99)

𝐾nonmetallic solid

This conductivity is a factor of 30 larger than 𝐾air. As a result, wearing wet clothes on a cold day is so unpleasant and can even be dangerous. Thick clothing (a coat) allowed a comfortable 60 watts of heat flow—a factor of 10

lower than the T-shirt allowed. Wetting the thick coat increases the thermal conductivity by a factor of 30. The heat loss therefore increases by a factor of 30—making it higher even than the heat loss through the dry T-shirt.

When you hike in the hills and mountains, bring waterproof clothing!

The table gives thermal conductivities for everyday substances (at room temperature). Our predictions for nonmetals match the data quite well.

Having examined gases (in particular, air) and nonmetallic solids and liquids (water), let's turn to the remaining category of material. As the table shows, metals have an even higher thermal conductivity than a typical nonconducting solid. (For the unusually high thermal conductivity of diamond, try Problem 7.33.)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

276

7 Probabilistic reasoning

Metals, similarly, have a higher thermal diffusivity than W

𝐾 (

most other substances. The reason, as we discussed in m K )

Section 7.3.3, is that, in a metal, heat is conducted not diamond 2000

only by phonons but also by electrons. The electrons Cu move much faster than the speed of sound, and the elec-400

Ag

tron mean free path is much greater than the phonon 350

Al

mean free path.

240

cast iron

55

Countering these increases, which increase the diffusiv- Hg 8.3

ity, only a small fraction of the free electrons participate in heat conduction. However, this effect is not enough to ice 2.2

overcome the greater speed and mean free path. Thus, sandstone 1.7

metals will have a higher thermal conductivity than non- glass 1

metallic liquids or solids. As a rule of thumb, the typical asphalt 0.8

brick

𝐾

0.8

metal is 200 watts per meter kelvin: a factor of 100 higher than that of nonmetallic solid.

concrete

0.6

water

0.6

For this reason, a hot piece of metal, such as a seat-belt soil (dry) 0.5

clip in a car outside on a hot day, feels much hotter than wood 0.15

the plastic button on the same seat-belt clip, even though the plastic and metal are at the same temperature. The He (gas) 0.14

large heat flow from the metal into your finger pulls the methane (gas) 0.03

surface temperature of your finger close to the tempera- air 0.02

ture of the hot metal. Ouch!

Problem 7.30

Stone versus wood floors

Why, on a winter morning, do wood floors feel more comfortable than stone floors?

Problem 7.31

Mercury is special

Why does mercury (Hg) have such a low thermal conductivity for a metal?

7.5 Summary and further problems

In large, complex systems, the information is either overwhelming or not available. Then we have to reason with incomplete information. The tool for this purpose is probabilistic reasoning—in particular, Bayesian probability. Probabilistic reasoning helps us manage incomplete information. Using it, we can estimate the uncertainty in our divide-and-conquer estimates and understand the physics of random walks and thereby viscosity, boundary layers, and heat flow.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

7.5 Summary and further problems 277

Problem 7.32

Reynolds number as a ratio of two times

For an object moving through a fluid, the Reynolds number is defined as 𝑣𝐿/𝜈, where 𝑣 is the object's speed, 𝐿 is its size (a length), and 𝜈 is the fluid's kinematic viscosity. Show that the Reynolds number has the physical interpretation momentum-diffusion time over a distance comparable to the size 𝐿

fluid-transport time over a distance comparable to the size 𝐿

. (7.100)

Problem 7.33

Diamond is special

Diamond has a high thermal conductivity, much higher even than many metals.

The speed of sound in diamond is 12 kilometers per second, and diamond's specific heat 𝑐p is 0.63 kilojoules per kilogram kelvin. Use those values to estimate the mean free path of phonons in diamond, as an absolute length and in units of typical interatomic spacings. How does the mean free path in diamond compare to a typical phonon mean free path of a few lattice spacings?

Problem 7.34

Baking in three dimensions

Extend the fish-cooking argument of Section 7.3.3.2 to three dimensions to predict the baking time of a 6-kilogram turkey (assumed to be a sphere). How well does the time agree with experience (for example, with the data given in Problem 7.22)?

Problem 7.35

Resistive networks to analyze random walks Random walks are closely connected to infinite resistive networks (this connection is explored deeply in Random Walks and Electric Networks [11]). In particular, the probability of escape 𝑝esc—the probability that an 𝑛-dimensional random walker escapes to infinity and never returns to the origin—is related to the resistance 𝑅

to infinity of a 𝑛-dimensional electrical network of unit resistors: 𝑝esc = 1/2𝑛𝑅.

Use this connection, along with lumping arguments, to estimate 𝑅 and thereby show that the two-dimensional random walk is recurrent (𝑝esc = 0) but that the three-dimensional walk is transient (𝑝esc > 0)—consistent with Pólya's theorem (Problem 7.17).

Problem 7.36

Turning differential equations into algebraic equations The cold days of winter arrive, and the ice on a lake cold air (< 0 ◦C)

starts thickening as heat flows upward through the heat

ice, turning ever more water into ice. Find the scal-ice

ing exponent 𝛽 in

water (0 ◦C)

ice thickness ∝ (time)𝛽.

(7.101)

Problem 7.37

Thermal and electrical conductivities

Among the metals, the better thermal conductors, such as copper and gold in comparison to aluminum, iron, or mercury, are also the better electrical conductors.

(This connection is quantified in the Wiedemann-–Franz law.) What is the reason for this connection?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

278

7 Probabilistic reasoning

Problem 7.38

Teacup spindown

You stir your afternoon tea to mix the milk (and sugar, if you have a sweet tooth). Once you remove the stirring spoon, the rotation begins to slow. In this problem you'll estimate the spindown time

tea

𝜏: the time for the angular

l

velocity of the tea to fall by a significant fraction. To estimate 𝜏, consider a lumped teacup: a cylinder with height 𝑙

and diameter 𝑙, filled with liquid. Tea near the edge of the l

teacup—and near the base, but for simplicity neglect the effect of the base—is slowed by the presence of the edge (a result of the no-slip boundary condition).

a. In terms of the viscous torque 𝑇, the initial angular velocity 𝜔, and 𝜌 and 𝑙, estimate the spindown time 𝜏. Hint: Consider angular momentum, and drop all dimensionless constants, such as 𝜋 and 2.

b. To estimate the viscous torque 𝑇, use the result of Problem 7.25: viscous force = 𝜌𝜈 × velocity gradient × surface area.

(7.102)

The velocity gradient is determined by the boundary-layer thickness 𝛿. In terms of 𝛿, estimate the velocity gradient near the edge and then the torque 𝑇.

c. Put your expression for 𝑇 into your earlier estimate for 𝜏, which should now contain only one quantity that you have not yet estimated (the boundary-layer thickness 𝛿).

d. Estimate 𝛿 in terms of a growth time 𝑡, which is the time to rotate 1 radian.

After 1 radian, the fluid is moving in a significantly different direction, so the momentum fluxes from different regions no longer add constructively to the growth of the boundary layer.

e. Put the preceding results together to estimate the spindown time 𝜏: symboli-cally in terms of 𝜈, 𝜌, 𝑙, and 𝜔; and then numerically.

f. Stir your tea and estimate 𝜏 experimentally, and compare with your prediction.

Then enjoy a well-deserved cup.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8Easy cases

8.1 Warming up

279

8.2 Two regimes

281

8.3 Three regimes

291

8.4 Two dimensionless quantities

308

8.5 Summary and further problems

