## ⭕Error: 
- ModuleNotFoundError: No module named `'airflow.providers.github'`

## 👇🏼Reason:
- Airflow container is isolated so, although installing the pakages from `pip install` could not help. 

## ✅Solution: 
### Made custome build 🐋

- Do foll changes in `docker-compose.yaml`
```python
x-airflow-common:
&airflow-common
# Comment the image line, place your Dockerfile in the directory.
# and uncomment the "build" line below, Then run `docker-compose build` to build the images.
# image: ${AIRFLOW_IMAGE_NAME:-apache/airflow:3.0.3}
build: .
```

- Write `requirements.txt` with neccessory packages
- Make `Dockerfile` as follows

```python
ARG AIRFLOW_VERSION=3.0.3
FROM apache/airflow:${AIRFLOW_VERSION}

USER airflow

COPY requirements.txt /requirements.txt

RUN pip install --no-cache-dir \
      "apache-airflow==${AIRFLOW_VERSION}" \
      -r /requirements.txt
```

- Run following commands
```python
docker compose up airflow-init
docker compose up -d --build
```

## Other Errors came under the process
- ImportError: cannot import name `'GitHubOperator'` from `'airflow.providers.github.operators.github'` 

## 🧠 Root Cause

The class was incorrectly imported as:

```python
GitHubOperator
But the actual class name is spelled with a lowercase "h": GithubOperator