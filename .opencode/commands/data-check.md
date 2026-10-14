---
description: "Profile a dataset and propose validation checks before it is used downstream."
---

When invoked with a dataset (file path, table or dataframe) and optionally its purpose:

1. Load it read-only with explicit dtypes where known. Do not modify the source.
2. Profile it: row and column counts, dtypes, null counts per column, duplicate rows, duplicates on the intended key, min and max for numeric and date columns, distinct counts for categorical columns.
3. Look for problems: mixed types in a column, impossible values (negative ages, future dates), inconsistent categories (case, whitespace), orphan foreign keys, and sudden shifts if there are several time periods.
4. Propose concrete validation checks for the issues found, written in whichever tool the project already uses (pandera, Great Expectations, dbt tests, plain asserts). If none is used, propose plain pytest checks.
5. Say which checks should fail the pipeline and which should only warn.
6. Summarise findings in a short table. Write checks to files only if the user agrees.
