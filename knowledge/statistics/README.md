# Statistics

This directory contains permanent notes on learning population quantities from random samples and quantifying sampling uncertainty.

## Current foundation

Recommended reading order:

1. [Parameters, estimators and estimates](parameters-estimators-and-estimates.md)
2. [Sampling distributions](sampling-distributions.md)
3. [Unbiasedness](unbiasedness.md)
4. [Consistency](consistency.md)
5. [Asymptotic normality](asymptotic-normality.md)

## Main distinctions

```text
parameter
= fixed but unknown population quantity

estimator
= random rule based on sample variables

estimate
= realized numerical value from one observed sample
```

The main estimator properties are separated deliberately:

- unbiasedness is a finite-sample expectation property;
- consistency is a large-sample concentration property;
- asymptotic normality describes the limiting shape and scale of estimation error.

## Connection to probability and econometrics

Probability supplies expectations, variances and limit theorems. Econometrics applies these statistical ideas to models relating outcomes and explanatory variables.

The central chain is:

```text
sampling process
→ estimator as a random variable
→ sampling distribution
→ finite-sample properties
→ probability limit
→ asymptotic distribution
→ standard errors and inference
```

## Status

The current notes are marked `developing`. They should be reviewed through derivations, examples and retrieval practice before being marked `stable`.
