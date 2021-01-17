Conservation of Momentum

10-1 Newton’s Third LawOn the basis of Newton’s second law of motion, which gives the relationbetween the acceleration of any body and the force acting on it, any problem inmechanics can be solved in principle. For example, to determine the motion ofa few particles, one can use the numerical method developed in the precedingchapter. But there are good reasons to make a further study of Newton’s laws.First, there are quite simple cases of motion which can be analyzed not onlyby numerical methods, but also by direct mathematical analysis. For example,although we know that the acceleration of a falling body is 32 ft/sec2, andfrom this fact could calculate the motion by numerical methods, it is mucheasier and more satisfactory to analyze the motion and ﬁnd the general solution,s = s0 + v0t + 16t2. In the same way, although we can work out the positions of aharmonic oscillator by numerical methods, it is also possible to show analyticallythat the general solution is a simple cosine function of t, and so it is unnecessaryto go to all that arithmetical trouble when there is a simple and more accurateway to get the result. In the same manner, although the motion of one bodyaround the sun, determined by gravitation, can be calculated point by point bythe numerical methods of Chapter 9, which show the general shape of the orbit,it is nice also to get the exact shape, which analysis reveals as a perfect ellipse.Unfortunately, there are really very few problems which can be solved exactlyby analysis. In the case of the harmonic oscillator, for example, if the springforce is not proportional to the displacement, but is something more complicated,one must fall back on the numerical method. Or if there are two bodies goingaround the sun, so that the total number of bodies is three, then analysis cannotproduce a simple formula for the motion, and in practice the problem mustbe done numerically. That is the famous three-body problem, which so longchallenged human powers of analysis; it is very interesting how long it tookpeople to appreciate the fact that perhaps the powers of mathematical analysis

10-1

were limited and it might be necessary to use the numerical methods. Today anenormous number of problems that cannot be done analytically are solved bynumerical methods, and the old three-body problem, which was supposed to beso diﬃcult, is solved as a matter of routine in exactly the same manner that wasdescribed in the preceding chapter, namely, by doing enough arithmetic. However,there are also situations where both methods fail: the simple problems we cando by analysis, and the moderately diﬃcult problems by numerical, arithmeticalmethods, but the very complicated problems we cannot do by either method. Acomplicated problem is, for example, the collision of two automobiles, or eventhe motion of the molecules of a gas. There are countless particles in a cubicmillimeter of gas, and it would be ridiculous to try to make calculations withso many variables (about 1017—a hundred million billion). Anything like themotion of the molecules or atoms of a gas or a block or iron, or the motion ofthe stars in a globular cluster, instead of just two or three planets going aroundthe sun—such problems we cannot do directly, so we have to seek other means.In the situations in which we cannot follow details, we need to know somegeneral properties, that is, general theorems or principles which are consequencesof Newton’s laws. One of these is the principle of conservation of energy, whichwas discussed in Chapter 4. Another is the principle of conservation of momentum,the subject of this chapter. Another reason for studying mechanics further isthat there are certain patterns of motion that are repeated in many diﬀerentcircumstances, so it is good to study these patterns in one particular circumstance.For example, we shall study collisions; diﬀerent kinds of collisions have muchin common. In the ﬂow of ﬂuids, it does not make much diﬀerence what theﬂuid is, the laws of the ﬂow are similar. Other problems that we shall studyare vibrations and oscillations and, in particular, the peculiar phenomena ofmechanical waves—sound, vibrations of rods, and so on.

In our discussion of Newton’s laws it was explained that these laws are a kindof program that says「Pay attention to the forces,」and that Newton told us onlytwo things about the nature of forces. In the case of gravitation, he gave us thecomplete law of the force. In the case of the very complicated forces betweenatoms, he was not aware of the right laws for the forces; however, he discoveredone rule, one general property of forces, which is expressed in his Third Law, andthat is the total knowledge that Newton had about the nature of forces—the lawof gravitation and this principle, but no other details.

This principle is that action equals reaction.

10-2

What is meant is something of this kind: Suppose we have two small bodies,say particles, and suppose that the ﬁrst one exerts a force on the second one,pushing it with a certain force. Then, simultaneously, according to Newton’sThird Law, the second particle will push on the ﬁrst with an equal force, inthe opposite direction; furthermore, these forces eﬀectively act in the same line.This is the hypothesis, or law, that Newton proposed, and it seems to be quiteaccurate, though not exact (we shall discuss the errors later). For the momentwe shall take it to be true that action equals reaction. Of course, if there is athird particle, not on the same line as the other two, the law does not mean thatthe total force on the ﬁrst one is equal to the total force on the second, sincethe third particle, for instance, exerts its own push on each of the other two.The result is that the total eﬀect on the ﬁrst two is in some other direction, andthe forces on the ﬁrst two particles are, in general, neither equal nor opposite.However, the forces on each particle can be resolved into parts, there being onecontribution or part due to each other interacting particle. Then each pair ofparticles has corresponding components of mutual interaction that are equal inmagnitude and opposite in direction.

10-2 Conservation of momentumNow what are the interesting consequences of the above relationship? Suppose,for simplicity, that we have just two interacting particles, possibly of diﬀerentmass, and numbered 1 and 2. The forces between them are equal and opposite;what are the consequences? According to Newton’s Second Law, force is thetime rate of change of the momentum, so we conclude that the rate of change ofmomentum p1 of particle 1 is equal to minus the rate of change of momentum p2of particle 2, or(10.1)Now if the rate of change is always equal and opposite, it follows that the totalchange in the momentum of particle 1 is equal and opposite to the total changein the momentum of particle 2; this means that if we add the momentum ofparticle 1 to the momentum of particle 2, the rate of change of the sum of these,due to the mutual forces (called internal forces) between particles, is zero; that is(10.2)There is assumed to be no other force in the problem. If the rate of change of thissum is always zero, that is just another way of saying that the quantity (p1 + p2)

dp1/dt = −dp2/dt.

d(p1 + p2)/dt = 0.

10-3

does not change. (This quantity is also written m1v1 + m2v2, and is called thetotal momentum of the two particles.) We have now obtained the result that thetotal momentum of the two particles does not change because of any mutualinteractions between them. This statement expresses the law of conservation ofmomentum in that particular example. We conclude that if there is any kindof force, no matter how complicated, between two particles, and we measure orcalculate m1v1 + m2v2, that is, the sum of the two momenta, both before andafter the forces act, the results should be equal, i.e., the total momentum is aconstant.

If we extend the argument to three or more interacting particles in morecomplicated circumstances, it is evident that so far as internal forces are concerned,the total momentum of all the particles stays constant, since an increase inmomentum of one, due to another, is exactly compensated by the decrease ofthe second, due to the ﬁrst. That is, all the internal forces will balance out, andtherefore cannot change the total momentum of the particles. Then if there areno forces from the outside (external forces), there are no forces that can changethe total momentum; hence the total momentum is a constant.

It is worth describing what happens if there are forces that do not come fromthe mutual actions of the particles in question: suppose we isolate the interactingparticles. If there are only mutual forces, then, as before, the total momentumof the particles does not change, no matter how complicated the forces. On theother hand, suppose there are also forces coming from the particles outside theisolated group. Any force exerted by outside bodies on inside bodies, we call anexternal force. We shall later demonstrate that the sum of all external forcesequals the rate of change of the total momentum of all the particles inside, avery useful theorem.

The conservation of the total momentum of a number of interacting particles

can be expressed as

m1v1 + m2v2 + m3v3 + ··· = a constant,

(10.3)if there are no net external forces. Here the masses and corresponding velocitiesof the particles are numbered 1, 2, 3, 4, . . . The general statement of Newton’sSecond Law for each particle,

(10.4)is true speciﬁcally for the components of force and momentum in any given

F = ddt

(mv),

10-4

direction; thus the x-component of the force on a particle is equal to the x-component of the rate of change of momentum of that particle, or

Fx = ddt

(mvx),

(10.5)

and similarly for the y- and z-directions. Therefore Eq. (10.3) is really threeequations, one for each direction.In addition to the law of conservation of momentum, there is another interest-ing consequence of Newton’s Second Law, to be proved later, but merely statednow. This principle is that the laws of physics will look the same whether we arestanding still or moving with a uniform speed in a straight line. For example,a child bouncing a ball in an airplane ﬁnds that the ball bounces the same asthough he were bouncing it on the ground. Even though the airplane is movingwith a very high velocity, unless it changes its velocity, the laws look the sameto the child as they do when the airplane is standing still. This is the so-calledrelativity principle. As we use it here we shall call it「Galilean relativity」todistinguish it from the more careful analysis made by Einstein, which we shallstudy later.

We have just derived the law of conservation of momentum from Newton’slaws, and we could go on from here to ﬁnd the special laws that describe impactsand collisions. But for the sake of variety, and also as an illustration of a kind ofreasoning that can be used in physics in other circumstances where, for example,one might not know Newton’s laws and might take a diﬀerent approach, we shalldiscuss the laws of impacts and collisions from a completely diﬀerent point ofview. We shall base our discussion on the principle of Galilean relativity, statedabove, and shall end up with the law of conservation of momentum.

We shall start by assuming that nature would look the same if we run along ata certain speed and watch it as it would if we were standing still. Before discussingcollisions in which two bodies collide and stick together, or come together andbounce apart, we shall ﬁrst consider two bodies that are held together by a springor something else, and are then suddenly released and pushed by the spring orperhaps by a little explosion. Further, we shall consider motion in only onedirection. First, let us suppose that the two objects are exactly the same, are nicesymmetrical objects, and then we have a little explosion between them. After theexplosion, one of the bodies will be moving, let us say toward the right, with avelocity v. Then it appears reasonable that the other body is moving toward theleft with a velocity v, because if the objects are alike there is no reason for right

10-5

or left to be preferred and so the bodies would do something that is symmetrical.This is an illustration of a kind of thinking that is very useful in many problemsbut would not be brought out if we just started with the formulas.

The ﬁrst result from our experiment is that equal objects will have equalspeed, but now suppose that we have two objects made of diﬀerent materials, saycopper and aluminum, and we make the two masses equal. We shall now supposethat if we do the experiment with two masses that are equal, even though theobjects are not identical, the velocities will be equal. Someone might object:「But you know, you could do it backwards, you did not have to suppose that. Youcould deﬁne equal masses to mean two masses that acquire equal velocities inthis experiment.」We follow that suggestion and make a little explosion betweenthe copper and a very large piece of aluminum, so heavy that the copper ﬂies outand the aluminum hardly budges. That is too much aluminum, so we reduce theamount until there is just a very tiny piece, then when we make the explosion thealuminum goes ﬂying away, and the copper hardly budges. That is not enoughaluminum. Evidently there is some right amount in between; so we keep adjustingthe amount until the velocities come out equal. Very well then—let us turn itaround, and say that when the velocities are equal, the masses are equal. Thisappears to be just a deﬁnition, and it seems remarkable that we can transformphysical laws into mere deﬁnitions. Nevertheless, there are some physical lawsinvolved, and if we accept this deﬁnition of equal masses, we immediately ﬁndone of the laws, as follows.

Suppose we know from the foregoing experiment that two pieces of matter,A and B (of copper and aluminum), have equal masses, and we compare athird body, say a piece of gold, with the copper in the same manner as above,making sure that its mass is equal to the mass of the copper. If we now makethe experiment between the aluminum and the gold, there is nothing in logicthat says these masses must be equal; however, the experiment shows that theyactually are. So now, by experiment, we have found a new law. A statement ofthis law might be: If two masses are each equal to a third mass (as determinedby equal velocities in this experiment), then they are equal to each other. (Thisstatement does not follow at all from a similar statement used as a postulateregarding mathematical quantities.) From this example we can see how quickly westart to infer things if we are careless. It is not just a deﬁnition to say the massesare equal when the velocities are equal, because to say the masses are equal is toimply the mathematical laws of equality, which in turn makes a prediction aboutan experiment.

10-6

As a second example, suppose that A and B are found to be equal by doingthe experiment with one strength of explosion, which gives a certain velocity; ifwe then use a stronger explosion, will it be true or not true that the velocitiesnow obtained are equal? Again, in logic there is nothing that can decide thisquestion, but experiment shows that it is true. So, here is another law, whichmight be stated: If two bodies have equal masses, as measured by equal velocitiesat one velocity, they will have equal masses when measured at another velocity.From these examples we see that what appeared to be only a deﬁnition reallyinvolved some laws of physics.

In the development that follows we shall assume it is true that equal masseshave equal and opposite velocities when an explosion occurs between them. Weshall make another assumption in the inverse case: If two identical objects,moving in opposite directions with equal velocities, collide and stick together bysome kind of glue, then which way will they be moving after the collision? Thisis again a symmetrical situation, with no preference between right and left, sowe assume that they stand still. We shall also suppose that any two objects ofequal mass, even if the objects are made of diﬀerent materials, which collide andstick together, when moving with the same velocity in opposite directions willcome to rest after the collision.

10-3 Momentum is conserved!We can verify the above assumptions experimentally: ﬁrst, that if two sta-tionary objects of equal mass are separated by an explosion they will move apartwith the same speed, and second, if two objects of equal mass, coming togetherwith the same speed, collide and stick together they will stop. This we cando by means of a marvelous invention called an air trough,* which gets rid offriction, the thing which continually bothered Galileo (Fig. 10-1). He could not

Fig. 10-1. End view of linear air trough.

* H. V. Neher and R. B. Leighton, Amer. Jour. of Phys. 31, 255 (1963).

10-7

Fig. 10-2. Sectional view of gliders with explosive interaction cylinder

attachment.

do experiments by sliding things because they do not slide freely, but, by addinga magic touch, we can today get rid of friction. Our objects will slide withoutdiﬃculty, on and on at a constant velocity, as advertised by Galileo. This isdone by supporting the objects on air. Because air has very low friction, anobject glides along with practically constant velocity when there is no appliedforce. First, we use two glide blocks which have been made carefully to havethe same weight, or mass (their weight was measured really, but we know thatthis weight is proportional to the mass), and we place a small explosive cap ina closed cylinder between the two blocks (Fig. 10-2). We shall start the blocksfrom rest at the center point of the track and force them apart by exploding thecap with an electric spark. What should happen? If the speeds are equal whenthey ﬂy apart, they should arrive at the ends of the trough at the same time. Onreaching the ends they will both bounce back with practically opposite velocity,and will come together and stop at the center where they started. It is a goodtest; when it is actually done the result is just as we have described (Fig. 10-3).

Fig. 10-3. Schematic view of action-reaction experiment with equal

masses.

10-8

Fig. 10-4. Two views of an inelastic collision between equal masses.

Now the next thing we would like to ﬁgure out is what happens in a lesssimple situation. Suppose we have two equal masses, one moving with velocity vand the other standing still, and they collide and stick; what is going to happen?There is a mass 2m altogether when we are ﬁnished, drifting with an unknownvelocity. What velocity? That is the problem. To ﬁnd the answer, we make theassumption that if we ride along in a car, physics will look the same as if weare standing still. We start with the knowledge that two equal masses, movingin opposite directions with equal speeds v, will stop dead when they collide.Now suppose that while this happens, we are riding by in an automobile, at avelocity −v. Then what does it look like? Since we are riding along with oneof the two masses which are coming together, that one appears to us to havezero velocity. The other mass, however, going the other way with velocity v, willappear to be coming toward us at a velocity 2v (Fig. 10-4). Finally, the combinedmasses after collision will seem to be passing by with velocity v. We thereforeconclude that an object with velocity 2v, hitting an equal one at rest, will endup with velocity v, or what is mathematically exactly the same, an object withvelocity v hitting and sticking to one at rest will produce an object moving withvelocity v/2. Note that if we multiply the mass and the velocity beforehand andadd them together, mv + 0, we get the same answer as when we multiply themass and the velocity of everything afterwards, 2m times v/2. So that tells uswhat happens when a mass of velocity v hits one standing still.

In exactly the same manner we can deduce what happens when equal objects

having any two velocities hit each other.

Suppose we have two equal bodies with velocities v1 and v2, respectively,which collide and stick together. What is their velocity v after the collision?Again we ride by in an automobile, say at velocity v2, so that one body appearsto be at rest. The other then appears to have a velocity v1 − v2, and we havethe same case that we had before. When it is all ﬁnished they will be moving

10-9

Fig. 10-5. Two views of another inelastic collision between equal

masses.

at 1ground?

2(v1 − v2) + v2 or 1

2(v1 − v2) with respect to the car. What then is the actual speed on theIt is v = 1

2(v1 + v2) (Fig. 10-5). Again we note that

mv1 + mv2 = 2m(v1 + v2)/2.

(10.6)

Thus, using this principle, we can analyze any kind of collision in which twobodies of equal mass hit each other and stick. In fact, although we have workedonly in one dimension, we can ﬁnd out a great deal about much more complicatedcollisions by imagining that we are riding by in a car in some oblique direction.The principle is the same, but the details get somewhat complicated.

In order to test experimentally whether an object moving with velocity v,colliding with an equal one at rest, forms an object moving with velocity v/2,we may perform the following experiment with our air-trough apparatus. Weplace in the trough three equally massive objects, two of which are initially joinedtogether with our explosive cylinder device, the third being very near to butslightly separated from these and provided with a sticky bumper so that it willstick to another object which hits it. Now, a moment after the explosion, we havetwo objects of mass m moving with equal and opposite velocities v. A momentafter that, one of these collides with the third object and makes an object ofmass 2m moving, so we believe, with velocity v/2. How do we test whether itis really v/2? By arranging the initial positions of the masses on the trough sothat the distances to the ends are not equal, but are in the ratio 2 : 1. Thus ourﬁrst mass, which continues to move with velocity v, should cover twice as muchdistance in a given time as the two which are stuck together (allowing for thesmall distance travelled by the second object before it collided with the third).The mass m and the mass 2m should reach the ends at the same time, and whenwe try it, we ﬁnd that they do (Fig. 10-6).

10-10

Fig. 10-6. An experiment to verify that a mass m with velocity v

striking a mass m with zero velocity gives 2m with velocity v/2.

The next problem that we want to work out is what happens if we have twodiﬀerent masses. Let us take a mass m and a mass 2m and apply our explosiveinteraction. What will happen then? If, as a result of the explosion, m moveswith velocity v, with what velocity does 2m move? The experiment we havejust done may be repeated with zero separation between the second and thirdmasses, and when we try it we get the same result, namely, the reacting massesm and 2m attain velocities −v and v/2. Thus the direct reaction between mand 2m gives the same result as the symmetrical reaction between m and m,followed by a collision between m and a third mass m in which they stick together.Furthermore, we ﬁnd that the masses m and 2m returning from the ends of thetrough, with their velocities (nearly) exactly reversed, stop dead if they sticktogether.

Now the next question we may ask is this. What will happen if a mass mwith velocity v, say, hits and sticks to another mass 2m at rest? This is veryeasy to answer using our principle of Galilean relativity, for we simply watchthe collision which we have just described from a car moving with velocity −v/2(Fig. 10-7). From the car, the velocities are

and

1 = v − v(car) = v + v/2 = 3v/2v0

2 = −v/2 − v(car) = −v/2 + v/2 = 0.v0

After the collision, the mass 3m appears to us to be moving with velocity v/2.Thus we have the answer, i.e., the ratio of velocities before and after collisionis 3 to 1: if an object of mass m collides with a stationary object of mass 2m,then the whole thing moves oﬀ, stuck together, with a velocity 1/3 as much. Thegeneral rule again is that the sum of the products of the masses and the velocities

10-11

Fig. 10-7. Two views of an inelastic collision between m and 2m.

stays the same: mv + 0 equals 3m times v/3, so we are gradually building upthe theorem of the conservation of momentum, piece by piece.Now we have one against two. Using the same arguments, we can predict theresult of one against three, two against three, etc. The case of two against three,starting from rest, is shown in Fig. 10-8.

Fig. 10-8. Action and reaction between 2m and 3m.

In every case we ﬁnd that the mass of the ﬁrst object times its velocity, plusthe mass of the second object times its velocity, is equal to the total mass of theﬁnal object times its velocity. These are all examples, then, of the conservationof momentum. Starting from simple, symmetrical cases, we have demonstratedthe law for more complex cases. We could, in fact, do it for any rational massratio, and since every ratio is exceedingly close to a rational ratio, we can handleevery ratio as precisely as we wish.

10-4 Momentum and energyAll the foregoing examples are simple cases where the bodies collide and sticktogether, or were initially stuck together and later separated by an explosion.

10-12

However, there are situations in which the bodies do not cohere, as, for example,two bodies of equal mass which collide with equal speeds and then rebound. Fora brief moment they are in contact and both are compressed. At the instant ofmaximum compression they both have zero velocity and energy is stored in theelastic bodies, as in a compressed spring. This energy is derived from the kineticenergy the bodies had before the collision, which becomes zero at the instanttheir velocity is zero. The loss of kinetic energy is only momentary, however. Thecompressed condition is analogous to the cap that releases energy in an explosion.The bodies are immediately decompressed in a kind of explosion, and ﬂy apartagain; but we already know that case—the bodies ﬂy apart with equal speeds.However, this speed of rebound is less, in general, than the initial speed, becausenot all the energy is available for the explosion, depending on the material. Ifthe material is putty no kinetic energy is recovered, but if it is something morerigid, some kinetic energy is usually regained. In the collision the rest of thekinetic energy is transformed into heat and vibrational energy—the bodies arehot and vibrating. The vibrational energy also is soon transformed into heat. Itis possible to make the colliding bodies from highly elastic materials, such assteel, with carefully designed spring bumpers, so that the collision generates verylittle heat and vibration. In these circumstances the velocities of rebound arepractically equal to the initial velocities; such a collision is called elastic.That the speeds before and after an elastic collision are equal is not a matter ofconservation of momentum, but a matter of conservation of kinetic energy. Thatthe velocities of the bodies rebounding after a symmetrical collision are equal toand opposite each other, however, is a matter of conservation of momentum.We might similarly analyze collisions between bodies of diﬀerent masses,diﬀerent initial velocities, and various degrees of elasticity, and determine theﬁnal velocities and the loss of kinetic energy, but we shall not go into the detailsof these processes.

Elastic collisions are especially interesting for systems that have no internal「gears, wheels, or parts.」Then when there is a collision there is nowhere for theenergy to be impounded, because the objects that move apart are in the samecondition as when they collided. Therefore, between very elementary objects,the collisions are always elastic or very nearly elastic. For instance, the collisionsbetween atoms or molecules in a gas are said to be perfectly elastic. Althoughthis is an excellent approximation, even such collisions are not perfectly elastic;otherwise one could not understand how energy in the form of light or heatradiation could come out of a gas. Once in a while, in a gas collision, a low-energy

10-13

infrared ray is emitted, but this occurrence is very rare and the energy emitted isvery small. So, for most purposes, collisions of molecules in gases are consideredto be perfectly elastic.

As an interesting example, let us consider an elastic collision between twoobjects of equal mass. If they come together with the same speed, they wouldcome apart at that same speed, by symmetry. But now look at this in anothercircumstance, in which one of them is moving with velocity v and the other oneis at rest. What happens? We have been through this before. We watch thesymmetrical collision from a car moving along with one of the objects, and weﬁnd that if a stationary body is struck elastically by another body of exactly thesame mass, the moving body stops, and the one that was standing still now movesaway with the same speed that the other one had; the bodies simply exchangevelocities. This behavior can easily be demonstrated with a suitable impactapparatus. More generally, if both bodies are moving, with diﬀerent velocities,they simply exchange velocity at impact.

Another example of an almost elastic interaction is magnetism. If we arrangea pair of U-shaped magnets in our glide blocks, so that they repel each other,when one drifts quietly up to the other, it pushes it away and stands perfectlystill, and now the other goes along, frictionlessly.

The principle of conservation of momentum is very useful, because it enablesus to solve many problems without knowing the details. We did not know thedetails of the gas motions in the cap explosion, yet we could predict the velocitieswith which the bodies came apart, for example. Another interesting example isrocket propulsion. A rocket of large mass, M, ejects a small piece, of mass m,with a terriﬁc velocity V relative to the rocket. After this the rocket, if it wereoriginally standing still, will be moving with a small velocity, v. Using theprinciple of conservation of momentum, we can calculate this velocity to be

v = mM

· V.

So long as material is being ejected, the rocket continues to pick up speed. Rocketpropulsion is essentially the same as the recoil of a gun: there is no need for anyair to push against.

10-5 Relativistic momentumIn modern times the law of conservation of momentum has undergone certainmodiﬁcations. However, the law is still true today, the modiﬁcations being mainly

10-14

in the deﬁnitions of things. In the theory of relativity it turns out that we do haveconservation of momentum; the particles have mass and the momentum is stillgiven by mv, the mass times the velocity, but the mass changes with the velocity,hence the momentum also changes. The mass varies with velocity according tothe law

m0p1 − v2/c2 ,

m =

(10.7)

(10.8)

where m0 is the mass of the body at rest and c is the speed of light. It is easy tosee from the formula that there is negligible diﬀerence between m and m0 unlessv is very large, and that for ordinary velocities the expression for momentumreduces to the old formula.

The components of momentum for a single particle are written as

p1 − v2/c2 ,

m0vx

px =

p1 − v2/c2 ,

m0vy

py =

p1 − v2/c2 ,

m0vz

pz =

x

y

z

+ v2

+ v2

. If the x-components are summed over all the interactingwhere v2 = v2particles, both before and after a collision, the sums are equal; that is, momentumis conserved in the x-direction. The same holds true in any direction.

In Chapter 4 we saw that the law of conservation of energy is not valid unlesswe recognize that energy appears in diﬀerent forms, electrical energy, mechanicalenergy, radiant energy, heat energy, and so on. In some of these cases, heatenergy for example, the energy might be said to be「hidden.」This examplemight suggest the question,「Are there also hidden forms of momentum—perhapsheat momentum?」The answer is that it is very hard to hide momentum for thefollowing reasons.

The random motions of the atoms of a body furnish a measure of heat energy,if the squares of the velocities are summed. This sum will be a positive result,having no directional character. The heat is there, whether or not the body movesas a whole, and conservation of energy in the form of heat is not very obvious.On the other hand, if one sums the velocities, which have direction, and ﬁnds aresult that is not zero, that means that there is a drift of the entire body in someparticular direction, and such a gross momentum is readily observed. Thus thereis no random internal lost momentum, because the body has net momentum onlywhen it moves as a whole. Therefore momentum, as a mechanical quantity, isdiﬃcult to hide. Nevertheless, momentum can be hidden—in the electromagneticﬁeld, for example. This case is another eﬀect of relativity.

10-15

One of the propositions of Newton was that interactions at a distance areinstantaneous. It turns out that such is not the case; in situations involving elec-trical forces, for instance, if an electrical charge at one location is suddenly moved,the eﬀects on another charge, at another place, do not appear instantaneously—there is a little delay. In those circumstances, even if the forces are equal themomentum will not check out; there will be a short time during which there willbe trouble, because for a while the ﬁrst charge will feel a certain reaction force,say, and will pick up some momentum, but the second charge has felt nothingand has not yet changed its momentum. It takes time for the inﬂuence to crossthe intervening distance, which it does at 186,000 miles a second. In that tinytime the momentum of the particles is not conserved. Of course after the secondcharge has felt the eﬀect of the ﬁrst one and all is quieted down, the momentumequation will check out all right, but during that small interval momentum is notconserved. We represent this by saying that during this interval there is anotherkind of momentum besides that of the particle, mv, and that is momentum inthe electromagnetic ﬁeld. If we add the ﬁeld momentum to the momentum ofthe particles, then momentum is conserved at any moment all the time. Thefact that the electromagnetic ﬁeld can possess momentum and energy makes thatﬁeld very real, and so, for better understanding, the original idea that there arejust the forces between particles has to be modiﬁed to the idea that a particlemakes a ﬁeld, and a ﬁeld acts on another particle, and the ﬁeld itself has suchfamiliar properties as energy content and momentum, just as particles can have.To take another example: an electromagnetic ﬁeld has waves, which we call light;it turns out that light also carries momentum with it, so when light impingeson an object it carries in a certain amount of momentum per second; this isequivalent to a force, because if the illuminated object is picking up a certainamount of momentum per second, its momentum is changing and the situationis exactly the same as if there were a force on it. Light can exert pressure bybombarding an object; this pressure is very small, but with suﬃciently delicateapparatus it is measurable.

Now in quantum mechanics it turns out that momentum is a diﬀerent thing—it is no longer mv. It is hard to deﬁne exactly what is meant by the velocity of aparticle, but momentum still exists. In quantum mechanics the diﬀerence is thatwhen the particles are represented as particles, the momentum is still mv, butwhen the particles are represented as waves, the momentum is measured by thenumber of waves per centimeter: the greater this number of waves, the greaterthe momentum. In spite of the diﬀerences, the law of conservation of momentum

10-16

holds also in quantum mechanics. Even though the law F = ma is false, andall the derivations of Newton were wrong for the conservation of momentum, inquantum mechanics, nevertheless, in the end, that particular law maintains itself!

10-17

11

