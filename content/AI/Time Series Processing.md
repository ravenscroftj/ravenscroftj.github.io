public:: true

-
- ## Event Processing
- It's quite common to stream data to [[Apache Spark]] and process streams of events there.
- You might want to [integrate kafka with pyspark](https://archive.jamesravey.me/archive/1656342686.931072/singlefile.html)
-
- ## Time Series Databases
-
- ### InfluxDB
	- Open source timeseries db with the following [Design Principles](https://docs.influxdata.com/influxdb/v2.3/reference/key-concepts/design-principles/):
		- Data is writtn in time-ascending order to maximise performance
		- Update and delete queries are strictly prohibited - its unusual to go back and change a time series
		- Priority is with fast read/write queries over strong consistency - queries are prioritised over transactions that affect the queried data
		- Schemaless design to facilitate flexible and ephemeral data
		- Data aggregation is most important- single entries don't have IDs in the traditional sense but are differentiated by timestamp and series (which stream they came from)
		- Influx does its own de-duplication, identical records are only stored once.
- ### Apache Flume - https://flume.apache.org/
	- A distributed service for aggregating large amounts of log data and storing it in HDFS
	-