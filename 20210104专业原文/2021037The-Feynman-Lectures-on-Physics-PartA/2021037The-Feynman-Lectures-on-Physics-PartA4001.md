The Principles of Statistical Mechanics

40-1 The exponential atmosphereWe have discussed some of the properties of large numbers of intercollidingatoms. The subject is called kinetic theory, a description of matter from the pointof view of collisions between the atoms. Fundamentally, we assert that the grossproperties of matter should be explainable in terms of the motion of its parts.We limit ourselves for the present to conditions of thermal equilibrium, that is,to a subclass of all the phenomena of nature. The laws of mechanics which applyjust to thermal equilibrium are called statistical mechanics, and in this sectionwe want to become acquainted with some of the central theorems of this subject.We already have one of the theorems of statistical mechanics, namely, themean value of the kinetic energy for any motion at the absolute temperature Tis 12 kT for each independent motion, i.e., for each degree of freedom. That tellsus something about the mean square velocities of the atoms. Our objective nowis to learn more about the positions of the atoms, to discover how many of themare going to be in diﬀerent places at thermal equilibrium, and also to go intoa little more detail on the distribution of the velocities. Although we have themean square velocity, we do not know how to answer a question such as howmany of them are going three times faster than the root mean square, or howmany of them are going one-quarter of the root mean square speed. Or have theyall the same speed exactly?

So, these are the two questions that we shall try to answer: How are themolecules distributed in space when there are forces acting on them, and howare they distributed in velocity?

It turns out that the two questions are completely independent, and thatthe distribution of velocities is always the same. We already received a hintof the latter fact when we found that the average kinetic energy is the same,2 kT per degree of freedom, no matter what forces are acting on the molecules.1

40-1

The distribution of the velocities of the molecules is independent of the forces,because the collision rates do not depend upon the forces.

Let us begin with an example: the distribution of the molecules in an at-mosphere like our own, but without the winds and other kinds of disturbance.Suppose that we have a column of gas extending to a great height, and at thermalequilibrium—unlike our atmosphere, which as we know gets colder as we go up.We could remark that if the temperature diﬀered at diﬀerent heights, we coulddemonstrate lack of equilibrium by connecting a rod to some balls at the bottom(Fig. 40-1), where they would pick up 12 kT from the molecules there and wouldshake, via the rod, the balls at the top and those would shake the moleculesat the top. So, ultimately, of course, the temperature becomes the same at allheights in a gravitational ﬁeld.

Fig. 40-1. The pressure at height h must exceed that at h + dh by

the weight of the intervening gas.

If the temperature is the same at all heights, the problem is to discover bywhat law the atmosphere becomes tenuous as we go up. If N is the total numberof molecules in a volume V of gas at pressure P, then we know P V = N kT,or P = nkT, where n = N/V is the number of molecules per unit volume. Inother words, if we know the number of molecules per unit volume, we knowthe pressure, and vice versa: they are proportional to each other, since the

40-2

temperature is constant in this problem. But the pressure is not constant, itmust increase as the altitude is reduced, because it has to hold, so to speak, theweight of all the gas above it. That is the clue by which we may determine howthe pressure changes with height. If we take a unit area at height h, then thevertical force from below, on this unit area, is the pressure P. The vertical forceper unit area pushing down at a height h + dh would be the same, in the absenceof gravity, but here it is not, because the force from below must exceed the forcefrom above by the weight of gas in the section between h and h + dh. Now mg isthe force of gravity on each molecule, where g is the acceleration due to gravity,and n dh is the total number of molecules in the unit section. So this gives usthe diﬀerential equation Ph+dh − Ph = dP = −mgn dh. Since P = nkT, and Tis constant, we can eliminate either P or n, say P, and get

dndh

= − mgkT

n

for the diﬀerential equation, which tells us how the density goes down as we goup in energy.

We thus have an equation for the particle density n, which varies with height,but which has a derivative which is proportional to itself. Now a function whichhas a derivative proportional to itself is an exponential, and the solution of thisdiﬀerential equation is

n = n0e−mgh/kT .

(40.1)Here the constant of integration, n0, is obviously the density at h = 0 (whichcan be chosen anywhere), and the density goes down exponentially with height.Note that if we have diﬀerent kinds of molecules with diﬀerent masses, theygo down with diﬀerent exponentials. The ones which were heavier would decreasewith altitude faster than the light ones. Therefore we would expect that becauseoxygen is heavier than nitrogen, as we go higher and higher in an atmospherewith nitrogen and oxygen the proportion of nitrogen would increase. This doesnot really happen in our own atmosphere, at least at reasonable heights, becausethere is so much agitation which mixes the gases back together again. It is notan isothermal atmosphere. Nevertheless, there is a tendency for lighter materials,like hydrogen, to dominate at very great heights in the atmosphere, because thelowest masses continue to exist, while the other exponentials have all died out(Fig. 40-2).

40-3

Fig. 40-2. The normalized density as a function of height in the earth’sgravitational ﬁeld for oxygen and for hydrogen, at constant temperature.

40-2 The Boltzmann lawHere we note the interesting fact that the numerator in the exponent ofEq. (40.1) is the potential energy of an atom. Therefore we can also state thisparticular law as: the density at any point is proportional to

e−the potential energy of each atom/kT .

That may be an accident, i.e., may be true only for this particular case ofa uniform gravitational ﬁeld. However, we can show that it is a more generalproposition. Suppose that there were some kind of force other than gravity actingon the molecules in a gas. For example, the molecules may be charged electrically,and may be acted on by an electric ﬁeld or another charge that attracts them.Or, because of the mutual attractions of the atoms for each other, or for the wall,or for a solid, or something, there is some force of attraction which varies withposition and which acts on all the molecules. Now suppose, for simplicity, thatthe molecules are all the same, and that the force acts on each individual one, sothat the total force on a piece of gas would be simply the number of molecules

40-4

times the force on each one. To avoid unnecessary complication, let us choose acoordinate system with the x-axis in the direction of the force, F .In the same manner as before, if we take two parallel planes in the gas,separated by a distance dx, then the force on each atom, times the n atoms percm3 (the generalization of the previous nmg), times dx, must be balanced by thepressure change: F n dx = dP = kT dn. Or, to put this law in a form which willbe useful to us later,

(ln n).

ddx

F = kT

n = (constant)e−P.E./kT .

(40.2)For the present, observe that −F dx is the work we would do in taking a moleculefrom x to x + dx, and if F comes from a potential, i.e., if the work done can berepresented by a potential energy at all, then this would also be the diﬀerence inthe potential energy (P.E.). The negative diﬀerential of potential energy is thework done, F dx, and we ﬁnd that d(ln n) = −d(P.E.)/kT, or, after integrating,(40.3)Therefore what we noticed in a special case turns out to be true in general.(What if F does not come from a potential? Then (40.2) has no solution at all.Energy can be generated, or lost by the atoms running around in cyclic pathsfor which the work done is not zero, and no equilibrium can be maintained atall. Thermal equilibrium cannot exist if the external forces on the atoms arenot conservative.) Equation (40.3), known as Boltzmann’s law, is another of theprinciples of statistical mechanics: that the probability of ﬁnding molecules in agiven spatial arrangement varies exponentially with the negative of the potentialenergy of that arrangement, divided by kT.This, then, could tell us the distribution of molecules: Suppose that we had apositive ion in a liquid, attracting negative ions around it, how many of themwould be at diﬀerent distances? If the potential energy is known as a function ofdistance, then the proportion of them at diﬀerent distances is given by this law,and so on, through many applications.

40-3 Evaporation of a liquidIn more advanced statistical mechanics one tries to solve the following impor-tant problem. Consider an assembly of molecules which attract each other, andsuppose that the force between any two, say i and j, depends only on their sepa-ration rij, and can be represented as the derivative of a potential function V (rij).

40-5

Fig. 40-3. A potential-energy function for two molecules, which

depends only on their separation.

Figure 40-3 shows a form such a function might have. For r > r0, the energydecreases as the molecules come together, because they attract, and then theenergy increases very sharply as they come still closer together, because they repelstrongly, which is characteristic of the way molecules behave, roughly speaking.Now suppose we have a whole box full of such molecules, and we would liketo know how they arrange themselves on the average. The answer is e−P.E./kT .The total potential energy in this case would be the sum over all the pairs,supposing that the forces are all in pairs (there may be three-body forces in morecomplicated things, but in electricity, for example, the potential energy is all inpairs). Then the probability for ﬁnding molecules in any particular combinationof rij’s will be proportional to

exph−X

i

V (rij)/kT

.

i,j

Now, if the temperature is very high, so that kT (cid:29) |V (r0)|, the exponent isrelatively small almost everywhere, and the probability of ﬁnding a molecule isalmost independent of position. Let us take the case of just two molecules: thee−P.E./kT would be the probability of ﬁnding them at various mutual distances r.Clearly, where the potential goes most negative, the probability is largest, andwhere the potential goes toward inﬁnity, the probability is almost zero, whichoccurs for very small distances. That means that for such atoms in a gas, thereis no chance that they are on top of each other, since they repel so strongly.But there is a greater chance of ﬁnding them per unit volume at the point r0than at any other point. How much greater, depends on the temperature. Ifthe temperature is very large compared with the diﬀerence in energy between

40-6

r = r0 and r = ∞, the exponential is always nearly unity. In this case, where themean kinetic energy (about kT) greatly exceeds the potential energy, the forcesdo not make much diﬀerence. But as the temperature falls, the probability ofﬁnding the molecules at the preferred distance r0 gradually increases relative tothe probability of ﬁnding them elsewhere and, in fact, if kT is much less than|V (r0)|, we have a relatively large positive exponent in that neighborhood. Inother words, in a given volume they are much more likely to be at the distanceof minimum energy than far apart. As the temperature falls, the atoms falltogether, clump in lumps, and reduce to liquids, and solids, and molecules, andas you heat them up they evaporate.

The requirements for the determination of exactly how things evaporate,exactly how things should happen in a given circumstance, involve the following.First, to discover the correct molecular-force law V (r), which must come fromsomething else, quantum mechanics, say, or experiment. But, given the law offorce between the molecules, to discover what a billion molecules are going to do

merely consists of studying the function e−P Vij /kT . Surprisingly enough, since

it is such a simple function and such an easy idea, given the potential, the laboris enormously complicated; the diﬃculty is the tremendous number of variables.In spite of such diﬃculties, the subject is quite exciting and interesting. It isoften called an example of a「many-body problem,」and it really has been a veryinteresting thing. In that single formula must be contained all the details, forexample, about the solidiﬁcation of gas, or the forms of the crystals that the solidcan take, and people have been trying to squeeze it out, but the mathematicaldiﬃculties are very great, not in writing the law, but in dealing with so enormousa number of variables.

That then, is the distribution of particles in space. That is the end of classicalstatistical mechanics, practically speaking, because if we know the forces, wecan, in principle, ﬁnd the distribution in space, and the distribution of velocitiesis something that we can work out once and for all, and is not something thatis diﬀerent for the diﬀerent cases. The great problems are in getting particularinformation out of our formal solution, and that is the main subject of classicalstatistical mechanics.

40-4 The distribution of molecular speedsNow we go on to discuss the distribution of velocities, because sometimesit is interesting or useful to know how many of them are moving at diﬀerent

40-7

speeds. In order to do that, we may make use of the facts which we discoveredwith regard to the gas in the atmosphere. We take it to be a perfect gas, as wehave already assumed in writing the potential energy, disregarding the energy ofmutual attraction of the atoms. The only potential energy that we included in ourﬁrst example was gravity. We would, of course, have something more complicatedif there were forces between the atoms. Thus we assume that there are no forcesbetween the atoms and, for a moment, disregard collisions also, returning laterto the justiﬁcation of this. Now we saw that there are fewer molecules at theheight h than there are at the height 0; according to formula (40.1), they decreaseexponentially with height. How can there be fewer at greater heights? Afterall, do not all the molecules which are moving up at height 0 arrive at h? No!,because some of those which are moving up at 0 are going too slowly, and cannotclimb the potential hill to h. With that clue, we can calculate how many mustbe moving at various speeds, because from (40.1) we know how many are movingwith less than enough speed to climb a given distance h. Those are just the onesthat account for the fact that the density at h is lower than at 0.

Now let us put that idea a little more precisely:

let us count how manymolecules are passing from below to above the plane h = 0 (by calling itheight = 0, we do not mean that there is a ﬂoor there; it is just a convenient label,and there is gas at negative h). These gas molecules are moving around in everydirection, but some of them are moving through the plane, and at any moment acertain number per second of them are passing through the plane from below to

Fig. 40-4. Only those molecules moving up at h = 0 with suﬃcient

velocity can arrive at height h.

40-8

above with diﬀerent velocities. Now we note the following: if we call u the velocitywhich is just needed to get up to the height h (kinetic energy mu2/2 = mgh),then the number of molecules per second which are passing upward throughthe lower plane in a vertical direction with velocity component greater than uis exactly the same as the number which pass through the upper plane withany upward velocity. Those molecules whose vertical velocity does not exceed ucannot get through the upper plane. So therefore we see that

Number passing h = 0 with vz > u = number passing h = h with vz > 0.

But the number which pass through h with any velocity greater than 0 is less thanthe number which pass through the lower height with any velocity greater than 0,because the number of atoms is greater; that is all we need. We know alreadythat the distribution of velocities is the same, after the argument we made earlierabout the temperature being constant all the way through the atmosphere. So,since the velocity distributions are the same, and it is just that there are moreatoms lower down, clearly the number n>0(h), passing with positive velocity atheight h, and the number n>0(0), passing with positive velocity at height 0, arein the same ratio as the densities at the two heights, which is e−mgh/kT . Butn>0(h) = n>u(0), and therefore we ﬁnd that

n>u(0)n>0(0) = e−mgh/kT = e−mu2/2kT ,

since 12 mu2 = mgh. Thus, in words, the number of molecules per unit areaper second passing the height 0 with a z-component of velocity greater than uis e−mu2/2kT times the total number that are passing through the plane withvelocity greater than zero.

Now this is not only true at the arbitrarily chosen height 0, but of course itis true at any other height, and thus the distributions of velocities are all thesame! (The ﬁnal statement does not involve the height h, which appeared onlyin the intermediate argument.) The result is a general proposition that gives usthe distribution of velocities. It tells us that if we drill a little hole in the sideof a gas pipe, a very tiny hole, so that the collisions are few and far between,i.e., are farther apart than the diameter of the hole, then the particles which arecoming out will have diﬀerent velocities, but the fraction of particles which comeout at a velocity greater than u is e−mu2/2kT .

40-9

Now we return to the question about the neglect of collisions: Why does itnot make any diﬀerence? We could have pursued the same argument, not with aﬁnite height h, but with an inﬁnitesimal height h, which is so small that therewould be no room for collisions between 0 and h. But that was not necessary:the argument is evidently based on an analysis of the energies involved, theconservation of energy, and in the collisions that occur there is an exchange ofenergies among the molecules. However, we do not really care whether we followthe same molecule if energy is merely exchanged with another molecule. So itturns out that even if the problem is analyzed more carefully (and it is morediﬃcult, naturally, to do a rigorous job), it still makes no diﬀerence in the result.

It is interesting that the velocity distribution we have found is just

n>u ∝ e−kinetic energy/kT .

(40.4)

This way of describing the distribution of velocities, by giving the numberof molecules that pass a given area with a certain minimum z-component, isnot the most convenient way of giving the velocity distribution. For instance,inside the gas, one more often wants to know how many molecules are movingwith a z-component of velocity between two given values, and that, of course, isnot directly given by Eq. (40.4). We would like to state our result in the moreconventional form, even though what we already have written is quite general.Note that it is not possible to say that any molecule has exactly some statedvelocity; none of them has a velocity exactly equal to 1.7962899173 meters persecond. So in order to make a meaningful statement, we have to ask how many areto be found in some range of velocities. We have to say how many have velocitiesbetween 1.796 and 1.797, and so on. On mathematical terms, let f(u) du bethe fraction of all the molecules which have velocities between u and u + du or,what is the same thing (if du is inﬁnitesimal), all that have a velocity u witha range du. Figure 40-5 shows a possible form for the function f(u), and theshaded part, of width du and mean height f(u), represents this fraction f(u) du.That is, the ratio of the shaded area to the total area of the curve is the relativeproportion of molecules with velocity u within du. If we deﬁne f(u) so that thefraction having a velocity in this range is given directly by the shaded area, thenthe total area must be 100 percent of them, that is,

Z ∞

−∞

f(u) du = 1.

40-10

(40.5)

Fig. 40-5. A velocity distribution function. The shaded area is f (u) du,

the fraction of particles having velocities within a range du about u.

ﬁrst we might think it is merely the integral ofR ∞

Now we have only to get this distribution by comparing it with the theoremwe derived before. First we ask, what is the number of molecules passing throughan area per second with a velocity greater than u, expressed in terms of f(u)? Atu f(u) du, but it is not, becausewe want the number that are passing the area per second. The faster ones passmore often, so to speak, than the slower ones, and in order to express how manypass, you have to multiply by the velocity. (We discussed that in the previouschapter when we talked about the number of collisions.) In a given time t thetotal number which pass through the surface is all of those which have been ableto arrive at the surface, and the number which arrive come from a distance ut.So the number of molecules which arrive is not simply the number which arethere, but the number that are there per unit volume, multiplied by the distancethat they sweep through in racing for the area through which they are supposedto go, and that distance is proportional to u. Thus we need the integral of utimes f(u) du, an inﬁnite integral with a lower limit u, and this must be the sameas we found before, namely e−mu2/2kT , with a proportionality constant whichwe will get later:

Z ∞

uf(u) du = const · e−mu2/2kT .

(40.6)

u

Now if we diﬀerentiate the integral with respect to u, we get the thing thatis inside the integral, i.e., the integrand (with a minus sign, since u is the lowerlimit), and if we diﬀerentiate the other side, we get u times the same exponential

40-11

Z ∞

dx = √

e−x2

(and some constants). The u’s cancel and we ﬁnd

f(u) du = Ce−mu2/2kT du.

(40.7)We retain the du on both sides as a reminder that it is a distribution, and it tellswhat the proportion is for velocity between u and u + du.The constant C must be so determined that the integral is unity, accordingto Eq. (40.5). Now we can prove* that

Using this fact, it is easy to ﬁnd that C =pm/2πkT.

−∞

π.

Since velocity and momentum are proportional, we may say that the distribu-tion of momenta is also proportional to e−K.E./kT per unit momentum range. Itturns out that this theorem is true in relativity too, if it is in terms of momentum,while if it is in velocity it is not, so it is best to learn it in momentum instead ofin velocity:

f(p) dp = Ce−K.E./kT dp.

(40.8)So we ﬁnd that the probabilities of diﬀerent conditions of energy, kinetic andpotential, are both given by e−energy/kT , a very easy thing to remember and arather beautiful proposition.So far we have, of course, only the distribution of the velocities「vertically.」We might want to ask, what is the probability that a molecule is moving inanother direction? Of course these distributions are connected, and one canobtain the complete distribution from the one we have, because the completedistribution depends only on the square of the magnitude of the velocity, notupon the z-component. It must be something that is independent of direction,

Then

* To get the value of the integral, let

I =R ∞

I2 =R ∞

−∞ e−x2

dx.

−∞ e−x2

dy =R ∞dx ·R ∞0 e−r2 · 2πr dr = πR ∞I2 =R ∞

−∞ e−y2

−∞

R ∞

−∞ e−(x2+y2) dy dx,

0 e−t dt = π.

which is a double integral over the whole xy-plane. But this can also be written in polarcoordinates as

40-12

and there is only one function involved, the probability of diﬀerent magnitudes.We have the distribution of the z-component, and therefore we can get thedistribution of the other components from it. The result is that the probabilityis still proportional to e−K.E/kT , but now the kinetic energy involves three parts,z /2, summed in the exponent. Or we can write it as amv2product:

y/2, and mv2

x/2, mv2

∝ e−mv2

y/2kT · e−mv2

f(vx, vy, vz) dvx dvy dvz

x/2kT · e−mv2

(40.9)You can see that this formula must be right because, ﬁrst, it is a function onlyof v2, as required, and second, the probabilities of various values of vz obtainedby integrating over all vx and vy is just (40.7). But this one function (40.9) cando both those things!

z /2kT dvx dvy dvz.

40-5 The speciﬁc heats of gasesNow we shall look at some ways to test the theory, and to see how successfulis the classical theory of gases. We saw earlier that if U is the internal energyof N molecules, then P V = N kT = (γ − 1)U holds, sometimes, for some gases,maybe. If it is a monatomic gas, we know this is also equal to 23 of the kineticenergy of the center-of-mass motion of the atoms. If it is a monatomic gas, thenthe kinetic energy is equal to the internal energy, and therefore γ − 1 = 23. Butsuppose it is, say, a more complicated molecule, that can spin and vibrate, andlet us suppose (it turns out to be true according to classical mechanics) thatthe energies of the internal motions are also proportional to kT. Then at agiven temperature, in addition to kinetic energy 32 kT, it has internal vibrationaland rotational energies. So the total U includes not just the kinetic energy, butalso the rotational and vibrational energies, and we get a diﬀerent value of γ.Technically, the best way to measure γ is by measuring the speciﬁc heat, whichis the change in energy with temperature. We will return to that approach later.For our present purposes, we may suppose γ is found experimentally from theP V γ curve for adiabatic compression.Let us make a calculation of γ for some cases. First, for a monatomic gas Uis the total energy, the same as the kinetic energy, and we know already that γshould be 53. For a diatomic gas, we may take, as an example, oxygen, hydrogeniodide, hydrogen, etc., and suppose that the diatomic gas can be represented

40-13

as two atoms held together by some kind of force like the one of Fig. 40-3. Wemay also suppose, and it turns out to be quite true, that at the temperaturesthat are of interest for the diatomic gas, the pairs of atoms tend strongly to beseparated by r0, the distance of potential minimum. If this were not true, if theprobability were not strongly varying enough to make the great majority sit nearthe bottom, we would have to remember that oxygen gas is a mixture of O2 andsingle oxygen atoms in a nontrivial ratio. We know that there are, in fact, veryfew single oxygen atoms, which means that the potential energy minimum is verymuch greater in magnitude than kT, as we have seen. Since they are clusteredstrongly around r0, the only part of the curve that is needed is the part nearthe minimum, which may be approximated by a parabola. A parabolic potentialimplies a harmonic oscillator, and in fact, to an excellent approximation, theoxygen molecule can be represented as two atoms connected by a spring.

2 plus 3

2 kT + 32), kinetic energy of rotation ( 2

Now what is the total energy of this molecule at temperature T? We know2 kT, sothat for each of the two atoms, each of the kinetic energies should be 32 kT. We can also put this in athe kinetic energy of both of them is 32 can also be looked at as kinetic energy of thediﬀerent way: the same 32), and kinetic energy of vibrationcenter of mass ( 32). We know that the kinetic energy of vibration is 12, since there is just one( 12 kT. Regarding the rotation,dimension involved and each degree of freedom has 1it can turn about either of two axes, so there are two independent motions. Weassume that the atoms are some kind of points, and cannot spin about the linejoining them; this is something to bear in mind, because if we get a disagreement,maybe that is where the trouble is. But we have one more thing, which is thepotential energy of vibration; how much is that? In a harmonic oscillator theaverage kinetic energy and average potential energy are equal, and therefore thepotential energy of vibration is 12 kT,3, i.e., γ = 1.286.or kT is 2We may compare these numbers with the relevant measured values shownin Table 40-1. Looking ﬁrst at helium, which is a monatomic gas, we ﬁnd3, and the error is probably experimental, although at such a lowvery nearly 5temperature there may be some forces between the atoms. Krypton and argon,both monatomic, agree also within the accuracy of the experiment.

2 kT, also. The grand total of energy is U = 7

7 U per atom. That means, then, that γ is 9

7 instead of 5

We turn to the diatomic gases and ﬁnd hydrogen with 1.404, which does notagree with the theory, 1.286. Oxygen, 1.399, is very similar, but again not inagreement. Hydrogen iodide again is similar at 1.40. It begins to look as thoughthe right answer is 1.40, but it is not, because if we look further at bromine

40-14

Table 40-1

Values of the speciﬁc heat ratio, γ, for various gases

Gas

HeKrArH2O2HIBr2I2NH3C2H6

T (◦C)−18019151001001003001851515

γ

1.6601.681.6681.4041.3991.401.321.301.3101.22

we see 1.32, and at iodine we see 1.30. Since 1.30 is reasonably close to 1.286,iodine may be said to agree rather well, but oxygen is far oﬀ. So here we have adilemma. We have it right for one molecule, we do not have it right for anothermolecule, and we may need to be pretty ingenious in order to explain both.

Let us look further at a still more complicated molecule with large numbersof parts, for example, C2H6, which is ethane. It has eight diﬀerent atoms, andthey are all vibrating and rotating in various combinations, so the total amountof internal energy must be an enormous number of kT’s, at least 12kT for kineticenergy alone, and γ − 1 must be very close to zero, or γ almost exactly 1. In fact,it is lower, but 1.22 is not so much lower, and is higher than the 1 112 calculatedfrom the kinetic energy alone, and it is just not understandable!Furthermore, the whole mystery is deep, because the diatomic moleculecannot be made rigid by a limit. Even if we made the couplings stiﬀer indeﬁnitely,although it might not vibrate much, it would nevertheless keep vibrating. Thevibrational energy inside is still kT, since it does not depend on the strength ofthe coupling. But if we could imagine absolute rigidity, stopping all vibration toeliminate a variable, then we would get U = 52 kT and γ = 1.40 for the diatomiccase. This looks good for H2 or O2. On the other hand, we would still haveproblems, because γ for either hydrogen or oxygen varies with temperature! Fromthe measured values shown in Fig. 40-6, we see that for H2, γ varies from about1.6 at −185◦C to 1.3 at 2000◦C. The variation is more substantial in the case of

40-15

Fig. 40-6. Experimental values of γ as a function of temperature forhydrogen and oxygen. Classical theory predicts γ = 1.286, independentof temperature.

hydrogen than for oxygen, but nevertheless, even in oxygen, γ tends deﬁnitely togo up as we go down in temperature.

40-6 The failure of classical physicsSo, all in all, we might say that we have some diﬃculty. We might try someforce law other than a spring, but it turns out that anything else will only makeγ higher. If we include more forms of energy, γ approaches unity more closely,contradicting the facts. All the classical theoretical things that one can think ofwill only make it worse. The fact is that there are electrons in each atom, andwe know from their spectra that there are internal motions; each of the electronsshould have at least 12 kT of kinetic energy, and something for the potential energy,so when these are added in, γ gets still smaller. It is ridiculous. It is wrong.The ﬁrst great paper on the dynamical theory of gases was by Maxwell in1859. On the basis of ideas we have been discussing, he was able accurately toexplain a great many known relations, such as Boyle’s law, the diﬀusion theory,the viscosity of gases, and things we shall talk about in the next chapter. He listedall these great successes in a ﬁnal summary, and at the end he said,「Finally, byestablishing a necessary relation between the motions of translation and rotation(he is talking about the 12 kT theorem) of all particles not spherical, we provedthat a system of such particles could not possibly satisfy the known relation

40-16

between the two speciﬁc heats.」He is referring to γ (which we shall see later isrelated to two ways of measuring speciﬁc heat), and he says we know we cannotget the right answer.

Ten years later, in a lecture, he said,「I have now put before you what Iconsider to be the greatest diﬃculty yet encountered by the molecular theory.」These words represent the ﬁrst discovery that the laws of classical physics werewrong. This was the ﬁrst indication that there was something fundamentallyimpossible, because a rigorously proved theorem did not agree with experiment.About 1890, Jeans was to talk about this puzzle again. One often hears it saidthat physicists at the latter part of the nineteenth century thought they knew allthe signiﬁcant physical laws and that all they had to do was to calculate moredecimal places. Someone may have said that once, and others copied it. But athorough reading of the literature of the time shows they were all worrying aboutsomething. Jeans said about this puzzle that it is a very mysterious phenomenon,and it seems as though as the temperature falls, certain kinds of motions「freezeout.」

If we could assume that the vibrational motion, say, did not exist at lowtemperature and did exist at high temperature, then we could imagine that a gasmight exist at a temperature suﬃciently low that vibrational motion does notoccur, so γ = 1.40, or a higher temperature at which it begins to come in, so γfalls. The same might be argued for the rotation. If we can eliminate the rotation,say it「freezes out」at suﬃciently low temperature, then we can understand thefact that the γ of hydrogen approaches 1.66 as we go down in temperature. Howcan we understand such a phenomenon? Of course that these motions「freezeout」cannot be understood by classical mechanics. It was only understood whenquantum mechanics was discovered.

Without proof, we may state the results for statistical mechanics of thequantum-mechanical theory. We recall that according to quantum mechanics, asystem which is bound by a potential, for the vibrations, for example, will havea discrete set of energy levels, i.e., states of diﬀerent energy. Now the questionis: how is statistical mechanics to be modiﬁed according to quantum-mechanicaltheory? It turns out, interestingly enough, that although most problems aremore diﬃcult in quantum mechanics than in classical mechanics, problems instatistical mechanics are much easier in quantum theory! The simple result wehave in classical mechanics, that n = n0e−energy/kT , becomes the following veryimportant theorem: If the energies of the set of molecular states are called, say,E0, E1, E2, . . . , Ei, . . . , then in thermal equilibrium the probability of ﬁnding a

40-17

molecule in the particular state of having energy Ei is proportional to e−Ei/kT .That gives the probability of being in various states. In other words, the relativechance, the probability, of being in state E1 relative to the chance of being instate E0, is

,

(40.10)

which, of course, is the same as

P1P0

= e−E1/kTe−E0/kT

n1 = n0e−(E1−E0)/kT ,

(40.11)since P1 = n1/N and P0 = n0/N. So it is less likely to be in a higher energy statethan in a lower one. The ratio of the number of atoms in the upper state to thenumber in the lower state is e raised to the power (minus the energy diﬀerence,over kT)—a very simple proposition.Now it turns out that for a harmonic oscillator the energy levels are evenlyspaced. Calling the lowest energy E0 = 0 (it actually is not zero, it is a littlediﬀerent, but it does not matter if we shift all energies by a constant), the ﬁrstone is then E1 = ω, and the second one is 2ω, and the third one is 3ω, andso on.Now let us see what happens. We suppose we are studying the vibrationsof a diatomic molecule, which we approximate as a harmonic oscillator. Letus ask what is the relative chance of ﬁnding a molecule in state E1 instead ofin state E0. The answer is that the chance of ﬁnding it in state E1, relativeto that of ﬁnding it in state E0, goes down as e−ω/kT . Now suppose that kTis much less than ω, and we have a low-temperature circumstance. Then theprobability of its being in state E1 is extremely small. Practically all the atomsare in state E0. If we change the temperature but still keep it very small, thenthe chance of its being in state E1 = ω remains inﬁnitesimal—the energy of theoscillator remains nearly zero; it does not change with temperature so long as thetemperature is much less than ω. All oscillators are in the bottom state, andtheir motion is eﬀectively「frozen」; there is no contribution of it to the speciﬁcheat. We can judge, then, from Table 40-1, that at 100◦C, which is 373 degreesabsolute, kT is much less than the vibrational energy in the oxygen or hydrogenmolecules, but not so in the iodine molecule. The reason for the diﬀerence isthat an iodine atom is very heavy, compared with hydrogen, and although theforces may be comparable in iodine and hydrogen, the iodine molecule is soheavy that the natural frequency of vibration is very low compared with the

40-18

natural frequency of hydrogen. With ω higher than kT at room temperaturefor hydrogen, but lower for iodine, only the latter, iodine, exhibits the classicalvibrational energy. As we increase the temperature of a gas, starting from a verylow value of T, with the molecules almost all in their lowest state, they graduallybegin to have an appreciable probability to be in the second state, and then inthe next state, and so on. When the probability is appreciable for many states,the behavior of the gas approaches that given by classical physics, because thequantized states become nearly indistinguishable from a continuum of energies,and the system can have almost any energy. Thus, as the temperature rises,we should again get the results of classical physics, as indeed seems to be thecase in Fig. 40-6. It is possible to show in the same way that the rotationalstates of atoms are also quantized, but the states are so much closer togetherthat in ordinary circumstances kT is bigger than the spacing. Then many levelsare excited, and the rotational kinetic energy in the system participates in theclassical way. The one example where this is not quite true at room temperatureis for hydrogen.

This is the ﬁrst time that we have really deduced, by comparison withexperiment, that there was something wrong with classical physics, and we havelooked for a resolution of the diﬃculty in quantum mechanics in much the sameway as it was done originally. It took 30 or 40 years before the next diﬃculty wasdiscovered, and that had to do again with statistical mechanics, but this timethe mechanics of a photon gas. That problem was solved by Planck, in the earlyyears of the 20th century.

40-19

41

