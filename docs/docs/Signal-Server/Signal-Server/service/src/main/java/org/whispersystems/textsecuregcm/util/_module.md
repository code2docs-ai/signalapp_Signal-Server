# 基础信息

|      |      |
|------|------|
| 名称 | util |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/util |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.util |
| 概述说明 | HmacUtils类提供HmacSHA256加密，UUIDUtil类处理UUID转换，AbstractPublicKeySerializer序列化公钥，InetAddressRange处理CIDR块，ExactlySizeValidatorForSecretBytes验证长度，Optionals类处理Optional值，ByteArrayBase64UrlAdapter转换字节数组，WeightedRandomSelect实现加权随机选择，EnumMapUtil转换枚举类，CircuitBreakerUtil监控断路器，AsyncTimerUtil记录异步耗时，RegistrationIdValidator验证注册ID，VirtualExecutorServiceProvider管理线程池，DeviceCapabilityAdapter序列化设备能力，ImpossiblePhoneNumberException处理无效电话，Constants定义常量，AttributeValues处理属性值，VirtualThreadPinEventMonitor监控虚拟线程，CertificateUtil管理证书，ManagedAwsCrt控制CRT生命周期，ServiceIdentifierAdapter处理JSON转换，IdentityKeyAdapter序列化IdentityKey，KEMPublicKeyAdapter序列化公钥，ByteArrayAdapter转换字节数组，BackupAuthCredentialAdapter处理Base64编码，Conversions处理数据类型转换，CompletableFutureUtil转换异步操作，DeviceNameByteArrayAdapter序列化设备名，UsernameHashZkProofVerifier验证哈希证明，GoogleApiUtil转换ApiFuture，HeaderUtils处理HTTP头，NoStackTraceException无堆栈跟踪，AbstractPublicKeyDeserializer反序列化公钥，DestinationDeviceValidator验证设备ID，NoStackTraceRuntimeException无堆栈异常，ByteArrayBase64WithPaddingAdapter转换字节数组，Logging模块管理日志，ObsoletePhoneNumberFormatException处理过时电话格式，NonNormalizedPhoneNumberException处理非标准电话，ECPublicKeyAdapter序列化EC公钥，ProfileHelper处理用户头像，HttpServletRequestUtil获取远程地址，ExceptionUtils处理CompletionException，ExactlySizeValidator验证对象大小，ExactlySizeValidatorForCollection验证集合大小，RedisClusterUtil处理Redis集群，HttpUtils处理HTTP响应，InstantAdapter序列化Instant，HostnameUtil获取主机名，BufferingInterceptor优化数据传输，SystemMapper处理JSON和YAML映射，ExactlySizeValidatorForString验证字符串长度，Util提供实用工具，ExactlySizeValidatorForArraysOfByte验证字节数组长度，UserAgent模块处理用户代理信息。 |

# 说明

## 概述
该代码模块是一个功能丰富的工具集，主要涵盖了数据处理、加密、验证、异步操作、异常处理、网络地址管理、序列化与反序列化等多个方面。模块中的类和方法旨在为开发者提供高效、灵活的解决方案，帮助处理复杂的业务逻辑和数据操作。通过这些工具类，开发者可以简化代码实现，提升系统的稳定性、安全性和可维护性。

## 主要业务场景
1. **数据加密与验证**：
   - `HmacUtils`类提供了HmacSHA256加密功能，支持字节数组和字符串的加密，生成加密结果、截断结果以及十六进制字符串，并支持比较。
   - `ExactlySizeValidator`及其子类用于验证对象、字符串、集合、字节数组等的大小是否符合预设要求。
   - `RegistrationIdValidator`用于验证注册ID是否在有效范围内，确保数据的合法性。

2. **数据处理与转换**：
   - `UUIDUtil`类提供了UUID与字节数组、ByteBuffer、ByteString之间的转换功能，满足不同数据类型的互转需求。
   - `ByteArrayBase64UrlAdapter`、`ByteArrayBase64WithPaddingAdapter`等类用于字节数组与Base64编码之间的转换，确保数据在传输和存储时的兼容性。
   - `Conversions`类提供了多种数据类型之间的转换功能，包括整数、字符串与字节数组的互转。

3. **序列化与反序列化**：
   - `AbstractPublicKeySerializer`和`AbstractPublicKeyDeserializer`类分别用于公钥的序列化和反序列化，支持Base64编码和解码。
   - `IdentityKeyAdapter`、`KEMPublicKeyAdapter`、`ECPublicKeyAdapter`等类专门处理不同公钥类型的序列化与反序列化操作。
   - `ServiceIdentifierAdapter`、`DeviceCapabilityAdapter`等类用于处理特定对象的JSON转换。

4. **异步操作与线程管理**：
   - `VirtualExecutorServiceProvider`提供了虚拟线程执行器的功能，支持创建和关闭线程池，并设置超时时间。
   - `AsyncTimerUtil`用于记录异步操作的耗时，帮助开发者分析和优化性能。
   - `CompletableFutureUtil`和`GoogleApiUtil`提供了将`ListenableFuture`和`ApiFuture`转换为`CompletableFuture`的功能，支持更灵活的异步编程。

5. **网络地址与HTTP处理**：
   - `InetAddressRange`类用于处理CIDR块，支持IP地址格式验证、子网掩码生成和地址包含关系检查。
   - `HttpUtils`类提供了HTTP响应成功判断和查询参数生成的功能，简化HTTP请求处理流程。
   - `HeaderUtils`类用于处理HTTP头，支持基本认证、时间戳生成和语言解析。

6. **异常处理与日志管理**：
   - `ImpossiblePhoneNumberException`、`ObsoletePhoneNumberFormatException`等异常类专门处理电话号码格式问题。
   - `NoStackTraceException`和`NoStackTraceRuntimeException`类用于处理不需要堆栈跟踪信息的异常场景，减少内存开销。
   - `ExceptionUtils`类提供了处理`CompletionException`的工具方法，简化异步操作中的异常管理。

7. **随机选择与权重分配**：
   - `WeightedRandomSelect`类支持根据权重进行随机选择，确保选择结果符合权重分配的概率。

8. **工具类与实用方法**：
   - `Util`类提供了电话号码验证、随机选择、睡眠控制、本地化处理等多种实用方法，简化常见任务的处理。
   - `EnumMapUtil`类用于将枚举类转换为`EnumMap`，支持自定义值映射和完整性检查。

该模块的各个类和方法紧密协作，为复杂的业务场景提供了全面的支持，确保了系统的高效运行和数据的准确处理。


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
    logging --> LoggingUnhandledExceptionMapper.java
    logging --> UnknownKeepaliveOptionFilterFactory.java
    logging --> RequestLogEnabledFilterFactory.java
    logging --> UriInfoUtil.java
    logging --> UncaughtExceptionHandler.java
    logging --> RequestLogManager.java
    logging --> UnknownKeepaliveOptionFilter.java
    logging --> RequestLogEnabledFilter.java
    ua --> UnrecognizedUserAgentException.java
    ua --> UserAgent.java
    ua --> UserAgentUtil.java
    ua --> ClientPlatform.java
```

该流程图展示了`util`目录下的所有文件和子目录的层级关系。`util`作为根节点，包含了多个工具类和子目录，如`logging`和`ua`。每个子目录下又包含多个具体的工具类或文件，用于处理不同的功能模块。整个结构清晰地展示了工具类的组织方式。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [ValidBase64URLString.java](ValidBase64URLString.md) | file | 内容为空，无法生成概要描述。 |
| [ValidHexString.java](ValidHexString.md) | file | 信息为空，无法生成概要描述。 |
| [CircuitBreakerUtil.java](CircuitBreakerUtil.md) | file | CircuitBreakerUtil类注册断路器并监控重试机制，记录各类事件。 |
| [Constants.java](Constants.md) | file | 定义常量：METRICS_NAME为"textsecure"，贴图最大301KiB，清单最大10KiB。 |
| [VirtualExecutorServiceProvider.java](VirtualExecutorServiceProvider.md) | file | 提供虚拟线程执行器服务，支持创建和关闭线程池，默认超时5000毫秒。 |
| [BackupAuthCredentialAdapter.java](BackupAuthCredentialAdapter.md) | file | BackupAuthCredentialAdapter类负责Base64编解码、序列化反序列化及错误计数。 |
| [KEMPublicKeyAdapter.java](KEMPublicKeyAdapter.md) | file | KEMPublicKeyAdapter类提供KEMPublicKey的序列化和反序列化功能。 |
| [ByteArrayBase64WithPaddingAdapter.java](ByteArrayBase64WithPaddingAdapter.md) | file | ByteArrayBase64WithPaddingAdapter类实现字节数组与Base64字符串互转。 |
| [AbstractPublicKeyDeserializer.java](AbstractPublicKeyDeserializer.md) | file | 抽象类实现公钥反序列化，处理Base64解码和无效密钥错误。 |
| [HeaderUtils.java](HeaderUtils.md) | file | HeaderUtils类提供HTTP头处理工具，支持认证、时间戳和语言解析。 |
| [ExactlySize.java](ExactlySize.md) | file | 无内容可总结。 |
| [HttpServletRequestUtil.java](HttpServletRequestUtil.md) | file | HttpServletRequestUtil类可获取并处理IPv6格式的远程地址。 |
| [ObsoletePhoneNumberFormatException.java](ObsoletePhoneNumberFormatException.md) | file | ObsoletePhoneNumberFormatException类表示包含区域代码的过时电话号码格式异常。 |
| [RedisClusterUtil.java](RedisClusterUtil.md) | file | RedisClusterUtil类实现集群槽位哈希标签及拓扑变化检测功能。 |
| [SystemMapper.java](SystemMapper.md) | file | SystemMapper类支持JSON和YAML映射，可配置属性过滤和模块注册。 |
| [LinkDeviceToken.java](LinkDeviceToken.md) | file | 信息为空，无法生成概要描述。 |
| [InstantAdapter.java](InstantAdapter.md) | file | InstantAdapter类含EpochSecondSerializer，用于序列化Instant为epoch秒数。 |
| [ExactlySizeValidatorForArraysOfByte.java](ExactlySizeValidatorForArraysOfByte.md) | file | ExactlySizeValidatorForArraysOfByte继承ExactlySizeValidator，重写size方法返回字节数组长度。 |
| [Util.java](Util.md) | file | Util类提供电话号码验证、格式化、随机选择、睡眠和本地化处理等工具方法。 |
| [ExactlySizeValidatorForString.java](ExactlySizeValidatorForString.md) | file | ExactlySizeValidatorForString继承ExactlySizeValidator，重写size方法以返回字符串长度。 |
| [BufferingInterceptor.java](BufferingInterceptor.md) | file | BufferingInterceptor拦截器启用虚拟线程输出流缓冲。 |
| [HostnameUtil.java](HostnameUtil.md) | file | HostnameUtil类用getLocalHostname获取主机名，失败返回unknown。 |
| [HttpUtils.java](HttpUtils.md) | file | HttpUtils类具备HTTP响应成功判断和查询参数字符串生成功能。 |
| [ExactlySizeValidatorForCollection.java](ExactlySizeValidatorForCollection.md) | file | ExactlySizeValidatorForCollection类验证集合大小，返回大小或0。 |
| [ExactlySizeValidator.java](ExactlySizeValidator.md) | file | ExactlySizeValidator类验证对象大小是否符合指定值集。 |
| [ExceptionUtils.java](ExceptionUtils.md) | file | ExceptionUtils类提供处理CompletionException的工具方法，包括解包和包装。 |
| [ProfileHelper.java](ProfileHelper.md) | file | ProfileHelper类管理头像大小、徽章合并、生成头像及身份验证。 |
| [ECPublicKeyAdapter.java](ECPublicKeyAdapter.md) | file | ECPublicKeyAdapter类用于EC公钥的序列化和反序列化操作。 |
| [NonNormalizedPhoneNumberException.java](NonNormalizedPhoneNumberException.md) | file | 非标准化电话号码异常类，含原始与标准化号码。 |
| [NoStackTraceRuntimeException.java](NoStackTraceRuntimeException.md) | file | 无堆栈异常类继承RuntimeException，支持多种构造方式。 |
| [DestinationDeviceValidator.java](DestinationDeviceValidator.md) | file | 验证设备ID、注册ID匹配性及设备列表完整性。 |
| [NoStackTraceException.java](NoStackTraceException.md) | file | 无堆栈跟踪异常类，继承Exception，支持多构造方法。 |
| [GoogleApiUtil.java](GoogleApiUtil.md) | file | GoogleApiUtil类实现ApiFuture到CompletableFuture的转换，支持成功和异常处理。 |
| [UsernameHashZkProofVerifier.java](UsernameHashZkProofVerifier.md) | file | 验证用户名哈希的零知识证明类，使用verifyProof方法进行验证。 |
| [E164.java](E164.md) | file | 无内容提供，无法生成概要描述。 |
| [DeviceNameByteArrayAdapter.java](DeviceNameByteArrayAdapter.md) | file | DeviceNameByteArrayAdapter类处理字节数组的序列化与反序列化，采用Base64编码，记录无效设备名称。 |
| [CompletableFutureUtil.java](CompletableFutureUtil.md) | file | 将ListenableFuture转为CompletableFuture，支持成功与异常处理。 |
| [Conversions.java](Conversions.md) | file | 提供多种数据类型转换和字节数组操作的实用方法。 |
| [ByteArrayAdapter.java](ByteArrayAdapter.md) | file | ByteArrayAdapter类提供Base64编码解码的byte[]序列化和反序列化方法。 |
| [IdentityKeyAdapter.java](IdentityKeyAdapter.md) | file | IdentityKeyAdapter实现序列化和反序列化，采用Base64编码。 |
| [ServiceIdentifierAdapter.java](ServiceIdentifierAdapter.md) | file | ServiceIdentifierAdapter处理ServiceIdentifier及其子类的JSON序列化和反序列化。 |
| [ManagedAwsCrt.java](ManagedAwsCrt.md) | file | ManagedAwsCrt类实现Managed接口，负责CRT的启动和停止管理。 |
| [CertificateUtil.java](CertificateUtil.md) | file | CertificateUtil类提供buildKeyStoreForPem和getCertificate方法，分别用于创建KeyStore和解析PEM证书。 |
| [VirtualThreadPinEventMonitor.java](VirtualThreadPinEventMonitor.md) | file | VirtualThreadPinEventMonitor类监控虚拟线程固定事件，支持启动和停止操作。 |
| [Pair.java](Pair.md) | file | 无内容，无法生成概要描述。 |
| [AttributeValues.java](AttributeValues.md) | file | AttributeValues类提供多种方法用于属性值的转换和提取。 |
| [ImpossiblePhoneNumberException.java](ImpossiblePhoneNumberException.md) | file | 自定义异常类处理无效电话号码。 |
| [DeviceCapabilityAdapter.java](DeviceCapabilityAdapter.md) | file | DeviceCapabilityAdapter类负责设备能力的序列化与反序列化，内置Serializer和Deserializer类。 |
| [RegistrationIdValidator.java](RegistrationIdValidator.md) | file | 验证注册ID是否在有效范围内。 |
| [AsyncTimerUtil.java](AsyncTimerUtil.md) | file | AsyncTimerUtil类用于记录异步操作耗时。 |
| [EnumMapUtil.java](EnumMapUtil.md) | file | EnumMapUtil提供静态方法，支持枚举类转EnumMap，自定义映射和完整性检查。 |
| [WeightedRandomSelect.java](WeightedRandomSelect.md) | file | 加权随机选择类，支持带权重随机选择，确保权重非负且非空。 |
| [ByteArrayBase64UrlAdapter.java](ByteArrayBase64UrlAdapter.md) | file | ByteArrayBase64UrlAdapter类实现字节数组与Base64 URL格式互转。 |
| [Optionals.java](Optionals.md) | file | Optional类的zipWith方法对两个Optional值应用函数，任一为空则返回空。 |
| [ExactlySizeValidatorForSecretBytes.java](ExactlySizeValidatorForSecretBytes.md) | file | ExactlySizeValidatorForSecretBytes继承ExactlySizeValidator，重写size方法返回SecretBytes长度。 |
| [InetAddressRange.java](InetAddressRange.md) | file | InetAddressRange类处理CIDR块，验证地址格式，生成掩码，检查包含关系，实现equals和hashCode方法。 |
| [AbstractPublicKeySerializer.java](AbstractPublicKeySerializer.md) | file | AbstractPublicKeySerializer将公钥序列化为Base64字符串。 |
| [UUIDUtil.java](UUIDUtil.md) | file | UUIDUtil类实现UUID与字节数组、ByteBuffer、ByteString的相互转换。 |
| [HmacUtils.java](HmacUtils.md) | file | HmacUtils类实现HmacSHA256加密，支持多种输入和输出格式，包含结果比较功能。 |
| [ua](ua/_module.md) | package | UnrecognizedUserAgentException处理未识别用户代理异常，UserAgent管理平台信息，UserAgentUtil解析用户代理字符串。 |
| [logging](logging/_module.md) | package | LoggingUnhandledExceptionMapper捕获未处理异常并记录日志。UnknownKeepaliveOptionFilterFactory过滤日志事件。RequestLogEnabledFilterFactory返回HTTP请求日志过滤器。UriInfoUtil拼接URI模板。UncaughtExceptionHandler注册未捕获异常处理器。RequestLogManager管理HTTP请求日志。UnknownKeepaliveOptionFilter过滤未知SO_KEEPALIVE选项。RequestLogEnabledFilter根据状态决定日志记录。 |


