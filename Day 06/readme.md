# Day 6:  Model Training & Tuning

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:



---
### 📚 Learn:

- Logistic Regression
- RandomForest
- Hyperparameter tuning



---

### 🛠️ Tasks:


1. Train Logistic model.
2. Train RandomForest.
3. Tune parameters.
4. Compare AUC.

---

### 📚 Key Concepts:





---

### 💻 Practice:

```python

from pyspark.ml.featureimport VectorAssemblerfrom pyspark.ml.classificationimport RandomForestClassifierfrom pyspark.ml.evaluationimport BinaryClassificationEvaluator

assembler = VectorAssembler(
    inputCols=["total_events","purchases","total_spent","avg_price"],
    outputCol="features"
)

data = assembler.transform(training_data) \
    .select("features","purchased")

rf = RandomForestClassifier(labelCol="purchased")
model = rf.fit(data)

predictions = model.transform(data)

evaluator = BinaryClassificationEvaluator(labelCol="purchased")print("AUC:", evaluator.evaluate(predictions))


```
---
### 🔗 Resources:

[https://spark.apache.org/docs/latest/ml-classification-regression.html](https://spark.apache.org/docs/latest/ml-classification-regression.html)
