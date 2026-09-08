# The Story of Statistics

Status: `developing`

This page is a low-friction overview of the statistics branch. It is meant to restore the big picture before you return to the formal notes.

## The story

Statistics begins with a simple problem: the population contains quantities we care about, but we usually observe only a sample.

A population quantity such as a mean or regression coefficient is a parameter. It is fixed but unknown.

We use a rule based on the random sample to learn about that parameter. That rule is an estimator. Once we observe one particular sample, the estimator produces an estimate.

Because a different sample would generally give a different estimate, the estimator itself is random before the data are observed. Its possible values across repeated samples form its sampling distribution.

This leads to the main questions in statistics.

Is the estimator centered on the correct value? That is the idea behind unbiasedness.

Does it get closer to the correct value as the sample becomes larger? That is consistency.

Can we describe the shape of its uncertainty in large samples? That is where asymptotic normality enters.

Once we know how an estimator behaves, we can quantify uncertainty using standard errors, confidence intervals and hypothesis tests.

So the main story is:

```text
unknown population quantity
→ random sample
→ estimator
→ sampling distribution
→ bias and variance
→ consistency
→ asymptotic normality
→ standard errors and inference
```

## The three objects that should never be mixed up

A parameter is the fixed but unknown target.

An estimator is the random procedure used to estimate it.

An estimate is the number produced by the estimator in one observed sample.

## What to remember

Unbiasedness and consistency are not the same thing. Unbiasedness is about the estimator's average over repeated samples. Consistency is about what happens as the sample size grows.

A sampling distribution is not the distribution of the original data. It is the distribution of an estimator across hypothetical repeated samples.

Large-sample theory matters because it lets us approximate estimator uncertainty even when exact finite-sample distributions are difficult.

## When the detailed notes feel heavy

Use this page to recover the logic first. Then open the detailed notes for the exact definitions and derivations.

## Related notes

- [Statistics index](README.md)
- [Parameters, estimators and estimates](parameters-estimators-and-estimates.md)
- [Sampling distributions](sampling-distributions.md)
- [Unbiasedness](unbiasedness.md)
- [Consistency](consistency.md)
- [Asymptotic normality](asymptotic-normality.md)
