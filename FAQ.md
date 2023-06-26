
---

# Cross Stack Reference 跨stack引用

在 AWS CloudFormation 中，Cross Stack Reference 是一种技术，用于在不同的 CloudFormation 堆栈之间引用资源。它允许你在一个堆栈中创建的资源与另一个堆栈中的资源建立关联。

以下是实现 Cross Stack Reference 的步骤：

创建源堆栈：在一个 CloudFormation 模板中定义并创建源堆栈，其中包含需要被引用的资源。确保给这些资源分配了适当的导出名称。

导出资源：在源堆栈中，使用 Export 函数将需要引用的资源导出。导出时，为每个资源指定一个导出名称。

```yaml
Outputs:
  MyResourceOutput:
    Value: !Ref MyResource
    Export:
      Name: MyExportedResource
```

创建目标堆栈：在另一个 CloudFormation 模板中定义并创建目标堆栈。在目标堆栈中，可以使用 Fn::ImportValue 函数来引用源堆栈中导出的资源。

```yaml
Resources:
  MyOtherResource:
    Type: AWS::EC2::Instance
    Properties:
      ...
      AnotherResource: !ImportValue MyExportedResource
```

通过上述步骤，你可以在目标堆栈中引用源堆栈中导出的资源。这种跨堆栈引用的方式可以帮助你在不同的堆栈之间建立关联，实现更复杂的架构和资源组合。

---

# ALB HTTP请求头

ALB（Application Load Balancer）在 HTTP 请求中提供了一系列的标准和自定义的请求头。以下是 ALB 常见的一些 HTTP 请求头：

Host：指示客户端请求的目标主机名。

X-Forwarded-For：包含客户端的原始 IP 地址和透明代理的 IP 地址列表，用逗号分隔。

X-Forwarded-Port：指示客户端请求的原始端口号。

X-Forwarded-Proto：指示客户端请求的原始协议（HTTP 或 HTTPS）。

X-Forwarded-Host：包含客户端请求的原始主机名。

X-Amzn-Trace-Id：AWS X-Ray 服务使用的追踪 ID。

X-SSL-Cert：如果使用 SSL/TLS 终端到终端加密，此请求头包含 SSL 证书信息。

X-Real-IP：如果使用代理服务器，此请求头包含客户端的真实 IP 地址。

上述列表仅列举了一些常见的请求头，ALB 还支持其他自定义请求头。对于每个请求头的具体用途和使用方式，可以参考 AWS 文档中关于 ALB 的详细说明。

---

# Auto Scaling Groups – Dynamic Scaling Policies
## Target Tracking Scaling
• Most simple and easy to set-up
• Example: I want the average ASG CPU to stay at around 40%
## Simple / Step Scaling
• When a CloudWatch alarm is triggered (example CPU > 70%), then add 2 units
• When a CloudWatch alarm is triggered (example CPU < 30%), then remove 1
## Scheduled Actions
• Anticipate a scaling based on known usage patterns
• Example: increase the min capacity to 10 at 5 pm on Friday
---

CloudTrail、CloudWatch Logs 加密

对于 AWS 服务中的日志和事件数据，默认情况下，CloudTrail、CloudWatch Logs 和 CloudWatch Events 都支持加密来保护数据的安全性。下面是它们的默认加密方式：

CloudTrail：CloudTrail 默认情况下会将日志数据以加密方式存储在 S3 存储桶中。具体来说，CloudTrail 使用服务器端加密 (SSE) 来保护存储在 S3 中的日志文件。SSE 使用 S3 管理的加密密钥 (SSE-S3) 或 AWS Key Management Service (KMS) 托管的密钥 (SSE-KMS) 来加密数据。您可以根据需要选择 SSE-S3 或 SSE-KMS 来进行加密。

CloudWatch Logs：CloudWatch Logs 默认情况下支持数据加密。当您创建 CloudWatch Logs 日志**组**时，您可以选择启用加密选项。加密可以使用 AWS 托管的密钥 (SSE-KMS) 进行，以保护存储在 CloudWatch Logs 中的日志数据。

CloudWatch Events：CloudWatch Events 并不直接存储数据，而是用于路由和处理事件数据。然而，与 CloudWatch Logs 集成时，如果您将事件数据发送到 CloudWatch Logs，那么 CloudWatch Logs 的加密机制将适用。您可以启用 CloudWatch Logs 的加密选项，保护存储在 CloudWatch Logs 中的事件数据。

需要注意的是，默认加密是为了提供一定级别的数据安全性，但您仍然可以根据需要进一步定制和加强数据的加密和安全控制。根据实际需求，您可以选择使用其他的加密选项，如客户端加密 (CSE) 或其他加密服务来加密和保护数据。


---

当然，以下是一些常见的 AWS 服务的数据大小限制的示例：

Amazon S3:

对象大小限制: 单个对象最大为 5TB。
Multipart Upload: 每个分段最小为 5MB，除最后一个分段外，每个分段最大为 5GB。
元数据和标签大小限制: 对象元数据最大为 2KB，标签最大为 10KB。
Amazon SQS:

消息大小限制: 单个消息最大为 256KB。
消息保留时间: 默认保留时间为 4 天，最长保留时间为 14 天。
Amazon DynamoDB:

项目大小限制: 单个项目最大为 400KB。
表格大小限制: 单个表格总共所有项目大小之和最大为 10GB。
AWS Lambda:

部署包大小限制: 压缩文件最大为 50MB (对于直接上传的方式) 或 250MB (对于在 S3 存储桶中引用的方式)。
单个请求/响应体大小限制: 请求体最大为 6MB，响应体最大为 6MB。
Amazon RDS:

数据库实例大小限制: 具体限制取决于所选的数据库引擎和实例类型。可以参考 AWS 文档了解每个数据库引擎的具体限制。
需要注意的是，上述限制仅为常见示例，并不涵盖所有 AWS 服务的限制。每个服务都有自己特定的限制，请在相关服务的官方文档中查找特定的限制和约束。此外，AWS 还提供一些手段来处理超过限制的数据，如使用分段上传等技术来处理大型对象。


---

# 以下是一些后台依赖于 AWS CloudFormation 来提供资源的 AWS 服务：

AWS Elastic Beanstalk：提供了一个快速部署和扩展应用程序的平台，使用 CloudFormation 在后台进行资源的创建和配置。

AWS Amplify：用于构建移动和 Web 应用程序的开发平台，也使用 CloudFormation 来创建和管理底层资源。

AWS AppSync：用于构建可扩展的后端数据图 API 的服务，使用 CloudFormation 进行资源创建和配置。

AWS Serverless Application Model (SAM)：是一种扩展 AWS CloudFormation 的框架，用于构建和部署无服务器应用程序。

AWS Cloud9：是一种云端集成开发环境 (IDE)，在后台使用 CloudFormation 来创建和配置所需的资源。

AWS Service Catalog：允许组织内的开发人员访问经批准的 AWS 服务，它使用 CloudFormation 来创建和管理服务目录中的产品。

这些服务在后台使用 AWS CloudFormation 来实现资源的自动化创建和配置，简化了部署和管理的过程。通过 CloudFormation，您可以以声明性的方式定义资源和其属性，并通过模板进行版本控制和重复使用。

---

# SSL Termination

ALB (Application Load Balancer) 的 SSL Termination 是指 ALB 在接收到加密的 SSL/TLS 请求后，将其解密并终止 SSL/TLS 连接，然后将解密后的请求转发到后端目标实例。

具体而言，当客户端发送加密的 SSL/TLS 请求到 ALB 时，ALB 会对请求进行解密，并检查其内容。ALB 可以使用自己的 SSL/TLS 证书与客户端建立安全的连接，也可以将客户端的 SSL/TLS 请求转发到后端实例，然后由后端实例使用自己的 SSL/TLS 证书与客户端建立连接。

ALB SSL Termination 提供了以下优势：

减轻后端实例的计算负载：由于 SSL/TLS 解密是一项计算密集型操作，ALB 可以代替后端实例执行解密操作，从而减轻后端实例的负载。
集中管理 SSL/TLS 证书：ALB 可以集中管理多个目标实例的 SSL/TLS 证书，简化证书管理和更新过程。
支持多个后端实例：ALB 可以将解密后的请求转发给多个后端实例，以实现负载均衡和高可用性。
通过 ALB SSL Termination，可以实现更好的性能、可伸缩性和安全性，同时简化了 SSL/TLS 证书管理过程。

---

# ALB Listener

在 Amazon Elastic Load Balancer (ALB) 中，Listener 是用于接收和路由传入请求的组件。Listener 监听特定的协议和端口，并将传入请求路由到适当的目标组（Target Group）。

每个 ALB 可以配置多个 Listener，每个 Listener 都定义了以下内容：

协议（Protocol）：监听的协议类型，例如 HTTP、HTTPS、TCP 等。
端口（Port）：监听的端口号。
默认目标组（Default Target Group）：未匹配任何规则时请求将路由到的默认目标组。
规则（Rules）：定义请求的路由规则，根据请求的特定条件将其路由到不同的目标组。
Listener 使用请求的协议和端口信息来确定将请求路由到哪个目标组。例如，可以设置一个 Listener 监听 HTTPS 端口 443，并根据请求的路径或域名将请求路由到相应的目标组。

通过 Listener，可以灵活地配置 ALB 的路由行为，将传入请求精确地路由到不同的目标组，以实现负载均衡、流量管理和应用程序的高可用性。

---

# SQS visibility timeout是什么

SQS（Simple Queue Service）中的 Visibility Timeout 是一个与消息可见性相关的设置。当消费者从队列中接收消息时，消息将在可见性超时期间保持可见状态。在此期间，其他消费者无法看到该消息并进行处理。

可见性超时是一种保护机制，用于确保消息不会被多个消费者同时处理。当一个消费者接收到消息时，可见性超时会启动，将消息标记为“不可见”。在可见性超时期间，该消息仍然在队列中，但对其他消费者不可见。

在可见性超时期间，消费者有足够的时间来处理消息，然后删除消息或延长消息的可见性超时时间。如果消费者在可见性超时期间未能处理消息或未删除消息，那么该消息将再次变为可见状态，供其他消费者处理。

可见性超时的设置可以根据应用程序的需求进行调整。较短的可见性超时时间可以更快地将消息重新分配给其他可用的消费者，以实现更快的处理速度和更高的吞吐量。较长的可见性超时时间可以提供更长的处理时间，适用于处理较长时间任务或处理较慢的消费者。

需要注意的是，如果消费者在消息处理期间发生故障或崩溃，消息可能会在可见性超时后重新分配给其他消费者，导致消息重复处理的情况。因此，在设计应用程序时，需要考虑幂等性和消息重复处理的情况，以确保数据的一致性和正确性。

---

# SQS delay second是什么

SQS（Simple Queue Service）中的 Delay Seconds 是一种消息延迟发送的机制。当你发送一条消息到队列时，可以设置一个延迟时间，该时间表示消息在被消费者可见之前的延迟秒数。

延迟秒数可以用来实现一些场景，例如：

定时任务：你可以将消息发送到队列，并设置延迟秒数，以便在一定时间后才可被消费者接收。这样可以实现定时触发的功能，例如定时发送通知或执行特定的任务。

消息重试：在某些情况下，如果消息发送失败或消费者无法处理消息，你可以使用延迟秒数来实现消息的延迟重试。通过设置延迟时间，让消息在一定时间后重新发送给消费者，以便进行重试处理。

延迟秒数的取值范围是从0秒到最大延迟时间。最大延迟时间取决于队列的最大延迟设置，最大可以设置为15分钟（900秒）。

需要注意的是，延迟秒数只适用于消息发送时设置的延迟，而不是消息在队列中的等待时间。消息在队列中的等待时间取决于队列的负载和消费者的处理速度。延迟秒数只影响消息在被消费者可见之前的延迟时间。

---

# SQS Long Polling是什么

SQS（Simple Queue Service）中的 Long Polling 是一种轮询消息的机制，用于接收队列中的消息。相比于传统的短轮询（Short Polling）方式，Long Polling 可以有效减少空闲的请求，提高消息获取的效率。

在短轮询中，客户端发送请求到 SQS 队列并立即收到响应，无论队列中是否有可用的消息。如果队列为空，客户端会立即收到空响应，需要重新发起请求。这种方式会导致频繁的请求和响应，增加了无效的网络流量。

而 Long Polling 则通过设置等待时间来减少无效请求。当客户端发起 Long Polling 请求时，如果队列中没有可用的消息，服务端会将请求保持打开，直到有消息到达队列或者超时。如果有消息到达队列，服务端会立即响应并返回消息给客户端。如果超时时间内没有消息到达，服务端会返回空响应。这样可以减少请求的频率，只在有消息到达时才返回响应，减少了网络开销和不必要的请求。

使用 Long Polling 可以实现实时或近实时的消息接收，并降低了对于空队列的频繁轮询。长轮询的超时时间可以根据具体需求进行配置，一般建议设置合理的超时时间，以兼顾实时性和资源利用率。

需要注意的是，Long Polling 不适用于所有场景。如果应用需要立即响应并处理消息，而不希望等待超时时间，那么短轮询可能更适合。但对于大多数场景，Long Polling 是一种更有效和经济的消息获取方式。

---

# ecs.config是什么

ecs.config 是一个配置文件，用于配置 Amazon Elastic Container Service (ECS) 代理（Amazon ECS Agent）。Amazon ECS Agent 是在 Amazon EC2 实例上运行的代理程序，用于管理容器和与 ECS 服务进行通信。

ecs.config 文件用于指定 ECS 代理的配置选项。它是一个文本文件，可以包含多个配置项和对应的值。通过编辑 ecs.config 文件，您可以自定义 ECS 代理的行为和设置。

一些常见的在 ecs.config 文件中配置的选项包括：

ECS_CLUSTER: 指定 ECS 集群的名称。
ECS_LOGFILE: 指定 ECS 代理的日志文件路径。
ECS_ENGINE_AUTH_TYPE: 指定 ECS 代理与容器注册表进行身份验证的类型，如 "docker" 或 "ecr"。
ECS_ENGINE_AUTH_DATA: 指定身份验证所需的凭据信息，如访问容器注册表的凭据。
通过编辑 ecs.config 文件，您可以根据特定的需求对 ECS 代理进行配置，并自定义其行为和功能。注意，在编辑 ecs.config 文件后，您需要重新启动 ECS 代理才能使新的配置生效。

请注意，ecs.config 文件只适用于 Amazon ECS Agent 版本 1.27.0 或更高版本。在较旧的代理版本中，可能需要使用其他方式进行配置。建议参考官方文档或相关文档以获取最新的配置和使用方式。

## ecs.config路径是什么

ecs.config 文件的路径取决于操作系统和代理的安装位置。以下是一些常见操作系统下 ecs.config 文件的默认路径：

Amazon Linux 2: /etc/ecs/ecs.config
Amazon Linux: /etc/ecs/ecs.config
Ubuntu: /etc/ecs/ecs.config
CentOS: /etc/ecs/ecs.config
Windows Server: C:\ProgramData\Amazon\ECS\ecs.config
请注意，这些路径是默认路径，实际路径可能因操作系统版本、代理安装方式或自定义配置而有所不同。如果在特定的环境中找不到 ecs.config 文件，请检查代理的安装位置或参考相关文档以获取正确的路径。

此外，您也可以通过自定义环境变量 ECS_AGENT_CONFIG_FILE 来指定 ecs.config 文件的位置。通过设置该环境变量，您可以将 ecs.config 文件放置在其他位置，并告知 ECS 代理使用该文件进行配置。

---

# RCU WCU

读取容量单位

一个读取容量单位表示对高达 4KB 大小的项目每秒执行一次强一致性读取，或每秒执行两次最终一致性读取。

例如，假设您创建一个带 10 个预置读取容量单位的表。对于最大 4KB 的项目，允许您每秒执行 10 次强一致性读取，或者每秒 20 次最终一致性读取。

读取大于 4KB 的项目时，将使用更多读取容量单位。例如，对 8 KB (4KB × 2) 的项目的强一致性读取占用 2 个读取容量单位。对同一项目执行最终一致性读取时，将仅使用 1 个读取容量单位。

对于读取操作，项目大小会向上取整为 4KB 的倍数。例如，读取一个 3500 字节的项目将使用的吞吐量与读取一个 4KB 项目相同。

## 读取的容量单位消耗

下面介绍 DynamoDB 读取操作如何占用读取容量单位：

    GetItem—从表中读取单个项目。要确定 GetItem 将使用的容量单位的数量，请使用项目大小并将其向上取整到下一个 4KB 界限值。如果指定了强一致性读取，则这是所需的容量单位数。对于最终一致性读取（默认值），请将此数字除以 2。

    例如，如果您读取一个 3.5 KB 的项目，DynamoDB 会将项目大小向上取整到 4KB。如果您读取一个 10 KB 的项目，DynamoDB 会将项目大小向上取整到 12 KB。

    BatchGetItem—从一个或多个表中读取多达 100 个项目。DynamoDB 将批次中的每个项目作为单个 GetItem 请求进行处理，因此 DynamoDB 会先将每个项目的大小向上取整到下一个 4KB 界限值，然后再计算总大小。计算得到的结果未必与所有项目大小的总和相同。例如，如果 BatchGetItem 读取一个 1.5 KB 的项目和一个 6.5 KB 的项目，则 DynamoDB 计算得出的大小为 12 KB (4KB + 8 KB)，而不是 8 KB (1.5 KB + 6.5 KB)。

    Query-读取具有相同分区键值的多个项目。返回的所有项目将视为一个读取操作，此时 DynamoDB 会计算所有项目的总大小，然后向上取整到下一个 4KB 界限值。例如，假设查询返回 10 个项目，其组合大小为 40.8 KB。DynamoDB 将操作的项目大小舍入为 44KB。如果查询返回了 1500 个项目，每个项目大小为 64 个字节，则累计大小为 96 KB。

    Scan-读取表中的所有项。DynamoDB 所考量的是评估所得的项目大小，而不是扫描返回项目的大小。

如果对不存在的项目执行读取操作，DynamoDB 仍会占用预置读取吞吐量：强一致性读取请求占用一个读取容量单位，而最终一致性读取请求占用 0.5 个读取容量单位。

对于返回项目的任意操作，您可以请求检索属性的子集。不过，这样做对项目大小计算没有影响。另外，Query 和 Scan 返回的是项目数而不是属性值。获取项目计数使用相同数量的读取容量单位，并且需要执行相同的项目大小计算。这是因为 DynamoDB 必须读取每个项目才能增加计数。

## 读取操作和读取一致性

前面的计算都假设提交的是强一致性读取请求。对于最终一致性读取请求，操作仅占用一半的容量单位。对于最终一致性读取，如果项目总大小为 80 KB，则操作仅占用 10 个容量单位。

## 写入容量单位

一个写入容量单位表示对大小最多为 1 KB 的项目每秒执行一次写入。

例如，假设您创建一个带 10 个写入容量单位的表。这允许对于最大 1 KB 的项目，每秒执行 10 次写入操作。

对于写入操作，项目大小会向上取整为 1 KB 的倍数。例如，写入一个 500 字节的项目使用的吞吐量与写入一个 1 KB 项目相同。
## 写入的容量单位消耗

下面介绍 DynamoDB 写入操作如何占用写入容量单位：

    PutItem—将单个项目写入表中。如果该表中存在具有相同主键的项目，此操作会替换该项目。在计算预置的吞吐量占用时，起作用的项目是二者中较大的那个。

    UpdateItem-修改表中的单个项目。DynamoDB 将考虑项目在更新前后显示的大小。消耗的预置吞吐量反映这些项目大小中较大的数据。即使您只更新项目属性的子集，UpdateItem 仍会占用全部的预置吞吐量 (“之前”和“之后”项目大小中的较大者)。

    DeleteItem—从表中删除单个项目。预置吞吐量占用情况取决于已删除的项目大小。

    BatchWriteItem-向一个或多个表写入最多 25 个项目。DynamoDB 将批处理中的每个项目作为单独的 PutItem 或者 DeleteItem 请求（不支持更新）。因此，DynamoDB 会首先将每个项目的大小向上取整到下一个 1 KB 界限值，然后再计算总大小。计算得到的结果未必与所有项目大小的总和相同。例如，如果 BatchWriteItem 写入一个 500 字节的项目和一个 3.5 KB 的项目，则 DynamoDB 计算得出的大小为 5 KB (1 KB + 4KB)，而不是 4KB（500 字节 + 3.5 KB）。

适用于PutItem、UpdateItem, 和 DeleteItem 操作时，DynamoDB 会将项目大小四舍五入到下一个 1 KB。例如，如果放入或删除 1.6 KB 的项目，则 DynamoDB 会将项目大小舍入为 2 KB。

PutItem、UpdateItem 和 DeleteItem 允许有条件写入，其中指定一个表达式的求值结果必须为 true，才能成功执行操作。如果该表达式计算为 false，DynamoDB 仍会消耗表的写入容量单位。消耗量取决于项目的大小（无论是表中的现有项目，还是您正在尝试创建或更新的新项目）。例如，如果现有项目为 300kb，而您尝试创建或更新的新项目为 310kb，则消耗的写入容量单位将为 310kb 项目。

---

# Global tables是什么

Global Tables 是 Amazon DynamoDB 提供的一种全球性的多区域复制解决方案，用于实现跨多个 AWS 区域的数据复制和数据访问。它允许您在多个 AWS 区域中创建和自动同步多个 DynamoDB 表，以实现低延迟的数据访问和全球性的高可用性。

使用 Global Tables，您可以在多个 AWS 区域中创建相同的 DynamoDB 表，并自动进行数据复制和同步。当您在一个区域中写入、更新或删除数据时，这些变更会自动同步到其他区域的表中，使得数据保持一致性。这意味着您可以将读写流量分散到不同的区域，实现全球性的负载均衡和高可用性。

Global Tables 还提供了一致的读取能力，即在任何区域读取数据时，您都可以获得最近的一致性数据。这是通过将写操作的变更异步复制到其他区域来实现的。当您在一个区域中进行写操作后，可以立即从该区域读取到最新的数据，而在其他区域稍后进行同步。

使用 Global Tables 可以帮助您构建全球性的应用程序，实现低延迟、高可用性和容错能力。它特别适用于需要在多个地理位置提供服务的应用程序，如跨大陆的分布式系统、全球性的网站和应用程序等。

需要注意的是，使用 Global Tables 需要在各个区域中创建 DynamoDB 表，并在这些表之间进行配置和同步。此外，数据复制和同步可能会产生额外的数据传输和存储成本。详细的使用和配置信息可以参考 Amazon DynamoDB 的文档和 Global Tables 的相关文档。

---

# CloudFormation Fn 函数

在 AWS CloudFormation 中，Fn 函数是用于处理模板中的各种转换、引用和函数操作的内置函数。以下是一些常用的 CloudFormation Fn 函数：

Fn::Ref：用于引用资源的逻辑名称或参数的值。
Fn::GetAtt：用于获取资源的属性值。
Fn::ImportValue：用于在不同的堆栈之间引用导出的值。
Fn::Sub：用于替换字符串中的变量或表达式。
Fn::Join：用于将多个字符串连接在一起。
Fn::Select：用于从列表或映射中选择特定的元素。
Fn::Split：用于将字符串拆分为列表。
Fn::If：用于根据条件选择不同的值。
Fn::Not：用于对布尔值进行取反操作。
Fn::Equals：用于检查两个值是否相等。
Fn::Condition：用于指定条件的逻辑值。
这只是一些常见的 Fn 函数示例，CloudFormation 还提供了其他功能丰富的 Fn 函数，可以根据需要进行使用。您可以参考 AWS CloudFormation 的官方文档以获取更详细的 Fn 函数列表和用法说明。

--- 
# Load Balancer 类型

AWS 提供了几种不同类型的负载均衡器（Load Balancer）：

Application Load Balancer (ALB)：ALB 是一种高级的负载均衡器，适用于将流量分发到多个应用程序实例，具有高级路由功能和支持 WebSocket 协议。它可以基于请求的内容进行路由决策，并支持应用层协议（如 HTTP、HTTPS）。

Network Load Balancer (NLB)：NLB 是一种 Layer 4（传输层）负载均衡器，适用于处理高吞吐量的流量，以及需要静态 IP 地址的应用程序。它支持 TCP、UDP 和 TLS 协议，并提供极高的性能和低延迟。

Classic Load Balancer (CLB)：CLB 是 AWS 最早引入的负载均衡器，提供基本的负载均衡功能，并支持传统的 HTTP 和 HTTPS 流量。但是，AWS 推荐使用 ALB 或 NLB 代替 CLB，因为 ALB 和 NLB 具有更多的功能和灵活性。

这些负载均衡器都是完全托管的 AWS 服务，可以自动将流量分发到多个目标实例，提高应用程序的可用性和可伸缩性。您可以根据应用程序的需求选择适当的负载均衡器类型。

---

# ALB Auto Scaling的CloudWatch Metric

ALB（Application Load Balancer）Auto Scaling 依赖于 CloudWatch 来监控和自动调整目标组（Target Group）的实例数量。以下是一些常用的 CloudWatch Metric，用于配置 ALB Auto Scaling：

RequestCountPerTarget：这个指标表示每个目标实例接收到的请求数量。可以根据请求数来自动调整目标组的实例数量。

HealthyHostCount：这个指标表示目标组中处于健康状态的实例数量。当实例变得不健康或无法响应请求时，可以根据这个指标来自动调整目标组的实例数量。

UnHealthyHostCount：这个指标表示目标组中处于不健康状态的实例数量。与 HealthyHostCount 相对应，可以根据不健康实例的数量来自动调整目标组的实例数量。

TargetResponseTime：这个指标表示目标实例处理请求的平均响应时间。可以根据响应时间来自动调整目标组的实例数量，以确保性能符合预期。

RequestCount：这个指标表示 ALB 收到的总请求数量。根据请求数量来自动调整目标组的实例数量，以处理更高的负载。

以上是一些常见的 CloudWatch Metric，可以用于配置 ALB Auto Scaling。您可以根据应用程序的需求和性能指标来选择适当的 Metric，并设置自动调整策略，以确保 ALB 可根据负载情况自动扩展或缩减实例数量。

---
# In-flight encryption 和 Encryption at rest

In-flight encryption和encryption at rest是两种不同的数据加密方式，用于保护 AWS Elastic Block Store (EBS) 存储卷的数据安全。

In-flight encryption（传输中加密）：这是指在数据在传输过程中进行加密，确保数据在从存储卷读取或写入到存储卷时的安全传输。在 EBS 的情况下，in-flight encryption 确保数据在存储卷和 Amazon EC2 实例之间的传输过程中进行加密。这种加密保护了数据在网络传输中的安全性。

Encryption at rest（静态存储加密）：这是指数据在存储卷上静态存储时进行加密，确保数据在存储卷上的安全性。在 EBS 的情况下，encryption at rest 通过对存储卷上的数据进行加密来保护数据的安全性。加密的数据在存储卷上保持加密状态，无论是在存储卷处于活动状态还是处于闲置状态。

使用 AWS KMS（Key Management Service），您可以对 EBS 存储卷进行 in-flight encryption 和 encryption at rest。通过选择适当的加密选项，您可以确保 EBS 存储卷的数据在传输和存储过程中得到保护，增强数据的安全性。

---

# Secrets Manager 是什么

AWS Secrets Manager 是一项用于安全存储和管理敏感信息的托管服务。它提供了一种简单的方法来存储和访问密码、API 密钥、数据库凭据和其他敏感信息，以便在应用程序、服务和 AWS 资源之间进行安全的共享和管理。

通过 Secrets Manager，您可以轻松地管理敏感数据，而无需在应用程序代码中明文存储密码和凭据。它提供了以下主要功能：

安全存储：Secrets Manager 将敏感数据以加密的形式存储在 AWS 管理的安全环境中。数据在存储和传输过程中得到保护，确保数据的安全性。

访问控制：您可以使用 AWS Identity and Access Management (IAM) 来管理对 Secrets Manager 中存储的敏感信息的访问权限。通过细粒度的访问控制策略，可以限制谁可以读取和更新存储的秘密。

密码轮换：Secrets Manager 支持自动密码轮换，您可以定义规则和策略来定期更换存储的密码，以增加安全性。

集成和自动化：Secrets Manager 可与各种 AWS 服务和应用程序集成，包括 Amazon RDS、Amazon Redshift、AWS Lambda 等。通过集成，您可以直接从应用程序或服务中访问和使用存储的敏感信息。

通过使用 Secrets Manager，您可以集中管理和保护敏感信息，减少了将密码和凭据硬编码到代码或配置文件中的风险，并提供了更好的安全性和可管理性。


---
# health check type of Auto Scaling group

在 Auto Scaling 组中，健康检查类型可以是以下两种：

EC2：健康检查由 EC2 实例自身执行。Auto Scaling 会发送一个请求到实例的指定端口，并根据返回的状态码判断实例的健康状态。

ELB：健康检查由 Elastic Load Balancer (ELB) 执行。Auto Scaling 会将健康检查请求发送到与 Auto Scaling 组关联的负载均衡器，负载均衡器将根据目标组中实例的状态来确定实例的健康状态。

根据您提供的语句，您需要将 Auto Scaling 组的健康检查类型从 EC2 更改为 ELB。这意味着健康检查请求将由负载均衡器执行，而不是直接发送到实例。

请注意，要更改 Auto Scaling 组的健康检查类型，您需要使用配置文件或 AWS CLI 命令进行操作。具体的操作步骤和配置方式会根据您的实际环境和需求而有所不同。


---

# Cognito user pool和identity pool的区别是什么 

Cognito User Pool 和 Cognito Identity Pool 是 AWS Cognito 服务中的两个不同的组件，用于用户身份验证和授权。它们之间的主要区别如下：

Cognito User Pool（用户池）：Cognito User Pool 是一项身份验证服务，用于管理用户的注册、登录和身份验证。它提供了用户注册、登录、密码重置等功能，并生成与用户关联的身份令牌。User Pool 可以轻松集成到应用程序中，允许开发人员管理用户的身份和访问控制。它是面向用户的身份验证服务。

Cognito Identity Pool（身份池）：Cognito Identity Pool 是一项授权服务，用于控制用户对 AWS 资源的访问权限。它允许用户通过不同的身份提供者进行身份验证，如 Cognito User Pool、社交媒体登录（如 Facebook、Google）、企业身份提供者等。Identity Pool 为用户生成一组临时的安全凭证（如 AWS 临时访问密钥），这些凭证用于访问受保护的 AWS 资源。它是面向授权和访问控制的服务。

总体而言，Cognito User Pool 主要用于管理用户的注册和身份验证，提供用户身份令牌，而 Cognito Identity Pool 则用于授权用户对 AWS 资源的访问，提供安全凭证。User Pool 是用于用户身份验证的身份提供者，而 Identity Pool 则是用于授权访问 AWS 资源的身份提供者。两者通常一起使用，以提供完整的用户身份验证和访问控制解决方案。

---

# CodeDeploy Deployment Groups

CodeDeploy Deployment Groups（部署组）是AWS CodeDeploy服务中的一个概念，用于管理和控制应用程序的部署过程。Deployment Group定义了一组具有相似部署要求和配置的实例，这些实例可以是EC2实例、自动扩展组或者Lambda函数。

通过创建Deployment Group，您可以将部署目标分组，便于管理和控制应用程序的部署。每个Deployment Group可以配置以下属性：

部署类型：指定部署的方式，可以是一次性部署、基于时间的滚动部署、基于流量的滚动部署等。
部署配置：定义部署过程中的各项设置，例如并发数、超时时间、失败阈值等。
部署策略：定义应用程序的更新策略，例如滚动更新时的权重分配、批次大小等。
实例过滤：根据标签、标识符等过滤条件选择要包含或排除的实例。
自动扩展组：将自动扩展组作为部署目标，以便在部署期间自动调整实例的数量。
Lambda函数：将Lambda函数作为部署目标，用于执行应用程序的更新逻辑。
通过Deployment Group，您可以对具有相似配置和部署要求的实例进行批量部署，并且具有灵活的部署控制和配置选项。您可以在AWS管理控制台、AWS CLI或者使用AWS SDK来创建和管理Deployment Groups。

使用CodeDeploy Deployment Groups，您可以轻松地管理和控制应用程序的部署过程，确保应用程序的更新和发布顺利进行，并提供了部署的可重复性和一致性。


假设您有一个Web应用程序，需要在多个环境中进行部署，例如开发环境、测试环境和生产环境。您可以为每个环境创建一个Deployment Group，并定义适合该环境的部署配置和策略。

开发环境部署组（Development Deployment Group）：

部署类型：一次性部署
部署配置：并发数为5，超时时间为10分钟
部署策略：无需滚动更新，直接替换现有实例
实例过滤：根据标签选择开发环境实例
自动扩展组：无

测试环境部署组（Testing Deployment Group）：

部署类型：基于时间的滚动部署
部署配置：并发数为2，超时时间为15分钟
部署策略：按时间表进行滚动更新，每次更新一定数量的实例
实例过滤：根据标签选择测试环境实例
自动扩展组：无

生产环境部署组（Production Deployment Group）：

部署类型：基于流量的滚动部署
部署配置：并发数为3，超时时间为20分钟
部署策略：按流量进行滚动更新，逐步将流量从旧版本切换到新版本
实例过滤：根据标签选择生产环境实例
自动扩展组：根据需求调整实例数量
通过创建不同的Deployment Groups，您可以针对每个环境应用不同的部署配置和策略，确保在不同的环境中具有适当的部署控制和灵活性。这样，您可以根据需要管理和控制每个环境的应用程序部署过程，确保应用程序的可靠性和一致性。


---


# Assume role

https://repost.aws/zh-Hans/knowledge-center/lambda-function-assume-iam-role

---

# provisioned concurrency和reserved concurrency 是什么

Provisioned Concurrency和Reserved Concurrency是AWS Lambda提供的两种功能，用于控制Lambda函数的并发行为。

Provisioned Concurrency（预置并发）：

Provisioned Concurrency允许您在Lambda函数中预先配置一定数量的执行环境（即实例）。
预置并发可以减少冷启动延迟，确保Lambda函数的实例始终保持热状态，以便立即响应请求。
您可以指定要为函数预置的并发实例数，并且这些实例将一直保持激活状态，无论是否有请求到达函数。
这对于对冷启动延迟非常敏感的应用程序或高吞吐量应用程序非常有用。
Reserved Concurrency（保留并发）：

Reserved Concurrency允许您为Lambda函数设置最大并发执行数量。
您可以指定函数可以并行处理的请求数量，并限制同时运行的执行实例数量。
保留并发设置可以确保函数不会超过指定的并发限制，用于控制函数的资源消耗。
保留并发还可以帮助您确保在与其他Lambda函数共享相同资源的情况下，您的函数获得适当的资源份额。
这两个功能都可以通过AWS管理控制台、AWS CLI或AWS SDK进行配置和管理。

总结：

Provisioned Concurrency用于预先配置Lambda函数的执行实例，以减少冷启动延迟。
Reserved Concurrency用于限制Lambda函数的最大并发执行数量，以控制函数的资源消耗。

---

# Deployment methods Blue/Green

https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.deploy-existing-version.html

---

# 为什么我终止的 Amazon ECS 容器实例仍注册到其集群？

简短描述

如果您通过已连接的 Amazon ECS 容器代理终止 RUNNING 容器实例，则代理将会从您的实例中自动取消注册该实例。但是，如果您通过已断开连接的代理终止 STOPPED 容器实例，则该容器实例不会自动从集群中删除。
解决方法

使用 Amazon ECS 控制台或 AWS 命令行界面，注销处于已停止状态的容器实例。

注销的容器实例将不再显示为 Amazon ECS 集群中的资源。

要排查断开连接的 ECS 代理，请参阅为什么具有 Amazon Linux 2 AMI 的 Amazon ECS 容器实例会断开连接？


---

# Code Deploy 

Deployment Type – method used to deploy the application to a Deployment Group 
• In-place Deployment – supports EC2/On-Premises
• Blue/Green Deployment – supports EC2 instances only, AWS Lambda, and Amazon ECS



## In-place Deployment和Blue/Green Deployment是什么 

In-place Deployment 和 Blue/Green Deployment 是两种常见的部署策略，用于更新和发布应用程序或服务的新版本。它们具有不同的特点和适用场景：

In-place Deployment（原地部署）：

In-place Deployment 是一种直接在现有环境中进行更新的部署方式，即在原有的部署环境中直接替换旧版本的应用程序或服务。
在 In-place Deployment 中，新版本的应用程序会直接替换旧版本，更新会在现有的服务器或实例上进行，不需要创建新的环境。
这种部署方式通常适用于轻量级应用或对服务中断时间要求不高的情况。它可以快速进行部署，但如果更新出现问题，可能会导致整个应用不可用。
Blue/Green Deployment（蓝绿部署）：

Blue/Green Deployment 是一种通过创建并切换到一个全新的环境来进行部署的策略。这个全新的环境称为 Green 环境，而旧版本的环境则称为 Blue 环境。
在 Blue/Green Deployment 中，新版本的应用程序会先在 Green 环境中进行部署和测试，当测试通过并确认稳定后，可以将流量从 Blue 环境切换到 Green 环境。
这种部署方式具有较低的风险，因为在切换之前可以对新版本进行彻底测试和验证。如果出现问题，可以快速切换回 Blue 环境以回滚到旧版本。
Blue/Green Deployment 通常适用于关键业务应用、高可用性要求较高的系统，以及对发布流程有更高控制要求的情况。
选择使用 In-place Deployment 还是 Blue/Green Deployment 取决于您的具体需求和应用程序的特点。如果对服务中断时间要求较低，且可以容忍一定风险，那么 In-place Deployment 可能更适合。如果对服务中断时间敏感，需要更高的可用性和回滚能力，以及更精细的发布控制，那么 Blue/Green Deployment 可能更适合。


---

# Stage Variables

Stage Variables（阶段变量）是 AWS API Gateway 中的一个功能，它允许您在不同的 API 阶段之间共享和访问自定义变量。API Gateway 是一项托管服务，用于构建、部署和管理具有 RESTful 接口的应用程序。

使用 Stage Variables，您可以在 API 的不同阶段（例如开发、测试、生产）之间定义变量，并在您的 API 配置中引用这些变量。这样，您可以根据不同的阶段配置不同的行为和设置，而无需修改每个 API 方法的代码。

Stage Variables 可以存储各种类型的数据，例如字符串、数字和布尔值。您可以在 API 的定义中使用这些变量，例如设置请求和响应的参数、定义集成和映射模板、配置条件和缓存等。

Stage Variables 具有以下特点：

可以在 API 的部署阶段设置和更新 Stage Variables。
变量的值在每个阶段是固定的，可以在不同的 API 部署中设置不同的值。
变量可以在 API Gateway 的控制台、API 配置文件或使用 AWS CLI 和 AWS SDK 进行设置和管理。
通过使用 Stage Variables，您可以更灵活地管理和配置 API Gateway，根据不同的阶段和环境调整行为和设置，使得您的 API 在不同的部署中具有可配置性和可重用性。

---

# Identity-based policies and resource-based policies

https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_identity-vs-resource.html

https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html#policy-eval-basics

---

# Route 53 routing policy 介绍

Route 53是AWS提供的域名系统（DNS）服务，用于管理和路由域名解析请求。Route 53提供了几种不同的路由策略，用于决定如何将域名解析请求路由到相应的终端节点。以下是常见的Route 53路由策略：

Simple Routing：简单路由策略允许将一个域名解析请求路由到一个资源记录集中的单个值。它适用于单一终端节点的情况，如单个ELB（Elastic Load Balancer）或单个IP地址。

Weighted Routing：加权路由策略允许根据权重分配流量到不同的资源记录集。可以为每个记录集分配一个权重值，流量将根据权重比例进行分发。适用于实现流量分流和AB测试等场景。

Latency-Based Routing：延迟路由策略根据用户请求的地理位置将流量路由到延迟最低的终端节点。可以配置多个资源记录集，每个记录集关联特定地理区域的终端节点。适用于需要优化用户体验的全球性应用。

Failover Routing：故障转移路由策略用于实现高可用性。可以配置主资源记录集和备份资源记录集，在主记录集不可用时自动将流量路由到备份记录集。

Geolocation Routing：地理位置路由策略根据用户请求的地理位置将流量路由到相应的终端节点。可以为不同地理区域配置不同的资源记录集。

Multi-Value Answer Routing：多值答案路由策略允许将流量分布到多个资源记录集中的多个值。每个记录集包含一个或多个值，Route 53将随机选择一个值返回给请求者。

这些路由策略可根据应用程序的需求和目标进行灵活配置，以实现不同的负载均衡、高可用性和全球就近访问等目标。

---

# Route 53 Alias Records介绍

Alias Records是AWS Route 53中的一种特殊类型的DNS记录。Alias Records允许将一个域名解析请求直接映射到另一个AWS资源，而无需使用传统的CNAME记录。

Alias Records具有以下特点和优势：

无需中间解析：与传统的CNAME记录不同，Alias Records直接将域名解析请求映射到特定的AWS资源，而不需要进行额外的中间解析步骤。这样可以减少解析的延迟和减少不必要的DNS查询。

自动更新：当目标资源的IP地址发生变化时，Alias Records会自动更新，确保域名解析请求仍然指向正确的资源。这使得在资源发生变化时无需手动更新DNS记录。

支持多个AWS服务：Alias Records可以用于将域名解析请求映射到多个AWS服务，包括但不限于S3存储桶、CloudFront分发、ELB负载均衡器和API Gateway等。这样可以方便地将域名解析请求直接路由到相关的AWS服务上。

与Route 53功能集成：Alias Records与Route 53的其他功能集成紧密，例如Failover Routing、Latency-Based Routing和Weighted Routing等。可以将Alias Records与这些功能结合使用，以实现高可用性、全球就近访问和流量分流等需求。

使用Alias Records可以简化和优化应用程序的DNS配置和管理。它提供了一种高级的解析方式，使得将域名解析请求与AWS资源直接关联变得更加灵活和高效。

---

## Blue/Green Deployments

A blue/green deployment is a deployment strategy in which you create two separate, but identical environments. One environment (blue) is running the current application version and one environment (green) is running the new application version. Using a blue/green deployment strategy increases application availability and reduces deployment risk by simplifying the rollback process if a deployment fails. Once testing has been completed on the green environment, live application traffic is directed to the green environment and the blue environment is deprecated.

A number of AWS deployment services support blue/green deployment strategies including Elastic Beanstalk, OpsWorks, CloudFormation, CodeDeploy, and Amazon ECS. Refer to Blue/Green Deployments on AWS
for more details and strategies for implementing blue/green deployment processes for your application. 

## Rolling Deployments

A rolling deployment is a deployment strategy that slowly replaces previous versions of an application with new versions of an application by completely replacing the infrastructure on which the application is running. For example, in a rolling deployment in Amazon ECS, containers running previous versions of the application will be replaced one-by-one with containers running new versions of the application.

A rolling deployment is generally faster than a blue/green deployment; however, unlike a blue/green deployment, in a rolling deployment there is no environment isolation between the old and new application versions. This allows rolling deployments to complete more quickly, but also increases risks and complicates the process of rollback if a deployment fails.

Rolling deployment strategies can be used with most deployment solutions. Refer to CloudFormation Update Policies for more information on rolling deployments with CloudFormation; Rolling Updates with Amazon ECS for more details on rolling deployments with Amazon ECS; Elastic Beanstalk Rolling Environment Configuration Updates for more details on rolling deployments with Elastic Beanstalk; and Using a Rolling Deployment in AWS OpsWorks for more details on rolling deployments with OpsWorks. 

## In-Place Deployments

An in-place deployment is a deployment strategy that updates the application version without replacing any infrastructure components. In an in-place deployment, the previous version of the application on each compute resource is stopped, the latest application is installed, and the new version of the application is started and validated. This allows application deployments to proceed with minimal disturbance to underlying infrastructure.

An in-place deployment allows you to deploy your application without creating new infrastructure; however, the availability of your application can be affected during these deployments. This approach also minimizes infrastructure costs and management overhead associated with creating new resources.

Refer to Overview of an In-Place Deployment for more details on using in-place deployment strategies with CodeDeploy. 

---

# AWS CloudFormation、AWS SAM、AWS Elastic Beanstalk、AWS CDK 和 AWS CodeDeploy 的区别

AWS CloudFormation：CloudFormation 是一项基础设施即代码服务，允许您以模板的形式定义和部署整个应用程序的基础架构和资源。它提供了声明性的方式来定义和管理基础设施，支持自动化部署和更新。CloudFormation 可以定义各种 AWS 资源，并提供一致性、可重复性和可管理性。

AWS SAM (Serverless Application Model)：SAM 是一个基于 CloudFormation 的扩展，专注于无服务器应用程序的构建和部署。它简化了无服务器应用程序的模板编写和管理过程，并提供了预定义的模板资源和转换。SAM 支持定义和部署 Lambda 函数、API Gateway、DynamoDB 表等无服务器资源，并提供本地开发和测试功能。

AWS Elastic Beanstalk：Elastic Beanstalk 是一项托管服务，用于快速部署和扩展应用程序。它简化了应用程序的部署和管理过程，无需关注底层基础设施的细节。Elastic Beanstalk 支持多种编程语言和应用程序框架，自动处理资源的创建和配置。您只需上传应用程序代码，Elastic Beanstalk 将自动完成部署、弹性扩展和应用程序的运行。

AWS CDK (Cloud Development Kit)：CDK 是一种软件开发工具包，用于以编程方式定义和部署 AWS 资源。它允许使用编程语言（如 TypeScript、Python、Java 等）来定义基础设施，而不是使用模板。CDK 提供了丰富的库和类来定义和组合 AWS 资源，并支持生成 CloudFormation 模板进行部署。

AWS CodeDeploy：CodeDeploy 是一项持续交付服务，用于自动化应用程序的部署到多个目标环境。它支持多种部署策略，包括原位部署和蓝绿部署，并提供了灵活的部署配置选项。CodeDeploy 可以与其他 AWS 服务集成，如 EC2、Lambda、ECS 等，以支持不同类型的应用程序部署。它提供了部署流程的自动化和可视化，确保应用程序在不同环境中的一致性和可靠性。

总结：CloudFormation 是基础设施即代码服务，SAM 是 CloudFormation 的扩展，专注于无服务器应用程序。Elastic Beanstalk 是托管服务，简化应用程序的部署和管理。CDK 是一种编程工具包，用于以编程方式定义和部署 AWS 资源。CodeDeploy 是持续交付服务，自动化应用程序

---

# ECS

---

# Dynamic Scaling Policies

---

# beanstalk Deployment policies

https://docs.aws.amazon.com/zh_cn/elasticbeanstalk/latest/dg/using-features.rolling-version-deploy.html
https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.rolling-version-deploy.html

---

# CloudFormation Building Blocks
## Templates components

https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html

```yaml
---
AWSTemplateFormatVersion: "version date"

Description:
  String

Metadata:
  template metadata

Parameters:
  set of parameters

Rules:
  set of rules

Mappings:
  set of mappings

Conditions:
  set of conditions

Transform:
  set of transforms

Resources:
  set of resources

Outputs:
  set of outputs
```

---

# Billing and cost management

---

# x-amz-server-side-encryption

---

# .ebextensitons

---

# X-Ray Sampling

---

# Lambda Authorizer

---
