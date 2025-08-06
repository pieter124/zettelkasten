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

**References**
*Stephen Abbott's*
**Understanding Analysis**
