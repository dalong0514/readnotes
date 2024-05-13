Work and Potential Energy (A)

13-1 Energy of a falling body In Chapter 4 we discussed the conservation of energy. In that discussion, we did not use Newton’s laws, but it is, of course, of great interest to see how it comes about that energy is in fact conserved in accordance with these laws. For clarity we shall start with the simplest possible example, and then develop harder and harder examples.

The simplest example of the conservation of energy is a vertically falling object, one that moves only in a vertical direction. An object which changes its height under the inﬂuence of gravity alone has a kinetic energy T (or K.E.) due to its motion during the fall, and a potential energy mgh, abbreviated U (or P.E.), whose sum is constant: 2 mv2 1 K.E.

+ mgh P.E.

= const,

or

T + U = const.

(13.1) Now we would like to show that this statement is true. What do we mean, show it is true? From Newton’s Second Law we can easily tell how the object moves, and it is easy to ﬁnd out how the velocity varies with time, namely, that it increases proportionally with the time, and that the height varies as the square of the time. So if we measure the height from a zero point where the object is stationary, it is no miracle that the height turns out to be equal to the square of the velocity times a number of constants. However, let us look at it a little more closely.

Let us ﬁnd out directly from Newton’s Second Law how the kinetic energy should change, by taking the derivative of the kinetic energy with respect to time 2 mv2 with respect to time, and then using Newton’s laws. When we diﬀerentiate 1 we obtain (13.2)

( 1 2 mv2) = 1

2 m2v

dT dt

= d dt

dv dt

= mv

dv dt

,

13-1

since m is assumed constant. But from Newton’s Second Law, m(dv/dt) = F, so that

dT /dt = F v.

(13.3) In general, it will come out to be F · v, but in our one-dimensional case let us leave it as the force times the velocity. Now in our simple example the force is constant, equal to −mg, a vertical force (the minus sign means that it acts downward), and the velocity, of course, is the rate of change of the vertical position, or height h, with time. Thus the rate of change of the kinetic energy is −mg(dh/dt), which quantity, miracle of miracles, is minus the rate of change of something else! It is minus the time rate of change of mgh! Therefore, as time goes on, the changes in kinetic energy and in the quantity mgh are equal and opposite, so that the sum of the two quantities remains constant. Q.E.D. We have shown, from Newton’s second law of motion, that energy is con- served for constant forces when we add the potential energy mgh to the kinetic energy 1 2 mv2. Now let us look into this further and see whether it can be gener- alized, and thus advance our understanding. Does it work only for a freely falling body, or is it more general? We expect from our discussion of the conservation of energy that it would work for an object moving from one point to another in some kind of frictionless curve, under the inﬂuence of gravity (Fig. 13-1). If the object reaches a certain height h from the original height H, then the same formula should again be right, even though the velocity is now in some direction other than the vertical. We would like to understand why the law is still correct. Let us follow the same analysis, ﬁnding the time rate of change of the kinetic energy. This will again be mv(dv/dt), but m(dv/dt) is the rate of change of the magnitude of the momentum, i.e., the force in the direction of motion—the

Fig. 13-1. An object moving on a frictionless curve under the inﬂuence

of gravity.

13-2

tangential force Ft. Thus

dT dt

= mv

dv dt

= Ftv.

Now the speed is the rate of change of distance along the curve, ds/dt, and the tangential force Ft is not −mg but is weaker by the ratio of the vertical distance dh to the distance ds along the path. In other words,

so that

Ft

ds dt

= −mg

Ft = −mg sin θ = −mg

dh ds

,

(cid:18) dh

(cid:19)(cid:18) ds

(cid:19)

ds

dt

= −mg

dh dt

,

since the ds’s cancel. Thus we get −mg(dh/dt), which is equal to the rate of change of −mgh, as before. In order to understand exactly how the conservation of energy works in general in mechanics, we shall now discuss a number of concepts which will help us to analyze it.

First, we discuss the rate of change of kinetic energy in general in three

dimensions. The kinetic energy in three dimensions is

T = 1

2 m(v2

x

+ v2

y

+ v2

z

).

(cid:18)

(cid:19)

.

When we diﬀerentiate this with respect to time, we get three terrifying terms:

= m

dT dt

vx

dvx dt

+ vy

dvy dt

+ vz

dvz dt

(13.4)

But m(dvx/dt) is the force Fx acting on the object in the x-direction. Thus the right side of Eq. (13.4) is Fxvx + Fyvy + Fzvz. We recall our vector analysis and recognize this as F · v; therefore

dT /dt = F · v.

(13.5) This result can be derived more quickly as follows: if a and b are two vectors, both of which may depend upon the time, the derivative of a · b is, in general, (13.6)

d(a · b)/dt = a · (db/dt) + (da/dt) · b.

13-3

We then use this in the form a = b = v:

d( 1

2 mv2) dt

= d( 1

2 mv · v)

dt

= m

dv dt

· v = F · v = F · ds dt

.

(13.7)

Because the concepts of kinetic energy, and energy in general, are so important, various names have been given to the important terms in equations such as these. 2 mv2 is, as we know, called kinetic energy. F · v is called power: the force acting 1 on an object times the velocity of the object (vector「dot」product) is the power being delivered to the object by that force. We thus have a marvelous theorem: the rate of change of kinetic energy of an object is equal to the power expended by the forces acting on it. However, to study the conservation of energy, we want to analyze this still more closely. Let us evaluate the change in kinetic energy in a very short time dt. If we multiply both sides of Eq. (13.7) by dt, we ﬁnd that the diﬀerential change in the kinetic energy is the force「dot」the diﬀerential distance moved:

If we now integrate, we get

∆T =

dT = F · ds.

Z 2

1

F · ds.

(13.8)

(13.9)

What does this mean? It means that if an object is moving in any way under the inﬂuence of a force, moving in some kind of curved path, then the change in K.E. when it goes from one point to another along the curve is equal to the integral of the component of the force along the curve times the diﬀerential displacement ds, the integral being carried out from one point to the other. This integral also has a name; it is called the work done by the force on the object. We see immediately that power equals work done per second. We also see that it is only a component of force in the direction of motion that contributes to the work done. In our simple example the forces were only vertical, and had only a single component, say Fz, equal to −mg. No matter how the object moves in those circumstances, falling in a parabola for example, F · s, which can be written as Fx dx + Fy dy + Fz dz, has nothing left of it but Fz dz = −mg dz, because the other components of force are zero. Therefore, in our simple case,

F · ds =

−mg dz = −mg(z2 − z1),

(13.10)

Z 2

1

Z z2

z1

13-4

so again we ﬁnd that it is only the vertical height from which the object falls that counts toward the potential energy. A word about units. Since forces are measured in newtons, and we multiply by a distance in order to obtain work, work is measured in newton ·meters (N·m), but people do not like to say newton-meters, they prefer to say joules (J). A newton-meter is called a joule; work is measured in joules. Power, then, is joules per second, and that is also called a watt (W). If we multiply watts by time, the result is the work done. The work done by the electrical company in our houses, technically, is equal to the watts times the time. That is where we get things like kilowatt hours, 1000 watts times 3600 seconds, or 3.6 × 106 joules. Now we take another example of the law of conservation of energy. Consider an object which initially has kinetic energy and is moving very fast, and which slides against the ﬂoor with friction. It stops. At the start the kinetic energy is not zero, but at the end it is zero; there is work done by the forces, because whenever there is friction there is always a component of force in a direction opposite to that of the motion, and so energy is steadily lost. But now let us take a mass on the end of a pivot swinging in a vertical plane in a gravitational ﬁeld with no friction. What happens here is diﬀerent, because when the mass is going up the force is downward, and when it is coming down, the force is also downward. Thus F · ds has one sign going up and another sign coming down. At each corresponding point of the downward and upward paths the values of F · ds are exactly equal in size but of opposite sign, so the net result of the integral will be zero for this case. Thus the kinetic energy with which the mass comes back to the bottom is the same as it had when it left; that is the principle of the conservation of energy. (Note that when there are friction forces the conservation of energy seems at ﬁrst sight to be invalid. We have to ﬁnd another form of energy. It turns out, in fact, that heat is generated in an object when it rubs another with friction, but at the moment we supposedly do not know that.)

13-2 Work done by gravity The next problem to be discussed is much more diﬃcult than the above; it has to do with the case when the forces are not constant, or simply vertical, as they were in the cases we have worked out. We want to consider a planet, for example, moving around the sun, or a satellite in the space around the earth.

We shall ﬁrst consider the motion of an object which starts at some point 1 and falls, say, directly toward the sun or toward the earth (Fig. 13-2). Will there

13-5

Fig. 13-2. A small mass m falls under the inﬂuence of gravity toward

a large mass M.

be a law of conservation of energy in these circumstances? The only diﬀerence is that in this case, the force is changing as we go along, it is not just a constant. As we know, the force is −GM/r2 times the mass m, where m is the mass that moves. Now certainly when a body falls toward the earth, the kinetic energy increases as the distance fallen increases, just as it does when we do not worry about the variation of force with height. The question is whether it is possible to ﬁnd another formula for potential energy diﬀerent from mgh, a diﬀerent function of distance away from the earth, so that conservation of energy will still be true. This one-dimensional case is easy to treat because we know that the change in the kinetic energy is equal to the integral, from one end of the motion to the other, of −GM m/r2 times the displacement dr:

T2 − T1 = −

GM m

dr r2 .

(13.11)

There are no cosines needed for this case because the force and the displacement are in the same direction. It is easy to integrate dr/r2; the result is −1/r, so Eq. (13.11) becomes

T2 − T1 = +GM m

(13.12)

Thus we have a diﬀerent formula for potential energy. Equation (13.12) tells us 2 mv2 − GM m/r) calculated at point 1, at point 2, or at any that the quantity ( 1 other place, has a constant value. We now have the formula for the potential energy in a gravitational ﬁeld for vertical motion. Now we have an interesting problem. Can we make perpetual motion in a gravitational ﬁeld? The gravitational ﬁeld varies; in diﬀerent places it is in diﬀerent directions and has diﬀerent strengths. Could we do something like this, using a ﬁxed, frictionless track: start at some point and lift an object out to some other point, then move it around an arc to a third point, then lower it a certain distance, then move it in at a certain slope and pull it out some other way, so that when we bring it back to the starting point, a certain amount of work

13-6

Z 2

1

(cid:18) 1

r2

(cid:19)

.

− 1

r1

has been done by the gravitational force, and the kinetic energy of the object is increased? Can we design the curve so that it comes back moving a little bit faster than it did before, so that it goes around and around and around, and gives us perpetual motion? Since perpetual motion is impossible, we ought to ﬁnd out that this is also impossible. We ought to discover the following proposition: since there is no friction the object should come back with neither higher nor lower velocity—it should be able to keep going around and around any closed path. Stated in another way, the total work done in going around a complete cycle should be zero for gravity forces, because if it is not zero we can get energy out by going around. (If the work turns out to be less than zero, so that we get less speed when we go around one way, then we merely go around the other way, because the forces, of course, depend only upon the position, not upon the direction; if one way is plus, the other way would be minus, so unless it is zero we will get perpetual motion by going around either way.)

Fig. 13-3. A closed path in a gravitational ﬁeld.

Is the work really zero? Let us try to demonstrate that it is. First we shall explain more or less why it is zero, and then we shall examine it a little better mathematically. Suppose that we use a simple path such as that shown in Fig. 13-3, in which a small mass is carried from point 1 to point 2, and then is made to go around a circle to 3, back to 4, then to 5, 6, 7, and 8, and ﬁnally back to 1. All of the lines are either purely radial or circular, with M as the center. How much work is done in carrying m around this path? Between points 1 and 2, it is GM m times the diﬀerence of 1/r between these two points:

W12 =

F · ds =

−GM m

dr r2

= GM m

From 2 to 3 the force is exactly at right angles to the curve, so that W23 ≡ 0. The work from 3 to 4 is

Z 2

1

Z 2

1

Z 4

3

W34 =

F · ds = GM m

13-7

(cid:19)

.

− 1

r1

(cid:18) 1 (cid:19)

r2

.

(cid:18) 1

r4

− 1

r3

In the same fashion, we ﬁnd that W45 = 0, W56 = GM m(1/r6 − 1/r5), W67 = 0, W78 = GM m(1/r8 − 1/r7), and W81 = 0. Thus + 1 r6

W = GM m

+ 1 r4

− 1

r7

− 1

r1

− 1

r3

(cid:18) 1

− 1

r5

+ 1 r8

(cid:19)

.

r2

But we note that r2 = r3, r4 = r5, r6 = r7, and r8 = r1. Therefore W = 0.

Fig. 13-4. A「smooth」closed path, showing a magniﬁed segment of it approximated by a series of radial and circumferential steps, and an enlarged view of one step.

Of course we may wonder whether this is too trivial a curve. What if we use a real curve? Let us try it on a real curve. First of all, we might like to assert that a real curve could always be imitated suﬃciently well by a series of sawtooth jiggles like those of Fig. 13-4, and that therefore, etc., Q.E.D., but without a little analysis, it is not obvious at ﬁrst that the work done going around even a small triangle is zero. Let us magnify one of the triangles, as shown in Fig. 13-4. Is the work done in going from a to b and b to c on a triangle the same as the work done in going directly from a to c? Suppose that the force is acting in a certain direction; let us take the triangle such that the side bc is in this direction, just as an example. We also suppose that the triangle is so small that the force is essentially constant over the entire triangle. What is the work done in going from a to c? It is

Z c

Wac =

F · ds = F s cos θ,

since the force is constant. Now let us calculate the work done in going around the other two sides of the triangle. On the vertical side ab the force is perpendicular

a

13-8

to ds, so that here the work is zero. On the horizontal side bc,

Z c

Wbc =

F · ds = F x.

b

Thus we see that the work done in going along the sides of a small triangle is the same as that done going on a slant, because s cos θ is equal to x. We have proved previously that the answer is zero for any path composed of a series of notches like those of Fig. 13-3, and also that we do the same work if we cut across the corners instead of going along the notches (so long as the notches are ﬁne enough, and we can always make them very ﬁne); therefore, the work done in going around any path in a gravitational ﬁeld is zero. This is a very remarkable result. It tells us something we did not previously know about planetary motion. It tells us that when a planet moves around the sun (without any other objects around, no other forces) it moves in such a manner that the square of the speed at any point minus some constants divided by the radius at that point is always the same at every point on the orbit. For example, the closer the planet is to the sun, the faster it is going, but by how much? By the following amount: if instead of letting the planet go around the sun, we were to change the direction (but not the magnitude) of its velocity and make it move radially, and then we let it fall from some special radius to the radius of interest, the new speed would be the same as the speed it had in the actual orbit, because this is just another example of a complicated path. So long as we come back to the same distance, the kinetic energy will be the same. So, whether the motion is the real, undisturbed one, or is changed in direction by channels, by frictionless constraints, the kinetic energy with which the planet arrives at a point will be the same.

Thus, when we make a numerical analysis of the motion of the planet in its orbit, as we did earlier, we can check whether or not we are making appreciable errors by calculating this constant quantity, the energy, at every step, and it should not change. For the orbit of Table 9-2 the energy does change,* it changes by some 1.5 percent from the beginning to the end. Why? Either because for the numerical method we use ﬁnite intervals, or else because we made a slight mistake somewhere in arithmetic.

Let us consider the energy in another case: the problem of a mass on a spring. When we displace the mass from its balanced position, the restoring force is

* The energy per unit mass is 1

2 (v2

x + v2

y) − 1/r in the units of Table 9-2.

13-9

Z x

0

Z x

0

proportional to the displacement. In those circumstances, can we work out a law for conservation of energy? Yes, because the work done by such a force is

W =

F dx =

−kx dx = − 1

2 kx2.

(13.13)

Therefore, for a mass on a spring we have that the kinetic energy of the oscillating mass plus 1 2 kx2 is a constant. Let us see how this works. We pull the mass down; it is standing still and so its speed is zero. But x is not zero, x is at its maximum, so there is some energy, the potential energy, of course. Now we release the mass and things begin to happen (the details not to be discussed), but at any instant the kinetic plus potential energy must be a constant. For example, after the mass is on its way past the original equilibrium point, the position x equals zero, but that is when it has its biggest v2, and as it gets more x2 it gets less v2, and so on. So the balance of x2 and v2 is maintained as the mass goes up and down. Thus we have another rule now, that the potential energy for a spring is 1 2 kx2, if the force is −kx.

13-3 Summation of energy Now we go on to the more general consideration of what happens when there are large numbers of objects. Suppose we have the complicated problem of many objects, which we label i = 1, 2, 3, . . . , all exerting gravitational pulls on each other. What happens then? We shall prove that if we add the kinetic energies of all the particles, and add to this the sum, over all pairs of particles, of their mutual gravitational potential energy, −GM m/rij, the total is a constant:

X

i

2 miv2 1

i

+ X

(pairs ij)

− Gmimj

rij

= const.

(13.14)

How do we prove it? We diﬀerentiate each side with respect to time and get zero. When we diﬀerentiate 1 , we ﬁnd derivatives of the velocity that are the forces, just as in Eq. (13.5). We replace these forces by the law of force that we know from Newton’s law of gravity and then we notice that what is left is

2 miv2

i

minus the time derivative of X

pairs

− Gmimj

rij

.

13-10

The time derivative of the potential energy is

But

so that

X

i

d dt

2 miv2 1

i

· vi

i

dvi mi dt F i · vi

=X =X X =X = X

j

i

d dt

i

rij

pairs

r3 ij

· vi.

+ Gmimj

− Gmimj

− Gmimjrij

! !(cid:18) drij (cid:19) X rij =q(xi − xj)2 + (yi − yj)2 + (zi − zj)2, (cid:19) (cid:19) (cid:19)(cid:21)

(cid:18) dxi (cid:18) dyi (cid:18) dzi

+ 2(yi − yj )

= 1 2rij

2(xi − xj)

drij dt

(cid:20)

r2 ij

pairs

dt

dt

dt

+ 2(zi − zj )

− dxj dt − dyj dt − dzj dt

.

= rij · vi − vj = rij · vi rij

rij + rji · vj rji

dt

,

The time derivative of the kinetic energy is

(13.15)

X

since rij = −rji, while rij = rji. Thus

(cid:20) Gmimjrij {P Now we must note carefully whatP } and P

= X

− Gmimj

d dt

r3 ij

pairs

pairs

rij

· vi + Gmjmirji

· vj

(13.16)

.

r3 ji

mean. In Eq. (13.15),P {P

} means that i takes on all values i = 1, 2, 3, . . . in turn, and for each value of i,

pairs

j

j

i

i

(cid:21)

13-11

pairs

In Eq. (13.16), on the other hand, P

the index j takes on all values except i. Thus if i = 3, j takes on the values 1, 2, 4, . . . means that given values of i and j occur only once. Thus the particle pair 1 and 3 contributes only one term to the sum. To keep track of this, we might agree to let i range over all values 1, 2, 3, . . . , and for each i let j range only over values greater than i. Thus if i = 3, j could only have values 4, 5, 6, . . . But we notice that for each i, j value there are two contributions to the sum, one involving vi, and the other vj, and that these terms have the same appearance as those of Eq. (13.15), where all values of i and j (except i = j) are included in the sum. Therefore, by matching the terms one by one, we see that Eqs. (13.16) and (13.15) are precisely the same, but of opposite sign, so that the time derivative of the kinetic plus potential energy is indeed zero. Thus we see that, for many objects, the kinetic energy is the sum of the contributions from each individual object, and that the potential energy is also simple, it being also just a sum of contributions, the energies between all the pairs. We can understand why it should be the energy of every pair this way: Suppose that we want to ﬁnd the total amount of work that must be done to bring the objects to certain distances from each other. We may do this in several steps, bringing them in from inﬁnity where there is no force, one by one. First we bring in number one, which requires no work, since no other objects are yet present to exert force on it. Next we bring in number two, which does take some work, namely W12 = −Gm1m2/r12. Now, and this is an important point, suppose we bring in the next object to position three. At any moment the force on number 3 can be written as the sum of two forces—the force exerted by number 1 and that exerted by number 2. Therefore the work done is the sum of the works done by each, because if F 3 can be resolved into the sum of two forces,

then the work isZ

Z

F 3 · ds =

F 3 = F 13 + F 23,

Z

F 13 · ds +

F 23 · ds = W13 + W23.

That is, the work done is the sum of the work done against the ﬁrst force and the second force, as if each acted independently. Proceeding in this way, we see that the total work required to assemble the given conﬁguration of objects is precisely the value given in Eq. (13.14) as the potential energy. It is because gravity obeys

13-12

the principle of superposition of forces that we can write the potential energy as a sum over each pair of particles.

13-4 Gravitational ﬁeld of large objects Now we shall calculate the ﬁelds which are met in a few physical circumstances involving distributions of mass. We have not so far considered distributions of mass, only particles, so it is interesting to calculate the forces when they are produced by more than just one particle. First we shall ﬁnd the gravitational force on a mass that is produced by a plane sheet of material, inﬁnite in extent. The force on a unit mass at a given point P, produced by this sheet of material (Fig. 13-5), will of course be directed toward the sheet. Let the distance of the point from the sheet be a, and let the amount of mass per unit area of this huge sheet be µ. We shall suppose µ to be constant; it is a uniform sheet of material. Now, what small ﬁeld dC is produced by the mass dm lying between ρ and ρ+ dρ from the point O of the sheet nearest point P? Answer: dC = −G(dm r/r3). But this ﬁeld is directed along r, and we know that only the x-component of it will remain when we add all the little vector dC’s to produce C. The x-component of dC is

= −G

dm a r3 .

dCx = −G

dm rx

r3

Now all masses dm which are at the same distance r from P will yield the same dCx, so we may at once write for dm the total mass in the ring between ρ and ρ + dρ, namely dm = µ2πρ dρ (2πρ dρ is the area of a ring of radius ρ and width dρ, if dρ (cid:28) ρ). Thus

dCx = −Gµ2πρ

dρ a r3 .

Fig. 13-5. The gravitational ﬁeld C at a mass point produced by an

inﬁnite plane sheet of matter.

13-13

Then, since r2 = ρ2 + a2, ρ dρ = r dr. Therefore, − 1 ∞

Cx = −2πGµa

= −2πGµa

(cid:16)1

a

Z ∞

a

dr r2

(cid:17) = −2πGµ.

(13.17)

Thus the force is independent of distance a! Why? Have we made a mistake? One might think that the farther away we go, the weaker the force would be. But no! If we are close, most of the matter is pulling at an unfavorable angle; if we are far away, more of the matter is situated more favorably to exert a pull toward the plane. At any distance, the matter which is most eﬀective lies in a certain cone. When we are farther away the force is smaller by the inverse square, but in the same cone, in the same angle, there is much more matter, larger by just the square of the distance! This analysis can be made rigorous by just noticing that the diﬀerential contribution in any given cone is in fact independent of the distance, because of the reciprocal variation of the strength of the force from a given mass, and the amount of mass included in the cone, with changing distance. The force is not really constant of course, because when we go on the other side of the sheet it is reversed in sign.

We have also, in eﬀect, solved an electrical problem: if we have an electrically charged plate, with an amount σ of charge per unit area, then the electric ﬁeld at a point outside the sheet is equal to σ/20, and is in the outward direction if the sheet is positively charged, and inward if the sheet is negatively charged. To prove this, we merely note that −G, for gravity, plays the same role as 1/4π0 for electricity. Now suppose that we have two plates, with a positive charge +σ on one and a negative charge −σ on another at a distance D from the ﬁrst. What is the ﬁeld? Outside the two plates it is zero. Why? Because one attracts and the other repels, the force being independent of distance, so that the two balance out! Also, the ﬁeld between the two plates is clearly twice as great as that from one plate, namely E = σ/0, and is directed from the positive plate to the negative one. Now we come to a most interesting and important problem, whose solution we have been assuming all the time, namely, that the force produced by the earth at a point on the surface or outside it is the same as if all the mass of the earth were located at its center. The validity of this assumption is not obvious, because when we are close, some of the mass is very close to us, and some is farther away, and so on. When we add the eﬀects all together, it seems a miracle that the net force is exactly the same as we would get if we put all the mass in the middle!

13-14

Fig. 13-6. A thin spherical shell of mass or charge.

We now demonstrate the correctness of this miracle.

In order to do so, however, we shall consider a thin uniform hollow shell instead of the whole earth. Let the total mass of the shell be m, and let us calculate the potential energy of a particle of mass m0 a distance R away from the center of the sphere (Fig. 13-6) and show that the potential energy is the same as it would be if the mass m were a point at the center. (The potential energy is easier to work with than is the ﬁeld because we do not have to worry about angles, we merely add the potential energies of all the pieces of mass.) If we call x the distance of a certain plane section from the center, then all the mass that is in a slice dx is at the same distance r from P, and the potential energy due to this ring is −Gm0 dm/r. How much mass is in the small slice dx? An amount

dm = 2πyµ ds = 2πyµ dx sin θ

= 2πyµ dx a

y

= 2πaµ dx,

where µ = m/4πa2 is the surface density of mass on the spherical shell. (It is a general rule that the area of a zone of a sphere is proportional to its axial width.) Therefore the potential energy due to dm is

But we see that

Thus

or

dW = − Gm0 dm

r

= − Gm02πaµ dx

r

.

r2 = y2 + (R − x)2 = y2 + x2 + R2 − 2Rx

= a2 + R2 − 2Rx.

2r dr = −2R dx

dx r

= − dr R

.

13-15

Therefore,

and so

dW = Gm02πaµ dr

R

W = Gm02πaµ = − Gm02πaµ = − Gm0m

R

.

R

,

R

Z R−a 2a = − Gm0(4πa2µ)

R+a

dr

R

(13.18)

Thus, for a thin spherical shell, the potential energy of a mass m0, external to the shell, is the same as though the mass of the shell were concentrated at its center. The earth can be imagined as a series of spherical shells, each one of which contributes an energy which depends only on its mass and the distance from its center to the particle; adding them all together we get the total mass, and therefore the earth acts as though all the material were at the center! But notice what happens if our point is on the inside of the shell. Making the same calculation, but with P on the inside, we still get the diﬀerence of the two r’s, but now in the form a− R − (a + R) = −2R, or minus twice the distance from the center. In other words, W comes out to be W = −Gm0m/a, which is independent of R and independent of position, i.e., the same energy no matter where we are inside. Therefore no force; no work is done when we move about inside. If the potential energy is the same no matter where an object is placed inside the sphere, there can be no force on it. So there is no force inside, there is only a force outside, and the force outside is the same as though the mass were all at the center.

13-16

14

