# Project requirements

## Objectives

1. Build a reproducible workflow that generates synthetic financial data, validates it, and loads accepted records into SQLite.
2. Report spending, budget, budget utilization, and actual-minus-budget variance by month, department, and expense category.
3. Show monthly spending trends and vendor spend. Let users trace summaries back to transactions and review records flagged by documented rules.
4. Produce Excel and CSV reports whose totals reconcile with the database and dashboard for the same filters.

## Synthetic-data-only scope

Generate every transaction, budget, department, expense category, and vendor record from fictional inputs. Use only generated data in sample files, test fixtures, the database, dashboard views, screenshots, and exports. Keep all names and identifiers fictional, including when modeling realistic spending patterns.

Real financial records, personal information, bank feeds, accounting system integrations, and production deployment are outside the four-week scope. Transaction flags support manual review of synthetic examples. They carry no fraud determination. PDF export is a possible future extension.

## Assumptions and calculation rules

- Use one reporting currency and calendar months. Assign actuals to a month using the transaction date. Currency conversion and fiscal calendar adjustments are outside scope.
- Each transaction has a unique identifier, a valid date and amount, and valid department, expense category, and vendor references. Each budget row represents one month, department, and expense category. That combination must be unique.
- Aggregate transactions to the budget grain before joining budgets so multiple transactions cannot multiply a budget amount. Include periods with a budget and zero spending.
- Calculate variance as actual spending minus budget. A positive value indicates overspending, a negative value indicates underspending, and zero indicates spending on budget. Calculate variance percentage as variance divided by budget and utilization as actuals divided by budget. Calculate ratios from totals when rolling up.
- Mark percentage metrics unavailable when the budget is zero or missing. Calculate absolute variance for a zero budget. Show groups with a missing budget as unbudgeted and leave their variance unavailable. Include every budgeted group in variance rollups, using zero actuals when a budgeted group has no transactions. Show unbudgeted actuals separately.
- Report vendor spend from transactions. Vendor-level variance is outside scope because budgets have no vendor dimension.
- Use a configurable random seed for repeatable datasets and include examples of overspending, underspending, zero budgets, and missing budgets.

## Acceptance criteria

- With the same seed and configuration, generation produces the same input records. Validation identifies duplicate keys, malformed records, and invalid references before loading and reports rejected rows with reasons.
- Variance checks cover over-budget, under-budget, on-budget, zero-budget, and missing-budget cases. Budget-only groups remain visible, and transaction totals reconcile after aggregation.
- Dashboard filters refresh relevant metrics and transaction details. Excel and CSV exports reconcile with the same filtered database results.
