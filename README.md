# Healthcare Insurance Analytics Platform — Capstone Project 

## What I Built

This project is an end-to-end data pipeline for a health insurance company. I take raw patient, subscriber, claims, and group/subgroup data, clean it, load it into a data warehouse, and generate 13 business-question reports from it.

## How I Built It

I started by generating sample data for the four source tables, since I didn't have the real dataset, and intentionally added some messy values (nulls and duplicates) so I'd have real cleaning work to do.

I wrote my pipeline in Python using PySpark, developed and tested entirely locally in PyCharm (instead of Databricks). The pipeline has two stages: first, a set of cleaning scripts that read each raw table, report and handle null values, remove duplicates, and write the cleaned data back out. Second, a set of 13 separate scripts — one per business use case (e.g. which disease has the most claims, which hospital sees the most patients, the most profitable subscriber group) — that read the cleaned data and produce one result table per use case.

For storage and the data warehouse, I used AWS. I created an S3 bucket to hold the raw data, the cleaned data, and the final results. I set up an Amazon Redshift Serverless workgroup as my data warehouse, with two schemas: one for the cleaned source tables (with primary/foreign keys) and one holding the 13 output tables. To move data from S3 into Redshift, I used Redshift's native COPY command rather than a JDBC connection, since I wasn't running this on Databricks.

I version-controlled the whole project in Git and pushed it to GitHub.

## Why I Made These Choices

I chose a Bronze-Silver-Gold style approach — raw data, then cleaned data, then business-ready output — because it keeps every stage traceable and easy to re-run independently if something changes upstream. I used PyCharm instead of Databricks because it let me develop and debug everything locally before touching any cloud resources, which made it much easier to catch and fix issues early.


## Author
- Ashwani Kaira
