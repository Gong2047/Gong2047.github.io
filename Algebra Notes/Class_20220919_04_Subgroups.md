# Class 4: Subgroups, Additive Integer Group and Its Subgroup - 2022/09/19

[TOC]

## Order

<u>**Definition:**</u> The <u>order</u> of a group $G$ is the number of element $G$ has, denoted by $|G|$.

* If $|G|<\infty$, we say $G$ is a finite group. 
* Otherwise $G$ is an infinite group

## Notation of composition in groups

If we write the composition of a group is a multiplicative way, we have:
$$
\begin{align*}
k>0, \qquad g^k &= \underbrace{g* g* \dots g}_\text{k-copies},\\
g^{-k} &= \underbrace{g^{-1}*g^{-1}\dots g^{-1}}_\text{k-copies}\\
k=0, \qquad g^0&=1
\end{align*}
$$
Note:    
$$
g^k\cdot g^l= g^{k+l}
$$

## Examples of Groups

1. $G = \{\pm 1\}$, composition is multiplication.

    $|G| = 2$. Finite group.
    $$
    (+1)\cdot (+1) = +1\\
    (+1)\cdot (-1) = -1\\
    (-1)\cdot (+1) = -1\\
    (-1)\cdot (-1) = +1
    $$

    * Since it's a finite group, we can use the multiplication table to show the results.

    > ## Multiplication Table
    >
    > * "<u>Multiplication Table</u>" for a finite group is a way to express the result of all the compositions for this group.
    >
    > * Example: $G$ is a finite group, $G = \{1, g_1, g_2,..., g_{n-1}\}$
    >
    >     ![image-20220927231057739](C:\Users\addas\AppData\Roaming\Typora\typora-user-images\image-20220927231057739.png)
    >
    > * In particular, for $G = \{\pm1\}$ we just defined, 
    >
    >     |      | +1   | -1   |
    >     | ---- | ---- | ---- |
    >     | +1   | +1   | -1   |
    >     | -1   | -1   | +1   |
    >
    > * The trivial group,
    >
    >     |      | 1    |
    >     | :--- | :--- |
    >     | 1    | 1    |

2. **<u>Klein</u> Four Group**

    > Named after the mathematician Klein 

    * $K_4 = \{1,a,b,c\}$

    * Law of composition is given by the table:

        |       | 1    | a    | b    | c    |
        | :---: | ---- | ---- | ---- | ---- |
        | **1** | 1    | a    | b    | c    |
        | **a** | a    | 1    | c    | b    |
        | **b** | b    | c    | 1    | a    |
        | **c** | c    | b    | a    | 1    |

    * Note:

        * $|K_4| = 4$
        * $\forall x \in K_4,\ \: x^{-1} = x$

    * Associativity: It was checked that $(xy)z = x(yz)$,  $\forall x,y,z \in K_4$.

        * $4^3 = 64$ cases

    * $K_4$ is an abelian group.

        > A finite group $G$ is Abelian $\iff$ its multiplication table is symmetric along diagonal

3. **Symmetric Groups $S_n$**

    > First group in math history

    * <u>Recall:</u>  

        * $X = \{1,2,3,...,n\}$.

        * $S_n$ is the groups of all bijections (permutations) on $X$.

        * with function composition

    * Problem: We don't have a good way to describe the elements (functions)

        * We can use cycle

## Cycle

### Definition

* A <u>cycle</u> $(a_1\ a_2\ ...\ a_k)$, where $a_1,a_2,...a_k$ are distinct elements in $\{1,2,...,n\}$, is an element in $S_n$ that sends $a_1\mapsto a_2$, $a_2\mapsto a_3$, ...... , $a_{k-1}\mapsto a_k$,  $a_k\mapsto a_{k+1}$, while fixing the remaining numbers.

### Example

* $\sigma = (1\quad 2\quad 3)\in S_5$ 
* $\sigma: \{1,2,3,4,5\} \rightarrow\{1,2,3,4,5\}$
* $\sigma(1) = 2$,  $\sigma(2) = 3$,  $\sigma(3) = 1$

> <u>**NOTE**</u>: $(1\quad 2\quad 3) = (2\quad 3\quad 1) = (3\quad 1\quad 2)$

* $S_1 = \{id\}$     $S_2 = \{id, (1\: 2)\}$
