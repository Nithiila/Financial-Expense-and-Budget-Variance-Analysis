# Data model

The model uses fictional transactions, monthly budgets, and reference values. See the [data dictionary](data_dictionary.md) for field constraints and the [metric definitions](metric_definitions.md) for aggregation rules.

| Entity | Grain | Key |
| --- | --- | --- |
| Transactions | One posted synthetic expense | `transaction_id` |
| Monthly budgets | One allocation per calendar month, department, and category | `(month, department_id, category_id)` |
| Departments | One synthetic organizational unit | `department_id` |
| Expense categories | One synthetic expense classification | `category_id` |
| Vendors | One fictional supplier | `vendor_id` |
| Payment methods | One controlled payment method | `payment_method` |

Transactions reference one department, category, vendor, and payment method. Budgets reference one department and category. Each reference value can appear in many transactions or, where applicable, many budget rows. Keep identifiers stable across datasets and reject unknown references and duplicate keys during validation.

Derive the transaction's month from its date. Aggregate actuals by month, department, and category before combining them with budgets. Preserve the union of transaction and budget groups so budget-only and unbudgeted spending remain visible. Vendor and payment method support spending analysis at transaction grain. Budget comparisons use the dimensions present in the budget.

Store and calculate monetary values in integer minor units to preserve exact totals. CSV inputs express amounts in major units with up to two decimal places. Use one reporting currency with two decimal places throughout a dataset.
