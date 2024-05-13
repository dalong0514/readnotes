## 0201. Differential Calculus of Vector Fields

2-1 Understanding physics

2-2 Scalar and vector ﬁelds—T

and h

gradient

2-3 Derivatives of ﬁelds—the2-4 The operator ∇2-5 Operations with ∇2-6 The diﬀerential equation of heat

ﬂow

2-7 Second derivatives of vector ﬁelds2-8 Pitfalls

Review: Chapter 11, Vol. I, Vectors

2

Differential Calculus of Vector Fields

2-1 Understanding physicsThe

physicist needs a facility in looking at problems from several points ofview. The exact analysis of real physical problems is usually quite complicated,and any particular physical situation may be too complicated to analyze directlyby solving the diﬀerential equation. But one can still get a very good idea ofthe behavior of a system if one has some feel for the character of the solutionin diﬀerent circumstances. Ideas such as the ﬁeld lines, capacitance, resistance,and inductance are, for such purposes, very useful. So we will spend much of ourtime analyzing them. In this way we will get a feel as to what should happen indiﬀerent electromagnetic situations. On the other hand, none of the heuristicmodels, such as ﬁeld lines, is really adequate and accurate for all situations.There is only one precise way of presenting the laws, and that is by means ofdiﬀerential equations. They have the advantage of being fundamental and, sofar as we know, precise. If you have learned the diﬀerential equations you canalways go back to them. There is nothing to unlearn.

It will take you some time to understand what should happen in diﬀerentcircumstances. You will have to solve the equations. Each time you solvethe equations, you will learn something about the character of the solutions.To keep these solutions in mind, it will be useful also to study their meaningin terms of ﬁeld lines and of other concepts. This is the way you will really「understand」the equations. That is the diﬀerence between mathematics andphysics. Mathematicians, or people who have very mathematical minds, are oftenled astray when「studying」physics because they lose sight of the physics. Theysay:「Look, these diﬀerential equations—the Maxwell equations—are all there isto electrodynamics; it is admitted by the physicists that there is nothing which isnot contained in the equations. The equations are complicated, but after all theyare only mathematical equations and if I understand them mathematically insideout, I will understand the physics inside out.」Only it doesn’t work that way.Mathematicians who study physics with that point of view—and there have beenmany of them—usually make little contribution to physics and, in fact, little tomathematics. They fail because the actual physical situations in the real worldare so complicated that it is necessary to have a much broader understanding ofthe equations.

What it means really to understand an equation—that is, in more than astrictly mathematical sense—was described by Dirac. He said:「I understandwhat an equation means if I have a way of ﬁguring out the characteristics of itssolution without actually solving it.」So if we have a way of knowing what shouldhappen in given circumstances without actually solving the equations, thenwe「understand」the equations, as applied to these circumstances. A physicalunderstanding is a completely unmathematical, imprecise, and inexact thing, butabsolutely necessary for a physicist.

Ordinarily, a course like this is given by developing gradually the physicalideas—by starting with simple situations and going on to more and more compli-cated situations. This requires that you continuously forget things you previouslylearned—things that are true in certain situations, but which are not true ingeneral. For example, the「law」that the electrical force depends on the squareof the distance is not always true. We prefer the opposite approach. We preferto take ﬁrst the complete laws, and then to step back and apply them to simple2-1

situations, developing the physical ideas as we go along. And that is what weare going to do.

Our approach is completely opposite to the historical approach in which onedevelops the subject in terms of the experiments by which the information wasobtained. But the subject of physics has been developed over the past 200 yearsby some very ingenious people, and as we have only a limited time to acquireour knowledge, we cannot possibly cover everything they did. Unfortunatelyone of the things that we shall have a tendency to lose in these lectures is thehistorical, experimental development. It is hoped that in the laboratory some ofthis lack can be corrected. You can also ﬁll in what we must leave out by readingthe Encyclopedia Britannica, which has excellent historical articles on electricityand on other parts of physics. You will also ﬁnd historical information in manytextbooks on electricity and magnetism.

2-2 Scalar and vector ﬁelds—T and hWe begin now with the abstract, mathematical view of the theory of electricityand magnetism. The ultimate idea is to explain the meaning of the laws given inChapter 1. But to do this we must ﬁrst explain a new and peculiar notation thatwe want to use. So let us forget electromagnetism for the moment and discussthe mathematics of vector ﬁelds. It is of very great importance, not only forelectromagnetism, but for all kinds of physical circumstances. Just as ordinarydiﬀerential and integral calculus is so important to all branches of physics, soalso is the diﬀerential calculus of vectors. We turn to that subject.

Listed below are a few facts from the algebra of vectors. It is assumed that

you already know them.

A · B = scalar = AxBx + AyBy + AzBzA × B = vector

(A × B)z = AxBy − AyBx(A × B)x = AyBz − Az By(A × B)y = Az Bx − AxBz

A × A = 0A · (A × B) = 0A · (B × C) = (A × B) · CA × (B × C) = B(A · C) − C(A · B)

Also we will want to use the two following equalities from the calculus:

∆f(x, y, z) = ∂f∂x∂2f∂x ∂y

∆x + ∂f∂y= ∂2f∂y ∂x

.

∆y + ∂f∂z

∆z,

(2.1)(2.2)

(2.3)(2.4)(2.5)(2.6)

(2.7)

(2.8)

The ﬁrst equation (2.7) is, of course, true only in the limit that ∆x, ∆y, and ∆zgo toward zero.The simplest possible physical ﬁeld is a scalar ﬁeld. By a ﬁeld, you remember,we mean a quantity which depends upon position in space. By a scalar ﬁeld wemerely mean a ﬁeld which is characterized at each point by a single number—ascalar. Of course the number may change in time, but we need not worry aboutthat for the moment. We will talk about what the ﬁeld looks like at a giveninstant. As an example of a scalar ﬁeld, consider a solid block of material whichhas been heated at some places and cooled at others, so that the temperature ofthe body varies from point to point in a complicated way. Then the temperaturewill be a function of x, y, and z, the position in space measured in a rectangularcoordinate system. Temperature is a scalar ﬁeld.

2-2

Fig. 2-1. Temperature T is an example of a scalarﬁeld. With each point (x, y , z ) in space there is asso-ciated a number T (x, y , z ). All points on the surfacemarked T = 20◦ (shown as a curve at z = 0) are at thesame temperature. The arrows are samples of the heatﬂow vector h.

One way of thinking about scalar ﬁelds is to imagine「contours」which areimaginary surfaces drawn through all points for which the ﬁeld has the samevalue, just as contour lines on a map connect points with the same height. Fora temperature ﬁeld the contours are called「isothermal surfaces」or isotherms.Figure 2-1 illustrates a temperature ﬁeld and shows the dependence of T on xand y when z = 0. Several isotherms are drawn.

There are also vector ﬁelds. The idea is very simple. A vector is given for eachpoint in space. The vector varies from point to point. As an example, consider arotating body. The velocity of the material of the body at any point is a vectorwhich is a function of position (Fig. 2-2). As a second example, consider the ﬂowof heat in a block of material. If the temperature in the block is high at oneplace and low at another, there will be a ﬂow of heat from the hotter places tothe colder. The heat will be ﬂowing in diﬀerent directions in diﬀerent parts ofthe block. The heat ﬂow is a directional quantity which we call h. Its magnitudeis a measure of how much heat is ﬂowing. Examples of the heat ﬂow vector arealso shown in Fig. 2-1.

Fig. 2-2. The velocity of the atoms ina rotating object is an example of a vectorﬁeld.

Fig. 2-3. Heat ﬂow is a vector ﬁeld. The vector hpoints along the direction of the ﬂow. Its magnitude isthe energy transported per unit time across a surfaceelement oriented perpendicular to the ﬂow, divided bythe area of the surface element.

Let’s make a more precise deﬁnition of h: The magnitude of the vector heatﬂow at a point is the amount of thermal energy that passes, per unit time andper unit area, through an inﬁnitesimal surface element at right angles to thedirection of ﬂow. The vector points in the direction of ﬂow (see Fig. 2-3). Insymbols: If ∆J is the thermal energy that passes per unit time through thesurface element ∆a, then

where ef is a unit vector in the direction of ﬂow.The vector h can be deﬁned in another way—in terms of its components. Weask how much heat ﬂows through a small surface at any angle with respect to the2-3

h = ∆J∆a

ef ,

(2.9)

ﬂow. In Fig. 2-4 we show a small surface ∆a2 inclined with respect to ∆a1, whichis perpendicular to the ﬂow. The unit vector n is normal to the surface ∆a2. Theangle θ between n and h is the same as the angle between the surfaces (since his normal to ∆a1). Now what is the heat ﬂow per unit area through ∆a2? Theﬂow through ∆a2 is the same as through ∆a1; only the areas are diﬀerent. Infact, ∆a1 = ∆a2 cos θ. The heat ﬂow through ∆a2 iscos θ = h · n.

(2.10)

∆J∆a2

= ∆J∆a1

We interpret this equation: the heat ﬂow (per unit time and per unit area) throughany surface element whose unit normal is n, is given by h · n. Equally, we couldsay: the component of the heat ﬂow perpendicular to the surface element ∆a2is h · n. We can, if we wish, consider that these statements deﬁne h. We will beapplying the same ideas to other vector ﬁelds.

Fig. 2-4. The heat ﬂow through ∆a2 is

the same as through ∆a1.

2-3 Derivatives of ﬁelds—the gradientWhen ﬁelds vary in time, we can describe the variation by giving theirderivatives with respect to t. We want to describe the variations with positionin a similar way, because we are interested in the relationship between, say, thetemperature in one place and the temperature at a nearby place. How shallwe take the derivative of the temperature with respect to position? Do wediﬀerentiate the temperature with respect to x? Or with respect to y, or z?Useful physical laws do not depend upon the orientation of the coordinatesystem. They should, therefore, be written in a form in which either both sidesare scalars or both sides are vectors. What is the derivative of a scalar ﬁeld,say ∂T /∂x? Is it a scalar, or a vector, or what? It is neither a scalar nor avector, as you can easily appreciate, because if we took a diﬀerent x-axis, ∂T /∂xwould certainly be diﬀerent. But notice: We have three possible derivatives:∂T /∂x, ∂T /∂y, and ∂T /∂z. Since there are three kinds of derivatives and weknow that it takes three numbers to form a vector, perhaps these three derivativesare the components of a vector:

(2.11)

(cid:18) ∂T

∂x

(cid:19) ?= a vector.

,

∂T∂y

,

∂T∂z

Of course it is not generally true that any three numbers form a vector. It istrue only if, when we rotate the coordinate system, the components of the vectortransform among themselves in the correct way. So it is necessary to analyzehow these derivatives are changed by a rotation of the coordinate system. Weshall show that (2.11) is indeed a vector. The derivatives do transform in thecorrect way when the coordinate system is rotated.

We can see this in several ways. One way is to ask a question whose answeris independent of the coordinate system, and try to express the answer in an「invariant」form. For instance, if S = A · B, and if A and B are vectors, weknow—because we proved it in Chapter 11 of Vol. I—that S is a scalar. Weknow that S is a scalar without investigating whether it changes with changes incoordinate systems. It can’t, because it’s a dot product of two vectors. Similarly,if we have three numbers B1, B2, and B3 and we ﬁnd out that for every vector A(2.12)where S is the same for any coordinate system, then it must be that the threenumbers B1, B2, B3 are the components Bx, By, Bz of some vector B.Now let’s think of the temperature ﬁeld. Suppose we take two points P1and P2, separated by the small interval ∆R. The temperature at P1 is T1 andat P2 is T2, and the diﬀerence ∆T = T2 − T1. The temperatures at these real,physical points certainly do not depend on what axis we choose for measuringthe coordinates. In particular, ∆T is a number independent of the coordinatesystem. It is a scalar.

AxB1 + AyB2 + AzB3 = S,

2-4

If we choose some convenient set of axes, we could write T1 = T(x, y, z) andT2 = T(x + ∆x, y + ∆y, z + ∆z), where ∆x, ∆y, and ∆z are the components ofthe vector ∆R (Fig. 2-5). Remembering Eq. (2.7), we can write

∆T = ∂T∂x

∆x + ∂T∂y

∆y + ∂T∂z

∆z.

(2.13)

The left side of Eq. (2.13) is a scalar. The right side is the sum of three productswith ∆x, ∆y, and ∆z, which are the components of a vector. It follows that thethree numbers

∂T∂x

,

∂T∂y

,

∂T∂z

are also the x-, y-, and z-components of a vector. We write this new vectorwith the symbol ∇T. The symbol ∇ (called「del」) is an upside-down ∆, andis supposed to remind us of diﬀerentiation. People read ∇T in various ways:「del-T,」or「gradient of T,」or「grad T;」*

(cid:18) ∂T

∂x

(cid:19)

grad T = ∇T =

,

∂T∂y

,

∂T∂z

.

(2.14)

Fig. 2-5. The vector ∆R, whose compo-

nents are ∆x, ∆y, and ∆z.

Using this notation, we can rewrite Eq. (2.13) in the more compact form

∆T = ∇T · ∆R.

(2.15)

In words, this equation says that the diﬀerence in temperature between twonearby points is the dot product of the gradient of T and the vector displacementbetween the points. The form of Eq. (2.15) also illustrates clearly our proof abovethat ∇T is indeed a vector.Perhaps you are still not convinced? Let’s prove it in a diﬀerent way. (Al-though if you look carefully, you may be able to see that it’s really the same proofin a longer-winded form!) We shall show that the components of ∇T transformin just the same way that components of R do. If they do, ∇T is a vectoraccording to our original deﬁnition of a vector in Chapter 11 of Vol. I. We take anew coordinate system x0, y0, z0, and in this new system we calculate ∂T /∂x0,∂T /∂y0, and ∂T /∂z0. To make things a little simpler, we let z = z0, so that wecan forget about the z-coordinate. (You can check out the more general case foryourself.)We take an x0y0-system rotated an angle θ with respect to the xy-system, as

in Fig. 2-6(a). For a point (x, y) the coordinates in the prime system are

x0 = x cos θ + y sin θ,y0 = −x sin θ + y cos θ.

(2.16)(2.17)

Or, solving for x and y,

x = x0 cos θ − y0 sin θ,y = x0 sin θ + y0 cos θ.

(2.18)(2.19)If any pair of numbers transforms with these equations in the same way that xand y do, they are the components of a vector.Now let’s look at the diﬀerence in temperature between the two nearby pointsP1 and P2, chosen as in Fig. 2-6(b). If we calculate with the x- and y-coordinates,we would write

—since ∆y is zero.

∆T = ∂T∂x

∆x

(2.20)

Fig. 2-6. (a) Transformation to a rotatedcoordinate system. (b) Special case of aninterval ∆R parallel to the x-axis.

* In our notation, the expression (a, b, c) represents a vector with components a, b, and c. If

you like to use the unit vectors i, j, and k, you may write

∇T = i

∂T∂x

+ j

∂T∂y

+ k

∂T∂z

.

2-5

What would a computation in the prime system give? We would have written

∆T = ∂T

∂x0 ∆x0 + ∂T

∂y0 ∆y0.

Looking at Fig. 2-6(b), we see that

∆x0 = ∆x cos θ

and

(2.23)since ∆y0 is negative when ∆x is positive. Substituting these in Eq. (2.21), weﬁnd that

∆y0 = −∆x sin θ,

∆T = ∂T

∂x0 ∆x cos θ − ∂T(cid:18) ∂T∂x0 cos θ − ∂TComparing Eq. (2.25) with (2.20), we see that∂x0 cos θ − ∂T= ∂T

∂T∂x

=

(cid:19)∂y0 ∆x sin θ∂y0 sin θ∆x.

∂y0 sin θ.

This equation says that ∂T /∂x is obtained from ∂T /∂x0 and ∂T /∂y0, just as xis obtained from x0 and y0 in Eq. (2.18). So ∂T /∂x is the x-component of avector. The same kind of arguments would show that ∂T /∂y and ∂T /∂z are y-and z-components. So ∇T is deﬁnitely a vector. It is a vector ﬁeld derived fromthe scalar ﬁeld T.

2-4 The operator ∇Now we can do something that is extremely amusing and ingenious—andcharacteristic of the things that make mathematics beautiful. The argumentthat grad T, or ∇T, is a vector did not depend upon what scalar ﬁeld we werediﬀerentiating. All the arguments would go the same if T were replaced by anyscalar ﬁeld. Since the transformation equations are the same no matter whatwe diﬀerentiate, we could just as well omit the T and replace Eq. (2.26) by theoperator equation

(2.21)

(2.22)

(2.24)

(2.25)

(2.26)

(2.27)

(2.28)

(2.29)

We leave the operators, as Jeans said,「hungry for something to diﬀerentiate.」Since the diﬀerential operators themselves transform as the components of avector should, we can call them components of a vector operator. We can write

∂∂x

∂x0 cos θ − ∂= ∂(cid:18) ∂

∂y0 sin θ.(cid:19)

∇ =

,

∂x

∂∂y

,

∂∂z

,

which means, of course,

∇x = ∂∂x

, ∇y = ∂∂y

, ∇z = ∂∂z

.

We have abstracted the gradient away from the T—that is the wonderful idea.You must always remember, of course, that ∇ is an operator. Alone, it meansnothing. If ∇ by itself means nothing, what does it mean if we multiply it by ascalar—say T—to get the product T∇? (One can always multiply a vector by ascalar.) It still does not mean anything. Its x-component is

which is not a number, but is still some kind of operator. However, according tothe algebra of vectors we would still call T∇ a vector.

T

∂∂x

,

(2.30)

2-6

Now let’s multiply ∇ by a scalar on the other side, so that we have the

product (∇T). In ordinary algebra

T A = AT,

(2.31)but we have to remember that operator algebra is a little diﬀerent from ordinaryvector algebra. With operators we must always keep the sequence right, so thatthe operations make proper sense. You will have no diﬃculty if you just rememberthat the operator ∇ obeys the same convention as the derivative notation. What isto be diﬀerentiated must be placed on the right of the ∇. The order is important.Keeping in mind this problem of order, we understand that T∇ is an operator,but the product ∇T is no longer a hungry operator; the operator is completelysatisﬁed. It is indeed a physical vector having a meaning. It represents thespatial rate of change of T. The x-component of ∇T is how fast T changes inthe x-direction. What is the direction of the vector ∇T? We know that the rateof change of T in any direction is the component of ∇T in that direction (seeEq. 2.15). It follows that the direction of ∇T is that in which it has the largestpossible component—in other words, the direction in which T changes the fastest.The gradient of T has the direction of the steepest uphill slope (in T).

2-5 Operations with ∇Can we do any other algebra with the vector operator ∇? Let us try combiningit with a vector. We can combine two vectors by making a dot product. Wecould make the products

(a vector) · ∇,

or

∇ · (a vector).

The ﬁrst one doesn’t mean anything yet, because it is still an operator. Whatit might ultimately mean would depend on what it is made to operate on. Thesecond product is some scalar ﬁeld. (A · B is always a scalar.)Let’s try the dot product of ∇ with a vector ﬁeld we know, say h. We writeout the components:(2.32)

∇ · h = ∇xhx + ∇yhy + ∇zhz

or

∇ · h = ∂hx∂x

+ ∂hy∂y

+ ∂hz∂z

.

(2.33)

The sum is invariant under a coordinate transformation. If we were to choose adiﬀerent system (indicated by primes), we would have*∂y0 + ∂hz0∂z0 ,

∂x0 + ∂hy0

∇0 · h = ∂hx0

(2.34)

which is the same number as would be gotten from Eq. (2.33), even though itlooks diﬀerent. That is,(2.35)for every point in space. So ∇ · h is a scalar ﬁeld, which must represent somephysical quantity. You should realize that the combination of derivatives in ∇· his rather special. There are all sorts of other combinations like ∂hy/∂x, whichare neither scalars nor components of vectors.The scalar quantity ∇ · (a vector) is extremely useful in physics. It has been

∇0 · h = ∇ · h

given the name the divergence. For example,

(2.36)As we did for ∇T, we can ascribe a physical signiﬁcance to ∇ · h. We shall,however, postpone that until later.

∇ · h = div h =「divergence of h.」

* We think of h as a physical quantity that depends on position in space, and not strictlyas a mathematical function of three variables. When h is「diﬀerentiated」with respect tox, y, and z, or with respect to x0, y0, and z0, the mathematical expression for h must ﬁrst beexpressed as a function of the appropriate variables.

2-7

First, we wish to see what else we can cook up with the vector operator ∇.

What about a cross product? We must expect that

(2.37)It is a vector whose components we can write by the usual rule for cross products(see Eq. 2.2):

∇ × h = a vector.

(∇ × h)z = ∇xhy − ∇yhx = ∂hy∂x

− ∂hx∂y

.

(∇ × h)x = ∇yhz − ∇z hy = ∂hz∂y

− ∂hy∂z

(2.38)

(2.39)

Similarly,

and

(∇ × h)y = ∇z hx − ∇xhz = ∂hx∂z

(2.40)The combination ∇ × h is called「the curl of h.」The reason for the nameSummarizing, we have three kinds of combinations with ∇:

and the physical meaning of the combination will be discussed later.

− ∂hz∂x

.

∇T= grad T = a vector,∇ · h = div h = a scalar,∇ × h = curl h = a vector.

Using these combinations, we can write about the spatial variations of ﬁelds ina convenient way—in a way that is general, in that it doesn’t depend on anyparticular set of axes.As an example of the use of our vector diﬀerential operator ∇, we write a setof vector equations which contain the same laws of electromagnetism that wegave in words in Chapter 1. They are called Maxwell’s equations.

Maxwell’s Equations

∇ · E = ρ0∇ × E = − ∂B∂t∇ · B = 0

(2.41)

(1)

(2)(3)

(4)

c2 ∇ × B = ∂E∂t

+ j0

where ρ (rho), the「electric charge density,」is the amount of charge per unitvolume, and j, the「electric current density,」is the rate at which charge ﬂowsthrough a unit area per second. These four equations contain the completeclassical theory of the electromagnetic ﬁeld. You see what an elegantly simpleform we can get with our new notation!

2-6 The diﬀerential equation of heat ﬂowLet us give another example of a law of physics written in vector notation. Thelaw is not a precise one, but for many metals and a number of other substances thatconduct heat it is quite accurate. You know that if you take a slab of material andheat one face to temperature T2 and cool the other to a diﬀerent temperature T1the heat will ﬂow through the material from T2 to T1 [Fig. 2-7(a)]. The heat ﬂowis proportional to the area A of the faces, and to the temperature diﬀerence. Itis also inversely proportional to d, the distance between the plates. (For a giventemperature diﬀerence, the thinner the slab the greater the heat ﬂow.) Letting Jbe the thermal energy that passes per unit time through the slab, we write

The constant of proportionality κ (kappa) is called the thermal conductivity.

J = κ(T2 − T1) Ad

.

(2.42)

Fig. 2-7. (a) Heat ﬂow through a slab.(b) An inﬁnitesimal slab parallel to anisothermal surface in a large block.

2-8

What will happen in a more complicated case? Say in an odd-shaped block ofmaterial in which the temperature varies in peculiar ways? Suppose we look at atiny piece of the block and imagine a slab like that of Fig. 2-7(a) on a miniaturescale. We orient the faces parallel to the isothermal surfaces, as in Fig. 2-7(b),so that Eq. (2.42) is correct for the small slab.

If the area of the small slab is ∆A, the heat ﬂow per unit time is

∆J = κ ∆T

∆A∆s

,

(2.43)

where ∆s is the thickness of the slab. Now ∆J/∆A we have deﬁned earlier asthe magnitude of h, whose direction is the heat ﬂow. The heat ﬂow will be fromT1 + ∆T toward T1 and so it will be perpendicular to the isotherms, as drawnin Fig. 2-7(b). Also, ∆T /∆s is just the rate of change of T with position. Andsince the position change is perpendicular to the isotherms, our ∆T /∆s is themaximum rate of change. It is, therefore, just the magnitude of ∇T. Now sincethe direction of ∇T is opposite to that of h, we can write (2.43) as a vectorequation:(2.44)(The minus sign is necessary because heat ﬂows「downhill」in temperature.)Equation (2.44) is the diﬀerential equation of heat conduction in bulk materials.You see that it is a proper vector equation. Each side is a vector if κ is just anumber. It is the generalization to arbitrary cases of the special relation (2.42) forrectangular slabs. Later we should learn to write all sorts of elementary physicsrelations like (2.42) in the more sophisticated vector notation. This notation isuseful not only because it makes the equations look simpler. It also shows mostclearly the physical content of the equations without reference to any arbitrarilychosen coordinate system.

h = −κ∇T.

2-7 Second derivatives of vector ﬁeldsSo far we have had only ﬁrst derivatives. Why not second derivatives? We

could have several combinations:

(a) ∇ · (∇T)(b) ∇ × (∇T)(c) ∇(∇ · h)(d) ∇ · (∇ × h)(e) ∇ × (∇ × h)

(2.45)

You can check that these are all the possible combinations.

Let’s look ﬁrst at the second one, (b). It has the same form as

A × (AT) = (A × A)T = 0,

since A × A is always zero. So we should have

(2.46)We can see how this equation comes about if we go through once with thecomponents:

curl(grad T) = ∇ × (∇T) = 0.

[∇ × (∇T)]z = ∇x(∇T)y − ∇y(∇T)x

(cid:18) ∂T

(cid:19)

∂y

= ∂∂x

(cid:18) ∂T

(cid:19)

∂x

− ∂∂y

,

(2.47)

It goes the same for the other components. Sowhich is zero (by Eq. 2.8).∇× (∇T) = 0, for any temperature distribution—in fact, for any scalar function.Now let us take another example. Let us see whether we can ﬁnd anotherzero. The dot product of a vector with a cross product which contains that vectoris zero:

A · (A × B) = 0,

(2.48)2-9

because A×B is perpendicular to A, and so has no components in the direction A.The same combination appears in (d) of (2.45), so we have

∇ · (∇ × h) = div(curl h) = 0.

(2.49)

Again, it is easy to show that it is zero by carrying through the operations withcomponents.

Now we are going to state two mathematical theorems that we will not prove.

They are very interesting and useful theorems for physicists to know.

In a physical problem we frequently ﬁnd that the curl of some quantity—sayof the vector ﬁeld A—is zero. Now we have seen (Eq. 2.46) that the curl of agradient is zero, which is easy to remember because of the way the vectors work.It could certainly be, then, that A is the gradient of some quantity, because thenits curl would necessarily be zero. The interesting theorem is that if the curl Ais zero, then A is always the gradient of something—there is some scalar ﬁeld ψ(psi) such that A is equal to grad ψ. In other words, we have the

Theorem:

∇ × A = 0

Ifthere is aψsuch that A = ∇ψ.

(2.50)

There is a similar theorem if the divergence of A is zero. We have seen inEq. (2.49) that the divergence of a curl of something is always zero. If you comeacross a vector ﬁeld D for which div D is zero, then you can conclude that D isthe curl of some vector ﬁeld C.

Theorem:

∇ · D = 0

Ifthere is asuch that D = ∇ × C.

C

(2.51)In looking at the possible combinations of two ∇ operators, we have foundthat two of them always give zero. Now we look at the ones that are not zero.Take the combination ∇ · (∇T), which was ﬁrst on our list. It is not, in general,zero. We write out the components:

Then

∇T = i∇xT + j∇yT + k∇zT.

∇ · (∇T) = ∇x(∇xT) + ∇y(∇yT) + ∇z(∇zT)

= ∂2T∂x2

+ ∂2T∂y2

+ ∂2T∂z2 ,

(2.52)

which would, in general, come out to be some number. It is a scalar ﬁeld.

You see that we do not need to keep the parentheses, but can write, without

any chance of confusion,

∇ · (∇T) = ∇ · ∇T = (∇ · ∇)T = ∇2T.

(2.53)We look at ∇2 as a new operator. It is a scalar operator. Because it appearsoften in physics, it has been given a special name—the Laplacian.

Laplacian = ∇2 = ∂2∂x2

+ ∂2∂y2

+ ∂2∂z2 .

(2.54)

Since the Laplacian is a scalar operator, we may operate with it on a vector—bywhich we mean the same operation on each component in rectangular coordinates:

∇2h = (∇2hx,∇2hy,∇2hz).

2-10

Let’s look at one more possibility: ∇ × (∇ × h), which was (e) in thelist (2.45). Now the curl of the curl can be written diﬀerently if we use the vectorequality (2.6):

A × (B × C) = B(A · C) − C(A · B).

(2.55)In order to use this formula, we should replace A and B by the operator ∇ andput C = h. If we do that, we get

∇ × (∇ × h) = ∇(∇ · h) − h(∇ · ∇) . . . ???

Wait a minute! Something is wrong. The ﬁrst two terms are vectors all right (theoperators are satisﬁed), but the last term doesn’t come out to anything. It’s stillan operator. The trouble is that we haven’t been careful enough about keepingthe order of our terms straight. If you look again at Eq. (2.55), however, you seethat we could equally well have written it as

A × (B × C) = B(A · C) − (A · B)C.

(2.56)

The order of terms looks better. Now let’s make our substitution in (2.56). Weget

(2.57)This form looks all right. It is, in fact, correct, as you can verify by computingthe components. The last term is the Laplacian, so we can equally well write

∇ × (∇ × h) = ∇(∇ · h) − (∇ · ∇)h.

∇ × (∇ × h) = ∇(∇ · h) − ∇2h.

(2.58)

We have had something to say about all of the combinations in our list ofdouble ∇’s, except for (c), ∇(∇ · h). It is a possible vector ﬁeld, but there isnothing special to say about it. It’s just some vector ﬁeld which may occasionallycome up.

It will be convenient to have a table of our conclusions:(a) ∇ · (∇T) = ∇2T = a scalar ﬁeld(b) ∇ × (∇T) = 0(c) ∇(∇ · h) = a vector ﬁeld(d) ∇ · (∇ × h) = 0(e) ∇ × (∇ × h) = ∇(∇ · h) − ∇2h(∇ · ∇)h = ∇2h = a vector ﬁeld(f)

(2.59)

You may notice that we haven’t tried to invent a new vector operator (∇ × ∇).Do you see why?

2-8 PitfallsWe have been applying our knowledge of ordinary vector algebra to the algebraof the operator ∇. We have to be careful, though, because it is possible to goastray. There are two pitfalls which we will mention, although they will notcome up in this course. What would you say about the following expression, thatinvolves the two scalar functions ψ and φ (phi):(∇ψ) × (∇φ)?

You might want to say: it must be zero because it’s just like

(Aa) × (Ab),

which is zero because the cross product of two equal vectors A× A is always zero.But in our example the two operators ∇ are not equal! The ﬁrst one operateson one function, ψ; the other operates on a diﬀerent function, φ. So althoughwe represent them by the same symbol ∇, they must be considered as diﬀerent2-11

operators. Clearly, the direction of ∇ψ depends on the function ψ, so it is notlikely to be parallel to ∇φ:

(∇ψ) × (∇φ) 6= 0

(generally).

Fortunately, we won’t have to use such expressions. (What we have said doesn’tchange the fact that ∇ × ∇ψ = 0 for any scalar ﬁeld, because here both ∇’soperate on the same function.)Pitfall number two (which, again, we need not get into in our course) is thefollowing: The rules that we have outlined here are simple and nice when weuse rectangular coordinates. For example, if we have ∇2h and we want thex-component, it is

(cid:18) ∂2

∂x2

(∇2h)x =

(cid:19)

+ ∂2∂y2

+ ∂2∂z2

hx = ∇2hx.

(2.60)

The same expression would not work if we were to ask for the radial componentof ∇2h. The radial component of ∇2h is not equal to ∇2hr. The reason is thatwhen we are dealing with the algebra of vectors, the directions of the vectors areall quite deﬁnite. But when we are dealing with vector ﬁelds, their directionsare diﬀerent at diﬀerent places. If we try to describe a vector ﬁeld in, say, polarcoordinates, what we call the「radial」direction varies from point to point. Sowe can get into a lot of trouble when we start to diﬀerentiate the components.For example, even for a constant vector ﬁeld, the radial component changes frompoint to point.It is usually safest and simplest just to stick to rectangular coordinatesand avoid trouble, but there is one exception worth mentioning: Since theLaplacian ∇2, is a scalar, we can write it in any coordinate system we want to(for example, in polar coordinates). But since it is a diﬀerential operator, weshould use it only on vectors whose components are in a ﬁxed direction—thatmeans rectangular coordinates. So we shall express all of our vector ﬁelds interms of their x-, y-, and z-components when we write our vector diﬀerentialequations out in components.

2-12
