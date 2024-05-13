17-1 The physics of inductionIn

the last chapter we described many phenomena which show that the eﬀectsof induction are quite complicated and interesting. Now we want to discussthe fundamental principles which govern these eﬀects. We have already deﬁnedthe emf in a conducting circuit as the total accumulated force on the chargesthroughout the length of the loop. More speciﬁcally, it is the tangential componentof the force per unit charge, integrated along the wire once around the circuit.This quantity is equal, therefore, to the total work done on a single charge thattravels once around the circuit.

We have also given the「ﬂux rule,」which says that the emf is equal to therate at which the magnetic ﬂux through such a conducting circuit is changing.Let’s see if we can understand why that might be. First, we’ll consider a case inwhich the ﬂux changes because a circuit is moved in a steady ﬁeld.

In Fig. 17-1 we show a simple loop of wire whose dimensions can be changed.The loop has two parts, a ﬁxed U-shaped part (a) and a movable crossbar (b)that can slide along the two legs of the U. There is always a complete circuit, butits area is variable. Suppose we now place the loop in a uniform magnetic ﬁeldwith the plane of the U perpendicular to the ﬁeld. According to the rule, whenthe crossbar is moved there should be in the loop an emf that is proportional tothe rate of change of the ﬂux through the loop. This emf will cause a current inthe loop. We will assume that there is enough resistance in the wire that thecurrents are small. Then we can neglect any magnetic ﬁeld from this current.The ﬂux through the loop is wLB, so the「ﬂux rule」would give for the

emf—which we write as E—

17-1 The physics of induction17-2 Exceptions to the「ﬂux rule」17-3 Particle acceleration by aninduced electric ﬁeld; thebetatron

17-4 A paradox17-5 Alternating-current generator17-6 Mutual inductance17-7 Self-inductance17-8 Inductance and magnetic energy

E = wB

dLdt

= wBv,

where v is the speed of translation of the crossbar.Now we should be able to understand this result from the magnetic v × Bforces on the charges in the moving crossbar. These charges will feel a force,tangential to the wire, equal to vB per unit charge. It is constant along thelength w of the crossbar and zero elsewhere, so the integral is

E = wvB,

Fig. 17-1. An emf is induced in a loop ifthe ﬂux is changed by varying the area ofthe circuit.

which is the same result we got from the rate of change of the ﬂux.

The argument just given can be extended to any case where there is a ﬁxedmagnetic ﬁeld and the wires are moved. One can prove, in general, that for anycircuit whose parts move in a ﬁxed magnetic ﬁeld the emf is the time derivativeof the ﬂux, regardless of the shape of the circuit.

On the other hand, what happens if the loop is stationary and the magneticﬁeld is changed? We cannot deduce the answer to this question from the sameargument. It was Faraday’s discovery—from experiment—that the「ﬂux rule」isstill correct no matter why the ﬂux changes. The force on electric charges is givenin complete generality by F = q(E + v × B); there are no new special「forces dueto changing magnetic ﬁelds.」Any forces on charges at rest in a stationary wirecome from the E term. Faraday’s observations led to the discovery that electricand magnetic ﬁelds are related by a new law: in a region where the magneticﬁeld is changing with time, electric ﬁelds are generated. It is this electric ﬁeld17-1

which drives the electrons around the wire—and so is responsible for the emf ina stationary circuit when there is a changing magnetic ﬂux.

The general law for the electric ﬁeld associated with a changing magnetic

ﬁeld is

(17.1)We will call this Faraday’s law. It was discovered by Faraday but was ﬁrst writtenin diﬀerential form by Maxwell, as one of his equations. Let’s see how thisequation gives the「ﬂux rule」for circuits.

∇ × E = − ∂B∂t

.

Using Stokes’ theorem, this law can be written in integral form as

E · ds =

(∇ × E) · n da = −

S

S

· n da,

∂B∂t

(17.2)

where, as usual, Γ is any closed curve and S is any surface bounded by it. Here,remember, Γ is a mathematical curve ﬁxed in space, and S is a ﬁxed surface.Then the time derivative can be taken outside the integral and we have

Z

I

Γ

Z

Z

B · n da

I

Γ

E · ds = − ddt= − ddt

S

(ﬂux through S).

(17.3)

Applying this relation to a curve Γ that follows a ﬁxed circuit of conductor, weget the「ﬂux rule」once again. The integral on the left is the emf, and that on theright is the negative rate of change of the ﬂux linked by the circuit. So Eq. (17.1)applied to a ﬁxed circuit is equivalent to the「ﬂux rule.」

So the「ﬂux rule」—that the emf in a circuit is equal to the rate of change ofthe magnetic ﬂux through the circuit—applies whether the ﬂux changes becausethe ﬁeld changes or because the circuit moves (or both). The two possibilities—「circuit moves」or「ﬁeld changes」—are not distinguished in the statement of therule. Yet in our explanation of the rule we have used two completely distinctlaws for the two cases—v × B for「circuit moves」and ∇ × E = −∂B/∂t for「ﬁeld changes.」We know of no other place in physics where such a simple and accurate generalprinciple requires for its real understanding an analysis in terms of two diﬀerentphenomena. Usually such a beautiful generalization is found to stem from asingle deep underlying principle. Nevertheless, in this case there does not appearto be any such profound implication. We have to understand the「rule」as thecombined eﬀects of two quite separate phenomena.We must look at the「ﬂux rule」in the following way. In general, the forceper unit charge is F /q = E + v × B. In moving wires there is the force from thesecond term. Also, there is an E-ﬁeld if there is somewhere a changing magneticﬁeld. They are independent eﬀects, but the emf around the loop of wire is alwaysequal to the rate of change of magnetic ﬂux through it.

17-2 Exceptions to the「ﬂux rule」We will now give some examples, due in part to Faraday, which show theimportance of keeping clearly in mind the distinction between the two eﬀectsresponsible for induced emf’s. Our examples involve situations to which the「ﬂuxrule」cannot be applied—either because there is no wire at all or because thepath taken by induced currents moves about within an extended volume of aconductor.We begin by making an important point: The part of the emf that comesfrom the E-ﬁeld does not depend on the existence of a physical wire (as does thev × B part). The E-ﬁeld can exist in free space, and its line integral around anyimaginary line ﬁxed in space is the rate of change of the ﬂux of B through thatline. (Note that this is quite unlike the E-ﬁeld produced by static charges, for inthat case the line integral of E around a closed loop is always zero.)

17-2

Fig. 17-2. When the disc rotates there isan emf from v × B, but with no change inthe linked ﬂux.

Now we will describe a situation in which the ﬂux through a circuit does notchange, but there is nevertheless an emf. Figure 17-2 shows a conducting discwhich can be rotated on a ﬁxed axis in the presence of a magnetic ﬁeld. Onecontact is made to the shaft and another rubs on the outer periphery of the disc.A circuit is completed through a galvanometer. As the disc rotates, the「circuit,」in the sense of the place in space where the currents are, is always the same. Butthe part of the「circuit」in the disc is in material which is moving. Although theﬂux through the「circuit」is constant, there is still an emf, as can be observed bythe deﬂection of the galvanometer. Clearly, here is a case where the v×B force inthe moving disc gives rise to an emf which cannot be equated to a change of ﬂux.Now we consider, as an opposite example, a somewhat unusual situation inwhich the ﬂux through a「circuit」(again in the sense of the place where thecurrent is) changes but where there is no emf. Imagine two metal plates withslightly curved edges, as shown in Fig. 17-3, placed in a uniform magnetic ﬁeldperpendicular to their surfaces. Each plate is connected to one of the terminalsof a galvanometer, as shown. The plates make contact at one point P, so there isa complete circuit. If the plates are now rocked through a small angle, the pointof contact will move to P 0. If we imagine the「circuit」to be completed throughthe plates on the dotted line shown in the ﬁgure, the magnetic ﬂux through thiscircuit changes by a large amount as the plates are rocked back and forth. Yetthe rocking can be done with small motions, so that v × B is very small andthere is practically no emf. The「ﬂux rule」does not work in this case. It must beapplied to circuits in which the material of the circuit remains the same. Whenthe material of the circuit is changing, we must return to the basic laws. Thecorrect physics is always given by the two basic laws

F = q(E + v × B),∇ × E = − ∂B∂t

.

Fig. 17-3. When the plates are rockedin a uniform magnetic ﬁeld, there can be alarge change in the ﬂux linkage without thegeneration of an emf.

17-3 Particle acceleration by an induced electric ﬁeld; the betatronWe have said that the electromotive force generated by a changing magneticﬁeld can exist even without conductors; that is, there can be magnetic inductionwithout wires. We may still imagine an electromotive force around an arbitrarymathematical curve in space. It is deﬁned as the tangential component of Eintegrated around the curve. Faraday’s law says that this line integral is equal tominus the rate of change of the magnetic ﬂux through the closed curve, Eq. (17.3).As an example of the eﬀect of such an induced electric ﬁeld, we want nowto consider the motion of an electron in a changing magnetic ﬁeld. We imaginea magnetic ﬁeld which, everywhere on a plane, points in a vertical direction,as shown in Fig. 17-4. The magnetic ﬁeld is produced by an electromagnet,but we will not worry about the details. For our example we will imagine thatthe magnetic ﬁeld is symmetric about some axis, i.e., that the strength of themagnetic ﬁeld will depend only on the distance from the axis. The magnetic ﬁeldis also varying with time. We now imagine an electron that is moving in this ﬁeld17-3

Fig. 17-4. An electron accelerating in an axially symmetric,

increasing magnetic ﬁeld.

on a path that is a circle of constant radius with its center at the axis of the ﬁeld.(We will see later how this motion can be arranged.) Because of the changingmagnetic ﬁeld, there will be an electric ﬁeld E tangential to the electron’s orbitwhich will drive it around the circle. Because of the symmetry, this electric ﬁeldwill have the same value everywhere on the circle. If the electron’s orbit has theradius r, the line integral of E around the orbit is equal to minus the rate ofchange of the magnetic ﬂux through the circle. The line integral of E is just itsmagnitude times the circumference of the circle, 2πr. The magnetic ﬂux must, ingeneral, be obtained from an integral. For the moment, we let Bav represent theaverage magnetic ﬁeld in the interior of the circle; then the ﬂux is this averagemagnetic ﬁeld times the area of the circle. We will have

2πrE = ddt

(Bav · πr2).

Since we are assuming r is constant, E is proportional to the time derivative

of the average ﬁeld:

(17.4)The electron will feel the electric force qE and will be accelerated by it. Re-membering that the relativistically correct equation of motion is that the rate ofchange of the momentum is proportional to the force, we have

E = r2

dt

dBav

.

qE = dpdt

.

(17.5)

For the circular orbit we have assumed, the electric force on the electron isalways in the direction of its motion, so its total momentum will be increasing atthe rate given by Eq. (17.5). Combining Eqs. (17.5) and (17.4), we may relatethe rate of change of momentum to the change of the average magnetic ﬁeld:

Integrating with respect to t, we ﬁnd for the electron’s momentum

dpdt

= qr2

dBav

dt

.

p = p0 + qr

2 ∆Bav,

(17.6)

(17.7)

where p0 is the momentum with which the electrons start out, and ∆Bav, isthe subsequent change in Bav. The operation of a betatron—a machine foraccelerating electrons to high energies—is based on this idea.To see how the betatron operates in detail, we must now examine how theelectron can be constrained to move on a circle. We have discussed in Chapter 11of Vol. I the principle involved. If we arrange that there is a magnetic ﬁeld B17-4

at the orbit of the electron, there will be a transverse force qv × B which, for asuitably chosen B, can cause the electron to keep moving on its assumed orbit.In the betatron this transverse force causes the electron to move in a circularorbit of constant radius. We can ﬁnd out what the magnetic ﬁeld at the orbitmust be by using again the relativistic equation of motion, but this time, for thetransverse component of the force. In the betatron (see Fig. 17-4), B is at rightangles to v, so the transverse force is qvB. Thus the force is equal to the rate ofchange of the transverse component pt of the momentum:

qvB = dptdt

.

(17.8)

When a particle is moving in a circle, the rate of change of its transversemomentum is equal to the magnitude of the total momentum times ω, theangular velocity of rotation (following the arguments of Chapter 11, Vol. I):

where, since the motion is circular,

dptdt

= ωp,

ω = vr

.

Setting the magnetic force equal to the transverse acceleration, we have

qvBorbit = p

vr

,

(17.9)

(17.10)

(17.11)

where Borbit is the ﬁeld at the radius r.As the betatron operates, the momentum of the electron grows in proportionto Bav, according to Eq. (17.7), and if the electron is to continue to move in itsproper circle, Eq. (17.11) must continue to hold as the momentum of the electronincreases. The value of Borbit must increase in proportion to the momentum p.Comparing Eq. (17.11) with Eq. (17.7), which determines p, we see that thefollowing relation must hold between Bav, the average magnetic ﬁeld inside theorbit at the radius r, and the magnetic ﬁeld Borbit at the orbit:

∆Bav = 2 ∆Borbit.

(17.12)

The correct operation of a betatron requires that the average magnetic ﬁeld insidethe orbit increases at twice the rate of the magnetic ﬁeld at the orbit itself. Inthese circumstances, as the energy of the particle is increased by the inducedelectric ﬁeld the magnetic ﬁeld at the orbit increases at just the rate required tokeep the particle moving in a circle.

The betatron is used to accelerate electrons to energies of tens of millions ofvolts, or even to hundreds of millions of volts. However, it becomes impractical forthe acceleration of electrons to energies much higher than a few hundred millionvolts for several reasons. One of them is the practical diﬃculty of attaining therequired high average value for the magnetic ﬁeld inside the orbit. Another is thatEq. (17.6) is no longer correct at very high energies because it does not includethe loss of energy from the particle due to its radiation of electromagnetic energy(the so-called synchrotron radiation discussed in Chapter 36, Vol. I). For thesereasons, the acceleration of electrons to the highest energies—to many billions ofelectron volts—is accomplished by means of a diﬀerent kind of machine, called asynchrotron.

17-4 A paradoxWe would now like to describe for you an apparent paradox. A paradox is asituation which gives one answer when analyzed one way, and a diﬀerent answerwhen analyzed another way, so that we are left in somewhat of a quandary asto actually what should happen. Of course, in physics there are never any realparadoxes because there is only one correct answer; at least we believe that nature17-5

will act in only one way (and that is the right way, naturally). So in physics aparadox is only a confusion in our own understanding. Here is our paradox.

Imagine that we construct a device like that shown in Fig. 17-5. There is athin, circular plastic disc supported on a concentric shaft with excellent bearings,so that it is quite free to rotate. On the disc is a coil of wire in the form of ashort solenoid concentric with the axis of rotation. This solenoid carries a steadycurrent I provided by a small battery, also mounted on the disc. Near the edgeof the disc and spaced uniformly around its circumference are a number of smallmetal spheres insulated from each other and from the solenoid by the plasticmaterial of the disc. Each of these small conducting spheres is charged with thesame electrostatic charge Q. Everything is quite stationary, and the disc is atrest. Suppose now that by some accident—or by prearrangement—the current inthe solenoid is interrupted, without, however, any intervention from the outside.So long as the current continued, there was a magnetic ﬂux through the solenoidmore or less parallel to the axis of the disc. When the current is interrupted, thisﬂux must go to zero. There will, therefore, be an electric ﬁeld induced whichwill circulate around in circles centered at the axis. The charged spheres onthe perimeter of the disc will all experience an electric ﬁeld tangential to theperimeter of the disc. This electric force is in the same sense for all the chargesand so will result in a net torque on the disc. From these arguments we wouldexpect that as the current in the solenoid disappears, the disc would begin torotate. If we knew the moment of inertia of the disc, the current in the solenoid,and the charges on the small spheres, we could compute the resulting angularvelocity.

But we could also make a diﬀerent argument. Using the principle of theconservation of angular momentum, we could say that the angular momentum ofthe disc with all its equipment is initially zero, and so the angular momentum ofthe assembly should remain zero. There should be no rotation when the currentis stopped. Which argument is correct? Will the disc rotate or will it not? Wewill leave this question for you to think about.

We should warn you that the correct answer does not depend on any nonessen-tial feature, such as the asymmetric position of a battery, for example. In fact,you can imagine an ideal situation such as the following: The solenoid is made ofsuperconducting wire through which there is a current. After the disc has beencarefully placed at rest, the temperature of the solenoid is allowed to rise slowlyWhen the temperature of the wire reaches the transition temperature betweensuperconductivity and normal conductivity, the current in the solenoid will bebrought to zero by the resistance of the wire. The ﬂux will, as before, fall to zero,and there will be an electric ﬁeld around the axis. We should also warn you thatthe solution is not easy, nor is it a trick. When you ﬁgure it out, you will havediscovered an important principle of electromagnetism.

Fig. 17-5. Will the disc rotate if the cur-

rent I is stopped?

17-5 Alternating-current generatorIn the remainder of this chapter we apply the principles of Section 17-1 toanalyze a number of the phenomena discussed in Chapter 16. We ﬁrst lookin more detail at the alternating-current generator. Such a generator consistsbasically of a coil of wire rotating in a uniform magnetic ﬁeld. The same resultcan also be achieved by a ﬁxed coil in a magnetic ﬁeld whose direction rotatesin the manner described in the last chapter. We will consider only the formercase. Suppose we have a circular coil of wire which can be turned on an axisalong one of its diameters. Let this coil be located in a uniform magnetic ﬁeldperpendicular to the axis of rotation, as in Fig. 17-6. We also imagine that thetwo ends of the coil are brought to external connections through some kind ofsliding contacts.

Due to the rotation of the coil, the magnetic ﬂux through it will be changing.The circuit of the coil will therefore have an emf in it. Let S be the area of thecoil and θ the angle between the magnetic ﬁeld and the normal to the plane of17-6

Fig. 17-6. A coil of wire rotating in auniform magnetic ﬁeld—the basic idea ofthe AC generator.

the coil.* The ﬂux through the coil is thenBS cos θ.

(17.13)If the coil is rotating at the uniform angular velocity ω, θ varies with timeas θ = ωt.Each turn of the coil will have an emf equal to the rate of change of this ﬂux.If the coil has N turns of wire the total emf will be N times larger, so

E = −N

ddt

(BS cos ωt) = N BSω sin ωt.

(17.14)

If we bring the wires from the generator to a point some distance from therotating coil, where the magnetic ﬁeld is zero, or at least is not varying with time,the curl of E in this region will be zero and we can deﬁne an electric potential.In fact, if there is no current being drawn from the generator, the potentialdiﬀerence V between the two wires will be equal to the emf in the rotating coil.That is,

V = N BSω sin ωt = V0 sin ωt.

The potential diﬀerence between the wires varies as sin ωt. Such a varyingpotential diﬀerence is called an alternating voltage.Since there is an electric ﬁeld between the wires, they must be electricallycharged. It is clear that the emf of the generator has pushed some excess chargesout to the wire until the electric ﬁeld from them is strong enough to exactlycounterbalance the induction force. Seen from outside the generator, the twowires appear as though they had been electrostatically charged to the potentialdiﬀerence V , and as though the charge was being changed with time to givean alternating potential diﬀerence. There is also another diﬀerence from anelectrostatic situation. If we connect the generator to an external circuit thatpermits passage of a current, we ﬁnd that the emf does not permit the wires tobe discharged but continues to provide charge to the wires as current is drawnfrom them, attempting to keep the wires always at the same potential diﬀerence.If, in fact, the generator is connected in a circuit whose total resistance is R, thecurrent through the circuit will be proportional to the emf of the generator andinversely proportional to R. Since the emf has a sinusoidal time variation, soalso does the current. There is an alternating current

I = ER

= V0R

sin ωt.

Power =

nvF · ds.

(17.15)

Now remember that qnv is the current I, and that the emf is deﬁned as theintegral of F/q around the circuit. We get the result

Power from a generator = EI.

(17.16)

* Now that we are using the letter A for the vector potential, we prefer to let S stand for a

surface area.

17-7

The schematic diagram of such a circuit is shown in Fig. 17-7.We can also see that the emf determines how much energy is supplied by thegenerator. Each charge in the wire is receiving energy at the rate F · v, where Fis the force on the charge and v is its velocity. Now let the number of movingcharges per unit length of the wire be n; then the power being delivered into anyelement ds of the wire is

For a wire, v is always along ds, so we can rewrite the power as

nvF · ds.

The total power being delivered to the complete circuit is the integral of thisexpression around the complete loop:

F · vn ds.

I

Fig. 17-7. A circuit with an AC generator

and a resistance.

When there is a current in the coil of the generator, there will also bemechanical forces on it. In fact, we know that the torque on the coil is proportionalto its magnetic moment, to the magnetic ﬁeld strength B, and to the sine of theangle between. The magnetic moment is the current in the coil times its area.Therefore the torque is

(17.17)The rate at which mechanical work must be done to keep the coil rotating is theangular velocity ω times the torque:

τ = N ISB sin θ.

dWdt

= ωτ = ωN ISB sin θ.

(17.18)

Comparing this equation with Eq. (17.14), we see that the rate of mechanicalwork required to rotate the coil against the magnetic forces is just equal to EI,the rate at which electrical energy is delivered by the emf of the generator. Allof the mechanical energy used up in the generator appears as electrical energy inthe circuit.

As another example of the currents and forces due to an induced emf, let’sanalyze what happens in the setup described in Section 17-1, and shown inFig. 17-1. There are two parallel wires and a sliding crossbar located in a uniformmagnetic ﬁeld perpendicular to the plane of the parallel wires. Now let’s assumethat the「bottom」of the U (the left side in the ﬁgure) is made of wires of highresistance, while the two side wires are made of a good conductor like copper—then we don’t need to worry about the change of the circuit resistance as thecrossbar is moved. As before, the emf in the circuit is

E = vBw.

(17.19)

The current in the circuit is proportional to this emf and inversely proportionalto the resistance of the circuit:

I = ER

= vBwR

.

(17.20)

Because of this current there will be a magnetic force on the crossbar that isproportional to its length, to the current in it, and to the magnetic ﬁeld, suchthat

F = BIw.

(17.21)

Taking I from Eq. (17.20), we have for the force

F = B2w2

R

v.

(17.22)

We see that the force is proportional to the velocity of the crossbar. The directionof the force, as you can easily see, is opposite to its velocity. Such a「velocity-proportional」force, which is like the force of viscosity, is found whenever inducedcurrents are produced by moving conductors in a magnetic ﬁeld. The examples ofeddy currents we gave in the last chapter also produced forces on the conductorsproportional to the velocity of the conductor, even though such situations, ingeneral, give a complicated distribution of currents which is diﬃcult to analyze.It is often convenient in the design of mechanical systems to have dampingforces which are proportional to the velocity. Eddy-current forces provide one ofthe most convenient ways of getting such a velocity-dependent force. An exampleof the application of such a force is found in the conventional domestic wattmeter.In the wattmeter there is a thin aluminum disc that rotates between the polesof a permanent magnet. This disc is driven by a small electric motor whosetorque is proportional to the power being consumed in the electrical circuit of thehouse. Because of the eddy-current forces in the disc, there is a resistive forceproportional to the velocity. In equilibrium, the velocity is therefore proportionalto the rate of consumption of electrical energy. By means of a counter attachedto the rotating disc, a record is kept of the number of revolutions it makes.17-8

This count is an indication of the total energy consumption, i.e., the number ofwatthours used.

We may also point out that Eq. (17.22) shows that the force from inducedcurrents—that is, any eddy-current force—is inversely proportional to the resis-tance. The force will be larger, the better the conductivity of the material. Thereason, of course, is that an emf produces more current if the resistance is low,and the stronger currents represent greater mechanical forces.

We can also see from our formulas how mechanical energy is converted intoelectrical energy. As before, the electrical energy supplied to the resistance ofthe circuit is the product EI. The rate at which work is done in moving theconducting crossbar is the force on the bar times its velocity. Using Eq. (17.21)for the force, the rate of doing work is

dWdt

= v2B2w2

R

.

We see that this is indeed equal to the product EI we would get from Eqs. (17.19)and (17.20). Again the mechanical work appears as electrical energy.

17-6 Mutual inductanceWe now want to consider a situation in which there are ﬁxed coils of wire butchanging magnetic ﬁelds. When we described the production of magnetic ﬁeldsby currents, we considered only the case of steady currents. But so long as thecurrents are changed slowly, the magnetic ﬁeld will at each instant be nearly thesame as the magnetic ﬁeld of a steady current. We will assume in the discussionof this section that the currents are always varying suﬃciently slowly that this istrue.

In Fig. 17-8 is shown an arrangement of two coils which demonstrates thebasic eﬀects responsible for the operation of a transformer. Coil 1 consists of aconducting wire wound in the form of a long solenoid. Around this coil—andinsulated from it—is wound coil 2, consisting of a few turns of wire. If now acurrent is passed through coil 1, we know that a magnetic ﬁeld will appear insideit. This magnetic ﬁeld also passes through coil 2. As the current in coil 1 isvaried, the magnetic ﬂux will also vary, and there will be an induced emf in coil 2.We will now calculate this induced emf.

We have seen in Section 13-5 that the magnetic ﬁeld inside a long solenoid is

uniform and has the magnitude

B = 10c2

N1I1

l

,

(17.23)

where N1 is the number of turns in coil 1, I1 is the current through it, and l is itslength. Let’s say that the cross-sectional area of coil 1 is S; then the ﬂux of B isits magnitude times S. If coil 2 has N2 turns, this ﬂux links the coil N2 times.Therefore the emf in coil 2 is given by

E2 = −N2S

dBdt

.

(17.24)

The only quantity in Eq. (17.23) which varies with time is I1. The emf is thereforegiven by

Fig. 17-8. A current in coil 1 produces a

magnetic ﬁeld through coil 2.

E2 = − N1N2S0c2l

dI1dt

.

(17.25)

We see that the emf in coil 2 is proportional to the rate of change of thecurrent in coil 1. The constant of proportionality, which is basically a geometricfactor of the two coils, is called the mutual inductance, and is usually designatedM21. Equation (17.25) is then written

E2 = M21

dI1dt

.

(17.26)

17-9

Suppose now that we were to pass a current through coil 2 and ask aboutthe emf in coil 1. We would compute the magnetic ﬁeld, which is everywhereproportional to the current I2. The ﬂux linkage through coil 1 would depend onthe geometry, but would be proportional to the current I2. The emf in coil 1would, therefore, again be proportional to dI2/dt: We can write

E1 = M12

dI2dt

.

(17.27)

The computation of M12 would be more diﬃcult than the computation we havejust done for M21. We will not carry through that computation now, because wewill show later in this chapter that M12 is necessarily equal to M21.Since for any coil its ﬁeld is proportional to its current, the same kind of resultwould be obtained for any two coils of wire. The equations (17.26) and (17.27)would have the same form; only the constants M21 and M12 would be diﬀerent.Their values would depend on the shapes of the coils and their relative positions.

Fig. 17-9. Any two coils have a mutualinductance M proportional to the integralof ds1 · ds2/r12.

Suppose that we wish to ﬁnd the mutual inductance between any two arbitrarycoils—for example, those shown in Fig. 17-9. We know that the general expressionfor the emf in coil 1 can be written asE1 = − ddt

B · n da,

Z

(1)

where B is the magnetic ﬁeld and the integral is to be taken over a surfacebounded by circuit 1. We have seen in Section 14-1 that such a surface integralof B can be related to a line integral of the vector potential. In particular,

Z

B · n da =

A · ds1,

(1)

(1)

where A represents the vector potential and ds1 is an element of circuit 1. Theline integral is to be taken around circuit 1. The emf in coil 1 can therefore bewritten as

E1 = − ddt

A · ds1.

(17.28)

Now let’s assume that the vector potential at circuit 1 comes from currents

in circuit 2. Then it can be written as a line integral around circuit 2:

A =

1

4π0c2

(2)

r12

I2 ds2

,

(17.29)

where I2 is the current in circuit 2, and r12 is the distance from the element ofthe circuit ds2 to the point on circuit 1 at which we are evaluating the vectorpotential. (See Fig. 17-9.) Combining Eqs. (17.28) and (17.29), we can expressthe emf in circuit 1 as a double line integral:

I

I

(1)

I

I

I

E1 = − 14π0c2

ddt

I2 ds2

· ds1.

(1)

(2)

r12

In this equation the integrals are all taken with respect to stationary circuits. Theonly variable quantity is the current I2, which does not depend on the variables17-10

of integration. We may therefore take it out of the integrals. The emf can thenbe written as

E1 = M12

dI2dt

I

,

ds2 · ds1

where the coeﬃcient M12 is

M12 = − 14π0c2

I

(1)

(2)

r12

.

(17.30)

We see from this integral that M12 depends only on the circuit geometry. Itdepends on a kind of average separation of the two circuits, with the averageweighted most for parallel segments of the two coils. Our equation can be usedfor calculating the mutual inductance of any two circuits of arbitrary shape. Also,it shows that the integral for M12 is identical to the integral for M21. We havetherefore shown that the two coeﬃcients are identical. For a system with onlytwo coils, the coeﬃcients M12 and M21 are often represented by the symbol Mwithout subscripts, called simply the mutual inductance:

M12 = M21 = M.

17-7 Self-inductanceIn discussing the induced electromotive forces in the two coils of Figs. 17-8or 17-9, we have considered only the case in which there was a current in onecoil or the other.If there are currents in the two coils simultaneously, themagnetic ﬂux linking either coil will be the sum of the two ﬂuxes which wouldexist separately, because the law of superposition applies for magnetic ﬁelds. Theemf in either coil will therefore be proportional not only to the change of thecurrent in the other coil, but also to the change in the current of the coil itself.Thus the total emf in coil 2 should be written*

E2 = M21

dI1dt

+ M22

dI2dt

.

(17.31)

Similarly, the emf in coil 1 will depend not only on the changing current in coil 2,but also on the changing current in itself:

E1 = M12

dI2dt

+ M11

dI1dt

.

(17.32)

The coeﬃcients M22 and M11 are always negative numbers. It is usual to write(17.33)

M11 = −L1,

M22 = −L2,

where L1 and L2 are called the self-inductances of the two coils.The self-induced emf will, of course, exist even if we have only one coil. Anycoil by itself will have a self-inductance L. The emf will be proportional to therate of change of the current in it. For a single coil, it is usual to adopt theconvention that the emf and the current are considered positive if they are in thesame direction. With this convention, we may write for the emf of a single coil

E = −L

dIdt

.

(17.34)

The negative sign indicates that the emf opposes the change in current—it isoften called a「back emf.」

Since any coil has a self-inductance which opposes the change in current,the current in the coil has a kind of inertia. In fact, if we wish to change thecurrent in a coil we must overcome this inertia by connecting the coil to someexternal voltage source such as a battery or a generator, as shown in the schematic

* The sign of M12 and M21 in Eqs. (17.31) and (17.32) depends on the arbitrary choices

for the sense of a positive current in the two coils.

17-11

diagram of Fig. 17-10(a). In such a circuit, the current I depends on the voltage Vaccording to the relation

dIdt

.

V = L

(17.35)This equation has the same form as Newton’s law of motion for a particlein one dimension. We can therefore study it by the principle that「the sameequations have the same solutions.」Thus, if we make the externally appliedvoltage V correspond to an externally applied force F, and the current I in a coilcorrespond to the velocity v of a particle, the inductance L of the coil correspondsto the mass m of the particle.* See Fig. 17-10(b). We can make the followingtable of corresponding quantities.

ParticleF (force)v (velocity)

x (displacement)

F = m

dvdt

mv (momentum)

2 mv2 (kinetic energy)1

V (potential diﬀerence)

Coil

I (current)q (charge)dIV = LdtLI

2 LI2 (magnetic energy)1

Fig. 17-10. (a) A circuit with a voltagesource and an inductance. (b) An analogousmechanical system.

17-8 Inductance and magnetic energyContinuing with the analogy of the preceding section, we would expect thatcorresponding to the mechanical momentum p = mv, whose rate of change is theapplied force, there should be an analogous quantity equal to LI, whose rate ofchange is V. We have no right, of course, to say that LI is the real momentum ofthe circuit; in fact, it isn’t. The whole circuit may be standing still and have nomomentum. It is only that LI is analogous to the momentum mv in the sense ofsatisfying corresponding equations. In the same way, to the kinetic energy 12 mv2,there corresponds an analogous quantity 12 LI2. But there we have a surprise.2 LI2 is really the energy in the electrical case also. This is because the rateThis 1of doing work on the inductance is VI, and in the mechanical system it is F v,the corresponding quantity. Therefore, in the case of the energy, the quantitiesnot only correspond mathematically, but also have the same physical meaning aswell.

We may see this in more detail as follows. As we found in Eq. (17.16), therate of electrical work by induced forces is the product of the electromotive forceand the current:

dWdt

= EI.

Replacing E by its expression in terms of the current from Eq. (17.34), we have

dWdt

= −LI

dIdt

.

(17.36)

Integrating this equation, we ﬁnd that the energy required from an externalsource to overcome the emf in the self-inductance while building up the current†(which must equal the energy stored, U) is− W = U = 1

2 LI2.Therefore the energy stored in an inductance is 1

Applying the same arguments to a pair of coils such as those in Figs. 17-8

or 17-9, we can show that the total electrical energy of the system is given by

2 LI2.

(17.37)

U = 1

2 L1I2

1 + 1

2 L2I2

2 + MI1I2.

(17.38)

* This is, incidentally, not the only way a correspondence can be set up between mechanical

and electrical quantities.

† We are neglecting any energy loss to heat from the current in the resistance of the coil.Such losses require additional energy from the source but do not change the energy which goesinto the inductance.

17-12

2 L2I2

2 L1I2

For, starting with I = 0 in both coils, we could ﬁrst turn on the current I1 incoil 1, with I2 = 0. The work done is just 11. But now, on turning up I2, wenot only do the work 12 against the emf in circuit 2, but also an additionalamount MI1I2, which is the integral of the emf [M(dI2/dt)] in circuit 1 timesthe now constant current I1 in that circuit.Suppose we now wish to ﬁnd the force between any two coils carrying thecurrents I1 and I2. We might at ﬁrst expect that we could use the principleof virtual work, by taking the change in the energy of Eq. (17.38). We mustremember, of course, that as we change the relative positions of the coils theonly quantity which varies is the mutual inductance M. We might then writethe equation of virtual work as

−F ∆x = ∆U = I1I2 ∆M (wrong).

But this equation is wrong because, as we have seen earlier, it includes only thechange in the energy of the two coils and not the change in the energy of thesources which are maintaining the currents I1 and I2 at their constant values. Wecan now understand that these sources must supply energy against the inducedemf’s in the coils as they are moved. If we wish to apply the principle of virtualwork correctly, we must also include these energies. As we have seen, however, wemay take a short cut and use the principle of virtual work by remembering thatthe total energy is the negative of what we have called Umech, the「mechanicalenergy.」We can therefore write for the force

− F ∆x = ∆Umech = −∆U.

(17.39)

The force between two coils is then given by

F ∆x = I1I2 ∆M.

Equation (17.38) for the energy of a system of two coils can be used to showthat an interesting inequality exists between mutual inductance M and the self-inductances L1 and L2 of the two coils. It is clear that the energy of two coilsmust be positive. If we begin with zero currents in the coils and increase thesecurrents to some values, we have been adding energy to the system. If not, thecurrents would spontaneously increase with release of energy to the rest of theworld—an unlikely thing to happen! Now our energy equation, Eq. (17.38), canequally well be written in the following form:+ 12

U = 1

(17.40)

(cid:19)2

2 L1

(cid:18)

(cid:18)

(cid:19)

L2 − M2L1

I22 .

I1 + ML1

I2

That is just an algebraic transformation. This quantity must always be positivefor any values of I1 and I2. In particular, it must be positive if I2 should happento have the special value

(17.41)But with this current for I2, the ﬁrst term in Eq. (17.40) is zero. If the energy isto be positive, the last term in (17.40) must be greater than zero. We have therequirement that

I2 = − L1M

I1.

L1L2 > M2.

We have thus proved the general result that the magnitude of the mutual induc-tance M of any two coils is necessarily less than or equal to the geometric meanof the two self-inductances. (M itself may be positive or negative, depending onthe sign conventions for the currents I1 and I2.)

The relation between M and the self-inductances is usually written as

pL1L2.pL1L2.

|M| <

M = k

(17.42)

(17.43)17-13

The constant k is called the coeﬃcient of coupling. If most of the ﬂux from onecoil links the other coil, the coeﬃcient of coupling is near one; we say the coilsare「tightly coupled.」If the coils are far apart or otherwise arranged so that thereis very little mutual ﬂux linkage, the coeﬃcient of coupling is near zero and themutual inductance is very small.

For calculating the mutual inductance of two coils, we have given in Eq. (17.30)a formula which is a double line integral around the two circuits. We might thinkthat the same formula could be used to get the self-inductance of a single coil bycarrying out both line integrals around the same coil. This, however, will notwork, because the denominator r12 of the integrand will go to zero when the twoline elements ds1 and ds2 are at the same point on the coil. The self-inductanceobtained from this formula is inﬁnite. The reason is that this formula is anapproximation that is valid only when the cross sections of the wires of thetwo circuits are small compared with the distance from one circuit to the other.Clearly, this approximation doesn’t hold for a single coil. It is, in fact, true thatthe inductance of a single coil tends logarithmically to inﬁnity as the diameter ofits wire is made smaller and smaller.

We must, then, look for a diﬀerent way of calculating the self-inductance of asingle coil. It is necessary to take into account the distribution of the currentswithin the wires because the size of the wire is an important parameter. Weshould therefore ask not what is the inductance of a「circuit,」but what is theinductance of a distribution of conductors. Perhaps the easiest way to ﬁndthis inductance is to make use of the magnetic energy. We found earlier, inSection 15-3, an expression for the magnetic energy of a distribution of stationarycurrents:

U = 12

j · A dV.

(17.44)

If we know the distribution of current density j, we can compute the vectorpotential A and then evaluate the integral of Eq. (17.44) to get the energy. Thisenergy is equal to the magnetic energy of the self-inductance, 12 LI2. Equatingthe two gives us a formula for the inductance:

L = 1I2

j · A dV.

(17.45)

We expect, of course, that the inductance is a number depending only on thegeometry of the circuit and not on the current I in the circuit. The formula ofEq. (17.45) will indeed give such a result, because the integral in this equation isproportional to the square of the current—the current appears once through jand again through the vector potential A. The integral divided by I2 will dependon the geometry of the circuit but not on the current I.

Equation (17.44) for the energy of a current distribution can be put in a quitediﬀerent form which is sometimes more convenient for calculation. Also, as wewill see later, it is a form that is important because it is more generally valid. Inthe energy equation, Eq. (17.44), both A and j can be related to B, so we canhope to express the energy in terms of the magnetic ﬁeld—just as we were ableto relate the electrostatic energy to the electric ﬁeld. We begin by replacing jby 0c2∇ × B. We cannot replace A so easily, since B = ∇ × A cannot bereversed to give A in terms of B. Anyway, we can write

Z

Z

Z

Z

U = 0c22

U = 0c22

(∇ × B) · A dV.

(17.46)

The interesting thing is that—with some restrictions—this integral can be

written as

B · (∇ × A) dV.

(17.47)

To see this, we write out in detail a typical term. Suppose that we take theterm (∇ × B)zAz which occurs in the integral of Eq. (17.46). Writing out the17-14

components, we get

Z (cid:18) ∂By

∂x

(cid:19)

− ∂Bx∂y

Az dx dy dz.

(There are, of course, two more integrals of the same kind.) We now integratethe ﬁrst term with respect to x—integrating by parts. That is, we can say

Z ∂By

∂x

Z

Az dx = ByAz −

By

∂Az∂x

dx.

Now suppose that our system—meaning the sources and ﬁelds—is ﬁnite, so thatas we go to large distances all ﬁelds go to zero. Then if the integrals are carriedout over all space, evaluating the term ByAz at the limits will give zero. We haveleft only the term with By(∂Az/∂x), which is evidently one part of By(∇ × A)yand, therefore, of B · (∇ × A). If you work out the other ﬁve terms, you will seethat Eq. (17.47) is indeed equivalent to Eq. (17.46).But now we can replace (∇ × A) by B, to get

Z

Z

U = 0c22

B · B dV.

(17.48)

We have expressed the energy of a magnetostatic situation in terms of themagnetic ﬁeld only. The expression corresponds closely to the formula we foundfor the electrostatic energy:

U = 02

E · E dV.

(17.49)

One reason for emphasizing these two energy formulas is that sometimes theyare more convenient to use. More important, it turns out that for dynamic ﬁelds(when E and B are changing with time) the two expressions (17.48) and (17.49)remain true, whereas the other formulas we have given for electric or magneticenergies are no longer correct—they hold only for static ﬁelds.

If we know the magnetic ﬁeld B of a single coil, we can ﬁnd the self-inductanceby equating the energy expression (17.48) to 12 LI2. Let’s see how this worksby ﬁnding the self-inductance of a long solenoid. We have seen earlier that themagnetic ﬁeld inside a solenoid is uniform and B outside is zero. The magnitudeof the ﬁeld inside is B = nI/0c2, where n is the number of turns per unit lengthin the winding and I is the current. If the radius of the coil is r and its lengthis L (we take L very long, so that we can neglect end eﬀects, i.e., L (cid:29) r), thevolume inside is πr2L. The magnetic energy is therefore

U = 0c2

2 B2 · (Vol) = n2I2

20c2 πr2L,

which is equal to 1

2 LI2. Or,

L = πr2n2

0c2 L.

(17.50)

17-15

18-1 Maxwell’s equations18-2 How the new term works18-3 All of classical physics18-4 A travelling ﬁeld18-5 The speed of light18-6 Solving Maxwell’s equations; thepotentials and the wave equation

18

The Maxwell Equations

18-1 Maxwell’s equationsIn

this chapter we come back to the complete set of the four Maxwell equationsthat we took as our starting point in Chapter 1. Until now, we have been studyingMaxwell’s equations in bits and pieces; it is time to add one ﬁnal piece, and toput them all together. We will then have the complete and correct story forelectromagnetic ﬁelds that may be changing with time in any way. Anything saidin this chapter that contradicts something said earlier is true and what was saidearlier is false—because what was said earlier applied to such special situationsas, for instance, steady currents or ﬁxed charges. Although we have been verycareful to point out the restrictions whenever we wrote an equation, it is easy toforget all of the qualiﬁcations and to learn too well the wrong equations. Nowwe are ready to give the whole truth, with no qualiﬁcations (or almost none).

The complete Maxwell equations are written in Table 18-1, in words as well asin mathematical symbols. The fact that the words are equivalent to the equationsshould by this time be familiar—you should be able to translate back and forthfrom one form to the other.

The ﬁrst equation—that the divergence of E is the charge density over 0—istrue in general. In dynamic as well as in static ﬁelds, Gauss’ law is always valid.The ﬂux of E through any closed surface is proportional to the charge inside.The third equation is the corresponding general law for magnetic ﬁelds. Sincethere are no magnetic charges, the ﬂux of B through any closed surface is alwayszero. The second equation, that the curl of E is −∂B/∂t, is Faraday’s law andwas discussed in the last two chapters. It also is generally true. The last equationhas something new. We have seen before only the part of it which holds forsteady currents. In that case we said that the curl of B is j/0c2, but the correctgeneral equation has a new part that was discovered by Maxwell.Until Maxwell’s work, the known laws of electricity and magnetism were thosewe have studied in Chapters 3 through 17. In particular, the equation for themagnetic ﬁeld of steady currents was known only as

∇ × B = j

0c2 .

(18.1)

Maxwell began by considering these known laws and expressing them as diﬀer-ential equations, as we have done here. (Although the ∇ notation was not yetinvented, it is mainly due to Maxwell that the importance of the combinations ofderivatives, which we today call the curl and the divergence, ﬁrst became appar-ent.) He then noticed that there was something strange about Eq. (18.1). If onetakes the divergence of this equation, the left-hand side will be zero, because thedivergence of a curl is always zero. So this equation requires that the divergenceof j also be zero. But if the divergence of j is zero, then the total ﬂux of currentout of any closed surface is also zero.The ﬂux of current from a closed surface is the decrease of the charge insidethe surface. This certainly cannot in general be zero because we know that thecharges can be moved from one place to another. The equation

∇ · j = − ∂ρ∂t

(18.2)

has, in fact, been almost our deﬁnition of j. This equation expresses the veryfundamental law that electric charge is conserved—any ﬂow of charge must come18-1

Table 18-1 Classical Physics

(Flux of E through a closed surface) = (Charge inside)/0

(Line integral of E around a loop) = − ddt(Flux of B through a closed surface) = 0

(Flux of B through the loop)

c2(Integral of B around a loop) = (Current through the loop)/0(Flux of E through the loop)

+ ddt

(Flux of current through a closed loop) = − ddt

(Charge inside)



mvp1 − v2/c2

(Newton’s law, with Einstein’s modiﬁcation)

Maxwell’s equationsI. ∇ · E = ρ0

II. ∇ × E = − ∂B∂t

III. ∇ · B = 0

IV.

c2∇ × B = j0

+ ∂E∂t

Conservation of charge

∇ · j = − ∂ρ∂t

Force law

F = q(E + v × B)

Law of motion

(p) = F ,

ddt

where

p =

Gravitation

F = −G

m1m2

r2

er

from some supply. Maxwell appreciated this diﬃculty and proposed that it couldbe avoided by adding the term ∂E/∂t to the right-hand side of Eq. (18.1); hethen got the fourth equation in Table 18-1:

IV.

c2∇ × B = j0

+ ∂E∂t

.

It was not yet customary in Maxwell’s time to think in terms of abstractﬁelds. Maxwell discussed his ideas in terms of a model in which the vacuum waslike an elastic solid. He also tried to explain the meaning of his new equation interms of the mechanical model. There was much reluctance to accept his theory,ﬁrst because of the model, and second because there was at ﬁrst no experimentaljustiﬁcation. Today, we understand better that what counts are the equationsthemselves and not the model used to get them. We may only question whetherthe equations are true or false. This is answered by doing experiments, and untoldnumbers of experiments have conﬁrmed Maxwell’s equations. If we take awaythe scaﬀolding he used to build it, we ﬁnd that Maxwell’s beautiful ediﬁce standson its own. He brought together all of the laws of electricity and magnetism andmade one complete and beautiful theory.

Let us show that the extra term is just what is required to straighten outthe diﬃculty Maxwell discovered. Taking the divergence of his equation (IV inTable 18-1), we must have that the divergence of the right-hand side is zero:

∇ · j0

+ ∇ · ∂E∂t

= 0.

(18.3)

In the second term, the order of the derivatives with respect to coordinates and18-2

time can be reversed, so the equation can be rewritten as

∇ · j + 0

∂∂t

∇ · E = 0.

(18.4)

But the ﬁrst of Maxwell’s equations says that the divergence of E is ρ/0.Inserting this equality in Eq. (18.4), we get back Eq. (18.2), which we know istrue. Conversely, if we accept Maxwell’s equations—and we do because no onehas ever found an experiment that disagrees with them—we must conclude thatcharge is always conserved.

The laws of physics have no answer to the question:「What happens if a chargeis suddenly created at this point—what electromagnetic eﬀects are produced?」No answer can be given because our equations say it doesn’t happen. If it wereto happen, we would need new laws, but we cannot say what they would be. Wehave not had the chance to observe how a world without charge conservationbehaves. According to our equations, if you suddenly place a charge at somepoint, you had to carry it there from somewhere else. In that case, we can saywhat would happen.

When we added a new term to the equation for the curl of E, we found thata whole new class of phenomena was described. We shall see that Maxwell’s littleaddition to the equation for ∇ × B also has far-reaching consequences. We cantouch on only a few of them in this chapter.

18-2 How the new term worksAs our ﬁrst example we consider what happens with a spherically symmetricradial distribution of current. Suppose we imagine a little sphere with radioactivematerial on it. This radioactive material is squirting out some charged particles.(Or we could imagine a large block of jello with a small hole in the center intowhich some charge had been injected with a hypodermic needle and from whichthe charge is slowly leaking out.) In either case we would have a current that iseverywhere radially outward. We will assume that it has the same magnitude inall directions.

Let the total charge inside any radius r be Q(r). If the radial current densityat the same radius is j(r), then Eq. (18.2) requires that Q decreases at the rate

∂Q(r)

∂t

= −4πr2j(r).

(18.5)

We now ask about the magnetic ﬁeld produced by the currents in this situation.Suppose we draw some loop Γ on a sphere of radius r, as shown in Fig. 18-1.There is some current through this loop, so we might expect to ﬁnd a magneticﬁeld circulating in the direction shown.

But we are already in diﬃculty. How can the B have any particular directionon the sphere? A diﬀerent choice of Γ would allow us to conclude that its directionis exactly opposite to that shown. So how can there be any circulation of Baround the currents?

We are saved by Maxwell’s equation. The circulation of B depends not onlyon the total current through Γ but also on the rate of change with time of theelectric ﬂux through it. It must be that these two parts just cancel. Let’s see ifthat works out.The electric ﬁeld at the radius r must be Q(r)/4π0r2—so long as the chargeis symmetrically distributed, as we assume. It is radial, and its rate of change isthen

=

∂E∂t

1

4π0r2

∂Q∂t

.

Comparing this with Eq. (18.5), we see

∂E∂t

= − j0

.

(18.6)

(18.7)

18-3

Fig. 18-1. What is the magnetic ﬁeld of

a spherically symmetric current?

Fig. 18-2. The magnetic ﬁeld near a charging capacitor.

In Eq. IV the two source terms cancel and the curl of B is always zero. There isno magnetic ﬁeld in our example.As our second example, we consider the magnetic ﬁeld of a wire used tocharge a parallel-plate condenser (see Fig. 18-2). If the charge Q on the plates ischanging with time (but not too fast), the current in the wires is equal to dQ/dt.We would expect that this current will produce a magnetic ﬁeld that encircles thewire. Surely, the current close to the plate must produce the normal magneticﬁeld—it cannot depend on where the current is going.

Suppose we take a loop Γ1 which is a circle with radius r, as shown in part (a)of the ﬁgure. The line integral of the magnetic ﬁeld should be equal to thecurrent I divided by 0c2. We have

2πrB = I

0c2 .

(18.8)

This is what we would get for a steady current, but it is also correct with Maxwell’saddition, because if we consider the plane surface S inside the circle, there areno electric ﬁelds on it (assuming the wire to be a very good conductor). Thesurface integral of ∂E/∂t is zero.Suppose, however, that we now slowly move the curve Γ downward. We getalways the same result until we draw even with the plates of the condenser. Thenthe current I goes to zero. Does the magnetic ﬁeld disappear? That would bequite strange. Let’s see what Maxwell’s equation says for the curve Γ2, which is acircle of radius r whose plane passes between the condenser plates [Fig. 18-2(b)].The line integral of B around Γ2 is 2πrB. This must equal the time derivative ofthe ﬂux of E through the plane circular surface S2. This ﬂux of E, we know fromGauss’ law, must be equal to 1/0 times the charge Q on one of the condenserplates. We have

(cid:18) Q

(cid:19)

That is very convenient. It is the same result we found in Eq. (18.8). In-tegrating over the changing electric ﬁeld gives the same magnetic ﬁeld as doesintegrating over the current in the wire. Of course, that is just what Maxwell’sequation says. It is easy to see that this must always be so by applying oursame arguments to the two surfaces S1 and S01 that are bounded by the samecircle Γ1 in Fig. 18-2(b). Through S1 there is the current I, but no electric ﬂux.Through S01 there is no current, but an electric ﬂux changing at the rate I/0.The same B is obtained if we use Eq. IV with either surface.From our discussion so far of Maxwell’s new term, you may have the impressionthat it doesn’t add much—that it just ﬁxes up the equations to agree with whatwe already expect. It is true that if we just consider Eq. IV by itself, nothingparticularly new comes out. The words「by itself 」are, however, all-important.Maxwell’s small change in Eq. IV, when combined with the other equations, does18-4

c2 2πrB = ddt

0

.

(18.9)

indeed produce much that is new and important. Before we take up these matters,however, we want to speak more about Table 18-1.

18-3 All of classical physicsIn Table 18-1 we have all that was known of fundamental classical physics,that is, the physics that was known by 1905. Here it all is, in one table. Withthese equations we can understand the complete realm of classical physics.

First we have the Maxwell equations—written in both the expanded form andthe short mathematical form. Then there is the conservation of charge, which iseven written in parentheses, because the moment we have the complete Maxwellequations, we can deduce from them the conservation of charge. So the table iseven a little redundant. Next, we have written the force law, because having allthe electric and magnetic ﬁelds doesn’t tell us anything until we know what theydo to charges. Knowing E and B, however, we can ﬁnd the force on an objectwith the charge q moving with velocity v. Finally, having the force doesn’t tellus anything until we know what happens when a force pushes on something; weneed the law of motion, which is that the force is equal to the rate of changeof the momentum. (Remember? We had that in Volume I.) We even include

relativity eﬀects by writing the momentum as p = m0v/p1 − v2/c2.

If we really want to be complete, we should add one more law—Newton’s law

of gravitation—so we put that at the end.

Therefore in one small table we have all the fundamental laws of classicalphysics—even with room to write them out in words and with some redundancy.This is a great moment. We have climbed a great peak. We are on the top of K-2—we are nearly ready for Mount Everest, which is quantum mechanics. We haveclimbed the peak of a「Great Divide,」and now we can go down the other side.We have mainly been trying to learn how to understand the equations. Nowthat we have the whole thing put together, we are going to study what theequations mean—what new things they say that we haven’t already seen. We’vebeen working hard to get up to this point. It has been a great eﬀort, but now weare going to have nice coasting downhill as we see all the consequences of ouraccomplishment.

18-4 A travelling ﬁeldNow for the new consequences. They come from putting together all ofMaxwell’s equations. First, let’s see what would happen in a circumstance whichwe pick to be particularly simple. By assuming that all the quantities vary only inone coordinate, we will have a one-dimensional problem. The situation is shown inFig. 18-3. We have a sheet of charge located on the yz-plane. The sheet is ﬁrst atrest, then instantaneously given a velocity u in the y-direction, and kept movingwith this constant velocity. You might worry about having such an「inﬁnite」

Fig. 18-3. An inﬁnite sheet of charge issuddenly set into motion parallel to itself.There are magnetic and electric ﬁelds thatpropagate out from the sheet at a constantspeed.18-5

acceleration, but it doesn’t really matter; just imagine that the velocity is broughtto u very quickly. So we have suddenly a surface current J (J is the current perunit width in the z-direction). To keep the problem simple, we suppose that thereis also a stationary sheet of charge of opposite sign superposed on the yz-plane, sothat there are no electrostatic eﬀects. Also, although in the ﬁgure we show onlywhat is happening in a ﬁnite region, we imagine that the sheet extends to inﬁnityin ±y and ±z. In other words, we have a situation where there is no current,and then suddenly there is a uniform sheet of current. What will happen?Well, when there is a sheet of current in the plus y-direction, there is, as weknow, a magnetic ﬁeld generated which will be in the minus z-direction for x > 0and in the opposite direction for x < 0. We could ﬁnd the magnitude of B byusing the fact that the line integral of the magnetic ﬁeld will be equal to thecurrent over 0c2. We would get that B = J/20c2 (since the current I in a stripof width w is Jw and the line integral of B is 2Bw).This gives us the ﬁeld next to the sheet—for small x—but since we areimagining an inﬁnite sheet, we would expect the same argument to give themagnetic ﬁeld farther out for larger values of x. However, that would mean that themoment we turn on the current, the magnetic ﬁeld is suddenly changed from zeroto a ﬁnite value everywhere. But wait! If the magnetic ﬁeld is suddenly changed,it will produce tremendous electrical eﬀects. (If it changes in any way, there areelectrical eﬀects.) So because we moved the sheet of charge, we make a changingmagnetic ﬁeld, and therefore electric ﬁelds must be generated. If there are electricﬁelds generated, they had to start from zero and change to something else. Therewill be some ∂E/∂t that will make a contribution, together with the current J,to the production of the magnetic ﬁeld. So through the various equations thereis a big intermixing, and we have to try to solve for all the ﬁelds at once.

By looking at the Maxwell equations alone, it is not easy to see directlyhow to get the solution. So we will ﬁrst show you what the answer is and thenverify that it does indeed satisfy the equations. The answer is the following: Theﬁeld B that we computed is, in fact, generated right next to the current sheet (forsmall x). It must be so, because if we make a tiny loop around the sheet, thereis no room for any electric ﬂux to go through it. But the ﬁeld B out farther—forlarger x—is, at ﬁrst, zero. It stays zero for awhile, and then suddenly turns on.In short, we turn on the current and the magnetic ﬁeld immediately next to itturns on to a constant value B; then the turning on of B spreads out from thesource region. After a certain time, there is a uniform magnetic ﬁeld everywhereout to some value x, and then zero beyond. Because of the symmetry, it spreadsin both the plus and minus x-directions.The E-ﬁeld does the same thing. Before t = 0 (when we turn on the current),the ﬁeld is zero everywhere. Then after the time t, both E and B are uniformout to the distance x = vt, and zero beyond. The ﬁelds make their way forwardlike a tidal wave, with a front moving at a uniform velocity which turns out tobe c, but for a while we will just call it v. A graph of the magnitude of E or Bversus x, as they appear at the time t, is shown in Fig. 18-4(a). Looking againat Fig. 18-3, at the time t, the region between x = ±vt is「ﬁlled」with the ﬁelds,but they have not yet reached beyond. We emphasize again that we are assumingthat the current sheet and, therefore the ﬁelds E and B, extend inﬁnitely farin both the y- and z-directions. (We cannot draw an inﬁnite sheet, so we haveshown only what happens in a ﬁnite area.)We want now to analyze quantitatively what is happening. To do that, wewant to look at two cross-sectional views, a top view looking down along they-axis, as shown in Fig. 18-5, and a side view looking back along the z-axis, asshown in Fig. 18-6. Suppose we start with the side view. We see the chargedsheet moving up; the magnetic ﬁeld points into the page for +x, and out of thepage for −x, and the electric ﬁeld is downward everywhere—out to x = ±vt.Let’s see if these ﬁelds are consistent with Maxwell’s equations. Let’s ﬁrst drawone of those loops that we use to calculate a line integral, say the rectangle Γ2shown in Fig. 18-6. You notice that one side of the rectangle is in the regionwhere there are ﬁelds, but one side is in the region the ﬁelds have still not18-6

Fig. 18-4. (a) The magnitude of B (or E)as a function of x at time t after the chargesheet is set in motion. (b) The ﬁelds fora charge sheet set in motion, toward nega-tive y at t = T . (c) The sum of (a) and (b).

TOP VIEW

J

(up)

CURRENTSHEET

E

B

x=0

z

Γ1

E = 0B = 0

L

x

y

J

SIDE VIEW

B

E

CURRENTSHEET

Γ2

E = 0B = 0

L

x

v t

v ∆t

v t

v ∆t

x=x0

0

x0

Fig. 18-5. Top view of Fig. 18-3.

Fig. 18-6. Side view of Fig. 18-3.

reached. There is some magnetic ﬂux through this loop. If it is changing, thereshould be an emf around it. If the wavefront is moving, we will have a changingmagnetic ﬂux, because the area in which B exists is progressively increasingat the velocity v. The ﬂux inside Γ2 is B times the part of the area inside Γ2which has a magnetic ﬁeld. The rate of change of the ﬂux, since the magnitudeof B is constant, is the magnitude times the rate of change of the area. The rateof change of the area is easy. If the width of the rectangle Γ2 is L, the area inwhich B exists changes by Lv ∆t in the time ∆t. (See Fig. 18-6.) The rate ofchange of ﬂux is then BLv. According to Faraday’s law, this should equal minusthe line integral of E around Γ2, which is just EL. We have the equation

and B:

(18.10)So if the ratio of E to B is v, the ﬁelds we have assumed will satisfy Faraday’sequation.But that is not the only equation; we have the other equation relating E

E = vB.

+ ∂E∂t

c2∇ × B = j0

(18.11)To apply this equation, we look at the top view in Fig. 18-5. We have seen thatthis equation will give us the value of B next to the current sheet. Also, for anyloop drawn outside the sheet but behind the wavefront, there is no curl of B norany j or changing E, so the equation is correct there. Now let’s look at whathappens for the curve Γ1 that intersects the wavefront, as shown in Fig. 18-5.Here there are no currents, so Eq. (18.11) can be written—in integral form—as

.

c2I

B · ds = ddt

Γ1

Z

inside Γ1

E · n da.

(18.12)

The line integral of B is just B times L. The rate of change of the ﬂux of E isdue only to the advancing wavefront. The area inside Γ1, where E is not zero, isincreasing at the rate vL. The right-hand side of Eq. (18.12) is then vLE. Thatequation becomes(18.13)We have a solution in which we have a constant B and a constant E behindthe front, both at right angles to the direction in which the front is moving andat right angles to each other. Maxwell’s equations specify the ratio of E to B.From Eqs. (18.10) and (18.13),

c2B = Ev.

E = vB,

and

E = c2

v

B.

But one moment! We have found two diﬀerent conditions on the ratio E/B. Cansuch a ﬁeld as we describe really exist? There is, of course, only one velocity v18-7

for which both of these equations can hold, namely v = c. The wavefront musttravel with the velocity c. We have an example in which the electrical inﬂuencefrom a current propagates at a certain ﬁnite velocity c.Now let’s ask what happens if we suddenly stop the motion of the chargedsheet after it has been on for a short time T. We can see what will happen bythe principle of superposition. We had a current that was zero and then wassuddenly turned on. We know the solution for that case. Now we are going toadd another set of ﬁelds. We take another charged sheet and suddenly start itmoving, in the opposite direction with the same speed, only at the time T afterwe started the ﬁrst current. The total current of the two added together is ﬁrstzero, then on for a time T, then oﬀ again—because the two currents cancel. Wehave a square「pulse」of current.The new negative current produces the same ﬁelds as the positive one, onlywith all the signs reversed and, of course, delayed in time by T. A wavefront againtravels out at the velocity c. At the time t it has reached the distance x = ±c(t−T),as shown in Fig. 18-4(b). So we have two「blocks」of ﬁeld marching out at thespeed c, as in parts (a) and (b) of Fig. 18-4. The combined ﬁelds are as shownin part (c) of the ﬁgure. The ﬁelds are zero for x > ct, they are constant (withthe values we found above) between x = c(t − T) and x = ct, and again zerofor x < c(t − T).In short, we have a little piece of ﬁeld—a block of thickness cT—which hasleft the current sheet and is travelling through space all by itself. The ﬁelds have「taken oﬀ」; they are propagating freely through space, no longer connected inany way with the source. The caterpillar has turned into a butterﬂy!How can this bundle of electric and magnetic ﬁelds maintain itself? Theanswer is: by the combined eﬀects of the Faraday law, ∇ × E = −∂B/∂t, andthe new term of Maxwell, c2∇ × B = ∂E/∂t. They cannot help maintainingthemselves. Suppose the magnetic ﬁeld were to disappear. There would be achanging magnetic ﬁeld which would produce an electric ﬁeld. If this electricﬁeld tries to go away, the changing electric ﬁeld would create a magnetic ﬁeldback again. So by a perpetual interplay—by the swishing back and forth fromone ﬁeld to the other—they must go on forever. It is impossible for them todisappear.* They maintain themselves in a kind of a dance—one making theother, the second making the ﬁrst—propagating onward through space.

18-5 The speed of lightWe have a wave which leaves the material source and goes outward at thevelocity c, which is the speed of light. But let’s go back a moment. From ahistorical point of view, it wasn’t known that the coeﬃcient c in Maxwell’sequations was also the speed of light propagation. There was just a constant inthe equations. We have called it c from the beginning, because we knew what itwould turn out to be. We didn’t think it would be sensible to make you learnthe formulas with a diﬀerent constant and then go back to substitute c whereverit belonged. From the point of view of electricity and magnetism, however, wejust start out with two constants, 0 and c2, that appear in the equations ofelectrostatics and magnetostatics:

and

∇ · E = ρ0

∇ × B = j

0c2 .

(18.14)

(18.15)

If we take any arbitrary deﬁnition of a unit of charge, we can determine exper-imentally the constant 0 required in Eq. (18.14)—say by measuring the forcebetween two unit charges at rest, using Coulomb’s law. We must also determine

* Well, not quite. They can be「absorbed」if they get to a region where there are charges.By which we mean that other ﬁelds can be produced somewhere which superpose on theseﬁelds and「cancel」them by destructive interference (see Chapter 31, Vol. I).

18-8

experimentally the constant 0c2 that appears in Eq. (18.15), which we can do,say, by measuring the force between two unit currents. (A unit current meansone unit of charge per second.) The ratio of these two experimental constantsis c2—just another「electromagnetic constant.」Notice now that this constant c2 is the same no matter what we choosefor our unit of charge. If we put twice as much「charge」—say twice as manyproton charges—in our「unit」of charge, 0 would need to be one-fourth as large.When we pass two of these「unit」currents through two wires, there will be twiceas much「charge」per second in each wire, so the force between two wires isfour times larger. The constant 0c2 must be reduced by one-fourth. But theratio 0c2/0 is unchanged.So just by experiments with charges and currents we ﬁnd a number c2 whichturns out to be the square of the velocity of propagation of electromagneticinﬂuences. From static measurements—by measuring the forces between two unitcharges and between two unit currents—we ﬁnd that c = 3.00 × 108 meters/sec.When Maxwell ﬁrst made this calculation with his equations, he said thatbundles of electric and magnetic ﬁelds should be propagated at this speed. Healso remarked on the mysterious coincidence that this was the same as the speedof light.「We can scarcely avoid the inference,」said Maxwell,「that light consistsin the transverse undulations of the same medium which is the cause of electricand magnetic phenomena.」

Maxwell had made one of the great uniﬁcations of physics. Before his time,there was light, and there was electricity and magnetism. The latter two hadbeen uniﬁed by the experimental work of Faraday, Oersted, and Ampère. Then,all of a sudden, light was no longer「something else,」but was only electricity andmagnetism in this new form—little pieces of electric and magnetic ﬁelds whichpropagate through space on their own.

We have called your attention to some characteristics of this special solution,which turn out to be true, however, for any electromagnetic wave: that themagnetic ﬁeld is perpendicular to the direction of motion of the wavefront;that the electric ﬁeld is likewise perpendicular to the direction of motion ofthe wavefront; and that the two vectors E and B are perpendicular to eachother. Furthermore, the magnitude of the electric ﬁeld E is equal to c times themagnitude of the magnetic ﬁeld B. These three facts—that the two ﬁelds aretransverse to the direction of propagation, that B is perpendicular to E, andthat E = cB—are generally true for any electromagnetic wave. Our special caseis a good one—it shows all the main features of electromagnetic waves.

18-6 Solving Maxwell’s equations; the potentials and the wave equationNow we would like to do something mathematical; we want to write Maxwell’sequations in a simpler form. You may consider that we are complicating them, butif you will be patient a little bit, they will suddenly come out simpler. Althoughby this time you are thoroughly used to each of the Maxwell equations, there aremany pieces that must all be put together. That’s what we want to do.We begin with ∇ · B = 0—the simplest of the equations. We know that it

implies that B is the curl of something. So, if we write

B = ∇ × A,

(18.16)

we have already solved one of Maxwell’s equations. (Incidentally, you appreciatethat it remains true that another vector A0 would be just as good if A0 = A+∇ψ—where ψ is any scalar ﬁeld—because the curl of ∇ψ is zero, and B is still thesame. We have talked about that before.)We take next the Faraday law, ∇ × E = −∂B/∂t, because it doesn’t involveany currents or charges. If we write B as ∇ × A and diﬀerentiate with respectto t, we can write Faraday’s law in the form

∇ × E = − ∂∂t

∇ × A.

18-9

Since we can diﬀerentiate either with respect to time or to space ﬁrst, we canalso write this equation as

(cid:18)

(cid:19)

∇ ×

E + ∂A∂t

= 0.

(18.17)

We see that E + ∂A/∂t is a vector whose curl is equal to zero. Therefore thatvector is the gradient of something. When we worked on electrostatics, we had∇ × E = 0, and then we decided that E itself was the gradient of something.We took it to be the gradient of −φ (the minus for technical convenience). Wedo the same thing for E + ∂A/∂t; we set

E + ∂A∂t

= −∇φ.

(18.18)

We use the same symbol φ so that, in the electrostatic case where nothing changeswith time and the ∂A/∂t term disappears, E will be our old −∇φ. So Faraday’sequation can be put in the form

E = −∇φ − ∂A∂t

.

(18.19)

We have solved two of Maxwell’s equations already, and we have found thatto describe the electromagnetic ﬁelds E and B, we need four potential functions:a scalar potential φ and a vector potential A, which is, of course, three functions.Now that A determines part of E, as well as B, what happens when wechange A to A0 = A + ∇ψ? In general, E would change if we didn’t take somespecial precaution. We can, however, still allow A to be changed in this waywithout aﬀecting the ﬁelds E and B—that is, without changing the physics—ifwe always change A and φ together by the rules

A0 = A + ∇ψ,

φ0 = φ − ∂ψ∂t

.

(18.20)

Then neither B nor E, obtained from Eq. (18.19), is changed.Previously, we chose to make ∇ · A = 0, to make the equations of staticssomewhat simpler. We are not going to do that now; we are going to make adiﬀerent choice. But we’ll wait a bit before saying what the choice is, becauselater it will be clear why the choice is made.Now we return to the two remaining Maxwell equations which will give usrelations between the potentials and the sources ρ and j. Once we can determineA and φ from the currents and charges, we can always get E and B from Eqs.(18.16) and (18.19), so we will have another form of Maxwell’s equations.

We begin by substituting Eq. (18.19) into ∇ · E = ρ/0; we get

(cid:18)

(cid:19)

∇ ·

which we can write also as

−∇φ − ∂A∂t

= ρ0

,

− ∇2φ − ∂∂t

∇ · A = ρ0

.

(18.21)

This is one equation relating φ and A to the sources.fourth Maxwell equation as

Our ﬁnal equation will be the most complicated. We start by rewriting the

c2∇ × B − ∂E∂t

= j0

,

and then substitute for B and E in terms of the potentials, using Eqs. (18.16)and (18.19):

(cid:18)

(cid:19)

c2∇ × (∇ × A) − ∂∂t

−∇φ − ∂A∂t

= j0

.

18-10

The ﬁrst term can be rewritten using the algebraic identity: ∇ × (∇ × A) =∇(∇ · A) − ∇2A; we get

− c2∇2A + c2∇(∇ · A) + ∂∂t

∇φ + ∂2A∂t2

= j0

.

(18.22)

It’s not very simple!

Fortunately, we can now make use of our freedom to choose arbitrarily thedivergence of A. What we are going to do is to use our choice to ﬁx things sothat the equations for A and for φ are separated but have the same form. Wecan do this by taking*

∇ · A = − 1c2

(18.23)When we do that, the two middle terms in A and φ in Eq. (18.22) cancel, andthat equation becomes much simpler:∇2A − 1c2

∂2A∂t2

= − j

(18.24)

0c2 .

∂φ∂t

.

And our equation for φ—Eq. (18.21)—takes on the same form:

∇2φ − 1c2

∂2φ∂t2

= − ρ0

.

(18.25)

What a beautiful set of equations! They are beautiful, ﬁrst, because theyare nicely separated—with the charge density, goes φ; with the current, goes A.Furthermore, although the left side looks a little funny—a Laplacian togetherwith a ∂2/∂t2—when we unfold it we see∂z2 − 1+ ∂2φ

+ ∂2φ∂y2

∂2φ∂t2

∂2φ∂x2

(18.26)

= − ρ0

c2

.

It has a nice symmetry in x, y, z, t—the −1/c2 is necessary because, of course,time and space are diﬀerent; they have diﬀerent units.Maxwell’s equations have led us to a new kind of equation for the potentialsφ and A but to the same mathematical form for all four functions φ, Ax, Ay,and Az. Once we learn how to solve these equations, we can get B and E from∇ × A and −∇φ − ∂A/∂t. We have another form of the electromagnetic lawsexactly equivalent to Maxwell’s equations, and in many situations they are muchsimpler to handle.

We have, in fact, already solved an equation much like Eq. (18.26). When we

studied sound in Chapter 47 of Vol. I, we had an equation of the form

∂2φ∂x2

= 1c2

∂2φ∂t2 ,

and we saw that it described the propagation of waves in the x-direction atthe speed c. Equation (18.26) is the corresponding wave equation for threedimensions. So in regions where there are no longer any charges and currents, thesolution of these equations is not that φ and A are zero. (Although that is indeedone possible solution.) There are solutions in which there is some set of φ and Awhich are changing in time but always moving out at the speed c. The ﬁelds travelonward through free space, as in our example at the beginning of the chapter.With Maxwell’s new term in Eq. IV, we have been able to write the ﬁeldequations in terms of A and φ in a form that is simple and that makes immediatelyapparent that there are electromagnetic waves. For many practical purposes, itwill still be convenient to use the original equations in terms of E and B. Butthey are on the other side of the mountain we have already climbed. Now we areready to cross over to the other side of the peak. Things will look diﬀerent—weare ready for some new and beautiful views.

* Choosing the ∇ · A is called「choosing a gauge.」Changing A by adding ∇ψ, is called a

「gauge transformation.」Equation (18.23) is called「the Lorenz gauge.」

18-11

19

The Principle of Least Action

