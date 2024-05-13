# 0801

8-1 The electrostatic energy of charges. A uniform sphereIn

the study of mechanics, one of the most interesting and useful discoverieswas the law of the conservation of energy. The expressions for the kinetic andpotential energies of a mechanical system helped us to discover connectionsbetween the states of a system at two diﬀerent times without having to look intothe details of what was occurring in between. We wish now to consider the energyof electrostatic systems. In electricity also the principle of the conservation ofenergy will be useful for discovering a number of interesting things.

The law of the energy of interaction in electrostatics is very simple; we have,in fact, already discussed it. Suppose we have two charges q1 and q2 separated bythe distance r12. There is some energy in the system, because a certain amountof work was required to bring the charges together. We have already calculatedthe work done in bringing two charges together from a large distance. It is

8-1 The electrostatic energy ofcharges. A uniform sphere

8-2 The energy of a condenser. Forces

on charged conductors

8-3 The electrostatic energy of an

ionic crystal

8-4 Electrostatic energy in nuclei8-5 Energy in the electrostatic ﬁeld8-6 The energy of a point charge

q1q24π0r12

.

(8.1)

We also know, from the principle of superposition, that if we have many chargespresent, the total force on any charge is the sum of the forces from the others. Itfollows, therefore, that the total energy of a system of a number of charges is thesum of terms due to the mutual interaction of each pair of charges. If qi and qjare any two of the charges and rij is the distance between them (Fig. 8-1), theenergy of that particular pair is

Review: Chapter 4, Vol. I, Conserva-tion of EnergyChapters 13 and 14, Vol. I,Work and Potential Energy

qiqj4π0rij

.

(8.2)

The total electrostatic energy U is the sum of the energies of all possible pairs ofcharges:

qiqj4π0rij

.

(8.3)

U = X

all pairs

If we have a distribution of charge speciﬁed by a charge density ρ, the sum ofEq. (8.3) is, of course, to be replaced by an integral.

We shall concern ourselves with two aspects of this energy. One is theapplication of the concept of energy to electrostatic problems; the other is theevaluation of the energy in diﬀerent ways. Sometimes it is easier to compute thework done for some special case than to evaluate the sum in Eq. (8.3), or thecorresponding integral. As an example, let us calculate the energy required toassemble a sphere of charge with a uniform charge density. The energy is justthe work done in gathering the charges together from inﬁnity.

Imagine that we assemble the sphere by building up a succession of thinspherical layers of inﬁnitesimal thickness. At each stage of the process, we gathera small amount of charge and put it in a thin layer from r to r + dr. We continuethe process until we arrive at the ﬁnal radius a (Fig. 8-2). If Qr is the charge ofthe sphere when it has been built up to the radius r, the work done in bringinga charge dQ to it is

dU = Qr dQ4π0r

.

(8.4)

8-1

Fig. 8-1. The electrostatic energy of asystem of particles is the sum of the elec-trostatic energy of each pair.

Fig. 8-2. The energy of a uniform sphereof charge can be computed by imaginingthat it is assembled from successive sphericalshells.

If the density of charge in the sphere is ρ, the charge Qr is

and the charge dQ is

Equation (8.4) becomes

Qr = ρ · 4

3 πr3,

dQ = ρ · 4πr2 dr.

dU = 4πρ2r4 dr

30

.

(8.5)

The total energy required to assemble the sphere is the integral of dU from r = 0to r = a, or

(8.6)Or if we wish to express the result in terms of the total charge Q of the sphere,

.

U = 4πρ2a5150

U = 35

Q24π0a

.

(8.7)

The energy is proportional to the square of the total charge and inversely propor-tional to the radius. We can also interpret Eq. (8.7) as saying that the averageof (1/rij) for all pairs of points in the sphere is 6/5a.

8-2 The energy of a condenser. Forces on charged conductorsWe consider now the energy required to charge a condenser. If the charge Qhas been taken from one of the conductors of a condenser and placed on theother, the potential diﬀerence between them is

V = QC

,

(8.8)

where C is the capacity of the condenser. How much work is done in chargingthe condenser? Proceeding as for the sphere, we imagine that the condenserhas been charged by transferring charge from one plate to the other in smallincrements dQ. The work required to transfer the charge dQ is

Taking V from Eq. (8.8), we write

dU = V dQ.

Or integrating from zero charge to the ﬁnal charge Q, we have

dU = Q dQC

.

U = 12

Q2C

.

This energy can also be written as

U = 1

2 CV 2.

Recalling that the capacity of a conducting sphere (relative to inﬁnity) is

we can immediately get from Eq. (8.9) the energy of a charged sphere,

Csphere = 4π0a,

U = 12

Q24π0a

.

(8.9)

(8.10)

(8.11)

This, of course, is also the energy of a thin spherical shell of total charge Q andis just 5/6 of the energy of a uniformly charged sphere, Eq. (8.7).

8-2

We now consider applications of the idea of electrostatic energy. Considerthe following questions: What is the force between the plates of a condenser?Or what is the torque about some axis of a charged conductor in the presenceof another with opposite charge? Such questions are easily answered by usingour result Eq. (8.9) for electrostatic energy of a condenser, together with theprinciple of virtual work (Chapters 4, 13, and 14 of Vol. I).

Let’s use this method for determining the force between the plates of aparallel-plate condenser. If we imagine that the spacing of the plates is increasedby the small amount ∆z, then the mechanical work done from the outside inmoving the plates would be

(8.12)where F is the force between the plates. This work must be equal to the changein the electrostatic energy of the condenser.

∆W = F ∆z,

By Eq. (8.9), the energy of the condenser was originally

U = 12

Q2C

.

The change in energy (if we do not let the charge change) is

Equating (8.12) and (8.13), we have

This can also be written as

(cid:18) 12 Q2 ∆(cid:18) 12 ∆

C

C

(cid:19)

.

.

(cid:19)

∆U = 1

F ∆z = Q2

F ∆z = − Q22C2

∆C.

(8.13)

(8.14)

(8.15)

The force, of course, results from the attraction of the charges on the plates, butwe see that we do not have to worry in detail about how they are distributed;everything we need is taken care of in the capacity C.

It is easy to see how the idea is extended to conductors of any shape, and forother components of the force. In Eq. (8.14), we replace F by the component weare looking for, and we replace ∆z by a small displacement in the correspondingdirection. Or if we have an electrode with a pivot and we want to know thetorque τ, we write the virtual work as

∆W = τ ∆θ,

where ∆θ is a small angular displacement. Of course, ∆(1/C) must be the changein 1/C which corresponds to ∆θ. We could, in this way, ﬁnd the torque on themovable plates in a variable condenser of the type shown in Fig. 8-3.

Returning to the special case of a parallel-plate condenser, we can use the

formula we derived in Chapter 6 for the capacity:

where A is the area of each plate. If we increase the separation by ∆z,

1C

= d0A

,

(cid:18) 1

(cid:19)

C

∆

= ∆z0A

.

From Eq. (8.14) we get that the force between the plates is

F = Q220A

.

Fig. 8-3. What is the torque on a variable

capacitor?

(8.16)

(8.17)

8-3

Let’s look at Eq. (8.17) a little more closely and see if we can tell how the

force arises. If for the charge on one plate we write

Eq. (8.17) can be rewritten as

Q = σA,

F = 12 Q

σ0

.

Or, since the electric ﬁeld between the plates is

E0 = σ0

,

F = 1

2 QE0.

then

(8.18)One would immediately guess that the force acting on one plate is the charge Qon the plate times the ﬁeld acting on the charge. But we have a surprising factorof one-half. The reason is that E0 is not the ﬁeld at the charges. If we imaginethat the charge at the surface of the plate occupies a thin layer, as indicated inFig. 8-4, the ﬁeld will vary from zero at the inner boundary of the layer to E0 inthe space outside of the plate. The average ﬁeld acting on the surface chargesis E0/2. That is why the factor one-half is in Eq. (8.18).You should notice that in computing the virtual work we have assumed thatthe charge on the condenser was constant—that it was not electrically connectedto other objects, and so the total charge could not change.

Suppose we had imagined that the condenser was held at a constant potential

diﬀerence as we made the virtual displacement. Then we should have taken

Fig. 8-4. The ﬁeld at the surface of aconductor varies from zero to E0 = σ/0,as one passes through the layer of surfacecharge.

2 CV 2and in place of Eq. (8.15) we would have had

U = 1

F∆z = 1

2 V 2 ∆C,

which gives a force equal in magnitude to the one in Eq. (8.15) (because V = Q/C),but with the opposite sign! Surely the force between the condenser plates doesn’treverse in sign as we disconnect it from its charging source. Also, we knowthat two plates with opposite electrical charges must attract. The principle ofvirtual work has been incorrectly applied in the second case—we have not takeninto account the virtual work done on the charging source. That is, to keepthe potential constant at V as the capacity changes, a charge V ∆C must besupplied by a source of charge. But this charge is supplied at a potential V , sothe work done by the electrical system which keeps the potential constant isV 2 ∆C. The mechanical work F ∆z plus this electrical work V 2 ∆C togethermake up the change in the total energy 12 V 2 ∆C of the condenser. ThereforeF ∆z is − 1

2 V 2 ∆C, as before.

8-3 The electrostatic energy of an ionic crystalWe now consider an application of the concept of electrostatic energy inatomic physics. We cannot easily measure the forces between atoms, but we areoften interested in the energy diﬀerences between one atomic arrangement andanother, as, for example, the energy of a chemical change. Since atomic forces arebasically electrical, chemical energies are in large part just electrostatic energies.Let’s consider, for example, the electrostatic energy of an ionic lattice. Anionic crystal like NaCl consists of positive and negative ions which can be thoughtof as rigid spheres. They attract electrically until they begin to touch; then there isa repulsive force which goes up very rapidly if we try to push them closer together.For our ﬁrst approximation, therefore, we imagine a set of rigid spheres thatrepresent the atoms in a salt crystal. The structure of the lattice has beendetermined by x-ray diﬀraction. It is a cubic lattice—like a three-dimensional8-4

Fig. 8-5. Cross section of a salt crystalon an atomic scale. The checkerboard ar-rangement of Na and Cl ions is the same inthe two cross sections perpendicular to theone shown. (See Vol. I, Fig. 1-7.)

checkerboard. Figure 8-5 shows a cross-sectional view. The spacing of the ions is2.81 Å (= 2.81 × 10−8 cm).If our picture of this system is correct, we should be able to check it byasking the following question: How much energy will it take to pull all theseions apart—that is, to separate the crystal completely into ions? This energyshould be equal to the heat of vaporization of NaCl plus the energy required todissociate the molecules into ions. This total energy to separate NaCl to ionsis determined experimentally to be 7.92 electron volts per molecule. Using theconversion

1 eV = 1.602 × 10−19 joule,

and Avogadro’s number for the number of molecules in a mole,

the energy of dissociation can also be given as

N0 = 6.02 × 1023,

W = 7.64 × 105 joules/mole.

Physical chemists prefer for an energy unit the kilocalorie, which is 4190 joules;so that 1 eV per molecule is 23 kilocalories per mole. A chemist would then saythat the dissociation energy of NaCl is

W = 183 kcal/mole.

Can we obtain this chemical energy theoretically by computing how muchwork it would take to pull apart the crystal? According to our theory, this work isthe sum of the potential energies of all the pairs of ions. The easiest way to ﬁgureout this sum is to pick out a particular ion and compute its potential energy witheach of the other ions. That will give us twice the energy per ion, because theenergy belongs to the pairs of charges. If we want the energy to be associatedwith one particular ion, we should take half the sum. But we really want theenergy per molecule, which contains two ions, so that the sum we compute willgive directly the energy per molecule.The energy of an ion with one of its nearest neighbors is e2/a, where e2 =e /4π0 and a is the center-to-center spacing between ions. (We are consideringq2monovalent ions.) This energy is 5.12 eV, which we already see is going to giveus a result of the correct order of magnitude. But it is still a long way from theinﬁnite sum of terms we need.

Let’s begin by summing all the terms from the ions along a straight line.Considering that the ion marked Na in Fig. 8-5 is our special ion, we shall considerﬁrst those ions on a horizontal line with it. There are two nearest Cl ions withnegative charges, each at the distance a. Then there are two positive ions at thedistance 2a, etc. Calling the energy of this sum U1, we write

U1 = e2

(cid:18)1 + 2−2(cid:18)= −2e21 − 1

a

a

2 − 22 + 1

3 + 23 − 1

4 ∓ ···4 ± ···

(cid:19)(cid:19)

.

(8.19)

The series converges slowly, so it is diﬃcult to evaluate numerically, but it isknown to be equal to ln 2. So

U1 = −2e2

ln 2 = −1.386 e2

.

(8.20)Now consider the next adjacent line of ions above. The nearest is negativeand at the distance a. Then there are two positives at the distance √2 a. Thenext pair are at the distance √5 a, the next at √10 a, and so on. So for the wholeline we get the series

a

a

(cid:18)

e2a

−11 + 2√2 − 2√5

+ 2√10 ∓ ···

(cid:19)

.

(8.21)

8-5

There are four such lines: above, below, in front, and in back. Then there arethe four lines which are the nearest lines on diagonals, and on and on.If you work patiently through for all the lines, and then take the sum, you

ﬁnd that the grand total is

U = −1.747 e2

,

a

which is just somewhat more than what we obtained in (8.20) for the ﬁrst line.Using e2/a = 5.12 eV, we get

U = −8.94 eV.

Our answer is about 10% above the experimentally observed energy. It showsthat our idea that the whole lattice is held together by electrical Coulomb forcesis fundamentally correct. This is the ﬁrst time that we have obtained a speciﬁcproperty of a macroscopic substance from a knowledge of atomic physics. Wewill do much more later. The subject that tries to understand the behavior ofbulk matter in terms of the laws of atomic behavior is called solid-state physics.Now what about the error in our calculation? Why is it not exactly right?It is because of the repulsion between the ions at close distances. They are notperfectly rigid spheres, so when they are close together they are partly squashed.They are not very soft, so they squash only a little bit. Some energy, however,is used in deforming them, and when the ions are pulled apart this energy isreleased. The actual energy needed to pull the ions apart is a little less than theenergy that we calculated; the repulsion helps in overcoming the electrostaticattraction.

Is there any way we can make an allowance for this contribution? We couldif we knew the law of the repulsive force. We are not ready to analyze thedetails of this repulsive mechanism, but we can get some idea of its characteristicsfrom some large-scale measurements. From a measurement of the compressibilityof the whole crystal, it is possible to obtain a quantitative idea of the law ofrepulsion between the ions and therefore of its contribution to the energy. In thisway it has been found that this contribution must be 1/9.4 of the contributionfrom the electrostatic attraction and, of course, of opposite sign. If we subtractthis contribution from the pure electrostatic energy, we obtain 7.99 eV for thedissociation energy per molecule. It is much closer to the observed result of7.92 eV, but still not in perfect agreement. There is one more thing we haven’ttaken into account: we have made no allowance for the kinetic energy of thecrystal vibrations. If a correction is made for this eﬀect, very good agreementwith the experimental number is obtained. The ideas are then correct; the majorcontribution to the energy of a crystal like NaCl is electrostatic.

8-4 Electrostatic energy in nucleiWe will now take up another example of electrostatic energy in atomic physics,the electrical energy of atomic nuclei. Before we do this we will have to discusssome properties of the main forces (called nuclear forces) that hold the protonsand neutrons together in a nucleus. In the early days of the discovery of nuclei—and of the neutrons and protons that make them up—it was hoped that the lawof the strong, nonelectrical part of the force between, say, a proton and anotherproton would have some simple law, like the inverse square law of electricity. Foronce one had determined this law of force, and the corresponding ones betweena proton and a neutron, and a neutron and a neutron, it would be possible todescribe theoretically the complete behavior of these particles in nuclei. Thereforea big program was started for the study of the scattering of protons, in the hopeof ﬁnding the law of force between them; but after thirty years of eﬀort, nothingsimple has emerged. A considerable knowledge of the force between proton andproton has been accumulated, but we ﬁnd that the force is as complicated as itcan possibly be.

What we mean by「as complicated as it can be」is that the force depends on

as many things as it possibly can.

8-6

First, the force is not a simple function of the distance between the twoprotons. At large distances there is an attraction, but at closer distances there isa repulsion. The distance dependence is a complicated function, still imperfectlyknown.

Second, the force depends on the orientation of the protons’ spin. The protonshave a spin, and any two interacting protons may be spinning with their angularmomenta in the same direction or in opposite directions. And the force is diﬀerentwhen the spins are parallel from what it is when they are antiparallel, as in (a)and (b) of Fig. 8-6. The diﬀerence is quite large; it is not a small eﬀect.

Third, the force is considerably diﬀerent when the separation of the twoprotons is in the direction parallel to their spins, as in (c) and (d) of Fig. 8-6,than it is when the separation is in a direction perpendicular to the spins, as in(a) and (b).Fourth, the force depends, as it does in magnetism, on the velocity of theprotons, only much more strongly than in magnetism. And this velocity-dependentforce is not a relativistic eﬀect; it is strong even at speeds much less than thespeed of light. Furthermore, this part of the force depends on other things besidesthe magnitude of the velocity. For instance, when a proton is moving near anotherproton, the force is diﬀerent when the orbital motion has the same direction ofrotation as the spin, as in (e) of Fig. 8-6, than when it has the opposite directionof rotation, as in (f). This is called the「spin orbit」part of the force.

The force between a proton and a neutron and between a neutron and aneutron are also equally complicated. To this day we do not know the machinerybehind these forces—that is to say, any simple way of understanding them.

There is, however, one important way in which the nucleon forces are simplerthan they could be. That is that the nuclear force between two neutrons is thesame as the force between a proton and a neutron, which is the same as theforce between two protons! If, in any nuclear situation, we replace a protonby a neutron (or vice versa), the nuclear interactions are not changed. The「fundamental reason」for this equality is not known, but it is an example of animportant principle that can be extended also to the interaction laws of otherstrongly interacting particles—such as the π-mesons and the「strange」particles.This fact is nicely illustrated by the locations of the energy levels in similarnuclei. Consider a nucleus like B11 (boron-eleven), which is composed of ﬁveprotons and six neutrons. In the nucleus the eleven particles interact with oneanother in a most complicated dance. Now, there is one conﬁguration of all thepossible interactions which has the lowest possible energy; this is the normalstate of the nucleus, and is called the ground state. If the nucleus is disturbed(for example, by being struck by a high-energy proton or other particle) it can beput into any number of other conﬁgurations, called excited states, each of whichwill have a characteristic energy that is higher than that of the ground state. Innuclear physics research, such as is carried on with Van de Graaﬀ generator (forexample, in Caltech’s Kellogg and Sloan Laboratories), the energies and otherproperties of these excited states are determined by experiment. The energies ofthe ﬁfteen lowest known excited states of B11 are shown in a one-dimensionalgraph on the left half of Fig. 8-7. The lowest horizontal line represents the groundstate. The ﬁrst excited state has an energy 2.14 MeV higher than the groundstate, the next an energy 4.46 MeV higher than the ground state, and so on.The study of nuclear physics attempts to ﬁnd an explanation for this rathercomplicated pattern of energies; there is as yet, however, no complete generaltheory of such nuclear energy levels.

If we replace one of the neutrons in B11 with a proton, we have the nucleus ofan isotope of carbon, C11. The energies of the lowest sixteen excited states of C11have also been measured; they are shown in the right half of Fig. 8-7. (The brokenlines indicate levels for which the experimental information is questionable.)

Looking at Fig. 8-7, we see a striking similarity between the pattern of theenergy levels in the two nuclei. The ﬁrst excited states are about 2 MeV abovethe ground states. There is a large gap of about 2.3 MeV to the second excitedstate, then a small jump of only 0.5 MeV to the third level. Again, between8-7

Fig. 8-6. The force between two protons

depends on every possible parameter.

Fig. 8-7. The energy levels of B11 andC11 (energies in MeV). The ground state ofC11 is 1.982 MeV higher than that of B11.

the fourth and ﬁfth levels, a big jump; but between the ﬁfth and sixth a tinyseparation of the order of 0.1 MeV. And so on. After about the tenth level, thecorrespondence seems to become lost, but can still be seen if the levels are labeledwith their other deﬁning characteristics—for instance, their angular momentumand what they do to lose their extra energy.

The striking similarity of the pattern of the energy levels of B11 and C11 issurely not just a coincidence. It must reveal some physical law. It shows, in fact,that even in the complicated situation in a nucleus, replacing a neutron by aproton makes very little change. This can mean only that the neutron-neutronand proton-proton forces must be nearly identical. Only then would we expectthe nuclear conﬁgurations with ﬁve protons and six neutrons to be the same aswith six protons and ﬁve neutrons.

Notice that the properties of these two nuclei tell us nothing about theneutron-proton force; there are the same number of neutron-proton combinationsin both nuclei. But if we compare two other nuclei, such as C14, which has sixprotons and eight neutrons, with N14, which has seven of each, we ﬁnd a similarcorrespondence of energy levels. So we can conclude that the p-p, n-n, and p-nforces are identical in all their complexities. There is an unexpected principle inthe laws of nuclear forces. Even though the force between each pair of nuclearparticles is very complicated, the force between the three possible diﬀerent pairsis the same.

But there are some small diﬀerences. The levels do not correspond exactly;also, the ground state of C11 has an absolute energy (its mass) which is higherthan the ground state of B11 by 1.982 MeV. All the other levels are also higherin absolute energy by this same amount. So the forces are not exactly equal. Butwe know very well that the complete forces are not exactly equal; there is anelectrical force between two protons because each has a positive charge, whilebetween two neutrons there is no such electrical force. Can we perhaps explainthe diﬀerences between B11 and C11 by the fact that the electrical interactionof the protons is diﬀerent in the two cases? Perhaps even the remaining minordiﬀerences in the levels are caused by electrical eﬀects? Since the nuclear forcesare so much stronger than the electrical force, electrical eﬀects would have onlya small perturbing eﬀect on the energies of the levels.

In order to check this idea, or rather to ﬁnd out what the consequences of thisidea are, we ﬁrst consider the diﬀerence in the ground-state energies of the twonuclei. To take a very simple model, we suppose that the nuclei are spheres ofradius r (to be determined), containing Z protons. If we consider that a nucleusis like a sphere with uniform charge density, we would expect the electrostaticenergy (from Eq. 8.7) to be

U = 35

(Zqe)24π0r

.

(8.22)

If we knew the nuclear radius r, we could use (8.23) to ﬁnd the electrostaticenergy diﬀerence between B11 and C11. But let’s do the opposite; let’s insteaduse the observed energy diﬀerence to compute the radius, assuming that theenergy diﬀerence is all electrostatic in origin.

That is, however, not quite right. The energy diﬀerence of 1.982 MeV betweenthe ground states of B11 and C11 includes the rest energies—that is, the en-ergy mc2—of all the particles. In going from B11 to C11, we replace a neutron bya proton and an electron, which have less mass. So part of the energy diﬀerence8-8

where qe is the elementary charge of the proton. Since Z is ﬁve for B11 and sixfor C11, their electrostatic energies would be diﬀerent.With such a small number of protons, however, Eq. (8.22) is not quite correct.If we compute the electrical energy between all pairs of protons, considered aspoints which we assume to be nearly uniformly distributed throughout the sphere,we ﬁnd that in Eq. (8.22) the quantity Z2 should be replaced by Z(Z − 1), sothe energy is

U = 35

Z(Z − 1)q2

e

4π0r

= 35

Z(Z − 1)e2

r

.

(8.23)

is the diﬀerence in the rest energies of a neutron and that of a proton plus anelectron, which is 0.784 MeV. The diﬀerence, to be accounted for by electrostaticenergy, is thus more than 1.982 MeV; it is

1.982 MeV + 0.784 MeV = 2.766 MeV.

Using this energy in Eq. (8.23), for the radius of either B11 or C11 we ﬁnd

r = 3.12 × 10−13 cm.

(8.24)Does this number have any meaning? To see whether it does, we shouldcompare it with some other determination of the radius of these nuclei. Forexample, we can make another measurement of the radius of a nucleus by seeinghow it scatters fast particles. From such measurements it has been found, in fact,that the density of matter in all nuclei is nearly the same, i.e., their volumes areproportional to the number of particles they contain. If we let A be the numberof protons and neutrons in a nucleus (a number very nearly proportional to itsmass), it is found that its radius is given byr = A1/3r0,

(8.25)

(8.26)From these measurements we ﬁnd that the radius of a B11 (or a C11) nucleus

r0 = 1.2 × 10−13 cm.

where

is expected to be

r = (11)1/3(1.2 × 10−13) cm = 2.7 × 10−13 cm.

Comparing this result with (8.24), we see that our assumptions that the energydiﬀerence between B11 and C11 is electrostatic is fairly good; the discrepancy isonly about 15% (not bad for our ﬁrst nuclear computation!).

The reason for the discrepancy is probably the following. According to thecurrent understanding of nuclei, an even number of nuclear particles—in the caseof B11, ﬁve neutrons together with ﬁve protons—makes a kind of core; when onemore particle is added to this core, it revolves around on the outside to make anew spherical nucleus, rather than being absorbed. If this is so, we should havetaken a diﬀerent electrostatic energy for the additional proton. We should havetaken the excess energy of C11 over B11 to be just

ZBq24π0r

e

which is the energy needed to add one more proton to the outside of the core.This number is just 5/6 of what Eq. (8.23) predicts, so the new prediction for theradius is 5/6 of (8.24), which is in much closer agreement with what is directlymeasured.We can draw two conclusions from this agreement. One is that the electricallaws appear to be working at dimensions as small as 10−13 cm. The other is thatwe have veriﬁed the remarkable coincidence that the nonelectrical part of theforces between proton and proton, neutron and neutron, and proton and neutronare all equal.

8-5 Energy in the electrostatic ﬁeldWe now consider other methods of calculating electrostatic energy. Theycan all be derived from the basic relation Eq. (8.3), the sum, over all pairs ofcharges, of the mutual energies of each charge-pair. First we wish to write anexpression for the energy of a charge distribution. As usual, we consider thateach volume element dV contains the element of charge ρ dV . Then Eq. (8.3)should be written

Z

all

space

U = 12

ρ(1)ρ(2)4π0r12

dV1dV2.

(8.27)

8-9

Notice the factor 12, which is introduced because in the double integral overdV1 and dV2 we have counted all pairs of charge elements twice. (There is noconvenient way of writing an integral that keeps track of the pairs so that eachpair is counted only once.) Next we notice that the integral over dV2 in (8.27) isjust the potential at (1). That is,

Z

ρ(2)4π0r12

dV2 = φ(1),

so that (8.27) can be written as

U = 12

Z

ρ(1)φ(1) dV1.

Or, since the point (2) no longer appears, we can simply write

Z

U = 12

ρφ dV.

(8.28)

This equation can be interpreted as follows. The potential energy of thecharge ρ dV is the product of this charge and the potential at the same point.The total energy is therefore the integral over φρ dV . But there is again the2. It is still required because we are counting energies twice. The mutualfactor 1energies of two charges is the charge of one times the potential at it due to theother. Or, it can be taken as the second charge times the potential at it fromthe ﬁrst. Thus for two point charges we would write

or

U = q1φ(1) = q1

U = q2φ(2) = q2

q2

4π0r12

q1

4π0r12

.

Notice that we could also write

U = 1

2[q1φ(1) + q2φ(2)].

(8.29)

The integral in (8.28) corresponds to the sum of both terms in the bracketsof (8.29). That is why we need the factor 12.

An interesting question is: Where is the electrostatic energy located? Onemight also ask: Who cares? What is the meaning of such a question? If there isa pair of interacting charges, the combination has a certain energy. Do we needto say that the energy is located at one of the charges or the other, or at both,or in between? These questions may not make sense because we really know onlythat the total energy is conserved. The idea that the energy is located somewhereis not necessary.Yet suppose that it did make sense to say, in general, that energy is locatedat a certain place, as it does for heat energy. We might then extend our principleof the conservation of energy with the idea that if the energy in a given volumechanges, we should be able to account for the change by the ﬂow of energy intoor out of that volume. You realize that our early statement of the principle ofthe conservation of energy is still perfectly all right if some energy disappears atone place and appears somewhere else far away without anything passing (thatis, without any special phenomena occurring) in the space between. We are,therefore, now discussing an extension of the idea of the conservation of energy.We might call it a principle of the local conservation of energy. Such a principlewould say that the energy in any given volume changes only by the amount thatﬂows into or out of the volume. It is indeed possible that energy is conservedlocally in such a way. If it is, we would have a much more detailed law than thesimple statement of the conservation of total energy. It does turn out that innature energy is conserved locally. We can ﬁnd formulas for where the energy islocated and how it travels from place to place.

8-10

There is also a physical reason why it is imperative that we be able to saywhere energy is located. According to the theory of gravitation, all mass is asource of gravitational attraction. We also know, by E = mc2, that mass andenergy are equivalent. All energy is, therefore, a source of gravitational force.If we could not locate the energy, we could not locate all the mass. We wouldnot be able to say where the sources of the gravitational ﬁeld are located. Thetheory of gravitation would be incomplete.

If we restrict ourselves to electrostatics there is really no way to tell where theenergy is located. The complete Maxwell equations of electrodynamics give usmuch more information (although even then the answer is, strictly speaking, notunique.) We will therefore discuss this question in detail again in a later chapter.We will give you now only the result for the particular case of electrostatics. Theenergy is located in space, where the electric ﬁeld is. This seems reasonablebecause we know that when charges are accelerated they radiate electric ﬁelds.We would like to say that when light or radiowaves travel from one point toanother, they carry their energy with them. But there are no charges in thewaves. So we would like to locate the energy where the electromagnetic ﬁeld isand not at the charges from which it came. We thus describe the energy, not interms of the charges, but in terms of the ﬁelds they produce. We can, in fact,show that Eq. (8.28) is numerically equal to

Z

U = 02

E · E dV.

(8.30)

We can then interpret this formula as saying that when an electric ﬁeld is present,there is located in space an energy whose density (energy per unit volume) is

u = 0

2 E · E = 0E22 .

(8.31)

This idea is illustrated in Fig. 8-8.

To show that Eq. (8.30) is consistent with our laws of electrostatics, we beginby introducing into Eq. (8.28) the relation between ρ and φ that we obtained inChapter 6:

ρ = −0 ∇2φ.

Z

U = − 02

φ∇2φ dV.

(cid:19)

(cid:18)

φ

(cid:19)

∂φ∂y

(cid:18)∂φ(cid:19)2

∂y

−

(cid:18)

φ

(cid:19)

∂φ∂z

−

+ ∂∂z

(8.32)

(cid:18)∂φ(cid:19)2

∂z(8.33)

Fig. 8-8. Each volume element dV =dx dy dz in an electric ﬁeld contains theenergy (0/2)E2 dV .

Writing out the components of the integrand, we see that

We get

(cid:18) ∂2φ(cid:18)

∂x2

φ

φ∇2φ = φ

+ ∂2φ(cid:19)∂y2−

+ ∂2φ(cid:18)∂φ(cid:19)2∂z2

∂φ∂x

= ∂∂x

+ ∂∂y= ∇ · (φ∇φ) − (∇φ) · (∇φ).

∂x

Our energy integral is then

U = 02

(∇φ) · (∇φ) dV − 02

Z

∇ · (φ∇φ) dV.

Z

Z

Z

We can use Gauss’ theorem to change the second integral into a surface integral:

∇ · (φ∇φ) dV =

(φ∇φ) · n da.

(8.34)

vol.

surface

We evaluate the surface integral in the case that the surface goes to inﬁnity(so the volume integrals become integrals over all space), supposing that all thecharges are located within some ﬁnite distance. The simple way to proceed is to8-11

take a spherical surface of enormous radius R whose center is at the origin ofcoordinates. We know that when we are very far away from all charges, φ variesas 1/R and ∇φ as 1/R2. (Both will decrease even faster with R if there thenet charge in the distribution is zero.) Since the surface area of the large sphereincreases as R2, we see that the surface integral falls oﬀ as (1/R)(1/R2)R2 = (1/R)as the radius of the sphere increases. So if we include all space in our integration(R → ∞), the surface integral goes to zero and we have that

U = 02

(∇φ) · (∇φ) dV = 02

E · E dV.

(8.35)

Z

all

space

Z

all

space

We see that it is possible for us to represent the energy of any charge distributionas being the integral over an energy density located in the ﬁeld.

8-6 The energy of a point chargeOur new relation, Eq. (8.35), says that even a single point charge q will have

some electrostatic energy. In this case, the electric ﬁeld is given by

So the energy density at the distance r from the charge is

E =

q

4π0r2 .

0E22 =

q2

32π20r4 .

We can take for an element of volume a spherical shell of thickness dr andarea 4πr2. The total energy is

∞Z

r=0

U =

q2

8π0r2 dr = − q28π0

1r

.

(8.36)

(cid:12)(cid:12)(cid:12)(cid:12)r=∞

r=0

Now the limit at r = ∞ gives no diﬃculty. But for a point charge we aresupposed to integrate down to r = 0, which gives an inﬁnite integral. Equa-tion (8.35) says that there is an inﬁnite amount of energy in the ﬁeld of a pointcharge, although we began with the idea that there was energy only betweenpoint charges. In our original energy formula for a collection of point charges(Eq. 8.3), we did not include any interaction energy of a charge with itself. Whathas happened is that when we went over to a continuous distribution of chargein Eq. (8.27), we counted the energy of interaction of every inﬁnitesimal chargewith all other inﬁnitesimal charges. The same account is included in Eq. (8.35),so when we apply it to a ﬁnite point charge, we are including the energy it wouldtake to assemble that charge from inﬁnitesimal parts. You will notice, in fact,that we would also get the result in Eq. (8.36) if we used our expression (8.11)for the energy of a charged sphere and let the radius tend toward zero.

We must conclude that the idea of locating the energy in the ﬁeld is inconsistentwith the assumption of the existence of point charges. One way out of the diﬃcultywould be to say that elementary charges, such as an electron, are not points butare really small distributions of charge. Alternatively, we could say that thereis something wrong in our theory of electricity at very small distances, or withthe idea of the local conservation of energy. There are diﬃculties with eitherpoint of view. These diﬃculties have never been overcome; they exist to thisday. Sometime later, when we have discussed some additional ideas, such as themomentum in an electromagnetic ﬁeld, we will give a more complete account ofthese fundamental diﬃculties in our understanding of nature.

8-12



