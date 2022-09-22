# Algebra

[TOC]



## Class 1 - 2022/9/7

We have roots formulas for polynomials up to the 4th degree

What about $n=5$?

<u>Abel</u>: for $n= 5$, the polynomials has no roots formula

<u>Galois</u>: found the sufficient and necessary conditions for determining whether a given 5-degree polynomial's roots are "solvable"



### Class will cover:

#### Group Theory

Started with the idea of "permutation"

One of the most fundamental tools

#### Ring Theory

#### Field Theory



Today we start with something easier.



### Set Theory

#### Functions (Maps)

$X,Y$ are sets. A Function from $X$ to $Y$, denoted by $f$ is a subset of $X\times Y$, satisfying :

​		$\forall x \in X, \exists ! y \in Y,(x,y) \in f$. 

$ \forall:$ Arbitrary
$\exists:$ existence
$\exists !: $ existence & uniqueness

If $(x,y)\in f,$  we write $y = f(x)$

We call    $X:$ domain of $f$

​		     	$Y:$ codomain of $f$

Define the image/range of $f$ :

(image are values in Y that are assigned to an X)

​				$Im(f) = \{y\in Y|\exists x \in X, y= f(x)\}$

If y=f(x), we also say y is the image of x
$$ {0}
\text{e.g.}\\
f: \R \rightarrow \R \\

f(x) = x^2\\

Im(f) = {y in R| y>=0}\\
$$

#### Injective

Wish: for each y in Y, it's the image of a unique x in X

Def: A function is <u>injective</u> if : f(x_1) = f(x_2)          =>              x_1 = x_2

equivalently; (add contrapositive here)

(We also call it one-to-one)

e.g.

f(x) = 2x-1

for any x1,x2 in \R , if 

f(x1) = f(x2)

2x1-1 = 2x2-1

2x1=2x2

x1=x2

e.g.

f(x) = x^2 is not injective

since f(1) = f(-1)



#### Surjective

Def: A function is subjective if $Im(f) = Y$

i.e, $\forall y \in Y, \exists x \in X, y = f(x)$

e.g. 

f(x) = 2x                

$f:\R \rightarrow \R$

 f is subjective because for any y in R, $y = 2\cdot y/2 = f(y/2)$

E.g.

g(x) = 2x

g:Z->Z

Im(g) = the set of all even numbers

$\ne \Z$

g is not subjective



#### Bijective 

def: A function is bijective if it's both injective and surjective

e.g. f:R->R f(x)=2x is bijective



#### Inverse Function

def: f: X->Y is a function. We say g: Y->X is the inverse of f if f·g = id_Y and g·f = id_X

----

id_X : X->X  x|-> x

---



Def If f:X->Y has inverse, then f is called <u>invertible</u>

eg

f:R->R f(x) = 2x

Let g:R->R f(x) = x/2

fog(y) = f(y/2) = y

gof(x) = g(2x/2) = x

}=>{ fog = id_Y

gof = id_X

So g is  the inverse o f f, f is invertible



<u>Prop.</u> $f:X\rightarrow Y$ is bijective if and only if it's invertible

<u>Lemma</u> If $f:X\rightarrow Y$, $g:Y\rightarrow X$, $gof = id_X$ ,  then g is surjective and f is injective

<u>Proof of Lemma</u>: if f(x1) = f(x2), then gof(x1) = gof(x2)

idx(x1) = idx(x2)

x1 = x2

so f is injective

for any x in X: x = idX(x) = gof(x) = g(f(x))

so g is surjective

<u>Proof of Prop</u>.

if f is invertible, it has inverse function g

Since gof = idx, fog = idY

by lemma, ............. f is bijective. 

If f is bijective, then \forall y in Y, \exists! x in X such that y = f(x)

Let x = g(y), then g is an inverse function of f.







