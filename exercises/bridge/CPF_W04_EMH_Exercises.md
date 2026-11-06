# Week 4 Bridge — Efficient Markets Hypothesis Exercises

## Review Question 1

**Question.** State the EMH in conditional expectation form and explain its meaning.

**Answer.**

The EMH can be written in conditional expectation form as

```math
E[r_{t+1}\mid\mathcal I_t]=\mu_t.
```

Here, $`\mathcal I_t`$ represents the information available at time $`t`$.

What this means to me is that once the information currently available to the market has been taken into account, there should not be a remaining predictable abnormal component in the next return. It does not mean that returns have to be zero. It means that available information should not consistently give me an advantage in predicting future abnormal returns.

## Review Question 2

**Question.** Describe the difference between weak-form and semi-strong-form efficiency.

**Answer.**

Weak-form efficiency says that current prices already reflect the information contained in past prices and returns. If weak-form efficiency holds, I should not be able to consistently earn excess returns simply by studying historical price patterns.

Semi-strong-form efficiency makes a stronger claim. It says prices incorporate all publicly available information, including earnings announcements, interest rates, economic releases, and other public news.

So the main difference is the information set. Weak form focuses on past market data, while semi-strong form includes all public information.

## Review Question 3

**Question.** Explain why predictable returns can be interpreted as a market inefficiency.

**Answer.**

Predictable returns can be interpreted as evidence against market efficiency because, if information that was already available allows me to systematically forecast future abnormal returns, then that information does not appear to have been fully incorporated into prices.

I would not automatically call every statistically significant pattern a market inefficiency, though. The effect could be small, unstable, compensation for risk, or disappear once transaction costs are included. I would want to see whether the predictability survives out of sample and whether it has actual economic value.

## Review Question 4

**Question.** Summarize the role of information sets in defining efficiency.

**Answer.**

The information set determines what kind of efficiency I am testing.

Under weak-form efficiency, the relevant information consists mainly of past prices and returns. Under semi-strong efficiency, the information set expands to all publicly available information.

This matters because I can only call something predictable relative to information that was actually available at the time. Using information that became available later would introduce lookahead bias and would not be a valid test of efficiency.

## Review Question 5

**Question.** Describe one common empirical test of the EMH and its intuition.

**Answer.**

One common empirical test of the EMH is autocorrelation.

For lag one,

```math
\rho_1=\operatorname{Corr}(r_t,r_{t-1}).
```

If past returns contain no useful linear information about future returns, I would expect this value to be close to zero.

Positive autocorrelation would indicate some short-run continuation, while negative autocorrelation would indicate some short-run reversal. A value close to zero would be more consistent with weak-form efficiency.

I would still distinguish statistical dependence from exploitable predictability because even a statistically detectable relationship may be too small or unstable to trade profitably.

# Exercises

## Exercise 1

**Question.** Using a return series, compute the autocorrelation at lag one and interpret whether it is consistent with weak-form efficiency.

**Answer.**

For the SPY series, I calculate the lag-one autocorrelation with

```python
acf_1 = returns.autocorr(lag=1)
print(acf_1)
```

The value is approximately

```math
\boxed{\rho_1\approx -0.133}.
```

The negative lag-one autocorrelation indicates some short-run reversal and therefore represents evidence against a strict weak-form benchmark of zero linear predictability at lag one. However, the autocorrelation result alone does not establish an economically exploitable inefficiency. I would still need to test whether the relationship is statistically reliable, stable out of sample, and strong enough to survive trading costs.

## Exercise 2

**Question.** Construct a simple regression of returns on a lagged signal and explain how to interpret the slope coefficient under the EMH.

**Answer.**

The one-lag regression is

```math
r_t=\alpha+\beta r_{t-1}+\varepsilon_t.
```

The notebook gives

```text
coef_lag_1 = -0.132945
p_lag_1    =  0.029434
r2         =  0.017671
```

So the estimated lag coefficient is

```math
\boxed{\beta=-0.132945}.
```

Because the coefficient is negative, the regression indicates short-run reversal rather than continuation.

The p-value is

```math
\boxed{0.029434},
```

which is below $`0.05`$. Therefore, the lag-one coefficient is statistically significant at the 5% level.

However,

```math
R^2=0.017671,
```

so the previous day's return explains only about **1.77%** of the variation in the current day's return.

My interpretation is that there is statistically detectable lag-one predictability in this sample, but its explanatory power is very small. Statistical significance therefore does not automatically imply useful trading predictability.

## Exercise 3

**Question.** Compute a variance ratio for a chosen horizon and interpret its meaning in the context of random walk behavior.

**Answer.**

I use

```math
q=5.
```

The notebook gives

```math
\boxed{VR(5)=0.860920}.
```

Under the random-walk benchmark,

```math
VR(5)=1.
```

Because

```math
0.860920<1,
```

the five-day variance is lower than what the simple random-walk benchmark would imply. This is consistent with some degree of mean-reverting or negatively serially correlated behavior.

The other variance ratios tell a similar story at shorter horizons:

```math
VR(2)=0.884876,
```

```math
VR(10)=0.832372,
```

while

```math
VR(20)=0.981283
```

moves much closer to one.

So the evidence of mean reversion is stronger at the shorter horizons and becomes much weaker by the 20-day horizon.

## Exercise 4

**Question.** Identify a publicly available macro variable and outline a test of whether it predicts equity index returns.

**Answer.**

I would use the **10-year Treasury yield** as the publicly available macro variable.

I would test whether the yield, or possibly the change in the yield, contains information about future SPY returns.

The return I would try to predict would be the next-period SPY return. The timing is important, so I would only use Treasury information that was actually available before the SPY return being predicted.

A simple regression would be

```math
r_{t+1}^{SPY}=\alpha+\beta y_t+\varepsilon_{t+1},
```

where $`y_t`$ is the Treasury yield observed at time $`t`$.

I would test

```math
H_0:\beta=0.
```

A statistically significant coefficient would indicate that the macro variable contains predictive information about future SPY returns. I would then want to test the relationship out of sample because an in-sample significant coefficient alone would not establish durable predictability.

## Exercise 5

**Question.** Compare the out-of-sample performance of a naive strategy and a buy-and-hold benchmark and discuss which result is more consistent with the EMH.

**Answer.**

The official SPY AR(1) out-of-sample strategy produced

```text
hit_rate  =  0.500000
gross_pnl = -0.342127
net_pnl   = -0.791527
```

The hit rate is exactly

```math
50\%.
```

So the strategy did no better than chance in predicting the direction of SPY returns.

Its cumulative gross PnL was

```math
-0.342127,
```

and its cumulative net PnL after trading costs was

```math
-0.791527.
```

For a fair comparison, I calculate the SPY buy-and-hold return over exactly the same out-of-sample evaluation window used by the AR(1) helper. Since the helper uses the first 252 observations as its rolling estimation window and begins evaluating the next realized return, the comparable buy-and-hold series begins at

```python
returns.iloc[253:]
```

The calculation is

```python
window = 252

oos_buy_hold = returns.iloc[window + 1:]

buy_hold_log_return = oos_buy_hold.sum()
buy_hold_simple_return = np.exp(buy_hold_log_return) - 1

print("Buy-and-hold log return:", buy_hold_log_return)
print("Buy-and-hold simple return:", buy_hold_simple_return)
```

which gives

```text
Buy-and-hold log return: 1.246002
Buy-and-hold simple return: 2.476417
```

So SPY buy-and-hold earned a cumulative simple return of approximately

```math
\boxed{247.64\%}.
```

Over the same out-of-sample period, buy-and-hold produced a strongly positive cumulative return, while the AR(1) strategy produced negative gross and net PnL.

The AR(1) strategy therefore clearly underperformed buy-and-hold. Its 50% hit rate also shows that it had no useful directional forecasting advantage out of sample.

This result is more consistent with the EMH than with the idea that the lag-one relationship represents an easily exploitable inefficiency. The in-sample regression showed statistically significant short-run reversal, but that statistical relationship did not translate into profitable out-of-sample trading performance.
