# 0701


7-1 Methods for ﬁnding the

electrostatic ﬁeld

7-2 Two-dimensional ﬁelds; functions

of the complex variable

7-3 Plasma oscillations7-4 Colloidal particles in an

electrolyte

7-5 The electrostatic ﬁeld of a grid

7

The Electric Field in Various Circumstances(Continued)

7-1 Methods for ﬁnding the electrostatic ﬁeldThis

chapter is a continuation of our consideration of the characteristics ofelectric ﬁelds in various particular situations. We shall ﬁrst describe some of themore elaborate methods for solving problems with conductors. It is not expectedthat these more advanced methods can be mastered at this time. Yet it may beof interest to have some idea about the kinds of problems that can be solved,using techniques that may be learned in more advanced courses. Then we takeup two examples in which the charge distribution is neither ﬁxed nor is carriedby a conductor, but instead is determined by some other law of physics.

As we found in Chapter 6, the problem of the electrostatic ﬁeld is fundamen-tally simple when the distribution of charges is speciﬁed; it requires only theevaluation of an integral. When there are conductors present, however, compli-cations arise because the charge distribution on the conductors is not initiallyknown; the charge must distribute itself on the surface of the conductor in sucha way that the conductor is an equipotential. The solution of such problems isneither direct nor simple.

We have looked at an indirect method of solving such problems, in which weﬁnd the equipotentials for some speciﬁed charge distribution and replace one ofthem by a conducting surface. In this way we can build up a catalog of specialsolutions for conductors in the shapes of spheres, planes, etc. The use of images,described in Chapter 6, is an example of an indirect method. We shall describeanother in this chapter.

If the problem to be solved does not belong to the class of problems for whichwe can construct solutions by the indirect method, we are forced to solve theproblem by a more direct method. The mathematical problem of the directmethod is the solution of Laplace’s equation,∇2φ = 0,

(7.1)subject to the condition that φ is a suitable constant on certain boundaries—thesurfaces of the conductors. Problems which involve the solution of a diﬀerentialﬁeld equation subject to certain boundary conditions are called boundary-valueproblems. They have been the object of considerable mathematical study. In thecase of conductors having complicated shapes, there are no general analyticalmethods. Even such a simple problem as that of a charged cylindrical metal canclosed at both ends—a beer can—presents formidable mathematical diﬃculties.It can be solved only approximately, using numerical methods. The only generalmethods of solution are numerical.There are a few problems for which Eq. (7.1) can be solved directly. Forexample, the problem of a charged conductor having the shape of an ellipsoidof revolution can be solved exactly in terms of known special functions. Thesolution for a thin disc can be obtained by letting the ellipsoid become inﬁnitelyoblate. In a similar manner, the solution for a needle can be obtained by lettingthe ellipsoid become inﬁnitely prolate. However, it must be stressed that theonly direct methods of general applicability are the numerical techniques.

Boundary-value problems can also be solved by measurements of a physicalanalog. Laplace’s equation arises in many diﬀerent physical situations: in steady-state heat ﬂow, in irrotational ﬂuid ﬂow, in current ﬂow in an extended medium,7-1

and in the deﬂection of an elastic membrane. It is frequently possible to set upa physical model which is analogous to an electrical problem which we wish tosolve. By the measurement of a suitable analogous quantity on the model, thesolution to the problem of interest can be determined. An example of the analogtechnique is the use of the electrolytic tank for the solution of two-dimensionalproblems in electrostatics. This works because the diﬀerential equation for thepotential in a uniform conducting medium is the same as it is for a vacuum.

There are many physical situations in which the variations of the physicalﬁelds in one direction are zero, or can be neglected in comparison with thevariations in the other two directions. Such problems are called two-dimensional;the ﬁeld depends on two coordinates only. For example, if we place a long chargedwire along the z-axis, then for points not too far from the wire the electric ﬁelddepends on x and y, but not on z; the problem is two-dimensional. Since in atwo-dimensional problem ∂φ/∂z = 0, the equation for φ in free space is

∂2φ∂x2

+ ∂2φ∂y2

= 0.

(7.2)

Because the two-dimensional equation is comparatively simple, there is a widerange of conditions under which it can be solved analytically. There is, in fact,a very powerful indirect mathematical technique which depends on a theoremfrom the mathematics of functions of a complex variable, and which we will nowdescribe.

7-2 Two-dimensional ﬁelds; functions of the complex variableThe complex variable z is deﬁned as

z = x + iy.

(Do not confuse z with the z-coordinate, which we ignore in the following discussionbecause we assume there is no z-dependence of the ﬁelds.) Every point in x and ythen corresponds to a complex number z. We can use z as a single (complex)variable, and with it write the usual kinds of mathematical functions F(z). Forexample,

F(z) = z2,

F(z) = 1/z3,

F(z) = z ln z,

or

or

and

and so forth.

Given any particular F(z) we can substitute z = x+iy, and we have a function

of x and y—with real and imaginary parts. For example,z2 = (x + iy)2 = x2 − y2 + 2ixy.

(7.3)Any function F(z) can be written as a sum of a pure real part and a pure

imaginary part, each part a function of x and y:

F(z) = U(x, y) + iV (x, y),

(7.4)where U(x, y) and V (x, y) are real functions. Thus from any complex function F(z)two new functions U(x, y) and V (x, y) can be derived. For example, F(z) = z2gives us the two functions(7.5)

U(x, y) = x2 − y2,

V (x, y) = 2xy.

(7.6)

Now we come to a miraculous mathematical theorem which is so delightfulthat we shall leave a proof of it for one of your courses in mathematics. (We7-2

should not reveal all the mysteries of mathematics, or that subject matter wouldbecome too dull.) It is this. For any「ordinary function」(mathematicians willdeﬁne it better) the functions U and V automatically satisfy the relations

∂U∂x

∂V∂x

,

= ∂V∂y= − ∂U∂y

.

(7.7)

(7.8)

It follows immediately that each of the functions U and V satisfy Laplace’sequation:

∂2U∂x2∂2V∂x2

+ ∂2U∂y2+ ∂2V∂y2

= 0,

= 0,

(7.9)

(7.10)

These equations are clearly true for the functions of (7.5) and (7.6).

Thus, starting with any ordinary function, we can arrive at two functionsU(x, y) and V (x, y), which are both solutions of Laplace’s equation in twodimensions. Each function represents a possible electrostatic potential. We canpick any function F(z) and it should represent some electric ﬁeld problem—infact, two problems, because U and V each represent solutions. We can writedown as many solutions as we wish—by just making up functions—then we justhave to ﬁnd the problem that goes with each solution. It may sound backwards,but it’s a possible approach.

Fig. 7-1. Two sets of orthogonal curves which can represent equipo-

tentials in a two-dimensional electrostatic ﬁeld.

As an example, let’s see what physics the function F(z) = z2 gives us. Fromit we get the two potential functions of (7.5) and (7.6). To see what problem thefunction U belongs to, we solve for the equipotential surfaces by setting U = A,a constant:

x2 − y2 = A.

This is the equation of a rectangular hyperbola. For various values of A, weget the hyperbolas shown in Fig. 7-1. When A = 0, we get the special case ofdiagonal straight lines through the origin.

7-3

CONDUCTOR +

etc.

E

etc.

Fig. 7-2. The ﬁeld near the point C is

the same as that in Fig. 7-1.

C

CONDUCTOR −

Such a set of equipotentials corresponds to several possible physical situations.First, it represents the ﬁne details of the ﬁeld near the point halfway between twoequal point charges. Second, it represents the ﬁeld at an inside right-angle cornerof a conductor. If we have two electrodes shaped like those in Fig. 7-2, which areheld at diﬀerent potentials, the ﬁeld near the corner marked C will look just likethe ﬁeld above the origin in Fig. 7-1. The solid lines are the equipotentials, andthe broken lines at right angles correspond to lines of E. Whereas at points orprotuberances the electric ﬁeld tends to be high, it tends to be low in dents orhollows.

The solution we have found also corresponds to that for a hyperbola-shapedelectrode near a right-angle corner, or for two hyperbolas at suitable potentials.You will notice that the ﬁeld of Fig. 7-1 has an interesting property. The x-component of the electric ﬁeld, Ex, is given by

Ex = − ∂φ∂x

= −2x.

The electric ﬁeld is proportional to the distance from the axis. This fact is used tomake devices (called quadrupole lenses) that are useful for focusing particle beams(see Section 29-7). The desired ﬁeld is usually obtained by using four hyperbolashaped electrodes, as shown in Fig. 7-3. For the electric ﬁeld lines in Fig. 7-3,we have simply copied from Fig. 7-1 the set of broken-line curves that representV = constant. We have a bonus! The curves for V = constant are orthogonal tothe ones for U = constant because of the equations (7.7) and (7.8). Wheneverwe choose a function F(z), we get from U and V both the equipotentials andﬁeld lines. And you will remember that we have solved either of two problems,depending on which set of curves we call the equipotentials.

As a second example, consider the function

If we write

where

and

then

z.

(7.11)

F(z) = √ρ =p

x2 + y2

z = x + iy = ρeiθ,

tan θ = y/x,

F(z) = ρ1/2eiθ/2

(cid:18)

= ρ1/2

cos θ

2 + i sin θ2

Fig. 7-3. The ﬁeld in a quadrupole lens.

(cid:19)

,

7-4

B=4

y

A=4

B=3

A=3

A=2

B=2

A=1

B=1

A=0

B=0

x

from which

(cid:20)(x2 + y2)1/2 + x

2

(cid:21)1/2

F(z) =

+ i

(cid:20)(x2 + y2)1/2 − x

2

Fig. 7-4. Curves of constant U(x, y )

and V (x, y ) from Eq. (7.12).

(cid:21)1/2

.

(7.12)

The curves for U(x, y) = A and V (x, y) = B, using U and V from Eq. (7.12),are plotted in Fig. 7-4. Again, there are many possible situations that could bedescribed by these ﬁelds. One of the most interesting is the ﬁeld near the edgeof a thin plate. If the line B = 0—to the right of the y-axis—represents a thincharged plate, the ﬁeld lines near it are given by the curves for various valuesof A. The physical situation is shown in Fig. 7-5.

Further examples are

F(z) = z2/3,

which yields the ﬁeld outside a rectangular corner

which yields the ﬁeld for a line charge, and

F(z) = ln z,

(7.13)

(7.14)

(7.15)which gives the ﬁeld for the two-dimensional analog of an electric dipole, i.e., twoparallel line charges with opposite polarities, very close together.

F(z) = 1/z,

We will not pursue this subject further in this course, but should emphasizethat although the complex variable technique is often powerful, it is limited totwo-dimensional problems; and also, it is an indirect method.

7-3 Plasma oscillationsWe consider now some physical situations in which the ﬁeld is determinedneither by ﬁxed charges nor by charges on conducting surfaces, but by a com-bination of two physical phenomena. In other words, the ﬁeld will be governedsimultaneously by two sets of equations: (1) the equations from electrostaticsrelating electric ﬁelds to charge distribution, and (2) an equation from anotherpart of physics that determines the positions or motions of the charges in thepresence of the ﬁeld.

The ﬁrst example that we will discuss is a dynamic one in which the motionof the charges is governed by Newton’s laws. A simple example of such a7-5

Fig. 7-5. The electric ﬁeld near the edge

of a thin grounded plate.

situation occurs in a plasma, which is an ionized gas consisting of ions and freeelectrons distributed over a region in space. The ionosphere—an upper layer ofthe atmosphere—is an example of such a plasma. The ultraviolet rays from thesun knock electrons oﬀ the molecules of the air, creating free electrons and ions.In such a plasma the positive ions are very much heavier than the electrons, sowe may neglect the ionic motion, in comparison to that of the electrons.

Let n0 be the density of electrons in the undisturbed, equilibrium state.Assuming the molecules are singly ionized, this must also be the density ofpositive ions, since the plasma is electrically neutral (when undisturbed). Nowwe suppose that the electrons are somehow moved from equilibrium and ask whathappens. If the density of the electrons in one region is increased, they will repeleach other and tend to return to their equilibrium positions. As the electronsmove toward their original positions they pick up kinetic energy, and instead ofcoming to rest in their equilibrium conﬁguration, they overshoot the mark. Theywill oscillate back and forth. The situation is similar to what occurs in soundwaves, in which the restoring force is the gas pressure. In a plasma, the restoringforce is the electrical force on the electrons.

To simplify the discussion, we will worry only about a situation in whichthe motions are all in one dimension, say x. Let us suppose that the electronsoriginally at x are, at the instant t, displaced from their equilibrium positionsby a small amount s(x, t). Since the electrons have been displaced, their densitywill, in general, be changed. The change in density is easily calculated. Referringto Fig. 7-6, the electrons initially contained between the two planes a and b havemoved and are now contained between the planes a0 and b0. The number ofelectrons that were between a and b is proportional to n0∆x; the same numberare now contained in the space whose width is ∆x+∆s. The density has changedto

n = n0∆x∆x + ∆s

=

n0

1 + (∆s/∆x) .

(7.16)

If the change in density is small, we can write [using the binomial expansionfor (1 + )−1]

(cid:18)1 − ∆s∆x

(cid:19)

.

n = n0

(7.17)

We assume that the positive ions do not move appreciably (because of the muchlarger inertia), so their density remains n0. Each electron carries the charge −qe,so the average charge density at any point is given by

or

ρ = −(n − n0)qe,

ρ = n0qe

dsdx

(7.18)

(where we have written the diﬀerential form for ∆s/∆x).

The charge density is related to the electric ﬁeld by Maxwell’s equations, in

particular,

∇ · E = ρ0

.

(7.19)

If the problem is indeed one-dimensional (and if there are no other ﬁelds but theone due to the displacements of the electrons), the electric ﬁeld E has a singlecomponent Ex. Equation (7.19), together with (7.18), gives

Integrating Eq. (7.20) gives

∂Ex∂x

= n0qe0

∂s∂x

.

Ex = n0qe0

s + K.

Since Ex = 0 when s = 0, the integration constant K is zero.

(7.20)

(7.21)

7-6

Fig. 7-6. Motion in a plasma wave. Theelectrons at the plane a move to a(cid:48), andthose at b move to b(cid:48).

The force on an electron in the displaced position is

Fx = − n0q20

e

s,

(7.22)

a restoring force proportional to the displacement s of the electron. This leadsto a harmonic oscillation of the electrons. The equation of motion of a displacedelectron is

d2sdt2

me

e

= − n0q2(7.23)0Its time variation will be as cos ωpt,

s.

We ﬁnd that s will vary harmonically.or—using the exponential notation of Vol. I—as

The frequency of oscillation ωp is determined from (7.23):

eiωpt.

ω2

p

= n0q2e0me

,

(7.24)

(7.25)

and is called the plasma frequency. It is a characteristic number of the plasma.When dealing with electron charges many people prefer to express theiranswers in terms of a quantity e2 deﬁned by

e2 = q2e4π0

= 2.3068 × 10−28 newton·meter2.

(7.26)

Using this convention, Eq. (7.25) becomes

ω2

p

= 4πe2n0me

,

(7.27)

which is the form you will ﬁnd in most books.

Thus we have found that a disturbance of a plasma will set up free oscillationsof the electrons about their equilibrium positions at the natural frequency ωp,which is proportional to the square root of the density of the electrons. Theplasma electrons behave like a resonant system, such as those we described inChapter 23 of Vol. I.

This natural resonance of a plasma has some interesting eﬀects. For example,if one tries to propagate a radiowave through the ionosphere, one ﬁnds that it canpenetrate only if its frequency is higher than the plasma frequency. Otherwise thesignal is reﬂected back. We must use high frequencies if we wish to communicatewith a satellite in space. On the other hand, if we wish to communicate with aradio station beyond the horizon, we must use frequencies lower than the plasmafrequency, so that the signal will be reﬂected back to the earth.

Another interesting example of plasma oscillations occurs in metals. In ametal we have a contained plasma of positive ions, and free electrons. Thedensity n0 is very high, so ωp is also. But it should still be possible to observethe electron oscillations. Now, according to quantum mechanics, a harmonicoscillator with a natural frequency ωp has energy levels which are separatedby the energy increment ωp. If, then, one shoots electrons through, say, analuminum foil, and makes very careful measurements of the electron energies onthe other side, one might expect to ﬁnd that the electrons sometimes lose theenergy ωp to the plasma oscillations. This does indeed happen. It was ﬁrstobserved experimentally in 1936 that electrons with energies of a few hundredto a few thousand electron volts lost energy in jumps when scattering from orgoing through a thin metal foil. The eﬀect was not understood until 1953 whenBohm and Pines* showed that the observations could be explained in terms ofquantum excitations of the plasma oscillations in the metal.

* For some recent work and a bibliography see C. J. Powell and J. B. Swann, Phys. Rev.

115, 869 (1959).

7-7

7-4 Colloidal particles in an electrolyteWe turn to another phenomenon in which the locations of charges are governedby a potential that arises in part from the same charges. The resulting eﬀectsinﬂuence in an important way the behavior of colloids. A colloid consists of asuspension in water of small charged particles which, though microscopic, froman atomic point of view are still very large. If the colloidal particles were notcharged, they would tend to coagulate into large lumps; but because of theircharge, they repel each other and remain in suspension.

Now if there is also some salt dissolved in the water, it will be dissociatedinto positive and negative ions. (Such a solution of ions is called an electrolyte.)The negative ions are attracted to the colloid particles (assuming their chargeis positive) and the positive ions are repelled. We will determine how the ionswhich surround such a colloidal particle are distributed in space.

To keep the ideas simple, we will again solve only a one-dimensional case. If wethink of a colloidal particle as a sphere having a very large radius—on an atomicscale!—we can then treat a small part of its surface as a plane. (Whenever one istrying to understand a new phenomenon it is a good idea to take a somewhatoversimpliﬁed model; then, having understood the problem with that model, oneis better able to proceed to tackle the more exact calculation.)We suppose that the distribution of ions generates a charge density ρ(x), andan electrical potential φ, related by the electrostatic law ∇2φ = −ρ/0 or, forﬁelds that vary in only one dimension, by

d2φdx2

= − ρ0

.

(7.28)

Now supposing there were such a potential φ(x), how would the ions distributethemselves in it? This we can determine by the principles of statistical mechanics.Our problem then is to determine φ so that the resulting charge density fromstatistical mechanics also satisﬁes (7.28).According to statistical mechanics (see Chapter 40, Vol. I), particles in thermalequilibrium in a force ﬁeld are distributed in such a way that the density n ofparticles at the position x is given by

n(x) = n0e−U(x)/kT ,

(7.29)where U(x) is the potential energy, k is Boltzmann’s constant, and T is theabsolute temperature.We assume that the ions carry one electronic charge, positive or negative. Atthe distance x from the surface of a colloidal particle, a positive ion will havepotential energy qeφ(x), so that

U(x) = qeφ(x).

The density of positive ions, n+, is then

n+(x) = n0e−qeφ(x)/kT .

Similarly, the density of negative ions is

n−(x) = n0e+qeφ(x)/kT .

The total charge density is

or

ρ = qen+ − qen−,

ρ = qen0(e−qeφ/kT − e+qeφ/kT ).

Combining this with Eq. (7.28), we ﬁnd that the potential φ must satisfy

d2φdx2

= − qen00

(e−qeφ/kT − e+qeφ/kT ).

(7.30)

(7.31)

7-8

This equation is readily solved in general [multiply both sides by 2(dφ/dx), andintegrate with respect to x], but to keep the problem as simple as possible, wewill consider here only the limiting case in which the potentials are small or thetemperature T is high. The case where φ is small corresponds to a dilute solution.For these cases the exponent is small, and we can approximate

Equation (7.31) then gives

e±qeφ/kT = 1 ± qeφkT

.

d2φdx2

= +2n0q2e0kT

φ(x).

(7.32)

(7.33)

Notice that this time the sign on the right is positive. The solutions for φ arenot oscillatory, but exponential.

The general solution of Eq. (7.33) is

with

φ = Ae−x/D + Be+x/D,

D2 = 0kT2n0q2

e

.

(7.34)

(7.35)

The constants A and B must be determined from the conditions of the problem.In our case, B must be zero; otherwise the potential would go to inﬁnity forlarge x. So we have that(7.36)

φ = Ae−x/D,

in which A is the potential at x = 0, the surface of the colloidal particle.

φ

A

Fig. 7-7. The variation of the potentialnear the surface of a colloidal particle. D isthe Debye length.

00

D

2D

3D

x

The potential decreases by a factor 1/e each time the distance increases by D,as shown in the graph of Fig. 7-7. The number D is called the Debye length, andis a measure of the thickness of the ion sheath that surrounds a large chargedparticle in an electrolyte. Equation (7.35) says that the sheath gets thinner withincreasing concentration of the ions (n0) or with decreasing temperature.density σ on the colloid particle. We know thatEn = Ex(0) = σ0

The constant A in Eq. (7.36) is easily obtained if we know the surface charge

(7.37)

.

But E is also the gradient of φ:

from which we get

Ex(0) = − ∂φ∂x

(cid:12)(cid:12)(cid:12)(cid:12)0

= + AD

,

(7.38)

(7.39)

7-9

A = σD0

.

Using this result in (7.36), we ﬁnd (by taking x = 0) that the potential of thecolloidal particle is

φ(0) = σD0

.

(7.40)

You will notice that this potential is the same as the potential diﬀerence across acondenser with a plate spacing D and a surface charge density σ.We have said that the colloidal particles are kept apart by their electricalrepulsion. But now we see that the ﬁeld a little way from the surface of a particleis reduced by the ion sheath that collects around it. If the sheaths get thinenough, the particles have a good chance of knocking against each other. Theywill then stick, and the colloid will coagulate and precipitate out of the liquid.From our analysis, we understand why adding enough salt to a colloid shouldcause it to precipitate out. The process is called「salting out a colloid.」

Another interesting example is the eﬀect that a salt solution has on proteinmolecules. A protein molecule is a long, complicated, and ﬂexible chain of aminoacids. The molecule has various charges on it, and it sometimes happens thatthere is a net charge, say negative, which is distributed along the chain. Becauseof mutual repulsion of the negative charges, the protein chain is kept stretchedout. Also, if there are other similar chain molecules present in the solution,they will be kept apart by the same repulsive eﬀects. We can, therefore, havea suspension of chain molecules in a liquid. But if we add salt to the liquidwe change the properties of the suspension. As salt is added to the solution,decreasing the Debye distance, the chain molecules can approach one another,and can also coil up. If enough salt is added to the solution, the chain moleculeswill precipitate out of the solution. There are many chemical eﬀects of this kindthat can be understood in terms of electrical forces.

7-5 The electrostatic ﬁeld of a gridAs our last example, we would like to describe another interesting property ofelectric ﬁelds. It is one which is made use of in the design of electrical instruments,in the construction of vacuum tubes, and for other purposes. This is the characterof the electric ﬁeld near a grid of charged wires. To make the problem as simpleas possible, let us consider an array of parallel wires lying in a plane, the wiresbeing inﬁnitely long and with a uniform spacing between them.

If we look at the ﬁeld a large distance above the plane of the wires, we seea constant electric ﬁeld, just as though the charge were uniformly spread overa plane. As we approach the grid of wires, the ﬁeld begins to deviate from theuniform ﬁeld we found at large distances from the grid. We would like to estimatehow close to the grid we have to be in order to see appreciable variations inthe potential. Figure 7-8 shows a rough sketch of the equipotentials at variousdistances from the grid. The closer we get to the grid, the larger the variations.As we travel parallel to the grid, we observe that the ﬁeld ﬂuctuates in a periodicmanner.

z

+

+

+

+

+

+

Fig. 7-8. Equipotential surfaces above a

uniform grid of charged wires.

a

x

7-10

try terms like

Now we have seen (Chapter 50, Vol. I) that any periodic quantity can beexpressed as a sum of sine waves (Fourier’s theorem). Let’s see if we can ﬁnd asuitable harmonic function that satisﬁes our ﬁeld equations.

If the wires lie in the xy-plane and run parallel to the y-axis, then we might

φ(x, z) = Fn(z) cos 2πnx

(7.41)where a is the spacing of the wires and n is the harmonic number. (We haveassumed long wires, so there should be no variation with y.) A complete solutionwould be made up of a sum of such terms for n = 1, 2, 3, . . . .If this is to be a valid potential, it must satisfy Laplace’s equation in theregion above the wires (where there are no charges). That is,

a

,

∂2φ∂x2

+ ∂2φ∂z2

= 0.

Trying this equation on the φ in (7.41), we ﬁnd that

− 4π2n2or that Fn(z) must satisfy

a2 Fn(z) cos 2πnx

a

+ d2Fndz2

cos 2πnx

a

= 0,

So we must have

where

d2Fndz2

= 4πn2

a2 Fn.

Fn = Ane−z/z0 ,

z0 = a2πn

.

(7.42)

(7.43)

(7.44)

(7.45)

We have found that if there is a Fourier component of the ﬁeld of harmonic n, thatcomponent will decrease exponentially with a characteristic distance z0 = a/2πn.For the ﬁrst harmonic (n = 1), the amplitude falls by the factor e−2π (a largedecrease) each time we increase z by one grid spacing a. The other harmonics falloﬀ even more rapidly as we move away from the grid. We see that if we are onlya few times the distance a away from the grid, the ﬁeld is very nearly uniform,i.e., the oscillating terms are small. There would, of course, always remain the「zero harmonic」ﬁeld

φ0 = −E0z

to give the uniform ﬁeld at large z. For a complete solution, we would combinethis term with a sum of terms like (7.41) with Fn from (7.44). The coeﬃcients Anwould be adjusted so that the total sum would, when diﬀerentiated, give anelectric ﬁeld that would ﬁt the charge density λ of the grid wires.The method we have just developed can be used to explain why electrostaticshielding by means of a screen is often just as good as with a solid metal sheet.Except within a distance from the screen a few times the spacing of the screenwires, the ﬁelds inside a closed screen are zero. We see why copper screen—lighter and cheaper than copper sheet—is often used to shield sensitive electricalequipment from external disturbing ﬁelds.

7-11

8

Electrostatic Energy

