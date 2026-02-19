# Day 1: Delta Conversion & Optimization

## Databricks 14-Day AI Challenge
---
### 🚀 Overview

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
