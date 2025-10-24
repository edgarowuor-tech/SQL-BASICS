# Copilot Instructions for SQL Data Science Workspace

## Overview
This workspace is focused on interactive data analysis using SQLite databases and Jupyter notebooks. The main workflow involves querying local SQLite databases (`data.sqlite`, `pets_database.db`) using Python (with `sqlite3` and `pandas`) inside `index.ipynb`.

## Key Files and Structure
- `index.ipynb`: Main notebook for all data exploration and SQL queries. All code and analysis should be added here unless otherwise specified.
- `data.sqlite`, `pets_database.db`: SQLite database files. Use these as the primary data sources for queries.

## Patterns and Conventions
- **Database Connections**: Use `sqlite3.connect('<db_file>')` to connect. Always close connections with `conn.close()` when done.
- **Querying Data**: Prefer `pandas.read_sql()` for running SQL queries and loading results into DataFrames for further analysis.
- **Notebook Cells**: Each logical step (connect, query, transform, visualize) should be in its own cell. Add markdown cells to explain the purpose of each code block.
- **Reconnecting**: If a connection is closed, reconnect using the same pattern. Example:
  ```python
  conn = sqlite3.connect('data.sqlite')
  ```
- **Table Discovery**: To list tables, use:
  ```python
  pd.read_sql("SELECT name FROM sqlite_master WHERE type='table';", conn)
  ```
- **Column Discovery**: Use cursor `.description` after a query to inspect column names.
- **SQL Style**: Use triple-quoted strings for multi-line SQL. Use aliases and SQL functions as needed.

## Example Workflow
```python
import sqlite3
import pandas as pd
conn = sqlite3.connect('data.sqlite')
df = pd.read_sql("SELECT * FROM employees;", conn)
df.head()
conn.close()
```

## Testing and Validation
- There are no automated tests. Validate queries by inspecting DataFrame outputs in the notebook.

## External Dependencies
- Only standard Python libraries (`sqlite3`, `pandas`) are used. Install additional packages via notebook cells if needed.

## Special Notes
- If working with a different database file, update the connection string accordingly.
- If you add new notebooks or scripts, follow the same connection/query patterns as in `index.ipynb`.

---

For questions or unclear patterns, review `index.ipynb` for examples or ask for clarification.