## Export Data
```sql
  EXPORT DATA
    OPTIONS (
      uri = 'gs://path-to/jsonl/*.jsonl.gz',
      format = 'JSON',
      compression='GZIP',
      overwrite = true
      )
  AS (
    SELECT *
    FROM `dataset.tablename`
  );
  ```

## Nested Data

Use the `UNNEST` command in `FROM` clause to unnest array structures in BigQuery rows. This does cause some repetition

## String Substrings (Contains)

- Best to use the `REGEXP_CONTAINS(container, containee)` syntax for doing string checks
