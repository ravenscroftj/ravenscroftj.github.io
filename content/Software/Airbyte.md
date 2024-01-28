---
aliases:
  - Airbyte
---


- Airbyte is a [[foss]] core tool for managing [[ETL]] operations between data sources.
- Airbyte uses [[dbt]] under the covers to do some of the heavy lifting during transformation.
-
- ## Octavia
  id:: 64b69e06-5869-42c5-bb96-3a93c4ebe82e
	- There is a GUI for configuring airbyte but there is also a cli which can be used to version control configurations
	- https://airbyte.com/tutorials/version-control-airbyte-configurations
	  id:: 64b3e51b-fe93-49f5-89dc-f7adb4cc428a
	- Secrets can be managed via a `~/.octavia` config file https://airbyte.com/tutorials/version-control-airbyte-configurations#create-a-postgres-source-with-octavia-cli
	  id:: 64b3e51b-259b-4a21-9458-46077bc3f0b0
	- I've written a little Python script to debug octavia configurations here: https://tungsten.filament.uk.com/ravenscroftj/airbyte-config-tool
	  id:: 64b3e51b-d2df-444e-938e-e782482ee08c
	-
-
-
- **08:15** [[quick capture]]:  [Data warehouse tech stack with MySQL, DBT, Airflow](https://archive.jamesravey.me/archive/1689318914.536566/singlefile.html)
-
- ##
- ## Airbyte Transformation
	- It seems like you can use DBT to do transformation after you've copied the data from the source
	- In order to connect Airbyte to [[Gitlab]] you can create a deploy token or access token and connect over http.
		- Any []non-blank value can be used as the username](https://stackoverflow.com/questions/63924723/access-gitlab-repo-with-project-access-token)
		-
	- **08:16** [[quick capture]]:  [Transformations with SQL (Part 1/3) | Airbyte Documentation](https://docs.airbyte.com/operator-guides/transformation-and-normalization/transformations-with-sql/)
	- **18:34** [[quick capture]]:  [Transforming raw data into datasets using Airbyte with dbt - WalkingTree Technologies](https://walkingtree.tech/transforming-raw-data-datasets-using-airbyte-dbt/)
	-
-
- ## Airbyte Connectors
	- We probably want to build a custom airbyte connector for [[Syfter]]
	- ### Authentication
		- Airbyte connectors can authenticate via Basic Auth, Bearer Token, API Key or OAuth
		- https://docs.airbyte.com/connector-development/connector-builder-ui/authentication
	- ## Record Processing
		- Airbyte connectors make HTTP requests, carry out transformations of the data
		- The documentation seems to imply that records can be arbitrary json objects - you just specify a JSON selector to point to where those records are.
		- We use json-schema to define the record object schema
		-