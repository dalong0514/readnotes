Linear Systems and Review

25-1 Linear diﬀerential equationsIn this chapter we shall discuss certain aspects of oscillating systems that arefound somewhat more generally than just in the particular systems we have beendiscussing. For our particular system, the diﬀerential equation that we have beensolving is

+ γm

dxdt

d2xdt2

m

+ mω2

0x = F(t).

(25.1)Now this particular combination of「operations」on the variable x has theinteresting property that if we substitute (x+ y) for x, then we get the sum of thesame operations on x and y; or, if we multiply x by a, then we get just a timesthe same combination. This is easy to prove. Just as a「shorthand」notation,because we get tired of writing down all those letters in (25.1), we shall use thesymbol L(x) instead. When we see this, it means the left-hand side of (25.1),with x substituted in. With this system of writing, L(x + y) would mean thefollowing:

L(x + y) = m

d2(x + y)

dt2

+ γm

d(x + y)

dt

+ mω2

0(x + y).

(25.2)

(We underline the L so as to remind ourselves that it is not an ordinary function.)We sometimes call this an operator notation, but it makes no diﬀerence what wecall it, it is just「shorthand.」

Our ﬁrst statement was that

(25.3)which of course follows from the fact that a(x + y) = ax + ay, d(x + y)/dt =dx/dt + dy/dt, etc.

L(x + y) = L(x) + L(y),

25-1

Our second statement was, for constant a,L(ax) = aL(x).

(25.4)[Actually, (25.3) and (25.4) are very closely related, because if we put x + xinto (25.3), this is the same as setting a = 2 in (25.4), and so on.]In more complicated problems, there may be more derivatives, and moreterms in L; the question of interest is whether the two equations (25.3) and (25.4)are maintained or not. If they are, we call such a problem a linear problem. Inthis chapter we shall discuss some of the properties that exist because the systemis linear, to appreciate the generality of some of the results that we have obtainedin our special analysis of a special equation.

L(x) = 0.

Now let us study some of the properties of linear diﬀerential equations, havingillustrated them already with the speciﬁc equation (25.1) that we have studiedso closely. The ﬁrst property of interest is this: suppose that we have to solvethe diﬀerential equation for a transient, the free oscillation with no driving force.That is, we want to solve

(25.5)Suppose that, by some hook or crook, we have found a particular solution, whichwe shall call x1. That is, we have an x1 for which L(x1) = 0. Now we noticethat ax1, is also a solution to the same equation; we can multiply this specialsolution by any constant whatever, and get a new solution. In other words, if wehad a motion of a certain「size,」then a motion twice as「big」is again a solution.Proof: L(ax1) = aL(x1) = a · 0 = 0.Next, suppose that, by hook or by crook, we have not only found one solu-tion x1, but also another solution, x2. (Remember that when we substitutedx = eiαt for ﬁnding the transients, we found two values for α, that is, two solutions,x1 and x2.) Now let us show that the combination (x1 + x2) is also a solution. Inother words, if we put x = x1 + x2, x is again a solution of the equation. Why?Because, if L(x1) = 0 and L(x2) = 0, then L(x1+x2) = L(x1)+L(x2) = 0+0 = 0.So if we have found a number of solutions for the motion of a linear system wecan add them together.

Combining these two ideas, we see, of course, that we can also add six ofone and two of the other: if x1 is a solution, so is αx1. Therefore any sum ofthese two solutions, such as (αx1 + βx2), is also a solution. If we happen tobe able to ﬁnd three solutions, then we ﬁnd that any combination of the threesolutions is again a solution, and so on. It turns out that the number of what

25-2

we call independent solutions* that we have obtained for our oscillator problemis only two. The number of independent solutions that one ﬁnds in the generalcase depends upon what is called the number of degrees of freedom. We shallnot discuss this in detail now, but if we have a second-order diﬀerential equation,there are only two independent solutions, and we have found both of them; sowe have the most general solution.

Now let us go on to another proposition, which applies to the situation in

which the system is subjected to an outside force. Suppose the equation is

L(x) = F(t),

(25.6)

and suppose that we have found a special solution of it. Let us say that Joe’ssolution is xJ, and that L(xJ) = F(t). Suppose we want to ﬁnd yet anothersolution; suppose we add to Joe’s solution one of those that was a solution of thefree equation (25.5), say x1. Then we see by (25.3) that

L(xJ + x1) = L(xJ) + L(x1) = F(t) + 0 = F(t).

(25.7)

Therefore, to the「forced」solution we can add any「free」solution, and we stillhave a solution. The free solution is called a transient solution.When we have no force acting, and suddenly turn one on, we do not imme-diately get the steady solution that we solved for with the sine wave solution,but for a while there is a transient which sooner or later dies out, if we wait longenough. The「forced」solution does not die out, since it keeps on being drivenby the force. Ultimately, for long periods of time, the solution is unique, butinitially the motions are diﬀerent for diﬀerent circumstances, depending on howthe system was started.

25-2 Superposition of solutionsNow we come to another interesting proposition. Suppose that we have acertain particular driving force Fa (let us say an oscillatory one with a certainω = ωa, but our conclusions will be true for any functional form of Fa) and wehave solved for the forced motion (with or without the transients; it makes nodiﬀerence). Now suppose some other force is acting, let us say Fb, and we solve

* Solutions which cannot be expressed as linear combinations of each other are called

independent.

25-3

the same problem, but for this diﬀerent force. Then suppose someone comesalong and says,「I have a new problem for you to solve; I have the force Fa + Fb.」Can we do it? Of course we can do it, because the solution is the sum of thetwo solutions xa and xb for the forces taken separately—a most remarkablecircumstance indeed. If we use (25.3), we see that

L(xa + xb) = L(xa) + L(xb) = Fa(t) + Fb(t).

(25.8)This is an example of what is called the principle of superposition for linearsystems, and it is very important. It means the following: if we have a complicatedforce which can be broken up in any convenient manner into a sum of separatepieces, each of which is in some way simple, in the sense that for each specialpiece into which we have divided the force we can solve the equation, then theanswer is available for the whole force, because we may simply add the pieces ofthe solution back together, in the same manner as the total force is compoundedout of pieces (Fig. 25-1).

Fig. 25-1. An example of the principle of superposition for linear

systems.

25-4

Let us give another example of the principle of superposition. In Chapter 12we said that it was one of the great facts of the laws of electricity that if we havea certain distribution of charges qa and calculate the electric ﬁeld Ea arising fromthese charges at a certain place P, and if, on the other hand, we have anotherset of charges qb and we calculate the ﬁeld Eb due to these at the correspondingplace, then if both charge distributions are present at the same time, the ﬁeld Eat P is the sum of Ea due to one set plus Eb due to the other. In other words,if we know the ﬁeld due to a certain charge, then the ﬁeld due to many chargesis merely the vector sum of the ﬁelds of these charges taken individually. Thisis exactly analogous to the above proposition that if we know the result of twogiven forces taken at one time, then if the force is considered as a sum of them,the response is a sum of the corresponding individual responses.

Fig. 25-2. The principle of superposition in electrostatics.

The reason why this is true in electricity is that the great laws of electricity,Maxwell’s equations, which determine the electric ﬁeld, turn out to be diﬀerentialequations which are linear, i.e., which have the property (25.3). What correspondsto the force is the charge generating the electric ﬁeld, and the equation whichdetermines the electric ﬁeld in terms of the charge is linear.

As another interesting example of this proposition, let us ask how it is possibleto「tune in」to a particular radio station at the same time as all the radio stationsare broadcasting. The radio station transmits, fundamentally, an oscillatingelectric ﬁeld of very high frequency which acts on our radio antenna. It is truethat the amplitude of the oscillation of the ﬁeld is changed, modulated, to carrythe signal of the voice, but that is very slow, and we are not going to worry aboutit. When one hears「This station is broadcasting at a frequency of 780 kilocycles,」this indicates that 780,000 oscillations per second is the frequency of the electricﬁeld of the station antenna, and this drives the electrons up and down at thatfrequency in our antenna. Now at the same time we may have another radiostation in the same town radiating at a diﬀerent frequency, say 550 kilocycles persecond; then the electrons in our antenna are also being driven by that frequency.Now the question is, how is it that we can separate the signals coming into the

25-5

one radio at 780 kilocycles from those coming in at 550 kilocycles? We certainlydo not hear both stations at the same time.

By the principle of superposition, the response of the electric circuit in theradio, the ﬁrst part of which is a linear circuit, to the forces that are acting dueto the electric ﬁeld Fa + Fb, is xa + xb. It therefore looks as though we will neverdisentangle them. In fact, the very proposition of superposition seems to insistthat we cannot avoid having both of them in our system. But remember, for aresonant circuit, the response curve, the amount of x per unit F, as a function ofthe frequency, looks like Fig. 25-3. If it were a very high Q circuit, the responsewould show a very sharp maximum. Now suppose that the two stations arecomparable in strength, that is, the two forces are of the same magnitude. Theresponse that we get is the sum of xa and xb. But, in Fig. 25-3, xa is tremendous,while xb is small. So, in spite of the fact that the two signals are equal in strength,when they go through the sharp resonant circuit of the radio tuned for ωa, thefrequency of the transmission of one station, then the response to this stationis much greater than to the other. Therefore the complete response, with bothsignals acting, is almost all made up of ωa, and we have selected the station wewant.

Fig. 25-3. A sharply tuned resonance curve.

Now what about the tuning? How do we tune it? We change ω0 by changingthe L or the C of the circuit, because the frequency of the circuit has to do withthe combination of L and C. In particular, most radios are built so that one canchange the capacitance. When we retune the radio, we can make a new settingof the dial, so that the natural frequency of the circuit is shifted, say, to ωc. Inthose circumstances we hear neither one station nor the other; we get silence,provided there is no other station at frequency ωc. If we keep on changing the

25-6

capacitance until the resonance curve is at ωb, then of course we hear the otherstation. That is how radio tuning works; it is again the principle of superposition,combined with a resonant response.*

To conclude this discussion, let us describe qualitatively what happens if weproceed further in analyzing a linear problem with a given force, when the force isquite complicated. Out of the many possible procedures, there are two especiallyuseful general ways that we can solve the problem. One is this: suppose that wecan solve it for special known forces, such as sine waves of diﬀerent frequencies.We know it is child’s play to solve it for sine waves. So we have the so-called「child’s play」cases. Now the question is whether our very complicated forcecan be represented as the sum of two or more「child’s play」forces. In Fig. 25-1we already had a fairly complicated curve, and of course we can make it morecomplicated still if we add in more sine waves. So it is certainly possible toobtain very complicated curves. And, in fact, the reverse is also true: practicallyevery curve can be obtained by adding together inﬁnite numbers of sine waves ofdiﬀerent wavelengths (or frequencies) for each one of which we know the answer.We just have to know how much of each sine wave to put in to make the given F,and then our answer, x, is the corresponding sum of the F sine waves, eachmultiplied by its eﬀective ratio of x to F. This method of solution is calledthe method of Fourier transforms or Fourier analysis. We are not going toactually carry out such an analysis just now; we only wish to describe the ideainvolved.

Another way in which our complicated problem can be solved is the followingvery interesting one. Suppose that, by some tremendous mental eﬀort, it werepossible to solve our problem for a special force, namely an impulse. The force isquickly turned on and then oﬀ; it is all over. Actually we need only solve for animpulse of some unit strength, any other strength can be gotten by multiplicationby an appropriate factor. We know that the response x for an impulse is adamped oscillation. Now what can we say about some other force, for instance aforce like that of Fig. 25-4?

Such a force can be likened to a succession of blows with a hammer. First thereis no force, and all of a sudden there is a steady force—impulse, impulse, impulse,

* In modern superheterodyne receivers the actual operation is more complex. The ampliﬁersare all tuned to a ﬁxed frequency (called IF frequency) and an oscillator of variable tunablefrequency is combined with the input signal in a nonlinear circuit to produce a new frequency(the diﬀerence of signal and oscillator frequency) equal to the IF frequency, which is thenampliﬁed. This will be discussed in Chapter 50.

25-7

Fig. 25-4. A complicated force may be treated as a succession of

sharp impulses.

impulse, . . . and then it stops. In other words, we imagine the continuous forceto be a series of impulses, very close together. Now, we know the result for animpulse, so the result for a whole series of impulses will be a whole series ofdamped oscillations: it will be the curve for the ﬁrst impulse, and then (slightlylater) we add to that the curve for the second impulse, and the curve for thethird impulse, and so on. Thus we can represent, mathematically, the completesolution for arbitrary functions if we know the answer for an impulse. We getthe answer for any other force simply by integrating. This method is called theGreen’s function method. A Green’s function is a response to an impulse, andthe method of analyzing any force by putting together the response of impulsesis called the Green’s function method.

The physical principles involved in both of these schemes are so simple,involving just the linear equation, that they can be readily understood, but themathematical problems that are involved, the complicated integrations and so on,are a little too advanced for us to attack right now. You will most likely returnto this some day when you have had more practice in mathematics. But the ideais very simple indeed.

Finally, we make some remarks on why linear systems are so important. Theanswer is simple: because we can solve them! So most of the time we solve linearproblems. Second (and most important), it turns out that the fundamental lawsof physics are often linear. The Maxwell equations for the laws of electricity arelinear, for example. The great laws of quantum mechanics turn out, so far aswe know, to be linear equations. That is why we spend so much time on linearequations: because if we understand linear equations, we are ready, in principle,to understand a lot of things.

We mention another situation where linear equations are found. Whendisplacements are small, many functions can be approximated linearly. For

25-8

example, if we have a simple pendulum, the correct equation for its motion is

d2θ/dt2 = −(g/L) sin θ.

(25.9)

This equation can be solved by elliptic functions, but the easiest way to solve it isnumerically, as was shown in Chapter 9 on Newton’s Laws of Motion. A nonlinearequation cannot be solved, ordinarily, any other way but numerically. Now forsmall θ, sin θ is practically equal to θ, and we have a linear equation. It turnsout that there are many circumstances where small eﬀects are linear: for theexample here the swing of a pendulum through small arcs. As another example,if we pull a little bit on a spring, the force is proportional to the extension. If wepull hard, we break the spring, and the force is a completely diﬀerent function ofthe distance! Linear equations are important. In fact they are so important thatperhaps ﬁfty percent of the time we are solving linear equations in physics andin engineering.

25-3 Oscillations in linear systemsLet us now review the things we have been talking about in the past fewchapters. It is very easy for the physics of oscillators to become obscured bythe mathematics. The physics is actually very simple, and if we may forget themathematics for a moment we shall see that we can understand almost everythingthat happens in an oscillating system. First, if we have only the spring and theweight, it is easy to understand why the system oscillates—it is a consequenceof inertia. We pull the mass down and the force pulls it back up; as it passeszero, which is the place it likes to be, it cannot just suddenly stop; because of itsmomentum it keeps on going and swings to the other side, and back and forth.So, if there were no friction, we would surely expect an oscillatory motion, andindeed we get one. But if there is even a little bit of friction, then on the returncycle, the swing will not be quite as high as it was the ﬁrst time.

Now what happens, cycle by cycle? That depends on the kind and amountof friction. Suppose that we could concoct a kind of friction force that alwaysremains in the same proportion to the other forces, of inertia and in the spring,as the amplitude of oscillation varies. In other words, for smaller oscillationsthe friction should be weaker than for big oscillations. Ordinary friction doesnot have this property, so a special kind of friction must be carefully inventedfor the very purpose of creating a friction that is directly proportional to the

25-9

velocity—so that for big oscillations it is stronger and for small oscillations itis weaker. If we happen to have that kind of friction, then at the end of eachsuccessive cycle the system is in the same condition as it was at the start, excepta little bit smaller. All the forces are smaller in the same proportion: the springforce is reduced, the inertial eﬀects are lower because the accelerations are nowweaker, and the friction is less too, by our careful design. When we actuallyhave that kind of friction, we ﬁnd that each oscillation is exactly the same as theﬁrst one, except reduced in amplitude. If the ﬁrst cycle dropped the amplitude,say, to 90 percent of what it was at the start, the next will drop it to 90 percentof 90 percent, and so on: the sizes of the oscillations are reduced by the samefraction of themselves in every cycle. An exponential function is a curve whichdoes just that. It changes by the same factor in each equal interval of time. Thatis to say, if the amplitude of one cycle, relative to the preceding one, is called a,then the amplitude of the next is a2, and of the next, a3. So the amplitude issome constant raised to a power equal to the number of cycles traversed:

A = A0an.

(25.10)But of course n ∝ t, so it is perfectly clear that the general solution will be somekind of an oscillation, sine or cosine ωt, times an amplitude which goes as btmore or less. But b can be written as e−c, if b is positive and less than 1. So thisis why the solution looks like e−ct cos ω0t. It is very simple.What happens if the friction is not so artiﬁcial; for example, ordinary rubbingon a table, so that the friction force is a certain constant amount, and is indepen-dent of the size of the oscillation that reverses its direction each half-cycle? Thenthe equation is no longer linear, it becomes hard to solve, and must be solvedby the numerical method given in Chapter 9, or by considering each half-cycleseparately. The numerical method is the most powerful method of all, and cansolve any equation. It is only when we have a simple problem that we can usemathematical analysis.

Mathematical analysis is not the grand thing it is said to be; it solves onlythe simplest possible equations. As soon as the equations get a little morecomplicated, just a shade—they cannot be solved analytically. But the numericalmethod, which was advertised at the beginning of the course, can take care ofany equation of physical interest.

Next, what about the resonance curve? Why is there a resonance? First,imagine for a moment that there is no friction, and we have something which

25-10

could oscillate by itself. If we tapped the pendulum just right each time it wentby, of course we could make it go like mad. But if we close our eyes and donot watch it, and tap at arbitrary equal intervals, what is going to happen?Sometimes we will ﬁnd ourselves tapping when it is going the wrong way. Whenwe happen to have the timing just right, of course, each tap is given at just theright time, and so it goes higher and higher and higher. So without friction weget a curve which looks like the solid curve in Fig. 25-5 for diﬀerent frequencies.Qualitatively, we understand the resonance curve; in order to get the exact shapeof the curve it is probably just as well to do the mathematics. The curve goestoward inﬁnity as ω → ω0, where ω0 is the natural frequency of the oscillator.

Fig. 25-5. Resonance curves with various amounts of friction present.

Now suppose there is a little bit of friction; then when the displacement ofthe oscillator is small, the friction does not aﬀect it much; the resonance curveis the same, except when we are near resonance. Instead of becoming inﬁnitenear resonance, the curve is only going to get so high that the work done byour tapping each time is enough to compensate for the loss of energy by frictionduring the cycle. So the top of the curve is rounded oﬀ—it does not go to inﬁnity.If there is more friction, the top of the curve is rounded oﬀ still more. Nowsomeone might say,「I thought the widths of the curves depended on the friction.」That is because the curve is usually plotted so that the top of the curve is calledone unit. However, the mathematical expression is even simpler to understand ifwe just plot all the curves on the same scale; then all that happens is that thefriction cuts down the top! If there is less friction, we can go farther up into thatlittle pinnacle before the friction cuts it oﬀ, so it looks relatively narrow. That is,

25-11

the higher the peak of the curve, the narrower the width at half the maximumheight.

Finally, we take the case where there is an enormous amount of friction. Itturns out that if there is too much friction, the system does not oscillate at all.The energy in the spring is barely able to move it against the frictional force,and so it slowly oozes down to the equilibrium point.

25-4 Analogs in physicsThe next aspect of this review is to note that masses and springs are not theonly linear systems; there are others. In particular, there are electrical systemscalled linear circuits, in which we ﬁnd a complete analog to mechanical systems.We did not learn exactly why each of the objects in an electrical circuit works inthe way it does—that is not to be understood at the present moment; we mayassert it as an experimentally veriﬁable fact that they behave as stated.

For example, let us take the simplest possible circumstance. We have a pieceof wire, which is just a resistance, and we have applied to it a diﬀerence inpotential, V . Now the V means this: if we carry a charge q through the wirefrom one terminal to another terminal, the work done is qV . The higher thevoltage diﬀerence, the more work was done when the charge, as we say,「falls」from the high potential end of the terminal to the low potential end. So chargesrelease energy in going from one end to the other. Now the charges do not simplyﬂy from one end straight to the other end; the atoms in the wire oﬀer someresistance to the current, and this resistance obeys the following law for almostall ordinary substances: if there is a current I, that is, so and so many chargesper second tumbling down, the number per second that comes tumbling throughthe wire is proportional to how hard we push them—in other words, proportionalto how much voltage there is:

V = IR = R(dq/dt).

(25.11)The coeﬃcient R is called the resistance, and the equation is called Ohm’s Law.The unit of resistance is the ohm; it is equal to one volt per ampere. In mechanicalsituations, to get such a frictional force in proportion to the velocity is diﬃcult;in an electrical system it is very easy, and this law is extremely accurate for mostmetals.

We are often interested in how much work is done per second, the power loss,or the energy liberated by the charges as they tumble down the wire. When

25-12

we carry a charge q through a voltage V , the work is qV , so the work done persecond would be V (dq/dt), which is the same as V I, or also IR · I = I2R. Thisis called the heating loss—this is how much heat is generated in the resistanceper second, by the conservation of energy. It is this heat that makes an ordinaryincandescent light bulb work.

Of course, there are other interesting properties of mechanical systems, suchas the mass (inertia), and it turns out that there is an electrical analog to inertiaalso. It is possible to make something called an inductor, having a propertycalled inductance, such that a current, once started through the inductance, doesnot want to stop. It requires a voltage in order to change the current! If thecurrent is constant, there is no voltage across an inductance. dc circuits do notknow anything about inductance; it is only when we change the current that theeﬀects of inductance show up. The equation is

V = L(dI/dt) = L(d2q/dt2),

(25.12)and the unit of inductance, called the henry, is such that one volt applied toan inductance of one henry produces a change of one ampere per second in thecurrent. Equation (25.12) is the analog of Newton’s law for electricity, if we wish:V corresponds to F, L corresponds to m, and I corresponds to velocity! All of theconsequent equations for the two kinds of systems will have the same derivationsbecause, in all the equations, we can change any letter to its correspondinganalog letter and we get the same equation; everything we deduce will have acorrespondence in the two systems.

Now what electrical thing corresponds to the mechanical spring, in whichthere was a force proportional to the stretch? If we start with F = kx and replaceF → V and x → q, we get V = αq. It turns out that there is such a thing, in factit is the only one of the three circuit elements we can really understand, becausewe did study a pair of parallel plates, and we found that if there were a charge ofcertain equal, opposite amounts on each plate, the electric ﬁeld between themwould be proportional to the size of the charge. So the work done in moving aunit charge across the gap from one plate to the other is precisely proportional tothe charge. This work is the deﬁnition of the voltage diﬀerence, and it is the lineintegral of the electric ﬁeld from one plate to another. It turns out, for historicalreasons, that the constant of proportionality is not called C, but 1/C. It couldhave been called C, but it was not. So we have

V = q/C.

25-13

(25.13)

The unit of capacitance, C, is the farad; a charge of one coulomb on each plateof a one-farad capacitor yields a voltage diﬀerence of one volt.There are our analogies, and the equation corresponding to the oscillating

circuit becomes the following, by direct substitution of L for m, q for x, etc:

m(d2x/dt2) + γm(dx/dt) + kx = F,L(d2q/dt2) + R(dq/dt) + q/C = V.

(25.14)(25.15)Now everything we learned about (25.14) can be transformed to apply to (25.15).Every consequence is the same; so much the same that there is a brilliant thingwe can do.Suppose we have a mechanical system which is quite complicated, not justone mass on a spring, but several masses on several springs, all hooked together.What do we do? Solve it? Perhaps; but look, we can make an electrical circuitwhich will have the same equations as the thing we are trying to analyze! Forinstance, if we wanted to analyze a mass on a spring, why can we not buildan electrical circuit in which we use an inductance proportional to the mass, aresistance proportional to the corresponding mγ, 1/C proportional to k, all inthe same ratio? Then, of course, this electrical circuit will be the exact analogof our mechanical one, in the sense that whatever q does, in response to V(V also is made to correspond to the forces that are acting), so the x woulddo in response to the force! So if we have a complicated thing with a wholelot of interconnecting elements, we can interconnect a whole lot of resistances,inductances, and capacitances, to imitate the mechanically complicated system.What is the advantage to that? One problem is just as hard (or as easy) asthe other, because they are exactly equivalent. The advantage is not that it isany easier to solve the mathematical equations after we discover that we have anelectrical circuit (although that is the method used by electrical engineers!), butinstead, the real reason for looking at the analog is that it is easier to make theelectrical circuit, and to change something in the system.Suppose we have designed an automobile, and want to know how much itis going to shake when it goes over a certain kind of bumpy road. We build anelectrical circuit with inductances to represent the inertia of the wheels, springconstants as capacitances to represent the springs of the wheels, and resistors torepresent the shock absorbers, and so on for the other parts of the automobile.Then we need a bumpy road. All right, we apply a voltage from a generator,which represents such and such a kind of bump, and then look at how the left

25-14

wheel jiggles by measuring the charge on some capacitor. Having measured it(it is easy to do), we ﬁnd that it is bumping too much. Do we need more shockabsorber, or less shock absorber? With a complicated thing like an automobile,do we actually change the shock absorber, and solve it all over again? No!, wesimply turn a dial; dial number ten is shock absorber number three, so we put inmore shock absorber. The bumps are worse—all right, we try less. The bumpsare still worse; we change the stiﬀness of the spring (dial 17), and we adjust allthese things electrically, with merely the turn of a knob.This is called an analog computer. It is a device which imitates the problemthat we want to solve by making another problem, which has the same equation,but in another circumstance of nature, and which is easier to build, to measure,to adjust, and to destroy!

25-5 Series and parallel impedancesFinally, there is an important item which is not quite in the nature of review.This has to do with an electrical circuit in which there is more than one circuitelement. For example, when we have an inductor, a resistor, and a capacitorconnected as in Fig. 24-2, we note that all the charge went through every oneof the three, so that the current in such a singly connected thing is the same atall points along the wire. Since the current is the same in each one, the voltageacross R is IR, the voltage across L is L(dI/dt), and so on. So, the total voltagedrop is the sum of these, and this leads to Eq. (25.15). Using complex numbers,we found that we could solve the equation for the steady-state motion in responseto a sinusoidal force. We thus found that ˆV = ˆZ ˆI. Now ˆZ is called the impedanceof this particular circuit. It tells us that if we apply a sinusoidal voltage, ˆV , weget a current ˆI.Now suppose we have a more complicated circuit which has two pieces,which by themselves have certain impedances, ˆZ1 and ˆZ2 and we put them in

Fig. 25-6. Two impedances, connected in series and in parallel.

25-15

series (Fig. 25-6a) and apply a voltage. What happens? It is now a little morecomplicated, but if ˆI is the current through ˆZ1, the voltage diﬀerence across ˆZ1,is ˆV1 = ˆI ˆZ1; similarly, the voltage across ˆZ2 is ˆV2 = ˆI ˆZ2. The same current goesthrough both. Therefore the total voltage is the sum of the voltages across thetwo sections and is equal to ˆV = ˆV1 + ˆV2 = ( ˆZ1 + ˆZ2)ˆI. This means that thevoltage on the complete circuit can be written ˆV = ˆI ˆZs, where the ˆZs of thecombined system in series is the sum of the two ˆZ’s of the separate pieces:

ˆZs = ˆZ1 + ˆZ2.

(25.16)This is not the only way things may be connected. We may also connectthem in another way, called a parallel connection (Fig. 25-6b). Now we see that agiven voltage across the terminals, if the connecting wires are perfect conductors,is eﬀectively applied to both of the impedances, and will cause currents in eachindependently. Therefore the current through ˆZ1 is equal to ˆI1 = ˆV / ˆZ1. Thecurrent in ˆZ2 is ˆI2 = ˆV / ˆZ2.It is the same voltage. Now the total currentwhich is supplied to the terminals is the sum of the currents in the two sections:ˆI = ˆV / ˆZ1 + ˆV / ˆZ2. This can be written as

ˆV =

ˆI

(1/ ˆZ1) + (1/ ˆZ2)1/ ˆZp = 1/ ˆZ1 + 1/ ˆZ2.

= ˆI ˆZp.

Thus

(25.17)More complicated circuits can sometimes be simpliﬁed by taking pieces ofthem, working out the succession of impedances of the pieces, and combiningthe circuit together step by step, using the above rules. If we have any kind ofcircuit with many impedances connected in all kinds of ways, and if we includethe voltages in the form of little generators having no impedance (when we passcharge through it, the generator adds a voltage V ), then the following principlesapply: (1) At any junction, the sum of the currents into a junction is zero.That is, all the current which comes in must come back out. (2) If we carry acharge around any loop, and back to where it started, the net work done is zero.These rules are called Kirchhoﬀ’s laws for electrical circuits. Their systematicapplication to complicated circuits often simpliﬁes the analysis of such circuits.We mention them here in conjunction with Eqs. (25.16) and (25.17), in case youhave already come across such circuits that you need to analyze in laboratorywork. They will be discussed again in more detail next year.

25-16

26

