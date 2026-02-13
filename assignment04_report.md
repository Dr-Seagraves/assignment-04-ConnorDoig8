# Assignment 04 Interpretation Memo

**Student Name:** Connor Doig
**Date:** February 13, 2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): 0.1096 (SE: 0.0062, p-value: <0.0001)
- Slope (β₁): -0.0670 (SE: 0.0327, p-value: 0.0406)
- R²: 0.001742 | N: 2407

**Model 2: ret ~ prime_rate**
- Intercept (β₀): 0.1268 (SE: 0.0158, p-value: <0.0001)
- Slope (β₁): -0.0052 (SE: 0.0037, p-value: 0.1546)
- R²: 0.000842 | N: 2407

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): 0.0996 (SE: 0.0094, p-value: <0.0001)
- Slope (β₁): 0.5090 (SE: 0.5793, p-value: 0.3796)
- R²: 0.000322 | N: 2398

*Note: Model 3 may have fewer observations if ffo_at_reit has missing values; statsmodels drops those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a -0.0670 (or -6.70 percentage point) change in annual return.
- This negative relationship suggests that REITs with higher current dividend yields earned lower subsequent annual returns during this period. This may reflect a "high-yield trap" where elevated yields signal financial stress or reduced growth prospects. The relationship is statistically significant at the 5% level.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a -0.0052 (or -0.52 percentage point) change in annual return.
- The evidence suggests REIT returns are negatively sensitive to interest rates (higher rates associated with lower returns), which intuition supports because higher discount rates reduce present values of future cash flows. However, this relationship is not statistically significant at the 5% level, meaning the observed slope could plausibly be zero.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets (fundamental performance) is associated with a 0.5090 change in annual return.
- This positive coefficient suggests that REITs with higher profitability measures (FFO relative to assets) tend to earn higher returns, although unexpectedly large in magnitude. However, the relationship is not statistically significant (p-value = 0.3796), so we cannot reliably conclude that fundamental profitability drives returns.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant — Higher dividend yield is significantly associated with lower subsequent annual returns (t = -2.05, p = 0.041).
- **prime_rate:** Not significant — The negative association with prime rates is suggestive but could arise by chance (t = -1.42, p = 0.155).
- **ffo_at_reit:** Not significant — FFO/Assets shows a positive slope but lacks statistical evidence of a reliable relationship (t = 0.88, p = 0.380).

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** Dividend yield (div12m_me) is the only predictor with a statistically significant slope at the 5% level. Its t-statistic of -2.05 is the largest in magnitude among the three models

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- Dividend yield explains 0.174% of variation in annual returns (R² = 0.001742)
- Prime rate explains 0.084% of variation in annual returns (R² = 0.000842)
- FFO to assets explains 0.032% of variation in annual returns (R² = 0.000322)

All R² values are extremely low, indicating that these single predictors explain virtually none of the variation in REIT annual returns. This suggests that other factors—such as market sentiment, sector rotation, leverage changes, or macroeconomic conditions not captured by dividend yield, interest rates, or profitability—play dominant roles in driving returns. The low explanatory power argues strongly for a multiple regression approach that includes additional predictors or control variables

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- **Market risk (beta/systematic risk):** REITs with higher market sensitivity may exhibit different return patterns independent of dividend yield or interest rates. If high-dividend REITs also have low market betas, omitting beta would bias the dividend yield coefficient downward (more negative than true effect).
- **Leverage (debt-to-equity ratio):** Highly leveraged REITs carry greater financial risk and interest-rate sensitivity. If leverage correlates with both high dividend yields and lower returns, failing to control for it would bias the dividend slope negatively, potentially overstating the dividend effect.
- **REIT sector/type dynamics:** Different property types (apartments, offices, industrial, retail) have distinct return drivers and dividend policies. Omitting sector variables may conflate sector effects with dividend yield effects, introducing specification bias.

**Potential bias:** If omitted variables are correlated with both the X variable and ret, our slope estimates may be biased. For instance, if high-dividend REITs are systematically overvalued (negative selection), the dividend yield coefficient would be biased downward. Conversely, if omitted growth opportunities correlate with low dividends, the bias would offset the true relationship. Without multiple regression, we cannot isolate the causal or partial effects.

---

## 7. Summary and Next Steps

**Key Takeaway:**
Among the three simple regressions, dividend yield (div12m_me) is the only predictor showing a statistically significant relationship with annual returns—and it is negative, suggesting a "value trap" where high-dividend REITs underperform. Prime rates and FFO/Assets show weak relationships without statistical backing. Overall, the very low R² values indicate that none of these single predictors capture the dominant drivers of REIT returns, pointing to the need for multivariate analysis that incorporates leverage, sector, market risk, and other factors.

**What we would do next:**
- Extend to multiple regression (include two or more predictors) to isolate partial effects and reduce omitted variable bias
- Test for heteroskedasticity using Breusch-Pagan or White tests to check OLS assumption validity
- Examine whether relationships vary by time period (pre/post 2008 financial crisis) or REIT property type sector
- Include interaction terms (e.g., div12m_me × prime_rate) to assess whether interest rate sensitivity varies with leverage
- Apply robust standard errors or fixed-effects models if data have clustering by REIT or sector

---

## Reproducibility Checklist
- [x] Script runs end-to-end without errors
- [x] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [x] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [x] Report accurately reflects regression results
- [x] All interpretations are in economic units (not just statistical jargon)
