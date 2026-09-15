# AR, MA and ARMA

AR, MA and ARMA are three ways of describing how the present depends on the past.

An AR model says that today's value is influenced by earlier values of the series itself. A high value yesterday can therefore carry into today, and because yesterday already contains the effects of even older shocks, the influence of the past can stretch a long way back.

A useful phrase is:

> AR remembers past values.

An MA model works differently. It says that today's value is built from current and past shocks. The model directly remembers shocks for only a fixed number of periods.

A useful phrase is:

> MA remembers past shocks.

An ARMA model simply combines both ideas: the current value can depend on previous values of the series and on current or past shocks.

The numbers in ARMA(p,q) tell you how many of each type of lag are included. The first number belongs to the AR side, and the second belongs to the MA side.

## One-sentence answers

**AR:** today's value depends on past values of the same series.

**MA:** today's value depends directly on recent shocks.

**ARMA:** combines dependence on past values and past shocks.
