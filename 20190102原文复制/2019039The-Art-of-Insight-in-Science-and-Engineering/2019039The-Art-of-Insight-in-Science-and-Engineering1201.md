135

When there is change, look for what does not change. That principle, introduced when we studied symmetry and conservation (Chapter 3), is also the basis for our next tool, proportional reasoning.

4.1 Population scaling

An everyday example of proportional reasoning often happens when cooking for a dinner party. When I prepare fish curry, which I normally cook for our family of four, I buy 250 grams of fish. But today another family of four will join us.

How much fish do I need?

I need 500 grams. As a general relation,

new amount = old amount × new number of diners usual number of diners.

(4.1)

Another way to state this relation is that the amount of fish is proportional to the number of diners. In symbols,

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

104

4 Proportional reasoning

𝑚fish ∝ 𝑁diners,

(4.2)

where the ∝ symbol is read「is proportional to.」

But where in this analysis is the quantity that does not change?

Another way to write the proportionality relation is new amount of fish

new number of diners = old amount of fish

old number of diners.

(4.3)

Thus, even when the number of diners changes, the quotient amount of fish

number of diners

(4.4)

does not change.

For an analogous application of proportional reasoning, here's one way to estimate the number of gas stations in the United States. Following the principle of using human-sized numbers, which we discussed in Section 1.4, I did not try to estimate this large number directly. Instead, I started with my small hometown of Summit, New Jersey. It had maybe 20 000 people and maybe five gas stations; the「maybe」indicates that these childhood memories may easily be a factor of 2 too small or too large. If the number of gas stations is proportional to the population (𝑁stations ∝ 𝑁people), then 𝑁US

people

𝑁US

3×108

⏞

stations = 𝑁 Summit

stations ×

.

(4.5)

2×104

⏟

𝑁Summit

people

The population ratio is roughly 15 000. Therefore, if Summit has five gas stations, the United States should have 75 000. We can check this estimate.

The US Census Bureau has an article (from 2008) entitled「A Gas Station for Every 2,500 People」; its title already indicates that an estimate of roughly 105 gas stations is reasonably accurate: Summit, in my reckoning, had 4000

people per gas station. Indeed, the article gives the total as 116 855 gas stations—as close to the estimate as we can expect given the uncertainties in childhood memories!

Problem 4.1

Homicide rates

The US homicide rate (in 2011) was roughly 14 000 per year. The UK rate in the same year was roughly 640. Which is the more dangerous country (per person), and by what factor?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 105

4.2 Finding scaling exponents

The dinner example (Section 4.1) used linear proportionality: When the number of dinner guests doubled, so did the amount of food. The relation between the quantities had the form 𝑦 ∝ 𝑥 or, more explicitly, 𝑦 ∝ 𝑥1. The exponent, which here is 1, is called the scaling exponent. For that reason, proportionalities are often called scaling relations. Scaling exponents are a powerful abstraction: Once you know the scaling exponent, you usually do not care about the mechanism underlying it.

4.2.1 Warmup

After linear proportionality, the next simplest and most common

√

type of proportionality is quadratic—a scaling exponent of 2—and 5 cm

=

its close cousin, a scaling exponent of 1/2. As an example, here is d big

a big circle with diameter 𝑑big = 5 cm.

What is the diameter of the circle with one-half the area of this circle?

Abig

Let's first do the very common brute-force solution, which does not use proportional reasoning, so that you see what not to do. It begins with the area of the big circle:

= ?

d small

𝐴big = 𝜋4𝑑2big = 54𝜋 cm2.

(4.6)

Abig

Asmall =

The area of the small circle 𝐴small is 𝐴big/2, so 𝐴small = 5𝜋/8 cm2.

2

Therefore, the diameter of the small circle is given by 𝑑small = 𝐴small

𝜋/4 = 52 cm.

(4.7)

Although this result is correct, by including 𝜋/4 and then dividing it out, we run around Robin Hood's barn (all of Sherwood forest) to reach a simple result. There must be a more elegant and insightful approach.

This improved approach also starts with the relation between a circle's area and its diameter: 𝐴 = 𝜋𝑑2/4. However, it discards the complexity early—in the next step—rather than carrying it through the analysis and having it vanish only at the end. An everyday analog of this approach is packing for a trip. Rather than dragging around books that you will not read or clothes that you will not wear, prune early and travel light: Pack only what you will use and set aside the rest.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

106

4 Proportional reasoning

To lighten your problem-solving luggage, observe that all circles, independent of their diameter, have the same prefactor 𝜋/4 connecting 𝑑2 and 𝐴.

Therefore, when we make a proportionality or scaling relation between 𝐴

and 𝑑, we discard the prefactor. The result is the following quadratic proportionality (one where the scaling exponent is 2): 𝐴 ∝ 𝑑2.

(4.8)

For finding the new diameter, we need the inverse scaling relation: 𝑑 ∝ 𝐴1/2.

(4.9)

In this form, the scaling exponent is 1/2. This proportionality is shorthand for the ratio relation

𝑑

1/2

small

𝐴small ⎞

𝑑

= ⎛⎜

⎟ .

(4.10)

big

⎝ 𝐴big ⎠

The area ratio is 1/2, so the diameter ratio is 1/ 2. Because the large diameter is 5 cm, the small diameter is 5/2 cm.

The proportional-reasoning solution is

shorter than the brute-force approach,

Abig

A

= 5π

= 5 cm2

cm

Asmall = 5π cm2

cm

4

small = 5π

4

8

so it offers fewer places to go wrong. It

(extra baggage)

is also more general: It shows that the

π

r

A

A =

d2

d =

4

π/4

result does not require that the shape

√

r

√

be a circle. As long as the area of the

d ∝ A1/2

5

dbig

d

= 5 cm

dsmall

d

=

cm

shape is proportional to the square of

prop. reasoning

2

its size (as a length)—a relation that

holds for all planar shapes—the length ratio is 1/ 2 whenever the area ratio is 1/2. All that matters is the scaling exponent.

Problem 4.2

Length of the horizontal bisecting path

In Problem 3.23, about the shortest path that bisects an equilateral triangle, one candidate path is a horizontal line. How long is that line relative to a side of the triangle?

Areas are connected to flux, because flux is rate per area. Thus, the scaling exponent for area—namely, 2—appears in flux relationships. For example: What is the solar flux at Pluto's orbit?

The solar flux 𝐹 at a distance 𝑟 from the Sun is the solar luminosity 𝐿Sun—the radiant power output of the sun—spread over a sphere with radius 𝑟: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 107

𝐹 = 𝐿Sun

4𝜋𝑟2 .

(4.11)

Even as 𝑟 changes, the solar luminosity remains the same (conservation!), as does the factor of 4𝜋. Therefore, in the spirit of packing light for a trip, simplify the equality 𝐹 = 𝐿Sun/4𝜋𝑟2 to the proportionality 𝐹 ∝ 𝑟−2

(4.12)

by discarding the factors 𝐿Sun and 4𝜋. The scaling exponent here is −2: The minus sign indicates the inverse proportionality between flux and area, and the 2 is the scaling exponent connecting 𝑟 to area.

The scaling relation is shorthand for

𝐹

−2

Pluto's orbit

𝐹

= (𝑟Pluto's orbit ) ,

(4.13)

Earth's orbit

𝑟Earth's orbit

or

−2

𝐹Pluto's orbit = 𝐹Earth's orbit (𝑟Pluto's orbit 𝑟

) .

(4.14)

Earth's orbit

The ratio of orbital radii is roughly 40. Therefore, the solar flux at Pluto's orbit is roughly 40−2 or 1/1600 of the flux at the Earth's orbit. The resulting flux is roughly 0.8 watts per square meter:

𝐹Pluto's orbit = 1300 W

m2 × 1

1600 ≈ 0.8 W

m2 .

(4.15)

Receiving such a small amount of sunlight, Pluto must be very cold. We can estimate its surface temperature with a further proportionality.

Surface temperature depends mostly on so-called energy

sunlight

blackbody

at planet

blackbody radiation. The surface temperature is surface

radiation

the temperature at which the radiated flux equals the incoming flux; we are making another box model. The radiated flux is given by the blackbody formula (which we will derive in Section 5.5.2)

𝐹 = 𝜎𝑇4,

(4.16)

where 𝑇 is the temperature, and 𝜎 is the Stefan–Boltzmann constant: 𝜎 ≈ 5.7 ×10−8 W .

(4.17)

m2 K4

What is the resulting surface temperature on Pluto?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

108

4 Proportional reasoning

As with any proportional-reasoning calculation, there is a long-winded, brute-force alternative (try Problem 4.5). The elegant approach directly uses the proportionalities

𝑇 ∝ 𝐹1/4

and

𝐹 ∝ 𝑟−2,

(4.18)

where 𝑟 is the orbital radius. Together, they produce a new proportionality 𝑇 ∝ (𝑟−2)1/4 = 𝑟−1/2.

(4.19)

A compact graphical notation, similar to the divide-and-conquer trees, encapsulates this derivation:

1

r

−2

F

T

4

As indicated by the 𝑟 → 𝐹 arrow, changing 𝑟 changes 𝐹. The boxed number along the arrow gives the scaling exponent. Therefore, the 𝑟 → 𝐹 arrow represents 𝐹 ∝ 𝑟−2. The 𝐹 → 𝑇 arrow indicates that changing 𝐹 changes 𝑇

and, in particular, that 𝑇 ∝ 𝐹1/4.

To find the scaling exponent connecting 𝑟 to 𝑇, multiply the scaling exponents along the path:

−2 × 14 = −12.

(4.20)

Problem 4.3

Explaining the graphical notation

In our graphical representation of scaling relations, why is the final scaling exponent the product, rather than the sum, of the scaling exponents along the way?

This scaling exponent represents the following comparison: 𝑇

−1/2

1/2

Earth

𝑇

= (𝑟Earth's orbit )

= (𝑟Pluto's orbit ) .

(4.21)

Pluto

𝑟Pluto's orbit

𝑟Earth's orbit

(The rightmost form, with the positive exponent, is more direct than the intermediate form, because it does not first produce a fraction smaller than 1

and then take its reciprocal with a negative exponent.) The ratio of orbital radii is 40, so the ratio of surface temperatures should be 40 or roughly 6.

Pluto's surface temperature should be roughly 50 K: 𝑇Pluto ≈ 𝑇Earth

6 ≈ 293 K

6 ≈ 50 K.

(4.22)

Pluto's actual mean surface temperature is 44 K, very close to our prediction based on proportional reasoning.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 109

Problem 4.4

Explaining the discrepancy

Why is our prediction for Pluto's mean temperature slightly too high?

Problem 4.5

Brute-force calculation of surface temperature To practice recognizing common but inferior problem-solving methods, use the brute-force method to estimate the surface temperature on Pluto: (a) From the solar flux at Pluto's orbit, calculate the solar flux averaged over the surface; (b) use that flux to estimate a blackbody temperature.

4.2.2 Orbital periods

In the preceding examples, the scaling relations formed chains (trees without branching):

food for a dinner party : Nguests +1

mfish

area of a circle : r +2

Acircle

(4.23)

surface temperature :

1

r

−2

F

T

4

More elaborate relationships also occur—as we will find in rederiving a famous law of planetary motion.

How does a planet's orbital period depend on its orbital radius 𝑟 ?

We'll study the special case of circular orbits (many planetary orbits are close to circular). Our exploratory thinking is often aided by making proportionality questions concrete. Therefore, rather than finding the scaling exponent using the abstract notion of「depend on,」answer the doubling question:「When I double this quantity, what happens to that quantity?」

What is so special about doubling?

Doubling—multiplying by a factor of 2—is the simplest useful change. A factor of 1 is simpler; however, being no change at all, it is too simple.

What happens to the period if we double the orbital radius?

The most direct effect of doubling the orbital radius is that gravity gets weaker. Because the gravitational force is an inverse-square force—that is, 𝐹 ∝ 𝑟−2—the gravitational force falls by a factor of 4. A compact and intuitive notation for these changes is to mark the change directly under the quantity: A notation of ×𝑛 indicates multiplication by a factor of 𝑛.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

110

4 Proportional reasoning

𝐹󾏟 ∝ 𝑟󾏟 −2.

(4.24)

× 14

×2

Because force is proportional to acceleration, the planet's acceleration 𝑎 falls by the same factor of 4.

In circular motion, acceleration and velocity are related by 𝑎 = 𝑣2/𝑟. (We will derive this relation in Section 5.1.1 and Section 6.3.4, with two different reasoning tools.) Therefore, the orbital velocity 𝑣 is 𝑎𝑟 , and doubling the radius increases the orbital speed by a factor of 1/2: 𝑣󾏟 = ( 𝑎󾏟 × 𝑟󾏟 )1/2.

(4.25)

× 12

× 14 ×2

Although this calculation is correct, when it is stated as a factor of 1/2

it confounds our expectations and produces numerical whiplash. As we finish reading「increases by a factor of,」we expect a number greater than 1.

But we get a number smaller than 1. An increase by a factor smaller than 1

is more simply described as a decrease. Therefore, it is more direct to say that the orbital speed falls by a factor of 2.

The orbital period is 𝑇 ∼ 𝑟/𝑣 (the ∼ contains the dimensionless prefactor 2𝜋), so it increases by a factor of 23/2:

𝑇󾏟 ∼ 𝑟󾏟 × 𝑣−1

⏟ .

(4.26)

×23/2

×2

× 2

In summary, doubling the orbital radius multiplies the orbital period by 23/2. In general, the connection between 𝑟 and 𝑇 is 𝑇 ∝ 𝑟3/2.

(4.27)

This result is Kepler's third law for circular orbits. Our scaling analysis has the following graphical representation:

F

+1

a

+ 1

−2

2

r

+ 1

v

2

−1

T

+1

In this structure, the new feature is that two paths reach the orbital velocity 𝑣. There we add the incoming exponents.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 111

1. r +1

v represents the 𝑟 in 𝑣 = 𝑎𝑟 . It carries +1/2 powers of 𝑟.

2

2. a +1

v represents the 𝑎 in 𝑣 = 𝑎𝑟 . To determine how many 2

powers of 𝑟 flow through this arrow, follow the chain containing it: r

−2

F

+1

a

+ 1

v

2

One power of 𝑟 starts at the left side. It becomes −2 powers after passing through the first scaling exponent and arriving at 𝐹. It remains −2

powers on arrival at 𝑎. Finally, it becomes −1 power on arrival at 𝑣. This path therefore carries −1 power of 𝑟.

Its contribution is the result of multiplying the three scaling exponents along the chain:

−2 × +1 × −1 = −1.

(4.28)

⏟ ⏟

2

⏟

𝑟→𝐹

𝐹→𝑎

𝑎→𝑣

The −1 power carried by the three-link chain, representing 𝑟−1, combines with the +1/2 from the direct 𝑟 → 𝑣 arrow, which represents 𝑟+1/2. Adding the exponents on 𝑟, the result is that 𝑣 contains −1/2 powers of 𝑟: 𝑣 ∝ 𝑟−1

⏟ × 𝑟+1/2

⏟ = 𝑟−1/2.

(4.29)

via 𝐹

direct

Let's practice the same reasoning by finding the scaling relation connecting 𝑇 and 𝑟—which is Kepler's third law. The direct 𝑟 → 𝑇 arrow, with a scaling exponent of +1, carries +1 powers of 𝑟. The 𝑣 → 𝑇 arrow carries −1 powers of 𝑣. Because 𝑣 contains −1/2 powers of 𝑟, the 𝑣 → 𝑇 arrow carries +1/2

powers of 𝑟:

−12 × −1 = +1

⏟ ⏟

2.

(4.30)

𝑟→𝑣

𝑣→𝑇

Together, the two arrows contribute +3/2 powers of 𝑟 and give us Kepler's third law:

𝑇 ∝ 𝑟+1

⏟ × 𝑟+1/2

⏟ = 𝑟+3/2.

(4.31)

𝑟→𝑇

via 𝑣

To summarize the exponent rules, for which we now have several illustra-tions: (1) Multiply exponents along a path, and (2) add exponents when paths meet.

Now let's apply Kepler's third law to a nearby planet.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

112

4 Proportional reasoning

How long is the Martian year?

The proportionality 𝑇 ∝ 𝑟3/2 is shorthand for the comparison 𝑇

3/2

Mars

𝑇

= (𝑟Mars ) ,

(4.32)

ref

𝑟ref

where 𝑟Mars is the orbital radius of Mars, 𝑟ref is the orbital radius of a reference planet, and 𝑇ref is its orbital period. Because we are most familiar with the Earth, let's choose it as the reference planet. The reference period is 1

(Earth) year; and the reference radius is 1 astronomical unit (AU), which is 1.5×1011 meters. The benefit of this choice is that we will obtain the period of Mars's orbit in the familiar unit of Earth years.

The distance of Mars to the Sun varies between 2.07 × 1011 meters (1.38 astronomical units) and 2.49 × 1011 meters (1.67 astronomical units). Thus, the orbit of Mars is not very circular and has no single orbital radius 𝑟Mars.

(Its significant deviation from circularity allowed Kepler to conclude that planets move in ellipses.) As a proxy for 𝑟Mars, let's use the average of the minimum and maximum radii. It is 1.52 astronomical units, making the ratio of orbital periods approximately 1.88: 𝑇

3/2

Mars

𝑇

= (1.52 AU

≈ 1.88.

(4.33)

Earth

1 AU )

Therefore, the Martian year is 1.88 Earth years long.

Problem 4.6

Brute-force calculation of the orbital period To emphasize the contrast between proportional reasoning and the brute-force approach, find the period of Mars's orbit using the brute-force approach by starting with Newton's law of gravitation and then finding the orbital velocity and circumference.

A surprising conclusion about orbits comes from our doubling question introduced on page 109.

What happens to the period of a planet if you double its mass?

Using a type of thought experiment due to Galileo, imagine two identical planets, orbiting one just behind the other along the same orbital path. They have the same period. Now tie them together. The rope does not change the period, so the double-mass planet has same period as each individual planet: The scaling exponent is zero (𝑇 ∝ 𝑚0)!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 113

Problem 4.7

Pendulum period versus mass

How does the period of an ideal pendulum depend on the mass of the bob?

4.2.3 Projectile range

v

In the previous examples, only one variable was independent; changing it changed all the others.

θ

However, many problems contain multiple independent variables. An example is the range 𝑅 of R

a rock launched at an angle 𝜃 with speed 𝑣. The traditional derivation uses calculus. You solve for the position of the rock as a function of time, solve for the time when its height is zero (the ground level), and then insert that time into the horizontal position to find the range.

This analysis is not wrong, but its result still seems like magic. I leave unsatisfied, thinking,「The result must be true. But I still do not know why.」

That「why」insight comes from proportional reasoning, which discards the nonessential complexity. Let's begin with our doubling question.

How does doubling each of the independent variables affect the range?

The independent variables include the launch velocity 𝑣, the gravitational acceleration 𝑔 (because gravity returns the rock to Earth), and the launch angle. However, angles do not fit so easily into proportional reasoning, so we won't explore the role of 𝜃 here (we will handle it in Section 8.2.2.1 using the tool of easy cases, or you can try Problem 4.9).

Because the only forces are vertical, the rock's horizontal velocity remains constant throughout its flight (an invariant!). Thus, the range is given by 𝑅 = time aloft × initial horizontal velocity.

(4.34)

The time aloft is determined by the initial vertical velocity, because gravity steadily reduces it (at the rate 𝑔):

initial vertical velocity

time aloft ∼

𝑔

.

(4.35)

Problem 4.8

Missing dimensionless prefactor

What is the missing dimensionless prefactor in the preceding expression for the time that the rock stays aloft?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

114

4 Proportional reasoning

Now double the launch velocity 𝑣. That change doubles the initial horizontal and vertical components of the velocity. Doubling the vertical component doubles the time aloft. Because the range is proportional to the horizontal velocity and to the time aloft, when the launch velocity doubles, the range quadruples. The scaling exponent connecting 𝑣 to 𝑅 is 2: 𝑅 ∝ 𝑣2.

What is the effect of doubling 𝑔 ?

Doubling 𝑔 doesn't change the horizontal velocity or the initial vertical velocity, but it halves the time aloft and therefore the range as well. The scaling exponent connecting 𝑔 to 𝑅 is −1: 𝑅 ∝ 𝑔−1.

The combined scaling relation, which gives the dependence of 𝑅 on both 𝑔

and 𝑣, is

𝑅 ∝ 𝑣2𝑔.

(4.36)

Using 𝑣𝑥 and 𝑣𝑦 for the horizontal and vertical components of the launch velocity, the graphical representation of this reasoning is vx

+

+

1

1

v

R

+1

v

+1

y

+1

t

−1

g

This graph shows a new feature: two independent variables, 𝑣 and 𝑔. We'll need to track the powers of 𝑣 and 𝑔 separately.

The range 𝑅 has two incoming paths. The path via the horizontal velocity 𝑣𝑥 contributes +1 × +1 = +1 powers of 𝑣 but no powers of 𝑔. The path via 𝑡 also contributes +1 powers of 𝑣, and contributes −1 powers of 𝑔. The diagram compactly represents how 𝑅 became proportional to 𝑣2/𝑔.

The full range formula, including the launch angle 𝜃 is 𝑅 ∼ 𝑣2𝑔 sin𝜃cos𝜃.

(4.37)

The dependence on 𝑣 and 𝑔 is just as we predicted.

The moral of this example is that you can derive and understand relations by ignoring constants of proportionality and instead concentrating on the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.2 Finding scaling exponents 115

scaling exponents. Furthermore, you can use this ability in order to spot mistakes: Just check each independent variable's scaling exponent. For example, if someone proposes that projectile range 𝑅 is proportional to 𝑣3/𝑔, think,「The 1/𝑔 makes sense from the time aloft. But what about the 𝑣3?

One power of 𝑣 comes from the horizontal velocity and one power from the time aloft, which explains two powers of 𝑣. But where does the third power comes from? The range should instead contain 𝑣2/𝑔.」

Problem 4.9

Angular factors in projectile range

Explain the sin 𝜃 and cos 𝜃 factors by using the relation range = time aloft × horizontal velocity.

(4.38)

4.2.4 Planetary surface gravity

Scaling, or proportional reasoning, connects independent to dependent variables. Often we have freedom in choosing the independent variables. Here is an example to show you how to use that freedom.

Assuming that planets are uniform spheres, how does 𝑔 , the gravitational acceleration at the surface, depend on the planet's radius 𝑅 ?

We seek the scaling exponent 𝑛 in 𝑔 ∝ 𝑅𝑛. At the planet's surface, the gravitational force 𝐹 on an object of mass 𝑚 is 𝐺𝑀𝑚/𝑅2, where 𝐺 is Newton's constant, and 𝑀 is the planet's mass. The gravitational acceleration 𝑔 is 𝐹/𝑚 or 𝐺𝑀/𝑅2. Because 𝐺 is the same for all objects, we pack light and eliminate 𝐺 to make the proportionality

𝑔 ∝ 𝑀

𝑅2 .

(4.39)

In this form, with mass 𝑀 and radius 𝑅 as the independent variables, the scaling exponent 𝑛 is −2.

However, an alternative relation comes from noticing that the planet's mass 𝑀 depends on the planet's radius 𝑅 and density 𝜌 as 𝑀 ∼ 𝜌𝑅3. Then 𝑔 ∝ 𝜌𝑅3

𝑅2 = 𝜌𝑅.

(4.40)

In this form, with density and radius as the independent variables, the scaling exponent on 𝑅 is now only 1.

Which scaling relation, with mass or density, is preferable?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

116

4 Proportional reasoning

Planets vary widely in their mass: from 3.3 × 1023 kilograms (Mercury) to 1.9×1027 kilograms (Jupiter), a range 4 decades wide (a factor of 104). They vary greatly in their radius: from 7 ×104 kilometers (Jupiter) down to 2.4×

103 kilometers (Mercury), a range of a factor of 30. The quotient 𝑀/𝑅2 has huge variations in the numerator and denominator that mostly oppose each other. When there is change, look for what does not change—or, at least, what does not change as much. In contrast to masses, planetary densities vary from only 0.7 grams per cubic centimeter (Saturn) to 5.5 grams per cubic centimeter (Earth)—a range of only a factor of 8. The variations in planetary surface gravity are easier to understand using the planet's radius and density rather than its radius and mass.

This result is general. Mass is an extensive quantity: When two objects combine, their masses add. Density, in contrast, is an intensive quantity.

Adding more of a particular substance does not change its density. Using intensive quantities for the independent variables usually leads to more insightful results than using extensive quantities does.

Problem 4.10

Distance to the Moon

The orbital period near the Earth's surface (say, for a low-flying satellite) is roughly 1.5 hours. Use that information to estimate the distance to the Moon.

Problem 4.11

Moon's angular diameter and radius

On a night with a full moon, estimate the Moon's angular diameter—that is, the visual angle subtended by the Moon. Use that angle and the result of Problem 4.10

to estimate the Moon's radius.

Problem 4.12

Surface gravity on the Moon

Assuming that all planets (and moons) have the same density, use the radius of the Moon (Problem 4.11) to estimate its surface gravity. Then compare your estimate with the actual value and suggest an explanation for the discrepancy.

Problem 4.13

Gravitational strength inside a planet

Imagine a uniform, spherical planet with radius 𝑅. How does the gravitational acceleration 𝑔 depend on 𝑟, the distance from the center of the planet? Give the scaling exponent when 𝑟 < 𝑅 and when 𝑟 ≥ 𝑅, and sketch 𝑔(𝑟).

Problem 4.14

Making toast land butter-side up

As a piece of toast slides off a dining table (starting with almost no horizontal velocity), it picks up angular velocity. Once it leaves the table, its angular velocity remains constant. In everyday experience, a toast usually backflips (rotates 180∘) by the time it hits the ground, and lands butter-side down. How high would tables have to be for a piece of toast to land butter-side up?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.3 Scaling exponents in fluid mechanics 117

4.3 Scaling exponents in fluid mechanics

The preceding introductory examples may mislead you into thinking that proportional reasoning is useful only when we could also find the exact solution. As a counterexample, we return to that source of mathematical beauty but also misery, fluid mechanics, where exact solutions exist for hardly any situations of practical interest. To make progress, we need to discard complexity by focusing on the scaling exponents.

4.3.1 Falling cones

In Section 3.5.1, we used conservation reasoning to show that the drag force is given by

𝐹drag ∼ 𝜌𝐴cs𝑣2.

(4.41)

In Section 3.5.2, we tested this result by correctly predicting the terminal speed of a falling paper cone. However, that experiment concerned only one cone of a particular size. A natural generalization of that experiment is to predict a cone's terminal speed as a function of its size.

How does the terminal speed of a paper cone depend on its size?

Size is an ambiguous notion. It might refer to an area, a volume, or a length.

Here, let's consider size to be the cone's cross-sectional radius 𝑟. The quantitative question is to find the scaling exponent 𝑛 in 𝑣 ∝ 𝑟𝑛, where 𝑣 is the cone's terminal speed.

The doubling question is,「What happens to the terminal speed when we double 𝑟?」At the terminal speed, drag and weight 𝑚𝑔 balance: 𝜌air𝐴cs𝑣2

⏟⏟⏟⏟⏟ ∼ 𝑚𝑔.

⏟

(4.42)

drag

weight

Therefore, the terminal speed is just what we found in Section 3.5.2: 𝑣 ∼

𝑚𝑔

𝜌

.

(4.43)

air𝐴cs

All cones feel the same 𝑔 and 𝜌air, so we pack light and eliminate these variables to make the proportionality

𝑣 ∝

𝑚

𝐴 .

(4.44)

cs

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

118

4 Proportional reasoning

Doubling 𝑟 quadruples the amount of paper used to make the cone and therefore its mass 𝑚. It also quadruples its cross-sectional area 𝐴cs. According to the proportionality, the two effects cancel: When 𝑟 doubles, 𝑣 should remain constant. All cones of the same shape (and made from the same paper) should fall at the same speed!

This result always surprises me. So I tried the experiment. I printed the cone template in Section 3.5.2 at 400-percent magnification (a factor of 4 increase in length), cut it out, taped the two straight edges together, and raced the small and big cones by dropping them from a height of about 2 meters.

After a roughly 2-second fall, they landed almost simultaneously—within 0.1 seconds of each other. Thus, their terminal speeds are the same, give or take 5 percent.

Proportional reasoning triumphs again! Surprisingly, the proportional-reasoning result is much more accurate than the drag-force estimate 𝜌air𝐴cs𝑣2

on which it is based.

How can predictions based on proportional reasoning be more accurate than the original relations?

To see how this happy situation arose, let's redo the calculation but include the dimensionless prefactor in the drag force. With the dimensionless prefactor (shaded in gray), the drag force is

𝐹drag = 12𝑐d 𝜌air𝐴cs𝑣2,

(4.45)

where 𝑐d is the drag coefficient (introduced in Section 3.2.1). The prefactor carries over to the terminal speed:

𝑣 =

𝑚

.

(4.46)

12𝑐d 𝐴cs

Ignoring the prefactor decreases 𝑣 by a factor of 2/𝑐d . (For nonstreamlined objects, 𝑐d ∼ 1, so the decrease is roughly by a factor of 2.) In contrast, in the ratio of terminal speeds 𝑣big/𝑣small, the prefactor drops out. Here is the ratio with the prefactors shaded in gray: 𝑣big

𝑚big

𝑚small

𝑣

=

.

(4.47)

small

1

⁄

1

2𝑐big

d

𝐴big

cs

2𝑐small

d

𝐴small

cs

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.3 Scaling exponents in fluid mechanics 119

As long as the drag coefficients 𝑐d are the same for the big and small cones, they divide out from the ratio. Then the scaling result—that the terminal speed is independent of size—is exact, independent of the drag coefficient.

The moral, once again, is to build on what we know, rather than computing quantities that we do not need and that only clutter the analysis and thereby our thinking. Scaling relations bootstrap our knowledge. Here, if you know the terminal speed of the small cone, use that speed—and the scaling result that speed is independent of size—to find the terminal speed of the large cone. In the next section, we will apply this approach to estimate the fuel consumption of a plane.

Problem 4.15

Taping the cones

The big cone, with twice the radius of the small cone, has four times the weight of paper. But what about the tape? If you tape along the entire radius of the cone template, how does the length of the tape compare between the large and small cones? How should you apply the tape in order to maintain the 4 : 1 weight ratio?

Problem 4.16

Bigger and bigger cones

Further test the scaling relation 𝑣 ∝ 𝑟0 (terminal speed is independent of size) by building a huge cone from a template with four times the radius of the template for the small cone. Then race the small, big, and huge cones.

Problem 4.17

Four cones versus one cone

Use the cone template in Section 3.5.2 (at 200-percent enlargement) to make five small cones. Then stack four of the cones to make one heavy small cone. How much faster will the four-cone stack fall in comparison to the single small cone?

That is, predict the ratio of terminal speeds 𝑣four cones

𝑣

.

(4.48)

one cone

Then check your prediction by trying the experiment.

4.3.2 Fuel consumption of a Boeing 747 jumbo jet In Section 3.5.4, we estimated the fuel consumption of automobiles. For the next example, we'll estimate the fuel consumption of a Boeing 747 jumbo jet. Rather than repeating the structure of the automobile estimate in Section 3.5.4 but with parameters for a plane—which would be the brute-force approach—we will reuse the automobile estimate and supplement it with proportional reasoning.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

120

4 Proportional reasoning

A plane uses its fuel to generate energy to fight drag and to generate lift.

However, for this estimate, forget about lift. At a plane's cruising speed, lift and drag are comparable (as we will show in Section 4.6). Neglecting lift ignores only a factor of 2, because lift plus drag is twice the lift alone, and allows us to make a decent estimate without having to estimate the lift.

Divide and conquer: Don't bite off all the complexity at once!

The energy consumed fighting drag is proportional to the drag force: 𝐸 ∝ 𝜌air𝐴cs𝑣2.

(4.49)

This scaling relation is shorthand for the following comparison between a plane and a car:

𝐸

2

plane

𝜌cruising altitude

𝑣

air

𝐴plane

cs

plane

𝐸

=

×

× (

) .

(4.50)

car

𝜌sea level

𝐴car

𝑣

air

cs

car

Thus, the energy-consumption ratio breaks into three ratio estimates.

What are reasonable estimates for the three ratios?

1. Air density. A plane's cruising altitude is typically 35 000 feet or 10 kilometers, which is slightly above Mount Everest. At that height, mountain climbers require oxygen tanks, so the air, and oxygen, density must be significantly lower than it is at sea level. (Once you learn the reasoning tool of lumping, you can predict the density—see Problem 6.36.) The density ratio turns out to be roughly 3:

𝜌cruising altitude

air

≈ 1

𝜌sea level

3.

(4.51)

air

The thinner air wins the plane a factor of 3 in fuel efficiency.

2. Cross-sectional area. To estimate the cross-sectional area of the plane body

plane, we need to estimate the width and height of the plane's body; its wings are very streamlined, so they contribute negli-3 units

gible drag. When estimating lengths, let's make our measuring rod (our unit) a person length. Using this measuring rod has cross section

two benefits. First, the measuring rod is easy for our gut to picture, because we feel our own size innately. Second, the lengths that we will measure will be only a small multiple of a person length. The numerical part of the quantity (for example, the 1.5 in「1.5 person lengths」) will be comparable to 1, and therefore also easy to picture. As a rule of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.3 Scaling exponents in fluid mechanics 121

thumb, ratios between 1/3 and 3 are easy to picture and feel in our gut because our mental number hardware is exact for the quantities 1, 2, and 3. We choose our measuring rods accordingly.

In applying the person-length measuring rod to the width of the plane's body, I remember the comfortable days of regulated air travel. As a child, I would find three adjacent empty seats in the back of the plane and sleep for the whole trip (which explains why my parents insist that traveling with small children was easy). A jumbo jet is three or four such seat groups across—call it three person lengths—and its cross section is roughly circular. A circle is roughly a square, so the cross-sectional area is roughly 10 square person lengths:

(3 person lengths)2 ≈ 10 (person length)2.

(4.52)

Although we might worry that this estimate used too many approximations, we should do it anyway: It gives us a rough-and-ready value and allows us to make progress. Our goal is edible jam today, not delicious jam tomorrow!

Now let's estimate the cross-sectional area of a car. In standard units, it's about 3 square meters, as we estimated in Section 3.5.4.

But let's apply our person-sized measuring rod. From noctur-1 unit

nal activities in cars, you may have experienced that cars, uncomfortably, are about one person across. A car's cross section carcrosssection is roughly square, so the cross-sectional area is roughly 1 square person length.

Problem 4.18

Comparing the cross-sectional areas

How well does 1 square person length match 3 square meters?

The ratio of cross-sectional areas is roughly 10; therefore, the plane's larger cross-sectional area costs it a factor of 10 in fuel efficiency.

3. Speed. A reason to fly rather than drive is that planes travel faster than cars. A plane travels almost at the speed of sound: 1000 kilometers per hour or 600 miles per hour. A car travels at around 100 kilometers per hour or 60 miles per hour. The speed ratio is roughly a factor of 10, so 𝑣

2

( plane

𝑣

) ≈ 100.

(4.53)

car

The plane's greater speed costs it a factor of 100 in fuel efficiency.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

122

4 Proportional reasoning

Now we can combine the three ratio estimates to estimate the ratio of energy consumptions:

𝐸plane

𝐸

∼ 1 × 10 × 100 ≈ 300.

(4.54)

car

3

⏟

⏟

⏟

density

area

(speed)2

A plane should be 300 times less fuel efficient than a car—terrible news for anyone who travels by plane!

Should you therefore never fly again?

Our conscience is saved because a plane carries roughly 300 passengers, whereas a typical (Western) car is driven by one person to and from work.

Therefore, per person, a plane and a car should have comparable fuel efficiencies: 30 passenger miles per gallon, as we estimated in Section 3.5.4, or 8 liters per 100 passenger kilometers.

According to Boeing's technical data on the 747-400 model, the plane has a range of 13 450 kilometers, its fuel tank contains 216 840 liters, and it carries 416 passengers. These data correspond to a fuel consumption of 4 liters per 100 passenger kilometers:

216 840 ℓ

13 450 km ×

1

416 passengers ≈

4 ℓ

100 passenger km.

(4.55)

Our proportional-reasoning estimate of 8 liters per 100 passenger kilometers is very reasonable, considering the simplicity of the method compared to a full fluid-dynamics analysis.

Problem 4.19

Density of air by proportional reasoning

Make rough estimates of your own top swimming and cycling speeds, or use the data that a record 5-kilometer swim time is 56:16.6 (almost 1 hour). Thereby explain why the density of water must be roughly 1000 times the density of air. Why is this estimate more accurate when based on cycling rather than running speeds?

Problem 4.20

Raindrop speed versus size

How does a raindrop's terminal speed depend on its radius?

Problem 4.21

Estimating an air ticket price from fuel cost Estimate the fuel cost for a long-distance plane journey—for example, London to Boston, London to Cape Town, or Los Angeles to Sydney. How does the fuel cost compare to the ticket price? (Airlines do not pay many of the fuel taxes paid by ordinary motorists, so their fuel costs are lower than motorists' fuel costs.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.4 Scaling exponents in mathematics 123

Problem 4.22

Relative fuel efficiency of a cycling

Estimate the fuel efficiency, relative to a car, of a bicyclist powered by peanut butter traveling at a decent speed (say, 10 meters per second or 20 miles per hour).

Compare your estimate with your estimate in Problem 3.34.

4.4 Scaling exponents in mathematics

Our scaling relations so far have connected physical quantities. But proportional reasoning can also bring us insight in mathematics. A classic example is the birthday paradox.

How many people must be in a room before the probability that two people share a birthday (for example, two people are born on July 18) is at least 50 percent?

Almost everyone, including me, reasons that, with 365 days in the year, we need roughly 50 percent of 365, or 183 people. Let's test this conjecture. The actual probability of having a shared birthday is 1 − (1 − 1

365) (1 − 2

365) (1 − 3

365) ⋯ (1 − 𝑛 − 1

365 ) .

(4.56)

(A derivation is in Everyday Probability and Statistics [50, p. 49] or in the advanced classic Probability Theory and its Application [13, vol. 1, p. 33]. But you can explain its structure already: Try Problem 4.23.) For 𝑛 = 183, the probability is 1 − 4.8×10−25 or almost exactly 1.

Problem 4.23

Explaining the probability of a shared birthday Explain the pieces of the formula for the probability of a shared birthday: What is the reason for the 1− in front of the product? Why does each factor in the product have a 1 − ? And why does the last factor have (𝑛 − 1)/365 rather than 𝑛/365?

To make this surprisingly high probability seem plausible, I gave random birthdays to 183 simulated people. Two people shared a birthday on 14 days (and we need only one such day); and three people shared a birthday on three days. According to this simulation and to the exact calculation, the plausible first guess of 183 people is far too high. This surprising result is the birthday paradox.

Even though we could use the exact probability to find the threshold number of people that makes the probability greater than 50 percent, we would still wonder why: Why is the plausible argument that 𝑛 ≈ 0.5×365 so badly wrong? That insight comes from a scaling analysis.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

124

4 Proportional reasoning

At roughly what 𝑛 does the probability of a shared birthday rise above 50 percent?

An image often helps me translate a problem into mathematics. Imagine everyone in the room greeting all the others by shaking hands, one handshake at a time, and checking for a shared birthday with each handshake.

How many handshakes happen?

Each person shakes hands with 𝑛 − 1 others, making 𝑛(𝑛 − 1) arrows from one person to another. But a handshake is shared between two people. To avoid counting each handshake twice, we need to divide 𝑛(𝑛−1) by 2. Thus, there are 𝑛(𝑛 − 1)/2 or roughly 𝑛2/2 handshakes.

With 365 possible birthdays, the probability, per handshake, of a shared birthday is 1/365. With 𝑛2/2 handshakes, the probability that no handshake joins two people with a shared birthday is approximately 𝑛2/2

(1 − 1

365)

.

(4.57)

To approximate this probability, take its natural logarithm: 𝑛2/2

ln (1 − 1

365)

= 𝑛22 ln(1 − 1365).

(4.58)

Then approximate the logarithm using ln(1 + 𝑥) ≈ 𝑥 (for 𝑥 ≪ 1): ln (1 − 1

365) ≈ − 1

365.

(4.59)

(You can test this useful approximation using a calculator, or see the picto-rial explanation in Street-Fighting Mathematics [33, Section 4.3].) With that approximation,

ln (probability of no shared birthday) ≈ −𝑛22 × 1365.

(4.60)

When the probability of no shared birthday falls below 0.5, the probability of a shared birthday rises above 0.5. Therefore, the condition for having enough people is

ln (probability of no shared birthday) < ln 12.

(4.61)

Because ln(1/2) = − ln 2, the condition simplifies to 𝑛2

2 × 365 > ln 2.

(4.62)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.4 Scaling exponents in mathematics 125

Using the approximation ln 2 ≈ 0.7, the threshold 𝑛 is approximately 22.6: 𝑛 > ln 2 × 2 × 365 ≈ 22.6.

(4.63)

People do not come in fractions, so we need 23 people. Indeed, the exact calculation for 𝑛 = 23 gives the probability of sharing a birthday as 0.507!

From this scaling analysis, we can compactly explain what went wrong with the plausible conjecture. It assumed that the shared-birthday probability 𝑝 is proportional to the number of people 𝑛, reaching 𝑝 = 0.5 when 𝑛 = 0.5 × 365. The handshake picture, however, shows that the probability is related to the number of handshakes, which is proportional to 𝑛2. What a difference from a simple change in a scaling exponent!

Problem 4.24

Three people sharing a birthday

Extend our scaling analysis to the three-birthday problem: How many people must be in a room before the probability of three people sharing a birthday rises above 0.5? (The results of the exact calculation, along with many approximations, are given by Diaconis and Mosteller [10].)

Problem 4.25

Scaling of bubble sort

The simplest algorithm for sorting—for example, to sort a list of 𝑛 web pages according to relevance—is bubble sort. You go through the list in passes, comparing neighboring items and swapping any that are out of order.

a. How many passes through the list do you need in order to guarantee that the list is sorted?

b. The running time 𝑡 (the time to sort the list) is proportional to the number of comparisons. What is the scaling exponent 𝛽 in 𝑡 ∝ 𝑛𝛽?

Problem 4.26

Scaling of merge sort

Bubble sort (Problem 4.25) is easy to describe, but there is an alternative that is almost as easy: merge sort. It is a recursive, divide-and-conquer algorithm. You divide the list of 𝑛 items into two equal parts (assume that 𝑛 is a power of 2), and sort each half using merge sort. To make the sorted list, just merge the two sorted halves.

a. Here is a list of eight randomly generated numbers: 98, 33, 34, 62, 31, 58, 61, and 15. Draw a tree illustrating how merge sort works on this list. Use two lines for each internal node, showing on one line the original list and on the second line the sorted list.

b. The running time 𝑡 is proportional to the number of comparison operations.

What are the scaling exponents 𝛼 and 𝛽 in

𝑡 ∝ 𝑛𝛼(log 𝑛)𝛽?

(4.64)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

126

4 Proportional reasoning

c. If you were a revenue agency and had to sort the tax records of all residents in a country, which algorithm would you use, merge sort or bubble sort?

Problem 4.27

Scaling of standard multiplication

In the usual school algorithm for multiplying 𝑛 digit numbers, you find and add partial products. If the running time 𝑡 is proportional to the number of single-digit multiplications, what is the scaling exponent 𝛽 in 𝑡 ∝ 𝑛𝛽?

Problem 4.28

Scaling of Karatsuba multiplication

The Karatsuba algorithm for multiplying two 𝑛-digit numbers, discovered by Anatoly Karatsuba in 1960 [28] and published in 1962 [29], was the first development in the theory of multiplication in centuries. Similarly to merge sort, you first break each number into two equal-length halves. For example, you split 2743 into 27

and 43. Using Karatsuba multiplication recursively, you form three products from those halves, and combine the three products to get the original product. The subdividing stops when the numbers are short enough to be multiplied by the computer's hardware (typically, at 32 or 64 bits).

The expensive step, repeated many times, is hardware multiplication, so the running time 𝑡 is proportional to the number of hardware multiplications. Find the scaling exponent 𝛽 in 𝑡 ∝ 𝑛𝛽. (You will find a scaling exponent that occurs rarely in physical scalings, namely an irrational number.) How does this 𝛽 compare with the exponent in the school algorithm for multiplication (Problem 4.27)?

4.5 Logarithmic scales in two dimensions

Scaling relations, which are so helpful in understanding the physical and mathematical worlds, have a natural representation on logarithmic scales, the representation that we introduced in Section 3.1.3 whereby distances correspond to factors or ratios rather than to differences.

As an example, here is the gravitational strength 𝑔 at a gearth distance 𝑟 from the center of a planet. Outside the planet, 𝑔 ∝ 𝑟−2 (the inverse-square law of gravitation). On linear axes, the graph of 𝑔 versus 𝑟 looks curved, like a hy-g ∝ r−2

g

perbola. However, its exact shape is hard to identify; the earth

4

graph does not make the relation between 𝑔 and 𝑟 obvious. For example, let's try to represent our favorite scal-Rearth 2Rearth

ing analysis: When 𝑟 doubles, from, say, 𝑅Earth to 2𝑅Earth, the gravitational acceleration falls from 𝑔Earth to 𝑔Earth/4. The graph shows that 𝑔(2𝑅) is smaller than 𝑔(𝑅); unfortunately, the scaling is hard to extract from these points or from the curve.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.5 Logarithmic scales in two dimensions 127

gearth

However, using logarithmic scales for both 𝑔 and 𝑟—called log–log axes—makes the relation clear. Let's try again to slope = −2

represent that when 𝑟 doubles, the gravitational accelera-g ∝ r−2

tion falls by a factor of 4. Call 1 unit on either logarithmic units2

scale a factor of 2. The factor of 2 increase in 𝑟 corresponds to moving 1 unit to the right. The factor of 4 decrease in 𝑔 gearth corresponds to moving 2 units downward. Therefore, the 4

graph of 𝑔 versus 𝑟 is a straight line—and its slope is −2.

1 unit

On logarithmic scales, scaling relations turn into straight Rearth

2Rearth

lines whose slope is the scaling exponent.

Problem 4.29

Sketching gravitational field strength

Imagine, as in Problem 4.13, a uniform spherical planet with radius 𝑅. Sketch, on log–log axes, gravitational field strength 𝑔 versus 𝑟, the distance from the center of the planet. Include the regions 𝑟 < 𝑅 and 𝑟 ≥ 𝑅.

Many natural processes, often for unclear reasons, obey word rank frequency scaling relations. A classic example is Zipf's law. In its simplest form, it states that the frequency of the 𝑘th most the 1

7.0%

common word in a language is proportional to 1/𝑘. The of 2

3.5

table gives the frequencies of the three most frequent Eng- and 3

2.9

lish words. For English, Zipf's law holds reasonably well up to 𝑘 ∼ 1000.

Zipf's law is useful for estimation. For example, suppose that you have to estimate the government budget of Delaware, one of the smallest US states (Problem 4.30). A key step in the estimate is the population. Delaware might be the smallest state, at least in area, and it is probably nearly the smallest in population. To use Zipf's law, we need the data for the most populous state. That information I happen to remember (information about the biggest item is usually easier to remember than information about the smallest item): The most populous state is California, with roughly 40 million people. Because the United States has 50 states, Zipf's law predicts that the smallest state will have a population 1/50th of California's, or roughly 1 million. This estimate is very close to Delaware's actual population: 917 000.

Problem 4.30

Government budget of Delaware

Based on the population of Delaware, estimate its annual government budget. Then look up the value and check your estimate.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

128

4 Proportional reasoning

4.6 Optimizing flight speed

With our skills in proportional reasoning, let's return to the energy and power consumption in forward flight (Section 3.6.2). In that analysis, we took the flight speed as a given; based on the speed, we estimated the power required to generate lift. Now we can estimate the flight speed itself. We will do so by estimating the speed that minimizes energy consumption.

4.6.1 Finding the optimum speed

Flying requires generating lift and fighting drag. To wing

find the optimum flight speed, we need to estimate the energy required by each process. The lift was the body

L

v

subject of Section 3.6.2, where we estimated the power required as

wing

𝑃lift ∼ (𝑚𝑔)2

𝜌air𝑣𝐿2 ,

(4.65)

where 𝑚 is the plane's mass, 𝑣 is its forward velocity, and 𝐿 is its wingspan.

The lift energy required to fly a distance 𝑑 is this power multiplied by the travel time 𝑑/𝑣:

𝐸

𝑑

lift = 𝑃lift 𝑣 ∼ (𝑚𝑔)2

𝜌air𝑣2𝐿2 𝑑.

(4.66)

In fighting drag, the energy consumed is the drag force times the distance.

The drag force is

𝐹drag = 12𝑐d𝜌air𝑣2𝐴cs,

(4.67)

where 𝑐d is the drag coefficient. To simplify comparing the energies required for lift and drag, let's write the drag force as 𝐹drag = 𝐶𝜌air𝑣2𝐿2,

(4.68)

where 𝐶 is a modified drag coefficient: It doesn't use the 1/2 that is part of the usual combination 𝑐d/2, and it is measured relative to the squared wingspan 𝐿2 rather than to the cross-sectional area 𝐴cs.

For a 747, which drag coefficient, 𝑐 d or 𝐶 , is smaller?

The drag force has two equivalent forms:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.6 Optimizing flight speed 129

⎧ 𝐶𝐿2

𝐹

{

drag = 𝜌air𝑣2 × ⎨

(4.69)

{ 1

⎩ 2𝑐d𝐴cs.

Thus, 𝐶𝐿2 = 𝑐d𝐴cs/2. For a plane, the squared wingspan 𝐿2 is much larger than the cross-sectional area, so 𝐶 is much smaller than 𝑐d.

With the new form for 𝐹drag, the drag energy is slope

𝐸drag = 𝐶𝜌air𝑣2𝐿2𝑑,

(4.70)

=

−2

and the total energy required for flying is

Edrag ∝ v2

𝐸total ∼ (𝑚𝑔)2

+ 𝐶𝜌

(4.71)

𝜌

air𝑣2𝐿2𝑑.

air 𝑣2𝐿2 𝑑

⏟⏟⏟⏟⏟ ⏟⏟⏟⏟⏟⏟⏟

𝐸lift

𝐸drag

2

Elift ∝ v−2

+

=

This formula looks intimidating because of the many parameters such as 𝑚, 𝑔, 𝐿, and 𝜌air. As our interest is the flight slope

speed 𝑣 (in order to find the total energy), let's use propor-vspecial

tional reasoning to reduce the energies to their essentials: 𝐸drag ∝ 𝑣2 and 𝐸lift ∝ 𝑣−2. On log–log axes, each relation is a straight line with slope +2 for drag and slope −2 for lift. Because the relations have different slopes, corresponding to different scaling exponents, their graphs must intersect.

To interpret the intersection, let's incorporate a sketch of the slope

total energy 𝐸total = 𝐸drag+𝐸lift. At low speeds, the dominant

=

E

consumer of energy is lift because of its

total

𝑣−2 dependence, so

−

the sketch of

2

𝐸

E

total follows 𝐸lift. At high speeds, the dominant drag ∝ v2

consumer of energy is drag because of its 𝑣2 dependence, so the sketch of 𝐸total follows 𝐸drag. Between these extremes is an optimum speed that minimizes the energy consumption.

2

(Because the axes are logarithmic, and

E

log(𝑎 + 𝑏) ≠ log 𝑎 +

lift ∝ v−2

+

=

log 𝑏, the sum of the two straight lines is not straight!) This optimum speed, marked 𝑣special, is the speed at which 𝐸drag slope

and 𝐸lift cross.

vspecial

Why is the optimum right at the crossing speed, rather than faster or slower than the crossing speed?

Symmetry! Try Problem 4.31 and then look afresh at Section 3.2.3, where we minimized 𝐸total without the benefit of log–log axes.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

130

4 Proportional reasoning

Flying faster or slower than the optimum speed means consuming more energy. That extra consumption cannot always be avoided. A plane is designed so that its cruising speed is its minimum-energy speed. At takeoff and landing, when it flies far below the minimum-energy speed, a plane must work harder to stay aloft, which is one reason that the engines are so loud at takeoff and landing (another reason is that the engine noise reflects off the ground and back to the plane).

The optimization constraint, that a plane flies at the minimum-energy speed, allows us to eliminate 𝑣 from the total energy. As we saw on the graph, at the minimum-energy speed, the drag and lift energies are equal: (𝑚𝑔)2

∼ 𝐶𝜌

(4.72)

𝜌

air𝑣2𝐿2𝑑,

air𝑣2𝐿2 𝑑

⏟⏟⏟⏟⏟ ⏟⏟⏟⏟⏟⏟⏟

𝐸lift

𝐸drag

or, solving for 𝑚𝑔 (and rejoicing that 𝑑 canceled out), 𝑚𝑔 ∼ 𝐶 𝜌air𝑣2𝐿2.

(4.73)

Now we could solve for 𝑣 explicitly (and you get to find and use that solution in Problems 4.34 and 4.36). However, here we are interested in the total energy, not the flight speed itself. To find the energy without finding the speed, notice a reusable idea, an abstraction, within the right side of the equation for 𝑚𝑔—which otherwise looks like a mess.

Namely, the mess contains 𝜌air𝑣2𝐿2, which is 𝐹drag/𝐶. Therefore, when the plane is flying at the minimum-energy speed, 𝐹

𝑚𝑔 ∼ 𝐶 drag

𝐶 ,

(4.74)

so

𝐹drag ∼ 𝐶 𝑚𝑔.

(4.75)

Thanks to our abstraction and all the surrounding approximations, we learn a surprisingly simple relation between the drag force and the plane's weight, connected through the square root of our modified drag coefficient 𝐶.

The energy consumed by drag—which, within a factor of 2, is also the total energy—is the drag force times the distance 𝑑. Therefore, the total energy is given by

𝐸total ∼ 𝐸drag

⏟ ∼ 𝐶 𝑚𝑔𝑑.

(4.76)

𝐹drag𝑑

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.6 Optimizing flight speed 131

By using an optimum flight speed, we have eliminated the flight speed 𝑣

from the total energy.

Does the total energy depend in reasonable ways upon 𝑚 , 𝑔 , 𝐶 , and 𝑑 ?

Yes! First, lift overcomes the weight 𝑚𝑔; therefore, the energy should, and does, increase with 𝑚𝑔. Second, a streamlined plane (low 𝐶) should use less energy than a bluff, blocky plane (high 𝐶); the energy should, and does, increase with the modified drag coefficient 𝐶. Finally, because the plane is flying at a constant speed, the energy should be, and is, proportional to the travel distance 𝑑.

4.6.2 Flight range

From the total energy, we can estimate the range of the 747—the distance that it can fly on a full tank of fuel. The energy is 𝐶 𝑚𝑔𝑑, so the range 𝑑 is 𝑑 ∼ 𝐸fuel ,

(4.77)

𝐶 𝑚𝑔

where 𝐸fuel is the energy in the full tank of fuel. To estimate 𝑑, we need to estimate 𝐸fuel, the modified drag coefficient 𝐶, and maybe also the plane's mass 𝑚.

How much energy is in a full tank of fuel?

The fuel energy is the fuel mass times its energy density (as an energy per mass). Let's describe the fuel mass relative to the plane's mass 𝑚, as a fraction 𝛽 of the plane's mass: 𝑚fuel = 𝛽𝑚. Using ℰfuel for the energy density of fuel,

𝐸fuel = 𝛽𝑚ℰfuel.

(4.78)

When we put this expression into the range 𝑑, the plane's mass 𝑚 in 𝐸fuel, which is the numerator of 𝑑, cancels the 𝑚 in the denominator 𝐶 𝑚𝑔. The range then simplifies to a relation independent of mass: 𝑑 ∼ 𝛽ℰfuel .

(4.79)

𝐶 𝑔

For the fuel fraction 𝛽, a reasonable guess for long-range flight is 𝛽 ≈ 0.4: a large portion of the payload is fuel. For the energy density ℰfuel, we learned in Section 2.1 that ℰfuel is roughly 4×107 joules per kilogram (9 kilocalories per gram). This energy density is what a perfect engine would extract. At 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

132

4 Proportional reasoning

the usual engine efficiency of one-fourth, ℰfuel becomes roughly 107 joules per kilogram.

How do we find the modified drag coefficient 𝐶 ?

This estimate is the trickiest part of the range estimate, because 𝐶 needs to be converted from more readily available data. According to Boeing, the manufacturer of the 747, a 747 has a drag coefficient of 𝐶′ ≈ 0.022. As the prime symbol indicates, 𝐶′ is yet another drag coefficient. It is measured using the wing area 𝐴wing and uses the traditional 1/2: 𝐹drag = 12𝐶′𝐴wing𝜌air𝑣2.

(4.80)

So we have three drag coefficients, depending on whether the coefficient is referenced to the cross-sectional area 𝐴cs (the usual definition of 𝑐d), to the wing area 𝐴wing (Boeing's definition of 𝐶′), or to the squared wingspan 𝐿2

(our definition of 𝐶, which also lacks the factor of 1/2 that the others have).

To convert between these definitions, compare the three ways to express the drag force:

⎧{ 1

{{ 2𝐶′𝐴wing (Boeing's definition),

𝐹drag = 𝜌air𝑣2 × ⎨𝐶𝐿2

(our definition),

(4.81)

{{{ 1

⎩ 2𝑐d𝐴cs

(the usual definition).

From this comparison,

12𝐶′𝐴wing = 𝐶𝐿2 = 12𝑐d𝐴cs.

(4.82)

The conversion from 𝐶′ to 𝐶 is therefore

𝐴

𝐶 = 1

wing

2𝐶′ 𝐿2 .

(4.83)

l

Using 𝑙 for the wing's front-to-back length, the wing area becomes 𝐴wing = 𝐿𝑙. Then the area ratio 𝐴wing/𝐿2

wing

simplifies to 𝑙/𝐿 (the reciprocal of the wing aspect ratio), and the drag coefficient 𝐶 simplifies to body

L

v

𝐶 = 1

wing

2𝐶′ 𝑙𝐿.

(4.84)

For a 747, 𝑙 ≈ 10 meters, 𝐿 ≈ 60 meters, and 𝐶′ ≈ 0.022, so 𝐶 ≈ 1/600:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.6 Optimizing flight speed 133

𝐶 ∼ 12 × 0.022 × 10m

60 m ≈ 1

600.

(4.85)

The resulting range is roughly 10 000 kilometers: 𝛽

ℰfuel

⏞⏞⏞⏞⏞

𝑑 ∼

0.4

⏞ × 107 Jkg−1 ≈107m=104km.

(4.86)

1/600

⏟⏟⏟⏟⏟ × 10 m s−2

⏟⏟⏟⏟⏟

𝐶

𝑔

The actual maximum range of a 747-400 is 13 450 kilometers (a figure we used in Section 4.3.2): Our approximate analysis is amazingly accurate.

Problem 4.31

Graphical interpretation of minimization using symmetry In Section 3.2.3, we started with the general form for the total energy 𝐸 ∼ 𝐴 + 𝐵𝑣2

𝑣2

(4.87)

⏟ ⏟

𝐸lift

𝐸drag

and found the optimum (minimum-energy) speed by constructing the following symmetry operation:

𝑣 ⟷ 𝐴/𝐵

𝑣 .

(4.88)

On the log–log plot of the energies versus 𝑣, what is the geometric interpretation of this symmetry operation?

Problem 4.32

Minimum-power speed

We estimated the flight speed 𝑣E that minimizes energy consumption. We could also have estimated 𝑣P, the speed that minimizes power consumption. What is the ratio 𝑣P/𝑣E? Before doing an exact calculation, sketch 𝑃lift, 𝑃drag, and 𝑃lift + 𝑃drag (on log–log axes) and place 𝑣P on the correct side of 𝑣E. Then check your placement against the result of the exact calculation.

Problem 4.33

Coefficient of lift

Just as we can define a dimensionless drag coefficient 𝑐d, where 𝐹drag = 12𝑐d𝜌air𝐴𝑣2,

(4.89)

we can define a dimensionless lift coefficient 𝑐L, where 𝐹lift = 12𝑐L𝜌air𝐴𝑣2,

(4.90)

where the area 𝐴 here is usually the wing area. (The same formula structure shows up in drag and lift—abstraction!) Estimate 𝑐L for a 747 in cruising flight.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

134

4 Proportional reasoning

4.6.3 Flight range versus size

In proportional reasoning, we ask,「How does one quantity change when we change an independent variable (for example, if we double an independent variable)?」Because flying objects come in such a wide range of sizes, a natural independent variable is size.

How does the flight range depend on the plane's size?

Let's assume that all planes are geometrically similar—that is, that they have the same shape and differ only in their size. Now let's see how changing the plane's size changes the quantities in the range 𝑑 ∼ 𝛽ℰfuel .

(4.91)

𝐶 𝑔

The gravitational acceleration 𝑔 remains fixed. The fuel energy density ℰfuel and the fuel fraction 𝛽 also remain fixed—which shows again the benefit of using intensive quantities, as we discussed in Section 4.2.4 when we made a scaling relation for planetary surface gravity. Finally, the drag coefficient 𝐶 depends only on the plane's shape (on how streamlined it is), not on its size, so it too remains constant. Therefore, the flight range is independent of the plane's size!

A further surprise comes from comparing the range of planes with the range of migrating birds. The proportionality 𝑑 ∝ 𝛽ℰfuel⁄ 𝐶 is shorthand for the comparison

𝑑

−1/2

plane

𝛽plane ℰfuel

plane

𝐶plane

𝑑

=

(

)

.

(4.92)

bird

𝛽bird ℰfuel

𝐶

bird

bird

The ratio of fuel fractions is roughly 1: For the plane, 𝛽 ≈ 0.4; and a bird, having eaten all summer, is perhaps 40 percent fat (the bird's fuel). The energy density in jet fuel and fat is similar, as is the efficiency of engines and animal metabolism (at about 25 percent). Therefore, the ratio of energy densities is also roughly 1. Finally, a bird has a similar shape to a plane, so the ratio of drag coefficients is also roughly 1. Therefore, planes and well-fattened migrating birds should have a similar maximum range, about 10 000 kilometers.

Let's check. The longest known nonstop flight by an animal is 11 680 kilometers: made by a bar-tailed godwit tracked by satellite by Robert Gill and his colleagues [19] as the bird flew nonstop from Alaska to New Zealand!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4.7 Summary and further problems 135

4.7 Summary and further problems

Proportional reasoning focuses our attention on how one quantity determines another. (A wonderful collection of pointers to further reading is the American Journal of Physics's「Resource Letter」on scaling laws [49].) By guiding us toward what is often the most important characteristic of a problem, the scaling exponent, it helps us discard spurious complexity.

Problem 4.34

Cruising speed versus mass

For geometrically similar animals (the same shape and composition but different sizes) in forward flight, how does the animal's minimum-energy flight speed 𝑣

depend on its mass 𝑚? In other words, what is the scaling exponent 𝛽 in 𝑣 ∝ 𝑚𝛽?

Problem 4.35

Hovering power versus size

In Section 3.6.1, we derived the power required to hover. For geometrically similar birds, how does the power per mass depend on the animal's size 𝐿? In other words, what is the scaling exponent 𝛾 in 𝑃hover/𝑚 ∝ 𝐿𝛾? Why are there no large hummingbirds?

Problem 4.36

Cruising speed versus air density

How does a plane's (or a bird's) minimum-energy speed 𝑣 depend on 𝜌air? In other words, what is the scaling exponent 𝛾 in 𝑣 ∝ 𝜌𝛾air?

Problem 4.37

Speed of a bar-tailed godwit

Use the results of Problem 4.34 and Problem 4.36 to write the ratio 𝑣747/𝑣godwit as a product of dimensionless factors, where 𝑣747 is the minimum-energy (cruising) speed of a 747, and 𝑣godwit is the minimum-energy (cruising) speed of a bar-tailed godwit. Using 𝑚godwit ≈ 400 grams, estimate the cruising speed of a bar-tailed godwit. Compare your result to the average speed of the record-setting bar-tailed godwit that was studied by Robert Gill and his colleagues [19], which made its 11 680-kilometer journey in 8.1 days.

Problem 4.38

Thermal resistance of a house versus a tea mug When we developed the analogy between low-pass electrical and thermal filters (Section 2.4.5)—whether 𝑅𝐶 circuits, tea mugs, or houses—we introduced the abstraction of thermal resistance 𝑅thermal. In this problem, you estimate the ratio of thermal resistances 𝑅house

thermal⁄𝑅tea mug

thermal .

House walls are thicker than teacup walls. Because thermal resistance, like electrical resistance, is proportional to the length of the resistor, the house's thicker walls raise its thermal resistance. However, the house's larger surface area, like having many resistors in parallel, lowers the house's thermal resistance. Estimate the size of these two effects and thus the ratio of the two thermal resistances.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

136

4 Proportional reasoning

Problem 4.39

General birthday problem

Extend the analysis of Problem 4.24 to 𝑘 people sharing a birthday. Then compare your predictions to the exact results given by Diaconis and Mosteller in [10].

Problem 4.40

Flight of the housefly

Estimate the mechanical power required for a common housefly Musca domestica (𝑚 ≈ 12 milligrams) to hover. From everyday experience, estimate its typical flight speed. At this flight speed, compare the power requirements for forward flight and for hovering.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

5Dimensions

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

