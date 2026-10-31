# Impulse Response Analysis (Week 4)

Status: developing

## Central question

If a one-time innovation unexpectedly hits a time series, how much does it change the series now and at each future horizon?

An **impulse response function** (IRF) traces the incremental path caused by a shock while other innovations are held fixed. Forecasting asks what will happen given current information; an IRF asks how the predicted path changes when a particular shock is introduced.

## 1. What the IRF means

For a causal linear process with the moving-average representation

$$
X_t-\mu=\sum_{j=0}^{\infty}\psi_j\varepsilon_{t-j},
\qquad \psi_0=1,
$$

the response at horizon $h$ to a one-unit innovation at time $t$ is

$$
\boxed{\operatorname{IRF}(h)=\psi_h.}
$$

For a shock of size $\delta$ (for example, one innovation standard deviation), the incremental response is $\delta\psi_h$. The response is *relative to the no-shock baseline*, not necessarily the total level of $X_{t+h}$.

The coefficients $\psi_h$ are obtained by expressing the process in current-and-past innovations. The same coefficients determine forecast-error variances and therefore connect Week 2 (causality) to Week 4 (forecasting and shocks).

## 2. AR(1): geometric shock decay

Let

$$
X_t=\phi X_{t-1}+\varepsilon_t,\qquad |\phi|<1.
$$

A one-unit shock raises $X_t$ by 1. In the next period, the shock reaches $X_{t+1}$ through $\phi X_t$, so its effect is $\phi$. After two periods it is $\phi^2$.

Therefore

$$
\boxed{\operatorname{IRF}(h)=\phi^h,\quad h=0,1,2,\ldots.}
$$

For $\phi=0.5$ the responses are $1,0.5,0.25,0.125,\ldots$. They decay to zero. With $\phi=-0.5$ they alternate signs: $1,-0.5,0.25,-0.125,\ldots$, still shrinking toward zero.

## 3. MA(1): the effect ends abruptly

For

$$
X_t=\varepsilon_t+\theta\varepsilon_{t-1},
$$

the IRF is

$$
\operatorname{IRF}(0)=1,\qquad
\operatorname{IRF}(1)=\theta,\qquad
\operatorname{IRF}(h)=0\text{ for }h\ge2.
$$

An MA(1) shock reaches exactly two dates. A stationary AR(1) shock can affect infinitely many dates, but with diminishing strength.

## 4. ARMA(1,1): a worked recursion

For

$$
(1-\phi L)X_t=(1+\theta L)\varepsilon_t
$$

the causal expansion is

$$
\frac{1+\theta L}{1-\phi L}
=1+(\phi+\theta)L+\phi(\phi+\theta)L^2+\cdots.
$$

Hence

$$
\boxed{\psi_0=1,\qquad \psi_h=(\phi+\theta)\phi^{h-1}\quad(h\ge1).}
$$

If $\phi=0.6$ and $\theta=0.2$, the first responses are $1,0.8,0.48,0.288$. Notice that the first response is **not** just the AR coefficient: the MA effect matters at horizon 1.

For a general ARMA$(p,q)$, match coefficients of powers of $L$ in

$$
\phi(L)\sum_{j\ge0}\psi_jL^j=\theta(L)
$$

and solve recursively, taking $\psi_j=0$ for $j<0$ and $\theta_j=0$ for $j>q$.

## 5. Unit roots and permanent effects

For a random walk,

$$
X_t=X_{t-1}+\varepsilon_t,
$$

a one-unit shock raises the current level by 1 and never disappears from the level. Its response is

$$
\operatorname{IRF}(h)=1\quad\text{for all }h\ge0.
$$

By contrast, the **differenced** series $\Delta X_t=\varepsilon_t$ has response 1 at horizon zero and 0 thereafter. This distinction is extremely important: *a temporary effect on growth can become a permanent effect on the level*.

For an ARIMA model, calculate the stationary IRF for its differenced component and then reconstruct the response of the level. When $W_t=\Delta X_t$, the level response through horizon $h$ is the cumulative sum of responses in $W$:

$$
\operatorname{IRF}_X(h)=\sum_{j=0}^{h}\operatorname{IRF}_W(j).
$$

Seasonal models use the corresponding ordinary and seasonal difference equations; inspect the impact at lags $s,2s,\ldots$ as well as adjacent dates.

## 6. IRF versus ordinary statistical or causal interpretation

In a single-series ARMA model, an innovation is an unpredictable model disturbance. An IRF describes the response *within that specified model*. It does not by itself prove that an identifiable real-world policy intervention caused the shock. Multivariate structural causality requires additional assumptions or identification.

The short rule:

- **Forecast:** the expected future value using current information.
- **Forecast error:** the eventual actual value minus that forecast.
- **IRF:** the difference between a shocked future path and its no-shock path.

## Common mistakes

- Treating the response as the total predicted level rather than the **additional effect** of a shock.
- Forgetting that a standard-deviation shock scales every response by $\sigma_\varepsilon$.
- Assuming all shocks vanish because the differenced series is stationary.
- Confusing ARMA causality (a past-shock representation) with real-world causal identification.
- Giving the AR(1) response $\phi^{h+1}$ instead of $\phi^h$ when the impact period is $h=0$.

## Retrieval questions

1. Write the IRF at horizons 0–3 for an AR(1) with $\phi=-0.4$.
2. For an MA(1) with $\theta=0.7$, at which horizon does the effect vanish exactly?
3. Derive the first four IRF coefficients for ARMA(1,1) with $\phi=0.6$ and $\theta=-0.3$.
4. Explain why a random-walk **level** responds permanently while its first difference responds for one period.
5. Distinguish the forecast, forecast error and impulse response in one sentence each.

## Related notes

- [Causality and MA representation](arma-models.md)
- [Forecasting and intervals](forecasting-and-prediction-intervals.md)
- [Unit roots](nonstationarity-unit-roots-and-integration.md)
- [Story](story.md)

## Sources

- VU Amsterdam, *Fundamentals of Time Series Econometrics*, Week 4, part 4 and Week 4 lecture.
