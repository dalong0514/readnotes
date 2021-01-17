Radiation Damping. Light Scattering

32-1 Radiation resistanceIn the last chapter we learned that when a system is oscillating, energy iscarried away, and we deduced a formula for the energy which is radiated by anoscillating system. If we know the electric ﬁeld, then the average of the squareof the ﬁeld times 0c is the amount of energy that passes per square meter persecond through a surface normal to the direction in which the radiation is going:

S = 0chE2i.

(32.1)

Any oscillating charge radiates energy; for instance, a driven antenna radiatesenergy. If the system radiates energy, then in order to account for the conservationof energy we must ﬁnd that power is being delivered along the wires which leadinto the antenna. That is, to the driving circuit the antenna acts like a resistance,or a place where energy can be「lost」(the energy is not really lost, it is reallyradiated out, but so far as the circuit is concerned, the energy is lost). In anordinary resistance, the energy which is「lost」passes into heat; in this case theenergy which is「lost」goes out into space. But from the standpoint of circuittheory, without considering where the energy goes, the net eﬀect on the circuit isthe same—energy is「lost」from that circuit. Therefore the antenna appears tothe generator as having a resistance, even though it may be made with perfectlygood copper. In fact, if it is well built it will appear as almost a pure resistance,with very little inductance or capacitance, because we would like to radiate asmuch energy as possible out of the antenna. This resistance that an antennashows is called the radiation resistance.If a current I is going to the antenna, then the average rate at which poweris delivered to the antenna is the average of the square of the current times theresistance. The rate at which power is radiated by the antenna is proportional

32-1

to the square of the current in the antenna, of course, because all the ﬁelds areproportional to the currents, and the energy liberated is proportional to thesquare of the ﬁeld. The coeﬃcient of proportionality between radiated powerand hI2i is the radiation resistance.An interesting question is, what is this radiation resistance due to? Let ustake a simple example: let us say that currents are driven up and down in anantenna. We ﬁnd that we have to put work in, if the antenna is to radiate energy.If we take a charged body and accelerate it up and down it radiates energy; ifit were not charged it would not radiate energy. It is one thing to calculatefrom the conservation of energy that energy is lost, but another thing to answerthe question, against what force are we doing the work? That is an interestingand very diﬃcult question which has never been completely and satisfactorilyanswered for electrons, although it has been for antennas. What happens is this:in an antenna, the ﬁelds produced by the moving charges in one part of theantenna react on the moving charges in another part of the antenna. We cancalculate these forces and ﬁnd out how much work they do, and so ﬁnd the rightrule for the radiation resistance. When we say「We can calculate—」that is notquite right—we cannot, because we have not yet studied the laws of electricity atshort distances; only at large distances do we know what the electric ﬁeld is. Wesaw the formula (28.3), but at present it is too complicated for us to calculatethe ﬁelds inside the wave zone. Of course, since conservation of energy is valid,we can calculate the result all right without knowing the ﬁelds at short distances.(As a matter of fact, by using this argument backwards it turns out that one canﬁnd the formula for the forces at short distances only by knowing the ﬁeld atvery large distances, by using the laws of conservation of energy, but we shall notgo into that here.)

The problem in the case of a single electron is this: if there is only one charge,what can the force act on? It has been proposed, in the old classical theory, thatthe charge was a little ball, and that one part of the charge acted on the otherpart. Because of the delay in the action across the tiny electron, the force is notexactly in phase with the motion. That is, if we have the electron standing still,we know that「action equals reaction.」So the various internal forces are equal,and there is no net force. But if the electron is accelerating, then because of thetime delay across it, the force which is acting on the front from the back is notexactly the same as the force on the back from the front, because of the delay inthe eﬀect. This delay in the timing makes for a lack of balance, so, as a net eﬀect,the thing holds itself back by its bootstraps! This model of the origin of the

32-2

resistance to acceleration, the radiation resistance of a moving charge, has runinto many diﬃculties, because our present view of the electron is that it is not a「little ball」; this problem has never been solved. Nevertheless we can calculateexactly, of course, what the net radiation resistance force must be, i.e., how muchloss there must be when we accelerate a charge, in spite of not knowing directlythe mechanism of how that force works.

32-2 The rate of radiation of energyNow we shall calculate the total energy radiated by an accelerating charge.To keep the discussion general, we shall take the case of a charge accelerating anywhich way, but nonrelativistically. At a moment when the acceleration is, say,vertical, we know that the electric ﬁeld that is generated is the charge multipliedby the projection of the retarded acceleration, divided by the distance. So weknow the electric ﬁeld at any point, and we therefore know the square of theelectric ﬁeld and thus the energy 0cE2 leaving through a unit area per second.The quantity 0c appears quite often in expressions involving radiowavepropagation. Its reciprocal is called the impedance of a vacuum, and it is an easynumber to remember: it has the value 1/0c = 377 ohms. So the power in wattsper square meter is equal to the average of the ﬁeld squared, divided by 377.

Using our expression (29.1) for the electric ﬁeld, we ﬁnd that

S = q2a02 sin2 θ16π20r2c3

(32.2)

is the power per square meter radiated in the direction θ. We notice that it goesinversely as the square of the distance, as we said before. Now suppose we wantedthe total energy radiated in all directions: then we must integrate (32.2) over alldirections. First we multiply by the area, to ﬁnd the amount that ﬂows within alittle angle dθ (Fig. 32-1). We need the area of a spherical section. The way tothink of it is this: if r is the radius, then the width of the annular segment is r dθ,and the circumference is 2πr sin θ, because r sin θ is the radius of the circle. Sothe area of the little piece of the sphere is 2πr sin θ times r dθ:

dA = 2πr2 sin θ dθ.

(32.3)

By multiplying the ﬂux [(32.2), the power per square meter] by the area in squaremeters included in the small angle dθ, we ﬁnd the amount of energy that is

32-3

Fig. 32-1. The area of a spherical segment is 2πr sin θ · r dθ.

liberated in this direction between θ and θ + dθ; then we integrate that over allthe angles θ from 0 to 180◦:

Z

Z π

By writing sin3 θ = (1−cos2 θ) sin θ it is not hard to show thatR π

0

sin3 θ dθ.

P =

S dA = q2a028π0c3

Using that fact, we ﬁnally get

(32.4)

0 sin3 θ dθ = 4/3.

P = q2a026π0c3 .

(32.5)

This expression deserves some remarks. First of all, since the vector a0 had acertain direction, the a02 in (32.5) would be the square of the vector a0, that is,a0 · a0, the length of the vector, squared. Secondly, the ﬂux (32.2) was calculatedusing the retarded acceleration; that is, the acceleration at the time at which theenergy now passing through the sphere was radiated. We might like to say thatthis energy was in fact liberated at this earlier time. This is not exactly true; itis only an approximate idea. The exact time when the energy is liberated cannotbe deﬁned precisely. All we can really calculate precisely is what happens in acomplete motion, like an oscillation or something, where the acceleration ﬁnallyceases. Then what we ﬁnd is that the total energy ﬂux per cycle is the averageof acceleration squared, for a complete cycle. This is what should really appearin (32.5). Or, if it is a motion with an acceleration that is initially and ﬁnallyzero, then the total energy that has ﬂown out is the time integral of (32.5).

To illustrate the consequences of formula (32.5) when we have an oscillatingsystem, let us see what happens if the displacement x of the charge is oscillatingso that the acceleration a is −ω2x0eiωt. The average of the acceleration squared

32-4

over a cycle (remember that we have to be very careful when we square thingsthat are written in complex notation—it really is the cosine, and the averageof cos2 ωt is one-half) thus is

Therefore

ha02i = 1

2 ω4x20.P = q2ω4x2012π0c3 .

(32.6)

The formulas we are now discussing are relatively advanced and more or lessmodern; they date from the beginning of the twentieth century, and they are veryfamous. Because of their historical value, it is important for us to be able to readabout them in older books. In fact, the older books also used a system of unitsdiﬀerent from our present mks system. However, all these complications can bestraightened out in the ﬁnal formulas dealing with electrons by the followingrule: The quantity q2e /4π0, where qe is the electronic charge (in coulombs), has,historically, been written as e2. It is very easy to calculate that e in the mkssystem is numerically equal to 1.5188×10−14, because we know that, numerically,qe = 1.60206 × 10−19 and 1/4π0 = 8.98748 × 109. Therefore we shall often usethe convenient abbreviation

e2 = q2e4π0

(32.7)If we use the above numerical value of e in the older formulas and treat them asthough they were written in mks units, we will get the right numerical results.3 e2a02/c3. Again, the potentialFor example, the older form of (32.5) is P = 2energy of a proton and an electron at distance r is q2e /4π0r or e2/r, withe = 1.5188 × 10−14 (mks).

.

32-3 Radiation dampingNow the fact that an oscillator loses a certain energy would mean that if wehad a charge on the end of a spring (or an electron in an atom) which has anatural frequency ω0, and we start it oscillating and let it go, it will not oscillateforever, even if it is in empty space millions of miles from anything. There is nooil, no resistance, in an ordinary sense; no「viscosity.」But nevertheless it willnot oscillate, as we might once have said,「forever,」because if it is charged it isradiating energy, and therefore the oscillation will slowly die out. How slowly?What is the Q of such an oscillator, caused by the electromagnetic eﬀects, the

32-5

so-called radiation resistance or radiation damping of the oscillator? The Q ofany oscillating system is the total energy content of the oscillator at any timedivided by the energy loss per radian:

Q = W

dW/dφ

.

Or (another way to write it), since dW/dφ = (dW/dt)/(dφ/dt) = (dW/dt)/ω,

Q = ωWdW/dt

.

(32.8)

If for a given Q this tells us how the energy of the oscillation dies out, dW/dt =−(ω/Q)W, which has the solution W = W0e−ωt/Q if W0 is the initial energy(at t = 0).To ﬁnd the Q for a radiator, we go back to (32.8) and use (32.6) for dW/dt.Now what do we use for the energy W of the oscillator? The kinetic energyof the oscillator is 10/4. But weremember that for the total energy of an oscillator, on the average half is kineticand half is potential energy, and so we double our result, and ﬁnd for the totalenergy of the oscillator

2 mv2, and the mean kinetic energy is mω2x2

W = 1

(32.9)What do we use for the frequency in our formulas? We use the natural frequency ω0because, for all practical purposes, that is the frequency at which our atom isradiating, and for m we use the electron mass me. Then, making the necessarydivisions and cancellations, the formula comes down to

2 mω2x20.

1Q

= 4πe2

3λmec2 .

(32.10)

(In order to see it better and in a more historical form we write it using ourabbreviation q2e /4π0 = e2, and the factor ω0/c which was left over has beenwritten as 2π/λ.) Since Q is dimensionless, the combination e2/mec2 must bea property only of the electron charge and mass, an intrinsic property of theelectron, and it must be a length. It has been given a name, the classical electronradius, because the early atomic models, which were invented to explain theradiation resistance on the basis of the force of one part of the electron actingon the other parts, all needed to have an electron whose dimensions were of this

32-6

general order of magnitude. However, this quantity no longer has the signiﬁcancethat we believe that the electron really has such a radius. Numerically, themagnitude of the radius is

r0 = e2mec2

= 2.82 × 10−15 m.

(32.11)

Now let us actually calculate the Q of an atom that is emitting light—let ussay a sodium atom. For a sodium atom, the wavelength is roughly 6000 angstroms,in the yellow part of the visible spectrum, and this is a typical wavelength. Thus

Q = 3λ4πr0

≈ 5 × 107,

(32.12)

so the Q of an atom is of the order 108. This means that an atomic oscillatorwill oscillate for 108 radians or about 107 oscillations, before its energy falls by afactor 1/e. The frequency of oscillation of light corresponding to 6000 angstroms,ν = c/λ, is on the order of 1015 cycles/sec, and therefore the lifetime, the timeit takes for the energy of a radiating atom to die out by a factor 1/e, is on theorder of 10−8 sec. In ordinary circumstances, freely emitting atoms usually takeabout this long to radiate. This is valid only for atoms which are in empty space,not being disturbed in any way. If the electron is in a solid and it has to hitother atoms or other electrons, then there are additional resistances and diﬀerentdamping.

The eﬀective resistance term γ in the resistance law for the oscillator canbe found from the relation 1/Q = γ/ω0, and we remember that the size of γdetermines how wide the resonance curve is (Fig. 23-2). Thus we have justcomputed the widths of spectral lines for freely radiating atoms! Since λ = 2πc/ω,we ﬁnd that

∆λ = 2πc ∆ω/ω2 = 2πcγ/ω2

0 = 2πc/Qω0= λ/Q = 4πr0/3 = 1.18 × 10−14 m.

(32.13)

32-4 Independent sourcesIn preparation for our second topic, the scattering of light, we must nowdiscuss a certain feature of the phenomenon of interference that we neglected todiscuss previously. This is the question of when interference does not occur. Ifwe have two sources S1 and S2, with amplitudes A1 and A2, and we make an

32-7

observation in a certain direction in which the phases of arrival of the two signalsare φ1 and φ2 (a combination of the actual time of oscillation and the delayedtime, depending on the position of observation), then the energy that we receivecan be found by compounding the two complex number vectors A1 and A2, oneat angle φ1 and the other at angle φ2 (as we did in Chapter 29) and we ﬁnd thatthe resultant energy is proportional to

A2

R

= A2

1 + A2

1 + A2

2 + 2A1A2 cos (φ1 − φ2).

(32.14)Now if the cross term 2A1A2 cos (φ1 − φ2) were not there, then the total energythat would be received in a given direction would simply be the sum of theenergies, A22, that would be liberated by each source separately, which iswhat we usually expect. That is, the combined intensity of light shining onsomething from two sources is the sum of the intensities of the two lights. On theother hand, if we have things set just right and we have a cross term, it is notsuch a sum, because there is also some interference. If there are circumstancesin which this term is of no importance, then we would say the interference isapparently lost. Of course, in nature it is always there, but we may not be ableto detect it.

Let us consider some examples. Suppose, ﬁrst, that the two sources are7,000,000,000 wavelengths apart, not an impossible arrangement. Then in a givendirection it is true that there is a very deﬁnite value of these phase diﬀerences.But, on the other hand, if we move just a hair in one direction, a few wavelengths,which is no distance at all (our eye already has a hole in it that is so large that weare averaging the eﬀects over a range very wide compared with one wavelength)then we change the relative phase, and the cosine changes very rapidly. If wetake the average of the intensity over a little region, then the cosine, which goesplus, minus, plus, minus, as we move around, averages to zero.

So if we average over regions where the phase varies very rapidly with position,

we get no interference.

Another example. Suppose that the two sources are two independent radiooscillators—not a single oscillator being fed by two wires, which guarantees thatthe phases are kept together, but two independent sources—and that they are notprecisely tuned at the same frequency (it is very hard to make them at exactlythe same frequency without actually wiring them together). In this case we havewhat we call two independent sources. Of course, since the frequencies are notexactly equal, although they started in phase, one of them begins to get a little

32-8

ahead of the other, and pretty soon they are out of phase, and then it gets stillfurther ahead, and pretty soon they are in phase again. So the phase diﬀerencebetween the two is gradually drifting with time, but if our observation is so crudethat we cannot see that little time, if we average over a much longer time, thenalthough the intensity swells and falls like what we call「beats」in sound, if theseswellings and fallings are too rapid for our equipment to follow, then again thisterm averages out.

In other words, in any circumstance in which the phase shift averages out, we

get no interference!

One ﬁnds many books which say that two distinct light sources never interfere.This is not a statement of physics, but is merely a statement of the degree ofsensitivity of the technique of the experiments at the time the book was written.What happens in a light source is that ﬁrst one atom radiates, then another atomradiates, and so forth, and we have just seen that atoms radiate a train of wavesonly for about 10−8 sec; after 10−8 sec, some atom has probably taken over, thenanother atom takes over, and so on. So the phases can really only stay the samefor about 10−8 sec. Therefore, if we average for very much more than 10−8 sec,we do not see an interference from two diﬀerent sources, because they cannot holdtheir phases steady for longer than 10−8 sec. With photocells, very high-speeddetection is possible, and one can show that there is an interference which varieswith time, up and down, in about 10−8 sec. But most detection equipment, ofcourse, does not look at such ﬁne time intervals, and thus sees no interference.Certainly with the eye, which has a tenth-of-a-second averaging time, there is nochance whatever of seeing an interference between two diﬀerent ordinary sources.Recently it has become possible to make light sources which get around thiseﬀect by making all the atoms emit together in time. The device which does thisis a very complicated thing, and has to be understood in a quantum-mechanicalway. It is called a laser, and it is possible to produce from a laser a source inwhich the time during which the phase is kept constant, is very much longer than10−8 sec. It can be of the order of a hundredth, a tenth, or even one second, andso, with ordinary photocells, one can pick up the frequency between two diﬀerentlasers. One can easily detect the pulsing of the beats between two laser sources.Soon, no doubt, someone will be able to demonstrate two sources shining on awall, in which the beats are so slow that one can see the wall get bright and dark!Another case in which the interference averages out is that in which, insteadof having only two sources, we have many. In this case, we would write theexpression for A2as the sum of a whole lot of amplitudes, complex numbers,

R

32-9

squared, and we would get the square of each one, all added together, plus crossterms between every pair, and if the circumstances are such that the latter averageout, then there will be no eﬀects of interference. It may be that the various sourcesare located in such random positions that, although the phase diﬀerence betweenA2 and A3 is also deﬁnite, it is very diﬀerent from that between A1 and A2, etc.So we would get a whole lot of cosines, many plus, many minus, all averaging out.So it is that in many circumstances we do not see the eﬀects of interference,but see only a collective, total intensity equal to the sum of all the intensities.

32-5 Scattering of lightThe above leads us to an eﬀect which occurs in air as a consequence of theirregular positions of the atoms. When we were discussing the index of refraction,we saw that an incoming beam of light will make the atoms radiate again. Theelectric ﬁeld of the incoming beam drives the electrons up and down, and theyradiate because of their acceleration. This scattered radiation combines to givea beam in the same direction as the incoming beam, but of somewhat diﬀerentphase, and this is the origin of the index of refraction.

But what can we say about the amount of re-radiated light in some otherdirection? Ordinarily, if the atoms are very beautifully located in a nice pattern,it is easy to show that we get nothing in other directions, because we are addinga lot of vectors with their phases always changing, and the result comes to zero.But if the objects are randomly located, then the total intensity in any directionis the sum of the intensities that are scattered by each atom, as we have justdiscussed. Furthermore, the atoms in a gas are in actual motion, so that althoughthe relative phase of two atoms is a deﬁnite amount now, later the phase would bequite diﬀerent, and therefore each cosine term will average out. Therefore, to ﬁndout how much light is scattered in a given direction by a gas, we merely study theeﬀects of one atom and multiply the intensity it radiates by the number of atoms.Earlier, we remarked that the phenomenon of scattering of light of this natureis the origin of the blue of the sky. The sunlight goes through the air, and whenwe look to one side of the sun—say at 90◦ to the beam—we see blue light; whatwe now have to calculate is how much light we see and why it is blue.If the incident beam has the electric ﬁeld* E = ˆE0eiωt at the point wherethe atom is located, we know that an electron in the atom will vibrate up and

* When a caret appears on a vector it signiﬁes that the components of the vector are complex:

ˆE = ( ˆEx, ˆEy, ˆEz).

32-10

Fig. 32-2. A beam of radiation falls on an atom and causes thecharges (electrons) in the atom to move. The moving electrons in turnradiate in various directions.

down in response to this E (Fig. 32-2). From Eq. (23.8), the response will be

ˆx =

ˆE0

m(ω2

qe0 − ω2 + iγω) .

(32.15)

We could include the damping and the possibility that the atom acts like severaloscillators of diﬀerent frequency and sum over the various frequencies, but forsimplicity let us just take one oscillator and neglect the damping. Then theresponse to the external electric ﬁeld, which we have already used in the calculationof the index of refraction, is simply

ˆx =

ˆE0qe0 − ω2) .m(ω2

(32.16)

We could now easily calculate the intensity of light that is emitted in variousdirections, using formula (32.2) and the acceleration corresponding to the above ˆx.Rather than do this, however, we shall simply calculate the total amount oflight scattered in all directions, just to save time. The total amount of lightenergy per second, scattered in all directions by the single atom, is of coursegiven by Eq. (32.6). So, putting together the various pieces and regrouping them,we get

P = [(q2= ( 1= ( 1

e ω4/12π0c3)q20)(8π/3)(q42 0cE20)(8πr22 0cE2

e

e E20 /m2e /16π22

(ω2 − ω20m20/3)[ω4/(ω2 − ω2

0)2]

ec4)[ω4/(ω2 − ω20)2]

0)2]

for the total scattered power, radiated in all directions.

32-11

(32.17)

2 E2

We have written the result in the above form because it is then easy toremember: First, the total energy that is scattered is proportional to the squareof the incident ﬁeld. What does that mean? Obviously, the square of the incidentﬁeld is proportional to the energy which is coming in per second. In fact, theenergy incident per square meter per second is 0c times the average hE2i ofthe square of the electric ﬁeld, and if E0 is the maximum value of E, thenhE2i = 10. In other words, the total energy scattered is proportional to theenergy per square meter that comes in; the brighter the sunlight that is shiningin the sky, the brighter the sky is going to look.

Next, what fraction of the incoming light is scattered? Let us imagine a「target」with a certain area, let us say σ, in the beam (not a real, material target,because this would diﬀract light, and so on; we mean an imaginary area drawnin space). The total amount of energy that would pass through this surface σin a given circumstance is proportional both to the incoming intensity and to σ,and the total power would be

P = ( 1

2 0cE2

0)σ.

(32.18)

Now we invent an idea: we say that the atom scatters a total amount ofintensity which is the amount which would fall on a certain geometrical area,and we give the answer by giving that area. That answer, then, is independentof the incident intensity; it gives the ratio of the energy scattered to the energyincident per square meter. In other words, the ratiototal energy scattered per second

energy incident per square meter per second is an area.

The signiﬁcance of this area is that, if all the energy that impinged on that areawere to be spewed in all directions, then that is the amount of energy that wouldbe scattered by the atom.

This area is called a cross section for scattering; the idea of cross section isused constantly, whenever some phenomenon occurs in proportion to the intensityof a beam. In such cases one always describes the amount of the phenomenon bysaying what the eﬀective area would have to be to pick up that much of the beam.It does not mean in any way that this oscillator actually has such an area. Ifthere were nothing present but a free electron shaking up and down there wouldbe no area directly associated with it, physically. It is merely a way of expressingthe answer to a certain kind of problem; it tells us what area the incident beam

32-12

0

·

ω4

would have to hit in order to account for that much energy coming oﬀ. Thus, forour case,

(ω2 − ω20)2

σs = 8πr23(the subscript s is for「scattering」).Let us look at some examples. First, if we go to a very low natural frequency ω0,or to completely unbound electrons, for which ω0 = 0, then the frequency ωcancels out and the cross section is a constant. This low-frequency limit, or thefree electron cross section, is known as the Thomson scattering cross section. Itis an area whose dimensions are approximately 10−15 meter, more or less, on aside, i.e., 10−30 square meter, which is rather small!

(32.19)

On the other hand, if we take the case of light in the air, we remember that forair the natural frequencies of the oscillators are higher than the frequency of thelight that we use. This means that, to a ﬁrst approximation, we can disregard ω2in the denominator, and we ﬁnd that the scattering is proportional to the fourthpower of the frequency. That is to say, light which is of higher frequency by, say,a factor of two, is sixteen times more intensely scattered, which is a quite sizablediﬀerence. This means that blue light, which has about twice the frequency ofthe reddish end of the spectrum, is scattered to a far greater extent than redlight. Thus when we look at the sky it looks that glorious blue that we see allthe time!

There are several points to be made about the above results. One interestingquestion is, why do we ever see the clouds? Where do the clouds come from?Everybody knows it is the condensation of water vapor. But, of course, thewater vapor is already in the atmosphere before it condenses, so why don’t wesee it then? After it condenses it is perfectly obvious. It wasn’t there, now it isthere. So the mystery of where the clouds come from is not really such a childishmystery as「Where does the water come from, Daddy?,」but has to be explained.We have just explained that every atom scatters light, and of course the watervapor will scatter light, too. The mystery is why, when the water is condensedinto clouds, does it scatter such a tremendously greater amount of light?

Consider what would happen if, instead of a single atom, we had an agglom-erate of atoms, say two, very close together compared with the wavelength of thelight. Remember, atoms are only an angstrom or so across, while the wavelengthof light is some 5000 angstroms, so when they form a clump, a few atoms together,they can be very close together compared with the wavelength of light. Then

32-13

when the electric ﬁeld acts, both of the atoms will move together. The electricﬁeld that is scattered will then be the sum of the two electric ﬁelds in phase, i.e.,double the amplitude that there was with a single atom, and the energy whichis scattered is therefore four times what it is with a single atom, not twice! Solumps of atoms radiate or scatter more energy than they do as single atoms. Ourargument that the phases are independent is based on the assumption that thereis a real and large diﬀerence in phase between any two atoms, which is true onlyif they are several wavelengths apart and randomly spaced, or moving. But ifthey are right next to each other, they necessarily scatter in phase, and they havea coherent interference which produces an increase in the scattering.

If we have N atoms in a lump, which is a tiny droplet of water, then each onewill be driven by the electric ﬁeld in about the same way as before (the eﬀect ofone atom on the other is not important; it is just to get the idea anyway) andthe amplitude of scattering from each one is the same, so the total ﬁeld which isscattered is N-fold increased. The intensity of the light which is scattered is thenthe square, or N 2-fold, increased. We would have expected, if the atoms werespread out in space, only N times as much as 1, whereas we get N 2 times asmuch as 1! That is to say, the scattering of water in lumps of N molecules eachis N times more intense than the scattering of the single atoms. So as the wateragglomerates the scattering increases. Does it increase ad inﬁnitum? No! Whendoes this analysis begin to fail? How many atoms can we put together beforewe cannot drive this argument any further? Answer: If the water drop gets sobig that from one end to the other is a wavelength or so, then the atoms areno longer all in phase because they are too far apart. So as we keep increasingthe size of the droplets we get more and more scattering, until such a time thata drop gets about the size of a wavelength, and then the scattering does notincrease anywhere nearly as rapidly as the drop gets bigger. Furthermore, theblue disappears, because for long wavelengths the drops can be bigger, beforethis limit is reached, than they can be for short wavelengths. Although the shortwaves scatter more per atom than the long waves, there is a bigger enhancementfor the red end of the spectrum than for the blue end when all the drops arebigger than the wavelength, so the color is shifted from the blue toward the red.Now we can make an experiment that demonstrates this. We can makeparticles that are very small at ﬁrst, and then gradually grow in size. We use asolution of sodium thiosulfate (hypo) with sulfuric acid, which precipitates veryﬁne grains of sulfur. As the sulfur precipitates, the grains ﬁrst start very small,and the scattering is a little bluish. As it precipitates more it gets more intense,

32-14

and then it will get whitish as the particles get bigger. In addition, the lightwhich goes straight through will have the blue taken out. That is why the sunsetis red, of course, because the light that comes through a lot of air, to the eye hashad a lot of blue light scattered out, so it is yellow-red.

Finally, there is one other important feature which really belongs in the nextchapter, on polarization, but it is so interesting that we point it out now. Thisis that the electric ﬁeld of the scattered light tends to vibrate in a particulardirection. The electric ﬁeld in the incoming light is oscillating in some way, andthe driven oscillator goes in this same direction, and if we are situated about atright angles to the beam, we will see polarized light, that is to say, light in whichthe electric ﬁeld is going only one way. In general, the atoms can vibrate in anydirection at right angles to the beam, but if they are driven directly toward oraway from us, we do not see it. So if the incoming light has an electric ﬁeld whichchanges and oscillates in any direction, which we call unpolarized light, then thelight which is coming out at 90◦ to the beam vibrates in only one direction! (SeeFig. 32-3.)

Fig. 32-3. Illustration of the origin of the polarization of radiation

scattered at right angles to the incident beam.

There is a substance called polaroid which has the property that when lightgoes through it, only the piece of the electric ﬁeld which is along one particularaxis can get through. We can use this to test for polarization, and indeed we ﬁndthe light scattered by the hypo solution to be strongly polarized.

32-15

33

