11

Inside Dielectrics

11-1 Molecular dipolesIn

this chapter we are going to discuss why it is that materials are dielectric.We said in the last chapter that we could understand the properties of electricalsystems with dielectrics once we appreciated that when an electric ﬁeld is appliedto a dielectric it induces a dipole moment in the atoms. Speciﬁcally, if theelectric ﬁeld E induces an average dipole moment per unit volume P, then κ,the dielectric constant, is given by

κ − 1 = P0E

.

(11.1)

We have already discussed how this equation is applied; now we have todiscuss the mechanism by which polarization arises when there is an electric ﬁeldinside a material. We begin with the simplest possible example—the polarizationof gases. But even gases already have complications: there are two types. Themolecules of some gases, like oxygen, which has a symmetric pair of atoms in eachmolecule, have no inherent dipole moment. But the molecules of others, like watervapor (which has a nonsymmetric arrangement of hydrogen and oxygen atoms)carry a permanent electric dipole moment. As we pointed out in Chapter 6, thereis in the water vapor molecule an average plus charge on the hydrogen atomsand a negative charge on the oxygen. Since the center of gravity of the negativecharge and the center of gravity of the positive charge do not coincide, the totalcharge distribution of the molecule has a dipole moment. Such a molecule iscalled a polar molecule. In oxygen, because of the symmetry of the molecule, thecenters of gravity of the positive and negative charges are the same, so it is anonpolar molecule. It does, however, become a dipole when placed in an electricﬁeld. The forms of the two types of molecules are sketched in Fig. 11-1.

11-2 Electronic polarizationWe will ﬁrst discuss the polarization of non polar molecules. We can start withthe simplest case of a monatomic gas (for instance, helium). When an atom ofsuch a gas is in an electric ﬁeld, the electrons are pulled one way by the ﬁeld whilethe nucleus is pulled the other way, as shown in Fig. 10-4. Although the atomsare very stiﬀ with respect to the electrical forces we can apply experimentally,there is a slight net displacement of the centers of charge, and a dipole momentis induced. For small ﬁelds, the amount of displacement, and so also the dipolemoment, is proportional to the electric ﬁeld. The displacement of the electrondistribution which produces this kind of induced dipole moment is called electronicpolarization.We have already discussed the inﬂuence of an electric ﬁeld on an atom inChapter 31 of Vol. I, when we were dealing with the theory of the index ofrefraction. If you think about it for a moment, you will see that what we mustdo now is exactly the same as we did then. But now we need worry only aboutﬁelds that do not vary with time, while the index of refraction depended ontime-varying ﬁelds.

In Chapter 31 of Vol. I we supposed that when an atom is placed in anoscillating electric ﬁeld the center of charge of the electrons obeys the equation

d2xdt2

m

+ mω2

0x = qeE.

(11.2)

11-1

11-4 Electric ﬁelds in cavities of a

polarization

dielectric

11-1 Molecular dipoles11-2 Electronic polarization11-3 Polar molecules; orientation

11-5 The dielectric constant of liquids;

the Clausius-Mossotti equation

11-6 Solid dielectrics11-7 Ferroelectricity; BaTiO3

Review: Chapter 31, Vol. I, The Originof the Refractive IndexChapter 40, Vol. I, The Prin-ciples of Statistical Mechanics

Fig. 11-1.

(a) An oxygen moleculewith zero dipole moment.(b) The wa-ter molecule has a permanent dipole mo-ment p0.

The ﬁrst term is the electron mass times its acceleration and the second is arestoring force, while the right-hand side is the force from the outside electricﬁeld. If the electric ﬁeld varies with the frequency ω, Eq. (11.2) has the solution

x =

m(ω2

qeE0 − ω2) ,

(11.3)

which has a resonance at ω = ω0. When we previously found this solution, weinterpreted it as saying that ω0 was the frequency at which light (in the opticalregion or in the ultraviolet, depending on the atom) was absorbed. For ourpurposes, however, we are interested only in the ease of constant ﬁelds, i.e.,for ω = 0, so we can disregard the acceleration term in (11.2), and we ﬁnd thatthe displacement is

From this we see that the dipole moment p of a single atom is

x = qeEmω20

.

p = qex = q2e Emω20

.

(11.4)

(11.5)

In this theory the dipole moment p is indeed proportional to the electric ﬁeld.

People usually write

p = α0E.

(11.6)(Again the 0 is put in for historical reasons.) The constant α is called thepolarizability of the atom, and has the dimensions L3. It is a measure of howeasy it is to induce a moment in an atom with an electric ﬁeld. Comparing (11.5)and (11.6), our simple theory says thatα = q20mω20

= 4πe2mω20

(11.7)

.

e

If there are N atoms in a unit volume, the polarization P—the dipole moment

per unit volume—is given by

P = N p = N α0E.

Putting (11.1) and (11.8) together, we get

or, using (11.7),

κ − 1 = P0E

= N α

κ − 1 = 4πN e2mω20

.

(11.8)

(11.9)

(11.10)

From Eq. (11.10) we would predict that the dielectric constant κ of diﬀerentgases should depend on the density of the gas and on the frequency ω0 of itsoptical absorption.Our formula is, of course, only a very rough approximation, because inEq. (11.2) we have taken a model which ignores the complications of quantummechanics. For example, we have assumed that an atom has only one resonantfrequency, when it really has many. To calculate properly the polarizability α ofatoms we must use the complete quantum-mechanical theory, but the classicalideas above give us a reasonable estimate.

Let’s see if we can get the right order of magnitude for the dielectric constantof some substance. Suppose we try hydrogen. We have once estimated (Chap-ter 38, Vol. I) that the energy needed to ionize the hydrogen atom should beapproximately

E ≈ 12

me42 .

(11.11)

11-2

For an estimate of the natural frequency ω0, we can set this energy equal to ω0—the energy of an atomic oscillator whose natural frequency is ω0. We get

If we now use this value of ω0 in Eq. (11.7), we ﬁnd for the electronic polarizability

me43 .

ω0 ≈ 12(cid:20) 2

(cid:21)3

α ≈ 16π

me2

.

(11.12)

The quantity (2/me2) is the radius of the ground-state orbit of a Bohr atom (seeChapter 38, Vol. I) and equals 0.528 angstroms. In a gas at standard pressure andtemperature (1 atmosphere, 0◦C) there are 2.69 × 1019 atoms/cm3, so Eq. (11.9)gives us

κ = 1 + (2.69 × 1019)16π(0.528 × 10−8)3 = 1.00020.The dielectric constant for hydrogen gas is measured to be

(11.13)

κexp = 1.00026.

We see that our theory is about right. We should not expect any better, becausethe measurements were, of course, made with normal hydrogen gas, whichhas diatomic molecules, not single atoms. We should not be surprised if thepolarization of the atoms in a molecule is not quite the same as that of theseparate atoms. The molecular eﬀect, however, is not really that large. An exactquantum-mechanical calculation of α for hydrogen atoms gives a result about12% higher than (11.12) (the 16π is changed to 18π), and therefore predicts adielectric constant somewhat closer to the observed one. In any case, it is clearthat our model of a dielectric is fairly good.

Another check on our theory is to try Eq. (11.12) on atoms which have ahigher frequency of excitation. For instance, it takes about 24.6 electron volts topull the electron oﬀ helium, compared with the 13.6 electron volts required toionize hydrogen. We would, therefore, expect that the absorption frequency ω0for helium would be about twice as big as for hydrogen and that α would beone-quarter as large. We expect that

Experimentally,

κhelium ≈ 1.000050.κhelium = 1.000068,

so you see that our rough estimates are coming out on the right track. So wehave understood the dielectric constant of nonpolar gas, but only qualitatively,because we have not yet used a correct atomic theory of the motions of the atomicelectrons.

11-3 Polar molecules; orientation polarizationNext we will consider a molecule which carries a permanent dipole moment p0—such as a water molecule. With no electric ﬁeld, the individual dipoles pointin random directions, so the net moment per unit volume is zero. But whenan electric ﬁeld is applied, two things happen: First, there is an extra dipolemoment induced because of the forces on the electrons; this part gives just thesame kind of electronic polarizability we found for a nonpolar molecule. For veryaccurate work, this eﬀect should, of course, be included, but we will neglect itfor the moment. (It can always be added in at the end.) Second, the electricﬁeld tends to line up the individual dipoles to produce a net moment per unitvolume. If all the dipoles in a gas were to line up, there would be a very largepolarization, but that does not happen. At ordinary temperatures and electricﬁelds the collisions of the molecules in their thermal motion keep them from lining11-3

Fig. 11-2. (a) In a gas of polar molecules,the individual moments are oriented at ran-dom; the average moment in a small vol-ume is zero. (b) When there is an electricﬁeld, there is some average alignment ofthe molecules.

Fig. 11-3. The energy of a dipole p0 in

the ﬁeld E is −p0 · E.

up very much. But there is some net alignment, and so some polarization (seeFig. 11-2). The polarization that does occur can be computed by the methods ofstatistical mechanics we described in Chapter 40 of Vol. I.

To use this method we need to know the energy of a dipole in an electricﬁeld. Consider a dipole of moment p0 in an electric ﬁeld, as shown in Fig. 11-3.The energy of the positive charge is qφ(1), and the energy of the negative chargeis −qφ(2). Thus the energy of the dipole is

U = qφ(1) − qφ(2) = qd · ∇φ,

or

U = −p0 · E = −p0E cos θ,

(11.14)where θ is the angle between p0 and E. As we would expect, the energy is lowerwhen the dipoles are lined up with the ﬁeld.We now ﬁnd out how much lining up occurs by using the methods of statisticalmechanics. We found in Chapter 40 of Vol. I that in a state of thermal equilibrium,the relative number of molecules with the potential energy U is proportional to(11.15)where U(x, y, z) is the potential energy as a function of position. The samearguments would say that using Eq. (11.14) for the potential energy as a functionof angle, the number of molecules at θ per unit solid angle is proportionalto e−U/kT .Letting n(θ) be the number of molecules per unit solid angle at θ, we have(11.16)

n(θ) = n0e+p0E cos θ/kT .

e−U/kT ,

For normal temperatures and ﬁelds, the exponent is small, so we can approximateby expanding the exponential:

(cid:18)1 + p0E cos θ

(cid:19)

kT

n(θ) = n0

.

(11.17)

We can ﬁnd n0 if we integrate (11.17) over all angles; the result should bejust N, the total number of molecules per unit volume. The average value of cos θover all angles is zero, so the integral is just n0 times the total solid angle 4π.We get

.

n0 = N4π

(11.18)We see from (11.17) that there will be more molecules oriented along the ﬁeld(cos θ = 1) than against the ﬁeld (cos θ = −1). So in any small volume containingmany molecules there will be a net dipole moment per unit volume—that is, apolarization P. To calculate P, we want the vector sum of all the molecularmoments in a unit volume. Since we know that the result is going to be in thedirection of E, we will just sum the components in that direction (the componentsat right angles to E will sum to zero):

P = X

unit

volume

p0 cos θi.

We can evaluate the sum by integrating over the angular distribution. The

solid angle at θ is 2π sin θ dθ, so

P =

n(θ)p0 cos θ 2π sin θ dθ.

(11.19)

Substituting for n(θ) from (11.17), we have

P = − N2

1

1 + p0EkT

cos θ

(cid:19)

p0 cos θ d(cos θ),

11-4

Z π(cid:18)Z −1

0

which is easily integrated to give

P = N p20E3kT

.

(11.20)

The polarization is proportional to the ﬁeld E, so there will be normal dielectricbehavior. Also, as we expect, the polarization depends inversely on the temper-ature, because at higher temperatures there is more disalignment by collisions.This 1/T dependence is called Curie’s law. The permanent moment p0 appearssquared for the following reason: In a given electric ﬁeld, the aligning forcedepends upon p0, and the mean moment that is produced by the lining up isagain proportional to p0. The average induced moment is proportional to p20.We should now try to see how well Eq. (11.20) agrees with experiment. Let’slook at the case of steam. Since we don’t know what p0 is, we cannot compute Pdirectly, but Eq. (11.20) does predict that κ − 1 should vary inversely as thetemperature, and this we should check.

From (11.20) we get

= N p2030kT

,

κ − 1 = P0E

(11.21)so κ − 1 should vary in direct proportion to the density N, and inversely asthe absolute temperature. The dielectric constant has been measured at severaldiﬀerent pressures and temperatures, chosen such that the number of moleculesin a unit volume remained ﬁxed.* [Notice that if the measurements had all beentaken at constant pressure, the number of molecules per unit volume woulddecrease linearly with increasing temperature and κ − 1 would vary as T −2instead of as T −1.] In Fig. 11-4 we plot the experimental observations for κ − 1as a function of 1/T. The dependence predicted by (11.21) is followed quite well.There is another characteristic of the dielectric constant of polar molecules—its variation with the frequency of the applied ﬁeld. Due to the moment of inertiaof the molecules, it takes a certain amount of time for the heavy molecules to turntoward the direction of the ﬁeld. So if we apply frequencies in the high microwaveregion or above, the polar contribution to the dielectric constant begins to fallaway because the molecules cannot follow. In contrast to this, the electronicpolarizability still remains the same up to optical frequencies, because of thesmaller inertia in the electrons.

11-4 Electric ﬁelds in cavities of a dielectricWe now turn to an interesting but complicated question—the problem of thedielectric constant in dense materials. Suppose that we take liquid helium or liquidargon or some other nonpolar material. We still expect electronic polarization.But in a dense material, P can be large, so the ﬁeld on an individual atom willbe inﬂuenced by the polarization of the atoms in its close neighborhood. Thequestion is, what electric ﬁeld acts on the individual atom?

Imagine that the liquid is put between the plates of a condenser.

If theplates are charged they will produce an electric ﬁeld in the liquid. But there arealso charges in the individual atoms, and the total ﬁeld E is the sum of bothof these eﬀects. This true electric ﬁeld varies very, very rapidly from point topoint in the liquid. It is very high inside the atoms—particularly right next tothe nucleus—and relatively small between the atoms. The potential diﬀerencebetween the plates is the line integral of this total ﬁeld. If we ignore all theﬁne-grained variations, we can think of an average electric ﬁeld E, which isjust V /d. (This is the ﬁeld we were using in the last chapter.) We should thinkof this ﬁeld as the average over a space containing many atoms.Now you might think that an「average」atom in an「average」location wouldfeel this average ﬁeld. But it is not that simple, as we can show by consideringwhat happens if we imagine diﬀerent-shaped holes in a dielectric. For instance,suppose that we cut a slot in a polarized dielectric, with the slot oriented parallel

* Sänger, Steiger, and Gächter, Helvetica Physica Acta 5, 200 (1932).

11-5

Fig. 11-4. Experimental measurementsof the dielectric constant of water vapor atvarious temperatures.

Fig. 11-5. The ﬁeld in a slot cut in adielectric depends on the shape and orienta-tion of the slot.

to the ﬁeld, as shown in part (a) of Fig. 11-5. Since we know that ∇ × E = 0,the line integral of E around the curve, Γ, which goes as shown in (b) of theﬁgure, should be zero. The ﬁeld inside the slot must give a contribution whichjust cancels the part from the ﬁeld outside. Therefore the ﬁeld E0 actually foundin the center of a long thin slot is equal to E, the average electric ﬁeld found inthe dielectric.

Now consider another slot whose large sides are perpendicular to E, as shownin part (c) of Fig. 11-5. In this case, the ﬁeld E0 in the slot is not the same as Ebecause polarization charges appear on the surfaces. If we apply Gauss’ law to asurface S drawn as in (d) of the ﬁgure, we ﬁnd that the ﬁeld E0 in the slot isgiven by

E0 = E + P0

,

(11.22)

where E is again the electric ﬁeld in the dielectric.(The gaussian surfacecontains the surface polarization charge σpol = P.) We mentioned in Chapter 10that 0E + P is often called D, so 0E0 = D0 is equal to D in the dielectric.Earlier in the history of physics, when it was supposed to be very importantto deﬁne every quantity by direct experiment, people were delighted to discoverthat they could deﬁne what they meant by E and D in a dielectric withouthaving to crawl around between the atoms. The average ﬁeld E is numericallyequal to the ﬁeld E0 that would be measured in a slot cut parallel to the ﬁeld.And the ﬁeld D could be measured by ﬁnding E0 in a slot cut normal to theﬁeld. But nobody ever measures them that way anyway, so it was just one ofthose philosophical things.

Fig. 11-6. The ﬁeld at any point A in adielectric can be considered as the sum ofthe ﬁeld in a spherical hole plus the ﬁeld dueto a spherical plug.

For most liquids which are not too complicated in structure, we could expectthat an atom ﬁnds itself, on the average, surrounded by the other atoms in whatwould be a good approximation to a spherical hole. And so we should ask:「Whatwould be the ﬁeld in a spherical hole?」We can ﬁnd out by noticing that if weimagine carving out a spherical hole in a uniformly polarized material, we are justremoving a sphere of polarized material. (We must imagine that the polarizationis「frozen in」before we cut out the hole.) By superposition, however, the ﬁeldsinside the dielectric, before the sphere was removed, is the sum of the ﬁelds fromall charges outside the spherical volume plus the ﬁelds from the charges withinthe polarized sphere. That is, if we call E the ﬁeld in the uniform dielectric, wecan write

E = Ehole + Eplug,

(11.23)where Ehole is the ﬁeld in the hole and Eplug is the ﬁeld inside a sphere whichis uniformly polarized (see Fig. 11-6). The ﬁelds due to a uniformly polarizedsphere are shown in Fig. 11-7. The electric ﬁeld inside the sphere is uniform, andits value is

Using (11.23), we get

Eplug = − P30

.

Ehole = E + P30

.

(11.24)

(11.25)

The ﬁeld in a spherical cavity is greater than the average ﬁeld by the amount P/30.(The spherical hole gives a ﬁeld 1/3 of the way between a slot parallel to the ﬁeldand a slot perpendicular to the ﬁeld.)

Fig. 11-7. The electric ﬁeld of a uniformly

polarized sphere.

11-6

11-5 The dielectric constant of liquids; the Clausius-Mossotti equationIn a liquid we expect that the ﬁeld which will polarize an individual atomis more like Ehole than just E. If we use the Ehole of (11.25) for the polarizingﬁeld in Eq. (11.6), then Eq. (11.8) becomes

(cid:18)

(cid:19)

,

or

P = N α0

E + P30

P =

N α

1 − (N α/3) 0E.

Remembering that κ − 1 is just P/0E, we have

κ − 1 =

N α

1 − (N α/3) ,

(11.26)

(11.27)

(11.28)

κ − 1 = N α.

which gives us the dielectric constant of a liquid in terms of α, the atomicpolarizability. This is called the Clausius-Mossotti equation.Whenever N α is very small, as it is for a gas (because the density N is small),then the term N α/3 can be neglected compared with 1, and we get our old result,Eq. (11.9), that(11.29)Let’s compare Eq. (11.28) with some experimental results. It is ﬁrst necessaryto look at gases for which, using the measurement of κ, we can ﬁnd α fromEq. (11.29). For instance, for carbon disulﬁde at zero degrees centigrade thedielectric constant is 1.0029, so N α is 0.0029. Now the density of the gas is easilyworked out and the density of the liquid can be found in handbooks. At 20◦C, thedensity of liquid CS2 is 381 times higher than the density of the gas at 0◦C. Thismeans that N is 381 times higher in the liquid than it is in the gas so, that—ifwe make the approximation that the basic atomic polarizability of the carbondisulﬁde doesn’t change when it is condensed into a liquid—N α in the liquidis equal to 381 times 0.0029, or 1.11. Notice that the N α/3 term amounts toalmost 0.4, so it is quite signiﬁcant. With these numbers we predict a dielectricconstant of 2.76, which agrees reasonably well with the observed value of 2.64.In Table 11-1 we give some experimental data on various materials (taken fromthe Handbook of Chemistry and Physics), together with the dielectric constantscalculated from Eq. (11.28) in the way just described. The agreement betweenobservation and theory is even better for argon and oxygen than for CS2—and notso good for carbon tetrachloride. On the whole, the results show that Eq. (11.28)works very well.

Table 11-1

Computation of the dielectric constants of liquids

from the dielectric constant of the gas.

Substance

CS2O2CCl4Ar

κ (exp)1.00291.0005231.00301.000545

Gas

N α0.00290.0005230.00300.000545

Liquid

Density Density Ratio1 N α0.003391.110.001430.4350.9770.004890.001780.441

1.2931.191.591.44

381832325810

κ (predict)

2.761.5092.451.517

κ (exp)2.641.5072.241.54

1 Ratio = density of liquid/density of gas.

Our derivation of Eq. (11.28) is valid only for electronic polarization in liquids.It is not right for a polar molecule like H2O. If we go through the same calculationsfor water, we get 13.2 for N α, which means that the dielectric constant for theliquid is negative, while the observed value of κ is 80. The problem has to do11-7

with the correct treatment of the permanent dipoles, and Onsager has pointedout the right way to go. We do not have the time to treat the case now, butif you are interested it is discussed in Kittel’s book, Introduction to Solid StatePhysics.

11-6 Solid dielectricsNow we turn to the solids. The ﬁrst interesting fact about solids is that therecan be a permanent polarization built in—which exists even without applying anelectric ﬁeld. An example occurs with a material like wax, which contains longmolecules having a permanent dipole moment. If you melt some wax and put astrong electric ﬁeld on it when it is a liquid, so that the dipole moments get partlylined up, they will stay that way when the liquid freezes. The solid material willhave a permanent polarization which remains when the ﬁeld is removed. Such asolid is called an electret.It is theelectrical analog of a magnet. It is not as useful, though, because free chargesfrom the air are attracted to its surfaces, eventually cancelling the polarizationcharges. The electret is「discharged」and there are no visible external ﬁelds.

An electret has permanent polarization charges on its surface.

A permanent internal polarization P is also found occurring naturally insome crystalline substances. In such crystals, each unit cell of the lattice has anidentical permanent dipole moment, as drawn in Fig. 11-8. All the dipoles pointin the same direction, even with no applied electric ﬁeld. Many complicatedcrystals have, in fact, such a polarization; we do not normally notice it becausethe external ﬁelds are discharged, just as for the electrets.

If these internal dipole moments of a crystal are changed, however, externalﬁelds appear because there is not time for stray charges to gather and cancelthe polarization charges. If the dielectric is in a condenser, free charges will beinduced on the electrodes. For example, the moments can change when a dielectricis heated, because of thermal expansion. The eﬀect is called pyroelectricity.Similarly, if we change the stresses in a crystal—for instance, if we bend it—again the moment may change a little bit, and a small electrical eﬀect, calledpiezoelectricity, can be detected.For crystals that do not have a permanent moment, one can work out atheory of the dielectric constant that involves the electronic polarizability of theatoms. It goes much the same as for liquids. Some crystals also have rotatabledipoles inside, and the rotation of these dipoles will also contribute to κ. In ioniccrystals such as NaCl there is also ionic polarizability. The crystal consists of acheckerboard of positive and negative ions, and in an electric ﬁeld the positiveions are pulled one way and the negatives the other; there is a net relative motionof the plus and minus charges, and so a volume polarization. We could estimatethe magnitude of the ionic polarizability from our knowledge of the stiﬀness ofsalt crystals, but we will not go into that subject here.

Fig. 11-8. A complex crystal lattice canhave a permanent intrinsic polarization P .

11-7 Ferroelectricity; BaTiO3We want to describe now one special class of crystals which have, just byaccident almost, a built-in permanent moment. The situation is so marginalthat if we increase the temperature a little bit they lose the permanent momentcompletely. On the other hand, if they are nearly cubic crystals, so that theirmoments can be turned in diﬀerent directions, we can detect a large change inthe moment when an applied electric ﬁeld is changed. All the moments ﬂip overand we get a large eﬀect. Substances which have this kind of permanent momentare called ferroelectric, after the corresponding ferromagnetic eﬀects which wereﬁrst discovered in iron.We would like to explain how ferroelectricity works by describing a partic-ular example of a ferroelectric material. There are several ways in which theferroelectric property can originate; but we will take up only one mysteriouscase—that of barium titanate, BaTiO3. This material has a crystal lattice whose11-8

Fig. 11-9. The unit cell of BaTiO3. Theatoms really ﬁll up most of the space; forclarity, only the positions of their centersare shown.

basic cell is sketched in Fig. 11-9. It turns out that above a certain temperature,speciﬁcally 118◦C, barium titanate is an ordinary dielectric with an enormousdielectric constant. Below this temperature, however, it suddenly takes on apermanent moment.

In working out the polarization of solid material, we must ﬁrst ﬁnd what arethe local ﬁelds in each unit cell. We must include the ﬁelds from the polarizationitself, just as we did for the case of a liquid. But a crystal is not a homogeneousliquid, so we cannot use for the local ﬁeld what we would get in a sphericalhole. If you work it out for a crystal, you ﬁnd that the factor 1/3 in Eq. (11.24)becomes slightly diﬀerent, but not far from 1/3. (For a simple cubic crystal, itis just 1/3.) We will, therefore, assume for our preliminary discussion that thefactor is 1/3 for BaTiO3.Now when we wrote Eq. (11.28) you may have wondered what would happenif N α became greater than 3. It appears as though κ would become negative. Butthat surely cannot be right. Let’s see what should happen if we were graduallyto increase α in a particular crystal. As α gets larger, the polarization getsbigger, making a bigger local ﬁeld. But a bigger local ﬁeld will polarize eachatom more, raising the local ﬁelds still more. If the「give」of the atoms is enough,the process keeps going; there is a kind of feedback that causes the polarizationto increase without limit—assuming that the polarization of each atom increasesin proportion to the ﬁeld. The「runaway」condition occurs when N α = 3. Thepolarization does not become inﬁnite, of course, because the proportionalitybetween the induced moment and the electric ﬁeld breaks down at high ﬁelds, sothat our formulas are no longer correct. What happens is that the lattice gets「locked in」with a high, self-generated, internal polarization.

In the case of BaTiO3, there is, in addition to an electronic polarization, alsoa rather large ionic polarization, presumed to be due to titanium ions which canmove a little within the cubic lattice. The lattice resists large motions, so afterthe titanium has gone a little way, it jams up and stops. But the crystal cell isthen left with a permanent dipole moment.

In most crystals, this is really the situation for all temperatures that can bereached. The very interesting thing about barium titanate is that there is sucha delicate condition that if N α is decreased just a little bit it comes unstuck.Since N decreases with increasing temperature—because of thermal expansion—we can vary N α by varying the temperature. Below the critical temperatureit is just barely stuck, so it is easy—by applying an external ﬁeld—to shift thepolarization and have it lock in a diﬀerent direction.

Let’s see if we can analyze what happens in more detail. We call Tc thecritical temperature at which N α is exactly 3. As the temperature increases, Ngoes down a little bit because of the expansion of the lattice. Since the expansionis small, we can say that near the critical temperature

N α = 3 − β(T − Tc),

(11.30)

where β is a small constant, of the same order of magnitude as the thermalexpansion coeﬃcient, or about 10−5 to 10−6 per degree C. Now if we substitutethis relation into Eq. (11.28), we get that

κ − 1 = 3 − β(T − Tc)β(T − Tc)/3 .

Since we have assumed that β(T − Tc) is small compared with one, we canapproximate this formula by

κ − 1 =

9

β(T − Tc) .

(11.31)

This relation is right, of course, only for T > Tc. We see that just abovethe critical temperature κ is enormous. Because N α is so close to 3, thereis a tremendous magniﬁcation eﬀect, and the dielectric constant can easily be11-9

as high as 50,000 to 100,000.It is also very sensitive to temperature. Forincreases in temperature, the dielectric constant goes down inversely as thetemperature, but, unlike the case of a dipolar gas, for which κ − 1 goes inverselyas the absolute temperature, for ferroelectrics it varies inversely as the diﬀerencebetween the absolute temperature and the critical temperature (this law is calledthe Curie-Weiss law).

When we lower the temperature to the critical temperature, what happens?If we imagine a lattice of unit cells like that in Fig. 11-9, we see that it is possibleto pick out chains of ions along vertical lines. One of them consists of alternatingoxygen and titanium ions. There are other lines made up of either barium oroxygen ions, but the spacing along these lines is greater. We make a simplemodel to imitate this situation by imagining, as shown in Fig. 11-10(a), a seriesof chains of ions. Along what we call the main chain, the separation of the ionsis a, which is half the lattice constant; the lateral distance between identicalchains is 2a. There are less-dense chains in between which we will ignore for themoment. To make the analysis a little easier, we will also suppose that all theions on the main chain are identical. (It is not a serious simpliﬁcation becauseall the important eﬀects will still appear. This is one of the tricks of theoreticalphysics. One does a diﬀerent problem because it is easier to ﬁgure out the ﬁrsttime—then when one understands how the thing works, it is time to put in allthe complications.)

Now let’s try to ﬁnd out what would happen with our model. We supposethat the dipole moment of each atom is p and we wish to calculate the ﬁeld atone of the atoms of the chain. We must ﬁnd the sum of the ﬁelds from all theother atoms. We will ﬁrst calculate the ﬁeld from the dipoles in only one verticalchain; we will talk about the other chains later. The ﬁeld at the distance r froma dipole in a direction along its axis is given by2pr3 .

E = 14π0

(11.32)

At any given atom, the dipoles at equal distances above and below it give ﬁeldsin the same direction, so for the whole chain we get64 + ···

(cid:18)2 + 2

27 + 2

8 + 2

Echain = p4π0

= p0

2a3 ·

(cid:19)

0.383a3

.

(11.33)

It is not too hard to show that if our model were like a completely cubic crystal—that is, if the next identical lines were only the distance a away—the number 0.383would be changed to 1/3. In other words, if the next lines were at the distance athey would contribute only −0.050 unit to our sum. However, the next main chainwe are considering is at the distance 2a and, as you remember from Chapter 7,the ﬁeld from a periodic structure dies oﬀ exponentially with distance. Thereforethese lines contribute much less than −0.050 and we can just ignore all the otherchains.It is necessary now to ﬁnd out what polarizability α is needed to make therunaway process work. Suppose that the induced moment p of each atom of thechain is proportional to the ﬁeld on it, as in Eq. (11.6). We get the polarizingﬁeld on the atom from Echain using Eq. (11.32). So we have the two equations

and

p = α0EchainEchain = 0.383a3

p0

.

There are two solutions: Echain and p both zero, or

α = a3

0.383 ,

with Echain and p both ﬁnite. Thus if α is as large as a3/0.383, a permanentpolarization sustained by its own ﬁeld will set in. This critical equality must be11-10

Fig. 11-10. Models of a ferroelectric:(a) corresponds to an antiferroelectric, and(b) to a normal ferroelectric.

reached for barium titanate at just the temperature Tc. (Notice that if α werelarger than the critical value for small ﬁelds, it would decrease at larger ﬁeldsand at equilibrium the same equality we have found would hold.)For BaTiO3, the spacing a is 2 × 10−8 cm, so we must expect that α =21.8 × 10−24 cm3. We can compare this with the known polarizabilities of theindividual atoms. For oxygen, α = 30.2 × 10−24 cm3; we’re on the right track!But for titanium, α = 2.4× 10−24 cm3; rather small. To use our model we shouldprobably take the average. (We could work out the chain again for alternatingatoms, but the result would be about the same.) So α(average) = 16.3×10−24 cm3,which is not high enough to give a permanent polarization.But wait a moment! We have so far only added up the electronic polarizabilities.There is also some ionic polarization due to the motion of the titanium ion. Allwe need is an ionic polarizability of 9.2×10−24 cm3. (A more precise computationusing alternating atoms shows that actually 11.9 × 10−24 cm3 is needed.) Tounderstand the properties of BaTiO3, we have to assume that such an ionicpolarizability exists.Why the titanium ion in barium titanate should have that much ionic polariz-ability is not known. Furthermore, why, at a lower temperature, it polarizes alongthe cube diagonal and the face diagonal equally well is not clear. If we ﬁgureout the actual size of the spheres in Fig. 11-9, and ask whether the titanium is alittle bit loose in the box formed by its neighboring oxygen atoms—which is whatyou would hope, so that it could be easily shifted—you ﬁnd quite the contrary.It ﬁts very tightly. The barium atoms are slightly loose, but if you let them bethe ones that move, it doesn’t work out. So you see that the subject is really notone-hundred percent clear; there are still mysteries we would like to understand.Returning to our simple model of Fig. 11-10(a), we see that the ﬁeld from onechain would tend to polarize the neighboring chain in the opposite direction, whichmeans that although each chain would be locked, there would be no net permanentmoment per unit volume! (Although there would be no external electric eﬀects,there are still certain thermodynamic eﬀects one could observe.) Such systemsexist, and are called antiferroelectric. So what we have explained is really anantiferroelectric. Barium titanate, however, is really like the arrangement inFig. 11-10(b). The oxygen-titanium chains are all polarized in the same directionbecause there are intermediate chains of atoms in between. Although the atomsin these chains are not very polarizable, or very dense, they will be somewhatpolarized, in the direction antiparallel to the oxygen-titanium chains. The smallﬁelds produced at the next oxygen-titanium chain will get it started parallel tothe ﬁrst. So BaTiO3 is really ferroelectric, and it is because of the atoms inbetween. You may be wondering:「But what about the direct eﬀect between thetwo O-Ti chains?」Remember, though, the direct eﬀect dies oﬀ exponentiallywith the separation; the eﬀect of the chain of strong dipoles at 2a can be lessthan the eﬀect of a chain of weak ones at the distance a.This completes our rather detailed report on our present understanding ofthe dielectric constants of gases, of liquids, and of solids.

11-11
