---
type: note
title: "DuckDB"
---

DuckDB is a local in-process [[olap]] database system written in C++ with extensions in various languages and an ice command line.

## Loading Data From JSON

It's possible to load json delineated files into a single table with a single command:

```sql
CREATE TABLE tablename as SELECT * FROM read_json_auto("*.jsonl.gz", lines=true, ignore_errors=True);
```