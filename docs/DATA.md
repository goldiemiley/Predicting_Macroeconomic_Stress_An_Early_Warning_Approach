# Data in Brief

This project examines country-year observations from the **World Bank World Development Indicators (WDI)**, queried through Google BigQuery and processed in Google Colab. The application area is macroeconomic risk monitoring, focusing on rule-defined warning signals of high inflation, unemployment, output contraction, external imbalance, and currency depreciation.

The submitted report describes **5,423 observations, 20 columns, and calendar years 1995–2020**. Each row represents a country-year. No raw dataset is bundled in this public repository.

## Variables

- Identifiers: `country_name`, `country_code`, `year`.
- Raw macroeconomic indicators: `gdp_growth_pct`, `gdp_per_capita_current_usd`, `inflation_pct`, `unemployment_pct`, `current_account_pct_gdp`, `exports_pct_gdp`, `imports_pct_gdp`, `trade_pct_gdp`, `fdi_net_inflows_pct_gdp`, `exchange_rate_lcu_per_usd`, `population`.
- Engineered: `misery_index` (inflation + unemployment), `trade_balance_proxy` (exports − imports as % GDP), `growth_inflation_gap` (GDP growth − inflation), `external_pressure_score` (current account + FDI as % GDP), `exchange_rate_change_pct` (annual local-currency-per-USD change).
- Binary output: `economic_stress`.

## Stress label as described in submitted report

Stress=1 if any indicator crosses: GDP growth < 0%, inflation > 10%, unemployment > 10%, current account < −5% of GDP, exchange-rate depreciation > 20%. The precise original source SQL and treatment of missing values must be verified before changing the label definition; the notebook separately reconstructs these five rules for comparison.

## Missingness reported in source project

| Indicator | Missing (%) |
|---|---:|
| Exchange-rate change | 31.96 |
| External-pressure score | 29.47 |
| Current account | 29.39 |
| Exchange-rate level | 29.34 |
| Trade indicators | Approximately 6–7 |

GDP growth, GDP per capita, inflation, unemployment, population, and the target were reported complete. The original model used median imputation within scikit-learn pipelines. The new notebook performs imputation within the training pipeline to avoid learning test-set medians.

These values are reported from the submitted PDF, not independently regenerated from a connected data table. WDI statistical aggregates (regions/income group totals) should be excluded if present, and unique country-year keys checked.
