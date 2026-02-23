# Day 5:  Production-Grade Feature Engineering

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:

Day 5 shifts the focus from simple data cleaning to Supervised Learning preparation. In a production environment, data doesn't come with "labels" (the answers) pre-attached. This day teaches you how to programmatically define a "Target" (what you want to predict), link it to the features you created on previous days, and prepare a statistically sound environment for training and testing a model.

The ultimate goal is to create a Training Dataset that accurately reflects a business problem.

---
### 📚 Learn:

- Target creation
- Feature selection
- Handling imbalance


---

### 🛠️ Tasks:

1. Create binary purchase label.
2. Join with feature table.
3. Split train/test.
4. Validate distribution.
---

### 📚 Key Concepts:

**1. Target (Label) Engineering**

In many real-world scenarios, you only have raw event logs (clicks, views, adds-to-cart). To train a model, you must create a Binary Label (1 or 0).

Concept: Using conditional logic (F.when) and aggregation (F.max) to determine if a user performed a specific action within a timeframe.

Why it's Production-Grade: In production, this logic must be consistent. If your labeling logic changes, your model’s entire meaning changes.

**2. Feature-Label Integration (The Join)**

Features (user behavior) and Labels (the outcome) often live in different tables.

Concept: Joining the features_df (input variables) with the label_df (the answer) using a unique identifier like user_id.

The Challenge: Ensuring no "Data Leakage." You must ensure that the features you use were generated before the purchase happened, otherwise, the model is "cheating" by looking into the future.

**3. Deterministic Data Splitting**

To evaluate a model fairly, you must hide some data from it during training (the Test set).

Concept: Using randomSplit([0.8, 0.2], seed=42).

The "Seed": The seed parameter is critical in production. It ensures that every time you run the code, the same rows go into "Train" and the same rows go into "Test," making your experiments reproducible.

**4. Handling Class Imbalance**

In e-commerce, most users don't buy anything. This results in a dataset where 98% of the labels might be 0 (no purchase) and only 2% are 1 (purchase).

Concept: Validating the distribution of your labels.

Importance: If a model simply predicts "No Purchase" for everyone, it would be 98% accurate but 0% useful. Recognizing this imbalance early allows you to use techniques like oversampling, undersampling, or adjusting class weights during training.

**5. Feature Selection**

Not all data is useful. Day 5 emphasizes selecting features that have a high correlation or predictive power for the target, while removing redundant or noisy data that could slow down the model.



---

### 💻 Practice:

```python
label_df = events.groupBy("user_id") \
    .agg(F.max(
        F.when(F.col("event_type")=="purchase",1).otherwise(0)
    ).alias("purchased"))

training_data = features_df.join(label_df,"user_id")
train, test = training_data.randomSplit([0.8,0.2], seed=42)



```
---
### 🔗 Resources:


[https://spark.apache.org/docs/latest/ml-guide.html](https://spark.apache.org/docs/latest/ml-guide.html)
