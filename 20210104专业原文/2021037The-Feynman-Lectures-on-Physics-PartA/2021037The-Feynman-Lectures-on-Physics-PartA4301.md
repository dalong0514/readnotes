Diffusion

43-1 Collisions between molecules We have considered so far only the molecular motions in a gas which is in thermal equilibrium. We want now to discuss what happens when things are near, but not exactly in, equilibrium. In a situation far from equilibrium, things are extremely complicated, but in a situation very close to equilibrium we can easily work out what happens. To see what happens, we must, however, return to the kinetic theory. Statistical mechanics and thermodynamics deal with the equilibrium situation, but away from equilibrium we can only analyze what occurs atom by atom, so to speak.

As a simple example of a nonequilibrium circumstance, we shall consider the diﬀusion of ions in a gas. Suppose that in a gas there is a relatively small concentration of ions—electrically charged molecules. If we put an electric ﬁeld on the gas, then each ion will have a force on it which is diﬀerent from the forces on the neutral molecules of the gas. If there were no other molecules present, an ion would have a constant acceleration until it reached the wall of the container. But because of the presence of the other molecules, it cannot do that; its velocity increases only until it collides with a molecule and loses its momentum. It starts again to pick up more speed, but then it loses its momentum again. The net eﬀect is that an ion works its way along an erratic path, but with a net motion in the direction of the electric force. We shall see that the ion has an average「drift」with a mean speed which is proportional to the electric ﬁeld—the stronger the ﬁeld, the faster it goes. While the ﬁeld is on, and while the ion is moving along, it is, of course, not in thermal equilibrium, it is trying to get to equilibrium, which is to be sitting at the end of the container. By means of the kinetic theory we can compute the drift velocity.

It turns out that with our present mathematical abilities we cannot really compute precisely what will happen, but we can obtain approximate results

43-1

which exhibit all the essential features. We can ﬁnd out how things will vary with pressure, with temperature, and so on, but it will not be possible to get precisely the correct numerical factors in front of all the terms. We shall, therefore, in our derivations, not worry about the precise value of numerical factors. They can be obtained only by a very much more sophisticated mathematical treatment.

Before we consider what happens in nonequilibrium situations, we shall need to look a little closer at what goes on in a gas in thermal equilibrium. We shall need to know, for example, what the average time between successive collisions of a molecule is.

Any molecule experiences a sequence of collisions with other molecules—in a random way, of course. A particular molecule will, in a long period of time T, have a certain number, N, of hits. If we double the length of time, there will be twice as many hits. So the number of collisions is proportional to the time T. We would like to write it this way:

N = T /τ.

(43.1) We have written the constant of proportionality as 1/τ, where τ will have the dimensions of a time. The constant τ is the average time between collisions. Suppose, for example, that in an hour there are 60 collisions; then τ is one minute. We would say that τ (one minute) is the average time between the collisions. We may often wish to ask the following question:「What is the chance that a molecule will experience a collision during the next small interval of time dt?」The answer, we may intuitively understand, is dt/τ. But let us try to make a more convincing argument. Suppose that there were a very large number N of molecules. How many will have collisions in the next interval of time dt? If there is equilibrium, nothing is changing on the average with time. So N molecules waiting the time dt will have the same number of collisions as one molecule waiting for the time N dt. That number we know is N dt/τ. So the number of hits of N molecules is N dt/τ in a time dt, and the chance, or probability, of a hit for any one molecule is just 1/N as large, or (1/N)(N dt/τ) = dt/τ, as we guessed above. That is to say, the fraction of the molecules which will suﬀer a collision in the time dt is dt/τ. To take an example, if τ is one minute, then in one second the fraction of particles which will suﬀer collisions is 1/60. What this means, of course, is that 1/60 of the molecules happen to be close enough to what they are going to hit next that their collisions will occur in the next second. When we say that τ, the mean time between collisions, is one minute, we do not mean that all the collisions will occur at times separated by exactly one

43-2

minute. A particular particle does not have a collision, wait one minute, and then have another collision. The times between successive collisions are quite variable. We will not need it for our later work here, but we may make a small diversion to answer the question:「What are the times between collisions?」We know that for the case above, the average time is one minute, but we might like to know, for example, what is the chance that we get no collision for two minutes?

We shall ﬁnd the answer to the general question:「What is the probability that a molecule will go for a time t without having a collision?」At some arbitrary instant—that we call t = 0—we begin to watch a particular molecule. What is the chance that it gets by until t without colliding with another molecule? To compute the probability, we observe what is happening to all N0 molecules in a container. After we have waited a time t, some of them will have had collisions. We let N(t) be the number that have not had collisions up to the time t. N(t) is, of course, less than N0. We can ﬁnd N(t) because we know how it changes with time. If we know that N(t) molecules have got by until t, then N(t + dt), the number which get by until t + dt, is less than N(t) by the number that have collisions in dt. The number that collide in dt we have written above in terms of the mean time τ as dN = N(t) dt/τ. We have the equation

N(t + dt) = N(t) − N(t) dt τ

.

(43.2)

The quantity on the left-hand side, N(t + dt), can be written, according to the deﬁnitions of calculus, as N(t) + (dN/dt) dt. Making this substitution, Eq. (43.2) yields

.

(43.3)

dN(t)

dt

= − N(t)

τ

The number that are being lost in the interval dt is proportional to the number that are present, and inversely proportional to the mean life τ. Equation (43.3) is easily integrated if we rewrite it as dN(t) N(t) = − dt

(43.4)

.

τ

Each side is a perfect diﬀerential, so the integral is

ln N(t) = −t/τ + (a constant),

(43.5)

43-3

which says the same thing as

P(t) = e−t/τ .

N(t) = N0e−t/τ .

N(t) = (constant)e−t/τ .

(43.6) We know that the constant must be just N0, the total number of molecules present, since all of them start at t = 0 to wait for their「next」collision. We can write our result as (43.7) If we wish the probability of no collision, P(t), we can get it by dividing N(t) by N0, so (43.8) Our result is: the probability that a particular molecule survives a time t without a collision is e−t/τ, where τ is the mean time between collisions. The probability starts out at 1 (or certainty) for t = 0, and gets less as t gets bigger and bigger. The probability that the molecule avoids a collision for a time equal to τ is e−1 ≈ 0.37. The chance is less than one-half that it will have a greater than average time between collisions. That is all right, because there are enough molecules which go collision-free for times much longer than the mean time before colliding, so that the average time can still be τ. We originally deﬁned τ as the average time between collisions. The result we have obtained in Eq. (43.7) also says that the mean time from an arbitrary starting instant to the next collision is also τ. We can demonstrate this somewhat surprising fact in the following way. The number of molecules which experience their next collision in the interval dt at the time t after an arbitrarily chosen starting time is N(t) dt/τ. Their「time until the next collision」is, of course, just t. The「average time until the next collision」is obtained in the usual way:

Z ∞

0

Average time until the next collision = 1 N0

N(t) dt

τ

.

t

Using N(t) obtained in (43.7) and evaluating the integral, we ﬁnd indeed that τ is the average time from any instant until the next collision.

43-2 The mean free path Another way of describing the molecular collisions is to talk not about the time between collisions, but about how far the particle moves between collisions. If

43-4

we say that the average time between collisions is τ, and that the molecules have a mean velocity v, we can expect that the average distance between collisions, which we shall call l, is just the product of τ and v. This distance between collisions is usually called the mean free path:

Mean free path l = τ v.

(43.9) In this chapter we shall be a little careless about what kind of average we mean in any particular case. The various possible averages—the mean, the root- mean-square, etc.—are all nearly equal and diﬀer by factors which are near to one. Since a detailed analysis is required to obtain the correct numerical factors anyway, we need not worry about which average is required at any particular point. We may also warn the reader that the algebraic symbols we are using for some of the physical quantities (e.g., l for the mean free path) do not follow a generally accepted convention, mainly because there is no general agreement. Just as the chance that a molecule will have a collision in a short time dt is equal to dt/τ, the chance that it will have a collision in going a distance dx is dx/l. Following the same line of argument used above, the reader can show that the probability that a molecule will go at least the distance x before having its next collision is e−x/l. The average distance a molecule goes before colliding with another molecule— the mean free path l—will depend on how many molecules there are around and on the「size」of the molecules, i.e., how big a target they represent. The eﬀective「size」of a target in a collision we usually describe by a「collision cross section,」the same idea that is used in nuclear physics, or in light-scattering problems.

Consider a moving particle which travels a distance dx through a gas which has n0 scatterers (molecules) per unit volume (Fig. 43-1). If we look at each unit

Fig. 43-1. Collision cross section.

43-5

of area perpendicular to the direction of motion of our selected particle, we will ﬁnd there n0 dx molecules. If each one presents an eﬀective collision area or, as it is usually called,「collision cross section,」σc, then the total area covered by the scatterers is σcn0 dx. By「collision cross section」we mean the area within which the center of our particle must be located if it is to collide with a particular molecule. If molecules were little spheres (a classical picture) we would expect that σc = π(r1 + r2)2, where r1 and r2 are the radii of the two colliding objects. The chance that our particle will have a collision is the ratio of the area covered by scattering molecules to the total area, which we have taken to be one. So the probability of a collision in going a distance dx is just σcn0 dx:

Chance of a collision in dx = σcn0 dx.

(43.10)

We have seen above that the chance of a collision in dx can also be written in terms of the mean free path l as dx/l. Comparing this with (43.10), we can relate the mean free path to the collision cross section:

1 l

= σcn0,

which is easier to remember if we write it as

σcn0l = 1.

(43.11)

(43.12)

This formula can be thought of as saying that there should be one collision, on the average, when the particle goes through a distance l in which the scattering molecules could just cover the total area. In a cylindrical volume of length l and a base of unit area, there are n0l scatterers; if each one has an area σc the total area covered is n0lσc, which is just one unit of area. The whole area is not covered, of course, because some molecules are partly hidden behind others. That is why some molecules go farther than l before having a collision. It is only on the average that the molecules have a collision by the time they go the distance l. From measurements of the mean free path l we can determine the scattering cross section σc, and compare the result with calculations based on a detailed theory of atomic structure. But that is a diﬀerent subject! So we return to the problem of nonequilibrium states.

43-6

43-3 The drift speed We want to describe what happens to a molecule, or several molecules, which are diﬀerent in some way from the large majority of the molecules in a gas. We shall refer to the「majority」molecules as the「background」molecules, and we shall call the molecules which are diﬀerent from the background molecules「special」molecules or, for short, the S-molecules. A molecule could be special for any number of reasons: It might be heavier than the background molecules. It might be a diﬀerent chemical. It might have an electric charge—i.e., be an ion in a background of uncharged molecules. Because of their diﬀerent masses or charges the S-molecules may have forces on them which are diﬀerent from the forces on the background molecules. By considering what happens to these S-molecules we can understand the basic eﬀects which come into play in a similar way in many diﬀerent phenomena. To list a few: the diﬀusion of gases, electric currents in batteries, sedimentation, centrifugal separation, etc.

We begin by concentrating on the basic process: an S-molecule in a back- ground gas is acted on by some speciﬁc force F (which might be, e.g., gravitational or electrical) and in addition by the not-so-speciﬁc forces due to collisions with the background molecules. We would like to describe the general behavior of the S-molecule. What happens to it, in detail, is that it darts around hither and yon as it collides over and over again with other molecules. But if we watch it carefully we see that it does make some net progress in the direction of the force F . We say that there is a drift, superposed on its random motion. We would like to know what the speed of its drift is—its drift velocity—due to the force F .

If we start to observe an S-molecule at some instant we may expect that it is somewhere between two collisions. In addition to the velocity it was left with after its last collision it is picking up some velocity component due to the force F . In a short time (on the average, in a time τ) it will experience a collision and start out on a new piece of its trajectory. It will have a new starting velocity, but the same acceleration from F .

To keep things simple for the moment, we shall suppose that after each collision our S-molecule gets a completely「fresh」start. That is, that it keeps no remembrance of its past acceleration by F . This might be a reasonable assumption if our S-molecule were much lighter than the background molecules, but it is certainly not valid in general. We shall discuss later an improved assumption. For the moment, then, our assumption is that the S-molecule leaves each collision with a velocity which may be in any direction with equal likelihood. The

43-7

starting velocity will take it equally in all directions and will not contribute to any net motion, so we shall not worry further about its initial velocity after a collision. In addition to its random motion, each S-molecule will have, at any moment, an additional velocity in the direction of the force F , which it has picked up since its last collision. What is the average value of this part of the velocity? It is just the acceleration F /m (where m is the mass of the S-molecule) times the average time since the last collision. Now the average time since the last collision must be the same as the average time until the next collision, which we have called τ, above. The average velocity from F , of course, is just what is called the drift velocity, so we have the relation

vdrift = F τ m

.

(43.13)

This basic relation is the heart of our subject. There may be some complication in determining what τ is, but the basic process is deﬁned by Eq. (43.13). You will notice that the drift velocity is proportional to the force. There is, unfortunately, no generally used name for the constant of proportionality. Diﬀerent names have been used for each diﬀerent kind of force. If in an electrical problem the force is written as the charge times the electric ﬁeld, F = qE, then the constant of proportionality between the velocity and the electric ﬁeld E is usually called the「mobility.」In spite of the possibility of some confusion, we shall use the term mobility for the ratio of the drift velocity to the force for any force. We write (43.14)

vdrift = µF.

in general, and we shall call µ the mobility. We have from Eq. (43.13) that

(43.15) The mobility is proportional to the mean time between collisions (there are fewer collisions to slow it down) and inversely proportional to the mass (more inertia means less speed picked up between collisions).

µ = τ /m.

To get the correct numerical coeﬃcient in Eq. (43.13), which is correct as given, takes some care. Without intending to confuse, we should still point out that the arguments have a subtlety which can be appreciated only by a careful and detailed study. To illustrate that there are diﬃculties, in spite of appearances, we shall make over again the argument which led to Eq. (43.13) in a reasonable but erroneous way (and the way one will ﬁnd in many textbooks!).

43-8

We might have said: The mean time between collisions is τ. After a collision the particle starts out with a random velocity, but it picks up an additional velocity between collisions, which is equal to the acceleration times the time. Since it takes the time τ to arrive at the next collision it gets there with the velocity (F/m)τ. At the beginning of the collision it had zero velocity. So between the two collisions it has, on the average, a velocity one-half of the ﬁnal velocity, so the mean drift velocity is 1 2 F τ /m. (Wrong!) This result is wrong and the result in Eq. (43.13) is right, although the arguments may sound equally satisfactory. The reason the second result is wrong is somewhat subtle, and has to do with the following: The argument is made as though all collisions were separated by the mean time τ. The fact is that some times are shorter and others are longer than the mean. Short times occur more often but make less contribution to the drift velocity because they have less chance「to really get going.」If one takes proper account of the distribution of free times between collisions, one can show that there should not be the factor 1 2 that was obtained from the second argument. The error was made in trying to relate by a simple argument the average ﬁnal velocity to the average velocity itself. This relationship is not simple, so it is best to concentrate on what is wanted: the average velocity itself. The ﬁrst argument we gave determines the average velocity directly—and correctly! But we can perhaps see now why we shall not in general try to get all of the correct numerical coeﬃcients in our elementary derivations!

We return now to our simplifying assumption that each collision knocks out all memory of the past motion—that a fresh start is made after each collision. Suppose our S-molecule is a heavy object in a background of lighter molecules. Then our S-molecule will not lose its「forward」momentum in each collision. It would take several collisions before its motion was「randomized」again. We should assume, instead, that at each collision—in each time τ on the average—it loses a certain fraction of its momentum. We shall not work out the details, but just state that the result is equivalent to replacing τ, the average collision time, by a new—and longer—τ which corresponds to the average「forgetting time,」i.e., the average time to forget its forward momentum. With such an interpretation of τ we can use our formula (43.15) for situations which are not quite as simple as we ﬁrst assumed.

43-4 Ionic conductivity We now apply our results to a special case. Suppose we have a gas in a vessel in which there are also some ions—atoms or molecules with a net electric charge.

43-9

We show the situation schematically in Fig. 43-2. If two opposite walls of the container are metallic plates, we can connect them to the terminals of a battery and thereby produce an electric ﬁeld in the gas. The electric ﬁeld will result in a force on the ions, so they will begin to drift toward one or the other of the plates. An electric current will be induced, and the gas with its ions will behave like a resistor. By computing the ion ﬂow from the drift velocity we can compute the resistance. We ask, speciﬁcally: How does the ﬂow of electric current depend on the voltage diﬀerence V that we apply across the two plates?

Fig. 43-2. Electric current from an ionized gas.

We consider the case that our container is a rectangular box of length b and cross-sectional area A (Fig. 43-2). If the potential diﬀerence, or voltage, from one plate to the other is V , the electric ﬁeld E between the plates is V /b. (The electric potential is the work done in carrying a unit charge from one plate to the other. The force on a unit charge is E. If E is the same everywhere between the plates, which is a good enough approximation for now, the work done on a unit charge is just Eb, so V = Eb.) The special force on an ion of the gas is qE, where q is the charge on the ion. The drift velocity of the ion is then µ times this force, or

vdrift = µF = µqE = µq

(43.16) An electric current I is the ﬂow of charge in a unit time. The electric current to one of the plates is given by the total charge of the ions which arrive at the plate in a unit of time. If the ions drift toward the plate with the velocity vdrift,

V b

.

43-10

then those which are within a distance (vdrift · T) will arrive at the plate in the time T. If there are ni ions per unit volume, the number which reach the plate in the time T is (ni · A · vdrift · T). Each ion carries the charge q, so we have that (43.17)

Charge collected in T = qniAvdriftT. The current I is the charge collected in T divided by T, so

Substituting vdrift from (43.16), we have

I = qniAvdrift.

I = µq2ni

A b

V.

(43.18)

(43.19)

We ﬁnd that the current is proportional to the voltage, which is just the form of Ohm’s law, and the resistance R is the inverse of the proportionality constant:

1 R

= µq2ni

A b

.

(43.20)

We have a relation between the resistance and the molecular properties ni, q, and µ, which depends in turn on m and τ. If we know ni and q from atomic measurements, a measurement of R could be used to determine µ, and from µ also τ.

43-5 Molecular diﬀusion We turn now to a diﬀerent kind of problem, and a diﬀerent kind of analysis: the theory of diﬀusion. Suppose that we have a container of gas in thermal equilibrium, and that we introduce a small amount of a diﬀerent kind of gas at some place in the container. We shall call the original gas the「background」gas and the new one the「special」gas. The special gas will start to spread out through the whole container, but it will spread slowly because of the presence of the background gas. This slow spreading-out process is called diﬀusion. The diﬀusion is controlled mainly by the molecules of the special gas getting knocked about by the molecules of the background gas. After a large number of collisions, the special molecules end up spread out more or less evenly throughout the whole volume. We must be careful not to confuse diﬀusion of a gas with the

43-11

gross transport that may occur due to convection currents. Most commonly, the mixing of two gases occurs by a combination of convection and diﬀusion. We are interested now only in the case that there are no「wind」currents. The gas is spreading only by molecular motions, by diﬀusion. We wish to compute how fast diﬀusion takes place.

We now compute the net ﬂow of molecules of the「special」gas due to the molecular motions. There will be a net ﬂow only when there is some nonuniform distribution of the molecules, otherwise all of the molecular motions would average to give no net ﬂow. Let us consider ﬁrst the ﬂow in the x-direction. To ﬁnd the ﬂow, we consider an imaginary plane surface perpendicular to the x-axis and count the number of special molecules that cross this plane. To obtain the net ﬂow, we must count as positive those molecules which cross in the direction of positive x and subtract from this number the number which cross in the negative x-direction. As we have seen many times, the number which cross a surface area in a time ∆T is given by the number which start the interval ∆T in a volume which extends the distance v ∆T from the plane. (Note that v, here, is the actual molecular velocity, not the drift velocity.)

We shall simplify our algebra by giving our surface one unit of area. Then the number of special molecules which pass from left to right (taking the +x-direction to the right) is n−v ∆T, where n− is the number of special molecules per unit volume to the left (within a factor of 2 or so, but we are ignoring such factors!). The number which cross from right to left is, similarly, n+v ∆T, where n+ is the number density of special molecules on the right-hand side of the plane. If we call the molecular current J, by which we mean the net ﬂow of molecules per unit area per unit time, we have

or

J = n−v ∆T − n+v ∆T

∆T

,

J = (n− − n+)v.

(43.21)

(43.22)

What shall we use for n− and n+? When we say「the density on the left,」how far to the left do we mean? We should choose the density at the place from which the molecules started their「ﬂight,」because the number which start such trips is determined by the number present at that place. So by n− we should mean the density a distance to the left equal to the mean free path l, and by n+, the density at the distance l to the right of our imaginary surface.

43-12

It is convenient to consider that the distribution of our special molecules in space is described by a continuous function of x, y, and z which we shall call na. By na(x, y, z) we mean the number density of special molecules in a small volume element centered on (x, y, z). In terms of na we can express the diﬀerence (n+ − n−) as

(n+ − n−) = dna dx

∆x = dna dx

· 2l.

(43.23)

Substituting this result in Eq. (43.22) and neglecting the factor of 2, we get

Jx = −lv

dna dx

.

(43.24)

We have found that the ﬂow of special molecules is proportional to the derivative of the density, or to what is sometimes called the「gradient」of the density.

It is clear that we have made several rough approximations. Besides various factors of two we have left out, we have used v where we should have used vx, and we have assumed that n+ and n− refer to places at the perpendicular distance l from our surface, whereas for those molecules which do not travel perpendicular to the surface element, l should correspond to the slant distance from the surface. All of these reﬁnements can be made; the result of a more careful analysis shows that the right-hand side of Eq. (43.24) should be multiplied by 1/3. So a better answer is

Jx = − lv 3

dna dx

.

(43.25)

Similar equations can be written for the currents in the y- and z-directions. The current Jx and the density gradient dna/dx can be measured by macro- scopic observations. Their experimentally determined ratio is called the「diﬀusion coeﬃcient,」D. That is,

Jx = −D

dna dx

.

(43.26)

We have been able to show that for a gas we expect

(43.27) So far in this chapter we have considered two distinct processes: mobility, the drift of molecules due to「outside」forces; and diﬀusion, the spreading determined only by the internal forces, the random collisions. There is, however, a relation

D = 1

3 lv.

43-13

between them, since they both depend basically on the thermal motions, and the mean free path l appears in both calculations.

If, in Eq. (43.25), we substitute l = vτ and τ = µm, we have

Jx = − 1

3 mv2µ

dna dx

.

But mv2 depends only on the temperature. We recall that

so

2 mv2 = 3 1

2 kT,

Jx = −µkT

dna dx

.

(43.28)

(43.29)

(43.30)

We ﬁnd that D, the diﬀusion coeﬃcient, is just kT times µ, the mobility coeﬃcient:

D = µkT.

(43.31)

And it turns out that the numerical coeﬃcient in (43.31) is exactly right—no extra factors have to be thrown in to adjust for our rough assumptions. We can show, in fact, that (43.31) must always be correct—even in complicated situations (for example, the case of a suspension in a liquid) where the details of our simple calculations would not apply at all.

To show that (43.31) must be correct in general, we shall derive it in a diﬀerent way, using only our basic principles of statistical mechanics. Imagine a situation in which there is a gradient of「special」molecules, and we have a diﬀusion current proportional to the density gradient, according to Eq. (43.26). We now apply a force ﬁeld in the x-direction, so that each special molecule feels the force F. According to the deﬁnition of the mobility µ there will be a drift velocity given by

vdrift = µF.

(43.32)

By our usual arguments, the drift current (the net number of molecules which pass a unit of area in a unit of time) will be

Jdrift = navdrift,

43-14

(43.33)

or

(43.34) We now adjust the force F so that the drift current due to F just balances the diﬀusion, so that there is no net ﬂow of our special molecules. We have Jx + Jdrift = 0, or

Jdrift = naµF.

(43.35) Under the「balance」conditions we ﬁnd a steady (with time) gradient of

= naµF.

dna dx

D

density given by

dna dx

(43.36) But notice! We are describing an equilibrium condition, so our equilibrium laws of statistical mechanics apply. According to these laws the probability of ﬁnding a molecule at the coordinate x is proportional to e−U/kT , where U is the potential energy. In terms of the number density na, this means that

= naµF D

.

If we diﬀerentiate (43.37) with respect to x, we ﬁnd

na = n0e−U/kT .

or

dna dx

= −n0e−U/kT · 1

kT

dU dx

,

dna dx

= − na kT

dU dx

.

(43.37)

(43.38)

(43.39)

In our situation, since the force F is in the x-direction, the potential energy U is just −F x, and −dU/dx = F. Equation (43.39) then gives

dna dx

= naF kT

.

(43.40)

[This is just exactly Eq. (40.2), from which we deduced e−U/kT in the ﬁrst place, so we have come in a circle]. Comparing (43.40) with (43.36), we get exactly Eq. (43.31). We have shown that Eq. (43.31), which gives the diﬀusion current in terms of the mobility, has the correct coeﬃcient and is very generally true. Mobility and diﬀusion are intimately connected. This relation was ﬁrst deduced by Einstein.

43-15

43-6 Thermal conductivity The methods of the kinetic theory that we have been using above can be used also to compute the thermal conductivity of a gas. If the gas at the top of a container is hotter than the gas at the bottom, heat will ﬂow from the top to the bottom. (We think of the top being hotter because otherwise convection currents would be set up and the problem would no longer be one of heat conduction.) The transfer of heat from the hotter gas to the colder gas is by the diﬀusion of the「hot」molecules—those with more energy—downward and the diﬀusion of the「cold」molecules upward. To compute the ﬂow of thermal energy we can ask about the energy carried downward across an element of area by the downward-moving molecules, and about the energy carried upward across the surface by the upward-moving molecules. The diﬀerence will give us the net downward ﬂow of energy.

The thermal conductivity κ is deﬁned as the ratio of the rate at which thermal

energy is carried across a unit surface area, to the temperature gradient:

1 A

dQ dt

= −κ

dT dz

.

(43.41)

Since the details of the calculations are quite similar to those we have done above in considering molecular diﬀusion, we shall leave it as an exercise for the reader to show that

κ = knlv γ − 1 ,

(43.42)

where kT /(γ − 1) is the average energy of a molecule at the temperature T. If we use our relation nlσc = 1, the heat conductivity can be written as

κ = 1 γ − 1

kv σc

.

(43.43)

We have a rather surprising result. We know that the average velocity of gas molecules depends on the temperature but not on the density. We expect σc to depend only on the size of the molecules. So our simple result says that the thermal conductivity κ (and therefore the rate of ﬂow of heat in any particular circumstance) is independent of the density of the gas! The change in the number of「carriers」of energy with a change in density is just compensated by the larger distance the「carriers」can go between collisions.

43-16

One may ask:「Is the heat ﬂow independent of the gas density in the limit as the density goes to zero? When there is no gas at all?」Certainly not! The formula (43.43) was derived, as were all the others in this chapter, under the assumption that the mean free path between collisions is much smaller than any of the dimensions of the container. Whenever the gas density is so low that a molecule has a fair chance of crossing from one wall of its container to the other without having a collision, none of the calculations of this chapter apply. We must in such cases go back to kinetic theory and calculate again the details of what will occur.

43-17

44

