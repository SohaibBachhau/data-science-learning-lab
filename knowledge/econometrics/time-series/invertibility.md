# Invertibility of MA Models

Status: `developing`

Invertibility is the MA-side counterpart to stationarity and causality on the AR side. The mathematical test looks very similar, but the interpretation is different.

## The main idea

For an ARMA model

$$
\phi(L)X_t=\theta(L)\varepsilon_t,
$$

stationarity and causality are determined by the AR polynomial $\phi(L)$. Invertibility is determined by the MA polynomial $\theta(L)$.

The general invertibility condition is:

$$
\boxed{\text{all roots of the MA polynomial must lie outside the unit circle}.}
$$

If the MA polynomial is

$$
\theta(L)=1+\theta_1L+\cdots+\theta_qL^q,
$$

replace $L$ by an ordinary variable $z$, solve

$$
\theta(z)=0,
$$

and check that every root satisfies

$$
|z|>1.
$$

The procedure is therefore the same kind of root calculation used for AR stationarity, but now the MA polynomial is being tested.

## MA(1) shortcut

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
$$

the MA polynomial is

$$
\theta(L)=1+\theta L.
$$

The root equation is

$$
1+\theta z=0,
$$

so

$$
z=-\frac{1}{\theta}.
$$

Invertibility requires

$$
\left|-\frac{1}{\theta}\right|>1,
$$

which is equivalent to

$$
\boxed{|\theta|<1.}
$$

This shortcut is specific to MA(1). For higher-order MA models, solve the roots of the full MA polynomial.

## Why invertibility matters: identification

For an MA(1), the lag-1 autocorrelation is

$$
\rho(1)=\frac{\theta}{1+\theta^2}.
$$

Now compare $\theta=a$ with $\theta=1/a$. They give the same lag-1 autocorrelation:

$$
\frac{1/a}{1+(1/a)^2}
=
\frac{a}{1+a^2}.
$$

For example,

$$
\theta=0.5
$$

and

$$
\theta=2
$$

both give

$$
\rho(1)=0.4.
$$

So the same autocorrelation pattern can correspond to more than one MA parameterization. This is the identifiability problem.

The invertibility restriction selects one representation. For MA(1), we keep the representation with

$$
|\theta|<1.
$$

Thus the representation with $\theta=0.5$ is invertible, while the representation with $\theta=2$ is not.

Important: the non-invertible representation does not somehow become invertible because we ignore it. It remains non-invertible. The point is that an equivalent invertible representation exists, and the invertibility restriction tells us which representation to use.

## Why it is called invertibility

Start from

$$
X_t=(1+\theta L)\varepsilon_t.
$$

If the MA polynomial is invertible, we can solve for the shock:

$$
\varepsilon_t=\frac{1}{1+\theta L}X_t.
$$

Using the geometric-series expansion,

$$
\frac{1}{1+\theta L}
=
1-\theta L+\theta^2L^2-\theta^3L^3+\cdots,
$$

when $|\theta|<1$.

Therefore,

$$
\varepsilon_t
=
X_t-\theta X_{t-1}+\theta^2X_{t-2}-\theta^3X_{t-3}+\cdots.
$$

So the current shock can be reconstructed from current and past observed values of the series.

The signs in this expression depend on the actual value of $\theta$. For example, if $\theta=-0.5$, then $-\theta=+0.5$, so the first lag coefficient is positive. Do not memorize the displayed minus sign as meaning that every numerical lag coefficient must be negative.

## AR(infinity) representation

Rearranging the previous expression gives

$$
X_t
=
\theta X_{t-1}
-\theta^2X_{t-2}
+\theta^3X_{t-3}
-\cdots
+\varepsilon_t.
$$

This is an AR($\infty$) representation.

This gives a useful symmetry:

- a causal AR model can be rewritten as an MA($\infty$) model;
- an invertible MA model can be rewritten as an AR($\infty$) model.

Causality asks whether $X_t$ can be built from current and past shocks. Invertibility asks whether the shock can be recovered from current and past observed $X$ values.

## Exam notation

Suppose

$$
X_t-X_{t-1}=\varepsilon_t-0.5\varepsilon_{t-1}.
$$

A clean exam solution is:

$$
(1-L)X_t=(1-0.5L)\varepsilon_t.
$$

Then label the MA polynomial:

$$
\theta(L)=1-0.5L.
$$

To find the roots, replace $L$ by $z$:

$$
\theta(z)=1-0.5z=0.
$$

Hence

$$
z=2.
$$

Since

$$
|2|>1,
$$

the MA polynomial is invertible.

The notation distinction is useful:

- $\theta(L)$ is the MA polynomial written with the lag operator;
- $\theta(z)$ is the same polynomial written with an ordinary variable so that its roots can be solved.

## Boundary example

Consider

$$
X_t-X_{t-1}
=
\varepsilon_t-1.3\varepsilon_{t-1}+0.3\varepsilon_{t-2}.
$$

The MA polynomial is

$$
\theta(L)=1-1.3L+0.3L^2.
$$

The root equation is

$$
1-1.3z+0.3z^2=0.
$$

The roots are

$$
z_1=\frac{10}{3},\qquad z_2=1.
$$

Although the first root lies outside the unit circle, the second root lies exactly on it. The condition requires every root to satisfy $|z|>1$, so the polynomial is not invertible.

A good exam conclusion is:

> The MA polynomial is not invertible because one root lies on the unit circle.

## Stationarity versus invertibility

Keep the two tests separate:

| Property | Polynomial to inspect | Root condition |
| --- | --- | --- |
| Stationarity / causality | AR polynomial $\phi(L)$ | all roots outside unit circle |
| Invertibility | MA polynomial $\theta(L)$ | all roots outside unit circle |

The root condition is the same. The polynomial being tested and the interpretation are different.

## What to remember

- MA models are always stationary, but they are not automatically invertible.
- Invertibility is about the MA polynomial.
- All MA roots must lie outside the unit circle.
- For MA(1), invertibility is equivalent to $|\theta|<1$.
- Invertibility solves the MA identification problem by selecting a unique representation.
- An invertible MA process can be written as an AR($\infty$) process.
- In exam solutions, clearly distinguish $\theta(L)$ from the root equation $\theta(z)=0$.

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2, part 5: Invertibility.
- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 2 exercise book.
