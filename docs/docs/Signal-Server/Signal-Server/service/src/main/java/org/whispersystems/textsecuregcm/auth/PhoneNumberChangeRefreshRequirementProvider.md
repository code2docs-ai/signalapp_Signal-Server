# 基础信息

|      |      |
|------|------|
| 名称 | PhoneNumberChangeRefreshRequirementProvider |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/auth/PhoneNumberChangeRefreshRequirementProvider.java |
| 包名 | org.whispersystems.textsecuregcm.auth |
| 依赖项 | ['java.util.Collections', 'java.util.List', 'java.util.UUID', 'java.util.stream.Collectors', 'org.glassfish.jersey.server.monitoring.RequestEvent', 'org.whispersystems.textsecuregcm.storage.AccountsManager', 'org.whispersystems.textsecuregcm.util.Pair'] |
| 概述说明 | 类实现Websocket刷新，处理电话号码变更。 |

# 说明

该类实现了Websocket刷新功能，主要用于处理电话号码变更请求。通过Websocket技术，确保在电话号码发生变更时，系统能够实时刷新并更新相关信息，从而保证数据的准确性和一致性。该类的设计旨在高效处理变更请求，确保系统在接收到新的电话号码信息后，能够迅速响应并完成刷新操作。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| PhoneNumberChangeRefreshRequirementProvider | class | 类实现Websocket刷新需求，处理电话号码变更请求。 |



## 类 PhoneNumberChangeRefreshRequirementProvider

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | PhoneNumberChangeRefreshRequirementProvider |
| 说明 | 类实现Websocket刷新需求，处理电话号码变更请求。 |


### UML类图

```mermaid
classDiagram
    class PhoneNumberChangeRefreshRequirementProvider {
        -String ACCOUNT_UUID
        -String INITIAL_NUMBER_KEY
        -AccountsManager accountsManager
        +PhoneNumberChangeRefreshRequirementProvider(AccountsManager accountsManager)
        +void handleRequestFiltered(RequestEvent requestEvent)
        +List~Pair~UUID, Byte~~ handleRequestFinished(RequestEvent requestEvent)
    }

    class AccountsManager {
        +Optional~Account~ getByAccountIdentifier(UUID accountId)
    }

    class RequestEvent {
        +UriInfo getUriInfo()
        +ContainerRequest getContainerRequest()
    }

    class UriInfo {
        +ResourceMethod getMatchedResourceMethod()
    }

    class ResourceMethod {
        +Invocable getInvocable()
    }

    class Invocable {
        +Method getHandlingMethod()
    }

    class Method {
        +ChangesPhoneNumber getAnnotation(Class~ChangesPhoneNumber~ annotationClass)
    }

    class ChangesPhoneNumber {
        <<Interface>>
    }

    class ContainerRequest {
        +void setProperty(String key, Object value)
        +Object getProperty(String key)
    }

    class Account {
        +String e164()
        +UUID accountId()
        +UUID getUuid()
        +String getNumber()
        +List~Device~ getDevices()
    }

    class Device {
        +Byte getId()
    }

    class Pair~T, U~ {
        +Pair(T first, U second)
    }

    PhoneNumberChangeRefreshRequirementProvider --> AccountsManager : 依赖
    PhoneNumberChangeRefreshRequirementProvider --> RequestEvent : 依赖
    RequestEvent --> UriInfo : 依赖
    UriInfo --> ResourceMethod : 依赖
    ResourceMethod --> Invocable : 依赖
    Invocable --> Method : 依赖
    Method --> ChangesPhoneNumber : 依赖
    RequestEvent --> ContainerRequest : 依赖
    AccountsManager --> Account : 依赖
    Account --> Device : 依赖
    PhoneNumberChangeRefreshRequirementProvider --> Pair~UUID, Byte~ : 依赖
```

这段代码展示了`PhoneNumberChangeRefreshRequirementProvider`类如何通过`WebsocketRefreshRequirementProvider`接口处理电话号码变更的刷新需求。它依赖于`AccountsManager`来管理账户信息，并通过`RequestEvent`获取请求的详细信息。类图中清晰地展示了各个类之间的关系和依赖，特别是`PhoneNumberChangeRefreshRequirementProvider`如何与其他类交互以完成其功能。


### 内部方法调用关系图

```mermaid
graph TD
    A["类PhoneNumberChangeRefreshRequirementProvider"]
    B["静态属性: String ACCOUNT_UUID"]
    C["静态属性: String INITIAL_NUMBER_KEY"]
    D["属性: AccountsManager accountsManager"]
    E["构造方法: PhoneNumberChangeRefreshRequirementProvider(AccountsManager accountsManager)"]
    F["方法: void handleRequestFiltered(RequestEvent requestEvent)"]
    G["方法: List<Pair<UUID, Byte>> handleRequestFinished(RequestEvent requestEvent)"]
    H["条件: 检查是否存在ChangesPhoneNumber注解"]
    I["操作: 设置INITIAL_NUMBER_KEY和ACCOUNT_UUID属性"]
    J["条件: 检查initialNumber是否为null"]
    K["操作: 获取账户并过滤设备"]
    L["返回: 返回设备列表或空列表"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    F --> H
    H -->|是| I
    H -->|否| L
    G --> J
    J -->|是| L
    J -->|否| K
    K --> L
```

该流程图描述了`PhoneNumberChangeRefreshRequirementProvider`类的结构和主要方法调用关系。类包含两个静态属性和一个`AccountsManager`属性，并通过构造方法初始化。`handleRequestFiltered`方法检查请求是否包含`ChangesPhoneNumber`注解，若存在则设置相关属性。`handleRequestFinished`方法根据初始号码和账户UUID获取设备列表，若初始号码为空则返回空列表，否则过滤并返回设备列表。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| accountsManager | AccountsManager | 私有且不可变的账户管理器实例。 |
| INITIAL_NUMBER_KEY =      PhoneNumberChangeRefreshRequirementProvider.class.getName() + ".initialNumber" | String | 私有静态常量INITIAL_NUMBER_KEY存储类名与初始号码的拼接字符串。 |
| ACCOUNT_UUID =      PhoneNumberChangeRefreshRequirementProvider.class.getName() + ".accountUuid" | String | 私有静态常量ACCOUNT_UUID存储类名与字符串“.accountUuid”的拼接结果。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| handleRequestFiltered | void | 处理请求时检查注解并设置账户属性。 |
| handleRequestFinished | List<Pair<UUID, Byte>> | 处理请求完成，返回账户UUID与设备ID列表。 |




