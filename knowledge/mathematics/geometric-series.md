# Geometric Series

Status: `developing`

This note contains the geometric-series ideas currently needed for time-series econometrics.

## Core rule

A geometric series has the form

$$
1+x+x^2+x^3+\cdots.
$$

When

$$
|x|<1,
$$

the powers shrink toward zero and the infinite series converges to

$$
\boxed{\frac{1}{1-x}=1+x+x^2+x^3+\cdots}.
$$

For example,

$$
1+0.5+0.5^2+0.5^3+\cdots=\frac{1}{1-0.5}=2.
$$

If `|x|>1`, the powers do not shrink toward zero, so this convergent expansion does not work.

## Short derivation

Let

$$
S=1+x+x^2+x^3+\cdots.
$$

Then

$$
xS=x+x^2+x^3+x^4+\cdots.
$$

Subtracting gives

$$
S-xS=1,
$$

so

$$
S(1-x)=1
$$

and therefore

$$
S=\frac{1}{1-x}.
$$

## Why it matters in time series

For a stationary AR(1),

$$
(1-\phi L)X_t=\varepsilon_t.
$$

Solving for `X_t` gives

$$
X_t=\frac{1}{1-\phi L}\varepsilon_t.
$$

When `|phi|<1`, use the geometric-series rule with `x=phi L`:

$$
\frac{1}{1-\phi L}
=
1+\phi L+\phi^2L^2+\phi^3L^3+\cdots.
$$

Therefore

$$
X_t
=
\varepsilon_t
+\phi\varepsilon_{t-1}
+\phi^2\varepsilon_{t-2}
+\phi^3\varepsilon_{t-3}
+\cdots.
$$

The powers have two different roles:

- `phi^2`, `phi^3`, etc. are ordinary numerical powers;
- `L^2`, `L^3`, etc. indicate how many periods to lag.

So `phi^2 L^2 epsilon_t = phi^2 epsilon_{t-2}`.

## Multiplying two power series

When an AR polynomial factors into two pieces, two geometric expansions may have to be multiplied.

For

$$
(a_0+a_1L+a_2L^2+\cdots)
(b_0+b_1L+b_2L^2+\cdots),
$$

the coefficient of `L^k` is obtained by multiplying every pair whose exponents add to `k`.

For `L^2`, use

$$
0+2,\quad1+1,\quad2+0.
$$

For `L^3`, use

$$
0+3,\quad1+2,\quad2+1,\quad3+0.
$$

So, when both series start at `L^0`, the coefficient of `L^k` receives `k+1` contributions.

## What to remember

- `1/(1-x) = 1+x+x^2+...` when `|x|<1`.
- The key reason is that the powers of `x` shrink toward zero.
- In time series, substitute `x=phi L` to invert a simple AR lag polynomial.
- Powers of coefficients are ordinary powers; powers of `L` are lag operators.
- When multiplying power series, collect all pairs of powers that add to the desired lag.

## Course connection

This mathematics is used in Week 2 to invert AR lag polynomials and obtain causal MA(infinity) representations.
