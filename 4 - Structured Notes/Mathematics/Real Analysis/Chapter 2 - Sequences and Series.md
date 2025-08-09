2025-07-09 

Tags: [[mathematics]]

# **Chapter 2 - Sequences and Series**

**2.1 Discussion: Rearrangements of Infinite Series**

Consider the infinite series:

$\large \sum_{n =1}^{\infty} \frac{(-1)^{n + 1}}{n} = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \frac{1}{5}...$

If we naively begin adding from the left-hand side, we get a sequence of what are called $\text{partial sums}$. In other words, let $s_n$ equal the sum of the first $n$ terms of the series, so that $s_1 = 1$, $s_2 = \frac{1}{2}$, $s_3 = \frac{5}{6}$, $s_4 = \frac{7}{12}$, and so on. One immediate observation is that the successive sums oscillate in a progressively narrower space. The odd sums decrease ($s_1 \gt s_3 \gt s_5 \gt ...$) while the even sums increase.

$\large s_2 \lt s_4 \lt s_6 \lt ... S ... \lt s_5 \lt s_3 \lt s_1$
It seems reasonable - and we will soon prove that the sequence ($s_n$) eventually hones in on a value, call it S, where the odd and even partial sums "meet". At this moment, we cannot compute S precisely, but we know it falls somewhere between 7/12 and 5/6. Summing a few hundred terms reveals that $S \approx .69$. Whatever its value, there is now an overwhelming temptation to write

(1) $\large S = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \frac{1}{5} ...$

meaning, perhaps, that if we could indeed add up all infinitely many of these numbers, then the sum would equal $S$. A more familiar example of an equation of this type might be

$\large 2 = 1 + \frac{1}{2} + \frac{1}{4} + \frac{1}{8} + \frac{1}{16} ...$

the only difference being that in the second equation we have a more recognizable value for the sum.
But now for the crux of the matter. The symbols $+$, $-$, and $=$ in the preceding equations are deceptively familiar notions being used in a very unfamiliar way. The crucial question is whether or not properties of addition and equality that are well understood for finite sums remain valid when applied to infinite objects such as equation (1). The answer, as we are about to witness, is somewhat ambiguous.

Treating equation (1) in a standard algebraic way, let's multiply through by $\frac{1}{2}$ and add it back to equation (1):

$\large \frac{1}{2}S = \frac{1}{2} - \frac{1}{4} + \frac{1}{6}....$

$\large +  S = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \frac{1}{5} - \frac{1}{6}...$

(2) $\large \frac{3}{2}S = 1 + \frac{1}{3} - \frac{1}{2} + \frac{1}{5} + \frac{1}{7} - \frac{1}{4}...$

Now, look carefully at the result. The sum in equation (2) consists precisely of the same terms as those in the original equation (1), only in a different order. Specifically, the series in (2) is a rearrangement of (1) where we list the first two positive terms ($1 + \frac{1}{3}$) followed by the first negative term ($-\frac{1}{2}$), followed by the next two positive terms and then the next negative term.

Continuing this, it is apparent that every term in (2) appears in (1) and vice versa.
The rub comes when we realize that equation (2) asserts that the sum of these rearranged, but otherwise unaltered, numbers is equal to $\frac{3}{2}$ its original value. Indeed, adding a few hundred terms of equation (2) produces partial sums in the neighborhood of $1.03$. Addition, in this infinite setting, is not commutative!

Let's look at a similar rearrangement of the series.

$\large \sum_{n = 0}^{\infty} (-\frac{1}{2})^n$

This series is geometric with first term 1 and common ratio $r = -\frac{1}{2}$. Using the formula 
$1 / (1 - r)$ for the sum of a geometric series, we get 

$\large 1 - \frac{1}{2} + \frac{1}{4} - \frac{1}{8} + \frac{1}{16} - \frac{1}{32} ... =$

$\large \frac{1}{1 - (-\frac{1}{2})} = \frac{2}{3}$ 

This time, some computational experimentation with the "two positives, one negative" rearrangement yields partial sums quite close to $\frac{2}{3}$. The sum of the first 30 terms, for instance, equals $0.66667$. Infinite addition is commutative in some instances but not in others.

Far from being a charming theoretical oddity of infinite series, this phenomenon can be the source of great consternation in many applied situations. How, for instance, should a double summation over two index variables be defined? Let's say we are given a grid of real numbers $\{a_{ij} : i, j \in \textbf{N}\}$, where $\large a_{ij} = \frac{1}{2^{j - i}}$ if $j \gt i$, $a_{ij} = -1$ if $j = i$, 
and $a_{ij} = 0$ if $j \lt i$.

![[Pasted image 20250719181621.png]]

We would like to attach a mathematical meaning to the summation

$\large \sum_{i, j = 1}^{\infty} a_{ij}$

whereby we intend to include every term in the preceding array in the total. One natural idea is to temporarily fix i and sum across each row. A moment’s reflection (and a fact about geometric series) shows that each row sums to 0. Summing the sums of the rows, we get

$\large \sum_{i, j  = 1}^{\infty} a_{ij} = \sum_{i = 1}^{\infty} (\sum_{j = 1}^{\infty} a_{ij})$

$\large = \sum_{i = 1}^{\infty} (0) = 0$

We could just as easily have decided to fix $j$ and sum down each column first.
In this case, we have

$\large \sum_{i, j  = 1}^{\infty} a_{ij} = \sum_{j = 1}^{\infty} (\sum_{i = 1}^{\infty} a_{ij})$

$\large =  \sum_{j = 1}^{\infty} (\frac{-1}{2^{j - 1}}) = -2$

Changing the order of the summation changes the value of the sum! One common way that double sums arise (although not this particular one) is from the multiplication of two series. 

Essentially, An infinite series $\sum a_n$​ is **absolutely convergent** if the series of the absolute values, $\sum |a_n|$, converges. If a series is absolutely convergent, then you can rearrange the terms in any way you want, and the sum will always be the same. The commutative property of addition, which we take for granted with finite sums, holds for absolutely convergent infinite series.

The product of two infinite series can be represented as a double summation, but for the result to be well-defined and independent of the order of summation, at least one of the original series must be **absolutely convergent**. This ensures that the double summation is also absolutely convergent, and its value is independent of the order in which you sum the terms.

A common method for multiplying series is the **Cauchy product**, where you sum the terms along diagonals:

$\large (\sum_{i = 0}^{\infty} a_i)(\sum_{j = 0}^{\infty} b_j) = \sum_{k = 0}^{\infty} c_k$, where $\large c_k = \sum_{i = 0}^{k} a_i b_{k - i}$ 

Manipulations that are legitimate in finite settings do not always extend to infinite settings. Deciding when they do and why they do not is one of the central themes of analysis.

# 2.2 The Limit of a Sequence

An understanding of infinite series depends heavily on a clear understanding of the theory of sequences. In fact, most of the concepts in analysis can be reduced to statements about the behaviour of sequences. Thus, we will spend a significant amount of time investigating sequences before taking on infinite series.

**Definition 2.2.1.** A $sequence$ is a function whose domain is $\textbf{N}$.

This formal definition leads immediately to the familiar depiction of a sequence as an ordered list of real numbers. Given a function $f : \textbf{N} \rightarrow \textbf{R}$, $f(n)$ is just the nth term on the list. The notation for sequences reinforces this familiar understanding.

On occasion, it will be more convenient to index a sequence beginning with n = 0 or n = $n_0$ for some natural number $n_0$ different from 1. These minor variations should cause no confusion. What is essential is that a sequence be an $\text{infinite}$ list of real numbers. What happens at the beginning of such a list is of little importance in most cases. The business of analysis is concerned with the behaviour of the infinite "tail" of a given sequence.

We now present what is arguably the most important definition in the book.

$\textbf{Definition 2.2.3 (Convergence of a Sequence).}$
A sequence ($a_n$) converges to a real number $a$ if, for every positive number $\epsilon$, there exists an $N \in \textbf{N}$ such that whenever $n \geq N$ it follows that $|a_n - a| \lt \epsilon$.

To indicate that ($a_n$) converges to $a$, we usually write $\text{lim}a_n = a$ or ($a_n$) $\rightarrow a$. The notation $\text{lim}_{n \rightarrow \infty} a_n = a$ is also standard.

$\textbf{Definition 2.2.4.}$
Given a real number $a \in \textbf{R}$ and a positive number $\epsilon \gt 0$, the set

$\large V_\epsilon(a) = \{x \in \textbf{R} :  |x - a| \lt \epsilon \}$ 

is called the $\epsilon \text{-neighborhood}$ of a.

Notice that $V_\epsilon(a)$ consists of all of those points whose distance from $a$ is less than $\epsilon$. Said another way, $V_\epsilon(a)$ is an interval, centered at $a$, with radius $\epsilon$.
![[Pasted image 20250806084937.png]]

Recasting the definition of convergence in terms of $\epsilon\text{-neighborhoods}$ gives a more geometric impression of what is being described.

$\textbf{Definition 2.2.3B (Convergence of a Sequence: Topological Version)}$
A sequence ($a_n$) converges to $a$ if, given any $\epsilon\text{-neighborhood}$ $V_\epsilon(a)$ of $a$, there exists a point in the sequence after which all of the terms are in $V_\epsilon(a)$. In other words, every $\epsilon\text{-neighborhood}$ contains all but a finite number of the terms of ($a_n$).
![[Pasted image 20250806085310.png]]

$\textbf{Definition 2.2.3}$ and $\textbf{Definition 2.2.3B}$ say precisely the same thing; the natural number $N$ in the original version of the definition is the point where the sequence ($a_n$) enters $V_\epsilon(a)$, never to leave. It should be apparent that the value of $N$ depends on the choice of $\epsilon$. The smaller the $\epsilon$-neighborhood, the larger $N$ may have to be.

We claim that 

$\large \text{lim}(\frac{1}{\sqrt{n}}) = 0$.

Proof. Let $\epsilon \gt 0$ be an arbitrary positive number. Choose a natural number $N$ satisfying 

$\large N \gt \frac{1}{\epsilon^2}$.

We now verify that this choice of $N$ has the desired property. Let $n \geq N$. Then,

$\large n \gt \frac{1}{\epsilon^2}$ implies $\large \frac{1}{\sqrt{n}} \lt \epsilon$, and hence $\large |a_n - 0| \lt \epsilon$. QED.

$\large \textbf{Quantifiers}$

The definition of convergence given earlier is the result of hundreds of years of refining the intuitive notion of limit onto a mathematically rigorous statement. The logic involved is complicated and is intimately tied to the use of the quantifiers "for all" and "there exists". Learning to write a grammatically correct convergence proof goes hand in hand with a deep understanding of why the quantifiers appear in the order that they do.

The definition begins with the phrase,

"For all $\epsilon \gt 0$, there exists $N \in \textbf{N}$ such that..."

Looking back at our first example, we see that our formal proof begins with, "Let $\epsilon \gt 0$ be an arbitrary positive number". This is followed by a construction of $N$ and then a demonstration that this choice of $N$ has the desired property. This, in fact, is a basic outline for how every convergence proof should be presented.

$\large \text{TEMPLATE FOR A PROOF THAT } (x_n) \rightarrow x$ :

- "Let $\epsilon \gt 0$ be arbitrary".
- Demonstrate a choice for $N \in \textbf{N}$. This step usually requires the most work, almost all of which is done prior to actually writing the formal proof.
- Now, show that $N$ actually works.
- "Assume $n \geq N$".
- With $N$ well chosen, it should be possible to derive the inequality $|x_n - x| \lt \epsilon$.

$\textbf{Example 2.2.6.}$ Show

$\large \text{lim}(\frac{n+1}{n}) = 1$

As mentioned, before attempting a formal proof, we first need to do some preliminary scratch work. In the first example, we experimented by assigning specific values to $\epsilon$ (and it is not a bad idea to do this again), but let us skip straight to the algebraic punch line. The last line of our proof should be that for suitably large values of $n$,

$\Large |\frac{n + 1}{n} - 1| \lt \epsilon$.

Because 

$\Large |\frac{n + 1}{n} - 1| = \frac{1}{n}$,

this is equivalent to the inequality $1/n \lt \epsilon$ or $n \gt 1/\epsilon$. Thus choosing N to be an integer greater than $1/\epsilon$ will suffice. With this work of the proof done, all that remains is the formal write up.

Proof. Let $\epsilon \gt 0$ be arbitrary. Choose $N \in \textbf{N}$ with $N \gt 1/\epsilon$. To verify that this choice of $N$ is appropriate, let $n \in \textbf{N}$ satisfy $n \geq N$. Then $n \geq N$ implies $n \gt 1/\epsilon$, which is the same as saying $1/n \lt \epsilon$. Finally, this means

$\large |\frac{n+1}{n} - 1| \lt \epsilon$,

as desired. QED.

It is instructive to see what goes wrong in the previous example if we try to prove that our sequence converges to some limit other than 1.

$\large \textbf{Theorem 2.2.7 (Uniqueness of Limits)}$.
The limit of a sequence, when it exists, must be unique.

Proof.
Let ($a_n$​) be a sequence of real numbers. We will prove this theorem by contradiction. Assume that the limit of ($a_n$​) exists but is not unique. This means there exist two distinct limits, $L1$​ and $L2​$, such that $L1​ \neq L2$​.

By the definition of a limit, for any $\epsilon \gt 0$, there exists a natural number $N1$​ such that for all $n \gt N1$​:

$∣a_n​ − L1​∣ \lt \epsilon$

Similarly, since $L2$​ is a limit of the sequence, there exists a natural number $N2$​ such that for all $n \gt N2​$:

$∣a_n​ − L2​∣ \lt \epsilon$

Since $L1 \neq L2$​, the distance between them is a positive number, i.e. $∣L1 ​− L2​∣ \gt 0$. Let's choose a specific value for $\epsilon$:

$\large \epsilon = \frac{|L1 - L2|}{2}$​

Now, let $N = max(N1​,N2​)$. For any $n \gt N$, both of the limit inequalities hold simultaneously. We can use the **triangle inequality** to analyze the distance between $L1$​ and $L2$​.

$|L1 ​− L2​| = |L1 ​− a_n ​+ a_n ​− L2​|$

By the triangle inequality, we have:

$|L1 ​− a_n ​+ a_n ​− L2​| \leq |L1 ​− a_n​| + |a_n ​−L2​|$

We also know that $|L1​ − a_n​| = |a_n​ − L1​|$. So, for any $n \gt N$:

$|L1 ​− L2​|  \leq |a_n​ − L1​| + |a_n ​− L2| \lt \epsilon + \epsilon = 2\epsilon$

Substituting our chosen value for $\epsilon$ back into the inequality, we get:

$|L1 ​− L2​| \lt 2(\frac{|L1 - L2|}{2})$

$|L1 ​− L2​| \lt |L1 ​− L2​|$

This final statement is a **contradiction**, as a number cannot be strictly less than itself. This contradiction proves that our initial assumption—that there exist two distinct limits—must be false. Therefore, the limit of a sequence must be unique. QED. [^1]

$\large \textbf{Divergence}$

Significant insight into the role of the quantifiers in the definition of convergence can be gained by studying an example of a sequence that does not have a limit.

$\textbf{Example 2.2.8}$ Consider the sequence

$\large (1, -\frac{1}{2}, \frac{1}{3}, -\frac{1}{4}, \frac{1}{5}, -\frac{1}{5}, \frac{1}{5}, -\frac{1}{5}, \frac{1}{5}, -\frac{1}{5}....)$.

How can we argue that this sequence does not converge to zero? Looking at the first few terms, it seems the initial evidence actually supports such a conclusion. Given a challenge of $\large \epsilon = \frac{1}{2}$, a little reflection reveals that after $N = 3$ all the terms fall into the neighborhood $\large (-\frac{1}{2}, \frac{1}{2})$. We could also handle $\large \epsilon = \frac{1}{4}$. (What is the smallest possible $N$ in this case?)

But the definition of convergence says "For all $\epsilon \gt 0..$," and it should be apparent that there is no response to a choice of $\large \epsilon = \frac{1}{10}$, for instance. This leads us to an important observation about the logical negation of the definition of convergence of a sequence.
To prove that a particular number $x$ is not the limit of a sequence $(x_n)$, we must produce a single value of $\epsilon$ for which no $N \in \textbf{N}$ works. More generally speaking, the negation of a statement that begins "For all P, there exists Q..." is the statement "For at least one P, no Q is possible...". For instance, how could we disprove the spurious claim that "At every college in the United States, there is a student who is at least seven foot tall"?

We have argued that the preceding sequence does not converge to 0. Let's argue against the claim that it converges to $\large \frac{1}{5}.$ Choosing $\large \epsilon = \frac{1}{10}$ produces the neighborhood $(1/10, 3/10)$. Although the sequence continually revisits this neighborhood, there is no point at which it enters and never leaves as the definition requires. Thus, no $N$ exists for $\large \epsilon = \frac{1}{10}$, so the sequence does not converge to $\large \frac{1}{5}$.

Of course, this sequence does not converge to any other real number, and it would be more satisfying to simply say that this sequence does not converge.

$\large \textbf{Definition 2.2.9.}$
A $\text{sequence}$ that does not $\text{converge}$ is said to $\text{diverge}$.

# 2.3 The Algebraic and Order Limit Theorems

The real purpose of creating a rigorous definition for convergence of a sequence is not to have a tool to verify computational statements such as $\text{lim}\frac{2n}{n + 2} = 2$. Historically, a definition of the limit like Definition 2.2.3 came 150 years after the founders of calculus began working with intuitive notions of convergence. The point of having such a logically tight description of convergence is so that we can confidently prove statements about convergent sequences in general. We are ultimately trying to resolve arguments about what is and is not true regarding the behaviour of limits with respect to the mathematical manipulations we intend to inflict on them.

As a first example, let us prove that convergent sequences are bounded. The term "bounded" has a rather familiar connotation but, like everything else, we need to be explicit about what it means in this context.

$\textbf{Definition 2.3.1.}$ A sequence ($x_n$) is bounded if there exists a number $M \gt 0$ such that $|x_n| \leq M$ for all $n \in \textbf{N}$.

Geometrically, this means that we can find an interval $[-M, M]$ that contains every term in the sequence $(x_n)$.

$\textbf{Theorem 2.3.2.}$ Every convergent sequence is bounded.

Proof. Assume $(x_n)$ converges to a limit $l$. This means that given a particular value of $\epsilon$, say $\epsilon = 1$, we know there must exist an $N \in \textbf{N}$ such that if $n \geq N$, then $x_n$ is in the interval $(l - 1, l + 1)$. Not knowing whether $l$ is positive or negative, we can certainly conclude that 

$|x_n| \lt |l| + 1$.

for all $n \geq N$.
![[Pasted image 20250809092433.png]]

We still need to worry (slightly) about the terms in the sequence that come before the $Nth$ term. Because there are only a finite number of these, we let

$\large M = max\{|x_1|, |x_2|, |x_3|, ..., |x_{N - 1}|, |l| + 1\}$

It follows that $|x_n| \leq M$ for all $n \in \textbf{N}$, as desired. QED.

This chapter began with a demonstration of how applying familiar algebraic properties (commutativity of addition) to infinite objects (series) can lead to paradoxical results. These examples are meant to instill in us a sense of caution and justify the extreme care we are taking in drawing our conclusions. The following theorems illustrate that sequences behave extremely well with respect to the operations of addition, multiplication, division, and order.

$\large \textbf{Theorem 2.3.3 (Algebraic Limit Theorem).}$
Let $\text{lim}a_n = a$, and $\text{lim}b_n = b$. Then,

(i) $\text{lim}(ca_n) = ca$, for all $c \in \textbf{R}$;
(ii) $\text{lim}(a_n + b_n) = a + b$;
(iii) $\text{lim}(a_nb_n) = ab$;
(iv) $\text{lim}(a_n/b_n) = a/b$, provided $b \neq 0$.

Proof. (i) Consider the case where $c \neq 0$. We want to show that the sequence $(ca_n)$ converges to $ca$, so the structure of the proof follows the template we described earlier. First we let $\epsilon$ be some arbitrary positive number. Our goal is to find some point in the sequence $(ca_n)$ after which we have

$\large |ca_n - ca| \lt \epsilon$.

Now,

$\large |ca_n - ca| = |c||a_n - a|$.

We are given that $(a_n) \rightarrow a$, so we know we can make $|a_n - a|$ as small as we like. In particular, we can choose an $N$ such that

$\large |a_n - a| \lt \dfrac{\epsilon}{|c|}$

whenever $n \geq N$. To see that this $N$ indeed works, observe that, for all $n \geq N$,

$\large |ca_n - ca| = |c| |a_n - a| \lt |c|\dfrac{\epsilon}{|c|} = \epsilon$.

Before embarking on a formal argument, it is a good idea to take an inventory of what we want to make less than $\epsilon$, and what we are given can be made small for suitable choices of $n$.

(ii) To prove this statement, we need to argue that the quantity

**References**
*Stephen Abbott's*
**Understanding Analysis**

[^1]: What a beautiful proof :)
