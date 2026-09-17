# Parameter Estimation for Stationary ARMA Models

Status: `developing`

Up to this point, the ARMA equations have usually been written as if the parameters were already known. In real data, they are not. Parameter estimation is the step where we use the observed time series to learn values such as $\phi_1$, $\phi_2$, $\theta_1$, the intercept, and the innovation variance.

## The basic problem

Suppose we believe a series follows

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

We observe the $X_t$ values, but we do not know $\phi$.

Different possible values of $\phi$ imply different predictions and therefore different residuals. Estimation asks which parameter value is most consistent with the data we actually observed.

The Week 2 lecture mentions three methods:

- Yule-Walker estimation, a time-series-specific method;
- least squares estimation for AR models;
- maximum likelihood estimation for ARMA models.

The lecture focuses mainly on maximum likelihood because it is the most general of these methods.

## Maximum likelihood intuition

Maximum likelihood asks:

> Which parameter values make the observed data most plausible under the assumed model and probability distribution?

For example, suppose

$$
X_t=\phi X_{t-1}+\varepsilon_t,
\qquad
\varepsilon_t\overset{iid}{\sim}N(0,\sigma^2),
$$

and we observe

$$
X_0=1,\qquad X_1=0.9,\qquad X_2=0.7.
$$

Compare two candidate values.

### Candidate 1: $\phi=0.8$

At $t=1$ the prediction is

$$
0.8(1)=0.8,
$$

so the implied residual is

$$
0.9-0.8=0.1.
$$

At $t=2$ the prediction is

$$
0.8(0.9)=0.72,
$$

so the implied residual is

$$
0.7-0.72=-0.02.
$$

The residuals are therefore $0.10$ and $-0.02$.

### Candidate 2: $\phi=0.2$

At $t=1$ the prediction is

$$
0.2(1)=0.2,
$$

so the residual is

$$
0.9-0.2=0.7.
$$

At $t=2$ the prediction is

$$
0.2(0.9)=0.18,
$$

so the residual is

$$
0.7-0.18=0.52.
$$

Under a normal error distribution centered at zero, the first pair of residuals is much more plausible than repeatedly observing residuals as large as $0.70$ and $0.52$.

So, in this small comparison, $\phi=0.8$ gives a higher likelihood than $\phi=0.2$.

A precise way to say this is:

> The residuals implied by $\phi=0.8$ are more likely under the assumed error distribution.

## Why a distributional assumption is needed

White noise by itself specifies properties such as zero mean, constant variance, and no autocorrelation, but it does not give a complete probability density.

Maximum likelihood needs a probability density because it measures how plausible the observed data are under particular parameter values.

The lecture therefore considers independent and normally distributed innovations, for example

$$
\varepsilon_t\overset{iid}{\sim}N(0,\sigma^2).
$$

The normality assumption lets us write down a density for the error and therefore a likelihood for the observed data.

## Why time-series likelihoods use conditional densities

Time-series observations are generally dependent. Therefore, we should not treat

$$
X_1,X_2,\ldots,X_T
$$

as if they were independent observations and simply multiply their marginal densities.

Instead, the joint density can be written using conditional densities. In general form,

$$
f(X_t\mid X_{t-1},X_{t-2},\ldots;\theta)
$$

asks:

> Given everything observed in the past, and given these parameter values, how plausible is the value observed at time $t$?

The full likelihood combines these conditional densities across time.

For a simple AR(1), conditioning on $X_{t-1}$ is enough because the direct model is

$$
X_t=\phi X_{t-1}+\varepsilon_t.
$$

Then

$$
E(X_t\mid X_{t-1})=\phi X_{t-1}
$$

and

$$
\operatorname{Var}(X_t\mid X_{t-1})=\sigma^2.
$$

For a general time-series model it is natural to write the conditional density as

$$
f(X_t\mid X_{t-1},X_{t-2},\ldots,X_1;\theta).
$$

The lecture does not require a manual derivation of all conditional means and variances for general ARMA models. Efficient algorithms and statistical software handle that part.

## Likelihood and log-likelihood

If the conditional density contribution from each date is denoted by $L_t$, the likelihood has a product form such as

$$
L(\theta)=L_1L_2\cdots L_T.
$$

Products of many densities can be inconvenient to work with, so we take the natural logarithm:

$$
\log L(\theta)
=
\log L_1+\log L_2+\cdots+\log L_T.
$$

The logarithm turns multiplication into addition.

The value that maximizes the likelihood also maximizes the log-likelihood because the natural logarithm is strictly increasing. So taking logs does not change which parameter values are selected.

The natural logarithm is used because it is mathematically convenient, especially in calculus. Another increasing logarithm base would lead to the same maximizer, but $\ln$ is the standard choice.

## Numerical maximization

For realistic ARMA models, the parameter values that maximize the log-likelihood are generally found with numerical optimization rather than by solving a simple closed-form equation by hand.

Conceptually, the computer does something like this:

```text
try parameter values
-> calculate the conditional likelihood
-> calculate the log-likelihood
-> move toward parameter values with a higher log-likelihood
-> repeat until a maximum is found
```

The important part for this course is understanding what is being maximized and why, not reproducing a software optimizer by hand.

## Relationship with least squares

Least squares chooses parameter values that make squared prediction errors small. Maximum likelihood chooses parameter values that make the observed data highly probable under an assumed distribution.

In simple models with normally distributed errors these ideas are closely related, which is why the methods can feel similar. For general ARMA models, maximum likelihood is the more general framework emphasized in the lecture.

## GDP-growth workflow from the lecture

The lecture applies the whole Week 2 workflow to GDP growth:

1. inspect the time series;
2. use the ACF and PACF to suggest lag orders;
3. choose an ARMA specification;
4. estimate its parameters by maximum likelihood.

In the example, the PACF cuts off after lag 2, suggesting two autoregressive lags. The chosen model is therefore ARMA(2,0), which is simply an AR(2), and its parameters are estimated using maximum likelihood.

## Note on the intercept reported by statsmodels

The lecture notes a software-specific convention. The `statsmodels` ARIMA method reports the estimated unconditional mean $\mu$ as the intercept-like quantity rather than directly reporting the $\alpha$ in

$$
X_t
=\alpha+\phi_1X_{t-1}+\cdots+\phi_pX_{t-p}+\varepsilon_t.
$$

For a stationary ARMA model,

$$
\mu=\frac{\alpha}{1-\sum_{i=1}^p\phi_i}.
$$

Rearranging gives

$$
\boxed{\alpha=\mu\left(1-\sum_{i=1}^p\phi_i\right).}
$$

So if software reports $\mu$ and the AR coefficients, the model intercept can be recovered with this formula.

## What to remember

- In practice, ARMA parameters are unknown and must be estimated from data.
- Yule-Walker, least squares, and maximum likelihood are estimation methods mentioned in Week 2.
- Maximum likelihood chooses parameter values that make the observed data most plausible under the assumed distribution.
- White noise alone is not enough for ML; a full error distribution must be specified.
- Time-series likelihoods use conditional densities because observations are dependent through time.
- The log-likelihood contains the same maximizer as the likelihood but is easier to work with.
- Numerical optimization is normally used to maximize the log-likelihood for ARMA models.
- General ARMA conditional-density derivations are beyond the scope of this course.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 pre-lecture / lecture: Parameter Estimation.
