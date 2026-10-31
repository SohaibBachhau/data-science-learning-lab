# Week 1 Lecture Notes: Return Characteristics

Status: developing  
Course source: Natalie Kessler, *Empirical Finance*, Module 1, VU Amsterdam, 2026 (slides 14-64).

These notes are our explanation of the lecture content, not a copy of the slides. Concepts already covered in the permanent time-series branch are linked rather than rewritten in full.

## 1. Prices and adjusted prices (slides 14-15)

Financial datasets distinguish open, high, low, close and adjusted close. Returns should be calculated from a price series appropriate for the investment question. Dividends and stock splits can make a price-only index differ substantially from a total-return index. The exact meaning of adjusted prices depends on the data vendor.

Let $P_t^{adj}>0$ denote a consistently adjusted asset price at time $t$.

The one-period simple net return is

$$
R_t = \frac{P_t^{adj}-P_{t-1}^{adj}}{P_{t-1}^{adj}}
= \frac{P_t^{adj}}{P_{t-1}^{adj}}-1.
$$

Its gross counterpart is $1+R_t$. For $n$ periods, the gross factors **multiply**:

$$
R_t(n)=\prod_{j=0}^{n-1}(1+R_{t-j})-1.
$$

The product starts with $j=0$, meaning zero periods back from $t$, not necessarily calendar day zero. The final minus one is outside the product. A +10% move followed by a -10% move gives $1.10(0.90)-1=-1\%$, not zero.

## 2. Log returns (slides 16-19)

Define the continuously compounded or log return by

$$
Y_t=\ln(1+R_t)
=\ln P_t^{adj}-\ln P_{t-1}^{adj}.
$$

The inverse transformation is $R_t=e^{Y_t}-1$. Be careful: it is $\ln(1+R_t)$, **not** $\ln R_t$.

Log returns add over time because intermediate log prices cancel:

$$
Y_t(n)=\sum_{j=0}^{n-1}Y_{t-j}
=\ln P_t^{adj}-\ln P_{t-n}^{adj}.
$$

Simple and log returns are close for small $R_t$ since $\ln(1+R_t)\approx R_t$. Their differences become important for large returns. Log returns are symmetric under reversing a price ratio: moving from 100 to 120 has log return $\ln(1.2)$; reversing the move has exactly $-\ln(1.2)$. Corresponding simple returns are +20% and -16.67%.

A total log return of 0.04 corresponds to a simple return of $e^{0.04}-1\approx4.081\%$.

## 3. Portfolio and index returns (slides 20-23)

For $K$ assets with weights $w_{t-1,k}$ set at the start of the period and summing to one, a portfolio's simple return is

$$
R_{t,p}=\sum_{k=1}^{K}w_{t-1,k}R_{t,k}.
$$

There is no corresponding exact weighted-average identity for individual log returns: the logarithm of a sum is not the sum of logarithms.

Market capitalisation is share price times outstanding shares. An index such as the S&P 500 uses a free-float-adjusted market-capitalisation methodology to determine constituent weights. An index is a benchmark; a portfolio is a set of actual or hypothetical holdings. A portfolio can be designed to track an index.

The lecture contrasts the S&P 500 price index with the corresponding return series. Price levels and fluctuations in returns answer different questions.

## 4. Descriptive return characteristics (slides 28-31)

Given observed returns $y_1,\ldots,y_T$, the sample mean and standard deviation are

$$
\bar y=\frac1T\sum_{t=1}^{T}y_t,\qquad
s=\sqrt{\frac1{T-1}\sum_{t=1}^{T}(y_t-\bar y)^2}.
$$

In finance, $s$ is often called realised sample volatility. A percentile is the value below which a stated percentage of observations lies. Lower percentiles are useful for thinking about unusually bad outcomes.

For the lecture's daily S&P 500 total-return log-return sample (2000 to mid-2026), the mean is approximately 0.000316, the standard deviation 0.012162, and the minimum and maximum roughly -0.127605 and 0.109582. The mean is tiny relative to the standard deviation.

Using the conventional approximations of 21 trading days per month and 252 per year, the lecture annualises log-return mean by multiplication and volatility by a square root:

$$
\mu_{\text{annual, log}}\approx252\mu_{\text{daily, log}},\qquad
\sigma_{\text{annual}}\approx\sqrt{252}\,\sigma_{\text{daily}}.
$$

The square-root-of-time rule comes from **variance additivity** when returns over the relevant periods are uncorrelated and have stable variances. It is not automatically exact in the presence of serial dependence or changing volatility. For a constant daily simple growth rate $r$, an annual compound rate is $(1+r)^{252}-1$.

## 5. Three stylised facts (slides 32-34 and 44-63)

1. **Volatility clustering:** Large changes in either direction tend to be near other large changes; quiet periods tend to cluster too.
2. **Fat tails:** Extreme returns occur more often than a comparable normal distribution would predict.
3. **Nonlinear or state-dependent dependence:** Correlation between assets can change with market conditions.

These observations motivate models of financial risk rather than relying solely on a constant mean, variance and correlation matrix.

## 6. Autocorrelation, de-meaning and squared returns (slides 35-38)

For a return series $y_t$, lag-$k$ autocorrelation is $\rho_y(k)=\operatorname{Corr}(y_t,y_{t-k})$. The ACF is the collection of autocorrelations over lags. A sample autocorrelation outside the approximate white-noise 95% bands

$$
\pm \frac{1.96}{\sqrt{T}}
$$

suggests serial correlation, under the assumptions that justify these bands. Significance does not automatically imply economically useful predictability.

De-meaning a series, $\tilde y_t=y_t-\bar y$, gives sample mean zero but leaves its ordinary autocorrelations unchanged: correlation is invariant to subtracting constants. Zero mean is not the same as zero serial correlation.

Volatility clustering is often investigated using squared returns. This involves the **ACF of the squared series**,

$$
\rho_{y^2}(k)=\operatorname{Corr}(y_t^2,y_{t-k}^2).
$$

Do not confuse this with squaring the autocorrelation of the original series. In general,

$$
[\rho_y(k)]^2 \ne \rho_{y^2}(k).
$$

Both ACFs are useful, but they answer different questions: dependence in returns versus dependence in return magnitudes.

## 7. Ljung-Box test (slides 39-43)

For a chosen input series and the first $m$ lags, the Ljung-Box statistic is

$$
Q(m)=T(T+2)\sum_{k=1}^{m}\frac{\hat\rho(k)^2}{T-k}.
$$

The null hypothesis is $\rho(1)=\cdots=\rho(m)=0$ and the alternative is that at least one tested autocorrelation differs from zero. Under the usual null conditions and large-sample approximation, $Q(m)$ has a $\chi^2(m)$ reference distribution for a raw series. Estimated-model residual tests may need degrees-of-freedom adjustment.

Because the statistic squares autocorrelations, both negative and positive correlations contribute positively. The rejection region is in the **upper tail**, not both tails. For $m=10$, the 5% upper critical value is about 18.31.

The lecture's ten-lag statistics are approximately 96.41 for returns and 6074.87 for squared returns. Both reject at 5%, with much stronger evidence of dependence in squared returns. This does not by itself quantify forecast accuracy.

Apply the test to $y_t$ to investigate return autocorrelation, or to $y_t^2$ to investigate autocorrelation in squared returns.

## 8. Skewness, kurtosis and fat tails (slides 45-48)

For a random variable $X$ with mean $\mu$ and positive standard deviation $\sigma$, population skewness and kurtosis are

$$
S=E\left[\left(\frac{X-\mu}{\sigma}\right)^3\right],\qquad
K=E\left[\left(\frac{X-\mu}{\sigma}\right)^4\right].
$$

A normal distribution has skewness zero and kurtosis 3. Excess kurtosis is $K-3$. Negative skewness signals a more pronounced left tail; positive skewness signals a more pronounced right tail. Kurtosis is particularly sensitive to extreme deviations.

Two distributions can share a mean and variance but differ in their higher moments and tail probabilities. For example, a Student-t random variable with $\nu>2$ has variance $\nu/(\nu-2)$; rescaling by $\sqrt{(\nu-2)/\nu}$ gives unit variance without making its shape normal. Small Student-t degrees-of-freedom parameter $\nu$ means heavier tails; as $\nu$ grows, the distribution approaches the normal.

Be careful with 1.96: it is a normal critical quantile, not a universal multiple of the standard error for all distributions. The standard deviation describes observations; the standard error describes an estimator.

## 9. Jarque-Bera test (slide 49)

Normality implies skewness zero and kurtosis three. With sample estimates $S$ and $K$, the Jarque-Bera statistic is

$$
JB=\frac{T}{6}S^2+\frac{T}{24}(K-3)^2.
$$

Under an iid normal null and suitable large-sample conditions, standardised sample skewness and excess kurtosis are approximately independent standard normals. Their squared sum produces the $\chi^2(2)$ reference distribution. At 5%, the upper critical value is about 5.99.

A large statistic rejects normality. It does **not** prove that fat tails alone caused rejection, since skewness can also be involved. The lecture's S&P 500 statistic is over 31,000, far beyond 5.99.

## 10. QQ plots (slides 50-55)

A quantile is a cutoff corresponding to a probability. A QQ plot places theoretical quantiles (for example, standard normal) on the horizontal axis and observed sample quantiles on the vertical axis. Standardise returns by $(y_t-\bar y)/s$ when comparing them with the standard normal.

- Roughly along the reference line: sample distribution resembles the reference.
- Fat tails relative to normal: low observed quantiles below the line, high observed quantiles above it.
- Thin tails: low end above the line and high end below it.
- Upward curvature can indicate right skew; downward curvature can indicate left skew.

Comparing against appropriately scaled Student-t quantiles can reveal whether a heavier-tailed reference better matches the observed extremes. QQ plots complement rather than replace formal normality tests.

## 11. Nonlinear dependence and diversification (slides 60-63)

Correlation is a linear measure. A constant unconditional correlation can conceal differences across market states. For example, two stocks may move relatively independently during calm markets but together during crisis periods.

This matters because increasing correlation in a downturn can reduce diversification exactly when it is most needed. The lecture plots changing quarterly Apple-Microsoft correlations to illustrate variation over time. Changing estimated correlation alone does not prove a specific causal explanation or nonlinear model.

## Sources and connections

- Natalie Kessler, *Empirical Finance*, Module 1 lecture slides, VU Amsterdam, 2026.
- [Time-series ACF and lag selection](../../../knowledge/econometrics/time-series/acf-pacf-and-lag-order-selection.md).
- [Time-series basic properties](../../../knowledge/econometrics/time-series/basic-properties.md).
- [Maximum likelihood branch](../../../knowledge/econometrics/maximum-likelihood/README.md).
- [Week 1 tutorial plan](tutorial-plan.md).

## Review log

- 2026-10-31: Initial organised lecture notes created from our teaching session. R tutorial remains pending.
