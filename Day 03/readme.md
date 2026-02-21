# Day 3:  Job Orchestration Basics

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:

The focus of Day 3 is transitioning from interactive development to production automation. While the first two days likely focused on writing code in notebooks, Day 3 teaches you how to make those notebooks dynamic using parameters and how to schedule them to run automatically using the Databricks Workflows (Jobs) UI.

The goal is to move away from manually clicking "Run All" and instead create a hands-off pipeline that can run daily or be triggered with specific configurations.

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

1. Parameterized Notebooks (Databricks Widgets)
   
In a production environment, you rarely want to hardcode values (like file paths or dates). Widgets allow you to pass variables into a notebook from the outside.

What they do: They create input fields at the top of your notebook.

How they work:

dbutils.widgets.text("name", "default_value"): Creates a text input box.

dbutils.widgets.get("name"): Retrieves the value entered in that box to use in your code.

Use Case: Running the same "Clean Data" notebook for different departments by simply changing a "department" parameter.

2. Jobs vs. Notebooks
   
Understanding the difference is critical for data engineering:

Notebooks: Best for exploration, visualization, and debugging. They run on interactive clusters.

Jobs (Workflows): The non-interactive execution of a notebook (or other tasks). Jobs typically run on Job Clusters, which are cheaper because they terminate as soon as the task is finished.

3. Job Orchestration & Scheduling
   
This involves setting up the "when" and "how" of your data pipeline:

Triggers: You can set a job to run on a Cron schedule (e.g., every day at 8:00 AM) or trigger it via an API.

UI Configuration: Using the Databricks "Workflows" tab to select a source notebook, choose a compute resource, and define retry policies if the job fails.

4. Modularization
   
Instead of having one giant notebook that does everything, Day 3 encourages "Modularizing logic."

Concept: Separating feature creation, data cleaning, and model training into distinct parts.

Benefit: Makes debugging easier and allows you to reuse specific logic across different projects.

Code Breakdown (The Practice Task)
The snippet provided illustrates how to capture external input:

Python
# 1. Create a text widget named "layer" with a default value of "silver"
dbutils.widgets.text("layer","silver")

# 2. Fetch the value currently stored in that widget
layer = dbutils.widgets.get("layer")

# 3. Use that value in your logic
print("Running layer:", layer)
Summary of Tasks for the Day:
Add Widgets: Make your notebook dynamic.

Organize Code: Clean up feature engineering logic so it’s "modular."

UI Setup: Go to the Workflows tab in Databricks and create a new Job pointing to your notebook.

Automate: Set the "Schedule" toggle to "Scheduled" and set it to run daily.



---

### 💻 Practice:
```python
dbutils.widgets.text("layer","silver")
layer = dbutils.widgets.get("layer")print("Running layer:", layer)

```
---
### 🔗 Resources:
[https://docs.databricks.com/jobs/](https://docs.databricks.com/jobs/)

