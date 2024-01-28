- CLI program that ships with [[mysql]] server that allows you to dump databases to sql files.
- ## Dump Structure Only
	- ```bash
	  mysqldump \
	   --routines \
	   --add-drop-table \
	   --disable-keys \
	   --skip-extended-insert \
	   --no-data \
	   --skip-lock-tables \
	   --host=<HOSTIP> \
	   --port=3306  \
	   --user <USERNAME> \
	   -p \
	   <DBNAME>
	  ```
	- Then type in password via CLI
	- It's also possible to pass in credentials via a my.cnf file like [[DBeaver]] seems to do. This might be more useful in an automated context e.g. inside [[Docker]] or a CI pipeline.
		- ```bash
		  /usr/bin/mysqldump \
		    --defaults-file=/tmp/.dbeaver-temp699335876542853025/.my.cnf \
		    --routines \
		    --add-drop-table \
		    --disable-keys \
		    --skip-extended-insert \
		    --no-data \
		   --host=<HOSTIP> \
		   --port=3306  \
		    <DBNAME>
		  ```