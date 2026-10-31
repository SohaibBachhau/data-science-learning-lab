# Empirical Finance Glossary

Status: developing. Definitions are short memory cues; use the [Week 1 notes](week-01/lecture-notes.md) for assumptions and examples.

## Prices, returns and portfolios

| Term | Meaning |
| --- | --- |
| Asset price | Market value of one unit of an asset at a particular time, usually denoted $P_t$. |
| Adjusted price | Price series adjusted for relevant corporate actions such as dividends and stock splits, according to the data provider's method. |
| Simple return | Relative price change, $R_t=P_t^{adj}/P_{t-1}^{adj}-1$. |
| Gross return | $1+R_t$, the factor by which the investment value changes in one period. |
| Log return | $Y_t=\ln(1+R_t)=\ln P_t^{adj}-\ln P_{t-1}^{adj}$. |
| Compounding | Combining simple gross returns by multiplication across time. |
| Market capitalisation | Share price multiplied by the number of shares outstanding; many indices use free-float adjustments. |
| Portfolio | A collection of investments with specified weights. |
| Index | A benchmark that tracks a defined basket of assets under a weighting methodology. |
| Portfolio simple return | Weighted sum of constituent simple returns, using beginning-of-period weights. |
| Annualisation | Expressing return moments at a common time frequency, under stated assumptions. |

## Return distribution and risk

| Term | Meaning |
| --- | --- |
| Mean return | Sample average of the observed returns. |
| Volatility | Standard deviation of returns, used as a measure of return variability. |
| Percentile | Value below which a specified percentage of observations falls. |
| Volatility clustering | Periods of unusually large absolute returns tend to be followed by other periods with large absolute returns, regardless of sign. |
| Fat tails | Relatively more extreme observations than a comparable normal distribution predicts. |
| Skewness | Standardised third central moment; describes asymmetry. |
| Kurtosis | Standardised fourth central moment; normal kurtosis equals 3. |
| Excess kurtosis | Kurtosis minus 3. |
| Student-t degrees of freedom | Shape parameter $\nu$ that controls tail heaviness; not automatically sample size minus one. |
| Nonlinear dependence | In this course, dependence or correlation that can vary with the state of the market. |

## Statistical diagnostics

| Term | Meaning |
| --- | --- |
| De-meaning | Subtracting the sample mean from each observation; changes the level, not ordinary autocorrelations. |
| Autocorrelation | Correlation between a series and one of its lags. |
| ACF | Collection of autocorrelations across different lags. |
| Squared-return ACF | Autocorrelation of $y_t^2$ with its lagged values; a diagnostic for dependence in return magnitudes. |
| Ljung-Box test | Joint test for serial correlations through a specified lag; uses a sum of squared autocorrelation estimates. |
| QQ plot | Graph comparing sample quantiles with theoretical distribution quantiles. |
| Jarque-Bera test | Test of normality based on skewness and excess kurtosis. |
| Critical value | Threshold determined by the null distribution and significance level; reject when the statistic enters the rejection region. |
| Degrees of freedom | Distribution-specific count or parameter: number of tested lags for a basic Ljung-Box test, two for Jarque-Bera, and a shape parameter for Student-t. |
| Standardisation | Subtracting a mean and dividing by a standard deviation; changes location and scale, not the distribution family. |

## Easy confusions

- $\ln(R_t)$ is not a log return. The formula is $\ln(1+R_t)$.
- To get a simple return from a log return, use $e^{Y_t}-1$.
- $[\operatorname{Corr}(y_t,y_{t-1})]^2$ is generally not $\operatorname{Corr}(y_t^2,y_{t-1}^2)$.
- A zero sample mean does not imply zero autocorrelation.
- The normal critical value 1.96 is not a universal critical value for all distributions or tests.
- A fat-tailed distribution can be rescaled to share the same variance as a normal distribution while having different extreme quantiles.
