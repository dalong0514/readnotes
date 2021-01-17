The Special Theory of Relativity

15-1 The principle of relativityFor over 200 years the equations of motion enunciated by Newton were believedto describe nature correctly, and the ﬁrst time that an error in these laws wasdiscovered, the way to correct it was also discovered. Both the error and itscorrection were discovered by Einstein in 1905.

Newton’s Second Law, which we have expressed by the equation

F = d(mv)/dt,

was stated with the tacit assumption that m is a constant, but we now knowthat this is not true, and that the mass of a body increases with velocity. InEinstein’s corrected formula m has the value

m0p1 − v2/c2 ,

m =

(15.1)

where the「rest mass」m0 represents the mass of a body that is not moving and cis the speed of light, which is about 3× 105 km· sec−1 or about 186,000 mi· sec−1.For those who want to learn just enough about it so they can solve problems,that is all there is to the theory of relativity—it just changes Newton’s laws byintroducing a correction factor to the mass. From the formula itself it is easyto see that this mass increase is very small in ordinary circumstances. If thevelocity is even as great as that of a satellite, which goes around the earth at5 mi/sec, then v/c = 5/186,000: putting this value into the formula shows thatthe correction to the mass is only one part in two to three billion, which is nearlyimpossible to observe. Actually, the correctness of the formula has been amplyconﬁrmed by the observation of many kinds of particles, moving at speeds rangingup to practically the speed of light. However, because the eﬀect is ordinarily

15-1

so small, it seems remarkable that it was discovered theoretically before it wasdiscovered experimentally. Empirically, at a suﬃciently high velocity, the eﬀectis very large, but it was not discovered that way. Therefore it is interesting to seehow a law that involved so delicate a modiﬁcation (at the time when it was ﬁrstdiscovered) was brought to light by a combination of experiments and physicalreasoning. Contributions to the discovery were made by a number of people, theﬁnal result of whose work was Einstein’s discovery.

There are really two Einstein theories of relativity. This chapter is concernedwith the Special Theory of Relativity, which dates from 1905. In 1915 Einsteinpublished an additional theory, called the General Theory of Relativity. Thislatter theory deals with the extension of the Special Theory to the case of thelaw of gravitation; we shall not discuss the General Theory here.

The principle of relativity was ﬁrst stated by Newton, in one of his corollariesto the laws of motion:「The motions of bodies included in a given space arethe same among themselves, whether that space is at rest or moves uniformlyforward in a straight line.」This means, for example, that if a space ship is driftingalong at a uniform speed, all experiments performed in the space ship and all thephenomena in the space ship will appear the same as if the ship were not moving,provided, of course, that one does not look outside. That is the meaning of theprinciple of relativity. This is a simple enough idea, and the only question iswhether it is true that in all experiments performed inside a moving system thelaws of physics will appear the same as they would if the system were standingstill. Let us ﬁrst investigate whether Newton’s laws appear the same in themoving system.

Suppose that Moe is moving in the x-direction with a uniform velocity u, andhe measures the position of a certain point, shown in Fig. 15-1. He designatesthe「x-distance」of the point in his coordinate system as x0. Joe is at rest, and

Fig. 15-1. Two coordinate systems in uniform relative motion along

their x-axes.

15-2

measures the position of the same point, designating its x-coordinate in hissystem as x. The relationship of the coordinates in the two systems is clear fromthe diagram. After time t Moe’s origin has moved a distance ut, and if the twosystems originally coincided,

x0 = x − ut,y0 = y,z0 = z,t0 = t.

(15.2)

If we substitute this transformation of coordinates into Newton’s laws we ﬁndthat these laws transform to the same laws in the primed system; that is, the lawsof Newton are of the same form in a moving system as in a stationary system,and therefore it is impossible to tell, by making mechanical experiments, whetherthe system is moving or not.

The principle of relativity has been used in mechanics for a long time. Itwas employed by various people, in particular Huygens, to obtain the rules forthe collision of billiard balls, in much the same way as we used it in Chapter 10to discuss the conservation of momentum. In the 19th century interest in itwas heightened as the result of investigations into the phenomena of electricity,magnetism, and light. A long series of careful studies of these phenomena bymany people culminated in Maxwell’s equations of the electromagnetic ﬁeld,which describe electricity, magnetism, and light in one uniform system. However,the Maxwell equations did not seem to obey the principle of relativity. Thatis, if we transform Maxwell’s equations by the substitution of equations (15.2),their form does not remain the same; therefore, in a moving space ship theelectrical and optical phenomena should be diﬀerent from those in a stationaryship. Thus one could use these optical phenomena to determine the speed ofthe ship; in particular, one could determine the absolute speed of the ship bymaking suitable optical or electrical measurements. One of the consequences ofMaxwell’s equations is that if there is a disturbance in the ﬁeld such that light isgenerated, these electromagnetic waves go out in all directions equally and atthe same speed c, or 186,000 mi/sec. Another consequence of the equations isthat if the source of the disturbance is moving, the light emitted goes throughspace at the same speed c. This is analogous to the case of sound, the speed ofsound waves being likewise independent of the motion of the source.This independence of the motion of the source, in the case of light, brings up

an interesting problem:

15-3

Suppose we are riding in a car that is going at a speed u, and light from therear is going past the car with speed c. Diﬀerentiating the ﬁrst equation in (15.2)gives

dx0/dt = dx/dt − u,

which means that according to the Galilean transformation the apparent speedof the passing light, as we measure it in the car, should not be c but shouldbe c − u. For instance, if the car is going 100,000 mi/sec, and the light isgoing 186,000 mi/sec, then apparently the light going past the car should go86,000 mi/sec. In any case, by measuring the speed of the light going past the car(if the Galilean transformation is correct for light), one could determine the speedof the car. A number of experiments based on this general idea were performed todetermine the velocity of the earth, but they all failed—they gave no velocity atall. We shall discuss one of these experiments in detail, to show exactly what wasdone and what was the matter; something was the matter, of course, somethingwas wrong with the equations of physics. What could it be?

15-2 The Lorentz transformationWhen the failure of the equations of physics in the above case came to light,the ﬁrst thought that occurred was that the trouble must lie in the new Maxwellequations of electrodynamics, which were only 20 years old at the time. It seemedalmost obvious that these equations must be wrong, so the thing to do was tochange them in such a way that under the Galilean transformation the principleof relativity would be satisﬁed. When this was tried, the new terms that had tobe put into the equations led to predictions of new electrical phenomena that didnot exist at all when tested experimentally, so this attempt had to be abandoned.Then it gradually became apparent that Maxwell’s laws of electrodynamics werecorrect, and the trouble must be sought elsewhere.

In the meantime, H. A. Lorentz noticed a remarkable and curious thing when

he made the following substitutions in the Maxwell equations:

x − ut

p1 − u2/c2 ,x0 =y0 = y,z0 = z,p1 − u2/c2 ,t0 = t − ux/c2

15-4

(15.3)

namely, Maxwell’s equations remain in the same form when this transformationis applied to them! Equations (15.3) are known as a Lorentz transformation.Einstein, following a suggestion originally made by Poincaré, then proposed thatall the physical laws should be of such a kind that they remain unchanged undera Lorentz transformation. In other words, we should change, not the laws ofelectrodynamics, but the laws of mechanics. How shall we change Newton’s lawsso that they will remain unchanged by the Lorentz transformation? If this goal isset, we then have to rewrite Newton’s equations in such a way that the conditionswe have imposed are satisﬁed. As it turned out, the only requirement is that themass m in Newton’s equations must be replaced by the form shown in Eq. (15.1).When this change is made, Newton’s laws and the laws of electrodynamics willharmonize. Then if we use the Lorentz transformation in comparing Moe’smeasurements with Joe’s, we shall never be able to detect whether either ismoving, because the form of all the equations will be the same in both coordinatesystems!

It is interesting to discuss what it means that we replace the old transformationbetween the coordinates and time with a new one, because the old one (Galilean)seems to be self-evident, and the new one (Lorentz) looks peculiar. We wishto know whether it is logically and experimentally possible that the new, andnot the old, transformation can be correct. To ﬁnd that out, it is not enoughto study the laws of mechanics but, as Einstein did, we too must analyze ourideas of space and time in order to understand this transformation. We shallhave to discuss these ideas and their implications for mechanics at some length,so we say in advance that the eﬀort will be justiﬁed, since the results agree withexperiment.

15-3 The Michelson-Morley experimentAs mentioned above, attempts were made to determine the absolute velocityof the earth through the hypothetical「ether」that was supposed to pervade allspace. The most famous of these experiments is one performed by Michelson andMorley in 1887. It was 18 years later before the negative results of the experimentwere ﬁnally explained, by Einstein.

The Michelson-Morley experiment was performed with an apparatus like thatshown schematically in Fig. 15-2. This apparatus is essentially comprised of alight source A, a partially silvered glass plate B, and two mirrors C and E, allmounted on a rigid base. The mirrors are placed at equal distances L from B.

15-5

Fig. 15-2. Schematic diagram of the Michelson-Morley experiment.

The plate B splits an oncoming beam of light, and the two resulting beamscontinue in mutually perpendicular directions to the mirrors, where they arereﬂected back to B. On arriving back at B, the two beams are recombined astwo superposed beams, D and F. If the time taken for the light to go from Bto E and back is the same as the time from B to C and back, the emergingbeams D and F will be in phase and will reinforce each other, but if the twotimes diﬀer slightly, the beams will be slightly out of phase and interference willresult. If the apparatus is「at rest」in the ether, the times should be preciselyequal, but if it is moving toward the right with a velocity u, there should be adiﬀerence in the times. Let us see why.

First, let us calculate the time required for the light to go from B to E andback. Let us say that the time for light to go from plate B to mirror E is t1,and the time for the return is t2. Now, while the light is on its way from Bto the mirror, the apparatus moves a distance ut1, so the light must traverse adistance L + ut1, at the speed c. We can also express this distance as ct1, so wehave

ct1 = L + ut1,

or

t1 = L/(c − u).

(This result is also obvious from the point of view that the velocity of light relativeto the apparatus is c − u, so the time is the length L divided by c − u.) In a likemanner, the time t2 can be calculated. During this time the plate B advances a

15-6

distance ut2, so the return distance of the light is L − ut2. Then we have

ct2 = L − ut2,

or

t2 = L/(c + u).

Then the total time is

For convenience in later comparison of times we write this as

t1 + t2 = 2Lc/(c2 − u2).

t1 + t2 = 2L/c

1 − u2/c2 .

(15.4)

Our second calculation will be of the time t3 for the light to go from B tothe mirror C. As before, during time t3 the mirror C moves to the right adistance ut3 to the position C0; in the same time, the light travels a distance ct3along the hypotenuse of a triangle, which is BC0. For this right triangle we have

or

from which we get

(ct3)2 = L2 + (ut3)2

L2 = c2t2

3 − u2t23 = (c2 − u2)t2p3,

c2 − u2.

t3 = L/

For the return trip from C0 the distance is the same, as can be seen from thesymmetry of the ﬁgure; therefore the return time is also the same, and the totaltime is 2t3. With a little rearrangement of the form we can write

2t3 =

2L√c2 − u2

=

p1 − u2/c2 .

2L/c

(15.5)

We are now able to compare the times taken by the two beams of light. Inexpressions (15.4) and (15.5) the numerators are identical, and represent thetime that would be taken if the apparatus were at rest. In the denominators, theterm u2/c2 will be small, unless u is comparable in size to c. The denominatorsrepresent the modiﬁcations in the times caused by the motion of the apparatus.And behold, these modiﬁcations are not the same—the time to go to C andback is a little less than the time to E and back, even though the mirrors areequidistant from B, and all we have to do is to measure that diﬀerence withprecision.

15-7

Here a minor technical point arises—suppose the two lengths L are not exactlyequal? In fact, we surely cannot make them exactly equal. In that case we simplyturn the apparatus 90 degrees, so that BC is in the line of motion and BEis perpendicular to the motion. Any small diﬀerence in length then becomesunimportant, and what we look for is a shift in the interference fringes when werotate the apparatus.In carrying out the experiment, Michelson and Morley oriented the apparatusso that the line BE was nearly parallel to the earth’s motion in its orbit (atcertain times of the day and night). This orbital speed is about 18 miles persecond, and any「ether drift」should be at least that much at some time of the dayor night and at some time during the year. The apparatus was amply sensitiveto observe such an eﬀect, but no time diﬀerence was found—the velocity of theearth through the ether could not be detected. The result of the experiment wasnull.

The result of the Michelson-Morley experiment was very puzzling and mostdisturbing. The ﬁrst fruitful idea for ﬁnding a way out of the impasse came fromLorentz. He suggested that material bodies contract when they are moving, andthat this foreshortening is only in the direction of the motion, and also, that ifthe length is L0 when a body is at rest, then when it moves with speed u parallelto its length, the new length, which we call Lk (L-parallel), is given by

Lk = L0

is shortened to Lp1 − u2/c2. Therefore Eq. (15.5) is not changed, but the L of

(15.6)When this modiﬁcation is applied to the Michelson-Morley interferometer appa-ratus the distance from B to C does not change, but the distance from B to EEq. (15.4) must be changed in accordance with Eq. (15.6). When this is done weobtain

p1 − u2/c2.

t1 + t2 = (2L/c)p1 − u2/c2

1 − u2/c2

p1 − u2/c2 .

2L/c

=

(15.7)

Comparing this result with Eq. (15.5), we see that t1+t2 = 2t3. So if the apparatusshrinks in the manner just described, we have a way of understanding why theMichelson-Morley experiment gives no eﬀect at all. Although the contractionhypothesis successfully accounted for the negative result of the experiment, it wasopen to the objection that it was invented for the express purpose of explainingaway the diﬃculty, and was too artiﬁcial. However, in many other experimentsto discover an ether wind, similar diﬃculties arose, until it appeared that nature

15-8

was in a「conspiracy」to thwart man by introducing some new phenomenon toundo every phenomenon that he thought would permit a measurement of u.It was ultimately recognized, as Poincaré pointed out, that a complete con-spiracy is itself a law of nature! Poincaré then proposed that there is such a lawof nature, that it is not possible to discover an ether wind by any experiment;that is, there is no way to determine an absolute velocity.

15-4 Transformation of timeIn checking out whether the contraction idea is in harmony with the factsin other experiments, it turns out that everything is correct provided that thetimes are also modiﬁed, in the manner expressed in the fourth equation of theset (15.3). That is because the time t3, calculated for the trip from B to C andback, is not the same when calculated by a man performing the experiment in amoving space ship as when calculated by a stationary observer who is watchingthe space ship. To the man in the ship the time is simply 2L/c, but to the othersees the man in the space ship lighting a cigar, all the actions appear to beslower than normal, while to the man inside, everything moves at a normal rate.So not only must the lengths shorten, but also the time-measuring instruments(「clocks」) must apparently slow down. That is, when the clock in the space ship

observer it is (2L/c)/p1 − u2/c2 (Eq. 15.5). In other words, when the outsiderrecords 1 second elapsed, as seen by the man in the ship, it shows 1/p1 − u2/c2

second to the man outside.

This slowing of the clocks in a moving system is a very peculiar phenomenon,and is worth an explanation. In order to understand this, we have to watch themachinery of the clock and see what happens when it is moving. Since that israther diﬃcult, we shall take a very simple kind of clock. The one we choose israther a silly kind of clock, but it will work in principle: it is a rod (meter stick)with a mirror at each end, and when we start a light signal between the mirrors,the light keeps going up and down, making a click every time it comes down,like a standard ticking clock. We build two such clocks, with exactly the samelengths, and synchronize them by starting them together; then they agree alwaysthereafter, because they are the same in length, and light always travels withspeed c. We give one of these clocks to the man to take along in his space ship,and he mounts the rod perpendicular to the direction of motion of the ship; thenthe length of the rod will not change. How do we know that perpendicular lengthsdo not change? The men can agree to make marks on each other’s y-meter stick

15-9

as they pass each other. By symmetry, the two marks must come at the same y-and y0-coordinates, since otherwise, when they get together to compare results,one mark will be above or below the other, and so we could tell who was reallymoving.

Now let us see what happens to the moving clock. Before the man took itaboard, he agreed that it was a nice, standard clock, and when he goes along inthe space ship he will not see anything peculiar. If he did, he would know hewas moving—if anything at all changed because of the motion, he could tell hewas moving. But the principle of relativity says this is impossible in a uniformlymoving system, so nothing has changed. On the other hand, when the externalobserver looks at the clock going by, he sees that the light, in going from mirrorto mirror, is「really」taking a zigzag path, since the rod is moving sidewise allthe while. We have already analyzed such a zigzag motion in connection withthe Michelson-Morley experiment. If in a given time the rod moves forwarda distance proportional to u in Fig. 15-3, the distance the light travels in thesame time is proportional to c, and the vertical distance is therefore proportionalto √c2 − u2.That is, it takes a longer time for light to go from end to end in the movingclock than in the stationary clock. Therefore the apparent time between clicks islonger for the moving clock, in the same proportion as shown in the hypotenuseof the triangle (that is the source of the square root expressions in our equations).From the ﬁgure it is also apparent that the greater u is, the more slowly themoving clock appears to run. Not only does this particular kind of clock runmore slowly, but if the theory of relativity is correct, any other clock, operatingon any principle whatsoever, would also appear to run slower, and in the sameproportion—we can say this without further analysis. Why is this so?

To answer the above question, suppose we had two other clocks made exactlyalike with wheels and gears, or perhaps based on radioactive decay, or somethingelse. Then we adjust these clocks so they both run in precise synchronism withour ﬁrst clocks. When light goes up and back in the ﬁrst clocks and announcesits arrival with a click, the new models also complete some sort of cycle, whichthey simultaneously announce by some doubly coincident ﬂash, or bong, or othersignal. One of these clocks is taken into the space ship, along with the ﬁrst kind.Perhaps this clock will not run slower, but will continue to keep the same timeas its stationary counterpart, and thus disagree with the other moving clock. Ahno, if that should happen, the man in the ship could use this mismatch betweenhis two clocks to determine the speed of his ship, which we have been supposing

15-10

Fig. 15-3. (a) A「light clock」at rest in the S(cid:48) system. (b) The sameclock, moving through the S system. (c) Illustration of the diagonalpath taken by the light beam in a moving「light clock.」

15-11

is impossible. We need not know anything about the machinery of the new clockthat might cause the eﬀect—we simply know that whatever the reason, it willappear to run slow, just like the ﬁrst one.

Now if all moving clocks run slower, if no way of measuring time gives anythingbut a slower rate, we shall just have to say, in a certain sense, that time itselfappears to be slower in a space ship. All the phenomena there—the man’spulse rate, his thought processes, the time he takes to light a cigar, how long ittakes to grow up and get old—all these things must be slowed down in the sameproportion, because he cannot tell he is moving. The biologists and medical mensometimes say it is not quite certain that the time it takes for a cancer to developwill be longer in a space ship, but from the viewpoint of a modern physicistit is nearly certain; otherwise one could use the rate of cancer development todetermine the speed of the ship!

A very interesting example of the slowing of time with motion is furnished bymu-mesons (muons), which are particles that disintegrate spontaneously after anaverage lifetime of 2.2 × 10−6 sec. They come to the earth in cosmic rays, andcan also be produced artiﬁcially in the laboratory. Some of them disintegratein midair, but the remainder disintegrate only after they encounter a piece ofmaterial and stop. It is clear that in its short lifetime a muon cannot travel,even at the speed of light, much more than 600 meters. But although the muonsare created at the top of the atmosphere, some 10 kilometers up, yet they areactually found in a laboratory down here, in cosmic rays. How can that be?The answer is that diﬀerent muons move at various speeds, some of which arevery close to the speed of light. While from their own point of view they liveonly about 2 µsec, from our point of view they live considerably longer—enoughlonger that they may reach the earth. The factor by which the time is increased

has already been given as 1/p1 − u2/c2. The average life has been measured

quite accurately for muons of diﬀerent velocities, and the values agree closelywith the formula.

We do not know why the meson disintegrates or what its machinery is, butwe do know its behavior satisﬁes the principle of relativity. That is the utility ofthe principle of relativity—it permits us to make predictions, even about thingsthat otherwise we do not know much about. For example, before we have anyidea at all about what makes the meson disintegrate, we can still predict thatwhen it is moving at nine-tenths of the speed of light, the apparent length of time

that it lasts is (2.2 × 10−6)/p1 − 92/102 sec; and our prediction works—that is

the good thing about it.

15-12

15-5 The Lorentz contractionNow let us return to the Lorentz transformation (15.3) and try to get a betterunderstanding of the relationship between the (x, y, z, t) and the (x0, y0, z0, t0)coordinate systems, which we shall call the S and S0 systems, or Joe and Moesystems, respectively. We have already noted that the ﬁrst equation is based onthe Lorentz suggestion of contraction along the x-direction; how can we provethat a contraction takes place? In the Michelson-Morley experiment, we nowappreciate that the transverse arm BC cannot change length, by the principleof relativity; yet the null result of the experiment demands that the times mustbe equal. So, in order for the experiment to give a null result, the longitudinal

arm BE must appear shorter, by the square rootp1 − u2/c2. What does this

contraction mean, in terms of measurements made by Joe and Moe? Supposethat Moe, moving with the S0 system in the x-direction, is measuring the x0-coordinate of some point with a meter stick. He lays the stick down x0 times, sohe thinks the distance is x0 meters. From the viewpoint of Joe in the S system,however, Moe is using a foreshortened ruler, so the「real」distance measured is

x0p1 − u2/c2 meters. Then if the S0 system has travelled a distance ut awayhis coordinates, is at a distance x = x0p1 − u2/c2 + ut, or

from the S system, the S observer would say that the same point, measured in

x − ut

p1 − u2/c2 ,

x0 =

which is the ﬁrst equation of the Lorentz transformation.

15-6 SimultaneityIn an analogous way, because of the diﬀerence in time scales, the denominatorexpression is introduced into the fourth equation of the Lorentz transformation.The most interesting term in that equation is the ux/c2 in the numerator, becausethat is quite new and unexpected. Now what does that mean? If we look at thesituation carefully we see that events that occur at two separated places at thesame time, as seen by Moe in S0, do not happen at the same time as viewed byJoe in S. If one event occurs at point x1 at time t0 and the other event at x2and t0 (the same time), we ﬁnd that the two corresponding times t02 diﬀerby an amount

1 and t0

p1 − u2/c2 .1 = u(x1 − x2)/c2

2 − t0t0

15-13

This circumstance is called「failure of simultaneity at a distance,」and to makethe idea a little clearer let us consider the following experiment.

Suppose that a man moving in a space ship (system S0) has placed a clock ateach end of the ship and is interested in making sure that the two clocks are insynchronism. How can the clocks be synchronized? There are many ways. Oneway, involving very little calculation, would be ﬁrst to locate exactly the midpointbetween the clocks. Then from this station we send out a light signal which willgo both ways at the same speed and will arrive at both clocks, clearly, at thesame time. This simultaneous arrival of the signals can be used to synchronizethe clocks. Let us then suppose that the man in S0 synchronizes his clocks bythis particular method. Let us see whether an observer in system S would agreethat the two clocks are synchronous. The man in S0 has a right to believe theyare, because he does not know that he is moving. But the man in S reasons thatsince the ship is moving forward, the clock in the front end was running awayfrom the light signal, hence the light had to go more than halfway in order tocatch up; the rear clock, however, was advancing to meet the light signal, so thisdistance was shorter. Therefore the signal reached the rear clock ﬁrst, althoughthe man in S0 thought that the signals arrived simultaneously. We thus see thatwhen a man in a space ship thinks the times at two locations are simultaneous,equal values of t0 in his coordinate system must correspond to diﬀerent valuesof t in the other coordinate system!

15-7 Four-vectorsLet us see what else we can discover in the Lorentz transformation. It isinteresting to note that the transformation between the x’s and t’s is analogousin form to the transformation of the x’s and y’s that we studied in Chapter 11for a rotation of coordinates. We then had

x0 = x cos θ + y sin θ,y0 = y cos θ − x sin θ,

(15.8)

in which the new x0 mixes the old x and y, and the new y0 also mixes the oldx and y; similarly, in the Lorentz transformation we ﬁnd a new x0 which is amixture of x and t, and a new t0 which is a mixture of t and x. So the Lorentztransformation is analogous to a rotation, only it is a「rotation」in space andtime, which appears to be a strange concept. A check of the analogy to rotation

15-14

can be made by calculating the quantity

x02 + y02 + z02 − c2t02 = x2 + y2 + z2 − c2t2.

(15.9)

In this equation the ﬁrst three terms on each side represent, in three-dimensionalgeometry, the square of the distance between a point and the origin (surfaceof a sphere) which remains unchanged (invariant) regardless of rotation of thecoordinate axes. Similarly, Eq. (15.9) shows that there is a certain combinationwhich includes time, that is invariant to a Lorentz transformation. Thus, theanalogy to a rotation is complete, and is of such a kind that vectors, i.e., quantitiesinvolving「components」which transform the same way as the coordinates andtime, are also useful in connection with relativity.

Thus we contemplate an extension of the idea of vectors, which we have so farconsidered to have only space components, to include a time component. Thatis, we expect that there will be vectors with four components, three of which arelike the components of an ordinary vector, and with these will be associated afourth component, which is the analog of the time part.

This concept will be analyzed further in the next chapters, where we shallﬁnd that if the ideas of the preceding paragraph are applied to momentum,the transformation gives three space parts that are like ordinary momentumcomponents, and a fourth component, the time part, which is the energy.

15-8 Relativistic dynamicsWe are now ready to investigate, more generally, what form the laws ofmechanics take under the Lorentz transformation. [We have thus far explainedhow length and time change, but not how we get the modiﬁed formula for m(Eq. 15.1). We shall do this in the next chapter.] To see the consequencesof Einstein’s modiﬁcation of m for Newtonian mechanics, we start with theNewtonian law that force is the rate of change of momentum, or

F = d(mv)/dt.

Momentum is still given by mv, but when we use the new m this becomes

(15.10)

p = mv =

m0vp1 − v2/c2 .

15-15

This is Einstein’s modiﬁcation of Newton’s laws. Under this modiﬁcation, ifaction and reaction are still equal (which they may not be in detail, but are inthe long run), there will be conservation of momentum in the same way as before,but the quantity that is being conserved is not the old mv with its constant mass,but instead is the quantity shown in (15.10), which has the modiﬁed mass. Whenthis change is made in the formula for momentum, conservation of momentumstill works.

Now let us see how momentum varies with speed. In Newtonian mechanics itis proportional to the speed and, according (15.10), over a considerable range ofspeed, but small compared with c, it is nearly the same in relativistic mechanics,because the square-root expression diﬀers only slightly from 1. But when v isalmost equal to c, the square-root expression approaches zero, and the momentumtherefore goes toward inﬁnity.What happens if a constant force acts on a body for a long time? In Newtonianmechanics the body keeps picking up speed until it goes faster than light. Butthis is impossible in relativistic mechanics. In relativity, the body keeps pickingup, not speed, but momentum, which can continually increase because the massis increasing. After a while there is practically no acceleration in the sense of achange of velocity, but the momentum continues to increase. Of course, whenevera force produces very little change in the velocity of a body, we say that the bodyhas a great deal of inertia, and that is exactly what our formula for relativisticmass says (see Eq. 15.10)—it says that the inertia is very great when v is nearlyas great as c. As an example of this eﬀect, to deﬂect the high-speed electronsin the synchrotron that is used here at Caltech, we need a magnetic ﬁeld thatis 2000 times stronger than would be expected on the basis of Newton’s laws.In other words, the mass of the electrons in the synchrotron is 2000 times asgreat as their normal mass, and is as great as that of a proton! That m shouldbe 2000 times m0 means that 1 − v2/c2 must be 1/4,000,000, and that meansthat v diﬀers from c by one part in 8,000,000, so the electrons are getting prettyclose to the speed of light. If the electrons and light were both to start fromthe synchrotron (estimated as 700 feet away) and rush out to Bridge Lab, whichwould arrive ﬁrst? The light, of course, because light always travels faster.* Howmuch earlier? That is too hard to tell—instead, we tell by what distance thelight is ahead: it is about 1/1000 of an inch, or 14 the thickness of a piece of

* The electrons would actually win the race versus visible light because of the index of

refraction of air. A gamma ray would make out better.

15-16

paper! When the electrons are going that fast their masses are enormous, buttheir speed cannot exceed the speed of light.

Now let us look at some further consequences of relativistic change of mass.Consider the motion of the molecules in a small tank of gas. When the gasis heated, the speed of the molecules is increased, and therefore the mass isalso increased and the gas is heavier. An approximate formula to express theincrease of mass, for the case when the velocity is small, can be found by

expanding m0/p1 − v2/c2 = m0(1 − v2/c2)−1/2 in a power series, using the

binomial theorem. We get

m0(1 − v2/c2)−1/2 = m0(1 + 1

8 v4/c4 + ··· ).

We see clearly from the formula that the series converges rapidly when v is small,and the terms after the ﬁrst two or three are negligible. So we can write

2 v2/c2 + 3(cid:19)

(cid:18) 1

c2

m ∼= m0 + 1

2 m0v2

(15.11)

in which the second term on the right expresses the increase of mass due tomolecular velocity. When the temperature increases the v2 increases proportion-ately, so we can say that the increase in mass is proportional to the increasein temperature. But since 12 m0v2 is the kinetic energy in the old-fashionedNewtonian sense, we can also say that the increase in mass of all this body of gasis equal to the increase in kinetic energy divided by c2, or ∆m = ∆(K.E.)/c2.

15-9 Equivalence of mass and energyThe above observation led Einstein to the suggestion that the mass of a bodycan be expressed more simply than by the formula (15.1), if we say that the massis equal to the total energy content divided by c2. If Eq. (15.11) is multipliedby c2 the result is(15.12)Here, the term on the left expresses the total energy of a body, and we recognizethe last term as the ordinary kinetic energy. Einstein interpreted the largeconstant term, m0c2, to be part of the total energy of the body, an intrinsicenergy known as the「rest energy.」Let us follow out the consequences of assuming, with Einstein, that theenergy of a body always equals mc2. As an interesting result, we shall ﬁnd the

mc2 = m0c2 + 1

2 m0v2 + ···

15-17

formula (15.1) for the variation of mass with speed, which we have merely assumedup to now. We start with the body at rest, when its energy is m0c2. Then weapply a force to the body, which starts it moving and gives it kinetic energy;therefore, since the energy has increased, the mass has increased—this is implicitin the original assumption. So long as the force continues, the energy and themass both continue to increase. We have already seen (Chapter 13) that the rateof change of energy with time equals the force times the velocity, or

= F · v.

dEdt

(15.13)

We also have (Chapter 9, Eq. 9.1) that F = d(mv)/dt. When these relations areput together with the deﬁnition of E, Eq. (15.13) becomes

d(mc2)

dt

= v · d(mv)

dt

.

(15.14)

We wish to solve this equation for m. To do this we ﬁrst use the mathematicaltrick of multiplying both sides by 2m, which changes the equation to

c2(2m) dmdt

= 2mv · d(mv)

dt

.

(15.15)

We need to get rid of the derivatives, which can be accomplished by integratingboth sides. The quantity (2m) dm/dt can be recognized as the time derivativeof m2, and (2mv) · d(mv)/dt is the time derivative of (mv)2. So, Eq. (15.15) isthe same as

If the derivatives of two quantities are equal, the quantities themselves diﬀer atmost by a constant, say C. This permits us to write

m2c2 = m2v2 + C.

(15.17)

We need to deﬁne the constant C more explicitly. Since Eq. (15.17) must be truefor all velocities, we can choose a special case where v = 0, and say that in thiscase the mass is m0. Substituting these values into Eq. (15.17) gives

0c2 = 0 + C.m2

15-18

c2 d(m2)

dt

= d(m2v2)

dt

.

(15.16)

We can now use this value of C in Eq. (15.17), which becomes

m2c2 = m2v2 + m2

0c2.

Dividing by c2 and rearranging terms gives

from which we get

m2(1 − v2/c2) = m20,

m = m0/p1 − v2/c2.

(15.18)

(15.19)

This is the formula (15.1), and is exactly what is necessary for the agreementbetween mass and energy in Eq. (15.12).

Ordinarily these energy changes represent extremely slight changes in mass,because most of the time we cannot generate much energy from a given amountof material; but in an atomic bomb of explosive energy equivalent to 20 kilotonsof TNT, for example, it can be shown that the dirt after the explosion is lighterby 1 gram than the initial mass of the reacting material, because of the energythat was released, i.e., the released energy had a mass of 1 gram, according tothe relationship ∆E = ∆(mc2). This theory of equivalence of mass and energyhas been beautifully veriﬁed by experiments in which matter is annihilated—converted totally to energy: An electron and a positron come together at rest,each with a rest mass m0. When they come together they disintegrate and twogamma rays emerge, each with the measured energy of m0c2. This experimentfurnishes a direct determination of the energy associated with the existence ofthe rest mass of a particle.

15-19

16

