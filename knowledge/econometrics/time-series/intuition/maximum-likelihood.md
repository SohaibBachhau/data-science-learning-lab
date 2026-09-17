# Maximum Likelihood

## In ordinary words

Maximum likelihood is a way of choosing model parameters by asking:

> Which parameter values make the data we actually observed look most plausible?

Suppose a model contains an unknown persistence parameter. Different possible values produce different predictions and therefore different residuals. Maximum likelihood compares how plausible those residuals are under the error distribution we assumed and chooses the parameter values that make the whole observed sample most plausible.

## Simple example

Imagine two candidate models for the same time series.

One model produces residuals such as 0.10 and -0.02.

The other produces residuals such as 0.70 and 0.52.

If the model assumes errors are normally distributed around zero, the first pair is much more plausible. Maximum likelihood therefore prefers the parameter values that generated those smaller, more plausible residuals.

The deeper point is not simply "smaller residuals are always better." The residuals are judged using the probability distribution assumed for the errors.

## Why do we need a distribution?

To say that one residual is more likely than another, we need a probability model for the errors.

White noise tells us useful things such as the mean, variance and lack of autocorrelation, but it does not fully specify the shape of the probability distribution. Maximum likelihood needs that extra information.

This is why the Week 2 lecture assumes a distribution such as normal IID errors when constructing the likelihood.

## Why time series are slightly different

In an ordinary independent sample, observations can often be treated separately.

In a time series, today's observation may depend on yesterday's observation and other earlier information. So the question becomes:

> Given what had happened up to yesterday, how plausible is what happened today?

Maximum likelihood therefore uses conditional probabilities or densities that condition on the past.

## Likelihood versus log-likelihood

The likelihood combines the plausibility of all observations under a particular set of parameters.

Because this often involves multiplying many probability densities, the numbers and algebra can become awkward. Taking the natural logarithm converts the product into a sum.

The log does not change which parameter values are best. It only makes the optimization easier.

## What the computer is doing

In practice, software tries different parameter values, calculates how well each set explains the observed data under the assumed distribution, and searches for the values with the highest log-likelihood.

You can picture it as:

```text
try parameters
-> calculate implied prediction errors
-> judge how plausible those errors are
-> combine that information across the sample
-> move toward parameters with a higher likelihood
```

## A good verbal answer

If someone asks, "What is maximum likelihood?", a strong short answer is:

> Maximum likelihood chooses the parameter values that make the observed data most plausible under the model and its assumed probability distribution.

A slightly longer answer is:

> We try possible parameter values, see what probability they assign to the data we observed, and choose the values that give the highest likelihood. In time series, this is usually done conditionally on the past because observations are dependent over time.
