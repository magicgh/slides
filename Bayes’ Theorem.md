---
marp: true
footer: 'Section 7.3'
class: 
- invert
paginate: true

---


<font face="Roboto">

# <!-- fit --> Bayes’ Theorem


</font>

---

# Section Summary
* Bayes’ Theorem
* Generalized Bayes’ Theorem
* Bayesian Spam Filters

---

# Motivation for Bayes’ Theorem
* Bayes’ theorem allows us to use probability to answer questions such as the following:
  * Given that someone tests positive for having a particular disease, what is the probability that they actually do have the disease?
  * Given that someone tests negative for the disease, what is the probability, that in fact they do have the disease?

* Bayes’ theorem has applications to medicine, law, artificial intelligence, engineering, and many diverse other areas.


---

# Definition
Suppose that $E$ and $F$ are events from a sample space $S$ such that $p(E)≠ 0$ and $p(F) ≠ 0$. Then:
$$p(F \mid E)=\frac{p(E \mid F) p(F)}{p(E \mid F) p(F)+p(E \mid \bar{F}) p(\bar{F})}$$

---

# Example
We have two boxes. The first box contains two green balls and seven red balls. The second contains four green balls and three red balls. Bob selects one of the boxes at random. Then he selects a ball from that box at random.  If he has a red ball, what is the probability that he selected a ball from the first box.
* Let E be the event that Bob has chosen a red ball and F be the event that Bob has chosen the first box.
* By Bayes’ theorem the probability  that Bob has picked the first box is:
$$p(F \mid E)=\frac{(7 / 9)(1 / 2)}{(7 / 9)(1 / 2)+(3 / 7)(1 / 2)}=\frac{7 / 18}{38 / 63}=\frac{49}{76} \approx 0.645$$


---

# Proof$^1$
* Recall the definition of the conditional probability $p(E|F)$:
$$p(E|F) = \frac{p(E \cap F)}{p(F)}$$
* From this definition, it follows that:
$$p(E|F) = \frac{p(E \cap F)}{p(F)}, p(F|E) = \frac{p(E \cap F)}{p(E)}$$


---

# Proof$^2$
* On the last slide we showed that:
$$p(F \mid E)=\frac{p(E \mid F) p(F)}{p(E)}$$
* Note that 
$$p(E)=p(E \mid F) p(F)+p(E \mid \bar{F}) p(\bar{F})$$

---

# Proof$^3$
Since 
$$p(E) = p(E \cap F) + p(E \cap \bar{F})$$

because 
$$E = E \cap S = E \cap (F \cup \bar{F}) = (E \cap F) \cup (E \cap \bar{F})$$
and 
$$(E \cap F) \cap (E \cap \bar{F}) = \emptyset$$
By the definition of conditional probability 
$$p(E)=p(E \cap F)+p(E \cap \bar{F})=p(E \mid F) p(F)+p(E \mid \bar{F}) p(\bar{F})$$
Hence, 
$$p(F \mid E)=\frac{p(E \mid F) p(F)}{p(E \mid F) p(F)+p(E \mid \bar{F}) p(\bar{F})}$$

---

# Application$^1$
## Example
Suppose that one person in 100,000 has a particular  disease. There is a test for the disease that gives a positive result 99% of the time when given to someone with the disease. When given to someone without the disease,  the test gives a negative result 99.5% of the time. Find:
1. the probability that a person who test positive has the disease.
2. the probability that a person who test negative does not have the disease.

Should someone who tests positive be worried?


---

# Application$^2$

## Solution$^1$
Let $D$ be the event that the person has the disease, and $E$ be the event that this person tests positive. We need to compute $p(D|E)$ from $p(D)$, $p(E|D)$, $p(E|\bar{D})$,  $p(\bar{D})$.

$$p(D) = 1/100000 = 0.00001 \quad p(\bar{D}) = 1 - 0.00001 = 0.99999$$
$$p(E|D) = 0.99 \quad p(\bar{E}|D) = 0.01 \quad p(E|\bar{D}) = 0.005 \quad p(\bar{E}|\bar{D}) = 0.995$$

---

## Solution$^2$

$$\begin{aligned}
p(D \mid E)&=\frac{p(E \mid D) p(D)}{p(E \mid D) p(D)+p(E \mid \bar{D}) p(\bar{D})} \\
&=\frac{(0.99)(0.00001)}{(0.99)(0.00001)+(0.005)(0.99999)}\\
&\approx 0.002
\end{aligned}$$
So, don’t worry too much,  if your test for this disease comes back positive.

---

# Application$^3$
## New Question
What if the result is negative?
$$\begin{aligned} p(\bar{D} \mid \bar{E})&=\frac{p(\bar{E} \mid \bar{D}) p(\bar{D})}{p(\bar{E} \mid \bar{D}) p(\bar{D})+p(\bar{E} \mid D) p(D)} \\ &=\frac{(0.995)(0.99999)}{(0.995)(0.99999)+(0.01)(0.00001)} \\ &\approx 0.9999999 \end{aligned}$$
So, it is extremely unlikely you have the disease if you test negative.

---

# Generalized Bayes’ Theorem
**Generalized Bayes’ Theorem:** Suppose that $E$ is an event from a sample space $S$ and that $F_1, F_2, …, F_n$ are mutually exclusive events such that $\bigcup_{i}^{n} F_{i}=S$.
Assume that $p(E) ≠ 0$ for $i = 1, 2, …, n$. Then
$$p\left(F_{j} \mid E\right)=\frac{p\left(E \mid F_{j}\right) p\left(F_{j}\right)}{\sum_{i=1}^{n} p\left(E \mid F_{i}\right) p\left(F_{i}\right)}$$

---

# Bayesian Spam Filters$^1$
How do we develop a tool for determining whether an email is likely to be spam?
    
If we have an initial set *B(ad)* of  spam messages and set *G(ood)* of non-spam messages.  We can use this information along with Bayes’ law to predict the probability that a new email message is spam.
    
We look at a particular word $w$, and count the number of times that it occurs in *B* and in *G*; $n_B(w)$ and $n_G(w)$. 
 * Empirical probability that an email containing $w$  is spam: $p(w) = n_B(w)/|B|$   
 * Empirical probability that an email containing $w$ is not spam: $q(w) = n_G(w)/|G|$

---

# Bayesian Spam Filters$^2$
Let $S$ be the event that the message is spam, and $E$ be the event that the message contains the word $w$. 
Using Bayes’ Rule,
$$p(S|E) = \frac{p(E|S)p(S)}{p(E|S)p(S)+p(E|\bar{S})p(\bar{S})}$$
Assuming that it is equally likely that an arbitrary message is spam and is not spam.
$$p(S|E) = \frac{p(E|S)}{p(E|S)+p(E|\bar{S})}$$
Note that if we have data on the frequency of spam messages, we can obtain a better estimate for $p(S)$. 

---
# Bayesian Spam Filters$^3$
Using our empirical estimates of $p(E | S)$ and $p(E |\bar{S})$.
$$r(w) = \frac{p(w)}{p(w)+q(w)}$$
$r(w)$ estimates the probability that the message is spam. We can class the message as spam if $r(w)$ is above a threshold we decide on apriori, such as $0.9$.

---
# Bayesian Spam Filters$^4$
## Example
We find that the word “Rolex” occurs in 250 out of 2000 spam messages and occurs in 5 out of 1000 non-spam messages. Estimate the probability that an incoming message containing the word “Rolex” is spam, if  the threshold for rejecting the email is 0.9.

## Solution
$p(Rolex) = 250/2000 =0.0125$ and                $q(Rolex) = 5/1000 = 0.005.$
$$r(Rolex) = \frac{p(Rolex)}{p(Rolex)+q(Rolex)} = \frac{0.125}{0.125+0.005}  \approx 0.962$$
We class the message as spam and reject the email!

---

# Bayesian Spam Filters using Multiple Words$^1$

Accuracy can be improved by considering more than one word as evidence.
    
Consider the case where $E_1$ and $E_2$ denote the events that the message contains the words $w_1$ and $w_2$ respectively.
   
We make the simplifying assumption that the events are independent. And again we assume that $p(S) = 1/2$.
$$p(S|E_1 \cap E_2) = \frac{p(E_1|S)p(E_2|S)}{p(E_1|S)p(E_2|S)+p(E_1|\bar{S})p(E_2|\bar{S})}$$
$$r(w_1,w_2) = \frac{p(w_1)p(w_2)}{p(w_1)p(w_2)+q(w_1)q(w_2)}$$
---
# Bayesian Spam Filters using Multiple Words$^2$
## Example 
We have 2000 spam messages and 1000 non-spam messages. The word “stock” occurs in 400  spam messages and  in 60 non-spam messages. The word “undervalued” occurs in 200 spam and 25 non-spam messages.  Should we reject as spam  message that contains both  “stock” and “undervalued”, if the threshold is set to 0.9?
## Solution$^1$
$p(stock)  = 400/2000 = 0.2 \quad q(stock) = 60/1000=0.06\\ p(undervalued) = 200/2000 = 0.1 \quad q(undervalued) = 25/1000 = 0.025$

---

## Solution$^2$
$$\begin{aligned}
r(stock,undervalued) &= \frac{p(stock)p(undervalued)}{p(stock)p(undervalued)+q(stock)q(undervalued)}\\&=\frac{0.2 \times 0.1}{0.2 \times 0.1 +0.06 \times 0.025}\\ &\approx 0.930\end{aligned}$$
If our threshold is $0.9$, we class the message as spam and reject it. 

---
# Bayesian Spam Filters using Multiple Words$^3$
In general, the more words we consider, the more accurate the spam filter. With the independence assumption if we consider $k$ words:
$$p(S|\bigcap_{i=1}^kE_i) = \frac{\prod\limits_{i=1}^kp(E_i\mid S)}{\prod \limits_{i=1}^kp(E_i|S)+\prod\limits_{i=1}^kp(E_i|\bar{S})}$$
$$r(w_1, w_2, ..., w_n) = \frac{\prod_i^kp(w_i)}{\prod_{i=1}^kp(w_i)+\prod_{i=1}^kq(w_i)}$$
We can further improve the filter by considering pairs of words as a single block or certain types of strings. 






