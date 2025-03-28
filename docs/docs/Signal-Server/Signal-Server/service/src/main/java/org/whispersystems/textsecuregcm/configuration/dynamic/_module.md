# 基础信息

|      |      |
|------|------|
| 名称 | dynamic |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/configuration/dynamic |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.configuration.dynamic |
| 概述说明 | 动态配置类管理实验、限速、支付、验证码等模块，支持灵活调整。 |

# 说明

## 概述

该代码模块主要涉及动态配置管理，旨在通过灵活的配置选项来支持系统的多种功能模块。这些配置项包括实验管理、限速策略、支付设置、验证码控制、消息持久化、用户注册、版本控制等。通过动态调整这些配置，系统能够适应不同的业务需求，提升系统的兼容性、安全性和性能。

## 主要业务场景

1. **版本控制与用户代理管理**：通过动态远程弃用配置类，管理客户端平台的版本控制和用户代理的访问权限，确保不同版本的客户端能够正常运行，同时控制用户代理的访问。
2. **实验管理**：动态实验配置类用于管理实验的启用比例、用户筛选和排除，确保实验的精准性和可控性。E164实验配置类则专门管理与E164号码相关的实验设置，如号码注册、国家代码和注册百分比。
3. **消息持久化**：动态消息持久化配置类管理消息的持久化行为和队列修剪策略，确保消息的高可靠性和存储优化。
4. **验证码控制**：动态验证码配置类管理验证码的分数下限、hCaptcha允许状态和站点密钥映射，确保验证码服务的严格性和独立性。
5. **支付管理**：动态支付配置类通过维护禁止前缀列表，限制特定前缀的支付操作，确保支付系统的安全性和合规性。
6. **动态配置整合**：DynamicConfiguration类负责整合多个动态配置项，包括实验、限速、支付和验证码等功能模块，提供统一的配置管理接口，确保系统能够灵活响应不同的业务需求。

通过这些动态配置管理，系统能够在不同的业务场景中实现灵活、高效的配置调整，提升系统的整体性能和用户体验。


### 包内部结构视图

```mermaid
graph TD
    dynamic --> DynamicRemoteDeprecationConfiguration.java
    dynamic --> DynamicE164ExperimentEnrollmentConfiguration.java
    dynamic --> DynamicVirtualThreadConfiguration.java
    dynamic --> DynamicRegistrationConfiguration.java
    dynamic --> DynamicMessagePersisterConfiguration.java
    dynamic --> DynamicExperimentEnrollmentConfiguration.java
    dynamic --> DynamicCaptchaConfiguration.java
    dynamic --> DynamicPaymentsConfiguration.java
    dynamic --> DynamicRateLimitPolicy.java
    dynamic --> DynamicMetricsConfiguration.java
    dynamic --> DynamicConfiguration.java
```

该流程图展示了Signal-Server项目中`dynamic`文件夹下的所有配置文件。这些文件分别对应不同的动态配置，如远程弃用配置、E164实验注册配置、虚拟线程配置等。每个文件都直接隶属于`dynamic`文件夹，清晰地反映了它们之间的层级关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [DynamicConfiguration.java](DynamicConfiguration.md) | file | DynamicConfiguration类提供实验、限速、支付、验证码等动态配置项及其获取方法。 |
| [DynamicMetricsConfiguration.java](DynamicMetricsConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [DynamicRateLimitPolicy.java](DynamicRateLimitPolicy.md) | file | 无内容，无法生成概要描述。 |
| [DynamicMessagePersisterConfiguration.java](DynamicMessagePersisterConfiguration.md) | file | 动态消息持久化配置类含开关和队列修剪比例。 |
| [DynamicRegistrationConfiguration.java](DynamicRegistrationConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [DynamicPaymentsConfiguration.java](DynamicPaymentsConfiguration.md) | file | 动态支付配置类，含禁止前缀列表及其获取方法。 |
| [DynamicCaptchaConfiguration.java](DynamicCaptchaConfiguration.md) | file | 动态验证码配置类：含分数下限、hCaptcha状态及站点密钥映射。 |
| [DynamicExperimentEnrollmentConfiguration.java](DynamicExperimentEnrollmentConfiguration.md) | file | 动态实验配置类含UUID选择器、排除集和启用百分比。 |
| [DynamicVirtualThreadConfiguration.java](DynamicVirtualThreadConfiguration.md) | file | 信息为空，无法生成概要描述。 |
| [DynamicE164ExperimentEnrollmentConfiguration.java](DynamicE164ExperimentEnrollmentConfiguration.md) | file | 动态E164实验配置类管理注册、排除号码、国家代码及注册百分比。 |
| [DynamicRemoteDeprecationConfiguration.java](DynamicRemoteDeprecationConfiguration.md) | file | 动态远程弃用配置类管理客户端版本和用户代理状态。 |


