---
updated: 2024-01-30T13:23
created: 2024-01-29T08:13
title: Airflow
aliases:
  - Airflow
---

Airflow is a data transformation pipeline tool for [[ETL]] and [[ELT]] workflows. Airflow is a [[foss]] package that can be [[Using-Airflow-Locally|installed locally]] with ease and also used in production.  Airflow is also rela

Airflow uses the notion of [[Airflow-DAGs|DAGs]] for units of execution. It's possible to create recursive or recurrent tasks by having DAGs call each other or using a timer/scheduler to call dags repeatedly.







- ## Developing Airflow Plugins
	- Modules need to be on the `pythonPath`
	- By default the `plugins` directory is on the `pythonPath` as is `dags`
	-
- ### Operators
	- Custom operators extend the `from airflow.models.baseoperator.BaseOperator` class and override the `execute` method.
	- You can use jinja templating on fields inside operators:
		- Define the properties on the operator that should be evaluated by the template engine in the `template_fields` property like so:
		  
		  ```python
		  class HelloOperator(BaseOperator):
		  
		      template_fields: Sequence[str] = ("name",)
		  
		      def __init__(self, name: str, world: str, **kwargs) -> None:
		          super().__init__(**kwargs)
		          self.name = name
		          self.world = world
		  
		      def execute(self, context):
		          message = f"Hello {self.world} it's {self.name}!"
		          print(message)
		          return message
		  ```
-
- ### Sensors
	- Custom sensors extend the `from airflow.sensors.base.BaseSensorOperator` class and override the `poke` method
	- Custom sensors can be set up in `reschedule` mode which allows them to terminate the DAG and free up a worker slot to do something else.
	- As a rule of thumb `reschedule` should be used for long-running processes (Every 15 minutes) and `poke` should be used for processes that need checking frequently (every second)

- ## Resources
	- [Airflow Sensors](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/sensors/base/index.html#airflow.sensors.base.BaseSensorOperator)
	- [How to create a custom Airflow Sensor](https://archive.jamesravey.me/archive/1688721178.487017/singlefile.html)
	- https://airflow.apache.org/docs/apache-airflow/stable/start.html
-