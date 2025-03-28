# 基础信息

|      |      |
|------|------|
| 名称 | NonEmptyFieldValidator |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/grpc/validators/NonEmptyFieldValidator.java |
| 包名 | org.whispersystems.textsecuregcm.grpc.validators |
| 依赖项 | ['org.whispersystems.textsecuregcm.grpc.validators.ValidatorUtils.invalidArgument', 'com.google.protobuf.ByteString', 'com.google.protobuf.Descriptors', 'com.google.protobuf.GeneratedMessageV3', 'io.grpc.StatusException', 'java.util.Set', 'org.apache.commons.lang3.StringUtils'] |
| 概述说明 | NonEmptyFieldValidator验证字符串、字节数组和重复字段非空。 |

# 说明

NonEmptyFieldValidator用于验证字段是否为空，支持多种数据类型，包括字符串、字节数组以及重复字段。该验证器确保这些字段在提交或处理时不为空，从而保证数据的完整性和有效性。通过这种方式，开发者可以避免因空字段引发的错误或异常，提升系统的稳定性和可靠性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| NonEmptyFieldValidator | class | NonEmptyFieldValidator验证字段非空，支持字符串、字节数组和重复字段。 |



## 类 NonEmptyFieldValidator

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | NonEmptyFieldValidator |
| 说明 | NonEmptyFieldValidator验证字段非空，支持字符串、字节数组和重复字段。 |


### UML类图

```mermaid
classDiagram
    class BaseFieldValidator~T~ {
        <<Abstract>>
        +BaseFieldValidator(String validatorName, Set~Descriptors.FieldDescriptor.Type~ validTypes, MissingOptionalAction missingOptionalAction, boolean isExtensionRequired)
        +~T~ resolveExtensionValue(Object extensionValue) throws StatusException
        +void validateBytesValue(~T~ extensionValue, ByteString fieldValue) throws StatusException
        +void validateStringValue(~T~ extensionValue, String fieldValue) throws StatusException
        +void validateRepeatedField(~T~ extensionValue, Descriptors.FieldDescriptor fd, GeneratedMessageV3 msg) throws StatusException
    }

    class NonEmptyFieldValidator {
        +NonEmptyFieldValidator()
        +Boolean resolveExtensionValue(Object extensionValue) throws StatusException
        +void validateBytesValue(Boolean extensionValue, ByteString fieldValue) throws StatusException
        +void validateStringValue(Boolean extensionValue, String fieldValue) throws StatusException
        +void validateRepeatedField(Boolean extensionValue, Descriptors.FieldDescriptor fd, GeneratedMessageV3 msg) throws StatusException
    }

    BaseFieldValidator~Boolean~ <|-- NonEmptyFieldValidator
```

这段代码定义了一个 `NonEmptyFieldValidator` 类，它继承自泛型类 `BaseFieldValidator<Boolean>`。`NonEmptyFieldValidator` 用于验证字段是否非空，支持字符串、字节数组和重复字段的验证。该类通过重写父类的方法，分别处理不同类型的字段验证逻辑，并在字段为空时抛出异常。


### 内部方法调用关系图

```mermaid
graph TD
    A["类NonEmptyFieldValidator"]
    B["构造方法: NonEmptyFieldValidator()"]
    C["方法: resolveExtensionValue(Object extensionValue)"]
    D["方法: validateBytesValue(Boolean extensionValue, ByteString fieldValue)"]
    E["方法: validateStringValue(Boolean extensionValue, String fieldValue)"]
    F["方法: validateRepeatedField(Boolean extensionValue, Descriptors.FieldDescriptor fd, GeneratedMessageV3 msg)"]
    G["调用: super('nonEmpty', Set.of(Descriptors.FieldDescriptor.Type.STRING, Descriptors.FieldDescriptor.Type.BYTES), MissingOptionalAction.FAIL, true)"]
    H["调用: requireFlagExtension(extensionValue)"]
    I["条件: !fieldValue.isEmpty()"]
    J["抛出异常: invalidArgument('byte array expected to be non-empty')"]
    K["条件: StringUtils.isNotEmpty(fieldValue)"]
    L["抛出异常: invalidArgument('string expected to be non-empty')"]
    M["条件: msg.getRepeatedFieldCount(fd) > 0"]
    N["抛出异常: invalidArgument('repeated field is expected to be non-empty')"]

    A --> B
    B --> G
    A --> C
    C --> H
    A --> D
    D --> I
    I -->|是| B
    I -->|否| J
    A --> E
    E --> K
    K -->|是| B
    K -->|否| L
    A --> F
    F --> M
    M -->|是| B
    M -->|否| N
```

**描述：**  
`NonEmptyFieldValidator` 类继承自 `BaseFieldValidator<Boolean>`，用于验证字段是否非空。构造方法初始化验证器类型和缺失操作策略。`resolveExtensionValue` 方法解析扩展值，`validateBytesValue` 和 `validateStringValue` 方法分别验证字节数组和字符串是否非空，`validateRepeatedField` 方法验证重复字段是否非空。如果字段为空，抛出相应的异常。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| resolveExtensionValue | Boolean | 重写方法，解析扩展值并返回布尔结果。 |
| validateRepeatedField | void | 验证重复字段非空，若为空则抛出异常。 |
| validateStringValue | void | 验证字符串非空，为空则抛出异常。 |
| validateBytesValue | void | 验证字节数组非空，若为空则抛出异常。 |




