🛒 **Real-Time Retail Streaming Pipeline**

✨ **Project Overview**


A real-time retail data pipeline demonstrating Bronze → Silver → Gold architecture using PySpark Structured Streaming on Azure Databricks.


💡 **Key features:**


Stream CSV data uploaded to DBFS input folder into Delta Bronze tables

Clean & deduplicate in Silver

Aggregate key business metrics in Gold (total sales, quantity, unique customers, average order value)

Visualize KPIs in Databricks for each country

Data Source: UCI Online Retail Dataset (https://archive.ics.uci.edu/ml/datasets/Online+Retail)

⚙️**How to Run**


1️⃣ Upload CSVs to the DBFS input folder (/FileStore/tables).

2️⃣ Run Bronze Notebook → raw ingestion to Delta Bronze.

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

6.DBFS Storage / CSV Input – Source data


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

b)Bronze–Silver–Gold Delta Lake architecture

c)Deduplication & data cleaning

d)Real-time KPI computation

e)Databricks visualizations for country-level metrics
