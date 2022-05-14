## 0201. Abstraction

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

Try, for example, to manage the millions of files on a computer — even my laptop says that it has almost 3 million files. Without any organization, with all the files in one monster directory or folder, you could never find information that you need. However, simply using divide and conquer by dividing the files into groups — the first 100 files by date, the second 100 files by date, and so on — does not disperse the chaos. A better solution is to organize the millions of files into a hierarchy: as a tree of folders and subfolders. The elements in this hierarchy get names — for example,「photos of the children」or

「files for typesetting this book」 — and these names guide us to the needed information.

Naming — or, more technically, abstraction — is our other tool for organizing complexity. A name or an abstraction gets its power from its reusability.

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

For a hydrocarbon with eight carbons — such as octane, a prime component of motor fuel — simply multiply this reaction by 8: (CH2)8 + 12 O2 ⟶ 8 CO2 + 8 H2O + lots of energy.

(2.3)

(The two additional hydrogens at the left and right ends of octane are not worth worrying about.)

How much energy is released by burning one CH2 unit?

To make this estimate, use the table of bond bond energy

energies. It gives the energy required to break kcal

kJ

eV

(not make) a chemical bond — for example, be-

( mol) (mol) (bond)

tween carbon and hydrogen. However, there

is no unique carbon–hydrogen (C–H) bond. C — H

99

414

4.3

The carbon–hydrogen bonds in methane are O — H

111

464

4.8

different from the carbon–hydrogen bonds in C — C

83

347

3.6

ethane. To make a reusable idea, we neglect C — O

86

360

3.7

those differences — placing them below our H — H

104

435

4.5

abstraction barrier — and make an abstraction C — N

73

305

3.2

called the carbon–hydrogen bond. So the ta- N — H

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

The left side of the reaction has two carbon–hy- 1 × C — C

1 × 83

1 × 347

drogen bonds,

2 × C — H

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

2 × O — H

2 × 111

2 × 464

The net result is, per mole of CH2, an energy release of Total 606

2535

606 minus 460 kilocalories, or approximately 145 kilocalories (610 kilojoules). Equivalently, it is also about 6 electron volts per CH2 unit — about 1.5 chemical bonds' worth of energy. The combustion energy is also useful as an energy per mass rather than per mole. A mole of CH2 units weighs 14 grams. Therefore, 145 kilocalories per mole is roughly 10 kilocalories or 40 kilojoules per gram. This energy density is worth memorizing because it gives the energy released by burning oil and gasoline or by metabolizing fat (even though fat is not a pure hydrocarbon).

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

site, gives actual combustion energies for plant and animal fuel sources (with pure hydrogen included for fun). The penultimate entry, stearic acid, is a large component of animal fat; animals store energy in a substance with an energy density comparable to the energy density in gasoline — roughly 10 kilocalories or 40 kilojoules per gram. Plants, on the other hand, store energy in starch, which is a chain of glucose units; glucose has an energy density of only roughly 4 kilocalories per gram. This value, the energy density of food carbohydrates (sugars and starches), is also worth memorizing.

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

flecting the alternative endings of the game. Each layer represents one flip. The game ends at a leaf, when one player has tossed heads. The shaded leaves show the first player's wins — for example, after H, TTH, or TTTTH. The probabili-H

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

1000 hours: roughly a year of work, allowing for other projects. (A few problems stapled together become a PhD.) In the course, each 2-week module required about 30 hours — approximately the geometric mean of the two endpoints. The modules were just the right length to help us cross the bridge from homework to research.

Problem 2.9

Horizon distance

How far is the horizon when you are standing at the shore? Hint: It's farther for an adult than for a child.

Problem 2.10

Distance to a ship

Standing at the shore, you see a ship (drawn to scale) with a 10-meter mast sail into the distance and disappear from view. How far away was it when it disappeared?

As further evidence that the geometric mean is a useful abstraction, the idea appears even when there is no geometric construction to produce it, such as in making gut estimates. We used this method in Section 1.6 to estimate the population density and then the population of the United States. Let's practice by estimating the oil imports of the United States in barrels per year — without the divide-and-conquer reasoning of Section 1.4.

The method requires that the gut supply a lower and an upper bound. My gut reports back that it would feel fairly surprised if the imports were less than 10 million barrels per year. On the upper end, my gut would be fairly surprised if the imports were higher than 1 trillion barrels per year — a barrel is a lot of oil, and a trillion is a large number!

You might wonder how your gut too can come up with such large numbers and how you can have any confidence in them. Admittedly, I have practiced a lot. But you can practice too. The key is the practice effectively. First, have the courage to guess even when you feel anxious about it (I feel this anxiety still, so I practice this courage often). Second, compare your guess to values in which you can place more confidence — for example, to your own more careful estimates or to official values. The comparison helps calibrate your gut (your right brain) to these large magnitudes. You will find a growing and justified confidence in your judgment of magnitude.

My best guess for the amount is the geometric mean of the lower and upper estimates:

10 million × 1 trillion barrels

year .

(2.12)

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

36

2 Abstraction

The result is roughly 3 billion barrels per year — close to the our estimate using divide and conquer and close to the true value. In contrast, the arithmetic mean would have produced an estimate of 500 billion barrels per year, which is far too high.

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

In the circuit, the voltage source — the 𝑉in on its left side — supplies a current that flows through the inductor (a wire wrapped around an iron rod) and capacitor (two metal plates separated by air). As current flows through the capacitor, it alters the charge on the capacitor. This「charge」is confusingly named, because the net charge on the capacitor remains zero. Instead, 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

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

These variables describe the state of the systems and how that state changes: They are the kinematics. But without the causes of the motion — the dynamics — the systems remain lifeless. In the mechanical system, dynamics results from force, which produces acceleration: 𝑎 = 𝐹𝑚.

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

(the parallel-combination operator has higher priority than — is computed before — the addition). This expression more plainly reflects the structure of the system, and our reasoning about it, than does the version 𝑅 = 1 Ω + 1 Ω × 𝑅

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

Voltage is an effort. Current, which results from the effort, is a flow. Therefore, the more general form — one step higher on the abstraction ladder — is effort = resistance × flow.

(2.38)

In this form, Newton's second law,

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

44

2 Abstraction

force = mass × acceleration,

(2.39)

identifies force as the effort, mass as the resistance, and acceleration as the flow.

Because the spring can wiggle either mass, just as current can flow through either of two parallel resistors, the spring feels a resistance equal to the parallel combination of the resistances — namely, 𝑚 ∥ 𝑀.

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

This more general resistance, which depends on the frequency, is called impedance and denoted 𝑍. (In the analogy of Section 2.4.1 between capacitors and springs, we found that capacitor offered a resistance to being charged of 1/𝐶. Impedance, the result of an analogy between capacitors and resistors, contains 1/𝐶 as well, but also contains the frequency in the 1/𝑗𝜔 factor.) Using impedance, we can describe what happens to any sinusoidal signal in a circuit containing capacitors. Our thinking is aided by the compact notation — the capacitive impedance 𝑍𝐶 (or even 𝑅𝐶). The notation hides the details of the capacitor differential equation and allows us to transfer our intuition about resistance and flow to a broader class of circuits.

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

This product is the circuit's time constant — usually denoted 𝜏.

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

After one time constant 𝜏, the capacitor voltage falls by a factor of 𝑒 toward its final value — here, from 𝑉0 to 𝑉0/𝑒. The 1/𝑒 time is our first interpretation of the time constant. Furthermore, if the capacitor voltage had decayed at its initial rate (just after 𝑡 = 0), it would have reached zero voltage after one time constant 𝜏 — the second interpretation of the time constant.

The time-constant abstraction hides — abstracts away — the details that produced it: here, electrical resistance and capacitance. Nonelectrical systems can also have a time constant but produce it by a different mechanism.

Our high-level understanding of time constants, because it is not limited to electrical systems, will help us transfer our understanding of the electrical low-pass filter to nonelectrical systems. In particular, we are now ready to understand heat flow in thermal systems.

Problem 2.19

Impedance of an inductor

An inductor has the voltage–current relation 𝑉 = 𝐿𝑑𝐼

𝑑𝑡 ,

(2.56)

where 𝐿 is the inductance. Find an inductor's frequency-dependent impedance 𝑍𝐿. After finding this impedance, you can analyze any linear circuit as if it were composed only of resistors.

2.4.5 Thermal systems

The 𝑅𝐶 circuit is a model for thermal systems — which are not obviously connected to circuits. In a thermal system, temperature difference, the analog of voltage difference, produces a current of energy. Energy current, in less fancy words, is heat flow. Furthermore, the current is proportional to the temperature difference — just as electric current is proportional to voltage difference. In both systems, flow is proportional to effort. Therefore, heat flow can be understood by using circuit analogies.

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

tea is a low-pass filter for temperature variations. It transmits this low-frequency input temperature signal almost unchanged to the output — to the tea temperature. Therefore, the inside (tea) temperature almost exactly follows the outside (room) temperature.

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

It turns out that the average temperature indoors is equal to the average temperature outdoors! To see why, let's think carefully about the reference temperature (our thermal analog of ground). Before, in the analysis of the forgotten tea mug, our reference temperature was the average indoor temperature. Because we are now trying to determine this value, let's instead use a known convenient reference temperature — for example, the cool 10 ∘C, which makes for round numbers in Celsius or Fahrenheit (50 ∘F).

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

Let's handle each piece in turn — we are using divide-and-conquer reasoning again. We just analyzed the varying piece: It passes through the house low-pass filter and, with 𝜔𝜏 ≈ 3, it shrinks significantly in amplitude. In contrast, the nonvarying part, which is the average outside temperature, has zero frequency by definition. Therefore, its dimensionless parameter 𝜔𝜏 is exactly 0. This signal passes through the house low-pass filter with a gain of 1. As a result, the average output signal (the inside temperature) is also 60 ∘F: the same steady 10 ∘F signal measured relative to the reference temperature of 50 ∘F.

2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

2.5 Summary and further problems 53

The 10 ∘F peak-to-peak inside-temperature amplitude is a variation around 60 ∘F. Therefore, the inside temperature varies between 55 ∘F and 65 ∘F

(13 ∘C to 18 ∘C). Indoors, when I am not often running or otherwise generating much heat, I feel comfortable at 68 ∘F (20 ∘C). So, as this circuit model of heat flow predicts, I wore a sweater day and night in the Cape Town house. (For more on using 𝑅𝐶 circuit analogies for building design, see the

「Design masterclass」article by Doug King [30].) Problem 2.20

When is the house coldest?

Based on the general form for the gain, 1/(1+𝑗𝜔𝜏), when in the day will the Cape Town house be the coldest, assuming that the outside is coldest at midnight?

2.5 Summary and further problems

Geometric means, impedances, low-pass filters — these ideas are all abstractions. An abstraction connects seemingly random details into a higher-level structure that allows us to transfer knowledge and insights. By building abstractions, we amplify our intelligence.

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
