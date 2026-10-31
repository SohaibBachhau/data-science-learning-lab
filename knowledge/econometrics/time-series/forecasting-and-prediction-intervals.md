# Forecasting and Prediction Intervals (Week 4)

Status: developing

## Central question

If we have observed a series up to time $t$, what should we predict for $X_{t+h}$, how do we calculate that prediction from ARMA or ARIMA models, and how uncertain is it?

**Short answer:** Under squared-error loss, predict the conditional mean. To forecast recursively, keep information already observed, replace unknown future values by their forecasts, and set future innovations to their conditional mean of zero. A prediction interval additionally describes uncertainty from future shocks.

## 1. Why define a loss function?

A forecast is a decision made before the future is known. The loss function says which mistakes matter. Let $\mathcal F_t$ denote the information available at date $t$, let $\widehat X_{t+h|t}$ be the $h$-step forecast, and let

$$
e_{t+h|t}=X_{t+h}-\widehat X_{t+h|t}
$$

be its forecast error. Squared loss $e^2$ penalizes large mistakes heavily, absolute loss $|e|$ penalizes proportionally, and quantile (pinball) loss treats errors above and below the forecast asymmetrically.

The optimal answer depends on the loss: the **conditional mean** minimizes expected squared loss; a **conditional median** minimizes expected absolute loss; a **conditional quantile** minimizes expected pinball loss. Do not say that the conditional mean is universally optimal.

## 2. Why the conditional mean minimizes MSE

Define $m_t=E(X_{t+h}\mid\mathcal F_t)$ and consider any other forecast $a_t$ based only on information at $t$. Decompose:

$$
X_{t+h}-a_t=(X_{t+h}-m_t)+(m_t-a_t).
$$

After squaring and conditioning, the cross term vanishes because

$$
E(X_{t+h}-m_t\mid\mathcal F_t)=0.
$$

Therefore,

$$
E[(X_{t+h}-a_t)^2\mid\mathcal F_t]
=
\operatorname{Var}(X_{t+h}\mid\mathcal F_t)+(m_t-a_t)^2.
$$

The first term cannot be reduced by choosing $a_t$. The second is minimized at $a_t=m_t$, so

$$
\boxed{\widehat X_{t+h|t}=E(X_{t+h}\mid\mathcal F_t).}
$$

This is a conditional result. It also explains why the conditional expectation forecast is unbiased **given the information set** under a correctly specified model.

## 3. The four recursive forecasting rules

Take a fitted causal and invertible ARMA model with zero-mean innovations $\varepsilon_t$ that are unpredictable from $\mathcal F_{t-1}$.

1. Keep past and present observed $X$ values as they are.
2. Replace future $X$ values by forecasts already computed.
3. Use innovations from the observed history (in practice, estimated innovations).
4. Replace future innovations by $E(\varepsilon_{t+j}\mid\mathcal F_t)=0$ for $j>0$.

The important distinction is **future shock = zero in the conditional forecast**, not that the shock will actually be zero. The future is uncertain, and those unobserved shocks generate forecast error.

For a one-step forecast, the innovation is the one-step forecast error under the correctly specified innovation representation:

$$
X_{t+1}-\widehat X_{t+1|t}=\varepsilon_{t+1}.
$$

## 4. Worked AR(1) example

Consider a stationary AR(1) with intercept:

$$
X_t=c+\phi X_{t-1}+\varepsilon_t,\qquad |\phi|<1,
$$

where $E(\varepsilon_t\mid\mathcal F_{t-1})=0$ and $\operatorname{Var}(\varepsilon_t)=\sigma_\varepsilon^2$. Its unconditional mean is $\mu=c/(1-\phi)$.

The one-step forecast is

$$
\widehat X_{t+1|t}=c+\phi X_t.
$$

The second-step forecast substitutes the first forecast for the not-yet-observed $X_{t+1}$:

$$
\widehat X_{t+2|t}=c+\phi\widehat X_{t+1|t}=c(1+\phi)+\phi^2X_t.
$$

More generally,

$$
\boxed{\widehat X_{t+h|t}=\mu+\phi^h(X_t-\mu).}
$$

For $\mu=10$, $\phi=0.6$ and $X_t=15$, the forecasts for $h=1,2,3$ are $13$, $11.8$, and $11.08$. They move toward the long-run mean of 10 as the horizon increases. If $\phi<0$, they can alternate above and below the mean while converging.

## 5. Worked MA(1) and ARMA(1,1) examples

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
$$

the one-step forecast is $\widehat X_{t+1|t}=\theta\varepsilon_t$; every forecast with $h\ge2$ is zero (the process mean), since the relevant shocks are still in the future.

For

$$
X_t=\phi X_{t-1}+\varepsilon_t+\theta\varepsilon_{t-1},
$$

we obtain

$$
\widehat X_{t+1|t}=\phi X_t+\theta\varepsilon_t,
$$

$$
\widehat X_{t+2|t}=\phi\widehat X_{t+1|t}.
$$

For $h\ge2$,

$$
\widehat X_{t+h|t}=\phi^{h-1}\widehat X_{t+1|t}.
$$

Here we have centered the process at zero. An intercept or nonzero mean must be handled explicitly.

## 6. Forecasting non-stationary levels

Do not assume forecasts of an integrated series return to a fixed unconditional level mean. A random walk has

$$
X_t=X_{t-1}+\varepsilon_t
\quad\Longrightarrow\quad
\widehat X_{t+h|t}=X_t.
$$

With drift $d$, $X_t=d+X_{t-1}+\varepsilon_t$ gives

$$
\widehat X_{t+h|t}=X_t+hd.
$$

For ARIMA models, first forecast the stationary differenced series $W_t=\Delta^d X_t$ using ARMA methods; then reconstruct level forecasts with the differencing identities. In the simple $d=1$ case:

$$
X_{t+h}=X_t+\sum_{j=1}^{h}W_{t+j},
$$

so

$$
\widehat X_{t+h|t}
=X_t+\sum_{j=1}^{h}\widehat W_{t+j|t}.
$$

For seasonal differences use the matching lag, for example $\Delta_{12}X_t=X_t-X_{t-12}$, and recursively reconstruct the seasonal levels.

## 7. Forecast-error variance

A point forecast hides how many future shocks may accumulate. For the AR(1) above,

$$
X_{t+h}-\widehat X_{t+h|t}
=\sum_{j=0}^{h-1}\phi^j\varepsilon_{t+h-j}.
$$

Under uncorrelated shocks with common variance,

$$
\boxed{\operatorname{Var}(e_{t+h|t})=\sigma_\varepsilon^2\sum_{j=0}^{h-1}\phi^{2j}
=\sigma_\varepsilon^2\frac{1-\phi^{2h}}{1-\phi^2}.}
$$

At $h=1$, this is $\sigma_\varepsilon^2$. As $h$ grows, the variance approaches the stationary process variance $\sigma_\varepsilon^2/(1-\phi^2)$.

For a random walk, future shocks accumulate without decay, so

$$
\operatorname{Var}(e_{t+h|t})=h\sigma_\varepsilon^2.
$$

The random walk's interval keeps widening with the horizon, unlike the stable AR(1) interval, which approaches a finite width.

## 8. Prediction intervals

If the conditional forecast-error distribution is normal with variance $v_h$ and the model parameters are treated as known, an approximate two-sided $(1-\alpha)$ prediction interval is

$$
\boxed{\widehat X_{t+h|t}\pm z_{1-\alpha/2}\sqrt{v_h}.}
$$

At 95%, $z_{0.975}\approx1.96$. For an AR(1) with $\phi=0.6$, $\sigma_\varepsilon=2$, and $h=2$:

$$
v_2=4(1+0.6^2)=5.44,\qquad \sqrt{v_2}\approx2.33.
$$

If the point forecast is $11.8$, the interval is approximately $[7.23,16.37]$.

This textbook interval accounts for **future innovation uncertainty** conditional on the fitted model. It does not automatically include parameter-estimation uncertainty, model misspecification, structural change or nonnormal tails. It is also an interval for a **future observation**, not merely a confidence interval for an estimated conditional mean.

## Common mistakes

- Confusing $X_{t+h}$ with $\widehat X_{t+h|t}$: one is random and unobserved, the other is computed at time $t$.
- Setting *observed* past shocks to zero rather than only future shocks.
- Believing zero forecasted innovation implies no forecast uncertainty.
- Expecting a random walk forecast to revert to a fixed mean.
- Using the AR(1) geometric variance formula when $|\phi|=1$ (use the random-walk result).
- Claiming normal prediction intervals are valid without discussing the distributional assumptions.

## Retrieval questions

1. Derive the conditional-mean forecasting result using the zero cross term.
2. Given $X_t=2+0.5X_{t-1}+\varepsilon_t$ and $X_t=8$, find the forecasts for $h=1,2,3$.
3. For a zero-mean MA(1), why is the two-step forecast zero but the one-step forecast generally nonzero?
4. Derive the two-step forecast variance of an AR(1).
5. Explain why forecast uncertainty differs between a stationary AR(1) and a random walk.

## Related notes

- [ARMA models](arma-models.md)
- [ARIMA models](arima-models.md)
- [Impulse responses](impulse-response-analysis.md)
- [Forecast evaluation](forecast-evaluation-and-cross-validation.md)
- [Plain-language story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 4, parts 1–3, and Week 4 lecture.
