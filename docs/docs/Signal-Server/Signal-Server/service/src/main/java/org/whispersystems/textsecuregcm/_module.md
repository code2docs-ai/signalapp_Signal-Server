# 基础信息

|      |      |
|------|------|
| 名称 | textsecuregcm |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm |
| 概述说明 | 该代码模块涵盖数据处理、加密、验证、异步操作、异常处理、网络地址管理、序列化与反序列化等功能，提供高效、灵活的解决方案，简化代码实现，提升系统稳定性、安全性和可维护性。 |

# 说明

## 概述

该代码模块是一个功能丰富且高度集成的后端服务模块，涵盖了数据处理、加密、验证、异步操作、异常处理、网络地址管理、序列化与反序列化、推送通知、订阅支付管理、呼叫路由优化、WebSocket通信、Redis集群管理、限流与唯一性估算、身份验证与访问控制、备份管理、任务调度等多个核心功能。模块通过多个子模块和工具类的协同工作，为复杂的业务场景提供了全面的支持，确保系统的高效性、安全性、稳定性和可扩展性。

## 主要业务场景

1. **数据处理与加密**：
   - 提供HmacSHA256加密、UUID与字节数组转换、Base64编码解码等功能，确保数据在传输和存储过程中的安全性和兼容性。
   - 通过`ExactlySizeValidator`、`RegistrationIdValidator`等验证工具，确保数据的合法性和完整性。

2. **推送通知与设备管理**：
   - 通过`FcmSender`、`APNSender`等类，支持通过Firebase和APNs发送推送通知，确保重要通知及时送达。
   - `IdleDeviceNotificationScheduler`等类监控设备状态，优化推送通知的发送策略，提升用户体验。

3. **订阅支付管理**：
   - 集成Google Play Billing、Apple App Store、Stripe、Braintree等支付平台，处理订阅的创建、更新、取消、验证等操作，确保支付流程的准确性和安全性。
   - `SubscriptionCurrencyUtil`等类支持货币转换，确保金额在不同系统之间的一致性。

4. **呼叫路由优化**：
   - `CallRoutingTable`类通过分析IP地址和地理位置信息，选择最优数据中心，优化呼叫路由效率。
   - `CallRoutingTableManager`类实时监控和更新路由表，确保路由信息的准确性和最新性。

5. **WebSocket通信与实时消息传递**：
   - `WebSocketConnection`等类管理WebSocket连接的建立、维护、认证和消息传递，确保实时通信的稳定性和安全性。
   - `ProvisioningConnectListener`等类处理设备间的通信和通知推送，提升系统的实时性和响应能力。

6. **Redis集群管理与限流**：
   - `FaultTolerantRedisClusterClient`等类提供高容错的Redis集群管理，支持发布订阅、连接管理、拓扑变化处理等功能。
   - `DynamicRateLimiter`等类实现限流管理，防止系统过载或遭受恶意攻击。

7. **身份验证与访问控制**：
   - `AccountAuthenticator`等类处理设备认证流程，确保只有经过合法认证的请求和设备能够访问系统资源。
   - `BasicAuthorizationHeader`等类解析和处理认证头信息，确保认证信息的准确性和安全性。

8. **备份管理与任务调度**：
   - `BackupManager`等类管理备份操作的全流程，包括认证、配额管理、上传、删除和恢复功能，确保备份操作的安全性和高效性。
   - `JobScheduler`等类负责调度和处理存储在DynamoDB中的任务，确保任务在指定时间内完成。

9. **异常处理与日志管理**：
   - `NoStackTraceException`等类处理不需要堆栈跟踪信息的异常场景，减少内存开销。
   - `MetricsRequestEventListener`等类监控HTTP请求的路径、方法、状态码等信息，帮助优化请求处理性能。

10. **AWS S3集成与文件上传管理**：
    - `PostPolicyGenerator`等类生成符合AWS S3要求的POST策略，确保文件上传过程的安全性和合规性。
    - `S3ObjectMonitor`类监控S3对象的状态变化，确保数据存储的实时性和可控性。

通过这些业务场景，该代码模块为复杂的业务需求提供了全面的支持，确保了系统的高效运行和数据的准确处理。


### 包内部结构视图

```mermaid
graph TD
    util --> HmacUtils.java
    util --> UUIDUtil.java
    util --> AbstractPublicKeySerializer.java
    util --> InetAddressRange.java
    util --> ExactlySizeValidatorForSecretBytes.java
    util --> ValidHexString.java
    util --> Optionals.java
    util --> ValidBase64URLString.java
    util --> ByteArrayBase64UrlAdapter.java
    util --> WeightedRandomSelect.java
    util --> EnumMapUtil.java
    util --> CircuitBreakerUtil.java
    util --> AsyncTimerUtil.java
    util --> RegistrationIdValidator.java
    util --> VirtualExecutorServiceProvider.java
    util --> DeviceCapabilityAdapter.java
    util --> ImpossiblePhoneNumberException.java
    util --> Constants.java
    util --> AttributeValues.java
    util --> Pair.java
    util --> VirtualThreadPinEventMonitor.java
    util --> CertificateUtil.java
    util --> ManagedAwsCrt.java
    util --> ServiceIdentifierAdapter.java
    util --> IdentityKeyAdapter.java
    util --> KEMPublicKeyAdapter.java
    util --> ByteArrayAdapter.java
    util --> BackupAuthCredentialAdapter.java
    util --> Conversions.java
    util --> CompletableFutureUtil.java
    util --> DeviceNameByteArrayAdapter.java
    util --> E164.java
    util --> UsernameHashZkProofVerifier.java
    util --> GoogleApiUtil.java
    util --> HeaderUtils.java
    util --> NoStackTraceException.java
    util --> AbstractPublicKeyDeserializer.java
    util --> DestinationDeviceValidator.java
    util --> NoStackTraceRuntimeException.java
    util --> ByteArrayBase64WithPaddingAdapter.java
    util --> logging
    logging --> LoggingUnhandledExceptionMapper.java
    logging --> UnknownKeepaliveOptionFilterFactory.java
    logging --> RequestLogEnabledFilterFactory.java
    logging --> UriInfoUtil.java
    logging --> UncaughtExceptionHandler.java
    logging --> RequestLogManager.java
    logging --> UnknownKeepaliveOptionFilter.java
    logging --> RequestLogEnabledFilter.java
    util --> ObsoletePhoneNumberFormatException.java
    util --> NonNormalizedPhoneNumberException.java
    util --> ECPublicKeyAdapter.java
    util --> ProfileHelper.java
    util --> HttpServletRequestUtil.java
    util --> ExactlySize.java
    util --> ExceptionUtils.java
    util --> ExactlySizeValidator.java
    util --> ExactlySizeValidatorForCollection.java
    util --> RedisClusterUtil.java
    util --> HttpUtils.java
    util --> InstantAdapter.java
    util --> LinkDeviceToken.java
    util --> HostnameUtil.java
    util --> BufferingInterceptor.java
    util --> SystemMapper.java
    util --> ExactlySizeValidatorForString.java
    util --> Util.java
    util --> ExactlySizeValidatorForArraysOfByte.java
    util --> ua
    ua --> UnrecognizedUserAgentException.java
    ua --> UserAgent.java
    ua --> UserAgentUtil.java
    ua --> ClientPlatform.java
```

该流程图展示了`util`目录下的文件及其子目录`logging`和`ua`的结构。`util`目录包含多个工具类文件，如`HmacUtils.java`、`UUIDUtil.java`等，同时还包含两个子目录`logging`和`ua`，分别用于处理日志记录和用户代理相关的功能。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [WhisperServerService.java](WhisperServerService.md) | file | WhisperServerService是基于Dropwizard的应用，负责配置、命令、监控及集成多种服务。 |
| [WhisperServerConfiguration.java](WhisperServerConfiguration.md) | file | WhisperServer配置类含TLS、AWS、支付、缓存、CDN、消息推送等关键组件。 |
| [websocket](websocket/_module.md) | package | ProvisioningConnectListener管理WebSocket连接，处理消息传递和异常。WebSocketAccountAuthenticator验证请求头认证信息。InvalidWebsocketAddressException处理无效地址异常。WebSocketConnection管理消息发送接收和错误处理。AuthenticatedConnectListener处理认证设备间通信和通知推送。 |
| [s3](s3/_module.md) | package | PostPolicyGenerator生成S3 POST策略，S3ObjectMonitor监控对象变化，PolicySigner生成AWS签名确保安全。 |
| [spam](spam/_module.md) | package | 输入内容为空，无法生成总结描述。请提供具体信息。 |
| [captcha](captcha/_module.md) | package | ShortCodeExpander类解析短码，返回结果。注册验证码管理器评估验证码有效性。CaptchaChecker验证验证码准确性。评估结果类存储验证数据，确保准确性。 |
| [http](http/_module.md) | package | FaultTolerantHttpClient类实现容错HTTP客户端，支持重试、断路器和负载均衡。 |
| [workers](workers/_module.md) | package | 多个命令类实现删除、推送、持久化等功能，支持并发控制、模拟运行和分段扫描，确保系统稳定性和数据安全。 |
| [backup](backup/_module.md) | package | 公共密钥冲突异常继承自IO异常，处理密钥操作冲突。Cdn3BackupCredentialGenerator生成CDN备份凭证。BackupManager管理备份操作，支持认证、配额、上传、删除和恢复。BackupsDb管理备份数据库操作。BackupAuthManager管理备份认证。Cdn3RemoteStorageManager管理远程存储操作。 |
| [auth](auth/_module.md) | package | 各类用于验证访问权限、管理设备状态、处理认证和凭证，确保系统安全稳定。 |
| [badges](badges/_module.md) | package | ProfileBadgeConverter类实现多语言徽章转换和动态生成功能。 |
| [providers](providers/_module.md) | package | Redis集群健康检查类验证节点连通性，确保集群稳定。多接收者消息处理类支持5000接收者和256KiB消息，提升传递效率。 |
| [mappers](mappers/_module.md) | package | 各类异常映射器将特定异常转换为HTTP响应，确保系统正确处理并反馈错误信息。 |
| [grpc](grpc/_module.md) | package | IdentityTypeUtil类实现gRPC与本地身份类型转换。BackupsGrpcService处理备份认证与凭证管理。KeysAnonymousGrpcService管理匿名密钥请求。KeysGrpcService支持EC和KEM密钥管理。AvatarChangeUtil转换gRPC AvatarChange类型。GroupSendTokenUtil验证群组发送令牌。DevicesGrpcService提供设备管理功能。AccountsGrpcService处理账户操作。ProfileGrpcService管理用户配置文件。 |
| [experiment](experiment/_module.md) | package | 推送通知实验类管理设备状态，记录时间，优化发送策略，提升用户满意度。 |
| [currency](currency/_module.md) | package | CoinGeckoClient获取加密货币价格，FixerClient获取汇率，CurrencyConversionManager管理货币转换。 |
| [keytransparency](keytransparency/_module.md) | package | KeyTransparencyServiceClient管理客户端证书并支持gRPC通信。 |
| [storage](storage/_module.md) | package | 多个类管理收据、密钥、消息、账户等，支持DynamoDB、Redis存储，确保数据一致性、安全性和高效操作。 |
| [gcp](gcp/_module.md) | package | 生成POST请求类含域名、邮箱、最大字节数和路径前缀，确保请求规范完整。签名工具使用RSA私钥，支持SHA256WITHRSA算法，验证请求合法性。封装类包含路径、查询参数等关键信息，确保请求准确。 |
| [scheduler](scheduler/_module.md) | package | 根据时区或创建时间确定通知发送时间，JobScheduler管理任务执行和并发处理。 |
| [entities](entities/_module.md) | package | 输入内容为空，无法进行总结描述。请提供具体内容以便生成相应的总结。 |
| [limits](limits/_module.md) | package | Signal-Server限流器类管理请求速率，确保系统稳定性和安全性。 |
| [redis](redis/_module.md) | package | 处理Redis集群拓扑变化，增强容错性和稳定性。 |
| [securevaluerecovery](securevaluerecovery/_module.md) | package | SecureValueRecovery2Client类用于安全删除备份数据，支持异步操作和HTTP通信。SecureValueRecoveryException处理安全值恢复错误，包含状态码和构造方法。 |
| [registration](registration/_module.md) | package | 各类异常处理注册服务中的传输、验证、欺诈等问题，确保系统安全可靠。 |
| [attachments](attachments/_module.md) | package | TusAttachmentGenerator生成附件描述符，GcsAttachmentGenerator处理GCS附件描述。 |
| [configuration](configuration/_module.md) | package | IssuedReceiptsTableConfiguration类配置收据生成规则和支付提供商最大收据数，管理过期收据。 |
| [filters](filters/_module.md) | package | RestDeprecationFilter过滤REST请求，RequestStatisticsFilter记录请求统计，ExternalRequestFilter拦截gRPC和HTTP请求，RemoteAddressFilter处理远程地址，RemoteDeprecationFilter检查客户端版本，TimestampResponseFilter设置响应时间戳。 |
| [metrics](metrics/_module.md) | package | 各类功能涵盖请求监控、内存管理、日志传输、性能分析、消息度量等，助力系统优化与稳定性提升。 |
| [controllers](controllers/_module.md) | package | Signal-Server控制器模块，涵盖附件、账户、限流、设备、备份、密钥、支付等功能，确保系统安全性和高效性。 |
| [identity](identity/_module.md) | package | 输入内容为空，无法生成总结描述。请提供具体信息。 |
| [securestorage](securestorage/_module.md) | package | SecureStorageClient类用于安全删除数据，支持认证、HTTP请求和异常处理。SecureStorageException继承RuntimeException，提供带消息的构造函数。 |
| [subscriptions](subscriptions/_module.md) | package | 多个类处理订阅支付流程，涵盖验证、取消、收据获取及货币转换等功能。 |
| [jetty](jetty/_module.md) | package | JettyHttpConfigurationCustomizer类禁止远程异步错误通知。 |
| [push](push/_module.md) | package | 空闲设备通知调度器管理设备状态并发送推送通知，提升管理效率和用户体验。 |
| [calls](calls/_module.md) | package | CallRoutingTable类根据IP和地理位置优化呼叫路由，支持IPv4/IPv6。 |
| [util](util/_module.md) | package | HmacUtils类提供HmacSHA256加密，UUIDUtil类处理UUID转换，AbstractPublicKeySerializer序列化公钥，InetAddressRange处理CIDR块，ExactlySizeValidatorForSecretBytes验证长度，Optionals类处理Optional值，ByteArrayBase64UrlAdapter转换字节数组，WeightedRandomSelect实现加权随机选择，EnumMapUtil转换枚举类，CircuitBreakerUtil监控断路器，AsyncTimerUtil记录异步耗时，RegistrationIdValidator验证注册ID，VirtualExecutorServiceProvider管理线程池，DeviceCapabilityAdapter序列化设备能力，ImpossiblePhoneNumberException处理无效电话，Constants定义常量，AttributeValues处理属性值，VirtualThreadPinEventMonitor监控虚拟线程，CertificateUtil管理证书，ManagedAwsCrt控制CRT生命周期，ServiceIdentifierAdapter处理JSON转换，IdentityKeyAdapter序列化IdentityKey，KEMPublicKeyAdapter序列化公钥，ByteArrayAdapter转换字节数组，BackupAuthCredentialAdapter处理Base64编码，Conversions处理数据类型转换，CompletableFutureUtil转换异步操作，DeviceNameByteArrayAdapter序列化设备名，UsernameHashZkProofVerifier验证哈希证明，GoogleApiUtil转换ApiFuture，HeaderUtils处理HTTP头，NoStackTraceException无堆栈跟踪，AbstractPublicKeyDeserializer反序列化公钥，DestinationDeviceValidator验证设备ID，NoStackTraceRuntimeException无堆栈异常，ByteArrayBase64WithPaddingAdapter转换字节数组，Logging模块管理日志，ObsoletePhoneNumberFormatException处理过时电话格式，NonNormalizedPhoneNumberException处理非标准电话，ECPublicKeyAdapter序列化EC公钥，ProfileHelper处理用户头像，HttpServletRequestUtil获取远程地址，ExceptionUtils处理CompletionException，ExactlySizeValidator验证对象大小，ExactlySizeValidatorForCollection验证集合大小，RedisClusterUtil处理Redis集群，HttpUtils处理HTTP响应，InstantAdapter序列化Instant，HostnameUtil获取主机名，BufferingInterceptor优化数据传输，SystemMapper处理JSON和YAML映射，ExactlySizeValidatorForString验证字符串长度，Util提供实用工具，ExactlySizeValidatorForArraysOfByte验证字节数组长度，UserAgent模块处理用户代理信息。 |


