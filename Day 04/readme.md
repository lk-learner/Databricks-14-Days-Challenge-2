# Day 4:  Structured Streaming (Basic Simulation)

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:


---
### 📚 Learn:

- Micro-batch streaming
- Checkpointing
- Streaming → Delta

---

### 🛠️ Tasks:

1. Simulate streaming from folder.
2. Write streaming output to Delta.
3. Query streaming results.

---

### 📚 Key Concepts:






---

### 💻 Practice:

```python
stream_df = spark.readStream \
    .schema(events.schema) \
    .csv("/FileStore/stream_input/")

query = stream_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option("checkpointLocation","/tmp/checkpoint") \
    .start("/delta/stream_output")

```
---
### 🔗 Resources:

[https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html)
