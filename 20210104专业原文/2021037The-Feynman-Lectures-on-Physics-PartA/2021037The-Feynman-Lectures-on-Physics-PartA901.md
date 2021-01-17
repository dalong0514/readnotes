Newton’s Laws of Dynamics

9-1 Momentum and forceThe discovery of the laws of dynamics, or the laws of motion, was a dramaticmoment in the history of science. Before Newton’s time, the motions of things likethe planets were a mystery, but after Newton there was complete understanding.Even the slight deviations from Kepler’s laws, due to the perturbations of theplanets, were computable. The motions of pendulums, oscillators with springsand weights in them, and so on, could all be analyzed completely after Newton’slaws were enunciated. So it is with this chapter: before this chapter we couldnot calculate how a mass on a spring would move; much less could we calculatethe perturbations on the planet Uranus due to Jupiter and Saturn. After thischapter we will be able to compute not only the motion of the oscillating mass,but also the perturbations on the planet Uranus produced by Jupiter and Saturn!Galileo made a great advance in the understanding of motion when he dis-covered the principle of inertia: if an object is left alone, is not disturbed, itcontinues to move with a constant velocity in a straight line if it was originallymoving, or it continues to stand still if it was just standing still. Of course thisnever appears to be the case in nature, for if we slide a block across a table itstops, but that is because it is not left to itself—it is rubbing against the table.It required a certain imagination to ﬁnd the right rule, and that imagination wassupplied by Galileo.

Of course, the next thing which is needed is a rule for ﬁnding how an objectchanges its speed if something is aﬀecting it. That is, the contribution of Newton.Newton wrote down three laws: The First Law was a mere restatement of theGalilean principle of inertia just described. The Second Law gave a speciﬁc wayof determining how the velocity changes under diﬀerent inﬂuences called forces.The Third Law describes the forces to some extent, and we shall discuss thatat another time. Here we shall discuss only the Second Law, which asserts thatthe motion of an object is changed by forces in this way: the time-rate-of-change

9-1

of a quantity called momentum is proportional to the force. We shall state thismathematically shortly, but let us ﬁrst explain the idea.Momentum is not the same as velocity. A lot of words are used in physics,and they all have precise meanings in physics, although they may not have suchprecise meanings in everyday language. Momentum is an example, and we mustdeﬁne it precisely. If we exert a certain push with our arms on an object thatis light, it moves easily; if we push just as hard on another object that is muchheavier in the usual sense, then it moves much less rapidly. Actually, we mustchange the words from「light」and「heavy」to less massive and more massive,because there is a diﬀerence to be understood between the weight of an objectand its inertia. (How hard it is to get it going is one thing, and how much itweighs is something else.) Weight and inertia are proportional, and on the earth’ssurface are often taken to be numerically equal, which causes a certain confusionto the student. On Mars, weights would be diﬀerent but the amount of forceneeded to overcome inertia would be the same.

We use the term mass as a quantitative measure of inertia, and we maymeasure mass, for example, by swinging an object in a circle at a certain speedand measuring how much force we need to keep it in the circle. In this way weﬁnd a certain quantity of mass for every object. Now the momentum of an objectis a product of two parts: its mass and its velocity. Thus Newton’s Second Lawmay be written mathematically this way:

F = ddt

(mv).

(9.1)

Now there are several points to be considered. In writing down any law such asthis, we use many intuitive ideas, implications, and assumptions which are atﬁrst combined approximately into our「law.」Later we may have to come backand study in greater detail exactly what each term means, but if we try to do thistoo soon we shall get confused. Thus at the beginning we take several things forgranted. First, that the mass of an object is constant; it isn’t really, but we shallstart out with the Newtonian approximation that mass is constant, the same allthe time, and that, further, when we put two objects together, their masses add.These ideas were of course implied by Newton when he wrote his equation, forotherwise it is meaningless. For example, suppose the mass varied inversely asthe velocity; then the momentum would never change in any circumstance, sothe law means nothing unless you know how the mass changes with velocity. Atﬁrst we say, it does not change.

9-2

Then there are some implications concerning force. As a rough approximationwe think of force as a kind of push or pull that we make with our muscles, butwe can deﬁne it more accurately now that we have this law of motion. The mostimportant thing to realize is that this relationship involves not only changes inthe magnitude of the momentum or of the velocity but also in their direction. Ifthe mass is constant, then Eq. (9.1) can also be written as

F = m

dvdt

= ma.

(9.2)

The acceleration a is the rate of change of the velocity, and Newton’s SecondLaw says more than that the eﬀect of a given force varies inversely as the mass;it says also that the direction of the change in the velocity and the direction ofthe force are the same. Thus we must understand that a change in a velocity, oran acceleration, has a wider meaning than in common language: The velocityof a moving object can change by its speeding up, slowing down (when it slowsdown, we say it accelerates with a negative acceleration), or changing its directionof motion. An acceleration at right angles to the velocity was discussed inChapter 7. There we saw that an object moving in a circle of radius R with acertain speed v along the circle falls away from a straightline path by a distanceequal to 12(v2/R)t2 if t is very small. Thus the formula for acceleration at rightangles to the motion is(9.3)and a force at right angles to the velocity will cause an object to move in a curvedpath whose radius of curvature can be found by dividing the force by the massto get the acceleration, and then using (9.3).

a = v2/R,

9-2 Speed and velocityIn order to make our language more precise, we shall make one furtherdeﬁnition in our use of the words speed and velocity. Ordinarily we think of speedand velocity as being the same, and in ordinary language they are the same. Butin physics we have taken advantage of the fact that there are two words and havechosen to use them to distinguish two ideas. We carefully distinguish velocity,which has both magnitude and direction, from speed, which we choose to meanthe magnitude of the velocity, but which does not include the direction. We canformulate this more precisely by describing how the x-, y-, and z-coordinates

9-3

Fig. 9-1. A small displacement of an object.

of an object change with time. Suppose, for example, that at a certain instantan object is moving as shown in Fig. 9-1. In a given small interval of time ∆tit will move a certain distance ∆x in the x-direction, ∆y in the y-direction,and ∆z in the z-direction. The total eﬀect of these three coordinate changes is adisplacement ∆s along the diagonal of a parallelepiped whose sides are ∆x, ∆y,and ∆z. In terms of the velocity, the displacement ∆x is the x-component of thevelocity times ∆t, and similarly for ∆y and ∆z:

∆x = vx ∆t,

∆y = vy ∆t,

∆z = vz ∆t.

(9.4)

9-3 Components of velocity, acceleration, and forceIn Eq. (9.4) we have resolved the velocity into components by telling how fastthe object is moving in the x-direction, the y-direction, and the z-direction. Thevelocity is completely speciﬁed, both as to magnitude and direction, if we givethe numerical values of its three rectangular components:

vy = dy/dt,On the other hand, the speed of the object is

vx = dx/dt,

vz = dz/dt.

ds/dt = |v| =q

v2x

+ v2

y

+ v2z .

(9.5)

(9.6)

Next, suppose that, because of the action of a force, the velocity changesto some other direction and a diﬀerent magnitude, as shown in Fig. 9-2. We

9-4

Fig. 9-2. A change in velocity in which both the magnitude and

direction change.

can analyze this apparently complex situation rather simply if we evaluate thechanges in the x-, y-, and z-components of velocity. The change in the componentof the velocity in the x-direction in a time ∆t is ∆vx = ax ∆t, where ax is whatwe call the x-component of the acceleration. Similarly, we see that ∆vy = ay ∆tand ∆vz = az ∆t. In these terms, we see that Newton’s Second Law, in sayingthat the force is in the same direction as the acceleration, is really three laws, inthe sense that the component of the force in the x-, y-, or z-direction is equal tothe mass times the rate of change of the corresponding component of velocity:

Fx = m(dvx/dt) = m(d2x/dt2) = max,Fy = m(dvy/dt) = m(d2y/dt2) = may,Fz = m(dvz /dt) = m(d2z /dt2) = maz .

(9.7)

Just as the velocity and acceleration have been resolved into components byprojecting a line segment representing the quantity, and its direction onto threecoordinate axes, so, in the same way, a force in a given direction is representedby certain components in the x-, y-, and z-directions:

Fx = F cos (x, F),Fy = F cos (y, F),Fz = F cos (z , F),

9-5

(9.8)

where F is the magnitude of the force and (x, F) represents the angle betweenthe x-axis and the direction of F, etc.

Newton’s Second Law is given in complete form in Eq. (9.7). If we knowthe forces on an object and resolve them into x-, y-, and z-components, thenwe can ﬁnd the motion of the object from these equations. Let us consider asimple example. Suppose there are no forces in the y- and z-directions, the onlyforce being in the x-direction, say vertically. Equation (9.7) tells us that therewould be changes in the velocity in the vertical direction, but no changes inthe horizontal direction. This was demonstrated with a special apparatus inChapter 7 (see Fig. 7-3). A falling body moves horizontally without any changein horizontal motion, while it moves vertically the same way as it would moveif the horizontal motion were zero. In other words, motions in the x-, y-, andz-directions are independent if the forces are not connected.

9-4 What is the force?In order to use Newton’s laws, we have to have some formula for the force;these laws say pay attention to the forces. If an object is accelerating, someagency is at work; ﬁnd it. Our program for the future of dynamics must be toﬁnd the laws for the force. Newton himself went on to give some examples. In thecase of gravity he gave a speciﬁc formula for the force. In the case of other forceshe gave some part of the information in his Third Law, which we will study inthe next chapter, having to do with the equality of action and reaction.

Extending our previous example, what are the forces on objects near theearth’s surface? Near the earth’s surface, the force in the vertical direction due togravity is proportional to the mass of the object and is nearly independent of heightfor heights small compared with the earth’s radius R: F = GmM/R2 = mg,where g = GM/R2 is called the acceleration of gravity. Thus the law of gravitytells us that weight is proportional to mass; the force is in the vertical directionand is the mass times g. Again we ﬁnd that the motion in the horizontal directionis at constant velocity. The interesting motion is in the vertical direction, andNewton’s Second Law tells us

mg = m(d2x/dt2).

(9.9)

Cancelling the m’s, we ﬁnd that the acceleration in the x-direction is constantand equal to g. This is of course the well known law of free fall under gravity,

9-6

Fig. 9-3. A mass on a spring.

which leads to the equations

vx = v0 + gt,x = x0 + v0t + 1

2 gt2.

(9.10)

As another example, let us suppose that we have been able to build a gad-get (Fig. 9-3) which applies a force proportional to the distance and directedoppositely—a spring. If we forget about gravity, which is of course balanced outby the initial stretch of the spring, and talk only about excess forces, we see thatif we pull the mass down, the spring pulls up, while if we push it up the springpulls down. This machine has been designed carefully so that the force is greater,the more we pull it up, in exact proportion to the displacement from the balancedcondition, and the force upward is similarly proportional to how far we pull down.If we watch the dynamics of this machine, we see a rather beautiful motion—up,down, up, down, . . . The question is, will Newton’s equations correctly describethis motion? Let us see whether we can exactly calculate how it moves with thisperiodic oscillation, by applying Newton’s law (9.7). In the present instance, theequation is

− kx = m(dvx/dt).

(9.11)Here we have a situation where the velocity in the x-direction changes at a rateproportional to x. Nothing will be gained by retaining numerous constants, sowe shall imagine either that the scale of time has changed or that there is anaccident in the units, so that we happen to have k/m = 1. Thus we shall try tosolve the equation

(9.12)To proceed, we must know what vx is, but of course we know that the velocity isthe rate of change of the position.

dvx/dt = −x.

9-7

9-5 Meaning of the dynamical equations

Now let us try to analyze just what Eq. (9.12) means. Suppose that at a giventime t the object has a certain velocity vx and position x. What is the velocityand what is the position at a slightly later time t + ? If we can answer thisquestion our problem is solved, for then we can start with the given condition andcompute how it changes for the ﬁrst instant, the next instant, the next instant,and so on, and in this way we gradually evolve the motion. To be speciﬁc, let ussuppose that at the time t = 0 we are given that x = 1 and vx = 0. Why doesthe object move at all? Because there is a force on it when it is at any positionexcept x = 0. If x > 0, that force is upward. Therefore the velocity which iszero starts to change, because of the law of motion. Once it starts to build upsome velocity the object starts to move up, and so on. Now at any time t, if  isvery small, we may express the position at time t +  in terms of the position attime t and the velocity at time t to a very good approximation as

x(t + ) = x(t) + vx(t).

(9.13)

The smaller the , the more accurate this expression is, but it is still usefullyaccurate even if  is not vanishingly small. Now what about the velocity? Inorder to get the velocity later, the velocity at the time t + , we need to knowhow the velocity changes, the acceleration. And how are we going to ﬁnd theacceleration? That is where the law of dynamics comes in. The law of dynamicstells us what the acceleration is. It says the acceleration is −x.

vx(t + ) = vx(t) + ax(t)= vx(t) − x(t).

(9.14)(9.15)

Equation (9.14) is merely kinematics; it says that a velocity changes because ofthe presence of acceleration. But Eq. (9.15) is dynamics, because it relates theacceleration to the force; it says that at this particular time for this particularproblem, you can replace the acceleration by −x(t). Therefore, if we know boththe x and v at a given time, we know the acceleration, which tells us the newvelocity, and we know the new position—this is how the machinery works. Thevelocity changes a little bit because of the force, and the position changes a littlebit because of the velocity.

9-8

9-6 Numerical solution of the equationsNow let us really solve the problem. Suppose that we take  = 0.100 sec. Afterwe do all the work if we ﬁnd that this is not small enough we may have to go backand do it again with  = 0.010 sec. Starting with our initial value x(0) = 1.00,what is x(0.1)? It is the old position x(0) plus the velocity (which is zero) times0.10 sec. Thus x(0.1) is still 1.00 because it has not yet started to move. Butthe new velocity at 0.10 sec will be the old velocity v(0) = 0 plus  times theacceleration. The acceleration is −x(0) = −1.00. Thus

Now at 0.20 sec

and

v(0.1) = 0.00 − 0.10 × 1.00 = −0.10.

x(0.2) = x(0.1) + v(0.1)

= 1.00 − 0.10 × 0.10 = 0.99

v(0.2) = v(0.1) + a(0.1)

= −0.10 − 0.10 × 1.00 = −0.20.

And so, on and on and on, we can calculate the rest of the motion, and that is justwhat we shall do. However, for practical purposes there are some little tricks bywhich we can increase the accuracy. If we continued this calculation as we havestarted it, we would ﬁnd the motion only rather crudely because  = 0.100 secis rather crude, and we would have to go to a very small interval, say  = 0.01.Then to go through a reasonable total time interval would take a lot of cyclesof computation. So we shall organize the work in a way that will increase theprecision of our calculations, using the same coarse interval  = 0.10 sec. Thiscan be done if we make a subtle improvement in the technique of the analysis.Notice that the new position is the old position plus the time interval  timesthe velocity. But the velocity when? The velocity at the beginning of the timeinterval is one velocity and the velocity at the end of the time interval is anothervelocity. Our improvement is to use the velocity halfway between. If we knowthe speed now, but the speed is changing, then we are not going to get the rightanswer by going at the same speed as now. We should use some speed betweenthe「now」speed and the「then」speed at the end of the interval. The sameconsiderations also apply to the velocity: to compute the velocity changes, weshould use the acceleration midway between the two times at which the velocityis to be found. Thus the equations that we shall actually use will be something

9-9

Table 9-1

Solution of dvx/dt = −xInterval:  = 0.10 sec

t0.0

0.1

0.2

0.3

0.4

0.5

0.6

0.7

0.8

0.9

1.0

1.1

1.2

1.3

1.4

x1.000

0.995

0.980

0.955

0.921

0.877

0.825

0.764

0.696

0.621

0.540

0.453

0.362

0.267

0.169

1.50.0701.6 −0.030

ax

vx0.000 −1.000−0.050−0.995−0.150−0.980−0.248−0.955−0.343−0.921−0.435−0.877−0.523−0.825−0.605−0.764−0.682−0.696−0.751−0.621−0.814−0.540−0.868−0.453−0.913−0.362−0.949−0.267−0.976−0.169−0.993−0.070−1.000

+0.030

9-10

like this: the position later is equal to the position before plus  times the velocityat the time in the middle of the interval. Similarly, the velocity at this halfwaypoint is the velocity at a time  before (which is in the middle of the previousinterval) plus  times the acceleration at the time t. That is, we use the equations

x(t + ) = x(t) + v(t + /2),v(t + /2) = v(t − /2) + a(t),

a(t) = −x(t).

(9.16)

There remains only one slight problem: what is v(/2)? At the start, we aregiven v(0), not v(−/2). To get our calculation started, we shall use a specialequation, namely, v(/2) = v(0) + (/2)a(0).Now we are ready to carry through our calculation. For convenience, wemay arrange the work in the form of a table, with columns for the time, theposition, the velocity, and the acceleration, and the in-between lines for thevelocity, as shown in Table 9-1. Such a table is, of course, just a convenient wayof representing the numerical values obtained from the set of equations (9.16),and in fact the equations themselves need never be written. We just ﬁll in thevarious spaces in the table one by one. This table now gives us a very good ideaof the motion: it starts from rest, ﬁrst picks up a little upward (negative) velocityand it loses some of its distance. The acceleration is then a little bit less butit is still gaining speed. But as it goes on it gains speed more and more slowly,until as it passes x = 0 at about t = 1.50 sec we can conﬁdently predict that itwill keep going, but now it will be on the other side; the position x will becomenegative, the acceleration therefore positive. Thus the speed decreases. It isinteresting to compare these numbers with the function x = cos t, which is donein Fig. 9-4. The agreement is within the three signiﬁcant ﬁgure accuracy of ourcalculation! We shall see later that x = cos t is the exact mathematical solutionof our equation of motion, but it is an impressive illustration of the power ofnumerical analysis that such an easy calculation should give such precise results.

9-7 Planetary motionsThe above analysis is very nice for the motion of an oscillating spring, but canwe analyze the motion of a planet around the sun? Let us see whether we canarrive at an approximation to an ellipse for the orbit. We shall suppose that thesun is inﬁnitely heavy, in the sense that we shall not include its motion. Suppose

9-11

Fig. 9-4. Graph of the motion of a mass on a spring.

a planet starts at a certain place and is moving with a certain velocity; it goesaround the sun in some curve, and we shall try to analyze, by Newton’s laws ofmotion and his law of gravitation, what the curve is. How? At a given moment itis at some position in space. If the radial distance from the sun to this positionis called r, then we know that there is a force directed inward which, accordingto the law of gravity, is equal to a constant times the product of the sun’s massand the planet’s mass divided by the square of the distance. To analyze thisfurther we must ﬁnd out what acceleration will be produced by this force. Weshall need the components of the acceleration along two directions, which we callx and y. Thus if we specify the position of the planet at a given moment bygiving x and y (we shall suppose that z is always zero because there is no forcein the z-direction and, if there is no initial velocity vz, there will be nothing tomake z other than zero), the force is directed along the line joining the planet tothe sun, as shown in Fig. 9-5.

Fig. 9-5. The force of gravity on a planet.

9-12

From this ﬁgure we see that the horizontal component of the force is relatedto the complete force in the same manner as the horizontal distance x is to thecomplete hypotenuse r, because the two triangles are similar. Also, if x is positive,Fx is negative. That is, Fx/|F| = −x/r, or Fx = −|F|x/r = −GM mx/r3. Nowwe use the dynamical law to ﬁnd that this force component is equal to the massof the planet times the rate of change of its velocity in the x-direction. Thus weﬁnd the following laws:

m(dvx/dt) = −GM mx/r3,m(dvy/dt) = −GM my/r3,

r =p

x2 + y2.

(9.17)

This, then, is the set of equations we must solve. Again, in order to simplifythe numerical work, we shall suppose that the unit of time, or the mass of thesun, has been so adjusted (or luck is with us) that GM ≡ 1. For our speciﬁcexample we shall suppose that the initial position of the planet is at x = 0.500and y = 0.000, and that the velocity is all in the, y-direction at the start, andis of magnitude 1.630. Now how do we make the calculation? We again makea table with columns for the time, the x-position, the x-velocity vx, and thex-acceleration ax; then, separated by a double line, three columns for position,velocity, and acceleration in the y-direction. In order to get the accelerations weare going to need Eq. (9.17); it tells us that the acceleration in the x-directionis −x/r3, and the acceleration in the y-direction is −y/r3, and that r is thesquare root of x2 + y2. Thus, given x and y, we must do a little calculating on theside, taking the square root of the sum of the squares to ﬁnd r and then, to getready to calculate the two accelerations, it is useful also to evaluate 1/r3. Thiswork can be done rather easily by using a table of squares, cubes, and reciprocals:then we need only multiply x by 1/r3, which we do on a slide rule.0.100: Initial values at t = 0:

Our calculation thus proceeds by the following steps, using time intervals  =

From these we ﬁnd:

x(0) = 0.500vx(0) = 0.000

y(0) = 0.000vy(0) = +1.630

r(0) = 0.500ax = −4.000

1/r3(0) = 8.000ay = 0.000

9-13

Thus we may calculate the velocities vx(0.05) and vy(0.05):vx(0.05) = 0.000 − 4.000 × 0.050 = −0.200;vy(0.05) = 1.630 + 0.000 × 0.050 = 1.630.

Now our main calculations begin:

x(0.1) = 0.500 − 0.20 × 0.1y(0.1) = 0.0 + 1.63 × 0.1

r =p0.4802 + 0.1632

= 0.480= 0.163= 0.507

1/r3 = 7.677

= −3.685ax(0.1) = −0.480 × 7.677ay(0.1) = −0.163 × 7.677= −1.250vx(0.15) = −0.200 − 3.685 × 0.1 = −0.568vy(0.15) = 1.630 − 1.250 × 0.1 = 1.505x(0.2) = 0.480 − 0.568 × 0.1 = 0.423y(0.2) = 0.163 + 1.505 × 0.1 = 0.313

etc.

In this way we obtain the values given in Table 9-2, and in 20 steps or so wehave chased the planet halfway around the sun! In Fig. 9-6 are plotted the x-and y-coordinates given in Table 9-2. The dots represent the positions at thesuccession of times a tenth of a unit apart; we see that at the start the planetmoves rapidly and at the end it moves slowly, and so the shape of the curve isdetermined. Thus we see that we really do know how to calculate the motion ofplanets!

Solution of dvx/dt = −x/r3, dvy/dt = −y/r3, r =px2 + y2.

Table 9-2

at

t = 0

ay0.000

r

0.500

1/r38.000

Orbit

vy = 1.63 vx = 0 x = 0.5 y = 0

Interval:  = 0.100

t0.0

x0.500

vx

−0.200

ax

−4.000

y0.000

vy

1.630

9-14

t0.1

0.2

0.3

0.4

x0.480

0.423

0.337

0.232

0.50.1150.6 −0.0060.7 −0.1270.8 −0.2440.9 −0.3561.0 −0.4611.1 −0.5581.2 −0.6461.3 −0.7251.4 −0.7951.5 −0.8561.6 −0.9081.7 −0.9501.8 −0.9821.9 −1.005

vx

−0.568−0.858−1.054−1.165−1.211−1.209−1.175−1.119−1.048−0.969−0.883−0.794−0.702−0.608−0.514−0.420−0.325−0.229

ax

−3.685−2.897−1.958−1.112−0.454

+0.018

+0.342

+0.559

+0.702

+0.796

+0.856

+0.895

+0.919

+0.933

+0.942

+0.947

+0.950

+0.952

+0.953

Table 9-2

y0.163

0.313

0.443

0.546

0.623

0.676

0.706

0.718

0.713

0.694

0.664

0.623

0.573

0.516

0.453

0.385

0.313

0.238

0.160

9-15

vy

1.505

1.290

1.033

0.772

0.527

0.308

0.117−0.048−0.189−0.309−0.411−0.497−0.569−0.630−0.680−0.720−0.751−0.774

ay

−1.251−2.146−2.569−2.617−2.449−2.190−1.911−1.646−1.408−1.200−1.019−0.862−0.726−0.605−0.498−0.402−0.313−0.230−0.152

r

0.507

1/r37.677

0.527

6.847

0.556

5.805

0.593

4.794

0.634

3.931

0.676

3.241

0.718

2.705

0.758

2.292

0.797

1.974

0.833

1.728

0.867

1.536

0.897

1.385

0.924

1.267

0.948

1.174

0.969

1.100

0.986

1.043

1.000

1.000

1.010

0.969

1.018

0.949

Table 9-2

x

t2.0 −1.0182.1 −1.0222.2 −1.017

2.3

vx

−0.134−0.038

+0.057

ax

y

+0.955

0.081

+0.9570.002+0.959 −0.078

vy

−0.790−0.797−0.797−0.790

ay

−0.076−0.002

r

1/r3

1.022

0.938

1.022

0.936

+0.074

1.020

0.944

Crossed x-axis at 2.101 sec, ∴ period = 4.20 sec.vx = 0 at 2.086 sec.Cross x at −1.022, ∴ semimajor axis = 1.022 + 0.500vy = 0.797.

2

Predicted time π(0.761)3/2 = π(0.663) = 2.082.

= 0.761.

Fig. 9-6. The calculated motion of a planet around the sun.

Now let us see how we can calculate the motion of Neptune, Jupiter, Uranus,or any other planet. If we have a great many planets, and let the sun movetoo, can we do the same thing? Of course we can. We calculate the force ona particular planet, let us say planet number i, which has a position xi, yi, zi(i = 1 may represent the sun, i = 2 Mercury, i = 3 Venus, and so on). We mustknow the positions of all the planets. The force acting on one is due to all theother bodies which are located, let us say, at positions xj, yj, zj. Therefore the

9-16

equations are

mi

dvixdt

mi

mi

dviydt

dvizdt

=

=

=

j=1

NXNXNX

j=1

j=1

− Gmimj(xi − xj)

r3ij

− Gmimj(yi − yj)

r3ij

− Gmimj(zi − zj )

r3ij

,

,

.

(9.18)

Further, we deﬁne rij as the distance between the two planets i and j; this isequal to

rij =q(xi − xj)2 + (yi − yj)2 + (zi − zj)2.

(9.19)

Also,P means a sum over all values of j—all other bodies—except, of course,

for j = i. Thus all we have to do is to make more columns, lots more columns.We need nine columns for the motions of Jupiter, nine for the motions of Saturn,and so on. Then when we have all initial positions and velocities we can calculateall the accelerations from Eq. (9.18) by ﬁrst calculating all the distances, usingEq. (9.19). How long will it take to do it? If you do it at home, it will take avery long time! But in modern times we have machines which do arithmeticvery rapidly; a very good computing machine may take 1 microsecond, that is, amillionth of a second, to do an addition. To do a multiplication takes longer, say10 microseconds. It may be that in one cycle of calculation, depending on theproblem, we may have 30 multiplications, or something like that, so one cycle willtake 300 microseconds. That means that we can do 3000 cycles of computationper second. In order to get an accuracy, of, say, one part in a billion, we wouldneed 4 × 105 cycles to correspond to one revolution of a planet around the sun.That corresponds to a computation time of 130 seconds or about two minutes.Thus it take only two minutes to follow Jupiter around the sun, with all theperturbations of all the planets correct to one part in a billion, by this method!(It turns out that the error varies about as the square of the interval . If wemake the interval a thousand times smaller, it is a million times more accurate.So, let us make the interval 10,000 times smaller.)So, as we said, we began this chapter not knowing how to calculate eventhe motion of a mass on a spring. Now, armed with the tremendous power of

9-17

Newton’s laws, we can not only calculate such simple motions but also, givenonly a machine to handle the arithmetic, even the tremendously complex motionsof the planets, to as high a degree of precision as we wish!

9-18

10

