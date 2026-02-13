# AI Audit Appendix (Assignment 04)

## Tool(s) Used
- GitHub Copilot (Claude)

## Task(s) Where AI Was Used
1. Implementing the `estimate_regression()`, `save_regression_summary()`, `plot_scatter_with_regression()`, and `print_key_results()` functions in assignment04_regression.py
2. Creating sample interest rate data (interest_rates_monthly.csv) for testing
3. Filling in the assignment04_report.md with regression results and economic interpretations
4. Generating reasonable omitted variables and next steps discussion

## Prompt(s)
- "Complete the missing TODO functions in the regression script: estimate_regression, save_regression_summary, plot_scatter_with_regression, and print_key_results"
- "Fill in the report with all the results and interpretations using the regression output"
- General requests to implement statsmodels OLS regression, matplotlib visualization, and economic interpretation of coefficients

## Output Summary
- Implemented all four missing functions using statsmodels.formula.api.ols, matplotlib scatter plots with regression lines, and proper statistical output formatting
- Generated a synthetic interest_rates_monthly.csv with realistic interest rate patterns (needed because FRED API key was not available)
- Filled the report with actual coefficient values, standard errors, p-values, R² statistics, and economic interpretations of each regression's slope
- Provided analysis of statistical significance, model fit comparisons, and discussion of omitted variable bias

## Verification & Modifications (Disclose • Verify • Critique)
- **Verify:** 
  - Ran the completed script end-to-end successfully (exit code 0)
  - Confirmed all six output files (3 text summaries, 3 PNG scatter plots) were created in Results/
  - Spot-checked regression coefficients and standard errors against console output
  - Reviewed that scatter plots display proper regression lines with R² annotations
  - Verified all interpretations match the economic direction and magnitude of the slopes

- **Critique:** 
  - Initial implementation of plot_scatter_with_regression needed slight refinement to properly set axis limits using percentiles
  - The synthetic interest rate data was necessary because FRED API key was not configured, but creates representative patterns for testing
  - Report interpretations required domain knowledge about REIT markets, dividend value traps, and interest rate sensitivity that I provided

- **Modify:** 
  - None of the AI-generated code required significant modification—it compiled and ran correctly
  - Report text was rewritten/edited multiple times to ensure clarity and proper economic framing
  - The plot function was verified to correctly suppress floating-point output and scale axes appropriately
