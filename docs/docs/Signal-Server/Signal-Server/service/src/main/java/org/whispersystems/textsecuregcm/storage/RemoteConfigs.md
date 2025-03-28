# 基础信息

|      |      |
|------|------|
| 名称 | RemoteConfigs |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/storage/RemoteConfigs.java |
| 包名 | org.whispersystems.textsecuregcm.storage |
| 依赖项 | ['org.whispersystems.textsecuregcm.util.AttributeValues', 'org.whispersystems.textsecuregcm.util.UUIDUtil', 'software.amazon.awssdk.core.SdkBytes', 'software.amazon.awssdk.services.dynamodb.DynamoDbClient', 'software.amazon.awssdk.services.dynamodb.model.AttributeValue', 'software.amazon.awssdk.services.dynamodb.model.DeleteItemRequest', 'software.amazon.awssdk.services.dynamodb.model.PutItemRequest', 'software.amazon.awssdk.services.dynamodb.model.ScanRequest', 'java.util.Collections', 'java.util.HashMap', 'java.util.List', 'java.util.Map', 'java.util.Set', 'java.util.UUID', 'java.util.stream.Collectors'] |
| 概述说明 | RemoteConfigs类管理DynamoDB远程配置，支持设置、获取和删除操作。 |

# 说明

RemoteConfigs类专门用于管理DynamoDB中的远程配置，提供了设置、获取和删除配置项的功能。该类简化了远程配置的操作，使用户能够高效地管理和维护存储在DynamoDB中的配置数据。通过该类，用户可以轻松地执行配置项的增删改查操作，确保配置数据的一致性和可用性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| RemoteConfigs | class | RemoteConfigs类用于管理DynamoDB中的远程配置，支持设置、获取和删除配置项。 |



## 类 RemoteConfigs

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | RemoteConfigs |
| 说明 | RemoteConfigs类用于管理DynamoDB中的远程配置，支持设置、获取和删除配置项。 |


### UML类图

```mermaid
classDiagram
    class RemoteConfigs {
        -DynamoDbClient dynamoDbClient
        -String tableName
        +RemoteConfigs(DynamoDbClient dynamoDbClient, String tableName)
        +void set(RemoteConfig remoteConfig)
        +List~RemoteConfig~ getAll()
        +void delete(String name)
    }

    class DynamoDbClient {
        <<Interface>>
        +void putItem(PutItemRequest putItemRequest)
        +ScanPaginator scanPaginator(ScanRequest scanRequest)
        +void deleteItem(DeleteItemRequest deleteItemRequest)
    }

    class RemoteConfig {
        +String getName()
        +int getPercentage()
        +Set~UUID~ getUuids()
        +String getDefaultValue()
        +String getValue()
        +String getHashKey()
    }

    class AttributeValues {
        <<Interface>>
        +String getString(Map~String, AttributeValue~ item, String key, String defaultValue)
        +int getInt(Map~String, AttributeValue~ item, String key, int defaultValue)
        +AttributeValue fromString(String value)
        +AttributeValue fromInt(int value)
    }

    class UUIDUtil {
        <<Interface>>
        +ByteBuffer toByteBuffer(UUID uuid)
        +UUID fromByteBuffer(ByteBuffer byteBuffer)
    }

    RemoteConfigs --> DynamoDbClient : 依赖
    RemoteConfigs --> RemoteConfig : 依赖
    RemoteConfigs --> AttributeValues : 依赖
    RemoteConfigs --> UUIDUtil : 依赖
```

**描述：**
`RemoteConfigs` 类负责管理与远程配置相关的操作，包括设置、获取和删除配置。它依赖于 `DynamoDbClient` 与 DynamoDB 数据库进行交互，并使用 `AttributeValues` 和 `UUIDUtil` 工具类来处理数据类型转换。`RemoteConfig` 类表示单个远程配置项，包含名称、百分比、UUID 集合、默认值、值和哈希键等属性。通过 `RemoteConfigs` 类，可以方便地对远程配置进行管理和操作。


### 内部方法调用关系图

```mermaid
graph TD
    A["类RemoteConfigs"]
    B["属性: DynamoDbClient dynamoDbClient"]
    C["属性: String tableName"]
    D["常量: String KEY_NAME = 'N'"]
    E["常量: String ATTR_PERCENTAGE = 'P'"]
    F["常量: String ATTR_UUIDS = 'U'"]
    G["常量: String ATTR_DEFAULT_VALUE = 'D'"]
    H["常量: String ATTR_VALUE = 'V'"]
    I["常量: String ATTR_HASH_KEY = 'H'"]
    J["构造方法: RemoteConfigs(DynamoDbClient dynamoDbClient, String tableName)"]
    K["方法: void set(RemoteConfig remoteConfig)"]
    L["方法: List<RemoteConfig> getAll()"]
    M["方法: void delete(String name)"]
    N["操作: Map<String, AttributeValue> item = new HashMap<>()"]
    O["操作: item.put(KEY_NAME, AttributeValues.fromString(remoteConfig.getName()))"]
    P["操作: item.put(ATTR_PERCENTAGE, AttributeValues.fromInt(remoteConfig.getPercentage()))"]
    Q["操作: if (remoteConfig.getUuids() != null && !remoteConfig.getUuids().isEmpty())"]
    R["操作: List<SdkBytes> uuidByteSets = remoteConfig.getUuids().stream().map(UUIDUtil::toByteBuffer).map(SdkBytes::fromByteBuffer).collect(Collectors.toList())"]
    S["操作: item.put(ATTR_UUIDS, AttributeValue.builder().bs(uuidByteSets).build())"]
    T["操作: if (remoteConfig.getDefaultValue() != null)"]
    U["操作: item.put(ATTR_DEFAULT_VALUE, AttributeValues.fromString(remoteConfig.getDefaultValue()))"]
    V["操作: if (remoteConfig.getValue() != null)"]
    W["操作: item.put(ATTR_VALUE, AttributeValues.fromString(remoteConfig.getValue()))"]
    X["操作: if (remoteConfig.getHashKey() != null)"]
    Y["操作: item.put(ATTR_HASH_KEY, AttributeValues.fromString(remoteConfig.getHashKey()))"]
    Z["操作: dynamoDbClient.putItem(PutItemRequest.builder().tableName(tableName).item(item).build())"]
    AA["操作: return dynamoDbClient.scanPaginator(ScanRequest.builder().tableName(tableName).consistentRead(true).build()).items().stream().map(item -> { ... }).collect(Collectors.toList())"]
    AB["操作: dynamoDbClient.deleteItem(DeleteItemRequest.builder().tableName(tableName).key(Map.of(KEY_NAME, AttributeValues.fromString(name))).build())"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    A --> K
    A --> L
    A --> M
    K --> N
    N --> O
    O --> P
    P --> Q
    Q --> R
    R --> S
    Q --> T
    T --> U
    T --> V
    V --> W
    V --> X
    X --> Y
    Y --> Z
    L --> AA
    M --> AB
```

这段代码定义了一个`RemoteConfigs`类，用于管理远程配置。类中包含三个主要方法：`set`用于设置配置项，`getAll`用于获取所有配置项，`delete`用于删除指定配置项。`set`方法通过构建一个包含配置信息的`Map`对象，并将其插入到DynamoDB表中。`getAll`方法通过扫描DynamoDB表，将结果映射为`RemoteConfig`对象列表。`delete`方法通过指定配置项的名称，从DynamoDB表中删除对应的配置项。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| dynamoDbClient | DynamoDbClient | 私有且不可变的DynamoDbClient实例。 |
| ATTR_DEFAULT_VALUE = "D" | String | 定义私有静态常量ATTR_DEFAULT_VALUE，默认值为"D"。 |
| ATTR_HASH_KEY = "H" | String | 定义了一个私有静态常量字符串ATTR_HASH_KEY，值为"H"。 |
| KEY_NAME = "N" | String | 定义常量KEY_NAME，值为"N"。 |
| ATTR_VALUE = "V" | String | 定义私有静态常量ATTR_VALUE，值为"V"。 |
| ATTR_PERCENTAGE = "P" | String | 定义私有静态常量字符串ATTR_PERCENTAGE为"P"。 |
| ATTR_UUIDS = "U" | String | 定义私有静态常量ATTR_UUIDS，值为"U"。 |
| tableName | String | 私有不可变的字符串变量tableName。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| set | void | 设置远程配置并存储到DynamoDB表。 |
| getAll | List<RemoteConfig> | 从DynamoDB表中扫描数据并映射为RemoteConfig对象列表。 |
| delete | void | 删除指定名称的DynamoDB表项。 |




