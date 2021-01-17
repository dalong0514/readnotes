The Brownian Movement

41-1 Equipartition of energy The Brownian movement was discovered in 1827 by Robert Brown, a botanist. While he was studying microscopic life, he noticed little particles of plant pollens jiggling around in the liquid he was looking at in the microscope, and he was wise enough to realize that these were not living, but were just little pieces of dirt moving around in the water. In fact he helped to demonstrate that this had nothing to do with life by getting from the ground an old piece of quartz in which there was some water trapped. It must have been trapped for millions and millions of years, but inside he could see the same motion. What one sees is that very tiny particles are jiggling all the time.

This was later proved to be one of the eﬀects of molecular motion, and we can understand it qualitatively by thinking of a great push ball on a playing ﬁeld, seen from a great distance, with a lot of people underneath, all pushing the ball in various directions. We cannot see the people because we imagine that we are too far away, but we can see the ball, and we notice that it moves around rather irregularly. We also know, from the theorems that we have discussed in previous chapters, that the mean kinetic energy of a small particle suspended in a liquid or a gas will be 3 2 kT even though it is very heavy compared with a molecule. If it is very heavy, that means that the speeds are relatively slow, but it turns out, actually, that the speed is not really so slow. In fact, we cannot see the speed of such a particle very easily because although the mean kinetic energy is 3 2 kT, which represents a speed of a millimeter or so per second for an object a micron or two in diameter, this is very hard to see even in a microscope, because the particle continuously reverses its direction and does not get anywhere. How far it does get we will discuss at the end of the present chapter. This problem was ﬁrst solved by Einstein at the beginning of the 20th century.

41-1

Incidentally, when we say that the mean kinetic energy of this particle is 3

2 kT, we claim to have derived this result from the kinetic theory, that is, from Newton’s laws. We shall ﬁnd that we can derive all kinds of things—marvelous things—from the kinetic theory, and it is most interesting that we can apparently get so much from so little. Of course we do not mean that Newton’s laws are「little」—they are enough to do it, really—what we mean is that we did not do very much. How do we get so much out? The answer is that we have been perpetually making a certain important assumption, which is that if a given system is in thermal equilibrium at some temperature, it will also be in thermal equilibrium with anything else at the same temperature. For instance, if we wanted to see how a particle would move if it was really colliding with water, we could imagine that there was a gas present, composed of another kind of particle, little ﬁne pellets that (we suppose) do not interact with water, but only hit the particle with「hard」collisions. Suppose the particle has a prong sticking out of it; all our pellets have to do is hit the prong. We know all about this imaginary gas of pellets at temperature T—it is an ideal gas. Water is complicated, but an ideal gas is simple. Now, our particle has to be in equilibrium with the gas of pellets. Therefore, the mean motion of the particle must be what we get for gaseous collisions, because if it were not moving at the right speed relative to the water but, say, was moving faster, that would mean that the pellets would pick up energy from it and get hotter than the water. But we had started them at the same temperature, and we assume that if a thing is once in equilibrium, it stays in equilibrium—parts of it do not get hotter and other parts colder, spontaneously. This proposition is true and can be proved from the laws of mechanics, but the proof is very complicated and can be established only by using advanced mechanics. It is much easier to prove in quantum mechanics than it is in classical mechanics. It was proved ﬁrst by Boltzmann, but for now we simply take it to 2 kT of energy if it be true, and then we can argue that our particle has to have 3 is hit with artiﬁcial pellets, so it also must have 3 2 kT when it is being hit with water at the same temperature and we take away the pellets; so it is 3 2 kT. It is a strange line of argument, but perfectly valid. In addition to the motion of colloidal particles for which the Brownian move- ment was ﬁrst discovered, there are a number of other phenomena, both in the laboratory and in other situations, where one can see Brownian movement. If we are trying to build the most delicate possible equipment, say a very small mirror on a thin quartz ﬁber for a very sensitive ballistic galvanometer (Fig. 41-1), the mirror does not stay put, but jiggles all the time—all the time—so that when we

41-2

Fig. 41-1. (a) A sensitive light-beam galvanometer. Light from a source L is reﬂected from a small mirror onto a scale. (b) A schematic record of the reading of the scale as a function of the time.

shine a light on it and look at the position of the spot, we do not have a perfect instrument because the mirror is always jiggling. Why? Because the average kinetic energy of rotation of this mirror has to be, on the average, 1

What is the mean-square angle over which the mirror will wobble? Suppose we ﬁnd the natural vibration period of the mirror by tapping on one side and seeing how long it takes to oscillate back and forth, and we also know the moment of inertia, I. We know the formula for the kinetic energy of rotation—it is given by Eq. (19.8): T = 1 2 Iω2. That is the kinetic energy, and the potential energy that goes with it will be proportional to the square of the angle—it is V = 1 2 αθ2. But, if we know the period t0 and calculate from that the natural frequency ω0 = 2π/t0, then the potential energy is V = 1 0θ2. Now we know that the average kinetic energy is 1 2 kT, but since it is a harmonic oscillator the average potential energy is also 1

2 kT.

2 kT. Thus

or

2 Iω2

0hθ2i = 1 2 Iω2 1 2 kT, hθ2i = kT /Iω2 0.

(41.1)

In this way we can calculate the oscillations of a galvanometer mirror, and thereby ﬁnd what the limitations of our instrument will be. If we want to have smaller oscillations, we have to cool the mirror. An interesting question is, where to cool it. This depends upon where it is getting its「kicks」from. If it is through the ﬁber, we cool it at the top—if the mirror is surrounded by a gas and is getting hit mostly by collisions in the gas, it is better to cool the gas. As a matter of fact, if we know where the damping of the oscillations comes from, it turns out that that is always the source of the ﬂuctuations also, a point which we will come back to.

41-3

Fig. 41-2. A high-Q resonant circuit. (a) Actual circuit, at tempera- ture T . (b) Artiﬁcial circuit, with an ideal (noiseless) resistance and a「noise generator」G.

The same thing works, amazingly enough, in electrical circuits. Suppose that we are building a very sensitive, accurate ampliﬁer for a deﬁnite frequency and have a resonant circuit (Fig. 41-2) in the input so as to make it very sensitive to this certain frequency, like a radio receiver, but a really good one. Suppose we wish to go down to the very lowest limit of things, so we take the voltage, say oﬀ the inductance, and send it into the rest of the ampliﬁer. Of course, in any circuit like this, there is a certain amount of loss. It is not a perfect resonant circuit, but it is a very good one and there is a little resistance, say (we put the resistor in so we can see it, but it is supposed to be small). Now we would like to ﬁnd out: How much does the voltage across the inductance ﬂuctuate? Answer: We know that 1 2 LI2 is the「kinetic energy」—the energy associated with a coil in a resonant circuit (Chapter 25). Therefore the mean value of 1 2 LI2 is 2 kT—that tells us what the rms current is and we can ﬁnd out what equal to 1 the rms voltage is from the rms current. For if we want the voltage across the inductance the formula is ˆVL = iωLˆI, and the mean absolute square voltage on the inductance is hV 2

0hI2i, and putting in 1

2 kT, we obtain

2 LhI2i = 1

Li = L2ω2

0kT.

hV 2

Li = Lω2

(41.2) So now we can design circuits and tell when we are going to get what is called Johnson noise, the noise associated with thermal ﬂuctuations! Where do the ﬂuctuations come from this time? They come again from the resistor—they come from the fact that the electrons in the resistor are jiggling around because they are in thermal equilibrium with the matter in the resistor, and they make ﬂuctuations in the density of electrons. They thus make tiny electric ﬁelds which drive the resonant circuit.

Electrical engineers represent the answer in another way. Physically, the resistor is eﬀectively the source of noise. However, we may replace the real circuit

41-4

having an honest, true physical resistor which is making noise, by an artiﬁcial circuit which contains a little generator that is going to represent the noise, and now the resistor is otherwise ideal—no noise comes from it. All the noise is in the artiﬁcial generator. And so if we knew the characteristics of the noise generated by a resistor, if we had the formula for that, then we could calculate what the circuit is going to do in response to that noise. So, we need a formula for the noise ﬂuctuations. Now the noise that is generated by the resistor is at all frequencies, since the resistor by itself is not resonant. Of course the resonant circuit only「listens」to the part that is near the right frequency, but the resistor has many diﬀerent frequencies in it. We may describe how strong the generator is, as follows: The mean power that the resistor would absorb if it were connected directly across the noise generator would be hE2i/R, if E were the voltage from the generator. But we would like to know in more detail how much power there is at every frequency. There is very little power in any one frequency; it is a distribution. Let P(ω) dω be the power that the generator would deliver in the frequency range dω into the very same resistor. Then we can prove (we shall prove it for another case, but the mathematics is exactly the same) that the power comes out

P(ω) dω = (2/π)kT dω,

(41.3)

and is independent of the resistance when put this way.

41-2 Thermal equilibrium of radiation Now we go on to consider a still more advanced and interesting proposition that is as follows. Suppose we have a charged oscillator like those we were talking about when we were discussing light, let us say an electron oscillating up and down in an atom. If it oscillates up and down, it radiates light. Now suppose that this oscillator is in a very thin gas of other atoms, and that from time to time the atoms collide with it. Then in equilibrium, after a long time, this oscillator 2 kT, and since will pick up energy such that its kinetic energy of oscillation is 1 it is a harmonic oscillator, its entire energy will become kT. That is, of course, a wrong description so far, because the oscillator carries electric charge, and if it has an energy kT it is shaking up and down and radiating light. Therefore it is impossible to have equilibrium of real matter alone without the charges in it emitting light, and as light is emitted, energy ﬂows away, the oscillator loses its kT as time goes on, and thus the whole gas which is colliding with the

41-5

oscillator gradually cools oﬀ. And that is, of course, the way a warm stove cools, by radiating the light into the sky, because the atoms are jiggling their charge and they continually radiate, and slowly, because of this radiation, the jiggling motion slows down.

On the other hand, if we enclose the whole thing in a box so that the light does not go away to inﬁnity, then we can eventually get thermal equilibrium. We may either put the gas in a box where we can say that there are other radiators in the box walls sending light back or, to take a nicer example, we may suppose the box has mirror walls. It is easier to think about that case. Thus we assume that all the radiation that goes out from the oscillator keeps running around in the box. Then, of course, it is true that the oscillator starts to radiate, but pretty soon it can maintain its kT of energy in spite of the fact that it is radiating, because it is being illuminated, we may say, by its own light reﬂected from the walls of the box. That is, after a while there is a great deal of light rushing around in the box, and although the oscillator is radiating some, the light comes back and returns some of the energy that was radiated.

We shall now determine how much light there must be in such a box at temperature T in order that the shining of the light on this oscillator will generate just enough energy to account for the light it radiated.

Let the gas atoms be very few and far between, so that we have an ideal oscillator with no resistance except radiation resistance. Then we consider that at thermal equilibrium the oscillator is doing two things at the same time. First, it has a mean energy kT, and we calculate how much radiation it emits. Second, this radiation should be exactly the amount that would result because of the fact that the light shining on the oscillator is scattered. Since there is nowhere else the energy can go, this eﬀective radiation is really just scattered light from the light that is in there.

Thus we ﬁrst calculate the energy that is radiated by the oscillator per second, if the oscillator has a certain energy. (We borrow from Chapter 32 on radiation resistance a number of equations without going back over their derivation.) The energy radiated per radian divided by the energy of the oscillator is called 1/Q (Eq. 32.8): 1/Q = (dW/dt)/ω0W. Using the quantity γ, the damping constant, this can also be written as 1/Q = γ/ω0, where ω0 is the natural frequency of the oscillator—if gamma is very small, Q is very large. The energy radiated per second is then

dW dt

= ω0W Q

= ω0W γ

ω0

= γW.

(41.4)

41-6

The energy radiated per second is thus simply gamma times the energy of the oscillator. Now the oscillator should have an average energy kT, so we see that gamma kT is the average amount of energy radiated per second:

hdW/dti = γkT.

(41.5)

Now we only have to know what gamma is. Gamma is easily found from Eq. (32.12). It is

γ = ω0 Q

= 2 3

r0ω2 0 c

,

(41.6)

where r0 = e2/mc2 is the classical electron radius, and we have set λ = 2πc/ω0. Our ﬁnal result for the average rate of radiation of light near the frequency ω0 is therefore

= 2 3

r0ω2 0kT c

.

dW dt

(41.7) Next we ask how much light must be shining on the oscillator. It must be enough that the energy absorbed from the light (and thereupon scattered) is just exactly this much. In other words, the emitted light is accounted for as scattered light from the light that is shining on the oscillator in the cavity. So we must now calculate how much light is scattered from the oscillator if there is a certain amount—unknown—of radiation incident on it. Let I(ω) dω be the amount of light energy there is at the frequency ω, within a certain range dω (because there is no light at exactly a certain frequency; it is spread all over the spectrum). So I(ω) is a certain spectral distribution which we are now going to ﬁnd—it is the color of a furnace at temperature T that we see when we open the door and look in the hole. Now how much light is absorbed? We worked out the amount of radiation absorbed from a given incident light beam, and we calculated it in terms of a cross section. It is just as though we said that all of the light that falls on a certain cross section is absorbed. So the total amount that is re-radiated (scattered) is the incident intensity I(ω) dω multiplied by the cross section σ. The formula for the cross section that we derived (Eq. 32.19) did not have the damping included. It is not hard to go through the derivation again and put in the resistance term, which we neglected. If we do that, and calculate the cross section the same way, we get

.

(41.8)

(cid:18)

σs = 8πr2 3

0

(cid:19)

ω4 (ω2 − ω2 0)2 + γ2ω2

41-7

Now, as a function of frequency, σs is of signiﬁcant size only for ω very near to the natural frequency ω0. (Remember that the Q for a radiating oscillator is about 108.) The oscillator scatters very strongly when ω is equal to ω0, and very weakly for other values of ω. Therefore we can replace ω by ω0 and ω2 − ω2 0 by 2ω0(ω − ω0), and we get

σs =

2πr2

0ω2 0

3[(ω − ω0)2 + γ2/4] .

(41.9)

Now the whole curve is localized near ω = ω0. (We do not really have to make any approximations, but it is much easier to do the integrals if we simplify the equation a bit.) Now we multiply the intensity in a given frequency range by the cross section of scattering, to get the amount of energy scattered in the range dω. The total energy scattered is then the integral of this for all ω. Thus

Z ∞ Z ∞

0

0

dWs dt

=

=

I(ω)σs(ω) dω

2πr2

0ω2

0I(ω) dω

3[(ω − ω0)2 + γ2/4] .

(41.10)

Now we set dWs/dt = 3γkT. Why three? Because when we made our analysis of the cross section in Chapter 32, we assumed that the polarization was such that the light could drive the oscillator. If we had used an oscillator which could move only in one direction, and the light, say, was polarized in the wrong way, it would not give any scattering. So we must either average the cross section of an oscillator which can go only in one direction, over all directions of incidence and polarization of the light or, more easily, we can imagine an oscillator which will follow the ﬁeld no matter which way the ﬁeld is pointing. Such an oscillator, which can oscillate equally in three directions, would have 3kT average energy because there are 3 degrees of freedom in that oscillator. So we should use 3γkT because of the 3 degrees of freedom.

Now we have to do the integral. Let us suppose that the unknown spectral distribution I(ω) of the light is a smooth curve and does not vary very much across the very narrow frequency region where σs is peaked (Fig. 41-3). Then the only signiﬁcant contribution comes when ω is very close to ω0, within an amount gamma, which is very small. So therefore, although I(ω) may be an unknown and complicated function, the only place where it is important is near ω = ω0,

41-8

resonance curve 1/(cid:2)(ω − ω0)2 + γ2/4(cid:3). To a good approximation the

Fig. 41-3. The factors in the integrand (41.10). The peak is the

factor I(ω) can be replaced by I(ω0).

and there we may replace the smooth curve by a ﬂat one—a「constant」—at the same height. In other words, we simply take I(ω) outside the integral sign and call it I(ω0). We may also take the rest of the constants out in front of the integral, and what we have left is

3 πr2 2

0ω2

0I(ω0)

dω

(ω − ω0)2 + γ2/4 = 3γkT.

(41.11)

Now, the integral should go from 0 to ∞, but 0 is so far from ω0 that the curve is all ﬁnished by that time, so we go instead to minus ∞—it makes no diﬀerence and it is much easier to do the integral. The integral is an inverse tangent function

of the form R dx/(x2 + a2). If we look it up in a book we see that it is equal

to π/a. So what it comes to for our case is 2π/γ. Therefore we get, with some rearranging,

Z ∞

0

I(ω0) = 9γ2kT 4π2r2 0ω2 0

.

(41.12)

Then we substitute the formula (41.6) for gamma (do not worry about writing ω0; since it is true of any ω0, we may just call it ω) and the formula for I(ω) then comes out

(41.13) And that gives us the distribution of light in a hot furnace. It is called the blackbody radiation. Black, because the hole in the furnace that we look at is black when the temperature is zero.

I(ω) = ω2kT π2c2 .

41-9

Inside a closed box at temperature T, (41.13) is the distribution of energy of the radiation, according to classical theory. First, let us notice a remarkable feature of that expression. The charge of the oscillator, the mass of the oscillator, all properties speciﬁc to the oscillator, cancel out, because once we have reached equilibrium with one oscillator, we must be at equilibrium with any other oscillator of a diﬀerent mass, or we will be in trouble. So this is an important kind of check on the proposition that equilibrium does not depend on what we are in equilibrium with, but only on the temperature. Now let us draw a picture of the I(ω) curve (Fig. 41-4). It tells us how much light we have at diﬀerent frequencies.

Fig. 41-4. The blackbody intensity distribution at two temperatures, according to classical physics (solid curves). The dashed curves show the actual distribution.

The amount of intensity that there is in our box, per unit frequency range, goes, as we see, as the square of the frequency, which means that if we have a box at any temperature at all, and if we look at the x-rays that are coming out, there will be a lot of them!

Of course we know this is false. When we open the furnace and take a look at it, we do not burn our eyes out from x-rays at all. It is completely false. Furthermore, the total energy in the box, the total of all this intensity summed over all frequencies, would be the area under this inﬁnite curve. Therefore, something is fundamentally, powerfully, and absolutely wrong.

Thus was the classical theory absolutely incapable of correctly describing the distribution of light from a blackbody, just as it was incapable of correctly describing the speciﬁc heats of gases. Physicists went back and forth over this derivation from many diﬀerent points of view, and there is no escape. This is the prediction of classical physics. Equation (41.13) is called Rayleigh’s law, and it is the prediction of classical physics, and is obviously absurd.

41-10

41-3 Equipartition and the quantum oscillator The diﬃculty above was another part of the continual problem of classical physics, which started with the diﬃculty of the speciﬁc heat of gases, and now has been focused on the distribution of light in a blackbody. Now, of course, at the time that theoreticians studied this thing, there were also many measurements of the actual curve. And it turned out that the correct curve looked like the dashed curves in Fig. 41-4. That is, the x-rays were not there. If we lower the temperature, the whole curve goes down in proportion to T, according to the classical theory, but the observed curve also cuts oﬀ sooner at a lower temperature. Thus the low-frequency end of the curve is right, but the high-frequency end is wrong. Why? When Sir James Jeans was worrying about the speciﬁc heats of gases, he noted that motions which have high frequency are「frozen out」as the temperature goes too low. That is, if the temperature is too low, if the frequency is too high, the oscillators do not have kT of energy on the average. Now recall how our derivation of (41.13) worked: It all depends on the energy of an oscillator at thermal equilibrium. What the kT of (41.5) was, and what the same kT in (41.13) is, is the mean energy of a harmonic oscillator of frequency ω at temperature T. Classically, this is kT, but experimentally, no!—not when the temperature is too low or the oscillator frequency is too high. And so the reason that the curve falls oﬀ is the same reason that the speciﬁc heats of gases fail. It is easier to study the blackbody curve than it is the speciﬁc heats of gases, which are so complicated, therefore our attention is focused on determining the true blackbody curve, because this curve is a curve which correctly tells us, at every frequency, what the average energy of harmonic oscillators actually is as a function of temperature.

Planck studied this curve. He ﬁrst determined the answer empirically, by ﬁtting the observed curve with a nice function that ﬁtted very well. Thus he had an empirical formula for the average energy of a harmonic oscillator as a function of frequency. In other words, he had the right formula instead of kT, and then by ﬁddling around he found a simple derivation for it which involved a very peculiar assumption. That assumption was that the harmonic oscillator can take up energies only ω at a time. The idea that they can have any energy at all is false. Of course, that was the beginning of the end of classical mechanics. The very ﬁrst correctly determined quantum-mechanical formula will now be derived. Suppose that the permitted energy levels of a harmonic oscillator were equally spaced at ω0 apart, so that the oscillator could take on only these diﬀerent

41-11

Fig. 41-5. The energy levels of a harmonic oscillator are equally

spaced: En = nω.

energies (Fig. 41-5). Planck made a somewhat more complicated argument than the one that is being given here, because that was the very beginning of quantum mechanics and he had to prove some things. But we are going to take it as a fact (which he demonstrated in this case) that the probability of occupying a level of energy E is P(E) = αe−E/kT . If we go along with that, we will obtain the right result.

Suppose now that we have a lot of oscillators, and each is a vibrator of frequency ω0. Some of these vibrators will be in the bottom quantum state, some will be in the next one, and so forth. What we would like to know is the average energy of all these oscillators. To ﬁnd out, let us calculate the total energy of all the oscillators and divide by the number of oscillators. That will be the average energy per oscillator in thermal equilibrium, and will also be the energy that is in equilibrium with the blackbody radiation and that should go in Eq. (41.13) in place of kT. Thus we let N0 be the number of oscillators that are in the ground state (the lowest energy state); N1 the number of oscillators in the state E1; N2 the number that are in state E2; and so on. According to the hypothesis (which we have not proved) that in quantum mechanics the law that replaced the probability e−P.E./kT or e−K.E./kT in classical mechanics is that the probability goes down as e−∆E/kT , where ∆E is the excess energy, we shall assume that the number N1 that are in the ﬁrst state will be the number N0 that are in the ground state, times e−ω/kT . Similarly, N2, the number of oscillators in the second state, is N2 = N0e−2ω/kT . To simplify the algebra, let us call e−ω/kT = x. Then we simply have N1 = N0x, N2 = N0x2, . . . , Nn = N0xn.

The total energy of all the oscillators must ﬁrst be worked out. If an oscillator is in the ground state, there is no energy. If it is in the ﬁrst state, the energy is ω, and there are N1 of them. So N1ω, or ωN0x is how much energy we get

41-12

from those. Those that are in the second state have 2ω, and there are N2 of them, so N2 · 2ω = 2ωN0x2 is how much energy we get, and so on. Then we add it all together to get Etot = N0ω(0 + x + 2x2 + 3x3 + ··· ). And now, how many oscillators are there? Of course, N0 is the number that are in the ground state, N1 in the ﬁrst state, and so on, and we add them together: Ntot = N0(1 + x + x2 + x3 + ··· ). Thus the average energy is = N0ω(0 + x + 2x2 + 3x3 + ··· ) N0(1 + x + x2 + x3 + ··· )

hEi = Etot Ntot

.

(41.14)

Now the two sums which appear here we shall leave for the reader to play with and have some fun with. When we are all ﬁnished summing and substituting for x in the sum, we should get—if we make no mistakes in the sum—

hEi =

ω

eω/kT − 1 .

(41.15)

This, then, was the ﬁrst quantum-mechanical formula ever known, or ever dis- cussed, and it was the beautiful culmination of decades of puzzlement. Maxwell knew that there was something wrong, and the problem was, what was right? Here is the quantitative answer of what is right instead of kT. This expression should, of course, approach kT as ω → 0 or as T → ∞. See if you can prove that it does—learn how to do the mathematics. This is the famous cutoﬀ factor that Jeans was looking for, and if we use it instead of kT in (41.13), we obtain for the distribution of light in a black box

I(ω) dω =

ω3 dω

π2c2(eω/kT − 1) .

(41.16)

We see that for a large ω, even though we have ω3 in the numerator, there is an e raised to a tremendous power in the denominator, so the curve comes down again and does not「blow up」—we do not get ultraviolet light and x-rays where we do not expect them!

One might complain that in our derivation of (41.16) we used the quantum theory for the energy levels of the harmonic oscillator, but the classical theory in determining the cross section σs. But the quantum theory of light interacting with a harmonic oscillator gives exactly the same result as that given by the classical theory. That, in fact, is why we were justiﬁed in spending so much

41-13

time on our analysis of the index of refraction and the scattering of light, using a model of atoms like little oscillators—the quantum formulas are substantially the same.

Now let us return to the Johnson noise in a resistor. We have already remarked that the theory of this noise power is really the same theory as that of the classical blackbody distribution. In fact, rather amusingly, we have already said that if the resistance in a circuit were not a real resistance, but were an antenna (an antenna acts like a resistance because it radiates energy), a radiation resistance, it would be easy for us to calculate what the power would be. It would be just the power that runs into the antenna from the light that is all around, and we would get the same distribution, changed by only one or two factors. We can suppose that the resistor is a generator with an unknown power spectrum P(ω). The spectrum is determined by the fact that this same generator, connected to a resonant circuit of any frequency, as in Fig. 41-2(b), generates in the inductance a voltage of the magnitude given in Eq. (41.2). One is thus led to the same integral as in (41.10), and the same method works to give Eq. (41.3). For low temperatures the kT in (41.3) must of course be replaced by (41.15). The two theories (blackbody radiation and Johnson noise) are also closely related physically, for we may of course connect a resonant circuit to an antenna, so the resistance R is a pure radiation resistance. Since (41.2) does not depend on the physical origin of the resistance, we know the generator G for a real resistance and for radiation resistance is the same. What is the origin of the generated power P(ω) if the resistance R is only an ideal antenna in equilibrium with its environment at temperature T? It is the radiation I(ω) in the space at temperature T which impinges on the antenna and, as「received signals,」makes an eﬀective generator. Therefore one can deduce a direct relation of P(ω) and I(ω), leading then from (41.13) to (41.3). All the things we have been talking about—the so-called Johnson noise and Planck’s distribution, and the correct theory of the Brownian movement which we are about to describe—are developments of the ﬁrst decade or so of the 20th century. Now with those points and that history in mind, we return to the Brownian movement.

41-4 The random walk Let us consider how the position of a jiggling particle should change with time, for very long times compared with the time between「kicks.」Consider a little

41-14

Fig. 41-6. A random walk of 36 steps of length l. How far is S36 from

B? Ans: about 6I on the average.

Brownian movement particle which is jiggling about because it is bombarded on all sides by irregularly jiggling water molecules. Query: After a given length of time, how far away is it likely to be from where it began? This problem was solved by Einstein and Smoluchowski. If we imagine that we divide the time into little intervals, let us say a hundredth of a second or so, then after the ﬁrst hundredth of a second it moves here, and in the next hundredth it moves some more, in the next hundredth of a second it moves somewhere else, and so on. In terms of the rate of bombardment, a hundredth of a second is a very long time. The reader may easily verify that the number of collisions a single molecule of water receives in a second is about 1014, so in a hundredth of a second it has 1012 collisions, which is a lot! Therefore, after a hundredth of a second it is not going to remember what happened before. In other words, the collisions are all random, so that one「step」is not related to the previous「step.」It is like the famous drunken sailor problem: the sailor comes out of the bar and takes a sequence of steps, but each step is chosen at an arbitrary angle, at random (Fig. 41-6). The question is: After a long time, where is the sailor? Of course we do not know! It is impossible to say. What do we mean—he is just somewhere more or less random. Well then, on the average, where is he? On the average, how far away from the bar has he gone? We have already answered this question, because once we were discussing the superposition of light from a whole lot of diﬀerent sources at diﬀerent phases, and that meant adding a lot of arrows at diﬀerent angles (Chapter 32). There we discovered that the mean square of the distance from one end to the other of the chain of random steps, which was the intensity of the light, is the sum of the intensities of the separate pieces. And so, by the same kind of mathematics, we can prove immediately that if RN is the vector distance from the origin after N steps, the mean square of the distance Ni = N L2, from the origin is proportional to the number N of steps. That is, hR2 where L is the length of each step. Since the number of steps is proportional to the time in our present problem, the mean square distance is proportional to the

41-15

time:

hR2i = αt.

(41.17) This does not mean that the mean distance is proportional to the time. If the mean distance were proportional to the time it would mean that the drifting is at a nice uniform velocity. The sailor is making some relatively sensible headway, but only such that his mean square distance is proportional to time. That is the characteristic of a random walk. We may show very easily that in each successive step the square of the distance increases, on the average, by L2. For if we write RN = RN−1 + L, we ﬁnd that R2

is

N

RN · RN = R2

N

= R2

N−1 + 2RN−1 · L + L2,

hR2

Ni = hR2

Ni = N L2.

and averaging over many trials, we have hR2 0. Thus, by induction,

N−1i+L2, since hRN−1 · Li = (41.18) Now we would like to calculate the coeﬃcient α in Eq. (41.17), and to do so we must add a feature. We are going to suppose that if we were to put a force on this particle (having nothing to do with the Brownian movement—we are taking a side issue for the moment), then it would react in the following way against the force. First, there would be inertia. Let m be the coeﬃcient of inertia, the eﬀective mass of the object (not necessarily the same as the real mass of the real particle, because the water has to move around the particle if we pull on it). Thus if we talk about motion in one direction, there is a term like m(d2x/dt2) on one side. And next, we want also to assume that if we kept a steady pull on the object, there would be a drag on it from the ﬂuid, proportional to its velocity. Besides the inertia of the ﬂuid, there is a resistance to ﬂow due to the viscosity and the complexity of the ﬂuid. It is absolutely essential that there be some irreversible losses, something like resistance, in order that there be ﬂuctuations. There is no way to produce the kT unless there are also losses. The source of the ﬂuctuations is very closely related to these losses. What the mechanism of this drag is, we will discuss soon—we shall talk about forces that are proportional to the velocity and where they come from. But let us suppose for now that there is such a resistance. Then the formula for the motion under an external force, when we are pulling on it in a normal manner, is

d2x dt2

+ µ

dx dt

m

= Fext.

41-16

(41.19)

The quantity µ can be determined directly from experiment. For example, we can watch the drop fall under gravity. Then we know that the force is mg, and µ is mg divided by the speed of fall the drop ultimately acquires. Or we could put the drop in a centrifuge and see how fast it sediments. Or if it is charged, we can put an electric ﬁeld on it. So µ is a measurable thing, not an artiﬁcial thing, and it is known for many types of colloidal particles, etc.

Now let us use the same formula in the case where the force is not external, but is equal to the irregular forces of the Brownian movement. We shall then try to determine the mean square distance that the object goes. Instead of taking the distances in three dimensions, let us take just one dimension, and ﬁnd the mean of x2, just to prepare ourselves. (Obviously the mean of x2 is the same as the mean of y2 is the same as the mean of z2, and therefore the mean square of the distance is just 3 times what we are going to calculate.) The x-component of the irregular forces is, of course, just as irregular as any other component. What is the rate of change of x2? It is d(x2)/dt = 2x(dx/dt), so what we have to ﬁnd is the average of the position times the velocity. We shall show that this is a constant, and that therefore the mean square radius will increase proportionally to the time, and at what rate. Now if we multiply Eq. (41.19) by x, mx(d2x/dt2) + µx(dx/dt) = xFx. We want the time average of x(dx/dt), so let us take the average of the whole equation, and study the three terms. Now what about x times the force? If the particle happens to have gone a certain distance x, then, since the irregular force is completely irregular and does not know where the particle started from, the next impulse can be in any direction relative to x. If x is positive, there is no reason why the average force should also be in that direction. It is just as likely to be one way as the other. The bombardment forces are not driving it in a deﬁnite direction. So the average value of x times F is zero. On the other hand, for the term mx(d2x/dt2) we will have to be a little fancy, and write this as

(cid:18) dx

(cid:19)2

.

dt

mx

d2x dt2

= m

d[x(dx/dt)]

dt

− m

Thus we put in these two terms and take the average of both. So let us see how much the ﬁrst term should be. Now x times the velocity has a mean that does not change with time, because when it gets to some position it has no remembrance of where it was before, so things are no longer changing with time. So this quantity, on the average, is zero. We have left the quantity mv2, and that is the only thing

41-17

we know: mv2/2 has a mean value 1

(cid:28)

mx

d2x dt2

+ µ

x

dx dt

(cid:29)

(cid:28) 2 kT. Therefore we ﬁnd that

(cid:29)

= hxFxi

implies

or

−hmv2i + µ 2

d dt

hx2i = 0,

dhx2i dt

= 2 kT µ

.

(41.20)

Therefore the object has a mean square distance hR2i, at the end of a certain amount of t, equal to

hR2i = 6kT

t µ

.

(41.21)

And so we can actually determine how far the particles go! We ﬁrst must determine how they react to a steady force, how fast they drift under a known force (to ﬁnd µ), and then we can determine how far they go in their random motions. This equation was of considerable importance historically, because it was one of the ﬁrst ways by which the constant k was determined. After all, we can measure µ, the time, how far the particles go, and we can take an average. The reason that the determination of k was important is that in the law P V = RT for a mole, we know that R, which can also be measured, is equal to the number of atoms in a mole times k. A mole was originally deﬁned as so and so many grams of oxygen-16 (now carbon is used), so the number of atoms in a mole was not known, originally. It is, of course, a very interesting and important problem. How big are atoms? How many are there? So one of the earliest determinations of the number of atoms was by the determination of how far a dirty little particle would move if we watched it patiently under a microscope for a certain length of time. And thus Boltzmann’s constant k and the Avogadro number N0 were determined because R had already been measured.

41-18

42

