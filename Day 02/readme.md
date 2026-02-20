# Day 2: Feature Table (Silver Layer Thinking)

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:

Day 2 focuses on the transition from the Bronze Layer (raw data) to the Silver Layer (refined data). In an AI/ML context, this is where "Feature Engineering" begins. The objective is to take raw event logs (like clicks and purchases) and transform them into a User-Level Feature Table , a structured dataset where each row represents a unique user with summarized behavioral metrics.

---

### 📚 Learn:

- Bronze → Silver → Gold
- Feature engineering in production
- Clean user-level aggregation

---

### 🛠️ Tasks:

1. Create user-level feature table.
2. Save it as Delta (Silver layer).
3. Ensure no duplicates.
4. Validate feature quality.

---
### 📚 Key Concepts:

1. The Medallion Architecture (Bronze → Silver)
   
Bronze: Raw data landing zone (often messy, includes duplicates).

Silver: The "Source of Truth" for features. Data here is cleaned, joined, and aggregated. For AI models, the Silver layer often acts as the Feature Store source.

2. Silver Layer Thinking
   
Moving to the Silver layer isn't just about moving data; it's about making it business-ready.

User-Level Aggregation: Instead of looking at individual events, you group data by user_id to understand behavior over time.

Dimensionality Reduction: Turning thousands of raw log rows into a few meaningful columns (e.g., total_spent).

3. Feature Engineering in Production
   
The practice code demonstrates how to programmatically create features:

Frequency: total_events (How active is the user?)

Monetary: total_spent (What is their value?)

Behavioral Ratio: purchases (Do they convert?)

Averages: avg_price (What is their price point preference?)

4. Delta Lake Fundamentals
   
The challenge emphasizes saving data in Delta format. Key technical takeaways include:

format("delta"): Ensuring the data has ACID transactions and schema enforcement.

mode("overwrite"): Refreshing the feature table with the latest calculations.

Data Quality: Ensuring "no duplicates" is critical; in a real-world Silver layer, you would often use MERGE INTO (Upsert) to update existing users rather than just overwriting.

Breakdown of the Practice Code

The provided script uses PySpark to perform the transformation:

Grouping: groupBy("user_id") collapses the raw logs into unique users.

Conditional Aggregation: F.when(F.col("event_type")=="purchase",1) is a standard way to create a counter for specific behaviors within an aggregate function.

Storage: Writing to /delta/silver/user_features establishes the organized directory structure required for professional data engineering.

Why this matters for AI

A machine learning model cannot "read" a list of 1 million raw clicks. It requires a fixed-length vector of numbers. By creating this Silver layer feature table, you are preparing the exact input needed for a Propensity Model (predicting if someone will buy) or a Churn Model (predicting if someone will leave).


---

### 📝 Practice:

```python
from pyspark.sqlimport functionsas F

features_df = events.groupBy("user_id").agg(
    F.count("*").alias("total_events"),
    F.count(F.when(F.col("event_type")=="purchase",1)).alias("purchases"),
    F.sum("price").alias("total_spent"),
    F.avg("price").alias("avg_price")
)

features_df.write.format("delta").mode("overwrite") \
    .save("/delta/silver/user_features")
```
---
### 🔗 Resources:

https://www.databricks.com/glossary/medallion-architecture
