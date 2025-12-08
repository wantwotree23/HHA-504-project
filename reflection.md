# Reflection

## Area of confidence
I feel confident about the data processing pipeline. Having the processing step to be event-driven helps by having the server only be on when the user accesses it and uploads a csv file. In addition, the scripts to process the data are created with python using the pandas library which utilizes my current experience from previous modules and assignments that handled example data and worked with python scripts. Automated triggering of processing after upload of csv eliminates the need for manual job scheduling or user intervention. I also feel confident regarding the data schema and relational database structure with claims tables. Using main indexes such as `claims_id`, `service_date`, and `provider_id` that is most commonly shared among different billing systems. In addition, I'm also confident about the cost management strategies applied. Cost are minimized by using free tier resources, and the lowest cost SQL database and cloud storage. Using a serverless approach further lowers cost by having the application turn on only when a user opens the application. 

Something that I feel less confident about is the implementation of the secret manager. I understand the basic concept of GCP secret manager but haven't used it in a real application before. I'm also less confident in the ability for the application to expand in utilization. If there were more users to upload csv files and generate reports, the scalability of the database and application might not function properly. Lastly, I'm not confident about how the application and database handles errors.

## Alternative architecture
An alternative architecture that I have considered was a full VM based application with a similar data pipeline. The benefit of utilizing a full VM based application allows for low cost and easy user configuration of the VM. However, scaling up the VM requires manual resizing of the VM. Furthermore, I will have to be manually monitoring all the logs in case any errors occur. Lastly, if the VM crashes, the whole application shuts down. I didn't go through with this alternative because of these drawbacks.

Another alternative architecture that I considered was a full serverless application by using GCP functions and API gateways. This was considered for the absolutely low cost since it only charges the me for each individual use of the application. A drawback with this approach is that the application requires a cold start every time the user wants to access it. Another drawback is that it is more of a hassle to develop the data pipeline with separated functions than to develop the whole thing on Flask. I didn't go through with this alternative architecture due to these drawbacks.

## Next steps of implementation with more time and credits
1. Enhance user experience
    - Ability for users to make custom dashboards by rearranging tabs.
    - Have a built in AI that answers user questions.
    - Be able to schedule the reports to be electronically sent to the user.
2. ML implementation
    - Have AI predict claims success/denial rate.
    - Have AI detect and flag abnormal data or trends.
3. Enhance data handling
    - Replace manual upload of csv files by connecting the to the billing systems through an API.