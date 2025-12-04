# Use Case: Cloud-based claims processing and analytics dashboard

## Problem statement
Healthcare organizations process mass claims every single day. The main problem that they face is incosistent file formats leading to a lot of manual processing of the files, compiling them into a single format, and generating insightful reports from the data. This lengthly process cost the organizations a lot of resources and manpower. Furthermore, it slows down the claim submission process leading to delays in financial decisions and lack of timely insights from claim patterns.

### Solution
Automated cloud-based claims processing pipeline that ingests raw data files, cleans and standardizes the data, stores it as a new SQL database, then provides dashboard for analysis.

### Target Users
1. Healthcare financial analyst:
    - They analyze the claims cost patterns.
    - They clean the data and generate reports.
2. Revenue cycle managers:
    - They monitor claim submission and approval/reject rates.
    - Check for claims that need further handling.
    - Take care of billing process.
3. Administrators:
    - Use the dashboards to see the analysis and reports.
    - Compare performance of departments.
    - Use the analysis and reports to make data-driven decisions relating to performance and cost.

## Data sources
Primary Data: Claims CSV Files with the following key fields
`Claim_ID`, `Provider_ID`, `Procedure_code`, `Diagnosis_code`, `service_date`, `Payer`, `Claim_amnt`, `Paid_amnt`, `claim_status`, `Location`

Data source: CSV files exported from billing systems

## Basic workflow
1. Data upload
    - User enters the flask application.
    - Upload the claims files into the application.
2. File storage
    - The uploaded CSV files are stored in the cloud storage.
    - Files auto-organize based on upload date.
3. Data loading
    - The csv file loads into a cloud SQL database.
4. Data processing
    - User selects which uploaded files to autoprocess.
    - A logs report is generated to show simple statistics of the file processed (rows processed, null values).
    - The processed file is then stored in another tab where the user can access.
5. Analytics processing
    - Automatic queries are performed on the processed data and generates results that are stored in summary tables within the dashboard.
6. Dashboard visualization
    - User access the analytics function within the application.
    - The dashboard queries the summary tables.
    - The user can filter the data by all the key fields.
    - The user also has the option to generate and export a report to either PDF or csv format.