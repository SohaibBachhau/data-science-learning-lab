# Model Selection and Residual Diagnostics (Week 5)

Status: developing

## Central question

Many ARMA or ARIMA models can fit the same observed data. How do we select a useful model without overfitting, and how do we check whether it has left predictable patterns behind?

## 1. Fit is not the whole objective

Adding parameters normally improves in-sample fit, even when the added lag does not capture a real relationship. An excessively complicated model can memorize noise; an oversimplified model can leave genuine dependence unexplained. Model selection balances fit and complexity.

ACF and PACF patterns help suggest plausible **candidate lag orders**. Then estimate several plausible models, compare information criteria, and reject candidates whose residuals reveal a serious failure. An information criterion is not a proof that the chosen model is correct.

## 2. Information criteria

Let $\ell(\widehat\vartheta)$ be the maximized log-likelihood, $k$ the total number of estimated parameters counted by the chosen software convention, and $n$ the sample size.

The usual definitions are

$$
\boxed{\operatorname{AIC}=-2\ell(\widehat\vartheta)+2k,}
$$

$$
\boxed{\operatorname{BIC}=-2\ell(\widehat\vartheta)+k\ln n,}
$$

$$
\operatorname{HQIC}=-2\ell(\widehat\vartheta)+2k\ln(\ln n),
$$

and one common small-sample correction is

$$
\operatorname{AICc}=\operatorname{AIC}+\frac{2k(k+1)}{n-k-1},
\qquad n>k+1.
$$

**Lower is preferred**, provided the models are evaluated on comparable data using compatible likelihood definitions. Do not compare IC values computed from different samples or incompatible response transformations as though they were automatically on the same scale.

AIC uses a fixed $2k$ penalty and is often oriented toward predictive fit. BIC uses a $k\ln n$ penalty, which becomes stronger with larger $n$; in appropriate settings it can consistently select the true finite-dimensional model if it is among the candidates. AICc makes a stronger correction when sample size is small. These are tendencies, not guarantees that AIC always forecasts best or BIC always explains best.

### Worked selection example

Suppose two models share $n=100$ observations. Model A has $\ell=-120$ and $k=3$; Model B has $\ell=-117$ and $k=6$.

$$
\operatorname{AIC}_A=240+6=246,
\qquad
\operatorname{AIC}_B=234+12=246.
$$

AIC ties them. For BIC:

$$
\operatorname{BIC}_A=240+3\ln100\approx253.82,
$$

$$
\operatorname{BIC}_B=234+6\ln100\approx261.63.
$$

BIC prefers A because B's extra improvement in fit does not compensate for the stronger complexity penalty.

## 3. What model residuals should look like

If the fitted model successfully explains the **linear time dependence**, the innovations should contain no remaining linear autocorrelation. Plot the residual series and sample ACF. Also inspect a histogram and QQ plot if a normal innovation distribution was assumed.

Two separate questions matter:

- **Autocorrelation:** is predictable linear dependence still present?
- **Normality:** does the distribution look compatible with normal innovations?

A process can be uncorrelated yet nonnormal. Passing a normality check does not prove that residuals are serially independent. Likewise, no autocorrelation alone does not rule out nonlinear dependence such as volatility clustering.

## 4. Ljung–Box test

This is a joint check of residual autocorrelations up to a selected lag $m$. The hypotheses are:

$$
H_0:\rho(1)=\cdots=\rho(m)=0,
$$

against the alternative that at least one of them is nonzero. With residual sample autocorrelations $\widehat\rho(h)$ and sample size $n$,

$$
Q=n(n+2)\sum_{h=1}^{m}\frac{\widehat\rho(h)^2}{n-h}.
$$

For raw white noise and suitable regularity, compare $Q$ to an approximate chi-squared reference with $m$ degrees of freedom. For fitted ARMA residuals, software may adjust the degrees of freedom, often using $m-p-q$ when positive; its assumptions and exact convention should be checked.

- Small p-value: evidence of remaining autocorrelation, so review the model.
- Large p-value: insufficient evidence of autocorrelation, **not proof** of independence or model correctness.

The point of a joint test is that checking many individual ACF bars creates a multiple-testing problem.

## 5. Jarque–Bera test

This checks whether sample skewness and kurtosis are compatible with a normal distribution. With sample skewness $S$ and ordinary (not excess) kurtosis $K$,

$$
\operatorname{JB}=\frac{n}{6}\left[S^2+\frac{(K-3)^2}{4}\right].
$$

Under normality and usual regularity conditions the statistic is asymptotically $\chi^2_2$.

- $H_0$: normality.
- Small p-value: evidence against normality.
- Large p-value: no compelling evidence against normality, not proof of it.

Nonnormal innovations can matter particularly for **normal-theory prediction intervals** and exact Gaussian likelihood interpretation. Some estimators can still be useful without exact normality; do not conclude that every model is unusable after a JB rejection.

## 6. A complete selection workflow

1. Identify whether the level is stationary; consider transformations, ADF/KPSS and seasonal patterns.
2. Find a plausible differencing order without overdifferencing.
3. Inspect ACF/PACF and propose several ARMA, ARIMA or SARIMA candidate orders.
4. Estimate the candidates on a comparable sample.
5. Compare AIC/AICc/BIC/HQIC, remembering the tradeoffs.
6. Examine residual time plots, ACF and Ljung–Box; check distributional assumptions with QQ plots/JB if relevant.
7. Compare **out-of-sample** forecast performance for forecasting applications.
8. Reconsider transformations, lag orders or model class if diagnostics fail.

## Common mistakes

- Choosing the lowest AIC while ignoring substantial residual autocorrelation.
- Treating a large p-value as proof of a true null.
- Mixing up the nulls: Ljung–Box tests **no autocorrelation**, while Jarque–Bera tests **normality**.
- Believing visually significant residual ACF spikes always imply a joint rejection.
- Comparing AIC across models estimated on non-comparable target variables or data samples.

## Retrieval questions

1. Compute AIC and BIC for $\ell=-80$, $k=4$, $n=100$.
2. Why does merely minimizing residual sum of squares favor excessive complexity?
3. What does a Ljung–Box p-value of 0.01 imply at the 5% level?
4. What is tested by Jarque–Bera, and what does a non-rejection not establish?
5. State a defensible order of operations from plotting the series to final model choice.

## Related notes

- [ACF/PACF and lag order](acf-pacf-and-lag-order-selection.md)
- [Maximum likelihood and parameter estimation](parameter-estimation.md)
- [Forecast evaluation](forecast-evaluation-and-cross-validation.md)
- [Story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 5, parts 1–2 and Week 5 lecture.
