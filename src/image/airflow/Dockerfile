#FROM apache/airflow:2.8.1
FROM apache/airflow:latest

USER root

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
  openjdk-17-jre-headless \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* 

RUN pip install apache-airflow-providers-airbyte
USER airflow

RUN pip install --upgrade pip

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

COPY requirements.txt /requirements.txt

# Copy dags
COPY ./dags /opt/airflow/dags

# Copy plugins
COPY ./plugins /opt/airflow/plugins

RUN pip install --no-cache-dir "apache-airflow==${AIRFLOW_VERSION}" -r /requirements.txt

#FROM quay.io/astronomer/astro-runtime:5.0.1
FROM quay.io/astronomer/astro-runtime:11.3.0

# install dbt into a virtual environment
RUN python -m venv dbt_venv && source dbt_venv/bin/activate && \
    pip install --no-cache-dir dbt-snowflake && deactivate
    
RUN pip install apache-airflow-providers-airbyte[http] \
    && pip install apache-airflow-providers-airbyte
