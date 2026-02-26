# DAY 7 : MLflow Tracking

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

Day 7 focuses on the transition from "writing code" to "managing experiments." In a professional environment, data scientists run hundreds of iterations of a model with different settings. Without a tracking system, it is impossible to remember which settings produced the best results.

MLflow Tracking acts as a "digital lab notebook." It automatically records everything about your training process, parameters, performance metrics, and the model files themselves—so you can review, share, and deploy them later.

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

**1. Experiment Logging**

This is the process of recording the "metadata" of your machine learning run. Every time you train a model, you wrap your code in an MLflow "run."

Parameters: These are the inputs to your model (e.g., learning_rate=0.01, n_estimators=100). In the practice code, model_type is logged as a parameter.

Tags: Used to categorize runs (e.g., env: production or user: data_scientist_A).

**2. Metrics Comparison**

Metrics are the quantitative results of your model.

Logging Metrics: Using mlflow.log_metric(), you save performance values like AUC (Area Under Curve), Accuracy, or RMSE.

Comparison: Once you have multiple runs, the MLflow UI allows you to select them and view a side-by-side comparison. You can generate parallel coordinates plots or scatter plots to see how changing a parameter (like depth of a tree) affected the metric (like AUC).

**3. Model Versioning & Artifacts**

Instead of just saving a .pkl or .save file locally, you use mlflow.spark.log_model() (or mlflow.sklearn.log_model()).

Artifacts: This stores the actual model object, dependencies, and environment files in a centralized location.

Reproducibility: Because the model is logged with the exact parameters and code version used to create it, anyone on your team can recreate the exact same model later.

**4. The MLflow UI in Databricks**

Databricks has a built-in MLflow sidebar. Key features explored today include:

Run History: A list of every execution.

Search/Filter: Finding the "best" model by searching for the run with the highest AUC.

Model Registry Prep: Logging a model is the first step toward "registering" it for production use.

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


