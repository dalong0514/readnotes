The Brownian Movement

41-1 Equipartition of energyThe Brownian movement was discovered in 1827 by Robert Brown, a botanist.While he was studying microscopic life, he noticed little particles of plant pollensjiggling around in the liquid he was looking at in the microscope, and he waswise enough to realize that these were not living, but were just little pieces ofdirt moving around in the water. In fact he helped to demonstrate that thishad nothing to do with life by getting from the ground an old piece of quartz inwhich there was some water trapped. It must have been trapped for millions andmillions of years, but inside he could see the same motion. What one sees is thatvery tiny particles are jiggling all the time.

This was later proved to be one of the eﬀects of molecular motion, and wecan understand it qualitatively by thinking of a great push ball on a playing ﬁeld,seen from a great distance, with a lot of people underneath, all pushing the ballin various directions. We cannot see the people because we imagine that we aretoo far away, but we can see the ball, and we notice that it moves around ratherirregularly. We also know, from the theorems that we have discussed in previouschapters, that the mean kinetic energy of a small particle suspended in a liquidor a gas will be 32 kT even though it is very heavy compared with a molecule. Ifit is very heavy, that means that the speeds are relatively slow, but it turns out,actually, that the speed is not really so slow. In fact, we cannot see the speedof such a particle very easily because although the mean kinetic energy is 32 kT,which represents a speed of a millimeter or so per second for an object a micronor two in diameter, this is very hard to see even in a microscope, because theparticle continuously reverses its direction and does not get anywhere. How farit does get we will discuss at the end of the present chapter. This problem wasﬁrst solved by Einstein at the beginning of the 20th century.

41-1

Incidentally, when we say that the mean kinetic energy of this particle is 3

2 kT,we claim to have derived this result from the kinetic theory, that is, from Newton’slaws. We shall ﬁnd that we can derive all kinds of things—marvelous things—fromthe kinetic theory, and it is most interesting that we can apparently get so muchfrom so little. Of course we do not mean that Newton’s laws are「little」—theyare enough to do it, really—what we mean is that we did not do very much. Howdo we get so much out? The answer is that we have been perpetually makinga certain important assumption, which is that if a given system is in thermalequilibrium at some temperature, it will also be in thermal equilibrium withanything else at the same temperature. For instance, if we wanted to see howa particle would move if it was really colliding with water, we could imaginethat there was a gas present, composed of another kind of particle, little ﬁnepellets that (we suppose) do not interact with water, but only hit the particlewith「hard」collisions. Suppose the particle has a prong sticking out of it; allour pellets have to do is hit the prong. We know all about this imaginary gas ofpellets at temperature T—it is an ideal gas. Water is complicated, but an idealgas is simple. Now, our particle has to be in equilibrium with the gas of pellets.Therefore, the mean motion of the particle must be what we get for gaseouscollisions, because if it were not moving at the right speed relative to the waterbut, say, was moving faster, that would mean that the pellets would pick upenergy from it and get hotter than the water. But we had started them at thesame temperature, and we assume that if a thing is once in equilibrium, it stays inequilibrium—parts of it do not get hotter and other parts colder, spontaneously.This proposition is true and can be proved from the laws of mechanics, butthe proof is very complicated and can be established only by using advancedmechanics. It is much easier to prove in quantum mechanics than it is in classicalmechanics. It was proved ﬁrst by Boltzmann, but for now we simply take it to2 kT of energy if itbe true, and then we can argue that our particle has to have 3is hit with artiﬁcial pellets, so it also must have 32 kT when it is being hit withwater at the same temperature and we take away the pellets; so it is 32 kT. It is astrange line of argument, but perfectly valid.In addition to the motion of colloidal particles for which the Brownian move-ment was ﬁrst discovered, there are a number of other phenomena, both in thelaboratory and in other situations, where one can see Brownian movement. If weare trying to build the most delicate possible equipment, say a very small mirroron a thin quartz ﬁber for a very sensitive ballistic galvanometer (Fig. 41-1), themirror does not stay put, but jiggles all the time—all the time—so that when we

41-2

Fig. 41-1. (a) A sensitive light-beam galvanometer. Light from asource L is reﬂected from a small mirror onto a scale. (b) A schematicrecord of the reading of the scale as a function of the time.

shine a light on it and look at the position of the spot, we do not have a perfectinstrument because the mirror is always jiggling. Why? Because the averagekinetic energy of rotation of this mirror has to be, on the average, 1

What is the mean-square angle over which the mirror will wobble? Suppose weﬁnd the natural vibration period of the mirror by tapping on one side and seeinghow long it takes to oscillate back and forth, and we also know the moment ofinertia, I. We know the formula for the kinetic energy of rotation—it is given byEq. (19.8): T = 12 Iω2. That is the kinetic energy, and the potential energy thatgoes with it will be proportional to the square of the angle—it is V = 12 αθ2. But,if we know the period t0 and calculate from that the natural frequency ω0 = 2π/t0,then the potential energy is V = 10θ2. Now we know that the average kineticenergy is 12 kT, but since it is a harmonic oscillator the average potential energyis also 1

2 kT.

2 kT. Thus

or

2 Iω2

0hθ2i = 12 Iω212 kT,hθ2i = kT /Iω20.

(41.1)

In this way we can calculate the oscillations of a galvanometer mirror, and therebyﬁnd what the limitations of our instrument will be. If we want to have smalleroscillations, we have to cool the mirror. An interesting question is, where to coolit. This depends upon where it is getting its「kicks」from. If it is through theﬁber, we cool it at the top—if the mirror is surrounded by a gas and is getting hitmostly by collisions in the gas, it is better to cool the gas. As a matter of fact, ifwe know where the damping of the oscillations comes from, it turns out that thatis always the source of the ﬂuctuations also, a point which we will come back to.

41-3

Fig. 41-2. A high-Q resonant circuit. (a) Actual circuit, at tempera-ture T . (b) Artiﬁcial circuit, with an ideal (noiseless) resistance and a「noise generator」G.

The same thing works, amazingly enough, in electrical circuits. Suppose thatwe are building a very sensitive, accurate ampliﬁer for a deﬁnite frequency andhave a resonant circuit (Fig. 41-2) in the input so as to make it very sensitive tothis certain frequency, like a radio receiver, but a really good one. Suppose wewish to go down to the very lowest limit of things, so we take the voltage, sayoﬀ the inductance, and send it into the rest of the ampliﬁer. Of course, in anycircuit like this, there is a certain amount of loss. It is not a perfect resonantcircuit, but it is a very good one and there is a little resistance, say (we putthe resistor in so we can see it, but it is supposed to be small). Now we wouldlike to ﬁnd out: How much does the voltage across the inductance ﬂuctuate?Answer: We know that 12 LI2 is the「kinetic energy」—the energy associated witha coil in a resonant circuit (Chapter 25). Therefore the mean value of 12 LI2 is2 kT—that tells us what the rms current is and we can ﬁnd out whatequal to 1the rms voltage is from the rms current. For if we want the voltage across theinductance the formula is ˆVL = iωLˆI, and the mean absolute square voltage onthe inductance is hV 2

0hI2i, and putting in 1

2 kT, we obtain

2 LhI2i = 1

Li = L2ω2

0kT.

hV 2

Li = Lω2

(41.2)So now we can design circuits and tell when we are going to get what is calledJohnson noise, the noise associated with thermal ﬂuctuations!Where do the ﬂuctuations come from this time? They come again from theresistor—they come from the fact that the electrons in the resistor are jigglingaround because they are in thermal equilibrium with the matter in the resistor,and they make ﬂuctuations in the density of electrons. They thus make tinyelectric ﬁelds which drive the resonant circuit.

Electrical engineers represent the answer in another way. Physically, theresistor is eﬀectively the source of noise. However, we may replace the real circuit

41-4

having an honest, true physical resistor which is making noise, by an artiﬁcialcircuit which contains a little generator that is going to represent the noise, andnow the resistor is otherwise ideal—no noise comes from it. All the noise isin the artiﬁcial generator. And so if we knew the characteristics of the noisegenerated by a resistor, if we had the formula for that, then we could calculatewhat the circuit is going to do in response to that noise. So, we need a formulafor the noise ﬂuctuations. Now the noise that is generated by the resistor is atall frequencies, since the resistor by itself is not resonant. Of course the resonantcircuit only「listens」to the part that is near the right frequency, but the resistorhas many diﬀerent frequencies in it. We may describe how strong the generatoris, as follows: The mean power that the resistor would absorb if it were connecteddirectly across the noise generator would be hE2i/R, if E were the voltage fromthe generator. But we would like to know in more detail how much power thereis at every frequency. There is very little power in any one frequency; it is adistribution. Let P(ω) dω be the power that the generator would deliver in thefrequency range dω into the very same resistor. Then we can prove (we shallprove it for another case, but the mathematics is exactly the same) that thepower comes out

P(ω) dω = (2/π)kT dω,

(41.3)

and is independent of the resistance when put this way.

41-2 Thermal equilibrium of radiationNow we go on to consider a still more advanced and interesting propositionthat is as follows. Suppose we have a charged oscillator like those we were talkingabout when we were discussing light, let us say an electron oscillating up anddown in an atom. If it oscillates up and down, it radiates light. Now suppose thatthis oscillator is in a very thin gas of other atoms, and that from time to timethe atoms collide with it. Then in equilibrium, after a long time, this oscillator2 kT, and sincewill pick up energy such that its kinetic energy of oscillation is 1it is a harmonic oscillator, its entire energy will become kT. That is, of course,a wrong description so far, because the oscillator carries electric charge, and ifit has an energy kT it is shaking up and down and radiating light. Thereforeit is impossible to have equilibrium of real matter alone without the chargesin it emitting light, and as light is emitted, energy ﬂows away, the oscillatorloses its kT as time goes on, and thus the whole gas which is colliding with the

41-5

oscillator gradually cools oﬀ. And that is, of course, the way a warm stove cools,by radiating the light into the sky, because the atoms are jiggling their chargeand they continually radiate, and slowly, because of this radiation, the jigglingmotion slows down.

On the other hand, if we enclose the whole thing in a box so that the lightdoes not go away to inﬁnity, then we can eventually get thermal equilibrium. Wemay either put the gas in a box where we can say that there are other radiatorsin the box walls sending light back or, to take a nicer example, we may supposethe box has mirror walls. It is easier to think about that case. Thus we assumethat all the radiation that goes out from the oscillator keeps running around inthe box. Then, of course, it is true that the oscillator starts to radiate, but prettysoon it can maintain its kT of energy in spite of the fact that it is radiating,because it is being illuminated, we may say, by its own light reﬂected from thewalls of the box. That is, after a while there is a great deal of light rushingaround in the box, and although the oscillator is radiating some, the light comesback and returns some of the energy that was radiated.

We shall now determine how much light there must be in such a box attemperature T in order that the shining of the light on this oscillator willgenerate just enough energy to account for the light it radiated.

Let the gas atoms be very few and far between, so that we have an idealoscillator with no resistance except radiation resistance. Then we consider thatat thermal equilibrium the oscillator is doing two things at the same time. First,it has a mean energy kT, and we calculate how much radiation it emits. Second,this radiation should be exactly the amount that would result because of the factthat the light shining on the oscillator is scattered. Since there is nowhere elsethe energy can go, this eﬀective radiation is really just scattered light from thelight that is in there.

Thus we ﬁrst calculate the energy that is radiated by the oscillator per second,if the oscillator has a certain energy. (We borrow from Chapter 32 on radiationresistance a number of equations without going back over their derivation.) Theenergy radiated per radian divided by the energy of the oscillator is called 1/Q(Eq. 32.8): 1/Q = (dW/dt)/ω0W. Using the quantity γ, the damping constant,this can also be written as 1/Q = γ/ω0, where ω0 is the natural frequency ofthe oscillator—if gamma is very small, Q is very large. The energy radiated persecond is then

dWdt

= ω0WQ

= ω0W γ

ω0

= γW.

(41.4)

41-6

The energy radiated per second is thus simply gamma times the energy of theoscillator. Now the oscillator should have an average energy kT, so we see thatgamma kT is the average amount of energy radiated per second:

hdW/dti = γkT.

(41.5)

Now we only have to know what gamma is. Gamma is easily found fromEq. (32.12). It is

γ = ω0Q

= 23

r0ω20c

,

(41.6)

where r0 = e2/mc2 is the classical electron radius, and we have set λ = 2πc/ω0.Our ﬁnal result for the average rate of radiation of light near the frequency ω0is therefore

= 23

r0ω20kTc

.

dWdt

(41.7)Next we ask how much light must be shining on the oscillator. It must beenough that the energy absorbed from the light (and thereupon scattered) is justexactly this much. In other words, the emitted light is accounted for as scatteredlight from the light that is shining on the oscillator in the cavity. So we mustnow calculate how much light is scattered from the oscillator if there is a certainamount—unknown—of radiation incident on it. Let I(ω) dω be the amount oflight energy there is at the frequency ω, within a certain range dω (because thereis no light at exactly a certain frequency; it is spread all over the spectrum). SoI(ω) is a certain spectral distribution which we are now going to ﬁnd—it is thecolor of a furnace at temperature T that we see when we open the door andlook in the hole. Now how much light is absorbed? We worked out the amountof radiation absorbed from a given incident light beam, and we calculated it interms of a cross section. It is just as though we said that all of the light that fallson a certain cross section is absorbed. So the total amount that is re-radiated(scattered) is the incident intensity I(ω) dω multiplied by the cross section σ.The formula for the cross section that we derived (Eq. 32.19) did not havethe damping included. It is not hard to go through the derivation again and putin the resistance term, which we neglected. If we do that, and calculate the crosssection the same way, we get

.

(41.8)

(cid:18)

σs = 8πr23

0

(cid:19)

ω4(ω2 − ω20)2 + γ2ω2

41-7

Now, as a function of frequency, σs is of signiﬁcant size only for ω very nearto the natural frequency ω0. (Remember that the Q for a radiating oscillatoris about 108.) The oscillator scatters very strongly when ω is equal to ω0, andvery weakly for other values of ω. Therefore we can replace ω by ω0 and ω2 − ω20by 2ω0(ω − ω0), and we get

σs =

2πr2

0ω20

3[(ω − ω0)2 + γ2/4] .

(41.9)

Now the whole curve is localized near ω = ω0. (We do not really have to makeany approximations, but it is much easier to do the integrals if we simplify theequation a bit.) Now we multiply the intensity in a given frequency range by thecross section of scattering, to get the amount of energy scattered in the range dω.The total energy scattered is then the integral of this for all ω. Thus

Z ∞Z ∞

0

0

dWsdt

=

=

I(ω)σs(ω) dω

2πr2

0ω2

0I(ω) dω

3[(ω − ω0)2 + γ2/4] .

(41.10)

Now we set dWs/dt = 3γkT. Why three? Because when we made our analysisof the cross section in Chapter 32, we assumed that the polarization was suchthat the light could drive the oscillator. If we had used an oscillator which couldmove only in one direction, and the light, say, was polarized in the wrong way,it would not give any scattering. So we must either average the cross section ofan oscillator which can go only in one direction, over all directions of incidenceand polarization of the light or, more easily, we can imagine an oscillator whichwill follow the ﬁeld no matter which way the ﬁeld is pointing. Such an oscillator,which can oscillate equally in three directions, would have 3kT average energybecause there are 3 degrees of freedom in that oscillator. So we should use 3γkTbecause of the 3 degrees of freedom.

Now we have to do the integral. Let us suppose that the unknown spectraldistribution I(ω) of the light is a smooth curve and does not vary very muchacross the very narrow frequency region where σs is peaked (Fig. 41-3). Then theonly signiﬁcant contribution comes when ω is very close to ω0, within an amountgamma, which is very small. So therefore, although I(ω) may be an unknownand complicated function, the only place where it is important is near ω = ω0,

41-8

resonance curve 1/(cid:2)(ω − ω0)2 + γ2/4(cid:3). To a good approximation the

Fig. 41-3. The factors in the integrand (41.10). The peak is the

factor I(ω) can be replaced by I(ω0).

and there we may replace the smooth curve by a ﬂat one—a「constant」—atthe same height. In other words, we simply take I(ω) outside the integral signand call it I(ω0). We may also take the rest of the constants out in front of theintegral, and what we have left is

3 πr22

0ω2

0I(ω0)

dω

(ω − ω0)2 + γ2/4 = 3γkT.

(41.11)

Now, the integral should go from 0 to ∞, but 0 is so far from ω0 that the curve isall ﬁnished by that time, so we go instead to minus ∞—it makes no diﬀerence andit is much easier to do the integral. The integral is an inverse tangent function

of the form R dx/(x2 + a2). If we look it up in a book we see that it is equal

to π/a. So what it comes to for our case is 2π/γ. Therefore we get, with somerearranging,

Z ∞

0

I(ω0) = 9γ2kT4π2r20ω20

.

(41.12)

Then we substitute the formula (41.6) for gamma (do not worry about writingω0; since it is true of any ω0, we may just call it ω) and the formula for I(ω)then comes out

(41.13)And that gives us the distribution of light in a hot furnace. It is called theblackbody radiation. Black, because the hole in the furnace that we look at isblack when the temperature is zero.

I(ω) = ω2kTπ2c2 .

41-9

Inside a closed box at temperature T, (41.13) is the distribution of energyof the radiation, according to classical theory. First, let us notice a remarkablefeature of that expression. The charge of the oscillator, the mass of the oscillator,all properties speciﬁc to the oscillator, cancel out, because once we have reachedequilibrium with one oscillator, we must be at equilibrium with any other oscillatorof a diﬀerent mass, or we will be in trouble. So this is an important kind ofcheck on the proposition that equilibrium does not depend on what we are inequilibrium with, but only on the temperature. Now let us draw a picture of theI(ω) curve (Fig. 41-4). It tells us how much light we have at diﬀerent frequencies.

Fig. 41-4. The blackbody intensity distribution at two temperatures,according to classical physics (solid curves). The dashed curves showthe actual distribution.

The amount of intensity that there is in our box, per unit frequency range,goes, as we see, as the square of the frequency, which means that if we have abox at any temperature at all, and if we look at the x-rays that are coming out,there will be a lot of them!

Of course we know this is false. When we open the furnace and take a lookat it, we do not burn our eyes out from x-rays at all. It is completely false.Furthermore, the total energy in the box, the total of all this intensity summedover all frequencies, would be the area under this inﬁnite curve. Therefore,something is fundamentally, powerfully, and absolutely wrong.

Thus was the classical theory absolutely incapable of correctly describingthe distribution of light from a blackbody, just as it was incapable of correctlydescribing the speciﬁc heats of gases. Physicists went back and forth over thisderivation from many diﬀerent points of view, and there is no escape. This isthe prediction of classical physics. Equation (41.13) is called Rayleigh’s law, andit is the prediction of classical physics, and is obviously absurd.

41-10

41-3 Equipartition and the quantum oscillatorThe diﬃculty above was another part of the continual problem of classicalphysics, which started with the diﬃculty of the speciﬁc heat of gases, and now hasbeen focused on the distribution of light in a blackbody. Now, of course, at thetime that theoreticians studied this thing, there were also many measurementsof the actual curve. And it turned out that the correct curve looked like thedashed curves in Fig. 41-4. That is, the x-rays were not there. If we lower thetemperature, the whole curve goes down in proportion to T, according to theclassical theory, but the observed curve also cuts oﬀ sooner at a lower temperature.Thus the low-frequency end of the curve is right, but the high-frequency endis wrong. Why? When Sir James Jeans was worrying about the speciﬁc heatsof gases, he noted that motions which have high frequency are「frozen out」asthe temperature goes too low. That is, if the temperature is too low, if thefrequency is too high, the oscillators do not have kT of energy on the average.Now recall how our derivation of (41.13) worked: It all depends on the energy ofan oscillator at thermal equilibrium. What the kT of (41.5) was, and what thesame kT in (41.13) is, is the mean energy of a harmonic oscillator of frequency ωat temperature T. Classically, this is kT, but experimentally, no!—not when thetemperature is too low or the oscillator frequency is too high. And so the reasonthat the curve falls oﬀ is the same reason that the speciﬁc heats of gases fail.It is easier to study the blackbody curve than it is the speciﬁc heats of gases,which are so complicated, therefore our attention is focused on determining thetrue blackbody curve, because this curve is a curve which correctly tells us, atevery frequency, what the average energy of harmonic oscillators actually is as afunction of temperature.

Planck studied this curve. He ﬁrst determined the answer empirically, byﬁtting the observed curve with a nice function that ﬁtted very well. Thus hehad an empirical formula for the average energy of a harmonic oscillator as afunction of frequency. In other words, he had the right formula instead of kT,and then by ﬁddling around he found a simple derivation for it which involved avery peculiar assumption. That assumption was that the harmonic oscillator cantake up energies only ω at a time. The idea that they can have any energy atall is false. Of course, that was the beginning of the end of classical mechanics.The very ﬁrst correctly determined quantum-mechanical formula will now bederived. Suppose that the permitted energy levels of a harmonic oscillator wereequally spaced at ω0 apart, so that the oscillator could take on only these diﬀerent

41-11

Fig. 41-5. The energy levels of a harmonic oscillator are equally

spaced: En = nω.

energies (Fig. 41-5). Planck made a somewhat more complicated argument thanthe one that is being given here, because that was the very beginning of quantummechanics and he had to prove some things. But we are going to take it as a fact(which he demonstrated in this case) that the probability of occupying a level ofenergy E is P(E) = αe−E/kT . If we go along with that, we will obtain the rightresult.

Suppose now that we have a lot of oscillators, and each is a vibrator offrequency ω0. Some of these vibrators will be in the bottom quantum state,some will be in the next one, and so forth. What we would like to know is theaverage energy of all these oscillators. To ﬁnd out, let us calculate the totalenergy of all the oscillators and divide by the number of oscillators. That willbe the average energy per oscillator in thermal equilibrium, and will also be theenergy that is in equilibrium with the blackbody radiation and that should goin Eq. (41.13) in place of kT. Thus we let N0 be the number of oscillators thatare in the ground state (the lowest energy state); N1 the number of oscillatorsin the state E1; N2 the number that are in state E2; and so on. According tothe hypothesis (which we have not proved) that in quantum mechanics the lawthat replaced the probability e−P.E./kT or e−K.E./kT in classical mechanics is thatthe probability goes down as e−∆E/kT , where ∆E is the excess energy, we shallassume that the number N1 that are in the ﬁrst state will be the number N0 thatare in the ground state, times e−ω/kT . Similarly, N2, the number of oscillatorsin the second state, is N2 = N0e−2ω/kT . To simplify the algebra, let us calle−ω/kT = x. Then we simply have N1 = N0x, N2 = N0x2, . . . , Nn = N0xn.

The total energy of all the oscillators must ﬁrst be worked out. If an oscillatoris in the ground state, there is no energy. If it is in the ﬁrst state, the energyis ω, and there are N1 of them. So N1ω, or ωN0x is how much energy we get

41-12

from those. Those that are in the second state have 2ω, and there are N2 ofthem, so N2 · 2ω = 2ωN0x2 is how much energy we get, and so on. Then weadd it all together to get Etot = N0ω(0 + x + 2x2 + 3x3 + ··· ).And now, how many oscillators are there? Of course, N0 is the number thatare in the ground state, N1 in the ﬁrst state, and so on, and we add them together:Ntot = N0(1 + x + x2 + x3 + ··· ). Thus the average energy is= N0ω(0 + x + 2x2 + 3x3 + ··· )N0(1 + x + x2 + x3 + ··· )

hEi = EtotNtot

.

(41.14)

Now the two sums which appear here we shall leave for the reader to play withand have some fun with. When we are all ﬁnished summing and substitutingfor x in the sum, we should get—if we make no mistakes in the sum—

hEi =

ω

eω/kT − 1 .

(41.15)

This, then, was the ﬁrst quantum-mechanical formula ever known, or ever dis-cussed, and it was the beautiful culmination of decades of puzzlement. Maxwellknew that there was something wrong, and the problem was, what was right?Here is the quantitative answer of what is right instead of kT. This expressionshould, of course, approach kT as ω → 0 or as T → ∞. See if you can prove thatit does—learn how to do the mathematics.This is the famous cutoﬀ factor that Jeans was looking for, and if we use itinstead of kT in (41.13), we obtain for the distribution of light in a black box

I(ω) dω =

ω3 dω

π2c2(eω/kT − 1) .

(41.16)

We see that for a large ω, even though we have ω3 in the numerator, there isan e raised to a tremendous power in the denominator, so the curve comes downagain and does not「blow up」—we do not get ultraviolet light and x-rays wherewe do not expect them!

One might complain that in our derivation of (41.16) we used the quantumtheory for the energy levels of the harmonic oscillator, but the classical theory indetermining the cross section σs. But the quantum theory of light interactingwith a harmonic oscillator gives exactly the same result as that given by theclassical theory. That, in fact, is why we were justiﬁed in spending so much

41-13

time on our analysis of the index of refraction and the scattering of light, usinga model of atoms like little oscillators—the quantum formulas are substantiallythe same.

Now let us return to the Johnson noise in a resistor. We have already remarkedthat the theory of this noise power is really the same theory as that of the classicalblackbody distribution. In fact, rather amusingly, we have already said that if theresistance in a circuit were not a real resistance, but were an antenna (an antennaacts like a resistance because it radiates energy), a radiation resistance, it wouldbe easy for us to calculate what the power would be. It would be just the powerthat runs into the antenna from the light that is all around, and we would get thesame distribution, changed by only one or two factors. We can suppose that theresistor is a generator with an unknown power spectrum P(ω). The spectrum isdetermined by the fact that this same generator, connected to a resonant circuitof any frequency, as in Fig. 41-2(b), generates in the inductance a voltage of themagnitude given in Eq. (41.2). One is thus led to the same integral as in (41.10),and the same method works to give Eq. (41.3). For low temperatures the kTin (41.3) must of course be replaced by (41.15). The two theories (blackbodyradiation and Johnson noise) are also closely related physically, for we may ofcourse connect a resonant circuit to an antenna, so the resistance R is a pureradiation resistance. Since (41.2) does not depend on the physical origin ofthe resistance, we know the generator G for a real resistance and for radiationresistance is the same. What is the origin of the generated power P(ω) if theresistance R is only an ideal antenna in equilibrium with its environment attemperature T? It is the radiation I(ω) in the space at temperature T whichimpinges on the antenna and, as「received signals,」makes an eﬀective generator.Therefore one can deduce a direct relation of P(ω) and I(ω), leading then from(41.13) to (41.3).All the things we have been talking about—the so-called Johnson noise andPlanck’s distribution, and the correct theory of the Brownian movement whichwe are about to describe—are developments of the ﬁrst decade or so of the 20thcentury. Now with those points and that history in mind, we return to theBrownian movement.

41-4 The random walkLet us consider how the position of a jiggling particle should change with time,for very long times compared with the time between「kicks.」Consider a little

41-14

Fig. 41-6. A random walk of 36 steps of length l. How far is S36 from

B? Ans: about 6I on the average.

Brownian movement particle which is jiggling about because it is bombardedon all sides by irregularly jiggling water molecules. Query: After a given lengthof time, how far away is it likely to be from where it began? This problem wassolved by Einstein and Smoluchowski. If we imagine that we divide the timeinto little intervals, let us say a hundredth of a second or so, then after the ﬁrsthundredth of a second it moves here, and in the next hundredth it moves somemore, in the next hundredth of a second it moves somewhere else, and so on. Interms of the rate of bombardment, a hundredth of a second is a very long time.The reader may easily verify that the number of collisions a single molecule ofwater receives in a second is about 1014, so in a hundredth of a second it has1012 collisions, which is a lot! Therefore, after a hundredth of a second it is notgoing to remember what happened before. In other words, the collisions areall random, so that one「step」is not related to the previous「step.」It is likethe famous drunken sailor problem: the sailor comes out of the bar and takesa sequence of steps, but each step is chosen at an arbitrary angle, at random(Fig. 41-6). The question is: After a long time, where is the sailor? Of course wedo not know! It is impossible to say. What do we mean—he is just somewheremore or less random. Well then, on the average, where is he? On the average,how far away from the bar has he gone? We have already answered this question,because once we were discussing the superposition of light from a whole lot ofdiﬀerent sources at diﬀerent phases, and that meant adding a lot of arrows atdiﬀerent angles (Chapter 32). There we discovered that the mean square of thedistance from one end to the other of the chain of random steps, which was theintensity of the light, is the sum of the intensities of the separate pieces. And so,by the same kind of mathematics, we can prove immediately that if RN is thevector distance from the origin after N steps, the mean square of the distanceNi = N L2,from the origin is proportional to the number N of steps. That is, hR2where L is the length of each step. Since the number of steps is proportional tothe time in our present problem, the mean square distance is proportional to the

41-15

time:

hR2i = αt.

(41.17)This does not mean that the mean distance is proportional to the time. If themean distance were proportional to the time it would mean that the drifting isat a nice uniform velocity. The sailor is making some relatively sensible headway,but only such that his mean square distance is proportional to time. That is thecharacteristic of a random walk.We may show very easily that in each successive step the square of the distanceincreases, on the average, by L2. For if we write RN = RN−1 + L, we ﬁnd thatR2

is

N

RN · RN = R2

N

= R2

N−1 + 2RN−1 · L + L2,

hR2

Ni = hR2

Ni = N L2.

and averaging over many trials, we have hR20. Thus, by induction,

N−1i+L2, since hRN−1 · Li =(41.18)Now we would like to calculate the coeﬃcient α in Eq. (41.17), and to do sowe must add a feature. We are going to suppose that if we were to put a force onthis particle (having nothing to do with the Brownian movement—we are takinga side issue for the moment), then it would react in the following way againstthe force. First, there would be inertia. Let m be the coeﬃcient of inertia, theeﬀective mass of the object (not necessarily the same as the real mass of thereal particle, because the water has to move around the particle if we pull on it).Thus if we talk about motion in one direction, there is a term like m(d2x/dt2) onone side. And next, we want also to assume that if we kept a steady pull on theobject, there would be a drag on it from the ﬂuid, proportional to its velocity.Besides the inertia of the ﬂuid, there is a resistance to ﬂow due to the viscosityand the complexity of the ﬂuid. It is absolutely essential that there be someirreversible losses, something like resistance, in order that there be ﬂuctuations.There is no way to produce the kT unless there are also losses. The source of theﬂuctuations is very closely related to these losses. What the mechanism of thisdrag is, we will discuss soon—we shall talk about forces that are proportional tothe velocity and where they come from. But let us suppose for now that thereis such a resistance. Then the formula for the motion under an external force,when we are pulling on it in a normal manner, is

d2xdt2

+ µ

dxdt

m

= Fext.

41-16

(41.19)

The quantity µ can be determined directly from experiment. For example, wecan watch the drop fall under gravity. Then we know that the force is mg, and µis mg divided by the speed of fall the drop ultimately acquires. Or we could putthe drop in a centrifuge and see how fast it sediments. Or if it is charged, we canput an electric ﬁeld on it. So µ is a measurable thing, not an artiﬁcial thing, andit is known for many types of colloidal particles, etc.

Now let us use the same formula in the case where the force is not external,but is equal to the irregular forces of the Brownian movement. We shall thentry to determine the mean square distance that the object goes.Instead oftaking the distances in three dimensions, let us take just one dimension, andﬁnd the mean of x2, just to prepare ourselves. (Obviously the mean of x2 isthe same as the mean of y2 is the same as the mean of z2, and therefore themean square of the distance is just 3 times what we are going to calculate.)The x-component of the irregular forces is, of course, just as irregular as anyother component. What is the rate of change of x2? It is d(x2)/dt = 2x(dx/dt),so what we have to ﬁnd is the average of the position times the velocity. Weshall show that this is a constant, and that therefore the mean square radiuswill increase proportionally to the time, and at what rate. Now if we multiplyEq. (41.19) by x, mx(d2x/dt2) + µx(dx/dt) = xFx. We want the time averageof x(dx/dt), so let us take the average of the whole equation, and study the threeterms. Now what about x times the force? If the particle happens to have gonea certain distance x, then, since the irregular force is completely irregular anddoes not know where the particle started from, the next impulse can be in anydirection relative to x. If x is positive, there is no reason why the average forceshould also be in that direction. It is just as likely to be one way as the other.The bombardment forces are not driving it in a deﬁnite direction. So the averagevalue of x times F is zero. On the other hand, for the term mx(d2x/dt2) we willhave to be a little fancy, and write this as

(cid:18) dx

(cid:19)2

.

dt

mx

d2xdt2

= m

d[x(dx/dt)]

dt

− m

Thus we put in these two terms and take the average of both. So let us see howmuch the ﬁrst term should be. Now x times the velocity has a mean that does notchange with time, because when it gets to some position it has no remembrance ofwhere it was before, so things are no longer changing with time. So this quantity,on the average, is zero. We have left the quantity mv2, and that is the only thing

41-17

we know: mv2/2 has a mean value 1

(cid:28)

mx

d2xdt2

+ µ

x

dxdt

(cid:29)

(cid:28)2 kT. Therefore we ﬁnd that

(cid:29)

= hxFxi

implies

or

−hmv2i + µ2

ddt

hx2i = 0,

dhx2idt

= 2 kTµ

.

(41.20)

Therefore the object has a mean square distance hR2i, at the end of a certainamount of t, equal to

hR2i = 6kT

tµ

.

(41.21)

And so we can actually determine how far the particles go! We ﬁrst mustdetermine how they react to a steady force, how fast they drift under a knownforce (to ﬁnd µ), and then we can determine how far they go in their randommotions. This equation was of considerable importance historically, becauseit was one of the ﬁrst ways by which the constant k was determined. Afterall, we can measure µ, the time, how far the particles go, and we can take anaverage. The reason that the determination of k was important is that in thelaw P V = RT for a mole, we know that R, which can also be measured, is equalto the number of atoms in a mole times k. A mole was originally deﬁned asso and so many grams of oxygen-16 (now carbon is used), so the number ofatoms in a mole was not known, originally. It is, of course, a very interestingand important problem. How big are atoms? How many are there? So one ofthe earliest determinations of the number of atoms was by the determinationof how far a dirty little particle would move if we watched it patiently under amicroscope for a certain length of time. And thus Boltzmann’s constant k andthe Avogadro number N0 were determined because R had already been measured.

41-18

42

