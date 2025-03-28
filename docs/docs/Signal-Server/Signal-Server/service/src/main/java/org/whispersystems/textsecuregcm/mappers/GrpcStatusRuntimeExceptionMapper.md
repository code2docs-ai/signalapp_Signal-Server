# 基础信息

|      |      |
|------|------|
| 名称 | GrpcStatusRuntimeExceptionMapper |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/mappers/GrpcStatusRuntimeExceptionMapper.java |
| 包名 | org.whispersystems.textsecuregcm.mappers |
| 依赖项 | ['io.dropwizard.jersey.errors.ErrorMessage', 'io.grpc.StatusRuntimeException', 'jakarta.ws.rs.core.MediaType', 'jakarta.ws.rs.core.Response', 'jakarta.ws.rs.ext.ExceptionMapper', 'jakarta.ws.rs.ext.Provider'] |
| 概述说明 | Grpc异常映射器转换gRPC状态码为HTTP状态码，返回JSON响应。 |

# 说明

Grpc异常映射器的主要功能是将gRPC协议中的状态码转换为HTTP状态码，并在处理过程中生成相应的JSON格式响应。这一机制确保了在gRPC服务与HTTP客户端之间的通信中，状态信息能够被正确理解和处理，从而提升系统的兼容性和用户体验。通过这种映射，开发者可以更方便地调试和监控服务间的交互，同时保持前后端通信的一致性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| GrpcStatusRuntimeExceptionMapper | class | Grpc异常映射器将gRPC状态码转换为HTTP状态码并返回JSON响应。 |



## 类 GrpcStatusRuntimeExceptionMapper

|      |      |
|------|------|
| 访问范围 | @Provider;public |
| 类型 | class |
| 名称 | GrpcStatusRuntimeExceptionMapper |
| 说明 | Grpc异常映射器将gRPC状态码转换为HTTP状态码并返回JSON响应。 |


### UML类图

```mermaid
classDiagram
    class GrpcStatusRuntimeExceptionMapper {
        +Response toResponse(StatusRuntimeException exception)
    }

    class StatusRuntimeException {
        +Status getStatus()
    }

    class Status {
        +Code getCode()
    }

    class Response {
        +Response status(int httpCode)
        +Response entity(Object entity)
        +Response type(MediaType type)
        +Response build()
    }

    class ErrorMessage {
        +ErrorMessage(int httpCode, String message)
    }

    class MediaType {
        <<Interface>>
        +static MediaType APPLICATION_JSON_TYPE
    }

    GrpcStatusRuntimeExceptionMapper --> StatusRuntimeException : 依赖
    StatusRuntimeException --> Status : 依赖
    GrpcStatusRuntimeExceptionMapper --> Response : 依赖
    Response --> ErrorMessage : 依赖
    Response --> MediaType : 依赖
```

这段代码定义了一个`GrpcStatusRuntimeExceptionMapper`类，该类实现了将`StatusRuntimeException`映射为HTTP响应的功能。`toResponse`方法根据异常的状态码生成相应的HTTP状态码，并构建一个包含错误信息的JSON响应。类图中展示了`GrpcStatusRuntimeExceptionMapper`与`StatusRuntimeException`、`Status`、`Response`、`ErrorMessage`和`MediaType`之间的依赖关系。


### 内部方法调用关系图

```mermaid
graph TD
    A["类GrpcStatusRuntimeExceptionMapper"]
    B["实现接口: ExceptionMapper<StatusRuntimeException>"]
    C["重写方法: Response toResponse(StatusRuntimeException exception)"]
    D["获取异常状态码: exception.getStatus().getCode()"]
    E["根据状态码确定HTTP状态码: switch语句"]
    F["创建Response对象: Response.status(httpCode)"]
    G["设置响应实体: .entity(new ErrorMessage(httpCode, exception.getMessage()))"]
    H["设置响应类型: .type(MediaType.APPLICATION_JSON_TYPE)"]
    I["构建并返回Response: .build()"]

    A --> B
    A --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
```

这段代码定义了一个`GrpcStatusRuntimeExceptionMapper`类，实现了`ExceptionMapper<StatusRuntimeException>`接口。它重写了`toResponse`方法，根据传入的`StatusRuntimeException`异常的状态码，映射到相应的HTTP状态码，并构建一个包含错误信息的JSON响应。流程图展示了从获取异常状态码到最终构建并返回响应的完整流程。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| toResponse | Response | 将StatusRuntimeException映射为HTTP状态码并返回JSON格式错误信息。 |




