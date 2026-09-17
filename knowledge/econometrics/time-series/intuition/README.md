# Time-Series Intuition

This folder explains important time-series terms in plain language with almost no mathematics.

Use it when you want to answer questions such as:

> What is stationarity?

> What is causality?

> What is invertibility?

> What is maximum likelihood?

without immediately giving formulas or technical definitions.

The goal is to understand what a concept is doing, why it matters, and how you would explain it naturally to another person. Once that story is clear, the formal notes in the parent folder provide the mathematics, derivations and exam calculations.

## Current terms

1. [Stationarity](stationarity.md)
2. [AR, MA and ARMA](ar-ma-arma.md)
3. [Causality](causality.md)
4. [Conditional versus unconditional](conditional-vs-unconditional.md)
5. [Mean reversion](mean-reversion.md)
6. [Autocovariance, autocorrelation and the ACF](autocorrelation-and-acf.md)
7. [Invertibility](invertibility.md)
8. [Maximum likelihood](maximum-likelihood.md)
9. [PACF and lag-order selection](pacf-and-lag-order.md)

## How to use this folder

A useful routine is:

1. Pick a term and try to explain it from memory without using a formula.
2. Ask what problem the concept solves or why we need it.
3. Give one concrete example.
4. Only after that, open the formal note and connect the intuition to the mathematics.

For example, before calculating characteristic roots for stationarity, you should first be able to say that stationarity means the underlying statistical behavior of the process stays stable over time. Before solving MA roots for invertibility, you should first understand that invertibility lets us uniquely work backwards from observed values to the underlying shocks.

If you can explain a term clearly in ordinary words, that is a strong sign that the mathematics has a conceptual foundation rather than being memorized mechanically.

For derivations, assumptions, notation and exam calculations, return to the permanent notes in the parent `time-series` folder.
