---
created: 2024-01-30T13:20
updated: 2024-01-30T13:21
---
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
