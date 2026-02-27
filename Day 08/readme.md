# DAY 8 : Batch Inference Pipeline

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

Day 8 marks the transition from Model Development to Model Deployment. After training and validating a model in previous days, Day 8 focuses on "Operationalizing" that model.

The goal is to build a production-grade pipeline that takes a trained model and applies it to a large, static dataset (all users) to generate predictions. These predictions are then stored in the Gold Layer of the Medallion Architecture, making them ready for business consumption, such as marketing campaigns or executive dashboards.

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

**1. Batch Inference (Offline Scoring)**

Unlike "Real-time Inference" (where a model predicts for one user at a time via an API), Batch Inference processes millions of records simultaneously at scheduled intervals (e.g., daily or weekly).

Scale: Leveraging Apache Spark to distribute the model application across a cluster.

Efficiency: It is cost-effective for use cases where immediate, sub-second response times are not required (like identifying potential buyers for a tomorrow's email blast).

**2. The Gold Layer (Medallion Architecture)**

In Databricks, data usually moves from Bronze (Raw) → Silver (Cleaned/Joined) → Gold (Business-Ready).

Day 8 Focus: Creating the Gold layer. This is the final stage where data is highly refined.

Purpose: The "Gold" table doesn't just contain raw features; it contains the outputs (predictions/probabilities) that a business user can actually act upon.

**3. Production Scoring**

This involves loading a "Production-Ready" model (typically from the MLflow Model Registry) and applying it to new features.

Concept: Using the model.transform(df) method in Spark or a UDF (User Defined Function) to map the machine learning model onto the Silver-layer feature table.

**4. Persistence with Delta Lake**

The practice snippet shows saving data in Delta format.

Overwrite Mode: Often used in batch pipelines to refresh the entire prediction set with the most up-to-date scores.

ACID Compliance: Ensures that even if the write process fails halfway, the table remains in a consistent state and doesn't provide partial data to the business.

**5. Actionable Insights (Top Predicted Buyers)**

The final task identifying top buyers is the "Why" behind the "How."

Business Logic: Once predictions (usually probabilities between 0 and 1) are saved, you filter or sort them.

Example: "Show me the top 10% of users with a purchase probability > 0.8." This allows the marketing team to target only the most likely customers, optimizing spend.

---
### 💻 Practice:

```python

predictions.write.format("delta").mode("overwrite") \
    .save("/delta/gold/predictions")

```
---
### 🔗 Resources:

[https://docs.databricks.com/delta/](https://docs.databricks.com/delta/)


