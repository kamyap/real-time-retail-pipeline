🛒 **Real-Time Retail Streaming Pipeline**

✨ **Project Overview**


A real-time retail data pipeline demonstrating Bronze → Silver → Gold architecture using PySpark Structured Streaming on Azure Databricks.


💡 **Key features:**


Stream retail transactions in **real time** from **Azure Event Hub** into **Delta Bronze tables**  

Clean & deduplicate in Silver

Aggregate key business metrics in Gold (total sales, quantity, unique customers, average order value)

Visualize KPIs in Databricks for each country

Data Source: UCI Online Retail Dataset (https://archive.ics.uci.edu/ml/datasets/Online+Retail)

**Configuration**

The pipeline uses a single configuration file to manage environment-specific settings:

1.Event Hub credentials (connection string, consumer group)

2.Delta table paths for Bronze, Silver, and Gold

  File location: configs/config.json

Usage: All notebooks read this file at runtime to connect to Event Hub and determine Delta storage locations.

For local testing or demo purposes, you can upload the file to Databricks DBFS (/FileStore/configs/config.json).
In production, you may use Databricks Secrets or another secure credential store instead.

⚙️**How to Run**


1️⃣ Ensure **Event Hub** is running and contains retail transaction messages.

2️⃣ Run Bronze Notebook → raw ingestion to Delta Bronze.[after uploading configs.json in dbfs]

3️⃣ Run Silver Notebook → clean & deduplicate data → Delta Silver.

4️⃣ Run Gold Notebook → perform aggregations → Delta Gold.

5️⃣ Visualize KPIs in Databricks using built-in charts for:

  Total Sales
  
  Average Order Value
  
  Unique Customers
  (All at a country level)

**Example: read Gold table**

        gold_df = spark.read.format("delta").load("dbfs:/mnt/gold/events")
        gold_df.display()


📊 **Key Metrics**


Total Sales -->	Sum of (Quantity × UnitPrice) per country

Total Quantity --> Sum of Quantity per country

Unique Customers --> Approx. count of customers per country

Avg Order Value --> Total Sales ÷ Total Quantity per country


🛠 **Technologies Used**


1.Apache Spark / PySpark – Stream processing

2.Delta Lake – ACID-compliant storage

3.Azure Databricks – Development & execution

4.Python – Core programming

5.Databricks Visualizations – Charts & graphs

6.Azure Event Hub – Real-time streaming source


🔍**Monitoring & Debugging**


a)Streaming checkpoints ensure fault tolerance

b)Check active streams:

spark.streams.active


c)Deduplication, type casting, and approximate distinct counts handled in Silver & Gold


🚀**Future Enhancements**


1.Integrate Power BI / Synapse Analytics dashboards

2.EventHub triggers for fully real-time ingestion

3.Optional ADF orchestration for hybrid workflows

4.Log Analytics Monitoring for streaming metrics


🎯**Skills Demonstrated**


a)Structured streaming with PySpark

b)Event Hub → Delta Bronze → Silver → Gold pipeline

c)Deduplication & data cleaning

d)Real-time KPI computation

e)Databricks visualizations for country-level metrics
