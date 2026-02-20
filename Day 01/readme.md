# Day 1: Delta Conversion & Optimization

## Databricks 14-Day AI Challenge
---
### 🚀 Overview

The goal of Day 1 is to move away from legacy file formats (like CSV) and adopt Delta Lake, the optimized storage layer of a Databricks Lakehouse. You will learn how to transform raw data into a high-performance format, understand common performance pitfalls (like the "Small File Problem"), and use built-in Databricks commands to keep your data organized and fast.


---
### 📚 Learn:
- Delta vs Parquet
- Small file problem
- OPTIMIZE
- Basic performance thinking

---

### 🛠️ Tasks:

1. Convert raw CSV to Delta format.
2. Create a managed Delta table.
3. Append data multiple times (simulate small files).
4. Apply OPTIMIZE and observe improvement.

---

### 📚 Key Concepts


1. Delta vs. Parquet
   
While Delta Lake is built on top of Parquet files, it adds a Transaction Log (the _delta_log folder).

Parquet: A columnar storage format that is great for reads but lacks ACID transactions. If a write fails halfway, you might end up with corrupted or partial data.

Delta: Adds "Intelligence" to Parquet. It supports ACID transactions (all or nothing writes), Schema Enforcement (prevents bad data from entering), and Time Travel (allows you to query older versions of data).

2. The "Small File Problem"
   
This is a common performance killer in Big Data.

The Cause: In Spark, every time you "Append" data or run a streaming job that writes every few seconds, Spark creates many tiny files (e.g., 1KB each).

The Problem: When you try to read this data, the system spends more time "opening and closing" thousands of tiny files than actually reading the data. This creates massive overhead and slows down your queries.

3. The OPTIMIZE Command
   
This is the "Defragmentation" for your data lake.

The OPTIMIZE command performs Compaction. It takes all those thousands of tiny files and merges them into a few large, optimally sized files (typically around 1GB).

Result: Faster read performance and better resource utilization.

4. Managed vs. Unmanaged (External) Tables
   
The practice task mentions creating a Managed Table.

Managed: Databricks manages both the data and the metadata. If you DROP TABLE, the data on the disk is deleted too.

External/Unmanaged: You point the table to a specific location (S3/ADLS). If you DROP TABLE, only the table definition in the catalog is removed; your files remain safe.

Breakdown of Practice Tasks
Convert CSV to Delta: You take unstructured/semi-structured CSVs and save them as Delta. This instantly gives the data a schema and transaction support.

Simulate Small Files: By looping 3 times and appending small chunks of data (limit(500)), you are intentionally creating a "messy" table with too many files.

Apply OPTIMIZE: After the table gets slow due to the small files, you run OPTIMIZE. You would notice (in a real environment) that the file count decreases and the "Time Taken" for subsequent queries drops significantly.

Pro-Tip for Day 1

When running OPTIMIZE, you can also use ZORDER BY (column_name). This not only merges files but also sorts the data within them, making filters on that specific column extremely fast (Data Skipping).

---

### 💻 Practice
```python
# Convert to Delta
events.write.format("delta").mode("overwrite").save("/delta/events")# Create table
spark.sql("""
CREATE TABLE events_delta
USING DELTA
LOCATION '/delta/events'
""")# Simulate small file problemfor iinrange(3):
    events.limit(500).write.format("delta").mode("append").save("/delta/events")# Optimize
spark.sql("OPTIMIZE events_delta")

```
---
### 🔗 Resources:

https://docs.databricks.com/delta/
