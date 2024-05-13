Relativistic Effects in Radiation

34-1 Moving sources In the present chapter we shall describe a number of miscellaneous eﬀects in connection with radiation, and then we shall be ﬁnished with the classical theory of light propagation. In our analysis of light, we have gone rather far and into considerable detail. The only phenomena of any consequence associated with electromagnetic radiation that we have not discussed is what happens if radiowaves are contained in a box with reﬂecting walls, the size of the box being comparable to a wavelength, or are transmitted down a long tube. The phenomena of so-called cavity resonators and waveguides we shall discuss later; we shall ﬁrst use another physical example—sound—and then we shall return to this subject. Except for this, the present chapter is our last consideration of the classical theory of light.

We can summarize all the eﬀects that we shall now discuss by remarking that they have to do with the eﬀects of moving sources. We no longer assume that the source is localized, with all its motion being at a relatively low speed near a ﬁxed point.

We recall that the fundamental laws of electrodynamics say that, at large

distances from a moving charge, the electric ﬁeld is given by the formula

E = − q

4π0c2

d2eR0 dt2 .

(34.1)

The second derivative of the unit vector eR0 which points in the apparent direction of the charge, is the determining feature of the electric ﬁeld. This unit vector does not point toward the present position of the charge, of course, but rather in the direction that the charge would seem to be, if the information travels only at the ﬁnite speed c from the charge to the observer.

34-1

Associated with the electric ﬁeld is a magnetic ﬁeld, always at right angles to the electric ﬁeld and at right angles to the apparent direction of the source, given by the formula

B = −eR0 × E/c.

(34.2)

Until now we have considered only the case in which motions are nonrelativistic in speed, so that there is no appreciable motion in the direction of the source to be considered. Now we shall be more general and study the case where the motion is at an arbitrary velocity, and see what diﬀerent eﬀects may be expected in those circumstances. We shall let the motion be at an arbitrary speed, but of course we shall still assume that the detector is very far from the source.

Fig. 34-1. The path of a moving charge. The true position at the

time τ is at T , but the retarded position is at A.

We already know from our discussion in Chapter 28 that the only things that count in d2eR0/dt2 are the changes in the direction of eR0. Let the coordinates of the charge be (x, y, z), with z measured along the direction of observation (Fig. 34-1). At a given moment in time, say the moment τ, the three components of the position are x(τ), y(τ), and z(τ). The distance R is very nearly equal to R(τ) = R0 + z(τ). Now the direction of the vector eR0 depends mainly on x and y, but hardly at all upon z: the transverse components of the unit vector are x/R and y/R, and when we diﬀerentiate these components we get things like R2 in the denominator:

d(x/R)

dt

= dx/dt

R

− dz dt

x R2 .

So, when we are far enough away the only terms we have to worry about are the

34-2

variations of x and y. Thus we take out the factor R0 and get

Ex = −

q

4π0c2R0

Ey = −

q

4π0c2R0

d2x0 dt2 , d2y0 dt2 ,

(34.3)

where R0 is the distance, more or less, to q; let us take it as the distance OP to the origin of the coordinates (x, y, z). Thus the electric ﬁeld is a constant multiplied by a very simple thing, the second derivatives of the x- and y-coordinates. (We could put it more mathematically by calling x and y the transverse components of the position vector r of the charge, but this would not add to the clarity.)

Of course, we realize that the coordinates must be measured at the retarded time. Here we ﬁnd that z(τ) does aﬀect the retardation. What time is the retarded time? If the time of observation is called t (the time at P) then the time τ to which this corresponds at A is not the time t, but is delayed by the total distance that the light has to go, divided by the speed of light. In the ﬁrst approximation, this delay is R0/c, a constant (an uninteresting feature), but in the next approximation we must include the eﬀects of the position in the z-direction at the time τ, because if q is a little farther back, there is a little more retardation. This is an eﬀect that we have neglected before, and it is the only change needed in order to make our results valid for all speeds.

What we must now do is to choose a certain value of t and calculate the value of τ from it, and thus ﬁnd out where x and y are at that τ. These are then the retarded x and y, which we call x0 and y0, whose second derivatives determine the ﬁeld. Thus τ is determined by

and

t = τ + R0 c

x0(t) = x(τ),

+ z(τ) y0(t) = y(τ).

c

(34.4)

Now these are complicated equations, but it is easy enough to make a geometrical picture to describe their solution. This picture will give us a good qualitative feeling for how things work, but it still takes a lot of detailed mathematics to deduce the precise results of a complicated problem.

34-3

Fig. 34-2. A geometrical solution of Eq. (34.5) to ﬁnd x(cid:48)(t).

34-2 Finding the「apparent」motion The above equation has an interesting simpliﬁcation. If we disregard the uninteresting constant delay R0/c, which just means that we must change the origin of t by a constant, then it says that

ct = cτ + z(τ),

x0 = x(τ),

y0 = y(τ).

(34.5)

Now we need to ﬁnd x0 and y0 as functions of t, not τ, and we can do this in the following way: Eq. (34.5) says that we should take the actual motion and add a constant (the speed of light) times τ. What that turns out to mean is shown in Fig. 34-2. We take the actual motion of the charge (shown at left) and imagine that as it is going around it is being swept away from the point P at the speed c (there are no contractions from relativity or anything like that; this is just a mathematical addition of the cτ). In this way we get a new motion, in which the line-of-sight coordinate is ct, as shown at the right. (The ﬁgure shows the result for a rather complicated motion in a plane, but of course the motion may not be in one plane—it may be even more complicated than motion in a plane.) The point is that the horizontal (i.e., line-of-sight) distance now is no longer the old z, but is z + cτ, and therefore is ct. Thus we have found a picture of the curve, x0 (and y0) against t! All we have to do to ﬁnd the ﬁeld is to look at the acceleration of this curve, i.e., to diﬀerentiate it twice. So the ﬁnal answer is: in order to ﬁnd the electric ﬁeld for a moving charge, take the motion of the charge and translate it back at the speed c to「open it out」; then the curve, so drawn, is a curve of the x0 and y0 positions of the function of t. The acceleration of this curve gives the electric ﬁeld as a function of t. Or, if we wish, we can now imagine that this whole「rigid」curve moves forward at the speed

34-4

Fig. 34-3. The x(cid:48)(t) curve for a particle moving at constant speed v =

0.94c in a circle.

c through the plane of sight, so that the point of intersection with the plane of sight has the coordinates x0 and y0. The acceleration of this point makes the electric ﬁeld. This solution is just as exact as the formula we started with—it is simply a geometrical representation.

If the motion is relatively slow, for instance if we have an oscillator just going up and down slowly, then when we shoot that motion away at the speed of light, we would get, of course, a simple cosine curve, and that gives a formula we have been looking at for a long time: it gives the ﬁeld produced by an oscillating charge. A more interesting example is an electron moving rapidly, very nearly at the speed of light, in a circle. If we look in the plane of the circle, the retarded x0(t) appears as shown in Fig. 34-3. What is this curve? If we imagine a radius vector from the center of the circle to the charge, and if we extend this radial line a little bit past the charge, just a shade if it is going fast, then we come to a point on the line that goes at the speed of light. Therefore, when we translate the motion back at the speed of light, that corresponds to having a wheel with a charge on it rolling backward (without slipping) at the speed c; thus we ﬁnd a curve which is very close to a cycloid—it is called a curtate cycloid. If the charge is going very nearly at the speed of light, the「cusps」are very sharp indeed; if it went at exactly the speed of light, they would be actual cusps, inﬁnitely sharp.「Inﬁnitely sharp」is interesting; it means that near a cusp the second derivative is enormous. Once in each cycle we get a sharp pulse of electric ﬁeld. This is not at all what we would get from a nonrelativistic motion, where each time the charge goes around there is an oscillation which is of about the same「strength」all the time. Instead, there are very sharp pulses of electric ﬁeld spaced at time intervals T0 apart, where T0 is the period of revolution. These strong electric

34-5

ﬁelds are emitted in a narrow cone in the direction of motion of the charge. When the charge is moving away from P, there is very little curvature and there is very little radiated ﬁeld in the direction of P.

34-3 Synchrotron radiation We have very fast electrons moving in circular paths in the synchrotron; they are travelling at very nearly the speed c, and it is possible to see the above radiation as actual light! Let us discuss this in more detail.

In the synchrotron we have electrons which go around in circles in a uniform magnetic ﬁeld. First, let us see why they go in circles. From Eq. (28.2), we know that the force on a particle in a magnetic ﬁeld is given by

F = qv × B,

(34.6)

and it is at right angles both to the ﬁeld and to the velocity. As usual, the force is equal to the rate of change of momentum with time. If the ﬁeld is directed upward out of the paper, the momentum of the particle and the force on it are as shown in Fig. 34-4. Since the force is at right angles to the velocity, the kinetic energy, and therefore the speed, remains constant. All the magnetic ﬁeld does is to change the direction of motion. In a short time ∆t, the momentum vector changes at right angles to itself by an amount ∆p = F ∆t, and therefore p turns through an angle ∆θ = ∆p/p = qvB ∆t/p, since |F| = qvB. But in this same time the particle has gone a distance ∆s = v ∆t. Evidently, the two lines AB and CD will intersect at a point O such that OA = OC = R, where ∆s = R ∆θ. Combining

Fig. 34-4. A charged particle moves in a circular (or helical) path in a

uniform magnetic ﬁeld.

34-6

this with the previous expressions, we ﬁnd R ∆θ/∆t = Rω = v = qvBR/p, from which we ﬁnd (34.7)

p = qBR

and

ω = qvB/p.

(34.8)

Since this same argument can be applied during the next instant, the next, and so on, we conclude that the particle must be moving in a circle of radius R, with angular velocity ω. The result that the momentum of the particle is equal to a charge times the radius times the magnetic ﬁeld is a very important law that is used a great deal. It is important for practical purposes because if we have elementary particles which all have the same charge and we observe them in a magnetic ﬁeld, we can measure the radii of curvature of their orbits and, knowing the magnetic ﬁeld, thus determine the momenta of the particles. If we multiply both sides of Eq. (34.7) by c, and express q in terms of the electronic charge, we can measure the momentum in units of the electron volt. In those units our formula is

pc(eV) = 3 × 108(q/qe)BR,

(34.9) where B, R, and the speed of light are all expressed in the mks system, the latter being 3 × 108, numerically. The mks unit of magnetic ﬁeld is called a weber per square meter. There is an older unit which is still in common use, called a gauss. One weber/m2 is equal to 104 gauss. To give an idea of how big magnetic ﬁelds are, the strongest magnetic ﬁeld that one can usually make in iron is about 1.5× 104 gauss; beyond that, the advantage of using iron disappears. Today, electromagnets wound with superconducting wire are able to produce steady ﬁelds of over 105 gauss strength—that is, 10 mks units. The ﬁeld of the earth is a few tenths of a gauss at the equator.

Returning to Eq. (34.9), we could imagine the synchrotron running at a billion electron volts, so pc would be 109 for a billion electron volts. (We shall come back to the energy in just a moment.) Then, if we had a B corresponding to, say, 10,000 gauss, which is a good substantial ﬁeld, one mks unit, then we see that R would have to be 3.3 meters. The actual radius of the Caltech synchrotron is 3.7 meters, the ﬁeld is a little bigger, and the energy is 1.5 billion, but it is the same idea. So now we have a feeling for why the synchrotron has the size it has.

34-7

including the rest energy, is given by W =pp2c2 + m2c4, and for an electron

We have calculated the momentum, but we know that the total energy, the rest energy corresponding to mc2 is 0.511 × 106 eV, so when pc is 109 eV we can neglect mc2, and so for all practical purposes W = pc when the speeds are relativistic. It is practically the same to say the energy of an electron is a billion electron volts as to say the momentum times c is a billion electron volts. If W = 109 eV, it is easy to show that the speed diﬀers from the speed of light by but one part in eight million! We turn now to the radiation emitted by such a particle. A particle moving on a circle of radius 3.3 meters, or 20 meters circumference, goes around once in roughly the time it takes light to go 20 meters. So the wavelength that should be emitted by such a particle would be 20 meters—in the shortwave radio region. But because of the piling up eﬀect that we have been discussing (Fig. 34-3), and because the distance by which we must extend the radius to reach the speed c is only one part in eight million of the radius, the cusps of the curtate cycloid are enormously sharp compared with the distance between them. The acceleration, which involves a second derivative with respect to time, gets twice the「compression factor」of 8 × 106 because the time scale is reduced by eight million twice in the neighborhood of the cusp. Thus we might expect the eﬀective wavelength to be much shorter, to the extent of 64 times 1012 smaller than 20 meters, and that corresponds to the x-ray region. (Actually, the cusp itself is not the entire determining factor; one must also include a certain region about the cusp. This changes the factor to the 3/2 power instead of the square, but still leaves us above the optical region.) Thus, even though a slowly moving electron would have radiated 20-meter radiowaves, the relativistic eﬀect cuts down the wavelength so much that we can see it! Clearly, the light should be polarized, with the electric ﬁeld perpendicular to the uniform magnetic ﬁeld. To further appreciate what we would observe, suppose that we were to take such light (to simplify things, because these pulses are so far apart in time, we shall just take one pulse) and direct it onto a diﬀraction grating, which is a lot of scattering wires. After this pulse comes away from the grating, what do we see? (We should see red light, blue light, and so on, if we see any light at all.) What do we see? The pulse strikes the grating head-on, and all the oscillators in the grating, together, are violently moved up and then back down again, just once. They then produce eﬀects in various directions, as shown in Fig. 34-5. But the point P is closer to one end of the grating than to the other, so at this point the electric ﬁeld arrives ﬁrst from wire A, next from B, and so on; ﬁnally, the

34-8

Fig. 34-5. The light which strikes a grating as a single, sharp pulse is

scattered in various directions as diﬀerent colors.

pulse from the last wire arrives. In short, the sum of the reﬂections from all the successive wires is as shown in Fig. 34-6(a); it is an electric ﬁeld which is a series of pulses, and it is very like a sine wave whose wavelength is the distance between the pulses, just as it would be for monochromatic light striking the grating! So, we get colored light all right. But, by the same argument, will we not get light from any kind of a「pulse」? No. Suppose that the curve were much smoother; then we would add all the scattered waves together, separated by a small time between them (Fig. 34-6b). Then we see that the ﬁeld would not shake at all, it would be a very smooth curve, because each pulse does not vary much in the time interval between pulses.

Fig. 34-6. The total electric ﬁeld due to a series of (a) sharp pulses

and (b) smooth pulses.

The electromagnetic radiation emitted by relativistic charged particles cir- culating in a magnetic ﬁeld is called synchrotron radiation. It is so named for obvious reasons, but it is not limited speciﬁcally to synchrotrons, or even to earthbound laboratories. It is exciting and interesting that it also occurs in nature!

34-9

Fig. 34-7. The crab nebula as seen in all colors (no ﬁlter).

34-4 Cosmic synchrotron radiation In the year 1054 the Chinese and Japanese civilizations were among the most advanced in the world; they were conscious of the external universe, and they recorded, most remarkably, an explosive bright star in that year. (It is amazing that none of the European monks, writing all the books of the middle ages, even bothered to write that a star exploded in the sky, but they did not.) Today we may take a picture of that star, and what we see is shown in Fig. 34-7. On the outside is a big mass of red ﬁlaments, which is produced by the atoms of the thin gas「ringing」at their natural frequencies; this makes a bright line spectrum with diﬀerent frequencies in it. The red happens in this case to be due to nitrogen. On the other hand, in the central region is a mysterious, fuzzy patch of light in a continuous distribution of frequency, i.e., there are no special frequencies associated with particular atoms. Yet this is not dust「lit up」by nearby stars, which is one way by which one can get a continuous spectrum. We can see stars through it, so it is transparent, but it is emitting light.

34-10

Fig. 34-8. The crab nebula as seen through a blue ﬁlter and a polaroid.

(a) Electric vector vertical. (b) Electric vector horizontal.

In Fig. 34-8 we look at the same object, using light in a region of the spectrum which has no bright spectral line, so that we see only the central region. But in this case, also, polarizers have been put on the telescope, and the two views correspond to two orientations 90◦ apart. We see that the pictures are diﬀerent! That is to say, the light is polarized. The reason, presumably, is that there is a local magnetic ﬁeld, and many very energetic electrons are going around in that magnetic ﬁeld.

We have just illustrated how the electrons could go around the ﬁeld in a circle. We can add to this, of course, any uniform motion in the direction of the ﬁeld, since the force, qv × B, has no component in this direction and, as we have already remarked, the synchrotron radiation is evidently polarized in a direction at right angles to the projection of the magnetic ﬁeld onto the plane of sight.

Putting these two facts together, we see that in a region where one picture is bright and the other one is black, the light must have its electric ﬁeld completely polarized in one direction. This means that there is a magnetic ﬁeld at right angles to this direction, while in other regions, where there is a strong emission in the other picture, the magnetic ﬁeld must be the other way. If we look carefully at Fig. 34-8, we may notice that there is, roughly speaking, a general set of「lines」that go one way in one picture and at right angles to this in the other. The pictures show a kind of ﬁbrous structure. Presumably, the magnetic ﬁeld lines will tend to extend relatively long distances in their own direction, and

34-11

so, presumably, there are long regions of magnetic ﬁeld with all the electrons spiralling one way, while in another region the ﬁeld is the other way and the electrons are also spiralling that way.

What keeps the electron energy so high for so long a time? After all, it is 900 years since the explosion—how can they keep going so fast? How they maintain their energy and how this whole thing keeps going is still not thoroughly understood.

34-5 Bremsstrahlung We shall next remark brieﬂy on one other interesting eﬀect of a very fast- moving particle that radiates energy. The idea is very similar to the one we have just discussed. Suppose that there are charged particles in a piece of matter and a very fast electron, say, comes by (Fig. 34-9). Then, because of the electric ﬁeld around the atomic nucleus the electron is pulled, accelerated, so that the curve of its motion has a slight kink or bend in it. If the electron is travelling at very nearly the speed of light, what is the electric ﬁeld produced in the direction C? Remember our rule: we take the actual motion, translate it backwards at speed c, and that gives us a curve whose curvature measures the electric ﬁeld. It was coming toward us at the speed v, so we get a backward motion, with the whole picture compressed into a smaller distance in proportion as c − v is smaller than c. So, if 1 − v/c (cid:28) 1, there is a very sharp and rapid curvature at B0, and when we take the second derivative of that we get a very high ﬁeld in the direction of the motion. So when very energetic electrons move through matter they spit radiation in a forward direction. This is called bremsstrahlung. As a matter of fact, the synchrotron is used, not so much to make high-energy electrons (actually if we could get them out of the machine more conveniently we would not say this) as to make very energetic photons—gamma rays—by passing the energetic

Fig. 34-9. A fast electron passing near a nucleus radiates energy in

the direction of its motion.

34-12

electrons through a solid tungsten「target,」and letting them radiate photons from this bremsstrahlung eﬀect.

34-6 The Doppler eﬀect Now we go on to consider some other examples of the eﬀects of moving sources. Let us suppose that the source is a stationary atom which is oscillating at one of its natural frequencies, ω0. Then we know that the frequency of the light we would observe is ω0. But now let us take another example, in which we have a similar oscillator oscillating with a frequency ω1, and at the same time the whole atom, the whole oscillator, is moving along in a direction toward the observer at velocity v. Then the actual motion in space, of course, is as shown in Fig. 34-10(a). Now we play our usual game, we add cτ; that is to say, we translate the whole curve backward and we ﬁnd then that it oscillates as in Fig. 34-10(b). In a given amount of time τ, when the oscillator would have gone a distance vτ, on the x0 vs. ct diagram it goes a distance (c − v)τ. So all the oscillations of frequency ω1 in the time ∆τ are now found in the interval ∆t = (1 − v/c) ∆τ; they are squashed together, and as this curve comes by us at speed c, we will see light of a higher frequency, higher by just the compression factor (1 − v/c). Thus we observe

ω = ω1

1 − v/c

.

(34.10)

We can, of course, analyze this situation in various other ways. Suppose that the atom were emitting, instead of sine waves, a series of pulses, pip, pip, pip, pip, at a certain frequency ω1. At what frequency would they be received by us? The ﬁrst one that arrives has a certain delay, but the next one is delayed less because in the meantime the atom moves closer to the receiver. Therefore, the time between the「pips」is decreased by the motion. If we analyze the

Fig. 34-10. The x-z and x(cid:48)-t curves of a moving oscillator.

34-13

geometry of the situation, we ﬁnd that the frequency of the pips is increased by the factor 1/(1 − v/c).

Is ω = ω0/(1 − v/c), then, the frequency that would be observed if we took an ordinary atom, which had a natural frequency ω0, and moved it toward the receiver at speed v? No; as we well know, the natural frequency ω1 of a moving atom is not the same as that measured when it is standing still, because of the relativistic dilation in the rate of passage of time. Thus if ω0 were the true natural frequency, then the modiﬁed natural frequency ω1 would be

ω1 = ω0 Therefore the observed frequency ω is

p1 − v2/c2. p1 − v2/c2

1 − v/c

.

ω = ω0

(34.11)

(34.12)

(34.13)

The shift in frequency observed in the above situation is called the Doppler eﬀect: if something moves toward us the light it emits appears more violet, and if it moves away it appears more red.

We shall now give two more derivations of this same interesting and important result. Suppose, now, that the source is standing still and is emitting waves at frequency ω0, while the observer is moving with speed v toward the source. After a certain period of time t the observer will have moved to a new position, a distance vt from where he was at t = 0. How many radians of phase will he have seen go by? A certain number, ω0t, went past any ﬁxed point, and in addition the observer has swept past some more by his own motion, namely a number vtk0 (the number of radians per meter times the distance). So the total number of radians in the time t, or the observed frequency, would be ω1 = ω0 + k0v. We have made this analysis from the point of view of a man at rest; we would like to know how it would look to the man who is moving. Here we have to worry again about the diﬀerence in clock rate for the two observers, and this time that

means that we have to divide byp1 − v2/c2. So if k0 is the wave number, the

number of radians per meter in the direction of motion, and ω0 is the frequency, then the observed frequency for a moving man is

p1 − v2/c2 . ω = ω0 + k0v

34-14

For the case of light, we know that k0 = ω0/c. So, in this particular problem,

the equation would read

p1 − v2/c2 , ω = ω0(1 + v/c)

(34.14)

which looks completely unlike formula (34.12)! Is the frequency that we would observe if we move toward a source diﬀerent than the frequency that we would see if the source moved toward us? Of course not! The theory of relativity says that these two must be exactly equal. If we were expert enough mathematicians we would probably recognize that these two mathematical expressions are exactly equal! In fact, the necessary equality of the two expressions is one of the ways by which some people like to demonstrate that relativity requires a time dilation, because if we did not put those square-root factors in, they would no longer be equal.

Since we know about relativity, let us analyze it in still a third way, which may appear a little more general. (It is really the same thing, since it makes no diﬀerence how we do it!) According to the relativity theory there is a relationship between position and time as observed by one man and position and time as seen by another who is moving relative to him. We wrote down those relationships long ago (Chapter 16). This is the Lorentz transformation and its inverse:

x + vt

p1 − v2/c2 , x0 = p1 − v2/c2 , t0 = t + vx/c2

p1 − v2/c2 , x = x0 − vt0 p1 − v2/c2 . t = t0 − vx0/c2

(34.15)

If we were standing still on the ground, the form of a wave would be cos (ωt− kx); all the nodes and maxima and minima would follow this form. But what would a man in motion, observing the same physical wave, see? Where the ﬁeld is zero, the positions of all the nodes are the same (when the ﬁeld is zero, everyone measures the ﬁeld as zero); that is a relativistic invariant. So the form is the same for the other man too, except that we must transform it into his frame of reference:

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

(cid:20) ω + kv p1 − v2/c2 | {z

} x0(cid:21) p1 − v2/c2 } t0 − k + vω/c2 {z |

k0

x0 ] .

ω0

= cos [

(34.16) This is again a wave, a cosine wave, in which there is a certain frequency ω0, a constant multiplying t0, and some other constant, k0, multiplying x0. We call k0 the wave number, or the number of waves per meter, for the other man. Therefore the other man will see a new frequency and a new wave number given by

t0 −

p1 − v2/c2 , ω0 = ω + kv p1 − v2/c2 . k0 = k + ωv/c2

(34.17)

(34.18)

If we look at (34.17), we see that it is the same formula (34.13), that we obtained by a more physical argument.

34-7 The ω, k four-vector The relationships indicated in Eqs. (34.17) and (34.18) are very interesting, because these say that the new frequency ω0 is a combination of the old frequency ω and the old wave number k, and that the new wave number is a combination of the old wave number and frequency. Now the wave number is the rate of change of phase with distance, and the frequency is the rate of change of phase with time, and in these expressions we see a close analogy with the Lorentz transformation of the position and time: if ω is thought of as being like t, and k is thought of as being like x divided by c2, then the new ω0 will be like t0, and the new k0 will be like x0/c2. That is to say, under the Lorentz transformation ω and k transform the same way as do t and x. They constitute what we call a four-vector; when a quantity has four components transforming like time and space, it is a four-vector. Everything seems all right, then, except for one little thing: we said that a four-vector has to have four components; where are the other two components? We have seen that ω and k are like time and space in one space direction, but not in all directions, and so we must next study the problem

34-16

Fig. 34-11. A plane wave travelling in an oblique direction.

of the propagation of light in three space dimensions, not just in one direction, as we have been doing up until now.

Suppose that we have a coordinate system, x, y, z, and a wave which is travelling along and whose wavefronts are as shown in Fig. 34-11. The wavelength of the wave is λ, but the direction of motion of the wave does not happen to be in the direction of one of the axes. What is the formula for such a wave? The answer is clearly cos (ωt − ks), where k = 2π/λ and s is the distance along the direction of motion of the wave—the component of the spatial position in the direction of motion. Let us put it this way: if r is the vector position of a point in space, then s is r · ek, where ek is a unit vector in the direction of motion. That is, s is just r cos (r, ek), the component of distance in the direction of motion. Therefore our wave is cos (ωt − kek · r). Now it turns out to be very convenient to deﬁne a vector k, which is called the wave vector, which has a magnitude equal to the wave number, 2π/λ, and is pointed in the direction of propagation of the waves:

k = 2πek/λ = kek.

(34.19)

Using this vector, our wave can be written as cos (ωt − k · r), or as cos (ωt − kxx − kyy − kzz). What is the signiﬁcance of a component of k, say kx? Clearly, kx is the rate of change of phase with respect to x. Referring to Fig. 34-11, we see that the phase changes as we change x, just as if there were a wave along x, but of a longer wavelength. The「wavelength in the x-direction」is longer than a natural, true wavelength by the secant of the angle α between the actual

34-17

direction of propagation and the x-axis:

λx = λ/ cos α.

(34.20) Therefore the rate of change of phase, which is proportional to the reciprocal of λx, is smaller by the factor cos α; that is just how kx would vary—it would be the magnitude of k, times the cosine of the angle between k and the x-axis! That, then, is the nature of the wave vector that we use to represent a wave in three dimensions. The four quantities ω, kx, ky, kz transform in relativity as a four-vector, where ω corresponds to the time, and kx, ky, kz correspond to the x-, y-, and z-components of the four-vector. In our previous discussion of special relativity (Chapter 17), we learned that there are ways of making relativistic dot products with four-vectors. If we use the position vector xµ, where µ stands for the four components (time and three space ones), and if we call the wave vector kµ, where the index µ again has four values, time and three space ones, then the dot product of xµ and kµ is written kµxµ (see Chapter 17). This dot product is an invariant, independent of the coordinate system; what is it equal to? By the deﬁnition of this dot product in

P0 four dimensions, it is X0 We know from our study of vectors thatP0

kµxµ = ωt − kxx − kyy − kzz.

(34.21)

kµxµ is invariant under the Lorentz transformation, since kµ is a four-vector. But this quantity is precisely what appears inside the cosine for a plane wave, and it ought to be invariant under a Lorentz transformation. We cannot have a formula with something that changes inside the cosine, since we know that the phase of the wave cannot change when we change the coordinate system.

34-8 Aberration In deriving Eqs. (34.17) and (34.18), we have taken a simple example where k happened to be in a direction of motion, but of course we can generalize it to other cases also. For example, suppose there is a source sending out light in a certain direction from the point of view of a man at rest, but we are moving along on the earth, say (Fig. 34-12). From which direction does the light appear to come? To ﬁnd out, we will have to write down the four components of kµ and

34-18

Fig. 34-12. A distant source S is viewed by (a) a stationary telescope,

and (b) a laterally moving telescope.

apply the Lorentz transformation. The answer, however, can be found by the following argument: we have to point our telescope at an angle to see the light. Why? Because light is coming down at the speed c, and we are moving sidewise at the speed v, so the telescope has to be tilted forward so that as the light comes down it goes「straight」down the tube. It is very easy to see that the horizontal distance is vt when the vertical distance is ct, and therefore, if θ0 is the angle of tilt, tan θ0 = v/c. How nice! How nice, indeed—except for one little thing: θ0 is not the angle at which we would have to set the telescope relative to the earth, because we made our analysis from the point of view of a「ﬁxed」observer. When we said the horizontal distance is vt, the man on the earth would have found a diﬀerent distance, since he measured with a「squashed」ruler. It turns out that, because of that contraction eﬀect,

which is equivalent to

tan θ =

v/cp1 − v2/c2 ,

(34.22)

(34.23) It will be instructive for the student to derive this result, using the Lorentz transformation.

sin θ = v/c.

This eﬀect, that a telescope has to be tilted, is called aberration, and it has been observed. How can we observe it? Who can say where a given star should be? Suppose we do have to look in the wrong direction to see a star; how do we

34-19

know it is the wrong direction? Because the earth goes around the sun. Today we have to point the telescope one way; six months later we have to tilt the telescope the other way. That is how we can tell that there is such an eﬀect.

34-9 The momentum of light Now we turn to a diﬀerent topic. We have never, in all our discussion of the past few chapters, said anything about the eﬀects of the magnetic ﬁeld that is associated with light. Ordinarily, the eﬀects of the magnetic ﬁeld are very small, but there is one interesting and important eﬀect which is a consequence of the magnetic ﬁeld. Suppose that light is coming from a source and is acting on a charge and driving that charge up and down. We will suppose that the electric ﬁeld is in the x-direction, so the motion of the charge is also in the x-direction: it has a position x and a velocity v, as shown in Fig. 34-13. The magnetic ﬁeld is at right angles to the electric ﬁeld. Now as the electric ﬁeld acts on the charge and moves it up and down, what does the magnetic ﬁeld do? The magnetic ﬁeld acts on the charge (say an electron) only when it is moving; but the electron is moving, it is driven by the electric ﬁeld, so the two of them work together: While the thing is going up and down it has a velocity and there is a force on it, B times v times q; but in which direction is this force? It is in the direction of the propagation of light. Therefore, when light is shining on a charge and it is oscillating in response to that light, there is a driving force in the direction of the light beam. This is called radiation pressure or light pressure. Let us determine how strong the radiation pressure is. Evidently it is F = qvB or, since everything is oscillating, it is the time average of this, hFi. From (34.2) the strength of the magnetic ﬁeld is the same as the strength of the electric ﬁeld divided by c, so we need to ﬁnd the average of the electric ﬁeld, times the velocity, times the charge, times 1/c: hFi = qhvEi/c. But the charge q times the ﬁeld E

Fig. 34-13. The magnetic force on a charge which is driven by the

electric ﬁeld is in the direction of the light beam.

34-20

is the electric force on a charge, and the force on the charge times the velocity is the work dW/dt being done on the charge! Therefore the force, the「pushing momentum,」that is delivered per second by the light, is equal to 1/c times the energy absorbed from the light per second! That is a general rule, since we did not say how strong the oscillator was, or whether some of the charges cancel out. In any circumstance where light is being absorbed, there is a pressure. The momentum that the light delivers is always equal to the energy that is absorbed, divided by c:

hFi = dW/dt

(34.24) That light carries energy we already know. We now understand that it also carries momentum, and further, that the momentum carried is always 1/c times the energy. When light is emitted from a source there is a recoil eﬀect: the same thing in reverse. If an atom is emitting an energy W in some direction, then there is a recoil momentum p = W/c. If light is reﬂected normally from a mirror, we get twice the force. That is as far as we shall go using the classical theory of light. Of course we know that there is a quantum theory, and that in many respects light acts like a particle. The energy of a light-particle is a constant times the frequency:

.

c

W = hν = ω.

(34.25)

We now appreciate that light also carries a momentum equal to the energy divided by c, so it is also true that these eﬀective particles, these photons, carry a momentum (34.26) The direction of the momentum is, of course, the direction of propagation of the light. So, to put it in vector form,

p = W/c = ω/c = k.

W = ω,

p = k.

(34.27)

We also know, of course, that the energy and momentum of a particle should form a four-vector. We have just discovered that ω and k form a four-vector. Therefore it is a good thing that (34.27) has the same constant in both cases; it means that the quantum theory and the theory of relativity are mutually consistent.

34-21

Equation (34.27) can be written more elegantly as pµ = kµ, a relativistic equation, for a particle associated with a wave. Although we have discussed this only for photons, for which k (the magnitude of k) equals ω/c and p = W/c, the relation is much more general. In quantum mechanics all particles, not only photons, exhibit wavelike properties, but the frequency and wave number of the waves is related to the energy and momentum of particles by (34.27) (called the de Broglie relations) even when p is not equal to W/c. In the last chapter we saw that a beam of right or left circularly polarized light also carries angular momentum in an amount proportional to the energy E of the wave. In the quantum picture, a beam of circularly polarized light is regarded as a stream of photons, each carrying an angular momentum ±, along the direction of propagation. That is what becomes of polarization in the corpuscular point of view—the photons carry angular momentum like spinning riﬂe bullets. But this「bullet」picture is really as incomplete as the「wave」picture, and we shall have to discuss these ideas more fully in a later chapter on Quantum Behavior.

34-22

35

