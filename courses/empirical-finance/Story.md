# The Story of Empirical Finance

Status: developing. This is an intuitive overview of what we have learned so far. Technical details live in the [Week 1 lecture notes](week-01/lecture-notes.md).

## From a price to a risk model

We begin with prices because they are the most visible part of financial markets. A price alone, however, does not tell us how well an investment performed. A gain of 5 euros means something very different on a 100-euro investment than on a 10,000-euro investment. Returns allow us to compare gains and losses relative to the money invested. Adjusted price data also matter because dividends and corporate actions affect the experience of an investor.

There are two convenient ways of expressing a return. Simple returns answer the direct investment question: what percentage did the investment gain or lose? Gross simple returns multiply across time. Log returns express the same price movement on a logarithmic scale. They add across time, so they are often easier to manipulate in time-series models. Neither is universally the best choice: simple returns aggregate neatly across portfolio weights, while log returns aggregate neatly over time.

Once we have calculated returns, we can describe them. Their mean tells us about the average movement, and their standard deviation, called volatility, tells us how much observations fluctuate around that mean. Percentiles answer another question: how bad or good are particular parts of the observed distribution? These summaries are a starting point, not a complete description of financial risk.

The first surprising finding is that volatility itself changes. Calm days often come in runs, and turbulent days often come in runs. Large positive and negative price changes can cluster together. We may have little ability to forecast the sign of tomorrow's return while still having information about the likely magnitude of tomorrow's move. Squared returns and their autocorrelations help us see this difference. The Ljung-Box test checks whether several autocorrelations, considered jointly, are too large to attribute to the null of no serial correlation.

The second surprise is that extreme returns are not as rare as a normal distribution would suggest. A normal distribution is determined by its mean and variance, but two distributions can share those properties and still look very different in their tails. Skewness helps us describe asymmetry, while kurtosis is sensitive to extreme deviations. The Jarque-Bera test combines both features to test normality. QQ plots make the departure visible: sample quantiles can be much more extreme than the theoretical normal quantiles. A Student-t distribution with a suitable degrees-of-freedom parameter can sometimes better capture those tails.

The third surprise concerns diversification. A single correlation coefficient can conceal how two assets behave in different market states. They might move relatively independently during calm periods but decline together during a crisis. If correlations rise in downturns, a portfolio can become less diversified just when protection is most valuable.

Those three discoveries motivate the rest of Empirical Finance. We need models that allow volatility to change, distributions that acknowledge extreme events, ways to forecast risk, and tests of whether those forecasts actually work. Eventually, we combine the tools to think about portfolios.

## One-sentence map

Prices -> adjusted returns -> descriptive statistics -> volatility clustering, fat tails and state-dependent dependence -> risk models -> forecast evaluation -> portfolio decisions.

## Questions to retrieve later

1. Why are simple returns compounded through time while log returns are added?
2. Why can squared returns be autocorrelated even if original returns are hard to predict?
3. How can two return distributions have the same variance but different tail risk?
4. Why might portfolio diversification become less effective in a crisis?

## Related notes

- [Week 1 lecture notes](week-01/lecture-notes.md)
- [Glossary](Glossary.md)
- [Time series intuition](../../knowledge/econometrics/time-series/README.md)
