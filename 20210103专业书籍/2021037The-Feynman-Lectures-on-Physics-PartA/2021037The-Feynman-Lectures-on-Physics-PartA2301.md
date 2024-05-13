Resonance

23-1 Complex numbers and harmonic motion In the present chapter we shall continue our discussion of the harmonic oscillator and, in particular, the forced harmonic oscillator, using a new technique in the analysis. In the preceding chapter we introduced the idea of complex numbers, which have real and imaginary parts and which can be represented on a diagram in which the ordinate represents the imaginary part and the abscissa represents the real part. If a is a complex number, we may write it as a = ar + iai, where the subscript r means the real part of a, and the subscript i means the imaginary part of a. Referring to Fig. 23-1, we see that we may also write a complex number a = x + iy in the form x + iy = reiθ, where r2 = x2 + y2 = (x + iy)(x − iy) = aa∗. (The complex conjugate of a, written a∗, is obtained by reversing the sign of i in a.) So we shall represent a complex number in either of two forms, a real plus an imaginary part, or a magnitude r and a phase angle θ, so-called. Given r and θ, x and y are clearly r cos θ and r sin θ the ratio of the imaginary to the real part.

and, in reverse, given a complex number x + iy, r =px2 + y2 and tan θ = y/x,

Fig. 23-1. A complex number may be represented by a point in the

「complex plane.」

23-1

We are going to apply complex numbers to our analysis of physical phenomena by the following trick. We have examples of things that oscillate; the oscillation may have a driving force which is a certain constant times cos ωt. Now such a force, F = F0 cos ωt, can be written as the real part of a complex number F = F0eiωt because eiωt = cos ωt + i sin ωt. The reason we do this is that it is easier to work with an exponential function than with a cosine. So the whole trick is to represent our oscillatory functions as the real parts of certain complex functions. The complex number F that we have so deﬁned is not a real physical force, because no force in physics is really complex; actual forces have no imaginary part, only a real part. We shall, however, speak of the「force」F0eiωt, but of course the actual force is the real part of that expression. Let us take another example. Suppose we want to represent a force which is a cosine wave that is out of phase with a delayed phase ∆. This, of course, would be the real part of F0ei(ωt−∆), but exponentials being what they are, we may write ei(ωt−∆) = eiωte−i∆. Thus we see that the algebra of exponentials is much easier than that of sines and cosines; this is the reason we choose to use complex numbers. We shall often write

(23.1) We write a little caret (ˆ) over the F to remind ourselves that this quantity is a complex number: here the number is

F = F0e−i∆eiωt = ˆF eiωt.

ˆF = F0e−i∆.

Now let us solve an equation, using complex numbers, to see whether we can

work out a problem for some real case. For example, let us try to solve

d2x dt2

+ kx m

= F m

= F0 m

cos ωt,

(23.2)

where F is the force which drives the oscillator and x is the displacement. Now, absurd though it may seem, let us suppose that x and F are actually complex numbers, for a mathematical purpose only. That is to say, x has a real part and an imaginary part times i, and F has a real part and an imaginary part times i. Now if we had a solution of (23.2) with complex numbers, and substituted the complex numbers in the equation, we would get + k(xr + ixi)

= Fr + iFi

d2(xr + ixi)

dt2

m

m

23-2

or

d2xr dt2

+ kxr m

(cid:18) d2xi

dt2

+ i

(cid:19)

+ kxi m

= Fr m

+ iFi m

.

Now, since if two complex numbers are equal, their real parts must be equal and their imaginary parts must be equal, we deduce that the real part of x satisﬁes the equation with the real part of the force. We must emphasize, however, that this separation into a real part and an imaginary part is not valid in general, but is valid only for equations which are linear, that is, for equations in which x appears in every term only in the ﬁrst power or the zeroth power. For instance, if there were in the equation a term λx2, then when we substitute xr + ixi, we would get λ(xr + ixi)2, but when separated into real and imaginary parts this would yield λ(x2 ) as the real part and 2iλxrxi as the imaginary part. So we , but also −λx2 see that the real part of the equation would not involve just λx2 . In this case we get a diﬀerent equation than the one we wanted to solve, with xi, the completely artiﬁcial thing we introduced in our analysis, mixed in. Let us now try our new method for the problem of the forced oscillator, that we already know how to solve. We want to solve Eq. (23.2) as before, but we say that we are going to try to solve

r − x2

r

i

i

d2x dt2

+ kx m

=

ˆF eiωt m

,

(23.3)

where ˆF eiωt is a complex number. Of course x will also be complex, but remember the rule: take the real part to ﬁnd out what is really going on. So we try to solve (23.3) for the forced solution; we shall discuss other solutions later. The forced solution has the same frequency as the applied force, and has some amplitude of oscillation and some phase, and so it can be represented also by some complex number ˆx whose magnitude represents the swing of x and whose phase represents the time delay in the same way as for the force. Now a wonderful feature of an exponential function is that d(ˆxeiωt)/dt = iωˆxeiωt. When we diﬀerentiate an exponential function, we bring down the exponent as a simple multiplier. The second derivative does the same thing, it brings down another iω, and so it is very simple to write immediately, by inspection, what the equation is for ˆx: every time we see a diﬀerentiation, we simply multiply by iω. (Diﬀerentiation is now as easy as multiplication! This idea of using exponentials in linear diﬀerential equations is almost as great as the invention of logarithms,

23-3

in which multiplication is replaced by addition. Here diﬀerentiation is replaced by multiplication.) Thus our equation becomes

(iω)2ˆx + (kˆx/m) = ˆF /m.

(23.4) (We have cancelled the common factor eiωt.) See how simple it is! Diﬀerential equations are immediately converted, by sight, into mere algebraic equations; we virtually have the solution by sight, that

ˆx =

ˆF /m

(k/m) − ω2 ,

0 − ω2).

ˆx = ˆF /m(ω2

since (iω)2 = −ω2. This maybe slightly simpliﬁed by substituting k/m = ω2 0, which gives (23.5) 0 − ω2) is a real This, of course, is the solution we had before; for since m(ω2 number, the phase angles of ˆF and of ˆx are the same (or perhaps 180◦ apart, if 0), as advertised previously. The magnitude of ˆx, which measures how far ω2 > ω2 it oscillates, is related to the size of the ˆF by the factor 1/m(ω2 0 − ω2), and this factor becomes enormous when ω is nearly equal to ω0. So we get a very strong response when we apply the right frequency ω (if we hold a pendulum on the end of a string and shake it at just the right frequency, we can make it swing very high).

23-2 The forced oscillator with damping That, then, is how we analyze oscillatory motion with the more elegant mathematical technique. But the elegance of the technique is not at all exhibited in such a problem that can be solved easily by other methods. It is only exhibited when one applies it to more diﬃcult problems. Let us therefore solve another, more diﬃcult problem, which furthermore adds a relatively realistic feature to the previous one. Equation (23.5) tells us that if the frequency ω were exactly equal to ω0, we would have an inﬁnite response. Actually, of course, no such inﬁnite response occurs because some other things, like friction, which we have so far ignored, limits the response. Let us therefore add to Eq. (23.2) a friction term.

Ordinarily such a problem is very diﬃcult because of the character and complexity of the frictional term. There are, however, many circumstances in

23-4

which the frictional force is proportional to the speed with which the object moves. An example of such friction is the friction for slow motion of an object in oil or a thick liquid. There is no force when it is just standing still, but the faster it moves the faster the oil has to go past the object, and the greater is the resistance. So we shall assume that there is, in addition to the terms in (23.2), another term, a resistance force proportional to the velocity: Ff = −c dx/dt. It will be convenient, in our mathematical analysis, to write the constant c as m times γ to simplify the equation a little. This is just the same trick we use with k when we replace it by mω2

0, just to simplify the algebra. Thus our equation will be

m(d2x/dt2) + c(dx/dt) + kx = F

or, writing c = mγ and k = mω2

0 and dividing out the mass m,

(d2x/dt2) + γ(dx/dt) + ω2

0x = F/m.

(23.6)

(23.6a)

Now we have the equation in the most convenient form to solve. If γ is very small, that represents very little friction; if γ is very large, there is a tremendous amount of friction. How do we solve this new linear diﬀerential equation? Suppose that the driving force is equal to F0 cos (ωt + ∆); we could put this into (23.6a) and try to solve it, but we shall instead solve it by our new method. Thus we write F as the real part of ˆF eiωt and x as the real part of ˆxeiωt, and substitute these into Eq. (23.6a). It is not even necessary to do the actual substituting, for we can see by inspection that the equation would become

[(iω)2ˆx + γ(iω)ˆx + ω2

0 ˆx]eiωt = ( ˆF /m)eiωt.

(23.7)

[As a matter of fact, if we tried to solve Eq. (23.6a) by our old straightforward way, we would really appreciate the magic of the「complex」method.] If we divide by eiωt on both sides, then we can obtain the response ˆx to the given force ˆF; it is (23.8) Thus again ˆx is given by ˆF times a certain factor. There is no technical name for this factor, no particular letter for it, but we may call it R for discussion purposes:

0 − ω2 + iγω).

ˆx = ˆF /m(ω2

R =

m(ω2

1

0 − ω2 + iγω) 23-5

and

ˆx = ˆF R.

(23.9) (Although the letters γ and ω0 are in very common use, this R has no particular name.) This factor R can either be written as p + iq, or as a certain magnitude ρ times eiθ. If it is written as a certain magnitude times eiθ, let us see what it means. Now ˆF = F0ei∆, and the actual force F is the real part of F0ei∆eiωt, that is, F0 cos (ωt + ∆). Next, Eq. (23.9) tells us that ˆx is equal to ˆF R. So, writing R = ρeiθ as another name for R, we get

ˆx = R ˆF = ρeiθF0ei∆ = ρF0ei(θ+∆).

Finally, going even further back, we see that the physical x, which is the real part of the complex ˆxeiωt, is equal to the real part of ρF0ei(θ+∆)eiωt. But ρ and F0 are real, and the real part of ei(θ+∆+ωt) is simply cos (ωt + ∆ + θ). Thus

x = ρF0 cos (ωt + ∆ + θ).

(23.10) This tells us that the amplitude of the response is the magnitude of the force F multiplied by a certain magniﬁcation factor, ρ; this gives us the「amount」of oscillation. It also tells us, however, that x is not oscillating in phase with the force, which has the phase ∆, but is shifted by an extra amount θ. Therefore ρ and θ represent the size of the response and the phase shift of the response. Now let us work out what ρ is. If we have a complex number, the square of the magnitude is equal to the number times its complex conjugate; thus

1

0 − ω2 − iγω)

ρ2 =

=

m2(ω2

0 − ω2 + iγω)(ω2 1 m2[(ω2 − ω2 0)2 + γ2ω2] .

(23.11)

In addition, the phase angle θ is easy to ﬁnd, for if we write 0 − ω2 + iγω),

1/R = 1/ρeiθ = (1/ρ)e−iθ = m(ω2

we see that

(23.12) It is minus because tan(−θ) = − tan θ. A negative value for θ results for all ω, and this corresponds to the displacement x lagging the force F.

tan θ = −γω/(ω2

0 − ω2).

23-6

Fig. 23-2. Plot of ρ2 versus ω.

Fig. 23-3. Plot of θ versus ω.

Figure 23-2 shows how ρ2 varies as a function of frequency (ρ2 is physically more interesting than ρ, because ρ2 is proportional to the square of the amplitude, or more or less to the energy that is developed in the oscillator by the force). We 0 − ω2)2 is the most important term, and see that if γ is very small, then 1/(ω2 the response tries to go up toward inﬁnity when ω equals ω0. Now the「inﬁnity」is not actually inﬁnite because if ω = ω0, then 1/γ2ω2 is still there. The phase shift varies as shown in Fig. 23-3. In certain circumstances we get a slightly diﬀerent formula than (23.8), also called a「resonance」formula, and one might think that it represents a diﬀerent phenomenon, but it does not. The reason is that if γ is very small the most interesting part of the curve is near ω = ω0, and we may replace (23.8) by an approximate formula which is very accurate if γ is small and ω is near ω0. 0 − ω2 = (ω0 − ω)(ω0 + ω), if ω is near ω0 this is nearly the same as Since ω2 2ω0(ω0 − ω) and γω is nearly the same as γω0. Using these in (23.8), we see that 0 − ω2 + iγω ≈ 2ω0(ω0 − ω + iγ/2), so that ω2

ˆx ≈ ˆF /2mω0(ω0 − ω + iγ/2)

if γ (cid:28) ω0

and ω ≈ ω0.

(23.13)

23-7

It is easy to ﬁnd the corresponding formula for ρ2. It is 0[(ω0 − ω)2 + γ2/4].

ρ2 ≈ 1/4m2ω2

We shall leave it to the student to show the following: if we call the maximum height of the curve of ρ2 vs. ω one unit, and we ask for the width ∆ω of the curve, at one half the maximum height, the full width at half the maximum height of the curve is ∆ω = γ, supposing that γ is small. The resonance is sharper and sharper as the frictional eﬀects are made smaller and smaller.

As another measure of the width, some people use a quantity Q which is deﬁned as Q = ω0/γ. The narrower the resonance, the higher the Q: Q = 1000 means a resonance whose width is only 1000th of the frequency scale. The Q of the resonance curve shown in Fig. 23-2 is 5.

The importance of the resonance phenomenon is that it occurs in many other circumstances, and so the rest of this chapter will describe some of these other circumstances.

23-3 Electrical resonance The simplest and broadest technical applications of resonance are in electricity. In the electrical world there are a number of objects which can be connected to make electric circuits. These passive circuit elements, as they are often called, are of three main types, although each one has a little bit of the other two mixed in. Before describing them in greater detail, let us note that the whole idea of our mechanical oscillator being a mass on the end of a spring is only an approximation. All the mass is not actually at the「mass」; some of the mass is in the inertia of the spring. Similarly, all of the spring is not at the「spring」; the mass itself has a little elasticity, and although it may appear so, it is not absolutely rigid, and as it goes up and down, it ﬂexes ever so slightly under the action of the spring pulling it. The same thing is true in electricity. There is an approximation in which we can lump things into「circuit elements」which are assumed to have pure, ideal characteristics. It is not the proper time to discuss that approximation here, we shall simply assume that it is true in the circumstances.

The three main kinds of circuit elements are the following. The ﬁrst is called a capacitor (Fig. 23-4); an example is two plane metallic plates spaced a very small distance apart by an insulating material. When the plates are charged there is a certain voltage diﬀerence, that is, a certain diﬀerence in potential, between

23-8

Fig. 23-4. The three passive circuit elements.

them. The same diﬀerence of potential appears between the terminals A and B, because if there were any diﬀerence along the connecting wire, electricity would ﬂow right away. So there is a certain voltage diﬀerence V between the plates if there is a certain electric charge +q and −q on them, respectively. Between the plates there will be a certain electric ﬁeld; we have even found a formula for it (Chapters 13 and 14):

V = σd/0 = qd/0A,

(23.14) where d is the spacing and A is the area of the plates. Note that the potential diﬀerence is a linear function of the charge. If we do not have parallel plates, but insulated electrodes which are of any other shape, the diﬀerence in potential is still precisely proportional to the charge, but the constant of proportionality may not be so easy to compute. However, all we need to know is that the potential diﬀerence across a capacitor is proportional to the charge: V = q/C; the proportionality constant is 1/C, where C is the capacitance of the object. The second kind of circuit element is called a resistor; it oﬀers resistance to the ﬂow of electrical current. It turns out that metallic wires and many other if there is a voltage substances resist the ﬂow of electricity in this manner: diﬀerence across a piece of some substance, there exists an electric current I = dq/dt that is proportional to the electric voltage diﬀerence:

V = RI = R dq/dt

(23.15) The proportionality coeﬃcient is called the resistance R. This relationship may already be familiar to you; it is Ohm’s law. If we think of the charge q on a capacitor as being analogous to the displace- ment x of a mechanical system, we see that the current, I = dq/dt, is analogous to velocity, 1/C is analogous to a spring constant k, and R is analogous to the resistive coeﬃcient c = mγ in Eq. (23.6). Now it is very interesting that there

23-9

exists another circuit element which is the analog of mass! This is a coil which builds up a magnetic ﬁeld within itself when there is a current in it. A changing magnetic ﬁeld develops in the coil a voltage that is proportional to dI/dt (this is how a transformer works, in fact). The magnetic ﬁeld is proportional to a current, and the induced voltage (so-called) in such a coil is proportional to the rate of change of the current:

V = L dI/dt = L d2q/dt2.

(23.16)

The coeﬃcient L is the self-inductance, and is analogous to the mass in a mechanical oscillating circuit.

Fig. 23-5. An oscillatory electrical circuit with resistance, inductance,

and capacitance.

Suppose we make a circuit in which we have connected the three circuit elements in series (Fig. 23-5); then the voltage across the whole thing from 1 to 2 is the work done in carrying a charge through, and it consists of the sum of several pieces: across the inductor, VL = L d2q/dt2; across the resistance, VR = R dq/dt; across the capacitor, VC = q/C. The sum of these is equal to the applied voltage, V :

L d2q/dt2 + R dq/dt + q/C = V (t).

(23.17)

Now we see that this equation is exactly the same as the mechanical equa- tion (23.6), and of course it can be solved in exactly the same manner. We suppose that V (t) is oscillatory: we are driving the circuit with a generator with a pure sine wave oscillation. Then we can write our V (t) as a complex ˆV with the understanding that it must be ultimately multiplied by eiωt, and the real part taken in order to ﬁnd the true V . Likewise, the charge q can thus be analyzed, and then in exactly the same manner as in Eq. (23.8) we write the corresponding equation: the second derivative of ˆq is (iω)2ˆq; the ﬁrst derivative is (iω)ˆq. Thus

23-10

(cid:21)

ˆq = ˆV

L(iω)2 + R(iω) + 1

C

ˆV

Eq. (23.17) translates to (cid:20)

or

ˆq =

which we can write in the form

L(iω)2 + R(iω) + 1

C

ˆq = ˆV /L(ω2

(23.18) where ω2 0 = 1/LC and γ = R/L. It is exactly the same denominator as we had in the mechanical case, with exactly the same resonance properties! The corre- spondence between the electrical and mechanical cases is outlined in Table 23-1.

0 − ω2 + iγω),

General

characteristic

indep. variable dep. variable inertia resistance stiﬀness resonant frequency period ﬁgure of merit

Table 23-1

Mechanical property

time (t) position (x) mass (m) drag coeﬀ. (c = γm) stiﬀness (k) ω2 0 = k/m

t0 = 2πpm/k

Q = ω0/γ

Electrical property

time (t) charge (q) inductance (L) resistance (R = γL) (capacitance)−1 (1/C) ω2 0 = 1/LC √ t0 = 2π LC Q = ω0L/R

We must mention a small technical point.

In the electrical literature, a diﬀerent notation is used. (From one ﬁeld to another, the subject is not really any diﬀerent, but the way of writing the notations is often diﬀerent.) First, j is commonly used instead of i in electrical engineering, to denote √−1. (After all, i must be the current!) Also, the engineers would rather have a relationship between ˆV and ˆI than between ˆV and ˆq, just because they are more used to it that way. Thus, since ˆI = dˆq/dt = iωˆq, we can just substitute ˆI/iω for ˆq and get (23.19)

ˆV = (iωL + R + 1/iωC)ˆI = ˆZ ˆI.

23-11

Another way is to rewrite Eq. (23.17), so that it looks more familiar; one often sees it written this way:

Z t

L dI/dt + RI + (1/C)

I dt = V (t).

(23.20)

At any rate, we ﬁnd the relation (23.19) between voltage ˆV and current ˆI which is just the same as (23.18) except divided by iω, and that produces Eq. (23.19). The quantity R + iωL + 1/iωC is a complex number, and is used so much in electrical engineering that it has a name: it is called the complex impedance, ˆZ. Thus we can write ˆV = ˆZ ˆI. The reason that the engineers like to do this is that they learned something when they were young: V = RI for resistances, when they only knew about resistances and dc. Now they have become more educated and have ac circuits, so they want the equation to look the same. Thus they write ˆV = ˆZ ˆI, the only diﬀerence being that the resistance is replaced by a more complicated thing, a complex quantity. So they insist that they cannot use what everyone else in the world uses for imaginary numbers, they have to use a j for that; it is a miracle that they did not insist also that the letter Z be an R! (Then they get into trouble when they talk about current densities, for which they also use j. The diﬃculties of science are to a large extent the diﬃculties of notations, the units, and all the other artiﬁcialities which are invented by man, not by nature.)

23-4 Resonance in nature Although we have discussed the electrical case in detail, we could also bring up case after case in many ﬁelds, and show exactly how the resonance equation is the same. There are many circumstances in nature in which something is「oscillating」and in which the resonance phenomenon occurs. We said that in an earlier chapter; let us now demonstrate it. If we walk around our study, pulling books oﬀ the shelves and simply looking through them to ﬁnd an example of a curve that corresponds to Fig. 23-2 and comes from the same equation, what do we ﬁnd? Just to demonstrate the wide range obtained by taking the smallest possible sample, it takes only ﬁve or six books to produce quite a series of phenomena which show resonances.

The ﬁrst two are from mechanics, the ﬁrst on a large scale: the atmosphere of the whole earth. If the atmosphere, which we suppose surrounds the earth evenly

23-12

Fig. 23-6. Response of the atmosphere to external excitation. a is the required response if the atmospheric S2-tide is of gravitational origin; peak ampliﬁcation is 100 : 1. b is derived from observed magniﬁcation and phase of M2-tide. [Munk and MacDonald,「Rotation of the Earth,」Cambridge University Press (1960)]

on all sides, is pulled to one side by the moon or, rather, squashed prolate into a double tide, and if we could then let it go, it would go sloshing up and down; it is an oscillator. This oscillator is driven by the moon, which is eﬀectively revolving about the earth; any one component of the force, say in the x-direction, has a cosine component, and so the response of the earth’s atmosphere to the tidal pull of the moon is that of an oscillator. The expected response of the atmosphere is shown in Fig. 23-6, curve b (curve a is another theoretical curve under discussion in the book from which this is taken out of context). Now one might think that we only have one point on this resonance curve, since we only have the one frequency, corresponding to the rotation of the earth under the moon, which occurs at a period of 12.42 hours—12 hours for the earth (the tide is a double bump), plus a little more because the moon is going around. But from the size of the atmospheric tides, and from the phase, the amount of delay, we can get both ρ and θ. From those we can get ω0 and γ, and thus draw the entire curve! This is an example of very poor science. From two numbers we obtain two numbers, and from those two numbers we draw a beautiful curve, which of course goes through the very point that determined the curve! It is of no use unless we can measure something else, and in the case of geophysics that is often very diﬃcult. But in this particular case there is another thing which we can show theoretically must

23-13

have the same timing as the natural frequency ω0: that is, if someone disturbed the atmosphere, it would oscillate with the frequency ω0. Now there was such a sharp disturbance in 1883; the Krakatoa volcano exploded and half the island blew oﬀ, and it made such a terriﬁc explosion in the atmosphere that the period of oscillation of the atmosphere could be measured. It came out to 10 1 2 hours. The ω0 obtained from Fig. 23-6 comes out 10 hours and 20 minutes, so there we have at least one check on the reality of our understanding of the atmospheric tides.

Next we go to the small scale of mechanical oscillation. This time we take a sodium chloride crystal, which has sodium ions and chlorine ions next to each other, as we described in an early chapter. These ions are electrically charged, alternately plus and minus. Now there is an interesting oscillation possible. Suppose that we could drive all the plus charges to the right and all the negative charges to the left, and let go; they would then oscillate back and forth, the sodium lattice against the chlorine lattice. How can we ever drive such a thing? That is easy, for if we apply an electric ﬁeld on the crystal, it will push the plus charge one way and the minus charge the other way! So, by having an external electric ﬁeld we can perhaps get the crystal to oscillate. The frequency of the electric ﬁeld needed is so high, however, that it corresponds to infrared radiation! So we try to ﬁnd a resonance curve by measuring the absorption of infrared light by sodium chloride. Such a curve is shown in Fig. 23-7. The abscissa is not frequency, but is given in terms of wavelength, but that is just a technical matter, of course, since for a wave there is a deﬁnite relation between frequency and wavelength; so it is really a frequency scale, and a certain frequency corresponds to the resonant frequency.

But what about the width? What determines the width? There are many cases in which the width that is seen on the curve is not really the natural width γ that one would have theoretically. There are two reasons why there can be a wider curve than the theoretical curve. If the objects do not all have the same frequency, as might happen if the crystal were strained in certain regions, so that in those regions the oscillation frequency were slightly diﬀerent than in other regions, then what we have is many resonance curves on top of each other; so we apparently get a wider curve. The other kind of width is simply this: perhaps we cannot measure the frequency precisely enough—if we open the slit of the spectrometer fairly wide, so although we thought we had only one frequency, we actually had a certain range ∆ω, then we may not have the resolving power needed to see a narrow curve. Oﬀhand, we cannot say whether the width in

23-14

Fig. 23-7. Transmission of infrared radiation through a thin (0.17 µ) sodium chloride ﬁlm. [After R. B. Barnes, Z. Physik 75, 723 (1932). Kittel, Introduction to Solid State Physics, Wiley, 1956.]

Fig. 23-7 is natural, or whether it is due to inhomogeneities in the crystal or the ﬁnite width of the slit of the spectrometer.

Now we turn to a more esoteric example, and that is the swinging of a magnet. If we have a magnet, with north and south poles, in a constant magnetic ﬁeld, the N end of the magnet will be pulled one way and the S end the other way, and there will in general be a torque on it, so it will vibrate about its equilibrium position, like a compass needle. However, the magnets we are talking about are atoms. These atoms have an angular momentum, the torque does not produce a simple motion in the direction of the ﬁeld, but instead, of course, a precession. Now, looked at from the side, any one component is「swinging,」and we can disturb or drive that swinging and measure an absorption. The curve in Fig. 23-8 represents a typical such resonance curve. What has been done here is slightly diﬀerent technically. The frequency of the lateral ﬁeld that is used to drive this swinging is always kept the same, while we would have expected that the investigators would vary that and plot the curve. They could have done it that way, but technically it was easier for them to leave the frequency ω ﬁxed, and change the strength of the constant magnetic ﬁeld, which corresponds to changing ω0 in our formula. They have plotted the resonance curve against ω0. Anyway, this is a typical resonance with a certain ω0 and γ.

Now we go still further. Our next example has to do with atomic nuclei. The motions of protons and neutrons in nuclei are oscillatory in certain ways, and we

23-15

Fig. 23-8. Magnetic energy loss in paramagnetic organic compound [Holden et al., Phys.

as function of applied magnetic ﬁeld intensity. Rev. 75, 1614 (1949)]

can demonstrate this by the following experiment. We bombard a lithium atom with protons, and we discover that a certain reaction, producing γ-rays, actually has a very sharp maximum typical of resonance. We note in Fig. 23-9, however, one diﬀerence from other cases: the horizontal scale is not a frequency, it is an energy! The reason is that in quantum mechanics what we think of classically as the energy will turn out to be really related to a frequency of a wave amplitude. When we analyze something which in simple large-scale physics has to do with a frequency, we ﬁnd that when we do quantum-mechanical experiments with atomic matter, we get the corresponding curve as a function of energy. In fact, this curve is a demonstration of this relationship, in a sense. It shows that frequency and energy have some deep interrelationship, which of course they do.

Now we turn to another example which also involves a nuclear energy level, but now a much, much narrower one. The ω0 in Fig. 23-10 corresponds to an energy of 100,000 electron volts, while the width γ is approximately 10−5 electron

23-16

Fig. 23-9. The intensity of gamma-radiation from lithium as a func- tion of the energy of the bombarding protons. The dashed curve is a theoretical one calculated for protons with an angular momentum (cid:96) = 0. [Bonner and Evans, Phys. Rev. 73, 666 (1948)]

Fig. 23-10. [Courtesy of Dr. R. Mössbauer]

23-17

volt; in other words, this has a Q of 1010! When this curve was measured it was the largest Q of any oscillator that had ever been measured. It was measured by Dr. Mössbauer, and it was the basis of his Nobel prize. The horizontal scale here is velocity, because the technique for obtaining the slightly diﬀerent frequencies was to use the Doppler eﬀect, by moving the source relative to the absorber. One can see how delicate the experiment is when we realize that the speed involved is a few centimeters per second! On the actual scale of the ﬁgure, zero frequency would correspond to a point about 1010 cm to the left—slightly oﬀ the paper!

Fig. 23-11. Momentum dependence of the cross section for the reactions (a) K− + p → Λ + π+ + π− and (b) K− + p → K0 + n. The lower curves in (a) and (b) represent the presumed nonresonant backgrounds, while the upper curves contain in addition the superposed resonance. [Ferro-Luzzi et al., Phys. Rev. Lett. 8, 28 (1962)]

Finally, if we look in an issue of the Physical Review, say that of January 1, 1962, will we ﬁnd a resonance curve? Every issue has a resonance curve, and Fig. 23-11 is the resonance curve for this one. This resonance curve turns out to be very interesting. It is the resonance found in a certain reaction among strange

23-18

particles, a reaction in which a K− and a proton interact. The resonance is detected by seeing how many of some kinds of particles come out, and depending on what and how many come out, one gets diﬀerent curves, but of the same shape and with the peak at the same energy. We thus determine that there is a resonance at a certain energy for the K− meson. That presumably means that there is some kind of a state, or condition, corresponding to this resonance, which can be attained by putting together a K− and a proton. This is a new particle, or resonance. Today we do not know whether to call a bump like this a「particle」or simply a resonance. When there is a very sharp resonance, it corresponds to a very deﬁnite energy, just as though there were a particle of that energy present in nature. When the resonance gets wider, then we do not know whether to say there is a particle which does not last very long, or simply a resonance in the reaction probability. In the second chapter, this point is made about the particles, but when the second chapter was written this resonance was not known, so our chart should now have still another particle in it!

23-19

24

