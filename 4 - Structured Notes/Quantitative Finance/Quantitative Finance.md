2025-06-11 

Tags: [[mathematics]] [[quant]]

# **Quantitative Finance**

Quants use mathematics, data and AI to make predictions on stocks and then place their bets using assets like currencies, options, futures and swaps, turning market swings into profit.

**So how do you model a stock using math?**

One approach is by looking at the percent change in price from day to day. In finance this is called the **return** (percent change). 

Another approach is by constructing a histogram from the data points collected in the year. The shape of the histogram is close to the normal distribution. This pattern shows up again and again in the quantitative finance space. 

In finance, we call the **mean of the normal distribution** the **return** and the **standard deviation**, the **risk**.

Some stocks move in ways that are related to each other. The **correlation** measures the **degree** in which two stocks tend to go up or down together. To tie risk, return, and correlation all together, we use a **higher dimensional normal distribution.**

From every side, we can see a bell curve but from a top-down view there is an oval (the sign of correlation).

**Modelling more stocks**
If we are modelling more than 2 stocks, we need more dimensions. So 500 stocks means figuring out 500 means, 500 standard deviations and nearly 125,000 correlation values. But we are short on data. On average, a month has 21 trading days, so we're looking at just 10,500 daily returns. It is nowhere close enough to estimate risks, returns and correlations for all 500 stocks with any real confidence. 

To make solid estimates, quants have to come up with clever models, find more data and use clever statistics. 

Most investors buy stocks, bonds, or funds. If the market goes up they are happy if it drops they are not. But professionals can make money even when prices drop, this is called **short selling**.

**Short selling**
- Instead of buying a stock, you sell it first, usually borrowing shares you don't own.
- You take the money from that sale, then wait.
- If the stock price falls, you buy it back at a lower price, return the shares, and keep the difference. But if the stock climbs instead, that's trouble.

**Pair trading**

Imagine two companies, A and B, based on the models we have built, we think A will outperform B over the next three months. This doesn't necessarily mean A will go up and B will go down, it just means A will do better than B. 

Let's say A is priced at £50 per share and B at £40 per share. To setup the trade, I short 25 shares of B taking in £1000. Then I use that £1000 to buy 20 shares of A. At this point I haven't put up any of my own money. We call this being short B and long A. This is what a **pair trade** is.

Jump ahead 3 months, both stocks have fallen £5 per share. So now I sell my 20 shares of A, I buy back 25 shares of B to return to the lender which costs £875. This results in £25 profit.

In finance, you can go long to profit when an asset rises or short to profit when it falls.
Price alone doesn't tell the whole story, what really matters is returns.

**Portfolio**
A carefully chosen collection of stocks.

One standard way to construct a portfolio is with **mean-variance optimization**, a mathematical technique that searches through all possible portfolios to find the best balance between expected return and risk. 

Let's explore this technique with a portfolio of all the stocks in the S&P 500.
Imagine we've got models that give us estimated returns and standard deviations from each stock along with the correlation from each pair of stocks. 

To organise this information, we bundle the expected returns into what's called a **return vector**, a list of 500 numbers. We put the standard deviations and correlations together into a **covariance matrix** of 500 by 500 grid of numbers. 

**How much money to put into each stock?**

We use something called a **weight vector** to handle that, a list of 500 unknown values, where **each number shows what percentage of our money goes into each stock.**

Our portfolio will behave like a new normal distribution. The **expected return** is given by the **dot product** of our **weight vector** and the **return vector.** The **risk**, or standard deviation is calculated using **matrix multiplication** using our **covariance matrix**.

We want to maximise returns and minimize risk. We have an **objective function**, a mathematical expression you want to maximise or minimize, sometimes called a **loss function**. Our goal is to find the weights that make the expression as large as possible, balancing return and risk according to our preferences.

But before we optimize, we need to decide what kind of portfolio we want:
- Are we sticking to just long positions?
	That means all the weights need to stay positive and they should add up to 1 so our capital is fully invested.
- Do we want both long and short positions?
	Some weights will be negative, representing the short positions.
- Should the portfolio be market neutral?
	That means the sum of all weights must be zero, balancing the longs and shorts.

Each of these requirements is called a **constraint**.

With our **loss function** and our **constraints** in place, we can use software to calculate the **optimal portfolio**, one that pushes our expected return as high as possible while keeping risk in check.

Nowadays, quants can use machine learning to predict trends and tap into new kinds of data. For instance, you could analyze credit card transaction data to see how consumer spending patterns are shifting. These insights come from what we call **alternative data**.

Some hedge funds go a different route. Pure speed. They place their computers right next to stock exchanges, cutting microseconds off every trade. That lets them spot tiny changes in supply and demand ahead of everyone else, racking up tiny profits thousands of times a second. This is known as **high frequency trading**.

**References**
*Socratica's*
**What is Quantitative Finance?:** https://www.youtube.com/watch?v=JVtUcM1sWQw