## 0501. Dimensions

5.1 Dimensionless groups

139

5.2 One dimensionless group

147

5.3 More dimensionless groups

152

5.4 Temperature and charge

165

5.5 Atoms, molecules, and materials

175

5.6 Summary and further problems

192

In 1906, Los Angeles received 540 millimeters of precipitation (rain, snow, sleet, and hail).

Is this rainfall large or small?

On the one hand, 540 is a large number, so the rainfall is large. On the other hand, the rainfall is also 0.00054 kilometers, and 0.00054 is a tiny number, so the rainfall is small. These arguments contradict each other, so at least one must be wrong. Here, both are nonsense.

A valid argument comes from a meaningful comparison — for example, comparing 540 millimeters per year with worldwide average rainfall — which we estimated in Section 3.4.3 as 1 meter per year. In comparison to this rainfall, Los Angeles in 1906 was dry. Another meaningful comparison is with the average rainfall in Los Angeles, which is roughly 350 millimeters per year. In comparison, 1906 was a wet year in Los Angeles.

In the nonsense arguments, changing the units of length changed the result of the comparison. In contrast, the meaningful comparisons are independent of the system of units: No matter what units we select for length and time, the ratio of rainfalls does not change. In the language of symmetry, which we met in Chapter 3, changing units is the symmetry operation, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae


and meaningful comparisons are the invariants. They are invariant because they have no dimensions. When there is change, look for what does not change: Make only dimensionless comparisons.

This criterion is necessary for avoiding nonsense; however, it is not sufficient. To illustrate the difficulty, let's compare rainfall with the orbital speed of the Earth. Both quantities have dimensions of speed, so their ratio is invariant under a change of units. However, judging the wetness or dryness of Los Angeles by comparing its rainfall to the Earth's orbital speed produces nonsense.

Here is the moral of the preceding comparisons. A quantity with dimensions is, by itself, meaningless. It acquires meaning only when compared with a relevant quantity that has the same dimensions. This principle underlies our next tool: dimensional analysis.

Problem 5.1

Book boxes are heavy

In Problem 1.1, you estimated the mass of a small moving-box packed with books.

Modify your calculation to use a medium moving-box, with a volume of roughly 0.1 cubic meters. Can you think of a (meaningful!) comparison to convince someone that the resulting mass is large?

Problem 5.2

Making energy consumption meaningful

The United States' annual energy consumption is roughly 1020 joules. Suggest two comparisons to make this quantity meaningful. (Look up any quantities that you need to make the estimate, except the energy consumption itself!) Problem 5.3

Making solar power meaningful

In Problem 3.31, you should have found that the solar power falling on Earth is roughly 1017 watts. Suggest a comparison to make this quantity meaningful.

Problem 5.4

Energy consumption by the brain

The human brain consumes about 20 watts, and has a mass of 1–2 kilograms.

a. Make the power more meaningful by estimating the brain's fraction of the body's power consumption:

brain power

basal metabolism .

(5.1)

b. Make this fraction even more meaningful by estimating the ratio the brain's fraction of the body's power consumption the brain's fraction of the body's mass

.

(5.2)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.1 Dimensionless groups 139

Problem 5.5

Making oil imports meaningful

In Section 1.4, we estimated that the United States imports roughly 3×109 barrels of oil per year. This quantity needs a comparison to make it meaningful. As one possibility, estimate the ratio

cost of the imported oil

US military spending to「defend」oil-rich regions .

(5.3)

If this ratio is less than 1, suggest why the US government does not cancel that part of the military budget and use the savings to provide US consumers with free imported oil.

Problem 5.6

Making the energy in a 9-volt battery meaningful Using your estimate in Problem 1.11 for the energy in a 9–volt battery, estimate energy content of the battery

cost of the battery

.

(5.4)

Compare that quotient to the same quotient for electricity from the wall socket.

5.1 Dimensionless groups

Because dimensionless quantities are the only meaningful quantities, we can understand the world better by describing it in terms of dimensionless quantities. But we need to find them.

5.1.1 Finding dimensionless groups

v

To illustrate finding these dimensionless quantities, let's try an example that uses familiar physics: When learning a new r

idea, it is helpful to try it on a familiar example. We'll find a a

train's inward acceleration as it moves on a curved track. The larger the acceleration, the more the track or the train needs to tilt so that the passengers do not feel uncomfortable and (if the track is not tilted enough) the train does not tip over.

Our goal is the relation between the train's acceleration 𝑎, its speed 𝑣, and the track's radius of curvature 𝑟. In our state of knowledge now, the relation could be almost anything. Here are a few possibilities: 𝑎 + 𝑣2

𝑟

= 𝑣3𝑎;

𝑟 + 𝑎2

𝑣 = 𝑎2

𝑣 + 𝑟;

𝑣

𝑟𝑎 + 𝑣3 = 𝑎 + 𝑣

𝑟2 .

(5.5)

Although those possibilities are bogus, among the vast sea of possible relations, one relation is correct.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

140

5 Dimensions

To find the constraint that will shrink the sea to a few drops, first defocus our eyes and see all the choices as examples of the general form blob A

=

blob B

(5.6)

⏟⏟⏟⏟⏟

⏟⏟⏟⏟⏟

some function of

another function of

𝑎, 𝑣, and 𝑟

𝑎, 𝑣, and 𝑟

Even though the blobs might be complicated functions, they must have identical dimensions. By dividing both sides by blob B, we get a simpler form:

blob A

= 1.

(5.7)

blob B

Now each side is dimensionless. Therefore, whatever the relation between 𝑎, 𝑣, and 𝑟, we can write it in dimensionless form.

The preceding process is not limited to this problem. In any valid equation, all the terms have identical dimensions. For example, here is the total energy in a spring–mass system:

𝐸total = 12𝑚𝑣2 + 12𝑘𝑥2.

(5.8)

The kinetic-energy term (𝑚𝑣2/2) and the potential-energy term (𝑘𝑥2/2) have the same dimensions (of energy). The same process of dividing by one of the terms turns any equation into a dimensionless equation. As a result, any equation can be written in dimensionless form. Because the dimensionless forms are a small fraction of all possible forms, this restriction offers us a huge reduction in complexity.

To benefit from this reduction, we must compactly describe all such forms: Any dimensionless form can be built from dimensionless groups. A dimensionless group is the product of the quantities, each raised to a power, such that the product has no dimensions. In our example, where the quantities are 𝑎, 𝑣, and 𝑟, any dimensionless group 𝐺 has the form 𝐺 ≡ 𝑎𝑥𝑣𝑦𝑟𝑧,

(5.9)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.1 Dimensionless groups 141

where 𝐺 has no dimensions and where the exponents 𝑥, 𝑦, and 𝑧 are real numbers (possibly negative or zero).

Because any equation describing the world can be written in dimensionless form, and because any dimensionless form can be written using dimensionless groups, any equation describing the world can be written using dimensionless groups.

That news is welcome, but how do we find these groups?

The first step is to tabulate the quantities with their descrip- 𝑎 LT−2 acceleration tions and dimensions. By convention, capital letters are 𝑣 LT−1 speed used to represent dimensions. For now, the possible di- 𝑟 L

radius

mensions are length (L), mass (M), and time (T). Then, for example, the dimensions of 𝑣 are length per time or, more compactly, LT−1.

Then, by staring at the table, we find all possible dimensionless groups. A dimensionless group contains no length, mass, or time dimensions. For our example, let's start by getting rid of the time dimension. It occurs in 𝑎 as T−2 and in 𝑣 as T−1. Therefore, any dimensionless group must contain 𝑎/𝑣2.

This quotient has dimensions of L−1. To make it dimensionless, multiply it by the only quantity that is purely a length, which is the radius 𝑟. The result, 𝑎𝑟/𝑣2, is a dimensionless group. In the 𝑎𝑥𝑣𝑦𝑟𝑧 form, it is 𝑎1𝑣−2𝑟1.

Are there other dimensionless groups?

To get rid of time, we started with 𝑎/𝑣2 and then ended, inevitably, with the group 𝑎𝑟/𝑣2. To make another dimensionless group, we would have to choose another starting point. However, the only starting points that get rid of time are powers of 𝑎/𝑣2 — for example, 𝑣2/𝑎 or 𝑎2/𝑣4 — and those choices lead to the corresponding power of 𝑎𝑟/𝑣2. Therefore, any dimensionless group can be formed from 𝑎𝑟/𝑣2. Our three quantities 𝑎, 𝑟, and 𝑣 produce exactly one independent dimensionless group.

As a result, any statement about the circular acceleration can be written using only 𝑎𝑟/𝑣2. All dimensionless statements using only 𝑎𝑟/𝑣2 have the general form

𝑎𝑟

𝑣2 = dimensionless constant,

(5.10)

because there are no other independent dimensionless groups to use on the right side.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

142

5 Dimensions

Why can't we use 𝑎𝑟/𝑣2 on the right side?

We can, but it doesn't create new possibilities. As an example, let's try the following dimensionless form:

𝑎𝑟

𝑣2 = 3 ( 𝑎𝑟

𝑣2 ) − 1.

(5.11)

Its solution is 𝑎𝑟/𝑣2 = 1/2, which is another example of our general form 𝑎𝑟

𝑣2 = dimensionless constant.

(5.12)

But what if we use a more complicated function?

Let's try one:

𝑎𝑟

2 − 1.

(5.13)

𝑣2 = ( 𝑎𝑟

𝑣2 )

Its solutions are

𝑎𝑟

𝑣2 = { 𝜙,

−1/𝜙,

(5.14)

where 𝜙 is the golden ratio (1.618…). Deciding between these solutions would require additional information or requirements, such as the sign convention for the acceleration. Even so, each solution is another example of the general form

𝑎𝑟

𝑣2 = dimensionless constant.

(5.15)

Using that form, which we cannot escape, the acceleration of the train is 𝑎 ∼ 𝑣2𝑟,

(5.16)

where the ∼ contains the (unknown) dimensionless constant. In this case, the dimensionless constant is 1. However, dimensional analysis, as this procedure is called, does not tell us its value — which would come from a calculus analysis or, approximately, from a lumping analysis (Section 6.3.4).

Using 𝑎 ∼ 𝑣2/𝑟, we can now estimate the inward acceleration of the train going around a curve. Imagine a moderately high-speed train traveling at 𝑣 ≈ 60 meters per second (approximately 220 kilometers or 135 miles per hour). At such speeds, railway engineers specify that the track's radius of curvature be at least 2 or 3 kilometers. Using the smaller radius of curvature, the inward acceleration becomes

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.1 Dimensionless groups 143

𝑎 ∼ (60 m s−1)2 = 1.8 m s−2.

(5.17)

2×103 m

Because no quantity with dimensions is large or small on its own, this acceleration by itself is meaningless. It acquires meaning in θ

comparison with a relevant acceleration: the gravitational acceleration 𝑔. For this train, the dimensionless ratio 𝑎/𝑔 is approx- a imately 0.18. This ratio is also tan 𝜃, where 𝜃 is the train's tilt that would make the passengers feel a net force perpendicular to train

θ

the floor. With 𝑎/𝑔 ≈ 0.18, the comfortable tilt angle is approximately 10∘. Indeed, tilting trains can tilt up to 8∘. (This range is usually sufficient, as a full tilt is disconcerting: One would see g

a tilted ground but would still feel gravity acting as it normally does, along one's body axis.)

CM

Using our formula for circular acceleration, we can also es-m

v

timate the maximum walking speed. In walking, one foot is always in contact with the ground. As a rough model of walking, the whole body, represented as a point mass at its leg

center of mass (CM), pivots around the foot in contact with l

the ground — as if the body were an inverted pendulum. If you walk at speed 𝑣 and have leg length 𝑙, then the resulting circular acceleration (the acceleration toward the foot) is 𝑣2/𝑙. When you walk fast enough such that this acceleration is more than 𝑔, gravity cannot supply enough acceleration.

This change happens when 𝑣 ∼ 𝑔𝑙 . Then your foot leaves the ground, and the walk turns into a run. Therefore, gait is determined by the dimensionless ratio 𝑣2/𝑔𝑙. This ratio, which also determines the speed of water waves (Problem 5.15) and of ships (Problem 5.64), is called the Froude number and abbreviated 𝖥𝗋.

Here are three ways to check whether our pendulum model of walking is reasonable. First, the resulting formula,

𝑣max ∼ 𝑔𝑙 ,

(5.18)

explains why tall people, with a longer leg length, generally walk faster than short people.

Second, it predicts a reasonable maximum walking speed. With a leg length of 𝑙 ∼ 1 meter, the limit is 3 meters per second or about 7 miles per hour: 𝑣max ∼ 10 m s−2 × 1 m ≈ 3 m s−1.

(5.19)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

144

5 Dimensions

This prediction is consistent with world-record racewalking speeds, where the back toe may not leave the ground until the front heel has touched the ground. The world records for 20-kilometer racewalking are 1h:24m:50s for women and 1h:17m:16s for men. The corresponding speeds are 3.9 and 4.3 meters per second.

The third test is based on gait. In a fascinating experiment, Rodger Kram and colleagues [31] reduced the effective gravity 𝑔. This reduction changed the speed of the walking–running transition, but the speed still satisfied 𝑣2/𝑔𝑙 ∼ 0.5. The universe cares only about dimensionless quantities!

Another moral of this introduction to dimensional analysis is that ar/v2

every dimensionless group is an abstraction. Here, the group 𝑎𝑟/𝑣2 tells us that the universe cares about 𝑎, 𝑟, or 𝑣 through

−2

the combination 𝑎𝑟/𝑣2. This relation is described by the tree diagram (the edge label of −2 is the exponent of 𝑣 in 𝑣−2). Because a r

v

there is only one independent dimensionless group, the universe cares only about 𝑎𝑟/𝑣2. Therefore, the universe cares about 𝑎, 𝑟, and 𝑣 only through the combination 𝑎𝑟/𝑣2. This freedom not to worry about individual quantities simplifies our picture of the world.

5.1.2 Counting dimensionless groups

Finding the circular acceleration required finding all possible dimensionless groups and showing that all groups could be constructed from one group — say, 𝑎𝑟/𝑣2. That reasoning followed a chain of constraints: To get rid of the time, the dimensionless group had to contain the quotient 𝑎/𝑣2; to get rid of the length, the quotient needed to be multiplied by the correct power of 𝑟.

For each problem, do we have to construct a similar chain of reasoning in order to count the dimensionless groups?

Following the constraints is useful for finding dimensionless groups, but there is a shortcut for counting independent dimensionless groups. The number of independent groups is, roughly, the number of quantities minus the number of dimensions. A more precise statement will come later, but this version is enough to get us started.

Let's test it using the acceleration example. There are three quantities: 𝑎, 𝑣, and 𝑟. There are two dimensions: length (L) and time (T). There should be, and there is, one independent dimensionless group.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.1 Dimensionless groups 145

Let's also test the shortcut on a familiar physics formula: 𝑊 MLT−2 weight 𝑊 = 𝑚𝑔, where 𝑊 is an object's weight, 𝑚 is its mass, and 𝑔 𝑚 M

mass

is the gravitational acceleration. There are three quantities 𝑔 LT−2

gravity

(𝑊, 𝑚, and 𝑔) made from three dimensions (M, L, and T).

Our shortcut predicts no dimensionless groups at all. However, 𝑊/𝑚𝑔 is dimensionless, which refutes the prediction!

What went wrong?

Although the three quantities seem to contain three dimensions, the three dimensional combinations actually used — force (MLT−2), mass (M), and acceleration (LT−2) — can be constructed from just two dimensions. For example, we can construct them from mass and acceleration.

But acceleration is not a fundamental dimension, so how can we use it?

The notion of fundamental dimensions is a human convention, part of our system of measurement. Dimensional analysis, however, is a mathematical process. It cares neither about the universe nor about our conventions for describing the universe. That lack of care may appear heartless and seem like a disadvantage. However, it means that dimensional analysis is independent of our arbitrary choices, giving it power and generality.

As far as dimensional analysis is concerned, we can choose 𝑊 M × [𝑎] weight any set of dimensions as our fundamental dimensions. The 𝑚 M

mass

only requirement is that they suffice to describe the dimen- 𝑔

[𝑎]

gravity

sions of our quantities. Here, mass and acceleration suffice, as the rewritten dimensions table shows: Using the notation [𝑎] for「the dimensions of 𝑎,」the dimensions of 𝑊 are M × [𝑎] and the dimensions of 𝑔 are just [𝑎].

In summary, the three quantities contain only two independent dimensions.

Three quantities minus two independent dimensions produce one independent dimensionless group. Accordingly, the revised counting shortcut is number of quantities

− number of independent dimensions

(5.20)

number of independent dimensionless groups

This shortcut, known as the Buckingham Pi theorem [4], is named after Edgar Buckingham and his uppercase Pi (Π) notation for dimensionless groups. (It is also the rank–nullity theorem of linear algebra [42].) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

146

5 Dimensions

Problem 5.7

Bounding the number of independent dimensionless groups Why is the number of independent dimensionless groups never more than the number of quantities?

Problem 5.8

Counting dimensionless groups

How many independent dimensionless groups do the following sets of quantities produce?

a. period 𝑇 of a spring–mass system in a gravitational field: 𝑇, 𝑘 (spring constant), 𝑚, 𝑥0 (amplitude), and 𝑔.

b. impact speed 𝑣 of a free-falling object: 𝑣, 𝑔, and ℎ (initial drop height).

c. impact speed 𝑣 of a downward-thrown free-falling object: 𝑣, 𝑔, ℎ, and 𝑣0 (launch velocity).

Problem 5.9

Using angular frequency instead of speed

Redo the dimensional-analysis derivation of circular acceleration using the radius 𝑟 and the angular frequency 𝜔 as independent variables. Using 𝑎 = 𝑣2/𝑟, find the dimensionless constant in the general dimensionless form dimensionless group proportional to 𝑎 = dimensionless constant.

(5.21)

Problem 5.10

Impact speed of a dropped object

Use dimensional analysis to estimate the impact speed of a freely falling rock that is dropped from a height ℎ.

Problem 5.11

Speed of gravity waves on deep water

In this problem, you use dimensional analysis to 𝑣 LT−1 wave speed find the speed of waves on the open ocean. These 𝑔 LT−2 gravity waves are the ones you would see from an airplane and are driven by gravity. Their speed could de- 𝜔

T−1

angular freq.

pend on gravity 𝑔, their angular frequency 𝜔, and 𝜌

ML−3

water density

the density of water 𝜌. Do the analysis as follows.

a. Explain why these quantities produce one independent dimensionless group.

b. What is the group proportional to 𝑣?

c. With the further information that the dimensionless constant is 1, predict the speed of waves with a period of 17 seconds (you can measure the period by timing the interval between each wave's arrival at the shore). This speed is also the speed of the winds that produced the waves. Is it a reasonable wind speed?

d. What would the dimensionless constant be if, in the table of quantities, angular frequency 𝜔 is replaced by the period 𝑇?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.2 One dimensionless group 147

Problem 5.12

Using period instead of speed

In finding a formula for circular acceleration (Section 5.1.1), our independent variables were the radius 𝑟 and the speed 𝑣. Redo the dimensional-analysis derivation using the radius 𝑟 and the period 𝑇 as the independent variables.

a. Explain why there is still only one independent dimensionless group.

b. What is the independent dimensionless group proportional to 𝑎?

c. What dimensionless constant is this group equal to?

5.2 One dimensionless group

The most frequent use of dimensional analysis involves one independent dimensionless group — for example, 𝑎𝑟/𝑣2 in our analysis of circular acceleration (Section 5.1.1). Let's look at this kind of case more closely, which has lessons for more complicated problems.

5.2.1 Universal constants

What we will find is that dimensional analysis reduces complexity by generating results with wide application. That is, in the general form l

independent dimensionless group = dimensionless constant, (5.22) θ 0

the dimensionless constant is universal. Let's see what universal means m

through an example — the analysis of a small-amplitude pendulum. So, imagine releasing a pendulum from a small angle 𝜃0.

What is its period of oscillation?

The first step in dimensional analysis is to list the relevant 𝑇 T

period

quantities. The list begins with the goal quantity — here, 𝑔 LT−2 gravity the period 𝑇. It depends on gravity 𝑔, the string length 𝑙 L

string length

𝑙, perhaps the mass 𝑚 of the bob, and perhaps the ampli- 𝑚 M

mass of bob

tude 𝜃0. Fortunately, when the amplitude is small, as it is here, then the amplitude turns out not to matter, so we won't list it.

What are the dimensionless groups?

These four quantities contain three independent dimensions (M, L, and T).

By the Buckingham Pi theorem (Section 5.1.2), they produce one independent dimensionless group. This group cannot contain 𝑚, because 𝑚 is the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

148

5 Dimensions

only quantity with dimensions of mass. A simple dimensionless group is 𝑔𝑇2/𝑙. However, because our eventual goal is the period 𝑇, let's make a dimensionless group proportional to 𝑇 itself rather than to 𝑇2. This group is 𝑇 𝑔/𝑙 . Then the most general dimensionless statement is 𝑇 𝑔𝑙 = 𝐶,

(5.23)

where 𝐶 is a dimensionless constant. Even though its value is, for the moment, unknown, it is universal. The same constant applies to a pendulum with a shorter string or, perhaps more surprisingly, to a pendulum on Mars, with its different gravitational strength. If we find the constant for one pendulum on one planet, we know it for all pendulums on all planets.

There are at least three ways to find 𝐶. The first is to solve the pendulum differential equation — which is hard work. The second approach is to solve a cleverly designed simpler problem (Problem 3.4). Although the approach is clever, it is not as general as the third method.

The third method is to measure 𝐶 with a home experiment! For that purpose, I turned my key ring into a pendulum by hanging it from a string. The string was roughly twice the length of American letter paper l

(thus, 2 × 11 inches) and the period was roughly 1.5 seconds. Therefore, 𝐶 = 𝑇 𝑔𝑙 ≈ 1.5s × 32fts−2

2 ft

= 6.

(5.24)

key ring

Would the constant be different in a modern system of units?

In metric units, 𝑔 ≈ 9.8 meters per second per second, 𝑙 ≈ 0.6 meters, and 𝐶 is, within calculation inaccuracies, still 6: 𝐶 ≈ 1.5 s × 9.8 m/s2

0.6 m ≈ 6.

(5.25)

The system of units does not matter — which is the reason for using dimensionless groups: They are invariant under a change of units. Even so, an explicit 6 probably would not appear if we solved the pendulum differential equation honestly. But a more precise measurement of 𝐶 might suggest a closed form for this dimensionless constant.

The pendulum length, from the knot where I hold it to the center of the key ring is 0.65 meters (slightly longer than the rough estimate of 0.6 meters).

Meanwhile, 10 periods took 15.97 seconds. Then 𝐶 is close to 6.20: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.2 One dimensionless group 149

𝐶 ≈ 1.597 s × 9.8 m s−2

0.65 m ≈ 6.20.

(5.26)

What dimensionless numbers could produce 6.20?

This value is close to 2𝜋, which is approximately 6.28. That guess feels like a leap, but have courage. The guess is plausible once we remember that pendulums oscillate and oscillations often involve 2𝜋, or that we are asking for the period rather than the angular frequency, a choice that often introduces a 2𝜋 (as in Problem 5.11(d)). The resulting period 𝑇 is 𝑇 = 𝐶 𝑙𝑔 = 2𝜋 𝑙𝑔 .

(5.27)

(For a physical explanation of the 2𝜋, try Problem 3.4.) This example shows how dimensional analysis, a mathematical approach, sits between two physical approaches. First we used our physical knowledge to list the relevant quantities. Then we reduced the space of possible relations by using dimensional analysis. Finally, to find the universal constant 𝐶, which dimensional analysis could not tell us, we again used physical knowledge (a home experiment).

Problem 5.13

Your own measurement

Make your own pendulum and measure the universal constant 𝑇 𝑔/𝑙 .

Problem 5.14

Period of a spring–mass system

Use dimensional analysis to find, except for a dimensionless constant, the period 𝑇 of a spring–mass system with spring constant 𝑘, mass 𝑚, and amplitude 𝑥0. Find the dimensionless constant in the most general dimensionless statement group proportional to 𝑇 = dimensionless constant.

(5.28)

Problem 5.15

Speed of waves in shallow water

In shallow water, where the wavelength is much larger than the depth, waves driven by gravity travel at a speed that could depend on gravity 𝑔, the water depth ℎ, and the density of water 𝜌.

a. Find the independent dimensionless group proportional to 𝑣2, where 𝑣 is the wave speed. Compare this group to the Froude number, the dimensionless ratio that we introduced to study walking (Section 5.1.1).

b. What therefore is the scaling exponent 𝛽 in the scaling relation 𝑣 ∝ ℎ𝛽? Test your prediction by measuring 𝑣(1 cm) and 𝑣(4 cm). To make the measurement, fill 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

150

5 Dimensions

a baking dish with water and excite a sloshing wave by slightly lifting and quickly setting down one end of the dish.

c. Using your data, estimate the universal (dimensionless) constant in the relation dimensionless group from part (a) = dimensionless constant.

(5.29)

d. Predict the speed of tidal waves, which are (shallow-water!) waves created by underwater earthquakes. How long does a tidal wave take to cross an ocean?

5.2.2 Atomic blast energy

Problems with only one dimensionless group need not be simple or 𝑡 (ms) 𝑅 (m) easy to by other methods. A classic example is finding the energy released by the first atomic bomb, detonated in the New Mexico desert 3.26

59.0

in 1945. The blast energy, or yield, was top secret. Yet declassified 4.61

67.3

photographs of the blast, because they had a scale bar, provided data 15.0

106.5

on the radius of the fireball at several times after the explosion. The 62.0

185.0

data must have seemed innocuous enough to release.

But from these data, G. I. Taylor of Cambridge University predicted the yield [44]. The analysis, like many calculations in R

fluid mechanics, is long and complicated. We'll instead use dimensional analysis to find the relation between the blast radius 𝑅, the time 𝑡 since the blast, the blast energy 𝐸, and the air density 𝜌.

Then we'll use the 𝑅(𝑡) data to predict 𝐸.

These four quantities contain three independent di- 𝐸 ML2T−2 blast energy mensions. Thus, they produce one independent di- 𝑅 L

blast radius

mensionless group. To find it, let's eliminate one 𝑡

T

time since blast

dimension at a time. Here, a bit of luck simplifies 𝜌air ML−3

air density

the process, because we have dimensions that are easy to eliminate.

Do any dimensions occur in only one or two quantities?

Yes: Mass occurs in 𝐸 as M1 and in 𝜌air also as M1; time appears in 𝐸 as T−2

and in 𝑡 as T1. Therefore, to eliminate mass, the dimensionless group must contain 𝐸/𝜌air. To eliminate time, the dimensionless group must contain 𝐸𝑡2.

Thus, 𝐸𝑡2/𝜌air eliminates mass and time. Because it has dimensions of L5, the only way to remove these dimensions without introducing any powers of time or mass is to divide by 𝑅5. The result, 𝐸𝑡2/𝜌air𝑅5, is an independent 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.2 One dimensionless group 151

dimensionless group. It is also the only dimensionless group proportional to our goal, the blast energy 𝐸.

With only one dimensionless group, the most general dimensionless statement about the blast energy is

𝐸𝑡2

𝜌air𝑅5 ∼ 1.

(5.30)

For a particular explosion, 𝐸 is fixed (although unknown), as is 𝜌air. Therefore, these quantities drop out of the corresponding scaling relation, which becomes 𝑡2 ∝ 𝑅5 or 𝑅 ∝ 𝑡2/5. On log–log axes, the data on the blast radius should fall along a line of slope 2/5 — as they almost exactly do: 185

R (m)

106.5

0.4 slope

67.3

59

t (ms)

3.26

4.61

15

62

With the dimensional analysis result 𝐸𝑡2/𝜌air𝑅5 ∼ 1, each point predicts a blast energy according to 𝐸 ∼ 𝜌air𝑅5/𝑡2. Using 1 kilogram per cubic meter for 𝜌air, the 𝐸 estimates lie between 5.6 and 6.7 ×1013 joules. Unfortunately for judging the accuracy of the estimate, joules are an unfamiliar unit for the energy of a bomb blast. The familiar unit is tons of TNT.

What is the predicted blast energy as a mass of TNT?

One gram of TNT releases 1 kilocalorie or roughly 4 kilojoules. It contains only one-fourth the energy density of sugar, but the energy is released much more rapidly! One kiloton is 109 grams, which release 4×1012 joules.

Our predicted yield of 6×1013 joules is thus roughly 15 kilotons of TNT.

Just for fun, if we reestimate the yield using a more accurate air density of 1.2 kilograms per cubic meter, the blast energy would be 18 kilotons. This result is shockingly accurate considering the number of approximations it contains: The classified yield was 20 kilotons. (The missing universal constant for shock-wave explosions must be very close to 1.) Dimensional analysis is powerful!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

152

5 Dimensions

5.3 More dimensionless groups

The biggest change in dimensional analysis comes with a second independent dimensionless group. With only one dimensionless group, the most general statement that the universe could make was dimensionless group ∼ 1.

(5.31)

With a second group, the universe gains freedom on the right side: group 1 = 𝑓 (group 2),

(5.32)

where 𝑓 is a dimensionless function: It takes a dimensionless number as its input, and it produces a dimensionless number as its output.

As an example of two independent dimensionless groups, let's extend the analysis of Problem 5.10, where you predicted the impact speed of a rock dropped from a height ℎ. The impact speed depends on 𝑔 and ℎ, so a reasonable choice for the independent dimensionless group is 𝑣/ 𝑔ℎ. Therefore, its value is a universal, dimensionless constant (which turns out to be 2).

To make a second independent dimensionless group, we add a degree of freedom to the problem: that the rock is thrown downward with speed 𝑣0

(the previous problem is the case 𝑣0 = 0).

With this complication, what are independent dimensionless groups?

Adding a quantity but no new independent dimension creates one more independent dimensionless group. Therefore, there are two independent groups — for example, 𝑣/ 𝑔ℎ and 𝑣0/ 𝑔ℎ. The most general dimensionless statement, which has the form group 1 = 𝑓 (group 2), is 𝑣 = 𝑓 ⎛⎜ 𝑣0 ⎞⎟.

(5.33)

𝑔ℎ

⎝ 𝑔ℎ ⎠

This point is as far as dimensional analysis can take us. To go further requires adding physics knowledge (Problem 5.16). But dimensional analysis already tells us that this function 𝑓 is a universal function: It describes the impact speed of every thrown object in the universe, no matter the launch velocity, the drop height, or the gravitational field strength.

Problem 5.16

Impact speed of a thrown rock

For a rock thrown downward with speed 𝑣0, use conservation of energy to find the form of the dimensionless function 𝑓 in 𝑣/ 𝑔ℎ = 𝑓 (𝑣0/ 𝑔ℎ).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 153

Problem 5.17

Nonideal spring

Imagine a mass connected to a spring with force law T

A

B

𝐹 ∝ 𝑥3 (instead of the ideal-spring force 𝐹 ∝ 𝑥) and therefore with potential energy 𝑉 ∼ 𝐶𝑥4 (where 𝐶 is a C

constant). Which curve shows how the system's oscil-D

lation period

E

𝑇 depends on the amplitude 𝑥0?

x

0

0

0

Problem 5.18

Rolling down the plane

In this problem, you use dimensional analysis to simplify finding the acceleration of a ring rolling (without slipping) down an inclined plane.

θ

a. List the quantities on which the ring's acceleration depends. Hint: Include the ring's moment of inertia and its radius. Do you also need to include its mass?

b. Form independent dimensionless groups to write the dimensionless statement group proportional to 𝑎 = 𝑓 (groups not containing 𝑎).

(5.34)

c. Does a bigger ring roll faster than a smaller ring?

d. Does a denser ring roll faster than a less dense ring (of the same radius)?

5.3.1 Bending of starlight by the Sun

Our next example of two independent dimensionless groups — the deflection of starlight by the Sun — will illustrate how to incorporate physical knowledge into the mathematical results from dimensional analysis.

Rocks, birds, and people feel the effect of gravity. So why not light? The analysis of its deflection is a triumph of Einstein's theory of general relativity. However, the theory is based on ten coupled, nonlinear partial-differential equations. Rather than solving these difficult equations, let's use dimensional analysis.

Because this problem is more complicated than the previous examples, let's organize the complexity by making the steps explicit, including the step of incorporating physical knowledge. Divide and conquer!

1. List the relevant quantities.

2. Form independent dimensionless groups.

3. Use the groups to make the most general statement about deflection.

4. Narrow the possibilities by incorporating physical knowledge.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

154

5 Dimensions

Step 1: Listing relevant quantities

In the first step, we think of and list the quantities that determine the bending. To find them, I often draw a diagram with verbal but without quantitative labels. As the diagram cries out for quantitative labels, it suggests quantities for the list.

apparent

position

eye

star

starlight

Sun

The bent path means that the star shifts its apparent position. The shift is most naturally measured not as an absolute distance but rather as an angle 𝜃. For example, if 𝜃 = 180∘ (𝜋 radians), much larger than the likely deflection, the star would be shifted halfway around the sky.

The labels and the list must include our goal, which 𝜃

1

angle

is the deflection angle 𝜃. Because deflection is pro- 𝐺𝑚 L3T−2 Sun's gravity duced by gravity, we should also include Newton's 𝑟

L

closest approach

gravitational constant 𝐺 and the Sun's mass 𝑚 (we'll use the more general symbol 𝑚 rather than 𝑀Sun, because we may apply the formula to light paths around other stellar objects). These quantities could join the list as two separate quantities. However, the physical consequences of gravity — for example, the gravitational force — depend on 𝐺 and 𝑚 only through the product 𝐺𝑚. Therefore, let's include just the 𝐺𝑚 abstraction on the list. (Problem 5.19 shows you how to find its dimensions.) The final quantity on the list is based on our knowledge that gravity gets weaker with distance. Therefore, we include the distance from the Sun to the light beam. The phrase「distance from the Sun」is ambiguous, because the beam is at various distances. Our quantity 𝑟 will be the shortest distance from the center of the Sun to the beam (the distance of closest approach).

apparent

position

θ

eye

star

starlight

r

Sun

mass m

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 155

Problem 5.19

Dimensions of 𝑮𝒎 and 𝑮

Use Newton's law of universal gravitation, 𝐹 = 𝐺𝑚1𝑚2/𝑟2, to find the dimensions of 𝐺𝑚 and 𝐺.

Step 2: Form independent dimensionless groups The second step is to form independent dimensionless groups. One group is easy: The angle 𝜃 is already dimensionless. Unfortunately, three quantities and two independent dimensions (L and T) produce only one independent dimensionless group. With only one dimensionless group, the most general statement is merely 𝜃 = constant.

This prediction is absurd. The bending, if it is produced by gravity, has to depend on 𝐺𝑚 and 𝑟. These quantities have to appear in a second dimensionless group. Creating a second group, we know from the Buckingham Pi theorem, requires at least one more quantity. Its absence indicates that our analysis is missing essential physics.

What physics is missing?

No quantity so far distinguishes between the path 𝜃

1

angle

of light and of, say, a planet. A crucial difference 𝐺𝑚 L3T−2 Sun's gravity is that light travels far more rapidly than a planet. 𝑟

L

closest approach

Let's represent this important characteristic of light 𝑐

LT−1

speed of light

by including the 𝑐.

This quantity, a speed, does not introduce a new independent dimension (it uses length and time). Therefore, it increases the number of independent dimensionless groups by one, from one to two. To find the new group, first check whether any dimension appears in only two quantities. If it does, the search simplifies. Time appears in only two quantities: in 𝐺𝑚 as T−2 and in 𝑐 as 𝑇−1. To cancel out time, the new dimensionless group must contain 𝐺𝑚/𝑐2. This quotient contains one power of length, so our dimensionless group is 𝐺𝑚/𝑟𝑐2.

As we hoped, the new group contains 𝐺𝑚 and 𝑟. Its form illustrates again that quantities with dimensions are not meaningful alone. For knowing just 𝐺𝑚 is not enough to decide whether or not gravity is strong. As a quantity with dimensions, 𝐺𝑚 must be compared to another relevant quantity with the same dimensions. Here, that quantity is 𝑟𝑐2, and the comparison leads to the dimensionless ratio 𝐺𝑚/𝑟𝑐2.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

156

5 Dimensions

Can we choose other pairs of independent dimensionless groups?

Yes. For example, 𝜃 and 𝐺𝑚𝜃/𝑟𝑐2 also make a set of independent dimensionless groups. Mathematically, all pairs of independent dimensionless groups are equivalent, in that any pair can represent any quantitative statement about light bending.

However, look ahead to the goal: We hope to solve for 𝜃. If 𝜃 appears in both groups, we will end up with an implicit equation for 𝜃, where 𝜃 appears on both sides of the equals sign. Although such an equation is mathematically legitimate, it is much harder to think about and to solve than is an explicit equation, where 𝜃 is on the left side only.

Therefore, when choosing independent dimensionless groups, place the goal quantity in only one group. This rule of thumb does not remove all our freedom in choosing the groups, but it greatly limits the choices.

Problem 5.20

Physical interpretation of the new group

Interpret the dimensionless group 𝐺𝑚/𝑟𝑐2 by multiplying by 𝑚light/𝑚light and re-grouping the quantities until you find physical interpretations for the numerator and denominator.

Step 3: Make the most general dimensionless statement The third step is to use the independent dimensionless groups to write the most general statement about the bending angle. It has the form group 1 =

𝑓 (group 2). Here,

𝜃 = 𝑓 (𝐺𝑚

𝑟𝑐2 ) ,

(5.35)

where 𝑓 is a universal, dimensionless function. Dimensional analysis cannot determine 𝑓 . However, it has told us that 𝑓 is a function only of 𝐺𝑚/𝑟𝑐2

and not of the four quantities 𝐺, 𝑚, 𝑟, and 𝑐 separately. That information is the great simplification.

Step 4: Use physical knowledge to narrow the possibilities The space of possible functions — here, all nonpathological functions of one variable — is vast. Therefore, the fourth and final step is to narrow the possibilities for 𝑓 by incorporating physical knowledge. First, imagine increasing the effect of gravity by increasing the mass 𝑚 — which increases 𝐺𝑚/𝑟𝑐2.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 157

This change should, based on our physical intuition about gravity, also increase the bending angle. Therefore, 𝑓 should be a monotonically increasing function of 𝐺𝑚/𝑟𝑐2. Second, imagine an antigravity world, where the gravitational constant 𝐺 is negative. Then the Sun would deflect light away from it, making the bending angle negative. In terms of 𝑥 ≡ 𝐺𝑚/𝑟𝑐2, this constraint eliminates even functions of 𝑥, such as 𝑓 (𝑥) ∼ 𝑥2, which produce the same sign for the bending angle independent of the sign of 𝑥.

The simplest function meeting both the monotonicity and sign constraints is 𝑓 (𝑥) ∼ 𝑥. In terms of the second group 𝐺𝑀/𝑟𝑐2, the form 𝑓 (𝑥) ∼ 𝑥 is the dimensionless statement about bending

𝜃 ∼ 𝐺𝑚

𝑟𝑐2 .

(5.36)

All reasonable theories of gravity will predict this relation, because it is almost entirely a mathematical requirement. The theories differ only in the dimensionless factor hidden in the single approximation sign ∼:

⎧{1 (simplest guess);

𝜃 = 𝐺𝑚

2 (Newtonian gravity);

(5.37)

𝑟𝑐2 × ⎨{⎩4 (general relativity).

The factor of 2 for Newtonian gravity results from solving for the trajectory of a rock roving past the Sun with speed 𝑐. The factor of 4 for general relativity, double the Newtonian value, results from solving the ten partial-differential equations in the limit that the gravitational field is weak.

How large are these angles?

Let's first estimate the bending angles closer to home — produced by the Earth's gravity. For a light ray just grazing the surface of the Earth, the bending angle (in radians!) is roughly 10−9: 𝐺

𝑚Earth

⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞

𝜃

6.7 ×10−11 kg−1 m3 s−2 × 6×1024 kg

Earth ∼

≈ 0.7 ×10−9.

(5.38)

6.4

⏟⏟ ×

⏟ 106

⏟ m

⏟⏟⏟ × 1017 m2 s−2

⏟⏟⏟⏟⏟⏟⏟

𝑅Earth

𝑐2

Can we observe this angle?

The bending angle is the angular shift in the position of the star making the starlight. To observe these shifts, astronomers compare a telescope picture of the star and surrounding sky, with and without the deflection. A 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

158

5 Dimensions

telescope with lens of diameter 𝐷 can resolve angles roughly as small as 𝜆/𝐷, where 𝜆 is the wavelength of light. As a result, a lens that can resolve 0.7 ×10−9 radians has a diameter of at least 700 meters: 𝐷 ∼ 𝜆

𝜃

∼ 0.5×10−6 m

Earth

0.7 ×10−9 ≈ 700 m.

(5.39)

On its own, this length does not mean much. However, the largest telescope lens has a diameter of roughly 1 meter; the largest telescope mirror, in a different telescope design, is still only 10 meters. No practical lens or mirror can be 700 meters in diameter. Thus, there is no way to see the deflection produced by the Earth's gravitational field.

Physicists therefore searched for a stronger source of light bending. The bending angle is proportional to 𝑚/𝑟. The largest mass in the solar system is the Sun. For a light ray grazing the surface of the Sun, 𝑟 = 𝑅Sun and 𝑚 = 𝑀Sun. So the ratio of Sun-to-Earth-produced bending angles is 𝜃

−1

Sun

𝜃

= 𝑀Sun × ( 𝑅Sun ) .

(5.40)

Earth

𝑚Earth

𝑅Earth

The mass ratio is roughly 3 × 105; the radius ratio is roughly 100. The ratio of deflection angles is therefore roughly 3000. The required lens diameter, which is inversely proportional to 𝜃, is correspondingly smaller than 700 meters by a factor of 3000: roughly 25 centimeters or 10 inches. That lens size is plausible, and the deflection might just be measurable.

Between 1909 and 1916, Einstein believed that a correct theory of gravity would predict the Newtonian value of 4.2×10−6 radians or 0.87 arcseconds: 0.7

⏟⏟×

⏟10−9

⏟ r

⏟ad

⏟⏟ ×

2

⏟

× 3000

⏟ ∼ 4.2×10−6 rad.

(5.41)

∼𝜃Earth

Newtonian gravity

𝜃Sun/𝜃Earth

The German astronomer Soldner had derived the same result in 1803. The eclipse expeditions to test his (and Soldner's) prediction got rained out or clouded out. By the time an expedition got lucky with the weather, in 1919, Einstein had invented a new theory of gravity — general relativity — and it predicted a deflection twice as large, or 1.75 arcseconds.

The eclipse expedition of 1919, led by Arthur Eddington of Cambridge University and using a 13-inch lens, measured the deflection. The measurements are difficult, and the results were not accurate enough to decide clearly which theory was right. But 1919 was the first year after World War One, in which Germany and Britain had fought each other almost to obliv-ion. A theory invented by a German, confirmed by an Englishman (from 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 159

Newton's university, no less) — such a picture was welcome after the war.

The world press and scientific community declared Einstein vindicated.

A proper confirmation of Einstein's prediction came only with the advent of radio astronomy, which allowed small deflections to be measured accurately (Problem 5.21). The results, described as the dimensionless factor multiplying 𝐺𝑚/𝑟𝑐2, were around 4 ± 0.2 — definitely different from the Newtonian prediction of 2 and consistent with general relativity.

Problem 5.21

Accuracy of radio-telescope measurements

The angular resolution of a telescope is 𝜆/𝐷, where 𝜆 is the wavelength and 𝐷 is the telescope's diameter. But radio waves have a much longer wavelength than light.

How can measurements of the bending angle that are made with radio telescopes be so much more accurate than measurements made with optical telescopes?

Problem 5.22

Another theory of gravity

An alternative to Newtonian gravity and to general relativity is the Brans–Dicke theory of gravitation [3]. Look up what it predicts for the angle that the Sun would deflect starlight. Express your answer as the dimensionless prefactor in 𝜃 ∼ 𝐺𝑚/𝑟𝑐2.

5.3.2 Drag

Even more difficult than the equations of general relativity, which at least have been solved for realistic problems, are the Navier–Stokes equations of fluid mechanics. We first met them in Section 3.5, where their complexity pushed us to find an alternative to solving them directly. We used a conservation argument, which we tested using a falling cone, and concluded that the drag force on an object traveling through a fluid is 𝐹drag ∼ 𝜌𝑣2𝐴cs,

(5.42)

where 𝜌 is the density of the fluid, 𝑣 is the speed of the object, and 𝐴cs is its cross-sectional area. This result is the starting point for our dimensional analysis.

With 𝐹drag dependent on 𝜌, 𝑣, and 𝐴cs, there are four quantities and three independent dimensions. Therefore, by the Buckingham Pi theorem, there is one independent dimensionless group. Our expression for the drag force already gives one such group:

𝐹drag .

(5.43)

𝜌𝑣2𝐴cs

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

160

5 Dimensions

Because the 𝜌𝑣2 in the denominator looks like 𝑚𝑣2 in kinetic energy, a factor of one-half is traditionally included in the denominator: 𝐹

group 1 ≡

drag .

1

(5.44)

2 𝜌𝑣2𝐴cs

The resulting dimensionless group is called the drag coefficient 𝑐d.

𝐹

𝑐

drag

d ≡ 1

(5.45)

2 𝜌𝑣2𝐴cs

As the only dimensionless group, it has to be a constant: There is no other group on which it could depend. Therefore,

𝐹drag = dimensionless constant.

1

(5.46)

2 𝜌𝑣2𝐴cs

This result is equivalent to our prediction based on conservation of energy, that 𝐹drag ∼ 𝜌𝑣2𝐴cs. However, trouble happens when we wonder about the dimensionless constant's value.

Dimensional analysis, as a mathematical technique, cannot predict the constant. Doing so requires physical reasoning, which starts with the observation that drag consumes energy. Here, no quantity on which 𝐹drag depends — namely, 𝜌, 𝑣, or 𝐴cs — represents a mechanism of energy loss. Therefore, the drag coefficient should be zero. Although this value is consistent with the prediction that the drag coefficient is constant, it contradicts all our experience of fluids!

Our analysis needs to include a mechanism of energy loss. In fluids, loss is due to viscosity (for an object moving at a constant speed and generating no waves). Its physics is the topic of Section 7.3.2, as an example of a diffusion constant. For our purposes here, we need just its dimensions in order to incorporate viscosity into a dimensionless group: The dimensions of kinematic viscosity 𝜈 are L2T−1. (Unfortunately, in almost every font, the standard symbols for velocity and kinematic viscosity, 𝑣 and 𝜈, look similar; however, even more confusion would result from selecting new symbols.) Thus, the kinematic viscosity joins our list. Adding one quantity without adding a new independent dimension creates a new independent dimensionless group. Similarly, in our analysis of the deflection of starlight (Section ), adding the speed of light 𝑐 created a second independent dimensionless group.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 161

What is this new group containing viscosity?

Before finding the group, look ahead to how it will be used. With a second group, the most general statement has the form group 1

⏟⏟⏟⏟⏟ = 𝑓 (group 2).

(5.47)

𝑐d

Our goal is 𝐹drag, which is already part of group 1. Including 𝐹drag also in group 2 would be a bad tactic, because it would produce an equation with 𝐹drag on both sides and, additionally, wrapped on the right side in the unknown function 𝑓 . Keep 𝐹drag out of group 2.

To make this group from the other quantities 𝑣, 𝐴cs, 𝜌, 𝑣 LT−1 speed and 𝜈, look for dimensions that appear in only one or 𝐴cs L2

area

two quantities. Mass appears only in the density; thus, 𝜌 ML−3 fluid density the density cannot appear in group 2: If it were part of 𝜈 L2T−1 viscosity group 2, there would be no way to cancel the dimensions of mass, and group 2 could not be dimensionless.

Time appears in two quantities: speed 𝑣 and viscosity 𝜈. Because each quantity contains the same power of time (T−1), group 2 has to contain the quotient 𝑣/𝜈 — otherwise the dimensions of time would not cancel.

Here's what we know so far about this dimensionless group: So that mass disappears, it cannot contain the density 𝜌; so that time disappears, it must contain 𝑣 and 𝜈 as their quotient 𝑣/𝜈. The remaining task is to make length disappear — for which purpose we use the object's cross-sectional area 𝐴cs.

The quotient 𝑣/𝜈 has dimensions of L−1, so 𝐴cs 𝑣/𝜈 is a new, independent dimensionless group.

Instead of 𝐴cs , usually one uses the diameter 𝐷. With that choice, our group 2 is called the Reynolds number 𝖱𝖾:

𝖱𝖾 ≡ 𝑣𝐷

𝜈 .

(5.48)

The conclusion from dimensional analysis is then drag coefficient

⏟⏟⏟⏟⏟⏟⏟⏟⏟ = 𝑓 ( Reynolds number

⏟⏟⏟⏟⏟⏟⏟⏟⏟ ).

(5.49)

𝑐d

𝖱𝖾

For each shape, the dimensionless function 𝑓 is a universal function; it depends on the shape of the object, but not on its size. For example, a sphere, a cylinder, and a cone have different functions 𝑓sphere, 𝑓cylinder, and 𝑓cone. Similarly, a narrow-angle cone and a wide-angle cone have different functions.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

162

5 Dimensions

But a small and a large sphere are described by the same function, as are a large and a small cone of the same opening angle. Any difference in the drag coefficients for different-sized objects of the same shape results only from the difference in Reynolds numbers (different because the sizes are different).

Here we see the power of dimensional analysis.

Reynolds number vD/ ν

It shows us that the universe doesn't care about the size, speed, or viscosity individually. The uni-

−1

verse cares about them only through the abstraction known as the Reynolds number. It is the only speed v size D

viscosity ν

information needed to determine the drag coefficient (for a given shape).

Now let's use this dimensionless framework to analyze the cone experiment: The experimental data showed that the small and large cones fell at the same speed — roughly 1 meter per second.

What are the corresponding Reynolds numbers?

The small cone has a diameter of 0.75×7 centimeters (0.75 because one-quarter of the original circumference was removed), which is roughly 5.3 centimeters. The viscosity of air is roughly 1.5×10−5 square meters per second (an estimate that we will make in Section 7.3.2). The resulting Reynolds number is roughly 3500:

𝑣

𝐷

⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞

𝖱𝖾 = 1 m s−1 × 0.053 m ≈ 3500.

(5.50)

1.5×10−5 m2 s−1

⏟⏟⏟⏟⏟⏟⏟⏟⏟

𝜈

What is the Reynolds number for the large cone?

Never make a calculation from scratch when you can use proportional reasoning. Both cones experience the same viscosity and share the same fall speed. Therefore, we can consider 𝜈 and 𝑣 to be constants, leaving the Reynolds number 𝑣𝐷/𝜈 proportional just to the diameter 𝐷.

Because the large cone has twice the diameter of the small cone, it has twice the Reynolds number:

𝖱𝖾large = 2 × 𝖱𝖾small ≈ 7000.

(5.51)

At that Reynolds number, what is the cone's drag coefficient?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.3 More dimensionless groups 163

The drag coefficient is

𝐹

𝑐

drag

d ≡ 1

(5.52)

2 𝜌air𝑣2𝐴cs

The cone falls at its terminal speed, so the drag force is also its weight 𝑊: 𝐹drag = 𝑊 = 𝐴paper𝜎paper 𝑔,

(5.53)

where 𝜎paper is the areal density (mass per area) of paper and 𝐴paper is the area of the cone template. The drag coefficient is then 𝐹drag

𝐴

⏞⏞⏞⏞⏞⏞⏞

𝑐

paper𝜎paper 𝑔

d =

.

1

(5.54)

2 𝜌air𝐴cs𝑣2

As we showed in Section 3.5.2,

𝐴cs = 34𝐴paper.

(5.55)

This proportionality means that the areas cancel out of the drag coefficient: 𝜎

𝑐

paper𝑔

d =

.

1

(5.56)

2 𝜌air × 34 𝑣2

To compute 𝑐d, plug in the areal density 𝜎paper ≈ 80 grams per square meter and the measured speed 𝑣 ≈ 1 meter per second: 𝜎paper

𝑔

⏞⏞⏞⏞⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞

𝑐

8×10−2 kg m−2 × 10 m s−2

d ≈

≈ 1.8.

1

(5.57)

2 × 1.2 kg m−3

⏟⏟⏟⏟⏟ × 34 × 1 m2 s−2

⏟⏟⏟⏟⏟

𝜌air

𝑣2

Because no quantity in this calculation depends on the cone's size, both cones have the same drag coefficient. (Our estimated drag coefficient is significantly larger than the canonical drag coefficient for a solid cone, roughly 0.7, and is approximately the drag coefficient for a wedge.) Thus, the drag coefficient is independent of Reynolds number — at least, for Reynolds numbers between 3500 and 7000. The giant-cone experiment of Problem 4.16 shows that the independence holds even to 𝖱𝖾 ∼ 14 000.

Within this range, the dimensionless function 𝑓 in drag coefficient = 𝑓cone(Reynolds number)

(5.58)

is a constant. What a simple description of the complexity of fluid flow!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

164

5 Dimensions

This conclusion for 𝑓cone is valid for most shapes. The most extensive drag data is for a sphere — plotted below on log–log axes (data adapted from Fluid-Dynamic Drag: Practical Information on Aerodynamic Drag and Hydrodynamic Resistance [23]):

104

103

102

cd 101

100

10−1

10−2

10−2

10−1

100

101

102

103

104

105

106

107

Re

Like the drag coefficient for the cone, the drag coefficient for a sphere is almost constant as the Reynolds number varies from 3500 to 7000. The drag coefficient holds constant even throughout the wider range 2000…3 × 105.

Around 𝖱𝖾 ≈ 3 × 105, the drag coefficient falls by a factor of 5, from 0.5 to roughly 0.1. This drop is the reason that golf balls have dimples (you will explain the connection in Problem 7.24).

At low Reynolds numbers, the drag coefficient becomes large. This behavior, which represents a small object oozing through honey, will be explained in Section 8.3.1.2 using the tool of easy cases. The main point here is that, for most everyday flows, where the Reynolds number is in the「few thousand to few hundred thousand」range, the drag coefficient is a constant that depends only on the shape of the object.

Problem 5.23

Giant cone

How large, as measured by the diameter of its cross section, would a paper cone need to be in order for its fall to have a Reynolds number of roughly 3 × 105 (the Reynolds number at which the drag coefficient of a sphere drops significantly)?

Problem 5.24

Reynolds numbers

Estimate the Reynolds number for (a) a falling raindrop, (b) a flying mosquito, (c) a person walking, and (d) a jumbo jet flying at its cruising speed.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.4 Temperature and charge 165

Problem 5.25

Compound pendulum

Use dimensional analysis to deduce as much as you can about the period 𝑇 of a compound pendulum — that is, a pendulum where the l

bob is not a point mass but is an extended object of mass 𝑚. The light rod (no longer a string) of length 𝑙 is fixed to the center of mass of the object, which has a moment of inertia 𝐼CM about the point of m

attachment. (Assume that the oscillation amplitude is small and mass

therefore doesn't affect the period.)

Problem 5.26

Terminal velocity of a raindrop

In Problem 3.37, you estimated the terminal speed of a raindrop using 𝐹drag ∼ 𝜌air𝐴cs𝑣2.

(5.59)

Redo the calculation using the more precise information that 𝑐d ≈ 0.5 and retaining the factor of 4𝜋/3 in the volume of a spherical raindrop.

5.4 Temperature and charge

The preceding examples of dimensional analysis have been mechanical, using the dimensions of length, mass, and time. Temperature and charge are also essential to describing the world and are equally amenable to dimensional analysis. Let's start with temperature.

5.4.1 Temperature

To handle temperature, do we need to add another fundamental dimension?

Representing temperature as a new fundamental dimension is one method, and the dimension is symbolized by Θ. However, there's a simpler method.

It uses another fundamental constant of nature: Boltzmann's constant 𝑘B.

It has dimensions of energy per temperature; thus, it connects temperature to energy. In SI units, 𝑘B is roughly 1.6 × 10−23 joules per kelvin. When a temperature 𝑇 appears, convert it to the corresponding energy 𝑘B𝑇 (just as we convert 𝐺, in gravity problems, to 𝐺𝑚).

For our first temperature example, let's estimate the speed of air molecules.

We will then use that knowledge to estimate the speed of sound. Because the speed 𝑣 of air molecules is a result of thermal energy, it depends on 𝑘B𝑇. But 𝑣 and 𝑘B𝑇 — two quantities made from two independent dimensions — cannot make a dimensionless group. We need one more quantity: the mass 𝑚 of an air molecule.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

166

5 Dimensions

Although these three quantities contain three di- 𝑣

LT−1

thermal speed

mensions, only two of the dimensions are indepen- 𝑘B𝑇 ML2T−2 thermal energy dent — for example, M and LT−1. Therefore, the 𝑚

M

molecular mass

three quantities produce one independent dimensionless group. A reasonable choice for it is 𝑚𝑣2/𝑘B𝑇. Then 𝑣 ∼ 𝑘B𝑇

𝑚 .

(5.60)

This result is quite accurate. The missing dimensionless prefactor is 3 for the root-mean-square speed and 8/𝜋 for the mean speed.

The dimensional-analysis result helps predict the speed of sound. In a gas, sound travels because of pressure, which is a result of thermal motion.

Thus, it is plausible that the speed of sound 𝑐s should be comparable to the thermal speed. Then,

𝑐s ∼ 𝑘B𝑇

𝑚 .

(5.61)

To evaluate the speed numerically, multiply by a form of 1 based on Avogadro's number:

𝑐s ∼ 𝑘B𝑇

𝑚 × 𝑁A

𝑁 .

(5.62)

A

The numerator now contains 𝑘B𝑁A, which is the universal gas constant 𝑅: 𝑅 ≈ 8 J

mol K.

(5.63)

The denominator in the square root is 𝑚𝑁A: the mass of one molecule multiplied by Avogadro's number. It is therefore the mass of one mole of air molecules. Air is mostly N2, with an atomic mass of 28. Including the oxygen for us animals, the molar mass of air is roughly 30 grams per mole.

Plugging in 300 K for room temperature gives a thermal speed of roughly 300 meters per second:

𝑐s ∼ 8 J mol−1 K−1 × 300 K ≈ 300 m s−1.

(5.64)

3×10−2 kg mol−1

The actual sound speed is 340 meters per second, not far from our estimate based on dimensional analysis and a bit of physical reasoning. (The discrepancy remaining is due to the difference between isothermal and adiabatic compression and expansion. For a related effect, later try Problem 8.27.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.4 Temperature and charge 167

With this understanding of how to handle temperature, let's use dimensional analysis to estimate the height of the atmosphere. This height, called the scale height 𝐻, is the length over which the atmosphere's properties, such as pressure and density, change significantly. At the height 𝐻, the atmospheric density and pressure will be significantly lower than at sea level.

The first step in dimensional analysis is to list 𝐻 L

atmosphere height

the quantities that determine the height. That 𝑔

LT−2

gravity

list requires a physical model: The atmosphere 𝑘B𝑇 ML2T−2 thermal energy is a competition between gravity and thermal 𝑚

M

molecular mass

motion. Gravity drags molecules toward Earth; thermal motion spreads them all over the universe. Our list must include quantities representing both sides of that competition: 𝑚 and 𝑔 for gravity, and 𝑘B𝑇 for thermal energy.

Four quantities (including the goal 𝐻) built from three independent dimensions produce one independent dimensionless group. A reasonable choice for the group — reasonable because it is proportional to the goal 𝐻 — is the ratio 𝑚𝑔𝐻/𝑘B𝑇. Therefore, the atmosphere's scale height is given by 𝐻 ∼ 𝑘B𝑇

𝑚𝑔 .

(5.65)

To evaluate this height numerically, again convert Boltzmann's constant 𝑘B

to the universal gas constant 𝑅 by multiplying by 𝑁A/𝑁A: 𝑅

𝑅

⏞

⏞⏞⏞⏞⏞⏞⏞

𝐻 ∼ 𝑘B𝑁A 𝑇 ≈

8 J mol−1 K−1 × 300 K

≈ 8 km.

(5.66)

𝑚𝑁A

⏟ 𝑔

3×10−2 kg mol−1

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × 10 m s−2

𝑚molar

𝑚molar

Thus, by 8 kilometers above sea level, atmospheric pressure and density should be significantly lower than at sea level. This conclusion is reasonable: Mount Everest is 9 kilometers high, where the significantly thinner air requires climbers to carry oxygen tanks.

As a rule of thumb for a decaying function such as atmospheric pressure or density, a「significant change」can be estimated as a rise or, here, a fall by a factor of 𝑒. (For more on this rule of thumb, try Problem 6.36 after you have studied lumping; see also Section 3.2.1 of Street-Fighting Mathematics

[33].) Indeed, at 8 kilometers, the standardized atmospheric parameters relative to sea level are 𝜌/𝜌0 ≈ 0.43 and 𝑝/𝑝0 ≈ 0.35. For comparison, 1/𝑒 is approximately 0.37.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

168

5 Dimensions

5.4.2 Charge

Our second new dimension is charge, symbolized by Q. By introducing charge, we can apply dimensional analysis to electrical phenomena. Let's begin by finding the dimensions of electrical quantities.

What are the dimensions of current, voltage, and resistance?

Current is the flow of charge; it has dimensions of charge per time. Using 𝐼 to denote current and [𝐼] to denote its dimensions,

[𝐼] = QT−1.

(5.67)

The dimensions of voltage can be determined from the relation voltage × current = power.

(5.68)

The corresponding dimensional equation is

[voltage] = [power]

[current].

(5.69)

Because the dimensions of power (energy per time) are ML2T−3, and the dimensions of current are QT−1, the dimensions of voltage are ML2T−2Q−1:

[voltage] = ML2T−3 = ML2T−2Q−1.

(5.70)

QT−1

In this expression, the dimensional combination ML2T−2 is energy. Therefore, voltage is also energy per charge. As a result, an electron volt (1 electron charge times 1 volt) is an energy. A few electron volts is the energy in chemical bonds. Because chemical bonds reflect a change in one or two electrons, atomic and molecular voltages must be a few volts. (An everyday consequence is that typical batteries supply a few volts.) To find the dimensions of resistance, we'll write Ohm's law as a dimensional equation:

[resistance] = [voltage]

[current] = ML2T−2Q−1 = ML2T−1Q−2.

(5.71)

QT−1

To simplify these dimensions, use [𝑉] — the dimensions of voltage — as an abstraction for the dimensional mess ML2T−2Q−1. Then,

[resistance] = [𝑉] × TQ−1.

(5.72)

This alternative is useful when the input to and output of a circuit is voltage. Then treating the dimensions of voltage as a fundamental dimension 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.4 Temperature and charge 169

simplifies the task of finding dimensionless groups. (For practice in using the dimensions of voltage, try Problem 5.27.) Problem 5.27

Capacitance and inductance

Express the dimensions of capacitance and inductance using L, M, T, and Q. Then write them using [𝑉] (the dimensions of voltage) along with any fundamental dimensions that you need.

Problem 5.28

RC circuit

R

In this problem, you apply dimensional analysis Vin V

to the low-pass 𝑅𝐶 circuit that we introduced in Section 2.4.4. In particular, make the input volt-C

age 𝑉in zero for time 𝑡 < 0 and a fixed voltage 𝑉0

for 𝑡 ≥ 0. The goal is the most general dimension-ground

less statement about the output voltage 𝑉, which depends on 𝑉0, 𝑡, 𝑅, and 𝐶.

a. Using [𝑉] to represent the dimensions of voltage, fill in a dimensional-analysis table for the quantities 𝑉, 𝑉0, 𝑡, 𝑅, and 𝐶.

b. How many independent dimensions are contained in these five quantities?

c. Form independent dimensionless groups and write the most general statement in the form

group containing 𝑉 but not 𝑡 = 𝑓 (group containing 𝑡 but not 𝑉, …), (5.73) where the … stands for the third dimensionless group (if it exists). Compare your expression to the analysis of the 𝑅𝐶 circuit in Section 2.4.4.

Problem 5.29

Dimensional analysis of an LRC circuit In the 𝐿𝑅𝐶 circuit, the input voltage 𝑉in is the real L

C

part of a complex-exponential signal 𝑉

Vin

Vout

0𝑒𝑗𝜔𝑡, where

𝑉0 is the input amplitude and 𝜔 is the angular os-R

cillation frequency. The output voltage 𝑉out is then the real part of 𝑉1𝑒𝑗𝜔𝑡, where 𝑉1 is the (possibly ground

complex) output amplitude. What quantities determine the gain 𝐺, defined as the ratio 𝑉1/𝑉0? What is a good set of independent dimensionless groups built from 𝐺 and these quantities?

Along with the potential (or voltage) 𝑉, a leading actor in electromagnetics is the electric field. (Once you understand how to handle electric fields, you can practice by analyzing magnetic fields — try Problems 5.31, 5.32, and 5.33.) Electric fields not only transmit force; they also contain energy. This energy is important, not least because its transport is how the Sun warms the Earth. We will estimate the energy contained in electric fields by using 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

170

5 Dimensions

dimensional analysis. This analysis will give us the result that we used in Section 2.4.2 to estimate, by analogy, the energy in a gravitational field. Like the gravitational field, the electric field extends over space. Therefore, we usually want not the energy itself, but rather the energy per volume — the energy density.

What is the energy density in an electric field?

To answer this question with dimensional analysis, let's follow most of the steps that we used in estimating the bending of starlight (Section 5.3.1).

1. List the relevant quantities.

2. Form independent dimensionless groups.

3. Use the groups to make the most general statement about the energy density.

4. Narrow the possibilities by incorporating physical knowledge. For this problem, we will be able to skip this step.

Thus, the first step is to tabulate the quantities on which our goal, the energy density ℰ, depends. It definitely depends on the electric field 𝐸. It also probably depends on 𝜖0, the permittivity of free space appearing in Coulomb's law, because most results in electrostatics contain 𝜖0. But ℰ shouldn't depend on the speed of light: The speed of light suggests radiation, which requires a changing electric field; however, even a constant electric field contains energy. Thus, our list might be complete. Let's see, by trying to make a dimensionless group.

So we list the quantities with their dimensions, ℰ ML−1T−2

energy density

with the goal at the head of the table. Energy 𝐸 MLT−2Q−1

electric field

density is energy per volume, so its dimensions 𝜖0 M−1L−3T2Q2 SI constant are ML−1T−2. Electric field is force per charge (just as gravitational field is force per mass — analogy!), so its dimensions are MLT−2Q−1.

What are the dimensions of 𝜖0 ?

This quantity is the trickiest. It shows up in Coulomb's law: electrostatic force = 𝑞2 1

4𝜋𝜖0 𝑟2.

(5.74)

As a dimensional equation,

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.4 Temperature and charge 171

[𝜖0] = Q2

[𝐹] L2 ,

(5.75)

where [𝐹] = MLT−2 represents the dimensions of force. Therefore, 𝜖0 has dimensions of M−1L−3T2Q2.

The second step is to find independent dimensionless groups. Any search is aided by knowing how many items to find. This count is provided by the Buckingham Pi theorem. To apply the theorem, we first need to count the independent dimensions.

How many independent dimensions do the three quantities contain?

At first glance, the quantities contain four independent dimensions: M, L, T, and Q. However, the Buckingham Pi theorem would then predict −1

dimensionless groups, which is nonsense. Indeed, the number of independent dimensions cannot exceed the number of quantities (a restriction that you explained in Problem 5.7). Here, as you verify in Problem 5.30, there are only two independent dimensions — for example, MLT−2Q−1 (the dimensions of electric field) and L2Q−1.

Three quantities constructed from two independent dimensions produce one independent dimensionless group. A useful choice for this group, because it is proportional to the goal ℰ, is ℰ/𝜖0𝐸2.

The third step is to use the independent dimensionless group to make the most general statement about the energy density. With only one group, the most general statement is

ℰ ∼ 𝜖0𝐸2.

(5.76)

The fourth step is to narrow the possibilities by using physical knowledge.

With only one independent dimensionless group, the space of possibilities is already narrow. The only freedom is the dimensionless prefactor hidden in the single approximation sign ∼; it turns out to be 1/2. In Section 5.4.3, the scaling ℰ ∝ 𝐸2 will help us explain the surprising behavior of the electric field produced by an accelerating charge — and thereby explain why stars are visible and radios work.

Problem 5.30

Rewriting the dimensions

Express the dimensions of ℰ, 𝐸, and 𝜖0 in terms of [𝐸] (the dimensions of electric field) and L2Q−1. Thus, show that the three quantities contain only two independent dimensions.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

172

5 Dimensions

Problem 5.31

Dimensions of magnetic field

A magnetic field 𝐁 produces a force on a moving charge 𝑞 given by 𝐅 = 𝑞(𝐯 × 𝐁),

(5.77)

where 𝐯 is the charge's velocity. Use this relation to find the dimensions of magnetic field in terms of M, L, T, and Q. Therefore, give the definition of a tesla, the SI unit of magnetic field.

Problem 5.32

Magnetic energy density

Just as electric fields depend on 𝜖0, the permittivity of free space, magnetic fields depend on the constant 𝜇0 called the permeability of free space. It is defined as 𝜇0 ≡ 4𝜋 ×10−7 N A−2,

(5.78)

where N is a newton and A is an ampere (a coulomb per second). Express the dimensions of 𝜇0 in terms of M, L, T, and Q.

Then use the dimensions of magnetic field (Problem 5.31) to find the energy density in a magnetic field 𝐵. (As with the electric field, the dimensionless prefactor will be 1/2, but dimensional analysis does not give us that information.) What analogies can you make between electrostatics and magnetism?

Problem 5.33

Magnetic field due to a wire

Use the dimensions of 𝐵 (Problem 5.31) and of the permeability of free space 𝜇0

(Problem 5.32) to find the magnetic field 𝐵 at a distance 𝑟 from an infinitely long wire carrying a current 𝐼. The missing dimensionless prefactor, which dimensional analysis cannot tell us, turns out to be 1/2𝜋.

Magnetic-resonance imaging (MRI) machines for medical diagnosis use fields of the order of 1 tesla. If this field were produced by a current-carrying wire 0.5 meters away, what current would be required? Therefore, explain why these magnetic fields are produced by superconducting magnets.

Problem 5.34

Fields due to a uniform sheet of charge

Imagine an infinite, uniform sheet of charge containing a charge per area 𝜎. Use dimensional analysis to find the electric field 𝐸 at a distance 𝑧 from the sheet. (The missing dimensionless prefactor turns out to be 1!) Therefore, give the scaling exponent 𝑛 in 𝐸 ∝ 𝑧𝑛. (In Problem 6.21, you'll investigate a physical explanation for this surprising result.)

Use the analogy between electric and gravitational fields (Section 2.4.2) to find the gravitational field above a uniform sheet with mass per area 𝜎.

5.4.3 Power radiated by a moving charge

In our next example, we'll estimate the power radiated by a moving charge, which is how a radio broadcasting antenna works. This power, when combined with our long-standing understanding of flux (Section 3.4.2) and our 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.4 Temperature and charge 173

new understanding of the energy density in an electric field (Section 5.4.2), will predict a surprising scaling relation for the strength of the radiation field, one responsible for our ability to see the world. The example also illustrates a simple way to manage the dimensions of charge.

How does the power radiated by a moving charge depend on the acceleration of the charge?

For the moment, let's ignore the charge's velocity. Most likely, the dependence on acceleration is a scaling relation

power ∝ (acceleration)𝑛.

(5.79)

We will find the scaling exponent 𝑛 using dimensional analysis.

First, we list the quantities on which the goal, the radiated power 𝑃, depends. It certainly depends on the charge's motion, which is represented by its acceleration 𝑎. It also depends on the amount of charge 𝑞, because more charge probably means more radiation. The list should also include the speed of light 𝑐, because the radiation travels at the speed of light.

It probably also needs the permittivity of free space 𝜖0. However, rather than including 𝜖0 directly, let's reuse the shortcut for gravitation, where we combined Newton's constant 𝐺 with a mass (in Section 5.3.1). Similarly, 𝜖0

always appears as 𝑞2/4𝜋𝜖0, whether in electrostatic energy or force. Therefore, rather than including 𝑞 and 𝜖0 separately, we can include only 𝑞2/4𝜋𝜖0.

What happened to the charge's velocity?

If the radiated power depended on the velocity, then we could use the principle of relativity to make a perpetual-motion machine: We generate energy simply by using a different (inertial) reference frame, one in which the charge moves faster. Rather than believing in perpetual motion, we should conclude that the velocity does not affect the power. Equivalently, we can eliminate the velocity by switching to a reference frame where the charge has zero velocity.

Why doesn't the reference-frame argument allow us to eliminate the acceleration?

It depends on changing to another inertial reference frame — that is, a frame that moves at a constant velocity relative to the original frame. This relative motion does not affect the charge's acceleration, only its velocity.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

174

5 Dimensions

However, if we change to a noninertial — an accelerating — reference frame, we must modify the equations of motion, adding terms for the Coriolis, cen-trifugal, and Euler forces. (For more on reference frames, a wonderful expo-sition is John Taylor's Classical Mechanics [45].) If we switch to a noninertial frame, all bets are off about the radiated power. In summary, acceleration is different from velocity.

These four quantities, built from three inde-

𝑃

ML2T−3

radiated power

pendent dimensions, produce just one inde- 𝑞2/4𝜋𝜖0 ML3T−2 electrostatic mess pendent dimensionless group. Because mass

𝑐

LT−1

speed of light

appears in only 𝑃 and 𝑞2/4𝜋𝜖0 (as M1), the

𝑎

LT−2

acceleration

group must contain 𝑃/(𝑞2/4𝜋𝜖0). This quo-

tient has dimensions of L−1T−1. Multiplying it by 𝑐3/𝑎2, which has dimensions of LT, makes the result dimensionless. Therefore, the independent dimensionless group proportional to 𝑃 is

𝑃

𝑐3

𝑞2/4𝜋𝜖0 𝑎2.

(5.80)

As the only group, it must be a dimensionless constant, so 𝑃 ∼ 𝑞2 𝑎2

4𝜋𝜖0 𝑐3 .

(5.81)

The exact result is almost identical:

𝑃 = 𝑞2 𝑎2

6𝜋𝜖0 𝑐3 .

(5.82)

This result is even correct at relativistic speeds, as long as we use the relativistic acceleration (the four-acceleration) as the generalization of 𝑎.

As a scaling relation between 𝑃 and 𝑎, it is simple: 𝑃 ∝ 𝑎2. Doubling the acceleration quadruples the radiated power. The steep dependence on the acceleration is an important part of the reason that the sky is blue (we'll do the analysis in Section 9.4.1).

This power is carried by a changing electric field. By using the energy density in the electric field, we can estimate and explain the surprising strength of this field. We start by estimating the energy flux (the power per area) at a distance 𝑟, by spreading the radiated power over a sphere of radius 𝑟. The sphere's surface area is comparable to 𝑟2, so energy flux ∼ 𝑃

𝑎2 1

𝑟2 ∼ 𝑞2

4𝜋𝜖0 𝑐3 𝑟2.

(5.83)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 175

Energy flux, based on what we learned in Section 3.4.2, is connected to energy density by

energy flux = energy density × transport speed.

(5.84)

The transport speed is the speed of light 𝑐, so 𝑞2 𝑎2 1

4𝜋𝜖

∼

𝜖0𝐸2 × 𝑐.

(5.85)

0 𝑐3 𝑟2

⏟⏟⏟⏟⏟⏟⏟

⏟

⏟

energy flux

energy density

speed

Now we can solve for the electric field:

𝐸 ∼ 𝑞𝑎 1

𝜖0𝑐2 𝑟 .

(5.86)

As a scaling relation, 𝐸 ∝ 𝑟−1. Compare it to the −2 scaling exponent for an electrostatic field, where 𝐸 ∝ 𝑟−2 (Coulomb's law). The radiation field therefore falls off more slowly with distance than the electrostatic field. This important difference explains why we can receive radio signals and see stars. If radiation fields were proportional to 1/𝑟2, stars, and most of the world, would be invisible. What difference a scaling exponent can make!

5.5 Atoms, molecules, and materials

With our growing repertoire of dimensional analyses, we can explore ever more of the world. Perhaps the most fundamental property of the world is that it is composed of atoms. Feynman argued for the importance of the atomic theory in his famous lectures on physics [14, Vol. 1, p. 1-2]: If, in some cataclysm, all of scientific knowledge were to be destroyed, and only one sentence passed on to the next generation of creatures, what statement would contain the most information in the fewest words? I believe it is the atomic hypothesis (or the atomic fact, or whatever you wish to call it) that all things are made of atoms — little particles that move around in perpetual motion, attracting each other when they are a little distance apart, but repelling upon being squeezed into one another. In that one sentence, you will see, there is an enormous amount of information about the world…. [emphasis in original]

The atomic theory was first stated over 2000 years ago by the ancient Greek philosopher Democritus. Using quantum mechanics, we can predict the properties of atoms in great detail — but the analysis involves complicated mathematics that buries the core ideas. By using dimensional analysis, we can keep the core ideas in sight.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

176

5 Dimensions

5.5.1 Dimensional analysis of hydrogen

We'll study the simplest atom: hydrogen. Dimensional analysis will explain its size, and its size will in turn explain the size of more complex atoms and molecules. Dimensional analysis will also help us estimate the energy needed to disassemble a hydrogen atom. This energy will in turn explain the bond energies in molecules. These energies will explain the stiffness of materials, the speed of sound, and the energy content of fat and sugar — all starting from hydrogen!

In the dimensional analysis of the size of hydrogen, the zeroth step is to give the size a name. The usual name and symbol for the radius of hydrogen is the Bohr radius 𝑎0.

electron

The first step is to find the quantities that determine the size. That determination requires a physical model of hydrogen. A simple model is an electron orbiting a proton at a distance 𝑎

a0

0. Their electrostatic attraction

provides the force 𝐹 holding the electron in orbit:

+ proton

𝐹 = 𝑒2 1

4𝜋𝜖

,

(5.87)

0 𝑎20

where 𝑒 is the electron charge. Our list of quantities should include the quantities in this equation; in that way, we teach dimensional analysis about what kind of force holds the atom together. Thus, we should somehow include 𝑒 and 𝜖0. As when we estimated the power radiated by an accelerating charge (Section 5.4.3), we'll include 𝑒 and 𝜖0 as one quantity, 𝑒2/4𝜋𝜖0.

The force on the electron does not by itself deter-

𝑎0

L

size

mine the electron's motion. Rather, the motion is 𝑒2/4𝜋𝜖0 ML3T−2 electrostatics determined by its acceleration. Computing the 𝑚e

M

electron mass

acceleration from the force requires the electron mass 𝑚e, so our list should include 𝑚e.

These three quantities made from three independent dimensions produce zero dimensionless groups (another application of the Buckingham Pi theorem introduced in Section 5.1.2). Without any dimensionless groups, we cannot say anything about the size of hydrogen. The lack of a dimensionless group tells us that our simple model of hydrogen is too simple.

There are two possible resolutions, each involving new physics that adds one new quantity to the list. The first possibility is to add special relativity by adding the speed of light 𝑐. That choice produces a dimensionless 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 177

group and therefore a size. However, this size has nothing to do with hydrogen. Rather, it is the size of an electron, considering it as a cloud of charge (Problem 5.37).

The other problem with this approach is that electromagnetic radiation travels at the speed of light, so once the list includes the speed of light, the electron might radiate. As we found in Section 5.4.3, the power radiated by an accelerating charge is

𝑃 ∼ 𝑞2 𝑎2

4𝜋𝜖0 𝑐3 .

(5.88)

An orbiting electron is an accelerating electron (accelerating inward with the circular acceleration 𝑎 = 𝑣2/𝑎0), so the electron would radiate. Radiation would carry away energy from the electron, the electron would spiral into the proton, and hydrogen would not exist — nor would any other atom.

So adding the speed of light only compounds our problem.

The second resolution is instead to add quantum mechanics. Its fundamental equation is the Schrödinger equation:

(− ℏ2

2𝑚∇2 + 𝑉) 𝜓 = 𝐸𝜓.

(5.89)

Most of the symbols in this partial-differential equation are not important for dimensional analysis — this disregard is how dimensional analysis simplifies problems. For dimensional analysis, the crucial point is that Schrö-

dinger's equation contains a new constant of nature: ℏ, which is Planck's constant ℎ divided by 2𝜋. We can include quantum mechanics in our model of hydrogen simply by including ℏ on our list of relevant quantities. In that way, we teach dimensional analysis about quantum mechanics.

The new quantity ℏ is an angular momentum, which is a length (the lever arm) times linear momentum (𝑚𝑣). Therefore, its dimensions are L

⏟ × M

⏟ × LT−1

⏟ = ML2T−1.

(5.90)

[𝑟]

[𝑚]

[𝑣]

The ℏ might save hydrogen. It contributes a

𝑎0

L

size

fourth quantity without a fourth independent 𝑒2/4𝜋𝜖0 ML3T−2 electrostatic mess dimension. Therefore, it creates an indepen-

𝑚e

M

electron mass

dent dimensionless group.

ℏ

ML2T−1

quantum

To find it, look for a dimension appearing in only two quantities. Time appears in 𝑒2/4𝜋𝜖0 as 𝑇−2 and in ℏ as 𝑇−1. Therefore, the group contains the quotient ℏ2/(𝑒2/4𝜋𝜖0). Its dimensions are ML, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

178

5 Dimensions

which can be canceled by dividing by 𝑚e𝑎0. The resulting dimensionless group is

ℏ2

.

(5.91)

𝑚e𝑎0(𝑒2/4𝜋𝜖0)

As the only independent dimensionless group, it must be a dimensionless constant. Therefore, the size (as the radius) of hydrogen is given by 𝑎0 ∼

ℏ2

.

(5.92)

𝑚e(𝑒2/4𝜋𝜖0)

Now let's plug in the constants. We could just look up each constant, but that approach gives exponent whiplash; the powers of ten swing up and down and end on a seemingly random value. To gain insight, we'll instead use the numbers for the backs of envelopes (p. xvii). That table deliberately has no entry for ℏ by itself, nor for the electron mass 𝑚e. Both omissions can be resolved with a symmetry operation (Problem 5.35).

Problem 5.35

Shortcuts for atomic calculations

Many atomic problems, such as the size or binding energy of hydrogen, end up in expressions with ℏ, the electron mass 𝑚e, and 𝑒2/4𝜋𝜖0. You can avoid remembering those constants by instead remembering the following values: ℏ𝑐 ≈ 200 eV nm = 2000 eV Å

𝑚e𝑐2 ∼ 0.5×106 eV (the electron rest energy) (5.93)

𝑒2/4𝜋𝜖0

ℏ𝑐

≡ 𝛼 ≈ 1/137 (the fine-structure constant).

Use these values and dimensional analysis to find the energy of a photon of green light (which has a wavelength of approximately 0.5 micrometers), expressing your answer in electron volts.

In our expression for the Bohr radius, ℏ2/𝑚e(𝑒2/4𝜋𝜖0), we can replace ℏ

with ℏ𝑐 and 𝑚e with 𝑚e𝑐2 simultaneously: Multiply by 1 in the form 𝑐2/𝑐2; it is a convenient symmetry operation.

𝑎0 ∼

ℏ2

× 𝑐2

.

(5.94)

𝑚e(𝑒2/4𝜋𝜖0) 𝑐2 =

(ℏ𝑐)2

𝑚e𝑐2(𝑒2/4𝜋𝜖0)

Now the table provides the needed values: for ℏ𝑐, 𝑚e𝑐2, and 𝑒2/4𝜋𝜖0. However, we can make one more simplification because the electrostatic mess 𝑒2/4𝜋𝜖0 is related to a dimensionless constant. To see the relation, multiply and divide by ℏ𝑐:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 179

𝑒2

𝑒2/4𝜋𝜖0⎞

4𝜋𝜖 = ⎛⎜

⎟ ℏ𝑐.

(5.95)

0

⎝ ℏ𝑐

⏟⏟⏟⏟⏟ ⎠

⏟⏟

𝛼

The factor in parentheses is known as the fine-structure constant 𝛼; it is a dimensionless measure of the strength of electrostatics, and its numerical value is close to 1/137 or roughly 0.7 ×10−2. Then 𝑒2

4𝜋𝜖 = 𝛼ℏ𝑐.

(5.96)

0

This substitution further simplifies the size of hydrogen: 𝑎0 ∼

(ℏ𝑐)2

=

(ℏ𝑐)2

=

ℏ𝑐

𝑚

𝛼 × 𝑚

e𝑐2 × 𝑒2/4𝜋𝜖0

𝑚e𝑐2 × 𝛼ℏ𝑐

e𝑐2 .

(5.97)

Only now, having simplified the calculation down to abstractions worth remembering (𝛼, 𝑚e𝑐2, and ℏ𝑐), do we plug in the entries from the table.

ℏ𝑐

⏞⏞⏞⏞⏞

𝑎

200 eV nm

0 ∼

.

(5.98)

0.7 ×10−2

⏟⏟⏟⏟⏟ × 5

⏟×

⏟105

⏟eV

⏟⏟

𝛼

𝑚e𝑐2

This calculation we can do mentally. The units of electron volts cancel, leaving only nanometers (nm). The two powers of ten upstairs (in the numerator) and the three powers of ten downstairs (in the denominator) result in 10−1 nanometers or 1 ångström (10−10 meters). The remaining factors result in a factor of 1/2: 2/(0.7 × 5) ≈ 1/2.

Therefore, the size of hydrogen — the Bohr radius — is about 0.5 ångströms: 𝑎0 ∼ 0.5×10−10 m = 0.5 Å.

(5.99)

Amazingly, the missing dimensionless prefactor is 1. Thus, atoms are ångström-sized. Indeed, hydrogen is 1 ångström in diameter. All other atoms, which have more electrons and therefore more electron shells, are larger. A useful rule of thumb is that a typical atomic diameter is 3 ångströms.

What binding energy does this size produce?

The binding energy is the energy required to disassemble the atom by removing the electron and dragging it to infinity. This energy, denoted 𝐸0, should be roughly the electrostatic energy of a proton and electron separated by the Bohr radius 𝑎0:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

180

5 Dimensions

𝐸

1

0 ∼ 𝑒2

4𝜋𝜖

.

(5.100)

0 𝑎0

With our result for 𝑎0, the binding energy becomes 2

𝐸

1

0 ∼ 𝑚e ( 𝑒2

4𝜋𝜖 )

0

ℏ2 .

(5.101)

The missing dimensionless prefactor is just 1/2: 2

𝐸

1

0 = 12𝑚e ( 𝑒2

4𝜋𝜖 )

0

ℏ2 .

(5.102)

Problem 5.36

Shortcut to calculate the binding energy of hydrogen Use the shortcuts in Problem 5.35 to show that the binding energy of hydrogen is roughly 14 electron volts. From your symbolic expression for the energy, which is also the kinetic energy of the electron, estimate its speed as a fraction of 𝑐.

In Problem 5.36, you showed, using the values of ℏ𝑐, 𝑚e𝑐2, and 𝛼, that this energy is roughly 14 electron volts. For the sake of a round number, let's call the binding energy roughly 10 electron volts.

This energy sets the scale for chemical bonds. In Section 3.2.1, we calculated, by unit conversion, that 1 electron volt per molecule corresponded to roughly 100 kilojoules per mole. Therefore, breaking a chemical bond requires roughly 1 megajoule per mole (of bonds). As a rough estimate, it is not far off. For example, if the molecule consists of a few life-related atoms (carbon, oxygen, and hydrogen), then the molar mass is roughly 50 grams — a small jelly donut. Therefore, burning a jelly donut, as our body does slowly when we eat the donut, should produce roughly 1 megajoule — a useful rule of thumb and way of imagining a megajoule.

Problem 5.37

Adding the speed of light

If we assume that 𝑎0 depends on 𝑒2/4𝜋𝜖0, 𝑚e, and 𝑐, what size would dimensional analysis predict for hydrogen? This size is called the classical electron radius and denoted 𝑟0. How does it compare to the actual Bohr radius?

Problem 5.38

Thermal expansion

Estimate a typical thermal-expansion coefficient, also denoted 𝛼. It is defined as fractional change in a substance's length

𝛼 ≡

change in temperature

.

(5.103)

The thermal-expansion coefficient depends on the binding energy 𝐸0. Assuming 𝐸0 ∼ 10 eV, compare your estimate for 𝛼 with its value for everyday substances.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 181

Problem 5.39

Diffraction in the eye

Light passing through an opening, such as a telescope θ

aperture or the pupil in the eye, diffracts (spreads out).

By estimating the diffraction angle

D

𝜃, we will be able

to understand aspects of the design of the eye.

a. What are the valid dimensionless relations connecting the diffraction angle 𝜃, the light wavelength 𝜆, and the pupil diameter 𝐷?

b. Diffraction is the result of the photons in the beam acquiring a vertical momentum Δ𝑝𝑦. What is the scaling exponent 𝛽 in 𝜃 ∝ (Δ𝑝𝑦)𝛽?

c. The Heisenberg uncertainty principle from quantum mechanics says that the uncertainty in the photon's vertical momentum Δ𝑝𝑦 is inversely proportional to the pupil diameter 𝐷. What is therefore the scaling exponent 𝛾 in 𝜃 ∝ 𝐷𝛾?

d. Therefore find 𝜃 as a function of 𝜆 and 𝐷.

e. Estimate a pupil diameter and the resulting diffraction angle. The light-sensitive cells in the retina that we use in bright light are the cones. They are most dense in the fovea — the central region of the retina that we use for reading and any other task requiring sharp vision. At that location, their density is roughly 0.5×107 per square centimeter. Is that what you would predict?

Problem 5.40

Kepler's third law for non-inverse-square force laws With an inverse-square force, Kepler's third law — the relation between orbit radius and period — is 𝑇 ∝ 𝑟3/2 (Section 4.2.2). Now generalize the law to forces of the form 𝐹 ∝ 𝑟𝑛, using dimensional analysis to find the scaling exponent 𝛽 in the orbital period 𝑇 ∝ 𝑟𝛽 as a function of the scaling exponent 𝑛 in the force law.

Problem 5.41

Ground state energy for general potentials Just as we can apply dimensional analysis to classical orbits (Problem 5.40), we can apply it to quantum orbits. When the force law is 𝐹 ∝ 𝑟−2 (electrostatics), or the potential is 𝑉 ∝ 𝑟−1, we have hydrogen, for which we estimated the binding or ground-state energy. Now generalize to potentials where 𝑉 = 𝐶𝑟𝛽.

The relevant quantities are the ground-state energy 𝐸0, the proportionality constant 𝐶 in the potential, the quantum constant ℏ, and the particle's mass 𝑚. These four quantities, built from three dimensions, form one independent dimensionless group. But it is not easy to find. Therefore, use linear algebra to find the exponents 𝛾, 𝛿, and 𝜖 that make 𝐸0𝐶𝛾ℏ𝛿𝑚𝜖 dimensionless. In the case 𝛽 = −1 (electrostatics), check that your result matches our result for hydrogen.

5.5.2 Blackbody radiation

With quantum mechanics and its new constant ℏ, we can explain the surface temperatures of planets or even stars. The basis is blackbody radiation: A 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

182

5 Dimensions

hot object — a so-called blackbody — radiates energy. (Here,「hot」means warmer than absolute zero, so every object is hot.) Hotter objects radiate more, so the radiated energy flux 𝐹 depends on the object's temperature 𝑇.

How are the energy flux 𝐹 and the surface temperature 𝑇 connected?

I stated the connection in Section 4.2, but now we know enough dimensional analysis to derive almost the entire result without a detailed study of the quantum theory of radiation. Thus, let's follow the steps of dimensional analysis to find 𝐹, and start by listing the relevant quantities.

The list begins with the goal, the energy flux 𝐹. Blackbody radiation can be understood properly through the quantum theory of radiation, which is the marriage of quantum mechanics to classical electrodynamics. (A diagram of the connection, which requires the subsequent tool of easy cases, is in Section 8.4.2.) For the purposes of dimensional analysis, this theory supplies two constants of nature: ℏ from quantum mechanics and the speed of light 𝑐 from classical electrodynamics. The list also includes the object's temperature 𝑇, so that dimensional analysis knows how hot the object is; but we'll include it as the thermal energy 𝑘B𝑇.

The four quantities built from three independent 𝐹

MT−3

energy flux

dimensions produce one independent dimension- 𝑘B𝑇 ML2T−2 thermal energy less group. Our usual route to finding this group, ℏ

ML2T−1

quantum

by looking for dimensions that appear in only one 𝑐

LT−1

speed of light

or two variables, fails because mass, like length, appears in three quantities, and time appears in all four. An alternative is to apply linear algebra, as you practiced in Problem 5.41. But it is messy.

A less brute-force and more physically meaningful alternative is to choose a system of units where 𝑐 ≡ 1 and ℏ ≡ 1. Each of these two choices has a physical meaning. Before using the choices, it is worth understanding these meanings. Otherwise we are back to pushing symbols around.

The first choice, 𝑐 ≡ 1, expresses the unity of space and time embedded and embodied in Einstein's theory of special relativity. With 𝑐 ≡ 1, length and time have the same dimensions and are measured in the same units. We can then say that the Sun is 8.3 minutes away from the Earth. That time is equivalent to the distance of 8.3 light minutes (the distance that light travels in 8.3 minutes).

The choice 𝑐 ≡ 1 also expresses the equivalence between mass and energy.

We use this choice implicitly when we say that the mass of an electron is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 183

5 × 105 electron volts — which is an energy. The complete statement is that, in the usual units, the electron's rest energy 𝑚e𝑐2 is 5 × 105 electron volts.

But when we choose 𝑐 ≡ 1, then 5×105 electron volts is also the mass 𝑚e.

The second choice, ℏ ≡ 1, expresses the fundamental insight of quantum mechanics, that energy is (angular) frequency. The complete connection between energy and frequency is

𝐸 = ℏ𝜔.

(5.104)

When ℏ ≡ 1, then 𝐸 is 𝜔.

These two unit choices implicitly incorporate their physical meanings into our analysis. Furthermore, the choices so simplify our table of dimensions that we can find the proportionality between flux and temperature without any linear algebra.

First, choosing 𝑐 ≡ 1 makes the dimensions of length and time equivalent: 𝑐 ≡ 1 implies L ≡ T.

(5.105)

Thus, in the table we can replace T with L.

Then adding the choice ℏ ≡ 1 contributes the dimensional equation ML2T−2

⏟⏟⏟⏟⏟ ≡ T−1

⏟

(5.106)

[𝐸]

[𝜔]

It looks like a useless mess; however, replacing T with L (from 𝑐 ≡ 1) simplifies it:

M ≡ L−1.

(5.107)

In summary, setting 𝑐 ≡ 1 and ℏ ≡ 1 makes length and time equivalent dimensions and makes mass and inverse length equivalent dimensions.

With these equivalences, let's rewrite the table of dimensions, one quantity at a time.

1. Flux 𝐹 . Its dimensions, in the usual system, were MT−3. In the new system, T−3 is equivalent to M3, so the dimensions of flux become M4.

2. Thermal energy 𝑘 B𝑇 . Its dimensions were ML2T−2. In the new system, T−2 is equivalent to L−2, so the dimensions of thermal energy become M. And they should: Choosing 𝑐 ≡ 1 makes energy equivalent to mass.

3. Quantum constant ℏ . By fiat (when we chose ℏ ≡ 1), it is now dimensionless and just 1, so we do not list it.

4. Speed of light 𝑐 . Also by fiat, 𝑐 is just 1, so we do not list it either.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

184

5 Dimensions

Our list has become shorter and the dimensions in it 𝐹

M4

energy flux

simpler. In the usual system, the list had four quan- 𝑘B𝑇 M thermal energy tities (𝐹, 𝑘B𝑇, ℏ, and 𝑐) and three independent dimensions (M, L, and T). Now the list has only two quantities (𝐹 and 𝑘B𝑇) and only one independent dimension (M). In both systems, there is only one dimensionless group.

In the usual system, the Buckingham Pi calculation is as follows: 4 quantities

− 3 independent dimensions

(5.108)

1 independent dimensionless group

In the new system, the calculation is

2 quantities

− 1 independent dimension

(5.109)

1 independent dimensionless group

(If the number of independent dimensionless groups had not been the same, we would know that we had made a mistake in converting to the new system.) In the simpler system, the independent dimensionless group proportional to 𝐹 is now almost obvious. Because 𝐹 contains M4 and 𝑘B𝑇 contains M1, the group is just 𝐹/(𝑘B𝑇)4.

Alas, no lunch is free and no good deed goes unpunished. Now we pay the price for the simplicity: We have to restore 𝑐 and ℏ in order to find the equivalent group in the usual system of units. Fortunately, the restoration doesn't require any linear algebra.

The first step is to compute the usual dimensions of 𝐹/(𝑘B𝑇)4:

[ 𝐹 ] =

MT−3

= M−3L−8T5.

(5.110)

(𝑘B𝑇)4

(ML2T−2)4

The rest of the analysis for making this quotient dimensionless just rolls downhill without our needing to make any choices. The only way to get rid of M−3 is to multiply by ℏ3: Only ℏ contains a dimension of mass.

The result has dimensions L−2T2:

[ 𝐹 ℏ3] = M−3

⏟⏟ L−8

⏟ T5 × (ML2

⏟⏟ T−1)3 = L−2T2.

(5.111)

(𝑘

⏟⏟

⏟⏟⏟

B𝑇)4

[𝐹/(𝑘B𝑇)4]

[ℏ]

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 185

To clear these dimensions, multiply by 𝑐2. The independent dimensionless group proportional to 𝐹 is therefore

𝐹ℏ3𝑐2 .

(5.112)

(𝑘B𝑇)4

As the only independent dimensionless group, it is a constant, so 𝐹 ∼ (𝑘B𝑇)4

ℏ3𝑐2 .

(5.113)

Including the dimensionless prefactor hidden in the twiddle (∼), 𝑘4

𝐹 = 𝜋2

B

60

𝑇4.

(5.114)

ℏ3𝑐2

⏟⏟⏟⏟⏟

𝜎

This result is the Stefan–Boltzmann law, and all the constants are lumped into 𝜎, the Stefan–Boltzmann constant:

𝑘4

𝜎 ≡ 𝜋2 B

60 ℏ3𝑐2 .

(5.115)

In Section 4.2.1, we used the scaling exponent in the Stefan–Boltzmann law to estimate the surface temperature of Pluto: We started from the surface temperature of the Earth and used proportional reasoning. Now that we know the full Stefan–Boltzmann law, we can directly calculate a surface temperature. In Problem 5.43, you will estimate the surface temperature of the Earth (and you then try to explain the life-saving discrepancy between prediction and reality). Here, we'll estimate the surface temperature of the Sun using the Stefan–Boltzmann law, the solar flux at the top of the Earth's atmosphere, and proportional reasoning.

Let's work backward from our goal toward what we know. We would like to find the Sun's surface temperature 𝑇Sun. If we knew the energy flux 𝐹Sun at the Sun's surface, then the Stefan–Boltzmann law would give us the temperature:

1/4

𝑇Sun = (𝐹Sun

𝜎 ) .

(5.116)

We can find 𝐹Sun from the solar flux 𝐹 at the Earth's orbit by using proportional reasoning. Flux, as we argued in Section 4.2.1, is inversely proportional to distance squared, because the same energy flow (a power) gets smeared over a surface area proportional to the square of the distance from the source. Therefore,

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

186

5 Dimensions

𝐹

2

Sun's surface

𝐹

= (𝑟Earth's orbit

𝑅

) ,

(5.117)

Sun

where 𝑅Sun is the radius of the Sun.

A related distance ratio is.

𝐷Sun

𝑟

= 2𝑅Sun ,

(5.118)

Earth's orbit

𝑟Earth's orbit

where 𝐷Sun is the diameter of the Sun. This ratio is the angular diameter of the Sun, denoted 𝜃Sun. Therefore,

𝑟Earth's orbit

𝑅

= 2 .

(5.119)

Sun

𝜃Sun

From a home experiment measuring the angular diameter of the Moon, which has the same angular diameter as the Sun, or from the table of constants, the angular diameter 𝜃Sun is approximately 10−2. Therefore, the distance ratio is approximately 200, and the flux ratio is approximately 2002 or 4×104.

Continuing to unwind the reasoning chain, we get the flux at the Sun's surface:

𝐹Sun's surface ≈ 4×104 × 1300 W m−2

⏟⏟⏟⏟⏟⏟⏟ ≈ 5×107 W m−2.

(5.120)

𝐹

This flux, from the Stefan–Boltzmann law, corresponds to a surface temperature of roughly 5400 K:

1/4

𝑇Sun ≈ ( 5×107 W m−2 ) ≈ 5400 K.

(5.121)

6×10−8 W m−2 K−4

This prediction is quite close to the measured temperature of 5800 K.

Problem 5.42

Redo the blackbody-radiation analysis using linear algebra Use linear algebra to find the exponents 𝑦, 𝑧, and 𝑤 that make the combination 𝐹 × (𝑘B𝑇)𝑦ℏ𝑧𝑐𝑤 dimensionless.

Problem 5.43

Blackbody temperature of the Earth

Use the Stefan–Boltzmann law 𝐹 = 𝜎𝑇4 to predict the surface temperature of the Earth. Your prediction should be somewhat colder than reality. How do you explain the (life-saving) difference between prediction and reality?

Problem 5.44

Lengths related by the fine-structure constant Arrange these important atomic-physics lengths in order of increasing size: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 187

a. the classical electron radius (Problem 5.37) 𝑟0 ≡ (𝑒2/4𝜋𝜖0)/𝑚e𝑐2 (roughly the radius of an electron if its rest energy were entirely electrostatic energy).

b. the Bohr radius 𝑎0 from Section 5.5.1.

c. the reduced wavelength 𝜆 of a photon with energy 2𝐸0, where 𝜆 ≡ 𝜆/2𝜋 (analogously to how ℏ ≡ ℎ/2𝜋 or 𝑓 = 𝜔/2𝜋) and 𝐸0 is the binding energy of hydrogen.

(The energy 2𝐸0, also the absolute value of the potential energy in hydrogen, is called the Rydberg).

d. the reduced Compton wavelength of the electron, defined as ℏ/𝑚e𝑐.

Place the lengths on a logarithmic scale, and label the gaps (the ratios of successive lengths) in terms of the fine-structure constant 𝛼.

5.5.3 Molecular binding energies

We studied hydrogen, which as an element scarcely exists on Earth, mainly to understand chemical bonds. Chemical bonds are formed by attractions between electrons and protons, so the hydrogen atom is the simplest chemical bond. The main defect of this model is that the electron–proton bond in a hydrogen atom is much shorter than in most bonds. A typical chemical bond is roughly 1.5 ångströms, three times larger than the Bohr radius. Because electrostatic energy scales as 𝐸 ∝ 1/𝑟, a typical bond energy should be smaller than hydrogen's binding energy by a factor of 3. Hydrogen's binding energy is roughly 14 electron volts, so 𝐸bond is roughly 4 electron volts — in agreement with the bond-energy values tabulated in Section 2.1.

Another important bond is the hydrogen bond. These intermolecular bonds, which hold water molecules together, are weaker than the intra molecular hydrogen–oxygen bonds within a water molecule. But hydrogen bonds determine important properties of the most important liquid on our planet.

For example, the hydrogen-bond energy determines water's heat of vaporization — which determines much of our weather, including the average rainfall on the Earth (as we found in Section 3.4.3).

O−

To estimate the strength of hydrogen bonds, use the proportionality

H+

H+

hydrogen

𝐸electrostatic ∝ 𝑞1𝑞2

bond

𝑟 .

(5.122)

O−

A hydrogen bond is slightly longer than a typical bond. Instead H+

H+

of the typical 1.5 ångströms, it is roughly 2 ångströms. The bond length is in the denominator, so the greater length reduces the bond energy by a factor of 4/3.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

188

5 Dimensions

Furthermore, the charges involved, 𝑞1 and 𝑞2, are smaller than the charges in a regular, intramolecular bond. A regular bond is between a full proton and a full electron of charge. A hydrogen bond, however, is between the excess charge on oxygen and the corresponding charge deficit on hydrogen. The excess and deficit are significantly smaller than a full charge. On oxygen the excess may be 0.5𝑒 (where 𝑒 is the electron charge). On each hydrogen, because of conservation, it would then be 0.25𝑒. These reductions in charge contribute factors of 1/2 and 1/4 to the hydrogen-bond energy.

The resulting energy is roughly 0.4 electron volts: 4 eV × 34 × 12 × 14 ≈ 0.4eV.

(5.123)

This estimate is not bad considering the rough numbers that it used. Empirically, a typical hydrogen bond is 23 kilojoules per mole or about 0.25 electron volts. Each water molecule forms close to four hydrogen bonds (two from the oxygen to foreign hydrogens, and one from each hydrogen to a foreign oxygen). Thus, each molecule gets credit for almost two hydrogen bonds — one-half of the per-molecule total in order to avoid counting each bond twice. Per water molecule, the result is 0.4 electron volts Because vaporizing water breaks the hydrogen bonds, but not the intramolecular bonds, the heat of vaporization of water should be approximately 0.4 electron volts per molecule. In macroscopic units, it would be roughly 40 kilojoules per mole — using the conversion factor from Section 3.2.1, that 1 electron volt per molecule is roughly 100 kilojoules per mole.

Because the molar mass of water is 1.8 × 10−2 kilograms, the heat of vaporization is also 2.2 megajoules per kilogram: 40 kJ

mol ×

1 mol

≈ 2.2×106 J

1.8×10−2 kg

kg

.

(5.124)

And it is (p. xvii). We used this value in Section 3.4.3 to estimate the average worldwide rainfall. The amount of rain, and so the rate at which many plants grow, is determined by the strength of hydrogen bonds.

Problem 5.45

Rotational energies

The quantum constant ℏ is also the smallest possible angular momentum of a rotating system. Use that information to estimate the rotational energy of a small molecule such as water (in electron volts). To what electromagnetic wavelength does this energy correspond, and where in the electromagnetic spectrum does it lie (for example, radio waves, ultraviolet, gamma rays)?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 189

5.5.4 Stiffness and sound speeds

An important macroscopic consequence of the per-atom and per-molecule energies is the existence of solid matter: substances that resist bending, twisting, squeezing, and stretching. These resistance properties are analogous to spring constants.

However, a spring constant is not the quantity to estimate first, because it is not invariant under simple changes. For example, a thick bar resists stretching more than a thin bar does. Similarly, a shorter bar resists stretching more than a longer bar does. The property independent of the shape or amount of substance — invariant to these changes — is the stiffness or elastic modulus. There are several elastic moduli, of which the Young's modulus is the most broadly useful. It is defined by stress

𝑌 =

𝜎 applied to the substance

fractional change in its length [(Δ𝑙)/𝑙].

(5.125)

The ratio in the denominator occurs so often that it has its own name and symbol: the strain 𝜖.

l

∆l

Stress, like the closely related quantity pressure, F

F

is force per area: It is the applied force 𝐹 divided by the cross-sectional area. The denominator, the fractional change in length, is the dimensionless ratio (Δ𝑙)/𝑙. Thus, the dimensions of stiffness are the dimensions of pressure — which are also the dimensions of energy density. To see the connection between pressure and energy density, multiply the definition of pressure (force per area) by length over length:

length

energy

pressure = force

area × length = volume.

(5.126)

As energy per volume, we can estimate a typical elastic modulus 𝑌. For the numerator, a suitable energy is the typical binding energy per atom — the energy 𝐸binding required to remove the atom from the substance by breaking its bonds to surrounding atoms. For the denominator, a suitable volume is a typical atomic volume 𝑎3, where 𝑎 is a typical interatomic spacing (3

ångströms). The result is

𝐸

𝑌 ∼ binding

𝑎3 .

(5.127)

This derivation is slightly incomplete: In multiplying the definition of pressure by length over length, we knew only that the two lengths have the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

190

5 Dimensions

same dimensions, but not whether they have comparable values. If they do not, then the estimate for 𝑌 needs a dimensionless prefactor, which might be far from 1. Therefore, before we estimate 𝑌, let's confirm the estimate by using a second method, an analogy — a form of abstraction that we learned in Section 2.4.

The analogy, with which we also began this discussion of stiffness, is between a spring constant (𝑘) and a Young's modulus (𝑌). There are three physical quantities in the analogy.

1. Stiffness. For a single spring, we measure stiffness using 𝑘. For a material, we use the Young's modulus 𝑌. Therefore, 𝑘 and 𝑌 are analogous.

2. Extension. For a single spring, we measure extension using the absolute length change Δ𝑥. For a material, we use the fractional length change (Δ𝑙)/𝑙 (the strain 𝜖). Therefore, Δ𝑥 and (Δ𝑙)/𝑙 are analogous.

3. Energy. For a single spring, we measure energy using the energy 𝐸 directly. For a material, we use an intensive quantity, the energy density ℰ ≡ 𝐸/𝑉. Therefore, 𝐸 and ℰ are analogous.

Because the energy in a spring is

𝐸 ∼ 𝑘(Δ𝑥)2,

(5.128)

by analogy the energy density in a material will be 2

ℰ ∼ 𝑌 (Δ𝑙𝑙) .

(5.129)

Let's estimate 𝑌 by setting Δ𝑙 ∼ 𝑙. Physically, this choice means stretching or compressing each bond by its own length. This harsh treatment is, as a reasonable assumption, sufficient to break the bond and release the binding energy. Then the right side becomes simply the Young's modulus 𝑌.

The left side, the energy density, becomes simply the bond energy per volume. For the volume, if we use the volume of one atom, roughly 𝑎3, then the bond energy contained in this volume is the binding energy of one atom.

Then the Young's modulus becomes

𝐸

𝑌 ∼ binding

𝑎3 .

(5.130)

This result is what we predicted based on the dimensions of pressure. However, we now have a physical model of the Young's modulus, based on an analogy between it and spring constant.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.5 Atoms, molecules, and materials 191

Having arrived at this conclusion from dimensions and from an analogy, let's apply it to estimate a typical Young's modulus. To estimate the numerator, the binding energy, start with the typical bond energy of 4 electron volts per bond. With each atom is connected to, say, five or six other atoms, the total energy is roughly 20 electron volts. Because bonds are connections between pairs of atoms, this 20 electron volts counts each bond twice.

Therefore, a typical binding energy is 10 electron volts per atom.

Using 𝑎 ∼ 3 ångströms, a typical stiffness or Young's modulus is 𝐸

𝑌 ∼ binding

× 1.6×10−19 J

𝑎3

∼

10 eV

(3×10−10 m)3

eV

∼ 12 ×1011Jm−3. (5.131)

For very rough estimates, a convenient value to remember 𝑌 (1011 Pa)

is 1011 joules per cubic meter. Because energy density and diamond 12

pressure have the same dimensions, this energy density is steel 2

also 1011 pascals or 106 atmospheres. (Because atmospheric Cu 1.2

pressure is only 1 atmosphere, a factor of 1 million smaller, Al 0.7

it has little effect on solids.)

glass

0.6

Using a typical stiffness, we can estimate sound speeds in granite 0.3

solids. The speed depends not only on the stiffness, but also Pb 0.18

on the density: denser materials respond more slowly to the concrete 0.17

forces due to the stiffness, so sound travels more slowly in oak 0.1

denser substances. From stiffness 𝑌 and density 𝜌, the only ice 0.1

dimensionally correct way to make a speed is 𝑌/𝜌 . If this speed is the speed of sound, then

𝑐s ∼ 𝑌𝜌 .

(5.132)

Based on a typical Young's modulus of 0.5×1011 pascals and a typical density of 2.5 × 103 kilograms per cubic meter (for example, rock), a typical speed of sound is 5 kilometers per second:

𝑐s ∼

0.5×1011 Pa

2.5×103 kg m−3 ≈ 5 km s−1.

(5.133)

This prediction is reasonable for most solids and is exactly correct for steel!

With this estimate, we end our dimensional-analysis tour of the properties of materials. Look what dimensional analysis, combined with analogy and proportional reasoning, has given us: the size of atoms, the energies of chemical bonds, the stiffness of materials, and the speed of sound.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

192

5 Dimensions

5.6 Summary and further problems

A quantity with dimensions has no meaning by itself. As Socrates might have put it, the uncompared quantity is not worth knowing. Using this principle, we learned to rewrite relations in dimensionless form: in terms of combinations of the quantities where the combination has no dimensions.

Because the space of dimensionless relations is much smaller than the space of all possible relations, this rewriting simplifies many problems. Like the other two tools in Part II, dimensional analysis discards complexity without loss of information.

Problem 5.46

Oblateness of the Earth

Because the Earth spins on its axis, it is an oblate sphere. You can estimate the oblateness using di-Rpolar

mensional analysis and some guessing. Our measure of oblateness will be Δ𝑅 = 𝑅eq − 𝑅polar (the Req

difference between the polar and equatorial radii).

Find two independent dimensionless groups built from Δ𝑅, 𝑔, 𝑅 (the Earth's mean radius), and 𝑣 (the Earth's rotation speed at the equator). Guess a reasonable relation between them in order to estimate Δ𝑅. Then compare your estimate to the actual value, which is approximately 21.4 kilometers.

Problem 5.47

Huge waves on deep water

One of the highest measured ocean waves was encountered in 1933 by a US Navy oiler, the USS Ramapo (a 147-meter-long ship) [34]. The wave period was 14.8 seconds. Find its wavelength using the results of Problem 5.11. Would a wave of this wavelength be dangerous to the ship?

Problem 5.48

Ice skating

For world-record ice skating, estimate the power consumed by sliding friction. (Ice skates sliding on ice have a coefficient of sliding friction around 0.005.) Then make that power meaningful by estimating the ratio power consumed in sliding friction

power consumed by air resistance .

(5.134)

Problem 5.49

Pressure melting during ice skating

Water expands when it freezes. Thus, increasing the pressure on ice should, by Le Chatelier's principle, push it toward becoming water — which lowers its freezing point. Based on the freezing point and the heat of vaporization of water, estimate the change in freezing point caused by ice-skate blades. Is this change large enough to explain why ice-skate blades slip with very low friction on a thin sheet of water?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.6 Summary and further problems 193

Problem 5.50

Contact radius

A solid ball of radius 𝑅, density 𝜌, and elastic modulus 𝑌 rests on the ground. Using dimensional analysis, how much can you deduce about the contact radius 𝑟?

Problem 5.51

Contact time

R

The ball of Problem 5.50 is dropped from a height, hits a r

r

hard table with speed 𝑣, and bounces off. Using dimensional analysis, how much can you deduce about the contact time?

Problem 5.52

Floating on water

Some insects can float on water thanks to the surface tension of water. In terms of the bug size 𝑙 (a length), find the scaling exponents 𝛼 and 𝛽 in 𝐹𝛾 ∝ 𝑙𝛼,

(5.135)

𝑊 ∝ 𝑙𝛽,

where 𝐹𝛾 is the surface-tension force and 𝑊 is the bug's weight. (Surface tension itself has dimensions of force per length.) Thereby explain why a small-enough bug can float on water.

Problem 5.53

Dimensionless measures of damping

A damped spring–mass system has three parameters: the spring constant 𝑘, the mass 𝑚, and the damping constant 𝛾. The damping constant determines the damping force through 𝐹𝛾 = −𝛾𝑣, where 𝑣 is the velocity of the mass.

a. Use these quantities to make the dimensionless group proportional to 𝛾. Mechanical and structural engineers use this group to the define the dimensionless damping ratio 𝜁 :

𝜁 ≡ 12 × the dimensionless group proportional to 𝛾.

(5.136)

b. Find the dimensionless group proportional to 𝛾−1. Physicists and electrical engineers, following conventions from the early days of radio, call this group the quality factor 𝑄.

Problem 5.54

Steel cable under its own weight

The stiffness of a material should not be confused with its strength! Strength is the stress (a pressure) at which the substance breaks; it is denoted 𝜎y. Like stiffness, it is an energy density. The dimensionless ratio 𝜎y/𝜎, called the yield strain 𝜖y, has a physical interpretation: the fractional length change at which the substance breaks. For most materials, it lies in the range 10−3…10−2 — with brittle materials (such as rock) toward the lower end. Using the preceding information, estimate the maximum length of a steel cable before it breaks under its own weight.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

194

5 Dimensions

Problem 5.55

Orbital dynamics

A planet orbits the Sun in an ellipse that can be described by the distance of closest approach 𝑟min and by the furl

thest distance 𝑟max. The length 𝑙 is their harmonic mean: rmin

rmax

Sun

𝑙 = 2 𝑟min𝑟max

𝑟

= 2 (𝑟min ∥ 𝑟max).

(5.137)

min + 𝑟max

(You will meet the harmonic mean again in Problem 8.22, as an example of a more general kind of mean.) The table gives 𝑟min and 𝑟max for the planets, as well as the specific effective potential 𝑉, which is the effective potential energy divided by the planet mass 𝑚 (the effective potential itself mixes the gravitational potential energy with one component of the kinetic energy). The purpose of this problem is to see how universal functions organize this seemingly messy data set.

𝑟min(m)

𝑟max (m)

𝑉 (m2 s−2)

Mercury

4.6001×1010

6.9818×1010

−1.1462×109

Venus

1.0748×1011

1.0894×1011

−6.1339×108

Earth

1.4710×1011

1.5210×1011

−4.4369×108

Mars

2.0666×1011

2.4923×1011

−2.9119×108

Jupiter

7.4067 ×1011

8.1601×1011

−8.5277 ×107

Saturn

1.3498×1012

1.5036×1012

−4.6523×107

Uranus

2.7350×1012

3.0063×1012

−2.3122×107

Neptune

4.4598×1012

4.5370×1012

−1.4755×107

a. On a graph of 𝑉 versus 𝑟, plot all the data. Each planet provides two data points, one for 𝑟 = 𝑟min and one for 𝑟 = 𝑟max. The plot should be a mess. But you'll straighten it out in the rest of the problem.

b. Now write the relation between 𝑉 and 𝑟 in dimensionless form. The relevant quantities are 𝑉, 𝑟, 𝐺𝑀Sun, and the length 𝑙. Choose your groups so that 𝑉

appears only in one group and 𝑟 appears only in a separate group.

c. Now use the dimensionless form to replot the data in dimensionless form. All the points should lie on one curve. You have found the universal function characterizing all planetary orbits!

Problem 5.56

Signal propagation speed in coaxial cable For the coaxial cable of Problem 2.25, estimate the signal propagation speed.

Problem 5.57

Meter stick under pressure

Estimate how much shorter a steel meter stick becomes due to being placed at the bottom of the ocean. What about a meter stick made of wood?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5.6 Summary and further problems 195

Problem 5.58

Speed of sound in water

Using the heat of vaporization of water as a measure of the energy density in its weakest bonds, estimate the speed of sound in water.

Problem 5.59

Delta-function potential

A simple potential used as a model to understand molecules is the one-dimensional delta-function potential 𝑉(𝑥) = −𝐸0𝐿𝛿(𝑥), where 𝐸0 is an energy and 𝐿 is a length (imagine a deep potential of depth 𝐸0 and small width 𝐿). Use dimensional analysis to estimate the ground-state energy.

Problem 5.60

Tube flow

In this problem you study fluid flow through a narrow r

tube. The quantity to predict is 𝑄, the volume flow rate flow

(volume per time). This rate depends on five quantities: l

𝑙

the length of the tube

Δ𝑝

the pressure difference between the tube ends 𝑟

the radius of the tube

𝜌

the density of the fluid

𝜈

the kinematic viscosity of the fluid

a. Find three independent dimensionless groups 𝐺1, 𝐺2, and 𝐺3 from these six quantities — preparing to write the most general statement as group 1 = 𝑓 (group 2, group 3).

(5.138)

Hint: One physically reasonable group is 𝐺2 = 𝑟/𝑙; to make solving for 𝑄 possible, put 𝑄 only in group 1 and make this group proportional to 𝑄.

b. Now imagine that the tube is long and thin (𝑙 ≫ 𝑟) and that the radius or flow speed is small enough to make the Reynolds number low. Then deduce the form of 𝑓 using proportional reasoning: First find the scaling exponent 𝛽 in 𝑄 ∝ (Δ𝑝)𝛽; then find the scaling exponent 𝛾 in 𝑄 ∝ 𝑙𝛾. Hint: If you double Δ𝑝

and 𝑙, what should happen to 𝑄?

Determine the form of 𝑓 that satisfies all your proportionality requirements.

If you get stuck, work backward from the correct result. Look up Poiseuille flow, and use the result to deduce the preceding proportionalities; and then give reasons for why they are that way.

c. The analysis in the preceding parts does not give you the universal, dimensionless constant. Use a syringe and needle to estimate the constant. Compare your estimate with the value that comes from solving the equations of fluid mechanics honestly (by looking up this value).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

196

5 Dimensions

Problem 5.61

Boiling versus boiling away

Look up the specific heat of water in the table of constants (p. xvii) and estimate the ratio

energy to bring a pot of water to boiling temperature energy to boil away the boiling water

.

(5.139)

Problem 5.62

Kepler's law for elliptical orbits

Kepler's third law connects the orbital period to the minimum and maximum orbital radii 𝑟min and 𝑟max and to the gravitational strength of the Sun: 𝑇 = 2𝜋 𝑎3/2 ,

(5.140)

𝐺𝑀Sun

where the semimajor axis 𝑎 is defined as 𝑎 ≡ (𝑟min + 𝑟max)/2. Write Kepler's third law in dimensionless form, making one independent dimensionless group proportional to 𝑇 and the other group proportional to 𝑟min.

Problem 5.63

Why Mars?

Why did Kepler need data about Mars's orbit to conclude that planets orbit the Sun in an ellipse rather than a circle? Hint: See the data in Problem 5.55.

Problem 5.64

Froude number for a ship's hull speed

For a ship, the hull speed is defined as

𝑣 ≡ 1.34 𝑙 ,

(5.141)

where 𝑣 is measured in knots (nautical miles per hour), and 𝑙, the waterline length, is measured in feet. The waterline length is, as you might expect, the length of the boat measured at the waterline. The hull speed is a boat's maximum speed before the water drag becomes very large.

Convert this unit-specific formula to an approximate Froude number 𝖥𝗋, the dimensionless number introduced in Section 5.1.1 to estimate the maximum walking speed. For the hull speed, the Froude number is defined as 𝖥𝗋 ≡ 𝑣2

𝑔𝑙 .

(5.142)

From the approximate Froude number, guess the exact value!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae
