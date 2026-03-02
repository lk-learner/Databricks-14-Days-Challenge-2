# DAY 11 : Time Travel & Data Recovery

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

Day 11 focuses on one of the most powerful features of Delta Lake: the ability to travel back in time to previous versions of your data. In traditional databases, once data is overwritten or deleted, it is often gone unless you have a backup. In Databricks, every transaction is logged, allowing you to query, compare, and restore data as it existed at any specific point in time or version number.

---
### 📚 Learn:

- Versioning
- Rollback
- Data recovery

---

### 🛠️ Tasks:

1. Append new records.
2. Query older version.
3. Compare differences.
---

### 📚 Key Concepts:

**1. Delta Versioning (The Transaction Log)**

Every time you perform an action on a Delta table (Insert, Update, Delete, or Merge), Databricks creates a new version of the table.

Version 0: The initial creation of the table.

Version 1, 2, 3...: Subsequent changes.

Mechanism: This is powered by the _delta_log folder, which stores JSON files tracking exactly which data files were added or removed during each transaction.

**2. Time Travel (Querying Older Data)**

Time travel allows you to see how your data looked in the past without restoring the entire database. There are two ways to do this:

Version As Of: Querying by a specific version number (e.g., "Show me the data at Version 0").

Timestamp As Of: Querying by a specific date and time (e.g., "Show me the data as it was at 10:00 AM yesterday").

**3. Data Recovery & Rollback**

If a "bad" write occurs (e.g., someone accidentally deletes all records or appends corrupt data), Day 11 covers how to recover:

RESTORE: You can use the RESTORE TABLE TO VERSION AS OF X command to instantly revert your table to a healthy state.

Manual Recovery: You can read an old version and overwrite the current table with that "clean" data.

**4. Comparing Differences**

By querying two different versions of the same table (e.g., Version 5 and Version 10), you can perform a Delta Comparison. This is essential for:

Identifying what changed during a specific ETL (Extract, Transform, Load) run.

Auditing who changed what data and when.

**Understanding the Practice Task**

The code snippet provided in the challenge:

**.option("versionAsOf", 0):** This is the "Time Travel" trigger. It tells Spark to ignore the current state of the table and specifically fetch the data exactly as it was when the table was first created (Version 0).

**.load("/delta/events"):** Points to the storage location of your table.

**Summary of Tasks for Day 11:**

Append: Add new data to see the version number increment.

Query: Use the versionAsOf option to "look back" at the table before the append happened.

Compare: Join or subtract the old version from the new version to isolate the newly added records.


---
### 💻 Practice:

```python
spark.read.format("delta") \
    .option("versionAsOf",0) \
    .load("/delta/events") \
    .show()


```
---
### 🔗 Resources:

[https://docs.databricks.com/performance/](https://docs.databricks.com/performance/)


