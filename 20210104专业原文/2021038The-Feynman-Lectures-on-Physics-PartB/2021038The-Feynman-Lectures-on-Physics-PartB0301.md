## 0301. Vector Integral Calculus

3-1 Vector integrals; the line integral of ∇ψWe

found in Chapter 2 that there were various ways of taking derivatives ofﬁelds. Some gave vector ﬁelds; some gave scalar ﬁelds. Although we developedmany diﬀerent formulas, everything in Chapter 2 could be summarized in onerule: the operators ∂/∂x, ∂/∂y, and ∂/∂z are the three components of a vectoroperator ∇. We would now like to get some understanding of the signiﬁcanceof the derivatives of ﬁelds. We will then have a better feeling for what a vectorﬁeld equation means.We have already discussed the meaning of the gradient operation (∇ on ascalar). Now we turn to the meanings of the divergence and curl operations. Theinterpretation of these quantities is best done in terms of certain vector integralsand equations relating such integrals. These equations cannot, unfortunately, beobtained from vector algebra by some easy substitution, so you will just have tolearn them as something new. Of these integral formulas, one is practically trivial,but the other two are not. We will derive them and explain their implications.The equations we shall study are really mathematical theorems. They will beuseful not only for interpreting the meaning and the content of the divergence andthe curl, but also in working out general physical theories. These mathematicaltheorems are, for the theory of ﬁelds, what the theorem of the conservation ofenergy is to the mechanics of particles. General theorems like these are importantfor a deeper understanding of physics. You will ﬁnd, though, that they are notvery useful for solving problems—except in the simplest cases. It is delightful,however, that in the beginning of our subject there will be many simple problemswhich can be solved with the three integral formulas we are going to treat. Wewill see, however, as the problems get harder, that we can no longer use thesesimple methods.

We take up ﬁrst an integral formula involving the gradient. The relationcontains a very simple idea: Since the gradient represents the rate of change of aﬁeld quantity, if we integrate that rate of change, we should get the total change.Suppose we have the scalar ﬁeld ψ(x, y, z). At any two points (1) and (2), thefunction ψ will have the values ψ(1) and ψ(2), respectively. [We use a convenientnotation, in which (2) represents the point (x2, y2, z2) and ψ(2) means the samething as ψ(x2, y2, z2).] If Γ (gamma) is any curve joining (1) and (2), as in Fig. 3-1,the following relation is true:

3-1 Vector integrals; the line integral

3-2 The ﬂux of a vector ﬁeld3-3 The ﬂux from a cube; Gauss’

3-4 Heat conduction; the diﬀusion

of ∇ψ

theorem

equation

3-5 The circulation of a vector ﬁeld3-6 The circulation around a square;

Stokes’ theorem

3-7 Curl-free and divergence-free

ﬁelds

3-8 Summary

Theorem 1.

ψ(2) − ψ(1) =

(∇ψ) · ds .

(3.1)

Fig. 3-1. The terms used in Eq. (3.1).The vector ∇ψ is evaluated at the line ele-ments ds.

Z (2)

(1)

along Γ

The integral is a line integral, from (1) to (2) along the curve Γ, of the dot productof ∇ψ—a vector—with ds—another vector which is an inﬁnitesimal line elementof the curve Γ (directed away from (1) and toward (2)).First, we should review what we mean by a line integral. Consider a scalarfunction f(x, y, z), and the curve Γ joining two points (1) and (2). We mark oﬀthe curve at a number of points and join these points by straight-line segments,as shown in Fig. 3-2. Each segment has the length ∆si, where i is an index that

runs 1, 2, 3, . . . By the line integralZ (2)

f ds

Fig. 3-2. The line integral is the limit of

(1)

along Γ

a sum.

3-1

we mean the limit of the sum X

fi∆si,

i

where fi is the value of the function at the ith segment. The limiting value iswhat the sum approaches as we add more and more segments (in a sensible way,so that the largest ∆si → 0).The integral in our theorem, Eq. (3.1), means the same thing, although itlooks a little diﬀerent. Instead of f, we have another scalar—the componentof ∇ψ in the direction of ∆s. If we write (∇ψ)t for this tangential component,it is clear that(3.2)

(∇ψ)t ∆s = (∇ψ) · ∆s.

Now let’s see why Eq. (3.1) is true.

The integral in Eq. (3.1) means the sum of such terms.In Chapter 2, we showed that thecomponent of ∇ψ along a small displacement ∆R was the rate of change of ψin the direction of ∆R. Consider the line segment ∆s from (1) to point a inFig. 3-2. According to our deﬁnition,

∆ψ1 = ψ(a) − ψ(1) = (∇ψ)1 · ∆s1.

(3.3)

Also, we have

ψ(b) − ψ(a) = (∇ψ)2 · ∆s2,

(3.4)where, of course, (∇ψ)1 means the gradient evaluated at the segment ∆s1,and (∇ψ)2, the gradient evaluated at ∆s2. If we add Eqs. (3.3) and (3.4), we get(3.5)

ψ(b) − ψ(1) = (∇ψ)1 · ∆s1 + (∇ψ)2 · ∆s2.

You can see that if we keep adding such terms, we get the result

ψ(2) − ψ(1) =X

(∇ψ)i · ∆si.

i

(3.6)

The left-hand side doesn’t depend on how we choose our intervals—if (1) and (2)are kept always the same—so we can take the limit of the right-hand side. Wehave therefore proved Eq. (3.1).

You can see from our proof that just as the equality doesn’t depend on howthe points a b, c, . . . , are chosen, similarly it doesn’t depend on what we choosefor the curve Γ to join (1) and (2). Our theorem is correct for any curve from (1)to (2).One remark on notation: You will see that there is no confusion if we write,

for convenience,

(∇ψ) · ds = ∇ψ · ds.

With this notation, our theorem is

Theorem 1.

ψ(2) − ψ(1) =

Z (2)

(1)

any curve from

(1) to (2)

∇ψ · ds .

(3.7)

(3.8)

3-2 The ﬂux of a vector ﬁeldBefore we consider our next integral theorem—a theorem about the divergence—we would like to study a certain idea which has an easily understood physicalsigniﬁcance in the case of heat ﬂow. We have deﬁned the vector h, which representsthe heat that ﬂows through a unit area in a unit time. Suppose that inside ablock of material we have some closed surface S which encloses the volume V(Fig. 3-3). We would like to ﬁnd out how much heat is ﬂowing out of this volume.We can, of course, ﬁnd it by calculating the total heat ﬂow out of the surface S.We write da for the area of an element of the surface. The symbol stands fora two-dimensional diﬀerential. If, for instance, the area happened to be in thexy-plane we would have

da = dx dy.

3-2

Fig. 3-3. The closed surface S deﬁnesthe volume V . The unit vector n is theoutward normal to the surface element da,and h is the heat-ﬂow vector at the surfaceelement.

Later we shall have integrals over volume and for these it is convenient to considera diﬀerential volume that is a little cube. So when we write dV we mean

dV = dx dy dz.

Some people like to write d2a instead of da to remind themselves that it iskind of a second-order quantity. They would also write d3V instead of dV . Wewill use the simpler notation, and assume that you can remember that an areahas two dimensions and a volume has three.

The heat ﬂow out through the surface element da is the area times thecomponent of h perpendicular to da. We have already deﬁned n as a unit vectorpointing outward at right angles to the surface (Fig. 3-3). The component of hthat we want is(3.9)

hn = h · n.

The heat ﬂow out through da is then

h · n da.

(3.10)

To get the total heat ﬂow through any surface we sum the contributions from allthe elements of the surface. In other words, we integrate (3.10) over the wholesurface:

Total heat ﬂow outward through S =

h · n da.

(3.11)

We are also going to call this surface integral「the ﬂux of h through thesurface.」Originally the word ﬂux meant ﬂow, so that the surface integral justmeans the ﬂow of h through the surface. We may think: h is the「current density」of heat ﬂow and the surface integral of it is the total heat current directed out ofthe surface; that is, the thermal energy per unit time (joules per second).

We would like to generalize this idea to the case where the vector does notrepresent the ﬂow of anything; for instance, it might be the electric ﬁeld. We cancertainly still integrate the normal component of the electric ﬁeld over an area ifwe wish. Although it is not the ﬂow of anything, we still call it the「ﬂux.」We say

Flux of E through the surface S =

E · n da.

(3.12)

Z

S

Z

S

Z

S

We generalize the word「ﬂux」to mean the「surface integral of the normalcomponent」of a vector. We will also use the same deﬁnition even when thesurface considered is not a closed one, as it is here.

Returning to the special case of heat ﬂow, let us take a situation in whichheat is conserved. For example, imagine some material in which after an initialheating no further heat energy is generated or absorbed. Then, if there is a netheat ﬂow out of a closed surface, the heat content of the volume inside mustdecrease. So, in circumstances in which heat would be conserved, we say that

h · n da = − dQdt

,

(3.13)

where Q is the heat inside the surface. The heat ﬂux out of S is equal to minusthe rate of change with respect to time of the total heat Q inside of S. Thisinterpretation is possible because we are speaking of heat ﬂow and also becausewe supposed that the heat was conserved. We could not, of course, speak of thetotal heat inside the volume if heat were being generated there.

Now we shall point out an interesting fact about the ﬂux of any vector. Youmay think of the heat ﬂow vector if you wish, but what we say will be true forany vector ﬁeld C. Imagine that we have a closed surface S that encloses thevolume V . We now separate the volume into two parts by some kind of a「cut,」as in Fig. 3-4. Now we have two closed surfaces and volumes. The volume V1 isenclosed in the surface S1, which is made up of part of the original surface Sa andof the surface of the cut, Sab. The volume V2 is enclosed by S2, which is made up3-3

Fig. 3-4. A volume V contained inside the surface Sis divided into two pieces by a「cut」at the surface Sab.We now have the volume V1 enclosed in the surfaceS1 = Sa + Sab and the volume V2 enclosed in the surfaceS2 = Sb + Sab.

of the rest of the original surface Sb and closed oﬀ by the cut Sab. Now considerthe following question: Suppose we calculate the ﬂux out through surface S1 andadd to it the ﬂux through surface S2. Does the sum equal the ﬂux through thewhole surface that we started with? The answer is yes. The ﬂux through thepart of the surfaces Sab common to both S1 and S2 just exactly cancels out. Forthe ﬂux of the vector C out of V1 we can writeC · n da +

Flux through S1 =

C · n1 da,

(3.14)

Sa

Sab

ZZ

ZZ

and for the ﬂux out of V2,

Flux through S2 =

C · n da +

C · n2 da.

(3.15)

Sb

Sab

Note that in the second integral we have written n1 for the outward normalfor Sab when it belongs to S1, and n2 when it belongs to S2, as shown in Fig. 3-4.

Clearly, n1 = −n2, so thatZ

Z

C · n1 da = −

C · n2 da.

(3.16)

Sab

Sab

If we now add Eqs. (3.14) and (3.15), we see that the sum of the ﬂuxes throughS1 and S2 is just the sum of two integrals which, taken together, give the ﬂuxthrough the original surface S = Sa + Sb.We see that the ﬂux through the complete outer surface S can be consideredas the sum of the ﬂuxes from the two pieces into which the volume was broken.We can similarly subdivide again—say by cutting V1 into two pieces. You seethat the same arguments apply. So for any way of dividing the original volume,it must be generally true that the ﬂux through the outer surface, which is theoriginal integral, is equal to a sum of the ﬂuxes out of all the little interior pieces.

3-3 The ﬂux from a cube; Gauss’ theoremWe now take the special case of a small cube* and ﬁnd an interesting formulafor the ﬂux out of it. Consider a cube whose edges are lined up with the axesas in Fig. 3-5. Let us suppose that the coordinates of the corner nearest theorigin are x, y, z. Let ∆x be the length of the cube in the x-direction, ∆y bethe length in the y-direction, and ∆z be the length in the z-direction. We wishto ﬁnd the ﬂux of a vector ﬁeld C through the surface of the cube. We shall dothis by making a sum of the ﬂuxes through each of the six faces. First, considerthe face marked 1 in the ﬁgure. The ﬂux outward on this face is the negative ofthe x-component of C, integrated over the area of the face. This ﬂux is

Z

−

Cx dy dz.

* The following development applies equally well to any rectangular parallelepiped.

3-4

Fig. 3-5. Computation of the ﬂux of C

out of a small cube.

Since we are considering a small cube, we can approximate this integral by thevalue of Cx at the center of the face—which we call the point (1)—multiplied bythe area of the face, ∆y ∆z:

Flux out of 1 = −Cx(1) ∆y ∆z.

Similarly, for the ﬂux out of face 2, we write

Flux out of 2 = Cx(2) ∆y ∆z.

Now Cx(1) and Cx(2) are, in general, slightly diﬀerent. If ∆x is small enough,we can write

Cx(2) = Cx(1) + ∂Cx∂x

∆x.

(cid:20)

There are, of course, more terms, but they will involve (∆x)2 and higher powers,and so will be negligible if we consider only the limit of small ∆x. So the ﬂuxthrough face 2 is

Flux out of 2 =

Cx(1) + ∂Cx∂x

∆x

∆y ∆z.

Summing the ﬂuxes for faces 1 and 2, we get

Flux out of 1 and 2 = ∂Cx∂x

∆x ∆y ∆z.

The derivative should really be evaluated at the center of face 1; that is, at[x, y + (∆y/2), z + (∆z/2)]. But in the limit of an inﬁnitesimal cube, we make anegligible error if we evaluate it at the corner (x, y, z).

Applying the same reasoning to each of the other pairs of faces, we have

Flux out of 3 and 4 = ∂Cy∂y

∆x ∆y ∆z

and

Flux out of 5 and 6 = ∂Cz∂z

∆x ∆y ∆z.

The total ﬂux through all the faces is the sum of these terms. We ﬁnd that

Z

cube

(cid:18) ∂Cx

∂x

C · n da =

+ ∂Cy∂y

+ ∂Cz∂z

∆x ∆y ∆z,

and the sum of the derivatives is just ∇ · C. Also, ∆x ∆y ∆z = ∆V , the volumeof the cube. So we can say that for an inﬁnitesimal cube

(cid:21)

(cid:19)

C · n da = (∇ · C) ∆V.

(3.17)

Z

surface

We have shown that the outward ﬂux from the surface of an inﬁnitesimal cube isequal to the divergence of the vector multiplied by the volume of the cube. Wenow see the「meaning」of the divergence of a vector. The divergence of a vectorat the point P is the ﬂux—the outgoing「ﬂow」of C—per unit volume, in theneighborhood of P.We have connected the divergence of C to the ﬂux of C out of each inﬁnitesimalvolume. For any ﬁnite volume we can use the fact we proved above—that thetotal ﬂux from a volume is the sum of the ﬂuxes out of each part. We can, thatis, integrate the divergence over the entire volume. This gives us the theoremthat the integral of the normal component of any vector over any closed surfacecan also be written as the integral of the divergence of the vector over the volumeenclosed by the surface. This theorem is named after Gauss.

Gauss’ Theorem.

Z

S

Z

V

C · n da =

∇ · C dV,

where S is any closed surface and V is the volume inside it.

(3.18)

3-5

3-4 Heat conduction; the diﬀusion equationLet’s consider an example of the use of this theorem, just to get familiar withit. Suppose we take again the case of heat ﬂow in, say, a metal. Suppose wehave a simple situation in which all the heat has been previously put in and thebody is just cooling oﬀ. There are no sources of heat, so that heat is conserved.Then how much heat is there inside some chosen volume at any time? It mustbe decreasing by just the amount that ﬂows out of the surface of the volume. Ifour volume is a little cube, we would write, following Eq. (3.17),

Heat out =

h · n da = ∇ · h ∆V.

(3.19)

Z

But this must equal the rate of loss of the heat inside the cube. If q is the heatper unit volume, the heat in the cube is q ∆V , and the rate of loss is

cube

− ∂∂t

(q ∆V ) = − ∂q∂t

∆V.

Comparing (3.19) and (3.20), we see that

− ∂q∂t

= ∇ · h.

(3.20)

(3.21)

Take careful note of the form of this equation; the form appears often inphysics. It expresses a conservation law—here the conservation of heat. We haveexpressed the same physical fact in another way in Eq. (3.13). Here we have thediﬀerential form of a conservation equation, while Eq. (3.13) is the integral form.We have obtained Eq. (3.21) by applying Eq. (3.13) to an inﬁnitesimal cube.We can also go the other way. For a big volume V bounded by S, Gauss’ lawsays that

h · n da =

∇ · h dV.

(3.22)

Z

S

Z

V

Using (3.21), the integral on the right-hand side is found to be just −dQ/dt, andagain we have Eq. (3.13).Now let’s consider a diﬀerent case. Imagine that we have a block of materialand that inside it there is a very tiny hole in which some chemical reaction istaking place and generating heat. Or we could imagine that there are some wiresrunning into a tiny resistor that is being heated by an electric current. We shallsuppose that the heat is generated practically at a point, and let W representthe energy liberated per second at that point. We shall suppose that in the restof the volume heat is conserved, and that the heat generation has been going onfor a long time—so that now the temperature is no longer changing anywhere.The problem is: What does the heat vector h look like at various places in themetal? How much heat ﬂow is there at each point?

We know that if we integrate the normal component of h over a closed surfacethat encloses the source, we will always get W. All the heat that is beinggenerated at the point source must ﬂow out through the surface, since we havesupposed that the ﬂow is steady. We have the diﬃcult problem of ﬁnding a vectorﬁeld which, when integrated over any surface, always gives W. We can, however,ﬁnd the ﬁeld rather easily by taking a somewhat special surface. We take asphere of radius R, centered at the source, and assume that the heat ﬂow is radial(Fig. 3-6). Our intuition tells us that h should be radial if the block of materialis large and we don’t get too close to the edges, and it should also have the samemagnitude at all points on the sphere. You see that we are adding a certainamount of guesswork—usually called「physical intuition」—to our mathematicsin order to ﬁnd the answer.

When h is radial and spherically symmetric, the integral of the normalcomponent of h over the area is very simple, because the normal component3-6

Fig. 3-6. In the region near a point source

of heat, the heat ﬂow is radially outward.

is just the magnitude of h and is constant. The area over which we integrate

is 4πR2. We have then that Z

h · n da = h · 4πR2

(3.23)

(where h is the magnitude of h). This integral should equal W, the rate at whichheat is produced at the source. We get

S

or

h = W

4πR2 ,

h = W

4πR2 er,

(3.24)

where, as usual, er represents a unit vector in the radial direction. Our resultsays that h is proportional to W and varies inversely as the square of the distancefrom the source.The result we have just obtained applies to the heat ﬂow in the vicinity ofa point source of heat. Let’s now try to ﬁnd the equations that hold in themost general kind of heat ﬂow, keeping only the condition that heat is conserved.We will be dealing only with what happens at places outside of any sources orabsorbers of heat.

The diﬀerential equation for the conduction of heat was derived in Chapter 2.

According to Eq. (2.44),

h = −κ∇T.

(3.25)(Remember that this relationship is an approximate one, but fairly good forsome materials like metals.) It is applicable, of course, only in regions of thematerial where there is no generation or absorption of heat. We derived aboveanother relation, Eq. (3.21), that holds when heat is conserved. If we combinethat equation with (3.25), we get

or

− ∂q∂t

∂q∂t

= ∇ · h = −∇ · (κ∇T),

= κ∇ · ∇T = κ∇2T,

(3.26)

if κ is a constant. You remember that q is the amount of heat in a unit volumeand ∇ · ∇ = ∇2 is the Laplacian operator+ ∂2∂y2

∇2 = ∂2∂x2

+ ∂2∂z2 .

If we now make one more assumption we can obtain a very interesting equation.We assume that the temperature of the material is proportional to the heat contentper unit volume—that is, that the material has a deﬁnite speciﬁc heat. Whenthis assumption is valid (as it often is), we can write

or

∆q = cv ∆T

∂q∂t

= cv

∂T∂t

.

(3.27)

The rate of change of heat is proportional to the rate of change of temperature.The constant of proportionality cv is, here, the speciﬁc heat per unit volume ofthe material. Using Eq. (3.27) with (3.26), we get

∂T∂t

= κcv

∇2T.

(3.28)

We ﬁnd that the time rate of change of T—at every point—is proportional tothe Laplacian of T, which is the second derivative of its spatial dependence. Wehave a diﬀerential equation—in x, y, z, and t—for the temperature T.

3-7

The diﬀerential equation (3.28) is called the heat diﬀusion equation. It is

often written as

= D ∇2T,

(3.29)

∂T∂t

where D is called the diﬀusion constant, and is here equal to κ/cv.The diﬀusion equation appears in many physical problems—in the diﬀusion ofgases, in the diﬀusion of neutrons, and in others. We have already discussed thephysics of some of these phenomena in Chapter 43 of Vol. I. Now you have thecomplete equation that describes diﬀusion in the most general possible situation.At some later time we will take up ways of solving the diﬀusion equation to ﬁndhow the temperature varies in particular cases. We turn back now to considerother theorems about vector ﬁelds.

3-5 The circulation of a vector ﬁeldWe wish now to look at the curl in somewhat the same way we looked atthe divergence. We obtained Gauss’ theorem by considering the integral overa surface, although it was not obvious at the beginning that we were going tobe dealing with the divergence. How did we know that we were supposed tointegrate over a surface in order to get the divergence? It was not at all clearthat this would be the result. And so with an apparent equal lack of justiﬁcation,we shall calculate something else about a vector and show that it is related tothe curl. This time we calculate what is called the circulation of a vector ﬁeld.If C is any vector ﬁeld, we take its component along a curved line and take theintegral of this component all the way around a complete loop. The integralis called the circulation of the vector ﬁeld around the loop. We have alreadyconsidered a line integral of ∇ψ earlier in this chapter. Now we do the samekind of thing for any vector ﬁeld C.Let Γ be any closed loop in space—imaginary, of course. An example is givenin Fig. 3-7. The line integral of the tangential component of C around the loopis written as

Ct ds =

C · ds.

(3.30)

I

Γ

I

Γ

You should note that the integral is taken all the way around, not from one pointto another as we did before. The little circle on the integral sign is to remindus that the integral is to be taken all the way around. This integral is calledthe circulation of the vector ﬁeld around the curve Γ. The name came originallyfrom considering the circulation of a liquid. But the name—like ﬂux—has beenextended to apply to any ﬁeld even when there is no material「circulating.」

Playing the same kind of game we did with the ﬂux, we can show that thecirculation around a loop is the sum of the circulations around two partial loops.Suppose we break up our curve of Fig. 3-7 into two loops, by joining two points(1) and (2) on the original curve by some line that cuts across as shown in Fig. 3-8.There are now two loops, Γ1 and Γ2. Γ1 is made up of Γa, which is that part ofthe original curve to the left of (1) and (2), plus Γab, the「short cut.」Γ2 is madeup of the rest of the original curve plus the short cut.The circulation around Γ1 is the sum of an integral along Γa and along Γab.Similarly, the circulation around Γ2 is the sum of two parts, one along Γb and theother along Γab. The integral along Γab will have, for the curve Γ2, the oppositesign from what it has for Γ1, because the direction of travel is opposite—we musttake both our line integrals with the same「sense」of rotation.Following the same kind of argument we used before, you can see that thesum of the two circulations will give just the line integral around the originalcurve Γ. The parts due to Γab cancel. The circulation around the one part plusthe circulation around the second part equals the circulation about the outerline. We can continue the process of cutting the original loop into any numberof smaller loops. When we add the circulations of the smaller loops, there isalways a cancellation of the parts on their adjacent portions, so that the sum isequivalent to the circulation around the original single loop.

3-8

Fig. 3-7. The circulation of C aroundthe curve Γ is the line integral of Ct, thetangential component of C.

Fig. 3-8. The circulation around thewhole loop is the sum of the circulationsaround the two loops: Γ1 = Γa + Γab andΓ2 = Γb + Γab.

Fig. 3-9. Some surface bounded by theloop Γ is chosen. The surface is dividedinto a number of small areas, each approxi-mately a square. The circulation around Γis the sum of the circulations around thelittle loops.

I

C · ds = Cx(1) ∆x + Cy(2) ∆y − Cx(3) ∆x − Cy(4) ∆y.Now let’s look at the ﬁrst and third pieces. Together they are

(3.31)

Fig. 3-10. Computing the circulation of C

around a small square.

Now let us suppose that the original loop is the boundary of some surface.There are, of course, an inﬁnite number of surfaces which all have the originalloops as the boundary. Our results will not, however, depend on which surfacewe choose. First, we break our original loop into a number of small loops thatall lie on the surface we have chosen, as in Fig. 3-9. No matter what the shapeof the surface, if we choose our small loops small enough, we can assume thateach of the small loops will enclose an area which is essentially ﬂat. Also, we canchoose our small loops so that each is very nearly a square. Now we can calculatethe circulation around the big loop Γ by ﬁnding the circulations around all ofthe little squares and then taking their sum.

3-6 The circulation around a square; Stokes’ theoremHow shall we ﬁnd the circulation for each little square? One question is, howis the square oriented in space? We could easily make the calculation if it had aspecial orientation. For example, if it were in one of the coordinate planes. Sincewe have not assumed anything as yet about the orientation of the coordinateaxes, we can just as well choose the axes so that the one little square we areconcentrating on at the moment lies in the xy-plane, as in Fig. 3-10. If our resultis expressed in vector notation, we can say that it will be the same no matterwhat the particular orientation of the plane.

We want now to ﬁnd the circulation of the ﬁeld C around our little square. Itwill be easy to do the line integral if we make the square small enough that thevector C doesn’t change much along any one side of the square. (The assumptionis better the smaller the square, so we are really talking about inﬁnitesimalsquares.) Starting at the point (x, y)—the lower left corner of the ﬁgure—we goaround in the direction indicated by the arrows. Along the ﬁrst side—marked (1)—the tangential component is Cx(1) and the distance is ∆x. The ﬁrst part of theintegral is Cx(1) ∆x. Along the second leg, we get Cy(2) ∆y. Along the third, weget −Cx(3) ∆x, and along the fourth, −Cy(4) ∆y. The minus signs are requiredbecause we want the tangential component in the direction of travel. The wholeline integral is then

[Cx(1) − Cx(3)] ∆x.

(3.32)You might think that to our approximation the diﬀerence is zero. That is trueto the ﬁrst approximation. We can be more accurate, however, and take intoaccount the rate of change of Cx. If we do, we may write

Cx(3) = Cx(1) + ∂Cx∂y

∆y.

(3.33)

If we included the next approximation, it would involve terms in (∆y)2, but sincewe will ultimately think of the limit as ∆y → 0, such terms can be neglected.Putting (3.33) together with (3.32), we ﬁnd that

[Cx(1) − Cx(3)] ∆x = − ∂Cx∂y

∆x ∆y.

The derivative can, to our approximation, be evaluated at (x, y).

Similarly, for the other two terms in the circulation, we may write

Cy(2) ∆y − Cy(4) ∆y = ∂Cy∂x

∆x ∆y.

The circulation around our square is then

(cid:18) ∂Cy

∂x

(cid:19)

− ∂Cx∂y

∆x ∆y,

(3.34)

(3.35)

(3.36)

3-9

which is interesting, because the two terms in the parentheses are just the z-component of the curl. Also, we note that ∆x ∆y is the area of our square. Sowe can write our circulation (3.36) as

(∇ × C)z ∆a.

But the z-component really means the component normal to the surface element.We can, therefore, write the circulation around a diﬀerential square in an invariantvector form:

C · ds = (∇ × C)n ∆a = (∇ × C) · n ∆a.

(3.37)

I

Our result is: the circulation of any vector C around an inﬁnitesimal squareis the component of the curl of C normal to the surface, times the area of thesquare.The circulation around any loop Γ can now be easily related to the curl ofthe vector ﬁeld. We ﬁll in the loop with any convenient surface S, as in Fig. 3-11,and add the circulations around a set of inﬁnitesimal squares in this surface. Thesum can be written as an integral. Our result is a very useful theorem calledStokes’ theorem (after Mr. Stokes).

Stokes’ Theorem. I

Z

S

C · ds =

(∇ × C)n da,

(3.38)

Γ

where S is any surface bounded by Γ.We must now speak about a convention of signs. In Fig. 3-10 the z-axis wouldpoint toward you in a「usual」—that is,「right-handed」—system of axes. Whenwe took our line integral with a「positive」sense of rotation, we found that thecirculation was equal to the z-component of ∇ × C. If we had gone around theother way, we would have gotten the opposite sign. Now how shall we know,in general, what direction to choose for the positive direction of the「normal」component of ∇× C? The「positive」normal must always be related to the senseof rotation, as in Fig. 3-10. It is indicated for the general case in Fig. 3-11.One way of remembering the relationship is by the「right-hand rule.」If youmake the ﬁngers of your right hand go around the curve Γ, with the ﬁngertipspointed in the direction of the positive sense of ds, then your thumb points inthe direction of the positive normal to the surface S.

3-7 Curl-free and divergence-free ﬁeldsWe would like, now, to consider some consequences of our new theorems. Takeﬁrst the case of a vector whose curl is everywhere zero. Then Stokes’ theoremsays that the circulation around any loop is zero. Now if we choose two points(1) and (2) on a closed curve (Fig. 3-12), it follows that the line integral of thetangential component from (1) to (2) is independent of which of the two possiblepaths is taken. We can conclude that the integral from (1) to (2) can dependonly on the location of these points—that is to say, it is some function of positiononly. The same logic was used in Chapter 14 of Vol. I, where we proved thatif the integral around a closed loop of some quantity is always zero, then thatintegral can be represented as the diﬀerence of a function of the position of thetwo ends. This fact allowed us to invent the idea of a potential. We proved,furthermore, that the vector ﬁeld was the gradient of this potential function (seeEq. 14.13 of Vol. I).It follows that any vector ﬁeld whose curl is zero is equal to the gradient ofsome scalar function. That is, if ∇ × C = 0, everywhere, there is some ψ (psi)for which C = ∇ψ—a useful idea. We can, if we wish, describe this special kindof vector ﬁeld by means of a scalar ﬁeld.Let’s show something else. Suppose we have any scalar ﬁeld φ (phi). If wetake its gradient, ∇φ, the integral of this vector around any closed loop must be3-10

Fig. 3-11. The circulation of C around Γis the surface integral of the normal compo-nent of ∇ × C.

Fig. 3-12. If ∇×C is zero, the circulationaround the closed curve Γ is zero. The lineintegral from (1) to (2) along a must bethe same as the line integral along b.

zero. Its line integral from point (1) to point (2) is [φ(2) − φ(1)]. If (1) and (2)are the same points, our Theorem 1, Eq. (3.8), tells us that the line integral iszero:

Using Stokes’ theorem, we can conclude that

I

loop

Z

∇φ · ds = 0.

(∇ × (∇φ))n da = 0

over any surface. But if the integral is zero over any surface, the integrand mustbe zero. So

∇ × (∇φ) = 0,

always.

We proved the same result in Section 2-7 by vector algebra.

Let’s look now at a special case in which we ﬁll in a small loop Γ with alarge surface S, as indicated in Fig. 3-13. We would like, in fact, to see whathappens when the loop shrinks down to a point, so that the surface boundarydisappears—the surface becomes closed. Now if the vector C is everywhere ﬁnite,the line integral around Γ must go to zero as we shrink the loop—the integral isroughly proportional to the circumference of Γ, which goes to zero. According toStokes’ theorem, the surface integral of (∇ × C)n must also vanish. Somehow,as we close the surface we add in contributions that cancel out what was therebefore. So we have a new theorem:

(∇ × C)n da = 0.

(3.39)

Z

any closed

surface

Fig. 3-13. Going to the limit of a closedsurface, we ﬁnd that the surface integralof (∇ × C)n must vanish.

Z

closedsurface

Z

Now this is interesting, because we already have a theorem about the surfaceintegral of a vector ﬁeld. Such a surface integral is equal to the volume integralof the divergence of the vector, according to Gauss’ theorem (Eq. 3.18). Gauss’theorem, applied to ∇ × C, says

(∇ × C)n da =

∇ · (∇ × C) dV.

(3.40)

Z

volumeinside

So we conclude that the second integral must also be zero:

∇ · (∇ × C) dV = 0,

(3.41)

any

volume

and this is true for any vector ﬁeld C whatever. Since Eq. (3.41) is true for anyvolume, it must be true that at every point in space the integrand is zero. Wehave

∇ · (∇ × C) = 0,

always.

But this is the same result we got from vector algebra in Section 2-7. Now webegin to see how everything ﬁts together.

3-8 SummaryLet us summarize what we have found about the vector calculus. These are

really the salient points of Chapters 2 and 3:

1. The operators ∂/∂x, ∂/∂y, and ∂/∂z can be considered as the three com-ponents of a vector operator ∇, and the formulas which result from vectoralgebra by treating this operator as a vector are correct:

(cid:18) ∂

∇ =

,

∂∂y

,

∂∂z

∂x

(cid:19)

.

3-11

2. The diﬀerence of the values of a scalar ﬁeld at two points is equal to the lineintegral of the tangential component of the gradient of that scalar alongany curve at all between the ﬁrst and second points:

ψ(2) − ψ(1) =

∇ψ · ds.

(3.42)

3. The surface integral of the normal component of an arbitrary vector over aclosed surface is equal to the integral of the divergence of the vector overthe volume interior to the surface:

C · n da =

∇ · C dV.

(3.43)

closedsurface

volumeinside

4. The line integral of the tangential component of an arbitrary vector arounda closed loop is equal to the surface integral of the normal component ofthe curl of that vector over any surface which is bounded by the loop:

Z (2)

(1)

any curve

Z

Z

Z

Z

C · ds =

boundary

surface

(∇ × C) · n da.

(3.44)

3-12

4-1 Statics4-2 Coulomb’s law; superposition4-3 Electric potential4-4 E = −∇φ4-5 The ﬂux of E4-6 Gauss’ law; the divergence of E4-7 Field of a sphere of charge4-8 Field lines; equipotential surfaces

Review: Chapters 13 and 14, Vol. I,

Work and Potential Energy

1074π

0c2 =1

≈ 9 × 1094π0[0] = coulomb2

/newton·meter2



