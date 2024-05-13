41-1 ViscosityIn

the last chapter we discussed the behavior of water, disregarding thephenomenon of viscosity. Now we would like to discuss the phenomena of theﬂow of ﬂuids, including the eﬀects of viscosity. We want to look at the realbehavior of ﬂuids. We will describe qualitatively the actual behavior of theﬂuids under various diﬀerent circumstances so that you will get some feel forthe subject. Although you will see some complicated equations and hear aboutsome complicated things, it is not our purpose that you should learn all thesethings. This is, in a sense, a「cultural」chapter which will give you some idea ofthe way the world is. There is only one item which is worth learning, and that isthe simple deﬁnition of viscosity which we will come to in a moment. The rest isonly for your entertainment.

In the last chapter we found that the laws of motion of a ﬂuid are contained

in the equation

+ (v · ∇)v = −∇p

∂v∂t

− ∇φ + f viscρ

ρ

.

(41.1)

In our「dry」water approximation we left out the last term, so we were neglectingall viscous eﬀects. Also, we sometimes made an additional approximation byconsidering the ﬂuid as incompressible; then we had the additional equation

∇ · v = 0.

This last approximation is often quite good—particularly when ﬂow speeds aremuch slower than the speed of sound. But in real ﬂuids it is almost never true thatwe can neglect the internal friction that we call viscosity; most of the interestingthings that happen come from it in one way or another. For example, we sawthat in「dry」water the circulation never changes—if there is none to start outwith, there will never be any. Yet, circulation in ﬂuids is an everyday occurrence.We must ﬁx up our theory.

We begin with an important experimental fact. When we worked out the ﬂowof「dry」water around or past a cylinder—the so-called「potential ﬂow」—we hadno reason not to permit the water to have a velocity tangent to the surface; onlythe normal component had to be zero. We took no account of the possibilitythat there might be a shear force between the liquid and the solid. It turnsout—although it is not at all self-evident—that in all circumstances where it hasbeen experimentally checked, the velocity of a ﬂuid is exactly zero at the surfaceof a solid. You have noticed, no doubt, that the blade of a fan will collect a thinlayer of dust—and that it is still there after the fan has been churning up theair. You can see the same eﬀect even on the great fan of a wind tunnel. Whyisn’t the dust blown oﬀ by the air? In spite of the fact that the fan blade ismoving at high speed through the air, the speed of the air relative to the fanblade goes to zero right at the surface. So the very smallest dust particles arenot disturbed.* We must modify the theory to agree with the experimental factthat in all ordinary ﬂuids, the molecules next to a solid surface have zero velocity(relative to the surface).†

* You can blow large dust particles from a table top, but not the very ﬁnest ones. The large

ones stick up into the breeze.

† You can imagine circumstances when it is not true: glass is theoretically a「liquid,」butit can certainly be made to slide along a steel surface. So our assertion must break downsomewhere.

41-1

Fig. 41-1. Viscous drag between two par-

allel plates.

We originally characterized a liquid by the fact that if you put a shearing stresson it—no matter how small—it would give way. It ﬂows. In static situations,there are no shear stresses. But before equilibrium is reached—as long as youstill push on it—there can be shear forces. Viscosity describes these shear forceswhich exist in a moving ﬂuid. To get a measure of the shear forces during themotion of a ﬂuid, we consider the following kind of experiment. Suppose that wehave two solid plane surfaces with water between them, as in Fig. 41-1, and wekeep one stationary while moving the other parallel to it at the slow speed v0. Ifyou measure the force required to keep the upper plate moving, you ﬁnd thatit is proportional to the area of the plates and to v0/d, where d is the distancebetween the plates. So the shear stress F/A is proportional to v0/d:

FA

= η

v0d

.

The constant of proportionality η is called the coeﬃcient of viscosity.If we have a more complicated situation, we can always consider a little, ﬂat,rectangular cell in the water with its faces parallel to the ﬂow, as in Fig. 41-2.The shear force across this cell is given by∆vx∆y

∆F∆A

(41.2)

∂vx∂y

.

= η

= η

Now, ∂vx/∂y is the rate of change of the shear strain we deﬁned in Chapter 39,so for a liquid, the shear stress is proportional to the rate of change of the shearstrain.

In the general case we write

(cid:18) ∂vy

∂x

(cid:19)

Sxy = η

+ ∂vx∂y

.

(41.3)

If there is a uniform rotation of the ﬂuid, ∂vx/∂y is the negative of ∂vy/∂x andSxy is zero—as it should be since there are no stresses in a uniformly rotatingﬂuid. (We did a similar thing in deﬁning exy in Chapter 39.) There are, of course,the corresponding expressions for Syz and Szx.As an example of the application of these ideas, we consider the motion of aﬂuid between two coaxial cylinders. Let the inner one have the radius a and theperipheral velocity va, and let the outer one have radius b and velocity vb. SeeFig. 41-3. We might ask, what is the velocity distribution between the cylinders?To answer this question, we begin by ﬁnding a formula for the viscous shear in theﬂuid at a distance r from the axis. From the symmetry of the problem, we canassume that the ﬂow is always tangential and that its magnitude depends onlyon r; v = v(r). If we watch a speck in the water at the radius r, its coordinatesas a function of time are

x = r cos ωt,

y = r sin ωt,

where ω = v/r. Then the x- and y-components of velocity are

vx = −rω sin ωt = −ωy

and

vy = rω cos ωt = ωx.

(41.4)

(41.5)

41-2

From Eq. (41.3), we have

(cid:20) ∂

Sxy = η

(xω) − ∂∂y

∂x

(yω)

= η

x

∂ω∂x

− y

∂ω∂y

(cid:21)

(cid:20)

(cid:21)

.

Fig. 41-2. The shear stress in a viscous

ﬂuid.

Fig. 41-3. The ﬂow in a ﬂuid betweentwo concentric cylinders rotating at diﬀerentangular velocities.

For a point at y = 0, ∂ω/∂y = 0, and x ∂ω/∂x is the same as r dω/dr. So at thatpoint

(Sxy)y=0 = ηr

.

(41.6)

dωdr

(It is reasonable that S should depend on ∂ω/∂r; when there is no change in ωwith r, the liquid is in uniform rotation and there are no stresses.)

The stress we have calculated is the tangential shear which is the same allaround the cylinder. We can get the torque acting across a cylindrical surfaceat the radius r by multiplying the shear stress by the moment arm r and thearea 2πrl (where l is the length of the cylinder). We get

τ = 2πr2l(Sxy)y=0 = 2πηlr3 dωdr

.

(41.7)

Since the motion of the water is steady—there is no angular acceleration—thenet torque on the cylindrical shell of water between r and r+dr must be zero; thatis, the torque at r must be balanced by an equal and opposite torque at r + dr,so that τ must be independent of r. In other words, r3 dω/dr is equal to someconstant, say A, and

= Ar3 .Integrating, we ﬁnd that ω varies with r as

dωdr

ω = − A2r2

+ B.

(41.8)

(41.9)

The constants A and B are to be determined to ﬁt the conditions that ω = ωaat r = a, and ω = ωb at r = b. We get that

(ωb − ωa),

A = 2a2b2b2 − a2B = b2ωb − a2ωab2 − a2

.

So we know ω as a function of r, and from it v = ωr.

If we want the torque, we can get it from Eqs. (41.7) and (41.8):

or

τ = 2πηlA

τ = 4πηla2b2b2 − a2

(ωb − ωa).

(41.10)

(41.11)

It is proportional to the relative angular velocities of the two cylinders. Onestandard apparatus for measuring the coeﬃcients of viscosity is built this way. Onecylinder—say the outer one—is on pivots but is held stationary by a spring balancewhich measures the torque on it, while the inner one is rotated at a constantangular velocity. The coeﬃcient of viscosity is then determined from Eq. (41.11).From its deﬁnition, you see that the units of η are newton·sec/m2. For water

at 20◦C,

η = 10−3 newton·sec/m2.

It is usually more convenient to use the speciﬁc viscosity, which is η divided bythe density ρ. The values for water and air are then comparable:

water at 20◦C,air at 20◦C,

η/ρ = 10−6 m2/sec,η/ρ = 15 × 10−6 m2/sec.

(41.12)

Viscosities usually depend strongly on temperature. For instance, for water justabove the freezing point, η/ρ is 1.8 times larger than it is at 20◦C.

41-3

(cid:18) ∂vi

∂xj

Sij = η

+ ∂vj∂xi

(cid:19)

41-2 Viscous ﬂowWe now go to a general theory of viscous ﬂow—at least in the most generalform known to man. We already understand that the shear stress componentsare proportional to the spatial derivatives of the various velocity componentssuch as ∂vx/∂y or ∂vy/∂x. However, in the general case of a compressible ﬂuidthere is another term in the stress which depends on other derivatives of thevelocity. The general expression is

+ η0 δij(∇ · v),

(41.13)

where xi is any one of the rectangular coordinates x, y, or z, and vi is any oneof the rectangular coordinates of the velocity. (The symbol δij is the Kroneckerdelta which is 1 when i = j and 0 for i 6= j.) The additional term adds η0 ∇· v toall the diagonal elements Sii of the stress tensor. If the liquid is incompressible∇· v = 0, and this extra term doesn’t appear. So it has to do with internal forcesduring compression. So two constants are required to describe the liquid, just aswe had two constants to describe a homogeneous elastic solid. The coeﬃcient ηis the「ordinary」coeﬃcient of viscosity which we have already encountered. Itis also called the ﬁrst coeﬃcient of viscosity or the「shear viscosity coeﬃcient,」and the new coeﬃcient η0 is called the second coeﬃcient of viscosity.Now we want to determine the viscous force per unit volume, f visc, so we canput it into Eq. (41.1) to get the equation of motion for a real ﬂuid. The forceon a small cubical volume element of a ﬂuid is the resultant of the forces on allthe six faces. Taking them two at a time, we will get diﬀerences that dependon the derivatives of the stresses, and, therefore, on the second derivatives ofthe velocity. This is nice because it will get us back to a vector equation. Thecomponent of the viscous force per unit volume in the direction of the rectangularcoordinate xi is

3X3X

j=1

j=1

(fvisc)i =

=

∂Sij∂xj

∂∂xj

(cid:26)

(cid:18) ∂vi

∂xj

η

+ ∂vj∂xi

(cid:19)(cid:27)

+ ∂∂xi

(η0 ∇ · v).

(41.14)

Usually, the variation of the viscosity coeﬃcients with position is not signiﬁcantand can be neglected. Then, the viscous force per unit volume contains onlysecond derivatives of the velocity. We saw in Chapter 39 that the most generalform of second derivatives that can occur in a vector equation is the sum ofa term in the Laplacian (∇ · ∇v = ∇2v), and a term in the gradient of theη and (η + η0). We get

divergence(cid:0)∇(∇ · v)(cid:1). Equation (41.14) is just such a sum with the coeﬃcients

f visc = η ∇2v + (η + η0)∇(∇ · v).

(41.15)In the incompressible case, ∇ · v = 0, and the viscous force per unit volume isjust η ∇2v. That is all that many people use; however, if you should want tocalculate the absorption of sound in a ﬂuid, you would need the second term.We can now complete our general equation of motion for a real ﬂuid. Substi-

tuting Eq. (41.15) into Eq. (41.1), we get

+ (v · ∇)v

= −∇p − ρ∇φ + η ∇2v + (η + η0)∇(∇ · v).

It’s complicated. But that’s the way nature is.

If we introduce the vorticity Ω = ∇ × v, as we did before, we can write our

(cid:26) ∂v

∂t

ρ

(cid:27)

(cid:27)

equation as

(cid:26) ∂v

∂t

ρ

+ Ω × v + 1

2 ∇v2

= −∇p − ρ∇φ + η ∇2v

+ (η + η0)∇(∇ · v).

(41.16)

41-4

We are supposing again that the only body forces acting are conservative forceslike gravity. To see what the new term means, let’s look at the incompressibleﬂuid case. Then, if we take the curl of Eq. (41.16), we get

∂Ω∂t

+ ∇ × (Ω × v) = ηρ

∇2Ω.

(41.17)

This is like Eq. (40.9) except for the new term on the right-hand side. Whenthe right-hand side was zero, we had the Helmholtz theorem that the vorticitystays with the ﬂuid. Now, we have the rather complicated nonzero term on theright-hand side which, however, has straightforward physical consequences. If wedisregard for the moment the term ∇ × (Ω × v), we have a diﬀusion equation.The new term means that the vorticity Ω diﬀuses through the ﬂuid. If there is alarge gradient in the vorticity, it will spread out into the neighboring ﬂuid.This is the term that causes the smoke ring to get thicker as it goes along.Also, it shows up nicely if you send a「clean」vortex (a「smokeless」ring made bythe apparatus described in the last chapter) through a cloud of smoke. Whenit comes out of the cloud, it will have picked up some smoke, and you will seea hollow shell of a smoke ring. Some of the Ω diﬀuses outward into the smoke,while still maintaining its forward motion with the vortex.

41-3 The Reynolds numberWe will now describe the changes which are made in the character of ﬂuidﬂow as a consequence of the new viscosity term. We will look at two problems insome detail. The ﬁrst of these is the ﬂow of a ﬂuid past a cylinder—a ﬂow whichwe tried to calculate in the previous chapter using the theory for nonviscous ﬂow.It turns out that the viscous equations can be solved by man today only for afew special cases. So some of what we will tell you is based on experimentalmeasurements—assuming that the experimental model satisﬁes Eq. (41.17).

The mathematical problem is this: We would like the solution for the ﬂowof an incompressible, viscous ﬂuid past a long cylinder of diameter D. The ﬂowshould be given by Eq. (41.17) and by

Ω = ∇ × v

(41.18)

with the conditions that the velocity at large distances is some constant velocity,say V (parallel to the x-axis), and at the surface of the cylinder is zero. That is,(41.19)

vx = vy = vz = 0

for

x2 + y2 = D24 .

That speciﬁes completely the mathematical problem.

If you look at the equations, you see that there are four diﬀerent parametersto the problem: η, ρ, D, and V . You might think that we would have to give awhole series of cases for diﬀerent V ’s, diﬀerent D’s, and so on. However, that isnot the case. All the diﬀerent possible solutions correspond to diﬀerent valuesof one parameter. This is the most important general thing we can say aboutviscous ﬂow. To see why this is so, notice ﬁrst that the viscosity and densityappear only in the ratio η/ρ—the speciﬁc viscosity. That reduces the number ofindependent parameters to three. Now suppose we measure all distances in theonly length that appears in the problem, the diameter D of the cylinder; that is,we substitute for x, y, z, the new variables x0, y0, z0 withz = z0D.

x = x0D,

y = y0D,

Then D disappears from (41.19). In the same way, if we measure all velocities interms of V —that is, we set v = v0V —we get rid of the V , and v0 is just equalto 1 at large distances. Since we have ﬁxed our units of length and velocity, our41-5

R = ρη

V D.

(41.22)

unit of time is now D/V ; so we should set

t = t0 DV

.

(41.20)

With our new variables, the derivatives in Eq. (41.18) get changed from ∂/∂x

to (1/D) ∂/∂x0, and so on; so Eq. (41.18) becomes

Ω = ∇ × v = VDOur main equation (41.17) then reads

∇0 × v0 = VD

Ω0.

(41.21)

∂Ω0∂t0 + ∇0 × (Ω0 × v0) = η

ρV D

∇02Ω0.

All the constants condense into one factor which we write, following tradition,as 1/R:

If we just remember that all of our equations are to be written with all quantitiesin the new units, we can omit all the primes. Our equations for the ﬂow are then

and

with the conditions

for

and

for

∂Ω∂t

+ ∇ × (Ω × v) = 1

R

∇2Ω.

Ω = ∇ × v

v = 0

x2 + y2 = 1/4

vx = 1,

vy = vz = 0

x2 + y2 + z2 (cid:29) 1.

(41.23)

(41.24)

What this all means physically is very interesting. It means, for example,that if we solve the problem of the ﬂow for one velocity V1 and a certain cylinderdiameter D1, and then ask about the ﬂow for a diﬀerent diameter D2 and adiﬀerent ﬂuid, the ﬂow will be the same for the velocity V2 which gives the sameReynolds number—that is, whenR1 = ρ1η1

V1D1 = R2 = ρ2η2

(41.25)

V2D2.

For any two situations which have the same Reynolds number, the ﬂows will「look」the same—in terms of the appropriate scaled x0, y0, z0, and t0. This isan important proposition because it means that we can determine what thebehavior of the ﬂow of air past an airplane wing will be without having to buildan airplane and try it. We can, instead, make a model and make measurementsusing a velocity that gives the same Reynolds number. This is the principle whichallows us to apply the results of「wind-tunnel」measurements on small-scaleairplanes, or「model-basin」results on scale model boats, to the full-scale objects.Remember, however, that we can only do this provided the compressibility of theﬂuid can be neglected. Otherwise, a new quantity enters—the speed of sound.And diﬀerent situations will really correspond to each other only if the ratio of Vto the sound speed is also the same. This latter ratio is called the Mach number.So, for velocities near the speed of sound or above, the ﬂows are the same in twosituations if both the Mach number and the Reynolds number are the same forboth situations.

41-6

Fig. 41-4. The drag coeﬃcient CD of a circular cylinder as a function of the Reynolds number.

41-4 Flow past a circular cylinderLet’s go back to the problem of low-speed (nearly incompressible) ﬂow over thecylinder. We will give a qualitative description of the ﬂow of a real ﬂuid. Thereare many things we might want to know about such a ﬂow—for instance, what isthe drag force on the cylinder? The drag force on a cylinder is plotted in Fig. 41-4as a function of R—which is proportional to the air speed V if everything else isheld ﬁxed. What is actually plotted is the so-called drag coeﬃcient CD, which isa dimensionless number equal to the force divided by 12 ρV 2Dl, where D is thediameter, l is the length of the cylinder, and ρ is the density of the liquid:

CD =

F

12 ρV 2Dl

.

The coeﬃcient of drag varies in a rather complicated way, giving us a pre-hint thatsomething rather interesting and complicated is happening in the ﬂow. We willnow describe the nature of ﬂow for the diﬀerent ranges of the Reynolds number.First, when the Reynolds number is very small, the ﬂow is quite steady; thatis, the velocity is constant at any place, and the ﬂow goes around the cylinder.The actual distribution of the ﬂow lines is, however, not like it is in potentialﬂow. They are solutions of a somewhat diﬀerent equation. When the velocityis very low or, what is equivalent, when the viscosity is very high so the stuﬀ islike honey, then the inertial terms are negligible and the ﬂow is described by theequation

∇2Ω = 0.

This equation was ﬁrst solved by Stokes. He also solved the same problem for asphere. If you have a small sphere moving under such conditions of low Reynoldsnumber, the force needed to drag it is equal to 6πηaV , where a is the radius ofthe sphere and V is its velocity. This is a very useful formula because it tells thespeed at which tiny grains of dirt (or other particles which can be approximated asspheres) move through a ﬂuid under a given force—as, for instance, in a centrifuge,or in sedimentation, or diﬀusion. In the low Reynolds number region—for R lessthan 1—the lines of v around a cylinder are as drawn in Fig. 41-5.If we now increase the ﬂuid speed to get a Reynolds number somewhat greaterthan 1, we ﬁnd that the ﬂow is diﬀerent. There is a circulation behind the41-7

Fig. 41-5. Viscous ﬂow (low velocities)

around a circular cylinder.

Fig. 41-6. Flow past a cylinder for various Reynolds numbers.

sphere, as shown in Fig. 41-6(b). It is still an open question as to whether thereis always a circulation there even at the smallest Reynolds number or whetherthings suddenly change at a certain Reynolds number. It used to be thoughtthat the circulation grew continuously. But it is now thought that it appearssuddenly, and it is certain that the circulation increases with R. In any case,there is a diﬀerent character to the ﬂow for R in the region from about 10 to 30.There is a pair of vortices behind the cylinder.

The ﬂow changes again by the time we get to a number of 40 or so. Thereis suddenly a complete change in the character of the motion. What happensis that one of the vortices behind the cylinder gets so long that it breaks oﬀand travels downstream with the ﬂuid. Then the ﬂuid curls around behind thecylinder and makes a new vortex. The vortices peel oﬀ alternately on each side,so an instantaneous view of the ﬂow looks roughly as sketched in Fig. 41-6(c).41-8

Fig. 41-7. Photograph by Ludwig Prandtlof the「vortex street」in the ﬂow behind acylinder.

The stream of vortices is called a「Kármán vortex street.」They always appearfor R > 40. We show a photograph of such a ﬂow in Fig. 41-7.The diﬀerence between the two ﬂows in Fig. 41-6(c) and 41-6(b) or 41-6(a)is almost a complete diﬀerence in regime. In Fig. 41-6(a) or (b), the velocityis constant, whereas in Fig. 41-6(c), the velocity at any point varies with time.There is no steady solution above R = 40—which we have marked on Fig. 41-4by a dashed line. For these higher Reynolds numbers, the ﬂow varies with timebut in a regular, cyclic fashion.We can get a physical idea of how these vortices are produced. We know thatthe ﬂuid velocity must be zero at the surface of the cylinder and that it alsoincreases rapidly away from that surface. Vorticity is created by this large localvariation in ﬂuid velocity. Now when the main stream velocity is low enough,there is suﬃcient time for this vorticity to diﬀuse out of the thin region near thesolid surface where it is produced and to grow into a large region of vorticity.This physical picture should help to prepare us for the next change in the natureof the ﬂow as the main stream velocity, or R, is increased still more.

As the velocity gets higher and higher, there is less and less time for thevorticity to diﬀuse into a larger region of ﬂuid. By the time we reach a Reynoldsnumber of several hundred, the vorticity begins to ﬁll in a thin band, as shownin Fig. 41-6(d). In this layer the ﬂow is chaotic and irregular. The region iscalled the boundary layer and this irregular ﬂow region works its way farther andfarther upstream as R is increased. In the turbulent region, the velocities arevery irregular and「noisy」; also the ﬂow is no longer two-dimensional but twistsand turns in all three dimensions. There is still a regular alternating motionsuperimposed on the turbulent one.

As the Reynolds number is increased further, the turbulent region works itsway forward until it reaches the point where the ﬂow lines leave the cylinder—forﬂows somewhat above R = 105. The ﬂow is as shown in Fig. 41-6(e), and wehave what is called a「turbulent boundary layer.」Also, there is a drastic changein, the drag force; it drops by a large factor, as shown in Fig. 41-4. In this speedregion, the drag force actually decreases with increasing speed. There seems tobe little evidence of periodicity.What happens for still larger Reynolds numbers? As we increase the speedfurther, the wake increases in size again and the drag increases. The latestexperiments—which go up to R = 107 or so—indicate that a new periodicityappears in the wake, either because the whole wake is oscillating back and forthin a gross motion or because some new kind of vortex is occurring together withan irregular noisy motion. The details are as yet not entirely clear, and are stillbeing studied experimentally.

41-5 The limit of zero viscosityWe would like to point out that none of the ﬂows we have described areanything like the potential ﬂow solution we found in the preceding chapter. Thisis, at ﬁrst sight, quite surprising. After all, R is proportional to 1/η. So η going41-9

to zero is equivalent to R going to inﬁnity. And if we take the limit of large R inEq. (41.23), we get rid of the right-hand side and get just the equations of thelast chapter. Yet, you would ﬁnd it hard to believe that the highly turbulentﬂow at R = 107 was approaching the smooth ﬂow computed from the equationsof「dry」water. How can it be that as we approach R = ∞, the ﬂow describedby Eq. (41.23) gives a completely diﬀerent solution from the one we obtainedtaking η = 0 to start out with? The answer is very interesting. Note that theright-hand term of Eq. (41.23) has 1/R times a second derivative. It is a higherderivative than any other derivative in the equation. What happens is thatalthough the coeﬃcient 1/R is small, there are very rapid variations of Ω inthe space near the surface. These rapid variations compensate for the smallcoeﬃcient, and the product does not go to zero with increasing R. The solutionsdo not approach the limiting case as the coeﬃcient of ∇2Ω goes to zero.You may be wondering,「What is the ﬁne-grain turbulence and how does itmaintain itself? How can the vorticity which is made somewhere at the edge ofthe cylinder generate so much noise in the background?」The answer is againinteresting. Vorticity has a tendency to amplify itself. If we forget for a momentabout the diﬀusion of vorticity which causes a loss, the laws of ﬂow say (as wehave seen) that the vortex lines are carried along with the ﬂuid, at the velocity v.We can imagine a certain number of lines of Ω which are being distorted andtwisted by the complicated ﬂow pattern of v. This pulls the lines closer togetherand mixes them all up. Lines that were simple before will get knotted and pulledclose together. They will be longer and tighter together. The strength of thevorticity will increase and its irregularities—the pluses and minuses—will, ingeneral, increase. So the magnitude of vorticity in three dimensions increases aswe twist the ﬂuid about.

You might well ask,「When is the potential ﬂow a satisfactory theory at all?」In the ﬁrst place, it is satisfactory outside the turbulent region where the vorticityhas not entered appreciably by diﬀusion. By making special streamlined bodies,we can keep the turbulent region as small as possible; the ﬂow around airplanewings—which are carefully designed—is almost entirely true potential ﬂow.

41-6 Couette ﬂowIt is possible to demonstrate that the complex and shifting character of theﬂow past a cylinder is not special but that the great variety of ﬂow possibilitiesoccurs generally. We have worked out in Section 41-1 a solution for the viscousﬂow between two cylinders, and we can compare the results with what actuallyhappens. If we take two concentric cylinders with an oil in the space betweenthem and put a ﬁne aluminum powder as a suspension in the oil, the ﬂow is easyto see. Now if we turn the outer cylinder slowly, nothing unexpected happens;see Fig. 41-8(a). Alternatively, if we turn the inner cylinder slowly, nothing verystriking occurs. However, if we turn the inner cylinder at a higher rate, we geta surprise. The ﬂuid breaks into horizontal bands, as indicated in Fig. 41-8(b).When the outer cylinder rotates at a similar rate with the inner one at rest, nosuch eﬀect occurs. How can it be that there is a diﬀerence between rotating theinner or the out cylinder? After all, the ﬂow pattern we derived in Section 41-1depended only on ωb − ωa. We can get the answer by looking at the cross sectionsshown in Fig. 41-9. When the inner layers of the ﬂuid are moving more rapidlythan the outer ones, they tend to move outward—the centrifugal force is largerthan the pressure holding them in place. A whole layer cannot move out uniformlybecause the outer layers are in the way. It must break into cells and circulate, asshown in Fig. 41-9(b). It is like the convection currents in a room which has hotair at the bottom. When the inner cylinder is at rest and the outer cylinder hasa high velocity, the centrifugal forces build up a pressure gradient which keepseverything in equilibrium—see Fig. 41-9(c) (as in a room with hot air at the top).Now let’s speed up the inner cylinder. At ﬁrst, the number of bands increases.Then suddenly you see the bands become wavy, as in Fig. 41-8(c), and the wavestravel around the cylinder. The speed of these waves is easily measured. For high41-10

Fig. 41-8. Liquid ﬂow patterns between

two transparent rotating cylinders.

Fig. 41-9. Why the ﬂow breaks up into bands.

rotation speeds they approach 1/3 the speed of the inner cylinder. And no oneknows why! There’s a challenge. A simple number like 1/3, and no explanation.In fact, the whole mechanism of the wave formation is not very well understood;yet it is steady laminar ﬂow.

If we now start rotating the outer cylinder also—but in the opposite direction—the ﬂow pattern starts to break up. We get wavy regions alternating withapparently quiet regions, as sketched in Fig. 41-8(d), making a spiral pattern. Inthese「quiet」regions, however, we can see that the ﬂow is really quite irregular;it is, in fact completely turbulent. The wavy regions also begin to show irregularturbulent ﬂow. If the cylinders are rotated still more rapidly, the whole ﬂowbecomes chaotically turbulent.

In this simple experiment we see many interesting regimes of ﬂow which arequite diﬀerent, and yet which are all contained in our simple equation for variousvalues of the one parameter R. With our rotating cylinders, we can see many ofthe eﬀects which occur in the ﬂow past a cylinder: ﬁrst, there is a steady ﬂow;second, a ﬂow sets in which varies in time but in a regular, smooth way; ﬁnally,the ﬂow becomes completely irregular. You have all seen the same eﬀects in thecolumn of smoke rising from a cigarette in quiet air. There is a smooth steadycolumn followed by a series of twistings as the stream of smoke begins to breakup, ending ﬁnally in an irregular churning cloud of smoke.

The main lesson to be learned from all of this is that a tremendous variety ofbehavior is hidden in the simple set of equations in (41.23). All the solutions arefor the same equations, only with diﬀerent values of R. We have no reason tothink that there are any terms missing from these equations. The only diﬃcultyis that we do not have the mathematical power today to analyze them except forvery small Reynolds numbers—that is, in the completely viscous case. That wehave written an equation does not remove from the ﬂow of ﬂuids its charm ormystery or its surprise.

If such variety is possible in a simple equation with only one parameter, howmuch more is possible with more complex equations! Perhaps the fundamentalequation that describes the swirling nebulae and the condensing, revolving, andexploding stars and galaxies is just a simple equation for the hydrodynamicbehavior of nearly pure hydrogen gas. Often, people in some unjustiﬁed fear ofphysics say you can’t write an equation for life. Well, perhaps we can. As a matterof fact, we very possibly already have the equation to a suﬃcient approximationwhen we write the equation of quantum mechanics:

Hψ = −

i

∂ψ∂t

.

We have just seen that the complexities of things can so easily and dramaticallyescape the simplicity of the equations which describe them. Unaware of the scopeof simple equations, man has often concluded that nothing short of God, notmere equations, is required to explain the complexities of the world.

41-11

We have written the equations of water ﬂow. From experiment, we ﬁnd a setof concepts and approximations to use to discuss the solution—vortex streets,turbulent wakes, boundary layers. When we have similar equations in a lessfamiliar situation, and one for which we cannot yet experiment, we try to solvethe equations in a primitive, halting, and confused way to try to determine whatnew qualitative features may come out, or what new qualitative forms are aconsequence of the equations. Our equations for the sun, for example, as a ball ofhydrogen gas, describe a sun without sunspots, without the rice-grain structureof the surface, without prominences, without coronas. Yet, all of these are reallyin the equations; we just haven’t found the way to get them out.

There are those who are going to be disappointed when no life is found onother planets. Not I—I want to be reminded and delighted and surprised onceagain, through interplanetary exploration, with the inﬁnite variety and noveltyof phenomena that can be generated from such simple principles. The test ofscience is its ability to predict. Had you never visited the earth, could you predictthe thunderstorms, the volcanos, the ocean waves, the auroras, and the colorfulsunset? A salutary lesson it will be when we learn of all that goes on on each ofthose dead planets—those eight or ten balls, each agglomerated from the samedust cloud and each obeying exactly the same laws of physics.

The next great era of awakening of human intellect may well produce a methodof understanding the qualitative content of equations. Today we cannot. Todaywe cannot see that the water ﬂow equations contain such things as the barberpole structure of turbulence that one sees between rotating cylinders. Today wecannot see whether Schrödinger’s equation contains frogs, musical composers, ormorality—or whether it does not. We cannot say whether something beyond itlike God is needed, or not. And so we can all hold strong opinions either way.

41-12

42

Curved Space

42-1 Curved spaces with two dimensionsAccording

to Newton everything attracts everything else with a force inverselyproportional to the square of the distance from it, and objects respond to forceswith accelerations proportional to the forces. They are Newton’s laws of universalgravitation and of motion. As you know, they account for the motions of balls,planets, satellites, galaxies, and so forth.

Einstein had a diﬀerent interpretation of the law of gravitation. Accordingto him, space and time—which must be put together as space-time—are curvednear heavy masses. And it is the attempt of things to go along「straight lines」in this curved space-time which makes them move the way they do. Now that isa complex idea—very complex. It is the idea we want to explain in this chapter.Our subject has three parts. One involves the eﬀects of gravitation. Anotherinvolves the ideas of space-time which we already studied. The third involves theidea of curved space-time. We will simplify our subject in the beginning by notworrying about gravity and by leaving out the time—discussing just curved space.We will talk later about the other parts, but we will concentrate now on the ideaof curved space—what is meant by curved space, and, more speciﬁcally, whatis meant by curved space in this application of Einstein. Now even that muchturns out to be somewhat diﬃcult in three dimensions. So we will ﬁrst reducethe problem still further and talk about what is meant by the words「curvedspace」in two dimensions.

In order to understand this idea of curved space in two dimensions you reallyhave to appreciate the limited point of view of the character who lives in such aspace. Suppose we imagine a bug with no eyes who lives on a plane, as shown inFig. 42-1. He can move only on the plane, and he has no way of knowing thatthere is anyway to discover any「outside world.」(He hasn’t got your imagination.)We are, of course, going to argue by analogy. We live in a three-dimensionalworld, and we don’t have any imagination about going oﬀ our three-dimensionalworld in a new direction; so we have to think the thing out by analogy. It is asthough we were bugs living on a plane, and there was a space in another direction.That’s why we will ﬁrst work with the bug, remembering that he must live onhis surface and can’t get out.

As another example of a bug living in two dimensions, let’s imagine one wholives on a sphere. We imagine that he can walk around on the surface of thesphere, as in Fig. 42-2 but that he can’t look「up,」or「down,」or「out.」

Now we want to consider still a third kind of creature. He is also a bug likethe others, and also lives on a plane, as our ﬁrst bug did, but this time the planeis peculiar. The temperature is diﬀerent at diﬀerent places. Also, the bug andany rulers he uses are all made of the same material which expands when it isheated. Whenever he puts a ruler somewhere to measure something the rulerexpands immediately to the proper length for the temperature at that place.Wherever he puts any object—himself, a ruler, a triangle, or anything—the thingstretches itself because of the thermal expansion. Everything is longer in the hotplaces than it is in the cold places, and everything has the same coeﬃcient ofexpansion. We will call the home of our third bug a「hot plate,」although wewill particularly want to think of a special kind of hot plate that is cold in thecenter and gets hotter as we go out toward the edges (Fig. 42-3).

Now we are going to imagine that our bugs begin to study geometry. Althoughwe imagine that they are blind so that they can’t see any「outside」world, they42-1

42-1 Curved spaces with two

dimensions

42-2 Curvature in three-dimensional

space

42-3 Our space is curved42-4 Geometry in space-time42-5 Gravity and the principle of

equivalence

42-6 The speed of clocks in a

gravitational ﬁeld

42-7 The curvature of space-time42-8 Motion in curved space-time42-9 Einstein’s theory of gravitation

Fig. 42-1. A bug on a plane surface.

Fig. 42-2. A bug on a sphere.

Fig. 42-3. A bug on a hot plate.

Fig. 42-4. Making a「straight」line on a

Fig. 42-5. Making a「straight line」on a

plane.

sphere.

can do a lot with their legs and feelers. They can draw lines, and they can makerulers, and measure oﬀ lengths. First, let’s suppose that they start with thesimplest idea in geometry. They learn how to make a straight line—deﬁned asthe shortest line between two points. Our ﬁrst bug—see Fig. 42-4—learns tomake very good lines. But what happens to the bug on the sphere? He drawshis straight line as the shortest distance—for him—between two points, as inFig. 42-5. It may look like a curve to us, but he has no way of getting oﬀ thesphere and ﬁnding out that there is「really」a shorter line. He just knows that ifhe tries any other path in his world it is always longer than his straight line. Sowe will let him have his straight line as the shortest arc between two points. (Itis, of course an arc of a great circle.)

Finally, our third bug—the one in Fig. 42-3—will also draw「straight lines」that look like curves to us. For instance, the shortest distance between A and Bin Fig. 42-6 would be on a curve like the one shown. Why? Because when his linecurves out toward the warmer parts of his hot plate, the rulers get longer (fromour omniscient point of view) and it takes fewer「yardsticks」laid end-to-end toget from A to B. So for him the line is straight—he has no way of knowing thatthere could be someone out in a strange three-dimensional world who would calla diﬀerent line「straight.」

We think you get the idea now that all the rest of the analysis will always befrom the point of view of the creatures on the particular surfaces and not fromour point of view. With that in mind let’s see what the rest of their geometrieslooks like. Let’s assume that the bugs have all learned how to make two linesintersect at right angles. (You can ﬁgure out how they could do it.) Then ourﬁrst bug (the one on the normal plane) ﬁnds an interesting fact. If he startsat the point A and makes a line 100 inches long, then makes a right angle andmarks oﬀ another 100 inches, then makes another right angle and goes another100 inches, then makes a third right angle and a fourth line 100 inches long, heends up right at the starting point as shown in Fig. 42-7(a). It is a property ofhis world—one of the facts of his「geometry.」

Then he discovers another interesting thing. If he makes a triangle—a ﬁgurewith three straight lines—the sum of the angles is equal to 180◦, that is, to thesum of two right angles. See Fig. 42-7(b).

Then he invents the circle. What’s a circle? A circle is made this way: Yourush oﬀ on straight lines in many many directions from a single point, and layout a lot of dots that are all the same distance from that point. See Fig. 42-7(c).(We have to be careful how we deﬁne these things because we’ve got to be able tomake the analogs for the other fellows.) Of course, its equivalent to the curve youcan make by swinging a ruler around a point. Anyway, our bug learns how tomake circles. Then one day he thinks of measuring the distance around a circle.He measures several circles and ﬁnds a neat relationship: The distance aroundis always the same number times the radius r (which is, of course, the distancefrom the center out to the curve). The circumference and the radius always havethe same ratio—approximately 6.283—independent of the size of the circle.Now let’s see what our other bugs have been ﬁnding out about their geometries.First, what happens to the bug on the sphere when he tries to make a「square」?42-2

Fig. 42-6. Making a「straight line」on the

hot plate.

Fig. 42-7. A square, triangle, and circle

in ﬂat space.

Fig. 42-8. Trying to make a「square」on

Fig. 42-9. Trying to make a「square」on

Fig. 42-10. On a sphere a「triangle」can

a sphere.

the hot plate.

have three 90◦ angles.

If he follows the prescription we gave above, he would probably think that theresult was hardly worth the trouble. He gets a ﬁgure like the one shown inFig. 42-8. His endpoint B isn’t on top of the starting point A. It doesn’t workout to a closed ﬁgure at all. Get a sphere and try it. A similar thing wouldhappen to our friend on the hot plate. If he lays out four straight lines of equallength—as measured with his expanding rulers—joined by right angles he gets apicture like the one in Fig. 42-9.

Now suppose that our bugs had each had their own Euclid who had told themwhat geometry「should」be like, and that they had checked him out roughlyby making crude measurements on a small scale. Then as they tried to makeaccurate squares on a larger scale they would discover that something was wrong.The point is, that just by geometrical measurements they would discover thatsomething was the matter with their space. We deﬁne a curved space to be aspace in which the geometry is not what we expect for a plane. The geometryof the bugs on the sphere or on the hot plate is the geometry of a curved space.The rules of Euclidean geometry fail. And it isn’t necessary to be able to liftyourself out of the plane in order to ﬁnd out that the world that you live in iscurved. It isn’t necessary to circumnavigate the globe in order to ﬁnd out that itis a ball. You can ﬁnd out that you live on a ball by laying out a square. If thesquare is very small you will need a lot of accuracy, but if the square is large themeasurement can be done more crudely.

Let’s take the case of a triangle on a plane. The sum of the angles is 180 degrees.Our friend on the sphere can ﬁnd triangles that are very peculiar. He can, forexample, ﬁnd triangles which have three right angles. Yes indeed! One is shownin Fig. 42-10. Suppose our bug starts at the north pole and makes a straightline all the way down to the equator. Then he makes a right angle and anotherperfect straight line the same length. Then he does it again. For the very speciallength he has chosen he gets right back to his starting point, and also meets theﬁrst line with a right angle. So there is no doubt that for him this triangle hasthree right angles, or 270 degrees in the sum. It turns out that for him the sum ofthe angles of the triangle is always greater than 180 degrees. In fact, the excess(for the special case shown, the extra 90 degrees) is proportional to how mucharea the triangle has. If a triangle on a sphere is very small, its angles add upto very nearly 180 degrees, only a little bit over. As the triangle gets bigger thediscrepancy goes up. The bugs on the hot plate would discover similar diﬃcultieswith their triangles.

Let’s look next at what our other bugs ﬁnd out about circles. They makecircles and measure their circumferences. For example, the bug on the spheremight make a circle like the one shown in Fig. 42-11. And he would discover thatthe circumference is less than 2π times the radius. (You can see that becausefrom the wisdom of our three-dimensional view it is obvious that what he callsthe「radius」is a curve which is longer than the true radius of the circle.) Supposethat the bug on the sphere had read Euclid, and decided to predict a radius bydividing the circumference C by 2π, taking

rpred = C2π

.

(42.1)

42-3

Fig. 42-11. Making a circle on a sphere.

Then he would ﬁnd that the measured radius was larger than the predicted radius.Pursuing the subject, he might deﬁne the diﬀerence to be the「excess radius,」and write

rmeas − rpred = rexcess,

(42.2)

and study how the excess radius eﬀect depended on the size of the circle.

Our bug on the hot plate would discover a similar phenomenon. Suppose hewas to draw a circle centered at the cold spot on the plate as in Fig. 42-12. Ifwe were to watch him as he makes the circle we would notice that his rulers areshort near the center and get longer as they are moved outward—although thebug doesn’t know it, of course. When he measures the circumference the ruler islong all the time, so he, too, ﬁnds out that the measured radius is longer thanthe predicted radius, C/2π. The hot-plate bug also ﬁnds an「excess radius eﬀect.」And again the size of the eﬀect depends on the radius of the circle.We will deﬁne a「curved space」as one in which these types of geometricalerrors occur: The sum of the angles of a triangle is diﬀerent from 180 degrees;the circumference of a circle divided by 2π is not equal to the radius; the rule formaking a square doesn’t give a closed ﬁgure. You can think of others.We have given two diﬀerent examples of curved space: the sphere and the hotplate. But it is interesting that if we choose the right temperature variation as afunction of distance on the hot plate, the two geometries will be exactly the same.It is rather amusing. We can make the bug on the hot plate get exactly the sameanswers as the bug on the ball. For those who like geometry and geometricalproblems we’ll tell you how it can be done. If you assume that the length of therulers (as determined by the temperature) goes in proportion to one plus someconstant times the square of the distance away from the origin, then you willﬁnd that the geometry of that hot plate is exactly the same in all details* as thegeometry of the sphere.

There are, of course, other kinds of geometry. We could ask about the geometryof a bug who lived on a pear, namely something which has a sharper curvature inone place and a weaker curvature in the other place, so that the excess in anglesin triangles is more severe when he makes little triangles in one part of his worldthan when he makes them in another part. In other words, the curvature of aspace can vary from place to place. That’s just a generalization of the idea. Itcan also be imitated by a suitable distribution of temperature on a hot plate.

We may also point out that the results could come out with the oppositekind of discrepancies. You could ﬁnd out, for example, that all triangles whenthey are made too large have the sum of their angles less than 180 degrees. Thatmay sound impossible, but it isn’t at all. First of all, we could have a hot platewith the temperature decreasing with the distance from the center. Then allthe eﬀects would be reversed. But we can also do it purely geometrically bylooking at the two-dimensional geometry of the surface of a saddle. Imagine asaddle-shaped surface like the one sketched in Fig. 42-13. Now draw a「circle」on the surface, deﬁned as the locus of all points the same distance from a center.This circle is a curve that oscillates up and down with a scallop eﬀect. So itscircumference is larger than you would expect from calculating 2πrmeas. So C/2πis now greater than rmeas. The「excess radius」would be negative.Spheres and pears and such are all surfaces of positive curvatures; and theothers are called surfaces of negative curvature. In general, a two-dimensionalworld will have a curvature which varies from place to place and may be positivein some places and negative in other places. In general, we mean by a curvedspace simply one in which the rules of Euclidean geometry break down with onesign of discrepancy or the other. The amount of curvature—deﬁned, say, by theexcess radius—may vary from place to place.

We might point out that, from our deﬁnition of curvature, a cylinder is,surprisingly enough, not curved.If a bug lived on a cylinder, as shown inFig. 42-14, he would ﬁnd out that triangles, squares, and circles would all havethe same behavior they have on a plane. This is easy to see, by just thinking

* Except for the one point at inﬁnity.

42-4

Fig. 42-12. Making a circle on the hot

plate.

Fig. 42-13. Making a「circle」on a saddle-

shaped surface.

Fig. 42-14. A two-dimensional space with

zero intrinsic curvature.

about how all the ﬁgures will look if the cylinder is unrolled onto a plane. Thenall the geometrical ﬁgures can be made to correspond exactly to the way theyare in a plane. So there is no way for a bug living on a cylinder (assuming thathe doesn’t go all the way around, but just makes local measurements) to discoverthat his space is curved. In our technical sense, then, we consider that his spaceis not curved. What we want to talk about is more precisely called intrinsiccurvature; that is, a curvature which can be found by measurements only in alocal region. (A cylinder has no intrinsic curvature.) This was the sense intendedby Einstein when he said that our space is curved. But we as yet only havedeﬁned a curved space in two dimensions; we must go onward to see what theidea might mean in three dimensions.

42-2 Curvature in three-dimensional spaceWe live in three-dimensional space and we are going to consider the idea thatthree-dimensional space is curved. You say,「But how can you imagine it beingbent in any direction?」Well, we can’t imagine space being bent in any directionbecause our imagination isn’t good enough. (Perhaps it’s just as well that wecan’t imagine too much, so that we don’t get too free of the real world.) But wecan still deﬁne a curvature without getting out of our three-dimensional world.All we have been talking about in two dimensions was simply an exercise to showhow we could get a deﬁnition of curvature which didn’t require that we be ableto「look in」from the outside.

We can determine whether our world is curved or not in a way quite analogousto the one used by the gentlemen who live on the sphere and on the hot plate.We may not be able to distinguish between two such cases but we certainly candistinguish those cases from the ﬂat space, the ordinary plane. How? Easyenough: We lay out a triangle and measure the angles. Or we make a great bigcircle and measure the circumference and the radius. Or we try to lay out someaccurate squares, or try to make a cube. In each case we test whether the laws ofgeometry work. If they don’t work, we say that our space is curved. If we lay outa big triangle and the sum of its angles exceeds 180 degrees, we can say our spaceis curved. Or if the measured radius of a circle is not equal to its circumferenceover 2π, we can say our space is curved.You will notice that in three dimensions the situation can be much morecomplicated than in two. At any one place in two dimensions there is a certainamount of curvature. But in three dimensions there can be several componentsto the curvature. If we lay out a triangle in some plane, we may get a diﬀerentanswer than if we orient the plane of the triangle in a diﬀerent way. Or takethe example of a circle. Suppose we draw a circle and measure the radius andit doesn’t check with C/2π so that there is some excess radius. Now we drawanother circle at right angles—as in Fig. 42-15. There’s no need for the excess tobe exactly the same for both circles. In fact, there might be a positive excess fora circle in one plane, and a defect (negative excess) for a circle in the other plane.Perhaps you are thinking of a better idea: Can’t we get around all of thesecomponents by using a sphere in three dimensions? We can specify a sphereby taking all the points that are the same distance from a given point in space.Then we can measure the surface area by laying out a ﬁne scale rectangular gridon the surface of the sphere and adding up all the bits of area. According toEuclid the total area A is supposed to be 4π times the square of the radius; so wedirectly by digging a hole to the center and measuring the distance. Again, wecan take the measured radius minus the predicted radius and call the diﬀerencethe radius excess,

can deﬁne a「predicted radius」aspA/4π. But we can also measure the radius

(cid:18)measured area

(cid:19)1/2

rexcess = rmeas −

4π

,

which would be a perfectly satisfactory measure of the curvature. It has the greatadvantage that it doesn’t depend upon how we orient a triangle or a circle.

42-5

Fig. 42-15. The excess radius may be dif-ferent for circles with diﬀerent orientations.

But the excess radius of a sphere also has a disadvantage; it doesn’t completelycharacterize the space. It gives what is called the mean curvature of the three-dimensional world, since there is an averaging eﬀect over the various curvatures.Since it is an average, however, it does not solve completely the problem of deﬁningthe geometry. If you know only this number you can’t predict all properties ofthe geometry of the space, because you can’t tell what would happen with circlesof diﬀerent orientation. The complete deﬁnition requires the speciﬁcation of six「curvature numbers」at each point. Of course the mathematicians know how towrite all those numbers. You can read someday in a mathematics book how towrite them all in a high-class and elegant form, but it is ﬁrst a good idea to knowin a rough way what it is that you are trying to write about. For most of ourpurposes the average curvature will be enough.*

42-3 Our space is curvedNow comes the main question. Is it true? That is, is the actual physicalthree-dimensional space we live in curved? Once we have enough imagination torealize the possibility that space might be curved, the human mind naturally getscurious about whether the real world is curved or not. People have made directgeometrical measurements to try to ﬁnd out, and haven’t found any deviations.On the other hand, by arguments about gravitation, Einstein discovered thatspace is curved, and we’d like to tell you what Einstein’s law is for the amountof curvature, and also tell you a little bit about how he found out about it.Einstein said that space is curved and that matter is the source of the curvature.(Matter is also the source of gravitation, so gravity is related to the curvature—but that will come later in the chapter.) Let us suppose, to make things a littleeasier, that the matter is distributed continuously with some density, which mayvary, however, as much as you want from place to place.† The rule that Einsteingave for the curvature is the following: If there is a region of space with matterin it and we take a sphere small enough that the density ρ of matter inside it iseﬀectively constant, then the radius excess for the sphere is proportional to themass inside the sphere. Using the deﬁnition of excess radius, we have

r

Radius excess = rmeas −

A4π

3c2 · M.= G

(42.3)

Here, G is the gravitational constant (of Newton’s theory), c is the velocity oflight, and M = 4πρr3/3 is the mass of the matter inside the sphere. This isEinstein’s law for the mean curvature of space.Suppose we take the earth as an example and forget that the density variesfrom point to point—so we won’t have to do any integrals. Suppose we wereto measure the surface of the earth very carefully, and then dig a hole to thecenter and measure the radius. From the surface area we could calculate thepredicted radius we would get from setting the area equal to 4πr2. When wecompared the predicted radius with the actual radius, we would ﬁnd that theactual radius exceeded the predicted radius by the amount given in Eq. (42.3).The constant G/3c2 is about 2.5×10−29 cm per gram, so for each gram of materialthe measured radius is oﬀ by 2.5 × 10−29 cm. Putting in the mass of the earth,which is about 6 × 1027 grams, it turns out that the earth has 1.5 millimetersmore radius than it should have for its surface area.‡ Doing the same calculationfor the sun, you ﬁnd that the sun’s radius is one-half a kilometer too long.

* We should mention one additional point for completeness.

If you want to carry thehot-plate model of curved space over into three dimensions you must imagine that the lengthof the ruler depends not only on where you put it, but also on which orientation the rulerhas when it is laid down. It is a generalization of the simple case in which the length of theruler depends on where it is, but is the same if set north-south, or east-west, or up-down. Thisgeneralization is needed if you want to represent a three-dimensional space with any arbitrarygeometry with such a model, although it happens not to be necessary for two dimensions.

† Nobody—not even Einstein—knows how to do it if mass comes concentrated at points.‡ Approximately, because the density is not independent of radius as we are assuming.

42-6

You should note that the law says that the average curvature above the surfacearea of the earth is zero. But that does not mean that all the components of thecurvature are zero. There may still be—and, in fact, there is—some curvatureabove the earth. For a circle in a plane there will be an excess radius of onesign for some orientations and of the opposite sign for other orientations. It justturns out that the average over a sphere is zero when there is no mass inside it.Incidentally, it turns out that there is a relation between the various componentsof the curvature and the variation of the average curvature from place to place.So if you know the average curvature everywhere, you can ﬁgure out the detailsof the curvature components at each place. The average curvature inside theearth varies with altitude, and this means that some curvature components arenonzero both inside the earth and outside. It is that curvature that we see as agravitational force.

Suppose we have a bug on a plane, and suppose that the「plane」has littlepimples in the surface. Wherever there is a pimple the bug would conclude thathis space had little local regions of curvature. We have the same thing in threedimensions. Wherever there is a lump of matter, our three-dimensional spacehas a local curvature—a kind of three-dimensional pimple.

If we make a lot of bumps on a plane there might be an overall curvaturebesides all the pimples—the surface might become like a ball.It would beinteresting to know whether our space has a net average curvature as well asthe local pimples due to the lumps of matter like the earth and the sun. Theastrophysicists have been trying to answer that question by making measurementsof galaxies at very large distances. For example, if the number of galaxies we seein a spherical shell at a large distance is diﬀerent from what we would expect fromour knowledge of the radius of the shell, we would have a measure of the excessradius of a tremendously large sphere. From such measurements it is hoped toﬁnd out whether our whole universe is ﬂat on the average, or round—whetherit is「closed,」like a sphere, or「open」like a plane. You may have heard aboutthe debates that are going on about this subject. There are debates because theastronomical measurements are still completely inconclusive; the experimentaldata are not precise enough to give a deﬁnite answer. Unfortunately, we don’thave the slightest idea about the overall curvature of our universe on a large scale.

42-4 Geometry in space-timeNow we have to talk about time. As you know from the special theory ofrelativity, measurements of space and measurements of time are interrelated. Andit would be kind of crazy to have something happening to the space, without thetime being involved in the same thing. You will remember that the measurementof time depends on the speed at which you move. For instance, if we watch a guygoing by in a spaceship we see that things happen more slowly for him than forus. Let’s say he takes oﬀ on a trip and returns in 100 seconds ﬂat by our watches;his watch might say that he had been gone for only 95 seconds. In comparisonwith ours, his watch—and all other processes, like his heart beat—have beenrunning slow.

Now let’s consider an interesting problem. Suppose you are the one in thespaceship. We ask you to start oﬀ at a given signal and return to your startingplace just in time to catch a later signal—at, say, exactly 100 seconds lateraccording to our clock. And you are also asked to make the trip in such a waythat your watch will show the longest possible elapsed time. How should youmove? You should stand still. If you move at all your watch will read less than100 sec when you get back.

Suppose, however, we change the problem a little. Suppose we ask you tostart at point A on a given signal and go to point B (both ﬁxed relative to us),and to do it in such a way that you arrive back just at the time of a secondsignal (say 100 seconds later according to our ﬁxed clock). Again you are askedto make the trip in the way that lets you arrive with the latest possible readingon your watch. How would you do it? For which path and schedule will your42-7

watch show the greatest elapsed time when you arrive? The answer is that youwill spend the longest time from your point of view if you make the trip by goingat a uniform speed along a straight line. Reason: Any extra motions and anyextra-high speeds will make your clock go slower. (Since the time deviationsdepend on the square of the velocity, what you lose by going extra fast at oneplace you can never make up by going extra slowly in another place.)The point of all this is that we can use the idea to deﬁne「a straight line」inspace-time. The analog of a straight line in space is for space-time a motion atuniform velocity in a constant direction.The curve of shortest distance in space corresponds in space-time not to thepath of shortest time, but to the one of longest time, because of the funny thingsthat happen to signs of the t-terms in relativity.「Straight-line」motion—theanalog of「uniform velocity along a straight line」—is then that motion whichtakes a watch from one place at one time to another place at another time in theway that gives the longest time reading for the watch. This will be our deﬁnitionfor the analog of a straight line in space-time.

42-5 Gravity and the principle of equivalenceNow we are ready to discuss the laws of gravitation. Einstein was tryingto generate a theory of gravitation that would ﬁt with the relativity theorythat he had developed earlier. He was struggling along until he latched ontoone important principle which guided him into getting the correct laws. Thatprinciple is based on the idea that when a thing is falling freely everything insideit seems weightless. For example, a satellite in orbit is falling freely in the earth’sgravity, and an astronaut in it feels weightless. This idea, when stated withgreater precision, is called Einstein’s principle of equivalence. It depends on thefact that all objects fall with exactly the same acceleration no matter what theirmass, or what they are made of. If we have a spaceship that is「coasting」—soit’s in a free fall—and there is a man inside, then the laws governing the fall ofthe man and the ship are the same. So if he puts himself in the middle of theship he will stay there. He doesn’t fall with respect to the ship. That’s what wemean when we say he is「weightless.」Now suppose you are in a rocket ship which is accelerating. Accelerating withrespect to what? Let’s just say that its engines are on and generating a thrust sothat it is not coasting in a free fall. Also imagine that you are way out in emptyspace so that there are practically no gravitational forces on the ship. If the shipis accelerating with「1 g」you will be able to stand on the「ﬂoor」and will feelyour normal weight. Also if you let go of a ball, it will「fall」toward the ﬂoor.Why? Because the ship is accelerating「upward,」but the ball has no forces onit, so it will not accelerate; it will get left behind. Inside the ship the ball willappear to have a downward acceleration of「1 g.」

Now let’s compare that with the situation in a spaceship sitting at rest onthe surface of the earth. Everything is the same! You would be pressed towardthe ﬂoor, a ball would fall with an acceleration of 1 g, and so on. In fact, howcould you tell inside a space ship whether you are sitting on the earth or areaccelerating in free space? According to Einstein’s equivalence principle there isno way to tell if you only make measurements of what happens to things inside!To be strictly correct, that is true only for one point inside the ship. Thegravitational ﬁeld of the earth is not precisely uniform, so a freely falling ball hasa slightly diﬀerent acceleration at diﬀerent places—the direction changes and themagnitude changes. But if we imagine a strictly uniform gravitational ﬁeld, it iscompletely imitated in every respect by a system with a constant acceleration.That is the basis of the principle of equivalence.

42-6 The speed of clocks in a gravitational ﬁeldNow we want to use the principle of equivalence for ﬁguring out a strange thingthat happens in a gravitational ﬁeld. We’ll show you something that happens42-8

in a rocket ship which you probably wouldn’t have expected to happen in agravitational ﬁeld. Suppose we put a clock at the「head」of the rocket ship—thatis, at the「front」end—and we put another identical clock at the「tail,」as inFig. 42-16. Let’s call the two clocks A and B. If we compare these two clockswhen the ship is accelerating, the clock at the head seems to run fast relativeto the one at the tail. To see that, imagine that the front clock emits a ﬂashof light each second, and that you are sitting at the tail comparing the arrivalof the light ﬂashes with the ticks of clock B. Let’s say that the rocket is in theposition a of Fig. 42-17 when clock A emits a ﬂash, and at the position b whenthe ﬂash arrives at clock B. Later on the ship will be at position c when theclock A emits its next ﬂash, and at position d when you see it arrive at clock B.The ﬁrst ﬂash travels the distance L1 and the second ﬂash travels the shorterdistance L2. It is a shorter distance because the ship is accelerating and has ahigher speed at the time of the second ﬂash. You can see, then, that if the twoﬂashes were emitted from clock A one second apart, they would arrive at clock Bwith a separation somewhat less than one second, since the second ﬂash doesn’tspend as much time on the way. The same thing will also happen for all the laterﬂashes. So if you were sitting in the tail you would conclude that clock A wasrunning faster than clock B. If you were to do the same thing in reverse—lettingclock B emit light and observing it at clock A—you would conclude that B wasrunning slower than A. Everything ﬁts together and there is nothing mysteriousabout it all.

But now let’s think of the rocket ship at rest in the earth’s gravity. The samething happens. If you sit on the ﬂoor with one clock and watch another one whichis sitting on a high shelf, it will appear to run faster than the one on the ﬂoor!You say,「But that is wrong. The times should be the same. With no accelerationthere’s no reason for the clocks to appear to be out of step.」But they must ifthe principle of equivalence is right. And Einstein insisted that the principle wasright, and went courageously and correctly ahead. He proposed that clocks atdiﬀerent places in a gravitational ﬁeld must appear to run at diﬀerent speeds.But if one always appears to be running at a diﬀerent speed with respect to theother, then so far as the ﬁrst is concerned the other is running at a diﬀerent rate.But now you see we have the analog for clocks of the hot ruler we were talkingabout earlier, when we had the bug on a hot plate. We imagined that rulers andbugs and everything changed lengths in the same way at various temperatures sothey could never tell that their measuring sticks were changing as they movedaround on the hot plate. It’s the same with clocks in a gravitational ﬁeld. Everyclock we put at a higher level is seen to go faster. Heartbeats go faster, allprocesses run faster.

If they didn’t you would be able to tell the diﬀerence between a gravitationalﬁeld and an accelerating reference system. The idea that time can vary from placeto place is a diﬃcult one, but it is the idea Einstein used, and it is correct—believeit or not.

Using the principle of equivalence we can ﬁgure out how much the speedof a clock changes with height in a gravitational ﬁeld. We just work out theapparent discrepancy between the two clocks in the accelerating rocket ship. Theeasiest way to do this is to use the result we found in Chapter 34 of Vol. I forthe Doppler eﬀect. There, we found—see Eq. (34.14)—that if v is the relativevelocity of a source and a receiver, the received frequency ω is related to theemitted frequency ω0 by

ω = ω0

1 + v/c

p1 − v2/c2 .

(42.4)

Fig. 42-16. An accelerating rocket ship

with two clocks.

Now if we think of the accelerating rocket ship in Fig. 42-17 the emitter andreceiver are moving with equal velocities at any one instant. But in the time thatit takes the light signals to go from clock A to clock B the ship has accelerated. Ithas, in fact, picked up the additional velocity gt, where g is the acceleration andt is time it takes light to travel the distance H from A to B. This time is verynearly H/c. So when the signals arrive at B, the ship has increased its velocity42-9

Fig. 42-17. A clock at the head of an ac-celerating rocket ship appears to run fasterthan a clock at the tail.

by gH/c. The receiver always has this velocity with respect to the emitter at theinstant the signal left it. So this is the velocity we should use in the Dopplershift formula, Eq. (42.4). Assuming that the acceleration and the length of theship are small enough that this velocity is much smaller than c, we can neglectthe term in v2/c2. We have that

(cid:18)

(cid:19)

.

ω = ω0

1 + gHc2

So for the two clocks in the spaceship we have the relation

(Rate at the receiver) = (Rate of emission)

(42.5)

(42.6)

(cid:19)

,

(cid:18)

1 + gHc2

where H is the height of the emitter above the receiver.

From the equivalence principle the same result must hold for two clocksseparated by the height H in a gravitational ﬁeld with the free fall acceleration g.This is such an important idea we would like to demonstrate that it alsofollows from another law of physics—from the conservation of energy. We knowthat the gravitational force on an object is proportional to its mass M, which isrelated to its total internal energy E by M = E/c2. For instance, the masses ofnuclei determined from the energies of nuclear reactions which transmute onenucleus into another agree with the masses obtained from atomic weights.Now think of an atom which has a lowest energy state of total energy E0 anda higher energy state E1, and which can go from the state E1 to the state E0 byemitting light. The frequency ω of the light will be given by

ω = E1 − E0.

(42.7)Now suppose we have such an atom in the state E1 sitting on the ﬂoor, andwe carry it from the ﬂoor to the height H. To do that we must do some work incarrying the mass m1 = E1/c2 up against the gravitational force. The amountof work done is

(42.8)Then we let the atom emit a photon and go into the lower energy state E0.Afterward we carry the atom back to the ﬂoor. On the return trip the massis E0/c2; we get back the energy

E1c2 gH.

E0c2 gH,

so we have done a net amount of work equal to∆U = E1 − E0

gH.

c2

(42.9)

(42.10)

When the atom emitted the photon it gave up the energy E1 − E0. Nowsuppose that the photon happened to go down to the ﬂoor and be absorbed.How much energy would it deliver there? You might at ﬁrst think that it woulddeliver just the energy E1 − E0. But that can’t be right if energy is conserved,as you can see from the following argument. We started with the energy E1 atthe ﬂoor. When we ﬁnish, the energy at the ﬂoor level is the energy E0 of theatom in its lower state plus the energy Eph received from the photon. In themeantime we have had to supply the additional energy ∆U of Eq. (42.10). Ifenergy is conserved, the energy we end up with at the ﬂoor must be greater thanwe started with by just the work we have done. Namely, we must have that

or

Eph + E0 = E1 + ∆U,

Eph = (E1 − E0) + ∆U.

(42.11)

42-10

It must be that the photon does not arrive at the ﬂoor with just the energy E1−E0it started with, but with a little more energy. Otherwise some energy would havebeen lost. If we substitute in Eq. (42.11) the ∆U we got in Eq. (42.10) we getthat the photon arrives at the ﬂoor with the energy

Eph = (E1 − E0)

1 + gHc2

.

(42.12)

But a photon of energy Eph has the frequency ω = Eph/. Calling the frequencyof the emitted photon ω0—which is by Eq. (42.7) equal to (E1 − E0)/—ourresult in Eq. (42.12) gives again the relation of (42.5) between the frequency ofthe photon when it is absorbed on the ﬂoor and the frequency with which it wasemitted.

The same result can be obtained in still another way. A photon of frequency ω0has the energy E0 = ω0. Since the energy E0 has the gravitational mass E0/c2the photon has a mass (not rest mass) ω0/c2, and is「attracted」by the earth. Infalling the distance H it will gain an additional energy (ω0/c2)gH, so it arriveswith the energy

(cid:18)

(cid:19)

(cid:18)

(cid:19)

.

E = ω0

1 + gHc2

But its frequency after the fall is E/, giving again the result in Eq. (42.5). Ourideas about relativity, quantum physics, and energy conservation all ﬁt togetheronly if Einstein’s predictions about clocks in a gravitational ﬁeld are right. Thefrequency changes we are talking about are normally very small. For instance, foran altitude diﬀerence of 20 meters at the earth’s surface the frequency diﬀerenceis only about two parts in 1015. However, just such a change has recently beenfound experimentally using the Mössbauer eﬀect.* Einstein was perfectly correct.

42-7 The curvature of space-timeNow we want to relate what we have just been talking about to the idea ofcurved space-time. We have already pointed out that if the time goes at diﬀerentrates in diﬀerent places, it is analogous to the curved space of the hot plate. Butit is more than an analogy; it means that space-time is curved. Let’s try to dosome geometry in space-time. That may at ﬁrst sound peculiar, but we haveoften made diagrams of space-time with distance plotted along one axis and timealong the other. Suppose we try to make a rectangle in space-time. We begin byplotting a graph of height H versus t as in Fig. 42-18(a). To make the base ofour rectangle we take an object which is at rest at the height H1 and follow itsworld line for 100 seconds. We get the line BD in part (b) of the ﬁgure which isparallel to the t-axis. Now let’s take another object which is 100 feet above theﬁrst one at t = 0. It starts at the point A in Fig. 42-18(c). Now we follow itsworld line for 100 seconds as measured by a clock at A. The object goes from Ato C, as shown in part (d) of the ﬁgure. But notice that since time goes at adiﬀerent rate at the two heights—we are assuming that there is a gravitationalﬁeld—the two points C and D are not simultaneous. If we try to complete thesquare by drawing a line to the point C0 which is 100 feet above D at the sametime, as in Fig. 42-18(e), the pieces don’t ﬁt. And that’s what we mean when wesay that space-time is curved.

42-8 Motion in curved space-timeLet’s consider an interesting little puzzle. We have two identical clocks, Aand B, sitting together on the surface of the earth as in Fig. 42-19. Now we liftclock A to some height H, hold it there awhile, and return it to the ground sothat it arrives at just the instant when clock B has advanced by 100 seconds.Then clock A will read something like 107 seconds, because it was running fasterwhen it was up in the air. Now here is the puzzle. How should we move clock A

* R. V. Pound and G. A. Rebka, Jr., Physical Review Letters Vol. 4, p. 337 (1960).

42-11

Fig. 42-18. Trying to make a rectangle

in space-time.

so that it reads the latest possible time—always assuming that it returns whenB reads 100 seconds? You say,「That’s easy. Just take A as high as you can.Then it will run as fast as possible, and be the latest when you return.」Wrong.You forgot something—we’ve only got 100 seconds to go up and back. If we govery high, we have to go very fast to get there and back in 100 seconds. Andyou mustn’t forget the eﬀect of special relativity which causes moving clocks to

slow down by the factorp1 − v2/c2. This relativity eﬀect works in the direction

of making clock A read less time than clock B. You see that we have a kind ofgame. If we stand still with clock A we get 100 seconds. If we go up slowly to asmall height and come down slowly we can get a little more than 100 seconds. Ifwe go a little higher, maybe we can gain a little more. But if we go too high wehave to move fast to get there, and we may slow down the clock enough that weend up with less than 100 seconds. What program of height versus time—howhigh to go and with what speed to get there, carefully adjusted to bring us backto clock B when it has increased by 100 seconds—will give us the largest possibletime reading on clock A?Answer: Find out how fast you have to throw a ball up into the air so thatit will fall back to earth in exactly 100 seconds. The ball’s motion—rising fast,slowing down, stopping, and coming back down—is exactly the right motion tomake the time the maximum on a wrist watch strapped to the ball.

Now consider a slightly diﬀerent game. We have two points A and B bothon the earth’s surface at some distance from one another. We play the samegame that we did earlier to ﬁnd what we call the straight line. We ask howwe should go from A to B so that the time on our moving watch will be thelongest—assuming we start at A on a given signal and arrive at B on anothersignal at B which we will say is 100 seconds later by a ﬁxed clock. Now you say,「Well we found out before that the thing to do is to coast along a straight line ata uniform speed chosen so that we arrive at B exactly 100 seconds later. If wedon’t go along a straight line it takes more speed, and our watch is slowed down.」But wait! That was before we took gravity into account. Isn’t it better to curveupward a little bit and then come down? Then during part of the time we arehigher up and our watch will run a little faster? It is, indeed. If you solve themathematical problem of adjusting the curve of the motion so that the elapsedtime of the moving watch is the most it can possibly be, you will ﬁnd that themotion is a parabola—the same curve followed by something that moves on afree ballistic path in the gravitational ﬁeld, as in Fig. 42-19. Therefore the lawof motion in a gravitational ﬁeld can also be stated: An object always movesfrom one place to another so that a clock carried on it gives a longer time than itwould on any other possible trajectory—with, of course, the same starting andﬁnishing conditions. The time measured by a moving clock is often called its「proper time.」In free fall, the trajectory makes the proper time of an object amaximum.

Let’s see how this all works out. We begin with Eq. (42.5) which says that

the excess rate of the moving watch is

ω0gH

c2

.

(42.13)

Besides this, we have to remember that there is a correction of the opposite signfor the speed. For this eﬀect we know that

p1 − v2/c2.

ω = ω0

Although the principle is valid for any speed, we take an example in which thespeeds are always much less than c. Then we can write this equation as

ω = ω0(1 − v2/2c2),

and the defect in the rate of our clock is− ω0

v22c2 .

(42.14)

42-12

Fig. 42-19.

In a uniform gravitationalﬁeld the trajectory with the maximum propertime for a ﬁxed elapsed time is a parabola.

Combining the two terms in (42.13) and (42.14) we have that

∆ω = ω0c2

(cid:19)

.

(cid:19)(cid:21)

(cid:18)gH − v22(cid:18) gHc2 − v22c2Z (cid:18)(cid:19)

gH − v22

dt,

(cid:20)

1c2

(42.15)

(42.17)

Such a frequency shift of our moving clock means that if we measure a time dton a ﬁxed clock, the moving clock will register the time

1 +

dt

,

(42.16)

The total time excess over the trajectory is the integral of the extra term withrespect to time, namely

which is supposed to be a maximum.The term gH is just the gravitational potential φ. Suppose we multiply thewhole thing by a constant factor −mc2, where m is the mass of the object. Theconstant won’t change the condition for the maximum, but the minus sign willjust change the maximum to a minimum. Equation (42.16) then says that the

object will move so thatZ (cid:18) mv2

(cid:19)

2 − mφ

dt = a minimum.

(42.18)

But now the integrand is just the diﬀerence of the kinetic and potential energies.And if you look in Chapter 19 of Volume II you will see that when we discussedthe principle of least action we showed that Newton’s laws for an object in anypotential could be written exactly in the form of Eq. (42.18).

42-9 Einstein’s theory of gravitationEinstein’s form of the equations of motion—that the proper time should bea maximum in curved space-time—gives the same results as Newton’s laws forlow velocities. As he was circling around the earth, Gordon Cooper’s watch wasreading later than it would have in any other path you could have imagined forhis satellite.*

So the law of gravitation can be stated in terms of the ideas of the geometry ofspace-time in this remarkable way. The particles always take the longest propertime—in space-time a quantity analogous to the「shortest distance.」That’s thelaw of motion in a gravitational ﬁeld. The great advantage of putting it this wayis that the law doesn’t depend on any coordinates, or any other way of deﬁningthe situation.

Now let’s summarize what we have done. We have given you two laws for

gravity:

(1) How the geometry of space-time changes when matter is present—namely,that the curvature expressed in terms of the excess radius is proportionalto the mass inside a sphere, Eq. (42.3).

(2) How objects move if there are only gravitational forces—namely, thatobjects move so that their proper time between two end conditions is amaximum.

Those two laws correspond to similar pairs of laws we have seen earlier. Weoriginally described motion in a gravitational ﬁeld in terms of Newton’s inversesquare law of gravitation and his laws of motion. Now laws (1) and (2) take

* Strictly speaking it is only a local maximum. We should have said that the proper time islarger than for any nearby path. For example, the proper time on an elliptical orbit around theearth need not be longer than on a ballistic path of an object which is shot to a great heightand falls back down.

42-13

their places. Our new pair of laws also correspond to what we have seen inelectrodynamics. There we had our law—the set of Maxwell’s equations—whichdetermines the ﬁelds produced by charges. It tells how the character of「space」is changed by the presence of charged matter, which is what law (1) does forgravity.In addition, we had a law about how particles move in the givenﬁelds—d(mv)/dt = q(E + v × B). This, for gravity, is done by law (2).In the laws (1) and (2) you have a precise statement of Einstein’s theoryof gravitation—although you will usually ﬁnd it stated in a more complicatedmathematical form. We should, however, make one further addition. Just as timescales change from place to place in a gravitational ﬁeld, so do also the lengthscales. Rulers change lengths as you move around. It is impossible with spaceand time so intimately mixed to have something happen with time that isn’t insome way reﬂected in space. Take even the simplest example: You are ridingpast the earth. What is「time」from your point of view is partly space from ourpoint of view. So there must also be changes in space. It is the entire space-timewhich is distorted by the presence of matter, and this is more complicated than achange only in time scale. However, the rule that we gave in Eq. (42.3) is enoughto determine completely all the laws of gravitation, provided that it is understoodthat this rule about the curvature of space applies not only from one man’spoint of view but is true for everybody. Somebody riding by a mass of materialsees a diﬀerent mass content because of the kinetic energy he calculates for itsmotion past him, and he must include the mass corresponding to that energy.The theory must be arranged so that everybody—no matter how he moves—will,when he draws a sphere, ﬁnd that the excess radius is G/3c2 times the totalmass (or, better, G/3c4 times the total energy content) inside the sphere. Thatthis law—law (1)—should be true in any moving system is one of the great lawsof gravitation, called Einstein’s ﬁeld equation. The other great law is (2)—thatthings must move so that the proper time is a maximum—and is called Einstein’sequation of motion.To write these laws in a complete algebraic form, to compare them withNewton’s laws, or to relate them to electrodynamics is diﬃcult mathematically.But it is the way our most complete laws of the physics of gravity look today.Although they gave a result in agreement with Newton’s mechanics for thesimple example we considered, they do not always do so. The three discrepanciesﬁrst derived by Einstein have been experimentally conﬁrmed: The orbit ofMercury is not a ﬁxed ellipse; starlight passing near the sun is deﬂected twiceas much as you would think; and the rates of clocks depend on their location ina gravitational ﬁeld. Whenever the predictions of Einstein have been found todiﬀer from the ideas of Newtonian mechanics Nature has chosen Einstein’s.

