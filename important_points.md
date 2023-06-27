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