
### Learn:

- Bronze → Silver → Gold
- Feature engineering in production
- Clean user-level aggregation

### 🛠️ Tasks:

1. Create user-level feature table.
2. Save it as Delta (Silver layer).
3. Ensure no duplicates.
4. Validate feature quality.

![2.png](attachment:37fb9329-c9ac-47b1-82c0-db4705aba7db:2.png)

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

### 🔗 Resources:

https://www.databricks.com/glossary/medallion-architecture
