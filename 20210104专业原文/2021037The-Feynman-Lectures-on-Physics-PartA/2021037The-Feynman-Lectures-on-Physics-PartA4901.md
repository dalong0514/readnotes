Modes

49-1 The reﬂection of waves This chapter will consider some of the remarkable phenomena which are a result of conﬁning waves in some ﬁnite region. We will be led ﬁrst to discover a few particular facts about vibrating strings, for example, and then the generalization of these facts will give us a principle which is probably the most far-reaching principle of mathematical physics.

Our ﬁrst example of conﬁning waves will be to conﬁne a wave at one boundary. Let us take the simple example of a one-dimensional wave on a string. One could equally well consider sound in one dimension against a wall, or other situations of a similar nature, but the example of a string will be suﬃcient for our present purposes. Suppose that the string is held at one end, for example by fastening it to an「inﬁnitely solid」wall. This can be expressed mathematically by saying that the displacement y of the string at the position x = 0 must be zero, because the end does not move. Now if it were not for the wall, we know that the general solution for the motion is the sum of two functions, F(x − ct) and G(x + ct), the ﬁrst representing a wave travelling one way in the string, and the second a wave travelling the other way in the string:

y = F(x − ct) + G(x + ct)

(49.1) is the general solution for any string. But we have next to satisfy the condition that the string does not move at one end. If we put x = 0 in Eq. (49.1) and examine y for any value of t, we get y = F(−ct) + G(+ct). Now if this is to be zero for all times, it means that the function G(ct) must be −F(−ct). In other words, G of anything must be −F of minus that same thing. If this result is put back into Eq. (49.1), we ﬁnd that the solution for the problem is

y = F(x − ct) − F(−x − ct).

(49.2)

It is easy to check that we will get y = 0 if we set x = 0.

49-1

Fig. 49-1. Reﬂection of a wave as a superposition of two travelling waves.

Figure 49-1 shows a wave travelling in the negative x-direction near x = 0, and a hypothetical wave travelling in the other direction reversed in sign and on the other side of the origin. We say hypothetical because, of course, there is no string to vibrate on that side of the origin. The total motion of the string is to be regarded as the sum of these two waves in the region of positive x. As they reach the origin, they will always cancel at x = 0, and ﬁnally the second (reﬂected) wave will be the only one to exist for positive x and it will, of course, be travelling in the opposite direction. These results are equivalent to the following statement: if a wave reaches the clamped end of a string, it will be reﬂected with a change in sign. Such a reﬂection can always be understood by imagining that what is coming to the end of the string comes out upside down from behind the wall. In short, if we assume that the string is inﬁnite and that whenever we have a wave going one way we have another one going the other way with the stated symmetry, the displacement at x = 0 will always be zero and it would make no diﬀerence if we clamped the string there.

The next point to be discussed is the reﬂection of a periodic wave. Suppose that the wave represented by F(x − ct) is a sine wave and has been reﬂected; then the reﬂected wave −F(−x−ct) is also a sine wave of the same frequency, but travelling in the opposite direction. This situation can be most simply described by using the complex function notation: F(x−ct) = eiω(t−x/c) and F(−x−ct) = eiω(t+x/c).

49-2

It can be seen that if these are substituted in (49.2) and if x is set equal to 0, then y = 0 for all values of t, so it satisﬁes the necessary condition. Because of the properties of exponentials, this can be written in a simpler form:

y = eiωt(e−iωx/c − eiωx/c) = −2ieiωt sin (ωx/c).

(49.3)

There is something interesting and new here, in that this solution tells us that if we look at any ﬁxed x, the string oscillates at frequency ω. No matter where this point is, the frequency is the same! But there are some places, in particular wherever sin (ωx/c) = 0, where there is no displacement at all. Furthermore, if at any time t we take a snapshot of the vibrating string, the picture will be a sine wave. However, the displacement of this sine wave will depend upon the time t. From inspection of Eq. (49.3) we can see that the length of one cycle of the sine wave is equal to the wavelength of either of the superimposed waves:

λ = 2πc/ω.

(49.4) The points where there is no motion satisfy the condition sin (ωx/c) = 0, which means that (ωx/c) = 0, π, 2π, . . . , nπ, . . . These points are called nodes. Between any two successive nodes, every point moves up and down sinusoidally, but the pattern of motion stays ﬁxed in space. This is the fundamental characteristic of what we call a mode. If one can ﬁnd a pattern of motion which has the property that at any point the object moves perfectly sinusoidally, and that all points move at the same frequency (though some will move more than others), then we have what is called a mode.

49-2 Conﬁned waves, with natural frequencies The next interesting problem is to consider what happens if the string is held at both ends, say at x = 0 and x = L. We can begin with the idea of the reﬂection of waves, starting with some kind of a bump moving in one direction. As time goes on, we would expect the bump to get near one end, and as time goes still further it will become a kind of little wobble, because it is combining with the reversed-image bump which is coming from the other side. Finally the original bump will disappear and the image bump will move in the other direction to repeat the process at the other end. This problem has an easy solution, but an interesting question is whether we can have a sinusoidal motion (the solution just described is periodic, but of course it is not sinusoidally periodic). Let us try

49-3

to put a sinusoidally periodic wave on a string. If the string is tied at one end, we know it must look like our earlier solution (49.3). If it is tied at the other end, it has to look the same at the other end. So the only possibility for periodic sinusoidal motion is that the sine wave must neatly ﬁt into the string length. If it does not ﬁt into the string length, then it is not a natural frequency at which the string can continue to oscillate. In short, if the string is started with a sine wave shape that just ﬁts in, then it will continue to keep that perfect shape of a sine wave and will oscillate harmonically at some frequency.

Mathematically, we can write sin kx for the shape, where k is equal to the factor (ω/c) in Eqs. (49.3) and (49.4), and this function will be zero at x = 0. However, it must also be zero at the other end. The signiﬁcance of this is that k is no longer arbitrary, as was the case for the half-open string. With the string closed at both ends, the only possibility is that sin (kL) = 0, because this is the only condition that will keep both ends ﬁxed. Now in order for a sine to be zero, the angle must be either 0, π, 2π, or some other integral multiple of π. The equation (49.5) will, therefore, give any one of the possible k’s, depending on what integer is put in. For each of the k’s there is a certain frequency ω, which, according to (49.3), is simply (49.6) So we have found the following: that a string has a property that it can have sinusoidal motions, but only at certain frequencies. This is the most important characteristic of conﬁned waves. No matter how complicated the system is, it always turns out that there are some patterns of motion which have a perfect sinusoidal time dependence, but with frequencies that are a property of the particular system and the nature of its boundaries. In the case of the string we have many diﬀerent possible frequencies, each one, by deﬁnition, corresponding to a mode, because a mode is a pattern of motion which repeats itself sinusoidally. Figure 49-2 shows the ﬁrst three modes for a string. For the ﬁrst mode the wavelength λ is 2L. This can be seen if one continues the wave out to x = 2L to obtain one complete cycle of the sine wave. The angular frequency ω is 2πc divided by the wavelength, in general, and in this case, since λ is 2L, the frequency is πc/L, which is in agreement with (49.6) with n = 1. Let us call the ﬁrst mode frequency ω1. Now the next mode shows two loops with one node in the middle. For this mode the wavelength, then, is simply L. The corresponding value of k is

ω = kc = nπc/L.

kL = nπ

49-4

Fig. 49-2. The ﬁrst three modes of a vibrating string.

twice as great and the frequency is twice as large; it is 2ω1. For the third mode it is 3ω1, and so on. So all the diﬀerent frequencies of the string are multiples, 1, 2, 3, 4, and so on, of the lowest frequency ω1.

Returning now to the general motion of the string, it turns out that any possible motion can always be analyzed by asserting that more than one mode is operating at the same time. In fact, for general motion an inﬁnite number of modes must be excited at the same time. To get some idea of this, let us illustrate what happens when there are two modes oscillating at the same time: Suppose that we have the ﬁrst mode oscillating as shown by the sequence of pictures in Fig. 49-3, which illustrates the deﬂection of the string for equally spaced time intervals extending through half a cycle of the lowest frequency.

Now, at the same time, we suppose that there is an oscillation of the second mode also. Figure 49-3 also shows a sequence of pictures of this mode, which at the start is 90◦ out of phase with the ﬁrst mode. This means that at the start it has no displacement, but the two halves of the string have oppositely directed velocities. Now we recall a general principle relating to linear systems: if there are any two solutions, then their sum is also a solution. Therefore a third possible motion of the string would be a displacement obtained by adding the two solutions shown in Fig. 49-3. The result, also shown in the ﬁgure, begins to suggest the idea of a bump running back and forth between the ends of the string, although with only two modes we cannot make a very good picture of it; more modes are needed. This result is, in fact, a special case of a great principle

49-5

Fig. 49-3. Two modes combine to give a travelling wave.

for linear systems:

Any motion at all can be analyzed by assuming that it is the sum of the motions of all the diﬀerent modes, combined with appropriate amplitudes and phases.

The importance of the principle derives from the fact that each mode is very simple—it is nothing but a sinusoidal motion in time. It is true that even the general motion of a string is not really very complicated, but there are other systems, for example the whipping of an airplane wing, in which the motion is much more complicated. Nevertheless, even with an airplane wing, we ﬁnd there is a certain particular way of twisting which has one frequency and other ways of twisting that have other frequencies. If these modes can be found, then the complete motion can always be analyzed as a superposition of harmonic oscillations (except when the whipping is of such degree that the system can no longer be considered as linear).

49-3 Modes in two dimensions The next example to be considered is the interesting situation of modes in two dimensions. Up to this point we have talked only about one-dimensional situations—a stretched string or sound waves in a tube. Ultimately we should consider three dimensions, but an easier step will be that to two dimensions.

49-6

Fig. 49-4. Vibrating rectangular plate.

Consider for deﬁniteness a rectangular rubber drumhead which is conﬁned so as to have no displacement anywhere on the rectangular edge, and let the dimensions of the rectangle be a and b, as shown in Fig. 49-4. Now the question is, what are the characteristics of the possible motion? We can start with the same procedure used for the string. If we had no conﬁnement at all, we would expect waves travelling along with some kind of wave motion. For example, (eiωt)(e−ikxx+ikyy) would represent a sine wave travelling in some direction which depends on the relative values of kx and ky. Now how can we make the x-axis, that is, the line y = 0, a node? Using the ideas developed for the one-dimensional string, we can imagine another wave represented by the complex function (−eiωt)(e−ikxx−ikyy). The superposition of these waves will give zero displacement at y = 0 regardless of the values of x and t. (Although these functions are deﬁned for negative y where there is no drumhead to vibrate, this can be ignored, since the displacement is truly zero at y = 0.) In this case we can look upon the second function as the reﬂected wave. However, we want a nodal line at y = b as well as at y = 0. How do we do that? The solution is related to something we did when studying reﬂection from crystals. These waves which cancel each other at y = 0 will do the same at y = b only if 2b sin θ is an integral multiple of λ, where θ is the angle shown in Fig. 49-4: (49.7) Now in the same way we can make the y-axis a nodal line by adding two more functions −(eiωt)(e+ikxx+ikyy) and +(eiωt)(e+ikxx−ikyy), each representing a reﬂection of one of the other two waves from the x = 0 line. The condition for a nodal line at x = a is similar to the one for y = b. It is that 2a cos θ must also be an integral multiple of λ: (49.8)

m = 0, 1, 2, . . .

mλ = 2b sin θ,

nλ = 2a cos θ.

49-7

Then the ﬁnal result is that the waves bouncing about in the box produce a standing-wave pattern, that is, a deﬁnite mode.

So we must satisfy the above two conditions if we are to have a mode. Let us ﬁrst ﬁnd the wavelength. This can be obtained by eliminating the angle θ from (49.7) and (49.8) to obtain the wavelength in terms of a, b, n and m. The easiest way to do that is to divide both sides of the respective equations by 2b and 2a, square them, and add the two equations together. The result is sin2 θ + cos2 θ = 1 = (nλ/2a)2 + (mλ/2b)2, which can be solved for λ:

1 λ2

= n2 4a2

+ m2 4b2 .

(49.9)

In this way we have determined the wavelength in terms of two integers, and from the wavelength we immediately get the frequency ω, because, as we know, the frequency is equal to 2πc divided by the wavelength. This result is interesting and important enough that we should deduce it by a purely mathematical analysis instead of by an argument about the reﬂections. Let us represent the vibration by a superposition of four waves chosen so that the four lines x = 0, x = a, y = 0, and y = b are all nodes. In addition we shall require that all waves have the same frequency, so that the resulting motion will represent a mode. From our earlier treatment of light reﬂection we know that (eiωt)(e−ikxx+ikyy) represents a wave travelling in the direction indicated in Fig. 49-4. Equation (49.6), that is, k = ω/c, still holds, provided

k2 = k2

x

+ k2 y.

(49.10)

Now our equation for the displacement, say φ, of the rectangular drumhead

It is clear from the ﬁgure that kx = k cos θ and ky = k sin θ. takes on the grand form φ = [eiωt][e(−ikxx+ikyy)− e(+ikxx+ikyy)− e(−ikxx−ikyy) + e(+ikxx−ikyy)]. (49.11a) Although this looks rather a mess, the sum of these things now is not very hard. The exponentials can be combined to give sine functions, so that the displacement turns out to be

(49.11b) In other words, it is a sinusoidal oscillation, all right, with a pattern that is also sinusoidal in both the x- and the y-direction. Our boundary conditions are of

φ = [4 sin kxx sin kyy][eiωt].

49-8

course satisﬁed at x = 0 and y = 0. We also want φ to be zero when x = a and when y = b. Therefore we have to put in two other conditions: kxa must be an integral multiple of π, and kyb must be another integral multiple of π. Since we have seen that kx = k cos θ and ky = k sin θ, we immediately get equations (49.7) and (49.8) and from these the ﬁnal result (49.9). Now let us take as an example a rectangle whose width is twice the height. If we take a = 2b and use Eqs. (49.4) and (49.9), we can calculate the frequencies of all of the modes:

(cid:18) πc

(cid:19)2 4m2 + n2

4

ω2 =

b

.

(49.12)

Table 49-1 lists a few of the simple modes and also shows their shape in a qualitative way.

The most important point to be emphasized about this particular case is that the frequencies are not multiples of each other, nor are they multiples of any number. The idea that the natural frequencies are harmonically related is not generally true. It is not true for a system of more than one dimension, nor is it true for one-dimensional systems which are more complicated than a string with uniform density and tension. A simple example of the latter is a hanging chain in which the tension is higher at the top than at the bottom. If such a chain is set in harmonic oscillation, there are various modes and frequencies, but the frequencies are not simple multiples of any number, nor are the mode shapes sinusoidal.

The modes of more complicated systems are still more elaborate. For example, inside the mouth we have a cavity above the vocal cords, and by moving the tongue and the lips, and so forth, we make an open-ended pipe or a closed-ended pipe of diﬀerent diameters and shapes; it is a terribly complicated resonator, but it is a resonator nevertheless. Now when one talks with the vocal cords, they are made to produce some kind of tone. The tone is rather complicated and there are many sounds coming out, but the cavity of the mouth further modiﬁes that tone because of the various resonant frequencies of the cavity. For instance, a singer can sing various vowels, a, or o, or oo, and so forth, at the same pitch, but they sound diﬀerent because the various harmonics are in resonance in this cavity to diﬀerent degrees. The very great importance of the resonant frequencies of a cavity in modifying the voice sounds can be demonstrated by a simple experiment. Since the speed of sound goes as the reciprocal of the square root of the density, the speed of sound may be varied by using diﬀerent gases. If one uses helium

49-9

Table 49-1

Mode shape

m

+

+

−

+ − +

− +

− +

+ −

1

1

1

2

2

n

1

2

3

1

2

(ω/ω0)2

1.25

ω/ω0

1.12

2.00

1.41

3.25

1.80

4.25

2.06

5.00

2.24

instead of air, so that the density is lower, the speed of sound is much higher, and all the frequencies of a cavity will be raised. Consequently if one ﬁlls one’s lungs with helium before speaking, the character of his voice will be drastically altered even though the vocal cords may still be vibrating at the same frequency.

49-4 Coupled pendulums Finally we should emphasize that not only do modes exist for complicated continuous systems, but also for very simple mechanical systems. A good example is the system of two coupled pendulums discussed in the preceding chapter. In that chapter it was shown that the motion could be analyzed as a superposition of two harmonic motions with diﬀerent frequencies. So even this system can

49-10

be analyzed in terms of harmonic motions or modes. The string has an inﬁnite number of modes and the two-dimensional surface also has an inﬁnite number of modes. In a sense it is a double inﬁnity, if we know how to count inﬁnities. But a simple mechanical thing which has only two degrees of freedom, and requires only two variables to describe it, has only two modes.

Fig. 49-5. Two coupled pendulums.

Let us make a mathematical analysis of these two modes for the case where the pendulums are of equal length. Let the displacement of one be x, and the displacement of the other be y, as shown in Fig. 49-5. Without a spring, the force on the ﬁrst mass is proportional to the displacement of that mass, because of gravity. There would be, if there were no spring, a certain natural frequency ω0 for this one alone. The equation of motion without a spring would be

d2x dt2

m

= −mω2

0x.

(49.13)

The other pendulum would swing in the same way if there were no spring. In addition to the force of restoration due to gravitation, there is an additional force pulling the ﬁrst mass. That force depends upon the excess distance of x over y and is proportional to that diﬀerence, so it is some constant which depends on the geometry, times (x − y). The same force in reverse sense acts on the second mass. The equations of motion that have to be solved are therefore

d2x dt2

m

= −mω2

0x − k(x − y),

d2y dt2

m

= −mω2

0y − k(y − x).

(49.14)

In order to ﬁnd a motion in which both of the masses move at the same In other words,

frequency, we must determine how much each mass moves.

49-11

pendulum x and pendulum y will oscillate at the same frequency, but their amplitudes must have certain values, A and B, whose relation is ﬁxed. Let us try this solution: (49.15) If these are substituted in Eqs. (49.14) and similar terms are collected, the results are

y = Beiωt.

x = Aeiωt,

(cid:18) (cid:18)

(cid:19) (cid:19)

ω2 − ω2

ω2 − ω2

0 − k m 0 − k m

A = − k m B = − k m

B,

A.

(49.16)

The equations as written have had the common factor eiωt removed and have been divided by m. Now we see that we have two equations for what looks like two unknowns. But there really are not two unknowns, because the whole size of the motion is something that we cannot determine from these equations. The above equations can determine only the ratio of A to B, but they must both give the same ratio. The necessity for both of these equations to be consistent is a requirement that the frequency be something very special.

In this particular case this can be worked out rather easily. If the two equations

are multiplied together, the result is

(cid:18)

(cid:19)2

(cid:18) k

(cid:19)2

m

ω2 − ω2

0 − k m

AB =

AB.

(49.17)

The term AB can be removed from both sides unless A and B are zero, which means there is no motion at all. If there is motion, then the other terms must be equal, giving a quadratic equation to solve. The result is that there are two possible frequencies:

2 = ω2 ω2

1 = ω2 ω2 0,

(49.18) Furthermore, if these values of frequency are substituted back into Eq. (49.16), we ﬁnd that for the ﬁrst frequency A = B, and for the second frequency A = −B. These are the「mode shapes,」as can be readily veriﬁed by experiment. It is clear that in the ﬁrst mode, where A = B, the spring is never stretched, and both masses oscillate at the frequency ω0, as though the spring were absent. In the other solution, where A = −B, the spring contributes a restoring force

m

0 + 2k

.

49-12

and raises the frequency. A more interesting case results if the pendulums have diﬀerent lengths. The analysis is very similar to that given above, and is left as an exercise for the reader.

49-5 Linear systems Now let us summarize the ideas discussed above, which are all aspects of what is probably the most general and wonderful principle of mathematical physics. If we have a linear system whose character is independent of the time, then the motion does not have to have any particular simplicity, and in fact may be exceedingly complex, but there are very special motions, usually a series of special motions, in which the whole pattern of motion varies exponentially with the time. For the vibrating systems that we are talking about now, the exponential is imaginary, and instead of saying「exponentially」we might prefer to say「sinusoidally」with time. However, one can be more general and say that the motions will vary exponentially with the time in very special modes, with very special shapes. The most general motion of the system can always be represented as a superposition of motions involving each of the diﬀerent exponentials.

This is worth stating again for the case of sinusoidal motion: a linear system need not be moving in a purely sinusoidal motion, i.e., at a deﬁnite single frequency, but no matter how it does move, this motion can be represented as a superposition of pure sinusoidal motions. The frequency of each of these motions is a characteristic of the system, and the pattern or waveform of each motion is also a characteristic of the system. The general motion in any such system can be characterized by giving the strength and the phase of each of these modes, and adding them all together. Another way of saying this is that any linear vibrating system is equivalent to a set of independent harmonic oscillators, with the natural frequencies corresponding to the modes.

We conclude this chapter by remarking on the connection of modes with quantum mechanics. In quantum mechanics the vibrating object, or the thing that varies in space, is the amplitude of a probability function that gives the probability of ﬁnding an electron, or system of electrons, in a given conﬁguration. This amplitude function can vary in space and time, and satisﬁes, in fact, a linear equation. But in quantum mechanics there is a transformation, in that what we call frequency of the probability amplitude is equal, in the classical idea, to energy. Therefore we can translate the principle stated above to this case by taking the word frequency and replacing it with energy. It becomes

49-13

something like this: a quantum-mechanical system, for example an atom, need not have a deﬁnite energy, just as a simple mechanical system does not have to have a deﬁnite frequency; but no matter how the system behaves, its behavior can always be represented as a superposition of states of deﬁnite energy. The energy of each state is a characteristic of the atom, and so is the pattern of amplitude which determines the probability of ﬁnding particles in diﬀerent places. The general motion can be described by giving the amplitude of each of these diﬀerent energy states. This is the origin of energy levels in quantum mechanics. Since quantum mechanics is represented by waves, in the circumstance in which the electron does not have enough energy to ultimately escape from the proton, they are conﬁned waves. Like the conﬁned waves of a string, there are deﬁnite frequencies for the solution of the wave equation for quantum mechanics. The quantum-mechanical interpretation is that these are deﬁnite energies. Therefore a quantum-mechanical system, because it is represented by waves, can have deﬁnite states of ﬁxed energy; examples are the energy levels of various atoms.

49-14

50

