# DAY 8 : Batch Inference Pipeline

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

---
### 📚 Learn:

- Production scoring
- Saving predictions
- Gold layer creation

---

### 🛠️ Tasks:

1. Score all users.
2. Save predictions to Gold Delta table.
3. Identify top predicted buyers.
---

### 📚 Key Concepts:


---
### 💻 Practice:

```python

predictions.write.format("delta").mode("overwrite") \
    .save("/delta/gold/predictions")

```
---
### 🔗 Resources:

[https://docs.databricks.com/delta/](https://docs.databricks.com/delta/)


