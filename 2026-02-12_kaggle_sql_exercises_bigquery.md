# Daily Log — Kaggle SQL Exercises (BigQuery)
Date: 2026-02-12  
Time spent: 5 hours  
Focus: Completed Kaggle SQL exercises using BigQuery (Python client + core SQL clauses)

---

## 1) What I learned (high level)
- Practiced BigQuery basics and table naming: `project.dataset.table` (with backticks).
- Got more comfortable using the BigQuery Python client to preview tables and run queries into pandas DataFrames.
- Refreshed and applied core SQL clauses through Kaggle exercises:
  - `SELECT`, `FROM`, `WHERE`
  - `COUNT()`, `GROUP BY`, `HAVING`, `AS`
  - `ORDER BY`
  - `WITH` (CTEs)
  - `INNER JOIN ... ON ...`
  - `EXTRACT()` for date/time breakdowns (year/month/hour)

---

## 2) Key concepts / notes

### 2.1 BigQuery + Python workflow (new skill in progress)
- BigQuery flow I used repeatedly:
  - `dataset_ref = client.dataset("...", project="bigquery-public-data")`
  - `dataset = client.get_dataset(dataset_ref)`
  - `table_ref = dataset_ref.table("...")`
  - `table = client.get_table(table_ref)`
  - `client.list_rows(table, max_results=5).to_dataframe()` to preview
  - `client.query(query).to_dataframe()` to run SQL into pandas
- BigQuery safety tip used in Kaggle: `QueryJobConfig(maximum_bytes_billed=...)` to avoid expensive queries.

### 2.2 SQL clauses practiced today (what each is for)
- `WHERE` filters rows early (important in large datasets).
- `GROUP BY` groups rows so aggregates can be computed per group.
- `HAVING` filters groups after aggregation (vs WHERE filters rows before grouping).
- `AS` renames output columns (cleaner results for analysis/dashboarding).
- `ORDER BY` sorts results (common for ranking/Top-N).
- `EXTRACT()` helps group by time parts (year/month/hour).
- `WITH` (CTE) makes multi-step queries readable (clean/filtered subset → final aggregation).
- `INNER JOIN` combines tables on matching keys (answers.parent_id = questions.id pattern).

---

## 3) Code snippets (if any)
``` python
from google.cloud import bigquery
client = bigquery.Client()

# Run query -> DataFrame
query = """
SELECT city
FROM `bigquery-public-data.openaq.global_air_quality`
WHERE country = 'US'
"""
df = client.query(query).to_dataframe()
```

---

## 4) Exercises completed

File(s):
- [Exercise 001 — Getting Started with SQL + BigQuery](https://github.com/arthur-gaudio/sql/blob/main/exercises/001_getting_started_bigquery.md)
- [Exercise 002 — SELECT / FROM / WHERE](https://github.com/arthur-gaudio/sql/blob/main/exercises/002_select_from_where.md)
- [Exercise 003 — GROUP BY / HAVING / COUNT](https://github.com/arthur-gaudio/sql/blob/main/exercises/003_group_by_having_count.md)
- [Exercise 004 — ORDER BY](https://github.com/arthur-gaudio/sql/blob/main/exercises/004_order_by.md)
- [Exercise 005 — AS + WITH (CTEs) + EXTRACT](https://github.com/arthur-gaudio/sql/blob/main/exercises/005_as_with_cte.md)
- [Exercise 006 — JOINing Data](https://github.com/arthur-gaudio/sql/blob/main/exercises/006_joining_data.md)

## What I struggled with:
- Keeping longer queries organized (especially CTEs with multiple filters and calculated fields).
- Remembering HAVING vs WHERE quickly (HAVING filters grouped results).

##What clicked:
- BigQuery table naming + backticks: project.dataset.table.
- EXTRACT() for time breakdowns (year/month/hour) in aggregation queries.
- JOIN logic and the importance of table aliases for readability.

---

## 5) Output shipped today
- Notes committed
- Exercises committed

---

## 6) Tomorrow plan
- Check sql/patterns/ files for WHERE, GROUP BY/HAVING, DATES/EXTRACT, CTEs, JOIN templates (if there are any updates)
- Start next SQL course in Kaggle and keep learning
