Applications of Kinetic Theory

42-1 Evaporation In this chapter we shall discuss some further applications of kinetic theory. In the previous chapter we emphasized one particular aspect of kinetic theory, namely, that the average kinetic energy in any degree of freedom of a molecule or other object is 1 2 kT. The central feature of what we shall now discuss, on the other hand, is the fact that the probability of ﬁnding a particle in diﬀerent places, per unit volume, varies as e−potential energy/kT ; we shall make a number of applications of this. The phenomena which we want to study are relatively complicated: a liquid evaporating, or electrons in a metal coming out of the surface, or a chemical reaction in which there are a large number of atoms involved. In such cases it is no longer possible to make from the kinetic theory any simple and correct statements, because the situation is too complicated. Therefore, this chapter, except where otherwise emphasized, is quite inexact. The idea to be emphasized is only that we can understand, from the kinetic theory, more or less how things ought to behave. By using thermodynamic arguments, or some empirical measurements of certain critical quantities, we can get a more accurate representation of the phenomena.

However, it is very useful to know even only more or less why something behaves as it does, so that when the situation is a new one, or one that we have not yet started to analyze, we can say, more or less, what ought to happen. So this discussion is highly inaccurate but essentially right—right in idea, but a little bit simpliﬁed, let us say, in the speciﬁc details.

The ﬁrst example that we shall consider is the evaporation of a liquid. Suppose we have a box with a large volume, partially ﬁlled with liquid in equilibrium and with the vapor at a certain temperature. We shall suppose that the molecules of the vapor are relatively far apart, and that inside the liquid, the molecules are

42-1

packed close together. The problem is to ﬁnd out how many molecules there are in the vapor phase, compared with the number there are in the liquid. How dense is the vapor at a given temperature, and how does it depend on the temperature? Let us say that n equals the number of molecules per unit volume in the vapor. That number, of course, varies with the temperature. If we add heat, we get more evaporation. Now let another quantity, 1/Va, equal the number of atoms per unit volume in the liquid: We suppose that each molecule in the liquid occupies a certain volume, so that if there are more molecules of liquid, then all together they occupy a bigger volume. Thus if Va is the volume occupied by one molecule, the number of molecules in a unit volume is a unit volume divided by the volume of each molecule. Furthermore, we suppose that there is a force of attraction between the molecules to hold them together in the liquid. Otherwise we cannot understand why it condenses. Thus suppose that there is such a force and that there is an energy of binding of the molecules in the liquid which is lost when they go into the vapor. That is, we are going to suppose that, in order to take a single molecule out of the liquid into the vapor, a certain amount of work W has to be done. There is a certain diﬀerence, W, in the energy of a molecule in the liquid from what it would have if it were in the vapor, because we have to pull it away from the other molecules which attract it.

Now we use the general principle that the number of atoms per unit volume in two diﬀerent regions is n2/n1 = e−(E2−E1)/kT . So the number n per unit volume in the vapor, divided by the number 1/Va per unit volume in the liquid, is equal to

nVa = e−W/kT ,

(42.1) because that is the general rule. It is like the atmosphere in equilibrium under gravity, where the gas at the bottom is denser than that at the top because of the work mgh needed to lift the gas molecules to the height h. In the liquid, the molecules are denser than in the vapor because we have to pull them out through the energy「hill」W, and the ratio of the densities is e−W/kT .

This is what we wanted to deduce—that the vapor density varies as e to the minus some energy or other over kT. The factors in front are not really interesting to us, because in most cases the vapor density is very much lower than the liquid density. In those circumstances, where we are not near the critical point where they are almost the same, but where the vapor density is much lower than the liquid density, then the fact that n is very much less than 1/Va is occasioned by the fact that W is very much greater than kT. So formulas such as (42.1)

42-2

are interesting only when W is very much bigger than kT, because in those circumstances, since we are raising e to minus a tremendous amount, if we change T a little bit, that tremendous power changes a bit, and the change produced in the exponential factor is very much more important than any change that might occur in the factors out in front. Why should there be any changes in such factors as Va? Because ours was an approximate analysis. After all, there is not really a deﬁnite volume for each molecule; as we change the temperature, the volume Va does not stay constant—the liquid expands. There are other little features like that, and so the actual situation is more complicated. There are slowly varying temperature-dependent factors all over the place. In fact, we might say that W itself varies slightly with temperature, because at a higher temperature, at a diﬀerent molecular volume, there would be diﬀerent average attractions, and so on. So, while we might think that if we have a formula in which everything varies in an unknown way with temperature then we have no formula at all, if we realize that the exponent W/kT is, in general, very large, we see that in the curve of the vapor density as a function of temperature most of the variation is occasioned by the exponential factor, and if we take W as a constant and the coeﬃcient 1/Va as nearly constant, it is a good approximation for short intervals along the curve. Most of the variation, in other words, is of the general nature e−W/kT . It turns out that there are many, many phenomena in nature which are characterized by having to borrow an energy from somewhere, and in which the central feature of the temperature variation is e to the minus the energy over kT. This is a useful fact only when the energy is large compared with kT, so that most of the variation is contained in the variation of the kT and not in the constant and in other factors. Now let us consider another way of obtaining a somewhat similar result for the evaporation, but looking at it in more detail. To arrive at (42.1), we simply applied a rule which is valid at equilibrium, but in order to understand things better, there is no harm in trying to look at the details of what is going on. We may also describe what is going on in the following way: the molecules that are in the vapor continually bombard the surface of the liquid; when they hit it, they may bounce oﬀ or they may get stuck. There is an unknown factor for that—maybe 50–50, maybe 10 to 90—we do not know. Let us say they always get stuck—we can analyze it over again later on the assumption that they do not always get stuck. Then at a given moment there will be a certain number of atoms which are condensing onto the surface of the liquid. The number of condensing molecules, the number that arrive on a unit area per unit time, is the

42-3

number n per unit volume times the velocity v. This velocity of the molecules is related to the temperature, because we know that 1 2 kT on the average. So v is some kind of a mean velocity. Of course we should integrate over the angles and get some kind of an average, but it is roughly proportional to the root-mean-square velocity, within some factor. Thus

2 mv2 is equal to 3

Nc = nv

(42.2)

is the rate at which the molecules arrive per unit area and are condensing.

At the same time, however, the atoms in the liquid are jiggling about, and from time to time one of them gets kicked out. Now we have to estimate how fast they get kicked out. The idea will be that at equilibrium the number that are kicked out per second and the number that arrive per second are equal.

How many get kicked out? In order to get kicked out, a particular molecule has to have acquired by accident an excess energy over its neighbors—a considerable excess energy, because it is attracted very strongly by the other molecules in the liquid. Ordinarily it does not leave because it is so strongly attracted, but in the collisions sometimes one of them gets an extra energy by accident. And the chance that it gets the extra energy W which it needs in our case is very small if W (cid:29) kT. In fact, e−W/kT is the chance that an atom has picked up more than this much energy. That is the general principle in kinetic theory: in order to borrow an excess energy W over the average, the odds are e to the minus the energy that we have to borrow, over kT. Now suppose that some molecules have borrowed this energy. We now have to estimate how many leave the surface per second. Of course, just because a molecule has the necessary energy does not mean that it will actually evaporate, since it may be buried too deeply inside the liquid or, even if it is near the surface, it may be travelling in the wrong direction. The number that are going to leave a unit area per second is going to be something like this: the number of atoms there are near the surface, per unit area, divided by the time it takes one to escape, multiplied by the probability e−W/kT that they are ready to escape in the sense that they have enough energy.

We shall suppose that each molecule at the surface of the liquid occupies a certain cross-sectional area A. Then the number of molecules per unit area of liquid surface will be 1/A. And now, how long does it take a molecule to escape? If the molecules have a certain average speed v, and have to move, say, one molecular diameter D, the thickness of the ﬁrst layer, then the time it takes

42-4

to get across that thickness is the time needed to escape, if the molecule has enough energy. The time will be D/v. Thus the number evaporating should be approximately (42.3) Now the area of each atom times the thickness of the layer is approximately the same as the volume Va occupied by a single atom. And so, in order to get equilibrium, we must have Nc = Ne, or

Ne = (1/A)(v/D)e−W/kT .

nv = (v/Va)e−W/kT .

(42.4) We may cancel the v’s, since they are equal; even though one is the velocity of a molecule in the vapor and the other is the velocity of an evaporating molecule, these are the same, because we know their mean kinetic energy (in one direction) 2 kT. But one may object,「No! No! These are the especially fast-moving ones; is 1 these are the ones that have picked up excess energy.」Not really, because the moment they start to pull away from the liquid, they have to lose that excess energy against the potential energy. So, as they come to the surface they are slowed down to the velocity v! It is the same as it was in our discussion of the distribution of molecular velocities in the atmosphere—at the bottom, the molecules had a certain distribution of energy. The ones that arrive at the top have the same distribution of energy, because the slow ones did not arrive at all, and the fast ones were slowed down. The molecules that are evaporating have the same distribution of energy as the ones inside—a rather remarkable fact. Anyway, it is useless to try to argue so closely about our formula because of other inaccuracies, such as the probability of bouncing back rather than entering the liquid, and so on. Thus we have a rough idea of the rate of evaporation and condensation, and we see, of course, that the vapor density n varies in the same way as before, but now we have understood it in some detail rather than just as an arbitrary formula.

This deeper understanding permits us to analyze some things. For example, suppose that we were to pump away the vapor at such a great rate that we removed the vapor as fast as it formed (if we had very good pumps and the liquid was evaporating very slowly), how fast would evaporation occur if we maintained a liquid temperature T? Suppose that we have already experimentally measured the equilibrium vapor density, so that we know, at the given temperature, how many molecules per unit volume are in equilibrium with the liquid. Now we would like to know how fast it will evaporate. Even though we have used only a

42-5

rough analysis so far as the evaporation part of it is concerned, the number of vapor molecules arriving was not done so badly, aside from the unknown factor of reﬂection coeﬃcient. So therefore we may use the fact that the number that are leaving, at equilibrium, is the same as the number that arrive. True, the vapor is being swept away and so the molecules are only coming out, but if the vapor were left alone, it would attain the equilibrium density at which the number that come back would equal the number that are evaporating. Therefore, we can easily see that the number that are coming oﬀ the surface per second is equal to the unknown reﬂection coeﬃcient R times the number that would come down to the surface per second were the vapor still there, because that is how many would balance the evaporation at equilibrium:

Ne = nvR = (vR/Va)e−W/kT .

(42.5)

Of course, the number of molecules that hit the liquid from the vapor is easy to calculate, since we do not need to know as much about the forces as we do when we are worrying about how they get to escape through the liquid surface; it is much easier to make the argument the other way.

42-2 Thermionic emission We may give another example of a very practical situation that is similar to the evaporation of a liquid—so similar that it is not worth making a separate analysis. It is essentially the same problem. In a radio tube there is a source of electrons, namely a heated tungsten ﬁlament, and a positively charged plate to attract the electrons. Any electron that escapes from the surface of the tungsten is immediately swept away to the plate. That is our ideal「pump,」which is「pumping」the electrons away all the time. Now the question is: How many electrons per second can we get out of a piece of tungsten, and how does that number vary with temperature? The answer to that problem is the same as (42.5), because it turns out that in a piece of metal, electrons are attracted to the ions, or to atoms, of the metal. They are attracted, if we may say it crudely, to the metal. In order to get an electron out of a piece of metal, it takes a certain amount of energy or work to pull it out. This work varies with the diﬀerent kinds of metal. In fact, it varies even with the character of the surface of a given kind of metal, but the total work may be a few electron volts, which, incidentally, is typical of the energy involved in chemical reactions. We can remember the latter

42-6

fact by remembering that the voltage in a chemical cell like a ﬂashlight battery, which is produced by chemical reactions, is about one volt.

How can we ﬁnd out how many electrons come out per second? It would be quite diﬃcult to analyze the eﬀects on the electrons going out; it is easier to analyze the situation the other way. So, we could start out by imagining that we did not draw the electrons away, and that the electrons were like a gas, and could come back to the metal. Then there would be a certain density of electrons at equilibrium which would, of course, be given by exactly the same formula as (42.1), where Va is the volume per electron in the metal, roughly, and W is equal to qeφ, where φ is the so-called work function, or the voltage needed to pull an electron oﬀ the surface. This would tell us how many electrons would have to be in the surrounding space and striking the metal in order to balance the ones that are coming out. And thus it is easy to calculate how many are coming out if we sweep away all of them, because the number that are coming out is exactly equal to the number that would be going in with the above density of electron「vapor.」In other words, the answer is that the current of electricity that comes in per unit area is equal to the charge on each times the number that arrive per second per unit area, which is the number per unit volume times the velocity, as we have seen many times:

I = qenv = (qev/Va)e−qeφ/kT .

(42.6) Now one electron volt corresponds to kT at a temperature of 11,600 degrees. The ﬁlament of the tube may be operating at a temperature of, say, 1100 degrees, so the exponential factor is something like e−10; when we change the temperature a little bit, the exponential factor changes a lot. Thus, again, the central feature of the formula is the e−qeφ/kT . As a matter of fact, the factor in front is quite wrong—it turns out that the behavior of electrons in a metal is not correctly described by the classical theory, but by quantum mechanics, but this only changes the factor in front a little. Actually, no one has ever been able to get the thing straightened out very well, even though many people have used the high-class quantum-mechanical theory for their calculations. The big problem is, does W change slightly with temperature? If it does, one cannot distinguish a W changing slowly with temperature from a diﬀerent coeﬃcient in front. That is, if W changed linearly, say, with temperature, so that W = W0 + αkT, then we would have

e−W/kT = e−(W0+αkT )/kT = e−αe−W0/kT .

42-7

Thus a linearly temperature-dependent W is equivalent to a shifted「constant.」It is really quite diﬃcult and usually fruitless to try to obtain the coeﬃcient in the front accurately.

42-3 Thermal ionization Now we go on to another example of the same idea; always the same idea. This has to do with ionization. Suppose that in a gas we have a whole lot of atoms which are in the neutral state, say, but the gas is hot and the atoms can become ionized. We would like to know how many ions there are in a given circumstance if we have a certain density of atoms per unit volume at a certain temperature. Again we consider a box in which there are N atoms which can hold electrons. (If an electron has come oﬀ an atom, it is called an ion, and if the atom is neutral, we simply call it an atom.) Then suppose that, at any given moment, the number of neutral atoms is na, the number of ions is ni, and the number of electrons is ne, all per unit volume. The problem is: What is the relationship of these three numbers? In the ﬁrst place, we have two conditions or constraints on the numbers. For instance, as we vary diﬀerent conditions, like the temperature and so on, na + ni would remain constant, because this would be simply the number N of atomic nuclei that are in the box. If we keep the number of nuclei per unit volume ﬁxed, and change, say, the temperature, then as the ionization proceeded some atoms would turn to ions, but the total number of atoms plus ions would be unchanged. That is, na + ni = N. Another condition is that if the entire gas is to be electrically neutral (and if we neglect double or triple ionization), that means that the number of ions is equal to the number of electrons at all times, or ni = ne. These are subsidiary equations that simply express the conservation of charge and the conservation of atoms. These equations are true, and we ultimately will use them when we consider a real problem. But we want to obtain another relationship between the quantities. We can do this as follows. We again use the idea that it takes a certain amount of energy to lift the electron out of the atom, which we call the ionization energy, and we would write it as W, in order to make all of the formulas look the same. So we let W equal the energy needed to pull an electron out of an atom and make an ion. Now we again say that the number of free electrons per unit volume in the「vapor」is equal to the number of bound electrons per unit volume in the atoms, times e to the minus the energy diﬀerence between being bound and

42-8

being free, over kT. That is the basic equation again. How can we write it? The number of free electrons per unit volume would, of course, be ne, because that is the deﬁnition of ne. Now what about the number of electrons per unit volume that are bound to atoms? The total number of places that we could put the electrons is apparently na + ni, and we will suppose that when they are bound each one is bound within a certain volume Va. So the total amount of volume which is available to electrons which would be bound is (na + ni)Va, so we might want to write our formula as

ne =

na

(na + ni)Va

e−W/kT .

The formula is wrong, however, in one essential feature, which is the following: when an electron is already on an atom, another electron cannot come to that volume anymore! In other words, all the volumes of all the possible sites are not really available for the one electron which is trying to make up its mind whether or not to be in the vapor or in the condensed position, because in this problem there is an extra feature that when one electron is where another electron is, it is not allowed to go—it is repelled. For that reason, it comes out that we should count only that part of the volume which is available for an electron to sit on or not. That is, those which are already occupied do not count in the total available volume, but the only volume which is allowed is that of the ions, where there are vacant places for the electron to go. Then, in those circumstances, we ﬁnd that a nicer way to write our formula is

neni na

= 1 Va

e−W/kT .

(42.7)

This formula is called the Saha ionization equation. Now let us see if we can understand qualitatively why a formula like this is right, by arguing about the kinetic things that are happening.

First, every once in a while an electron comes to an ion and they combine to make an atom. And also, every once in a while, an atom gets into a collision and breaks up into an ion and an electron. Now those two rates must be equal. How fast do electrons and ions ﬁnd each other? The rate is certainly increased if the number of electrons per unit volume is increased. It is also increased if the number of ions per unit volume is increased. That is, the total rate at which recombination is occurring is certainly proportional to the number of electrons times the number of ions. Now the total rate at which ionization is occurring

42-9

due to collisions must be dependent linearly on how many atoms there are to ionize. And so the rates will balance when there is some relationship between the product neni and the number of atoms, na. The fact that this relationship happens to be given by this particular formula, where W is the ionization energy, is of course a little bit more information, but we can easily understand that the formula would necessarily involve the concentrations of the electrons, ions, and atoms in the combination neni/na to produce a constant independent of the n’s, and dependent only on temperature, the atomic cross sections, and other constant factors.

We may also note that, since the equation involves the numbers per unit volume, if we were to do two experiments with a given total number N of atoms plus ions, that is, a certain ﬁxed number of nuclei, but using boxes with diﬀerent volumes, the n’s would all be smaller in the larger box. But since the ratio neni/na stays the same, the total number of electrons and ions must be greater in the larger box. To see this, suppose that there are N nuclei inside a box of volume V , and that a fraction f of them are ionized. Then ne = f N/V = ni, and na = (1 − f)N/V . Then our equation becomes

f 2 1 − f

N V

= e−W/kT Va

.

(42.8)

In other words, if we take a smaller and smaller density of atoms, or make the volume of the container bigger and bigger, the fraction f of electrons and ions must increase. That ionization, just from「expansion」as the density goes down, is the reason why we believe that at very low densities, such as in the cold space between the stars, there may be ions present, even though we might not understand it from the point of view of the available energy. Although it takes many, many kT of energy to make them, there are ions present.

Why can there be ions present when there is so much space around, while if we increase the density, the ions tend to disappear? Answer: Consider an atom. Every once in a while, light, or another atom, or an ion, or whatever it is that maintains thermal equilibrium, strikes it. Very rarely, because it takes such a terriﬁc amount of excess energy, an electron comes oﬀ and an ion is left. Now that electron, if the space is enormous, wanders and wanders and does not come near anything for years, perhaps. But once in a very great while, it does come back to an ion and they combine to make an atom. So the rate at which electrons are coming out from the atoms is very slow. But if the volume is enormous, an

42-10

electron which has escaped takes so long to ﬁnd another ion to recombine with that its probability of recombination is very, very small; thus, in spite of the large excess energy needed, there may be a reasonable number of electrons.

nAnB nAB

= ce−W/kT .

42-4 Chemical kinetics The same situation that we have just called「ionization」is also found in a chemical reaction. For instance, if two objects A and B combine into a compound AB, then if we think about it for a while we see that AB is what we have called an atom, B is what we call an electron, and A is what we call an ion. With these substitutions the equations of equilibrium are exactly the same in form:

(42.9) This formula, of course, is not exact, since the「constant」c depends on how much volume is allowed for the A and B to combine, and so on, but by thermodynamic arguments one can identify what the meaning of the W in the exponential factor is, and it turns out that it is very close to the energy needed in the reaction. Suppose that we tried to understand this formula as a result of collisions, much in the way that we understood the evaporation formula, by arguing about how many electrons came oﬀ and how many of them came back per unit time. Suppose that A and B combine in a collision every once in a while to form a compound AB. And suppose that the compound AB is a complicated molecule which jiggles around and is hit by other molecules, and from time to time it gets enough energy to explode and break up again into A and B. Now it actually turns out, in chemical reactions, that if the atoms come together with too small an energy, even though energy may be released in the reaction A + B → AB, the fact that A and B may touch each other does not necessarily make the reaction start. It usually is required that the collision be

Fig. 42-1. The energy relationship for the reaction A + B → AB.

42-11

rather hard, in fact, to get the reaction to go at all—a「soft」collision between A and B may not do it, even though energy may be released in the process. So let us suppose that it is very common in chemical reactions that, in order for A and B to form AB, they cannot just hit each other, but they have to hit each other with suﬃcient energy. This energy is called the activation energy—the energy needed to「activate」the reaction. Call A∗ the activation energy, the excess energy needed in a collision in order that the reaction may really occur. Then the rate Rf at which A and B produce AB would involve the number of atoms of A times the number of atoms of B, times the rate at which a single atom would strike a certain cross section σAB, times a factor e−A∗/kT which is the probability that they have enough energy:

Rf = nAnBvσABe−A∗/kT .

(42.10) Now we have to ﬁnd the opposite rate, Rr. There is a certain chance that AB will ﬂy apart. In order to ﬂy apart, it not only must have the energy W which it needs in order to get apart at all but, just as it was hard for A and B to come together, so there is a kind of hill that A and B have to climb over to get apart again; they must have not only enough energy just to get ready to pull apart, but a certain excess. It is like climbing a hill to get into a deep valley; they have to climb the hill coming in and they have to climb out of the valley and then over the hill coming back (Fig. 42-1). Thus the rate at which AB goes to A and B will be proportional to the number nAB that are present, times e−(W +A∗)/kT : (42.11) The c0 will involve the volume of atoms and the rate of collisions, which we can work out, as we did the case of evaporation, with areas and times and thicknesses; but we shall not do this. The main feature of interest to us is that when these two rates are equal, the ratio of them is equal to unity. This tells us that nAnB/nAB = ce−W/kT , as before, where c involves the cross sections, velocities, and other factors independent of the n’s. The interesting thing is that the rate of the reaction also varies as e−const/kT , although the constant is not the same as that which governs the concentrations; the activation energy A∗ is quite diﬀerent from the energy W. W governs the proportions of A, B, and AB that we have in equilibrium, but if we want to know how fast A + B goes to AB, that is not a question of equilibrium, and here a

Rr = c0nABe−(W +A∗)/kT .

42-12

diﬀerent energy, the activation energy, governs the rate of reaction through an exponential factor. Furthermore, A∗ is not a fundamental constant like W. Suppose that at the surface of the wall—or at some other place—A and B could temporarily stick there in such a way that they could combine more easily. In other words, we might ﬁnd a「tunnel」through the hill, or perhaps a lower hill. By the conservation of energy, when we are all ﬁnished we have still made AB out of A and B, so the energy diﬀerence W will be quite independent of the way the reaction occurred, but the activation energy A∗ will depend very much on the way the reaction occurs. This is why the rates of chemical reactions are very sensitive to outside conditions. We can change the rate by putting in a surface of a diﬀerent kind, we can put it in a「diﬀerent barrel」and it will go at a diﬀerent rate, if it depends on the nature of the surface. Or if we put in a third kind of object it may change the rate very much; some things produce enormous changes in rate simply by changing the A∗ a little bit—they are called catalysts. A reaction might practically not occur at all because A∗ is too big at the given temperature, but when we put in this special stuﬀ, the catalyst, then the reaction goes very fast indeed, because A∗ is reduced. Incidentally, there is some trouble with such a reaction, A plus B, making AB, because we cannot conserve both energy and momentum when we try to put two objects together to make one that is more stable. Therefore, we need at least a third object C, so the actual reaction is much more complicated. The forward rate would involve the product nAnBnC, and it might seem that our formula is going wrong, but no! When we look at the rate at which AB goes the other way, we ﬁnd that it also needs to collide with C, so there is an nABnC in the reverse rate; the nC’s cancel out in the formula for the equilibrium concentrations. The law of equilibrium, (42.9), which we ﬁrst wrote down is absolutely guaranteed to be true, no matter what the mechanism of the reaction may be!

42-5 Einstein’s laws of radiation We now turn to an interesting analogous situation having to do with the blackbody radiation law. In the last chapter we worked out the distribution law for the radiation in a cavity the way Planck did, considering the radiation from an oscillator. The oscillator had to have a certain mean energy, and since it was oscillating, it would radiate and would keep pumping radiation into the cavity until it piled up enough radiation to balance the absorption and emission. In

42-13

that way we found that the intensity of radiation at frequency ω was given by the formula

ω3 dω

π2c2(eω/kT − 1) .

I(ω) dω =

(42.12)

This result involved the assumption that the oscillator which was generating the radiation had deﬁnite, equally spaced energy levels. We did not say that light had to be a photon or anything like that. There was no discussion about how, when an atom goes from one level to another, the energy must come out in one unit of energy, ω, in the form of light. Planck’s original idea was that the matter was quantized but not the light: material oscillators cannot take up just any energy, but have to take it in lumps. Furthermore, the trouble with the derivation is that it was partially classical. We calculated the rate of radiation from an oscillator according to classical physics; then we turned around and said,「No, this oscillator has a lot of energy levels.」So gradually, in order to ﬁnd the right result, the completely quantum-mechanical result, there was a slow development which culminated in the quantum mechanics of 1927. But in the meantime, there was an attempt by Einstein to convert Planck’s viewpoint that only oscillators of matter were quantized, to the idea that light was really photons and could be considered in a certain way as particles with energy ω. Furthermore, Bohr had pointed out that any system of atoms has energy levels, but they are not necessarily equally spaced like Planck’s oscillator. And so it became necessary to rederive or at least rediscuss the radiation law from a more completely quantum-mechanical viewpoint.

Einstein assumed that Planck’s ﬁnal formula was right, and he used that formula to obtain some new information, previously unknown, about the inter- action of radiation with matter. His discussion went as follows: Consider any two of the many energy levels of an atom, say the mth level and the nth level (Fig. 42-2). Now Einstein proposed that when such an atom has light of the right frequency shining on it, it can absorb that photon of light and make a transition from state n to state m, and that the probability that this occurs per second

Fig. 42-2. Transitions between two energy levels of an atom.

42-14

depends upon the two levels, of course, but is proportional to how intense the light is that is shining on it. Let us call the proportionality constant Bnm, merely to remind us that this is not a universal constant of nature, but depends on the particular pair of levels: some levels are easy to excite; some levels are hard to excite. Now what is the formula going to be for the rate of emission from m to n? Einstein proposed that this must have two parts to it. First, even if there were no light present, there would be some chance that an atom in an excited state would fall to a lower state, emitting a photon; this we call spontaneous emission. It is analogous to the idea that an oscillator with a certain amount of energy, even in classical physics, does not keep that energy, but loses it by radiation. Thus the analog of spontaneous radiation of a classical system is that if the atom is in an excited state there is a certain probability Amn, which depends on the levels again, for it to go down from m to n, and this probability is independent of whether light is shining on the atom or not. But then Einstein went further, and by comparison with the classical theory and by other arguments, concluded that emission was also inﬂuenced by the presence of light—that when light of the right frequency is shining on an atom, it has an increased rate of emitting a photon that is proportional to the intensity of the light, with a proportionality constant Bmn. Later, if we deduce that this coeﬃcient is zero, then we will have found that Einstein was wrong. Of course we will ﬁnd he was right. Thus Einstein assumed that there are three kinds of processes: an absorption proportional to the intensity of light, an emission proportional to the inten- sity of light, called induced emission or sometimes stimulated emission, and a spontaneous emission independent of light.

Now suppose that we have, in equilibrium at temperature T, a certain number of atoms Nn in the state n and another number Nm in the state m. Then the total number of atoms that are going from n to m is the number that are in the state n times the rate per second that, if one is in n, it goes up to m. So we have a formula for the number that are going from n to m per second:

Rn→m = NnBnmI(ω).

(42.13)

The number that will go from m to n is expressed in the same manner, as the number Nm that are in m, times the chance per second that each one goes down to n. This time our expression is

Rm→n = Nm[Amn + BmnI(ω)].

(42.14)

42-15

Now we shall suppose that in thermal equilibrium the number of atoms going up must equal the number coming down. That is one way, at least, in which the number will be sure to stay constant in each level.* So we take these two rates to be equal at equilibrium. But we have one other piece of information: we know how large Nm is compared with Nn—the ratio of those two is e−(Em−En)/kT . Now Einstein assumed that the only light which is eﬀective in making the transition from n to m is the light which has the frequency corresponding to the energy diﬀerence, so Em − En = ω in all our formulas. Thus

(42.15) Thus if we set the two rates equal: NnBnmI(ω) = Nm[Amn + BmnI(ω)], and

Nm = Nne−ω/kT .

divide by Nm, we get

BnmI(ω)e

ω/kT = Amn + BmnI(ω).

From this equation, we can calculate I(ω). It is simply

I(ω) =

Amn

Bnmeω/kT − Bmn

.

(42.16)

(42.17)

But Planck has already told us that the formula must be (42.12). Therefore we can deduce something: First, that Bnm must equal Bmn, since otherwise we ω/kT − 1). So Einstein discovered some things that he did cannot get the (e not know how to calculate, namely that the induced emission probability and the absorption probability must be equal. This is interesting. And furthermore, in order for (42.17) and (42.12) to agree,

Amn/Bmn

must be

ω3/π2c2.

(42.18) So if we know, for instance, the absorption rate for a given level, we can deduce the spontaneous emission rate and the induced emission rate, or any combination. This is as far as Einstein or anyone else could go using such arguments. To actually compute the absolute spontaneous emission rate or the other rates for any speciﬁc atomic transition, of course, requires a knowledge of the machinery of the atom, called quantum electrodynamics, which was not discovered until eleven years later. This work of Einstein was done in 1916.

* This is not the only way one can arrange to keep the numbers of atoms in the various levels constant, but it is the way it actually works. That every process must, in thermal equilibrium, be balanced by its exact opposite is called the principle of detailed balancing.

42-16

Fig. 42-3. By exciting, say by blue light, a higher state h, which may emit a photon leaving atoms in state m, the number in this state m becomes suﬃciently large to start laser action.

The possibility of induced emission has, today, found interesting applications. If there is light present, it will tend to induce the downward transition. The transition then adds its ω to the available light energy, if there were some atoms sitting in the upper state. Now we can arrange, by some nonthermal method, to have a gas in which the number in the state m is very much greater than the number in the state n. This is far out of equilibrium, and so is not given by the formula e−ω/kT , which is for equilibrium. We can even arrange it so that the number in the upper state is very large, while the number in the lower state is practically zero. Then light which has the frequency corresponding to the energy diﬀerence Em − En will not be strongly absorbed, because there are not many atoms in state n to absorb it. On the other hand, when that light is present, it will induce the emission from this upper state! So, if we had a lot of atoms in the upper state, there would be a sort of chain reaction, in which, the moment the atoms began to emit, more would be caused to emit, and the whole lot of them would dump down together. This is what is called a laser, or, in the case of the far infrared, a maser.

Various tricks can be used to obtain the atoms in state m. There may be higher levels to which the atoms can get if we shine in a strong beam of light of high frequency. From these high levels, they may trickle down, emitting various photons, until they all get stuck in the state m. If they tend to stay in the state m without emitting, the state is called metastable. And then they are all dumped down together by induced emissions. One more technical point—if we put this system in an ordinary box, it would radiate in so many diﬀerent directions spontaneously, compared with the induced eﬀect, that we would still be in trouble. But we can enhance the induced eﬀect, increase its eﬃciency, by

42-17

putting nearly perfect mirrors on each side of the box, so that the light which is emitted gets another chance, and another chance, and another chance, to induce more emission. Although the mirrors are almost one hundred percent reﬂecting, there is a slight amount of transmission of the mirror, and a little light gets out. In the end, of course, from the conservation of energy, all the light goes out in a nice uniform straight direction which makes the strong light beams that are possible today with lasers.

42-18

43

