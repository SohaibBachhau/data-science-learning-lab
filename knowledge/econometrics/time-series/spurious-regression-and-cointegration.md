# Spurious Regression and Cointegration (Week 6)

Status: developing

## Central question

When two trending time series move together, is their apparent regression relationship real, or have we discovered a coincidence produced by shared non-stationary behavior?

A regression between unrelated integrated processes can create misleading conventional t-statistics and apparently high fit. **Cointegration** is a special situation in which non-stationary series have a stable linear combination, allowing a meaningful long-run statistical relationship.

## 1. The spurious-regression problem

Take two **independent random walks**:

$$
X_t=X_{t-1}+u_t,\qquad Y_t=Y_{t-1}+v_t,
$$

where the two innovation sequences are mutually independent white noise. By construction, neither walk helps explain the other.

Now fit an ordinary levels regression:

$$
Y_t=\alpha+\beta X_t+e_t.
$$

A conventional regression output may nonetheless show a low p-value, apparently significant $\widehat\beta$, or substantial $R^2$. The variables can happen to drift together for long stretches even though no underlying relationship exists. Standard stationary regression approximations are not reliable in this setting.

**Crucial nuance:** Non-stationarity raises the risk of a spurious levels regression, but **not every regression involving non-stationary variables is spurious**. Cointegrated variables are an important exception.

Spurious regression is about invalid statistical inference from non-stationary data; a statistically non-spurious relationship is still not necessarily a causal relationship.

## 2. Why not always difference both variables?

If $X_t$ and $Y_t$ are each $I(1)$, their differences are often $I(0)$. Regressing $\Delta Y_t$ on $\Delta X_t$ can avoid some of the problematic levels-regression behavior.

However, differencing changes the question: it focuses on short-run changes and can erase information about a stable **long-run equilibrium** in levels. For consumption and income, short-run movements can be noisy even if a persistent long-run relation exists.

## 3. Cointegration in the I(1) case

Two $I(1)$ variables $Y_t$ and $X_t$ are cointegrated if there exists a nontrivial coefficient vector, often normalized into

$$
z_t=Y_t-\alpha-\beta X_t,
$$

such that $z_t$ is $I(0)$. Each level series may wander, but the deviation from their linear relation does not wander without bound in the same way.

**Example using a shared random walk:** Let $S_t=S_{t-1}+\eta_t$ and let $a_t,b_t$ be stationary noises. Define

$$
X_t=S_t+a_t,\qquad
Y_t=2S_t+b_t.
$$

Then both $X$ and $Y$ are $I(1)$, but

$$
Y_t-2X_t=b_t-2a_t
$$

is stationary (under ordinary joint-stationarity assumptions). Thus the cointegrating slope is $\beta=2$.

The cointegrating vector can be scaled without changing the stationary combination. For example, $(1,-2)$ and $(2,-4)$ encode the same relation. Normalization, such as setting the coefficient of $Y_t$ equal to 1, solves the arbitrary scaling.

## 4. What a stationary spread means

Imagine two prices for similar crude oil grades, Brent and WTI. Each price might be highly persistent or approximately $I(1)$, but their difference can remain bounded around a stable level. A departure from the usual price spread may be temporary even though neither price itself returns to a constant mean.

Do **not** assume $\beta=1$ simply because the example involves two prices. The cointegrating vector is an empirical question unless justified by theory or institutional conditions.

## 5. Engle–Granger two-step testing

For two candidate $I(1)$ variables:

1. First examine their integration orders. Confirm that they plausibly share the relevant order.
2. Estimate the long-run levels relation using OLS, for example $Y_t=\alpha+\beta X_t+z_t$.
3. Compute fitted residuals $\widehat z_t=Y_t-\widehat\alpha-\widehat\beta X_t$.
4. Test the residuals for a unit root with an appropriate residual-based Engle–Granger test.

The null is **no cointegration** (residual has a unit root), while the alternative is cointegration under the specified model. Evidence that the fitted residual is stationary supports cointegration.

**Important exam trap:** Do not blindly use ordinary ADF critical values on regression residuals. Because $\alpha$ and $\beta$ were estimated to make those residuals small, the residual test has a different null distribution. Use Engle–Granger or cointegration-specific critical values and account for the deterministic specification.

A small p-value in a properly implemented Engle–Granger test supports rejecting the null of no cointegration. A large p-value does not prove no long-run relation, especially when sample size is small or structural breaks are present.

## 6. Broader definitions and limitations

The common course case is $I(1)$ variables with an $I(0)$ linear combination, often denoted cointegration of order $(1,1)$. In broader settings, variables integrated of order $d$ can have a combination integrated of a lower order $d-b$, for $b>0$.

Cointegration is a **statistical long-run equilibrium relationship**, not automatic proof of economic causation. A relation can fail over time because of regime shifts, omitted structural features or a misspecified combination. For more than two series, there can be multiple distinct cointegrating relations.

## Common mistakes

- Declaring a levels regression valid solely because the t-statistic is large.
- Claiming all regressions between $I(1)$ variables are invalid.
- Confusing an $I(0)$ **difference** such as $\Delta X_t$ with an $I(0)$ **cointegrating spread** such as $Y_t-\beta X_t$.
- Testing fitted cointegrating residuals with the ordinary ADF reference distribution.
- Assuming correlation or cointegration itself proves causation.
- Using a cointegration test before thinking about each variable's integration order.

## Retrieval questions

1. Why can two independent random walks produce a seemingly significant regression?
2. If $X_t=S_t+a_t$ and $Y_t=3S_t+b_t$, find a stationary linear combination.
3. State the Engle–Granger steps and the correct null hypothesis.
4. Why do the residuals require special unit-root critical values?
5. Explain why differencing can discard a long-run relation even while helping with stationarity.

## Related notes

- [Unit roots and integration](nonstationarity-unit-roots-and-integration.md)
- [ADF and KPSS](unit-root-testing.md)
- [Error-correction models](error-correction-and-granger-causality.md)
- [Story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 6, parts 1–2.
