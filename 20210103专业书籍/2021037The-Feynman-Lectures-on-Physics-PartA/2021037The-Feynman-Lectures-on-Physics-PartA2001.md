Rotation in space

20-1 Torques in three dimensions In this chapter we shall discuss one of the most remarkable and amusing consequences of mechanics, the behavior of a rotating wheel. In order to do this we must ﬁrst extend the mathematical formulation of rotational motion, the principles of angular momentum, torque, and so on, to three-dimensional space. We shall not use these equations in all their generality and study all their consequences, because this would take many years, and we must soon turn to other subjects. In an introductory course we can present only the fundamental laws and apply them to a very few situations of special interest.

First, we notice that if we have a rotation in three dimensions, whether of a rigid body or any other system, what we deduced for two dimensions is still right. That is, it is still true that xFy − yFx is the torque「in the xy-plane,」or the torque「around the z-axis.」It also turns out that this torque is still equal to the rate of change of xpy − ypx, for if we go back over the derivation of Eq. (18.15) from Newton’s laws we see that we did not have to assume that the motion was in a plane; when we diﬀerentiate xpy − ypx, we get xFy − yFx, so this theorem is still right. The quantity xpy − ypx, then, we call the angular momentum belonging to the xy-plane, or the angular momentum about the z-axis. This being true, we can use any other pair of axes and get another equation. For instance, we can use the yz-plane, and it is clear from symmetry that if we just substitute y for x and z for y, we would ﬁnd yFz − zFy for the torque and ypz − zpy would be the angular momentum associated with the yz-plane. Of course we could have another plane, the zx-plane, and for this we would ﬁnd zFx − xFz = d/dt (zpx − xpz). That these three equations can be deduced for the motion of a single particle is quite clear. Furthermore, if we added such things as xpy − ypx together for many particles and called it the total angular momentum, we would have three kinds for the three planes xy, yz, and zx, and if we did the same with the forces,

20-1

we would talk about the torque in the planes xy, yz, and zx also. Thus we would have laws that the external torque associated with any plane is equal to the rate of change of the angular momentum associated with that plane. This is just a generalization of what we wrote in two dimensions.

But now one may say,「Ah, but there are more planes; after all, can we not take some other plane at some angle, and calculate the torque on that plane from the forces? Since we would have to write another set of equations for every such plane, we would have a lot of equations!」Interestingly enough, it turns out that if we were to work out the combination x0Fy0 − y0Fx0 for another plane, measuring the x0, Fy0, etc., in that plane, the result can be written as some combination of the three expressions for the xy-, yz- and zx-planes. There is nothing new. In other words, if we know what the three torques in the xy-, yz-, and zx-planes are, then the torque in any other plane, and correspondingly the angular momentum also, can be written as some combination of these: six percent of one and ninety-two percent of another, and so on. This property we shall now analyze.

Suppose that in the xyz-axes, Joe has worked out all his torques and his angular momenta in his planes. But Moe has axes x0, y0, z0 in some other direction. To make it a little easier, we shall suppose that only the x- and y-axes have been turned. Moe’s x0 and y0 are new, but his z0 happens to be the same. That is, he has new planes, let us say, for yz and zx. He therefore has new torques and angular momenta which he would work out. For example, his torque in the x0y0-plane would be equal to x0Fy0 − y0Fx0 and so forth. What we must now do is to ﬁnd the relationship between the new torques and the old torques, so we will be able to make a connection from one set of axes to the other. Someone may say,「That looks just like what we did with vectors.」And indeed, that is exactly what we are intending to do. Then he may say,「Well, isn’t torque just a vector?」It does turn out to be a vector, but we do not know that right away without making an analysis. So in the following steps we shall make the analysis. We shall not discuss every step in detail, since we only want to illustrate how it works. The torques calculated by Joe are

τxy = xFy − yFx, τyz = yFz − z Fy, τzx = z Fx − xFz .

(20.1)

We digress at this point to note that in such cases as this one may get the wrong sign for some quantity if the coordinates are not handled in the right way. Why not

20-2

write τyz = zFy − yFz? The problem arises from the fact that a coordinate system may be either「right-handed」or「left-handed.」Having chosen (arbitrarily) a sign for, say τxy, then the correct expressions for the other two quantities may always be found by interchanging the letters xyz in either order or

x

x

z

y

z

y

Moe now calculates the torques in his system: τx0y0 = x0Fy0 − y0Fx0, τy0z0 = y0Fz0 − z0 Fy0 , τz0x0 = z0 Fx0 − x0Fz0 .

(20.2)

Now we suppose that one coordinate system is rotated by a ﬁxed angle θ, such that the z- and z0-axes are the same. (This angle θ has nothing to do with rotating objects or what is going on inside the coordinate system. It is merely the relationship between the axes used by one man and the axes used by the other, and is supposedly constant.) Thus the coordinates of the two systems are related by

x0 = x cos θ + y sin θ, y0 = y cos θ − x sin θ, z0 = z .

(20.3)

Likewise, because force is a vector it transforms into the new system in the same way as do x, y, and z, since a thing is a vector if and only if the various components transform in the same way as x, y, and z:

Fx0 = Fx cos θ + Fy sin θ, Fy0 = Fy cos θ − Fx sin θ, Fz0 = Fz .

(20.4)

Now we can ﬁnd out how the torque transforms by merely substituting for x0, y0, and z0 the expressions (20.3), and for Fx0, Fy0, Fz0 those given by (20.4), all into (20.2). So, we have a rather long string of terms for τx0y0 and (rather surprisingly at ﬁrst) it turns out that it comes right down to xFy − yFx, which

20-3

we recognize to be the torque in the xy-plane:

τx0y0 = (x cos θ + y sin θ)(Fy cos θ − Fx sin θ)

− (y cos θ − x sin θ)(Fx cos θ + Fy sin θ)

= xFy(cos2 θ + sin2 θ) − yFx(sin2 θ + cos2 θ)

+ xFx(− sin θ cos θ + sin θ cos θ) + yFy(sin θ cos θ − sin θ cos θ)

= xFy − yFx = τxy.

(20.5) That result is clear, for if we only turn our axes in the plane, the twist around z in that plane is no diﬀerent than it was before, because it is the same plane! What will be more interesting is the expression for τy0z0, because that is a new plane. We now do exactly the same thing with the y0z0-plane, and it comes out as follows:

τy0z0 = (y cos θ − x sin θ)Fz

− z(Fy cos θ − Fx sin θ)

= (yFz − zFy) cos θ + (zFx − xFz) sin θ = τyz cos θ + τzx sin θ.

Finally, we do it for z0x0:

τz0x0 = z(Fx cos θ + Fy sin θ) − (x cos θ + y sin θ)Fz

= (zFx − xFz) cos θ − (yFz − zFy) sin θ = τzx cos θ − τyz sin θ.

(20.6)

(20.7)

We wanted to get a rule for ﬁnding torques in new axes in terms of torques in old axes, and now we have the rule. How can we ever remember that rule? If we look carefully at (20.5), (20.6), and (20.7), we see that there is a close relationship between these equations and the equations for x, y, and z. If, somehow, we could call τxy the z-component of something, let us call it the z-component of τ, then it would be all right; we would understand (20.5) as a vector transformation, since the z-component would be unchanged, as it should be. Likewise, if we associate with the yz-plane the x-component of our newly invented vector, and with the

20-4

zx-plane, the y-component, then these transformation expressions would read

τz0 = τz , τx0 = τx cos θ + τy sin θ, τy0 = τy cos θ − τx sin θ,

(20.8)

which is just the rule for vectors!

Therefore we have proved that we may identify the combination of xFy − yFx with what we ordinarily call the z-component of a certain artiﬁcially invented vector. Although a torque is a twist on a plane, and it has no a priori vector character, mathematically it does behave like a vector. This vector is at right angles to the plane of the twist, and its length is proportional to the strength of the twist. The three components of such a quantity will transform like a real vector.

So we represent torques by vectors; with each plane on which the torque is supposed to be acting, we associate a line at right angles, by a rule. But「at right angles」leaves the sign unspeciﬁed. To get the sign right, we must adopt a rule which will tell us that if the torque were in a certain sense on the xy-plane, then the axis that we want to associate with it is in the「up」z-direction. That is, somebody has to deﬁne「right」and「left」for us. Supposing that the coordinate system is x, y, z in a right-hand system, then the rule will be the following: if we think of the twist as if we were turning a screw having a right-hand thread, then the direction of the vector that we will associate with that twist is in the direction that the screw would advance.

Why is torque a vector? It is a miracle of good luck that we can associate a single axis with a plane, and therefore that we can associate a vector with the torque; it is a special property of three-dimensional space. In two dimensions, the torque is an ordinary scalar, and there need be no direction associated with it. In three dimensions, it is a vector. If we had four dimensions, we would be in great diﬃculty, because (if we had time, for example, as the fourth dimension) we would not only have planes like xy, yz, and zx, we would also have tx-, ty-, and tz- planes. There would be six of them, and one cannot represent six quantities as one vector in four dimensions. We will be living in three dimensions for a long time, so it is well to notice that the foregoing mathematical treatment did not depend upon the fact that x was position and F was force; it only depended on the transformation laws for vectors. Therefore if, instead of x, we used the x-component of some other vector,

20-5

it is not going to make any diﬀerence. In other words, if we were to calculate axby − aybx, where a and b are vectors, and call it the z-component of some new quantity c, then these new quantities form a vector c. We need a mathematical notation for the relationship of the new vector, with its three components, to the vectors a and b. The notation that has been devised for this is c = a × b. We have then, in addition to the ordinary scalar product in the theory of vector analysis, a new kind of product, called the vector product. Thus, if c = a × b, this is the same as writing

cx = aybz − az by, cy = az bx − axbz , cz = axby − aybx.

(20.9)

If we reverse the order of a and b, calling a, b and b, a, we would have the sign of c reversed, because cz would be bxay − byax. Therefore the cross product is unlike ordinary multiplication, where ab = ba; for the cross product, b × a = −a × b. From this, we can prove at once that if a = b, the cross product is zero. Thus, a × a = 0. The cross product is very important for representing the features of rotation, and it is important that we understand the geometrical relationship of the three vectors a, b, and c. Of course the relationship in components is given in Eq. (20.9) and from that one can determine what the relationship is in geometry. The answer is, ﬁrst, that the vector c is perpendicular to both a and b. (Try to calculate c · a, and see if it does not reduce to zero.) Second, the magnitude of c turns out to be the magnitude of a times the magnitude of b times the sine of the angle between the two. In which direction does c point? Imagine that we turn a into b through an angle less than 180◦; a screw with a right-hand thread turning in this way will advance in the direction of c. The fact that we say a right-hand screw instead of a left-hand screw is a convention, and is a perpetual reminder that if a and b are「honest」vectors in the ordinary sense, the new kind of「vector」which we have created by a × b is artiﬁcial, or slightly diﬀerent in its character from a and b, because it was made up with a special rule. If a and b are called ordinary vectors, we have a special name for them, we call them polar vectors. Examples of such vectors are the coordinate r, force F , momentum p, velocity v, electric ﬁeld E, etc.; these are ordinary polar vectors. Vectors which involve just one cross product in their deﬁnition are called axial vectors or pseudo vectors. Examples of pseudo vectors are, of course, torque τ and the angular

20-6

momentum L. It also turns out that the angular velocity ω is a pseudo vector, as is the magnetic ﬁeld B. In order to complete the mathematical properties of vectors, we should know all the rules for their multiplication, using dot and cross products. In our applications at the moment, we will need very little of this, but for the sake of completeness we shall write down all of the rules for vector multiplication so that we can use the results later. These are

(a) (b) (c) (d) (e) (f)

a × (b + c) = a × b + a × c,

(αa) × b = α(a × b), a · (b × c) = (a × b) · c, a × (b × c) = b(a · c) − c(a · b),

a × a = 0, a · (a × b) = 0.

(20.10)

20-2 The rotation equations using cross products Now let us ask whether any equations in physics can be written using the cross product. The answer, of course, is that a great many equations can be so written. For instance, we see immediately that the torque is equal to the position vector cross the force:

(20.11) This is a vector summary of the three equations τx = yFz − zFy, etc. By the same token, the angular momentum vector, if there is only one particle present, is the distance from the origin multiplied by the vector momentum:

τ = r × F .

L = r × p.

(20.12) For three-dimensional space rotation, the dynamical law analogous to the law F = dp/dt of Newton, is that the torque vector is the rate of change with time of the angular momentum vector: (20.13) If we sum (20.13) over many particles, the external torque on a system is the rate of change of the total angular momentum: τ ext = dLtot/dt.

τ = dL/dt.

(20.14)

20-7

Another theorem: If the total external torque is zero, then the total vector angular momentum of the system is a constant. This is called the law of conser- vation of angular momentum. If there is no torque on a given system, its angular momentum cannot change. What about angular velocity? Is it a vector? We have already discussed turning a solid object about a ﬁxed axis, but for a moment suppose that we are turning it simultaneously about two axes. It might be turning about an axis inside a box, while the box is turning about some other axis. The net result of such combined motions is that the object simply turns about some new axis! The wonderful thing about this new axis is that it can be ﬁgured out this way. If the rate of turning in the xy-plane is written as a vector in the z-direction whose length is equal to the rate of rotation in the plane, and if another vector is drawn in the y-direction, say, which is the rate of rotation in the zx-plane, then if we add these together as a vector, the magnitude of the result tells us how fast the object is turning, and the direction tells us in what plane, by the rule of the parallelogram. That is to say, simply, angular velocity is a vector, where we draw the magnitudes of the rotations in the three planes as projections at right angles to those planes.*

As a simple application of the use of the angular velocity vector, we may evaluate the power being expended by the torque acting on a rigid body. The power, of course, is the rate of change of work with time; in three dimensions, the power turns out to be P = τ · ω. All the formulas that we wrote for plane rotation can be generalized to three dimensions. For example, if a rigid body is turning about a certain axis with angular velocity ω, we might ask,「What is the velocity of a point at a certain radial position r?」We shall leave it as a problem for the student to show that the velocity of a particle in a rigid body is given by v = ω × r, where ω is the angular velocity and r is the position. Also, as another example of cross products, we had a formula for Coriolis force, which can also be written using cross products: F c = 2mv × ω. That is, if a particle is moving with velocity v in a coordinate system which is, in fact, rotating with angular velocity ω, and we want to think in terms of the rotating coordinate system, then we have to add the pseudo force F c.

* That this is true can be derived by compounding the displacements of the particles of the body during an inﬁnitesimal time ∆t. It is not self-evident, and is left to those who are interested to try to ﬁgure it out.

20-8

20-3 The gyroscope Let us now return to the law of conservation of angular momentum. This law may be demonstrated with a rapidly spinning wheel, or gyroscope, as follows (see Fig. 20-1). If we sit on a swivel chair and hold the spinning wheel with its axis horizontal, the wheel has an angular momentum about the horizontal axis. Angular momentum around a vertical axis cannot change because of the (frictionless) pivot of the chair, so if we turn the axis of the wheel into the vertical, then the wheel would have angular momentum about the vertical axis, because it is now spinning about this axis. But the system (wheel, ourself, and chair) cannot have a vertical component, so we and the chair have to turn in the direction opposite to the spin of the wheel, to balance it.

Fig. 20-1. Before: axis is horizontal; moment about vertical axis = 0. After: axis is vertical; momentum about vertical axis is still zero; man and chair spin in direction opposite to spin of the wheel.

First let us analyze in more detail the thing we have just described. What is surprising, and what we must understand, is the origin of the forces which turn us and the chair around as we turn the axis of the gyroscope toward the vertical. Figure 20-2 shows the wheel spinning rapidly about the y-axis. Therefore its angular velocity is about that axis and, it turns out, its angular momentum is likewise in that direction. Now suppose that we wish to rotate the wheel about the x-axis at a small angular velocity Ω; what forces are required? After a short time ∆t, the axis has turned to a new position, tilted at an angle ∆θ with the

20-9

Fig. 20-2. A gyroscope.

τ = Ω × L0.

horizontal. Since the major part of the angular momentum is due to the spin on the axis (very little is contributed by the slow turning), we see that the angular momentum vector has changed. What is the change in angular momentum? The angular momentum does not change in magnitude, but it does change in direction by an amount ∆θ. The magnitude of the vector ∆L is thus ∆L = L0 ∆θ, so that the torque, which is the time rate of change of the angular momentum, is τ = ∆L/∆t = L0 ∆θ/∆t = L0Ω. Taking the directions of the various quantities into account, we see that (20.15) Thus, if Ω and L0 are both horizontal, as shown in the ﬁgure, τ is vertical. To produce such a torque, horizontal forces F and −F must be applied at the ends of the axle. How are these forces applied? By our hands, as we try to rotate the axis of the wheel into the vertical direction. But Newton’s Third Law demands that equal and opposite forces (and equal and opposite torques) act on us. This causes us to rotate in the opposite sense about the vertical axis z. This result can be generalized for a rapidly spinning top. In the familiar case of a spinning top, gravity acting on its center of mass furnishes a torque about the point of contact with the ﬂoor (see Fig. 20-3). This torque is in the horizontal direction, and causes the top to precess with its axis moving in a circular cone about the vertical. If Ω is the (vertical) angular velocity of precession, we again ﬁnd that

τ = dL/dt = Ω × L0.

Thus, when we apply a torque to a rapidly spinning top, the direction of the precessional motion is in the direction of the torque, or at right angles to the forces producing the torque.

We may now claim to understand the precession of gyroscopes, and indeed we do, mathematically. However, this is a mathematical thing which, in a sense,

20-10

Fig. 20-3. A rapidly spinning top. Note that the direction of the

torque vector is the direction of the precession.

appears as a「miracle.」It will turn out, as we go to more and more advanced physics, that many simple things can be deduced mathematically more rapidly than they can be really understood in a fundamental or simple sense. This is a strange characteristic, and as we get into more and more advanced work there are circumstances in which mathematics will produce results which no one has really been able to understand in any direct fashion. An example is the Dirac equation, which appears in a very simple and beautiful form, but whose consequences are hard to understand. In our particular case, the precession of a top looks like some kind of a miracle involving right angles and circles, and twists and right-hand screws. What we should try to do is to understand it in a more physical way.

How can we explain the torque in terms of the real forces and the accelerations? We note that when the wheel is precessing, the particles that are going around the wheel are not really moving in a plane because the wheel is precessing (see Fig. 20-4). As we explained previously (Fig. 19-4), the particles which are crossing through the precession axis are moving in curved paths, and this requires application of a lateral force. This is supplied by our pushing on the axle, which

Fig. 20-4. The motion of particles in the spinning wheel of Fig. 20-2,

whose axis is turning, is in curved lines.

20-11

then communicates the force to the rim through the spokes.「Wait,」someone says,「what about the particles that are going back on the other side?」It does not take long to decide that there must be a force in the opposite direction on that side. The net force that we have to apply is therefore zero. The forces balance out, but one of them must be applied at one side of the wheel, and the other must be applied at the other side of the wheel. We could apply these forces directly, but because the wheel is solid we are allowed to do it by pushing on the axle, since forces can be carried up through the spokes.

What we have so far proved is that if the wheel is precessing, it can balance the torque due to gravity or some other applied torque. But all we have shown is that this is a solution of an equation. That is, if the torque is given, and if we get the spinning started right, then the wheel will precess smoothly and uniformly. But we have not proved (and it is not true) that a uniform precession is the most general motion a spinning body can undergo as the result of a given torque. The general motion involves also a「wobbling」about the mean precession. This「wobbling」is called nutation. Some people like to say that when one exerts a torque on a gyroscope, it turns and it precesses, and that the torque produces the precession. It is very strange that when one suddenly lets go of a gyroscope, it does not fall under the action of gravity, but moves sidewise instead! Why is it that the downward force of the gravity, which we know and feel, makes it go sidewise? All the formulas in the world like (20.15) are not going to tell us, because (20.15) is a special equation, valid only after the gyroscope is precessing nicely. What really happens, in detail, is the following. If we were to hold the axis absolutely ﬁxed, so that it cannot precess in any manner (but the top is spinning) then there is no torque acting, not even a torque from gravity, because it is balanced by our ﬁngers. But if we suddenly let go, then there will instantaneously be a torque from gravity. Anyone in his right mind would think that the top would fall, and that is what it starts to do, as can be seen if the top is not spinning too fast.

The gyro actually does fall, as we would expect. But as soon as it falls, it is then turning, and if this turning were to continue, a torque would be required. In the absence of a torque in this direction, the gyro begins to「fall」in the direction opposite that of the missing force. This gives the gyro a component of motion around the vertical axis, as it would have in steady precession. But the actual motion「overshoots」the steady precessional velocity, and the axis actually rises again to the level from which it started. The path followed by the end of the axle is a cycloid (the path followed by a pebble that is stuck in the tread of an

20-12

automobile tire). Ordinarily, this motion is too quick for the eye to follow, and it damps out quickly because of the friction in the gimbal bearings, leaving only the steady precessional drift (Fig. 20-5). The slower the wheel spins, the more obvious the nutation is.

Fig. 20-5. Actual motion of tip of axis of gyroscope under gravity just

after releasing axis previously held ﬁxed.

When the motion settles down, the axis of the gyro is a little bit lower than it was at the start. Why? (These are the more complicated details, but we bring them in because we do not want the reader to get the idea that the gyroscope is an absolute miracle. It is a wonderful thing, but it is not a miracle.) If we were holding the axis absolutely horizontally, and suddenly let go, then the simple precession equation would tell us that it precesses, that it goes around in a horizontal plane. But that is impossible! Although we neglected it before, it is true that the wheel has some moment of inertia about the precession axis, and if it is moving about that axis, even slowly, it has a weak angular momentum about the axis. Where did it come from? If the pivots are perfect, there is no torque about the vertical axis. How then does it get to precess if there is no change in the angular momentum? The answer is that the cycloidal motion of the end of the axis damps down to the average, steady motion of the center of the equivalent rolling circle. That is, it settles down a little bit low. Because it is low, the spin angular momentum now has a small vertical component, which is exactly what is needed for the precession. So you see it has to go down a little, in order to go around. It has to yield a little bit to the gravity; by turning its axis down a little bit, it maintains the rotation about the vertical axis. That, then, is the way a gyroscope works.

20-13

20-4 Angular momentum of a solid body Before we leave the subject of rotations in three dimensions, we shall discuss, at least qualitatively, a few eﬀects that occur in three-dimensional rotations that are not self-evident. The main eﬀect is that, in general, the angular momentum of a rigid body is not necessarily in the same direction as the angular velocity. Consider a wheel that is fastened onto a shaft in a lopsided fashion, but with the axis through the center of gravity, to be sure (Fig. 20-6). When we spin the wheel around the axis, anybody knows that there will be shaking at the bearings because of the lopsided way we have it mounted. Qualitatively, we know that in the rotating system there is centrifugal force acting on the wheel, trying to throw its mass as far as possible from the axis. This tends to line up the plane of the wheel so that it is perpendicular to the axis. To resist this tendency, a torque is exerted by the bearings. If there is a torque exerted by the bearings, there must be a rate of change of angular momentum. How can there be a rate of change of angular momentum when we are simply turning the wheel about the axis? Suppose we break the angular velocity ω into components ω1 and ω2 perpendicular and parallel to the plane of the wheel. What is the angular momentum? The moments of inertia about these two axes are diﬀerent, so the angular momentum components, which (in these particular, special axes only) are equal to the moments of inertia times the corresponding angular velocity components, are in a diﬀerent ratio than are the angular velocity components. Therefore the angular momentum vector is in a direction in space not along the axis. When we turn the object, we have to turn the angular momentum vector in space, so we must exert torques on the shaft.

Fig. 20-6. The angular momentum of a rotating body is not necessarily

parallel to the angular velocity.

Although it is much too complicated to prove here, there is a very important and interesting property of the moment of inertia which is easy to describe and to

20-14

use, and which is the basis of our above analysis. This property is the following: Any rigid body, even an irregular one like a potato, possesses three mutually perpendicular axes through the CM, such that the moment of inertia about one of these axes has the greatest possible value for any axis through the CM, the moment of inertia about another of the axes has the minimum possible value, and the moment of inertia about the third axis is intermediate between these two (or equal to one of them). These axes are called the principal axes of the body, and they have the important property that if the body is rotating about one of them, its angular momentum is in the same direction as the angular velocity. For a body having axes of symmetry, the principal axes are along the symmetry axes.

Fig. 20-7. The angular velocity and angular momentum of a rigid

body (A > B > C).

If we take the x-, y-, and z-axes along the principal axes, and call the corresponding principal moments of inertia A, B, and C, we may easily evaluate the angular momentum and the kinetic energy of rotation of the body for any angular velocity ω. If we resolve ω into components ωx, ωy, and ωz along the x-, y-, z-axes, and use unit vectors i, j, k, also along x, y, z, we may write the angular momentum as

L = Aωxi + Bωyj + Cωzk.

(20.16)

20-15

The kinetic energy of rotation is

KE = 1 = 1

2(Aω2 2 L · ω.

x

+ Bω2

y

+ Cω2

z

)

(20.17)

20-16

21

