A company is implementing an application on Amazon EC2 instances. The application needs to process incoming transactions. When the application detects a transaction that is not valid, the application must send a chat message to the company's support team. To send the message, the application needs to retrieve the access token to authenticate by using the chat API.
A developer needs to implement a solution to store the access token. The access token must be encrypted at rest and in transit. The access token must also be accessible from other AWS accounts.
Which solution will meet these requirements with the LEAST management overhead?

A. Use an AWS Systems Manager Parameter Store SecureString parameter that uses an AWS Key Management Service (AWS KMS) AWS managed key to store the access token. Add a resource-based policy to the parameter to allow access from other accounts. Update the IAM role of the EC2 instances with permissions to access Parameter Store. Retrieve the token from Parameter Store with the decrypt flag enabled. Use the decrypted access token to send the message to the chat.
B. Encrypt the access token by using an AWS Key Management Service (AWS KMS) customer managed key. Store the access token in an Amazon DynamoDB table. Update the IAM role of the EC2 instances with permissions to access DynamoDB and AWS KMS. Retrieve the token from DynamoDDecrypt the token by using AWS KMS on the EC2 instances. Use the decrypted access token to send the message to the chat.
C. Use AWS Secrets Manager with an AWS Key Management Service (AWS KMS) customer managed key to store the access token. Add a resource-based policy to the secret to allow access from other accounts. Update the IAM role of the EC2 instances with permissions to access Secrets Manager. Retrieve the token from Secrets Manager. Use the decrypted access token to send the message to the chat.
D. Encrypt the access token by using an AWS Key Management Service (AWS KMS) AWS managed key. Store the access token in an Amazon S3 bucket. Add a bucket policy to the S3 bucket to allow access from other accounts. Update the IAM role of the EC2 instances with permissions to access Amazon S3 and AWS KMS. Retrieve the token from the S3 bucket. Decrypt the token by using AWS KMS on the EC2 instances. Use the decrypted access token to send the massage to the chat.

Correct Answer:  C 不确定

要跨account访问

---

A company is running Amazon EC2 instances in multiple AWS accounts. A developer needs to implement an application that collects all the lifecycle events of the EC2 instances. The application needs to store the lifecycle events in a single Amazon Simple Queue Service (Amazon SQS) queue in the company's main AWS account for further processing.
Which solution will meet these requirements?

A. Configure Amazon EC2 to deliver the EC2 instance lifecycle events from all accounts to the Amazon EventBridge event bus of the main account. Add an EventBridge rule to the event bus of the main account that matches all EC2 instance lifecycle events. Add the SQS queue as a target of the rule.
B. Use the resource policies of the SQS queue in the main account to give each account permissions to write to that SQS queue. Add to the Amazon EventBridge event bus of each account an EventBridge rule that matches all EC2 instance lifecycle events. Add the SQS queue in the main account as a target of the rule.
C. Write an AWS Lambda function that scans through all EC2 instances in the company accounts to detect EC2 instance lifecycle changes. Configure the Lambda function to write a notification message to the SQS queue in the main account if the function detects an EC2 instance lifecycle change. Add an Amazon EventBridge scheduled rule that invokes the Lambda function every minute.
D. Configure the permissions on the main account event bus to receive events from all accounts. Create an Amazon EventBridge rule in each account to send all the EC2 instance lifecycle events to the main account event bus. Add an EventBridge rule to the main account event bus that matches all EC2 instance lifecycle events. Set the SQS queue as a target for the rule. 
    
Correct Answer: D 

要跨account传递消息，用event bridge

---

An application is using Amazon Cognito user pools and identity pools for secure access. A developer wants to integrate the user-specific file upload and download features in the application with Amazon S3. The developer must ensure that the files are saved and retrieved in a secure manner and that users can access only their own files. The file sizes range from 3 KB to 300 MB.
Which option will meet these requirements with the HIGHEST level of security?

A. Use S3 Event Notifications to validate the file upload and download requests and update the user interface (UI).
B. Save the details of the uploaded files in a separate Amazon DynamoDB table. Filter the list of files in the user interface (UI) by comparing the current user ID with the user ID associated with the file in the table.
C. Use Amazon API Gateway and an AWS Lambda function to upload and download files. Validate each request in the Lambda function before performing the requested operation.
D. Use an IAM policy within the Amazon Cognito identity prefix to restrict users to use their own folders in Amazon S3. 

Correct Answer: D

前两个狗屁不通，C选项自己实现验证也是狗屁不通，D是对的
Amazon Cognito identity prefix指的应该是
```json
      "Condition": {
        "StringLike": {
          "s3:prefix": [
            "cognito/application-name/${cognito-identity.amazonaws.com:sub}/*"
          ]
        }
```
https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/reference_policies_examples_s3_cognito-bucket.html

---

A company is building a scalable data management solution by using AWS services to improve the speed and agility of development. The solution will ingest large volumes of data from various sources and will process this data through multiple business rules and transformations.
The solution requires business rules to run in sequence and to handle reprocessing of data if errors occur when the business rules run. The company needs the solution to be scalable and to require the least possible maintenance.
Which AWS service should the company use to manage and automate the orchestration of the data flows to meet these requirements?

A. AWS Batch
B. AWS Step Functions
C. AWS Glue
D. AWS Lambda

Correct Answer: B

step function：无服务器、工作流程、顺序、出错也可以retry和catch

https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html

---

A developer has created an AWS Lambda function that is written in Python. The Lambda function reads data from objects in Amazon S3 and writes data to an Amazon DynamoDB table. The function is successfully invoked from an S3 event notification when an object is created. However, the function fails when it attempts to write to the DynamoDB table.
What is the MOST likely cause of this issue?

A. The Lambda function's concurrency limit has been exceeded.
B. DynamoDB table requires a global secondary index (GSI) to support writes.
C. The Lambda function does not have IAM permissions to write to DynamoDB.
D. The DynamoDB table is not running in the same Availability Zone as the Lambda function.

Correct Answer: C

---

A developer is creating an AWS CloudFormation template to deploy Amazon EC2 instances across multiple AWS accounts. The developer must choose the EC2 instances from a list of approved instance types.
How can the developer incorporate the list of approved instance types in the CloudFormation template?

A. Create a separate CloudFormation template for each EC2 instance type in the list.
B. In the Resources section of the CloudFormation template, create resources for each EC2 instance type in the list.
C. In the CloudFormation template, create a separate parameter for each EC2 instance type in the list.
D. In the CloudFormation template, create a parameter with the list of EC2 instance types as AllowedValues.

Correct Answer: D

---

A developer has an application that makes batch requests directly to Amazon DynamoDB by using the BatchGetItem low-level API operation. The responses frequently return values in the UnprocessedKeys element.
Which actions should the developer take to increase the resiliency of the application when the batch response includes values in UnprocessedKeys? (Choose two.)

A. Retry the batch operation immediately.
B. Retry the batch operation with exponential backoff and randomized delay.
C. Update the application to use an AWS software development kit (AWS SDK) to make the requests.
D. Increase the provisioned read capacity of the DynamoDB tables that the operation accesses.
E. Increase the provisioned write capacity of the DynamoDB tables that the operation accesses.

Correct Answer: B 和 C

D好像也对，不确定

The AWS SDKs implement automatic retry logic and exponential backoff.

BatchGetItem：  UnprocessedKeys for failed read operations (exponential backoff or add RCU)

---

A company is running a custom application on a set of on-premises Linux servers that are accessed using Amazon API Gateway. AWS X-Ray tracing has been enabled on the API test stage.
How can a developer enable X-Ray tracing on the on-premises servers with the LEAST amount of configuration?

A. Install and run the X-Ray SDK on the on-premises servers to capture and relay the data to the X-Ray service.
B. Install and run the X-Ray daemon on the on-premises servers to capture and relay the data to the X-Ray service.
C. Capture incoming requests on-premises and configure an AWS Lambda function to pull, process, and relay relevant data to X-Ray using the PutTraceSegments API call.
D. Capture incoming requests on-premises and configure an AWS Lambda function to pull, process, and relay relevant data to X-Ray using the PutTelemetryRecords API call.

Correct Answer: B 

---

Question #9

A company wants to share information with a third party. The third party has an HTTP API endpoint that the company can use to share the information. The company has the required API key to access the HTTP API.
The company needs a way to manage the API key by using code. The integration of the API key with the application code cannot affect application performance.
Which solution will meet these requirements MOST securely?

A. Store the API credentials in AWS Secrets Manager. Retrieve the API credentials at runtime by using the AWS SDK. Use the credentials to make the API call.
B. Store the API credentials in a local code variable. Push the code to a secure Git repository. Use the local code variable at runtime to make the API call.
C. Store the API credentials as an object in a private Amazon S3 bucket. Restrict access to the S3 object by using IAM policies. Retrieve the API credentials at runtime by using the AWS SDK. Use the credentials to make the API call.
D. Store the API credentials in an Amazon DynamoDB table. Restrict access to the table by using resource-based policies. Retrieve the API credentials at runtime by using the AWS SDK. Use the credentials to make the API call.

Correct Answer: A

---

Question #10

A developer is deploying a new application to Amazon Elastic Container Service (Amazon ECS). The developer needs to securely store and retrieve different types of variables. These variables include authentication information for a remote API, the URL for the API, and credentials. The authentication information and API URL must be available to all current and future deployed versions of the application across development, testing, and production environments.
How should the developer retrieve the variables with the FEWEST application changes?

A. Update the application to retrieve the variables from AWS Systems Manager Parameter Store. Use unique paths in Parameter Store for each variable in each environment. Store the credentials in AWS Secrets Manager in each environment.
B. Update the application to retrieve the variables from AWS Key Management Service (AWS KMS). Store the API URL and credentials as unique keys for each environment.
C. Update the application to retrieve the variables from an encrypted file that is stored with the application. Store the API URL and credentials in unique files for each environment.
D. Update the application to retrieve the variables from each of the deployed environments. Define the authentication information and API URL in the ECS task definition as unique names during the deployment process.

Correct Answer: A

---

Question #11

A company is migrating legacy internal applications to AWS. Leadership wants to rewrite the internal employee directory to use native AWS services. A developer needs to create a solution for storing employee contact details and high-resolution photos for use with the new application.
Which solution will enable the search and retrieval of each employee's individual details and high-resolution photos using AWS APIs?

A. Encode each employee's contact information and photos using Base64. Store the information in an Amazon DynamoDB table using a sort key.
B. Store each employee's contact information in an Amazon DynamoDB table along with the object keys for the photos stored in Amazon S3.
C. Use Amazon Cognito user pools to implement the employee directory in a fully managed software-as-a-service (SaaS) method.
D. Store employee contact information in an Amazon RDS DB instance with the photos stored in Amazon Elastic File System (Amazon EFS).

Correct Answer: B

---

Question #12

A developer is creating an application that will give users the ability to store photos from their cellphones in the cloud. The application needs to support tens of thousands of users. The application uses an Amazon API Gateway REST API that is integrated with AWS Lambda functions to process the photos. The application stores details about the photos in Amazon DynamoDB.
Users need to create an account to access the application. In the application, users must be able to upload photos and retrieve previously uploaded photos. The photos will range in size from 300 KB to 5 MB.
Which solution will meet these requirements with the LEAST operational overhead?

A. Use Amazon Cognito user pools to manage user accounts. Create an Amazon Cognito user pool authorizer in API Gateway to control access to the API. Use the Lambda function to store the photos and details in the DynamoDB table. Retrieve previously uploaded photos directly from the DynamoDB table.
B. Use Amazon Cognito user pools to manage user accounts. Create an Amazon Cognito user pool authorizer in API Gateway to control access to the API. Use the Lambda function to store the photos in Amazon S3. Store the object's S3 key as part of the photo details in the DynamoDB table. Retrieve previously uploaded photos by querying DynamoDB for the S3 key.
C. Create an IAM user for each user of the application during the sign-up process. Use IAM authentication to access the API Gateway API. Use the Lambda function to store the photos in Amazon S3. Store the object's S3 key as part of the photo details in the DynamoDB table. Retrieve previously uploaded photos by querying DynamoDB for the S3 key.
D. Create a users table in DynamoDB. Use the table to manage user accounts. Create a Lambda authorizer that validates user credentials against the users table. Integrate the Lambda authorizer with API Gateway to control access to the API. Use the Lambda function to store the photos in Amazon S3. Store the object's S3 key as par of the photo details in the DynamoDB table. Retrieve previously uploaded photos by querying DynamoDB for the S3 key.

Correct Answer: B 

---

Question #13

A company receives food orders from multiple partners. The company has a microservices application that uses Amazon API Gateway APIs with AWS Lambda integration. Each partner sends orders by calling a customized API that is exposed through API Gateway. The API call invokes a shared Lambda function to process the orders.
Partners need to be notified after the Lambda function processes the orders. Each partner must receive updates for only the partner's own orders. The company wants to add new partners in the future with the fewest code changes possible.
Which solution will meet these requirements in the MOST scalable way?

A. Create a different Amazon Simple Notification Service (Amazon SNS) topic for each partner. Configure the Lambda function to publish messages for each partner to the partner's SNS topic.
B. Create a different Lambda function for each partner. Configure the Lambda function to notify each partner's service endpoint directly.
C. Create an Amazon Simple Notification Service (Amazon SNS) topic. Configure the Lambda function to publish messages with specific attributes to the SNS topic. Subscribe each partner to the SNS topic. Apply the appropriate filter policy to the topic subscriptions.
D. Create one Amazon Simple Notification Service (Amazon SNS) topic. Subscribe all partners to the SNS topic.

Correct Answer: C 

https://docs.aws.amazon.com/sns/latest/dg/sns-message-filtering.html
默认情况下，Amazon SNS 主题订阅者会收到发布到该主题的每条消息。要仅接收一部分消息，订阅者必须将筛选策略 分配给主题订阅。

筛选策略是一个 JSON 对象，包含定义订阅者接收的消息的属性。根据您为订阅设置的筛选策略范围，Amazon SNS 支持对消息属性或消息正文进行操作的策略。消息正文的筛选策略假设消息有效负载是格式正确的 JSON 对象。

如果某个订阅没有筛选策略，则订阅者将接收发布到其主题的每条消息。当您将一条消息发布到具有筛选策略的某个主题时，Amazon SNS 会为该主题的每个订阅，将消息属性或消息正文与筛选策略中的操作进行比较。如果任何消息属性或消息正文匹配，Amazon SNS 会将消息发送给订阅者。否则，Amazon SNS 不会将消息发送给该订阅者。


---

Question #14

A financial company must store original customer records for 10 years for legal reasons. A complete record contains personally identifiable information (PII). According to local regulations, PII is available to only certain people in the company and must not be shared with third parties. The company needs to make the records available to third-party organizations for statistical analysis without sharing the PII.
A developer wants to store the original immutable record in Amazon S3. Depending on who accesses the S3 document, the document should be returned as is or with all the PII removed. The developer has written an AWS Lambda function to remove the PII from the document. The function is named removePii.
What should the developer do so that the company can meet the PII requirements while maintaining only one copy of the document?

A. Set up an S3 event notification that invokes the removePii function when an S3 GET request is made. Call Amazon S3 by using a GET request to access the object without PII.
B. Set up an S3 event notification that invokes the removePii function when an S3 PUT request is made. Call Amazon S3 by using a PUT request to access the object without PII.
C. Create an S3 Object Lambda access point from the S3 console. Select the removePii function. Use S3 Access Points to access the object without PII.
D. Create an S3 access point from the S3 console. Use the access point name to call the GetObjectLegalHold S3 API function. Pass in the removePii function name to access the object without PII.

Correct Answer: C

https://aws.amazon.com/cn/s3/features/object-lambda/

借助 S3 Object Lambda，您可以将自己的代码添加到 S3 GET、HEAD 和 LIST 请求中，以便在数据返回到应用程序时修改和处理数据。您可以使用自定义代码来修改 S3 GET 请求返回的数据，以便实施筛选行、动态调整图像大小、隐去机密数据等操作。您还可以使用 S3 Object Lambda 来修改 S3 LIST 请求的输出，以创建存储桶中对象的自定义视图，并使用 S3 HEAD 请求修改对象元数据（如对象名称和大小）。在 AWS Lambda 函数的支持下，无需对应用程序进行任何更改，您的代码即可在 AWS 完全托管的基础设施上运行，不需要创建和存储数据的衍生副本，也不需要运行昂贵的代理。

access point是用来访问控制的

• Access Points simplify security management for S3 Buckets
• Each Access Point has:
• its own DNS name (Internet Origin or VPC Origin)
• an access point policy (similar to bucket policy) – manage security at scale

---

Question #15

A developer is deploying an AWS Lambda function The developer wants the ability to return to older versions of the function quickly and seamlessly.
How can the developer achieve this goal with the LEAST operational overhead?

A. Use AWS OpsWorks to perform blue/green deployments.
B. Use a function alias with different versions.
C. Maintain deployment packages for older versions in Amazon S3.
D. Use AWS CodePipeline for deployments and rollbacks.

Correct Answer: B 

---

Question #16

A developer has written an AWS Lambda function. The function is CPU-bound. The developer wants to ensure that the function returns responses quickly.
How can the developer improve the function's performance?

A. Increase the function's CPU core count.
B. Increase the function's memory.
C. Increase the function's reserved concurrency.
D. Increase the function's timeout.

Correct Answer: B

---

Question #17

For a deployment using AWS Code Deploy, what is the run order of the hooks for in-place deployments?

A. BeforeInstall -> ApplicationStop -> ApplicationStart -> AfterInstall
B. ApplicationStop -> BeforeInstall -> AfterInstall -> ApplicationStart
C. BeforeInstall -> ApplicationStop -> ValidateService -> ApplicationStart
D. ApplicationStop -> BeforeInstall -> ValidateService -> ApplicationStart

Correct Answer: B

https://docs.aws.amazon.com/zh_cn/codedeploy/latest/userguide/reference-appspec-file-structure-hooks.html#reference-appspec-file-structure-hooks-run-order-ecs

在install前要先stop
在start之后才能validate

ApplicationStop -> BeforeInstall -> AfterInstall -> ApplicationStart -> ValidateService

---

Question #18

A company is building a serverless application on AWS. The application uses an AWS Lambda function to process customer orders 24 hours a day, 7 days a week. The Lambda function calls an external vendor's HTTP API to process payments.
During load tests, a developer discovers that the external vendor payment processing API occasionally times out and returns errors. The company expects that some payment processing API calls will return errors.
The company wants the support team to receive notifications in near real time only when the payment processing external API error rate exceed 5% of the total number of transactions in an hour. Developers need to use an existing Amazon Simple Notification Service (Amazon SNS) topic that is configured to notify the support team.
Which solution will meet these requirements?

A. Write the results of payment processing API calls to Amazon CloudWatch. Use Amazon CloudWatch Logs Insights to query the CloudWatch logs. Schedule the Lambda function to check the CloudWatch logs and notify the existing SNS topic.
B. Publish custom metrics to CloudWatch that record the failures of the external payment processing API calls. Configure a CloudWatch alarm to notify the existing SNS topic when error rate exceeds the specified rate.
C. Publish the results of the external payment processing API calls to a new Amazon SNS topic. Subscribe the support team members to the new SNS topic.
D. Write the results of the external payment processing API calls to Amazon S3. Schedule an Amazon Athena query to run at regular intervals. Configure Athena to send notifications to the existing SNS topic when the error rate exceeds the specified rate.

Correct Answer: B 

Logs Insights是另一个东西，A太复杂
CloudWatch Logs Insights can be used to query logs and add queries to CloudWatch Dashboard

---

Question #19
A company is offering APIs as a service over the internet to provide unauthenticated read access to statistical information that is updated daily. The company uses Amazon API Gateway and AWS Lambda to develop the APIs. The service has become popular, and the company wants to enhance the responsiveness of the APIs.
Which action can help the company achieve this goal?

A. Enable API caching in API Gateway.
B. Configure API Gateway to use an interface VPC endpoint.
C. Enable cross-origin resource sharing (CORS) for the APIs.
D. Configure usage plans and API keys in API Gateway.

Correct Answer: A 

---

Question #20

A developer wants to store information about movies. Each movie has a title, release year, and genre. The movie information also can include additional properties about the cast and production crew. This additional information is inconsistent across movies. For example, one movie might have an assistant director, and another movie might have an animal trainer.
The developer needs to implement a solution to support the following use cases:
For a given title and release year, get all details about the movie that has that title and release year.
For a given title, get all details about all movies that have that title.
For a given genre, get all details about all movies in that genre.
Which data store configuration will meet these requirements?

A. Create an Amazon DynamoDB table. Configure the table with a primary key that consists of the title as the partition key and the release year as the sort key. Create a global secondary index that uses the genre as the partition key and the title as the sort key.
B. Create an Amazon DynamoDB table. Configure the table with a primary key that consists of the genre as the partition key and the release year as the sort key. Create a global secondary index that uses the title as the partition key.
C. On an Amazon RDS DB instance, create a table that contains columns for title, release year, and genre. Configure the title as the primary key.
D. On an Amazon RDS DB instance, create a table where the primary key is the title and all other data is encoded into JSON format as one additional column.

Correct Answer: A

---

Question #21

A developer maintains an Amazon API Gateway REST API. Customers use the API through a frontend UI and Amazon Cognito authentication.
The developer has a new version of the API that contains new endpoints and backward-incompatible interface changes. The developer needs to provide beta access to other developers on the team without affecting customers.
Which solution will meet these requirements with the LEAST operational overhead?

A. Define a development stage on the API Gateway API. Instruct the other developers to point the endpoints to the development stage.
B. Define a new API Gateway API that points to the new API application code. Instruct the other developers to point the endpoints to the new API.
C. Implement a query parameter in the API application code that determines which code version to call.
D. Specify new API Gateway endpoints for the API endpoints that the developer wants to add.

Correct Answer: A 

---

Question #22

A developer is creating an application that will store personal health information (PHI). The PHI needs to be encrypted at all times. An encrypted Amazon RDS for MySQL DB instance is storing the data. The developer wants to increase the performance of the application by caching frequently accessed data while adding the ability to sort or rank the cached datasets.
Which solution will meet these requirements?

A. Create an Amazon ElastiCache for Redis instance. Enable encryption of data in transit and at rest. Store frequently accessed data in the cache.
B. Create an Amazon ElastiCache for Memcached instance. Enable encryption of data in transit and at rest. Store frequently accessed data in the cache.
C. Create an Amazon RDS for MySQL read replica. Connect to the read replica by using SSL. Configure the read replica to store frequently accessed data.
D. Create an Amazon DynamoDB table and a DynamoDB Accelerator (DAX) cluster for the table. Store frequently accessed data in the DynamoDB table.

Correct Answer: A

---

Question #23

A company has a multi-node Windows legacy application that runs on premises. The application uses a network shared folder as a centralized configuration repository to store configuration files in .xml format. The company is migrating the application to Amazon EC2 instances. As part of the migration to AWS, a developer must identify a solution that provides high availability for the repository.
Which solution will meet this requirement MOST cost-effectively?

A. Mount an Amazon Elastic Block Store (Amazon EBS) volume onto one of the EC2 instances. Deploy a file system on the EBS volume. Use the host operating system to share a folder. Update the application code to read and write configuration files from the shared folder.
B. Deploy a micro EC2 instance with an instance store volume. Use the host operating system to share a folder. Update the application code to read and write configuration files from the shared folder.
C. Create an Amazon S3 bucket to host the repository. Migrate the existing .xml files to the S3 bucket. Update the application code to use the AWS SDK to read and write configuration files from Amazon S3.
D. Create an Amazon S3 bucket to host the repository. Migrate the existing .xml files to the S3 bucket. Mount the S3 bucket to the EC2 instances as a local volume. Update the application code to read and write configuration files from the disk.
 
Correct Answer: C

---

Question #24

A company wants to deploy and maintain static websites on AWS. Each website's source code is hosted in one of several version control systems, including AWS CodeCommit, Bitbucket, and GitHub.
The company wants to implement phased releases by using development, staging, user acceptance testing, and production environments in the AWS Cloud. Deployments to each environment must be started by code merges on the relevant Git branch. The company wants to use HTTPS for all data exchange. The company needs a solution that does not require servers to run continuously.
Which solution will meet these requirements with the LEAST operational overhead?

A. Host each website by using AWS Amplify with a serverless backend. Conned the repository branches that correspond to each of the desired environments. Start deployments by merging code changes to a desired branch.
B. Host each website in AWS Elastic Beanstalk with multiple environments. Use the EB CLI to link each repository branch. Integrate AWS CodePipeline to automate deployments from version control code merges.
C. Host each website in different Amazon S3 buckets for each environment. Configure AWS CodePipeline to pull source code from version control. Add an AWS CodeBuild stage to copy source code to Amazon S3.
D. Host each website on its own Amazon EC2 instance. Write a custom deployment script to bundle each website's static assets. Copy the assets to Amazon EC2. Set up a workflow to run the script when code is merged.

Correct Answer: A

B和D会引入running server
C不支持HTTPS，所以有问题

AWS Amplify是一组专门构建的工具和功能，使前端 Web 和移动开发人员能够快速轻松地在上构建全栈应用程序AWS。Amplify 提供两项服务：Amplify Hosting 和 Amplify Studio。Amplify Hosting 提供了基于 git 的工作流，用于托管持续部署的全栈无服务器 Web 应用程序。该用户指南提供了开始使用 Amplify Hostace Hofy Hostace。

Amazon S3 website endpoints do not support HTTPS. If you want to use HTTPS, you can use Amazon CloudFront to serve a static website hosted on Amazon S3.

---

Question #25

A company is migrating an on-premises database to Amazon RDS for MySQL. The company has read-heavy workloads. The company wants to refactor the code to achieve optimum read performance for queries.
Which solution will meet this requirement with LEAST current and future effort?

A. Use a multi-AZ Amazon RDS deployment. Increase the number of connections that the code makes to the database or increase the connection pool size if a connection pool is in use.
B. Use a multi-AZ Amazon RDS deployment. Modify the code so that queries access the secondary RDS instance.
C. Deploy Amazon RDS with one or more read replicas. Modify the application code so that queries use the URL for the read replicas.
D. Use open source replication software to create a copy of the MySQL database on an Amazon EC2 instance. Modify the application code so that queries use the IP address of the EC2 instance.

Correct Answer: C

---

Question #26

A developer is creating an application that will be deployed on IoT devices. The application will send data to a RESTful API that is deployed as an AWS Lambda function. The application will assign each API request a unique identifier. The volume of API requests from the application can randomly increase at any given time of day.
During periods of request throttling, the application might need to retry requests. The API must be able to handle duplicate requests without inconsistencies or data loss.
Which solution will meet these requirements?

A. Create an Amazon RDS for MySQL DB instance. Store the unique identifier for each request in a database table. Modify the Lambda function to check the table for the identifier before processing the request.
B. Create an Amazon DynamoDB table. Store the unique identifier for each request in the table. Modify the Lambda function to check the table for the identifier before processing the request.
C. Create an Amazon DynamoDB table. Store the unique identifier for each request in the table. Modify the Lambda function to return a client error response when the function receives a duplicate request.
D. Create an Amazon ElastiCache for Memcached instance. Store the unique identifier for each request in the cache. Modify the Lambda function to check the cache for the identifier before processing the request.

Correct Answer: B 

---

Question #27

A developer wants to expand an application to run in multiple AWS Regions. The developer wants to copy Amazon Machine Images (AMIs) with the latest changes and create a new application stack in the destination Region. According to company requirements, all AMIs must be encrypted in all Regions. However, not all the AMIs that the company uses are encrypted.
How can the developer expand the application to run in the destination Region while meeting the encryption requirement?

A. Create new AMIs, and specify encryption parameters. Copy the encrypted AMIs to the destination Region. Delete the unencrypted AMIs.
B. Use AWS Key Management Service (AWS KMS) to enable encryption on the unencrypted AMIs. Copy the encrypted AMIs to the destination Region.
C. Use AWS Certificate Manager (ACM) to enable encryption on the unencrypted AMIs. Copy the encrypted AMIs to the destination Region.
D. Copy the unencrypted AMIs to the destination Region. Enable encryption by default in the destination Region.

Correct Answer: A

如果不使用显式加密参数，在默认情况下，CopyImage 操作会在复制 AMI 的源快照时保持这些快照的现有加密状态。您也可以复制 AMI，同时通过提供加密参数来对其关联的 EBS 快照应用新的加密状态。

您无法直接加密现有未加密卷或快照。但是，您可以从未加密的卷或快照创建加密卷或快照。

Question #28

A company hosts a client-side web application for one of its subsidiaries on Amazon S3. The web application can be accessed through Amazon CloudFront from https://www.example.com. After a successful rollout, the company wants to host three more client-side web applications for its remaining subsidiaries on three separate S3 buckets.
To achieve this goal, a developer moves all the common JavaScript files and web fonts to a central S3 bucket that serves the web applications. However, during testing, the developer notices that the browser blocks the JavaScript files and web fonts.
What should the developer do to prevent the browser from blocking the JavaScript files and web fonts?

A. Create four access points that allow access to the central S3 bucket. Assign an access point to each web application bucket.
B. Create a bucket policy that allows access to the central S3 bucket. Attach the bucket policy to the central S3 bucket
C. Create a cross-origin resource sharing (CORS) configuration that allows access to the central S3 bucket. Add the CORS configuration to the central S3 bucket.
D. Create a Content-MD5 header that provides a message integrity check for the central S3 bucket. Insert the Content-MD5 header for each web application request.

Correct Answer: C 

---

Question #29

An application is processing clickstream data using Amazon Kinesis. The clickstream data feed into Kinesis experiences periodic spikes. The PutRecords API call occasionally fails and the logs show that the failed call returns the response shown below:

![Rate exceed for shard shardId-xxxxx in stream xxxxx under account xxxxx](./image1.png)

Which techniques will help mitigate this exception? (Choose two.)

A. Implement retries with exponential backoff.
B. Use a PutRecord API instead of PutRecords.
C. Reduce the frequency and/or size of the requests.
D. Use Amazon SNS instead of Kinesis.
E. Reduce the number of KCL consumers.

Correct Answer: AC 

---

Question #30
A company has an application that uses Amazon Cognito user pools as an identity provider. The company must secure access to user records. The company has set up multi-factor authentication (MFA). The company also wants to send a login activity notification by email every time a user logs in.
What is the MOST operationally efficient solution that meets this requirement?

A. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Add an Amazon API Gateway API to invoke the function. Call the API from the client side when login confirmation is received.
B. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Add an Amazon Cognito post authentication Lambda trigger for the function.
C. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Create an Amazon CloudWatch Logs log subscription filter to invoke the function based on the login status.
D. Configure Amazon Cognito to stream all logs to Amazon Kinesis Data Firehose. Create an AWS Lambda function to process the streamed logs and to send the email notification based on the login status of each user.

Correct Answer: B

---

Question #31

A developer has an application that stores data in an Amazon S3 bucket. The application uses an HTTP API to store and retrieve objects. When the PutObject API operation adds objects to the S3 bucket the developer must encrypt these objects at rest by using server-side encryption with Amazon S3 managed keys (SSE-S3).
Which solution will meet this requirement?

A. Create an AWS Key Management Service (AWS KMS) key. Assign the KMS key to the S3 bucket.
B. Set the x-amz-server-side-encryption header when invoking the PutObject API operation.
C. Provide the encryption key in the HTTP header of every request.
D. Apply TLS to encrypt the traffic to the S3 bucket.

Correct Answer: B


---

Question #32

A developer needs to perform geographic load testing of an API. The developer must deploy resources to multiple AWS Regions to support the load testing of the API.
How can the developer meet these requirements without additional application code?

A. Create and deploy an AWS Lambda function in each desired Region. Configure the Lambda function to create a stack from an AWS CloudFormation template in that Region when the function is invoked.
B. Create an AWS CloudFormation template that defines the load test resources. Use the AWS CLI create-stack-set command to create a stack set in the desired Regions.
C. Create an AWS Systems Manager document that defines the resources. Use the document to create the resources in the desired Regions.
D. Create an AWS CloudFormation template that defines the load test resources. Use the AWS CLI deploy command to create a stack from the template in each Region.

Correct Answer: B 

AWS CloudFormation StackSets allow developers to deploy CloudFormation stacks across multiple AWS accounts and regions with a single CloudFormation template.


---

Question #33

A developer is creating an application that includes an Amazon API Gateway REST API in the us-east-2 Region. The developer wants to use Amazon CloudFront and a custom domain name for the API. The developer has acquired an SSL/TLS certificate for the domain from a third-party provider.
How should the developer configure the custom domain for the application?

A. Import the SSL/TLS certificate into AWS Certificate Manager (ACM) in the same Region as the API. Create a DNS A record for the custom domain.
B. Import the SSL/TLS certificate into CloudFront. Create a DNS CNAME record for the custom domain.
C. Import the SSL/TLS certificate into AWS Certificate Manager (ACM) in the same Region as the API. Create a DNS CNAME record for the custom domain.
D. Import the SSL/TLS certificate into AWS Certificate Manager (ACM) in the us-east-1 Region. Create a DNS CNAME record for the custom domain.

Correct Answer: D

要在 AWS Certificate Manager (ACM) 中使用证书以要求在查看器和 CloudFront 之间使用 HTTPS，请确保您在美国东部（弗吉尼亚北部）区域 (us-east-1) 中请求（或导入）该证书。

如果您需要在 CloudFront 和您的源之间使用 HTTPS，并且正在 Elastic Load Balancing 中使用负载均衡器作为源，则您可以在任何 AWS 区域中请求或导入证书。

To use a certificate in AWS Certificate Manager (ACM) to require HTTPS between viewers and CloudFront, make sure you request (or import) the certificate in the US East (N. Virginia) Region (us-east-1).

If you want to require HTTPS between CloudFront and your origin, and you’re using a load balancer in Elastic Load Balancing as your origin, you can request or import the certificate in any AWS Region.

---

Question #34

A developer is creating a template that uses AWS CloudFormation to deploy an application. The application is serverless and uses Amazon API Gateway, Amazon DynamoDB, and AWS Lambda.
Which AWS service or tool should the developer use to define serverless resources in YAML?

A. CloudFormation serverless intrinsic functions
B. AWS Elastic Beanstalk
C. AWS Serverless Application Model (AWS SAM)
D. AWS Cloud Development Kit (AWS CDK)

Correct Answer: C 

---

Question #35

A developer wants to insert a record into an Amazon DynamoDB table as soon as a new file is added to an Amazon S3 bucket.
Which set of steps would be necessary to achieve this?

A. Create an event with Amazon EventBridge that will monitor the S3 bucket and then insert the records into DynamoDB.
B. Configure an S3 event to invoke an AWS Lambda function that inserts records into DynamoDB.
C. Create an AWS Lambda function that will poll the S3 bucket and then insert the records into DynamoDB.
D. Create a cron job that will run at a scheduled time and insert the records into DynamoDB.

Correct Answer: B

---

Question #36

A development team maintains a web application by using a single AWS CloudFormation template. The template defines web servers and an Amazon RDS database. The team uses the Cloud Formation template to deploy the Cloud Formation stack to different environments.
During a recent application deployment, a developer caused the primary development database to be dropped and recreated. The result of this incident was a loss of data. The team needs to avoid accidental database deletion in the future.
Which solutions will meet these requirements? (Choose two.)

A. Add a CloudFormation Deletion Policy attribute with the Retain value to the database resource.
B. Update the CloudFormation stack policy to prevent updates to the database.
C. Modify the database to use a Multi-AZ deployment.
D. Create a CloudFormation stack set for the web application and database deployments.
E. Add a Cloud Formation DeletionPolicy attribute with the Retain value to the stack.

Correct Answer: AB

https://docs.aws.amazon.com/zh_cn/AWSCloudFormation/latest/UserGuide/aws-attribute-deletionpolicy.html

利用 DeletionPolicy 属性，您可以在某个资源的堆栈被删除时保留并（在某些情况下）备份该资源。您可为要控制的每个资源指定 DeletionPolicy 属性。默认情况下，如果某个资源不具有 DeletionPolicy 属性，AWS CloudFormation 将删除该资源。

https://docs.aws.amazon.com/zh_cn/AWSCloudFormation/latest/UserGuide/protect-stack-resources.html

在创建堆栈时，允许对所有资源执行所有更新操作。默认情况下，具有堆栈更新权限的任何人均可更新堆栈中的所有资源。在更新期间，一些资源可能需要中断或可能已完全替换，这会生成新的物理 ID 或全新的存储。使用堆栈策略可以防止堆栈资源在堆栈更新过程中被意外更新或删除。堆栈策略是一个 JSON 文档，该文档定义可对指定资源执行的更新操作。

---

Question #37

A company has an Amazon S3 bucket that contains sensitive data. The data must be encrypted in transit and at rest. The company encrypts the data in the S3 bucket by using an AWS Key Management Service (AWS KMS) key. A developer needs to grant several other AWS accounts the permission to use the S3 GetObject operation to retrieve the data from the S3 bucket.
How can the developer enforce that all requests to retrieve the data provide encryption in transit?

A. Define a resource-based policy on the S3 bucket to deny access when a request meets the condition “aws:SecureTransport”: “false”.
B. Define a resource-based policy on the S3 bucket to allow access when a request meets the condition “aws:SecureTransport”: “false”.
C. Define a role-based policy on the other accounts' roles to deny access when a request meets the condition of “aws:SecureTransport”: “false”.
D. Define a resource-based policy on the KMS key to deny access when a request meets the condition of “aws:SecureTransport”: “false”.

Correct Answer: A 

https://docs.aws.amazon.com/zh_cn/AmazonS3/latest/userguide/security-best-practices.html
您可以使用 HTTPS（TLS）帮助防止潜在攻击者使用中间人攻击或类似攻击来窃听或操纵网络流量。我们建议通过在 Amazon S3 桶策略中使用 aws:SecureTransport 条件，以只允许通过 HTTPS（TLS）的加密连接。
https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/reference_policies_elements_condition_operators.html#Conditions_Boolean
例如，此基于身份的策略使用 Bool 条件运算符与 aws:SecureTransport 键拒绝对存储桶及其内容的所有 S3 操作（如果请求不是通过 SSL 进行的）。

重要
该策略不允许进行任何操作。可将此策略与允许特定操作的其他策略结合使用。

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BooleanExample",
      "Action": "s3:*",
      "Effect": "Deny",
      "Resource": [
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET",
        "arn:aws:s3:::DOC-EXAMPLE-BUCKET/*"
      ],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "false"
        }
      }
    }
  ]
}
```

---

Question #38

An application that is hosted on an Amazon EC2 instance needs access to files that are stored in an Amazon S3 bucket. The application lists the objects that are stored in the S3 bucket and displays a table to the user. During testing, a developer discovers that the application does not show any objects in the list.
What is the MOST secure way to resolve this issue?

A. Update the IAM instance profile that is attached to the EC2 instance to include the S3:* permission for the S3 bucket.
B. Update the IAM instance profile that is attached to the EC2 instance to include the S3:ListBucket permission for the S3 bucket.
C. Update the developer's user permissions to include the S3:ListBucket permission for the S3 bucket.
D. Update the S3 bucket policy by including the S3:ListBucket permission and by setting the Principal element to specify the account number of the EC2 instance.

Correct Answer: B

Question #39

A company is planning to securely manage one-time fixed license keys in AWS. The company's development team needs to access the license keys in automaton scripts that run in Amazon EC2 instances and in AWS CloudFormation stacks.
Which solution will meet these requirements MOST cost-effectively?

A. Amazon S3 with encrypted files prefixed with “config”
B. AWS Secrets Manager secrets with a tag that is named SecretString
C. AWS Systems Manager Parameter Store SecureString parameters
D. CloudFormation NoEcho parameters

Correct Answer: C 

---

Question #40

A company has deployed infrastructure on AWS. A development team wants to create an AWS Lambda function that will retrieve data from an Amazon Aurora database. The Amazon Aurora database is in a private subnet in company's VPC. The VPC is named VPC1. The data is relational in nature. The Lambda function needs to access the data securely.
Which solution will meet these requirements?

A. Create the Lambda function. Configure VPC1 access for the function. Attach a security group named SG1 to both the Lambda function and the database. Configure the security group inbound and outbound rules to allow TCP traffic on Port 3306.
B. Create and launch a Lambda function in a new public subnet that is in a new VPC named VPC2. Create a peering connection between VPC1 and VPC2.
C. Create the Lambda function. Configure VPC1 access for the function. Assign a security group named SG1 to the Lambda function. Assign a second security group named SG2 to the database. Add an inbound rule to SG1 to allow TCP traffic from Port 3306.
D. Export the data from the Aurora database to Amazon S3. Create and launch a Lambda function in VPC1. Configure the Lambda function query the data from Amazon S3.

Correct Answer: C 

Answer A is wrong because you do not need to configure outbound rule for security groups. 

---

Question #41

A developer is building a web application that uses Amazon API Gateway to expose an AWS Lambda function to process requests from clients. During testing, the developer notices that the API Gateway times out even though the Lambda function finishes under the set time limit.
Which of the following API Gateway metrics in Amazon CloudWatch can help the developer troubleshoot the issue? (Choose two.)

A. CacheHitCount
B. IntegrationLatency
C. CacheMissCount
D. Latency
E. Count

Correct Answer: BD 

• IntegrationLatency: The time between when API Gateway relays a 
request to the backend and when it receives a response from the 
backend.
• Latency: The time between when API Gateway receives a request from 
a client and when it returns a response to the client. The latency 
includes the integration latency and other API Gateway overhead.

---

Question #42

A development team wants to build a continuous integration/continuous delivery (CI/CD) pipeline. The team is using AWS CodePipeline to automate the code build and deployment. The team wants to store the program code to prepare for the CI/CD pipeline.
Which AWS service should the team use to store the program code?

A. AWS CodeDeploy
B. AWS CodeArtifact
C. AWS CodeCommit
D. Amazon CodeGuru

Correct Answer: C 

---

Question #43

A developer is designing an AWS Lambda function that creates temporary files that are less than 10 MB during invocation. The temporary files will be accessed and modified multiple times during invocation. The developer has no need to save or retrieve these files in the future.
Where should the temporary files be stored?

A. the /tmp directory
B. Amazon Elastic File System (Amazon EFS)
C. Amazon Elastic Block Store (Amazon EBS)
D. Amazon S3

Correct Answer: A 

---

Question #44

A developer is designing a serverless application with two AWS Lambda functions to process photos. One Lambda function stores objects in an Amazon S3 bucket and stores the associated metadata in an Amazon DynamoDB table. The other Lambda function fetches the objects from the S3 bucket by using the metadata from the DynamoDB table. Both Lambda functions use the same Python library to perform complex computations and are approaching the quota for the maximum size of zipped deployment packages.
What should the developer do to reduce the size of the Lambda deployment packages with the LEAST operational overhead?

A. Package each Python library in its own .zip file archive. Deploy each Lambda function with its own copy of the library.
B. Create a Lambda layer with the required Python library. Use the Lambda layer in both Lambda functions.
C. Combine the two Lambda functions into one Lambda function. Deploy the Lambda function as a single .zip file archive.
D. Download the Python library to an S3 bucket. Program the Lambda functions to reference the object URLs.

Correct Answer: B 

Lambda 层是可以包含其他代码或其他内容的 .zip 文件归档。层可以包含库、自定义运行时、数据或配置文件。使用层可以缩小部署包大小，并促进代码共享和责任分离，以便您可以更快地迭代编写业务逻辑。

---
Question #45

A developer is writing an AWS Lambda function. The developer wants to log key events that occur while the Lambda function runs. The developer wants to include a unique identifier to associate the events with a specific function invocation. The developer adds the following code to the Lambda function:

```
function handler(evnet, context){
}
```

Which solution will meet this requirement?

A. Obtain the request identifier from the AWS request ID field in the context object. Configure the application to write logs to standard output.
B. Obtain the request identifier from the AWS request ID field in the event object. Configure the application to write logs to a file.
C. Obtain the request identifier from the AWS request ID field in the event object. Configure the application to write logs to standard output.
D. Obtain the request identifier from the AWS request ID field in the context object. Configure the application to write logs to a file.

Correct Answer: A

Event Object
• JSON-formatted document contains data for the function to process
• Contains information from the invoking service (e.g., EventBridge, custom, …)
• Lambda runtime converts the event to an object (e.g., dict type in Python)
• Example: input arguments, invoking service arguments, …

Context Object
• Provides methods and properties that provide information about the invocation, 
function, and runtime environment
• Passed to your function by Lambda at runtime
• Example: aws_request_id, function_name, memory_limit_in_mb

---

Question #46

A developer is working on a serverless application that needs to process any changes to an Amazon DynamoDB table with an AWS Lambda function.
How should the developer configure the Lambda function to detect changes to the DynamoDB table?

A. Create an Amazon Kinesis data stream, and attach it to the DynamoDB table. Create a trigger to connect the data stream to the Lambda function.
B. Create an Amazon EventBridge rule to invoke the Lambda function on a regular schedule. Conned to the DynamoDB table from the Lambda function to detect changes.
C. Enable DynamoDB Streams on the table. Create a trigger to connect the DynamoDB stream to the Lambda function.
D. Create an Amazon Kinesis Data Firehose delivery stream, and attach it to the DynamoDB table. Configure the delivery stream destination as the Lambda function.

Correct Answer: C 

---

Question #47

An application uses an Amazon EC2 Auto Scaling group. A developer notices that EC2 instances are taking a long time to become available during scale-out events. The UserData script is taking a long time to run.
The developer must implement a solution to decrease the time that elapses before an EC2 instance becomes available. The solution must make the most recent version of the application available at all times and must apply all available security updates. The solution also must minimize the number of images that are created. The images must be validated.
Which combination of steps should the developer take to meet these requirements? (Choose two.)

A. Use EC2 Image Builder to create an Amazon Machine Image (AMI). Install all the patches and agents that are needed to manage and run the application. Update the Auto Scaling group launch configuration to use the AMI.
B. Use EC2 Image Builder to create an Amazon Machine Image (AMI). Install the latest version of the application and all the patches and agents that are needed to manage and run the application. Update the Auto Scaling group launch configuration to use the AMI.
C. Set up AWS CodeDeploy to deploy the most recent version of the application at runtime.
D. Set up AWS CodePipeline to deploy the most recent version of the application at runtime.
E. Remove any commands that perform operating system patching from the UserData script.

Correct Answer: AE （不确定）

Question #48

A developer is creating an AWS Lambda function that needs credentials to connect to an Amazon RDS for MySQL database. An Amazon S3 bucket currently stores the credentials. The developer needs to improve the existing solution by implementing credential rotation and secure storage. The developer also needs to provide integration with the Lambda function.
Which solution should the developer use to store and retrieve the credentials with the LEAST management overhead?

A. Store the credentials in AWS Systems Manager Parameter Store. Select the database that the parameter will access. Use the default AWS Key Management Service (AWS KMS) key to encrypt the parameter. Enable automatic rotation for the parameter. Use the parameter from Parameter Store on the Lambda function to connect to the database.
B. Encrypt the credentials with the default AWS Key Management Service (AWS KMS) key. Store the credentials as environment variables for the Lambda function. Create a second Lambda function to generate new credentials and to rotate the credentials by updating the environment variables of the first Lambda function. Invoke the second Lambda function by using an Amazon EventBridge rule that runs on a schedule. Update the database to use the new credentials. On the first Lambda function, retrieve the credentials from the environment variables. Decrypt the credentials by using AWS KMS, Connect to the database.
C. Store the credentials in AWS Secrets Manager. Set the secret type to Credentials for Amazon RDS database. Select the database that the secret will access. Use the default AWS Key Management Service (AWS KMS) key to encrypt the secret. Enable automatic rotation for the secret. Use the secret from Secrets Manager on the Lambda function to connect to the database.
D. Encrypt the credentials by using AWS Key Management Service (AWS KMS). Store the credentials in an Amazon DynamoDB table. Create a second Lambda function to rotate the credentials. Invoke the second Lambda function by using an Amazon EventBridge rule that runs on a schedule. Update the DynamoDB table. Update the database to use the generated credentials. Retrieve the credentials from DynamoDB with the first Lambda function. Connect to the database.

Correct Answer: C 

---

Question #49 

A developer has written the following IAM policy to provide access to an Amazon S3 bucket:
![image3](./image3.png)
Which access does the policy allow regarding the s3:GetObject and s3:PutObject actions?

A. Access on all buckets except the “DOC-EXAMPLE-BUCKET” bucket
B. Access on all buckets that start with “DOC-EXAMPLE-BUCKET” except the “DOC-EXAMPLE-BUCKET/secrets” bucket
C. Access on all objects in the “DOC-EXAMPLE-BUCKET” bucket along with access to all S3 actions for objects in the “DOC-EXAMPLE-BUCKET” bucket that start with “secrets”
D. Access on all objects in the “DOC-EXAMPLE-BUCKET” bucket except on objects that start with “secrets”

Correct Answer: D 

---

Question #50

A developer is creating a mobile app that calls a backend service by using an Amazon API Gateway REST API. For integration testing during the development phase, the developer wants to simulate different backend responses without invoking the backend service.
Which solution will meet these requirements with the LEAST operational overhead?

A. Create an AWS Lambda function. Use API Gateway proxy integration to return constant HTTP responses.
B. Create an Amazon EC2 instance that serves the backend REST API by using an AWS CloudFormation template.
C. Customize the API Gateway stage to select a response type based on the request.
D. Use a request mapping template to select the mock integration response.

Correct Answer: D

---


Question #51

A developer has a legacy application that is hosted on-premises. Other applications hosted on AWS depend on the on-premises application for proper functioning. In case of any application errors, the developer wants to be able to use Amazon CloudWatch to monitor and troubleshoot all applications from one place.
How can the developer accomplish this?

A. Install an AWS SDK on the on-premises server to automatically send logs to CloudWatch.
B. Download the CloudWatch agent to the on-premises server. Configure the agent to use IAM user credentials with permissions for CloudWatch.
C. Upload log files from the on-premises server to Amazon S3 and have CloudWatch read the files.
D. Upload log files from the on-premises server to an Amazon EC2 instance and have the instance forward the logs to CloudWatch.

Correct Answer: B

---

Question #52

An Amazon Kinesis Data Firehose delivery stream is receiving customer data that contains personally identifiable information. A developer needs to remove pattern-based customer identifiers from the data and store the modified data in an Amazon S3 bucket.
What should the developer do to meet these requirements?

A. Implement Kinesis Data Firehose data transformation as an AWS Lambda function. Configure the function to remove the customer identifiers. Set an Amazon S3 bucket as the destination of the delivery stream.
B. Launch an Amazon EC2 instance. Set the EC2 instance as the destination of the delivery stream. Run an application on the EC2 instance to remove the customer identifiers. Store the transformed data in an Amazon S3 bucket.
C. Create an Amazon OpenSearch Service instance. Set the OpenSearch Service instance as the destination of the delivery stream. Use search and replace to remove the customer identifiers. Export the data to an Amazon S3 bucket.
D. Create an AWS Step Functions workflow to remove the customer identifiers. As the last step in the workflow, store the transformed data in an Amazon S3 bucket. Set the workflow as the destination of the delivery stream.

Correct Answer: A 

---

Question #53

A developer is using an AWS Lambda function to generate avatars for profile pictures that are uploaded to an Amazon S3 bucket. The Lambda function is automatically invoked for profile pictures that are saved under the /original/ S3 prefix. The developer notices that some pictures cause the Lambda function to time out. The developer wants to implement a fallback mechanism by using another Lambda function that resizes the profile picture.
Which solution will meet these requirements with the LEAST development effort?

A. Set the image resize Lambda function as a destination of the avatar generator Lambda function for the events that fail processing.
B. Create an Amazon Simple Queue Service (Amazon SQS) queue. Set the SQS queue as a destination with an on failure condition for the avatar generator Lambda function. Configure the image resize Lambda function to poll from the SQS queue.
C. Create an AWS Step Functions state machine that invokes the avatar generator Lambda function and uses the image resize Lambda function as a fallback. Create an Amazon EventBridge rule that matches events from the S3 bucket to invoke the state machine.
D. Create an Amazon Simple Notification Service (Amazon SNS) topic. Set the SNS topic as a destination with an on failure condition for the avatar generator Lambda function. Subscribe the image resize Lambda function to the SNS topic.

Correct Answer: A 不确定

Nov 2019: Can configure to send result to a 
destination
Asynchronous invocations - can define destinations for 
successful and failed event:
• Amazon SQS
• Amazon SNS
• AWS Lambda
• Amazon EventBridge bus
Note: AWS recommends you use destinations instead of 
DLQ now (but both can be used at the same time)

---

Question #54

A developer needs to migrate an online retail application to AWS to handle an anticipated increase in traffic. The application currently runs on two servers: one server for the web application and another server for the database. The web server renders webpages and manages session state in memory. The database server hosts a MySQL database that contains order details. When traffic to the application is heavy, the memory usage for the web server approaches 100% and the application slows down considerably.
The developer has found that most of the memory increase and performance decrease is related to the load of managing additional user sessions. For the web server migration, the developer will use Amazon EC2 instances with an Auto Scaling group behind an Application Load Balancer.
Which additional set of changes should the developer make to the application to improve the application's performance?

A. Use an EC2 instance to host the MySQL database. Store the session data and the application data in the MySQL database.
B. Use Amazon ElastiCache for Memcached to store and manage the session data. Use an Amazon RDS for MySQL DB instance to store the application data.
C. Use Amazon ElastiCache for Memcached to store and manage the session data and the application data.
D. Use the EC2 instance store to manage the session data. Use an Amazon RDS for MySQL DB instance to store the application data.

Correct Answer: B

---

Question #55

An application uses Lambda functions to extract metadata from files uploaded to an S3 bucket; the metadata is stored in Amazon DynamoDB. The application starts behaving unexpectedly, and the developer wants to examine the logs of the Lambda function code for errors.
Based on this system configuration, where would the developer find the logs?

A. Amazon S3
B. AWS CloudTrail
C. Amazon CloudWatch
D. Amazon DynamoDB

Correct Answer: C

---

Question #56

A company is using an AWS Lambda function to process records from an Amazon Kinesis data stream. The company recently observed slow processing of the records. A developer notices that the iterator age metric for the function is increasing and that the Lambda run duration is constantly above normal.
Which actions should the developer take to increase the processing speed? (Choose two.)

A. Increase the number of shards of the Kinesis data stream.
B. Decrease the timeout of the Lambda function.
C. Increase the memory that is allocated to the Lambda function.
D. Decrease the number of shards of the Kinesis data stream.
E. Increase the timeout of the Lambda function.

Correct Answer: AC 

https://repost.aws/knowledge-center/lambda-iterator-age

A low number of shards in a stream increases a function's iterator age. Increasing the number of shards in a stream increases the number of concurrent Lambda functions consuming from your stream, which decreases a function's iterator age.

---

Question #57

A company needs to harden its container images before the images are in a running state. The company's application uses Amazon Elastic Container Registry (Amazon ECR) as an image registry. Amazon Elastic Kubernetes Service (Amazon EKS) for compute, and an AWS CodePipeline pipeline that orchestrates a continuous integration and continuous delivery (CI/CD) workflow.
Dynamic application security testing occurs in the final stage of the pipeline after a new image is deployed to a development namespace in the EKS cluster. A developer needs to place an analysis stage before this deployment to analyze the container image earlier in the CI/CD pipeline.
Which solution will meet these requirements with the MOST operational efficiency?

A. Build the container image and run the docker scan command locally. Mitigate any findings before pushing changes to the source code repository. Write a pre-commit hook that enforces the use of this workflow before commit.
B. Create a new CodePipeline stage that occurs after the container image is built. Configure ECR basic image scanning to scan on image push. Use an AWS Lambda function as the action provider. Configure the Lambda function to check the scan results and to fail the pipeline if there are findings.
C. Create a new CodePipeline stage that occurs after source code has been retrieved from its repository. Run a security scanner on the latest revision of the source code. Fail the pipeline if there are findings.
D. Add an action to the deployment stage of the pipeline so that the action occurs before the deployment to the EKS cluster. Configure ECR basic image scanning to scan on image push. Use an AWS Lambda function as the action provider. Configure the Lambda function to check the scan results and to fail the pipeline if there are findings.

Correct Answer: B 不确定

---

Question #58

A developer is testing a new file storage application that uses an Amazon CloudFront distribution to serve content from an Amazon S3 bucket. The distribution accesses the S3 bucket by using an origin access identity (OAI). The S3 bucket's permissions explicitly deny access to all other users.
The application prompts users to authenticate on a login page and then uses signed cookies to allow users to access their personal storage directories. The developer has configured the distribution to use its default cache behavior with restricted viewer access and has set the origin to point to the S3 bucket. However, when the developer tries to navigate to the login page, the developer receives a 403 Forbidden error.
The developer needs to implement a solution to allow unauthenticated access to the login page. The solution also must keep all private content secure.
Which solution will meet these requirements?

A. Add a second cache behavior to the distribution with the same origin as the default cache behavior. Set the path pattern for the second cache behavior to the path of the login page, and make viewer access unrestricted. Keep the default cache behavior's settings unchanged.
B. Add a second cache behavior to the distribution with the same origin as the default cache behavior. Set the path pattern for the second cache behavior to *, and make viewer access restricted. Change the default cache behavior's path pattern to the path of the login page, and make viewer access unrestricted.
C. Add a second origin as a failover origin to the default cache behavior. Point the failover origin to the S3 bucket. Set the path pattern for the primary origin to *, and make viewer access restricted. Set the path pattern for the failover origin to the path of the login page, and make viewer access unrestricted.
D. Add a bucket policy to the S3 bucket to allow read access. Set the resource on the policy to the Amazon Resource Name (ARN) of the login page object in the S3 bucket. Add a CloudFront function to the default cache behavior to redirect unauthorized requests to the login page's S3 URL.

Correct Answer: A

Cache Behaviors是CloudFront的内容

• Configure different settings for a given URL path 
pattern
• Example: one specific cache behavior to images/*.jpg 
files on your origin web server
• Route to different kind of origins/origin groups 
based on the content type or path pattern
• /images/*
• /api/*
• /* (default cache behavior)
• When adding additional Cache Behaviors, the 
Default Cache Behavior is always the last to be 
processed and is always /*

---

Question #59

A developer is using AWS Amplify Hosting to build and deploy an application. The developer is receiving an increased number of bug reports from users. The developer wants to add end-to-end testing to the application to eliminate as many bugs as possible before the bugs reach production.
Which solution should the developer implement to meet these requirements?

A. Run the amplify add test command in the Amplify CLI.
B. Create unit tests in the application. Deploy the unit tests by using the amplify push command in the Amplify CLI.
C. Add a test phase to the amplify.yml build settings for the application.
D. Add a test phase to the aws-exports.js file for the application.

Correct Answer: C

---

Question #60

An ecommerce company is using an AWS Lambda function behind Amazon API Gateway as its application tier. To process orders during checkout, the application calls a POST API from the frontend. The POST API invokes the Lambda function asynchronously. In rare situations, the application has not processed orders. The Lambda application logs show no errors or failures.
What should a developer do to solve this problem?

A. Inspect the frontend logs for API failures. Call the POST API manually by using the requests from the log file.
B. Create and inspect the Lambda dead-letter queue. Troubleshoot the failed functions. Reprocess the events.
C. Inspect the Lambda logs in Amazon CloudWatch for possible errors. Fix the errors.
D. Make sure that caching is disabled for the POST API in API Gateway.

Correct Answer: B

A不对是因为这是asynchronously的，所以前端永远202

---

Question #61

A company is building a web application on AWS. When a customer sends a request, the application will generate reports and then make the reports available to the customer within one hour. Reports should be accessible to the customer for 8 hours. Some reports are larger than 1 MB. Each report is unique to the customer. The application should delete all reports that are older than 2 days.
Which solution will meet these requirements with the LEAST operational overhead?

A. Generate the reports and then store the reports as Amazon DynamoDB items that have a specified TTL. Generate a URL that retrieves the reports from DynamoDB. Provide the URL to customers through the web application.
B. Generate the reports and then store the reports in an Amazon S3 bucket that uses server-side encryption. Attach the reports to an Amazon Simple Notification Service (Amazon SNS) message. Subscribe the customer to email notifications from Amazon SNS.
C. Generate the reports and then store the reports in an Amazon S3 bucket that uses server-side encryption. Generate a presigned URL that contains an expiration date Provide the URL to customers through the web application. Add S3 Lifecycle configuration rules to the S3 bucket to delete old reports.
D. Generate the reports and then store the reports in an Amazon RDS database with a date stamp. Generate an URL that retrieves the reports from the RDS database. Provide the URL to customers through the web application. Schedule an hourly AWS Lambda function to delete database records that have expired date stamps.

Correct Answer: C

---

Question #62

A company has deployed an application on AWS Elastic Beanstalk. The company has configured the Auto Scaling group that is associated with the Elastic Beanstalk environment to have five Amazon EC2 instances. If the capacity is fewer than four EC2 instances during the deployment, application performance degrades. The company is using the all-at-once deployment policy.
What is the MOST cost-effective way to solve the deployment issue?

A. Change the Auto Scaling group to six desired instances.
B. Change the deployment policy to traffic splitting. Specify an evaluation time of 1 hour.
C. Change the deployment policy to rolling with additional batch. Specify a batch size of 1.
D. Change the deployment policy to rolling. Specify a batch size of 2.

Correct Answer: C

---

Question #63

A developer is incorporating AWS X-Ray into an application that handles personal identifiable information (PII). The application is hosted on Amazon EC2 instances. The application trace messages include encrypted PII and go to Amazon CloudWatch. The developer needs to ensure that no PII goes outside of the EC2 instances.
Which solution will meet these requirements?

A. Manually instrument the X-Ray SDK in the application code.
B. Use the X-Ray auto-instrumentation agent.
C. Use Amazon Macie to detect and hide PII. Call the X-Ray API from AWS Lambda.
D. Use AWS Distro for Open Telemetry.

Correct Answer: A

C is wrong, Amazon Macie discover PII but dont hide it

Amazon Macie 是一项数据安全服务，该服务使用机器学习和模式匹配来发现敏感数据，提供对数据安全风险的可见性，并实现针对这些风险的自动防护。

为了帮助您管理组织的 Amazon Simazon Service (Amazon S3) 桶的清单，并且自动评估和监控这些桶以实现安全性和访问控制。如果 Macie 检测到潜在的数据安全性或隐私问题（例如桶变为可供公共访问），Macie 会生成调查发现，供您查看并在必要时进行补救。

Macie 还自动发现和报告敏感数据，让您更好地了解组织在 Amazon S3 中存储的数据。要检测敏感数据，您可以使用 Macie 提供的内置标准和技术、您定义的自定义标准或两者的组合。如果 Macie 在 S3 对象中检测到敏感数据，Macie 会生成调查发现来通知您 Macie 找到的敏感数据。

除了调查发现，Macie 还提供统计数据和其他数据，让您深入了解 Amazon S3 数据的安全状况，以及敏感数据可能存在于数据资产中的位置。统计数据和数据可以指导您做出决定，对特定 S3 存储桶和对象进行更深入的调查。您可以使用 Amazon Macie 控制台或 Amazon Macie API 查看和分析调查结果、统计数据和其他数据。您还可以利用 Macie 与 Amazon EventBridge 的集成，通过使用其他服务、应用程序和系统来监控、处理和修复调查结果。

---

Question #64

A developer is migrating some features from a legacy monolithic application to use AWS Lambda functions instead. The application currently stores data in an Amazon Aurora DB cluster that runs in private subnets in a VPC. The AWS account has one VPC deployed. The Lambda functions and the DB cluster are deployed in the same AWS Region in the same AWS account.
The developer needs to ensure that the Lambda functions can securely access the DB cluster without crossing the public internet.
Which solution will meet these requirements?

A. Configure the DB cluster's public access setting to Yes.
B. Configure an Amazon RDS database proxy for he Lambda functions.
C. Configure a NAT gateway and a security group for the Lambda functions.
D. Configure the VPC, subnets, and a security group for the Lambda functions.

Correct Answer: D 

Lambda in VPC
• You must define the VPC ID, the Subnets and the Security Groups
• Lambda will create an ENI (Elastic Network Interface) in your subnets

• A Lambda function in your VPC does not have internet access 
• Deploying a Lambda function in a public subnet does not give it internet access or a public IP
• Deploying a Lambda function in a private subnet gives it internet access if you have a NAT Gateway / Instance
• You can use VPC endpoints to privately access AWS services without a NAT

---

Question #: 65
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is building a new application on AWS. The application uses an AWS Lambda function that retrieves information from an Amazon DynamoDB table. The developer hard coded the DynamoDB table name into the Lambda function code. The table name might change over time. The developer does not want to modify the Lambda code if the table name changes.
Which solution will meet these requirements MOST efficiently?

A. Create a Lambda environment variable to store the table name. Use the standard method for the programming language to retrieve the variable.
B. Store the table name in a file. Store the file in the /tmp folder. Use the SDK for the programming language to retrieve the table name.
C. Create a file to store the table name. Zip the file and upload the file to the Lambda layer. Use the SDK for the programming language to retrieve the table name.
D. Create a global variable that is outside the handler in the Lambda function to store the table name.

Suggested Answer: A

---

Question #: 66
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has a critical application on AWS. The application exposes an HTTP API by using Amazon API Gateway. The API is integrated with an AWS Lambda function. The application stores data in an Amazon RDS for MySQL DB instance with 2 virtual CPUs (vCPUs) and 64 GB of RAM.

Customers have reported that some of the API calls return HTTP 500 Internal Server Error responses. Amazon CloudWatch Logs shows errors for “too many connections.” The errors occur during peak usage times that are unpredictable.

The company needs to make the application resilient. The database cannot be down outside of scheduled maintenance hours.

Which solution will meet these requirements?

A. Decrease the number of vCPUs for the DB instance. Increase the max_connections setting.
B. Use Amazon RDS Proxy to create a proxy that connects to the DB instance. Update the Lambda function to connect to the proxy.
C. Add a CloudWatch alarm that changes the DB instance class when the number of connections increases to more than 1,000.
D. Add an Amazon EventBridge rule that increases the max_connections setting of the DB instance when CPU utilization is above 75%.

Suggested Answer: B

Amazon RDS Proxy
• Fully managed database proxy for RDS
• Allows apps to pool and share DB connections established with the database
• Improving database efficiency by reducing the stress on database resources (e.g., CPU, RAM) and minimize open connections (and timeouts)
• Serverless, autoscaling, highly available (multi-AZ)
• Reduced RDS & Aurora failover time by up 66%
• Supports RDS (MySQL, PostgreSQL, MariaDB) and Aurora (MySQL, PostgreSQL)
• No code changes required for most apps
• Enforce IAM Authentication for DB, and securely store credentials in AWS Secrets Manager
• RDS Proxy is never publicly accessible (must be 
accessed from VPC)

---

Question #: 67
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has installed smart meters in all its customer locations. The smart meters measure power usage at 1-minute intervals and send the usage readings to a remote endpoint for collection. The company needs to create an endpoint that will receive the smart meter readings and store the readings in a database. The company wants to store the location ID and timestamp information.

The company wants to give its customers low-latency access to their current usage and historical usage on demand. The company expects demand to increase significantly. The solution must not impact performance or include downtime while scaling.

Which solution will meet these requirements MOST cost-effectively?

A. Store the smart meter readings in an Amazon RDS database. Create an index on the location ID and timestamp columns. Use the columns to filter on the customers' data.
B. Store the smart meter readings in an Amazon DynamoDB table. Create a composite key by using the location ID and timestamp columns. Use the columns to filter on the customers' data.
C. Store the smart meter readings in Amazon ElastiCache for Redis. Create a SortedSet key by using the location ID and timestamp columns. Use the columns to filter on the customers' data.
D. Store the smart meter readings in Amazon S3. Partition the data by using the location ID and timestamp columns. Use Amazon Athena to filter on the customers' data.

Suggested Answer: B 

---

Question #: 68
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is building a serverless application that uses AWS Lambda functions. The company needs to create a set of test events to test Lambda functions in a development environment. The test events will be created once and then will be used by all the developers in an IAM developer group. The test events must be editable by any of the IAM users in the IAM developer group.

Which solution will meet these requirements?

A. Create and store the test events in Amazon S3 as JSON objects. Allow S3 bucket access to all IAM users.
B. Create the test events. Configure the event sharing settings to make the test events shareable.
C. Create and store the test events in Amazon DynamoDB. Allow access to DynamoDB by using IAM roles.
D. Create the test events. Configure the event sharing settings to make the test events private.

Suggested Answer: B

https://docs.aws.amazon.com/lambda/latest/dg/testing-functions.html#creating-shareable-events

可共享测试事件

可共享测试事件是您可与同一 AWS 账户中的其他用户共享的测试事件。您可以编辑其他用户的可共享测试事件并使用这些测试事件调用您的函数。

Lambda 将可共享测试事件作为 Schema 保存在一个名为 lambda-testevent-schemas 的 Amazon EventBridge（CloudWatch Events）Schema 注册表中。由于 Lambda 利用此注册表来存储和调用您创建的可共享测试事件，因此我们建议您不要编辑此注册表或使用 lambda-testevent-schemas 名称创建注册表。

要查看、共享和编辑可共享测试事件，您必须拥有以下所有 EventBridge（CloudWatch Events）Schema 注册表 API 操作的权限

创建可共享测试事件

    打开 Lamba 控制台的 Functions

（函数）页面。

选择要测试的函数的名称。

选择 Test（测试）选项卡。

在 Test event（测试事件）下执行以下操作：

    选择一个 Template（模板）。

    输入测试的 Name（名称）。

    在文本输入框中，输入 JSON 测试事件。

    在 Event sharing settings（事件共享设置）下，选择 Shareable（可共享）。

选择 Save changes（保存更改）。

---

Question #: 69
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is configuring an application's deployment environment in AWS CodePipeline. The application code is stored in a GitHub repository. The developer wants to ensure that the repository package's unit tests run in the new deployment environment. The developer has already set the pipeline's source provider to GitHub and has specified the repository and branch to use in the deployment.

Which combination of steps should the developer take next to meet these requirements with the LEAST overhead? (Choose two.)

A. Create an AWS CodeCommit project. Add the repository package's build and test commands to the project's buildspec.
B. Create an AWS CodeBuild project. Add the repository package's build and test commands to the project's buildspec.
C. Create an AWS CodeDeploy project. Add the repository package's build and test commands to the project's buildspec.
D. Add an action to the source stage. Specify the newly created project as the action provider. Specify the build artifact as the action's input artifact.
E. Add a new stage to the pipeline after the source stage. Add an action to the new stage. Specify the newly created project as the action provider. Specify the source artifact as the action's input artifact.

Suggested Answer: BE

E选项的  “newly created project”指的是B选项中建的CodeBuild project，所以input是source artifact


---

Question #: 70
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
An engineer created an A/B test of a new feature on an Amazon CloudWatch Evidently project. The engineer configured two variations of the feature (Variation A and Variation B) for the test. The engineer wants to work exclusively with Variation A. The engineer needs to make updates so that Variation A is the only variation that appears when the engineer hits the application's endpoint.

Which solution will meet this requirement?

A. Add an override to the feature. Set the identifier of the override to the engineer's user ID. Set the variation to Variation A.
B. Add an override to the feature. Set the identifier of the override to Variation A. Set the variation to 100%.
C. Add an experiment to the project. Set the identifier of the experiment to Variation B. Set the variation to 0%.
D. Add an experiment to the project. Set the identifier of the experiment to the AWS account's account ISet the variation to Variation A.

Suggested Answer: A

向项目添加功能

    通过以下网址打开 CloudWatch 控制台：https://console.aws.amazon.com/cloudwatch/

。

在导航窗格中，依次选择 Application monitoring（监控应用程序）、Evidently。

请选择项目名称。

请选择 Add feature（添加功能）。

对于 Feature name（功能名称），输入用于标识此项目中此功能的名称。

您也可以添加功能描述。

对于 Feature variations（功能变体）和 Variation type（变体类型），请选择 Boolean、Long（长整数）、Double（双精度）或者 String（字符串）。有关更多信息，请参阅变体类型。

最多可向功能添加五个变体。每个变体的 Value（值）必须对您选择的 Variation type（变体类型）有效。

指定其中一个变体作为默认变体。这是将与其他变体进行比较的基准，并且应作为现在向用户提供的变体。这也是向未添加到此功能的启动或实验中的用户提供的变体。

请选择 Sample code（示例代码）。此代码示例显示了为设置变体并为其分配用户会话，您需要添加到应用程序中的内容。您可以在 JavaScript、Java 和 Python 之间选择代码。

您现在无需将代码添加到应用程序中，但必须在开始启动或实验之前添加。

有关更多信息，请参阅将代码添加到应用程序。

（可选）要指定某些用户可以始终看到某个变体，请选择 Overrides（覆盖）、Add override（添加覆盖）。然后，通过在 Identifier（标识符）中输入用户 ID、账户 ID 或其他一些标识符，指定用户并指定其可以看到的变体。

如果您想确保自己的测试团队成员或其他内部用户可以看到特定变体，这非常有用。已分配覆盖的用户的会话无益于启动或试验指标。

您可以通过再次选择 Add override（添加覆盖），为多达 10 个用户重复此操作。

（可选）要向此功能添加标签，请选择 Tags（标签）、Add new tag（添加新标签）。

然后，对于 Key（键），输入标签的名称。您可以在 Value (值) 中添加可选的标签值。

要添加其他标签，请再次选择 Add new tag（添加新标签）。

有关更多信息，请参阅标记 AWS 资源。

请选择 Add feature（添加功能）。

---

Question #: 71
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is working on an existing application that uses Amazon DynamoDB as its data store. The DynamoDB table has the following attributes: partNumber (partition key), vendor (sort key), description, productFamily, and productType. When the developer analyzes the usage patterns, the developer notices that there are application modules that frequently look for a list of products based on the productFamily and productType attributes.

The developer wants to make changes to the application to improve performance of the query operations.

Which solution will meet these requirements?

A. Create a global secondary index (GSI) with productFamily as the partition key and productType as the sort key.
B. Create a local secondary index (LSI) with productFamily as the partition key and productType as the sort key.
C. Recreate the table. Add partNumber as the partition key and vendor as the sort key. During table creation, add a local secondary index (LSI) with productFamily as the partition key and productType as the sort key.
D. Update the queries to use Scan operations with productFamily as the partition key and productType as the sort key.

Suggested Answer: A

---

Question #: 72
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer creates a VPC named VPC-A that has public and private subnets. The developer also creates an Amazon RDS database inside the private subnet of VPC-A. To perform some queries, the developer creates an AWS Lambda function in the default VPC. The Lambda function has code to access the RDS database. When the Lambda function runs, an error message indicates that the function cannot connect to the RDS database.

How can the developer solve this problem?

A. Modify the RDS security group. Add a rule to allow traffic from all the ports from the VPC CIDR block.
B. Redeploy the Lambda function in the same subnet as the RDS instance. Ensure that the RDS security group allows traffic from the Lambda function.
C. Create a security group for the Lambda function. Add a new rule in the RDS security group to allow traffic from the new Lambda security group.
D. Create an IAM role. Attach a policy that allows access to the RDS database. Attach the role to the Lambda function.

Suggested Answer: B

---

Question #: 73
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company runs an application on AWS. The company deployed the application on Amazon EC2 instances. The application stores data on Amazon Aurora.

The application recently logged multiple application-specific custom DECRYP_ERROR errors to Amazon CloudWatch logs. The company did not detect the issue until the automated tests that run every 30 minutes failed. A developer must implement a solution that will monitor for the custom errors and alert a development team in real time when these errors occur in the production environment.

Which solution will meet these requirements with the LEAST operational overhead?

A. Configure the application to create a custom metric and to push the metric to CloudWatch. Create an AWS CloudTrail alarm. Configure the CloudTrail alarm to use an Amazon Simple Notification Service (Amazon SNS) topic to send notifications.
B. Create an AWS Lambda function to run every 5 minutes to scan the CloudWatch logs for the keyword DECRYP_ERROR. Configure the Lambda function to use Amazon Simple Notification Service (Amazon SNS) to send a notification.
C. Use Amazon CloudWatch Logs to create a metric filter that has a filter pattern for DECRYP_ERROR. Create a CloudWatch alarm on this metric for a threshold >=1. Configure the alarm to send Amazon Simple Notification Service (Amazon SNS) notifications.
D. Install the CloudWatch unified agent on the EC2 instance. Configure the application to generate a metric for the keyword DECRYP_ERROR errors. Configure the agent to send Amazon Simple Notification Service (Amazon SNS) notifications.

Suggested Answer: C

• CloudWatch Logs can use filter expressions
  • For example, find a specific IP inside of a log
  • Or count occurrences of “ERROR” in your logs 
• Metric filters can be used to trigger CloudWatch alarms

CloudWatch Logs Insights can be used to query logs and add queries to CloudWatch Dashboard

---

Question #: 74
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer created an AWS Lambda function that accesses resources in a VPC. The Lambda function polls an Amazon Simple Queue Service (Amazon SQS) queue for new messages through a VPC endpoint. Then the function calculates a rolling average of the numeric values that are contained in the messages. After initial tests of the Lambda function, the developer found that the value of the rolling average that the function returned was not accurate.

How can the developer ensure that the function calculates an accurate rolling average?

A. Set the function's reserved concurrency to 1. Calculate the rolling average in the function. Store the calculated rolling average in Amazon ElastiCache.
B. Modify the function to store the values in Amazon ElastiCache. When the function initializes, use the previous values from the cache to calculate the rolling average.
C. Set the function's provisioned concurrency to 1. Calculate the rolling average in the function. Store the calculated rolling average in Amazon ElastiCache.
D. Modify the function to store the values in the function's layers. When the function initializes, use the previously stored values to calculate the rolling average.

Suggested Answer: A

不确定

---

Question #: 75
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is writing unit tests for a new application that will be deployed on AWS. The developer wants to validate all pull requests with unit tests and merge the code with the main branch only when all tests pass.

The developer stores the code in AWS CodeCommit and sets up AWS CodeBuild to run the unit tests. The developer creates an AWS Lambda function to start the CodeBuild task. The developer needs to identify the CodeCommit events in an Amazon EventBridge event that can invoke the Lambda function when a pull request is created or updated.

Which CodeCommit event will meet these requirements?

![](75.png)

Suggested Answer: C

pullRequestSourceBranchUpdated 事件

在此示例事件中，代入名为 Admin 的角色（会话名称为 Mary_Major）的用户为 ID 为 1 的拉取请求更新了名为 test-branch 的源分支。

pullRequestCreated 事件

在此示例事件中，在名为 MyDemoRepo 的存储库中创建了一个拉取请求，创建者为代入名为 Admin 的角色（会话名称为 Mary_Major）的用户。未提供会话标记信息，因此该信息不包含在事件中。

---

Question #: 76
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer deployed an application to an Amazon EC2 instance. The application needs to know the public IPv4 address of the instance.

How can the application find this information?

A. Query the instance metadata from http://169.254.169.254/latest/meta-data/.
B. Query the instance user data from http://169.254.169.254/latest/user-data/.
C. Query the Amazon Machine Image (AMI) information from http://169.254.169.254/latest/meta-data/ami/.
D. Check the hosts file of the operating system.

Suggested Answer: A

---

Question #: 77
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
An application under development is required to store hundreds of video files. The data must be encrypted within the application prior to storage, with a unique key for each video file.

How should the developer code the application?

A. Use the KMS Encrypt API to encrypt the data. Store the encrypted data key and data.
B. Use a cryptography library to generate an encryption key for the application. Use the encryption key to encrypt the data. Store the encrypted data.
C. Use the KMS GenerateDataKey API to get a data key. Encrypt the data with the data key. Store the encrypted data key and data.
D. Upload the data to an S3 bucket using server side-encryption with an AWS KMS key.

Suggested Answer: C 

---

Question #: 78
Topic #: 1
[All AWS Certified Developer Associate Questions]

A developer has created a web API that uses Amazon Elastic Container Service (Amazon ECS) and an Application Load Balancer (ALB). An Amazon CloudFront distribution uses the API as an origin for web clients. The application has received millions of requests with a JSON Web Token (JWT) that is not valid in the authorization header. The developer has scaled out the application to handle the unauthenticated requests.
What should the developer do to reduce the number of unauthenticated requests to the API?

A. Add a request routing rule to the ALB to return a 401 status code if the authorization header is missing.
B. Add a container to the ECS task definition to validate JWTs Set the new container as a dependency of the application container.
C. Create a CloudFront function for the distribution Use the crypto module in the function to validate the JWT.
D. Add a custom authorizer for AWS Lambda to the CloudFront distribution to validate the JWT.

Suggested Answer: C 

A: 有的有header但是header是无效的，要检查header
B: 狗屁不通
D: 和lambda无关

---

Question #: 79
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer wants to debug an application by searching and filtering log data. The application logs are stored in Amazon CloudWatch Logs. The developer creates a new metric filter to count exceptions in the application logs. However, no results are returned from the logs.

What is the reason that no filtered results are being returned?

A. A setup of the Amazon CloudWatch interface VPC endpoint is required for filtering the CloudWatch Logs in the VPC.
B. CloudWatch Logs only publishes metric data for events that happen after the filter is created.
C. The log group for CloudWatch Logs should be first streamed to Amazon OpenSearch Service before metric filtering returns the results.
D. Metric data points for logs groups can be filtered only after they are exported to an Amazon S3 bucket.

Suggested Answer: B

Filters do not retroactively filter data. Filters only publish the metric data points for events that happen after the filter was created.
筛选条件不会以回溯方式筛选数据。筛选条件只会发布在创建后发生的事件的指标数据点。筛选结果返回前 50 行，如果筛选结果上的时间戳早于指标创建时间，则不会显示这些行。

---

Question #: 80
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is planning to use AWS CodeDeploy to deploy an application to Amazon Elastic Container Service (Amazon ECS). During the deployment of a new version of the application, the company initially must expose only 10% of live traffic to the new version of the deployed application. Then, after 15 minutes elapse, the company must route all the remaining live traffic to the new version of the deployed application.

Which CodeDeploy predefined configuration will meet these requirements?

A. CodeDeployDefault.ECSCanary10Percent15Minutes
B. CodeDeployDefault.LambdaCanary10Percent5Minutes
C. CodeDeployDefault.LambdaCanary10Percentl15Minutes
D. CodeDeployDefault.ECSLinear10PercentEvery1Minutes

Suggested Answer: A

---

Question #: 81
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company hosts a batch processing application on AWS Elastic Beanstalk with instances that run the most recent version of Amazon Linux. The application sorts and processes large datasets.

In recent weeks, the application's performance has decreased significantly during a peak period for traffic. A developer suspects that the application issues are related to the memory usage. The developer checks the Elastic Beanstalk console and notices that memory usage is not being tracked.

How should the developer gather more information about the application performance issues?

A. Configure the Amazon CloudWatch agent to push logs to Amazon CloudWatch Logs by using port 443.
B. Configure the Elastic Beanstalk .ebextensions directory to track the memory usage of the instances.
C. Configure the Amazon CloudWatch agent to track the memory usage of the instances.
D. Configure an Amazon CloudWatch dashboard to track the memory usage of the instances.

Suggested Answer: C

---

Question #: 82
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is building a highly secure healthcare application using serverless components. This application requires writing temporary data to /tmp storage on an AWS Lambda function.

How should the developer encrypt this data?

A. Enable Amazon EBS volume encryption with an AWS KMS key in the Lambda function configuration so that all storage attached to the Lambda function is encrypted.
B. Set up the Lambda function with a role and key policy to access an AWS KMS key. Use the key to generate a data key used to encrypt all data prior to writing to /tmp storage.
C. Use OpenSSL to generate a symmetric encryption key on Lambda startup. Use this key to encrypt the data prior to writing to /tmp.
D. Use an on-premises hardware security module (HSM) to generate keys, where the Lambda function requests a data key from the HSM and uses that to encrypt data on all requests to the function.

Suggested Answer: B 

---

Question #: 83
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer has created an AWS Lambda function to provide notification through Amazon Simple Notification Service (Amazon SNS) whenever a file is uploaded to Amazon S3 that is larger than 50 MB. The developer has deployed and tested the Lambda function by using the CLI. However, when the event notification is added to the S3 bucket and a 3,000 MB file is uploaded, the Lambda function does not launch.

Which of the following is a possible reason for the Lambda function's inability to launch?

A. The S3 event notification does not activate for files that are larger than 1,000 MB.
B. The resource-based policy for the Lambda function does not have the required permissions to be invoked by Amazon S3.
C. Lambda functions cannot be invoked directly from an S3 event.
D. The S3 bucket needs to be made public.

Suggested Answer: B 

---

Question #: 84
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating a Ruby application and needs to automate the deployment, scaling, and management of an environment without requiring knowledge of the underlying infrastructure.

Which service would best accomplish this task?

A. AWS CodeDeploy
B. AWS CloudFormation
C. AWS OpsWorks
D. AWS Elastic Beanstalk

Suggested Answer: D

---

Question #: 85
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has a web application that is deployed on AWS. The application uses an Amazon API Gateway API and an AWS Lambda function as its backend.

The application recently demonstrated unexpected behavior. A developer examines the Lambda function code, finds an error, and modifies the code to resolve the problem. Before deploying the change to production, the developer needs to run tests to validate that the application operates properly.

The application has only a production environment available. The developer must create a new development environment to test the code changes. The developer must also prevent other developers from overwriting these changes during the test cycle.

Which combination of steps will meet these requirements with the LEAST development effort? (Choose two.)

A. Create a new resource in the current stage. Create a new method with Lambda proxy integration. Select the Lambda function. Add the hotfix alias. Redeploy the current stage. Test the backend.
B. Update the Lambda function in the API Gateway API integration request to use the hotfix alias. Deploy the API Gateway API to a new stage named hotfix. Test the backend.
C. Modify the Lambda function by fixing the code. Test the Lambda function. Create the alias hotfix. Point the alias to the $LATEST version.
D. Modify the Lambda function by fixing the code. Test the Lambda function. When the Lambda function is working as expected, publish the Lambda function as a new version. Create the alias hotfix. Point the alias to the new version.
E. Create a new API Gateway API for the development environment. Add a resource and method with Lambda integration. Choose the Lambda function and the hotfix alias. Deploy to a new stage. Test the backend.

Suggested Answer: BD 

It is B & D.

Clearly E isn't operationally efficient. So we got to choose from A & B one, and C & D the second.

Between A & B, we gotta pick B since in the question it clearly states that we don't want to touch the existing solution.

Regarding C & D, seems like D is more thorough and also pointing to $LATEST is not sufficiently explicit when you troubleshoot.

---

Question #: 86
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is implementing an AWS Cloud Development Kit (AWS CDK) serverless application. The developer will provision several AWS Lambda functions and Amazon API Gateway APIs during AWS CloudFormation stack creation. The developer's workstation has the AWS Serverless Application Model (AWS SAM) and the AWS CDK installed locally.

How can the developer test a specific Lambda function locally?

A. Run the sam package and sam deploy commands. Create a Lambda test event from the AWS Management Console. Test the Lambda function.
B. Run the cdk synth and cdk deploy commands. Create a Lambda test event from the AWS Management Console. Test the Lambda function.
C. Run the cdk synth and sam local invoke commands with the function construct identifier and the path to the synthesized CloudFormation template.
D. Run the cdk synth and sam local start-lambda commands with the function construct identifier and the path to the synthesized CloudFormation template.

Suggested Answer: C

https://docs.aws.amazon.com/zh_cn/serverless-application-model/latest/developerguide/using-sam-cli-local-invoke.html

使用AWS Serverless Application Model命令行接口 (AWS SAMCLI)sam local start-lambda 子命令通过AWS Command Line Interface (AWS CLI) 或 SDK 调用您的AWS Lambda函数。此命令启动模拟的本地端点AWS Lambda。
使用AWS Serverless Application Model命令行接口 (AWS SAMCLI)sam local invoke 子命令在本地启动AWS Lambda函数的一次性调用。

• Locally start AWS Lambda

sam local start-lambda
• Starts a local endpoint that emulates AWS Lambda
• Can run automated tests against this local endpoint
• Locally Invoke Lambda Function

sam local invoke
• Invoke Lambda function with payload once and quit after invocation completes
• Helpful for generating test cases
• If the function make API calls to AWS, make sure you are using the correct --profile option

传递自定义事件调用 Lambda 函数

要将事件传递给 Lambda 函数，请使用--event选项。以下是示例：

`$ sam local invoke --event events/s3.json S3JsonLoggerFunction`

您可以使用sam local generate-event子命令创建事件。要了解更多信息，请参阅 使用 sam local generate-event。

https://docs.aws.amazon.com/zh_cn/cdk/v2/guide/hello_world.html

CDK – Important Commands to know
Command Description
npm install -g aws-cdk-lib - Install the CDK CLI and libraries
cdk init app - Create a new CDK project from a specified template
cdk synth - Synthesizes and prints the CloudFormation template
cdk bootstrap - Deploys the CDK Toolkit staging Stack
cdk deploy - Deploy the Stack(s)
cdk diff - View differences of local CDK and deployed Stack
cdk destroy - Destroy the Stack(s)

---

Question #: 88
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company caches session information for a web application in an Amazon DynamoDB table. The company wants an automated way to delete old items from the table.

What is the simplest way to do this?

A. Write a script that deletes old records; schedule the script as a cron job on an Amazon EC2 instance.
B. Add an attribute with the expiration time; enable the Time To Live feature based on that attribute.
C. Each day, create a new table to hold session data; delete the previous day's table.
D. Add an attribute with the expiration time; name the attribute ItemExpiration.

Suggested Answer: B

---

Question #: 89
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is using an Amazon API Gateway REST API endpoint as a webhook to publish events from an on-premises source control management (SCM) system to Amazon EventBridge. The company has configured an EventBridge rule to listen for the events and to control application deployment in a central AWS account. The company needs to receive the same events across multiple receiver AWS accounts.

How can a developer meet these requirements without changing the configuration of the SCM system?

A. Deploy the API Gateway REST API to all the required AWS accounts. Use the same custom domain name for all the gateway endpoints so that a single SCM webhook can be used for all events from all accounts.
B. Deploy the API Gateway REST API to all the receiver AWS accounts. Create as many SCM webhooks as the number of AWS accounts.
C. Grant permission to the central AWS account for EventBridge to access the receiver AWS accounts. Add an EventBridge event bus on the receiver AWS accounts as the targets to the existing EventBridge rule.
D. Convert the API Gateway type from REST API to HTTP API.

Suggested Answer: C


---

Question #: 90
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company moved some of its secure files to a private Amazon S3 bucket that has no public access. The company wants to develop a serverless application that gives its employees the ability to log in and securely share the files with other users.

Which AWS feature should the company use to share and access the files securely?

A. Amazon Cognito user pool
B. S3 presigned URLs
C. S3 bucket policy
D. Amazon Cognito identity pool

Suggested Answer: A / B 不确定

---

Question #: 91
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company needs to develop a proof of concept for a web service application. The application will show the weather forecast for one of the company's office locations. The application will provide a REST endpoint that clients can call. Where possible, the application should use caching features provided by AWS to limit the number of requests to the backend service. The application backend will receive a small amount of traffic only during testing.

Which approach should the developer take to provide the REST endpoint MOST cost-effectively?

A. Create a container image. Deploy the container image by using Amazon Elastic Kubernetes Service (Amazon EKS). Expose the functionality by using Amazon API Gateway.
B. Create an AWS Lambda function by using the AWS Serverless Application Model (AWS SAM). Expose the Lambda functionality by using Amazon API Gateway.
C. Create a container image. Deploy the container image by using Amazon Elastic Container Service (Amazon ECS). Expose the functionality by using Amazon API Gateway.
D. Create a microservices application. Deploy the application to AWS Elastic Beanstalk. Expose the AWS Lambda functionality by using an Application Load Balancer.

Suggested Answer: B

---

Question #: 92
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
An e-commerce web application that shares session state on-premises is being migrated to AWS. The application must be fault tolerant, natively highly scalable, and any service interruption should not affect the user experience.

What is the best option to store the session state?

A. Store the session state in Amazon ElastiCache.
B. Store the session state in Amazon CloudFront.
C. Store the session state in Amazon S3.
D. Enable session stickiness using elastic load balancers.

Suggested Answer: A 

---

Question #: 93
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is building an application that uses Amazon DynamoDB. The developer wants to retrieve multiple specific items from the database with a single API call.

Which DynamoDB API call will meet these requirements with the MINIMUM impact on the database?

A. BatchGetItem
B. GetItem
C. Scan
D. Query

Suggested Answer: A


DynamoDB – Batch Operations
• Allows you to save in latency by reducing the number of API calls
• Operations are done in parallel for better efficiency
• Part of a batch can fail; in which case we need to try again for the failed items

BatchWriteItem
• Up to 25 PutItem and/or DeleteItem in one call
• Up to 16 MB of data written, up to 400 KB of data per item
• Can’t update items (use UpdateItem)
• UnprocessedItems for failed write operations (exponential backoff or add WCU)

BatchGetItem
• Return items from one or more tables
• Up to 100 items, up to 16 MB of data
• Items are retrieved in parallel to minimize latency
• UnprocessedKeys for failed read operations (exponential backoff or add RCU)

---

Question #: 94
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer has written an application that runs on Amazon EC2 instances. The developer is adding functionality for the application to write objects to an Amazon S3 bucket.

Which policy must the developer modify to allow the instances to write these objects?

A. The IAM policy that is attached to the EC2 instance profile role
B. The session policy that is applied to the EC2 instance role session
C. The AWS Key Management Service (AWS KMS) key policy that is attached to the EC2 instance profile role
D. The Amazon VPC endpoint policy

Suggested Answer: A 

---

Question #: 95
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is leveraging a Border Gateway Protocol (BGP)-based AWS VPN connection to connect from on-premises to Amazon EC2 instances in the developer's account. The developer is able to access an EC2 instance in subnet A, but is unable to access an EC2 instance in subnet B in the same VPC.

Which logs can the developer use to verify whether the traffic is reaching subnet B?

A. VPN logs
B. BGP logs
C. VPC Flow Logs
D. AWS CloudTrail logs


Suggested Answer: C 

VPC Flow Logs
• Capture information about IP traffic going into your interfaces:
  • VPC Flow Logs
  • Subnet Flow Logs
  • Elastic Network Interface Flow Logs
• Helps to monitor & troubleshoot connectivity issues. Example:
  • Subnets to internet
  • Subnets to subnets
  • Internet to subnets
• Captures network information from AWS managed interfaces too: Elastic Load Balancers, ElastiCache, RDS, Aurora, etc…
• VPC Flow logs data can go to S3 / CloudWatch Logs

---

Question #: 96
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating a service that uses an Amazon S3 bucket for image uploads. The service will use an AWS Lambda function to create a thumbnail of each image. Each time an image is uploaded, the service needs to send an email notification and create the thumbnail. The developer needs to configure the image processing and email notifications setup.

Which solution will meet these requirements?

A. Create an Amazon Simple Notification Service (Amazon SNS) topic. Configure S3 event notifications with a destination of the SNS topic. Subscribe the Lambda function to the SNS topic. Create an email notification subscription to the SNS topic.
B. Create an Amazon Simple Notification Service (Amazon SNS) topic. Configure S3 event notifications with a destination of the SNS topic. Subscribe the Lambda function to the SNS topic. Create an Amazon Simple Queue Service (Amazon SQS) queue. Subscribe the SQS queue to the SNS topic. Create an email notification subscription to the SQS queue.
C. Create an Amazon Simple Queue Service (Amazon SQS) queue. Configure S3 event notifications with a destination of the SQS queue. Subscribe the Lambda function to the SQS queue. Create an email notification subscription to the SQS queue.
D. Create an Amazon Simple Queue Service (Amazon SQS) queue. Send S3 event notifications to Amazon EventBridge. Create an EventBridge rule that runs the Lambda function when images are uploaded to the S3 bucket. Create an EventBridge rule that sends notifications to the SQS queue. Create an email notification subscription to the SQS queue.

Suggested Answer: A

---

Question #: 97
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer has designed an application to store incoming data as JSON files in Amazon S3 objects. Custom business logic in an AWS Lambda function then transforms the objects, and the Lambda function loads the data into an Amazon DynamoDB table. Recently, the workload has experienced sudden and significant changes in traffic. The flow of data to the DynamoDB table is becoming throttled.

The developer needs to implement a solution to eliminate the throttling and load the data into the DynamoDB table more consistently.

Which solution will meet these requirements?

A. Refactor the Lambda function into two functions. Configure one function to transform the data and one function to load the data into the DynamoDB table. Create an Amazon Simple Queue Service (Amazon SQS) queue in between the functions to hold the items as messages and to invoke the second function.
B. Turn on auto scaling for the DynamoDB table. Use Amazon CloudWatch to monitor the table's read and write capacity metrics and to track consumed capacity.
C. Create an alias for the Lambda function. Configure provisioned concurrency for the application to use.
D. Refactor the Lambda function into two functions. Configure one function to store the data in the DynamoDB table. Configure the second function to process the data and update the items after the data is stored in DynamoDB. Create a DynamoDB stream to invoke the second function after the data is stored.

A / D / B 不确定

---

Question #: 98
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating an AWS Lambda function in VPC mode. An Amazon S3 event will invoke the Lambda function when an object is uploaded into an S3 bucket. The Lambda function will process the object and produce some analytic results that will be recorded into a file. Each processed object will also generate a log entry that will be recorded into a file.

Other Lambda functions, AWS services, and on-premises resources must have access to the result files and log file. Each log entry must also be appended to the same shared log file. The developer needs a solution that can share files and append results into an existing file.

Which solution should the developer use to meet these requirements?

A. Create an Amazon Elastic File System (Amazon EFS) file system. Mount the EFS file system in Lambda. Store the result files and log file in the mount point. Append the log entries to the log file.
B. Create an Amazon Elastic Block Store (Amazon EBS) Multi-Attach enabled volume. Attach the EBS volume to all Lambda functions. Update the Lambda function code to download the log file, append the log entries, and upload the modified log file to Amazon EBS.
C. Create a reference to the /tmp local directory. Store the result files and log file by using the directory reference. Append the log entry to the log file.
D. Create a reference to the /opt storage directory. Store the result files and log file by using the directory reference. Append the log entry to the log file.

Suggested Answer: A

其它服务也都要访问文件

Lambda – File Systems Mounting
• Lambda functions can access EFS file systems if they are running in a VPC
• Configure Lambda to mount EFS file systems to local directory during initialization
• Must leverage EFS Access Points
• Limitations: watch out for the EFS connection limits (one function instance = one connection) and connection burst limits

Amazon ECS – Data Volumes (EFS)
• Mount EFS file systems onto ECS tasks
• Works for both EC2 and Fargate launch types
• Tasks running in any AZ will share the same data in the EFS file system
• Fargate + EFS = Serverless
• Use cases: persistent multi-AZ shared storage for your containers

---

Question #: 99
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has an AWS Lambda function that processes incoming requests from an Amazon API Gateway API. The API calls the Lambda function by using a Lambda alias. A developer updated the Lambda function code to handle more details related to the incoming requests. The developer wants to deploy the new Lambda function for more testing by other developers with no impact to customers that use the API.

Which solution will meet these requirements with the LEAST operational overhead?

A. Create a new version of the Lambda function. Create a new stage on API Gateway with integration to the new Lambda version. Use the new API Gateway stage to test the Lambda function.
B. Update the existing Lambda alias used by API Gateway to a weighted alias. Add the new Lambda version as an additional Lambda function with a weight of 10%. Use the existing API Gateway stage for testing.
C. Create a new version of the Lambda function. Create and deploy a second Lambda function to filter incoming requests from API Gateway. If the filtering Lambda function detects a test request, the filtering Lambda function will invoke the new Lambda version of the code. For other requests, the filtering Lambda function will invoke the old Lambda version. Update the API Gateway API to use the filtering Lambda function.
D. Create a new version of the Lambda function. Create a new API Gateway API for testing purposes. Update the integration of the new API with the new Lambda version. Use the new API for testing.

Suggested Answer: A

---

Question #: 100
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company uses AWS Lambda functions and an Amazon S3 trigger to process images into an S3 bucket. A development team set up multiple environments in a single AWS account.

After a recent production deployment, the development team observed that the development S3 buckets invoked the production environment Lambda functions. These invocations caused unwanted execution of development S3 files by using production Lambda functions. The development team must prevent these invocations. The team must follow security best practices.

Which solution will meet these requirements?

A. Update the Lambda execution role for the production Lambda function to add a policy that allows the execution role to read from only the production environment S3 bucket.
B. Move the development and production environments into separate AWS accounts. Add a resource policy to each Lambda function to allow only S3 buckets that are within the same account to invoke the function.
C. Add a resource policy to the production Lambda function to allow only the production environment S3 bucket to invoke the function.
D. Move the development and production environments into separate AWS accounts. Update the Lambda execution role for each function to add a policy that allows the execution role to read from the S3 bucket that is within the same account.

Suggested Answer: B / C 不确定

https://wa.aws.amazon.com/wat.question.SEC_1.en.html

Best Practices:
Separate workloads using accounts: Establish common guardrails and isolation between environments (such as production, development, and test) and workloads through a multi-account strategy. Account-level separation is strongly recommended, as it provides a strong isolation boundary for security, billing, and access.

---

Question #: 101
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating an application. New users of the application must be able to create an account and register by using their own social media accounts.

Which AWS service or resource should the developer use to meet these requirements?

A. IAM role
B. Amazon Cognito identity pools
C. Amazon Cognito user pools
D. AWS Directory Service

Suggested Answer: C 

---

Question #: 102
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A social media application uses the AWS SDK for JavaScript on the frontend to get user credentials from AWS Security Token Service (AWS STS). The application stores its assets in an Amazon S3 bucket. The application serves its content by using an Amazon CloudFront distribution with the origin set to the S3 bucket.

The credentials for the role that the application assumes to make the SDK calls are stored in plaintext in a JSON file within the application code. The developer needs to implement a solution that will allow the application to get user credentials without having any credentials hardcoded in the application code.

Which solution will meet these requirements?

A. Add a Lambda@Edge function to the distribution. Invoke the function on viewer request. Add permissions to the function's execution role to allow the function to access AWS STS. Move all SDK calls from the frontend into the function.
B. Add a CloudFront function to the distribution. Invoke the function on viewer request. Add permissions to the function's execution role to allow the function to access AWS STS. Move all SDK calls from the frontend into the function.
C. Add a Lambda@Edge function to the distribution. Invoke the function on viewer request. Move the credentials from the JSON file into the function. Move all SDK calls from the frontend into the function.
D. Add a CloudFront function to the distribution. Invoke the function on viewer request. Move the credentials from the JSON file into the function. Move all SDK calls from the frontend into the function.

Suggested Answer: A

The answer is A. Here is a reference directly from AWS docs:

"If you need some of the capabilities of Lambda@Edge that are not available with CloudFront Functions, such as network access or a longer execution time, you can still use Lambda@Edge before and after content is cached by CloudFront."

Since the requirement is to access the STS service, network access is required. Therefore, it can't be Cloudfront functions. Also, as a side note it's worth to mention that Cloudfront functions can only execute for up to 1ms. Apparently this isn't enough to fetch user creds (tokens) from STS.

The table in the following link summarises the differences between Cloudfront functions and Lambda@edge

https://aws.amazon.com/blogs/aws/introducing-cloudfront-functions-run-your-code-at-the-edge-with-low-latency-at-any-scale/

---

Question #: 103
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

An ecommerce website uses an AWS Lambda function and an Amazon RDS for MySQL database for an order fulfillment service. The service needs to return order confirmation immediately.

During a marketing campaign that caused an increase in the number of orders, the website's operations team noticed errors for “too many connections” from Amazon RDS. However, the RDS DB cluster metrics are healthy. CPU and memory capacity are still available.

What should a developer do to resolve the errors?

A. Initialize the database connection outside the handler function. Increase the max_user_connections value on the parameter group of the DB cluster. Restart the DB cluster.
B. Initialize the database connection outside the handler function. Use RDS Proxy instead of connecting directly to the DB cluster.
C. Use Amazon Simple Queue Service (Amazon SQS) FIFO queues to queue the orders. Ingest the orders into the database. Set the Lambda function's concurrency to a value that equals the number of available database connections.
D. Use Amazon Simple Queue Service (Amazon SQS) FIFO queues to queue the orders. Ingest the orders into the database. Set the Lambda function's concurrency to a value that is less than the number of available database connections.

Suggested Answer: B

---

Question #: 104
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A company stores its data in data tables in a series of Amazon S3 buckets. The company received an alert that customer credit card information might have been exposed in a data table on one of the company's public applications. A developer needs to identify all potential exposures within the application environment.

Which solution will meet these requirements?

A. Use Amazon Athena to run a job on the S3 buckets that contain the affected data. Filter the findings by using the SensitiveData:S3Object/Personal finding type.
B. Use Amazon Macie to run a job on the S3 buckets that contain the affected data. Filter the findings by using the SensitiveData:S3Object/Financial finding type.
C. Use Amazon Macie to run a job on the S3 buckets that contain the affected data. Filter the findings by using the SensitiveData:S3Object/Personal finding type.
D. Use Amazon Athena to run a job on the S3 buckets that contain the affected data. Filter the findings by using the SensitiveData:S3Object/Financial finding type.

Suggested Answer: B

---

Question #: 105
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A software company is launching a multimedia application. The application will allow guest users to access sample content before the users decide if they want to create an account to gain full access. The company wants to implement an authentication process that can identify users who have already created an account. The company also needs to keep track of the number of guest users who eventually create an account.

Which combination of steps will meet these requirements? (Choose two.)

A. Create an Amazon Cognito user pool. Configure the user pool to allow unauthenticated users. Exchange user tokens for temporary credentials that allow authenticated users to assume a role.
B. Create an Amazon Cognito identity pool. Configure the identity pool to allow unauthenticated users. Exchange unique identity for temporary credentials that allow all users to assume a role.
C. Create an Amazon CloudFront distribution. Configure the distribution to allow unauthenticated users. Exchange user tokens for temporary credentials that allow all users to assume a role.
D. Create a role for authenticated users that allows access to all content. Create a role for unauthenticated users that allows access to only the sample content.
E. Allow all users to access the sample content by default. Create a role for authenticated users that allows access to the other content.

Suggested Answer: BD

option B because by configuring the identity pool to allow unauthenticated users, you can enable guest users to access the sample content. When users create an account, they can be authenticated, and then given access to the full content by assuming a role that allows them access.
Option D is correct because creating roles for authenticated and unauthenticated users with different levels of access is an appropriate way to meet the requirement of identifying users who have created an account and keeping track of the number of guest users who eventually create an account.


• Cognito Identity Pools allow for unauthenticated (guest) access

---

Question #: 106
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A company is updating an application to move the backend of the application from Amazon EC2 instances to a serverless model. The application uses an Amazon RDS for MySQL DB instance and runs in a single VPC on AWS. The application and the DB instance are deployed in a private subnet in the VPC.

The company needs to connect AWS Lambda functions to the DB instance.

Which solution will meet these requirements?

A. Create Lambda functions inside the VPC with the AWSLambdaBasicExecutionRole policy attached to the Lambda execution role. Modify the RDS security group to allow inbound access from the Lambda security group.
B. Create Lambda functions inside the VPC with the AWSLambdaVPCAccessExecutionRole policy attached to the Lambda execution role. Modify the RDS security group to allow inbound access from the Lambda security group.
C. Create Lambda functions with the AWSLambdaBasicExecutionRole policy attached to the Lambda execution role. Create an interface VPC endpoint for the Lambda functions. Configure the interface endpoint policy to allow the lambda:InvokeFunclion action for each Lambda function's Amazon Resource Name (ARN).
D. Create Lambda functions with the AWSLambdaVPCAccessExecutionRole policy attached to the Lambda execution role. Create an interface VPC endpoint for the Lambda functions. Configure the interface endpoint policy to allow the lambda:InvokeFunction action for each Lambda function's Amazon Resource Name (ARN).

Suggested Answer: B

---

Question #: 107
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A company has a web application that runs on Amazon EC2 instances with a custom Amazon Machine Image (AMI). The company uses AWS CloudFormation to provision the application. The application runs in the us-east-1 Region, and the company needs to deploy the application to the us-west-1 Region.

An attempt to create the AWS CloudFormation stack in us-west-1 fails. An error message states that the AMI ID does not exist. A developer must resolve this error with a solution that uses the least amount of operational overhead.

Which solution meets these requirements?

A. Change the AWS CloudFormation templates for us-east-1 and us-west-1 to use an AWS AMI. Relaunch the stack for both Regions.
B. Copy the custom AMI from us-east-1 to us-west-1. Update the AWS CloudFormation template for us-west-1 to refer to AMI ID for the copied AMI. Relaunch the stack.
C. Build the custom AMI in us-west-1. Create a new AWS CloudFormation template to launch the stack in us-west-1 with the new AMI ID.
D. Manually deploy the application outside AWS CloudFormation in us-west-1.

Suggested Answer: B

---

Question #: 108
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer is updating several AWS Lambda functions and notices that all the Lambda functions share the same custom libraries. The developer wants to centralize all the libraries, update the libraries in a convenient way, and keep the libraries versioned.

Which solution will meet these requirements with the LEAST development effort?

A. Create an AWS CodeArtifact repository that contains all the custom libraries.
B. Create a custom container image for the Lambda functions to save all the custom libraries.
C. Create a Lambda layer that contains all the custom libraries.
D. Create an Amazon Elastic File System (Amazon EFS) file system to store all the custom libraries.

Suggested Answer: C

---

Question #: 109
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer wants to use AWS Elastic Beanstalk to test a new version of an application in a test environment.

Which deployment method offers the FASTEST deployment?

A. Immutable
B. Rolling
C. Rolling with additional batch
D. All at once

Suggested Answer: D

---

Question #: 110
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is providing read access to objects in an Amazon S3 bucket for different customers. The company uses IAM permissions to restrict access to the S3 bucket. The customers can access only their own files.

Due to a regulation requirement, the company needs to enforce encryption in transit for interactions with Amazon S3.

Which solution will meet these requirements?

A. Add a bucket policy to the S3 bucket to deny S3 actions when the aws:SecureTransport condition is equal to false.
B. Add a bucket policy to the S3 bucket to deny S3 actions when the s3:x-amz-acl condition is equal to public-read.
C. Add an IAM policy to the IAM users to enforce the usage of the AWS SDK.
D. Add an IAM policy to the IAM users that allows S3 actions when the s3:x-amz-acl condition is equal to bucket-owner-read.

Suggested Answer: A

---

Question #: 111
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has an image storage web application that runs on AWS. The company hosts the application on Amazon EC2 instances in an Auto Scaling group. The Auto Scaling group acts as the target group for an Application Load Balancer (ALB) and uses an Amazon S3 bucket to store the images for sale.

The company wants to develop a feature to test system requests. The feature will direct requests to a separate target group that hosts a new beta version of the application.

Which solution will meet this requirement with the LEAST effort?

A. Create a new Auto Scaling group and target group for the beta version of the application. Update the ALB routing rule with a condition that looks for a cookie named version that has a value of beta. Update the test system code to use this cookie to test the beta version of the application.
B. Create a new ALB, Auto Scaling group, and target group for the beta version of the application. Configure an alternate Amazon Route 53 record for the new ALB endpoint. Use the alternate Route 53 endpoint in the test system requests to test the beta version of the application.
C. Create a new ALB, Auto Scaling group, and target group for the beta version of the application. Use Amazon CloudFront with Lambda@Edge to determine which specific request will go to the new ALB. Use the CloudFront endpoint to send the test system requests to test the beta version of the application.
D. Create a new Auto Scaling group and target group for the beta version of the application. Update the ALB routing rule with a condition that looks for a cookie named version that has a value of beta. Use Amazon CloudFront with Lambda@Edge to update the test system requests to add the required cookie when the requests go to the ALB.

Suggested Answer: A / B 不确定

---

Exam question from Amazon's AWS Certified Developer - Associate DVA-C02
Question #: 112
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A team is developing an application that is deployed on Amazon EC2 instances. During testing, the team receives an error. The EC2 instances are unable to access an Amazon S3 bucket.

Which steps should the team take to troubleshoot this issue? (Choose two.)

A. Check whether the policy that is assigned to the IAM role that is attached to the EC2 instances grants access to Amazon S3.
B. Check the S3 bucket policy to validate the access permissions for the S3 bucket.
C. Check whether the policy that is assigned to the IAM user that is attached to the EC2 instances grants access to Amazon S3.
D. Check the S3 Lifecycle policy to validate the permissions that are assigned to the S3 bucket.
E. Check the security groups that are assigned to the EC2 instances. Make sure that a rule is not blocking the access to Amazon S3.

Suggested Answer: AB

---

Question #: 113
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer is working on an ecommerce website. The developer wants to review server logs without logging in to each of the application servers individually. The website runs on multiple Amazon EC2 instances, is written in Python, and needs to be highly available.

How can the developer update the application to meet these requirements with MINIMUM changes?

A. Rewrite the application to be cloud native and to run on AWS Lambda, where the logs can be reviewed in Amazon CloudWatch.
B. Set up centralized logging by using Amazon OpenSearch Service, Logstash, and OpenSearch Dashboards.
C. Scale down the application to one larger EC2 instance where only one instance is recording logs.
D. Install the unified Amazon CloudWatch agent on the EC2 instances. Configure the agent to push the application logs to CloudWatch.

Suggested Answer: D 

---

Question #: 114
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is creating an application that processes .csv files from Amazon S3. A developer has created an S3 bucket. The developer has also created an AWS Lambda function to process the .csv files from the S3 bucket.

Which combination of steps will invoke the Lambda function when a .csv file is uploaded to Amazon S3? (Choose two.)

A. Create an Amazon EventBridge rule. Configure the rule with a pattern to match the S3 object created event.
B. Schedule an Amazon EventBridge rule to run a new Lambda function to scan the S3 bucket.
C. Add a trigger to the existing Lambda function. Set the trigger type to EventBridge. Select the Amazon EventBridge rule.
D. Create a new Lambda function to scan the S3 bucket for recently added S3 objects.
E. Add S3 Lifecycle rules to invoke the existing Lambda function.

Suggested Answer: AC

---

Question #: 115
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer needs to build an AWS CloudFormation template that self-populates the AWS Region variable that deploys the CloudFormation template.

What is the MOST operationally efficient way to determine the Region in which the template is being deployed?

A. Use the AWS::Region pseudo parameter.
B. Require the Region as a CloudFormation parameter.
C. Find the Region from the AWS::StackId pseudo parameter by using the Fn::Split intrinsic function.
D. Dynamically import the Region by referencing the relevant parameter in AWS Systems Manager Parameter Store.

Suggested Answer: A

---

Question #: 116
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A company has hundreds of AWS Lambda functions that the company's QA team needs to test by using the Lambda function URLs. A developer needs to configure the authentication of the Lambda functions to allow access so that the QA IAM group can invoke the Lambda functions by using the public URLs.

Which solution will meet these requirements?

A. Create a CLI script that loops on the Lambda functions to add a Lambda function URL with the AWS_IAM auth type. Run another script to create an IAM identity-based policy that allows the lambda:InvokeFunctionUrl action to all the Lambda function Amazon Resource Names (ARNs). Attach the policy to the QA IAM group.
B. Create a CLI script that loops on the Lambda functions to add a Lambda function URL with the NONE auth type. Run another script to create an IAM resource-based policy that allows the lambda:InvokeFunctionUrl action to all the Lambda function Amazon Resource Names (ARNs). Attach the policy to the QA IAM group.
C. Create a CLI script that loops on the Lambda functions to add a Lambda function URL with the AWS_IAM auth type. Run another script to loop on the Lambda functions to create an IAM identity-based policy that allows the lambda:InvokeFunctionUrl action from the QA IAM group's Amazon Resource Name (ARN).
D. Create a CLI script that loops on the Lambda functions to add a Lambda function URL with the NONE auth type. Run another script to loop on the Lambda functions to create an IAM resource-based policy that allows the lambda:InvokeFunctionUrl action from the QA IAM group's Amazon Resource Name (ARN).

Suggested Answer: A 

Lambda – Function URL Security

• AuthType NONE – allow public and unauthenticated access
  • Resource-based Policy is always in effect (must grant public access)

• AuthType AWS_IAM – IAM is used to authenticate and authorize requests
  • Both Principal’s Identity-based Policy & Resource-based Policy are evaluated
  • Principal must have lambda:InvokeFunctionUrl permissions
  • Same account – Identity-based Policy OR Resource-based Policy as ALLOW
  • Cross account – Identity-based Policy AND Resource Based Policy as ALLOW

https://docs.aws.amazon.com/zh_cn/lambda/latest/dg/urls-auth.html

您可以使用 AuthType 参数和附上特定函数的基于资源的策略来控制对 Lambda 函数 URL 的访问。这两个组件的配置决定了谁可以对函数 URL 调用或执行其他管理操作。

AuthType 参数确定了 Lambda 如何对函数 URL 的请求进行身份验证或授权。配置函数 URL 时，必须指定以下 AuthType 选项之一：

AWS_IAM – Lambda 根据 IAM 主体的身份策略和函数基于资源的策略使用 AWS Identity and Access Management (IAM) 对请求进行身份验证和授权。如果只希望经过身份验证的 用户和角色通过函数 URL 调用函数，请选择此选项。

NONE – Lambda 在调用函数之前不会执行任何身份验证。但是，函数基于资源的策略始终有效，并且必须在函数 URL 接收请求之前授予公有访问权限。选择此选项可允许对函数 URL 进行未经身份验证的公有访问。

如果选择 AWS_IAM 身份验证类型，则需要调用 Lambda 函数 URL 的用户必须具有 lambda:InvokeFunctionUrl 权限。根据发出调用请求的人员，您可能需要使用基于资源的策略授予此权限。

如果发出请求的主体与函数 URL 的 AWS 账户 相同，则主体必须或者在其基于身份的策略中拥有 lambda:InvokeFunctionUrl 权限，或者在函数基于资源的策略中获授权限。换句话说，如果用户已经在其基于身份的策略中拥有 lambda:InvokeFunctionUrl 权限，则基于资源的策略为可选。策略评估遵循确定是允许还是拒绝账户内的请求中概述的规则。

如果发出请求的主体位于不同的账户中，则主体必须同时具有基于身份的策略（该策略为其提供 lambda:InvokeFunctionUrl 权限）和基于资源的策略（基于其尝试调用的函数）中授予的权限。在这些跨账户情况下，策略评估遵循确定是否允许跨账户请求中概述的规则。


```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::444455556666:role/example"
            },
            "Action": "lambda:InvokeFunctionUrl",
            "Resource": "arn:aws:lambda:us-east-1:123456789012:function:my-function",
            "Condition": {
                "StringEquals": {
                    "lambda:FunctionUrlAuthType": "AWS_IAM"
                }
            }
        }
    ]
}
```

如果选择 NONE 身份验证类型，Lambda 不会使用 IAM 对函数 URL 的请求进行身份验证。但是，用户仍必须拥有 lambda:InvokeFunctionUrl 权限才能成功调用函数 URL。您可以使用以下基于资源的策略授予 lambda:InvokeFunctionUrl 权限：

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "lambda:InvokeFunctionUrl",
            "Resource": "arn:aws:lambda:us-east-1:123456789012:function:my-function",
            "Condition": {
                "StringEquals": {
                    "lambda:FunctionUrlAuthType": "NONE"
                }
            }
        }
    ]
}
```

---

Question #: 117
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer maintains a critical business application that uses Amazon DynamoDB as the primary data store. The DynamoDB table contains millions of documents and receives 30-60 requests each minute. The developer needs to perform processing in near-real time on the documents when they are added or updated in the DynamoDB table.

How can the developer implement this feature with the LEAST amount of change to the existing application code?

A. Set up a cron job on an Amazon EC2 instance. Run a script every hour to query the table for changes and process the documents.
B. Enable a DynamoDB stream on the table. Invoke an AWS Lambda function to process the documents.
C. Update the application to send a PutEvents request to Amazon EventBridge. Create an EventBridge rule to invoke an AWS Lambda function to process the documents.
D. Update the application to synchronously process the documents directly after the DynamoDB write.

Suggested Answer: B 

---

Question #: 118
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is writing an application for a company. The application will be deployed on Amazon EC2 and will use an Amazon RDS for Microsoft SQL Server database. The company's security team requires that database credentials are rotated at least weekly.

How should the developer configure the database credentials for this application?

A. Create a database user. Store the user name and password in an AWS Systems Manager Parameter Store secure string parameter. Enable rotation of the AWS Key Management Service (AWS KMS) key that is used to encrypt the parameter.
B. Enable IAM authentication for the database. Create a database user for use with IAM authentication. Enable password rotation.
C. Create a database user. Store the user name and password in an AWS Secrets Manager secret that has daily rotation enabled.
D. Use the EC2 user data to create a database user. Provide the user name and password in environment variables to the application.

Suggested Answer: C

---

Question #: 119
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A real-time messaging application uses Amazon API Gateway WebSocket APIs with backend HTTP service. A developer needs to build a feature in the application to identify a client that keeps connecting to and disconnecting from the WebSocket connection. The developer also needs the ability to remove the client.

Which combination of changes should the developer make to the application to meet these requirements? (Choose two.)

A. Switch to HTTP APIs in the backend service.
B. Switch to REST APIs in the backend service.
C. Use the callback URL to disconnect the client from the backend service.
D. Add code to track the client status in Amazon ElastiCache in the backend service.
E. Implement $connect and $disconnect routes in the backend service.

Suggested Answer: CE/DE 不确定

https://docs.aws.amazon.com/zh_cn/apigateway/latest/developerguide/apigateway-how-to-call-websocket-api-connections.html

您后端服务可以使用以下 WebSocket 连接 HTTP 请求向连接的客户端发送回调消息、获取连接信息或断开客户端连接。

重要
这些请求使用 IAM 授权，因此您必须使用签名版本 4 (SigV4) 对其进行签名。为此，您可以使用 API Gateway 管理 API。有关更多信息，请参阅 ApiGatewayManagementApi。

在以下命令中，您需要将 {api-id} 替换为实际的 API ID，该 ID 显示在 API Gateway 控制台中或由 AWS CLI create-api 命令返回。此外，如果您的 API 位于 us-east-1 以外的区域，则需要替换正确的区域。

要向客户端发送回调消息，请使用：
POST https://{api-id}.execute-api.us-east-1.amazonaws.com/{stage}/@connections/{connection_id}
要获取客户端的最新连接状态，请使用：
GET https://{api-id}.execute-api.us-east-1.amazonaws.com/{stage}/@connections/{connection_id}
要断开客户端连接，请使用：
DELETE https://{api-id}.execute-api.us-east-1.amazonaws.com/{stage}/@connections/{connection_id}

https://docs.aws.amazon.com/zh_cn/apigateway/latest/developerguide/apigateway-websocket-api-route-keys-connect-disconnect.html

客户端应用程序通过发送 WebSocket 升级请求连接到 WebSocket API。如果请求成功，则在建立连接时会执行 $connect 路由。
在连接关闭后，会执行 $disconnect 路由。

API Gateway – WebSocket API – Routing
• Incoming JSON messages are routed to different backend
• If no routes => sent to $default
• You request a route selection expression to select the field on JSON to route from
• Sample expression: $request.body.action
• The result is evaluated against the route keys available in your API Gateway
• The route is then connected to the backend you’ve setup through API Gateway

---

Question #: 120
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer has written code for an application and wants to share it with other developers on the team to receive feedback. The shared application code needs to be stored long-term with multiple versions and batch change tracking.

Which AWS service should the developer use?

A. AWS CodeBuild
B. Amazon S3
C. AWS CodeCommit
D. AWS Cloud9

Suggested Answer: C

---

Question #: 121
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company's developer is building a static website to be deployed in Amazon S3 for a production environment. The website integrates with an Amazon Aurora PostgreSQL database by using an AWS Lambda function. The website that is deployed to production will use a Lambda alias that points to a specific version of the Lambda function.

The company must rotate the database credentials every 2 weeks. Lambda functions that the company deployed previously must be able to use the most recent credentials.

Which solution will meet these requirements?

A. Store the database credentials in AWS Secrets Manager. Turn on rotation. Write code in the Lambda function to retrieve the credentials from Secrets Manager.
B. Include the database credentials as part of the Lambda function code. Update the credentials periodically and deploy the new Lambda function.
C. Use Lambda environment variables. Update the environment variables when new credentials are available.
D. Store the database credentials in AWS Systems Manager Parameter Store. Turn on rotation. Write code in the Lambda function to retrieve the credentials from Systems Manager Parameter Store.

Suggested Answer: A 

---

Question #: 122
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is developing an application that uses signed requests (Signature Version 4) to call other AWS services. The developer has created a canonical request, has created the string to sign, and has calculated signing information.

Which methods could the developer use to complete a signed request? (Choose two.)

A. Add the signature to an HTTP header that is named Authorization.
B. Add the signature to a session cookie.
C. Add the signature to an HTTP header that is named Authentication.
D. Add the signature to a query string parameter that is named X-Amz-Signature.
E. Add the signature to an HTTP header that is named WWW-Authenticate.

Suggested Answer: AD

Signing AWS API requests
• When you call the AWS HTTP API, you sign the request so that AWS can identify you, using your AWS credentials (access key & secret key)
• Note: some requests to Amazon S3 don’t need to be signed
• If you use the SDK or CLI, the HTTP requests are signed for you
• You should sign an AWS HTTP request using Signature v4 (SigV4)

SigV4 Request examples

HTTP Header option (signature in Authorization header)

Query String option, ex: S3 pre-signed URLs (signature in X-Amz-Signature)

您可使用 HTTP Authorization 标头或查询字符串参数，将身份验证信息添加至请求。您无法同时使用 Authorization 标头和查询字符串参数来添加身份验证信息。

例 示例：授权标头
以下示例显示了 DescribeInstances 操作的 Authorization 标头。为便于阅读，此示例已使用换行符编排过格式。在您的代码中，这必须是连续的字符串。算法和 Credential 之间没有逗号。但是，必须使用逗号分隔其他元素。

```
Authorization: AWS4-HMAC-SHA256
Credential=AKIAIOSFODNN7EXAMPLE/20220830/us-east-1/ec2/aws4_request,
SignedHeaders=host;x-amz-date,
Signature=calculated-signature
```
例 示例：请求在查询字符串中使用身份验证参数
以下示例显示了对包含身份验证信息的 DescribeInstances 操作的查询。为便于阅读，此示例已使用换行符编排过格式，而非 URL 编码。在您的代码中，查询字符串必须是采用 URL 编码的连续字符串。

```
https://ec2.amazonaws.com/?
Action=DescribeInstances&
Version=2016-11-15&
X-Amz-Algorithm=AWS4-HMAC-SHA256&
X-Amz-Credential=AKIAIOSFODNN7EXAMPLE/20220830/us-east-1/ec2/aws4_request&
X-Amz-Date=20220830T123600Z&
X-Amz-SignedHeaders=host;x-amz-date&
X-Amz-Signature=calculated-signature
```

---

Question #: 123
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company must deploy all its Amazon RDS DB instances by using AWS CloudFormation templates as part of AWS CodePipeline continuous integration and continuous delivery (CI/CD) automation. The primary password for the DB instance must be automatically generated as part of the deployment process.

Which solution will meet these requirements with the LEAST development effort?

A. Create an AWS Lambda-backed CloudFormation custom resource. Write Lambda code that generates a secure string. Return the value of the secure string as a data field of the custom resource response object. Use the CloudFormation Fn::GetAtt intrinsic function to get the value of the secure string. Use the value to create the DB instance.
B. Use the AWS CodeBuild action of CodePipeline to generate a secure string by using the following AWS CLI command: aws secretsmanager get-random-password. Pass the generated secure string as a CloudFormation parameter with the NoEcho attribute set to true. Use the parameter reference to create the DB instance.
C. Create an AWS Lambda-backed CloudFormation custom resource. Write Lambda code that generates a secure string. Return the value of the secure string as a data field of the custom resource response object. Use the CloudFormation Fn::GetAtt intrinsic function to get a value of the secure string. Create secrets in AWS Secrets Manager. Use the secretsmanager dynamic reference to use the value stored in the secret to create the DB instance.
D. Use the AWS::SecretsManager::Secret resource to generate a secure string. Store the secure string as a secret in AWS Secrets Manager. Use the secretsmanager dynamic reference to use the value stored in the secret to create the DB instance.

Suggested Answer: D

https://docs.aws.amazon.com/zh_cn/AWSCloudFormation/latest/UserGuide/aws-resource-secretsmanager-secret.html

AWS::SecretsManager::Secret

Creates a new secret. A secret can be a password, a set of credentials such as a user name and password, an OAuth token, or other secret information that you store in an encrypted form in Secrets Manager.

B选项生成的密码没地方管理

---

Question #: 124
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
An organization is storing large files in Amazon S3, and is writing a web application to display meta-data about the files to end-users. Based on the metadata a user selects an object to download. The organization needs a mechanism to index the files and provide single-digit millisecond latency retrieval for the metadata.

What AWS service should be used to accomplish this?

A. Amazon DynamoDB
B. Amazon EC2
C. AWS Lambda
D. Amazon RDS

Suggested Answer: A

---

Question #: 125
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating an AWS Serverless Application Model (AWS SAM) template. The AWS SAM template contains the definition of multiple AWS Lambda functions, an Amazon S3 bucket, and an Amazon CloudFront distribution. One of the Lambda functions runs on Lambda@Edge in the CloudFront distribution. The S3 bucket is configured as an origin for the CloudFront distribution.

When the developer deploys the AWS SAM template in the eu-west-1 Region, the creation of the stack fails.

Which of the following could be the reason for this issue?

A. CloudFront distributions can be created only in the us-east-1 Region.
B. Lambda@Edge functions can be created only in the us-east-1 Region.
C. A single AWS SAM template cannot contain multiple Lambda functions.
D. The CloudFront distribution and the S3 bucket cannot be created in the same Region.

Suggested Answer: B

Lambda@Edge function 只能在 us-east-1

---

Question #: 126
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is integrating Amazon ElastiCache in an application. The cache will store data from a database. The cached data must populate real-time dashboards.

Which caching strategy will meet these requirements?

A. A read-through cache
B. A write-behind cache
C. A lazy-loading cache
D. A write-through cache

Suggested Answer: D 

---

Question #: 127
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is creating an AWS Lambda function. The Lambda function needs an external library to connect to a third-party solution. The external library is a collection of files with a total size of 100 MB. The developer needs to make the external library available to the Lambda execution environment and reduce the Lambda package space.

Which solution will meet these requirements with the LEAST operational overhead?

A. Create a Lambda layer to store the external library. Configure the Lambda function to use the layer.
B. Create an Amazon S3 bucket. Upload the external library into the S3 bucket. Mount the S3 bucket folder in the Lambda function. Import the library by using the proper folder in the mount point.
C. Load the external library to the Lambda function's /tmp directory during deployment of the Lambda package. Import the library from the /tmp directory.
D. Create an Amazon Elastic File System (Amazon EFS) volume. Upload the external library to the EFS volume. Mount the EFS volume in the Lambda function. Import the library by using the proper folder in the mount point.

Suggested Answer: A

---

Question #: 128
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company has a front-end application that runs on four Amazon EC2 instances behind an Elastic Load Balancer (ELB) in a production environment that is provisioned by AWS Elastic Beanstalk. A developer needs to deploy and test new application code while updating the Elastic Beanstalk platform from the current version to a newer version of Node.js. The solution must result in zero downtime for the application.

Which solution meets these requirements?

A. Clone the production environment to a different platform version. Deploy the new application code, and test it. Swap the environment URLs upon verification.
B. Deploy the new application code in an all-at-once deployment to the existing EC2 instances. Test the code. Redeploy the previous code if verification fails.
C. Perform an immutable update to deploy the new application code to new EC2 instances. Serve traffic to the new instances after they pass health checks.
D. Use a rolling deployment for the new application code. Apply the code to a subset of EC2 instances until the tests pass. Redeploy the previous code if the tests fail.

Suggested Answer: C

---

Question #: 129
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]

A developer is creating an AWS Lambda function. The Lambda function will consume messages from an Amazon Simple Queue Service (Amazon SQS) queue. The developer wants to integrate unit testing as part of the function's continuous integration and continuous delivery (CI/CD) process.

How can the developer unit test the function?

A. Create an AWS CloudFormation template that creates an SQS queue and deploys the Lambda function. Create a stack from the template during the CI/CD process. Invoke the deployed function. Verify the output.
B. Create an SQS event for tests. Use a test that consumes messages from the SQS queue during the function's Cl/CD process.
C. Create an SQS queue for tests. Use this SQS queue in the application's unit test. Run the unit tests during the CI/CD process.
D. Use the aws lambda invoke command with a test event during the CIICD process.

Suggested Answer: C

Unit testing is a type of testing that verifies the correctness of individual units of source code, typically functions or methods. When unit testing a Lambda function that interacts with Amazon SQS, you can create a separate test SQS queue that the Lambda function interacts with during testing. You would then validate the behavior of the function based on its interactions with the test queue. This approach isolates the function's behavior from the rest of the system, which is a key principle of unit testing.

Option A is incorrect because AWS CloudFormation is typically used for infrastructure deployment, not for unit testing.

Option B is incorrect because it does not actually test the function; it only creates an event.

Option D is incorrect because the 'aws lambda invoke' command is used to manually trigger a Lambda function, but doesn't necessarily facilitate testing the function's behavior when consuming messages from an SQS queue.
能自定义假事件来测试lambda的是sam local invoke 

---

Question #: 130
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A developer is working on a web application that uses Amazon DynamoDB as its data store. The application has two DynamoDB tables: one table that is named artists and one table that is named songs. The artists table has artistName as the partition key. The songs table has songName as the partition key and artistName as the sort key.

The table usage patterns include the retrieval of multiple songs and artists in a single database operation from the webpage. The developer needs a way to retrieve this information with minimal network traffic and optimal application performance.

Which solution will meet these requirements?

A. Perform a BatchGetltem operation that returns items from the two tables. Use the list of songName/artistName keys for the songs table and the list of artistName key for the artists table.
B. Create a local secondary index (LSI) on the songs table that uses artistName as the partition key. Perform a query operation for each artistName on the songs table that filters by the list of songName. Perform a query operation for each artistName on the artists table.
C. Perform a BatchGetitem operation on the songs table that uses the songName/artistName keys. Perform a BatchGetltem operation on the artists table that uses artistName as the key.
D. Perform a Scan operation on each table that filters by the list of songName/artistName for the songs table and the list of artistName in the artists table.

Suggested Answer: A 

---

Question #: 131
Topic #: 1
[All AWS Certified Developer - Associate DVA-C02 Questions]
A company is developing an ecommerce application that uses Amazon API Gateway APIs. The application uses AWS Lambda as a backend. The company needs to test the code in a dedicated, monitored test environment before the company releases the code to the production environment.

Which solution will meet these requirements?

A. Use a single stage in API Gateway. Create a Lambda function for each environment. Configure API clients to send a query parameter that indicates the environment and the specific Lambda function.
B. Use multiple stages in API Gateway. Create a single Lambda function for all environments. Add different code blocks for different environments in the Lambda function based on Lambda environment variables.
C. Use multiple stages in API Gateway. Create a Lambda function for each environment. Configure API Gateway stage variables to route traffic to the Lambda function in different environments.
D. Use a single stage in API Gateway. Configure API clients to send a query parameter that indicates the environment. Add different code blocks for different environments in the Lambda function to match the value of the query parameter.

Suggested Answer: C

---

Question #: 132
Topic #: 1
[All AWS Certified Developer Associate Questions]

How should custom libraries be utilized in AWS Lambda?
A. Host the library on Amazon S3 and reference to it from the Lambda function.
B. Install the library locally and upload a ZIP file of the Lambda function.
C. Import the necessary Lambda blueprint when creating the function.
D. Modify the function runtime to include the necessary library.

Suggested Answer: B

---

Question #: 133
Topic #: 1
[All AWS Certified Developer Associate Questions]

A developer is using an Amazon Kinesis Data Firehose delivery stream to store data in Amazon S3. Before storing the data in Amazon S3, the developer wants to enrich the data by combining the data with data from an Amazon DynamoDB table.
How can the developer implement the data enrichment?

A. Create a Kinesis Data Firehose data transformation by using an Amazon EC2 instance.
B. Configure the Kinesis Data Firehose delivery stream to send data to a Kinesis data stream. Enrich the data by using an AWS Lambda function.
C. Configure the Kinesis Data Firehose delivery stream to store data in the DynamoDB table. Export the table to Amazon S3.
D. Create a Kinesis Data Firehose data transformation by using an AWS Lambda function.

Suggested Answer: D

---

Question #: 134
Topic #: 1
[All AWS Certified Developer Associate Questions]

An AWS Lambda function generates a 3MB JSON file and then uploads it to an Amazon S3 bucket daily. The file contains sensitive information, so the Developer must ensure that it is encrypted before uploading to the bucket.
Which of the following modifications should the Developer make to ensure that the data is encrypted before uploading it to the bucket?

A. Use the default AWS KMS customer master key for S3 in the Lambda function code.
B. Use the S3 managed key and call the GenerateDataKey API to encrypt the file.
C. Use the GenerateDateKey API, then use that data key to encrypt the file in the Lambda function code.
D. Use a custom KMS customer master key created for S3 in the Lambda function code.

Suggested Answer: C

---

Question #: 135
Topic #: 1
[All AWS Certified Developer Associate Questions]

A Developer wants to find a list of items in a global secondary index from an Amazon DynamoDB table.
Which DynamoDB API call can the Developer use in order to consume the LEAST number of read capacity units?

A. Scan operation using eventually-consistent reads
B. Query operation using strongly-consistent reads
C. Query operation using eventually-consistent reads
D. Scan operation using strongly-consistent reads

Suggested Answer: C

---

Question #: 136
Topic #: 1
[All AWS Certified Developer Associate Questions]

A Developer has published an update to an application that is served to a global user base using Amazon CloudFront. After deploying the application, users are not able to see the updated changes.
How can the Developer resolve this issue?

A. Remove the origin from the CloudFront configuration and add it again.
B. Disable forwarding of query strings and request headers from the CloudFront distribution configuration.
C. Invalidate all the application objects from the edge caches.
D. Disable the CloudFront distribution and enable it again to update all the edge locations.

Suggested Answer: C


If you need to remove a file from CloudFront edge caches before it expires, you can do one of the following:

Invalidate the file from edge caches. The next time a viewer requests the file, CloudFront returns to the origin to fetch the latest version of the file.

Use file versioning to serve a different version of the file that has a different name. For more information, see Updating existing files using versioned file names.

To invalidate files, you can specify either the path for individual files or a path that ends with the * wildcard, which might apply to one file or to many, as shown in the following examples:

/images/image1.jpg

/images/image*

/images/*

CloudFront Caching
• The cache lives at each CloudFront Edge Location
• CloudFront identifies each object in the cache using the Cache Key (see next slide)
• You want to maximize the Cache Hit ratio to minimize requests to the origin
• You can invalidate part of the cache using the CreateInvalidation API

What is CloudFront Cache Key?
• A unique identifier for every object in the cache
• By default, consists of hostname + resource portion of the URL
• If you have an application that serves up content that varies based on user, device, language, location…
• You can add other elements (HTTP headers, cookies, query strings) to the Cache Key using CloudFront Cache Policies

CloudFront – Cache Invalidations
• In case you update the back-end origin, CloudFront doesn’t know about it and will only get the refreshed content after the TTL has expired
• However, you can force an entire or partial cache refresh (thus bypassing the TTL) by performing a CloudFront Invalidation
• You can invalidate all files * or a special path (/images/*)
