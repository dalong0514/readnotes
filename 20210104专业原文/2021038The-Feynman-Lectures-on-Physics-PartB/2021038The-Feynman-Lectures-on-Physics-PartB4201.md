27-1 Local conservationIt

is clear that the energy of matter is not conserved. When an object radiateslight it loses energy. However, the energy lost is possibly describable in someother form, say in the light. Therefore the theory of the conservation of energyis incomplete without a consideration of the energy which is associated withthe light or, in general, with the electromagnetic ﬁeld. We take up now the lawof conservation of energy and, also, of momentum for the ﬁelds. Certainly, wecannot treat one without the other, because in the relativity theory they arediﬀerent aspects of the same four-vector.

Very early in Volume I, we discussed the conservation of energy; we said thenmerely that the total energy in the world is constant. Now we want to extendthe idea of the energy conservation law in an important way—in a way thatsays something in detail about how energy is conserved. The new law will saythat if energy goes away from a region, it is because it ﬂows away through theboundaries of that region. It is a somewhat stronger law than the conservationof energy without such a restriction.

To see what the statement means, let’s look at how the law of the conservationof charge works. We described the conservation of charge by saying that there isa current density j and a charge density ρ, and that when the charge decreasesat some place there must be a ﬂow of charge away from that place. We call thatthe conservation of charge. The mathematical form of the conservation law is

27-1 Local conservation27-2 Energy conservation and

electromagnetism

27-3 Energy density and energy ﬂow

in the electromagnetic ﬁeld

27-4 The ambiguity of the ﬁeld energy27-5 Examples of energy ﬂow27-6 Field momentum

∇ · j = − ∂ρ∂t

.

(27.1)

This law has the consequence that the total charge in the world is always constant—there is never any net gain or loss of charge. However, the total charge in the worldcould be constant in another way. Suppose that there is some charge Q1 nearsome point (1) while there is no charge near some point (2) some distance away(Fig. 27-1). Now suppose that, as time goes on, the charge Q1 were to graduallyfade away and that simultaneously with the decrease of Q1 some charge Q2 wouldappear near point (2), and in such a way that at every instant the sum of Q1and Q2 was a constant. In other words, at any intermediate state the amount ofcharge lost by Q1 would be added to Q2. Then the total amount of charge inthe world would be conserved. That’s a「world-wide」conservation, but not whatwe will call a「local」conservation, because in order for the charge to get from(1) to (2), it didn’t have to appear anywhere in the space between point (1) andpoint (2). Locally, the charge was just「lost.」

There is a diﬃculty with such a「world-wide」conservation law in the theory ofrelativity. The concept of「simultaneous moments」at distant points is one whichis not equivalent in diﬀerent systems. Two events that are simultaneous in onesystem are not simultaneous for another system moving past. For「world-wide」conservation of the kind described, it is necessary that the charge lost from Q1should appear simultaneously in Q2. Otherwise there would be some momentswhen the charge was not conserved. There seems to be no way to make thelaw of charge conservation relativistically invariant without making it a「local」conservation law. As a matter of fact, the requirement of the Lorentz relativisticinvariance seems to restrict the possible laws of nature in surprising ways. Inmodern quantum ﬁeld theory, for example, people have often wanted to alter thetheory by allowing what we call a「nonlocal」interaction—where something here27-1

Fig. 27-1. Two ways to conserve charge:(a) Q1 + Q2 is constant; (b) dQ1/dt =

−(cid:82) j · n da = −dQ2/dt.

has a direct eﬀect on something there—but we get in trouble with the relativityprinciple.「Local」conservation involves another idea. It says that a charge can getfrom one place to another only if there is something happening in the spacebetween. To describe the law we need not only the density of charge, ρ, but alsoanother kind of quantity, namely j, a vector giving the rate of ﬂow of chargeacross a surface. Then the ﬂow is related to the rate of change of the densityby Eq. (27.1). This is the more extreme kind of a conservation law. It says thatcharge is conserved in a special way—conserved「locally.」

It turns out that energy conservation is also a local process. There is not onlyan energy density in a given region of space but also a vector to represent therate of ﬂow of the energy through a surface. For example, when a light sourceradiates, we can ﬁnd the light energy moving out from the source. If we imaginesome mathematical surface surrounding the light source, the energy lost frominside the surface is equal to the energy that ﬂows out through the surface.

27-2 Energy conservation and electromagnetismWe want now to write quantitatively the conservation of energy for electro-magnetism. To do that, we have to describe how much energy there is in anyvolume element of space, and also the rate of energy ﬂow. Suppose we thinkﬁrst only of the electromagnetic ﬁeld energy. We will let u represent the energydensity in the ﬁeld (that is, the amount of energy per unit volume in space) andlet the vector S represent the energy ﬂux of the ﬁeld (that is, the ﬂow of energyper unit time across a unit area perpendicular to the ﬂow). Then, in perfectanalogy with the conservation of charge, Eq. (27.1), we can write the「local」lawof energy conservation in the ﬁeld as

= −∇ · S.

∂u∂t

(27.2)

Of course, this law is not true in general; it is not true that the ﬁeld energy isconserved. Suppose you are in a dark room and then turn on the light switch. Allof a sudden the room is full of light, so there is energy in the ﬁeld, although therewasn’t any energy there before. Equation (27.2) is not the complete conservationlaw, because the ﬁeld energy alone is not conserved, only the total energy in theworld—there is also the energy of matter. The ﬁeld energy will change if there issome work being done by matter on the ﬁeld or by the ﬁeld on matter.

energy it has: Each particle has the energy m0c2/p1 − v2/c2. The total energy

However, if there is matter inside the volume of interest, we know how much

of the matter is just the sum of all the particle energies, and the ﬂow of thisenergy through a surface is just the sum of the energy carried by each particlethat crosses the surface. We want now to talk only about the energy of theelectromagnetic ﬁeld. So we must write an equation which says that the totalﬁeld energy in a given volume decreases either because ﬁeld energy ﬂows out ofthe volume or because the ﬁeld loses energy to matter (or gains energy, which isjust a negative loss). The ﬁeld energy inside a volume V is

Z

u dV,

V

and its rate of decrease is minus the time derivative of this integral. The ﬂow ofﬁeld energy out of the volume V is the integral of the normal component of S

S · n da + (work done on matter inside V ).

(27.3)

27-2

over the surface Σ that encloses V ,Z

So

Z

V

− ddt

Z

Σ

u dV =

S · n da.

Σ

We have seen before that the ﬁeld does work on each unit volume of matterat the rate E · j. [The force on a particle is F = q(E + v × B), and the rate ofdoing work is F · v = qE · v. If there are N particles per unit volume, the rateof doing work per unit volume is N qE · v, but N qv = j.] So the quantity E · jmust be equal to the loss of energy per unit time and per unit volume by theﬁeld. Equation (27.3) then becomes

u dV =

S · n da +

E · j dV.

(27.4)

This is our conservation law for energy in the ﬁeld. We can convert it into adiﬀerential equation like Eq. (27.2) if we can change the second term to a volumeintegral. That is easy to do with Gauss’ theorem. The surface integral of thenormal component of S is the integral of its divergence over the volume inside.So Eq. (27.3) is equivalent to

Z

V

− ddt

Z

Z

Σ

Z

Z

V

Z

−

dV =

∂u∂t

V

∇ · S dV +

E · j dV,

V

V

where we have put the time derivative of the ﬁrst term inside the integral. Sincethis equation is true for any volume, we can take away the integrals and we havethe energy equation for the electromagnetic ﬁelds:

− ∂u∂t

= ∇ · S + E · j.

(27.5)

Now this equation doesn’t do us a bit of good unless we know what u and Sare. Perhaps we should just tell you what they are in terms of E and B, becauseall we really want is the result. However, we would rather show you the kind ofargument that was used by Poynting in 1884 to obtain formulas for S and u,so you can see where they come from. (You won’t, however, need to learn thisderivation for our later work.)

27-3 Energy density and energy ﬂow in the electromagnetic ﬁeldThe idea is to suppose that there is a ﬁeld energy density u and a ﬂux Sthat depend only upon the ﬁelds E and B. (For example, we know that in2 0E · E.) Of course,electrostatics, at least, the energy density can be written 1the u and S might depend on the potentials or something else, but let’s see whatwe can work out. We can try to rewrite the quantity E · j in such a way that itbecomes the sum of two terms: one that is the time derivative of one quantityand another that is the divergence of a second quantity. The ﬁrst quantity wouldthen be u and the second would be S (with suitable signs). Both quantities mustbe written in terms of the ﬁelds only; that is, we want to write our equality as

E · j = − ∂u∂t

− ∇ · S.

(27.6)

The left-hand side must ﬁrst be expressed in terms of the ﬁelds only. How canwe do that? By using Maxwell’s equations, of course. From Maxwell’s equationfor the curl of B,

Substituting this in (27.6) we will have only E’s and B’s:

j = 0c2∇ × B − 0

∂E∂t

.

E · j = 0c2E · (∇ × B) − 0E · ∂E∂t

.

(27.7)

We are already partly ﬁnished. The last term is a time derivative—it is2 0E · E is at least one part of u. It’s the same thing we(∂/∂t)( 1found in electrostatics. Now, all we have to do is to make the other term intothe divergence of something.

2 0E · E). So 1

27-3

Notice that the ﬁrst term on the right-hand side of (27.7) is the same as

(∇ × B) · E.

∇ · (B × E)

(27.8)And, as you know from vector algebra, (a × b) · c is the same as a · (b × c); soour term is also the same as(27.9)and we have the divergence of「something,」just as we wanted. Only that’s wrong!We warned you before that ∇ is「like」a vector, but not「exactly」the same. Thereason it is not is because there is an additional convention from calculus: whena derivative operator is in front of a product, it works on everything to the right.In Eq. (27.7), the ∇ operates only on B, not on E. But in the form (27.9), thenormal convention would say that ∇ operates on both B and E. So it’s not thesame thing. In fact, if we work out the components of ∇ · (B × E) we can seethat it is equal to E · (∇ × B) plus some other terms. It’s like what happenswhen we take a derivative of a product in algebra. For instance,

ddx

(f g) = dfdx

g + f

dgdx

.

Rather than working out all the components of ∇ · (B × E), we would liketo show you a trick that is very useful for this kind of problem. It is a trickthat allows you to use all the rules of vector algebra on expressions with the∇ operator, without getting into trouble. The trick is to throw out—for a whileat least—the rule of the calculus notation about what the derivative operatorworks on. You see, ordinarily, the order of terms is used for two separate purposes.One is for calculus: f(d/dx)g is not the same as g(d/dx)f; and the other is forvectors: a × b is diﬀerent from b × a. We can, if we want, choose to abandonmomentarily the calculus rule. Instead of saying that a derivative operates oneverything to the right, we make a new rule that doesn’t depend on the orderin which terms are written down. Then we can juggle terms around withoutworrying.

Here is our new convention: we show, by a subscript, what a diﬀerentialoperator works on; the order has no meaning. Suppose we let the operator Dstand for ∂/∂x. Then Df means that only the derivative of the variable quantity fis taken. Then

Df f = ∂f∂x

Df f g =

But if we have Df f g, it means

.

(cid:19)

g.

(cid:18) ∂f

∂x

But notice now that according to our new rule, f Df g means the same thing. Wecan write the same thing any which way:

Df f g = gDf f = f Df g = f gDf .

You see, the Df can even come after everything. (It’s surprising that such ahandy notation is never taught in books on mathematics or physics.)You may wonder: What if I want to write the derivative of f g? I want thederivative of both terms. That’s easy, you just say so; you write Df(f g)+ Dg(f g).That is just g(∂f /∂x) + f(∂g/∂x), which is what you mean in the old notationby ∂(f g)/∂x.You will see that it is now going to be very easy to work out a new expressionfor ∇ · (B × E). We start by changing to the new notation; we write

∇ · (B × E) = ∇B · (B × E) + ∇E · (B × E).

(27.10)

The moment we do that we don’t have to keep the order straight any more. Wealways know that ∇E operates on E only, and ∇B operates on B only. In these27-4

circumstances, we can use ∇ as though it were an ordinary vector. (Of course,when we are ﬁnished, we will want to return to the「standard」notation thateverybody usually uses.) So now we can do the various things like interchangingdots and crosses and making other kinds of rearrangements of the terms. Forinstance, the middle term of Eq. (27.10) can be rewritten as E · ∇ × B. (Youremember that a· b× c = b· c× a.) And the last term is the same as B · E ×∇E.It looks freakish, but it is all right. Now if we try to go back to the ordinaryconvention, we have to arrange that the ∇ operates only on its「own」variable.The ﬁrst one is already that way, so we can just leave oﬀ the subscript. Thesecond one needs some rearranging to put the ∇ in front of the E, which we cando by reversing the cross product and changing sign:

B · (E × ∇E) = −B · (∇E × E).

Now it is in a conventional order, so we can return to the usual notation. Equa-tion (27.10) is equivalent to

∇ · (B × E) = E · (∇ × B) − B · (∇ × E).

(27.11)(A quicker way would have been to use components in this special case, but itwas worth taking the time to show you the mathematical trick. You probablywon’t see it anywhere else, and it is very good for unlocking vector algebra fromthe rules about the order of terms with derivatives.)We now return to our energy conservation discussion and use our new result,Eq. (27.11), to transform the ∇ × B term of Eq. (27.7). That energy equationbecomes

E · j = 0c2∇ · (B × E) + 0c2B · (∇ × E) − ∂∂t

2 0E · E).( 1

(27.12)

Now you see, we’re almost ﬁnished. We have one term which is a nice derivativewith respect to t to use for u and another that is a beautiful divergence torepresent S. Unfortunately, there is the center term left over, which is neithera divergence nor a derivative with respect to t. So we almost made it, but notquite. After some thought, we look back at the diﬀerential equations of Maxwelland discover that ∇ × E is, fortunately, equal to −∂B/∂t, which means that wecan turn the extra term into something that is a pure time derivative:

(cid:18)

(cid:18) B · B

B · (∇ × E) = B ·

(cid:19)(cid:18) 0c22 B · B + 0which is exactly like Eq. (27.6), if we make the deﬁnitions

Now we have exactly what we want. Our energy equation reads2 E · E

E · j = ∇ · (0c2B × E) − ∂∂t

− ∂B∂t

= − ∂∂t

2

.

(cid:19)(cid:19)

,

(27.13)

(27.14)

(27.15)

and

u = 0

2 B · B

2 E · E + 0c2S = 0c2E × B.

(Reversing the cross product makes the signs come out right.)

Our program was successful. We have an expression for the energy densitythat is the sum of an「electric」energy density and a「magnetic」energy density,whose forms are just like the ones we found in statics when we worked out theenergy in terms of the ﬁelds. Also, we have found a formula for the energy ﬂowvector of the electromagnetic ﬁeld. This new vector, S = 0c2E × B, is called「Poynting’s vector,」after its discoverer. It tells us the rate at which the ﬁeldenergy moves around in space. The energy which ﬂows through a small area daper second is S · n da, where n is the unit vector perpendicular to da. (Now thatwe have our formulas for u and S, you can forget the derivations if you want.)27-5

27-4 The ambiguity of the ﬁeld energyBefore we take up some applications of the Poynting formulas [Eqs. (27.14)and (27.15)], we would like to say that we have not really「proved」them. Allwe did was to ﬁnd a possible「u」and a possible「S.」How do we know that byjuggling the terms around some more we couldn’t ﬁnd another formula for「u」and another formula for「S」? The new S and the new u would be diﬀerent,but they would still satisfy Eq. (27.6). It’s possible. It can be done, but theforms that have been found always involve various derivatives of the ﬁeld (andalways with second-order terms like a second derivative or the square of a ﬁrstderivative). There are, in fact, an inﬁnite number of diﬀerent possibilities for uand S, and so far no one has thought of an experimental way to tell which one isright! People have guessed that the simplest one is probably the correct one, butwe must say that we do not know for certain what is the actual location in spaceof the electromagnetic ﬁeld energy. So we too will take the easy way out and saythat the ﬁeld energy is given by Eq. (27.14). Then the ﬂow vector S must begiven by Eq. (27.15).It is interesting that there seems to be no unique way to resolve the indeﬁnite-ness in the location of the ﬁeld energy. It is sometimes claimed that this problemcan be resolved by using the theory of gravitation in the following argument. Inthe theory of gravity, all energy is the source of gravitational attraction. Thereforethe energy density of electricity must be located properly if we are to know inwhich direction the gravity force acts. As yet, however, no one has done sucha delicate experiment that the precise location of the gravitational inﬂuence ofelectromagnetic ﬁelds could be determined. That electromagnetic ﬁelds alonecan be the source of gravitational force is an idea it is hard to do without. It has,in fact, been observed that light is deﬂected as it passes near the sun—we couldsay that the sun pulls the light down toward it. Do you not want to allow thatthe light pulls equally on the sun? Anyway, everyone always accepts the simpleexpressions we have found for the location of electromagnetic energy and its ﬂow.And although sometimes the results obtained from using them seem strange,nobody has ever found anything wrong with them—that is, no disagreement withexperiment. So we will follow the rest of the world—besides, we believe that it isprobably perfectly right.

We should make one further remark about the energy formula. In the ﬁrstplace, the energy per unit volume in the ﬁeld is very simple: It is the electrostaticenergy plus the magnetic energy, if we write the electrostatic energy in termsof E2 and the magnetic energy as B2. We found two such expressions as possibleexpressions for the energy when we were doing static problems. We also founda number of other formulas for the energy in the electrostatic ﬁeld, such as ρφ,which is equal to the integral of E · E in the electrostatic case. However, in anelectrodynamic ﬁeld the equality failed, and there was no obvious choice as towhich was the right one. Now we know which is the right one. Similarly, we havefound the formula for the magnetic energy that is correct in general. The rightformula for the energy density of dynamic ﬁelds is Eq. (27.14).

27-5 Examples of energy ﬂowOur formula for the energy ﬂow vector S is something quite new. We wantnow to see how it works in some special cases and also to see whether it checksout with anything that we knew before. The ﬁrst example we will take is light. Ina light wave we have an E vector and a B vector at right angles to each other andto the direction of the wave propagation. (See Fig. 27-2.) In an electromagneticwave, the magnitude of B is equal to 1/c times the magnitude of E, and sincethey are at right angles,

Therefore, for light, the ﬂow of energy per unit area per second is

c

|E × B| = E2

.

S = 0cE2.

(27.16)27-6

Fig. 27-2. The vectors E, B, and S for

a light wave.

For a light wave in which E = E0 cos ω(t − x/c), the average rate of energy ﬂowper unit area, hSiav—which is called the「intensity」of the light—is the meanvalue of the square of the electric ﬁeld times 0c:

Intensity = hSiav = 0chE2iav.

(27.17)

Believe it or not, we have already derived this result in Section 31-5 of Vol. I,when we were studying light. We can believe that it is right because it also checksagainst something else. When we have a light beam, there is an energy densityin space given by Eq. (27.14). Using cB = E for a light wave, we get that

u = 0

2 E2 + 0c22

= 0E2.

(cid:18) E2

(cid:19)

c2

But E varies in space, so the average energy density is

(27.18)Now the wave travels at the speed c, so we should think that the energy thatgoes through a square meter in a second is c times the amount of energy in onecubic meter. So we would say that

huiav = 0hE2iav.

hSiav = 0chE2iav.

And it’s right; it is the same as Eq. (27.17).

Now we take another example. Here is a rather curious one. We look at theenergy ﬂow in a capacitor that we are charging slowly. (We don’t want frequenciesso high that the capacitor is beginning to look like a resonant cavity, but wedon’t want dc either.) Suppose we use a circular parallel plate capacitor of ourusual kind, as shown in Fig. 27-3. There is a nearly uniform electric ﬁeld insidewhich is changing with time. At any instant the total electromagnetic energyinside is u times the volume. If the plates have a radius a and a separation h,the total energy between the plates is

U =

2 E2

(πa2h).

(27.19)

This energy changes when E changes. When the capacitor is being charged, thevolume between the plates is receiving energy at the rate

= 0πa2hE ˙E.

dUdt

(27.20)

So there must be a ﬂow of energy into that volume from somewhere. Of courseyou know that it must come in on the charging wires—not at all! It can’t enterthe space between the plates from that direction, because E is perpendicular tothe plates; E × B must be parallel to the plates.You remember, of course, that there is a magnetic ﬁeld that circles aroundthe axis when the capacitor is charging. We discussed that in Chapter 23. Usingthe last of Maxwell’s equations, we found that the magnetic ﬁeld at the edge ofthe capacitor is given by

(cid:18) 0

(cid:19)

or

2πac2B = ˙E · πa2,

B = a2c2

˙E.

Its direction is shown in Fig. 27-3. So there is an energy ﬂow proportionalto E × B that comes in all around the edges, as shown in the ﬁgure. Theenergy isn’t actually coming down the wires, but from the space surrounding thecapacitor.

Let’s check whether or not the total amount of ﬂow through the whole surfacebetween the edges of the plates checks with the rate of change of the energy27-7

Fig. 27-3. Near a charging capacitor, thePoynting vector S points inward toward theaxis.

inside—it had better; we went through all that work proving Eq. (27.15) to makesure, but let’s see. The area of the surface is 2πah, and S = 0c2E × B is inmagnitude

(cid:19)

˙E

,

(cid:18) a

2c2

0c2E

so the total ﬂux of energy is

πa2h0E ˙E.

It does check with Eq. (27.20). But it tells us a peculiar thing: that when we arecharging a capacitor, the energy is not coming down the wires; it is coming inthrough the edges of the gap. That’s what this theory says!

How can that be? That’s not an easy question, but here is one way of thinkingabout it. Suppose that we had some charges above and below the capacitorand far away. When the charges are far away, there is a weak but enormouslyspread-out ﬁeld that surrounds the capacitor. (See Fig. 27-4.) Then, as thecharges come together, the ﬁeld gets stronger nearer to the capacitor. So theﬁeld energy which is way out moves toward the capacitor and eventually ends upbetween the plates.

As another example, we ask what happens in a piece of resistance wire whenit is carrying a current. Since the wire has resistance, there is an electric ﬁeldalong it, driving the current. Because there is a potential drop along the wire,there is also an electric ﬁeld just outside the wire, parallel to the surface. (SeeFig. 27-5.) There is, in addition, a magnetic ﬁeld which goes around the wirebecause of the current. The E and B are at right angles; therefore there is aPoynting vector directed radially inward, as shown in the ﬁgure. There is a ﬂowof energy into the wire all around. It is, of course, equal to the energy being lostin the wire in the form of heat. So our「crazy」theory says that the electrons aregetting their energy to generate heat because of the energy ﬂowing into the wirefrom the ﬁeld outside. Intuition would seem to tell us that the electrons get theirenergy from being pushed along the wire, so the energy should be ﬂowing down(or up) along the wire. But the theory says that the electrons are really beingpushed by an electric ﬁeld, which has come from some charges very far away,and that the electrons get their energy for generating heat from these ﬁelds. Theenergy somehow ﬂows from the distant charges into a wide area of space andthen inward to the wire.

Finally, in order to really convince you that this theory is obviously nuts,we will take one more example—an example in which an electric charge and amagnet are at rest near each other—both sitting quite still. Suppose we take theexample of a point charge sitting near the center of a bar magnet, as shown inFig. 27-6. Everything is at rest, so the energy is not changing with time. Also,E and B are quite static. But the Poynting vector says that there is a ﬂow ofenergy, because there is an E × B that is not zero. If you look at the energyﬂow, you ﬁnd that it just circulates around and around. There isn’t any changein the energy anywhere—everything which ﬂows into one volume ﬂows out again.It is like incompressible water ﬂowing around. So there is a circulation of energyin this so-called static condition. How absurd it gets!

Perhaps it isn’t so terribly puzzling, though, when you remember that what wecalled a「static」magnet is really a circulating permanent current. In a permanentmagnet the electrons are spinning permanently inside. So maybe a circulation ofthe energy outside isn’t so queer after all.

You no doubt begin to get the impression that the Poynting theory at leastpartially violates your intuition as to where energy is located in an electromagneticﬁeld. You might believe that you must revamp all your intuitions, and, thereforehave a lot of things to study here. But it seems really not necessary. You don’tneed to feel that you will be in great trouble if you forget once in a while thatthe energy in a wire is ﬂowing into the wire from the outside, rather than alongthe wire. It seems to be only rarely of value, when using the idea of energyconservation, to notice in detail what path the energy is taking. The circulationof energy around a magnet and a charge seems, in most circumstances, to be quite27-8

Fig. 27-4. The ﬁelds outside a capacitorwhen it is being charged by bringing twocharges from a large distance.

Fig. 27-5. The Poynting vector S near a

wire carrying a current.

Fig. 27-6. A charge and a magnet pro-duce a Poynting vector that circulates inclosed loops.

unimportant. It is not a vital detail, but it is clear that our ordinary intuitionsare quite wrong.

27-6 Field momentumNext we would like to talk about the momentum in the electromagnetic ﬁeld.Just as the ﬁeld has energy, it will have a certain momentum per unit volume.Let us call that momentum density g. Of course, momentum has various possibledirections, so that g must be a vector. Let’s talk about one component at a time;ﬁrst, we take the x-component. Since each component of momentum is conservedwe should be able to write down a law that looks something like this:

(cid:18)momentum

(cid:19)

of matter

− ∂∂t

(cid:18)momentum

(cid:19)

outﬂow

.

x

= ∂gx∂t

+

x

The left side is easy. The rate-of-change of the momentum of matter is just theforce on it. For a particle, it is F = q(E + v × B); for a distribution of charges,the force per unit volume is (ρE + j × B). The「momentum outﬂow」term,however, is strange. It cannot be the divergence of a vector because it is not ascalar; it is, rather, an x-component of some vector. Anyway, it should probablylook something like

∂a∂x

+ ∂b∂y

+ ∂c∂z

,

because the x-momentum could be ﬂowing in any one of the three directions.In any case, whatever a, b, and c are, the combination is supposed to equal theoutﬂow of the x-momentum.Now the game would be to write ρE + j × B in terms only of E and B—eliminating ρ and j by using Maxwell’s equations—and then to juggle terms andmake substitutions to get it into a form that looks like

∂gx∂t

+ ∂a∂x

+ ∂b∂y

+ ∂c∂z

.

Then, by identifying terms, we would have expressions for gx, a, b, and c. It’s alot of work, and we are not going to do it. Instead, we are only going to ﬁnd anexpression for g, the momentum density—and by a diﬀerent route.

There is an important theorem in mechanics which is this: whenever thereis a ﬂow of energy in any circumstance at all (ﬁeld energy or any other kind ofenergy), the energy ﬂowing through a unit area per unit time, when multipliedby 1/c2, is equal to the momentum per unit volume in the space. In the specialcase of electrodynamics, this theorem gives the result that g is 1/c2 times thePoynting vector:

g = 1

c2 S.

(27.21)

So the Poynting vector gives not only energy ﬂow but, if you divide by c2, alsothe momentum density. The same result would come out of the other analysiswe suggested, but it is more interesting to notice this more general result. Wewill now give a number of interesting examples and arguments to convince youthat the general theorem is true.

First example: Suppose that we have a lot of particles in a box—let’s say Nper cubic meter—and that they are moving along with some velocity v. Nowlet’s consider an imaginary plane surface perpendicular to v. The energy ﬂowthrough a unit area of this surface per second is equal to N v, the number whichﬂow through the surface per second, times the energy carried by each one. The

energy in each particle is m0c2/p1 − v2/c2. So the energy ﬂow per second is

p1 − v2/c2 .

m0c2

N v

27-9

But the momentum of each particle is m0v/p1 − v2/c2, so the density of mo-

mentum is

m0vp1 − v2/c2 ,

N

which is just 1/c2 times the energy ﬂow—as the theorem says. So the theorem istrue for a bunch of particles.It is also true for light. When we studied light in Volume I, we saw that whenthe energy is absorbed from a light beam, a certain amount of momentum isdelivered to the absorber. We have, in fact, shown in Chapter 34 of Vol. I thatthe momentum is 1/c times the energy absorbed [Eq. (34.24) of Vol. I]. If welet U0 be the energy arriving at a unit area per second, then the momentumarriving at a unit area per second is U0/c. But the momentum is travelling atthe speed c, so its density in front of the absorber must be U0/c2. So again thetheorem is right.Finally we will give an argument due to Einstein which demonstrates thesame thing once more. Suppose that we have a railroad car on wheels (assumedfrictionless) with a certain big mass M. At one end there is a device which willshoot out some particles or light (or anything, it doesn’t make any diﬀerence whatit is), which are then stopped at the opposite end of the car. There was someenergy originally at one end—say the energy U indicated in Fig. 27-7(a)—andthen later it is at the opposite end, as shown in Fig. 27-7(c). The energy U hasbeen displaced the distance L, the length of the car. Now the energy U hasthe mass U/c2, so if the car stayed still, the center of gravity of the car wouldbe moved. Einstein didn’t like the idea that the center of gravity of an objectcould be moved by fooling around only on the inside, so he assumed that it isimpossible to move the center of gravity by doing anything inside. But if that isthe case, when we moved the energy U from one end to the other, the whole carmust have recoiled some distance x, as shown in part (c) of the ﬁgure. You cansee, in fact, that the total mass of the car, times x, must equal the mass of theenergy moved, U/c2 times L (assuming that U/c2 is much less than M):

M x = U

c2 L.

(27.22)

Let’s now look at the special case of the energy being carried by a light ﬂash.(The argument would work as well for particles, but we will follow Einstein,who was interested in the problem of light.) What causes the car to be moved?Einstein argued as follows: When the light is emitted there must be a recoil,some unknown recoil with momentum p. It is this recoil which makes the carroll backward. The recoil velocity v of the car will be this momentum divided bythe mass of the car:

v = pM

.

The car moves with this velocity until the light energy U gets to the oppositeend. Then, when it hits, it gives back its momentum and stops the car. If x issmall, then the time the car moves is nearly equal to L/c; so we have that

x = vt = v

LcPutting this x in Eq. (27.22), we get thatp = Uc

= pM

Lc

.

.

Again we have the relation of energy and momentum for light. Dividing by c toget the momentum density g = p/c, we get once more that

g = Uc2 .

(27.23)

You may well wonder: What is so important about the center-of-gravitytheorem? Maybe it is wrong. Perhaps, but then we would also lose the con-servation of angular momentum. Suppose that our boxcar is moving along a27-10

Fig. 27-7. The energy U in motion at the

speed c carries the momentum U/c.

track at some speed v and that we shoot some light energy from the top to thebottom of the car—say, from A to B in Fig. 27-8. Now we look at the angularmomentum of the system about the point P. Before the energy U leaves A, it hasthe mass m = U/c2 and the velocity v, so it has the angular momentum mvrA.When it arrives at B, it has the same mass and, if the linear momentum of thewhole boxcar is not to change, it must still have the velocity v. It’s angular mo-mentum about P is then mvrB. The angular momentum will be changed unlessthe right recoil momentum was given to the car when the light was emitted—thatis, unless the light carries the momentum U/c. It turns out that the angularmomentum conservation and the theorem of center-of-gravity are closely relatedin the relativity theory. So the conservation of angular momentum would alsobe destroyed if our theorem were not true. At any rate, it does turn out to bea true general law, and in the case of electrodynamics we can use it to get themomentum in the ﬁeld.

We will mention two further examples of momentum in the electromagneticﬁeld. We pointed out in Section 26-2 the failure of the law of action and reactionwhen two charged particles were moving on orthogonal trajectories. The forceson the two particles don’t balance out, so the action and reaction are not equal;therefore the net momentum of the matter must be changing. It is not conserved.But the momentum in the ﬁeld is also changing in such a situation.If youwork out the amount of momentum given by the Poynting vector, it is notconstant. However, the change of the particle momenta is just made up by theﬁeld momentum, so the total momentum of particles plus ﬁeld is conserved.

Finally, another example is the situation with the magnet and the charge,shown in Fig. 27-6. We were unhappy to ﬁnd that energy was ﬂowing aroundin circles, but now, since we know that energy ﬂow and momentum are pro-portional, we know also that there is momentum circulating in the space. Buta circulating momentum means that there is angular momentum. So there isangular momentum in the ﬁeld. Do you remember the paradox we described inSection 17-4 about a solenoid and some charges mounted on a disc? It seemedthat when the current turned oﬀ, the whole disc should start to turn. The puzzlewas: Where did the angular momentum come from? The answer is that if youhave a magnetic ﬁeld and some charges, there will be some angular momentumin the ﬁeld. It must have been put there when the ﬁeld was built up. Whenthe ﬁeld is turned oﬀ, the angular momentum is given back. So the disc in theparadox would start rotating. This mystic circulating ﬂow of energy, which atﬁrst seemed so ridiculous, is absolutely necessary. There is really a momentumﬂow. It is needed to maintain the conservation of angular momentum in thewhole world.

Fig. 27-8. The energy U must carry themomentum U/c if the angular momentumabout P is to be conserved.

27-11

28-1 The ﬁeld energy of a point charge28-2 The ﬁeld momentum of a moving

28-3 Electromagnetic mass28-4 The force of an electron on itself28-5 Attempts to modify the Maxwell

charge

theory

28-6 The nuclear force ﬁeld

28

Electromagnetic Mass

