# Financial Expense and Budget Variance Analysis

This project demonstrates how a finance team can compare monthly spending with approved budgets, identify the departments and expense categories driving variances, and review the transactions behind those differences. The repository currently contains the project plan and dependency list. The pipeline, dashboard, and reports are planned deliverables.

## Scope

- Generate and validate synthetic transactions, monthly budgets, departments, expense categories, and vendors.
- Load validated records into SQLite and calculate monthly spending, budget utilization, and variance by department and category.
- Explore spending trends, vendor totals, and flagged transactions in a Streamlit dashboard.
- Export reconciled summaries and transaction details to Excel and CSV.

All inputs and outputs use synthetic data. See [project requirements](docs/requirements.md) for the data boundary, calculation rules, and acceptance criteria.

## Technology stack

| Technology | Planned use |
| --- | --- |
| Python, pandas, NumPy | Generate data, validate inputs, and calculate metrics |
| SQLite and SQL | Store validated records and query analytical summaries |
| Streamlit and Plotly | Build the dashboard and interactive charts |
| openpyxl | Create formatted Excel reports |
| pytest | Verify metric calculations, pipeline behavior, and reporting |

## Four-week roadmap

| Week | Deliverable |
| --- | --- |
| 1 | Define schemas and validation rules. Generate repeatable synthetic datasets and create the SQLite schema. |
| 2 | Load validated data and build monthly, department, category, and vendor analyses. Reconcile spending and budgets to source totals. |
| 3 | Build the dashboard with filters, trend and variance charts, vendor summaries, and transaction review. |
| 4 | Produce Excel and CSV exports, verify dashboard and report totals against the database, and document how to run the workflow. |
