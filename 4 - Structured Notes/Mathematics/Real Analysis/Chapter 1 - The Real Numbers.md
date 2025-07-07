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
$\textbf{Theorem 1.4.2 (Archimedean Property). } \text{(i) Given any number } x \in \textbf{R}\text{, there exists an } n \in \textbf{N}\text{ satisfying } n \gt x$
$\text{(ii) Given any real number } y \gt 0\text{, there exists an } n \in \textbf{N }\text{satisfying } \frac{1}{n} \lt y$.

$\textbf{Theorem 1.4.3 (Density of Q in R.)}$ 
$\text{For every two real numbers a and b with a } \gt \text{b, } \text{there exists a rational number r satisfying } a \lt r \lt b$
$\textbf{Corollary 1.4.4. } \text{Given any two real numbers } a \lt b,$
$\text{there exists an irrational number t satisfying } a \lt t \lt b$.

**The Existence of Square Roots**

$\textbf{Theoreom 1.4.5.} \text{ There exists a real number } \alpha \in \textbf{R } \text{satisfying } \alpha^2 = 2.$

Proof. Consider the set:
$\large T = \text{\{}t \in \textbf{R} : t^2 \lt 2 \text{\}}$

and set $\alpha = \text{supT}$. We are going to prove $\alpha^2 = 2$ by ruling out the possibilities $\alpha^2 \lt 2$ and $\alpha^2 \gt 2$. 
Let's assume that $\alpha^2 \lt 2$. In search of an element of T that is larger than $\alpha$, write

$\LARGE (\alpha + \frac{1}{n})^2 = \alpha^2 + \frac{2\alpha}{n} + \frac{1}{n^2}$

$\LARGE \lt \alpha^2 + \frac{2\alpha}{n} + \frac{1}{n}$

$\LARGE =\alpha^2 + \frac{2\alpha +1}{n}$

But now assuming $\alpha^2 \lt 2$ gives us a little space in which to fit the $(2\alpha + 1) / n$
term and keep the total less than 2. Specifically, choose $n_0 \in \textbf{N}$ large enough so that

$\LARGE \frac{1}{n_0} \lt \frac{2 - \alpha^2}{2\alpha + 1}$

This implies $(2\alpha + 1) / n_0 \lt 2 - \alpha^2$, and consequently that

$\LARGE (\alpha + \frac{1}{n_0})^2 \lt \alpha^2 + (2 - \alpha^2) = 2$

Thus, $\alpha + 1 / n_0 \in T$, contradicting the fact that \alpha is an upper bound for T. We conclude that $\alpha^2 \lt 2$ cannot happen.

Now the case for $\alpha^2 \gt 2$ we write

$\LARGE (\alpha - \frac{1}{n})^2 = \alpha^2 - \frac{2\alpha}{n} + \frac{1}{n^2}$

$\LARGE \gt \alpha^2 - \frac{2\alpha}{n}$

Since we assumed $\alpha^2 \gt 2$, there is a positive "gap" of $\alpha^2 - 2$. We want to choose n large enough such that by subtracting $\large \frac{2\alpha}{n}$, we still remain above 2, meaning $\alpha - \frac{1}{n}$ is still too large to be in T and could potentially be a smaller upper bound.
Specifically, we want to choose $n_1 \in \textbf{N}$ large enough such that:

$\LARGE \frac{2\alpha}{n_1} \lt \alpha^2 - 2$

This is possible because $\alpha^2 - 2 \gt 0$. We can rewrite this inequality as:

$\LARGE n_1 \gt \frac{2\alpha}{\alpha^2 - 2}$ 

By the Archimedian property, such an $n_1$ exists.
We know:

$\LARGE (\alpha - \frac{1}{n_1})^2 \gt \alpha^2 - \frac{2\alpha}{n_1}$

Combining these, we get:

$\LARGE (\alpha - \frac{1}{n_1})^2 \gt 2$

This means that any $t \in T$ must satisfy $t^2 \lt 2$. Since $\large (\alpha - \frac{1}{n_1})^2 \gt 2$, it follows that
$\alpha - \frac{1}{n_1}$ cannot be in T. More importantly, for any $t \in T$, we must have $t \leq \sqrt{2}$. Since
$\alpha - \frac{1}{n_1} \gt \sqrt{2}$ (because its square is greater than 2), it follows that $\alpha - \frac{1}{n_1}$ is an upper bound for T.

Contradiction... We have found an upper bound for T, namely $\alpha - \frac{1}{n_1}$.
However, since $n_1 \in \textbf{N}$, $\frac{1}{n_1} \gt 0$, which implies:

$\LARGE \alpha - \frac{1}{n_1} \lt \alpha$

This means we have found an upper bound for T ($\alpha - \frac{1}{n_1}$) that is strictly smaller than $\alpha$.
This contradicts the definition of $\alpha$ as the least upper bound (supremum) of T.

# 1.5 Cardinality

**1 - 1 Correspondence**
The term cardinality is used in mathematics to refer to the size of a set. The cardinalities of finite sets can be compared simply by attaching a natural number to each set.

**Definition 1.5.1.** 
$\text{A function } f : A \rightarrow B \text{ is one-to-one if } a_1 \neq a_2$
$\text{in A implies that } f(a_1) \neq f(a_2) \text{ in B. The function } f \text{ is onto if, given any } b \in B \text{,}$
$\text{it is possible to find an element } a \in A \text{ for which } f(a) = B$.

**Definition 1.5.2.** $\text{The set A has the same cardinality as B if there exists } f : A \rightarrow B \text{ that is 1-1 and onto.}$ 
$\text{In this case, we write } A \sim B$.

**Definition 1.5.5.**
A set $A$ is countable if $\textbf{N} \sim A$. An infinite set that is not countable is called an uncountable set.

**Theorem 1.5.6.**
(i) The set $\textbf{Q}$ is countable. (ii) The set $\textbf{R}$ is uncountable.

Proof for (ii). Assume that there does exist a 1-1, onto function $f : \textbf{N} \rightarrow \textbf{R}$.
This suggests that it is possible to enumerate the elements of $\textbf{R}$. If we let $x_1 = f(1)$,$x_2 = f(2)$, and so on, then our assumption that $f$ is onto means that we can write

(1)   $\large \textbf{R} = \{x_1, x_2, x_3, x_4, ...\}$
and be confident that every real number appears somewhere on the list. We will now use the Nested Interval Property to produce a real number that is not there.

Let $I_1$ be a closed interval that does not contain $x_1$. Next, let $I_2$ be a closed interval, contained in $I_1$, which does not contain $x_2$. The existence of such an $I_2$ is easy to verify.
Certainly $I_1$ contains two smaller disjoint closed intervals, and $x_2$ can only be in one of these. In general, given an interval $I_n$, construct $I_{n+1}$ to satisfy

(i) $\large I_{n+1} \subseteq I_n$ and

(ii) $\large x_{n+1} \notin I_{n+1}$

We now consider the intersection $\bigcap_{n = 1}^{\infty} I_n$. If $x_{n0}$ is some real number from the list in (1), then we have $x_{n0} \notin I_{n0}$, and it follows that

$\large x_{n0} \notin \bigcap_{n=1}^{\infty} I_n$.

Now, we are assuming that the list in (1) contains every real number, and this leads to the conclusion that 

$\large \bigcap_{n=1}^{\infty} I_n = \emptyset$.

However, the Nested Interval Property asserts that $\large \bigcap_{n=1}^{\infty} I_n \neq \emptyset$.
By NIP, there is at least one $x \in \cap_{n=1}^{\infty} I_n$ that, consequently, cannot be on the list in (1). This contradiction means that such an enumeration of $\textbf{R}$ is impossible, and we conclude that $\textbf{R}$ is an uncountable set. Because $\textbf{R} = \textbf{Q} \cup \textbf{I}$, it follows that $\textbf{I}$ cannot be countable otherwise $\textbf{R}$ would be.

**Theorem 1.5.7.**
If $A \subseteq B$ and $B$ is countable, then $A$ is either countable or finite.

**Theorem 1.5.8.**
(i) If $A_1$, $A_2$, ... , $A_m$ are each countable sets, then the union $A_1 \cup A_2  \cup$ ... $\cup A_m$ is countable.

(ii) If $A_n$ is a countable set for each $n \in \textbf{N}$, then $\bigcup_{n=1}^{\infty} A_n$ is countable.

# 1.6 Cantor's Theorem

**Cantor's Diagonalization Method**
Cantor published his discovery that $\textbf{R}$ is uncountable in 1874. Although it has some modern polish on it, the argument presented in Theorem 1.5.6. (ii) is actually quite similar to the one Cantor originally found. In 1891, Cantor offered another proof of this same fact that is startling in its simplicity. It relies on decimal representations for real numbers, which we will accept and use without any formal definitions.

**Theorem 1.6.1.** 
The open interval $(0, 1) = \{ x \in \textbf{R} : 0 \lt x \lt 1 \}$ is uncountable.

Proof. As with Theorem 1.5.6, we proceed by contradiction and assume that there does exist a function $f : \textbf{N} \rightarrow (0, 1)$ that is 1-1 and onto. For each $m \in \textbf{N}$, $f(m)$ is a real number between 0 and 1,  and we represent it using the decimal notation

$\large f(m) = . a_{m1}a_{m2}a_{m3}a_{m4}....$

What is meant here is that for each $m$, $n \in \textbf{N}$, $a_{mn}$ is the digit from the set $\{0, 1, 2, ... , 9\}$ that represents the nth digit in the decimal expansion of $f(m)$. The 1-1 correspondence between $\textbf{N}$ and $(0, 1)$ can be summarized in the doubly indexed array.
![[Pasted image 20250706211011.png]]

So, $a_{11}$ is the 1st digit of the 1st number on the list. The key assumption about this correspondence is that every real number in (0, 1) is assumed to appear somewhere on the list. Now for the pearl of the argument. Define a real number $x \in (0, 1)$ with the decimal expansion $x$ = $.b_1b_2b_3b_4..$ using the rule
$$
\large b_n = \begin{cases} 
2 & \text{if } a_{nn} \neq 2 \\
3 & \text{if }a_{nn} = 2
\end {cases}
$$

Let's be clear about this. To compute the digit $b_1$, we look at the digit $a_{11}$ in the upper left-hand corner of the array. If $a_{11} = 2$, then we choose $b_1 = 3$; otherwise, we set $b_1 = 2$.
To compute $b_2$ we look at $a_{22}$. If $a_{22} = 2$, we choose $b_2 = 3$; otherwise, we set $b_2 = 2$. In general, to compute $b_n$, we look at $a_{nn}$, the nth digit of $f(n)$. If $a_{nn} = 2$, we choose $b_n = 3$;
otherwise, we set $b_n = 2$.

Now, we have constructed a real number $x = .b_1b_2b_3b_4...$ such that $x \in (0, 1)$. We claim that $x$ is not on the list $f(1)$, $f(2)$, $f(3)$,...

Consider any $f(m)$ from the list. We want to show that $x \neq f(m)$.
By construction, the mth digit of $x$ is $b_m$. The mth digit of $f(m)$ is $a_{mm}$.

Since the mth digit $x (b_m)$ is different from the mth digit of $f(m) (a_{mm})$, it follows that $x \neq f(m)$. This is true for every $m \in \textbf{N}$.

Therefore, the number $x$ is in $(0, 1)$ but does not appear anywhere on the list. This contradicts our initial assumption that the function $f$ is onto, meaning that it maps $\textbf{N}$ to all numbers in $(0,1)$.

This contradiction proves that our initial assumption (that there exists a function $f : \textbf{N} \rightarrow (0,1)$ that is 1-1 and onto) must be false. Hence, no such bijection exists, and the open interval $(0,1)$ is uncountable.

**Power Sets and Cantor's Theorem**
Given a set $A$, the power set $P(A)$ refers to the collection of all subsets of $A$. It is important to understand that $P(A)$ is itself considered a set whose elements are the different possible subsets of A.

**Theorem 1.6.2. (Cantor's Theorem)**.
Given any set $A$, there does not exist a function $f : A \rightarrow P(A)$ that is onto.

Proof. This proof, like the others of its kind, is indirect. Thus, assume, for contradiction, that $f : A \rightarrow P(A)$ is onto. Unlike the usual situation in which we have sets of numbers for the domain and range, $f$ is a correspondence between a set and its power set. For each element $a \in A$, $f(a)$ is a particular subset of $A$. 

The assumption that $f$ is onto means that every subset of $A$ appears as $f(a)$ for some $a \in A$. To arrive at a contradiction, we will produce a subset $B \subseteq A$ that is not equal to $f(a)$for any $a \in A$.
Construct $B$ using the following rule. For each element $a \in A$, consider the subset $f(a)$. This subset of $A$ may contain the element $a$ or it may not. This depends on the function $f$. If $f(a)$ does not contain $a$, then we include $a$ in our set $B$. More precisely, let

$\large B = \{a \in A : a \notin f(a) \}$.

**1.7 Epilogue**
The relationship of having the same cardinality is an equivalence relation, meaning, roughly, that all of the sets in the mathematical universe can be organized into disjoint groups according to their size. Two sets appear in the same group, or equivalence class, if and only if they have the same cardinality. Thus, $\textbf{N}$, $\textbf{Z}$, and $\textbf{Q}$ are grouped together in one class with all of the other countable sets, whereas $\textbf{R}$ is in another class that includes the intervals $(a, b)$ as well as $P(\textbf{N})$. One implication of Cantor's Theorem is that $P(\textbf{R})$ - the set of all subsets of $\textbf{R}$ - is in a different class from $\textbf{R}$, and there is no reason to stop there. The set of subsets of $P(\textbf{R})$ - namely $P(P(\textbf{R}))$ - is in yet another class, and this process continues indefinitely.

Having divided the universe of sets into disjoint groups, it would be convenient to attach a "number" to each collection which could be used the way natural numbers are used to refer to the sizes of finite sets. Given a set $X$, there exists something called the cardinal number of $X$, denoted card $X$, which behaves very much in this fashion. For instance, two sets $X$ and $Y$ satisfy card $X =$ card $Y$ if and only if $X \sim Y$. (Rigorously defining card $X$ requires some significant set theory. One way this is done is to define card $X$ to be a very particular set that can always be uniquely found in the same equivalence class as $X$.)

Looking back at Cantor's Theorem, we get the strong sense that there is an order on the sizes of infinite sets that should be reflected in our new cardinal number system. Specifically, if it is possible to map a set $X$ into $Y$ in a 1-1 fashion, 
then we want card $X \leq$ card $Y$. Writing the strict inequality card $X \lt$ card $Y$ should indicate that it is possible to map $X$ into $Y$ but that it is not the case that $X \sim Y$. Restated in this notation, Cantor's Theorem states that for every set $A$, 
card $A \lt$ card $P(A)$.

There are some significant details to work out. A kind of metaphysical problem arises when we realise that an implication of Cantor's Theorem is that there can be no "largest" set. A declaration such as, "Let $U$ be the set of all possible things," is paradoxical because we immediately get that card $U \lt$ card $P(U)$ and thus the set $U$ does not contain everything that it was advertised to hold. Issues such as this one are ultimately resolved by imposing some restrictions on what can qualify as a set. As set theory was formalised, the axioms had to be crafted so that objects such as $U$ are simply not allowed. A more down-to-earth problem in need of attention is demonstrating that our definition of "$\leq$" between cardinal numbers really is an ordering. This involves showing that cardinal numbers possess a property analogous to real numbers, which states that if card $X \leq$ card $Y$ and card $Y \leq$ card $X$, then card $X =$ card $Y$. In the end, this boils down to proving that if there exists $f : X \rightarrow Y$ that is 1-1, and if there exists $g : Y \rightarrow X$ that is 1-1, then it is possible to find a function $h : X \rightarrow Y$ that is both 1-1 and onto. A proof of this fact eluded Cantor but was eventually supplied independently by Ernst Schroeder (in 1896) and Felix Bernstein (in 1898). 

There was another deep problem stemming from the budding theory of cardinal numbers that occupied Cantor and which was not resolved during his lifetime. Because of the importance of countable sets, the symbol $\aleph_0$ is frequently used for card $\textbf{N}$. The subscript "0" is appropriate when we remember that countable sets are the smallest type of infinite set. In term of cardinal numbers, if card $X \lt$ $\aleph_0$, then $X$ is finite. Thus, $\aleph_0$ is the smallest infinite cardinal number. The cardinality of $\textbf{R}$ is also significant enough to deserve the special designation $\textbf{c} =$ card $\textbf{R}$ = card $(0,1)$. The question that plagued Cantor was whether there were any cardinal numbers strictly in between these two. Cantor was of the opinion that no such set existed. In the ordering of cardinal numbers, he conjectured, c was the immediate successor of $\aleph_0$.

Cantor's "continuum hypothesis," as it came to be called, was one of the most famous mathematical challenges of the past century. Its unexpected resolution came in two parts. 
In 1940, the German logician and mathematician Kurt Godel demonstrated that, using only the agreed-upon set of axioms of set theory, there was no way to disprove the continuum hypothesis. In 1963, Paul Cohen successfully showed that, under the same rules, it was also impossible to prove this conjecture. Taken together, what these two discoveries imply is that the continuum hypothesis is undecidable. It can be accepted or rejected as a statement about the nature of infinite sets, and in neither case will any logical contradictions arise.

The mention of Kurt Godel brings to mind a final comment about the significance of Cantor's work. Godel is best known for his "Incompleteness Theorems," which pertain to the strength of axiomatic systems in general. What Godel showed was that any consistent axiomatic system created to study arithmetic was necessarily destined to be "incomplete" in the sense that there would always be true statements that the system of axioms would be too weak to prove. At the heart of Godel's very complicated proof is a type of manipulation closely related to what is happening in the proofs of Theorems 1.6.1 and 1.6.2.
Variations of Cantor's proof methods can also be found in the limitative results of computer science. The "halting problem" asks, loosely, whether some general algorithm exists that can look at every program and decide if that program eventually terminates. The proof that no such algorithm exists uses a diagonalization-type construction at the core of the argument. The main point to make is that not only are the implications of Cantor's theorem profound but the argumentative techniques are as well. 

**Summary in my own words:**

**1.3**
An axiom in mathematics is an accepted assumption, to be used without proof.
Essentially the definition of $\textbf{R}$ is made by the axiom of completeness which essentially states that any non-empty set of real numbers has a least upper bound. Meaning you can always find a number such that anything lower than that number must be in the set or is either the least upper bound. This is what gives the "infinite" appearance of any interval/set of real numbers.

**1.4**
Nested Interval Property is essentially saying that, for example, given a rope, if you continuously cut equal length of each ends of the rope, there will always be a little bit of rope left in the middle. So there always exists a real number between an interval

Archimedian Property is an important property that ensures that you can always find a natural number greater than any given real number, no matter how big that real number is as well as being able to find a unit fraction that is smaller for any positive real number. A direct consequence of the Archimedian Property is that between any two distinct real numbers, there exists a rational number (The rational numbers are dense in the real numbers).

**1.5**
Size of sets are an important property to consider, especially when comparing sets. This was first year mathematics in my course.

**1.6**
Cantor's diagonalization theorem basically shows that we can try to construct a list of real numbers represented by natural numbers and find a number that is not apart of the list but is apart of the interval, proving that the function that maps from natural numbers to real numbers is not onto, showing the difference in cardinality. Since no bijection exists, the interval $(0,1)$ is uncountable and so is the real number set.

**References**
*Stephen Abbott's*
**Understanding Analysis**

[^1]: A proof of the flipped and negated version of the statement proves the original statement.