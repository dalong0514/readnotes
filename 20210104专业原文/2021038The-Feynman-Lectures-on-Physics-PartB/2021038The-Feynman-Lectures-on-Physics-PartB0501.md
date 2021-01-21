# 0501

5-1 Electrostatics is Gauss’ law plus . . .There

are two laws of electrostatics: that the ﬂux of the electric ﬁeld from avolume is proportional to the charge inside—Gauss’ law, and that the circulation ofthe electric ﬁeld is zero—E is a gradient. From these two laws, all the predictionsof electrostatics follow. But to say these things mathematically is one thing; to usethem easily, and with a certain amount of ingenuity, is another. In this chapterwe will work through a number of calculations which can be made with Gauss’law directly. We will prove theorems and describe some eﬀects, particularly inconductors, that can be understood very easily from Gauss’ law. Gauss’ law byitself cannot give the solution of any problem because the other law must be obeyedtoo. So when we use Gauss’ law for the solution of particular problems, we willhave to add something to it. We will have to presuppose, for instance, some ideaof how the ﬁeld looks—based, for example, on arguments of symmetry. Or we mayhave to introduce speciﬁcally the idea that the ﬁeld is the gradient of a potential.

5-2 Equilibrium in an electrostatic ﬁeldConsider ﬁrst the following question: When can a point charge be in stablemechanical equilibrium in the electric ﬁeld of other charges? As an example,imagine three negative charges at the corners of an equilateral triangle in ahorizontal plane. Would a positive charge placed at the center of the triangleremain there? (It will be simpler if we ignore gravity for the moment, althoughincluding it would not change the results.) The force on the positive charge iszero, but is the equilibrium stable? Would the charge return to the equilibriumposition if displaced slightly? The answer is no.

There are no points of stable equilibrium in any electrostatic ﬁeld—exceptright on top of another charge. Using Gauss’ law, it is easy to see why. First, fora charge to be in equilibrium at any particular point P0, the ﬁeld must be zero.Second, if the equilibrium is to be a stable one, we require that if we move thecharge away from P0 in any direction, there should be a restoring force directedopposite to the displacement. The electric ﬁeld at all nearby points must bepointing inward—toward the point P0. But that is in violation of Gauss’ law ifthere is no charge at P0, as we can easily see.Consider a tiny imaginary surface that encloses P0, as in Fig. 5-1. If theelectric ﬁeld everywhere in the vicinity is pointed toward P0, the surface integralof the normal component is certainly not zero. For the case shown in the ﬁgure,the ﬂux through the surface must be a negative number. But Gauss’ law saysthat the ﬂux of electric ﬁeld through any surface is proportional to the totalcharge inside. If there is no charge at P0, the ﬁeld we have imagined violatesGauss’ law. It is impossible to balance a positive charge in empty space—ata point where there is not some negative charge. A positive charge can be inequilibrium if it is in the middle of a distributed negative charge. Of course,the negative charge distribution would have to be held in place by other thanelectrical forces!

Our result has been obtained for a point charge. Does the same conclusionhold for a complicated arrangement of charges held together in ﬁxed relativepositions—with rods, for example? We consider the question for two equal chargesﬁxed on a rod. Is it possible that this combination can be in equilibrium in someelectrostatic ﬁeld? The answer is again no. The total force on the rod cannot berestoring for displacements in every direction.

5-1

5-1 Electrostatics is Gauss’ law

plus . . .

ﬁeld

5-2 Equilibrium in an electrostatic

5-3 Equilibrium with conductors5-4 Stability of atoms5-5 The ﬁeld of a line charge5-6 A sheet of charge; two sheets5-7 A sphere of charge; a spherical

shell

5-8 Is the ﬁeld of a point charge

exactly 1/r2?

5-9 The ﬁelds of a conductor5-10 The ﬁeld in a cavity of a

conductor

Fig. 5-1. If P0 were a position of stableequilibrium for a positive charge, the electricﬁeld everywhere in the neighborhood wouldpoint toward P0.

Call F the total force on the rod in any position—F is then a vector ﬁeld.Following the argument used above, we conclude that at a position of stableequilibrium, the divergence of F must be a negative number. But the total forceon the rod is the ﬁrst charge times the ﬁeld at its position, plus the second chargetimes the ﬁeld at its position:

F = q1E1 + q2E2.

(5.1)

The divergence of F is given by

∇ · F = q1(∇ · E1) + q2(∇ · E2).

If each of the two charges q1 and q2 is in free space, both ∇ · E1 and ∇ · E2 arezero, and ∇ · F is zero—not negative, as would be required for equilibrium. Youcan see that an extension of the argument shows that no rigid combination of anynumber of charges can have a position of stable equilibrium in an electrostaticﬁeld in free space.

Fig. 5-2. A charge can be in equilibrium

if there are mechanical constraints.

Now we have not shown that equilibrium is forbidden if there are pivots orother mechanical constraints. As an example, consider a hollow tube in which acharge can move back and forth freely, but not sideways. Now it is very easy todevise an electric ﬁeld that points inward at both ends of the tube if it is allowedthat the ﬁeld may point laterally outward near the center of the tube. We simplyplace positive charges at each end of the tube, as in Fig. 5-2. There can now bean equilibrium point even though the divergence of E is zero. The charge, ofcourse, would not be in stable equilibrium for sideways motion were it not for「nonelectrical」forces from the tube walls.

5-3 Equilibrium with conductorsThere is no stable spot in the ﬁeld of a system of ﬁxed charges. What abouta system of charged conductors? Can a system of charged conductors produce aﬁeld that will have a stable equilibrium point for a point charge? (We mean ata point other than on a conductor, of course.) You know that conductors havethe property that charges can move freely around in them. Perhaps when thepoint charge is displaced slightly, the other charges on the conductors will movein a way that will give a restoring force to the point charge? The answer is stillno—although the proof we have just given doesn’t show it. The proof for thiscase is more diﬃcult, and we will only indicate how it goes.

First, we note that when charges redistribute themselves on the conductors,they can only do so if their motion decreases their total potential energy. (Someenergy is lost to heat as they move in the conductor.) Now we have alreadyshown that if the charges producing a ﬁeld are stationary, there is, near anyzero point P0 in the ﬁeld, some direction for which moving a point charge awayfrom P0 will decrease the energy of the system (since the force is away from P0).Any readjustment of the charges on the conductors can only lower the potentialenergy still more, so (by the principle of virtual work) their motion will onlyincrease the force in that particular direction away from P0, and not reverse it.Our conclusions do not mean that it is not possible to balance a charge byelectrical forces. It is possible if one is willing to control the locations or the sizesof the supporting charges with suitable devices. You know that a rod standingon its point in a gravitational ﬁeld is unstable, but this does not prove that itcannot be balanced on the end of a ﬁnger. Similarly, a charge can be held inone spot by electric ﬁelds if they are variable. But not with a passive—that is, astatic—system.

5-2

5-4 Stability of atomsIf charges cannot be held stably in position, it is surely not proper to imaginematter to be made up of static point charges (electrons and protons) governedonly by the laws of electrostatics. Such a static conﬁguration is impossible; itwould collapse!

It was once suggested that the positive charge of an atom could be distributeduniformly in a sphere, and the negative charges, the electrons, could be at restinside the positive charge, as shown in Fig. 5-3. This was the ﬁrst atomic model,proposed by Thomson. But Rutherford concluded from the experiment of Geigerand Marsden that the positive charges were very much concentrated, in what hecalled the nucleus. Thomson’s static model had to be abandoned. Rutherford andBohr then suggested that the equilibrium might be dynamic, with the electronsrevolving in orbits, as shown in Fig. 5-4. The electrons would be kept from fallingin toward the nucleus by their orbital motion. We already know at least onediﬃculty with this picture. With such motion, the electrons would be accelerating(because of the circular motion) and would, therefore, be radiating energy. Theywould lose the kinetic energy required to stay in orbit, and would spiral in towardthe nucleus. Again unstable!

The stability of the atoms is now explained in terms of quantum mechanics.The electrostatic forces pull the electron as close to the nucleus as possible, butthe electron is compelled to stay spread out in space over a distance given bythe uncertainty principle. If it were conﬁned in too small a space, it would havea great uncertainty in momentum. But that means that it would have a highexpected energy—which it would use to escape from the electrical attraction.The net result is an electrical equilibrium not too diﬀerent from the idea ofThomson—only it is the negative charge that is spread out (because the mass ofthe electron is so much smaller than the mass of the proton).

5-5 The ﬁeld of a line chargeGauss’ law can be used to solve a number of electrostatic ﬁeld problemsinvolving a special symmetry—usually spherical, cylindrical, or planar symmetry.In the remainder of this chapter we will apply Gauss’ law to a few such problems.The ease with which these problems can be solved may give the misleadingimpression that the method is very powerful, and that one should be able to goon to many other problems. It is unfortunately not so. One soon exhausts thelist of problems that can be solved easily with Gauss’ law. In later chapters wewill develop more powerful methods for investigating electrostatic ﬁelds.

As our ﬁrst example, we consider a system with cylindrical symmetry. Supposethat we have a very long, uniformly charged rod. By this we mean that electriccharges are distributed uniformly along an indeﬁnitely long straight line, with thecharge λ per unit length. We wish to know the electric ﬁeld. The problem can,of course, be solved by integrating the contribution to the ﬁeld from every partof the line. We are going to do it without integrating, by using Gauss’ law andsome guesswork. First, we surmise that the electric ﬁeld will be directed radiallyoutward from the line. Any axial component from charges on one side would beaccompanied by an equal axial component from charges on the other side. The re-sult could only be a radial ﬁeld. It also seems reasonable that the ﬁeld should havethe same magnitude at all points equidistant from the line. This is obvious. (Itmay not be easy to prove, but it is true if space is symmetric—as we believe it is.)We can use Gauss’ law in the following way. We consider an imaginary surfacein the shape of a cylinder coaxial with the line, as shown in Fig. 5-5. Accordingto Gauss’ law, the total ﬂux of E from this surface is equal to the charge insidedivided by 0. Since the ﬁeld is assumed to be normal to the surface, the normalcomponent is the magnitude of the ﬁeld. Let’s call it E. Also, let the radius ofthe cylinder be r, and its length be taken as one unit, for convenience. The ﬂuxthrough the cylindrical surface is equal to E times the area of the surface, whichis 2πr. The ﬂux through the two end faces is zero because the electric ﬁeld is5-3

Fig. 5-3. The Thomson model of an atom.

Fig. 5-4. The Rutherford-Bohr model of

an atom.

Fig. 5-5. A cylindrical gaussian surface

coaxial with a line charge.

tangential to them. The total charge inside our surface is just λ, because thelength of the line inside is one unit. Gauss’ law then gives

E · 2πr = λ/0,E = λ

.

2π0r

(5.2)

The electric ﬁeld of a line charge depends inversely on the ﬁrst power of thedistance from the line.

5-6 A sheet of charge; two sheetsAs another example, we will calculate the ﬁeld from a uniform plane sheetof charge. Suppose that the sheet is inﬁnite in extent and that the charge perunit area is σ. We are going to take another guess. Considerations of symmetrylead us to believe that the ﬁeld direction is everywhere normal to the plane, andif we have no ﬁeld from any other charges in the world, the ﬁelds must be thesame (in magnitude) on each side. This time we choose for our Gaussian surfacea rectangular box that cuts through the sheet, as shown in Fig. 5-6. The twofaces parallel to the sheet will have equal areas, say A. The ﬁeld is normal tothese two faces, and parallel to the other four. The total ﬂux is E times the areaof the ﬁrst face, plus E times the area of the opposite face—with no contributionfrom the other four faces. The total charge enclosed in the box is σA. Equatingthe ﬂux to the charge inside, we have

from which

EA + EA = σA0

,

E = σ20

,

a simple but important result.

(5.3)

Fig. 5-6. The electric ﬁeld near a uni-formly charged sheet can be found by apply-ing Gauss’ law to an imaginary box.

You may remember that the same result was obtained in an earlier chapterby an integration over the entire surface. Gauss’ law gives us the answer, in thisinstance, much more quickly (although it is not as generally applicable as theearlier method).

We emphasize that this result applies only to the ﬁeld due to the charges onthe sheet. If there are other charges in the neighborhood, the total ﬁeld near thesheet would be the sum of (5.3) and the ﬁeld of the other charges. Gauss’ lawwould then tell us only that

where E1 and E2 are the ﬁelds directed outward on each side of the sheet.The problem of two parallel sheets with equal and opposite charge densities,+σ and −σ, is equally simple if we assume again that the outside world isquite symmetric. Either by superposing two solutions for a single sheet or byconstructing a gaussian box that includes both sheets, it is easily seen that the ﬁeldis zero outside of the two sheets (Fig. 5-7a). By considering a box that includesonly one surface or the other, as in (b) or (c) of the ﬁgure, it can be seen that theﬁeld between the sheets must be twice what it is for a single sheet. The result is(5.5)(5.6)

E (between the sheets) = σ/0,E (outside)

= 0.

E1 + E2 = σ0

,

(5.4)

5-7 A sphere of charge; a spherical shellWe have already (in Chapter 4) used Gauss’ law to ﬁnd the ﬁeld outside auniformly charged spherical region. The same method can also give us the ﬁeldat points inside the sphere. For example, the computation can be used to obtaina good approximation to the ﬁeld inside an atomic nucleus. In spite of the fact5-4

Fig. 5-7. The ﬁeld between two charged

sheets is σ/0.

that the protons in a nucleus repel each other, they are, because of the strongnuclear forces, spread nearly uniformly throughout the body of the nucleus.

Suppose that we have a sphere of radius R ﬁlled uniformly with charge. Let ρbe the charge per unit volume. Again using arguments of symmetry, we assumethe ﬁeld to be radial and equal in magnitude at all points at the same distancefrom the center. To ﬁnd the ﬁeld at the distance r from the center, we take aspherical gaussian surface of radius r (r < R), as shown in Fig. 5-8. The ﬂux outof this surface is

4πr2E.

Fig. 5-8. Gauss’ law can be used to ﬁndthe ﬁeld inside a uniformly charged sphere.

The charge inside our gaussian surface is the volume inside times ρ, or

3 πr3ρ.4

Using Gauss’ law, it follows that the magnitude of the ﬁeld is given by

E = ρr30

(r < R).

(5.7)

You can see that this formula gives the proper result for r = R. The electric ﬁeldis proportional to the radius and is directed radially outward.The arguments we have just given for a uniformly charged sphere can beapplied also to a thin spherical shell of charge. Assuming that the ﬁeld iseverywhere radial and is spherically symmetric, one gets immediately from Gauss’law that the ﬁeld outside the shell is like that of a point charge, while the ﬁeldeverywhere inside the shell is zero. (A gaussian surface inside the shell willcontain no charge.)

5-8 Is the ﬁeld of a point charge exactly 1/r2?If we look in a little more detail at how the ﬁeld inside the shell gets to bezero, we can see more clearly why it is that Gauss’ law is true only becausethe Coulomb force depends exactly on the square of the distance. Consider anypoint P inside a uniform spherical shell of charge. Imagine a small cone whoseapex is at P and which extends to the surface of the sphere, where it cuts outa small surface area ∆a1, as in Fig. 5-9. An exactly symmetric cone divergingfrom the opposite side of P would cut out the surface area ∆a2. If the distancesfrom P to these two elements of area are r1 and r2, the areas are in the ratio

∆a2∆a1

= r22r21

.

(You can show this by geometry for any point P inside the sphere.)the elements of area is proportional to the area, so

If the surface of the sphere is uniformly charged, the charge ∆q on each of

∆q2∆q1

= ∆a2∆a1

.

Coulomb’s law then says that the magnitudes of the ﬁelds produced at P bythese two surface elements are in the ratio= ∆q2/r22∆q1/r21

= 1.

E2E1

The ﬁelds cancel exactly. Since all parts of the surface can be paired oﬀ in thesame way, the total ﬁeld at P is zero. But you can see that it would not be so ifthe exponent of r in Coulomb’s law were not exactly two.The validity of Gauss’ law depends upon the inverse square law of Coulomb.If the force law were not exactly the inverse square, it would not be true that theﬁeld inside a uniformly charged sphere would be exactly zero. For instance, ifthe force varied more rapidly, like, say, the inverse cube of r, that portion of thesurface which is nearer to an interior point would produce a ﬁeld which is larger5-5

Fig. 5-9. The ﬁeld is zero at any point P

inside a spherical shell of charge.

than that which is farther away, resulting in a radial inward ﬁeld for a positivesurface charge. These conclusions suggest an elegant way of ﬁnding out whetherthe inverse square law is precisely correct. We need only determine whether ornot the ﬁeld inside of a uniformly charged spherical shell is precisely zero.

It is lucky that such a method exists. It is usually diﬃcult to measure aphysical quantity to high precision—a one percent result may not be too diﬃcult,but how would one go about measuring, say, Coulomb’s law to an accuracy ofone part in a billion? It is almost certainly not possible with the best availabletechniques to measure the force between two charged objects with such anaccuracy. But by determining only that the electric ﬁelds inside a charged sphereare smaller than some value we can make a highly accurate measurement ofthe correctness of Gauss’ law, and hence of the inverse square dependence ofCoulomb’s law. What one does, in eﬀect, is compare the force law to an idealinverse square. Such comparisons of things that are equal, or nearly so, areusually the bases of the most precise physical measurements.

How shall we observe the ﬁeld inside a charged sphere? One way is to tryto charge an object by touching it to the inside of a spherical conductor. Youknow that if we touch a small metal ball to a charged object and then touchit to an electrometer the meter will become charged and the pointer will movefrom zero (Fig. 5-10a). The ball picks up charge because there are electric ﬁeldsoutside the charged sphere that cause charges to run onto (or oﬀ) the little ball.If you do the same experiment by touching the little ball to the inside of thecharged sphere, you ﬁnd that no charge is carried to the electrometer. With suchan experiment you can easily show that the ﬁeld inside is, at most, a few percentof the ﬁeld outside, and that Gauss’ law is at least approximately correct.

It appears that Benjamin Franklin was the ﬁrst to notice that the ﬁeld insidea conducting shell is zero. The result seemed strange to him. When he reportedhis observation to Priestley, the latter suggested that it might be connectedwith an inverse square law, since it was known that a spherical shell of matterproduced no gravitational ﬁeld inside. But Coulomb didn’t measure the inversesquare dependence until 18 years later, and Gauss’ law came even later still.

Gauss’ law has been checked carefully by putting an electrometer inside alarge sphere and observing whether any deﬂections occur when the sphere ischarged to a high voltage. A null result is always obtained. Knowing the geometryof the apparatus and the sensitivity of the meter, it is possible to compute theminimum ﬁeld that would be observed. From this number it is possible to placean upper limit on the deviation of the exponent from two. If we write that theelectrostatic force depends on r−2+, we can place an upper bound on . By thismethod Maxwell determined that  was less than 1/10,000. The experiment wasrepeated and improved upon in 1936 by Plimpton and Lawton. They found thatCoulomb’s exponent diﬀers from two by less than one part in a billion.

Now that brings up an interesting question: How accurate do we know thisCoulomb law to be in various circumstances? The experiments we just describedmeasure the dependence of the ﬁeld on distance for distances of some tens ofcentimeters. But what about the distances inside an atom—in the hydrogenatom, for instance, where we believe the electron is attracted to the nucleusby the same inverse square law? It is true that quantum mechanics must beused for the mechanical part of the behavior of the electron, but the force is theusual electrostatic one. In the formulation of the problem, the potential energyof an electron must be known as a function of distance from the nucleus, andCoulomb’s law gives a potential which varies inversely with the ﬁrst power of thedistance. How accurately is the exponent known for such small distances? Asa result of very careful measurements in 1947 by Lamb and Retherford on therelative positions of the energy levels of hydrogen, we know that the exponent iscorrect again to one part in a billion on the atomic scale—that is, at distances ofthe order of one angstrom (10−8 centimeter).

The accuracy of the Lamb-Retherford measurement was possible again becauseof a physical「accident.」Two of the states of a hydrogen atom are expected tohave almost identical energies only if the potential varies exactly as 1/r. A5-6

Fig. 5-10. The electric ﬁeld is zero inside

a closed conducting shell.

measurement was made of the very slight diﬀerence in energies by ﬁnding thefrequency ω of the photons that are emitted or absorbed in the transition fromone state to the other, using for the energy diﬀerence ∆E = ω. Computationsshowed that ∆E would have been noticeably diﬀerent from what was observed ifthe exponent in the force law 1/r2 diﬀered from 2 by as much as one part in abillion.Is the same exponent correct at still shorter distances? From measurementsin nuclear physics it is found that there are electrostatic forces at typical nucleardistances—at about 10−13 centimeter—and that they still vary approximatelyas the inverse square. We shall look at some of the evidence in a later chapter.Coulomb’s law is, we know, still valid, at least to some extent, at distances ofthe order of 10−13 centimeter.

How about 10−14 centimeter? This range can be investigated by bombardingprotons with very energetic electrons and observing how they are scattered.Results to date seem to indicate that the law fails at these distances. Theelectrical force seems to be about 10 times too weak at distances less than10−14 centimeter. Now there are two possible explanations. One is that theCoulomb law does not work at such small distances; the other is that our objects,the electrons and protons, are not point charges. Perhaps either the electron orproton, or both, is some kind of a smear. Most physicists prefer to think that thecharge of the proton is smeared. We know that protons interact strongly withmesons. This implies that a proton will, from time to time, exist as a neutronwith a π+ meson around it. Such a conﬁguration would act—on the average—likea little sphere of positive charge. We know that the ﬁeld from a sphere of chargedoes not vary as 1/r2 all the way into the center. It is quite likely that the protoncharge is smeared, but the theory of pions is still quite incomplete, so it may alsobe that Coulomb’s law fails at very small distances. The question is still open.One more point: The inverse square law is valid at distances like one meterand also at 10−10 m; but is the coeﬃcient 1/4π0 the same? The answer is yes;at least to an accuracy of 15 parts in a million.We go back now to an important matter that we slighted when we spoke ofthe experimental veriﬁcation of Gauss’ law. You may have wondered how theexperiment of Maxwell or of Plimpton and Lawton could give such an accuracyunless the spherical conductor they used was a perfect sphere. An accuracyof one part in a billion is really something to achieve, and you might well askwhether they could make a sphere which was that precise. There are certain tobe slight irregularities in any real sphere and if there are irregularities, will theynot produce ﬁelds inside? We wish to show now that it is not necessary to havea perfect sphere. It is possible, in fact, to show that there is no ﬁeld inside aclosed conducting shell of any shape. In other words, the experiments dependedon 1/r2, but had nothing to do with the surface being a sphere (except that witha sphere it is easier to calculate what the ﬁelds would be if Coulomb had beenwrong), so we take up that subject now. To show this, it is necessary to knowsome of the properties of electrical conductors.

5-9 The ﬁelds of a conductorAn electrical conductor is a solid that contains many「free」electrons. Theelectrons can move around freely in the material, but cannot leave the surface.In a metal there are so many free electrons that any electric ﬁeld will set largenumbers of them into motion. Either the current of electrons so set up mustbe continually kept moving by external sources of energy, or the motion of theelectrons will cease as they discharge the sources producing the initial ﬁeld. In「electrostatic」situations, we do not consider continuous sources of current (theywill be considered later when we study magnetostatics), so the electrons moveonly until they have arranged themselves to produce zero electric ﬁeld everywhereinside the conductor. (This usually happens in a small fraction of a second.) Ifthere were any ﬁeld left, this ﬁeld would urge still more electrons to move; theonly electrostatic solution is that the ﬁeld is everywhere zero inside.

5-7

Now consider the interior of a charged conducting object. (By「interior」wemean in the metal itself.) Since the metal is a conductor, the interior ﬁeld mustbe zero, and so the gradient of the potential φ is zero. That means that φ doesnot vary from point to point. Every conductor is an equipotential region, and itssurface is an equipotential surface. Since in a conducting material the electricﬁeld is everywhere zero, the divergence of E is zero, and by Gauss’ law the chargedensity in the interior of the conductor must be zero.If there can be no charges in a conductor, how can it ever be charged? Whatdo we mean when we say a conductor is「charged」? Where are the charges? Theanswer is that they reside at the surface of the conductor, where there are strongforces to keep them from leaving—they are not completely「free.」When we studysolid-state physics, we shall ﬁnd that the excess charge of any conductor is on theaverage within one or two atomic layers of the surface. For our present purposes,it is accurate enough to say that if any charge is put on, or in, a conductor it allaccumulates on the surface; there is no charge in the interior of a conductor.We note also that the electric ﬁeld just outside the surface of a conductormust be normal to the surface. There can be no tangential component. If therewere a tangential component, the electrons would move along the surface; thereare no forces preventing that. Saying it another way: we know that the electricﬁeld lines must always go at right angles to an equipotential surface.

We can also, using Gauss’ law, relate the ﬁeld strength just outside a conductorto the local density of the charge at the surface. For a gaussian surface, we take asmall cylindrical box half inside and half outside the surface, like the one shownin Fig. 5-11. There is a contribution to the total ﬂux of E only from the side ofthe box outside the conductor. The ﬁeld just outside the surface of a conductoris then

Fig. 5-11. The electric ﬁeld just outsidethe surface of a conductor is proportionalto the local surface density of charge.

Outside a conductor:

,

(5.8)

E = σ0where σ is the local surface charge density.Why does a sheet of charge on a conductor produce a diﬀerent ﬁeld thanjust a sheet of charge? In other words, why is (5.8) twice as large as (5.3)? Thereason, of course, is that we have not said for the conductor that there are no「other」charges around. There must, in fact, be some to make E = 0 in theconductor. The charges in the immediate neighborhood of a point P on thesurface do, in fact, give a ﬁeld Elocal = σlocal/20 both inside and outside thesurface. But all the rest of the charges on the conductor「conspire」to producean additional ﬁeld at the point P equal in magnitude to Elocal. The total ﬁeldinside goes to zero and the ﬁeld outside to 2Elocal = σ/0.

5-10 The ﬁeld in a cavity of a conductorWe return now to the problem of the hollow container—a conductor with acavity. There is no ﬁeld in the metal, but what about in the cavity? We shallshow that if the cavity is empty then there are no ﬁelds in it, no matter what theshape of the conductor or the cavity—say for the one in Fig. 5-12. Consider agaussian surface, like S in Fig. 5-12, that encloses the cavity but stays everywherein the conducting material. Everywhere on S the ﬁeld is zero, so there is no ﬂuxthrough S and the total charge inside S is zero. For a spherical shell, one couldthen argue from symmetry that there could be no charge inside. But, in general,we can only say that there are equal amounts of positive and negative charge onthe inner surface of the conductor. There could be a positive surface charge onone part and a negative one somewhere else, as indicated in Fig. 5-12. Such athing cannot be ruled out by Gauss’ law.

What really happens, of course, is that any equal and opposite charges on theinner surface would slide around to meet each other, cancelling out completely. Wecan show that they must cancel completely by using the law that the circulationof E is always zero (electrostatics). Suppose there were charges on some partsof the inner surface. We know that there would have to be an equal number of5-8

Fig. 5-12. What is the ﬁeld in an empty

cavity of a conductor, for any shape?

opposite charges somewhere else. Now any lines of E would have to start on thepositive charges and end on the negative charges (since we are considering onlythe case that there are no free charges in the cavity). Now imagine a loop Γ thatcrosses the cavity along a line of force from some positive charge to some negativecharge, and returns to its starting point via the conductor (as in Fig. 5-12). Theintegral along such a line of force from the positive to the negative charges wouldnot be zero. The integral through the metal is zero, since E = 0. So we wouldhave

I

E · ds 6= 0???

But the line integral of E around any closed loop in an electrostatic ﬁeld is alwayszero. So there can be no ﬁelds inside the empty cavity, nor any charges on theinside surface.

You should notice carefully one important qualiﬁcation we have made. Wehave always said「inside an empty」cavity. If some charges are placed at someﬁxed locations in the cavity—as on an insulator or on a small conductor insulatedfrom the main one—then there can be ﬁelds in the cavity. But then that is notan「empty」cavity.We have shown that if a cavity is completely enclosed by a conductor, no staticdistribution of charges outside can ever produce any ﬁelds inside. This explainsthe principle of「shielding」electrical equipment by placing it in a metal can. Thesame arguments can be used to show that no static distribution of charges insidea closed grounded conductor can produce any ﬁelds outside. Shielding worksboth ways! In electrostatics—but not in varying ﬁelds—the ﬁelds on the twosides of a closed grounded conducting shell are completely independent.

Now you see why it was possible to check Coulomb’s law to such a greatprecision. The shape of the hollow shell used doesn’t matter. It doesn’t need to bespherical; it could be square! If Gauss’ law is exact, the ﬁeld inside is always zero.Now you also understand why it is safe to sit inside the high-voltage terminalof a million-volt Van de Graaﬀ generator, without worrying about getting ashock—because of Gauss’ law.

5-9