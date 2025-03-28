# 基础信息

|      |      |
|------|------|
| 名称 | storage |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/storage |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.storage |
| 概述说明 | 多个类管理收据、密钥、消息、账户等，支持DynamoDB、Redis存储，确保数据一致性、安全性和高效操作。 |

# 说明

## 概述

该代码模块是一个基于Signal-Server的服务端存储管理模块，主要用于处理与用户账户、消息、密钥、订阅、设备等相关的数据存储和管理操作。模块的核心功能包括账户管理、消息缓存与持久化、密钥存储与管理、订阅管理、设备认证等。模块通过DynamoDB、Redis等数据库实现高效的数据存储与检索，并支持异步操作和分布式锁机制，确保系统在高并发环境下的性能和可靠性。此外，模块还定义了一系列自定义异常类，用于处理各种业务场景下的错误情况，提高系统的健壮性和可维护性。

## 主要业务场景

1. **账户管理**：通过`AccountsManager`、`Accounts`、`Account`等类，模块提供了账户的创建、更新、删除、设备管理等功能。支持多线程操作和事务处理，确保在高并发环境下的数据一致性和原子性。

2. **消息管理**：`MessagesManager`、`MessagesCache`、`MessagesDynamoDb`等类负责消息的缓存、持久化、查询和删除操作。支持多接收者消息处理和异步操作，确保消息传递的高效性和可靠性。

3. **密钥管理**：`KeysManager`、`SingleUsePreKeyStore`、`RepeatedUseSignedPreKeyStore`等类负责管理各种密钥的存储、检索和删除操作。通过DynamoDB异步客户端实现高效的数据管理，确保密钥的安全性和可用性。

4. **订阅管理**：`SubscriptionManager`、`Subscriptions`等类处理用户的订阅信息，支持订阅的创建、更新、查询和取消操作。通过集中管理订阅生命周期，确保用户订阅状态的一致性和完整性。

5. **设备管理**：`Device`、`DeviceIdDeserializer`、`AccountLockManager`等类负责设备的认证、锁定、过期检测等操作。通过分布式锁机制，确保设备资源的高效利用和并发控制。

6. **异常处理**：模块定义了一系列自定义异常类，如`MessagePersistenceException`、`AccountAlreadyExistsException`、`OptimisticLockRetryLimitExceededException`等，用于处理各种业务场景下的错误情况，确保系统在遇到异常时能够进行适当的错误处理和恢复。

7. **配置管理**：`DynamicConfigurationManager`、`RemoteConfigsManager`等类负责监控和管理系统的动态配置，确保配置的准确性和一致性，支持系统初始化和配置更新。

8. **验证会话管理**：`VerificationSessionManager`、`VerificationSessions`等类负责管理验证会话的创建、更新和查询操作，确保验证会话的有效性和数据的准确维护。

9. **捐赠与支付管理**：`OneTimeDonationsManager`、`PaymentTime`等类处理一次性捐赠和支付时间的管理，确保支付流程的时效性和数据一致性。

10. **数据持久化与缓存**：通过`MessagePersister`、`MessagesCacheGetQueuesToPersistScript`等类，模块支持消息的持久化和缓存管理，确保数据的高效存储和检索，提升系统性能和资源利用率。


### 包内部结构视图

```mermaid
graph TD
    storage --> RedeemedReceiptsManager.java
    storage --> DynamicConfigurationManager.java
    storage --> SingleUseECPreKeyStore.java
    storage --> MessagesCacheGetQueuesToPersistScript.java
    storage --> ClientReleases.java
    storage --> IssuedReceiptsManager.java
    storage --> MessagesCacheGetItemsScript.java
    storage --> ReportMessageDynamoDb.java
    storage --> RepeatedUseECSignedPreKeyStore.java
    storage --> DeviceIdDeserializer.java
    storage --> RefreshingAccountNotFoundException.java
    storage --> VerificationSessions.java
    storage --> MessagesCache.java
    storage --> AccountLockManager.java
    storage --> MessagePersistenceException.java
    storage --> VerificationSessionManager.java
    storage --> ClientPublicKeys.java
    storage --> ClientReleaseManager.java
    storage --> MessagePersister.java
    storage --> AccountsManager.java
    storage --> SubscriptionException.java
    storage --> KeysManager.java
    storage --> UsernameHashNotAvailableException.java
    storage --> MessagesCacheRemoveQueueScript.java
    storage --> MessagesCacheInsertScript.java
    storage --> PhoneNumberIdentifiers.java
    storage --> Subscriptions.java
    storage --> SingleUsePreKeyStore.java
    storage --> ChangeNumberManager.java
    storage --> MessagesCacheInsertSharedMultiRecipientPayloadAndViewsScript.java
    storage --> AccountUtil.java
    storage --> RemoteConfigs.java
    storage --> RepeatedUseSignedPreKeyStore.java
    storage --> AccountPrincipalSupplier.java
    storage --> Profiles.java
    storage --> RepeatedUseKEMSignedPreKeyStore.java
    storage --> RemoteConfigsManager.java
    storage --> AbstractDynamoDbStore.java
    storage --> MessagesManager.java
    storage --> Device.java
    storage --> RegistrationRecoveryPasswordsManager.java
    storage --> SerializedExpireableJsonDynamoStore.java
    storage --> SubscriptionManager.java
    storage --> Accounts.java
    storage --> MessagesDynamoDb.java
    storage --> ClientPublicKeysManager.java
    storage --> devicecheck
    storage --> RemovedMessage.java
    storage --> PaymentTime.java
    storage --> ProfilesManager.java
    storage --> DeviceSpec.java
    storage --> RemoteConfig.java
    storage --> MrmDataMissingException.java
    storage --> OneTimeDonationsManager.java
    storage --> AccountBadge.java
    storage --> ChunkProcessingFailedException.java
    storage --> AccountChangeValidator.java
    storage --> OptimisticLockRetryLimitExceededException.java
    storage --> ContestedOptimisticLockException.java
    storage --> ReportedMessageListener.java
    storage --> ReportMessageManager.java
    storage --> AccountAlreadyExistsException.java
    storage --> ClientRelease.java
    storage --> PersistentTimer.java
    storage --> MessagesCacheUnlockQueueScript.java
    storage --> SingleUseKEMPreKeyStore.java
    storage --> LinkDeviceTokenAlreadyUsedException.java
    storage --> MessagesCacheRemoveByGuidScript.java
    storage --> DeviceCapability.java
    storage --> UsernameReservationNotFoundException.java
    storage --> Account.java
    storage --> PushChallengeDynamoDb.java
    storage --> VersionedProfile.java
    storage --> MessagesCacheRemoveRecipientViewFromMrmDataScript.java
    storage --> SubscriberCredentials.java
    storage --> RegistrationRecoveryPasswords.java
    devicecheck --> TooManyKeysException.java
    devicecheck --> DuplicatePublicKeyException.java
    devicecheck --> DeviceCheckKeyIdNotFoundException.java
    devicecheck --> AppleDeviceChecks.java
    devicecheck --> AppleDeviceCheckTrustAnchor.java
    devicecheck --> AppleDeviceCheckManager.java
    devicecheck --> ChallengeNotFoundException.java
    devicecheck --> DeviceCheckVerificationFailedException.java
    devicecheck --> RequestReuseException.java
```

该流程图展示了Signal-Server项目中`storage`目录下的所有文件和子目录的层级关系。`storage`目录下包含多个Java类文件，以及一个名为`devicecheck`的子目录，该子目录下又包含多个与设备检查相关的异常和工具类。该图清晰地展示了各个文件与目录之间的从属关系，便于理解项目的结构。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [VerificationSessionManager.java](VerificationSessionManager.md) | file | VerificationSessionManager类负责验证会话的增删改查操作。 |
| [MessagesCache.java](MessagesCache.md) | file | MessagesCache类负责消息缓存的插入、删除、获取及多接收者处理，同时监控状态和性能。 |
| [DeviceIdDeserializer.java](DeviceIdDeserializer.md) | file | DeviceIdDeserializer类反序列化字节型设备ID，ID小于PRIMARY_ID时抛出异常。 |
| [MessagesCacheGetItemsScript.java](MessagesCacheGetItemsScript.md) | file | MessagesCacheGetItemsScript类用Lua脚本从Redis集群获取消息列表，支持UUID、设备ID、限制和消息ID参数。 |
| [SingleUseECPreKeyStore.java](SingleUseECPreKeyStore.md) | file | SingleUseECPreKeyStore类继承SingleUsePreKeyStore，处理ECPreKey存储，使用DynamoDB异步客户端和表名初始化，实现预密钥生成与解析。 |
| [Subscriptions.java](Subscriptions.md) | file | Subscriptions类管理用户订阅信息，支持增删改查操作。 |
| [PhoneNumberIdentifiers.java](PhoneNumberIdentifiers.md) | file | 类PhoneNumberIdentifiers管理电话号码标识符，支持PNI查询和设置，使用DynamoDB存储和重试机制。 |
| [MessagesCacheInsertScript.java](MessagesCacheInsertScript.md) | file | MessagesCacheInsertScript类通过Lua脚本和Redis集群异步插入消息并发布事件。 |
| [MessagesCacheRemoveQueueScript.java](MessagesCacheRemoveQueueScript.md) | file | MessagesCacheRemoveQueueScript类从Redis集群移除消息队列，支持批量分页处理。 |
| [UsernameHashNotAvailableException.java](UsernameHashNotAvailableException.md) | file | 自定义异常类用于处理用户名哈希不可用的情况。 |
| [KeysManager.java](KeysManager.md) | file | KeysManager类管理密钥存储，支持插入、删除和查询操作。 |
| [SubscriptionException.java](SubscriptionException.md) | file | SubscriptionException及其子类处理订阅错误，包含错误详情和多种特定异常。 |
| [AccountsManager.java](AccountsManager.md) | file | AccountsManager类负责账户操作、设备管理及Redis交互，支持多线程和事务处理。 |
| [ChangeNumberManager.java](ChangeNumberManager.md) | file | ChangeNumberManager类负责账户号码变更、设备消息验证及更新发送。 |
| [SingleUsePreKeyStore.java](SingleUsePreKeyStore.md) | file | SingleUsePreKeyStore类管理DynamoDB单次预密钥，支持存储、删除和检索。 |
| [ClientPublicKeysManager.java](ClientPublicKeysManager.md) | file | ClientPublicKeysManager管理客户端公钥，支持设置、插入、删除和查找操作。 |
| [SubscriptionManager.java](SubscriptionManager.md) | file | SubscriptionManager负责订阅的支付、取消、更新及信息获取。 |
| [Device.java](Device.md) | file | Device类定义设备属性，支持锁定和过期检测。 |
| [AbstractDynamoDbStore.java](AbstractDynamoDbStore.md) | file | AbstractDynamoDbStore处理DynamoDB批量写入和扫描，支持重试和分批处理。 |
| [AccountPrincipalSupplier.java](AccountPrincipalSupplier.md) | file | AccountPrincipalSupplier实现PrincipalSupplier接口，负责设备认证与账户刷新管理。 |
| [PaymentTime.java](PaymentTime.md) | file | PaymentTime类管理支付时间，支持计算收据过期时间。 |
| [RemovedMessage.java](RemovedMessage.md) | file | 信息为空，无法生成概要描述。 |
| [ReportedMessageListener.java](ReportedMessageListener.md) | file | 无内容可总结。 |
| [AccountChangeValidator.java](AccountChangeValidator.md) | file | 限制账户变更验证类中号码和用户名哈希的修改方式。 |
| [AccountBadge.java](AccountBadge.md) | file | 信息为空，无法生成概要描述。 |
| [MrmDataMissingException.java](MrmDataMissingException.md) | file | MrmDataMissingException继承NoStackTraceRuntimeException，含Type枚举和类型字段。 |
| [DeviceSpec.java](DeviceSpec.md) | file | 输入信息为空，无法生成概要描述。 |
| [SubscriberCredentials.java](SubscriberCredentials.md) | file | 信息为空，无法生成概要描述。 |
| [VersionedProfile.java](VersionedProfile.md) | file | 输入信息为空，请提供具体内容以便生成概要描述。 |
| [Account.java](Account.md) | file | Account类含UUID、电话、设备、密钥，支持用户名、加密、注册锁功能。 |
| [DeviceCapability.java](DeviceCapability.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [SingleUseKEMPreKeyStore.java](SingleUseKEMPreKeyStore.md) | file | SingleUseKEMPreKeyStore继承SingleUsePreKeyStore，管理KEMSignedPreKey，支持DynamoDB操作。 |
| [ClientRelease.java](ClientRelease.md) | file | 信息为空，无法生成概要描述。 |
| [RegistrationRecoveryPasswords.java](RegistrationRecoveryPasswords.md) | file | 注册恢复密码类用于管理用户密码的查找、添加、替换和删除操作。 |
| [MessagesCacheRemoveRecipientViewFromMrmDataScript.java](MessagesCacheRemoveRecipientViewFromMrmDataScript.md) | file | Lua脚本从Redis集群移除收件人视图数据。 |
| [PushChallengeDynamoDb.java](PushChallengeDynamoDb.md) | file | PushChallengeDynamoDb类管理用户推送挑战令牌，支持增删操作。 |
| [UsernameReservationNotFoundException.java](UsernameReservationNotFoundException.md) | file | 自定义异常类用于处理用户名预留未找到的情况。 |
| [MessagesCacheRemoveByGuidScript.java](MessagesCacheRemoveByGuidScript.md) | file | Lua脚本在Redis集群中删除指定消息。 |
| [LinkDeviceTokenAlreadyUsedException.java](LinkDeviceTokenAlreadyUsedException.md) | file | LinkDeviceTokenAlreadyUsedException继承自Exception类。 |
| [MessagesCacheUnlockQueueScript.java](MessagesCacheUnlockQueueScript.md) | file | MessagesCacheUnlockQueueScript类处理Lua脚本和事件参数以解锁队列。 |
| [PersistentTimer.java](PersistentTimer.md) | file | 持久计时器类利用Redis记录时间，支持停止和解析功能。 |
| [AccountAlreadyExistsException.java](AccountAlreadyExistsException.md) | file | AccountAlreadyExistsException继承Exception，记录现有账户信息。 |
| [ReportMessageManager.java](ReportMessageManager.md) | file | ReportMessageManager类管理消息、存储哈希、处理事件并统计报告次数。 |
| [ContestedOptimisticLockException.java](ContestedOptimisticLockException.md) | file | ContestedOptimisticLockException继承NoStackTraceRuntimeException。 |
| [OptimisticLockRetryLimitExceededException.java](OptimisticLockRetryLimitExceededException.md) | file | 乐观锁重试超限异常继承自运行时异常。 |
| [ChunkProcessingFailedException.java](ChunkProcessingFailedException.md) | file | ChunkProcessingFailedException继承Exception，支持消息和异常原因构造。 |
| [OneTimeDonationsManager.java](OneTimeDonationsManager.md) | file | 管理捐赠，处理支付时间与TTL，采用DynamoDB异步客户端。 |
| [RemoteConfig.java](RemoteConfig.md) | file | RemoteConfig类包含名称、百分比、UUID集合、默认值、值和哈希键，提供getter方法。 |
| [ProfilesManager.java](ProfilesManager.md) | file | ProfilesManager管理用户配置，支持同步异步操作，集成Redis缓存和持久化存储。 |
| [MessagesDynamoDb.java](MessagesDynamoDb.md) | file | MessagesDynamoDb类负责DynamoDB消息的存储、查询、删除，支持批量写入、TTL和异步处理。 |
| [Accounts.java](Accounts.md) | file | Accounts类管理账户数据，支持增删改查，使用DynamoDB存储，含用户名、电话、唯一标识等字段。 |
| [SerializedExpireableJsonDynamoStore.java](SerializedExpireableJsonDynamoStore.md) | file | 抽象类实现DynamoDB存储，支持数据插入、更新、查询和删除操作。 |
| [RegistrationRecoveryPasswordsManager.java](RegistrationRecoveryPasswordsManager.md) | file | 管理注册密码恢复，支持验证、存储、删除及UUID与字节数组操作。 |
| [MessagesManager.java](MessagesManager.md) | file | MessagesManager类管理设备消息，支持插入、查询、删除及多接收者处理。 |
| [RemoteConfigsManager.java](RemoteConfigsManager.md) | file | RemoteConfigsManager类管理远程配置，支持获取、设置、删除，配置缓存10秒。 |
| [RepeatedUseKEMSignedPreKeyStore.java](RepeatedUseKEMSignedPreKeyStore.md) | file | RepeatedUseKEMSignedPreKeyStore继承RepeatedUseSignedPreKeyStore，存储KEMSignedPreKey，支持DynamoDb操作。 |
| [Profiles.java](Profiles.md) | file | Profiles类管理用户档案，支持同步异步操作，使用DynamoDB存储数据。 |
| [RepeatedUseSignedPreKeyStore.java](RepeatedUseSignedPreKeyStore.md) | file | 类RepeatedUseSignedPreKeyStore用于存储和查找设备重复使用的预签名密钥，使用DynamoDB异步客户端。 |
| [RemoteConfigs.java](RemoteConfigs.md) | file | RemoteConfigs类管理DynamoDB远程配置，支持设置、获取和删除操作。 |
| [AccountUtil.java](AccountUtil.md) | file | AccountUtil类提供克隆非陈旧账户的静态方法。 |
| [MessagesCacheInsertSharedMultiRecipientPayloadAndViewsScript.java](MessagesCacheInsertSharedMultiRecipientPayloadAndViewsScript.md) | file | Lua脚本插入多接收者消息数据和视图。 |
| [MessagePersister.java](MessagePersister.md) | file | MessagePersister类负责消息持久化，含缓存、管理器、配置，支持多线程处理队列并记录指标。 |
| [ClientReleaseManager.java](ClientReleaseManager.md) | file | ClientReleaseManager负责管理客户端版本，定时刷新并验证版本有效性。 |
| [ClientPublicKeys.java](ClientPublicKeys.md) | file | ClientPublicKeys类管理账户/设备公钥，支持存储、查找、删除，使用DynamoDB异步存储。 |
| [MessagePersistenceException.java](MessagePersistenceException.md) | file | MessagePersistenceException继承Exception，处理消息持久化异常。 |
| [AccountLockManager.java](AccountLockManager.md) | file | AccountLockManager利用DynamoDB实现分布式锁，支持同步异步锁定电话号码，任务完成释放锁。 |
| [VerificationSessions.java](VerificationSessions.md) | file | VerificationSessions类继承SerializedExpireableJsonDynamoStore，管理验证会话。 |
| [RefreshingAccountNotFoundException.java](RefreshingAccountNotFoundException.md) | file | 刷新账户未找到异常类继承运行时异常。 |
| [RepeatedUseECSignedPreKeyStore.java](RepeatedUseECSignedPreKeyStore.md) | file | RepeatedUseECSignedPreKeyStore类存储EC签名预密钥，支持DynamoDB异步操作。 |
| [ReportMessageDynamoDb.java](ReportMessageDynamoDb.md) | file | ReportMessageDynamoDb类管理DynamoDB消息存储、删除及TTL，支持异步操作。 |
| [IssuedReceiptsManager.java](IssuedReceiptsManager.md) | file | IssuedReceiptsManager类管理并发收据发放，防重复并生成唯一标签。 |
| [ClientReleases.java](ClientReleases.md) | file | ClientReleases类通过DynamoDB异步获取客户端发布信息，涵盖平台、版本、发布时间及过期时间。 |
| [MessagesCacheGetQueuesToPersistScript.java](MessagesCacheGetQueuesToPersistScript.md) | file | 类MessagesCacheGetQueuesToPersistScript用Lua脚本获取待持久化队列，支持时间和数量限制。 |
| [DynamicConfigurationManager.java](DynamicConfigurationManager.md) | file | 动态配置管理器监控S3配置更新，解析验证后确保初始化完成。 |
| [RedeemedReceiptsManager.java](RedeemedReceiptsManager.md) | file | RedeemedReceiptsManager类负责管理已兑换收据，支持插入和更新，并确保请求幂等性。 |
| [devicecheck](devicecheck/_module.md) | package | 多个自定义异常类用于处理设备检查错误，包括键数量、公钥重复等，提升代码健壮性。 |


