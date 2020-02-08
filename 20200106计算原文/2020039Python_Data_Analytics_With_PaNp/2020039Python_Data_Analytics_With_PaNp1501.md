LaTeX is extensively used in Python. In this appendix there are many examples that can be useful to represent LaTeX expressions inside Python implementations. This same information can be found at the link http://matplotlib.org/users/mathtext.html .

With matplotlib

You can enter the LaTeX expression directly as an argument of various functions that can accept it. For example, the title() function that draws a chart title.

import matplotlib.pyplot as plt

%matplotlib inline

plt.title(r'$\alpha > \beta$')

With IPython Notebook in a Markdown Cell

You can enter the LaTeX expression between two '$$'.

$$c = \sqrt{a^2 + b^2}$$

With IPython Notebook in a Python 2 Cell

You can enter the LaTeX expression within the Math() function.

from IPython.display import display, Math, Latex

display(Math(r'F(k) = \int_{-\infty}^{\infty} f(x) e^{2\pi i k} dx'))

Subscripts and Superscripts

To make subscripts and superscripts, use the ‘_’ and ‘^’ symbols:

r'$\alpha_i > \beta_i$'

This could be very useful when you have to write summations:

r'$\sum_{i=0}^\infty x_i$'

Fractions, Binomials, and Stacked Numbers

Fractions, binomials, and stacked numbers can be created with the \frac{}{}, \binom{}{}, and \stackrel{}{} commands, respectively:

r'$\frac{3}{4} \binom{3}{4} \stackrel{3}{4}$'

Fractions can be arbitrarily nested:

Note that special care needs to be taken to place parentheses and brackets around fractions. You have to insert \left and \right preceding the bracket in order to inform the parser that those brackets encompass the entire object:

Radicals

Radicals can be produced with the \sqrt[]{} command.

r'$\sqrt{2}$'

Fonts

The default font is italics for mathematical symbols. To change fonts, for example with trigonometric functions as sin:

The choices available with all fonts are

from IPython.display import display, Math, Latex

display(Math(r'\mathrm{Roman}'))

display(Math(r'\mathit{Italic}'))

display(Math(r'\mathtt{Typewriter}'))

display(Math(r'\mathcal{CALLIGRAPHY}'))

Accents

An accent command may precede any symbol to add an accent above it. There are long and short forms for some of them.

\acute a or \'a

\bar a

\breve a

\ddot a or \"a

\dot a or \.a

\grave a or \`a

\hat a or \^a

\tilde a or \∼a

\vec a

\overline{abc}

Symbols

You can also use a large number of the TeX symbols.

Lowercase Greek \alpha

\beta

\chi

\delta

\digamma

\epsilon

\eta

\gamma

\iota

\kappa

\lambda

\mu

\nu

\omega

\phi

\pi

\psi

\rho

\sigma

\tau

\theta

\upsilon

\varepsilon

\varkappa

\varphi

\varpi

\varrho

\varsigma

\vartheta

\xi

\zeta

Uppercase Greek \Delta

\Gamma

\Lambda

\Omega

\Phi

\Pi

\Psi

\Sigma

\Theta

\Upsilon

\Xi

\mho

\nabla

Hebrew \aleph

\beth

\daleth

\gimel

Delimiters /

[

\Downarrow

\Uparrow

\Vert

\backslash

\downarrow

\langle

\lceil

\lfloor

\llcorner

\lrcorner

\rangle

\rceil

\rfloor

\ulcorner

\uparrow

\urcorner

\vert

\{

\|

\}

]

|

Big Symbols \bigcap

\bigcup

\bigodot

\bigoplus

\bigotimes

\biguplus

\bigvee

\bigwedge

\coprod

\int

\oint

\prod

\sum

Standard Function Names \Pr

\arccos

\arcsin

\arctan

\arg

\cos

\cosh

\cot

\coth

\csc

\deg

\det

\dim

\exp

\gcd

\hom

\inf

\ker

\lg

\lim

\liminf

\limsup

\ln

\log

\max

\min

\sec

\sin

\sinh

\sup

\tan

\tanh

Binary Operation and Relation Symbols \Bumpeq

\Cap

\Cup

\Doteq

\Join

\Subset

\Supset

\Vdash

\Vvdash

\approx

\approxeq

\ast

\asymp

\backepsilon

\backsim

\backsimeq

\barwedge

\because

\between

\bigcirc

\bigtriangledown

\bigtriangleup

\blacktriangleleft

\blacktriangleright

\bot

\bowtie

\boxdot

\boxminus

\boxplus

\boxtimes

\bullet

\bumpeq

\cap

\cdot

\circ

\circeq

\coloneq

\cong

\cup

\curlyeqprec

\curlyeqsucc

\curlyvee

\curlywedge

\dag

\dashv

\ddag

\diamond

\div

\divideontimes

\doteq

\doteqdot

\dotplus

\doublebarwedge

\eqcirc

\eqcolon

\eqsim

\eqslantgtr

\eqslantless

\equiv

\fallingdotseq

\frown

\geq

\geqq

\geqslant

\gg

\ggg

\gnapprox

\gneqq

\gnsim

\gtrapprox

\gtrdot

\gtreqless

\gtreqqless

\gtrless

\gtrsim

\in

\intercal

\leftthreetimes

\leq

\leqq

\leqslant

\lessapprox

\lessdot

\lesseqgtr

\lesseqqgtr

\lessgtr

\lesssim

\ll

\lll

\lnapprox

\lneqq

\lnsim

\ltimes

\mid

\models

\mp

\nVDash

\nVdash

\napprox

\ncong

\ne

\neq

\neq

\nequiv

\ngeq

\ngtr

\ni

\nleq

\nless

\nmid

\notin

\nparallel

\nprec

\nsim

\nsubset

\nsubseteq

\nsucc

\nsupset

\nsupseteq

\ntriangleleft

\ntrianglelefteq

\ntriangleright

\ntrianglerighteq

\nvDash

\nvdash

\odot

\ominus

\oplus

\oslash

\otimes

\parallel

\perp

\pitchfork

\pm

\prec

\precapprox

\preccurlyeq

\preceq

\precnapprox

\precnsim

\precsim

\propto

\rightthreetimes

\risingdotseq

\rtimes

\sim

\simeq

\slash

\smile

\sqcap

\sqcup

\sqsubset

\sqsubset

\sqsubseteq

\sqsupset

\sqsupset

\sqsupseteq

\star

\subset

\subseteq

\subseteqq

\subsetneq

\subsetneqq

\succ

\succapprox

\succcurlyeq

\succeq

\succnapprox

\succnsim

\succsim

\supset

\supseteq

\supseteqq

\supsetneq

\supsetneqq

\therefore

\times

\top

\triangleleft

\trianglelefteq

\triangleq

\triangleright

\trianglerighteq

\uplus

\vDash

\varpropto

\vartriangleleft

\vartriangleright

\vdash

\vee

\veebar

\wedge

\wr

Arrow Symbols \Downarrow

\Leftarrow

\Leftrightarrow

\Lleftarrow

\Longleftarrow

\Longleftrightarrow

\Longrightarrow

\Lsh

\Nearrow

\Nwarrow

\Rightarrow

\Rrightarrow

\Rsh

\Searrow

\Swarrow

\Uparrow

\Updownarrow

\circlearrowleft

\circlearrowright

\curvearrowleft

\curvearrowright

\dashleftarrow

\dashrightarrow

\downarrow

\downdownarrows

\downharpoonleft

\downharpoonright

\hookleftarrow

\hookrightarrow

\leadsto

\leftarrow

\leftarrowtail

\leftharpoondown

\leftharpoonup

\leftleftarrows

\leftrightarrow

\leftrightarrows

\leftrightharpoons

\leftrightsquigarrow

\leftsquigarrow

\longleftarrow

\longleftrightarrow

\longmapsto

\longrightarrow

\looparrowleft

\looparrowright

\mapsto

\multimap

\nLeftarrow

\nLeftrightarrow

\nRightarrow

\nearrow

\nleftarrow

\nleftrightarrow

\nrightarrow

\nwarrow

\rightarrow

\rightarrowtail

\rightharpoondown

\rightharpoonup

\rightleftarrows

\rightleftarrows

\rightleftharpoons

\rightleftharpoons

\rightrightarrows

\rightrightarrows

\rightsquigarrow

\searrow

\swarrow

\to

\twoheadleftarrow

\twoheadrightarrow

\uparrow

\updownarrow

\updownarrow

\upharpoonleft

\upharpoonright

\upuparrows

Miscellaneous Symbols \$

\AA

\Finv

\Game

\Im

\P

\Re

\S

\angle

\backprime

\bigstar

\blacksquare

\blacktriangle

\blacktriangledown

\cdots

\checkmark

\circledR

\circledS

\clubsuit

\complement

\copyright

\ddots

\diamondsuit

\ell

\emptyset

\eth

\exists

\flat

\forall

\hbar

\heartsuit

\hslash

\iiint

\iint

\iint

\imath

\infty

\jmath

\ldots

\measuredangle

\natural

\neg

\nexists

\oiiint

\partial

\prime

\sharp

\spadesuit

\sphericalangle

\ss

\triangledown

\varnothing

\vartriangle

\vdots

\wp

\yen

Appendix B: Political and Government Data

Political and Government Data

Data.gov

http://data.gov

