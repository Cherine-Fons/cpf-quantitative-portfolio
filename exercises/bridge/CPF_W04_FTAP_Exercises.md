# Week 4 Bridge — Fundamental Theorems of Asset Pricing Exercises

## Review Question 1

**Question.** Define no-arbitrage in a one-period, finite-state market.

**Answer.**

In a one-period finite-state market, **no-arbitrage** means there is no portfolio that costs nothing or produces money initially, can never lose money at the end of the period, and produces a strictly positive payoff in at least one state.

So an arbitrage would satisfy

```math
V_0\le 0,
```

while

```math
V_1(\omega)\ge 0
```

in every state, with

```math
V_1(\omega)>0
```

in at least one state.

The basic idea is that the market should not allow a riskless profit with no net investment.

## Review Question 2

**Question.** Explain what a state price vector represents.

**Answer.**

A **state price vector** assigns a current value to payoffs delivered in each possible future state.

If there are $`n`$ states, I can write it as

```math
\pi=(\pi_1,\ldots,\pi_n).
```

The component $`\pi_i`$ can be interpreted as the value assigned today to one unit of payoff delivered only in state $`i`$.

For every traded or attainable payoff $`Y`$, the state price vector must satisfy

```math
P(Y)=\sum_{i=1}^n \pi_iY_i.
```

Equivalently, if $`S_1`$ is the matrix of traded asset payoffs and $`S_0`$ is the vector of current prices,

```math
S_0=S_1^\top\pi.
```

Under no-arbitrage, a strictly positive state price vector exists.

In a complete market, the state price vector is unique and therefore gives a unique price for every contingent claim. In an incomplete market, more than one state price vector may satisfy the traded-asset pricing equations, so a non-replicable claim need not have a unique price.

## Review Question 3

**Question.** Describe the meaning of an equivalent martingale measure.

**Answer.**

An **equivalent martingale measure**, or risk-neutral probability measure, is a probability vector under which discounted asset prices behave like martingales.

In a one-period market,

```math
S_0 = \frac{1}{R} E_Q[S_1],
```

where $`R`$ is the gross risk-free return.

The word **equivalent** means that the risk-neutral measure assigns positive probability to the same states that are possible under the original probability measure.

I do not interpret risk-neutral probabilities as actual predictions of how likely the states are. They are pricing probabilities that make current asset prices consistent with discounted expected future payoffs.

## Review Question 4

**Question.** Explain the difference between completeness and incompleteness.

**Answer.**

A market is **complete** if every possible contingent claim can be replicated exactly using the traded assets.

In a finite-state model, this means the traded payoff vectors span the entire state space.

If there are $`n`$ states, completeness requires

```math
\operatorname{rank}(A)=n,
```

where $`A`$ is the payoff matrix.

A market is **incomplete** when some contingent claims cannot be replicated. In that case, the available securities do not span all possible state-dependent payoffs. Assuming no-arbitrage, FTAP II implies that the equivalent martingale measure is not unique, so non-replicable claims may have a range of arbitrage-free prices rather than one uniquely determined price.

## Review Question 5

**Question.** Summarize the statement of the first and second fundamental theorems.

**Answer.**

The **first fundamental theorem of asset pricing** says that, in a finite market, there is no arbitrage if and only if there exists an equivalent martingale measure. Equivalently, there must exist a strictly positive state price vector that correctly prices the traded assets.

The **second fundamental theorem** says that, assuming no-arbitrage, the market is complete if and only if the equivalent martingale measure is unique.

So the first theorem connects **no-arbitrage to existence**, while the second connects **completeness to uniqueness**.

# Exercises

## Exercise 1

**Question.** Construct a two-state market with one risk-free and one risky asset. Compute the state prices and verify no-arbitrage.

**Answer.**

I use a two-state market with an up state $`U`$ and a down state $`D`$.

The risk-free asset costs

```math
B_0=1
```

and pays

```math
B_1=(1,1).
```

The risky asset costs

```math
S_0=1
```

and pays

```math
S_1=(1.5,0.5).
```

Let the state prices be

```math
\pi_U,\pi_D.
```

Pricing the risk-free asset gives

```math
\pi_U+\pi_D=1.
```

Pricing the risky asset gives

```math
1.5\pi_U+0.5\pi_D=1.
```

Using

```math
\pi_D=1-\pi_U,
```

I obtain

```math
1.5\pi_U+0.5(1-\pi_U)=1,
```

so

```math
\pi_U=0.5
```

and

```math
\pi_D=0.5.
```

Therefore,

```math
\boxed{\pi=(0.5,0.5)}.
```

Both state prices are strictly positive, so this market satisfies the no-arbitrage condition.

Another way to see this is that any payoff that is nonnegative in every state and strictly positive in at least one state must have a strictly positive price under this state price vector. Therefore, I cannot obtain such a payoff for zero or negative cost.

## Exercise 2

**Question.** Given a three-state payoff matrix, determine whether the market is complete.

**Answer.**

Consider the following three-state payoff matrix, where the rows are states and the columns are traded assets:

```math
A=
\begin{pmatrix}
1&2&0\\
1&1&1\\
1&0&2
\end{pmatrix}.
```

The first asset can be viewed as a risk-free asset.

Notice that the third column satisfies

```math
A_3=2A_1-A_2.
```

So the three columns are not linearly independent.

Therefore,

```math
\operatorname{rank}(A)=2.
```

There are three states, so completeness would require rank $`3`$.

Thus,

```math
\boxed{\text{the market is incomplete}.}
```

Even though there are three traded securities, they provide only two independent payoff directions. Some three-state claims therefore cannot be replicated.

## Exercise 3

**Question.** Price a contingent claim using state prices and compare the result to a replication strategy.

**Answer.**

I use the same two-state market from Exercise 1.

The state prices are

```math
\pi=(0.5,0.5).
```

Consider a contingent claim paying

```math
H=(1,0).
```

It pays $`1`$ in the up state and $`0`$ in the down state.

Using state prices,

```math
P(H) = 0.5(1)+0.5(0) = \boxed{0.5}.
```

Now I replicate the claim.

Let $`x`$ be the amount invested in the risk-free asset and $`y`$ the number of units of the risky asset.

I need

```math
x+1.5y=1
```

in the up state and

```math
x+0.5y=0
```

in the down state.

Subtracting gives

```math
y=1.
```

Then

```math
x+0.5=0,
```

so

```math
x=-0.5.
```

Therefore, the replicating portfolio is

```math
\boxed{x=-0.5,\qquad y=1}.
```

Its initial cost is

```math
-0.5(1)+1(1)=0.5.
```

Its state payoffs are

```math
-0.5+1.5=1
```

and

```math
-0.5+0.5=0.
```

So it exactly reproduces $`H=(1,0)`$.

The replication price is therefore

```math
\boxed{0.5},
```

which is exactly the same price obtained using state prices.

## Exercise 4

**Question.** Identify an arbitrage opportunity in a small market by constructing a zero-cost portfolio with positive payoffs.

**Answer.**

Consider two securities in a two-state market.

The ordinary risk-free bond has

```math
B_0=1
```

and payoff

```math
B_1=(1,1).
```

Suppose another security has price

```math
X_0=0.9
```

but has exactly the same payoff

```math
X_1=(1,1).
```

Since the two assets have identical future payoffs but different current prices, there is an arbitrage.

I buy one unit of the cheaper security and short $`0.9`$ units of the bond.

The initial cost is

```math
0.9-0.9(1)=0.
```

The final payoff in either state is

```math
1-0.9=0.1.
```

Therefore, the portfolio has payoff

```math
\boxed{(0.1,0.1)}.
```

So I have

```math
V_0=0
```

and

```math
V_1=(0.1,0.1)>0.
```

This is an explicit arbitrage because the portfolio costs nothing initially and produces a positive payoff in every state.

## Exercise 5

**Question.** Use a risk-neutral probability vector to price a payoff and confirm that it matches the state price approach.

**Answer.**

Again I use the two-state market from Exercise 1.

Since the risk-free gross return is

```math
R=1,
```

the state prices and risk-neutral probabilities are related by

```math
\pi_i=\frac{q_i}{R}.
```

Because

```math
\pi=(0.5,0.5),
```

the risk-neutral probability vector is

```math
\boxed{Q=(0.5,0.5)}.
```

For the claim

```math
H=(1,0),
```

risk-neutral pricing gives

```math
P(H) = \frac{1}{R}E_Q[H].
```

Therefore,

```math
P(H) = 0.5(1)+0.5(0) = \boxed{0.5}.
```

Using the state price approach,

```math
P(H) = \pi_UH_U+\pi_DH_D
```

gives

```math
P(H) = 0.5(1)+0.5(0) = \boxed{0.5}.
```

So the risk-neutral probability method and the state price method give exactly the same price, as they should.

# Advanced Exercise 1

**Question.** Derive price bounds for a contingent claim in an incomplete market.

**Answer.**

For the incomplete-market example, consider three states and only two traded assets.

The risk-free asset has

```math
B_0=1
```

and payoff

```math
B_1=(1,1,1).
```

The risky asset has

```math
S_0=1
```

and payoff

```math
S_1=(0.5,1,1.5).
```

Since there are only two independent traded payoff vectors in a three-dimensional state space, the market is incomplete.

Let

```math
\pi=(\pi_1,\pi_2,\pi_3)
```

be a state price vector.

Pricing the bond gives

```math
\pi_1+\pi_2+\pi_3=1.
```

Pricing the risky asset gives

```math
0.5\pi_1+\pi_2+1.5\pi_3=1.
```

Subtracting the first equation from the second gives

```math
-0.5\pi_1+0.5\pi_3=0,
```

so

```math
\pi_1=\pi_3.
```

Let

```math
\pi_1=\pi_3=t.
```

Then

```math
\pi_2=1-2t.
```

For all state prices to remain strictly positive,

```math
t>0
```

and

```math
1-2t>0.
```

Therefore,

```math
0<t<\frac12.
```

So there is an entire family of admissible state price vectors

```math
\boxed{
\pi(t)=(t,1-2t,t),
\qquad
0<t<\frac12.
}
```

Now consider a contingent claim

```math
H=(1,0,0).
```

Its price under a particular state price vector is

```math
P(H)=\pi_1=t.
```

Therefore,

```math
0<P(H)<\frac12.
```

The upper bound can also be seen directly through superhedging. Consider a portfolio containing $`1.5`$ units of the bond and $`-1`$ unit of the risky asset.

Its initial cost is

```math
1.5-1=0.5.
```

Its payoff is

```math
(1.5,1.5,1.5)-(0.5,1,1.5)=(1,0.5,0).
```

This dominates

```math
H=(1,0,0).
```

If the claim were priced at

```math
P(H)=0.5,
```

I could buy this superhedging portfolio and short the claim at zero net initial cost. The resulting payoff would be

```math
(1,0.5,0)-(1,0,0)=(0,0.5,0),
```

which is nonnegative in every state and strictly positive in one state. That is an arbitrage.

At the lower endpoint, if

```math
P(H)=0,
```

I could acquire the claim for zero cost and receive the nonnegative, nonzero payoff

```math
(1,0,0),
```

which is also an arbitrage.

The closure of the state-price family gives the limiting bounds

```math
0\le P(H)\le \frac12.
```

However, the endpoint state-price vectors contain zero components and are not strictly positive. If I require the extended market including $`H`$ itself to remain arbitrage-free under the strict state-price definition, both endpoints are excluded. Therefore the admissible no-arbitrage prices are

```math
\boxed{
0<P(H)<\frac12.
}
```
