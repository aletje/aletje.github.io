---
layout: post
title:  "Data Pipelines with Airflow - variables and connections for S3 bucket"
date:   2021-03-24
categories: airflow
---

##### Notes from Udacity Data Engineering Nano Degree - lesson 1 chapter 22

### create variables and connections in Airflow for AWS S3 bucket.
1. Open your browser to localhost:8080 and open Admin->Variables
2. Click "Create"
3. Set "Key" equal to "s3_bucket" and set "Val" equal to "udacity-dend"
4. Set "Key" equal to "s3_prefix" and set "Val" equal to "data-pipelines"
5. Click save
6. Open Admin->Connections
7. Click "Create"
8. Set "Conn Id" to "aws_credentials", "Conn Type" to "Amazon Web Services"
9. Set "Login" to your aws_access_key_id and "Password" to your aws_secret_key
10. Click save
11. Run the DAG