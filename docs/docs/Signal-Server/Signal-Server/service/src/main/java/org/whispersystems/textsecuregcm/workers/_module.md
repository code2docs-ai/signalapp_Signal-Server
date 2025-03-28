# 基础信息

|      |      |
|------|------|
| 名称 | workers |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/workers |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.workers |
| 概述说明 | 多个命令类实现删除、推送、持久化等功能，支持并发控制、模拟运行和分段扫描，确保系统稳定性和数据安全。 |

# 说明

## 概述

该代码模块主要包含一系列用于管理和执行系统任务的命令类，涵盖了备份管理、用户数据控制、设备管理、推送通知、消息持久化、密钥生成、证书管理、日志管理等多个功能领域。这些命令类设计上普遍支持并发控制、模拟运行、分段扫描、异常处理等机制，以确保任务的高效性、安全性和可测试性。模块中的类通常用于后台任务调度、数据清理、系统配置验证等场景，帮助维护系统的稳定性和数据的完整性。

## 主要业务场景

1. **备份管理**：
   - **删除过期备份**：通过分段扫描和并发控制，逐步清理过期备份数据，同时提供宽限期和模拟运行功能，确保操作的安全性和效率。
   - **备份指标报告**：通过分段扫描和指标记录，定期备份和监控关键指标数据，确保数据的完整性和可追溯性。

2. **用户数据控制**：
   - **设置用户可发现性**：通过UUID或E164标识，灵活控制用户在系统中的可见性，确保用户数据的隐私和可访问性。
   - **删除过期账户**：自动清理超过120天未活动的账户，支持并发处理和模拟运行，确保系统资源的有效利用。
   - **删除过期用户名**：定期清理过期用户名，支持模拟运行和并发控制，提高系统的维护效率。

3. **设备管理**：
   - **移除过期设备**：通过并发处理、缓冲和重试机制，清理过期设备，支持干运行模式进行模拟测试。
   - **解绑设备**：根据设备ID和账户UUID，解绑设备并清除相关消息，确保解绑过程彻底且无遗留问题。
   - **检查设备闲置状态**：根据设备的闲置时长，决定是否发送推送通知，优化推送策略，提升用户体验。

4. **推送通知**：
   - **调度空闲设备通知**：支持并发控制和模拟运行，确保在设备空闲时能够及时触发通知。
   - **推送通知实验管理**：支持并发控制和状态记录，管理推送通知实验的启动、执行和完成过程，确保实验的可靠性和效率。
   - **废弃推送通知实验样本**：处理实验样本的废弃操作，支持配置最大并发数，优化系统性能和资源利用率。

5. **消息持久化**：
   - **持久化未送达消息**：在多线程环境中，确保消息在未能成功送达时被安全保存，避免数据丢失，并支持后续处理或重新发送。

6. **密钥与证书管理**：
   - **生成服务器密钥**：生成并输出服务器的公钥和私钥，确保服务器的安全通信和数据保护。
   - **生成服务器证书**：支持生成CA参数和进行证书签名操作，包含密钥ID校验和错误处理机制，确保操作的稳定性和安全性。

7. **日志与配置管理**：
   - **设置请求日志启用状态**：灵活控制请求日志的记录行为，确保系统日志管理的有效性和可配置性。
   - **检查动态配置文件有效性**：验证配置文件内容是否符合预期格式和规范，确保配置文件的正确性和可用性。

8. **任务调度与执行**：
   - **定时任务处理**：支持固定延迟配置和关闭等待配置，确保任务按计划执行并在服务关闭时完成，提高任务的可靠性和系统的稳定性。
   - **抽象命令类管理**：通过抽象化的方式，统一管理依赖项的启动与停止操作，并在异常发生时进行适当处理，维护系统的稳定性和可靠性。

这些业务场景共同构成了该代码模块的核心功能，帮助系统在多个关键领域实现高效、安全和可扩展的任务管理。


### 包内部结构视图

```mermaid
graph TD
    workers --> RemoveExpiredBackupsCommand.java
    workers --> SetUserDiscoverabilityCommand.java
    workers --> RemoveExpiredLinkedDevicesCommand.java
    workers --> BackupMetricsCommand.java
    workers --> NotifyIdleDevicesCommand.java
    workers --> MessagePersisterServiceCommand.java
    workers --> PushNotificationExperimentFactory.java
    workers --> ZkParamsCommand.java
    workers --> RemoveExpiredUsernameHoldsCommand.java
    workers --> RemoveExpiredAccountsCommand.java
    workers --> AbstractSinglePassCrawlAccountsCommand.java
    workers --> JobSchedulerFactory.java
    workers --> StartPushNotificationExperimentCommand.java
    workers --> CertificateCommand.java
    workers --> CommandDependencies.java
    workers --> CheckDynamicConfigurationCommand.java
    workers --> SetRequestLoggingEnabledTask.java
    workers --> ScheduledApnPushNotificationSenderServiceCommand.java
    workers --> ServerVersionCommand.java
    workers --> DiscardPushNotificationExperimentSamplesCommand.java
    workers --> IdleWakeupEligibilityChecker.java
    workers --> ProcessScheduledJobsServiceCommand.java
    workers --> AbstractCommandWithDependencies.java
    workers --> UnlinkDeviceCommand.java
    workers --> IdleDeviceNotificationSchedulerFactory.java
    workers --> DeleteUserCommand.java
    workers --> FinishPushNotificationExperimentCommand.java
```

该流程图展示了 `workers` 文件夹下的所有命令和任务文件，这些文件主要用于处理各种后台任务和命令执行。每个文件都直接与 `workers` 文件夹相连，表示它们属于同一层级。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [JobSchedulerFactory.java](JobSchedulerFactory.md) | file | 信息为空，无法生成概要描述。 |
| [ZkParamsCommand.java](ZkParamsCommand.md) | file | ZkParamsCommand类生成并输出服务器的公钥和私钥。 |
| [PushNotificationExperimentFactory.java](PushNotificationExperimentFactory.md) | file | 无内容提供，无法生成概要描述。 |
| [BackupMetricsCommand.java](BackupMetricsCommand.md) | file | BackupMetricsCommand类备份指标报告，支持分段扫描和记录。 |
| [FinishPushNotificationExperimentCommand.java](FinishPushNotificationExperimentCommand.md) | file | FinishPushNotificationExperimentCommand类完成推送实验，支持并发与状态记录。 |
| [UnlinkDeviceCommand.java](UnlinkDeviceCommand.md) | file | UnlinkDeviceCommand类解绑设备并清除消息，需设备ID和账户UUID。 |
| [IdleWakeupEligibilityChecker.java](IdleWakeupEligibilityChecker.md) | file | 检查设备推送通知适配性，区分短时和长时闲置。 |
| [SetRequestLoggingEnabledTask.java](SetRequestLoggingEnabledTask.md) | file | SetRequestLoggingEnabledTask类用于更新请求日志启用状态并输出结果。 |
| [CommandDependencies.java](CommandDependencies.md) | file | 信息为空，无法生成概要描述。 |
| [DeleteUserCommand.java](DeleteUserCommand.md) | file | 删除用户命令类支持多用户删除，记录日志并处理异常。 |
| [IdleDeviceNotificationSchedulerFactory.java](IdleDeviceNotificationSchedulerFactory.md) | file | IdleDeviceNotificationSchedulerFactory实现JobSchedulerFactory接口，构建IdleDeviceNotificationScheduler实例。 |
| [AbstractCommandWithDependencies.java](AbstractCommandWithDependencies.md) | file | 抽象命令类管理依赖项启停，处理异常。 |
| [ProcessScheduledJobsServiceCommand.java](ProcessScheduledJobsServiceCommand.md) | file | Java服务类支持定时任务处理，可配置固定延迟和关闭等待。 |
| [DiscardPushNotificationExperimentSamplesCommand.java](DiscardPushNotificationExperimentSamplesCommand.md) | file | 废弃推送通知实验样本类，支持配置最大并发数。 |
| [ServerVersionCommand.java](ServerVersionCommand.md) | file | ServerVersionCommand类用于输出服务版本信息。 |
| [ScheduledApnPushNotificationSenderServiceCommand.java](ScheduledApnPushNotificationSenderServiceCommand.md) | file | ScheduledApnPushNotificationSenderServiceCommand类启动定时APNs推送服务，配置线程和并发数。 |
| [CheckDynamicConfigurationCommand.java](CheckDynamicConfigurationCommand.md) | file | 检查动态配置文件有效性并输出结果。 |
| [CertificateCommand.java](CertificateCommand.md) | file | CertificateCommand类生成服务器证书，支持CA参数、签名、密钥ID校验及错误处理。 |
| [StartPushNotificationExperimentCommand.java](StartPushNotificationExperimentCommand.md) | file | 启动推送通知实验命令类，支持并发控制与模拟运行。 |
| [AbstractSinglePassCrawlAccountsCommand.java](AbstractSinglePassCrawlAccountsCommand.md) | file | 抽象类实现单次爬取账户，涵盖配置、依赖管理和爬取逻辑。 |
| [RemoveExpiredAccountsCommand.java](RemoveExpiredAccountsCommand.md) | file | 删除120天未活动账户，支持并发和模拟运行。 |
| [RemoveExpiredUsernameHoldsCommand.java](RemoveExpiredUsernameHoldsCommand.md) | file | 删除过期用户名命令支持模拟运行和并发控制。 |
| [MessagePersisterServiceCommand.java](MessagePersisterServiceCommand.md) | file | MessagePersisterServiceCommand类用于多线程持久化未送达消息。 |
| [NotifyIdleDevicesCommand.java](NotifyIdleDevicesCommand.md) | file | NotifyIdleDevicesCommand类用于调度空闲设备推送通知，支持并发和模拟运行。 |
| [RemoveExpiredLinkedDevicesCommand.java](RemoveExpiredLinkedDevicesCommand.md) | file | 移除过期设备命令类，支持并发、缓冲、重试，含干运行模式。 |
| [SetUserDiscoverabilityCommand.java](SetUserDiscoverabilityCommand.md) | file | SetUserDiscoverabilityCommand用于设置CDS中用户的可发现性，支持UUID或E164标识，并可更新状态。 |
| [RemoveExpiredBackupsCommand.java](RemoveExpiredBackupsCommand.md) | file | 删除过期备份命令类，支持分段扫描、并发控制、宽限期和模拟运行。 |


