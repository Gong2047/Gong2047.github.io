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







## Class 2022-09-12

Equivalent relation



Ex. 

$S=\Z$, the set of intergers.

* If define relation by $a\sim b$
* The "trivial" equivalence relation
* Define on $\Z$, $a\sim b$ if a-b is even. (We use 2Z for the set of even numbers)
    * We'll check if it's equivalence relation
    1. $\forall a \in \Z, a-a = 0$. 0 is even, so $a\sim a$. 
    2. a~b => a-b is even => b-a is even => b~a
    3. a~b, b~c. => a-b, b-c are even. => a-c = (a-b)+(b-c) is even => a~c

Remark: for any $n\ge 2$, we can define the equivalence relation on $\Z$ by $a\sim b$ iff n divides $a-b$. This leads to the study of integers (mod n). i.e. congruence in number theory.

* Let X= set o f all integreble functions on [0,1]. 
* Define a relation on X by:
    * $f\sim g$     if      $\displaystyle\int^1_0 |f-g|dx = 0$.
* This is an equivalence relation.
    * $\forall f \in X$,     $\displaystyle\int^1_0 |f-f|dx = 0$. So f~f.
    * f~g => $\displaystyle\int^1_0 |g-f|dx = \int^1_0 |f-g|dx = 0$ => g~f
    * $f~g,g~h$ => $\int^1_0 |f-g|dx = 0 and \int^1_0 |g-h|dx = 0$
              => by triangle inequality, (|f-h|\le |f-g|+|g-h|)
                 $0\le \int^1_0 |f-h|dx \le \int^1_0 |f-g|dx + \int^1_0 |g-h|dx = 0+0 = 0$
              => $\int^1_0 |f-h|dx =0$
              => f~h


Ex.  

X is the set of all Cities in the world. Define A~B if one could walk from A to B. (Assume enough energy.)

For example, NYC~Chicago, but not NYC~Paris.

We'll see this is an equivalence relation

1. A~A. True
2. A~B => B~A. 
3. A~B, B~C => A~C.

<u>Definition.</u> Given an equivalence relation on a set $S$, for any $a \in S$, define its equivalence class to be 
$$
[a] = \{s \in S|a \sim s\}
$$

e.g.           If in $\Z$,    $a\sim b$ if $a-b$ is even, then: 

* $[0] = \{n \in \Z|0 \sim n\} = \{n \in \Z|\text{0-n is even}\} = 2\Z.$ It's the set of all even numbers
* $[1] = \{n \in \Z|1 \sim n\} = \{n \in \Z|\text{1-n is even}\}.$ It's the set of all odd numbers
* If we continue for 2,3,4,.... you'll see
* [0] = [2] = [4] = ...... = the set of even numbers
* .....

<u>Proposition.</u>  Given an equivalence relation on $S$, $a, b \in S$, then $[a] = [b]$ or $[a]\cap [b] = \O$.

Proof. 

Assume $[a] \ne [b]$.

Suppose $[a]\cap [b] \ne \O$,    $\exists s \in [a]\cap [b]$.

So $s \in [a]$ and $s \in [b]$.

$\forall x \in [a], x\sim a \sim s \sim b$.    i.e. $x\sim b$,   $x \in [b]$. 

So $[a] \sube [b]$.

Similarly, you can show $[b] \sube [a]$. 

So $[a]=[b]$. Contradiction.

We conclude $[a]\cap [b] = \O$





Definition. A partition of a set S in S = \bigcup_i\in I  S_i, where the S_i are non-empty, non-overlapping subsets of S. 

e.g. S = [1,2,3,4,5,6]. S = {1}\cup{2,3}\cup{4,5,6} is a partition.

Note given partitioin S = \bigcup... Si. \forall s \in S,   \exists i in I, s \in S_i.



<u>Theorem.</u>  S is a set

....





Definition. Given an equivalence relation R on S. Defince the quotient space S/R to be the set of distinct equivalence classes.





































​		







