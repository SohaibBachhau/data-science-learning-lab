# Intuition: Spurious Regression, Cointegration and Error Correction

Status: developing

## The trap of two wandering lines

Imagine watching two people independently wander through a large city. For a while they might both move north, giving the impression that they are traveling together. A regression of one person's position on the other's could show a surprisingly strong trend, even though neither knows or follows the other.

That is the danger with independent non-stationary time series. Their wandering paths can line up by chance. A strong-looking levels regression is not automatically evidence of a meaningful relation.

## Cointegration: wandering together with a tether

Now imagine two people walking while connected by an elastic cord. They can move widely through the city, so neither person's position stays around one fixed point. But the *distance between them* stays within a stable range because they are linked.

This resembles cointegration. Two $I(1)$ series may individually drift, but some linear combination of their levels is stationary. In economics, the tether can represent a long-run statistical relation such as between related commodity prices or between income and consumption. A cointegrating vector tells us the weights needed to form the stable spread.

Simply taking first differences focuses on how fast the walkers move; it may hide the tether. Cointegration retains the information about how far apart their levels have moved.

## Error correction: the pull back toward the tether

Suppose one walker gets too far ahead. The cord pulls them back toward their usual separation. In an error-correction model, last period's *equilibrium error* influences this period's change. That is why the model includes both changes and a lagged levels-based spread.

If we define the error as actual $Y$ minus its long-run expected $Y$, a negative adjustment coefficient pushes an excessively high $Y$ downward. The coefficient's sign is not meaningful until we state which direction the error was defined.

## Granger causality: knowing the past improves predictions

If seeing one walker's earlier movements helps you forecast the second walker's next movements, the first may Granger-cause the second. But that does not demonstrate a physical pull. They could both be following a third person's instructions or responding to the same conditions.

Granger causality is therefore about **predictive information**, not a verified cause-and-effect intervention. It is also distinct from saying an ARMA model is "causal," which refers to using present and past shocks.

## Quick recall

- Spurious regression: wandering non-stationary series can appear related by chance.
- Cointegration: a stable weighted combination can exist even when each level wanders.
- Engle–Granger: estimate the candidate long-run relation, then test its fitted residual for stationarity using special critical values.
- ECM: short-run change responds to last period's long-run gap.
- Granger: lagged information improves predictions, not proof of structural causality.

For exact formulas and examples, use [cointegration](../spurious-regression-and-cointegration.md) and [ECM/Granger](../error-correction-and-granger-causality.md).
