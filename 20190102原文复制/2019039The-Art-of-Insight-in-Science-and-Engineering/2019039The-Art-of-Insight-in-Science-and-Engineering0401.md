## 0401. Proportional reasoning

4.1 Population scaling

4.2 Finding scaling exponents

4.3 Scaling exponents in fluid mechanics

4.4 Scaling exponents in mathematics

4.5 Logarithmic scales in two dimensions

4.6 Optimizing flight speed

4.7 Summary and further problems

When there is change, look for what does not change. That principle, introduced when we studied symmetry and conservation (Chapter 3), is also the basis for our next tool, proportional reasoning.

0401 正比分析

每当有变化发生，就去寻找不变量。这个在研究对称性和守恒（第 3 章）时引进的原则，也是我们下一个工具的基础，即正比分析。

### 4.1 Population scaling

An everyday example of proportional reasoning often happens when cooking for a dinner party. When I prepare fish curry, which I normally cook for our family of four, I buy 250 grams of fish. But today another family of four will join us.

How much fish do I need?

I need 500 grams. As a general relation,

new amount = old amount × new number of diners usual number of diners. (4.1)

Another way to state this relation is that the amount of fish is proportional to the number of diners. In symbols,

𝑚fish ∝ 𝑁diners, (4.2)

where the ∝ symbol is read「is proportional to.」

But where in this analysis is the quantity that does not change?

Another way to write the proportionality relation is new amount of fish

new number of diners = old amount of fish / old number of diners. (4.3)

Thus, even when the number of diners changes, the quotient 

amount of fish / number of diners (4.4)

does not change.

For an analogous application of proportional reasoning, here's one way to estimate the number of gas stations in the United States. Following the principle of using human-sized numbers, which we discussed in Section 1.4, I did not try to estimate this large number directly. Instead, I started with my small hometown of Summit, New Jersey. It had maybe 20 000 people and maybe five gas stations; the「maybe」indicates that these childhood memories may easily be a factor of 2 too small or too large. If the number of gas stations is proportional to the population (𝑁stations ∝ 𝑁people), then 

(4.5)

The population ratio is roughly 15 000. Therefore, if Summit has five gas stations, the United States should have 75 000. We can check this estimate.

The US Census Bureau has an article (from 2008) entitled「A Gas Station for Every 2,500 People」; its title already indicates that an estimate of roughly 105 gas stations is reasonably accurate: Summit, in my reckoning, had 4000

people per gas station. Indeed, the article gives the total as 116 855 gas stations — as close to the estimate as we can expect given the uncertainties in childhood memories!

Problem 4.1 Homicide rates

The US homicide rate (in 2011) was roughly 14 000 per year. The UK rate in the same year was roughly 640. Which is the more dangerous country (per person), and by what factor?

4.1 人口标度

日常生活中一个正比分析的例子常常出现在准备晚宴的时候。我做咖喱鱼的时候，通常是给我们自己的四口之家准备的，我会买 250 克的鱼。但今天另一个四口之家会加入我们。

我需要购买多少鱼？

新的鱼数由下式给出：

新的鱼数=原来的鱼数×（新的就餐者数/原来的就餐者数） —  —  (4.1)

另一个表示这个关系的方式是鱼的数量正比于就餐者的数量。用符号表示，即：

(4.2)

其中符号 ∝ 读作「正比于」。

1『因为打不出正比于的符号，先用 oc 代替。（2022-06-03）』

➤ 但在分析中，哪个量是不变的？

比例关系可以写成另一种形式：

新的鱼数/原来的鱼数 = 新的就餐者数/原来的就餐者数 (4.3)
 
于是，即使就餐者的数量在变化，但比例：

(4.4)

是不变的。

作为正比分析的一个类似的应用，下面给出估算美国加油站数量的一种方式。根据我们曾在章节 1.4 中讨论过的使用与人体相关的数量的原则，我不打算直接估算这个大数。而是从我的小镇，新泽西的萨米特镇开始。小镇也许有 20000 居民，可能有 5 个加油站；这里「也许」意味着儿时的记忆很容易有比实际大 2 倍或小 2 倍的差异。如果加油站的数量正比于人口，则：

(4.5)

人口的比大约是 15000。因此，如果萨米特镇有 5 个加油站，全美国就应该有 75000 个加油站。我们可以来验证这个结果。按照美国人口普查局的统计（2008 年）「每 2500 人有一个加油站」；这已经告诉我们 10^5 个加油站的粗略估算结果达到了合理的精度：我推算的萨米特镇是每 4000 人一个加油站。的确，人口普查局统计给出的总数是 116885 个加油站  —  —  考虑到儿时的估算不确定性，已经非常接近于我们所能期待的估算结果！

题 4.1 凶杀案发率

美国的凶杀案发率（2011 年）大约是每年 14000 件。英国同时期的案发率大约是 640 件。哪个国家是更危险的国家（对每个人），相差多大的因子？

### 4.2 Finding scaling exponents

The dinner example (Section 4.1) used linear proportionality: When the number of dinner guests doubled, so did the amount of food. The relation between the quantities had the form 𝑦 ∝ 𝑥 or, more explicitly, 𝑦 ∝ 𝑥1. The exponent, which here is 1, is called the scaling exponent. For that reason, proportionalities are often called scaling relations. Scaling exponents are a powerful abstraction: Once you know the scaling exponent, you usually do not care about the mechanism underlying it.

#### 4.2.1 Warmup

After linear proportionality, the next simplest and most common type of proportionality is quadratic — a scaling exponent of 2 — and its close cousin, a scaling exponent of 1/2. As an example, here is a big circle with diameter 𝑑big = 5 cm.

What is the diameter of the circle with one-half the area of this circle?

Let's first do the very common brute-force solution, which does not use proportional reasoning, so that you see what not to do. It begins with the area of the big circle:

(4.6)

The area of the small circle 𝐴small is 𝐴big/2, so 𝐴small = 5𝜋/8 cm2.

Therefore, the diameter of the small circle is given by 

(4.7)

Although this result is correct, by including 𝜋/4 and then dividing it out, we run around Robin Hood's barn (all of Sherwood forest) to reach a simple result. There must be a more elegant and insightful approach.

This improved approach also starts with the relation between a circle's area and its diameter: 𝐴 = 𝜋𝑑2/4. However, it discards the complexity early — in the next step — rather than carrying it through the analysis and having it vanish only at the end. An everyday analog of this approach is packing for a trip. Rather than dragging around books that you will not read or clothes that you will not wear, prune early and travel light: Pack only what you will use and set aside the rest.

To lighten your problem-solving luggage, observe that all circles, independent of their diameter, have the same prefactor 𝜋/4 connecting 𝑑2 and 𝐴.

Therefore, when we make a proportionality or scaling relation between 𝐴 and 𝑑, we discard the prefactor. The result is the following quadratic proportionality (one where the scaling exponent is 2): 

𝐴 ∝ 𝑑2. (4.8)

For finding the new diameter, we need the inverse scaling relation: 

𝑑 ∝ 𝐴1/2. (4.9)

In this form, the scaling exponent is 1/2. This proportionality is shorthand for the ratio relation

(4.10)

The area ratio is 1/2, so the diameter ratio is 1/ 2. Because the large diameter is 5 cm, the small diameter is √5/2 cm.

The proportional-reasoning solution is shorter than the brute-force approach, so it offers fewer places to go wrong. It is also more general: It shows that the result does not require that the shape be a circle. As long as the area of the shape is proportional to the square of its size (as a length) — a relation that holds for all planar shapes — the length ratio is 1/ 2 whenever the area ratio is 1/2. All that matters is the scaling exponent.

Problem 4.2 Length of the horizontal bisecting path

In Problem 3.23, about the shortest path that bisects an equilateral triangle, one candidate path is a horizontal line. How long is that line relative to a side of the triangle?

Areas are connected to flux, because flux is rate per area. Thus, the scaling exponent for area — namely, 2 — appears in flux relationships. For example: What is the solar flux at Pluto's orbit?

The solar flux 𝐹 at a distance 𝑟 from the Sun is the solar luminosity 𝐿Sun — the radiant power output of the sun — spread over a sphere with radius 𝑟: 

𝐹 = 𝐿Sun/4𝜋𝑟2 (4.11)

Even as 𝑟 changes, the solar luminosity remains the same (conservation!), as does the factor of 4𝜋. Therefore, in the spirit of packing light for a trip, simplify the equality 𝐹 = 𝐿Sun/4𝜋𝑟2 to the proportionality 

𝐹 ∝ 𝑟−2 (4.12)

by discarding the factors 𝐿Sun and 4𝜋. The scaling exponent here is −2: The minus sign indicates the inverse proportionality between flux and area, and the 2 is the scaling exponent connecting 𝑟 to area.

The scaling relation is shorthand for

(4.13)

or

(4.14)

Earth's orbit

The ratio of orbital radii is roughly 40. Therefore, the solar flux at Pluto's orbit is roughly 40−2 or 1/1600 of the flux at the Earth's orbit. The resulting flux is roughly 0.8 watts per square meter:

(4.15)

Receiving such a small amount of sunlight, Pluto must be very cold. We can estimate its surface temperature with a further proportionality.

Surface temperature depends mostly on so-called blackbody radiation. The surface temperature is the temperature at which the radiated flux equals the incoming flux; we are making another box model. The radiated flux is given by the blackbody formula (which we will derive in Section 5.5.2)

𝐹 = 𝜎𝑇4, (4.16)

where 𝑇 is the temperature, and 𝜎 is the Stefan–Boltzmann constant: 

𝜎 ≈ 5.7 ×10−8 W (4.17)

What is the resulting surface temperature on Pluto?

As with any proportional-reasoning calculation, there is a long-winded, brute-force alternative (try Problem 4.5). The elegant approach directly uses the proportionalities

𝑇 ∝ 𝐹1/4 and 𝐹 ∝ 𝑟−2, (4.18)

where 𝑟 is the orbital radius. Together, they produce a new proportionality 

𝑇 ∝ (𝑟−2)1/4 = 𝑟−1/2. (4.19)

A compact graphical notation, similar to the divide-and-conquer trees, encapsulates this derivation:

As indicated by the 𝑟 → 𝐹 arrow, changing 𝑟 changes 𝐹. The boxed number along the arrow gives the scaling exponent. Therefore, the 𝑟 → 𝐹 arrow represents 𝐹 ∝ 𝑟−2. The 𝐹 → 𝑇 arrow indicates that changing 𝐹 changes 𝑇 and, in particular, that 𝑇 ∝ 𝐹1/4.

To find the scaling exponent connecting 𝑟 to 𝑇, multiply the scaling exponents along the path:

−2 × 14 = −12. (4.20)

Problem 4.3 Explaining the graphical notation

In our graphical representation of scaling relations, why is the final scaling exponent the product, rather than the sum, of the scaling exponents along the way?

This scaling exponent represents the following comparison: 

(4.21)

(The rightmost form, with the positive exponent, is more direct than the intermediate form, because it does not first produce a fraction smaller than 1 and then take its reciprocal with a negative exponent.) The ratio of orbital radii is 40, so the ratio of surface temperatures should be 40 or roughly 6.

Pluto's surface temperature should be roughly 50 K: 

(4.22)

Pluto's actual mean surface temperature is 44 K, very close to our prediction based on proportional reasoning.

Problem 4.4 Explaining the discrepancy

Why is our prediction for Pluto's mean temperature slightly too high?

Problem 4.5 Brute-force calculation of surface temperature 

To practice recognizing common but inferior problem-solving methods, use the brute-force method to estimate the surface temperature on Pluto: (a) From the solar flux at Pluto's orbit, calculate the solar flux averaged over the surface; (b) use that flux to estimate a blackbody temperature.

#### 4.2.2 Orbital periods

In the preceding examples, the scaling relations formed chains (trees without branching):

food for a dinner party : 

(4.23)

More elaborate relationships also occur — as we will find in rederiving a famous law of planetary motion.

How does a planet's orbital period depend on its orbital radius 𝑟 ?

We'll study the special case of circular orbits (many planetary orbits are close to circular). Our exploratory thinking is often aided by making proportionality questions concrete. Therefore, rather than finding the scaling exponent using the abstract notion of「depend on,」answer the doubling question:「When I double this quantity, what happens to that quantity?」

What is so special about doubling?

Doubling — multiplying by a factor of 2 — is the simplest useful change. A factor of 1 is simpler; however, being no change at all, it is too simple.

What happens to the period if we double the orbital radius?

The most direct effect of doubling the orbital radius is that gravity gets weaker. Because the gravitational force is an inverse-square force — that is, 𝐹 ∝ 𝑟−2 — the gravitational force falls by a factor of 4. A compact and intuitive notation for these changes is to mark the change directly under the quantity: A notation of ×𝑛 indicates multiplication by a factor of 𝑛.

(4.24)

Because force is proportional to acceleration, the planet's acceleration 𝑎 falls by the same factor of 4.

In circular motion, acceleration and velocity are related by 𝑎 = 𝑣2/𝑟. (We will derive this relation in Section 5.1.1 and Section 6.3.4, with two different reasoning tools.) Therefore, the orbital velocity 𝑣 is 𝑎𝑟 , and doubling the radius increases the orbital speed by a factor of 1/2: 

(4.25)

Although this calculation is correct, when it is stated as a factor of 1/2

it confounds our expectations and produces numerical whiplash. As we finish reading「increases by a factor of,」we expect a number greater than 1.

But we get a number smaller than 1. An increase by a factor smaller than 1 is more simply described as a decrease. Therefore, it is more direct to say that the orbital speed falls by a factor of 2.

The orbital period is 𝑇 ∼ 𝑟/𝑣 (the ∼ contains the dimensionless prefactor 2𝜋), so it increases by a factor of 23/2:

(4.26)

In summary, doubling the orbital radius multiplies the orbital period by 23/2. In general, the connection between 𝑟 and 𝑇  is 𝑇 ∝ 𝑟3/2.

(4.27)

This result is Kepler's third law for circular orbits. Our scaling analysis has the following graphical representation:

In this structure, the new feature is that two paths reach the orbital velocity 𝑣. There we add the incoming exponents.

1 r +1, v represents the 𝑟 in 𝑣 = 𝑎𝑟 . It carries +1/2 powers of 𝑟.

2 a +1, v represents the 𝑎 in 𝑣 = 𝑎𝑟 . To determine how many 2

powers of 𝑟 flow through this arrow, follow the chain containing it: 

One power of 𝑟 starts at the left side. It becomes −2 powers after passing through the first scaling exponent and arriving at 𝐹. It remains −2

powers on arrival at 𝑎. Finally, it becomes −1 power on arrival at 𝑣. This path therefore carries −1 power of 𝑟.

Its contribution is the result of multiplying the three scaling exponents along the chain:

(4.28)

The −1 power carried by the three-link chain, representing 𝑟−1, combines with the +1/2 from the direct 𝑟 → 𝑣 arrow, which represents 𝑟+1/2. Adding the exponents on 𝑟, the result is that 𝑣 contains −1/2 powers of 𝑟: 

(4.29)

Let's practice the same reasoning by finding the scaling relation connecting 𝑇 and 𝑟 — which is Kepler's third law. The direct 𝑟 → 𝑇 arrow, with a scaling exponent of +1, carries +1 powers of 𝑟. The 𝑣 → 𝑇 arrow carries −1 powers of 𝑣. Because 𝑣 contains −1/2 powers of 𝑟, the 𝑣 → 𝑇 arrow carries +1/2 powers of 𝑟:

(4.30)

Together, the two arrows contribute +3/2 powers of 𝑟 and give us Kepler's third law:

(4.31)

To summarize the exponent rules, for which we now have several illustra-tions: (1) Multiply exponents along a path, and (2) add exponents when paths meet.

Now let's apply Kepler's third law to a nearby planet.

How long is the Martian year?

The proportionality 𝑇 ∝ 𝑟3/2 is shorthand for the comparison 𝑇

(4.32)

where 𝑟Mars is the orbital radius of Mars, 𝑟ref is the orbital radius of a reference planet, and 𝑇ref is its orbital period. Because we are most familiar with the Earth, let's choose it as the reference planet. The reference period is 1 (Earth) year; and the reference radius is 1 astronomical unit (AU), which is 1.5×1011 meters. The benefit of this choice is that we will obtain the period of Mars's orbit in the familiar unit of Earth years.

The distance of Mars to the Sun varies between 2.07 × 1011 meters (1.38 astronomical units) and 2.49 × 1011 meters (1.67 astronomical units). Thus, the orbit of Mars is not very circular and has no single orbital radius 𝑟Mars.

(Its significant deviation from circularity allowed Kepler to conclude that planets move in ellipses.) As a proxy for 𝑟Mars, let's use the average of the minimum and maximum radii. It is 1.52 astronomical units, making the ratio of orbital periods approximately 1.88: 

(4.33)

Therefore, the Martian year is 1.88 Earth years long.

Problem 4.6 Brute-force calculation of the orbital period 

To emphasize the contrast between proportional reasoning and the brute-force approach, find the period of Mars's orbit using the brute-force approach by starting with Newton's law of gravitation and then finding the orbital velocity and circumference.

A surprising conclusion about orbits comes from our doubling question introduced on page 109.

What happens to the period of a planet if you double its mass?

Using a type of thought experiment due to Galileo, imagine two identical planets, orbiting one just behind the other along the same orbital path. They have the same period. Now tie them together. The rope does not change the period, so the double-mass planet has same period as each individual planet: The scaling exponent is zero (𝑇 ∝ 𝑚0)!

Problem 4.7 Pendulum period versus mass

How does the period of an ideal pendulum depend on the mass of the bob?

#### 4.2.3 Projectile range

In the previous examples, only one variable was independent; changing it changed all the others.

However, many problems contain multiple independent variables. An example is the range 𝑅 of R a rock launched at an angle 𝜃 with speed 𝑣. The traditional derivation uses calculus. You solve for the position of the rock as a function of time, solve for the time when its height is zero (the ground level), and then insert that time into the horizontal position to find the range.

This analysis is not wrong, but its result still seems like magic. I leave unsatisfied, thinking,「The result must be true. But I still do not know why.」

That「why」insight comes from proportional reasoning, which discards the nonessential complexity. Let's begin with our doubling question.

How does doubling each of the independent variables affect the range?

The independent variables include the launch velocity 𝑣, the gravitational acceleration 𝑔 (because gravity returns the rock to Earth), and the launch angle. However, angles do not fit so easily into proportional reasoning, so we won't explore the role of 𝜃 here (we will handle it in Section 8.2.2.1 using the tool of easy cases, or you can try Problem 4.9).

Because the only forces are vertical, the rock's horizontal velocity remains constant throughout its flight (an invariant!). Thus, the range is given by 𝑅 = time aloft × initial horizontal velocity.

(4.34)

The time aloft is determined by the initial vertical velocity, because gravity steadily reduces it (at the rate 𝑔):

(4.35)

Problem 4.8 Missing dimensionless prefactor

What is the missing dimensionless prefactor in the preceding expression for the time that the rock stays aloft?

Now double the launch velocity 𝑣. That change doubles the initial horizontal and vertical components of the velocity. Doubling the vertical component doubles the time aloft. Because the range is proportional to the horizontal velocity and to the time aloft, when the launch velocity doubles, the range quadruples. The scaling exponent connecting 𝑣 to 𝑅 is 2: 𝑅 ∝ 𝑣2.

What is the effect of doubling 𝑔 ?

Doubling 𝑔 doesn't change the horizontal velocity or the initial vertical velocity, but it halves the time aloft and therefore the range as well. The scaling exponent connecting 𝑔 to 𝑅 is −1: 𝑅 ∝ 𝑔−1.

The combined scaling relation, which gives the dependence of 𝑅 on both 𝑔 and 𝑣, is

𝑅 ∝ 𝑣2𝑔. (4.36)

Using 𝑣𝑥 and 𝑣𝑦 for the horizontal and vertical components of the launch velocity, the graphical representation of this reasoning is vx

This graph shows a new feature: two independent variables, 𝑣 and 𝑔. We'll need to track the powers of 𝑣 and 𝑔 separately.

The range 𝑅 has two incoming paths. The path via the horizontal velocity 𝑣𝑥 contributes +1 × +1 = +1 powers of 𝑣 but no powers of 𝑔. The path via 𝑡 also contributes +1 powers of 𝑣, and contributes −1 powers of 𝑔. The diagram compactly represents how 𝑅 became proportional to 𝑣2/𝑔.

The full range formula, including the launch angle 𝜃 is 

𝑅 ∼ 𝑣2𝑔 sin𝜃cos𝜃. (4.37)

The dependence on 𝑣 and 𝑔 is just as we predicted.

The moral of this example is that you can derive and understand relations by ignoring constants of proportionality and instead concentrating on the scaling exponents. Furthermore, you can use this ability in order to spot mistakes: Just check each independent variable's scaling exponent. For example, if someone proposes that projectile range 𝑅 is proportional to 𝑣3/𝑔, think,「The 1/𝑔 makes sense from the time aloft. But what about the 𝑣3?

One power of 𝑣 comes from the horizontal velocity and one power from the time aloft, which explains two powers of 𝑣. But where does the third power comes from? The range should instead contain 𝑣2/𝑔.」

Problem 4.9 Angular factors in projectile range

Explain the sin 𝜃 and cos 𝜃 factors by using the relation range = time aloft × horizontal velocity.(4.38)

4.2.4 Planetary surface gravity

Scaling, or proportional reasoning, connects independent to dependent variables. Often we have freedom in choosing the independent variables. Here is an example to show you how to use that freedom.

Assuming that planets are uniform spheres, how does 𝑔 , the gravitational acceleration at the surface, depend on the planet's radius 𝑅 ?

We seek the scaling exponent 𝑛 in 𝑔 ∝ 𝑅𝑛. At the planet's surface, the gravitational force 𝐹 on an object of mass 𝑚 is 𝐺𝑀𝑚/𝑅2, where 𝐺 is Newton's constant, and 𝑀 is the planet's mass. The gravitational acceleration 𝑔 is 𝐹/𝑚 or 𝐺𝑀/𝑅2. Because 𝐺 is the same for all objects, we pack light and eliminate 𝐺 to make the proportionality

(4.39)

In this form, with mass 𝑀 and radius 𝑅 as the independent variables, the scaling exponent 𝑛 is −2.

However, an alternative relation comes from noticing that the planet's mass 𝑀 depends on the planet's radius 𝑅 and density 𝜌 as 𝑀 ∼ 𝜌𝑅3. Then 𝑔 ∝ 𝜌𝑅3

𝑅2 = 𝜌𝑅.

(4.40)

In this form, with density and radius as the independent variables, the scaling exponent on 𝑅 is now only 1.

Which scaling relation, with mass or density, is preferable?

Planets vary widely in their mass: from 3.3 × 1023 kilograms (Mercury) to 1.9×1027 kilograms (Jupiter), a range 4 decades wide (a factor of 104). They vary greatly in their radius: from 7 ×104 kilometers (Jupiter) down to 2.4×

103 kilometers (Mercury), a range of a factor of 30. The quotient 𝑀/𝑅2 has huge variations in the numerator and denominator that mostly oppose each other. When there is change, look for what does not change — or, at least, what does not change as much. In contrast to masses, planetary densities vary from only 0.7 grams per cubic centimeter (Saturn) to 5.5 grams per cubic centimeter (Earth) — a range of only a factor of 8. The variations in planetary surface gravity are easier to understand using the planet's radius and density rather than its radius and mass.

This result is general. Mass is an extensive quantity: When two objects combine, their masses add. Density, in contrast, is an intensive quantity.

Adding more of a particular substance does not change its density. Using intensive quantities for the independent variables usually leads to more insightful results than using extensive quantities does.

Problem 4.10 Distance to the Moon

The orbital period near the Earth's surface (say, for a low-flying satellite) is roughly 1.5 hours. Use that information to estimate the distance to the Moon.

Problem 4.11 Moon's angular diameter and radius

On a night with a full moon, estimate the Moon's angular diameter — that is, the visual angle subtended by the Moon. Use that angle and the result of Problem 4.10

to estimate the Moon's radius.

Problem 4.12 Surface gravity on the Moon

Assuming that all planets (and moons) have the same density, use the radius of the Moon (Problem 4.11) to estimate its surface gravity. Then compare your estimate with the actual value and suggest an explanation for the discrepancy.

Problem 4.13 Gravitational strength inside a planet

Imagine a uniform, spherical planet with radius 𝑅. How does the gravitational acceleration 𝑔 depend on 𝑟, the distance from the center of the planet? Give the scaling exponent when 𝑟 < 𝑅 and when 𝑟 ≥ 𝑅, and sketch 𝑔(𝑟).

Problem 4.14 Making toast land butter-side up

As a piece of toast slides off a dining table (starting with almost no horizontal velocity), it picks up angular velocity. Once it leaves the table, its angular velocity remains constant. In everyday experience, a toast usually backflips (rotates 180∘) by the time it hits the ground, and lands butter-side down. How high would tables have to be for a piece of toast to land butter-side up?

4.2 找出标度指数

在晚餐的例子（章节 4,1）中使用了线性正比：当就餐的客人加倍时，需要的食物也加倍。不同量之间的关系具有形式 y oc x，或者，更明显点写成 y oc x^1。其中指数 1 称为标度指数。由于这个原因，比例关系常常被称为标度关系。标度指数是一个有力的抽象：一旦你知道了标度指数，你通常就不再去关注背后的机制。

1-3『书籍「2018148规模」（必读书目），整本书的核心内容讲的就是这里的标度指数。（2022-06-03）』

4.2.1 热身

在线性正比关系之后，下一个最简单最常见的正比类型就是平方正比 —— 即标度指数为 2 —— 以及其近亲，平方根（标度指数为 1/2）等正比关系。作为例子，这里是一个直径为 d=√5 厘米的大圆。

➤ 面积是这个圆的一半的圆半径是多少？

我们首先用非常普通的直接求解的方式，不用正比分析的方式，因此你可以看到什么是不用做的。

从大圆的面积出发：

小圆的面积 A 小国是 A 大圆/2。因此，小圆的半径由下式给出：

(4.7)

考虑到 π/4 并将其约去，我们沿着迂回曲折的路线最后得到了一个简单的结果。尽管这个结果是正确的，但一定有一个更美妙和更富有洞察力的做法。

改进的做法也是从圆面积和直径的关系 A=πd^2/4 出发。但是，这种做法会在较早的时候 —— 即第二步 —— 就将复杂性扔掉，而不是将其保留到分析的最后一步再消去。在日常生活中的类似做法就是旅行前整理行李。你并不会把你不打算读的书和不穿的衣服都拿出来，而是尽早去掉不需要的，轻松旅行：只将必需的装到箱子里，其余的放在一边。

为了让问题简化 —— 解决行李问题，可以看到所有的圆，不管直径如何，都通过相同的因子 (π/4) 将 d^2 和 A 联系起来。因此，当我们要建立 A 和 d 之间的比例关系或标度关系时，我们就扔掉这个因子。结果就是下面的平方正比关系（其中标度指数为 2）：

```
A oc d^2 (4.8)
```

为了得到新的半径，我们需要反过来的标度关系：

```
d oc A^(1/2)  (4.9)
```

在这个形式下，标度指数为 1/2。这个比例关系是下式的简写：

(4.10)

面积比是 1/2，所以直径比是 1/√2。因为大圆的直径是 5 厘米，所以小圆的直径为 √5/2 厘米。

正比分析的解法比直接硬解要更简单和更一般。这个方法还证明了这一结果并不要求形状是圆。只要面积与大小（长度）的平方成正比 —— 这是对所有平面图形都成立的 —— 只要面积比是 1/2，那么长度比就是 1/√2。问题的关键就是标度指数。

题 4.2 水平等分线的长度

在题 3.23，讨论了等分一个等边三角形的最短路径，一个可能的路径是水平线。相对三角形的边，这条线有多长？

通量与面积相联系，因为通量是单位面积的速率。因此，有关面积的标度指数即 —— 即 2 —— 出现在通量的关系中。例如：

➤ 冥王星轨道的太阳通量是多少？

距离太阳 r 处的太阳通量 F 是太阳光度 L —— 即太阳的辐射输出功率 —— 分布在半径为 r 的球面上：

(4.11)

即使 r 在变化，太阳光度是不变的（守恒！），就如因子 4π 一样。因此，按照轻装旅行的精神，将方程 F=L/4πr2 简化为比例关系：

```
F oc r^-2  (4.12)
```

以上扔掉了因子 L 太阳和 4π。这里标度因子是 - 2。负号表示通量和面积成反比关系，2 是将 r 和面积联系起来的标度指数。

标度关系可以简写为：

(4.13)

或

(4.14)

两轨道半径的比大约是 40。因此，冥王星轨道处的太阳通量大约是地球轨道处太阳通量的 40^2 或 1/1600。最后得到的通量大约是 0.8 瓦/m2：

(4.15)

只接受到如此少的阳光，冥王星上一定很冷。我们再次利用正比关系可以估算其阳光表面温度。

表面温度基本上取决于所谓的黑体辐射。表面温度是辐射通量等于接收通量的温度；我们来建立另一个黑箱模型。辐射通量由黑体辐射公式给出（这个公式将在章节 5.5.2 推导）：

```
F=σT^4 (4.16)
```

其中 T 是温度，σ 是斯特藩-玻尔兹曼常数：

(4.17)

➤ 冥王星的表面温度是多少？

正如任何用正比分析计算的例子一样，这个问题也可以用啰唆的硬解方法（尝试题 4.5）。优美的做法是直接利用正比关系：

(4.18) 

其中 r 是轨道半径。将这些关系合并，就得到一个新的正比关系：

(4.19)

一个类似于分而治之法树图的紧凑的图形记号，可以将推导过程总结如：

正如 r→F 的箭头所显示的，改变，也就改变了 F。跟着箭头的方框内数字给出标度指数。因此，r→F 表示 Focr^-2。

F→T 的箭头表示改变 F也就改变了 T，特别地，有 TocF^1/4。

为了找到联系 r 和 F 的标度指数，将这条路径上的标度指数相乘即可：

(4.20)

题 4.3 解释图形记号

在我们标度关系的图形表示中，为什么最后的标度指数是路径上标度指数的相乘，而不是相加？

标度指数表示下列量的比：

(4.21)

（最右边的形式，具有正的标度指数，要比中间形式更为直接和直观，因为不需要先得到一个小于 1 的分数，然后再由于负的指数取倒数。）轨道半径的比是 40，所以表面温度的比应该是 √40 或大约是 6。冥王星的表面温度大约是 50K：

(4.22)

冥王星实际的表面温度是 44K，与我们基于正比分析给出的结果非常接近。

题 4.4 解释不一致

为何我们对冥王星表面温度的预言稍微有点高？

题 4.5 硬算表面温度

为了体验并认识到这种常见但是较差的解题方法，用硬算的方法来估算冥王星的表面温度：（a）从冥王星轨道处的太阳通量，计算表面的平均太阳通量；（b）利用这个通量来估算一个黑体的温度。

4.2.2 轨道周期

在前面的例子中，标度关系形成了一个链（没有分叉的树）：

晚宴上的食物：

圆的面积：

表面温度：

(4.23)

更为详尽的关系也会出现一重新推导著名的行星运动规律时我们就会发现。

➤ 行星的轨道周期是如何取决于其轨道半径 r 的？

我们将研究圆周轨道这一特殊情形（许多行星的轨道都接近于圆周）。我们的探索性思维尝尝得益于将正比问题具体化。因此，我们不是用抽象的记号「依赖于」某量来找到标度指数，而是回答加倍的问题：「当我把这个量加倍时，那个量会如何变化？」

➤ 加倍有什么特殊意义？

加倍 —— 即乘一个 2 倍的因子 —— 是一个最简单的有用的变化。因子 1 虽然是最简单的，但因为完全没有变化，所以是过于简单了。

➤ 将轨道半径加倍后周期会有什么变化？

将轨道半径加倍的最直接后果就是引力变弱了。因为引力是一种平方反比力 —— 即，F oc r^-2 —— 引力将会下降一个 4 倍的因子。表示这些变化的紧凑而直观的方式是直接标出这些量的变化：用记号 ×n 表示所要乘的因子。

(4.24)

因为力正比于加速度，行星的加速度 α 也同样下降一个 4 倍的因子。

对于圆周运动，加速度和速度通过 a=v^ 2/r 联系起来。（我们将在章节 5.1.1 和 6.3.4 通过两种不同的分析工具来导出这个关系。）因此，轨道的速度 v 是 √ar，因此半径加倍，轨道速度增加的因子是 √I/2：

(4.25)

尽管这个计算是正确的，但当我们说到一个√1/2 的因子时，会有一个数值上的冲击。当我们读到「增加一个因子」时，总是会期待一个大于 1 的因子。但这里我们得到的是小于 1 的因子。增加一个小于 1 的因子，常常被简单地描述为减少。因此，更为直观的说法是轨道速度下降了√2 倍的因子。

轨道周期为 T~r/v（记号 ~ 包含了无量纲的因子 2π），因而增大的因子为 2^(3/2)：

总之，将轨道半径加倍则轨道周期要乘以因子 2^(3/2)。一般地，联系 r 和 T 的关系为：

T oc r^(3/2)  (4.27)

这就是计算圆周轨道的开普勒第三定律。我们的标度分析可以用下图表示：

在这个结构中，新的特征是连接的两个带指数的箭头：

1、表示公式 V=√ar 中的 √r。具有 r 的幂次 +1/2。

2、表示公式 V=√ar 中的 √a。为了确定沿着箭头 r 共有多少幂次，只要顺着包含这个箭头的链看：

从左边开始时 r 的幂次是 1。当经过第一个标度指数到达 F 时指数变为 -2。到达 a 时指数仍保持为 -2。最后到达 v 的时候变成 -1。即沿这条路径 r 的幂次是 -1。

总的贡献来自沿着链的三个标度指数的乘积：

(4.28)

这个三元链所携带的指数 -1，表示 r^-1，考虑到直接 r→v 的 +1/2，即表示 r^(+1/2)。结果是 v 将包含 r 的 -1/2 幂次：

让我们再来体验下用同样的分析方法找出联系 T 和 r 的标度关系—— 即开普勒第三定律。直接的 r->T 箭头，具有标度指数 +1，r 的幂次为 +1。v→T 的箭头带有 v 的幂次 -1。因为 v 包含 r 的 -1/2 幂次， 因此 v→T 箭头包含了 r 的 +1/2 幂次：

(4.30)

合并上述结果，两个箭头贡献了 r 的 +3/2 幂次并给出开普勒第三定律：

(4.31)

小结一下我们已经说明很多次的关于指数的规则：1）沿着一条路径时将指数相乘；2）不同路径相交时将指数相加。

让我们将开普勒第三定律应用到一个附近的行星。

➤ 火星年有多长？

正比关系 T oc r^(3/2) 是下列比例关系的简写：

(4.32)

其中 r 火星是火星的轨道半径，r 参考星是参考行星的轨道半径，T 参考是是相应的轨道周期。因为我们最熟悉的是地球，可以将地球作为参考行星。参考行星的周期就是 1（地球）年；而参考半径是 1 天文单位（AU），即 1.5×10^11米。这一选择的好处是求出的火星轨道周期可以用熟悉的单位地球年来表示。

火星到太阳的距离在 2.07×10^11 米（1.38 天文单位）到 2.07×10^11 米（1.67 天文单位）之间变化。因此，火星的轨道并不是非常接近圆周故没有单一的半径 r 火星。（正是由于其轨道显著偏离圆，使得开普勒得出行星沿着椭圆轨道运动的结论）作为 r 火星的近似，我们采用最大和最小半径的平均。这个值是 1.52 天文单位，这给出周期的比约为 1.88：

(4.33)

因此，一个火星年相当于 1.88 个地球年。

题 4.6 轨道周期的硬算

为了强调正比分析和硬算方法的对比，利用硬算的方法来得出火星轨道的周期：从牛顿引力定律出发，然后求出轨道速度和轨道周长。

一个关于轨道的令人惊讶的结论来自加倍问题。

➤ 如果将质量加倍，行星的周期会怎么变化？

利用伽利略倡导的思想实验，想象两个相同质量的行星，一个在另一个后面沿着相同轨道运动。它们具有相同的周期。现在将两个行星捆绑在一起，绳索不改变周期，所以质量加倍的行星与原来单个行星的周期相同：标度指数是零（T oc m^0）！

题 4.7 单摆周期与质量

➤ 一个理想单摆的周期如何取决于摆球的质量？

4.2.3 抛射体的射程

在前面的例子中，只有一个独立变量，改变这个量就改变了所有的量。然而，有许多问题包含了多个独立变量。一个例子就是以速度 v，仰角 θ 抛射出去的石头射程 R。传统推导要用到微积分。你可以解出石头的位置随时间的函数，解出当高度为零（地面）的时间并代回水平距离的公式来算出射程。这么分析是没错，但结果似乎有点像魔术。我不太满意，会这么想，「结果一定是对的。但我还是不知道为什么。」

这个「为什么」的洞察来自正比分析，其中舍去了并非本质的复杂性。

让我们从加倍问题开始。

➤ 每个独立变量都加倍后会如何影响射程？

独立变量包括抛射的速度 v，重力加速度 g（因为是引力将石头拉回地球），以及抛射角。但是角度不是那么容易纳入正比分析，所以我们将不在此讨论 θ 的作用（我们将在章节 8.2.2.1 利用简单案例的工具来处理）。

因为唯一的力沿竖直方向，石头的水平速度在整个飞行中保持常数（是个不变量！）。于是，射程由下式给出：

R = 悬浮时间 x 初始水平速度 (4.34)

悬浮时间是由初始垂直速度决定的，因为引力会稳定地减小它（以 g 的变化率）：

(4.35)

题 4.8 缺失的无量纲因子

前面关于石头悬浮时间表达式前面的无量纲因子是什么？

现在将抛射速度 v 加倍。这将会使初始速度的水平分量和垂直分量加倍。垂直分量的加倍将会使悬浮时间加倍。因为射程正比于水平速度和悬浮时间，当抛射速度加倍时，射程就是原来的四倍。联结ⅴ和 R 的标度指数是 2：R oc v^2。

➤ 加倍 g 的效果是什么？

加倍 g 不会改变水平速度或初始垂直速度，但会使悬浮时间减半因而使射程减半。联结 g 和 R 的标度指数是 -1：R oc g^-1。

最后得到的标度关系，给出 R 同时依赖于 v 和 g 的关系：

(4.36)

利用 vx 和 vy，表示抛射速度的水平分量和垂直分量，这一分析的图形表示为：

这张图向我们展示了一个新特征：两个独立的变量 v和 y。我们将分别求出 v 和 g 的幂次。

射程 R 有两条路径。一条经过 vx 的路径贡献了 v 的 (+1)×(+1)=+1 幂次，但没有 g 的幂次。经过 t 的路径也贡献了 v 的 +1 幂 次，还贡献了 g 的 -1 幂次。上图简要显示了 R  是如何正比于 v^2/g 的。

包括投射角θ在内的完整公式为：

(4.37)

对 v 和 g 的依赖关系正是我们刚才所给出的。角度因子 sinθcosθ 将会用简单案例中的工具来猜测（章节 8.2.2.1），或者尝试题 4.9。

这个例子的意义在于你可以在忽略正比关系的常数情况下导出并理解这个关系，进而将精力集中在标度指数上。进一步，你可以利用这个能力找出错误：来检查下每个独立变量是否具有正确的标度指数。比如，如 果某个人认为抛射体射程R正比于 v^3/g，想一下，「来自悬浮时间的 1/g 是对的，但 v^3 呢？v 的一个幂次来自水平速度另一个幂次来自悬浮时间，这些可以解释 ⅴ 的两个幂次。但第三个幂次是从哪里来的呢？所以射程应该是 v^2/g。」

题 4.9 抛射体射程中的角度因子

利用下列关系解释因子 sinθ 和 cosθ。

射程 = 悬浮时间 x 水平速度 (4.38)

4.2.4 行星表面引力

标度，或者正比分析将独立变量与因变量联系起来。在选择独立变量的时候我们常常有一定的自由度。下面就是显示如何使用这个自由度的例子。

➤ 假定行星是均匀的球形，则表面的重力加速度 g 如何依赖于行星的半径 R?

我们在 g oc R$^n$ 中找出标度指数 n。在行星表面，作用在质量 m 的物体上的引力为 GMm/R^2，其中 G 是牛顿常数，M 为行星质量。重力加速度 g 为 F/m 或 GM/R2。因为 G 对所有物体都是相同的，我们可以轻装上阵将 G 略去，并给出正比关系：

(4.39)

在这个形式中，M 和 R 为独立变量，标度指数 n 为 -2。但是，注意到行星质量 M 与半径 R 和密度 p 有关，M~R^3，可以得到另一个关系。即：

(4.40)

在这个形式中，密度和半径是独立变量，R 的标度指数现在仅为 1。

➤ 哪个标度关系，质量还是密度，是更好的呢？

行星的质量差别很大，从 3.3×10$^23$ 千克（水星）到 1.9×10$^27$ 千克（木星），相差四个数量级（相差 10$^4$ 倍）。半径的变化也很大：从 7×10$^4$ 公里（木星）到 2.4×10$^3$ 公里，相差 30 倍。当分子分母都趋于相反的极端值时，比值 M/R2 变化非常巨大。每当有变化发生，就去寻找不变量 —— 或者，至少找到变化不太大的量。相比质量，行星的密度变化仅从 0.7克/厘米3（土星）到 5.5 克/厘米3（地球）—— 只相差8 倍。行星表面引力的变化用行星的半径和密度来描述会比用其半径和质量来描写更容易理解。

这个结果是一般性的。质量是广延量：当两个物体组合时，质量是相加的。相反，密度是强度量。加入更多的某一物质并不改变其密度。用强度量作为独立变量通常比用广延量作为独立变量会给出更直观更富有洞察力的结果。

题 4.10 到月球的距离

靠近地面的轨道周期（如低空飞行的卫星）大约是 1.5 小时。利用这个信息来估算地球到月球的距离。

题 4.11 月球的角直径和半径

在满月的夜晚，估算月球的角直径一即月球所张视角。利用这个角度和题 4.10 的结果估算月球的半径。

题 4.12 月球的表面引力

假定所有行星（包括月球）都具有相同的密度，利用月球的半径（题 4.11）估算月球的表面引力。将你的估算结果与实际值比较，给出不一致解释的建议。

题 4.13 行星内部的引力强度

假定有一个半径为 R 的均匀球形行星。重力加速度 g 是如何依赖于到行星中心的距离 r 的？给出 `r<R` 和 `r≥R` 时的标度指数，并画出 g(r) 的图形。

题 4.14 让吐司掉地时奶油面朝上

当一片吐司从餐桌掉下时，会获得一个角速度。当它离开桌子后，其角速度保持常数。在日常生活中，一片吐司掉地上时通常会翻转（旋转 180），着地时奶油面朝下。桌子要多高才会使吐司着地时奶油面朝上？

### 4.3 Scaling exponents in fluid mechanics

The preceding introductory examples may mislead you into thinking that proportional reasoning is useful only when we could also find the exact solution. As a counterexample, we return to that source of mathematical beauty but also misery, fluid mechanics, where exact solutions exist for hardly any situations of practical interest. To make progress, we need to discard complexity by focusing on the scaling exponents.

#### 4.3.1 Falling cones

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

After a roughly 2-second fall, they landed almost simultaneously — within 0.1 seconds of each other. Thus, their terminal speeds are the same, give or take 5 percent.

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

As long as the drag coefficients 𝑐d are the same for the big and small cones, they divide out from the ratio. Then the scaling result — that the terminal speed is independent of size — is exact, independent of the drag coefficient.

The moral, once again, is to build on what we know, rather than computing quantities that we do not need and that only clutter the analysis and thereby our thinking. Scaling relations bootstrap our knowledge. Here, if you know the terminal speed of the small cone, use that speed — and the scaling result that speed is independent of size — to find the terminal speed of the large cone. In the next section, we will apply this approach to estimate the fuel consumption of a plane.

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

4.3.2 Fuel consumption of a Boeing 747 jumbo jet In Section 3.5.4, we estimated the fuel consumption of automobiles. For the next example, we'll estimate the fuel consumption of a Boeing 747 jumbo jet. Rather than repeating the structure of the automobile estimate in Section 3.5.4 but with parameters for a plane — which would be the brute-force approach — we will reuse the automobile estimate and supplement it with proportional reasoning.

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

1. Air density. A plane's cruising altitude is typically 35 000 feet or 10 kilometers, which is slightly above Mount Everest. At that height, mountain climbers require oxygen tanks, so the air, and oxygen, density must be significantly lower than it is at sea level. (Once you learn the reasoning tool of lumping, you can predict the density — see Problem 6.36.) The density ratio turns out to be roughly 3:

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

In applying the person-length measuring rod to the width of the plane's body, I remember the comfortable days of regulated air travel. As a child, I would find three adjacent empty seats in the back of the plane and sleep for the whole trip (which explains why my parents insist that traveling with small children was easy). A jumbo jet is three or four such seat groups across — call it three person lengths — and its cross section is roughly circular. A circle is roughly a square, so the cross-sectional area is roughly 10 square person lengths:

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

A plane should be 300 times less fuel efficient than a car — terrible news for anyone who travels by plane!

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

Estimating an air ticket price from fuel cost Estimate the fuel cost for a long-distance plane journey — for example, London to Boston, London to Cape Town, or Los Angeles to Sydney. How does the fuel cost compare to the ticket price? (Airlines do not pay many of the fuel taxes paid by ordinary motorists, so their fuel costs are lower than motorists' fuel costs.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

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

The simplest algorithm for sorting — for example, to sort a list of 𝑛 web pages according to relevance — is bubble sort. You go through the list in passes, comparing neighboring items and swapping any that are out of order.

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

However, using logarithmic scales for both 𝑔 and 𝑟 — called log–log axes — makes the relation clear. Let's try again to slope = −2

represent that when 𝑟 doubles, the gravitational accelera-g ∝ r−2

tion falls by a factor of 4. Call 1 unit on either logarithmic units2

scale a factor of 2. The factor of 2 increase in 𝑟 corresponds to moving 1 unit to the right. The factor of 4 decrease in 𝑔 gearth corresponds to moving 2 units downward. Therefore, the 4

graph of 𝑔 versus 𝑟 is a straight line — and its slope is −2.

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

Now we could solve for 𝑣 explicitly (and you get to find and use that solution in Problems 4.34 and 4.36). However, here we are interested in the total energy, not the flight speed itself. To find the energy without finding the speed, notice a reusable idea, an abstraction, within the right side of the equation for 𝑚𝑔 — which otherwise looks like a mess.

Namely, the mess contains 𝜌air𝑣2𝐿2, which is 𝐹drag/𝐶. Therefore, when the plane is flying at the minimum-energy speed, 𝐹

𝑚𝑔 ∼ 𝐶 drag

𝐶 ,

(4.74)

so

𝐹drag ∼ 𝐶 𝑚𝑔.

(4.75)

Thanks to our abstraction and all the surrounding approximations, we learn a surprisingly simple relation between the drag force and the plane's weight, connected through the square root of our modified drag coefficient 𝐶.

The energy consumed by drag — which, within a factor of 2, is also the total energy — is the drag force times the distance 𝑑. Therefore, the total energy is given by

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

From the total energy, we can estimate the range of the 747 — the distance that it can fly on a full tank of fuel. The energy is 𝐶 𝑚𝑔𝑑, so the range 𝑑 is 𝑑 ∼ 𝐸fuel ,

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

where the area 𝐴 here is usually the wing area. (The same formula structure shows up in drag and lift — abstraction!) Estimate 𝑐L for a 747 in cruising flight.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

134

4 Proportional reasoning

4.6.3 Flight range versus size

In proportional reasoning, we ask,「How does one quantity change when we change an independent variable (for example, if we double an independent variable)?」Because flying objects come in such a wide range of sizes, a natural independent variable is size.

How does the flight range depend on the plane's size?

Let's assume that all planes are geometrically similar — that is, that they have the same shape and differ only in their size. Now let's see how changing the plane's size changes the quantities in the range 𝑑 ∼ 𝛽ℰfuel .

(4.91)

𝐶 𝑔

The gravitational acceleration 𝑔 remains fixed. The fuel energy density ℰfuel and the fuel fraction 𝛽 also remain fixed — which shows again the benefit of using intensive quantities, as we discussed in Section 4.2.4 when we made a scaling relation for planetary surface gravity. Finally, the drag coefficient 𝐶 depends only on the plane's shape (on how streamlined it is), not on its size, so it too remains constant. Therefore, the flight range is independent of the plane's size!

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

### 4.7 Summary and further problems

Proportional reasoning focuses our attention on how one quantity determines another. (A wonderful collection of pointers to further reading is the American Journal of Physics's「Resource Letter」on scaling laws [49].) By guiding us toward what is often the most important characteristic of a problem, the scaling exponent, it helps us discard spurious complexity.

Problem 4.34 Cruising speed versus mass

For geometrically similar animals (the same shape and composition but different sizes) in forward flight, how does the animal's minimum-energy flight speed 𝑣

depend on its mass 𝑚? In other words, what is the scaling exponent 𝛽 in 𝑣 ∝ 𝑚𝛽?

Problem 4.35 Hovering power versus size

In Section 3.6.1, we derived the power required to hover. For geometrically similar birds, how does the power per mass depend on the animal's size 𝐿? In other words, what is the scaling exponent 𝛾 in 𝑃hover/𝑚 ∝ 𝐿𝛾? Why are there no large hummingbirds?

Problem 4.36 Cruising speed versus air density

How does a plane's (or a bird's) minimum-energy speed 𝑣 depend on 𝜌air? In other words, what is the scaling exponent 𝛾 in 𝑣 ∝ 𝜌𝛾air?

Problem 4.37 Speed of a bar-tailed godwit

Use the results of Problem 4.34 and Problem 4.36 to write the ratio 𝑣747/𝑣godwit as a product of dimensionless factors, where 𝑣747 is the minimum-energy (cruising) speed of a 747, and 𝑣godwit is the minimum-energy (cruising) speed of a bar-tailed godwit. Using 𝑚godwit ≈ 400 grams, estimate the cruising speed of a bar-tailed godwit. Compare your result to the average speed of the record-setting bar-tailed godwit that was studied by Robert Gill and his colleagues [19], which made its 11 680-kilometer journey in 8.1 days.

Problem 4.38 Thermal resistance of a house versus a tea mug 

When we developed the analogy between low-pass electrical and thermal filters (Section 2.4.5) — whether 𝑅𝐶 circuits, tea mugs, or houses — we introduced the abstraction of thermal resistance 𝑅thermal. In this problem, you estimate the ratio of thermal resistances 𝑅house thermal⁄𝑅tea mug thermal.

House walls are thicker than teacup walls. Because thermal resistance, like electrical resistance, is proportional to the length of the resistor, the house's thicker walls raise its thermal resistance. However, the house's larger surface area, like having many resistors in parallel, lowers the house's thermal resistance. Estimate the size of these two effects and thus the ratio of the two thermal resistances.

Problem 4.39 General birthday problem

Extend the analysis of Problem 4.24 to 𝑘 people sharing a birthday. Then compare your predictions to the exact results given by Diaconis and Mosteller in [10].

Problem 4.40 Flight of the housefly

Estimate the mechanical power required for a common housefly Musca domestica (𝑚 ≈ 12 milligrams) to hover. From everyday experience, estimate its typical flight speed. At this flight speed, compare the power requirements for forward flight and for hovering.

4.7 小结及进一步的问题

正比分析将我们的注意力集中在一个量如何决定另一个量。（进一步了解，见参考文献 [25]。）通过引导我们接近一个问题最重要的特征，标度指数帮助我们舍去了令人迷惑的复杂性。

题 4.34 削土豆

你是乐意削一个 500 克的土豆，还是 10 个 50 克的土豆，或者 5 个 100 克的土豆？利用标度关系解释你的答案。

题 4.35 巡航速度与质量

对于形状相似的动物（同样的形状和结构但不同的大小），动物能耗最小飞行速度 v 如何取决于其质量 m？换言之，标度关系 v oc m^β 中的标度指数 β 是多少？

题 4.36 巡航速度与空气密度

飞机（或鸟）的能耗最小速度 v 如何取决于 ρ 空气？换言之，标度关系 v∞p^r 室气中的标度指数 r 是多少？

题 4.37 斑尾塍鹬的速度

利用题 4.35 和题 4.36 的结果将速度比 v747/vx 写成无量纲因子的乘积，其中 v747 是波音 747 飞机能耗最小（巡航）速度，而 vx 尾膽稀是斑尾塍鹬能耗最小（巡航）速度。利用 m 尾鹬 ~ 400 克，估算斑尾塍鹬的巡航速度。将你的结果与罗伯特·吉尔和同事研究的创纪录的斑尾塍鹬平均速度 [24] 幻比较，这个速度使斑尾塍鹬在 8.1 天完成了 11680 公里的旅程。

题 4.38 房子和茶杯的热阻

我们在发展低通电路和热滤波之间的类比时（章节 2.4.5） —  —  不论 RC 电路，茶杯，或者房子  —  —  我们引入了热阻 R 热的抽象。在本题中，你估算一下热阻的比 R1/R2。

墙壁要比茶杯壁厚。像电阻一样，热阻抗正比于热阻的长度，房子较厚的墙增大了热阻。但是，房子较大的表面积就像有很多电阻并联样又降低了房子的热阻。估算这两种效应的大小并给出两种热阻的比。

题 4.39 一般的生日问题

将题 4.24 的分析推广到 k 个人具有相同生日的问题。

题 4.40 家蝇的飞行

估算一只普通家蝇（约 12 毫克）悬停时所需的功率。根据日常生活经验，估算其典型的飞行速度。以此速度飞行时，比较向前飞行和悬停所需功率。