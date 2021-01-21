

# 0601

6-1 Equations of the electrostatic

potential

6-2 The electric dipole6-3 Remarks on vector equations6-4 The dipole potential as a gradient6-5 The dipole approximation for an

arbitrary distribution

6-6 The ﬁelds of charged conductors6-7 The method of images6-8 A point charge near a conducting

6-9 A point charge near a conducting

plane

sphere

6-10 Condensers; parallel plates6-11 High-voltage breakdown6-12 The ﬁeld-emission microscope

Review: Chapter 23, Vol. I, Resonance

6

The Electric Field in Various Circumstances

6-1 Equations of the electrostatic potentialThis

chapter will describe the behavior of the electric ﬁeld in a number ofdiﬀerent circumstances. It will provide some experience with the way the electricﬁeld behaves, and will describe some of the mathematical methods which areused to ﬁnd this ﬁeld.

We begin by pointing out that the whole mathematical problem is the solution

of two equations, the Maxwell equations for electrostatics:

,

(6.1)

∇ · E = ρ0∇ × E = 0.

(6.2)In fact, the two can be combined into a single equation. From the second equation,we know at once that we can describe the ﬁeld as the gradient of a scalar (seeSection 3-7):

(6.3)We may, if we wish, completely describe any particular electric ﬁeld in termsof its potential φ. We obtain the diﬀerential equation that φ must obey bysubstituting Eq. (6.3) into (6.1), to get

E = −∇φ.

The divergence of the gradient of φ is the same as ∇2 operating on φ:

∇ · ∇φ = − ρ0

.

∇ · ∇φ = ∇2φ = ∂2φ∂x2

+ ∂2φ∂y2

+ ∂2φ∂z2 ,

(6.4)

(6.5)

so we write Eq. (6.4) as

.

∇2φ = − ρ0

(6.6)The operator ∇2 is called the Laplacian, and Eq. (6.6) is called the Poissonequation. The entire subject of electrostatics, from a mathematical point of view,is merely a study of the solutions of the single equation (6.6). Once φ is obtainedby solving Eq. (6.6) we can ﬁnd E immediately from Eq. (6.3).We take up ﬁrst the special class of problems in which ρ is given as a functionof x, y, z. In that case the problem is almost trivial, for we already know thesolution of Eq. (6.6) for the general case. We have shown that if ρ is known atevery point, the potential at point (1) is

Z ρ(2) dV2

4π0r12

φ(1) =

,

(6.7)

where ρ(2) is the charge density, dV2 is the volume element at point (2), and r12is the distance between points (1) and (2). The solution of the diﬀerentialequation (6.6) is reduced to an integration over space. The solution (6.7) shouldbe especially noted, because there are many situations in physics that lead toequations like

∇2(something) = (something else),

and Eq. (6.7) is a prototype of the solution for any of these problems.

The solution of electrostatic ﬁeld problems is thus completely straightforwardwhen the positions of all the charges are known. Let’s see how it works in a fewexamples.

6-1

6-2 The electric dipoleFirst, take two point charges, +q and −q, separated by the distance d. Letthe z-axis go through the charges, and pick the origin halfway between, as shownin Fig. 6-1. Then, using (4.24), the potential from the two charges is given by

(cid:20)

φ(x, y, z)

= 14π0

p[z − (d/2)]2 + x2 + y2

q

p[z + (d/2)]2 + x2 + y2

−q

+

(cid:21)

.

(6.8)

We are not going to write out the formula for the electric ﬁeld, but we can alwayscalculate it once we have the potential. So we have solved the problem of twocharges.

There is an important special case in which the two charges are very closetogether—which is to say that we are interested in the ﬁelds only at distancesfrom the charges large in comparison with their separation. We call such a closepair of charges a dipole. Dipoles are very common.A「dipole」antenna can often be approximated by two charges separated by asmall distance—if we don’t ask about the ﬁeld too close to the antenna. (We areusually interested in antennas with moving charges; then the equations of staticsdo not really apply, but for some purposes they are an adequate approximation.)More important perhaps, are atomic dipoles. If there is an electric ﬁeld in anymaterial, the electrons and protons feel opposite forces and are displaced relativeto each other. In a conductor, you remember, some of the electrons move tothe surfaces, so that the ﬁeld inside becomes zero. In an insulator the electronscannot move very far; they are pulled back by the attraction of the nucleus. Theydo, however, shift a little bit. So although an atom, or molecule, remains neutralin an external electric ﬁeld, there is a very tiny separation of its positive andnegative charges and it becomes a microscopic dipole. If we are interested in theﬁelds of these atomic dipoles in the neighborhood of ordinary-sized objects, weare normally dealing with distances large compared with the separations of thepairs of charges.

In some molecules the charges are somewhat separated even in the absenceof external ﬁelds, because of the form of the molecule. In a water molecule, forexample, there is a net negative charge on the oxygen atom and a net positivecharge on each of the two hydrogen atoms, which are not placed symmetricallybut as in Fig. 6-2. Although the charge of the whole molecule is zero, there is acharge distribution with a little more negative charge on one side and a little morepositive charge on the other. This arrangement is certainly not as simple as twopoint charges, but when seen from far away the system acts like a dipole. As weshall see a little later, the ﬁeld at large distances is not sensitive to the ﬁne details.Let’s look, then, at the ﬁeld of two opposite charges with a small separation d.If d becomes zero, the two charges are on top of each other, the two potentialscancel, and there is no ﬁeld. But if they are not exactly on top of each other, wecan get a good approximation to the potential by expanding the terms of (6.8) ina power series in the small quantity d (using the binomial expansion). Keepingterms only to ﬁrst order in d, we can write

(cid:18)

(cid:19)2

z − d2

≈ z2 − zd.

It is convenient to write

Then

and

(cid:19)2

(cid:18)

z − d2

x2 + y2 + z2 = r2.

+ x2 + y2 ≈ r2 − zd = r2

(cid:18)

(cid:19)

,

1 − zdr2

(cid:18)

p[z − (d/2)]2 + x2 + y2 ≈

1

pr2[1 − (zd/r2)]

1

= 1

r

1 − zdr2

(cid:19)−1/2

.

6-2

Fig. 6-1. A dipole:

and −q the distance d apart.

two charges +q

Fig. 6-2. The water molecule H2O. Thehydrogen atoms have slightly less than theirshare of the electron cloud; the oxygen,slightly more.

Using the binomial expansion again for [1 − (zd/r2)]−1/2—and throwing awayterms with the square or higher powers of d—we get

(cid:18)

(cid:19)p[z + (d/2)]2 + x2 + y2 ≈ 1

1 + 12

zdr2

1r

.

(cid:18)

Similarly,

1 − 12The diﬀerence of these two terms gives for the potential

1

r

zdr2

(cid:19)

.

φ(x, y, z) = 14π0

zr3 qd.

(6.9)

The potential, and hence the ﬁeld, which is its derivative, is proportional to qd,the product of the charge and the separation. This product is deﬁned as thedipole moment of the two charges, for which we will use the symbol p (do notconfuse with momentum!):(6.10)

p = qd.

Equation (6.9) can also be written asφ(x, y, z) = 14π0

p cos θ

r2

,

(6.11)

since z/r = cos θ, where θ is the angle between the axis of the dipole andthe radius vector to the point (x, y, z)—see Fig. 6-1. The potential of a dipoledecreases as 1/r2 for a given direction from the axis (whereas for a point chargeit goes as 1/r). The electric ﬁeld E of the dipole will then decrease as 1/r3.We can put our formula into a vector form if we deﬁne p as a vector whosemagnitude is p and whose direction is along the axis of the dipole, pointing from−q toward +q. Then(6.12)where er is the unit radial vector (Fig. 6-3). We can also represent the point(x, y, z) by r. ThenDipole potential:

p cos θ = p · er,

φ(r) = 14π0

p · err2

= 14π0

p · rr3

(6.13)

Fig. 6-3. Vector notation for a dipole.

This formula is valid for a dipole with any orientation and position if r representsthe vector from the dipole to the point of interest.If we want the electric ﬁeld of the dipole we can get it by taking the gradientof φ. For example, the z-component of the ﬁeld is −∂φ/∂z. For a dipole orientedalong the z-axis we can use (6.9):

(cid:18) 1r3 − 3z2

r5

(cid:19)

,

(cid:18) z

(cid:19)

r3

= − p4π03 cos2 θ − 1

r3

Ez = p4π0

.

(6.14)

− ∂φ∂z

= − p4π0

∂∂z

or

The x- and y-components areEx = p4π0

3zxr5 ,

Ey = p4π0

3zyr5 .

These two can be combined to give one component directed perpendicular to thez-axis, which we will call the transverse component E⊥:

or

E⊥ =q

p

x2 + y2

E2x

+ E2

y

E⊥ = p4π0

3zr5

= p4π03 cos θ sin θ

r3

.

(6.15)

6-3

The transverse component E⊥ is in the xy-plane and points directly away fromthe axis of the dipole. The total ﬁeld, of course, is

E =q

E2z

+ E2⊥.

The dipole ﬁeld varies inversely as the cube of the distance from the dipole.On the axis, at θ = 0, it is twice as strong as at θ = 90◦. At both of these specialangles the electric ﬁeld has only a z-component, but of opposite sign at the twoplaces (Fig. 6-4).

6-3 Remarks on vector equationsThis is a good place to make a general remark about vector analysis. Thefundamental proofs can be expressed by elegant equations in a general form, butin making various calculations and analyses it is always a good idea to choosethe axes in some convenient way. Notice that when we were ﬁnding the potentialof a dipole we chose the z-axis along the direction of the dipole, rather than atsome arbitrary angle. This made the work much easier. But then we wrote theequations in vector form so that they would no longer depend on any particularcoordinate system. After that, we are allowed to choose any coordinate systemwe wish, knowing that the relation is, in general, true. It clearly doesn’t makeany sense to bother with an arbitrary coordinate system at some complicatedangle when you can choose a neat system for the particular problem—providedthat the result can ﬁnally be expressed as a vector equation. So by all means takeadvantage of the fact that vector equations are independent of any coordinatesystem.On the other hand, if you are trying to calculate the divergence of a vector,instead of just looking at ∇ · E and wondering what it is, don’t forget that itcan always be spread out as

∂Ex∂x

+ ∂Ey∂y

+ ∂Ez∂z

.

If you can then work out the x-, y-, and z-components of the electric ﬁeldand diﬀerentiate them, you will have the divergence. There often seems to bea feeling that there is something inelegant—some kind of defeat involved—inwriting out the components; that somehow there ought always to be a way todo everything with the vector operators. There is often no advantage to it. Theﬁrst time we encounter a particular kind of problem, it usually helps to write outthe components to be sure we understand what is going on. There is nothinginelegant about putting numbers into equations, and nothing inelegant aboutsubstituting the derivatives for the fancy symbols. In fact, there is often a certaincleverness in doing just that. Of course when you publish a paper in a professionaljournal it will look better—and be more easily understood—if you can writeeverything in vector form. Besides, it saves print.

Fig. 6-4. The electric ﬁeld of a dipole.

6-4 The dipole potential as a gradientWe would like to point out a rather amusing thing about the dipole formula,

Eq. (6.13). The potential can also be written as

(cid:18)1

(cid:19)

r

p · ∇

.

(6.16)

φ = − 14π0(cid:19)(cid:18)1

If you calculate the gradient of 1/r, you get= − rr3

∇

r

= − err2 ,

and Eq. (6.16) is the same as Eq. (6.13).

How did we think of that? We just remembered that er/r2 appeared in theformula for the ﬁeld of a point charge, and that the ﬁeld was the gradient of apotential which has a 1/r dependence.

6-4

There is a physical reason for being able to write the dipole potential in theform of Eq. (6.16). Suppose we have a point charge q at the origin. The potentialat the point P at (x, y, z) is

(Let’s leave oﬀ the 1/4π0 while we make these arguments; we can stick it in atthe end.) Now if we move the charge +q up a distance ∆z, the potential at Pwill change a little, by, say, ∆φ+. How much is ∆φ+? Well, it is just the amountthat the potential would change if we were to leave the charge at the origin andmove P downward by the same distance ∆z (Fig. 6-5). That is,

φ0 = qr

.

∆φ+ = − ∂φ0∂z

∆z,

where by ∆z we mean the same as d/2. So, using φ0 = q/r, we have that thepotential from the positive charge is

φ+ = qr

− ∂∂z

(6.17)

Applying the same reasoning for the potential from the negative charge, we

can write

2 .The total potential is the sum of (6.17) and (6.18):

r

r

φ− = −q

+ ∂∂z

r

2 .

(cid:18) q(cid:19) d(cid:19) d(cid:18)−q(cid:19)(cid:18) q(cid:18)1(cid:19)

r

φ = φ+ + φ− = − ∂∂z= − ∂∂z

d

qd

r

(6.18)

(6.19)

Fig. 6-5. The potential at P from a pointcharge at ∆z above the origin is the sameas the potential at P (cid:48) (∆z below P ) fromthe same charge at the origin.

For other orientations of the dipole, we could represent the displacement ofthe positive charge by the vector ∆r+. We should then write the equation aboveEq. (6.17) as

∆φ+ = −∇φ0 · ∆r+,

where ∆r+ is then to be replaced by d/2. Completing the derivation as before,Eq. (6.19) would then become

(cid:18)1

(cid:19)

r

φ = −∇

· qd.

This is the same as Eq. (6.16), if we replace qd = p, and put back the 1/4π0.Looking at it another way, we see that the dipole potential, Eq. (6.13), can beinterpreted as

φ = −p · ∇Φ0,

(6.20)

where Φ0 = 1/4π0r is the potential of a unit point charge.Although we can always ﬁnd the potential of a known charge distributionby an integration, it is sometimes possible to save time by getting the answerwith a clever trick. For example, one can often make use of the superpositionprinciple. If we are given a charge distribution that can be made up of the sumof two distributions for which the potentials are already known, it is easy to ﬁndthe desired potential by just adding the two known ones. One example of this isour derivation of (6.20), another is the following.

Suppose we have a spherical surface with a distribution of surface charge thatvaries as the cosine of the polar angle. The integration for this distribution is fairlymessy. But, surprisingly, such a distribution can be analyzed by superposition.For imagine a sphere with a uniform volume density of positive charge, andanother sphere with an equal uniform volume density of negative charge, originallysuperposed to make a neutral—that is, uncharged—sphere. If the positive sphere6-5

Fig. 6-6. Two uniformly charged spheres,superposed with a slight displacement, areequivalent to a nonuniform distribution ofsurface charge.

is then displaced slightly with respect to the negative sphere, the body of theuncharged sphere would remain neutral, but a little positive charge will appear onone side, and some negative charge will appear on the opposite side, as illustratedin Fig. 6-6. If the relative displacement of the two spheres is small, the net chargeis equivalent to a surface charge (on a spherical surface), and the surface chargedensity will be proportional to the cosine of the polar angle.

Now if we want the potential from this distribution, we do not need to do anintegral. We know that the potential from each of the spheres of charge is—forpoints outside the sphere—the same as from a point charge. The two displacedspheres are like two point charges; the potential is just that of a dipole.

In this way you can show that a charge distribution on a sphere of radius a

with a surface charge density

σ = σ0 cos θ

produces a ﬁeld outside the sphere which is just that of a dipole whose moment is

p = 4πσ0a3

3

.

It can also be shown that inside the sphere the ﬁeld is constant, with the value

E = σ030

.

If θ is the angle from the positive z-axis, the electric ﬁeld inside the sphere is inthe negative z-direction. The example we have just considered is not as artiﬁcialas it may appear; we will encounter it again in the theory of dielectrics.

6-5 The dipole approximation for an arbitrary distributionThe dipole ﬁeld appears in another circumstance both interesting and im-portant. Suppose that we have an object that has a complicated distributionof charge—like the water molecule (Fig. 6-2)—and we are interested only inthe ﬁelds far away. We will show that it is possible to ﬁnd a relatively simpleexpression for the ﬁelds which is appropriate for distances large compared withthe size of the object.

We can think of our object as an assembly of point charges qi in a certainlimited region, as shown in Fig. 6-7. (We can, later, replace qi by ρ dV if wewish.) Let each charge qi be located at the displacement di from an origin chosen

Fig. 6-7. Computation of the potentialat a point P at a large distance from a setof charges.

6-6

somewhere in the middle of the group of charges. What is the potential at thepoint P, located at R, where R is much larger than the maximum di? Thepotential from the whole collection is given by

X

i

φ = 14π0

qiri

,

(6.21)

where ri is the distance from P to the charge qi (the length of the vector R− di).Now if the distance from the charges to P, the point of observation, is enormous,each of the ri’s can be approximated by R. Each term becomes qi/R, and wecan take 1/R out as a factor in front of the summation. This gives us the simpleresult

qi = Q

4π0R

,

(6.22)

φ = 14π0

1R

X

i

where Q is just the total charge of the whole object. Thus we ﬁnd that for pointsfar enough from any lump of charge, the lump looks like a point charge. Theresult is not too surprising.

But what if there are equal numbers of positive and negative charges? Thenthe total charge Q of the object is zero. This is not an unusual case; in fact, aswe know, objects are usually neutral. The water molecule is neutral, but thecharges are not all at one point, so if we are close enough we should be able to seesome eﬀects of the separate charges. We need a better approximation than (6.22)for the potential from an arbitrary distribution of charge in a neutral object.Equation (6.21) is still precise, but we can no longer just set ri = R. We needa more accurate expression for ri. If the point P is at a large distance, ri willdiﬀer from R to an excellent approximation by the projection of d on R, as canbe seen from Fig. 6-7. (You should imagine that P is really farther away thanis shown in the ﬁgure.) In other words, if eR is the unit vector in the directionof R, then our next approximation to ri is

(6.23)What we really want is 1/ri, which, since di (cid:28) R, can be written to ourapproximation as

ri ≈ R − di · eR.

Substituting this in (6.21), we get that the potential is

1ri

(cid:19)

.

(cid:18)1 + di · eR≈ 1(cid:18) Q+X

R

R

qi

di · eRR2

R

i

φ = 14π0

(cid:19)

.

(6.24)

(6.25)

+ ···

The three dots indicate the terms of higher order in di/R that we have neglected.These, as well as the ones we have already obtained, are successive terms in aTaylor expansion of 1/ri about 1/R in powers of di/R.The ﬁrst term in (6.25) is what we got before; it drops out if the object isneutral. The second term depends on 1/R2, just as for a dipole. In fact, if wedeﬁne

(6.26)

as a property of the charge distribution, the second term of the potential (6.25)is

,

(6.27)

precisely a dipole potential. The quantity p is called the dipole moment of thedistribution. It is a generalization of our earlier deﬁnition, and reduces to it forthe special case of two point charges.

Our result is that, far enough away from any mess of charges that is as awhole neutral, the potential is a dipole potential. It decreases as 1/R2 and varies6-7

p =X

i

qidi

φ = 14π0

p · eRR2

as cos θ—and its strength depends on the dipole moment of the distribution ofcharge. It is for these reasons that dipole ﬁelds are important, since the simplecase of a pair of point charges is quite rare.

The water molecule, for example, has a rather strong dipole moment. Theelectric ﬁelds that result from this moment are responsible for some of theimportant properties of water. For many molecules, for example CO2, the dipolemoment vanishes because of the symmetry of the molecule. For them we shouldexpand still more accurately, obtaining another term in the potential whichdecreases as 1/R3, and which is called a quadrupole potential. We will discusssuch cases later.

6-6 The ﬁelds of charged conductorsWe have now ﬁnished with the examples we wish to cover of situations inwhich the charge distribution is known from the start. It has been a problemwithout serious complications, involving at most some integrations. We turn nowto an entirely new kind of problem, the determination of the ﬁelds near chargedconductors.

Suppose that we have a situation in which a total charge Q is placed on anarbitrary conductor. Now we will not be able to say exactly where the chargesare. They will spread out in some way on the surface. How can we know howthe charges have distributed themselves on the surface? They must distributethemselves so that the potential of the surface is constant. If the surface werenot an equipotential, there would be an electric ﬁeld inside the conductor, andthe charges would keep moving until it became zero. The general problem of thiskind can be solved in the following way. We guess at a distribution of charge andcalculate the potential. If the potential turns out to be constant everywhere onthe surface, the problem is ﬁnished. If the surface is not an equipotential, we haveguessed the wrong distribution of charges, and should guess again—hopefullywith an improved guess! This can go on forever, unless we are judicious aboutthe successive guesses.

The question of how to guess at the distribution is mathematically diﬃcult.Nature, of course, has time to do it; the charges push and pull until they allbalance themselves. When we try to solve the problem, however, it takes us solong to make each trial that that method is very tedious. With an arbitrarygroup of conductors and charges the problem can be very complicated, and ingeneral it cannot be solved without rather elaborate numerical methods. Suchnumerical computations, these days, are set up on a computing machine thatwill do the work for us, once we have told it how to proceed.

On the other hand, there are a lot of little practical cases where it would benice to be able to ﬁnd the answer by some more direct method—without havingto write a program for a computer. Fortunately, there are a number of caseswhere the answer can be obtained by squeezing it out of Nature by some trick orother. The ﬁrst trick we will describe involves making use of solutions we havealready obtained for situations in which charges have speciﬁed locations.

Fig. 6-8. The ﬁeld lines and equipoten-

tials for two point charges.

6-7 The method of imagesWe have solved, for example, the ﬁeld of two point charges. Figure 6-8 showssome of the ﬁeld lines and equipotential surfaces we obtained by the computationsin Chapter 4. Now consider the equipotential surface marked A. Suppose wewere to shape a thin sheet of metal so that it just ﬁts this surface. If we place itright at the surface and adjust its potential to the proper value, no one wouldever know it was there, because nothing would be changed.

But notice! We have really solved a new problem. We have a situation inwhich the surface of a curved conductor with a given potential is placed near apoint charge. If the metal sheet we placed at the equipotential surface eventuallycloses on itself (or, in practice, if it goes far enough) we have the kind of situationconsidered in Section 5-10, in which our space is divided into two regions, one6-8

Fig. 6-9. The ﬁeld outside a conductorshaped like the equipotential A of Fig. 6-8.

inside and one outside a closed conducting shell. We found there that the ﬁeldsin the two regions are quite independent of each other. So we would have thesame ﬁelds outside our curved conductor no matter what is inside. We can evenﬁll up the whole inside with conducting material. We have found, therefore, theﬁelds for the arrangement of Fig. 6-9. In the space outside the conductor theﬁeld is just like that of two point charges, as in Fig. 6-8. Inside the conductor,it is zero. Also—as it must be—the electric ﬁeld just outside the conductor isnormal to the surface.Thus we can compute the ﬁelds in Fig. 6-9 by computing the ﬁeld due to qand to an imaginary point charge −q at a suitable point. The point charge we「imagine」existing behind the conducting surface is called an image charge.In books you can ﬁnd long lists of solutions for hyperbolic-shaped conductorsand other complicated looking things, and you wonder how anyone ever solvedthese terrible shapes. They were solved backwards! Someone solved a simpleproblem with given charges. He then saw that some equipotential surface showedup in a new shape, and he wrote a paper in which he pointed out that the ﬁeldoutside that particular shape can be described in a certain way.

6-8 A point charge near a conducting planeAs the simplest application of the use of this method, let’s make use of theplane equipotential surface B of Fig. 6-8. With it, we can solve the problem of acharge in front of a conducting sheet. We just cross out the left-hand half of thepicture. The ﬁeld lines for our solution are shown in Fig. 6-10. Notice that theplane, since it was halfway between the two charges, has zero potential. We havesolved the problem of a positive charge next to a grounded conducting sheet.

We have now solved for the total ﬁeld, but what about the real charges thatare responsible for it? There are, in addition to our positive point charge, someinduced negative charges on the conducting sheet that have been attracted bythe positive charge (from large distances away). Now suppose that for some

Fig. 6-10. The ﬁeld of a charge near a plane conducting surface, found by the method

of images.

6-9

technical reason—or out of curiosity—you would like to know how the negativecharges are distributed on the surface. You can ﬁnd the surface charge densityby using the result we worked out in Section 5-9 with Gauss’ law. The normalcomponent of the electric ﬁeld just outside a conductor is equal to the density ofsurface charge σ divided by 0. We can obtain the density of charge at any pointon the surface by working backwards from the normal component of the electricﬁeld at the surface. We know that, because we know the ﬁeld everywhere.

Consider a point on the surface at the distance ρ from the point directlybeneath the positive charge (Fig. 6-10). The electric ﬁeld at this point is normalto the surface and is directed into it. The component normal to the surface ofthe ﬁeld from the positive point charge is

En+ = − 14π0

aq

(a2 + ρ2)3/2 .

(6.28)

To this we must add the electric ﬁeld produced by the negative image charge.That just doubles the normal component (and cancels all others), so the chargedensity σ at any point on the surface isσ(ρ) = 0E(ρ) = −

(6.29)

2aq

4π(a2 + ρ2)3/2 .

An interesting check on our work is to integrate σ over the whole surface. Weﬁnd that the total induced charge is −q, as it should be.One further question: Is there a force on the point charge? Yes, because thereis an attraction from the induced negative surface charge on the plate. Now thatwe know what the surface charges are (from Eq. 6.29), we could compute theforce on our positive point charge by an integral. But we also know that the forceacting on the positive charge is exactly the same as it would be with the negativeimage charge instead of the plate, because the ﬁelds in the neighborhood arethe same in both cases. The point charge feels a force toward the plate whosemagnitude is

F = 14π0

q2(2a)2 .

(6.30)

We have found the force much more easily than by integrating over all the negativecharges.

6-9 A point charge near a conducting sphereWhat other surfaces besides a plane have a simple solution? The next mostsimple shape is a sphere. Let’s ﬁnd the ﬁelds around a grounded metal spherewhich has a point charge q near it, as shown in Fig. 6-11. Now we must look fora simple physical situation which gives a sphere for an equipotential surface. Ifwe look around at problems people have already solved, we ﬁnd that someonehas noticed that the ﬁeld of two unequal point charges has an equipotential thatis a sphere. Aha! If we choose the location of an image charge—and pick theright amount of charge—maybe we can make the equipotential surface ﬁt oursphere. Indeed, it can be done with the following prescription.

Assume that you want the equipotential surface to be a sphere of radius awith its center at the distance b from the charge q. Put an image charge ofstrength q0 = −q(a/b) on the line from the charge to the center of the sphere,and at a distance a2/b from the center. The sphere will be at zero potential.The mathematical reason stems from the fact that a sphere is the locus of allpoints for which the distances from two points are in a constant ratio. Referringto Fig. 6-11, the potential at P from q and q0 is proportional to

Fig. 6-11. The point charge q inducescharges on a grounded conducting spherewhose ﬁelds are those of an image charge q(cid:48)placed at the point shown.

+ q0r2

.

qr1

The potential will thus be zero at all points for which= − q0

or

q0r2

= − qr1

r2r1

q

.

6-10

If we place q0 at the distance a2/b from the center, the ratio r2/r1 has the constantvalue a/b. Then if

q0q

= − ab

(6.31)

the sphere is an equipotential. Its potential is, in fact, zero.

q.

What happens if we are interested in a sphere that is not at zero potential?That would be so only if its total charge happens accidentally to be q0. Of courseif it is grounded, the charges induced on it would have to be just that. But whatif it is insulated, and we have put no charge on it? Or if we know that the totalcharge Q has been put on it? Or just that it has a given potential not equalto zero? All these questions are easily answered. We can always add a pointcharge q00 at the center of the sphere. The sphere still remains an equipotentialby superposition; only the magnitude of the potential will be changed.If we have, for example, a conducting sphere which is initially uncharged andinsulated from everything else, and we bring near to it the positive point charge q,the total charge of the sphere will remain zero. The solution is found by usingan image charge q0 as before, but, in addition, adding a charge q00 at the centerof the sphere, choosing

q00 = −q0 = ab

(6.32)The ﬁelds everywhere outside the sphere are given by the superposition of theﬁelds of q, q0, and q00. The problem is solved.We can see now that there will be a force of attraction between the sphereand the point charge q. It is not zero even though there is no charge on theneutral sphere. Where does the attraction come from? When you bring a positivecharge up to a conducting sphere, the positive charge attracts negative charges tothe side closer to itself and leaves positive charges on the surface of the far side.The attraction by the negative charges exceeds the repulsion from the positivecharges; there is a net attraction. We can ﬁnd out how large the attraction isby computing the force on q in the ﬁeld produced by q0 and q00. The total forceis the sum of the attractive force between q and a charge q0 = −(a/b)q, at thedistance b − (a2/b), and the repulsive force between q and a charge q00 = +(a/b)qat the distance b.Those who were entertained in childhood by the baking powder box whichhas on its label a picture of a baking powder box which has on its label a pictureof a baking powder box which has . . . may be interested in the following problem.Two equal spheres, one with a total charge of +Q and the other with a totalcharge of −Q, are placed at some distance from each other. What is the forcebetween them? The problem can be solved with an inﬁnite number of images.One ﬁrst approximates each sphere by a charge at its center. These charges willhave image charges in the other sphere. The image charges will have images, etc.,etc., etc. The solution is like the picture on the box of baking powder—and itconverges pretty fast.

6-10 Condensers; parallel platesWe take up now another kind of a problem involving conductors. Consider twolarge metal plates which are parallel to each other and separated by a distancesmall compared with their width. Let’s suppose that equal and opposite chargeshave been put on the plates. The charges on each plate will be attracted by thecharges on the other plate, and the charges will spread out uniformly on the innersurfaces of the plates. The plates will have surface charge densities +σ and −σ,respectively, as in Fig. 6-12. From Chapter 5 we know that the ﬁeld between theplates is σ/0, and that the ﬁeld outside the plates is zero. The plates will havediﬀerent potentials φ1 and φ2. For convenience we will call the diﬀerence V ; it isoften called the「voltage」:

φ1 − φ2 = V.

(You will ﬁnd that sometimes people use V for the potential, but we have chosento use φ.)

6-11

Fig. 6-12. A parallel-plate condenser.

The potential diﬀerence V is the work per unit charge required to carry a

small charge from one plate to the other, so that

V = Ed = σ0

d = d0A

Q,

(6.33)

where ±Q is the total charge on each plate, A is the area of the plates, and d isthe separation.We ﬁnd that the voltage is proportional to the charge. Such a proportionalitybetween V and Q is found for any two conductors in space if there is a pluscharge on one and an equal minus charge on the other. The potential diﬀerencebetween them—that is, the voltage—will be proportional to the charge. (We areassuming that there are no other charges around.)

Why this proportionality? Just the superposition principle. Suppose we knowthe solution for one set of charges, and then we superimpose two such solutions.The charges are doubled, the ﬁelds are doubled, and the work done in carrying aunit charge from one point to the other is also doubled. Therefore the potentialdiﬀerence between any two points is proportional to the charges. In particular,the potential diﬀerence between the two conductors is proportional to the chargeson them. Someone originally wrote the equation of proportionality the other way.That is, they wrote

Q = CV,

where C is a constant. This coeﬃcient of proportionality is called the capacity,and such a system of two conductors is called a condenser.* For our parallel-platecondenser

C = 0Ad

(parallel plates).

(6.34)

This formula is not exact, because the ﬁeld is not really uniform everywherebetween the plates, as we assumed. The ﬁeld does not just suddenly quit at theedges, but really is more as shown in Fig. 6-13. The total charge is not σA, as wehave assumed—there is a little correction for the eﬀects at the edges. To ﬁnd outwhat the correction is, we will have to calculate the ﬁeld more exactly and ﬁndout just what does happen at the edges. That is a complicated mathematicalproblem which can, however, be solved by techniques which we will not describenow. The result of such calculations is that the charge density rises somewhatnear the edges of the plates. This means that the capacity of the plates is a littlehigher than we computed.

We have talked about the capacity for two conductors only. Sometimes peopletalk about the capacity of a single object. They say, for instance, that the capacityof a sphere of radius a is 4π0a. What they imagine is that the other terminal isanother sphere of inﬁnite radius—that when there is a charge +Q on the sphere,the opposite charge, −Q, is on an inﬁnite sphere. One can also speak of capacitieswhen there are three or more conductors, a discussion we shall, however, defer.Suppose that we wish to have a condenser with a very large capacity. Wecould get a large capacity by taking a very big area and a very small separation.We could put waxed paper between sheets of aluminum foil and roll it up. (Ifwe seal it in plastic, we have a typical radio-type condenser.) What good is it?It is good for storing charge. If we try to store charge on a ball, for example,its potential rises rapidly as we charge it up. It may even get so high that thecharge begins to escape into the air by way of sparks. But if we put the samecharge on a condenser whose capacity is very large, the voltage developed acrossthe condenser will be small.

In many applications in electronic circuits, it is useful to have somethingwhich can absorb or deliver large quantities of charge without changing itspotential much. A condenser (or「capacitor」) does just that. There are alsomany applications in electronic instruments and in computers where a condenser

* Some people think the words「capacitance」and「capacitor」should be used, instead of「capacity」and「condensor.」We have decided to use the older terminology, because it is stillmore commonly heard in the physics laboratory—even if not in textbooks!

6-12

Fig. 6-13. The electric ﬁeld near the edge

of two parallel plates.

is used to get a speciﬁed change in voltage in response to a particular changein charge. We have seen a similar application in Chapter 23, Vol. I, where wedescribed the properties of resonant circuits.

From the deﬁnition of C, we see that its unit is one coulomb/volt. This unitis also called a farad. Looking at Eq. (6.34), we see that one can express theunits of 0 as farad/meter, which is the unit most commonly used. Typical sizesof condensers run from one micro-microfarad (1 picofarad) to millifarads. Smallcondensers of a few picofarads are used in high-frequency tuned circuits, andcapacities up to hundreds or thousands of microfarads are found in power-supplyﬁlters. A pair of plates one square centimeter in area with a one millimeterseparation have a capacity of roughly one micro-microfarad.

0 ≈

1

36π × 109 farad/meter

6-11 High-voltage breakdownWe would like now to discuss qualitatively some of the characteristics of theﬁelds around conductors. If we charge a conductor that is not a sphere, but onethat has on it a point or a very sharp end, as, for example, the object sketchedin Fig. 6-14, the ﬁeld around the point is much higher than the ﬁeld in the otherregions. The reason is, qualitatively, that charges try to spread out as much aspossible on the surface of a conductor, and the tip of a sharp point is as far awayas it is possible to be from most of the surface. Some of the charges on the plateget pushed all the way to the tip. A relatively small amount of charge on the tipcan still provide a large surface density; a high charge density means a high ﬁeldjust outside.One way to see that the ﬁeld is highest at those places on a conductor wherethe radius of curvature is smallest is to consider the combination of a big sphereand a little sphere connected by a wire, as shown in Fig. 6-15. It is a somewhatidealized version of the conductor of Fig. 6-14. The wire will have little inﬂuenceon the ﬁelds outside; it is there to keep the spheres at the same potential. Now,which ball has the biggest ﬁeld at its surface? If the ball on the left has theradius a and carries a charge Q, its potential is about

(Of course the presence of one ball changes the charge distribution on the other,so that the charges are not really spherically symmetric on either. But if we areinterested only in an estimate of the ﬁelds, we can use the potential of a sphericalcharge.) If the smaller ball, whose radius is b, carries the charge q, its potentialis about

φ1 = 14π0

Qa

.

φ2 = 14π0

qb

.

Qa

= qb

.

But φ1 = φ2, so

On the other hand, the ﬁeld at the surface (see Eq. 5.8) is proportional to thesurface charge density, which is like the total charge over the radius squared. Weget that

= Q/a2q/b2

.

EaEb

= ba

(6.35)Therefore the ﬁeld is higher at the surface of the small sphere. The ﬁelds are inthe inverse proportion of the radii.

This result is technically very important, because air will break down if theelectric ﬁeld is too great. What happens is that a loose charge (electron, or ion)somewhere in the air is accelerated by the ﬁeld, and if the ﬁeld is very great,the charge can pick up enough speed before it hits another atom to be able toknock an electron oﬀ that atom. As a result, more and more ions are produced.Their motion constitutes a discharge, or spark. If you want to charge an objectto a high potential and not have it discharge itself by sparks in the air, you mustbe sure that the surface is smooth, so that there is no place where the ﬁeld isabnormally large.

6-13

Fig. 6-14. The electric ﬁeld near a sharp

point on a conductor is very high.

Fig. 6-15. The ﬁeld of a pointed objectcan be approximated by that of two spheresat the same potential.

6-12 The ﬁeld-emission microscopeThere is an interesting application of the extremely high electric ﬁeld whichsurrounds any sharp protuberance on a charged conductor. The ﬁeld-emissionmicroscope depends for its operation on the high ﬁelds produced at a sharpmetal point.* It is built in the following way. A very ﬁne needle, with a tipwhose diameter is about 1000 angstroms, is placed at the center of an evacuatedglass sphere (Fig. 6-16). The inner surface of the sphere is coated with a thinconducting layer of ﬂuorescent material, and a very high potential diﬀerence isapplied between the ﬂuorescent coating and the needle.

Let’s ﬁrst consider what happens when the needle is negative with respect tothe ﬂuorescent coating. The ﬁeld lines are highly concentrated at the sharp point.The electric ﬁeld can be as high as 40 million volts per centimeter. In such intenseﬁelds, electrons are pulled out of the surface of the needle and accelerated acrossthe potential diﬀerence between the needle and the ﬂuorescent layer. When theyarrive there they cause light to be emitted, just as in a television picture tube.The electrons which arrive at a given point on the ﬂuorescent surface are, toan excellent approximation, those which leave the other end of the radial ﬁeldline, because the electrons will travel along the ﬁeld line passing from the pointto the surface. Thus we see on the surface some kind of an image of the tip ofthe needle. More precisely, we see a picture of the emissivity of the surface of theneedle—that is the ease with which electrons can leave the surface of the metaltip. If the resolution were high enough, one could hope to resolve the positionsof the individual atoms on the tip of the needle. With electrons, this resolutionis not possible for the following reasons. First, there is quantum-mechanicaldiﬀraction of the electron waves which blurs the image. Second, due to theinternal motions of the electrons in the metal they have a small sideways initialvelocity when they leave the needle, and this random transverse component ofthe velocity causes some smearing of the image. The combination of these twoeﬀects limits the resolution to 25 Å or so.

If, however, we reverse the polarity and introduce a small amount of helium gasinto the bulb, much higher resolutions are possible. When a helium atom collideswith the tip of the needle, the intense ﬁeld there strips an electron oﬀ the heliumatom, leaving it positively charged. The helium ion is then accelerated outwardalong a ﬁeld line to the ﬂuorescent screen. Since the helium ion is so much heavierthan an electron, the quantum-mechanical wavelengths are much smaller. If thetemperature is not too high, the eﬀect of the thermal velocities is also smallerthan in the electron case. With less smearing of the image a much sharper pictureof the point is obtained. It has been possible to obtain magniﬁcations up to2,000,000 times with the positive ion ﬁeld-emission microscope—a magniﬁcationten times better than is obtained with the best electron microscope.Figure 6-17 is an example of the results which were obtained with a ﬁeld-ionmicroscope, using a tungsten needle. The center of a tungsten atom ionizes ahelium atom at a slightly diﬀerent rate than the spaces between the tungstenatoms. The pattern of spots on the ﬂuorescent screen shows the arrangement ofthe individual atoms on the tungsten tip. The reason the spots appear in ringscan be understood by visualizing a large box of balls packed in a rectangulararray, representing the atoms in the metal. If you cut an approximately sphericalsection out of this box, you will see the ring pattern characteristic of the atomicstructure. The ﬁeld-ion microscope provided human beings with the means ofseeing atoms for the ﬁrst time. This is a remarkable achievement, consideringthe simplicity of the instrument.

* See E. W. Müller:「The ﬁeld-ion microscope,」Advances in Electronics and Electron

Physics, 13, 83–179 (1960). Academic Press, New York.

6-14

Fig. 6-16. Field-emission microscope.

Fig. 6-17.

Image produced by a ﬁeld-emission microscope. [Courtesy of Erwin W.Müller, Research Prof. of Physics, Pennsyl-vania State University.]
