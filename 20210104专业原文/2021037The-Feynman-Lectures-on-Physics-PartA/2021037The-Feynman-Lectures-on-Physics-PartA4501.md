Illustrations of Thermodynamics

45-1 Internal energyThermodynamics is a rather diﬃcult and complex subject when we come toapply it, and it is not appropriate for us to go very far into the applicationsin this course. The subject is of very great importance, of course, to engineersand chemists, and those who are interested in the subject can learn about theapplications in physical chemistry or in engineering thermodynamics. Thereare also good equation reference books, such as Zemansky’s Heat and Thermo-dynamics, where one can learn more about the subject. In the EncyclopediaBritannica, fourteenth edition, one can ﬁnd excellent articles on thermodynamicsand thermochemistry, and in the article on chemistry, the sections on physicalchemistry, vaporization, liqueﬁcation of gases, and so on.

The subject of thermodynamics is complicated because there are so manydiﬀerent ways of describing the same thing. If we wish to describe the behaviorof a gas, we can say that the pressure depends on the temperature and on thevolume, or we can say that the volume depends on the temperature and thepressure. Or with respect to the internal energy U, we might say that it dependson the temperature and volume, if those are the variables we have chosen—butwe might also say that it depends on the temperature and the pressure, or thepressure and the volume, and so on. In the last chapter we discussed anotherfunction of temperature and volume, called the entropy S, and we can of courseconstruct as many other functions of these variables as we like: U − T S is afunction of temperature and volume. So we have a large number of diﬀerentquantities which can be functions of many diﬀerent combinations of variables.To keep the subject simple in this chapter, we shall decide at the startto use temperature and volume as the independent variables. Chemists usetemperature and pressure, because they are easier to measure and control inchemical experiments, but we shall use temperature and volume throughout this

45-1

chapter, except in one place where we shall see how to make the transformationinto the chemists’ system of variables.

We shall ﬁrst, then, consider only one system of independent variables: tem-perature and volume. Secondly, we shall discuss only two dependent functions:the internal energy and the pressure. All the other functions can be derivedfrom these, so it is not necessary to discuss them. With these limitations,thermodynamics is still a fairly diﬃcult subject, but it is not quite so impossible!First we shall review some mathematics. If a quantity is a function of twovariables, the idea of the derivative of the quantity requires a little more carefulthought than for the case where there is only one variable. What do we meanby the derivative of the pressure with respect to the temperature? The pressurechange accompanying a change in the temperature depends partly, of course, onwhat happens to the volume while T is changing. We must specify the changein V before the concept of a derivative with respect to T has a precise meaning.We might ask, for example, for the rate of change of P with respect to T if V isheld constant. This ratio is just the ordinary derivative that we usually writeas dP/dT. We customarily use a special symbol, ∂P/∂T, to remind us that Pdepends on another variable V as well as on T, and that this other variable isheld constant. We shall not only use the symbol ∂ to call attention to the factthat the other variable is held constant, but we shall also write the variable thatis held constant as a subscript, (∂P/∂T)V . Since we have only two independentvariables, this notation is redundant, but it will help us keep our wits about usin the thermodynamic jungle of partial derivatives.

Let us suppose that the function f(x, y) depends on the two independentvariables x and y. By (∂f /∂x)y we mean simply the ordinary derivative, obtainedin the usual way, if we treat y as a constant:

y

= limit∆x→0

= limit∆y→0

f(x + ∆x, y) − f(x, y)

∆x

f(x, y + ∆y) − f(x, y)

∆y

.

.

(cid:18) ∂fSimilarly, we deﬁne(cid:18) ∂f

∂x

(cid:19)(cid:19)

∂y

x

For example, if f(x, y) = x2 + yx, then (∂f /∂x)y = 2x + y, and (∂f /∂y)x = x.We can extend this idea to higher derivatives: ∂2f /∂y2 or ∂2f /∂y∂x. The lattersymbol indicates that we ﬁrst diﬀerentiate f with respect to x, treating y as a

45-2

constant, then diﬀerentiate the result with respect to y, treating x as a constant.The actual order of diﬀerentiation is immaterial: ∂2f /∂x∂y = ∂2f /∂y∂x.We will need to compute the change ∆f in f(x, y) when x changes to x + ∆xand y changes to y + ∆y. We assume throughout the following that ∆x and ∆yare inﬁnitesimally small:

∆f = f(x + ∆x, y + ∆y) − f(x, y)

= f(x + ∆x, y + ∆y) − f(x, y + ∆y)

|

=

∆x

{z(cid:18) ∂f

(cid:19)

∂x

y

} + f(x, y + ∆y) − f(x, y)|}

{z(cid:18) ∂f

(cid:19)

+

∆y

∂y

x

(45.1)

The last equation is the fundamental relation that expresses ∆f in terms of ∆xand ∆y.As an example of the use of this relation, let us calculate the change in theinternal energy U(T, V ) when the temperature changes from T to T + ∆T andthe volume changes from V to V + ∆V . Using Eq. (45.1), we write

(cid:18) ∂U

(cid:19)

∂T

V

(cid:18) ∂U

(cid:19)

∂V

∆U = ∆T

+ ∆V

.

T

(45.2)

In our last chapter we found another expression for the change ∆U in the internalenergy when a quantity of heat ∆Q was added to the gas:

∆U = ∆Q − P ∆V.

(45.3)

In comparing Eqs. (45.2) and (45.3) one might at ﬁrst be inclined to think thatP = −(∂U/∂V )T , but this is not correct. To obtain the correct relation, let us ﬁrstsuppose that we add a quantity of heat ∆Q to the gas while keeping the volumeconstant, so that ∆V = 0. With ∆V = 0, Eq. (45.3) tells us that ∆U = ∆Q,and Eq. (45.2) tells us that ∆U = (∂U/∂T)V ∆T, so that (∂U/∂T)V = ∆Q/∆T.The ratio ∆Q/∆T, the amount of heat one must put into a substance in orderto change its temperature by one degree with the volume held constant, is calledthe speciﬁc heat at constant volume and is designated by the symbol CV . By this

argument we have shown that (cid:18) ∂U

(cid:19)

= CV .

(45.4)

∂T

V

45-3

Fig. 45-1. Pressure-volume diagram for a Carnot cycle. The curvesmarked T and T − ∆T are isothermal lines; the steeper curves areadiabatic lines. ∆V is the volume change as heat ∆Q is added to thegas at constant temperature T . ∆P is the pressure change at constantvolume as the gas temperature is changed from T to T − ∆T .

Now let us again add a quantity of heat ∆Q to the gas, but this time wewill hold T constant and allow the volume to change by ∆V . The analysis inthis case is more complex, but we can calculate ∆U by the argument of Carnot,making use of the Carnot cycle we introduced in the last chapter.

The pressure-volume diagram for the Carnot cycle is shown in Fig. 45-1. Aswe have already shown, the total amount of work done by the gas in a reversiblecycle is ∆Q(∆T /T), where ∆Q is the amount of heat energy added to the gasas it expands isothermally at temperature T from volume V to V + ∆V , andT − ∆T is the ﬁnal temperature reached by the gas as it expands adiabaticallyon the second leg of the cycle. Now we will show that this work done is alsogiven by the shaded area in Fig. 45-1. In any circumstances, the work done by

the gas isR P dV , and is positive when the gas expands and negative when thethe integralR P dV , is the area under the curve connecting the initial and ﬁnal

gas is compressed. If we plot P vs. V , the variation of P and V is representedby a curve which gives the value of P corresponding to a particular value of V .As the volume changes from one value to another, the work done by the gas,

values of V . When we apply this idea to the Carnot cycle, we see that as we goaround the cycle, paying attention to the sign of the work done by the gas, thenet work done by the gas is just the shaded area in Fig. 45-1.

Now we want to evaluate the shaded area geometrically. The cycle wehave used in Fig. 45-1 diﬀers from that used in the previous chapter in thatwe now suppose that ∆T and ∆Q are inﬁnitesimally small. We are working

45-4

Fig. 45-2. Shaded area = area enclosed by dashed lines = area of

rectangle = ∆P ∆V .

between adiabatic lines and isothermal lines that are very close together, andthe ﬁgure described by the heavy lines in Fig. 45-1 will approach a parallelogramas the increments ∆T and ∆Q approach zero. The area of this parallelogram isjust ∆V ∆P, where ∆V is the change in volume as energy ∆Q is added to the gasat constant temperature, and ∆P is the change in pressure as the temperaturechanges by ∆T at constant volume. One can easily show that the shaded areain Fig. 45-1 is given by ∆V ∆P by recognizing that the shaded area is equal tothe area enclosed by the dotted lines in Fig. 45-2, which in turn diﬀers from therectangle bounded by ∆P and ∆V only by the addition and subtraction of theequal triangular areas in Fig. 45-2.Now let us summarize the results of the arguments we have developed so far:

(cid:18)∆T

(cid:19)



(45.5)

or

or

Work done by the gas = shaded area = ∆V ∆P = ∆Q

T

∆TT

· (heat needed to change V by ∆V )constant T

= ∆V · (change in P when T changes by ∆T)constant V1∆V

· (heat needed to change V by ∆V )T = T(∂P/∂T)V .

Equation (45.5) expresses the essential result of Carnot’s argument. The wholeof thermodynamics can be deduced from Eq. (45.5) and the First Law, which isstated in Eq. (45.3). Equation (45.5) is essentially the Second Law, although it

45-5

was originally deduced by Carnot in a slightly diﬀerent form, since he did notuse our deﬁnition of temperature.

Now we can proceed to calculate (∂U/∂V )T . By how much would the internalenergy U change if we changed the volume by ∆V ? First, U changes becauseheat is put in, and second, U changes because work is done. The heat put in is

(cid:18) ∂P

(cid:19)

∂T

V

∆Q = T

∆V,

according to Eq. (45.5), and the work done on the substance is −P ∆V . Thereforethe change ∆U in internal energy has two pieces:

∆U = T

∆V − P ∆V.

(cid:18) ∂P(cid:19)

∂T

(cid:19)(cid:18) ∂P

V

= T

T

(cid:19)

(cid:18) ∂U

∂V

− P.

∂T

V

(45.6)

(45.7)

Dividing both sides by ∆V , we ﬁnd for the rate of change of U with V atconstant T

In our thermodynamics, in which T and V are the only variables and P and Uare the only functions, Eqs. (45.3) and (45.7) are the basic equations from whichall the results of the subject can be deduced.

45-2 ApplicationsNow let us discuss the meaning of Eq. (45.7) and see why it answers thequestions which we proposed in our last chapter. We considered the followingproblem: in kinetic theory it is obvious that an increase in temperature leadsto an increase in pressure, because of the bombardments of the atoms on apiston. For the same physical reason, when we let the piston move back, heatis taken out of the gas and, in order to keep the temperature constant, heatwill have to be put back in. The gas cools when it expands, and the pressurerises when it is heated. There must be some connection between these twophenomena, and this connection is given explicitly in Eq. (45.7). If we hold thevolume ﬁxed and increase the temperature, the pressure rises at a rate (∂P/∂T)V .Related to that fact is this: if we increase the volume, the gas will cool unless wepour some heat in to maintain the temperature constant, and (∂U/∂V )T tellsus the amount of heat needed to maintain the temperature. Equation (45.7)

45-6

expresses the fundamental interrelationship between these two eﬀects. That iswhat we promised we would ﬁnd when we came to the laws of thermodynamics.Without knowing the internal mechanism of the gas, and knowing only that wecannot make perpetual motion of the second type, we can deduce the relationshipbetween the amount of heat needed to maintain a constant temperature whenthe gas expands, and the pressure change when the gas is heated at constantvolume!

Now that we have the result we wanted for a gas, let us consider the rubberband. When we stretch a rubber band, we ﬁnd that its temperature rises, andwhen we heat a rubber band, we ﬁnd that it pulls itself in. What is the equationthat gives the same relation for a rubber band as Eq. (45.3) gives for gas? For arubber band the situation will be something like this: when heat ∆Q is put in,the internal energy is changed by ∆U and some work is done. The only diﬀerencewill be that the work done by the rubber band is −F ∆L instead of P ∆V , whereF is the force on the band, and L is the length of the band. The force F is afunction of temperature and of length of the band. Replacing P ∆V in Eq. (45.3)by −F ∆L, we get

∆U = ∆Q + F ∆L.

(45.8)

Comparing Eqs. (45.3) and (45.8), we see that the rubber band equation isobtained by a mere substitution of one letter for another. Furthermore, if wesubstitute L for V , and −F for P, all of our discussion of the Carnot cycleapplies to the rubber band. We can immediately deduce, for instance, that theheat ∆Q needed to change the length by ∆L is given by the analog to Eq. (45.5):∆Q = −T(∂F/∂T)L ∆L. This equation tells us that if we keep the length of arubber band ﬁxed and heat the band, we can calculate how much the force willincrease in terms of the heat needed to keep the temperature constant when theband is relaxed a little bit. So we see that the same equation applies to both gasand a rubber band. In fact, if one can write ∆U = ∆Q + A ∆B, where A and Brepresent diﬀerent quantities, force and length, pressure and volume, etc., one canapply the results obtained for a gas by substituting A and B for −P and V . Forexample, consider the electric potential diﬀerence, or「voltage,」E in a batteryand the charge ∆Z that moves through the battery. We know that the work donein a reversible electric cell, like a storage battery, is E ∆Z. (Since we includeno P ∆V term in the work, we require that our battery maintain a constantvolume.) Let us see what thermodynamics can tell us about the performance of

45-7

a battery. If we substitute E for P and Z for V in Eq. (45.6), we obtain

∆U∆Z

= T

∂T

Z

(cid:18) ∂E

(cid:19)

− E.

(45.9)

Equation (45.9) says that the internal energy U is changed when a charge ∆Zmoves through the cell. Why is ∆U/∆Z not simply the voltage E of the battery?(The answer is that a real battery gets warm when charge moves through thecell. The internal energy of the battery is changed, ﬁrst, because the battery didsome work on the outside circuit, and second, because the battery is heated.)The remarkable thing is that the second part can again be expressed in termsof the way in which the battery voltage changes with temperature. Incidentally,when the charge moves through the cell, chemical reactions occur, and Eq. (45.9)suggests a nifty way of measuring the amount of energy required to producea chemical reaction. All we need to do is construct a cell that works on thereaction, measure the voltage, and measure how much the voltage changes withtemperature when we draw no charge from the battery!

Now we have assumed that the volume of the battery can be maintainedconstant, since we have omitted the P ∆V term when we set the work done by thebattery equal to E ∆Z. It turns out that it is technically quite diﬃcult to keepthe volume constant. It is much easier to keep the cell at constant atmosphericpressure. For that reason, the chemists do not like any of the equations wehave written above: they prefer equations which describe performance underconstant pressure. We chose at the beginning of this chapter to use V and T asindependent variables. The chemists prefer P and T, and we will now considerhow the results we have obtained so far can be transformed into the chemists’system of variables. Remember that in the following treatment confusion caneasily set in because we are shifting gears from T and V to T and P.We started in Eq. (45.3) with ∆U = ∆Q − P ∆V ; P ∆V may be replaced byE ∆Z or A ∆B. If we could somehow replace the last term, P ∆V , by V ∆P,then we would have interchanged V and P, and the chemists would be happy.Well, a clever man noticed that the diﬀerential of the product P V is d(P V ) =P dV + V dP, and if he added this equality to Eq. (45.3), he obtained

∆(P V ) = P ∆V + V ∆P∆U = ∆Q − P ∆V∆(U + P V ) = ∆Q + V ∆P

45-8

In order that the result look like Eq. (45.3), we deﬁne U + P V to be somethingnew, called the enthalpy, H, and we write ∆H = ∆Q + V ∆P.Now we are ready to transform our results into chemists’ language with thefollowing rules: U → H, P → −V , V → P. For example, the fundamentalrelationship that chemists would use instead of Eq. (45.7) is

(cid:18) ∂H

(cid:19)

∂P

T

(cid:18) ∂V

(cid:19)

∂T

P

= −T

+ V.

It should now be clear how one transforms to the chemists’ variables T and P.We now go back to our original variables: for the remainder of this chapter, Tand V are the independent variables.

Now let us apply the results we have obtained to a number of physicalsituations. Consider ﬁrst the ideal gas. From kinetic theory we know that theinternal energy of a gas depends only on the motion of the molecules and thenumber of molecules. The internal energy depends on T, but not on V . If wechange V , but keep T constant, U is not changed. Therefore (∂U/∂V )T = 0, andEq. (45.7) tells us that for an ideal gas

(cid:18) ∂P

(cid:19)

∂T

V

T

− P = 0.

(45.10)

Equation (45.10) is a diﬀerential equation that can tell us something about P.We take account of the partial derivatives in the following way: Since the partialderivative is at constant V , we will replace the partial derivative by an ordinaryderivative and write explicitly, to remind us,「constant V .」Equation (45.10) thenbecomes

∆P∆Twhich we can integrate to get

T

− P = 0;

const V ,

ln P = ln T + const;

P = const × T;

const V ,const V .

We know that for an ideal gas the pressure per mole is equal to

P = RTV

,

45-9

(45.11)

(45.12)

(45.13)

which is consistent with (45.12), since V and R are constants. Why did webother to go through this calculation if we already knew the results? Becausewe have been using two independent deﬁnitions of temperature! At one stagewe assumed that the kinetic energy of the molecules was proportional to thetemperature, an assumption that deﬁnes one scale of temperature which we willcall the ideal gas scale. The T in Eq. (45.13) is based on the gas scale. Wealso call temperatures measured on the gas scale kinetic temperatures. Later,we deﬁned the temperature in a second way which was completely independentof any substance. From arguments based on the Second Law we deﬁned whatwe might call the「grand thermodynamic absolute temperature」T, the T thatappears in Eq. (45.12). What we proved here is that the pressure of an ideal gas(deﬁned as one for which the internal energy does not depend on the volume) isproportional to the grand thermodynamic absolute temperature. We also knowthat the pressure is proportional to the temperature measured on the gas scale.Therefore we can deduce that the kinetic temperature is proportional to the「grand thermodynamic absolute temperature.」That means, of course, that if wewere sensible we could make two scales agree. In this instance, at least, the twoscales have been chosen so that they coincide; the proportionality constant hasbeen chosen to be 1. Most of the time man chooses trouble for himself, but inthis case he made them equal!

45-3 The Clausius-Clapeyron equationThe vaporization of a liquid is another application of the results we havederived. Suppose we have some liquid in a cylinder, such that we can compressit by pushing on the piston, and we ask ourselves,「If we keep the temperatureconstant, how does the pressure vary with volume?」In other words, we wantto draw an isothermal line on the P-V diagram. The substance in the cylinderis not the ideal gas that we considered earlier; now it may be in the liquid orthe vapor phase, or both may be present. If we apply suﬃcient pressure, thesubstance will condense to a liquid. Now if we squeeze still harder, the volumechanges very little, and our isothermal line rises rapidly with decreasing volume,as shown at the left in Fig. 45-3.

If we increase the volume by pulling the piston out, the pressure drops untilwe reach the point at which the liquid starts to boil, and then vapor starts to form.If we pull the piston out farther, all that happens is that more liquid vaporizes.When there is part liquid and part vapor in the cylinder, the two phases are in

45-10

Fig. 45-3. Isothermal lines for a condensable vapor compressed in acylinder. At the left, the substance is in the liquid phase. At the right,the substance is vaporized. In the center, both liquid, and vapor arepresent in the cylinder.

Fig. 45-4. Pressure-volume diagram for a Carnot cycle with a con-densable vapor in the cylinder. At the left, the substance is in the liquidstate. A quantity of heat L is added at temperature T to vaporize theliquid. The vapor expands adiabatically as T changes to T − ∆T .

45-11

equilibrium—liquid is evaporating and vapor is condensing at the same rate. Ifwe make more room for the vapor, more vapor is needed to maintain the pressure,so a little more liquid evaporates, but the pressure remains constant. On the ﬂatpart of the curve in Fig. 45-3 the pressure does not change, and the value of thepressure here is called the vapor pressure at temperature T. As we continue toincrease the volume, there comes a time when there is no more liquid to evaporate.At this juncture, if we expand the volume further, the pressure will fall as foran ordinary gas, as shown at the right of the P-V diagram. The lower curve inFig. 45-3 is the isothermal line at a slightly lower temperature T − ∆T. Thepressure in the liquid phase is slightly reduced because liquid expands with anincrease in temperature (for most substances, but not for water near the freezingpoint) and, of course, the vapor pressure is lower at the lower temperature.

We will now make a cycle out of the two isothermal lines by connectingthem (say by adiabatic lines) at both ends of the upper ﬂat section, as shown inFig. 45-4. We are going to use the argument of Carnot, which tells us that theheat added to the substance in changing it from a liquid to a vapor is relatedto the work done by the substance as it goes around the cycle. Let us call Lthe heat needed to vaporize the substance in the cylinder. As in the argumentimmediately preceding Eq. (45.5), we know that L(∆T /T) = work done by thesubstance. As before, the work done by the substance is the shaded area, which isapproximately ∆P(VG − VL), where ∆P is the diﬀerence in vapor pressure at thetwo temperatures T and T −∆T, VG is the volume of the gas, and VL is the volumeof the liquid, both volumes measured at the vapor pressure at temperature T.Setting these two expressions for the area equal, we get L ∆T /T = ∆P(VG − VL),or

L

T(VG − VL) = (∂Pvap/∂T).

(45.14)

Equation (45.14) gives the relationship between the rate of change of vaporpressure with temperature and the amount of heat required to evaporate theliquid. This relationship was deduced by Carnot, but it is called the Clausius-Clapeyron equation.

Now let us compare Eq. (45.14) with the results deduced from kinetic theory.Usually VG is very much larger than VL. So VG − VL ≈ VG = RT /P per mole. Ifwe further assume that L is a constant, independent of temperature—not a verygood approximation—then we would have ∂P/∂T = L/(RT 2/P). The solution

45-12

of this diﬀerential equation is

P = const e−L/RT .

(45.15)

(cid:18) 1

(cid:19)

Va

Let us compare this with the pressure variation with temperature that we deducedearlier from kinetic theory. Kinetic theory indicated the possibility, at leastroughly, that the number of molecules per unit volume of vapor above a liquidwould be

n =

e−(UG−UL)/RT ,

(45.16)where UG − UL is the internal energy per mole in the gas minus the internalenergy per mole in the liquid, i.e., the energy needed to vaporize a mole ofliquid. Equation (45.15) from thermodynamics and Eq. (45.16) from kinetictheory are very closely related because the pressure is nkT, but they are notexactly the same. However, they will turn out to be exactly the same if weassume UG − UL = const, instead of L = const. If we assume UG − UL = const,independent of temperature, then the argument leading to Eq. (45.15) willproduce Eq. (45.16). Since the pressure is constant while the volume is changing,the change in internal energy UG − UL is equal to the heat L put in minus thework done P(VG − VL), so L = (UG + P VG) − (UL + P VL).This comparison shows the advantages and disadvantages of thermodynamicsover kinetic theory: First of all, Eq. (45.14) obtained by thermodynamics isexact, while Eq. (45.16) can only be approximated, for instance, if U is nearlyconstant, and if the model is right. Second, we may not understand correctlyhow the gas goes into the liquid; nevertheless, Eq. (45.14) is right, while (45.16)is only approximate. Third, although our treatment applies to a gas condensinginto a liquid, the argument is true for any other change of state. For instance,the solid-to-liquid transition has the same kind of curve as that shown in Figs.45-3 and 45-4. Introducing the latent heat for melting, M/mole, the formulaanalogous to Eq. (45.14) then is (∂Pmelt/∂T)V = M/[T(Vliq − Vsolid)]. Althoughwe may not understand the kinetic theory of the melting process, we neverthelesshave a correct equation. However, when we can understand the kinetic theory,we have another advantage. Equation (45.14) is only a diﬀerential relationship,and we have no way of obtaining the constants of integration. In the kinetictheory we can obtain the constants also if we have a good model that describesthe phenomenon completely. So there are advantages and disadvantages toeach. When knowledge is weak and the situation is complicated, thermodynamic

45-13

relations are really the most powerful. When the situation is very simple and atheoretical analysis can be made, then it is better to try to get more informationfrom theoretical analysis.

One more example: blackbody radiation. We have discussed a box containingradiation and nothing else. We have talked about the equilibrium between theoscillator and the radiation. We also found that the photons hitting the wall ofthe box would exert the pressure P, and we found P V = U/3, where U is thetotal energy of all the photons and V is the volume of the box. If we substituteU = 3P V in the basic Eq. (45.7), we ﬁnd*

(cid:18) ∂U

(cid:19)

∂V

T

(cid:18) ∂P

(cid:19)

∂T

V

= 3P = T

− P.

(45.17)

Since the volume of our box is constant, we can replace (∂P/∂T)V by dP/dT toobtain an ordinary diﬀerential equation we can integrate: ln P = 4 ln T + const,or P = const × T 4. The pressure of radiation varies as the fourth power of thetemperature, and the total energy density of the radiation, U/V = 3P, alsovaries as T 4. It is usual to write U/V = (4σ/c)T 4, where c is the speed of lightand σ is called the Stefan-Boltzmann constant. It is not possible to get σ fromthermodynamics alone. Here is a good example of its power, and its limitations.To know that U/V goes as T 4 is a great deal, but to know how big U/V actuallyis at any temperature requires that we go into the kind of detail that only acomplete theory can supply. For blackbody radiation we have such a theory andwe can derive an expression for the constant σ in the following manner.Let I(ω) dω be the intensity distribution, the energy ﬂow through 1 m2in one second with frequency between ω and ω + dω. The energy densitydistribution = energy/volume = I(ω) dω/c is

= total energy density

UV

Z ∞

ω=0

=

energy density between ω and ω + dω

* In this case (∂P/∂V )T = 0, because in order to keep the oscillator in equilibrium at agiven temperature, the radiation in the neighborhood of the oscillator has to be the same,regardless of the volume of the box. The total quantity of photons inside the box must thereforebe proportional to its volume, so the internal energy per unit volume, and thus the pressure,depends only on the temperature.

45-14

Z ∞

0

=

I(ω) dω

c

.

From our earlier discussions, we know that

I(ω) =

ω3

π2c2(eω/kT − 1) .

UV

= 1π2c3

ω3 dωeω/kT − 1 .If we substitute x = ω/kT, the expression becomesx3 dxex − 1 .

= (kT)43π2c3

Z ∞

UV

0

Substituting this expression for I(ω) in our equation for U/V , we get

Z ∞

0

This integral is just some number that we can get, approximately, by drawinga curve and taking the area by counting squares. It is roughly 6.5. The math-ematicians among us can show that the integral is exactly π4/15.* Comparingthis expression with U/V = (4σ/c)T 4, we ﬁnd

σ = k4π2603c3

= 5.67 × 10−8

watts

(meter)2(degree)4 .

If we make a small hole in our box, how much energy will ﬂow per secondthrough the hole of unit area? To go from energy density to energy ﬂow, wemultiply the energy density U/V by c. We also multiply by 14, which arises2, because only the energy which is ﬂowing outas follows: ﬁrst, a factor of 1∞X

* Since (ex − 1)−1 = e−x + e−2x + · · · , the integral is

ButR ∞0 e−nx dx = 1/n, and diﬀerentiating with respect to n three times givesR ∞

0 x3e−nx dx =81 + · · · ) and a good estimate comes from adding the ﬁrst6/n4, so the integral is 6(1 + 1few terms. In Chapter 50 we will ﬁnd a way to show that the sum of the reciprocal fourthpowers of the integers is, in fact, π4/90.

Z ∞

e−nxx3 dx.

16 + 1

n=1

0

45-15

escapes; and second, another factor 12, because energy which approaches thehole at an angle to the normal is less eﬀective in getting through the hole by acosine factor. The average value of the cosine is 12. It is clear now why we writeU/V = (4σ/c)T 4: so that we can ultimately say that the ﬂux from a small holeis σT 4 per unit area.

45-16

46

