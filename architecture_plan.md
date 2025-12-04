# Architecture and Implementation Plan

## Service mapping
  
| Layer               | Service (Cloud)                              | Role in Solution                                           | Related Assignment/Module |
|---------------------|----------------------------------------------|------------------------------------------------------------|---------------------------|
| Frontend/API        | Cloud Run                                    | Host Flask web app for user interface, file uploading, and dashboard visualization    | Assignment 2       |
| Storage             | GCP Cloud Storage                            | Store raw uploaded CSV files with versioning               | Module 6                  |
| Compute             | Cloud functions                              | Serverless functions for automated data cleaning           | Assignment 3/Module 5     |
| Database/SQL        | Cloud SQL                                    | Store cleaned claims data in relational tables with indexes| Assignment 4/Module 7     |
| Analytics           | BigQuery                                     | Analytics engine for complex aggregations and trend analysis     | Module 7            |
| Secrets Management  | Secret Manager                               | Store database passwords and API keys securely             |        |
| AI                  | Vertex AI                                    | Predict claim denial chance or outlier costs               | Module 9                  |

## Data flow narrative
1. User exports the csv files from their billing system and uploads it via Flask.
2. The csv file is stored in the cloud storage.
3. The csv file is then organized based on the upload date.
4. A cloud function is triggered automatically by the storage event.
5. The function loads the data into a cloud SQL database.
6. The function performs data cleaning.
7. The cleaned data is loaded into a new csv file stored in the dashboard.
8. User goes on the dashboard and accesses the cleaned data.
9. An API runs to generate summary tables for the user.

## Security, identity, and governance basics
