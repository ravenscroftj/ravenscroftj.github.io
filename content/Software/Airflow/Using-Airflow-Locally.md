---
created: 2024-01-30T13:10
updated: 2024-01-30T15:03
---
## Local Installation

In order to install [[Public/Software/Airflow/index]] locally you can use the following bash script to bootstrap the process.
 
```shell
  # Airflow needs a home. `~/airflow` is the default, but you can put it
  # somewhere else if you prefer (optional)
  export AIRFLOW_HOME=~/airflow
  
  # Install Airflow using the constraints file
  AIRFLOW_VERSION=2.5.3
  PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
  # For example: 3.7
  CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
  # For example: https://raw.githubusercontent.com/apache/airflow/constraints-2.5.3/constraints-3.7.txt
  pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"

  #--------------------------
  #
  # NB: Before running the next step it is probably worth configuring the DB
  #
  #--------------------------
  # The Standalone command will initialise the database, make a user,
  # and start all components for you.
  airflow db init
  
  # Visit localhost:8080 in the browser and use the admin account details
  # shown on the terminal to login.
  # Enable the example_bash_operator DAG in the home page
```

## Config File

There is a file named `airflow.cfg` which contains configuration for your airflow instance including the full path to the DAGs folder and also SQLalchemy connection credentials.

### Initialise Airflow User
```bash
airflow users create -u airflow -p airflow --role Admin -e test@test.com -f test -l test
```
### Postgres Data Storage

Use the `psycopg2-binary` package to provide [[PostgreSQL]] db support:

`pip install psycopg2-binary`

And in the config:

`sql_alchemy_conn = postgresql+psycopg2://airflow:airflow@localhost/airflow`

The easiest solution is to use a [[Public/Software/PostgreSQL|PostgreSQL]] Docker setup.

