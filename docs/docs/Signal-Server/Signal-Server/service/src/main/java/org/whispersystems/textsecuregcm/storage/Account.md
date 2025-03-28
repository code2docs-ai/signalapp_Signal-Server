# 基础信息

|      |      |
|------|------|
| 名称 | Account |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/storage/Account.java |
| 包名 | org.whispersystems.textsecuregcm.storage |
| 依赖项 | ['com.fasterxml.jackson.annotation.JsonFilter', 'com.fasterxml.jackson.annotation.JsonIgnore', 'com.fasterxml.jackson.annotation.JsonProperty', 'com.fasterxml.jackson.databind.annotation.JsonDeserialize', 'com.fasterxml.jackson.databind.annotation.JsonSerialize', 'java.time.Clock', 'java.time.Instant', 'java.util.ArrayList', 'java.util.Collections', 'java.util.List', 'java.util.Objects', 'java.util.Optional', 'java.util.UUID', 'javax.annotation.Nullable', 'org.apache.commons.lang3.StringUtils', 'org.signal.libsignal.protocol.IdentityKey', 'org.signal.libsignal.zkgroup.backups.BackupCredentialType', 'org.slf4j.Logger', 'org.slf4j.LoggerFactory', 'org.whispersystems.textsecuregcm.auth.SaltedTokenHash', 'org.whispersystems.textsecuregcm.auth.StoredRegistrationLock', 'org.whispersystems.textsecuregcm.entities.AccountAttributes', 'org.whispersystems.textsecuregcm.identity.IdentityType', 'org.whispersystems.textsecuregcm.identity.ServiceIdentifier', 'org.whispersystems.textsecuregcm.util.ByteArrayBase64UrlAdapter', 'org.whispersystems.textsecuregcm.util.IdentityKeyAdapter'] |
| 概述说明 | Account类含UUID、电话、设备、密钥，支持用户名、加密、注册锁功能。 |

# 说明

Account类包含多个关键属性，包括UUID、电话号码标识符、设备列表和身份密钥。该类支持多种功能，如用户名设置、加密用户名管理以及注册锁机制。这些属性和功能共同构成了账户管理的基础，确保账户的安全性和唯一性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| Account | class | Account类包含UUID、电话号码标识符、设备列表、身份密钥等属性，支持用户名、加密用户名、注册锁等功能。 |



## 类 Account

|      |      |
|------|------|
| 访问范围 | @JsonFilter("Account");public |
| 类型 | class |
| 名称 | Account |
| 说明 | Account类包含UUID、电话号码标识符、设备列表、身份密钥等属性，支持用户名、加密用户名、注册锁等功能。 |


### UML类图

```mermaid
classDiagram
    class Account {
        -Logger logger
        -UUID uuid
        -UUID phoneNumberIdentifier
        -String number
        -byte[] usernameHash
        -byte[] reservedUsernameHash
        -UUID usernameLinkHandle
        -byte[] encryptedUsername
        -List~Device~ devices
        -IdentityKey identityKey
        -IdentityKey phoneNumberIdentityKey
        -String currentProfileVersion
        -List~AccountBadge~ badges
        -String registrationLock
        -String registrationLockSalt
        -byte[] unidentifiedAccessKey
        -boolean unrestrictedUnidentifiedAccess
        -boolean discoverableByPhoneNumber
        -byte[] messagesBackupCredentialRequest
        -byte[] mediaBackupCredentialRequest
        -BackupVoucher backupVoucher
        -int version
        -List~UsernameHold~ usernameHolds
        -boolean stale
        +UUID getIdentifier(IdentityType identityType)
        +UUID getUuid()
        +void setUuid(UUID uuid)
        +UUID getPhoneNumberIdentifier()
        +boolean isIdentifiedBy(ServiceIdentifier serviceIdentifier)
        +String getNumber()
        +void setNumber(String number, UUID phoneNumberIdentifier)
        +Optional~byte[]~ getUsernameHash()
        +void setUsernameHash(byte[] usernameHash)
        +Optional~byte[]~ getReservedUsernameHash()
        +void setReservedUsernameHash(byte[] reservedUsernameHash)
        +UUID getUsernameLinkHandle()
        +Optional~byte[]~ getEncryptedUsername()
        +void setUsernameLinkDetails(UUID usernameLinkHandle, byte[] encryptedUsername)
        +void setUsernameLinkHandle(UUID usernameLinkHandle)
        +void addDevice(Device device)
        +void removeDevice(byte deviceId)
        +List~Device~ getDevices()
        +Device getPrimaryDevice()
        +Optional~Device~ getDevice(byte deviceId)
        +boolean hasCapability(DeviceCapability capability)
        +byte getNextDeviceId()
        +void setIdentityKey(IdentityKey identityKey)
        +IdentityKey getIdentityKey(IdentityType identityType)
        +void setPhoneNumberIdentityKey(IdentityKey phoneNumberIdentityKey)
        +long getLastSeen()
        +Optional~String~ getCurrentProfileVersion()
        +void setCurrentProfileVersion(String currentProfileVersion)
        +List~AccountBadge~ getBadges()
        +void setBadges(Clock clock, List~AccountBadge~ badges)
        +void addBadge(Clock clock, AccountBadge badge)
        +void makeBadgePrimaryIfExists(Clock clock, String badgeId)
        +void removeBadge(Clock clock, String id)
        +void purgeStaleBadges(Clock clock)
        +void setRegistrationLockFromAttributes(AccountAttributes attributes)
        +void setRegistrationLock(String registrationLock, String registrationLockSalt)
        +StoredRegistrationLock getRegistrationLock()
        +Optional~byte[]~ getUnidentifiedAccessKey()
        +void setUnidentifiedAccessKey(byte[] unidentifiedAccessKey)
        +boolean isUnrestrictedUnidentifiedAccess()
        +void setUnrestrictedUnidentifiedAccess(boolean unrestrictedUnidentifiedAccess)
        +boolean isDiscoverableByPhoneNumber()
        +void setDiscoverableByPhoneNumber(boolean discoverableByPhoneNumber)
        +int getVersion()
        +void setVersion(int version)
        +void setBackupCredentialRequests(byte[] messagesBackupCredentialRequest, byte[] mediaBackupCredentialRequest)
        +Optional~byte[]~ getBackupCredentialRequest(BackupCredentialType credentialType)
        +BackupVoucher getBackupVoucher()
        +void setBackupVoucher(BackupVoucher backupVoucher)
        +boolean hasLockedCredentials()
        +void lockAuthTokenHash()
        +List~UsernameHold~ getUsernameHolds()
        +void setUsernameHolds(List~UsernameHold~ usernameHolds)
        +void markStale()
        -void requireNotStale()
    }

    class UsernameHold {
        +byte[] usernameHash
        +long expirationSecs
    }

    class BackupVoucher {
        +long receiptLevel
        +Instant expiration
    }

    class Device {
        +byte getId()
        +boolean hasCapability(DeviceCapability capability)
        +long getLastSeen()
        +void lockAuthTokenHash()
    }

    class AccountBadge {
        +String id()
        +Instant expiration()
        +AccountBadge mergeWith(AccountBadge other)
    }

    class IdentityKey {
    }

    class ServiceIdentifier {
        +IdentityType identityType()
        +UUID uuid()
    }

    class IdentityType {
    }

    class DeviceCapability {
        +AccountCapabilityMode getAccountCapabilityMode()
    }

    class AccountCapabilityMode {
    }

    class Clock {
        +Instant instant()
    }

    class AccountAttributes {
        +String getRegistrationLock()
    }

    class StoredRegistrationLock {
        +Optional~String~ getHash()
        +Optional~String~ getSalt()
        +Instant getLastSeen()
    }

    class BackupCredentialType {
    }

    Account --> Device : 包含
    Account --> UsernameHold : 包含
    Account --> BackupVoucher : 包含
    Account --> IdentityKey : 依赖
    Account --> ServiceIdentifier : 依赖
    Account --> DeviceCapability : 依赖
    Account --> Clock : 依赖
    Account --> AccountAttributes : 依赖
    Account --> StoredRegistrationLock : 依赖
    Account --> BackupCredentialType : 依赖
    UsernameHold --> Account : 依赖
    BackupVoucher --> Account : 依赖
    Device --> Account : 依赖
    AccountBadge --> Account : 依赖
    IdentityKey --> Account : 依赖
    ServiceIdentifier --> Account : 依赖
    DeviceCapability --> Account : 依赖
    Clock --> Account : 依赖
    AccountAttributes --> Account : 依赖
    StoredRegistrationLock --> Account : 依赖
    BackupCredentialType --> Account : 依赖
```

这段代码定义了一个 `Account` 类，用于管理账户信息。`Account` 类包含了多个私有字段，如 `uuid`、`phoneNumberIdentifier`、`number` 等，以及一系列公有方法用于获取和设置这些字段的值。类中还定义了多个内部类，如 `UsernameHold` 和 `BackupVoucher`，用于存储特定类型的数据。`Account` 类与其他类（如 `Device`、`IdentityKey` 等）存在依赖关系，通过这些依赖关系，`Account` 类能够管理设备、身份密钥等信息。整体设计复杂且功能丰富，适用于需要管理多种账户信息的场景。


### 内部方法调用关系图

```mermaid
graph TD
    A["类Account"]
    B["属性: UUID uuid"]
    C["属性: UUID phoneNumberIdentifier"]
    D["属性: String number"]
    E["属性: byte[] usernameHash"]
    F["属性: byte[] reservedUsernameHash"]
    G["属性: UUID usernameLinkHandle"]
    H["属性: byte[] encryptedUsername"]
    I["属性: List<Device> devices"]
    J["属性: IdentityKey identityKey"]
    K["属性: IdentityKey phoneNumberIdentityKey"]
    L["属性: String currentProfileVersion"]
    M["属性: List<AccountBadge> badges"]
    N["属性: String registrationLock"]
    O["属性: String registrationLockSalt"]
    P["属性: byte[] unidentifiedAccessKey"]
    Q["属性: boolean unrestrictedUnidentifiedAccess"]
    R["属性: boolean discoverableByPhoneNumber"]
    S["属性: byte[] messagesBackupCredentialRequest"]
    T["属性: byte[] mediaBackupCredentialRequest"]
    U["属性: BackupVoucher backupVoucher"]
    V["属性: int version"]
    W["属性: List<UsernameHold> usernameHolds"]
    X["属性: boolean stale"]
    Y["方法: UUID getIdentifier(IdentityType identityType)"]
    Z["方法: UUID getUuid()"]
    AA["方法: void setUuid(UUID uuid)"]
    AB["方法: UUID getPhoneNumberIdentifier()"]
    AC["方法: boolean isIdentifiedBy(ServiceIdentifier serviceIdentifier)"]
    AD["方法: String getNumber()"]
    AE["方法: void setNumber(String number, UUID phoneNumberIdentifier)"]
    AF["方法: Optional<byte[]> getUsernameHash()"]
    AG["方法: void setUsernameHash(byte[] usernameHash)"]
    AH["方法: Optional<byte[]> getReservedUsernameHash()"]
    AI["方法: void setReservedUsernameHash(byte[] reservedUsernameHash)"]
    AJ["方法: UUID getUsernameLinkHandle()"]
    AK["方法: Optional<byte[]> getEncryptedUsername()"]
    AL["方法: void setUsernameLinkDetails(UUID usernameLinkHandle, byte[] encryptedUsername)"]
    AM["方法: void setUsernameLinkHandle(UUID usernameLinkHandle)"]
    AN["方法: void addDevice(Device device)"]
    AO["方法: void removeDevice(byte deviceId)"]
    AP["方法: List<Device> getDevices()"]
    AQ["方法: Device getPrimaryDevice()"]
    AR["方法: Optional<Device> getDevice(byte deviceId)"]
    AS["方法: boolean hasCapability(DeviceCapability capability)"]
    AT["方法: byte getNextDeviceId()"]
    AU["方法: void setIdentityKey(IdentityKey identityKey)"]
    AV["方法: IdentityKey getIdentityKey(IdentityType identityType)"]
    AW["方法: void setPhoneNumberIdentityKey(IdentityKey phoneNumberIdentityKey)"]
    AX["方法: long getLastSeen()"]
    AY["方法: Optional<String> getCurrentProfileVersion()"]
    AZ["方法: void setCurrentProfileVersion(String currentProfileVersion)"]
    BA["方法: List<AccountBadge> getBadges()"]
    BB["方法: void setBadges(Clock clock, List<AccountBadge> badges)"]
    BC["方法: void addBadge(Clock clock, AccountBadge badge)"]
    BD["方法: void makeBadgePrimaryIfExists(Clock clock, String badgeId)"]
    BE["方法: void removeBadge(Clock clock, String id)"]
    BF["方法: void purgeStaleBadges(Clock clock)"]
    BG["方法: void setRegistrationLockFromAttributes(AccountAttributes attributes)"]
    BH["方法: void setRegistrationLock(String registrationLock, String registrationLockSalt)"]
    BI["方法: StoredRegistrationLock getRegistrationLock()"]
    BJ["方法: Optional<byte[]> getUnidentifiedAccessKey()"]
    BK["方法: void setUnidentifiedAccessKey(byte[] unidentifiedAccessKey)"]
    BL["方法: boolean isUnrestrictedUnidentifiedAccess()"]
    BM["方法: void setUnrestrictedUnidentifiedAccess(boolean unrestrictedUnidentifiedAccess)"]
    BN["方法: boolean isDiscoverableByPhoneNumber()"]
    BO["方法: void setDiscoverableByPhoneNumber(boolean discoverableByPhoneNumber)"]
    BP["方法: int getVersion()"]
    BQ["方法: void setVersion(int version)"]
    BR["方法: void setBackupCredentialRequests(byte[] messagesBackupCredentialRequest, byte[] mediaBackupCredentialRequest)"]
    BS["方法: Optional<byte[]> getBackupCredentialRequest(BackupCredentialType credentialType)"]
    BT["方法: BackupVoucher getBackupVoucher()"]
    BU["方法: void setBackupVoucher(BackupVoucher backupVoucher)"]
    BV["方法: boolean hasLockedCredentials()"]
    BW["方法: void lockAuthTokenHash()"]
    BX["方法: List<UsernameHold> getUsernameHolds()"]
    BY["方法: void setUsernameHolds(List<UsernameHold> usernameHolds)"]
    BZ["方法: void markStale()"]
    CA["方法: void requireNotStale()"]

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
    A --> N
    A --> O
    A --> P
    A --> Q
    A --> R
    A --> S
    A --> T
    A --> U
    A --> V
    A --> W
    A --> X
    A --> Y
    A --> Z
    A --> AA
    A --> AB
    A --> AC
    A --> AD
    A --> AE
    A --> AF
    A --> AG
    A --> AH
    A --> AI
    A --> AJ
    A --> AK
    A --> AL
    A --> AM
    A --> AN
    A --> AO
    A --> AP
    A --> AQ
    A --> AR
    A --> AS
    A --> AT
    A --> AU
    A --> AV
    A --> AW
    A --> AX
    A --> AY
    A --> AZ
    A --> BA
    A --> BB
    A --> BC
    A --> BD
    A --> BE
    A --> BF
    A --> BG
    A --> BH
    A --> BI
    A --> BJ
    A --> BK
    A --> BL
    A --> BM
    A --> BN
    A --> BO
    A --> BP
    A --> BQ
    A --> BR
    A --> BS
    A --> BT
    A --> BU
    A --> BV
    A --> BW
    A --> BX
    A --> BY
    A --> BZ
    A --> CA
```

这段代码定义了一个名为 `Account` 的类，该类包含了多个属性和方法，用于管理账户的相关信息。属性包括账户的唯一标识符、电话号码标识符、用户名哈希、设备列表、身份密钥等。方法则提供了对这些属性的访问和修改功能，例如获取和设置账户标识符、管理设备、处理账户徽章、设置注册锁等。代码中还包含了一些验证逻辑，确保在访问或修改账户信息时，账户状态是有效的。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| uuid | UUID | JSON属性映射UUID字段。 |
| logger = LoggerFactory.getLogger(Account.class) | Logger | 定义Account类的私有静态日志记录器实例。 |
| unrestrictedUnidentifiedAccess | boolean | 属性uua表示是否允许无限制的未识别访问。 |
| usernameLinkHandle | UUID | 可空属性usernameLinkHandle，类型为UUID。 |
| registrationLock | String | 属性registrationLock使用JsonProperty注解进行序列化。 |
| devices = new ArrayList<>() | List<Device> | 定义私有设备列表并初始化为空数组。 |
| badges = new ArrayList<>() | List<AccountBadge> | 私有属性badges为AccountBadge类型的列表，初始化为空ArrayList。 |
| number | String | JSON属性映射为私有字符串变量number。 |
| registrationLockSalt | String | 定义私有字符串变量registrationLockSalt，并使用JsonProperty注解。 |
| mediaBackupCredentialRequest | byte[] | 可空字节数组存储媒体备份凭证请求。 |
| phoneNumberIdentityKey | IdentityKey | PNI身份键的JSON序列化与反序列化配置。 |
| stale | boolean | 忽略JSON序列化的stale布尔字段。 |
| identityKey | IdentityKey | 使用IdentityKeyAdapter进行JSON序列化和反序列化的IdentityKey属性。 |
| reservedUsernameHash | byte[] | 使用注解处理Base64编码的可空字节数组。 |
| version | int | 使用JsonProperty注解标注私有整型变量version。 |
| phoneNumberIdentifier | UUID | 类中定义了一个私有UUID类型的电话号码标识符字段。 |
| encryptedUsername | byte[] | 属性encryptedUsername可为空，存储加密用户名字节数组。 |
| discoverableByPhoneNumber = true | boolean | 属性discoverableByPhoneNumber默认为true，用于控制电话号码可发现性。 |
| usernameHolds = Collections.emptyList() | List<UsernameHold> | 属性`usernameHolds`存储`UsernameHold`对象列表，默认为空列表。 |
| usernameHash | byte[] | 使用注解处理字节数组的Base64 URL编码与解码，支持空值。 |
| messagesBackupCredentialRequest | byte[] | 代码定义了一个可为空的字节数组变量messagesBackupCredentialRequest，使用JsonProperty注解标记为bcr。 |
| currentProfileVersion | String | 类中定义私有字符串变量currentProfileVersion，使用JsonProperty注解映射为cpv。 |
| unidentifiedAccessKey | byte[] | 代码定义了一个名为unidentifiedAccessKey的字节数组私有变量，并使用JsonProperty注解标记为uak。 |
| backupVoucher | BackupVoucher | Java类中定义了一个可空的BackupVoucher类型变量backupVoucher，并使用JsonProperty注解标记为"bv"。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| setCurrentProfileVersion | void | 设置当前配置文件版本，确保状态未过期。 |
| setDiscoverableByPhoneNumber | void | 设置是否通过电话号码可被发现。 |
| hasLockedCredentials | boolean | 检查所有设备是否锁定凭据。 |
| getUsernameHash | Optional<byte[]> | 方法返回可选的用户名哈希值，确保对象未过期。 |
| setPhoneNumberIdentityKey | void | 设置电话号码身份密钥。 |
| removeDevice | void | 删除指定ID的设备。 |
| getPrimaryDevice | Device | 获取主设备，若无则抛出异常。 |
| lockAuthTokenHash | void | 锁定所有设备的认证令牌哈希值。 |
| getUnidentifiedAccessKey | Optional<byte[]> | 获取未识别访问密钥，返回可选字节数组。 |
| getIdentifier | UUID | 根据身份类型返回对应的UUID或电话号码标识符。 |
| markStale | void | 标记对象为过时状态。 |
| setUuid | void | 方法设置UUID，确保对象未过期。 |
| getDevices | List<Device> | 获取设备列表前检查状态，返回设备集合。 |
| getLastSeen | long | 获取设备列表中最近一次活动时间，若无则返回0。 |
| getVersion | int | 获取版本号前检查状态，返回当前版本号。 |
| setUsernameLinkDetails | void | 方法设置用户名链接详情，验证参数一致性及字段状态。 |
| getBadges | List<AccountBadge> | 获取账户徽章列表，确保数据非过时。 |
| isDiscoverableByPhoneNumber | boolean | 该方法检查手机号是否可被发现，返回布尔值。 |
| getUsernameLinkHandle | UUID | 方法返回非空UUID，检查状态后返回usernameLinkHandle。 |
| setUsernameLinkHandle | void | 方法设置用户名链接句柄，确保对象未过期。 |
| getEncryptedUsername | Optional<byte[]> | 方法返回加密用户名，确保数据未过期。 |
| requireNotStale | void | 检查账户状态，若过期则记录错误。 |
| setRegistrationLockFromAttributes | void | 根据账户属性设置注册锁定，生成哈希和盐值。 |
| getBackupVoucher | BackupVoucher | 获取备份凭证，需确保数据未过期。 |
| getDevice | Optional<Device> | 根据设备ID获取设备对象，返回首个匹配项。 |
| setBadges | void | 设置徽章列表并清除过期徽章。 |
| getUsernameHolds | List<UsernameHold> | 该方法返回不可修改的用户名持有列表。 |
| setBackupCredentialRequests | void | 设置备份凭证请求，包括消息和媒体备份凭证请求。 |
| getNumber | String | 该方法返回非过期的数字值。 |
| setNumber | void | 设置号码和标识符，确保数据未过期。 |
| setUsernameHolds | void | 设置用户名持有列表，确保对象未过时。 |
| setUsernameHash | void | 设置用户名字节数组哈希值，确保数据未过期。 |
| hasCapability | boolean | 检查设备是否具备指定功能，支持主设备、任意设备和所有设备模式。 |
| getPhoneNumberIdentifier | UUID | 获取非过期的电话号码标识符。 |
| getUuid | UUID | 该方法返回账户的UUID，允许在过时账户上调用。 |
| getReservedUsernameHash | Optional<byte[]> | 获取保留用户名哈希值的可选方法，确保数据未过期。 |
| setVersion | void | 该方法设置版本号，确保对象未过期。 |
| removeBadge | void | 移除指定ID的徽章并清理过期徽章。 |
| addDevice | void | 方法`addDevice`先检查状态，移除旧设备后添加新设备。 |
| getIdentityKey | IdentityKey | 该方法根据身份类型返回对应的身份密钥。 |
| getBackupCredentialRequest | Optional<byte[]> | 获取备份凭证请求，根据类型返回相应凭证。 |
| addBadge | void | 方法添加或合并徽章，确保不重复并清除过期徽章。 |
| setRegistrationLock | void | 设置注册锁及其盐值，确保数据未过期。 |
| getCurrentProfileVersion | Optional<String> | 该方法返回当前配置版本，确保数据未过期。 |
| isUnrestrictedUnidentifiedAccess | boolean | 方法检查是否允许未识别访问，返回布尔值。 |
| purgeStaleBadges | void | 清除过期徽章，基于当前时间删除已过期的账户徽章。 |
| getRegistrationLock | StoredRegistrationLock | 获取注册锁信息，包含锁值、盐值和最后访问时间。 |
| getNextDeviceId | byte | 获取下一个可用设备ID，避免溢出并返回。 |
| setBackupVoucher | void | 设置备份凭证，检查状态后更新为指定值。 |
| makeBadgePrimaryIfExists | void | 方法检查并置顶指定徽章，移除过期徽章。 |
| setIdentityKey | void | 设置身份密钥，确保非过期状态。 |
| setUnrestrictedUnidentifiedAccess | void | 设置未识别访问权限，确保对象未过期。 |
| setReservedUsernameHash | void | 设置保留用户名哈希值，确保数据未过期。 |
| setUnidentifiedAccessKey | void | 设置未识别访问密钥的方法，确保状态有效。 |
| isIdentifiedBy | boolean | 该方法根据服务标识类型检查UUID或电话号码标识符是否匹配。 |




