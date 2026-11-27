# Financial metric definitions

Use validated records from the [data model](data_model.md). Calculate monetary metrics in the dataset's reporting currency. Display unavailable metrics as `N/A` and retain them as null in machine-readable outputs.

| Metric | Calculation |
| --- | --- |
| Actual spend | Sum of transaction amounts in the selected period and dimensions. A covered period or budgeted group with no transactions has zero actual spend. |
| Variance amount | Actual spend minus budget for the same budgeted groups. Positive indicates overspending, negative indicates underspending, and zero indicates spending on budget. |
| Variance percentage | `(actual spend - budget) / budget × 100` for the same budgeted groups when their total budget is positive. |
| Budget utilization | `actual spend / budget × 100` for the same budgeted groups when their total budget is positive. Values above 100% indicate overspending. |
| Month-over-month change amount | Current month's actual spend minus the immediately preceding calendar month's actual spend, using the same dimension filters. |
| Month-over-month change percentage | `(current actual spend - prior actual spend) / prior actual spend × 100` when prior actual spend is positive. |

## Zero and missing values

- With an explicit zero budget, variance amount equals actual spend. Variance percentage and utilization are unavailable at that grain.
- Without a budget row, show the actual spend and mark the group unbudgeted. Budget, variance amount, variance percentage, and utilization are unavailable for that group.
- With a positive budget and no transactions, actual spend is zero, variance amount is the negative budget, variance percentage is −100%, and utilization is 0%.
- With zero prior-month spending, month-over-month amount is available and the percentage is unavailable. When the prior calendar month is outside dataset coverage, both changes are unavailable. A covered month without transactions has zero spend. A dashboard date filter may hide the prior month while the calculation still uses it.

## Calculation assumptions

- Use complete calendar months within the configured synthetic reporting window and assign actuals by transaction date. The initial model covers positive expenses. Refunds, credits, and currency conversion are outside this model.
- Aggregate actuals at the budget grain before joining. For variance rollups, sum budgets and the corresponding actuals across all budgeted groups, including zero allocations and budget-only groups. Show all actuals in the actual spend KPI and expose unbudgeted actuals separately. When no groups are budgeted, budget comparison metrics are unavailable.
- Calculate rollup percentages from summed amounts and round only for presentation. Month-over-month changes use total actual spend, including unbudgeted spending.
- Under vendor or payment method filters, display spending and spending trends. Budget comparison metrics are unavailable because allocations have neither dimension.

For example, two budgeted groups have actuals of 120 and 30 against budgets of 100 and 0. A third group has 20 in unbudgeted actuals. Total actual spend is 170. The budgeted groups contribute 150 in actuals and 100 in budget, giving a variance of 50, variance percentage of 50%, and utilization of 150%. If total prior-month actuals were 100, month-over-month change would be 70 in currency units and 70%.
