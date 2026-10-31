# Forecast Evaluation, Time-Series Cross-Validation and Diebold–Mariano (Week 5)

Status: developing

## Central question

A model may fit the past extremely well but forecast future data poorly. How do we measure forecast performance and compare competing models fairly?

## 1. Keep future observations out of the training information

Divide the series chronologically into a **training** period for estimation and a later **test** period for evaluation. Never randomly shuffle dates and give a model information from a later date when simulating an earlier forecast.

For a horizon $h$, define the out-of-sample forecast error

$$
e_{t+h|t}=X_{t+h}-\widehat X_{t+h|t},
$$

where the forecast is computed using only data available at forecast origin $t$. Make clear whether all test-set forecasts originate from one fixed date or whether the model/forecast is recursively updated as test dates arrive. These are different evaluation designs.

## 2. Forecast accuracy measures

For $N$ test forecasts indexed by $i$, with error $e_i=y_i-\widehat y_i$:

$$
\operatorname{MSE}=\frac1N\sum_{i=1}^{N}e_i^2,
$$

$$
\operatorname{RMSE}=\sqrt{\frac1N\sum_{i=1}^{N}e_i^2},
$$

$$
\operatorname{MAE}=\frac1N\sum_{i=1}^{N}|e_i|,
$$

$$
\operatorname{MAPE}=\frac{100}{N}\sum_{i=1}^{N}\left|\frac{e_i}{y_i}\right|,
$$

when all actual $y_i$ are nonzero.

MSE and RMSE punish occasional large misses heavily; RMSE shares the original data unit while MSE uses squared units. MAE is easier to interpret in the data's unit and is less affected by outliers. MAPE can be compared as a percentage, but is undefined at $y_i=0$ and unstable when $|y_i|$ is close to zero. It can be inappropriate for variables that are naturally zero or cross zero.

### Worked example

Suppose actual observations are $(10,12,15)$ and forecasts are $(11,10,14)$. Errors are $(-1,2,1)$.

$$
\operatorname{MSE}=\frac{1+4+1}{3}=2,
\qquad
\operatorname{RMSE}=\sqrt{2}\approx1.414,
$$

$$
\operatorname{MAE}=\frac{1+2+1}{3}=\frac43\approx1.333.
$$

Lower error scores are preferred **for the same targets and evaluation design**.

## 3. Time-series cross-validation

A single split is sensitive to the chosen cutoff. **Expanding-window cross-validation** repeats the train-then-forecast exercise, using increasingly long observed histories:

- Fit on $1,\ldots,T_0$; forecast $T_0+h$.
- Fit on $1,\ldots,T_0+1$; forecast $T_0+1+h$.
- Continue until the selected evaluation period ends.

For a **rolling window**, use a fixed-length most-recent history instead of all history since the start. An expanding window uses more data; a rolling window may adapt faster if older regimes have become less relevant. Either way, the training window must end **before** the forecast target and contain only data actually known at the origin.

When evaluating $h>1$, be especially careful about overlapping forecast horizons and the exact forecast origin. The error sequence can be correlated even if the underlying innovations are not.

## 4. Compare against a simple benchmark

Complicated ARIMA forecasts are not automatically better than a random-walk forecast $\widehat X_{t+h|t}=X_t$, a seasonal-naive forecast using the most recent matching season, or another sensible simple baseline. Models should be judged against a relevant baseline using the **same dates and horizons**.

An AIC comparison answers a penalized in-sample likelihood question. Time-series cross-validation answers the more direct question: *How well would the method have predicted observations that were not available yet?*

## 5. Diebold–Mariano (DM) forecast comparison

Suppose two models make forecasts for the same targets, horizon and test dates. Let

$$
d_i=L(e_{1,i})-L(e_{2,i})
$$

be the difference in forecast losses, where $L$ could be squared or absolute error.

The null is

$$
H_0:E(d_i)=0
$$

(equal expected predictive accuracy); the usual alternative is $E(d_i)\ne0$. With $N$ paired forecast errors, a common large-sample form is

$$
\boxed{\operatorname{DM}=\frac{\overline d}{\sqrt{\widehat\Omega/N}},}
$$

where $\widehat\Omega$ estimates the long-run variance of the loss-differential sequence:

$$
\Omega=\gamma_d(0)+2\sum_{j=1}^{\infty}\gamma_d(j).
$$

In practical implementations one uses a suitable truncated or heteroskedasticity/autocorrelation-consistent estimate. Overlapping $h$-step forecast errors often require accounting for serial correlation up to at least the relevant overlap lags. Under suitable conditions, DM is approximately standard normal under $H_0$.

If the test is two-sided at 5%, an asymptotic $|DM|>1.96$ suggests rejecting equal accuracy. With our sign convention:

- $\overline d>0$: model 1 has *greater* average loss and model 2 performs better in sample.
- $\overline d<0$: model 1 has *smaller* average loss.

Statistical evidence that forecasting performance differs is not the same as proof of causality or a guarantee of future superiority. Small test samples also deserve caution.

## 6. The practical decision chain

Specify sensible candidate models, compare information criteria, check residual assumptions, produce genuine out-of-sample forecasts, calculate loss measures, and only then ask whether observed differences in losses are meaningfully different from zero. The steps solve related but distinct problems.

## Common mistakes

- Reporting training-set errors as if they were out-of-sample performance.
- Using random K-fold shuffling that leaks future information.
- Comparing a 1-step forecast from one model with a 4-step forecast from another.
- Applying MAPE to zero actual values.
- Interpreting a lower RMSE by itself as a formal statistical rejection of equal accuracy.
- Forgetting that the sign of a DM loss differential depends on the order of subtraction.

## Retrieval questions

1. Compute MSE, RMSE and MAE for forecast errors $(2,-1,-3)$.
2. Explain expanding versus rolling time-series cross-validation.
3. Why is shuffled cross-validation usually inappropriate for forecasting?
4. What is the null hypothesis of DM? What does a negative $\overline d$ mean with $d=L_1-L_2$?
5. Explain why an in-sample AIC winner need not be the out-of-sample RMSE winner.

## Related notes

- [Forecasting and intervals](forecasting-and-prediction-intervals.md)
- [Model selection and diagnostics](model-selection-and-diagnostics.md)
- [Story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 5, parts 3–4 and Week 5 lecture.
