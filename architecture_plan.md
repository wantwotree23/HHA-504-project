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
User credential/authentication will be set in place to make sure that the right person is accessing the Flask app dashboard. There will be a requirement to log in to the Flask app using 2fa and also an orginization email. Different permission levels will be granted to different accounts on the Flask app. Some users can upload csv files and generate cleaned data while other users may only read the files within the dashboard. To avoid putting real PHI information in public environments, the uploaded csv files must be all de-itentified of all patient information. The data with the SQL database and cloud storage will all be encrypted for security purposes. Database passwords will be stored in Secret Manager.

## Cost and operational considerations
Within GCP, the service that might cost the most monthly is Cloud SQL database. This is due to the managed version of Cloud SQL that handles the full infrastructure management. The second costly service would be cloud run which hosts the Flask web app. Other functions which GCP are not as resource intensive monthly. I chose to use serverless rather than always-on VM because healthcare organization may send batches of claims periodically rather than every day. So it is not necessary to have the Flask app running the whole time. 

To keep this Flask app in a "student budget" I have focused on services that depend on low resources and are cheap to run. For example, for Cloud run I would make sure that the instances set are to 1 only and make sure that it doesn't charge a cost when idle. Also use the smalles instance available for Cloud SQL. Furtheremore, I decided to keep all this services serverless to only pay when the database is active.