26-1 The four-potential of a moving chargeWe

saw in the last chapter that the potential Aµ = (φ, A) is a four-vector.The time component is the scalar potential φ, and the three space components arethe vector potential A. We also worked out the potentials of a particle movingwith uniform speed on a straight line by using the Lorentz transformation. (Wehad already found them by another method in Chapter 21.) For a point chargewhose position at the time t is (vt, 0, 0), the potentials at the point (x, y, z) are

φ =

Ax =

1√1 − v21√1 − v2

4π0

4π0

Ay = Az = 0.

(cid:20)(x − vt)2(cid:20)(x − vt)2

1 − v2

1 − v2

(cid:21)1/2(cid:21)1/2

q+ y2 + z2

qv+ y2 + z2

Equations (26.1) give the potentials at x, y, and z at the time t, for a chargewhose「present」position (by which we mean the position at the time t) isat x = vt. Notice that the equations are in terms of (x − vt), y, and z which arethe coordinates measured from the current position P of the moving charge (seeFig. 26-1). The actual inﬂuence we know really travels at the speed c, so it is thebehavior of the charge back at the retarded position P 0 that really counts.* Thepoint P 0 is at x = vt0 (where t0 = t− r0/c is the retarded time). But we said thatthe charge was moving with uniform velocity in a straight line, so naturally thebehavior at P 0 and the current position are directly related. In fact, if we makethe added assumption that the potentials depend only upon the position and thevelocity at the retarded moment, we have in equations (26.1) a complete formulafor the potentials for a charge moving any way. It works this way. Suppose thatyou have a charge moving in some arbitrary fashion, say with the trajectory inFig. 26-2, and you are trying to ﬁnd the potentials at the point (x, y, z). First,you ﬁnd the retarded position P 0 and the velocity v0 at that point. Then youimagine that the charge would keep on moving with this velocity during the delaytime (t0 − t), so that it would then appear at an imaginary position Pproj, whichwe can call the「projected position,」and would arrive there with the velocity v0.(Of course, it doesn’t do that; its real position at t is at P.) Then the potentialsat (x, y, z) are just what equations (26.1) would give for the imaginary chargeat the projected position Pproj. What we are saying is that since the potentialsdepend only on what the charge is doing at the retarded time, the potentialswill be the same whether the charge continued moving at a constant velocity orwhether it changed its velocity after t0—that is, after the potentials that weregoing to appear at (x, y, z) at the time t were already determined.You know, of course, that the moment that we have the formula for thepotentials from a charge moving in any manner whatsoever, we have the completeelectrodynamics; we can get the potentials of any charge distribution by superpo-sition. Therefore we can summarize all the phenomena of electrodynamics either

* The primes used here to indicate the retarded positions and times should not be confused

with the primes referring to a Lorentz-transformed frame in the preceding chapter.

26-1

26-1 The four-potential of a moving

26-2 The ﬁelds of a point charge with

a constant velocity

26-3 Relativistic transformation of the

charge

ﬁelds

26-4 The equations of motion in

relativistic notation

(26.1)

In this chapter: c = 1

Review: Chapter 20, Vol. II, Solutionof Maxwell’s Equations in FreeSpace

Fig. 26-1. Finding the ﬁelds at (x, y , z )due to a charge q moving along the x-axiswith the constant speed v. The ﬁeld「now」at the point (x, y , z ) can be expressed interms of the「present」position P , as wellas in terms of P (cid:48), the「retarded」position(at t(cid:48) = t − r (cid:48)/c).

by writing Maxwell’s equations or by the following series of remarks. (Rememberthem in case you are ever on a desert island. From them, all can be reconstructed.You will, of course, know the Lorentz transformation; you will never forget thaton a desert island or anywhere else.)First, Aµ is a four-vector. Second, the Coulomb potential for a stationarycharge is q/4π0r. Third, the potentials produced by a charge moving in anyway depend only upon the velocity and position at the retarded time. Withthose three facts we have everything. From the fact that Aµ is a four-vector, wetransform the Coulomb potential, which we know, and get the potentials for aconstant velocity. Then, by the last statement that potentials depend only uponthe past velocity at the retarded time, we can use the projected position game toﬁnd them. It is not a particularly useful way of doing things, but it is interestingto show that the laws of physics can be put in so many diﬀerent ways.

It is sometimes said, by people who are careless, that all of electrodynamicscan be deduced solely from the Lorentz transformation and Coulomb’s law.Of course, that is completely false. First, we have to suppose that there is ascalar potential and a vector potential that together make a four-vector. Thattells us how the potentials transform. Then why is it that the eﬀects at theretarded time are the only things that count? Better yet, why is it that thepotentials depend only on the position and the velocity and not, for instance,on the acceleration? The ﬁelds E and B do depend on the acceleration. If youtry to make the same kind of an argument with respect to them, you wouldsay that they depend only upon the position and velocity at the retarded time.But then the ﬁelds from an accelerating charge would be the same as the ﬁeldsfrom a charge at the projected position—which is false. The ﬁelds depend notonly on the position and the velocity along the path but also on the acceleration.So there are several additional tacit assumptions in this great statement thateverything can be deduced from the Lorentz transformation. (Whenever you seea sweeping statement that a tremendous amount can come from a very smallnumber of assumptions, you always ﬁnd that it is false. There are usually a largenumber of implied assumptions that are far from obvious if you think about themsuﬃciently carefully.)

26-2 The ﬁelds of a point charge with a constant velocityNow that we have the potentials from a point charge moving at constantvelocity, we ought to ﬁnd the ﬁelds—for practical reasons. There are manycases where we have uniformly moving particles—for instance, cosmic rays goingthrough a cloud chamber, or even slow-moving electrons in a wire. So let’s at leastsee what the ﬁelds actually do look like for any speed—even for speeds nearlythat of light—assuming only that there is no acceleration. It is an interestingquestion.

We get the ﬁelds from the potentials by the usual rules:

First, for Ez

E = −∇φ − ∂A∂t

,

B = ∇ × A.

Ez = − ∂φ∂z

− ∂Az∂t

.

Fig. 26-2. A charge moves on an arbitrarytrajectory. The potentials at (x, y , z ) at thetime t are determined by the position P (cid:48)and velocity v (cid:48) at the retarded time t(cid:48)−r (cid:48)/c.They are conveniently expressed in terms ofthe coordinates from the「projected」posi-tion Pproj. (The actual position at t is P .)

But Az is zero; so diﬀerentiating φ in equations (26.1), we get

(cid:20)(x − vt)2(cid:20)(x − vt)2

1 − v2

1 − v2

(cid:21)3/2 .(cid:21)3/2 .

z+ y2 + z2

y+ y2 + z2

Ez =

q

√1 − v2

4π0

Similarly, for Ey,

Ey =

q

√1 − v2

4π0

(26.2)

(26.3)

26-2

The x-component is a little more work. The derivative of φ is more complicatedand Ax is not zero. First,

− ∂φ∂x

=

q

√1 − v2

4π0

(cid:20)(x − vt)2

(x − vt)/(1 − v2)+ y2 + z2

1 − v2

(cid:21)3/2 .

Then, diﬀerentiating Ax with respect to t, we ﬁnd

− ∂Ax∂t

=

q

√1 − v2

4π0

−v2(x − vt)/(1 − v2)

(cid:20)(x − vt)2

1 − v2

(cid:21)3/2 .

+ y2 + z2

And ﬁnally, taking the sum,

Ex =

q

√1 − v2

4π0

(cid:20)(x − vt)2

1 − v2

x − vt+ y2 + z2

(cid:21)3/2 .

(26.4)

(26.5)

(26.6)

We’ll look at the physics of E in a minute; let’s ﬁrst ﬁnd B. For the z-

component,

Bz = ∂Ay∂x

− ∂Ax∂y

.

Since Ay is zero, we have just one derivative to get. Notice, however, that Ax isjust vφ, and ∂/∂y of vφ is just −vEy. So

Bz = vEy.

(26.7)

Fig. 26-4. The electric ﬁeld of a chargemoving with constant speed v = 0.9c,part (b), compared with the ﬁeld of a chargeat rest, part (a).

∂φ∂z

,

Fig. 26-3. For a charge moving with con-stant speed, the electric ﬁeld points radiallyfrom the「present」position of the charge.

Similarly,

and

= +v

− ∂Az∂x

By = ∂Ax∂zBy = −vEz.

B = v × E.

(26.8)Finally, Bx is zero, since Ay and Az are both zero. We can write the magneticﬁeld simply as(26.9)Now let’s see what the ﬁelds look like. We will try to draw a picture of theﬁeld at various positions around the present position of the charge. It is true thatthe inﬂuence of the charge comes, in a certain sense, from the retarded position;but because the motion is exactly speciﬁed, the retarded position is uniquelygiven in terms of the present position. For uniform velocities, it’s nicer to relatethe ﬁelds to the current position, because the ﬁeld components at (x, y, z) dependonly on (x− vt), y, and z—which are the components of the displacement r fromthe present position to (x, y, z) (see Fig. 26-3).Consider ﬁrst a point with z = 0. Then E has only x- and y-components.From Eqs. (26.3) and (26.6), the ratio of these components is just equal to theratio of the x- and y-components of the displacement. That means that E is inthe same direction as r, as shown in Fig. 26-3. Since Ez is also proportional to z,it is clear that this result holds in three dimensions. In short, the electric ﬁeld isradial from the charge, and the ﬁeld lines radiate directly out of the charge, justas they do for a stationary charge. Of course, the ﬁeld isn’t exactly the sameas for the stationary charge, because of all the extra factors of (1 − v2). But wecan show something rather interesting. The diﬀerence is just what you wouldget if you were to draw the Coulomb ﬁeld with a peculiar set of coordinates inwhich the scale of x was squashed up by the factor √1 − v2. If you do that, theﬁeld lines will be spread out ahead and behind the charge and will be squeezedtogether around the sides, as shown in Fig. 26-4.

If we relate the strength of E to the density of the ﬁeld lines in the conventionalway, we see a stronger ﬁeld at the sides and a weaker ﬁeld ahead and behind,26-3

which is just what the equations say. First, if we look at the strength of the ﬁeldat right angles to the line of motion, that is, for (x − vt) = 0, the distance from

the charge ispy2 + z2. Here the total ﬁeld strength isq

, which is

E2y

+ E2

z

E =

q

√1 − v2

4π0

1

y2 + z2 .

(26.10)

The ﬁeld is proportional to the inverse square of the distance—just like the√1 − v2, which isCoulomb ﬁeld except increased by the constant, extra factor 1/always greater than one. So at the sides of a moving charge, the electric ﬁeld isstronger than you get from the Coulomb law. In fact, the ﬁeld in the sidewisedirection is bigger than the Coulomb potential by the ratio of the energy of theparticle to its rest mass.

Ahead of the charge (and behind), y and z are zero and

E = Ex = q(1 − v2)

4π0(x − vt)2 .

(26.11)

The ﬁeld again varies as the inverse square of the distance from the charge butis now reduced by the factor (1 − v2), in agreement with the picture of the ﬁeldlines. If v/c is small, v2/c2 is still smaller, and the eﬀect of the (1 − v2) terms isvery small; we get back to Coulomb’s law. But if a particle is moving very closeto the speed of light, the ﬁeld in the forward direction is enormously reduced,and the ﬁeld in the sidewise direction is enormously increased.

Our results for the electric ﬁeld of a charge can be put this way: Supposeyou were to draw on a piece of paper the ﬁeld lines for a charge at rest, andthen set the picture to travelling with the speed v. Then, of course, the wholepicture would be compressed by the Lorentz contraction; that is, the carbongranules on the paper would appear in diﬀerent places. The miracle of it is thatthe picture you would see as the page ﬂies by would still represent the ﬁeld linesof the point charge. The contraction moves them closer together at the sides andspreads them out ahead and behind, just in the right way to give the correctline densities. We have emphasized before that ﬁeld lines are not real but areonly one way of representing the ﬁeld. However, here they almost seem to bereal. In this particular case, if you make the mistake of thinking that the ﬁeldlines are somehow really there in space, and transform them, you get the correctﬁeld. That doesn’t, however, make the ﬁeld lines any more real. All you needdo to remind yourself that they aren’t real is to think about the electric ﬁeldsproduced by a charge together with a magnet; when the magnet moves, newelectric ﬁelds are produced, and destroy the beautiful picture. So the neat ideaof the contracting picture doesn’t work in general. It is, however, a handy wayto remember what the ﬁelds from a fast-moving charge are like.

The magnetic ﬁeld is v × E [from Eq. (26.9)]. If you take the velocity crossedinto a radial E-ﬁeld, you get a B which circles around the line of motion, asshown in Fig. 26-5. If we put back the c’s, you will see that it’s the same resultwe had for low-velocity charges. A good way to see where the c’s must go is torefer back to the force law,

F = q(E + v × B).

You see that a velocity times the magnetic ﬁeld has the same dimensions as anelectric ﬁeld. So the right-hand side of Eq. (26.9) must have a factor 1/c2:

B = v × Ec2

.

(26.12)

For a slow-moving charge (v (cid:28) c), we can take for E the Coulomb ﬁeld; then

B =

q

4π0c2

v × rr3

.

(26.13)

26-4

Fig. 26-5. The magnetic ﬁeld near a[Compare with

moving charge is v × E.Fig. 26-4.]

Fig. 26-6. The forces between two mov-ing charges are not always equal and oppo-site. It appears that「action」is not equal to「reaction.」

This formula corresponds exactly to equations for the magnetic ﬁeld of a currentthat we found in Section 14-7.

We would like to point out, in passing, something interesting for you to thinkabout. (We will come back to discuss it again later.) Imagine two protons withvelocities at right angles, so that one will cross over the path of the other, but infront of it, so they don’t collide. At some instant, their relative positions will beas in Fig. 26-6(a). We look at the force on q1 due to q2 and vice versa. On q2there is only the electric force from q1, since q1 makes no magnetic ﬁeld along itsline of motion. On q1, however, there is again the electric force but, in addition,a magnetic force, since it is moving in a B-ﬁeld made by q2. The forces are asdrawn in Fig. 26-6(b). The electric forces on q1 and q2 are equal and opposite.However, there is a sidewise (magnetic) force on q1 and no sidewise force on q2.Does action not equal reaction? We leave it for you to worry about.

26-3 Relativistic transformation of the ﬁeldsIn the last section we calculated the electric and magnetic ﬁelds from thetransformed potentials. The ﬁelds are important, of course, in spite of thearguments given earlier that there is physical meaning and reality to the potentials.The ﬁelds, too, are real. It would be convenient for many purposes to have a wayto compute the ﬁelds in a moving system if you already know the ﬁelds in some「rest」system. We have the transformation laws for φ and A, because Aµ is afour-vector. Now we would like to know the transformation laws of E and B.Given E and B in one frame, how do they look in another frame moving past? Itis a convenient transformation to have. We could always work back through thepotentials, but it is useful sometimes to be able to transform the ﬁelds directly.We will now see how that goes.

How can we ﬁnd the transformation laws of the ﬁelds? We know the transfor-mation laws of the φ and A, and we know how the ﬁelds are given in terms of φand A—it should be easy to ﬁnd the transformation for the B and E. (You mightthink that with every vector there should be something to make it a four-vector,so with E there’s got to be something else we can use for the fourth component.And also for B. But it’s not so. It’s quite diﬀerent from what you would expect.)To begin with, let’s take just a magnetic ﬁeld B, which is, of course ∇× A. Nowwe know that the vector potential with its x-, y-, and z-components is only apiece of something; there is also a t-component. Also we know that for derivativeslike ∇, besides the x, y, z parts, there is also a derivative with respect to t. Solet’s try to ﬁgure out what happens if we replace a「y」by a「t」, or a「z」by a「t,」or something like that.First, notice the form of the terms in ∇×A when we write out the components:Bx = ∂Az∂y

By = ∂Ax∂z

Bz = ∂Ay∂x

− ∂Ax∂y

− ∂Ay∂z

− ∂Az∂x

(26.14)

.

,

,

The x-component is equal to a couple of terms that involve only y- and z-components. Suppose we call this combination of derivatives and components a「zy-thing,」and give it a shorthand name, Fzy. We simply mean that

Fzy ≡ ∂Az∂y

− ∂Ay∂z

.

(26.15)

Bx = Fzy,

Similarly, By is equal to the same kind of「thing,」but this time it is an「xz-thing.」And Bz is, of course, the corresponding「yx-thing.」We haveBz = Fyx.

(26.16)Now what happens if we simply try to concoct also some「t」-type things likeFxt and Ftz (since nature should be nice and symmetric in x, y, z, and t)? Forinstance, what is Ftz? It is, of course,∂At∂z

By = Fxz,

− ∂Az∂t

.

26-5

But remember that At = φ, so it is also

∂φ∂z

− ∂Az∂t

.

You’ve seen that before. It is the z-component of E. Well, almost—there is asign wrong. But we forgot that in the four-dimensional gradient the t-derivativecomes with the opposite sign from x, y, and z. So we should really have takenthe more consistent extension of Ftz, asFtz = ∂At∂z

(26.17)Then it is exactly equal to −Ez. Trying also Ftx and Fty, we ﬁnd that the threepossibilities give

+ ∂Az∂t

Ftx = −Ex,

(26.18)What happens if both subscripts are t? Or, for that matter, if both are x?

Fty = −Ey,

Ftz = −Ez.

We get things like

and

Ftt = ∂At∂t

− ∂At∂t

,

Fxx = ∂Ax∂x

− ∂Ax∂x

,

which give nothing but zero.

We have then six of these F-things. There are six more which you get by

reversing the subscripts, but they give nothing really new, since

Fxy = −Fyx,

Fµν = ∇µAν − ∇νAµ,

and so on. So, out of sixteen possible combinations of the four subscripts takenin pairs, we get only six diﬀerent physical objects; and they are the componentsof B and E.To represent the general term of F, we will use the general subscripts µ and ν,where each can stand for 0, 1, 2, or 3—meaning in our usual four-vector notationt, x, y, and z. Also, everything will be consistent with our four-vector notation ifwe deﬁne Fµν by(26.19)remembering that ∇µ = (∂/∂t,−∂/∂x,−∂/∂y,−∂/∂z) and that Aµ = (φ, Ax, Ay,Az).What we have found is that there are six quantities that belong together innature—that are diﬀerent aspects of the same thing. The electric and magneticﬁelds which we have considered as separate vectors in our slow-moving world(where we don’t worry about the speed of light) are not vectors in four-space.They are parts of a new「thing.」Our physical「ﬁeld」is really the six-componentobject Fµν. That is the way we must look at it for relativity. We summarize ourresults on Fµν in Table 26-1.You see that what we have done here is to generalize the cross product. Webegan with the curl operation, and the fact that the transformation propertiesof the curl are the same as the transformation properties of two vectors—theordinary three-dimensional vector A and the gradient operator which we knowalso behaves like a vector. Let’s look for a moment at an ordinary cross productin three dimensions, for example, the angular momentum of a particle. When anobject is moving in a plane, the quantity (xvy − yvx) is important. For motionin three dimensions, there are three such important quantities, which we call theangular momentum:

Lxy = m(xvy − yvx),

Lyz = m(yvz − zvy),

Lzx = m(zvx − xvz).

Then (although you may have forgotten by now) we discovered in Chapter 20of Vol. I the miracle that these three quantities could be identiﬁed with the26-6

Table 26-1

The components of F µν

Fµν = −FνµFµµ = 0

Fxy = −BzFyz = −BxFzx = −By

Fxt = ExFyt = EyFzt = Ez

components of a vector. In order to do so, we had to make an artiﬁcial rule witha right-hand convention. It was just luck. It was luck because Lij (with i and jequal to x, y, or z) was an antisymmetric object:

Lij = −Lji,

Lii = 0.

Of the nine possible quantities, there are only three independent numbers. Andit just happens that when you change coordinate systems these three objectstransform in exactly the same way as the components of a vector.

The same thing lets us represent an element of surface as a vector. A surfaceelement has two parts—say dx and dy—which we can represent by the vector danormal to the surface. But we can’t do that in four dimensions. What is the「normal」to dx dy? Is it along z or along t?In short, for three dimensions it happens by luck that after you’ve taken acombination of two vectors like Lij, you can represent it again by another vectorbecause there are just three terms that happen to transform like the componentsof a vector. But in four dimensions that is evidently impossible, because thereare six independent terms, and you can’t represent six things by four things.

Even in three dimensions it is possible to have combinations of vectors thatcan’t be represented by vectors. Suppose we take any two vectors a = (ax, ay, az)and b = (bx, by, bz), and make the various possible combinations of components,like axbx, axby, etc. There would be nine possible quantities:

axbx,

aybx,

azbx,

axby,

ayby,

azby,

axbz,

aybz,

azbz.

We might call these quantities Tij.If we now go to a rotated coordinate system (say rotated about the z-axis),the components of a and b are changed. In the new system, ax, for example,gets replaced by

And similarly for other components. The nine components of the product quan-tity Tij we have invented are all changed too, of course. For instance, Txy = axbygets changed to

T 0

xy

= axby(cos2 θ) − axbx(cos θ sin θ) + ayby(sin θ cos θ) − aybx(sin2 θ),

or

T 0

xy

= Txy cos2 θ − Txx cos θ sin θ + Tyy sin θ cos θ − Tyx sin2 θ.

ij

is a linear combination of the components of Tij.

Each component of T 0So we discover that it is not only possible to have a「vector product」like a× bwhich has three components that transform like a vector, but we can—artiﬁcially—also make another kind of「product」of two vectors Tij with nine componentsthat transform under a rotation by a complicated set of rules that we could ﬁgureout. Such an object which has two indices to describe it, instead of one, is calleda tensor. It is a tensor of the「second rank,」because you can play this gamewith three vectors too and get a tensor of the third rank—or with four, to get atensor of the fourth rank, and so on. A tensor of the ﬁrst rank is a vector.

The point of all this is that our electromagnetic quantity Fµν is also a tensorof the second rank, because it has two indices in it. It is, however, a tensor infour dimensions. It transforms in a special way which we will work out in amoment—it is just the way a product of vectors transforms. For Fµν it happensthat if you change the indices around, Fµν changes sign. That’s a special case—itis an antisymmetric tensor. So we say: the electric and magnetic ﬁelds are bothpart of an antisymmetric tensor of the second rank in four dimensions.

26-7

and by gets replaced by

a0

x

b0

y

= ax cos θ + ay sin θ,

= by cos θ − bx sin θ.

You’ve come a long way. Remember way back when we deﬁned what a velocitymeant? Now we are talking about「an antisymmetric tensor of the second rankin four dimensions.」

Now we have to ﬁnd the law of the transformation of Fµν. It isn’t at alldiﬃcult to do; it’s just laborious—the brains involved are nil, but the work isnot. What we want is the Lorentz transformation of ∇µAν − ∇νAµ. Since ∇µis just a special case of a vector, we will work with the general antisymmetricvector combination, which we can call Gµν:

Gµν = aµbν − aνbµ.

(26.20)(For our purposes, aµ will eventually be replaced by ∇µ and bµ will be replacedby the potential Aµ.) The components of aµ and bµ transform by the Lorentzformulas, which are

= at − vax√1 − v2 ,= ax − vat√1 − v2 ,= ay,= az,

a0

t

x

a0a0a0

y

z

= bt − vbx√1 − v2 ,= bx − vbt√1 − v2 ,= by,= bz.

(26.21)

b0

t

x

b0b0b0

y

z

Now let’s transform the components of Gµν. We start with Gtx:

G0

tx

t

(cid:18) at − vaxx − a0= a0tb0xb0√1 − v2= atbx − axbt.

=

(cid:19)

(cid:19)(cid:18) bx − vbt√1 − v2

(cid:18) ax − vat√1 − v2

(cid:19)(cid:18) bt − vbx√1 − v2

(cid:19)

−

But that is just Gtx; so we have the simple result

G0

tx

= Gtx.

We will do one more.

G0

ty

= at − vax√1 − v2 by − ay

bt − vbx√1 − v2

= (atby − aybt) − v(axby − aybx)

√1 − v2

.

So we get that

G0And, of course, in the same way,

ty

= Gty − vGxy√1 − v2

.

G0

tz

= Gtz − vGxz√1 − v2

.

It is clear how the rest will go. Let’s make a table of all six terms; only now wemay as well write them for Fµν:

F 0

tx

F 0

ty

F 0

tz

= Ftx,= Fty − vFxy√1 − v2 ,= Ftz − vFxz√1 − v2 ,= −F 0

νµ

µν

F 0

xy

F 0

yz

F 0

zx

= Fxy − vFty√1 − v2 ,

= Fyz,= Fzx − vFzt√1 − v2 .

Of course, we still have F 0

and F 0

µµ

= 0.

(26.22)

26-8

So we have the transformation of the electric and magnetic ﬁelds. All we haveto do is look at Table 26-1 to ﬁnd out what our grand notation in terms of Fµνmeans in terms of E and B. It’s just a matter of substitution. So that we cansee how it looks in the ordinary symbols, we’ll rewrite our transformation of theﬁeld components in Table 26-2.

The Lorentz transformation of the electric and magnetic ﬁelds (Note: c = 1)

Table 26-2

E0x = Exy = Ey − vBz√E01 − v2z = Ez + vByE01 − v2

√

B0x = Bxy = By + vEz√B01 − v2z = Bz − vEyB01 − v2

√

The equations in Table 26-2 tell us how E and B change if we go from oneinertial frame to another. If we know E and B in one system, we can ﬁnd whatthey are in another that moves by with the speed v.

We can write these equations in a form that is easier to remember if we noticethat since v is in the x-direction, all the terms with v are components of the crossproducts v × E and v × B. So we can rewrite the transformations as shown inTable 26-3.

An alternative form for the ﬁeld transformations (Note: c = 1)

Table 26-3

E0x = Exy = (E + v × B)y√E01 − v2z = (E + v × B)z√E01 − v2

B0x = Bxy = (B − v × E)y√B01 − v2z = (B − v × E)zB01 − v2

√

It is now easier to remember which components go where.

In fact, thetransformation can be written even more simply if we deﬁne the ﬁeld componentsalong x as the「parallel」components Ek and Bk (because they are parallel tothe relative velocity of S and S0), and the total transverse components—thevector sums of the y- and z-components—as the「perpendicular」componentsE⊥ and B⊥. Then we get the equations in Table 26-4. (We have also put backthe c’s, so it will be more convenient when we want to refer back later.)

Still another form for the Lorentz transformation of E and B

Table 26-4

E0k = Ek

p1 − v2/c2⊥ = (E + v × B)⊥E0

B0k = Bk

B0⊥ =

(cid:18)

(cid:19)B − v × Ep1 − v2/c2c2

⊥

The ﬁeld transformations give us another way of solving some problems wehave done before—for instance, for ﬁnding the ﬁelds of a moving point charge.We have worked out the ﬁelds before by diﬀerentiating the potentials. But wecould now do it by transforming the Coulomb ﬁeld. If we have a point charge atrest in the S-frame, then there is only the simple radial E-ﬁeld. In the S0-framewe will see a point charge moving with the velocity u, if the S0-frame moves by the26-9

Fig. 26-7. The coordinate frame S(cid:48) mov-

ing through a static electric ﬁeld.

S-frame with the speed v = −u. We will let you show that the transformationsof Tables 26-3 and 26-4 give the same electric and magnetic ﬁelds we got inSection 26-2.

The transformation of Table 26-2 gives us an interesting and simple answer forwhat we see if we move past any system of ﬁxed charges. For example, supposewe want to know the ﬁelds in our frame S0 if we are moving along between theplates of a condenser, as shown in Fig. 26-7. (It is, of course, the same thingif we say that a charged condenser is moving past us.) What do we see? Thetransformation is easy in this case because the B-ﬁeld in the original systemis zero. Suppose, ﬁrst, that our motion is perpendicular to E; then we will see

an E0 = E/p1 − v2/c2 which is still completely transverse. We will see, inaddition, a magnetic ﬁeld B0 = −v × E0/c2. (Thep1 − v2/c2 doesn’t appear in

the magnetic ﬁeld changed by the factor 1/p1 − v2/c2 (assuming it is transverse).

our formula for B0 because we wrote it in terms of E0 rather than E; but it’s thesame thing.) So when we move along perpendicular to a static electric ﬁeld, wesee a reduced E and an added transverse B. If our motion is not perpendicularto E, we break E into Ek and E⊥. The parallel part is unchanged, E0k = Ek,and the perpendicular component does as just described.Let’s take the opposite case, and imagine we are moving through a pure staticmagnetic ﬁeld. This time we would see an electric ﬁeld E0 equal to v × B0, andSo long as v is much less than c, we can neglect the change in the magnetic ﬁeld,and the main eﬀect is that an electric ﬁeld appears. As one example of this eﬀect,consider this once famous problem of determining the speed of an airplane. It’s nolonger famous, since radar can now be used to determine the air speed from groundreﬂections, but for many years it was very hard to ﬁnd the speed of an airplane inbad weather. You could not see the ground and you didn’t know which way wasup, and so on. Yet it was important to know how fast you were moving relative tothe earth. How can this be done without seeing the earth? Many who knew thetransformation formulas thought of the idea of using the fact that the airplanemoves in the magnetic ﬁeld of the earth. Suppose that an airplane is ﬂying wherethere is a magnetic ﬁeld more or less known. Let’s just take the simple casewhere the magnetic ﬁeld is vertical. If we were ﬂying through it with a horizontalvelocity v, then, according to our formula, we should see an electric ﬁeld whichis v × B, i.e., perpendicular to the line of motion. If we hang an insulated wireacross the airplane, this electric ﬁeld will induce charges on the ends of the wire.That is nothing new. From the point of view of someone on the ground, we aremoving a wire through a ﬁeld, and the v × B force causes charges to move tothe ends of the wire. The transformation equations just say the same thing ina diﬀerent way. (The fact that we can say the thing more than one way doesn’tmean that one way is better than another. We are getting so many diﬀerentmethods and tools that we can usually get the same result in 65 diﬀerent ways!)So to measure v, all we have to do is measure the voltage between the ends ofthe wire. We can’t do it with a voltmeter because the same ﬁelds will act on thewires in the voltmeter, but there are ways of measuring such ﬁelds. We talkedabout some of them when we discussed atmospheric electricity in Chapter 9. Soit should be possible to measure the speed of the airplane.

This important problem was, however, never solved this way. The reason isthat the electric ﬁeld that is developed is of the order of millivolts per meter.It is possible to measure such ﬁelds, but the trouble is that these ﬁelds are,unfortunately, not any diﬀerent from any other electric ﬁelds. The ﬁeld that isproduced by motion through the magnetic ﬁeld can’t be distinguished from someelectric ﬁeld that was already in the air from another cause, say from electrostaticcharges in the air, or on the clouds. We described in Chapter 9 that there are,typically, electric ﬁelds above the surface of the earth with strengths of about100 volts per meter. But they are quite irregular. So as the airplane ﬂies throughthe air, it sees ﬂuctuations of atmospheric electric ﬁelds which are enormous incomparison to the tiny ﬁelds produced by the v × B term, and it turns out forpractical reasons to be impossible to measure speeds of an airplane by its motionthrough the earth’s magnetic ﬁeld.

26-10

26-4 The equations of motion in relativistic notation*It doesn’t do much good to ﬁnd electric and magnetic ﬁelds from Maxwell’sequations unless we know what the ﬁelds do when we have them. You mayremember that the ﬁelds are required to ﬁnd the forces on charges, and thatthose forces determine the motion of the charge. So, of course, part of the theoryof electrodynamics is the relation between the motion of charges and the forces.

For a single charge in the ﬁelds E and B, the force is

F = q(E + v × B).

(26.23)This force is equal to the mass times the acceleration for low velocities, butthe correct law for any velocity is that the force is equal to dp/dt. Writingis

p = m0v/p1 − v2/c2, we ﬁnd that the relativistically correct equation of motion

= F = q(E + v × B).

(26.24)

(cid:18) m0vp1 − v2/c2

(cid:19)

ddt

is the energy m0c2/p1 − v2/c2. So we might think to replace the left-hand side

We would like now to discuss this equation from the point of view of relativ-ity. Since we have put our Maxwell equations in relativistic form, it would beinteresting to see what the equations of motion would look like in relativisticform. Let’s see whether we can rewrite the equation in a four-vector notation.We know that the momentum is part of a four-vector pµ whose time componentof Eq. (26.24) by dpµ/dt. Then we need only ﬁnd a fourth component to gowith F . This fourth component must equal the rate-of-change of the energy, orthe rate of doing work, which is F · v. We would then like to write the right-handside of Eq. (26.24) as a four-vector like (F · v, Fx, Fy, Fz). But this does notmake a four-vector.The time derivative of a four-vector is no longer a four-vector, because the d/dtrequires the choice of some special frame for measuring t. We got into that troublebefore when we tried to make v into a four-vector. Our ﬁrst guess was that thetime component would be cdt/dt = c. But the quantities

(cid:18)

(cid:19)

c,

dxdt

,

dydt

,

dzdt

= (c, v)

(26.25)

are not the components of a four-vector. We found that they could be made intothe four-vector

one by multiplying each component by 1/p1 − v2/c2. The「four-velocity」uµ isSo it appears that the trick is to multiply d/dt by 1/p1 − v2/c2, if we want the

cp1 − v2/c2 ,

vp1 − v2/c2

(26.26)

uµ =

(cid:18)

(cid:19)

.

derivatives to make a four-vector.Our second guess then is that

1p1 − v2/c2

(pµ)

ddt

(26.27)

should be a four-vector. But what is v? It is the velocity of the particle—not ofa coordinate frame! Then the quantity fµ deﬁned by

(cid:18)

fµ =

F · v

p1 − v2/c2 ,

Fp1 − v2/c2

(cid:19)

(26.28)

is the extension into four dimensions of a force—we can call it the「four-force.」Itis indeed a four-vector, and its space components are not the components of FThe question is—why is fµ a four-vector? It would be nice to get a little

but of F /p1 − v2/c2.understanding of that 1/p1 − v2/c2 factor. Since it has come up twice now, it

* In this section we will put back all of the c’s

26-11

is time to see why the d/dt can always be ﬁxed by the same factor. The answeris in the following: When we take the time derivative of some function x, wecompute the increment ∆x in a small interval ∆t in the variable t. But in anotherframe, the interval ∆t might correspond to a change in both t0 and x0, so if wevary only t0, the change in x will be diﬀerent. We have to ﬁnd a variable for ourdiﬀerentiation that is a measure of an「interval」in space-time, which will thenbe the same in all coordinate systems. When we take ∆x for that interval, it willbe the same for all coordinate frames. When a particle「moves」in four-space,there are the changes ∆t, ∆x, ∆y, ∆z. Can we make an invariant interval out ofthem? Well, they are the components of the four-vector xµ = (ct, x, y, z) so if wedeﬁne a quantity ∆s by

(∆s)2 = 1c2

∆xµ∆xµ = 1c2

(c2∆t2 − ∆x2 − ∆y2 − ∆z2)

(26.29)

can deﬁne a parameter s =R ds. And a derivative with respect to s, d/ds, is a

—which is a four-dimensional dot product—we then have a good four-scalar touse as a measure of a four-dimensional interval. From ∆s—or its limit ds—wenice four-dimensional operation, because it is invariant with respect to a Lorentztransformation.

It is easy to relate ds to dt for a moving particle. For a moving point particle,(26.30)

dy = vy dt,

and

dx = vx dt,

ds =q(dt2/c2)(c2 − v2

x − v2

y − v2

z

dz = vz dt,

) = dtp1 − v2/c2.

(26.31)

So the operator

1p1 − v2/c2

ddt

is an invariant operator. If we operate on any four-vector with it, we get anotherfour-vector. For instance, if we operate on (ct, x, y, z), we get the four-velocity uµ:

We see now why the factorp1 − v2/c2 ﬁxes things up.

= uµ.

dxµds

The invariant variable s is a useful physical quantity. It is called the「propertime」along the path of a particle, because ds is always an interval of timein a frame that is moving with the particle at any particular instant. (Then,∆x = ∆y = ∆z = 0, and ∆s = ∆t.) If you can imagine some「clock」whose ratedoesn’t depend on the acceleration, such a clock carried along with the particlewould show the time s.the neat form

We can now go back and write Newton’s law (as corrected by Einstein) in

where fµ is given in Eq. (26.28). Also, the momentum pµ can be written as

dpµds

= fµ,

(26.32)

pµ = m0uµ = m0

dxµds

,

(26.33)

where the coordinates xµ = (ct, x, y, z) now describe the trajectory of the particle.Finally, the four-dimensional notation gives us this very simple form of theequations of motion:

d2xµds2 ,

fµ = m0

(26.34)which is reminiscent of F = ma. It is important to notice that Eq. (26.34) is notthe same as F = ma, because the four-vector formula Eq. (26.34) has in it therelativistic mechanics which are diﬀerent from Newton’s law for high velocities.It is unlike the case of Maxwell’s equations, where we were able to rewrite the26-12

(cid:20)

= q

equations in the relativistic form without any change in the meaning at all—butwith just a change of notation.Now let’s return to Eq. (26.24) and see how we can write the right-hand side in

four-vector notation. The three components—when divided byp1 − v2/c2—arethe components of fµ, sop1 − v2/c2fx = q(E + v × B)xNow we must put all quantities in their relativistic notation. First, c/p1 − v2/c2and vy/p1 − v2/c2 and vz/p1 − v2/c2 are the t-, y-, and z-components of the

p1 − v2/c2 −

p1 − v2/c2

Exp1 − v2/c2

four-velocity uµ. And the components of E and B are components of the second-rank tensor of the ﬁelds Fµν. Looking back in Table 26-1 for the componentsof Fµν that correspond to Ex, Bz, and By, we get*

+

vyBz

vzBy

. (26.35)

(cid:21)

fx = q(utFxt − uyFxy − uzFxz),

fx = q(utFxt − uxFxx − uyFxy − uzFxz).

which begins to look interesting. Every term has the subscript x, which isreasonable, since we’re ﬁnding an x-component. Then all the others appear inpairs: tt, yy, zz—except that the xx-term is missing. So we just stick it in, andwrite(26.36)We haven’t changed anything because Fµν is antisymmetric, and Fxx is zero.The reason for wanting to put in the xx-term is so that we can write Eq. (26.36)in the short-hand form(26.37)This equation is the same as Eq. (26.36) if we make the rule that whenever anysubscript occurs twice (as ν does here), you automatically sum over terms in thesame way as for the scalar product, using the same convention for the signs.You can easily believe that (26.37) works equally well for µ = y or µ = z, butwhat about µ = t? Let’s see, for fun, what it says:

fµ = quνFµν.

ft = q(utFtt − uxFtx − uyFty − uzFtz).

Now we have to translate back to E’s and B’s. We get

(cid:18)

0 +

vxp1 − v2/c2 Ex +

ft = q

or

(cid:19)

,

(26.38)

vzp1 − v2/c2 Ez

ft =

qv · E

vyp1 − v2/c2 Ey +p1 − v2/c2 .p1 − v2/c2= q(E + v × B) · v

.

F · v

p1 − v2/c2

But from Eq. (26.28), ft is supposed to be

This is the same thing as Eq. (26.38), since (v × B) · v is zero. So everythingcomes out all right.

Summarizing, our equation of motion can be written in the elegant form

m0

d2xµds2

= fµ = quνFµν.

(26.39)

Although it is nice to see that the equations can be written that way, this form isnot particularly useful. It’s usually more convenient to solve for particle motionsby using the original equations (26.24), and that’s what we will usually do.

* When we put the c’s back in Table 26-1, all components of Fµν, corresponding to

components of E are multiplied by 1/c.

26-13

27

Field Energy and Field Momentum

