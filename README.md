# End-to-End Data Pipeline: AWS S3 → Snowflake → Power BI  
An automated, near-real-time data engineering project using AWS, Snowflake, and Power BI Report Builder.

---

## 📌 Overview

This repository demonstrates a complete **cloud data pipeline** where Yelp dataset JSON files are:

1. **Stored in Amazon S3**
2. **Automatically ingested into Snowflake using Snowpipe**
3. **Tracked using Snowflake Streams (CDC)**
4. **Transformed using Snowflake Tasks**
5. **Sentiment-scored using a Python UDF**
6. **Loaded into curated analytical tables**
7. **Visualized using Power BI Report Builder**

This project represents a modern ELT architecture using fully cloud-native, event-driven data processing.

---

## 📊 Architecture Diagram

> **Replace the link below once you upload your lifecycle image**

![Architecture Diagram](./assets/lifecycle.png)

---

## 🚀 Key Components

### **1. AWS S3 – Raw Data Storage**
- Yelp JSON files stored in folder paths:
  - `s3://yelp-database-practice/reviews/`
  - `s3://yelp-database-practice/business/`
- S3 Event Notifications → SQS → Snowpipe triggers ingestion.

---

### **2. Snowflake – Ingestion, CDC & Transformations**

#### 🔹 **Storage Integration**
Secure connection from Snowflake to AWS using IAM roles & external ID.

#### 🔹 **Snowpipe (Auto-Ingest)**
Automatically loads new JSON files from S3 to raw Snowflake tables.

#### 🔹 **Raw Tables (Landing Zone)**
- `YELP_REVIEWS`
- `YELP_BUSINESS`

Semi-structured variant columns store raw JSON.

#### 🔹 **Streams (CDC)**
Tracks new rows added by Snowpipe for incremental processing.

#### 🔹 **Tasks (Automated Transformations)**
Runs only when new data is detected via:
```sql
WHEN SYSTEM$STREAM_HAS_DATA('<stream>')

```
🔹 Python UDF (Sentiment Analysis)

Uses TextBlob + keyword rules to categorize reviews as:

Positive
Negative
Neutral

🔹 Curated / Analytical Tables

TBL_YELP_REVIEWS
TBL_YELP_BUSINESS

Includes sentiment and cleaned fields.

📈 Power BI Reporting

Power BI Report Builder is used to create:
Business summary reports
Sentiment distribution dashboards
Review trend analyses
Download the report as PDF
City/State performance breakdowns

![Power BI Report Builder Diagram](./assets/power_bi_report.jpg)

Snowflake is connected through the Snowflake ODBC driver.

📦 yelp-data-pipeline
│
├── assets/
│   └── lifecycle.png        # Architecture diagram
│
├── scripts/
│   ├── 01_storage_integration.sql
│   ├── 02_snowpipe_setup.sql
│   ├── 03_raw_tables.sql
│   ├── 04_transformation_tasks.sql
│   └── 05_sentiment_udf.sql
│
├── powerbi/
│   └── report.rdl          # Example Power BI Report Builder file
│
└── README.md

⚙️ How the Pipeline Works (Step-by-Step)
1️⃣ File uploaded to S3

User uploads reviews_xxx.json → S3 Event fires.

2️⃣ S3 Event triggers Snowpipe

S3 → SQS → Snowflake → COPY INTO → raw tables.

3️⃣ Streams capture new rows

Streams detect inserts into raw tables.

4️⃣ Tasks transform new rows

Tasks automatically run when streams have new data.

5️⃣ Curated tables get updated

Sentiment added, JSON flattened, data cleaned.

6️⃣ Power BI displays the insights

Using curated Snowflake tables.

🧪 Features Demonstrated

Event-driven ELT architecture

Snowpipe auto-ingest

Snowflake Streams (CDC)

Snowflake Tasks (incremental ELT)

Python UDFs inside Snowflake

S3 → Snowflake secure IAM integration

Building analytical datasets

Power BI Report Builder visualization

🛠️ Technologies Used
Component	Technology
Cloud Storage	AWS S3
Ingestion	Snowflake Snowpipe
CDC	Snowflake Streams
Automation	Snowflake Tasks
Compute	Snowflake Warehouse
Analytics	Python UDF (TextBlob)
Reporting	Power BI Report Builder
Integration	IAM Role + External ID



📬 Contact

For questions or collaboration, feel free to reach out!

Shubham Gagare
Data Analyst & Cloud BI Engineer
Pune, India
