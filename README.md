# 🚀 CSV to SQLite3 ETL Pipeline

A simple **ETL (Extract, Transform, Load)** project built with **Python**, **Pandas**, and **SQLite3**.  
It reads data from a CSV file, applies optional transformations, and loads it into an SQLite database — either **in-memory** or saved as a `.db` file.

---

## 🧠 Project Overview

This project demonstrates a basic data engineering workflow:

1. **Extract** – Read structured data from a CSV file using `pandas.read_csv()`.
2. **Transform** – Clean, filter, or reshape data (optional).
3. **Load** – Store the transformed data in an **SQLite3** database using `sqlite3` and `pandas.to_sql()`.

---

## ⚙️ Features

- ✅ Read CSV files into Pandas DataFrames  
- ✅ Load data into SQLite3 (in-memory or local `.db` file)  
- ✅ Logging for better ETL tracking  
- ✅ Simple, extendable architecture for learning or prototyping  
- ✅ Compatible with Python 3.8+  

---

## 🧩 Example Code

```python
import pandas as pd
import sqlite3
import logging

logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")

def extract_csv(file_path: str) -> pd.DataFrame:
    logging.info(f"Extracting data from {file_path}")
    return pd.read_csv(file_path)

def load_to_sqlite(df: pd.DataFrame, table_name: str, db_path=":memory:"):
    logging.info(f"Loading DataFrame into SQLite ({db_path}), table: {table_name}")
    with sqlite3.connect(db_path) as conn:
        df.to_sql(table_name, conn, if_exists='replace', index=False)
        logging.info("Data successfully loaded into SQLite database.")

if __name__ == "__main__":
    file_path = "data/sample.csv"
    df = extract_csv(file_path)
    load_to_sqlite(df, table_name="dataset")
