# 基础信息

|      |      |
|------|------|
| 名称 | auth |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/auth |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.auth |
| 概述说明 | 各类用于验证访问权限、管理设备状态、处理认证和凭证，确保系统安全稳定。 |

# 说明

## 概述
该代码模块主要围绕身份验证、访问控制、设备管理以及凭证生成和管理展开，涵盖了多个类用于处理不同场景下的认证和权限管理。这些类通过验证用户凭证、管理设备状态、生成和解析凭证等方式，确保系统的安全性和稳定性。模块中的类共同协作，提供了从用户认证到设备管理的完整解决方案，确保只有经过合法认证的请求和设备能够访问系统资源。

## 主要业务场景
1. **身份验证与访问控制**：
   - `OptionalAccess`：验证账户和设备的访问权限，处理未授权访问和资源不存在的异常情况。
   - `AccountAuthenticator`：处理设备认证流程，验证用户凭证并更新设备的最后访问时间。
   - `BasicAuthorizationHeader`：解析和处理Basic认证头信息，确保认证信息的准确性和安全性。
   - `InvalidAuthorizationHeaderException`：处理无效的授权头信息，确保未经授权的访问被及时拦截。

2. **设备管理与监控**：
   - `IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter`：监控主设备的空闲状态，并在检测到空闲时发送警报，确保设备在使用WebSocket时的活跃状态。
   - `LinkedDeviceRefreshRequirementProvider`：处理设备状态变化，触发设备的重新认证流程，确保设备在系统内的合法性和有效性。
   - `DisconnectionRequestManager`：管理断开连接请求，利用Redis的发布订阅机制进行请求的广播和处理。

3. **凭证生成与管理**：
   - `CloudflareTurnCredentialsManager`：管理TURN凭证，确保TURN服务的有效配置和运行。
   - `ExternalServiceCredentialsGenerator`：生成外部服务凭证，增强凭证的安全性和唯一性。
   - `CertificateGenerator`：生成发送者证书，确保证书的合法性和时效性。

4. **异常处理与日志记录**：
   - `RegistrationLockVerificationManager`：验证账户注册锁的有效性，处理注册锁的过期、缺失或需要验证的情况。
   - `PhoneVerificationTokenManager`：处理手机号码的验证，确保验证流程的稳定性和可靠性。
   - `WebsocketRefreshRequestEventListener`：监听请求事件，处理Websocket连接的刷新和断开，记录设备账户的位移信息。

通过这些业务场景，该模块实现了严格的身份验证和权限管理机制，确保了系统的安全性和稳定性。


### 包内部结构视图

```mermaid
graph TD
    auth --> OptionalAccess.java
    auth --> IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter.java
    auth --> CloudflareTurnCredentialsManager.java
    auth --> WebsocketRefreshRequirementProvider.java
    auth --> Anonymous.java
    auth --> StoredRegistrationLock.java
    auth --> ChangesLinkedDevices.java
    auth --> ExternalServiceCredentialsGenerator.java
    auth --> SaltedTokenHash.java
    auth --> CombinedUnidentifiedSenderAccessKeys.java
    auth --> AccountAndAuthenticatedDeviceHolder.java
    auth --> RegistrationLockVerificationManager.java
    auth --> PhoneVerificationTokenManager.java
    auth --> InvalidAuthorizationHeaderException.java
    auth --> WebsocketRefreshApplicationEventListener.java
    auth --> AccountAuthenticator.java
    auth --> AuthenticatedDevice.java
    auth --> PhoneNumberChangeRefreshRequirementProvider.java
    auth --> BasicAuthorizationHeader.java
    auth --> DisconnectionRequestManager.java
    auth --> ExternalServiceCredentialsSelector.java
    auth --> DisconnectionRequestListener.java
    auth --> WebsocketRefreshRequestEventListener.java
    auth --> ContainerRequestUtil.java
    auth --> CertificateGenerator.java
    auth --> AuthenticatedBackupUser.java
    auth --> ChangesPhoneNumber.java
    auth --> grpc
    auth --> LinkedDeviceRefreshRequirementProvider.java
    auth --> UnidentifiedAccessChecksum.java
    auth --> TurnToken.java
    auth --> GroupSendTokenHeader.java
    auth --> UnidentifiedAccessUtil.java
    auth --> ExternalServiceCredentials.java
    grpc --> RequireAuthenticationInterceptor.java
    grpc --> AuthenticationUtil.java
    grpc --> ProhibitAuthenticationInterceptor.java
    grpc --> AuthenticatedDevice.java
    grpc --> AbstractAuthenticationInterceptor.java
```

该流程图展示了`auth`目录下的文件结构及其层级关系。`auth`目录包含多个Java文件，如`OptionalAccess.java`、`IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter.java`等，同时还包含一个`grpc`子目录。`grpc`子目录下也有多个Java文件，如`RequireAuthenticationInterceptor.java`和`AuthenticationUtil.java`。整体结构清晰，展示了文件与子目录之间的从属关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [AccountAuthenticator.java](AccountAuthenticator.md) | file | AccountAuthenticator类负责设备认证、验证用户凭证及更新访问时间。 |
| [PhoneVerificationTokenManager.java](PhoneVerificationTokenManager.md) | file | PhoneVerificationTokenManager类验证手机号，支持会话ID和恢复密码，处理超时异常。 |
| [AccountAndAuthenticatedDeviceHolder.java](AccountAndAuthenticatedDeviceHolder.md) | file | 信息为空，无法生成概要描述。 |
| [SaltedTokenHash.java](SaltedTokenHash.md) | file | 暂无内容，请提供具体信息以便生成概要。 |
| [ChangesLinkedDevices.java](ChangesLinkedDevices.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [WebsocketRefreshRequirementProvider.java](WebsocketRefreshRequirementProvider.md) | file | 信息为空，无法生成概要描述。 |
| [ExternalServiceCredentialsSelector.java](ExternalServiceCredentialsSelector.md) | file | 验证用户凭证，更新有效凭证并标记无效凭证。 |
| [DisconnectionRequestManager.java](DisconnectionRequestManager.md) | file | DisconnectionRequestManager通过Redis广播处理断开请求，支持监听和ID过滤。 |
| [ExternalServiceCredentials.java](ExternalServiceCredentials.md) | file | 无内容提供，无法生成概要描述。 |
| [GroupSendTokenHeader.java](GroupSendTokenHeader.md) | file | 无内容，无法生成概要描述。 |
| [TurnToken.java](TurnToken.md) | file | 信息为空，无法生成概要描述。 |
| [ChangesPhoneNumber.java](ChangesPhoneNumber.md) | file | 信息为空，无法生成概要描述。 |
| [ContainerRequestUtil.java](ContainerRequestUtil.md) | file | ContainerRequestUtil类用于记录和获取认证账户信息。 |
| [DisconnectionRequestListener.java](DisconnectionRequestListener.md) | file | 无信息提供，无法生成概要描述。 |
| [UnidentifiedAccessUtil.java](UnidentifiedAccessUtil.md) | file | UnidentifiedAccessUtil类验证并计算未识别访问密钥的权限组合。 |
| [UnidentifiedAccessChecksum.java](UnidentifiedAccessChecksum.md) | file | 生成HmacSHA256校验码以验证访问密钥长度是否有效。 |
| [LinkedDeviceRefreshRequirementProvider.java](LinkedDeviceRefreshRequirementProvider.md) | file | LinkedDeviceRefreshRequirementProvider类处理设备状态变化，触发重新认证。 |
| [AuthenticatedBackupUser.java](AuthenticatedBackupUser.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [CertificateGenerator.java](CertificateGenerator.md) | file | 证书生成器类利用私钥、有效期和服务器证书生成发送者证书。 |
| [WebsocketRefreshRequestEventListener.java](WebsocketRefreshRequestEventListener.md) | file | 监听请求，处理Websocket刷新与断连，记录设备位移。 |
| [BasicAuthorizationHeader.java](BasicAuthorizationHeader.md) | file | BasicAuthorizationHeader类解析Basic认证头，提取并验证用户名、设备ID和密码。 |
| [PhoneNumberChangeRefreshRequirementProvider.java](PhoneNumberChangeRefreshRequirementProvider.md) | file | 类实现Websocket刷新，处理电话号码变更。 |
| [AuthenticatedDevice.java](AuthenticatedDevice.md) | file | AuthenticatedDevice类实现Principal接口，包含账户和设备信息，提供获取方法。 |
| [WebsocketRefreshApplicationEventListener.java](WebsocketRefreshApplicationEventListener.md) | file | WebsocketRefreshApplicationEventListener类监听应用事件，依赖WebsocketRefreshRequestEventListener处理请求。 |
| [InvalidAuthorizationHeaderException.java](InvalidAuthorizationHeaderException.md) | file | 无效授权头异常类继承WebApplicationException，处理未授权状态。 |
| [RegistrationLockVerificationManager.java](RegistrationLockVerificationManager.md) | file | 注册锁验证管理器负责验证账户注册锁状态，处理异常情况，记录指标并触发操作。 |
| [CombinedUnidentifiedSenderAccessKeys.java](CombinedUnidentifiedSenderAccessKeys.md) | file | 类CombinedUnidentifiedSenderAccessKeys解析并验证Base64编码的访问密钥。 |
| [ExternalServiceCredentialsGenerator.java](ExternalServiceCredentialsGenerator.md) | file | 工具类生成外部服务凭证，支持用户名派生、时间戳前缀和签名截断。 |
| [StoredRegistrationLock.java](StoredRegistrationLock.md) | file | 存储注册锁类，管理状态、验证及剩余时间计算。 |
| [Anonymous.java](Anonymous.md) | file | Anonymous类解码Base64头信息并转换为字节数组。 |
| [CloudflareTurnCredentialsManager.java](CloudflareTurnCredentialsManager.md) | file | CloudflareTurnCredentialsManager类负责获取并解析Cloudflare的TURN凭证。 |
| [IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter.java](IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter.md) | file | IdlePrimaryDeviceAuthenticatedWebSocketUpgradeFilter类用于检查主设备空闲状态并发警报。 |
| [OptionalAccess.java](OptionalAccess.md) | file | OptionalAccess类负责验证账户和设备权限，处理未授权及未找到异常。 |
| [grpc](grpc/_module.md) | package | RequireAuthenticationInterceptor验证gRPC调用身份，确保通信安全。AuthenticationUtil获取认证设备信息，确保主设备执行。ProhibitAuthenticationInterceptor拒绝未认证请求，保护系统安全。AbstractAuthenticationInterceptor管理客户端连接，控制访问权限。 |


