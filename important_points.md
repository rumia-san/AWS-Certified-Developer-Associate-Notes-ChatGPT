# IAM

IAM users can't create CloudFront key pairs. You must log in using root credentials to create key pairs.

Which is the only resource-based policy that the IAM service supports? **Trust policy**

By default, IAM users do not have access to the AWS Billing and Cost Management console. You or your account administrator must grant users access. You can do this by activating IAM user access to the Billing and Cost Management console and attaching an IAM policy to your users. Then, you need to activate IAM user access for IAM policies to take effect. You only need to activate IAM user access once.

# SAM

SAM 侧重serverless，要放到EC2上的话，Beanstalk会好一些

# Load Balancer
A Load Balancer can target EC2 instances only within an AWS Region.

# Beanstalk

rolling deployments: 如果在一批或多批实例成功完成后部署失败，则已完成的批次将运行新版本的应用程序，而待处理的批次则会继续运行旧版本

# Elasticache

Elasticache for Memcached **cannot be used with API Gateway** to improve the responsiveness of the API for the given use case. You should note that Elasticache for Memcached is a downstream service in the request flow.

# CodeBuild

CloudWatch **cannot** be used to impact the code build process.

# DynamoDB

DynamoDB is a better fit than RDS MySQL to handle **massive traffic spikes for write requests.** DynamoDB is a key-value and document database that supports tables of virtually any size with **horizontal scaling**. DynamoDB scales to more than 10 trillion requests per day and with tables that have more than ten million read and write requests per second and petabytes of data storage. DynamoDB can be used to build applications that need consistent single-digit millisecond performance. **MySQL RDS can be scaled vertically**, however, it cannot match the performance benefits offered by DynamoDB for the given use case.

# CloudFormation

`!FindInMap [ MapName, TopLevelKey, SecondLevelKey ]`

```yaml
Mappings:
  RegionMap:
    us-east-1:
      HVM64: "ami-0ff8a91507f77f867"
      HVMG2: "ami-0a584ac55a7631c0c"
    us-west-1:
      HVM64: "ami-0bdb828fd58c52235"
      HVMG2: "ami-066ee5fd4a9ef77f1"
    eu-west-1:
      HVM64: "ami-047bb4163c506cd98"
      HVMG2: "ami-31c2f645"
    ap-southeast-1:
      HVM64: "ami-08569b978cc4dfa10"
      HVMG2: "ami-0be9df32ae9f92309"
    ap-northeast-1:
      HVM64: "ami-06cd52961ce9f0d85"
      HVMG2: "ami-053cdd503598e4a9d"
Resources:
  myEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: !FindInMap
        - RegionMap
        - !Ref 'AWS::Region'
        - HVM64
      InstanceType: m1.small
```

AWS CloudFormation StackSets 通过让您在单个操作中 **跨多个账户和 AWS 区域** 创建、更新或删除堆栈来扩展堆栈的功能。

# Security group

Security groups are stateful, so allowing inbound traffic to the necessary ports enables the connection. Network ACLs are stateless, so you must allow both inbound and outbound traffic.

# codecommit的git登录
https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/id_credentials_ssh-keys.html

# 在AWS账户之间发送和接收亚马逊EventBridge事件
跨账户传event
https://docs.aws.amazon.com/zh_cn/eventbridge/latest/userguide/eb-cross-account.html

# At-least-once 交付

Amazon SQS 将消息的副本存储在多台服务器上，从而实现冗余和高可用性。在极少数情况下，当您接收或删除消息时，存储消息副本的某台服务器可能不可用。

如果出现这种情况，则该不可用服务器上的消息副本将不会被删除，并且您在接收消息时可能会再次获得该消息副本。将应用程序设计为幂等 应用程序 (多次处理同一消息时，它们不应受到不利影响)。

# exactly once 确切一次处理

与标准队列不同，FIFO 队列不会引入重复的消息。FIFO 队列可帮助您避免向队列发送重复的内容。如果您在 5 分钟的重复数据删除间隔内重试该SendMessage操作，Amazon SQS 不会在队列中引入任何重复项。

要配置重复数据删除，必须执行以下操作之一：

    启用基于内容的重复数据删除。这指示 Amazon SQS 使用 SHA-256 哈希通过消息的正文（而不是消息的属性）生成消息的重复数据删除 ID。有关更多信息，请参阅《亚马逊简单队列服务 API 参考》中关于GetQueueAttributes、和SetQueueAttributes操作的文档。CreateQueue

    为消息显式提供消息重复数据删除 ID (或查看序列号)。有关更多信息，请参阅《亚马逊简单队列服务 API 参考》中关于SendMessageBatch、和ReceiveMessage操作的文档。SendMessage

• Two de-duplication methods:
• Content-based deduplication: will do a SHA-256 hash of the message body
• Explicitly provide a Message Deduplication ID 