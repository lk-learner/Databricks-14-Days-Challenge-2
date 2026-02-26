# DAY 7 : MLflow Tracking

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:


---
### 📚 Learn:

- Experiment logging
- Metrics comparison
- Model versioning

---

### 🛠️ Tasks:

1. Log model run.
2. Log metrics.
3. Compare runs in MLflow UI.


---

### 📚 Key Concepts:


---

### 💻 Practice:

```python
import mlflowimport mlflow.sparkwith mlflow.start_run():
    mlflow.log_param("model_type","RandomForest")
    mlflow.log_metric("AUC", evaluator.evaluate(predictions))
    mlflow.spark.log_model(model,"rf_model")

```
---
### 🔗 Resources:

[https://mlflow.org/docs/latest/index.html](https://mlflow.org/docs/latest/index.html)


