Rotation in Two Dimensions

18-1 The center of mass In the previous chapters we have been studying the mechanics of points, or small particles whose internal structure does not concern us. For the next few chapters we shall study the application of Newton’s laws to more complicated things. When the world becomes more complicated, it also becomes more interesting, and we shall ﬁnd that the phenomena associated with the mechanics of a more complex object than just a point are really quite striking. Of course these phenomena involve nothing but combinations of Newton’s laws, but it is sometimes hard to believe that only F = ma is at work. The more complicated objects we deal with can be of several kinds: water ﬂowing, galaxies whirling, and so on. The simplest「complicated」object to analyze, at the start, is what we call a rigid body, a solid object that is turning as it moves about. However, even such a simple object may have a most complex motion, and we shall therefore ﬁrst consider the simplest aspects of such motion, in which an extended body rotates about a ﬁxed axis. A given point on such a body then moves in a plane perpendicular to this axis. Such rotation of a body about a ﬁxed axis is called plane rotation or rotation in two dimensions. We shall later generalize the results to three dimensions, but in doing so we shall ﬁnd that, unlike the case of ordinary particle mechanics, rotations are subtle and hard to understand unless we ﬁrst get a solid grounding in two dimensions.

The ﬁrst interesting theorem concerning the motion of complicated objects can be observed at work if we throw an object made of a lot of blocks and spokes, held together by strings, into the air. Of course we know it goes in a parabola, because we studied that for a particle. But now our object is not a particle; it wobbles and it jiggles, and so on. It does go in a parabola though; one can see that. What goes in a parabola? Certainly not the point on the corner of the block, because that is jiggling about; neither is it the end of the wooden stick,

18-1

or the middle of the wooden stick, or the middle of the block. But something goes in a parabola, there is an eﬀective「center」which moves in a parabola. So our ﬁrst theorem about complicated objects is to demonstrate that there is a mean position which is mathematically deﬁnable, but not necessarily a point of the material itself, which goes in a parabola. That is called the theorem of the center of the mass, and the proof of it is as follows.

We may consider any object as being made of lots of little particles, the atoms, with various forces among them. Let i represent an index which deﬁnes one of the particles. (There are millions of them, so i goes to 1023, or something.) Then the force on the ith particle is, of course, the mass times the acceleration of that particle:

F i = mi(d2ri/dt2).

(18.1) In the next few chapters our moving objects will be ones in which all the parts are moving at speeds very much slower than the speed of light, and we shall use the nonrelativistic approximation for all quantities. In these circumstances the mass is constant, so that

F i = d2(miri)/dt2.

(18.2)

If we now add the force on all the particles, that is, if we take the sum of all the F i’s for all the diﬀerent indexes, we get the total force, F . On the other side of the equation, we get the same thing as though we added before the diﬀerentiation:

.

(18.3)

F i = F = d2(P

i miri) dt2

X

i

Therefore the total force is the second derivative of the masses times their positions, added together.

Now the total force on all the particles is the same as the external force. Why? Although there are all kinds of forces on the particles because of the strings, the wigglings, the pullings and pushings, and the atomic forces, and who knows what, and we have to add all these together, we are rescued by Newton’s Third Law. Between any two particles the action and reaction are equal, so that when we add all the equations together, if any two particles have forces between them it cancels out in the sum; therefore the net result is only those forces which arise from other particles which are not included in whatever object we decide to sum over. So if Eq. (18.3) is the sum over a certain number of the particles, which

18-2

together are called「the object,」then the external force on the total object is equal to the sum of all the forces on all its constituent particles.

Now it would be nice if we could write Eq. (18.3) as the total mass times some acceleration. We can. Let us say M is the sum of all the masses, i.e., the total mass. Then if we deﬁne a certain vector R to be

R =X

miri/M,

(18.4)

(18.5)

Eq. (18.3) will be simply

i

F = d2(M R)/dt2 = M(d2R/dt2),

since M is a constant. Thus we ﬁnd that the external force is the total mass times the acceleration of an imaginary point whose location is R. This point is called the center of mass of the body. It is a point somewhere in the「middle」of the object, a kind of average r in which the diﬀerent ri’s have weights or importances proportional to the masses. We shall discuss this important theorem in more detail in a later chapter, and we shall therefore limit our remarks to two points: First, if the external forces are zero, if the object were ﬂoating in empty space, it might whirl, and jiggle, and twist, and do all kinds of things. But the center of mass, this artiﬁcially invented, calculated position, somewhere in the middle, will move with a constant velocity. In particular, if it is initially at rest, it will stay at rest. So if we have some kind of a box, perhaps a space ship, with people in it, and we calculate the location of the center of mass and ﬁnd it is standing still, then the center of mass will continue to stand still if no external forces are acting on the box. Of course, the space ship may move a little in space, but that is because the people are walking back and forth inside; when one walks toward the front, the ship goes toward the back so as to keep the average position of all the masses in exactly the same place.

Is rocket propulsion therefore absolutely impossible because one cannot move the center of mass? No; but of course we ﬁnd that to propel an interesting part of the rocket, an uninteresting part must be thrown away. In other words, if we start with a rocket at zero velocity and we spit some gas out the back end, then this little blob of gas goes one way as the rocket ship goes the other, but the center of mass is still exactly where it was before. So we simply move the part that we are interested in against the part we are not interested in.

18-3

The second point concerning the center of mass, which is the reason we introduced it into our discussion at this time, is that it may be treated separately from the「internal」motions of an object, and may therefore be ignored in our discussion of rotation.

18-2 Rotation of a rigid body Now let us discuss rotations. Of course an ordinary object does not simply rotate, it wobbles, shakes, and bends, so to simplify matters we shall discuss the motion of a nonexistent ideal object which we call a rigid body. This means an object in which the forces between the atoms are so strong, and of such character, that the little forces that are needed to move it do not bend it. Its shape stays essentially the same as it moves about. If we wish to study the motion of such a body, and agree to ignore the motion of its center of mass, there is only one thing left for it to do, and that is to turn. We have to describe that. How? Suppose there is some line in the body which stays put (perhaps it includes the center of mass and perhaps not), and the body is rotating about this particular line as an axis. How do we deﬁne the rotation? That is easy enough, for if we mark a point somewhere on the object, anywhere except on the axis, we can always tell exactly where the object is, if we only know where this point has gone to. The only thing needed to describe the position of that point is an angle. So rotation consists of a study of the variations of the angle with time. In order to study rotation, we observe the angle through which a body has turned. Of course, we are not referring to any particular angle inside the object itself; it is not that we draw some angle on the object. We are talking about the angular change of the position of the whole thing, from one time to another. First, let us study the kinematics of rotations. The angle will change with time, and just as we talked about position and velocity in one dimension, we may talk about angular position and angular velocity in plane rotation. In fact, there is a very interesting relationship between rotation in two dimensions and one-dimensional displacement, in which almost every quantity has its analog. First, we have the angle θ which deﬁnes how far the body has gone around; this replaces the distance y, which deﬁnes how far it has gone along. In the same manner, we have a velocity of turning, ω = dθ/dt, which tells us how much the angle changes in a second, just as v = ds/dt describes how fast a thing moves, or how far it moves in a second. If the angle is measured in radians, then the angular velocity ω will be so and so many radians per second. The greater the

18-4

angular velocity, the faster the object is turning, the faster the angle changes. We can go on: we can diﬀerentiate the angular velocity with respect to time, and we can call α = dω/dt = d2θ/dt2 the angular acceleration. That would be the analog of the ordinary acceleration.

Fig. 18-1. Kinematics of two-dimensional rotation.

Now of course we shall have to relate the dynamics of rotation to the laws of dynamics of the particles of which the object is made, so we must ﬁnd out how a particular particle moves when the angular velocity is such and such. To do this, let us take a certain particle which is located at a distance r from the axis and say it is in a certain location P(x, y) at a given instant, in the usual manner (Fig. 18-1). If at a moment ∆t later the angle of the whole object has turned through ∆θ, then this particle is carried with it. It is at the same radius away from O as it was before, but is carried to Q. The ﬁrst thing we would like to know is how much the distance x changes and how much the distance y changes. If OP is called r, then the length P Q is r ∆θ, because of the way angles are deﬁned. The change in x, then, is simply the projection of r ∆θ in the x-direction:

∆x = −P Q sin θ = −r ∆θ · (y/r) = −y ∆θ.

(18.6)

Similarly,

(18.7) If the object is turning with a given angular velocity ω, we ﬁnd, by dividing both sides of (18.6) and (18.7) by ∆t, that the velocity of the particle is

∆y = +x ∆θ.

vx = −ωy

and

vy = +ωx.

Of course if we want to ﬁnd the magnitude of the velocity, we just write

(18.8)

(18.9)

v =q

=p

v2 x

+ v2

y

ω2y2 + ω2x2 = ω

x2 + y2 = ωr.

p

18-5

It should not be mysterious that the value of the magnitude of this velocity is ωr; in fact, it should be self-evident, because the distance that it moves is r ∆θ and the distance it moves per second is r ∆θ/∆t, or rω. Let us now move on to consider the dynamics of rotation. Here a new concept, force, must be introduced. Let us inquire whether we can invent something which we shall call the torque (L. torquere, to twist) which bears the same relationship to rotation as force does to linear movement. A force is the thing that is needed to make linear motion, and the thing that makes something rotate is a「rotary force」or a「twisting force,」i.e., a torque. Qualitatively, a torque is a「twist」; what is a torque quantitatively? We shall get to the theory of torques quantitatively by studying the work done in turning an object, for one very nice way of deﬁning a force is to say how much work it does when it acts through a given displacement. We are going to try to maintain the analogy between linear and angular quantities by equating the work that we do when we turn something a little bit when there are forces acting on it, to the torque times the angle it turns through. In other words, the deﬁnition of the torque is going to be so arranged that the theorem of work has an absolute analog: force times distance is work, and torque times angle is going to be work. That tells us what torque is. Consider, for instance, a rigid body of some kind with various forces acting on it, and an axis about which the body rotates. Let us at ﬁrst concentrate on one force and suppose that this force is applied at a certain point (x, y). How much work would be done if we were to turn the object through a very small angle? That is easy. The work done is

We need only to substitute Eqs. (18.6) and (18.7) for ∆x and ∆y to obtain

∆W = Fx ∆x + Fy ∆y.

(18.10)

∆W = (xFy − yFx)∆θ.

(18.11) That is, the amount of work that we have done is, in fact, equal to the angle through which we have turned the object, multiplied by a strange-looking combi- nation of the force and the distance. This「strange combination」is what we call the torque. So, deﬁning the change in work as the torque times the angle, we now have the formula for torque in terms of the forces. (Obviously, torque is not a completely new idea independent of Newtonian mechanics—torque must have a deﬁnite deﬁnition in terms of the force.)

When there are several forces acting, the work that is done is, of course, the sum of the works done by all the forces, so that ∆W will be a whole lot of terms,

18-6

all added together, for all the forces, each of which is proportional, however, to ∆θ. We can take the ∆θ outside and therefore can say that the change in the work is equal to the sum of all the torques due to all the diﬀerent forces that are acting, times ∆θ. This sum we might call the total torque, τ. Thus torques add by the ordinary laws of algebra, but we shall later see that this is only because we are working in a plane. It is like one-dimensional kinematics, where the forces simply add algebraically, but only because they are all in the same direction. It is more complicated in three dimensions. Thus, for two-dimensional rotation,

and

τi = xiFyi − yiFxi

τ =X

τi.

(18.12)

(18.13)

It must be emphasized that the torque is about a given axis. If a diﬀerent axis is chosen, so that all the xi and yi are changed, the value of the torque is (usually) changed too. Now we pause brieﬂy to note that our foregoing introduction of torque, through the idea of work, gives us a most important result for an object in equilibrium: if all the forces on an object are in balance both for translation and rotation, not only is the net force zero, but the total of all the torques is also zero, because if an object is in equilibrium, no work is done by the forces for a small displacement. Therefore, since ∆W = τ ∆θ = 0, the sum of all the torques must be zero. So there are two conditions for equilibrium: that the sum of the forces is zero, and that the sum of the torques is zero. Prove that it suﬃces to be sure that the sum of torques about any one axis (in two dimensions) is zero. Now let us consider a single force, and try to ﬁgure out, geometrically, what this strange thing xFy − yFx amounts to. In Fig. 18-2 we see a force F acting at a point r. When the object has rotated through a small angle ∆θ, the work done, of course, is the component of force in the direction of the displacement times the

Fig. 18-2. The torque produced by a force.

18-7

displacement. In other words, it is only the tangential component of the force that counts, and this must be multiplied by the distance r ∆θ. Therefore we see that the torque is also equal to the tangential component of force (perpendicular to the radius) times the radius. That makes sense in terms of our ordinary idea of the torque, because if the force were completely radial, it would not put any「twist」on the body; it is evident that the twisting eﬀect should involve only the part of the force which is not pulling out from the center, and that means the tangential component. Furthermore, it is clear that a given force is more eﬀective on a long arm than near the axis. In fact, if we take the case where we push right on the axis, we are not twisting at all! So it makes sense that the amount of twist, or torque, is proportional both to the radial distance and to the tangential component of the force.

There is still a third formula for the torque which is very interesting. We have just seen that the torque is the force times the radius times the sine of the angle α, in Fig. 18-2. But if we extend the line of action of the force and draw the line OS, the perpendicular distance to the line of action of the force (the lever arm of the force) we notice that this lever arm is shorter than r in just the same proportion as the tangential part of the force is less than the total force. Therefore the formula for the torque can also be written as the magnitude of the force times the length of the lever arm.

The torque is also often called the moment of the force. The origin of this term is obscure, but it may be related to the fact that「moment」is derived from the Latin movimentum, and that the capability of a force to move an object (using the force on a lever or crowbar) increases with the length of the lever arm. In mathematics「moment」means weighted by how far away it is from an axis.

18-3 Angular momentum Although we have so far considered only the special case of a rigid body, the properties of torques and their mathematical relationships are interesting also even when an object is not rigid. In fact, we can prove a very remarkable theorem: just as external force is the rate of change of a quantity p, which we call the total momentum of a collection of particles, so the external torque is the rate of change of a quantity L which we call the angular momentum of the group of particles. To prove this, we shall suppose that there is a system of particles on which there are some forces acting and ﬁnd out what happens to the system as a result

18-8

Fig. 18-3. A particle moves about an axis O.

of the torques due to these forces. First, of course, we should consider just one particle. In Fig. 18-3 is one particle of mass m, and an axis O; the particle is not necessarily rotating in a circle about O, it may be moving in an ellipse, like a planet going around the sun, or in some other curve. It is moving somehow, and there are forces on it, and it accelerates according to the usual formula that the x-component of force is the mass times the x-component of acceleration, etc. But let us see what the torque does. The torque equals xFy − yFx, and the force in the x- or y-direction is the mass times the acceleration in the x- or y-direction:

τ = xFy − yFx = = xm(d2y/dt2) − ym(d2x/dt2).

(18.14) Now, although this does not appear to be the derivative of any simple quantity, it is in fact the derivative of the quantity xm(dy/dt) − ym(dx/dt):

(cid:20)

d dt

xm

(cid:18) dy

(cid:19)

dt

− ym

(cid:19)(cid:21) (cid:18) dx (cid:19) (cid:18) d2x

dt

−

dt2

(cid:19) (cid:18) d2y (cid:19) (cid:18) dx (cid:19)

dt2

m

+

= xm

(cid:18) dy

dt

dt

(cid:18) dx

dt

= xm

(cid:19)

(cid:18) dy (cid:19) (cid:19) (cid:18) d2y

dt

m

dt2

−ym

(cid:18) d2x

dt2

(cid:19)

.

(18.15)

− ym

So it is true that the torque is the rate of change of something with time! So we pay attention to the「something,」we give it a name: we call it L, the angular momentum:

L = xm(dy/dt) − ym(dx/dt)

(18.16) Although our present discussion is nonrelativistic, the second form for L given above is relativistically correct. So we have found that there is also a rotational

= xpy − ypx.

18-9

analog for the momentum, and that this analog, the angular momentum, is given by an expression in terms of the components of linear momentum that is just like the formula for torque in terms of the force components! Thus, if we want to know the angular momentum of a particle about an axis, we take only the component of the momentum that is tangential, and multiply it by the radius. In other words, what counts for angular momentum is not how fast it is going away from the origin, but how much it is going around the origin. Only the tangential part of the momentum counts for angular momentum. Furthermore, the farther out the line of the momentum extends, the greater the angular momentum. And also, because the geometrical facts are the same whether the quantity is labeled p or F, it is true that there is a lever arm (not the same as the lever arm of the force on the particle!) which is obtained by extending the line of the momentum and ﬁnding the perpendicular distance to the axis. Thus the angular momentum is the magnitude of the momentum times the momentum lever arm. So we have three formulas for angular momentum, just as we have three formulas for the torque:

L = xpy − ypx

= rptang = p · lever arm.

(18.17) Like torque, angular momentum depends upon the position of the axis about which it is to be calculated.

Before proceeding to a treatment of more than one particle, let us apply the above results to a planet going around the sun. In which direction is the force? The force is toward the sun. What, then, is the torque on the object? Of course, this depends upon where we take the axis, but we get a very simple result if we take it at the sun itself, for the torque is the force times the lever arm, or the component of force perpendicular to r, times r. But there is no tangential force, so there is no torque about an axis at the sun! Therefore, the angular momentum of the planet going around the sun must remain constant. Let us see what that means. The tangential component of velocity, times the mass, times the radius, will be constant, because that is the angular momentum, and the rate of change of the angular momentum is the torque, and, in this problem, the torque is zero. Of course since the mass is also a constant, this means that the tangential velocity times the radius is a constant. But this is something we already knew for the motion of a planet. Suppose we consider a small amount of

18-10

time ∆t. How far will the planet move when it moves from P to Q (Fig. 18-3)? How much area will it sweep through? Disregarding the very tiny area QQ0P compared with the much larger area OP Q, it is simply half the base P Q times the height, OR. In other words, the area that is swept through in unit time will be equal to the velocity times the lever arm of the velocity (times one-half). Thus the rate of change of area is proportional to the angular momentum, which is constant. So Kepler’s law about equal areas in equal times is a word description of the statement of the law of conservation of angular momentum, when there is no torque produced by the force.

18-4 Conservation of angular momentum Now we shall go on to consider what happens when there is a large number of particles, when an object is made of many pieces with many forces acting between them and on them from the outside. Of course, we already know that, about any given ﬁxed axis, the torque on the ith particle (which is the force on the ith particle times the lever arm of that force) is equal to the rate of change of the angular momentum of that particle, and that the angular momentum of the ith particle is its momentum times its momentum lever arm. Now suppose we add the torques τi for all the particles and call it the total torque τ. Then this will be the rate of change of the sum of the angular momenta of all the particles Li, and that deﬁnes a new quantity which we call the total angular momentum L. Just as the total momentum of an object is the sum of the momenta of all the parts, so the angular momentum is the sum of the angular momenta of all the parts. Then the rate of change of the total L is the total torque:

τ =X

τi =X dLi

= dL dt

.

(18.18)

dt

Now it might seem that the total torque is a complicated thing. There are all those internal forces and all the outside forces to be considered. But, if we take Newton’s law of action and reaction to say, not simply that the action and reaction are equal, but also that they are directed exactly oppositely along the same line (Newton may or may not actually have said this, but he tacitly assumed it), then the two torques on the reacting objects, due to their mutual interaction, will be equal and opposite because the lever arms for any axis are equal. Therefore the internal torques balance out pair by pair, and so we have the remarkable theorem that the rate of change of the total angular momentum

18-11

about any axis is equal to the external torque about that axis!

τ =X

τi = τext = dL/dt.

(18.19)

Thus we have a very powerful theorem concerning the motion of large collections of particles, which permits us to study the over-all motion without having to look at the detailed machinery inside. This theorem is true for any collection of objects, whether they form a rigid body or not.

One extremely important case of the above theorem is the law of conservation of angular momentum: if no external torques act upon a system of particles, the angular momentum remains constant. A special case of great importance is that of a rigid body, that is, an object of a deﬁnite shape that is just turning around. Consider an object that is ﬁxed in its geometrical dimensions, and which is rotating about a ﬁxed axis. Various parts of the object bear the same relationship to one another at all times. Now let us try to ﬁnd the total angular momentum of this object. If the mass of one of its particles is mi, and its position or location is at (xi, yi), then the problem is to ﬁnd the angular momentum of that particle, because the total angular momentum is the sum of the angular momenta of all such particles in the body. For an object going around in a circle, the angular momentum, of course, is the mass times the velocity times the distance from the axis, and the velocity is equal to the angular velocity times the distance from the axis:

Li = miviri = mir2

i ω,

or, summing over all the particles i, we get L = Iω,

where

I =X

mir2 i .

(18.20)

(18.21)

(18.22)

i

This is the analog of the law that the momentum is mass times velocity. Velocity is replaced by angular velocity, and we see that the mass is replaced by a new thing which we call the moment of inertia I, which is analogous to the mass. Equations (18.21) and (18.22) say that a body has inertia for turning which depends, not just on the masses, but on how far away they are from the axis. So, if we have two objects of the same mass, when we put the masses

18-12

Fig. 18-4. The「inertia for turning」depends upon the lever arm of the

masses.

farther away from the axis, the inertia for turning will be higher. This is easily demonstrated by the apparatus shown in Fig. 18-4, where a weight M is kept from falling very fast because it has to turn the large weighted rod. At ﬁrst, the masses m are close to the axis, and M speeds up at a certain rate. But when we change the moment of inertia by putting the two masses m much farther away from the axis, then we see that M accelerates much less rapidly than it did before, because the body has much more inertia against turning. The moment of inertia is the inertia against turning, and is the sum of the contributions of all the masses, times their distances squared, from the axis. There is one important diﬀerence between mass and moment of inertia which is very dramatic. The mass of an object never changes, but its moment of inertia can be changed. If we stand on a frictionless rotatable stand with our arms outstretched, and hold some weights in our hands as we rotate slowly, we may change our moment of inertia by drawing our arms in, but our mass does not change. When we do this, all kinds of wonderful things happen, because of the law of the conservation of angular momentum: If the external torque is zero, then the angular momentum, the moment of inertia times omega, remains constant. Initially, we were rotating with a large moment of inertia I1 at a low angular velocity ω1, and the angular momentum was I1ω1. Then we changed our moment of inertia by pulling our arms in, say to a smaller value I2. Then the product Iω, which has to stay the same because the total angular momentum has to stay the same, was I2ω2. So I1ω1 = I2ω2. That is, if we reduce the moment of inertia, we have to increase the angular velocity.

18-13

19

