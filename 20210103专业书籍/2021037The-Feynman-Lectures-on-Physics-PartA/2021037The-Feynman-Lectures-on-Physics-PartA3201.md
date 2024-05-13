Radiation Damping. Light Scattering

32-1 Radiation resistance In the last chapter we learned that when a system is oscillating, energy is carried away, and we deduced a formula for the energy which is radiated by an oscillating system. If we know the electric ﬁeld, then the average of the square of the ﬁeld times 0c is the amount of energy that passes per square meter per second through a surface normal to the direction in which the radiation is going:

S = 0chE2i.

(32.1)

Any oscillating charge radiates energy; for instance, a driven antenna radiates energy. If the system radiates energy, then in order to account for the conservation of energy we must ﬁnd that power is being delivered along the wires which lead into the antenna. That is, to the driving circuit the antenna acts like a resistance, or a place where energy can be「lost」(the energy is not really lost, it is really radiated out, but so far as the circuit is concerned, the energy is lost). In an ordinary resistance, the energy which is「lost」passes into heat; in this case the energy which is「lost」goes out into space. But from the standpoint of circuit theory, without considering where the energy goes, the net eﬀect on the circuit is the same—energy is「lost」from that circuit. Therefore the antenna appears to the generator as having a resistance, even though it may be made with perfectly good copper. In fact, if it is well built it will appear as almost a pure resistance, with very little inductance or capacitance, because we would like to radiate as much energy as possible out of the antenna. This resistance that an antenna shows is called the radiation resistance. If a current I is going to the antenna, then the average rate at which power is delivered to the antenna is the average of the square of the current times the resistance. The rate at which power is radiated by the antenna is proportional

32-1

to the square of the current in the antenna, of course, because all the ﬁelds are proportional to the currents, and the energy liberated is proportional to the square of the ﬁeld. The coeﬃcient of proportionality between radiated power and hI2i is the radiation resistance. An interesting question is, what is this radiation resistance due to? Let us take a simple example: let us say that currents are driven up and down in an antenna. We ﬁnd that we have to put work in, if the antenna is to radiate energy. If we take a charged body and accelerate it up and down it radiates energy; if it were not charged it would not radiate energy. It is one thing to calculate from the conservation of energy that energy is lost, but another thing to answer the question, against what force are we doing the work? That is an interesting and very diﬃcult question which has never been completely and satisfactorily answered for electrons, although it has been for antennas. What happens is this: in an antenna, the ﬁelds produced by the moving charges in one part of the antenna react on the moving charges in another part of the antenna. We can calculate these forces and ﬁnd out how much work they do, and so ﬁnd the right rule for the radiation resistance. When we say「We can calculate—」that is not quite right—we cannot, because we have not yet studied the laws of electricity at short distances; only at large distances do we know what the electric ﬁeld is. We saw the formula (28.3), but at present it is too complicated for us to calculate the ﬁelds inside the wave zone. Of course, since conservation of energy is valid, we can calculate the result all right without knowing the ﬁelds at short distances. (As a matter of fact, by using this argument backwards it turns out that one can ﬁnd the formula for the forces at short distances only by knowing the ﬁeld at very large distances, by using the laws of conservation of energy, but we shall not go into that here.)

The problem in the case of a single electron is this: if there is only one charge, what can the force act on? It has been proposed, in the old classical theory, that the charge was a little ball, and that one part of the charge acted on the other part. Because of the delay in the action across the tiny electron, the force is not exactly in phase with the motion. That is, if we have the electron standing still, we know that「action equals reaction.」So the various internal forces are equal, and there is no net force. But if the electron is accelerating, then because of the time delay across it, the force which is acting on the front from the back is not exactly the same as the force on the back from the front, because of the delay in the eﬀect. This delay in the timing makes for a lack of balance, so, as a net eﬀect, the thing holds itself back by its bootstraps! This model of the origin of the

32-2

resistance to acceleration, the radiation resistance of a moving charge, has run into many diﬃculties, because our present view of the electron is that it is not a「little ball」; this problem has never been solved. Nevertheless we can calculate exactly, of course, what the net radiation resistance force must be, i.e., how much loss there must be when we accelerate a charge, in spite of not knowing directly the mechanism of how that force works.

32-2 The rate of radiation of energy Now we shall calculate the total energy radiated by an accelerating charge. To keep the discussion general, we shall take the case of a charge accelerating any which way, but nonrelativistically. At a moment when the acceleration is, say, vertical, we know that the electric ﬁeld that is generated is the charge multiplied by the projection of the retarded acceleration, divided by the distance. So we know the electric ﬁeld at any point, and we therefore know the square of the electric ﬁeld and thus the energy 0cE2 leaving through a unit area per second. The quantity 0c appears quite often in expressions involving radiowave propagation. Its reciprocal is called the impedance of a vacuum, and it is an easy number to remember: it has the value 1/0c = 377 ohms. So the power in watts per square meter is equal to the average of the ﬁeld squared, divided by 377.

Using our expression (29.1) for the electric ﬁeld, we ﬁnd that

S = q2a02 sin2 θ 16π20r2c3

(32.2)

is the power per square meter radiated in the direction θ. We notice that it goes inversely as the square of the distance, as we said before. Now suppose we wanted the total energy radiated in all directions: then we must integrate (32.2) over all directions. First we multiply by the area, to ﬁnd the amount that ﬂows within a little angle dθ (Fig. 32-1). We need the area of a spherical section. The way to think of it is this: if r is the radius, then the width of the annular segment is r dθ, and the circumference is 2πr sin θ, because r sin θ is the radius of the circle. So the area of the little piece of the sphere is 2πr sin θ times r dθ:

dA = 2πr2 sin θ dθ.

(32.3)

By multiplying the ﬂux [(32.2), the power per square meter] by the area in square meters included in the small angle dθ, we ﬁnd the amount of energy that is

32-3

Fig. 32-1. The area of a spherical segment is 2πr sin θ · r dθ.

liberated in this direction between θ and θ + dθ; then we integrate that over all the angles θ from 0 to 180◦:

Z

Z π

By writing sin3 θ = (1−cos2 θ) sin θ it is not hard to show thatR π

0

sin3 θ dθ.

P =

S dA = q2a02 8π0c3

Using that fact, we ﬁnally get

(32.4)

0 sin3 θ dθ = 4/3.

P = q2a02 6π0c3 .

(32.5)

This expression deserves some remarks. First of all, since the vector a0 had a certain direction, the a02 in (32.5) would be the square of the vector a0, that is, a0 · a0, the length of the vector, squared. Secondly, the ﬂux (32.2) was calculated using the retarded acceleration; that is, the acceleration at the time at which the energy now passing through the sphere was radiated. We might like to say that this energy was in fact liberated at this earlier time. This is not exactly true; it is only an approximate idea. The exact time when the energy is liberated cannot be deﬁned precisely. All we can really calculate precisely is what happens in a complete motion, like an oscillation or something, where the acceleration ﬁnally ceases. Then what we ﬁnd is that the total energy ﬂux per cycle is the average of acceleration squared, for a complete cycle. This is what should really appear in (32.5). Or, if it is a motion with an acceleration that is initially and ﬁnally zero, then the total energy that has ﬂown out is the time integral of (32.5).

To illustrate the consequences of formula (32.5) when we have an oscillating system, let us see what happens if the displacement x of the charge is oscillating so that the acceleration a is −ω2x0eiωt. The average of the acceleration squared

32-4

over a cycle (remember that we have to be very careful when we square things that are written in complex notation—it really is the cosine, and the average of cos2 ωt is one-half) thus is

Therefore

ha02i = 1

2 ω4x2 0. P = q2ω4x2 0 12π0c3 .

(32.6)

The formulas we are now discussing are relatively advanced and more or less modern; they date from the beginning of the twentieth century, and they are very famous. Because of their historical value, it is important for us to be able to read about them in older books. In fact, the older books also used a system of units diﬀerent from our present mks system. However, all these complications can be straightened out in the ﬁnal formulas dealing with electrons by the following rule: The quantity q2 e /4π0, where qe is the electronic charge (in coulombs), has, historically, been written as e2. It is very easy to calculate that e in the mks system is numerically equal to 1.5188×10−14, because we know that, numerically, qe = 1.60206 × 10−19 and 1/4π0 = 8.98748 × 109. Therefore we shall often use the convenient abbreviation

e2 = q2 e4π0

(32.7) If we use the above numerical value of e in the older formulas and treat them as though they were written in mks units, we will get the right numerical results. 3 e2a02/c3. Again, the potential For example, the older form of (32.5) is P = 2 energy of a proton and an electron at distance r is q2 e /4π0r or e2/r, with e = 1.5188 × 10−14 (mks).

.

32-3 Radiation damping Now the fact that an oscillator loses a certain energy would mean that if we had a charge on the end of a spring (or an electron in an atom) which has a natural frequency ω0, and we start it oscillating and let it go, it will not oscillate forever, even if it is in empty space millions of miles from anything. There is no oil, no resistance, in an ordinary sense; no「viscosity.」But nevertheless it will not oscillate, as we might once have said,「forever,」because if it is charged it is radiating energy, and therefore the oscillation will slowly die out. How slowly? What is the Q of such an oscillator, caused by the electromagnetic eﬀects, the

32-5

so-called radiation resistance or radiation damping of the oscillator? The Q of any oscillating system is the total energy content of the oscillator at any time divided by the energy loss per radian:

Q = W

dW/dφ

.

Or (another way to write it), since dW/dφ = (dW/dt)/(dφ/dt) = (dW/dt)/ω,

Q = ωW dW/dt

.

(32.8)

If for a given Q this tells us how the energy of the oscillation dies out, dW/dt = −(ω/Q)W, which has the solution W = W0e−ωt/Q if W0 is the initial energy (at t = 0). To ﬁnd the Q for a radiator, we go back to (32.8) and use (32.6) for dW/dt. Now what do we use for the energy W of the oscillator? The kinetic energy of the oscillator is 1 0/4. But we remember that for the total energy of an oscillator, on the average half is kinetic and half is potential energy, and so we double our result, and ﬁnd for the total energy of the oscillator

2 mv2, and the mean kinetic energy is mω2x2

W = 1

(32.9) What do we use for the frequency in our formulas? We use the natural frequency ω0 because, for all practical purposes, that is the frequency at which our atom is radiating, and for m we use the electron mass me. Then, making the necessary divisions and cancellations, the formula comes down to

2 mω2x2 0.

1 Q

= 4πe2

3λmec2 .

(32.10)

(In order to see it better and in a more historical form we write it using our abbreviation q2 e /4π0 = e2, and the factor ω0/c which was left over has been written as 2π/λ.) Since Q is dimensionless, the combination e2/mec2 must be a property only of the electron charge and mass, an intrinsic property of the electron, and it must be a length. It has been given a name, the classical electron radius, because the early atomic models, which were invented to explain the radiation resistance on the basis of the force of one part of the electron acting on the other parts, all needed to have an electron whose dimensions were of this

32-6

general order of magnitude. However, this quantity no longer has the signiﬁcance that we believe that the electron really has such a radius. Numerically, the magnitude of the radius is

r0 = e2 mec2

= 2.82 × 10−15 m.

(32.11)

Now let us actually calculate the Q of an atom that is emitting light—let us say a sodium atom. For a sodium atom, the wavelength is roughly 6000 angstroms, in the yellow part of the visible spectrum, and this is a typical wavelength. Thus

Q = 3λ 4πr0

≈ 5 × 107,

(32.12)

so the Q of an atom is of the order 108. This means that an atomic oscillator will oscillate for 108 radians or about 107 oscillations, before its energy falls by a factor 1/e. The frequency of oscillation of light corresponding to 6000 angstroms, ν = c/λ, is on the order of 1015 cycles/sec, and therefore the lifetime, the time it takes for the energy of a radiating atom to die out by a factor 1/e, is on the order of 10−8 sec. In ordinary circumstances, freely emitting atoms usually take about this long to radiate. This is valid only for atoms which are in empty space, not being disturbed in any way. If the electron is in a solid and it has to hit other atoms or other electrons, then there are additional resistances and diﬀerent damping.

The eﬀective resistance term γ in the resistance law for the oscillator can be found from the relation 1/Q = γ/ω0, and we remember that the size of γ determines how wide the resonance curve is (Fig. 23-2). Thus we have just computed the widths of spectral lines for freely radiating atoms! Since λ = 2πc/ω, we ﬁnd that

∆λ = 2πc ∆ω/ω2 = 2πcγ/ω2

0 = 2πc/Qω0 = λ/Q = 4πr0/3 = 1.18 × 10−14 m.

(32.13)

32-4 Independent sources In preparation for our second topic, the scattering of light, we must now discuss a certain feature of the phenomenon of interference that we neglected to discuss previously. This is the question of when interference does not occur. If we have two sources S1 and S2, with amplitudes A1 and A2, and we make an

32-7

observation in a certain direction in which the phases of arrival of the two signals are φ1 and φ2 (a combination of the actual time of oscillation and the delayed time, depending on the position of observation), then the energy that we receive can be found by compounding the two complex number vectors A1 and A2, one at angle φ1 and the other at angle φ2 (as we did in Chapter 29) and we ﬁnd that the resultant energy is proportional to

A2

R

= A2

1 + A2

1 + A2

2 + 2A1A2 cos (φ1 − φ2).

(32.14) Now if the cross term 2A1A2 cos (φ1 − φ2) were not there, then the total energy that would be received in a given direction would simply be the sum of the energies, A2 2, that would be liberated by each source separately, which is what we usually expect. That is, the combined intensity of light shining on something from two sources is the sum of the intensities of the two lights. On the other hand, if we have things set just right and we have a cross term, it is not such a sum, because there is also some interference. If there are circumstances in which this term is of no importance, then we would say the interference is apparently lost. Of course, in nature it is always there, but we may not be able to detect it.

Let us consider some examples. Suppose, ﬁrst, that the two sources are 7,000,000,000 wavelengths apart, not an impossible arrangement. Then in a given direction it is true that there is a very deﬁnite value of these phase diﬀerences. But, on the other hand, if we move just a hair in one direction, a few wavelengths, which is no distance at all (our eye already has a hole in it that is so large that we are averaging the eﬀects over a range very wide compared with one wavelength) then we change the relative phase, and the cosine changes very rapidly. If we take the average of the intensity over a little region, then the cosine, which goes plus, minus, plus, minus, as we move around, averages to zero.

So if we average over regions where the phase varies very rapidly with position,

we get no interference.

Another example. Suppose that the two sources are two independent radio oscillators—not a single oscillator being fed by two wires, which guarantees that the phases are kept together, but two independent sources—and that they are not precisely tuned at the same frequency (it is very hard to make them at exactly the same frequency without actually wiring them together). In this case we have what we call two independent sources. Of course, since the frequencies are not exactly equal, although they started in phase, one of them begins to get a little

32-8

ahead of the other, and pretty soon they are out of phase, and then it gets still further ahead, and pretty soon they are in phase again. So the phase diﬀerence between the two is gradually drifting with time, but if our observation is so crude that we cannot see that little time, if we average over a much longer time, then although the intensity swells and falls like what we call「beats」in sound, if these swellings and fallings are too rapid for our equipment to follow, then again this term averages out.

In other words, in any circumstance in which the phase shift averages out, we

get no interference!

One ﬁnds many books which say that two distinct light sources never interfere. This is not a statement of physics, but is merely a statement of the degree of sensitivity of the technique of the experiments at the time the book was written. What happens in a light source is that ﬁrst one atom radiates, then another atom radiates, and so forth, and we have just seen that atoms radiate a train of waves only for about 10−8 sec; after 10−8 sec, some atom has probably taken over, then another atom takes over, and so on. So the phases can really only stay the same for about 10−8 sec. Therefore, if we average for very much more than 10−8 sec, we do not see an interference from two diﬀerent sources, because they cannot hold their phases steady for longer than 10−8 sec. With photocells, very high-speed detection is possible, and one can show that there is an interference which varies with time, up and down, in about 10−8 sec. But most detection equipment, of course, does not look at such ﬁne time intervals, and thus sees no interference. Certainly with the eye, which has a tenth-of-a-second averaging time, there is no chance whatever of seeing an interference between two diﬀerent ordinary sources. Recently it has become possible to make light sources which get around this eﬀect by making all the atoms emit together in time. The device which does this is a very complicated thing, and has to be understood in a quantum-mechanical way. It is called a laser, and it is possible to produce from a laser a source in which the time during which the phase is kept constant, is very much longer than 10−8 sec. It can be of the order of a hundredth, a tenth, or even one second, and so, with ordinary photocells, one can pick up the frequency between two diﬀerent lasers. One can easily detect the pulsing of the beats between two laser sources. Soon, no doubt, someone will be able to demonstrate two sources shining on a wall, in which the beats are so slow that one can see the wall get bright and dark! Another case in which the interference averages out is that in which, instead of having only two sources, we have many. In this case, we would write the expression for A2 as the sum of a whole lot of amplitudes, complex numbers,

R

32-9

squared, and we would get the square of each one, all added together, plus cross terms between every pair, and if the circumstances are such that the latter average out, then there will be no eﬀects of interference. It may be that the various sources are located in such random positions that, although the phase diﬀerence between A2 and A3 is also deﬁnite, it is very diﬀerent from that between A1 and A2, etc. So we would get a whole lot of cosines, many plus, many minus, all averaging out. So it is that in many circumstances we do not see the eﬀects of interference, but see only a collective, total intensity equal to the sum of all the intensities.

32-5 Scattering of light The above leads us to an eﬀect which occurs in air as a consequence of the irregular positions of the atoms. When we were discussing the index of refraction, we saw that an incoming beam of light will make the atoms radiate again. The electric ﬁeld of the incoming beam drives the electrons up and down, and they radiate because of their acceleration. This scattered radiation combines to give a beam in the same direction as the incoming beam, but of somewhat diﬀerent phase, and this is the origin of the index of refraction.

But what can we say about the amount of re-radiated light in some other direction? Ordinarily, if the atoms are very beautifully located in a nice pattern, it is easy to show that we get nothing in other directions, because we are adding a lot of vectors with their phases always changing, and the result comes to zero. But if the objects are randomly located, then the total intensity in any direction is the sum of the intensities that are scattered by each atom, as we have just discussed. Furthermore, the atoms in a gas are in actual motion, so that although the relative phase of two atoms is a deﬁnite amount now, later the phase would be quite diﬀerent, and therefore each cosine term will average out. Therefore, to ﬁnd out how much light is scattered in a given direction by a gas, we merely study the eﬀects of one atom and multiply the intensity it radiates by the number of atoms. Earlier, we remarked that the phenomenon of scattering of light of this nature is the origin of the blue of the sky. The sunlight goes through the air, and when we look to one side of the sun—say at 90◦ to the beam—we see blue light; what we now have to calculate is how much light we see and why it is blue. If the incident beam has the electric ﬁeld* E = ˆE0eiωt at the point where the atom is located, we know that an electron in the atom will vibrate up and

* When a caret appears on a vector it signiﬁes that the components of the vector are complex:

ˆE = ( ˆEx, ˆEy, ˆEz).

32-10

Fig. 32-2. A beam of radiation falls on an atom and causes the charges (electrons) in the atom to move. The moving electrons in turn radiate in various directions.

down in response to this E (Fig. 32-2). From Eq. (23.8), the response will be

ˆx =

ˆE0

m(ω2

qe 0 − ω2 + iγω) .

(32.15)

We could include the damping and the possibility that the atom acts like several oscillators of diﬀerent frequency and sum over the various frequencies, but for simplicity let us just take one oscillator and neglect the damping. Then the response to the external electric ﬁeld, which we have already used in the calculation of the index of refraction, is simply

ˆx =

ˆE0 qe 0 − ω2) . m(ω2

(32.16)

We could now easily calculate the intensity of light that is emitted in various directions, using formula (32.2) and the acceleration corresponding to the above ˆx. Rather than do this, however, we shall simply calculate the total amount of light scattered in all directions, just to save time. The total amount of light energy per second, scattered in all directions by the single atom, is of course given by Eq. (32.6). So, putting together the various pieces and regrouping them, we get

P = [(q2 = ( 1 = ( 1

e ω4/12π0c3)q2 0)(8π/3)(q4 2 0cE2 0)(8πr2 2 0cE2

e

e E2 0 /m2 e /16π22

(ω2 − ω2 0m2 0/3)[ω4/(ω2 − ω2

0)2]

ec4)[ω4/(ω2 − ω2 0)2]

0)2]

for the total scattered power, radiated in all directions.

32-11

(32.17)

2 E2

We have written the result in the above form because it is then easy to remember: First, the total energy that is scattered is proportional to the square of the incident ﬁeld. What does that mean? Obviously, the square of the incident ﬁeld is proportional to the energy which is coming in per second. In fact, the energy incident per square meter per second is 0c times the average hE2i of the square of the electric ﬁeld, and if E0 is the maximum value of E, then hE2i = 1 0. In other words, the total energy scattered is proportional to the energy per square meter that comes in; the brighter the sunlight that is shining in the sky, the brighter the sky is going to look.

Next, what fraction of the incoming light is scattered? Let us imagine a「target」with a certain area, let us say σ, in the beam (not a real, material target, because this would diﬀract light, and so on; we mean an imaginary area drawn in space). The total amount of energy that would pass through this surface σ in a given circumstance is proportional both to the incoming intensity and to σ, and the total power would be

P = ( 1

2 0cE2

0)σ.

(32.18)

Now we invent an idea: we say that the atom scatters a total amount of intensity which is the amount which would fall on a certain geometrical area, and we give the answer by giving that area. That answer, then, is independent of the incident intensity; it gives the ratio of the energy scattered to the energy incident per square meter. In other words, the ratio total energy scattered per second

energy incident per square meter per second is an area.

The signiﬁcance of this area is that, if all the energy that impinged on that area were to be spewed in all directions, then that is the amount of energy that would be scattered by the atom.

This area is called a cross section for scattering; the idea of cross section is used constantly, whenever some phenomenon occurs in proportion to the intensity of a beam. In such cases one always describes the amount of the phenomenon by saying what the eﬀective area would have to be to pick up that much of the beam. It does not mean in any way that this oscillator actually has such an area. If there were nothing present but a free electron shaking up and down there would be no area directly associated with it, physically. It is merely a way of expressing the answer to a certain kind of problem; it tells us what area the incident beam

32-12

0

·

ω4

would have to hit in order to account for that much energy coming oﬀ. Thus, for our case,

(ω2 − ω2 0)2

σs = 8πr2 3 (the subscript s is for「scattering」). Let us look at some examples. First, if we go to a very low natural frequency ω0, or to completely unbound electrons, for which ω0 = 0, then the frequency ω cancels out and the cross section is a constant. This low-frequency limit, or the free electron cross section, is known as the Thomson scattering cross section. It is an area whose dimensions are approximately 10−15 meter, more or less, on a side, i.e., 10−30 square meter, which is rather small!

(32.19)

On the other hand, if we take the case of light in the air, we remember that for air the natural frequencies of the oscillators are higher than the frequency of the light that we use. This means that, to a ﬁrst approximation, we can disregard ω2 in the denominator, and we ﬁnd that the scattering is proportional to the fourth power of the frequency. That is to say, light which is of higher frequency by, say, a factor of two, is sixteen times more intensely scattered, which is a quite sizable diﬀerence. This means that blue light, which has about twice the frequency of the reddish end of the spectrum, is scattered to a far greater extent than red light. Thus when we look at the sky it looks that glorious blue that we see all the time!

There are several points to be made about the above results. One interesting question is, why do we ever see the clouds? Where do the clouds come from? Everybody knows it is the condensation of water vapor. But, of course, the water vapor is already in the atmosphere before it condenses, so why don’t we see it then? After it condenses it is perfectly obvious. It wasn’t there, now it is there. So the mystery of where the clouds come from is not really such a childish mystery as「Where does the water come from, Daddy?,」but has to be explained. We have just explained that every atom scatters light, and of course the water vapor will scatter light, too. The mystery is why, when the water is condensed into clouds, does it scatter such a tremendously greater amount of light?

Consider what would happen if, instead of a single atom, we had an agglom- erate of atoms, say two, very close together compared with the wavelength of the light. Remember, atoms are only an angstrom or so across, while the wavelength of light is some 5000 angstroms, so when they form a clump, a few atoms together, they can be very close together compared with the wavelength of light. Then

32-13

when the electric ﬁeld acts, both of the atoms will move together. The electric ﬁeld that is scattered will then be the sum of the two electric ﬁelds in phase, i.e., double the amplitude that there was with a single atom, and the energy which is scattered is therefore four times what it is with a single atom, not twice! So lumps of atoms radiate or scatter more energy than they do as single atoms. Our argument that the phases are independent is based on the assumption that there is a real and large diﬀerence in phase between any two atoms, which is true only if they are several wavelengths apart and randomly spaced, or moving. But if they are right next to each other, they necessarily scatter in phase, and they have a coherent interference which produces an increase in the scattering.

If we have N atoms in a lump, which is a tiny droplet of water, then each one will be driven by the electric ﬁeld in about the same way as before (the eﬀect of one atom on the other is not important; it is just to get the idea anyway) and the amplitude of scattering from each one is the same, so the total ﬁeld which is scattered is N-fold increased. The intensity of the light which is scattered is then the square, or N 2-fold, increased. We would have expected, if the atoms were spread out in space, only N times as much as 1, whereas we get N 2 times as much as 1! That is to say, the scattering of water in lumps of N molecules each is N times more intense than the scattering of the single atoms. So as the water agglomerates the scattering increases. Does it increase ad inﬁnitum? No! When does this analysis begin to fail? How many atoms can we put together before we cannot drive this argument any further? Answer: If the water drop gets so big that from one end to the other is a wavelength or so, then the atoms are no longer all in phase because they are too far apart. So as we keep increasing the size of the droplets we get more and more scattering, until such a time that a drop gets about the size of a wavelength, and then the scattering does not increase anywhere nearly as rapidly as the drop gets bigger. Furthermore, the blue disappears, because for long wavelengths the drops can be bigger, before this limit is reached, than they can be for short wavelengths. Although the short waves scatter more per atom than the long waves, there is a bigger enhancement for the red end of the spectrum than for the blue end when all the drops are bigger than the wavelength, so the color is shifted from the blue toward the red. Now we can make an experiment that demonstrates this. We can make particles that are very small at ﬁrst, and then gradually grow in size. We use a solution of sodium thiosulfate (hypo) with sulfuric acid, which precipitates very ﬁne grains of sulfur. As the sulfur precipitates, the grains ﬁrst start very small, and the scattering is a little bluish. As it precipitates more it gets more intense,

32-14

and then it will get whitish as the particles get bigger. In addition, the light which goes straight through will have the blue taken out. That is why the sunset is red, of course, because the light that comes through a lot of air, to the eye has had a lot of blue light scattered out, so it is yellow-red.

Finally, there is one other important feature which really belongs in the next chapter, on polarization, but it is so interesting that we point it out now. This is that the electric ﬁeld of the scattered light tends to vibrate in a particular direction. The electric ﬁeld in the incoming light is oscillating in some way, and the driven oscillator goes in this same direction, and if we are situated about at right angles to the beam, we will see polarized light, that is to say, light in which the electric ﬁeld is going only one way. In general, the atoms can vibrate in any direction at right angles to the beam, but if they are driven directly toward or away from us, we do not see it. So if the incoming light has an electric ﬁeld which changes and oscillates in any direction, which we call unpolarized light, then the light which is coming out at 90◦ to the beam vibrates in only one direction! (See Fig. 32-3.)

Fig. 32-3. Illustration of the origin of the polarization of radiation

scattered at right angles to the incident beam.

There is a substance called polaroid which has the property that when light goes through it, only the piece of the electric ﬁeld which is along one particular axis can get through. We can use this to test for polarization, and indeed we ﬁnd the light scattered by the hypo solution to be strongly polarized.

32-15

33

