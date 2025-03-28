# 基础信息

|      |      |
|------|------|
| 名称 | grpc |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/grpc |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.grpc |
| 概述说明 | IdentityTypeUtil类实现gRPC与本地身份类型转换。BackupsGrpcService处理备份认证与凭证管理。KeysAnonymousGrpcService管理匿名密钥请求。KeysGrpcService支持EC和KEM密钥管理。AvatarChangeUtil转换gRPC AvatarChange类型。GroupSendTokenUtil验证群组发送令牌。DevicesGrpcService提供设备管理功能。AccountsGrpcService处理账户操作。ProfileGrpcService管理用户配置文件。 |

# 说明

## 概述

该代码模块主要围绕gRPC通信和身份管理展开，提供了多种功能类和服务类，用于处理身份类型转换、备份管理、密钥管理、设备管理、账户管理、配置文件管理、支付处理、速率限制、验证拦截、凭证管理等功能。模块中的类主要分为以下几类：

1. **身份类型转换**：如`IdentityTypeUtil`，负责gRPC与本地IdentityType之间的相互转换，确保身份信息在系统间传递时的一致性。
2. **备份管理**：如`BackupsGrpcService`和`BackupsAnonymousGrpcService`，负责处理备份认证、凭证管理、备份信息的设置、获取和删除等操作。
3. **密钥管理**：如`KeysGrpcService`和`KeysAnonymousGrpcService`，负责处理预密钥的获取、存储、签名验证以及匿名密钥的管理。
4. **设备管理**：如`DevicesGrpcService`和`DeviceCapabilityUtil`，负责设备信息的获取、移除、命名、推送令牌管理以及设备能力的转换。
5. **账户管理**：如`AccountsGrpcService`和`AccountsAnonymousGrpcService`，负责用户身份验证、账户删除、注册锁管理、用户名管理、账户检查等操作。
6. **配置文件管理**：如`ProfileGrpcService`和`ProfileAnonymousGrpcService`，负责用户配置文件的设置、获取、验证以及用户资料的请求处理。
7. **支付处理**：如`PaymentsGrpcService`，负责货币转换请求的验证和处理。
8. **速率限制**：如`RateLimitUtil`，负责通过远程地址实现速率限制，防止系统过载。
9. **验证拦截**：如`ValidatingInterceptor`和`ErrorMappingInterceptor`，负责验证消息字段的有效性，自动将未知状态转换为gRPC状态。
10. **凭证管理**：如`ExternalServiceCredentialsGrpcService`和`ExternalServiceCredentialsAnonymousGrpcService`，负责外部服务凭证的生成、验证和管理。

## 主要业务场景

该模块适用于以下主要业务场景：

1. **身份信息管理**：通过身份类型转换工具类，确保身份信息在不同系统间的无缝对接和一致性。
2. **备份与恢复**：通过备份管理服务，确保备份任务的安全性和高效性，支持备份ID的设置、收据的兑换以及备份凭证的获取。
3. **密钥管理**：通过密钥管理服务，确保预密钥和匿名密钥的安全性和准确性，支持密钥的获取、存储和验证。
4. **设备管理**：通过设备管理服务，支持设备信息的获取、移除、命名、推送令牌管理以及设备能力的配置。
5. **账户管理**：通过账户管理服务，支持用户身份验证、账户删除、注册锁管理、用户名管理以及账户检查等操作。
6. **配置文件管理**：通过配置文件管理服务，支持用户配置文件的设置、获取、验证以及用户资料的请求处理。
7. **支付处理**：通过支付处理服务，确保货币转换请求的安全性和准确性，支持认证验证和货币转换计算。
8. **速率限制**：通过速率限制工具类，防止系统因过多的请求而过载或遭受恶意攻击。
9. **消息验证**：通过验证拦截器，确保消息字段的有效性，防止无效数据导致系统错误或崩溃。
10. **凭证管理**：通过凭证管理服务，确保外部服务凭证的生成、验证和管理的安全性和可靠性。

该模块通过提供一系列高度集成的服务类和工具类，能够有效支持复杂的gRPC通信和身份管理需求，确保系统的高效性、安全性和稳定性。


### 包内部结构视图

```mermaid
graph TD
    grpc --> IdentityTypeUtil.java
    grpc --> BackupsGrpcService.java
    grpc --> ConvertibleToGrpcStatus.java
    grpc --> KeysAnonymousGrpcService.java
    grpc --> ExternalServiceDefinitions.java
    grpc --> KeysGrpcService.java
    grpc --> AvatarChangeUtil.java
    grpc --> GroupSendTokenUtil.java
    grpc --> StatusConstants.java
    grpc --> DevicesGrpcService.java
    grpc --> DeviceCapabilityUtil.java
    grpc --> ErrorMappingInterceptor.java
    grpc --> PaymentsGrpcService.java
    grpc --> AccountsGrpcService.java
    grpc --> ProfileGrpcService.java
    grpc --> RequestAttributesInterceptor.java
    grpc --> ExternalServiceCredentialsAnonymousGrpcService.java
    grpc --> ExternalServiceCredentialsGrpcService.java
    grpc --> RequestAttributesUtil.java
    grpc --> AccountsAnonymousGrpcService.java
    grpc --> validators
    grpc --> RateLimitUtil.java
    grpc --> ValidatingInterceptor.java
    grpc --> ProfileGrpcHelper.java
    grpc --> BackupsAnonymousGrpcService.java
    grpc --> DeviceIdUtil.java
    grpc --> ServiceIdentifierUtil.java
    grpc --> net
    grpc --> ProfileAnonymousGrpcService.java
    grpc --> KeysGrpcHelper.java
    validators --> ExactlySizeFieldValidator.java
    validators --> BaseFieldValidator.java
    validators --> SizeFieldValidator.java
    validators --> PresentFieldValidator.java
    validators --> EnumSpecifiedFieldValidator.java
    validators --> NonEmptyFieldValidator.java
    validators --> FieldValidator.java
    validators --> RangeFieldValidator.java
    validators --> ValidatorUtils.java
    validators --> Range.java
    validators --> E164FieldValidator.java
    net --> ManagedNioEventLoopGroup.java
    net --> HandshakePattern.java
    net --> ProxyProtocolDetectionHandler.java
    net --> GrpcClientConnectionManager.java
    net --> ApplicationWebSocketCloseReason.java
    net --> NoiseHandshakeException.java
    net --> NoiseIdentityDeterminedEvent.java
    net --> RejectUnsupportedMessagesHandler.java
    net --> WebsocketHandshakeCompleteHandler.java
    net --> NoiseException.java
    net --> EstablishLocalGrpcConnectionHandler.java
    net --> ManagedLocalGrpcServer.java
    net --> HAProxyMessageHandler.java
    net --> NoiseHandler.java
    net --> ErrorHandler.java
    net --> WebSocketOpeningHandshakeHandler.java
    net --> NoiseHandshakeHelper.java
    net --> NoiseAuthenticatedHandler.java
    net --> ProxyHandler.java
    net --> NoiseAnonymousHandler.java
    net --> NoiseWebSocketTunnelServer.java
    net --> ClientAuthenticationException.java
    net --> ManagedDefaultEventLoopGroup.java
```

该流程图展示了Signal-Server项目中`grpc`目录下的文件与子目录的层级关系。`grpc`目录下包含多个Java文件以及两个子目录`validators`和`net`，每个子目录下又包含了多个相关的Java文件。这些文件和目录共同构成了Signal-Server项目中与gRPC服务相关的代码结构。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [KeysGrpcService.java](KeysGrpcService.md) | file | KeysGrpcService管理密钥，支持EC和KEM类型，处理预密钥获取、存储及签名验证。 |
| [ExternalServiceDefinitions.java](ExternalServiceDefinitions.md) | file | 信息为空，无法生成概要描述。 |
| [KeysAnonymousGrpcService.java](KeysAnonymousGrpcService.md) | file | KeysAnonymousGrpcService处理匿名密钥请求，依赖AccountsManager和KeysManager。 |
| [ConvertibleToGrpcStatus.java](ConvertibleToGrpcStatus.md) | file | 无内容提供，无法生成概要描述。 |
| [IdentityTypeUtil.java](IdentityTypeUtil.md) | file | IdentityTypeUtil类实现gRPC与本地IdentityType的互转。 |
| [ProfileGrpcHelper.java](ProfileGrpcHelper.md) | file | ProfileGrpcHelper类负责处理用户档案、徽章和设备能力信息的GRPC接口。 |
| [RequestAttributesUtil.java](RequestAttributesUtil.md) | file | RequestAttributesUtil类提取gRPC请求的客户端语言、远程地址和用户代理信息。 |
| [RequestAttributesInterceptor.java](RequestAttributesInterceptor.md) | file | 拦截器处理gRPC请求，获取地址、语言和用户代理，更新上下文。 |
| [PaymentsGrpcService.java](PaymentsGrpcService.md) | file | PaymentsGrpcService处理货币转换，验证设备并返回结果。 |
| [DevicesGrpcService.java](DevicesGrpcService.md) | file | DevicesGrpcService实现设备管理功能，涵盖获取、移除、命名、设置推送令牌及设备能力。 |
| [KeysGrpcHelper.java](KeysGrpcHelper.md) | file | KeysGrpcHelper类通过getPreKeys获取目标账户预密钥，支持所有或指定设备，返回EC和KEM预密钥。 |
| [ProfileAnonymousGrpcService.java](ProfileAnonymousGrpcService.md) | file | 匿名GRPC服务处理用户资料请求，支持多种密钥凭证获取方式。 |
| [ServiceIdentifierUtil.java](ServiceIdentifierUtil.md) | file | ServiceIdentifierUtil类实现gRPC与服务标识符的互转。 |
| [DeviceIdUtil.java](DeviceIdUtil.md) | file | DeviceIdUtil类验证设备ID有效性，无效则抛出异常。 |
| [BackupsAnonymousGrpcService.java](BackupsAnonymousGrpcService.md) | file | BackupsAnonymousGrpcService类实现备份管理，涵盖认证、CDN凭证、信息获取、刷新、公钥设置、上传、复制、列出和删除媒体等功能。 |
| [ValidatingInterceptor.java](ValidatingInterceptor.md) | file | ValidatingInterceptor实现服务器拦截器，验证消息字段，处理异常并控制调用转发。 |
| [RateLimitUtil.java](RateLimitUtil.md) | file | RateLimitUtil类利用远程地址进行速率控制。 |
| [AccountsAnonymousGrpcService.java](AccountsAnonymousGrpcService.md) | file | AccountsAnonymousGrpcService提供账户检查、哈希查找和链接查找功能。 |
| [ExternalServiceCredentialsGrpcService.java](ExternalServiceCredentialsGrpcService.md) | file | 外部gRPC服务负责生成和验证设备凭证，并实施限流控制。 |
| [ExternalServiceCredentialsAnonymousGrpcService.java](ExternalServiceCredentialsAnonymousGrpcService.md) | file | 匿名Grpc服务，验证凭证，管理账户，生成凭证，检查有效性，返回结果。 |
| [ProfileGrpcService.java](ProfileGrpcService.md) | file | ProfileGrpcService负责用户配置文件的设置、获取和验证操作。 |
| [AccountsGrpcService.java](AccountsGrpcService.md) | file | AccountsGrpcService负责账户操作，涵盖身份验证、删除、注册锁及用户名管理。 |
| [ErrorMappingInterceptor.java](ErrorMappingInterceptor.md) | file | 拦截器自动转换未知状态为gRPC状态，防止服务逻辑冲突。 |
| [DeviceCapabilityUtil.java](DeviceCapabilityUtil.md) | file | DeviceCapabilityUtil类实现gRPC设备能力与本地枚举的相互转换。 |
| [StatusConstants.java](StatusConstants.md) | file | 状态常量类定义无效参数状态及描述。 |
| [GroupSendTokenUtil.java](GroupSendTokenUtil.md) | file | GroupSendTokenUtil类验证群组发送令牌的有效性和服务标识符匹配。 |
| [AvatarChangeUtil.java](AvatarChangeUtil.md) | file | AvatarChangeUtil类负责gRPC AvatarChange类型到内部类型的转换及异常处理。 |
| [BackupsGrpcService.java](BackupsGrpcService.md) | file | BackupsGrpcService负责备份认证与凭证管理，包括设置ID、兑换收据和获取凭证。 |
| [net](net/_module.md) | package | ManagedNioEventLoopGroup继承NioEventLoopGroup，重写stop方法确保优雅关闭。ProxyProtocolDetectionHandler检测代理协议，动态添加解码器。GrpcClientConnectionManager管理gRPC连接，处理认证等信息。NoiseHandshakeException继承Exception，提供详细异常信息。RejectUnsupportedMessagesHandler处理不支持WebSocket帧，释放资源并关闭连接。WebsocketHandshakeCompleteHandler管理客户端公钥，验证代理。NoiseException继承Exception，传递特定错误信息。EstablishLocalGrpcConnectionHandler管理本地gRPC连接，确保安全。ManagedLocalGrpcServer管理本地gRPC服务器，提供启动停止功能。HAProxyMessageHandler处理并丢弃HAProxy消息，清理管道。NoiseHandler处理加密通信，管理握手和传输状态。ErrorHandler处理WebSocket握手异常，记录日志。WebSocketOpeningHandshakeHandler验证WebSocket握手请求，生成响应。NoiseHandshakeHelper管理Noise协议握手，处理密钥和消息。NoiseAuthenticatedHandler验证客户端公钥，确保通信安全。ProxyHandler转发消息，失败时关闭连接。NoiseAnonymousHandler处理匿名通信握手载荷。NoiseWebSocketTunnelServer实现WebSocket隧道，支持TLS和gRPC。ClientAuthenticationException继承Exception，处理客户端认证异常。ManagedDefaultEventLoopGroup继承DefaultEventLoopGroup，重写stop方法优雅关闭。 |
| [validators](validators/_module.md) | package | 验证器类用于字段大小、范围、枚举、非空及E164格式验证，确保数据完整性和准确性。 |


