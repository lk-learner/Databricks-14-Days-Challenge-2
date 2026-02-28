# DAY 9 : Recommendation System

## Databricks 14-Day AI Challenge

---
### 🚀 Overview:

The goal of Day 9 is to understand how to leverage user behavior data (like clicks, cart additions, and purchases) to predict what products a user might want to buy next. Instead of manually suggesting items, you train an ALS (Alternating Least Squares) model that learns patterns from a massive matrix of interactions to provide personalized Top-5 recommendations for every user.

---
### 📚 Learn:

- Collaborative filtering
- User-item interaction
- Cold start concept
---

### 🛠️ Tasks:

1. Create rating mapping.
2. Train ALS model.
3. Generate Top-5 recommendations.

---

### 📚 Key Concepts:

**1. Collaborative Filtering**

This is the "wisdom of the crowd" approach. It makes predictions about a user’s interests by collecting preferences from many users.

The Logic: If User A and User B both bought a laptop, and User A also bought a mouse, the system assumes User B is likely to want a mouse too.

Why it’s powerful: It doesn't need to know the details of the product (like color or brand); it only needs to know who interacted with what.

**2. User-Item Interaction (Implicit vs. Explicit)**

In many real-world scenarios, users don't leave 5-star ratings. Day 9 teaches you how to turn behavior into a numerical "rating":

Purchase (Rating 3): High intent/preference.

Add to Cart (Rating 2): Medium intent.

Other/View (Rating 1): Low intent.
By mapping these events to numbers, the model can quantify how much a user "likes" a product.

**3. ALS (Alternating Least Squares) Algorithm**

ALS is the specific algorithm used in Spark for collaborative filtering.

It performs Matrix Factorization: It breaks down a giant, mostly empty table (users vs. products) into two smaller, dense tables (user features and product features).

By multiplying these smaller tables back together, it "fills in the blanks" to predict ratings for items a user hasn't seen yet.

**4. The Cold Start Concept**

One of the biggest challenges in AI recommendations is "Cold Start" , what do you do with a brand-new user or a brand-new product with no history?

The Solution in Practice: In the provided code, coldStartStrategy="drop" is used. This tells Spark to drop any users or items in the test set that weren't present in the training set, preventing the model from crashing or returning "NaN" (Not a Number) errors.

**Summary of the Workflow**

Prepare Data: Transform raw event logs into a user_id, product_id, and rating format.

Configure ALS: Define the columns and set the cold start strategy.

Train (.fit): The model learns the latent factors (hidden patterns) of users and items.

Recommend: Use recommendForAllUsers(5) to generate a list of the 5 most relevant products for every individual in your database.


---
### 💻 Practice:

```python

from pyspark.ml.recommendationimport ALS

interaction_df = events.withColumn("rating",
    F.when(F.col("event_type")=="purchase",3)
     .when(F.col("event_type")=="cart",2)
     .otherwise(1)
).select("user_id","product_id","rating")

als = ALS(userCol="user_id",
          itemCol="product_id",
          ratingCol="rating",
          coldStartStrategy="drop")

als_model = als.fit(interaction_df)
als_model.recommendForAllUsers(5).show(5)

```
---
### 🔗 Resources:

[https://spark.apache.org/docs/latest/ml-collaborative-filtering.html](https://spark.apache.org/docs/latest/ml-collaborative-filtering.html)
