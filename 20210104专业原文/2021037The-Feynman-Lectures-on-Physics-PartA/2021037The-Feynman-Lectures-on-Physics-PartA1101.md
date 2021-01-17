Vectors

11-1 Symmetry in physics In this chapter we introduce a subject that is technically known in physics as symmetry in physical law. The word「symmetry」is used here with a special meaning, and therefore needs to be deﬁned. When is a thing symmetrical—how can we deﬁne it? When we have a picture that is symmetrical, one side is somehow the same as the other side. Professor Hermann Weyl has given this deﬁnition of symmetry: a thing is symmetrical if one can subject it to a certain operation and it appears exactly the same after the operation. For instance, if we look at a silhouette of a vase that is left-and-right symmetrical, then turn it 180◦ around the vertical axis, it looks the same. We shall adopt the deﬁnition of symmetry in Weyl’s more general form, and in that form we shall discuss symmetry of physical laws.

Suppose we build a complex machine in a certain place, with a lot of compli- cated interactions, and balls bouncing around with forces between them, and so on. Now suppose we build exactly the same kind of equipment at some other place, matching part by part, with the same dimensions and the same orientation, everything the same only displaced laterally by some distance. Then, if we start the two machines in the same initial circumstances, in exact correspondence, we ask: will one machine behave exactly the same as the other? Will it follow all the motions in exact parallelism? Of course the answer may well be no, because if we choose the wrong place for our machine it might be inside a wall and interferences from the wall would make the machine not work.

All of our ideas in physics require a certain amount of common sense in their application; they are not purely mathematical or abstract ideas. We have to understand what we mean when we say that the phenomena are the same when we move the apparatus to a new position. We mean that we move everything that we believe is relevant; if the phenomenon is not the same, we suggest that

11-1

something relevant has not been moved, and we proceed to look for it. If we never ﬁnd it, then we claim that the laws of physics do not have this symmetry. On the other hand, we may ﬁnd it—we expect to ﬁnd it—if the laws of physics do have this symmetry; looking around, we may discover, for instance, that the wall is pushing on the apparatus. The basic question is, if we deﬁne things well enough, if all the essential forces are included inside the apparatus, if all the relevant parts are moved from one place to another, will the laws be the same? Will the machinery work the same way?

It is clear that what we want to do is to move all the equipment and essential inﬂuences, but not everything in the world—planets, stars, and all—for if we do that, we have the same phenomenon again for the trivial reason that we are right back where we started. No, we cannot move everything. But it turns out in practice that with a certain amount of intelligence about what to move, the machinery will work. In other words, if we do not go inside a wall, if we know the origin of the outside forces, and arrange that those are moved too, then the machinery will work the same in one location as in another.

11-2 Translations We shall limit our analysis to just mechanics, for which we now have suﬃcient knowledge. In previous chapters we have seen that the laws of mechanics can be summarized by a set of three equations for each particle:

m(d2x/dt2) = Fx,

m(d2y/dt2) = Fy,

m(d2z/dt2) = Fz.

(11.1)

Now this means that there exists a way to measure x, y, and z on three perpen- dicular axes, and the forces along those directions, such that these laws are true. These must be measured from some origin, but where do we put the origin? All that Newton would tell us at ﬁrst is that there is some place that we can measure from, perhaps the center of the universe, such that these laws are correct. But we can show immediately that we can never ﬁnd the center, because if we use some other origin it would make no diﬀerence. In other words, suppose that there are two people—Joe, who has an origin in one place, and Moe, who has a parallel system whose origin is somewhere else (Fig. 11-1). Now when Joe measures the location of the point in space, he ﬁnds it at x, y, and z (we shall usually leave z out because it is too confusing to draw in a picture). Moe, on the other hand, when measuring the same point, will obtain a diﬀerent x (in order to distinguish

11-2

Fig. 11-1. Two parallel coordinate systems.

it, we will call it x0), and in principle a diﬀerent y, although in our example they are numerically equal. So we have x0 = x − a,

(11.2) Now in order to complete our analysis we must know what Moe would obtain for the forces. The force is supposed to act along some line, and by the force in the x-direction we mean the part of the total which is in the x-direction, which is the magnitude of the force times this cosine of its angle with the x-axis. Now we see that Moe would use exactly the same projection as Joe would use, so we have a set of equations

y0 = y,

z0 = z.

Fx0 = Fx,

Fy0 = Fy,

Fz0 = Fz.

(11.3)

These would be the relationships between quantities as seen by Joe and Moe.

The question is, if Joe knows Newton’s laws, and if Moe tries to write down Newton’s laws, will they also be correct for him? Does it make any diﬀerence from which origin we measure the points? In other words, assuming that equations (11.1) are true, and the Eqs. (11.2) and (11.3) give the relationship of the measurements, is it or is it not true that

(a) m(d2x0/dt2) = Fx0, (b) m(d2y0/dt2) = Fy0 , (c) m(d2z0 /dt2) = Fz0 ?

(11.4)

In order to test these equations we shall diﬀerentiate the formula for x0 twice.

First of all

dx0 dt

= d dt

(x − a) = dx dt

− da dt

.

11-3

Now we shall assume that Moe’s origin is ﬁxed (not moving) relative to Joe’s; therefore a is a constant and da/dt = 0, so we ﬁnd that

and therefore

dx0/dt = dx/dt

d2x0/dt2 = d2x/dt2;

therefore we know that Eq. (11.4a) becomes

m(d2x/dt2) = Fx0.

(We also suppose that the masses measured by Joe and Moe are equal.) Thus the acceleration times the mass is the same as the other fellow’s. We have also found the formula for Fx0, for, substituting from Eq. (11.1), we ﬁnd that

Fx0 = Fx.

Therefore the laws as seen by Moe appear the same; he can write Newton’s laws too, with diﬀerent coordinates, and they will still be right. That means that there is no unique way to deﬁne the origin of the world, because the laws will appear the same, from whatever position they are observed.

This is also true: if there is a piece of equipment in one place with a certain kind of machinery in it, the same equipment in another place will behave in the same way. Why? Because one machine, when analyzed by Moe, has exactly the same equations as the other one, analyzed by Joe. Since the equations are the same, the phenomena appear the same. So the proof that an apparatus in a new position behaves the same as it did in the old position is the same as the proof that the equations when displaced in space reproduce themselves. Therefore we say that the laws of physics are symmetrical for translational displacements, symmetrical in the sense that the laws do not change when we make a translation of our coordinates. Of course it is quite obvious intuitively that this is true, but it is interesting and entertaining to discuss the mathematics of it.

11-3 Rotations The above is the ﬁrst of a series of ever more complicated propositions concerning the symmetry of a physical law. The next proposition is that it should make no diﬀerence in which direction we choose the axes. In other words, if we

11-4

build a piece of equipment in some place and watch it operate, and nearby we build the same kind of apparatus but put it up on an angle, will it operate in the same way? Obviously it will not if it is a Grandfather clock, for example! If a pendulum clock stands upright, it works ﬁne, but if it is tilted the pendulum falls against the side of the case and nothing happens. The theorem is then false in the case of the pendulum clock, unless we include the earth, which is pulling on the pendulum. Therefore we can make a prediction about pendulum clocks if we believe in the symmetry of physical law for rotation: something else is involved in the operation of a pendulum clock besides the machinery of the clock, something outside it that we should look for. We may also predict that pendulum clocks will not work the same way when located in diﬀerent places relative to this mysterious source of asymmetry, perhaps the earth. Indeed, we know that a pendulum clock up in an artiﬁcial satellite, for example, would not tick either, because there is no eﬀective force, and on Mars it would go at a diﬀerent rate. Pendulum clocks do involve something more than just the machinery inside, they involve something on the outside. Once we recognize this factor, we see that we must turn the earth along with the apparatus. Of course we do not have to worry about that, it is easy to do; one simply waits a moment or two and the earth turns; then the pendulum clock ticks again in the new position the same as it did before. While we are rotating in space our angles are always changing, absolutely; this change does not seem to bother us very much, for in the new position we seem to be in the same condition as in the old. This has a certain tendency to confuse one, because it is true that in the new turned position the laws are the same as in the unturned position, but it is not true that as we turn a thing it follows the same laws as it does when we are not turning it. If we perform suﬃciently delicate experiments, we can tell that the earth is rotating, but not that it had rotated. In other words, we cannot locate its angular position, but we can tell that it is changing. Now we may discuss the eﬀects of angular orientation upon physical laws. Let us ﬁnd out whether the same game with Joe and Moe works again. This time, to avoid needless complication, we shall suppose that Joe and Moe use the same origin (we have already shown that the axes can be moved by translation to another place). Assume that Moe’s axes have rotated relative to Joe’s by an angle θ. The two coordinate systems are shown in Fig. 11-2, which is restricted to two dimensions. Consider any point P having coordinates (x, y) in Joe’s system and (x0, y0) in Moe’s system. We shall begin, as in the previous case, by expressing the coordinates x0 and y0 in terms of x, y, and θ. To do so, we ﬁrst drop perpendiculars from P to all four axes and draw AB perpendicular to P Q.

11-5

Fig. 11-2. Two coordinate systems having diﬀerent angular orienta-

tions.

Inspection of the ﬁgure shows that x0 can be written as the sum of two lengths along the x0-axis, and y0 as the diﬀerence of two lengths along AB. All these lengths are expressed in terms of x, y, and θ in equations (11.5), to which we have added an equation for the third dimension. x0 = x cos θ + y sin θ, y0 = y cos θ − x sin θ, z0 = z .

(11.5)

The next step is to analyze the relationship of forces as seen by the two observers, following the same general method as before. Let us assume that a force F , which has already been analyzed as having components Fx and Fy (as seen by Joe), is acting on a particle of mass m, located at point P in Fig. 11-2. For simplicity, let us move both sets of axes so that the origin is at P, as shown in Fig. 11-3. Moe sees the components of F along his axes as Fx0 and Fy0. Fx has components along both the x0- and y0-axes, and Fy likewise has components along both these axes. To express Fx0 in terms of Fx and Fy, we sum these components along the x0-axis, and in a like manner we can express Fy0 in terms of Fx and Fy. The results are

Fx0 = Fx cos θ + Fy sin θ, Fy0 = Fy cos θ − Fx sin θ, Fz0 = Fz .

(11.6)

It is interesting to note an accident of sorts, which is of extreme importance: the formulas (11.5) and (11.6), for coordinates of P and components of F , respectively, are of identical form.

11-6

Fig. 11-3. Components of a force in the two systems.

As before, Newton’s laws are assumed to be true in Joe’s system, and are expressed by equations (11.1). The question, again, is whether Moe can apply Newton’s laws—will the results be correct for his system of rotated axes? In other words, if we assume that Eqs. (11.5) and (11.6) give the relationship of the measurements, is it true or not true that

m(d2x0/dt2) = Fx0, m(d2y0/dt2) = Fy0, m(d2z0 /dt2) = Fz0?

(11.7)

To test these equations, we calculate the left and right sides independently, and compare the results. To calculate the left sides, we multiply equations (11.5) by m, and diﬀerentiate twice with respect to time, assuming the angle θ to be constant. This gives

m(d2x0/dt2) = m(d2x/dt2) cos θ + m(d2y/dt2) sin θ, m(d2y0/dt2) = m(d2y/dt2) cos θ − m(d2x/dt2) sin θ, m(d2z0 /dt2) = m(d2z /dt2).

(11.8)

We calculate the right sides of equations (11.7) by substituting equations (11.1) into equations (11.6). This gives

Fx0 = m(d2x/dt2) cos θ + m(d2y/dt2) sin θ, Fy0 = m(d2y/dt2) cos θ − m(d2x/dt2) sin θ, Fz0 = m(d2z /dt2).

(11.9)

11-7

Behold! The right sides of Eqs. (11.8) and (11.9) are identical, so we conclude that if Newton’s laws are correct on one set of axes, they are also valid on any other set of axes. This result, which has now been established for both translation and rotation of axes, has certain consequences: ﬁrst, no one can claim his particular axes are unique, but of course they can be more convenient for certain particular problems. For example, it is handy to have gravity along one axis, but this is not physically necessary. Second, it means that any piece of equipment which is completely self-contained, with all the force-generating equipment completely inside the apparatus, would work the same when turned at an angle.

11-4 Vectors Not only Newton’s laws, but also the other laws of physics, so far as we know today, have the two properties which we call invariance (or symmetry) under translation of axes and rotation of axes. These properties are so important that a mathematical technique has been developed to take advantage of them in writing and using physical laws.

The foregoing analysis involved considerable tedious mathematical work. To reduce the details to a minimum in the analysis of such questions, a very powerful mathematical machinery has been devised. This system, called vector analysis, supplies the title of this chapter; strictly speaking, however, this is a chapter on the symmetry of physical laws. By the methods of the preceding analysis we were able to do everything required for obtaining the results that we sought, but in practice we should like to do things more easily and rapidly, so we employ the vector technique.

We began by noting some characteristics of two kinds of quantities that are important in physics. (Actually there are more than two, but let us start out with two.) One of them, like the number of potatoes in a sack, we call an ordinary quantity, or an undirected quantity, or a scalar. Temperature is an example of such a quantity. Other quantities that are important in physics do have direction, for instance velocity: we have to keep track of which way a body is going, not just its speed. Momentum and force also have direction, as does displacement: when someone steps from one place to another in space, we can keep track of how far he went, but if we wish also to know where he went, we have to specify a direction. All quantities that have a direction, like a step in space, are called vectors.

11-8

A vector is three numbers. In order to represent a step in space, say from the origin to some particular point P whose location is (x, y, z), we really need three numbers, but we are going to invent a single mathematical symbol, r, which is unlike any other mathematical symbols we have so far used.* It is not a single number, it represents three numbers: x, y, and z. It means three numbers, but not really only those three numbers, because if we were to use a diﬀerent coordinate system, the three numbers would be changed to x0, y0, and z0. However, we want to keep our mathematics simple and so we are going to use the same mark to represent the three numbers (x, y, z) and the three numbers (x0, y0, z0). That is, we use the same mark to represent the ﬁrst set of three numbers for one coordinate system, but the second set of three numbers if we are using the other coordinate system. This has the advantage that when we change the coordinate system, we do not have to change the letters of our equations. If we write an equation in terms of x, y, z, and then use another system, we have to change to x0, y0, z0, but we shall just write r, with the convention that it represents (x, y, z) if we use one set of axes, or (x0, y0, z0) if we use another set of axes, and so on. The three numbers which describe the quantity in a given coordinate system are called the components of the vector in the direction of the coordinate axes of that system. That is, we use the same symbol for the three letters that correspond to the same object, as seen from diﬀerent axes. The very fact that we can say「the same object」implies a physical intuition about the reality of a step in space, that is independent of the components in terms of which we measure it. So the symbol r will represent the same thing no matter how we turn the axes. Now suppose there is another directed physical quantity, any other quantity, which also has three numbers associated with it, like force, and these three numbers change to three other numbers by a certain mathematical rule, if we change the axes. It must be the same rule that changes (x, y, z) into (x0, y0, z0). In other words, any physical quantity associated with three numbers which transform as do the components of a step in space is a vector. An equation like

F = r

would thus be true in any coordinate system if it were true in one. This equation, of course, stands for the three equations

Fx = x,

Fy = y,

Fz = z,

* In type, vectors are represented by boldface; in handwritten form an arrow is used: ~r.

11-9

or, alternatively, for

Fx0 = x0,

Fy0 = y0,

Fz0 = z0.

The fact that a physical relationship can be expressed as a vector equation assures us the relationship is unchanged by a mere rotation of the coordinate system. That is the reason why vectors are so useful in physics.

Now let us examine some of the properties of vectors. As examples of vectors we may mention velocity, momentum, force, and acceleration. For many purposes it is convenient to represent a vector quantity by an arrow that indicates the direction in which it is acting. Why can we represent force, say, by an arrow? Because it has the same mathematical transformation properties as a「step in space.」We thus represent it in a diagram as if it were a step, using a scale such that one unit of force, or one newton, corresponds to a certain convenient length. Once we have done this, all forces can be represented as lengths, because an equation like

F = kr,

where k is some constant, is a perfectly legitimate equation. Thus we can always represent forces by lines, which is very convenient, because once we have drawn the line we no longer need the axes. Of course, we can quickly calculate the three components as they change upon turning the axes, because that is just a geometric problem.

11-5 Vector algebra Now we must describe the laws, or rules, for combining vectors in various ways. The ﬁrst such combination is the addition of two vectors: suppose that a is a vector which in some particular coordinate system has the three components (ax, ay, az), and that b is another vector which has the three components (bx, by, bz). Now let us invent three new numbers (ax + bx, ay + by, az + bz). Do these form a vector?「Well,」we might say,「they are three numbers, and every three numbers form a vector.」No, not every three numbers form a vector! In order for it to be a vector, not only must there be three numbers, but these must be associated with a coordinate system in such a way that if we turn the coordinate system, the three numbers「revolve」on each other, get「mixed up」in each other, by the precise laws we have already described. So the question is, if we now rotate the coordinate system so that (ax, ay, az) become (ax0, ay0, az0) and (bx, by, bz)

11-10

become (bx0, by0, bz0), what do (ax + bx, ay + by, az + bz) become? Do they become (ax0 + bx0, ay0 + by0, az0 + bz0) or not? The answer is, of course, yes, because the prototype transformations of Eq. (11.5) constitute what we call a linear transformation. If we apply those transformations to ax and bx to get ax0 + bx0, we ﬁnd that the transformed ax + bx is indeed the same as ax0 + bx0. When a and b are「added together」in this sense, they will form a vector which we may call c. We would write this as

Now c has the interesting property

c = a + b.

c = b + a,

as we can immediately see from its components. Thus also,

a + (b + c) = (a + b) + c.

We can add vectors in any order.

What is the geometric signiﬁcance of a + b? Suppose that a and b were represented by lines on a piece of paper, what would c look like? This is shown in Fig. 11-4. We see that we can add the components of b to those of a most conveniently if we place the rectangle representing the components of b next to that representing the components of a in the manner indicated. Since b just「ﬁts」into its rectangle, as does a into its rectangle, this is the same as putting the「tail」of b on the「head」of a, the arrow from the「tail」of a to the「head」of b being the vector c. Of course, if we added a to b the other way around, we

Fig. 11-4. The addition of vectors.

11-11

would put the「tail」of a on the「head」of b, and by the geometrical properties of parallelograms we would get the same result for c. Note that vectors can be added in this way without reference to any coordinate axes. Suppose we multiply a vector by a number α, what does this mean? We deﬁne it to mean a new vector whose components are αax, αay, and αaz. We leave it as a problem for the student to prove that it is a vector. Now let us consider vector subtraction. We may deﬁne subtraction in the same way as addition, but instead of adding, we subtract the components. Or we might deﬁne subtraction by deﬁning a negative vector, −b = −1b, and then we would add the components. It comes to the same thing. The result is shown in Fig. 11-5. This ﬁgure shows d = a − b = a + (−b); we also note that the diﬀerence a − b can be found very easily from a and b by using the equivalent relation a = b + d. Thus the diﬀerence is even easier to ﬁnd than the sum: we just draw the vector from b to a, to get a − b!

Fig. 11-5. The subtraction of vectors.

Next we discuss velocity. Why is velocity a vector? If position is given by the three coordinates (x, y, z), what is the velocity? The velocity is given by dx/dt, dy/dt, and dz/dt. Is that a vector, or not? We can ﬁnd out by diﬀerentiating the expressions in Eq. (11.5) to ﬁnd out whether dx0/dt transforms in the right way. We see that the components dx/dt and dy/dt do transform according to the same law as x and y, and therefore the time derivative is a vector. So the velocity is a vector. We can write the velocity in an interesting way as

v = dr/dt.

What the velocity is, and why it is a vector, can also be understood more pictorially: How far does a particle move in a short time ∆t? Answer: ∆r, so if a particle is「here」at one instant and「there」at another instant, then the vector diﬀerence of the positions ∆r = r2 − r1, which is in the direction of motion

11-12

shown in Fig. 11-6, divided by the time interval ∆t = t2 − t1, is the「average velocity」vector.

Fig. 11-6. The displacement of a particle in a short time interval ∆t =

t2 − t1.

In other words, by vector velocity we mean the limit, as ∆t goes to 0, of the diﬀerence between the radius vectors at the time t + ∆t and the time t, divided by ∆t: (11.10) Thus velocity is a vector because it is the diﬀerence of two vectors. It is also the right deﬁnition of velocity because its components are dx/dt, dy/dt, and dz/dt. In fact, we see from this argument that if we diﬀerentiate any vector with respect to time we produce a new vector. So we have several ways of producing new vectors: (1) multiply by a constant, (2) diﬀerentiate with respect to time, (3) add or subtract two vectors.

(∆r/∆t) = dr/dt.

v = lim ∆t→0

11-6 Newton’s laws in vector notation In order to write Newton’s laws in vector form, we have to go just one step further, and deﬁne the acceleration vector. This is the time derivative of the velocity vector, and it is easy to demonstrate that its components are the second derivatives of x, y, and z with respect to t:

= d2r dt2 , az = dvz dt

= d2z dt2 .

(11.11)

(11.12)

(cid:18) d

=

a = dv dt ay = dvy dt

ax = dvx dt

= d2x dt2 ,

(cid:19)(cid:18) dr

(cid:19)

dt dt = d2y dt2 ,

11-13

With this deﬁnition, then, Newton’s laws can be written in this way:

or

ma = F

(11.13)

m(d2r/dt2) = F .

(11.14) Now the problem of proving the invariance of Newton’s laws under rotation of coordinates is this: prove that a is a vector; this we have just done. Prove that F is a vector; we suppose it is. So if force is a vector, then, since we know acceleration is a vector, Eq. (11.13) will look the same in any coordinate system. Writing it in a form which does not explicitly contain x’s, y’s, and z’s has the advantage that from now on we need not write three laws every time we write Newton’s equations or other laws of physics. We write what looks like one law, but really, of course, it is the three laws for any particular set of axes, because any vector equation involves the statement that each of the components is equal.

Fig. 11-7. A curved trajectory.

The fact that the acceleration is the rate of change of the vector velocity helps us to calculate the acceleration in some rather complicated circumstances. Suppose, for instance, that a particle is moving on some complicated curve (Fig. 11-7) and that, at a given instant t, it had a certain velocity v1, but that when we go to another instant t2 a little later, it has a diﬀerent velocity v2. What is the acceleration? Answer: Acceleration is the diﬀerence in the velocity divided by the small time interval, so we need the diﬀerence of the two velocities. How do we get the diﬀerence of the velocities? To subtract two vectors, we put the vector across the ends of v2 and v1; that is, we draw ∆v as the diﬀerence of the two vectors, right? No! That only works when the tails of the vectors are in the same place! It has no meaning if we move the vector somewhere else and then

11-14

Fig. 11-8. Diagram for calculating the acceleration.

draw a line across, so watch out! We have to draw a new diagram to subtract the vectors. In Fig. 11-8, v1 and v2 are both drawn parallel and equal to their counterparts in Fig. 11-7, and now we can discuss the acceleration. Of course the acceleration is simply ∆v/∆t. It is interesting to note that we can compose the velocity diﬀerence out of two parts; we can think of acceleration as having two components, ∆vk, in the direction tangent to the path and ∆v⊥ at right angles to the path, as indicated in Fig. 11-8. The acceleration tangent to the path is, of course, just the change in the length of the vector, i.e., the change in the speed v: (11.15) The other component of acceleration, at right angles to the curve, is easy to calculate, using Figs. 11-7 and 11-8. In the short time ∆t let the change in angle between v1 and v2 be the small angle ∆θ. If the magnitude of the velocity is called v, then of course

ak = dv/dt.

and the acceleration a will be

∆v⊥ = v ∆θ

a⊥ = v (∆θ/∆t).

Now we need to know ∆θ/∆t, which can be found this way: If, at the given moment, the curve is approximated as a circle of a certain radius R, then in a time ∆t the distance s is, of course, v ∆t, where v is the speed.

∆θ = (v ∆t)/R,

or

∆θ/∆t = v/R.

Therefore, we ﬁnd

as we have seen before.

a⊥ = v2/R,

(11.16)

11-7 Scalar product of vectors Now let us examine a little further the properties of vectors. It is easy to see that the length of a step in space would be the same in any coordinate system.

11-15

That is, if a particular step r is represented by x, y, z, in one coordinate system, and by x0, y0, z0 in another coordinate system, surely the distance r = |r| would be the same in both. Now

and also

r =p r0 =p

x2 + y2 + z2

x02 + y02 + z02.

So what we wish to verify is that these two quantities are equal. It is much more convenient not to bother to take the square root, so let us talk about the square of the distance; that is, let us ﬁnd out whether

x2 + y2 + z2 = x02 + y02 + z02.

(11.17)

It had better be—and if we substitute Eq. (11.5) we do indeed ﬁnd that it is. So we see that there are other kinds of equations which are true for any two coordinate systems.

Something new is involved. We can produce a new quantity, a function of x, y, and z, called a scalar function, a quantity which has no direction but which is the same in both systems. Out of a vector we can make a scalar. We have to ﬁnd a general rule for that. It is clear what the rule is for the case just considered: add the squares of the components. Let us now deﬁne a new thing, which we call a · a. This is not a vector, but a scalar; it is a number that is the same in all coordinate systems, and it is deﬁned to be the sum of the squares of the three components of the vector:

a · a = a2

x

+ a2

y

+ a2 z.

(11.18)

Now you say,「But with what axes?」It does not depend on the axes, the answer is the same in every set of axes. So we have a new kind of quantity, a new invariant or scalar produced by one vector「squared.」If we now deﬁne the following quantity for any two vectors a and b:

a · b = axbx + ayby + azbz,

(11.19)

we ﬁnd that this quantity, calculated in the primed and unprimed systems, also stays the same. To prove it we note that it is true of a · a, b · b, and c · c, where

11-16

c = a + b. Therefore the sum of the squares (ax + bx)2 + (ay + by)2 + (az + bz)2 will be invariant:

(ax + bx)2 + (ay + by)2 + (az + bz)2 = (ax0 + bx0)2

+ (ay0 + by0)2 + (az0 + bz0)2.

(11.20) If both sides of this equation are expanded, there will be cross products of just the type appearing in Eq. (11.19), as well as the sums of squares of the components of a and b. The invariance of terms of the form of Eq. (11.18) then leaves the cross product terms (11.19) invariant also. The quantity a · b is called the scalar product of two vectors, a and b, and it has many interesting and useful properties. For instance, it is easily proved that (11.21) Also, there is a simple geometrical way to calculate a · b, without having to calculate the components of a and b: a · b is the product of the length of a and the length of b times the cosine of the angle between them. Why? Suppose that we choose a special coordinate system in which the x-axis lies along a; in those circumstances, the only component of a that will be there is ax, which is of course the whole length of a. Thus Eq. (11.19) reduces to a · b = axbx for this case, and this is the length of a times the component of b in the direction of a, that is, b cos θ:

a · (b + c) = a · b + a · c.

a · b = ab cos θ.

Therefore, in that special coordinate system, we have proved that a · b is the length of a times the length of b times cos θ. But if it is true in one coordinate system, it is true in all, because a · b is independent of the coordinate system; that is our argument. What good is the dot product? Are there any cases in physics where we need it? Yes, we need it all the time. For instance, in Chapter 4 the kinetic energy was called 1 2 mv2, but if the object is moving in space it should be the velocity squared in the x-direction, the y-direction, and the z-direction, and so the formula for kinetic energy according to vector analysis is ).

(11.22) Energy does not have direction. Momentum has direction; it is a vector, and it is the mass times the velocity vector.

2 m(v · v) = 1

K.E. = 1

+ v2

2 m(v2

x

+ v2

y

z

11-17

Work = F · s.

Another example of a dot product is the work done by a force when something is pushed from one place to the other. We have not yet deﬁned work, but it is equivalent to the energy change, the weights lifted, when a force F acts through a distance s: (11.23) It is sometimes very convenient to talk about the component of a vector in a certain direction (say the vertical direction because that is the direction of gravity). For such purposes, it is useful to invent what we call a unit vector in the direction that we want to study. By a unit vector we mean one whose dot product with itself is equal to unity. Let us call this unit vector i; then i · i = 1. Then, if we want the component of some vector in the direction of i, we see that the dot product a · i will be a cos θ, i.e., the component of a in the direction of i. This is a nice way to get the component; in fact, it permits us to get all the components and to write a rather amusing formula. Suppose that in a given system of coordinates, x, y, and z, we invent three vectors: i, a unit vector in the direction x; j, a unit vector in the direction y; and k, a unit vector in the direction z. Note ﬁrst that i · i = 1. What is i · j? When two vectors are at right angles, their dot product is zero. Thus

i · i = 1 i · j = 0 i · k = 0

j · j = 1 j · k = 0

k · k = 1

(11.24)

Now with these deﬁnitions, any vector whatsoever can be written this way:

a = axi + ayj + azk.

(11.25)

By this means we can go from the components of a vector to the vector itself. This discussion of vectors is by no means complete. However, rather than try to go more deeply into the subject now, we shall ﬁrst learn to use in physical situations some of the ideas so far discussed. Then, when we have properly mastered this basic material, we shall ﬁnd it easier to penetrate more deeply into the subject without getting too confused. We shall later ﬁnd that it is useful to deﬁne another kind of product of two vectors, called the vector product, and written as a × b. However, we shall undertake a discussion of such matters in a later chapter.

11-18

12

