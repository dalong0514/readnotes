40-1 HydrostaticsThe

subject of the ﬂow of ﬂuids, and particularly of water, fascinates everybody.We can all remember, as children, playing in the bathtub or in mud puddles withthe strange stuﬀ. As we get older, we watch streams, waterfalls, and whirlpools,and we are fascinated by this substance which seems almost alive relative to solids.The behavior of ﬂuids is in many ways very unexpected and interesting—it is thesubject of this chapter and the next. The eﬀorts of a child trying to dam a smallstream ﬂowing in the street and his surprise at the strange way the water worksits way out has its analog in our attempts over the years to understand the ﬂow ofﬂuids. We have tried to dam the water up—in our understanding—by getting thelaws and the equations that describe the ﬂow. We will describe these attemptsin this chapter. In the next chapter, we will describe the unique way in whichwater has broken through the dam and escaped our attempts to understand it.We suppose that the elementary properties of water are already known to you.The main property that distinguishes a ﬂuid from a solid is that a ﬂuid cannotmaintain a shear stress for any length of time. If a shear is applied to a ﬂuid, itwill move under the shear. Thicker liquids like honey move less easily than ﬂuidslike air or water. The measure of the ease with which a ﬂuid yields is its viscosity.In this chapter we will consider only situations in which the viscous eﬀects canbe ignored. The eﬀects of viscosity will be taken up in the next chapter.

We begin by considering hydrostatics, the theory of liquids at rest. Whenliquids are at rest, there are no shear forces (even for viscous liquids). The lawof hydrostatics, therefore, is that the stresses are always normal to any surfaceinside the ﬂuid. The normal force per unit area is called the pressure. From thefact that there is no shear in a static ﬂuid it follows that the pressure stress is thesame in all directions (Fig. 40-1). We will let you entertain yourself by provingthat if there is no shear on any plane in a ﬂuid, the pressure must be the samein any direction.

The pressure in a ﬂuid may vary from place to place. For example, in a staticﬂuid at the earth’s surface the pressure will vary with height because of theweight of the ﬂuid. If the density ρ of the ﬂuid is considered constant, and if thepressure at some arbitrary zero level is called p0 (Fig. 40-2), then the pressure ata height h above this point is p = p0 − ρgh, where g is the gravitational forceper unit mass. The combination

40-1 Hydrostatics40-2 The equations of motion40-3 Steady ﬂow—Bernoulli’s

theorem

40-4 Circulation40-5 Vortex lines

Fig. 40-1. In a static ﬂuid the force perunit area across any surface is normal to thesurface and is the same for all orientationsof the surface.

p + ρgh

is, therefore, a constant in the static ﬂuid. This relation is familiar to you, butwe will now derive a more general result of which it is a special case.

If we take a small cube of water, what is the net force on it from the pressure?Since the pressure at any place is the same in all directions, there can be anet force per unit volume only because the pressure varies from one point toanother. Suppose that the pressure is varying in the x-direction—and we take thecoordinate directions parallel to the cube edges. The pressure on the face at xgives the force p ∆y ∆z (Fig. 40-3), and the pressure on the face at x+∆x gives theforce −[p+(∂p/∂x) ∆x] ∆y ∆z, so that the resultant force is −(∂p/∂x) ∆x ∆y ∆z.If we take the remaining pairs of faces of the cube, we easily see that the pressureforce per unit volume is −∇p. If there are other forces in addition—such asgravity—then the pressure must balance them to give equilibrium.

40-1

Fig. 40-2. The pressure in a static liquid.

Fig. 40-3. The net pressure force on a

cube is −∇p per unit volume.

Let’s take a circumstance in which such an additional force can be describedby a potential energy, as would be true in the case of gravitation; we will letφ stand for the potential energy per unit mass. (For gravity, for instance, φ isjust gz.) The force per unit mass is given in terms of the potential by −∇φ, and ifρ is the density of the ﬂuid, the force per unit volume is −ρ∇φ. For equilibriumthis force per unit volume added to the pressure force per unit volume must givezero:

− ∇p − ρ∇φ = 0.

(40.1)Equation (40.1) is the equation of hydrostatics. In general, it has no solution. Ifthe density varies in space in an arbitrary way, there is no way for the forces tobe in balance, and the ﬂuid cannot be in static equilibrium. Convection currentswill start up. We can see this from the equation since the pressure term is a puregradient, whereas for variable ρ the other term is not. Only when ρ is a constantis the potential term a pure gradient. Then the equation has a solution

p + ρφ = const.

Another possibility which allows hydrostatic equilibrium is for ρ to be a functiononly of p. However, we will leave the subject of hydrostatics because it is notnearly so interesting as the situation when ﬂuids are in motion.

40-2 The equations of motionFirst, we will discuss ﬂuid motions in a purely abstract, theoretical way andthen consider special examples. To describe the motion of a ﬂuid, we must give itsproperties at every point. For example, at diﬀerent places, the water (let us callthe ﬂuid「water」) is moving with diﬀerent velocities. To specify the character ofthe ﬂow, therefore, we must give the three components of velocity at every pointand for any time. If we can ﬁnd the equations that determine the velocity, thenwe would know how the liquid moves at all times. The velocity, however, is notthe only property that the ﬂuid has which varies from point to point. We havejust discussed the variation of the pressure from point to point. And there arestill other variables. There may also be a variation of density from point to point.In addition, the ﬂuid may be a conductor and carry an electric current whosedensity j varies from point to point in magnitude and direction. There may bea temperature which varies from point to point, or a magnetic ﬁeld, and so on.So the number of ﬁelds needed to describe the complete situation will depend onhow complicated the problem is. There are interesting phenomena when currentsand magnetism play a dominant part in determining the behavior of the ﬂuid; thesubject is called magnetohydrodynamics, and great attention is being paid to it atthe present time. However, we are not going to consider these more complicatedsituations because there are already interesting phenomena at a lower level ofcomplexity, and even the more elementary level will be complicated enough.

We will take the situation where there is no magnetic ﬁeld and no conductivity,and we will not worry about the temperature because we will suppose that thedensity and pressure determine in a unique manner the temperature at any point.As a matter of fact, we will reduce the complexity of our work by making theassumption that the density is a constant—we imagine that the ﬂuid is essentiallyincompressible. Putting it another way, we are supposing that the variations ofpressure are so small that the changes in density produced thereby are negligible.If that is not the case, we would encounter phenomena additional to the oneswe will be discussing here—for example, the propagation of sound or of shockwaves. We have already discussed the propagation of sound and shocks to someextent, so we will now isolate our consideration of hydrodynamics from theseother phenomena by making the approximation that the density ρ is a constant.It is easy to determine when the approximation of constant ρ is a good one. Wecan say that if the velocities of ﬂow are much less than the speed of a soundwave in the ﬂuid, we do not have to worry about variations in density. Theescape that water makes in our attempts to understand it is not related to the40-2

approximation of constant density. The complications that do permit the escapewill be discussed in the next chapter.

In the general theory of ﬂuids one must begin with an equation of state forthe ﬂuid which connects the pressure to the density. In our approximation thisequation of state is simply

ρ = const.

This then is the ﬁrst relation for our variables. The next relation expresses theconservation of matter—if matter ﬂows away from a point, there must be adecrease in the amount left behind. If the ﬂuid velocity is v, then the mass whichﬂows in a unit time across a unit area of surface is the component of ρv normalto the surface. We have had a similar relation in electricity. We also know fromelectricity that the divergence of such a quantity gives the rate of decrease of thedensity per unit time. In the same way, the equation

∇ · (ρv) = − ∂ρ∂t

(40.2)

expresses the conservation of mass for a ﬂuid; it is the hydrodynamic equation ofcontinuity. In our approximation, which is the incompressible ﬂuid approximation,ρ is a constant, and the equation of continuity is simply

∇ · v = 0.

(40.3)

The ﬂuid velocity v—like the magnetic ﬁeld B—has zero divergence. (The hydro-dynamic equations are often closely analogous to the electrodynamic equations;that’s why we studied electrodynamics ﬁrst. Some people argue the other way;they think that one should study hydrodynamics ﬁrst so that it will be easierto understand electricity afterwards. But electrodynamics is really much easierthan hydrodynamics.)

We will get our next equation from Newton’s law which tells us how thevelocity changes because of the forces. The mass of an element of volume of theﬂuid times its acceleration must be equal to the force on the element. Taking anelement of unit volume, and writing the force per unit volume as f, we have

ρ × (acceleration) = f .

ρ × (acceleration) = −∇p − ρ∇φ + f visc.

We will write the force density as the sum of three terms. We have already con-sidered the pressure force per unit volume, −∇p. Then there are the「external」forces which act at a distance—like gravity or electricity. When they are conser-vative forces with a potential per unit mass, φ, they give a force density −ρ∇φ.(If the external forces are not conservative, we would have to write f ext for theexternal force per unit volume.) Then there is another「internal」force per unitvolume, which is due to the fact that in a ﬂowing ﬂuid there can also be a shearingstress. This is called the viscous force, which we will write f visc. Our equationof motion is(40.4)For this chapter we are going to suppose that the liquid is「thin」in the sensethat the viscosity is unimportant, so we will omit f visc. When we drop theviscosity term, we will be making an approximation which describes some idealstuﬀ rather than real water. John von Neumann was well aware of the tremendousdiﬀerence between what happens when you don’t have the viscous terms andwhen you do, and he was also aware that, during most of the development ofhydrodynamics until about 1900, almost the main interest was in solving beautifulmathematical problems with this approximation which had almost nothing todo with real ﬂuids. He characterized the theorist who made such analyses as aman who studied「dry water.」Such analyses leave out an essential property ofthe ﬂuid. It is because we are leaving this property out of our calculations inthis chapter that we have given it the title「The Flow of Dry Water.」We arepostponing a discussion of real water to the next chapter.

40-3

Fig. 40-4. The acceleration of a ﬂuid

particle.

If we leave out f visc, we have in Eq. (40.4) everything we need except anexpression for the acceleration. You might think that the formula for the acceler-ation of a ﬂuid particle would be very simple, for it seems obvious that if v is thevelocity of a ﬂuid particle at some place in the ﬂuid, the acceleration would justbe ∂v/∂t. It is not—and for a rather subtle reason. The derivative ∂v/∂t, is therate at which the velocity v(x, y, z, t) changes at a ﬁxed point in space. Whatwe need is how fast the velocity changes for a particular piece of ﬂuid. Imaginethat we mark one of the drops of water with a colored speck so we can watch it.In a small interval of time ∆t, this drop will move to a diﬀerent location. If thedrop is moving along some path as sketched in Fig. 40-4, it might in ∆t movefrom P1 to P2. In fact, it will move in the x-direction by an amount vx ∆t, inthe y-direction by the amount vy ∆t, and in the z-direction by the amount vz ∆t.We see that, if v(x, y, z, t) is the velocity of the ﬂuid particle which is at (x, y, z)at the time t, then the velocity of the same particle, at the time t + ∆t is givenby v(x + ∆x, y + ∆y, z + ∆z, t + ∆t)—with

∆x = vx ∆t,

∆y = vy ∆t,

and

∆z = vz ∆t.

From the deﬁnition of the partial derivatives—recall Eq. (2.7)—we have, to ﬁrstorder, that

v(x + vx ∆t, y + vy ∆t, z + vz ∆t, t + ∆t)

= v(x, y, z, t) + ∂v∂x

vx ∆t + ∂v∂y

vy ∆t + ∂v∂z

vz ∆t + ∂v∂t

∆t.

The acceleration ∆v/∆t is

vx

+ vy

∂v∂x

∂v∂y

+ vz

∂v∂z

+ ∂v∂t

.

We can write this symbolically—treating ∇ as a vector—as

(v · ∇)v + ∂v∂t

.

(40.5)

Note that there can be an acceleration even though ∂v/∂t = 0 so that velocityat a given point is not changing. As an example, water ﬂowing in a circle at aconstant speed is accelerating even though the velocity at a given point is notchanging. The reason is, of course, that the velocity of a particular piece of waterwhich is initially at one point on the circle has a diﬀerent direction a momentlater; there is a centripetal acceleration.

The rest of our theory is just mathematical—ﬁnding solutions of the equation

of motion we get by putting the acceleration (40.5) into Eq. (40.4). We get

+ (v · ∇)v = −∇p

ρ

∂v∂t

− ∇φ,

(40.6)

where viscosity has been omitted. We can rearrange this equation by using thefollowing identity from vector analysis:

(v · ∇)v = (∇ × v) × v + 1

2∇(v · v).

40-4

If we now deﬁne a new vector ﬁeld Ω, as the curl of v,

Ω = ∇ × v,

(40.7)

the vector identity can be written as

(v · ∇)v = Ω × v + 1

2∇v2,

and our equation of motion (40.6) becomes

+ Ω × v + 1

2 ∇v2 = −∇p

ρ

∂v∂t

− ∇φ.

(40.8)

You can verify that Eqs. (40.6) and (40.8) are equivalent by checking that thecomponents of the two sides of the equation are equal—and making use of (40.7).The vector ﬁeld Ω is called the vorticity. If the vorticity is zero everywhere,we say that the ﬂow is irrotational. We have already deﬁned in Section 3-5 athing called the circulation of a vector ﬁeld. The circulation around any closedloop in a ﬂuid is the line integral of the ﬂuid velocity, at a given instant of time,around that loop:

I

(Circulation) =

v · ds.

The circulation per unit area for an inﬁnitesimal loop is then—using Stokes’theorem—equal to ∇ × v. So the vorticity Ω is the circulation around a unitarea (perpendicular to the direction of Ω). It also follows that if you put a littlepiece of dirt—not an inﬁnitesimal point—at any place in the liquid it will rotatewith the angular velocity Ω/2. Try to see if you can prove that. You can alsocheck it out that for a bucket of water on a turntable, Ω is equal to twice thelocal angular velocity of the water.If we are interested only in the velocity ﬁeld, we can eliminate the pressurefrom our equations. Taking the curl of both sides of Eq. (40.8), remembering thatρ is a constant and that the curl of any gradient is zero, and using Eq. (40.3), weget

This equation, together with the equations

∂Ω∂t

+ ∇ × (Ω × v) = 0.

Ω = ∇ × v

(40.9)

(40.10)

and

∇ · v = 0,

(40.11)describes completely the velocity ﬁeld v. Mathematically speaking, if we knowΩ at some time, then we know the curl of the velocity vector, and we also knowthat its divergence is zero, so given the physical situation we have all we needto determine v everywhere. (It is just like the situation in magnetism where wehad ∇ · B = 0 and ∇ × B = j/0c2.) Thus, a given Ω determines v just as agiven j determines B. Then, knowing v, Eq. (40.9) tells us the rate of changeof Ω from which we can get the new Ω for the next instant. Using Eq. (40.10),again we ﬁnd the new v, and so on. You see how these equations contain all themachinery for calculating the ﬂow. Note, however, that this procedure gives thevelocity ﬁeld only; we have lost all information about the pressure.

We point out one special consequence of our equation. If Ω = 0 everywhereat any time t, ∂Ω/∂t also vanishes, so that Ω is still zero everywhere at t + ∆t.We have a solution to the equation; the ﬂow is permanently irrotational. If a ﬂowwas started with zero rotation, it would always have zero rotation. The equationsto be solved then are

∇ · v = 0,

∇ × v = 0.

They are just like the equations for the electrostatic or magnetostatic ﬁelds infree space. We will come back to them and look at some special problems later.40-5

Fig. 40-5. Streamlines in steady ﬂuid

ﬂow.

40-3 Steady ﬂow—Bernoulli’s theoremNow we want to return to the equation of motion, Eq. (40.8), but limitourselves to situations in which the ﬂow is「steady.」By steady ﬂow we meanthat at any one place in the ﬂuid the velocity never changes. The ﬂuid at anypoint is always replaced by new ﬂuid moving in exactly the same way. Thevelocity picture always looks the same—v is a static vector ﬁeld. In the sameway that we drew「ﬁeld lines」in magnetostatics, we can now draw lines whichare always tangent to the ﬂuid velocity as shown in Fig. 40-5. These lines arecalled streamlines. For steady ﬂow, they are evidently the actual paths of ﬂuidparticles. (In unsteady ﬂow the streamline pattern changes in time, and thestreamline pattern at any instant does not represent the path of a ﬂuid particle.)A steady ﬂow does not mean that nothing is happening—atoms in the ﬂuidare moving and changing their velocities. It only means that ∂v/∂t = 0. Then ifwe take the dot product of v into the equation of motion, the term v · (Ω × v)drops out, and we are left withv · ∇

+ φ + 1

(cid:26) p

(40.12)

(cid:27)

2 v2

= 0.

ρ

This equation says that for a small displacement in the direction of the ﬂuidvelocity the quantity inside the brackets doesn’t change. Now in steady ﬂow alldisplacements are along streamlines, so Eq. (40.12) tells us that for all the pointsalong a streamline, we can write

+ 1

pρ

2 v2 + φ = const (streamline).

(40.13)

This is Bernoulli’s theorem. The constant may in general be diﬀerent for diﬀerentstreamlines; all we know is that the left-hand side of Eq. (40.13) is the same allalong a given streamline. Incidentally, we may notice that for steady irrotationalmotion for which Ω = 0, the equation of motion (40.8) gives us the relation

(cid:26) p

ρ

∇

(cid:27)

+ 1

2 v2 + φ

= 0,

so that

+ 1

2 v2 + φ = const (everywhere).

pρ

(40.14)

It’s just like Eq. (40.13) except that now the constant has the same value through-out the ﬂuid.

Fig. 40-6. Fluid motion in a ﬂow tube.

The theorem of Bernoulli is in fact nothing more than a statement of theconservation of energy. A conservation theorem such as this gives us a lotof information about a ﬂow without our actually having to solve the detailedequations. Bernoulli’s theorem is so important and so simple that we would liketo show you how it can be derived in a way that is diﬀerent from the formalcalculations we have just used. Imagine a bundle of adjacent streamlines whichform a stream tube as sketched in Fig. 40-6. Since the walls of the tube consistof streamlines, no ﬂuid ﬂows out through the wall. Let’s call the area at one end40-6

of the stream tube A1, the ﬂuid velocity there v1, the density of the ﬂuid ρ1, andthe potential energy φ1. At the other end of the tube, we have the correspondingquantities A2, v2, ρ2, and φ2. Now after a short interval of time ∆t, the ﬂuidat A1 has moved a distance v1 ∆t, and the ﬂuid at A2 has moved a distance v2 ∆t[Fig. 40-6(b)]. The conservation of mass requires that the mass which entersthrough A1 must be equal to the mass which leaves through A2. These massesat these two ends must be the same:

∆M = ρ1A1v1 ∆t = ρ2A2v2 ∆t.

So we have the equality

ρ1A1v1 = ρ2A2v2.

(40.15)This equation tells us that the velocity varies inversely with the area of the streamtube if ρ is constant.Now we calculate the work done by the ﬂuid pressure. The work done onthe ﬂuid entering at A1 is p1A1v1 ∆t, and the work given up at A2 is p2A2v2 ∆t.The net work on the ﬂuid between A1 and A2 is, therefore,

p1A1v1 ∆t − p2A2v2 ∆t,

which must equal the increase in the energy of a mass ∆M of ﬂuid in going fromA1 to A2. In other words,

p1A1v1 ∆t − p2A2v2 ∆t = ∆M(E2 − E1),

(40.16)where E1 is the energy per unit mass of ﬂuid at A1, and E2 is the energy perunit mass at A2. The energy per unit mass of the ﬂuid can be written as

E = 1

2 v2 + φ + U,

where 12 v2 is the kinetic energy per unit mass, φ is the potential energy per unitmass, and U is an additional term which represents the internal energy per unitmass of ﬂuid. The internal energy might correspond, for example, to the thermalenergy in a compressible ﬂuid, or to chemical energy. All these quantities canvary from point to point. Using this form for the energies in (40.16), we have

p1A1v1 ∆t

∆M

− p2A2v2 ∆t

∆M

= 1

2 + φ2 + U2 − 12 v2

2 v2

1 − φ1 − U1.

But we have seen that ∆M = ρAv ∆t, so we get+ 1

+ 1

2 v2

1 + φ1 + U1 = p2ρ2

p1ρ1

2 + φ2 + U2,

2 v2

(40.17)

which is the Bernoulli result with an additional term for the internal energy. Ifthe ﬂuid is incompressible, the internal energy term is the same on both sides,and we get again that Eq. (40.14) holds along any streamline.

We consider now some simple examples in which the Bernoulli integral givesus a description of the ﬂow. Suppose we have water ﬂowing out of a hole near thebottom of a tank, as drawn in Fig. 40-7. We take a situation in which the ﬂowspeed vout at the hole is much larger than the ﬂow speed near the top of the tank;in other words, we imagine that the diameter of the tank is so large that we canneglect the drop in the liquid level. (We could make a more accurate calculationif we wished.) At the top of the tank the pressure is p0, the atmospheric pressure,and the pressure at the sides of the jet is also p0. Now we write our Bernoulliequation for a streamline, such as the one shown in the ﬁgure. At the top of thetank, we take v equal to zero and we also take the gravity potential φ to be zero.At the speed vout, and φ = −gh, so thatp0 = p0 + 1

out − ρgh,

or

2 ρv2

vout =p2gh.

(40.18)

40-7

Fig. 40-7. Flow from a tank.

Fig. 40-8. With a re-entrant dischargetube, the stream contracts to one-half thearea of the opening.

This velocity is just what we would get for something which falls the distance h. Itis not too surprising, since the water at the exit gains kinetic energy at the expenseof the potential energy of the water at the top. Do not get the idea, however, thatyou can ﬁgure out the rate that the ﬂuid ﬂows out of the tank by multiplying thisvelocity by the area of the hole. The ﬂuid velocities as the jet leaves the hole arenot all parallel to each other but have components inward toward the center of thestream—the jet is converging. After the jet has gone a little way, the contractionstops and the velocities do become parallel. So the total ﬂow is the velocity timesthe area at that point. In fact, if we have a discharge opening which is just a roundhole with a sharp edge, the jet contracts to 62 percent of the area of the hole.The reduced eﬀective area of the discharge varies for diﬀerent shapes of dischargetubes, and experimental contractions are available as tables of eﬄux coeﬃcients.If the discharge tube is re-entrant, as shown in Fig. 40-8, it is possible toprove in a most beautiful way that the eﬄux coeﬃcient is exactly 50 percent.We will give just a hint of how the proof goes. We have used the conservation ofenergy to get the velocity, Eq. (40.18), but there is also momentum conservationto consider. Since there is an outﬂow of momentum in the discharge jet, theremust be a force applied over the cross section of the discharge tube. Where doesthe force come from? The force must come from the pressure on the walls. Aslong as the eﬄux hole is small and away from the walls, the ﬂuid velocity nearthe walls of the tank will be very small. Therefore, the pressure on every face isalmost exactly the same as the static pressure in a ﬂuid at rest—from Eq. (40.14).Then the static pressure at any point on the side of the tank must be matchedby an equal pressure at the point on the opposite wall, except at the points onthe wall opposite the charge tube. If we calculate the momentum poured outthrough the jet by this pressure, we can show that the eﬄux coeﬃcient is 1/2.We cannot use this method for a discharge hole like that shown in Fig. 40-7,however, because the velocity increase along the wall right near the dischargearea gives a pressure fall which we are not able to calculate.

Let’s look at another example—a horizontal pipe with changing cross section,as shown in Fig. 40-9, with water ﬂowing in one end and out the other. Theconservation of energy, namely Bernoulli’s formula, says that the pressure is lowerin the constricted area where the velocity is higher. We can easily demonstratethis eﬀect by measuring the pressure at diﬀerent cross sections with small verticalcolumns of water attached to the ﬂow tube through holes small enough so thatthey do not disturb the ﬂow. The pressure is then measured by the height of waterin these vertical columns. The pressure is found to be less at the constrictionthan it is on either side. If the area beyond the constriction comes back to the40-8

Fig. 40-9. The pressure is lowest where

the velocity is highest.

same value it had before the constriction, the pressure rises again. Bernoulli’sformula would predict that the pressure downstream of the constriction shouldbe the same as it was upstream, but actually it is noticeably less. The reasonthat our prediction is wrong is that we have neglected the frictional, viscousforces which cause a pressure drop along the tube. Despite this pressure drop thepressure is deﬁnitely lower at the constriction (because of the increased speed)than it is on either side of it—as predicted by Bernoulli. The speed v2 mustcertainly exceed v1 to get the same amount of water through the narrower tube.So the water accelerates in going from the wide to the narrow part. The forcethat gives this acceleration comes from the drop in pressure.

We can check our results with another simple demonstration. Suppose wehave on a tank a discharge tube which throws a jet of water upward as shown inFig. 40-10. If the eﬄux velocity were exactly √2gh, the discharge water shouldrise to a level even with the surface of the water in the tank. Experimentally, itfalls somewhat short. Our prediction is roughly right, but again viscous frictionwhich has not been included in our energy conservation formula has resulted in aloss of energy.

Have you ever held two pieces of paper close together and tried to blow themapart? Try it! They come together. The reason, of course, is that the air has ahigher speed going through the constricted space between the sheets than it doeswhen it gets outside. The pressure between the sheets is lower than atmosphericpressure, so they come together rather than separating.

40-4 CirculationWe saw at the beginning of the last section that if we have an incompressible

ﬂuid with no circulation, the ﬂow satisﬁes the following two equations:

∇ · v = 0,

∇ × v = 0.

(40.19)They are the same as the equations of electrostatics or magnetostatics in emptyspace. The divergence of the electric ﬁeld is zero when there are no charges, andthe curl of the electrostatic ﬁeld is always zero. The curl of the magnetostatic ﬁeldis zero if there are no currents, and the divergence of the magnetic ﬁeld is alwayszero. Therefore, Eqs. (40.19) have the same solutions as the equations for E inelectrostatics or for B in magnetostatics. As a matter of fact, we have alreadysolved the problem of the ﬂow of a ﬂuid past a sphere, as an electrostatic analogy, inSection 12-5. The electrostatic analog is a uniform electric ﬁeld plus a dipole ﬁeld.The dipole ﬁeld is so adjusted that the ﬂow velocity normal to the surface of thesphere is zero. The same problem for the ﬂow past a cylinder can be worked out ina similar way by using a suitable line dipole with a uniform ﬂow ﬁeld. This solutionholds for a situation in which the ﬂuid velocity at large distances is constant—bothin magnitude and direction. The solution is sketched in Fig. 40-11(a).

There is another solution for the ﬂow around a cylinder when the conditionsare such that the ﬂuid at large distances moves in circles around the cylinder.The ﬂow is, then, circular everywhere, as in Fig. 40-11(b). Such a ﬂow has acirculation around the cylinder, although ∇× v is still zero in the ﬂuid. How canthere be circulation without a curl? We have a circulation around the cylinderbecause the line integral of v around any loop enclosing the cylinder is not zero.At the same time, the line integral of v around any closed path which does notinclude the cylinder is zero. We saw the same thing when we found the magneticﬁeld around a wire. The curl of B was zero outside of the wire, although a lineintegral of B around a path which encloses the wire did not vanish. The velocityﬁeld in an irrotational circulation around a cylinder is precisely the same as themagnetic ﬁeld around a wire. For a circular path with its center at the center ofthe cylinder, the line integral of the velocity is

I

v · ds = 2πrv.

For irrotational ﬂow the integral must be independent of r. Let’s call the constant40-9

√Fig. 40-10. Proof that v is not equal

2gh.

to

Fig. 40-11. (a) Ideal ﬂuid ﬂow past acylinder. (b) Circulation around a cylinder.(c) The superposition of (a) and (b).

Fig. 40-12. Water with circulation drain-

ing from a tank.

value C, then we have that

v = C2πr

,

(40.20)

where v is the tangential velocity, and r is the distance from the axis.There is a nice demonstration of a ﬂuid circulating around a hole. You take atransparent cylindrical tank with a drain hole in the center of the bottom. Youﬁll it with water, stir up some circulation with a stick, and pull the drain plug.You get the pretty eﬀect shown in Fig. 40-12. (You’ve seen a similar thing manytimes in the bathtub!) Although you put in some ω at beginning, it soon diesdown because of viscosity and the ﬂow becomes irrotational—although still withsome circulation around the hole.

From the theory, we can calculate the shape of the inner surface of the water.As a particle of the water moves inward it picks up speed. From Eq. (40.20)the tangential velocity goes as 1/r—it’s just from the conservation of angularmomentum, like the skater pulling in her arms. Also the radial velocity goesas 1/r. Ignoring the tangential motion, we have water going radially inwardtoward a hole; from ∇ · v = 0, it follows that the radial velocity is proportionalto 1/r. So the total velocity also increases as 1/r, and the water goes in alongArchimedean spirals. The air-water surface is all at atmospheric pressure, so itmust have—from Eq. (40.14)—the property that2 v2 = const.

gz + 1

But v is proportional to 1/r, so the shape of the surface is

(z − z0) = kr2 .

An interesting point—which is not true in general but is true for incompress-ible, irrotational ﬂow—is that if we have one solution and a second solution, thenthe sum is also a solution. This is true because the equations in (40.19) are linear.The complete equations of hydrodynamics, Eqs. (40.9), (40.10), and (40.11), arenot linear, which makes a vast diﬀerence. For the irrotational ﬂow about thecylinder, however, we can superpose the ﬂow of Fig. 40-11(a) on the ﬂow ofFig. 40-11(b) and get the new ﬂow pattern shown in Fig. 40-11(c). This ﬂow isof special interest. The ﬂow velocity is higher on the upper side of the cylinderthan on the lower side. The pressures are therefore lower on the upper side thanon the lower side. So when we have a combination of a circulation around acylinder and a net horizontal ﬂow, there is a net vertical force on the cylinder—itis called a lift force. Of course, if there is no circulation, there is no net force onany body according to our theory of「dry」water.

40-5 Vortex linesWe have already written down the general equations for the ﬂow of an

incompressible ﬂuid when there may be vorticity. They are

I. ∇ · v = 0,II. Ω = ∇ × v,III.

∂Ω∂t

+ ∇ × (Ω × v) = 0.

The physical content of these equations has been described in words by Helmholtzin terms of three theorems. First, imagine that in the ﬂuid we were to draw vortexlines rather than streamlines. By vortex lines we mean ﬁeld lines that have thedirection of Ω and have a density in any region proportional to the magnitudeof Ω. From II the divergence of Ω is always zero (remember—Section 3-7—thatthe divergence of a curl is always zero). So vortex lines are like lines of B—they never start or stop, and will tend to go in closed loops. Now Helmholtzdescribed III in words by the following statement: the vortex lines move with40-10

the ﬂuid. This means that if you were to mark the ﬂuid particles along somevortex lines—by coloring them with ink, for example—then as the ﬂuid movesand carries those particles along, they will always mark the new positions of thevortex lines. In whatever way the atoms of the liquid move, the vortex lines movewith them. That is one way to describe the laws.

It also suggests a method for solving any problems. Given the initial ﬂowpattern—say v everywhere—then you can calculate Ω. From the v you can alsotell where the vortex lines are going to be a little later—they move with thespeed v. With the new Ω you can use I and II to ﬁnd the new v. (That’s just likethe problem of ﬁnding B, given the currents.) If we are given the ﬂow pattern atone instant we can in principle calculate it for all subsequent times. We have thegeneral solution for nonviscous ﬂow.

We would like to show how Helmholtz’s statement—and, therefore, III—canbe at least partly understood. It is really just the law of conservation of angularmomentum applied to the ﬂuid. Suppose we imagine a small cylinder of the liquidwhose axis is parallel to the vortex lines, as in Fig. 40-13(a). At some time later,this same piece of ﬂuid will be somewhere else. Generally it will occupy a cylinderwith a diﬀerent diameter and be in a diﬀerent place. It may also have a diﬀerentorientation, say as in Fig. 40-13(b). If, however, the diameter has decreased asshown in Fig. 40-13, the length will have increased to keep the volume constant(since we are assuming an incompressible ﬂuid). Also, since the vortex lines arestuck with the material, their density will go up as the cross-sectional area goesdown. The product of the vorticity Ω and area A of the cylinder will remainconstant, so according to Helmholtz, we should have

Ω2A2 = Ω1A1.

(40.21)Now notice that with zero viscosity all the forces on the surface of thecylindrical volume (or any volume, for that matter) are perpendicular to thesurface. The pressure forces can cause the volume to be moved from place to place,or can cause it to change shape; but with no tangential forces the magnitudeof the angular momentum of the material inside cannot change. The angularmomentum of the liquid in the little cylinder is its moment of inertia I times theangular velocity of the liquid, which is proportional to the vorticity Ω. For acylinder, the moment of inertia is proportional to mr2. So from the conservationof angular momentum, we would conclude that1)Ω1 = (M2R2

(M1R2

2)Ω2.

Fig. 40-13. (a) A group of vortex linesat t; (b) the same lines at a later time t(cid:48).

But the mass is the same, M1 = M2, and the areas are proportional to R2,so we get again just Eq. (40.21). Helmholtz’s statement—which is equivalentto III—is just a consequence of the fact that in the absence of viscosity theangular momentum of an element of the ﬂuid cannot change.

Fig. 40-14. Making a travelling vortex ring.

There is a nice demonstration of a moving vortex which is made with thesimple apparatus of Fig. 40-14. It is a「drum」two feet in diameter and two feetlong made by stretching a thick rubber sheet over the open end of a cylindrical「box.」The「bottom」—the drum is tipped on its side—is solid except for a 3-inchdiameter hole. If you give a sharp blow on the rubber diaphragm with your hand,a vortex ring is projected out of the hole. Although the vortex is invisible, youcan tell it’s there because it will blow out a candle 10 to 20 feet away. By the40-11

delay in the eﬀect, you can tell that「something」is travelling at a ﬁnite speed.You can see better what is going on if you ﬁrst blow some smoke into the box.Then you see the vortex as a beautiful round「smoke ring.」The smoke ring is a torus-shaped bundle of vortex lines, as shown inFig. 40-15(a). Since Ω = ∇ × v, these vortex lines represent also a circula-tion of v as shown in part (b) of the ﬁgure. We can understand the forwardmotion of the ring in the following way: The circulating velocity around thebottom of the ring extends up to the top of the ring, having there a forwardmotion. Since the lines of Ω move with the ﬂuid, they also move ahead with thevelocity v. (Of course, the circulation of v around the top part of the ring isresponsible for the forward motion of the vortex lines at the bottom.)We must now mention a serious diﬃculty. We have already noted thatEq. (40.9) says that, if Ω is initially zero, it will always be zero. This result is agreat failure of the theory of「dry」water, because it means that once Ω is zero itis always zero—it is impossible to produce any vorticity under any circumstance.Yet, in our simple demonstration with the drum, we can generate a vortex ringstarting with air which was initially at rest. (Certainly, v = 0, Ω = 0 everywherein the box before we hit it.) Also, we all know that we can start some vorticityin a lake with a paddle. Clearly, we must go to a theory of「wet」water to get acomplete understanding of the behavior of a ﬂuid.

Another feature of the dry water theory which is incorrect is the suppositionwe make regarding the ﬂow at the boundary between it and the surface of a solid.When we discussed the ﬂow past a cylinder—as in Fig. 40-11, for example—wepermitted the ﬂuid to slide along the surface of the solid. In our theory, thevelocity at a solid surface could have any value depending on how it got started,and we did not consider any「friction」between the ﬂuid and the solid. It is anexperimental fact, however, that the velocity of a real ﬂuid always goes to zeroat the surface of a solid object. Therefore, our solution for the cylinder, withor without circulation, is wrong—as is our result regarding the generation ofvorticity. We will tell you about the more correct theories in the next chapter.

Fig. 40-15. A moving vortex ring (asmoke ring). (a) The vortex lines. (b) Across section of the ring.

40-12

41-1 Viscosity41-2 Viscous ﬂow41-3 The Reynolds number41-4 Flow past a circular cylinder41-5 The limit of zero viscosity41-6 Couette ﬂow

41

The Flow of Wet Water

