Beats

48-1 Adding two wavesSome time ago we discussed in considerable detail the properties of lightwaves and their interference—that is, the eﬀects of the superposition of two wavesfrom diﬀerent sources. In all these analyses we assumed that the frequenciesof the sources were all the same. In this chapter we shall discuss some of thephenomena which result from the interference of two sources which have diﬀerentfrequencies.It is easy to guess what is going to happen. Proceeding in the same way as wehave done previously, suppose we have two equal oscillating sources of the samefrequency whose phases are so adjusted, say, that the signals arrive in phase atsome point P. At that point, if it is light, the light is very strong; if it is sound,it is very loud; or if it is electrons, many of them arrive. On the other hand, ifthe arriving signals were 180◦ out of phase, we would get no signal at P, becausethe net amplitude there is then a minimum. Now suppose that someone twiststhe「phase knob」of one of the sources and changes the phase at P back andforth, say, ﬁrst making it 0◦ and then 180◦, and so on. Of course, we would thenﬁnd variations in the net signal strength. Now we also see that if the phase ofone source is slowly changing relative to that of the other in a gradual, uniformmanner, starting at zero, going up to ten, twenty, thirty, forty degrees, and soon, then what we would measure at P would be a series of strong and weak「pulsations,」because when the phase shifts through 360◦ the amplitude returnsto a maximum. Of course, to say that one source is shifting its phase relative toanother at a uniform rate is the same as saying that the number of oscillationsper second is slightly diﬀerent for the two.

So we know the answer: if we have two sources at slightly diﬀerent frequencieswe should ﬁnd, as a net result, an oscillation with a slowly pulsating intensity.That is all there really is to the subject!

48-1

Fig. 48-1. The superposition of two cosine waves with frequencies inthe ratio 8 : 10. The precise repetition of the pattern within each「beat」is not typical of the general case.

It is very easy to formulate this result mathematically also. Suppose, forexample, that we have two waves, and that we do not worry for the momentabout all the spatial relations, but simply analyze what arrives at P. From onesource, let us say, we would have cos ω1t, and from the other source, cos ω2t,where the two ω’s are not exactly the same. Of course the amplitudes may notbe the same, either, but we can solve the general problem later; let us ﬁrst takethe case where the amplitudes are equal. Then the total amplitude at P is thesum of these two cosines. If we plot the amplitudes of the waves against the time,as in Fig. 48-1, we see that where the crests coincide we get a strong wave, andwhere a trough and crest coincide we get practically zero, and then when thecrests coincide again we get a strong wave again.

Mathematically, we need only to add two cosines and rearrange the resultsomehow. There exist a number of useful relations among cosines which are notdiﬃcult to derive. Of course we know that

ei(a+b) = eiaeib,

(48.1)

and that eia has a real part, cos a, and an imaginary part, sin a. If we take the

48-2

real part of ei(a+b), we get cos (a + b). If we multiply out:eiaeib = (cos a + i sin a)(cos b + i sin b),

we get cos a cos b − sin a sin b, plus some imaginary parts. But we now need onlythe real part, so we have

cos (a + b) = cos a cos b − sin a sin b.

(48.2)

Now if we change the sign of b, since the cosine does not change sign while thesine does, the same equation, for negative b, is

cos (a − b) = cos a cos b + sin a sin b.

(48.3)

If we add these two equations together, we lose the sines and we learn that theproduct of two cosines is half the cosine of the sum, plus half the cosine of thediﬀerence:

cos a cos b = 1

2 cos (a + b) + 1

(48.4)Now we can also reverse the formula and ﬁnd a formula for cos α + cos β if we2(α − β), sosimply let α = a + b and β = a − b. That is, a = 1that(48.5)

2(α + β) and b = 1

2 cos (a − b).

cos α + cos β = 2 cos 1

2(α + β) cos 1

2(α − β).

Now we can analyze our problem. The sum of cos ω1t and cos ω2t is

2(ω1 − ω2)t.

2(ω1 + ω2)t cos 1

cos ω1t + cos ω2t = 2 cos 1

(48.6)Now let us suppose that the two frequencies are nearly the same, so that 12(ω1+ω2)is the average frequency, and is more or less the same as either. But ω1 − ω2is much smaller than ω1 or ω2 because, as we suppose, ω1 and ω2 are nearlyequal. That means that we can represent the solution by saying that there isa high-frequency cosine wave more or less like the ones we started with, butthat its「size」is slowly changing—its「size」is pulsating with a frequency which2(ω1 − ω2). But is this the frequency at which the beats areappears to be 12(ω1 − ω2)t, what itheard? Although (48.6) says that the amplitude goes as cos 1is really telling us is that the high-frequency oscillations are contained betweentwo opposed cosine curves (shown dotted in Fig. 48-1). On this basis one could2(ω1 − ω2), but if we are talkingsay that the amplitude varies at the frequency 1

48-3

about the intensity of the wave we must think of it as having twice this frequency.That is, the modulation of the amplitude, in the sense of the strength of itsintensity, is at frequency ω1 − ω2, although the formula tells us that we multiplyby a cosine wave at half that frequency. The technical basis for the diﬀerenceis that the high frequency-wave has a little diﬀerent phase relationship in thesecond half-cycle.

Ignoring this small complication, we may conclude that if we add two waves offrequency ω1 and ω2, we will get a net resulting wave of average frequency 12(ω1 +ω2) which oscillates in strength with a frequency ω1 − ω2.If the two amplitudes are diﬀerent, we can do it all over again by multiplyingthe cosines by diﬀerent amplitudes A1 and A2, and do a lot of mathematics,rearranging, and so on, using equations like (48.2)–(48.5). However, there areother, easier ways of doing the same analysis. For example, we know that itis much easier to work with exponentials than with sines and cosines and thatwe can represent A1 cos ω1t as the real part of A1eiω1t. The other wave wouldsimilarly be the real part of A2eiω2t. If we add the two, we get A1eiω1t + A2eiω2t.If we then factor out the average frequency, we have

A1eiω1t + A2eiω2t = ei(ω1+ω2)t/2[A1ei(ω1−ω2)t/2 + A2e−i(ω1−ω2)t/2].

(48.7)

Again we have the high-frequency wave with a modulation at the lower frequency.

48-2 Beat notes and modulationIf we are now asked for the intensity of the wave of Eq. (48.7), we can eithertake the absolute square of the left side, or of the right side. Let us take the leftside. The intensity then is

I = A2

1 + A2

2 + 2A1A2 cos (ω1 − ω2)t.

(48.8)We see that the intensity swells and falls at a frequency ω1 − ω2, varying betweenthe limits (A1 + A2)2 and (A1 − A2)2. If A1 6= A2, the minimum intensity is notzero.One more way to represent this idea is by means of a drawing, like Fig. 48-2.We draw a vector of length A1, rotating at a frequency ω1, to represent one ofthe waves in the complex plane. We draw another vector of length A2, goingaround at a frequency ω2, to represent the second wave. If the two frequenciesare exactly equal, their resultant is of ﬁxed length as it keeps revolving, and we

48-4

Fig. 48-2. The resultant of two complex vectors of equal frequency.

Fig. 48-3. The resultant of two complex vectors of unequal frequency,as seen in the rotating frame of reference of one vector. Nine successivepositions of the slowly rotating vector are shown.

get a deﬁnite, ﬁxed intensity from the two. But if the frequencies are slightlydiﬀerent, the two complex vectors go around at diﬀerent speeds. Figure 48-3shows what the situation looks like relative to the vector A1eiω1t. We see thatA2 is turning slowly away from A1, and so the amplitude that we get by addingthe two is ﬁrst strong, and then, as it opens out, when it gets to the 180◦ relativeposition the resultant gets particularly weak, and so on. As the vectors go around,the amplitude of the sum vector gets bigger and smaller, and the intensity thuspulsates. It is a relatively simple idea, and there are many diﬀerent ways ofrepresenting the same thing.

The eﬀect is very easy to observe experimentally. In the case of acoustics, wemay arrange two loudspeakers driven by two separate oscillators, one for eachloudspeaker, so that they each make a tone. We thus receive one note from onesource and a diﬀerent note from the other source. If we make the frequenciesexactly the same, the resulting eﬀect will have a deﬁnite strength at a given space

48-5

location. If we then de-tune them a little bit, we hear some variations in theintensity. The farther they are de-tuned, the more rapid are the variations of sound.The ear has some trouble following variations more rapid than ten or so per second.We may also see the eﬀect on an oscilloscope which simply displays the sumof the currents to the two speakers. If the frequency of pulsing is relatively low,we simply see a sinusoidal wave train whose amplitude pulsates, but as we makethe pulsations more rapid we see the kind of wave shown in Fig. 48-1. As we goto greater frequency diﬀerences, the「bumps」move closer together. Also, if theamplitudes are not equal and we make one signal stronger than the other, thenwe get a wave whose amplitude does not ever become zero, just as we expect.Everything works the way it should, both acoustically and electrically.

The opposite phenomenon occurs too! In radio transmission using so-calledamplitude modulation (am), the sound is broadcast by the radio station asfollows: the radio transmitter has an ac electric oscillation which is at a veryhigh frequency, for example 800 kilocycles per second, in the broadcast band.If this carrier signal is turned on, the radio station emits a wave which is ofuniform amplitude at 800,000 oscillations a second. The way the「information」is transmitted, the useless kind of information about what kind of car to buy, isthat when somebody talks into a microphone the amplitude of the carrier signalis changed in step with the vibrations of sound entering the microphone.

If we take as the simplest mathematical case the situation where a sopranois singing a perfect note, with perfect sinusoidal oscillations of her vocal cords,then we get a signal whose strength is alternating as shown in Fig. 48-4. Theaudiofrequency alternation is then recovered in the receiver; we get rid of thecarrier wave and just look at the envelope which represents the oscillations of thevocal cords, or the sound of the singer. The loudspeaker then makes correspondingvibrations at the same frequency in the air, and the listener is then essentially

Fig. 48-4. A modulated carrier wave.

ωc /ωm = 5. In an actual radiowave, ωc /ωm ∼ 100.

In this schematic sketch,

48-6

unable to tell the diﬀerence, so they say. Because of a number of distortions andother subtle eﬀects, it is, in fact, possible to tell whether we are listening to aradio or to a real soprano; otherwise the idea is as indicated above.

2 b cos (ωc + ωm)t + 1

2 b cos (ωc − ωm)t.

S = cos ωct + 1

S = (1 + b cos ωmt) cos ωct,

48-3 Side bandsMathematically, the modulated wave described above would be expressed as(48.9)where ωc represents the frequency of the carrier and ωm is the frequency of theaudio tone. Again we use all those theorems about the cosines, or we can use eiθ;it makes no diﬀerence—it is easier with eiθ, but it is the same thing. We then get(48.10)So, from another point of view, we can say that the output wave of the systemconsists of three waves added in superposition: ﬁrst, the regular wave at thefrequency ωc, that is, at the carrier frequency, and then two new waves at twonew frequencies. One is the carrier frequency plus the modulation frequency, andthe other is the carrier frequency minus the modulation frequency. If, therefore,we make some kind of plot of the intensity being generated by the generator asa function of frequency, we would ﬁnd a lot of intensity at the frequency of thecarrier, naturally, but when a singer started to sing, we would suddenly also ﬁndintensity proportional to the strength of the singer, b2, at frequency ωc + ωmand ωc − ωm, as shown in Fig. 48-5. These are called side bands; when there isa modulated signal from the transmitter, there are side bands. If there is morethan one note at the same time, say ωm and ωm0, there are two instruments

Fig. 48-5. The frequency spectrum of a carrier wave ωc modulated

by a single cosine wave ωm.

48-7

playing; or if there is any other complicated cosine wave, then, of course, we cansee from the mathematics that we get some more waves that correspond to thefrequencies ωc ± ωm0.Therefore, when there is a complicated modulation that can be represented asthe sum of many cosines,* we ﬁnd that the actual transmitter is transmitting overa range of frequencies, namely the carrier frequency plus or minus the maximumfrequency that the modulation signal contains.

Although at ﬁrst we might believe that a radio transmitter transmits onlyat the nominal frequency of the carrier, since there are big, superstable crystaloscillators in there, and everything is adjusted to be at precisely 800 kilocycles,the moment someone announces that they are at 800 kilocycles, he modulatesthe 800 kilocycles, and so they are no longer precisely at 800 kilocycles! Supposethat the ampliﬁers are so built that they are able to transmit over a good rangeof the ear’s sensitivity (the ear can hear up to 20,000 cycles per second, butusually radio transmitters and receivers do not work beyond 10,000, so we donot hear the highest parts), then, when the man speaks, his voice may containfrequencies ranging up, say, to 10,000 cycles, so the transmitter is transmittingfrequencies which may range from 790 to 810 kilocycles per second. Now if therewere another station at 795 kc/sec, there would be a lot of confusion. Also, if wemade our receiver so sensitive that it picked up only 800, and did not pick up the10 kilocycles on either side, we would not hear what the man was saying, becausethe information would be on these other frequencies! Therefore it is absolutelyessential to keep the stations a certain distance apart, so that their side bandsdo not overlap and, also, the receiver must not be so selective that it does notpermit reception of the side bands as well as of the main nominal frequency. Inthe case of sound, this problem does not really cause much trouble. We can hearover a ±20 kc/sec range, and we have usually from 500 to 1500 kc/sec in thebroadcast band, so there is plenty of room for lots of stations.The television problem is more diﬃcult. As the electron beam goes acrossthe face of the picture tube, there are various little spots of light and dark. That

* A slight side remark: In what circumstances can a curve be represented as a sum of a lotof cosines? Answer: In all ordinary circumstances, except for certain cases the mathematicianscan dream up. Of course, the curve must have only one value at a given point, and it mustnot be a crazy curve which jumps an inﬁnite number of times in an inﬁnitesimal distance, orsomething like that. But aside from such restrictions any reasonable curve (one that a singer isgoing to be able to make by shaking her vocal cords) can always be compounded by addingcosine waves together.

48-8

「light」and「dark」is the「signal.」Now ordinarily the beam scans over the wholepicture, 500 lines, approximately, in a thirtieth of a second. Let us considerthat the resolution of the picture vertically and horizontally is more or less thesame, so that there are the same number of spots per inch along a scan line.We want to be able to distinguish dark from light, dark from light, dark fromlight, over, say, 500 lines. In order to be able to do this with cosine waves, theshortest wavelength needed thus corresponds to a wavelength, from maximumto maximum, of one 250th of the screen size. So we have 250 × 500 × 30 piecesof information per second. The highest frequency that we are going to carry,therefore, is close to 4 megacycles per second. Actually, to keep the televisionstations apart, we have to use a little bit more than this, about 6 mc/sec; partof it is used to carry the sound signal, and other information. So, televisionchannels are 6 megacycles per second wide. It certainly would not be possibleto transmit tv on an 800 kc/sec carrier, since we cannot modulate at a higherfrequency than the carrier.

At any rate, the television band starts at 54 megacycles. The ﬁrst transmissionchannel, which is channel 2 (!), has a frequency range from 54 to 60 mc/sec,which is 6 mc/sec wide.「But,」one might say,「we have just proved that therewere side bands on both sides, and therefore it should be twice that wide.」Itturns out that the radio engineers are rather clever. If we analyze the modulationsignal using not just cosine terms, but cosine and sine terms, to allow for phasediﬀerences, we then see that there is a deﬁnite, invariant relationship betweenthe side band on the high-frequency side and the side band on the low-frequencyside. What we mean is that there is no new information on that other side band.So what is done is to suppress one side band, and the receiver is wired insidesuch that the information which is missing is reconstituted by looking at thesingle side band and the carrier. Single side-band transmission is a clever schemefor decreasing the band widths needed to transmit information.

48-4 Localized wave trainsThe next subject we shall discuss is the interference of waves in both spaceand time. Suppose that we have two waves travelling in space. We know, ofcourse, that we can represent a wave travelling in space by ei(ωt−kx). This mightbe, for example, the displacement in a sound wave. This is a solution of thewave equation provided that ω2 = k2c2, where c is the speed of propagation ofthe wave. In this case we can write it as e−ik(x−ct), which is of the general form

48-9

f(x − ct). Therefore this must be a wave which is travelling at this velocity, ω/k,and that is c and everything is all right.Now we want to add two such waves together. Suppose we have a wave that istravelling with one frequency, and another wave travelling with another frequency.We leave to the reader to consider the case where the amplitudes are diﬀerent; itmakes no real diﬀerence. Thus we want to add ei(ω1t−k1x) + ei(ω2t−k2x). We canadd these by the same kind of mathematics we used when we added signal waves.Of course, if c is the same for both, this is easy, since it is the same as what wedid before:(48.11)except that t0 = t − x/c is the variable instead of t. So we get the same kind ofmodulations, naturally, but we see, of course, that those modulations are movingalong with the wave. In other words, if we added two waves, but these waveswere not just oscillating, but also moving in space, then the resultant wave wouldmove along also, at the same speed.

eiω1(t−x/c) + eiω2(t−x/c) = eiω1t0 + eiω2t0

Now we would like to generalize this to the case of waves in which therelationship between the frequency and the wave number k is not so simple.Example: material having an index of refraction. We have already studied thetheory of the index of refraction in Chapter 31, where we found that we couldwrite k = nω/c, where n is the index of refraction. As an interesting example,for x-rays we found that the index n is

,

n = 1 − N q2

e

20mω2 .

(48.12)

We actually derived a more complicated formula in Chapter 31, but this one isas good as any, as an example.

Incidentally, we know that even when ω and k are not linearly proportional,the ratio ω/k is certainly the speed of propagation for the particular frequencyand wave number. We call this ratio the phase velocity; it is the speed at whichthe phase, or the nodes of a single wave, would move along:

vp = ωk

.

(48.13)

This phase velocity, for the case of x-rays in glass, is greater than the speed oflight in vacuum (since n in 48.12 is less than 1), and that is a bit bothersome,because we do not think we can send signals faster than the speed of light!

48-10

What we are going to discuss now is the interference of two waves in which ωand k have a deﬁnite formula relating them. The above formula for n says thatk is given as a deﬁnite function of ω. To be speciﬁc, in this particular problem,the formula for k in terms of ω is

k = ωc

− aωc

,

(48.14)

where a = N q2deﬁnite wave number, and we want to add two such waves together.

e /20m, a constant. At any rate, for each frequency there is a

Let us do it just as we did in Eq. (48.7):ei(ω1t−k1x) + ei(ω2t−k2x) = ei[(ω1+ω2)t−(k1+k2)x]/2

× {ei[(ω1−ω2)t−(k1−k2)x]/2 + e−i[(ω1−ω2)t−(k1−k2)x]/2}.

(48.15)

So we have a modulated wave again, a wave which travels with the mean frequencyand the mean wave number, but whose strength is varying with a form whichdepends on the diﬀerence frequency and the diﬀerence wave number.

Now let us take the case that the diﬀerence between the two waves is relativelysmall. Let us suppose that we are adding two waves whose frequencies are nearlyequal; then (ω1 + ω2)/2 is practically the same as either one of the ω’s, andsimilarly for (k1 + k2)/2. Thus the speed of the wave, the fast oscillations,the nodes, is still essentially ω/k. But look, the speed of propagation of themodulation is not the same! How much do we have to change x to account for acertain amount of t? The speed of this modulation wave is the ratio

vM = ω1 − ω2k1 − k2

.

(48.16)

The speed of modulation is sometimes called the group velocity. If we take thecase that the diﬀerence in frequency is relatively small, and the diﬀerence inwave number is then also relatively small, then this expression approaches, inthe limit,

vg = dωdk

.

(48.17)

In other words, for the slowest modulation, the slowest beats, there is a deﬁnitespeed at which they travel which is not the same as the phase speed of thewaves—what a mysterious thing!

48-11

The group velocity is the derivative of ω with respect to k, and the phasevelocity is ω/k.

Let us see if we can understand why. Consider two waves, again of slightlydiﬀerent wavelength, as in Fig. 48-1. They are out of phase, in phase, out ofphase, and so on. Now these waves represent, really, the waves in space travellingwith slightly diﬀerent frequencies also. Now because the phase velocity, thevelocity of the nodes of these two waves, is not precisely the same, somethingnew happens. Suppose we ride along with one of the waves and look at the otherone; if they both went at the same speed, then the other wave would stay rightwhere it was relative to us, as we ride along on this crest. We ride on that crestand right opposite us we see a crest; if the two velocities are equal the crests stayon top of each other. But it is not so that the two velocities are really equal.There is only a small diﬀerence in frequency and therefore only a small diﬀerencein velocity, but because of that diﬀerence in velocity, as we ride along the otherwave moves slowly forward, say, or behind, relative to our wave. So as time goeson, what happens to the node? If we move one wave train just a shade forward,the node moves forward (or backward) a considerable distance. That is, the sumof these two waves has an envelope, and as the waves travel along, the enveloperides on them at a diﬀerent speed. The group velocity is the speed at whichmodulated signals would be transmitted.If we made a signal, i.e., some kind of change in the wave that one couldrecognize when he listened to it, a kind of modulation, then that modulationwould travel at the group velocity, provided that the modulations were relativelyslow. (When they are fast, it is much more diﬃcult to analyze.)

Now we may show (at long last), that the speed of propagation of x-rays in ablock of carbon is not greater than the speed of light, although the phase velocityis greater than the speed of light. In order to do that, we must ﬁnd dω/dk, whichwe get by diﬀerentiating (48.14): dk/dω = 1/c + a/ω2c. The group velocity,therefore, is the reciprocal of this, namely,c

which is smaller than c! So although the phases can travel faster than the speedof light, the modulation signals travel slower, and that is the resolution of theapparent paradox! Of course, if we have the simple case that ω = kc, then dω/dkis also c. So when all the phases have the same velocity, naturally the group hasthe same velocity.

vg =

1 + a/ω2 ,

(48.18)

48-12

48-5 Probability amplitudes for particlesLet us now consider one more example of the phase velocity which is extremelyinteresting. It has to do with quantum mechanics. We know that the amplitudeto ﬁnd a particle at a place can, in some circumstances, vary in space and time,let us say in one dimension, in this manner:

ψ = Aei(ωt−kx),

(48.19)where ω is the frequency, which is related to the classical idea of the energythrough E = ω, and k is the wave number, which is related to the momentumthrough p = k. We would say the particle had a deﬁnite momentum p if thewave number were exactly k, that is, a perfect wave which goes on with thesame amplitude everywhere. Equation (48.19) gives the amplitude, and if wetake the absolute square, we get the relative probability for ﬁnding the particleas a function of position and time. This is a constant, which means that theprobability is the same to ﬁnd a particle anywhere. Now suppose, instead, thatwe have a situation where we know that the particle is more likely to be at oneplace than at another. We would represent such a situation by a wave which hasa maximum and dies out on either side (Fig. 48-6). (It is not quite the same as awave like (48.1) which has a series of maxima, but it is possible, by adding severalwaves of nearly the same ω and k together, to get rid of all but one maximum.)

Fig. 48-6. A localized wave train.

Now in those circumstances, since the square of (48.19) represents the chanceof ﬁnding a particle somewhere, we know that at a given instant the particleis most likely to be near the center of the「lump,」where the amplitude of thewave is maximum. If now we wait a few moments, the waves will move, andafter some time the「lump」will be somewhere else. If we knew that the particleoriginally was situated somewhere, classically, we would expect that it wouldlater be elsewhere as a matter of fact, because it has a speed, after all, and a

48-13

momentum. The quantum theory, then, will go into the correct classical theoryfor the relationship of momentum, energy, and velocity only if the group velocity,the velocity of the modulation, is equal to the velocity that we would obtainclassically for a particle of the same momentum.

It is now necessary to demonstrate that this is, or is not, the case. Accordingto the classical theory, the energy is related to the velocity through an equationlike

(48.20)

(48.21)

Similarly, the momentum is

E =

p =

mc2p1 − v2/c2 .mvp1 − v2/c2 .

That is the classical theory, and as a consequence of the classical theory, byeliminating v, we can show that

E2 − p2c2 = m2c4.

That is the four-dimensional grand result that we have talked and talked about,that pµpµ = m2; that is the relation between energy and momentum in theclassical theory. Now that means, since these E’s and p’s are going to becomeω’s and k’s, by substitution of E = ω and p = k, that for quantum mechanicsit is necessary that

(48.22)This, then, is the relationship between the frequency and the wave number of aquantum-mechanical amplitude wave representing a particle of mass m. Fromthis equation we can deduce that ω is

2ω2c2 − 2k2 = m2c2.ω = cpk2 + m2c2/2.

The phase velocity, ω/k, is here again faster than the speed of light!Now let us look at the group velocity. The group velocity should be dω/dk,the speed at which the modulations move. We have to diﬀerentiate a square root,which is not very diﬃcult. The derivative is

pk2 + m2c2/2 .

kc

=

dωdk

48-14

Now the square root is, after all, ω/c, so we could write this as dω/dk = c2k/ω.Further, k/ω is p/E, so

vg = c2p

.

E

But from (48.20) and (48.21), c2p/E = v, the velocity of the particle, according toclassical mechanics. So we see that whereas the fundamental quantum-mechanicalrelationship E = ω and p = k, for the identiﬁcation of ω and k with the classicalE and p, only produces the equation ω2−k2c2 = m2c4/2, now we also understandthe relationships (48.20) and (48.21) which connected E and p to the velocity. Ofcourse the group velocity must be the velocity of the particle if the interpretationis going to make any sense. If we think the particle is over here at one time,and then ten minutes later we think it is over there, as the quantum mechanicssaid, the distance traversed by the「lump,」divided by the time interval, mustbe, classically, the velocity of the particle.

48-6 Waves in three dimensionsWe shall now bring our discussion of waves to a close with a few generalremarks about the wave equation. These remarks are intended to give someview of the future—not that we can understand everything exactly just now, butrather to see what things are going to look like when we study waves a littlemore. First of all, the wave equation for sound in one dimension was

∂2χ∂x2

= 1c2

∂2χ∂t2 ,

where c is the speed of whatever the wave is—in the case of sound, it is the soundspeed; in the case of light, it is the speed of light. We showed that for a soundwave the displacements would propagate themselves at a certain speed. Butthe excess pressure also propagates at a certain speed, and so does the excessdensity. So we should expect that the pressure would satisfy the same equation,as indeed it does. We shall leave it to the reader to prove that it does. Hint:ρe is proportional to the rate of change of χ with respect to x. Therefore if wediﬀerentiate the wave equation with respect to x, we will immediately discoverthat ∂χ/∂x satisﬁes the same equation. That is to say, ρe satisﬁes the sameequation. But Pe is proportional to ρe, and therefore Pe does too. So the pressure,the displacements, everything, satisfy the same wave equation.

48-15

Usually one sees the wave equation for sound written in terms of pressureinstead of in terms of displacement, because the pressure is a scalar and has nodirection. But the displacement is a vector and has direction, and it is thus easierto analyze the pressure.

The next matter we discuss has to do with the wave equation in threedimensions. We know that the sound wave solution in one dimension is ei(ωt−kx),with ω = kcs, but we also know that in three dimensions a wave would berepresented by ei(ωt−kxx−kyy−kzz), where, in this case, ω2 = k2cs, which is, ofcourse, (k2. Now what we want to do is to guess what the correctwave equation in three dimensions is. Naturally, for the case of sound this can bededuced by going through the same dynamic argument in three dimensions thatwe made in one dimension. But we shall not do that; instead we just write downwhat comes out: the equation for the pressure (or displacement, or anything) is

+ k2

+ k2

)c2

x

y

z

s

∂2Pe∂x2

+ ∂2Pe∂y2

+ ∂2Pe∂z2

= 1c2s

∂2Pe∂t2 .

(48.23)

x

zPe. On the right, we get −(ω2/c2

, so the ﬁrst term would become −k2

That this is true can be veriﬁed by substituting in ei(ωt−k·r). Clearly, every timewe diﬀerentiate with respect to x, we multiply by −ikx. If we diﬀerentiate twice,it is equivalent to multiplying by −k2xPe,for that wave. Similarly, the second term becomes −k2yPe, and the third termbecomes −k2)Pe. Then, if we take away the Pe’sand change the sign, we see that the relationship between k and ω is the onethat we want.Working backwards again, we cannot resist writing down the grand equationwhich corresponds to the dispersion equation (48.22) for quantum-mechanicalwaves. If φ represents the amplitude for ﬁnding a particle at position x, y, z, atthe time t, then the great equation of quantum mechanics for free particles isthis:

s

∂2φ∂x2

+ ∂2φ∂y2

∂z2 − 1+ ∂2φ

c2

∂2φ∂t2

= m2c2

2 φ.

(48.24)

First of all, the relativity character of this expression is suggested by the ap-pearance of x, y, z and t in the nice combination relativity usually involves.Second, it is a wave equation which, if we try a plane wave, would produce asa consequence that −k2 + ω2/c2 = m2c2/2, which is the right relationship forquantum mechanics. There is still another great thing contained in the waveequation: the fact that any superposition of waves is also a solution. So this

48-16

equation contains all of the quantum mechanics and the relativity that we havebeen discussing so far, at least so long as it deals with a single particle in emptyspace with no external potentials or forces on it!

48-7 Normal modesNow we turn to another example of the phenomenon of beats which is rathercurious and a little diﬀerent. Imagine two equal pendulums which have, betweenthem, a rather weak spring connection. They are made as nearly as possible thesame length. If we pull one aside and let go, it moves back and forth, and it pullson the connecting spring as it moves back and forth, and so it really is a machinefor generating a force which has the natural frequency of the other pendulum.Therefore, as a consequence of the theory of resonance, which we studied before,when we put a force on something at just the right frequency, it will drive it. So,sure enough, one pendulum moving back and forth drives the other. However, inthis circumstance there is a new thing happening, because the total energy of thesystem is ﬁnite, so when one pendulum pours its energy into the other to driveit, it ﬁnds itself gradually losing energy, until, if the timing is just right alongwith the speed, it loses all its energy and is reduced to a stationary condition!Then, of course, it is the other pendulum ball that has all the energy and theﬁrst one which has none, and as time goes on we see that it works also in theopposite direction, and that the energy is passed back into the ﬁrst ball; this is avery interesting and amusing phenomenon. We said, however, that this is relatedto the theory of beats, and we must now explain how we can analyze this motionfrom the point of view of the theory of beats.

We note that the motion of either of the two balls is an oscillation which hasan amplitude which changes cyclically. Therefore the motion of one of the balls ispresumably analyzable in a diﬀerent way, in that it is the sum of two oscillations,present at the same time but having two slightly diﬀerent frequencies. Thereforeit ought to be possible to ﬁnd two other motions in this system, and to claimthat what we saw was a superposition of the two solutions, because this is ofcourse a linear system. Indeed, it is easy to ﬁnd two ways that we could startthe motion, each one of which is a perfect, single-frequency motion—absolutelyperiodic. The motion that we started with before was not strictly periodic, sinceit did not last; soon one ball was passing energy to the other and so changing itsamplitude; but there are ways of starting the motion so that nothing changes and,of course, as soon as we see it we understand why. For example, if we made both

48-17

pendulums go together, then, since they are of the same length and the spring isnot then doing anything, they will of course continue to swing like that for alltime, assuming no friction and that everything is perfect. On the other hand,there is another possible motion which also has a deﬁnite frequency: that is, ifwe move the pendulums oppositely, pulling them aside exactly equal distances,then again they would be in absolutely periodic motion. We can appreciate thatthe spring just adds a little to the restoring force that the gravity supplies, thatis all, and the system just keeps oscillating at a slightly higher frequency thanin the ﬁrst case. Why higher? Because the spring is pulling, in addition to thegravitation, and it makes the system a little「stiﬀer,」so that the frequency ofthis motion is just a shade higher than that of the other.

Thus this system has two ways in which it can oscillate with unchangingamplitude: it can either oscillate in a manner in which both pendulums go thesame way and oscillate all the time at one frequency, or they could go in oppositedirections at a slightly higher frequency.

Now the actual motion of the thing, because the system is linear, can berepresented as a superposition of the two. (The subject of this chapter, remember,is the eﬀects of adding two motions with diﬀerent frequencies.) So think whatwould happen if we combined these two solutions. If at t = 0 the two motionsare started with equal amplitude and in the same phase, the sum of the twomotions means that one ball, having been impressed one way by the ﬁrst motionand the other way by the second motion, is at zero, while the other ball, havingbeen displaced the same way in both motions, has a large amplitude. As timegoes on, however, the two basic motions proceed independently, so the phaseof one relative to the other is slowly shifting. That means, then, that after asuﬃciently long time, when the time is enough that one motion could have gone「900 12」oscillations, while the other went only「900,」the relative phase would bejust reversed with respect to what it was before. That is, the large-amplitudemotion will have fallen to zero, and in the meantime, of course, the initiallymotionless ball will have attained full strength!

So we see that we could analyze this complicated motion either by the ideathat there is a resonance and that one passes energy to the other, or else by thesuperposition of two constant-amplitude motions at two diﬀerent frequencies.

48-18

49

