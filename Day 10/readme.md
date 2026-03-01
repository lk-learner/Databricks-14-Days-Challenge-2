# DAY 10 : Query Optimization & Explain Plans

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

The primary focus of Day 10 is Performance Tuning. In previous days, the focus was likely on how to process and move data; today is about understanding how Spark executes those commands and how to make them run faster and cheaper.

The goal is to transition from a developer who just writes code to one who can diagnose bottlenecks using Explain Plans and optimize execution using Caching and Partitioning.


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

**1. The .explain() Method**

Before Spark runs a query, it creates a "Plan" (a series of steps). Using .explain(True) allows you to see the "Logical" vs. the "Physical" plan.

Why it matters: It reveals if Spark is doing something inefficient, like a "Broadcast Hash Join" vs. a "Sort Merge Join," or if it is scanning too much data.

Practice Tip: In the code spark.sql("...").explain(True), look for the "Physical Plan" at the bottom. This is what Spark actually executes on the cluster.

**2. Partition Pruning**

This is one of the most effective ways to speed up queries.

How it works: If your data is partitioned by a column (e.g., date or event_type), and you write a WHERE clause filtering for a specific value, Spark will "prune" (skip) the files and folders that don't match that filter.

The Benefit: Instead of scanning 1 Terabyte of data, Spark might only scan 1 Gigabyte, drastically reducing I/O and execution time.

**3. Caching (.cache())**

Caching stores a DataFrame or Table in the memory (RAM) of the cluster's worker nodes.

When to use it: Use caching when you plan to use the same DataFrame multiple times later in your script (e.g., you filter a base table and then perform five different aggregations on it).

The "Lazy" Rule: Caching is lazy. As seen in the practice code spark.table("events_delta").cache().count(), the .cache() command doesn't actually store the data until an Action (like .count()) is called.

Comparison: On the first run (the .count()), Spark reads from disk and stores in memory. On the second run, Spark pulls directly from memory, which is usually 10x–100x faster.



---
### 💻 Practice:

```python

spark.sql("SELECT * FROM events_delta WHERE event_type='purchase'").explain(True)

spark.table("events_delta").cache().count()

```
---
### 🔗 Resources:

[https://docs.databricks.com/performance/](https://docs.databricks.com/performance/)


