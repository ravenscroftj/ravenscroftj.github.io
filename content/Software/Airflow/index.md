---
updated: 2024-01-30T13:25
created: 2024-01-29T08:13
title: Airflow
aliases:
  - Airflow
---

Airflow is a data transformation pipeline tool for [[ETL]] and [[ELT]] workflows. Airflow is a [[foss]] package that can be [[Using-Airflow-Locally|installed locally]] with ease and also used in production.  Airflow is also relatively easy to extend with a[ plugin api](Airflow-Plugins) and a large number of community packages such as [[Using-Airflow-GCloud|google cloud integration]].

Airflow uses the notion of [[Airflow-DAGs|DAGs]] for units of execution. It's possible to create recursive or recurrent tasks by having DAGs call each other or using a timer/scheduler to call dags repeatedly.




-