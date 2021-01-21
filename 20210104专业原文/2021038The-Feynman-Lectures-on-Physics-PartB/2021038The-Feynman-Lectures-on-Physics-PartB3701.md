# 1301

13-1 The magnetic ﬁeldThe

force on an electric charge depends not only on where it is, but alsoon how fast it is moving. Every point in space is characterized by two vectorquantities which determine the force on any charge. First, there is the electricforce, which gives a force component independent of the motion of the charge. Wedescribe it by the electric ﬁeld, E. Second, there is an additional force component,called the magnetic force, which depends on the velocity of the charge. Thismagnetic force has a strange directional character: At any particular point inspace, both the direction of the force and its magnitude depend on the directionof motion of the particle: at every instant the force is always at right anglesto the velocity vector; also, at any particular point, the force is always at rightangles to a ﬁxed direction in space (see Fig. 13-1); and ﬁnally, the magnitude ofthe force is proportional to the component of the velocity at right angles to thisunique direction. It is possible to describe all of this behavior by deﬁning themagnetic ﬁeld vector B, which speciﬁes both the unique direction in space andthe constant of proportionality with the velocity, and to write the magnetic forceas qv × B. The total electromagnetic force on a charge can, then, be written as(13.1)

F = q(E + v × B).

13-1 The magnetic ﬁeld13-2 Electric current; the conservation

of charge

13-3 The magnetic force on a current13-4 The magnetic ﬁeld of steady

currents; Ampère’s law

13-5 The magnetic ﬁeld of a straight

wire and of a solenoid; atomiccurrents

13-6 The relativity of magnetic and

13-7 The transformation of currents

13-8 Superposition; the right-hand

electric ﬁelds

and charges

rule

This is called the Lorentz force.The magnetic force is easily demonstrated by bringing a bar magnet close toa cathode-ray tube. The deﬂection of the electron beam shows that the presenceof the magnet results in forces on the electrons transverse to their direction ofmotion, as we described in Chapter 12 of Vol. I.The unit of magnetic ﬁeld B is evidently one newton·second per coulomb-meter. The same unit is also one volt·second per meter2. It is also called oneweber per square meter.

13-2 Electric current; the conservation of chargeWe consider ﬁrst how we can understand the magnetic forces on wires carryingelectric currents. In order to do this, we deﬁne what is meant by the currentdensity. Electric currents are electrons or other charges in motion with a net driftor ﬂow. We can represent the charge ﬂow by a vector which gives the amountof charge passing per unit area and per unit time through a surface element atright angles to the ﬂow (just as we did for the case of heat ﬂow). We call this thecurrent density and represent it by the vector j. It is directed along the motionof the charges. If we take a small area ∆S at a given place in the material, theamount of charge ﬂowing across that area in a unit time is

j · n ∆S,

(13.2)

where n is the unit vector normal to ∆S.The current density is related to the average ﬂow velocity of the charges. Sup-pose that we have a distribution of charges whose average motion is a drift with thevelocity v. As this distribution passes over a surface element ∆S, the charge ∆qpassing through the surface element in a time ∆t is equal to the charge con-tained in a parallelepiped whose base is ∆S and whose height is v ∆t, as shown inFig. 13-2. The volume of the parallelepiped is the projection of ∆S at right angles13-1

Review: Chapter 15, Vol. I, The Special

Theory of Relativity

Fig. 13-1. The velocity-dependent com-ponent of the force on a moving charge is atright angles to v and to the direction of B.It is also proportional to the component of vat right angles to B, that is, to v sin θ.

Fig. 13-2. If a charge distribution of den-sity ρ moves with the velocity v, the chargeper unit time through ∆S is ρv · n ∆S.

Z

any closed

surface

j · n dS = − ddt

(Qinside).

(13.6)

surface S is(cid:82) j · n dS.

Fig. 13-3. The current I through the

to v times v ∆t, which when multiplied by the charge density ρ will give ∆q. Thus

The charge per unit time is then ρv · n ∆S, from which we get

∆q = ρv · n ∆S ∆t.

(13.3)If the charge distribution consists of individual charges, say electrons, eachwith the charge q and moving with the mean velocity v, then the current density is(13.4)

j = ρv.

j = N qv.

where N is the number of charges per unit volume.The total charge passing per unit time through any surface S is called theelectric current, I. It is equal to the integral of the normal component of the ﬂowthrough all of the elements of the surface:

I =

j · n dS

(13.5)

(see Fig. 13-3).

The current I out of a closed surface S represents the rate at which chargeleaves the volume V enclosed by S. One of the basic laws of physics is thatelectric charge is indestructible; it is never lost or created. Electric charges canmove from place to place but never appear from nowhere. We say that charge isconserved. If there is a net current out of a closed surface, the amount of chargeinside must decrease by the corresponding amount (Fig. 13-4). We can, therefore,write the law of the conservation of charge as

Z

S

The charge inside can be written as a volume integral of the charge density:

Qinside =

ρ dV.

(13.7)

Z

Vinside S

If we apply (13.6) to a small volume ∆V , we know that the left-hand integralis ∇ · j ∆V . The charge inside is ρ ∆V , so the conservation of charge can alsobe written as

∇ · j = − ∂ρ∂t

(13.8)

(Gauss’ mathematics once again!).

13-3 The magnetic force on a currentNow we are ready to ﬁnd the force on a current-carrying wire in a magneticﬁeld. The current consists of charged particles moving with the velocity v alongthe wire. Each charge feels a transverse forceF = qv × B

(Fig. 13-5a). If there are N such charges per unit volume, the number in a smallvolume ∆V of the wire is N ∆V . The total magnetic force ∆F on the volume ∆Vis the sum of the forces on the individual charges, that is,

Fig. 13-4. The integral of j · n over aclosed surface is negative the rate of changeof the total charge Q inside.

∆F = (N ∆V )(qv × B).

But N qv is just j, so

∆F = j × B ∆V(Fig. 13-5b). The force per unit volume is j × B.

(13.9)

13-2

Fig. 13-5. The magnetic force on acurrent-carrying wire is the sum of the forceson the individual moving charges.

If the current is uniform across a wire whose cross-sectional area is A, we maytake as the volume element a cylinder with the base area A and the length ∆L.Then(13.10)Now we can call jA the vector current I in the wire. (Its magnitude is theelectric current in the wire, and its direction is along the wire.) Then

∆F = j × BA ∆L.

∆F = I × B ∆L.

(13.11)

The force per unit length on a wire is I × B.This equation gives the important result that the magnetic force on a wire,due to the movement of charges in it, depends only on the total current, and noton the amount of charge carried by each particle—or even its sign! The magneticforce on a wire near a magnet is easily shown by observing its deﬂection when acurrent is turned on, as was described in Chapter 1 (see Fig. 1-6).

13-4 The magnetic ﬁeld of steady currents; Ampère’s lawWe have seen that there is a force on a wire in the presence of a magnetic ﬁeld,produced, say, by a magnet. From the principle that action equals reaction wemight expect that there should be a force on the source of the magnetic ﬁeld, i.e.,on the magnet, when there is a current through the wire.* There are indeed suchforces, as is seen by the deﬂection of a compass needle near a current-carryingwire. Now we know that magnets feel forces from other magnets, so that meansthat when there is a current in a wire, the wire itself generates a magnetic ﬁeld.Moving charges, then, produce a magnetic ﬁeld. We would like now to try todiscover the laws that determine how such magnetic ﬁelds are created. Thequestion is: Given a current, what magnetic ﬁeld does it make? The answer tothis question was determined experimentally by three critical experiments and abrilliant theoretical argument given by Ampère. We will pass over this interestinghistorical development and simply say that a large number of experiments havedemonstrated the validity of Maxwell’s equations. We take them as our startingpoint. If we drop the terms involving time derivatives in these equations we getthe equations of magnetostatics:

and

∇ · B = 0

c2∇ × B = j0

.

(13.12)

(13.13)

These equations are valid only if all electric charge densities are constant andall currents are steady, so that the electric and magnetic ﬁelds are not changingwith time—all of the ﬁelds are「static.」

We may remark that it is rather dangerous to think that there is such athing as a static magnetic situation, because there must be currents in order toget a magnetic ﬁeld at all—and currents can come only from moving charges.「Magnetostatics」is, therefore, an approximation. It refers to a special kindof dynamic situation with large numbers of charges in motion, which we canapproximate by a steady ﬂow of charge. Only then can we speak of a currentdensity j which does not change with time. The subject should more accuratelybe called the study of steady currents. Assuming that all ﬁelds are steady, we dropall terms in ∂E/∂t and ∂B/∂t from the complete Maxwell equations, Eqs. (2.41),and obtain the two equations (13.12) and (13.13) above. Also notice that sincethe divergence of the curl of any vector is necessarily zero, Eq. (13.13) requiresthat ∇ · j = 0. This is true, by Eq. (13.8), only if ∂ρ/∂t is zero. But that mustbe so if E is not changing with time, so our assumptions are consistent.The requirement that ∇ · j = 0 means that we may only have charges whichﬂow in paths that close back on themselves. They may, for instance, ﬂow in wires

* We will see later, however, that such assumptions are not generally correct for electromag-

netic forces!

13-3

that form complete loops—called circuits. The circuits may, of course, containgenerators or batteries that keep the charges ﬂowing. But they may not includecondensers which are charging or discharging. (We will, of course, extend thetheory later to include dynamic ﬁelds, but we want ﬁrst to take the simpler caseof steady currents.)

Now let us look at Eqs. (13.12) and (13.13) to see what they mean. Theﬁrst one says that the divergence of B is zero. Comparing it to the analogousequation in electrostatics, which says that ∇ · E = −ρ/0, we can conclude thatthere is no magnetic analog of an electric charge. There are no magnetic chargesfrom which lines of B can emerge. If we think in terms of「lines」of the vectorﬁeld B, they can never start and they never stop. Then where do they comefrom? Magnetic ﬁelds「appear」in the presence of currents; they have a curlproportional to the current density. Wherever there are currents, there are linesof magnetic ﬁeld making loops around the currents. Since lines of B do not beginor end, they will often close back on themselves, making closed loops. But therecan also be complicated situations in which the lines are not simple closed loops.But whatever they do, they never diverge from points. No magnetic charges haveever been discovered, so ∇· B = 0. This much is true not only for magnetostatics,it is always true—even for dynamic ﬁelds.The connection between the B ﬁeld and currents is contained in Eq. (13.13).Here we have a new kind of situation which is quite diﬀerent from electrostatics,where we had ∇ × E = 0. That equation meant that the line integral of E

around any closed path is zero: I

E · ds = 0.

loop

We got that result from Stokes’ theorem, which says that the integral aroundany closed path of any vector ﬁeld is equal to the surface integral of the normalcomponent of the curl of the vector (taken over any surface which has the closedloop as its periphery). Applying the same theorem to the magnetic ﬁeld vectorand using the symbols shown in Fig. 13-6, we get

Taking the curl of B from Eq. (13.13), we have

II

Γ

Z

S

B · ds =

(∇ × B) · n dS.

Z

S

B · ds = 10c2

Γ

j · n dS.

(13.14)

(13.15)

The integral over S, according to (13.5), is the total current I through thesurface S. Since for steady currents the current through S is independent ofthe shape of S, so long as it is bounded by the curve Γ, one usually speaks of「the current through the loop Γ.」We have, then, a general law: the circulationof B around any closed curve is equal to the current I through the loop, dividedby 0c2:

B · ds = Ithrough Γ

.

0c2

(13.16)

I

Γ

This law—called Ampère’s law—plays the same role in magnetostatics that Gauss’law played in electrostatics. Ampère’s law alone does not determine B fromcurrents; we must, in general, also use ∇ · B = 0. But, as we will see in thenext section, it can be used to ﬁnd the ﬁeld in special circumstances which havecertain simple symmetries.

13-5 The magnetic ﬁeld of a straight wire and of a solenoid; atomic currentsWe can illustrate the use of Ampère’s law by ﬁnding the magnetic ﬁeld neara wire. We ask: What is the ﬁeld outside a long straight wire with a cylindricalcross section? We will assume something which may not be at all evident, but13-4

Fig. 13-6. The line integral of the tangen-tial component of B is equal to the surfaceintegral of the normal component of ∇× B.

which is nevertheless true: that the ﬁeld lines of B go around the wire in closedcircles. If we make this assumption, then Ampère’s law, Eq. (13.16), tells ushow strong the ﬁeld is. From the symmetry of the problem, B has the samemagnitude at all points on a circle concentric with the wire (see Fig. 13-7). Wecan then do the line integral of B · ds quite easily; it is just the magnitude of Btimes the circumference. If r is the radius of the circle, then

I

B · ds = B · 2πr.

The total current through the loop is merely the current I in the wire, so

or

B =

1

4π0c2

B · 2πr = I

0c2 ,2Ir

.

(13.17)

The strength of the magnetic ﬁeld drops oﬀ inversely as r, the distance fromthe axis of the wire. We can, if we wish, write Eq. (13.17) in vector form.Remembering that B is at right angles both to I and to r, we have

Fig. 13-7. The magnetic ﬁeld outside of

a long wire carrying the current I.

B =

1

4π0c2

2I × er

r

.

(13.18)

We have separated out the factor 1/4π0c2, because it appears often. It is worthremembering that it is exactly 10−7 (in the mks system), since an equationlike (13.17) is used to deﬁne the unit of current, the ampere. At one meter froma current of one ampere the magnetic ﬁeld is 2 × 10−7 webers per square meter.Since a current produces a magnetic ﬁeld, it will exert a force on a nearbywire which is also carrying a current.In Chapter 1 we described a simpledemonstration of the forces between two current-carrying wires. If the wires areparallel, each is at right angles to the B ﬁeld of the other; the wires should thenbe pushed either toward or away from each other. When currents are in the samedirection, the wires attract; when the currents are moving in opposite directions,the wires repel.

Fig. 13-8. The magnetic ﬁeld of a long

solenoid.

Let’s take another example that can be analyzed by Ampère’s law if we addsome knowledge about the ﬁeld. Suppose we have a long coil of wire wound in atight spiral, as shown by the cross sections in Fig. 13-8. Such a coil is called asolenoid. We observe experimentally that when a solenoid is very long comparedwith its diameter, the ﬁeld outside is very small compared with the ﬁeld inside.Using just that fact, together with Ampère’s law, we can ﬁnd the size of the ﬁeldinside.

Since the ﬁeld stays inside (and has zero divergence), its lines must go alongparallel to the axis, as shown in Fig. 13-8. That being the case, we can useAmpère’s law with the rectangular「curve」Γ shown in the ﬁgure. This loop goesthe distance L inside the solenoid, where the ﬁeld is, say, B0, then goes at rightangles to the ﬁeld, and returns along the outside, where the ﬁeld is negligible.13-5

Fig. 13-9. The magnetic ﬁeld outside of

a solenoid.

The line integral of B for this curve is just B0L, and it must be 1/0c2 times thetotal current through Γ, which is N I if there are N turns of the solenoid in thelength L. We have

B0L = N I0c2 .

Or, letting n be the number of turns per unit length of the solenoid (that is,n = N/L), we get

B0 = nI0c2 .

(13.19)

What happens to the lines of B when they get to the end of the solenoid?Presumably, they spread out in some way and return to enter the solenoid at theother end, as sketched in Fig. 13-9. Such a ﬁeld is just what is observed outsideof a bar magnet. But what is a magnet anyway? Our equations say that Bcomes from the presence of currents. Yet we know that ordinary bars of iron(no batteries or generators) also produce magnetic ﬁelds. You might expect thatthere should be some other terms on the right-hand side of (13.12) or (13.13) torepresent「the density of magnetic iron」or some such quantity. But there is nosuch term. Our theory says that the magnetic eﬀects of iron come from someinternal currents which are already taken care of by the j term.Matter is very complex when looked at from a fundamental point of view—aswe saw when we tried to understand dielectrics. In order not to interrupt ourpresent discussion, we will wait until later to deal in detail with the interiormechanisms of magnetic materials like iron: You will have to accept, for themoment, that all magnetism is produced from currents, and that in a permanentmagnet there are permanent internal currents. In the case of iron, these currentscome from electrons spinning around their own axes. Every electron has sucha spin, which corresponds to a tiny circulating current. Of course, one electrondoesn’t produce much magnetic ﬁeld, but in an ordinary piece of matter there arebillions and billions of electrons. Normally these spin and point every which way,so that there is no net eﬀect. The miracle is that in a very few substances, likeiron, a large fraction of the electrons spin with their axes in the same direction—for iron, two electrons of each atom take part in this cooperative motion. In a barmagnet there are large numbers of electrons all spinning in the same directionand, as we will see, their total eﬀect is equivalent to a current circulating on thesurface of the bar. (This is quite analogous to what we found for dielectrics—thata uniformly polarized dielectric is equivalent to a distribution of charges on itssurface.) It is, therefore, no accident that a bar magnet is equivalent to a solenoid.

13-6 The relativity of magnetic and electric ﬁeldsWhen we said that the magnetic force on a charge was proportional to itsvelocity, you may have wondered:「What velocity? With respect to whichreference frame?」It is, in fact, clear from the deﬁnition of B given at thebeginning of this chapter that what this vector is will depend on what we chooseas a reference frame for our speciﬁcation of the velocity of charges. But we havesaid nothing about which is the proper frame for specifying the magnetic ﬁeld.It turns out that any inertial frame will do. We will also see that magnetismand electricity are not independent things—that they should always be takentogether as one complete electromagnetic ﬁeld. Although in the static caseMaxwell’s equations separate into two distinct pairs, one pair for electricity andone pair for magnetism, with no apparent connection between the two ﬁelds,nevertheless, in nature itself there is a very intimate relationship between themthat arises from the principle of relativity. Historically, the principle of relativitywas discovered after Maxwell’s equations. It was, in fact, the study of electricityand magnetism which led ultimately to Einstein’s discovery of his principle ofrelativity. But let’s see what our knowledge of relativity would tell us aboutmagnetic forces if we assume that the relativity principle is applicable—as itis—to electromagnetism.

13-6

Fig. 13-10. The interaction of a current-carrying wire and a particle with thecharge q as seen in two frames. In frame S (part a), the wire is at rest; in frame S(cid:48)(part b), the charge is at rest.

Suppose we think about what happens when a negative charge moves withvelocity v0 parallel to a current-carrying wire, as in Fig. 13-10. We will try tounderstand what goes on in two reference frames: one ﬁxed with respect to thewire, as in part (a) of the ﬁgure, and one ﬁxed with respect to the particle, as inpart (b). We will call the ﬁrst frame S and the second S0.In the S-frame, there is clearly a magnetic force on the particle. The forceis directed toward the wire, so if the charge were moving freely we would see itcurve in toward the wire. But in the S0-frame there can be no magnetic forceon the particle, because its velocity is zero. Does it, therefore, stay where it is?Would we see diﬀerent things happening in the two systems? The principle ofrelativity would say that in S0 we should also see the particle move closer to thewire. We must try to understand why that would happen.We return to our atomic description of a wire carrying a current. In a normalconductor, like copper, the electric currents come from the motion of some of thenegative electrons—called the conduction electrons—while the positive nuclearcharges and the remainder of the electrons stay ﬁxed in the body of the material.We let the charge density of the conduction electrons be ρ− and their velocityin S be v. The density of the charges at rest in S is ρ+, which must be equal tothe negative of ρ−, since we are considering an uncharged wire. There is thus noelectric ﬁeld outside the wire, and the force on the moving particle is just

F = qv0 × B.

Using the result we found in Eq. (13.18) for the magnetic ﬁeld at the distance rfrom the axis of a wire, we conclude that the force on the particle is directedtoward the wire and has the magnitude1

4π0c2 · 2Iqv0

r

F =

.

Using Eqs. (13.3) and (13.5), the current I can be written as ρ−vA, where A isthe area of a cross section of the wire. Then

F =

1

4π0c2 · 2qρ−Avv0

r

.

(13.20)

We could continue to treat the general case of arbitrary velocities for v and v0,but it will be just as good to look at the special case in which the velocity v0of the particle is the same as the velocity v of the conduction electrons. So wewrite v0 = v, and Eq. (13.20) becomes

F = q2π0

ρ−A

r

v2c2 .

(13.21)

Now we turn our attention to what happens in S0, in which the particle is atrest and the wire is running past (toward the left in the ﬁgure) with the speed v.The positive charges moving with the wire will make some magnetic ﬁeld B0 atthe particle. But the particle is now at rest, so there is no magnetic force on it!If there is any force on the particle, it must come from an electric ﬁeld. It must13-7

moving. We know that the apparent mass of a particle changes by 1/p1 − v2/c2.

be that the moving wire has produced an electric ﬁeld. But it can do that only ifit appears charged—it must be that a neutral wire with a current appears to becharged when set in motion.We must look into this. We must try to compute the charge density in thewire in S0 from what we know about it in S. One might, at ﬁrst, think theyare the same; but we know that lengths are changed between S and S0 (seeChapter 15, Vol. I), so volumes will change also. Since the charge densitiesdepend on the volume occupied by charges, the densities will change, too.Before we can decide about the charge densities in S0, we must know whathappens to the electric charge of a bunch of electrons when the charges areDoes its charge do something similar? No! Charges are always the same, movingor not. Otherwise we would not always observe that the total charge is conserved.Suppose that we take a block of material, say a conductor, which is initiallyuncharged. Now we heat it up. Because the electrons have a diﬀerent massthan the protons, the velocities of the electrons and of the protons will changeby diﬀerent amounts. If the charge of a particle depended on the speed of theparticle carrying it, in the heated block the charge of the electrons and protonswould no longer balance. A block would become charged when heated. As wehave seen earlier, a very small fractional change in the charge of all the electronsin a block would give rise to enormous electric ﬁelds. No such eﬀect has everbeen observed.

Also, we can point out that the mean speed of the electrons in matter dependson its chemical composition. If the charge on an electron changed with speed,the net charge in a piece of material would be changed in a chemical reaction.Again, a straightforward calculation shows that even a very small dependence ofcharge on speed would give enormous ﬁelds from the simplest chemical reactions.No such eﬀect is observed, and we conclude that the electric charge of a singleparticle is independent of its state of motion.

So the charge q on a particle is an invariant scalar quantity, independent ofthe frame of reference. That means that in any frame the charge density of adistribution of electrons is just proportional to the number of electrons per unitvolume. We need only worry about the fact that the volume can change becauseof the relativistic contraction of distances.We now apply these ideas to our moving wire. If we take a length L0 of thewire, in which there is a charge density ρ0 of stationary charges, it will contain thetotal charge Q = ρ0L0A0. If the same charges are observed in a diﬀerent frameto be moving with velocity v, they will all be found in a piece of the materialwith the shorter length(13.22)but with the same area A0 (since dimensions transverse to the motion areunchanged). See Fig. 13-11.If we call ρ the density of charges in the frame in which they are moving, thetotal charge Q will be ρLA0. This must also be equal to ρ0L0A0, because chargeis the same in any system, so that ρL = ρ0L0 or, from (13.22),

p1 − v2/c2,

L = L0

ρ0p1 − v2/c2 .

ρ =

(13.23)

the same charges will have the density ρ = ρ0/(cid:112)

Fig. 13-11. If a distribution of charged particles at rest has the charge density ρ0,1 − v 2/c 2 when seen from a frame

with the relative velocity v.

13-8

The charge density of a moving distribution of charges varies in the same way asthe relativistic mass of a particle.We now use this general result for the positive charge density ρ+ of our wire.These charges are at rest in frame S. In S0, however, where the wire moves withthe speed v, the positive charge density becomes

(13.24)

The negative charges are at rest in S0. So they have their「rest density」ρ0 inthis frame. In Eq. (13.23) ρ0 = ρ0−, because they have the density ρ− when thewire is at rest, i.e., in frame S, where the speed of the negative charges is v. Forthe conduction electrons, we then have thatρ0

(13.25)

ρ+p1 − v2/c2 .

ρ0+ =

ρ− =

−p1 − v2/c2 ,− = ρ−p1 − v2/c2.

or

(13.26)Now we can see why there are electric ﬁelds in S0—because in this frame the

ρ0

wire has the net charge density ρ0 given by+ + ρ0−.

ρ0 = ρ0

Using (13.24) and (13.26), we have

ρ+p1 − v2/c2

ρ0 =

+ ρ−p1 − v2/c2.

Since the stationary wire is neutral, ρ− = −ρ+, and we have

ρ0 = ρ+

p1 − v2/c2 .

v2/c2

(13.27)

Our moving wire is positively charged and will produce an electric ﬁeld E0 at theexternal stationary particle. We have already solved the electrostatic problem ofa uniformly charged cylinder. The electric ﬁeld at the distance r from the axis ofthe cylinder is

E0 = ρ0A2π0r

=

2π0rp1 − v2/c2 .

ρ+Av2/c2

(13.28)

The force on the negatively charged particle is toward the wire. We have, atleast, a force in the same direction from the two points of view; the electric forcein S0 has the same direction as the magnetic force in S.

The magnitude of the force in S0 is

F 0 = q2π0

ρ+A

r

p1 − v2/c2 .

v2/c2

(13.29)

Comparing this result for F 0 with our result for F in Eq. (13.21), we see thatthe magnitudes of the forces are almost identical from the two points of view. Infact,

Fp1 − v2/c2 ,

F 0 =

(13.30)

so for the small velocities we have been considering, the two forces are equal.We can say that for low velocities, at least, we understand that magnetism andelectricity are just「two ways of looking at the same thing.」

But things are even better than that. If we take into account the fact thatforces also transform when we go from one system to the other, we ﬁnd that thetwo ways of looking at what happens do indeed give the same physical result forany velocity.

13-9

One way of seeing this is to ask a question like: What transverse momentumwill the particle have after the force has acted for a little while? We know fromChapter 16 of Vol. I that the transverse momentum of a particle should be thesame in both the S- and S0-frames. Calling the transverse coordinate y, we wantto compare ∆py and ∆p0. Using the relativistically correct equation of motion,F = dp/dt, we expect that after the time ∆t our particle will have a transversemomentum ∆py in the S-system given by

y

∆py = F ∆t.

(13.31)

In the S0-system, the transverse momentum will be

∆p0

= F 0 ∆t0.

(13.32)We must, of course, compare ∆py and ∆p0for corresponding time intervals ∆tand ∆t0. We have seen in Chapter 15 of Vol. I that the time intervals referredto a moving particle appear to be longer than those in the rest system of theparticle. Since our particle is initially at rest in S0, we expect, for small ∆t, that

y

y

∆t0p1 − v2/c2 ,

∆t =

(13.33)

Fig. 13-12. In frame S the charge densityis zero and the current density is j. There isonly a magnetic ﬁeld. In S(cid:48), there is a chargedensity ρ(cid:48) and a diﬀerent current density j(cid:48).The magnetic ﬁeld B(cid:48) is diﬀerent and thereis an electric ﬁeld E(cid:48).

and everything comes out O.K. From (13.31) and (13.32),

∆p0∆py

y

= F 0 ∆t0F ∆t

,

which is just = 1 if we combine (13.30) and (13.33).

We have found that we get the same physical result whether we analyze themotion of a particle moving along a wire in a coordinate system at rest withrespect to the wire, or in a system at rest with respect to the particle. In the ﬁrstinstance, the force was purely「magnetic,」in the second, it was purely「electric.」The two points of view are illustrated in Fig. 13-12 (although there is still amagnetic ﬁeld B0 in the second frame, it produces no forces on the stationaryparticle).If we had chosen still another coordinate system, we would have found adiﬀerent mixture of E and B ﬁelds. Electric and magnetic forces are part ofone physical phenomenon—the electromagnetic interactions of particles. Theseparation of this interaction into electric and magnetic parts depends very muchon the reference frame chosen for the description. But a complete electromagneticdescription is invariant; electricity and magnetism taken together are consistentwith Einstein’s relativity.

Since electric and magnetic ﬁelds appear in diﬀerent mixtures if we changeour frame of reference, we must be careful about how we look at the ﬁelds Eand B. For instance, if we think of「lines」of E or B, we must not attach toomuch reality to them. The lines may disappear if we try to observe them from adiﬀerent coordinate system. For example, in system S0 there are electric ﬁeldlines, which we do not ﬁnd「moving past us with velocity v in system S.」Insystem S there are no electric ﬁeld lines at all! Therefore it makes no sense tosay something like: When I move a magnet, it takes its ﬁeld with it, so the linesof B are also moved. There is no way to make sense, in general, out of the ideaof「the speed of a moving ﬁeld line.」The ﬁelds are our way of describing whatgoes on at a point in space. In particular, E and B tell us about the forces thatwill act on a moving particle. The question「What is the force on a charge froma moving magnetic ﬁeld?」doesn’t mean anything precise. The force is given bythe values of E and B at the charge, and the formula (13.1) is not to be alteredif the source of E or B is moving (it is the values of E and B that will be alteredby the motion). Our mathematical description deals only with the ﬁelds as afunction of x, y, z, and t with respect to some inertial frame.We will later be speaking of「a wave of electric and magnetic ﬁelds travellingthrough space,」as, for instance, a light wave. But that is like speaking of a wave13-10

travelling on a string. We don’t then mean that some part of the string is movingin the direction of the wave, we mean that the displacement of the string appearsﬁrst at one place and later at another. Similarly, in an electromagnetic wave,the wave travels; but the magnitude of the ﬁelds change. So in the future whenwe—or someone else—speaks of a「moving」ﬁeld, you should think of it as just ahandy, short way of describing a changing ﬁeld in some circumstances.

13-7 The transformation of currents and chargesYou may have worried about the simpliﬁcation we made above when wetook the same velocity v for the particle and for the conduction electrons in thewire. We could go back and carry through the analysis again for two diﬀerentvelocities, but it is easier to simply notice that charge and current density arethe components of a four-vector (see Chapter 17, Vol. I).

We have seen that if ρ0 is the density of the charges in their rest frame, then

in a frame in which they have the velocity v, the density is

In that frame their current density is

ρ =

ρ0p1 − v2/c2 .ρ0vp1 − v2/c2 .

j = ρv =

Now we know that the energy U and momentum p of a particle moving with

velocity v are given by

p1 − v2/c2 ,

m0c2

m0vp1 − v2/c2 ,

p =

U =

where m0 is its rest mass. We also know that U and p form a relativistic four-vector. Since ρ and j depend on the velocity v exactly as do U and p, we canconclude that ρ and j are also the components of a relativistic four-vector. Thisproperty is the key to a general analysis of the ﬁeld of a wire moving with anyvelocity, which we would need if we want to do the problem again with thevelocity v0 of the particle diﬀerent from the velocity of the conduction electrons.If we wish to transform ρ and j to a coordinate system moving with avelocity u in the x-direction, we know that they transform just like t and (x, y, z),so that we have (see Chapter 15, Vol. I)

x − ut

p1 − u2/c2 ,

x0 =y0 = y,z0 = z,p1 − u2/c2 ,t0 = t − ux/c2

x

p1 − u2/c2= jx − uρj0j0= jy,j0= jz,p1 − u2/c2 .ρ0 = ρ − ujx/c2

y

z

(13.34)

(13.35)

With these equations we can relate charges and currents in one frame to thosein another. Taking the charges and currents in either frame, we can solve theelectromagnetic problem in that frame by using our Maxwell equations. Theresult we obtain for the motions of particles will be the same no matter whichframe we choose. We will return at a later time to the relativistic transformationsof the electromagnetic ﬁelds.

13-8 Superposition; the right-hand ruleWe will conclude this chapter by making two further points regarding the

subject of magnetostatics. First, our basic equations for the magnetic ﬁeld,

∇ · B = 0,

∇ × B = j/c20,

13-11

are linear in B and j. That means that the principle of superposition also appliesto magnetic ﬁelds. The ﬁeld produced by two diﬀerent steady currents is thesum of the individual ﬁelds from each current acting alone. Our second remarkconcerns the right-hand rules which we have encountered (such as the right-handrule for the magnetic ﬁeld produced by a current). We have also observed thatthe magnetization of an iron magnet is to be understood from the spin of theelectrons in the material. The direction of the magnetic ﬁeld of a spinning electronis related to its spin axis by the same right-hand rule. Because B is determinedby a「handed」rule—involving either a cross product or a curl—it is called anaxial vector. (Vectors whose direction in space does not depend on a reference toa right or left hand are called polar vectors. Displacement, velocity, force, and E,for example, are polar vectors.)Physically observable quantities in electromagnetism are not, however, right-(or left-) handed. Electromagnetic interactions are symmetrical under reﬂection(see Chapter 52, Vol. I). Whenever magnetic forces between two sets of currents arecomputed, the result is invariant with respect to a change in the hand convention.Our equations lead, independently of the right-hand convention, to the end resultthat parallel currents attract, or that currents in opposite directions repel. (Tryworking out the force using「left-hand rules.」) An attraction or repulsion is apolar vector. This happens because in describing any complete interaction, weuse the right-hand rule twice—once to ﬁnd B from currents, again to ﬁnd theforce this B produces on a second current. Using the right-hand rule twice isthe same as using the left-hand rule twice. If we were to change our conventionsto a left-hand system all our B ﬁelds would be reversed, but all forces—or,what is perhaps more relevant, the observed accelerations of objects—would beunchanged.

Although physicists have recently found to their surprise that all the laws ofnature are not always invariant for mirror reﬂections, the laws of electromagnetismdo have such a basic symmetry.

13-12

14-1 The vector potential14-2 The vector potential of known

currents

14-3 A straight wire14-4 A long solenoid14-5 The ﬁeld of a small loop; the

magnetic dipole

14-6 The vector potential of a circuit14-7 The law of Biot and Savart

14

The Magnetic Field in Various Situations

14-1 The vector potentialIn

this chapter we continue our discussion of magnetic ﬁelds associated withsteady currents—the subject of magnetostatics. The magnetic ﬁeld is related toelectric currents by our basic equations

∇ · B = 0,c2∇ × B = j0

.

(14.1)

(14.2)

We want now to solve these equations mathematically in a general way, that is,without requiring any special symmetry or intuitive guessing. In electrostatics,we found that there was a straightforward procedure for ﬁnding the ﬁeld whenthe positions of all electric charges are known: One simply works out the scalarpotential φ by taking an integral over the charges—as in Eq. (4.25). Then if onewants the electric ﬁeld, it is obtained from the derivatives of φ. We will now showthat there is a corresponding procedure for ﬁnding the magnetic ﬁeld B if weknow the current density j of all moving charges.In electrostatics we saw that (because the curl of E was always zero) it waspossible to represent E as the gradient of a scalar ﬁeld φ. Now the curl of Bis not always zero, so it is not possible, in general, to represent it as a gradient.However, the divergence of B is always zero, and this means that we can alwaysrepresent B as the curl of another vector ﬁeld. For, as we saw in Section 2-8,the divergence of a curl is always zero. Thus we can always relate B to a ﬁeldwe will call A by(14.3)

B = ∇ × A.

Or, by writing out the components,

Bx = (∇ × A)x = ∂Az∂yBy = (∇ × A)y = ∂Ax∂zBz = (∇ × A)z = ∂Ay∂x

− ∂Ay∂z− ∂Az∂x− ∂Ax∂y

,

,

.

(14.4)

Writing B = ∇ × A guarantees that Eq. (14.1) is satisﬁed, since, necessarily,

∇ · B = ∇ · (∇ × A) = 0.

The ﬁeld A is called the vector potential.You will remember that the scalar potential φ was not completely speciﬁed byits deﬁnition. If we have found φ for some problem, we can always ﬁnd anotherpotential φ0 that is equally good by adding a constant:

φ0 = φ + C.

The new potential φ0 gives the same electric ﬁelds, since the gradient ∇C is zero;φ0 and φ represent the same physics.Similarly, we can have diﬀerent vector potentials A which give the samemagnetic ﬁelds. Again, because B is obtained from A by diﬀerentiation, adding aconstant to A doesn’t change anything physical. But there is even more latitude14-1

for A. We can add to A any ﬁeld which is the gradient of some scalar ﬁeld,without changing the physics. We can show this as follows. Suppose we havean A that gives correctly the magnetic ﬁeld B for some real situation, and askin what circumstances some other new vector potential A0 will give the sameﬁeld B if substituted into (14.3). Then A and A0 must have the same curl:

Therefore

B = ∇ × A0 = ∇ × A.

∇ × A0 − ∇ × A = ∇ × (A0 − A) = 0.

But if the curl of a vector is zero it must be the gradient of some scalar ﬁeld,say ψ, so A0 − A = ∇ψ. That means that if A is a satisfactory vector potentialfor a problem then, for any ψ, at all,

A0 = A + ∇ψ

(14.5)

will be an equally satisfactory vector potential, leading to the same ﬁeld B.It is usually convenient to take some of the「latitude」out of A by arbitrarilyplacing some other condition on it (in much the same way that we found itconvenient—often—to choose to make the potential φ zero at large distances).We can, for instance, restrict A by choosing arbitrarily what the divergence of Amust be. We can always do that without aﬀecting B. This is because althoughA0 and A have the same curl, and give the same B, they do not need to havethe same divergence. In fact, ∇ · A0 = ∇ · A + ∇2ψ, and by a suitable choiceof ψ we can make ∇ · A0 anything we wish.What should we choose for ∇ · A? The choice should be made to get thegreatest mathematical convenience and will depend on the problem we are doing.For magnetostatics, we will make the simple choice

∇ · A = 0.

(14.6)

(Later, when we take up electrodynamics, we will change our choice.) Our completedeﬁnition* of A is then, for the moment, ∇ × A = B and ∇ · A = 0.To get some experience with the vector potential, let’s look ﬁrst at what it isfor a uniform magnetic ﬁeld B0. Taking our z-axis in the direction of B0, wemust have

Bx = ∂Az∂yBy = ∂Ax∂zBz = ∂Ay∂x

− ∂Ay∂z− ∂Az∂x− ∂Ax∂y

= 0,

= 0,

= B0.

(14.7)

By inspection, we see that one possible solution of these equations is

Ay = xB0,

Ax = 0,

Az = 0.

Or we could equally well take

Ax = −yB0,

Ay = 0,

Az = 0.

Still another solution is a linear combination of the two:

Ax = − 1

(14.8)It is clear that for any particular ﬁeld B, the vector potential A is not unique;there are many possibilities.

Az = 0.

2 yB0,

Ay = 1

2 xB0,

* Our deﬁnition still does not uniquely determine A. For a unique speciﬁcation we wouldalso have to say something about how the ﬁeld A behaves on some boundary, or at largedistances. It is sometimes convenient, for example, to choose a ﬁeld which goes to zero at largedistances.

14-2

Fig. 14-1. A uniform magnetic ﬁeld Bin the z-direction corresponds to a vectorpotential A that rotates about the z-axis,with the magnitude A = Br (cid:48)/2 (r (cid:48)is thedisplacement from the z-axis).

The third solution, Eq. (14.8), has some interesting properties. Since thex-component is proportional to −y and the y-component is proportional to +x,A must be at right angles to the vector from the z-axis, which we will call r0 (the「prime」is to remind us that it is not the vector displacement from the origin).

Also, the magnitude of A is proportional topx2 + y2 and, hence, to r0. So A

can be simply written (for our uniform ﬁeld) as2 B0 × r0.

(14.9)The vector potential A has the magnitude B0r0/2 and rotates about the z-axis asshown in Fig. 14-1. If, for example, the B ﬁeld is the axial ﬁeld inside a solenoid,then the vector potential circulates in the same sense as do the currents of thesolenoid.

The vector potential for a uniform ﬁeld can be obtained in another way. Thecirculation of A on any closed loop Γ can be related to the surface integralof ∇ × A by Stokes’ theorem, Eq. (3.38):

A = 1

A · ds =

(∇ × A) · n da.

(14.10)

But the integral on the right is equal to the ﬂux of B through the loop, so

A · ds =

B · n da.

(14.11)

inside Γ

So the circulation of A around any loop is equal to the ﬂux of B through theloop. If we take a circular loop, of radius r0 in a plane perpendicular to a uniformﬁeld B, the ﬂux is just

πr02B.

If we choose our origin on an axis of symmetry, so that we can take A ascircumferential and a function only of r0, the circulation will be

Z

inside Γ

Z

I

Γ

I

Γ

I

We get, as before,

A · ds = 2πr0A = πr02B.

A = Br02 .

In the example we have just given, we have calculated the vector potential fromthe magnetic ﬁeld, which is opposite to what one normally does. In complicatedproblems it is usually easier to solve for the vector potential, and then determinethe magnetic ﬁeld from it. We will now show how this can be done.

14-2 The vector potential of known currentsSince B is determined by currents, so also is A. We want now to ﬁnd A in

terms of the currents. We start with our basic equation (14.2):

which means, of course, that

c2∇ × B = j0

,

c2∇ × (∇ × A) = j0

.

This equation is for magnetostatics what the equation

was for electrostatics.

∇ · ∇φ = − ρ0

(14.12)

(14.13)

14-3

Fig. 14-2. The vector potential A atpoint 1 is given by an integral over the cur-rent elements j dV at all points 2.

Our equation (14.12) for the vector potential looks even more like that for φ

if we rewrite ∇ × (∇ × A) using the vector identity Eq. (2.58):

(14.14)Since we have chosen to make ∇ · A = 0 (and now you see why), Eq. (14.12)becomes

∇ × (∇ × A) = ∇(∇ · A) − ∇2A.

This vector equation means, of course, three equations:

∇2Ax = − jx0c2 ,

∇2Ay = − jy0c2 ,

∇2Az = − jz0c2 .

And each of these equations is mathematically identical to

∇2A = − j

0c2 .

∇2φ = − ρ0

.

All we have learned about solving for potentials when ρ is known can be used forsolving for each component of A when j is known!We have seen in Chapter 4 that a general solution for the electrostaticequation (14.17) is

(14.15)

(14.16)

(14.17)

(14.19)

So we know immediately that a general solution for Ax is

and similarly for Ay and Az. (Figure 14-2 will remind you of our conventions forr12 and dV2.) We can combine the three solutions in the vector form

,

(14.18)

.

r12

Z ρ(2) dV2Z jx(2) dV2Z j(2) dV2

r12

,

r12

1

1

φ(1) = 14π0

Ax(1) =

4π0c2

A(1) =

4π0c2

(You can verify if you wish, by direct diﬀerentiation of components, that thisintegral for A satisﬁes ∇ · A = 0 so long as ∇ · j = 0, which, as we saw, musthappen for steady currents.)We have, then, a general method for ﬁnding the magnetic ﬁeld of steadycurrents. The principle is: the x-component of vector potential arising from acurrent density j is the same as the electric potential φ that would be producedby a charge density ρ equal to jx/c2—and similarly for the y- and z-components.(This principle works only with components in ﬁxed directions. The「radial」component of A does not come in the same way from the「radial」componentof j, for example.) So from the vector current density j, we can ﬁnd A usingEq. (14.19)—that is, we ﬁnd each component of A by solving three imaginaryelectrostatic problems for the charge distributions ρ1 = jx/c2, ρ2 = jy/c2,and ρ3 = jz/c2. Then we get B by taking various derivatives of A to obtain ∇×A.It’s a little more complicated than electrostatics, but the same idea. We will nowillustrate the theory by solving for the vector potential in a few special cases.

14-3 A straight wireFor our ﬁrst example, we will again ﬁnd the ﬁeld of a straight wire—which wesolved in the last chapter by using Eq. (14.2) and some arguments of symmetry.We take a long straight wire of radius a, carrying the steady current I. Unlikethe charge on a conductor in the electrostatic case, a steady current in a wireis uniformly distributed throughout the cross section of the wire. If we chooseour coordinates as shown in Fig. 14-3, the current density vector j has only az-component. Its magnitude is

inside the wire, and zero outside.

jz = Iπa2

(14.20)

14-4

Since jx and jy are both zero, we have immediately

Ax = 0,

Ay = 0.

To get Az we can use our solution for the electrostatic potential φ of a wire with auniform charge density ρ = jz/c2. For points outside an inﬁnite charged cylinder,the electrostatic potential is

where r0 =px2 + y2 and λ is the charge per unit length, πa2ρ. So Az must be

φ = − λ2π0

ln r0,

Az = − πa2jz2π0c2

ln r0

for points outside a long wire carrying a uniform current. Since πa2jz = I, wecan also write

Az = − I

2π0c2

ln r0

(14.21)

Now we can ﬁnd B from (14.4). There are only two of the six derivatives

that are not zero. We get

Bx = − I

2π0c2

By =

I

2π0c2

∂∂y

∂∂x

ln r0 = − I

2π0c2

ln r0 =

I

2π0c2

yr02 ,xr02 ,

Bz = 0.

(14.22)

(14.23)

We get the same result as before: B circles around the wire, and has the magnitude

B =

1

4π0c2

2Ir0 .

(14.24)

14-4 A long solenoidNext, we consider again the inﬁnitely long solenoid with a circumferentialcurrent on the surface of nI per unit length. (We imagine there are n turns ofwire per unit length, carrying the current I, and we neglect the slight pitch ofthe winding.)Just as we have deﬁned a「surface charge density」σ, we deﬁne here a「surfacecurrent density」J equal to the current per unit length on the surface of thesolenoid (which is, of course, just the average j times the thickness of the thinwinding). The magnitude of J is, here, nI. This surface current (see Fig. 14-4)has the components:

Jx = −J sin φ,

Jy = J cos φ,

Jz = 0.

Now we must ﬁnd A for such a current distribution.First, we wish to ﬁnd Ax for points outside the solenoid. The result is thesame as the electrostatic potential outside a cylinder with a surface charge density

σ = σ0 sin φ,

with σ0 = −J/c2. We have not solved such a charge distribution, but we have donesomething similar. This charge distribution is equivalent to two solid cylinders ofcharge, one positive and one negative, with a slight relative displacement of theiraxes in the y-direction. The potential of such a pair of cylinders is proportionalto the derivative with respect to y of the potential of a single uniformly charged14-5

Fig. 14-3. A long cylindrical wire alongthe z-axis with a uniform current density j.

Fig. 14-4. A long solenoid with a surface

current density J.

cylinder. We could work out the constant of proportionality, but let’s not worryabout it for the moment.

The potential of a cylinder of charge is proportional to ln r0; the potential of

the pair is then

So we know that

φ ∝ ∂ln r0

∂y

= yr02 .

Ax = −K

yr02 ,

where K is some constant. Following the same argument, we would ﬁnd

Ay = K

xr02 .

Although we said before that there was no magnetic ﬁeld outside a solenoid,we ﬁnd now that there is an A-ﬁeld which circulates around the z-axis, as inFig. 14-4. The question is: Is its curl zero?

(14.25)

(14.26)

Clearly, Bx and By are zero, and

(cid:19)(cid:18)x(cid:18) 1r02r02 − 2x2r04

(cid:18)− ∂−Kyr02∂y+ 1r02 − 2y2r04

(cid:19)(cid:19)

= 0.

Bz = ∂∂x

K

= K

So the magnetic ﬁeld outside a very long solenoid is indeed zero, even thoughthe vector potential is not.

We can check our result against something else we know: The circulation ofthe vector potential around the solenoid should be equal to the ﬂux of B insidethe coil (Eq. 14.11). The circulation is A·2πr0 or, since A = K/r0, the circulationis 2πK. Notice that it is independent of r0. That is just as it should be if thereis no B outside, because the ﬂux is just the magnitude of B inside the solenoidtimes πa2. It is the same for all circles of radius r0 > a. We have found in thelast chapter that the ﬁeld inside is nI/0c2, so we can determine the constant K:

or

2πK = πa2 nI0c2 ,

K = nIa220c2 .

So the vector potential outside has the magnitude

(14.27)

1A = nIa2r0 ,20c2and is always perpendicular to the vector r0.We have been thinking of a solenoidal coil of wire, but we would producethe same ﬁelds if we rotated a long cylinder with an electrostatic charge on thesurface. If we have a thin cylindrical shell of radius a with a surface charge σ,rotating the cylinder makes a surface current J = σv, where v = aω is the velocityof the surface charge. There will then be a magnetic ﬁeld B = σaω/0c2 insidethe cylinder.Now we can raise an interesting question. Suppose we put a short piece ofwire W perpendicular to the axis of the cylinder, extending from the axis out tothe surface, and fastened to the cylinder so that it rotates with it, as in Fig. 14-5.This wire is moving in a magnetic ﬁeld, so the v × B forces will cause the endsof the wire to be charged (they will charge up until the E-ﬁeld from the chargesjust balances the v × B force). If the cylinder has a positive charge, the end ofthe wire at the axis will have a negative charge. By measuring the charge on theend of the wire, we could measure the speed of rotation of the system. We wouldhave an「angular-velocity meter」!

14-6

Fig. 14-5. A rotating charged cylinderproduces a magnetic ﬁeld inside. A shortradial wire rotating with the cylinder hascharges induced on its ends.

But are you wondering:「What if I put myself in the frame of reference of therotating cylinder? Then there is just a charged cylinder at rest, and I know thatthe electrostatic equations say there will be no electric ﬁelds inside, so there willbe no force pushing charges to the center. So something must be wrong.」Butthere is nothing wrong. There is no「relativity of rotation.」A rotating system isnot an inertial frame, and the laws of physics are diﬀerent. We must be sure to useequations of electromagnetism only with respect to inertial coordinate systems.It would be nice if we could measure the absolute rotation of the earth withsuch a charged cylinder, but unfortunately the eﬀect is much too small to observeeven with the most delicate instruments now available.

14-5 The ﬁeld of a small loop; the magnetic dipoleLet’s use the vector-potential method to ﬁnd the magnetic ﬁeld of a smallloop of current. As usual, by「small」we mean simply that we are interested inthe ﬁelds only at distances large compared with the size of the loop. It will turnout that any small loop is a「magnetic dipole.」That is, it produces a magneticﬁeld like the electric ﬁeld from an electric dipole.

Fig. 14-6. A rectangular loop of wire with the current I.

What is the magnetic ﬁeld at P ? (R (cid:29) a and R (cid:29) b.)

Fig. 14-7. The distribution of jx in the

current loop of Fig. 14-6.

We take ﬁrst a rectangular loop, and choose our coordinates as shown inFig. 14-6. There are no currents in the z-direction, so Az is zero. Thereare currents in the x-direction on the two sides of length a. In each leg, thecurrent density (and current) is uniform. So the solution for Ax is just like theelectrostatic potential from two charged rods (see Fig. 14-7). Since the rods haveopposite charges, their electric potential at large distances would be just thedipole potential (Section 6-5). At the point P in Fig. 14-6, the potential wouldbe

(14.28)where p is the dipole moment of the charge distribution. The dipole moment, inthis case, is the total charge on one rod times the separation between them:

,

φ = 14π0

p · eRR2

(14.29)The dipole moment points in the negative y-direction, so the cosine of the anglebetween R and p is −y/R (where y is the coordinate of P). So we have

p = λab.

λabR2We get Ax simply by replacing λ by I/c2:

φ = − 14π0

yR

.

By the same reasoning,

Ax = − Iab4π0c2

yR3 .

Ay = Iab4π0c2

xR3 .

(14.30)

(14.31)

14-7

Again, Ay is proportional to x and Ax is proportional to −y, so the vectorpotential (at large distances) goes in circles around the z-axis, circulating in thesame sense as I in the loop, as shown in Fig. 14-8.The strength of A is proportional to Iab, which is the current times the areaof the loop. This product is called the magnetic dipole moment (or, often, just「magnetic moment」) of the loop. We represent it by µ:

(14.32)The vector potential of a small plane loop of any shape (circle, triangle, etc.) isalso given by Eqs. (14.30) and (14.31) provided we replace Iab by

µ = Iab.

µ = I · (area of the loop).

(14.33)

We leave the proof of this to you.

We can put our equation in vector form if we deﬁne the direction of thevector µ to be the normal to the plane of the loop, with a positive sense givenby the right-hand rule (Fig. 14-8). Then we can write

A =

1

4π0c2

µ × RR3

=

1

4π0c2

µ × eR

R2

.

(14.34)

We have still to ﬁnd B. Using (14.33) and (14.34), together with (14.4), we

Fig. 14-8. The vector potential of a smallcurrent loop at the origin (in the xy-plane);a magnetic dipole ﬁeld.

get

Bx = − ∂∂z(where by ··· we mean µ/4π0c2),

µ

4π0c2

= ··· 3xzR5

xR3

(14.35)

(14.36)

(cid:19)

(cid:18)(cid:18)

By = ∂∂zBz = ∂∂x= −···

(cid:19)

= ··· 3yz(cid:18)R5 ,−··· y(cid:19)R3

−··· yR3

(cid:19)··· x− ∂(cid:18) 1R3∂yR3 − 3z2

R5

.

The components of the B-ﬁeld behave exactly like those of the E-ﬁeld fora dipole oriented along the z-axis. (See Eqs. (6.14) and (6.15); also Fig. 6-4.)That’s why we call the loop a magnetic dipole. The word「dipole」is slightlymisleading when applied to a magnetic ﬁeld because there are no magnetic「poles」that correspond to electric charges. The magnetic「dipole ﬁeld」is not producedby two「charges,」but by an elementary current loop.It is curious, though, that starting with completely diﬀerent laws, ∇·E = ρ/0and ∇ × B = j/0c2, we can end up with the same kind of a ﬁeld. Why shouldthat be? It is because the dipole ﬁelds appear only when we are far away fromall charges or currents. So through most of the relevant space the equations forE and B are identical: both have zero divergence and zero curl. So they givethe same solutions. However, the sources whose conﬁguration we summarize bythe dipole moments are physically quite diﬀerent—in one case, it’s a circulatingcurrent; in the other, a pair of charges, one above and one below the plane of theloop for the corresponding ﬁeld.

14-6 The vector potential of a circuitWe are often interested in the magnetic ﬁelds produced by circuits of wire inwhich the diameter of the wire is very small compared with the dimensions ofthe whole system. In such cases, we can simplify the equations for the magneticﬁeld. For a thin wire we can write our volume element as

dV = S ds

14-8

where S is the cross-sectional area of the wire and ds is the element of distancealong the wire. In fact, since the vector ds is in the same direction as j, asshown in Fig. 14-9 (and we can assume that j is constant across any given crosssection), we can write a vector equation:

(14.37)But jS is just what we call the current I in a wire, so our integral for the vectorpotential (14.19) becomes

j dV = jS ds.

Z I ds2

r12

A(1) =

1

4π0c2

(14.38)

Fig. 14-9. For a ﬁne wire j dV is the

same as I ds.

Fig. 14-10. The magnetic ﬁeld of a wirecan be obtained from an integral around thecircuit.

(see Fig. 14-10). (We assume that I is the same throughout the circuit.Ifthere are several branches with diﬀerent currents, we should, of course, use theappropriate I for each branch.)solving the corresponding electrostatic problems.

Again, we can ﬁnd the ﬁelds from (14.38) either by integrating directly or by

14-7 The law of Biot and SavartIn studying electrostatics we found that the electric ﬁeld of a known charge

distribution could be obtained directly with an integral, Eq. (4.16):

Z ρ(2)e12 dV2

.

r212

E(1) = 14π0

As we have seen, it is usually more work to evaluate this integral—there arereally three integrals, one for each component—than to do the integral for thepotential and take its gradient.

There is a similar integral which relates the magnetic ﬁeld to the currents.We already have an integral for A, Eq. (14.19); we can get an integral for B bytaking the curl of both sides:

B(1) = ∇ × A(1) = ∇ ×

(14.39)

(cid:20)

1

4π0c2

Z j(2) dV2

(cid:21)

.

r12

Now we must be careful: The curl operator means taking the derivatives of A(1),that is, it operates only on the coordinates (x1, y1, z1). We can move the ∇× op-erator inside the integral sign if we remember that it operates only on variableswith the subscript 1, which of course, appear only in

r12 = [(x1 − x2)2 + (y1 − y2)2 + (z1 − z2)2]1/2.

(14.40)

We have, for the x-component of B,

Bx = ∂Az∂y11

− ∂Ay∂z1

Z (cid:20)Z (cid:20)

jz

=4π0c2= − 14π0c2

(cid:18) 1

(cid:19)

∂∂y1r12y1 − y2r312

jz

− jy

∂∂z1z1 − z2r312

− jy

(cid:18) 1(cid:21)

r12

dV2.

(cid:19)(cid:21)

dV2

(14.41)

The quantity in brackets is just the negative of the x-component of

Corresponding results will be found for the other components, so we have

j × r12

r312

r212

= j × e12Z j(2) × e12

r212

B(1) =

1

4π0c2

dV2.

(14.42)

14-9

The integral gives B directly in terms of the known currents. The geometryinvolved is the same as that shown in Fig. 14-2.If the currents exist only in circuits of small wires we can, as in the last section,immediately do the integral across the wire, replacing j dV by I ds, where ds isan element of length of the wire. Then, using the symbols in Fig. 14-10,

Z Ie12 × ds2

r212

B(1) = − 14π0c2

.

(14.43)

(The minus sign appears because we have reversed the order of the cross product.)This equation for B is called the Biot-Savart law, after its discoverers. It givesa formula for obtaining directly the magnetic ﬁeld produced by wires carryingcurrents.

You may wonder:「What is the advantage of the vector potential if we canﬁnd B directly with a vector integral? After all, A also involves three integrals!」Because of the cross product, the integrals for B are usually more complicated,as is evident from Eq. (14.41). Also, since the integrals for A are like those ofelectrostatics, we may already know them. Finally, we will see that in moreadvanced theoretical matters (in relativity, in advanced formulations of the laws ofmechanics, like the principle of least action to be discussed later, and in quantummechanics) the vector potential plays an important role.

14-10

15

The Vector Potential

15-1 The forces on a current loop; energy of a dipoleIn

the last chapter we studied the magnetic ﬁeld produced by a small rectan-gular current loop. We found that it is a dipole ﬁeld, with the dipole momentgiven by

(15.1)where I is the current and A is the area of the loop. The direction of the momentis normal to the plane of the loop, so we can also write

µ = IA,

µ = IAn,

where n is the unit normal to the area A.

A current loop—or magnetic dipole—not only produces magnetic ﬁelds, butwill also experience forces when placed in the magnetic ﬁeld of other currents.We will look ﬁrst at the forces on a rectangular loop in a uniform magnetic ﬁeld.Let the z-axis be along the direction of the ﬁeld, and the plane of the loop beplaced through the y-axis, making the angle θ with the xy-plane as in Fig. 15-1.Then the magnetic moment of the loop—which is normal to its plane—will makethe angle θ with the magnetic ﬁeld.

Since the currents are opposite on opposite sides of the loop, the forces arealso opposite, so there is no net force on the loop (when the ﬁeld is uniform).Because of forces on the two sides marked 1 and 2 in the ﬁgure, however, thereis a torque which tends to rotate the loop about the y-axis. The magnitude ofthese forces F1 and F2 is

Their moment arm is

so the torque is

F1 = F2 = IBb.

a sin θ,

τ = Iab B sin θ,

15-1 The forces on a current loop;

energy of a dipole

15-2 Mechanical and electrical

energies

15-3 The energy of steady currents15-4 B versus A15-5 The vector potential and

quantum mechanics

15-6 What is true for statics is false for

dynamics

or, since Iab is the magnetic moment of the loop,

τ = µB sin θ.The torque can be written in vector notation:τ = µ × B.

(15.2)

Although we have only shown that the torque is given by Eq. (15.2) in one ratherspecial case, the result is right for a small loop of any shape, as we will see. Thesame kind of relationship holds for the torque of an electric dipole in an electricﬁeld:

τ = p × E.

We now ask about the mechanical energy of our current loop. Since thereis a torque, the energy evidently depends on the orientation. The principle ofvirtual work says that the torque is the rate of change of energy with angle, sowe can write

dU = τ dθ.

15-1

Fig. 15-1. A rectangular loop carrying thecurrent I sits in a uniform ﬁeld B (in thez-direction). The torque on the loop is τ =µ × B, where the magnetic moment µ =Iab.

Setting τ = µB sin θ, and integrating, we can write for the energy

U = −µB cos θ + a constant.

(15.3)(The sign is negative because the torque tries to line up the moment with theﬁeld; the energy is lowest when µ and B are parallel.)For reasons which we will discuss later, this energy is not the total energyof a current loop. (We have, for one thing, not taken into account the energyrequired to maintain the current in the loop.) We will, therefore, call this energyUmech, to remind us that it is only part of the energy. Also, since we are leavingout some of the energy anyway, we can set the constant of integration equal tozero in Eq. (15.3). So we rewrite the equation:Umech = −µ · B.

(15.4)

Again, this corresponds to the result for an electric dipole:

U = −p · E.

(15.5)Now the electrostatic energy U in Eq. (15.5) is the true energy, but Umechin (15.4) is not the real energy. It can, however, be used in computing forces,by the principle of virtual work, supposing that the current in the loop—or atleast µ—is kept constant.We can show for our rectangular loop that Umech also corresponds to themechanical work done in bringing the loop into the ﬁeld. The total force on theloop is zero only in a uniform ﬁeld; in a nonuniform ﬁeld there are net forces ona current loop. In putting the loop into a region with a ﬁeld, we must have gonethrough places where the ﬁeld was not uniform, and so work was done. To makethe calculation simple, we shall imagine that the loop is brought into the ﬁeldwith its moment pointing along the ﬁeld. (It can be rotated to its ﬁnal positionafter it is in place.)

Imagine that we want to move the loop in the x-direction—toward a regionof stronger ﬁeld—and that the loop is oriented as shown in Fig. 15-2. We startsomewhere where the ﬁeld is zero and integrate the force times the distance aswe bring the loop into the ﬁeld.

Fig. 15-2. A loop is carried along the x-direction through the ﬁeld B, at right anglesto x.

First, let’s compute the work done on each side separately and then take thesum (rather than adding the forces before integrating). The forces on sides 3and 4 are at right angles to the direction of motion, so no work is done on them.The force on side 2 is IbB(x) in the x-direction, and to get the work done againstthe magnetic forces we must integrate this from some x where the ﬁeld is zero,say at x = −∞, to x2, its present position:

(15.6)

(15.7)

15-2

W2 = −

F2 dx = −Ib

B(x) dx.

Similarly, the work done against the forces on side 1 is

W1 = −

F1 dx = Ib

B(x) dx.

Z x2Z x1

−∞

−∞

Z x2Z x1

−∞

−∞

To ﬁnd each integral, we need to know how B(x) depends on x. But notice thatside 1 follows along right behind side 2, so that its integral includes most of thework done on side 2. In fact, the sum of (15.6) and (15.7) is just

W = −Ib

B(x) dx.

(15.8)

Z x2

x1

But if we are in a region where B is nearly the same on both sides 1 and 2, we

can write the integral asZ x2

B(x) dx = (x2 − x1)B = aB,

x1

where B is the ﬁeld at the center of the loop. The total mechanical energy wehave put in is(15.9)

Umech = W = −Iab B = −µB.

The result agrees with the energy we took for Eq. (15.4).

We would, of course, have gotten the same result if we had added the forceson the loop before integrating to ﬁnd the work. If we let B1 be the ﬁeld at side 1and B2 be the ﬁeld at side 2, then the total force in the x-direction is

Fx = Ib(B2 − B1).

If the loop is「small,」that is, if B2 and B1 are not too diﬀerent, we can write

So the force is

B2 = B1 + ∂B∂x

∆x = B1 + ∂B∂x

a.

Fx = Iab

.

(15.10)

The total work done on the loop by external forces is

−

Fx dx = −Iab

dx = −IabB,

Z x

−∞

∂B∂x

Z ∂B

∂x

which is again just −µB. Only now we see why it is that the force on a smallcurrent loop is proportional to the derivative of the magnetic ﬁeld, as we wouldexpect from

Fx ∆x = −∆Umech = −∆(−µ · B).

(15.11)Our result, then, is that even though Umech = −µ · B may not include allthe energy of a system—it is a fake kind of energy—it can still be used with theprinciple of virtual work to ﬁnd the forces on steady current loops.

15-2 Mechanical and electrical energiesWe want now to show why the energy Umech discussed in the previous sectionis not the correct energy associated with steady currents—that it does not keeptrack of the total energy in the world. We have, indeed, emphasized that it canbe used like the energy, for computing forces from the principle of virtual work,provided that the current in the loop (and all other currents) do not change.Let’s see why all this works.Imagine that the loop in Fig. 15-2 is moving in the +x-direction and take thez-axis in the direction of B. The conduction electrons in side 2 will experiencea force along the wire, in the y-direction. But because of their ﬂow—as anelectric current—there is a component of their motion in the same direction asthe force. Each electron is, therefore, having work done on it at the rate Fyvy,where vy, is the component of the electron velocity along the wire. We will callthis work done on the electrons electrical work. Now it turns out that if theloop is moving in a uniform ﬁeld, the total electrical work is zero, since positivework is done on some parts of the loop and an equal amount of negative work is15-3

done on other parts. But this is not true if the circuit is moving in a nonuniformﬁeld—then there will be a net amount of work done on the electrons. In general,this work would tend to change the ﬂow of the electrons, but if the current isbeing held constant, energy must be absorbed or delivered by the battery orother source that is keeping the current steady. This energy was not includedwhen we computed Umech in Eq. (15.9), because our computations included onlythe mechanical forces on the body of the wire.You may be thinking: But the force on the electrons depends on how fastthe wire is moved; perhaps if the wire is moved slowly enough this electricalenergy can be neglected. It is true that the rate at which the electrical energy isdelivered is proportional to the speed of the wire, but the total energy deliveredis proportional also to the time that this rate goes on. So the total electricalenergy is proportional to the velocity times the time, which is just the distancemoved. For a given distance moved in a ﬁeld the same amount of electrical workis done.

Let’s consider a segment of wire of unit length carrying the current I andmoving in a direction perpendicular to itself and to a magnetic ﬁeld B with thespeed vwire. Because of the current the electrons will have a drift velocity vdriftalong the wire. The component of the magnetic force on each electron in thedirection of the drift is qevwireB. So the rate at which electrical work is beingdone is F vdrift = (qevwireB)vdrift. If there are N conduction electrons in the unitlength of the wire, the total rate at which electrical work is being done is

dUelect

dt

= N qevwireBvdrift.

But N qevdrift = I, the current in the wire, so

dUelect

dt

= IvwireB.

Now since the current is held constant, the forces on the conduction electronsdo not cause them to accelerate; the electrical energy is not going into theelectrons but into the source that is keeping the current constant.

But notice that the force on the wire is IB, so IBvwire is also the rate ofmechanical work done on the wire, dUmech/dt = IBvwire. We conclude that themechanical work done on the wire is just equal to the electrical work done onthe current source, so the energy of the loop is a constant!total force on each charge in the wire is

This is not a coincidence, but a consequence of the law we already know. The

The rate at which work is done is

F = q(E + v × B).

v · F = q[v · E + v · (v × B)].

(15.12)

If there are no electric ﬁelds we have only the second term, which is always zero.We shall see later that changing magnetic ﬁelds produce electric ﬁelds, so ourreasoning applies only to moving wires in steady magnetic ﬁelds.How is it then that the principle of virtual work gives the right answer?Because we still have not taken into account the total energy of the world. Wehave not included the energy of the currents that are producing the magneticﬁeld we start out with.Suppose we imagine a complete system such as that drawn in Fig. 15-3(a),in which we are moving our loop with the current I1 into the magnetic ﬁeld B1produced by the current I2 in a coil. Now the current I1 in the loop will also beproducing some magnetic ﬁeld B2 at the coil. If the loop is moving, the ﬁeld B2will be changing. As we shall see in the next chapter, a changing magnetic ﬁeldgenerates an E-ﬁeld; and this E-ﬁeld will do work on the charges in the coil.This energy must also be included in our balance sheet of the total energy.

15-4

Fig. 15-3. Finding the energy of a small loop in a magnetic ﬁeld.

We could wait until the next chapter to ﬁnd out about this new energy term,but we can also see what it will be if we use the principle of relativity in thefollowing way. When we are moving the loop toward the stationary coil we knowthat its electrical energy is just equal and opposite to the mechanical work done. So

Umech + Uelect(loop) = 0.

Suppose now we look at what is happening from a diﬀerent point of view, inwhich the loop is at rest, and the coil is moved toward it. The coil is then movinginto the ﬁeld produced by the loop. The same arguments would give that

Umech + Uelect(coil) = 0.

The mechanical energy is the same in the two cases because it comes from theforce between the two circuits.

The sum of the two equations gives

2Umech + Uelect(loop) + Uelect(coil) = 0.

The total energy of the whole system is, of course, the sum of the two electricalenergies plus the mechanical energy taken only once. So we have

Utotal = Uelect(loop) + Uelect(coil) + Umech = −Umech.

(15.13)The total energy of the world is really the negative of Umech. If we want the

true energy of a magnetic dipole, for example, we should write

Utotal = +µ · B.

It is only if we make the condition that all currents are constant that we canuse only a part of the energy, Umech (which is always the negative of the trueenergy), to ﬁnd the mechanical forces. In a more general problem, we must becareful to include all energies.

We have seen an analogous situation in electrostatics. We showed that theenergy of a capacitor is equal to Q2/2C. When we use the principle of virtualwork to ﬁnd the force between the plates of the capacitor, the change in energyis equal to Q2/2 times the change in 1/C. That is,= − Q22

∆U = Q2

(15.14)

∆CC2 .

(cid:18) 1

(cid:19)

C

2 ∆

Now suppose that we were to calculate the work done in moving two conductorssubject to the diﬀerent condition that the voltage between them is held constant.Then we can get the right answers for force from the principle of virtual work if wedo something artiﬁcial. Since Q = CV , the real energy is 12 CV 2. But if we deﬁnean artiﬁcial energy equal to − 12 CV 2, then the principle of virtual work can be usedto get forces by setting the change in the artiﬁcial energy equal to the mechanicalwork, provided that we insist that the voltage V be held constant. Then

(cid:18)

(cid:19)

∆Umech = ∆

− CV 22

= − V 2

2 ∆C,

(15.15)15-5

which is the same as Eq. (15.14). We get the correct result even though we areneglecting the work done by the electrical system to keep the voltage constant.Again, this electrical energy is just twice as big as the mechanical energy andof the opposite sign.

Thus if we calculate artiﬁcially, disregarding the fact that the source of thepotential has to do work to maintain the voltages constant, we get the rightanswer. It is exactly analogous to the situation in magnetostatics.

15-3 The energy of steady currentsWe can now use our knowledge that Utotal = −Umech to ﬁnd the true energyof steady currents in magnetic ﬁelds. We can begin with the true energy of asmall current loop. Calling Utotal just U, we write

U = µ · B.

(15.16)

Although we calculated this energy for a plane rectangular loop, the same resultholds for a small plane loop of any shape.

We can ﬁnd the energy of a circuit of any shape by imagining that it is madeup of small current loops. Say we have a wire in the shape of the loop Γ ofFig. 15-4. We ﬁll in this curve with the surface S, and on the surface mark out alarge number of small loops, each of which can be considered plane. If we let thecurrent I circulate around each of the little loops, the net result will be the sameas a current around Γ, since the currents will cancel on all lines internal to Γ.Physically, the system of little currents is indistinguishable from the originalcircuit. The energy must also be the same, and so is just the sum of the energiesof the little loops.

If the area of each little loop is ∆a, its energy is I∆aBn, where Bn is the

component normal to ∆a. The total energy is

U =XZ

IBn ∆a.

Z

Z

I

S

Going to the limit of inﬁnitesimal loops, the sum becomes an integral, and

U = I

Bn da = I

B · n da,

(15.17)

where n is the unit normal to da.using Stokes’ theorem,

If we set B = ∇ × A, we can connect the surface integral to a line integral,

I

Γ

I

circuit

(∇ × A) · n da = I

A · ds,

(15.18)

where ds is the line element along Γ. So we have the energy for a circuit of anyshape:

U = I

A · ds,

(15.19)

In this expression A refers, of course, to the vector potential due to those currents(other than the I in the wire) which produce the ﬁeld B at the wire.Now any distribution of steady currents can be imagined to be made up ofﬁlaments that run parallel to the lines of current ﬂow. For each pair of suchcircuits, the energy is given by (15.19), where the integral is taken around onecircuit, using the vector potential A from the other circuit. For the total energywe want the sum of all such pairs. If, instead of keeping track of the pairs, wetake the complete sum over all the ﬁlaments, we would be counting the energytwice (we saw a similar eﬀect in electrostatics), so the total energy can be written

Z

U = 12

j · A dV.

(15.20)

15-6

Fig. 15-4. The energy of a large loop ina magnetic ﬁeld can be considered as thesum of energies of smaller loops.

Z

This formula corresponds to the result we found for the electrostatic energy:

U = 12

ρφ dV.

(15.21)

So we may if we wish think of A as a kind of potential for currents in magne-tostatics. Unfortunately, this idea is not too useful, because it is true only forstatic ﬁelds. In fact, neither of the equations (15.20) and (15.21) gives the correctenergy when the ﬁelds change with time.

15-4 B versus AIn this section we would like to discuss the following questions: Is the vectorpotential merely a device which is useful in making calculations—as the scalarpotential is useful in electrostatics—or is the vector potential a「real」ﬁeld? Isn’tthe magnetic ﬁeld the「real」ﬁeld, because it is responsible for the force on amoving particle? First we should say that the phrase「a real ﬁeld」is not verymeaningful. For one thing, you probably don’t feel that the magnetic ﬁeld is very「real」anyway, because even the whole idea of a ﬁeld is a rather abstract thing.You cannot put out your hand and feel the magnetic ﬁeld. Furthermore, the valueof the magnetic ﬁeld is not very deﬁnite; by choosing a suitable moving coordinatesystem, for instance, you can make a magnetic ﬁeld at a given point disappear.What we mean here by a「real」ﬁeld is this: a real ﬁeld is a mathematicalfunction we use for avoiding the idea of action at a distance. If we have a chargedparticle at the position P, it is aﬀected by other charges located at some distancefrom P. One way to describe the interaction is to say that the other chargesmake some「condition」—whatever it may be—in the environment at P. If weknow that condition, which we describe by giving the electric and magnetic ﬁelds,then we can determine completely the behavior of the particle—with no furtherreference to how those conditions came about.

In other words, if those other charges were altered in some way, but theconditions at P that are described by the electric and magnetic ﬁeld at P remainthe same, then the motion of the charge will also be the same. A「real」ﬁeld isthen a set of numbers we specify in such a way that what happens at a pointdepends only on the numbers at that point. We do not need to know any moreabout what’s going on at other places. It is in this sense that we will discusswhether the vector potential is a「real」ﬁeld.

You may be wondering about the fact that the vector potential is not unique—that it can be changed by adding the gradient of any scalar with no change atall in the forces on particles. That has not, however, anything to do with thequestion of reality in the sense that we are talking about. For instance, themagnetic ﬁeld is in a sense altered by a relativity change (as are also E and A).But we are not worried about what happens if the ﬁeld can be changed in thisway. That doesn’t really make any diﬀerence; that has nothing to do with thequestion of whether the vector potential is a proper「real」ﬁeld for describingmagnetic eﬀects, or whether it is just a useful mathematical tool.

We should also make some remarks on the usefulness of the vector potential A.We have seen that it can be used in a formal procedure for calculating themagnetic ﬁelds of known currents, just as φ can be used to ﬁnd electric ﬁelds. Inelectrostatics we saw that φ was given by the scalar integral

Z ρ(2)

r12

Z ρ(2)e12

r212

φ(1) = 14π0

E(1) = 14π0

dV2.

(15.22)

From this φ, we get the three components of E by three diﬀerential operations.This procedure is usually easier to handle than evaluating the three integrals inthe vector formula

dV2.

(15.23)

First, there are three integrals; and second, each integral is in general somewhatmore diﬃcult.

15-7

The advantages are much less clear for magnetostatics. The integral for A is

already a vector integral:

Z j(2) dV2

r12

A(1) =

1

4π0c2

,

(15.24)

which is, of course, three integrals. Also, when we take the curl of A to get B,we have six derivatives to do and combine by pairs. It is not immediately obviouswhether in most problems this procedure is really any easier than computing Bdirectly from

Z j(2) × e12

r212

B(1) =

1

4π0c2

dV2.

(15.25)

Using the vector potential is often more diﬃcult for simple problems for thefollowing reason. Suppose we are interested only in the magnetic ﬁeld B at onepoint, and that the problem has some nice symmetry—say we want the ﬁeld at apoint on the axis of a ring of current. Because of the symmetry, we can easilyget B by doing the integral of Eq. (15.25). If, however, we were to ﬁnd A ﬁrst,we would have to compute B from derivatives of A, so we must know what A isat all points in the neighborhood of the point of interest. And most of these pointsare oﬀ the axis of symmetry, so the integral for A gets complicated. In the ringproblem, for example, we would need to use elliptic integrals. In such problems,A is clearly not very useful. It is true that in many complex problems it is easierto work with A, but it would be hard to argue that this ease of technique wouldjustify making you learn about one more vector ﬁeld.We have introduced A because it does have an important physical signiﬁcance.Not only is it related to the energies of currents, as we saw in the last section, butit is also a「real」physical ﬁeld in the sense that we described above. In classicalmechanics it is clear that we can write the force on a particle as

F = q(E + v × B),

(15.26)so that, given the forces, everything about the motion is determined. In anyregion where B = 0 even if A is not zero, such as outside a solenoid, there isno discernible eﬀect of A. Therefore for a long time it was believed that A wasnot a「real」ﬁeld. It turns out, however, that there are phenomena involvingquantum mechanics which show that the ﬁeld A is in fact a「real」ﬁeld in thesense we have deﬁned it. In the next section we will show you how that works.

15-5 The vector potential and quantum mechanicsThere are many changes in what concepts are important when we go fromclassical to quantum mechanics. We have already discussed some of them inVol. I. In particular, the force concept gradually fades away, while the conceptsof energy and momentum become of paramount importance. You rememberthat instead of particle motions, one deals with probability amplitudes whichvary in space and time. In these amplitudes there are wavelengths related tomomenta, and frequencies related to energies. The momenta and energies, whichdetermine the phases of wave functions, are therefore the important quantities inquantum mechanics. Instead of forces, we deal with the way interactions changethe wavelength of the waves. The idea of a force becomes quite secondary—if itis there at all. When people talk about nuclear forces, for example, what theyusually analyze and work with are the energies of interaction of two nucleons,and not the force between them. Nobody ever diﬀerentiates the energy to ﬁndout what the force looks like. In this section we want to describe how the vectorand scalar potentials enter into quantum mechanics. It is, in fact, just becausemomentum and energy play a central role in quantum mechanics that A and φprovide the most direct way of introducing electromagnetic eﬀects into quantumdescriptions.

We must review a little how quantum mechanics works. We will consideragain the imaginary experiment described in Chapter 37 of Vol. I, in which15-8

Fig. 15-5. An interference experiment with electrons (see

also Chapter 37 of Vol. I).

electrons are diﬀracted by two slits. The arrangement is shown again in Fig. 15-5.Electrons, all of nearly the same energy, leave the source and travel toward a wallwith two narrow slits. Beyond the wall is a「backstop」with a movable detector.The detector measures the rate, which we call I, at which electrons arrive at asmall region of the backstop at the distance x from the axis of symmetry. Therate is proportional to the probability that an individual electron that leavesthe source will reach that region of the backstop. This probability has thecomplicated-looking distribution shown in the ﬁgure, which we understand as dueto the interference of two amplitudes, one from each slit. The interference of thetwo amplitudes depends on their phase diﬀerence. That is, if the amplitudes areC1eiΦ1 and C2eiΦ2, the phase diﬀerence δ = Φ1−Φ2 determines their interferencepattern [see Eq. (29.12) in Vol. I]. If the distance between the screen and theslits is L, and if the diﬀerence in the path lengths for electrons going throughthe two slits is a, as shown in the ﬁgure, then the phase diﬀerence of the twowaves is given by

(15.27)As usual, we let λ = λ/2π, where λ is the wavelength of the space variation ofthe probability amplitude. For simplicity, we will consider only values of x muchless than L; then we can set

δ = aλ

.

and

a = xL

d

.

dλ

δ = xL

(15.28)When x is zero, δ is zero; the waves are in phase, and the probability has amaximum. When δ is π, the waves are out of phase, they interfere destructively,and the probability is a minimum. So we get the wavy function for the electronintensity.Now we would like to state the law that for quantum mechanics replacesthe force law F = qv × B. It will be the law that determines the behavior ofquantum-mechanical particles in an electromagnetic ﬁeld. Since what happensis determined by amplitudes, the law must tell us how the magnetic inﬂuencesaﬀect the amplitudes; we are no longer dealing with the acceleration of a particle.The law is the following: the phase of the amplitude to arrive via any trajectoryis changed by the presence of a magnetic ﬁeld by an amount equal to the integralof the vector potential along the whole trajectory times the charge of the particleover Planck’s constant. That is,

Magnetic change in phase = q

A · ds.

Z

trajectory

(15.29)

15-9

If there were no magnetic ﬁeld there would be a certain phase of arrival. If thereis a magnetic ﬁeld anywhere, the phase of the arriving wave is increased by theintegral in Eq. (15.29).

Although we will not need to use it for our present discussion, we mentionthat the eﬀect of an electrostatic ﬁeld is to produce a phase change given by thenegative of the time integral of the scalar potential φ:

Electric change in phase = − q

φ dt.

Z

These two expressions are correct not only for static ﬁelds, but together give thecorrect result for any electromagnetic ﬁeld, static or dynamic. This is the lawthat replaces F = q(E + v × B). We want now, however, to consider only astatic magnetic ﬁeld.Suppose that there is a magnetic ﬁeld present in the two-slit experiment. Wewant to ask for the phase of arrival at the screen of the two waves whose pathspass through the two slits. Their interference determines where the maxima inthe probability will be. We may call Φ1 the phase of the wave along trajectory (1).If Φ1(B = 0) is the phase without the magnetic ﬁeld, then when the ﬁeld isturned on the phase will be

ZZ

(1)

(2)

Φ1 = Φ1(B = 0) + q

Similarly, the phase for trajectory (2) is

Φ2 = Φ2(B = 0) + q

A · ds.

A · ds.

(15.30)

(15.31)

The interference of the waves at the detector depends on the phase diﬀerence

δ = Φ1(B = 0) − Φ2(B = 0) + q

A · ds − q

(1)

(2)

A · ds.

(15.32)

The no-ﬁeld diﬀerence we will call δ(B = 0); it is just the phase diﬀerence wehave calculated above in Eq. (15.28). Also, we notice that the two integrals canbe written as one integral that goes forward along (1) and back along (2); wecall this the closed path (1–2). So we have

Z

Z

I

δ = δ(B = 0) + q

(1–2)

A · ds.

(15.33)

This equation tells us how the electron motion is changed by the magnetic ﬁeld;with it we can ﬁnd the new positions of the intensity maxima and minima at thebackstop.

Before we do that, however, we want to raise the following interesting andimportant point. You remember that the vector potential function has somearbitrariness. Two diﬀerent vector potential functions A and A0 whose diﬀerenceis the gradient of some scalar function ∇ψ, both represent the same magneticﬁeld, since the curl of a gradient is zero. They give, therefore, the same classicalforce qv × B. If in quantum mechanics the eﬀects depend on the vector potential,which of the many possible A-functions is correct?The answer is that the same arbitrariness in A continues to exist for quantummechanics. If in Eq. (15.33) we change A to A0 = A + ∇ψ, the integral on Abecomes

I

I

I

A0 · ds =

A · ds +

∇ψ · ds.

(1–2)

(1–2)

(1–2)

The integral of ∇ψ is around the closed path (1–2), but the integral of thetangential component of a gradient on a closed path is always zero, by Stokes’theorem. Therefore both A and A0 give the same phase diﬀerences and the samequantum-mechanical interference eﬀects. In both classical and quantum theoryit is only the curl of A that matters; any choice of the function of A which hasthe correct curl gives the correct physics.

15-10

The same conclusion is evident if we use the results of Section 14-1. There wefound that the line integral of A around a closed path is the ﬂux of B throughthe path, which here is the ﬂux between paths (1) and (2). Equation (15.33) can,if we wish, be written as

δ = δ(B = 0) + q

[ﬂux of B between (1) and (2)],

(15.34)

where by the ﬂux of B we mean, as usual, the surface integral of the normal com-ponent of B. The result depends only on B, and therefore only on the curl of A.Now because we can write the result in terms of B as well as in terms of A,you might be inclined to think that the B holds its own as a「real」ﬁeld and thatthe A can still be thought of as an artiﬁcial construction. But the deﬁnition of「real」ﬁeld that we originally proposed was based on the idea that a「real」ﬁeldwould not act on a particle from a distance. We can, however, give an examplein which B is zero—or at least arbitrarily small—at any place where there issome chance to ﬁnd the particles, so that it is not possible to think of it actingdirectly on them.

You remember that for a long solenoid carrying an electric current there is aB-ﬁeld inside but none outside, while there is lots of A circulating around outside,as shown in Fig. 15-6. If we arrange a situation in which electrons are to befound only outside of the solenoid—only where there is A—there will still be aninﬂuence on the motion, according to Eq. (15.33). Classically, that is impossible.Classically, the force depends only on B; in order to know that the solenoid iscarrying current, the particle must go through it. But quantum-mechanically youcan ﬁnd out that there is a magnetic ﬁeld inside the solenoid by going aroundit—without ever going close to it!

Suppose that we put a very long solenoid of small diameter just behind thewall and between the two slits, as shown in Fig. 15-7. The diameter of thesolenoid is to be much smaller than the distance d between the two slits. In thesecircumstances, the diﬀraction of the electrons at the slit gives no appreciableprobability that the electrons will get near the solenoid. What will be the eﬀecton our interference experiment?

Fig. 15-6. The magnetic ﬁeld and vector

potential of a long solenoid.

Fig. 15-7. A magnetic ﬁeld can inﬂuence the motion of electrons even thoughit exists only in regions where there is an arbitrarily small probability of ﬁnding theelectrons.

We compare the situation with and without a current through the solenoid.If we have no current, we have no B or A and we get the original pattern ofelectron intensity at the backstop. If we turn the current on in the solenoid andbuild up a magnetic ﬁeld B inside, then there is an A outside. There is a shiftin the phase diﬀerence proportional to the circulation of A outside the solenoid,which will mean that the pattern of maxima and minima is shifted to a newposition. In fact, since the ﬂux of B inside is a constant for any pair of paths,so also is the circulation of A. For every arrival point there is the same phase15-11

change; this corresponds to shifting the entire pattern in x by a constant amount,say x0, that we can easily calculate. The maximum intensity will occur where thephase diﬀerence between the two waves is zero. Using Eq. (15.33) or Eq. (15.34)for δ and Eq. (15.28) for x, we have

I

(15.35)

(15.36)

or

x0 = − Ld

λ

q

A · ds,

(1–2)

x0 = − Ld

λ

q

[ﬂux of B between (1) and (2)].

The pattern with the solenoid in place should appear* as shown in Fig. 15-7. Atleast, that is the prediction of quantum mechanics.

Precisely this experiment has recently been done. It is a very, very diﬃcultexperiment. Because the wavelength of the electrons is so small, the apparatusmust be on a tiny scale to observe the interference. The slits must be very closetogether, and that means that one needs an exceedingly small solenoid. It turnsout that in certain circumstances, iron crystals will grow in the form of very long,microscopically thin ﬁlaments called whiskers. When these iron whiskers aremagnetized they are like a tiny solenoid, and there is no ﬁeld outside except nearthe ends. The electron interference experiment was done with such a whiskerbetween two slits, and the predicted displacement in the pattern of electrons wasobserved.

In our sense then, the A-ﬁeld is「real.」You may say:「But there was amagnetic ﬁeld.」There was, but remember our original idea—that a ﬁeld is「real」if it is what must be speciﬁed at the position of the particle in order to get themotion. The B-ﬁeld in the whisker acts at a distance. If we want to describe itsinﬂuence not as action-at-a-distance, we must use the vector potential.This subject has an interesting history. The theory we have described wasknown from the beginning of quantum mechanics in 1926. The fact that thevector potential appears in the wave equation of quantum mechanics (called theSchrödinger equation) was obvious from the day it was written. That it cannotbe replaced by the magnetic ﬁeld in any easy way was observed by one man afterthe other who tried to do so. This is also clear from our example of electronsmoving in a region where there is no ﬁeld and being aﬀected nevertheless. Butbecause in classical mechanics A did not appear to have any direct importanceand, furthermore, because it could be changed by adding a gradient, peoplerepeatedly said that the vector potential had no direct physical signiﬁcance—thatonly the magnetic and electric ﬁelds are「right」even in quantum mechanics. Itseems strange in retrospect that no one thought of discussing this experimentuntil 1956, when Bohm and Aharonov ﬁrst suggested it and made the wholequestion crystal clear. The implication was there all the time, but no one paidattention to it. Thus many people were rather shocked when the matter wasbrought up. That’s why someone thought it would be worth while to do theexperiment to see that it really was right, even though quantum mechanics, whichhad been believed for so many years, gave an unequivocal answer. It is interestingthat something like this can be around for thirty years but, because of certainprejudices of what is and is not signiﬁcant, continues to be ignored.

Now we wish to continue in our analysis a little further. We will show theconnection between the quantum-mechanical formula and the classical formula—to show why it turns out that if we look at things on a large enough scale it willlook as though the particles are acted on by a force equal to qv × the curl of A.To get classical mechanics from quantum mechanics, we need to consider casesin which all the wavelengths are very small compared with distances over whichexternal conditions, like ﬁelds, vary appreciably. We shall not prove the result ingreat generality, but only in a very simple example, to show how it works. Againwe consider the same slit experiment. But instead of putting all the magnetic

* If the ﬁeld B comes out of the plane of the ﬁgure, the ﬂux as we have deﬁned it is positive

and since q for electrons is negative, x0 is positive.

15-12

Fig. 15-8. The shift of the interference pattern due to a strip of magnetic ﬁeld.

ﬁeld in a very tiny region between the slits, we imagine a magnetic ﬁeld thatextends over a larger region behind the slits, as shown in Fig. 15-8. We will takethe idealized case where we have a magnetic ﬁeld which is uniform in a narrowstrip of width w, considered small as compared with L. (That can easily bearranged; the backstop can be put as far out as we want.) In order to calculatethe shift in phase, we must take the two integrals of A along the two trajectories(1) and (2). They diﬀer, as we have seen, merely by the ﬂux of B between thepaths. To our approximation, the ﬂux is Bwd. The phase diﬀerence for the twopaths is then

δ = δ(B = 0) + q

(15.37)We note that, to our approximation, the phase shift is independent of the angle.So again the eﬀect will be to shift the whole pattern upward by an amount ∆x.Using Eq. (15.35),

 Bwd.

∆x = − LλdUsing (15.37) for δ − δ(B = 0),

∆δ = − Lλd

[δ − δ(B = 0)].

∆x = −Lλ

q Bw.

(15.38)

Such a shift is equivalent to deﬂecting all the trajectories by the small angle α(see Fig. 15-8), where

α = ∆x

L

= − λ

 qBw.

(15.39)

Now classically we would also expect a thin strip of magnetic ﬁeld to deﬂectall trajectories through some small angle, say α0, as shown in Fig. 15-9(a). Asthe electrons go through the magnetic ﬁeld, they feel a transverse force qv × Bwhich lasts for a time w/v. The change in their transverse momentum is justequal to this impulse, so(15.40)The angular deﬂection [Fig. 15-9(b)] is equal to the ratio of this transversemomentum to the total momentum p. We get that

∆px = −qwB.

α0 = ∆px

p

= − qwBp

.

(15.41)

We can compare this result with Eq. (15.39), which gives the same quantitycomputed quantum-mechanically. But the connection between classical mechanicsand quantum mechanics is this: A particle of momentum p corresponds to a15-13

Fig. 15-9. Deﬂection of a particle due topassage through a strip of magnetic ﬁeld.

quantum amplitude varying with the wavelength λ = /p. With this equality, αand α0 are identical; the classical and quantum calculations give the same result.From the analysis we see how it is that the vector potential which appears inquantum mechanics in an explicit form produces a classical force which dependsonly on its derivatives. In quantum mechanics what matters is the interferencebetween nearby paths; it always turns out that the eﬀects depend only onhow much the ﬁeld A changes from point to point, and therefore only on thederivatives of A and not on the value itself. Nevertheless, the vector potential A(together with the scalar potential φ that goes with it) appears to give the mostdirect description of the physics. This becomes more and more apparent themore deeply we go into the quantum theory. In the general theory of quantumelectrodynamics, one takes the vector and scalar potentials as the fundamentalquantities in a set of equations that replace the Maxwell equations: E and Bare slowly disappearing from the modern expression of physical laws; they arebeing replaced by A and φ.

15-6 What is true for statics is false for dynamicsWe are now at the end of our exploration of the subject of static ﬁelds. Alreadyin this chapter we have come perilously close to having to worry about whathappens when ﬁelds change with time. We were barely able to avoid it in ourtreatment of magnetic energy by taking refuge in a relativistic argument. Evenso, our treatment of the energy problem was somewhat artiﬁcial and perhapseven mysterious, because we ignored the fact that moving coils must, in fact,produce changing ﬁelds. It is now time to take up the treatment of time-varyingﬁelds—the subject of electrodynamics. We will do so in the next chapter. First,however, we would like to emphasize a few points.

Although we began this course with a presentation of the complete and correctequations of electromagnetism, we immediately began to study some incompletepieces—because that was easier. There is a great advantage in starting with thesimpler theory of static ﬁelds, and proceeding only later to the more complicatedtheory which includes dynamic ﬁelds. There is less new material to learn all atonce, and there is time for you to develop your intellectual muscles in preparationfor the bigger task.

But there is the danger in this process that before we get to see the completestory, the incomplete truths learned on the way may become ingrained and takenas the whole truth—that what is true and what is only sometimes true willbecome confused. So we give in Table 15-1 a summary of the important formulaswe have covered, separating those which are true in general from those which aretrue for statics, but false for dynamics. This summary also shows, in part, wherewe are going, since as we treat dynamics we will be developing in detail what wemust just state here without proof.

It may be useful to make a few remarks about the table. First, you shouldnotice that the equations we started with are the true equations—we have notmisled you there. The electromagnetic force (often called the Lorentz force)F = q(E + v × B) is true. It is only Coulomb’s law that is false, to be usedonly for statics. The four Maxwell equations for E and B are also true. Theequations we took for statics are false, of course, because we left oﬀ all termswith time derivatives.Gauss’ law, ∇ · E = ρ/0, remains, but the curl of E is not zero in general.So E cannot always be equated to the gradient of a scalar—the electrostaticpotential. We will see that a scalar potential still remains, but it is a time-varying quantity that must be used together with vector potentials for a completedescription of the electric ﬁeld. The equations governing this new scalar potentialare, necessarily, also new.

We must also give up the idea that E is zero in conductors. When the ﬁeldsare changing, the charges in conductors do not, in general, have time to rearrangethemselves to make the ﬁeld zero. They are set in motion, but never reachequilibrium. The only general statement is: electric ﬁelds in conductors produce15-14

FALSE IN GENERAL (true only for statics)F = 14π0

(Coulomb’s law)

q1q2r2

∇ × E = 0

E = −∇φE(1) = 14π0

Z ρ(2)e12

r212

dV2

Table 15-1

TRUE ALWAYS

F = q(E + v × B)∇ · E = ρ0

∇ × E = − ∂B∂tE = −∇φ − ∂A∂t

(Lorentz force)

(Gauss’ law)

(Faraday’s law)

For conductors, E = 0, φ = constant. Q = CV

In a conductor, E makes currents.



c2∇ × B = j0

B(1) =

1

4π0c2

Z j(2) × e12

r212

(Ampère’s law)

dV2

(Poisson’s equation)

∇2φ = − ρ0

∇2A = − j0c2

with

∇ · A = 0

φ(1) = 14π01

A(1) =

Z ρ(2)Z j(2)

r12

dV2

4π0c2

dV2

r12

Z

U = 12

Z

j · A dV

ρφ dV + 12

The equations marked with (

) are Maxwell’s equations.



(No magnetic charges)

∇ · B = 0B = ∇ × Ac2∇ × B = j0

+ ∂E∂t

∇2φ − 1c2∇2A − 1c2

∂2φ∂t2

= − ρ0

∂2A∂t2

= − j0c2

and

with

c2∇ · A + ∂φ∂t

= 0

Z ρ(2, t0)Z j(2, t0)

r12

dV2

4π0c2

dV2

r12

and

with

φ(1, t) = 14π01

A(1, t) =

t0 = t − r12c

Z (cid:18) 02 E · E + 0c2

2 B · B

(cid:19)

dV

U =

15-15

currents. So in varying ﬁelds a conductor is not an equipotential. It also followsthat the idea of a capacitance is no longer precise.Since there are no magnetic charges, the divergence of B is always zero. So Bcan always be equated to ∇×A. (Everything doesn’t change!) But the generationof B is not only from currents; ∇ × B is proportional to the current density plusa new term ∂E/∂t. This means that A is related to currents by a new equation.It is also related to φ. If we make use of our freedom to choose ∇ · A for ourown convenience, the equations for A or φ can be arranged to take on a simpleand elegant form. We therefore make the condition that c2∇ · A = −∂φ/∂t, andthe diﬀerential equations for A or φ appear as shown in the table.The potentials A and φ can still be found by integrals over the currents andcharges, but not the same integrals as for statics. Most wonderfully, though, thetrue integrals are like the static ones, with only a small and physically appealingmodiﬁcation. When we do the integrals to ﬁnd the potentials at some point, saypoint (1) in Fig. 15-10, we must use the values of j and ρ at the point (2) at anearlier time t0 = t − r12/c. As you would expect, the inﬂuences propagate frompoint (2) to point (1) at the speed c. With this small change, one can solve forthe ﬁelds of varying currents and charges, because once we have A and φ, weget B from ∇ × A, as before, and E from −∇φ − ∂A/∂t.

Fig. 15-10. The potentials at point (1)and at the time t are given by summingthe contributions from each element of thesource at the roving point (2), using thecurrents and charges which were present atthe earlier time t − r12/c.

Finally, you will notice that some results—for example, that the energy densityin an electric ﬁeld is 0E2/2—are true for electrodynamics as well as for statics.You should not be misled into thinking that this is at all「natural.」The validityof any formula derived in the static case must be demonstrated over again for thedynamic case. A contrary example is the expression for the electrostatic energyin terms of a volume integral of ρφ. This result is true only for statics.We will consider all these matters in more detail in due time, but it willperhaps be useful to keep in mind this summary, so you will know what you canforget, and what you should remember as always true.

15-16

16

Induced Currents

16-1 Motors and generatorsThe

discovery in 1820 that there was a close connection between electricity andmagnetism was very exciting—until then, the two subjects had been considered asquite independent. The ﬁrst discovery was that currents in wires make magneticﬁelds; then, in the same year, it was found that wires carrying current in amagnetic ﬁeld have forces on them.

One of the excitements whenever there is a mechanical force is the possibilityof using it in an engine to do work. Almost immediately after their discovery,people started to design electric motors using the forces on current-carrying wires.The principle of the electromagnetic motor is shown in bare outline in Fig. 16-1.A permanent magnet—usually with some pieces of soft iron—is used to producea magnetic ﬁeld in two slots. Across each slot there is a north and south pole, asshown. A rectangular coil of copper is placed with one side in each slot. When acurrent passes through the coil, it ﬂows in opposite directions in the two slots, sothe forces are also opposite, producing a torque on the coil about the axis shown.If the coil is mounted on a shaft so that it can turn, it can be coupled to pulleysor gears and can do work.

The same idea can be used for making a sensitive instrument for electricalmeasurements. Thus the moment the force law was discovered the precision ofelectrical measurements was greatly increased. First, the torque of such a motorcan be made much greater for a given current by making the current go aroundmany turns instead of just one. Then the coil can be mounted so that it turns withvery little torque—either by supporting its shaft on very delicate jewel bearingsor by hanging the coil on a very ﬁne wire or a quartz ﬁber. Then an exceedinglysmall current will make the coil turn, and for small angles the amount of rotationwill be proportional to the current. The rotation can be measured by gluing apointer to the coil or, for the most delicate instruments, by attaching a smallmirror to the coil and looking at the shift of the image of a scale. Such instrumentsare called galvanometers. Voltmeters and ammeters work on the same principle.The same ideas can be applied on a large scale to make large motors forproviding mechanical power. The coil can be made to go around and around byarranging that the connections to the coil are reversed each half-turn by contactsmounted on the shaft. Then the torque is always in the same direction. Smalldc motors are made just this way. Larger motors, dc or ac, are often madeby replacing the permanent magnet by an electromagnet, energized from theelectrical power source.

With the realization that electric currents make magnetic ﬁelds, peopleimmediately suggested that, somehow or other, magnets might also make electricﬁelds. Various experiments were tried. For example, two wires were placedparallel to each other and a current was passed through one of them in thehope of ﬁnding a current in the other. The thought was that the magnetic ﬁeldmight in some way drag the electrons along in the second wire, giving somesuch law as「likes prefer to move alike.」With the largest available current andthe most sensitive galvanometer to detect any current, the result was negative.Large magnets next to wires also produced no observed eﬀects. Finally, Faradaydiscovered in 1840 the essential feature that had been missed—that electric eﬀectsexist only when there is something changing. If one of a pair of wires has achanging current, a current is induced in the other, or if a magnet is moved nearan electric circuit, there is a current. We say that currents are induced. This was16-1

16-1 Motors and generators16-2 Transformers and inductances16-3 Forces on induced currents16-4 Electrical technology

Fig. 16-1. Schematic outline of a simple

electromagnetic motor.

the induction eﬀect discovered by Faraday. It transformed the rather dull subjectof static ﬁelds into a very exciting dynamic subject with an enormous range ofwonderful phenomena. This chapter is devoted to a qualitative description ofsome of them. As we will see, one can quickly get into fairly complicated situationsthat are hard to analyze quantitatively in all their details. But never mind, ourmain purpose in this chapter is ﬁrst to acquaint you with the phenomena involved.We will take up the detailed analysis later.

We can easily understand one feature of magnetic induction from what wealready know, although it was not known in Faraday’s time. It comes from thev × B force on a moving charge that is proportional to its velocity in a magneticﬁeld. Suppose that we have a wire which passes near a magnet, as shown inFig. 16-2, and that we connect the ends of the wire to a galvanometer. If wemove the wire across the end of the magnet the galvanometer pointer moves.

The magnet produces some vertical magnetic ﬁeld, and when we push the wireacross the ﬁeld, the electrons in the wire feel a sideways force—at right angles tothe ﬁeld and to the motion. The force pushes the electrons along the wire. Butwhy does this move the galvanometer, which is so far from the force? Becausewhen the electrons which feel the magnetic force try to move, they push—byelectric repulsion—the electrons a little farther down the wire; they, in turn, repelthe electrons a little farther on, and so on for a long distance. An amazing thing.It was so amazing to Gauss and Weber—who ﬁrst built a galvanometer—thatthey tried to see how far the forces in the wire would go. They strung a wireall the way across their city. Mr. Gauss, at one end, connected the wires toa battery (batteries were known before generators) and Mr. Weber watchedthe galvanometer move. They had a way of signaling long distances—it wasthe beginning of the telegraph! Of course, this has nothing directly to do withinduction—it has to do with the way wires carry currents, whether the currentsare pushed by induction or not.

Now suppose in the setup of Fig. 16-2 we leave the wire alone and movethe magnet. We still see an eﬀect on the galvanometer. As Faraday discovered,moving the magnet under the wire—one way—has the same eﬀect as movingthe wire over the magnet—the other way. But when the magnet is moved, we nolonger have any v×B force on the electrons in the wire. This is the new eﬀect thatFaraday found. Today, we might hope to understand it from a relativity argument.We already understand that the magnetic ﬁeld of a magnet comes from itsinternal currents. So we expect to observe the same eﬀect if instead of a magnetin Fig. 16-2 we use a coil of wire in which there is a current. If we move the wirepast the coil there will be a current through the galvanometer, or also if we movethe coil past the wire. But there is now a more exciting thing: If we change themagnetic ﬁeld of the coil not by moving it, but by changing its current, there isagain an eﬀect in the galvanometer. For example, if we have a loop of wire neara coil, as shown in Fig. 16-3, and if we keep both of them stationary but switchoﬀ the current, there is a pulse of current through the galvanometer. When weswitch the coil on again, the galvanometer kicks in the other direction.

Whenever the galvanometer in a situation such as the one shown in Fig. 16-2,or in Fig. 16-3, has a current, there is a net push on the electrons in the wire in onedirection along the wire. There may be pushes in diﬀerent directions at diﬀerentplaces, but there is more push in one direction than another. What counts isthe push integrated around the complete circuit. We call this net integratedpush the electromotive force (abbreviated emf) in the circuit. More precisely, theemf is deﬁned as the tangential force per unit charge in the wire integrated overlength, once around the complete circuit. Faraday’s complete discovery was thatemf’s can be generated in a wire in three diﬀerent ways: by moving the wire, bymoving a magnet near the wire, or by changing a current in a nearby wire.

Let’s consider the simple machine of Fig. 16-1 again, only now, instead ofputting a current through the wire to make it turn, let’s turn the loop by anexternal force, for example by hand or by a waterwheel. When the coil rotates,its wires are moving in the magnetic ﬁeld and we will ﬁnd an emf in the circuitof the coil. The motor becomes a generator.

16-2

Fig. 16-2. Moving a wire through a magnetic ﬁeld pro-

duces a current, as shown by the galvanometer.

Fig. 16-3. A coil with current produces a currentin a second coil if the ﬁrst coil is moved or if itscurrent is changed.

The coil of the generator has an induced emf from its motion. The amount ofthe emf is given by a simple rule discovered by Faraday. (We will just state therule now and wait until later to examine it in detail.) The rule is that when themagnetic ﬂux that passes through the loop (this ﬂux is the normal componentof B integrated over the area of the loop) is changing with time, the emf is equal tothe rate of change of the ﬂux. We will refer to this as「the ﬂux rule.」You see thatwhen the coil of Fig. 16-1 is rotated, the ﬂux through it changes. At the start someﬂux goes through one way; then when the coil has rotated 180◦ the same ﬂux goesthrough the other way. If we continuously rotate the coil the ﬂux is ﬁrst positive,then negative, then positive, and so on. The rate of change of the ﬂux mustalternate also. So there is an alternating emf in the coil. If we connect the two endsof the coil to outside wires through some sliding contacts—called slip-rings—(justso the wires won’t get twisted) we have an alternating-current generator.

Or we can also arrange, by means of some sliding contacts, that after everyone-half rotation, the connection between the coil ends and the outside wires isreversed, so that when the emf reverses, so do the connections. Then the pulses ofemf will always push currents in the same direction through the external circuit.We have what is called a direct-current generator.

The machine of Fig. 16-1 is either a motor or a generator. The reciprocitybetween motors and generators is nicely shown by using two identical dc「motors」of the permanent magnet kind, with their coils connected by two copper wires.When the shaft of one is turned mechanically, it becomes a generator and drivesthe other as a motor. If the shaft of the second is turned, it becomes the generatorand drives the ﬁrst as a motor. So here is an interesting example of a new kindof equivalence of nature: motor and generator are equivalent. The quantitativeequivalence is, in fact, not completely accidental. It is related to the law ofconservation of energy.

Another example of a device that can operate either to generate emf’s or torespond to emf’s is the receiver of a standard telephone—that is, an「earphone.」The original telephone of Bell consisted of two such「earphones」connected bytwo long wires. The basic principle is shown in Fig. 16-4. A permanent magnetproduces a magnetic ﬁeld in two「yokes」of soft iron and in a thin diaphragmthat is moved by sound pressure. When the diaphragm moves, it changes theamount of magnetic ﬁeld in the yokes. Therefore a coil of wire wound around oneof the yokes will have the ﬂux through it changed when a sound wave hits the16-3

Fig. 16-4. A telephone transmitter or

receiver.

diaphragm. So there is an emf in the coil. If the ends of the coil are connectedto a circuit, a current which is an electrical representation of the sound is set up.If the ends of the coil of Fig. 16-4 are connected by two wires to anotheridentical gadget, varying currents will ﬂow in the second coil. These currents willproduce a varying magnetic ﬁeld and will make a varying attraction on the irondiaphragm. The diaphragm will wiggle and make sound waves approximatelysimilar to the ones that moved the original diaphragm. With a few bits of ironand copper the human voice is transmitted over wires!

(The modern home telephone uses a receiver like the one described but uses animproved invention to get a more powerful transmitter. It is the「carbon-buttonmicrophone,」that uses sound pressure to vary the electric current from a battery.)

16-2 Transformers and inductancesOne of the most interesting features of Faraday’s discoveries is not that anemf exists in a moving coil—which we can understand in terms of the magneticforce qv × B—but that a changing current in one coil makes an emf in a secondcoil. And quite surprisingly the amount of emf induced in the second coil isgiven by the same「ﬂux rule」: that the emf is equal to the rate of change ofthe magnetic ﬂux through the coil. Suppose that we take two coils, each woundaround separate bundles of iron sheets (these help to make stronger magneticﬁelds), as shown in Fig. 16-5. Now we connect one of the coils—coil (a)—toan alternating-current generator. The continually changing current produces acontinuously varying magnetic ﬁeld. This varying ﬁeld generates an alternatingemf in the second coil—coil (b). This emf can, for example, produce enoughpower to light an electric bulb.

The emf alternates in coil (b) at a frequency which is, of course, the same asthe frequency of the original generator. But the current in coil (b) can be largeror smaller than the current in coil (a). The current in coil (b) depends on theemf induced in it and on the resistance and inductance of the rest of its circuit.The emf can be less than that of the generator if, say, there is little ﬂux change.Or the emf in coil (b) can be made much larger than that in the generator bywinding coil (b) with many turns, since in a given magnetic ﬁeld the ﬂux throughthe coil is then greater. (Or if you prefer to look at it another way, the emf is thesame in each turn, and since the total emf is the sum of the emf’s of the separateturns, many turns in series produce a large emf.)

Such a combination of two coils—usually with an arrangement of iron sheetsto guide the magnetic ﬁelds—is called a transformer. It can「transform」one emf(also called a「voltage」) to another.There are also induction eﬀects in a single coil. For instance, in the setup inFig. 16-5 there is a changing ﬂux not only through coil (b), which lights the bulb,but also through coil (a). The varying current in coil (a) produces a varyingmagnetic ﬁeld inside itself and the ﬂux of this ﬁeld is continually changing, sothere is a self-induced emf in coil (a). There is an emf acting on any currentwhen it is building up a magnetic ﬁeld—or, in general, when its ﬁeld is changingin any way. The eﬀect is called self-inductance.When we gave「the ﬂux rule」that the emf is equal to the rate of change ofthe ﬂux linkage, we didn’t specify the direction of the emf. There is a simplerule, called Lenz’s rule, for ﬁguring out which way the emf goes: the emf triesto oppose any ﬂux change. That is, the direction of an induced emf is alwayssuch that if a current were to ﬂow in the direction of the emf, it would produce aﬂux of B that opposes the change in B that produces the emf. Lenz’s rule canbe used to ﬁnd the direction of the emf in the generator of Fig. 16-1, or in thetransformer winding of Fig. 16-3.

In particular, if there is a changing current in a single coil (or in any wire)there is a「back」emf in the circuit. This emf acts on the charges ﬂowing incoil (a) of Fig. 16-5 to oppose the change in magnetic ﬁeld, and so in the directionto oppose the change in current.It tries to keep the current constant; it isopposite to the current when the current is increasing, and it is in the direction16-4

Fig. 16-5. Two coils, wrapped aroundbundles of iron sheets, allow a generator tolight a bulb with no direct connection.

Fig. 16-6. Circuit connections for an elec-tromagnet. The lamp allows the passage ofcurrent when the switch is opened, prevent-ing the appearance of excessive emf’s.

of the current when it is decreasing. A current in a self-inductance has「inertia,」because the inductive eﬀects try to keep the ﬂow constant, just as mechanicalinertia tries to keep the velocity of an object constant.

Any large electromagnet will have a large self-inductance. Suppose that abattery is connected to the coil of a large electromagnet, as in Fig. 16-6, and thata strong magnetic ﬁeld has been built up. (The current reaches a steady valuedetermined by the battery voltage and the resistance of the wire in the coil.) Butnow suppose that we try to disconnect the battery by opening the switch. If wereally opened the circuit, the current would go to zero rapidly, and in doing so itwould generate an enormous emf. In most cases this emf would be large enoughto develop an arc across the opening contacts of the switch. The high voltagethat appears might also damage the insulation of the coil—or you, if you arethe person who opens the switch! For these reasons, electromagnets are usuallyconnected in a circuit like the one shown in Fig. 16-6. When the switch is opened,the current does not change rapidly but remains steady, ﬂowing instead throughthe lamp, being driven by the emf from the self-inductance of the coil.

16-3 Forces on induced currentsYou have probably seen the dramatic demonstration of Lenz’s rule madewith the gadget shown in Fig. 16-7. It is an electromagnet, just like coil (a) ofFig. 16-5. An aluminum ring is placed on the end of the magnet. When the coilis connected to an alternating-current generator by closing the switch, the ringﬂies into the air. The force comes, of course, from the induced currents in thering. The fact that the ring ﬂies away shows that the currents in it oppose thechange of the ﬁeld through it. When the magnet is making a north pole at itstop, the induced current in the ring is making a downward-pointing north pole.The ring and the coil are repelled just like two magnets with like poles opposite.If a thin radial cut is made in the ring the force disappears, showing that it doesindeed come from the currents in the ring.

Fig. 16-7. A conducting ring is strongly repelled by

Fig. 16-8. An electromagnet near a perfectly con-

an electromagnet with a varying current.

ducting plate.

16-5

If, instead of the ring, we place a disc of aluminum or copper across the endof the electromagnet of Fig. 16-7, it is also repelled; induced currents circulate inthe material of the disc, and again produce a repulsion.

An interesting eﬀect, similar in origin, occurs with a sheet of a perfectconductor.In a「perfect conductor」there is no resistance whatever to thecurrent. So if currents are generated in it, they can keep going forever. In fact,the slightest emf would generate an arbitrarily large current—which really meansthat there can be no emf’s at all. Any attempt to make a magnetic ﬂux gothrough such a sheet generates currents that create opposite B ﬁelds—all withinﬁnitesimal emf’s, so with no ﬂux entering.If we have a sheet of a perfect conductor and put an electromagnet next to it,when we turn on the current in the magnet, currents called eddy currents appearin the sheet, so that no magnetic ﬂux enters. The ﬁeld lines would look as shownin Fig. 16-8. The same thing happens, of course, if we bring a bar magnet neara perfect conductor. Since the eddy currents are creating opposing ﬁelds, themagnets are repelled from the conductor. This makes it possible to suspend a barmagnet in air above a sheet of perfect conductor shaped like a dish, as shown inFig. 16-9. The magnet is suspended by the repulsion of the induced eddy currentsin the perfect conductor. There are no perfect conductors at ordinary tempera-tures, but some materials become perfect conductors at low enough temperatures.For instance, below 3.8◦K tin conducts perfectly. It is called a superconductor.If the conductor in Fig. 16-8 is not quite perfect there will be some resistanceto ﬂow of the eddy currents. The currents will tend to die out and the magnetwill slowly settle down. The eddy currents in an imperfect conductor need anemf to keep them going, and to have an emf the ﬂux must keep changing. Theﬂux of the magnetic ﬁeld gradually penetrates the conductor.

In a normal conductor, there are not only repulsive forces from eddy currents,but there can also be sidewise forces. For instance, if we move a magnet sidewaysalong a conducting surface the eddy currents produce a force of drag, because theinduced currents are opposing the changing of the location of ﬂux. Such forcesare proportional to the velocity and are like a kind of viscous force.

These eﬀects show up nicely in the apparatus shown in Fig. 16-10. A squaresheet of copper is suspended on the end of a rod to make a pendulum. Thecopper swings back and forth between the poles of an electromagnet. When themagnet is turned on, the pendulum motion is suddenly arrested. As the metalplate enters the gap of the magnet, there is a current induced in the plate whichacts to oppose the change in ﬂux through the plate. If the sheet were a perfectconductor, the currents would be so great that they would push the plate outagain—it would bounce back. With a copper plate there is some resistance in theplate, so the currents at ﬁrst bring the plate almost to a dead stop as it starts toenter the ﬁeld. Then, as the currents die down, the plate slowly settles to rest inthe magnetic ﬁeld.

The nature of the eddy currents in the copper pendulum is shown in Fig. 16-11.The strength and geometry of the currents are quite sensitive to the shape of theplate. If, for instance, the copper plate is replaced by one which has several narrowslots cut in it, as shown in Fig. 16-12, the eddy-current eﬀects are drasticallyreduced. The pendulum swings through the magnetic ﬁeld with only a smallretarding force. The reason is that the currents in each section of the copperhave less ﬂux to drive them, so the eﬀects of the resistance of each loop aregreater. The currents are smaller and the drag is less. The viscous character ofthe force is seen even more clearly if a sheet of copper is placed between the polesof the magnet of Fig. 16-10 and then released. It doesn’t fall; it just sinks slowlydownward. The eddy currents exert a strong resistance to the motion—just likethe viscous drag in honey.

If, instead of dragging a conductor past a magnet, we try to rotate it in amagnetic ﬁeld, there will be a resistive torque from the same eﬀects. Alternatively,if we rotate a magnet—end over end—near a conducting plate or ring, the ringis dragged around; currents in the ring will create a torque that tends to rotatethe ring with the magnet.

16-6

Fig. 16-9. A bar magnet is suspendedabove a superconducting bowl, by the repul-sion of eddy currents.

Fig. 16-10. The braking of the pendulum

shows the forces due to eddy currents.

Fig. 16-11. The eddy currents in the

copper pendulum.

Fig. 16-12. Eddy-current eﬀects are drastically

reduced by cutting slots in the plate.

Fig. 16-13. Making a rotating magnetic ﬁeld.

A ﬁeld just like that of a rotating magnet can be made with an arrangement ofcoils such as is shown in Fig. 16-13. We take a torus of iron (that is, a ring of ironlike a doughnut) and wind six coils on it. If we put a current, as shown in part (a),through windings (1) and (4), there will be a magnetic ﬁeld in the direction shownin the ﬁgure. If we now switch the current to windings (2) and (5), the magneticﬁeld will be in a new direction, as shown in part (b) of the ﬁgure. Continuing theprocess, we get the sequence of ﬁelds shown in the rest of the ﬁgure. If the processis done smoothly, we have a「rotating」magnetic ﬁeld. We can easily get therequired sequence of currents by connecting the coils to a three-phase power line,which provides just such a sequence of currents.「Three-phase power」is madein a generator using the principle of Fig. 16-1, except that there are three loopsfastened together on the same shaft in a symmetrical way—that is, with an angleof 120◦ from one loop to the next. When the coils are rotated as a unit, the emf isa maximum in one, then in the next, and so on in a regular sequence. There aremany practical advantages of three-phase power. One of them is the possibilityof making a rotating magnetic ﬁeld. The torque produced on a conductor bysuch a rotating ﬁeld is easily shown by standing a metal ring on an insulatingtable just above the torus, as shown in Fig. 16-14. The rotating ﬁeld causes thering to spin about a vertical axis. The basic elements seen here are quite thesame as those at play in a large commercial three-phase induction motor.

Another form of induction motor is shown in Fig. 16-15. The arrangementshown is not suitable for a practical high-eﬃciency motor but will illustrate theprinciple. The electromagnet M, consisting of a bundle of laminated iron sheetswound with a solenoidal coil, is powered with alternating current from a generator.The magnet produces a varying ﬂux of B through the aluminum disc. If we havejust these two components, as shown in part (a) of the ﬁgure, we do not yet havea motor. There are eddy currents in the disc, but they are symmetric and there isno torque. (There will be some heating of the disc due to the induced currents.) Ifwe now cover only one-half of the magnet pole with an aluminum plate, as shownin part (b) of the ﬁgure, the disc begins to rotate, and we have a motor. The opera-tion depends on two eddy-current eﬀects. First, the eddy currents in the aluminumplate oppose the change of ﬂux through it, so the magnetic ﬁeld above the platealways lags the ﬁeld above that half of the pole which is not covered. This so-called16-7

Fig. 16-14. The

rotating ﬁeld ofFig. 16-13 can be used to provide torque ona conducting ring.

Fig. 16-15. A simple example of a shaded-pole induction motor.

「shaded-pole」eﬀect produces a ﬁeld which in the「shaded」region varies much likethat in the「unshaded」region except that it is delayed a constant amount in time.The whole eﬀect is as if there were a magnet only half as wide which is continuallybeing moved from the unshaded region toward the shaded one. Then the varyingﬁelds interact with the eddy currents in the disc to produce the torque on it.

16-4 Electrical technologyWhen Faraday ﬁrst made public his remarkable discovery that a changingmagnetic ﬂux produces an emf, he was asked (as anyone is asked when he discoversa new fact of nature),「What is the use of it?」All he had found was the odditythat a tiny current was produced when he moved a wire near a magnet. Of whatpossible「use」could that be? His answer was:「What is the use of a newbornbaby?」

Yet think of the tremendous practical applications his discovery has led to.What we have been describing are not just toys but examples chosen in mostcases to represent the principle of some practical machine. For instance, therotating ring in the turning ﬁeld is an induction motor. There are, of course,some diﬀerences between it and a practical induction motor. The ring has avery small torque; it can be stopped with your hand. For a good motor, thingshave to be put together more intimately: there shouldn’t be so much「wasted」magnetic ﬁeld out in the air. First, the ﬁeld is concentrated by using iron. Wehave not discussed how iron does that, but iron can make the magnetic ﬁeld tensof thousands of times stronger than copper coils alone could do. Second, the gapsbetween the pieces of iron are made small; to do that, some iron is even builtinto the rotating ring. Everything is arranged so as to get the greatest forcesand the greatest eﬃciency—that is, conversion of electrical power to mechanicalpower—until the「ring」can no longer be held still by your hand.

This problem of closing the gaps and making the thing work in the mostpractical way is engineering. It requires serious study of design problems, althoughthere are no new basic principles from which the forces are obtained. But there isa long way to go from the basic principles to a practical and economic design. Yetit is just such careful engineering design that has made possible such a tremendousthing as Boulder Dam and all that goes with it.

What is Boulder Dam? A huge river is stopped by a concrete wall. But whata wall it is! Shaped with a perfect curve that is very carefully worked out so thatthe least possible amount of concrete will hold back a whole river. It thickens atthe bottom in that wonderful shape that the artists like but that the engineerscan appreciate because they know that such thickening is related to the increaseof pressure with the depth of the water. But we are getting away from electricity.Then the water of the river is diverted into a huge pipe. That’s a nice engineer-ing accomplishment in itself. The pipe feeds the water into a「waterwheel」—ahuge turbine—and makes wheels turn. (Another engineering feat.) But why turnwheels? They are coupled to an exquisitely intricate mess of copper and iron, all16-8

twisted and interwoven. With two parts—one that turns and one that doesn’t.All a complex intermixture of a few materials, mostly iron and copper but alsosome paper and shellac for insulation. A revolving monster thing. A generator.Somewhere out of the mess of copper and iron come a few special pieces of copper.The dam, the turbine, the iron, the copper, all put there to make somethingspecial happen to a few bars of copper—an emf. Then the copper bars go a littleway and circle for several times around another piece of iron in a transformer;then their job is done.

But around that same piece of iron curls another cable of copper which hasno direct connection whatsoever to the bars from the generator; they have justbeen inﬂuenced because they passed near it—to get their emf. The transformerconverts the power from the relatively low voltages required for the eﬃcient designof the generator to the very high voltages that are best for eﬃcient transmissionof electrical energy over long cables.

And everything must be enormously eﬃcient—there can be no waste, noloss. Why? The power for a metropolis is going through. If a small fractionwere lost—one or two percent—think of the energy left behind! If one percent ofthe power were left in the transformer, that energy would need to be taken outsomehow. If it appeared as heat, it would quickly melt the whole thing. There is,of course, some small ineﬃciency, but all that is required are a few pumps whichcirculate some oil through a radiator to keep the transformer from heating up.Out of the Boulder Dam come a few dozen rods of copper—long, long, longrods of copper perhaps the thickness of your wrist that go for hundreds of miles inall directions. Small rods of copper carrying the power of a giant river. Then therods are split to make more rods . . . then to more transformers . . . sometimesto great generators which recreate the current in another form . . . sometimesto engines turning for big industrial purposes . . . to more transformers . . . thenmore splitting and spreading . . . until ﬁnally the river is spread throughout thewhole city—turning motors, making heat, making light, working gadgetry. Themiracle of hot lights from cold water over 600 miles away—all done with speciallyarranged pieces of copper and iron. Large motors for rolling steel, or tiny motorsfor a dentist’s drill. Thousands of little wheels, turning in response to the turningof the big wheel at Boulder Dam. Stop the big wheel, and all the wheels stop;the lights go out. They really are connected.

Yet there is more. The same phenomena that take the tremendous power ofthe river and spread it through the countryside, until a few drops of the riverare running the dentist’s drill, come again into the building of extremely ﬁneinstruments . . . for the detection of incredibly small amounts of current . . . for thetransmission of voices, music, and pictures . . . for computers . . . for automaticmachines of fantastic precision.

All this is possible because of carefully designed arrangements of copper andiron—eﬃciently created magnetic ﬁelds . . . blocks of rotating iron six feet indiameter whirling with clearances of 1/16 of an inch . . . careful proportions ofcopper for the optimum eﬃciency . . . strange shapes all serving a purpose, likethe curve of the dam.

If some future archaeologist uncovers Boulder Dam, we may guess that hewould admire the beauty of its curves. But also the explorers from some greatfuture civilizations will look at the generators and transformers and say:「Noticethat every iron piece has a beautifully eﬃcient shape. Think of the thought thathas gone into every piece of copper!」

This is the power of engineering and the careful design of our electricaltechnology. There has been created in the generator something which existsnowhere else in nature. It is true that there are forces of induction in otherplaces. Certainly in some places around the sun and stars there are eﬀects ofelectromagnetic induction. Perhaps also (though it’s not certain) the magneticﬁeld of the earth is maintained by an analog of an electric generator that operateson circulating currents in the interior of the earth. But nowhere have there beenpieces put together with moving parts to generate electrical power as is done inthe generator—with great eﬃciency and regularity.

16-9

You may think that designing electric generators is no longer an interestingsubject, that it is a dead subject because they are all designed. Almost perfectgenerators or motors can be taken from a shelf. Even if this were true, we canadmire the wonderful accomplishment of a problem solved to near perfection. Butthere remain as many unﬁnished problems. Even generators and transformers arereturning as problems. It is likely that the whole ﬁeld of low temperatures andsuperconductors will soon be applied to the problem of electric power distribution.With a radically new factor in the problem, new optimum designs will have tobe created. Power networks of the future may have little resemblance to those oftoday.

You can see that there is an endless number of applications and problemsthat one could take up while studying the laws of induction. The study of thedesign of electrical machinery is a life work in itself. We cannot go very far inthat direction, but we should be aware of the fact that when we have discoveredthe law of induction, we have suddenly connected our theory to an enormouspractical development. We must, however, leave that subject to the engineersand applied scientists who are interested in working out the details of particularapplications. Physics only supplies the base—the basic principles that apply,no matter what. (We have not yet completed the base, because we have yet toconsider in detail the properties of iron and of copper. Physics has something tosay about these as we will see a little later!)

Modern electrical technology began with Faraday’s discoveries. The uselessbaby developed into a prodigy and changed the face of the earth in ways itsproud father could never have imagined.

16-10

17

The Laws of Induction

