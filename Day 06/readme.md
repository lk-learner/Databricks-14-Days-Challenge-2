# Day 6:  Model Training & Tuning

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:

Day 6 is designed to teach you how to build and evaluate classification models at scale. The curriculum focuses on predicting binary outcomes (e.g., "Will a user purchase?") using two popular algorithms: Logistic Regression (a statistical baseline) and Random Forest (a robust ensemble method). The session also introduces the critical step of Hyperparameter Tuning, where you move beyond default settings to optimize model performance.

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

**1. Logistic Regression**

Definition: A fundamental classification algorithm used to predict the probability of a binary outcome (1 or 0, True or False).

Role in Spark ML: It uses the sigmoid function to map feature inputs to a probability between 0 and 1. In Databricks, LogisticRegression is often the first baseline model tested due to its simplicity and interpretability.

**2. Random Forest (Ensemble Learning)**

Definition: An ensemble method that builds multiple decision trees and merges them together to get a more accurate and stable prediction.

Strength: It is less prone to overfitting than a single decision tree and handles non-linear relationships and missing data well. In the practice code, RandomForestClassifier is used to capture complex patterns in user behavior data.

**3. Hyperparameter Tuning**

The Concept: While models have default settings (like the number of trees in a forest), tuning involves testing different combinations of these "hyperparameters" to find the best-performing version.

Implementation: In PySpark, this is typically handled using a ParamGridBuilder (to define the search space) and CrossValidator (to test each combination against different subsets of the data).

**4. Feature Engineering with VectorAssembler**

Requirement: Spark ML algorithms require all input features to be combined into a single vector column (usually named features).

Practice: The VectorAssembler takes individual columns like total_events and purchases and merges them into this required format before the model can be "fit" to the data.

**5. Model Evaluation (AUC)**

Metric: The Area Under the ROC Curve (AUC) is the primary metric used here. It measures the model's ability to distinguish between classes.

Interpretation: An AUC of 1.0 represents a perfect model, while 0.5 represents a model no better than random guessing. Comparing AUC scores is how you decide whether Logistic Regression or Random Forest is better for your specific dataset.



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
