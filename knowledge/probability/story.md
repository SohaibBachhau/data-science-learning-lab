# The Story of Probability

Status: `developing`

This page is a low-friction overview of the probability branch. It is meant to help you remember how the ideas connect before opening the detailed notes.

## The story

Probability starts with uncertainty.

Before data are observed, we do not know exactly what values will appear. We therefore describe possible outcomes using random variables and probability distributions.

A distribution tells us which values a random variable can take and how likely those values are. Once we have a distribution, we naturally want to summarize it. Expectation tells us where the distribution is centered, while variance tells us how spread out it is.

Real problems usually involve more than one random variable. That is why joint distributions matter. They describe how variables behave together. Covariance measures whether two variables tend to move together, while independence is a stronger idea: knowing one variable does not change the distribution of the other.

Conditioning then lets us update what we expect once information is known. Instead of asking only for the average value of Y, we can ask what we expect Y to be when X is known:

$$
E(Y \mid X).
$$

This idea becomes central in econometrics because regression is largely about conditional relationships.

When we move from one observation to a sample, we need to understand what happens as the sample grows. The law of large numbers explains why sample averages can settle near population expectations. The central limit theorem explains why many properly standardized sample averages become approximately normal in large samples.

So the main story is:

```text
uncertainty
→ random variables and distributions
→ expectation and variance
→ joint behavior and dependence
→ conditional expectation
→ repeated sampling
→ law of large numbers
→ central limit theorem
→ statistical and econometric inference
```

## What to remember

Probability is the language for describing uncertainty before we observe the data.

Expectation describes the center of a distribution. Variance describes its spread. Covariance describes linear co-movement between variables. Conditional expectation tells us how our expected value changes when information is known.

The LLN and CLT are the bridge from probability to statistics: one explains convergence, the other explains the approximate shape of remaining sampling uncertainty.

## When the detailed notes feel heavy

Use this page first to recover the story. Then open the detailed note for the definition, assumptions, derivation, examples and edge cases.

## Related notes

- [Probability index](README.md)
- [Random variables and distributions](random-variables-and-distributions.md)
- [Expectation](expectation.md)
- [Conditional expectation](conditional-expectation.md)
- [Variance, covariance and moments](variance-covariance-and-moments.md)
- [Law of large numbers](law-of-large-numbers.md)
- [Central limit theorem](central-limit-theorem.md)
