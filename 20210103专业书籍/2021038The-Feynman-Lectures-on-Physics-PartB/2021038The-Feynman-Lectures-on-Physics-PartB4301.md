28-1 The ﬁeld energy of a point chargeIn

bringing together relativity and Maxwell’s equations, we have ﬁnished ourmain work on the theory of electromagnetism. There are, of course, some detailswe have skipped over and one large area that we will be concerned with in thefuture—the interaction of electromagnetic ﬁelds with matter. But we want tostop for a moment to show you that this tremendous ediﬁce, which is such abeautiful success in explaining so many phenomena, ultimately falls on its face.When you follow any of our physics too far, you ﬁnd that it always gets into somekind of trouble. Now we want to discuss a serious trouble—the failure of theclassical electromagnetic theory. You can appreciate that there is a failure of allclassical physics because of the quantum-mechanical eﬀects. Classical mechanicsis a mathematically consistent theory; it just doesn’t agree with experience.It is interesting, though, that the classical theory of electromagnetism is anunsatisfactory theory all by itself. There are diﬃculties associated with theideas of Maxwell’s theory which are not solved by and not directly associatedwith quantum mechanics. You may say,「Perhaps there’s no use worrying aboutthese diﬃculties. Since the quantum mechanics is going to change the lawsof electrodynamics, we should wait to see what diﬃculties there are after themodiﬁcation.」However, when electromagnetism is joined to quantum mechanics,the diﬃculties remain. So it will not be a waste of our time now to look at whatthese diﬃculties are. Also, they are of great historical importance. Furthermore,you may get some feeling of accomplishment from being able to go far enoughwith the theory to see everything—including all of its troubles.

The diﬃculty we speak of is associated with the concepts of electromagneticmomentum and energy, when applied to the electron or any charged particle. Theconcepts of simple charged particles and the electromagnetic ﬁeld are in someway inconsistent. To describe the diﬃculty, we begin by doing some exerciseswith our energy and momentum concepts.

First, we compute the energy of a charged particle. Suppose we take a simplemodel of an electron in which all of its charge q is uniformly distributed on thesurface of a sphere of radius a, which we may take to be zero for the special caseof a point charge. Now let’s calculate the energy in the electromagnetic ﬁeld. Ifthe charge is standing still, there is no magnetic ﬁeld, and the energy per unitvolume is proportional to the square of the electric ﬁeld. The magnitude of theelectric ﬁeld is q/4π0r2, and the energy density is

To get the total energy, we must integrate this density over all space. Using thevolume element 4πr2 dr, the total energy, which we will call Uelec, is

q2

32π20r4 .

u = 0

2 E2 =Z

Uelec =

q2

8π0r2 dr.

This is readily integrated. The lower limit is a, and the upper limit is ∞, so

Uelec = 12

q24π0

1a

.

(28.1)

28-1

If we use the electronic charge qe for q and the symbol e2 for q2

e /4π0, then

Uelec = 12

e2a

.

(28.2)

It is all ﬁne until we set a equal to zero for a point charge—there’s the greatdiﬃculty. Because the energy of the ﬁeld varies inversely as the fourth power ofthe distance from the center, its volume integral is inﬁnite. There is an inﬁniteamount of energy in the ﬁeld surrounding a point charge.

What’s wrong with an inﬁnite energy? If the energy can’t get out, but muststay there forever, is there any real diﬃculty with an inﬁnite energy? Of course,a quantity that comes out inﬁnite may be annoying, but what really matters isonly whether there are any observable physical eﬀects. To answer that question,we must turn to something else besides the energy. Suppose we ask how theenergy changes when we move the charge. Then, if the changes are inﬁnite, wewill be in trouble.

28-2 The ﬁeld momentum of a moving chargeSuppose an electron is moving at a uniform velocity through space, assumingfor a moment that the velocity is low compared with the speed of light. Associatedwith this moving electron there is a momentum—even if the electron had nomass before it was charged—because of the momentum in the electromagneticﬁeld. We can show that the ﬁeld momentum is in the direction of the velocity vof the charge and is, for small velocities, proportional to v. For a point P at thedistance r from the center of the charge and at the angle θ with respect to theline of motion (see Fig. 28-1) the electric ﬁeld is radial and, as we have seen, themagnetic ﬁeld is v × E/c2. The momentum density, Eq. (27.21), is

g = 0E × B.

It is directed obliquely toward the line of motion, as shown in the ﬁgure, and hasthe magnitude

g = 0v

c2 E2 sin θ.

The ﬁelds are symmetric about the line of motion, so when we integrate overspace, the transverse components will sum to zero, giving a resultant momentumparallel to v. The component of g in this direction is g sin θ, which we mustintegrate over all space. We take as our volume element a ring with its planeperpendicular to v, as shown in Fig. 28-2. Its volume is 2πr2 sin θ dθ dr. Thetotal momentum is then

Z 0vc2 E2 sin2 θ 2πr2 sin θ dθ dr.

p =

Since E is independent of θ (for v (cid:28) c), we can immediately integrate over θ;

the integral isZ

Z

sin3 θ dθ = −

(1 − cos2 θ) d(cos θ) = − cos θ + cos3 θ3

.

The limits of θ are 0 and π, so the θ-integral gives merely a factor of 4/3, and

Z

p = 8π3

0vc2

E2r2 dr.

The integral (for v (cid:28) c) is the one we have just evaluated to ﬁnd the energy; itis q2/16π22

0a, and

or

vac2 ,

p = 23p = 23

q24π0e2ac2 v.

(28.3)

28-2

Fig. 28-1. The ﬁelds E and B and themomentum density g for a positive electron.For a negative electron, E and B are re-versed but g is not.

Fig. 28-2. The

element2πr 2 sin θ dθ dr used for calculating the ﬁeldmomentum.

volume

The momentum in the ﬁeld—the electromagnetic momentum—is proportionalto v. It is just what we should have for a particle with the mass equal to thecoeﬃcient of v. We can, therefore, call this coeﬃcient the electromagnetic mass,melec, and write it as

melec = 23

e2ac2 .

(28.4)

28-3 Electromagnetic massWhere does the mass come from? In our laws of mechanics we have supposedthat every object「carries」a thing we call the mass—which also means that it「carries」a momentum proportional to its velocity. Now we discover that it isunderstandable that a charged particle carries a momentum proportional to itsvelocity. It might, in fact, be that the mass is just the eﬀect of electrodynamics.The origin of mass has until now been unexplained. We have at last in thetheory of electrodynamics a grand opportunity to understand something that wenever understood before. It comes out of the blue—or rather, from Maxwell andPoynting—that any charged particle will have a momentum proportional to itsvelocity just from electromagnetic inﬂuences.

Let’s be conservative and say, for a moment, that there are two kinds ofmass—that the total momentum of an object could be the sum of a mechanicalmomentum and the electromagnetic momentum. The mechanical momentumis the「mechanical」mass, mmech, times v. In experiments where we measurethe mass of a particle by seeing how much momentum it has, or how it swingsaround in an orbit, we are measuring the total mass. We say generally that themomentum is the total mass (mmech + melec) times the velocity. So the observedmass can consist of two pieces (or possibly more if we include other ﬁelds): amechanical piece plus an electromagnetic piece. We know that there is deﬁnitelyan electromagnetic piece, and we have a formula for it. And there is the thrillingpossibility that the mechanical piece is not there at all—that the mass is allelectromagnetic.

Let’s see what size the electron must have if there is to be no mechanicalmass. We can ﬁnd out by setting the electromagnetic mass of Eq. (28.4) equalto the observed mass me of an electron. We ﬁnd

a = 23

e2mec2 .

(28.5)

The quantity

r0 = e2mec2

(28.6)is called the「classical electron radius」; it has the numerical value 2.82×10−13 cm,about one one-hundred-thousandth of the diameter of an atom.Why is r0 called the electron radius, rather than our a? Because we couldequally well do the same calculation with other assumed distributions of charges—the charge might be spread uniformly through the volume of a sphere or it might besmeared out like a fuzzy ball. For any particular assumption the factor 2/3 wouldchange to some other fraction. For instance, for a charge uniformly distributedthroughout the volume of a sphere, the 2/3 gets replaced by 4/5. Rather thanto argue over which distribution is correct, it was decided to deﬁne r0 as the「nominal」radius. Then diﬀerent theories could supply their pet coeﬃcients.Let’s pursue our electromagnetic theory of mass. Our calculation was for v (cid:28) c;what happens if we go to high velocities? Early attempts led to a certain amountof confusion, but Lorentz realized that the charged sphere would contract into aellipsoid at high velocities and that the ﬁelds would change in accordance withthe formulas (26.6) and (26.7) we derived for the relativistic case in Chapter 26.If you carry through the integrals for p in that case, you ﬁnd that for an arbitrary

velocity v, the momentum is altered by the factor 1/p1 − v2/c2:

p = 23

e2ac2

vp1 − v2/c2 .

(28.7)

28-3

In other words, the electromagnetic mass rises with velocity inversely as

p1 − v2/c2—a discovery that was made before the theory of relativity.

Early experiments were proposed to measure the changes with velocity inthe observed mass of a particle in order to determine how much of the mass wasmechanical and how much was electrical. It was believed at the time that theelectrical part would vary with velocity, whereas the mechanical part would not.But while the experiments were being done, the theorists were also at work. Soonthe theory of relativity was developed, which proposed that no matter what the

origin of the mass, it all should vary as m0/p1 − v2/c2. Equation (28.7) was

the beginning of the theory that mass depended on velocity.

Let’s now go back to our calculation of the energy in the ﬁeld, which ledto Eq. (28.2). According to the theory of relativity, the energy U will have themass U/c2; Eq. (28.2) then says that the ﬁeld of the electron should have themass

(28.8)which is not the same as the electromagnetic mass, melec, of Eq. (28.4). In fact,if we just combine Eqs. (28.2) and (28.4), we would write

m0elec = Uelecc2

= 12

e2ac2 ,

Uelec = 3

4 melecc2.

This formula was discovered before relativity, and when Einstein and othersbegan to realize that it must always be that U = mc2, there was great confusion.

28-4 The force of an electron on itselfThe discrepancy between the two formulas for the electromagnetic massis especially annoying, because we have carefully proved that the theory ofelectrodynamics is consistent with the principle of relativity. Yet the theory ofrelativity implies without question that the momentum must be the same as theenergy times v/c2. So we are in some kind of trouble; we must have made amistake. We did not make an algebraic mistake in our calculations, but we haveleft something out.

In deriving our equations for energy and momentum, we assumed the conser-vation laws. We assumed that all forces were taken into account and that anywork done and any momentum carried by other「nonelectrical」machinery wasincluded. Now if we have a sphere of charge, the electrical forces are all repulsiveand an electron would tend to ﬂy apart. Because the system has unbalancedforces, we can get all kinds of errors in the laws relating energy and momen-tum. To get a consistent picture, we must imagine that something holds theelectron together. The charges must be held to the sphere by some kind of rubberbands—something that keeps the charges from ﬂying oﬀ. It was ﬁrst pointedout by Poincaré that the rubber bands—or whatever it is that holds the electrontogether—must be included in the energy and momentum calculations. For thisreason the extra nonelectrical forces are also known by the more elegant name「the Poincaré stresses.」If the extra forces are included in the calculations, themasses obtained in two ways are changed (in a way that depends on the detailedassumptions). And the results are consistent with relativity; i.e., the mass thatcomes out from the momentum calculation is the same as the one that comesfrom the energy calculation. However, both of them contain two contributions:an electromagnetic mass and contribution from the Poincaré stresses. Only whenthe two are added together do we get a consistent theory.

It is therefore impossible to get all the mass to be electromagnetic in theway we hoped. It is not a legal theory if we have nothing but electrodynamics.Something else has to be added. Whatever you call them—「rubber bands,」or「Poincaré stresses,」or something else—there have to be other forces in nature tomake a consistent theory of this kind.

Clearly, as soon as we have to put forces on the inside of the electron, thebeauty of the whole idea begins to disappear. Things get very complicated. You28-4

would want to ask: How strong are the stresses? How does the electron shake?Does it oscillate? What are all its internal properties? And so on. It mightbe possible that an electron does have some complicated internal properties.If we made a theory of the electron along these lines, it would predict oddproperties, like modes of oscillation, which haven’t apparently been observed. Wesay「apparently」because we observe a lot of things in nature that still do notmake sense. We may someday ﬁnd out that one of the things we don’t understandtoday (for example, the muon) can, in fact, be explained as an oscillation of thePoincaré stresses. It doesn’t seem likely, but no one can say for sure. Thereare so many things about fundamental particles that we still don’t understand.Anyway, the complex structure implied by this theory is undesirable, and theattempt to explain all mass in terms of electromagnetism—at least in the waywe have described—has led to a blind alley.

We would like to think a little more about why we say we have a mass whenthe momentum in the ﬁeld is proportional to the velocity. Easy! The mass isthe coeﬃcient between momentum and velocity. But we can look at the mass inanother way: a particle has mass if you have to exert a force in order to accelerateit. So it may help our understanding if we look a little more closely at where theforces come from. How do we know that there has to be a force? Because wehave proved the law of the conservation of momentum for the ﬁelds. If we have acharged particle and push on it for awhile, there will be some momentum in theelectromagnetic ﬁeld. Momentum must have been poured into the ﬁeld somehow.Therefore there must have been a force pushing on the electron in order to get itgoing—a force in addition to that required by its mechanical inertia, a force dueto its electromagnetic interaction. And there must be a corresponding force backon the「pusher.」But where does that force come from?

Fig. 28-3. The self-force on an accelerating electron is not zero because of the retardation.(By dF we mean the force on a surface element da; by d 2F we mean the force on the surfaceelement daα from the charge on the surface element daβ.

The picture is something like this. We can think of the electron as a chargedsphere. When it is at rest, each piece of charge repels electrically each other piece,but the forces all balance in pairs, so that there is no net force. [See Fig. 28-3(a).]However, when the electron is being accelerated, the forces will no longer be inbalance because of the fact that the electromagnetic inﬂuences take time to gofrom one piece to another. For instance, the force on the piece α in Fig. 28-3(b)from a piece β on the opposite side depends on the position of β at an earliertime, as shown. Both the magnitude and direction of the force depend on themotion of the charge. If the charge is accelerating, the forces on various parts ofthe electron might be as shown in Fig. 28-3(c). When all these forces are addedup, they don’t cancel out. They would cancel for a uniform velocity, even thoughit looks at ﬁrst glance as though the retardation would give an unbalanced forceeven for a uniform velocity. But it turns out that there is no net force unless theelectron is being accelerated. With acceleration, if we look at the forces betweenthe various parts of the electron, action and reaction are not exactly equal, andthe electron exerts a force on itself that tries to hold back the acceleration. Itholds itself back by its own bootstraps.

28-5

e2ac2

¨x − 23

e2c3

e2ac4

It is possible, but diﬃcult, to calculate this self-reaction force; however, wedon’t want to go into such an elaborate calculation here. We will tell you what theresult is for the special case of relatively uncomplicated motion in one dimension,say x. Then, the self-force can be written in a series. The ﬁrst term in the seriesdepends on the acceleration ¨x, the next term is proportional to ˙˙˙x, and so on.*The result is

˙˙˙˙x + ··· ,

˙˙˙x + γ

F = α

(28.9)where α and γ are numerical coeﬃcients of the order of 1. The coeﬃcient αof the ¨x term depends on what charge distribution is assumed; if the charge isdistributed uniformly on a sphere, then α = 2/3. So there is a term, proportionalto the acceleration, which varies inversely as the radius a of the electron and agreesexactly with the value we got in Eq. (28.4) for melec. If the charge distributionis chosen to be diﬀerent, so that α is changed, the fraction 2/3 in Eq. (28.4)would be changed in the same way. The term in ˙˙˙x is independent of the assumedradius a, and also of the assumed distribution of the charge; its coeﬃcient isalways 2/3. The next term is proportional to the radius a, and its coeﬃcient γdepends on the charge distribution. You will notice that if we let the electronradius a go to zero, the last term (and all higher terms) will go to zero; the secondterm remains constant, but the ﬁrst term—the electromagnetic mass—goes toinﬁnity. And we can see that the inﬁnity arises because of the force of one part ofthe electron on another—because we have allowed what is perhaps a silly thing,the possibility of the「point」electron acting on itself.

28-5 Attempts to modify the Maxwell theoryWe would like now to discuss how it might be possible to modify Maxwell’stheory of electrodynamics so that the idea of an electron as a simple point chargecould be maintained. Many attempts have been made, and some of the theorieswere even able to arrange things so that all the electron mass was electromagnetic.But all of these theories have died. It is still interesting to discuss some of thepossibilities that have been suggested—to see the struggles of the human mind.We started out our theory of electricity by talking about the interaction ofone charge with another. Then we made up a theory of these interacting chargesand ended up with a ﬁeld theory. We believe it so much that we allow it to tellus about the force of one part of an electron on another. Perhaps the entirediﬃculty is that electrons do not act on themselves; perhaps we are making toogreat an extrapolation from the interaction of separate electrons to the idea thatan electron interacts with itself. Therefore some theories have been proposedin which the possibility that an electron acts on itself is ruled out. Then thereis no longer the inﬁnity due to the self-action. Also, there is no longer anyelectromagnetic mass associated with the particle; all the mass is back to beingmechanical, but there are new diﬃculties in the theory.

We must say immediately that such theories require a modiﬁcation of theidea of the electromagnetic ﬁeld. You remember we said at the start that theforce on a particle at any point was determined by just two quantities—E and B.If we abandon the「self-force」this can no longer be true, because if there is anelectron in a certain place, the force isn’t given by the total E and B, but byonly those parts due to other charges. So we have to keep track always of howmuch of E and B is due to the charge on which you are calculating the forceand how much is due to the other charges. This makes the theory much moreelaborate, but it gets rid of the diﬃculty of the inﬁnity.

So we can, if we want to, say that there is no such thing as the electron actingupon itself, and throw away the whole set of forces in Eq. (28.9). However, wehave then thrown away the baby with the bath! Because the second term inEq. (28.9), the term in ˙˙˙x, is needed. That force does something very deﬁnite.If you throw it away, you’re in trouble again. When we accelerate a charge,

* We are using the notation:

˙x = dx/dt, ¨x = d2x/dt2, ˙˙˙x = d3x/dt3, etc.

28-6

it radiates electromagnetic waves, so it loses energy. Therefore, to acceleratea charge, we must require more force than is required to accelerate a neutralobject of the same mass; otherwise energy wouldn’t be conserved. The rate atwhich we do work on an accelerating charge must be equal to the rate of lossof energy by radiation. We have talked about this eﬀect before—it is called theradiation resistance. We still have to answer the question: Where does the extraforce, against which we must do this work, come from? When a big antenna isradiating, the forces come from the inﬂuence of one part of the antenna currenton another. For a single accelerating electron radiating into otherwise emptyspace, there would seem to be only one place the force could come from—theaction of one part of the electron on another part.

We found back in Chapter 32 of Vol. I that an oscillating charge radiates

energy at the rate

e2(¨x)2

= 23

(28.10)Let’s see what we get for the rate of doing work on an electron against thebootstrap force of Eq. (28.9). The rate of work is the force times the velocity,or F ˙x:

dWdt

c3

.

dWdt

˙˙˙x ˙x + ···

= α

(28.11)The ﬁrst term is proportional to d ˙x2/dt, and therefore just corresponds to the rateof change of the kinetic energy 12 mv2 associated with the electromagnetic mass.The second term should correspond to the radiated power in Eq. (28.10). But itis diﬀerent. The discrepancy comes from the fact that the term in Eq. (28.11) isgenerally true, whereas Eq. (28.10) is right only for an oscillating charge. Wecan show that the two are equivalent if the motion of the charge is periodic. Todo that, we rewrite the second term of Eq. (28.11) as

¨x ˙x − 23

e2ac2

e2c3

−23

e2c3

( ˙x¨x) + 23

ddt

e2c3

(¨x)2,

which is just an algebraic transformation. If the motion of the electron is periodic,the quantity ˙x¨x returns periodically to the same value, so that if we take theaverage of its time derivative, we get zero. The second term, however, is alwayspositive (it’s a square), so its average is also positive. This term gives the network done and is just equal to Eq. (28.10).

The term in ˙˙˙x of the bootstrap force is required in order to have energyconservation in radiating systems, and we can’t throw it away. It was, in fact,one of the triumphs of Lorentz to show that there is such a force and that itcomes from the action of the electron on itself. We must believe in the idea ofthe action of the electron on itself, and we need the term in ˙˙˙x. The problem ishow we can get that term without getting the ﬁrst term in Eq. (28.9), whichgives all the trouble. We don’t know how. You see that the classical electrontheory has pushed itself into a tight corner.

There have been several other attempts to modify the laws in order tostraighten the thing out. One way, proposed by Born and Infeld, is to changethe Maxwell equations in a complicated way so that they are no longer linear.Then the electromagnetic energy and momentum can be made to come out ﬁnite.But the laws they suggest predict phenomena which have never been observed.Their theory also suﬀers from another diﬃculty we will come to later, which iscommon to all the attempts to avoid the troubles we have described.

The following peculiar possibility was suggested by Dirac. He said: Let’sadmit that an electron acts on itself through the second term in Eq. (28.9) butnot through the ﬁrst. He then had an ingenious idea for getting rid of one but notthe other. Look, he said, we made a special assumption when we took only theretarded wave solutions of Maxwell’s equations; if we were to take the advancedwaves instead, we would get something diﬀerent. The formula for the self-forcewould be

F = α

e2ac2

¨x + 23

e2c3

˙˙˙x + γ

e2ac4

˙˙˙˙x + ···

(28.12)

28-7

This equation is just like Eq. (28.9) except for the sign of the second term—andsome higher terms—of the series. [Changing from retarded to advanced waves isjust changing the sign of the delay which, it is not hard to see, is equivalent tochanging the sign of t everywhere. The only eﬀect on Eq. (28.9) is to change thesign of all the odd time derivatives.] So, Dirac said, let’s make the new rule thatan electron acts on itself by one-half the diﬀerence of the retarded and advancedﬁelds which it produces. The diﬀerence of Eqs. (28.9) and (28.12), divided bytwo, is then

F = −23

e2c3

˙˙˙x + higher terms.

In all the higher terms, the radius a appears to some positive power in thenumerator. Therefore, when we go to the limit of a point charge, we get only theone term—just what is needed. In this way, Dirac got the radiation resistanceforce and none of the inertial forces. There is no electromagnetic mass, and theclassical theory is saved—but at the expense of an arbitrary assumption aboutthe self-force.

The arbitrariness of the extra assumption of Dirac was removed, to someextent at least, by Wheeler and Feynman, who proposed a still stranger theory.They suggest that point charges interact only with other charges, but that theinteraction is half through the advanced and half through the retarded waves. Itturns out, most surprisingly, that in most situations you won’t see any eﬀects ofthe advanced waves, but they do have the eﬀect of producing just the radiationreaction force. The radiation resistance is not due to the electron acting on itself,but from the following peculiar eﬀect. When an electron is accelerated at thetime t, it shakes all the other charges in the world at a later time t0 = t + r/c(where r is the distance to the other charge), because of the retarded waves.But then these other charges react back on the original electron through theiradvanced waves, which will arrive at the time t00, equal to t0 minus r/c, which is, ofcourse, just t. (They also react back with their retarded waves too, but that justcorresponds to the normal「reﬂected」waves.) The combination of the advancedand retarded waves means that at the instant it is accelerated an oscillatingcharge feels a force from all the charges that are「going to」absorb its radiatedwaves. You see what tight knots people have gotten into in trying to get a theoryof the electron!

We’ll describe now still another kind of theory, to show the kind of thingsthat people think of when they are stuck. This is another modiﬁcation of thelaws of electrodynamics, proposed by Bopp. You realize that once you decideto change the equations of electromagnetism you can start anywhere you want.You can change the force law for an electron, or you can change the Maxwellequations (as we saw in the examples we have described), or you can make achange somewhere else. One possibility is to change the formulas that give thepotentials in terms of the charges and currents. One of our formulas has beenthat the potentials at some point are given by the current density (or charge)at each other point at an earlier time. Using our four-vector notation for thepotentials, we write

Aµ(1, t) =

1

4π0c2

Z jµ(2, t − r12/c)

r12

dV2.

(28.13)

Bopp’s beautifully simple idea is that: Maybe the trouble is in the 1/r factor inthe integral. Suppose we were to start out by assuming only that the potentialat one point depends on the charge density at any other point as some functionof the distance between the points, say as f(r12). The total potential at point (1)will then be given by the integral of jµ times this function over all space:

Z

Aµ(1, t) =

jµ(2, t − r12/c)f(r12) dV2.

That’s all. No diﬀerential equation, nothing else. Well, one more thing. We alsoask that the result should be relativistically invariant. So by「distance」we should28-8

take the invariant「distance」between two points in space-time. This distancesquared (within a sign which doesn’t matter) is

12 = c2(t1 − t2)2 − r2s212

= c2(t1 − t2)2 − (x1 − x2)2 − (y1 − y2)2 − (z1 − z2)2.

(28.14)

So, for a relativistically invariant theory, we should take some function of themagnitude of s12, or what is the same thing, some function of s212. So Bopp’stheory is that

Aµ(1, t1) =

jµ(2, t2)F(s2

12) dV2 dt2.

(28.15)

Z

(The integral must, of course, be over the four-dimensional volume dt2 dx2 dy2 dz2.)All that remains is to choose a suitable function for F. We assume only onething about F—that it is very small except when its argument is near zero—sothat a graph of F would be a curve like the one in Fig. 28-4. It is a narrowspike with a ﬁnite area centered at s2 = 0, and with a width which we can say isroughly a2. We can say, crudely, that when we calculate the potential at point (1),only those points (2) produce any appreciable eﬀect if s212 iswithin ±a2 of zero. We can indicate this by saying that F is important only for(28.16)

12 = c2(t1 − t2)2 − r2

12 = c2(t1 − t2)2 − r2s2

12 ≈ ±a2.

You can make it more mathematical if you want to, but that’s the idea.Now suppose that a is very small in comparison with the size of ordinaryobjects like motors, generators, and the like so that for normal problems r12 (cid:29) a.Then Eq. (28.16) says that charges contribute to the integral of Eq. (28.15) onlywhen t1 − t2 is in the small range

s

c(t1 − t2) ≈q(cid:18)

t1 − t2 = r12c

12 ± a2 = r12r2

1 ± a2r212

.

(cid:19)

1 ± a22r212

= r12c

± a22r12c

.

Since a2/r2

12 (cid:28) 1, the square root can be approximated by 1 ± a2/2r2

12, so

Fig. 28-4. The function F (s 2) used in

the nonlocal theory of Bopp.

What is the signiﬁcance? This result says that the only times t2 that areimportant in the integral of Aµ are those which diﬀer from the time t1, at whichwe want the potential, by the delay r12/c—with a negligible correction so longas r12 (cid:29) a. In other words, this theory of Bopp approaches the Maxwell theory—so long as we are far away from any particular charge—in the sense that it givesthe retarded wave eﬀects.We can, in fact, see approximately what the integral of Eq. (28.15) is goingto give. If we integrate ﬁrst over t2 from −∞ to +∞—keeping r12 ﬁxed—then12 is also going to go from −∞ to +∞. The integral will all come from t2’s ins2a small interval of width ∆t2 = 2 × a2/2r12c, centered at t1 − r12/c. Say thatthe function F(s2) has the value K at s2 = 0; then the integral over t2 givesapproximately Kjµ∆t2, or

We should, of course, take the value of jµ at t2 = t1 − r12/c, so that Eq. (28.15)becomes

Ka2c

jµr12

.

Z jµ(2, t1 − r12/c)

r12

dV2.

Aµ(1, t1) = Ka2

c

If we pick K = 1/4π0ca2, we are right back to the retarded potential solution ofMaxwell’s equations—including automatically the 1/r dependence! And it allcame out of the simple proposition that the potential at one point in space-timedepends on the current density at all other points in space-time, but with a28-9

weighting factor that is some narrow function of the four-dimensional distancebetween the two points. This theory again predicts a ﬁnite electromagnetic massfor the electron, and the energy and mass have the right relation for the relativitytheory. They must, because the theory is relativistically invariant from the start,and everything seems to be all right.

There is, however, one fundamental objection to this theory and to all theother theories we have described. All particles we know obey the laws of quantummechanics, so a quantum-mechanical modiﬁcation of electrodynamics has to bemade. Light behaves like photons. It isn’t 100 percent like the Maxwell theory.So the electrodynamic theory has to be changed. We have already mentionedthat it might be a waste of time to work so hard to straighten out the classicaltheory, because it could turn out that in quantum electrodynamics the diﬃcultieswill disappear or may be resolved in some other fashion. But the diﬃcultiesdo not disappear in quantum electrodynamics. That is one of the reasons thatpeople have spent so much eﬀort trying to straighten out the classical diﬃculties,hoping that if they could straighten out the classical diﬃculty and then makethe quantum modiﬁcations, everything would be straightened out. The Maxwelltheory still has the diﬃculties after the quantum mechanics modiﬁcations aremade.

The quantum eﬀects do make some changes—the formula for the mass ismodiﬁed, and Planck’s constant  appears—but the answer still comes out inﬁniteunless you cut oﬀ an integration somehow—just as we had to stop the classicalintegrals at r = a. And the answers depend on how you stop the integrals. Wecannot, unfortunately, demonstrate for you here that the diﬃculties are reallybasically the same, because we have developed so little of the theory of quantummechanics and even less of quantum electrodynamics. So you must just take ourword that the quantized theory of Maxwell’s electrodynamics gives an inﬁnitemass for a point electron.

It turns out, however, that nobody has ever succeeded in making, a self-consistent quantum theory out of any of the modiﬁed theories. Born and Infeld’sideas have never been satisfactorily made into a quantum theory. The theorieswith the advanced and retarded waves of Dirac, or of Wheeler and Feynman,have never been made into a satisfactory quantum theory. The theory of Bopphas never been made into a satisfactory quantum theory. So today, there is noknown solution to this problem. We do not know how to make a consistenttheory—including the quantum mechanics—which does not produce an inﬁnityfor the self-energy of an electron, or any point charge. And at the same time,there is no satisfactory theory that describes a non-point charge. It’s an unsolvedproblem.

In case you are deciding to rush oﬀ to make a theory in which the actionof an electron on itself is completely removed, so that electromagnetic mass isno longer meaningful, and then to make a quantum theory of it, you should bewarned that you are certain to be in trouble. There is deﬁnite experimentalevidence of the existence of electromagnetic inertia—there is evidence that someof the mass of charged particles is electromagnetic in origin.

It used to be said in the older books that since Nature will obviously notpresent us with two particles—one neutral and the other charged, but otherwisethe same—we will never be able to tell how much of the mass is electromagneticand how much is mechanical. But it turns out that Nature has been kind enoughto present us with just such objects, so that by comparing the observed mass ofthe charged one with the observed mass of the neutral one, we can tell whetherthere is any electromagnetic mass. For example, there are the neutrons andprotons. They interact with tremendous forces—the nuclear forces—whose originis unknown. However, as we have already described, the nuclear forces have oneremarkable property. So far as they are concerned, the neutron and proton areexactly the same. The nuclear forces between neutron and neutron, neutron andproton, and proton and proton are all identical as far as we can tell. Only thelittle electromagnetic forces are diﬀerent; electrically the proton and neutron areas diﬀerent as night and day. This is just what we wanted. There are two particles,28-10

identical from the point of view of the strong interactions, but diﬀerent electrically.And they have a small diﬀerence in mass. The mass diﬀerence between the protonand the neutron—expressed as the diﬀerence in the rest-energy mc2 in units ofMeV—is about 1.3 MeV, which is about 2.6 times the electron mass. The classicaltheory would then predict a radius of about 12 the classical electron radius,or about 10−13 cm. Of course, one should really use the quantum theory, but bysome strange accident, all the constants—2π’s and ’s, etc.—come out so thatthe quantum theory gives roughly the same radius as the classical theory. Theonly trouble is that the sign is wrong! The neutron is heavier than the proton.

3 to 1

Table 28-1

Particle Masses

Particle

n (neutron)p (proton)

π (π-meson)

K (K-meson)

Σ (sigma)

Charge

(electronic)

0+1

0±1

0±1

0+1−1

Mass(MeV)939.5938.2

135.0139.6

497.8493.9

1191.51189.41196.0

∆m1(MeV)

−1.3

+4.6

−3.9

−2.1+4.5

1 ∆m = (mass of charged) − (mass of neutral).

Nature has also given us several other pairs—or triplets—of particles whichappear to be exactly the same except for their electrical charge. They interactwith protons and neutrons, through the so-called「strong」interactions of thenuclear forces. In such interactions, the particles of a given kind—say the π-mesons—behave in every way like one object except for their electrical charge. InTable 28-1 we give a list of such particles, together with their measured masses.The charged π-mesons—positive or negative—have a mass of 139.6 MeV, butthe neutral π-meson is 4.6 MeV lighter. We believe that this mass diﬀerence iselectromagnetic; it would correspond to a particle radius of 3 to 4 × 10−14 cm.You will see from the table that the mass diﬀerences of the other particles areusually of the same general size.

Now the size of these particles can be determined by other methods, forinstance by the diameters they appear to have in high-energy collisions. So theelectromagnetic mass seems to be in general agreement with electromagnetictheory, if we stop our integrals of the ﬁeld energy at the same radius obtained bythese other methods. That’s why we believe that the diﬀerences do representelectromagnetic mass.

You are no doubt worried about the diﬀerent signs of the mass diﬀerencesin the table. It is easy to see why the charged ones should be heavier thanthe neutral ones. But what about those pairs like the proton and the neutron,where the measured mass comes out the other way? Well, it turns out thatthese particles are complicated, and the computation of the electromagnetic massmust be more elaborate for them. For instance, although the neutron has no netcharge, it does have a charge distribution inside it—it is only the net charge thatis zero. In fact, we believe that the neutron looks—at least sometimes—like aproton with a negative π-meson in a「cloud」around it, as shown in Fig. 28-5.Although the neutron is「neutral,」because its total charge is zero, there are stillelectromagnetic energies (for example, it has a magnetic moment), so it’s noteasy to tell the sign of the electromagnetic mass diﬀerence without a detailedtheory of the internal structure.

28-11

Fig. 28-5. A neutron may exist, at times,as a proton surrounded by a negative π-meson.

We only wish to emphasize here the following points: (1) the electromagnetictheory predicts the existence of an electromagnetic mass, but it also falls on itsface in doing so, because it does not produce a consistent theory—and the sameis true with the quantum modiﬁcations; (2) there is experimental evidence forthe existence of electromagnetic mass; and (3) all these masses are roughly thesame as the mass of an electron. So we come back again to the original idea ofLorentz—maybe all the mass of an electron is purely electromagnetic, maybe thewhole 0.511 MeV is due to electrodynamics. Is it or isn’t it? We haven’t got atheory, so we cannot say.We must mention one more piece of information, which is the most annoying.There is another particle in the world called a muon—or µ-meson—which, so faras we can tell, diﬀers in no way whatsoever from an electron except for its mass.It acts in every way like an electron: it interacts with neutrinos and with theelectromagnetic ﬁeld, and it has no nuclear forces. It does nothing diﬀerent fromwhat an electron does—at least, nothing which cannot be understood as merelya consequence of its higher mass (206.77 times the electron mass). Therefore,whenever someone ﬁnally gets the explanation of the mass of an electron, he willthen have the puzzle of where a muon gets its mass. Why? Because whatever theelectron does, the muon does the same—so the mass ought to come out the same.There are those who believe faithfully in the idea that the muon and the electronare the same particle and that, in the ﬁnal theory of the mass, the formula for themass will be a quadratic equation with two roots—one for each particle. Thereare also those who propose it will be a transcendental equation with an inﬁnitenumber of roots, and who are engaged in guessing what the masses of the otherparticles in the series must be, and why these particles haven’t been discoveredyet.

28-6 The nuclear force ﬁeldWe would like to make some further remarks about the part of the massof nuclear particles that is not electromagnetic. Where does this other largefraction come from? There are other forces besides electrodynamics—like nuclearforces—that have their own ﬁeld theories, although no one knows whether thecurrent theories are right. These theories also predict a ﬁeld energy which givesthe nuclear particles a mass term analogous to electromagnetic mass; we couldcall it the「π-mesic-ﬁeld-mass.」It is presumably very large, because the forcesare great, and it is the possible origin of the mass of the heavy particles. Butthe meson ﬁeld theories are still in a most rudimentary state. Even with thewell-developed theory of electromagnetism, we found it impossible to get beyondﬁrst base in explaining the electron mass. With the theory of the mesons, westrike out.

We may take a moment to outline the theory of the mesons, because of itsinteresting connection with electrodynamics. In electrodynamics, the ﬁeld canbe described in terms of a four-potential that satisﬁes the equation

(cid:3)2Aµ = sources.

Now we have seen that pieces of the ﬁeld can be radiated away so that theyexist separated from the sources. These are the photons of light, and they aredescribed by a diﬀerential equation without sources:

(cid:3)2Aµ = 0.

People have argued that the ﬁeld of nuclear forces ought also to have its own「photons」—they would presumably be the π-mesons—and that they should bedescribed by an analogous diﬀerential equation. (Because of the weakness of thehuman brain, we can’t think of something really new; so we argue by analogywith what we know.) So the meson equation might be

(cid:3)2φ = 0,

28-12

where φ could be a diﬀerent four-vector or perhaps a scalar. It turns out that thepion has no polarization, so φ should be a scalar. With the simple equation (cid:3)2φ =0, the meson ﬁeld would vary with distance from a source as 1/r2, just as theelectric ﬁeld does. But we know that nuclear forces have much shorter distancesof action, so the simple equation won’t work. There is one way we can changethings without disrupting the relativistic invariance: we can add or subtractfrom the D’Alembertian a constant, times φ. So Yukawa suggested that the freequanta of the nuclear force ﬁeld might obey the equation

(28.17)(Since (cid:3)2 is a scalarwhere µ2 is a constant—that is, an invariant scalar.diﬀerential operator in four dimensions, its invariance is unchanged if we addanother scalar to it.)

− (cid:3)2φ − µ2φ = 0,

Let’s see what Eq. (28.17) gives for the nuclear force when things are not

changing with time. We want a spherically symmetric solution of

∇2φ − µ2φ = 0

around some point source at, say, the origin. If φ depends only on r, we knowthat

So we have the equation

or

1r

∇2φ = 1

∂2∂r2

r

(rφ).

∂2∂r2∂2∂r2

(rφ) − µ2φ = 0

(rφ) = µ2(rφ).

Thinking of (rφ) as our dependent variable, this is an equation we have seenmany times. Its solution is

rφ = Ke±µr.

e−µrr

.

Clearly, φ cannot become inﬁnite for large r, so the + sign in the exponent isruled out. The solution is

φ = K

(28.18)This function is called the Yukawa potential. For an attractive force, K is anegative number whose magnitude must be adjusted to ﬁt the experimentallyobserved strength of the forces.

The Yukawa potential of the nuclear forces dies oﬀ more rapidly than 1/rby the exponential factor. The potential—and therefore the force—falls to zeromuch more rapidly than 1/r for distances beyond 1/µ, as shown in Fig. 28-6.The「range」of nuclear forces is much less than the「range」of electrostatic forces.It is found experimentally that the nuclear forces do not extend beyond about10−13 cm, so µ ≈ 1015 m−1.

Finally, let’s look at the free-wave solution of Eq. (28.17). If we substitute

into Eq. (28.17), we get that

φ = φ0ei(ωt−kz)

ω2c2 − k2 − µ2 = 0.

Relating frequency to energy and wave number to momentum, as we did at theend of Chapter 34 of Vol. I, we get that

E2c2 − p2 = µ22,

which says that the Yukawa「photon」has a mass equal to µ/c. If we use for µthe estimate 1015 m−1, which gives the observed range of the nuclear forces, the28-13

Fig. 28-6. The Yukawa potential e−µr /r,compared with the Coulomb potential 1/r.

mass comes out to 3 × 10−25 g, or 170 MeV, which is roughly the observed massof the π-meson. So, by an analogy with electrodynamics, we would say that theπ-meson is the「photon」of the nuclear force ﬁeld. But now we have pushed theideas of electrodynamics into regions where they may not really be valid—wehave gone beyond electrodynamics to the problem of the nuclear forces.

28-14

29

The Motion of Charges in Electric andMagnetic Fields

