# Serverless-Architecture-on-AWS
##Overview
This project demonstrates how to implement a **Serverless Architecture** on AWS.  
It is an inventory tracking system where stores upload CSV files to an S3 bucket.  
The solution automatically loads the data into DynamoDB, checks stock availability,  
and sends notifications when items are out of stock.

##  Architecture
The workflow is as follows:

1. **Upload inventory file** → An S3 bucket receives the file.
2. **S3 Event** → Triggers a Lambda function (`Load-Inventory`).
3. **Lambda (Load-Inventory)** → Reads the CSV and inserts items into DynamoDB.
4. **DynamoDB Stream** → Invokes another Lambda (`Check-Stock`).
5. **Lambda (Check-Stock)** → Checks if an item count is 0 → sends notification via SNS.
6. **SNS** → Sends an Email alert.

##  AWS Services Used
- **Amazon S3** → File storage & Lambda trigger.
- **AWS Lambda** → Serverless compute to process files.
- **Amazon DynamoDB** → NoSQL database for inventory data.
- **Amazon SNS** → Notifications when stock is out.

##  Lambda Functions

###  Load-Inventory Function
- Triggered by S3 event.
- Reads CSV file.
- Inserts data into DynamoDB.

Code:[Load-Inventory Code](./lambda-functions/load_inventory.py) 

###  Check-Stock Function
- Triggered by DynamoDB Stream.
- Checks item count.
- Sends notification via SNS if stock is `0`.
Code:  [Check-Stock Code](./lambda-functions/check_stock.py)

## Results
- Inventory data successfully loaded into DynamoDB.  
- Dashboard displays real-time inventory status.  
- SNS notification sent when an item is out of stock. 

##  Conclusion
This project helped me practice:
- Building **Serverless applications** on AWS.  
- Integrating multiple AWS services (S3, Lambda, DynamoDB, SNS, Cognito).  
- Automating workflows without managing servers.  




