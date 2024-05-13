21-1 Light and electromagnetic wavesWe

saw in the last chapter that among their solutions, Maxwell’s equationshave waves of electricity and magnetism. These waves correspond to the phe-nomena of radio, light, x-rays, and so on, depending on the wavelength. Wehave already studied light in great detail in Vol. I. In this chapter we want totie together the two subjects—we want to show that Maxwell’s equations canindeed form the base for our earlier treatment of the phenomena of light.

When we studied light, we began by writing down equations for the electricand magnetic ﬁelds produced by a charge which moves in any arbitrary way.Those equations were

E = q4π0

and

(cid:20) er0

r02

(cid:18) er0

(cid:19)

+ r0

ddt

c

r02cB = er0 × E.

(cid:21)

+ 1c2

d2dt2 er0

(21.1)

[See Eqs. (28.3) and (28.4), Vol. I. As explained below, the signs here are thenegatives of the old ones.]

If a charge moves in an arbitrary way, the electric ﬁeld we would ﬁnd now atsome point depends only on the position and motion of the charge not now, butat an earlier time—at an instant which is earlier by the time it would take light,going at the speed c, to travel the distance r0 from the charge to the ﬁeld point.In other words, if we want the electric ﬁeld at point (1) at the time t, we mustcalculate the location (20) of the charge and its motion at the time (t − r0/c),where r0 is the distance to the point (1) from the position of the charge (20) atthe time (t − r0/c). The prime is to remind you that r0 is the so-called「retardeddistance」from the point (20) to the point (1), and not the actual distance betweenpoint (2), the position of the charge at the time t, and the ﬁeld point (1) (seeFig. 21-1). Note that we are using a diﬀerent convention now for the direction ofthe unit vector er. In Chapters 28 and 34 of Vol. I it was convenient to take r(and hence er) pointing toward the source. Now we are following the deﬁnitionwe took for Coulomb’s law, in which r is directed from the charge, at (2), towardthe ﬁeld point at (1). The only diﬀerence, of course, is that our new r (and er)are the negatives of the old ones.We have also seen that if the velocity v of a charge is always much less than c,and if we consider only points at large distances from the charge, so that onlythe last term of Eq. (21.1) is important, the ﬁelds can also be written as

(cid:20)acceleration of the charge at (t − r0/c)

projected at right angles to r0

(cid:21)

(21.10)

E =

q

4π0c2r0

and

cB = er0 × E.

21-1 Light and electromagnetic waves21-2 Spherical waves from a point

source

equations

21-3 The general solution of Maxwell’s

21-4 The ﬁelds of an oscillating dipole21-5 The potentials of a moving

charge; the general solution ofLiénard and Wiechert

21-6 The potentials for a charge

moving with constant velocity;the Lorentz formula

Review: Chapter 28, Vol. I, Electromag-netic RadiationChapter 31, Vol. I, The Originof the Refractive IndexChapter 34, Vol. I, RelativisticEﬀects in Radiation

Let’s look at what the complete equation, Eq. (21.1), says in a little moredetail. The vector er0 is the unit vector to point (1) from the retarded position (20).The ﬁrst term, then, is what we would expect for the Coulomb ﬁeld of the chargeat its retarded position—we may call this「the retarded Coulomb ﬁeld.」Theelectric ﬁeld depends inversely on the square of the distance and is directed awayfrom the retarded position of the charge (that is, in the direction of er0).

21-1

Fig. 21-1. The ﬁelds at (1) at the time tdepend on the position (2(cid:48)) occupied by thecharge q at the time (t − r (cid:48)/c).

But that is only the ﬁrst term. The other terms tell us that the laws ofelectricity do not say that all the ﬁelds are the same as the static ones, but justretarded (which is what people sometimes like to say). To the「retarded Coulombﬁeld」we must add the other two terms. The second term says that there is a「correction」to the retarded Coulomb ﬁeld which is the rate of change of theretarded Coulomb ﬁeld multiplied by r0/c, the retardation delay. In a way ofspeaking, this term tends to compensate for the retardation in the ﬁrst term. Theﬁrst two terms correspond to computing the「retarded Coulomb ﬁeld」and thenextrapolating it toward the future by the amount r0/c, that is, right up to thetime t! The extrapolation is linear, as if we were to assume that the「retardedCoulomb ﬁeld」would continue to change at the rate computed for the chargeat the point (20). If the ﬁeld is changing slowly, the eﬀect of the retardation isalmost completely removed by the correction term, and the two terms togethergive us an electric ﬁeld that is the「instantaneous Coulomb ﬁeld」—that is, theCoulomb ﬁeld of the charge at the point (2)—to a very good approximation.

Finally, there is a third term in Eq. (21.1) which is the second derivative of theunit vector er0. For our study of the phenomena of light, we made use of the factthat far away from the charge the ﬁrst two terms went inversely as the square ofthe distance and, for large distances, became very weak in comparison to the lastterm, which decreases as 1/r. So we concentrated entirely on the last term, andwe showed that it is (again, for large distances) proportional to the component ofthe acceleration of the charge at right angles to the line of sight. (Also, for mostof our work in Vol. I, we took the case in which the charges were moving nonrela-tivistically. We considered the relativistic eﬀects in only one chapter, Chapter 34.)Now we should try to connect the two things together. We have the Maxwellequations, and we have Eq. (21.1) for the ﬁeld of a point charge. We shouldcertainly ask whether they are equivalent. If we can deduce Eq. (21.1) fromMaxwell’s equations, we will really understand the connection between light andelectromagnetism. To make this connection is the main purpose of this chapter.It turns out that we won’t quite make it—that the mathematical details gettoo complicated for us to carry through in all their gory details. But we will comeclose enough so that you should easily see how the connection could be made.The missing pieces will only be in the mathematical details. Some of you mayﬁnd the mathematics in this chapter rather complicated, and you may not wishto follow the argument very closely. We think it is important, however, to makethe connection between what you have learned earlier and what you are learningnow, or at least to indicate how such a connection can be made. You will notice,if you look over the earlier chapters, that whenever we have taken a statement asa starting point for a discussion, we have carefully explained whether it is a new「assumption」that is a「basic law,」or whether it can ultimately be deduced fromsome other laws. We owe it to you in the spirit of these lectures to make theconnection between light and Maxwell’s equations. If it gets diﬃcult in places,well, that’s life—there is no other way.

21-2 Spherical waves from a point sourceIn Chapter 18 we found that Maxwell’s equations could be solved by letting

and

E = −∇φ − ∂A∂tB = ∇ × A,

where φ and A must then be solutions of the equations

and

∂2φ∂t2

= − ρ0

∇2φ − 1c2∇2A − 1c2

∂2A∂t2

= − j

0c2 ,

(21.2)

(21.3)

(21.4)

(21.5)

21-2

and must also satisfy the condition that

∇ · A = − 1c2

∂φ∂t

.

(21.6)

Now we will ﬁnd the solution of Eqs. (21.4) and (21.5). To do that we have

to ﬁnd the solution ψ, of the equation∇2ψ − 1c2

∂2ψ∂t2

= −s,

(21.7)

where s, which we call the source, is known. Of course, s corresponds to ρ/0and ψ to φ for Eq. (21.4), or s is jx/0c2 if ψ is Ax, etc., but we want to solveEq. (21.7) as a mathematical problem no matter what ψ and s are physically.In places where ρ and j are zero—in what we have called「free」space—thepotentials φ and A, and the ﬁelds E and B, all satisfy the three-dimensionalwave equation without sources, whose mathematical form is

∇2ψ − 1c2

∂2ψ∂t2

= 0.

(21.8)

In Chapter 20 we saw that solutions of this equation can represent waves ofvarious kinds: plane waves in the x-direction, ψ = f(t − x/c); plane waves in they- or z-direction, or in any other direction; or spherical waves of the form

ψ(x, y, z, t) = f(t − r/c)

r

.

(21.9)

(The solutions can be written in still other ways, for example cylindrical wavesthat spread out from an axis.)

We also remarked that, physically, Eq. (21.9) does not represent a wave infree space—that there must be charges at the origin to get the outgoing wavestarted. In other words, Eq. (21.9) is a solution of Eq. (21.8) everywhere exceptright near r = 0, where it must be a solution of the complete equation (21.7),including some sources. Let’s see how that works. What kind of a source s inEq. (21.7) would give rise to a wave like Eq. (21.9)?Suppose we have the spherical wave of Eq. (21.9) and look at what is happeningfor very small r. Then the retardation −r/c in f(t − r/c) can be neglected—provided f is a smooth function—and ψ becomes

ψ = f(t)

r

(r → 0).

(21.10)

So ψ is just like a Coulomb ﬁeld for a charge at the origin that varies with time.That is, if we had a little lump of charge, limited to a very small region near theorigin, with a density ρ, we know that

where Q =R ρ dV . Now we know that such a φ satisﬁes the equation

r

,

φ = Q/4π0

∇2φ = − ρ0

.

satisﬁes

Following the same mathematics, we would say that the ψ of Eq. (21.10)(21.11)

∇2ψ = −s

(r → 0),

where s is related to f by

with

f = S4π

,

Z

S =

s dV.

21-3

The only diﬀerence is that in the general case, s, and therefore S, can be afunction of time.Now the important thing is that if ψ, satisﬁes Eq. (21.11) for small r, it alsosatisﬁes Eq. (21.7). As we go very close to the origin, the 1/r dependence of ψcauses the space derivatives to become very large. But the time derivatives keeptheir same values. [They are just the time derivatives of f(t).] So as r goes tozero, the term ∂2ψ/∂t2 in Eq. (21.7) can be neglected in comparison with ∇2ψ,and Eq. (21.7) becomes equivalent to Eq. (21.11).To summarize, then, if the source function s(t) of Eq. (21.7) is localized at

the origin and has the total strength

S(t) =

the solution of Eq. (21.7) is

Z

s(t) dV,

(21.12)

(21.13)

ψ(x, y, z, t) = 14π

S(t − r/c)

r

.

The only eﬀect of the term ∂2ψ/∂t2 in Eq. (21.7) is to introduce the retarda-tion (t − r/c) in the Coulomb-like potential.

21-3 The general solution of Maxwell’s equationsWe have found the solution of Eq. (21.7) for a「point」source. The nextquestion is: What is the solution for a spread-out source? That’s easy; we canthink of any source s(x, y, z, t) as made up of the sum of many「point」sources,one for each volume element dV , and each with the source strength s(x, y, z, t) dV .Since Eq. (21.7) is linear, the resultant ﬁeld is the superposition of the ﬁelds fromall of such source elements.

Using the results of the preceding section [Eq. (21.13)] we know that theﬁeld dψ at the point (x1, y1, z1)—or (1) for short—at the time t, from a sourceelement s dV at the point (x2, y2, z2)—or (2) for short—is given by

dψ(1, t) = s(2, t − r12/c) dV2

4πr12

,

where r12 is the distance from (2) to (1). Adding the contributions from allthe pieces of the source means, of course, doing an integral over all regionswhere s 6= 0; so we have

ψ(1, t) =

dV2.

(21.14)

That is, the ﬁeld at (1) at the time t is the sum of all the spherical waves whichleave the source elements at (2) at the times (t − r12/c). This is the solution ofour wave equation for any set of sources.We see now how to obtain a general solution for Maxwell’s equations. Iffor ψ we mean the scalar potential φ, the source function s becomes ρ/0. Or wecan let ψ represent any one of the three components of the vector potential A,replacing s by the corresponding component of j/0c2. Thus, if we know thecharge density ρ(x, y, z, t) and the current density j(x, y, z, t) everywhere, we canimmediately write down the solutions of Eqs. (21.4) and (21.5). They are

Z s(2, t − r12/c)

4πr12

Z ρ(2, t − r12/c)Z j(2, t − r12/c)

4π0r12

4π0c2r12

and

φ(1, t) =

A(1, t) =

dV2

dV2.

(21.15)

(21.16)

The ﬁelds E and B can then be found by diﬀerentiating the potentials, usingEqs. (21.2) and (21.3). [Incidentally, it is possible to verify that the φ and Aobtained from Eqs. (21.15) and (21.16) do satisfy the equality (21.6).]

21-4

We have solved Maxwell’s equations. Given the currents and charges in anycircumstance, we can ﬁnd the potentials directly from these integrals and thendiﬀerentiate and get the ﬁelds. So we have ﬁnished with the Maxwell theory. Alsothis permits us to close the ring back to our theory of light, because to connect withour earlier work on light, we need only calculate the electric ﬁeld from a movingcharge. All that remains is to take a moving charge, calculate the potentials fromthese integrals, and then diﬀerentiate to ﬁnd E from −∇φ − ∂A/∂t. We shouldget Eq. (21.1). It turns out to be lots of work, but that’s the principle.So here is the center of the universe of electromagnetism—the complete theoryof electricity and magnetism, and of light; a complete description of the ﬁeldsproduced by any moving charges; and more. It is all here. Here is the structurebuilt by Maxwell, complete in all its power and beauty. It is probably one of thegreatest accomplishments of physics. To remind you of its importance, we willput it all together in a nice frame.

Maxwell’s equations:

∇ · E = ρ0

∇ × E = −∂B∂t

∇ · B = 0

c2∇ × B = j0

+ ∂E∂t

Their solutions:

E = −∇φ − ∂A∂tB = ∇ × AZ ρ(2, t − r12/c)Z j(2, t − r12/c)

4π0r12

4π0c2r12

φ(1, t) =

A(1, t) =

dV2

dV2

21-4 The ﬁelds of an oscillating dipoleWe have still not lived up to our promise to derive Eq. (21.1) for the electricﬁeld of a point charge in motion. Even with the results we already have, it is arelatively complicated thing to derive. We have not found Eq. (21.1) anywhere inthe published literature except in Vol. I of these lectures.* So you can see that it isnot easy to derive. (The ﬁelds of a moving charge have been written in many otherforms that are equivalent, of course.) We will have to limit ourselves here just toshowing that, in a few examples, Eqs. (21.15) and (21.16) give the same resultsas Eq. (21.1). First, we will show that Eq. (21.1) gives the correct ﬁelds with onlythe restriction that the motion of the charged particle is nonrelativistic. (Just thisspecial case will take care of 90 percent, or more, of what we said about light.)We consider a situation in which we have a blob of charge that is movingabout in some way, in a small region, and we will ﬁnd the ﬁelds far away. Toput it another way, we are ﬁnding the ﬁeld at any distance from a point chargethat is shaking up and down in very small motion. Since light is usually emittedfrom neutral objects such as atoms, we will consider that our wiggling charge qis located near an equal and opposite charge at rest. If the separation betweenthe centers of the charges is d, the charges will have a dipole moment p = qd,It was independentlydiscovered by R. P. Feynman, in about 1950, and given in some lectures as a good way ofthinking about synchrotron radiation.

* The formula was ﬁrst published by Oliver Heaviside in 1902.

21-5

which we take to be a function of time. Now we should expect that if we lookat the ﬁelds close to the charges, we won’t have to worry about the delay; theelectric ﬁeld will be exactly the same as the one we have calculated earlier foran electrostatic dipole—using, of course, the instantaneous dipole moment p(t).But if we go very far out, we ought to ﬁnd a term in the ﬁeld that goes as 1/rand depends on the acceleration of the charge perpendicular to the line of sight.Let’s see if we get such a result.

We begin by calculating the vector potential A, using Eq. (21.16). Supposethat our moving charge is in a small blob whose charge density is given by ρ(x, y, z),and the whole thing is moving at any instant with the velocity v. Then thecurrent density j(x, y, z) will be equal to vρ(x, y, z). It will be convenient totake our coordinate system so that the z-axis is in the direction of v; then thegeometry of our problem is as shown in Fig. 21-2. We want the integral

Z j(2, t − r12/c)

r12

dV2.

(21.17)

Now if the size of the charge-blob is really very small compared with r12, wecan set the r12 term in the denominator equal to r, the distance to the center ofthe blob, and take r outside the integral. Next, we are also going to set r12 = rin the numerator, although that is not really quite right. It is not right becausewe should take j at, say, the top of the blob at a slightly diﬀerent time than weused for j at the bottom of the blob. When we set r12 = r in j(t− r12/c), we aretaking the current density for the whole blob at the same time (t − r/c). That isan approximation that will be good only if the velocity v of the charge is muchless than c. So we are making a nonrelativistic calculation. Replacing j by ρv,the integral (21.17) becomes

Z

1r

vρ(2, t − r/c) dV2.

Fig. 21-2. The potential at (1) are given

by integrals over the charge density ρ.

Since all the charge has the same velocity, this integral is just v/r times the totalcharge q. But qv is just ∂p/∂t, the rate of change of the dipole moment—whichis, of course, to be evaluated at the retarded time (t − r/c). We will write itas ˙p(t − r/c). So we get for the vector potential

A(1, t) =

1

4π0c2

˙p(t − r/c)

r

.

(21.18)

Our result says that the current in a varying dipole produces a vector potentialin the form of spherical waves whose source strength is ˙p/0c2.We can now get the magnetic ﬁeld from B = ∇× A. Since ˙p is totally in thez-direction, A has only a z-component; there are only two nonzero derivatives inthe curl. So Bx = ∂Az/∂y and By = −∂Az/∂x. Let’s ﬁrst look at Bx:

To carry out the diﬀerentiation, we must remember that r =px2 + y2 + z2, so

4π0c2

Bx = ∂Az∂y

(21.19)

∂∂y

=

r

.

1

˙p(t − r/c)

(cid:18)1

(cid:19)

1

Bx =

1∂r∂yRemembering that ∂r/∂y = y/r, the ﬁrst term gives

˙p(t − r/c) ∂∂y

+ 1

4π0c2

4π0c2

r

˙p(t − r/c).

(21.20)

− 14π0c2

y ˙p(t − r/c)

r3

,

(21.21)

which drops oﬀ as 1/r2 like the potential of a static dipole (because y/r is constantfor a given direction).The second term in Eq. (21.20) gives us the new eﬀects. Carrying out the

diﬀerentiation, we get

− 14π0c2

ycr2

¨p(t − r/c),

(21.22)

21-6

where ¨p means, of course, the second derivative of p with respect to t. Thisterm, which comes from diﬀerentiating the numerator, is responsible for radiation.First, it describes a ﬁeld which decreases with distance only as 1/r. Second, itdepends on the acceleration of the charge. You can begin to see how we are goingto get a result like Eq. (21.10), which describes the radiation of light.Let’s examine in a little more detail how this radiation term comes about—itis such an interesting and important result. We start with the expression (21.18),which has a 1/r dependence and is therefore like a Coulomb potential, except forthe delay term in the numerator. Why is it then that when we diﬀerentiate withrespect to space coordinates to get the ﬁelds, we don’t just get a 1/r2 ﬁeld—with,of course, the corresponding time delays?We can see why in the following way: Suppose that we let our dipole oscillate

up and down in a sinusoidal motion. Then we would have

and

p = pz = p0 sin ωt

Az =

1

4π0c2

ωp0 cos ω(t − r/c)

r

.

If we plot a graph of Az as a function of r at a given instant, we get the curveshown in Fig. 21-3. The peak amplitude decreases as 1/r, but there is, in addition,an oscillation in space, bounded by the 1/r envelope. When we take the spatialderivatives, they will be proportional to the slope of the curve. From the ﬁgurewe see that there are slopes much steeper than the slope of the 1/r curve itself.It is, in fact, evident that for a given frequency the peak slopes are proportionalto the amplitude of the wave, which varies as 1/r. So that explains the drop-oﬀrate of the radiation term.It all comes about because the variations with time at the source are translatedinto variations in space as the waves are propagated outward, and the magneticﬁelds depend on the spatial derivatives of the potential.Let’s go back and ﬁnish our calculation of the magnetic ﬁeld. We have for Bxthe two terms (21.21) and (21.22), so

(cid:20)− y ˙p(t − r/c)(cid:20) x ˙p(t − r/c)With the same kind of mathematics, we get

4π0c2

Bx =

r3

1

1

By =

(cid:21)− y¨p(t − r/c)(cid:21)

+ x¨p(t − r/c)

cr2

.

.

4π0c2

cr2Or we can put it all together in a nice vector formula:[ ˙p + (r/c)¨p]t−r/c × r

r3

1

B =

4π0c2

r3

.

(21.23)

Fig. 21-3. The z-component of A as afunction of r at the instant t for the spheri-cal wave from an oscillating dipole.

Now let’s look at this formula. First of all, if we go very far out in r, only the¨p term counts. The direction of B is given by ¨p×r, which is at right angles to theradius r and also at right angles to the acceleration, as in Fig. 21-4. Everythingis coming out right; that is also the result we get from Eq. (21.10).Now let’s look at what we are not used to—at what happens closer in. InSection 14-7 we worked out the law of Biot and Savart for the magnetic ﬁeld ofan element of current. We found that a current element j dV contributes to themagnetic ﬁeld the amount

dB =

1

4π0c2

j × rr3 dV.

(21.24)

You see that this formula looks very much like the ﬁrst term of Eq. (21.23), ifwe remember that ˙p is the current. But there is one diﬀerence. In Eq. (21.23),the current is to be evaluated at the time (t − r/c), which doesn’t appear in21-7

Fig. 21-4. The radiation ﬁelds B and E

of an oscillating dipole.

Eq. (21.24). Actually, however, Eq. (21.24) is still very good for small r, becausethe second term of Eq. (21.23) tends to cancel out the eﬀect of the retardationin the ﬁrst term. The two together give a result very near to Eq. (21.24) when ris small.We can see that this way: When r is small, (t − r/c) is not very diﬀerentfrom t, so we can expand the bracket in Eq. (21.23) in a Taylor series. For theﬁrst term,

and to the same order in r/c,

˙p(t − r/c) = ˙p(t) − rc

¨p(t) + etc.,

rc

¨p(t − r/c) = rc

¨p(t) + etc.

When we take the sum, the two terms in ¨p cancel, and we are left with theunretarded current ˙p: that is, ˙p(t)—plus terms of order (r/c)2 or higher [e.g.,2(r/c)2˙˙˙p ] which will be very small for r small enough that ˙p does not alter1markedly in the time r/c.So Eq. (21.23) gives ﬁelds very much like the instantaneous theory—muchcloser than the instantaneous theory with a delay; the ﬁrst-order eﬀects of thedelay are taken out by the second term. The static formulas are very accurate,much more accurate than you might think. Of course, the compensation onlyworks for points close in. For points far out the correction becomes very bad,because the time delays produce a very large eﬀect, and we get the important1/r term of the radiation.We still have the problem of computing the electric ﬁeld and demonstratingthat it is the same as Eq. (21.10). For large distances we can see that the answeris going to come out all right. We know that far from the sources, where we havea propagating wave, E is perpendicular to B (and also to r), as in Fig. 21-4,and that cB = E. So E is proportional to the acceleration ¨p, as expected fromEq. (21.10).To get the electric ﬁeld completely for all distances, we need to solve for theelectrostatic potential. When we computed the current integral for A to getEq. (21.18), we made an approximation by disregarding the slight variation of rin the delay terms. This will not work for the electrostatic potential, because wewould then get 1/r times the integral of the charge density, which is a constant.This approximation is too rough. We need to go to one higher order. Instead ofgetting involved in that higher-order computation directly, we can do somethingelse—we can determine the scalar potential from Eq. (21.6), using the vectorpotential we have already found. The divergence of A, in our case, is just∂Az/∂z—since Ax and Ay are identically zero. Diﬀerentiating in the same waythat we did above to ﬁnd B,

(cid:20)˙p(t − r/c) ∂(cid:20)∂z− z ˙p(t − r/c)

+ 1

(cid:18)1(cid:19)− z¨p(t − r/c)

∂∂z

r

r

(cid:21)

.

r3

cr2

(cid:21)

˙p(t − r/c)

∇ · A =

1

4π0c2

=

1

4π0c2

Or, in vector notation,

∇ · A = − 14π0c2

[ ˙p + (r/c)¨p]t−r/c · r

r3

.

Using Eq. (21.6), we have an equation for φ:

∂φ∂t

= 14π0

[ ˙p + (r/c)¨p]t−r/c · r

r3

.

Integrating with respect to t just removes one dot from each of the p’s, so

φ(r, t) = 14π0

[p + (r/c) ˙p]t−r/c · r

r3

.

(21.25)

21-8

(The constant of integration would correspond to some superposed static ﬁeldwhich could, of course, exist. For the oscillating dipole we have taken, there isno static ﬁeld.)

We are now able to ﬁnd the electric ﬁeld E from

E = −∇φ − ∂A∂t

.

Since the steps are tedious but straightforward [providing you remember that p(t−r/c) and its time derivatives depend on x, y, and z through the retardation r/c],we will just give the result:

(cid:21)

c2{¨p(t − r/c) × r} × r˙p(t − r/c).

(21.26)

(21.27)

E(r, t) =

1

4π0r3

with

(cid:20)3(p∗ · r)r

r2

− p∗ + 1

p∗ = p(t − r/c) + r

c

Although it looks rather complicated, the result is easily interpreted. Thevector p∗ is the dipole moment retarded and then「corrected」for the retardation,so the two terms with p∗ give just the static dipole ﬁeld when r is small. [SeeChapter 6, Eq. (6.14).] When r is large, the term in ¨p dominates, and the electricﬁeld is proportional to the acceleration of the charges, at right angles to r, and,in fact, directed along the projection of ¨p in a plane perpendicular to r.This result agrees with what we would have gotten using Eq. (21.1). Of course,Eq. (21.1) is more general; it works with any motion, while Eq. (21.26) is validonly for small motions for which we can take the retardation r/c as constant overthe source. At any rate, we have now provided the underpinnings for our entireprevious discussion of light (excepting some matters discussed in Chapter 34 ofVol. I), for it all hinged on the last term of Eq. (21.26). We will discuss nexthow the ﬁelds can be obtained for more rapidly moving charges (leading to therelativistic eﬀects of Chapter 34 of Vol. I).

21-5 The potentials of a moving charge; the general solution of Liénard and

Wiechert

In the last section we made a simpliﬁcation in calculating our integral for Aby considering only low velocities. But in doing so we missed an important pointand also one where it is easy to go wrong. We will therefore take up now acalculation of the potentials for a point charge moving in any way whatever—evenwith a relativistic velocity. Once we have this result, we will have the completeelectromagnetism of electric charges. Even Eq. (21.1) can then be derived bytaking derivatives. The story will be complete. So bear with us.

Let’s try to calculate the scalar potential φ(1) at the point (x1, y1, z1) producedby a point charge, such as an electron, moving in any manner whatsoever. By a「point」charge we mean a very small ball of charge, shrunk down as small as youlike, with a charge density ρ(x, y, z). We can ﬁnd φ from Eq. (21.15):

Z ρ(2, t − r12/c)

r12

φ(1, t) = 14π0

dV2.

(21.28)

The answer would seem to be—and almost everyone would, at ﬁrst, think—thatthe integral of ρ over such a「point」charge is just the total charge q, so that

φ(1, t) = 14π0

qr012

(wrong).

By r0the retarded time (t − r12/c). It is wrong.

12 we mean the radius vector from the charge at point (2) to point (1) atThe correct answer is

φ(1, t) = 14π0

·

qr012

1

1 − vr0/c

,

(21.29)

21-9

Fig. 21-5. (a) A「point」charge—considered as a small cubical distribution ofcharge—moving with the speed v toward point (1). (b) The volume element ∆Vi usedfor calculating the potentials.

where vr0, is the component of the velocity of the charge parallel to r012—namely,toward point (1). We will now show you why. To make the argument easier tofollow, we will make the calculation ﬁrst for a「point」charge which is in theform of a little cube of charge moving toward the point (1) with the speed v, asshown in Fig. 21-5(a). Let the length of a side of the cube be a, which we taketo be much, much less than r12, the distance from the center of the charge to thepoint (1).Now to evaluate the integral of Eq. (21.28), we will return to basic principles;

we will write it as the sum

ρi ∆Vi

ri

,

(21.30)

X

i

where ri is the distance from point (1) to the ith volume element ∆Vi and ρi isthe charge density at ∆Vi at the time ti = t − ri/c. Since ri (cid:29) a, always, it willbe convenient to take our ∆Vi in the form of thin, rectangular slices perpendicularto r12, as shown in Fig. 21-5(b).Suppose we start by taking the volume elements ∆Vi with some thickness wmuch less than a. The individual elements will appear as shown in Fig. 21-6(a),where we have put in more than enough to cover the charge. But we have notshown the charge, and for a good reason. Where should we draw it? For eachvolume element ∆Vi we are to take ρ at the time ti = (t − ri/c), but since thecharge is moving, it is in a diﬀerent place for each volume element ∆Vi!Let’s say that we begin with the volume element labeled「1」in Fig. 21-6(a),chosen so that at the time t1 = (t − r1/c) the「back」edge of the charge occu-pies ∆V1, as shown in Fig. 21-6(b). Then when we evaluate ρ2 ∆V2, we must usethe position of the charge at the slightly later time t2 = (t − r2/c), when thecharge will be in the position shown in Fig. 21-6(c). And so on, for ∆V3, ∆V4,etc. Now we can evaluate the sum.Since the thickness of each ∆Vi is w, its volume is wa2. Then each volumeelement that overlaps the charge distribution contains the amount of charge wa2ρ,where ρ is the density of charge within the cube—which we take to be uniform.When the distance from the charge to point (1) is large, we will make a negligibleerror by setting all the ri’s in the denominators equal to some average value, saythe retarded position r0 of the center of the charge. Then the sum (21.30) is

NX

i=1

ρwa2r0

,

N

(cid:19)

.

(cid:18) N wρwa2r0 = ρa3r0(cid:19)(cid:18) b

φ = q

a

.

4π0r0

a

where ∆VN is the last ∆Vi that overlaps the charge distributions, as shown inFig. 21-6(e). The sum is, clearly,

Fig. 21-6. Integrating ρ(t − r (cid:48)/c) dV for

a moving charge.

Now ρa3 is just the total charge q and N w is the length b shown in part (e) ofthe ﬁgure. So we have

(21.31)

21-10

What is b? It is the length of the cube of charge increased by the distancemoved by the charge between t1 = (t − r1/c) and tN = (t − rN /c)—which is thedistance the charge moves in the time

∆t = tN − t1 = (r1 − rN)/c = b/c.

Since the speed of the charge is v, the distance moved is v ∆t = vb/c. But thelength b is this distance added to a:

Solving for b, we get

b = a + vc

b.

b =

a

1 − (v/c) .

Of course by v we mean the velocity at the retarded time t0 = (t − r0/c), whichwe can indicate by writing [1 − v/c]ret, and Eq. (21.31) for the potential becomes

φ(1, t) = q

4π0r0

1

[1 − (v/c)]ret

.

This result agrees with our assertion, Eq. (21.29). There is a correction termwhich comes about because the charge is moving as our integral「sweeps overthe charge.」When the charge is moving toward the point (1), its contributionto the integral is increased by the ratio b/a. Therefore the correct integral isq/r0 multiplied by b/a, which is 1/[1 − v/c]ret.If the velocity of the charge is not directed toward the observation point (1),you can see that what matters is the component of its velocity toward point (1).Calling this velocity component vr, the correction factor is 1/[1 − vr/c]ret. Also,the analysis we have made goes exactly the same way for a charge distribution ofany shape—it doesn’t have to be a cube. Finally, since the「size」of the charge qdoesn’t enter into the ﬁnal result, the same result holds when we let the chargeshrink to any size—even to a point. The general result is that the scalar potentialfor a point charge moving with any velocity is

4π0r0[1 − (vr/c)]retThis equation is often written in the equivalent form

φ(1, t) =

q

φ(1, t) =

q

4π0[r − (v · r/c)]ret

.

,

(21.32)

(21.33)

where r is the vector from the charge to the point (1), where φ is being evaluated,and all the quantities in the bracket are to have their values at the retardedtime t0 = t − r0/c.The same thing happens when we compute A for a point charge, fromEq. (21.16). The current density is ρv and the integral over ρ is the same as wefound for φ. The vector potential is

A(1, t) =

qvret

4π0c2[r − (v · r/c)]ret

.

(21.34)

The potentials for a point charge were ﬁrst deduced in this form by Liénard

and Wiechert and are called the Liénard-Wiechert potentials.To close the ring back to Eq. (21.1) it is only necessary to compute E and Bfrom these potentials (using B = ∇ × A and E = −∇φ − ∂A/∂t). It is nowonly arithmetic. The arithmetic, however, is fairly involved, so we will not writeout the details. Perhaps you will take our word for it that Eq. (21.1) is equivalentto the Liénard-Wiechert potentials we have derived.*

* If you have a lot of paper and time you can try to work it through yourself. We would,then, make two suggestions: First, don’t forget that the derivatives of r0 are complicated, sinceit is a function of t0. Second, don’t try to derive (21.1), but carry out all of the derivatives in it,and then compare what you get with the E obtained from the potentials (21.33) and (21.34).21-11

21-6 The potentials for a charge moving with constant velocity; the Lorentz

formula

We want next to use the Liénard-Wiechert potentials for a special case—to ﬁndthe ﬁelds of a charge moving with uniform velocity in a straight line. We will do itagain later, using the principle of relativity. We already know what the potentialsare when we are standing in the rest frame of a charge. When the charge ismoving, we can ﬁgure everything out by a relativistic transformation from onesystem to the other. But relativity had its origin in the theory of electricity andmagnetism. The formulas of the Lorentz transformation (Chapter 15, Vol. I) werediscoveries made by Lorentz when he was studying the equations of electricity andmagnetism. So that you can appreciate where things have come from, we wouldlike to show that the Maxwell equations do lead to the Lorentz transformation.We begin by calculating the potentials of a charge moving with uniform velocity,directly from the electrodynamics of Maxwell’s equations. We have shown thatMaxwell’s equations lead to the potentials for a moving charge that we got inthe last section. So when we use these potentials, we are using Maxwell’s theory.

Fig. 21-7. Finding the potential at P of acharge moving with uniform velocity alongthe x-axis.

Suppose we have a charge moving along the x-axis with the speed v. Wewant the potentials at the point P(x, y, z), as shown in Fig. 21-7. If t = 0 is themoment when the charge is at the origin, at the time t the charge is at x = vt,y = z = 0. What we need to know, however, is its position at the retarded time

t0 = t − r0

c

,

(21.35)

where r0 is the distance to the point P from the charge at the retarded time. Atthe earlier time t0, the charge was at x = vt0, so

(21.36)To ﬁnd r0 or t0 we have to combine this equation with Eq. (21.35). First, weeliminate r0 by solving Eq. (21.35) for r0 and substituting in Eq. (21.36). Then,squaring both sides, we get

r0 =p(x − vt0)2 + y2 + z2.

c2(t − t0)2 = (x − vt0)2 + y2 + z2,

which is a quadratic equation in t0. Expanding the squared binomials andcollecting like terms in t0, we get

(v2 − c2)t02 − 2(xv − c2t)t0 + x2 + y2 + z2 − (ct)2 = 0.

Solving for t0,

(cid:18)

1 − v2c2

(cid:19)

t0 = t − vx

c2 − 1

c

s

(x − vt)2 +

(cid:19)

(cid:18)

1 − v2c2

(y2 + z2).

(21.37)

21-12

To get r0 we have to substitute this expression for t0 into

r0 = c(t − t0).

Now we are ready to ﬁnd φ from Eq. (21.33), which, since v is constant,

becomes

(21.38)The component of v in the direction of r0 is v × (x − vt0)/r0, so v · r0 is justv × (x − vt0), and the whole denominator is

φ(x, y, z, t) = q4π0

r0 − (v · r0/c) .

1

(cid:18)

(cid:20)

c2 −t − vx(cid:18)

(cid:19)t0(cid:21)

.

1 − v2c2Substituting for (1 − v2/c2)t0 from Eq. (21.37), we get for φ

c(t − t0) − vc

(x − vt0) = c

φ(x, y, z, t) = q4π0

s

(cid:19)

11 − v2c2

.

(y2 + z2)

(x − vt)2 +

This equation is more understandable if we rewrite it as

φ(x, y, z, t) = q4π0

1r1 − v2c2

(cid:20)(cid:18) x − vtp1 − v2/c2

1

(cid:19)2

+ y2 + z2

(cid:21)1/2 .

(21.39)

The vector potential A is the same expression with an additional factor of v/c2:

A = v

c2 φ.

In Eq. (21.39) you can clearly see the beginning of the Lorentz transformation.

If the charge were at the origin in its own rest frame, its potential would be

φ(x, y, z) = q4π0

1

[x2 + y2 + z2]1/2 .

We are seeing it in a moving coordinate system, and it appears that the coordinatesshould be transformed by

p1 − v2/c2 ,x → x − vty → y,z → z.

That is just the Lorentz transformation, and what we have done is essentiallythe way Lorentz discovered it.

But what about that extra factor 1/p1 − v2/c2 that appears at the front ofThe extra 1/p1 − v2/c2 in Eq. (21.39) is the same factor that always comesdensity ρ transforms to ρ/p1 − v2/c2. In fact, it is almost apparent from Eqs.

Eq. (21.39)? Also, how does the vector potential A appear, when it is everywherezero in the rest frame of the particle? We will soon show that A and φ togetherconstitute a four-vector, like the momentum p and the total energy U of a particle.in when one transforms the components of a four-vector—just as the charge

(21.4) and (21.5) that A and φ are components of a four-vector, because we havealready shown in Chapter 13 that j and ρ are the components of a four-vector.Later we will take up in more detail the relativity of electrodynamics; herewe only wished to show how naturally the Maxwell equations lead to the Lorentztransformation. You will not, then, be surprised to ﬁnd that the laws of electricityand magnetism are already correct for Einstein’s relativity. We will not have to「ﬁx them up,」as we had to do for Newton’s laws of mechanics.

21-13

22-1 Impedances22-2 Generators22-3 Networks of ideal elements;

Kirchhoﬀ’s rules

22-4 Equivalent circuits22-5 Energy22-6 A ladder network22-7 Filters22-8 Other circuit elements

Review: Chapter 22, Vol. I, Algebra

Chapter 23, Vol. I, ResonanceChapter 25, Vol. I, Linear Sys-tems and Review

22

AC Circuits

22-1 ImpedancesMost

of our work in this course has been aimed at reaching the completeequations of Maxwell. In the last two chapters we have been discussing theconsequences of these equations. We have found that the equations contain allthe static phenomena we had worked out earlier, as well as the phenomena ofelectromagnetic waves and light that we had gone over in some detail in Volume I.The Maxwell equations give both phenomena, depending upon whether onecomputes the ﬁelds close to the currents and charges, or very far from them.There is not much interesting to say about the intermediate region; no specialphenomena appear there.

There still remain, however, several subjects in electromagnetism that wewant to take up. We want to discuss the question of relativity and the Maxwellequations—what happens when one looks at the Maxwell equations with respectto moving coordinate systems. There is also the question of the conservation ofenergy in electromagnetic systems. Then there is the broad subject of the elec-tromagnetic properties of materials; so far, except for the study of the propertiesof dielectrics, we have considered only the electromagnetic ﬁelds in free space.And although we covered the subject of light in some detail in Volume I, thereare still a few things we would like to do again from the point of view of the ﬁeldequations.

In particular, we want to take up again the subject of the index of refraction,particularly for dense materials. Finally, there are the phenomena associatedwith waves conﬁned in a limited region of space. We touched on this kind ofproblem brieﬂy when we were studying sound waves. Maxwell’s equations leadalso to solutions which represent conﬁned waves of the electric and magneticﬁelds. We will take up this subject, which has important technical applications,in some of the following chapters. In order to lead up to that subject, we willbegin by considering the properties of electrical circuits at low frequencies. Wewill then be able to make a comparison between those situations in which thealmost static approximations of Maxwell’s equations are applicable and thosesituations in which high-frequency eﬀects are dominant.

So we descend from the great and esoteric heights of the last few chaptersand turn to the relatively low-level subject of electrical circuits. We will see,however, that even such a mundane subject, when looked at in suﬃcient detail,can contain great complications.

We have already discussed some of the properties of electrical circuits inChapters 23 and 25 of Vol. I. Now we will cover some of the same material again,but in greater detail. Again we are going to deal only with linear systems andwith voltages and currents which all vary sinusoidally; we can then representall voltages and currents by complex numbers, using the exponential notationdescribed in Chapter 23 of Vol. I. Thus a time-varying voltage V (t) will bewritten

(22.1)where ˆV represents a complex number that is independent of t. It is, of course,understood that the actual time-varying voltage V (t) is given by the real part ofthe complex function on the right-hand side of the equation.

V (t) = ˆV eiωt,

22-1

Similarly, all of our other time-varying quantities will be taken to vary sinu-

soidally at the same frequency ω. So we write

I = ˆI eiωtE = ˆE eiωtE = ˆE eiωt

(current),(emf),(electric ﬁeld),

(22.2)

and so on.Most of the time we will write our equations in terms of V , I, E, . . . (insteadof in terms of ˆV , ˆI, ˆE, . . . ), remembering, though, that the time variations areas given in (22.2).In our earlier discussion of circuits we assumed that such things as inductances,capacitances, and resistances were familiar to you. We want now to look in alittle a more detail at what is meant by these idealized circuit elements. Webegin with the inductance.

An inductance is made by winding many turns of wire in the form of a coil andbringing the two ends out to terminals at some distance from the coil, as shownin Fig. 22-1. We want to assume that the magnetic ﬁeld produced by currents inthe coil does not spread out strongly all over space and interact with other partsof the circuit. This is usually arranged by winding the coil in a doughnut-shapedform, or by conﬁning the magnetic ﬁeld by winding the coil on a suitable ironcore, or by placing the coil in some suitable metal box, as indicated schematicallyin Fig. 22-1. In any case, we assume that there is a negligible magnetic ﬁeld inthe external region near the terminals a and b. We are also going to assume thatwe can neglect any electrical resistance in the wire of the coil. Finally, we willassume that we can neglect the amount of electrical charge that appears on thesurface of a wire in building up the electric ﬁelds.

With all these approximations we have what we call an「ideal」inductance.(We will come back later and discuss what happens in a real inductance.) For anideal inductance we say that the voltage across the terminals is equal to L(dI/dt).Let’s see why that is so. When there is a current through the inductance, amagnetic ﬁeld proportional to the current is built up inside the coil. If the currentchanges with time, the magnetic ﬁeld also changes. In general, the curl of E isequal to −∂B/∂t; or, put diﬀerently, the line integral of E all the way around anyclosed path is equal to the negative of the rate of change of the ﬂux of B throughthe loop. Now suppose we consider the following path: Begin at terminal a andgo along the coil (staying always inside the wire) to terminal b; then return fromterminal b to terminal a through the air in the space outside the inductance. Theline integral of E around this closed path can be written as the sum of two parts:

E · ds =

E · ds +

E · ds.

(22.3)

I

Z b

Z a

aviacoil

b

outside

As we have seen before, there can be no electric ﬁelds inside a perfect conductor.(The smallest ﬁelds would produce inﬁnite currents.) Therefore the integral froma to b via the coil is zero. The whole contribution to the line integral of E comesfrom the path outside the inductance from terminal b to terminal a. Since wehave assumed that there are no magnetic ﬁelds in the space outside of the「box,」this part of the integral is independent of the path chosen and we can deﬁne thepotentials of the two terminals. The diﬀerence of these two potentials is what wecall the voltage diﬀerence, or simply the voltage V , so we have

Z a

I

V = −

E · ds = −

E · ds.

b

The complete line integral is what we have before called the electromotiveforce E and is, of course, equal to the rate of change of the magnetic ﬂux in the22-2

Fig. 22-1. An inductance.

coil. We have seen earlier that this emf is equal to the negative rate of change ofthe current, so we have

where L is the inductance of the coil. Since dI/dt = iωI, we have

V = −E = L

dIdt

,

V = iωLI.

(22.4)

The way we have described the ideal inductance illustrates the general ap-proach to other ideal circuit elements—usually called「lumped」elements. Theproperties of the element are described completely in terms of currents andvoltages that appear at the terminals. By making suitable approximations, itis possible to ignore the great complexities of the ﬁelds that appear inside theobject. A separation is made between what happens inside and what happensoutside.

For all the circuit elements we will ﬁnd a relation like the one in Eq. (22.4), inwhich the voltage is proportional to the current with a proportionality constantthat is, in general, a complex number. This complex coeﬃcient of proportionalityis called the impedance and is usually written as z (not to be confused with thez-coordinate). It is, in general, a function of the frequency ω. So for any lumpedelement we write

For an inductance, we have

=

VI

ˆVˆI

= z.

(22.5)

(22.6)

z (inductance) = zL = iωL.

Fig. 22-2. A capacitor (or condenser).

Now let’s look at a capacitor from the same point of view.* A capacitorconsists of a pair of conducting plates from which two wires are brought out tosuitable terminals. The plates may be of any shape whatsoever, and are oftenseparated by some dielectric material. We illustrate such a situation schematicallyin Fig. 22-2. Again we make several simplifying assumptions. We assume that theplates and the wires are perfect conductors. We also assume that the insulationbetween the plates is perfect, so that no charges can ﬂow across the insulationfrom one plate to the other. Next, we assume that the two conductors are closeto each other but far from all others, so that all ﬁeld lines which leave one plateend up on the other. Then there are always equal and opposite charges on thetwo plates and the charges on the plates are much larger than the charges onthe surfaces of the lead-in wires. Finally, we assume that there are no magneticﬁelds close to the capacitor.

Suppose now we consider the line integral of E around a closed loop whichstarts at terminal a, goes along inside the wire to the top plate of the capacitor,jumps across the space between the plates, passes from the lower plate toterminal b through the wire, and returns to terminal a in the space outside thecapacitor. Since there is no magnetic ﬁeld, the line integral of E around thisclosed path is zero. The integral can be broken down into three parts:

E · ds =

E · ds +

E · ds +

E · ds.

(22.7)

alongwires

betweenplates

b

outside

The integral along the wires is zero, because there are no electric ﬁelds insideperfect conductors. The integral from b to a outside the capacitor is equal to thenegative of the potential diﬀerence between the terminals. Since we imagined

* There are people who say we should call the objects by the names「inductor」and「capacitor」and call their properties「inductance」and「capacitance」(by analogy with「resistor」and「resistance」). We would rather use the words you will hear in the laboratory. Most peoplestill say「inductance」for both the physical coil and its inductance L. The word「capacitor」seems to have caught on—although you will still hear「condenser」fairly often—and most peoplestill prefer the sound of「capacity」to「capacitance.」

22-3

I

Z

Z

Z a

that the two plates are in some way isolated from the rest of the world, the totalcharge on the two plates must be zero; if there is a charge Q on the upper plate,there is an equal, opposite charge −Q on the lower plate. We have seen earlierthat if two conductors have equal and opposite charges, plus and minus Q, thepotential diﬀerence between the plates is equal to Q/C, where C is called thecapacity of the two conductors. From Eq. (22.7) the potential diﬀerence betweenthe terminals a and b is equal to the potential diﬀerence between the plates. Wehave, therefore, that

V = QC

.

The electric current I entering the capacitor through terminal a (and leavingthrough terminal b) is equal to dQ/dt, the rate of change of the electric chargeon the plates. Writing dV /dt as iωV , we can put the voltage current relationshipfor a capacitor in the following way:

or

iωV = IC

V = IiωC

,

.

The impedance z of a capacitor, is then

z (capacitor) = zC = 1

iωC

.

(22.8)

(22.9)

The third element we want to consider is a resistor. However, since we havenot yet discussed the electrical properties of real materials, we are not yet readyto talk about what happens inside a real conductor. We will just have to acceptas fact that electric ﬁelds can exist inside real materials, that these electric ﬁeldsgive rise to a ﬂow of electric charge—that is, to a current—and that this currentis proportional to the integral of the electric ﬁeld from one end of the conductorto the other. We then imagine an ideal resistor constructed as in the diagramof Fig. 22-3. Two wires which we take to be perfect conductors go from theterminals a and b to the two ends of a bar of resistive material. Following ourusual line of argument, the potential diﬀerence between the terminals a and bis equal to the line integral of the external electric ﬁeld, which is also equal tothe line integral of the electric ﬁeld through the bar of resistive material. It thenfollows that the current I through the resistor is proportional to the terminalvoltage V :

I = VR

,

where R is called the resistance. We will see later that the relation betweenthe current and the voltage for real conducting materials is only approximatelylinear. We will also see that this approximate proportionality is expected to beindependent of the frequency of variation of the current and voltage only if thefrequency is not too high. For alternating currents then, the voltage across aresistor is in phase with the current, which means that the impedance is a realnumber:

z (resistance) = zR = R.

(22.10)Our results for the three lumped circuit elements—the inductor, the capacitor,and the resistor—are summarized in Fig. 22-4. In this ﬁgure, as well as in thepreceding ones, we have indicated the voltage by an arrow that is directed fromone terminal to another. If the voltage is「positive」—that is, if the terminal a isat a higher potential than the terminal b—the arrow indicates the direction of apositive「voltage drop.」Although we are talking about alternating currents, we can of course includethe special case of circuits with steady currents by taking the limit as thefrequency ω goes to zero. For zero frequency—that is, for dc—the impedance ofan inductance goes to zero; it becomes a short circuit. For dc, the impedance of22-4

Fig. 22-3. A resistor

Fig. 22-4. The ideal lumped circuit ele-

ments (passive).

a condenser goes to inﬁnity; it becomes an open circuit. Since the impedance ofa resistor is independent of frequency, it is the only element left when we analyzea circuit for dc.

In the circuit elements we have described so far, the current and voltage areproportional to each other. If one is zero, so also is the other. We usually think interms like these: An applied voltage is「responsible」for the current, or a current「gives rise to」a voltage across the terminals; so in a sense the elements「respond」to the「applied」external conditions. For this reason these elements are calledpassive elements. They can thus be contrasted with the active elements, such asthe generators we will consider in the next section, which are the sources of theoscillating currents or voltages in a circuit.

22-2 GeneratorsNow we want to talk about an active circuit element—one that is a source ofthe currents and voltages in a circuit—namely, a generator.Suppose that we have a coil like an inductance except that it has very fewturns, so that we may neglect the magnetic ﬁeld of its own current. This coil,however, sits in a changing magnetic ﬁeld such as might be produced by a rotatingmagnet, as sketched in Fig. 22-5. (We have seen earlier that such a rotatingmagnetic ﬁeld can also be produced by a suitable set of coils with alternatingcurrents.) Again we must make several simplifying assumptions. The assumptionswe will make are all the ones that we described for the case of the inductance. Inparticular, we assume that the varying magnetic ﬁeld is restricted to a deﬁniteregion in the vicinity of the coil and does not appear outside the generator in thespace between the terminals.

Following closely the analysis we made for the inductance, we consider the lineintegral of E around a complete loop that starts at terminal a, goes through thecoil to terminal b and returns to its starting point in the space between the twoterminals. Again we conclude that the potential diﬀerence between the terminalsis equal to the total line integral of E around the loop:

I

V = −

E · ds.

This line integral is equal to the emf in the circuit, so the potential diﬀerence Vacross the terminals of the generator is also equal to the rate of change of themagnetic ﬂux linking the coil:

V = −E = ddt

(ﬂux).

(22.11)

For an ideal generator we assume that the magnetic ﬂux linking the coil is deter-mined by external conditions—such as the angular velocity of a rotating magneticﬁeld—and is not inﬂuenced in any way by the currents through the generator.Thus a generator—at least the ideal generator we are considering—is not animpedance. The potential diﬀerence across its terminals is determined by the ar-bitrarily assigned electromotive force E(t). Such an ideal generator is representedby the symbol shown in Fig. 22-6. The little arrow represents the direction of theemf when it is positive. A positive emf in the generator of Fig. 22-6 will producea voltage V = E, with the terminal a at a higher potential than the terminal b.There is another way to make a generator which is quite diﬀerent on theinside but which is indistinguishable from the one we have just described insofaras what happens beyond its terminals. Suppose we have a coil of wire which isrotated in a ﬁxed magnetic ﬁeld, as indicated in Fig. 22-7. We show a bar magnetto indicate the presence of a magnetic ﬁeld; it could, of course, be replaced byany other source of a steady magnetic ﬁeld, such as an additional coil carrying asteady current. As shown in the ﬁgure, connections from the rotating coil aremade to the outside world by means of sliding contacts or「slip rings.」Again, weare interested in the potential diﬀerence that appears across the two terminals22-5

Fig. 22-5. A generator consisting of a

ﬁxed coil and a rotating magnetic ﬁeld.

Fig. 22-6. Symbol for an ideal generator.

Fig. 22-7. A generator consisting of a

coil rotating in a ﬁxed magnetic ﬁeld.

a and b, which is of course the integral of the electric ﬁeld from terminal a toterminal b along a path outside the generator.Now in the system of Fig. 22-7 there are no changing magnetic ﬁelds, so wemight at ﬁrst wonder how any voltage could appear at the generator terminals. Infact, there are no electric ﬁelds anywhere inside the generator. We are, as usual,assuming for our ideal elements that the wires inside are made of a perfectlyconducting material, and as we have said many times, the electric ﬁeld inside aperfect conductor is equal to zero. But that is not true. It is not true when aconductor is moving in a magnetic ﬁeld. The true statement is that the totalforce on any charge inside a perfect conductor must be zero. Otherwise therewould be an inﬁnite ﬂow of the free charges. So what is always true is that thesum of the electric ﬁeld E and the cross product of the velocity of the conductorand the magnetic ﬁeld B—which is the total force on a unit charge—must havethe value zero inside the conductor:

(in a perfect conductor),

F /unit charge = E + v × B = 0

(22.12)where v represents the velocity of the conductor. Our earlier statement thatthere is no electric ﬁeld inside a perfect conductor is all right if the velocity v ofthe conductor is zero; otherwise the correct statement is given by Eq. (22.12).Returning to our generator of Fig. 22-7, we now see that the line integral ofthe electric ﬁeld E from terminal a to terminal b through the conducting path ofthe generator must be equal to the line integral of v × B on the same path,

Z b

Z b

E · ds = −

(v × B) · ds.

(22.13)

a

inside

conductor

a

inside

conductor

It is still true, however, that the line integral of E around a complete loop,including the return from b to a outside the generator, must be zero, becausethere are no changing magnetic ﬁelds. So the ﬁrst integral in Eq. (22.13) isalso equal to V , the voltage between the two terminals. It turns out that theright-hand integral of Eq. (22.13) is just the rate of change of the ﬂux linkagethrough the coil and is therefore—by the ﬂux rule—equal to the emf in the coil.So we have again that the potential diﬀerence across the terminals is equal tothe electromotive force in the circuit, in agreement with Eq. (22.11). So whetherwe have a generator in which a magnetic ﬁeld changes near a ﬁxed coil, or onein which a coil moves in a ﬁxed magnetic ﬁeld, the external properties of thegenerators are the same. There is a voltage diﬀerence V across the terminals,which is independent of the current in the circuit but depends only on thearbitrarily assigned conditions inside the generator.

So long as we are trying to understand the operation of generators fromthe point of view of Maxwell’s equations, we might also ask about the ordinarychemical cell, like a ﬂashlight battery. It is also a generator, i.e., a voltage source,although it will of course only appear in dc circuits. The simplest kind of cell22-6

to understand is shown in Fig. 22-8. We imagine two metal plates immersedin some chemical solution. We suppose that the solution contains positive andnegative ions. We suppose also that one kind of ion, say the negative, is muchheavier than the one of opposite polarity, so that its motion through the solutionby the process of diﬀusion is much slower. We suppose next that by some meansor other it is arranged that the concentration of the solution is made to varyfrom one part of the liquid to the other, so that the number of ions of bothpolarities near, say, the lower plate is much larger than the concentration of ionsnear the upper plate. Because of their rapid mobility the positive ions will driftmore readily into the region of lower concentration, so that there will be a slightexcess of positive charge arriving at the upper plate. The upper plate will becomepositively charged and the lower plate will have a net negative charge.

As more and more charges diﬀuse to the upper plate, the potential of thisplate will rise until the resulting electric ﬁeld between the plates produces forceson the ions which just compensate for their excess mobility, so the two plates ofthe cell quickly reach a potential diﬀerence which is characteristic of the internalconstruction.

Arguing just as we did for the ideal capacitor, we see that the potential diﬀer-ence between the terminals a and b is just equal to the line integral of the electricﬁeld between the two plates when there is no longer any net diﬀusion of the ions.There is, of course, an essential diﬀerence between a capacitor and such a chemicalcell. If we short-circuit the terminals of a condenser for a moment, the capacitoris discharged and there is no longer any potential diﬀerence across the terminals.In the case of the chemical cell a current can be drawn from the terminals con-tinuously without any change in the emf—until, of course, the chemicals insidethe cell have been used up. In a real cell it is found that the potential diﬀerenceacross the terminals decreases as the current drawn from the cell increases. Inkeeping with the abstractions we have been making, however, we may imagine anideal cell in which the voltage across the terminals is independent of the current.A real cell can then be looked at as an ideal cell in series with a resistor.

22-3 Networks of ideal elements; Kirchhoﬀ’s rulesAs we have seen in the last section, the description of an ideal circuit elementin terms of what happens outside the element is quite simple. The current and thevoltage are linearly related. But what is actually happening inside the element isquite complicated, and it is quite diﬃcult to give a precise description in terms ofMaxwell’s equations. Imagine trying to give a precise description of the electricand magnetic ﬁelds of the inside of a radio which contains hundreds of resistors,capacitors, and inductors. It would be an impossible task to analyze such athing by using Maxwell’s equations. But by making the many approximationswe have described in Section 22-2 and summarizing the essential features of thereal circuit elements in terms of idealizations, it becomes possible to analyze anelectrical circuit in a relatively straightforward way. We will now show how thatis done.

Suppose we have a circuit consisting of a generator and several impedancesconnected together, as shown in Fig. 22-9. According to our approximationsthere is no magnetic ﬁeld in the region outside the individual circuit elements.Therefore the line integral of E around any curve which does not pass throughany of the elements is zero. Consider then the curve Γ shown by the broken linewhich goes all the way around the circuit in Fig. 22-9. The line integral of Earound this curve is made up of several pieces. Each piece is the line integralfrom one terminal of a circuit element to the other. This line integral we havecalled the voltage drop across the circuit element. The complete line integral isthen just the sum of the voltage drops across all of the elements in the circuit:

I

E · ds =X

Vn.

Since the line integral is zero, we have that the sum of the potential diﬀerences22-7

Fig. 22-8. A chemical cell.

Fig. 22-9. The sum of the voltage drops

around any closed path is zero.

around a complete loop of a circuit is equal to zero:

X

Vn = 0.

(22.14)

aroundany loop

This result follows from one of Maxwell’s equations—that in a region where thereare no magnetic ﬁelds the line integral of E around any complete loop is zero.Suppose we consider now a circuit like that shown in Fig. 22-10. The horizontalline joining the terminals a, b, c, and d is intended to show that these terminalsare all connected, or that they are joined by wires of negligible resistance. Inany case, the drawing means that terminals a, b, c, and d are all at the samepotential and, similarly, that the terminals e, f, g, and h are also at one commonpotential. Then the voltage drop V across each of the four elements is the same.Now one of our idealizations has been that negligible electrical charges accu-mulate on the terminals of the impedances. We now assume further that anyelectrical charges on the wires joining terminals can also be neglected. Then theconservation of charge requires that any charge which leaves one circuit elementimmediately enters some other circuit element. Or, what is the same thing, werequire that the algebraic sum of the currents which enter any given junctionmust be zero. By a junction, of course, we mean any set of terminals such asa, b, c, and d which are connected. Such a set of connected terminals is usuallycalled a「node.」The conservation of charge then requires that for the circuit ofFig. 22-10,

(22.15)The sum of the currents entering the node which consists of the four terminalse, f, g, and h must also be zero:

I1 − I2 − I3 − I4 = 0.

(22.16)This is, of course, the same as Eq. (22.15). The two equations are not independent.The general rule is that the sum of the currents into any node must be zero:

− I1 + I2 + I3 + I4 = 0.

In = 0.

(22.17)

intoa node

Our earlier conclusion that the sum of the voltage drops around a closed loopis zero must apply to any loop in a complicated circuit. Also, our result that thesum of the currents into a node is zero must be true for any node. These twoequations are known as Kirchhoﬀ’s rules. With these two rules it is possible tosolve for the currents and voltages in any network whatever.Suppose we consider the more complicated circuit of Fig. 22-11. How shall weﬁnd the currents and voltages in this circuit? We can ﬁnd them in the followingstraightforward way. We consider separately each of the four subsidiary closedloops, which appear in the circuit. (For instance, one loop goes from terminal ato terminal b to terminal e to terminal d and back to terminal a.) For each ofthe loops we write the equation for the ﬁrst of Kirchhoﬀ’s rules—that the sumof the voltages around each loop is equal to zero. We must remember to countthe voltage drop as positive if we are going in the direction of the current andnegative if we are going across an element in the direction opposite to the current;and we must remember that the voltage drop across a generator is the negativeof the emf in that direction. Thus if we consider the small loop that starts andends at terminal a we have the equation

z1I1 + z3I3 + z4I4 − E1 = 0.

Applying the same rule to the remaining loops, we would get three more equationsof the same kind.

Next, we must write the current equation for each of the nodes in the circuit.For example, summing the currents into the node at terminal b gives the equation

I1 − I3 − I2 = 0.

22-8

X

Fig. 22-10. The sum of the currents into

any node is zero.

Fig. 22-11. Analyzing a circuit with Kirch-

hoﬀ’s rules.

Similarly, for the node labeled e we would have the current equation

I3 − I4 + I8 − I5 = 0.

For the circuit shown there are ﬁve such current equations. It turns out, however,that any one of these equations can be derived from the other four; there are,therefore, only four independent current equations. We thus have a total of eightindependent, linear equations: the four voltage equations and the four currentequations. With these eight equations we can solve for the eight unknown currents.Once the currents are known the circuit is solved. The voltage drop across anyelement is given by the current through that element times its impedance (or, inthe case of the voltage sources, it is already known).

We have seen that when we write the current equations, we get one equationwhich is not independent of the others. Generally it is also possible to write downtoo many voltage equations. For example, in the circuit of Fig. 22-11, although wehave considered only the four small loops, there are a large number of other loopsfor which we could write the voltage equation. There is, for example, the loopalong the path abcf eda. There is another loop which follows the path abcf ehgda.You can see that there are many loops. In analyzing complicated circuits it isvery easy to get too many equations. There are rules which tell us how to proceedso that only the minimum number of equations is written down, but usually witha little thought it is possible to see how to get the right number of equationsin the simplest form. Besides, writing an extra equation or two doesn’t do anyharm. They will not lead to any wrong answers, only perhaps a little unnecessaryalgebra.

In Chapter 25 of Vol. I we showed that if the two impedances z1 and z2 are

in series, they are equivalent to a single impedance zs given by

(22.18)We also showed that if the two impedances are connected in parallel, they areequivalent to the single impedance zp given by

zs = z1 + z2.

zp =

1

(1/z1) + (1/z2) = z1z2z1 + z2

.

(22.19)

If you look back you will see that in deriving these results we were in eﬀectmaking use of Kirchhoﬀ’s rules. It is often possible to analyze a complicatedcircuit by repeated application of the formulas for series and parallel impedances.For instance, the circuit of Fig. 22-12 can be analyzed that way. First, theimpedances z4 and z5 can be replaced by their parallel equivalent, and so also canz6 and z7. Then the impedance z2 can be combined with the parallel equivalentof z6 and z7 by the series rule. Proceeding in this way, the whole circuit can bereduced to a generator in series with a single impedance Z. The current throughthe generator is then just E/Z. Then by working backward one can solve for thecurrents in each of the impedances.There are, however, quite simple circuits which cannot be analyzed by thismethod, as for example the circuit of Fig. 22-13. To analyze this circuit we must

Fig. 22-12. A circuit which can be ana-lyzed in terms of series and parallel combi-nations.

Fig. 22-13. A circuit that cannot be ana-lyzed in terms of series and parallel combi-nations.

22-9

write down the current and voltage equations from Kirchhoﬀ’s rules. Let’s do it.There is just one current equation:

so we know immediately that

I1 + I2 + I3 = 0,

I3 = −(I1 + I2).

We can save ourselves some algebra if we immediately make use of this result inwriting the voltage equations. For this circuit there are two independent voltageequations; they are

−E1 + I2z2 − I1z1 = 0

and

E2 − (I1 + I2)z3 − I2z2 = 0.

There are two equations and two unknown currents. Solving these equations forI1 and I2, we get

I1 = z2E2 − (z2 + z3)E1z1(z2 + z3) + z2z3

I2 =

z1E2 + z3E1

z1(z2 + z3) + z2z3

.

(22.20)

(22.21)

and

The third current is obtained from the sum of these two.

Another example of a circuit that cannot be analyzed by using the rules forseries and parallel impedance is shown in Fig. 22-14. Such a circuit is called a「bridge.」It appears in many instruments used for measuring impedances. Withsuch a circuit one is usually interested in the question: How must the variousimpedances be related if the current through the impedance z3 is to be zero? Weleave it for you to ﬁnd the conditions for which this is so.

Fig. 22-14. A bridge circuit.

22-4 Equivalent circuitsSuppose we connect a generator E to a circuit containing some complicatedinterconnection of impedances, as indicated schematically in Fig. 22-15(a). Allof the equations we get from Kirchhoﬀ’s rules are linear, so when we solve themfor the current I through the generator, we will get that I is proportional to E.We can write

I = Ezeﬀ

,

where now zeﬀ is some complex number, an algebraic function of all the elementsin the circuit. (If the circuit contains no generators other than the one shown,there is no additional term independent of E.) But this equation is just whatwe would write for the circuit of Fig. 22-15(b). So long as we are interestedonly in what happens to the left of the two terminals a and b, the two circuitsof Fig. 22-15 are equivalent. We can, therefore, make the general statementthat any two-terminal network of passive elements can be replaced by a singleimpedance zeﬀ without changing the currents and voltages in the rest of thecircuit. This statement is of course, just a remark about what comes out ofKirchhoﬀ’s rules—and ultimately from the linearity of Maxwell’s equations.

The idea can be generalized to a circuit that contains generators as well asimpedances. Suppose we look at such a circuit「from the point of view」of one ofthe impedances, which we will call zn, as in Fig. 22-16(a). If we were to solvethe equation for the whole circuit, we would ﬁnd that the voltage Vn betweenthe two terminals a and b is a linear function of I, which we can write

Vn = A − BIn,

(22.22)

where A and B depend on the generators and impedances in the circuit to the22-10

Fig. 22-15. Any two-terminal network ofpassive elements is equivalent to an eﬀectiveimpedance.

left of the terminals. For instance, for the circuit of Fig. 22-13, we ﬁnd V1 = I1z1.This can be written (by rearranging Eq. (22.20)] as

(cid:20)(cid:18) z2

z2 + z3

V1 =

(cid:19)

(cid:21)

E2 − E1

− z2z3z2 + z3

I1.

(22.23)

The complete solution is then obtained by combining this equation with the onefor the impedance z1, namely, V1 = I1z1, or in the general case, by combiningEq. (22.22) with

Vn = Inzn.

If now we consider that zn is attached to a simple series circuit of a generatorand a current, as in Fig. 22-15(b), the equation corresponding to Eq. (22.22) is

Vn = Eeﬀ − Inzeﬀ,

which is identical to Eq. (22.22) provided we set Eeﬀ = A and zeﬀ = B. So if weare interested only in what happens to the right of the terminals a and b, thearbitrary circuit of Fig. 22-16 can always be replaced by an equivalent combinationof a generator in series with an impedance.

22-5 EnergyWe have seen that to build up the current I in an inductance, the energy U =2 LI2 must be provided by the external circuit. When the current falls back to1zero, this energy is delivered back to the external circuit. There is no energy-lossmechanism in an ideal inductance. When there is an alternating current throughan inductance, energy ﬂows back and forth between it and the rest of the circuit,but the average rate at which energy is delivered to the circuit is zero. We say thatan inductance is a nondissipative element; no electrical energy is dissipated—thatis,「lost」—in it.2 CV 2, is returned to the externalcircuit when a condenser is discharged. When a condenser is in an ac circuitenergy ﬂows in and out of it, but the net energy ﬂow in each cycle is zero. Anideal condenser is also a nondissipative element.

Similarly, the energy of a condenser, U = 1

We know that an emf is a source of energy. When a current I ﬂows in the direc-tion of the emf, energy is delivered to the external circuit at the rate dU/dt = EI.If current is driven against the emf—by other generators in the circuit—the emfwill absorb energy at the rate EI; since I is negative, dU/dt will also be negative.If a generator is connected to a resistor R, the current through the resistoris I = E/R. The energy being supplied by the generator at the rate EI is beingabsorbed by the resistor. This energy goes into heat in the resistor and is lostfrom the electrical energy of the circuit. We say that electrical energy is dissipatedin a resistor. The rate at which energy is dissipated in a resistor is dU/dt = RI2.In an ac circuit the average rate of energy lost to a resistor is the averageof RI2 over one cycle. Since I = ˆIeiωt—by which we really mean that I variesas cos ωt—the average of I2 over one cycle is |ˆI|2/2, since the peak current is |ˆI|and the average of cos2 ωt is 1/2.What about the energy loss when a generator is connected to an arbitraryimpedance z? (By「loss」we mean, of course, conversion of electrical energy intothermal energy.) Any impedance z can be written as the sum of its real andimaginary parts. That is,(22.24)where R and X are real numbers. From the point of view of equivalent circuitswe can say that any impedance is equivalent to a resistance in series with a pureimaginary impedance—called a reactance—as shown in Fig. 22-17.We have seen earlier that any circuit that contains only L’s and C’s has animpedance that is a pure imaginary number. Since there is no energy loss into anyof the L’s and C’s on the average, a pure reactance containing only L’s and C’s willhave no energy loss. We can see that this must be true in general for a reactance.22-11

z = R + iX,

Fig. 22-16. Any two-terminal networkcan be replaced by a generator in series withan impedance.

Fig. 22-17. Any impedance is equivalentto a series combination of a pure resistanceand a pure reactance.

If a generator with the emf E is connected to the impedance z of Fig. 22-17,

the emf must be related to the current I from the generator by

E = I(R + iX).

(22.25)

To ﬁnd the average rate at which energy is delivered, we want the average ofthe product EI. Now we must be careful. When dealing with such products, wemust deal with the real quantities E(t) and I(t). (The real parts of the complexfunctions will represent the actual physical quantities only when we have linearequations; now we are concerned with products, which are certainly not linear.)Suppose we choose our origin of t so that the amplitude ˆI is a real number,let’s say I0; then the actual time variation I is given by

The emf of Eq. (22.25) is the real part of

I = I0 cos ωt.

I0eiωt(R + iX)

or

E = I0R cos ωt − I0X sin ωt.

(22.26)The two terms in Eq. (22.26) represent the voltage drops across R and X inFig. 22-17. We see that the voltage drop across the resistance is in phase withthe current, while the voltage drop across the purely reactive part is out of phasewith the current.The average rate of energy loss, hPiav, from the generator is the integral of

the product EI over one cycle divided by the period T; in other words,

Z T

Z T

0

0 R cos2 ωt dt − 1I2

0 X cos ωt sin ωt dt.I2

EI dt = 1

hPiav = 1The ﬁrst integral is 1

0

T

T0 R, and the second integral is zero. So the average2 I2energy loss in an impedance z = R + iX depends only on the real part of z, andis I20 R/2, which is in agreement with our earlier result for the energy loss in aresistor. There is no energy loss in the reactive part.

T

0

Z T

22-6 A ladder networkWe would like now to consider an interesting circuit which can be analyzedin terms of series and parallel combinations. Suppose we start with the circuitof Fig. 22-18(a). We can see right away that the impedance from terminal a toterminal b is simply z1 + z2. Now let’s take a little harder circuit, the one shownin Fig. 22-18(b). We could analyze this circuit using Kirchhoﬀ’s rules, but it isalso easy to handle with series and parallel combinations. We can replace thetwo impedances on the right-hand end by a single impedance z3 = z1 + z2, as inpart (c) of the ﬁgure. Then the two impedances z2 and z3 can be replaced bytheir equivalent parallel impedance z4, as shown in part (d) of the ﬁgure. Finally,z1 and z4 are equivalent to a single impedance z5, as shown in part (e).Now we may ask an amusing question: What would happen if in the networkof Fig. 22-18(b) we kept on adding more sections forever—as we indicate bythe dashed lines in Fig. 22-19(a)? Can we solve such an inﬁnite network? Well,

Fig. 22-18. The eﬀective impedance of

a ladder.

Fig. 22-19. The eﬀective impedance of an inﬁnite ladder.

22-12

that’s not so hard. First, we notice that such an inﬁnite network is unchanged ifwe add one more section at the「front」end. Surely, if we add one more sectionto an inﬁnite network it is still the same inﬁnite network. Suppose we call theimpedance between the two terminals a and b of the inﬁnite network z0; thenthe impedance of all the stuﬀ to the right of the two terminals c and d is also z0.Therefore, so far as the front end is concerned, we can represent the networkas shown in Fig. 22-19(b). Forming the parallel combination of z2 with z0 andadding the result in series with z1, we can immediately write down the impedanceof this circuit:

z = z1 +

z = z1 + z2z0z2 + z0But this impedance is also equal to z0, so we have the equation

(1/z2) + (1/z0)

or

.

1

We can solve for z0 to get

z0 = z1 + z2z0z2 + z0

.

2 +q(z2

z0 = z1

1/4) + z1z2.

(22.27)So we have found the solution for the impedance of an inﬁnite ladder of repeatedseries and parallel impedances. The impedance z0 is called the characteristicimpedance of such an inﬁnite network.Let’s now consider a speciﬁc example in which the series element is aninductance L and the shunt element is a capacitance C, as shown in Fig. 22-20(a).In this case we ﬁnd the impedance of the inﬁnite network by setting z1 = iωLand z2 = 1/iωC. Notice that the ﬁrst term, z1/2, in Eq. (22.27) is just one-halfthe impedance of the ﬁrst element. It would therefore seem more natural, orat least somewhat simpler, if we were to draw our inﬁnite network as shown inFig. 22-20(b). Looking at the inﬁnite network from the terminal a0 we would seethe characteristic impedance

z0 =p(L/C) − (ω2L2/4).

(22.28)Now there are two interesting cases, depending on the frequency ω. If ω2 is lessthan 4/LC, the second term in the radical will be smaller than the ﬁrst, and theimpedance z0 will be a real number. On the other hand, if ω2 is greater than 4/LCthe impedance z0 will be a pure imaginary number which we can write as

z0 = ip(ω2L2/4) − (L/C).

low p4/LC? For higher frequencies the impedance is purely imaginary, in

We have said earlier that a circuit which contains only imaginary impedances,such as inductances and capacitances, will have an impedance which is purelyimaginary. How can it be then that for the circuit we are now studying—whichhas only L’s and C’s—the impedance is a pure resistance for frequencies be-agreement with our earlier statement. For lower frequencies the impedance isa pure resistance and will therefore absorb energy. But how can the circuitcontinuously absorb energy, as a resistance does, if it is made only of inductancesand capacitances? Answer: Because there is an inﬁnite number of inductancesand capacitances, so that when a source is connected to the circuit, it suppliesenergy to the ﬁrst inductance and capacitance, then to the second, to the third,and so on. In a circuit of this kind, energy is continually absorbed from thegenerator at a constant rate and ﬂows constantly out into the network, supplyingenergy which is stored in the inductances and capacitances down the line.

This idea suggests an interesting point about what is happening in the circuit.We would expect that if we connect a source to the front end, the eﬀects ofthis source will be propagated through the network toward the inﬁnite end.The propagation of the waves down the line is much like the radiation from anantenna which absorbs energy from its driving source; that is, we expect sucha propagation to occur when the impedance is real, which occurs if ω is less

thanp4/LC. But when the impedance is purely imaginary, which happens forω greater thanp4/LC, we would not expect to see any such propagation.

22-13

Fig. 22-20. An L-C ladder drawn in two

equivalent ways.

22-7 FiltersWe saw in the last section that the inﬁnite ladder network of Fig. 22-20absorbs energy continuously if it is driven at a frequency below a certain critical

frequency p4/LC, which we will call the cutoﬀ frequency ω0. We suggested

that this eﬀect could be understood in terms of a continuous transport of energydown the line. On the other hand, at high frequencies, for w > ω0, there is nocontinuous absorption of energy; we should then expect that perhaps the currentsdon’t「penetrate」very far down the line. Let’s see whether these ideas are right.Suppose we have the front end of the ladder connected to some ac generatorand we ask what the voltage looks like at, say, the 754th section of the ladder.Since the network is inﬁnite, whatever happens to the voltage from one sectionto the next is always the same; so let’s just look at what happens when we gofrom some section, say the nth to the next. We will deﬁne the currents In andvoltages Vn as shown in Fig. 22-21(a).

Fig. 22-21. Finding the propagation factor of a ladder.

We can get the voltage Vn+1 from Vn by remembering that we can always re-place the rest of the ladder after the nth section by its characteristic impedance z0;then we need only analyze the circuit of Fig. 22-21(b). First, we notice thatany Vn, since it is across z0, must equal Inz0. Also, the diﬀerence between Vnand Vn+1 is just Inz1:

So we get the ratio

Vn − Vn+1 = Inz1 = Vn

Vn+1Vn

= 1 − z1z0

= z0 − z1

z0

z1z0

.

.

We can call this ratio the propagation factor for one section of the ladder; we’llcall it α. It is, of course, the same for all sections:

α = z0 − z1

z0

.

(22.29)

The voltage after the nth section is then

(22.30)You can now ﬁnd the voltage after 754 sections; it is just α to the 754th powertimes E.Suppose we see what α is like for the L-C ladder of Fig. 22-20(a). Using z0

Vn = αnE.

from Eq. (22.27), and z1 = iωL, we get

p(L/C) − (ω2L2/4) − i(ωL/2)p(L/C) − (ω2L2/4) + i(ωL/2) .

α =

If the driving frequency is below the cutoﬀ frequency ω0 =p4/LC, the radical

is a real number, and the magnitudes of the complex numbers in the numeratorand denominator are equal. Therefore, the magnitude of α is one; we can write

(22.31)

α = eiδ,

22-14

which means that the magnitude of the voltage is the same at every section;only its phase changes. The phase change δ is, in fact, a negative number andrepresents the「delay」of the voltage as it passes along the network.For frequencies above the cutoﬀ frequency ω0 it is better to factor out an i

from the numerator and denominator of Eq. (22.31) and rewrite it as

p(ω2L2/4) − (L/C) − (ωL/2)p(ω2L2/4) − (L/C) + (ωL/2) .

α =

(22.32)

The propagation factor α is now a real number, and a number less than one.That means that the voltage at any section is always less than the voltage at thepreceding section by the factor α. For any frequency above ω0, the voltage diesaway rapidly as we go along the network. A plot of the absolute value of α as afunction of frequency looks like the graph in Fig. 22-22.We see that the behavior of α, both above and below ω0, agrees with ourinterpretation that the network propagates energy for ω < ω0 and blocks itfor ω > ω0. We say that the network「passes」low frequencies and「rejects」or「ﬁlters out」the high frequencies. Any network designed to have its characteristicsvary in a prescribed way with frequency is called a「ﬁlter.」We have been analyzinga「low-pass ﬁlter.」

pure resistance R =pL/C.

You may be wondering why all this discussion of an inﬁnite network whichobviously cannot actually occur. The point is that the same characteristics arefound in a ﬁnite network if we ﬁnish it oﬀ at the end with an impedance equalto the characteristic impedance z0. Now in practice it is not possible to exactlyreproduce the characteristic impedance with a few simple elements—like R’s, L’s,and C’s. But it is often possible to do so with a fair approximation for a certainrange of frequencies. In this way one can make a ﬁnite ﬁlter network whoseproperties are very nearly the same as those for the inﬁnite case. For instance,the L-C ladder behaves much as we have described it if it is terminated in theIf in our L-C ladder we interchange the positions of the L’s and C’s, to makethe ladder shown in Fig. 22-23(a), we can have a ﬁlter that propagates highfrequencies and rejects low frequencies. It is easy to see what happens with thisnetwork by using the results we already have. You will notice that whenever wechange an L to a C and vice versa, we also change every iω to 1/iω. So whateverhappened at ω before will now happen at 1/ω. In particular, we can see how αwill vary with frequency by using Fig. 22-22 and changing the label on the axisto 1/ω, as we have done in Fig. 22-23(b).The low-pass and high-pass ﬁlters we have described have various technicalapplications. An L-C low-pass ﬁlter is often used as a「smoothing」ﬁlter in adc power supply. If we want to manufacture dc power from an ac source, webegin with a rectiﬁer which permits current to ﬂow only in one direction. Fromthe rectiﬁer we get a series of pulses that look like the function V (t) shown inFig. 22-24, which is lousy dc, because it wobbles up and down. Suppose wewould like a nice pure dc, such as a battery provides. We can come close to thatby putting a low-pass ﬁlter between the rectiﬁer and the load.

We know from Chapter 50 of Vol. I that the time function in Fig. 22-24 canbe represented as a superposition of a constant voltage plus a sine wave, plus ahigher-frequency sine wave, plus a still higher-frequency sine wave, etc.—by aFourier series. If our ﬁlter is linear (if, as we have been assuming, the L’s and C’sdon’t vary with the currents or voltages) then what comes out of the ﬁlter isthe superposition of the outputs for each component at the input. If we arrangethat the cutoﬀ frequency ω0 of our ﬁlter is well below the lowest frequency in thefunction V (t), the dc (for which ω = 0) goes through ﬁne, but the amplitude ofthe ﬁrst harmonic will be cut down a lot. And amplitudes of the higher harmonicswill be cut down even more. So we can get the output as smooth as we wish,depending only on how many ﬁlter sections we are willing to buy.

A high-pass ﬁlter is used if one wants to reject certain low frequencies. Forinstance, in a phonograph ampliﬁer a high-pass ﬁlter may be used to let the22-15

Fig. 22-22. The propagation factor of a

section of an L-C ladder.

Fig. 22-23. (a) A high-pass ﬁlter; (b) its

propagation factor as a function of 1/ω.

Fig. 22-24. The output voltage of a full-

wave rectiﬁer.

music through, while keeping out the low-pitched rumbling from the motor ofthe turntable.

It is also possible to make「band-pass」ﬁlters that reject frequencies belowsome frequency ω1 and above another frequency ω2 (greater than ω1), but passthe frequencies between ω1 and ω2. This can be done simply by putting togethera high-pass and a low-pass ﬁlter, but it is more usually done by making a ladder inwhich the impedances z1 and z2 are more complicated—being each a combinationof L’s and C’s. Such a band-pass ﬁlter might have a propagation constant likethat shown in Fig. 22-25(a). It might be used, for example, in separating signalsthat occupy only an interval of frequencies, such as each of the many voicechannels in a high-frequency telephone cable, or the modulated carrier of a radiotransmission.

We have seen in Chapter 25 of Vol. I that such ﬁltering can also be doneusing the selectivity of an ordinary resonance curve, which we have drawn forcomparison in Fig. 22-25(b). But the resonant ﬁlter is not as good for somepurposes as the band-pass ﬁlter. You will remember (Chapter 48, Vol. I) thatwhen a carrier of frequency ωc is modulated with a「signal」frequency ωs, thetotal signal contains not only the carrier frequency but also the two side-bandfrequencies ωc + ωs and ωc − ωs. With a resonant ﬁlter, these side-bands arealways attenuated somewhat, and the attenuation is more, the higher the signalfrequency, as you can see from the ﬁgure. So there is a poor「frequency response.」The higher musical tones don’t get through. But if the ﬁltering is done with aband-pass ﬁlter designed so that the width ω2 − ω1 is at least twice the highestsignal frequency, the frequency response will be「ﬂat」for the signals wanted.We want to make one more point about the ladder ﬁlter: the L-C ladderof Fig. 22-20 is also an approximate representation of a transmission line. Ifwe have a long conductor that runs parallel to another conductor—such as awire in a coaxial cable, or a wire suspended above the earth—there will be somecapacitance between the two conductors and also some inductance due to themagnetic ﬁeld between them. If we imagine the line as broken up into smalllengths ∆‘, each length will look like one section of the L-C ladder with a seriesinductance ∆L and a shunt capacitance ∆C. We can then use our results for theladder ﬁlter. If we take the limit as ∆‘ goes to zero, we have a good descriptionof the transmission line. Notice that as ∆‘ is made smaller and smaller, both ∆Land ∆C decrease, but in the same proportion, so that the ratio ∆L/∆C remainsconstant. So if we take the limit of Eq. (22.28) as ∆L and ∆C go to zero, weﬁnd that the characteristic impedance z0 is a pure resistance whose magnitudeare the inductance and capacitance of a unit length of the line; then we have

isp∆L/∆C. We can also write the ratio ∆L/∆C as L0/C0, where L0 and C0

p4/LC goes to inﬁnity. There is no cutoﬀ frequency for an ideal transmission

You will also notice that as ∆L and ∆C go to zero, the cutoﬀ frequency ω0 =

line.

r L0

.

C0

z0 =

(22.33)

Fig. 22-25. (a) A band-pass ﬁlter. (b) A

simple resonant ﬁlter.

22-8 Other circuit elementsWe have so far deﬁned only the ideal circuit impedances—the inductance, thecapacitance, and the resistance—as well as the ideal voltage generator. We wantnow to show that other elements, such as mutual inductances or transistors orvacuum tubes, can be described by using only the same basic elements. Supposethat we have two coils and that on purpose, or otherwise, some ﬂux from one ofthe coils links the other, as shown in Fig. 22-26(a). Then the two coils will havea mutual inductance M such that when the current varies in one of the coils,there will be a voltage generated in the other. Can we take into account such aneﬀect in our equivalent circuits? We can in the following way. We have seen that22-16

Fig. 22-26. Equivalent circuit of a mutual

inductance.

the induced emf’s in each of two interacting coils can be written as the sum oftwo parts:

E1 = −L1

E2 = −L2

± M

± M

dI1dtdI2dt

dI2dtdI1dt

,

.

(22.34)

The ﬁrst term comes from the self-inductance of the coil, and the second termcomes from its mutual inductance with the other coil. The sign of the second termcan be plus or minus, depending on the way the ﬂux from one coil links the other.Making the same approximations we used in describing an ideal inductance, wewould say that the potential diﬀerence across the terminals of each coil is equalto the electromotive force in the coil. Then the two equations of (22.34) are thesame as the ones we would get from the circuit of Fig. 22-26(b), provided theelectromotive force in each of the two circuits shown depends on the current inthe opposite circuit according to the relations

E1 = ±iωM I2,

E2 = ±iωM I1.

(22.35)

So what we can do is represent the eﬀect of the self-inductance in a normal waybut replace the eﬀect of the mutual inductance by an auxiliary ideal voltagegenerator. We must in addition, of course, have the equation that relates this emfto the current in some other part of the circuit; but so long as this equation islinear, we have just added more linear equations to our circuit equations, and allof our earlier conclusions about equivalent circuits and so forth are still correct.In addition to mutual inductances there may also be mutual capacitances. Sofar, when we have talked about condensers we have always imagined that therewere only two electrodes, but in many situations, for example in a vacuum tube,there may be many electrodes close to each other. If we put an electric charge onany one of the electrodes, its electric ﬁeld will induce charges on each of the otherelectrodes and aﬀect its potential. As an example, consider the arrangement offour plates shown in Fig. 22-27(a). Suppose these four plates are connected toexternal circuits by means of the wires A, B, C, and D. So long as we are onlyworried about electrostatic eﬀects, the equivalent circuit of such an arrangementof electrodes is as shown in part (b) of the ﬁgure. The electrostatic interactionof any electrode with each of the others is equivalent to a capacity between thetwo electrodes.

Finally, let’s consider how we should represent such complicated devices astransistors and radio tubes in an ac circuit. We should point out at the startthat such devices are often operated in such a way that the relationship betweenthe currents and voltages is not at all linear. In such cases, those statements wehave made which depend on the linearity of equations are, of course, no longercorrect. On the other hand, in many applications the operating characteristicsare suﬃciently linear that we may consider the transistors and tubes to be lineardevices. By this we mean that the alternating currents in, say, the plate ofa vacuum tube are linearly proportional to the voltages that appear on theother electrodes, say the grid voltage and the plate voltage. When we have suchlinear relationships, we can incorporate the device into our equivalent circuitrepresentation.

As in the case of the mutual inductance, our representation will have toinclude auxiliary voltage generators which describe the inﬂuence of the voltagesor currents in one part of the device on the currents or voltages in another part.For example, the plate circuit of a triode can usually be represented by a resistancein series with an ideal voltage generator whose source strength is proportional tothe grid voltage. We get the equivalent circuit shown in Fig. 22-28.* Similarly,the collector circuit of a transistor is conveniently represented as a resistor inseries with an ideal voltage generator whose source strength is proportional to the

* The equivalent circuit shown is correct only for low frequencies. For high frequencies theequivalent circuit gets much more complicated and will include various so-called「parasitic」capacitances and inductances.

22-17

Fig. 22-27. Equivalent circuit of mutual

capacitance.

Fig. 22-28. A low-frequency equivalent

circuit of a vacuum triode.

Fig. 22-29. A low-frequency equivalent

circuit of a transistor.

current from the emitter to the base of the transistor. The equivalent circuit isthen like that in Fig. 22-29. So long as the equations which describe the operationare linear, we can use such representations for tubes or transistors. Then, whenthey are incorporated in a complicated network, our general conclusions aboutthe equivalent representation of any arbitrary connection of elements is still valid.There is one remarkable thing about transistor and radio tube circuits whichis diﬀerent from circuits containing only impedances: the real part of the eﬀectiveimpedance zeﬀ can become negative. We have seen that the real part of zrepresents the loss of energy. But it is the important characteristic of transistorsand tubes that they supply energy to the circuit. (Of course they don’t just「make」energy; they take energy from the dc circuits of the power supplies andconvert it into ac energy.) So it is possible to have a circuit with a negativeresistance. Such a circuit has the property that if you connect it to an impedancewith a positive real part, i.e., a positive resistance, and arrange matters so thatthe sum of the two real parts is exactly zero, then there is no dissipation inthe combined circuit. If there is no loss of energy, any alternating voltage oncestarted will remain forever. This is the basic idea behind the operation of anoscillator or signal generator which can be used as a source of alternating voltageat any desired frequency.

22-18

23

Cavity Resonators

23-1 Real circuit elementsWhen

looked at from any one pair of terminals, any arbitrary circuit madeup of ideal impedances and generators is, at any given frequency, equivalent to agenerator E in series with an impedance z. That comes about because if we puta voltage V across the terminals and solve all the equations to ﬁnd the current I,we must get a linear relation between the current and the voltage. Since all theequations are linear, the result for I must also depend only linearly on V . Themost general linear form can be expressed as

I = 1

z

(V − E).

(23.1)

In general, both z and E may depend in some complicated way on the frequency ω.Equation (23.1), however, is the relation we would get if behind the two terminalsthere was just the generator E(ω) in series with the impedance z(ω).There is also the opposite kind of question: If we have any electromagneticdevice at all with two terminals and we measure the relation between I and V todetermine E and z as functions of frequency, can we ﬁnd a combination of our idealelements that is equivalent to the internal impedance z? The answer is that for anyreasonable—that is, physically meaningful—function z(ω), it is possible to approx-imate the situation to as high an accuracy as you wish with a circuit containinga ﬁnite set of ideal elements. We don’t want to consider the general problem now,but only look at what might be expected from physical arguments for a few cases.If we think of a real resistor, we know that the current through it will producea magnetic ﬁeld. So any real resistor should also have some inductance. Also,when a resistor has a potential diﬀerence across it, there must be charges onthe ends of the resistor to produce the necessary electric ﬁelds. As the voltagechanges, the charges will change in proportion, so the resistor will also have somecapacitance. We expect that a real resistor might have the equivalent circuitshown in Fig. 23-1. In a well-designed resistor, the so-called「parasitic」elementsL and C are small, so that at the frequencies for which it is intended, ωL is muchless than R, and 1/ωC is much greater than R. It may therefore be possible toneglect them. As the frequency is raised, however, they will eventually becomeimportant, and a resistor begins to look like a resonant circuit.

circuit is justP R+P iωL, which is equivalent to the simpler diagram of part (a).

A real inductance is also not equal to the idealized inductance, whose impe-dance is iωL. A real coil of wire will have some resistance, so at low frequencies thecoil is really equivalent to an inductance in series with some resistance, as shownin Fig. 23-2(a). But, you are thinking, the resistance and inductance are togetherin a real coil—the resistance is spread all along the wire, so it is mixed in with theinductance. We should probably use a circuit more like the one in Fig. 23-2(b),which has several little R’s and L’s in series. But the total impedance of such aAs we go up in frequency with a real coil, the approximation of an inductanceplus a resistance is no longer very good. The charges that must build up on thewires to make the voltages will become important. It is as if there were littlecondensers across the turns of the coil, as sketched in Fig. 23-3(a). We might tryto approximate the real coil by the circuit in Fig. 23-3(b). At low frequencies,this circuit can be imitated fairly well by the simpler one in part (c) of the ﬁgure(which is again the same resonant circuit we found for the high-frequency modelof a resistor). For higher frequencies, however, the more complicated circuit of23-1

23-1 Real circuit elements23-2 A capacitor at high frequencies23-3 A resonant cavity23-4 Cavity modes23-5 Cavities and resonant circuits

Review: Chapter 23, Vol. I, Resonance

Chapter 49, Vol. I, Modes

Fig. 23-1. Equivalent circuit of a real

resistor.

Fig. 23-2. The equivalent circuit of a real

inductance at low frequencies.

Fig. 23-3(b) is better. In fact, the more accurately you wish to represent theactual impedance of a real, physical inductance, the more ideal elements you willhave to use in the artiﬁcial model of it.

Let’s look a little more closely at what goes on in a real coil. The impedanceof an inductance goes as ωL, so it becomes zero at low frequencies—it is a「shortcircuit」: all we see is the resistance of the wire. As we go up in frequency, ωLsoon becomes much larger than R, and the coil looks pretty much like an idealinductance. As we go still higher, however, the capacities become important.Their impedance is proportional to 1/ωC, which is large for small ω. For smallenough frequencies a condenser is an「open circuit,」and when it is in parallelwith something else, it draws no current. But at high frequencies, the currentprefers to ﬂow into the capacitance between the turns, rather than throughthe inductance. So the current in the coil jumps from one turn to the otherand doesn’t bother to go around and around where it has to buck the emf. Soalthough we may have intended that the current should go around the loop, itwill take the easier path—the path of least impedance.If the subject had been one of popular interest, this eﬀect would have beencalled「the high-frequency barrier,」or some such name. The same kind of thinghappens in all subjects. In aerodynamics, if you try to make things go fasterthan the speed of sound when they were designed for lower speeds, they don’twork. It doesn’t mean that there is a great「barrier」there; it just means that theobject should be redesigned. So this coil which we designed as an「inductance」is not going to work as a good inductance, but as some other kind of thing atvery high frequencies. For high frequencies, we have to ﬁnd a new design.

23-2 A capacitor at high frequenciesNow we want to discuss in detail the behavior of a capacitor—a geometricallyideal capacitor—as the frequency gets larger and larger, so we can see thetransition of its properties. (We prefer to use a capacitor instead of an inductance,because the geometry of a pair of plates is much less complicated than the geometryof a coil.) We consider the capacitor shown in Fig. 23-4(a), which consists of twoparallel circular plates connected to an external generator by a pair of wires. Ifwe charge the capacitor with dc, there will be a positive charge on one plate anda negative charge on the other; and there will be a uniform electric ﬁeld betweenthe plates.

Now suppose that instead of dc, we put an ac of low frequency on the plates.(We will ﬁnd out later what is「low」and what is「high」.) Say we connect thecapacitor to a lower-frequency generator. As the voltage alternates, the positivecharge on the top plate is taken oﬀ and negative charge is put on. While thatis happening, the electric ﬁeld disappears and then builds up in the opposite

Fig. 23-3. The equivalence circuit of a

real inductance at higher frequencies.

Fig. 23-4. The electric and magnetic ﬁelds between the plates of a capacitor.

23-2

direction. As the charge sloshes back and forth slowly, the electric ﬁeld follows.At each instant the electric ﬁeld is uniform, as shown in Fig. 23-4(b), except forsome edge eﬀects which we are going to disregard. We can write the magnitudeof the electric ﬁeld as

E = E0eiωt,

(23.2)

where E0 is a constant.Now will that continue to be right as the frequency goes up? No, because asthe electric ﬁeld is going up and down, there is a ﬂux of electric ﬁeld throughany loop like Γ1 in Fig. 23-4(a). And, as you know, a changing electric ﬁeld actsto produce a magnetic ﬁeld. One of Maxwell’s equations says that when there isa varying electric ﬁeld, as there is here, there has got to be a line integral of themagnetic ﬁeld. The integral of the magnetic ﬁeld around a closed ring, multipliedby c2, is equal to the time rate-of-change of the electric ﬂux through the areainside the ring (if there are no currents):

c2I

Z

E · ds = − ddt

(ﬂux of B).

23-3

Γ

B · ds = ddt

Γ

inside Γ

E · n da.

(23.3)

So how much magnetic ﬁeld is there? That’s not very hard. Suppose that wetake the loop Γ1, which is a circle of radius r. We can see from symmetry thatthe magnetic ﬁeld goes around as shown in the ﬁgure. Then the line integralof B is 2πrB. And, since the electric ﬁeld is uniform, the ﬂux of the electric ﬁeldis simply E multiplied by πr2, the area of the circle:

c2B · 2πr = ∂∂t

E · πr2.

(23.4)

The derivative of E with respect to time is, for our alternating ﬁeld, sim-ply iωE0eiωt. So we ﬁnd that our capacitor has the magnetic ﬁeld

B = iωr

2c2 E0eiωt.

(23.5)

In other words, the magnetic ﬁeld also oscillates and has a strength proportionalto r.What is the eﬀect of that? When there is a magnetic ﬁeld that is varying,there will be induced electric ﬁelds and the capacitor will begin to act a little bitlike an inductance. As the frequency goes up, the magnetic ﬁeld gets stronger; itis proportional to the rate of change of E, and so to ω. The impedance of thecapacitor will no longer be simply 1/iωC.Let’s continue to raise the frequency and to analyze what happens morecarefully. We have a magnetic ﬁeld that goes sloshing back and forth. But thenthe electric ﬁeld cannot be uniform, as we have assumed! When there is a varyingmagnetic ﬁeld, there must be a line integral of the electric ﬁeld—because ofFaraday’s law. So if there is an appreciable magnetic ﬁeld, as begins to happenat high frequencies, the electric ﬁeld cannot be the same at all distances fromthe center. The electric ﬁeld must change with r so that the line integral of theelectric ﬁeld can equal the changing ﬂux of the magnetic ﬁeld.Let’s see if we can ﬁgure out the correct electric ﬁeld. We can do that bycomputing a「correction」to the uniform ﬁeld we originally assumed for lowfrequencies. Let’s call the uniform ﬁeld E1, which will still be E0eiωt, and writethe correct ﬁeld as

E = E1 + E2,

where E2 is the correction due to the changing magnetic ﬁeld. For any ω we willwrite the ﬁeld at the center of the condenser as E0eiωt (thereby deﬁning E0), sothat we have no correction at the center; E2 = 0 at r = 0.

To ﬁnd E2 we can use the integral form of Faraday’s law:

I

The integrals are simple if we take them for the curve Γ2, shown in Fig. 23-4(b),which goes up along the axis, out radially the distance r along the top plate,down vertically to the bottom plate, and back to the axis. The line integral of E1around this curve is, of course, zero; so only E2 contributes, and its integral isjust −E2(r)·h, where h is the spacing between the plates. (We call E positive if itpoints upward.) This is equal to minus the rate of change of the ﬂux of B, whichwe have to get by an integral over the shaded area S inside Γ2 in Fig. 23-4(b).The ﬂux through a vertical strip of width dr is B(r)h dr, so the total ﬂux is

Z

h

B(r) dr.

Setting −∂/∂t of the ﬂux equal to the line integral of E2, we have

Z

E2(r) = ∂∂t

B(r) dr.

(23.6)

Notice that the h cancels out; the ﬁelds don’t depend on the separation of theplates.

Using Eq. (23.5) for B(r), we have

E2(r) = ∂∂t

iωr24c2 E0eiωt.

The time derivative just brings down another factor iω; we get

E2(r) = − ω2r2

4c2 E0eiωt.

(23.7)

As we expect, the induced ﬁeld tends to reduce the electric ﬁeld farther out. Thecorrected ﬁeld E = E1 + E2 is then

E = E1 + E2 =

E0eiωt.

(23.8)

(cid:18)

1 − 14

ω2r2c2

(cid:19)

Fig. 23-5. The electric ﬁeld between thecapacitor plates at high frequency. (Edgeeﬀects are neglected.)

The electric ﬁeld in the capacitor is no longer uniform; it has the parabolicshape shown by the broken line in Fig. 23-5. You see that our simple capacitoris getting slightly complicated.

We could now use our results to calculate the impedance of the capacitorat high frequencies. Knowing the electric ﬁeld, we could compute the chargeson the plates and ﬁnd out how the current through the capacitor depends onthe frequency ω, but we are not interested in that problem for the moment. Weare more interested in seeing what happens as we continue to go up with thefrequency—to see what happens at even higher frequencies. Aren’t we alreadyﬁnished? No, because we have corrected the electric ﬁeld, which means thatthe magnetic ﬁeld we have calculated is no longer right. The magnetic ﬁeld ofEq. (23.5) is approximately right, but it is only a ﬁrst approximation. So let’scall it B1. We should then rewrite Eq. (23.5) as

B1 = iωr

2c2 E0eiωt.

(23.9)

You will remember that this ﬁeld was produced by the variation of E1. Now thecorrect magnetic ﬁeld will be that produced by the total electric ﬁeld E1 + E2. Ifwe write the magnetic ﬁeld as B = B1 + B2, the second term is just the additionalﬁeld produced by E2. To ﬁnd B2 we can go through the same arguments wehave used to ﬁnd B1; the line integral of B2 around the curve Γ1 is equal to therate of change of the ﬂux of E2 through Γ1. We will just have Eq. (23.4) againwith B replaced by B2 and E replaced by E2:

c2B2 · 2πr = ddt

(ﬂux of E2 through Γ1).

23-4

Since E2 varies with radius, to obtain its ﬂux we must integrate over the circularsurface inside Γ1. Using 2πr dr as the element of area, this integral is

Z r

0

E2(r) · 2πr dr.

Z

B2(r) = 1rc2

∂∂t

So we get for B2(r)

E2(r)r dr.

(23.10)

Z

Using E2(r) from Eq. (23.7), we need the integral of r3 dr, which is, of course,r4/4. Our correction to the magnetic ﬁeld becomes

B2(r) = − iω3r3

16c4 E0eiωt.

(23.11)

But we are still not ﬁnished! If the magnetic ﬁeld B is not the same as weﬁrst thought, then we have incorrectly computed E2. We must make a furthercorrection to E, which comes from the extra magnetic ﬁeld B2. Let’s call thisadditional correction to the electric ﬁeld E3. It is related to the magnetic ﬁeld B2in the same way that E2 was related to B1. We can use Eq. (23.6) all over againjust by changing the subscripts:

E3(r) = ∂∂t

B2(r) dr.

(23.12)

Using our result, Eq. (23.11), for B2, the new correction to the electric ﬁeld is

Writing our doubly corrected electric ﬁeld as E = E1 + E2 + E3, we get

64c4 E0eiωt.

E3(r) = + ω4r4(cid:19)2(cid:20)(cid:18) ωr1 − 122

c

(cid:18) ωr

(cid:19)4(cid:21)

.

c

+ 122 · 42

E = E0eiωt

(23.13)

(23.14)

The variation of the electric ﬁeld with radius is no longer the simple parabola wedrew in Fig. 23-5, but at large radii lies slightly above the curve (E1 + E2).We are not quite through yet. The new electric ﬁeld produces a new correctionto the magnetic ﬁeld, and the newly corrected magnetic ﬁeld will produce a furthercorrection to the electric ﬁeld, and on and on. However, we already have all theformulas that we need. For B3 we can use Eq. (23.10), changing the subscriptsof B and E from 2 to 3.

The next correction to the electric ﬁeld is

(cid:19)6

(cid:18) ωr(cid:19)4(cid:18) ωr

c

2c

E4 = −

1

22 · 42 · 62

(cid:18) ωr

(cid:19)2

2c

+ 1(2!)2

E0eiωt.

(cid:18) ωr

(cid:19)6

2c

(cid:21)

.

(23.15)

± ···

− 1(3!)2

(cid:20)

E = E0eiωt

1 − 1(1!)2

So to this order we have that the complete electric ﬁeld is given by

where we have written the numerical coeﬃcients in such a way that it is obvioushow the series is to be continued.

Our ﬁnal result is that the electric ﬁeld between the plates of the capacitor,for any frequency, is given by E0eiωt times the inﬁnite series which contains onlythe variable ωr/c. If we wish, we can deﬁne a special function, which we willcall J0(x), as the inﬁnite series that appears in the brackets of Eq. (23.15):

J0(x) = 1 − 1(1!)2

+ 1(2!)2

(cid:18) x

(cid:19)2

2

(cid:18) x

(cid:19)4

2

(cid:18) x

(cid:19)6

2

− 1(3!)2

± ···

(23.16)

23-5

Then we can write our solution as E0eiωt times this function, with x = ωr/c:

(cid:18) ωr

(cid:19)

E = E0eiωtJ0

.

c

(23.17)

The reason we have called our special function J0 is that, naturally, this isnot the ﬁrst time anyone has ever worked out a problem with oscillations in acylinder. The function has come up before and is usually called J0. It alwayscomes up whenever you solve a problem about waves with cylindrical symmetry.The function J0 is to cylindrical waves what the cosine function is to waves on astraight line. So it is an important function, invented a long time ago. Then aman named Bessel got his name attached to it. The subscript zero means thatBessel invented a whole lot of diﬀerent functions and this is just the ﬁrst of them.The other functions of Bessel—J1, J2, and so on—have to do with cylindricalwaves which have a variation of their strength with the angle around the axis ofthe cylinder.

The completely corrected electric ﬁeld between the plates of our circularcapacitor, given by Eq. (23.17), is plotted as the solid line in Fig. 23-5. Forfrequencies that are not too high, our second approximation was already quitegood. The third approximation was even better—so good, in fact, that if we hadplotted it, you would not have been able to see the diﬀerence between it and thesolid curve. You will see in the next section, however, that the complete series isneeded to get an accurate description for large radii, or for high frequencies.

23-3 A resonant cavityWe want to look now at what our solution gives for the electric ﬁeld betweenthe plates of the capacitor as we continue to go to higher and higher frequencies.For large ω, the parameter x = ωr/c also gets large, and the ﬁrst few terms inthe series for J0 of x will increase rapidly. That means that the parabola we havedrawn in Fig. 23-5 curves downward more steeply at higher frequencies. In fact,it looks as though the ﬁeld would fall all the way to zero at some high frequency,perhaps when c/ω is approximately one-half of a. Let’s see whether J0 doesindeed go through zero and become negative. We begin by trying x = 2:

J0(2) = 1 − 1 + 1

4 − 1

36 = 0.22.

The function is still not zero, so let’s try a higher value of x, say, x = 2.5. Puttingin numbers, we write

J0(2.5) = 1 − 1.56 + 0.61 − 0.11 = −0.06.

The function J0 has already gone through zero by the time we get to x = 2.5.Comparing the results for x = 2 and x = 2.5, it looks as though J0 goes throughzero at one-ﬁfth of the way from 2.5 to 2. We would guess that the zero occursfor x approximately equal to 2.4. Let’s see what that value of x gives:

J0(2.4) = 1 − 1.44 + 0.52 − 0.08 = 0.00.

We get zero to the accuracy of our two decimal places. If we make the calculationmore accurate (or since J0 is a well-known function, if we look it up in a book),we ﬁnd that it goes through zero at x = 2.405. We have worked it out by handto show you that you too could have discovered these things rather than havingto borrow them from a book.

As long as we are looking up J0 in a book, it is interesting to notice how itgoes for larger values of x; it looks like the graph in Fig. 23-6. As x increases,J0(x) oscillates between positive and negative values with a decreasing amplitudeof oscillation.We have gotten the following interesting result: If we go high enough infrequency, the electric ﬁeld at the center of our condenser will be one way andthe electric ﬁeld near the edge will point in the opposite direction. For example,23-6

Fig. 23-6. The Bessel function J0(x).

suppose that we take an ω high enough so that x = ωr/c at the outer edge ofthe capacitor is equal to 4; then the edge of the capacitor corresponds to theabscissa x = 4 in Fig. 23-6. This means that our capacitor is being operated atthe frequency ω = 4c/a. At the edge of the plates, the electric ﬁeld will havea rather high magnitude opposite the direction we would expect. That is theterrible thing that can happen to a capacitor at high frequencies. If we go tovery high frequencies, the direction of the electric ﬁeld oscillates back and forthmany times as we go out from the center of the capacitor. Also there are themagnetic ﬁelds associated with these electric ﬁelds. It is not surprising that ourcapacitor doesn’t look like the ideal capacitance for high frequencies. We mayeven start to wonder whether it looks more like a capacitor or an inductance.We should emphasize that there are even more complicated eﬀects that we haveneglected which happen at the edges of the capacitor. For instance, there will bea radiation of waves out past the edges, so the ﬁelds are even more complicatedthan the ones we have computed, but we will not worry about those eﬀects now.We could try to ﬁgure out an equivalent circuit for the capacitor, but perhapsit is better if we just admit that the capacitor we have designed for low-frequencyﬁelds is just no longer satisfactory when the frequency is too high. If we want totreat the operation of such an object at high frequencies, we should abandon theapproximations to Maxwell’s equations that we have made for treating circuitsand return to the complete set of equations which describe completely the ﬁeldsin space. Instead of dealing with idealized circuit elements, we have to deal withthe real conductors as they are, taking into account all the ﬁelds in the spaces inbetween. For instance, if we want a resonant circuit at high frequencies we willnot try to design one using a coil and a parallel-plate capacitor.

We have already mentioned that the parallel-plate capacitor we have beenanalyzing has some of the aspects of both a capacitor and an inductance. Withthe electric ﬁeld there are charges on the surfaces of the plates, and with themagnetic ﬁelds there are back emf’s. Is it possible that we already have a resonantcircuit? We do indeed. Suppose we pick a frequency for which the electric ﬁeldpattern falls to zero at some radius inside the edge of the disc; that is, wechoose ωa/c greater than 2.405. Everywhere on a circle coaxial with the platesthe electric ﬁeld will be zero. Now suppose we take a thin metal sheet and cuta strip just wide enough to ﬁt between the plates of the capacitor. Then webend it into a cylinder that will go around at the radius where the electric ﬁeldis zero. Since there are no electric ﬁelds there, when we put this conductingcylinder in place, no currents will ﬂow in it; and there will be no changes inthe electric and magnetic ﬁelds. We have been able to put a direct short circuitacross the capacitor without changing anything. And look what we have; wehave a complete cylindrical can with electrical and magnetic ﬁelds inside andno connection at all to the outside world. The ﬁelds inside won’t change even ifwe throw away the edges of the plates outside our can, and also the capacitorleads. All we have left is a closed can with electric and magnetic ﬁelds inside,as shown in Fig. 23-7(a). The electric ﬁelds are oscillating back and forth atthe frequency ω—which, don’t forget, determined the diameter of the can. Theamplitude of the oscillating E ﬁeld varies with the distance from the axis of thecan, as shown in the graph of Fig. 23-7(b). This curve is just the ﬁrst arch of theBessel function of zero order. There is also a magnetic ﬁeld which goes in circlesaround the axis and oscillates in time 90◦ out of phase with the electric ﬁeld.

We can also write out a series for the magnetic ﬁeld and plot it, as shown in

the graph of Fig. 23-7(c).

How is it that we can have an electric and magnetic ﬁeld inside a can withno external connections? It is because the electric and magnetic ﬁelds maintainthemselves, the changing E makes a B and the changing B makes an E—allaccording to the equations of Maxwell. The magnetic ﬁeld has an inductiveaspect, and the electric ﬁeld a capacitive aspect; together they make somethinglike a resonant circuit. Notice that the conditions we have described would onlyhappen if the radius of the can is exactly 2.405c/ω. For a can of a given radius,the oscillating electric and magnetic ﬁelds will maintain themselves—in the way23-7

Fig. 23-7. The electric and magnetic

ﬁelds in an enclosed cylindrical can.

we have described—only at that particular frequency. So a cylindrical can ofradius r is resonant at the frequency

ω0 = 2.405 cr

.

(23.18)

We have said that the ﬁelds continue to oscillate in the same way after the canis completely closed. That is not exactly right. It would be possible if the walls ofthe can were perfect conductors. For a real can, however, the oscillating currentswhich exist on the inside walls of the can lose energy because of the resistanceof the material. The oscillations of the ﬁelds will gradually die away. We cansee from Fig. 23-7 that there must be strong currents associated with electricand magnetic ﬁelds inside the cavity. Because the vertical electrical ﬁeld stopssuddenly at the top and bottom plates of the can, it has a large divergence there;so there must be positive and negative electric charges on the inner surfaces ofthe can, as shown in Fig. 23-7(a). When the electric ﬁeld reverses, the chargesmust reverse also, so there must be an alternating current between the top andbottom plates of the can. These charges will ﬂow in the sides of the can, as shownin the ﬁgure. We can also see that there must be currents in the sides of the canby considering what happens to the magnetic ﬁeld. The graph of Fig. 23-7(c)tells us that the magnetic ﬁeld suddenly drops to zero at the edge of the can.Such a sudden change in the magnetic ﬁeld can happen only if there is a currentin the wall. This current is what gives the alternating electric charges on the topand bottom plates of the can.

You may be wondering about our discovery of currents in the vertical sidesof the can. What about our earlier statement that nothing would be changedwhen we introduced these vertical sides in a region where the electric ﬁeld waszero? Remember, however, that when we ﬁrst put in the sides of the can, the topand bottom plates extended out beyond them, so that there were also magneticﬁelds on the outside of our can. It was only when we threw away the parts ofthe capacitor plates beyond the edges of the can that net currents had to appearon the insides of the vertical walls.

Although the electric and magnetic ﬁelds in the completely enclosed can willgradually die away because of the energy losses, we can stop this from happeningif we make a little hole in the can and put in a little bit of electrical energy tomake up the losses. We take a small wire, poke it through the hole in the side ofthe can, and fasten it to the inside wall so that it makes a small loop, as shown inFig. 23-8. If we now connect this wire to a source of high-frequency alternatingcurrent, this current will couple energy into the electric and magnetic ﬁelds ofthe cavity and keep the oscillations going. This will happen, of course, only ifthe frequency of the driving source is at the resonant frequency of the can. Ifthe source is at the wrong frequency, the electric and magnetic ﬁelds will notresonate, and the ﬁelds in the can will be very weak.

The resonant behavior can easily be seen by making another small hole in thecan and hooking in another coupling loop, as we have also drawn in Fig. 23-8. Thechanging magnetic ﬁeld through this loop will generate an induced electromotiveforce in the loop. If this loop is now connected to some external measuringcircuit, the currents will be proportional to the strength of the ﬁelds in the cavity.Suppose we now connect the input loop of our cavity to an RF signal generator,as shown in Fig. 23-9. The signal generator contains a source of alternatingcurrent whose frequency can be varied by varying the knob on the front of thegenerator. Then we connect the output loop of the cavity to a「detector,」whichis an instrument that measures the current from the output loop. It gives a meterreading proportional to this current. If we now measure the output current as afunction of the frequency of the signal generator, we ﬁnd a curve like that shown inFig. 23-10. The output current is small for all frequencies except those very nearthe frequency ω0, which is the resonant frequency of the cavity. The resonancecurve is very much like those we described in Chapter 23 of Vol. I. The width ofthe resonance is however, much narrower than we usually ﬁnd for resonant circuitsmade of inductances and capacitors; that is, the Q of the cavity is very high. It23-8

Fig. 23-8. Coupling into and out of a

resonant cavity.

Fig. 23-9. A setup for observing the cav-

ity resonance.

Fig. 23-10. The frequency response curve

of a resonant cavity.

is not unusual to ﬁnd Q’s as high as 100,000 or more if the inside walls of thecavity are made of some material with a very good conductivity, such as silver.

23-4 Cavity modesSuppose we now try to check our theory by making measurements with anactual can. We take a can which is a cylinder with a diameter of 3.0 inches anda height of about 2.5 inches. The can is ﬁtted with an input and output loop, asshown in Fig. 23-8. If we calculate the resonant frequency expected for this canaccording to Eq. (23.18), we get that f0 = ω0/2π = 3010 megacycles. When weset the frequency of our signal generator near 3000 megacycles and vary it slightlyuntil we ﬁnd the resonance, we observe that the maximum output current occursfor a frequency of 3050 megacycles, which is quite close to the predicted resonantfrequency, but not exactly the same. There are several possible reasons for thediscrepancy. Perhaps the resonant frequency is changed a little bit because of theholes we have cut to put in the coupling loops. A little thought, however, showsthat the holes should lower the resonant frequency a little bit, so that cannot bethe reason. Perhaps there is some slight error in the frequency calibration of thesignal generator, or perhaps our measurement of the diameter of the cavity isnot accurate enough. Anyway, the agreement is fairly close.

Much more important is something that happens if we vary the frequency ofour signal generator somewhat further from 3000 megacycles. When we do thatwe get the results shown in Fig. 23-11. We ﬁnd that, in addition to the resonancewe expected near 3000 megacycles, there is also a resonance near 3300 megacyclesand one near 3820 megacycles. What do these extra resonances mean? We mightget a clue from Fig. 23-6. Although we have been assuming that the ﬁrst zeroof the Bessel function occurs at the edge of the can, it could also be that thesecond zero of the Bessel function corresponds to the edge of the can, so thatthere is one complete oscillation of the electric ﬁeld as we move from the centerof the can out to the edge, as shown in Fig. 23-12. This is another possible modefor the oscillating ﬁelds. We should certainly expect the can to resonate in sucha mode. But notice, the second zero of the Bessel function occurs at x = 5.52,which is over twice as large as the value at the ﬁrst zero. The resonant frequencyof this mode should therefore be higher than 6000 megacycles. We would, nodoubt, ﬁnd it there, but it doesn’t explain the resonance we observe at 3300.

The trouble is that in our analysis of the behavior of a resonant cavity wehave considered only one possible geometric arrangement of the electric andmagnetic ﬁelds. We have assumed that the electric ﬁelds are vertical and thatthe magnetic ﬁelds lie in horizontal circles. But other ﬁelds are possible. Theonly requirements are that the ﬁelds should satisfy Maxwell’s equations insidethe can and that the electric ﬁeld should meet the wall at right angles. We haveconsidered the case in which the top and the bottom of the can are ﬂat, butthings would not be completely diﬀerent if the top and bottom were curved. Infact, how is the can supposed to know which is its top and bottom, and whichare its sides? It is, in fact, possible to show that there is a mode of oscillationof the ﬁelds inside the can in which the electric ﬁelds go more or less across thediameter of the can, as shown in Fig. 23-13.

It is not too hard to understand why the natural frequency of this modeshould be not very diﬀerent from the natural frequency of the ﬁrst mode we haveconsidered. Suppose that instead of our cylindrical cavity we had taken a cavitywhich was a cube 3 inches on a side. It is clear that this cavity would have threediﬀerent modes, but all with the same frequency. A mode with the electric ﬁeldgoing more or less up and down would certainly have the same frequency as themode in which the electric ﬁeld was directed right and left. If we now distortthe cube into a cylinder, we will change these frequencies somewhat. We wouldstill expect them not to be changed too much, provided we keep the dimensionsof the cavity more or less the same. So the frequency of the mode of Fig. 23-13should not be too diﬀerent from the mode of Fig. 23-8. We could make a detailedcalculation of the natural frequency of the mode shown in Fig. 23-13, but we will23-9

Fig. 23-11. Observed resonant frequen-

cies of a cylindrical cavity.

Fig. 23-12. A higher-frequency mode.

Fig. 23-13. A transverse mode of the

cylindrical cavity.

not do that now. When the calculations are carried through, it is found that, forthe dimensions we have assumed, the resonant frequency comes out very close tothe observed resonance at 3300 megacycles.

By similar calculations it is possible to show that there should be still anothermode at the other resonant frequency we found near 3800 megacycles. For thismode, the electric and magnetic ﬁelds are as shown in Fig. 23-14. The electricﬁeld does not bother to go all the way across the cavity. It goes from the sidesto the ends, as shown.

As you will probably now believe, if we go higher and higher in frequency weshould expect to ﬁnd more and more resonances. There are many diﬀerent modes,each of which will have a diﬀerent resonant frequency corresponding to someparticular complicated arrangement of the electric and magnetic ﬁelds. Each ofthese ﬁeld arrangements is called a resonant mode. The resonance frequency ofeach mode can be calculated by solving Maxwell’s equations for the electric andmagnetic ﬁelds in the cavity.

When we have a resonance at some particular frequency, how can we knowwhich mode is being excited? One way is to poke a little wire into the cavitythrough a small hole. If the electric ﬁeld is along the wire, as in Fig. 23-15(a),there will be relatively large currents in the wire, sapping energy from theﬁelds, and the resonance will be suppressed. If the electric ﬁeld is as shown inFig. 23-15(b), the wire will have a much smaller eﬀect. We could ﬁnd whichway the ﬁeld points in this mode by bending the end of the wire, as shown inFig. 23-15(c). Then, as we rotate the wire, there will be a big eﬀect when theend of the wire is parallel to E and a small eﬀect when it is rotated so as to beat 90◦ to E.

Fig. 23-14. Another mode of a cylindrical

cavity.

Fig. 23-15. A short metal wire inserted into a cavity will disturb theresonance much more when it is parallel to E than when it is at right angles.

23-5 Cavities and resonant circuitsAlthough the resonant cavity we have been describing seems to be quitediﬀerent from the ordinary resonant circuit consisting of an inductance and acapacitor, the two resonant systems are, of course, closely related. They are bothmembers of the same family; they are just two extreme cases of electromagneticresonators—and there are many intermediate cases between these two extremes.Suppose we start by considering the resonant circuit of a capacitor in parallelwith an inductance, as shown in Fig. 23-16(a). This circuit will resonate at the√frequency ω0 = 1/LC. If we want to raise the resonant frequency of this circuit,we can do so by lowering the inductance L. One way is to decrease the numberof turns in the coil. We can, however, go only so far in this direction. Eventuallywe will get down to the last turn, and we will have just a piece of wire joining thetop and bottom plates of the condenser. We could raise the resonant frequencystill further by making the capacitance smaller; however, we can also continue todecrease the inductance by putting several inductances in parallel. Two one-turninductances in parallel will have only half the inductance of each turn. So whenour inductance has been reduced to a single turn, we can continue to raise the23-10

Fig. 23-16. Resonators of progressively higher resonant frequencies.

resonant frequency by adding other single loops from the top plate to the bottomplate of the condenser. For instance, Fig. 23-16(b) shows the condenser platesconnected by six such「single-turn inductances.」If we continue to add many suchpieces of wire, we can make the transition to the completely enclosed resonantsystem shown in part (c) of the ﬁgure, which is a drawing of the cross section of acylindrically symmetrical object. Our inductance is now a cylindrical hollow canattached to the edges of the condenser plates. The electric and magnetic ﬁeldswill be as shown in the ﬁgure. Such an object is, of course, a resonant cavity. Itis called a「loaded」cavity. But we can still think of it as an L-C circuit in whichthe capacity section is the region where we ﬁnd most of the electric ﬁeld and theinductance section is that region where we ﬁnd most of the magnetic ﬁeld.

If we want to make the frequency of the resonator in Fig. 23-16(c) still higher,we can do so by continuing to decrease the inductance L. To do that, we mustdecrease the geometric dimensions of the inductance section, for example bydecreasing the dimension h in the drawing. As h is decreased, the resonantfrequency will be increased. Eventually, of course, we will get to the situation inwhich the height h is just equal to the separation between the condenser plates.We then have just a cylindrical can; our resonant circuit has become the cavityresonator of Fig. 23-7.

You will notice that in the original L-C resonant circuit of Fig. 23-16 theelectric and magnetic ﬁelds are quite separate. As we have gradually modiﬁed theresonant system to make higher and higher frequencies, the magnetic ﬁeld hasbeen brought closer and closer to the electric ﬁeld until in the cavity resonatorthe two are quite intermixed.

Although the cavity resonators we have talked about in this chapter have beencylindrical cans, there is nothing magic about the cylindrical shape. A can of anyshape will have resonant frequencies corresponding to various possible modes ofoscillations of the electric and magnetic ﬁelds. For example, the「cavity」shownin Fig. 23-17 will have its own particular set of resonant frequencies—althoughthey would be rather diﬃcult to calculate.

23-11

Fig. 23-17. Another resonant cavity.

24

Waveguides

24-1 The transmission lineIn

the last chapter we studied what happened to the lumped elements ofcircuits when they were operated at very high frequencies, and we were led to seethat a resonant circuit could be replaced by a cavity with the ﬁelds resonatinginside. Another interesting technical problem is the connection of one objectto another, so that electromagnetic energy can be transmitted between them.In low-frequency circuits the connection is made with wires, but this methoddoesn’t work very well at high frequencies because the circuits would radiateenergy into all the space around them, and it is hard to control where the energywill go. The ﬁelds spread out around the wires; the currents and voltages are not「guided」very well by the wires. In this chapter we want to look into the waysthat objects can be interconnected at high frequencies. At least, that’s one wayof presenting our subject.

Another way is to say that we have been discussing the behavior of waves infree space. Now it is time to see what happens when oscillating ﬁelds are conﬁnedin one or more dimensions. We will discover the interesting new phenomenonwhen the ﬁelds are conﬁned in only two dimensions and allowed to go free inthe third dimension, they propagate in waves. These are「guided waves」—thesubject of this chapter.

We begin by working out the general theory of the transmission line. The or-dinary power transmission line that runs from tower to tower over the countrysideradiates away some of its power, but the power frequencies (50–60 cycles/sec) areso low that this loss is not serious. The radiation could be stopped by surroundingthe line with a metal pipe, but this method would not be practical for power linesbecause the voltages and currents used would require a very large, expensive,and heavy pipe. So simple「open lines」are used.

For somewhat higher frequencies—say a few kilocycles—radiation can alreadybe serious. However, it can be reduced by using「twisted-pair」transmission lines,as is done for short-run telephone connections. At higher frequencies, however,the radiation soon becomes intolerable, either because of power losses or becausethe energy appears in other circuits where it isn’t wanted. For frequencies from afew kilocycles to some hundreds of megacycles, electromagnetic signals and powerare usually transmitted via coaxial lines consisting of a wire inside a cylindrical「outer conductor」or「shield.」Although the following treatment will apply to atransmission line of two parallel conductors of any shape, we will carry it outreferring to a coaxial line.

We take the simplest coaxial line that has a central conductor, which wesuppose is a thin hollow cylinder, and an outer conductor which is another thincylinder on the same axis as the inner conductor, as in Fig. 24-1. We begin byﬁguring out approximately how the line behaves at relatively low frequencies. Wehave already described some of the low-frequency behavior when we said earlierthat two such conductors had a certain amount of inductance per unit length ora certain capacity per unit length. We can, in fact, describe the low-frequencybehavior of any transmission line by giving its inductance per unit length, L0 andits capacity per unit length, C0. Then we can analyze the line as the limiting caseof the L-C ﬁlter as discussed in Section 22-6. We can make a ﬁlter which imitatesthe line by taking small series elements L0 ∆x and small shunt capacities C0 ∆x,where ∆x is an element of length of the line. Using our results for the inﬁniteﬁlter, we see that there would be a propagation of electric signals along the line.24-1

24-1 The transmission line24-2 The rectangular waveguide24-3 The cutoﬀ frequency24-4 The speed of the guided waves24-5 Observing guided waves24-6 Waveguide plumbing24-7 Waveguide modes24-8 Another way of looking at the

guided waves

Fig. 24-1. A coaxial transmission line.

Rather than following that approach, however, we would now rather look at theline from the point of view of a diﬀerential equation.

Suppose that we see what happens at two neighboring points along thetransmission line, say at the distances x and x + ∆x from the beginning of theline. Let’s call the voltage diﬀerence between the two conductors V (x), and thecurrent along the「hot」conductor I(x) (see Fig. 24-2). If the current in the lineis varying, the inductance will give us a voltage drop across the small section ofline from x to x + ∆x in the amount

∆V = V (x + ∆x) − V (x) = −L0 ∆x

Or, taking the limit as ∆x → 0, we get

dIdt

.

∂V∂x

= −L0

∂I∂t

.

(24.1)

The changing current gives a gradient of the voltage.

Referring again to the ﬁgure, if the voltage at x is changing, there mustbe some charge supplied to the capacity in that region. If we take the smallpiece of line between x and x + ∆x, the charge on it is q = C0 ∆xV . The timerate-of-change of this charge is C0 ∆x dV /dt, but the charge changes only if thecurrent I(x) into the element is diﬀerent from the current I(x + ∆x) out. Callingthe diﬀerence ∆I, we have

Fig. 24-2. The currents and voltages of

a transmission line.

or

∂2V∂x2∂2I∂x2

= C0L0

= C0L0

∂2V∂t2∂2I∂t2

(24.3)

(24.4)

∆I = −C0 ∆x

dVdt

.

Taking the limit as ∆x → 0, we get∂I∂x

= −C0

∂V∂t

.

(24.2)

So the conservation of charge implies that the gradient of the current is propor-tional to the time rate-of-change of the voltage.

Equations (24.1) and (24.2) are then the basic equations of a transmissionline. If we wish, we could modify them to include the eﬀects of resistance in theconductors or of leakage of charge through the insulation between the conductors,but for our present discussion we will just stay with the simple example.

The two transmission line equations can be combined by diﬀerentiating onewith respect to t and the other with respect to x and eliminating either V or I.Then we have either

Once more we recognize the wave equation in x. For a uniform transmissionline, the voltage (and current) propagates along the line as a wave. The voltagealong the line must be of the form V (x, t) = f(x − vt) or V (x, t) = g(x + vt), ora sum of both. Now what is the velocity v? We know that the coeﬃcient of the∂2/∂t2 term is just 1/v2, so

v =

(24.5)We will leave it for you to show that the voltage for each wave in a line isproportional to the current of that wave and that the constant of proportionalityis just the characteristic impedance z0. Calling V+ and I+ the voltage and currentfor a wave going in the plus x-direction, you should get

L0C0

.

1√

Similarly, for the wave going toward minus x the relation is

V+ = z0I+.

V− = z0I−.

(24.6)

24-2

The characteristic impedance—as we found out from our ﬁlter equations—is

given by

z0 =

,

(24.7)

r L0

C0

and is, therefore, a pure resistance.

To ﬁnd the propagation speed v and the characteristic impedance z0 of atransmission line, we have to know the inductance and capacity per unit length.We can calculate them easily for a coaxial cable, so we will see how that goes.For the inductance we follow the ideas of Section 17-8, and set 12 LI2 equal to themagnetic energy which we get by integrating 0c2B2/2 over the volume. Supposethat the central conductor carries the current I; then we know that B = I/2π0c2r,where r is the distance from the axis. Taking as a volume element a cylindricalshell of thickness dr and of length l, we have for the magnetic energy

Z b

(cid:18)

a

(cid:19)2

U = 0c22

I

2π0c2r

l 2πr dr,

where a and b are the radii of the inner and outer conductors, respectively.Carrying out the integral, we get

Setting the energy equal to 1

U = I2l4π0c22 LI2, we ﬁndl

L =

2π0c2

ln ba

.

ln ba

.

(24.8)

(24.9)

It is, as it should be, proportional to the length l of the line, so the inductanceper unit length L0 is

(24.10)

We have worked out the charge on a cylindrical condenser (see Section 12-2).

Now, dividing the charge by the potential diﬀerence, we get

L0 = ln(b/a)2π0c2 .

C = 2π0lln(b/a) .

The capacity per unit length C0 is C/l. Combining this result with Eq. (24.10),√we see that the product L0C0 is just equal to 1/c2, so v = 1/L0C0 is equalto c. The wave travels down the line with the speed of light. We point outthat this result depends on our assumptions: (a) that there are no dielectricsor magnetic materials in the space between the conductors, and (b) that thecurrents are all on the surfaces of the conductors (as they would be for perfectconductors). We will see later that for good conductors at high frequencies,all currents distribute themselves on the surfaces as they would for a perfectconductor, so this assumption is then valid.

Now it is interesting that so long as assumptions (a) and (b) are correct, theproduct L0C0 is equal to 1/c2 for any parallel pair of conductors—even, say, for ahexagonal inner conductor anywhere inside an elliptical outer conductor. So longas the cross section is constant and the space between has no material, waves arepropagated at the velocity of light.

No such general statement can be made about the characteristic impedance.

For the coaxial line, it is

z0 = ln(b/a)2π0c

(24.11)The factor 1/0c has the dimensions of a resistance and is equal to 120π ohms.The geometric factor ln(b/a) depends only logarithmically on the dimensions, sofor the coaxial line—and most lines—the characteristic impedance has typicalvalues of from 50 ohms or so to a few hundred ohms.

.

24-3

24-2 The rectangular waveguideThe next thing we want to talk about seems, at ﬁrst sight, to be a strikingphenomenon: if the central conductor is removed from the coaxial line, it can stillcarry electromagnetic power. In other words, at high enough frequencies a hollowtube will work just as well as one with wires. It is related to the mysteriousway in which a resonant circuit of a condenser and inductance gets replaced bynothing but a can at high frequencies.

Although it may seem to be a remarkable thing when one has been thinkingin terms of a transmission line as a distributed inductance and capacity, we allknow that electromagnetic waves can travel along inside a hollow metal pipe. Ifthe pipe is straight, we can see through it! So certainly electromagnetic waves gothrough a pipe. But we also know that it is not possible to transmit low-frequencywaves (power or telephone) through the inside of a single metal pipe. So it mustbe that electromagnetic waves will go through if their wavelength is short enough.Therefore we want to discuss the limiting case of the longest wavelength (or thelowest frequency) that can get through a pipe of a given size. Since the pipe isthen being used to carry waves, it is called a waveguide.

We will begin with a rectangular pipe, because it is the simplest case toanalyze. We will ﬁrst give a mathematical treatment and come back later to lookat the problem in a much more elementary way. The more elementary approach,however, can be applied easily only to a rectangular guide. The basic phenomenaare the same for a general guide of arbitrary shape, so the mathematical argumentis fundamentally more sound.

Our problem, then, is to ﬁnd what kind of waves can exist inside a rectangularpipe. Let’s ﬁrst choose some convenient coordinates; we take the z-axis alongthe length of the pipe, and the x- and y-axes parallel to the two sides, as shownin Fig. 24-3.

Fig. 24-3. Coordinates chosen for the

rectangular waveguide.

Fig. 24-4. The electric ﬁeld in the wave-

guide at some value of z.

We know that when light waves go down the pipe, they have a transverseelectric ﬁeld; so suppose we look ﬁrst for solutions in which E is perpendicularto z, say with only a y-component, Ey. This electric ﬁeld will have some variationacross the guide; in fact, it must go to zero at the sides parallel to the y-axis,because the currents and charges in a conductor always adjust themselves so thatthere is no tangential component of the electric ﬁeld at the surface of a conductor.So Ey will vary with x in some arch, as shown in Fig. 24-4. Perhaps it is theBessel function we found for a cavity? No, because the Bessel function has todo with cylindrical geometries. For a rectangular geometry, waves are usuallysimple harmonic functions, so we should try something like sin kxx.Since we want waves that propagate down the guide, we expect the ﬁeld toalternate between positive and negative values as we go along in z, as in Fig. 24-5,and these oscillations will travel along the guide with some velocity v. If wehave oscillations at some deﬁnite frequency ω, we would guess that the wavemight vary with z like cos (ωt− kzz), or to use the more convenient mathematicalform, like ei(ωt−kzz). This z-dependence represents a wave travelling with thespeed v = ω/kz (see Chapter 29, Vol. I).So we might guess that the wave in the guide would have the followingmathematical form:

Ey = E0ei(ωt−kzz) sin kxx.

(24.12)Let’s see whether this guess satisﬁes the correct ﬁeld equations. First, theelectric ﬁeld should have no tangential components at the conductors. Our ﬁeldsatisﬁes this requirement; it is perpendicular to the top and bottom faces andis zero at the two side faces. Well, it is if we choose kx so that one-half a cycleof sin kxx just ﬁts in the width of the guide—that is, if

kxa = π.

There are other possibilities, like kxa = 2π, 3π, . . . , or, in general,

kxa = nπ,

(24.13)

(24.14)24-4

Fig. 24-5. The z-dependence of the ﬁeld

in the waveguide.

where n is any integer. These represent various complicated arrangements of theﬁeld, but for now let’s take only the simplest one, where kx = π/a, where a isthe width of the inside of the guide.Next, the divergence of E must be zero in the free space inside the guide,since there are no charges there. Our E has only a y-component, and it doesn’tchange with y, so we do have that ∇ · E = 0.Finally, our electric ﬁeld must agree with the rest of Maxwell’s equations inthe free space inside the guide. That is the same thing as saying that it mustsatisfy the wave equation

∂2Ey∂x2

+ ∂2Ey∂y2

∂z2 − 1+ ∂2Ey

c2

∂2Ey∂t2

= 0.

(24.15)

We have to see whether our guess, Eq. (24.12), will work. The second derivativeof Ey with respect to x is just −k2xEy. The second derivative with respect to yis zero, since nothing depends on y. The second derivative with respect to zis −k2zEy, and the second derivative with respect to t is −ω2Ey. Equation (24.15)then says that

xEy + k2k2

zEy − ω2

c2 Ey = 0.

Unless Ey is zero everywhere (which is not very interesting), this equation iscorrect if

(24.16)We have already ﬁxed kx, so this equation tells us that there can be waves of thetype we have assumed if kz is related to the frequency ω so that Eq. (24.16) issatisﬁed—in other words, if

+ k2

= 0.

k2

x

z − ω2c2

(24.17)The waves we have described are propagated in the z-direction with this valueof kz.The wave number kz we get from Eq. (24.17) tells us, for a given frequency ω,the speed with which the nodes of the wave propagate down the guide. Thephase velocity is

kz =p(ω2/c2) − (π2/a2).

p1 − (λ0/2a)2 .

λ0

λg =

Fig. 24-6. The magnetic ﬁeld in the

waveguide.

(24.19)

v = ωkz

.

(24.18)

You will remember that the wavelength λ of a travelling wave is given by λ =2πv/ω, so kz is also equal to 2π/λg, where λg is the wavelength of the oscillationsalong the z-direction—the「guide wavelength.」The wavelength in the guide isdiﬀerent, of course, from the free-space wavelength of electromagnetic wavesof the same frequency. If we call the free-space wavelength λ0, which is equalto 2πc/ω, we can write Eq. (24.17) as

Besides the electric ﬁelds there are magnetic ﬁelds that will travel with thewave, but we will not bother to work out an expression for them right now.Since c2∇ × B = ∂E/∂t, the lines of B will circulate around the regions inwhich ∂E/∂t is largest, that is, halfway between the maximum and minimumof E. The loops of B will lie parallel to the xz-plane and between the crests andtroughs of E, as shown in Fig. 24-6.

24-3 The cutoﬀ frequencyIn solving Eq. (24.16) for kz, there should really be two roots—one plus and

one minus. We should write

kz = ±p(ω2/c2) − (π2/a2).

(24.20)24-5

The two signs simply mean that there can be waves which propagate with anegative phase velocity (toward −z), as well as waves which propagate in thepositive direction in the guide. Naturally, it should be possible for waves to goin either direction. Since both types of waves can be present at the same time,there will be the possibility of standing-wave solutions.

Our equation for kz also tells us that higher frequencies give larger valuesof kz, and therefore smaller wavelengths, until in the limit of large ω, k becomesequal to ω/c, which is the value we would expect for waves in free space. Thelight we「see」through a pipe still travels at the speed c. But now notice that ifwe go toward low frequencies, something strange happens. At ﬁrst the wavelengthgets longer and longer, but if ω gets too small the quantity inside the square rootof Eq. (24.20) suddenly becomes negative. This will happen as soon as ω gets tobe less than πc/a—or when λ0 becomes greater than 2a. In other words, whenthe frequency gets smaller than a certain critical frequency ωc = πc/a, the wavenumber kz (and also λg) becomes imaginary and we haven’t got a solution anymore. Or do we? Who said that kz has to be real? What if it does come outimaginary? Our ﬁeld equations are still satisﬁed. Perhaps an imaginary kz alsorepresents a wave.

Suppose ω is less than ωc; then we can write

where k0 is a positive real number:

kz = ±ik0,

k =p(π2/a2) − (ω2/c2).

If we now go back to our expression, Eq. (24.12), for Ey, we have

which we can write as

Ey = E0ei(ωt∓ik0z) sin kxx,

(24.21)

(24.22)

(24.23)

Ey = E0e±k0zeiωt sin kxx.

(24.24)This expression gives an E-ﬁeld that oscillates with time as eiωt but whichvaries with z as e±k0z.It decreases or increases with z smoothly as a realexponential. In our derivation we didn’t worry about the sources that started thewaves, but there must, of course, be a source someplace in the guide. The signthat goes with k0 must be the one that makes the ﬁeld decrease with increasingdistance from the source of the waves.So for frequencies below ωc = πc/a, waves do not propagate down the guide;the oscillating ﬁelds penetrate into the guide only a distance of the order of 1/k0.For this reason, the frequency ωc is called the「cutoﬀ frequency」of the guide.Looking at Eq. (24.22), we see that for frequencies just a little below ωc, thenumber k0 is small and the ﬁelds can penetrate a long distance into the guide.But if ω is much less than ωc, the exponential coeﬃcient k0 is equal to π/a andthe ﬁeld dies oﬀ extremely rapidly, as shown in Fig. 24-7. The ﬁeld decreasesby 1/e in the distance a/π, or in only about one-third of the guide width. Theﬁelds penetrate very little distance from the source.We want to emphasize an interesting feature of our analysis of the guidedwaves—the appearance of the imaginary wave number kz. Normally, if wesolve an equation in physics and get an imaginary number, it doesn’t meananything physical. For waves, however, an imaginary wave number does meansomething. The wave equation is still satisﬁed; it only means that the solutiongives exponentially decreasing ﬁelds instead of propagating waves. So in anywave problem where k becomes imaginary for some frequency, it means that theform of the wave changes—the sine wave changes into an exponential.

24-4 The speed of the guided wavesThe wave velocity we have used above is the phase velocity, which is the speedof a node of the wave; it is a function of frequency. If we combine Eqs. (24.17)24-6

Fig. 24-7. The variation of Ey with z

for ω (cid:28) ωc.

and (24.18), we can write

vphase =

cp1 − (ωc/ω)2 .

(24.25)

For frequencies above cutoﬀ—where travelling waves exist—ωc/ω is less than one,and vphase is real and greater than the speed of light. We have already seen inChapter 48 of Vol. I that phase velocities greater than light are possible, becauseit is just the nodes of the wave which are moving and not energy or information.In order to know how fast signals will travel, we have to calculate the speed ofpulses or modulations made by the interference of a wave of one frequency withone or more waves of slightly diﬀerent frequencies (see Chapter 48, Vol. I). Wehave called the speed of the envelope of such a group of waves the group velocity;it is not ω/k but dω/dk:

(24.26)Taking the derivative of Eq. (24.17) with respect to ω and inverting to get dω/dk,we ﬁnd that(24.27)

vgroup = cp1 − (ωc/ω)2,

vgroup = dωdk

.

which is less than the speed of light.

The geometric mean of vphase and vgroup is just c, the speed of light:

vphasevgroup = c2.

(24.28)

This is curious, because we have seen a similar relation in quantum mechanics. Fora particle with any velocity—even relativistic—the momentum p and energy Uare related by(24.29)But in quantum mechanics the energy is ω, and the momentum is /λ, whichis equal to k; so Eq. (24.29) can be written

U 2 = p2c2 + m2c4.

or

ω2c2

= k2 + m2c22 ,

k =p(ω2/c2) − (m2c2/2),

(24.30)

(24.31)

which looks very much like Eq. (24.17) . . . Interesting!

The group velocity of the waves is also the speed at which energy is transportedalong the guide. If we want to ﬁnd the energy ﬂow down the guide, we can get itfrom the energy density times the group velocity. If the root mean square electricﬁeld is E0, then the average density of electric energy is 0E20 /2. There is alsosome energy associated with the magnetic ﬁeld. We will not prove it here, butin any cavity or guide the magnetic and electric energies are equal, so the totalelectromagnetic energy density is 0E20. The power dU/dt transmitted by theguide is then

(We will see later another, more general way of getting the energy ﬂow.)

dUdt

= 0E2

0 abvgroup.

(24.32)

24-5 Observing guided wavesEnergy can be coupled into a waveguide by some kind of an「antenna.」Forexample, a little vertical wire or「stub」will do. The presence of the guided wavescan be observed by picking up some of the electromagnetic energy with a littlereceiving「antenna,」which again can be a little stub of wire or a small loop. InFig. 24-8, we show a guide with some cutaways to show a driving stub and apickup「probe」. The driving stub can be connected to a signal generator via acoaxial cable, and the pickup probe can be connected by a similar cable to adetector. It is usually convenient to insert the pickup probe via a long thin slot24-7

Fig. 24-8. A waveguide with a driving

stub and a pickup probe.

in the guide, as shown in Fig. 24-8. Then the probe can be moved back and forthalong the guide to sample the ﬁelds at various positions.

If the signal generator is set at some frequency ω greater than the cutoﬀfrequency ωc, there will be waves propagated down the guide from the drivingstub. These will be the only waves present if the guide is inﬁnitely long, whichcan eﬀectively be arranged by terminating the guide with a carefully designedabsorber in such a way that there are no reﬂections from the far end. Then, sincethe detector measures the time average of the ﬁelds near the probe, it will pickup a signal which is independent of the position along the guide; its output willbe proportional to the power being transmitted.

If now the far end of the guide is ﬁnished oﬀ in some way that produces areﬂected wave—as an extreme example, if we closed it oﬀ with a metal plate—there will be a reﬂected wave in addition to the original forward wave. Thesetwo waves will interfere and produce a standing wave in the guide similar to thestanding waves on a string which we discussed in Chapter 49 of Vol. I. Then,as the pickup probe is moved along the line, the detector reading will rise andfall periodically, showing a maximum in the ﬁelds at each loop of the standingwave and a minimum at each node. The distance between two successive nodes(or loops) is just λg/2. This gives a convenient way of measuring the guidewavelength. If the frequency is now moved closer to ωc, the distances betweennodes increase, showing that the guide wavelength increases as predicted byEq. (24.19).

Suppose now the signal generator is set at a frequency just a little below ωc.Then the detector output will decrease gradually as the pickup probe is moveddown the guide. If the frequency is set somewhat lower, the ﬁeld strength willfall rapidly, following the curve of Fig. 24-7, and showing that waves are notpropagated.

24-6 Waveguide plumbingAn important practical use of waveguides is for the transmission of high-frequency power, as, for example, in coupling the high-frequency oscillator oroutput ampliﬁer of a radar set to an antenna. In fact, the antenna itself usuallyconsists of a parabolic reﬂector fed at its focus by a waveguide ﬂared out at theend to make a「horn」that radiates the waves coming along the guide. Althoughhigh frequencies can be transmitted along a coaxial cable, a waveguide is betterfor transmitting large amounts of power. First, the maximum power that can betransmitted along a line is limited by the breakdown of the insulation (solid orgas) between the conductors. For a given amount of power, the ﬁeld strengths ina guide are usually less than they are in a coaxial cable, so higher powers can betransmitted before breakdown occurs. Second, the power losses in the coaxialcable are usually greater than in a waveguide. In a coaxial cable there must beinsulating material to support the central conductor, and there is an energy lossin this material—particularly at high frequencies. Also, the current densities onthe central conductor are quite high, and since the losses go as the square of thecurrent density, the lower currents that appear on the walls of the guide result inlower energy losses. To keep these losses to a minimum, the inner surfaces of theguide are often plated with a material of high conductivity, such as silver.

24-8

Fig. 24-9. Sections of waveguide connected with

Fig. 24-10. A low-loss connection between two

ﬂanges.

sections of waveguide.

The problem of connecting a「circuit」with waveguides is quite diﬀerentfrom the corresponding circuit problem at low frequencies, and is usually calledmicrowave「plumbing.」Many special devices have been developed for the purpose.For instance, two sections of waveguide are usually connected together by meansof ﬂanges, as can be seen in Fig. 24-9. Such connections can, however, causeserious energy losses, because the surface currents must ﬂow across the joint,which may have a relatively high resistance. One way to avoid such losses is tomake the ﬂanges as shown in the cross section drawn in Fig. 24-10. A small spaceis left between the adjacent sections of the guide, and a groove is cut in the face ofone of the ﬂanges to make a small cavity of the type shown in Fig. 23-16(c). Thedimensions are chosen so that this cavity is resonant at the frequency being used.This resonant cavity presents a high「impedance」to the currents, so relativelylittle current ﬂows across the metallic joints (at a in Fig. 24-10). The high guidecurrents simply charge and discharge the「capacity」of the gap (at b in the ﬁgure),where there is little dissipation of energy.

Suppose you want to stop a waveguide in a way that won’t result in reﬂectedwaves. Then you must put something at the end that imitates an inﬁnite lengthof guide. You need a「termination」which acts for the guide like the characteristicimpedance does for a transmission line—something that absorbs the arrivingwaves without making reﬂections. Then the guide will act as though it went onforever. Such terminations are made by putting inside the guide some wedges ofresistance material carefully designed to absorb the wave energy while generatingalmost no reﬂected waves.

If you want to connect three things together—for instance, one source to twodiﬀerent antennas—then you can use a「T」like the one shown in Fig. 24-11.Power fed in at the center section of the「T」will be split and go out the two sidearms (and there may also be some reﬂected waves). You can see qualitativelyfrom the sketches in Fig. 24-12 that the ﬁelds would spread out when they get tothe end of the input section and make electric ﬁelds that will start waves goingout the two arms. Depending on whether electric ﬁelds in the guide are parallelor perpendicular to the「top」of the「T,」the ﬁelds at the junction would beroughly as shown in (a) or (b) of Fig. 24-12.

Finally, we would like to describe a device called an「unidirectional coupler,」which is very useful for telling what is going on after you have connected acomplicated arrangement of waveguides. Suppose you want to know which waythe waves are going in a particular section of guide—you might be wondering,for instance, whether or not there is a strong reﬂected wave. The unidirectionalcoupler takes out a small fraction of the power of a guide if there is a wave goingone way, but none if the wave is going the other way. By connecting the outputof the coupler to a detector, you can measure the「one-way」power in the guide.24-9

Fig. 24-11. A waveguide「T.」(Theﬂanges have plastic end caps to keep theinside clean while the「T」is not being used.

Fig. 24-12. The electric ﬁelds in a wave-guide「T」for two possible ﬁeld orientations.

Figure 24-13 is a drawing of a unidirectional coupler; a piece of waveguide ABhas another piece of waveguide CD soldered to it along one face. The guide CDis curved away so that there is room for the connecting ﬂanges. Before theguides are soldered together, two (or more) holes have been drilled in each guide(matching each other) so that some of the ﬁelds in the main guide AB can becoupled into the secondary guide CD. Each of the holes acts like a little antennathat produces a wave in the secondary guide. If there were only one hole, waveswould be sent in both directions and would be the same no matter which waythe wave was going in the primary guide. But when there are two holes with aseparation space equal to one-quarter of the guide wavelength, they will maketwo sources 90◦ out of phase. Do you remember that we considered in Chapter 29of Vol. I the interference of the waves from two antennas spaced λ/4 apart andexcited 90◦ out of phase in time? We found that the waves subtract in onedirection and add in the opposite direction. The same thing will happen here.The wave produced in the guide CD will be going in the same direction as thewave in AB.If the wave in the primary guide is travelling from A toward B, there willbe a wave at the output D of the secondary guide. If the wave in the primaryguide goes from B toward A, there will be a wave going toward the end C of thesecondary guide. This end is equipped with a termination, so that this wave isabsorbed and there is no wave at the output of the coupler.

24-7 Waveguide modesThe wave we have chosen to analyze is a special solution of the ﬁeld equations.There are many more. Each solution is called a waveguide「mode.」For example,our x-dependence of the ﬁeld was just one-half a cycle of a sine wave. There is anequally good solution with a full cycle; then the variation of Ey with x is as shownin Fig. 24-14. The kx for such a mode is twice as large, so the cutoﬀ frequency ismuch higher. Also, in the wave we studied E has only a y-component, but thereare other modes with more complicated electric ﬁelds. If the electric ﬁeld hascomponents only in x and y—so that the total electric ﬁeld is always at rightangles to the z-direction—the mode is called a「transverse electric」(or TE) mode.The magnetic ﬁeld of such modes will always have a z-component. It turns outthat if E has a component in the z-direction (along the direction of propagation),then the magnetic ﬁeld will always have only transverse components. So suchﬁelds are called transverse magnetic (TM) modes. For a rectangular guide, allthe other modes have a higher cutoﬀ frequency than the simple TE mode we havedescribed. It is, therefore, possible—and usual—to use a guide with a frequencyjust above the cutoﬀ for this lowest mode but below the cutoﬀ frequency for allthe others, so that just the one mode is propagated. Otherwise, the behaviorgets complicated and diﬃcult to control.

24-8 Another way of looking at the guided wavesWe want now to show you another way of understanding why a waveguideattenuates the ﬁelds rapidly for frequencies below the cutoﬀ frequency ωc. Thenyou will have a more「physical」idea of why the behavior changes so drasticallybetween low and high frequencies. We can do this for the rectangular guide byanalyzing the ﬁelds in terms of reﬂections—or images—in the walls of the guide.The approach only works for rectangular guides, however; that’s why we startedwith the more mathematical analysis which works, in principle, for guides of anyshape.

For the mode we have described, the vertical dimension (in y) had no eﬀect,so we can ignore the top and bottom of the guide and imagine that the guide isextended indeﬁnitely in the vertical direction. We imagine then that the guidejust consists of two vertical plates with the separation a.Let’s say that the source of the ﬁelds is a vertical wire placed in the middleof the guide, with the wire carrying a current that oscillates at the frequency ω.In the absence of the guide walls such a wire would radiate cylindrical waves.

24-10

Fig. 24-13. A unidirectional coupler.

Fig. 24-14. Another possible variation of

Ey with x

Now we consider that the guide walls are perfect conductors. Then, just asin electrostatics, the conditions at the surface will be correct if we add to theﬁeld of the wire the ﬁeld of one or more suitable image wires. The image ideaworks just as well for electrodynamics as it does for electrostatics, provided, ofcourse, that we also include the retardations. We know that is true because wehave often seen a mirror producing an image of a light source. And a mirror isjust a「perfect」conductor for electromagnetic waves with optical frequencies.Now let’s take a horizontal cross section, as shown in Fig. 24-15, where W1and W2 are the two guide walls and S0 is the source wire. We call the directionof the current in the wire positive. Now if there were only one wall, say W1,we could remove it if we placed an image source (with opposite polarity) at theposition marked S1. But with both walls in place there will also be an imageof S0 in the wall W2, which we show as the image S2. This source, too, will havean image in W1, which we call S3. Now both S1 and S3 will have images in W2at the positions marked S4 and S6, and so on. For our two plane conductorswith the source halfway between, the ﬁelds are the same as those produced byan inﬁnite line of sources, all separated by the distance a. (It is, in fact justwhat you would see if you looked at a wire placed halfway between two parallelmirrors.) For the ﬁelds to be zero at the walls, the polarity of the currents in theimages must alternate from one image to the next. In other words, they oscillate180◦ out of phase. The waveguide ﬁeld is, then, just the superposition of theﬁelds of such an inﬁnite set of line sources.

We know that if we are close to the sources, the ﬁeld is very much like thestatic ﬁelds. We considered in Section 7-5 the static ﬁeld of a grid of line sourcesand found that it is like the ﬁeld of a charged plate except for terms that decreaseexponentially with the distance from the grid. Here the average source strengthis zero, because the sign alternates from one source to the next. Any ﬁelds whichexist should fall oﬀ exponentially with distance. Close to the source, we see theﬁeld mainly of the nearest source; at large distances, many sources contributeand their average eﬀect is zero. So now we see why the waveguide below cutoﬀfrequency gives an exponentially decreasing ﬁeld. At low frequencies, in particular,the static approximation is good, and it predicts a rapid attenuation of the ﬁeldswith distance.

Now we are faced with the opposite question: Why are waves propagatedat all? That is the mysterious part! The reason is that at high frequencies theretardation of the ﬁelds can introduce additional changes in phase which cancause the ﬁelds of the out-of-phase sources to add instead of cancelling. In fact,in Chapter 29 of Vol. I we have already studied, just for this problem, the ﬁeldsgenerated by an array of antennas or by an optical grating. There we found thatwhen several radio antennas are suitably arranged, they can give an interferencepattern that has a strong signal in some direction but no signal in another.

Suppose we go back to Fig. 24-15 and look at the ﬁelds which arrive at alarge distance from the array of image sources. The ﬁelds will be strong only incertain directions which depend on the frequency—only in those directions forwhich the ﬁelds from all the sources add in phase. At a reasonable distance fromthe sources the ﬁeld propagates in these special directions as plane waves. Wehave sketched such a wave in Fig. 24-16, where the solid lines represent the wavecrests and the dashed lines represent the troughs. The wave direction will be theone for which the diﬀerence in the retardation for two neighboring sources to thecrest of a wave corresponds to one-half a period of oscillation. In other words, thediﬀerence between r2 and r0 in the ﬁgure is one-half of the free-space wavelength:

The angle θ is then given by

r2 − r0 = λ02 .

sin θ = λ02a

.

(24.33)

There is, of course, another set of waves travelling downward at the symmetricangle with respect to the array of sources. The complete waveguide ﬁeld (not24-11

Fig. 24-15. The line source S0 betweenthe conducting plane walls W1 and W2. Thewalls can be replaced by the inﬁnite sequenceof image sources.

Fig. 24-16. One set of coherent waves

from an array of line sources.

too close to the source) is the superposition of these two sets of waves, as shownin Fig. 24-17. The actual ﬁelds are really like this, of course, only between thetwo walls of the waveguide.

At points like A and C, the crests of the two wave patterns coincide, and theﬁeld will have a maximum; at points like B, both waves have their peak negativevalue, and the ﬁeld has its minimum (largest negative) value. As time goes on theﬁeld in the guide appears to be travelling along the guide with a wavelength λg,which is the distance from A to C. That distance is related to θ by

cos θ = λ0λg

.

Using Eq. (24.33) for θ, we get that

λg = λ0cos θ

=

p1 − (λ0/2a)2 ,

λ0

(24.34)

(24.35)

which is just what we found in Eq. (24.19).

Now we see why there is only wave propagation above the cutoﬀ frequency ω0.If the free-space wavelength is longer than 2a, there is no angle where the wavesshown in Fig. 24-16 can appear. The necessary constructive interference appearssuddenly when λ0 drops below 2a, or when ω goes above ω0 = πc/a.If the frequency is high enough, there can be two or more possible directionsin which the waves will appear. For our case, this will happen if λ0 < 23 a. Ingeneral, however, it could also happen when λ0 < a. These additional wavescorrespond to the higher guide modes we have mentioned.It has also been made evident by our analysis why the phase velocity of theguided waves is greater than c and why this velocity depends on ω. As ω ischanged, the angle of the free waves of Fig. 24-16 changes, and therefore so doesthe velocity along the guide.

Although we have described the guided wave as the superposition of the ﬁeldsof an inﬁnite array of line sources, you can see that we would arrive at the sameresult if we imagined two sets of free-space waves being continually reﬂected backand forth between two perfect mirrors—remembering that a reﬂection meansa reversal of phase. These sets of reﬂecting waves would all cancel each otherunless they were going at just the angle θ given in Eq. (24.33). There are manyways of looking at the same thing.

Fig. 24-17. The waveguide ﬁeld can beviewed as the superposition of two trains ofplane waves.

24-12

25

Electrodynamics in Relativistic Notation

25-1 Four-vectorsWe

now discuss the application of the special theory of relativity to electrody-namics. Since we have already studied the special theory of relativity in Chapters15 through 17 of Vol. I, we will just review quickly the basic ideas.

It is found experimentally that the laws of physics are unchanged if we movewith uniform velocity. You can’t tell if you are inside a spaceship moving withuniform velocity in a straight line, unless you look outside the spaceship, or atleast make an observation having to do with the world outside. Any true law ofphysics we write down must be arranged so that this fact of nature is built in.The relationship between the space and time of two systems of coordinates,one, S0, in uniform motion in the x-direction with speed v relative to the other,S, is given by the Lorentz transformation:t0 = t − vx√1 − v2 ,x0 = x − vt√1 − v2 ,

y0 = y,

z0 = z.

(25.1)

The laws of physics must be such that after a Lorentz transformation, the newform of the laws looks just like the old form. This is just like the principle thatthe laws of physics don’t depend on the orientation of our coordinate system.In Chapter 11 of Vol. I, we saw that the way to describe mathematically theinvariance of physics with respect to rotations was to write our equations in termsof vectors.

For example, if we have two vectors

A = (Ax, Ay, Az)

and

B = (Bx, By, Bz),

we found that the combination

A · B = AxBx + AyBy + AzBz

25-1 Four-vectors25-2 The scalar product25-3 The four-dimensional gradient25-4 Electrodynamics in

four-dimensional notation

25-5 The four-potential of a moving

charge

25-6 The invariance of the equations of

electrodynamics

In this chapter: c = 1

Review: Chapter 15, Vol. I, The SpecialTheory of RelativityChapter 16, Vol. I, RelativisticEnergy and MomentumChapter 17, Vol. I, Space-TimeChapter 13, Vol. II, Magneto-statics

was not changed if we transformed to a rotated coordinate system. So we knowthat if we have a scalar product like A · B on both sides of an equation, theequation will have exactly the same form in all rotated coordinate systems. Wealso discovered an operator (see Chapter 2),

(cid:19)

,

(cid:18) ∂

∇ =

,

∂∂y

,

∂∂z

∂x

which, when applied to a scalar function, gave three quantities which transformjust like a vector. With this operator we deﬁned the gradient, and in combinationwith other vectors, the divergence and the Laplacian. Finally we discovered thatby taking sums of certain products of pairs of the components of two vectors wecould get three new quantities which behaved like a new vector. We called it thecross product of two vectors. Using the cross product with our operator ∇ wethen deﬁned the curl of a vector.Since we will be referring back to what we have done in vector analysis, wehave put in Table 25-1 a summary of all the important vector operations in threedimensions that we have used in the past. The point is that it must be possible towrite the equations of physics so that both sides transform the same way under25-1

Table 25-1

The important quantities and operationsof vector analysis in three dimensions

Deﬁnition of a

vector

Scalar productDiﬀerential vector

operator

GradientDivergenceLaplacianCross productCurl

A = (Ax, Ay, Az)A · B

∇∇φ∇ · A∇ · ∇ = ∇2A × B∇ × A

rotations. If one side is a vector, the other side must also be a vector, and bothsides will change together in exactly the same way if we rotate our coordinatesystem. Similarly, if one side is a scalar, the other side must also be a scalar, sothat neither side changes when we rotate coordinates, and so on.

Now in the case of special relativity, time and space are inextricably mixed,and we must do the analogous things for four dimensions. We want our equationsto remain the same not only for rotations, but also for any inertial frame. Thatmeans that our equations should be invariant under the Lorentz transformationof equations (25.1). The purpose of this chapter is to show you how that can bedone. Before we get started, however, we want to do something that makes ourwork a lot easier (and saves some confusion). And that is to choose our units oflength and time so that the speed of light c is equal to 1. You can think of it astaking our unit of time to be the time that it takes light to go one meter (whichis about 3 × 10−9 sec). We can even call this time unit「one meter.」Using thisunit, all of our equations will show more clearly the space-time symmetry. Also,all the c’s will disappear from our relativistic equations. (If this bothers you, youcan always put the c’s back into any equation by replacing every t by ct, or, ingeneral, by sticking in a c wherever it is needed to make the dimensions of theequations come out right.) With this groundwork we are ready to begin. Ourprogram is to do in the four dimensions of space-time all of the things we didwith vectors for three dimensions. It is really quite a simple game; we just workby analogy. The only real complications is the notation (we’ve already used upthe vector symbol for three dimensions) and one slight twist of signs.

First, by analogy with vectors in three dimensions, we deﬁne a four-vectoras a set of the four quantities at, ax, ay, and az, which transform like t, x, y,and z when we change to a moving coordinate system. There are several diﬀerentnotations people use for a four-vector; we will write aµ, by which we mean thegroup of four numbers (at, ax, ay, az)—in other words, the subscript µ can takeon the four「values」t, x, y, z. It will also be convenient, at times, to indicatethe three space components by a three-vector, like this: aµ = (at, a).We have already encountered one four-vector, which consists of the energyand momentum of a particle (Chapter 17, Vol. I): In our new notation we write

pµ = (E, p),

(25.2)which means that the four-vector pµ is made up of the energy E and the threecomponents of the three-vector p of a particle.It looks as though the game is really very simple—for each three-vector inphysics all we have to do is ﬁnd what the remaining component should be, andwe have a four-vector. To see that this is not the case, consider the velocityvector with components

vx = dxdt

,

vy = dydt

,

vz = dzdt

.

The question is: What is the time component? Instinct should give the rightanswer. Since four-vectors are like t, x, y, z, we would guess that the timecomponent is

vt = dtdt

= 1.

This is wrong. The reason is that the t in each denominator is not an invari-ant when we make a Lorentz transformation. The numerators have the rightbehavior to make a four-vector, but the dt in the denominator spoils things; it isunsymmetric and is not the same in two diﬀerent systems.It turns out that the four「velocity」components which we have written downwill become the components of a four-vector if we just divide by √1 − v2. Wecan see that that is true because if we start with the momentum four-vector

(cid:18) m0√1 − v2 ,

(cid:19)

pµ = (E, p) =

m0v√1 − v2

,

(25.3)

25-2

and divide it by the rest mass m0, which is an invariant scalar in four dimensions,we have

(cid:19)

(cid:18)

=

pµm0

1√1 − v2 ,

v√1 − v2

,

(25.4)

which must still be a four-vector. (Dividing by an invariant scalar doesn’t changethe transformation properties.) So we can deﬁne the「velocity four-vector」uµ by

ut =

ux =

1√1 − v2 ,vx√1 − v2 ,

uy =

uz =

vy√1 − v2 ,vz√1 − v2 ,

The four-velocity is a useful quantity; we can, for instance, write

pµ = m0uµ.

(25.5)

(25.6)

This is the typical sort of form an equation which is relativistically correct musthave; each side is a four-vector. (The right-hand side is an invariant times afour-vector, which is still a four-vector.)

25-2 The scalar productIt is an accident of life, if you wish, that under coordinate rotations thedistance of a point from the origin does not change. This means mathematicallythat r2 = x2 + y2 + z2 is an invariant. In other words, after a rotation r02 = r2,or

x02 + y02 + z02 = x2 + y2 + z2.

Now the question is: Is there a similar quantity which is invariant under theLorentz transformation? There is. From Eq. (25.1) you can see that

t02 − x02 = t2 − x2.

That is pretty nice, except that it depends on a particular choice of the x-direction.We can ﬁx that up by subtracting y2 and z2. Then any Lorentz transformationplus a rotation will leave the quantity unchanged. So the quantity which isanalogous to r2 for three dimensions, in four dimensions is

t2 − x2 − y2 − z2.

It is an invariant under what is called the「complete Lorentz group」—whichmeans for transformation of both translations at constant velocity and rotations.Now since this invariance is an algebraic matter depending only on thetransformation rules of Eq. (25.1)—plus rotations—it is true for any four-vector(by deﬁnition they all transform the same). So for a four-vector aµ we have that

t − a02a02

x − a02

y − a02

z

= a2

t − a2

x − a2

y − a2z.

We will call this quantity the square of「the length」of the four-vector aµ.(Sometimes people change the sign of all the terms and call the length a2+z − a2a2form in the same way, so the combination

Now if we have two vectors aµ and bµ their corresponding components trans-

, so you’ll have to watch out.)

+ a2

x

y

t

atbt − axbx − ayby − azbz

is also an invariant (scalar) quantity. (We have in fact already proved this inChapter 17 of Vol. I.) Clearly this expression is quite analogous to the dot productfor vectors. We will, in fact, call it the dot product or scalar product of twofour-vectors. It would seem logical to write it as aµ · bµ, so it would look like a dotproduct. But, unhappily, it’s not done that way; it is usually written without the25-3

aµbµ = atbt − axbx − ayby − azbz.

dot. So we will follow the convention and write the dot product simply as aµbµ.So, by deﬁnition,(25.7)Whenever you see two identical subscripts together (we will occasionally have touse ν or some other letter instead of µ) it means that you are to take the fourproducts and sum, remembering the minus sign for the products of the spacecomponents. With this convention the invariance of the scalar product under aLorentz transformation can be written as

a0µb0

µ

= aµbµ.

Since the last three terms in (25.7) are just the scalar dot product in three

dimensions, it is often more convenient to writeaµbµ = atbt − a · b.

It is also obvious that the four-dimensional length we described above can bewritten as aµaµ:

aµaµ = a2

t − a2

x − a2

y − a2

z

= a2

t − a · a.

(25.8)

It will also be convenient to sometimes write this quantity as a2

µ

:

µ ≡ aµaµ.a2

We will now give you an illustration of the usefulness of four-vector dot

products. Antiprotons (P) are produced in large accelerators by the reaction

P + P → P + P + P + P.

That is, an energetic proton collides with a proton at rest (for example, in ahydrogen target placed in the beam), and if the incident proton has enoughenergy, a proton-antiproton pair may be produced, in addition to the two originalprotons.* The question is: How much energy must be given to the incident protonto make this reaction energetically possible?

The easiest way to get the answer is to consider what the reaction lookslike in the center-of-mass (CM) system (see Fig. 25-1). We’ll call the incident

Fig. 25-1. The reaction P + P → 3P + Pviewed in the laboratory and CM systems.The incident proton is supposed to have justbarely enough energy to make the reactiongo. Protons are denoted by solid circles;antiprotons by open circles.

* You may well ask: Why not consider the reactionsP + P → P + P + P,

or even

P + P → P + P

which clearly require less energy? The answer is that a principle called conservation of baryonstells us the quantity「number of protons minus number of antiprotons」cannot change. Thisquantity is 2 on the left side of our reaction. Therefore, if we want an antiproton on the rightside, we must have also three protons (or other baryons).

25-4

µ

. Similarly, we’ll call the target proton bproton a and its four-momentum paand its four-momentum pb. If the incident proton has just barely enough energyto make the reaction go, the ﬁnal state—the situation after the collision—willconsist of a glob containing three protons and an antiproton at rest in the CMsystem. If the incident energy were slightly higher, the ﬁnal state particles wouldhave some kinetic energy and be moving apart; if the incident energy were slightlylower, there would not be enough energy to make the four particles.

µ

the total four-momentum of the whole glob in the ﬁnal state,

If we call pc

µ

conservation of energy and momentum tells us that

and

pa + pb = pc,

Ea + Eb = Ec.

Combining these two equations, we can write that

µ

paµ

+ pb

= pcµ.

(25.9)Now the important thing is that this is an equation among four-vectors, andis, therefore, true in any inertial frame. We can use this fact to simplify ourcalculations. We start by taking the「length」of each side of Eq. (25.9); they are,of course, also equal. We get(pa

(25.10)is invariant, we can evaluate it in any coordinate system. In the CMSince pcis the rest energy of four protons, namely 4M,system, the time component of pc= (4M, 0). We have used the fact that theand the space part p is zero; so pcrest mass of an antiproton equals the rest mass of a proton, and we have calledthis common mass M.

) = pc

+ pb

+ pb

)(pa

µpcµ.

µpcµ

µ

µ

µ

µ

µ

µ

Thus, Eq. (25.10) becomes

paµpaµ

+ 2pa

(25.11)are very easy, since the「length」of the momentum four-vector

= 16M 2.

+ pb

µpbµ

µpbµ

Now paof any particle is just the mass of the particle squared:

and pb

µpbµ

µpaµ

pµpµ = E2 − p2 = M 2.

This can be shown by direct calculation or, more cleverly, by noting that for aparticle at rest pµ = (M, 0), so pµpµ = M 2. But since it is an invariant, it isequal to M 2 in any frame. Using these results in Eq. (25.11), we have

or

2pa

µpbµ

= 14M 2

paµpbµNow we can also evaluate pa

(25.12)0 in the laboratory system. The0 = (M, 0), since it describesfour-vector pa0 must also be equal to M Ea0; and since we knowa proton at rest. Thus, pathe scalar product is an invariant this must be numerically the same as what wefound in (25.12). So we have that

0 can be written (Ea0, pa0), while pb

= 7M 2.0pb= pa

µpbµ

0pb

µ

µ

µ

µ

µ

µ

Ea0 = 7M,

which is the result we were after. The total energy of the initial proton mustbe at least 7M (about 6.6 Gev since M = 938 MeV) or, subtracting the restmass M, the kinetic energy must be at least 6M (about 5.6 Gev). The Bevatronaccelerator at Berkeley was designed to give about 6.2 Gev of kinetic energy tothe protons it accelerates, in order to be able to make antiprotons.Since scalar products are invariant, they are always interesting to evaluate.

What about the「length」of the four-velocity uµuµ?1 − v2 − v21 − v2

t − u2 = 1

uµuµ = u2

Thus, uµ is the unit four-vector.

= 1.

25-5

25-3 The four-dimensional gradientThe next thing that we have to discuss is the four-dimensional analog of thegradient. We recall (Chapter 14, Vol. I) that the three diﬀerential operators∂/∂x, ∂/∂y, ∂/∂z transform like a three-vector and are called the gradient. Thesame scheme ought to work in four dimensions; that is, we might guess that thefour-dimensional gradient should be (∂/∂t, ∂/∂x, ∂/∂y, ∂/∂z). This is wrong.To see the error, consider a scalar function φ which depends only on x and t.The change in φ, if we make a small change ∆t in t while holding x constant, is

∆φ = ∂φ∂t

∆t.

(25.13)

On the other hand, according to a moving observer,∂t0 ∆t0.

∂x0 ∆x0 + ∂φ

∆φ = ∂φ

We can express ∆x0 and ∆t0 in terms of ∆t by using Eq. (25.1). Rememberingthat we are holding x constant, so that ∆x = 0, we write∆t0 = ∆t√1 − v2 . ∆t√1 − v2

v√1 − v2

+ ∂φ∂t0

Thus,

!

∆t;

∆x0 = −

v√1 − v2 ∆φ = ∂φ(cid:18) ∂φ∂x0∂t0 − v

−

=

Comparing this result with Eq. (25.13), we learn that

∆t

∂φ∂x0

!(cid:19) ∆t√1 − v2 .(cid:18) ∂φ1√1 − v2∂t0 − v(cid:18) ∂φ∂x0 − v

1√1 − v2

(cid:19)(cid:19)

.

.

∂φ∂x0

∂φ∂t0

∂φ∂tA similar calculation gives

=

=

∂φ∂x

(25.14)

(25.15)

Now we can see that the gradient is rather strange. The formulas for x and t

in terms of x0 and t0 [obtained by solving Eq. (25.1)] are:x = x0 + vt0√1 − v2 .

t = t0 + vx0√1 − v2 ,

This is the way a four-vector must transform. But Eqs. (25.14) and (25.15) havea couple of signs wrong!The answer is that instead of the incorrect (∂/∂t,∇), we must deﬁne thefour-dimensional gradient operator, which we will call ∇µ, by

∇µ =

,−∇

=

,− ∂∂x

,− ∂∂y

,− ∂∂z

∂t

(25.16)

With this deﬁnition, the sign diﬃculties encountered above go away, and ∇µbehaves as a four-vector should. (It’s rather awkward to have those minus signs,but that’s the way the world is.) Of course, what it means to say that ∇µ「behaveslike a four-vector」is simply that the four-gradient of a scalar is a four-vector.If φ is a true scalar invariant ﬁeld (Lorentz invariant) then ∇µφ is a four-vectorﬁeld.All right, now that we have vectors, gradients, and dot products, the nextthing is to look for an invariant which is analogous to the divergence of three-dimensional vector analysis. Clearly, the analog is to form the expression ∇µbµ,25-6

(cid:18) ∂

∂t

(cid:19)

(cid:18) ∂

(cid:19)

.

where bµ is a four-vector ﬁeld whose components are functions of space and time.We deﬁne the divergence of the four-vector bµ = (bt, b) as the dot product of ∇µand bµ:

(cid:18)

(cid:19)

(cid:18)

(cid:19)

(cid:18)

(cid:19)

bx −

− ∂∂y

by −

− ∂∂z

bz

(25.17)

∇µbµ = ∂∂t= ∂∂t

bt −

− ∂∂xbt + ∇ · b,

where ∇ · b is the ordinary three-divergence of the three-vector b. Note thatone has to be careful with the signs. Some of the minus signs come from thedeﬁnition of the scalar product, Eq. (25.7); the others are required because thespace components of ∇µ are −∂/∂x, etc., as in Eq. (25.16). The divergence asdeﬁned by (25.17) is an invariant and gives the same answer in all coordinatesystems which diﬀer by a Lorentz transformation.

Let’s look at a physical example in which the four-divergence shows up. Wecan use it to solve the problem of the ﬁelds around a moving wire. We have alreadyseen (Section 13-7) that the electric charge density ρ and the current density jform a four-vector jµ = (ρ, j). If an uncharged wire carries the current jx, thenin a frame moving past it with velocity v (along x), the wire will have the chargeand current density [obtained from the Lorentz transformation Eqs. (25.1)] asfollows:

ρ0 = −vjx√1 − v2 ,

j0

x

=

jx√1 − v2 .

These are just what we found in Chapter 13. We can then use these sources

in Maxwell’s equations in the moving system to ﬁnd the ﬁelds.four-vector notation. Consider the four divergence of jµ:

The charge conservation law, Section 13-2, also takes on a simple form in the

∇µjµ = ∂ρ∂t

+ ∇ · j.

(25.18)

The law of the conservation of charge says that the outﬂow of current per unitvolume must equal the negative rate of increase of charge density. In other words,that

This operator, which is the analog of the three-dimensional Laplacian, is calledthe D’Alembertian and has a special notation:(cid:3)2 = ∇µ∇µ = ∂2

(25.20)

∂t2 − ∇2.

25-7

∇ · j = − ∂ρ∂t

.

Putting this into Eq. (25.18), the law of conservation of charge takes on thesimple form

(25.19)Since ∇µjµ is an invariant scalar, if it is zero in one frame it is zero in all frames.We have the result that if charge is conserved in one coordinate system, it isconserved in all coordinate systems moving with uniform velocity.As our last example we want to consider the scalar product of the gradientoperator ∇µ with itself. In three dimensions, such a product gives the Laplacian

∇µjµ = 0.

What do we get in four dimensions? That’s easy. Following our rules for dotproducts and gradients, we get

∇2 = ∇ · ∇ = ∂2∂x2(cid:18)(cid:19)

(cid:19)(cid:18)

+ ∂2+ ∂2∂z2 .∂y2(cid:19)(cid:18)

(cid:19)

− ∂∂x

− ∂∂x

−

− ∂∂y

(cid:18)

(cid:18)

(cid:19)(cid:18)

(cid:19)

− ∂∂y

−

− ∂∂z

− ∂∂z

−

∂∂t

∇µ∇µ = ∂∂t= ∂2∂t2 − ∇2.

From its deﬁnition it is an invariant scalar operator; if it operates on a four-vectorﬁeld, it produces a new four-vector ﬁeld. (Some people deﬁne the D’Alembertianwith the opposite sign to Eq. (25.20), so you will have to be careful when readingthe literature.)

We have now found four-dimensional equivalents of most of the three-dimen-sional quantities we had listed in Table 25-1. (We do not yet have the equivalentsof the cross product and the curl operation; we won’t get to them until the nextchapter.) It may help you remember how they go if we put all the importantdeﬁnitions and results together in one place, so we have made such a summaryin Table 25-2.

The important quantities of vector analysis in three and four dimensions.

Table 25-2

Vector

Scalar product

Vector operator

Gradient

Divergence

Laplacian andD’Alembertian

Three dimensions

A = (Ax, Ay, Az)

A · B = AxBx + AyBy + AzBz

∇ = (∂/∂x, ∂/∂y, ∂/∂z)

(cid:18) ∂ψ

∂x

∇ψ =

,

∂ψ∂y

,

∂ψ∂z

(cid:19)

Four dimensions

aµ = (at, ax, ay, az) = (at, a)

aµbµ = atbt − axbx − ayby − azbz = atbt − a · b∇µ = (∂/∂t,−∂/∂x,−∂/∂y,−∂/∂z) = (∂/∂t,−∇)

∇µϕ =

,− ∂ϕ∂x

,− ∂ϕ∂y

,− ∂ϕ∂z

=

,−∇ϕ

(cid:19)

(cid:18) ∂ϕ

∂t

(cid:19)

(cid:18) ∂ϕ

∂t

∇ · A = ∂Ax∂x

+ ∂Ay∂y

+ ∂Az∂z

∇µaµ = ∂at∂t

+ ∂ax∂x

+ ∂ay∂y

+ ∂az∂z

= ∂at∂t

+ ∇ · a

∇ · ∇ = ∂2

∂x2 + ∂2

∂y2 + ∂2

∂z2 = ∇2

∇µ∇µ = ∂2

∂t2 − ∂2

∂x2 − ∂2

∂y2 − ∂2

∂z2 = ∂2

∂t2 − ∇2 = (cid:3)2

25-4 Electrodynamics in four-dimensional notationWe have already encountered the D’Alembertian operator, without givingit that name, in Section 18-6; the diﬀerential equations we found there for thepotentials can be written in the new notations as:

(cid:3)2φ = ρ0

,

(cid:3)2A = j0

.

(25.21)

The four quantities on the right-hand side of the two equations in (25.21) areρ, jx, jy, jz divided by 0, which is a universal constant which will be the samein all coordinate systems if the same unit of charge is used in all frames. So thefour quantities ρ/0, jx/0, jy/0, jz/0 also transform as a four-vector. We canwrite them as jµ/0. The D’Alembertian doesn’t change when the coordinatesystem is changed, so the quantities φ, Ax, Ay, Az must also transform like afour-vector—which means that they are the components of a four-vector. Inshort,

Aµ = (φ, A)

is a four-vector. What we call the scalar and vector potentials are really diﬀerentaspects of the same physical thing. They belong together. And if they arekept together the relativistic invariance of the world is obvious. We call Aµ thefour-potential.

In the four-vector notation Eqs. (25.21) become simply

(cid:3)2Aµ = jµ0

,

(25.22)

25-8

The physics of this equation is just the same as Maxwell’s equations. But there issome pleasure in being able to rewrite them in an elegant form. The pretty formis also meaningful; it shows directly the invariance of electrodynamics under theLorentz transformation.

Remember that Eqs. (25.21) could be deduced from Maxwell’s equations only

if we imposed the gauge condition

∂φ∂t

+ ∇ · A = 0,

(25.23)which just says ∇µAµ = 0; the gauge condition says that the divergence of thefour-vector Aµ is zero. This condition is called the Lorenz condition. It is veryconvenient because it is an invariant condition and therefore Maxwell’s equationsstay in the form of Eq. (25.22) for all frames.

25-5 The four-potential of a moving chargeAlthough it is implicit in what we have already said, let us write down thetransformation laws which give φ and A in a moving system in terms of φ and Ain a stationary system. Since Aµ = (φ, A) is a four-vector, the equations mustlook just like Eqs. (25.1), except that t is replaced by φ, and x is replaced by A.Thus,

φ0 = φ − vAx√1 − v2 ,= Ax − vφ√1 − v2 ,

x

A0

A0

y

= Ay,

A0

z

= Az.

(25.24)

This assumes that the primed coordinate system is moving with speed v in thepositive x-direction, as measured in the unprimed coordinate system.We will consider one example of the usefulness of the idea of the four-potential.What are the vector and scalar potentials of a charge q moving with speed valong the x-axis? The problem is easy in a coordinate system moving with thecharge, since in this system the charge is standing still. Let’s say that the chargeis at the origin of the S0-frame, as shown in Fig. 25-2. The scalar potential inthe moving system is then given by

φ0 = q

4π0r0 ,

(25.25)

r0 being the distance from q to the ﬁeld point, as measured in the moving system.The vector potential A0 is, of course, zero.Now it is straightforward to ﬁnd φ and A, the potentials as measured in thestationary coordinates. The inverse relations to Eqs. (25.24) are

x

φ = φ0 + vA0√1 − v2 ,Ax = A0+ vφ0√1 − v2 ,

x

Az = A0z.Using the φ0 given by Eq. (25.25), and A0 = 0, we get

Ay = A0y,

(25.26)

φ = q4π0= q4π0

1

r0√1 − v2√1 − v2px02 + y02 + z02

1

.

This gives us the scalar potential φ we would see in S, but, unfortunately,expressed in terms of the S0 coordinates. We can get things in terms of t, x, y, zby substituting for t0, x0, y0, and z0, using (25.1). We get

φ = q4π0

1√1 − v2

q[(x − vt)/

1

√1 − v2]2 + y2 + z2

.

(25.27)

25-9

Fig. 25-2. The frame S(cid:48) moves with ve-locity v (in the x-direction) with respectto S. A charge at rest at the origin of S(cid:48) isat x = v t in S. The potentials at P can becomputed in either frame.

Following the same procedure for the components of A, you can show that

These are the same formulas we derived by a diﬀerent method in Chapter 21.

A = vφ.

(25.28)

25-6 The invariance of the equations of electrodynamicsWe have found that the potentials φ and A taken together form a four-vector which we call Aµ, and that the wave equations—the full equations whichdetermine the Aµ in terms of the jµ—can be written as in Eq. (25.22). Thisequation, together with the conservation of charge, Eq. (25.19), gives us thefundamental law of the electromagnetic ﬁeld:

(cid:3)2Aµ = 1

0

jµ,

∇µjµ = 0.

(25.29)

There, in one tiny space on the page, are all of the Maxwell equations—beautifuland simple. Did we learn anything from writing the equations this way, besidesthat they are beautiful and simple? In the ﬁrst place, is it anything diﬀerent fromwhat we had before when we wrote everything out in all the various components?Can we from this equation deduce something that could not be deduced fromthe wave equations for the potentials in terms of the charges and currents? Theanswer is deﬁnitely no. The only thing we have been doing is changing thenames of things—using a new notation. We have written a square symbol torepresent the derivatives, but it still means nothing more nor less than the secondderivative with respect to t, minus the second derivative with respect to x, minusthe second derivative with respect to y, minus the second derivative with respectto z. And the µ means that we have four equations, one each for µ = t, x, y,or z. What then is the signiﬁcance of the fact that the equations can be writtenin this simple form? From the point of view of deducing anything directly, itdoesn’t mean anything. Perhaps, though, the simplicity of the equations meansthat nature also has a certain simplicity.

Let us show you something interesting that we have recently discovered: All

of the laws of physics can be contained in one equation. That equation is

U = 0.

(25.30)

What a simple equation! Of course, it is necessary to know what the symbol means.U is a physical quantity which we will call the「unworldliness」of the situation.And we have a formula for it. Here is how you calculate the unworldliness. Youtake all of the known physical laws and write them in a special form. For example,suppose you take the law of mechanics, F = ma, and rewrite it as F − ma = 0.Then you can call (F − ma)—which should, of course, be zero—the「mismatch」of mechanics. Next, you take the square of this mismatch and call it U1, whichcan be called the「unworldliness of mechanical eﬀects.」In other words, you take

U1 = (F − ma)2.

(25.31)

Now you write another physical law, say, ∇ · E = ρ/0 and deﬁne

(cid:19)2

,

(cid:18)

U2 =

∇ · E − ρ0

which you might call「the gaussian unworldliness of electricity.」You continue towrite U3, U4, and so on—one for every physical law there is.

unworldlinesses Ui from all the subphenomena that are involved; that is, U =P Ui.

Finally you call the total unworldliness U of the world the sum of the various

Then the great「law of nature」is

U = 0.

(25.32)25-10

This「law」means, of course, that the sum of the squares of all the individualmismatches is zero, and the only way the sum of a lot of squares can be zero isfor each one of the terms to be zero.

So the「beautifully simple」law in Eq. (25.32) is equivalent to the wholeseries of equations that you originally wrote down. It is therefore absolutelyobvious that a simple notation that just hides the complexity in the deﬁnitionsof symbols is not real simplicity. It is just a trick. The beauty that appears inEq. (25.32)—just from the fact that several equations are hidden within it—isno more than a trick. When you unwrap the whole thing, you get back whereyou were before.

However, there is more to the simplicity of the laws of electromagnetismwritten in the form of Eq. (25.29). It means more, just as a theory of vectoranalysis means more. The fact that the electromagnetic equations can be writtenin a very particular notation which was designed for the four-dimensional geometryof the Lorentz transformations—in other words, as a vector equation in the four-space—means that it is invariant under the Lorentz transformations. It is becausethe Maxwell equations are invariant under those transformations that they canbe written in a beautiful form.

It is no accident that the equations of electrodynamics can be written in thebeautifully elegant form of Eq. (25.29). The theory of relativity was developedbecause it was found experimentally that the phenomena predicted by Maxwell’sequations were the same in all inertial systems. And it was precisely by studyingthe transformation properties of Maxwell’s equations that Lorentz discovered histransformation as the one which left the equations invariant.

There is, however, another reason for writing our equations this way. It hasbeen discovered—after Einstein guessed that it might be so—that all of the lawsof physics are invariant under the Lorentz transformation. That is the principleof relativity. Therefore, if we invent a notation which shows immediately when alaw is written down whether it is invariant or not, we can be sure that in tryingto make new theories we will write only equations which are consistent with theprinciple of relativity.

The fact that the Maxwell equations are simple in this particular notation isnot a miracle, because the notation was invented with them in mind. But theinteresting physical thing is that every law of physics—the propagation of mesonwaves or the behavior of neutrinos in beta decay, and so forth—must have thissame invariance under the same transformation. Then when you are moving at auniform velocity in a spaceship, all of the laws of nature transform together insuch a way that no new phenomenon will show up. It is because the principle ofrelativity is a fact of nature that in the notation of four-dimensional vectors theequations of the world will look simple.

25-11

26

Lorentz Transformations of the Fields

