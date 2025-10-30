# 🧠 Machine Learning Data Preparation with SQLite and Python

This project demonstrates a **complete workflow for preparing raw data for machine learning** using Python and SQLite.  
It includes loading a dataset, creating a database connection, storing and retrieving data from SQLite, and previewing records for further analysis or model training.

---

## 📋 Project Overview

Data preparation is a key step in any machine learning pipeline.  
This project focuses on the **data ingestion and storage stage**, where a CSV dataset is loaded, written to a local SQLite database, and queried for validation.

### 🔍 Key Objectives

- Load raw data from a CSV file using `pandas`
- Create and manage a SQLite database connection
- Store the dataset in a SQLite table
- Retrieve and preview data using SQL queries
- Prepare the environment for downstream data cleaning and model development

---

## 🏗️ Project Structure
├── db_raw.db # SQLite database file created during runtime
├── raw_data.csv # Source dataset (input)
├── main.py # Main script for data preparation
├── README.md # Project documentation (this file)
└── requirements.txt # Python dependencies (optional)

---

🧩 Code Explanation

1️⃣ Database Connection
Function: create_connection(db_file)
Establishes a connection to a SQLite database (creates it if it doesn’t exist)
Returns a connection object that can be reused across functions

---

2️⃣ Create Table from DataFrame
Function: create_table_from_df(conn, df, table_name)
Writes the contents of a pandas DataFrame to a database table
Uses if_exists='replace' by default, so the table is recreated each run (you can change to 'append')

---

3️⃣ Execute SQL Queries
Function: execute_query(conn, query)
Allows running any valid SQL command (e.g., CREATE TABLE, INSERT, UPDATE)
Commits changes automatically

---

4️⃣ Fetch Data from SQL
Function: fetch_data(conn, query)
Runs a SELECT query and fetches all results
Returns the results as a list of tuples, which can be converted to a pandas DataFrame

---

5️⃣ Main Function
Function: main()
Loads the raw CSV file
Creates a SQLite connection
Stores the data in a database table

# Verification
In the main function there is need to verify whether the data is loaded properly.
By use of sql and the script: rows= fetch_data(conn, "SELECT * FROM sample_df LIMIT 5")
This ensures we have the data we wanted.

issue- the query doesn't include table names
fix- I added (# Get column names from cursor.description
        columns = [description[0] for description in c.description]
        # Convert to DataFrame
        df = pd.DataFrame(rows, columns=columns)
        return df)
        
        
