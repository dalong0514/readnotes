Algebra

22-1 Addition and multiplicationIn our study of oscillating systems we shall have occasion to use one of themost remarkable, almost astounding, formulas in all of mathematics. From thephysicist’s point of view we could bring forth this formula in two minutes orso, and be done with it. But science is as much for intellectual enjoyment asfor practical utility, so instead of just spending a few minutes on this amazingjewel, we shall surround the jewel by its proper setting in the grand design ofthat branch of mathematics which is called elementary algebra.

Now you may ask,「What is mathematics doing in a physics lecture?」Wehave several possible excuses: ﬁrst, of course, mathematics is an important tool,but that would only excuse us for giving the formula in two minutes. On theother hand, in theoretical physics we discover that all our laws can be written inmathematical form; and that this has a certain simplicity and beauty about it.So, ultimately, in order to understand nature it may be necessary to have a deeperunderstanding of mathematical relationships. But the real reason is that thesubject is enjoyable, and although we humans cut nature up in diﬀerent ways, andwe have diﬀerent courses in diﬀerent departments, such compartmentalization isreally artiﬁcial, and we should take our intellectual pleasures where we ﬁnd them.Another reason for looking more carefully at algebra now, even though mostof us studied algebra in high school, is that that was the ﬁrst time we studied it;all the equations were unfamiliar, and it was hard work, just as physics is now.Every so often it is a great pleasure to look back to see what territory has beencovered, and what the great map or plan of the whole thing is. Perhaps some daysomebody in the Mathematics Department will present a lecture on mechanics insuch a way as to show what it was we were trying to learn in the physics course!The subject of algebra will not be developed from the point of view of amathematician, exactly, because the mathematicians are mainly interested in howvarious mathematical facts are demonstrated, and how many assumptions areabsolutely required, and what is not required. They are not so interested in the

22-1

result of what they prove. For example, we may ﬁnd the Pythagorean theoremquite interesting, that the sum of the squares of the sides of a right triangle isequal to the square of the hypotenuse; that is an interesting fact, a curiouslysimple thing, which may be appreciated without discussing the question of howto prove it, or what axioms are required. So, in the same spirit, we shall describequalitatively, if we may put it that way, the system of elementary algebra. Wesay elementary algebra because there is a branch of mathematics called modernalgebra in which some of the rules such as ab = ba, are abandoned, and it is stillcalled algebra, but we shall not discuss that.To discuss this subject we start in the middle. We suppose that we alreadyknow what integers are, what zero is, and what it means to increase a numberby one unit. You may say,「That is not in the middle!」But it is the middle froma mathematical standpoint, because we could go even further back and describethe theory of sets in order to derive some of these properties of integers. But weare not going in that direction, the direction of mathematical philosophy andmathematical logic, but rather in the other direction, from the assumption thatwe know what integers are and we know how to count.

If we start with a certain number a, an integer, and we count successivelyone unit b times, the number we arrive at we call a + b, and that deﬁnes additionof integers.Once we have deﬁned addition, then we can consider this: if we start withnothing and add a to it, b times in succession, we call the result multiplication ofintegers; we call it b times a.Now we can also have a succession of multiplications: if we start with 1 andmultiply by a, b times in succession, we call that raising to a power: ab.Now as a consequence of these deﬁnitions it can be easily shown that all ofthe following relationships are true:

(a) a + b = b + aab = ba(c)(e)(ab)c = a(bc)(g) abac = a(b+c)(i)(k) a1 = a

a + 0 = a

(b) a + (b + c) = (a + b) + c(d) a(b + c) = ab + ac(f)(h)(j)

(ab)c = acbc(ab)c = a(bc)a · 1 = a

(22.1)

These results are well known and we shall not belabor the point, we merely list

22-2

them. Of course, 1 and 0 have special properties; for example, a + 0 is a, a times1 = a, and a to the ﬁrst power is a.In this discussion we must also assume a few other properties like continuityand ordering, which are very hard to deﬁne; we will let the rigorous theory do it.Furthermore, it is deﬁnitely true that we have written down too many「rules」;some of them may be deducible from the others, but we shall not worry aboutsuch matters.

22-2 The inverse operationsIn addition to the direct operations of addition, multiplication, and raising toa power, we have also the inverse operations, which are deﬁned as follows. Let usassume that a and c are given, and that we wish to ﬁnd what values of b satisfysuch equations as a+ b = c, ab = c, ba = c. If a+ b = c, b is deﬁned as c− a, whichis called subtraction. The operation called division is also clear: if ab = c, thenb = c/a deﬁnes division—a solution of the equation ab = c「backwards.」Now ifwe have a power ba = c and we ask ourselves,「What is b?,」it is called the ath root√of c: b = ac. For instance, if we ask ourselves the following question,「Whatinteger, raised to the third power, equals 8?,」then the answer is called the cuberoot of 8; it is 2. Because ba and ab are not equal, there are two inverse problemsassociated with powers, and the other inverse problem would be,「To what powermust we raise 2 to get 8?」This is called taking the logarithm. If ab = c, we writea c. The fact that it has a cumbersome notation relative to the others doesb = lognot mean that it is any less elementary, at least applied to integers, than the otherprocesses. Although logarithms come late in an algebra class, in practice they are,of course, just as simple as roots; they are just a diﬀerent kind of solution of analgebraic equation. The direct and inverse operations are summarized as follows:

(a)

additiona + b = c

(b) multiplication

ab = c(c) powerba = c(d) powerab = c

22-3

(a0)

subtractionb = c − a(b0) divisionb = c/aroot√b = alogarithmb = log

(d0)

(c0)

c

a c

(22.2)

Now here is the idea. These relationships, or rules, are correct for integers,since they follow from the deﬁnitions of addition, multiplication, and raising to apower. We are going to discuss whether or not we can broaden the class of objectswhich a, b, and c represent so that they will obey these same rules, although theprocesses for a + b, and so on, will not be deﬁnable in terms of the direct actionof adding 1, for instance, or successive multiplications by integers.

22-3 Abstraction and generalizationWhen we try to solve simple algebraic equations using all these deﬁnitions,we soon discover some insoluble problems, such as the following. Suppose thatwe try to solve the equation b = 3 − 5. That means, according to our def-inition of subtraction, that we must ﬁnd a number which, when added to 5,gives 3. And of course there is no such number, because we consider onlypositive integers; this is an insoluble problem. However, the plan, the greatidea, is this: abstraction and generalization. From the whole structure of al-gebra, rules plus integers, we abstract the original deﬁnitions of addition andmultiplication, but we leave the rules (22.1) and (22.2), and assume these tobe true in general on a wider class of numbers, even though they are originallyderived on a smaller class. Thus, rather than using integers symbolically todeﬁne the rules, we use the rules as the deﬁnition of the symbols, which thenrepresent a more general kind of number. As an example, by working withthe rules alone we can show that 3 − 5 = 0 − 2.In fact we can show thatone can make all subtractions, provided we deﬁne a whole set of new num-bers: 0 − 1, 0 − 2, 0 − 3, 0 − 4, and so on, called the negative integers. Thenwe may use all the other rules, like a(b + c) = ab + ac and so forth, to ﬁndwhat the rules are for multiplying negative numbers, and we will discover, infact, that all of the rules can be maintained with negative as well as positiveintegers.

So we have increased the range of objects over which the rules work, but themeaning of the symbols is diﬀerent.One cannot say, for instance, that −2 times 5 really means to add 5 togethersuccessively −2 times. That means nothing. But nevertheless everything willwork out all right according to the rules.An interesting problem comes up in taking powers. Suppose that we wishto discover what a(3−5) means. We know only that 3 − 5 is a solution of theproblem, (3 − 5) + 5 = 3. Knowing that, we know that a(3−5)a5 = a3. Therefore

22-4

a(3−5) = a3/a5, by the deﬁnition of division. With a little more work, this canbe reduced to 1/a2. So we ﬁnd that the negative powers are the reciprocals ofthe positive powers, but 1/a2 is a meaningless symbol, because if a is a positiveor negative integer, the square of it is greater than 1, and we do not yet knowwhat we mean by 1 divided by a number greater than 1!

Onward! The great plan is to continue the process of generalization; wheneverwe ﬁnd another problem that we cannot solve we extend our realm of numbers.Consider division: we cannot ﬁnd a number which is an integer, even a negativeinteger, which is equal to the result of dividing 3 by 5. But if we suppose that allfractional numbers also satisfy the rules, then we can talk about multiplying andadding fractions, and everything works as well as it did before.

Take another example of powers: what is a3/5? We know only that (3/5)5 = 3,since that was the deﬁnition of 3/5. So we know also that (a(3/5))5 = a(3/5)(5) =a3, because this is one of the rules. Then by the deﬁnition of roots we ﬁnd thata(3/5) = 5√In this way, then, we can deﬁne what we mean by putting fractions in thevarious symbols, by using the rules themselves to help us determine the deﬁnition—it is not arbitrary. It is a remarkable fact that all the rules still work for positiveand negative integers, as well as for fractions!We go on in the process of generalization. Are there any other equationswe cannot solve? Yes, there are. For example, it is impossible to solve thisequation: b = 21/2 = √2. It is impossible to ﬁnd a number which is rational (afraction) whose square is equal to 2. It is very easy for us in modern days toanswer this question. We know the decimal system, and so we have no diﬃcultyin appreciating the meaning of an unending decimal as a type of approximationto the square root of 2. Historically, this idea presented great diﬃculty to theGreeks. To really deﬁne precisely what is meant here requires that we add somesubstance of continuity and ordering, and it is, in fact, quite the most diﬃcultstep in the processes of generalization just at this point. It was made, formallyand rigorously, by Dedekind. However, without worrying about the mathematicalrigor of the thing, it is quite easy to understand that what we mean is that we aregoing to ﬁnd a whole sequence of approximate fractions, perfect fractions (becauseany decimal, when stopped somewhere, is of course rational), which just keepson going, getting closer and closer to the desired result. That is good enoughfor what we wish to discuss, and it permits us to involve ourselves in irrationalnumbers, and to calculate things like the square root of 2 to any accuracy thatwe desire, with enough work.

a3.

22-5

22-4 Approximating irrational numbersThe next problem comes with what happens with the irrational powers.√Suppose that we want to deﬁne, for instance, 102. In principle, the answer issimple enough. If we approximate the square root of 2 to a certain number ofdecimal places, then the power is rational, and we can take the approximate root,√using the above method, and get an approximation to 102. Then we may run itup a few more decimal places (it is again rational), take the appropriate root,this time a much higher root because there is a much bigger denominator in thefraction, and get a better approximation. Of course we are going to get someenormously high roots involved here, and the work is quite diﬃcult. How can wecope with this problem?

In the computations of square roots, cube roots, and other small roots, thereis an arithmetical process available by which we can get one decimal place afteranother. But the amount of labor needed to calculate irrational powers andthe logarithms that go with them (the inverse problem) is so great that thereis no simple arithmetical process we can use. Therefore tables have been builtup which permit us to calculate these powers, and these are called the tablesof logarithms, or the tables of powers, depending on which way the table is setup. It is merely a question of saving time; if we must raise some number to anirrational power, we can look it up rather than having to compute it. Of course,such a computation is just a technical problem, but it is an interesting one, andof great historical value. In the ﬁrst place, not only do we have the problem ofsolving x = 102, but we also have the problem of solving 10x = 2, or x = log10 2.This is not a problem where we have to deﬁne a new kind of number for theresult, it is merely a computational problem. The answer is simply an irrationalnumber, an unending decimal, not a new kind of a number.

Let us now discuss the problem of calculating solutions of such equations.The general idea is really very simple. If we could calculate 101, and 104/10, and101/100, and 104/1000 and so on, and multiply them all together, we would get101.414... or 102, and that is the general idea on which things work. But insteadof calculating 101/10 and so on, we shall calculate 101/2, 101/4, and so on. Beforewe start, we should explain why we make so much work with 10, instead of someother number. Of course, we realize that logarithm tables are of great practicalutility, quite aside from the mathematical problem of taking roots, since withany base at all,

√

√

(22.3)

log

(ac) = log

b a + log

b c.

b

22-6

We are all familiar with the fact that one can use this fact in a practical way tomultiply numbers if we have a table of logarithms. The only question is, withwhat base b shall we compute? It makes no diﬀerence what base is used; wecan use the same principle all the time, and if we are using logarithms to anyparticular base, we can ﬁnd logarithms to any other base merely by a changein scale, a multiplying factor. If we multiply Eq. (22.3) by 61, it is just as true,and if we had a table of logs with a base b, and somebody else multiplied all ofour table by 61, there would be no essential diﬀerence. Suppose that we knowthe logarithms of all the numbers to the base b. In other words, we can solvethe equation ba = c for any c because we have a table. The problem is to ﬁndthe logarithm of the same number c to some other base, let us say the base x.We would like to solve xa0 = c. It is easy to do, because we can always writex = bt, which deﬁnes t, knowing x and b. As a matter of fact, t = logb x. Thenif we put that in and solve for a0, we see that (bt)a0 = ba0t = c. In other words,ta0 is the logarithm of c in base b. Thus a0 = a/t. Thus logs to base x are just1/t, which is a constant, times the logs to the base, b. Therefore any log table isequivalent to any other log table if we multiply by a constant, and the constantis 1/ logb x. This permits us to choose a particular base, and for convenience wetake the base 10. (The question may arise as to whether there is any naturalbase, any base in which things are somehow simpler, and we shall try to ﬁnd ananswer to that later. At the moment we shall just use the base 10.)

Now let us see how to calculate logarithms. We begin by computing successivesquare roots of 10, by cut and try. The results are shown in Table 22-1. Thepowers of 10 are given in the ﬁrst column, and the result, 10s, is given in thethird column. Thus 101 = 10. The one-half power of 10 we can easily work out,because that is the square root of 10, and there is a known, simple process fortaking square roots of any number.* Using this process, we ﬁnd the ﬁrst squareroot to be 3.16228. What good is that? It already tells us something, it tellsus how to take 100.5, so we now know at least one logarithm, if we happen toneed the logarithm of 3.16228, we know the answer is close to 0.50000. But wemust do a little bit better than that; we clearly need more information. So wetake the square root again, and ﬁnd 101/4, which is 1.77828. Now we have thelogarithm of more numbers than we had before, 1.250 is the logarithm of 17.78* There is a deﬁnite arithmetic procedure, but the easiest way to ﬁnd the square root of anynumber N is to choose some a fairly close, ﬁnd N/a, average a0 = 12 [a + (N/a)], and use thisaverage a0 for the next choice for a. The convergence is very rapid—the number of signiﬁcantﬁgures doubles each time.

22-7

Table 22-1

Successive Square Roots of Ten

Power s

1024 s

10s

(10s − 1)/s

10245122561286432168421

10.000003.162281.778281.333521.154781.0746071.0366331.0181521.00903501.00450731.0022511

11/21/41/81/161/321/641/1281/2561/5121/1024

∆/1024(∆ → 0)

9.004.323.1132.6682.4762.38742.34452.32342112.31301042.3077 532.3051 26

y 26

∆ 1 + 0.0022486∆←−2.3025

and, incidentally, if it happens that somebody asks for 100.75, we can get it,because that is 10(0.5+0.25); it is therefore the product of the second and thirdnumbers. If we can get enough numbers in column s to be able to make upalmost any number, then by multiplying the proper things in column 3, we canget 10 to any power; that is the plan. So we evaluate ten successive square rootsof 10, and that is the main work which is involved in the calculations.

Why don’t we keep on going for more and more accuracy? Because we beginto notice something. When we raise 10 to a very small power, we get 1 plusa small amount. The reason for this is clear, because we are going to have totake the 1000th power of 101/1000 to get back to 10, so we had better not startwith too big a number; it has to be close to 1. What we notice is that the smallnumbers that are added to 1 begin to look as though we are merely dividingby 2 each time; we see 1815 becomes 903, then 450, 225; so it is clear that, to anexcellent approximation, if we take another root, we shall get 1.00112 something,and rather than actually take all the square roots, we guess at the ultimatelimit. When we take a small fraction ∆/1024 as ∆ approaches zero, what willthe answer be? Of course it will be some number close to 1 + 0.0022511 ∆. Not

22-8

exactly 1 + 0.0022511 ∆, however—we can get a better value by the followingtrick: we subtract the 1, and then divide by the power s. This ought to correctall the excesses to the same value. We see that they are very closely equal. Atthe top of the table they are not equal, but as they come down, they get closerand closer to a constant value. What is the value? Again we look to see how theseries is going, how it has changed with s. It changed by 211, by 104, by 53, by26. These changes are obviously half of each other, very closely, as we go down.Therefore, if we kept going, the changes would be 13, 7, 3, 2 and 1, more or less,or a total of 26. Thus we have only 26 more to go, and so we ﬁnd that the truenumber is 2.3025. (Actually, we shall later see that the exact number shouldbe 2.3026, but to keep it realistic, we shall not alter anything in the arithmetic.)From this table we can now calculate any power of 10, by compounding the powerout of 1024ths.

Let us now actually calculate a logarithm, because the process we shall use iswhere logarithm tables actually come from. The procedure is shown in Table 22-2,and the numerical values are shown in Table 22-1 (columns 2 and 3).

Table 22-2

Calculation of a logarithm: log10 2

2 ÷ 1.77828 = 1.1246821.124682 ÷ 1.074607 = 1.046598, etc.∴ 2 = (1.77828)(1.074607)(1.036633)(1.0090350)(1.000573)

(cid:20) 1

(cid:21)(cid:18) 5731024(256 + 32 + 16 + 4 + 0.254)

= 10

= 100.30103

(cid:21)

(cid:20)308.254(cid:19)2249 = 0.254

= 10

1024

∴ log10 2 = 0.30103

Suppose we want the logarithm of 2. That is, we want to know to what powerwe must raise 10 to get 2. Can we raise 10 to the 1/2 power? No; that is too big.In other words, we can see that the answer is going to be bigger than 1/4, andless than 1/2. Let us take the factor 101/4 out; we divide 2 by 1.778 . . . , and get1.124 . . . , and so on, and now we know that we have taken away 0.250000 fromthe logarithm. The number 1.124 . . . , is now the number whose logarithm weneed. When we are ﬁnished we shall add back the 1/4, or 256/1024. Now we

22-9

look in the table for the next number just below 1.124 . . . , and that is 1.074607.We therefore divide by 1.074607 and get 1.046598. From that we discover that 2can be made up of a product of numbers that are in Table 22-1, as follows:

2 = (1.77828)(1.074607)(1.036633)(1.0090350)(1.000573).

There was one factor (1.000573) left over, naturally, which is beyond the range ofour table. To get the logarithm of this factor, we use our result that 10∆/1024 ≈1 + 2.3025∆/1024. We ﬁnd ∆ = 0.254. Therefore our answer is 10 to thefollowing power: (256 + 32 + 16 + 4 + 0.254)/1024. Adding those together, we get308.254/1024. Dividing, we get 0.30103, so we know that the log10 2 = 0.30103,which happens to be right to 5 ﬁgures!This is how logarithms were originally computed by Mr. Briggs of Halifax,in 1620. He said,「I computed successively 54 square roots of 10.」We know hereally computed only the ﬁrst 27, because the rest of them can be obtained by thistrick with ∆. His work involved calculating the square root of 10 twenty-seventimes, which is not much more than the ten times we did; however, it was morework because he calculated to sixteen decimal places, and then reduced his answerto fourteen when he published it, so that there were no rounding errors. Hemade tables of logarithms to fourteen decimal places by this method, which isquite tedious. But all logarithm tables for three hundred years were borrowedfrom Mr. Briggs’ tables by reducing the number of decimal places. Only inmodern times, with the WPA and computing machines, have new tables beenindependently computed. There are much more eﬃcient methods of computinglogarithms today, using certain series expansions.

In the above process, we discovered something rather interesting, and thatis that for very small powers  we can calculate 10 easily; we have discoveredthat 10 = 1 + 2.3025, by sheer numerical analysis. Of course this also meansthat 10n/2.3025 = 1 + n if n is very small. Now logarithms to any other baseare merely multiples of logarithms to the base 10. The base 10 was used onlybecause we have 10 ﬁngers, and the arithmetic of it is easy, but if we ask for amathematically natural base, one that has nothing to do with the number ofﬁngers on human beings, we might try to change our scale of logarithms in someconvenient and natural manner, and the method which people have chosen isto redeﬁne the logarithms by multiplying all the logarithms to the base 10 by2.3025 . . . This then corresponds to using some other base, and this is called thenatural base, or base e. Note that log

(1 + n) ≈ n, or en ≈ 1 + n as n → 0.

e

22-10

It is easy enough to ﬁnd out what e is: e = 101/2.3025 or 100.434294..., anirrational power. Our table of the successive square roots of 10 can be usedto compute, not just logarithms, but also 10 to any power, so let us use it tocalculate this natural base e. For convenience we transform 0.434294 . . . into444.73/1024. Now, 444.73 is 256 + 128 + 32 + 16 + 8 + 4 + 0.73. Therefore e,since it is an exponent of a sum, will be a product of the numbers

(1.77828)(1.33352)(1.074607)(1.036633)(1.018152)(1.009035)(1.001643) = 2.7184.(The only problem is the last one, which is 0.73, and which is not in the table,but we know that if ∆ is small enough, the answer is 1 + 2.3025 ∆.) When wemultiply all these together, we get 2.7184 (it should be 2.7183, but it is goodenough). The use of such tables, then, is the way in which irrational powers andthe logarithms of irrational numbers are all calculated. That takes care of theirrationals.

22-5 Complex numbersNow it turns out that after all that work we still cannot solve every equation!For instance, what is the square root of −1? Suppose we have to ﬁnd x2 = −1.The square of no rational, of no irrational, of nothing that we have discovered sofar, is equal to −1. So we again have to generalize our numbers to a still widerclass. Let us suppose that a speciﬁc solution of x2 = −1 is called something, weshall call it i; i has the property, by deﬁnition, that its square is −1. That isabout all we are going to say about it; of course, there is more than one rootof the equation x2 = −1. Someone could write i, but another could say,「No,I prefer −i. My i is minus your i.」It is just as good a solution, and since theonly deﬁnition that i has is that i2 = −1, it must be true that any equation wecan write is equally true if the sign of i is changed everywhere. This is calledtaking the complex conjugate. Now we are going to make up numbers by addingsuccessive i’s, and multiplying i’s by numbers, and adding other numbers, andso on, according to all of our rules. In this way we ﬁnd that numbers can all bewritten in the form p + iq, where p and q are what we call real numbers, i.e., thenumbers we have been deﬁning up until now. The number i is called the unitimaginary number. Any real multiple of i is called pure imaginary. The mostgeneral number, a, is of the form p + iq and is called a complex number. Thingsdo not get any worse if, for instance, we multiply two such numbers, let us say

22-11

(r + is)(p + iq). Then, using the rules, we get

(r + is)(p + iq) = rp + r(iq) + (is)p + (is)(iq)= rp + i(rq) + i(sp) + (ii)(sq)= (rp − sq) + i(rq + sp),

(22.4)since ii = i2 = −1. Therefore all the numbers that now belong in the rules (22.1)have this mathematical form.Now you say,「This can go on forever! We have deﬁned powers of imaginariesand all the rest, and when we are all ﬁnished, somebody else will come along withanother equation which cannot be solved, like x6 + 3x2 = −2. Then we have togeneralize all over again!」But it turns out that with this one more invention, justthe square root of −1, every algebraic equation can be solved! This is a fantasticfact, which we must leave to the Mathematics Department to prove. The proofsare very beautiful and very interesting, but certainly not self-evident. In fact,the most obvious supposition is that we are going to have to invent again andagain and again. But the greatest miracle of all is that we do not. This is thelast invention. After this invention of complex numbers, we ﬁnd that the rulesstill work with complex numbers, and we are ﬁnished inventing new things. Wecan ﬁnd the complex power of any complex number, we can solve any equationthat is written algebraically, in terms of a ﬁnite number of those symbols. Wedo not ﬁnd any new numbers. The square root of i, for instance, has a deﬁniteresult, it is not something new; and ii is something. We will discuss that now.We have already discussed multiplication, and addition is also easy; if we addtwo complex numbers, (p + iq) + (r + is), the answer is (p + r) + i(q + s). Nowwe can add and multiply complex numbers. But the real problem, of course, isto compute complex powers of complex numbers. It turns out that the problemis actually no more diﬃcult than computing complex powers of real numbers. Solet us concentrate now on the problem of calculating 10 to a complex power, notjust an irrational power, but 10(r+is). Of course, we must at all times use ourrules (22.1) and (22.2). Thus

(22.5)But 10r we already know how to compute, and we can always multiply anythingby anything else; therefore the problem is to compute only 10is. Let us call itsome complex number, x + iy. Problem: given s, ﬁnd x, ﬁnd y. Now if

10(r+is) = 10r10is.

10is = x + iy,

22-12

then the complex conjugate of this equation must also be true, so that

10−is = x − iy.

(Thus we see that we can deduce a number of things without actually computinganything, by using our rules.) We deduce another interesting thing by multiplyingthese together:

10is10−is = 100 = 1 = (x + iy)(x − iy) = x2 + y2.

(22.6)

Thus if we ﬁnd x, we have y also.Now the problem is how to compute 10 to an imaginary power. What guideis there? We may work over our rules until we can go no further, but here is areasonable guide: if we can compute it for any particular s, we can get it for allthe rest. If we know 10is for any one s and then we want it for twice that s, wecan square the number, and so on. But how can we ﬁnd 10is for even one specialvalue of s? To do so we shall make one additional assumption, which is not quitein the category of all the other rules, but which leads to reasonable results andpermits us to make progress: when the power is small, we shall suppose that the「law」10 = 1 + 2.3025 is right, as  gets very small, not only for real , but forcomplex  as well. Therefore, we begin with the supposition that this law is truein general, and that tells us that 10is = 1 + 2.3025 · is, for s → 0. So we assumethat if s is very small, say one part in 1024, we have a rather good approximationto 10is.Now we make a table by which we can compute all the imaginary powersof 10, that is, compute x and y. It is done as follows. The ﬁrst power we startwith is the 1/1024 power, which we presume is very nearly 1 + 2.3025i/1024.Thus we start with(22.7)and if we keep multiplying the number by itself, we can get to a higher imaginarypower. In fact, we may just reverse the procedure we used in making our logarithmtable, and calculate the square, 4th power, 8th power, etc., of (22.7), and thusbuild up the values shown in Table 22-3. We notice an interesting thing, thatthe x numbers are positive at ﬁrst, but then swing negative. We shall look intothat a little bit more in a moment. But ﬁrst we may be curious to ﬁnd for whatnumber s the real part of 10is is zero. The y-value would be 1, and so we wouldhave 10is = 1i, or is = log10 i. As an example of how to use this table, just aswe calculated log10 2 before, let us now use Table 22-3 to ﬁnd log10 i.

10i/1024 = 1.00000 + 0.0022486i,

22-13

Table 22-3

Successive Squares of 10i/1024 = 1 + 0.0022486i

Power is

1024s

10is

i/1024i/512i/256i/128i/64i/32i/16i/8i/4i/2i/1

1.00000 + 0.00225i*11.00000 + 0.00450i20.99996 + 0.00900i40.99984 + 0.01800i80.99936 + 0.03599i160.99742 + 0.07193i320.98967 + 0.14349i640.95885 + 0.28402i1280.83872 + 0.54467i2560.40679 + 0.91365i5121024 −0.66928 + 0.74332i* Should be 0.0022486i

Which of the numbers in Table 22-3 do we have to multiply together toget a pure imaginary result? After a little trial and error, we discover that toreduce x the most, it is best to multiply「512」by「128.」This gives 0.13056 +0.99159i. Then we discover that we should multiply this by a number whoseimaginary part is about equal to the size of the real part we are trying to remove.Thus we choose「64」whose y-value is 0.14349, since that is closest to 0.13056.This then gives −0.01308 + 1.00008i. Now we have overshot, and must divideby 0.99996 + 0.00900i. How do we do that? By changing the sign of i andmultiplying by 0.99996 − 0.00900i (which works if x2 + y2 = 1). Continuing inthis way, we ﬁnd that the entire power to which 10 must be raised to give i isi(512 + 128 + 64 − 4 − 2 + 0.20)/1024, or 698.20i/1024. If we raise 10 to thatpower, we can get i. Therefore log10 i = 0.68184i.

22-6 Imaginary exponentsTo further investigate the subject of taking complex imaginary powers, letus look at the powers of 10 taking successive powers, not doubling the powereach time, in order to follow Table 22-3 further and to see what happens to thoseminus signs. This is shown in Table 22-4, in which we take 10i/8, and just keep

22-14

Table 22-4

Successive Powers of 10i/8

p = power · 8/i

10ip/8

0123456789101112141618202224

1.00000 + 0.00000i0.95882 + 0.28402i0.83867 + 0.54465i0.64944 + 0.76042i0.40672 + 0.91356i0.13050 + 0.99146i−0.15647 + 0.98770i−0.43055 + 0.90260i−0.66917 + 0.74315i−0.85268 + 0.52249i−0.96596 + 0.25880i−0.99969 − 0.02620i−0.95104 − 0.30905i−0.62928 − 0.77717i−0.10447 − 0.99453i+0.45454 − 0.89098i+0.86648 − 0.49967i+0.99884 + 0.05287i+0.80890 + 0.58836i

multiplying it. We see that x decreases, passes through zero, swings almost to −1(if we could get in between p = 10 and p = 11 it would obviously swing to −1),and swings back. The y-value is going back and forth too.

In Fig. 22-1 the dots represent the numbers that appear in Table 22-4, andthe lines are just drawn to help you visually. So we see that the numbers x and yoscillate; 10is repeats itself, it is a periodic thing, and as such, it is easy enoughto explain, because if a certain power is i, then the fourth power of that wouldbe i2 squared. It would be +1 again, and therefore, since 100.68i is equal to i, bytaking the fourth power we discover that 102.72i is equal to +1. Therefore, if wewanted 103.00i, for instance, we could write it as 102.72i times 100.28i. In otherwords, it has a period, it repeats. Of course, we recognize what the curves looklike! They look like the sine and cosine, and we shall call them, for a while, thealgebraic sine and algebraic cosine. However, instead of using the base 10, we

22-15

Figure 22-1

eit = cos t + i sin t.

shall put them into our natural base, which only changes the horizontal scale;so we denote 2.3025s by t, and write 10is = eit, where t is a real number. Noweit = x + iy, and we shall write this as the algebraic cosine of t plus i times thealgebraic sine of t. Thus(22.8)What are the properties of cos t and sin t? First, we know, for instance, thatx2 + y2 must be 1; we have proved that before, and it is just as true for base eas for base 10. Therefore cos2 t + sin2 t = 1. We also know that, for smallt, eit = 1 + it, and therefore cos t is nearly 1, and sin t is nearly t, and so itgoes, that all of the various properties of these remarkable functions, whichcome from taking imaginary powers, are the same as the sine and cosine oftrigonometry.Is the period the same? Let us ﬁnd out. e to what power is equal to i? Whatis the logarithm of i to the base e? We worked it out before, in the base 10it was 0.68184i, but when we change our logarithmic scale to e, we have tomultiply by 2.3025, and if we do that it comes out 1.570. So this will be called「algebraic π/2.」But, we see, it diﬀers from the regular π/2 by only one placein the last point, and that, of course, is the result of errors in our arithmetic!So we have created two new functions in a purely algebraic manner, the cosineand the sine, which belong to algebra, and only to algebra. We wake up at theend to discover the very functions that are natural to geometry. So there is aconnection, ultimately, between algebra and geometry.

We summarize with this, the most remarkable formula in mathematics:

This is our jewel.

eiθ = cos θ + i sin θ.

(22.9)

22-16

We may relate the geometry to the algebra by representing complex numbersin a plane; the horizontal position of a point is x, the vertical position of a pointis y (Fig. 22-2). We represent every complex number, x + iy. Then if the radialdistance to this point is called r and the angle is called θ, the algebraic law is thatx + iy is written in the form reiθ, where the geometrical relationships betweenx, y, r, and θ are as shown. This, then, is the uniﬁcation of algebra and geometry.

Fig. 22-2. x + iy = r e iθ.

When we began this chapter, armed only with the basic notions of integersand counting, we had little idea of the power of the processes of abstractionand generalization. Using the set of algebraic「laws,」or properties of numbers,Eq. (22.1), and the deﬁnitions of inverse operations (22.2), we have been ablehere, ourselves, to manufacture not only numbers but useful things like tables oflogarithms, powers, and trigonometric functions (for these are what the imaginarypowers of real numbers are), all merely by extracting ten successive square rootsof ten!

22-17

23

