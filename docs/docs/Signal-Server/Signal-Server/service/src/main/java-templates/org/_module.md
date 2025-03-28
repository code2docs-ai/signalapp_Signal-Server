# 基础信息

|      |      |
|------|------|
| 名称 | org |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java-templates/org |
| 包名 | Signal-Server.service.src.main.java-templates.org |
| 概述说明 | WhisperServerVersion类用于获取服务器版本号。 |

# 说明

WhisperServerVersion类是一个用于获取服务器版本号的工具类。该类的主要功能是提供一种方法来获取当前服务器的版本号信息。通过调用该类的方法，用户可以方便地获取服务器的版本号，以便进行版本控制、兼容性检查或其他相关操作。


### 包内部结构视图

```mermaid
graph TD
    org --> whispersystems
    whispersystems --> textsecuregcm
    textsecuregcm --> WhisperServerVersion.java
```

该流程图展示了Signal-Server项目中Java代码的层级结构。从根目录`org`开始，逐级深入到`whispersystems`和`textsecuregcm`，最终指向`WhisperServerVersion.java`文件。这种结构清晰地反映了代码的组织方式，便于开发人员理解和维护。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [whispersystems](whispersystems/_module.md) | package | WhisperServerVersion类用于获取服务器版本号。 |


