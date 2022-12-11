# TOP - 20221018 - Poiss

> This is from a lecture recording from Fall 2020

[TOC]

## Approximating Poisson with Binomial

Let $X\sim Bin(n,\ p)$

* $\text{pmf: } P(X=k)=\displaystyle \binom nk p^k (1-p)^{n-k}$
* $E(X) = np$
* $Var(X) = np(1-p)$

### Claim

<u>**Claim**</u>: If $n$ is "large" enough and p "small" enought such that $np$ is "moderate", then using $\lambda = np$, $X\sim Pois(\lambda)$, that is $X\sim Pois(np)$.

### Rules

Rule of Thumb

* $n\ge 20$  &  $p\le 0.05$

    ​             or

* $n\ge 100$  &  $np\le 10$

### Proof


* Given $X\sim Bin(n,\ p)$

* Let $\lambda = np\quad \Rightarrow\  p = \lambda/n$


* $\text{pmf: }$  
    $$
    \begin{align*}
    P(X=k)&= \binom nk p^k(1-p)^{n-k} \\
    &= \binom nk \Big(\frac\lambda n \Big)^k\Big(1-\frac\lambda n\Big)^{n-k}\\
    &= \frac{n!}{(n-k)!\ k!}\cdot\frac{\lambda^k}{n^k}\cdot\frac{(1-\lambda/n)^n}{(1-\lambda/n)^k}\\
    &= \frac{n!}{(n-k)!\ n^k}\cdot\Big(\frac{\lambda^k}{k!}\Big)\cdot\frac{(1-\lambda/n)^n}{(1-\lambda/n)^k}\\
    &= \frac{n(n-1)...(n-(n-k)+1)}{n\  \cdot\   n \quad  \quad.... \quad \quad n\qquad}\cdot\frac{\lambda^k}{k!}\cdot\frac{(1-\lambda/n)^n}{(1-\lambda/n)^k}
    \end{align*}
    $$
    
    
    * Note that $\displaystyle \frac{n!}{(n-k)!} = n\cdot(n-1)\cdot(n-2)...(n-(n-k)+1)$
    
        * has $k$ items
    * Thus $\displaystyle \frac{n!}{(n-k)!n^k} = \frac{n(n-1)(n-2)...(n-(n-k)+1)}{n \cdot \quad n\  \cdot\ \quad\ n\ \quad\ \quad....\ \qquad n\qquad}$
    
    
    
* Now, 
    $$
    \text{Pmf} = \frac{n(n-1)...(n-(n-k)+1)}{n\  \cdot\   n \quad  \quad.... \quad \quad n\qquad}\cdot\Big(\frac{\lambda^k}{k!}\Big)\cdot\frac{(1-\lambda/n)^n}{(1-\lambda/n)^k}
    $$

* As $n\rightarrow \infty$, 
    * $\displaystyle \frac nn = \frac {n-1}n = ...=\frac{n-(n-k)+1}n = 1$
    * $(1-\lambda /n)^n \  = e^{-\lambda}$
    
        > #### Important Limit Expansions of $e^x$
        >
        > 1. $$
        >     \lim_{n\rightarrow \infty}\bigg(1+\frac xn\bigg)^n = e^x
        >     $$
        >
        > 2. $$
        >     \lim_{n\rightarrow \infty}\bigg(1-\frac xn\bigg)^n = e^{-x}
        >     $$
    
    * $(1-\lambda/n)^k=1$    $(\text{as }\lambda/n \rightarrow 0)$


​    

* Therefore,

$$
\begin{align*}
\text{Pmf}_{n\rightarrow \infty} &= 1\cdot\bigg(\frac{\lambda^k}{k!}\bigg)\cdot\frac{e^{-\lambda}}{1}\\
&= \frac{e^{-\lambda}\cdot\lambda^k}{k!}\\
&= P(X=k)\quad \text{ for }X\sim Pois(\lambda)
\end{align*}
$$

### Recap

Let $X\sim Bin(n,\ p)$

$P(X=k) = \displaystyle\binom nk p^k(1-p)^{n-k}\approx \frac {e^{-\lambda}\lambda^k}{k!} = P(X=k)\quad$for $X\sim Pois(\lambda = np)$

* When $n$ is large