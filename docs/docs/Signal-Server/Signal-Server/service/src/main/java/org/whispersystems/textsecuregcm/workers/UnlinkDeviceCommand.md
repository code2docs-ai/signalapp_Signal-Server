# 基础信息

|      |      |
|------|------|
| 名称 | UnlinkDeviceCommand |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/workers/UnlinkDeviceCommand.java |
| 包名 | org.whispersystems.textsecuregcm.workers |
| 依赖项 | ['com.fasterxml.jackson.databind.DeserializationFeature', 'io.dropwizard.core.Application', 'io.dropwizard.core.cli.EnvironmentCommand', 'io.dropwizard.core.setup.Environment', 'java.util.List', 'java.util.UUID', 'net.sourceforge.argparse4j.impl.Arguments', 'net.sourceforge.argparse4j.inf.Namespace', 'net.sourceforge.argparse4j.inf.Subparser', 'org.whispersystems.textsecuregcm.WhisperServerConfiguration', 'org.whispersystems.textsecuregcm.storage.Account', 'org.whispersystems.textsecuregcm.storage.Device'] |
| 概述说明 | UnlinkDeviceCommand类解绑设备并清除消息，需设备ID和账户UUID。 |

# 说明

UnlinkDeviceCommand类的主要功能是解绑设备并清除相关消息。为了执行这一操作，需要提供两个关键参数：设备ID和账户UUID。设备ID用于标识要解绑的具体设备，而账户UUID则用于确认与该设备关联的用户账户。通过这两个参数，该类能够准确地找到并处理需要解绑的设备，同时清除与该设备相关的消息，确保解绑过程彻底且无遗留问题。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| UnlinkDeviceCommand | class | UnlinkDeviceCommand类用于解绑设备并清除消息，需提供设备ID和账户UUID。 |



## 类 UnlinkDeviceCommand

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | UnlinkDeviceCommand |
| 说明 | UnlinkDeviceCommand类用于解绑设备并清除消息，需提供设备ID和账户UUID。 |


### UML类图

```mermaid
classDiagram
    class AbstractCommandWithDependencies {
        +AbstractCommandWithDependencies(Application~WhisperServerConfiguration, Environment~ application, String name, String description)
        +void configure(Subparser subparser)
        +void run(Environment environment, Namespace namespace, WhisperServerConfiguration configuration, CommandDependencies deps)
    }

    class UnlinkDeviceCommand {
        +UnlinkDeviceCommand()
        +void configure(Subparser subparser)
        +void run(Environment environment, Namespace namespace, WhisperServerConfiguration configuration, CommandDependencies deps)
    }

    class Application~T, U~ {
        <<Interface>>
        +void run(T configuration, U environment)
    }

    class WhisperServerConfiguration {
    }

    class Environment {
    }

    class Subparser {
        +void addArgument(String... arguments)
    }

    class Namespace {
        +String getString(String key)
        +List~Byte~ getList(String key)
    }

    class CommandDependencies {
        +AccountsManager accountsManager()
    }

    class AccountsManager {
        +Optional~Account~ getByAccountIdentifier(UUID aci)
        +CompletableFuture~Void~ removeDevice(Account account, byte deviceId)
    }

    class Account {
    }

    class Device {
        +static final byte PRIMARY_ID
    }

    UnlinkDeviceCommand --|> AbstractCommandWithDependencies : 继承
    AbstractCommandWithDependencies --> Application~WhisperServerConfiguration, Environment~ : 依赖
    UnlinkDeviceCommand --> Subparser : 依赖
    UnlinkDeviceCommand --> Namespace : 依赖
    UnlinkDeviceCommand --> WhisperServerConfiguration : 依赖
    UnlinkDeviceCommand --> CommandDependencies : 依赖
    CommandDependencies --> AccountsManager : 依赖
    AccountsManager --> Account : 依赖
    UnlinkDeviceCommand --> Device : 依赖
```

### 描述
`UnlinkDeviceCommand` 类继承自 `AbstractCommandWithDependencies`，用于执行解绑设备的命令。它通过配置命令行参数（如设备ID和账户UUID）来执行解绑操作。该类依赖于 `Subparser`、`Namespace`、`WhisperServerConfiguration` 和 `CommandDependencies` 等类，并通过 `AccountsManager` 类来管理账户和设备。`UnlinkDeviceCommand` 在执行时会检查设备ID，确保不会删除主设备，并逐个移除指定设备。


### 内部方法调用关系图

```mermaid
graph TD
    A["类UnlinkDeviceCommand"]
    B["构造方法: UnlinkDeviceCommand()"]
    C["方法: configure(Subparser subparser)"]
    D["方法: run(Environment environment, Namespace namespace, WhisperServerConfiguration configuration, CommandDependencies deps)"]
    E["内部调用: super.configure(subparser)"]
    F["添加参数: -d/--deviceId"]
    G["添加参数: -u/--uuid"]
    H["获取UUID: UUID.fromString(namespace.getString('uuid').trim())"]
    I["获取设备ID列表: namespace.getList('deviceIds')"]
    J["获取账户: deps.accountsManager().getByAccountIdentifier(aci)"]
    K["检查是否为Primary设备: deviceIds.contains(Device.PRIMARY_ID)"]
    L["抛出异常: IllegalArgumentException('cannot delete primary device')"]
    M["遍历设备ID: for (byte deviceId : deviceIds)"]
    N["输出设备移除信息: System.out.format('Removing device %s::%d', aci, deviceId)"]
    O["移除设备: deps.accountsManager().removeDevice(account, deviceId).join()"]

    A --> B
    A --> C
    A --> D
    C --> E
    C --> F
    C --> G
    D --> H
    D --> I
    D --> J
    D --> K
    K --> L
    D --> M
    M --> N
    M --> O
```

这段代码描述了一个用于解除设备链接的命令类 `UnlinkDeviceCommand`。它通过命令行参数接收设备ID和账户UUID，检查是否为Primary设备，然后遍历设备ID列表，逐个移除设备并输出移除信息。代码结构清晰，包含了参数配置、异常处理和设备移除的逻辑。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| configure | void | 配置命令行参数，包含设备ID和账户UUID，均为必填项。 |
| run | void | 从命名空间获取UUID和设备ID，检查账户存在，删除非主设备。 |




