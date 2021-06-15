99

The rain is pouring down and shelter is a few hundred yards away. Do you get less wet by running? On the one hand, running means less time for raindrops to hit you. On the other hand, running means that the raindrops come toward you more directly and therefore more rapidly. The resolution is not obvious—until you apply the new tool of this chapter: symmetry and conservation. (In Section 3.1.1, we'll resolve this run-in-the-rain question.) 3.1 Invariants

We use symmetry and conservation whenever we find a quantity that, despite the surrounding complexity, does not change. This conserved quantity is called an invariant. Finding invariants simplifies many problems.

Our first invariant appeared unannounced in Section 1.2 when we estimated the carrying capacity of a lane of highway. The carrying capacity—the rate at which cars flow down the lane—depends on the separation between the cars and on their speed. We could have tried to estimate each quantity and then the carrying capacity. However, the separation between cars and the cars' speeds vary greatly, so these estimates are hard to make reliably.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

58

3 Symmetry and conservation

Instead, we invoked the 2-second following rule. As long as drivers obey it, the separation between cars equals 2 seconds of driving. Therefore, one car flows by every 2 seconds—which is the lane's carrying capacity (in cars per time). By finding an invariant, we simplified a complex, changing process.

When there is change, look for what does not change! (This wisdom is from Arthur Engel's Problem-Solving Strategies [12].) 3.1.1 To run or walk in the rain?

We'll practice with this tool by deciding whether to run or walk in the rain.

It's pouring, your umbrella is sitting at home, and home lies a few hundred meters away.

To minimize how wet you become, should you run or walk?

you

Let's answer this question with three simplifications. First, assume that there is no wind, so the raindrops

rain is falling vertically. Second, assume that the v

home

rain is steady. Third, assume that you are a thin sheet: You have zero thickness along the direction toward your house (this approximation was more valid in my youth). Equivalently, your head is protected by a waterproof cap, so you do not care whether raindrops hit your head. You try to minimize just the amount of water hitting your front.

Your only degree of freedom—the only parameter that you get to choose—is your speed. A high speed leaves you in the rain for less time. However, it also makes the rain come at you more directly (more horizontally). But what remains constant, independent of your speed, is the volume of air that you sweep out. Because the rain is steady, that volume contains a fixed number of raindrops, independent of your speed. Only these raindrops hit your front. Therefore, you get equally wet, no matter your speed.

This surprising conclusion is another application of the principle that when there is change, look for what does not change. Here, we could change our speed by choosing to walk or run. Yet no matter what our speed, we sweep out the same volume of air—our invariant.

Because the conclusion of this invariance analysis, that it makes no difference whether you walk or run, is surprising, you might still harbor a nag-ging doubt. Surely running in the rain, which we do almost as a reflex, provide some advantage over a leisurely stroll.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.1 Invariants

59

Is it irrational to run to avoid getting wet?

If you are infinitely thin, and are just a rectangle moving in the rain, then the preceding analysis applies: Whether you run or walk, your front will absorb the same number of raindrops. But most of us have a thickness, and the number of drops landing on our head depends on our speed. If your head is exposed and you care how many drops land on your head, then you should run. But if your head is covered, feel free to save your energy and enjoy the stroll. Running won't keep you any dryer.

3.1.2 Tiling a mouse-eaten chessboard

Often a good way to practice a new tool is on a mathematical problem. Then we do not add the complexity of the physical world to the problem of learning a new tool. Here, therefore, is a mathematical problem: a solitaire game.

A mouse comes and eats two diagonally opposite corners out of a standard, 8 × 8 chessboard. We have a box of rectangular, 2 × 1 dominoes.

Can these dominoes tile the mouse-eaten chessboard? In other words, can we lay down the dominoes to cover every square exactly once (with no empty squares and no overlapping dominoes)?

Placing a domino on the board is one move in this solitaire game. For each move, you choose where to place the domino—so you have many choices at each move. The number of possible move sequences grows rapidly. Instead of examining all these sequences, we'll look for an invariant: a quantity unchanged by any move of the game.

Because each domino covers one white square and one black square, the following quantity 𝐼 is invariant (remains fixed): 𝐼 = uncovered black squares − uncovered white squares.

(3.1)

On a regular chess board, with 32 white squares and 32 black squares, the initial position has 𝐼 = 0. The nibbled board has two fewer black squares, so 𝐼 starts at 30 − 32 = −2. In the winning position, all squares are covered, so 𝐼 = 0. Because 𝐼 is invariant, we cannot win: The dominoes cannot tile the nibbled board.

Each move in this game changes the chessboard. By finding what does not change, an invariant, we simplified the analysis.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

60

3 Symmetry and conservation

Invariants are powerful partly because they are abstractions. The details of the empty squares—their exact locations—lie below the abstraction barrier.

Above the barrier, we see only the excess of black over white squares. The abstraction contains all the information we need in order to know that we can never tile the chessboard.

Problem 3.1

Cube solitaire

A cube has numbers at each vertex; all vertices start at 0 except for the lower left corner, which starts at 1. The moves are all of the same form: Pick any edge and increment its two vertices by one. The goal of this solitaire game is to make all vertices multiples of 3.

For example, picking the bottom edge of the front face and then the bottom edge of the back face, makes the following sequence of cube configurations:

⟶

⟶

(3.2)

Although no configuration above wins the game, can you win with a different move sequence? If you can win, give a winning sequence. If you cannot win, prove that you cannot.

Hint: Create analogous but simpler versions of this game.

Problem 3.2

Triplet solitaire

Here is another solitaire game. Start with the triplet (3, 4, 5). At each move, choose any two of the three numbers. Call the choices 𝑎 and 𝑏. Then make the following replacements:

𝑎 ⟶ 0.8𝑎 − 0.6𝑏;

(3.3)

𝑏 ⟶ 0.6𝑎 + 0.8𝑏.

Can you reach (4, 4, 4)? If you can, give a move sequence; otherwise, prove that it is impossible.

Problem 3.3

Triplet-solitaire moves as rotations in space At each step in triplet solitaire (Problem 3.2), there are three possible moves, depending on which pair of numbers from among 𝑎, 𝑏, and 𝑐 you choose to replace.

Describe each of the three moves as a rotation in space. That is, for each move, give the rotation axis and the angle of rotation.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.1 Invariants

61

Problem 3.4

Conical pendulum

Finding the period of a pendulum, even at small amplitudes, requires calculus because of the pendulum's varying speed.

When there is change, look for what does not change. Accord-

θ

ingly, Christiaan Huygens (1629–1695), called「the most inge-nious watchmaker of all time」[20, p. 79] by the great physicist Arnold Sommerfeld, analyzed the motion of a pendulum moving in a horizontal circle (a conical pendulum). Project-ing its two-dimensional motion onto a vertical screen produces one-dimensional pendulum motion; thus, the period of the two-dimensional motion is the same as the period of one-dimensional pendulum motion! Use that idea to find the period of a pendulum (without calculus!).

3.1.3 Logarithmic scales

In the solitaire game in Section 3.1.2, a move covered low end of hearing 20 Hz

two chessboard squares with a domino. In the game piano middle C

262 Hz

of understanding the world, a frequent move is chang- highest piano C

4186 Hz

ing the system of units. As in solitaire, ask,「When high end of hearing 20 kHz

such a move is made, what is invariant?」As an example to crystallize our thinking, here are frequencies related to human hearing. Let's graph them using kilohertz (kHz) as the unit. The frequencies then arrange themselves as follows:

low end

high C

high end

kHz

0

10

20

middle C

Now let's change units from kilohertz to hertz (Hz)—and keep the 0, 10, and 20 labels at their current positions on the page. This change magnifies every spacing by a factor of 1000: The new 20 hertz is where 20 kilohertz was (about 4 inches or 10 centimeters to the right of the origin), and 20 kilohertz, the high end of human hearing, sits 100 meters to our right—far beyond the borders of the page. This new scale is not very useful.

However, we missed the chance to use an invariant: the ratio between frequencies. For example, the ratio between the upper end of human hearing (20 kilohertz) and middle C (262 hertz) is roughly 80. If we use a representation based on ratio rather than absolute difference, then the spacing between frequencies would not change even when we changed the unit.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

62

3 Symmetry and conservation

We have such a representation: logarithms! On a logarithmic scale, a distance corresponds to a ratio rather than a difference. To see the contrast, let's place the numbers from 1 to 10 on a logarithmic scale.

1

2

3

4

5

6

7

8

9 10

The physical gap between 1 and 2 represents not their difference but rather their ratio, namely 2. According to my ruler, the gap is approximately 3.16

centimeters. Similarly, the physical gap between 2 and 3—approximately 1.85 centimeters—represents the smaller ratio 1.5. In contrast to their relative positions on a linear scale, 2 and 3 on a logarithmic scale are closer than 1 and 2 are. On a logarithmic scale, 1 and 2 have the same separation as 2

and 4: Both gaps represent a ratio of 2 and therefore have the same physical size (3.16 centimeters).

Problem 3.5

Practice with ratio thinking

On a logarithmic scale, how does the physical gap between 2 and 8 compare to the gap between 1 and 2? Decide based on your understanding of ratios; then check your reasoning by measuring both gaps.

Problem 3.6

More practice with ratio thinking

Is the gap between 1 and 10 less than twice, equal to twice, or more than twice the gap between 1 and 3? Decide based on your understanding of ratios; then check your reasoning by measuring both gaps.

Problem 3.7

Moving along a logarithmic scale

On the logarithmic scale in the text, the gap between 2 and 3 is approximately 1.85

centimeters. Where do you land if you start at 6 and move 1.85 centimeters right-ward? Decide based on your understanding of ratios; then check your reasoning by using a ruler to find the new location.

Problem 3.8

Extending the scale to the right

On the logarithmic scale in the text, the gap between 1 and 10 is approximately 10.5 centimeters. If the scale were extended to include numbers up to 1000, how large would the gap between 10 and 1000 be?

Problem 3.9

Extending the scale to the left

If the logarithmic scale were extended to include numbers down to 0.01, how far to the left of 1 would you have to place 0.04?

On a logarithmic scale, the frequencies related to hearing arrange themselves as follows:

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.1 Invariants

63

low end

middle C

high C

high end

Hz

10−2

10−1

100

101

102

103

104

105

Changing the units to kilohertz just shifts all the frequencies, but leaves their relative positions invariant:

low end

middle C

high C

high end

kHz

10−2

10−1

100

101

102

103

104

105

Problem 3.10

Acoustic energy fluxes

In acoustics, sound intensity is measured by energy flux, which is measured in decibels (dB)—a logarithmic representation of watts per square meter. On the decibel scale, 0 decibels corresponds to the reference level of 10−12 watts per square meter.

Every 10 decibels (or 1 bel) represents an increase in energy flux of a factor of 10

(thus, 20 decibels represents a factor-of-100 increase in energy flux).

a. How many watts per square meter is 60 decibels (the sound level of normal conversation)?

b. Place the following energy fluxes on a decibel scale: 10−9 watts per square meter (an empty church), 10−2 watts per square meter (front row at an orchestra concert), and 1 watt per square meter (painfully loud).

Logarithmic scales offer two benefits. First, as we saw explicitly, logarithmic scales incorporate invariance. The second benefit was only implicit in the previous discussion: Logarithmic scales, unlike linear scales, allow us to represent a huge range. For example, if we include power-line hum (50 or 60 hertz) on the linear frequency scale on p. 61, we can hardly distinguish its position from 0 kilohertz. The logarithmic scale has no problem.

low end

middle C

high C

high end

Hz

10−2

10−1

100

101

102

103

104

105

power-line hum

In our fallen world, benefits usually conflict. One usually has to sacrifice one benefit for another (speed for accuracy or justice for mercy). With logarithmic scales, however, we can eat our cake and have it.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

64

3 Symmetry and conservation

Problem 3.11

Labeling a logarithmic scale

Let's make a scale to represent sizes in the universe, from protons (10−15 meters) to galaxies (1030 meters), with people and bacteria in between. With such a large range, we should use a logarithmic scale for size 𝐿. Which one of these two ways of labeling the scale is correct, and which way is nonsense?

a.

log

L

10

−10

0

10

20

30

b.

L (m)

10−10

100

1010

1020

1030

Logarithmic scales can make otherwise obscure symbolic calculations intuitive. An example is the geometric mean, which we used in Section 1.6 to make gut estimates:

estimate = lower bound × upper bound.

(3.4)

Geometric means also occur in the physical world.

h

d

As you found in Problem 2.9, the distance 𝑑 to the horizon, as seen from a height ℎ above the Earth's surface, is

R

𝑑 ≈ ℎ𝐷 ,

(3.5)

where 𝐷 = 2𝑅Earth is the diameter of the Earth.

Imagine a lifeguard sitting with his or her eyes at a height ℎ = 4 meters above sea level. Then the distance to the horizon is 𝑑 ≈ ( 4 m

⏟ × 12

⏟ 000

⏟

km

⏟⏟⏟ )1/2.

(3.6)

ℎ

𝐷

To do the calculation, we convert 12 000 kilometers to 1.2 × 107 meters, calculate 4 × 1.2×107, and compute the square root: 𝑑 ≈ 4 × 1.2×107 m ≈ 7000 m = 7 km.

(3.7)

In this symbolic form with a square root, the calculation obscures the fundamental structure of the geometric mean. We first calculate ℎ𝐷, which is an area (and often contains, as it did here, a huge number). Then we take the square root to get back a distance. However, the area has nothing to do with the structure of the problem. It is merely a bookkeeping device.

Bookkeeping devices are useful; they are how you tell a computer what to calculate. However, to understand the calculation, we, as humans, should use a logarithmic scale to represent the distances. This scale captures the structure of the problem.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.1 Invariants

65

√

h

hD

D

left gap

right gap

m

100

102

104

106

108

How can we describe the position of the geometric mean ℎ𝐷 ?

The first clue is that the geometric mean, because it gap endpoints

ratio

is a mean, lies somewhere between ℎ and 𝐷. This property is not obvious from the calculation using left ℎ… ℎ𝐷

ℎ𝐷

ℎ = 𝐷ℎ

the square root. To find where the geometric mean lies, mind the gaps. On a logarithmic scale, a gap right ℎ𝐷 …𝐷

𝐷 = 𝐷

ℎ𝐷

ℎ

represents the ratio of its endpoints. As shown in the table, the left and right gaps represent the same ratio, namely 𝐷/ℎ! Therefore, on the logarithmic scale, the geometric mean lies exactly halfway between ℎ and 𝐷.

Based on this ratio representation, we can rephrase the geometric-mean calculation in a form that we can do mentally.

What distance is as large compared to 4 meters as 12 000 kilometers is compared to it?

For lack of imagination, my first guess is 1 kilometer. It's 12 000 times smaller than the diameter 𝐷 (which is 12 000 kilometers), but only 250 times larger than the height ℎ (4 meters). My guess of 1 kilometer is therefore somewhat too small.

How is a guess of 10 kilometers?

It's 2500 times larger than ℎ, but only 1200 times smaller than 𝐷. I overshot slightly. How about 7 kilometers? It's roughly 1750 times larger than 4 meters, and roughly 1700 times smaller than 12 000 kilometers. Those gaps are close to each other, so 7 kilometers is the approximate geometric mean.

√

h

hD ≈ 7 km

D

factor of 1732

factor of 1732

m

100

102

104

106

108

Similarly, when we make gut estimates, we should place our lower and upper estimates on a logarithmic scale. Our best gut estimate is then their midpoint. What a simple picture!

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

66

3 Symmetry and conservation

Should all quantities be placed on a logarithmic scale?

No. An illustrative contrast is between size and position. Both quantities have the same units. But size ranges from 0 to ∞, whereas position ranges from −∞ to ∞. Position therefore cannot be placed on a logarithmic scale (where would you put −1 meter?). In contrast, size (a magnitude) belongs on a logarithmic scale. In general, location parameters, such as position, should not be placed on a logarithmic scale but magnitudes should.

3.2 From invariant to symmetry operation

In the preceding examples, we knew the moves of the game and sought the invariant. In the mouse-eaten chessboard (Section 3.1.2), the moves are putting down a 2×1 domino on two adjacent empty squares. The invariant was the difference between empty black and white squares. Often, however, the benefit of invariants lies in the other direction: You know the invariant and seek the moves that preserve it. These moves are called the symmetry operations or simply the symmetries.

We'll first examine this idea in a familiar situation: converting units (Section 3.2.1). Then we'll practice it on a sum solved by the three-year-old Carl Friedrich Gauss (Section 3.2.2) and then by finding maxima and minima (Section 3.2.3).

3.2.1 Converting units

We often convert a quantity from one unit system to another—for example, mass from English to metric units or prices from dollars to pounds or euros.

A useful physical conversion is writing energy density—energy divided by amount of stuff—in useful units. Let's start with the reasonable energy unit for a chemical bond, namely the electron volt or eV (Section 2.1). Then a useful unit for energy density is

1 eV

molecule.

(3.8)

This energy density is our invariant. As we convert from one unit system to another, our moves have to preserve the energy density.

What are the legal moves—the moves that preserve the energy density?

The legal moves are all ways of multiplying by 1—for example, by 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.2 From invariant to symmetry operation 67

6×1023 molecules

1 mol

or

1 mol

.

(3.9)

6×1023 molecules

Either quotient is a form of 1, because 1 mole is defined to be Avogadro's number of molecules, and Avogadro's number is 6×1023. I carefully wrote

「1 mol」with the number rather than simply as「mol.」The more explicit form reminds us that「6×1023 molecules per mole」is shorthand for a quotient of two identical quantities: 6×1023 molecules and 1 mole.

Multiplying the energy density by the first form of 1 gives 1 eV

6×1023 molecules

6×1023 eV

×

=

.

(3.10)

molecule

1 mol

mol

(If we had multiplied by the second form of 1, the units of molecules would have become molecules squared instead of canceling. The strike-through lines help us check that we got the desired units.) The giant exponent makes this form almost meaningless. To improve it, let's multiply by another form of 1, based on the definition of an electron volt. Two forms of 1 are 1.6×10−19 J

1 eV

or

1 eV

.

(3.11)

1.6×10−19 J

Multiplying by the first form of 1 gives

1 eV

6×1023 molecules

×

× 1.6×10−19 J ≈ 102 kJ.

(3.12)

molecule

1 mol

1 eV

mol

(A more exact value is 96 kilojoules per mole.) In the United States, energies related to food are stated in Calories, also known as kilocalories (roughly 4.2 kilojoules). In calorie units, the useful energy-density unit is 96 kJ

1 kcal

23 kcal

×

≈

.

(3.13)

1 mol 4.2 kJ

mol

Which form is more meaningful: 23 kcal or 23 kcal?

mol

mol

The forms are mathematically equivalent: You can multiply by 23 before or after dividing by a mole. However, they are not psychologically equivalent.

The first form builds the abstraction of kilocalories per mole, and then says,

「Here are 23 of them.」In contrast, the second form gives us the energy for 1 mole, a human-sized amount. The second form is more meaningful.

Similarly, the speed of light 𝑐 is commonly quoted as (approximately) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

68

3 Symmetry and conservation

3×108 ms.

(3.14)

The psychologically fruitful alternative is

𝑐 = 3×108 m

1 s

.

(3.15)

This form suggests that 300 million meters, at least for light, is the same as 1 second. With this idea, you can convert wavelength to frequency (Problem 3.14); with a slight extension, you can convert frequency to energy (Problem 3.15) and energy to temperature (Problem 3.16).

Problem 3.12

Absurd units

By multiplying by suitable forms of 1, convert 1 furlong per fortnight into meters per second.

Problem 3.13

Rainfall units

Rainfall, in nonmetric parts of the world, is sometimes measured in acre feet. By multiplying by suitable forms of 1, convert 1 acre foot to cubic meters. (One square mile is 640 acres.)

Problem 3.14

Converting wavelength to frequency

Convert green-light wavelength, 0.5 micrometers (0.5 μm), to a frequency in cycles per second (hertz or Hz).

Problem 3.15

Converting frequency to energy

Analogously to how you used the speed of light in Problem 3.14, use Planck's constant ℎ to convert the frequency of green light to an energy in joules (J) and in electron volts (eV). This energy is the energy of a green-light photon.

Problem 3.16

Converting energy to temperature

Use Boltzmann's constant 𝑘B to convert the energy of a green-light photon (Problem 3.15) to a temperature (in kelvin). This temperature, except for a factor of 3, is the surface temperature of the Sun!

Conversion factors need not be numerical. Insight often comes from symbolic factors. Here is an example from fluid flow. As we will derive in Section 5.3.2, the drag coefficient 𝑐d is defined as the dimensionless ratio 𝐹

𝑐

drag

d ≡

,

1

(3.16)

2 𝜌𝑣2𝐴

where 𝜌 is the fluid density, 𝑣 is the speed of the object moving in the fluid, and 𝐴 is the object's cross-sectional area. To give this definition and ratio a 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.2 From invariant to symmetry operation 69

physical interpretation, multiply it by 𝑑/𝑑, where 𝑑 is the distance that the object travels:

𝐹

𝑐

drag 𝑑

d ≡

.

1

(3.17)

2 𝜌𝑣2𝐴𝑑

The numerator, 𝐹drag𝑑, is the work done or the energy consumed by drag.

In the denominator, the product 𝐴𝑑 is the volume of fluid displaced by the object, so 𝜌𝐴𝑑 is the corresponding mass of fluid. Therefore, the denominator is also

12 ×massoffluiddisplaced×𝑣2.

(3.18)

The object's speed 𝑣 is also approximately the speed given to the displaced fluid (which the object shoved it out of its way). Therefore, the denominator is roughly

12 ×massoffluiddisplaced×(speedofdisplacedfluid)2.

(3.19)

This expression is the kinetic energy given to the displaced fluid. The drag coefficient is therefore roughly the ratio

energy consumed by drag

𝑐d ∼ energy given to the fluid .

(3.20)

My tenth-grade chemistry teacher, Mr. McCready, told us that unit conversion was the one idea that we should remember from the entire course.

Almost every problem in the chemistry textbook could be solved by unit conversion, which says something about the quality of the book but also about the power of the method.

3.2.2 Gauss's childhood sum

A classic example of going from the invariant to the symmetry is the following story of the young Carl Friedrich Gauss. Although maybe just a legend, the story is so instructive that it ought to be true. Once upon a time, when Gauss was 3 years old, his schoolteacher, wanting to occupy the students, assigned them to compute the sum

𝑆 = 1 + 2 + 3 + ⋯ + 100,

(3.21)

and sat back to enjoy the break. In a few minutes, Gauss returned with an answer of 5050.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

70

3 Symmetry and conservation

Was Gauss right? If so, how did he compute the sum so quickly?

Gauss saw that the sum—the invariant—is unchanged when the terms are added backward, from highest to lowest:

1 + 2 + 3 + ⋯ + 100 = 100 + 99 + 98 + ⋯ + 1.

(3.22)

Then he added the two versions of the sum, the original and the reflected: 1 + 2 + 3 + ⋯ + 100 = 𝑆

+ 100 + 99 + 98 + ⋯ + 1 = 𝑆

(3.23)

101 + 101 + 101 + ⋯ + 101 = 2𝑆.

In this form, 2𝑆 is easy to compute: It contains 100 copies of 101. Therefore, 2𝑆 = 100 × 101, and 𝑆 = 50 × 101 or 5050—as the young Gauss claimed. He made the problem so simple by finding a symmetry: a transformation that preserved the invariant.

Problem 3.17

Number sum

Use Gauss's method to find the sum of the integers between 200 and 300 (inclusive).

Problem 3.18

Symmetry for algebra

Use symmetry to find the missing coefficients in the expansion of (𝑎 − 𝑏)3: (𝑎 − 𝑏)3 = 𝑎3 − 3𝑎2𝑏+? 𝑎𝑏2+? 𝑏3.

(3.24)

Problem 3.19

Integrals

Evaluate these definite integrals. Hint: Use symmetry.

10

∞

∞

(a) ∫ 𝑥3𝑒−𝑥2 𝑑𝑥, (b) ∫

𝑥3

∫ ln 𝑥

1 + 7𝑥2 + 18𝑥8 𝑑𝑥, and (c)

1 + 𝑥2 𝑑𝑥.

−10

−∞

0

3.2.3 Finding maxima or minima

To practice finding the symmetry operation, we'll find the maximum of the function 6𝑥 − 𝑥2 without using calculus. Calculus is the elephant gun. It can solve many problems, but only after blasting them into the same form (smithereens). Avoiding calculus forces us to use more particular, but more subtle methods—such as symmetry. As Gauss did in summing 1 + 2 + ⋯ +

100, let's find a symmetry operation that preserves the essential feature of the problem—namely, the location of the maximum.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.2 From invariant to symmetry operation 71

Symmetry implies moving around an object's pieces. Fortunately, our function 6𝑥 − 𝑥2 factors into pieces:

6𝑥 − 𝑥2 = 𝑥(6 − 𝑥).

(3.25)

This form, along with the idea that multiplication is commutative, suggests the symmetry operation. For if the operation just swaps the two factors, replacing 𝑥(6 − 𝑥) with (6 − 𝑥)𝑥, it does not change the location of the maximum. (A parabola has exactly one maximum or minimum.) The symmetry operation that makes the swap is 𝑥 ⟷ 6 − 𝑥.

(3.26)

It turns 2 into 4 (and vice versa) and 1 into 5 (and vice versa). The only value unchanged (left invariant) by the symmetry operation is 𝑥 = 3. Therefore, 6𝑥 − 𝑥2 has its maximum at 𝑥 = 3.

maximum

Geometrically, the symmetry operation reflects the graph of 6𝑥 − 𝑥2 through the line 𝑥 = 3. By construction, this symme-6x − x2

try operation preserves the location of the maximum. Therefore, the maximum has to lie on the line 𝑥 = 3.

We could have found this maximum in several other ways, so the use of symmetry might seem superfluous or like overkill.

However, it warms us up for the following, more compli-x = 3

cated use. The energy required to fly has two pieces: generating lift, which requires an energy 𝐴/𝑣2, and fighting drag, which requires an energy 𝐵𝑣2. (𝐴 and 𝐵 are constants that we estimate in Sections 3.6.2 and 4.6.1.)

𝐸flight = 𝐴

𝑣2 + 𝐵𝑣2.

(3.27)

To minimize fuel consumption, planes choose their cruising speed to minimize 𝐸flight. More precisely, a cruising speed is selected, and the plane is designed so that this speed minimizes 𝐸flight.

In terms of the constants 𝐴 and 𝐵 , what speed minimizes 𝐸 flight?

Like the parabola 𝑥(6−𝑥), this energy has one extremum. For the parabola, the extremum was a maximum; here, it is a minimum. Also similar to the parabola, this energy has two pieces connected by a commutative operation. For the parabola, the operation was multiplication; here, it is addition.

Continuing the analogy, if we find a symmetry operation that transposes 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

72

3 Symmetry and conservation

the two pieces, then the speed preserved by the operation will be the minimum-energy speed.

Finding this symmetry operation is hard to do in one gulp, because it must transpose 1/𝑣2 and 𝑣2 and transpose 𝐴 and 𝐵. These two difficulties suggest that we apply divide-and-conquer reasoning: Find a symmetry operation that transposes 1/𝑣2 and 𝑣2, and then modify so that it also transposes 𝐴

and 𝐵.

E

To transpose 1/𝑣2 and 𝑣2, the symmetry operation is the following:

𝑣 ⟷ 1𝑣.

(3.28)

Now let's restore one of the two constants and modify Eflight

the symmetry operation so that it transposes 𝐴/𝑣2 and Edrag

𝑣2:

Elift

𝑣 ⟷ 𝐴

vmin

v

𝑣 .

(3.29)

Now let's restore the second constant, 𝐵, and find the full symmetry operation that transposes 𝐴/𝑣2 and 𝐵𝑣2: 𝐵 𝑣 ⟷ 𝐴

𝑣 .

(3.30)

Rewriting it as a replacement for 𝑣, the symmetry operation becomes 𝑣 ⟷ 𝐴/𝐵

𝑣 .

(3.31)

This symmetry operation transposes the drag energy and lift energy, leaving the total energy 𝐸flight unchanged. Solving for the speed preserved by the symmetry operation gives us the minimum-energy speed: 1/4

𝑣min = (𝐴𝐵) .

(3.32)

In Section 4.6.1, once we find 𝐴 and 𝐵 in terms of the characteristics of the air (its density) and the plane (such as its wingspan), we can estimate the minimum-energy (cruising) speeds of planes and birds.

Problem 3.20

Solving a quadratic equation using symmetry The equation 6𝑥−𝑥2 +7 = 0 has a solution at 𝑥 = −1. Without using the quadratic formula, find any other solutions.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.3 Physical symmetry

73

3.3 Physical symmetry

For a physical application of symmetry, imagine a uniform metal 80◦

10◦

sheet, perhaps aluminum foil, cut into the shape of a regular penT = ?

tagon. Imagine that to the edges are attached heat sources and 10◦

10◦

sinks—big blocks of metal at a fixed temperature—in order to 10◦

hold the edges at the temperatures marked on the figure. After we wait long enough, the temperature distribution in the pentagon stops changing (comes to equilibrium).

Once the pentagon temperature equilibrates, what is the temperature at its center?

A brute-force, analytic solution is difficult. Heat flow is described by the heat equation, a linear second-order partial-differential equation: 𝜅∇2𝑇 = ∂𝑇

∂𝑡 ,

(3.33)

where 𝑇 is the temperature as a function of position and time, and 𝜅 (kappa) is the thermal diffusivity (which we will study in more detail in Chapter 7).

But don't worry: You do not have to understand the equation, only that it is difficult to solve!

80◦

Once the temperature settles down, the time derivative becomes zero, and the equation simplifies to 𝜅∇2𝑇 = 0. However, even this 10◦

10◦

simpler equation has solutions only for simple shapes, and the solutions are complicated. For example, the temperature distrib-10◦

ution on the simpler square sheet is hardly intuitive (the figure shows contour lines spaced every 10∘). For a pentagon, the temperature distribution is worse. However, because the pentagon is regular, symmetry might make the solution flow.

What is a useful symmetry operation?

Nature, in the person of the heat equation, does not care about the direction of our coordinate system. Thus, rotating the pentagon about its center does not change the temperature at the center. Therefore, the following five orientations of the pentagon share the same central temperature: 80◦

10◦

10◦

10◦

10◦

10◦

10◦

10◦

10◦

80◦

10◦

10◦

80◦

10◦

10◦

10◦

10◦

80◦

10◦

10◦

10◦

10◦

80◦

10◦

10◦

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

74

3 Symmetry and conservation

Like Gauss adding the two versions of his sum (Section 3.2.2), stack these sheets mentally and add the temperatures that lie on top of each other to make the temperature profile of a new super sheet (adding the temperatures is valid because the heat equation is linear).

=

(3.34)

Each super edge contains one 80∘ edge and four 10∘ edges, for a temperature of 120∘. The super sheet is a regular pentagon where all edges are at 120∘.

Therefore, the temperature throughout the sheet is 120∘—including at the center. Because the symmetry operation has helped us construct a much easier problem, we did not have to solve the heat equation.

One more step tells us the temperature in the center of the original sheet.

The symmetry operation rotates the pentagon about its center; when the plates are stacked, the centers align. Each center then contributes one-fifth of the 120∘ in the center, so the original central temperature is 24∘.

To highlight the transferable ideas (abstractions), compare the symmetry solutions to Gauss's sum and to this temperature problem. First, both problems seem complicated. Gauss's sum has many terms, all different; the pentagon problem seems to require solving a difficult differential equation.

Second, both problems contain a symmetry operation. In Gauss's sum, the symmetry operation reversed the order of the terms; for the pentagon, the symmetry operation rotates it by 72∘. Finally, the symmetry operation leaves an important quantity unchanged. For Gauss's problem, this quantity is the sum; for the pentagon, it is the central temperature.

When there is change, look for what does not change. Look for invariants and the corresponding symmetries: the operations that preserve the invariants.

Problem 3.21

Symmetry solution for a square sheet

Here is the contour plot again of the temperature on a square 80◦

sheet. The contour lines are separated by 10∘. Use that information to label the temperature of each contour line. Based 10◦

10◦

on the symmetry reasoning, what should the temperature at the center of the square be? Is this predicted temperature con-10◦

sistent with what is shown in the contour plot?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.4 Box models and conservation 75

Problem 3.22

Simulating the heat equation

Using symmetry, we showed that the temperature at the cen-80◦

10◦

ter of the pentagon is the average of the temperatures of the T = ?

sides. Check the solution by simulating the heat equation 10◦

10◦

with a pentagonal boundary.

10◦

Problem 3.23

Shortest bisecting path

What is the shortest path that bisects an equilateral triangle into two equal areas?

Here are three examples of bisecting paths:

To set your problem-solving gears in motion, first rank these three bisecting paths according to their lengths.

3.4 Box models and conservation

Invariance underlies a powerful everyday abstraction: box models. We already made a box model in Section 3.1.1, to decide whether to run or walk in the rain. Now let's examine this method further. The simplest kind of box contains a fixed amount of stuff—perhaps the volume of fluid or the number of students at an ideal university (where every student graduates in a fixed time). Then what goes into the box must come out. This conclusion seems simple, even simplistic, but it has wide application.

3.4.1 Supply and demand

box

For another example of a box model, return to our supply

demand

estimate of US oil usage (Section 1.4). The flow oil

into the box—the push or the supply—is the imported and domestically produced oil. The flow out of the box—the pull or the demand—is the oil usage. The estimate, literally taken, asks for the supply (how much oil is imported and domestically produced). This estimate is difficult. Fortunately, as long as oil does not accumulate in the box (for example, as long as oil is not salted away in underground storage bunkers), then the amount of oil in the box is an invariant, so the supply equals the demand. To estimate the supply, we accordingly estimated the demand. This conservation reasoning is the basis of the following estimate of a market size.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

76

3 Symmetry and conservation

How many taxis are there in Boston, Massachusetts?

For many car-free years, I lived in an old neighborhood of Boston. I often rode in taxis and wondered about the size of the taxi market—in particular, how many taxis there were. This number seemed hard to estimate, because taxis are scattered throughout the city and hard to count.

The box contains the available taxi driving (mea-supply

available

demand

sured, for example, as time). It is supplied by taxi driving

(drivers)

(users)

taxi drivers. The demand is due to taxi users. As long as the supply and demand match, we can

estimate the supply by estimating the demand.

For estimating the demand, the starting point is that Boston has roughly 500 000 residents. As a gut estimate, each resident uses maybe one taxi per month, for a 15-minute ride: Boston taxis are expensive; unless one doesn't own a car, it's hard to imagine using them more often than once a month or for longer than 15 minutes. Then the demand is about 105 hours of taxi driving per month:

15 min

1 hr

105 hr

5×105 residents ×

×

≈

.

(3.35)

resident month 60 min

month

How many taxi drivers will that many monthly hours support?

Taxi drivers work long shifts, maybe 60 hours per week. I'd guess that they carry passengers one-half of that time: 30 hours per week or roughly 100

hours per month. At that pace, 105 hours of monthly demand could be supplied by 1000 taxi drivers or, assuming each taxi is driven by one driver, by 1000 taxis.

What about tourists?

Tourists are very short-term Boston residents, mostly without cars. Tourists, although fewer than residents, use taxis more often and for longer than residents do. To include the tourist contribution to taxi demand, I'll simply double the previous estimate to get 2000 taxis.

This estimate can be checked reliably, because Boston is one of the United States cities where taxis may pick up passengers only with a special permit, the medallion. The number of medallions is strictly controlled, so medallions cost a fortune. For about 60 years, their number was restricted to 1525, until a 10-year court battle got the limit raised by 260, to about 1800.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.4 Box models and conservation 77

The estimate of 2000 may seem more accurate than it deserves. However, chance favors the prepared mind. We prepared by using good tools: a box model and divide-and-conquer reasoning. In making your own estimates, have confidence in the tools, and expect your estimates to be at least half decent. You will thereby find the courage to start: Optimism oils the rails of estimation.

Problem 3.24

Differential equation for an RC circuit box

Explain how a box model leads to the differential R

equation for the low-pass 𝑅𝐶 circuit of Section 2.4.4: Vin Vout

𝑅𝐶 𝑑𝑉out

C

𝑑𝑡 + 𝑉out = 𝑉in.

(3.36)

(Almost every differential equation arises from a box or conservation argument.)

Problem 3.25

Boston taxicabs tree

Draw a divide-and-conquer tree for estimating the number of Boston taxicabs.

First draw it without estimates. Then include your estimates, and propagate the values toward the root.

Problem 3.26

Needles on a Christmas tree

Estimate the number of needles on a Christmas tree.

3.4.2 Flux

Flows, such as the demand for oil or the supply of taxi cabs, are rates—an amount per time. Physical flows are also rates, but they live in a geometry. This embedding allows us to de- flow rate area

fine a related quantity: flux.

amount

=

time

flux of stuff ≡ rate

area = amount of stuff

area × time .

(3.37)

For example, particle flux is the rate at which particles (say, molecules) pass through a surface perpendicular to the flow, divided by the area of the surface. Dividing by the surface area, an operation with no counterpart in nonphysical flows (for example, in the demand for taxicabs), makes flux more invariant and useful than rate. For if you double the surface area, you double the rate. This proportionality is not newsworthy, and usually doesn't add insight, only clutter. When there is change, look for what does not change: Even when the area changes, flux does not.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

78

3 Symmetry and conservation

Problem 3.27

Rate versus amount

Explain why rate (amount per time) is more useful than amount.

Problem 3.28

What is current density?

What kind of flux (flux of what?) is current density (current per area)?

The definition of flux leads to a simple and important connection between flux and flow speed. Imagine a tube of stuff (for example, molecules) with cross-sectional area 𝐴. The stuff flows through the tube at a speed 𝑣.

In a time 𝑡 , how much stuff leaves the tube?

vt

In the time 𝑡, the stuff in the shaded chunk, spanning a length 𝑣𝑡, leaves the tube. This

chunk has volume 𝐴𝑣𝑡. The amount of stuff

A

v

in that volume is

stuff

v

× 𝐴𝑣𝑡.

(3.38)

⏟olume

⏟⏟⏟⏟ ⏟

density of stuff

volume

The amount of stuff per volume, the density of stuff, occurs so often that it usually gets a special symbol. When the stuff is particles, the density is labeled 𝑛 for number density (in contrast to 𝑁 for the number itself). When the stuff is charge or mass, the density is labeled 𝜌.

From the amount of stuff, we can find the flux: 𝐴𝑣𝑡

density of stuff

volume

⏞⏞⏞⏞⏞

flux of stuff = amount of stuff

×

area × time =

area

.

(3.39)

⏟⏟⏟ × time

⏟⏟⏟⏟

𝐴𝑡

The product 𝐴𝑡 cancels, leaving the general relation flux of stuff = density of stuff × flow speed.

(3.40)

As a particular example, when the stuff is charge (Problem 3.28), the flux of stuff becomes charge per time per area, which is current per area or current density. With that label for the flux, the general relation becomes current density

⏟⏟⏟⏟⏟⏟⏟⏟⏟ = charge density

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × flow speed

⏟⏟⏟⏟⏟⏟⏟,

(3.41)

𝐽

𝜌

𝑣drift

where 𝑣drift is the flow speed of the charge—which you will estimate in Problem 6.16 for electrons in a wire.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.4 Box models and conservation 79

The general relation will be crucial in estimating the power required to fly (Section 3.6) and in understanding heat conduction (Section 7.4.2).

3.4.3 Average solar flux

An important flux is energy flux: the rate at which energy passes through a surface, divided by the area of the surface. Here, rate means energy per time, or power. Therefore, energy flux is power per area. An energy flux essential to life is the solar flux: the solar power per area falling on Earth.

This flux drives most of our weather. At the top of the atmosphere, looking directly toward the sun, the flux is roughly 𝐹 = 1300 watts per square meter.

However, this flux is not evenly distributed over the surface of the earth.

The simplest reason is night and day. On the night side of the Earth, the solar flux is zero. More subtly, different latitudes have different solar fluxes: The equatorial regions are warmer than the poles because they receive more solar flux than the poles do.

What is the solar flux averaged over the whole Earth?

We can find the average flux using a box model (a sunlight

Earth

conservation argument). Here is sunlight coming to the Earth (with parallel rays, because the Sun is so far away). Hold a disk with radius 𝑅Earth perpendicular to the sunlight so that it blocks all sunlight that the Earth otherwise would get. The disk absorbs a power that we can find from the energy flux: power = energy flux × area = 𝐹𝜋𝑅2Earth,

(3.42)

where 𝐹 is the solar flux. Now spread this power over the whole Earth, which has surface area 4𝜋𝑅2Earth:

power

𝐹𝜋𝑅2

average flux =

Earth

surface area =

= 𝐹

4𝜋𝑅2

4 .

(3.43)

Earth

Because one-half of the Earth is in night, averaging over the night and day-light parts of the earth accounts for a factor of 2. Therefore, averaging over latitudes must account for another factor of 2 (Problem 3.29).

Problem 3.29

Averaging solar flux over all latitudes

Integrate the solar flux over the whole sunny side of the Earth, accounting for the varying angles between the incident sunlight and the surface. Check that the result agrees with the result of the box model.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

80

3 Symmetry and conservation

The result is roughly 325 watts per square meter. This average flux slightly overestimates what the Earth receives at ground level, because not all of the 1300 watts per square meter hitting the top of the atmosphere reaches the surface. Roughly 30 percent gets reflected near the top of the atmosphere (by clouds). The surviving amount is about 1000 watts per square meter.

Averaged over the surface of the Earth, it becomes 250 watts per square meter (which then goes into the surface and the atmosphere), or approximately 𝐹/5, where 𝐹 is the flux at the top of the atmosphere.

3.4.4 Rainfall

These 250 watts per square meter determine characteristics of our weather that are essential to life: the average surface temperature and the average rainfall. You get to estimate the surface temperature in Problem 5.43, once you learn the reasoning tool of dimensional analysis. Here, we will estimate the average rainfall.

If the box representing the atmosphere holds a evaporation water in rainfall

fixed amount of water—and over a long timescale, atmosphere

the amount is constant (it is our invariant)—then what goes into the box must come out of the box.

The inflow is evaporation; the outflow is rain. Therefore, to estimate the rainfall, estimate the evaporation—which is produced by the solar flux.

How much rain falls on Earth?

Rainfall is measured as a height of water per time—typically, inches or millimeters per year. To estimate global average rainfall, convert the supply of solar energy to the supply of rainwater. In other words, convert power per area to height per time. The structure of the conversion is power

height

area × ?? = time ,

(3.44)

where ?/? represents the conversion factor that we need to determine. To find what this conversion factor represents, we multiply both sides by area per power. The result is

?

area × height

? = power × time = volume

energy .

(3.45)

What physical quantity could this volume per energy be?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.4 Box models and conservation 81

We are trying to determine the amount of rain, so the volume in the numerator must be the volume of rain. Evaporating the water requires energy, so the energy in the denominator must be the energy required to evaporate that much water. The conversion factor is then the reciprocal of the heat of vaporization of water 𝐿vap, but expressed as an energy per volume. In Section 1.7.3, we estimated 𝐿vap as an energy per mass. To make it an energy per volume, just multiply by a mass per volume—namely, by 𝜌water: energy

mass

energy

×

=

.

(3.46)

mass

⏟⏟⏟⏟⏟ volume

⏟⏟⏟⏟⏟

volume

⏟⏟⏟⏟⏟

𝐿vap

𝜌water

𝜌water𝐿vap

Our conversion factor, volume per energy, is the reciprocal, 1/𝜌water𝐿vap.

Our estimate for the average rainfall then becomes solar flux going to evaporate water

𝜌

.

(3.47)

water𝐿vap

For the numerator, we cannot just use 𝐹, the full solar flux at the top of the atmosphere. Rather, the numerator incorporates several dimensionless ratios that account for the hoops through which sunlight must jump in order to reach the surface and evaporate water:

0.25

averaging the intercepted flux over the whole surface of the Earth (Section 3.4.3)

0.7

the fraction not reflected at the top of the atmosphere 0.7

of the sunlight not reflected, the fraction reaching the surface (the other 30 percent is absorbed in the atmosphere)

× 0.7

of the sunlight reaching the surface, the fraction reaching the oceans (the other 30 percent mostly warms land)

= 0.09

fraction of full flux 𝐹 that evaporates water (including averaging the full flux over the whole surface)

The product of these four factors is roughly 9 percent. With 𝐿vap = 2.2 ×

106 joules per kilogram (which we estimated in Section 1.7.3), our rainfall estimate becomes roughly

𝐹

fraction

1300

⏞⏞⏞ Wm

⏞⏞−2

⏞⏞ × 0.09

⏞

≈ 5.3×10−8 m

103 kg m−3

s

.

(3.48)

⏟⏟⏟⏟⏟⏟⏟ × 2.2×106 J kg−3

⏟⏟⏟⏟⏟⏟⏟⏟⏟

𝜌water

𝐿vap

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

82

3 Symmetry and conservation

The length in the numerator is tiny and hard to perceive. Therefore, the common time unit for rainfall is a year rather than a second. To convert the rainfall estimate to meters per year, multiply by 1: 5.3×10−8 m 3×107 s

1.6 m

×

≈

(3.49)

s

1 yr

yr

(about 64 inches per year). Not bad: Including all forms of falling water, such as snow, the world average is 0.99 meters per year—slightly higher over the oceans and slightly lower over land (where it is 0.72 meters per year). The moderate discrepancy between our estimate and the actual average arises because some sunlight warms water without evaporating it. To reflect this effect, our table on page 81 needs one more fraction (≈ 2/3).

Problem 3.30

Solar luminosity

Estimate the solar luminosity—the power output of the Sun (say, in watts)—based on the solar flux at the top of the Earth's atmosphere.

Problem 3.31

Total solar power falling on Earth

Estimate the total solar power falling on the Earth's surface. How does it compare to the world energy consumption?

Problem 3.32

Explaining the difference between ocean and land rainfall Why is the average rainfall over land lower than over the ocean?

3.4.5 Residence times

Because of evaporation, the atmosphere contains a lot of water: roughly 1.3×1016 kilograms—as vapor, liquid, and solid. This mass tells us the residence time: how long a water molecule remains in the atmosphere before it falls back to the Earth as precipitation (the overall name for rain, snow, or hail). The estimate will illustrate a new way to use box models.

Here is the box representing the water in the atmosphere (assumed to need only one box). The box is filled by evaporation and emptied by rainfall.

evaporation

mwater

rainfall

in atmosphere

Imagine that the box is a water hose holding a mass 𝑚water. How long does a water molecule take to get from one end of the hose to other? This time is the average time taken by a water molecule from evaporation until its 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.4 Box models and conservation 83

return to the Earth as precipitation. In the box model, the time is the time to completely fill the box. This time constant, denoted 𝜏, is mass of water in the atmosphere

𝜏 = rate of inflow or outflow, as a mass per time .

(3.50)

The numerator is 𝑚water. For the denominator, we convert rainfall, which is a speed (for example, in meters per year), to a mass flow rate (mass per time). Let's name the rainfall speed 𝑣rainfall. The corresponding mass flux is, using our results from Section 3.4.2, 𝜌water𝑣rainfall: mass flux = density

⏟⏟⏟⏟⏟ × flow speed

⏟⏟⏟⏟⏟⏟⏟ = 𝜌water𝑣rainfall.

(3.51)

𝜌water

𝑣rainfall

Flux is flow per area, so we multiply mass flux by the Earth's surface area 𝐴Earth to get the mass flow:

mass flow = 𝜌water𝑣rainfall 𝐴Earth.

(3.52)

At this rate, the fill time is

𝜏 =

𝑚water

𝜌

.

(3.53)

water𝑣rainfall 𝐴Earth

There are two ways to evaluate this time: the direct but less insightful method, and the less direct but more insightful method. Let's first do the direct method, so that we at least have an estimate for 𝜏: 𝜏 ∼

1.3×1016 kg

≈ 2.5×10−2 yr,

(3.54)

103 kg m−3 × 1 m yr−1 × 4𝜋 × (6×106 m)2

which is roughly 10 days. Therefore, after evaporating, water remains in the atmosphere for roughly 10 days.

For the less direct but more insightful method, notice which quantities are not reasonably sized—that is, not graspable by our minds—namely, 𝑚water and 𝐴Earth. But the combination 𝑚water/𝜌water𝐴Earth is reasonably sized: 𝑚water

𝜌

∼

1.3×1016 kg

water 𝐴Earth

103 kg m−3 × 4𝜋 × (6×106 m)2 ≈ 2.5×10−2 m.

(3.55)

This length, 2.5 centimeters, has a physical interpretation. If all water, snow, and vapor fell out of the atmosphere to the surface of the Earth, it would form an additional global ocean 2.5 centimeters deep.

Rainfall takes away 100 centimeters per year. Therefore, draining this ocean, with a 2.5-centimeter depth, requires 2.5×10−2 years or about 10 days. This time is, once again, the residence time of water in the atmosphere.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

84

3 Symmetry and conservation

3.5 Drag using conservation of energy

A box model will next help us estimate drag forces. Drag, one of the most difficult subjects in physics, is also one of the most important forces in everyday life. If it weren't for drag, bicycling, flying, and driving would be a breeze. Because of drag, locomotion requires energy. Rigorously calculating a drag force requires solving the Navier–Stokes equations: (𝐯⋅∇)𝐯 + ∂𝐯

∂𝑡 = −1𝜌∇𝑝 + 𝜈∇2𝐯.

(3.56)

They are coupled, nonlinear, partial-differential equations. You could read many volumes describing the mathematics to solve these equations. Even then, solutions are known only in a few circumstances—for example, a sphere moving slowly in a viscous fluid or moving at any speed in a nonviscous fluid. However, a nonviscous fluid—what Feynman [14, Section II-40-2], quoting John von Neumann, rightly disparages as「dry water」—is particularly irrelevant to real life because viscosity is the cause of drag, so a zero-viscosity solution predicts zero drag! Using a box model and conservation of energy is a simple and insightful alternative.

3.5.1 Box model for drag

We will first estimate the energy lost to drag as an ob-Acs

v

ject moves through a fluid, as in Section 3.2.1. From the energy, we will find the drag force. To quantify the the d

problem, imagine pushing an object of cross-sectional area 𝐴cs at speed 𝑣 for a distance 𝑑. The object sweeps out a tube of fluid.

(The tube length 𝑑 is arbitrary, but it will cancel out of the force.) How much energy is consumed by drag?

Energy is consumed because the object gives kinetic energy to the fluid (say, water or air); viscosity, as we will model in Section 6.4.4, then turns this energy into heat. The kinetic energy depends on the mass of the fluid and on the speed it is given. The mass of fluid in the tube is 𝜌𝐴cs𝑑, where 𝜌 is the fluid density. The speed imparted to the fluid is roughly the speed of the object, which is 𝑣. Therefore, the kinetic energy given to the fluid is roughly 𝜌𝐴cs𝑣2𝑑:

𝐸kinetic ∼ 𝜌𝐴cs𝑑

⏟ × 𝑣2 = 𝜌𝐴cs𝑣2𝑑.

(3.57)

mass

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 85

This calculation ignores the factor of one-half in the definition of kinetic energy. However, the other approximations, such as assuming that only the swept-out fluid is affected or that all the swept-out fluid gets speed 𝑣, are at least as inaccurate. For this rough calculation, there is little point in including the factor of one-half.

This kinetic energy is roughly the energy converted into heat. Therefore, the energy lost to drag is roughly 𝜌𝐴cs𝑣2𝑑. The drag force is then given by energy lost to drag

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟ = drag force

⏟⏟⏟⏟⏟ × distance

⏟⏟⏟⏟⏟ .

(3.58)

∼𝜌𝐴cs𝑣2𝑑

𝐹drag

𝑑

Now we can solve for the drag force:

𝐹drag ∼ 𝜌𝐴cs𝑣2.

(3.59)

As expected, the arbitrary distance 𝑑 has canceled out.

3.5.2 Testing the analysis with a home experiment To test this analysis, try the following home experiment. Photocopy or print this page at 200 percent enlargement (a factor of 2 larger in width and height), cut out the template, and tape the two straight edges together to make a cone:

⟶

(3.60)

3.5 cm

We could use many other shapes. However, a cone is easy to construct, and also falls without swishing back and forth (as a sheet of paper would) or flipping over (as long as you drop it point down).

We'll test the analysis by predicting the cone's terminal speed: that is, its steady speed while falling. When the cone is falling at this constant speed, its acceleration is zero, so the net force on it is, by Newton's second law, also zero. Thus, the drag force 𝐹drag equals the cone's weight 𝑚𝑔

(where 𝑚 is the cone's mass and 𝑔 is the gravitational acceleration): 𝜌air𝑣2𝐴cs ∼ 𝑚𝑔.

(3.61)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

86

3 Symmetry and conservation

The terminal speed thus reveals the drag force. (Even though the drag force equals the weight, the left side is only an approximation to the drag force, so we connect the left and right sides with a single approximation sign ∼.) The terminal speed 𝑣term is then

𝑣term ∼

𝑚𝑔

𝐴

.

(3.62)

cs𝜌air

The mass of the cone is

𝑚 = 𝐴paper × areal density of paper.

⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟⏟

(3.63)

𝜎paper

Here, 𝐴paper is the area of the cone template; and the areal density 𝜎paper, named in analogy to the regular (volume) density, is the mass per area of paper. Although areal density seems like a strange quantity to define, it is used worldwide to describe the「weight」of different papers.

The quotient 𝑚/𝐴cs contains the ratio 𝐴paper/𝐴cs. Rather than estimating both areas and finding their ratio, let's estimate the ratio directly.

How does the cross-sectional area 𝐴 cs compare to the area of the paper?

Because the cone's circumference is three-quarters of the circum-r

ference of the full circle, its cross-sectional radius is three-quar-co

ters of the radius 𝑟 of the template circle. Therefore, ne circumference

2

𝐴cs = 𝜋 (34𝑟) .

(3.64)

Because the template is three-quarters of a full circle, 𝐴paper = 34𝜋𝑟2.

(3.65)

The paper area has one factor of three-quarters, whereas the cross-sectional area has two factors of three-quarters, so 𝐴paper/𝐴cs = 4/3. Now 𝑣term simplifies as follows:

𝑚

1/2

1/2

⎛

4

𝐴

⏞⏞⏞⏞⏞⏞⏞ × 𝑔⎞

⎛

⎞

𝑣

⎜⎜ paper 𝜎paper

⎟⎟

⎜⎜ 3𝜎paper 𝑔⎟⎟

term ∼ ⎜

⎜⎜

𝐴

⎟⎟ = ⎜⎜

⎟⎟ .

(3.66)

cs 𝜌air

⎟

⎜ 𝜌air ⎟

⎝

⎠

⎝

⎠

The only unfamiliar number is the areal density 𝜎paper, the mass per area of paper. Fortunately, areal density is used commercially, so most reams of printer paper state their areal density: typically, 80 grams per square meter.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 87

Is this 𝜎 paper consistent with the estimates for a dollar bill in Section 1.1?

There we estimated that the thickness 𝑡 of a dollar bill, or of paper in general, is approximately 0.01 centimeters. The regular (volume) density 𝜌 would then be 0.8 grams per cubic centimeter:

𝜎

g

𝜌

paper

paper =

𝑡 ≈ 80 g m−2 × 1 m2 = 0.8

10−2 cm 104 cm2

cm3 .

(3.67)

This density, slightly below the density of water, is a good guess for the density of paper, which originates as wood (which barely floats on water).

Therefore, our estimate in Section 1.1 is consistent with the proposed areal density of 80 grams per square meter.

After putting in the constants, the cone's terminal speed is predicted to be roughly 0.9 meters per second:

𝜎

1/2

paper

𝑔

⎛⎜

⏞⏞⏞⏞⏞⏞⏞⏞⏞ ⏞⏞⏞⏞⏞⎞⎟

𝑣

⎜⎜4 8×10−2 kgm−2 × 10ms−2 ⎟⎟

term ∼ ⎜

⎜⎜

⎟ ≈ 0.9 m s−1.

(3.68)

⎜3 ×

1.2 kg m−3

⎟

⏟⏟⏟⏟⏟

⎟⎟

⎝

𝜌air

⎠

To test the prediction and, with it, the analysis justifying it, I held the cone slightly above my head, from about 2 meters high. After I let the cone go, it fell for almost exactly 2 seconds before it hit the ground—for a speed of roughly 1 meter per second, very close to the prediction. Box models and conservation triumph again!

3.5.3 Cycling

In introducing the analysis of drag, I said that drag is one of the most important physical effects in everyday life. Our analysis of drag will now help us understand the physics of a fantastically efficient form of locomotion—cycling (for its efficiency, see Problem 3.34).

What is the world-record cycling speed?

The first task is to define the kind of world record. Let's analyze cycling on level ground using a regular bicycle, even though faster speeds are possible riding downhill or on special bicycles. In bicycling, energy goes into rolling resistance, friction in the chain and gears, and air drag. The importance of drag rises rapidly with speed, due to the factor of 𝑣2 in the drag force, so at high-enough speeds drag is the dominant consumer of energy.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

88

3 Symmetry and conservation

Therefore, let's simplify the analysis by assuming that drag is the only consumer of energy. At the maximum cycling speed, the power consumed by drag equals the maximum power that the rider can supply. The problem therefore divides into two estimates: the power consumed by drag (𝑃drag) and the power that an athlete can supply (𝑃athlete).

Power is force times velocity:

energy

power = time = force×distance

time

= force × velocity.

(3.69)

Therefore,

𝑃drag = 𝐹drag𝑣max ∼ 𝜌𝑣3𝐴cs.

(3.70)

Setting 𝑃drag = 𝑃athlete allows us to solve for the maximum speed: 1/3

𝑣max ∼ ( 𝑃athlete

𝜌

) ,

(3.71)

air 𝐴cs

where 𝐴cs is the cyclist's cross-sectional area. In Section 1.7.2, we estimated 𝑃athlete as 300 watts. To estimate the cross-sectional area, divide it into a width and a height. The width is a body width—say, 0.4 meters. A racing cyclist crouches, so the height is roughly 1 meter rather than a full 2 meters.

Then 𝐴cs is roughly 0.4 square meters.

Plugging in the numbers gives

1/3

𝑣max ∼ (

300 W

.

(3.72)

1 kg m−3 × 0.4 m2 )

That formula, with its mix of watts, meters, and seconds, looks suspicious. Are the units correct?

Let's translate a watt stepwise into meters, kilograms, and seconds, using the definitions of a watt, joule, and newton: kg m

W ≡ Js,

J ≡ N m,

N ≡ s2 .

(3.73)

The three definitions are represented in the next divide-and-conquer tree, one definition at each nonleaf node. Propagating the leaves toward the root gives us the following expression for the watt in terms of meters, kilograms, and seconds (the fundamental units in the SI system): kg m2

W ≡ s3 .

(3.74)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 89

The units in 𝑣max become

W

kg m2 s−3

W

1/3

⎛⎜ ⏞⏞⏞⏞⏞⏞⏞

⎜

⎞

1/3

⎜ kg m2 s−3 ⎟

⎜

⎟

⎜

⎟ = ( s−3

.

(3.75)

⎜

⎟

kg m−3 × m2 ⎟⎟

m−3 )

J

⎝

⎠

kg m2 s−2

s−1

The kilograms cancel, as do the square meters. The cube root then contains only meters cubed over seconds cubed; therefore, the units for 𝑣max are meters per N

m

second.

kg m s−2

Let's estimate how many meters per second. Don't let the cube root frighten you into using a calculator. We kg

m

s−2

can do the arithmetic mentally, if we massage (adjust) the numbers slightly. If only the power were 400 watts (or instead the area were 0.3 square meters)! Instead of wishing, make it so—and don't worry about the loss of accuracy: Because we have neglected the drag coefficient, our speed will be approximate anyway. Then the cube root becomes an easy calculation:

300 400 W

1/3

𝑣

⎞

max ∼ ⎛

⎜

⎟ = (1000)1/3 m s−1 = 10 m s−1.

(3.76)

⎝1 kg m−3 × 0.4 m2 ⎠

In more familiar units, the record speed is 22 miles per hour or 36 kilometers per hour. As a comparison, the world 1-hour record—cycling as far as possible in 1 hour—is 49.7 kilometers or 30.9 miles, set in 2005 by Ondřej Sosenka. Our prediction, based on the conservation analysis of drag, is roughly 70 percent of the actual value.

How can such an estimate be considered useful?

High accuracy often requires analyzing and tracking many physical effects.

The calculations and bookkeeping can easily obscure the most important effect and its core idea, costing us insight and understanding. Therefore, almost everywhere in this book, the goal is an estimate within a factor of 2

or 3. That level of agreement is usually enough to convince us that our model contains the situation's essential features.

Here, our predicted speed is only 30 percent lower than the actual value, so our model of the energy cost of cycling must be broadly correct. Its main error arises from the factor of one-half that we ignored when estimating the drag force—as you can check by doing Problem 3.33.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

90

3 Symmetry and conservation

3.5.4 Fuel efficiency of automobiles

Bicycles, in many places, are overshadowed by cars. From the analysis of drag, we can estimate the fuel consumption of a car (at highway speeds).

Most of the world measures fuel consumption in liters of fuel per 100 kilometers of driving. The United States uses the reciprocal quantity, fuel efficiency—distance per volume of fuel—measured in miles per US gallon. To develop unit flexibility, we'll do the calculation using both systems.

For a bicycle, we compared powers: the power consumed by drag with the power supplied by an athlete. For a car, we are interested in the fuel consumption, which is related to the energy contained in the fuel. Therefore, we need to compare energies. For cars traveling at highway speeds, most of the energy is consumed fighting drag. Therefore, the energy consumed by drag equals the energy supplied by the fuel.

Driving a distance 𝑑, which will be 100 kilometers, consumes an energy 𝐸drag ∼ 𝜌air𝑣2𝐴cs 𝑑.

(3.77)

The fuel provides an energy

𝐸fuel ∼ energy density

⏟⏟⏟⏟⏟⏟⏟⏟⏟ × fuel mass

⏟⏟⏟⏟⏟ = ℰfuel 𝜌fuel𝑉fuel.

(3.78)

ℰfuel

𝜌fuel 𝑉fuel

Because 𝐸fuel ∼ 𝐸drag, the volume of fuel required is given by 𝐸

𝑉

drag

𝑣2𝐴cs

fuel ∼ 𝜌

∼ 𝜌air

𝑑.

(3.79)

fuelℰfuel

𝜌fuel ℰfuel

⏟⏟⏟⏟⏟⏟⏟

𝐴consumption

Because the left-hand side, 𝑉fuel, is a volume, the complicated factor in front of the travel distance 𝑑 must be an area. Let's make an abstraction by naming this area. Because it is proportional to fuel consumption, a self-documenting name is 𝐴consumption. Now let's estimate the quantities in it.

1. Density ratio 𝜌 air/𝜌 fuel. The density of gasoline is similar to the density of water, so the density ratio is roughly 10−3.

2. Speed 𝑣. A highway speed is roughly 100 kilometers per hour (60 miles per hour) or 30 meters per second. (A useful approximation for Americans is that 1 meter per second is roughly 2 miles per hour.) 3. Energy density ℰ fuel. We estimated this quantity Section 2.1 as roughly 10 kilocalories per gram or 40 megajoules per kilogram.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.5 Drag using conservation of energy 91

4. Cross-sectional area 𝐴 cs. A car's cross section is about 2 me-car

ters across by 1.5 meters high, so 𝐴cs ∼ 3 square meters.

1.5 m

(cross section)

With these values,

2 m

𝑣2

𝐴cs

⏞⏞⏞⏞⏞

𝐴

103 m2 s−2 × 3 m2

⏞

consumption ∼ 10−3 ×

≈ 8×10−8 m2.

(3.80)

4×107 J kg−1

⏟⏟⏟⏟⏟⏟⏟

ℰfuel

To find the fuel consumption, which is the volume of fuel per 100 kilometers of driving, simply multiply 𝐴consumption by 𝑑 = 100 kilometers or 105 meters, and then convert to liters to get 8 liters per 100 kilometers: 𝑉fuel ≈ 8×10−8 m2

⏟⏟⏟⏟⏟⏟⏟ × 105 m

⏟ × 103 ℓ = 8 ℓ.

(3.81)

1m3

𝐴consumption

𝑑

For the fuel efficiency, we use 𝐴consumption in the form 𝑑 = 𝑉fuel/𝐴consumption to find the distance traveled on 1 gallon of fuel, converting the gallon to cubic meters:

𝑉fuel

1

⏞ g

⏞ allon

⏞⏞⏞

4 ℓ

10−3 m3

𝑑 ∼

×

×

= 5×104 m.

(3.82)

8×10−8 m2

⏟⏟⏟⏟⏟⏟⏟ 1 gallon

1 ℓ

𝐴consumption

The struck-through exponent of 3 in the m3 indicates that the cubic meters became linear meters, as a result of cancellation with the m2 in the 𝐴consumption. The resulting distance is 50 kilometers or 30 miles. The predicted fuel efficiency is thus roughly 30 miles per gallon.

This prediction is very close to the official values. For example, for new mid-size American cars (in 2013), fuel efficiencies of nonelectric vehicles range from 16 to 43 miles per gallon, with a mean and median of 30 miles per gallon (7.8 liters per 100 kilometers).

The fuel-efficiency and fuel-consumption predictions are far more accurate than we deserve, given the many approximations! For example, we ignored all energy losses except for drag. We also used a very rough drag force 𝜌air𝑣2𝐴cs, derived from a reasonable but crude conservation argument. Yet, like Pippi Longstocking, we came out right anyway.

What went right?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

92

3 Symmetry and conservation

The analysis neglects two important factors, so such accuracy is possible only if these factors cancel. The first factor is the dimensionless constant hidden in the single approximation sign of the drag force: 𝐹drag ∼ 𝜌air𝐴cs𝑣2.

(3.83)

Including the dimensionless prefactor (shown in gray), the drag force is 𝐹drag = 12𝑐d 𝜌air𝐴cs𝑣2,

(3.84)

where 𝑐d is the drag coefficient (introduced in Section 3.2.1). The factor of one-half comes from the one-half in the definition of kinetic energy. The drag coefficient is the remaining adjustment, and its origin is the subject of Section 5.3.2. For now, we need to know only that, for a typical car, 𝑐d ≈ 1/2.

Therefore, the dimensionless prefactor hidden in the single approximation sign is approximately 1/4.

Based on this more accurate drag force, will cars use more or less than 8 liters of fuel per 100 kilometers?

Including the 𝑐d/2 reduces the drag force and the fuel consumption by a factor of 4. Therefore, cars would travel 120 miles on 1 gallon of fuel or would consume only 2 liters per 100 kilometers. This more careful prediction is far too optimistic—and far worse than the original, simpler estimate.

What other effect did we neglect?

The engine efficiency—a typical combustion engine, whether gasoline or human, is only about 25 percent efficient: An engine extracts only one-quarter of the combustion energy in the fuel; the remaining three-quarters turns into heat without doing mechanical work. Including this factor increases our estimate of the fuel consumption by a factor of 4.

The engine efficiency and the more accurate drag force together give the following estimate of the fuel consumption, with the new effect in gray: 1

𝑉

2 𝑐d

fuel ≈ 0.25 × 𝜌air𝑣2𝐴cs

𝜌

𝑑.

(3.85)

fuelℰfuel

The 0.25 in the denominator, from the engine efficiency, cancels the 12𝑐d in the numerator. That is why our carefree estimate, which neglected both factors, was so accurate. The moral, which I intend only half jokingly: Neglect many factors, so that the errors can cancel one another out.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum 93

Problem 3.33

Adjusting the cycling record

Our estimate of the world 1-hour record as roughly 35 kilometers (Section 3.5.3) ignored the drag coefficient. For a bicyclist, 𝑐d ≈ 1. Will including the drag coefficient improve or worsen the prediction in comparison with the actual world record (roughly 50 kilometers)? Answer that question before making the new prediction!

What is the revised prediction?

Problem 3.34

Bicyclist fuel efficiency

What is the fuel consumption and efficiency of a bicyclist powered by peanut butter? Express your estimate as an efficiency (miles per gallon of peanut butter) and a consumption (liters of peanut butter per 100 kilometers). How does a bicycle compare with a car?

3.6 Lift using conservation of momentum

If drag is a drag, our next force, which is the companion to drag, should lift our spirits. Using conservation and box models, we will estimate the power required to generate lift. There are two main cases: hovering flight—for example, a hummingbird—and forward flight. Compared to forward flight, hovering flight has one fewer parameter (there is no forward velocity), so let's begin with its analysis, for a bird of mass 𝑚.

3.6.1 Hovering: Hummingbirds

How much power does a hummingbird require to hover?

box

Hovering demands power because a hummingbird has weight: The Earth, via the gravitational field, supplies the hummingbird bird

with downward momentum. The Earth therefore loses downward downward

momentum or, equivalently, acquires upward momentum. (Thus, momentum

the Earth accelerates upward toward the hummingbird, although earth

very, very slowly.) This flow of momentum can be tracked with a box model. Let's draw the box around the Earth–hummingbird system and imagine the system as the whole universe. The box contains a fixed (constant) amount of downward momentum, so the gravitational field can transfer downward momentum only within the box. In particular, the field transfers downward momentum from the Earth to the hummingbird. This picture is a fancy way of saying that the Earth exerts a downward force on the hummingbird, but the fancy way shows us what the hovering hummingbird must do to stay aloft.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

94

3 Symmetry and conservation

box

If the hummingbird keeps this downward momentum, it would accumulate downward speed—and crash to the ground. Fortunately, the air

box has one more constituent: the fluid (air). The hummingbird gives the downward momentum to the air: It flaps its wings and sends air bird

downward. Lift, like drag, requires a fluid. (The air pushes down on the Earth, returning the downward momentum that the Earth lost via the gravitational field. Thus, the Earth does not accelerate.) earth

How much power is required to send air downward?

Power is force times speed. The force is the gravitational force 𝑚𝑔 that the hummingbird is unloading onto the air. Estimating the air's downward speed 𝑣𝑧 requires careful thought about the flow of momentum. The air carries the downward momentum supplied to the hummingbird. The momentum supply (a momentum rate or momentum per time) is area ∼ L2

the force 𝑚𝑔: Force is simply momentum per time. Because mo-vz

mentum flux is momentum per time per area, 𝑚𝑔 = momentum flux × area.

(3.86)

downward

mom. density

When we first studied flux, in Section 3.4.2, we derived that

∼ ρ airvz

flux of stuff = density of stuff × flow speed.

(3.87)

Because our stuff is momentum, this relation takes the particular form momentum flux = momentum density × flow speed.

(3.88)

Substituting this momentum flux into 𝑚𝑔 = momentum flux × area, 𝑚𝑔 = momentum density × flow speed × area.

(3.89)

Momentum density is momentum (𝑚air𝑣𝑧) per volume, so it is 𝜌air𝑣𝑧. The flow speed is 𝑣𝑧. Thus,

𝑚𝑔 = 𝜌air𝑣𝑧 × 𝑣𝑧 × area = 𝜌air𝑣2𝑧 × area.

(3.90)

To complete this equation, so that it gives us the downward velocity 𝑣𝑧, we need to estimate the area. It is the area over which the hummingbird directs air downward. It is roughly 𝐿2, where 𝐿 is the wingspan (wingtip to wingtip). Even though the wings do not fill that entire area, the relevant area is still 𝐿2, because the wings disturb air in a region whose size is comparable to their longest dimension. (For this reason, high-efficiency planes, such as gliders, have very long wings.)

Using 𝐿2 as the estimate for the area, we get 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum 95

𝑚𝑔 ∼ 𝜌air𝑣2𝑧𝐿2,

(3.91)

so the downward velocity is

𝑣𝑧 ∼

𝑚𝑔

𝜌air𝐿2 .

(3.92)

With this downward velocity and with the downward force 𝑚𝑔, the power 𝑃 (not to be confused with momentum!) is

𝑃 = 𝐹𝑣𝑧 ∼ 𝑚𝑔 𝑚𝑔

𝜌air𝐿2 .

(3.93)

Let's estimate this power for an actual hummingbird: the Calliope hummingbird, the smallest bird in North America. Its two relevant characteristics are the following:

wingspan 𝐿 ≈ 11 cm,

(3.94)

mass 𝑚 ≈ 2.5 g.

As the first step in estimating the hovering power, we'll estimate the downward air speed using our formula for 𝑣𝑧. The result is that, to stay aloft, the hummingbird sends air downward at roughly 1.3 meters per second: 𝑚𝑔

⏞⏞⏞⏞⏞⏞⏞

1/2

𝑣

2.5×10−2 N

⎞

𝑧 ∼ ⎛

⎜

⎟ ≈ 1.3 m s−1.

(3.95)

⎝ 1.2 kg m−3

⏟⏟⏟⏟⏟ × 1.2×10−2 m2

⏟⏟⏟⏟⏟⏟⏟⎠

𝜌air

𝐿2

The resulting power consumption is roughly 30 milliwatts: 𝑃 ∼ 2.5

⏟⏟×

⏟ 10−2

⏟⏟ N

⏟⏟ × 1.3 m s−1

⏟⏟⏟⏟⏟ ≈ 3

⏟×10−2

⏟⏟ W

⏟⏟ .

(3.96)

𝑚𝑔

𝑣𝑧

30 mW

(Because animal metabolism, like a car engine, is only about 25 percent efficient, the hummingbird needs to eat food at a rate corresponding to 120

milliwatts.)

This power seems small: Even an (incandescent) flashlight bulb, for example, requires a few watts. However, as a power per mass, it looks more significant:

𝑃𝑚 ∼ 3×10−2W ≈ 10 W

2.5×10−3 kg

kg.

(3.97)

In comparison, the world-champion cyclist Lance Armstrong, with one of the highest human power outputs, was measured to have a power output of 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

96

3 Symmetry and conservation

7 watts per kilogram (Section 1.7.2). However, for a chemically unenhanced world-class athlete, 5 watts per kilogram is a more typical value. According to our estimates, hummingbird muscles should be twice as powerful as this world-class human value! Even for a small bird, hovering is hard work.

Problem 3.35

Fueling hovering

How much nectar must a hummingbird drink, as a fraction of its body mass, in order to hover for its working day (roughly 8 hours)? By mass, nectar is roughly 50 percent sugar.

Problem 3.36

Human hovering

How much power would a person have to put out in order to hover by flapping his or her arms?

3.6.2 Lift in forward flight

Now that we understand the fundamental mechanism wing

of lift—discarding downward momentum by giving it to the air—we are ready to study forward flight: the body

L

v

flight of a migrating bird or of a plane. Forward flight is more complicated than hovering because forward wing

flight has two velocities: the plane's forward velocity 𝑣 and the downward component 𝑣𝑧 of the air's velocity after passing around the wing. In forward flight, 𝑣𝑧 depends not only on the plane's weight and wingspan, but also on the plane's forward velocity.

To stay aloft, the plane, like the hummingbird, must deflect air downward.

air

wing

v

(side view)

vz

The wing does this magic using complicated fluid mechanics, but we need not investigate it. All the gymnastics are hidden in the box. We need just the downward velocity 𝑣𝑧 required to keep the plane aloft, and the power required to give the air that much downward velocity. The power is, as with hovering, 𝑚𝑔𝑣𝑧. However, the downward velocity 𝑣𝑧 is not the same as in hovering.

It is determined by a slightly different momentum-flow diagram. It shows the air flow before and after it meets the wing.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.6 Lift using conservation of momentum

97

downward

mom. density

∼ ρ airvz

Before the air reaches the wing (the left tube), the air has zero downward momentum. As in the analysis of hovering flight, the Earth supplies downward momentum to the plane, which passes it onto the air. This downward momentum is carried away by the air after the wing (the right tube).

As with any flux, the rate of transfer of downward momentum is flux of downward momentum × area.

(3.98)

As in the analysis of the hummingbird, this rate must be 𝑚𝑔, so that the plane stays aloft. The first factor, the flux of downward momentum, is density of downward momentum × flow speed.

(3.99)

Therefore,

𝑚𝑔 = density of downward momentum × flow speed × area.

(3.100)

As in the analysis of hovering, the density of downward momentum is 𝜌𝑣𝑧.

In contrast to the analysis of hovering, where the stuff (downward momentum) is carried by the air moving downward, here the stuff is carried by air moving to the right. Thus, where the flow speed in hovering was the downward air speed 𝑣𝑧, in forward flight the flow speed is the forward velocity 𝑣.

As in the analysis of hovering, the relevant area is the squared wingspan 𝐿2, because the wings alter the airflow over a distance comparable to their longest dimension, which is their wingspan. You can see this effect in a NASA photograph of an airplane flying through a cloud of smoke. The giant swirl, known as the wake vortex, has a diameter comparable to the plane's wingspan. Large planes can generate vortices that flip over small planes. Thus, when coming in for landing, planes must maintain enough separation to give these vortices time to dissipate.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

98

3 Symmetry and conservation

With these estimates, the equation for 𝑣𝑧 becomes 𝑚𝑔

⏟ ∼

𝜌air𝑣𝑧

⏟

×

𝑣

⏟ × 𝐿2

⏟ .

(3.101)

transfer rate

downward-momentum density

flow speed

area

Now we can solve for the downward air speed: 𝑣𝑧 ∼ 𝑚𝑔

𝜌air𝑣𝐿2 .

(3.102)

Now we can estimate the power required to generate lift in forward flight: 𝑃 = force

⏟ × velocity

⏟⏟⏟⏟⏟ ∼ 𝑚𝑔 × 𝑚𝑔

𝜌

𝑚𝑔

𝑣

air𝑣𝐿2 = (𝑚𝑔)2

𝜌air𝑣𝐿2 .

(3.103)

𝑧

Here is a comparison of hovering and forward flight.

hovering

forward flight

deflection area

𝐿2

𝐿2

downward-momentum density

𝜌air𝑣𝑧

𝜌air𝑣𝑧

flow speed

𝑣𝑧

𝑣

downward-momentum flux

𝜌air𝑣2𝑧

𝜌air𝑣𝑧𝑣

downward-momentum flow 𝑚𝑔

𝜌air𝑣2𝑧𝐿2

𝜌air𝑣𝑧𝑣𝐿2

downward velocity 𝑣𝑧

𝑚𝑔/𝜌air𝐿2

𝑚𝑔/𝜌air𝑣𝐿2

power to generate lift (𝑚𝑔𝑣𝑧)

𝑚𝑔 𝑚𝑔/𝜌air𝐿2

(𝑚𝑔)2/𝜌air𝑣𝐿2

In contrast to hovering, in forward flight the power contains the forward velocity in the denominator—a location that would produce nonsense for hovering, where the forward velocity is zero.

As we did for hovering flight using the Calliope hummingbird, let's apply our knowledge of forward flight to an actual object. The object will be a Boeing 747-400 jumbo jet, and we will estimate the power that it requires in order to take off. A 747 has a wingspan 𝐿 of approximately 60 meters, and a maximum takeoff mass 𝑚 of approximately 4×105 kilograms (400 tons).

We'll estimate the power in two steps: the weight 𝑚𝑔 and then the downward air speed 𝑣𝑧. The weight is the easy step: It is just 4 × 106 newtons.

The downward air speed 𝑣𝑧 is 𝑚𝑔/𝜌air𝑣𝐿2. The only unknown quantity is the takeoff speed 𝑣. You can estimate it by estimating the plane's acceleration 𝑎 while taxiing on the runway and by estimating the duration of the 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.7 Summary and further problems 99

acceleration. When I last flew on a 747, I measured the acceleration by suspending my key chain from a string and estimating the angle 𝜃 that it made with vertical (perpendicular to the ground). Then tan 𝜃 = 𝑎/𝑔. For small 𝜃, the relation simplifies to 𝑎/𝑔 ≈ 𝜃. I found 𝜃 ≈ 0.2, so the acceleration was about 0.2𝑔 or 2 meters per second per second. This acceleration lasted for about 40 seconds, giving a takeoff speed of 𝑣 ≈ 80 meters per second (180

miles per hour).

The resulting downward speed 𝑣𝑧 is roughly 12 meters per second: 𝑚𝑔

⏞⏞⏞⏞⏞

𝑣

4×106 N

𝑧 ∼

≈ 12 m s−1.

(3.104)

1.2 kg m−3

⏟⏟⏟⏟⏟ × 80 m s−1

⏟⏟⏟⏟⏟ × 3.6×103 m2

⏟⏟⏟⏟⏟⏟⏟

𝜌air

𝑣

𝐿2

Then the power required to generate lift is roughly 50 megawatts: 𝑃 ∼ 𝑚𝑔𝑣𝑧 ≈ 4×106 N × 12 m s−1 ≈ 5×107 W.

(3.105)

Let's see whether these estimates are reasonable. According to the plane's technical documentation, the 747-400's four engines together can provide roughly 1 meganewton of thrust. This thrust can accelerate the plane, with a mass of 4×105 kilograms, at 2.5 meters per second. This value is in good agreement with my estimate of 2 meters per second, made by suspending a key chain from a string and turning it into a plumb line.

As another check: At takeoff, when 𝑣 is roughly 80 meters per second, the meganewton of thrust corresponds to a power output 𝐹𝑣 of 80 megawatts.

This output is comparable to our estimate of 50 megawatts for the power to lift the plane off the ground. After liftoff, the engines use some of their power to lift the plane and some to accelerate the plane, because the plane still needs to reach its cruising speed of 250 meters per second.

Symmetry and conservation make even fluid dynamics tractable.

3.7 Summary and further problems

In the midst of change, find what does not change—the invariant or conserved quantity. Finding these quantities simplifies problems: We focus on the few quantities that do not change rather than on the many ways in which quantities do change. An instance of this idea with wide application is a box model, where what goes in must come out. By choosing suitable boxes, we could estimate rainfalls and drag forces, and understand lift.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

100

3 Symmetry and conservation

Problem 3.37

Raindrop speed

Use the drag force 𝐹drag ∼ 𝜌𝐴cs𝑣2 to estimate the terminal speed of a typical raindrop with a diameter of 0.5 centimeters. How could you check the prediction?

Problem 3.38

Average value of sin squared

Use symmetry to find the average value of sin2𝑡 over the interval 𝑡 = [0, 𝜋].

Problem 3.39

Moment of inertia of a spherical shell

The moment of inertia of an object about an axis of rotation is axis

∑ 𝑚𝑖𝑑2𝑖,

(3.106)

summed over all mass points 𝑖, where 𝑑𝑖 is the distance of the r

point from an axis of rotation. Use symmetry to find the moment of inertia of a spherical shell with mass 𝑚 and radius 𝑟 about an axis through its center. You shouldn't need to do any integrals!

Problem 3.40

Flying bicyclist

Estimate the wingspan a world-champion bicyclist would require in order to get enough lift for takeoff.

Problem 3.41

Maximum-gain frequency for a second-order system In this problem, you use symmetry to maximize L

C

the gain of an 𝐿𝑅𝐶 circuit or a spring–mass system Vin Vout

with damping (using the analogy in Section 2.4.1).

R

The gain 𝐺, which is the amplitude ratio 𝑉out/𝑉in, depends on the signal's angular frequency 𝜔: ground

𝑗𝜔

𝐺(𝜔) =

𝜔0

(3.107)

1 + 𝑗 𝜔

𝑄 𝜔 − 𝜔2

0

𝜔20

where 𝑗 = −1, 𝜔0 is the natural frequency of the system, and 𝑄, the quality factor, is a dimensionless measure of the damping. Don't worry about where the gain formula comes from: You can derive it using the impedance method (Problem 2.22), but the purpose of this problem is to maximize its magnitude ∣𝐺(𝜔)∣. Do so by finding a symmetry operation on 𝜔 that leaves ∣𝐺(𝜔)∣ invariant.

Problem 3.42

Runway length

Estimate the runway length required by a 747 in order to take off.

Problem 3.43

Hovering versus flying

At what forward flight speed does the hummingbird of Section 3.6.1 require as much power to generate lift as it would to hover? How does this speed compare to its typical flight speed?

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

3.7 Summary and further problems 101

Problem 3.44

Resistive grid

In an infinite grid of 1-ohm resistors, what is the resistance measured across one resistor?

To measure resistance, an ohmmeter injects a current Ω

𝐼 at one terminal (for simplicity, imagine that 𝐼 = 1 ampere). It removes the same current from the other terminal, and measures the resulting voltage difference 𝑉 between the terminals. The resistance is 𝑅 = 𝑉/𝐼.

Hint: Use symmetry. But it's still a hard problem!

Problem 3.45

Inertia tensor

Here is an inertia tensor (the generalization of moment of inertia) of a particular object, calculated in an ill-chosen (but Cartesian) coordinate system:

⎛ 4 0 0

⎜⎜0 5 4⎞⎟⎟

(3.108)

⎝ 0 4 5 ⎠

a. Change the coordinate system to a set of principal axes, where the inertia tensor has the diagonal form

⎛ 𝐼xx 0

0

⎜⎜ 0 𝐼

⎞

yy

0 ⎟⎟

(3.109)

⎝ 0

0 𝐼zz ⎠

and give the principal moments of inertia 𝐼xx, 𝐼yy, and 𝐼zz. Hint: Which properties of a matrix are invariant when changing coordinate systems?

b. Give an example of an object with a similar inertia tensor. Rhetorical question: In which coordinate system is it easier to think of such an object?

This problem was inspired by a problem on the physics written qualifying exam during my days as a PhD student. The problem required diagonalizing an inertia tensor, and there was too little time to rederive or even apply the change-of-basis formulas. Time pressure sometimes pushes one toward better solutions!

Problem 3.46

Temperature distribution on an infinite sheet 1

On this infinite, uniform sheet, the 𝑥 axis is held at zero tempera-

=

ture, and the 𝑦 axis is held at unit temperature (𝑇 = 1). Find the T

T = 0

temperature everywhere (except the origin!). Use Cartesian coordinates 𝑇(𝑥, 𝑦) or polar coordinates 𝑇(𝑟, 𝜃), whichever choice makes it easier to describe the temperature.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

4Proportional reasoning

4.1 Population scaling

103

4.2 Finding scaling exponents

105

4.3 Scaling exponents in fluid mechanics

117

4.4 Scaling exponents in mathematics

123

4.5 Logarithmic scales in two dimensions

126

4.6 Optimizing flight speed

128

4.7 Summary and further problems

