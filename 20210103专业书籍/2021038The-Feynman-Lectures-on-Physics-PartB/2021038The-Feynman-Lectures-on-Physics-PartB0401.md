4

Electrostatics

4-1 StaticsWe

begin now our detailed study of the theory of electromagnetism. All of

electromagnetism is contained in the Maxwell equations.

Maxwell’s equations:

∇ · E = ρ0

,

,

∇ × E = − ∂B∂tc2 ∇ × B = ∂E+ j∂t0∇ · B = 0.

,

(4.1)

(4.2)

(4.3)

(4.4)

The situations that are described by these equations can be very complicated.We will consider ﬁrst relatively simple situations, and learn how to handle thembefore we take up more complicated ones. The easiest circumstance to treat isone in which nothing depends on the time—called the static case. All chargesare permanently ﬁxed in space, or if they do move, they move as a steady ﬂowin a circuit (so ρ and j are constant in time). In these circumstances, all of theterms in the Maxwell equations which are time derivatives of the ﬁeld are zero.In this case, the Maxwell equations become:

Electrostatics:

Magnetostatics:

∇ · E = ρ0∇ × E = 0.

,

∇ × B = j∇ · B = 0.

0c2 ,

(4.5)

(4.6)

(4.7)

(4.8)

You will notice an interesting thing about this set of four equations. It canbe separated into two pairs. The electric ﬁeld E appears only in the ﬁrst two,and the magnetic ﬁeld B appears only in the second two. The two ﬁelds arenot interconnected. This means that electricity and magnetism are distinctphenomena so long as charges and currents are static. The interdependence of Eand B does not appear until there are changes in charges or currents, as when acondensor is charged, or a magnet moved. Only when there are suﬃciently rapidchanges, so that the time derivatives in Maxwell’s equations become signiﬁcant,will E and B depend on each other.Now if you look at the equations of statics you will see that the study ofthe two subjects we call electrostatics and magnetostatics is ideal from thepoint of view of learning about the mathematical properties of vector ﬁelds.Electrostatics is a neat example of a vector ﬁeld with zero curl and a givendivergence. Magnetostatics is a neat example of a ﬁeld with zero divergenceand a given curl. The more conventional—and you may be thinking, moresatisfactory—way of presenting the theory of electromagnetism is to start ﬁrstwith electrostatics and thus to learn about the divergence. Magnetostatics andthe curl are taken up later. Finally, electricity and magnetism are put together.4-1

We have chosen to start with the complete theory of vector calculus. Now weshall apply it to the special case of electrostatics, the ﬁeld of E given by the ﬁrstpair of equations.We will begin with the simplest situations—ones in which the positions of allcharges are speciﬁed. If we had only to study electrostatics at this level (as weshall do in the next two chapters), life would be very simple—in fact, almost trivial.Everything can be obtained from Coulomb’s law and some integration, as youwill see. In many real electrostatic problems, however, we do not know, initially,where the charges are. We know only that they have distributed themselves inways that depend on the properties of matter. The positions that the charges takeup depend on the E ﬁeld, which in turn depends on the positions of the charges.Then things can get quite complicated. If, for instance, a charged body is broughtnear a conductor or insulator, the electrons and protons in the conductor orinsulator will move around. The charge density ρ in Eq. (4.5) may have onepart that we know about, from the charge that we brought up; but there willbe other parts from charges that have moved around in the conductor. And allof the charges must be taken into account. One can get into some rather subtleand interesting problems. So although this chapter is to be on electrostatics, itwill not cover the more beautiful and subtle parts of the subject. It will treatonly the situation where we can assume that the positions of all the charges areknown. Naturally, you should be able to do that case before you try to handlethe other ones.

Coulomb’s law:

4-2 Coulomb’s law; superpositionIt would be logical to use Eqs. (4.5) and (4.6) as our starting points. It willbe easier, however, if we start somewhere else and come back to these equations.The results will be equivalent. We will start with a law that we have talkedabout before, called Coulomb’s law, which says that between two charges at restthere is a force directly proportional to the product of the charges and inverselyproportional to the square of the distance between. The force is along the straightline from one charge to the other.F 1 = 14π0

(4.9)F 1 is the force on charge q1, e12 is the unit vector in the direction to q1 from q2,and r12 is the distance between q1 and q2. The force F 2 on q2 is equal andopposite to F 1.The constant of proportionality, for historical reasons, is written as 1/4π0.In the system of units which we use—the mks system—it is deﬁned as exactly10−7 times the speed of light squared. Now since the speed of light is approximately3 × 108 meters per second, the constant is approximately 9 × 109, and the unitturns out to be newton·meter2 per coulomb2 or volt·meter per coulomb.

e12 = −F 2.

q1q2r212

= 10−7c2= 9.0 × 109

(by deﬁnition)(by experiment).

(4.10)

14π0

Unit: newton·meter2/coulomb2,

or volt·meter/coulomb.

When there are more than two charges present—the only really interestingtimes—we must supplement Coulomb’s law with one other fact of nature: theforce on any charge is the vector sum of the Coulomb forces from each of theother charges. This fact is called「the principle of superposition.」That’s allthere is to electrostatics. If we combine the Coulomb law and the principle ofsuperposition, there is nothing else. Equations (4.5) and (4.6)—the electrostaticequations—say no more and no less.

When applying Coulomb’s law, it is convenient to introduce the idea of anelectric ﬁeld. We say that the ﬁeld E(1) is the force per unit charge on q1 (due4-2

to all other charges). Dividing Eq. (4.9) by q1, we have, for one other chargebesides q1,

E(1) = 14π0

q2r212

e12.

(4.11)

Also, we consider that E(1) describes something about the point (1) even if q1were not there—assuming that all other charges keep their same positions. Wesay: E(1) is the electric ﬁeld at the point (1).The electric ﬁeld E is a vector, so by Eq. (4.11) we really mean three equa-tions—one for each component. Writing out explicitly the x-component, Eq. (4.11)means

Ex(x1, y1, z1) = q24π0

x1 − x2

[(x1 − x2)2 + (y1 − y2)2 + (z1 − z2)2]3/2 ,

(4.12)

and similarly for the other components.

If there are many charges present, the ﬁeld E at any point (1) is a sum ofthe contributions from each of the other charges. Each term of the sum will looklike (4.11) or (4.12). Letting qj be the magnitude of the jth charge, and r1j thedisplacement from qj to the point (1), we writeqjr21j

E(1) =X

14π0

(4.13)

e1j.

j

Which means, of course,

Ex(x1, y1, z1) =X

j

14π0

qj(x1 − xj)

[(x1 − xj)2 + (y1 − yj)2 + (z1 − zj)2]3/2 ,

(4.14)

and so on.

Often it is convenient to ignore the fact that charges come in packages likeelectrons and protons, and think of them as being spread out in a continuoussmear—or in a「distribution,」as it is called. This is O.K. so long as we arenot interested in what is happening on too small a scale. We describe a chargedistribution by the「charge density,」ρ(x, y, z). If the amount of charge in a smallvolume ∆V2 located at the point (2) is ∆q2, then ρ is deﬁned by

(4.15)To use Coulomb’s law with such a description, we replace the sums of Eqs.(4.13) or (4.14) by integrals over all volumes containing charges. Then we have

∆q2 = ρ(2)∆V2.

E(1) = 14π0

ρ(2)e12 dV2

r212

.

(4.16)

all

space

e12 = r12r12

,

Z

Z

all

space

Some people prefer to write

where r12 is the vector displacement to (1) from (2), as shown in Fig. 4-1. Theintegral for E is then written as

E(1) = 14π0

ρ(2)r12 dV2

r312

.

(4.17)

Fig. 4-1. The electric ﬁeld E at point (1),from a charge distribution, is obtained froman integral over the distribution. Point (1)could also be inside the distribution.

When we want to calculate something with these integrals, we usually haveto write them out in explicit detail. For the x-component of either Eq. (4.16)or (4.17), we would have

Ex(x1, y1, z1) =

Z

all

space

(x1 − x2)ρ(x2, y2, z2) dx2 dy2 dz2

4π0[(x1 − x2)2 + (y1 − y2)2 + (z1 − z2)2]3/2 .

(4.18)

4-3

We are not going to use this formula much. We write it here only to emphasizethe fact that we have completely solved all the electrostatic problems in whichwe know the locations of all of the charges. Given the charges, what are theﬁelds? Answer: Do this integral. So there is nothing to the subject; it is just acase of doing complicated integrals over three dimensions—strictly a job for acomputing machine!

With our integrals we can ﬁnd the ﬁelds produced by a sheet of charge, from aline of charge, from a spherical shell of charge, or from any speciﬁed distribution.It is important to realize, as we go on to draw ﬁeld lines, to talk about potentials,or to calculate divergences, that we already have the answer here. It is merely amatter of it being sometimes easier to do an integral by some clever guessworkthan by actually carrying it out. The guesswork requires learning all kinds ofstrange things. In practice, it might be easier to forget trying to be clever andalways to do the integral directly instead of being so smart. We are, however,going to try to be smart about it. We shall go on to discuss some other featuresof the electric ﬁeld.

4-3 Electric potentialFirst we take up the idea of electric potential, which is related to the workdone in carrying a charge from one point to another. There is some distributionof charge, which produces an electric ﬁeld. We ask about how much work itwould take to carry a small charge from one place to another. The work doneagainst the electrical forces in carrying a charge along some path is the negativeof the component of the electrical force in the direction of the motion, integratedalong the path. If we carry a charge from point a to point b,

Z b

a

W = −

F · ds,

Z b

where F is the electrical force on the charge at each point, and ds is the diﬀerentialvector displacement along the path. (See Fig. 4-2.)It is more interesting for our purposes to consider the work that would bedone in carrying one unit of charge. Then the force on the charge is numericallythe same as the electric ﬁeld. Calling the work done against electrical forces inthis case W(unit), we write

W(unit) = −

E · ds.

(4.19)

a

Now, in general, what we get with this kind of an integral depends on the pathwe take. But if the integral of (4.19) depended on the path from a to b, we couldget work out of the ﬁeld by carrying the charge to b along one path and thenback to a on the other. We would go to b along the path for which W is smallerand back along the other, getting out more work than we put in.There is nothing impossible, in principle, about getting energy out of a ﬁeld.We shall, in fact, encounter ﬁelds where it is possible. It could be that as youmove a charge you produce forces on the other part of the「machinery.」If the「machinery」moved against the force it would lose energy, thereby keeping thetotal energy in the world constant. For electrostatics, however, there is no such「machinery.」We know what the forces back on the sources of the ﬁeld are. Theyare the Coulomb forces on the charges responsible for the ﬁeld. If the other chargesare ﬁxed in position—as we assume in electrostatics only—these back forces cando no work on them. There is no way to get energy from them—provided, ofcourse, that the principle of energy conservation works for electrostatic situations.We believe that it will work, but let’s just show that it must follow from Coulomb’slaw of force.

We consider ﬁrst what happens in the ﬁeld due to a single charge q. Letpoint a be at the distance ra from q, and point b at rb. Now we carry a diﬀerentcharge, which we will call the「test」charge, and whose magnitude we choose to4-4

Fig. 4-2. The work done in carrying acharge from a to b is the negative of theintegral of F · ds along the path taken.

Z b

a

−

Z b

a0

(cid:19)

(cid:18) 1

ra

− 1

rb

be one unit, from a to b. Let’s start with the easiest possible path to calculate.We carry our test charge ﬁrst along the arc of a circle, then along a radius, asshown in part (a) of Fig. 4-3. Now on that particular path it is child’s play toﬁnd the work done (otherwise we wouldn’t have picked it). First, there is nowork done at all on the path from a to a0. The ﬁeld is radial (from Coulomb’slaw), so it is at right angles to the direction of motion. Next, on the path froma0 to b, the ﬁeld is in the direction of motion and varies as 1/r2. Thus the workdone on the test charge in carrying it from a to b would be

E · ds = − q4π0

drr2

= − q4π0

.

(4.20)

Now let’s take another easy path. For instance, the one shown in part (b)of Fig. 4-3. It goes for awhile along an arc of a circle, then radially for awhile,then along an arc again, then radially, and so on. Every time we go along thecircular parts, we do no work. Every time we go along the radial parts, we mustjust integrate 1/r2. Along the ﬁrst radial stretch, we integrate from ra to ra0,then along the next radial stretch from ra0 to ra00, and so on. The sum of allthese integrals is the same as a single integral directly from ra to rb. We get thesame answer for this path that we did for the ﬁrst path we tried. It is clear thatwe would get the same answer for any path which is made up of an arbitrarynumber of the same kinds of pieces.What about smooth paths? Would we get the same answer? We discussedthis point previously in Chapter 13 of Vol. I. Applying the same arguments usedthere, we can conclude that work done in carrying a unit charge from a to b isindependent of the path.

)

W(unit)a → b

Z b

aanypath

= −

E · ds.

Since the work done depends only on the endpoints, it can be represented asthe diﬀerence between two numbers. We can see this in the following way. Let’schoose a reference point P0 and agree to evaluate our integral by using a paththat always goes by way of point P0. Let φ(a) stand for the work done againstthe ﬁeld in going from P0 to point a, and let φ(b) be the work done in goingfrom P0 to point b (Fig. 4-4). The work in going to P0 from a (on the way to b)is the negative of φ(a), so we have that

Z b

a

−

E · ds = φ(b) − φ(a).

(4.21)

Since only the diﬀerence in the function φ at two points is ever involved, wedo not really have to specify the location of P0. Once we have chosen somereference point, however, a number φ is determined for any point in space; φ isthen a scalar ﬁeld. It is a function of x, y, z. We call this scalar function theelectrostatic potential at any point.

Electrostatic potential:

φ(P) = −

E · ds.

(4.22)

Z P

P0

For convenience, we will often take the reference point at inﬁnity. Then, for asingle charge at the origin, the potential φ is given for any point (x, y, z)—usingEq. (4.20):

φ(x, y, z) = q4π0

1r

.

(4.23)

The electric ﬁeld from several charges can be written as the sum of the electricﬁeld from the ﬁrst, from the second, from the third, etc. When we integratethe sum to ﬁnd the potential we get a sum of integrals. Each of the integrals4-5

Fig. 4-3. In carrying a test charge froma to b the same work is done along eitherpath.

Fig. 4-4. The work done in going alongany path from a to b is the negative of thework from some point P0 to a plus the workfrom P0 to b.

is the negative of the potential from one of the charges. We conclude thatthe potential φ from a lot of charges is the sum of the potentials from all theindividual charges. There is a superposition principle also for potentials. Usingthe same kind of arguments by which we found the electric ﬁeld from a group ofcharges and for a distribution of charges, we can get the complete formulas forthe potential φ at a point we call (1):

φ(1) =Xφ(1) = 14π0

j

14π0

Z

all

space

,

qjr1jρ(2) dV2

r12

.

(4.24)

(4.25)

Remember that the potential φ has a physical signiﬁcance: it is the potentialenergy which a unit charge would have if brought to the speciﬁed point in spacefrom some reference point.

4-4 E = −∇φWho cares about φ? Forces on charges are given by E, the electric ﬁeld. Thepoint is that E can be obtained easily from φ—it is as easy, in fact, as taking aderivative. Consider two points, one at x and one at (x + ∆x), but both at thesame y and z, and ask how much work is done in carrying a unit charge fromone point to the other. The path is along the horizontal line from x to x + ∆x.The work done is the diﬀerence in the potential at the two points:

∆W = φ(x + ∆x, y, z) − φ(x, y, z) = ∂φ∂xBut the work done against the ﬁeld for the same path is

∆x.

∆W = −

We see that

E · ds = −Ex ∆x.

Z

Z b

.

Ex = − ∂φ∂x

(4.26)Similarly, Ey = −∂φ/∂y, Ez = −∂φ/∂z, or, summarizing with the notation ofvector analysis,(4.27)This equation is the diﬀerential form of Eq. (4.22). Any problem with speciﬁedcharges can be solved by computing the potential from (4.24) or (4.25) andusing (4.27) to get the ﬁeld. Equation (4.27) also agrees with what we foundfrom vector calculus: that for any scalar ﬁeld φ

E = −∇φ.

∇φ · ds = φ(b) − φ(a).

(4.28)

a

According to Eq. (4.25) the scalar potential φ is given by a three-dimensionalintegral similar to the one we had for E. Is there any advantage to computing φrather than E? Yes. There is only one integral for φ, while there are threeintegrals for E—because it is a vector. Furthermore, 1/r is usually a little easierto integrate than x/r3. It turns out in many practical cases that it is easier tocalculate φ and then take the gradient to ﬁnd the electric ﬁeld, than it is toevaluate the three integrals for E. It is merely a practical matter.There is also a deeper physical signiﬁcance to the potential φ. We haveshown that E of Coulomb’s law is obtained from E = − grad φ, when φ is givenby (4.22). But if E is equal to the gradient of a scalar ﬁeld, then we know fromthe vector calculus that the curl of E must vanish:

∇ × E = 0.

(4.29)4-6

But that is just our second fundamental equation of electrostatics, Eq. (4.6). Wehave shown that Coulomb’s law gives an E ﬁeld that satisﬁes that condition. Sofar, everything is all right.We had really proved that ∇ × E was zero before we deﬁned the potential.

We had shown that the work done around a closed path is zero. That is, that

I

E · ds = 0

for any path. We saw in Chapter 3 that for any such ﬁeld ∇ × E must be zeroeverywhere. The electric ﬁeld in electrostatics is an example of a curl-free ﬁeld.You can practice your vector calculus by proving that ∇ × E is zero in adiﬀerent way—by computing the components of ∇ × E for the ﬁeld of a pointcharge, as given by Eq. (4.11). If you get zero, the superposition principle saysyou would get zero for the ﬁeld of any charge distribution.

We should point out an important fact. For any radial force the work doneis independent of the path, and there exists a potential. If you think aboutit, the entire argument we made above to show that the work integral wasindependent of the path depended only on the fact that the force from a singlecharge was radial and spherically symmetric. It did not depend on the fact thatthe dependence on distance was as 1/r2—there could have been any r dependence.The existence of a potential, and the fact that the curl of E is zero, comes reallyonly from the symmetry and direction of the electrostatic forces. Because of this,Eq. (4.28)—or (4.29)—can contain only part of the laws of electricity.

4-5 The ﬂux of EWe will now derive a ﬁeld equation that depends speciﬁcally and directly onthe fact that the force law is inverse square. That the ﬁeld varies inversely asthe square of the distance seems, for some people, to be「only natural,」because「that’s the way things spread out.」Take a light source with light streaming out:the amount of light that passes through a surface cut out by a cone with itsapex at the source is the same no matter at what radius the surface is placed. Itmust be so if there is to be conservation of light energy. The amount of light perunit area—the intensity—must vary inversely as the area cut by the cone, i. e.,inversely as the square of the distance from the source. Certainly the electric ﬁeldshould vary inversely as the square of the distance for the same reason! But thereis no such thing as the「same reason」here. Nobody can say that the electric ﬁeldmeasures the ﬂow of something like light which must be conserved. If we hada「model」of the electric ﬁeld in which the electric ﬁeld vector represented thedirection and speed—say the current—of some kind of little「bullets」which wereﬂying out, and if our model required that these bullets were conserved, that nonecould ever disappear once it was shot out of a charge, then we might say thatwe can「see」that the inverse square law is necessary. On the other hand, therewould necessarily be some mathematical way to express this physical idea. If theelectric ﬁeld were like conserved bullets going out, then it would vary inverselyas the square of the distance and we would be able to describe that behavior byan equation—which is purely mathematical. Now there is no harm in thinkingthis way, so long as we do not say that the electric ﬁeld is made out of bullets,but realize that we are using a model to help us ﬁnd the right mathematics.Suppose, indeed, that we imagine for a moment that the electric ﬁeld didrepresent the ﬂow of something that was conserved—everywhere, that is, exceptat charges. (It has to start somewhere!) We imagine that whatever it is ﬂows outof a charge into the space around. If E were the vector of such a ﬂow (as h is forheat ﬂow), it would have a 1/r2 dependence near a point source. Now we wishto use this model to ﬁnd out how to state the inverse square law in a deeper ormore abstract way, rather than simply saying「inverse square.」(You may wonderwhy we should want to avoid the direct statement of such a simple law, and wantinstead to imply the same thing sneakily in a diﬀerent way. Patience! It willturn out to be useful.)

4-7

Closed Surface S

Eb

Ea

b

Surface S

En

θ

E

∆a

a

+Point Charge

Fig. 4-5. The ﬂux of E out of the sur-

face S is zero.

+Point Charge

Fig. 4-6. The ﬂux of E out of the sur-

face S is zero.

We ask: What is the「ﬂow」of E out of an arbitrary closed surface in theneighborhood of a point charge? First let’s take an easy surface—the one shownin Fig. 4-5. If the E ﬁeld is like a ﬂow, the net ﬂow out of this box should be zero.That is what we get if by the「ﬂow」from this surface we mean the surface integralof the normal component of E—that is, the ﬂux of E. On the radial faces, thenormal component is zero. On the spherical faces, the normal component En isjust the magnitude of E—minus for the smaller face and plus for the larger face.The magnitude of E decreases as 1/r2, but the surface area is proportional to r2,so the product is independent of r. The ﬂux of E into face a is just cancelled by theﬂux out of face b. The total ﬂow out of S is zero, which is to say that for this surface

Z

En da = 0.

(4.30)

S

Next we show that the two end surfaces may be tilted with respect to the radialline without changing the integral (4.30). Although it is true in general, for ourpurposes it is only necessary to show that this is true when the end surfaces aresmall, so that they subtend a small angle from the source—in fact, an inﬁnitesimalangle. In Fig. 4-6 we show a surface S whose「sides」are radial, but whose「ends」are tilted. The end surfaces are not small in the ﬁgure, but you are to imaginethe situation for very small end surfaces. Then the ﬁeld E will be suﬃcientlyuniform over the surface that we can use just its value at the center. When wetilt the surface by an angle θ, the area is increased by the factor 1/ cos θ. But En,the component of E normal to the surface, is decreased by the factor cos θ. Theproduct En ∆a is unchanged. The ﬂux out of the whole surface S is still zero.Now it is easy to see that the ﬂux out of a volume enclosed by any surface Smust be zero. Any volume can be thought of as made up of pieces, like that inFig. 4-6. The surface will be subdivided completely into pairs of end surfaces,and since the ﬂuxes in and out of these end surfaces cancel by pairs, the totalﬂux out of the surface will be zero. The idea is illustrated in Fig. 4-7. We havethe completely general result that the total ﬂux of E out of any surface S in theﬁeld of a point charge is zero.But notice! Our proof works only if the surface S does not surround thecharge. What would happen if the point charge were inside the surface? Wecould still divide our surface into pairs of areas that are matched by radial linesthrough the charge, as shown in Fig. 4-8. The ﬂuxes through the two surfacesare still equal—by the same arguments as before—only now they have the samesign. The ﬂux out of a surface that surrounds a charge is not zero. Then whatis it? We can ﬁnd out by a little trick. Suppose we「remove」the charge fromthe「inside」by surrounding the charge by a little surface S0 totally inside theoriginal surface S, as shown in Fig. 4-9. Now the volume enclosed between thetwo surfaces S and S0 has no charge in it. The total ﬂux out of this volume(including that through S0) is zero, by the arguments we have given above. Thearguments tell us, in fact, that the ﬂux into the volume through S0 is the sameas the ﬂux outward through S.

4-8

Fig. 4-7. Any volume can be thoughtof as completely made up of inﬁnitesimaltruncated cones. The ﬂux of E from oneend of each conical segment is equal andopposite to the ﬂux from the other end. Thetotal ﬂux from the surface S is thereforezero.

Fig. 4-8. If a charge is inside a surface,

the ﬂux out is not zero.

Fig. 4-9. The ﬂux through S is the same

as the ﬂux through S(cid:48).

Fig. 4-10. The ﬂux through a sphericalsurface containing a point charge q is q/0.

We can choose any shape we wish for S0, so let’s make it a sphere centeredon the charge, as in Fig. 4-10. Then we can easily calculate the ﬂux through it.If the radius of the little sphere is r, the value of E everywhere on its surface is

14π0

qr2 ,

and is directed always normal to the surface. We ﬁnd the total ﬂux through S0 ifwe multiply this normal component of E by the surface area:

(cid:18) 1

(cid:19)

Flux through the surface S0 =

4π0

qr2

(4πr2) = q0

,

(4.31)

a number independent of the radius of the sphere! We know then that the ﬂuxoutward through S is also q/0—a value independent of the shape of S so longas the charge q is inside.

We can write our conclusions as follows:

Z

any surface S

0;

q0

En da =

q outside Sq inside S

;

(4.32)

Let’s return to our「bullet」analogy and see if it makes sense. Our theorem saysthat the net ﬂow of bullets through a surface is zero if the surface does not enclosethe gun that shoots the bullets. If the gun is enclosed in a surface, whatever sizeand shape it is, the number of bullets passing through is the same—it is given bythe rate at which bullets are generated at the gun. It all seems quite reasonable forconserved bullets. But does the model tell us anything more than we get simply bywriting Eq. (4.32)? No one has succeeded in making these「bullets」do anythingelse but produce this one law. After that, they produce nothing but errors. Thatis why today we prefer to represent the electromagnetic ﬁeld purely abstractly.

4-6 Gauss’ law; the divergence of EOur nice result, Eq. (4.32), was proved for a single point charge. Now supposethat there are two charges, a charge q1 at one point and a charge q2 at another.The problem looks more diﬃcult. The electric ﬁeld whose normal component weintegrate for the ﬂux is the ﬁeld due to both charges. That is, if E1 representsthe electric ﬁeld that would have been produced by q1 alone, and E2 representsthe electric ﬁeld produced by q2 alone, the total electric ﬁeld is E = E1 + E2.The ﬂux through any closed surface S is

Z

Z

Z

(E1n + E2n) da =

E1n da +

E2n da.

(4.33)

S

S

S

The ﬂux with both charges present is the ﬂux due to a single charge plus the ﬂuxdue to the other charge. If both charges are outside S, the ﬂux through S is zero.If q1 is inside S but q2 is outside, then the ﬁrst integral gives q1/0 and the secondintegral gives zero. If the surface encloses both charges, each will give its contribu-tion and we have that the ﬂux is (q1 + q2)/0. The general rule is clearly that thetotal ﬂux out of a closed surface is equal to the total charge inside, divided by 0.Our result is an important general law of the electrostatic ﬁeld, called Gauss’law.

Gauss’ law:

Z

or

any closedsurface S

En da = sum of charges insideZ

0

E · n da = Qint0

,

any closedsurface S

,

(4.34)

(4.35)

4-9

Z

where

Qint = X

inside S

qi.

(4.36)

If we describe the location of charges in terms of a charge density ρ, we canconsider that each inﬁnitesimal volume dV contains a「point」charge ρ dV . Thesum over all charges is then the integral

Qint =

ρ dV.

(4.37)

volumeinside S

From our derivation you see that Gauss’ law follows from the fact that theexponent in Coulomb’s law is exactly two. A 1/r3 ﬁeld, or any 1/rn ﬁeld withn 6= 2, would not give Gauss’ law. So Gauss’ law is just an expression, ina diﬀerent form, of the Coulomb law of forces between two charges. In fact,working back from Gauss’ law, you can derive Coulomb’s law. The two are quiteequivalent so long as we keep in mind the rule that the forces between chargesare radial.

We would now like to write Gauss’ law in terms of derivatives. To do this, weapply Gauss’ law to an inﬁnitesimal cubical surface. We showed in Chapter 3that the ﬂux of E out of such a cube is ∇ · E times the volume dV of the cube.The charge inside of dV , by the deﬁnition of ρ, is equal to ρ dV , so Gauss’ lawgives

or

∇ · E dV = ρ dV0

,

∇ · E = ρ0

.

(4.38)

The diﬀerential form of Gauss’ law is the ﬁrst of our fundamental ﬁeld equationsof electrostatics, Eq. (4.5). We have now shown that the two equations ofelectrostatics, Eqs. (4.5) and (4.6), are equivalent to Coulomb’s law of force. Wewill now consider one example of the use of Gauss’ law. (We will come later tomany more examples.)

4-7 Field of a sphere of chargeOne of the diﬃcult problems we had when we studied the theory of gravi-tational attractions was to prove that the force produced by a solid sphere ofmatter was the same at the surface of the sphere as it would be if all the matterwere concentrated at the center. For many years Newton didn’t make publichis theory of gravitation, because he couldn’t be sure this theorem was true.We proved the theorem in Chapter 13 of Vol. I by doing the integral for thepotential and then ﬁnding the gravitational force by using the gradient. Now wecan prove the theorem in a most simple fashion. Only this time we will provethe corresponding theorem for a uniform sphere of electrical charge. (Since thelaws of electrostatics are the same as those of gravitation, the same proof couldbe done for the gravitational ﬁeld.)

We ask: What is the electric ﬁeld E at a point P anywhere outside the surfaceof a sphere ﬁlled with a uniform distribution of charge? Since there is no「special」direction, we can assume that E is everywhere directed away from the center ofthe sphere. We consider an imaginary surface that is spherical and concentricwith the sphere of charge, and that passes through the point P (Fig. 4-11). For

this surface, the ﬂux outward isZ

En da = E · 4πR2.

Gauss’ law tells us that this ﬂux is equal to the total charge Q of the sphere(over 0):

E · 4πR2 = Q0

,

4-10

Fig. 4-11. Using Gauss’ law to ﬁnd the

ﬁeld of a uniform sphere of charge.

Fig. 4-12. Field lines and equipotential surfaces for a positive point charge.

or

E = 14π0

QR2 ,

(4.39)

which is the same formula we would have for a point charge Q. We have provedNewton’s problem more easily than by doing the integral. It is, of course, a falsekind of easiness—it has taken you some time to be able to understand Gauss’law, so you may think that no time has really been saved. But after you haveused the theorem more and more, it begins to pay. It is a question of eﬃciency.

4-8 Field lines; equipotential surfacesWe would like now to give a geometrical description of the electrostatic ﬁeld.The two laws of electrostatics, one that the ﬂux is proportional to the chargeinside and the other that the electric ﬁeld is the gradient of a potential, can alsobe represented geometrically. We illustrate this with two examples.

First, we take the ﬁeld of a point charge. We draw lines in the direction ofthe ﬁeld—lines which are always tangent to the ﬁeld, as in Fig. 4-12. These arecalled ﬁeld lines. The lines show everywhere the direction of the electric vector.But we also wish to represent the magnitude of the vector. We can make therule that the strength of the electric ﬁeld will be represented by the「density」ofthe lines. By the density of the lines we mean the number of lines per unit areathrough a surface perpendicular to the lines. With these two rules we can havea picture of the electric ﬁeld. For a point charge, the density of the lines mustdecrease as 1/r2. But the area of a spherical surface perpendicular to the linesat any radius r increases as r2, so if we always keep the same number of linesfor all distances from the charge, the density will remain in proportion to themagnitude of the ﬁeld. We can guarantee that there are the same number oflines at every distance if we insist that the lines be continuous—that once a lineis started from the charge, it never stops. In terms of the ﬁeld lines, Gauss’ lawsays that lines should start only at plus charges and stop at minus charges. Thenumber which leave a charge q must be equal to q/0.

4-11

Fig. 4-13. Field lines and equipotentials for two equal and opposite point charges.

Now, we can ﬁnd a similar geometrical picture for the potential φ. The easiestway to represent the potential is to draw surfaces on which φ is a constant. Wecall them equipotential surfaces—surfaces of equal potential. Now what is thegeometrical relationship of the equipotential surfaces to the ﬁeld lines? Theelectric ﬁeld is the gradient of the potential. The gradient is in the directionof the most rapid change of the potential, and is therefore perpendicular to anequipotential surface. If E were not perpendicular to the surface, it would havea component in the surface. The potential would be changing in the surface, butthen it wouldn’t be an equipotential. The equipotential surfaces must then beeverywhere at right angles to the electric ﬁeld lines.

For a point charge all by itself, the equipotential surfaces are spheres centeredat the charge. We have shown in Fig. 4-12 the intersection of these spheres witha plane through the charge.

As a second example, we consider the ﬁeld near two equal charges, a positiveone and a negative one. To get the ﬁeld is easy. The ﬁeld is the superposition ofthe ﬁelds from each of the two charges. So, we can take two pictures like Fig. 4-12and superimpose them—impossible! Then we would have ﬁeld lines crossing eachother, and that’s not possible, because E can’t have two directions at the samepoint. The disadvantage of the ﬁeld-line picture is now evident. By geometricalarguments it is impossible to analyze in a very simple way where the new linesgo. From the two independent pictures, we can’t get the combined picture. Theprinciple of superposition, a simple and deep principle about electric ﬁelds, doesnot have, in the ﬁeld-line picture, an easy representation.

The ﬁeld-line picture has its uses, however, so we might still like to drawthe picture for a pair of equal (and opposite) charges. If we calculate the ﬁeldsfrom Eq. (4.13) and the potentials from (4.24), we can draw the ﬁeld lines andequipotentials. Figure 4-13 shows the result. But we ﬁrst had to solve theproblem mathematically!

4-12

A Note about Units

Quantity

FQLWρ ∼ Q/L31/0 ∼ F L2/Q2E ∼ F/Qφ ∼ W/QE ∼ φ/L1/0 ∼ EL2/Q

Unit

newtoncoulombmeterjoulecoulomb/meter3newton·meter2/coulomb2newton/coulombjoule/coulomb = voltvolt/metervolt·meter/coulomb

5

Application of Gauss’ Law