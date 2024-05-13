312

A correct analysis works in all cases — including the simplest ones. This principle is the basis of our next tool for discarding complexity: the method of easy cases. We will meet the transferable ideas in an everyday example (Section 8.1.1). Then we will use them to simplify and understand complex phenomena, including black holes (Section 8.2.2.2), the temperature of the Sun (Section 8.3.2.3), and the diversity of water waves (Section 8.4.1).

8.1 Warming up

Let's start with an everyday example, so that we do not have to handle mathematical or physical complexity along with learning the new tool.

8.1.1 Everyday example of easy cases

One August, upon becoming eligible for one of the tax benefits at work, I chose to put `$`500 in an account for the calendar year's health costs (a feature of America's bureaucratic health system). The payroll office advised me that they would deduct `$`125 each month for the rest of the year — namely, for August through December. As August is the eighth month and December the twelfth month, the amount looked correct: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

280

8 Easy cases

`$`500

12th month − 8th month = `$`500

4 months = `$`125

month.

(8.1)

However, in January, the payroll office advised me that they should have deducted only `$`100 per month.

Which amount was correct?

The simplest way to decide is the method of easy cases. Don't directly solve the hard problem of computing the correct deduction in general. Instead, imagine a simpler world in which I started deducting for the year in December. In this easy case, with only one month providing the year's deduction, the answer requires no calculation: Deduct `$`500 per month.

Then use the easy case and this result to check the proposed recipe, which predicted `$`125 per month when deductions started in August. In the easy case, when deductions start in December, the starting and ending months are both the twelfth month, so the recipe predicts an infinite deduction: `$`500

`$` infinity

12th month − 12th month = `$`500

0 months = month .

(8.2)

They do not pay me enough to survive that recipe. It needs an adjustment: `$`500

= `$`500

12th month − 12th month +1 month

1 month = `$`500

month.

(8.3)

Applying this modified recipe to an August instead of a December start, the denominator is 5 months rather than 4 months, and the deduction is `$`100

per month. The revised advice from the payroll office was correct.

This analysis contains several features that we can abstract away and use to simplify difficult problems. First, the easy cases are specified by values of a dimensionless quantity. Here, it is the difference 𝑚2 − 𝑚1 between the first and last month numbers. Second, for particular values of the dimensionless quantity — for the easy cases — the problem has an obvious answer. Here, the easy case is 𝑚2 − 𝑚1 = 0. Third, understanding the easy cases transfers to the hard cases. Here, our understanding of the case 𝑚2 − 𝑚1 = 0 shows that the denominator should be 𝑚2 − 𝑚1 + 1 rather than 𝑚2 − 𝑚1.

8.1.2 Easy cases of the shared-birthday probability The same easy-cases reasoning helps us check more abstruse formulas. As an example, cast your mind back to the birthday paradox of Section 4.4.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.2 Two regimes

281

There, we used proportional reasoning to explain why we need only 23

people, rather than 183 people, in a room before two people are likely to share a birthday. Checking the prediction required the exact probability of a shared birthday:

(𝑛 − 1)

𝑝

⎞

shared = 1 − (1 − 1

365) (1 − 2

365) ⋯ ⎛⎜1 −

⎟ .

(8.4)

⎝

365 ⎠

The last part of Problem 4.23 asked why, with 𝑛 people in the room, the last factor in this probability contains (𝑛 − 1)/365 rather than 𝑛/365.

The simplest answer comes from the easy case 𝑛 = 1. With one person in the room, the probability of sharing a birthday is zero. In this easy case, the prediction of the candidate formula with 𝑛 in the numerator is easy to test.

Its last factor would be 1 − 1/365:

𝑝candidate with 𝑛 = 1 − (1 − 1

365) .

(8.5)

This probability is 1/365, which is incorrect. Thus, with 𝑛 people in the room, the last factor in the probability of a shared birthday cannot contain 𝑛/365. In contrast, the candidate formula with (𝑛 − 1)/365 in the last factor correctly predicts zero probability when 𝑛 = 1: 𝑝candidate with 𝑛−1 = 1 − (1 − 0

365) = 0.

(8.6)

This candidate must be correct.

Problem 8.1

Sine or cosine by easy cases

For a mass sliding down an inclined plane, is its acceleration along the plane 𝑔 sin 𝜃

or g cos 𝜃, where 𝜃 is the angle the plane makes with horizontal? Use an easy case to decide. Assume (the easy case of!) zero friction.

Problem 8.2

Friction by easy cases

For the mass of Problem 8.1, relax the assumption of zero friction. If the coefficient of sliding friction is 𝜇, choose the block's correct acceleration along the plane: (a) 𝑔(sin 𝜃 + 𝜇 cos 𝜃), (b) 𝑔(1 + 𝜇) sin 𝜃, (c) 𝑔(sin 𝜃 − 𝜇 cos 𝜃), or (d) 𝑔(1 − 𝜇) sin 𝜃.

8.2 Two regimes

After warming up with the examples in Section 8.1, let's now look system-atically at how to use the method of easy cases. The first step is to identify the dimensionless quantity. Once you know it — let's call it 𝛽 — the behavior 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

282

8 Easy cases

of the system almost always divides into three regimes: 𝛽 ≪ 1, 𝛽 ∼ 1 (or 𝛽 = 1), and 𝛽 ≫ 1. In a common simplification, which is the subject of this section, one regime is impossible, so two regimes remain. (In Section 8.3, we will discuss what to do when all three regimes remain.) This simplification can happen because symmetry makes the bookend regimes 𝛽 ≪ 1

and 𝛽 ≫ 1 equivalent (Section 8.2.1) or because a geometric or physical constraint excludes one regime (Section 8.2.2).

8.2.1 Only two regimes because of symmetry The bookend regimes 𝛽 ≪ 1 and 𝛽 ≫ 1 are often connected by a symmetry.

Then the analysis at one bookend can be used as the analysis for the other bookend, and there are really two regimes: the symmetric bookends and the middle regime.

8.2.1.1 Why multiplication is more important than addition As an example, here's an easy-cases explanation of why, when estimating, multiplication is a more important operation than addition. Let's say that we are estimating a cost, a force, or an energy consumption that splits into two pieces 𝐴 and 𝐵 to add together — for example, energy for heating and for transportation. Estimating 𝐴 + 𝐵 seems to require addition.

The need disappears after we examine the easy-cases regimes. The regimes are determined by a dimensionless quantity. Because 𝐴 and 𝐵 have the same dimensions, their ratio 𝐴/𝐵 is dimensionless, and it categorizes the three easy-cases regimes.

Regime 1

Regime 2

Regime 3

𝐴 ≪ 𝐵

𝐴 ∼ 𝐵

𝐴 ≫ 𝐵

𝐴/𝐵 ≪ 1

𝐴/𝐵 ∼ 1

𝐴/𝐵 ≫ 1

In the first regime, the sum 𝐴 + 𝐵 is approximately 𝐵. In the symmetric third regime, the sum is approximately 𝐴. The common feature of the first and third regimes — their invariant — is that one contribution dominates the other. Only the second regime, where 𝐴 ∼ 𝐵, is different. To handle it, just make the lumping approximation that 𝐴 = 𝐵; then 𝐴 + 𝐵 ≈ 2𝐴.

So, when estimating 𝐴 + 𝐵, we do not need addition. In the first and third regimes, we just pick the larger contribution, 𝐴 or 𝐵. In the second regime, we just multiply by 2.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.2 Two regimes

283

8.2.1.2 Area of an ellipse

A mathematical example of this kind of symmetry happens when b

guessing the area of an ellipse. The dimensionless quantity is its a

aspect ratio 𝑎/𝑏, where 𝑎 is one-half of the horizontal diameter and 𝑏 is one-half of the vertical diameter. Here are the regimes.

Regime 1

Regime 2

Regime 3

b

b

b

a

a

a

𝑎/𝑏 ≪ 1

𝑎/𝑏 = 1

𝑎/𝑏 ≫ 1

area → 0

area = 𝜋𝑎2

area → 0

The first and third regimes are identical because of a symmetry: Interchanging 𝑎 and 𝑏 rotates the ellipse by 90∘ (and reflects it through its vertical axis) without changing its area. Therefore, any proposed formula for the area must work in the first regime, must satisfy the symmetry requirement that interchanging 𝑎 and 𝑏 has no effect on the area (thereby taking care of the third regime), and must work for a circle (the second regime).

Because of the symmetry requirement, simple but asymmetric modifica-tions of the area of a circle — namely, 𝜋𝑎2 and 𝜋𝑏2 — cannot be the area of an ellipse. A plausible, symmetric alternative is 𝜋(𝑎2 + 𝑏2)/2. In the second regime, where 𝑎 = 𝑏, it correctly predicts the area of a circle. However, it fails in the first regime: The area isn't zero even when 𝑎 = 0.

Is there an alternative that passes all three tests?

A successful alternative is 𝜋𝑎𝑏. It predicts zero area when 𝑎 = 0; it is symmetric; and it works when 𝑎 = 𝑏. It is also the correct area.

8.2.1.3 Atwood machine

In the preceding examples, we had a ready-made dimensionless group and used it to categorize the three easy-cases regimes. The next example shows what you do when there is no group handy: Use dimensional analysis to make one. Then use the group to categorize the regimes and understand the system's behavior. Easy cases and dimensional analysis work together.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

284

8 Easy cases

The example is the Atwood machine, a staple of the introductory mechanics curriculum. Two masses, 𝑚1 and 𝑚2, are connected by a massless, frictionless string and are free to move up and down because of the pulley. This machine, invented by the Reverend George Atwood, reduces the effective gravitational acceleration by a known fraction and makes m1 m2

constant-acceleration motion easier to study. (A historical discussion of the Atwood machine is given by Thomas Greenslade in [27].) Today its principle is used in elevators: The elevator car is 𝑚1, and the counter-weight is 𝑚2.

What is the acceleration of the masses?

Our second step is to identify the easy-cases regimes, 𝑎 LT−2 acceleration but our first step is to find the dimensionless group 𝑔 LT−2 gravity that categorizes them. Therefore, we make our list of 𝑚1 M

left block's mass

relevant quantities and their dimensions. The goal 𝑚2 M

right block's mass

is the acceleration of the masses. Because they are connected by a string, their accelerations have the same magnitude but opposite directions. Let 𝑎 be the downward acceleration of the mass on the left — whether it is labeled 𝑚1 or 𝑚2 (planning for an application of symmetry). Because 𝑎 is our goal quantity, it is the first quantity on the list. The motion is caused by gravity, so the list includes 𝑔. Finally, the masses affect the acceleration, so the list includes 𝑚1 and 𝑚2. And that's the whole list.

Doesn't the tension also affect the acceleration?

The tension has an important effect: Without the tension, there would be no problem to solve, because each mass would accelerate downward at 𝑔.

However, the tension is a consequence of 𝑚1, 𝑚2, and 𝑔 — quantities already on the list. Thus, tension is redundant; adding it would only confuse the dimensional analysis.

This list contains only two independent dimensions: mass (M) and acceleration (LT−2). Four quantities built from two independent dimensions produce two independent dimensionless groups. The most natural choices are the acceleration ratio 𝑎/𝑔 and the mass ratio 𝑚1/𝑚2. Then the most general dimensionless statement is

𝑎𝑔 = 𝑓 (𝑚1𝑚),

(8.7)

2

where 𝑓 is a dimensionless function.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.2 Two regimes

285

Although the next step is to use easy cases to guess the dimensionless function, first pause for a moment. The more we think now in order to choose a suitable representation, the less algebra we have to do later. Here, the ratio 𝑚1/𝑚2 does not respect the symmetry of the problem. Interchanging the masses 𝑚1 and 𝑚2 turns 𝑚1/𝑚2 into its reciprocal: It raises the ratio to the −1 power. Meanwhile, because the left mass is now 𝑚2, which has the opposite acceleration to 𝑚1, this symmetry operation changes the sign of the acceleration 𝑎 (which measures the downward acceleration of the left mass): It multiplies the acceleration by −1. The function 𝑓 will have to incorporate this change in the nature of the symmetry and will have to work hard to turn 𝑚1/𝑚2 into an acceleration. Therefore, 𝑓 will be complicated and hard to guess. (You can find it anyway in Problem 8.3.) A more symmetric alternative to the ratio 𝑚1/𝑚2 is the difference 𝑚1 − 𝑚2.

Now interchanging 𝑚1 and 𝑚2 negates 𝑚1 − 𝑚2, just as it negates the acceleration. Unfortunately, 𝑚1 − 𝑚2 is not dimensionless! It has dimensions of mass. To make it dimensionless, we need to divide it by another mass, say 𝑚1, to make (𝑚1−𝑚2)/𝑚1. Unfortunately, that choice abandons our beloved symmetry. Dividing instead by the symmetric combination 𝑚1 + 𝑚2 solves all the problems. Let's call the result 𝑥:

𝑥 ≡ 𝑚1 − 𝑚2

𝑚

.

(8.8)

1 + 𝑚2

This ratio is dimensionless and respects the problem's symmetry. With it as the dimensionless group, the most general dimensionless statement is 𝑎𝑔 = ℎ(𝑚1−𝑚2

𝑚

) ,

(8.9)

1 + 𝑚2

where ℎ is a dimensionless function (different from 𝑓 ). (This combination of 𝑚1 and 𝑚2 doesn't satisfy the definition of a group given in Section 5.1.1, as a dimensionless product of the quantities raised to various powers. However, it is worth extending the concept to include such combinations.) To guess ℎ, study the easy-cases regimes according to 𝑥. They are three: 𝑥 = −1 (imagine that 𝑚1 = 0), 𝑥 = 0 (when 𝑚1 = 𝑚2), and 𝑥 = +1 (imagine that 𝑚2 = 0). Here you see how easy cases help us. The extremity of the first and third regimes and the simplicity of the second regime amplify our physical intuition and help our gut predict the behavior.

In the first regime, 𝑚2 falls as if there were no mass on the other end of the string. Thus, 𝑚1 rises with acceleration +𝑔. Because 𝑎 measures the downward acceleration of the left mass, 𝑎 = −𝑔. In the third, symmetric 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

286

8 Easy cases

Regime 1

Regime 2

Regime 3

m1

m2

m1

m1

m1

m2

g

g

𝑥 = −1

𝑥 = 0

𝑥 = +1

𝑚1 = 0

𝑚1 = 𝑚2

𝑚2 = 0

𝑎 = −𝑔

𝑎 = 0

𝑎 = +𝑔

regime, 𝑚1 accelerates downward as if there were no mass on the other end, so 𝑎 = +𝑔. In the second regime, where 𝑥 = 0 or 𝑚1 = 𝑚2, the masses are in equilibrium, and 𝑎 = 0.

a/g

Here are the three easy cases plotted on a graph m2 = 0

of the dimensionless acceleration 𝑎/𝑔 versus the 1

dimensionless mass parameter 𝑥. Based on this graph, the simplest conjecture, an educated guess, is that the full graph of ℎ(𝑥) is the straight line of m1 = m2

unit slope passing through the three points. Thus, x

−

its equation is

1

1

𝑎/𝑔 = 𝑥. In terms of the masses, the

equation is

𝑎𝑔 = 𝑚1−𝑚2

𝑚

.

(8.10)

1 + 𝑚2

−1

m1 = 0

In Problem 8.4(d), you solve for the acceleration by using Newton's laws to find the tension in the string. Then you'll confirm our reasonable conjecture based on easy-cases reasoning.

Problem 8.3

Using the less symmetric dimensionless group Find the dimensionless function 𝑓 based on the simpler, but less symmetric, dimensionless group 𝑚1/𝑚2:

𝑎𝑔 = 𝑓 (𝑚1𝑚).

(8.11)

2

Compare it to the dimensionless function that results from choosing the symmetric form (𝑚1 − 𝑚2)/(𝑚1 + 𝑚2) as the independent variable.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.2 Two regimes

287

Problem 8.4

Tension in the string in Atwood's machine In this problem you use easy cases to guess the tension in the connecting string.

a. The tension 𝑇, like the acceleration, depends on 𝑚1, 𝑚2, and 𝑔. Explain why these four quantities produce two independent dimensionless groups.

b. Choose two suitable independent dimensionless groups so that you can write an equation for the tension in this form:

group proportional to 𝑇 = 𝑓 (group without 𝑇).

(8.12)

c. Use easy cases to guess 𝑓 ; then sketch 𝑓 .

d. Solve for 𝑇 using freebody diagrams and Newton's laws. Then compare that result with your guess in part (c), and use 𝑇 to find 𝑎, the downward acceleration of 𝑚1.

8.2.2 Only two regimes because of a restriction In the preceding examples, there were three regimes of a dimensionless quantity, but the two bookend regimes were connected by a symmetry operation and were therefore the same situation. Therefore, there were only two qualitatively different regimes. In the next group of examples, there are only two regimes for a different reason: A geometric or physical constraint excludes one bookend regime.

8.2.2.1 Projectile range

v

In Section 4.2.3, we used proportional reasoning to show that the range of a projectile should have θ

the form 𝑅 ∼ 𝑣2/𝑔, where 𝑣 is its launch velocity.

However, we didn't determine how the launch

R

angle 𝜃 affects the range. We can do so using easy cases, with help from dimensional analysis.

Now the problem contains four quantities: 𝑅, 𝑣, 𝑔, and 𝑅 L

range

𝜃. Four quantities containing two independent dimen- 𝑣 LT−1 launch velocity sions (for example, L and T) produce two independent 𝑔 LT−2 gravity dimensionless groups. A reasonable pair is the launch 𝜃 1

launch angle

angle 𝜃 — which is already dimensionless — and, based on the proportional-reasoning result, 𝑅𝑔/𝑣2. Then the most general dimensionless statement is

𝑅𝑔

𝑣2 = 𝑓 (𝜃),

(8.13)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

288

8 Easy cases

where 𝑓 is a dimensionless function. Solving for 𝑅, 𝑅 = 𝑣2𝑔 × 𝑓(𝜃).

(8.14)

Dimensional analysis does not tell us the form of 𝑓 , but we can guess it by examining the easy cases. Easy-cases reasoning is a way of introducing physical knowledge.

Because angles are dimensionless, 𝜃 can categorize the easy-cases regimes.

The natural easy cases of any quantity are its extremes: 𝜃 ≪ 1 (our usual first regime) and 𝜃 ≫ 1 (our usual third regime). The regime 𝜃 ≪ 1 includes the smallest launch angle 𝜃 = 0∘. Then the range is zero: The projectile starts at ground level, is launched horizontally, and hits the ground immediately. However, the opposite extreme 𝜃 ≫ 1 is not useful, because angles are periodic. Any angle beyond 2𝜋 is already handled by an angle less than 2𝜋. Our usual third regime is therefore geometrically excluded.

Our usual second regime is 𝜃 ∼ 1. Here, the easy angle comparable to 1

(in radians) is 𝜃 = 90∘ (𝜋/2 radians). This angle describes a vertical launch, which doesn't produce any range. Thus, 𝑅 in this regime is also 0.

The two regimes are therefore 𝜃 = 0 (an example of 𝜃 ≪ 1) and 𝜃 = 𝜋/2 (an example of 𝜃 ∼ 1).

Regime 1

Regime 2

𝜃 = 0

𝜃 = 𝜋/2

𝑅 = 0

𝑅 = 0

𝑓 (𝜃) = 0

𝑓 (𝜃) = 0

What reasonable functions satisfy the two easy-cases constraints on 𝑓 (𝜃) ?

π −

One such function is the product of two straight lines, 2

θ

θ

each line ensuring that one of the constraints is satisfied: 𝑓 (𝜃) = 𝜃 (𝜋2 − 𝜃).

(8.15)

π −

2

θ θ

θ

However, this functional form looks funny. The π

𝜋/2 in 0

2

the second factor appears by magic, with no obvious origin in the equations of free fall. Worse, the guess is not periodic. Increasing 𝜃 by 2𝜋 shouldn't change the range, but it changes this proposed 𝑓 . Thus, we need to keep looking.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.2 Two regimes

289

cos θ

sin θ

A similar but less magical form, also the product of two factors, is

𝑓 (𝜃) ∼ sin 𝜃 cos 𝜃.

(8.16)

sin θ cos θ

The cos 𝜃 factor ensures that 𝑓 (𝜋/2) = 0. The sin 𝜃 fac-

θ

π

0

2

tor ensures that 𝑓 (0) = 0. This functional form is also periodic. And it has a physical justification: sin 𝜃 is the trigonometric factor that converts the launch velocity 𝑣 into its vertical component 𝑣𝑦; the cos 𝜃 factor does the same for the horizontal component 𝑣𝑥.

Because these velocities appeared in the proportional-reasoning analysis of Section 4.2.3, we already know that they are physically relevant, making this functional form more plausible than the preceding form.

The resulting range, including the effect of the angle, is then 𝑅 ∼ 𝑣2𝑔 sin𝜃cos𝜃.

(8.17)

This form is correct, and the dimensionless prefactor turns out to be 2 (as you can show in Problem 8.5).

Problem 8.5

Finding the dimensionless constant

Extend the proportional-reasoning analysis of Section 4.2.3 to show that the missing dimensionless prefactor in the projectile range is 2.

8.2.2.2 Light bending with large angles

Our next example of a physical limit excluding a third regime also involves an angle: the bending of light by gravity.

apparent

position

θ

eye

star

starlight

r

Sun

mass m

In Section 6.4.6, we used lumping to find that the gravitational field from a mass 𝑚 bends light by an angle

𝜃 ∼ 𝐺𝑚

𝑟𝑐2 ,

(8.18)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

290

8 Easy cases

where 𝑟 is the distance of closest approach.

This angle is dimensionless. Thus, let's use it to categorize and to investigate the easy cases of light bending. The first regime is 𝜃 ≪ 1 — for example, the Sun bending starlight by roughly 1 arcsecond. The second regime is 𝜃 ∼ 1. In this regime, a new physical phenomenon appears, and lumping will help us analyze it.

coyote:

The lumping analysis is based on the American televi-road

」Oh, no!」

runner

sion cartoon of the Road Runner pursued by the Wile g

E. Coyote. The road runner runs across a chasm, followed by the coyote. They cruise as if gravity is gone, until the road runner, safely across the gap, holds up a sign with an arrow pointing downward explaining,

「Gravity this way.」The coyote looks down, remembers chasm

the existence of gravity, and falls into the chasm.

ray goes merrily along

In the coyote model, light zooms past the mass Bend!

(say, a star) ignorant of gravity. After it has gone θ

too far — by a distance comparable to

r

𝑟 — the star

holds up a sign saying,「You forgot about grav-m

ity! Please bend by

r

𝜃 now!」In this second regime,

𝜃 ∼ 1. The following pictures and analysis are clearest if 𝜃 = 𝜋/2 (or 90∘), so let's use 90∘ to rep-

θ

θ

resent the 𝜃 ∼ 1 regime.

Bend!

Bend!

The ray, on command, bends by 90∘. It travels along and gets reminded again. The distance of closest approach is still 𝑟, so 𝜃 is still 90∘. The beam traces out a square. Although the ray doesn't actually follow this path with its sharp corners, the path illustrates the fundamental feature of the 𝜃 ∼ 1 regime: The ray is in orbit around the star.

When 𝜃 ∼ 1, light gets captured by the strong gravitational field. The third regime, 𝜃 ≫ 1, doesn't introduce a new physical phenomenon — the light is still captured by the gravitational field. In either regime, the mass is a black hole.

Problem 8.6

Guessing a variance

The variance is a squared measure of the spread in a distribution: Var 𝑥 = ⟨𝑥2⟩ − ⟨𝑥⟩2.

(8.19)

where ⟨𝑥2⟩ is the average or expected value of 𝑥2 (the mean square) and ⟨𝑥⟩ is the average value of 𝑥 (the mean).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

291

a. Use an easy case to convince yourself that the mean square ⟨𝑥2⟩ is never smaller than the squared mean ⟨𝑥⟩2.

b. The simplest possible distribution has only two possibilities, 𝑥 = 0 and 𝑥 = 1, with probabilities 1 − 𝑝 and 𝑝, respectively. This distribution describes a coin toss where heads (represented by 𝑥 = 1) comes up with probability 𝑝. Use easy cases to guess Var 𝑥.

Problem 8.7

Local black hole

What is roughly the largest radius that the Earth could have, with its current mass, and be a black hole?

8.3 Three regimes

Two regimes are easier than three. Therefore, we studied that case first to develop experience and identify the transferable ideas. Fortunately, even when a complex situation has three regimes, two simplifications are possible. First, the bookend regimes are often easier than the middle regime (Section 8.3.1). Then we study the bookends and, to predict the behavior in the middle, interpolate between the bookends. Alternatively, two effects compete and reach a draw in the middle regime (Section 8.3.2). This middle regime is then the regime found in nature.

8.3.1 Three regimes where the bookends are easier In a common easy-cases situation, the dimensionless number categorizing the three regimes is a ratio between two physical effects. Then the two bookends are the easiest regimes to analyze — because at each bookend, one or the other effect vanishes. We'll practice this analysis in an example from introductory mechanics (Section 8.3.1.1); then we'll graduate to drag (Section 8.3.1.2).

8.3.1.1 Rolling down the plane

mass m

As our introductory example, let's revisit objects rolling without slipping down an inclined plane. The goal will be to prer

dict an object's acceleration

a

𝑎 along the plane. Dimensional

θ

analysis, from Problem 5.18, tells us that the most general dimensionless statement about 𝑎 is

𝑎𝑔 = 𝑓 (𝜃, 𝐼𝑚𝑟2),

(8.20)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

292

8 Easy cases

where 𝑓 is a dimensionless function, 𝜃 is the incline angle, 𝐼 is the object's moment of inertia, 𝑚 is its mass, and 𝑟 is its radius. The only quantities that affect the acceleration are the two dimensionless groups: the incline angle 𝜃 and the dimensionless mass distribution 𝐼/𝑚𝑟2. The ratio 𝐼/𝑚𝑟2, and therefore the acceleration, is invariant under changes to the object's mass or radius (for example, making a bigger ring or disc). In plainer language, which however doesn't connect as much to symmetry reasoning, simply changing the object's mass or radius without changing its shape does not change its acceleration.

Which shape rolls faster — a ring or a disc?

In this comparison, the inclined plane and thus the incline angle 𝜃 remain fixed. However, the dimensionless group 𝐼/𝑚𝑟2 changes and can categorize the easy-cases regimes. This group occurs repeatedly in the analysis, so we'll often symbolize it as 𝛽. By understanding the behavior in the regimes defined by 𝛽, we'll be able to predict the result of the ring–disc race.

Let's start with the first regime, 𝐼/𝑚𝑟2 = 0. This regime is reached by making 𝐼 zero. Then rolling, represented by 𝐼, becomes irrelevant. The object moves as if it were sliding down the plane without friction. Its acceleration is then 𝑔 sin 𝜃, and 𝑎/𝑔 = sin 𝜃.

With this easy-cases result, we can simplify the unknown function 𝑓 , which unfortunately is a function of two dimensionless groups. As a reasonable conjecture, the dependence on angle is probably still sin 𝜃, even when 𝐼 is not zero. Then the dimensionless statement simplifies to 𝑎𝑔 = ℎ( 𝐼𝑚𝑟2)sin𝜃,

(8.21)

where ℎ is a dimensionless function of only one group.

Let's guess ℎ using easy cases of 𝛽 = 𝐼/𝑚𝑟2. The three regimes will be 𝛽 = 0

(a special case of 𝛽 ≪ 1), 𝛽 ∼ 1, and 𝛽 ≫ 1. In the first regime, when 𝛽 = 0, rolling is unimportant, as we just observed. Therefore, 𝑎/𝑔 = sin 𝜃 and the dimensionless function ℎ(𝛽) is just 1.

The middle regime 𝛽 ∼ 1 is difficult to analyze without a full calculation.

Yet the goal of an easy-cases analysis is to make the situation simple enough that the behavior is easy to see and we can skip the full calculation. Even the simplest value within this regime, 𝛽 = 1, is not any easier than other values. (It describes the ring, where all mass is distributed at the edge of the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

293

object, at a distance 𝑟 from the center). The middle regime is, as promised, the difficult regime. Neither fish nor fowl, it mixes rolling and sliding in comparable amounts.

The solution is to study the third regime, where 𝛽 ≫ 1, and then to interpolate between the first and third regimes in order to predict the behavior in the middle regime. (We implicitly used this interpolation approach in Section 6.4.3, when we estimated the time and distance for a falling cone to reach its terminal speed.)

For an object rolling down the plane, how can 𝛽 be increased beyond 1?

There seems to be no way to increase 𝛽 beyond 1: When 𝛽 = 1, all mass is already distributed at the edge. Fortunately, the subtle point is that, in the dimensional analysis, 𝑟 is the rolling radius, rather than the radius of the object, because the rolling radius determines the torque and the motion.

The object's radius can be larger than the rolling radius. This possibility allows us to increase 𝛽 as much as we want.

ear

As an example, imagine a barbell used for weight lifting: A axle

thin axle of radius 𝑟 connects two large and massive ears of radii 𝑅. Place the axle on the inclined plane, with the ears θ

beyond the plane. The rolling radius is the radius 𝑟 of the axle.

However, the moment of inertia 𝐼 is mostly due to the large ears, because moment of inertia ∝ (distance from the axis of rotation)2.

(8.22)

Thus, 𝐼 ∼ 𝑚𝑅2, where 𝑚 is the combined mass of the two ears, which is almost the same as the mass of the whole object. By choosing 𝑅 ≫ 𝑟, we can make 𝛽 ≫ 1:

2

𝛽 ≡ 𝐼

≫ 1.

(8.23)

𝑚𝑟2 ∼ (𝑅𝑟)

How quickly does this large-𝛽 object accelerate down the plane?

This extreme regime is easier to think about than the intermediate regime 𝛽 = 1. The extremity of the 𝛽 ≫ 1 regime amplifies our intuition and shouts loudly enough for our gut to hear. Then our gut's answer is loud enough for us to hear: The barbell, rolling on its small axle, as long as it doesn't slip, will creep down the plane (the italics represent my gut's shouting). Going fast would, in spinning up the ears, demand far more energy than gravity can provide. Thus, as the ears get ever larger and 𝛽 goes to infinity, the dimensionless rolling factor ℎ(𝛽) goes to zero.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

294

8 Easy cases

Regime 1

Regime 2

Regime 3

ear

axle

m

θ

θ

θ

𝛽 ≡ 𝐼

𝑚𝑟2 = 0

𝐼

𝑚𝑟2 ∼ 1

𝐼

𝑚𝑟2 ≫ 1

𝑎 = 𝑔 sin 𝜃

𝑎 = ?

𝑎 → 0

ℎ = 1

ℎ = ?

ℎ → 0

A simple guess that accounts for the two extreme 1 sliding limit: h(0) = 1

regimes is

interpolated

ℎ(𝛽) = 1

guess

1 + 𝛽.

(8.24)

h( β) → 0

In terms of the original quantities, the acceleration would be

big-ears limit

0

𝑎 = 𝑔 sin 𝜃

0

1

β

1 + 𝐼/𝑚𝑟2 .

(8.25)

This educated guess turns out to be correct (Problem 8.8). Now we can answer our original question about which shape rolls faster. The farther outward the mass is distributed, the greater 𝛽 is, so 𝛽ring > 𝛽disc. Because 𝑎

decreases as 𝛽 increases, the disc rolls faster than the ring.

Problem 8.8

Exact solution to rolling down the plane

Use conservation of energy to find the acceleration of the object along the plane, and confirm the guess based on the easy-cases regimes.

Problem 8.9

A pendulum with chewing gum

A pendulum with a disc as the pendulum bob is oscillating with period 𝑇. You then stick a small piece of chewing gum onto the center of the disc. How does the gum affect the pendulum's period: an increase, no effect, or a decrease?

rod

rod

gum

before

after

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

295

8.3.1.2 Drag using easy cases

Drag, like any phenomenon related to fluids, is a hard problem. In particular, there is no way to calculate the drag coefficient 𝑐d as a function of Reynolds number 𝖱𝖾 — even for simple shapes such as a sphere or a cylinder.

However, dimensional analysis (Section 5.3.2) has told us that drag coefficient

⏟⏟⏟⏟⏟⏟⏟ = 𝑓 (Reynolds number

⏟⏟⏟⏟⏟⏟⏟⏟⏟).

(8.26)

𝑐d

𝖱𝖾

However, dimensional analysis could not tell us the function 𝑓 . That's no slur on dimensional analysis; finding the whole function is beyond our present-day understanding of mathematics. However, we can understand much about 𝑓 in two easy cases: the bookend regimes 𝖱𝖾 ≫ 1 and 𝖱𝖾 ≪ 1.

In the difficult middle regime 𝖱𝖾 ∼ 1, the function 𝑓 interpolates between its behavior in the two extremes.

Low Reynolds number. Flows at low Reynolds number, although not as frequent in everyday experience as flows at high Reynolds number, include a fog droplet falling in air (Problem 8.13), a bacterium swimming in water (discussed in the classic paper「Life at low Reynolds number」[39]), and ions conducting electricity in seawater (Problem 8.10). Our goal here is to find the drag coefficient in the regime 𝖱𝖾 ≪ 1.

The Reynolds number (based on radius) is 𝑣𝑟/𝜈, where 𝑣 is the speed, 𝑟 is the object's radius, and 𝜈 is the kinematic viscosity of the fluid. Therefore, to shrink 𝖱𝖾, either make the object small, make the object's speed low, or use a fluid with high viscosity. The method does not matter, as long as 𝖱𝖾

is small: The drag coefficient is determined not by any of the individual parameters 𝑟, 𝑣, or 𝜈, but rather by the abstraction 𝖱𝖾. We'll choose the means that leads to the most transparent physical reasoning: making the viscosity huge. Imagine, for example, a tiny bead oozing through a jar of cold honey. (The tininess of the bead further reduces 𝖱𝖾.) In this extremely viscous flow, the drag force, as you might expect, is produced directly by viscous forces. As you reasoned in Problem 7.25, viscous forces, which are proportional to the kinematic viscosity 𝜈, are given by 𝐹viscous ∼ 𝜌𝜈 × velocity gradient × area.

(8.27)

The area is the surface area of the object. The velocity gradient is the rate at which velocity changes with distance; it is analogous to the concentration gradient Δ𝑛/Δ𝑥 in the Fick's-law analysis of Section 7.4.2 or to the temperature gradient Δ𝑇/Δ𝑥 in the heat-flow analysis of Section 7.4.4.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

296

8 Easy cases

Because the drag force is due to viscous forces directly, it should be proportional to 𝜈. This constraint determines the form of the function 𝑓 and therefore the drag force. Let's write out the dimensional-analysis result connecting the drag coefficient and the Reynolds number: 𝑐d ≡

𝐹d

= 𝑓 (𝑣𝑟 ,

1

𝜈 )

(8.28)

⏟

2 𝜌𝐴cs𝑣2

𝖱𝖾

where 𝐹d is the drag force and 𝐴cs is the object's cross-sectional area. In terms of the radius, 𝐴cs ∼ 𝑟2, so

𝐹d ∼ 𝑓 (𝑣𝑟 .

(8.29)

𝜌𝑟2𝑣2

⏟

𝜈 )

⏟

∼𝑐d

𝖱𝖾

The viscosity 𝜈 appears only in the Reynolds number, where it appears in the denominator. To make 𝐹d proportional to 𝜈 requires making the drag coefficient proportional to 1/𝖱𝖾. Equivalently, the function 𝑓 , when 𝖱𝖾 ≪ 1, is given by 𝑓 (𝑥) ∼ 1/𝑥. Then

𝐹d

𝜌𝑟2𝑣2 ∼ 𝜈𝑣𝑟.

(8.30)

For the drag force itself, the consequence is (as you found in Problem 7.26) 𝐹d ∼ 𝜌𝑟2𝑣2 𝜈𝑣𝑟 = 𝜌𝜈𝑣𝑟.

(8.31)

This result is valid for almost all shapes; only the dimensionless prefactor changes. For a sphere, the British mathematician George Stokes showed that the missing dimensionless prefactor is 6𝜋: 𝐹d = 6𝜋𝜌𝜈𝑣𝑟.

(8.32)

Accordingly, this result is called Stokes drag.

High Reynolds number. Because the Reynolds number 𝑟𝑣/𝜈 contains three quantities, the limit of high Reynolds number can also be reached in three ways, all of which produce the same behavior. We'll choose the method that is easiest to feel, which is to shrink the viscosity 𝜈 to 0. In this limit, called form drag, viscosity disappears from the problem and the drag force should not depend on viscosity. This reasoning contains several untruths, but they are subtle and the conclusion is mostly correct. (Clarifying the subtleties required centuries of progress in mathematics, culminating in the theory of singular perturbations and boundary layers, the subject of Section 7.3.4 and discussed much more in Physical Fluid Dynamics [46].) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

297

Without viscosity and thus without the Reynolds number to depend 𝑐d

on, the dimensionless function 𝑓 must be a constant! Its value de- car 0.4

pends on the shape of the object and typically ranges from 0.5 to 2. sphere 0.5

Because the drag coefficient is 𝐹d/12𝜌𝑣2𝐴cs, the drag force is cylinder

1.0

𝐹d ∼ 𝜌𝑣2𝐴cs.

(8.33) flat plate

2.0

This result agrees with our analysis in Section 3.5.1 based on energy conservation. In that analysis, we had implicitly assumed a high Reynolds number without knowing it.

Problem 8.10

Conductivity of seawater

Estimate the conductivity of seawater by assuming that the current-carrying ions (Na+ or Cl−) travel with a shell one layer thick of water molecules around them.

Problem 8.11

Drag coefficient resulting from Stokes drag At low Reynolds number, the drag force on a sphere is 𝐹 = 6𝜋𝜌𝜈𝑣𝑟 (Stokes drag).

Find the drag coefficient 𝑐d as a function of Reynolds number, basing the Reynolds number on the sphere's diameter rather than its radius.

Problem 8.12

Choosing the high- or low-Reynolds-number regime To estimate the terminal speed of a raindrop (Problem 3.37), you implicitly used the high-Reynolds-number regime. Now that you know another regime, how can you choose which regime to use? Without knowing which regime, you cannot find the terminal speed. Without the terminal speed, how do you find Reynolds number, which you need to choose the regime? The answer is to choose a regime and see whether the result is self-consistent. If it is not, choose the other regime.

As practice with this reasoning, assume that the Reynolds number for the falling raindrop is small and therefore that the drag force 𝐹d is given by Stokes drag: 𝐹d ∼ 𝜌air𝜈𝑣𝑟.

(8.34)

Estimate the resulting terminal speed 𝑣 for the raindrop (diameter of about 0.5

centimeters). Then check the assumption that 𝖱𝖾 ≪ 1.

Problem 8.13

Terminal speed of fog droplets

a. Estimate the terminal speed of fog droplets (𝑟 ∼ 10 𝜇m). In estimating the drag force, use either the limit of low or high Reynolds numbers — whichever limit you guess is more likely to be valid. (Problem 8.12 introduces this reasoning.) b. Use the speed to estimate the Reynolds number and check whether you used the correct limit for the drag force. If not, try the other limit!

c. Fog is a low-lying cloud. How long does a fog droplet require to fall 1 kilometer (a typical cloud height)? What is the everyday effect of this settling time?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

298

8 Easy cases

Interpolation. We now know the drag force in the two extreme regimes: viscous drag (low Reynolds number) and form drag (high Reynolds number).

Interpolating between these regimes is easiest in dimensionless form — that is, in terms of the drag coefficient rather than the drag force.

24

When 𝖱𝖾 ≫ 1, the drag coefficient 𝑐d is roughly cd ≈ Re

0.5 (for a sphere). On log–log axes, the 𝖱𝖾 ≫ 1

behavior is a straight line with zero slope. In the 𝖱𝖾 ≪ 1 regime, you should have found in Prob- Re 1

Re 1

lem 8.11 that the drag coefficient (for a sphere) is

c

24/𝖱𝖾, where the Reynolds number is based

d ≈ 0.5

on the diameter rather than the radius: The 1/𝖱𝖾

scaling happens because, as we just deduced, 𝑓 (𝖱𝖾) ∼ 1/𝖱𝖾 to make the drag force proportional to viscosity 𝜈; the dimensionless prefactor of 24 is what you had to compute. On log–log axes, the 𝖱𝖾 ≪ 1 behavior is also a straight line but with a −1 slope.

The dashed line interpolates between the extremes. The final twist is that at 𝖱𝖾 ∼ 3×105, the boundary layer becomes turbulent (Problem 7.23), and the drag coefficient drops significantly. With that caveat, we have explained the main features of drag, a ubiquitous force in the living world.

Problem 8.14

Q as an easy-cases parameter

A damped spring–mass system has a dimensionless measure of damping known as the quality factor 𝑄, which you studied in Problem 5.53. Choose 𝑄 ≪ 0.5, 𝑄 = 0.5, or 𝑄 ≫ 0.5 to describe each of the three regimes: (a) underdamped, (b) critically damped, and (c) overdamped.

Problem 8.15

Floating on water

Some insects can float on water thanks to the surface tension of water. Extend the analysis of this effect from Problem 5.52 by estimating the dimensionless ratio force due to surface tension

𝑅 ≡

weight of the bug

(8.35)

as a function of the bug's size 𝑙 (as a length). Interpret the regimes 𝑅 ≪ 1 and 𝑅 ≫ 1, and find the critical bug size 𝑙0 for floating on water.

Problem 8.16

Energy loss in highway versus city driving Explain why the following dimensionless ratio measures the importance of drag: mass of fluid swept out

mass of object

.

(8.36)

An equivalent computation, except for a dimensionless factor of order unity, is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

299

fluid density

distance traveled

object density × size of object ,

(8.37)

where the size of the object is its linear dimension in the direction of travel. When this ratio is comparable to unity, drag significantly affects the trajectory.

Apply either form of the ratio to a car during city driving, and find the distance 𝑑 at which the ratio becomes significant (say, roughly 1). How does the distance compare with the distance between stop signs or traffic lights on city streets? What therefore is the main mechanism of energy loss in city driving? How does this analysis change for highway driving?

Problem 8.17

Gain of an RC circuit

R

The low-pass 𝑅𝐶 circuit of Section 2.4.4 is amen- Vin Vout

able to easy-cases analysis. With the abstraction of capacitive impedance (Section 2.4.4), explain C

the unity gain at low frequency and why the gain goes to zero at high frequency. What is the dimen-ground

sionless way to say「high frequency」?

Problem 8.18

Bode magnitude sketch for an RC circuit A Bode magnitude plot is a log–log plot of ∣gain∣ versus frequency. In a lumped Bode sketch, which often gives the most insight into the behavior of a system, the segments of the plot are straight lines. Make the Bode magnitude sketch for the low-pass 𝑅𝐶 circuit of Problem 8.17, labeling the slopes and intersection points.

8.3.2 Three regimes where two effects compete In the final group of three-regime examples, the three regimes are again based on the relative size of two physical effects. However, in contrast to the examples in Section 8.3.1, where we chose a regime — for example, by choosing a flow speed and thus the Reynolds number — here nature chooses. Nature chooses the middle regime, where the two competing physical effects reach a draw. The method of easy cases shows how that choice is made.

8.3.2.1 Height of the atmosphere

Competition between physical effects is the theme of the wonderful Gases, Liquids and Solids and Other States of Matter [43, pp. xiii], where we learn how「the three primary states of matter are the result of competition between thermal energy and intermolecular forces.」The following example, estimating the height of our atmosphere, illustrates an analogous competition: between thermal energy and gravity. Here is how these two physical effects determine the height of the atmosphere.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

300

8 Easy cases

1. Thermal energy. Thermal energy gives the molecules speed. Unfettered by gravity, the air molecules and the atmosphere would disperse into space. Thermal energy is therefore responsible for increasing the atmosphere's height.

2. Gravity. Gravity pulls air molecules downward. If gravity is the only effect, meaning that thermal motion is absent (the atmosphere is at absolute zero), then gravity pulls the molecules all the way to the ground.

Gravity therefore decreases the atmosphere's height.

A dimensionless measure of the relative size of the two effects is a comparison of the typical gravitational energy with the thermal energy of one molecule. The typical thermal energy is 𝑘B𝑇. With 𝑚 for the molecule's mass and 𝐻 for the characteristic or typical or scale height of the atmosphere, the typical gravitational potential energy is 𝑚𝑔𝐻. The energy ratio is then 𝛽 ≡ 𝑚𝑔𝐻

𝑘B𝑇 .

(8.38)

This ratio categorizes the three easy-cases regimes: 𝛽 ≪ 1, 𝛽 ∼ 1, and 𝛽 ≫ 1.

Regime 1

Regime 2

Regime 3

gravity

thermal

atmosphere

atmosphere

atmosphere

expanding

stable

contracting

𝛽 ≪ 1

𝛽 ∼ 1

𝛽 ≫ 1

𝑚𝑔𝐻 ≪ 𝑘B𝑇

𝑚𝑔𝐻 ∼ 𝑘B𝑇

𝑚𝑔𝐻 ≫ 𝑘B𝑇

In the first regime, the atmosphere is expanding: The molecules have so much thermal energy that they escape farther from Earth. In the third regime, the atmosphere is contracting: The molecules do not have enough thermal energy to resist gravity as it pulls them back to Earth. The happy medium, where the atmosphere is stable, is the middle regime.

Therefore, the regime is chosen not by us but by nature. The height of the atmosphere is determined by the requirement that the two effects compete and reach a draw — when the two effects are comparable in strength. In that regime, 𝑚𝑔𝐻 ∼ 𝑘B𝑇, so the atmosphere's scale height is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

301

𝐻 ∼ 𝑘B𝑇

𝑚𝑔 .

(8.39)

For the Earth's atmosphere, where 𝑇 ≈ 300 K and the molecular mass 𝑚 is approximately the mass of a nitrogen molecule, this height is roughly 8 kilometers — as we predicted in Section 5.4.1 using dimensional analysis. The easy-cases reasoning complements the dimensional analysis by providing a physical model.

As a bonus, this general model of competition explains why we guess that an unknown dimensionless number is comparable to 1 — for example, when we estimated an atomic blast energy in Section 5.2.2. Often, the dimensionless number represents a ratio between two physical effects. Then「comparable to 1」means「the effects have reached a draw.」By guessing that unknown dimensionless numbers were comparable to 1, we foreshadowed the easy-cases reasoning that we use for these examples of competition.

8.3.2.2 Hydrogen's binding energy

Our next example, before we turn to the giant scales of stars, is our old friend the hydrogen atom. In Section 5.5.1, we predicted its size, the Bohr radius 𝑎0, using dimensional analysis. The prediction was correct, but, as with the dimensional analysis of the atmosphere height, dimensional analysis didn't give us a physical model. Easy-cases reasoning will help us make our tacit physical knowledge about hydrogen explicit and thereby build a physical model.

As we found in Section 6.5.2 using lumping, two physical effects compete: 1. Electrostatics. The electrostatic attraction between the proton and electron shrinks the atom.

2. Quantum mechanics. Via the uncertainty principle, quantum mechanics gives an electron confined to a small region a high momentum uncertainty and, therefore, a high kinetic energy. With this confinement energy, analogous to the thermal energy of an air molecule, the electron can resist the inward pull of electrostatics. Therefore, quantum mechanics expands the atom.

A dimensionless ratio that measures the relative size of the two effects is the energy ratio

∣ electrostatic potential energy ∣

𝛽 ≡

confinement energy

,

(8.40)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

302

8 Easy cases

where the absolute-value bars say that, although the electrostatic potential energy is negative, we care only about its magnitude.

In a hydrogen atom of radius 𝑟, the electrostatic energy is 𝑒2/4𝜋𝜖0𝑟. The confinement energy — which we estimated in Section 6.5.2 by using lumping — is comparable to ℏ2/𝑚e𝑟2. Therefore,

𝛽 ∼ 𝑒2/4𝜋𝜖0𝑟

ℏ2/𝑚e𝑟2 .

(8.41)

Regime 1

Regime 2

Regime 3

𝛽 ≪ 1

𝛽 ∼ 1

𝛽 ≫ 1

expanding

stable

contracting

𝑒2

𝑒2

𝑒2

4𝜋𝜖0𝑟 ≪ ℏ2

𝑚e𝑟2

4𝜋𝜖0𝑟 ∼ ℏ2

𝑚e𝑟2

4𝜋𝜖0𝑟 ≫ ℏ2

𝑚e𝑟2

In the first regime, 𝛽 ≪ 1, quantum mechanics is much stronger than electrostatics, and the huge kinetic energy from quantum mechanics (the confinement energy) expands the atom. In the third regime, 𝛽 ≫ 1, electrostatics, now much stronger than quantum mechanics, contracts the atom.

The radius of hydrogen, like the height of the atmosphere, is determined by the requirement that two physical effects compete and reach a draw. This truce happens in the middle regime. There, 𝑒2/4𝜋𝜖0𝑟 ∼ ℏ2/𝑚e𝑟2, so 𝑟 ∼

ℏ2

,

(8.42)

𝑚e(𝑒2/4𝜋𝜖0)

which is the Bohr radius 𝑎0 that we found using dimensional analysis (Section 5.5.1) and lumping (Section 6.5.2).

An alternative approach, which also uses easy cases but gives different insights, is to base the dimensionless ratio on the size 𝑟 directly. Making 𝑟

dimensionless requires another size. Fortunately, we have one, because the two energies, electrostatic and confinement, have different scaling exponents. The electrostatic energy is proportional to 𝑟−1. The confinement energy is proportional to 𝑟−2.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

303

Regime 1

Regime 2

Regime 3

𝛽 ≪ 1

𝛽 ∼ 1

𝛽 ≫ 1

expanding

stable

contracting

𝑟 ≪ 𝑟0

𝑟 ∼ 𝑟0

𝑟 ≫ 𝑟0

On log–log axes, they are straight lines but with different slopes: Econfinement

−2 for the confinement line and −1 for the electrostatic-energy

∝ r−2

line. Therefore, they intersect. The size at which they intersect Eelectrostatic is a special size. Let's call it 𝑟0. Then our dimensionless ratio is

∝ r−1

𝛽 ≡ 𝑟/𝑟0, and the three regimes are shown in the table.

r0

The stable middle regime is the one chosen by nature. Then 𝑟, the radius of hydrogen, is comparable to our special radius 𝑟0.

The special radius, and therefore 𝑟, is determined by equating electrostatic and confinement energies, which is how we found the Bohr radius 𝑎0 in Section 6.5.2. Thus, the radius of hydrogen is the Bohr radius and results from competition between electrostatics and quantum mechanics.

E

Our next project is to use the easy-cases regimes of size to understand thermal expansion — why substances expand upon heating. The first step is to sketch the total energy 𝐸, Econfinement

which is the sum of confinement and electrostatic energies.

This sketch is easiest in the bookend regimes. In the first regime, where 𝑟 ≪ 𝑟0, the atom is too small, and quan-r

tum mechanics is stronger: Its kinetic-energy contribution Eelectrostatic

is the dominant term in the energy, because its 1/𝑟2 scaling overwhelms the 1/𝑟 scaling of the potential energy. In the third regime, where 𝑟 ≫ 𝑟0, the atom is too large, and electrostatics is the dominant term in the energy: Its 1/𝑟 scaling goes to zero more slowly than the 1/𝑟2 scaling of the kinetic energy. Therefore, in the extremes (the bookends), the total energy has two different scalings: 𝐸 ∝ { 1/𝑟2 (regime 1: 𝑟 ≪ 𝑟0)

−1/𝑟 (regime 3: 𝑟 ≫ 𝑟0)

(8.43)

To complete the sketch, we interpolate between the bookend regimes.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

304

8 Easy cases

E

The slopes in the two regimes have opposite signs, so there is no smooth way to connect the two extreme segments without introducing a point where the slope is zero. This Econfinement

point, where the energy is a minimum, is nature's choice for the ground state of hydrogen.

a0

With this sketch, we can explain thermal expansion. Ther-r

mal expansion first appeared in Problem 5.38, where you Eelectrostatic

used dimensional analysis to estimate a typical thermal-expansion coefficient. However, the problem glided over the fundamental question: the coefficient's sign. Knowing nothing about thermal expansion, we might guess that positive and negative coefficients are equally likely. Equivalently, substances are equally likely to expand as to contract when heated: Some substances might expand, and others might contract. However, this symmetry reasoning fails empirically: Almost all substances expand rather than contract when heated. The symmetry between positive and negative thermal-expansion coefficients, or between expansion and contraction, must get broken somewhere.

The curve of energy versus size for hydrogen shows where the symmetry gets broken. In its generic shape, the curve applies to all bonds, whether intra-atomic (such as the electron–proton bond in hydrogen), interatomic (such as hydrogen–oxygen bonds in a water molecule), or even intermolecular (such as the hydrogen bonds between water molecules). Bonds result from a competition between (1) attraction, which is important at long distances and which looks like the electrostatic piece of the generic curve, and (2) repulsion, which is important at short distances and which looks like the confinement piece of the generic curve. (Even the gravitational bond between the Sun and a planet, represented by the curve that you drew in Problem 5.55c, has the same shape.)

Therefore, the curve of bond energy versus separation cannot be symmetric.

At the 𝑟 ≪ 𝑟0 end, which is the first regime, 𝑟 has a minimum possible value, namely zero. However, at the 𝑟 ≫ 𝑟0 end, which is the third regime, 𝑟 is unbounded. Thus, the two bookend regimes are not symmetric, and the bond-energy curve skews toward larger 𝑟.

To see how this asymmetry leads to thermal expansion, look at how thermal energy affects the average bond length. First, think of the bond as a spring (a model that we will discuss further in Section 9.1). As the bond vibrates around its equilibrium length 𝑟0, thermal energy, which is a kinetic energy, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

305

converts into and out of potential energy in the bond. The minimum bond length 𝑟min and the maximum bond length 𝑟max are determined by where the vibration speed is zero — where the bond has slurped up all the kinetic energy (the thermal energy) and turned it into potential energy.

ravg

ravg

ravg

r

r

r

Ethermal

Ethermal

cold

warm

hot

Graphically, we draw a horizontal line at a height 𝐸thermal above the minimum energy. This line intersects the potential-energy curve twice, at 𝑟 =

𝑟min and at 𝑟 = 𝑟max. Because the potential-energy curve skews to the right, toward 𝑟 ≫ 𝑟0, the average bond length 𝑟avg = (𝑟min + 𝑟max)/2 is larger than 𝑟0. As 𝐸thermal grows, the skew affects the average more, and the difference between 𝑟avg and 𝑟0 grows: Adding thermal energy increases the bond length. Therefore, substances expand when heated.

8.3.2.3 Core temperature of the Sun

As our final example, we'll estimate the temperature of the core of the Sun.

The Sun, like the atmosphere, is a result of competition between thermal motion and gravity: Thermal motion expands the Sun; gravity compresses the Sun. A dimensionless measure of the two effects' relative strength is thermal energy

𝛽 ≡

.

(8.44)

∣ gravitational potential energy ∣

The numerator, the thermal energy for one particle, is just 𝑘B𝑇. For the denominator, we need to know the mass of a particle. The Sun itself is made of hydrogen, but in the core of the Sun, the thermal energy is more than enough to strip an electron from the proton (as you verify in Problem 8.19).

Each proton gets gravitational potential energy from the rest of the Sun, which has mass 𝑀Sun. The rest of the Sun, if lumped into a massive particle, would be at a distance comparable to 𝑅Sun, where 𝑅Sun is the Sun's radius.

Therefore, the typical gravitational potential energy (per particle) is 𝐺𝑀

𝐸

Sun𝑚p

gravitational ∼

𝑅

,

(8.45)

Sun

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

306

8 Easy cases

where the ∼ contains the minus sign in the potential energy. The ratio of energies is therefore

𝛽 ∼

𝑘B𝑇

𝐺𝑀

,

(8.46)

Sun𝑚p/𝑅Sun

and it produces the following three regimes.

Regime 1

Regime 2

Regime 3

too cold, contracting

stable

too hot, expanding

𝛽 ≪ 1

𝛽 ∼ 1

𝛽 ≫ 1

𝐺𝑀

𝐺𝑀

𝐺𝑀

𝑘

Sun𝑚p

Sun𝑚p

Sun𝑚p

B𝑇 ≪

𝑅

𝑘B𝑇 ∼

𝑘B𝑇 ≫

Sun

𝑅Sun

𝑅Sun

In the first regime, the Sun is too cold for its size, so gravity wins the competition and compresses the sun. This contraction shows the difference between the thermal–gravitational competition in the Sun and in the Earth's atmosphere (Section 8.3.2.1). The temperature of the atmosphere is determined by the blackbody temperature of the Earth, roughly 300 K (Problem 5.43). In our analysis of the height of the atmosphere, we therefore held the temperature fixed and let only the height vary until it produced the gravitational energy to match the fixed thermal energy. In the Sun, however, the temperature is determined by the speed of the fusion reactions, which depends on the temperature and the density: Higher density means more frequent collisions that might result in fusion, and higher temperature (faster thermal motion) means that each collision has a higher chance of resulting in fusion. Thus, as the Sun contracts, the density increases, as does the temperature and the reaction rate. The contraction stops when the temperature is high enough for thermal motion to balance gravity.

(There is a caveat. If a star contracts very quickly, its core can heat up faster than the negative-feedback process can oppose the change. Then the core ignites like a giant hydrogen bomb and the star becomes a supernova.) In the third regime, the Sun is too hot for its size, so thermal motion wins the competition and expands the Sun. As the Sun expands, the reaction rate, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.3 Three regimes

307

the temperature, and the thermal energy fall — until thermal motion again balances gravity. The result is the middle regime. In the middle regime, the Sun has just the right temperature — determined by the condition 𝑘B𝑇 ∼

𝐺𝑀Sun𝑚p/𝑅Sun, so

𝐺𝑀

𝑇 ∼

Sun𝑚p

𝑘

.

(8.47)

B𝑅Sun

The proton mass 𝑚p in the numerator and Boltzmann's constant 𝑘B in the denominator are easier to handle if we multiply each constant by Avogadro's number 𝑁A. The product 𝑁A𝑘B is the universal gas constant 𝑅. The product 𝑚p𝑁A is the molar mass of protons, which is approximately the molar mass of hydrogen: 1 gram per mole. Then

𝐺

𝑀Sun

𝑁A𝑚p

⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞⏞⏞

𝑇 ∼ 6.7 ×10−11 kg−1 m3 s−2 × 2×1030 kg × 10−3 kg mol−1 .

(8.48)

8 J mol−1 K−1

⏟⏟⏟⏟⏟⏟⏟ × 0.7 ×109 m

⏟⏟⏟⏟⏟⏟⏟

𝑁A𝑘B

𝑅Sun

To evaluate 𝑇, start with the most important piece.

1. Units. The inverse moles in the numerator and denominator cancel. The numerator then contributes kg m3 s−2, which is J m. The denominator contributes J K−1 m. Therefore, the J m in the numerator and denominator cancel, and the inverse kelvins in the denominator become the kelvins in the Sun's core temperature.

2. Powers of ten. The numerator contributes 16 powers of ten; the denominator contributes 9. The result is 7 powers of ten. Thus, the temperature will be comparable to 107 K.

3. Numerical prefactor. The 6.7 in the numerator is mostly canceled out by the 8×0.7 in the denominator, leaving only the 2 in the numerator. Thus, the temperature is roughly 2×107 K.

No one has measured the internal temperature directly, but the current best estimate for the core temperature is 1.5 × 107 K. Our easy-cases model of competition between gravity and thermal motion is surprisingly accurate.

Problem 8.19

Thermal versus electronic energy

Compare the thermal energy (per particle) in the core of the Sun to the binding energy of hydrogen. Were we justified in assuming that the electrons get stripped from the protons?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

308

8 Easy cases

8.4 Two dimensionless quantities

In the examples of Section 8.3, one dimensionless quantity categorized the easy-cases regimes. Whether the quantity was small, comparable to 1, or large, the regimes could all be arranged on one axis. To extend that idea, we'll use easy cases to categorize the world using two dimensionless quantities and therefore two axes. For practice, we'll organize the world of waves onto a two-dimensional map (Section 8.4.1). Then we'll organize the four fundamental branches of physics (Section 8.4.2).

8.4.1 The two-dimensional world of water waves Water waves come in several varieties. Perhaps the most evident regime represents waves near a beach. These waves, the subject of Problem 5.15, have a wavelength much larger than the depth of the water. You can make them at home: Fill a bathtub or baking dish with water, disturb the water, and create waves sloshing back and forth. Their speed 𝑣 is given by 𝑣2 = 𝑔ℎ, where ℎ is the depth of the water.

Before these shallow-water waves reached the beach, they traveled shallow-water

waves

on the open ocean, where their wavelength was much smaller than v2 = gh

the depth. Their speed — technically, the phase velocity — is given by 𝑣2 = 𝑔𝜆 (Problem 5.11), where 𝜆 is the reduced wavelength 𝜆/2𝜋.

h → 0

These two regimes — deep and shallow water — are distinguished by n

the dimensionless ratio ℎ/𝜆. (You can also use ℎ/𝜆, but the math-deep-water

ematical descriptions turn out to be simpler using ℎ/𝜆.) Therefore, waves

the two regimes sit on a dimensionless axis that measures depth.

v2 = gn

Because the axis measures depth, let's orient the axis vertically and place deep water at the bottom.

Another familiar kind of wave is produced by dropping a pebble in a pond.

Small ripples zoom outward from the point of impact. These waves have a small wavelength, much smaller than the depth of the pond. Therefore, ℎ/𝜆 is large — as it is for deep-water waves.

However, these ripples are different from the deep-water waves on the open ocean. Ocean waves are driven by the water's weight — that is, by gravity. In contrast, ripples are driven by the water's surface tension — the same effect that allows small bugs to walk on water (see Problem 8.15). In order to distinguish ripples from deep-water gravity waves, our second axis should measure the relative importance of gravity and surface tension.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.4 Two dimensionless quantities 309

This axis is therefore labeled by the ratio of gravity to surface tension. This ratio is a dimensionless group, so we can find it using dimensional analysis.

The ratio will depend on two characteristics of the water: its density 𝜌 (to make the weight) and its surface tension 𝛾. It will depend on gravity 𝑔

(to make the weight). And it will depend on the (reduced) wavelength 𝜆.

These four quantities, built from three dimensions, form one independent dimensionless group. A useful choice is 𝜌𝑔𝜆2/𝛾.

At long wavelengths (large 𝜆), in dense fluids (large 𝜌), or in strong gravity (large 𝑔), this dimensionless ratio is large, indicating that gravity drives the waves. For short wavelengths (ripples) or, equivalently, high surface tension, this ratio is small, indicating that surface tension drives the waves.

Here are the three regimes categorized using both groups.

shallow-water

gravity waves

v2 = gh

h → 0

n

ρg 2

n

→

deep-water

deep-water

γ

0

ripples

gravity waves

γ

v2 = gn

v2 = ρn

The empty corner stares at us, asking to be filled. It incorporates both limits: ℎ𝜆 → 0 (shallowwater) and 𝜌𝑔𝜆2𝛾 → 0 (ripples).

(8.49)

shallow-water

shallow-water

ripples

gravity waves

2

γh

v2 = gh

ρgn

v2 =

→ 0

ρ 2

n

γ

h

h

→ 0

→ 0

n

n

ρg 2

n

→

deep-water

deep-water

γ

0

ripples

gravity waves

γ

v2 = gn

v2 = ρn

These waves are therefore ripples on shallow water. (They are hard to make, because ripples are tiny, smaller than a few millimeters, yet the water depth must be even smaller.)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

310

8 Easy cases

The four corners are the bookend regimes on two axes. If each axis had three regimes, two axes could have made three squared or nine regimes.

The missing five middle regimes can be constructed by interpolating between the corners. The easy-cases map shows how: First fill in the four regions between the corners, and then fill in the center. That analysis, which involves addition and a tanh function, gives the following map.

ρg 2

n

ρg 2

n

shallow-water

shallow-water

∞ ←

shallow-water waves

→

γ

γ

0

ripples

gravity waves

γh

v2 = gh +

γh

v2 = gh

ρ 2

n

v2 = ρ 2

n

h

h

→ 0

→

h

0

→ 0

n

n

n

ρg 2

2

n

ρgn

gravity waves

∞ ←

all waves

→ 0

ripples

γ

γ

h

γ !

h

γ

h

v2 = gn tanh

v2 = gn +

tanh

v2 =

ρn

n

ρ tanh

n

n

n

h

h

h

→ ∞

→ ∞

→ ∞

n

n

n

ρg 2

n

ρg 2

n

∞ ←

→

deep-water

deep-water

deep-water waves

γ

γ

0

ripples

gravity waves

γ

v2 = g

γ

n +

v2 = gn

ρ

v2 =

n

ρn

On this map, the middle regimes are not our usual middle regimes. Our usual middle regimes represented a particular regime (which was usually of the form 𝛽 ∼ 1). However, on this map, the middle regimes represent the general solution 𝛽 = anything. As an example, look at the bottom, deep-water row of three regimes. The bookend regimes, deep-water gravity waves and deep-water ripples, are easy cases of the middle, deep-water regime. For fun, check the other limiting cases, including that the central regime — which covers waves driven by any mixture of gravity and surface tension and traveling on any depth of water — turns into the other eight regimes in the appropriate limits.

8.4.2 The two-dimensional world of physics Now we'll use the same method to organize the four fundamental branches of physics: classical (Newtonian) mechanics, quantum mechanics, special relativity, and quantum electrodynamics.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.4 Two dimensionless quantities 311

As a first step, which will determine the first axis, let's compare classical mechanics and special relativity. Special relativity is Einstein's theory of motion. It unifies classical mechanics and classical electrodynamics (the theory of radiation), giving a special role to the speed of light 𝑐. This role is popularized in the T-shirt showing Einstein in a policeman's hat. He holds out his arm and palm to make a「Stop」signal and warns:「186 000 miles per second. It's not just a good idea. It's the law!」The speed of light is the universe's speed limit, and special relativity obeys it. In contrast, classical mechanics knows no speed limit. Classical mechanics and special relativity therefore sit on an axis connected by the speed of light. In the limit 𝑐 → ∞, special relativity turns into classical mechanics.

special

c → ∞

classical

relativity

mechanics

For the second axis, we compare one of the two remaining branches of physics — either quantum mechanics or quantum electrodynamics — with either classical mechanics or special relativity. Because quantum electrodynamics, if only from its name, looks frightening, let's select quantum mechanics. We've seen its effect several times: Quantum mechanics contributes a new constant of nature ℏ. This constant appears in the Heisenberg uncertainty principle Δ𝑝Δ𝑥 ∼ ℏ, where Δ𝑝 and Δ𝑥 are a particle's momentum and position uncertainties, respectively. The Heisenberg uncertainty principle restricts how small we can make these uncertainties, and therefore how accurately we can determine the position and momentum.

However, if ℏ were zero, then the uncertainty principle would not restrict anything. We could exactly determine the position and momentum of a particle simultaneously, as we expect in classical mechanics. Classical mechanics is the ℏ → 0 limit of quantum mechanics. Therefore, classical and quantum mechanics are connected on a second, ℏ axis. The map including quantum mechanics therefore has two dimensions.

quantum

mechanics

¯h → 0

special

c → ∞

classical

relativity

mechanics

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

312

8 Easy cases

In this two-dimensional map of physics, one corner sits empty. Furthermore, one branch of physics — quantum electrodynamics — hasn't been considered. We need only a bit of courage to set quantum electrodynamics in the empty corner. Quantum mechanics must be the 𝑐 → ∞ limit of quantum electrodynamics. And it is. Quantum electrodynamics is the result of marrying special relativity (𝑐 < ∞) and quantum mechanics (ℏ > 0). Thus, in the ℏ → 0 limit, quantum electrodynamics turns into special relativity.

quantum

quantum

electrodynamics

c → ∞

mechanics

¯h → 0

¯h → 0

special

c → ∞

classical

relativity

mechanics

What happened to the bookend regimes?

The bookend regimes are here implicitly, because this example introduced a new feature: These axes are not labeled using dimensionless quantities!

Only for a dimensionless quantity can we sensibly distinguish the three regimes ≪ 1, ∼ 1, and ≫ 1. Because 𝑐 and ℏ have dimensions, the only valid comparisons are with zero or with infinity (which are zero and infinity in any system of units). Thus, there are only two regimes on each axis.

The special-relativity–classical-mechanics axis compares 𝑐 with infinity; the quantum-mechanics–classical-mechanics axis compares ℏ with zero.

8.5 Summary and further problems

When the going gets tough, the tough lower their standards. In this chapter, you learned how to do that by studying the easy cases of a problem. This tool is based on the idea that a correct solution works in all cases, including the easy cases. Therefore, look at the easy cases first. Often, we can completely solve a problem simply by understanding the easy cases.

Problem 8.20

Easy cases for the period of a pendulum

Does the period of a pendulum increase, decrease, or remain constant as the amplitude is increased? Decide by selecting an amplitude for which you can easily predict the period.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.5 Summary and further problems 313

Problem 8.21

Pyramid volume

Use easy cases to find the dimensionless prefactor in the volume of a pyramid with height ℎ and a square (𝑏 × 𝑏) base:

𝑉 = dimensionless prefactor × 𝑏2ℎ.

(8.50)

In particular, choose the easy case of a pyramid that, with a few more copies of itself, can be assembled into a cube.

Problem 8.22

Power means

The arithmetic and geometric means are easy cases of a higher-level abstraction: the power mean. The 𝑘th power mean of two positive numbers 𝑎 and 𝑏 is defined by

1/𝑘

𝑀𝑘(𝑎, 𝑏) ≡ (𝑎𝑘 + 𝑏𝑘

2 ) .

(8.51)

You raise the numbers to the 𝑘th power, take the (regular) mean, and then undo the exponentiation by taking the 𝑘th root.

a. What is 𝑘 for an arithmetic mean?

b. What is 𝑘 for the rms (root mean square)?

c. The harmonic mean of 𝑎 and 𝑏 is sometimes written as 2(𝑎 ∥ 𝑏), where ∥ denotes the parallel combination of 𝑎 and 𝑏 (introduced in Section 2.4.3). What is 𝑘 for the harmonic mean?

d. (Surprising!) What is 𝑘 for the geometric mean?

Problem 8.23

Easy case of the compound pendulum

For the compound pendulum of Problem 5.25, what easy case produces an ordinary, noncompound pendulum? Check that, in this limit, your formula for the period from Problem 5.25 behaves correctly.

Problem 8.24

Means in an elliptical orbit

A planetary orbit (an ellipse) has two important orbit

radii: 𝑟min and 𝑟max. The other lengths in the el-b

lipse are power means of these radii (see Problem 8.22 about power means).

a

Sun

rmax

rmin

Match the three power means — arithmetic, geo-

metric, and harmonic — to the three lengths: the l

semimajor axis 𝑎 (which is related to the orbital period), the semiminor axis 𝑏, and the semilatus rectum 𝑙 (which is related to the orbital angular momentum).

Hint: The power-mean theorem says that 𝑀𝑚(𝑎, 𝑏) < 𝑀𝑛(𝑎, 𝑏) if and only if 𝑚 < 𝑛.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

314

8 Easy cases

Problem 8.25

Four regimes in orbital motion

Once in a while, there are four interesting easy-cases regimes. An example is orbits.

The dimensionless parameter 𝛽 that characterizes the type of an orbit is kinetic energy

𝛽 ≡

,

(8.52)

∣ gravitational potential energy ∣

where the absolute value handles a possibly negative potential energy.

A related dimensionless parameter is the orbit eccentricity 𝜖. In terms of the eccentricity, a planet's orbit in polar coordinates is 𝑟(𝜃) =

𝑙

1 + 𝜖 cos 𝜃 ,

(8.53)

where the Sun is at the origin, and 𝑙 is the length scale of the orbit (𝑙 is diagrammed in Problem 8.24). Sketch and classify the four orbit shapes according to their values of 𝛽 and 𝜖 (giving a point value or a range, as appropriate): (a) circle, (b) ellipse, (c) parabola, and (d) hyperbola.

Problem 8.26

Superfluid helium

Helium, when cold, turns into a liquid. When very cold, the liquid turns into a superfluid — a quantum liquid. Here is a dimensionless ratio determining how quantum the liquid is

quantum uncertainty in the position of a helium atom 𝛽 ≡

separation between atoms

.

(8.54)

a. Estimate 𝛽 in terms of the quantum constant ℏ, helium's density 𝜌 (as a liquid), the thermal energy 𝑘B𝑇, and the atomic mass 𝑚He.

b. In the 𝛽 ∼ 1 regime, helium becomes a quantum liquid (a superfluid). Thus, estimate the superfluid transition temperature.

Problem 8.27

Adiabatic atmosphere

The simplest model of the atmosphere is isothermal: The atmosphere has one temperature throughout it. A better approximation, the adiabatic atmosphere, relaxes this assumption and incorporates the adiabatic gas law: 𝑝𝑉𝛾 ∝ 1,

(8.55)

where 𝑝 is atmospheric pressure, 𝑉 is the volume of a parcel of air, and 𝛾 ≡ 𝑐p/𝑐v is the ratio of the two specific heats in the gas. (For dry air, 𝛾 = 1.4.) Imagine an air parcel rising up a mountain. As the parcel rises into air with a lower pressure, it expands, and its volume and temperature change according to a combination of the adiabatic and ideal gas laws.

a. What easy case of 𝛾 reproduces the isothermal atmosphere?

b. For 𝛾 = 1.4 (dry air), will air temperature decrease with, increase with, or be independent of height?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

8.5 Summary and further problems 315

Problem 8.28

Loan payments

A fixed-term, fixed-interest-rate loan has four important parameters: the principal 𝑃 (the amount borrowed), the interest rate 𝑟, the repayment interval 𝜏, and the number of payments 𝑛. The loan is repaid in 𝑛 equal payments over the loan term 𝑛𝜏. Each payment consists of a principal and an interest portion. The interest portion is the interest accumulated on the principal outstanding during the term; the principal portion reduces the outstanding principal.

The dimensionless quantity determining the type of loan is 𝛽 ≡ 𝑛𝜏𝑟.

a. Estimate the payment (the amount per term) in the easy case 𝛽 = 0, in terms of 𝑃, 𝑛, and 𝜏. (The term 𝑛𝜏 and the repayment interval 𝜏 don't vary that much — 𝜏 is usually 1 month and 𝑛𝜏 is somewhere between 3 to 30 years — so 𝛽 ≪ 1 is usually reached by lowering the interest rate 𝑟.) b. Estimate the payment in the slightly harder case where 𝛽 ≪ 1 (which includes the 𝛽 = 0 case). In this regime, the loan is called an installment loan.

c. Estimate the payment in the easy case 𝛽 ≫ 1. In this regime, the loan is called an annuity. (This regime is usually reached by increasing 𝑛.) Problem 8.29

Heavy nuclei

In this problem, you study the innermost electron in an atom such as uranium that has many protons, and analyze a surprising physical consequence of its binding energy. Imagine a nucleus with 𝑍 protons around which orbits one electron. Let 𝐸(𝑍) be the binding energy (the hydrogen binding energy is the case 𝑍 = 1).

a. Show that the ratio 𝐸(𝑍)/𝐸(1) is 𝑍2.

b. In Problem 5.36, you showed that 𝐸(1) is the kinetic energy of an electron moving with speed 𝛼𝑐 where 𝛼 is the fine-structure constant (roughly 10−2). How fast does the innermost electron move around a heavy nucleus with charge 𝑍?

c. When that speed is comparable to the speed of light, the electron has a kinetic energy comparable to its (relativistic) rest energy. One consequence of such a high kinetic energy is that the electron has enough kinetic energy to produce a positron (an anti-electron) out of nowhere; this process is called pair creation.

That positron leaves the nucleus, turning a proton into a neutron as it exits: The atomic number 𝑍 decreases by one. The nucleus is unstable! Relativity therefore places an upper limit to 𝑍. Estimate this maximum 𝑍 and compare it with the 𝑍 for the heaviest stable nucleus (uranium).

Problem 8.30

Minimum wave speed

For deep-water waves, estimate the minimum wave speed in terms of 𝜌, 𝑔, and 𝛾

(the surface tension). Test your prediction in two different ways. (1) Drop a pebble into water, and observe how fast the slowest ripples move outward. (2) Move a toothpick through a pan of water, and look for the fastest speed at which the toothpick generates no waves.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

316

8 Easy cases

Problem 8.31

Surface tension and the size of raindrops A liquid's surface tension, usually denoted 𝛾, is the energy required to create new surface divided by the area of the new surface. For a falling raindrop, surface tension and drag compete: the drag force flattens the raindrop, and surface tension keeps it spherical. If the drop gets too flat, it can lower its surface energy by breaking into smaller and more spherical droplets. The fluid dynamics is complicated, but we don't need to know it. Instead, use competition reasoning (easy cases) to estimate the maximum size of raindrops.

Problem 8.32

Waves driven by surface tension

Imagine a wave with reduced wavelength 𝜆 on the surface of a fluid.

a. Show that the dimensionless ratio

potential energy due to gravity

𝑅 ≡ potential energy due to surface tension

(8.56)

is, after ignoring dimensionless constants, the dimensionless group 𝜌𝑔𝜆2/𝛾

that we used in Section 8.4.1 to distinguish waves driven by gravity from waves driven by surface tension.

b. For water, estimate the critical wavelength 𝜆 at which 𝑅 ∼ 1.

Problem 8.33

Including buoyancy

The terminal speed 𝑣 of a raindrop with radius 𝑟 can be written in the following dimensionless form:

𝑣2

𝑟𝑔 = 𝑓 (𝜌water

𝜌

) .

(8.57)

air

In this problem, you use easy cases of 𝑥 ≡ 𝜌water/𝜌air to guess how buoyancy affects this result. (Imagine that you may vary the density of air or water as needed.) In dimensional analysis, including the buoyant force requires including 𝜌air, 𝑔, and 𝑟 in order to compute the weight of the displaced fluid (which is the buoyant force) — but those variables are already included in the dimensional analysis.

Therefore, including buoyancy doesn't require a new dimensionless group. So it must change the form of the dimensionless function 𝑓 .

a. Before you account for buoyancy: What is the dimensionless function 𝑓 (𝑥)?

Assume spherical raindrops and that 𝑐d ≈ 0.5.

b. What would be the effect of buoyancy if 𝜌water were equal to 𝜌air? This thought experiment is the easy case 𝑥 = 1. Therefore, find 𝑓 (1).

c. Guess the general form of 𝑓 with buoyancy, and thereby find 𝑣 including the effect of buoyancy.

d. Explain physically the difference between 𝑣 without and with buoyancy. Hint: How does buoyancy affect 𝑔?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9

Spring models

9.1 Bond springs

317

9.2 Energy reasoning

321

9.3 Generating sound, light, and gravitational radiation 331

9.4 Effect of radiation: Blue skies and red sunsets 345

9.5 Summary and further problems

353

Our final tool for mastering complexity is making spring models. The essential characteristics of an ideal spring, the transferable abstractions, are that it produces a restoring force proportional to the displacement from equilibrium and stores an energy proportional to the displacement squared. These seemingly specific requirements are met far more widely than we might expect. Spring models thereby connect chemical bonds (Section 9.1), xylophone notes (Section 9.2.3), gravitational radiation (Section 9.3.3), and the colors of the sky and sunsets (Section 9.4).

9.1 Bond springs

A ubiquitous spring is the bond between the electron and proton in hydrogen — the bond that is our model for all chemical bonds. In Section 9.1.1, we'll build a spring model of hydrogen, giving us a physical model for the Young's modulus (Section 9.1.2) and for the speed of sound (Section 9.1.3).

9.1.1 Finding the spring

In Section 8.3.2.2, we saw how hydrogen is a competition between electrostatics and quantum mechanics. When the electron–proton separation 𝑥 is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

318

9 Spring models

much smaller than the Bohr radius 𝑎0, quantum mechanics wins, and the net force on the electron is outward (positive). When the separation is much larger than the Bohr radius, electrostatics wins, and the net force is inward (negative). Between these two extremes, when the separation is the Bohr radius (when 𝑥 = 𝑎0), the force crosses the zero-force line (the 𝑥 axis).

F

This equilibrium point is an easy case that helps us de-repulsion

scribe the bond force simply. We magnify the force curve at the equilibrium point. The curve now looks straight, because any curve looks straight at a large-enough mag-magnification

nification. Equivalently, any curve can be approximated region

a0

x

locally by its tangent line — which is an example of lumping shapes and graphs (Section 6.4) and is where spring attraction

models discard actual information and complexity.

Physically, the straight-line approximation means that, as long as the bond distance differs from 𝑎0 by only a small amount Δ𝑥, the force is linearly proportional to the deviation Δ𝑥. Furthermore, the force curve has a negative slope: A negative deviation produces a positive force, and vice versa. The force therefore opposes the deviation and is a restoring force. A linear restoring force is the force from an ideal spring, so the electron–proton bond is an ideal spring! It has an equilibrium length 𝑎0 at which 𝐹 = 0 and spring constant 𝑘, where −𝑘 is the slope of the force curve.

𝐹 = −𝑘Δ𝑥.

(9.1)

To make this small Δ𝑥 stretch, the required energy Δ𝐸 is Δ𝐸 ∼ force × Δ𝑥.

(9.2)

Because the force varies from 0 to 𝑘Δ𝑥, the typical or characteristic force is comparable to 𝑘Δ𝑥. Then

Δ𝐸 ∼ 𝑘Δ𝑥 ⋅ Δ𝑥 = 𝑘(Δ𝑥)2.

(9.3)

The scaling exponent connecting Δ𝐸 and Δ𝑥 is 2. This quadratic dependence on the displacement is the energy signature of a spring. For small displacements around the equilibrium point (the minimum), the energy-versus-displacement curve is a parabola. (This analysis is a physical version of a Taylor-series approximation.)

Because almost any energy curve has a minimum, almost every system contains a spring. For the bond spring, the energy relation Δ𝐸 ∼ 𝑘(Δ𝑥)2 gives us an estimate of the spring constant 𝑘. Pretend that the energy curve is exactly a parabola, even for large displacements, and increase Δ𝑥 to the bond 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.1 Bond springs

319

size 𝑎 (for hydrogen, 𝑎 is the Bohr radius 𝑎0). That stretch requires an energy Δ𝐸 ∼ 𝑘𝑎2. It is a characteristic energy of the bond, so it must be comparable to the bond energy 𝐸0. Then 𝐸0 ∼ 𝑘𝑎2, and

𝑘 ∼ 𝐸0

𝑎2 .

(9.4)

This relation is an estimate for the spring constant in terms of quantities that we know in other ways: 𝐸0 from the heat of vaporization and 𝑎 from the density and atomic mass. The estimate is often off by a factor of 3 or 10, because of the inaccuracy in extending the parabolic, ideal-spring approximation to displacements comparable to the bond length. But it gives us an order of magnitude that will be useful in subsequent estimates.

9.1.2 Young's modulus

From the spring constant of one bond, we could find the spring constant of a block of material. But as we discussed in Section 5.5.4, a better measure is the Young's modulus 𝑌: It is an intensive quantity, so not dependent on the block's dimensions. The Young's modulus is measured by stretching a block of material with a force 𝐹 at each end.

𝑌 ≡ stress

strain.

(9.5)

The stress is 𝐹/𝐴, where 𝐴 is the block's cross-sectional area. Estimating the strain requires more steps. Fortunately, the estimate breaks into a tree.

To grow it, imagine the block as a bundle of fibers, each a chain of springs (bonds) and masses (atoms). Because strain is the fractional length change, the strain in the block is the strain in each fiber and the strain in each spring of each fiber:

spring extension

strain = bond length 𝑎 .

(9.6)

That's the root of the tree. Here are the internal nodes: spring extension =

force/fiber

spring constant 𝑘 ;

(9.7)

force

fiber =

𝐹

𝑁

.

(9.8)

fibers

The number of fibers will be

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

320

9 Spring models

𝑁

strain

fibers =

cross-sectional area 𝐴

per-fiber cross-sectional area 𝑎2 .

(9.9)

Fa/kA

Here is how the leaf values propagate to the root.

−1

1. The force per fiber becomes 𝐹𝑎2/𝐴.

spring

bond

2. The per-spring extension becomes 𝐹𝑎2/𝑘𝐴.

extension

length

Fa2/kA

a

3. The strain becomes 𝐹𝑎/𝑘𝐴.

Finally, the Young's modulus becomes 𝑘/𝑎:

−1

𝑌 ≡ stress

strain = 𝐹/𝐴

force

𝐹𝑎/𝑘𝐴 = 𝑘𝑎.

(9.10)

spring

fiber

constant

Because 𝑘 ∼ 𝐸0/𝑎2 (Section 9.1.1), 𝑌 ∼ 𝐸0/𝑎3, which k

Fa2/A

confirms with a spring model our dimensional-analysis prediction in Section 5.5.4.

−1

force

Nfibers

F

A/a2

9.1.3 Sound speed in solids and liquids

The spring model of solids and even liquids also gives a physical model for the speed of sound. Start with a fiber of atoms and bonds: m

m

m · · ·

abond

The sound speed is the speed at which a vibration signal travels along the fiber. Let's study the simplest lumped signal: In one instant, the first mass moves to the right by a distance 𝑥, the signal amplitude.

m

m

m · · ·

x

The compressed bond pushes the second atom to the right. When the second atom has moved to the right by the signal amplitude 𝑥, the signal has traveled one bond length. The sound speed is the propagation distance 𝑎bond divided by this one-bond propagation time.

m

m

m · · ·

x

x

What is the propagation time? That is, roughly how much time does the second mass require to move to the right by the signal amplitude 𝑥 ?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.2 Energy reasoning

321

The second mass moves because of the spring force from the first spring.

At 𝑡 = 0, the spring force is 𝑘𝑥. As the mass moves, the spring loses compression, and the force on the second mass falls. So an exact calculation of the propagation time requires solving a differential equation. But lumping will turn the calculation into algebra: Just replace the changing spring force with its typical or characteristic value, which is comparable to 𝑘𝑥.

The force produces a typical acceleration 𝑎 ∼ 𝑘𝑥/𝑚. After a time 𝑡, the mass will have a velocity comparable to 𝑎𝑡 and therefore will have moved a distance comparable to 𝑎𝑡2. This force acts for long enough to move the mass by a distance 𝑥, so 𝑎𝑡2 ∼ 𝑥. Using 𝑎 ∼ 𝑘𝑥/𝑚 gives 𝑘𝑥𝑡2/𝑚 ∼ 𝑥. The amplitude 𝑥 cancels, as it always does in ideal-spring motion. (Thus, the sound speed does not depend on loudness.) The propagation time is then 𝑡 ∼ 𝑚𝑘 .

(9.11)

This characteristic time is just the reciprocal of the natural frequency 𝜔0 =

𝑘/𝑚 . In this time, the signal travels a distance 𝑎bond, so 𝑘𝑎2

𝑐

bond

s ∼ distance traveled

propagation time ∼ 𝑎bond =

𝑚/𝑘

𝑚 .

(9.12)

To make this expression more meaningful, let's convert the numerator and denominator, which are in terms of microscopic (atomic) quantities, into macroscopic quantities. To do so, divide by 𝑎3bond/𝑎3bond in the square root: 𝑘𝑎2

𝑐

bond/𝑎3bond

s ∼

=

𝑘/𝑎bond .

(9.13)

𝑚/𝑎3bond

𝑚/𝑎3bond

The numerator 𝑘/𝑎bond is, as we saw in Section 9.1.2, the Young's modulus 𝑌.

The denominator is the mass per molecular volume, so it is the substance's density 𝜌. Thus, 𝑐s ∼ 𝑌/𝜌 . Our physical, spring model therefore confirms our estimate for 𝑐s in Section 5.5.4 based on dimensions analysis.

9.2 Energy reasoning

The analysis of sound propagation in Section 9.1.3 required estimating the spring forces. Often, however, the forces or their effects are harder to track than are the energies. Then, as you'll see in the next examples, we track the energy and look for the energy signature of a spring: the quadratic dependence of energy on displacement.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

322

9 Spring models

9.2.1 Oscillation frequency of a spring–mass system k

To illustrate the energy method, let's practice on the most fa-m

miliar spring system by finding its natural (angular) oscillation frequency 𝜔0. The method requires finding its kinetic and potential energies. Because these energies vary in complicated ways, we use typical or characteristic energies.

In terms of the amplitude 𝐴0, the typical potential energy is comparable to 𝑘𝐴20. The typical kinetic energy is comparable to 𝑚𝑣2, where 𝑣 is the typical speed of the oscillating mass. This speed is comparable to 𝐴0𝜔0, because the mass travels a distance comparable to 𝐴0 in the characteristic time 1/𝜔0

(which corresponds to 1 radian, or approximately one-sixth of an oscillation period). Thus, the typical kinetic energy is comparable to 𝑚𝐴20𝜔20.

In spring motion, kinetic and potential energy interconvert, so the ratio typical potential energy

typical kinetic energy

(9.14)

should be comparable to 1. This bold conclusion is not limited to spring motion. For example, for gravitational orbits, the ratio, defined carefully using the time-averaged energies, is −2. More generally, the virial theorem says that, with a potential 𝑉 ∝ 𝑟𝑛, the energy ratio will be 2/𝑛.

Equating the typical energies gives an equation for 𝜔0: 𝑘𝐴20

⏟ ∼ 𝑚𝐴20𝜔20.

⏟⏟⏟⏟⏟

(9.15)

𝐸potential

𝐸kinetic

The amplitude 𝐴0 divides out — another illustration that a spring's period is independent of amplitude — giving 𝜔0 ∼ 𝑘/𝑚 . Because the energy ratio is 1 (due to the virial theorem), the missing dimensionless prefactor is 1.

9.2.2 Vibrations of a piano string

From springs to strings: A piano string is a steel wire stretched close to its breaking point — the high tension makes the string's resistance to bending less important and the sound cleaner (as you investigated in Problem 9.17).

When you push a piano key, a hammer bangs on the string and sets it into vibration — whose frequency we'll estimate with a spring model.

For a physical model, start with an unstretched piano string of length 𝐿.

It is a bundle of springs and masses, so it acts like one large spring. Now stretch the string by putting it under tension 𝑇. Then hammer it.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.2 Energy reasoning

323

The hammer gives the atoms vertical velocities. Eventu- y0

ally the kinetic energy turns into potential energy, and 0

λ

the string gets a sinusoidal shape with a wavelength L = 2

𝜆 = 2𝐿 and a small amplitude 𝑦0.

As we did for the simple spring–mass system (Section 9.2.1), we'll find the typical potential energy in the string and the typical kinetic energy in the motion of the string. The potential energy comes from the tension force: The curved string is longer than the equilibrium string, so the tension force has done work on the string by stretching it; the string stores that work as its potential energy. The work done is the force times the distance, so 𝐸potential ∼ 𝑇 × extra length.

(9.16)

string

To estimate the extra length, lump a piece of the curved string as the hypotenuse of a right triangle with base 𝜆,

≈ y0

where 𝜆 ≡ 𝜆/2𝜋. This base represents 1 radian of the θ ≈ y0/n

sine-wave shape. In 1 radian, a sine wave attains almost n

its full height (sin 1 ≈ 0.84), so the height of the triangle is comparable to the amplitude 𝑦0. The triangle then has slope tan 𝜃 ≈ 𝑦0/𝜆.

Because 𝑦0 ≪ 𝜆, the opening angle 𝜃 is small; thus, tan 𝜃 ≈ 𝜃 and 𝜃 ≈ 𝑦0/𝜆.

Using our lumping triangle, we'll find the fractional change 2 /2

in length between the hypotenuse and the base. Fractional

√

2 ≈ 1 + θ

θ

1 + θ

changes, being dimensionless, require less algebra and are 1

more widely applicable than absolute changes. To find the fractional change, rescale the triangle so that the base has unit length; then it has height 𝜃 and hypotenuse 1 + 𝜃2 . Because 𝜃 is small, the square root is, by the binomial theorem, approximately 1 + 𝜃2/2. Thus, the fractional increase in length is comparable to 𝜃2, which is 𝑦20/𝜆2.

The fractional increase applies to the whole string, whose length was 𝐿, so 2

extra length ∼ 𝐿 (𝑦0𝜆) .

(9.17)

The work done in making this much stretch, which is the potential energy in the string, is 𝑇 × extra length, where 𝑇 is the tension, so 2

𝐸potential ∼ 𝑇𝐿 (𝑦0𝜆) .

(9.18)

As befits a spring, even a giant one composed of individual bond springs, the potential energy is proportional to the square of the amplitude 𝑦0.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

324

9 Spring models

Now let's estimate the kinetic energy in the motion of the string. As the string vibrates at the so-far-unknown angular frequency 𝜔, the pieces of the string move up and down with a typical speed 𝜔𝑦0. Thus, 𝐸kinetic ∼ mass × (typical speed)2 ∼ 𝜌𝑏2𝐿

⏟ × 𝜔2𝑦20

⏟,

(9.19)

𝑚

∼𝑣2

where 𝜌 is the string's density and 𝑏 is its diameter. The kinetic energy is also proportional to the squared amplitude 𝑦20 — the other energy signature of a spring. Equating the energies gives the equation for 𝜔: 𝑦 2

𝜌𝑏2 𝐿 𝜔2 𝑦2

0 ⎞

0 ∼ 𝑇 𝐿 ⎛

⎜ ⎟ .

(9.20)

⏟⏟⏟⏟⏟⏟⏟ ⏟⏟ ⎝ 𝜆

⏟⏟ ⎠

⏟⏟⏟

∼𝐸kinetic

∼𝐸potential

The length 𝐿 and the squared amplitude 𝑦20 cancel, leaving 𝜔 = 1

𝑇

𝜆 𝜌𝑏2 .

(9.21)

Despite the extensive use of lumping, this result turns out to be exact — as do many energy-based spring analyses. The circular frequency 𝑓 = 𝜔/2𝜋

has the same structure:

𝑓 = 1

𝑇

𝜆 𝜌𝑏2 .

(9.22)

The wave propagation speed is 𝑓 𝜆 (or 𝜔𝜆), which is just 𝑇/𝜌𝑏2 . Let's check that this speed makes sense. As a first step, it can be rewritten as 𝑣 = 𝑇/𝑏2

𝜌 .

(9.23)

Because the numerator 𝑇/𝑏2 is the pressure (force per area) applied to the ends of the string to put it under the tension 𝑇, the speed of these transverse waves is applied pressure/𝜌 . (They are called transverse waves because the direction of vibration is perpendicular, or transverse, to the direction of travel.) This speed is analogous to the speed of sound that we found in Section 5.5.4, pressure/𝜌, where the pressure was the gas pressure or the elastic modulus. So our speed makes good sense.

How long is the middle-C string on a piano?

We can find the length from the propagation speed and the frequency. The frequency of middle C is roughly 250 hertz. The propagation speed is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.2 Energy reasoning

325

𝑣 = 𝜎𝜌 ,

(9.24)

where 𝜎 is the stress 𝑇/𝑏2. This stress is also 𝜖𝑌, where 𝜖 is the strain (the fractional change in length). Using 𝜎 = 𝜖𝑌 and 𝑐s = 𝑌/𝜌 , 𝑣 = 𝜖𝑌

𝜌 = 𝜖 𝑌𝜌 = 𝜖 𝑐s.

(9.25)

Thus, in terms of the Mach number 𝖬, which measures speeds relative to the full wave speed, transverse waves have a Mach number of 𝜖 .

In steel, 𝑐s ≈ 5 kilometers per second. For piano wire, which is made of high-strength carbon steel, the yield strain is roughly 0.01. However, the string is not stretched quite so far. To provide a margin of safety, the strain 𝜖 is kept to roughly 3×10−3. Then the transverse-wave speed is y

𝑣 ≈ 0.06 × 5

⏟×

⏟103

⏟ m

⏟ s−1 = 300 m s−1.

(9.26)

0

⏟

⏟⏟⏟

𝜖

𝑐s

0

λ

L =

At 𝑓 ≈ 250 hertz, the wavelength is roughly 1.2 meters: 2

𝜆 = 𝑣𝑓 ≈ 300ms−1

250 Hz = 1.2 m.

(9.27)

The wavelength of this lowest, fundamental frequency is twice the string's length, so the string should be 0.6 meters long. To check, I looked into our piano: 0.6 meters is almost exactly the length of the strings set into motion when I play middle C.

9.2.3 Musical notes from bending beams

Another musical device that we can model is a wooden or metal slat in a marimba or xylophone. Using spring models, proportional reasoning, and dimensional analysis, we'll find how the frequency of the slat's musical note depends on its dimensions.

Thus, imagine a thin block of wood of length 𝑙, width 𝑤, and thickness ℎ. It is supported at the two dots (or held at one of them) and tapped in the center. As it vibrates, its shape varies from bent to straight and back to bent. Here are the shapes shown in side view.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

326

9 Spring models

How does the slat's width 𝑤 affect the frequency?

The answer comes from that cheapest kind of experiment, a thought experiment. Using a type of argument developed by Galileo in his study of free fall, lay two identical slats of width 𝑤 side by side. Tapping both slats simultaneously produces the same motion as does tapping a slat of width 2𝑤 (the result of gluing the two slats along the long, thin edge). So the width cannot affect the frequency.

How does the slat's thickness ℎ affect the frequency?

The slat, made of atoms connected by bond springs, acts like a giant spring–mass system. When the slat is straight (the equilibrium position), it has zero potential energy. The energy increases upon bending the slat, which stretches or compresses the bond springs. Thus, the slat resists bending. As befits a giant spring, its resistance to bending can be represented by a stiffness or spring constant 𝑘. (Mechanical engineers define a related quantity called the bending stiffness or the flexural rigidity, which has dimensions of energy times length. Our stiffness is an actual spring constant, with dimensions of force per length.)

Then, as befits a giant spring–mass system, the slat has a vibration frequency comparable to 𝑘/𝑚 , where 𝑚 is its mass. Deciding how the thickness affects the frequency has split into two smaller problems: how the thickness affects the mass and how the thickness affects the stiffness. The first decision is not difficult: The mass is proportional to the thickness.

How does the stiffness 𝑘 depend on thickness?

To answer this proportional-reasoning question, we'll perform the thought experiment of bending each slat by the same vertical deflection 𝑦.

y

y

The stiffness 𝑘 is proportional to the force 𝐹 required to bend the beam (𝐹 = −𝑘𝑦). However, we won't try to understand 𝑘 by finding how the thickness affects 𝐹 itself. Force is a vector, so finding the required force requires carefully bookkeeping many little forces and their directions to know 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.2 Energy reasoning

327

which contributions cancel. Instead, we'll find how the thickness affects the stored energy (the potential energy). As a positive scalar quantity, potential energy has no direction or even sign and is therefore easier to bookkeep.

Because a slat is a big spring, the energy required to produce the vertical deflection 𝑦 is given by

𝐸 ∼ 𝑘𝑦2.

(9.28)

Because 𝑦 is the same for the slats (an easy condition to enforce in a thought experiment), the energy relation becomes the proportionality 𝐸 ∝ 𝑘. To find how 𝑘 depends on thickness, let's redraw the bent slats with a dotted line showing the neutral line (the line without compression or extension): y

y

Above the neutral line, the bond springs along the length of the block get extended; below the neutral line, they get compressed. The compression or extension Δ𝑙 determines the energy stored in each bond spring. Then the stored energy in the whole slat is

𝐸 ∼ 𝐸typical spring × 𝑁springs.

(9.29)

Because 𝐸 ∝ 𝑘,

𝑘 ∝ 𝐸typical spring × 𝑁springs.

(9.30)

To find how 𝐸typical spring depends on the slat's thickness ℎ, break the energy into factors (divide and conquer):

𝐸typical spring ∼ 𝑘bond × (Δ𝑙)2typical spring.

(9.31)

Because the bonds in the two blocks are the same (the blocks differ only in thickness), this relation becomes the proportionality 𝐸typical spring ∝ (Δ𝑙)2typical spring.

(9.32)

Therefore, the stiffness is

𝑘 ∝ (Δ𝑙)2typical spring × 𝑁springs.

(9.33)

To find how (Δ𝑙)typical spring depends on ℎ, compare typical bond springs in the thick and thin blocks — for example, a spring halfway from the neutral line to the top surface. Because the thick block is twice as thick as the thin block, this spring is twice as far from the neutral line in absolute distance.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

328

9 Spring models

The extension is proportional to the distance from the neutral line — as you can guess by observing that it is the simplest scaling relationship that predicts zero extension at the neutral line (or try Problem 9.1). In symbols, (Δ𝑙)typical spring ∝ ℎ.

(9.34)

Furthermore, 𝑁springs is also proportional to ℎ. Therefore, 𝑘 ∝ ℎ3: 𝑘 ∝ (Δ𝑙)2typical spring × 𝑁springs ∝ ℎ3.

(9.35)

Doubling the thickness multiplies the stiffness by eight! The vibration frequency of a slat, considered as a giant spring, is 𝜔 ∼ 𝑘𝑚 .

(9.36)

The mass is proportional to ℎ, so 𝜔 ∝ ℎ:

𝜔 ∝ ℎ3ℎ = ℎ.

(9.37)

Doubling the thickness should double the frequency. To test this prediction, I tapped two pine slats having these dimensions: 30 cm

⏟ × 5 cm

⏟ × { 1 cm (ℎ for the thin slat);

2 cm (ℎ for the thick slat).

(9.38)

𝑙

𝑤

To measure the frequencies, I matched each slat's note to a note on a piano. The thin slat sounded like C one octave above middle C. The thick slat sounded like A in the octave above the thin block. The interval between the two notes is almost an octave or a factor of 2 in frequency.

Now let's extend the analysis to the xylophone slats, which vary not in thickness but in length. This extension bring us to the third scaling question.

How does the slat's length 𝑙 affect the frequency?

We already found the scaling relation between 𝜔 (frequency) and 𝑤 (width), namely 𝜔 ∝ 𝑤0; and between 𝜔 and ℎ (thickness), namely 𝜔 ∝ ℎ. By adding the constraints of dimensional analysis to these scaling relations, we can find the scaling relation between 𝜔 and 𝑙.

The quantities relevant to the frequency 𝜔 are the speed of sound 𝑐s and two of the three dimensions: thickness ℎ and length 𝑙. The third dimension, the width, is not on the list, because the frequency, we already found, is independent of the width. (Instead of the speed of sound, the list could include the Young's modulus 𝑌 and the density 𝜌. As the only two variables containing mass, 𝑌 and 𝑐s would end up combining anyway to make 𝑐s.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.2 Energy reasoning

329

These four quantities, made from two dimensions, make 𝜔 T−1

frequency

two independent dimensionless groups. The first group 𝑐s LT−1 sound speed should be proportional to the goal 𝜔. Because 𝜔 and 𝑐s ℎ L

thickness

are the only quantities containing time, each as T−1, the 𝑙 L

length

group has to contain 𝜔/𝑐s. Making 𝜔/𝑐s dimensionless requires multiplying by a length. Either of the two lengths works. Let's choose 𝑙. (For the alternative, try Problem 9.2). Then the group is 𝜔𝑙/𝑐s.

The other group should not contain the goal 𝜔. Then the only choices are powers of the aspect ratio ℎ/𝑙. If we use ℎ/𝑙 itself, the most general dimensionless statement is

𝜔𝑙

𝑐 = 𝑓 (ℎ

s

𝑙 ) .

(9.39)

The thickness scaling relation, 𝜔 ∝ ℎ, determines the form of 𝑓 , giving 𝜔𝑙

𝑐 ∼ ℎ

s

𝑙 .

(9.40)

Solving for the frequency,

𝜔 ∼ 𝑐sℎ

𝑙2 .

(9.41)

As a scaling relation, 𝜔 ∝ 𝑙−2. Let's check the scaling expo-

𝑙 (cm)

𝑓 (Hz)

nent against experimental data. When my older daughter was C

small, she got a toy xylophone from her uncle. Its (metal) slats 12.2

261.6

D

have the tabulated dimensions and frequencies. The lower and 11.5

293.6

E

higher C notes (C and C') are a factor of

10.9

329.6

2 apart in frequency. If F

the scaling relation is correct, C should come from the longer 10.6

349.2

G

slat, and the ratio of slat lengths should be 10.0

392.0

2. Indeed, the A

measured length ratio is almost exactly

9.4

440.0

2 ≈ 1.414:

B

8.9

493.8

12.2 cm

C'

8.6

523.2

8.6 cm ≈ 1.419.

(9.42)

Problem 9.1

Spring extension versus distance from the neutral line Consider a bent slat as an arc of a circle, and thereby explain why the spring extension is proportional to the distance from the neutral line.

Problem 9.2

Alternative dimensionless group

Repeat the dimensional analysis for the dependence of the oscillation frequency on slat length but using 𝜔ℎ/𝑐s and ℎ/𝑙 as the two independent dimensionless groups.

Do you still conclude that 𝜔 ∝ 𝑙−2?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

330

9 Spring models

Solving the beam differential equation gives the vibration frequency as 𝑓 ≈ 3.56 × 𝑐 ℎ

12

s 𝑙2.

(9.43)

The dimensionless prefactor 3.56/ 12 is almost exactly 1. This example is one of the rare cases where using circular frequency ( 𝑓 ) rather than angular frequency (𝜔) makes the prefactor closer to 1.

For my block of pine, a light wood, 𝜌 ≈ 0.5𝜌water and 𝑌 ≈ 1010 pascals, so 𝑐s = 𝑌𝜌 ∼

1010 Pa

0.5×103 kg m−3 ≈ 4.5 km s−1.

(9.44)

For the thin block, ℎ = 1 centimeter and 𝑙 = 30 centimeters, so 𝑓 ≈ 𝑐 ℎ

s

∼ 450 Hz.

(9.45)

𝑙2 ≈ 4.5×103 m s−1 × 10−2 m

10−1 m2

This estimate is reasonably accurate. The thin block's note was approximately one octave above middle C, with a frequency of roughly 520 hertz.

Problem 9.3

Graphing the data on frequency versus length Check the scaling 𝜔 ∝ 𝑙−2 by plotting the xylophone data for frequency versus length on log–log axes. What slope should the graph have?

Problem 9.4

Finding the stiffness, then the frequency Use dimensional analysis to write the most general dimensionless statement connecting stiffness 𝑘 to a slat's Young's modulus 𝑌, width 𝑤, length 𝑙, and thickness ℎ. What is the scaling exponent 𝑞 in 𝑘 ∝ 𝑤𝑞? Use that scaling relation and 𝑘 ∝ ℎ3

to find the missing exponents in 𝑘 ∼ 𝑌𝑝𝑤𝑞𝑙𝑟ℎ3.

Problem 9.5

Xylophone notes

If you double the width, thickness, and length of a xylophone slat, what happens to the frequency of the note that it makes?

Problem 9.6

Location of the node

Here's how you can predict the location of the node node

CM

node

(where to hold the wood block) using conservation.

Because the bar vibrates freely without an external force, the center of mass (the dot) stays fixed. Approximate the bar's shape as a shallow parabola, find the center of mass (CM), and therefore find the node locations (as a fraction of the bar's length). My daughter's longest xylophone slat is 12.2 centimeters long with holes 2.7 centimeters from the ends. Is that fraction consistent with your prediction?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 331

9.3 Generating sound, light, and gravitational radiation The sound generated by the vibrating wood blocks is an example of the most pervasive spring: radiation. It comes in three varieties. Electromagnetic radiation (or, more informally, light) is produced by an accelerating charge. Sound (acoustic radiation) can be produced simply by a changing but nonmoving charge (such as an expanding or contracting speaker membrane). Therefore, sound is simpler than light — which in turn is simpler than gravitational radiation. Do the easy cases first: We'll first apply spring models to sound (Section 9.3.1). By adding the complexity of motion, we'll extend the analysis to light (Section 9.3.2). Then we'll be ready for the complexity of gravitational radiation (Section 9.3.3).

9.3.1 Acoustic radiation from a charge monopole When we think of radiation, we think first of electromagnetic radiation, which we see (pun intended) everywhere. To analyze sound radiation while benefiting from what we know about electromagnetic radiation, we'll find an analogy between electromagnetic and acoustic radiation — starting at the source of radiation, namely a single charge (a monopole).

The search for the acoustic analog of charge is aided by scaling relations. An electric charge 𝑞 produces a disturbance, the electric field 𝐸. Their connection is 𝐸 ∝ 𝑞. Because the symbols 𝐸 and 𝑞 amplify the mental connection to electromagnetism, let's write the relation between 𝐸 and 𝑞 in words. Words promote a broader, more abstract view not limited to electromagnetism: field ∝ charge.

(9.46)

Another transferable scaling comes from the energy density ℰ (energy per volume) in the field. For an electric field, ℰ ∝ 𝐸2. In words, energy density ∝ field2.

(9.47)

Sound waves move fluid, and motion means kinetic energy. Because the kinetic-energy density is proportional to the fluid velocity squared, the acoustic field could be the fluid velocity 𝑣 itself. Then our first scaling relation, that field ∝ charge, becomes

𝑣 ∝ charge.

(9.48)

Thus, an acoustic charge moves fluid and with a speed proportional to the charge. In contrast to electromagnetism, acoustic charge cannot measure a 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

332

9 Spring models

fixed amount of stuff. For example, it cannot measure simply the volume of a speaker. A fixed volume would produce no motion and no acoustic field.

Instead, acoustic charge must measure a change in the source. As an example of such a change, imagine an expanding speaker. As it expands, it pushes fluid outward. The faster it expands, the faster the fluid moves. To identify the kind of change to measure, let's work backward from the electric field 𝐸 of a point electric charge to the velocity field 𝑣 of a point acoustic charge. The electric field points outward with magnitude 𝐸 =

𝑞

4𝜋𝜖0𝑟2.

(9.49)

Furthermore, the electrostatic 𝜖0 appears in the energy density ℰ = 12𝜖0𝐸2,

(9.50)

whose acoustic counterpart is the kinetic-energy density ℰ = 12𝜌𝑣2.

(9.51)

Because 𝐸 and 𝑣 are analogous, the electrostatic 𝜖0 corresponds, in acoustics, to the fluid density 𝜌. Therefore, in the electric field, let's replace 𝜖0 by 𝜌, 𝐸 by 𝑣, and 𝑞 by acoustic charge to get

acoustic charge

𝑣 =

4𝜋𝜌𝑟2

,

(9.52)

or

acoustic charge = 𝜌𝑣 × 4𝜋𝑟2.

(9.53)

Here, 𝑟 is the distance from the charge, and 𝑣 is the fluid's speed outward (just as the electric field points outward). Then each factor in the acoustic charge has a meaning, as does the product. The factor 𝜌𝑣 is the mass flux: flux

⏟ = density of stuff

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × speed.

⏟

(9.54)

𝜌𝑣

𝜌

𝑣

The factor 4𝜋𝑟2 is the surface area of a sphere of radius 𝑟. Thus, the acoustic charge 𝜌𝑣 × 4𝜋𝑟2 measures the rate at which mass flows out of this sphere.

The acoustic charge itself, at the center of this sphere, must displace mass at this rate. So the acoustic analog of charge is a mass source. The source could be an expanding speaker that directly forces fluid outward. Alternatively, it could be a hose supplying new fluid that forces the old fluid outward. For 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 333

the rate, a convenient notation is ˙

𝑀: The dot represents the time derivative,

turning mass into a mass rate — which is the charge strength.

acoustics

electrostatics

field

fluid velocity 𝑣

electric field 𝐸

source strength (charge)

˙𝑀

𝑞

˙

field from a point source

𝑀 1

𝑞 1

4𝜋𝜌 𝑟2

4𝜋𝜖0 𝑟2

We have found an acoustic field 𝑣 proportional to 𝑟−2. But, as we found in Section 5.4.3, the signature of radiation is that the field is proportional to 𝑟−1. So, we have constructed the acoustic analog of a static electric field and charge, but we have not yet constructed a radiating acoustic system.

Producing radiation requires change — for example, due to a speaker. As a model of a speaker, a small pulsating sphere grows and shrinks in response to the music that it broadcasts. Maybe you put the sphere in a fancy box and slap a brand name on it, but growing and shrinking is still its fundamental operating principle and how it makes sound. A simple model of this change is spring motion — a sinusoidal oscillation in the charge:

˙𝑀 = ˙𝑀0 cos𝜔𝑡.

(9.55)

At 𝑡 = 0, when cos 𝜔𝑡 = 1, the speaker is expanding at its maximum rate, displacing mass at a rate ˙

𝑀0. At 𝑡 = 𝜋/𝜔, the speaker is contracting at its maximum rate. Here is one cycle of its oscillation.

𝜔𝑡 = 0

𝜔𝑡 = 𝜋2

𝜔𝑡 = 𝜋

𝜔𝑡 = 3𝜋

2

𝜔𝑡 = 2𝜋

How much power does this changing acoustic charge radiate?

This analysis requires easy cases and lumping. Easy cases will help us find the velocity field; because the charge and field are changing, lumping will help us find the resulting energy flow. The easiest case is near the charge: News about the changes requires no time to arrive, so the fluid responds to a changing ˙

𝑀 instantaneously. In this region, we know 𝑣:

˙

𝑣 = 𝑀

4𝜋𝜌𝑟2

(9.56)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

334

9 Spring models

Far from the charge, however, the fluid cannot know right away that ˙

𝑀 has

changed. But what does「far」mean? As we learned in Chapter 8, easy cases are defined by a dimensionless parameter, so the distance from the source is not enough information by itself to decide between near and far.

The decision needs a comparison length. This length is based on how the news is transmitted: It travels as a sound wave, so it has speed 𝑐s. Because the change happens at a rate 𝜔 (the angular frequency of the charge oscillation), the characteristic timescale of the changes is 𝜏 = 1/𝜔. In this time, the charge changes significantly, and the news has traveled a distance 𝑐s𝜏

or ∼ 𝑐s/𝜔. This distance is the reduced wavelength 𝜆 of the sound wave produced by the speaker (𝜆 ≡ 𝜆/2𝜋).

Therefore,「near the charge」(in the near field or zone) means 𝑟 ≪ 𝜆.「Far from the charge」(in the far field or

∼ n

r

the radiation field or zone) means 𝑟 ≫ 𝜆. For example, near

far

charge

zone

zone

for middle C ( 𝑓 ≈ 250 hertz, and 𝜆 ≈ 1.3 meters), near r n

r n

and far are measured relative to 20 centimeters.

With 𝜆 as the comparison length, the dimensionless ratio determining whether 𝑟 is small or large is 𝑟/𝜆, which is 𝑟𝜔/𝑐s. At the boundary between the near and far zones, 𝑟 ∼ 𝜆.

In the lumping model, the velocity field in the near zone follows the changes in ˙

𝑀 instantly, with energy flowing outward and inward in rhythm with the speaker's motion. At the zone boundary, at 𝑟 ∼ 𝜆, the velocity field changes its character. It becomes a signal describing those changes, and this signal, a sound wave, travels outward at the speed of sound 𝑐s.

To estimate the power carried by this signal — which is the power radiated by the source — start with the power per area, which is energy flux. At the zone boundary, 𝑟 ∼ 𝜆, so

energy flux = energy density (at 𝑟 ∼ 𝜆)

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ × propagation speed.

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ (9.57)

𝜌𝑣2/2

𝑐s

To estimate the energy density at 𝑟 ∼ 𝜆, return to the lumping approximation — that the velocity field tracks the changes in ˙

𝑀 throughout the

near zone — and gather enough courage to extend the assumption. Assume that the instantaneous tracking happens all the way out to the zone boundary — that is, it applies not just when 𝑟 ≪ 𝜆 but even when 𝑟 ∼ 𝜆 (where the field abruptly changes its character and becomes a radiation field).

In this approximation, the velocity field at 𝑟 ∼ 𝜆 is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 335

˙

𝑣 ∼ 𝑀

4𝜋𝜌𝜆2 ,

(9.58)

so the energy density ℰ ∼ 𝜌𝑣2/2 becomes

˙

2

ℰ ∼ 1

𝑀 ⎞

2𝜌 ⎛⎜

⎟ .

(9.59)

⎝4𝜋𝜌𝜆2 ⎠

The radiated power 𝑃 is the energy flux times the surface area of the sphere enclosing the near zone:

˙

2

𝑃 ∼ 4𝜋𝜆2 ×

1

𝑀 ⎞⎟

×

𝑐s.

(9.60)

⏟

2𝜌 ⎛⎜

⏟ ⎝4𝜋𝜌𝜆2

⏟⏟⏟⏟ ⎠

⏟⏟

⏟

surface area

energy density 𝜌𝑣2/2

propagation speed

Using 𝜆 = 𝑐s/𝜔, the power radiated by our acoustic monopole becomes

˙

𝑃

𝑀2𝜔2

monopole = 1

8𝜋 𝜌𝑐 .

(9.61)

s

Despite the absurd number of lumping approximations, this result is exact!

Let's use it to estimate the acoustic power output of a tiny speaker.

How much power is radiated by an 𝑅 = 1 centimeter speaker whose radius varies by ± 1 millimeter at 𝑓 = 1 kilohertz (roughly two octaves above middle C)?

±1 mm

This calculation becomes slightly simpler if we replace ˙

𝑀 by 𝜌 ˙𝑉,

where ˙𝑉 is the rate of volume change. (In acoustics, ˙𝑉 is often called the source strength 𝑄 — for example, in the classic work The Physics 1 cm

of Musical Instruments [15, p. 172]. However, for the sake of the analogy with electromagnetism, it is more consistent to make the source strength ˙

𝑀 rather than ˙𝑉.) In terms of ˙𝑉,

𝑃

𝜌 ˙𝑉2𝜔2

monopole = 1

8𝜋 𝑐

.

(9.62)

s

Here, ˙𝑉 = ˙𝑉0 cos 𝜔𝑡, where ˙𝑉0 is the amplitude of the oscillations in ˙𝑉.

Therefore, the power 𝑃monopole is also oscillating. By symmetry, the average value of cos2𝜔𝑡 is 1/2 (Problem 3.38), so the time-averaged power is one-half the maximum power:

𝜌 ˙𝑉2

𝑃

0𝜔2

avg =

1

16𝜋 𝑐

.

(9.63)

s

To find the amplitude ˙𝑉0, write ˙𝑉 in terms of the speaker dimensions: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

336

9 Spring models

˙𝑉 = 4𝜋𝑅2

⏟ × 𝑣surface,

(9.64)

surface area

where 𝑣surface is the outward speed of the speaker membrane. Because the surface is oscillating like a mass on a spring with amplitude 𝐴0, its maximum velocity is 𝐴0𝜔 and its time variation is 𝑣surface(𝑡) = 𝐴0𝜔 cos 𝜔𝑡.

(9.65)

Then

˙𝑉 = 4𝜋𝑅2𝐴0𝜔 cos𝜔𝑡.

(9.66)

The corresponding amplitude is everything except the cos 𝜔𝑡:

˙𝑉0 = 4𝜋𝑅2𝐴0𝜔.

(9.67)

The radiated power is then

˙𝑉20

⏞⏞⏞⏞⏞⏞⏞

𝜋𝜌𝑅4𝐴2

𝑃

𝜌 (4𝜋𝑅2𝐴0𝜔)2 𝜔2

0𝜔4

avg =

1

16𝜋

𝑐

=

.

(9.68)

s

𝑐s

By multiplying 𝑃avg by 𝑐3s/𝑐3s, the power can be written in terms of the dimensionless ratio 𝑅𝜔/𝑐s, which is also 𝑅/𝜆:

4

4

𝑃 = 𝜋𝜌𝑐3s𝐴20 (𝑅𝜔

𝑐 ) = 𝜋𝜌𝑐3s𝐴20 (𝑅 .

(9.69)

s

𝜆 )

Physically, 𝑅/𝜆 is the dimensionless speaker size (measured relative to 𝜆).

The scaling exponent of 4 tells us that the radiated power depends strongly on the dimensionless size of the speaker. As a result, big speakers (large 𝑅) are loud; and long wavelengths (low frequencies) require big speakers.

For this speaker, the radius is 𝑅 is 1 centimeter, the surface-oscillation amplitude 𝐴0 is 1 millimeter, and 𝑓 is 1 kilohertz. So the wavelength of the sound is roughly 30 centimeters (𝜆 = 𝑐s/ 𝑓 ), and 𝜆 is roughly 5 centimeters.

Then the dimensionless speaker size 𝑅/𝜆 is approximately 0.2, and 𝑃avg ≈ 3

⏟ × 1 kg m−3

⏟⏟⏟⏟⏟ × (3×102 m s−1)3

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × (10−3 m)2

⏟⏟⏟⏟⏟ × 0.24.

⏟

(9.70)

𝜋

𝜌

𝑐3s

𝐴20

(𝑅/𝜆)4

To evaluate this power mentally, divide and conquer as usual: 1. Units. They are watts:

kg m−3 × m3 s−3 × m2 = kg m2 s−3 = W.

(9.71)

2. Powers of ten. They contribute 10−4: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 337

106

⏟ × 10−6

⏟ × 10−4

⏟ = 10−4.

(9.72)

from 𝑐3s

from 𝐴20

from (𝑅/𝜆)4

So far, the power is 10−4 watts.

3. Remaining numerical factors. They are 3

⏟ × 33

⏟ ×

24.

⏟

(9.73)

from 𝜋 from 𝑐3 from

s

(𝑅/𝜆)4

Because 24 = 16 and 3×33 is (32)2 or roughly 102, the remaining numerical factors contribute roughly 1600. Let's round it to 2000.

Then the power is roughly 2000 × 10−4 or 0.2 watts.

Does that power represent a loud or a soft sound?

It depends on how close you stand to the speaker. If you are 1 meter away, the 0.2 watts are spread over a sphere of area 4𝜋 × (1 meter)2, or roughly 10 square meters. Then the power flux is roughly 0.02 watts per square meter. In decibels, which is the more familiar measure of loudness (introduced in Problem 3.10), this power flux corresponds to just over 100 decibels, which is very loud, almost enough to cause pain.

What radius fluctuations would produce a barely audible, 0-decibel flux?

Shrinking the flux to 0 decibels, which is a drop of 100 decibels, is a drop of a factor of 1010 in energy flux and power. Because the energy flux is proportional to 𝐴20, 𝐴0 must fall by a factor of 105: from 10−3 meters to 10−8 meters. Thus, 10-nanometer fluctuations in a small speaker's radius are (barely) enough to produce an audible sound. The human ear has an amazing dynamic range and sensitivity.

9.3.2 Electromagnetic radiation from a dipole In the spirit of laziness, let's transfer, by analogy, the radi- acoustics electrostatics ated power from acoustic to electromagnetic radiation. In 𝜌

𝜖0

Section 9.3.1, we developed the analogy between acoustics 𝑣

𝐸

and electrostatics. Using it, the acoustic radiated power, 𝑐s

𝑐

˙𝑀2𝜔2

˙𝑀

𝑞

𝑃monopole = 1

8𝜋 𝜌𝑐 ,

(9.74)

s

implies an electromagnetic radiated power of 𝑞2𝜔2/8𝜋𝜖0𝑐.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

338

9 Spring models

Alas, this conjecture has three problems. First, if it represents the power radiated by an oscillating charge — moving, say, on a spring oscillating with frequency 𝜔 — then its acceleration is ∝ 𝜔2, so the radiated power is proportional to the acceleration. However, we learned from dimensional analysis (Section 5.4.3) that the power had to be proportional to the acceleration squared. Second, the power should depend on the amplitude of the motion, which is a length, yet the proposed power contains no such length.

These two problems are symptoms of the third problem, that transferring the acoustic analysis to electromagnetism has made an illegal situation. A single changing electromagnetic charge 𝑞(𝑡) violates charge conservation: If 𝑞(𝑡) is increasing, from where would the new charge come?

This question suggests the valid physical model, that the new charge +

comes from a nearby charge. As a model of this flow, imagine a pair of opposite, nearby charges. As the positive charge flows to the negative flow

charge, the two charges swap places; and vice versa. This model is an oscillating dipole. Here is a full cycle of its oscillation.

−

+

−

+

−

+

−

𝜔𝑡 = 0

𝜔𝑡 = 𝜋

𝜔𝑡 = 2𝜋

If the charges are ±𝑞 and their separation is 𝑙, then 𝑞𝑙 is called their dipole +q moment 𝑑. Here, the time-varying dipole moment is 𝑑(𝑡) = 𝑑0 cos 𝜔𝑡, where 𝑑

l

0 is the amplitude of the oscillations in the dipole moment. To estimate the power radiated, we'll reuse the structure from acoustics,

−q

𝑃 ∼ 4𝜋𝑟2 ×

1

×

𝑐,

(9.75)

⏟

2𝜖0𝐸2

⏟

⏟

surface area

energy density propagation speed

and evaluate it at the near-field–far-field boundary (𝑟 ∼ 𝜆). The only change from acoustics is that the electric field 𝐸 is not the field from a single point charge (a monopole source) but rather from two opposite charges (a dipole source). Let's evaluate their field at the position of a test charge at 𝑟 ∼ 𝜆.

The two charges (the monopoles) contribute slightly different electric fields 𝐄+ and 𝐄−. Because these fields are vectors, adding them correctly requires tracking their individual components. Let's therefore make the lumping approximation that we can add the vectors using only their magnitudes: 𝐸dipole ≈ 𝐸+ − 𝐸−.

(9.76)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 339

E+

This approximation would be exact if the vectors lay along the test

same line — which they would if the dipole were an ideal di-charge

pole, with zero separation (𝑙 = 0). By making this approximation even for this nonideal dipole, we will obtain an important E−

and transferable insight about the field of a dipole.

Because the distances from the test charge to the monopoles +q are almost identical, the two fields 𝐸+ and 𝐸− have almost the l

same magnitude. Therefore, the difference 𝐸+ − 𝐸− is almost zero. (The key word is almost. If the difference were exactly −q zero, there would be no light and no radiation.) Let's approximate the difference using a further lumping approximation.

The dipole field is the difference Δ𝐸 = 𝐸(𝑟+) − 𝐸(𝑟−), where 𝐸(𝑟) is the monopole field. The difference is approximately E+

Δ𝐸

⏟ ≈ 𝐸′(𝑟)

⏟ × Δ𝑟

⏟,

(9.77)

rise

slope

run

E(r)

∆E

where Δ𝑟 = 𝑟− − 𝑟+. (This formula ignores a minus sign, but we E

are interested only in the magnitude of the field, so the sign doesn't

−

∆r

matter.) In Leibniz's notation, the slope 𝐸′(𝑟) is also 𝑑𝐸/𝑑𝑟. Using r+

r−

the lumping approximation of Section 6.3.4 (which I remember as 𝑑 ∼ 𝑑), the 𝑑s cancel and 𝑑𝐸/𝑑𝑟, and therefore 𝐸′(𝑟), is roughly 𝐸/𝑟.

The trickiest factor is Δ𝑟, which is 𝑟− − 𝑟+. It depends on the charge separation 𝑙 and on the position of the test charge relative to the dipole's orientation. When the test charge is directly above the dipole (at the north pole), Δ𝑟 is just the charge separation 𝑙. When the test charge is at the equator, Δ𝑟 = 0. With our lumping approximation, Δ𝑟 is comparable to 𝑙.

Then the difference Δ𝐸, which is the dipole field, becomes 𝐸dipole ∼ 𝐸monopole × 𝑙𝑟.

(9.78)

The 1/𝑟 factor comes from differentiating the monopole field. The factor of 𝑙, the dipole size, turns the derivative of the field back into a field and makes the overall operation dimensionless: Making a dipole from two monopoles dimensionlessly differentiates the monopole field.

Because the energy density ℰ in the electric field is proportional to 𝐸2, and the power radiated is proportional to the energy density, the power is 2

𝑃dipole ∼ 𝑃monopole ( 𝑙𝑟) .

(9.79)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

340

9 Spring models

In evaluating the radiated power, what 𝑟 should we use?

The power radiated is determined by the energy density at the boundary between the near- and far-field regions: at 𝑟 ∼ 𝑐/𝜔. With that substitution, 2

𝑃

𝑞2𝜔2

𝑞2𝑙2𝜔4

dipole ∼

1

8𝜋 𝜖

× ( 𝑙

= 1

0𝑐

⏟⏟⏟⏟⏟

𝑐/𝜔)

8𝜋 𝜖0𝑐3 .

(9.80)

𝑃monopole

With a 1/6𝜋 instead of 1/8𝜋, this result is exact. Furthermore, if the source is a single accelerating charge, instead of a charge flow, then its acceleration is comparable to 𝑙𝜔2, and 𝑃dipole ∼ 𝑞2𝑎2/𝜖0𝑐3, which is now consistent with what we derived in Section 5.4.3 using dimensional analysis.

In terms of the dipole moment 𝑑 = 𝑞𝑙,

𝑃

𝜔4𝑑2

dipole = 1

6𝜋 𝜖0𝑐3 .

(9.81)

Dipole radiation is the strongest kind of electromagnetic radiation. In Section 9.4, we'll use the dipole power to explain why the sky is blue and a sunset red.

Problem 9.7

Lifetime of hydrogen if it could radiate

Assuming that the ground state of hydrogen could radiate as an oscillating dipole (because of the orbiting electron), estimate the time 𝜏 required for it to radiate its binding energy 𝐸0. The ground state of hydrogen is protected by quantum mechanics — there is no lower-energy state to go to — but many of hydrogen's higher-energy states have a lifetime comparable to 𝜏.

9.3.3 Gravitational radiation from a quadrupole Having started with acoustics and practiced with electromagnetics, we can extend our analysis of radiation to gravitational waves — without solving the equations of general relativity. In acoustics, radiation could be produced by a monopole (a point charge). In electromagnetics, radiation could be produced by a dipole but not by a monopole. Building a dipole requires charges of two signs. Because the gravitational equivalent of charge is mass, which comes in one sign, there is no way to make a gravitational dipole.

Therefore, gravitational radiation requires a quadrupole. A quadrupole is to a dipole what a dipole is to a monopole. It is two nearby dipoles with opposite strengths — so that their fields almost cancel.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 341

−

An example is an oblate sphere. Relative to a sphere, it is fat at the equator (represented by the + signs) and thin at 1

the poles (represented by the − signs). One plus–minus dipole

+

+

pair forms one dipole. The other plus–minus pair forms 2

the second dipole. They have the same magnitude but dipole

point in opposite directions. As the sphere shifts to pro-

−

lateness (tall and thin), the signs of the charges flip, as do the directions of the dipoles.

Just as the dipole field is the dimensionless derivative of the monopole field (Section 9.3.2), the quadrupole field is the dimensionless derivative of the dipole field. Thus, if the pulsating object has size 𝑙, so that the two dipoles are separated by a distance comparable to 𝑙, then at the boundary between the near and far fields (at 𝑟 ∼ 𝑐/𝜔), the fields are related by 𝐸quadrupole ∼ 𝐸dipole × 𝑙

𝑐/𝜔 = 𝐸dipole × 𝜔𝑙

𝑐 .

(9.82)

The radiated powers are related by the square of the extra factor: 2

𝑃quadrupole ∼ 𝑃dipole × (𝜔𝑙

𝑐 ) .

(9.83)

That dimensionless ratio in parenthesis has a physical interpretation. Its numerator 𝜔𝑙 is the characteristic speed of the objects making the field. Its denominator 𝑐 is the wave speed. Their ratio is the Mach number 𝖬, so 𝜔𝑙/𝑐 is the characteristic Mach number of the sources. In terms of 𝖬, 𝑃quadrupole ∼ 𝑃dipole × 𝖬2.

(9.84)

For the radiated power from an electromagnetic dipole, we found an analogous relation:

𝑃dipole ∼ 𝑃monopole × 𝖬2.

(9.85)

In general,

𝑃2𝑚-pole ∼ 𝑃monopole × 𝖬2𝑚,

(9.86)

where a 20-pole is a monopole, a 21-pole is a dipole, and so on.

With the analogy between electrostatics and gravity (from Section 2.4.2), we can convert the power radiated by an electromagnetic dipole to the power radiated by a gravitational dipole, if it existed. Then we just adjust for the difference between a dipole and a quadrupole. From the analogy, the electrostatic field 𝐸 is analogous to the gravitational field 𝑔, and electrostatic 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

342

9 Spring models

charge 𝑞 is analogous to mass 𝑚. Finally, because 𝑔 = 𝐺𝑚/𝑟2 is analogous to 𝐸 = 𝑞/4𝜋𝜖0𝑟2, the electrostatic combination 1/4𝜋𝜖0 is analogous to Newton's constant 𝐺.

For electromagnetic dipole radiation, the power radiated is 𝑃

𝑞2𝑙2𝜔4

dipole =

1

6𝜋𝜖0 𝑐3 .

(9.87)

Replacing 1/4𝜋𝜖0 with 𝐺 and 𝑞 with 𝑚, but leaving 𝑐 alone because gravitational waves also travel at the speed of light (a limitation set by relativity), the power radiated by a gravitational dipole, if it existed, would be 𝑃dipole ∼ 𝐺𝑚2𝑙2𝜔4

𝑐3

.

(9.88)

Changing from dipole to quadrupole radiation adds a factor of 𝜔𝑙/𝑐 to the field and (𝜔𝑙/𝑐)2 to the power, so

𝑃quadrupole ∼ 𝐺𝑚2𝑙4𝜔6

𝑐5

.

(9.89)

Let's use this formula to estimate the gravitational power radiated by the Earth–Sun system. We'll divide the system into two sources. One source is the Earth as it rotates around the system's center of mass (CM). The other source is the Sun as it rotates around the system's center of mass.

CM

CM

CM

Sun

E

=

E

+

Sun

(9.90)

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

⏟⏟⏟⏟⏟⏟⏟

⏟⏟⏟⏟⏟

system

Earth as source

Sun as source

Which source generates more gravitational radiation?

The two sources share the constants of nature 𝐺 and 𝑐. Because they orbit around the center of mass like a spinning dumbbell, they also share the angular velocity 𝜔. Therefore, the power simplifies to a proportionality without 𝐺, 𝑐, or 𝜔:

𝑃quadrupole ∝ 𝑚2𝑙4,

(9.91)

where 𝑚 is the mass of the object (either the Earth or Sun) and 𝑙 is its distance from the center of mass. Furthermore, 𝑚𝑙 is shared, because the center of mass is defined as the point that makes 𝑚𝑙 the same for both objects.

𝑚Earth × 𝑙Earth–CM distance = 𝑀Sun × 𝑙Sun–CM distance.

(9.92)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.3 Generating sound, light, and gravitational radiation 343

By factoring out two powers of 𝑚𝑙 and discarding them, the proportionality further simplifies from 𝑃quadrupole ∝ 𝑚2𝑙4 to 𝑃quadrupole ∝ 𝑙2. The Earth, with the longer lever arm 𝑙, generates most of the gravitational wave energy.

Equivalently, we can factor out four powers of 𝑚𝑙 and get 𝑃quadrupole ∝ 𝑚−2; the Earth, with the smaller mass, still wins. So, 𝐺𝑚2

𝑃

Earth𝑙4𝜔6

quadrupole ∼

𝑐5

.

(9.93)

As the last simplification before evaluating the power, let's eliminate the angular frequency 𝜔. For motion in a circle of radius 𝑙, the centripetal acceleration is 𝑣2/𝑙 (as we found in Section 5.1.1). In terms of the angular velocity, this acceleration is 𝜔2𝑙. It is produced by the gravitational force 𝐹 ≈ 𝐺𝑀Sun𝑚Earth

𝑙2

(9.94)

(approximately, because 𝑙 is slightly smaller than the Earth–Sun distance).

The resulting centripetal acceleration is 𝐹/𝑚Earth or 𝐺𝑀Sun/𝑙2, so 𝜔2𝑙 = 𝐺𝑀Sun

𝑙2 .

(9.95)

Using this relation to replace (𝜔2𝑙)3 in 𝑃quadrupole with (𝐺𝑀Sun/𝑙2)3 gives 𝐺4𝑚2

𝑃

Earth𝑀3Sun

quadrupole ∼

𝑙5𝑐5

.

(9.96)

The power based on a long and difficult general-relativity calculation is almost the same:

𝑃

𝐺4

quadrupole ≈ 32

5 𝑙5𝑐5 (𝑚Earth𝑀Sun)2(𝑚Earth + 𝑀Sun).

(9.97)

With the approximation that 𝑚Earth + 𝑀Sun ≈ 𝑀Sun, the only difference between our estimate and the exact power is the dimensionless prefactor of 32/5. Including that factor and approximating 𝑚Earth + 𝑀Sun by 𝑀Sun, 𝐺4𝑚2

𝑃

Earth𝑀3Sun

quadrupole ≈ 32

5

𝑙5𝑐5

.

(9.98)

To avoid exponent whiplash and promote formula hygiene, let's rewrite the power using a dimensionless ratio, by pairing another velocity with the 𝑐 in the denominator. It would also be helpful to get rid of 𝐺, which seems like a random, meaningless value. To fulfill both wishes, we again equate the two ways of finding the Earth's centripetal acceleration, as the acceleration produced by the Sun's gravity and as the circular acceleration 𝑣2/𝑙: 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

344

9 Spring models

𝐺𝑀Sun

𝑙2

= 𝑣2𝑙.

(9.99)

Therefore, 𝐺𝑀Sun/𝑙 = 𝑣2 and

𝐺4𝑀4Sun = 𝑣8.

(9.100)

𝑙4

That substitution gives

𝑚2

𝑃

Earth 𝑣8

quadrupole ≈ 32

5 𝑀Sun 𝑙𝑐5 .

(9.101)

The ratio 𝑣5/𝑐5 is 𝖬5, where 𝖬 is the Mach number of the Earth (its orbital velocity compared to the speed of light). Of the three remaining powers of 𝑣, one power combines with 𝑙 in the denominator to give back the angular velocity 𝜔 = 𝑣/𝑙. The remaining two powers of 𝑣 combine with one power of 𝑚Earth to give (except for a factor of 2) the orbital kinetic energy of the Earth. The remaining masses make the Earth–Sun mass ratio 𝑚Earth/𝑀Sun.

Therefore, in a more meaningful form, the power is 𝑃

𝑚Earth

quadrupole ≈ 32

5 𝑀

𝖬5 × 𝑚Earth𝑣2 𝜔.

(9.102)

Sun

In this processed form, the dimensions are more obviously correct than they were in the unprocessed form. The factors before the × sign are all dimensionless. The factor of 𝑚Earth𝑣2 is an energy. And the factor of 𝜔 converts energy into energy per time — which is power.

Now that we have reorganized the formula into meaningful chunks, we are ready to evaluate its factors.

1. The mass ratio is 3×10−6:

𝑚Earth

𝑀

≈ 6×1024 kg = 3×10−6.

(9.103)

Sun

2×1030 kg

2. The Mach number 𝖬 ≡ 𝑣/𝑐 turns out to have a compact value. The Earth's orbital velocity 𝑣 is 30 kilometers per second (Problem 6.5): 𝑣 = circumference

orbital period ≈ 2𝜋 × 1.5 × 1011 m = 3 × 104 m s−1, (9.104)

𝜋 ×107 s

which uses the estimate from Section 6.2.2 of the number of seconds in a year. The corresponding Mach number is 10−4: 𝖬 ≡ 𝑣𝑐 = 3×104ms−1 = 10−4.

(9.105)

3×108 m s−1

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.4 Effect of radiation: Blue skies and red sunsets 345

3. For the factor 𝑚Earth𝑣2, we know 𝑚Earth and have just evaluated 𝑣. The result is 6×1033 joules:

6×1024 kg

⏟⏟⏟⏟⏟ × 109 m2 s−2

⏟⏟⏟⏟⏟ = 6×1033 J.

(9.106)

𝑚Earth

𝑣2

4. The final factor is the Earth's orbital angular velocity 𝜔. Because the orbital period is 1 year, 𝜔 = 2𝜋/1 year, or

𝜔 ≈

2𝜋

= 2×10−7 s−1.

(9.107)

𝜋 ×107 s

With these values,

𝑃quadrupole ≈ 32

5 × 3×10−6

⏟⏟⏟⏟⏟ × 10−20

⏟ × 6×1033 J

⏟⏟⏟⏟⏟ × 2×10−7 s−1.

⏟⏟⏟⏟⏟⏟⏟ (9.108)

𝑚Earth/𝑀Sun

𝖬5

𝑚Earth𝑣2

𝜔

The resulting radiated power is about 200 watts. At that rate, the Earth's orbit will not soon collapse due to gravitational radiation (Problem 9.8).

Quadrupole radiation depends strongly on the Mach number 𝑣source/𝑐, and the Earth's Mach number is tiny. However, when a star gets captured by a black hole, the orbital speed can be a large fraction of 𝑐. Then the Mach number is close to 1 and the radiated power can be enormous — perhaps large enough for us to detect on distant Earth.

Problem 9.8

Energy loss through gravitational radiation In terms of a gravitational system's Mach number and mass ratio, how many orbital periods are required for the system to lose a significant fraction of its kinetic energy? Estimate this number for the Earth–Sun system.

Problem 9.9

Gravitational radiation from the Earth–Moon system Estimate the gravitational power radiated by the Earth–Moon system. Use the results of Problem 9.8 to estimate how many orbital periods are required for the system to lose a significant fraction of its kinetic energy.

9.4 Effect of radiation: Blue skies and red sunsets We have developed almost all the pieces and tools to understand our final two phenomena: blue skies (Section 9.4.1) and red sunsets (Section 9.4.2).

The only missing piece is the amplitude of a spring–mass system when it is driven by an oscillating force. We'll build that piece where it is first needed, and then put all the pieces together.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

346

9 Spring models

9.4.1 Skies are blue

The light that we see from a clear sky is dipole radiation

−

scattered from air molecules (on the Moon, with no atmosphere, there are no blue skies). Plenty of sunlight sunlight

+

does not get affected by air molecules, but unless we look at the sun, which is almost always very hazardous, the scattered

direct sunlight does not reach our eye. (The exception is light

just at sunset, and in Section 9.4.2 we'll use the exception to help explain why sunsets are red.)

The analysis makes the most sense as a causal sequence from the sunlight to this scattered radiation. Sunlight is an oscillating electric field. The electric field exerts a force on the charged particles in an air molecule (say, in N2). The charged particles, the electrons and protons, form spring–mass systems, and the electric force accelerates the masses. Accelerating charges radiate, which is the radiation that reaches our eye. By quantifying the steps in the sequence from sunlight to scattered radiation, we'll see why the scattered radiation looks blue.

1. Electric field of the sunbeam. Sunlight contains many colors of light, each simple to describe as an electric field (divide and conquer!): 𝐸(𝜔) = 𝐸0(𝜔) cos 𝜔𝑡,

(9.109)

where 𝜔 is the angular frequency corresponding to that color. For example, for red light, 𝜔 is 3 × 1015 radians per second. The amplitude 𝐸0(𝜔) depends on the intensity of the color in sunlight, so 𝐸(𝜔) is a distribution over 𝜔, and it and the amplitude 𝐸0(𝜔) have dimensions of field per frequency. However, as a simple lumping approximation, think of seven separate fields, one for each color in the color mnemonic Roy G. Biv: red, orange, yellow, green, blue, indigo, and violet.

For the color of the sky, what matters is the relative distribution of colors in the sunbeam and how that relative distribution is different in scattered light. Therefore, let's do our calculations in terms of an unknown 𝐸0 and, in the spirit of proportional reasoning, determine the dependence of 𝐸0 on 𝜔 in the scattered light.

2. Force on the charged particles. The electric field produces a force on the electrons and protons in an air molecule. Using 𝑒 for the electron charge and ignoring signs,

𝐹 = 𝑒𝐸 = 𝑒𝐸0 cos 𝜔𝑡,

(9.110)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.4 Effect of radiation: Blue skies and red sunsets 347

3. Amplitude of the motion of the charged particles. Because protons are much heavier than an electrons, the electrons move faster and farther than the protons and produce most of the scattered radiation. Therefore, let's assume that the protons are fixed and analyze the motion of an electron.

The electron, which is connected to its proton by k

a spring, is driven by the oscillating force proton

m

𝐹. For-

e

F

tunately, we do not need to solve for the motion in general, because we can use easy cases based on the ratio between the driving frequency 𝜔 and the system's natural frequency 𝜔0 (which is 𝑘/𝑚e, where 𝑘 is the bond's spring constant).

The three regimes are then (1) 𝜔 ≪ 𝜔0, (2) 𝜔 = 𝜔0, and (3) 𝜔 ≫ 𝜔0.

To decide which regime is relevant, let's make a rough estimate of how the two frequencies compare. For air molecules, the natural frequency 𝜔0 corresponds to ultraviolet radiation — the radiation required to break the strong triple bond in N2. The driving frequency 𝜔 corresponds to one of the colors in visible light (sunlight), so the electron's motion is in the first, low-frequency regime 𝜔 ≪ 𝜔0. (For the analysis of the other regimes, try Problems 9.12 and 9.15.)

The low-frequency regime is easiest to study in the 𝜔 = 0 extreme. It represents a constant force 𝐹 = 𝑒𝐸0 pulling on the electron and stretching the electron–proton bond. When there is change, make what does not change! The bond stretches until the spring force balances the stretching force 𝑒𝐸0. The forces balance when the stretch is 𝑥 = 𝐹/𝑘 or 𝑒𝐸0/𝑘.

Because 𝜔 = 0, the force has been constant since forever, so the bond stretched to its extended length back in the mists of time. When 𝜔 is nonzero, but still much smaller than 𝜔0, the bond still behaves approximately as it did when 𝜔 = 0: It stretches so that the spring force balances the slowly oscillating force 𝐹. Therefore, the stretch, which is the displacement of the electron, is

𝑥(𝑡) ≈ 𝑒𝐸0

𝑘 cos 𝜔𝑡.

(9.111)

4. Acceleration of the electron. We can find the acceleration using dimensional analysis. In driven spring motion, the important length is the displacement 𝑥, and the important time is 1/𝜔. Therefore, the acceleration, which has dimensions of LT−2, must be comparable to 𝑥𝜔2. Because we used the angular frequency (𝜔 rather than 𝑓 ), the dimensionless prefactor turns out to be 1. Then the electron's acceleration is 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

348

9 Spring models

𝑎(𝑡) = 𝑥(𝑡)𝜔2 ≈ 𝑒𝐸0𝜔2

𝑘 cos 𝜔𝑡.

(9.112)

Because the spring constant 𝑘 is related to the electron mass 𝑚e and to the natural frequency 𝜔0 by 𝑘 = 𝑚e𝜔20,

𝑎(𝑡) ≈ 𝑒𝐸0 𝜔2

𝑚

cos 𝜔𝑡.

(9.113)

e 𝜔20

5. Power radiated by the accelerating electron. We found in Sections 5.4.3 and 9.3.2 that the power radiated by an accelerating charge 𝑒 is 𝑃

𝑎2

dipole =

𝑒2

6𝜋𝜖0 𝑐3 .

(9.114)

For the squared acceleration 𝑎2, we'll use the time average to find the average radiated power. Because the time average of cos2𝜔𝑡 is 1/2, 𝑒2𝐸2

⟨𝑎2⟩ = 1

0 𝜔4

2

.

(9.115)

𝑚2e 𝜔40

Then

𝑒4𝐸2

4

𝑃

1

0

dipole =

1

12𝜋𝜖

( 𝜔 ) .

(9.116)

0 𝑐3 𝑚2

𝜔

e

0

This mouthful is useful in explaining the color of sunsets (Section 9.4.2), so it has been worthwhile carrying lots of baggage on the trip from sunlight to scattered light. But to explain the color of the daytime sky, we can simplify the power using proportional reasoning. Because 𝜖0, 𝑐, 𝜔0, 𝑚e, and 𝑒 are independent of the driving frequency 𝜔 (which represents the color), 𝑃dipole ∝ 𝐸20𝜔4.

(9.117)

The factor of 𝐸20 is proportional to the energy density in the incoming sunlight (at frequency 𝜔), which itself is proportional to the incoming power in the sunlight (also at the frequency 𝜔). Thus, 𝑃dipole ∝ 𝑃sunlight𝜔4.

(9.118)

Let's review how the four powers of 𝜔 got here. For low frequencies — and visible light is a low frequency compared to the natural electronic-vibration frequency of an air molecule — the amplitude of spring motion is independent of the driving frequency. The acceleration is then proportional to 𝜔2.

And the radiated power is proportional to the square of the acceleration, so it is proportional to 𝜔4.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.4 Effect of radiation: Blue skies and red sunsets 349

Therefore, the air molecule acts like a filter that takes in (some of the) incoming sunlight and produces scattered light, altering the distribution of colors — similar to how a circuit changes the amplitude of each incoming frequency. However, unlike the low-pass 𝑅𝐶 circuit of Section 2.4.4, which preserves low frequencies and attenuates high frequencies, the air molecule amplifies the high frequencies.

Here are the sunlight and the scattered spectra based on the 𝜔4 filter. Each spectrum shows, by the area of each band, the relative intensities of the various colors. (The unlabeled color band between red and yellow is orange.) I

I

sunlight

scattered

→

ω

ω

red

een

blue

red

een

blue

gr

violet

gr

violet

yellow

yellow

Sunlight looks white. In the scattered light, the high-frequency colors such as blue and violet are much more prominent than they are in sunlight. For example, because 𝜔blue/𝜔red ≈ 1.5 and 1.54 ≈ 5, the blue part of the sunlight is amplified by a factor of 5 compared to the red part. As a result, the scattered light — what comes to us from the sky — looks blue!

9.4.2 Sunsets are red

As sunlight passes through the atmosphere, ever more of its energy gets taken in by air molecules and then scattered (reradiated) in all directions.

As we found in Section 9.4.1, this process happens more rapidly at higher (bluer) frequencies, due to the factor of 𝜔4 in the radiated power. Therefore, the sunbeam becomes redder as it travels through the atmosphere. If the beam travels far enough in the atmosphere, sunsets should look red.

To estimate the necessary travel distance, we can adapt the analysis of Section 9.4.1. Then we will use geometry to estimate the actual travel distance.

How far must sunlight travel in the atmosphere before the beam looks red?

To estimate this length, let's estimate the rate at which energy gets scattered out of the beam. The beam carries an energy flux 𝐹 = 12𝜖0𝐸20𝑐,

(9.119)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

350

9 Spring models

which has the usual form of energy density times propagation speed. (The electric and magnetic fields each contribute one-half of this flux.) To measure the effect of one scattering electron on the beam, let's compute one electron's radiated power divided by the flux: 𝑃

4

dipole

1 𝑒4 𝐸20

𝐹 =

1

12𝜋𝜖

( 𝜔 ) ⁄ 1

(9.120)

0 𝑐3 𝑚2

𝜔

2𝜖0 𝐸20 𝑐.

e

0

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ ⏟

𝑃dipole

𝐹

Noticing that the (unknown) field amplitude 𝐸0 cancels out and doing the rest of the algebra, we get

𝑃

2

4

dipole

1

𝐹 = 8𝜋

3 ( 𝑒2

4𝜋𝜖

× ( 𝜔 ) .

(9.121)

0 𝑚e𝑐2 )

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

𝜔0

area 𝜎

The left side, 𝑃dipole/𝐹, is power divided by power per area. Thus, 𝑃dipole/𝐹

has dimensions of area. It represents the area of the beam whose energy flux gets removed and scattered in all directions. The area is therefore called the scattering cross section 𝜎 (a concept introduced in Section 6.4.5, when we estimated the mean free path of air molecules).

On the right side, the frequency ratio 𝜔/𝜔0 is dimensionless, so the prefactor must also be an area. It is called the Thomson cross section 𝜎T: 2

𝜎

1

T ≡ 8𝜋

3 ( 𝑒2

4𝜋𝜖

≈ 7 ×10−29 m2.

(9.122)

0 𝑚e𝑐2 )

Because 𝜎T is an area, the factor inside the parentheses must be a length.

Indeed, it is the classical electron radius 𝑟0 of Problems 5.37 and 5.44(a). It is comparable to the proton radius of 10−15 meters: 𝑟

1

0 ≡ 𝑒2

4𝜋𝜖0 𝑚e𝑐2 ≈ 2.8×10−15 m.

(9.123)

It approximately answers the question: For the electron to acquire its mass from its electrostatic energy, how large should the electron be? This electron's cross-sectional area is, roughly, the Thomson cross section. In terms of the Thomson cross section, our scattering cross section 𝜎 is 4

𝜎 = 𝜎T ( 𝜔

𝜔 ) .

(9.124)

0

Each scattering electron converts this much area of the beam into scattered radiation. As a rough estimate, each air molecule contributes one scattering 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.4 Effect of radiation: Blue skies and red sunsets 351

electron (the inner electrons, which are tightly bound to the nucleus, have a large 𝜔0 and a tiny scattering cross section). As we found in Section 6.4.5, the mean free path 𝜆mfp and scattering cross section 𝜎 are related by 𝑛𝜎𝜆mfp ∼ 1,

(9.125)

where 𝑛 is the number density of scattering electrons. The mean free path is how far the beam travels before a significant fraction of its energy (at that frequency) is scattered in all directions and is no longer part of the beam.

With one scattering electron per air molecule, 𝑛 is the number density of air molecules. This number density, like the mass density, varies with the height above sea level. To simplify the analysis, we will use a lumped atmosphere. It has a constant temperature, pressure, and density from sea level to the atmosphere's scale height 𝐻, which we estimated in Section 5.4.1 using dimensional analysis (and you estimated using lumping in Problem 6.36).

At 𝐻, the atmosphere ends, and the density abruptly goes to zero.

In this lumped atmosphere, 1 mole of air molecules at any height occupies approximately 22 liters. The resulting number density is approximately 3×1025 molecules per cubic meter:

𝑛 = 1 mol

22 ℓ × 6×1023

1 mol × 103 ℓ

1 m3 ≈ 3×1025 m−3.

(9.126)

Using this 𝑛 and 𝜎 = 𝜎T(𝜔/𝜔0)4, the mean free path becomes 4

𝜆mfp ∼ 1

𝑛𝜎 ≈

1

×

1

× (𝜔0

3×1025 m−3

⏟⏟⏟⏟⏟⏟⏟

7 ×10−29 m2

⏟⏟⏟⏟⏟⏟⏟

𝜔 )

𝑛

𝜎T

(9.127)

4

≈ 12 km × (𝜔0𝜔) .

Unlike the scattering cross section 𝜎, which grows rapidly with 𝜔, the mean free path falls rapidly with 𝜔: High frequencies scatter out of the beam rapidly and travel shorter distances before getting significantly attenuated.

To estimate the frequency ratio 𝜔0/𝜔, let's estimate the equivalent energy ratio ℏ𝜔0/ℏ𝜔. The numerator ℏ𝜔0 is the bond energy. Because air is mostly N2, and the nitrogen–nitrogen triple bond is much stronger than a typical chemical bond (roughly 4 electron volts), the natural frequency 𝜔0 corresponds to an energy ℏ𝜔0 of about 10 electron volts.

The denominator ℏ𝜔 depends on the color of the light. As a lumping approximation, let's divide light into two colors: red and, to represent nonred 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

352

9 Spring models

light, blue–green light. A blue–green photon has an energy ℏ𝜔 of approximately 2.5 electron volts, so ℏ𝜔0/ℏ𝜔 ≈ 4 and (𝜔0/𝜔)4 ≈ 200. Because the mean free path is

4

𝜆mfp ≈ 12 km × (𝜔0𝜔) ,

(9.128)

for blue–green light 𝜆mfp ∼ 100 kilometers. After a distance comparable to 100 kilometers, a significant fraction of the nonred light has been removed (and scattered in all directions).

At midday, when the Sun is overhead, the travel distance is the thickness of the atmosphere 𝐻, roughly 8 kilometers. This distance is much shorter than the mean free path, so very little light (of any color) is scattered out of the sunbeam, and the Sun looks white as it would from space. (Fortunately, our theory doesn't predict that the midday Sun looks red — but do not test this analysis by looking directly at the Sun!) As the Sun descends in the sky, sunlight travels ever farther in the atmosphere.

At sunset, how far does sunlight travel in the atmosphere?

This length is the horizon distance: Standing as high as x

the atmosphere (𝐻 ≈ 8 kilometers), the horizon distance H

R

𝑥 is the distance that sunlight travels through the atmos-Earth

phere at sunset. It is the geometric mean of the atmosphere height 𝐻 and of the Earth's diameter 2𝑅Earth (Problem 2.9), and is approximately 300 kilometers: 𝑥 = 𝐻 × 2𝑅Earth ≈ 8 km × 2 × 6000 km

(9.129)

≈ 300 km.

This distance is a few mean free paths. Each mean free path produces a significant reduction in intensity (more precisely, a factor-of-𝑒 reduction).

Therefore, at sunset, most of the nonred light is gone.

However, for red light the story is different. Because a red-light photon has an energy of approximately 1.8 electron volts, in contrast to the 2.5 electron volts for a blue-green photon, its mean free path is a factor of (2.5/1.8)4 ≈ 4

longer than 100 kilometers for a blue–green photon. The trip of 300 kilometers in the atmosphere scatters out a decent fraction of red light, but much less than the corresponding fraction of blue–green light. The moral of the story is visual: Together the springs in the air molecules and the steep dependence of dipole radiation on frequency produce a beautiful red sunset.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.5 Summary and further problems 353

9.5 Summary and further problems

Many physical processes contain a minimum-energy state where small deviations from the minimum require an energy proportional to the square of the deviation. This behavior is the essential characteristic of a spring. A spring is therefore not only a physical object but a transferable abstraction.

This abstraction has helped us understand chemical bonds, sound speeds, and acoustic, electromagnetic, and gravitational radiation — and from there the colors of the sky and sunset.

Problem 9.10

Two-dimensional acoustics

An acoustic line source is an infinitely long tube that can expand and contract. In terms of the source strength per length, find the power radiated per length.

Problem 9.11

Decay of a lightly damped oscillation

k

In an undamped spring–mass system, the motion is de-m

scribed by 𝑥 = 𝑥0 cos 𝜔0𝑡, where 𝑥0 is the amplitude and 𝜔0, the natural frequency, is 𝑘/𝑚 . In this problem, you use easy cases and lumping to find the effect of a small amount of (linear) damping. The damping force will be 𝐹 = −𝛾𝑣, where 𝛾 is the damping coefficient and 𝑣 is the velocity of the mass.

a. In terms of 𝜔0 and 𝑥0, estimate the typical speed and damping force, and then the typical energy lost to damping in 1 radian of oscillation (a time 1/𝜔0).

b. Express the dimensionless measure of energy loss Δ𝐸

energy lost per radian of oscillation

𝐸 =

oscillation energy

(9.130)

by finding the scaling exponent 𝑛 in

Δ𝐸

𝐸 ∼ 𝑄𝑛

(9.131)

where 𝑄 is the quality factor from Problem 5.53. In terms of 𝑄, what does「a small amount of damping」mean?

c. Find the rate constant 𝐶, built from 𝑄 and 𝜔0, in the time-averaged oscillation energy:

𝐸 ≈ 𝐸0𝑒𝐶𝑡,

(9.132)

d. Using the scaling between amplitude and energy, represent how the mass's position 𝑥 varies with time by finding the rate constant 𝐶′ in the formula 𝑥(𝑡) ≈ 𝑥0 cos 𝜔0𝑡 × 𝑒𝐶′𝑡,

(9.133)

Sketch 𝑥(𝑡).

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

354

9 Spring models

Problem 9.12

Driving a spring at high frequency

Sunlight driving an electron in nitrogen is the easy-case regime 𝜔 ≪ 𝜔0. The opposite regime is 𝜔 ≫ 𝜔0. This regime includes metals, where the electrons are free (the spring constant is zero, so 𝜔0 is zero). Estimate, using characteristic or typical values, the amplitude 𝑥0 of a spring–mass system driven by a force 𝐹 = 𝐹0 cos 𝜔𝑡,

(9.134)

where 𝜔 ≫ 𝜔0. In particular, find the scaling exponent 𝑛 in the transfer function 𝑥0/𝐹0 ∝ 𝜔𝑛.

Problem 9.13

High-frequency scattering

Use the result of Problem 9.12 to show that, in the 𝜔 ≫ 𝜔0 regime (for example, for a free electron), the scattering cross section 𝑃dipole/𝐹 is independent of 𝜔 and is the Thomson cross section 𝜎T.

Problem 9.14

Fiber-optic cable

A fiber-optic cable, used for transmitting telephone calls and other digital data, is a thin glass fiber that carries electromagnetic radiation. High data transmission rates require a high radiation frequency 𝜔. However, scattering losses are proportional to 𝜔4, so high-frequency signals attenuate in a short distance. As a compromise, glass fibers carry「near-infrared」radiation (roughly 1-micrometer in wavelength).

Estimate the mean free path of this radiation by comparing the density of glass to the density of air.

Problem 9.15

Resonance

In Problem 9.12, you analyzed the case of driving a spring at a frequency 𝜔 much higher than its natural frequency 𝜔0. The discussion of blue skies in Section 9.4.1

required the opposite regime, 𝜔 ≪ 𝜔0. In this problem, you analyze the middle regime, which is called resonance. It is a lightly damped spring–mass system driven at its natural frequency.

Assuming a driving force 𝐹0 cos 𝜔𝑡, estimate the energy input per radian of oscillation, in terms of 𝐹0 and the amplitude 𝑥0. Using Problem 9.11(b), estimate the energy lost per radian in terms of the amplitude 𝑥0, the natural frequency 𝜔0, the quality factor 𝑄, and the mass 𝑚.

By equating the energy loss and the energy input, which is the condition for a steady amplitude, find the quotient 𝑥0/𝐹0. This quotient is the gain 𝐺 of the system at the resonance frequency 𝜔 = 𝜔0. Find the scaling exponent 𝑛 in 𝐺 ∝ 𝑄𝑛.

Problem 9.16

Ball resting on the ground as a spring system A ball resting on the ground can be thought of as a spring system. The larger the compression 𝛿, the larger the restoring force 𝐹. (Imagine setting weights on top of the ball so that the extra weight plus the ball's weight is 𝐹.) Find the scaling exponent 𝑛 in 𝐹 ∝ 𝛿𝑛. Is this system an ideal spring (for which 𝑛 = 1)?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

9.5 Summary and further problems 355

Problem 9.17

Inharmonicity of piano strings

An ideal piano string is under tension and has vibration frequencies given by 𝑓

𝑇

𝑛 = 𝑛

2𝐿 𝜌𝐴 ,

(9.135)

where 𝐴 is its cross-sectional area, 𝑇 is the tension, 𝐿 is the string length, and 𝑛 = 1, 2, 3, …. (In Section 9.2.2, we estimated 𝑓1.) Assume that the string's cross section is a square of side length 𝑏. The piano sounds pleasant when harmonics match: for example, when the second harmonic ( 𝑓2) of the middle C string has the same frequency as the fundamental ( 𝑓1) of the C string one octave higher.

However, the stiffness of the string (its resistance to bending) alters these frequencies slightly. Estimate the dimensionless ratio potential energy from stiffness

potential energy from stretching (tension) .

(9.136)

This ratio is also roughly the fractional change in frequency due to stiffness. Write this ratio in terms of the mode number 𝑛, the string side length (or diameter) 𝑏, the string length 𝐿, and the tension-induced strain 𝜖.

Problem 9.18

Buckling

In this problem you estimate the force required to buckle a strut, F

such as a leg bone landing on the ground. The strut has Young's modulus 𝑌, thickness ℎ, width 𝑤, and length 𝑙. The force 𝐹 has de- ∆x flected the strut by Δ𝑥, producing a torque 𝐹Δ𝑥. Find the restoring torque and the approximate condition on 𝐹 for 𝐹Δ𝑥 to exceed the restoring torque — whereupon the strut buckles.

Problem 9.19

Buckling versus tension

l

A strut can withstand a tension force

𝐹T ∼ 𝜖y𝑌 × ℎ𝑤,

(9.137)

w

where 𝜖y is the yield strain. The force 𝐹T is just the yield stress 𝜖y𝑌 h times the cross-sectional area ℎ𝑤. The yield strain typically ranges from 10−3 for brittle materials like rock to 10−2 for piano-wire steel.

Use the result of Problem 9.18 to show that

force that a strut can withstand in tension

force that a strut can withstand against buckling ∼ 𝑙2

ℎ2 𝜖y,

(9.138)

and estimate this ratio for a bicycle spoke.

Problem 9.20

Buckling of leg bone

How much margin of safety, if any, does a typical human leg bone (𝑌 ∼ 1010 pascals) have against buckling, where the buckling force is the person's weight?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

356

9 Spring models

Problem 9.21

Inharmonicity of a typical piano

Estimate the inharmonicity in a typical upright piano's middle-C note. (Its parameters are given in Section 9.2.2.) In particular, estimate the frequency shift of its fourth harmonic (𝑛 = 4).

Problem 9.22

Cylinder resting on the ground

For a solid cylinder of radius 𝑅 resting on the ground (for example, a train wheel), the contact area is a rectangle. Find the scaling exponent 𝛽 in

𝑥

𝛽

R

𝑅 = (𝜌𝑔𝑅

𝑌 ) ,

(9.139)

x

where 𝑥 is the width of the contact strip. Then find the scaling exponent 𝛾 in 𝐹 ∝ 𝛿𝛾, where 𝐹 is the contact force and 𝛿 is the tip compression.

(In Problem 9.16, you computed the analogous scaling exponent for a sphere.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

Bon voyage:

