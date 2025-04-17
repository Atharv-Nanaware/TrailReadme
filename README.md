# Real-Time Production-Grade Data Pipeline


In this project, I built a real-time, production-ready data pipeline using
modern data engineering tools. It handles everything from streaming data 
ingestion to transformation, validation, orchestration, and storage. 
The goal was to create an end-to-end solution that’s not just functional but 
scalable and reliable—something you’d actually use in a real-world 
production environment.


## Architecture


![Architecture Diagram](./assets/Architecture.png)


**Components:**
- **Kafka**: Real-time data ingestion (user profile stream)
- **Spark**: Distributed stream processing
- **Airflow**: Workflow orchestration and scheduling
- **Cassandra**: Scalable NoSQL data storage
- **Docker Compose**: Container orchestration for easy setup and reproducibility



## Features
- Real-time user profile data ingestion with Kafka
- Distributed stream processing with Spark
- Automated workflow management with Airflow
- Scalable, fault-tolerant data storage with Cassandra
- Fully containerized setup using Docker Compose


## Project Structure
```
├── dags/                # Airflow DAGs
├── spark_streaming/     # Spark streaming jobs
├── constants/           # Shared constants/configs
├── pipelines/           # ETL pipelines
├── docker-compose.yml   # Main orchestration file
├── requirements.txt     # Python dependencies
└── ...
```

## Getting Started

### 1. Clone the Repository
```sh
git clone https://github.com/Atharv-Nanaware/realtime-production-grade-pipeline.git
```
```
cd realtime-production-grade-pipeline
```

### 2. Start All Services
**Initialize Airflow:**
```
docker compose up airflow-init
```
**Start All Services:**
```sh
docker compose up -d
```
**Check All Containers Started:**
```aiignore
dokcer ps
```

### 3. Run DAG ON Airflow UI:

add Image Over Here

this will Create a kafka - topic we can see that on the kafka Ui



### 4. Submit Spark Job
```sh
zip -r dependencies.zip constants spark_streaming
```
```aiignore
docker cp dependencies.zip spark-master:/dependencies.zip
```
```aiignore
docker exec -it spark-master spark-submit \
    --packages com.datastax.spark:spark-cassandra-connector_2.12:3.5.1,org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.1 \
    --py-files /dependencies.zip \
    /opt/spark/spark_streaming/spark_processing.py
```
### 5. Verify Data in Cassandra
**Check record count:**
```sh
docker exec -it cassandra cqlsh -e "SELECT COUNT(*) FROM spark_streaming.created_users;"
```
**View sample data:**
```sh
docker exec -it cassandra cqlsh -e "SELECT * FROM spark_streaming.created_users LIMIT 5;"
```



[//]: # (## Use Case Example)

[//]: # (- **Scenario:** Ingest user profile data in real time &#40;e.g., user signups, updates&#41;)

[//]: # (- **Flow:**)

[//]: # (    1. Producer sends user profile events to Kafka topic `user_profile_stream`)

[//]: # (    2. Spark streaming job consumes from Kafka, processes/transforms data)

[//]: # (    3. Processed data is written to Cassandra for fast, scalable storage)

[//]: # (    4. Airflow orchestrates/schedules batch or streaming jobs as needed)



## Notes
- This project is designed for learning and demonstration. For production, consider adding monitoring, alerting, and security best practices.

---

[//]: # (**Feel free to use, extend, or adapt this project for your own learning or interviews!**)
