# Business Insights & Findings
### Sales Channel Forecasting — MLForecast + LightGBM

---

## The Business Problem

Most mid-size companies fly blind on channel-level revenue 30, 60, and 90 days out. They're working off gut feel, last month's numbers, or a spreadsheet someone built three years ago. That gap costs money — in missed inventory calls, understaffed sales teams, and budgets built on assumptions instead of data.

This model was built to answer a straightforward question: **given what we know about how each channel has performed, what should we expect over the next six months — and how confident should we be in that number?**

---

## What the Data Showed

Three channels were modeled independently — Direct, Retail, and Online — each with distinct growth trajectories over 36 months of history.

**Online was the fastest-growing channel by a significant margin.** It outpaced Direct and Retail in month-over-month growth rate, which has real implications for where a business should be allocating budget and headcount. If you're still splitting resources evenly across channels, this data would tell you to stop.

**Direct was the highest-revenue channel in absolute dollars**, but its growth rate was the slowest of the three. That's a classic mature channel profile — reliable base, but not where incremental investment pays off.

**Retail sat in the middle** — stable, predictable, modest growth. The kind of channel that doesn't need active management so much as it needs to not be neglected.

---

## What the Model Predicted

The 6-month forward forecast continued each channel's established trend with high consistency. No dramatic inflection points, no sudden reversals — which is exactly what you'd expect from a business without heavy seasonality or external shock variables.

Key takeaway for a business leader: **the next six months look like the last six months, scaled forward.** If that's acceptable, no action needed. If leadership is expecting a step-change in any channel, this model would tell you that expectation isn't supported by the historical pattern — and that's a conversation worth having before the budget is locked.

---

## How Accurate Was It?

The model was validated using time series cross-validation — meaning it was tested by training on earlier data and predicting periods it had never seen, the same way it would perform in production. This avoids the common mistake of testing a model on data it was already trained on, which inflates accuracy scores artificially.

**LightGBM outperformed Linear Regression on every channel.** The gap wasn't dramatic, which actually tells you something useful — the underlying relationships in this data are largely linear. Trend and recent momentum explain most of what's happening. You don't need a complex model to forecast this business well. That's a feature, not a limitation.

Error rates (MAE) stayed within a range that would be operationally acceptable for budgeting and planning purposes — meaning the forecasts were close enough to actuals that a finance team could use them as a planning input with reasonable confidence.

---

## What Drove the Predictions

The feature importance analysis showed that **the most recent month's sales value was the single strongest predictor of next month's performance**, followed by the 3-month rolling average. Longer lags (3 and 6 months back) contributed less, and the month of year contributed almost nothing — confirming the low-seasonality assumption.

In plain English: **where you were last month is the best indicator of where you'll be next month.** For a stable, trend-driven business, that's both intuitive and actionable. It means the model isn't finding hidden patterns — it's confirming that the business behaves consistently, which is actually what you want to see before trusting a forecast.

---

## So What Would You Do With This?

A few concrete decisions this model would support in a real business context:

- **Budget allocation** — shift incremental investment toward Online, which is growing fastest and shows no signs of plateauing in the forecast window
- **Sales capacity planning** — use the 6-month channel forecasts as inputs to headcount modeling, so hiring decisions are tied to projected demand rather than last year's actuals
- **Executive reporting** — replace the "here's what happened last month" narrative with a forward-looking view that gives leadership something to act on
- **Early warning system** — when actual monthly results come in, compare them against the forecast. A consistent miss in either direction is a signal that something structural has changed and the model needs to be updated

---

## What This Model Doesn't Do

Worth being direct about the limitations, because a forecast without caveats is just a guess with a confidence problem.

- **It doesn't account for external events** — a pricing change, a competitor move, a macro shift, or a new product launch would not be captured in a model trained on historical sales alone. Those would need to be added as external regressors.
- **It assumes the past predicts the future** — which holds until it doesn't. This model would not have predicted COVID's impact on channel mix in Q1 2020, for example.
- **The data here is synthetic** — built to mirror realistic channel dynamics, but not drawn from an actual business. The methodology is production-ready; the numbers are illustrative.

---

*For technical implementation details, see the [main notebook](./sales_channel_forecast_Final.ipynb).*
