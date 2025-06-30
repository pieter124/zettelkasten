2025-06-11 

Tags:  [[mathematics]]

# **Chapter 1 - The Real Numbers 

# 1.1 - The irrationality of $\large \sqrt{2}$

A field is any set where addition and multiplication are well-defined operations that are commutative, associative, and obey the familiar distributivity property:
$\large a(b + c) =  ab + ac$
There must be an additive identity, and every element must have an additive inverse. There also must be a multiplicative identity, and multiplicative inverses must exist for all nonzero elements of the field.

The real numbers $\large\bf{R}$ are an extension to $\large\bf{Q}$ to fill in the gaps as e.g. handling cases like $\large\sqrt{2}$. Wherever there is a *gap*, a new *irrational* number is defined and placed into the ordering. The real numbers are the union of these irrational numbers together with the rational numbers.

# 1.2 - Preliminaries

**Sets**
Given $A \subseteq \textbf{R}$, the *complement* of A, written $A^c$, refers to the set of all elements of $\textbf{R}$ not in A. Thus, for $A \subseteq \textbf{R}$,

$\large A^c = \{ x \in  \textbf{R}: x \notin A \}$.

De Morgan's Law, states that:
$\large (A \cap B)^c = A^c \cup B^c$
and
$\large (A \cup B)^c = A^c \cap B^c$ 

**Functions**
Given two sets A and B, a *function* from A to B is a rule or mapping that takes each element $x \in A$ and associates with it a single element of B. In this case, we write $\large f : A \rightarrow B$. Given an element $x \in A$, the expression $f(x)$ is used to represent the element of B associated with $x$ by $f$. The set A is called the *domain* of $f$. The *range* of $f$ is not necessarily equal to B but refers to the subset of B given by:

$\large \{y \in B: y = f(x)$ for some $\large x \in A \}$.

The absolute value function is given by:

$\large |x| = \begin{cases} x & \text{if } x \ge 0 \\ -x & \text{if } x < 0. \end{cases}$

With respect to multiplication and division, the absolute value function satisfies:
(i) $\large |ab| = |a| |b|$

(ii) $\large |a + b| \le |a| + |b|$

for all $a, b \in \textbf{R}$.
Property (ii) is called the *triangle inequality*. It turns out to be very important and will be frequently employed in the following way. Given three real numbers a, b, and c, we certainly have

$\large |a - b| = |(a - c) + (c - b)|$ .

By the triangle inequality,

$\large |(a - c) + (c - b)| \le |a - c| + |c - b|$.

so we get

(1) $\large |a - b| \le |a - c| + |c - b|$.

Now, the expression $\large |a - b|$ is equal to $\large |b - a|$ and is best understood as the distance between the two points on the number line.

**Logic & Proofs**
When the contradiction is with the theorem's hypothesis, we technically have what is called a *contrapositive* proof[^1].

$\textbf{Theorem 1.2.6 } \text{Two real numbers a and b are equal if and only if } \forall \epsilon \gt 0, \epsilon \in \textbf{R} \text{, it follows that } |a - b| \lt \epsilon$
*Proof.* To say "if and only if" in mathematics is an economical way of stating that the proposition is true in two directions.

In the forward direction, we must prove the statement:
$\large(\Rightarrow) \text{ If } a = b, \text{then for every real number } \epsilon \gt 0 \text{ it follows that } |a - b| \lt \epsilon.$

We must also prove the converse statement:$\large (\Leftarrow) \text{ If for every real number } \epsilon \gt 0 \text{ if follows that } |a - b| \lt \epsilon \text{, then we must have } a = b.$
For the proof of the first statement, if $a = b$, then $|a - b| = 0$, and so certainly $|a - b| \lt \epsilon$ no matter what $\epsilon \gt 0$ is chosen. For the second statement, we give a proof of contradiction. The conclusion of the proposition in this direction states that $a = b$, so we assume that $a \not= b$. Heading off in search of a contradiction brings us to a consideration of the phrase "for every $\epsilon \gt 0$." Some equivalent ways to state the hypothesis would be to say that "for all possible choices of $\epsilon \gt 0$" or "no matter how $\epsilon \gt 0$ is selected, it is always the case that $|a - b| \lt \epsilon$." But assuming $a \not= b$, the choice of 

$\large \epsilon _0 = |a - b| \gt 0$

poses a serious problem. We are assuming that $|a - b| \lt \epsilon$ is true for every $\epsilon \gt 0$, so this must certainly be true of the particular $\epsilon _0$ just defined. However, the statements

$\large |a - b| \lt \epsilon_0$ and $\large |a - b| = \epsilon_0$

cannot both be true. This contradiction means that our initial assumption that $a \not= b$ is unacceptable. Therefore, $a = b$, and the indirect proof is complete. $\square$

**Induction**

The fundamental principle behind induction is that if S is some subset of $\large\textbf{N}$ with the property that

(i) S contains 1 and 
(ii) whenever S contains a natural number *n*, it also contains *n + 1*,

then it must be that S = $\large\textbf{N}$. 

# 1.3 The Axiom of Completeness
Most work done about the nature of $\textbf{R}$ was initially based on intuitive assumptions. However, there are modern definitions which give a more rigorous structure for constructing $\textbf{R}$ from $\textbf{Q}$.

**An Initial Definition for R**
First, $\textbf{R}$ is a set containing $\textbf{Q}$. The operations of addition and multiplication on $\textbf{Q}$ extend to all of $\textbf{R}$ in such a way that every element of $\textbf{R}$ has an additive inverse and every non-zero element of $\textbf{R}$ has a multiplicative inverse. We assume $\textbf{R}$ is an ordered field, which contains $\textbf{Q}$ as a subfield.

**Axiom of Completeness**. *Every non-empty set of real numbers that is bounded above has a least upper bound*.

What does this mean?

**Least Upper Bounds and Greatest Lower Bounds**

Definition 1.3.1. A set $A \subseteq \textbf{R}$ is *bounded above* if there exists a number 
$\text{b} \in \textbf{R}$ such that $a \leq b$ for all $a \in A$. The number b is called an *upper bound* for A. Similarly, the set A is *bounded below* if there exists a *lower bound* $l \in \textbf{R}$ satisfying $l \leq a$ for every $a \in A$.

Definition 1.3.2. A real number s is the least upper bound for a set $A \subseteq \textbf{R}$
if it meets the following two criteria:
(i) s is an upper bound for A;
(ii) if b is any upper bound for A, then $s \leq b$.

The least upper bound is also frequently called the supremum of the set A.
Although the notation s = lub A is sometimes used, we will always write s = sup A for the least upper bound. 
The greatest lower bound or *infimum* for A is defined in a similar way and is denoted by inf A.

$\large A = \{\frac{1}{n} : n \in N\} =  \{1, \frac{1}{2}, \frac{1}{3}, ... \}$

Important lesson to takeaway is that the infimum and supremum of A may not be elements of the set A. e.g. inf A = 0.

Definition 1.3.4. A real number $a_0$ is a *maximum* of the set A if $a_0$ is an element of A and $a_0 \leq a$ for all $a \in A$. Similarly, a number $a_1$ is a *minimum* of A if $a_1 \in A$ and $a_1 \leq a$ for every $a \in A$.

An example:
Consider the open interval
$\large (0, 2) = \{ x \in \textbf{R} : 0 \lt x \lt 2 \}$
and the closed interval
$\large [0, 2] = \{x \in \textbf{R} : 0 \leq x \leq 2 \}$.

Both sets are bounded above (and below), and both have the same least upper bound, 2. It is not the case, however that both sets have a maximum. A maximum is a specific type of upper bound that is required to be an element of the set in question, and the open interval (0, 2) does not possess such an element. Thus, the supremum can exist and not be a maximum, but when a maximum exists, then it is also the supremum.

Let us remind ourselves why the axiom of completeness is not a valid statement about $\textbf{Q}$.

An example:
Consider again the set 
$\large S = \{r \in \textbf{Q} : r^2 \lt 2\},$

If we go searching for a least upper bound, we might try b = 142/100 which is indeed an upper bound but not the lowest. This then goes onto an infinite regress where there isn't a suitable rational number that is the infimum of the set S. In the real numbers, there is. The axiom of completeness states that we may set $\alpha = sup S$ and be confident that such a number exists.

The following lemma offers an alternative way to restate part (ii) of the definition of the supremum.

Lemma 1.3.8. Assume $s \in \textbf{R}$ is an upper bound for a set $A \subseteq \textbf{R}$. Then, s = sup A if and only if, for every choice of $\epsilon \gt 0$, there exists an element $a \in A$ satisfying $s - \epsilon \lt a$ 

# 1.4 Consequences of Completeness
$\textbf{Theorem 1.4.1 (Nested Interval Property)} \text{. For each } n \in \textbf{N}\text{, assume we are given a closed interval }$
$I_n =  [a_n, b_n]  = \{ x \in \textbf{R} : a_n \leq x \leq b_n\}$
$\text{Assume also that each } I_n \text{ contains } I_{n+1}\text{. Then, the resulting nested sequence of closed intervals}$ $I_1 \supseteq I_2 \supseteq I_3 \supseteq I_4 \supseteq ....$
$\text{has a nonempty intersection; that is } \bigcap\limits_{n = 1}^{\infty}I_n \neq \emptyset$

**The Density of Q in R**
$\textbf{Theorem 1.4.2 (Archimedean Property). } \text{(i) Given any number } x \in \textbf{R}\text{, there exists an} n \in \textbf{N}\text{ satisfying } n \gt x$
$\text{(ii) Given any real number } y \gt 0\text{, there exists an } n \in \textbf{N }\text{satisfying } \frac{1}{n} \lt y$.



**Summary in my own words:**

**1.3**
An axiom in mathematics is an accepted assumption, to be used without proof.
Essentially the definition of $\textbf{R}$ is made by the axiom of completeness which essentially states that any non-empty set of real numbers has a least upper bound. Meaning you can always find a number such that anything lower than that number must be in the set or is either the least upper bound. This is what gives the "infinite" appearance of any interval/set of real numbers.

**1.4**


**What I do not know:**



**References**
*Stephen Abbott's*
**Understanding Analysis**

[^1]: A proof of the flipped and negated version of the statement proves the original statement.