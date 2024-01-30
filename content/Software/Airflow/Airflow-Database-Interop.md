---
created: 2024-01-30T14:01
updated: 2024-01-30T14:04
---

### [[PostgreSQL]]

Install the PostgreSQL plugin with:

`pip install apache-airflow-providers-postgres 


### [[MySQL]]


Install the MySQL plugin with:

`pip install apache-airflow-providers-mysql` 

This has a hard dependency on the mysqlclient package which requires C libraries and headers so it may be easiest to install that stuff first with conda before running the pip install:

`conda install mysqlclient`

