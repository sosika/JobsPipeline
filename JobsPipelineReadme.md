
# Jobs Pipeline README

## Overview

This project provides an automated pipeline for job data ingestion, transformation, and visualization. The pipeline leverages Coresignal's LinkedIn data partner API, AWS services, and Grafana for robust data management and insights.

---

## Data Ingestion

### Coresignal API Integration
Since LinkedIn prohibits scraping, this pipeline utilizes Coresignal, LinkedIn's official partner, to gather job postings. 
- **API Features**: Job Search and Collect Endpoints
- **Focus**: Remote Program Manager positions in the US within the software development industry.
- **Filter Criteria**:
  ```json
  {
    "application_active": true,
    "last_updated_gte": "2024-12-01 00:00:01",
    "country": "United States",
    "title": "(Program manager) AND (Remote)",
    "deleted": 0,
    "industry": "Software development"
  }
  ```
- **Lambda Functions**:
  - **Job Search Function**: Pulls job IDs matching the filter criteria.
  - **Job Collect Function**: Fetches detailed job data using job IDs.
- **Data Storage**: Results are streamed to S3 buckets (`myjobsdata` and `jobs-with-details`) via Firehose for further processing.

### Scheduling
- **Automation**: EventBridge schedules API pulls to ensure consistent and timely ingestion.

---

## Data Transformation

### AWS Glue
- **Glue Crawlers**: Extract and structure job data into AWS Athena tables:
  - `jobs` table: Contains `job_id`.
  - `jobdetails` table: Includes details such as job ID, title, company, description, salary, etc.
- **Data Format**: 
  - **Parquet**: Chosen for optimized querying and efficient storage.
- **ETL Workflow**:
  1. Trigger `Jobs_crawler` to create the `jobs_myjobsdata` table.
  2. Execute `ExtractJobDetails` crawler to build the `jobdetails` table.
  3. Refresh Parquet table by deleting and recreating it.
  4. Perform data quality checks for missing or invalid data:
     - Null `job_id`, `job title`, or `company name`.
  5. Generate a production-ready Parquet table.

---

## Visualization

### Grafana Integration
- **Setup**:
  - Use `grafana-athena-datasource` for data visualization.
  - Generate AWS IAM access and secret keys for integration.
- **Features**:
  - Write custom Athena queries to visualize job metrics effectively.

---

## Monitoring & Automation

- **Monitoring**: Use AWS CloudWatch for job status tracking.
- **Alerts**: Set notifications for job failures to ensure pipeline reliability.

---

## Next Steps

1. Ensure API credentials and AWS configurations are correctly set up.
2. Run the Lambda Functions to initiate data ingestion.
3. Monitor and validate the ETL workflow for data integrity.
4. Explore Grafana dashboards for actionable insights.
