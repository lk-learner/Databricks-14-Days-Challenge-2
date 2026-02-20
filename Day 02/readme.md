# Day 2: Feature Table (Silver Layer Thinking)

## Databricks 14-Day AI Challenge
---
### 🚀 Overview

Day 2 focuses on the transition from the Bronze Layer (raw data) to the Silver Layer (refined data). In an AI/ML context, this is where "Feature Engineering" begins. The objective is to take raw event logs (like clicks and purchases) and transform them into a User-Level Feature Table—a structured dataset where each row represents a unique user with summarized behavioral metrics.

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
### 📚 Key Concepts




---

### 📝 Practice

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
