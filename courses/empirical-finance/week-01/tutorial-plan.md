# Week 1 R Tutorial: Plan and Checklist

**Status: not started.** This records what the VU handout asks us to practise, not results we have independently replicated. We will add reviewed R code and interpretation notes only as we actually complete them.

## Part 1: Data, prices and returns

1. Start from a clean R session. Load only required packages.
2. Retrieve the S&P 500 **total return** index and inspect the first/last rows, missingness and unusual values.
3. Compare the total-return and price-only S&P 500 indices. Dividends matter.
4. Compute simple returns and log returns from adjusted values; confirm $Y_t=\ln(1+R_t)$.
5. Inspect the difference between return types, especially on extreme days; compare with the small-return approximation $R^2/2$.
6. Create a well-labelled summary-statistics table for prices, including sample period, units and observation count.

The tutorial handout uses tidyquant, dplyr, ggplot2, tseries and knitr. It covers data from around January 2000 to June 2026. Do not commit downloaded data or course PDFs without checking rights and size.

## Part 2: Fat tails and normality

1. Standardise daily log returns to mean zero and sample SD one.
2. Plot a histogram of standardised returns with a normal-density overlay.
3. Produce a normal QQ plot and inspect the tails.
4. Compute and interpret Jarque-Bera skewness, kurtosis, test statistic, critical value and p-value.
5. As an extra task, compare QQ plots against Student-t references with $\nu=3$, $\nu=5$ and $\nu=30$, matching scale appropriately for fair comparison.
6. Reproduce plots and tables after restarting R to verify a self-contained analysis.

## Quality checks

- No package installation commands inside the submitted script.
- Verify data source, ticker, dates, dividends and missing values.
- Use explicit package names where functions can conflict.
- Use informative plot titles, labelled axes, sensible units and dates.
- Give consistent rounding in tables; do not display a tiny p-value as zero.
- State null hypothesis, evidence, decision and financial interpretation in words.
- Separate a successful execution from a substantively correct result.

## Next action

Start the handout with the data and setup section together; record actual R code and results in this folder when completed.

## Source

*Empirical Finance Week 1 tutorial for students*, VU Amsterdam, 2026.
