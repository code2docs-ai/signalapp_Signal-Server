# 基础信息

|      |      |
|------|------|
| 名称 | configuration |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/configuration |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.configuration |
| 概述说明 | IssuedReceiptsTableConfiguration类配置收据生成规则和支付提供商最大收据数，管理过期收据。 |

# 说明

## 概述

该代码模块主要围绕系统的配置管理展开，涵盖了多个关键功能模块的配置类。这些配置类负责管理系统的各种参数和行为，包括DynamoDB表配置、Redis集群配置、支付系统配置、验证码控制、消息持久化、用户注册、版本控制等。通过动态调整这些配置，系统能够适应不同的业务需求，提升系统的兼容性、安全性和性能。

## 主要业务场景

1. **DynamoDB表管理**：`IssuedReceiptsTableConfiguration`类继承自`DynamoDbTables.TableWithExpiration`，负责配置生成器和支付提供商的最大收据数，并处理带有过期时间的DynamoDB表配置，确保收据数据在一定时间后自动失效。

2. **Redis集群配置**：`RedisConfiguration`类和`RedisClusterConfiguration`类用于管理Redis集群的连接和操作设置，包括URI、超时、熔断器和重试配置等，确保客户端具备容错能力，适用于高可用性和高并发场景。

3. **支付系统配置**：`BraintreeConfiguration`类和`StripeConfiguration`类负责管理支付系统的相关配置，包括支付提供商的最大收据数、支付操作的限制等，确保支付系统的安全性和合规性。

4. **验证码控制**：`SpamFilterConfiguration`类用于配置垃圾邮件过滤功能，包含环境属性和构造方法，确保验证码服务的严格性和独立性。

5. **消息持久化**：`MessageCacheConfiguration`类用于配置Redis集群的相关参数，并设置持久化操作的延迟时间，确保消息的高可靠性和存储优化。

6. **用户注册与版本控制**：`RegistrationServiceConfiguration`类和`ClientReleaseConfiguration`类负责管理用户注册和客户端版本的配置，确保不同版本的客户端能够正常运行，同时控制用户代理的访问。

7. **动态配置管理**：`DynamicConfiguration`类负责整合多个动态配置项，包括实验、限速、支付和验证码等功能模块，提供统一的配置管理接口，确保系统能够灵活响应不同的业务需求。

通过这些配置管理，系统能够在不同的业务场景中实现灵活、高效的配置调整，提升系统的整体性能和用户体验。


### 包内部结构视图

```mermaid
graph TD
    configuration --> IssuedReceiptsTableConfiguration.java
    configuration --> CloudflareTurnConfiguration.java
    configuration --> RegistrationServiceClientFactory.java
    configuration --> KeyTransparencyServiceConfiguration.java
    configuration --> BraintreeConfiguration.java
    configuration --> DeviceCheckConfiguration.java
    configuration --> BadgeConfiguration.java
    configuration --> ShortCodeExpanderConfiguration.java
    configuration --> CdnConfiguration.java
    configuration --> StaticAwsCredentialsFactory.java
    configuration --> RedisConfiguration.java
    configuration --> RetryConfiguration.java
    configuration --> DatadogConfiguration.java
    configuration --> VirtualThreadConfiguration.java
    configuration --> PaymentsServiceConfiguration.java
    configuration --> ClientReleaseConfiguration.java
    configuration --> secrets
    configuration --> IdlePrimaryDeviceReminderConfiguration.java
    configuration --> MessageCacheConfiguration.java
    configuration --> DirectoryV2ClientConfiguration.java
    configuration --> GooglePlayBillingConfiguration.java
    configuration --> TurnUriConfiguration.java
    configuration --> BadgesConfiguration.java
    configuration --> ReportMessageConfiguration.java
    configuration --> SecureValueRecovery2Configuration.java
    configuration --> RemoteConfigConfiguration.java
    configuration --> AwsCredentialsProviderFactory.java
    configuration --> ApnConfiguration.java
    configuration --> FaultTolerantRedisClientFactory.java
    configuration --> SubscriptionLevelConfiguration.java
    configuration --> StripeConfiguration.java
    configuration --> SpamFilterConfiguration.java
    configuration --> dynamic
    configuration --> PubSubPublisherFactory.java
    configuration --> DynamoDbClientFactory.java
    configuration --> MessageByteLimitCardinalityEstimatorConfiguration.java
    configuration --> URLSerializationConverter.java
    configuration --> AppleDeviceCheckConfiguration.java
    configuration --> ZkConfig.java
    configuration --> NoiseWebSocketTunnelConfiguration.java
    configuration --> S3ObjectMonitorFactory.java
    configuration --> RedisClusterConfiguration.java
    configuration --> FcmConfiguration.java
    configuration --> DogstatsdConfiguration.java
    configuration --> MaxDeviceConfiguration.java
    configuration --> ClientCdnConfiguration.java
    configuration --> PaymentsServiceClientsConfiguration.java
    configuration --> SecureStorageServiceConfiguration.java
    configuration --> UnidentifiedDeliveryConfiguration.java
    configuration --> TurnConfiguration.java
    configuration --> OneTimeDonationConfiguration.java
    configuration --> LinkDeviceSecretConfiguration.java
    configuration --> OneTimeDonationCurrencyConfiguration.java
    configuration --> PaymentsServiceClientsFactory.java
    configuration --> AccountsTableConfiguration.java
    configuration --> Cdn3StorageManagerConfiguration.java
    configuration --> RegistrationServiceConfiguration.java
    configuration --> DynamoDbTables.java
    configuration --> AppleAppStoreConfiguration.java
    configuration --> TlsKeyStoreConfiguration.java
    configuration --> DirectoryV2Configuration.java
    configuration --> CircuitBreakerConfiguration.java
    configuration --> GenericZkConfig.java
    configuration --> FaultTolerantRedisClusterFactory.java
    configuration --> SubscriptionPriceConfiguration.java
    configuration --> DynamoDbClientConfiguration.java
    configuration --> DefaultPubSubPublisherFactory.java
    configuration --> MonitoredS3ObjectConfiguration.java
    configuration --> GcpAttachmentsConfiguration.java
    configuration --> DefaultAwsCredentialsFactory.java
    configuration --> SubscriptionConfiguration.java
    configuration --> ExternalRequestFilterConfiguration.java
    secrets --> SecretBytesList.java
    secrets --> Secret.java
    secrets --> SecretStore.java
    secrets --> BaseSecretValidator.java
    secrets --> SecretBytes.java
    secrets --> SecretString.java
    secrets --> SecretsModule.java
    secrets --> SecretStringList.java
    dynamic --> DynamicRemoteDeprecationConfiguration.java
    dynamic --> DynamicE164ExperimentEnrollmentConfiguration.java
    dynamic --> DynamicVirtualThreadConfiguration.java
    dynamic --> DynamicRegistrationConfiguration.java
    dynamic --> DynamicMessagePersisterConfiguration.java
    dynamic --> DynamicExperimentEnrollmentConfiguration.java
    dynamic --> DynamicCaptchaConfiguration.java
    dynamic --> DynamicPaymentsConfiguration.java
    dynamic --> DynamicRateLimitPolicy.java
    dynamic --> DynamicMetricsConfiguration.java
    dynamic --> DynamicConfiguration.java
```

该流程图展示了Signal-Server项目中`configuration`目录下的文件及其子目录`secrets`和`dynamic`的层级关系。`configuration`目录下包含多个配置文件，而`secrets`和`dynamic`子目录分别管理密钥和动态配置相关的文件。整个结构清晰地反映了项目的配置管理架构。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [RegistrationServiceClientFactory.java](RegistrationServiceClientFactory.md) | file | 信息为空，无法生成概要描述。 |
| [IdlePrimaryDeviceReminderConfiguration.java](IdlePrimaryDeviceReminderConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [ClientReleaseConfiguration.java](ClientReleaseConfiguration.md) | file | 无内容可总结。 |
| [PaymentsServiceConfiguration.java](PaymentsServiceConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [VirtualThreadConfiguration.java](VirtualThreadConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [StaticAwsCredentialsFactory.java](StaticAwsCredentialsFactory.md) | file | 无内容提供，请补充具体信息。 |
| [CdnConfiguration.java](CdnConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [ShortCodeExpanderConfiguration.java](ShortCodeExpanderConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [DeviceCheckConfiguration.java](DeviceCheckConfiguration.md) | file | 输入为空，无法生成概要描述。 |
| [StripeConfiguration.java](StripeConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [SubscriptionLevelConfiguration.java](SubscriptionLevelConfiguration.md) | file | 无内容可总结。 |
| [FaultTolerantRedisClientFactory.java](FaultTolerantRedisClientFactory.md) | file | 输入信息为空，无法生成概要描述。 |
| [AwsCredentialsProviderFactory.java](AwsCredentialsProviderFactory.md) | file | 无内容，无法生成概要。 |
| [SecureValueRecovery2Configuration.java](SecureValueRecovery2Configuration.md) | file | 无内容提供，无法生成概要描述。 |
| [BadgesConfiguration.java](BadgesConfiguration.md) | file | BadgesConfiguration类管理徽章配置，验证收据级别配置。 |
| [OneTimeDonationConfiguration.java](OneTimeDonationConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [UnidentifiedDeliveryConfiguration.java](UnidentifiedDeliveryConfiguration.md) | file | 输入内容为空，无法生成概要描述。 |
| [PaymentsServiceClientsConfiguration.java](PaymentsServiceClientsConfiguration.md) | file | 暂无内容可供总结。 |
| [DogstatsdConfiguration.java](DogstatsdConfiguration.md) | file | Dogstatsd配置类含步长、环境、主机属性，返回Datadog风格及关闭等待时长。 |
| [S3ObjectMonitorFactory.java](S3ObjectMonitorFactory.md) | file | 信息为空，无法生成概要描述。 |
| [NoiseWebSocketTunnelConfiguration.java](NoiseWebSocketTunnelConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [ZkConfig.java](ZkConfig.md) | file | 信息为空，无法生成概要描述。 |
| [MessageByteLimitCardinalityEstimatorConfiguration.java](MessageByteLimitCardinalityEstimatorConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [DynamoDbClientFactory.java](DynamoDbClientFactory.md) | file | 无内容提供，无法生成概要描述。 |
| [PubSubPublisherFactory.java](PubSubPublisherFactory.md) | file | 信息为空，无法生成概要描述。 |
| [GenericZkConfig.java](GenericZkConfig.md) | file | 信息为空，无法生成概要描述。 |
| [TlsKeyStoreConfiguration.java](TlsKeyStoreConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [AppleAppStoreConfiguration.java](AppleAppStoreConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [RegistrationServiceConfiguration.java](RegistrationServiceConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [Cdn3StorageManagerConfiguration.java](Cdn3StorageManagerConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [ExternalRequestFilterConfiguration.java](ExternalRequestFilterConfiguration.md) | file | 输入信息为空，请提供具体内容以便生成概要描述。 |
| [SubscriptionConfiguration.java](SubscriptionConfiguration.md) | file | 订阅配置类包含徽章、备份期限、捐赠等级及验证方法。 |
| [GcpAttachmentsConfiguration.java](GcpAttachmentsConfiguration.md) | file | 内容为空，无法生成概要描述。 |
| [DefaultPubSubPublisherFactory.java](DefaultPubSubPublisherFactory.md) | file | 内容为空，无法生成概要描述。 |
| [DynamoDbClientConfiguration.java](DynamoDbClientConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [DefaultAwsCredentialsFactory.java](DefaultAwsCredentialsFactory.md) | file | 信息为空，无法生成概要描述。 |
| [MonitoredS3ObjectConfiguration.java](MonitoredS3ObjectConfiguration.md) | file | 输入信息为空，请提供具体内容以便生成概要描述。 |
| [SubscriptionPriceConfiguration.java](SubscriptionPriceConfiguration.md) | file | 无内容可总结。 |
| [FaultTolerantRedisClusterFactory.java](FaultTolerantRedisClusterFactory.md) | file | 信息为空，无法生成概要描述。 |
| [CircuitBreakerConfiguration.java](CircuitBreakerConfiguration.md) | file | 断路器配置类包含故障率、半开状态调用数、滑动窗口及最小调用数、开放状态等待时间等参数。 |
| [DirectoryV2Configuration.java](DirectoryV2Configuration.md) | file | DirectoryV2Configuration类包含并管理DirectoryV2ClientConfiguration实例。 |
| [DynamoDbTables.java](DynamoDbTables.md) | file | DynamoDbTables类管理基础表及带过期时间的DynamoDB表。 |
| [AccountsTableConfiguration.java](AccountsTableConfiguration.md) | file | AccountsTableConfiguration继承Table，包含四个表名属性及getter方法。 |
| [PaymentsServiceClientsFactory.java](PaymentsServiceClientsFactory.md) | file | 无内容提供，无法生成概要描述。 |
| [OneTimeDonationCurrencyConfiguration.java](OneTimeDonationCurrencyConfiguration.md) | file | 输入信息为空，请提供具体内容以便生成概要描述。 |
| [LinkDeviceSecretConfiguration.java](LinkDeviceSecretConfiguration.md) | file | 无内容可总结。 |
| [TurnConfiguration.java](TurnConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [SecureStorageServiceConfiguration.java](SecureStorageServiceConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [ClientCdnConfiguration.java](ClientCdnConfiguration.md) | file | 客户端CDN配置类，支持熔断与重试功能。 |
| [MaxDeviceConfiguration.java](MaxDeviceConfiguration.md) | file | MaxDeviceConfiguration类含字符串number和整数count，提供getter方法。 |
| [FcmConfiguration.java](FcmConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [RedisClusterConfiguration.java](RedisClusterConfiguration.md) | file | Redis集群配置类，支持URI、超时、熔断器和重试，构建容错客户端。 |
| [AppleDeviceCheckConfiguration.java](AppleDeviceCheckConfiguration.md) | file | 内容为空，无法生成概要描述。 |
| [URLSerializationConverter.java](URLSerializationConverter.md) | file | URLSerializationConverter类实现URL到字符串的转换。 |
| [SpamFilterConfiguration.java](SpamFilterConfiguration.md) | file | SpamFilterConfiguration类包含环境属性和构造方法。 |
| [ApnConfiguration.java](ApnConfiguration.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [RemoteConfigConfiguration.java](RemoteConfigConfiguration.md) | file | 无内容提供，无法生成概要描述。 |
| [ReportMessageConfiguration.java](ReportMessageConfiguration.md) | file | 报告配置类设置7天报告和1天计数器的生存时间。 |
| [TurnUriConfiguration.java](TurnUriConfiguration.md) | file | TurnUriConfiguration类管理URI列表、权重和注册ACIs，并提供获取方法。 |
| [GooglePlayBillingConfiguration.java](GooglePlayBillingConfiguration.md) | file | 无内容，无法生成概要描述。 |
| [DirectoryV2ClientConfiguration.java](DirectoryV2ClientConfiguration.md) | file | 输入为空，请提供具体内容以便生成概要描述。 |
| [MessageCacheConfiguration.java](MessageCacheConfiguration.md) | file | MessageCacheConfiguration类配置Redis集群和持久化延迟时间。 |
| [DatadogConfiguration.java](DatadogConfiguration.md) | file | 无内容可总结。 |
| [RetryConfiguration.java](RetryConfiguration.md) | file | RetryConfiguration类配置重试机制，含最大尝试次数和等待时长，提供转换方法。 |
| [RedisConfiguration.java](RedisConfiguration.md) | file | Redis配置类含URI、超时、熔断、重试，支持容错客户端。 |
| [BadgeConfiguration.java](BadgeConfiguration.md) | file | BadgeConfiguration类包含ID、类别、精灵列表、SVG及SVG列表，提供获取和测试方法。 |
| [BraintreeConfiguration.java](BraintreeConfiguration.md) | file | 无内容，无法生成概要。 |
| [KeyTransparencyServiceConfiguration.java](KeyTransparencyServiceConfiguration.md) | file | 无内容可总结。 |
| [CloudflareTurnConfiguration.java](CloudflareTurnConfiguration.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [IssuedReceiptsTableConfiguration.java](IssuedReceiptsTableConfiguration.md) | file | IssuedReceiptsTableConfiguration继承DynamoDbTables.TableWithExpiration，配置生成器和支付提供商最大收据数。 |
| [dynamic](dynamic/_module.md) | package | 动态配置类管理实验、限速、支付、验证码等模块，支持灵活调整。 |
| [secrets](secrets/_module.md) | package | Secret类及其子类用于封装和验证数据，确保安全性和完整性。SecretStore管理密钥，SecretsModule处理秘密数据反序列化。 |


