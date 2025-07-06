Real-Time AWS Data Processing Pipeline

This project demonstrates how to build a real-time data processing pipeline using AWS services. It's ideal for handling data from IoT sensors or any live data stream.

1) What This Project Does

   a) This pipeline receives "real-time sensor data", processes it, stores the "raw data in Amazon S3" and saves a "summary of the latest readings in DynamoDB".

   b) It’s a simplified version of what many companies use for real-time monitoring systems (e.g., smart homes, factory sensors, etc.).

2) AWS Services Used

       | Service        | Purpose                                                 |
       |----------------|---------------------------------------------------------|
       | Amazon Kinesis | Ingests real-time data (e.g., from IoT sensors)         |
       | AWS Lambda     | Processes each data record as it arrives                |
       | Amazon S3      | Stores raw data files (in JSON format)                  |
       | DynamoDB       | Stores the latest temperature reading per device        |
       | IAM            | Provides permissions for Lambda to access S3 & DynamoDB |

3) Project Structure

       real-time-pipeline/
       ├── lambda/
       │ └── process_stream.py # Python code for processing data
       ├── iam/
       │ └── lambda_role_policy.json # IAM permissions for the Lambda function
       ├── cloudformation/
       │ └── pipeline_stack.yaml # AWS CloudFormation to set up the infrastructure
       └── README.md # Project documentation

4) Sample Data (Sent to Kinesis)

    json
   
       {
         "device_id": "sensor-123",
         "temperature": 27.5
       }

  This sample simulates a device sending temperature data.

5) How It Works :

   1) Sensor or data source sends data to a Kinesis stream.

   2) Lambda function automatically triggers for every new record:
 
      a) Decodes the record

      b) Saves raw JSON data to an S3 bucket

      c) Updates the latest temperature in DynamoDB

   3) You can view:

      a) Raw data in the S3 bucket

      b) Latest temperature per device in DynamoDB

6) Deployment Instructions

   You must have an AWS account with necessary permissions.

   1) Deploy the Infrastructure

      Use AWS CloudFormation with pipeline_stack.yaml to create:

      a) Kinesis Stream

      b) S3 bucket

      c) DynamoDB table

      d) IAM role

      e) Lambda function 

   2) Upload the Lambda Code

      a) Zip the process_stream.py file and upload it to S3.

   3) Test It

      a) Use the AWS Kinesis console or AWS CLI to send a test record like the one above.

7)  Use Cases

    1) IoT monitoring (temperature, pressure, location, etc.)

    2) Real-time analytics dashboards

    3) Fraud detection or alerting systems

    4) Smart agriculture or factory systems

