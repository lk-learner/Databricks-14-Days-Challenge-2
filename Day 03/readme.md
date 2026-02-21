# Day 3:  Job Orchestration Basics

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:



---
### 📚 Learn:

- Parameterized notebooks
- Jobs vs notebooks
- Basic scheduling

---

### 🛠️ Tasks:

1. Add widget parameter to notebook.
2. Modularize feature creation logic.
3. Create a Job in UI.
4. Schedule daily run.

---

### 📚 Key Concepts:





---

### 💻 Practice:
```python
dbutils.widgets.text("layer","silver")
layer = dbutils.widgets.get("layer")print("Running layer:", layer)

```
---
### 🔗 Resources:
[https://docs.databricks.com/jobs/](https://docs.databricks.com/jobs/)

