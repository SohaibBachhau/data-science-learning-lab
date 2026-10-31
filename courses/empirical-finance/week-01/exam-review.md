# Week 1 Exam Review

Status: developing. This page records **conceptual lessons** from the lecture's eight multiple-choice checks without reproducing the copyrighted slide questions.

## Answer key and interpretation

| Lecture check | Correct option | The point to understand |
| --- | --- | --- |
| Q1, slide 25 | C | Simple and log returns approximately coincide for small price changes, since $\ln(1+R)\approx R$. |
| Q2, slide 26 | D | S&P 500 returns are based on market-cap-weighted *relative returns*, not absolute price changes. |
| Q3, slide 27 | C | Compound gross daily returns: $(1.01)^{10}(1.005)^{10}-1\approx16.11\%$. |
| Q4, slide 42 | A | Volatility clustering concerns large or small magnitudes following similar magnitudes, regardless of sign. |
| Q5, slide 43 | C | De-meaning changes the mean but leaves ordinary autocorrelations unchanged. |
| Q6, slide 57 | A | In fat tails, lower observed quantiles are below theoretical normal quantiles, upper observed quantiles above them. |
| Q7, slide 58 | D | The displayed sample histogram has a narrower observed range than the normal reference, indicating thin tails. |
| Q8, slide 59 | B | Standardisation makes mean zero and SD one but preserves a scaled Student-t distribution and its $\nu=4$ tail-shape parameter. |

## Mistakes worth preventing

**Don't confuse a calculation with an option letter.** In the twenty-day return question, the compounding formula is correct only if the computed value is matched to its option.

**Read every word of a market-cap question.** A market-cap-weighted index averages *relative* stock returns, not absolute euro or dollar price differences.

**Be precise about quantile signs.** In the lower tail, -2.33 is *higher* than -3.50; in the upper tail, +2.33 is *lower* than +3.50.

**Separate two kinds of squaring.** The Ljung-Box statistic squares autocorrelation coefficients for any input series. Testing squared returns first squares the data, then computes its ACF.

**Use the right null distribution.** Ljung-Box uses an upper-tail chi-squared threshold with $m$ degrees of freedom for $m$ tested lags (under the basic assumptions). Jarque-Bera uses two degrees of freedom.

## Fresh retrieval questions

1. A stock rises by 20% and then falls by 20%. What is the total simple return?
2. An index gives a 70% weight to a stock returning 5% and a 30% weight to a stock returning -10%. What is its simple return?
3. Why can a zero-mean AR(1) process still be serially correlated?
4. What changes when you standardise a fat-tailed return series? What stays the same?
5. How can a distribution have heavier extreme tails but the same variance as a normal distribution?

### Answers to self-check

1. $1.20(0.80)-1=-4\%$.
2. $0.70(0.05)+0.30(-0.10)=0.005=0.5\%$.
3. De-meaning removes a level, not lagged dependence.
4. Sample mean becomes zero and sample SD one; basic distribution shape and Student-t degrees-of-freedom parameter do not become normal automatically.
5. More extreme outcomes may be sufficiently rare and offset by more mass near the centre; or a heavier-tailed distribution can be rescaled to the same variance.
