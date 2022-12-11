[TOC]

### Bernoulli Trial

* A trial with exactly two outcomes: 
    * <u>Success</u> ($P(S) = p$) 

    * <u>Failure</u> ($P(F) = 1-P(S) = 1-p$)

* Ex. Given an experiment and an event $A$. 
    * Success: $A$ occurs
    * Failure: $A$ does not occur
* Note: A Bernoulli Trial is only a single trial.



### Binomial distributions

* Making $n$ independent Bernoulli trials with $P(Success) = p$
* $X$ is the R.V. that counts the number of success
* $X\sim Bin(n,\ p)$
    * $P(X=a) = \displaystyle \binom nap^a(1-p)^{n-a}$
    * $E(X) = np$
    * $Var(X) = np(1-p)$
    * $SD(X) = \sqrt{np(1-p)}$

**Note:**

* We have **Fixed** number of trials ($n$)
* Trials are **Independent**
* Each trial has **Same probability of Success** ($p$)



### Geometric distributions

* Making independent Bernoulli trials with $P(Success) = p$
* $X$ counts number of trials until first success
* $X\sim Geo(p)$
    * $X = \{1,2,3,...\}$
    * $P(X=x) = (1-p)^{x-1}p$
    * $E(X) = 1/p$
    * $\displaystyle Var(X) = \frac{1-p}{p^2}$

**Note:**

* **Independent** Bernoulli trials
* Each with **same probability** of success $p$
* <u>NOT a **fixed** number of trials</u> 



### Negative Binomial Distribution

* Making independent Bernoulli trials with $P(Success) = p$
* Let $X$ count the number of trials needed to achieve $k$ successes.

* $X\sim Neg\ Bin(p,\ k)$

    * $X = \{k,k+1,...\}$

    * $\displaystyle P(X = n) = \binom {n-1}{k-1}p^k(1-p)^{n-k}$

**Note:**

* **Independent** Trials
* **Same probability** of success $p$
* <u>NOT a **fixed** number of trials</u> 

<u>Note:</u>

* If $X\sim Geo(p)$, then $X\sim Neg\ Bin(p,1)$



### Hypergeometric Distribution

* Suppose we have $N$ balls, of which $w$ are white
* Choose $k$ balls from all the balls
* Let $X$ count the number of white balls we have
* $X\sim Hyper(N,w,k)$
    * $P(X=x) = \frac{\displaystyle \binom wx\binom{N-w}{k-x}}{\displaystyle \binom Nk}$

Note:

* Two outcomes = Success / Failure
* **Fixed** number of trials
* <u>Trials are NOT **independent**</u>



