# 基础信息

|      |      |
|------|------|
| 名称 | UserAgentTagUtil |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/metrics/UserAgentTagUtil.java |
| 包名 | org.whispersystems.textsecuregcm.metrics |
| 依赖项 | ['io.micrometer.core.instrument.Tag', 'java.util.List', 'java.util.Optional', 'org.whispersystems.textsecuregcm.storage.ClientReleaseManager', 'org.whispersystems.textsecuregcm.util.ua.UnrecognizedUserAgentException', 'org.whispersystems.textsecuregcm.util.ua.UserAgent', 'org.whispersystems.textsecuregcm.util.ua.UserAgentUtil'] |
| 概述说明 | UserAgentTagUtil类解析用户代理字符串，生成平台、版本和libsignal标签。 |

# 说明

UserAgentTagUtil类的主要功能是解析用户代理字符串，并从中提取平台、版本和libsignal标签信息。通过解析用户代理字符串，该类能够生成相关的标签，帮助识别用户所使用的平台及其版本，以及libsignal的相关信息。这一过程对于理解和处理用户代理数据至关重要，尤其是在需要根据用户代理信息进行特定操作或分析的场景中。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| UserAgentTagUtil | class | UserAgentTagUtil类用于解析用户代理字符串，生成平台、版本和libsignal标签。 |



## 类 UserAgentTagUtil

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | UserAgentTagUtil |
| 说明 | UserAgentTagUtil类用于解析用户代理字符串，生成平台、版本和libsignal标签。 |


### UML类图

```mermaid
classDiagram
    class UserAgentTagUtil {
        +String PLATFORM_TAG
        +String VERSION_TAG
        +String LIBSIGNAL_TAG
        -UserAgentTagUtil()
        +Tag getPlatformTag(String userAgentString)
        +Optional~Tag~ getClientVersionTag(String userAgentString, ClientReleaseManager clientReleaseManager)
        +List~Tag~ getLibsignalAndPlatformTags(String userAgentString)
    }

    class UserAgentUtil {
        <<Interface>>
        +UserAgent parseUserAgentString(String userAgentString)
    }

    class UserAgent {
        +String getPlatform()
        +String getVersion()
        +Optional~String~ getAdditionalSpecifiers()
    }

    class ClientReleaseManager {
        <<Interface>>
        +boolean isVersionActive(String platform, String version)
    }

    class Tag {
        +Tag of(String key, String value)
    }

    UserAgentTagUtil --> UserAgentUtil : 依赖
    UserAgentTagUtil --> ClientReleaseManager : 依赖
    UserAgentTagUtil --> Tag : 依赖
    UserAgentUtil --> UserAgent : 依赖
```

这段代码定义了一个 `UserAgentTagUtil` 工具类，用于从用户代理字符串中提取平台、客户端版本和 libsignal 相关的标签。该类依赖于 `UserAgentUtil` 来解析用户代理字符串，`ClientReleaseManager` 来验证客户端版本是否活跃，以及 `Tag` 类来创建标签。代码通过捕获 `UnrecognizedUserAgentException` 异常来处理无法识别的用户代理字符串，确保在异常情况下返回默认值或空值。


### 内部方法调用关系图

```mermaid
graph TD
    A["类UserAgentTagUtil"]
    B["常量: PLATFORM_TAG"]
    C["常量: VERSION_TAG"]
    D["常量: LIBSIGNAL_TAG"]
    E["私有构造方法: UserAgentTagUtil()"]
    F["方法: getPlatformTag(String userAgentString)"]
    G["方法: getClientVersionTag(String userAgentString, ClientReleaseManager clientReleaseManager)"]
    H["方法: getLibsignalAndPlatformTags(String userAgentString)"]
    I["调用: UserAgentUtil.parseUserAgentString(userAgentString)"]
    J["调用: getPlatform().name().toLowerCase()"]
    K["异常处理: UnrecognizedUserAgentException"]
    L["返回: Tag.of(PLATFORM_TAG, platform)"]
    M["调用: clientReleaseManager.isVersionActive(platform, version)"]
    N["返回: Optional.of(Tag.of(VERSION_TAG, version))"]
    O["返回: Optional.empty()"]
    P["调用: getAdditionalSpecifiers().map(additionalSpecifiers -> additionalSpecifiers.contains('libsignal')).orElse(false)"]
    Q["返回: List.of(Tag.of(PLATFORM_TAG, platform), Tag.of(LIBSIGNAL_TAG, String.valueOf(libsignal)))"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    F --> I
    F --> J
    F --> K
    F --> L
    G --> I
    G --> M
    G --> N
    G --> O
    H --> I
    H --> P
    H --> Q
```

这段代码定义了一个`UserAgentTagUtil`工具类，用于解析用户代理字符串并生成相应的标签。类中包含三个静态方法：`getPlatformTag`用于获取平台标签，`getClientVersionTag`用于获取客户端版本标签，`getLibsignalAndPlatformTags`用于获取平台和libsignal标签。每个方法都通过`UserAgentUtil.parseUserAgentString`解析用户代理字符串，并根据解析结果生成相应的标签。代码还处理了`UnrecognizedUserAgentException`异常，确保在解析失败时返回默认值。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| PLATFORM_TAG = "platform" | String | 定义了一个静态常量字符串变量，标签为“platform”。 |
| VERSION_TAG = "clientVersion" | String | 定义常量VERSION_TAG，值为"clientVersion"。 |
| LIBSIGNAL_TAG = "libsignal" | String | LIBSIGNAL_TAG 定义为常量字符串 "libsignal"。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getClientVersionTag | Optional<Tag> | 方法解析用户代理字符串，若版本有效则返回版本标签，否则返回空。 |
| getLibsignalAndPlatformTags | List<Tag> | 解析用户代理字符串，获取平台和libsignal信息，返回标签列表。 |
| getPlatformTag | Tag | 从用户代理字符串中提取平台标签，若无法识别则标记为"unrecognized"。 |




