# DAY 10 : Query Optimization & Explain Plans

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:



---
### 📚 Learn:

- .explain()
- Partition pruning
- Caching

---

### 🛠️ Tasks:

1. Run heavy query.
2. Analyze explain plan.
3. Enable caching.
4. Compare execution time.

---

### 📚 Key Concepts:





---
### 💻 Practice:

```python

spark.sql("SELECT * FROM events_delta WHERE event_type='purchase'").explain(True)

spark.table("events_delta").cache().count()

```
---
### 🔗 Resources:

[https://docs.databricks.com/performance/](https://docs.databricks.com/performance/)


