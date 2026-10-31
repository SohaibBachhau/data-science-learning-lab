# Weeks 4–6: Integrated Exam Review and Practice

Status: developing

This checkpoint links the three final course themes: forecasting and responses to shocks (Week 4), selecting/checking/evaluating models (Week 5), and relationships between multiple non-stationary series (Week 6).

It is a **study aid** rather than a copy of the VU preparation exam or its solutions. Try each problem before opening the worked answer. Explanations distinguish the mathematical result from the assumption making it valid.

## The big storyline

1. **Week 1:** identify the basic statistical structure of data observed in time.
2. **Week 2:** explain stationary dynamics using AR, MA and ARMA models.
3. **Week 3:** handle trends, unit roots and seasonality through integration, tests, ARIMA and SARIMA.
4. **Week 4:** turn a model into point forecasts, forecast intervals and shock-response paths.
5. **Week 5:** compare candidates, detect misspecification and evaluate unseen predictions.
6. **Week 6:** avoid false relationships between wandering series; use cointegration and ECM where a stable long-run relation exists.

## Core results to be able to derive

### Optimal forecast

For $\mathcal F_t$-measurable $a_t$ and $m_t=E(X_{t+h}\mid\mathcal F_t)$,

$$
E[(X_{t+h}-a_t)^2\mid\mathcal F_t]
=
\operatorname{Var}(X_{t+h}\mid\mathcal F_t)+(m_t-a_t)^2.
$$

Consequently, $a_t=m_t$ minimizes conditional MSE.

### Stationary AR(1)

For $X_t=c+\phi X_{t-1}+\varepsilon_t$ with $|\phi|<1$,

$$
\mu=\frac{c}{1-\phi},
\qquad
\widehat X_{t+h|t}=\mu+\phi^h(X_t-\mu),
$$

$$
v_h=\sigma_\varepsilon^2\sum_{j=0}^{h-1}\phi^{2j}.
$$

The IRF at horizon $h$ is $\phi^h$ per unit shock.

### Random walk

For $X_t=X_{t-1}+\varepsilon_t$,

$$
\widehat X_{t+h|t}=X_t,
\qquad
v_h=h\sigma_\varepsilon^2.
$$

The level IRF is 1 at every horizon, while the differenced-series IRF is 0 after the impact period.

### Selection and testing

$$
\operatorname{AIC}=-2\ell+2k,\qquad
\operatorname{BIC}=-2\ell+k\ln n.
$$

**Nulls worth memorizing:**

| Test | Null hypothesis |
|---|---|
| ADF | Unit root (with specification-dependent deterministic terms) |
| KPSS | Stationarity around the specified level/trend |
| Ljung–Box | No autocorrelation through selected lag |
| Jarque–Bera | Normality |
| Diebold–Mariano | Equal expected forecast loss |
| Engle–Granger | No cointegration |
| Granger causality test $X\to Y$ | Lagged $X$ terms have no incremental predictive power for $Y$ |

## Problem 1: Forecasts and uncertainty

At time $t$, $X_t=14$ and

$$
X_s=2+0.5X_{s-1}+\varepsilon_s,\quad
E(\varepsilon_s)=0,\quad
\operatorname{Var}(\varepsilon_s)=4.
$$

Assume the innovations are uncorrelated with the past and $|\phi|<1$.

**Tasks:**

1. Find the unconditional mean.
2. Compute $\widehat X_{t+1|t}$ and $\widehat X_{t+2|t}$.
3. Compute the conditional variance of the 2-step forecast error.
4. Give an approximate 95% normal prediction interval for $X_{t+2}$ under Gaussian innovations and known parameters.

<details>
<summary>Worked answer</summary>

The mean is $\mu=2/(1-0.5)=4$. Forecast 1: $2+0.5(14)=9$. Forecast 2: $2+0.5(9)=6.5$. The forecast error combines $\varepsilon_{t+2}+0.5\varepsilon_{t+1}$, so its variance is $4(1+0.5^2)=5$. The normal interval is $6.5\pm1.96\sqrt5\approx[2.12,10.88]$.

</details>

## Problem 2: Impulse responses

For a zero-mean ARMA(1,1),

$$
(1-0.4L)X_t=(1+0.3L)\varepsilon_t,
$$

**Tasks:**

1. Find the IRF for horizons $h=0,1,2,3$.
2. State whether the effect disappears exactly after a finite horizon.
3. Distinguish this from an MA(1).

<details>
<summary>Worked answer</summary>

The MA-infinity coefficients are $\psi_0=1$ and $\psi_h=(0.4+0.3)(0.4)^{h-1}$ for $h\ge1$. Thus the values are $1,0.7,0.28,0.112$. The response keeps decaying rather than becoming exactly zero at a finite horizon. For an MA(1), the impact is zero at all horizons $h\ge2$.

</details>

## Problem 3: Choose a model, then test it

On the same sample of $n=100$, model A has maximized log-likelihood $-100$ and $k=3$ parameters; model B has log-likelihood $-97$ and $k=6$. Model B's Ljung–Box p-value is $0.01$ at the chosen residual lag.

**Tasks:**

1. Calculate both AIC values.
2. Calculate both BIC values.
3. At 5%, would a residual diagnostic challenge model B?

<details>
<summary>Worked answer</summary>

AIC(A) $=200+6=206$; AIC(B) $=194+12=206$, a tie. BIC(A) $=200+3\ln100\approx213.82$; BIC(B) $=194+6\ln100\approx221.63$, so BIC prefers A. With a Ljung–Box p-value of $0.01$, reject the null of no residual autocorrelation at 5%. Model B's remaining serial dependence warrants review, irrespective of the AIC tie.

</details>

## Problem 4: Forecast comparison

Two methods forecast the same test dates. Their squared errors are:

- Model A: $(1,4,9)$.
- Model B: $(4,4,4)$.

**Tasks:**

1. Calculate each model's MSE and RMSE.
2. Calculate the observed average squared-loss difference $\overline d$ for $d=L_A-L_B$.
3. Can you determine the statistical significance of the difference from these averages alone?

<details>
<summary>Worked answer</summary>

MSE(A) $=14/3\approx4.667$ and RMSE(A) $\approx2.160$. MSE(B) $=4$ and RMSE(B) $=2$. The observed average loss difference is $(1-4+4-4+9-4)/3=2/3>0$, favoring B. This is **not** enough to conduct a DM significance test: we need an appropriate estimate of the loss-differential variance (and with only three forecasts, asymptotic inference would be precarious).

</details>

## Problem 5: Cointegration and adjustment

Let $S_t$ be an $I(1)$ random walk and $u_t,v_t$ jointly stationary. Define

$$
X_t=S_t+u_t,\qquad Y_t=2S_t+v_t.
$$

**Tasks:**

1. Find a stationary linear combination of $X_t$ and $Y_t$.
2. If the cointegrating error is $z_t=Y_t-2X_t$, write a simple ECM with adjustment $\lambda=-0.3$.
3. Explain the sign when $z_{t-1}=5$ and all other dynamic terms are zero.

<details>
<summary>Worked answer</summary>

$Y_t-2X_t=v_t-2u_t$ is stationary. A simple ECM is $\Delta Y_t=c-0.3z_{t-1}+\gamma\Delta X_t+e_t$. With the other contributions set to zero, the adjustment is $-1.5$, pushing $Y_t$ down toward its long-run relation with $X_t$.

</details>

## Problem 6: Explain rather than calculate

Answer each in no more than three sentences:

1. Why is fitting levels of independent random walks dangerous?
2. Why can differencing alone remove useful long-run information?
3. Why does the Engle–Granger residual test need special critical values?
4. Why is Granger causality not evidence of an economic intervention effect?
5. Why can good in-sample fit coexist with poor forecasts?

<details>
<summary>Answer check</summary>

1. Wandering trends can align by chance and invalidate conventional stationary regression inference.
2. Differences focus on short-run movements; a stable level spread or equilibrium relation can disappear from the model.
3. The residuals were constructed using estimated regression coefficients, changing the null distribution relative to an ordinary ADF test.
4. It measures improvement in prediction from earlier values and may reflect confounding or common information.
5. A model can fit noise or the training period's quirks rather than repeatable dynamics.

</details>

## Personal retrieval checklist

Can you do the following without opening a note?

- [ ] Explain *why* the conditional mean is MSE-optimal, not just quote the theorem.
- [ ] Forecast 1, 2, and 3 steps recursively for AR, MA, ARMA and basic ARIMA.
- [ ] Compute forecast-error variance and a conditional normal prediction interval.
- [ ] Calculate an ARMA impulse response and explain a persistent unit-root level shock.
- [ ] Calculate AIC/BIC and distinguish Ljung–Box from Jarque–Bera.
- [ ] Compare RMSE/MAE and design a chronological evaluation.
- [ ] State the Diebold–Mariano null and interpret a loss differential sign.
- [ ] Explain spurious regression, cointegration and an Engle–Granger residual check.
- [ ] Interpret the error-correction coefficient and its sign convention.
- [ ] Distinguish three meanings of "causality": ARMA, Granger, structural.

## Study path

- [Week 4: forecasting and prediction intervals](forecasting-and-prediction-intervals.md)
- [Week 4: impulse responses](impulse-response-analysis.md)
- [Week 5: model selection and diagnostics](model-selection-and-diagnostics.md)
- [Week 5: out-of-sample forecast evaluation](forecast-evaluation-and-cross-validation.md)
- [Week 6: spurious regressions and cointegration](spurious-regression-and-cointegration.md)
- [Week 6: ECM and Granger causality](error-correction-and-granger-causality.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Weeks 4–6 lecture materials and 2026 preparation-exam topics. Problems and answers on this page are independently written study examples.
