---
layout: post
title:  "Data Pipelines with Airflow - Context variables"
date:   2021-03-25 09:04:00
categories: airflow
---

##### Notes from Udacity Data Engineering Nano Degree - lesson 1 chapter 25

### Context variables 
Context variables are useful for accesing or segmenting data before prosessing.

The following function will:
- get the name variable `execution_date` out of the key word argument.
- `execution_date` is coming from the provided context in the `PythonOperator(..., provide_context=True)`
- When we provide a context Airflow is going to pass through a number of runtime variables to the application such that we could access them in our python functions or in other operators. 

{% highlight python %}
import datetime
import logging

from airflow import DAG
from airflow.models import Variable
from airflow.operators.python_operator import PythonOperator
from airflow.hooks.S3_hook import S3Hook


def log_details(*args, **kwargs):
    #
    # Extracting ds, run_id, prev_ds, and next_ds from the kwargs, and log them
    # Availiable context variables passed in on kwargs:
    # https://airflow.apache.org/macros.html
    #

    ds = kwargs['ds']
    run_id = kwargs['run_id']
    previous_ds = kwargs.get('previous_ds')
    next_ds = kwargs.get('previous_ds')

    logging.info(f"Execution date is {ds}")
    logging.info(f"My run id is {run_id}")
    if previous_ds:
        logging.info(f"My previous run was on {previous_ds}")
    if next_ds:
        logging.info(f"My next run will be {next_ds}")

dag = DAG(
    'demo_log_details',
    schedule_interval="@daily",
    start_date=datetime.datetime.now() - datetime.timedelta(days=2)
)

list_task = PythonOperator(
    task_id="log_details",
    python_callable=log_details,
    provide_context=True,
    dag=dag
)
{% endhighlight %}