---
marp: true
footer: 'Section 7.4'
class: 
- invert
paginate: true

---
<font face="Roboto">

# <!-- fit --> Expected Value and Variance

</font>

---

# Section Summary 
* Expected Value
* Linearity of Expectations
* Average-Case Computational Complexity
* Geometric Distribution
* Independent Random Variables
* Variance
* Chebyshev’s Inequality

---
# Expected Value$^1$
## Definition
The expected value (or expectation or mean) of the random variable *X* on the sample space *S* is equal to
$$E(X) = \sum\limits_{s \in S} p(s)X(s)$$
## Example-Expected Value of a Die
Let *X* be the number that comes up when a fair die is rolled. What is the expected value of *X*?

---
## Solution
The random variable *X* takes the values 1, 2, 3, 4, 5, or 6. Each has probability 1/6. It follows that
$$E(X) = \frac{1}{6} \cdot 1 + \frac{1}{6} \cdot 2 + ...+ \frac{1}{6} \cdot 6 = \frac{7}{2}$$

---
# Expected Value$^2$
## Theorem 1
If *X* is a random variable and *p(X = r)* is the probability that X = r, so that
$$p(X=r) = \sum_{s \in S, X(s) = r} p(s)$$
then
$$E(X) = \sum\limits_{r \in X(S)} p(X=r)r$$
---

## Proof
Suppose that *X* is a random variable with range *X(S)* and let *p(X = r)* be the probability that *X* takes the value *r*.    
  
Consequently, *p(X = r)* is the sum of the probabilities of the outcomes s such that *X(s) = r*. Hence,
$$E(X) = \sum\limits_{r \in X(S)}p(X=r)r$$

---
# Expected Value$^3$

## Theorem 2
The expected number of successes when *n* mutually independent Bernoulli trials are performed, where *p* is the probability of success on each trial, is *np*.
## Proof
Let *X* be the random variable equal to the number of success in n trials. By Theorem 2 of section 7.2, $p(X = k) = C(n,k)p^kq^{n−k}$. Hence,
$$E(X) = \sum_{k=1}^nkp(X=k)$$ 

---
# Expected Value$^4$


<div style="font-size:21px">

$$
\begin{aligned}
E(X) &=\sum_{k=1}^{n} k p(X=k) \\
&=\sum_{k=1}^{n} k C(n, k) p^{k} q^{n-k} \\
&=\sum_{k=1}^{n} n C(n-1, k-1) p^{k} q^{n-k} \\
&=n p \sum_{k=1}^{n} C(n-1, k-1) p^{k-1} q^{n-k} \\
&=n p \sum_{j=0}^{n-1} C(n-1, j) p^{j} q^{n-1-j} \\
&=n p(p+q)^{n-1} \\
&=n p
\end{aligned}
$$

</div>


<div style="font-size:27px">
We see that the expected number of successes in n mutually independent Bernoulli trials is <em>np</em>.


</div>


---

# Linearity of Expectations$^1$

The following theorem tells us that expected values are linear. For example, the expected value of the sum of random variables is the sum of their expected values.

## Theorem 3
If $X_i, i = 1, 2, …,n$ with *n* a positive integer, are random variables on *S*, and if *a* and *b* are real numbers, then 
1. $E(X_1+X_2+...+X_n) = E(X_1)+E(X_2)+...+E(X_n)$
2. $E(aX+b) = aE(X)+b$

---

# Linearity of Expectations$^2$

## Expected Value in the Hatcheck Problem
A new employee started a job checking hats, but forgot to put the claim check numbers on the hats. So, the *n* customers just receive a random hat from those remaining. What is the expected number of hat returned correctly?
  
## Solution$^1$
Let *X* be the random variable that equals the number of people who receive the correct hat. Note that $X = X_1 + X_2 + ... + X_n$,  where $X_i = 1$ if the ith person receives the hat and $X_i = 0$ otherwise. 

---
## Solution$^2$

Because it is equally likely that the checker returns any of the hats to the ith person, it follows that the probability that the *i*th person receives the correct hat is *1/n*. Consequently (by Theorem 1), for all $i$
$$E(X_i) = 1 \cdot p(X_i=1)+0 \cdot p(X_i=0) = \frac{1}{n}$$
By the linearity of expectations (Theorem 3), it follows that
$$E(X) = E(X_1)+E(X_2) + ... + E(X_n) = \frac{n \cdot 1}{n}=1$$

Consequently, the average number of people who receive the correct hat is exactly 1.

---

# Linearity of Expectations$^3$
## Expected Number of Inversions in a Permutation

The ordered pair *(i,j)* is an inversion in a permutation of the first *n* positive integers if *i < j*, but *j* precedes *i* in the permutation. 
### Example
There are six inversions in the permutation of *3, 5, 1, 4, 2*

$$ (1, 3), (1, 5), (2, 3), (2, 4), (2, 5), (4, 5)$$

Find the average number of inversions in a random permutation of the first $n$ integers.

---
### Solution$^{1}$
Let $I_{i,j}$ be the random variable on the set of all permutations of the first $n$ positive integers with $I_{i,j} = 1$ if $(i,j)$ is an inversion of the permutation and $I_{i,j} = 0$ otherwise. If $X$ is the random variable equal to the number of inversions in the permutation, then $X = \sum\limits_{1\leq i < j \leq n}I_{i,j}$.
  
Since it is equally likely for $i$ to precede $j$ in a randomly chosen permutation as it is for $j$ to precede $i$, we have:  $E(I_{i,j}) = 1 \cdot p(I_{i ,j} = 1) + 0 \cdot p(I_{i,j} = 0) = 1 \cdot 1/2 + 0 = 1/2$, for all $(i,j)$ .

---

### Solution$^{2}$
Because there are $C_n^2$ pairs $i$ and $j$ with $1 ≤ i < j ≤ n$, by the linearity of expectations(Theorem 3), we have:
$$
E(X)=\sum_{1 \leq i<j \leq n} E\left(I_{i, j}\right)=C_n^2 \cdot \frac{1}{2}=\frac{n-1}{2} \cdot \frac{1}{2}
$$
Consequently, it follows that there is an average of  n(n−1)/4 inversions in a random permutation of the first n positive integers.

---

# Average-Case Computational Complexity

The average-case computational complexity of an algorithm can be found by computing the expected value of a random variable.

Let the sample space of an experiment be the set of possible inputs $a_j, j = 1, 2, …,n$, and let the random variable $X$ be the assignment to $a_j$ of the number of operations used by the algorithm when given $a_j$ as input.
  
Assign a probability $p(a_j)$ to each possible input value $a_j$.
    
The expected value of $X$ is the average-case computational complexity of the algorithm.
$$E(X) = \sum \limits_{j=1}^np(a_j)X(a_j)$$

---

# Average-Case Complexity of Linear Search$^1$
What is the average-case complexity of linear search (described in Chapter 3) if the probability that $x$ is in the list is $p$ and it is equally likely that $x$ is any of the $n$ elements of the list?

```{r, eval = FALSE}
procedure linear search(x: integer,  a1, a2, …,an: distinct integers)
i := 1
while (i ≤ n and x ≠ ai)
	i := i + 1
	if i ≤ n then location := i
		else location := 0
return location{location is the subscript of the term that equals x, or is 0 if x is not found}

```

---

# Average-Case Complexity of Linear Search$^2$

## Solution$^1$
There are *n + 1* possible types of input: one type for each of the *n* numbers on the list and one additional type for the numbers not on the list.
Recall that: 
* *2i + 1* comparisons are needed if *x* equals the *i*th element of the list.
* *2n + 2* comparisons are used if *x* is not on the list.

---

## Solution$^2$
The probability that *x* equals $a_i$ is *p/n* and the probability that *x* is not in the list is *q = 1− p*. The average-case case computational complexity of the linear search algorithm is:

$$\begin{aligned}E&=3p/n+5p/n+...+(2n+1)p/n+(2n+2)q\\&=(p/n)(3+5+...+(2n+1))+(2n+2)q \\&= (p/n)((n+1)^2-1)+(2n+2)q \\&= p(n+2)+(2n+2)q\end{aligned}$$


---

## Solution$^3$

When $x$ is guaranteed to be in the list, $p = 1, q = 0$, so that $E = n + 2$.
When $p$ is $½$ and $q$ = $½$, then $E = (n + 2)/2 + n + 1 = (3n + 4) /2$.
When $p$ is $¾$ and $q$ = $¼$ then $E = (n + 2)/4 + (n + 1)/2 = (5n + 8) /4$.
When $x$ is guaranteed not to be in the list, $p = 0$ and $q = 1$, then $E = 2n + 2$.

---

# Average-Case Complexity of Insertion Sort$^1$
What is the average number of comparisons used by insertion sort from *Chapter 3* to sort n distinct elements?

At step $i$ for $i = 2, …,n$ insertion sort inserts the $i$th element in the original list into the correct position in the sorted list of the first $i -1$ elements.

```
procedure insertion sort(a1,…,an: reals with n ≥ 2)
	for j := 2 to n
	i := 1
	while aj > ai
		i := i + 1
	m := aj
	for k := 0 to j − i − 1
        aj-k := aj-k-1
	ai := m
{Now a1,…,an is in increasing order}
```

---
# Average-Case Complexity of Insertion Sort$^2$
## Solution$^1$
Let $X$ be the random variable equal to the number of comparisons used by insertion sort to sort a list of $a_1, a_2, …., a_n$ distinct elements. $E(X)$ is the average number of comparisons.

* Let $X_i$ be the random variable equal to the number of comparisons used to insert $a_i$ into the proper position after the first $i −1$ elements $a_1, a_2, …., a_{i-1}$ have been sorted. 
* Since $X = X_2 + X_3 + ... + X_n$
$E(X) = E(X_2 + X_3 + ... + X_n) = E(X_2) + E(X_3) + ... + E(X_n)$.

---

## Solution$^2$
To find $E(X_i)$ for $i = 2,3,…,n$, let $p_j(k)$ be the probability that the largest of the first $j$ elements in the list occurs at the $k$th position, that is, $\max(a_1, a_2, …, a_j ) = a_k$, where $1 ≤ k ≤ j$.
Assume uniform distribution; $p_j(k) = 1/j$ .
Then $X_i(k) = k$.
Since $a_i$ could be inserted into any of the first $i$ positions
$$
E\left(X_{i}\right)=\sum_{k=1}^{i} p_{i}(k) \cdot X_{i}(k)=\sum_{k=1}^{i} \frac{1}{i} \cdot k=\frac{1}{i} \sum_{k=1}^{i} k=\frac{1}{i} \cdot \frac{i(i+1)}{2}=\frac{i+1}{2}
$$

---

## Solution$^3$
It follows that
$$
E(X)=\sum\limits_{i=2}^{n} E\left(X_{i}\right)=\sum\limits_{i=2}^{n} \frac{i+1}{2}=\frac{1}{2} \sum\limits_{j=3}^{n+1} j
=\frac{1}{2} \frac{(n+1)(n+2)}{2}-\frac{1}{2}(1+2)=\frac{n^{2}+3 n-4}{4}
$$
Hence, the average-case complexity is $\Theta(n^2)$.

---
# The Geometric Distribution$^1$
## Definition
A random variable $X$ has geometric distribution with parameter $p$ if $p(X = k) = (1 − p)^{k-1}p$ for $k = 1,2,3,…$, where $p$ is a real number with $0 ≤ p ≤ 1$.
## Theorem 4
If the random variable $X$ has the geometric distribution with parameter $p$, then $E(X) = 1/p$.

---
# The Geometric Distribution$^2$
## Example
Suppose the probability that a coin comes up tails is $p$. What is the expected number of flips until this coin comes up tails?
* The sample space is *{T, HT, HHT, HHHT, HHHHT, …}*.
* Let *X* be the random variable equal to the number of flips in an element of the sample space; *X(T) = 1, X(HT) = 2, X(HHT) = 3*, etc.
* By Theorem 4, *E(X) = 1/p*.
---
# Independent Random Variables
## Definition
The random variables *X* and *Y* on a sample space S are independent if

$$p(X = r_1 \wedge Y = r_2) = p(X = r_1) \cdot p(Y = r_2)$$

## Theorem 5
If $X$ and $Y$ are independent variables on a sample space $S$, then $E(XY) = E(X)E(Y)$.

---
# Variance$^1$

## Deviation
The deviation of $X$ at $s ∊ S$ is $X(s) − E(X)$, the difference between the value of $X$ and the mean of $X$.

## Definition
Let $X$ be a random variable on the sample space $S$. The variance of $X$, denoted by $V(X)$ is
$$V(X) = \sum\limits_{s \in S} (X(s)-E(X))^2p(s)$$

That is $V(X)$ is the weighted average of the square of the deviation of $X$. The standard deviation of X, denoted by $σ(X)$ is defined to be $\sqrt{V(X)}$.

---

# Variance$^2$
## Theorem 6
If $X$ is a random variable on a sample space $S$, then $V(X) = E(X^2) − E(X)^2$.
## Corollary 1
If $X$ is a random variable on a sample space $S$ and $E(X) = μ$ , then $V(X) = E((X −μ)^2)$.

---

# Variance$^3$
## Example
What is the variance of the random variable $X$, where $X(t) = 1$ if a Bernoulli trial is a success and $X(t) = 0$ if it is a failure, where $p$ is the probability of success and $q$ is the probability of failure?
## Solution
Because $X$ takes only the values $0$ and $1$, it follows that $X^2(t) = X(t)$. Hence,
$$
V(X)=E\left(X^{2}\right)-E(X)^{2}=p-p^{2}=p(1-p)=p q
$$

---

# Variance$^4$

## Variance of the Value of a Die
What is the variance of a random variable $X$, where $X$ is the number that comes up when a fair die is rolled?

## Solution 
We have $V(X) = E(X^2) - E(X)^2$. In an earlier example, we saw that $E(X) = \frac{7}{2}$. Note that 
$$E(X^2) = \frac{1}{6}(1^2+2^2+3^2+4^2+5^2+6^2) = \frac{91}{6}$$
We conclude that $\displaystyle V(X) = \frac{91}{6} - (\frac{7}{2})^2 = \frac{35}{12}$.

---

# Variance$^5$

## Bienaymé‘s Formula

If $X$ and $Y$ are two independent random variables on a sample space $S$, then $V(X + Y) = V(X) + V(Y)$. Furthermore, if $X_i, i = 1,2, …,n$, with $n$ a positive integer, are pairwise independent random variables on $S$, then
$$
\mathrm{V}\left(X_{1}+X_{2}+\cdots+X_{n}\right)=\mathrm{V}\left(X_{1}\right)+\mathrm{V}\left(X_{2}\right)+\cdots+\mathrm{V}\left(X_{n}\right)
$$

---

# Variance$^6$

## Example

<div style = "font-size:26px">

Find the variance of the number of successes when $n$ independent Bernoulli trials are performed, where on each trial, $p$ is the probability of success and $q$ is the probability of failure.

</div>

## Solution

<div style = "font-size:26px">

Let $X_i$ be the random variable with $X_i ((t_1, t_2, …, t_n)) = 1$ if trial $t_i$ is a success and $X_i ((t1, t2, …, tn)) = 0$ if it is a failure. Let $X = X_2 + X_3 + … + X_n$. Then $X$ counts the number of successes in the $n$ trials.

</div>

<div style = "font-size:26px">

* By Bienaymé ‘s Formula, it follows that  $V(X)= V(X_1) + V(X_2) + ...+ V(X_n)$.
* By the previous example ,$V(X_i) = pq$ for $i = 1,2, …,n$.

Hence, $V(X) = npq$.

</div>

---

# Chebyshev’s Inequality$^1$

## Definition
Let $X$ be a random variable on a sample space $S$ with probability function $p$. If $r$ is a positive real number, then
$$
p(|X(s)-E(X)| \geq r) \leq \frac{\mathrm{V}(X)}{r^{2}}
$$

---

# Chebyshev’s Inequality$^2$

## Example

Suppose that $X$ is a random variable that counts the number of tails when a fair coin is tossed $n$ times. Note that $X$ is the number of successes when $n$ independent Bernoulli trials, each with probability of success $½$ are done. Hence, (by Theorem 2)  $E(X) = n/2$ and $V(X) = n/4$.

By Chebyschev’s inequality with $r = \sqrt{n}$,
$$
p(|X(s)-n / 2| \geq \sqrt{n}) \leq(n / 4)(\sqrt{n})^{2}=1 / 4
$$
This means that the probability that the number of tails that come up on $n$ tosses deviates from the mean, $n/2$, by more than $\sqrt{n}$ is no larger than $¼$.
