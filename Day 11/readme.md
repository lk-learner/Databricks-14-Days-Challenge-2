# DAY 11 : Time Travel & Data Recovery

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:



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


