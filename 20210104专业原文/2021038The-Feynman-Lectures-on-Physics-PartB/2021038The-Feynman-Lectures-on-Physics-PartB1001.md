# 1001

10-1 The dielectric constantHere

we begin to discuss another of the peculiar properties of matter underthe inﬂuence of the electric ﬁeld. In an earlier chapter we considered the behaviorof conductors, in which the charges move freely in response to an electric ﬁeldto such points that there is no ﬁeld left inside a conductor. Now we will discussinsulators, materials which do not conduct electricity. One might at ﬁrst believethat there should be no eﬀect whatsoever. However, using a simple electroscopeand a parallel-plate capacitor, Faraday discovered that this was not so. Hisexperiments showed that the capacitance of such a capacitor is increased whenan insulator is put between the plates. If the insulator completely ﬁlls the spacebetween the plates, the capacitance is increased by a factor κ which dependsonly on the nature of the insulating material. Insulating materials are also calleddielectrics; the factor κ is then a property of the dielectric, and is called thedielectric constant. The dielectric constant of a vacuum is, of course, unity.Our problem now is to explain why there is any electrical eﬀect if the insu-lators are indeed insulators and do not conduct electricity. We begin with theexperimental fact that the capacitance is increased and try to reason out whatmight be going on. Consider a parallel-plate capacitor with some charges onthe surfaces of the conductors, let us say negative charge on the top plate andpositive charge on the bottom plate. Suppose that the spacing between the platesis d and the area of each plate is A. As we have proved earlier, the capacitance is

and the charge and voltage on the capacitor are related by

C = 0Ad

,

Q = CV.

(10.1)

(10.2)

Now the experimental fact is that if we put a piece of insulating material likelucite or glass between the plates, we ﬁnd that the capacitance is larger. Thatmeans, of course, that the voltage is lower for the same charge. But the voltagediﬀerence is the integral of the electric ﬁeld across the capacitor; so we mustconclude that inside the capacitor, the electric ﬁeld is reduced even though thecharges on the plates remain unchanged.

Fig. 10-1. A parallel-plate capacitor with

a dielectric. The lines of E are shown.

Now how can that be? We have a law due to Gauss that tells us that theﬂux of the electric ﬁeld is directly related to the enclosed charge. Consider thegaussian surface S shown by broken lines in Fig. 10-1. Since the electric ﬁeld isreduced with the dielectric present, we conclude that the net charge inside the10-1

surface must be lower than it would be without the material. There is only onepossible conclusion, and that is that there must be positive charges on the surfaceof the dielectric. Since the ﬁeld is reduced but is not zero, we would expect thispositive charge to be smaller than the negative charge on the conductor. So thephenomena can be explained if we could understand in some way that when adielectric material is placed in an electric ﬁeld there is positive charge inducedon one surface and negative charge induced on the other.

Fig. 10-2. If we put a conducting platein the gap of a parallel-plate condenser, theinduced charges reduce the ﬁeld in the con-ductor to zero.

We would expect that to happen for a conductor. For example, suppose thatwe had a capacitor with a plate spacing d, and we put between the plates aneutral conductor whose thickness is b, as in Fig. 10-2. The electric ﬁeld inducesa positive charge on the upper surface and a negative charge on the lower surface,so there is no ﬁeld inside the conductor. The ﬁeld in the rest of the space is thesame as it was without the conductor, because it is the surface density of chargedivided by 0; but the distance over which we have to integrate to get the voltage(the potential diﬀerence) is reduced. The voltage is

V = σ0

(d − b).

The resulting equation for the capacitance is like Eq. (10.1), with (d − b) substi-tuted for d:

(10.3)

C =

0A

d[1 − (b/d)] .

The capacitance is increased by a factor which depends upon (b/d), the proportionof the volume which is occupied by the conductor.This gives us an obvious model for what happens with dielectrics—that insidethe material there are many little sheets of conducting material. The troublewith such a model is that it has a speciﬁc axis, the normal to the sheets, whereasmost dielectrics have no such axis. However, this diﬃculty can be eliminated if weassume that all insulating materials contain small conducting spheres separatedfrom each other by insulation, as shown in Fig. 10-3. The phenomenon of thedielectric constant is explained by the eﬀect of the charges which would be inducedon each sphere. This is one of the earliest physical models of dielectrics used toexplain the phenomenon that Faraday observed. More speciﬁcally, it was assumedthat each of the atoms of a material was a perfect conductor, but insulated fromthe others. The dielectric constant κ would depend on the proportion of spacewhich was occupied by the conducting spheres. This is not, however, the modelthat is used today.

10-2 The polarization vector PIf we follow the above analysis further, we discover that the idea of regions ofperfect conductivity and insulation is not essential. Each of the small spheresacts like a dipole, the moment of which is induced by the external ﬁeld. The onlything that is essential to the understanding of dielectrics is that there are manylittle dipoles induced in the material. Whether the dipoles are induced becausethere are tiny conducting spheres or for any other reason is irrelevant.

10-2

Fig. 10-3. A model of a dielectric: smallconducting spheres embedded in an idealizedinsulator.

Why should a ﬁeld induce a dipole moment in an atom if the atom is nota conducting sphere? This subject will be discussed in much greater detail inthe next chapter, which will be about the inner workings of dielectric materials.However, we give here one example to illustrate a possible mechanism. An atomhas a positive charge on the nucleus, which is surrounded by negative electrons.In an electric ﬁeld, the nucleus will be attracted in one direction and the electronsin the other. The orbits or wave patterns of the electrons (or whatever pictureis used in quantum mechanics) will be distorted to some extent, as shown inFig. 10-4; the center of gravity of the negative charge will be displaced and willno longer coincide with the positive charge of the nucleus. We have alreadydiscussed such distributions of charge. If we look from a distance, such a neutralconﬁguration is equivalent, to a ﬁrst approximation, to a little dipole.

It seems reasonable that if the ﬁeld is not too enormous, the amount of induceddipole moment will be proportional to the ﬁeld. That is, a small ﬁeld will displacethe charges a little bit and a larger ﬁeld will displace them further—and inproportion to the ﬁeld—unless the displacement gets too large. For the remainderof this chapter, it will be supposed that the dipole moment is exactly proportionalto the ﬁeld.

We will now assume that in each atom there are charges q separated by adistance δ, so that qδ is the dipole moment per atom. (We use δ because we arealready using d for the plate separation.) If there are N atoms per unit volume,there will be a dipole moment per unit volume equal to N qδ. This dipole momentper unit volume will be represented by a vector, P . Needless to say, it is in thedirection of the individual dipole moments, i.e., in the direction of the chargeseparation δ:

(10.4)In general, P will vary from place to place in the dielectric. However, at anypoint in the material, P is proportional to the electric ﬁeld E. The constant ofproportionality, which depends on the ease with which the electron are displaced,will depend on the kinds of atoms in the material.

P = N qδ.

Fig. 10-4. An atom in an electric ﬁeldhas its distribution of electrons displacedwith respect to the nucleus.

What actually determines how this constant of proportionality behaves, howaccurately it is constant for very large ﬁelds, and what is going on inside diﬀerentmaterials, we will discuss at a later time. For the present, we will simply supposethat there exists a mechanism by which a dipole moment is induced which isproportional to the electric ﬁeld.

10-3 Polarization chargesNow let us see what this model gives for the theory of a condenser with adielectric. First consider a sheet of material in which there is a certain dipolemoment per unit volume. Will there be on the average any charge densityproduced by this? Not if P is uniform. If the positive and negative charges beingdisplaced relative to each other have the same average density, the fact that theyare displaced does not produce any net charge inside the volume. On the otherhand, if P were larger at one place and smaller at another, that would meanthat more charge would be moved into some region than away from it; we wouldthen expect to get a volume density of charge. For the parallel-plate condenser,we suppose that P is uniform, so we need to look only at what happens at thesurfaces. At one surface the negative charges, the electrons, have eﬀectivelymoved out a distance δ; at the other surface they have moved in, leaving somepositive charge eﬀectively out a distance δ. As shown in Fig. 10-5, we will have asurface density of charge, which will be called the surface polarization charge.

Fig. 10-5. A dielectric slab in a uniformﬁeld. The positive charges displaced thedistance δ with respect to the negatives.

10-3

This charge can be calculated as follows. If A is the area of the plate, thenumber of electrons that appear at the surface is the product of A and N, thenumber per unit volume, and the displacement δ, which we assume here isperpendicular to the surface. The total charge is obtained by multiplying by theelectronic charge qe. To get the surface density of the polarization charge inducedon the surface, we divide by A. The magnitude of the surface charge density is

σpol = N qeδ.

σpol = P.

But this is just equal to the magnitude P of the polarization vector P , Eq. (10.4):(10.5)The surface density of charge is equal to the polarization inside the material. Thesurface charge is, of course, positive on one surface and negative on the other.

Now let us assume that our slab is the dielectric of a parallel-plate capacitor.The plates of the capacitor also have a surface charge, which we will call σfree,because they can move「freely」anywhere on the conductor. This is, of course, thecharge that we put on when we charged the capacitor. It should be emphasizedthat σpol exists only because of σfree. If σfree is removed by discharging thecapacitor, then σpol will disappear, not by going out on the discharging wire, butby moving back into the material—by the relaxation of the polarization insidethe material.

We can now apply Gauss’ law to the gaussian surface S in Fig. 10-1. Theelectric ﬁeld E in the dielectric is equal to the total surface charge density dividedby 0. It is clear that σpol and σfree have opposite signs, so

E = σfree − σpol

0

.

(10.6)

Note that the ﬁeld E0 between the metal plate and the surface of the dielectricis higher than the ﬁeld E; it corresponds to σfree alone. But here we are concernedwith the ﬁeld inside the dielectric which, if the dielectric nearly ﬁlls the gap, isthe ﬁeld over nearly the whole volume. Using Eq. (10.5), we can write

E = σfree − P

0

.

(10.7)

This equation doesn’t tell us what the electric ﬁeld is unless we know what Pis. Here, however, we are assuming that P depends on E—in fact, that it isproportional to E. This proportionality is usually written as

(10.8)The constant χ (Greek「khi」) is called the electric susceptibility of the dielectric.

P = χ0E.

Then Eq. (10.7) becomes

E = σfree0

1

(1 + χ) ,

(10.9)

which gives us the factor 1/(1 + χ) by which the ﬁeld is reduced.The voltage between the plates is the integral of the electric ﬁeld. Since theﬁeld is uniform, the integral is just the product of E and the plate separation d.We have that

V = Ed = σfreed

0(1 + χ) .

The total charge on the capacitor is σfreeA, so that the capacitance deﬁned

by (10.2) becomes

(10.10)We have explained the observed facts. When a parallel-plate capacitor is

= κ0A

d

d

.

C = 0A(1 + χ)

ﬁlled with a dielectric, the capacitance is increased by the factor

κ = 1 + χ,

(10.11)10-4

which is a property of the material. Our explanation, of course, is not completeuntil we have explained—as we will do later—how the atomic polarization comesabout.

Let’s now consider something a little bit more complicated—the situationin which the polarization P is not everywhere the same. As mentioned earlier,if the polarization is not constant, we would expect in general to ﬁnd a chargedensity in the volume, because more charge might come into one side of a smallvolume element than leaves it on the other. How can we ﬁnd out how muchcharge is gained or lost from a small volume?

First let’s compute how much charge moves across any imaginary surfacewhen the material is polarized. The amount of charge that goes across a surfaceis just P times the surface area if the polarization is normal to the surface. Ofcourse, if the polarization is tangential to the surface, no charge moves across it.Following the same arguments we have already used, it is easy to see thatthe charge moved across any surface element is proportional to the componentof P perpendicular to the surface. Compare Fig. 10-6 with Fig. 10-5. We seethat Eq. (10.5) should, in the general case, be written

σpol = P · n.

(10.12)

If we are thinking of an imagined surface element inside the dielectric,Eq. (10.12) gives the charge moved across the surface but doesn’t result ina net surface charge, because there are equal and opposite contributions fromthe dielectric on the two sides of the surface.

The displacements of the charges can, however, result in a volume chargedensity. The total charge displaced out of any volume V by the polarizationis the integral of the outward normal component of P over the surface S thatbounds the volume (see Fig. 10-7). An equal excess charge of the opposite signis left behind. Denoting the net charge inside V by ∆Qpol we write

∆Qpol = −

P · n da.

(10.13)

We can attribute ∆Qpol to a volume distribution of charge with the density ρpol,and so

Combining the two equations yields

∆Qpol =

ρpol dV = −

ρpol dV.

Z

S

P · n da.

(10.14)

(10.15)

Z

S

Z

V

Z

Z

V

Z

We have a kind of Gauss’ theorem that relates the charge density from polarizedmaterials to the polarization vector P . We can see that it agrees with theresult we got for the surface polarization charge or the dielectric in a parallel-plate capacitor. Using Eq. (10.15) with the gaussian surface of Fig. 10-1, thesurface integral gives P ∆A, and the charge inside is σpol ∆A, so we get againthat σpol = P.Just as we did for Gauss’ law of electrostatics, we can convert Eq. (10.15) toa diﬀerential form—using Gauss’ mathematical theorem:

P · n da =

∇ · P dV.

We get

S

V

ρpol = −∇ · P .

(10.16)

If there is a nonuniform polarization, its divergence gives the net density of chargeappearing in the material. We emphasize that this is a perfectly real chargedensity; we call it「polarization charge」only to remind ourselves how it got there.10-5

Fig. 10-6. The charge moved across anelement of an imaginary surface in a dielec-tric is proportional to the component of Pnormal to the surface.

Fig. 10-7. A nonuniform polarization Pcan result in a net charge in the body of adielectric.

10-4 The electrostatic equations with dielectricsNow let’s combine the above result with our theory of electrostatics. The

fundamental equation is

∇ · E = ρ0

(10.17)The ρ here is the density of all electric charges. Since it is not easy to keep trackof the polarization charges, it is convenient to separate ρ into two parts. Againwe call ρpol the charges due to nonuniform polarizations, and call ρfree all therest. Usually ρfree is the charge we put on conductors, or at known places inspace. Equation (10.17) then becomes

.

or

= ρfree − ∇ · P∇ · E = ρfree + ρpol(cid:19)

(cid:18)

0

0

= ρfree0

.

∇ ·

E + P0

Of course, the equation for the curl of E is unchanged:

∇ × E = 0.

Taking P from Eq. (10.8), we get the simpler equation

∇ · [(1 + χ)E] = ∇ · (κE) = ρfree0

.

(10.18)

(10.19)

(10.20)

These are the equations of electrostatics when there are dielectrics. They don’t,of course, say anything new, but they are in a form which is more convenient forcomputation in cases where ρfree is known and the polarization P is proportionalto E.Notice that we have not taken the dielectric「constant,」κ, out of the divergence.That is because it may not be the same everywhere. If it has everywhere the samevalue, it can be factored out and the equations are just those of electrostatics withthe charge density ρfree divided by κ. In the form we have given, the equationsapply to the general case where diﬀerent dielectrics may be in diﬀerent places inthe ﬁeld. Then the equations may be quite diﬃcult to solve.

There is a matter of some historical importance which should be mentionedhere. In the early days of electricity, the atomic mechanism of polarization wasnot known and the existence of ρpol was not appreciated. The charge ρfree wasconsidered to be the entire charge density. In order to write Maxwell’s equationsin a simple form, a new vector D was deﬁned to be equal to a linear combinationof E and P :(10.21)As a result, Eqs. (10.18) and (10.19) were written in an apparently very simpleform:

D = 0E + P .

(10.22)Can one solve these? Only if a third equation is given for the relationship betweenD and E. When Eq. (10.8) holds, this relationship isD = 0(1 + χ)E = κ0E.

∇ · D = ρfree,

∇ × E = 0.

(10.23)

This equation was usually written

D = E,

(10.24)where  is still another constant for describing the dielectric property of materials.It is called the「permittivity.」(Now you see why we have 0 in our equations, itis the「permittivity of empty space.」) Evidently, = κ0 = (1 + χ)0.

(10.25)10-6

Today we look upon these matters from another point of view, namely, thatwe have simpler equations in a vacuum, and if we exhibit in every case all thecharges, whatever their origin, the equations are always correct. If we separatesome of the charges away for convenience, or because we do not want to discusswhat is going on in detail, then we can, if we wish, write our equations in anyother form that may be convenient.

One more point should be emphasized. An equation like D = E is anattempt to describe a property of matter. But matter is extremely complicated,and such an equation is in fact not correct. For instance, if E gets too large,then D is no longer proportional to E. For some substances, the proportionalitybreaks down even with relatively small ﬁelds. Also, the「constant」of propor-tionality may depend on how fast E changes with time. Therefore this kind ofequation is a kind of approximation, like Hooke’s law. It cannot be a deep andfundamental equation. On the other hand, our fundamental equations for E,(10.17) and (10.19), represent our deepest and most complete understanding ofelectrostatics.

10-5 Fields and forces with dielectricsWe will now prove some rather general theorems for electrostatics in situationswhere dielectrics are present. We have seen that the capacitance of a parallel-platecapacitor is increased by a deﬁnite factor if it is ﬁlled with a dielectric. We canshow that this is true for a capacitor of any shape, provided the entire region inthe neighborhood of the two conductors is ﬁlled with a uniform linear dielectric.Without the dielectric, the equations to be solved are

∇ · E0 = ρfree0

and

∇ × E0 = 0.

With the dielectric present, the ﬁrst of these equations is modiﬁed; we haveinstead the equations

∇ · (κE) = ρfree0

and

∇ × E = 0.

(10.26)

Now since we are taking κ to be everywhere the same, the last two equationscan be written as

∇ · (κE) = ρfree0

and

∇ × (κE) = 0.

(10.27)

We therefore have the same equations for κE as for E0, so they have thesolution κE = E0.In other words, the ﬁeld is everywhere smaller, by thefactor 1/κ, than in the case without the dielectric. Since the voltage diﬀerence isa line integral of the ﬁeld, the voltage is reduced by this same factor. Since thecharge on the electrodes of the capacitor has been taken the same in both cases,Eq. (10.2) tells us that the capacitance, in the case of an everywhere uniformdielectric, is increased by the factor κ.Let us now ask what the force would be between two charged conductorsin a dielectric. We consider a liquid dielectric that is homogeneous everywhere.We have seen earlier that one way to obtain the force is to diﬀerentiate theenergy with respect to the appropriate distance. If the conductors have equal andopposite charges, the energy U = Q2/2C, where C is their capacitance. Usingthe principle of virtual work, any component is given by a diﬀerentiation; forexample,

(cid:18) 1

(cid:19)

C

Fx = − ∂U∂x

= − Q22

∂∂x

.

(10.28)

Since the dielectric increases the capacity by a factor κ, all forces will be reducedby this same factor.One point should be emphasized. What we have said is true only if thedielectric is a liquid. Any motion of conductors that are embedded in a solid10-7

dielectric changes the mechanical stress conditions of the dielectric and alters itselectrical properties, as well as causing some mechanical energy change in thedielectric. Moving the conductors in a liquid does not change the liquid. Theliquid moves to a new place but its electrical characteristics are not changed.

Many older books on electricity start with the「fundamental」law that the

force between two charges is

F = q1q2

4π0κr2 ,

(10.29)

a point of view which is thoroughly unsatisfactory. For one thing, it is not truein general; it is true only for a world ﬁlled with a liquid. Secondly, it dependson the fact that κ is a constant, which is only approximately true for most realmaterials. It is much better to start with Coulomb’s law for charges in a vacuum,which is always right (for stationary charges).What does happen in a solid? This is a very diﬃcult problem which has notbeen solved, because it is, in a sense, indeterminate. If you put charges insidea dielectric solid, there are many kinds of pressures and strains. You cannotdeal with virtual work without including also the mechanical energy required tocompress the solid, and it is a diﬃcult matter, generally speaking, to make aunique distinction between the electrical forces and the mechanical forces dueto the solid material itself. Fortunately, no one ever really needs to know theanswer to the question proposed. He may sometimes want to know how muchstrain there is going to be in a solid, and that can be worked out. But it is muchmore complicated than the simple result we got for liquids.

A surprisingly complicated problem in the theory of dielectrics is the following:Why does a charged object pick up little pieces of dielectric? If you comb yourhair on a dry day, the comb readily picks up small scraps of paper. If you thoughtcasually about it, you probably assumed the comb had one charge on it and thepaper had the opposite charge on it. But the paper is initially electrically neutral.It hasn’t any net charge, but it is attracted anyway. It is true that sometimes thepaper will come up to the comb and then ﬂy away, repelled immediately afterit touches the comb. The reason is, of course, that when the paper touches thecomb, it picks up some negative charges and then the like charges repel. Butthat doesn’t answer the original question. Why did the paper come toward thecomb in the ﬁrst place?

The answer has to do with the polarization of a dielectric when it is placedin an electric ﬁeld. There are polarization charges of both signs, which areattracted and repelled by the comb. There is a net attraction, however, becausethe ﬁeld nearer the comb is stronger than the ﬁeld farther away—the comb isnot an inﬁnite sheet. Its charge is localized. A neutral piece of paper will not beattracted to either plate inside the parallel plates of a capacitor. The variationof the ﬁeld is an essential part of the attraction mechanism.

As illustrated in Fig. 10-8, a dielectric is always drawn from a region of weakﬁeld toward a region of stronger ﬁeld. In fact, one can prove that for smallobjects the force is proportional to the gradient of the square of the electricﬁeld. Why does it depend on the square of the ﬁeld? Because the inducedpolarization charges are proportional to the ﬁelds, and for given charges theforces are proportional to the ﬁeld. However, as we have just indicated, there willbe a net force only if the square of the ﬁeld is changing from point to point. Sothe force is proportional to the gradient of the square of the ﬁeld. The constantof proportionality involves, among other things, the dielectric constant of theobject, and it also depends upon the size and shape of the object.

There is a related problem in which the force on a dielectric can be workedout quite accurately.If we have a parallel-plate capacitor with a dielectricslab only partially inserted, as shown in Fig. 10-9, there will be a force drivingthe sheet in. A detailed examination of the force is quite complicated; it isrelated to nonuniformities in the ﬁeld near the edges of the dielectric and theplates. However, if we do not look at the details, but merely use the principle ofconservation of energy, we can easily calculate the force. We can ﬁnd the force10-8

Fig. 10-8. A dielectric object in a nonuni-form ﬁeld feels a force toward regions ofhigher ﬁeld strength.

Fig. 10-9. The force on a dielectric sheetin a parallel-plate capacitor can be com-puted by applying the principle of energyconservation.

from the formula we derived earlier. Equation (10.28) is equivalent to

Fx = − ∂U∂x

= + V 22

∂C∂x

.

(10.30)

We need only ﬁnd out how the capacitance varies with the position of the dielectricslab.

Let’s suppose that the total length of the plates is L, that the width of theplates is W, that the plate separation and dielectric thickness are d, and thatthe distance to which the dielectric has been inserted is x. The capacitance isthe ratio of the total free charge on the plates to the voltage between the plates.We have seen above that for a given voltage V the surface charge density of freecharge is κ0V /d. So the total charge on the plates is

Q = κ0Vd

xW + 0Vd

(L − x)W,

from which we get the capacitance:

Using (10.30), we have

C = 0Wd

(κx + L − x).

Fx = V 22

0W

d

(κ − 1).

(10.31)

(10.32)

Now this equation is not particularly useful for anything unless you happen toneed to know the force in such circumstances. We only wished to show thatthe theory of energy can often be used to avoid enormous complications indetermining the forces on dielectric materials—as there would be in the presentcase.

Our discussion of the theory of dielectrics has dealt only with electricalphenomena, accepting the fact that the material has a polarization which isproportional to the electric ﬁeld. Why there is such a proportionality is perhapsof greater interest to physics. Once we understand the origin of the dielectricconstants from an atomic point of view, we can use electrical measurements ofthe dielectric constants in varying circumstances to obtain detailed informationabout atomic or molecular structure. This aspect will be treated in part in thenext chapter.

10-9




