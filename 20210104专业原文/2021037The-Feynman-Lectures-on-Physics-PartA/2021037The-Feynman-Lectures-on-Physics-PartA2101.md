The Harmonic Oscillator

21-1 Linear diﬀerential equationsIn the study of physics, usually the course is divided into a series of subjects,such as mechanics, electricity, optics, etc., and one studies one subject after theother. For example, this course has so far dealt mostly with mechanics. But astrange thing occurs again and again: the equations which appear in diﬀerentﬁelds of physics, and even in other sciences, are often almost exactly the same,so that many phenomena have analogs in these diﬀerent ﬁelds. To take thesimplest example, the propagation of sound waves is in many ways analogous tothe propagation of light waves. If we study acoustics in great detail we discoverthat much of the work is the same as it would be if we were studying optics ingreat detail. So the study of a phenomenon in one ﬁeld may permit an extensionof our knowledge in another ﬁeld. It is best to realize from the ﬁrst that suchextensions are possible, for otherwise one might not understand the reason forspending a great deal of time and energy on what appears to be only a smallpart of mechanics.

The harmonic oscillator, which we are about to study, has close analogs inmany other ﬁelds; although we start with a mechanical example of a weight on aspring, or a pendulum with a small swing, or certain other mechanical devices, weare really studying a certain diﬀerential equation. This equation appears againand again in physics and in other sciences, and in fact it is a part of so manyphenomena that its close study is well worth our while. Some of the phenomenainvolving this equation are the oscillations of a mass on a spring; the oscillationsof charge ﬂowing back and forth in an electrical circuit; the vibrations of a tuningfork which is generating sound waves; the analogous vibrations of the electronsin an atom, which generate light waves; the equations for the operation of aservosystem, such as a thermostat trying to adjust a temperature; complicatedinteractions in chemical reactions; the growth of a colony of bacteria in interaction

21-1

with the food supply and the poisons the bacteria produce; foxes eating rabbitseating grass, and so on; all these phenomena follow equations which are verysimilar to one another, and this is the reason why we study the mechanicaloscillator in such detail. The equations are called linear diﬀerential equationswith constant coeﬃcients. A linear diﬀerential equation with constant coeﬃcientsis a diﬀerential equation consisting of a sum of several terms, each term being aderivative of the dependent variable with respect to the independent variable,and multiplied by some constant. Thus

an dnx/dtn + an−1 dn−1x/dtn−1 + ··· + a1 dx/dt + a0x = f(t)

(21.1)

is called a linear diﬀerential equation of order n with constant coeﬃcients (eachai is constant).

21-2 The harmonic oscillatorPerhaps the simplest mechanical system whose motion follows a linear diﬀer-ential equation with constant coeﬃcients is a mass on a spring: ﬁrst the springstretches to balance the gravity; once it is balanced, we then discuss the verticaldisplacement of the mass from its equilibrium position (Fig. 21-1). We shallcall this upward displacement x, and we shall also suppose that the spring isperfectly linear, in which case the force pulling back when the spring is stretchedis precisely proportional to the amount of stretch. That is, the force is −kx(with a minus sign to remind us that it pulls back). Thus the mass times theacceleration must equal −kx:

m d2x/dt2 = −kx.

(21.2)

Fig. 21-1. A mass on a spring: a simple example of a harmonic

oscillator.

21-2

For simplicity, suppose it happens (or we change our unit of time measurement)that the ratio k/m = 1. We shall ﬁrst study the equation

d2x/dt2 = −x.

(21.3)

Later we shall come back to Eq. (21.2) with the k and m explicitly present.

We have already analyzed Eq. (21.3) in detail numerically; when we ﬁrstintroduced the subject of mechanics we solved this equation (see Eq. 9.12) toﬁnd the motion. By numerical integration we found a curve (Fig. 9-4) whichshowed that if m was initially displaced, but at rest, it would come down and gothrough zero; we did not then follow it any farther, but of course we know thatit just keeps going up and down—it oscillates. When we calculated the motionnumerically, we found that it went through the equilibrium point at t = 1.570.The length of the whole cycle is four times this long, or t0 = 6.28「sec.」Thiswas found numerically, before we knew much calculus. We assume that in themeantime the Mathematics Department has brought forth a function which,when diﬀerentiated twice, is equal to itself with a minus sign. (There are, ofcourse, ways of getting at this function in a direct fashion, but they are morecomplicated than already knowing what the answer is.) The function is x = cos t.If we diﬀerentiate this we ﬁnd dx/dt = − sin t and d2x/dt2 = − cos t = −x. Thefunction x = cos t starts, at t = 0, with x = 1, and no initial velocity; that wasthe situation with which we started when we did our numerical work. Now thatwe know that x = cos t, we can calculate a precise value for the time at which itshould pass x = 0. The answer is t = π/2, or 1.57080. We were wrong in the lastﬁgure because of the errors of numerical analysis, but it was very close!

Now to go further with the original problem, we restore the time units to realseconds. What is the solution then? First of all, we might think that we can get theconstants k and m in by multiplying cos t by something. So let us try the equationx = A cos t; then we ﬁnd dx/dt = −A sin t, and d2x/dt2 = −A cos t = −x. Thuswe discover to our horror that we did not succeed in solving Eq. (21.2), but wegot Eq. (21.3) again! That fact illustrates one of the most important propertiesof linear diﬀerential equations: if we multiply a solution of the equation by anyconstant, it is again a solution. The mathematical reason for this is clear. If x isa solution, and we multiply both sides of the equation, say by A, we see that allderivatives are also multiplied by A, and therefore Ax is just as good a solutionof the original equation as x was. The physics of it is the following. If we have aweight on a spring, and pull it down twice as far, the force is twice as much, the

21-3

resulting acceleration is twice as great, the velocity it acquires in a given time istwice as great, the distance covered in a given time is twice as great; but it hasto cover twice as great a distance in order to get back to the origin because it ispulled down twice as far. So it takes the same time to get back to the origin,irrespective of the initial displacement. In other words, with a linear equation,the motion has the same time pattern, no matter how「strong」it is.That was the wrong thing to do—it only taught us that we can multiplythe solution by anything, and it satisﬁes the same equation, but not a diﬀerentequation. After a little cut and try to get to an equation with a diﬀerent constantmultiplying x, we ﬁnd that we must alter the scale of time. In other words,Eq. (21.2) has a solution of the form

x = cos ω0t.

(21.4)(It is important to realize that in the present case, ω0 is not an angular velocityof a spinning body, but we run out of letters if we are not allowed to use the sameletter for more than one thing.) The reason we put a subscript「0」on ω is that weare going to have more omegas before long; let us remember that ω0 refers to thenatural motion of this oscillator. Now we try Eq. (21.4) and this time we are moresuccessful, because dx/dt = −ω0 sin ω0t and d2x/dt2 = −ω20x. Soat last we have solved the equation that we really wanted to solve. The equationd2x/dt2 = −ω2The next thing we must investigate is the physical signiﬁcance of ω0. Weknow that the cosine function repeats itself when the angle it refers to is 2π. Sox = cos ω0t will repeat its motion, it will go through a complete cycle, when the「angle」changes by 2π. The quantity ω0t is often called the phase of the motion.In order to change ω0t by 2π, the time must change by an amount t0, calledthe period of one complete oscillation; of course t0 must be such that ω0t0 = 2π.That is, ω0t0 must account for one cycle of the angle, and then everything willrepeat itself—if we increase t by t0, we add 2π to the phase. Thus

0x is the same as Eq. (21.2) if ω2

0 cos ω0t = −ω2

0 = k/m.

t0 = 2π/ω0 = 2πpm/k.

(21.5)Thus if we had a heavier mass, it would take longer to oscillate back and forthon a spring. That is because it has more inertia, and so, while the forces are thesame, it takes longer to get the mass moving. Or, if the spring is stronger, it willmove more quickly, and that is right: the period is less if the spring is stronger.Note that the period of oscillation of a mass on a spring does not dependin any way on how it has been started, how far down we pull it. The period

21-4

is determined, but the amplitude of the oscillation is not determined by theequation of motion (21.2). The amplitude is determined, in fact, by how we letgo of it, by what we call the initial conditions or starting conditions.Actually, we have not quite found the most general possible solution ofEq. (21.2). There are other solutions. It should be clear why: because all of thecases covered by x = a cos ω0t start with an initial displacement and no initialvelocity. But it is possible, for instance, for the mass to start at x = 0, and wemay then give it an impulsive kick, so that it has some speed at t = 0. Sucha motion is not represented by a cosine—it is represented by a sine. To put itanother way, if x = cos ω0t is a solution, then is it not obvious that if we wereto happen to walk into the room at some time (which we would call「t = 0」)and saw the mass as it was passing x = 0, it would keep on going just the same?Therefore, x = cos ω0t cannot be the most general solution; it must be possibleto shift the beginning of time, so to speak. As an example, we could write thesolution this way: x = a cos ω0(t − t1), where t1 is some constant. This alsocorresponds to shifting the origin of time to some new instant. Furthermore, wemay expand

cos (ω0t + ∆) = cos ω0t cos ∆ − sin ω0t sin ∆,

and write

x = A cos ω0t + B sin ω0t,

where A = a cos ∆ and B = −a sin ∆. Any one of these forms is a possible wayto write the complete, general solution of (21.2): that is, every solution of thediﬀerential equation d2x/dt2 = −ω20x that exists in the world can be written as

or

or

(a)

(b)

(c)

x = a cos ω0(t − t1),

x = a cos (ω0t + ∆),

x = A cos ω0t + B sin ω0t.

(21.6)

Some of the quantities in (21.6) have names: ω0 is called the angular frequency;it is the number of radians by which the phase changes in a second. That isdetermined by the diﬀerential equation. The other constants are not determinedby the equation, but by how the motion is started. Of these constants, a measuresthe maximum displacement attained by the mass, and is called the amplitude

21-5

of oscillation. The constant ∆ is sometimes called the phase of the oscillation,but that is a confusion, because other people call ω0t + ∆ the phase, and saythe phase changes with time. We might say that ∆ is a phase shift from somedeﬁned zero. Let us put it diﬀerently. Diﬀerent ∆’s correspond to motions indiﬀerent phases. That is true, but whether we want to call ∆ the phase, or not,is another question.

21-3 Harmonic motion and circular motionThe fact that cosines are involved in the solution of Eq. (21.2) suggests thatthere might be some relationship to circles. This is artiﬁcial, of course, becausethere is no circle actually involved in the linear motion—it just goes up and down.We may point out that we have, in fact, already solved that diﬀerential equationwhen we were studying the mechanics of circular motion. If a particle moves ina circle with a constant speed v, the radius vector from the center of the circleto the particle turns through an angle whose size is proportional to the time. Ifwe call this angle θ = vt/R (Fig. 21-2) then dθ/dt = ω0 = v/R. We know thatthere is an acceleration a = v2/R = ω20R toward the center. Now we also knowthat the position x, at a given moment, is the radius of the circle times cos θ,and that y is the radius times sin θ:x = R cos θ,

y = R sin θ.

Now what about the acceleration? What is the x-component of acceleration,d2x/dt2? We have already worked that out geometrically; it is the magnitudeof the acceleration times the cosine of the projection angle, with a minus signbecause it is toward the center.

ax = −a cos θ = −ω2

0R cos θ = −ω20x.

(21.7)

Fig. 21-2. A particle moving in a circular path at constant speed.

21-6

In other words, when a particle is moving in a circle, the horizontal component ofits motion has an acceleration which is proportional to the horizontal displacementfrom the center. Of course we also have the solution for motion in a circle:x = R cos ω0t. Equation (21.7) does not depend upon the radius of the circle, sofor a circle of any radius, one ﬁnds the same equation for a given ω0. Thus, forseveral reasons, we expect that the displacement of a mass on a spring will turnout to be proportional to cos ω0t, and will, in fact, be exactly the same motionas we would see if we looked at the x-component of the position of an objectrotating in a circle with angular velocity ω0. As a check on this, one can devisean experiment to show that the up-and-down motion of a mass on a spring is thesame as that of a point going around in a circle. In Fig. 21-3 an arc light projectedon a screen casts shadows of a crank pin on a shaft and of a vertically oscillatingmass, side by side. If we let go of the mass at the right time from the right place,and if the shaft speed is carefully adjusted so that the frequencies match, eachshould follow the other exactly. One can also check the numerical solution weobtained earlier with the cosine function, and see whether that agrees very well.

Fig. 21-3. Demonstration of the equivalence between simple harmonic

motion and uniform circular motion.

Here we may point out that because uniform motion in a circle is so closelyrelated mathematically to oscillatory up-and-down motion, we can analyze oscil-latory motion in a simpler way if we imagine it to be a projection of somethinggoing in a circle. In other words, although the distance y means nothing in theoscillator problem, we may still artiﬁcially supplement Eq. (21.2) with another

21-7

equation using y, and put the two together. If we do this, we will be able toanalyze our one-dimensional oscillator with circular motions, which is a lot easierthan having to solve a diﬀerential equation. The trick in doing this is to usecomplex numbers, a procedure we shall introduce in the next chapter.

21-4 Initial conditionsNow let us consider what determines the constants A and B, or a and ∆. Ofcourse these are determined by how we start the motion. If we start the motionwith just a small displacement, that is one type of oscillation; if we start withan initial displacement and then push up when we let go, we get still a diﬀerentmotion. The constants A and B, or a and ∆, or any other way of putting it, aredetermined, of course, by the way the motion started, not by any other featuresof the situation. These are called the initial conditions. We would like to connectthe initial conditions with the constants. Although this can be done using anyone of the forms (21.6), it turns out to be easiest if we use Eq. (21.6c). Supposethat at t = 0 we have started with an initial displacement x0 and a certainvelocity v0. This is the most general way we can start the motion. (We cannotspecify the acceleration with which it started, true, because that is determinedby the spring, once we specify x0.) Now let us calculate A and B. We start withthe equation for x,

x = A cos ω0t + B sin ω0t.

Since we shall later need the velocity also, we diﬀerentiate x and obtain

v = −ω0A sin ω0t + ω0B cos ω0t.

These expressions are valid for all t, but we have special knowledge about x and vat t = 0. So if we put t = 0 into these equations, on the left we get x0 and v0,because that is what x and v are at t = 0; also, we know that the cosine of zerois unity, and the sine of zero is zero. Therefore we get

and

x0 = A · 1 + B · 0 = A

v0 = −ω0A · 0 + ω0B · 1 = ω0B.

So for this particular case we ﬁnd that

From these values of A and B, we can get a and ∆ if we wish.

A = x0,

B = v0/ω0.

21-8

That is the end of our solution, but there is one physically interesting thingto check, and that is the conservation of energy. Since there are no frictionallosses, energy ought to be conserved. Let us use the formula

then

x = a cos (ω0t + ∆);v = −ω0a sin (ω0t + ∆).

Now let us ﬁnd out what the kinetic energy T is, and what the potential energy Uis. The potential energy at any moment is 12 kx2, where x is the displacementand k is the constant of the spring. If we substitute for x, using our expressionabove, we get

U = 1

2 kx2 = 1

2 ka2 cos2 (ω0t + ∆).

Of course the potential energy is not constant; the potential never becomesnegative, naturally—there is always some energy in the spring, but the amountof energy ﬂuctuates with x. The kinetic energy, on the other hand, is 12 mv2, andby substituting for v we getT = 1

0a2 sin2 (ω0t + ∆).

2 mv2 = 1

2 mω2

Now the kinetic energy is zero when x is at the maximum, because then thereis no velocity; on the other hand, it is maximal when x is passing through zero,because then it is moving fastest. This variation of the kinetic energy is justthe opposite of that of the potential energy. But the total energy ought to be aconstant. If we note that k = mω2

0, we see that

T + U = 1

2 mω2

0a2[cos2 (ω0t + ∆) + sin2 (ω0t + ∆)] = 1

2 mω2

0a2.

The energy is dependent on the square of the amplitude; if we have twice theamplitude, we get an oscillation which has four times the energy. The averagepotential energy is half the maximum and, therefore, half the total, and theaverage kinetic energy is likewise half the total energy.

21-5 Forced oscillationsNext we shall discuss the forced harmonic oscillator, i.e., one in which there

is an external driving force acting. The equation then is the following:

m d2x/dt2 = −kx + F(t).

(21.8)

21-9

We would like to ﬁnd out what happens in these circumstances. The externaldriving force can have various kinds of functional dependence on the time; theﬁrst one that we shall analyze is very simple—we shall suppose that the force isoscillating:

F(t) = F0 cos ωt.

(21.9)Notice, however, that this ω is not necessarily ω0: we have ω under our control;the forcing may be done at diﬀerent frequencies. So we try to solve Eq. (21.8)with the special force (21.9). What is the solution of (21.8)? One special solution,(we shall discuss the more general cases later) is

x = C cos ωt,

(21.10)where the constant is to be determined. In other words, we might suppose thatif we kept pushing back and forth, the mass would follow back and forth in stepwith the force. We can try it anyway. So we put (21.10) and (21.9) into (21.8),and get

− mω2C cos ωt = −mω2

(21.11)We have also put in k = mω20, so that we will understand the equation better atthe end. Now because the cosine appears everywhere, we can divide it out, andthat shows that (21.10) is, in fact, a solution, provided we pick C just right. Theanswer is that C must be

0C cos ωt + F0 cos ωt.

0 − ω2).

C = F0/m(ω2

(21.12)That is, m oscillates at the same frequency as the force, but with an amplitudewhich depends on the frequency of the force, and also upon the frequency of thenatural motion of the oscillator. It means, ﬁrst, that if ω is very small comparedwith ω0, then the displacement and the force are in the same direction. On theother hand, if we shake it back and forth very fast, then (21.12) tells us that C isnegative if ω is above the natural frequency ω0 of the harmonic oscillator. (Wewill call ω0 the natural frequency of the harmonic oscillator, and ω the appliedfrequency.) At very high frequency the denominator may become very large, andthere is then not much amplitude.

Of course the solution we have found is the solution only if things are startedjust right, for otherwise there is a part which usually dies out after a while. Thisother part is called the transient response to F(t), while (21.10) and (21.12) arecalled the steady-state response.

21-10

According to our formula (21.12), a very remarkable thing should also occur:if ω is almost exactly the same as ω0, then C should approach inﬁnity. So if weadjust the frequency of the force to be「in time」with the natural frequency, thenwe should get an enormous displacement. This is well known to anybody whohas pushed a child on a swing. It does not work very well to close our eyes andpush at a certain speed at random. If we happen to get the right timing, thenthe swing goes very high, but if we have the wrong timing, then sometimes wemay be pushing when we should be pulling, and so on, and it does not work.

If we make ω exactly equal to ω0, we ﬁnd that it should oscillate at aninﬁnite amplitude, which is, of course, impossible. The reason it does not is thatsomething goes wrong with the equation, there are some other frictional terms,and other forces, which are not in (21.8) but which occur in the real world. Sothe amplitude does not reach inﬁnity for some reason; it may be that the springbreaks!

21-11

22

