# Data dictionary

All fields below are required. Identifiers are stable text codes and comparisons use the codes. Display names and descriptions are fictional. The [data model](data_model.md) defines how the datasets relate.

## Transactions

| Field | Type | Definition and validation | Example |
| --- | --- | --- | --- |
| `transaction_id` | Text | Unique, nonblank expense identifier | `TXN-0001` |
| `transaction_date` | Date | Valid calendar date in `YYYY-MM-DD` format. Determines the reporting month. | `2026-01-15` |
| `department_id` | Text | Code in the departments reference dataset | `OPS` |
| `category_id` | Text | Code in the expense categories reference dataset | `SOFTWARE` |
| `vendor_id` | Text | Code in the vendors reference dataset | `V001` |
| `description` | Text | Nonblank fictional description of the expense | Monthly dispatch software subscription |
| `amount` | Decimal | Positive expense in reporting currency with up to two decimal places | `125.50` |
| `payment_method` | Text | Code from the controlled payment method list | `CARD` |

## Monthly budgets

| Field | Type | Definition and validation | Example |
| --- | --- | --- | --- |
| `month` | Date | First day of the calendar month in `YYYY-MM-DD` format | `2026-01-01` |
| `department_id` | Text | Code in the departments reference dataset | `OPS` |
| `category_id` | Text | Code in the expense categories reference dataset | `SOFTWARE` |
| `budget_amount` | Decimal | Nonnegative monthly allocation in reporting currency with up to two decimal places | `150.00` |

The combination of month, department, and category is unique. An explicit zero means a zero allocation. An absent row means the group is unbudgeted.

## Synthetic reference values

These are starter values for the synthetic dataset. Each reference dataset pairs its unique code with a required display name.

| Reference dataset | Fields | Starter values |
| --- | --- | --- |
| Departments | `department_id`, `department_name` | `OPS` Operations, `FIN` Finance, `ENG` Engineering, `MKT` Marketing |
| Expense categories | `category_id`, `category_name` | `SOFTWARE` Software, `SUPPLIES` Office supplies, `TRAVEL` Travel, `SERVICES` Professional services |
| Vendors | `vendor_id`, `vendor_name` | `V001` Example Dispatch Systems, `V002` Example Paper Supply, `V003` Example Travel Desk, `V004` Example Advisory Studio |
| Payment methods | `payment_method`, `payment_method_name` | `CARD` Corporate card, `TRANSFER` Bank transfer, `CHECK` Check, `CASH` Cash |
