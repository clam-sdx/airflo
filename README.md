# airflo
mini intro to airflow data pipelines 

## Setup

### Install `uv` with one of

```python
curl -LsSf https://astral.sh/uv/install.sh | sh
wget -qO- https://astral.sh/uv/install.sh | sh
```

If `which -a uv` returns nothing, then the "shadowed commands" warning can be ignored.
If `echo $SHELL` returns `/bin/bash` or `/bin/zsh`, use: `source $HOME/.local/bin/env`

Install a version of python thats >=3.11 and use that python version in a virtual environment

Within the root `airflo/` directory do:
```python

uv python install 3.11
uv venv .venv --python 3.11
source .venv/bin/activate
uv pip install "apache-airflow[celery]==2.10.5" --constraint "https://raw.githubusercontent.com/apache/airflow/constraints-2.10.5/constraints-3.11.txt"

# Make sure AIRFLOW_HOME is set to your project directory
export AIRFLOW_HOME=$(pwd)

# Remove any existing database file (typically airflow.db)
rm -f airflow.db

# Initialize the database
airflow db init

# Create an admin user
airflow users create \
    --username admin \
    --firstname Admin \
    --lastname User \
    --role Admin \
    --email admin@example.com \
    --password admin

airflow webserver -p 8080
```

in another terminal (after setting the same environment variable)
```
airflow scheduler
```

In your browser navigate to http://0.0.0.0:8080/dags/my_dag/grid?tab=graph


