Relativistic Effects in Radiation

34-1 Moving sourcesIn the present chapter we shall describe a number of miscellaneous eﬀectsin connection with radiation, and then we shall be ﬁnished with the classicaltheory of light propagation. In our analysis of light, we have gone rather far andinto considerable detail. The only phenomena of any consequence associatedwith electromagnetic radiation that we have not discussed is what happens ifradiowaves are contained in a box with reﬂecting walls, the size of the boxbeing comparable to a wavelength, or are transmitted down a long tube. Thephenomena of so-called cavity resonators and waveguides we shall discuss later;we shall ﬁrst use another physical example—sound—and then we shall return tothis subject. Except for this, the present chapter is our last consideration of theclassical theory of light.

We can summarize all the eﬀects that we shall now discuss by remarking thatthey have to do with the eﬀects of moving sources. We no longer assume thatthe source is localized, with all its motion being at a relatively low speed near aﬁxed point.

We recall that the fundamental laws of electrodynamics say that, at large

distances from a moving charge, the electric ﬁeld is given by the formula

E = − q

4π0c2

d2eR0dt2 .

(34.1)

The second derivative of the unit vector eR0 which points in the apparent directionof the charge, is the determining feature of the electric ﬁeld. This unit vectordoes not point toward the present position of the charge, of course, but rather inthe direction that the charge would seem to be, if the information travels only atthe ﬁnite speed c from the charge to the observer.

34-1

Associated with the electric ﬁeld is a magnetic ﬁeld, always at right anglesto the electric ﬁeld and at right angles to the apparent direction of the source,given by the formula

B = −eR0 × E/c.

(34.2)

Until now we have considered only the case in which motions are nonrelativisticin speed, so that there is no appreciable motion in the direction of the sourceto be considered. Now we shall be more general and study the case where themotion is at an arbitrary velocity, and see what diﬀerent eﬀects may be expectedin those circumstances. We shall let the motion be at an arbitrary speed, but ofcourse we shall still assume that the detector is very far from the source.

Fig. 34-1. The path of a moving charge. The true position at the

time τ is at T , but the retarded position is at A.

We already know from our discussion in Chapter 28 that the only things thatcount in d2eR0/dt2 are the changes in the direction of eR0. Let the coordinatesof the charge be (x, y, z), with z measured along the direction of observation(Fig. 34-1). At a given moment in time, say the moment τ, the three componentsof the position are x(τ), y(τ), and z(τ). The distance R is very nearly equalto R(τ) = R0 + z(τ). Now the direction of the vector eR0 depends mainly on xand y, but hardly at all upon z: the transverse components of the unit vector arex/R and y/R, and when we diﬀerentiate these components we get things like R2in the denominator:

d(x/R)

dt

= dx/dt

R

− dzdt

xR2 .

So, when we are far enough away the only terms we have to worry about are the

34-2

variations of x and y. Thus we take out the factor R0 and get

Ex = −

q

4π0c2R0

Ey = −

q

4π0c2R0

d2x0dt2 ,d2y0dt2 ,

(34.3)

where R0 is the distance, more or less, to q; let us take it as the distance OP to theorigin of the coordinates (x, y, z). Thus the electric ﬁeld is a constant multipliedby a very simple thing, the second derivatives of the x- and y-coordinates. (Wecould put it more mathematically by calling x and y the transverse componentsof the position vector r of the charge, but this would not add to the clarity.)

Of course, we realize that the coordinates must be measured at the retardedtime. Here we ﬁnd that z(τ) does aﬀect the retardation. What time is theretarded time? If the time of observation is called t (the time at P) then thetime τ to which this corresponds at A is not the time t, but is delayed by thetotal distance that the light has to go, divided by the speed of light. In theﬁrst approximation, this delay is R0/c, a constant (an uninteresting feature),but in the next approximation we must include the eﬀects of the position in thez-direction at the time τ, because if q is a little farther back, there is a littlemore retardation. This is an eﬀect that we have neglected before, and it is theonly change needed in order to make our results valid for all speeds.

What we must now do is to choose a certain value of t and calculate the valueof τ from it, and thus ﬁnd out where x and y are at that τ. These are then theretarded x and y, which we call x0 and y0, whose second derivatives determinethe ﬁeld. Thus τ is determined by

and

t = τ + R0c

x0(t) = x(τ),

+ z(τ)y0(t) = y(τ).

c

(34.4)

Now these are complicated equations, but it is easy enough to make a geometricalpicture to describe their solution. This picture will give us a good qualitativefeeling for how things work, but it still takes a lot of detailed mathematics todeduce the precise results of a complicated problem.

34-3

Fig. 34-2. A geometrical solution of Eq. (34.5) to ﬁnd x(cid:48)(t).

34-2 Finding the「apparent」motionThe above equation has an interesting simpliﬁcation. If we disregard theuninteresting constant delay R0/c, which just means that we must change theorigin of t by a constant, then it says that

ct = cτ + z(τ),

x0 = x(τ),

y0 = y(τ).

(34.5)

Now we need to ﬁnd x0 and y0 as functions of t, not τ, and we can do this inthe following way: Eq. (34.5) says that we should take the actual motion andadd a constant (the speed of light) times τ. What that turns out to mean isshown in Fig. 34-2. We take the actual motion of the charge (shown at left) andimagine that as it is going around it is being swept away from the point P atthe speed c (there are no contractions from relativity or anything like that; thisis just a mathematical addition of the cτ). In this way we get a new motion,in which the line-of-sight coordinate is ct, as shown at the right. (The ﬁgureshows the result for a rather complicated motion in a plane, but of course themotion may not be in one plane—it may be even more complicated than motionin a plane.) The point is that the horizontal (i.e., line-of-sight) distance now isno longer the old z, but is z + cτ, and therefore is ct. Thus we have found apicture of the curve, x0 (and y0) against t! All we have to do to ﬁnd the ﬁeldis to look at the acceleration of this curve, i.e., to diﬀerentiate it twice. So theﬁnal answer is: in order to ﬁnd the electric ﬁeld for a moving charge, take themotion of the charge and translate it back at the speed c to「open it out」; thenthe curve, so drawn, is a curve of the x0 and y0 positions of the function of t. Theacceleration of this curve gives the electric ﬁeld as a function of t. Or, if we wish,we can now imagine that this whole「rigid」curve moves forward at the speed

34-4

Fig. 34-3. The x(cid:48)(t) curve for a particle moving at constant speed v =

0.94c in a circle.

c through the plane of sight, so that the point of intersection with the plane ofsight has the coordinates x0 and y0. The acceleration of this point makes theelectric ﬁeld. This solution is just as exact as the formula we started with—it issimply a geometrical representation.

If the motion is relatively slow, for instance if we have an oscillator just goingup and down slowly, then when we shoot that motion away at the speed of light,we would get, of course, a simple cosine curve, and that gives a formula we havebeen looking at for a long time: it gives the ﬁeld produced by an oscillating charge.A more interesting example is an electron moving rapidly, very nearly at thespeed of light, in a circle. If we look in the plane of the circle, the retarded x0(t)appears as shown in Fig. 34-3. What is this curve? If we imagine a radius vectorfrom the center of the circle to the charge, and if we extend this radial line alittle bit past the charge, just a shade if it is going fast, then we come to a pointon the line that goes at the speed of light. Therefore, when we translate themotion back at the speed of light, that corresponds to having a wheel with acharge on it rolling backward (without slipping) at the speed c; thus we ﬁnd acurve which is very close to a cycloid—it is called a curtate cycloid. If the chargeis going very nearly at the speed of light, the「cusps」are very sharp indeed; if itwent at exactly the speed of light, they would be actual cusps, inﬁnitely sharp.「Inﬁnitely sharp」is interesting; it means that near a cusp the second derivativeis enormous. Once in each cycle we get a sharp pulse of electric ﬁeld. This isnot at all what we would get from a nonrelativistic motion, where each time thecharge goes around there is an oscillation which is of about the same「strength」all the time. Instead, there are very sharp pulses of electric ﬁeld spaced at timeintervals T0 apart, where T0 is the period of revolution. These strong electric

34-5

ﬁelds are emitted in a narrow cone in the direction of motion of the charge. Whenthe charge is moving away from P, there is very little curvature and there is verylittle radiated ﬁeld in the direction of P.

34-3 Synchrotron radiationWe have very fast electrons moving in circular paths in the synchrotron; theyare travelling at very nearly the speed c, and it is possible to see the aboveradiation as actual light! Let us discuss this in more detail.

In the synchrotron we have electrons which go around in circles in a uniformmagnetic ﬁeld. First, let us see why they go in circles. From Eq. (28.2), we knowthat the force on a particle in a magnetic ﬁeld is given by

F = qv × B,

(34.6)

and it is at right angles both to the ﬁeld and to the velocity. As usual, the force isequal to the rate of change of momentum with time. If the ﬁeld is directed upwardout of the paper, the momentum of the particle and the force on it are as shown inFig. 34-4. Since the force is at right angles to the velocity, the kinetic energy, andtherefore the speed, remains constant. All the magnetic ﬁeld does is to changethe direction of motion. In a short time ∆t, the momentum vector changes atright angles to itself by an amount ∆p = F ∆t, and therefore p turns throughan angle ∆θ = ∆p/p = qvB ∆t/p, since |F| = qvB. But in this same time theparticle has gone a distance ∆s = v ∆t. Evidently, the two lines AB and CD willintersect at a point O such that OA = OC = R, where ∆s = R ∆θ. Combining

Fig. 34-4. A charged particle moves in a circular (or helical) path in a

uniform magnetic ﬁeld.

34-6

this with the previous expressions, we ﬁnd R ∆θ/∆t = Rω = v = qvBR/p, fromwhich we ﬁnd(34.7)

p = qBR

and

ω = qvB/p.

(34.8)

Since this same argument can be applied during the next instant, the next, andso on, we conclude that the particle must be moving in a circle of radius R, withangular velocity ω.The result that the momentum of the particle is equal to a charge times theradius times the magnetic ﬁeld is a very important law that is used a great deal.It is important for practical purposes because if we have elementary particleswhich all have the same charge and we observe them in a magnetic ﬁeld, wecan measure the radii of curvature of their orbits and, knowing the magneticﬁeld, thus determine the momenta of the particles. If we multiply both sides ofEq. (34.7) by c, and express q in terms of the electronic charge, we can measurethe momentum in units of the electron volt. In those units our formula is

pc(eV) = 3 × 108(q/qe)BR,

(34.9)where B, R, and the speed of light are all expressed in the mks system, the latterbeing 3 × 108, numerically.The mks unit of magnetic ﬁeld is called a weber per square meter. There isan older unit which is still in common use, called a gauss. One weber/m2 isequal to 104 gauss. To give an idea of how big magnetic ﬁelds are, the strongestmagnetic ﬁeld that one can usually make in iron is about 1.5× 104 gauss; beyondthat, the advantage of using iron disappears. Today, electromagnets woundwith superconducting wire are able to produce steady ﬁelds of over 105 gaussstrength—that is, 10 mks units. The ﬁeld of the earth is a few tenths of a gaussat the equator.

Returning to Eq. (34.9), we could imagine the synchrotron running at a billionelectron volts, so pc would be 109 for a billion electron volts. (We shall comeback to the energy in just a moment.) Then, if we had a B corresponding to, say,10,000 gauss, which is a good substantial ﬁeld, one mks unit, then we see that Rwould have to be 3.3 meters. The actual radius of the Caltech synchrotron is3.7 meters, the ﬁeld is a little bigger, and the energy is 1.5 billion, but it is thesame idea. So now we have a feeling for why the synchrotron has the size it has.

34-7

including the rest energy, is given by W =pp2c2 + m2c4, and for an electron

We have calculated the momentum, but we know that the total energy,the rest energy corresponding to mc2 is 0.511 × 106 eV, so when pc is 109 eVwe can neglect mc2, and so for all practical purposes W = pc when the speedsare relativistic. It is practically the same to say the energy of an electron is abillion electron volts as to say the momentum times c is a billion electron volts.If W = 109 eV, it is easy to show that the speed diﬀers from the speed of lightby but one part in eight million!We turn now to the radiation emitted by such a particle. A particle movingon a circle of radius 3.3 meters, or 20 meters circumference, goes around oncein roughly the time it takes light to go 20 meters. So the wavelength thatshould be emitted by such a particle would be 20 meters—in the shortwaveradio region. But because of the piling up eﬀect that we have been discussing(Fig. 34-3), and because the distance by which we must extend the radius toreach the speed c is only one part in eight million of the radius, the cusps of thecurtate cycloid are enormously sharp compared with the distance between them.The acceleration, which involves a second derivative with respect to time, getstwice the「compression factor」of 8 × 106 because the time scale is reduced byeight million twice in the neighborhood of the cusp. Thus we might expect theeﬀective wavelength to be much shorter, to the extent of 64 times 1012 smallerthan 20 meters, and that corresponds to the x-ray region. (Actually, the cuspitself is not the entire determining factor; one must also include a certain regionabout the cusp. This changes the factor to the 3/2 power instead of the square,but still leaves us above the optical region.) Thus, even though a slowly movingelectron would have radiated 20-meter radiowaves, the relativistic eﬀect cutsdown the wavelength so much that we can see it! Clearly, the light should bepolarized, with the electric ﬁeld perpendicular to the uniform magnetic ﬁeld.To further appreciate what we would observe, suppose that we were to takesuch light (to simplify things, because these pulses are so far apart in time, weshall just take one pulse) and direct it onto a diﬀraction grating, which is a lotof scattering wires. After this pulse comes away from the grating, what do wesee? (We should see red light, blue light, and so on, if we see any light at all.)What do we see? The pulse strikes the grating head-on, and all the oscillatorsin the grating, together, are violently moved up and then back down again, justonce. They then produce eﬀects in various directions, as shown in Fig. 34-5. Butthe point P is closer to one end of the grating than to the other, so at this pointthe electric ﬁeld arrives ﬁrst from wire A, next from B, and so on; ﬁnally, the

34-8

Fig. 34-5. The light which strikes a grating as a single, sharp pulse is

scattered in various directions as diﬀerent colors.

pulse from the last wire arrives. In short, the sum of the reﬂections from all thesuccessive wires is as shown in Fig. 34-6(a); it is an electric ﬁeld which is a seriesof pulses, and it is very like a sine wave whose wavelength is the distance betweenthe pulses, just as it would be for monochromatic light striking the grating! So,we get colored light all right. But, by the same argument, will we not get lightfrom any kind of a「pulse」? No. Suppose that the curve were much smoother;then we would add all the scattered waves together, separated by a small timebetween them (Fig. 34-6b). Then we see that the ﬁeld would not shake at all,it would be a very smooth curve, because each pulse does not vary much in thetime interval between pulses.

Fig. 34-6. The total electric ﬁeld due to a series of (a) sharp pulses

and (b) smooth pulses.

The electromagnetic radiation emitted by relativistic charged particles cir-culating in a magnetic ﬁeld is called synchrotron radiation. It is so named forobvious reasons, but it is not limited speciﬁcally to synchrotrons, or even toearthbound laboratories. It is exciting and interesting that it also occurs innature!

34-9

Fig. 34-7. The crab nebula as seen in all colors (no ﬁlter).

34-4 Cosmic synchrotron radiationIn the year 1054 the Chinese and Japanese civilizations were among the mostadvanced in the world; they were conscious of the external universe, and theyrecorded, most remarkably, an explosive bright star in that year. (It is amazingthat none of the European monks, writing all the books of the middle ages, evenbothered to write that a star exploded in the sky, but they did not.) Today wemay take a picture of that star, and what we see is shown in Fig. 34-7. On theoutside is a big mass of red ﬁlaments, which is produced by the atoms of the thingas「ringing」at their natural frequencies; this makes a bright line spectrum withdiﬀerent frequencies in it. The red happens in this case to be due to nitrogen.On the other hand, in the central region is a mysterious, fuzzy patch of lightin a continuous distribution of frequency, i.e., there are no special frequenciesassociated with particular atoms. Yet this is not dust「lit up」by nearby stars,which is one way by which one can get a continuous spectrum. We can see starsthrough it, so it is transparent, but it is emitting light.

34-10

Fig. 34-8. The crab nebula as seen through a blue ﬁlter and a polaroid.

(a) Electric vector vertical. (b) Electric vector horizontal.

In Fig. 34-8 we look at the same object, using light in a region of the spectrumwhich has no bright spectral line, so that we see only the central region. Butin this case, also, polarizers have been put on the telescope, and the two viewscorrespond to two orientations 90◦ apart. We see that the pictures are diﬀerent!That is to say, the light is polarized. The reason, presumably, is that there is alocal magnetic ﬁeld, and many very energetic electrons are going around in thatmagnetic ﬁeld.

We have just illustrated how the electrons could go around the ﬁeld in a circle.We can add to this, of course, any uniform motion in the direction of the ﬁeld,since the force, qv × B, has no component in this direction and, as we havealready remarked, the synchrotron radiation is evidently polarized in a directionat right angles to the projection of the magnetic ﬁeld onto the plane of sight.

Putting these two facts together, we see that in a region where one picture isbright and the other one is black, the light must have its electric ﬁeld completelypolarized in one direction. This means that there is a magnetic ﬁeld at rightangles to this direction, while in other regions, where there is a strong emission inthe other picture, the magnetic ﬁeld must be the other way. If we look carefullyat Fig. 34-8, we may notice that there is, roughly speaking, a general set of「lines」that go one way in one picture and at right angles to this in the other.The pictures show a kind of ﬁbrous structure. Presumably, the magnetic ﬁeldlines will tend to extend relatively long distances in their own direction, and

34-11

so, presumably, there are long regions of magnetic ﬁeld with all the electronsspiralling one way, while in another region the ﬁeld is the other way and theelectrons are also spiralling that way.

What keeps the electron energy so high for so long a time? After all, itis 900 years since the explosion—how can they keep going so fast? How theymaintain their energy and how this whole thing keeps going is still not thoroughlyunderstood.

34-5 BremsstrahlungWe shall next remark brieﬂy on one other interesting eﬀect of a very fast-moving particle that radiates energy. The idea is very similar to the one we havejust discussed. Suppose that there are charged particles in a piece of matter anda very fast electron, say, comes by (Fig. 34-9). Then, because of the electric ﬁeldaround the atomic nucleus the electron is pulled, accelerated, so that the curveof its motion has a slight kink or bend in it. If the electron is travelling at verynearly the speed of light, what is the electric ﬁeld produced in the direction C?Remember our rule: we take the actual motion, translate it backwards at speed c,and that gives us a curve whose curvature measures the electric ﬁeld. It wascoming toward us at the speed v, so we get a backward motion, with the wholepicture compressed into a smaller distance in proportion as c − v is smaller thanc. So, if 1 − v/c (cid:28) 1, there is a very sharp and rapid curvature at B0, and whenwe take the second derivative of that we get a very high ﬁeld in the directionof the motion. So when very energetic electrons move through matter they spitradiation in a forward direction. This is called bremsstrahlung. As a matter offact, the synchrotron is used, not so much to make high-energy electrons (actuallyif we could get them out of the machine more conveniently we would not saythis) as to make very energetic photons—gamma rays—by passing the energetic

Fig. 34-9. A fast electron passing near a nucleus radiates energy in

the direction of its motion.

34-12

electrons through a solid tungsten「target,」and letting them radiate photonsfrom this bremsstrahlung eﬀect.

34-6 The Doppler eﬀectNow we go on to consider some other examples of the eﬀects of moving sources.Let us suppose that the source is a stationary atom which is oscillating at oneof its natural frequencies, ω0. Then we know that the frequency of the lightwe would observe is ω0. But now let us take another example, in which wehave a similar oscillator oscillating with a frequency ω1, and at the same timethe whole atom, the whole oscillator, is moving along in a direction toward theobserver at velocity v. Then the actual motion in space, of course, is as shown inFig. 34-10(a). Now we play our usual game, we add cτ; that is to say, we translatethe whole curve backward and we ﬁnd then that it oscillates as in Fig. 34-10(b).In a given amount of time τ, when the oscillator would have gone a distance vτ,on the x0 vs. ct diagram it goes a distance (c − v)τ. So all the oscillations offrequency ω1 in the time ∆τ are now found in the interval ∆t = (1 − v/c) ∆τ;they are squashed together, and as this curve comes by us at speed c, we will seelight of a higher frequency, higher by just the compression factor (1 − v/c). Thuswe observe

ω = ω1

1 − v/c

.

(34.10)

We can, of course, analyze this situation in various other ways. Suppose thatthe atom were emitting, instead of sine waves, a series of pulses, pip, pip, pip,pip, at a certain frequency ω1. At what frequency would they be received byus? The ﬁrst one that arrives has a certain delay, but the next one is delayedless because in the meantime the atom moves closer to the receiver. Therefore,the time between the「pips」is decreased by the motion.If we analyze the

Fig. 34-10. The x-z and x(cid:48)-t curves of a moving oscillator.

34-13

geometry of the situation, we ﬁnd that the frequency of the pips is increased bythe factor 1/(1 − v/c).

Is ω = ω0/(1 − v/c), then, the frequency that would be observed if we tookan ordinary atom, which had a natural frequency ω0, and moved it toward thereceiver at speed v? No; as we well know, the natural frequency ω1 of a movingatom is not the same as that measured when it is standing still, because of therelativistic dilation in the rate of passage of time. Thus if ω0 were the truenatural frequency, then the modiﬁed natural frequency ω1 would be

ω1 = ω0Therefore the observed frequency ω is

p1 − v2/c2.p1 − v2/c2

1 − v/c

.

ω = ω0

(34.11)

(34.12)

(34.13)

The shift in frequency observed in the above situation is called the Dopplereﬀect: if something moves toward us the light it emits appears more violet, andif it moves away it appears more red.

We shall now give two more derivations of this same interesting and importantresult. Suppose, now, that the source is standing still and is emitting wavesat frequency ω0, while the observer is moving with speed v toward the source.After a certain period of time t the observer will have moved to a new position, adistance vt from where he was at t = 0. How many radians of phase will he haveseen go by? A certain number, ω0t, went past any ﬁxed point, and in additionthe observer has swept past some more by his own motion, namely a number vtk0(the number of radians per meter times the distance). So the total number ofradians in the time t, or the observed frequency, would be ω1 = ω0 + k0v. Wehave made this analysis from the point of view of a man at rest; we would liketo know how it would look to the man who is moving. Here we have to worryagain about the diﬀerence in clock rate for the two observers, and this time that

means that we have to divide byp1 − v2/c2. So if k0 is the wave number, the

number of radians per meter in the direction of motion, and ω0 is the frequency,then the observed frequency for a moving man is

p1 − v2/c2 .ω = ω0 + k0v

34-14

For the case of light, we know that k0 = ω0/c. So, in this particular problem,

the equation would read

p1 − v2/c2 ,ω = ω0(1 + v/c)

(34.14)

which looks completely unlike formula (34.12)! Is the frequency that we wouldobserve if we move toward a source diﬀerent than the frequency that we wouldsee if the source moved toward us? Of course not! The theory of relativity saysthat these two must be exactly equal. If we were expert enough mathematicianswe would probably recognize that these two mathematical expressions are exactlyequal! In fact, the necessary equality of the two expressions is one of the waysby which some people like to demonstrate that relativity requires a time dilation,because if we did not put those square-root factors in, they would no longer beequal.

Since we know about relativity, let us analyze it in still a third way, whichmay appear a little more general. (It is really the same thing, since it makes nodiﬀerence how we do it!) According to the relativity theory there is a relationshipbetween position and time as observed by one man and position and time as seenby another who is moving relative to him. We wrote down those relationshipslong ago (Chapter 16). This is the Lorentz transformation and its inverse:

x + vt

p1 − v2/c2 ,x0 =p1 − v2/c2 ,t0 = t + vx/c2

p1 − v2/c2 ,x = x0 − vt0p1 − v2/c2 .t = t0 − vx0/c2

(34.15)

If we were standing still on the ground, the form of a wave would be cos (ωt− kx);all the nodes and maxima and minima would follow this form. But what woulda man in motion, observing the same physical wave, see? Where the ﬁeld iszero, the positions of all the nodes are the same (when the ﬁeld is zero, everyonemeasures the ﬁeld as zero); that is a relativistic invariant. So the form is thesame for the other man too, except that we must transform it into his frame ofreference:

(cid:20)

t0 − vx0/c2

p1 − v2/c2 − k

x0 − vt0

p1 − v2/c2

(cid:21)

.

cos (ωt − kx) = cos

ω

34-15

If we regroup the terms inside the brackets, we get

cos (ωt − kx) = cos

(cid:20) ω + kvp1 − v2/c2|{z

} x0(cid:21)p1 − v2/c2} t0 − k + vω/c2{z|

k0

x0 ] .

ω0

= cos [

(34.16)This is again a wave, a cosine wave, in which there is a certain frequency ω0, aconstant multiplying t0, and some other constant, k0, multiplying x0. We call k0the wave number, or the number of waves per meter, for the other man. Thereforethe other man will see a new frequency and a new wave number given by

t0 −

p1 − v2/c2 ,ω0 = ω + kvp1 − v2/c2 .k0 = k + ωv/c2

(34.17)

(34.18)

If we look at (34.17), we see that it is the same formula (34.13), that we obtainedby a more physical argument.

34-7 The ω, k four-vectorThe relationships indicated in Eqs. (34.17) and (34.18) are very interesting,because these say that the new frequency ω0 is a combination of the old frequency ωand the old wave number k, and that the new wave number is a combinationof the old wave number and frequency. Now the wave number is the rate ofchange of phase with distance, and the frequency is the rate of change of phasewith time, and in these expressions we see a close analogy with the Lorentztransformation of the position and time: if ω is thought of as being like t, and kis thought of as being like x divided by c2, then the new ω0 will be like t0, andthe new k0 will be like x0/c2. That is to say, under the Lorentz transformation ωand k transform the same way as do t and x. They constitute what we call afour-vector; when a quantity has four components transforming like time andspace, it is a four-vector. Everything seems all right, then, except for one littlething: we said that a four-vector has to have four components; where are theother two components? We have seen that ω and k are like time and space in onespace direction, but not in all directions, and so we must next study the problem

34-16

Fig. 34-11. A plane wave travelling in an oblique direction.

of the propagation of light in three space dimensions, not just in one direction,as we have been doing up until now.

Suppose that we have a coordinate system, x, y, z, and a wave which istravelling along and whose wavefronts are as shown in Fig. 34-11. The wavelengthof the wave is λ, but the direction of motion of the wave does not happen to bein the direction of one of the axes. What is the formula for such a wave? Theanswer is clearly cos (ωt − ks), where k = 2π/λ and s is the distance along thedirection of motion of the wave—the component of the spatial position in thedirection of motion. Let us put it this way: if r is the vector position of a point inspace, then s is r · ek, where ek is a unit vector in the direction of motion. Thatis, s is just r cos (r, ek), the component of distance in the direction of motion.Therefore our wave is cos (ωt − kek · r).Now it turns out to be very convenient to deﬁne a vector k, which is calledthe wave vector, which has a magnitude equal to the wave number, 2π/λ, and ispointed in the direction of propagation of the waves:

k = 2πek/λ = kek.

(34.19)

Using this vector, our wave can be written as cos (ωt − k · r), or as cos (ωt −kxx − kyy − kzz). What is the signiﬁcance of a component of k, say kx? Clearly,kx is the rate of change of phase with respect to x. Referring to Fig. 34-11, wesee that the phase changes as we change x, just as if there were a wave alongx, but of a longer wavelength. The「wavelength in the x-direction」is longerthan a natural, true wavelength by the secant of the angle α between the actual

34-17

direction of propagation and the x-axis:

λx = λ/ cos α.

(34.20)Therefore the rate of change of phase, which is proportional to the reciprocalof λx, is smaller by the factor cos α; that is just how kx would vary—it wouldbe the magnitude of k, times the cosine of the angle between k and the x-axis!That, then, is the nature of the wave vector that we use to represent a wavein three dimensions. The four quantities ω, kx, ky, kz transform in relativity asa four-vector, where ω corresponds to the time, and kx, ky, kz correspond to thex-, y-, and z-components of the four-vector.In our previous discussion of special relativity (Chapter 17), we learned thatthere are ways of making relativistic dot products with four-vectors. If we usethe position vector xµ, where µ stands for the four components (time and threespace ones), and if we call the wave vector kµ, where the index µ again has fourvalues, time and three space ones, then the dot product of xµ and kµ is writtenkµxµ (see Chapter 17). This dot product is an invariant, independent of thecoordinate system; what is it equal to? By the deﬁnition of this dot product in

P0four dimensions, it is X0We know from our study of vectors thatP0

kµxµ = ωt − kxx − kyy − kzz.

(34.21)

kµxµ is invariant under the Lorentztransformation, since kµ is a four-vector. But this quantity is precisely whatappears inside the cosine for a plane wave, and it ought to be invariant under aLorentz transformation. We cannot have a formula with something that changesinside the cosine, since we know that the phase of the wave cannot change whenwe change the coordinate system.

34-8 AberrationIn deriving Eqs. (34.17) and (34.18), we have taken a simple example wherek happened to be in a direction of motion, but of course we can generalize itto other cases also. For example, suppose there is a source sending out light ina certain direction from the point of view of a man at rest, but we are movingalong on the earth, say (Fig. 34-12). From which direction does the light appearto come? To ﬁnd out, we will have to write down the four components of kµ and

34-18

Fig. 34-12. A distant source S is viewed by (a) a stationary telescope,

and (b) a laterally moving telescope.

apply the Lorentz transformation. The answer, however, can be found by thefollowing argument: we have to point our telescope at an angle to see the light.Why? Because light is coming down at the speed c, and we are moving sidewiseat the speed v, so the telescope has to be tilted forward so that as the light comesdown it goes「straight」down the tube. It is very easy to see that the horizontaldistance is vt when the vertical distance is ct, and therefore, if θ0 is the angleof tilt, tan θ0 = v/c. How nice! How nice, indeed—except for one little thing:θ0 is not the angle at which we would have to set the telescope relative to theearth, because we made our analysis from the point of view of a「ﬁxed」observer.When we said the horizontal distance is vt, the man on the earth would havefound a diﬀerent distance, since he measured with a「squashed」ruler. It turnsout that, because of that contraction eﬀect,

which is equivalent to

tan θ =

v/cp1 − v2/c2 ,

(34.22)

(34.23)It will be instructive for the student to derive this result, using the Lorentztransformation.

sin θ = v/c.

This eﬀect, that a telescope has to be tilted, is called aberration, and it hasbeen observed. How can we observe it? Who can say where a given star shouldbe? Suppose we do have to look in the wrong direction to see a star; how do we

34-19

know it is the wrong direction? Because the earth goes around the sun. Todaywe have to point the telescope one way; six months later we have to tilt thetelescope the other way. That is how we can tell that there is such an eﬀect.

34-9 The momentum of lightNow we turn to a diﬀerent topic. We have never, in all our discussion of thepast few chapters, said anything about the eﬀects of the magnetic ﬁeld that isassociated with light. Ordinarily, the eﬀects of the magnetic ﬁeld are very small,but there is one interesting and important eﬀect which is a consequence of themagnetic ﬁeld. Suppose that light is coming from a source and is acting on acharge and driving that charge up and down. We will suppose that the electricﬁeld is in the x-direction, so the motion of the charge is also in the x-direction:it has a position x and a velocity v, as shown in Fig. 34-13. The magnetic ﬁeldis at right angles to the electric ﬁeld. Now as the electric ﬁeld acts on the chargeand moves it up and down, what does the magnetic ﬁeld do? The magnetic ﬁeldacts on the charge (say an electron) only when it is moving; but the electronis moving, it is driven by the electric ﬁeld, so the two of them work together:While the thing is going up and down it has a velocity and there is a force on it,B times v times q; but in which direction is this force? It is in the direction ofthe propagation of light. Therefore, when light is shining on a charge and it isoscillating in response to that light, there is a driving force in the direction ofthe light beam. This is called radiation pressure or light pressure.Let us determine how strong the radiation pressure is. Evidently it is F = qvBor, since everything is oscillating, it is the time average of this, hFi. From (34.2)the strength of the magnetic ﬁeld is the same as the strength of the electric ﬁelddivided by c, so we need to ﬁnd the average of the electric ﬁeld, times the velocity,times the charge, times 1/c: hFi = qhvEi/c. But the charge q times the ﬁeld E

Fig. 34-13. The magnetic force on a charge which is driven by the

electric ﬁeld is in the direction of the light beam.

34-20

is the electric force on a charge, and the force on the charge times the velocityis the work dW/dt being done on the charge! Therefore the force, the「pushingmomentum,」that is delivered per second by the light, is equal to 1/c times theenergy absorbed from the light per second! That is a general rule, since we didnot say how strong the oscillator was, or whether some of the charges cancelout. In any circumstance where light is being absorbed, there is a pressure. Themomentum that the light delivers is always equal to the energy that is absorbed,divided by c:

hFi = dW/dt

(34.24)That light carries energy we already know. We now understand that it alsocarries momentum, and further, that the momentum carried is always 1/c timesthe energy.When light is emitted from a source there is a recoil eﬀect: the same thing inreverse. If an atom is emitting an energy W in some direction, then there is arecoil momentum p = W/c. If light is reﬂected normally from a mirror, we gettwice the force.That is as far as we shall go using the classical theory of light. Of course weknow that there is a quantum theory, and that in many respects light acts like aparticle. The energy of a light-particle is a constant times the frequency:

.

c

W = hν = ω.

(34.25)

We now appreciate that light also carries a momentum equal to the energydivided by c, so it is also true that these eﬀective particles, these photons, carrya momentum(34.26)The direction of the momentum is, of course, the direction of propagation of thelight. So, to put it in vector form,

p = W/c = ω/c = k.

W = ω,

p = k.

(34.27)

We also know, of course, that the energy and momentum of a particle shouldform a four-vector. We have just discovered that ω and k form a four-vector.Therefore it is a good thing that (34.27) has the same constant in both cases;it means that the quantum theory and the theory of relativity are mutuallyconsistent.

34-21

Equation (34.27) can be written more elegantly as pµ = kµ, a relativisticequation, for a particle associated with a wave. Although we have discussed thisonly for photons, for which k (the magnitude of k) equals ω/c and p = W/c,the relation is much more general. In quantum mechanics all particles, not onlyphotons, exhibit wavelike properties, but the frequency and wave number of thewaves is related to the energy and momentum of particles by (34.27) (called thede Broglie relations) even when p is not equal to W/c.In the last chapter we saw that a beam of right or left circularly polarized lightalso carries angular momentum in an amount proportional to the energy E of thewave. In the quantum picture, a beam of circularly polarized light is regarded asa stream of photons, each carrying an angular momentum ±, along the directionof propagation. That is what becomes of polarization in the corpuscular point ofview—the photons carry angular momentum like spinning riﬂe bullets. But this「bullet」picture is really as incomplete as the「wave」picture, and we shall haveto discuss these ideas more fully in a later chapter on Quantum Behavior.

34-22

35

