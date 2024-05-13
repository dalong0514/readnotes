The Harmonic Oscillator

21-1 Linear diﬀerential equations In the study of physics, usually the course is divided into a series of subjects, such as mechanics, electricity, optics, etc., and one studies one subject after the other. For example, this course has so far dealt mostly with mechanics. But a strange thing occurs again and again: the equations which appear in diﬀerent ﬁelds of physics, and even in other sciences, are often almost exactly the same, so that many phenomena have analogs in these diﬀerent ﬁelds. To take the simplest example, the propagation of sound waves is in many ways analogous to the propagation of light waves. If we study acoustics in great detail we discover that much of the work is the same as it would be if we were studying optics in great detail. So the study of a phenomenon in one ﬁeld may permit an extension of our knowledge in another ﬁeld. It is best to realize from the ﬁrst that such extensions are possible, for otherwise one might not understand the reason for spending a great deal of time and energy on what appears to be only a small part of mechanics.

The harmonic oscillator, which we are about to study, has close analogs in many other ﬁelds; although we start with a mechanical example of a weight on a spring, or a pendulum with a small swing, or certain other mechanical devices, we are really studying a certain diﬀerential equation. This equation appears again and again in physics and in other sciences, and in fact it is a part of so many phenomena that its close study is well worth our while. Some of the phenomena involving this equation are the oscillations of a mass on a spring; the oscillations of charge ﬂowing back and forth in an electrical circuit; the vibrations of a tuning fork which is generating sound waves; the analogous vibrations of the electrons in an atom, which generate light waves; the equations for the operation of a servosystem, such as a thermostat trying to adjust a temperature; complicated interactions in chemical reactions; the growth of a colony of bacteria in interaction

21-1

with the food supply and the poisons the bacteria produce; foxes eating rabbits eating grass, and so on; all these phenomena follow equations which are very similar to one another, and this is the reason why we study the mechanical oscillator in such detail. The equations are called linear diﬀerential equations with constant coeﬃcients. A linear diﬀerential equation with constant coeﬃcients is a diﬀerential equation consisting of a sum of several terms, each term being a derivative of the dependent variable with respect to the independent variable, and multiplied by some constant. Thus

an dnx/dtn + an−1 dn−1x/dtn−1 + ··· + a1 dx/dt + a0x = f(t)

(21.1)

is called a linear diﬀerential equation of order n with constant coeﬃcients (each ai is constant).

21-2 The harmonic oscillator Perhaps the simplest mechanical system whose motion follows a linear diﬀer- ential equation with constant coeﬃcients is a mass on a spring: ﬁrst the spring stretches to balance the gravity; once it is balanced, we then discuss the vertical displacement of the mass from its equilibrium position (Fig. 21-1). We shall call this upward displacement x, and we shall also suppose that the spring is perfectly linear, in which case the force pulling back when the spring is stretched is precisely proportional to the amount of stretch. That is, the force is −kx (with a minus sign to remind us that it pulls back). Thus the mass times the acceleration must equal −kx:

m d2x/dt2 = −kx.

(21.2)

Fig. 21-1. A mass on a spring: a simple example of a harmonic

oscillator.

21-2

For simplicity, suppose it happens (or we change our unit of time measurement) that the ratio k/m = 1. We shall ﬁrst study the equation

d2x/dt2 = −x.

(21.3)

Later we shall come back to Eq. (21.2) with the k and m explicitly present.

We have already analyzed Eq. (21.3) in detail numerically; when we ﬁrst introduced the subject of mechanics we solved this equation (see Eq. 9.12) to ﬁnd the motion. By numerical integration we found a curve (Fig. 9-4) which showed that if m was initially displaced, but at rest, it would come down and go through zero; we did not then follow it any farther, but of course we know that it just keeps going up and down—it oscillates. When we calculated the motion numerically, we found that it went through the equilibrium point at t = 1.570. The length of the whole cycle is four times this long, or t0 = 6.28「sec.」This was found numerically, before we knew much calculus. We assume that in the meantime the Mathematics Department has brought forth a function which, when diﬀerentiated twice, is equal to itself with a minus sign. (There are, of course, ways of getting at this function in a direct fashion, but they are more complicated than already knowing what the answer is.) The function is x = cos t. If we diﬀerentiate this we ﬁnd dx/dt = − sin t and d2x/dt2 = − cos t = −x. The function x = cos t starts, at t = 0, with x = 1, and no initial velocity; that was the situation with which we started when we did our numerical work. Now that we know that x = cos t, we can calculate a precise value for the time at which it should pass x = 0. The answer is t = π/2, or 1.57080. We were wrong in the last ﬁgure because of the errors of numerical analysis, but it was very close!

Now to go further with the original problem, we restore the time units to real seconds. What is the solution then? First of all, we might think that we can get the constants k and m in by multiplying cos t by something. So let us try the equation x = A cos t; then we ﬁnd dx/dt = −A sin t, and d2x/dt2 = −A cos t = −x. Thus we discover to our horror that we did not succeed in solving Eq. (21.2), but we got Eq. (21.3) again! That fact illustrates one of the most important properties of linear diﬀerential equations: if we multiply a solution of the equation by any constant, it is again a solution. The mathematical reason for this is clear. If x is a solution, and we multiply both sides of the equation, say by A, we see that all derivatives are also multiplied by A, and therefore Ax is just as good a solution of the original equation as x was. The physics of it is the following. If we have a weight on a spring, and pull it down twice as far, the force is twice as much, the

21-3

resulting acceleration is twice as great, the velocity it acquires in a given time is twice as great, the distance covered in a given time is twice as great; but it has to cover twice as great a distance in order to get back to the origin because it is pulled down twice as far. So it takes the same time to get back to the origin, irrespective of the initial displacement. In other words, with a linear equation, the motion has the same time pattern, no matter how「strong」it is. That was the wrong thing to do—it only taught us that we can multiply the solution by anything, and it satisﬁes the same equation, but not a diﬀerent equation. After a little cut and try to get to an equation with a diﬀerent constant multiplying x, we ﬁnd that we must alter the scale of time. In other words, Eq. (21.2) has a solution of the form

x = cos ω0t.

(21.4) (It is important to realize that in the present case, ω0 is not an angular velocity of a spinning body, but we run out of letters if we are not allowed to use the same letter for more than one thing.) The reason we put a subscript「0」on ω is that we are going to have more omegas before long; let us remember that ω0 refers to the natural motion of this oscillator. Now we try Eq. (21.4) and this time we are more successful, because dx/dt = −ω0 sin ω0t and d2x/dt2 = −ω2 0x. So at last we have solved the equation that we really wanted to solve. The equation d2x/dt2 = −ω2 The next thing we must investigate is the physical signiﬁcance of ω0. We know that the cosine function repeats itself when the angle it refers to is 2π. So x = cos ω0t will repeat its motion, it will go through a complete cycle, when the「angle」changes by 2π. The quantity ω0t is often called the phase of the motion. In order to change ω0t by 2π, the time must change by an amount t0, called the period of one complete oscillation; of course t0 must be such that ω0t0 = 2π. That is, ω0t0 must account for one cycle of the angle, and then everything will repeat itself—if we increase t by t0, we add 2π to the phase. Thus

0x is the same as Eq. (21.2) if ω2

0 cos ω0t = −ω2

0 = k/m.

t0 = 2π/ω0 = 2πpm/k.

(21.5) Thus if we had a heavier mass, it would take longer to oscillate back and forth on a spring. That is because it has more inertia, and so, while the forces are the same, it takes longer to get the mass moving. Or, if the spring is stronger, it will move more quickly, and that is right: the period is less if the spring is stronger. Note that the period of oscillation of a mass on a spring does not depend in any way on how it has been started, how far down we pull it. The period

21-4

is determined, but the amplitude of the oscillation is not determined by the equation of motion (21.2). The amplitude is determined, in fact, by how we let go of it, by what we call the initial conditions or starting conditions. Actually, we have not quite found the most general possible solution of Eq. (21.2). There are other solutions. It should be clear why: because all of the cases covered by x = a cos ω0t start with an initial displacement and no initial velocity. But it is possible, for instance, for the mass to start at x = 0, and we may then give it an impulsive kick, so that it has some speed at t = 0. Such a motion is not represented by a cosine—it is represented by a sine. To put it another way, if x = cos ω0t is a solution, then is it not obvious that if we were to happen to walk into the room at some time (which we would call「t = 0」) and saw the mass as it was passing x = 0, it would keep on going just the same? Therefore, x = cos ω0t cannot be the most general solution; it must be possible to shift the beginning of time, so to speak. As an example, we could write the solution this way: x = a cos ω0(t − t1), where t1 is some constant. This also corresponds to shifting the origin of time to some new instant. Furthermore, we may expand

cos (ω0t + ∆) = cos ω0t cos ∆ − sin ω0t sin ∆,

and write

x = A cos ω0t + B sin ω0t,

where A = a cos ∆ and B = −a sin ∆. Any one of these forms is a possible way to write the complete, general solution of (21.2): that is, every solution of the diﬀerential equation d2x/dt2 = −ω2 0x that exists in the world can be written as

or

or

(a)

(b)

(c)

x = a cos ω0(t − t1),

x = a cos (ω0t + ∆),

x = A cos ω0t + B sin ω0t.

(21.6)

Some of the quantities in (21.6) have names: ω0 is called the angular frequency; it is the number of radians by which the phase changes in a second. That is determined by the diﬀerential equation. The other constants are not determined by the equation, but by how the motion is started. Of these constants, a measures the maximum displacement attained by the mass, and is called the amplitude

21-5

of oscillation. The constant ∆ is sometimes called the phase of the oscillation, but that is a confusion, because other people call ω0t + ∆ the phase, and say the phase changes with time. We might say that ∆ is a phase shift from some deﬁned zero. Let us put it diﬀerently. Diﬀerent ∆’s correspond to motions in diﬀerent phases. That is true, but whether we want to call ∆ the phase, or not, is another question.

21-3 Harmonic motion and circular motion The fact that cosines are involved in the solution of Eq. (21.2) suggests that there might be some relationship to circles. This is artiﬁcial, of course, because there is no circle actually involved in the linear motion—it just goes up and down. We may point out that we have, in fact, already solved that diﬀerential equation when we were studying the mechanics of circular motion. If a particle moves in a circle with a constant speed v, the radius vector from the center of the circle to the particle turns through an angle whose size is proportional to the time. If we call this angle θ = vt/R (Fig. 21-2) then dθ/dt = ω0 = v/R. We know that there is an acceleration a = v2/R = ω2 0R toward the center. Now we also know that the position x, at a given moment, is the radius of the circle times cos θ, and that y is the radius times sin θ: x = R cos θ,

y = R sin θ.

Now what about the acceleration? What is the x-component of acceleration, d2x/dt2? We have already worked that out geometrically; it is the magnitude of the acceleration times the cosine of the projection angle, with a minus sign because it is toward the center.

ax = −a cos θ = −ω2

0R cos θ = −ω2 0x.

(21.7)

Fig. 21-2. A particle moving in a circular path at constant speed.

21-6

In other words, when a particle is moving in a circle, the horizontal component of its motion has an acceleration which is proportional to the horizontal displacement from the center. Of course we also have the solution for motion in a circle: x = R cos ω0t. Equation (21.7) does not depend upon the radius of the circle, so for a circle of any radius, one ﬁnds the same equation for a given ω0. Thus, for several reasons, we expect that the displacement of a mass on a spring will turn out to be proportional to cos ω0t, and will, in fact, be exactly the same motion as we would see if we looked at the x-component of the position of an object rotating in a circle with angular velocity ω0. As a check on this, one can devise an experiment to show that the up-and-down motion of a mass on a spring is the same as that of a point going around in a circle. In Fig. 21-3 an arc light projected on a screen casts shadows of a crank pin on a shaft and of a vertically oscillating mass, side by side. If we let go of the mass at the right time from the right place, and if the shaft speed is carefully adjusted so that the frequencies match, each should follow the other exactly. One can also check the numerical solution we obtained earlier with the cosine function, and see whether that agrees very well.

Fig. 21-3. Demonstration of the equivalence between simple harmonic

motion and uniform circular motion.

Here we may point out that because uniform motion in a circle is so closely related mathematically to oscillatory up-and-down motion, we can analyze oscil- latory motion in a simpler way if we imagine it to be a projection of something going in a circle. In other words, although the distance y means nothing in the oscillator problem, we may still artiﬁcially supplement Eq. (21.2) with another

21-7

equation using y, and put the two together. If we do this, we will be able to analyze our one-dimensional oscillator with circular motions, which is a lot easier than having to solve a diﬀerential equation. The trick in doing this is to use complex numbers, a procedure we shall introduce in the next chapter.

21-4 Initial conditions Now let us consider what determines the constants A and B, or a and ∆. Of course these are determined by how we start the motion. If we start the motion with just a small displacement, that is one type of oscillation; if we start with an initial displacement and then push up when we let go, we get still a diﬀerent motion. The constants A and B, or a and ∆, or any other way of putting it, are determined, of course, by the way the motion started, not by any other features of the situation. These are called the initial conditions. We would like to connect the initial conditions with the constants. Although this can be done using any one of the forms (21.6), it turns out to be easiest if we use Eq. (21.6c). Suppose that at t = 0 we have started with an initial displacement x0 and a certain velocity v0. This is the most general way we can start the motion. (We cannot specify the acceleration with which it started, true, because that is determined by the spring, once we specify x0.) Now let us calculate A and B. We start with the equation for x,

x = A cos ω0t + B sin ω0t.

Since we shall later need the velocity also, we diﬀerentiate x and obtain

v = −ω0A sin ω0t + ω0B cos ω0t.

These expressions are valid for all t, but we have special knowledge about x and v at t = 0. So if we put t = 0 into these equations, on the left we get x0 and v0, because that is what x and v are at t = 0; also, we know that the cosine of zero is unity, and the sine of zero is zero. Therefore we get

and

x0 = A · 1 + B · 0 = A

v0 = −ω0A · 0 + ω0B · 1 = ω0B.

So for this particular case we ﬁnd that

From these values of A and B, we can get a and ∆ if we wish.

A = x0,

B = v0/ω0.

21-8

That is the end of our solution, but there is one physically interesting thing to check, and that is the conservation of energy. Since there are no frictional losses, energy ought to be conserved. Let us use the formula

then

x = a cos (ω0t + ∆); v = −ω0a sin (ω0t + ∆).

Now let us ﬁnd out what the kinetic energy T is, and what the potential energy U is. The potential energy at any moment is 1 2 kx2, where x is the displacement and k is the constant of the spring. If we substitute for x, using our expression above, we get

U = 1

2 kx2 = 1

2 ka2 cos2 (ω0t + ∆).

Of course the potential energy is not constant; the potential never becomes negative, naturally—there is always some energy in the spring, but the amount of energy ﬂuctuates with x. The kinetic energy, on the other hand, is 1 2 mv2, and by substituting for v we get T = 1

0a2 sin2 (ω0t + ∆).

2 mv2 = 1

2 mω2

Now the kinetic energy is zero when x is at the maximum, because then there is no velocity; on the other hand, it is maximal when x is passing through zero, because then it is moving fastest. This variation of the kinetic energy is just the opposite of that of the potential energy. But the total energy ought to be a constant. If we note that k = mω2

0, we see that

T + U = 1

2 mω2

0a2[cos2 (ω0t + ∆) + sin2 (ω0t + ∆)] = 1

2 mω2

0a2.

The energy is dependent on the square of the amplitude; if we have twice the amplitude, we get an oscillation which has four times the energy. The average potential energy is half the maximum and, therefore, half the total, and the average kinetic energy is likewise half the total energy.

21-5 Forced oscillations Next we shall discuss the forced harmonic oscillator, i.e., one in which there

is an external driving force acting. The equation then is the following:

m d2x/dt2 = −kx + F(t).

(21.8)

21-9

We would like to ﬁnd out what happens in these circumstances. The external driving force can have various kinds of functional dependence on the time; the ﬁrst one that we shall analyze is very simple—we shall suppose that the force is oscillating:

F(t) = F0 cos ωt.

(21.9) Notice, however, that this ω is not necessarily ω0: we have ω under our control; the forcing may be done at diﬀerent frequencies. So we try to solve Eq. (21.8) with the special force (21.9). What is the solution of (21.8)? One special solution, (we shall discuss the more general cases later) is

x = C cos ωt,

(21.10) where the constant is to be determined. In other words, we might suppose that if we kept pushing back and forth, the mass would follow back and forth in step with the force. We can try it anyway. So we put (21.10) and (21.9) into (21.8), and get

− mω2C cos ωt = −mω2

(21.11) We have also put in k = mω2 0, so that we will understand the equation better at the end. Now because the cosine appears everywhere, we can divide it out, and that shows that (21.10) is, in fact, a solution, provided we pick C just right. The answer is that C must be

0C cos ωt + F0 cos ωt.

0 − ω2).

C = F0/m(ω2

(21.12) That is, m oscillates at the same frequency as the force, but with an amplitude which depends on the frequency of the force, and also upon the frequency of the natural motion of the oscillator. It means, ﬁrst, that if ω is very small compared with ω0, then the displacement and the force are in the same direction. On the other hand, if we shake it back and forth very fast, then (21.12) tells us that C is negative if ω is above the natural frequency ω0 of the harmonic oscillator. (We will call ω0 the natural frequency of the harmonic oscillator, and ω the applied frequency.) At very high frequency the denominator may become very large, and there is then not much amplitude.

Of course the solution we have found is the solution only if things are started just right, for otherwise there is a part which usually dies out after a while. This other part is called the transient response to F(t), while (21.10) and (21.12) are called the steady-state response.

21-10

According to our formula (21.12), a very remarkable thing should also occur: if ω is almost exactly the same as ω0, then C should approach inﬁnity. So if we adjust the frequency of the force to be「in time」with the natural frequency, then we should get an enormous displacement. This is well known to anybody who has pushed a child on a swing. It does not work very well to close our eyes and push at a certain speed at random. If we happen to get the right timing, then the swing goes very high, but if we have the wrong timing, then sometimes we may be pushing when we should be pulling, and so on, and it does not work.

If we make ω exactly equal to ω0, we ﬁnd that it should oscillate at an inﬁnite amplitude, which is, of course, impossible. The reason it does not is that something goes wrong with the equation, there are some other frictional terms, and other forces, which are not in (21.8) but which occur in the real world. So the amplitude does not reach inﬁnity for some reason; it may be that the spring breaks!

21-11

22

