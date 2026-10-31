# Error-Correction Models and Granger Causality (Week 6)

Status: developing

## Central question

If two non-stationary variables share a long-run equilibrium, how can short-run changes respond when they drift apart? And can one variable's past improve predictions of the other?

These are two different questions. An **error-correction model** (ECM) combines short-run changes with the lagged equilibrium error. **Granger causality** asks about incremental predictive information from past values; it is not in itself causal identification.

## 1. From cointegration to error correction

Suppose $X_t$ and $Y_t$ are each $I(1)$ and cointegrated:

$$
z_t=Y_t-\alpha-\beta X_t\sim I(0).
$$

Here $z_t$ is the equilibrium deviation or **error-correction term**. A simple single-equation ECM is

$$
\boxed{
\Delta Y_t
=c+\lambda z_{t-1}
+\gamma\Delta X_t
+\delta\Delta Y_{t-1}
+u_t.
}
$$

The lagged level combination $z_{t-1}=Y_{t-1}-\alpha-\beta X_{t-1}$ represents long-run disequilibrium. The differenced terms describe shorter-run adjustment. With appropriate assumptions and specification, $u_t$ is an innovation.

The model is often estimated after an Engle–Granger cointegration step by substituting the fitted lagged spread $\widehat z_{t-1}$.

## 2. Why the sign matters

Suppose $\beta>0$ and $Y_{t-1}$ is **above** its long-run value $\alpha+\beta X_{t-1}$, so $z_{t-1}>0$. If $\lambda<0$, the term $\lambda z_{t-1}$ pushes $\Delta Y_t$ downward. This is the correction mechanism.

Example: the long-run relation is $Y_t=2X_t$, yesterday $X_{t-1}=10$ and $Y_{t-1}=23$, so

$$
z_{t-1}=23-2(10)=3.
$$

With $\lambda=-0.2$ and all other right-hand-side contributions zero,

$$
\Delta Y_t=-0.2(3)=-0.6.
$$

The deviation falls from $3$ to $2.4$ if $X$ remains unchanged. This represents a 20% correction over one period in the simplified setup.

The interpretation **depends on how the error term is defined**. If instead someone defines the spread as $\alpha+\beta X-Y$, the adjustment coefficient should have the opposite sign for the same restoring behavior.

## 3. Speed of adjustment and overshooting

In the stripped-down mechanism with fixed $X$ and other terms set to zero,

$$
z_t=(1+\lambda)z_{t-1}.
$$

The deviation converges when $|1+\lambda|<1$, or

$$
\boxed{-2<\lambda<0.}
$$

- $-1<\lambda<0$: gradual monotonic correction.
- $\lambda=-1$: one-step correction.
- $-2<\lambda<-1$: correcting with alternating overshoots.
- $\lambda=0$: no error correction through this equation.
- Outside the stable interval: this simple mechanism does not converge.

These rules apply to the **isolated adjustment equation**, not necessarily to every multivariate ECM with feedback between variables. Always check which variable adjusts and what other dynamics are present.

## 4. Why an ECM is different from differencing alone

A regression containing only $\Delta Y_t$ and $\Delta X_t$ describes co-movements in changes. It says nothing about whether yesterday's gap between levels matters for today's adjustment.

The ECM preserves the key level information through $z_{t-1}$ while keeping the other dynamics in stationary differences. This is the bridge between a long-run relation and short-run dynamics.

A negative estimated $\lambda$ may be consistent with error correction; its economic interpretation and statistical reliability still depend on correct specification, cointegration, parameter uncertainty and the chosen normalization.

## 5. Granger causality: what it actually tests

Past $X$ values **Granger-cause** $Y$ if they help predict $Y$ after accounting for relevant past $Y$ and any other conditioning information in the chosen model. One common finite-lag regression for stationary series is

$$
Y_t=c+\sum_{i=1}^{p}a_iY_{t-i}
+\sum_{j=1}^{q}b_jX_{t-j}+u_t.
$$

The predictive null is

$$
\boxed{H_0:b_1=b_2=\cdots=b_q=0.}
$$

A joint F or Wald test can ask whether these lagged $X$ terms add predictive power. Depending on the integration and cointegration properties, the series may need to be transformed or modeled in an appropriate VAR/VECM framework for valid inference.

A rejection means lagged $X$ adds statistically significant predictive information **in that particular model and information set**. It does not imply that changing $X$ by intervention will change $Y$.

## 6. Why Granger causality is not ordinary causality

Consider an example where a weather forecast predicts both rain and umbrella sales. Earlier forecasts could help predict later umbrella purchases without themselves causing the weather. Similarly, confounding variables, common trends, omitted information or feedback can drive apparent predictive direction.

It is possible for $X$ to Granger-cause $Y$, for $Y$ to Granger-cause $X$, for both directions to be significant, or for neither direction to be significant. Results depend on lag length, information set, stationarity treatment and sample.

**Distinguish three uses of the word "causal":**

1. **Causal ARMA representation:** current $X_t$ uses current and past innovations, not future innovations.
2. **Granger causality:** past $X$ adds predictive information for $Y$.
3. **Economic/structural causality:** an actual intervention on $X$ changes $Y$, requiring additional identifying assumptions or research design.

They are not interchangeable.

## Common mistakes

- Putting $z_t$ rather than lagged $z_{t-1}$ into the basic ECM without considering simultaneity.
- Saying $\lambda$ must always be negative without defining the orientation of the spread.
- Interpreting a negative coefficient as meaningful without evidence of cointegration.
- Forgetting that positive $z$ means a level is above equilibrium only under the chosen normalization.
- Claiming a Granger rejection establishes policy causation.
- Running standard level-regression lag tests on integrated variables without addressing inference.

## Retrieval questions

1. Write the ECM if the cointegrating relation is $Y_t=1+1.5X_t$.
2. If yesterday's spread $Y_{t-1}-1-1.5X_{t-1}$ is $4$ and $\lambda=-0.25$, what is its isolated correction contribution to $\Delta Y_t$?
3. For the stripped-down ECM, explain the difference between $\lambda=-0.4$ and $\lambda=-1.3$.
4. State the null of a Granger causality test from $X$ to $Y$.
5. Explain in ordinary words why Granger causality and actual causation differ.

## Related notes

- [Cointegration and spurious regression](spurious-regression-and-cointegration.md)
- [ARMA causality](arma-models.md)
- [Forecasting](forecasting-and-prediction-intervals.md)
- [Story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 6, parts 3–4.
