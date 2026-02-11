# Daily Log — BigQuery + SQL Refresher (Python Client + Core Clauses)
Date: 2026-02-11  
Time spent: 5 hours  
Focus: Revising core SQL clauses + learning BigQuery Python client for dataset/table fetching and previewing

---

## 1) What I learned (high level)
- BigQuery organizes data as **Project → Dataset → Table**, and tables are referenced as `project.dataset.table`.
- How to use the **BigQuery Python client** to:
  - fetch a dataset (`dataset_ref` → `get_dataset()`)
  - fetch a table (`table_ref` → `get_table()`)
  - inspect schema (`table.schema`)
  - preview rows (`list_rows(...).to_dataframe()`)
- SQL refreshers:
  - `SELECT`, `FROM`, `WHERE`
  - `COUNT()`, `GROUP BY`, `HAVING`, `AS`
  - `ORDER BY`
  - date types (`DATE`, `DATETIME`) + `EXTRACT()`
  - CTEs using `WITH`
  - joining tables using `INNER JOIN ... ON ...`

---

## 2) Key concepts / notes

### 2.1 BigQuery basics (mental model)
- BigQuery is a service that lets you run **SQL on huge datasets**.
- Each dataset lives inside a **project**.
- Table naming (fully qualified):
  - `project.dataset.table`
  - Example: `bigquery-public-data.openaq.global_air_quality`

### 2.2 BigQuery Python client workflow (dataset → table → schema → preview)
Steps:
1. Create a dataset reference using `.dataset()`
2. Fetch the dataset metadata using `get_dataset()`
3. Create a table reference using `.table()`
4. Fetch table metadata using `get_table()`
5. Inspect schema with `table.schema`
6. Preview rows with `list_rows()` → `.to_dataframe()`

Schema fields include:
- column name
- field type (datatype)
- mode (e.g., `NULLABLE`)
- description

### 2.3 Core SQL clauses (refresher)
- `SELECT`: which columns to return  
- `FROM`: where the data comes from  
- `WHERE`: row filtering (important because BigQuery tables are large)  
- `SELECT *`: selects all columns (generally avoid unless needed)

### 2.4 Aggregations and grouping
- `COUNT()` is an aggregate function (others: `SUM`, `AVG`, `MIN`, `MAX`)
- `GROUP BY` groups rows so aggregates apply per group
- `HAVING` filters **groups** after grouping (think: “if condition for grouped results”)
- `AS` aliases a computed output column name

Rule of thumb:
If you use `GROUP BY`, every selected field must be either:
- included in `GROUP BY`, or
- wrapped in an aggregate function (like `COUNT()`)

### 2.5 Ordering results
- `ORDER BY` sorts results and is usually near the end of the query.
- Common use case: sorting by counts or dates.

### 2.6 Dates in BigQuery
Two common types:
- `DATE`: `YYYY-MM-DD`
- `DATETIME`: `YYYY-MM-DD HH:MM:SS`

Use `EXTRACT()` to pull parts of a date/time (year, month, day, etc.).

### 2.7 CTEs (WITH)
- `WITH` creates a **temporary table** for use inside the query only.
- Helps keep queries readable and pushes transformation work into SQL (BigQuery is fast vs doing heavy cleaning in pandas).

### 2.8 JOINs
- JOINs combine data across multiple tables.
- `ON` defines which columns link the tables.
- Best practice: always qualify columns with table aliases (`sf.col`, `l.col`) to avoid confusion.
- `INNER JOIN` keeps only rows where the key exists in both tables.

---

## 3) Code snippets (if any)

### 3.1 Fetch dataset + table (BigQuery Python)
```python
from google.cloud import bigquery

client = bigquery.Client()

# Construct a reference to the "hacker_news" dataset
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)

# Construct a reference to the "full" table
table_ref = dataset_ref.table("full")

# API request - fetch the table
table = client.get_table(table_ref)
```

### 3.2 Preview rows + specific columns
```python
# Preview the first five lines of the "full" table
client.list_rows(table, max_results=5).to_dataframe()

# Preview the first five entries in the first column (schema[:1])
client.list_rows(table, selected_fields=table.schema[:1], max_results=5).to_dataframe()
```

### 3.3 Simple SELECT/FROM/WHERE query (OpenAQ example)
```python
from google.cloud import bigquery

client = bigquery.Client()

query = """
    SELECT city
    FROM `bigquery-public-data.openaq.global_air_quality`
    WHERE country = 'US'
"""

us_cities = client.query(query).to_dataframe()
```

### 3.4 GROUP BY + HAVING + COUNT + aliasing (Hacker News example)
```python
query = """
    SELECT parent, COUNT(id) AS NumReplies
    FROM `bigquery-public-data.hacker_news.full`
    GROUP BY parent
    HAVING COUNT(id) > 10
    ORDER BY NumReplies DESC
"""

most_discussions = client.query(query).to_dataframe()
most_discussions.head()
```

###3.5 JOIN example (GitHub repos dataset)
``` sql
SELECT
  l.license,
  COUNT(1) AS number_of_files
FROM `bigquery-public-data.github_repos.sample_files` AS sf
INNER JOIN `bigquery-public-data.github_repos.licenses` AS l
  ON sf.repo_name = l.repo_name
GROUP BY l.license
ORDER BY number_of_files DESC;
```

## 4) Exercises completed
- None today (focus was on learning + note cleanup)

### What I struggled with:
- Nothing major — mostly getting comfortable with the BigQuery Python client flow (dataset_ref → table_ref → schema → preview).

### What clicked:
- The mental model: Project → Dataset → Table + the fully-qualified table naming.
- Using list_rows(...).to_dataframe() as a quick “peek” before writing queries.

## 5) Output shipped today

 - Notes committed
 - Exercise list committed

## 6) Tomorrow plan

 - Write 5–10 SQL queries using: WHERE, GROUP BY, HAVING, ORDER BY
 - Practice one date query using EXTRACT()
 - Write one JOIN query using the GitHub repos public dataset
 - Save best queries into the sql/patterns/ folder
