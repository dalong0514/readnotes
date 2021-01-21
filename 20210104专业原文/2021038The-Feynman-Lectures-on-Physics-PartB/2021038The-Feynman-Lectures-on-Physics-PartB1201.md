# 1201

12-1 The same equations have the

same solutions

12-2 The ﬂow of heat; a point sourcenear an inﬁnite plane boundary

12-3 The stretched membrane12-4 The diﬀusion of neutrons; auniform spherical source in ahomogeneous medium

12-5 Irrotational ﬂuid ﬂow; the ﬂow

past a sphere

12-6 Illumination; the uniform

lighting of a plane

12-7 The「underlying unity」of nature

12

Electrostatic Analogs

12-1 The same equations have the same solutionsThe

total amount of information which has been acquired about the physicalworld since the beginning of scientiﬁc progress is enormous, and it seems almostimpossible that any one person could know a reasonable fraction of it. But it isactually quite possible for a physicist to retain a broad knowledge of the physicalworld rather than to become a specialist in some narrow area. The reasons forthis are threefold: First, there are great principles which apply to all the diﬀerentkinds of phenomena—such as the principles of the conservation of energy andof angular momentum. A thorough understanding of such principles gives anunderstanding of a great deal all at once. Second, there is the fact that manycomplicated phenomena, such as the behavior of solids under compression, reallybasically depend on electrical and quantum-mechanical forces, so that if oneunderstands the fundamental laws of electricity and quantum mechanics, there isat least some possibility of understanding many of the phenomena that occurin complex situations. Finally, there is a most remarkable coincidence: Theequations for many diﬀerent physical situations have exactly the same appearance.Of course, the symbols may be diﬀerent—one letter is substituted for another—but the mathematical form of the equations is the same. This means that havingstudied one subject, we immediately have a great deal of direct and preciseknowledge about the solutions of the equations of another.

We are now ﬁnished with the subject of electrostatics, and will soon go on tostudy magnetism and electrodynamics. But before doing so, we would like toshow that while learning electrostatics we have simultaneously learned about alarge number of other subjects. We will ﬁnd that the equations of electrostaticsappear in several other places in physics. By a direct translation of the solutions(of course the same mathematical equations must have the same solutions) it ispossible to solve problems in other ﬁelds with the same ease—or with the samediﬃculty—as in electrostatics.

The equations of electrostatics, we know, are∇ · (κE) = ρfree0∇ × E = 0.

,

(12.1)

(12.2)

(12.3)

(We take the equations of electrostatics with dielectrics so as to have the mostgeneral situation.) The same physics can be expressed in another mathematicalform:

E = −∇φ,

∇ · (κ∇φ) = − ρfree0

.

(12.4)

Now the point is that there are many physics problems whose mathematical equa-tions have the same form. There is a potential (φ) whose gradient multiplied by ascalar function (κ) has a divergence equal to another scalar function (−ρfree/0).Whatever we know about electrostatics can immediately be carried over intothat other subject, and vice versa. (It works both ways, of course—if the othersubject has some particular characteristics that are known, then we can applythat knowledge to the corresponding electrostatic problem.) We want to considera series of examples from diﬀerent subjects that produce equations of this form.12-1

12-2 The ﬂow of heat; a point source near an inﬁnite plane boundaryWe have discussed one example earlier (Section 3-4)—the ﬂow of heat. Imaginea block of material, which need not be homogeneous but may consist of diﬀerentmaterials at diﬀerent places, in which the temperature varies from point to point.As a consequence of these temperature variations there is a ﬂow of heat, whichcan be represented by the vector h. It represents the amount of heat energywhich ﬂows per unit time through a unit area perpendicular to the ﬂow. Thedivergence of h represents the rate per unit volume at which heat is leaving aregion:

∇ · h = rate of heat out per unit volume.

(We could, of course, write the equation in integral form—just as we did inelectrostatics with Gauss’ law—which would say that the ﬂux through a surfaceis equal to the rate of change of heat energy inside the material. We will notbother to translate the equations back and forth between the diﬀerential and theintegral forms, because it goes exactly the same as in electrostatics.)

The rate at which heat is generated or absorbed at various places depends,of course, on the problem. Suppose, for example, that there is a source of heatinside the material (perhaps a radioactive source, or a resistor heated by anelectrical current). Let us call s the heat energy produced per unit volume persecond by this source. There may also be losses (or gains) of thermal energy toother internal energies in the volume. If u is the internal energy per unit volume,−du/dt will also be a「source」of heat energy. We have, then,

∇ · h = s − dudt

.

(12.5)

We are not going to discuss just now the complete equation in which thingschange with time, because we are making an analogy to electrostatics, wherenothing depends on the time. We will consider only steady heat-ﬂow problems,in which constant sources have produced an equilibrium state. In these cases,

∇ · h = s.

(12.6)

It is, of course, necessary to have another equation, which describes how theheat ﬂows at various places. In many materials the heat current is approximatelyproportional to the rate of change of the temperature with position: the largerthe temperature diﬀerence, the more the heat current. As we have seen, thevector heat current is proportional to the temperature gradient. The constant ofproportionality K, a property of the material, is called the thermal conductivity.(12.7)If the properties of the material vary from place to place, then K = K(x, y, z),a function of position. [Equation (12.7) is not as fundamental as (12.5), whichexpresses the conservation of heat energy, since the former depends upon a specialproperty of the substance.] If now we substitute Eq. (12.7) into Eq. (12.6) wehave

h = −K ∇T.

∇ · (K ∇T) = −s,

(12.8)which has exactly the same form as (12.4). Steady heat-ﬂow problems andelectrostatic problems are the same. The heat ﬂow vector h corresponds to E,and the temperature T corresponds to φ. We have already noticed that a pointheat source produces a temperature ﬁeld which varies as 1/r and a heat ﬂowwhich varies as 1/r2. This is nothing more than a translation of the statementsfrom electrostatics that a point charge generates a potential which varies as 1/rand an electric ﬁeld which varies as 1/r2. We can, in general, solve static heatproblems as easily as we can solve electrostatic problems.Consider a simple example. Suppose that we have a cylinder of radius a atthe temperature T1, maintained by the generation of heat in the cylinder. (Itcould be, for example, a wire carrying a current, or a pipe with steam condensing12-2

inside.) The cylinder is covered with a concentric sheath of insulating materialwhich has a conductivity K. Say the outside radius of the insulation is b and theoutside is kept at temperature T2 (Fig. 12-1a). We want to ﬁnd out at what rateheat will be lost by the wire, or steampipe, or whatever it is in the center. Letthe total amount of heat lost from a length L of the pipe be called G—which iswhat we are trying to ﬁnd.How can we solve this problem? We have the diﬀerential equations, butsince these are the same as those of electrostatics, we have really already solvedthe mathematical problem. The analogous problem is that of a conductor ofradius a at the potential φ1, separated from another conductor of radius b at thepotential φ2, with a concentric layer of dielectric material in between, as drawnin Fig. 12-1(b). Now since the heat ﬂow h corresponds to the electric ﬁeld E,the quantity G that we want to ﬁnd corresponds to the ﬂux of the electric ﬁeldfrom a unit length (in other words, to the electric charge per unit length over 0).We have solved the electrostatic problem by using Gauss’ law. We follow thesame procedure for our heat-ﬂow problem.

From the symmetry of the situation, we know that h depends only on thedistance from the center. So we enclose the pipe in a gaussian cylinder of length Land radius r. From Gauss’ law, we know that the heat ﬂow h multiplied by thearea 2πrL of the surface must be equal to the total amount of heat generatedinside, which is what we are calling G:

2πrLh = G

or

h = G2πrL

.

(12.9)

The heat ﬂow is proportional to the temperature gradient:

h = −K ∇T,or, in this case, the radial component of h is

h = −K

dTdr

.

This, together with (12.9), gives

Integrating from r = a to r = b, we get

dTdr

= − G

2πKLr

.

Solving for G, we ﬁnd

T2 − T1 = − G

2πKL

ln ba

.

G = 2πKL(T1 − T2)

ln(b/a)

.

(12.10)

(12.11)

(12.12)

Fig. 12-1. (a) Heat ﬂow in a cylindricalgeometry. (b) The corresponding electricalproblem.

This result corresponds exactly to the result for the charge on a cylindricalcondenser:

Q = 2π0L(φ1 − φ2)

.

ln(b/a)

The problems are the same, and they have the same solutions. From our knowledgeof electrostatics, we also know how much heat is lost by an insulated pipe.

Let’s consider another example of heat ﬂow. Suppose we wish to know theheat ﬂow in the neighborhood of a point source of heat located a little waybeneath the surface of the earth, or near the surface of a large metal block. Thelocalized heat source might be an atomic bomb that was set oﬀ underground,leaving an intense source of heat, or it might correspond to a small radioactivesource inside a block of iron—there are numerous possibilities.

We will treat the idealized problem of a point heat source of strength Gat the distance a beneath the surface of an inﬁnite block of uniform materialwhose thermal conductivity is K. And we will neglect the thermal conductivity12-3

of the air outside the material. We want to determine the distribution of thetemperature on the surface of the block. How hot is it right above the sourceand at various places on the surface of the block?

How shall we solve it? It is like an electrostatic problem with two materialswith diﬀerent dielectric coeﬃcients κ on opposite sides of a plane boundary. Aha!Perhaps it is the analog of a point charge near the boundary between a dielectricand a conductor, or something similar. Let’s see what the situation is near thesurface. The physical condition is that the normal component of h on the surfaceis zero, since we have assumed there is no heat ﬂow out of the block. We shouldask: In what electrostatic problem do we have the condition that the normalcomponent of the electric ﬁeld E (which is the analog of h) is zero at a surface?There is none!That is one of the things that we have to watch out for. For physical reasons,there may be certain restrictions in the kinds of mathematical conditions whicharise in any one subject. So if we have analyzed the diﬀerential equation only forcertain limited cases, we may have missed some kinds of solutions that can occurin other physical situations. For example, there is no material with a dielectricconstant of zero, whereas a vacuum does have zero thermal conductivity. Sothere is no electrostatic analogy for a perfect heat insulator. We can, however,still use the same methods. We can try to imagine what would happen if thedielectric constant were zero. (Of course, the dielectric constant is never zero inany real situation. But we might have a case in which there is a material with avery high dielectric constant, so that we could neglect the dielectric constant ofthe air outside.)How shall we ﬁnd an electric ﬁeld that has no component perpendicular to thesurface? That is, one which is always tangent at the surface? You will notice thatour problem is opposite to the one of a point charge near a plane conductor. Therewe wanted the ﬁeld to be perpendicular to the surface, because the conductorwas all at the same potential. In the electrical problem, we invented a solution byimagining a point charge behind the conducting plate. We can use the same ideaagain. We try to pick an「image source」that will automatically make the normalcomponent of the ﬁeld zero at the surface. The solution is shown in Fig. 12-2.An image source of the same sign and the same strength placed at the distance aabove the surface will cause the ﬁeld to be always horizontal at the surface. Thenormal components of the two sources cancel out.

Thus our heat ﬂow problem is solved. The temperature everywhere is thesame, by direct analogy, as the potential due to two equal point charges! Thetemperature T at the distance r from a single point source G in an inﬁnitemedium is

(12.13)(This, of course, is just the analog of φ = q/4π0R.) The temperature for a pointsource, together with its image source, is

T = G4πKr

.

T = G

4πKr1

+ G

4πKr2

.

(12.14)

Fig. 12-2. The heat ﬂow and isothermalsnear a point heat source at the distance abelow the surface of a good thermal con-ductor.

This formula gives us the temperature everywhere in the block. Several isothermalsurfaces are shown in Fig. 12-2. Also shown are lines of h, which can be obtainedfrom h = −K ∇T.We originally asked for the temperature distribution on the surface. For a

point on the surface at the distance ρ from the axis, r1 = r2 =pρ2 + a2, so

.

(12.15)

T(surface) = 14πK

2Gpρ2 + a2

This function is also shown in the ﬁgure. The temperature is, naturally, higherright above the source than it is farther away. This is the kind of problem thatgeophysicists often need to solve. We now see that it is the same kind of thingwe have already been solving for electricity.

12-4

12-3 The stretched membraneNow let us consider a completely diﬀerent physical situation which, nev-ertheless, gives the same equations again. Consider a thin rubber sheet—amembrane—which has been stretched over a large horizontal frame (like a drum-head). Suppose now that the membrane is pushed up in one place and down inanother; as shown in Fig. 12-3. Can we describe the shape of the surface? Wewill show how the problem can be solved when the deﬂections of the membraneare not too large.

There are forces in the sheet because it is stretched. If we were to make asmall cut anywhere, the two sides of the cut would pull apart (see Fig. 12-4). Sothere is a surface tension in the sheet, analogous to the one-dimensional tensionin a stretched string. We deﬁne the magnitude of the surface tension τ as theforce per unit length which will just hold together the two sides of a cut such asone of those shown in Fig. 12-4.Suppose now that we look at a vertical cross section of the membrane. It willappear as a curve, like the one in Fig. 12-5. Let u be the vertical displacementof the membrane from its normal position, and x and y the coordinates in thehorizontal plane. (The cross section shown is parallel to the x-axis.)Consider a little piece of the surface of length ∆x and width ∆y. There willbe forces on the piece from the surface tension along each edge. The force alongedge 1 of the ﬁgure will be τ1 ∆y, directed tangent to the surface—that is, atthe angle θ1 from the horizontal. Along edge 2, the force will be τ2 ∆y at theangle θ2. (There will be similar forces on the other two edges of the piece, butwe will forget them for the moment.) The net upward force on the piece fromedges 1 and 2 is

∆F = τ2 ∆y sin θ2 − τ1 ∆y sin θ1.

We will limit our considerations to small distortions of the membrane, i.e., tosmall slopes: we can then replace sin θ by tan θ, which can be written as ∂u/∂x.The force is then

The quantity in brackets can be equally well written (for small ∆x) as

(cid:20)

∆F =

τ2

(cid:18) ∂u

(cid:19)

(cid:21)

∂x

1

∆y.

− τ1

2

∂x

(cid:19)

(cid:18) ∂u(cid:18)(cid:18)

∂∂x

τ

(cid:19)(cid:19)

∂u∂x

∆x;

∆F = ∂∂x

τ

∂u∂x

∆x ∆y.

then

There will be another contribution to ∆F from the forces on the other two

edges; the total is evidently

(cid:19)

(cid:18)

(cid:19)(cid:21)

(cid:20) ∂

(cid:18)

∂x

∆F =

τ

∂u∂x

+ ∂∂y

τ

∂u∂y

∆x ∆y.

(12.16)

The distortions of the diaphragm are caused by external forces. Let’s let frepresent the upward force per unit area on the sheet (a kind of「pressure」) fromthe external forces. When the membrane is in equilibrium (the static case), thisforce must be balanced by the internal force we have just computed, Eq. (12.16).That is

f = − ∆F∆x ∆y

.

Equation (12.16) can then be written

f = −∇ · (τ ∇u),

(12.17)where by ∇ we now mean, of course, the two-dimensional gradient operator(∂/∂x, ∂/∂y). We have the diﬀerential equation that relates u(x, y) to the applied12-5

Fig. 12-3. A thin rubber sheet stretchedover a cylindrical frame (like a drumhead).If the sheet is pushed up at A and downat B, what is the shape of the surface?

Fig. 12-4. The surface tension τ of astretched rubber sheet is the force per unitlength across a line.

Fig. 12-5. Cross section of the deﬂected

sheet.

forces f(x, y) and the surface tension τ(x, y), which may, in general, vary fromplace to place in the sheet. (The distortions of a three-dimensional elastic bodyare also governed by similar equations, but we will stick to two-dimensions.) Wewill worry only about the case in which the tension τ is constant throughout thesheet. We can then write for Eq. (12.17),

∇2u = − fτ

.

(12.18)

We have another equation that is the same as for electrostatics!—only thistime, limited to two-dimensions. The displacement u corresponds to φ, and f /τcorresponds to ρ/0. So all the work we have done for inﬁnite plane chargedsheets, or long parallel wires, or charged cylinders is directly applicable to thestretched membrane.

Suppose we push the membrane at some points up to a deﬁnite height—thatis, we ﬁx the value of u at some places. That is the analog of having a deﬁnitepotential at the corresponding places in an electrical situation. So, for instance,we may make a positive「potential」by pushing up on the membrane with anobject having the cross-sectional shape of the corresponding cylindrical conductor.For example, if we push the sheet up with a round rod, the surface will takeon the shape shown in Fig. 12-6. The height u is the same as the electrostaticpotential φ of a charged cylindrical rod. It falls oﬀ as ln(1/r). (The slope, whichcorresponds to the electric ﬁeld E, drops oﬀ as 1/r.)

Fig. 12-6. Cross section of a stretchedrubber sheet pushed up by a round rod. Thefunction u(x, y ) is the same as the electricpotential φ(x, y ) near a very long chargesrod.

The stretched rubber sheet has often been used as a way of solving complicatedelectrical problems experimentally. The analogy is used backwards! Various rodsand bars are pushed against the sheet to heights that correspond to the potentialsof a set of electrodes. Measurements of the height then give the electrical potentialfor the electrical situation. The analogy has been carried even further. If littleballs are placed on the membrane, their motion corresponds approximately to themotion of electrons in the corresponding electric ﬁeld. One can actually watchthe「electrons」move on their trajectories. This method was used to design thecomplicated geometry of many photomultiplier tubes (such as the ones used forscintillation counters, and the one used for controlling the headlight beams onCadillacs). The method is still used, but the accuracy is limited. For the mostaccurate work, it is better to determine the ﬁelds by numerical methods, usingthe large electronic computing machines.

12-4 The diﬀusion of neutrons; a uniform spherical source in a homogeneous

medium

We take another example that gives the same kind of equation, this timehaving to do with diﬀusion. In Chapter 43 of Vol. I we considered the diﬀusionof ions in a single gas, and of one gas through another. This time, let’s takea diﬀerent example—the diﬀusion of neutrons in a material like graphite. Wechoose to speak of graphite (a pure form of carbon) because carbon doesn’tabsorb slow neutrons. In it the neutrons are free to wander around. They travelin a straight line for several centimeters, on the average, before being scattered bya nucleus and deﬂected into a new direction. So if we have a large block—manymeters on a side—the neutrons initially at one place will diﬀuse to other places.We want to ﬁnd a description of their average behavior—that is, their averageﬂow.

12-6

Let N(x, y, z) ∆V be the number of neutrons in the element of volume ∆Vat the point (x, y, z). Because of their motion, some neutrons will be leaving ∆V ,and others will be coming in. If there are more neutrons in one region than ina nearby region, more neutrons will go from the ﬁrst region to the second thancome back; there will be a net ﬂow. Following the arguments of Chapter 43in Vol. I, we describe the ﬂow by a ﬂow vector J. Its x-component Jx is thenet number of neutrons that pass in unit time a unit area perpendicular to thex-direction. We found that

(12.19)where the diﬀusion constant D is given in terms of the mean velocity v, and themean-free-path l between scatterings is given by

Jx = −D

∂N∂x

,

D = 1

3 lv.

The vector equation for J is

J = −D ∇N.

(12.20)The rate at which neutrons ﬂow across any surface element da is J · n da(where, as usual, n is the unit normal). The net ﬂow out of a volume element isthen (following the usual gaussian argument) ∇ · J dV . This ﬂow would resultin a decrease with time of the number in ∆V unless neutrons are being createdin ∆V (by some nuclear process). If there are sources in the volume that generateS neutrons per unit time in a unit volume, then the net ﬂow out of ∆V will beequal to (S − ∂N/∂t) ∆V . We have then that∇ · J = S − ∂N∂t

(12.21)

.

Combining (12.21) with (12.20), we get the neutron diﬀusion equation

∇ · (−D ∇N) = S − ∂N∂t

.

(12.22)

In the static case—where ∂N/∂t = 0—we have Eq. (12.4) all over again! Wecan use our knowledge of electrostatics to solve problems about the diﬀusion ofneutrons. So let’s solve a problem. (You may wonder: Why do a problem if wehave already done all the problems in electrostatics? We can do it faster thistime because we have done the electrostatic problems!)Suppose we have a block of material in which neutrons are being generated—say by uranium ﬁssion—uniformly throughout a spherical region of radius a(Fig. 12-7). We would like to know: What is the density of neutrons everywhere?How uniform is the density of neutrons in the region where they are beinggenerated? What is the ratio of the neutron density at the center to the neutrondensity at the surface of the source region? Finding the answers is easy. Thesource density S0 replaces the charge density ρ, so our problem is the same asthe problem of a sphere of uniform charge density. Finding N is just like ﬁndingthe potential φ. We have already worked out the ﬁelds inside and outside of auniformly charged sphere; we can integrate them to get the potential. Outside,the potential is Q/4π0r, with the total charge Q given by 4πa3ρ/3. So

φoutside = ρa330r

.

(12.23)

For points inside, the ﬁeld is due only to the charge Q(r) inside the sphere ofradius r, Q(r) = 4πr3ρ/3, so

The ﬁeld increases linearly with r. Integrating E to get φ, we have

E = ρr30

.

(12.24)

φinside = − ρr260

+ a constant.

12-7

Fig. 12-7. (a) Neutrons are produced uni-formly throughout a sphere of radius a ina large graphite block and diﬀuse outward.The neutron density N is found as a functionof r, the distance from the center of thesource. (b) The analogous electrostatic sit-uation: a uniform sphere of charge, where Ncorresponds to φ and J corresponds to E.

At the radius a, φinside must be the same as φoutside, so the constant mustbe ρa2/20. (We are assuming that φ is zero at large distances from the source,which will correspond to N being zero for the neutrons.) Therefore,

(cid:18)3a22 − r22

(cid:19)

.

φinside = ρ30

(12.25)

We know immediately the neutron density in our other problem. The answer

is

and

,

Noutside = Sa3(cid:18)3a23Dr2 − r22

Ninside = S3D

(cid:19)

.

(12.26)

(12.27)

N is shown as a function of r in Fig. 12-7.Now what is the ratio of density at the center to that at the edge? At thecenter (r = 0), it is proportional to 3a2/2. At the edge (r = a) it is proportionalto 2a2/2, so the ratio of densities is 3/2. A uniform source doesn’t produce auniform density of neutrons. You see, our knowledge of electrostatics gives us agood start on the physics of nuclear reactors.

There are many physical circumstances in which diﬀusion plays a big part.The motion of ions through a liquid, or of electrons through a semiconductor,obeys the same equation. We ﬁnd again and again the same equations.

12-5 Irrotational ﬂuid ﬂow; the ﬂow past a sphereLet’s now consider an example which is not really a very good one, because theequations we will use will not really represent the subject with complete generalitybut only in an artiﬁcial idealized situation. We take up the problem of waterﬂow. In the case of the stretched sheet, our equations were an approximationwhich was correct only for small deﬂections. For our consideration of water ﬂow,we will not make that kind of an approximation; we must make restrictions thatdo not apply at all to real water. We treat only the case of the steady ﬂow of anincompressible, nonviscous, circulation-free liquid. Then we represent the ﬂow bygiving the velocity v(r) as a function of position r. If the motion is steady (theonly case for which there is an electrostatic analog) v is independent of time. Ifρ is the density of the ﬂuid, then ρv is the amount of mass which passes per unittime through a unit area. By the conservation of matter, the divergence of ρvwill be, in general, the time rate of change of the mass of the material per unitvolume. We will assume that there are no processes for the continuous creation ordestruction of matter. The conservation of matter then requires that ∇ · ρv = 0.(It should, in general, be equal to −∂ρ/∂t, but since our ﬂuid is incompressible,ρ cannot change.) Since ρ is everywhere the same, we can factor it out, and ourequation is simply

∇ · v = 0.

Good! We have electrostatics again (with no charges); it’s just like ∇ · E = 0.Not so! Electrostatics is not simply ∇ · E = 0. It is a pair of equations. Oneequation does not tell us enough; we need still an additional equation. Tomatch electrostatics, we should have also that the curl of v is zero. But thatis not generally true for real liquids. Most liquids will ordinarily develop somecirculation. So we are restricted to the situation in which there is no circulationof the ﬂuid. Such ﬂow is often called irrotational. Anyway, if we make all ourassumptions, we can imagine a case of ﬂuid ﬂow that is analogous to electrostatics.So we take

∇ · v = 0

(12.28)

and

∇ × v = 0.

(12.29)

12-8

We want to emphasize that the number of circumstances in which liquidﬂow follows these equations is far from the great majority, but there are a few.They must be cases in which we can neglect surface tension, compressibility,and viscosity, and in which we can assume that the ﬂow is irrotational. Theseassumptions are valid so rarely for real water that the mathematician Johnvon Neumann said that people who analyze Eqs. (12.28) and (12.29) are studying「dry water」! (We take up the problem of ﬂuid ﬂow in more detail in Chapters 40and 41.)Because ∇× v = 0, the velocity of「dry water」can be written as the gradient(12.30)What is the physical meaning of ψ? There isn’t any very useful meaning. Thevelocity can be written as the gradient of a potential simply because the ﬂow isirrotational. And by analogy with electrostatics, ψ is called the velocity potential,but it is not related to a potential energy in the way that φ is. Since the divergenceof v is zero, we have

of some potential:

v = −∇ψ.

∇ · (∇ψ) = ∇2ψ = 0.

(12.31)The velocity potential ψ obeys the same diﬀerential equation as the electrostaticpotential in free space (ρ = 0).

Let’s pick a problem in irrotational ﬂow and see whether we can solve it by themethods we have learned. Consider the problem of a spherical ball falling througha liquid. If it is going too slowly, the viscous forces, which we are disregarding,will be important. If it is going too fast, little whirlpools (turbulence) will appearin its wake and there will be some circulation of the water. But if the ball isgoing neither too fast nor too slow, it is more or less true that the water ﬂow willﬁt our assumptions, and we can describe the motion of the water by our simpleequations.

It is convenient to describe what happens in a frame of reference ﬁxed in thesphere. In this frame we are asking the question: How does water ﬂow past asphere at rest when the ﬂow at large distances is uniform? That is, when, far fromthe sphere, the ﬂow is everywhere the same. The ﬂow near the sphere will be asshown by the streamlines drawn in Fig. 12-8. These lines, always parallel to v,correspond to lines of electric ﬁeld. We want to get a quantitative description forthe velocity ﬁeld, i.e., an expression for the velocity at any point P.

We can ﬁnd the velocity from the gradient of ψ, so we ﬁrst work out thepotential. We want a potential that satisﬁes Eq. (12.31) everywhere, and whichalso satisﬁes two restrictions: (1) there is no ﬂow in the spherical region inside thesurface of the ball, and (2) the ﬂow is constant at large distances. To satisfy (1),the component of v normal to the surface of the sphere must be zero. Thatmeans that ∂ψ/∂r is zero at r = a. To satisfy (2), we must have ∂ψ/∂z = v0 atall points where r (cid:29) a. Strictly speaking, there is no electrostatic case whichcorresponds exactly to our problem. It really corresponds to putting a sphereof dielectric constant zero in a uniform electric ﬁeld. If we had worked out thesolution to the problem of a sphere of a dielectric constant κ in a uniform ﬁeld,then by putting κ = 0 we would immediately have the solution to this problem.We have not actually worked out this particular electrostatic problem in detail,but let’s do it now. (We could work directly on the ﬂuid problem with v and ψ,but we will use E and φ because we are so used to them.)The problem is: Find a solution of ∇2φ = 0 such that E = −∇φ is a constant,say E0, for large r, and such that the radial component of E is equal to zeroat r = a. That is,

(cid:12)(cid:12)(cid:12)(cid:12)r=a

∂φ∂r

= 0.

(12.32)

Our problem involves a new kind of boundary condition, not one for which φis a constant on a surface, but for which ∂φ/∂r is a constant. That is a littlediﬀerent. It is not easy to get the answer immediately. First of all, withoutthe sphere, φ would be −E0z. Then E would be in the z-direction and have12-9

Fig. 12-8. The velocity ﬁeld of irrota-

tional ﬂuid ﬂow past a sphere.

the constant magnitude E0, everywhere. Now we have analyzed the case of adielectric sphere which has a uniform polarization inside it, and we found thatthe ﬁeld inside such a polarized sphere is a uniform ﬁeld, and that outside itis the same as the ﬁeld of a point dipole located at the center. So let’s guessthat the solution we want is a superposition of a uniform ﬁeld plus the ﬁeld of adipole. The potential of a dipole (Chapter 6) is pz/4π0r3. Thus we assume that(12.33)

φ = −E0z + pz

4π0r3 .

Since the dipole ﬁeld falls oﬀ as 1/r3, at large distances we have just the ﬁeld E0.Our guess will automatically satisfy condition (2) above. But what do we takefor the dipole strength p? To ﬁnd out, we may use the other condition on φ,Eq. (12.32). We must diﬀerentiate φ with respect to r, but of course we must doso at a constant angle θ, so it is more convenient if we ﬁrst express φ in terms ofr and θ, rather than of z and r. Since z = r cos θ, we get

φ = −E0r cos θ + p cos θ4π0r2 .

The radial component of E is− ∂φ∂r

= +E0 cos θ + p cos θ2π0r3 .This must be zero at r = a for all θ. This will be true if

(12.34)

(12.35)

p = −2π0a3E0.

(12.36)Note carefully that if both terms in Eq. (12.35) had not had the same θ-dependence, it would not have been possible to choose p so that (12.35) turnedout to be zero at r = a for all angles. The fact that it works out means thatwe have guessed wisely in writing Eq. (12.33). Of course, when we made theguess we were looking ahead; we knew that we would need another term that(a) satisﬁed ∇2φ = 0 (any real ﬁeld would do that), (b) dependent on cos θ, and(c) fell to zero at large r. The dipole ﬁeld is the only one that does all three.

Using (12.36), our potential is

(cid:19)(cid:19)

(cid:18)r + a32r2(cid:18)r + a32r2

.

.

(12.37)

(12.38)

The solution of the ﬂuid ﬂow problem can be written simply as

φ = −E0 cos θ

ψ = −v0 cos θ

It is straightforward to ﬁnd v from this potential. We will not pursue the matterfurther.

12-6 Illumination; the uniform lighting of a planeIn this section we turn to a completely diﬀerent physical problem—we wantto illustrate the great variety of possibilities. This time we will do something thatleads to the same kind of integral that we found in electrostatics. (If we have amathematical problem which gives us a certain integral, then we know somethingabout the properties of that integral if it is the same integral that we had todo for another problem.) We take our example from illumination engineering.Suppose there is a light source at the distance a above a plane surface. Whatis the illumination of the surface? That is, what is the radiant energy per unittime arriving at a unit area of the surface? (See Fig. 12-9.) We suppose that thesource is spherically symmetric, so that light is radiated equally in all directions.Then the amount of radiant energy which passes through a unit area at rightangles to a light ﬂow varies inversely as the square of the distance. It is evident12-10

Fig. 12-9. The illumination In of a surfaceis the radiant energy per unit time arrivingat a unit area of the surface.

that the intensity of the light in the direction normal to the ﬂow is given by thesame kind of formula as for the electric ﬁeld from a point source. If the light raysmeet the surface at an angle θ to the normal, then In, the energy arriving perunit area of the surface, is only cos θ as great, because the same energy goes ontoan area larger by 1/ cos θ. If we call the strength of our light source S, then In,the illumination of a surface, is

In = S

r2 er · n,

(12.39)

where er is the unit vector from the source and n is the unit normal to thesurface. The illumination In corresponds to the normal component of the electricﬁeld from a point charge of strength 4π0S. Knowing that, we see that for anydistribution of light sources, we can ﬁnd the answer by solving the correspondingelectrostatic problem. We calculate the vertical component of electric ﬁeld onthe plane due to a distribution of charge in the same way as for that of the lightsources.*

Consider the following example. We wish for some special experimentalsituation to arrange that the top surface of a table will have a very uniformillumination. We have available long tubular ﬂuorescent lights which radiateuniformly along their lengths. We can illuminate the table by placing theﬂuorescent tubes in a regular array on the ceiling, which is at the height z abovethe table. What is the widest spacing b from tube to tube that we should useif we want the surface illumination to be uniform to, say, within one part ina thousand? Answer: (1) Find the electric ﬁeld from a grid of wires with thespacing b, each charged uniformly; (2) compute the vertical component of theelectric ﬁeld; (3) ﬁnd out what b must be so that the ripples of the ﬁeld are notmore than one part in a thousand.In Chapter 7 we saw that the electric ﬁeld of a grid of charged wires could berepresented as a sum of terms, each one of which gave a sinusoidal variation ofthe ﬁeld with a period of b/n, where n is an integer. The amplitude of any oneof these terms is given by Eq. (7.44):

Fn = Ane−2πnz/b.

We need consider only n = 1, so long as we only want the ﬁeld at points nottoo close to the grid. For a complete solution, we would still need to determinethe coeﬃcients An, which we have not yet done (although it is a straightforwardcalculation). Since we need only A1, we can estimate that its magnitude isroughly the same as that of the average ﬁeld. The exponential factor wouldthen give us directly the relative amplitude of the variations. If we want thisfactor to be 10−3, we ﬁnd that b must be 0.91z. If we make the spacing of the

* Since we are talking about incoherent sources whose intensities always add linearly, theanalogous electric charges will always have the same sign. Also, our analogy applies only to thelight energy arriving at the top of an opaque surface, so we must include in our integral onlythe sources which shine on the surface (and, naturally, not sources located below the surface!).12-11

ﬂuorescent tubes 3/4 of the distance to the ceiling, the exponential factor isthen 1/4000, and we have a safety factor of 4, so we are fairly sure that we willhave the illumination constant to one part in a thousand. (An exact calculationshows that A1 is really twice the average ﬁeld, so that b ≈ 0.83z.) It is somewhatsurprising that for such a uniform illumination the allowed separation of thetubes comes out so large.

12-7 The「underlying unity」of natureIn this chapter, we wished to show that in learning electrostatics you havelearned at the same time how to handle many subjects in physics, and that bykeeping this in mind, it is possible to learn almost all of physics in a limitednumber of years.

However, a question surely suggests itself at the end of such a discussion:Why are the equations from diﬀerent phenomena so similar? We might say:「It is the underlying unity of nature.」But what does that mean? What couldsuch a statement mean? It could mean simply that the equations are similar fordiﬀerent phenomena; but then, of course, we have given no explanation. The「underlying unity」might mean that everything is made out of the same stuﬀ,and therefore obeys the same equations. That sounds like a good explanation,but let us think. The electrostatic potential, the diﬀusion of neutrons, heatﬂow—are we really dealing with the same stuﬀ? Can we really imagine thatthe electrostatic potential is physically identical to the temperature, or to thedensity of particles? Certainly φ is not exactly the same as the thermal energy ofparticles. The displacement of a membrane is certainly not like a temperature.Why, then, is there「an underlying unity」?A closer look at the physics of the various subjects shows, in fact, that theequations are not really identical. The equation we found for neutron diﬀusion isonly an approximation that is good when the distance over which we are lookingis large compared with the mean free path. If we look more closely, we would seethe individual neutrons running around. Certainly the motion of an individualneutron is a completely diﬀerent thing from the smooth variation we get fromsolving the diﬀerential equation. The diﬀerential equation is an approximation,because we assume that the neutrons are smoothly distributed in space.Is it possible that this is the clue? That the thing which is common to allthe phenomena is the space, the framework into which the physics is put? Aslong as things are reasonably smooth in space, then the important things thatwill be involved will be the rates of change of quantities with position in space.That is why we always get an equation with a gradient. The derivatives mustappear in the form of a gradient or a divergence; because the laws of physics areindependent of direction, they must be expressible in vector form. The equations ofelectrostatics are the simplest vector equations that one can get which involve onlythe spatial derivatives of quantities. Any other simple problem—or simpliﬁcationof a complicated problem—must look like electrostatics. What is common toall our problems is that they involve space and that we have imitated what isactually a complicated phenomenon by a simple diﬀerential equation.That leads us to another interesting question. Is the same statement perhapsalso true for the electrostatic equations? Are they also correct only as a smoothed-out imitation of a really much more complicated microscopic world? Could itbe that the real world consists of little X-ons which can be seen only at verytiny distances? And that in our measurements we are always observing on sucha large scale that we can’t see these little X-ons, and that is why we get thediﬀerential equations?

Our currently most complete theory of electrodynamics does indeed haveits diﬃculties at very short distances. So it is possible, in principle, that theseequations are smoothed-out versions of something. They appear to be correctat distances down to about 10−14 cm, but then they begin to look wrong. Itis possible that there is some as yet undiscovered underlying「machinery,」andthat the details of an underlying complexity are hidden in the smooth-looking12-12

equations—as is so in the「smooth」diﬀusion of neutrons. But no one has yetformulated a successful theory that works that way.

Strangely enough, it turns out (for reasons that we do not at all understand)that the combination of relativity and quantum mechanics as we know themseems to forbid the invention of an equation that is fundamentally diﬀerentfrom Eq. (12.4), and which does not at the same time lead to some kind ofcontradiction. Not simply a disagreement with experiment, but an internalcontradiction. As, for example, the prediction that the sum of the probabilitiesof all possible occurrences is not equal to unity, or that energies may sometimescome out as complex numbers, or some other such idiocy. No one has yet madeup a theory of electricity for which ∇2φ = −ρ/0 is understood as a smoothed-outapproximation to a mechanism underneath, and which does not lead ultimatelyto some kind of an absurdity. But, it must be added, it is also true that theassumption that ∇2φ = −ρ/0 is valid for all distances, no matter how small,leads to absurdities of its own (the electrical energy of an electron is inﬁnite)—absurdities from which no one yet knows an escape.

12-13

13

Magnetostatics