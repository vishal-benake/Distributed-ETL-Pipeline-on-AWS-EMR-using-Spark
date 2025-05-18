# Distributed-ETL-Pipeline-on-AWS-EMR-using-Spark 

This project demonstrates how to process large datasets using **Amazon EMR** and **Apache Spark**. It includes a Spark-based ETL pipeline, AWS CLI scripts for EMR management, and a sample dataset for testing purposes.

---

## 🧠 Project Overview

This project securely ingests, processes, and analyzes structured and semi-structured YouTube trending video data using scalable AWS services.

### 🔍 Project Goals

1. **Data Ingestion** – Automate ingestion from diverse sources.
2. **ETL System** – Transform raw data into a structured format.
3. **Data Lake** – Store all data centrally using Amazon S3.
4. **Scalability** – Design for performance as data volume grows.
5. **Cloud Processing** – Use AWS EMR to process data at scale.
6. **Reporting** – Visualize insights using Amazon QuickSight.

---

## ☁️ AWS Services Used

| Service        | Purpose                                                                 |
|----------------|-------------------------------------------------------------------------|
| Amazon S3      | Centralized object storage for raw and processed data                   |
| AWS IAM        | Securely manage access to AWS resources                                 |
| AWS Glue       | Serverless data cataloging and preparation                              |
| AWS Lambda     | Trigger ETL tasks without server management                             |
| AWS Athena     | Run SQL queries directly on data stored in S3                           |
| Amazon EMR     | Distributed data processing using Apache Spark                          |
| Amazon QuickSight | Business intelligence tool to build dashboards from processed data  |

---

## 📁 Project Structure

```
.
├── spark-etl.py       # Apache Spark ETL script
├── commands.py        # AWS CLI commands for EMR setup
├── data/              # Sample dataset
├── assets/
│   └── Architecture.png  # Architecture diagram
```

---

## 🧰 Requirements

Make sure the following are available:

- ✅ Apache Spark (locally or via EMR)
- ✅ AWS CLI configured with valid credentials
- ✅ AWS account with:
  - EMR creation & termination permissions
  - S3 bucket access
  - IAM Roles: `EMR_DefaultRole`, `EMR_EC2_DefaultRole`
- ✅ EC2 Key Pair (for optional SSH access)

---

## 🏗️ System Architecture

![Architecture](assets/Architecture.png)

---

## 🔥 Spark Script (`spark-etl.py`)

The Spark script reads raw input data from an **S3 path**, applies transformations (e.g., adds timestamps), and writes the cleaned data to another **S3 path** in **Parquet format**.

### ▶️ Usage

Run the script using the following command:

```bash
spark-submit spark-etl.py [s3-input-folder] [s3-output-folder]
```

**Replace:**

- `[s3-input-folder]`: S3 path to the raw input data  
- `[s3-output-folder]`: Target S3 path where processed output should be saved

---

## ⚙️ AWS Commands (`commands.py`)

This file contains AWS CLI commands for setting up and managing your EMR cluster and submitting Spark jobs.

### 1. Create EMR Cluster

```bash
aws emr create-cluster   --name "EMR-Spark-Cluster"   --release-label emr-6.10.0   --applications Name=Spark   --ec2-attributes KeyName=your-key-pair   --instance-type m5.xlarge   --instance-count 3   --use-default-roles   --log-uri s3://your-bucket/logs/
```

### 2. Submit Spark Job

```bash
aws emr add-steps   --cluster-id j-XXXXXXXXXXXXX   --steps Type=Spark,Name="SparkETLJob",ActionOnFailure=CONTINUE,Args=[spark-submit,--deploy-mode,cluster,s3://your-bucket/scripts/spark-etl.py,s3://your-bucket/input/,s3://your-bucket/output/]
```

### 3. Terminate Cluster

```bash
aws emr terminate-clusters --cluster-ids j-XXXXXXXXXXXXX
```

> 📝 Replace `your-key-pair`, `your-bucket`, and `j-XXXXXXXXXXXXX` with your actual key name, S3 bucket, and EMR cluster ID.

---

## 📊 Sample Data

The `data/` directory contains a sample dataset representing the expected format for this ETL pipeline.  
You can replace this with a larger structured dataset in formats such as **CSV** or **JSON** for full-scale testing.

---

## ✅ Final Notes

- Use Amazon Athena for interactive querying of processed data.
- Use Amazon QuickSight to visualize trends by video category, region, and engagement.
- Use AWS Glue Crawlers to build schema catalog for Parquet data in S3.
- Clean, scalable, and reproducible architecture for beginner-to-intermediate Data Engineers.

---

## <img src="https://upload.wikimedia.org/wikipedia/commons/0/09/YouTube_full-color_icon_%282017%29.svg" width="20" height="20"> Youtube
<h4>If you like, do follow me on Youtube</h4>
<a href="https://www.youtube.com/@Code-With-Vishal">Connect with me on  Youtube</a>

## <img src="https://upload.wikimedia.org/wikipedia/commons/e/e7/Instagram_logo_2016.svg" width="20" height="20"> Instagram
<h4>If you like, do follow me on Instagram</h4>
<a href="https://www.instagram.com/vishaal_87">Connect with me on Instagram</a>
