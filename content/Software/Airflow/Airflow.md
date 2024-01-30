---
updated: 2024-01-30T13:11
created: 2024-01-29T08:13
---

- Airflow is a data transformation pipeline tool for [[ETL]] and [[ELT]] workflows.




## Google Cloud Compatibility

Install airflow with `google` optional module: `pip install apache-airflow[google]`.

Credenials can be side-loaded in via an environment variable

`export AIRFLOW_CONN_GOOGLE_CLOUD_DEFAULT='{"conn_type": "google-cloud-platform", "key_path": "/secrets/key.json", "scope": "https://www.googleapis.com/auth/cloud-platform", "project": "airflow", "num_retries": 5}'`
#### Google OIDC auth 

It's possible to authenticate airflow against your google org using SAML/OpenID flow: https://airflow.apache.org/docs/apache-airflow-providers-google/stable/api-auth-backend/google-openid.html
## Airflow TriggerDAGRunOperator
- You can use `wait_for_completion=True` and it will detect whether the dag passed or failed.
- If you have a cleanup function make sure that it marks the upstream task as failed as appropriate. 
  
```python
  for task_instance in kwargs['dag_run'].get_task_instances():
        if task_instance.current_state() not in [State.SUCCESS, State.SKIPPED] and \
                task_instance.task_id != kwargs['task_instance'].task_id:
            raise Exception("Task {} failed. Failing this DAG run".format(task_instance.task_id))
```
## Mapping Tasks

Dynamic task expansion using the `partial` and `expand` functions has a hard limit which is governed by the environment variable `AIRFLOW__CORE__MAX_MAP_LENGTH` and defaults to 1024.
## Handling non-string DAG parameters

You may need to pass a dag parameter to an operator using templates - however, it may be important that this is the right data type (e.g. bool). By default all template values are stringified.

You can override this by passing `render_template_as_native_obj=True` to the DAG constructor which fills the template and then casts the value to the expected type.

For example
```python

with DAG(
  dag_id="example",
  catchup=False,
  start_date=datetime(2023, 4, 26),
  render_template_as_native_obj=True,
  params={
      "test_run": Param(False, title="Test run only", description="If true, don't do the transaction, just spoof it", type='boolean')
  }
) as dag:


  task_id = f"trigger_build_table_{table}"
  
  ts = datetime.now().replace(tzinfo=tz)
  dag_execution_ts = TriggerDagRunOperator(
          trigger_dag_id="exampledag",
          wait_for_completion=True,
          poke_interval=10,
          # reset_dag_run=True,tk
          execution_date=ts.isoformat(),
          trigger_run_id=f"example_dag_{ts.isoformat()}",
          conf={
              "table_name": table,
              "date_suffix": date_suffix,
              "test_run": "{{params.test_run}}"
          },
  )
```
-
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
-
-
-
- ## Resources
	- [Airflow Sensors](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/sensors/base/index.html#airflow.sensors.base.BaseSensorOperator)
	- [How to create a custom Airflow Sensor](https://archive.jamesravey.me/archive/1688721178.487017/singlefile.html)
	- https://airflow.apache.org/docs/apache-airflow/stable/start.html
-