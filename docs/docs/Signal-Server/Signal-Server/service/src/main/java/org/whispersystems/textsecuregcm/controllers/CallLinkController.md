# 基础信息

|      |      |
|------|------|
| 名称 | CallLinkController |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/controllers/CallLinkController.java |
| 包名 | org.whispersystems.textsecuregcm.controllers |
| 依赖项 | ['io.dropwizard.auth.Auth', 'io.swagger.v3.oas.annotations.Operation', 'io.swagger.v3.oas.annotations.responses.ApiResponse', 'jakarta.validation.Valid', 'jakarta.validation.constraints.NotNull', 'jakarta.ws.rs.BadRequestException', 'jakarta.ws.rs.POST', 'jakarta.ws.rs.Path', 'jakarta.ws.rs.Produces', 'jakarta.ws.rs.core.MediaType', 'java.time.Instant', 'java.time.temporal.ChronoUnit', 'org.signal.libsignal.protocol.ServiceId', 'org.signal.libsignal.zkgroup.GenericServerSecretParams', 'org.signal.libsignal.zkgroup.InvalidInputException', 'org.signal.libsignal.zkgroup.calllinks.CreateCallLinkCredentialRequest', 'org.whispersystems.textsecuregcm.auth.AuthenticatedDevice', 'org.whispersystems.textsecuregcm.entities.CreateCallLinkCredential', 'org.whispersystems.textsecuregcm.entities.GetCreateCallLinkCredentialsRequest', 'org.whispersystems.textsecuregcm.limits.RateLimiters', 'org.whispersystems.websocket.auth.ReadOnly'] |
| 概述说明 | CallLinkController类处理通话链接凭证生成，支持POST请求，返回JSON凭证，处理错误响应。 |

# 说明

CallLinkController类负责处理创建通话链接凭证的功能。该类包含限速和服务器密钥参数，支持通过POST请求生成凭证，并返回JSON格式的凭证信息。此外，该类还能够处理多种错误响应，确保在异常情况下提供相应的反馈。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| CallLinkController | class | CallLinkController类处理创建通话链接凭证，包含限速和服务器密钥参数，支持POST请求生成凭证，返回JSON格式凭证，处理多种错误响应。 |



## 类 CallLinkController

|      |      |
|------|------|
| 访问范围 | @Path("/v1/call-link");@io.swagger.v3.oas.annotations.tags.Tag(name = "CallLink");public |
| 类型 | class |
| 名称 | CallLinkController |
| 说明 | CallLinkController类处理创建通话链接凭证，包含限速和服务器密钥参数，支持POST请求生成凭证，返回JSON格式凭证，处理多种错误响应。 |


### UML类图

```mermaid
classDiagram
    class CallLinkController {
        -RateLimiters rateLimiters
        -GenericServerSecretParams genericServerSecretParams
        +CallLinkController(RateLimiters rateLimiters, GenericServerSecretParams genericServerSecretParams)
        +CreateCallLinkCredential getCreateAuth(AuthenticatedDevice auth, GetCreateCallLinkCredentialsRequest request) throws RateLimitExceededException
    }

    class RateLimiters {
        +RateLimiter getCreateCallLinkLimiter()
    }

    class GenericServerSecretParams {
        // 类成员和方法未在代码中展示
    }

    class AuthenticatedDevice {
        +Account getAccount()
    }

    class Account {
        +UUID getUuid()
    }

    class GetCreateCallLinkCredentialsRequest {
        +CreateCallLinkCredentialRequest createCallLinkCredentialRequest()
    }

    class CreateCallLinkCredentialRequest {
        +String issueCredential(ServiceId.Aci aci, Instant timestamp, GenericServerSecretParams params)
        +String serialize()
    }

    class CreateCallLinkCredential {
        +CreateCallLinkCredential(String credential, long timestamp)
    }

    class ServiceId.Aci {
        +ServiceId.Aci(UUID uuid)
    }

    class InvalidInputException {
        // 异常类
    }

    class BadRequestException {
        // 异常类
    }

    class RateLimitExceededException {
        // 异常类
    }

    CallLinkController --> RateLimiters : 依赖
    CallLinkController --> GenericServerSecretParams : 依赖
    CallLinkController --> AuthenticatedDevice : 依赖
    CallLinkController --> GetCreateCallLinkCredentialsRequest : 依赖
    CallLinkController --> CreateCallLinkCredentialRequest : 依赖
    CallLinkController --> CreateCallLinkCredential : 依赖
    CallLinkController --> InvalidInputException : 依赖
    CallLinkController --> BadRequestException : 依赖
    CallLinkController --> RateLimitExceededException : 依赖
    AuthenticatedDevice --> Account : 依赖
    GetCreateCallLinkCredentialsRequest --> CreateCallLinkCredentialRequest : 依赖
    CreateCallLinkCredentialRequest --> ServiceId.Aci : 依赖
    CreateCallLinkCredentialRequest --> GenericServerSecretParams : 依赖
```

这段代码定义了一个 `CallLinkController` 类，用于处理创建通话链接凭证的请求。该类依赖于 `RateLimiters` 和 `GenericServerSecretParams` 来执行限流和生成凭证。`getCreateAuth` 方法接收一个已认证的设备和一个请求对象，验证请求并生成凭证。代码中还涉及多个异常类，用于处理不同的错误情况。整体设计体现了分层和依赖注入的思想，确保了代码的可维护性和扩展性。


### 内部方法调用关系图

```mermaid
graph TD
    A["类CallLinkController"]
    B["属性: RateLimiters rateLimiters"]
    C["属性: GenericServerSecretParams genericServerSecretParams"]
    D["构造方法: CallLinkController(RateLimiters rateLimiters, GenericServerSecretParams genericServerSecretParams)"]
    E["方法: CreateCallLinkCredential getCreateAuth(AuthenticatedDevice auth, GetCreateCallLinkCredentialsRequest request)"]
    F["验证: rateLimiters.getCreateCallLinkLimiter().validate(auth.getAccount().getUuid())"]
    G["获取时间戳: Instant truncatedDayTimestamp = Instant.now().truncatedTo(ChronoUnit.DAYS)"]
    H["创建请求: createCallLinkCredentialRequest = new CreateCallLinkCredentialRequest(request.createCallLinkCredentialRequest())"]
    I["异常处理: throw new BadRequestException('Invalid create call link credential request', e)"]
    J["返回结果: return new CreateCallLinkCredential(createCallLinkCredentialRequest.issueCredential(new ServiceId.Aci(auth.getAccount().getUuid()), truncatedDayTimestamp, genericServerSecretParams).serialize(), truncatedDayTimestamp.getEpochSecond())"]

    A --> B
    A --> C
    A --> D
    A --> E
    E --> F
    E --> G
    E --> H
    H --> I
    H --> J
```

这段代码定义了一个名为`CallLinkController`的类，该类用于处理创建通话链接凭证的请求。代码首先通过`rateLimiters`进行速率限制验证，然后获取当前时间戳并创建请求对象。如果请求无效，则抛出异常；否则，返回生成的凭证。整个流程展示了从请求验证到凭证生成的全过程，确保了请求的合法性和安全性。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| genericServerSecretParams | GenericServerSecretParams | 私有不可变的GenericServerSecretParams实例变量。 |
| rateLimiters | RateLimiters | 私有且不可变的限流器实例。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getCreateAuth | CreateCallLinkCredential | 生成通话链接凭证的API，验证请求并返回JSON凭证。 |




