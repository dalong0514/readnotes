Conservation of Momentum

10-1 Newton’s Third Law On the basis of Newton’s second law of motion, which gives the relation between the acceleration of any body and the force acting on it, any problem in mechanics can be solved in principle. For example, to determine the motion of a few particles, one can use the numerical method developed in the preceding chapter. But there are good reasons to make a further study of Newton’s laws. First, there are quite simple cases of motion which can be analyzed not only by numerical methods, but also by direct mathematical analysis. For example, although we know that the acceleration of a falling body is 32 ft/sec2, and from this fact could calculate the motion by numerical methods, it is much easier and more satisfactory to analyze the motion and ﬁnd the general solution, s = s0 + v0t + 16t2. In the same way, although we can work out the positions of a harmonic oscillator by numerical methods, it is also possible to show analytically that the general solution is a simple cosine function of t, and so it is unnecessary to go to all that arithmetical trouble when there is a simple and more accurate way to get the result. In the same manner, although the motion of one body around the sun, determined by gravitation, can be calculated point by point by the numerical methods of Chapter 9, which show the general shape of the orbit, it is nice also to get the exact shape, which analysis reveals as a perfect ellipse. Unfortunately, there are really very few problems which can be solved exactly by analysis. In the case of the harmonic oscillator, for example, if the spring force is not proportional to the displacement, but is something more complicated, one must fall back on the numerical method. Or if there are two bodies going around the sun, so that the total number of bodies is three, then analysis cannot produce a simple formula for the motion, and in practice the problem must be done numerically. That is the famous three-body problem, which so long challenged human powers of analysis; it is very interesting how long it took people to appreciate the fact that perhaps the powers of mathematical analysis

10-1

were limited and it might be necessary to use the numerical methods. Today an enormous number of problems that cannot be done analytically are solved by numerical methods, and the old three-body problem, which was supposed to be so diﬃcult, is solved as a matter of routine in exactly the same manner that was described in the preceding chapter, namely, by doing enough arithmetic. However, there are also situations where both methods fail: the simple problems we can do by analysis, and the moderately diﬃcult problems by numerical, arithmetical methods, but the very complicated problems we cannot do by either method. A complicated problem is, for example, the collision of two automobiles, or even the motion of the molecules of a gas. There are countless particles in a cubic millimeter of gas, and it would be ridiculous to try to make calculations with so many variables (about 1017—a hundred million billion). Anything like the motion of the molecules or atoms of a gas or a block or iron, or the motion of the stars in a globular cluster, instead of just two or three planets going around the sun—such problems we cannot do directly, so we have to seek other means. In the situations in which we cannot follow details, we need to know some general properties, that is, general theorems or principles which are consequences of Newton’s laws. One of these is the principle of conservation of energy, which was discussed in Chapter 4. Another is the principle of conservation of momentum, the subject of this chapter. Another reason for studying mechanics further is that there are certain patterns of motion that are repeated in many diﬀerent circumstances, so it is good to study these patterns in one particular circumstance. For example, we shall study collisions; diﬀerent kinds of collisions have much in common. In the ﬂow of ﬂuids, it does not make much diﬀerence what the ﬂuid is, the laws of the ﬂow are similar. Other problems that we shall study are vibrations and oscillations and, in particular, the peculiar phenomena of mechanical waves—sound, vibrations of rods, and so on.

In our discussion of Newton’s laws it was explained that these laws are a kind of program that says「Pay attention to the forces,」and that Newton told us only two things about the nature of forces. In the case of gravitation, he gave us the complete law of the force. In the case of the very complicated forces between atoms, he was not aware of the right laws for the forces; however, he discovered one rule, one general property of forces, which is expressed in his Third Law, and that is the total knowledge that Newton had about the nature of forces—the law of gravitation and this principle, but no other details.

This principle is that action equals reaction.

10-2

What is meant is something of this kind: Suppose we have two small bodies, say particles, and suppose that the ﬁrst one exerts a force on the second one, pushing it with a certain force. Then, simultaneously, according to Newton’s Third Law, the second particle will push on the ﬁrst with an equal force, in the opposite direction; furthermore, these forces eﬀectively act in the same line. This is the hypothesis, or law, that Newton proposed, and it seems to be quite accurate, though not exact (we shall discuss the errors later). For the moment we shall take it to be true that action equals reaction. Of course, if there is a third particle, not on the same line as the other two, the law does not mean that the total force on the ﬁrst one is equal to the total force on the second, since the third particle, for instance, exerts its own push on each of the other two. The result is that the total eﬀect on the ﬁrst two is in some other direction, and the forces on the ﬁrst two particles are, in general, neither equal nor opposite. However, the forces on each particle can be resolved into parts, there being one contribution or part due to each other interacting particle. Then each pair of particles has corresponding components of mutual interaction that are equal in magnitude and opposite in direction.

10-2 Conservation of momentum Now what are the interesting consequences of the above relationship? Suppose, for simplicity, that we have just two interacting particles, possibly of diﬀerent mass, and numbered 1 and 2. The forces between them are equal and opposite; what are the consequences? According to Newton’s Second Law, force is the time rate of change of the momentum, so we conclude that the rate of change of momentum p1 of particle 1 is equal to minus the rate of change of momentum p2 of particle 2, or (10.1) Now if the rate of change is always equal and opposite, it follows that the total change in the momentum of particle 1 is equal and opposite to the total change in the momentum of particle 2; this means that if we add the momentum of particle 1 to the momentum of particle 2, the rate of change of the sum of these, due to the mutual forces (called internal forces) between particles, is zero; that is (10.2) There is assumed to be no other force in the problem. If the rate of change of this sum is always zero, that is just another way of saying that the quantity (p1 + p2)

dp1/dt = −dp2/dt.

d(p1 + p2)/dt = 0.

10-3

does not change. (This quantity is also written m1v1 + m2v2, and is called the total momentum of the two particles.) We have now obtained the result that the total momentum of the two particles does not change because of any mutual interactions between them. This statement expresses the law of conservation of momentum in that particular example. We conclude that if there is any kind of force, no matter how complicated, between two particles, and we measure or calculate m1v1 + m2v2, that is, the sum of the two momenta, both before and after the forces act, the results should be equal, i.e., the total momentum is a constant.

If we extend the argument to three or more interacting particles in more complicated circumstances, it is evident that so far as internal forces are concerned, the total momentum of all the particles stays constant, since an increase in momentum of one, due to another, is exactly compensated by the decrease of the second, due to the ﬁrst. That is, all the internal forces will balance out, and therefore cannot change the total momentum of the particles. Then if there are no forces from the outside (external forces), there are no forces that can change the total momentum; hence the total momentum is a constant.

It is worth describing what happens if there are forces that do not come from the mutual actions of the particles in question: suppose we isolate the interacting particles. If there are only mutual forces, then, as before, the total momentum of the particles does not change, no matter how complicated the forces. On the other hand, suppose there are also forces coming from the particles outside the isolated group. Any force exerted by outside bodies on inside bodies, we call an external force. We shall later demonstrate that the sum of all external forces equals the rate of change of the total momentum of all the particles inside, a very useful theorem.

The conservation of the total momentum of a number of interacting particles

can be expressed as

m1v1 + m2v2 + m3v3 + ··· = a constant,

(10.3) if there are no net external forces. Here the masses and corresponding velocities of the particles are numbered 1, 2, 3, 4, . . . The general statement of Newton’s Second Law for each particle,

(10.4) is true speciﬁcally for the components of force and momentum in any given

F = d dt

(mv),

10-4

direction; thus the x-component of the force on a particle is equal to the x- component of the rate of change of momentum of that particle, or

Fx = d dt

(mvx),

(10.5)

and similarly for the y- and z-directions. Therefore Eq. (10.3) is really three equations, one for each direction. In addition to the law of conservation of momentum, there is another interest- ing consequence of Newton’s Second Law, to be proved later, but merely stated now. This principle is that the laws of physics will look the same whether we are standing still or moving with a uniform speed in a straight line. For example, a child bouncing a ball in an airplane ﬁnds that the ball bounces the same as though he were bouncing it on the ground. Even though the airplane is moving with a very high velocity, unless it changes its velocity, the laws look the same to the child as they do when the airplane is standing still. This is the so-called relativity principle. As we use it here we shall call it「Galilean relativity」to distinguish it from the more careful analysis made by Einstein, which we shall study later.

We have just derived the law of conservation of momentum from Newton’s laws, and we could go on from here to ﬁnd the special laws that describe impacts and collisions. But for the sake of variety, and also as an illustration of a kind of reasoning that can be used in physics in other circumstances where, for example, one might not know Newton’s laws and might take a diﬀerent approach, we shall discuss the laws of impacts and collisions from a completely diﬀerent point of view. We shall base our discussion on the principle of Galilean relativity, stated above, and shall end up with the law of conservation of momentum.

We shall start by assuming that nature would look the same if we run along at a certain speed and watch it as it would if we were standing still. Before discussing collisions in which two bodies collide and stick together, or come together and bounce apart, we shall ﬁrst consider two bodies that are held together by a spring or something else, and are then suddenly released and pushed by the spring or perhaps by a little explosion. Further, we shall consider motion in only one direction. First, let us suppose that the two objects are exactly the same, are nice symmetrical objects, and then we have a little explosion between them. After the explosion, one of the bodies will be moving, let us say toward the right, with a velocity v. Then it appears reasonable that the other body is moving toward the left with a velocity v, because if the objects are alike there is no reason for right

10-5

or left to be preferred and so the bodies would do something that is symmetrical. This is an illustration of a kind of thinking that is very useful in many problems but would not be brought out if we just started with the formulas.

The ﬁrst result from our experiment is that equal objects will have equal speed, but now suppose that we have two objects made of diﬀerent materials, say copper and aluminum, and we make the two masses equal. We shall now suppose that if we do the experiment with two masses that are equal, even though the objects are not identical, the velocities will be equal. Someone might object:「But you know, you could do it backwards, you did not have to suppose that. You could deﬁne equal masses to mean two masses that acquire equal velocities in this experiment.」We follow that suggestion and make a little explosion between the copper and a very large piece of aluminum, so heavy that the copper ﬂies out and the aluminum hardly budges. That is too much aluminum, so we reduce the amount until there is just a very tiny piece, then when we make the explosion the aluminum goes ﬂying away, and the copper hardly budges. That is not enough aluminum. Evidently there is some right amount in between; so we keep adjusting the amount until the velocities come out equal. Very well then—let us turn it around, and say that when the velocities are equal, the masses are equal. This appears to be just a deﬁnition, and it seems remarkable that we can transform physical laws into mere deﬁnitions. Nevertheless, there are some physical laws involved, and if we accept this deﬁnition of equal masses, we immediately ﬁnd one of the laws, as follows.

Suppose we know from the foregoing experiment that two pieces of matter, A and B (of copper and aluminum), have equal masses, and we compare a third body, say a piece of gold, with the copper in the same manner as above, making sure that its mass is equal to the mass of the copper. If we now make the experiment between the aluminum and the gold, there is nothing in logic that says these masses must be equal; however, the experiment shows that they actually are. So now, by experiment, we have found a new law. A statement of this law might be: If two masses are each equal to a third mass (as determined by equal velocities in this experiment), then they are equal to each other. (This statement does not follow at all from a similar statement used as a postulate regarding mathematical quantities.) From this example we can see how quickly we start to infer things if we are careless. It is not just a deﬁnition to say the masses are equal when the velocities are equal, because to say the masses are equal is to imply the mathematical laws of equality, which in turn makes a prediction about an experiment.

10-6

As a second example, suppose that A and B are found to be equal by doing the experiment with one strength of explosion, which gives a certain velocity; if we then use a stronger explosion, will it be true or not true that the velocities now obtained are equal? Again, in logic there is nothing that can decide this question, but experiment shows that it is true. So, here is another law, which might be stated: If two bodies have equal masses, as measured by equal velocities at one velocity, they will have equal masses when measured at another velocity. From these examples we see that what appeared to be only a deﬁnition really involved some laws of physics.

In the development that follows we shall assume it is true that equal masses have equal and opposite velocities when an explosion occurs between them. We shall make another assumption in the inverse case: If two identical objects, moving in opposite directions with equal velocities, collide and stick together by some kind of glue, then which way will they be moving after the collision? This is again a symmetrical situation, with no preference between right and left, so we assume that they stand still. We shall also suppose that any two objects of equal mass, even if the objects are made of diﬀerent materials, which collide and stick together, when moving with the same velocity in opposite directions will come to rest after the collision.

10-3 Momentum is conserved! We can verify the above assumptions experimentally: ﬁrst, that if two sta- tionary objects of equal mass are separated by an explosion they will move apart with the same speed, and second, if two objects of equal mass, coming together with the same speed, collide and stick together they will stop. This we can do by means of a marvelous invention called an air trough,* which gets rid of friction, the thing which continually bothered Galileo (Fig. 10-1). He could not

Fig. 10-1. End view of linear air trough.

* H. V. Neher and R. B. Leighton, Amer. Jour. of Phys. 31, 255 (1963).

10-7

Fig. 10-2. Sectional view of gliders with explosive interaction cylinder

attachment.

do experiments by sliding things because they do not slide freely, but, by adding a magic touch, we can today get rid of friction. Our objects will slide without diﬃculty, on and on at a constant velocity, as advertised by Galileo. This is done by supporting the objects on air. Because air has very low friction, an object glides along with practically constant velocity when there is no applied force. First, we use two glide blocks which have been made carefully to have the same weight, or mass (their weight was measured really, but we know that this weight is proportional to the mass), and we place a small explosive cap in a closed cylinder between the two blocks (Fig. 10-2). We shall start the blocks from rest at the center point of the track and force them apart by exploding the cap with an electric spark. What should happen? If the speeds are equal when they ﬂy apart, they should arrive at the ends of the trough at the same time. On reaching the ends they will both bounce back with practically opposite velocity, and will come together and stop at the center where they started. It is a good test; when it is actually done the result is just as we have described (Fig. 10-3).

Fig. 10-3. Schematic view of action-reaction experiment with equal

masses.

10-8

Fig. 10-4. Two views of an inelastic collision between equal masses.

Now the next thing we would like to ﬁgure out is what happens in a less simple situation. Suppose we have two equal masses, one moving with velocity v and the other standing still, and they collide and stick; what is going to happen? There is a mass 2m altogether when we are ﬁnished, drifting with an unknown velocity. What velocity? That is the problem. To ﬁnd the answer, we make the assumption that if we ride along in a car, physics will look the same as if we are standing still. We start with the knowledge that two equal masses, moving in opposite directions with equal speeds v, will stop dead when they collide. Now suppose that while this happens, we are riding by in an automobile, at a velocity −v. Then what does it look like? Since we are riding along with one of the two masses which are coming together, that one appears to us to have zero velocity. The other mass, however, going the other way with velocity v, will appear to be coming toward us at a velocity 2v (Fig. 10-4). Finally, the combined masses after collision will seem to be passing by with velocity v. We therefore conclude that an object with velocity 2v, hitting an equal one at rest, will end up with velocity v, or what is mathematically exactly the same, an object with velocity v hitting and sticking to one at rest will produce an object moving with velocity v/2. Note that if we multiply the mass and the velocity beforehand and add them together, mv + 0, we get the same answer as when we multiply the mass and the velocity of everything afterwards, 2m times v/2. So that tells us what happens when a mass of velocity v hits one standing still.

In exactly the same manner we can deduce what happens when equal objects

having any two velocities hit each other.

Suppose we have two equal bodies with velocities v1 and v2, respectively, which collide and stick together. What is their velocity v after the collision? Again we ride by in an automobile, say at velocity v2, so that one body appears to be at rest. The other then appears to have a velocity v1 − v2, and we have the same case that we had before. When it is all ﬁnished they will be moving

10-9

Fig. 10-5. Two views of another inelastic collision between equal

masses.

at 1 ground?

2(v1 − v2) + v2 or 1

2(v1 − v2) with respect to the car. What then is the actual speed on the It is v = 1

2(v1 + v2) (Fig. 10-5). Again we note that

mv1 + mv2 = 2m(v1 + v2)/2.

(10.6)

Thus, using this principle, we can analyze any kind of collision in which two bodies of equal mass hit each other and stick. In fact, although we have worked only in one dimension, we can ﬁnd out a great deal about much more complicated collisions by imagining that we are riding by in a car in some oblique direction. The principle is the same, but the details get somewhat complicated.

In order to test experimentally whether an object moving with velocity v, colliding with an equal one at rest, forms an object moving with velocity v/2, we may perform the following experiment with our air-trough apparatus. We place in the trough three equally massive objects, two of which are initially joined together with our explosive cylinder device, the third being very near to but slightly separated from these and provided with a sticky bumper so that it will stick to another object which hits it. Now, a moment after the explosion, we have two objects of mass m moving with equal and opposite velocities v. A moment after that, one of these collides with the third object and makes an object of mass 2m moving, so we believe, with velocity v/2. How do we test whether it is really v/2? By arranging the initial positions of the masses on the trough so that the distances to the ends are not equal, but are in the ratio 2 : 1. Thus our ﬁrst mass, which continues to move with velocity v, should cover twice as much distance in a given time as the two which are stuck together (allowing for the small distance travelled by the second object before it collided with the third). The mass m and the mass 2m should reach the ends at the same time, and when we try it, we ﬁnd that they do (Fig. 10-6).

10-10

Fig. 10-6. An experiment to verify that a mass m with velocity v

striking a mass m with zero velocity gives 2m with velocity v/2.

The next problem that we want to work out is what happens if we have two diﬀerent masses. Let us take a mass m and a mass 2m and apply our explosive interaction. What will happen then? If, as a result of the explosion, m moves with velocity v, with what velocity does 2m move? The experiment we have just done may be repeated with zero separation between the second and third masses, and when we try it we get the same result, namely, the reacting masses m and 2m attain velocities −v and v/2. Thus the direct reaction between m and 2m gives the same result as the symmetrical reaction between m and m, followed by a collision between m and a third mass m in which they stick together. Furthermore, we ﬁnd that the masses m and 2m returning from the ends of the trough, with their velocities (nearly) exactly reversed, stop dead if they stick together.

Now the next question we may ask is this. What will happen if a mass m with velocity v, say, hits and sticks to another mass 2m at rest? This is very easy to answer using our principle of Galilean relativity, for we simply watch the collision which we have just described from a car moving with velocity −v/2 (Fig. 10-7). From the car, the velocities are

and

1 = v − v(car) = v + v/2 = 3v/2 v0

2 = −v/2 − v(car) = −v/2 + v/2 = 0. v0

After the collision, the mass 3m appears to us to be moving with velocity v/2. Thus we have the answer, i.e., the ratio of velocities before and after collision is 3 to 1: if an object of mass m collides with a stationary object of mass 2m, then the whole thing moves oﬀ, stuck together, with a velocity 1/3 as much. The general rule again is that the sum of the products of the masses and the velocities

10-11

Fig. 10-7. Two views of an inelastic collision between m and 2m.

stays the same: mv + 0 equals 3m times v/3, so we are gradually building up the theorem of the conservation of momentum, piece by piece. Now we have one against two. Using the same arguments, we can predict the result of one against three, two against three, etc. The case of two against three, starting from rest, is shown in Fig. 10-8.

Fig. 10-8. Action and reaction between 2m and 3m.

In every case we ﬁnd that the mass of the ﬁrst object times its velocity, plus the mass of the second object times its velocity, is equal to the total mass of the ﬁnal object times its velocity. These are all examples, then, of the conservation of momentum. Starting from simple, symmetrical cases, we have demonstrated the law for more complex cases. We could, in fact, do it for any rational mass ratio, and since every ratio is exceedingly close to a rational ratio, we can handle every ratio as precisely as we wish.

10-4 Momentum and energy All the foregoing examples are simple cases where the bodies collide and stick together, or were initially stuck together and later separated by an explosion.

10-12

However, there are situations in which the bodies do not cohere, as, for example, two bodies of equal mass which collide with equal speeds and then rebound. For a brief moment they are in contact and both are compressed. At the instant of maximum compression they both have zero velocity and energy is stored in the elastic bodies, as in a compressed spring. This energy is derived from the kinetic energy the bodies had before the collision, which becomes zero at the instant their velocity is zero. The loss of kinetic energy is only momentary, however. The compressed condition is analogous to the cap that releases energy in an explosion. The bodies are immediately decompressed in a kind of explosion, and ﬂy apart again; but we already know that case—the bodies ﬂy apart with equal speeds. However, this speed of rebound is less, in general, than the initial speed, because not all the energy is available for the explosion, depending on the material. If the material is putty no kinetic energy is recovered, but if it is something more rigid, some kinetic energy is usually regained. In the collision the rest of the kinetic energy is transformed into heat and vibrational energy—the bodies are hot and vibrating. The vibrational energy also is soon transformed into heat. It is possible to make the colliding bodies from highly elastic materials, such as steel, with carefully designed spring bumpers, so that the collision generates very little heat and vibration. In these circumstances the velocities of rebound are practically equal to the initial velocities; such a collision is called elastic. That the speeds before and after an elastic collision are equal is not a matter of conservation of momentum, but a matter of conservation of kinetic energy. That the velocities of the bodies rebounding after a symmetrical collision are equal to and opposite each other, however, is a matter of conservation of momentum. We might similarly analyze collisions between bodies of diﬀerent masses, diﬀerent initial velocities, and various degrees of elasticity, and determine the ﬁnal velocities and the loss of kinetic energy, but we shall not go into the details of these processes.

Elastic collisions are especially interesting for systems that have no internal「gears, wheels, or parts.」Then when there is a collision there is nowhere for the energy to be impounded, because the objects that move apart are in the same condition as when they collided. Therefore, between very elementary objects, the collisions are always elastic or very nearly elastic. For instance, the collisions between atoms or molecules in a gas are said to be perfectly elastic. Although this is an excellent approximation, even such collisions are not perfectly elastic; otherwise one could not understand how energy in the form of light or heat radiation could come out of a gas. Once in a while, in a gas collision, a low-energy

10-13

infrared ray is emitted, but this occurrence is very rare and the energy emitted is very small. So, for most purposes, collisions of molecules in gases are considered to be perfectly elastic.

As an interesting example, let us consider an elastic collision between two objects of equal mass. If they come together with the same speed, they would come apart at that same speed, by symmetry. But now look at this in another circumstance, in which one of them is moving with velocity v and the other one is at rest. What happens? We have been through this before. We watch the symmetrical collision from a car moving along with one of the objects, and we ﬁnd that if a stationary body is struck elastically by another body of exactly the same mass, the moving body stops, and the one that was standing still now moves away with the same speed that the other one had; the bodies simply exchange velocities. This behavior can easily be demonstrated with a suitable impact apparatus. More generally, if both bodies are moving, with diﬀerent velocities, they simply exchange velocity at impact.

Another example of an almost elastic interaction is magnetism. If we arrange a pair of U-shaped magnets in our glide blocks, so that they repel each other, when one drifts quietly up to the other, it pushes it away and stands perfectly still, and now the other goes along, frictionlessly.

The principle of conservation of momentum is very useful, because it enables us to solve many problems without knowing the details. We did not know the details of the gas motions in the cap explosion, yet we could predict the velocities with which the bodies came apart, for example. Another interesting example is rocket propulsion. A rocket of large mass, M, ejects a small piece, of mass m, with a terriﬁc velocity V relative to the rocket. After this the rocket, if it were originally standing still, will be moving with a small velocity, v. Using the principle of conservation of momentum, we can calculate this velocity to be

v = m M

· V.

So long as material is being ejected, the rocket continues to pick up speed. Rocket propulsion is essentially the same as the recoil of a gun: there is no need for any air to push against.

10-5 Relativistic momentum In modern times the law of conservation of momentum has undergone certain modiﬁcations. However, the law is still true today, the modiﬁcations being mainly

10-14

in the deﬁnitions of things. In the theory of relativity it turns out that we do have conservation of momentum; the particles have mass and the momentum is still given by mv, the mass times the velocity, but the mass changes with the velocity, hence the momentum also changes. The mass varies with velocity according to the law

m0p1 − v2/c2 ,

m =

(10.7)

(10.8)

where m0 is the mass of the body at rest and c is the speed of light. It is easy to see from the formula that there is negligible diﬀerence between m and m0 unless v is very large, and that for ordinary velocities the expression for momentum reduces to the old formula.

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

. If the x-components are summed over all the interacting where v2 = v2 particles, both before and after a collision, the sums are equal; that is, momentum is conserved in the x-direction. The same holds true in any direction.

In Chapter 4 we saw that the law of conservation of energy is not valid unless we recognize that energy appears in diﬀerent forms, electrical energy, mechanical energy, radiant energy, heat energy, and so on. In some of these cases, heat energy for example, the energy might be said to be「hidden.」This example might suggest the question,「Are there also hidden forms of momentum—perhaps heat momentum?」The answer is that it is very hard to hide momentum for the following reasons.

The random motions of the atoms of a body furnish a measure of heat energy, if the squares of the velocities are summed. This sum will be a positive result, having no directional character. The heat is there, whether or not the body moves as a whole, and conservation of energy in the form of heat is not very obvious. On the other hand, if one sums the velocities, which have direction, and ﬁnds a result that is not zero, that means that there is a drift of the entire body in some particular direction, and such a gross momentum is readily observed. Thus there is no random internal lost momentum, because the body has net momentum only when it moves as a whole. Therefore momentum, as a mechanical quantity, is diﬃcult to hide. Nevertheless, momentum can be hidden—in the electromagnetic ﬁeld, for example. This case is another eﬀect of relativity.

10-15

One of the propositions of Newton was that interactions at a distance are instantaneous. It turns out that such is not the case; in situations involving elec- trical forces, for instance, if an electrical charge at one location is suddenly moved, the eﬀects on another charge, at another place, do not appear instantaneously— there is a little delay. In those circumstances, even if the forces are equal the momentum will not check out; there will be a short time during which there will be trouble, because for a while the ﬁrst charge will feel a certain reaction force, say, and will pick up some momentum, but the second charge has felt nothing and has not yet changed its momentum. It takes time for the inﬂuence to cross the intervening distance, which it does at 186,000 miles a second. In that tiny time the momentum of the particles is not conserved. Of course after the second charge has felt the eﬀect of the ﬁrst one and all is quieted down, the momentum equation will check out all right, but during that small interval momentum is not conserved. We represent this by saying that during this interval there is another kind of momentum besides that of the particle, mv, and that is momentum in the electromagnetic ﬁeld. If we add the ﬁeld momentum to the momentum of the particles, then momentum is conserved at any moment all the time. The fact that the electromagnetic ﬁeld can possess momentum and energy makes that ﬁeld very real, and so, for better understanding, the original idea that there are just the forces between particles has to be modiﬁed to the idea that a particle makes a ﬁeld, and a ﬁeld acts on another particle, and the ﬁeld itself has such familiar properties as energy content and momentum, just as particles can have. To take another example: an electromagnetic ﬁeld has waves, which we call light; it turns out that light also carries momentum with it, so when light impinges on an object it carries in a certain amount of momentum per second; this is equivalent to a force, because if the illuminated object is picking up a certain amount of momentum per second, its momentum is changing and the situation is exactly the same as if there were a force on it. Light can exert pressure by bombarding an object; this pressure is very small, but with suﬃciently delicate apparatus it is measurable.

Now in quantum mechanics it turns out that momentum is a diﬀerent thing— it is no longer mv. It is hard to deﬁne exactly what is meant by the velocity of a particle, but momentum still exists. In quantum mechanics the diﬀerence is that when the particles are represented as particles, the momentum is still mv, but when the particles are represented as waves, the momentum is measured by the number of waves per centimeter: the greater this number of waves, the greater the momentum. In spite of the diﬀerences, the law of conservation of momentum

10-16

holds also in quantum mechanics. Even though the law F = ma is false, and all the derivations of Newton were wrong for the conservation of momentum, in quantum mechanics, nevertheless, in the end, that particular law maintains itself!

10-17

11

