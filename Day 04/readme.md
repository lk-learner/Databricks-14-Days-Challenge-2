# Day 4:  Structured Streaming (Basic Simulation)

## Databricks 14-Day AI Challenge
---
### 🚀 Overview:

Day 4 shifts the focus from static data processing to Real-Time Data Processing. The objective is to understand how Apache Spark handles continuous data streams. Instead of reading a file once, you are setting up a pipeline that "listens" to a folder and automatically processes new files as they arrive. This is the foundation for building "Live" dashboards and real-time AI features.

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

**1. Micro-batch Processing**
   
Structured Streaming doesn't necessarily process data record-by-record in real-time. Instead, it uses a Micro-batch engine.

It checks the source at regular intervals (triggers).

It picks up any new data since the last check.

It processes that data as a small Spark DataFrame.

**2. readStream vs. writeStream**

In previous days, you likely used spark.read and df.write.

readStream: Tells Spark to treat the source (like a folder or a Kafka topic) as an "Unbounded Table." As new data arrives, rows are added to this table.

writeStream: This triggers the actual execution of the streaming query. Unlike static writes, this process keeps running until you manually stop it.

**3. Schema Enforcement**

When streaming from files (like CSV or JSON), Spark requires you to define the schema upfront.

Why? Because Spark needs to know the structure of the data before it arrives to ensure the pipeline doesn't break if a corrupt file is added to the folder.

**4. Checkpointing (Crucial for Fault Tolerance)**

The code snippet includes .option("checkpointLocation", "/tmp/checkpoint").

What it does: It saves the "state" of the stream (how much data has been processed) to a cloud storage folder.

Why it matters: If your cluster crashes or the job stops, Spark looks at the checkpoint folder when it restarts. It will pick up exactly where it left off, ensuring no data is lost or processed twice (Exactly-once semantics).

**5. Output Modes**

The example uses .outputMode("append").

Append: Only adds new records to the sink (Delta table).

Complete: Overwrites the entire sink every time there is new data (usually used for streaming aggregations/counts).

Update: Only updates the rows that changed.

**6. Streaming to Delta Lake**

Using .format("delta") as the sink is the industry standard. Delta Lake allows you to perform "Streaming Sink" operations while simultaneously allowing other users to query the table without any read/write conflicts, thanks to ACID transactions.

**Practice Code Logic Breakdown**

Looking at your practice snippet:

Source: It monitors /FileStore/stream_input/ for new CSV files.

Schema: It inherits the structure from an existing events object.

Sink: It writes the incoming data into a Delta Table located at /delta/stream_output.

Recovery: It uses a checkpoint to ensure it can recover from failures.

How to test this?
To see this in action on Databricks:

Start the stream using the code provided.

While the stream is running, upload a new CSV file into the /FileStore/stream_input/ folder.

Run a simple SQL query: SELECT count(*) FROM delta./delta/stream_output``.

You will see the count increase automatically as soon as the file lands in the folder!




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
