# DAY 12 : Cost Optimization Basics

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

Day 12 focuses on the foundational principles of Cost Optimization. In Databricks, where costs are primarily driven by compute usage (measured in Databricks Units or DBUs), mastering these basics is essential for moving from experimental projects to production-ready, budget-conscious pipelines.

The core objective of this day is to teach how to balance performance and expenditure. This moves beyond just "making code work" to "making code efficient," emphasizing that a poorly configured cluster or an unoptimized data layout can lead to unnecessary cloud bills.

---

### 📚 Learn:

- Cluster sizing
- Caching vs recompute
- Data partitioning

---

### 🛠️ Tasks:

1. Analyze job runtime.
2. Reduce unnecessary actions.
3. Document cost-saving ideas.

---

### 📚 Key Concepts:


**1. Cluster Sizing**

This involves selecting the right compute resources for your specific workload.

Right-Sizing: Instead of using the largest cluster available, start small and scale up. Use Compute-Optimized instances for CPU-heavy tasks (like transformations) and Memory-Optimized instances for memory-intensive tasks (like large joins or ML training).

Autoscaling: Enable this to let Databricks dynamically add or remove workers based on the load.

Job Clusters vs. All-Purpose Clusters: For production tasks, always use Job Clusters. They are significantly cheaper (often half the cost) than the All-Purpose clusters used for interactive development.

Auto-Termination: Set aggressive idle-time limits (e.g., 15–20 minutes) for interactive clusters to ensure they don't run overnight.

**2. Caching vs. Recompute**

This is the trade-off between using memory/disk to save data versus recalculating it from scratch.

Caching: When you need to access the same dataset multiple times in a notebook (e.g., in a loop or for multiple downstream charts), use .cache() or .persist(). This saves time and compute by reading from memory/SSD instead of the data lake.

Recompute: If you only use a dataset once, recomputing it is cheaper because caching consumes cluster memory which could be used for processing, potentially forcing the cluster to scale up.

Databricks Disk Caching: Modern Databricks runtimes automatically cache data on the local SSD of workers (formerly called Delta Caching), which is often more efficient than manual Spark caching.

**3. Data Partitioning**

Partitioning is the physical organization of data in your storage (S3/ADLS/GCS).

The Strategy: Organize data into folders based on a column you frequently filter by (e.g., year, month, or region).

Partition Skipping: When you run a query like WHERE year = 2024, Databricks skips all other folders. This drastically reduces the amount of data read, lowering both time and cost.

Best Practice: Only partition tables larger than 1TB. For smaller tables, use Z-Ordering (within the OPTIMIZE command) to achieve similar performance without the overhead of too many small files.

Guidance on Tasks
Analyze Job Runtime: Use the Spark UI or Compute "Metrics" tab to see if your CPUs are idling while the cluster is running. A job that takes 1 hour but only uses 10% of the CPU is a prime candidate for a smaller cluster.

Reduce Unnecessary Actions: Avoid calling .count(), .show(), or .collect() inside production loops. These "Actions" force Spark to trigger a job and move data to the driver, which is slow and expensive.

Document Cost-Saving Ideas: Think about using Spot Instances for non-critical jobs to save up to 80%, or enabling the Photon Engine only for complex SQL queries where the speed boost justifies the higher DBU cost.


---
### 🔗 Resources:

https://www.youtube.com/watch?v=ADBZ3bouyp8


