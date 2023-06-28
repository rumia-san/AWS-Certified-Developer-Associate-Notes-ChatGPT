Question #1

A gaming website gives users the ability to trade game items with each other on the platform. The platform requires both users' records to be updated and persisted in one transaction. If any update fails, the transaction must roll back.
Which AWS solution can provide the transactional capability that is required for this feature?

A. Amazon DynamoDB with operations made with the Consistent Read parameter set to true
B. Amazon ElastiCache for Memcached with operations made within a transaction block
C. Amazon DynamoDB with reads and writes made by using Transact* operations
D. Amazon Aurora MySQL with operations made within a transaction block
E. Amazon Athena with operations made within a transaction block

Correct Answer: C 不确定

---

Question #2

A developer has created a Java application that makes HTTP requests directly to AWS services. Application logging shows 5xx HTTP response codes that occur at irregular intervals. The errors are affecting users.
How should the developer update the application to improve the application's resiliency?
A. Revise the request content in the application code.
B. Use the AWS SDK for Java to interact with AWS APIs.
C. Scale out the application so that more instances of the application are running.
D. Add additional logging to the application code.

Correct Answer: B

All AWS SDKs have a built-in retry mechanism with an algorithm that uses exponential backoff. This algorithm implements increasingly longer wait times between retries for consecutive error responses.

---

Question #3

A global company has a mobile app with static data stored in an Amazon S3 bucket in the us-east-1 Region. The company serves the content through an Amazon
CloudFront distribution. The company is launching the mobile app in South Africa. The data must reside in the af-south-1 Region. The company does not want to deploy a specific mobile client for South Africa.
What should the company do to meet these requirements?

A. Use the CloudFront geographic restriction feature to block access to users in South Africa.
B. Create a Lambda@Edge function. Associate the Lambda@Edge function as an origin request trigger with the CloudFront distribution to change the S3 origin Region.
C. Create a Lambda@Edge function. Associate the Lambda@Edge function as a viewer response trigger with the CloudFront distribution to change the S3 origin Region.
D. Include af-south-1 in the alternate domain name (CNAME) of the CloudFront distribution.

Correct Answer: B

Lambda@Edge – Lambda@Edge 是 AWS Lambda 的扩展，可为复杂的函数提供强大而灵活的计算，并带来更接近您的查看器的完整应用程序逻辑，并且具有高度安全性。Lambda@Edge 函数在 Node.js 或 Python 运行时环境中运行。您将函数发布到单个 AWS 区域，当您关联该函数与 CloudFront 分配时，Lambda@Edge 可自动将您的代码复制到世界上任何地点。

 Used to change CloudFront requests and responses:
• Viewer Request – after CloudFront receives a request from a 
viewer
• Origin Request – before CloudFront forwards the request to the 
origin
• Origin Response – after CloudFront receives the response from the 
origin
• Viewer Response – before CloudFront forwards the response to 
the viewer

---

Question #4

A developer is testing an AWS Lambda function by using the AWS Serverless Application Model (AWS SAM) local CLI. The application that is implemented by the
Lambda function makes several AWS API calls by using the AWS software development kit (SDK). The developer wants to allow the function to make AWS API calls in a test AWS account from the developer's laptop.
What should the developer do to meet these requirements?
A. Edit the template.yml file. Add the AWS_ACCESS_KEY_ID property and the AWS_SECRET_ACCESS_KEY property in the Globals section.
B. Add a test profile by using the aws configure command with the --profile option. Run AWS SAM by using the sam local invoke command with the -profile option.
C. Edit the template.yml tile. For the AWS::Serverless::Function resource, set the role to an IAM role in the AWS account.
D. Run the function by using the sam local invoke command. Override the AWS_ACCESS_KEY_ID parameter and the AWS_SECRET_ACCESS_KEY parameter by specifying the --parameter-overrides option.

Correct Answer: B

---

Question #5

A developer designed an application on an Amazon EC2 instance. The application makes API requests to objects in an Amazon S3 bucket.
Which combination of steps will ensure that the application makes the API requests in the MOST secure manner? (Choose two.)
A. Create an IAM user that has permissions to the S3 bucket. Add the user to an IAM group.
B. Create an IAM role that has permissions to the S3 bucket.
C. Add the IAM role to an instance profile. Attach the instance profile to the EC2 instance.
D. Create an IAM role that has permissions to the S3 bucket. Assign the role to an 1AM group.
E. Store the credentials of the IAM user in the environment variables on the EC2 instance.

Correct Answer: BC 

---

Question #6

A developer is configuring an Amazon CloudFront distribution for a new application to provide encryption in transit. The application is running in the eu-west-1
Region. The developer creates a new certificate in AWS Certificate Manager (ACM) in eu-west-1, but the certificate is not visible in the CloudFront distribution settings.
What should the developer do to fix this problem?
A. Create the certificate for the domain in the same Region as the application. Ensure that the alternate domain name (CNAME) in the distribution settings matches the domain name in the certificate.
B. Create the certificate in the eu-west-1 Region. Ensure that the alternate domain name (CNAME) in the distribution settings matches the domain name in the certificate.
C. Recreate the CloudFront distribution in the same Region as the certificate.
D. Specify the ACM certificate name as the default root object of the CloudFront distribution.

Correct Answer: B 

这题打错字了，B选项是us-west-1

---

Question #7

A developer is building an application that runs behind an Application Load Balancer (ALB). The ALB is configured as the origin for an Amazon CloudFront distribution. Users will log in to the application by using their social media accounts.
How can the developer authenticate users?
A. Validate the users by inspecting the tokens in an AWS Lambda authorizer on the ALB.
B. Configure the ALB to use Amazon Cognito as one of the authentication providers.
C. Configure CloudFront to use Amazon Cognito as one of the authentication providers.
D. Validate the users by calling the Amazon Cognito API in an AWS Lambda authorizer on the ALB.

Correct Answer: B

Lambda Authorizer (formerly Custom Authorizers)是API GateWay的东西，自己实现一个lambda Authorizer，来和第三方验证tokens集成
ALB有个identity providers


---

Question #8

A company has an application that analyzes photographs. A developer is preparing the application for deployment to Amazon EC2 instances. The application's image analysis functions require a mix of GPU instances and CPU instances that run on Amazon Linux. The developer needs to add code to the application so that the functions can determine whether they are running on a GPU instance.
What should the functions do to obtain this information?
A. Call the DescribeInstances API operation and filter on the current instance ID. Examine the ElasticGpuAssociations property.
B. Evaluate the GPU AVAILABLE environment variable.
C. Call the DescribeElasticGpus API operation.
D. Retrieve the instance type from the instance metadata.

Correct Answer: D

http://169.254.169.254/latest/meta-data/

---

Question #9

A company has an application that uses Amazon Cognito user pools as an identity provider. The company must secure access to user records. The company has set up multi-factor authentication (MFA). The company also wants to send a login activity notification by email every time a user logs in.
What is the MOST operationally efficient solution that meets this requirement?
A. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Add an Amazon API Gateway API to invoke the function. Call the API from the client side when login confirmation is received.
B. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Add an Amazon Cognito post authentication Lambda trigger for the function.
C. Create an AWS Lambda function that uses Amazon Simple Email Service (Amazon SES) to send the email notification. Create an Amazon CloudWatch Logs log subscription filter to invoke the function based on the login status.
D. Configure Amazon Cognito to stream all logs to Amazon Kinesis Data Firehose. Create an AWS Lambda function to process the streamed logs and to send the email notification based on the login status of each user.

Correct Answer: B 

CUP can invoke a Lambda function synchronously on these triggers

---

Question #10

A company hosts a three-tier web application on AWS behind an Amazon CloudFront distribution. A developer wants a dashboard to monitor error rates and anomalies of the CloudFront distribution with the shortest possible refresh interval.
Which combination of slops should the developer take to meet these requirements? (Choose two.)
A. Activate real-time logs on the CloudFront distribution. Create a stream in Amazon Kinesis Data Streams.
B. Export the CloudFront logs to an Amazon S3 bucket. Detect anomalies and error rates with Amazon QuickSight.
C. Configure Amazon Kinesis Data Streams to deliver logs to Amazon OpenSearch Service (Amazon Elasticsearch Service). Create a dashboard in OpenSearch Dashboards (Kibana).
D. Create Amazon CloudWatch alarms based on expected values of selected CloudWatch metrics to detect anomalies and errors.
E. Design an Amazon CloudWatch dashboard of the selected CloudFront distribution metrics.

Correct Answer: AC 

It mentions shortest possible refresh interval so best to use the real-time logs

---

Question #11

A developer creates a customer managed key for multiple AWS users to encrypt data in Amazon S3. The developer configures Amazon Simple Notification
Service (Amazon SNS) to publish a message if key deletion is scheduled. The developer needs to preserve any SNS messages that cannot be delivered so that those messages can be reprocessed.
Which AWS service or feature should the developer use to meet this requirement?
A. Amazon Simple Email Service (Amazon SES)
B. AWS Lambda
C. Amazon Simple Queue Service (Amazon SQS)
D. Amazon CloudWatch alarm

Correct Answer: C

---

Question #12

A developer needs to deploy an application to AWS Elastic Beanstalk for a company. The application consists of a single Docker image. The company's automated continuous integration and continuous delivery (CI/CD) process builds the Docker image and pushes the image to a public Docker registry.
How should the developer deploy the application to Elastic Beanstalk?

A. Create a Dockerfile. Configure Elastic Beanstalk to build the application as a Docker image.
B. Create a docker-compose.yml file. Use the Elastic Beanstalk CLI to deploy the application.
C. Create a .zip file that contains the Docker image. Upload the .zip file to Elastic Beanstalk.
D. Create a Dockerfile. Run the Elastic Beanstalk CLI eb local run command in the same directory.

Correct Answer: B

不确定

---

Question #13

A company is using AWS CodeDeploy for all production deployments. A developer has an Amazon Elastic Container Service (Amazon ECS) application that uses the CodeDeployDefault.ECSAIIAtOnce configuration. The developer needs to update the production environment in increments of 10% until the entire production environment is updated.
Which CodeDeploy configuration should the developer use to meet these requirements?
A. CodeDeployDefault.ECSCanary10Percent5Minutes
B. CodeDeployDefault.ECSLinear10PercentEvery3Minutes
C. CodeDeployDefault.OneAtATime
D. CodeDeployDefault.LambdaCanary10Percent5Minutes

Correct Answer: B 

---

Question #14

A company is using AWS Elastic Beanstalk to deploy a three-tier application. The application uses an Amazon RDS DB instance as the database tier. The company wants to decouple the DB instance from the Elastic Beanstalk environment.
Which combination of steps should a developer lake to meet this requirement? (Choose two.)

A. Create a new Elastic Beanstalk environment that connects to the DB instance.
B. Create a new DB instance from a snapshot of the previous DB instance.
C. Use the Elastic Beanstalk CLI to decouple the DB instance.
D. Use the AWS CLI to decouple the DB instance.
E. Modify the current Elastic Beanstalk environment to connect to the DB instance.

Correct Answer: AB  不确定
https://aws.amazon.com/premiumsupport/knowledge-center/decouple-rds-from-beanstalk/

在不影响环境运行状况的前提下，按照以下步骤从 Elastic Beanstalk 环境解耦您的数据库：

    创建 Amazon RDS 数据库快照。
    防止您的 RDS 数据数据库实例被删除。
    创建新 Elastic Beanstalk 环境。
    执行蓝绿部署。
    更新 beanstalk 环境 A 的数据库删除策略。
    从 beanstalk 环境 A 解耦 RDS 实例。
    终止旧 Elastic Beanstalk 环境。


---

Question #15

A company has point-of-sale devices across thousands of retail shops that synchronize sales transactions with a centralized system. The system includes an
Amazon API Gateway API that exposes an AWS Lambda function. The Lambda function processes the transactions and stores the transactions in Amazon RDS for MySQL. The number of transactions increases rapidly during the day and is near zero at night.
How can a developer increase the elasticity of the system MOST cost-effectively?

A. Migrate from Amazon RDS to Amazon Aurora MySQL. Use an Aurora Auto Scaling policy to scale road replicas based on CPU consumption.
B. Migrate from Amazon RDS to Amazon Aurora MySQL. Use an Aurora Auto Scaling policy to scale read replicas based on the number of database connections.
C. Create an Amazon Simple Queue Service (Amazon SQS) queue. Publish transactions to the queue. Set the queue to invoke the Lambda function. Turn on enhanced fanout for the Lambda function.
D. Create an Amazon Simple Queue Service (Amazon SQS) queue. Publish transactions to the queue. Set the queue to invoke the Lambda function. Set the reserved concurrency of the Lambda function to be less than the number of database connections.

Correct Answer: D

A and B are for read problem, nor for write.
C its not possible because enhanced fanout its for kinesis
D is the most probably


---


Question #16

A developer is writing an AWS Lambda function. The Lambda function needs to access items that are stored in an Amazon DynamoDB table.
What is the MOST secure way to configure this access for the Lambda function?

A. Create an IAM user that has permissions to access the DynamoDB table. Create an access key for this user. Store the access key ID and secret access key in the Lambda function environment variables.
B. Add a resource-based policy to the DynamoDB table to allow access from the Lambda function's IAM role.
C. Create an IAM policy that allows access to the DynamoDB table. Attach this policy to the Lambda function's IAM role.
D. Create a DynamoDB Accelerator (DAX) cluster. Configure the Lambda function to use the DAX duster to access the DynamoDB table.

Correct Answer: C 

Amazon DynamoDB **不支持resource-based policy**

---

Question #17

A developer is implementing user authentication and authorization for a web application that is hosted on an Amazon EC2 instance. The developer needs to ensure that the user credentials are encrypted and secure when they are stored and transmitted.
Which solution will meet these requirements?

A. Activate web server modules for authentication and authorization on the instance. Use HTTP basic authentication for the user login.
B. Deploy a custom authentication and authorization API over HTTP. Store the user credentials on Amazon ElastiCache for Redis.
C. Use Amazon Cognito to configure a user pool. Use the Amazon Cognito API to authenticate and authorize the users.
D. Create IAM users. Assign the users to different IAM groups. Use AWS Single Sign-On to authenticate and authorize each user.

Correct Answer: C

---

Question #18

A company that has multiple offices uses an Amazon DynamoDB table to store employee payroll information. Item attributes consist of employee names, office identifiers, and cumulative daily hours worked The most frequently used query extracts a report of an alphabetical subset of employees for a specific office.
Which design of the DynamoDB table primary key will have the MINIMUM performance impact?

A. Partition key on the office identifier and sort key on the employee name
B. Partition key on the employee name and sort key on the office identifier
C. Partition key on the employee name
D. Partition key on the office identifier

Correct Answer: A

不确定

---

Question #19

A company hosts a microservices application that uses Amazon API Gateway. AWS Lambda, Amazon Simple Queue Service (Amazon SQS), and Amazon
DynamoDB. One of the Lambda functions adds messages to an SQS FIFO queue.
When a developer checks the application logs, the developer finds a few duplicated items in a DynamoDB table. The items were inserted by another polling function that processes messages from the queue.
What is the MOST likely cause of this issue?

A. Write operations on the DynamoDB table are being throttled.
B. The SQS queue delivered the message to the function more than once.
C. API Gateway duplicated the message in the SQS queue.
D. The polling function timeout is greater than the queue visibility timeout.

Correct Answer: D

---

Question #20

A development team has been using a builder server that is hosted on an Amazon EC2 instance to perform builds and deployments for the last 3 months. The
EC2 instance's instance profile uses an IAM role that contains the Administrator Access managed policy. The development team must replace that policy with a policy that provides only the required permissions.
What is the FASTEST way to create a custom 1AM policy for the EC2 instance to meet this requirement?

A. Create a new IAM policy based on services that the build server deployed or updated in the last 3 months.
B. Create a new IAM policy that includes all actions that AWS CloudTrail recorded for the IAM role in the last 3 months.
C. Create a new permissions boundary policy that denies all access. Associate the permissions boundaries with the IAM role.
D. Create a new IAM policy by using Amazon Athena to query an Amazon S3 bucket that contains AWS CloudTrail events that the IAM role performed in the last 3 months.

Correct Answer: B

"As an administrator or developer, you might grant permissions to IAM entities (users or roles) beyond what they require. IAM provides several options to help you refine the permissions that you grant. One option is to generate an IAM policy that is based on access activity for an entity. IAM Access Analyzer reviews your AWS CloudTrail logs and generates a policy template that contains the permissions that the entity used in your specified date range. You can use the template to create a policy with fine-grained permissions that grant only the permissions that are required to support your specific use case."

https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_generate-policy.html

---

Question #21

A developer needs to write an AWS CloudFormation template on a local machine and deploy a CloudFormation stack to AWS.
What must the developer do to complete these tasks?

A. Install the AWS CLI. Configure the AWS CLI by using an IAM user name and password.
B. Install the AWS CLI. Configure the AWS CLI by using an SSH key.
C. Install the AWS CLI. Configure the AWS CLI by using an IAM user access key and secret key.
D. Install an AWS software development kit (SDK). Configure the SDK by using an X.509 certificate.

Correct Answer: C

---

Question #22

A developer is working on a web application that runs on Amazon Elastic Container Service (Amazon ECS) and uses an Amazon DynamoDB table to store data.
The application performs a large number of read requests against a small set of the table data.
How can the developer improve the performance of these requests? (Choose two.)

A. Create an Amazon ElastiCache cluster. Configure the application to cache data in the cluster.
B. Create a DynamoDB Accelerator (DAX) cluster. Configure the application to use the DAX cluster for DynamoDB requests.
C. Configure the application to make strongly consistent read requests against the DynamoDB table.
D. Increase the read capacity of the DynamoDB table.
E. Enable DynamoDB adaptive capacity.

Correct Answer: AB 或者 BD 不确定


DynamoDB本身不直接支持使用ElastiCache来缓存数据。
然而，您可以在应用程序层面使用ElastiCache来缓存从DynamoDB中检索的数据。这需要您在应用程序中编写逻辑，将从DynamoDB获取的数据存储到ElastiCache中，并在需要时首先检查缓存以获取数据，而不是直接从DynamoDB读取。这样可以减少对DynamoDB的请求次数，提高读取性能和降低成本。

---

Question #23

A developer needs to use Amazon DynamoDB to store customer orders. The developer's company requires all customer data to be encrypted at rest with a key that the company generates.
What should the developer do to meet these requirements?
A. Create the DynamoDB table with encryption set to None. Code the application to use the key to decrypt the data when the application reads from the table. Code the application to use the key to encrypt the data when the application writes to the table.
B. Store the key by using AWS Key Management Service (AWS KMS). Choose an AWS KMS customer managed key during creation of the DynamoDB table. Provide the Amazon Resource Name (ARN) of the AWS KMS key.
C. Store the key by using AWS Key Management Service (AWS KMS). Create the DynamoDB table with default encryption. Include the kms:Encrypt parameter with the Amazon Resource Name (ARN) of the AWS KMS key when using the DynamoDB software development kit (SDK).
D. Store the key by using AWS Key Management Service (AWS KMS). Choose an AWS KMS AWS managed key during creation of the DynamoDB table. Provide the Amazon Resource Name (ARN) of the AWS KMS key.

Correct Answer: B

https://aws.amazon.com/blogs/database/bring-your-own-encryption-keys-to-amazon-dynamodb/

---

Question #24

A developer is creating a solution to track an account's Amazon S3 buckets over time. The developer has created an AWS Lambda function that will run on a schedule. The function will list the account's S3 buckets and will store the list in an Amazon DynamoDB table. The developer receives a permissions error when the developer runs the function with the AWSLambdaBasicExecutionRole AWS managed policy.
Which combination of permissions should the developer use to resolve this error? (Choose two.)

A. Cross-account IAM role
B. Permission for the Lambda function to list buckets in Amazon S3
C. Permission for the Lambda function to write in DynamoDB
D. Permission for Amazon S3 to invoke the Lambda function
E. Permission for DynamoDB to invoke the Lambda function

Correct Answer: BC

---

Question #25

A company is adding items to an Amazon DynamoDB table from an AWS Lambda function that is written in Python. A developer needs to implement a solution that inserts records in the DynamoDB table and performs automatic retry when the insert fails.
Which solution meets these requirements with MINIMUM code changes?

A. Configure the Python code to run the AWS CLI through shell to call the PutItem operation
B. Call the PutItem operation from Python by using the DynamoDB HTTP API
C. Queue the items in AWS Glue, which will put them into the DynamoDB table
D. Use the AWS software development kit (SDK) for Python (boto3) to call the PutItem operation

Correct Answer: D 

---

Question #26

A developer is writing an AWS Lambda function. The developer wants to log key events that occur during the Lambda function and include a unique identifier to associate the events with a specific function invocation.
Which of the following will help the developer accomplish this objective?
A. Obtain the request identifier from the Lambda context object. Architect the application to write logs to the console.
B. Obtain the request identifier from the Lambda event object. Architect the application to write logs to a file.
C. Obtain the request identifier from the Lambda event object. Architect the application to write logs to the console.
D. Obtain the request identifier from the Lambda context object. Architect the application to write logs to a file.

Correct Answer: A 

---

Question #27

A company experienced partial downtime during the last deployment of a new application. AWS Elastic Beanstalk split the environment's Amazon EC2 instances into batches and deployed a new version one batch at a time after taking them out of service. Therefore, full capacity was not maintained during deployment.
The developer plans to release a new version of the application, and is looking for a policy that will maintain full capacity and minimize the impact of the failed deployment.

Which deployment policy should the developer use?
A. Immutable
B. All at Once
C. Rolling
D. Rolling with an Additional Batch

Correct Answer: A 

这题没有提到成本，所以最厉害的是A

The answer is the A given that we must have full capacity and we have to minimize the impact of failed deployment. With immutable we can prepare the new environment and switch when it is ready. If there is some issue it is always possible to switch back to the previuos version.

---

Question #28

A company is providing services to many downstream consumers. Each consumer may connect to one or more services. This has resulted in a complex architecture that is difficult to manage and does not scale well. The company needs a single interface to manage these services to consumers.
Which AWS service should be used to refactor this architecture?

A. AWS Lambda
B. AWS X-Ray
C. Amazon SQS
D. Amazon API Gateway

Correct Answer: D

---


Question #29

When a Developer tries to run an AWS CodeBuild project, it raises an error because the length of all environment variables exceeds the limit for the combined maximum of characters.
What is the recommended solution?

A. Add the export LC_ALL=ג€en_US.utf8ג€ command to the pre_build section to ensure POSIX localization.
B. Use Amazon Cognito to store key-value pairs for large numbers of environment variables.
C. Update the settings for the build project to use an Amazon S3 bucket for large numbers of environment variables.
D. Use AWS Systems Manager Parameter Store to store large numbers of environment variables.

Correct Answer: D

---

Question #30

A Development team decides to adopt a continuous integration/continuous delivery (CI/CD) process using AWS CodePipeline and AWS CodeCommit for a new application. However, management wants a person to review and approve the code before it is deployed to production.
How can the Development team add a manual approver to the CI/CD pipeline?

A. Use AWS SES to send an email to approvers when their action is required. Develop a simple application that allows approvers to accept or reject a build. Invoke an AWS Lambda function to advance the pipeline when a build is accepted.
B. If approved, add an approved tag when pushing changes to the CodeCommit repository. CodePipeline will proceed to build and deploy approved commits without interruption.
C. Add an approval step to CodeCommit. Commits will not be saved until approved.
D. Add an approval action to the pipeline. Configure the approval action to publish to an Amazon SNS topic when approval is required. The pipeline execution will stop and wait for an approval.

Correct Answer: D 

https://docs.aws.amazon.com/codepipeline/latest/userguide/approvals-action-add.html

---

Question #31

A Developer is migrating an on-premises application to AWS. The application currently takes user uploads and saves them to a local directory on the server. All uploads must be saved and made immediately available to all instances in an Auto Scaling group.
Which approach will meet these requirements?

A. Use Amazon EBS and configure the application AMI to use a snapshot of the same EBS instance on boot.
B. Use Amazon S3 and rearchitect the application so all uploads are placed in S3.
C. Use instance storage and share it between instances launched from the same Amazon Machine Image (AMI).
D. Use Amazon EBS and file synchronization software to achieve eventual consistency among the Auto Scaling group.

Correct Answer: B

Of course B is obvious. But why are others wrong?
A - need to reboot instance? -> out
C - instance storage cannot shared between instances
D - only achieve eventual consistency while the requirement is "immediately available"

---

Question #32


A developer is creating a script to automate the deployment process for a serverless application. The developer wants to use an existing AWS Serverless
Application Model (AWS SAM) template for the application.
What should the developer use for the project? (Choose two.)
A. Call aws cloudformation package to create the deployment package. Call aws cloudformation deploy to deploy the package afterward.
B. Call sam package to create the deployment package. Call sam deploy to deploy the package afterward.
C. Call aws s3 cp to upload the AWS SAM template to Amazon S3. Call aws lambda update-function-code to create the application.
D. Create a ZIP package locally and call aws serverlessrepo create-application to create the application.
E. Create a ZIP package and upload it to Amazon S3. Call aws cloudformation create-stack to create the application.

Correct Answer: AB

AWS SAM
• Transform Header indicates it’s SAM template: 
• Transform: 'AWS::Serverless-2016-10-31'
• Write Code 
• AWS::Serverless::Function 
• AWS::Serverless::Api 
• AWS::Serverless::SimpleTable 
• Package & Deploy: 
• aws cloudformation package / sam package 
• aws cloudformation deploy / sam deplo

---

Question #33

A developer has built a market application that stores pricing data in Amazon DynamoDB with Amazon ElastiCache in front. The prices of items in the market change frequently. Sellers have begun complaining that, after they update the price of an item, the price does not actually change in the product listing.
What could be causing this issue?
A. The cache is not being invalidated when the price of the item is changed
B. The price of the item is being retrieved using a write-through ElastiCache cluster
C. The DynamoDB table was provisioned with insufficient read capacity
D. The DynamoDB table was provisioned with insufficient write capacity

Correct Answer: A 

---

Question #34

The developer is creating a web application that collects highly regulated and confidential user data through a POST request. The web application is served through Amazon CloudFront. User names and phone numbers must be encrypted at the edge and must remain encrypted throughout the entire application stack.
What is the MOST secure way to meet these requirements?

A. Enforce Match Viewer with HTTPS Only on CloudFront.
B. Use only the newest TLS security policy on CloudFront.
C. Enforce a signed URL on CloudFront on the front end.
D. Use field-level encryption on CloudFront.

Correct Answer: D 

Field-level encryption adds an additional layer of security along with HTTPS that lets you protect specific data throughout system processing so that only certain applications can see it. By configuring field-level encryption in CloudFront, you can securely upload user-submitted sensitive information to your web servers. The sensitive information provided by your clients is encrypted at the edge closer to the user. It remains encrypted throughout your entire application stack, ensuring that only applications that need the data—and have the credentials to decrypt it—are able to do so.

字段级加密增加了一个额外的安全保护层以及 HTTPS，使您可以在整个系统处理过程中保护特定的数据，以便只有某些应用程序才能查看它。通过在 CloudFront 中配置字段级加密，您可以将用户提交的敏感信息安全上传到您的 Web 服务器。客户端提供的敏感信息在更接近用户的边缘站点中进行加密。这些敏感信息在整个应用程序堆栈中保持加密状态，从而确保仅需要该数据（以及具有用于解密的凭证）的应用程序才能使用该数据。

---

Question #35

A Developer has been asked to create an AWS Lambda function that is triggered any time updates are made to items in an Amazon DynamoDB table. The function has been created, and appropriate permissions have been added to the Lambda execution role. Amazon DynamoDB streams have been enabled for the table, but the function is still not being triggered.
Which option would enable DynamoDB table updates to trigger the Lambda function?

A. Change the StreamViewType parameter value to NEW_AND_OLD_IMAGES for the DynamoDB table
B. Configure event source mapping for the Lambda function
C. Map an Amazon SNS topic to the DynamoDB streams
D. Increase the maximum execution time (timeout) setting of the Lambda function
 
Correct Answer: B

Event Source Mapping（事件源映射）是AWS Lambda 中的一个概念，它用于将事件源与 Lambda 函数进行关联。事件源可以是 AWS 的各种服务，如 Amazon S3、Amazon DynamoDB、Amazon Kinesis 等，以及自定义的事件源。

通过创建事件源映射，您可以配置 Lambda 函数在事件发生时自动触发执行。事件源将生成事件通知，这些通知将被传递给 Lambda 函数进行处理。Lambda 函数可以根据事件的内容和上下文执行相应的操作。

---

Question #36

A company maintains a REST service using Amazon API Gateway and the API Gateway native API key validation. The company recently launched a new registration page, which allows users to sign up for the service. The registration page creates a new API key using CreateApiKey and sends the new key to the user. When the user attempts to call the API using this key, the user receives a 403 Forbidden error. Existing users are unaffected and can still call the API.
What code updates will grant these new users access to the API?

A. The createDeployment method must be called so the API can be redeployed to include the newly created API key.
B. The updateAuthorizer method must be called to update the API's authorizer to include the newly created API key.
C. The importApiKeys method must be called to import all newly created API keys into the current stage of the API.
D. The createUsagePlanKey method must be called to associate the newly created API key with the correct usage plan.

Correct Answer: D

---

Question #37

An application uploads photos to an Amazon S3 bucket. Each photo that is uploaded to the S3 bucket must be resized to a thumbnail image by the application.
Each thumbnail image is uploaded with a new name in the same S3 bucket.
Which AWS service can a developer configure to directly process each single S3 event for each S3 object upload?

A. Amazon EC2
B. Amazon Elastic Container Service (Amazon ECS)
C. AWS Elastic Beanstalk
D. AWS Lambda

Correct Answer: D

---

Question #38

A company is running a Docker application on Amazon ECS. The application must scale based on user load in the last 15 seconds.
How should a Developer instrument the code so that the requirement can be met?
A. Create a high-resolution custom Amazon CloudWatch metric for user activity data, then publish data every 30 seconds
B. Create a high-resolution custom Amazon CloudWatch metric for user activity data, then publish data every 5 seconds
C. Create a standard-resolution custom Amazon CloudWatch metric for user activity data, then publish data every 30 seconds
D. Create a standard-resolution custom Amazon CloudWatch metric for user activity data, then publish data every 5 seconds

Correct Answer: B

---

Question #39

Where should the appspec.yml file be placed in order for AWS CodeDeploy to work?
A. In the root of the application source code directory structure
B. In the bin folder along with all the complied code
C. In an S3 bucket
D. In the same folder as the application configuration files

Correct Answer: A 

---

Question #40

A Developer is working on an application that handles 10MB documents that contain highly-sensitive data. The application will use AWS KMS to perform client-side encryption.
What steps must be followed?

A. Invoke the Encrypt API passing the plaintext data that must be encrypted, then reference the customer managed key ARN in the KeyId parameter
B. Invoke the GenerateRandom API to get a data encryption key, then use the data encryption key to encrypt the data
C. Invoke the GenerateDataKey API to retrieve the encrypted version of the data encryption key to encrypt the data
D. Invoke the GenerateDataKey API to retrieve the plaintext version of the data encryption key to encrypt the data

Correct Answer: D

**For the exam: anything over 4 KB of data that needs to be encrypted must use the Envelope Encryption == GenerateDataKey API**

---

Question #41

An application uses Amazon Kinesis Data Streams to ingest and process large streams of data records in real time. Amazon EC2 instances consume and process the data from the shards of the Kinesis data stream by using Amazon Kinesis Client Library (KCL). The application handles the failure scenarios and does not require standby workers. The application reports that a specific shard is receiving more data than expected. To adapt to the changes in the rate of data flow, the
`hot` shard is resharded.
Assuming that the initial number of shards in the Kinesis data stream is 4, and after resharding the number of shards increased to 6, what is the maximum number of EC2 instances that can be deployed to process data from all the shards?
A. 12
B. 6
C. 4
D. 1

Correct Answer: B

Typically, when you use the KCL, you should ensure that the number of instances does not exceed the number of shards (except for failure standby purposes). Each shard is processed by exactly one KCL worker and has exactly one corresponding record processor, so you never need multiple instances to process one shard. However, one worker can process any number of shards, so it's fine if the number of shards exceeds the number of instances.
https://docs.aws.amazon.com/streams/latest/dev/kinesis-record-processor-scaling.html

---

Question #42

A Company runs continuous integration/continuous delivery (CI/CD) pipelines for its application on AWS CodePipeline. A Developer must write unit tests and run them as part of the pipelines before staging the artifacts for testing.
How should the Developer incorporate unit tests as part of CI/CD pipelines?

A. Create a separate CodePipeline pipeline to run unit tests
B. Update the AWS CodeBuild specification to include a phase for running unit tests
C. Install the AWS CodeDeploy agent on an Amazon EC2 instance to run unit tests
D. Create a testing branch in AWS CodeCommit to run unit tests

Correct Answer: B

---

Question #43

A Developer has written an application that runs on Amazon EC2 instances and generates a value every minute. The Developer wants to monitor and graph the values generated over time without logging in to the instance each time.
Which approach should the Developer use to achieve this goal?

A. Use the Amazon CloudWatch metrics reported by default for all EC2 instances. View each value from the CloudWatch console.
B. Develop the application to store each value in a file on Amazon S3 every minute with the timestamp as the name.
C. Publish each generated value as a custom metric to Amazon CloudWatch using available AWS SDKs.
D. Store each value as a variable and add the variable to the list of EC2 metrics that should be reported to the Amazon CloudWatch console.

Correct Answer: C

---

Question #44

A developer is trying to get data from an Amazon DynamoDB table called demoman-table. The developer configured the AWS CLI to use a specific IAM user's credentials and executed the following command:
`aws dynamodb get-item --table-name damoman-table --key '{"id": { "N": "1993"}}'
`

The command returned errors and no rows were returned.
What is the MOST likely cause of these issues?

A. The command is incorrect; it should be rewritten to use put-item with a string argument.
B. The developer needs to log a ticket with AWS Support to enable access to the demoman-table.
C. Amazon DynamoDB cannot be accessed from the AWS CLI and needs to be called via the REST API.
D. The IAM user needs an associated policy with read access to demoman-table.

Correct Answer: D

---

Question #45

A Development team is working on a case management solution that allows medical claims to be processed and reviewed. Users log in to provide information related to their medical and financial situations.
As part of the application, sensitive documents such as medical records, medical imaging, bank statements, and receipts are uploaded to Amazon S3. All documents must be securely transmitted and stored. All access to the documents must be recorded for auditing.
What is the MOST secure approach?

A. Use S3 default encryption using Advanced Encryption Standard-256 (AES-256) on the destination bucket.
B. Use Amazon Cognito for authorization and authentication to ensure the security of the application and documents.
C. Use AWS Lambda to encrypt and decrypt objects as they are placed into the S3 bucket.
D. Use client-side encryption/decryption with Amazon S3 and AWS KMS.

Correct Answer: D

D. is Correct.
Use client-side encryption/decryption with Amazon S3 and AWS KMS.
Keywords: Auditing is required, AWS KMS has auditing capability.
and has to be Client Side Encryption for securely transmitting.

---

Question #46

A developer is planning to use an Amazon API Gateway and AWS Lambda to provide a REST API. The developer will have three distinct environments to manage: development, test, and production.
How should the application be deployed while minimizing the number of resources to manage?

A. Create a separate API Gateway and separate Lambda function for each environment in the same Region.
B. Assign a Region for each environment and deploy API Gateway and Lambda to each Region.
C. Create one API Gateway with multiple stages with one Lambda function with multiple aliases.
D. Create one API Gateway and one Lambda function, and use a REST parameter to identify the environment.

Correct Answer: C 

---

Question #47

An application needs to use the IP address of the client in its processing. The application has been moved into AWS and has been placed behind an Application
Load Balancer (ALB). However, all the client IP addresses now appear to be the same. The application must maintain the ability to scale horizontally.
Based on this scenario, what is the MOST cost-effective solution to this problem?

A. Remove the application from the ALB. Delete the ALB and change Amazon Route 53 to direct traffic to the instance running the application.
B. Remove the application from the ALB. Create a Classic Load Balancer in its place. Direct traffic to the application using the HTTP protocol.
C. Alter the application code to inspect the X-Forwarded-For header. Ensure that the code can work properly if a list of IP addresses is passed in the header.
D. Alter the application code to inspect a custom header. Alter the client code to pass the IP address in the custom header.

Correct Answer: C 

---

Question #48

A developer tested an application locally and then deployed it to AWS Lambda. While testing the application remotely, the Lambda function fails with an access denied message.
How can this issue be addressed?

A. Update the Lambda function's execution role to include the missing permissions.
B. Update the Lambda function's resource policy to include the missing permissions.
C. Include an IAM policy document at the root of the deployment package and redeploy the Lambda function.
D. Redeploy the Lambda function using an account with access to the AdministratorAccess policy.

Correct Answer: A

---

Question #49

A Developer must analyze performance issues with production-distributed applications written as AWS Lambda functions. These distributed Lambda applications invoke other components that make up the applications.
How should the Developer identify and troubleshoot the root cause of the performance issues in production?

A. Add logging statements to the Lambda functions, then use Amazon CloudWatch to view the logs.
B. Use AWS CloudTrail and then examine the logs.
C. Use AWS X-Ray, then examine the segments and errors.
D. Run Amazon Inspector agents and then analyze performance.

Correct Answer: C

---

Question #50

A company is building a compute-intensive application that will run on a fleet of Amazon EC2 instances. The application uses attached Amazon EBS disks for storing data. The application will process sensitive information and all the data must be encrypted.
What should a Developer do to ensure the data is encrypted on disk without impacting performance?

A. Configure the Amazon EC2 instance fleet to use encrypted EBS volumes for storing data.
B. Add logic to write all data to an encrypted Amazon S3 bucket.
C. Add a custom encryption algorithm to the application that will encrypt and decrypt all data.
D. Create a new Amazon Machine Image (AMI) with an encrypted root volume and store the data to ephemeral disks.

Correct Answer: A

---

Question #51

A Developer is working on a serverless project based in Java. Initial testing shows a cold start takes about 8 seconds on average for AWS Lambda functions.
What should the Developer do to reduce the cold start time? (Choose two.)

A. Add the Spring Framework to the project and enable dependency injection.
B. Reduce the deployment package by including only needed modules from the AWS SDK for Java.
C. Increase the memory allocation setting for the Lambda function.
D. Increase the timeout setting for the Lambda function.
E. Change the Lambda invocation mode from synchronous to asynchronous.

Correct Answer: BC

---

Question #52

A company runs an e-commerce website that uses Amazon DynamoDB where pricing for items is dynamically updated in real time. At any given time, multiple updates may occur simultaneously for pricing information on a particular product. This is causing the original editor's changes to be overwritten without a proper review process.
Which DynamoDB write option should be selected to prevent this overwriting?

A. Concurrent writes
B. Conditional writes
C. Atomic writes
D. Batch writes

Correct Answer: B 

Conditional Writes
• Accept a write/update/delete only if conditions are met, otherwise returns an error
• Helps with concurrent access to items 
• No performance impact

---

Question #53

A developer is storing JSON files in an Amazon S3 bucket. The developer wants to securely share an object with a specific group of people.
How can the developer securely provide temporary access to the objects that are stored in the S3 bucket?

A. Set object retention on the files. Use the AWS software development kit (SDK) to restore the object before subsequent requests. Provide the bucket's S3 URL.
B. Use the AWS software development kit (SDK) to generate a presigned URL. Provide the presigned URL.
C. Set a bucket policy that restricts access after a period of time. Provide the bucket's S3 URL.
D. Configure static web hosting on the S3 bucket. Provide the bucket's web URL.

Correct Answer: B

---

Question #54

A front-end web application is using Amazon Cognito user pools to handle the user authentication flow. A developer is integrating Amazon DynamoDB into the application using the AWS SDK for JavaScript.
How would the developer securely call the API without exposing the access or secret keys?

A. Configure Amazon Cognito identity pools and exchange the JSON Web Token (JWT) for temporary credentials.
B. Run the web application in an Amazon EC2 instance with the instance profile configured.
C. Hardcore the credentials, use Amazon S3 to host the web application, and enable server-side encryption.
D. Use Amazon Cognito user pool JSON Web Tokens (JWITs) to access the DynamoDB APIs.

Correct Answer: A

---

Question #55

A Developer must build an application that uses Amazon DynamoDB. The requirements state that the items being stored in the DynamoDB table will be 7KB in size and that reads must be strongly consistent. The maximum read rate is 3 items per second, and the maximum write rate is 10 items per second.
How should the Developer size the DynamoDB table to meet these requirements?
A. Read: 3 read capacity units Write: 70 write capacity units
B. Read: 6 read capacity units Write: 70 write capacity units
C. Read: 6 read capacity units Write: 10 write capacity units
D. Read: 3 read capacity units Write: 10 write capacity units

Correct Answer: B

• One Write Capacity Unit (WCU) represents one write per second for an item up to 1 KB in size
• If the items are larger than 1 KB, more WCUs are consumed

• One Read Capacity Unit (RCU) represents one Strongly Consistent Read per second, or two Eventually Consistent Reads per second, for an item up to 4 KB in size
• If the items are larger than 4 KB, more RCUs are consumed

---

Question #56

A company needs to ingest terabytes of data each hour from thousands of sources that are delivered almost continually throughout the day. The volume of messages generated varies over the course of the day. Messages must be delivered in real time for fraud detection and live operational dashboards.
Which approach will meet these requirements?

A. Send the messages to an Amazon SQS queue, then process the messages by using a fleet of Amazon EC2 instances
B. Use the Amazon S3 API to write messages to an S3 bucket, then process the messages by using Amazon Redshift
C. Use AWS Data Pipeline to automate the movement and transformation of data
D. Use Amazon Kinesis Data Streams with Kinesis Client Library to ingest and deliver messages

Correct Answer: D 

Kinesis Client Library (KCL)
• A Java library that helps read record from a Kinesis Data Stream with distributed applications sharing the read workload
• Each shard is to be read by only one KCL instance

---

Question #57

A developer is debugging an AWS Lambda function behind an Amazon API Gateway. Whenever the API Gateway endpoint is called, HTTP status code 200 is returned even though AWS Lambda is recording a 4xx error.
What change needs to be made to return a proper error code through the API Gateway?

A. Enable CORS in the API Gateway method settings
B. Use a Lambda proxy integration to return HTTP codes and headers
C. Enable API Gateway error pass-through.
D. Return the value in the header x-Amzn-ErrorType.

Correct Answer: B

• Integration Type AWS_PROXY (Lambda Proxy):
• incoming request from the client is the input to Lambda
• The function is responsible for the logic of request / response 
• No mapping template, headers, query string parameters… are passed as arguments

---

Question #58

For a deployment using AWS CodeDeploy, what is the run order of the hooks for in-place deployments?

A. Before Install -> Application Stop -> Application Start -> After Install
B. Application Stop -> Before Install -> After Install -> Application Start
C. Before Install -> Application Stop -> Validate Service -> Application Start
D. Application Stop -> Before Install -> Validate Service -> Application Start

Correct Answer: B

---

Question #59

A developer is using Amazon S3 as the event source that invokes a Lambda function when new objects are created in the bucket. The event source mapping information is stored in the bucket notification configuration. The developer is working with different versions of the Lambda function, and has a constant need to update notification configuration so that Amazon S3 invokes the correct version.
What is the MOST efficient and effective way to achieve mapping between the S3 event and Lambda?

A. Use a different Lambda trigger.
B. Use Lambda environment variables.
C. Use a Lambda alias.
D. Use Lambda tags.

Correct Answer: C

---

Question #60

A company has a multi-tier application that uses Amazon API Gateway, AWS Lambda, and Amazon RDS. The company wants to investigate a slow response time to calls that come from the API Gateway API.
What is the MOST operationally efficient way for the company to determine which internal call is causing the slow response times?

A. Use Amazon CloudWatch.
B. Use AWS X-Ray.
C. Use AWS CloudTrail.
D. Use VPC Flow Logs.

Correct Answer: B 

---


