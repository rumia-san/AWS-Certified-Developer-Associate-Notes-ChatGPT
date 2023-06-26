# IAM

IAM users can't create CloudFront key pairs. You must log in using root credentials to create key pairs.

# SAM

SAM 侧重serverless，要放到EC2上的话，Beanstalk会好一些

# Load Balancer
A Load Balancer can target EC2 instances only within an AWS Region.

# Beanstalk

rolling deployments: 如果在一批或多批实例成功完成后部署失败，则已完成的批次将运行新版本的应用程序，而待处理的批次则会继续运行旧版本