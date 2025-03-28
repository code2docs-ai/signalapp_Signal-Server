# 基础信息

|      |      |
|------|------|
| 名称 | entities |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/entities |
| 包名 | Signal-Server.service.src.main.java.org.whispersystems.textsecuregcm.entities |
| 概述说明 | 输入内容为空，无法进行总结描述。请提供具体内容以便生成相应的总结。 |

# 说明

## 概述

该代码模块主要涉及Signal-Server服务中的实体类，这些实体类用于处理各种业务场景中的数据结构和业务逻辑。模块中的类涵盖了账户管理、消息通信、密钥管理、验证流程、配置文件管理等多个方面。通过这些实体类，系统能够有效地管理用户账户、处理消息传输、确保通信安全、以及进行各种验证和配置操作。模块中的类设计合理，提供了丰富的属性和方法，支持数据的序列化与反序列化，确保了系统的灵活性和可扩展性。

## 主要业务场景

1. **账户管理**：包括账户的创建、更新、验证、设备管理等功能。相关类如`AccountCreationResponse`、`AccountAttributes`、`AccountIdentifierResponse`等，用于处理账户相关的操作和数据管理。
   
2. **消息通信**：涉及WebSocket消息的处理、消息的发送与接收、消息的确认与同步等。相关类如`IncomingWebsocketMessage`、`SendMessageResponse`、`OutgoingMessageEntity`等，用于确保消息的稳定传输和正确处理。

3. **密钥管理**：包括预密钥、签名密钥、身份密钥的管理与验证。相关类如`PreKey`、`PreKeyResponse`、`PreKeySignatureValidator`等，用于确保通信过程中的安全性和密钥的正确性。

4. **验证流程**：涉及用户身份验证、验证码处理、验证会话管理等。相关类如`VerificationCodeRequest`、`CreateVerificationSessionRequest`、`AnswerChallengeRequest`等，用于处理用户身份验证和会话管理。

5. **配置文件管理**：包括用户配置文件的管理、版本控制、配置文件的上传与更新等。相关类如`CredentialProfileResponse`、`VersionedProfileResponse`、`ProfileAvatarUploadAttributes`等，用于管理用户配置文件和相关信息。

6. **徽章管理**：涉及用户徽章的管理、徽章的上传与展示等。相关类如`Badge`、`PurchasableBadge`、`SelfBadge`等，用于处理用户徽章相关的数据和操作。

7. **货币转换**：涉及货币转换的管理、汇率信息的存储与更新等。相关类如`CurrencyConversionEntity`、`CurrencyConversionEntityList`等，用于处理货币转换相关的数据和操作。

通过这些业务场景，该代码模块为Signal-Server服务提供了全面的支持，确保了系统的稳定性、安全性和可扩展性。


### 包内部结构视图

```mermaid
graph TD
    entities --> AccountIdentityResponse.java
    entities --> CredentialProfileResponse.java
    entities --> VerificationSessionResponse.java
    entities --> RegistrationRequest.java
    entities --> IncomingWebsocketMessage.java
    entities --> PreKey.java
    entities --> GroupCredentials.java
    entities --> ExpiringProfileKeyCredentialResponseAdapter.java
    entities --> AccountStaleDevices.java
    entities --> BadgeSvg.java
    entities --> RemoteAttachment.java
    entities --> ProvisioningMessage.java
    entities --> GcmRegistrationId.java
    entities --> PreKeySignatureValidator.java
    entities --> ECSignedPreKey.java
    entities --> BatchIdentityCheckRequest.java
    entities --> VersionedProfileResponse.java
    entities --> CheckKeysRequest.java
    entities --> IncomingMessage.java
    entities --> ProfileAvatarUploadAttributes.java
    entities --> PurchasableBadge.java
    entities --> KeyTransparencySearchRequest.java
    entities --> UsernameLinkHandle.java
    entities --> LinkDeviceResponse.java
    entities --> AuthCheckResponseV3.java
    entities --> KeyTransparencyMonitorResponse.java
    entities --> AccountAttributes.java
    entities --> AccountCreationResponse.java
    entities --> OutgoingMessageEntityList.java
    entities --> SubmitVerificationCodeRequest.java
    entities --> StaleDevices.java
    entities --> BatchIdentityCheckResponse.java
    entities --> LinkDeviceRequest.java
    entities --> RateLimitChallenge.java
    entities --> SelfBadge.java
    entities --> RegistrationLock.java
    entities --> ConfirmUsernameHashRequest.java
    entities --> ApnRegistrationId.java
    entities --> AvatarChange.java
    entities --> PhoneNumberIdentityKeyDistributionRequest.java
    entities --> OutgoingMessageEntity.java
    entities --> ChangeNumberRequest.java
    entities --> ReserveUsernameHashResponse.java
    entities --> ReserveUsernameHashRequest.java
    entities --> KeyTransparencyDistinguishedKeyResponse.java
    entities --> RestoreAccountRequest.java
    entities --> GetCreateCallLinkCredentialsRequest.java
    entities --> RegistrationServiceSession.java
    entities --> IncomingMessageList.java
    entities --> SpamReport.java
    entities --> CurrencyConversionEntityList.java
    entities --> RemoteAttachmentError.java
    entities --> MismatchedDevices.java
    entities --> Entitlements.java
    entities --> Badge.java
    entities --> AnswerCaptchaChallengeRequest.java
    entities --> CreateCallLinkCredential.java
    entities --> RegistrationLockFailure.java
    entities --> DeliveryCertificate.java
    entities --> SignedPreKey.java
    entities --> TransferArchiveUploadedRequest.java
    entities --> AnswerPushChallengeRequest.java
    entities --> ECPreKey.java
    entities --> SendMultiRecipientMessageResponse.java
    entities --> PreKeyResponse.java
    entities --> SetPublicKeyRequest.java
    entities --> AuthCheckResponseV2.java
    entities --> PhoneVerificationRequest.java
    entities --> StickerPackFormUploadAttributes.java
    entities --> ExpiringProfileKeyCredentialProfileResponse.java
    entities --> VerificationCodeRequest.java
    entities --> RedeemReceiptRequest.java
    entities --> CurrencyConversionEntity.java
    entities --> DeviceName.java
    entities --> SendMessageResponse.java
    entities --> DeviceInfoList.java
    entities --> UpdateVerificationSessionRequest.java
    entities --> UserRemoteConfigList.java
    entities --> KeyTransparencySearchResponse.java
    entities --> KEMSignedPreKey.java
    entities --> KeyTransparencyMonitorRequest.java
    entities --> PreKeyCount.java
    entities --> CreateVerificationSessionRequest.java
    entities --> PhoneNumberDiscoverabilityRequest.java
    entities --> AttachmentDescriptorV3.java
    entities --> PreKeyResponseItem.java
    entities --> AnswerChallengeRequest.java
    entities --> DeviceInfo.java
    entities --> AccountMismatchedDevices.java
    entities --> UsernameHashResponse.java
    entities --> AccountDataReportResponse.java
    entities --> BaseProfileResponse.java
    entities --> AuthCheckRequest.java
    entities --> SetKeysRequest.java
    entities --> EncryptedUsername.java
    entities --> UserRemoteConfig.java
    entities --> CreateProfileRequest.java
    entities --> AccountIdentifierResponse.java
    entities --> TransferArchiveResult.java
    entities --> DeviceActivationRequest.java
    entities --> ProfileKeyCommitmentAdapter.java
```

该流程图展示了 `entities` 文件夹下的所有文件及其层级关系。`entities` 是根节点，直接连接到多个 Java 文件，每个文件都代表了不同的实体类或响应类。这些文件涵盖了从账户管理、消息处理到密钥验证等多个功能模块，反映了项目的复杂性和多样性。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [RegistrationRequest.java](RegistrationRequest.md) | file | 信息为空，无法生成概要描述。 |
| [AccountIdentityResponse.java](AccountIdentityResponse.md) | file | 信息为空，无法生成概要描述。 |
| [ReserveUsernameHashResponse.java](ReserveUsernameHashResponse.md) | file | 信息为空，无法生成概要描述。 |
| [OutgoingMessageEntity.java](OutgoingMessageEntity.md) | file | 信息为空，无法生成概要描述。 |
| [AvatarChange.java](AvatarChange.md) | file | 无内容提供，无法生成概要描述。 |
| [ApnRegistrationId.java](ApnRegistrationId.md) | file | 信息为空，无法生成概要描述。 |
| [RegistrationLock.java](RegistrationLock.md) | file | 类RegistrationLock包含64字符注册锁字符串，提供构造和获取方法。 |
| [LinkDeviceRequest.java](LinkDeviceRequest.md) | file | 信息为空，无法生成概要描述。 |
| [StaleDevices.java](StaleDevices.md) | file | 信息为空，无法生成概要描述。 |
| [SubmitVerificationCodeRequest.java](SubmitVerificationCodeRequest.md) | file | 信息为空，无法生成概要描述。 |
| [AccountAttributes.java](AccountAttributes.md) | file | AccountAttributes类管理账户属性，支持测试和验证。 |
| [AuthCheckResponseV3.java](AuthCheckResponseV3.md) | file | 信息为空，无法生成概要描述。 |
| [LinkDeviceResponse.java](LinkDeviceResponse.md) | file | 无内容可总结。 |
| [KeyTransparencySearchRequest.java](KeyTransparencySearchRequest.md) | file | 信息为空，无法生成概要描述。 |
| [IncomingMessage.java](IncomingMessage.md) | file | 信息为空，无法生成概要描述。 |
| [CheckKeysRequest.java](CheckKeysRequest.md) | file | 信息为空，无法生成概要描述。 |
| [BatchIdentityCheckRequest.java](BatchIdentityCheckRequest.md) | file | 信息为空，无法生成概要描述。 |
| [GcmRegistrationId.java](GcmRegistrationId.md) | file | 信息为空，无法生成概要描述。 |
| [ProvisioningMessage.java](ProvisioningMessage.md) | file | 无内容可总结。 |
| [RemoteAttachment.java](RemoteAttachment.md) | file | 内容为空，无法生成概要描述。 |
| [AccountStaleDevices.java](AccountStaleDevices.md) | file | 信息为空，无法生成概要描述。 |
| [GroupCredentials.java](GroupCredentials.md) | file | 信息为空，无法生成概要描述。 |
| [PreKey.java](PreKey.md) | file | 输入信息为空，请提供具体内容以便生成概要描述。 |
| [SpamReport.java](SpamReport.md) | file | 信息为空，无法生成概要描述。 |
| [IncomingMessageList.java](IncomingMessageList.md) | file | 无内容可概括。 |
| [GetCreateCallLinkCredentialsRequest.java](GetCreateCallLinkCredentialsRequest.md) | file | 无内容，无法生成概要。 |
| [KeyTransparencyDistinguishedKeyResponse.java](KeyTransparencyDistinguishedKeyResponse.md) | file | 信息为空，无法生成概要描述。 |
| [KeyTransparencyMonitorRequest.java](KeyTransparencyMonitorRequest.md) | file | 无内容提供，无法生成概要描述。 |
| [KeyTransparencySearchResponse.java](KeyTransparencySearchResponse.md) | file | 无内容，无法生成概要描述。 |
| [UpdateVerificationSessionRequest.java](UpdateVerificationSessionRequest.md) | file | 无内容，无法生成概要。 |
| [DeviceName.java](DeviceName.md) | file | 内容为空，无法生成概要描述。 |
| [VerificationCodeRequest.java](VerificationCodeRequest.md) | file | 无内容提供，无法生成概要描述。 |
| [StickerPackFormUploadAttributes.java](StickerPackFormUploadAttributes.md) | file | StickerPackFormUploadAttributes类管理贴纸包上传信息，包含packId、manifest和stickers属性。 |
| [PhoneVerificationRequest.java](PhoneVerificationRequest.md) | file | 无内容提供，无法生成概要描述。 |
| [SetPublicKeyRequest.java](SetPublicKeyRequest.md) | file | 信息为空，无法生成概要描述。 |
| [SendMultiRecipientMessageResponse.java](SendMultiRecipientMessageResponse.md) | file | 无内容提供，无法生成概要描述。 |
| [AnswerPushChallengeRequest.java](AnswerPushChallengeRequest.md) | file | 类AnswerPushChallengeRequest继承AnswerChallengeRequest，含挑战令牌字段。 |
| [SignedPreKey.java](SignedPreKey.md) | file | 无内容提供，无法生成概要描述。 |
| [RegistrationLockFailure.java](RegistrationLockFailure.md) | file | 内容为空，无法生成概要描述。 |
| [Badge.java](Badge.md) | file | Badge类包含ID、类别、名称、描述、6精灵图、SVG及列表，含数据验证和重写方法。 |
| [MismatchedDevices.java](MismatchedDevices.md) | file | 无内容提供，无法生成概要描述。 |
| [AccountDataReportResponse.java](AccountDataReportResponse.md) | file | 请提供具体信息以便进行概要描述。 |
| [AccountMismatchedDevices.java](AccountMismatchedDevices.md) | file | 输入内容为空，无法生成概要描述。 |
| [AttachmentDescriptorV3.java](AttachmentDescriptorV3.md) | file | 无内容，无法生成概要描述。 |
| [PhoneNumberDiscoverabilityRequest.java](PhoneNumberDiscoverabilityRequest.md) | file | 信息为空，无法生成概要描述。 |
| [ProfileKeyCommitmentAdapter.java](ProfileKeyCommitmentAdapter.md) | file | ProfileKeyCommitmentAdapter类实现ProfileKeyCommitment对象的Base64编码转换。 |
| [DeviceActivationRequest.java](DeviceActivationRequest.md) | file | 信息为空，无法生成概要描述。 |
| [TransferArchiveResult.java](TransferArchiveResult.md) | file | 无内容可总结。 |
| [AccountIdentifierResponse.java](AccountIdentifierResponse.md) | file | 信息为空，无法生成概要描述。 |
| [CreateProfileRequest.java](CreateProfileRequest.md) | file | 信息为空，无法生成概要描述。 |
| [UserRemoteConfig.java](UserRemoteConfig.md) | file | 用户远程配置类：名称、启用状态、配置值。 |
| [EncryptedUsername.java](EncryptedUsername.md) | file | 内容为空，无法生成概要描述。 |
| [SetKeysRequest.java](SetKeysRequest.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [AuthCheckRequest.java](AuthCheckRequest.md) | file | 无内容可总结。 |
| [BaseProfileResponse.java](BaseProfileResponse.md) | file | BaseProfileResponse类包含身份密钥、未识别访问、能力、徽章和UUID等属性。 |
| [UsernameHashResponse.java](UsernameHashResponse.md) | file | 信息为空，无法生成概要描述。 |
| [DeviceInfo.java](DeviceInfo.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [AnswerChallengeRequest.java](AnswerChallengeRequest.md) | file | 抽象类AnswerChallengeRequest支持rateLimitPushChallenge和captcha两种类型。 |
| [PreKeyResponseItem.java](PreKeyResponseItem.md) | file | PreKeyResponseItem类包含设备ID、注册ID、签名预密钥、预密钥和量子预密钥。 |
| [CreateVerificationSessionRequest.java](CreateVerificationSessionRequest.md) | file | 创建验证会话请求类，包含E164格式电话号码和更新验证会话请求。 |
| [PreKeyCount.java](PreKeyCount.md) | file | PreKeyCount类存储椭圆曲线和一次性后量子预密钥数量。 |
| [KEMSignedPreKey.java](KEMSignedPreKey.md) | file | 信息为空，无法生成概要描述。 |
| [UserRemoteConfigList.java](UserRemoteConfigList.md) | file | 用户远程配置类，含配置列表及生成时间戳。 |
| [DeviceInfoList.java](DeviceInfoList.md) | file | 信息为空，无法生成概要描述。 |
| [SendMessageResponse.java](SendMessageResponse.md) | file | SendMessageResponse类的needsSync属性表示同步需求。 |
| [CurrencyConversionEntity.java](CurrencyConversionEntity.md) | file | CurrencyConversionEntity类管理基础货币及汇率转换映射。 |
| [RedeemReceiptRequest.java](RedeemReceiptRequest.md) | file | RedeemReceiptRequest类含凭证展示、可见性及主状态属性。 |
| [ExpiringProfileKeyCredentialProfileResponse.java](ExpiringProfileKeyCredentialProfileResponse.md) | file | ExpiringProfileKeyCredentialProfileResponse继承CredentialProfileResponse，含可空凭证属性。 |
| [AuthCheckResponseV2.java](AuthCheckResponseV2.md) | file | 无内容提供，无法生成描述。 |
| [PreKeyResponse.java](PreKeyResponse.md) | file | PreKeyResponse类存储身份密钥和设备信息，支持获取密钥和设备数量。 |
| [ECPreKey.java](ECPreKey.md) | file | 信息为空，无法生成概要描述。 |
| [TransferArchiveUploadedRequest.java](TransferArchiveUploadedRequest.md) | file | 输入内容为空，请提供具体信息以便生成概要描述。 |
| [DeliveryCertificate.java](DeliveryCertificate.md) | file | DeliveryCertificate类包含字节数组证书，提供构造和获取方法。 |
| [CreateCallLinkCredential.java](CreateCallLinkCredential.md) | file | 暂无内容，请提供具体信息以便生成概要描述。 |
| [AnswerCaptchaChallengeRequest.java](AnswerCaptchaChallengeRequest.md) | file | 类AnswerCaptchaChallengeRequest继承AnswerChallengeRequest，包含token和captcha字段及其获取方法。 |
| [Entitlements.java](Entitlements.md) | file | 无内容可总结。 |
| [RemoteAttachmentError.java](RemoteAttachmentError.md) | file | 无内容提供，无法生成概要描述。 |
| [CurrencyConversionEntityList.java](CurrencyConversionEntityList.md) | file | 类包含货币转换列表和时间戳，提供构造和获取方法。 |
| [RegistrationServiceSession.java](RegistrationServiceSession.md) | file | 输入内容为空，无法生成概要描述。 |
| [RestoreAccountRequest.java](RestoreAccountRequest.md) | file | 信息为空，无法生成概要描述。 |
| [ReserveUsernameHashRequest.java](ReserveUsernameHashRequest.md) | file | 无内容提供，无法生成概要描述。 |
| [ChangeNumberRequest.java](ChangeNumberRequest.md) | file | 信息为空，无法生成概要描述。 |
| [PhoneNumberIdentityKeyDistributionRequest.java](PhoneNumberIdentityKeyDistributionRequest.md) | file | 信息为空，无法生成概要描述。 |
| [ConfirmUsernameHashRequest.java](ConfirmUsernameHashRequest.md) | file | 无内容可总结。 |
| [SelfBadge.java](SelfBadge.md) | file | SelfBadge继承Badge，含过期时间和可见性，重写equals、hashCode、toString方法。 |
| [RateLimitChallenge.java](RateLimitChallenge.md) | file | RateLimitChallenge类含token和options属性，提供构造和获取方法。 |
| [BatchIdentityCheckResponse.java](BatchIdentityCheckResponse.md) | file | 信息为空，无法生成概要描述。 |
| [OutgoingMessageEntityList.java](OutgoingMessageEntityList.md) | file | 信息为空，无法生成概要描述。 |
| [AccountCreationResponse.java](AccountCreationResponse.md) | file | 账户创建响应类包含身份信息和重新注册标识。 |
| [KeyTransparencyMonitorResponse.java](KeyTransparencyMonitorResponse.md) | file | 无内容可总结。 |
| [UsernameLinkHandle.java](UsernameLinkHandle.md) | file | 信息为空，无法生成概要描述。 |
| [PurchasableBadge.java](PurchasableBadge.md) | file | PurchasableBadge继承Badge，新增duration，重写构造方法和equals、hashCode、toString。 |
| [ProfileAvatarUploadAttributes.java](ProfileAvatarUploadAttributes.md) | file | ProfileAvatarUploadAttributes类存储上传头像的关键属性。 |
| [VersionedProfileResponse.java](VersionedProfileResponse.md) | file | VersionedProfileResponse类包含基本信息、名称、简介、表情、头像、支付地址和电话号码共享。 |
| [ECSignedPreKey.java](ECSignedPreKey.md) | file | 输入信息为空，无法生成概要描述。 |
| [PreKeySignatureValidator.java](PreKeySignatureValidator.md) | file | 预密钥签名验证类用于验证签名有效性并统计无效签名次数。 |
| [BadgeSvg.java](BadgeSvg.md) | file | BadgeSvg类含light、dark属性，验证非空并实现equals、hashCode、toString方法。 |
| [ExpiringProfileKeyCredentialResponseAdapter.java](ExpiringProfileKeyCredentialResponseAdapter.md) | file | ExpiringProfileKeyCredentialResponse的JSON序列化与反序列化适配器。 |
| [IncomingWebsocketMessage.java](IncomingWebsocketMessage.md) | file | WebSocket消息类，包含ACK、PING、PONG类型及获取方法。 |
| [VerificationSessionResponse.java](VerificationSessionResponse.md) | file | 信息为空，无法生成概要描述。 |
| [CredentialProfileResponse.java](CredentialProfileResponse.md) | file | 抽象类CredentialProfileResponse提供版本化配置文件响应的构造和获取方法。 |


