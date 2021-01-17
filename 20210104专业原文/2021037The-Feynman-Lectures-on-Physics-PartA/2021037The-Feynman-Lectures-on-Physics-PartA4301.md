Diffusion

43-1 Collisions between moleculesWe have considered so far only the molecular motions in a gas which is inthermal equilibrium. We want now to discuss what happens when things arenear, but not exactly in, equilibrium. In a situation far from equilibrium, thingsare extremely complicated, but in a situation very close to equilibrium we caneasily work out what happens. To see what happens, we must, however, returnto the kinetic theory. Statistical mechanics and thermodynamics deal with theequilibrium situation, but away from equilibrium we can only analyze what occursatom by atom, so to speak.

As a simple example of a nonequilibrium circumstance, we shall considerthe diﬀusion of ions in a gas. Suppose that in a gas there is a relatively smallconcentration of ions—electrically charged molecules. If we put an electric ﬁeldon the gas, then each ion will have a force on it which is diﬀerent from the forceson the neutral molecules of the gas. If there were no other molecules present, anion would have a constant acceleration until it reached the wall of the container.But because of the presence of the other molecules, it cannot do that; its velocityincreases only until it collides with a molecule and loses its momentum. It startsagain to pick up more speed, but then it loses its momentum again. The neteﬀect is that an ion works its way along an erratic path, but with a net motion inthe direction of the electric force. We shall see that the ion has an average「drift」with a mean speed which is proportional to the electric ﬁeld—the stronger theﬁeld, the faster it goes. While the ﬁeld is on, and while the ion is moving along, itis, of course, not in thermal equilibrium, it is trying to get to equilibrium, whichis to be sitting at the end of the container. By means of the kinetic theory wecan compute the drift velocity.

It turns out that with our present mathematical abilities we cannot reallycompute precisely what will happen, but we can obtain approximate results

43-1

which exhibit all the essential features. We can ﬁnd out how things will vary withpressure, with temperature, and so on, but it will not be possible to get preciselythe correct numerical factors in front of all the terms. We shall, therefore, in ourderivations, not worry about the precise value of numerical factors. They can beobtained only by a very much more sophisticated mathematical treatment.

Before we consider what happens in nonequilibrium situations, we shall needto look a little closer at what goes on in a gas in thermal equilibrium. We shallneed to know, for example, what the average time between successive collisionsof a molecule is.

Any molecule experiences a sequence of collisions with other molecules—in arandom way, of course. A particular molecule will, in a long period of time T,have a certain number, N, of hits. If we double the length of time, there will betwice as many hits. So the number of collisions is proportional to the time T.We would like to write it this way:

N = T /τ.

(43.1)We have written the constant of proportionality as 1/τ, where τ will have thedimensions of a time. The constant τ is the average time between collisions.Suppose, for example, that in an hour there are 60 collisions; then τ is one minute.We would say that τ (one minute) is the average time between the collisions.We may often wish to ask the following question:「What is the chance that amolecule will experience a collision during the next small interval of time dt?」The answer, we may intuitively understand, is dt/τ. But let us try to make amore convincing argument. Suppose that there were a very large number N ofmolecules. How many will have collisions in the next interval of time dt? If thereis equilibrium, nothing is changing on the average with time. So N moleculeswaiting the time dt will have the same number of collisions as one moleculewaiting for the time N dt. That number we know is N dt/τ. So the number ofhits of N molecules is N dt/τ in a time dt, and the chance, or probability, of ahit for any one molecule is just 1/N as large, or (1/N)(N dt/τ) = dt/τ, as weguessed above. That is to say, the fraction of the molecules which will suﬀer acollision in the time dt is dt/τ. To take an example, if τ is one minute, then inone second the fraction of particles which will suﬀer collisions is 1/60. What thismeans, of course, is that 1/60 of the molecules happen to be close enough towhat they are going to hit next that their collisions will occur in the next second.When we say that τ, the mean time between collisions, is one minute, wedo not mean that all the collisions will occur at times separated by exactly one

43-2

minute. A particular particle does not have a collision, wait one minute, and thenhave another collision. The times between successive collisions are quite variable.We will not need it for our later work here, but we may make a small diversionto answer the question:「What are the times between collisions?」We know thatfor the case above, the average time is one minute, but we might like to know,for example, what is the chance that we get no collision for two minutes?

We shall ﬁnd the answer to the general question:「What is the probabilitythat a molecule will go for a time t without having a collision?」At some arbitraryinstant—that we call t = 0—we begin to watch a particular molecule. What isthe chance that it gets by until t without colliding with another molecule? Tocompute the probability, we observe what is happening to all N0 molecules in acontainer. After we have waited a time t, some of them will have had collisions.We let N(t) be the number that have not had collisions up to the time t. N(t)is, of course, less than N0. We can ﬁnd N(t) because we know how it changeswith time. If we know that N(t) molecules have got by until t, then N(t + dt),the number which get by until t + dt, is less than N(t) by the number that havecollisions in dt. The number that collide in dt we have written above in terms ofthe mean time τ as dN = N(t) dt/τ. We have the equation

N(t + dt) = N(t) − N(t) dtτ

.

(43.2)

The quantity on the left-hand side, N(t + dt), can be written, according to thedeﬁnitions of calculus, as N(t) + (dN/dt) dt. Making this substitution, Eq. (43.2)yields

.

(43.3)

dN(t)

dt

= − N(t)

τ

The number that are being lost in the interval dt is proportional to the numberthat are present, and inversely proportional to the mean life τ. Equation (43.3)is easily integrated if we rewrite it asdN(t)N(t) = − dt

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

(43.6)We know that the constant must be just N0, the total number of moleculespresent, since all of them start at t = 0 to wait for their「next」collision. We canwrite our result as(43.7)If we wish the probability of no collision, P(t), we can get it by dividing N(t)by N0, so(43.8)Our result is: the probability that a particular molecule survives a time t withouta collision is e−t/τ, where τ is the mean time between collisions. The probabilitystarts out at 1 (or certainty) for t = 0, and gets less as t gets bigger andbigger. The probability that the molecule avoids a collision for a time equalto τ is e−1 ≈ 0.37. The chance is less than one-half that it will have a greaterthan average time between collisions. That is all right, because there are enoughmolecules which go collision-free for times much longer than the mean time beforecolliding, so that the average time can still be τ.We originally deﬁned τ as the average time between collisions. The resultwe have obtained in Eq. (43.7) also says that the mean time from an arbitrarystarting instant to the next collision is also τ. We can demonstrate this somewhatsurprising fact in the following way. The number of molecules which experiencetheir next collision in the interval dt at the time t after an arbitrarily chosenstarting time is N(t) dt/τ. Their「time until the next collision」is, of course,just t. The「average time until the next collision」is obtained in the usual way:

Z ∞

0

Average time until the next collision = 1N0

N(t) dt

τ

.

t

Using N(t) obtained in (43.7) and evaluating the integral, we ﬁnd indeed that τis the average time from any instant until the next collision.

43-2 The mean free pathAnother way of describing the molecular collisions is to talk not about the timebetween collisions, but about how far the particle moves between collisions. If

43-4

we say that the average time between collisions is τ, and that the molecules havea mean velocity v, we can expect that the average distance between collisions,which we shall call l, is just the product of τ and v. This distance betweencollisions is usually called the mean free path:

Mean free path l = τ v.

(43.9)In this chapter we shall be a little careless about what kind of average wemean in any particular case. The various possible averages—the mean, the root-mean-square, etc.—are all nearly equal and diﬀer by factors which are near toone. Since a detailed analysis is required to obtain the correct numerical factorsanyway, we need not worry about which average is required at any particularpoint. We may also warn the reader that the algebraic symbols we are using forsome of the physical quantities (e.g., l for the mean free path) do not follow agenerally accepted convention, mainly because there is no general agreement.Just as the chance that a molecule will have a collision in a short time dtis equal to dt/τ, the chance that it will have a collision in going a distance dxis dx/l. Following the same line of argument used above, the reader can showthat the probability that a molecule will go at least the distance x before havingits next collision is e−x/l.The average distance a molecule goes before colliding with another molecule—the mean free path l—will depend on how many molecules there are around andon the「size」of the molecules, i.e., how big a target they represent. The eﬀective「size」of a target in a collision we usually describe by a「collision cross section,」the same idea that is used in nuclear physics, or in light-scattering problems.

Consider a moving particle which travels a distance dx through a gas whichhas n0 scatterers (molecules) per unit volume (Fig. 43-1). If we look at each unit

Fig. 43-1. Collision cross section.

43-5

of area perpendicular to the direction of motion of our selected particle, we willﬁnd there n0 dx molecules. If each one presents an eﬀective collision area or, asit is usually called,「collision cross section,」σc, then the total area covered bythe scatterers is σcn0 dx.By「collision cross section」we mean the area within which the center of ourparticle must be located if it is to collide with a particular molecule. If moleculeswere little spheres (a classical picture) we would expect that σc = π(r1 + r2)2,where r1 and r2 are the radii of the two colliding objects. The chance thatour particle will have a collision is the ratio of the area covered by scatteringmolecules to the total area, which we have taken to be one. So the probability ofa collision in going a distance dx is just σcn0 dx:

Chance of a collision in dx = σcn0 dx.

(43.10)

We have seen above that the chance of a collision in dx can also be writtenin terms of the mean free path l as dx/l. Comparing this with (43.10), we canrelate the mean free path to the collision cross section:

1l

= σcn0,

which is easier to remember if we write it as

σcn0l = 1.

(43.11)

(43.12)

This formula can be thought of as saying that there should be one collision, onthe average, when the particle goes through a distance l in which the scatteringmolecules could just cover the total area. In a cylindrical volume of length land a base of unit area, there are n0l scatterers; if each one has an area σc thetotal area covered is n0lσc, which is just one unit of area. The whole area isnot covered, of course, because some molecules are partly hidden behind others.That is why some molecules go farther than l before having a collision. It isonly on the average that the molecules have a collision by the time they go thedistance l. From measurements of the mean free path l we can determine thescattering cross section σc, and compare the result with calculations based on adetailed theory of atomic structure. But that is a diﬀerent subject! So we returnto the problem of nonequilibrium states.

43-6

43-3 The drift speedWe want to describe what happens to a molecule, or several molecules, whichare diﬀerent in some way from the large majority of the molecules in a gas.We shall refer to the「majority」molecules as the「background」molecules, andwe shall call the molecules which are diﬀerent from the background molecules「special」molecules or, for short, the S-molecules. A molecule could be specialfor any number of reasons: It might be heavier than the background molecules.It might be a diﬀerent chemical. It might have an electric charge—i.e., be anion in a background of uncharged molecules. Because of their diﬀerent massesor charges the S-molecules may have forces on them which are diﬀerent fromthe forces on the background molecules. By considering what happens to theseS-molecules we can understand the basic eﬀects which come into play in a similarway in many diﬀerent phenomena. To list a few: the diﬀusion of gases, electriccurrents in batteries, sedimentation, centrifugal separation, etc.

We begin by concentrating on the basic process: an S-molecule in a back-ground gas is acted on by some speciﬁc force F (which might be, e.g., gravitationalor electrical) and in addition by the not-so-speciﬁc forces due to collisions withthe background molecules. We would like to describe the general behavior of theS-molecule. What happens to it, in detail, is that it darts around hither and yonas it collides over and over again with other molecules. But if we watch it carefullywe see that it does make some net progress in the direction of the force F . Wesay that there is a drift, superposed on its random motion. We would like toknow what the speed of its drift is—its drift velocity—due to the force F .

If we start to observe an S-molecule at some instant we may expect that it issomewhere between two collisions. In addition to the velocity it was left withafter its last collision it is picking up some velocity component due to the force F .In a short time (on the average, in a time τ) it will experience a collision andstart out on a new piece of its trajectory. It will have a new starting velocity,but the same acceleration from F .

To keep things simple for the moment, we shall suppose that after eachcollision our S-molecule gets a completely「fresh」start. That is, that it keeps noremembrance of its past acceleration by F . This might be a reasonable assumptionif our S-molecule were much lighter than the background molecules, but it iscertainly not valid in general. We shall discuss later an improved assumption.For the moment, then, our assumption is that the S-molecule leaves eachcollision with a velocity which may be in any direction with equal likelihood. The

43-7

starting velocity will take it equally in all directions and will not contribute toany net motion, so we shall not worry further about its initial velocity after acollision. In addition to its random motion, each S-molecule will have, at anymoment, an additional velocity in the direction of the force F , which it has pickedup since its last collision. What is the average value of this part of the velocity?It is just the acceleration F /m (where m is the mass of the S-molecule) timesthe average time since the last collision. Now the average time since the lastcollision must be the same as the average time until the next collision, whichwe have called τ, above. The average velocity from F , of course, is just what iscalled the drift velocity, so we have the relation

vdrift = F τm

.

(43.13)

This basic relation is the heart of our subject. There may be some complicationin determining what τ is, but the basic process is deﬁned by Eq. (43.13).You will notice that the drift velocity is proportional to the force. Thereis, unfortunately, no generally used name for the constant of proportionality.Diﬀerent names have been used for each diﬀerent kind of force. If in an electricalproblem the force is written as the charge times the electric ﬁeld, F = qE, thenthe constant of proportionality between the velocity and the electric ﬁeld E isusually called the「mobility.」In spite of the possibility of some confusion, weshall use the term mobility for the ratio of the drift velocity to the force for anyforce. We write(43.14)

vdrift = µF.

in general, and we shall call µ the mobility. We have from Eq. (43.13) that

(43.15)The mobility is proportional to the mean time between collisions (there are fewercollisions to slow it down) and inversely proportional to the mass (more inertiameans less speed picked up between collisions).

µ = τ /m.

To get the correct numerical coeﬃcient in Eq. (43.13), which is correct asgiven, takes some care. Without intending to confuse, we should still point outthat the arguments have a subtlety which can be appreciated only by a carefuland detailed study. To illustrate that there are diﬃculties, in spite of appearances,we shall make over again the argument which led to Eq. (43.13) in a reasonablebut erroneous way (and the way one will ﬁnd in many textbooks!).

43-8

We might have said: The mean time between collisions is τ. After a collisionthe particle starts out with a random velocity, but it picks up an additionalvelocity between collisions, which is equal to the acceleration times the time.Since it takes the time τ to arrive at the next collision it gets there with thevelocity (F/m)τ. At the beginning of the collision it had zero velocity. So betweenthe two collisions it has, on the average, a velocity one-half of the ﬁnal velocity, sothe mean drift velocity is 12 F τ /m. (Wrong!) This result is wrong and the resultin Eq. (43.13) is right, although the arguments may sound equally satisfactory.The reason the second result is wrong is somewhat subtle, and has to do with thefollowing: The argument is made as though all collisions were separated by themean time τ. The fact is that some times are shorter and others are longer thanthe mean. Short times occur more often but make less contribution to the driftvelocity because they have less chance「to really get going.」If one takes properaccount of the distribution of free times between collisions, one can show thatthere should not be the factor 12 that was obtained from the second argument.The error was made in trying to relate by a simple argument the average ﬁnalvelocity to the average velocity itself. This relationship is not simple, so it is bestto concentrate on what is wanted: the average velocity itself. The ﬁrst argumentwe gave determines the average velocity directly—and correctly! But we canperhaps see now why we shall not in general try to get all of the correct numericalcoeﬃcients in our elementary derivations!

We return now to our simplifying assumption that each collision knocks outall memory of the past motion—that a fresh start is made after each collision.Suppose our S-molecule is a heavy object in a background of lighter molecules.Then our S-molecule will not lose its「forward」momentum in each collision.It would take several collisions before its motion was「randomized」again. Weshould assume, instead, that at each collision—in each time τ on the average—itloses a certain fraction of its momentum. We shall not work out the details, butjust state that the result is equivalent to replacing τ, the average collision time,by a new—and longer—τ which corresponds to the average「forgetting time,」i.e.,the average time to forget its forward momentum. With such an interpretationof τ we can use our formula (43.15) for situations which are not quite as simpleas we ﬁrst assumed.

43-4 Ionic conductivityWe now apply our results to a special case. Suppose we have a gas in a vesselin which there are also some ions—atoms or molecules with a net electric charge.

43-9

We show the situation schematically in Fig. 43-2. If two opposite walls of thecontainer are metallic plates, we can connect them to the terminals of a batteryand thereby produce an electric ﬁeld in the gas. The electric ﬁeld will result in aforce on the ions, so they will begin to drift toward one or the other of the plates.An electric current will be induced, and the gas with its ions will behave like aresistor. By computing the ion ﬂow from the drift velocity we can compute theresistance. We ask, speciﬁcally: How does the ﬂow of electric current depend onthe voltage diﬀerence V that we apply across the two plates?

Fig. 43-2. Electric current from an ionized gas.

We consider the case that our container is a rectangular box of length b andcross-sectional area A (Fig. 43-2). If the potential diﬀerence, or voltage, fromone plate to the other is V , the electric ﬁeld E between the plates is V /b. (Theelectric potential is the work done in carrying a unit charge from one plate tothe other. The force on a unit charge is E. If E is the same everywhere betweenthe plates, which is a good enough approximation for now, the work done on aunit charge is just Eb, so V = Eb.) The special force on an ion of the gas is qE,where q is the charge on the ion. The drift velocity of the ion is then µ timesthis force, or

vdrift = µF = µqE = µq

(43.16)An electric current I is the ﬂow of charge in a unit time. The electric currentto one of the plates is given by the total charge of the ions which arrive at theplate in a unit of time. If the ions drift toward the plate with the velocity vdrift,

Vb

.

43-10

then those which are within a distance (vdrift · T) will arrive at the plate in thetime T. If there are ni ions per unit volume, the number which reach the platein the time T is (ni · A · vdrift · T). Each ion carries the charge q, so we have that(43.17)

Charge collected in T = qniAvdriftT.The current I is the charge collected in T divided by T, so

Substituting vdrift from (43.16), we have

I = qniAvdrift.

I = µq2ni

Ab

V.

(43.18)

(43.19)

We ﬁnd that the current is proportional to the voltage, which is just the form ofOhm’s law, and the resistance R is the inverse of the proportionality constant:

1R

= µq2ni

Ab

.

(43.20)

We have a relation between the resistance and the molecular properties ni, q,and µ, which depends in turn on m and τ. If we know ni and q from atomicmeasurements, a measurement of R could be used to determine µ, and from µalso τ.

43-5 Molecular diﬀusionWe turn now to a diﬀerent kind of problem, and a diﬀerent kind of analysis:the theory of diﬀusion. Suppose that we have a container of gas in thermalequilibrium, and that we introduce a small amount of a diﬀerent kind of gasat some place in the container. We shall call the original gas the「background」gas and the new one the「special」gas. The special gas will start to spread outthrough the whole container, but it will spread slowly because of the presenceof the background gas. This slow spreading-out process is called diﬀusion. Thediﬀusion is controlled mainly by the molecules of the special gas getting knockedabout by the molecules of the background gas. After a large number of collisions,the special molecules end up spread out more or less evenly throughout thewhole volume. We must be careful not to confuse diﬀusion of a gas with the

43-11

gross transport that may occur due to convection currents. Most commonly, themixing of two gases occurs by a combination of convection and diﬀusion. We areinterested now only in the case that there are no「wind」currents. The gas isspreading only by molecular motions, by diﬀusion. We wish to compute how fastdiﬀusion takes place.

We now compute the net ﬂow of molecules of the「special」gas due to themolecular motions. There will be a net ﬂow only when there is some nonuniformdistribution of the molecules, otherwise all of the molecular motions would averageto give no net ﬂow. Let us consider ﬁrst the ﬂow in the x-direction. To ﬁnd theﬂow, we consider an imaginary plane surface perpendicular to the x-axis andcount the number of special molecules that cross this plane. To obtain the netﬂow, we must count as positive those molecules which cross in the direction ofpositive x and subtract from this number the number which cross in the negativex-direction. As we have seen many times, the number which cross a surface areain a time ∆T is given by the number which start the interval ∆T in a volumewhich extends the distance v ∆T from the plane. (Note that v, here, is the actualmolecular velocity, not the drift velocity.)

We shall simplify our algebra by giving our surface one unit of area. Then thenumber of special molecules which pass from left to right (taking the +x-directionto the right) is n−v ∆T, where n− is the number of special molecules per unitvolume to the left (within a factor of 2 or so, but we are ignoring such factors!).The number which cross from right to left is, similarly, n+v ∆T, where n+ is thenumber density of special molecules on the right-hand side of the plane. If wecall the molecular current J, by which we mean the net ﬂow of molecules perunit area per unit time, we have

or

J = n−v ∆T − n+v ∆T

∆T

,

J = (n− − n+)v.

(43.21)

(43.22)

What shall we use for n− and n+? When we say「the density on the left,」how far to the left do we mean? We should choose the density at the place fromwhich the molecules started their「ﬂight,」because the number which start suchtrips is determined by the number present at that place. So by n− we shouldmean the density a distance to the left equal to the mean free path l, and by n+,the density at the distance l to the right of our imaginary surface.

43-12

It is convenient to consider that the distribution of our special moleculesin space is described by a continuous function of x, y, and z which we shallcall na. By na(x, y, z) we mean the number density of special molecules in asmall volume element centered on (x, y, z). In terms of na we can express thediﬀerence (n+ − n−) as

(n+ − n−) = dnadx

∆x = dnadx

· 2l.

(43.23)

Substituting this result in Eq. (43.22) and neglecting the factor of 2, we get

Jx = −lv

dnadx

.

(43.24)

We have found that the ﬂow of special molecules is proportional to the derivativeof the density, or to what is sometimes called the「gradient」of the density.

It is clear that we have made several rough approximations. Besides variousfactors of two we have left out, we have used v where we should have used vx, andwe have assumed that n+ and n− refer to places at the perpendicular distance lfrom our surface, whereas for those molecules which do not travel perpendicularto the surface element, l should correspond to the slant distance from the surface.All of these reﬁnements can be made; the result of a more careful analysis showsthat the right-hand side of Eq. (43.24) should be multiplied by 1/3. So a betteranswer is

Jx = − lv3

dnadx

.

(43.25)

Similar equations can be written for the currents in the y- and z-directions.The current Jx and the density gradient dna/dx can be measured by macro-scopic observations. Their experimentally determined ratio is called the「diﬀusioncoeﬃcient,」D. That is,

Jx = −D

dnadx

.

(43.26)

We have been able to show that for a gas we expect

(43.27)So far in this chapter we have considered two distinct processes: mobility, thedrift of molecules due to「outside」forces; and diﬀusion, the spreading determinedonly by the internal forces, the random collisions. There is, however, a relation

D = 1

3 lv.

43-13

between them, since they both depend basically on the thermal motions, and themean free path l appears in both calculations.

If, in Eq. (43.25), we substitute l = vτ and τ = µm, we have

Jx = − 1

3 mv2µ

dnadx

.

But mv2 depends only on the temperature. We recall that

so

2 mv2 = 31

2 kT,

Jx = −µkT

dnadx

.

(43.28)

(43.29)

(43.30)

We ﬁnd that D, the diﬀusion coeﬃcient, is just kT times µ, the mobility coeﬃcient:

D = µkT.

(43.31)

And it turns out that the numerical coeﬃcient in (43.31) is exactly right—noextra factors have to be thrown in to adjust for our rough assumptions. Wecan show, in fact, that (43.31) must always be correct—even in complicatedsituations (for example, the case of a suspension in a liquid) where the details ofour simple calculations would not apply at all.

To show that (43.31) must be correct in general, we shall derive it in a diﬀerentway, using only our basic principles of statistical mechanics. Imagine a situationin which there is a gradient of「special」molecules, and we have a diﬀusion currentproportional to the density gradient, according to Eq. (43.26). We now applya force ﬁeld in the x-direction, so that each special molecule feels the force F.According to the deﬁnition of the mobility µ there will be a drift velocity givenby

vdrift = µF.

(43.32)

By our usual arguments, the drift current (the net number of molecules whichpass a unit of area in a unit of time) will be

Jdrift = navdrift,

43-14

(43.33)

or

(43.34)We now adjust the force F so that the drift current due to F just balancesthe diﬀusion, so that there is no net ﬂow of our special molecules. We haveJx + Jdrift = 0, or

Jdrift = naµF.

(43.35)Under the「balance」conditions we ﬁnd a steady (with time) gradient of

= naµF.

dnadx

D

density given by

dnadx

(43.36)But notice! We are describing an equilibrium condition, so our equilibriumlaws of statistical mechanics apply. According to these laws the probability ofﬁnding a molecule at the coordinate x is proportional to e−U/kT , where U is thepotential energy. In terms of the number density na, this means that

= naµFD

.

If we diﬀerentiate (43.37) with respect to x, we ﬁnd

na = n0e−U/kT .

or

dnadx

= −n0e−U/kT · 1

kT

dUdx

,

dnadx

= − nakT

dUdx

.

(43.37)

(43.38)

(43.39)

In our situation, since the force F is in the x-direction, the potential energy U isjust −F x, and −dU/dx = F. Equation (43.39) then gives

dnadx

= naFkT

.

(43.40)

[This is just exactly Eq. (40.2), from which we deduced e−U/kT in the ﬁrst place,so we have come in a circle]. Comparing (43.40) with (43.36), we get exactlyEq. (43.31). We have shown that Eq. (43.31), which gives the diﬀusion currentin terms of the mobility, has the correct coeﬃcient and is very generally true.Mobility and diﬀusion are intimately connected. This relation was ﬁrst deducedby Einstein.

43-15

43-6 Thermal conductivityThe methods of the kinetic theory that we have been using above can beused also to compute the thermal conductivity of a gas. If the gas at the top of acontainer is hotter than the gas at the bottom, heat will ﬂow from the top to thebottom. (We think of the top being hotter because otherwise convection currentswould be set up and the problem would no longer be one of heat conduction.)The transfer of heat from the hotter gas to the colder gas is by the diﬀusionof the「hot」molecules—those with more energy—downward and the diﬀusionof the「cold」molecules upward. To compute the ﬂow of thermal energy wecan ask about the energy carried downward across an element of area by thedownward-moving molecules, and about the energy carried upward across thesurface by the upward-moving molecules. The diﬀerence will give us the netdownward ﬂow of energy.

The thermal conductivity κ is deﬁned as the ratio of the rate at which thermal

energy is carried across a unit surface area, to the temperature gradient:

1A

dQdt

= −κ

dTdz

.

(43.41)

Since the details of the calculations are quite similar to those we have done abovein considering molecular diﬀusion, we shall leave it as an exercise for the readerto show that

κ = knlvγ − 1 ,

(43.42)

where kT /(γ − 1) is the average energy of a molecule at the temperature T.If we use our relation nlσc = 1, the heat conductivity can be written as

κ = 1γ − 1

kvσc

.

(43.43)

We have a rather surprising result. We know that the average velocity of gasmolecules depends on the temperature but not on the density. We expect σcto depend only on the size of the molecules. So our simple result says that thethermal conductivity κ (and therefore the rate of ﬂow of heat in any particularcircumstance) is independent of the density of the gas! The change in the numberof「carriers」of energy with a change in density is just compensated by the largerdistance the「carriers」can go between collisions.

43-16

One may ask:「Is the heat ﬂow independent of the gas density in the limitas the density goes to zero? When there is no gas at all?」Certainly not! Theformula (43.43) was derived, as were all the others in this chapter, under theassumption that the mean free path between collisions is much smaller than anyof the dimensions of the container. Whenever the gas density is so low that amolecule has a fair chance of crossing from one wall of its container to the otherwithout having a collision, none of the calculations of this chapter apply. Wemust in such cases go back to kinetic theory and calculate again the details ofwhat will occur.

43-17

44

