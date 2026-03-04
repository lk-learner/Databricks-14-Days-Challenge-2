# DAY 13 : End-to-End Architecture Design

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

Day 13 is a crucial transition from individual technical tasks to high-level system engineering. 
The primary goal of Day 13 is to synthesize everything learned during the previous days into a cohesive, production-ready system. This day shifts the focus from writing individual Spark jobs or training a single model to designing the entire ecosystem that allows data to flow seamlessly from its raw source to a deployed AI model that provides business value.

---

### 📚 Learn:

- Data flow design
- Bronze → Silver → Gold
- ML lifecycle integration

---

### 🛠️ Tasks:

1. Draw architecture diagram.
2. Document pipeline flow.
3. Define retraining strategy.

Day 13 Tasks Explained: 

Architecture Diagram: Create a visual map showing the flow from Source → Bronze → Silver → Gold → MLflow → Serving.

Pipeline Documentation: Document the "How" and "Why". For example "Data is ingested from S3 every 4 hours using Auto Loader."

Retraining Strategy: Define the criteria for when a model is no longer accurate and needs to be updated.

---

### 📚 Key Concepts:

**Medallion Architecture (The Data Foundation)**

Bronze Layer: The "Landing" or "Raw" zone where data is stored in its original format. It serves as a historical record.

Silver Layer: The "Cleansed" zone. Data is filtered, cleaned, and augmented. This is where you enforce schemas and handle data quality.

Gold Layer: The "Curated" or "Business" zone. Data is aggregated and structured specifically for reporting or as features for Machine Learning models.

**ML Lifecycle Integration**

Integrating MLflow into the data pipeline to track experiments, parameters, and metrics.

Using the Model Registry to manage model versions (Staging vs. Production).

Ensuring the pipeline can serve models either via Batch Inference or Real-time API endpoints.

**Data Flow & Pipeline Orchestration**

Designing how data moves using Databricks Workflows or Delta Live Tables (DLT).

Understanding the "Trigger" mechanisms: Does the pipeline run on a schedule, or is it event-driven?

**Retraining Strategy**

Scheduled Retraining: Training models at fixed intervals (e.g., weekly).

Trigger-based Retraining: Automating retraining when "Model Drift" or "Data Drift" is detected.



---
### 🔗 Resources:

[Official Documentation: Databricks Medallion Architecture Guide](https://www.databricks.com/blog/what-is-medallion-architecture)


[Databricks Architecture - How it really works](https://docs.databricks.com/aws/en/getting-started/architecture)


