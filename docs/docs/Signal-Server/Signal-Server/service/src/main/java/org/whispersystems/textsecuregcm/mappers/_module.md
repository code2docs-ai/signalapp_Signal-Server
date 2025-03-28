# 基础信息

|      |      |
|------|------|
| 名称 | mappers |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/mappers |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.mappers |
| 概述说明 | 各类异常映射器将特定异常转换为HTTP响应，确保系统正确处理并反馈错误信息。 |

# 说明

## 概述
该代码模块主要处理各种异常情况，并将其映射为相应的HTTP响应。通过捕获和处理不同类型的异常，模块确保系统能够正确反馈错误信息，提升系统的稳定性和用户体验。模块中的各个类分别负责处理特定的异常类型，如无效WebSocket地址、远程服务拒绝请求、过时电话号码格式、gRPC协议状态码转换、CompletionException、无效电话号码、JSON映射错误、订阅异常、IO异常、设备超限、速率限制、非标准化电话号码等。每个映射器类都会根据异常的具体情况返回相应的HTTP状态码和错误信息，确保客户端能够准确了解请求的处理结果。

## 主要业务场景
1. **无效WebSocket地址处理**：当检测到无效的WebSocket地址时，系统返回HTTP 400响应，提示客户端请求错误。
2. **远程服务拒绝请求处理**：当远程服务返回状态码440时，系统捕获并映射该异常，提供具体的失败原因。
3. **过时电话号码格式处理**：当检测到过时电话号码格式时，系统返回HTTP 499响应，提示客户端请求因格式问题被拒绝。
4. **gRPC协议状态码转换**：将gRPC协议中的状态码转换为HTTP状态码，并生成相应的JSON格式响应，确保gRPC服务与HTTP客户端之间的通信一致性。
5. **CompletionException处理**：通过分析CompletionException的原因，将其映射为相应的响应信息，确保系统在遇到此类异常时能够返回恰当的反馈。
6. **无效电话号码处理**：当检测到无效电话号码时，系统捕获并计数错误，返回相应的错误响应，提高数据的准确性和系统的稳定性。
7. **JSON映射错误处理**：当JSON数据映射到Java对象出现问题时，系统返回相应的HTTP状态码，如400 Bad Request或500 Internal Server Error。
8. **订阅异常处理**：在订阅过程中出现异常时，系统根据异常类型返回相应的HTTP状态码和JSON格式的错误信息，便于问题的诊断和解决。
9. **IO异常处理**：当发生IO异常时，系统记录异常信息并返回相应的HTTP状态码，确保客户端能够准确了解请求的处理结果。
10. **设备超限处理**：当设备数量超过最大限制时，系统返回HTTP 411响应，并提供当前设备数量和最大允许设备数的信息。
11. **速率限制处理**：当请求速率超过限制时，系统返回HTTP 429响应，并包含Retry-After头，提示客户端在指定时间后重试。
12. **非标准化电话号码处理**：当检测到非标准格式的电话号码时，系统记录异常信息并生成相应的错误响应，提高数据处理的准确性和可靠性。
13. **服务器拒绝请求处理**：当服务器拒绝请求时，系统返回HTTP 508响应，确保客户端能够接收到明确的错误信息。

通过这些业务场景的处理，该代码模块确保了系统在各种异常情况下的稳定性和可靠性，提升了用户体验和系统的可维护性。


### 包内部结构视图

```mermaid
graph TD
    mappers --> InvalidWebsocketAddressExceptionMapper.java
    mappers --> RegistrationServiceSenderExceptionMapper.java
    mappers --> ObsoletePhoneNumberFormatExceptionMapper.java
    mappers --> GrpcStatusRuntimeExceptionMapper.java
    mappers --> CompletionExceptionMapper.java
    mappers --> ImpossiblePhoneNumberExceptionMapper.java
    mappers --> JsonMappingExceptionMapper.java
    mappers --> SubscriptionExceptionMapper.java
    mappers --> IOExceptionMapper.java
    mappers --> DeviceLimitExceededExceptionMapper.java
    mappers --> NonNormalizedPhoneNumberResponse.java
    mappers --> RateLimitExceededExceptionMapper.java
    mappers --> NonNormalizedPhoneNumberExceptionMapper.java
    mappers --> ServerRejectedExceptionMapper.java
```

该流程图展示了 `mappers` 文件夹下的所有文件及其层级关系。`mappers` 是根节点，所有 `.java` 文件都是其子节点，表示这些文件都位于 `mappers` 文件夹中。每个文件都是一个独立的节点，清晰地展示了它们与父文件夹的关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [IOExceptionMapper.java](IOExceptionMapper.md) | file | 处理IO异常，记录日志并返回HTTP状态码。 |
| [ImpossiblePhoneNumberExceptionMapper.java](ImpossiblePhoneNumberExceptionMapper.md) | file | 处理无效电话号码异常，计数并返回错误响应。 |
| [ObsoletePhoneNumberFormatExceptionMapper.java](ObsoletePhoneNumberFormatExceptionMapper.md) | file | ObsoletePhoneNumberFormatExceptionMapper类处理异常，记录错误并返回499状态码。 |
| [ServerRejectedExceptionMapper.java](ServerRejectedExceptionMapper.md) | file | ServerRejectedExceptionMapper类将异常映射为508状态码。 |
| [NonNormalizedPhoneNumberExceptionMapper.java](NonNormalizedPhoneNumberExceptionMapper.md) | file | 非标电话号码异常映射器记录异常并返回错误。 |
| [RateLimitExceededExceptionMapper.java](RateLimitExceededExceptionMapper.md) | file | 将RateLimitExceededException转为429响应，含Retry-After头。 |
| [NonNormalizedPhoneNumberResponse.java](NonNormalizedPhoneNumberResponse.md) | file | 类NonNormalizedPhoneNumberResponse包含原始号码和标准化号码，并提供获取方法。 |
| [DeviceLimitExceededExceptionMapper.java](DeviceLimitExceededExceptionMapper.md) | file | 设备超限异常映射器返回411状态码及当前与最大设备数信息。 |
| [SubscriptionExceptionMapper.java](SubscriptionExceptionMapper.md) | file | SubscriptionExceptionMapper处理订阅异常，返回状态码和JSON错误信息。 |
| [JsonMappingExceptionMapper.java](JsonMappingExceptionMapper.md) | file | JsonMappingExceptionMapper根据异常原因返回不同HTTP状态码。 |
| [CompletionExceptionMapper.java](CompletionExceptionMapper.md) | file | CompletionExceptionMapper处理异常，映射原因并返回响应。 |
| [GrpcStatusRuntimeExceptionMapper.java](GrpcStatusRuntimeExceptionMapper.md) | file | Grpc异常映射器转换gRPC状态码为HTTP状态码，返回JSON响应。 |
| [RegistrationServiceSenderExceptionMapper.java](RegistrationServiceSenderExceptionMapper.md) | file | 注册服务异常类处理远程请求失败，返回状态码440及原因。 |
| [InvalidWebsocketAddressExceptionMapper.java](InvalidWebsocketAddressExceptionMapper.md) | file | InvalidWebsocketAddressExceptionMapper类将异常映射为HTTP 400响应。 |


