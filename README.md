# JobsPipeline

Welcome to the JobsPipeline project! This repository is dedicated to the time I spent searching for jobs. I dedicated three hours per day to searching for jobs. I dreamt of automation that could save me time. So here is the result!

## Table of Contents

- [Introduction](#introduction)
- [Architecture Diagram](#architecture)


## Introduction

**JobsPipeline** is a serverless AWS-based project designed to automate and streamline the job search process, alleviating the tedious tasks that most job seekers face. By leveraging the **Coresignal API**, it fetches job data directly from LinkedIn, processes it through a robust AWS workflow, and delivers actionable insights through Grafana dashboards.

This project utilizes a combination of AWS services, including **Lambda**, **Kinesis Firehose**, **S3**, **Glue Crawler**, **Glue ETL**, **EventBridge**, and **CloudWatch**, to ensure a seamless, efficient, and scalable pipeline for data ingestion, processing, and visualization. The processed data is made accessible and insightful by connecting **Athena** to Grafana for real-time visualization, empowering users with a comprehensive view of job opportunities.

## Architecture Diagram

![Alt Text](path/to/image.png)



