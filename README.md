# 🚀 Real-Time Data Streaming Pipeline

<div align="center">

![Data Engineering](https://img.shields.io/badge/Data-Engineering-blue)
![Apache Kafka](https://img.shields.io/badge/Apache-Kafka-231F20?logo=apache-kafka)
![Apache Spark](https://img.shields.io/badge/Apache-Spark-E25A1C?logo=apache-spark)
![Apache Airflow](https://img.shields.io/badge/Apache-Airflow-017CEE?logo=apache-airflow)
![Cassandra](https://img.shields.io/badge/Apache-Cassandra-1287B1?logo=apache-cassandra)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.9-3776AB?logo=python&logoColor=white)

**An end-to-end real-time data streaming pipeline built with Apache Kafka, Spark, Airflow, and Cassandra**

[Architecture](#-architecture) • [Features](#-features) • [Quick Start](#-quick-start) • [Tech Stack](#-tech-stack)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Architecture](#-architecture)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Data Flow](#-data-flow)
- [Monitoring](#-monitoring)
- [Troubleshooting](#-troubleshooting)
- [Future Enhancements](#-future-enhancements)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

---

## 🎯 Overview

This project implements a **production-ready real-time data streaming pipeline** that ingests user data from an external API, processes it through a distributed streaming architecture, and stores it in a NoSQL database for analytics.

### **What This Pipeline Does:**

1. **Fetches** random user data from [Random User API](https://randomuser.me/)
2. **Orchestrates** data ingestion using Apache Airflow
3. **Streams** data through Apache Kafka message queues
4. **Processes** data in real-time using Apache Spark
5. **Stores** processed data in Apache Cassandra
6. **Monitors** the entire pipeline with Kafka Control Center

### **Real-World Use Cases:**

- IoT sensor data processing
- Financial transaction monitoring
- Social media analytics
- E-commerce event tracking
- Log aggregation and analysis

---

## 🏗️ Architecture

<div align="center">
  <img src="Data_engineering_architecture.png" alt="System Architecture" width="800"/>
</div>

### **Component Breakdown:**

| Component | Role | Technology |
|-----------|------|------------|
| **Data Source** | External API providing user data | Random User API |
| **Orchestrator** | Workflow scheduling and management | Apache Airflow |
| **Message Queue** | Distributed streaming platform | Apache Kafka + ZooKeeper |
| **Stream Processor** | Real-time data processing | Apache Spark (1 Master + 4 Workers) |
| **Database** | Distributed NoSQL storage | Apache Cassandra |
| **Monitoring** | Pipeline monitoring and visualization | Kafka Control Center + Schema Registry |
| **Containerization** | Service orchestration | Docker & Docker Compose |

---

## ✨ Features

### **Core Capabilities:**

- ✅ **Real-Time Processing**: Sub-second latency data pipeline
- ✅ **Distributed Architecture**: Horizontally scalable components
- ✅ **Fault Tolerance**: Automatic recovery and checkpointing
- ✅ **Schema Management**: Centralized schema registry
- ✅ **Monitoring**: Built-in observability with Kafka Control Center
- ✅ **Containerized**: Easy deployment with Docker Compose

### **Technical Highlights:**

```python
# Stream Processing with Spark
- Micro-batch processing (2-second intervals)
- Exactly-once semantics with checkpointing
- Parallel processing across 4 worker nodes
- Automatic schema validation

# Data Ingestion
- Scheduled DAGs with Airflow
- 100+ messages per minute throughput
- JSON data transformation
- UUID generation for unique records

# Data Storage
- Distributed writes to Cassandra
- Primary key-based partitioning
- Configurable replication factor
- CQL query interface
```

---

## 🛠️ Tech Stack

<table>
<tr>
<td width="50%">

### **Data Engineering**
- Apache Kafka 7.4.0
- Apache Spark 3.5.0
- Apache Airflow 2.6.0
- Apache Cassandra 4.1.10
- ZooKeeper 7.4.0

</td>
<td width="50%">

### **Programming & Tools**
- Python 3.9
- Docker & Docker Compose
- PostgreSQL (Airflow metadata)
- Kafka Connect
- Schema Registry

</td>
</tr>
</table>

**Python Libraries:**
```
apache-airflow==2.6.0
kafka-python==2.0.2
cassandra-driver==3.29.3
pyspark==3.5.0
requests==2.31.0
```

---

## 📦 Prerequisites

Before you begin, ensure you have:

- **Docker Desktop** (4.20+) - [Download](https://www.docker.com/products/docker-desktop)
- **Docker Compose** (2.0+)
- **Git**
- **8GB+ RAM** available
- **10GB+ disk space**

### **System Requirements:**

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| RAM | 8 GB | 16 GB |
| CPU Cores | 4 | 8 |
| Disk Space | 10 GB | 20 GB |
| OS | macOS, Linux, Windows 10+ | Any |

---

## 🚀 Installation

### **1. Clone the Repository**

```bash
git clone https://github.com/MulayeMuhammad/RealTime_Data_Streaming.git
cd RealTime_Data_Streaming
```

### **2. Project Structure**

```
RealTime_Data_Streaming/
├── dags/
│   └── kafka_stream.py          # Airflow DAG for data ingestion
├── script/
│   └── entrypoint.sh             # Airflow initialization script
├── spark_stream.py               # Spark streaming application
├── docker-compose.yml            # Docker services configuration
├── requirements.txt              # Python dependencies
├── Data_engineering_architecture.png
└── README.md
```

### **3. Start the Pipeline**

```bash
# Start all services
docker-compose up -d

# Verify all containers are running
docker ps
```

**Expected Output:**
```
CONTAINER ID   IMAGE                                      STATUS
xxxxx          apache/airflow:2.6.0                      Up
xxxxx          confluentinc/cp-kafka:7.4.0               Up
xxxxx          confluentinc/cp-zookeeper:7.4.0           Up
xxxxx          bitnami/spark:latest                      Up
xxxxx          cassandra:latest                          Up
```

### **4. Initialize Services**

**Access Airflow UI:**
```bash
open http://localhost:8080
```
- **Username:** `admin`
- **Password:** `admin`

**Access Kafka Control Center:**
```bash
open http://localhost:9021
```

---

## 🎮 Usage

### **Step 1: Trigger Data Ingestion**

**Option A: Via Airflow UI**
1. Navigate to http://localhost:8080
2. Find `user_automation` DAG
3. Click the "Play" button to trigger

**Option B: Via CLI**
```bash
docker exec -it realtime_data_streaming-webserver-1 \
  airflow dags trigger user_automation
```

### **Step 2: Start Spark Streaming**

```bash
docker exec -it --user root spark-master /opt/spark/bin/spark-submit \
  --packages com.datastax.spark:spark-cassandra-connector_2.12:3.4.1,\
org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.0 \
  /opt/spark_stream.py
```

**Expected Output:**
```
INFO:root:Spark connection created successfully!
INFO:root:kafka dataframe created successfully
INFO:root:Streaming is being started...
```

### **Step 3: Verify Data in Cassandra**

```bash
# Connect to Cassandra
docker exec -it cassandra cqlsh

# Query data
USE spark_streams;
SELECT COUNT(*) FROM created_users;
SELECT first_name, last_name, email FROM created_users LIMIT 10;
```

**Sample Output:**
```
 count
-------
   333

 first_name | last_name | email
------------+-----------+--------------------------------
        Tom |      Boyd |           tom.boyd@example.com
       Joao |      Held |          joao.held@example.com
```

---

## 📊 Data Flow

### **Detailed Pipeline Flow:**

```
┌─────────────┐
│ Random User │
│     API     │
└──────┬──────┘
       │ HTTP GET
       ▼
┌─────────────────┐
│ Apache Airflow  │
│ - Fetch data    │
│ - Transform     │
│ - Generate UUID │
└──────┬──────────┘
       │ Kafka Producer
       ▼
┌──────────────────┐
│  Apache Kafka    │
│ Topic:           │
│ users_created    │
└──────┬───────────┘
       │ Stream
       ▼
┌──────────────────┐
│  Apache Spark    │
│ - Read stream    │
│ - Parse JSON     │
│ - Validate       │
│ - Transform      │
└──────┬───────────┘
       │ Batch Write
       ▼
┌──────────────────┐
│    Cassandra     │
│ Keyspace:        │
│ spark_streams    │
│ Table:           │
│ created_users    │
└──────────────────┘
```

### **Data Schema:**

```python
{
    "id": "UUID",                    # Primary Key
    "first_name": "String",
    "last_name": "String",
    "gender": "String",
    "address": "String",             # Formatted full address
    "post_code": "String",
    "email": "String",
    "username": "String",
    "dob": "ISO8601 Timestamp",
    "registered_date": "ISO8601 Timestamp",
    "phone": "String",
    "picture": "URL"
}
```

---

## 📈 Monitoring

### **Airflow Dashboard**
- **URL:** http://localhost:8080
- **Monitor:** DAG runs, task status, execution logs
- **Metrics:** Success/failure rates, execution time

### **Kafka Control Center**
- **URL:** http://localhost:9021
- **Monitor:** Topic throughput, consumer lag, broker health
- **Features:** Message inspection, schema management

### **Spark UI**
- **URL:** http://localhost:9090 (Master)
- **Monitor:** Job progress, executor status, streaming statistics
- **Metrics:** Processing rate, batch duration, failures

### **Cassandra Monitoring**

```bash
# Check cluster status
docker exec -it cassandra nodetool status

# View table statistics
docker exec -it cassandra nodetool tablestats spark_streams.created_users
```

---

## 🐛 Troubleshooting

### **Common Issues:**

<details>
<summary><b>Services won't start</b></summary>

```bash
# Check Docker resources
docker system df

# Restart all services
docker-compose down
docker-compose up -d
```
</details>

<details>
<summary><b>Kafka connection errors</b></summary>

```bash
# Verify Kafka is running
docker exec -it broker kafka-topics --list --bootstrap-server localhost:9092

# Check broker logs
docker logs broker
```
</details>

<details>
<summary><b>Spark streaming fails</b></summary>

```bash
# Check Spark logs
docker logs spark-master

# Verify Cassandra connection
docker exec -it cassandra cqlsh -e "DESCRIBE KEYSPACES;"
```
</details>

<details>
<summary><b>No data in Cassandra</b></summary>

```bash
# Verify Kafka has messages
docker exec -it broker kafka-console-consumer \
  --bootstrap-server broker:29092 \
  --topic users_created \
  --from-beginning \
  --max-messages 5

# Check if Airflow DAG succeeded
docker exec -it realtime_data_streaming-webserver-1 \
  airflow dags list-runs -d user_automation
```
</details>

---

## 🚀 Future Enhancements

### **Planned Features:**

- [ ] **Real-time Dashboard**: Grafana visualization
- [ ] **Data Quality Checks**: Great Expectations integration
- [ ] **Multiple Data Sources**: REST APIs, webhooks, databases
- [ ] **Machine Learning**: Spark MLlib for real-time predictions
- [ ] **Auto-scaling**: Kubernetes deployment
- [ ] **Advanced Analytics**: Spark SQL queries on streaming data
- [ ] **Alerting**: PagerDuty/Slack notifications on failures
- [ ] **Data Lake**: Integration with S3/HDFS for long-term storage
- [ ] **CI/CD Pipeline**: GitHub Actions for automated deployment
- [ ] **Security**: SSL/TLS encryption, authentication, RBAC

### **Scalability Improvements:**

```yaml
# Production Configuration
Kafka:
  - Partitions: 10-50
  - Replication Factor: 3
  - Compression: snappy

Spark:
  - Workers: 10-100
  - Executor Memory: 8-16GB
  - Cores per Executor: 4-8

Cassandra:
  - Nodes: 3-10
  - Replication Factor: 3
  - Consistency Level: QUORUM
```

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### **Development Guidelines:**

- Follow PEP 8 style guide for Python code
- Add tests for new features
- Update documentation
- Ensure all tests pass before submitting PR

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 📞 Contact

**Mulaye Muhammad Ahmed Brahim**

[![GitHub](https://img.shields.io/badge/GitHub-MulayeMuhammad-181717?logo=github)](https://github.com/MulayeMuhammad)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?logo=linkedin)](https://www.linkedin.com/in/your-profile)
[![Email](https://img.shields.io/badge/Email-Contact-D14836?logo=gmail)](mailto:your.email@example.com)

**Project Link:** [https://github.com/MulayeMuhammad/RealTime_Data_Streaming](https://github.com/MulayeMuhammad/RealTime_Data_Streaming)

---

## 🙏 Acknowledgments

- [Random User API](https://randomuser.me/) for providing test data
- [Apache Software Foundation](https://apache.org/) for amazing open-source tools
- [Confluent](https://www.confluent.io/) for Kafka Docker images
- Data engineering community for inspiration and support

---

<div align="center">

**⭐ Star this repo if you found it helpful!**

Made with ❤️ by [Mulaye Muhammad](https://github.com/MulayeMuhammad)

</div>
