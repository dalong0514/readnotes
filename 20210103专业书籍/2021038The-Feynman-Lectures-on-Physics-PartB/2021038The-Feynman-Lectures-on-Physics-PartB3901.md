19-1 A special lecture—almost verbatim*「When

I was in high school, my physics teacher—whose name was Mr. Bader—called me down one day after physics class and said, ‘You look bored; I wantto tell you something interesting.’ Then he told me something which I foundabsolutely fascinating, and have, since then, always found fascinating. Everytime the subject comes up, I work on it. In fact, when I began to prepare thislecture I found myself making more analyses on the thing. Instead of worryingabout the lecture, I got involved in a new problem. The subject is this—theprinciple of least action.

「Mr. Bader told me the following: Suppose you have a particle (in a gravita-tional ﬁeld, for instance) which starts somewhere and moves to some other pointby free motion—you throw it, and it goes up and comes down.It goes from the original place to the ﬁnal place in a certain amount of time.Now, you try a diﬀerent motion. Suppose that to get from here to there, it wentlike thisbut got there in just the same amount of time. Then he said this: If you calculatethe kinetic energy at every moment on the path, take away the potential energy,and integrate it over the time during the whole path, you’ll ﬁnd that the numberyou’ll get is bigger than that for the actual motion.「In other words, the laws of Newton could be stated not in the form F = mabut in the form: the average kinetic energy less the average potential energy isas little as possible for the path of an object going from one point to another.

* Later chapters do not depend on the material of this special lecture—which is intended to

be for「entertainment.」

19-1

19-1 A special lecture—almost

verbatim

19-2 A note added after the lecture

「Let me illustrate a little bit better what it means. If you take the caseof the gravitational ﬁeld, then if the particle has the path x(t) (let’s just takeone dimension for a moment; we take a trajectory that goes up and downand not sideways), where x is the height above the ground, the kinetic energy2 m (dx/dt)2, and the potential energy at any time is mgx. Now I take theis 1kinetic energy minus the potential energy at every moment along the path andintegrate that with respect to time from the initial time to the ﬁnal time. Let’ssuppose that at the original time t1 we started at some height and at the end ofthe time t2 we are deﬁnitely ending at some other place.

「Then the integral is Z t2

t1

(cid:20)1

2 m

dt

(cid:18) dx

(cid:19)2

(cid:21)

− mgx

dt.

The actual motion is some kind of a curve—it’s a parabola if we plot againstthe time—and gives a certain value for the integral. But we could imagine someother motion that went very high and came up and down in some peculiar way.

We can calculate the kinetic energy minus the potential energy and integrate forsuch a path . . . or for any other path we want. The miracle is that the true pathis the one for which that integral is least.

「Let’s try it out. First, suppose we take the case of a free particle for whichthere is no potential energy at all. Then the rule says that in going from onepoint to another in a given amount of time, the kinetic energy integral is least,so it must go at a uniform speed. (We know that’s the right answer—to go at auniform speed.) Why is that? Because if the particle were to go any other way,the velocities would be sometimes higher and sometimes lower than the average.The average velocity is the same for every case because it has to get from ‘here’to ‘there’ in a given amount of time.

「As an example, say your job is to start from home and get to school in agiven length of time with the car. You can do it several ways: You can acceleratelike mad at the beginning and slow down with the brakes near the end, or youcan go at a uniform speed, or you can go backwards for a while and then goforward, and so on. The thing is that the average speed has got to be, of course,the total distance that you have gone over the time. But if you do anything butgo at a uniform speed, then sometimes you are going too fast and sometimesyou are going too slow. Now the mean square of something that deviates aroundan average, as you know, is always greater than the square of the mean; so thekinetic energy integral would always be higher if you wobbled your velocity thanif you went at a uniform velocity. So we see that the integral is a minimum if thevelocity is a constant (when there are no forces). The correct path is like this.

「Now, an object thrown up in a gravitational ﬁeld does rise faster ﬁrst andthen slow down. That is because there is also the potential energy, and we musthave the least diﬀerence of kinetic and potential energy on the average. Becausethe potential energy rises as we go up in space, we will get a lower diﬀerence ifwe can get as soon as possible up to where there is a high potential energy. Thenwe can take that potential away from the kinetic energy and get a lower average.So it is better to take a path which goes up and gets a lot of negative stuﬀ fromthe potential energy.

「On the other hand, you can’t go up too fast, or too far, because you willthen have too much kinetic energy involved—you have to go very fast to get wayup and come down again in the ﬁxed amount of time available. So you don’twant to go too far up, but you want to go up some. So it turns out that thesolution is some kind of balance between trying to get more potential energy withthe least amount of extra kinetic energy—trying to get the diﬀerence, kineticminus the potential, as small as possible.

19-2

「That is all my teacher told me, because he was a very good teacher and knewwhen to stop talking. But I don’t know when to stop talking. So instead of leavingit as an interesting remark, I am going to horrify and disgust you with the complex-ities of life by proving that it is so. The kind of mathematical problem we will haveis very diﬃcult and a new kind. We have a certain quantity which is called theaction, S. It is the kinetic energy, minus the potential energy, integrated over time.

Action = S =

(KE − PE) dt.

Z t2

t1

Remember that the PE and KE are both functions of time. For each diﬀerentpossible path you get a diﬀerent number for this action. Our mathematicalproblem is to ﬁnd out for what curve that number is the least.

「You say—Oh, that’s just the ordinary calculus of maxima and minima. You

calculate the action and just diﬀerentiate to ﬁnd the minimum.

「But watch out. Ordinarily we just have a function of some variable, and wehave to ﬁnd the value of that variable where the function is least or most. Forinstance, we have a rod which has been heated in the middle and the heat is spreadaround. For each point on the rod we have a temperature, and we must ﬁnd thepoint at which that temperature is largest. But now for each path in space we havea number—quite a diﬀerent thing—and we have to ﬁnd the path in space for whichthe number is the minimum. That is a completely diﬀerent branch of mathematics.It is not the ordinary calculus. In fact, it is called the calculus of variations.「There are many problems in this kind of mathematics. For example, thecircle is usually deﬁned as the locus of all points at a constant distance from aﬁxed point, but another way of deﬁning a circle is this: a circle is that curve ofgiven length which encloses the biggest area. Any other curve encloses less areafor a given perimeter than the circle does. So if we give the problem: ﬁnd thatcurve which encloses the greatest area for a given perimeter, we would have aproblem of the calculus of variations—a diﬀerent kind of calculus than you’reused to.

「So we make the calculation for the path of an object. Here is the way weare going to do it. The idea is that we imagine that there is a true path and thatany other curve we draw is a false path, so that if we calculate the action for thefalse path we will get a value that is bigger than if we calculate the action forthe true path.

「Problem: Find the true path. Where is it? One way, of course, is to calculatethe action for millions and millions of paths and look at which one is lowest.When you ﬁnd the lowest one, that’s the true path.

「That’s a possible way. But we can do it better than that. When we have aquantity which has a minimum—for instance, in an ordinary function like thetemperature—one of the properties of the minimum is that if we go away from theminimum in the ﬁrst order, the deviation of the function from its minimum valueis only second order. At any place else on the curve, if we move a small distancethe value of the function changes also in the ﬁrst order. But at a minimum, a tinymotion away makes, in the ﬁrst approximation, no diﬀerence.

「That is what we are going to use to calculate the true path. If we havethe true path, a curve which diﬀers only a little bit from it will, in the ﬁrstapproximation, make no diﬀerence in the action. Any diﬀerence will be in thesecond approximation, if we really have a minimum.

「That is easy to prove. If there is a change in the ﬁrst order when I deviatethe curve a certain way, there is a change in the action that is proportional tothe deviation. The change presumably makes the action greater; otherwise wehaven’t got a minimum. But then if the change is proportional to the deviation,reversing the sign of the deviation will make the action less. We would get theaction to increase one way and to decrease the other way. The only way that itcould really be a minimum is that in the ﬁrst approximation it doesn’t make anychange, that the changes are proportional to the square of the deviations fromthe true path.

19-3

「So we work it this way: We call x(t) (with an underline) the true path—theone we are trying to ﬁnd. We take some trial path x(t) that diﬀers from the truepath by a small amount which we will call η(t) (eta of t).

「Now the idea is that if we calculate the action S for the path x(t), then thediﬀerence between that S and the action that we calculated for the path x(t)—tosimplify the writing we can call it S—the diﬀerence of S and S must be zero inthe ﬁrst-order approximation of small η. It can diﬀer in the second order, but inthe ﬁrst order the diﬀerence must be zero.「And that must be true for any η at all. Well, not quite. The method doesn’tmean anything unless you consider paths which all begin and end at the sametwo points—each path begins at a certain point at t1 and ends at a certain otherpoint at t2, and those points and times are kept ﬁxed. So the deviations in our ηhave to be zero at each end, η(t1) = 0 and η(t2) = 0. With that condition, wehave speciﬁed our mathematical problem.「If you didn’t know any calculus, you might do the same kind of thing toﬁnd the minimum of an ordinary function f(x). You could discuss what happensif you take f(x) and add a small amount h to x and argue that the correctionto f(x) in the ﬁrst order in h must be zero at the minimum. You would substitutex + h for x and expand out to the ﬁrst order in h . . . just as we are going to dowith η.「The idea is then that we substitute x(t) = x(t) + η(t) in the formula for theaction:

Z (cid:20) m

(cid:18) dx

(cid:19)2

2

dt

S =

(cid:21)

− V (x)

dt,

where I call the potential energy V (x). The derivative dx/dt is, of course, thederivative of x(t) plus the derivative of η(t), so for the action I get this expression:

(cid:19)2

(cid:21)

S =

+ dηdt

− V (x + η)

dt.

「Now I must write this out in more detail. For the squared term I get

(cid:20) m(cid:18) dxZ t2(cid:19)2(cid:18) dx

dt

2

t1

(cid:18) dη

(cid:19)2

.

dt

+ 2 dxdt

+

dηdt

dt

(cid:18) dx

(cid:19)2

dt

m2

But wait. I’m not worrying about higher than the ﬁrst order, so I will take allthe terms which involve η2 and higher powers and put them in a little box called‘second and higher order.’ From this term I get only second order, but there willbe more from something else. So the kinetic energy part is

+ m

dxdt

dηdt

+ (second and higher order).

「Now we need the potential V at x + η. I consider η small, so I can writeV (x) as a Taylor series. It is approximately V (x); in the next approximation(from the ordinary nature of derivatives) the correction is η times the rate ofchange of V with respect to x, and so on:

V (x + η) = V (x) + ηV 0(x) + η2

2 V 00(x) + ···

I have written V 0 for the derivative of V with respect to x in order to savewriting. The term in η2 and the ones beyond fall into the ‘second and higherorder’ category and we don’t have to worry about them. Putting it all together,

Z t2

(cid:20) m

(cid:18) dx

(cid:19)2

2

dt

t1

S =

− V (x) + m

dηdt

dxdt− ηV 0(x) + (second and higher order)

(cid:21)

dt.

19-4

Now if we look carefully at the thing, we see that the ﬁrst two terms which Ihave arranged here correspond to the action S that I would have calculated withthe true path x. The thing I want to concentrate on is the change in S—thediﬀerence between the S and the S that we would get for the right path. Thisdiﬀerence we will write as δS, called the variation in S. Leaving out the ‘secondand higher order’ terms, I have for δS

Z t2

(cid:20)

t1

δS =

m

dxdt

dηdt

− ηV 0(x)

dt.

(cid:21)

「Now the problem is this: Here is a certain integral. I don’t know whatthe x is yet, but I do know that no matter what η is, this integral must be zero.Well, you think, the only way that that can happen is that what multiplies ηmust be zero. But what about the ﬁrst term with dη/dt? Well, after all, if ηcan be anything at all, its derivative is anything also, so you conclude that thecoeﬃcient of dη/dt must also be zero. That isn’t quite right. It isn’t quite rightbecause there is a connection between η and its derivative; they are not absolutelyindependent, because η(t) must be zero at both t1 and t2.「The method of solving all problems in the calculus of variations always usesthe same general principle. You make the shift in the thing you want to vary (aswe did by adding η); you look at the ﬁrst-order terms; then you always arrangethings in such a form that you get an integral of the form ‘some kind of stuﬀ timesthe shift (η),’ but with no other derivatives (no dη/dt). It must be rearranged soit is always ‘something’ times η. You will see the great value of that in a minute.(There are formulas that tell you how to do this in some cases without actuallycalculating, but they are not general enough to be worth bothering about; thebest way is to calculate it out this way.)

「How can I rearrange the term in dη/dt to make it have an η? I can dothat by integrating by parts. It turns out that the whole trick of the calculusof variations consists of writing down the variation of S and then integratingby parts so that the derivatives of η disappear. It is always the same in everyproblem in which derivatives appear.「You remember the general principle for integrating by parts. If you haveany function f times dη/dt integrated with respect to t, you write down thederivative of ηf:

+ fThe integral you want is over the last term, so

(ηf) = η

dfdt

ddt

dηdt

.

dt = ηf −

f

dηdt

η

dfdt

dt.

Z(cid:12)(cid:12)(cid:12)(cid:12)t2

t1

(cid:18)

Z t2

t1

Z

(cid:19)

Z t2

t1

「In our formula for δS, the function f is m times dx/dt; therefore, I have the

following formula for δS.

δS = m

dxdt

η(t)

−

ddt

m

dxdt

η(t) dt −

V 0(x) η(t) dt.

The ﬁrst term must be evaluated at the two limits t1 and t2. Then I must havethe integral from the rest of the integration by parts. The last term is broughtdown without change.

「Now comes something which always happens—the integrated part disappears.(In fact, if the integrated part does not disappear, you restate the principle, addingconditions to make sure it does!) We have already said that η must be zero at bothends of the path, because the principle is that the action is a minimum providedthat the varied curve begins and ends at the chosen points. The condition is thatη(t1) = 0, and η(t2) = 0. So the integrated term is zero. We collect the otherterms together and obtain this:

Z t2

(cid:20)

t1

(cid:21)d2xdt2 − V 0(x)

δS =

−m

η(t) dt.

19-5

The variation in S is now the way we wanted it—there is the stuﬀ in brackets,say F, all multiplied by η(t) and integrated from t1 to t2.

「We have that an integral of something or other times η(t) is always zero:

Z

F(t) η(t) dt = 0.

I have some function of t; I multiply it by η(t); and I integrate it from one endto the other. And no matter what the η is, I get zero. That means that thefunction F(t) is zero. That’s obvious, but anyway I’ll show you one kind of proof.「Suppose that for η(t) I took something which was zero for all t except right

near one particular value. It stays zero until it gets to this t,

then it blips up for a moment and blips right back down. When we do the integralof this η times any function F, the only place that you get anything other thanzero was where η(t) was blipping, and then you get the value of F at that placetimes the integral over the blip. The integral over the blip alone isn’t zero, butwhen multiplied by F it has to be; so the function F has to be zero where theblip was. But the blip was anywhere I wanted to put it, so F must be zeroeverywhere.

「We see that if our integral is zero for any η, then the coeﬃcient of η mustbe zero. The action integral will be a minimum for the path that satisﬁes thiscomplicated diﬀerential equation:

(cid:20)

(cid:21)

−m

d2xdt2 − V 0(x)

= 0.

It’s not really so complicated; you have seen it before. It is just F = ma. Theﬁrst term is the mass times acceleration, and the second is the derivative of thepotential energy, which is the force.

「So, for a conservative system at least, we have demonstrated that the principleof least action gives the right answer; it says that the path that has the minimumaction is the one satisfying Newton’s law.

「One remark: I did not prove it was a minimum—maybe it’s a maximum.In fact, it doesn’t really have to be a minimum. It is quite analogous to whatwe found for the ‘principle of least time’ which we discussed in optics. Therealso, we said at ﬁrst it was ‘least’ time. It turned out, however, that there weresituations in which it wasn’t the least time. The fundamental principle was thatfor any ﬁrst-order variation away from the optical path, the change in time waszero; it is the same story. What we really mean by ‘least’ is that the ﬁrst-orderchange in the value of S, when you change the path, is zero. It is not necessarilya ‘minimum.’

「Next, I remark on some generalizations. In the ﬁrst place, the thing can bedone in three dimensions. Instead of just x, I would have x, y, and z as functionsof t; the action is more complicated. For three-dimensional motion, you have touse the complete kinetic energy—(m/2) times the whole velocity squared. Thatis,

(cid:20)(cid:18) dx

(cid:19)2

dt

(cid:18) dy

(cid:19)2

dt

+

(cid:18) dz

(cid:19)2(cid:21)

.

dt

+

KE = m2

Also, the potential energy is a function of x, y, and z. And what about the path?The path is some general curve in space, which is not so easily drawn, but theidea is the same. And what about the η? Well, η can have three components.You could shift the paths in x, or in y, or in z—or you could shift in all threedirections simultaneously. So η would be a vector. This doesn’t really complicatethings too much, though. Since only the ﬁrst-order variation has to be zero,we can do the calculation by three successive shifts. We can shift η only in thex-direction and say that coeﬃcient must be zero. We get one equation. Thenwe shift it in the y-direction and get another. And in the z-direction and getanother. Or, of course, in any order that you want. Anyway, you get three19-6

equations. And, of course, Newton’s law is really three equations in the threedimensions—one for each component. I think that you can practically see that itis bound to work, but we will leave you to show for yourself that it will work forthree dimensions. Incidentally, you could use any coordinate system you want,polar or otherwise, and get Newton’s laws appropriate to that system right oﬀby seeing what happens if you have the shift η in radius, or in angle, etc.

「Similarly, the method can be generalized to any number of particles. If youhave, say, two particles with a force between them, so that there is a mutualpotential energy, then you just add the kinetic energy of both particles and takethe potential energy of the mutual interaction. And what do you vary? You varythe paths of both particles. Then, for two particles moving in three dimensions,there are six equations. You can vary the position of particle 1 in the x-direction,in the y-direction, and in the z-direction, and similarly for particle 2; so thereare six equations. And that’s as it should be. There are the three equationsthat determine the acceleration of particle 1 in terms of the force on it and threefor the acceleration of particle 2, from the force on it. You follow the samegame through, and you get Newton’s law in three dimensions for any number ofparticles.

「I have been saying that we get Newton’s law. That is not quite true, becauseNewton’s law includes nonconservative forces like friction. Newton said that mais equal to any F. But the principle of least action only works for conservativesystems—where all forces can be gotten from a potential function. You know,however, that on a microscopic level—on the deepest level of physics—thereare no nonconservative forces. Nonconservative forces, like friction, appear onlybecause we neglect microscopic complications—there are just too many particlesto analyze. But the fundamental laws can be put in the form of a principle ofleast action.

p1 − v2/c2 dt − q

「Let me generalize still further. Suppose we ask what happens if the particlemoves relativistically. We did not get the right relativistic equation of motion;F = ma is only right nonrelativistically. The question is: Is there a correspondingprinciple of least action for the relativistic case? There is. The formula in thecase of relativity is the following:

S = −m0c2Z t2integral of a function of velocity,p1 − v2/c2. Then instead of just the potential

The ﬁrst part of the action integral is the rest mass m0 times c2 times theenergy, we have an integral over the scalar potential φ and over v times thevector potential A. Of course, we are then including only electromagnetic forces.All electric and magnetic ﬁelds are given in terms of φ and A. This actionfunction gives the complete theory of relativistic motion of a single particle in anelectromagnetic ﬁeld.

[φ(x, y, z, t) − v · A(x, y, z, t)] dt.

you remember, p = m0v/p1 − v2/c2.

「Of course, wherever I have written v, you understand that before you tryto ﬁgure anything out, you must substitute dx/dt for vx and so on for the othercomponents. Also, you put the point along the path at time t, x(t), y(t), z(t)where I wrote simply x, y, z. Properly, it is only after you have made thosereplacements for the v’s that you have the formula for the action for a relativisticparticle. I will leave to the more ingenious of you the problem to demonstrate thatthis action formula does, in fact, give the correct equations of motion for relativity.May I suggest you do it ﬁrst without the A, that is, for no magnetic ﬁeld? Thenyou should get the components of the equation of motion, dp/dt = −q ∇φ, where,「It is much more diﬃcult to include also the case with a vector potential. Thevariations get much more complicated. But in the end, the force term does comeout equal to q(E + v × B), as it should. But I will leave that for you to playwith.「I would like to emphasize that in the general case, for instance in the rela-tivistic formula, the action integrand no longer has the form of the kinetic energy19-7

Z t2

t1

t1

minus the potential energy. That’s only true in the nonrelativistic approximation.

For example, the term m0c2p1 − v2/c2 is not what we have called the kinetic

energy. The question of what the action should be for any particular case mustbe determined by some kind of trial and error. It is just the same problem asdetermining what are the laws of motion in the ﬁrst place. You just have toﬁddle around with the equations that you know and see if you can get them intothe form of the principle of least action.

「One other point on terminology. The function that is integrated over timeto get the action S is called the Lagrangian, L, which is a function only of thevelocities and positions of particles. So the principle of least action is also written

Z t2

S =

L(xi, vi) dt,

t1

where by xi and vi are meant all the components of the positions and velocities.So if you hear someone talking about the ‘Lagrangian,’ you know they aretalking about the function that is used to ﬁnd S. For relativistic motion in anelectromagnetic ﬁeld

L = −m0c2p1 − v2/c2 − q(φ − v · A).

「Also, I should say that S is not really called the ‘action’ by the most preciseand pedantic people. It is called ‘Hamilton’s ﬁrst principal function.’ Now I hateto give a lecture on ‘the-principle-of-least-Hamilton’s-ﬁrst-principal-function.’ SoI call it ‘the action.’ Also, more and more people are calling it the action. Yousee, historically something else which is not quite as useful was called the action,but I think it’s more sensible to change to a newer deﬁnition. So now you toowill call the new function the action, and pretty soon everybody will call it bythat simple name.

「Now I want to say some things on this subject which are similar to thediscussions I gave about the principle of least time. There is quite a diﬀerencein the characteristic of a law which says a certain integral from one place toanother is a minimum—which tells something about the whole path—and of alaw which says that as you go along, there is a force that makes it accelerate.The second way tells how you inch your way along the path, and the other is agrand statement about the whole path. In the case of light, we talked about theconnection of these two. Now, I would like to explain why it is true that there arediﬀerential laws when there is a least action principle of this kind. The reason isthe following: Consider the actual path in space and time. As before, let’s takeonly one dimension, so we can plot the graph of x as a function of t. Along thetrue path, S is a minimum. Let’s suppose that we have the true path and that itgoes through some point a in space and time, and also through another nearbypoint b.Now if the entire integral from t1 to t2 is a minimum, it is also necessary thatthe integral along the little section from a to b is also a minimum. It can’t bethat the part from a to b is a little bit more. Otherwise you could just ﬁddlewith just that piece of the path and make the whole integral a little lower.「So every subsection of the path must also be a minimum. And this is trueno matter how short the subsection. Therefore, the principle that the whole pathgives a minimum can be stated also by saying that an inﬁnitesimal section ofpath also has a curve such that it has a minimum action. Now if we take a shortenough section of path—between two points a and b very close together—how thepotential varies from one place to another far away is not the important thing,because you are staying almost in the same place over the whole little piece ofthe path. The only thing that you have to discuss is the ﬁrst-order change in thepotential. The answer can only depend on the derivative of the potential andnot on the potential everywhere. So the statement about the gross property ofthe whole path becomes a statement of what happens for a short section of thepath—a diﬀerential statement. And this diﬀerential statement only involves the19-8

derivatives of the potential, that is, the force at a point. That’s the qualitativeexplanation of the relation between the gross law and the diﬀerential law.

「In the case of light we also discussed the question: How does the particleﬁnd the right path? From the diﬀerential point of view, it is easy to understand.Every moment it gets an acceleration and knows only what to do at that instant.But all your instincts on cause and eﬀect go haywire when you say that theparticle decides to take the path that is going to give the minimum action. Doesit ‘smell’ the neighboring paths to ﬁnd out whether or not they have more action?In the case of light, when we put blocks in the way so that the photons couldnot test all the paths, we found that they couldn’t ﬁgure out which way to go,and we had the phenomenon of diﬀraction.

「Is the same thing true in mechanics? Is it true that the particle doesn’t just‘take the right path’ but that it looks at all the other possible trajectories? Andif by having things in the way, we don’t let it look, that we will get an analogof diﬀraction? The miracle of it all is, of course, that it does just that. That’swhat the laws of quantum mechanics say. So our principle of least action isincompletely stated. It isn’t that a particle takes the path of least action but thatit smells all the paths in the neighborhood and chooses the one that has the leastaction by a method analogous to the one by which light chose the shortest time.You remember that the way light chose the shortest time was this: If it went ona path that took a diﬀerent amount of time, it would arrive at a diﬀerent phase.And the total amplitude at some point is the sum of contributions of amplitudefor all the diﬀerent ways the light can arrive. All the paths that give wildlydiﬀerent phases don’t add up to anything. But if you can ﬁnd a whole sequenceof paths which have phases almost all the same, then the little contributions willadd up and you get a reasonable total amplitude to arrive. The important pathbecomes the one for which there are many nearby paths which give the samephase.

「It is just exactly the same thing for quantum mechanics. The completequantum mechanics (for the nonrelativistic case and neglecting electron spin)works as follows: The probability that a particle starting at point 1 at the time t1will arrive at point 2 at the time t2 is the square of a probability amplitude. Thetotal amplitude can be written as the sum of the amplitudes for each possiblepath—for each way of arrival. For every x(t) that we could have—for everypossible imaginary trajectory—we have to calculate an amplitude. Then weadd them all together. What do we take for the amplitude for each path? Ouraction integral tells us what the amplitude for a single path ought to be. Theamplitude is proportional to some constant times eiS/, where S is the actionfor that path. That is, if we represent the phase of the amplitude by a complexnumber, the phase angle is S/. The action S has dimensions of energy timestime, and Planck’s constant  has the same dimensions. It is the constant thatdetermines when quantum mechanics is important.

「Here is how it works: Suppose that for all paths, S is very large comparedto . One path contributes a certain amplitude. For a nearby path, the phase isquite diﬀerent, because with an enormous S even a small change in S means acompletely diﬀerent phase—because  is so tiny. So nearby paths will normallycancel their eﬀects out in taking the sum—except for one region, and that is whena path and a nearby path all give the same phase in the ﬁrst approximation (moreprecisely, the same action within ). Only those paths will be the important ones.So in the limiting case in which Planck’s constant  goes to zero, the correctquantum-mechanical laws can be summarized by simply saying: ‘Forget aboutall these probability amplitudes. The particle does go on a special path, namely,that one for which S does not vary in the ﬁrst approximation.’ That’s the relationbetween the principle of least action and quantum mechanics. The fact thatquantum mechanics can be formulated in this way was discovered in 1942 by astudent of that same teacher, Bader, I spoke of at the beginning of this lecture.[Quantum mechanics was originally formulated by giving a diﬀerential equationfor the amplitude (Schrödinger) and also by some other matrix mathematics(Heisenberg).]

19-9

「Now I want to talk about other minimum principles in physics. There aremany very interesting ones. I will not try to list them all now but will onlydescribe one more. Later on, when we come to a physical phenomenon which hasa nice minimum principle, I will tell about it then. I want now to show that wecan describe electrostatics, not by giving a diﬀerential equation for the ﬁeld, butby saying that a certain integral is a maximum or a minimum. First, let’s takethe case where the charge density is known everywhere, and the problem is toﬁnd the potential φ everywhere in space. You know that the answer should be

∇2φ = −ρ/0.

But another way of stating the same thing is this: Calculate the integral U∗,where

Z

(∇φ)2 dV −

ρφ dV,

Z

U∗ = 02

which is a volume integral to be taken over all space. This thing is a minimumfor the correct potential distribution φ(x, y, z).「We can show that the two statements about electrostatics are equivalent.Let’s suppose that we pick any function φ. We want to show that when we takefor φ the correct potential φ, plus a small deviation f, then in the ﬁrst order, thechange in U∗ is zero. So we write

φ = φ + f.

The φ is what we are looking for, but we are making a variation of it to ﬁndwhat it has to be so that the variation of U∗ is zero to ﬁrst order. For the ﬁrstpart of U∗, we need

(∇φ)2 = (∇φ)2 + 2∇φ · ∇f + (∇f)2.

The only ﬁrst-order term that will vary is

In the second term of the quantity U∗, the integrand is

2∇φ · ∇f.

ρφ = ρφ + ρf,

whose variable part is ρf. So, keeping only the variable parts, we need theintegral

Z

∆U∗ =

(0∇φ · ∇f − ρf) dV.

「Now, following the old general rule, we have to get the darn thing all clearof derivatives of f. Let’s look at what the derivatives are. The dot product is

∂φ∂x

∂f∂x

+ ∂φ∂y

∂f∂y

+ ∂φ∂z

∂f∂z

,

which we have to integrate with respect to x, to y, and to z. Now here is thetrick: to get rid of ∂f /∂x we integrate by parts with respect to x. That willcarry the derivative over onto the φ. It’s the same general idea we used to getrid of derivatives with respect to t. We use the equality

Z ∂φ

∂x

Z

dx = f

∂f∂x

−

∂φ∂x

∂2φ∂x2 dx.

f

The integrated term is zero, since we have to make f zero at inﬁnity. (Thatcorresponds to making η zero at t1 and t2. So our principle should be moreaccurately stated: U∗ is less for the true φ than for any other φ(x, y, z) havingthe same values at inﬁnity.) Then we do the same thing for y and z. So ourintegral ∆U∗ is

Z

∆U∗ =

(−0∇2φ − ρ)f dV.

19-10

In order for this variation to be zero for any f, no matter what, the coeﬃcientof f must be zero and, therefore,

∇2φ = −ρ/0.

We get back our old equation. So our ‘minimum’ proposition is correct.

「We can generalize our proposition if we do our algebra in a little diﬀerentway. Let’s go back and do our integration by parts without taking components.We start by looking at the following equality:

∇ · (f ∇φ) = ∇f · ∇φ + f ∇2φ.

If I diﬀerentiate out the left-hand side, I can show that it is just equal to theright-hand side. Now we can use this equation to integrate by parts. In ourintegral ∆U∗, we replace ∇φ · ∇f by ∇ · (f ∇φ) − f ∇2φ, which gets integratedover volume. The divergence term integrated over volume can be replaced by asurface integral:

Z

Z

∇ · (f ∇φ) dV =

f ∇φ · n da.

Since we are integrating over all space, the surface over which we are integratingis at inﬁnity. There, f is zero and we get the same answer as before.「Only now we see how to solve a problem when we don’t know where all thecharges are. Suppose that we have conductors with charges spread out on themin some way. We can still use our minimum principle if the potentials of all theconductors are ﬁxed. We carry out the integral for U∗ only in the space outsideof all conductors. Then, since we can’t vary φ on the conductor, f is zero on allthose surfaces, and the surface integral

is still zero. The remaining volume integral

∆U∗ =

(−0 ∇2φ − ρ)f dV

f ∇φ · n da

ZZ

∇2φ = −ρ/0.

is only to be carried out in the spaces between conductors. Of course, we getPoisson’s equation again,

So we have shown that our original integral U∗ is also a minimum if we evaluateit over the space outside of conductors all at ﬁxed potentials (that is, such thatany trial φ(x, y, z) must equal the given potential of the conductors when (x, y, z)is a point on the surface of a conductor).「There is an interesting case when the only charges are on conductors. Then

Z

U∗ = 02

(∇φ)2 dV.

Our minimum principle says that in the case where there are conductors setat certain given potentials, the potential between them adjusts itself so thatintegral U∗ is least. What is this integral? The term ∇φ is the electric ﬁeld,so the integral is the electrostatic energy. The true ﬁeld is the one, of all thosecoming from the gradient of a potential, with the minimum total energy.

「I would like to use this result to calculate something particular to show youthat these things are really quite practical. Suppose I take two conductors in theform of a cylindrical condenser.The inside conductor has the potential V , and the outside is at the potentialzero. Let the radius of the inside conductor be a and that of the outside, b. Nowwe can suppose any distribution of potential between the two. If we use the

correct φ, and calculate 0/2R (∇φ)2 dV , it should be the energy of the system,

19-11

2 CV 2. So we can also calculate C by our principle. But if we use a wrong1distribution of potential and try to calculate the capacity C by this method, wewill get a capacity that is too big, since V is speciﬁed. Any assumed potential φthat is not the exactly correct one will give a fake C that is larger than thecorrect value. But if my false φ is any rough approximation, the C will be a goodapproximation, because the error in C is second order in the error in φ.「Suppose I don’t know the capacity of a cylindrical condenser. I can usethis principle to ﬁnd it. I just guess at the potential function φ until I get thelowest C. Suppose, for instance, I pick a potential that corresponds to a constantﬁeld. (You know, of course, that the ﬁeld isn’t really constant here; it variesas 1/r.) A ﬁeld which is constant means a potential which goes linearly withdistance. To ﬁt the conditions at the two conductors, it must be

(cid:18)1 − r − ab − a

(cid:19)

.

φ = V

This function is V at r = a, zero at r = b, and in between has a constant slopeequal to −V /(b − a). So what one does to ﬁnd the integral U∗ is multiply thesquare of this gradient by 0/2 and integrate over all volume. Let’s do thiscalculation for a cylinder of unit length. A volume element at the radius ris 2πr dr. Doing the integral, I ﬁnd that my ﬁrst try at the capacity gives

The integral is easy; it is just

Z b12 CV 2(ﬁrst try) = 02(cid:19)(cid:18) b + a

a

πV 2

b − a

.

V 2

(b − a)2

2πr dr.

So I have a formula for the capacity which is not the true one but is an approximatejob:

C2π0

= b + a2(b − a) .

It is, naturally, diﬀerent from the correct answer C = 2π0/ ln(b/a), but it’s nottoo bad. Let’s compare it with the right answer for several values of b/a. I havecomputed out the answers in this table:

ba2410100

1.51.1

Ctrue2π01.44230.7210.4340.2172.466210.492059

C(ﬁrst approx.)

2π01.5000.8330.6120.512.5010.500000

Even when b/a is as big as 2—which gives a pretty big variation in the ﬁeldcompared with a linearly varying ﬁeld—I get a pretty fair approximation. Theanswer is, of course, a little too high, as expected. The thing gets much worse ifyou have a tiny wire inside a big cylinder. Then the ﬁeld has enormous variationsand if you represent it by a constant, you’re not doing very well. With b/a = 100,we’re oﬀ by nearly a factor of two. Things are much better for small b/a. To takethe opposite extreme, when the conductors are not very far apart—say b/a = 1.1—then the constant ﬁeld is a pretty good approximation, and we get the correctvalue for C to within a tenth of a percent.「Now I would like to tell you how to improve such a calculation. (Of course,you know the right answer for the cylinder, but the method is the same for someother odd shapes, where you may not know the right answer.) The next step is19-12

to try a better approximation to the unknown true φ. For example, we might trya constant plus an exponential φ, etc. But how do you know when you have abetter approximation unless you know the true φ? Answer: You calculate C; thelowest C is the value nearest the truth. Let us try this idea out. Suppose thatthe potential is not linear but say quadratic in r—that the electric ﬁeld is notconstant but linear. The most general quadratic form that ﬁts φ = 0 at r = band φ = V at r = a is

(cid:20)

(cid:19)

(cid:18) r − a

b − a

φ = V

1 + α

− (1 + α)

(cid:18) r − a

b − a

(cid:19)2(cid:21)

,

where α is any constant number. This formula is a little more complicated. Itinvolves a quadratic term in the potential as well as a linear term. It is very easyto get the ﬁeld out of it. The ﬁeld is just

E = − dφdr

= − αVb − a

+ 2(1 + α) (r − a)V(b − a)2 .

Now we have to square this and integrate over volume. But wait a moment.What should I take for α? I can take a parabola for the φ; but what parabola?Here’s what I do: Calculate the capacity with an arbitrary α. What I get is

(cid:20) b

a

(cid:18) α26 + 2α

3 + 1

(cid:19)

(cid:21)

.

+ 16 α2 + 13

C2π0

= ab − a

It looks a little complicated, but it comes out of integrating the square of theﬁeld. Now I can pick my α. I know that the truth lies lower than anything thatI am going to calculate, so whatever I put in for α is going to give me an answertoo big. But if I keep playing with α and get the lowest possible value I can, thatlowest value is nearer to the truth than any other value. So what I do next isto pick the α that gives the minimum value for C. Working it out by ordinarycalculus, I get that the minimum C occurs for α = −2b/(b + a). Substitutingthat value into the formula, I obtain for the minimum capacity

C2π0

= b2 + 4ab + a23(b2 − a2)

.

「I’ve worked out what this formula gives for C for various values of b/a. I callthese numbers C(quadratic). Here is a table that compares C(quadratic) withthe true C.

ba2410100

1.51.1

Ctrue2π01.44230.7210.4340.2172.466210.492059

C(quadratic)

2π01.4440.7330.4750.3462.466710.492065

「For example, when the ratio of the radii is 2 to 1, I have 1.444, which is avery good approximation to the true answer, 1.4423. Even for larger b/a, it stayspretty good—it is much, much better than the ﬁrst approximation. It is evenfairly good—only oﬀ by 10 percent—when b/a is 10 to 1. But when it gets to be100 to 1—well, things begin to go wild. I get that C is 0.346 instead of 0.217.On the other hand, for a ratio of radii of 1.5, the answer is excellent; and fora b/a of 1.1, the answer comes out 10.492065 instead of 10.492059. Where theanswer should be good, it is very, very good.「I have given these examples, ﬁrst, to show the theoretical value of theprinciples of minimum action and minimum principles in general and, second,19-13

to show their practical utility—not just to calculate a capacity when we alreadyknow the answer. For any other shape, you can guess an approximate ﬁeld withsome unknown parameters like α and adjust them to get a minimum. You willget excellent numerical results for otherwise intractable problems.」

19-2 A note added after the lecture「I should like to add something that I didn’t have time for in the lecture. (Ialways seem to prepare more than I have time to tell about.) As I mentionedearlier, I got interested in a problem while working on this lecture. I want totell you what that problem is. Among the minimum principles that I couldmention, I noticed that most of them sprang in one way or another from theleast action principle of mechanics and electrodynamics. But there is also a classthat does not. As an example, if currents are made to go through a piece ofmaterial obeying Ohm’s law, the currents distribute themselves inside the pieceso that the rate at which heat is generated is as little as possible. Also we cansay (if things are kept isothermal) that the rate at which energy is generatedis a minimum. Now, this principle also holds, according to classical theory, indetermining even the distribution of velocities of the electrons inside a metalwhich is carrying a current. The distribution of velocities is not exactly theequilibrium distribution [Chapter 40, Vol. I, Eq. (40.6)] because they are driftingsideways. The new distribution can be found from the principle that it is thedistribution for a given current for which the entropy developed per second bycollisions is as small as possible. The true description of the electrons’ behaviorought to be by quantum mechanics, however. The question is: Does the sameprinciple of minimum entropy generation also hold when the situation is describedquantum-mechanically? I haven’t found out yet.

「The question is interesting academically, of course. Such principles arefascinating, and it is always worth while to try to see how general they are.But also from a more practical point of view, I want to know. I, with somecolleagues, have published a paper in which we calculated by quantum mechanicsapproximately the electrical resistance felt by an electron moving through an ioniccrystal like NaCl. [Feynman, Hellwarth, Iddings, and Platzman,「Mobility of SlowElectrons in a Polar Crystal,」Phys. Rev. 127, 1004 (1962).] But if a minimumprinciple existed, we could use it to make the results much more accurate, just asthe minimum principle for the capacity of a condenser permitted us to get suchaccuracy for that capacity even though we had only a rough knowledge of theelectric ﬁeld.」

19-14

20

Solutions of Maxwell’s Equations in FreeSpace

20-1 Waves in free space; plane wavesIn

Chapter 18 we had reached the point where we had the Maxwell equationsin complete form. All there is to know about the classical theory of the electricand magnetic ﬁelds can be found in the four equations:

I. ∇ · E = ρ0III. ∇ · B = 0

II. ∇ × E = − ∂B∂t+ ∂E∂t

c2∇ × B = j0

IV.

(20.1)

When we put all these equations together, a remarkable new phenomenon occurs:ﬁelds generated by moving charges can leave the sources and travel alone throughspace. We considered a special example in which an inﬁnite current sheet issuddenly turned on. After the current has been on for the time t, there areuniform electric and magnetic ﬁelds extending out the distance ct from the source.Suppose that the current sheet lies in the yz-plane with a surface current density Jgoing toward positive y. The electric ﬁeld will have only a y-component, and themagnetic ﬁeld, only a z-component. The ﬁeld components are given by

Ey = cBz = − J20c

,

(20.2)

for positive values of x less than ct. For larger x the ﬁelds are zero. There are,of course, similar ﬁelds extending the same distance from the current sheet inthe negative x-direction. In Fig. 20-1 we show a graph of the magnitude of theﬁelds as a function of x at the instant t. As time goes on, the「wavefront」at ctmoves outward in x at the constant velocity c.Now consider the following sequence of events. We turn on a current of unitstrength for a while, then suddenly increase the current strength to three units,and hold it constant at this value. What do the ﬁelds look like then? We can seewhat the ﬁelds will look like in the following way. First, we imagine a currentof unit strength that is turned on at t = 0 and left constant forever. The ﬁeldsfor positive x are then given by the graph in part (a) of Fig. 20-2. Next, we askwhat would happen if we turn on a steady current of two units at the time t1.The ﬁelds in this case will be twice as high as before, but will extend outin x only the distance c(t − t1), as shown in part (b) of the ﬁgure. When we addthese two solutions, using the principle of superposition, we ﬁnd that the sum ofthe two sources is a current of one unit for the time from zero to t1 and a currentof three units for times greater than t1. At the time t the ﬁelds will vary with xas shown in part (c) of Fig. 20-2.Now let’s take a more complicated problem. Consider a current which isturned on to one unit for a while, then turned up to three units, and later turnedoﬀ to zero. What are the ﬁelds for such a current? We can ﬁnd the solution inthe same way—by adding the solutions of three separate problems. First, weﬁnd the ﬁelds for a step current of unit strength. (We have solved that problemalready.) Next, we ﬁnd the ﬁelds produced by a step current of two units. Finally,we solve for the ﬁelds of a step current of minus three units. When we add thethree solutions, we will have a current which is one unit strong from t = 0 tosome later time, say t1, then three units strong until a still later time t2, and20-1

20-1 Waves in free space; plane waves20-2 Three-dimensional waves20-3 Scientiﬁc imagination20-4 Spherical waves

References: Chapter 47, Vol. I: Sound:The Wave EquationChapter 28, Vol. I: Elec-tromagnetic Radiation

Fig. 20-1. The electric and magnetic ﬁeldas a function of x at the time t after thecurrent sheet is turned on.

Fig. 20-2. The electric ﬁeld of a currentsheet. (a) One unit of current turned onat t = 0; (b) Two units of current turned onat t = t1; (c) Superposition of (a) and (b).

Fig. 20-3. If the current source strength varies as shown in (a), then at the time t

shown by the arrow the electric ﬁeld as a function of x is as shown in (b).

then turned oﬀ—that is, to zero. A graph of the current as a function of time isshown in Fig. 20-3(a). When we add the three solutions for the electric ﬁeld, weﬁnd that its variation with x, at a given instant t, is as shown in Fig. 20-3(b).The ﬁeld is an exact representation of the current. The ﬁeld distribution in spaceis a nice graph of the current variation with time—only drawn backwards. Astime goes on the whole picture moves outward at the speed c, so there is a littleblob of ﬁeld, travelling toward positive x, which contains a completely detailedmemory of the history of all the current variations. If we were to stand milesaway, we could tell from the variation of the electric or magnetic ﬁeld exactlyhow the current had varied at the source.

You will also notice that long after all activity at the source has completelystopped and all charges and currents are zero, the block of ﬁeld continues totravel through space. We have a distribution of electric and magnetic ﬁelds thatexist independently of any charges or currents. That is the new eﬀect that comesfrom the complete set of Maxwell’s equations. If we want, we can give a completemathematical representation of the analysis we have just done by writing thatthe electric ﬁeld at a given place and a given time is proportional to the currentat the source, only not at the same time, but at the earlier time t − x/c. We canwrite

.

(20.3)

Ey(t) = − J(t − x/c)

20c

We have, believe it or not, already derived this same equation from anotherpoint of view in Vol. I, when we were dealing with the theory of the index ofrefraction. Then, we had to ﬁgure out what ﬁelds were produced by a thinlayer of oscillating dipoles in a sheet of dielectric material with the dipoles set inmotion by the electric ﬁeld of an incoming electromagnetic wave. Our problemwas to calculate the combined ﬁelds of the original wave and the waves radiatedby the oscillating dipoles. How could we have calculated the ﬁelds generated bymoving charges when we didn’t have Maxwell’s equations? At that time we tookas our starting point (without any derivation) a formula for the radiation ﬁeldsproduced at large distances from an accelerating point charge. If you will look inChapter 31 of Vol. I, you will see that Eq. (31.9) there is just the same as theEq. (20.3) that we have just written down. Although our earlier derivation wascorrect only at large distances from the source, we see now that the same resultcontinues to be correct even right up to the source.

We want now to look in a general way at the behavior of electric and magneticﬁelds in empty space far away from the sources, i.e., from the currents and charges.Very near the sources—near enough so that during the delay in transmission, thesource has not had time to change much—the ﬁelds are very much the same aswe have found in what we called the electrostatic or magnetostatic cases. If we goout to distances large enough so that the delays become important, however, thenature of the ﬁelds can be radically diﬀerent from the solutions we have found.In a sense, the ﬁelds begin to take on a character of their own when they havegone a long way from all the sources. So we can begin by discussing the behaviorof the ﬁelds in a region where there are no currents or charges.

20-2

Suppose we ask: What kind of ﬁelds can there be in regions where ρ and jare both zero? In Chapter 18 we saw that the physics of Maxwell’s equationscould also be expressed in terms of diﬀerential equations for the scalar and vectorpotentials:

∇2φ − 1c2∇2A − 1c2

∂2φ∂t2∂2A∂t2

,

= − ρ0= − j

0c2 .

(20.4)

(20.5)

(20.6)

(20.7)

If ρ and j are zero, these equations take on the simpler form

∇2φ − 1c2∇2A − 1c2

∂2φ∂t2∂2A∂t2

= 0,

= 0.

Thus in free space the scalar potential φ and each component of the vectorpotential A all satisfy the same mathematical equation. Suppose we let ψ (psi)stand for any one of the four quantities φ, Ax, Ay, Az; then we want to investigatethe general solutions of the following equation:

∇2ψ − 1c2

∂2ψ∂t2

= 0.

(20.8)

This equation is called the three-dimensional wave equation—three-dimensional,because the function ψ may depend in general on x, y, and z, and we need toworry about variations in all three coordinates. This is made clear if we writeout explicitly the three terms of the Laplacian operator:

∂2ψ∂x2

+ ∂2ψ∂y2

∂z2 − 1+ ∂2ψ

c2

∂2ψ∂t2

= 0.

(20.9)

In free space, the electric ﬁelds E and B also satisfy the wave equation. Forexample, since B = ∇ × A, we can get a diﬀerential equation for B by takingthe curl of Eq. (20.7). Since the Laplacian is a scalar operator, the order of theLaplacian and curl operations can be interchanged:

∇ × (∇2A) = ∇2(∇ × A) = ∇2B.

Similarly, the order of the operations curl and ∂/∂t can be interchanged:

∇ × 1c2

∂2A∂t2

= 1c2

∂2∂t2

(∇ × A) = 1c2

∂2B∂t2 .

Using these results, we get the following diﬀerential equation for B:

∇2B − 1c2

∂2B∂t2

= 0.

(20.10)

So each component of the magnetic ﬁeld B satisﬁes the three-dimensional waveequation. Similarly, using the fact that E = −∇φ − ∂A/∂t, it follows that theelectric ﬁeld E in free space also satisﬁes the three-dimensional wave equation:

∇2E − 1c2

∂2E∂t2

= 0.

(20.11)

All of our electromagnetic ﬁelds satisfy the same wave equation, Eq. (20.8).We might well ask: What is the most general solution to this equation? However,rather than tackling that diﬃcult question right away, we will look ﬁrst at whatcan be said in general about those solutions in which nothing varies in y and z.(Always do an easy case ﬁrst so that you can see what is going to happen, and thenyou can go to the more complicated cases.) Let’s suppose that the magnitudes ofthe ﬁelds depend only upon x—that there are no variations of the ﬁelds with y20-3

and z. We are, of course, considering plane waves again. We should expect to getresults something like those in the previous section. In fact, we will ﬁnd preciselythe same answers. You may ask:「Why do it all over again?」It is important todo it again, ﬁrst, because we did not show that the waves we found were the mostgeneral solutions for plane waves, and second, because we found the ﬁelds onlyfrom a very particular kind of current source. We would like to ask now: Whatis the most general kind of one-dimensional wave there can be in free space? Wecannot ﬁnd that by seeing what happens for this or that particular source, butmust work with greater generality. Also we are going to work this time withdiﬀerential equations instead of with integral forms. Although we will get thesame results, it is a way of practicing back and forth to show that it doesn’t makeany diﬀerence which way you go. You should know how to do things every whichway, because when you get a hard problem, you will often ﬁnd that only one ofthe various ways is tractable.

We could consider directly the solution of the wave equation for some elec-tromagnetic quantity. Instead, we want to start right from the beginning withMaxwell’s equations in free space so that you can see their close relationship tothe electromagnetic waves. So we start with the equations in (20.1), setting thecharges and currents equal to zero. They become

I. ∇ · E = 0

II. ∇ × E = − ∂B∂tIII. ∇ · B = 0

(20.12)

c2∇ × B = ∂E∂tWe write the ﬁrst equation out in components:

IV.

∇ · E = ∂Ex∂x

+ ∂Ey∂y

+ ∂Ez∂z

= 0.

(20.13)

We are assuming that there are no variations with y and z, so the last two termsare zero. This equation then tells us that

∂Ex∂x

= 0.

(20.14)

Its solution is that Ex, the component of the electric ﬁeld in the x-direction, is aconstant in space. If you look at IV in (20.12), supposing no B-variation in yand z either, you can see that Ex is also constant in time. Such a ﬁeld could bethe steady dc ﬁeld from some charged condenser plates a long distance away. Weare not interested now in such an uninteresting static ﬁeld; we are at the momentinterested only in dynamically varying ﬁelds. For dynamic ﬁelds, Ex = 0.We have then the important result that for the propagation of plane waves inany direction, the electric ﬁeld must be at right angles to the direction of propa-gation. It can, of course, still vary in a complicated way with the coordinate x.The transverse E-ﬁeld can always be resolved into two components, say they-component and the z-component. So let’s ﬁrst work out a case in which theelectric ﬁeld has only one transverse component. We’ll take ﬁrst an electric ﬁeldthat is always in the y-direction, with zero z-component. Evidently, if we solvethis problem we can also solve for the case where the electric ﬁeld is always in thez-direction. The general solution can always be expressed as the superposition oftwo such ﬁelds.

How easy our equations now get. The only component of the electric ﬁeldthat is not zero is Ey, and all derivatives—except those with respect to x—arezero. The rest of Maxwell’s equations then become quite simple.

20-4

Let’s look next at the second of Maxwell’s equations [II of Eq. (20.12)]. Writing

out the components of the curl E, we have

(∇ × E)x = ∂Ez∂y(∇ × E)y = ∂Ex∂z(∇ × E)z = ∂Ey∂x

− ∂Ey∂z− ∂Ez∂x− ∂Ex∂y

= 0,

= 0,

= ∂Ey∂x

.

The x-component of ∇ × E is zero because the derivatives with respect to yand z are zero. The y-component is also zero; the ﬁrst term is zero because thederivative with respect to z is zero, and the second term is zero because Ez iszero. The only components of the curl of E that is not zero is the z-component,which is equal to ∂Ey/∂x. Setting the three components of ∇ × E equal to thecorresponding components of −∂B/∂t, we can conclude the following:

∂Bx∂t∂Bz∂t

= 0,

∂By∂t

= 0.

= − ∂Ey∂x

.

(20.15)

(20.16)

Since the x-component of the magnetic ﬁeld and the y-component of the magneticﬁeld both have zero time derivatives, these two components are just constantﬁelds and correspond to the magnetostatic solutions we found earlier. Somebodymay have left some permanent magnets near where the waves are propagating.We will ignore these constant ﬁelds and set Bx and By equal to zero.Incidentally, we would already have concluded that the x-component of Bshould be zero for a diﬀerent reason. Since the divergence of B is zero (from thethird Maxwell equation), applying the same arguments we used above for theelectric ﬁeld, we would conclude that the longitudinal component of the magneticﬁeld can have no variation with x. Since we are ignoring such uniform ﬁelds inour wave solutions, we would have set Bx equal to zero. In plane electromagneticwaves the B-ﬁeld, as well as the E-ﬁeld, must be directed at right angles to thedirection of propagation.

Equation (20.16) gives us the additional proposition that if the electric ﬁeldhas only a y-component, the magnetic ﬁeld will have only a z-component. So Eand B are at right angles to each other. This is exactly what happened in thespecial wave we have already considered.

We are now ready to use the last of Maxwell’s equations for free space [IV of

Eq. (20.12)]. Writing out the components, we have

c2(∇ × B)x = c2 ∂Bz∂yc2(∇ × B)y = c2 ∂Bx∂zc2(∇ × B)z = c2 ∂By∂x

− c2 ∂By∂z− c2 ∂Bz∂x− c2 ∂Bx∂y

= ∂Ex∂t= ∂Ey∂t= ∂Ez∂t

,

,

.

(20.17)

Of the six derivatives of the components of B, only the term ∂Bz/∂x is not equalto zero. So the three equations give us simply

− c2 ∂Bz∂x

= ∂Ey∂t

.

(20.18)

The result of all our work is that only one component each of the electric andmagnetic ﬁelds is not zero, and that these components must satisfy Eqs. (20.16)and (20.18). The two equations can be combined into one if we diﬀerentiate theﬁrst with respect to x and the second with respect to t; the left-hand sides of20-5

the two equations will then be the same (except for the factor c2). So we ﬁndthat Ey satisﬁes the equation

∂x2 − 1∂2Ey

c2

∂2Ey∂t2

= 0.

(20.19)

We have seen the same diﬀerential equation before, when we studied the propa-gation of sound. It is the wave equation for one-dimensional waves.

You should note that in the process of our derivation we have found somethingmore than is contained in Eq. (20.11). Maxwell’s equations have given us thefurther information that electromagnetic waves have ﬁeld components only atright angles to the direction of the wave propagation.

Let’s review what we know about the solutions of the one-dimensional wave

equation. If any quantity ψ satisﬁes the one-dimensional wave equation

∂2ψ

∂x2 − 1

c2

∂2ψ∂t2

= 0,

(20.20)

then one possible solution is a function ψ(x, t) of the form

ψ(x, t) = f(x − ct),

(20.21)that is, some function of the single variable (x − ct). The function f(x − ct)represents a「rigid」pattern in x which travels toward positive x at the speed c(see Fig. 20-4). For example, if the function f has a maximum when its argumentis zero, then for t = 0 the maximum of ψ, will occur at x = 0. At some latertime, say t = 10, ψ will have its maximum at x = 10c. As time goes on, themaximum moves toward positive x at the speed c.Sometimes it is more convenient to say that a solution of the one-dimensionalwave equation is a function of (t − x/c). However, this is saying the same thing,because any function of (t − x/c) is also a function of (x − ct):

(cid:20)− x − ct

(cid:21)

c

F(t − x/c) = F

= f(x − ct).

Let’s show that f(x− ct) is indeed a solution of the wave equation. Since it isa function of only one variable—the variable (x− ct)—we will let f0 represent thederivative of f with respect to its variable and f00 represent the second derivativeof f. Diﬀerentiating Eq. (20.21) with respect to x, we have

= f0(x − ct),

∂ψ∂x

since the derivative of (x − ct) with respect to x is 1. The second derivative of ψ,with respect to x is clearly

= f00(x − ct).Taking derivatives of ψ with respect to t, we ﬁnd

∂2ψ∂x2

(20.22)

= f0(x − ct)(−c),

∂ψ∂t∂2ψ∂t2

= +c2f00(x − ct).

(20.23)

We see that ψ does indeed satisfy the one-dimensional wave equation.You may be wondering:「If I have the wave equation, how do I know that Ishould take f(x− ct) as a solution? I don’t like this backward method. Isn’t theresome forward way to ﬁnd the solution?」Well, one good forward way is to knowthe solution. It is possible to「cook up」an apparently forward mathematicalargument, especially because we know what the solution is supposed to be, butwith an equation as simple as this we don’t have to play games. Soon you will get20-6

Fig. 20-4. The function f (x − ct) repre-sents a constant「shape」that travels towardpositive x with the speed c.

so that when you see Eq. (20.20), you nearly simultaneously see ψ = f(x − xt)as a solution. (Just as now when you see the integral of x2 dx, you know rightaway that the answer is x3/3.)Actually you should also see a little more. Not only is any function of (x− ct)a solution, but any function of (x + ct) is also a solution. Since the wave equationcontains only c2, changing the sign of c makes no diﬀerence. In fact, the mostgeneral solution of the one-dimensional wave equation is the sum of two arbitraryfunctions, one of (x − ct) and the other of (x + ct):ψ = f(x − ct) + g(x + ct).

(20.24)

The ﬁrst term represents a wave travelling toward positive x, and the secondterm an arbitrary wave travelling toward negative x. The general solution is thesuperposition of two such waves both existing at the same time.

We will leave the following amusing question for you to think about. Take a

function ψ of the following form:

ψ = cos kx cos kct.

This equation isn’t in the form of a function of (x− ct) or of (x + ct). Yet you can easilyshow that this function is a solution of the wave equation by direct substitution intoEq. (20.20). How can we then say that the general solution is of the form of Eq. (20.24)?

Applying our conclusions about the solution of the wave equation to they-component of the electric ﬁeld, Ey, we conclude that Ey can vary with x in anyarbitrary fashion. However, the ﬁelds which do exist can always be consideredas the sum of two patterns. One wave is sailing through space in one directionwith speed c, with an associated magnetic ﬁeld perpendicular to the electricﬁeld; another wave is travelling in the opposite direction with the same speed.Such waves correspond to the electromagnetic waves that we know about—light,radiowaves, infrared radiation, ultraviolet radiation, x-rays, and so on. We havealready discussed the radiation of light in great detail in Vol. I. Since everythingwe learned there applies to any electromagnetic wave, we don’t need to considerin great detail here the behavior of these waves.

We should perhaps make a few further remarks on the question of the polar-ization of the electromagnetic waves. In our solution we chose to consider thespecial case in which the electric ﬁeld has only a y-component. There is clearlyanother solution for waves travelling in the plus or minus x-direction, with anelectric ﬁeld which has only a z-component. Since Maxwell’s equations are linear,the general solution for one-dimensional waves propagating in the x-direction isthe sum of waves of Ey and waves of Ez. This general solution is summarized inthe following equations:

E = (0, Ey, Ez)Ey = f(x − ct) + g(x + ct)Ez = F(x − ct) + G(x + ct)B = (0, By, Bz)cBz = f(x − ct) − g(x + ct)cBy = −F(x − ct) + G(x + ct).

(20.25)

Such electromagnetic waves have an E-vector whose direction is not constant butwhich gyrates around in some arbitrary way in the yz-plane. At every point themagnetic ﬁeld is always perpendicular to the electric ﬁeld and to the direction ofpropagation.

If there are only waves travelling in one direction, say the positive x-direction,there is a simple rule which tells the relative orientation of the electric and20-7

magnetic ﬁelds. The rule is that the cross product E × B—which is, of course,a vector at right angles to both E and B—points in the direction in which thewave is travelling. If E is rotated into B by a right-hand screw, the screw pointsin the direction of the wave velocity. (We shall see later that the vector E × Bhas a special physical signiﬁcance: it is a vector which describes the ﬂow of energyin an electromagnetic ﬁeld.)

20-2 Three-dimensional wavesWe want now to turn to the subject of three-dimensional waves. We havealready seen that the vector E satisﬁes the wave equation. It is also easy to arriveat the same conclusion by arguing directly from Maxwell’s equations. Supposewe start with the equation

and take the curl of both sides:

∇ × E = − ∂B∂t

∇ × (∇ × E) = − ∂∂t

(∇ × B).

(20.26)

You will remember that the curl of the curl of any vector can be written as thesum of two terms, one involving the divergence and the other the Laplacian,

∇ × (∇ × E) = ∇(∇ · E) − ∇2E.

In free space, however, the divergence of E is zero, so only the Laplacian termremains. Also, from the fourth of Maxwell’s equations in free space [Eq. (20.12)]the time derivative of c2 ∇ × B is the second derivative of E with respect to t:

c2 ∂∂t

(∇ × B) = ∂2E∂t2 .

Equation (20.26) then becomes

∇2E = 1c2

∂2E∂t2 ,

which is the three-dimensional wave equation. Written out in all its glory, thisequation is, of course,

∂2E∂x2

+ ∂2E∂y2

∂z2 − 1+ ∂2E

c2

∂2E∂t2

= 0.

(20.27)

How shall we ﬁnd the general wave solution? The answer is that all thesolutions of the three-dimensional wave equation can be represented as a superpo-sition of the one-dimensional solutions we have already found. We obtained theequation for waves which move in the x-direction by supposing that the ﬁeld didnot depend on y and z. Obviously, there are other solutions in which the ﬁeldsdo not depend on x and z, representing waves going in the y-direction. Thenthere are solutions which do not depend on x and y, representing waves travellingin the z-direction. Or in general, since we have written our equations in vectorform, the three-dimensional wave equation can have solutions which are planewaves moving in any direction at all. Again, since the equations are linear, wemay have simultaneously as many plane waves as we wish, travelling in as manydiﬀerent directions. Thus the most general solution of the three-dimensionalwave equation is a superposition of all sorts of plane waves moving in all sorts ofdirections.

Try to imagine what the electric and magnetic ﬁelds look like at present inthe space in this lecture room. First of all, there is a steady magnetic ﬁeld;it comes from the currents in the interior of the earth—that is, the earth’ssteady magnetic ﬁeld. Then there are some irregular, nearly static electric ﬁeldsproduced perhaps by electric charges generated by friction as various people move20-8

about in their chairs and rub their coat sleeves against the chair arms. Thenthere are other magnetic ﬁelds produced by oscillating currents in the electricalwiring—ﬁelds which vary at a frequency of 60 cycles per second, in synchronismwith the generator at Boulder Dam. But more interesting are the electric andmagnetic ﬁelds varying at much higher frequencies. For instance, as light travelsfrom window to ﬂoor and wall to wall, there are little wiggles of the electric andmagnetic ﬁelds moving along at 186,000 miles per second. Then there are alsoinfrared waves travelling from the warm foreheads to the cold blackboard. Andwe have forgotten the ultraviolet light, the x-rays, and the radiowaves travellingthrough the room.

Flying across the room are electromagnetic waves which carry music of a jazzband. There are waves modulated by a series of impulses representing picturesof events going on in other parts of the world, or of imaginary aspirins dissolvingin imaginary stomachs. To demonstrate the reality of these waves it is onlynecessary to turn on electronic equipment that converts these waves into picturesand sounds.

If we go into further detail to analyze even the smallest wiggles, there are tinyelectromagnetic waves that have come into the room from enormous distances.There are now tiny oscillations of the electric ﬁeld, whose crests are separated bya distance of one foot, that have come from millions of miles away, transmitted tothe earth from the Mariner II space craft which has just passed Venus. Its signalscarry summaries of information it has picked up about the planets (informationobtained from electromagnetic waves that travelled from the planet to the spacecraft).

There are very tiny wiggles of the electric and magnetic ﬁelds that are waveswhich originated billions of light years away—from galaxies in the remotestcorners of the universe. That this is true has been found by「ﬁlling the room withwires」—by building antennas as large as this room. Such radiowaves have beendetected from places in space beyond the range of the greatest optical telescopes.Even they, the optical telescopes, are simply gatherers of electromagnetic waves.What we call the stars are only inferences, inferences drawn from the only physicalreality we have yet gotten from them—from a careful study of the unendinglycomplex undulations of the electric and magnetic ﬁelds reaching us on earth.

There is, of course, more: the ﬁelds produced by lightning miles away, theﬁelds of the charged cosmic ray particles as they zip through the room, and more,and more. What a complicated thing is the electric ﬁeld in the space aroundyou! Yet it always satisﬁes the three-dimensional wave equation.

20-3 Scientiﬁc imaginationI have asked you to imagine these electric and magnetic ﬁelds. What doyou do? Do you know how? How do I imagine the electric and magnetic ﬁeld?What do I actually see? What are the demands of scientiﬁc imagination? Isit any diﬀerent from trying to imagine that the room is full of invisible angels?No, it is not like imagining invisible angels. It requires a much higher degree ofimagination to understand the electromagnetic ﬁeld than to understand invisibleangels. Why? Because to make invisible angels understandable, all I have to do isto alter their properties a little bit—I make them slightly visible, and then I cansee the shapes of their wings, and bodies, and halos. Once I succeed in imagininga visible angel, the abstraction required—which is to take almost invisible angelsand imagine them completely invisible—is relatively easy. So you say,「Professor,please give me an approximate description of the electromagnetic waves, eventhough it may be slightly inaccurate, so that I too can see them as well as Ican see almost invisible angels. Then I will modify the picture to the necessaryabstraction.」

I’m sorry I can’t do that for you. I don’t know how. I have no picture ofthis electromagnetic ﬁeld that is in any sense accurate. I have known aboutthe electromagnetic ﬁeld a long time—I was in the same position 25 years agothat you are now, and I have had 25 years more of experience thinking about20-9

these wiggling waves. When I start describing the magnetic ﬁeld moving throughspace, I speak of the E- and B-ﬁelds and wave my arms and you may imaginethat I can see them. I’ll tell you what I see. I see some kind of vague shadowy,wiggling lines—here and there is an E and B written on them somehow, andperhaps some of the lines have arrows on them—an arrow here or there whichdisappears when I look too closely at it. When I talk about the ﬁelds swishingthrough space, I have a terrible confusion between the symbols I use to describethe objects and the objects themselves. I cannot really make a picture that iseven nearly like the true waves. So if you have some diﬃculty in making such apicture, you should not be worried that your diﬃculty is unusual.

Our science makes terriﬁc demands on the imagination. The degree ofimagination that is required is much more extreme than that required for someof the ancient ideas. The modern ideas are much harder to imagine. We use a lotof tools, though. We use mathematical equations and rules, and make a lot ofpictures. What I realize now is that when I talk about the electromagnetic ﬁeld inspace, I see some kind of a superposition of all of the diagrams which I’ve ever seendrawn about them. I don’t see little bundles of ﬁeld lines running about becauseit worries me that if I ran at a diﬀerent speed the bundles would disappear, Idon’t even always see the electric and magnetic ﬁelds because sometimes I thinkI should have made a picture with the vector potential and the scalar potential,for those were perhaps the more physically signiﬁcant things that were wiggling.Perhaps the only hope, you say, is to take a mathematical view. Now what isa mathematical view? From a mathematical view, there is an electric ﬁeld vectorand a magnetic ﬁeld vector at every point in space; that is, there are six numbersassociated with every point. Can you imagine six numbers associated with eachpoint in space? That’s too hard. Can you imagine even one number associatedwith every point? I cannot! I can imagine such a thing as the temperature atevery point in space. That seems to be understandable. There is a hotness andcoldness that varies from place to place. But I honestly do not understand theidea of a number at every point.So perhaps we should put the question: Can we represent the electric ﬁeldby something more like a temperature, say like the displacement of a piece ofjello? Suppose that we were to begin by imagining that the world was ﬁlled withthin jello and that the ﬁelds represented some distortion—say a stretching ortwisting—of the jello. Then we could visualize the ﬁeld. After we「see」what it islike we could abstract the jello away. For many years that’s what people tried todo. Maxwell, Ampère, Faraday, and others tried to understand electromagnetismthis way. (Sometimes they called the abstract jello「ether.」) But it turned outthat the attempt to imagine the electromagnetic ﬁeld in that way was reallystanding in the way of progress. We are unfortunately limited to abstractions, tousing instruments to detect the ﬁeld, to using mathematical symbols to describethe ﬁeld, etc. But nevertheless, in some sense the ﬁelds are real, because after weare all ﬁnished ﬁddling around with mathematical equations—with or withoutmaking pictures and drawings or trying to visualize the thing—we can still makethe instruments detect the signals from Mariner II and ﬁnd out about galaxies abillion miles away, and so on.

The whole question of imagination in science is often misunderstood by peoplein other disciplines. They try to test our imagination in the following way. Theysay,「Here is a picture of some people in a situation. What do you imagine willhappen next?」When we say,「I can’t imagine,」they may think we have a weakimagination. They overlook the fact that whatever we are allowed to imagine inscience must be consistent with everything else we know: that the electric ﬁeldsand the waves we talk about are not just some happy thoughts which we arefree to make as we wish, but ideas which must be consistent with all the lawsof physics we know. We can’t allow ourselves to seriously imagine things whichare obviously in contradiction to the known laws of nature. And so our kind ofimagination is quite a diﬃcult game. One has to have the imagination to thinkof something that has never been seen before, never been heard of before. Atthe same time the thoughts are restricted in a strait jacket, so to speak, limited20-10

by the conditions that come from our knowledge of the way nature really is.The problem of creating something which is new, but which is consistent witheverything which has been seen before, is one of extreme diﬃculty.

While I’m on this subject I want to talk about whether it will ever be possibleto imagine beauty that we can’t see. It is an interesting question. When we lookat a rainbow, it looks beautiful to us. Everybody says,「Ooh, a rainbow.」(Yousee how scientiﬁc I am. I am afraid to say something is beautiful unless I havean experimental way of deﬁning it.) But how would we describe a rainbow if wewere blind? We are blind when we measure the infrared reﬂection coeﬃcientof sodium chloride, or when we talk about the frequency of the waves that arecoming from some galaxy that we can’t see—we make a diagram, we make a plot.For instance, for the rainbow, such a plot would be the intensity of radiationvs. wavelength measured with a spectrophotometer for each direction in the sky.Generally, such measurements would give a curve that was rather ﬂat. Thensome day, someone would discover that for certain conditions of the weather, andat certain angles in the sky, the spectrum of intensity as a function of wavelengthwould behave strangely; it would have a bump. As the angle of the instrumentwas varied only a little bit, the maximum of the bump would move from onewavelength to another. Then one day the physical review of the blind men mightpublish a technical article with the title「The Intensity of Radiation as a Functionof Angle under Certain Conditions of the Weather.」In this article there mightappear a graph such as the one in Fig. 20-5. The author would perhaps remarkthat at the larger angles there was more radiation at long wavelengths, whereasfor the smaller angles the maximum in the radiation came at shorter wavelengths.(From our point of view, we would say that the light at 40◦ is predominantlygreen and the light at 42◦ is predominantly red.)

Fig. 20-5. The intensity of electromag-netic waves as a function of wavelength forthree angles (measured from the directionopposite the sun), observed only with cer-tain meteorological conditions.

Now do we ﬁnd the graph of Fig. 20-5 beautiful? It contains much more detailthan we apprehend when we look at a rainbow, because our eyes cannot see theexact details in the shape of a spectrum. The eye, however, ﬁnds the rainbowbeautiful. Do we have enough imagination to see in the spectral curves the samebeauty we see when we look directly at the rainbow? I don’t know.

But suppose I have a graph of the reﬂection coeﬃcient of a sodium chloridecrystal as a function of wavelength in the infrared, and also as a function of angle.I would have a representation of how it would look to my eyes if they could see inthe infrared—perhaps some glowing, shiny「green,」mixed with reﬂections fromthe surface in a「metallic red.」That would be a beautiful thing, but I don’t knowwhether I can ever look at a graph of the reﬂection coeﬃcient of NaCl measuredwith some instrument and say that it has the same beauty.

On the other hand, even if we cannot see beauty in particular measuredresults, we can already claim to see a certain beauty in the equations whichdescribe general physical laws. For example, in the wave equation (20.9), there’ssomething nice about the regularity of the appearance of the x, the y, the z, andthe t. And this nice symmetry in appearance of the x, y, z, and t suggests tothe mind still a greater beauty which has to do with the four dimensions, thepossibility that space has four-dimensional symmetry, the possibility of analyzingthat and the developments of the special theory of relativity. So there is plentyof intellectual beauty associated with the equations.

20-11

20-4 Spherical wavesWe have seen that there are solutions of the wave equation which correspondto plane waves, and that any electromagnetic wave can be described as a su-perposition of many plane waves. In certain special cases, however, it is moreconvenient to describe the wave ﬁeld in a diﬀerent mathematical form. We wouldlike to discuss now the theory of spherical waves—waves which correspond tospherical surfaces that are spreading out from some center. When you drop astone into a lake, the ripples spread out in circular waves on the surface—theyare two-dimensional waves. A spherical wave is a similar thing except that itspreads out in three dimensions.

Before we start describing spherical waves, we need a little mathematics.Suppose we have a function that depends only on the radial distance r from acertain origin—in other words, a function that is spherically symmetric. Let’scall the function ψ(r), where by r we mean

r =p

x2 + y2 + z2,

the radial distance from the origin. In order to ﬁnd out what functions ψ(r)satisfy the wave equation, we will need an expression for the Laplacian of ψ. Sowe want to ﬁnd the sum of the second derivatives of ψ with respect to x, y, and z.We will use the notation that ψ0(r) represents the derivative of ψ with respectto r and ψ00(r) represents the second derivative of ψ with respect to r.

First, we ﬁnd the derivatives with respect to x. The ﬁrst derivative is

= ψ0(r) ∂r∂xThe second derivative of ψ with respect to x is

.

∂ψ(r)∂x

= ψ00(cid:18) ∂r

(cid:19)2

∂x

∂2ψ∂x2

We can evaluate the partial derivatives of r with respect to x from

∂r∂x

= xr

,

∂2r∂x2

= 1(cid:18)So the second derivative of ψ with respect to x is1 − x2(cid:18)r21 − y2(cid:18)r21 − z2r2

r2 ψ00 + 1= x2r2 ψ00 + 1= y2r2 ψ00 + 1= z2

∂2ψ∂y2∂2ψ∂z2

Likewise,

∂2ψ∂x2

r

r

r

(cid:19)

r

+ ψ0 ∂2r∂x2 .(cid:18)1 − x2r2(cid:19)(cid:19)(cid:19)

ψ0.

ψ0,

ψ0.

.

(20.28)

(20.29)

(20.30)

The Laplacian is the sum of these three derivatives. Remembering that

x2 + y2 + z2 = r2, we get

∇2ψ(r) = ψ00(r) + 2

r

ψ0(r).

It is often more convenient to write this equation in the following form:

∇2ψ(r) = 1

r

d2dr2

(rψ).

(20.31)

(20.32)

If you carry out the diﬀerentiation indicated in Eq. (20.32), you will see that theright-hand side is the same as in Eq. (20.31).

If we wish to consider spherically symmetric ﬁelds which can propagate asspherical waves, our ﬁeld quantity must be a function of both r and t. Suppose20-12

we ask, then, what functions ψ(r, t) are solutions of the three-dimensional waveequation

∇2ψ(r, t) − 1c2

(20.33)Since ψ(r, t) depends only on the spatial coordinates through r, we can use theequation for the Laplacian we found above, Eq. (20.32). To be precise, however,since ψ is also a function of t, we should write the derivatives with respect to ras partial derivatives. Then the wave equation becomes

∂2∂t2 ψ(r, t) = 0.

1r

∂2∂r2

(rψ) − 1c2

∂2∂t2 ψ = 0.

We must now solve this equation, which appears to be much more complicatedthan the plane wave case. But notice that if we multiply this equation by r, weget

∂2∂r2

(rψ) − 1c2

∂2∂t2

(rψ) = 0.

(20.34)This equation tells us that the function rψ satisﬁes the one-dimensional waveequation in the variable r. Using the general principle which we have emphasizedso often, that the same equations always have the same solutions, we know thatif rψ is a function only of (r − ct) then it will be a solution of Eq. (20.34). So weknow that spherical waves must have the form

rψ(r, t) = f(r − ct).

Or, as we have seen before, we can equally well say that rψ can have the form

rψ = f(t − r/c).

ψ = f(t − r/c)

Dividing by r, we ﬁnd that the ﬁeld quantity ψ (whatever it may be) has thefollowing form:

.

r

(20.35)Such a function represents a general spherical wave travelling outward from theorigin at the speed c. If we forget about the r in the denominator for a moment,the amplitude of the wave as a function of the distance from the origin at agiven time has a certain shape that travels outward at the speed c. The factor rin the denominator, however, says that the amplitude of the wave decreases inproportion to 1/r as the wave propagates. In other words, unlike a plane wavein which the amplitude remains constant as the wave runs along, in a sphericalwave the amplitude steadily decreases, as shown in Fig. 20-6. This eﬀect is easyto understand from a simple physical argument.

Fig. 20-6. A spherical wave ψ = f (t − r /c)/r. (a) ψ as a function of r for t = t1 and the same wave

for the later time t2. (b) ψ as a function of t for r = r1 and the same wave seen at r2.

20-13

We know that the energy density in a wave depends on the square of the waveamplitude. As the wave spreads, its energy is spread over larger and larger areasproportional to the radial distance squared. If the total energy is conserved, theenergy density must fall as 1/r2, and the amplitude of the wave must decreaseas 1/r. So Eq. (20.35) is the「reasonable」form for a spherical wave.

We have disregarded the second possible solution to the one-dimensional wave

equation:

or

rψ = g(t + r/c),ψ = g(t + r/c)

.

r

This also represents a spherical wave, but one which travels inward from large rtoward the origin.

We are now going to make a special assumption. We say, without anydemonstration whatever, that the waves generated by a source are only the waveswhich go outward. Since we know that waves are caused by the motion of charges,we want to think that the waves proceed outward from the charges. It would berather strange to imagine that before charges were set in motion, a spherical wavestarted out from inﬁnity and arrived at the charges just at the time they beganto move. That is a possible solution, but experience shows that when chargesare accelerated the waves travel outward from the charges. Although Maxwell’sequations would allow either possibility, we will put in an additional fact—basedon experience—that only the outgoing wave solution makes「physical sense.」

We should remark, however, that there is an interesting consequence to thisadditional assumption: we are removing the symmetry with respect to time thatexists in Maxwell’s equations. The original equations for E and B, and alsothe wave equations we derived from them, have the property that if we changethe sign of t, the equation is unchanged. These equations say that for everysolution corresponding to a wave going in one direction there is an equally validsolution for a wave travelling in the opposite direction. Our statement that we willconsider only the outgoing spherical waves is an important additional assumption.(A formulation of electrodynamics in which this additional assumption is avoidedhas been carefully studied. Surprisingly, in many circumstances it does not leadto physically absurd conclusions, but it would take us too far astray to discussthese ideas just now. We will talk about them a little more in Chapter 28.)

We must mention another important point. In our solution for an outgoingwave, Eq. (20.35), the function ψ is inﬁnite at the origin. That is somewhatpeculiar. We would like to have a wave solution which is smooth everywhere.Our solution must represent physically a situation in which there is some sourceat the origin. In other words, we have inadvertently made a mistake. We havenot solved the free wave equation (20.33) everywhere; we have solved Eq. (20.33)with zero on the right everywhere, except at the origin. Our mistake crept inbecause some of the steps in our derivation are not「legal」when r = 0.

Let’s show that it is easy to make the same kind of mistake in an electrostaticproblem. Suppose we want a solution of the equation for an electrostatic potentialin free space, ∇2φ = 0. The Laplacian is equal to zero, because we are assumingthat there are no charges anywhere. But what about a spherically symmetricsolution to this equation—that is, some function φ that depends only on r. Usingthe formula of Eq. (20.32) for the Laplacian, we have

1r

d2dr2

(rφ) = 0.

Multiplying this equation by r, we have an equation which is readily integrated:

d2dr2

(rφ) = 0.

If we integrate once with respect to r, we ﬁnd that the ﬁrst derivative of rφ is a20-14

constant, which we may call a:

(rφ) = a.

ddr

Integrating again, we ﬁnd that rφ is of the form

rφ = ar + b,

where b is another constant of integration. So we have found that the following φis a solution for the electrostatic potential in free space:

φ = a + br

.

Something is evidently wrong.

In the region where there are no electriccharges, we know the solution for the electrostatic potential: the potential iseverywhere a constant. That corresponds to the ﬁrst term in our solution. Butwe also have the second term, which says that there is a contribution to thepotential that varies as one over the distance from the origin. We know, however,that such a potential corresponds to a point charge at the origin. So, althoughwe thought we were solving for the potential in free space, our solution also givesthe ﬁeld for a point source at the origin. Do you see the similarity between whathappened now and what happened when we solved for a spherically symmetricsolution to the wave equation? If there were really no charges or currents atthe origin, there would not be spherical outgoing waves. The spherical wavesmust, of course, be produced by sources at the origin. In the next chapter wewill investigate the connection between the outgoing electromagnetic waves andthe currents and voltages which produce them.

20-15

21

Solutions of Maxwell’s Equations withCurrents and Charges

