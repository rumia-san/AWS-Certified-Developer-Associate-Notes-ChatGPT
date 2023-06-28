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



