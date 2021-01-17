Transients

24-1 The energy of an oscillator Although this chapter is entitled「transients,」certain parts of it are, in a way, part of the last chapter on forced oscillation. One of the features of a forced oscillation which we have not yet discussed is the energy in the oscillation. Let us now consider that energy. In a mechanical oscillator, how much kinetic energy is there? It is proportional to the square of the velocity. Now we come to an important point. Consider an arbitrary quantity A, which may be the velocity or something else that we want to discuss. When we write A = ˆAeiωt, a complex number, the true and honest A, in the physical world, is only the real part; therefore if, for some reason, we want to use the square of A, it is not right to square the complex number and then take the real part, because the real part of the square of a complex number is not just the square of the real part, but also involves the imaginary part. So when we wish to ﬁnd the energy we have to get away from the complex notation for a while to see what the inner workings are. Now the true physical A is the real part of A0ei(ωt+∆), that is, A = A0 cos (ωt+ ∆), where ˆA, the complex number, is written as A0ei∆. Now the square of this 0 cos2 (ωt + ∆). The square of the quantity, then, real physical quantity is A2 = A2 goes up and down from a maximum to zero, like the square of the cosine. The square of the cosine has a maximum of 1 and a minimum of 0, and its average value is 1/2. In many circumstances we are not interested in the energy at any speciﬁc moment during the oscillation; for a large number of applications we merely want the average of A2, the mean of the square of A over a period of time large compared with the period of oscillation. In those circumstances, the average of the cosine squared may be used, so we have the following theorem: if A is represented by a complex number, then the mean of A2 is equal to 1 0. Now A2 0

2 A2

24-1

is the square of the magnitude of the complex ˆA. (This can be written in many ways—some people like to write | ˆA|2; others write, ˆA ˆA∗, ˆA times its complex conjugate.) We shall use this theorem several times. Now let us consider the energy in a forced oscillator. The equation for the

forced oscillator is

m d2x/dt2 + γm dx/dt + mω2

0x = F(t).

(24.1)

In our problem, of course, F(t) is a cosine function of t. Now let us analyze the situation: how much work is done by the outside force F? The work done by the force per second, i.e., the power, is the force times the velocity. (We know that the diﬀerential work in a time dt is F dx, and the power is F dx/dt.) Thus

(cid:18) dx

(cid:19)2

dt

+ γm

.

(24.2)

(cid:20)(cid:18) dx

(cid:19)(cid:18) d2x

(cid:19)

dt

dt2

(cid:18) dx

(cid:19)(cid:21)

dt

+ ω2 0x

P = F

= m

dx dt

2 m(dx/dt)2 + But the ﬁrst two terms on the right can also be written as d/dt[ 1 0x2], as is immediately veriﬁed by diﬀerentiating. That is to say, the term in 1 2 mω2 brackets is a pure derivative of two terms that are easy to understand—one is the kinetic energy of motion, and the other is the potential energy of the spring. Let us call this quantity the stored energy, that is, the energy stored in the oscillation. Suppose that we want the average power over many cycles when the oscillator is being forced and has been running for a long time. In the long run, the stored energy does not change—its derivative gives zero average eﬀect. In other words, if we average the power in the long run, all the energy ultimately ends up in the resistive term γm(dx/dt)2. There is some energy stored in the oscillation, but that does not change with time, if we average over many cycles. Therefore the mean power hPi is

(24.3) Using our method of writing complex numbers, and our theorem that hA2i = 0, we may ﬁnd this mean power. Thus if x = ˆxeiωt, then dx/dt = iωˆxeiωt.

1 2 A2 Therefore, in these circumstances, the average power could be written as

hPi = hγm(dx/dt)2i.

hPi = 1

2 γmω2x2 0.

(24.4)

In the notation for electrical circuits, dx/dt is replaced by the current I (I is dq/dt, where q corresponds to x), and mγ corresponds to the resistance R. Thus

24-2

the rate of the energy loss—the power used up by the forcing function—is the resistance in the circuit times the average square of the current:

2 I2 0 .

(24.5) This energy, of course, goes into heating the resistor; it is sometimes called the heating loss or the Joule heating.

hPi = RhI2i = R · 1

Another interesting feature to discuss is how much energy is stored. That is not the same as the power, because although power was at ﬁrst used to store up some energy, after that the system keeps on absorbing power, insofar as there are any heating (resistive) losses. At any moment there is a certain amount of stored energy, so we would like to calculate the mean stored energy hEi also. We have already calculated what the average of (dx/dt)2 is, so we ﬁnd

hEi = 1 = 1

2 mh(dx/dt)2i + 1 2 mω2 2 m(ω2 + ω2 2 x2 0.

0) 1

0hx2i

(24.6)

Now, when an oscillator is very eﬃcient, and if ω is near ω0, so that |ˆx| is large, the stored energy is very high—we can get a large stored energy from a relatively small force. The force does a great deal of work in getting the oscillation going, but then to keep it steady, all it has to do is to ﬁght the friction. The oscillator can have a great deal of energy if the friction is very low, and even though it is oscillating strongly, not much energy is being lost. The eﬃciency of an oscillator can be measured by how much energy is stored, compared with how much work the force does per oscillation.

How does the stored energy compare with the amount of work that is done in one cycle? This is called the Q of the system, and Q is deﬁned as 2π times the mean stored energy, divided by the work done per cycle. (If we were to say the work done per radian instead of per cycle, then the 2π disappears.)

Q = 2π

0) · hx2i 2 m(ω2 + ω2 1 γmω2hx2i · 2π/ω

= ω2 + ω2 2γω

0

.

(24.7)

Q is not a very useful number unless it is very large. When it is relatively large, it gives a measure of how good the oscillator is. People have tried to deﬁne Q in the simplest and most useful way; various deﬁnitions diﬀer a bit from one another, but if Q is very large, all deﬁnitions are in agreement. The most generally accepted deﬁnition is Eq. (24.7), which depends on ω. For a good oscillator, close

24-3

to resonance, we can simplify (24.7) a little by setting ω = ω0, and we then have Q = ω0/γ, which is the deﬁnition of Q that we used before. What is Q for an electrical circuit? To ﬁnd out, we merely have to translate L for m, R for mγ, and 1/C for mω2 0 (see Table 23-1). The Q at resonance is Lω/R, where ω is the resonance frequency. If we consider a circuit with a high Q, that means that the amount of energy stored in the oscillation is very large compared with the amount of work done per cycle by the machinery that drives the oscillations.

24-2 Damped oscillations We now turn to our main topic of discussion: transients. By a transient is meant a solution of the diﬀerential equation when there is no force present, but when the system is not simply at rest. (Of course, if it is standing still at the origin with no force acting, that is a nice problem—it stays there!) Suppose the oscillation starts another way: say it was driven by a force for a while, and then we turn oﬀ the force. What happens then? Let us ﬁrst get a rough idea of what will happen for a very high Q system. So long as a force is acting, the stored energy stays the same, and there is a certain amount of work done to maintain it. Now suppose we turn oﬀ the force, and no more work is being done; then the losses which are eating up the energy of the supply are no longer eating up its energy—there is no more driver. The losses will have to consume, so to speak, the energy that is stored. Let us suppose that Q/2π = 1000. Then the work done per cycle is 1/1000 of the stored energy. Is it not reasonable, since it is oscillating with no driving force, that in one cycle the system will still lose a thousandth of its energy E, which ordinarily would have been supplied from the outside, and that it will continue oscillating, always losing 1/1000 of its energy per cycle? So, as a guess, for a relatively high Q system, we would suppose that the following equation might be roughly right (we will later do it exactly, and it will turn out that it was right!):

dE/dt = −ωE/Q.

(24.8)

This is rough because it is true only for large Q. In each radian the system loses a fraction 1/Q of the stored energy E. Thus in a given amount of time dt the energy will change by an amount ω dt/Q, since the number of radians associated with the time dt is ω dt. What is the frequency? Let us suppose that the system moves

24-4

so nicely, with hardly any force, that if we let go it will oscillate at essentially the same frequency all by itself. So we will guess that ω is the resonant frequency ω0. Then we deduce from Eq. (24.8) that the stored energy will vary as

E = E0e−ω0t/Q = E0e−γt.

(24.9) This would be the measure of the energy at any moment. What would the formula be, roughly, for the amplitude of the oscillation as a function of the time? The same? No! The amount of energy in a spring, say, goes as the square of the displacement; the kinetic energy goes as the square of the velocity; so the total energy goes as the square of the displacement. Thus the displacement, the amplitude of oscillation, will decrease half as fast because of the square. In other words, we guess that the solution for the damped transient motion will be an oscillation of frequency close to the resonance frequency ω0, in which the amplitude of the sine-wave motion will diminish as e−γt/2:

x = A0e−γt/2 cos ω0t.

(24.10) This equation and Fig. 24-1 give us an idea of what we should expect; now let us try to analyze the motion precisely by solving the diﬀerential equation of the motion itself.

Fig. 24-1. A damped cosine oscillation.

So, starting with Eq. (24.1), with no outside force, how do we solve it? Being physicists, we do not have to worry about the method as much as we do about what the solution is. Armed with our previous experience, let us try as a solution an exponential curve, x = Aeiαt. (Why do we try this? It is the easiest thing to diﬀerentiate!) We put this into (24.1) (with F(t) = 0), using the rule that each

24-5

time we diﬀerentiate x with respect to time, we multiply by iα. So it is really quite simple to substitute. Thus our equation looks like this:

(−α2 + iγα + ω2

0)Aeiαt = 0.

(24.11)

The net result must be zero for all times, which is impossible unless (a) A = 0, which is no solution at all—it stands still, or (b)

− α2 + iαγ + ω2

0 = 0.

(24.12)

If we can solve this and ﬁnd an α, then we will have a solution in which A need not be zero!

(24.13) For a while we shall assume that γ is fairly small compared with ω0, so that 0 − γ2/4 is deﬁnitely positive, and there is nothing the matter with taking the ω2 square root. The only bothersome thing is that we get two solutions! Thus

0 − γ2/4. ω2

α = iγ/2 ±q

and

α1 = iγ/2 +q α2 = iγ/2 −q

0 − γ2/4 = iγ/2 + ωγ ω2

0 − γ2/4 = iγ/2 − ωγ. ω2

(24.14)

(24.15)

come so many times and it takes so long to write, we shall callpω2

Let us consider the ﬁrst one, supposing that we had not noticed that the square root has two possible values. Then we know that a solution for x is x1 = Aeiα1t, where A is any constant whatever. Now, in substituting α1, because it is going to 0 − γ2/4 = ωγ. Thus iα1 = −γ/2 + iωγ, and we get x = Ae(−γ/2+iωγ)t, or what is the same, because of the wonderful properties of an exponential,

x1 = Ae−γt/2eiωγ t.

(24.16)

First, we recognize this as an oscillation, an oscillation at a frequency ωγ, which is not exactly the frequency ω0, but is rather close to ω0 if it is a good system. Second, the amplitude of the oscillation is decreasing exponentially! If we take, for instance, the real part of (24.16), we get

x1 = Ae−γt/2 cos ωγt.

(24.17)

24-6

This is very much like our guessed-at solution (24.10), except that the frequency really is ωγ. This is the only error, so it is the same thing—we have the right idea. But everything is not all right! What is not all right is that there is another solution. The other solution is α2, and we see that the diﬀerence is only that the sign of ωγ is reversed: (24.18) What does this mean? We shall soon prove that if x1 and x2 are each a possible solution of Eq. (24.1) with F = 0, then x1 + x2 is also a solution of the same equation! So the general solution x is of the mathematical form

x2 = Be−γt/2e−iωγ t.

x = e−γt/2(Aeiωγ t + Be−iωγ t).

(24.19) Now we may wonder why we bother to give this other solution, since we were so happy with the ﬁrst one all by itself. What is the extra one for, because of course we know we should only take the real part? We know that we must take the real part, but how did the mathematics know that we only wanted the real part? When we had a nonzero driving force F(t), we put in an artiﬁcial force to go with it, and the imaginary part of the equation, so to speak, was driven in a deﬁnite way. But when we put F(t) ≡ 0, our convention that x should be only the real part of whatever we write down is purely our own, and the mathematical equations do not know it yet. The physical world has a real solution, but the answer that we were so happy with before is not real, it is complex. The equation does not know that we are arbitrarily going to take the real part, so it has to present us, so to speak, with a complex conjugate type of solution, so that by putting them together we can make a truly real solution; that is what α2 is doing for us. In order for x to be real, Be−ωγ t will have to be the complex conjugate of Aeωγ t that the imaginary parts disappear. So it turns out that B is the complex conjugate of A, and our real solution is

(24.20) So our real solution is an oscillation with a phase shift and a damping—just as advertised.

x = e−γt/2(Aeiωγ t + A∗e−iωγ t).

24-3 Electrical transients Now let us see if the above really works. We construct the electrical circuit shown in Fig. 24-2, in which we apply to an oscilloscope the voltage across the

24-7

Fig. 24-2. An electrical circuit for demonstrating transients.

inductance L after we suddenly turn on a voltage by closing the switch S. It is an oscillatory circuit, and it generates a transient of some kind. It corresponds to a circumstance in which we suddenly apply a force and the system starts to oscillate. It is the electrical analog of a damped mechanical oscillator, and we watch the oscillation on an oscilloscope, where we should see the curves that we were trying to analyze. (The horizontal motion of the oscilloscope is driven at a uniform speed, while the vertical motion is the voltage across the inductor. The rest of the circuit is only a technical detail. We would like to repeat the experiment many, many times, since the persistence of vision is not good enough to see only one trace on the screen. So we do the experiment again and again by closing the switch 60 times a second; each time we close the switch, we also start the oscilloscope horizontal sweep, and it draws the curve over and over.) In Figs. 24-3 to 24-6 we see examples of damped oscillations, actually photographed on an oscilloscope screen. Figure 24-3 shows a damped oscillation in a circuit which has a high Q, a small γ. It does not die out very fast; it oscillates many times on the way down. But let us see what happens as we decrease Q, so that the oscillation dies out more rapidly. We can decrease Q by increasing the resistance R in the circuit. When we increase the resistance in the circuit, it dies out faster (Fig. 24-4). Then if we increase the resistance in the circuit still more, it dies out faster still (Fig. 24-5). But when we put in more than a certain amount, we cannot see any oscillation at all! The question is, is this because our eyes are not good enough? If we increase the resistance still more, we get a curve like that of Fig. 24-6, which does not appear to have any oscillations, except perhaps one. Now, how can we explain that by mathematics?

The resistance is, of course, proportional to the γ term in the mechanical device. Speciﬁcally, γ is R/L. Now if we increase the γ in the solutions (24.14) and (24.15) that we were so happy with before, chaos sets in when γ/2 exceeds ω0; we must write it a diﬀerent way, as

q

iγ/2 + i

γ2/4 − ω2 0

q

γ2/4 − ω2 0.

iγ/2 − i

and

24-8

Figure 24-3

Figure 24-4

Figure 24-5

Figure 24-6

24-9

Those are now the two solutions and, following the same line of mathematical reasoning as previously, we again ﬁnd two solutions: eiα1t and eiα2t. If we now substitute for α1, we get

a nice exponential decay with no oscillations. Likewise, the other solution is

√

√

x = Ae−(γ/2+

γ2/4−ω2

0)t,

x = Be−(γ/2−

γ2/4−ω2

0)t.

Note that the square root cannot exceed γ/2, because even if ω0 = 0, one term just equals the other. But ω2 0 is taken away from γ2/4, so the square root is less than γ/2, and the term in parentheses is, therefore, always a positive number. Thank goodness! Why? Because if it were negative, we would ﬁnd e raised to a positive factor times t, which would mean it was exploding! In putting more and more resistance into the circuit, we know it is not going to explode—quite the contrary. So now we have two solutions, each one by itself a dying exponential, but one having a much faster「dying rate」than the other. The general solution is of course a combination of the two; the coeﬃcients in the combination depending upon how the motion starts—what the initial conditions of the problem are. In the particular way this circuit happens to be starting, the A is negative and the B is positive, so we get the diﬀerence of two exponential curves. Now let us discuss how we can ﬁnd the two coeﬃcients A and B (or A and A∗), if we know how the motion was started. Suppose that at t = 0 we know that x = x0, and dx/dt = v0. If we put t = 0,

x = x0, and dx/dt = v0 into the expressions x = e−γt/2(Aeiωγ t + A∗e−iωγ t),

dx/dt = e−γt/2[(−γ/2 + iωγ)Aeiωγ t + (−γ/2 − iωγ)A∗e−iωγ t],

we ﬁnd, since e0 = ei0 = 1,

x0 = A + A∗ = 2AR, v0 = −(γ/2)(A + A∗) + iωγ(A − A∗)

= −γx0/2 + iωγ(2iAI),

where A = AR + iAI, and A∗ = AR − iAI. Thus we ﬁnd

AR = x0/2

24-10

and

AI = −(v0 + γx0/2)/2ωγ.

(24.21) This completely determines A and A∗, and therefore the complete curve of the transient solution, in terms of how it begins. Incidentally, we can write the solution another way if we note that

eiθ + e−iθ = 2 cos θ

and

eiθ − e−iθ = 2i sin θ.

We may then write the complete solution as

(cid:20) x0 cos ωγt + v0 + γx0/2

(cid:21)

,

sin ωγt

(24.22)

ωγ

x = e−γt/2

where ωγ = +pω2

0 − γ2/4. This is the mathematical expression for the way an oscillation dies out. We shall not make direct use of it, but there are a number of points we should like to emphasize that are true in more general cases.

First of all the behavior of such a system with no external force is expressed by a sum, or superposition, of pure exponentials in time (which we wrote as eiαt). This is a good solution to try in such circumstances. The values of α may be complex in general, the imaginary parts representing damping. Finally the intimate mathematical relation of the sinusoidal and exponential function discussed in Chapter 22 often appears physically as a change from oscillatory to exponential behavior when some physical parameter (in this case resistance, γ) exceeds some critical value.

24-11

25

