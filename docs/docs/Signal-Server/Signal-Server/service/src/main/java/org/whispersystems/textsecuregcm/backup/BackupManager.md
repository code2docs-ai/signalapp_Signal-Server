# 基础信息

|      |      |
|------|------|
| 名称 | BackupManager |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/backup/BackupManager.java |
| 包名 | org.whispersystems.textsecuregcm.backup |
| 依赖项 | ['com.google.common.annotations.VisibleForTesting', 'io.dropwizard.util.DataSize', 'io.grpc.Status', 'io.micrometer.core.instrument.DistributionSummary', 'io.micrometer.core.instrument.Metrics', 'io.micrometer.core.instrument.Timer', 'java.security.SecureRandom', 'java.time.Clock', 'java.time.Duration', 'java.time.Instant', 'java.util.Base64', 'java.util.List', 'java.util.Map', 'java.util.Optional', 'java.util.concurrent.CompletableFuture', 'java.util.concurrent.CompletionStage', 'java.util.concurrent.atomic.AtomicLong', 'java.util.function.Function', 'org.signal.libsignal.protocol.ecc.Curve', 'org.signal.libsignal.protocol.ecc.ECPublicKey', 'org.signal.libsignal.zkgroup.GenericServerSecretParams', 'org.signal.libsignal.zkgroup.VerificationFailedException', 'org.signal.libsignal.zkgroup.backups.BackupAuthCredentialPresentation', 'org.signal.libsignal.zkgroup.backups.BackupCredentialType', 'org.signal.libsignal.zkgroup.backups.BackupLevel', 'org.whispersystems.textsecuregcm.attachments.AttachmentGenerator', 'org.whispersystems.textsecuregcm.attachments.TusAttachmentGenerator', 'org.whispersystems.textsecuregcm.auth.AuthenticatedBackupUser', 'org.whispersystems.textsecuregcm.limits.RateLimiters', 'org.whispersystems.textsecuregcm.metrics.MetricsUtil', 'org.whispersystems.textsecuregcm.util.AsyncTimerUtil', 'org.whispersystems.textsecuregcm.util.ExceptionUtils', 'org.whispersystems.textsecuregcm.util.Pair', 'reactor.core.publisher.Flux', 'reactor.core.publisher.Mono', 'reactor.core.scheduler.Scheduler'] |
| 概述说明 | BackupManager类管理备份操作，含认证、配额、上传、删除和恢复功能。 |

# 说明

BackupManager类是一个用于管理备份操作的工具，具备多种功能。它支持认证功能，确保用户权限验证。提供配额管理，用于监控和控制备份资源的使用情况。包含上传功能，允许用户将数据备份到指定位置。具备删除功能，用于移除不再需要的备份数据。还支持恢复功能，帮助用户从备份中还原数据。整体上，BackupManager类通过集成这些功能，全面管理和优化备份流程。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| BackupManager | class | BackupManager类用于管理备份操作，包括认证、配额、上传、删除和恢复功能。 |



## 类 BackupManager

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | BackupManager |
| 说明 | BackupManager类用于管理备份操作，包括认证、配额、上传、删除和恢复功能。 |


### UML类图

```mermaid
classDiagram
    class BackupManager {
        <<Interface>> PresentationSignatureVerifier
        +String MESSAGE_BACKUP_NAME
        +long MAX_TOTAL_BACKUP_MEDIA_BYTES
        +long MAX_MEDIA_OBJECT_SIZE
        +Duration MAX_QUOTA_STALENESS
        -int DELETION_CONCURRENCY
        -int COPY_CONCURRENCY
        -String ZK_AUTHN_COUNTER_NAME
        -String ZK_AUTHZ_FAILURE_COUNTER_NAME
        -String USAGE_RECALCULATION_COUNTER_NAME
        -String DELETE_COUNT_DISTRIBUTION_NAME
        -Timer SYNCHRONOUS_DELETE_TIMER
        -String SUCCESS_TAG_NAME
        -String FAILURE_REASON_TAG_NAME
        -BackupsDb backupsDb
        -GenericServerSecretParams serverSecretParams
        -RateLimiters rateLimiters
        -TusAttachmentGenerator tusAttachmentGenerator
        -Cdn3BackupCredentialGenerator cdn3BackupCredentialGenerator
        -RemoteStorageManager remoteStorageManager
        -SecureRandom secureRandom
        -Clock clock
        +BackupManager(BackupsDb, GenericServerSecretParams, RateLimiters, TusAttachmentGenerator, Cdn3BackupCredentialGenerator, RemoteStorageManager, Clock)
        +CompletableFuture~Void~ setPublicKey(BackupAuthCredentialPresentation, byte[], ECPublicKey)
        +CompletableFuture~BackupUploadDescriptor~ createMessageBackupUploadDescriptor(AuthenticatedBackupUser)
        +CompletableFuture~BackupUploadDescriptor~ createTemporaryAttachmentUploadDescriptor(AuthenticatedBackupUser)
        +CompletableFuture~Void~ ttlRefresh(AuthenticatedBackupUser)
        +CompletableFuture~BackupInfo~ backupInfo(AuthenticatedBackupUser)
        +Flux~CopyResult~ copyToBackup(AuthenticatedBackupUser, List~CopyParameters~)
        +Map~String, String~ generateReadAuth(AuthenticatedBackupUser, int)
        +CompletionStage~ListMediaResult~ list(AuthenticatedBackupUser, Optional~String~, int)
        +CompletableFuture~Void~ deleteEntireBackup(AuthenticatedBackupUser)
        +Flux~StorageDescriptor~ deleteMedia(AuthenticatedBackupUser, List~StorageDescriptor~)
        +CompletableFuture~AuthenticatedBackupUser~ authenticateBackupUser(BackupAuthCredentialPresentation, byte[])
        +Flux~StoredBackupAttributes~ listBackupAttributes(int, Scheduler)
        +Flux~ExpiredBackup~ getExpiredBackups(int, Scheduler, Instant)
        +CompletableFuture~Void~ expireBackup(ExpiredBackup)
        -CompletableFuture~QuotaResult~ enforceQuota(AuthenticatedBackupUser, List~CopyParameters~)
        -Mono~CopyResult~ copyToBackup(AuthenticatedBackupUser, CopyParameters)
        -static int indexWhereTotalExceeds(List~T~, Function~T, Long~, long)
        -static String encodeMediaIdForCdn(byte[])
        -static byte[] decodeMediaIdFromCdn(String)
        -static String cdnMessageBackupName(AuthenticatedBackupUser)
        -static String cdnMediaDirectory(AuthenticatedBackupUser)
        -static String cdnMediaPath(AuthenticatedBackupUser, byte[])
        -static String rateLimitKey(AuthenticatedBackupUser)
        -static void checkBackupLevel(AuthenticatedBackupUser, BackupLevel)
        -static void checkBackupCredentialType(AuthenticatedBackupUser, BackupCredentialType)
        -PresentationSignatureVerifier verifyPresentation(BackupAuthCredentialPresentation)
    }
    class UsageBatcher {
        -AtomicLong countDelta
        -AtomicLong usageDelta
        +void update(long)
    }
    class PresentationSignatureVerifier {
        <<Interface>>
        +Pair~BackupCredentialType, BackupLevel~ verifySignature(byte[], ECPublicKey)
    }
    class BackupsDb {
        <<Interface>>
        +CompletableFuture~Void~ setPublicKey(String, BackupLevel, ECPublicKey)
        +CompletableFuture~Void~ addMessageBackup(AuthenticatedBackupUser)
        +CompletableFuture~Void~ ttlRefresh(AuthenticatedBackupUser)
        +CompletableFuture~BackupDescription~ describeBackup(AuthenticatedBackupUser)
        +CompletableFuture~QuotaResult~ enforceQuota(AuthenticatedBackupUser, List~CopyParameters~)
        +CompletableFuture~Void~ trackMedia(AuthenticatedBackupUser, long, long)
        +CompletableFuture~Optional~AuthenticationData~~ retrieveAuthenticationData(String)
        +CompletableFuture~Void~ scheduleBackupDeletion(AuthenticatedBackupUser)
        +CompletableFuture~Void~ startExpiration(ExpiredBackup)
        +CompletableFuture~Void~ finishExpiration(ExpiredBackup)
        +Flux~StoredBackupAttributes~ listBackupAttributes(int, Scheduler)
        +Flux~ExpiredBackup~ getExpiredBackups(int, Scheduler, Instant)
    }
    class RemoteStorageManager {
        <<Interface>>
        +CompletableFuture~Void~ copy(int, byte[], long, EncryptionParameters, String)
        +CompletableFuture~Void~ delete(String)
        +CompletableFuture~ListResult~ list(String, Optional~String~, int)
        +CompletableFuture~Long~ calculateBytesUsed(String)
        +int cdnNumber()
    }
    class TusAttachmentGenerator {
        <<Interface>>
        +Descriptor generateAttachment(String)
    }
    class Cdn3BackupCredentialGenerator {
        <<Interface>>
        +BackupUploadDescriptor generateUpload(String)
        +Map~String, String~ readHeaders(String)
    }
    class RateLimiters {
        <<Interface>>
        +RateLimiter forDescriptor(For)
    }
    class BackupInfo {
        +int cdn
        +String backupSubdir
        +String mediaSubdir
        +String messageBackupKey
        +Optional~Long~ mediaUsedSpace
    }
    class CopyResult {
        +Outcome outcome
        +String destinationMediaId
        +Integer cdnNumber
    }
    class QuotaResult {
        +List~CopyParameters~ requestsToCopy
        +List~CopyParameters~ requestsToReject
    }
    class ListMediaResult {
        +List~StorageDescriptorWithLength~ media
        +Optional~String~ cursor
    }
    class ExpiredBackup {
        +String prefixToDelete
    }
    class StoredBackupAttributes {
        +String backupId
        +BackupLevel backupLevel
        +BackupCredentialType credentialType
        +String backupDir
        +String mediaDir
    }
    class BackupAuthCredentialPresentation {
        +String getBackupId()
        +BackupCredentialType getType()
        +BackupLevel getBackupLevel()
        +byte[] serialize()
        +void verify(Instant, GenericServerSecretParams)
    }
    class AuthenticatedBackupUser {
        +String backupId
        +BackupCredentialType credentialType
        +BackupLevel backupLevel
        +String backupDir
        +String mediaDir
    }
    class CopyParameters {
        +int sourceCdn
        +byte[] sourceKey
        +long sourceLength
        +EncryptionParameters encryptionParameters
        +String destinationMediaId
        +long destinationObjectSize
    }
    class StorageDescriptor {
        +int cdn
        +byte[] key
    }
    class StorageDescriptorWithLength {
        +int cdn
        +byte[] key
        +long length
    }
    class ECPublicKey {
        +boolean verifySignature(byte[], byte[])
    }
    class EncryptionParameters {
        +String algorithm
        +byte[] key
    }
    class RateLimiter {
        +CompletableFuture~Void~ validateAsync(String)
    }
    class Descriptor {
        +Map~String, String~ headers
        +String signedUploadLocation
    }
    class BackupUploadDescriptor {
        +int cdn
        +String key
        +Map~String, String~ headers
        +String signedUploadLocation
    }
    class BackupCredentialType {
        <<Enum>>
        +MESSAGES
        +MEDIA
    }
    class BackupLevel {
        <<Enum>>
        +FREE
        +PAID
    }
    class For {
        <<Enum>>
        +BACKUP_ATTACHMENT
    }
    class Scheduler {
        <<Interface>>
    }
    class Clock {
        <<Interface>>
        +Instant instant()
    }
    class GenericServerSecretParams {
        +byte[] serialize()
    }
    class Pair~A, B~ {
        +A first
        +B second
    }
    class Metrics {
        <<Interface>>
        +Counter counter(String, String, String)
        +Timer timer(String)
        +DistributionSummary builder(String)
    }
    class MetricsUtil {
        <<Interface>>
        +String name(Class~?~, String)
    }
    class DistributionSummary {
        <<Interface>>
        +void record(long)
    }
    class Counter {
        <<Interface>>
        +void increment()
    }
    class Timer {
        <<Interface>>
        +void record(Runnable)
    }
    class Status {
        <<Interface>>
        +RuntimeException withDescription(String)
        +RuntimeException withCause(Throwable)
        +RuntimeException asRuntimeException()
    }
    class VerificationFailedException {
        +String getMessage()
    }
    class PublicKeyConflictException {
        +String getMessage()
    }
    class PendingDeletionException {
        +String getMessage()
    }
    class ExceptionUtils {
        <<Interface>>
        +Function~Throwable, CompletableFuture~Void~~ exceptionallyHandler(Class~?~, Function~Throwable, CompletableFuture~Void~~)
    }
    class AsyncTimerUtil {
        <<Interface>>
        +CompletableFuture~Void~ record(Timer, Runnable)
    }
    class Base64 {
        <<Interface>>
        +String encodeToString(byte[])
        +byte[] decode(String)
    }
    class Curve {
        <<Interface>>
        +KeyPair generateKeyPair()
    }
    class KeyPair {
        +ECPublicKey getPublicKey()
    }
    class AtomicLong {
        +long get()
        +void set(long)
        +long incrementAndGet()
        +long decrementAndGet()
        +long addAndGet(long)
    }
    class Flux~T~ {
        <<Interface>>
        +Flux~T~ fromIterable(Iterable~T~)
        +Flux~T~ flatMapSequential(Function~T, Publisher~T~~, int)
        +Flux~T~ concat(Publisher~T~, Publisher~T~)
        +Flux~T~ usingWhen(Publisher~T~, Function~T, Publisher~T~~, Function~T, Publisher~Void~~)
        +Flux~T~ expand(Function~T, Publisher~T~~)
        +Flux~T~ flatMap(Function~T, Publisher~T~~, int)
        +Mono~Long~ count()
        +Mono~Void~ then()
    }
    class Mono~T~ {
        <<Interface>>
        +Mono~T~ fromCompletionStage(CompletionStage~T~)
        +Mono~T~ fromFuture(CompletableFuture~T~)
        +Mono~T~ just(T)
        +Mono~T~ empty()
        +Mono~T~ onErrorResume(Predicate~Throwable~, Function~Throwable, Mono~T~~)
        +Mono~T~ thenReturn(T)
        +Mono~T~ then(Mono~T~)
        +Mono~T~ doOnSuccess(Consumer~T~)
        +Mono~T~ doOnNext(Consumer~T~)
        +CompletableFuture~T~ toFuture()
    }
    class CompletableFuture~T~ {
        <<Interface>>
        +CompletableFuture~T~ exceptionally(Function~Throwable, T~)
        +CompletableFuture~T~ thenApply(Function~T, U~)
        +CompletableFuture~T~ thenCompose(Function~T, CompletableFuture~U~~)
        +CompletableFuture~T~ whenComplete(BiConsumer~T, Throwable~)
        +CompletableFuture~T~ thenApplyAsync(Function~T, U~, Executor)
        +CompletableFuture~T~ thenComposeAsync(Function~T, CompletableFuture~U~~, Executor)
        +CompletableFuture~T~ completedFuture(T)
        +CompletableFuture~T~ exceptionallyCompose(Function~Throwable, CompletableFuture~T~~)
    }
    class CompletionStage~T~ {
        <<Interface>>
        +CompletionStage~T~ thenApply(Function~T, U~)
        +CompletionStage~T~ thenCompose(Function~T, CompletionStage~U~~)
        +CompletionStage~T~ whenComplete(BiConsumer~T, Throwable~)
    }
    class Publisher~T~ {
        <<Interface>>
    }
    class Function~T, R~ {
        <<Interface>>
        +R apply(T)
    }
    class BiConsumer~T, U~ {
        <<Interface>>
        +void accept(T, U)
    }
    class Consumer~T~ {
        <<Interface>>
        +void accept(T)
    }
    class Predicate~T~ {
        <<Interface>>
        +boolean test(T)
    }
    class Executor {
        <<Interface>>
    }
    class Optional~T~ {
        <<Interface>>
        +boolean isPresent()
        +T get()
    }
    class List~T~ {
        <<Interface>>
        +int size()
        +T get(int)
        +List~T~ subList(int, int)
        +Stream~T~ stream()
    }
    class Stream~T~ {
        <<Interface>>
        +long count()
        +Stream~T~ map(Function~T, R~)
        +Stream~T~ filter(Predicate~T~)
        +Stream~T~ sorted(Comparator~T~)
        +Stream~T~ distinct()
        +Stream~T~ limit(long)
        +Stream~T~ skip(long)
        +Stream~T~ peek(Consumer~T~)
        +Stream~T~ flatMap(Function~T, Stream~R~~)
        +Stream~T~ mapToInt(ToIntFunction~T~)
        +Stream~T~ mapToLong(ToLongFunction~T~)
        +Stream~T~ mapToDouble(ToDoubleFunction~T~)
        +Stream~T~ boxed()
        +Stream~T~ parallel()
        +Stream~T~ sequential()
        +Stream~T~ unordered()
        +Stream~T~ onClose(Runnable)
        +void forEach(Consumer~T~)
        +void forEachOrdered(Consumer~T~)
        +T reduce(T, BinaryOperator~T~)
        +Optional~T~ reduce(BinaryOperator~T~)
        +R collect(Collector~T, A, R~)
        +R collect(Supplier~R~, BiConsumer~R, T~, BiConsumer~R, R~)
        +Optional~T~ min(Comparator~T~)
        +Optional~T~ max(Comparator~T~)
        +boolean anyMatch(Predicate~T~)
        +boolean allMatch(Predicate~T~)
        +boolean noneMatch(Predicate~T~)
        +Optional~T~ findFirst()
        +Optional~T~ findAny()
        +Iterator~T~ iterator()
        +Spliterator~T~ spliterator()
        +long count()
        +Object[] toArray()
        +A[] toArray(IntFunction~A[]~)
        +Stream~T~ concat(Stream~T~, Stream~T~)
        +Stream~T~ of(T...)
        +Stream~T~ empty()
        +Stream~T~ iterate(T, UnaryOperator~T~)
        +Stream~T~ generate(Supplier~T~)
        +Stream~T~ ofNullable(T)
        +Stream~T~ of(T)
        +Stream~T~ of(T, T)
        +Stream~T~ of(T, T, T)
        +Stream~T~ of(T, T, T, T)
        +Stream~T~ of(T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T, T)
        +Stream~T~ of(T, T, T, T, T


### 内部方法调用关系图

```mermaid
graph TD
    A["类BackupManager"]
    B["静态常量: MESSAGE_BACKUP_NAME"]
    C["静态常量: MAX_TOTAL_BACKUP_MEDIA_BYTES"]
    D["静态常量: MAX_MEDIA_OBJECT_SIZE"]
    E["静态常量: MAX_QUOTA_STALENESS"]
    F["静态常量: DELETION_CONCURRENCY"]
    G["静态常量: COPY_CONCURRENCY"]
    H["静态常量: ZK_AUTHN_COUNTER_NAME"]
    I["静态常量: ZK_AUTHZ_FAILURE_COUNTER_NAME"]
    J["静态常量: USAGE_RECALCULATION_COUNTER_NAME"]
    K["静态常量: DELETE_COUNT_DISTRIBUTION_NAME"]
    L["静态常量: SYNCHRONOUS_DELETE_TIMER"]
    M["静态常量: SUCCESS_TAG_NAME"]
    N["静态常量: FAILURE_REASON_TAG_NAME"]
    O["属性: BackupsDb backupsDb"]
    P["属性: GenericServerSecretParams serverSecretParams"]
    Q["属性: RateLimiters rateLimiters"]
    R["属性: TusAttachmentGenerator tusAttachmentGenerator"]
    S["属性: Cdn3BackupCredentialGenerator cdn3BackupCredentialGenerator"]
    T["属性: RemoteStorageManager remoteStorageManager"]
    U["属性: SecureRandom secureRandom"]
    V["属性: Clock clock"]
    W["构造方法: BackupManager"]
    X["方法: setPublicKey"]
    Y["方法: createMessageBackupUploadDescriptor"]
    Z["方法: createTemporaryAttachmentUploadDescriptor"]
    AA["方法: ttlRefresh"]
    AB["方法: backupInfo"]
    AC["方法: copyToBackup"]
    AD["方法: generateReadAuth"]
    AE["方法: list"]
    AF["方法: deleteEntireBackup"]
    AG["方法: deleteMedia"]
    AH["方法: authenticateBackupUser"]
    AI["方法: listBackupAttributes"]
    AJ["方法: getExpiredBackups"]
    AK["方法: expireBackup"]
    AL["方法: deletePrefix"]
    AM["内部类: UsageBatcher"]
    AN["内部接口: PresentationSignatureVerifier"]

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
```

**描述**：`BackupManager`类负责管理备份操作，包括设置公钥、创建备份上传描述符、刷新TTL、复制到备份、生成读取凭证、列出备份、删除备份等。该类通过多个静态常量定义配置参数，并通过多个方法实现具体的备份管理功能。内部类`UsageBatcher`用于跟踪媒体使用情况，内部接口`PresentationSignatureVerifier`用于验证签名。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| tusAttachmentGenerator | TusAttachmentGenerator | 私有Tus附件生成器实例。 |
| secureRandom = new SecureRandom() | SecureRandom | 使用SecureRandom生成安全随机数。 |
| serverSecretParams | GenericServerSecretParams | 私有不可变的服务器秘密参数对象。 |
| backupsDb | BackupsDb | 私有备份数据库实例。 |
| rateLimiters | RateLimiters | 私有且不可变的限流器实例。 |
| remoteStorageManager | RemoteStorageManager | 私有且不可变的远程存储管理器实例。 |
| SUCCESS_TAG_NAME = "success" | String | 定义静态常量SUCCESS_TAG_NAME，值为"success"。 |
| clock | Clock | 私有且不可变的时钟变量。 |
| COPY_CONCURRENCY = 10 | int | 定义了一个私有静态常量COPY_CONCURRENCY，值为10。 |
| MAX_QUOTA_STALENESS = Duration.ofDays(1) | Duration | 最大配额过期时间为1天。 |
| ZK_AUTHN_COUNTER_NAME = MetricsUtil.name(BackupManager.class, "authentication") | String | 定义ZK认证计数器名称为BackupManager类的认证指标。 |
| USAGE_RECALCULATION_COUNTER_NAME = MetricsUtil.name(BackupManager.class,      "usageRecalculation") | String | BackupManager类中定义了一个用于使用量重新计算的计数器变量。 |
| DELETION_CONCURRENCY = 10 | int | 静态常量DELETION_CONCURRENCY值为10，控制删除操作的并发数。 |
| MESSAGE_BACKUP_NAME = "messageBackup" | String | 定义静态常量MESSAGE_BACKUP_NAME，值为"messageBackup"。 |
| DELETE_COUNT_DISTRIBUTION_NAME = MetricsUtil.name(BackupManager.class,      "deleteCount") | String | 定义静态常量DELETE_COUNT_DISTRIBUTION_NAME，用于备份管理类删除计数指标名。 |
| INVALID_PUBLIC_KEY = Curve.generateKeyPair().getPublicKey() | ECPublicKey | 定义无效公钥常量，使用曲线生成密钥对的公钥。 |
| cdn3BackupCredentialGenerator | Cdn3BackupCredentialGenerator | 私有成员cdn3BackupCredentialGenerator，类型为Cdn3BackupCredentialGenerator。 |
| FAILURE_REASON_TAG_NAME = "reason" | String | 定义常量FAILURE_REASON_TAG_NAME，值为"reason"。 |
| SYNCHRONOUS_DELETE_TIMER =      Metrics.timer(MetricsUtil.name(BackupManager.class, "synchronousDelete")) | Timer | BackupManager类中定义了一个同步删除计时器SYNCHRONOUS_DELETE_TIMER。 |
| MAX_TOTAL_BACKUP_MEDIA_BYTES = DataSize.gibibytes(100).toBytes() | long | 常量MAX_TOTAL_BACKUP_MEDIA_BYTES表示最大备份媒体字节数为100GB。 |
| ZK_AUTHZ_FAILURE_COUNTER_NAME = MetricsUtil.name(BackupManager.class,      "authorizationFailure") | String | BackupManager类中定义了一个静态字符串常量，用于记录授权失败次数的计数器名称。 |
| MAX_MEDIA_OBJECT_SIZE = DataSize.mebibytes(101).toBytes() | long | 定义最大媒体对象大小为101MiB的字节数。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| ttlRefresh | CompletableFuture<Void> | 异步刷新免费备份用户的消息存储时间。 |
| decodeMediaIdFromCdn | byte[] | 该方法将CDN中的Base64编码字符串解码为字节数组。 |
| listBackupAttributes | Flux<StoredBackupAttributes> | 列出备份属性，调用数据库接口并返回结果。 |
| expireBackup | CompletableFuture<Void> | 异步执行备份过期操作，包括启动、删除和完成步骤。 |
| createTemporaryAttachmentUploadDescriptor | CompletableFuture<BackupUploadDescriptor> | 验证用户权限后生成临时附件上传描述符并返回。 |
| cdnMediaDirectory | String | 该方法返回备份用户媒体目录的路径。 |
| indexWhereTotalExceeds | int | 查找列表中元素累加值首次超过指定最大值的索引。 |
| cdnMediaPath | String | 静态方法生成CDN媒体路径，拼接用户目录与编码后的媒体ID。 |
| cdnMessageBackupName | String | 生成备份消息路径，格式为备份目录加消息备份名。 |
| deletePrefix | CompletableFuture<Void> | 异步删除指定前缀的远程存储对象，支持并发操作并记录删除数量。 |
| copyToBackup | Mono<CopyResult> | 异步备份方法，处理成功与错误结果，返回复制状态。 |
| getExpiredBackups | Flux<ExpiredBackup> | 获取过期备份数据，参数为分段数、调度器和清除时间。 |
| backupInfo | CompletableFuture<BackupInfo> | 方法备份用户信息，验证级别后从数据库获取描述并生成备份信息。 |
| setPublicKey | CompletableFuture<Void> | 设置公钥时验证签名，确保与现有公钥一致，否则抛出异常。 |
| authenticateBackupUser | CompletableFuture<AuthenticatedBackupUser> | 方法验证备份用户身份，检查签名并返回认证结果。 |
| deleteMedia | Flux<StorageDescriptor> | 删除媒体文件，检查用户权限和CDN支持，批量删除并更新配额。 |
| generateReadAuth | Map<String, String> | 生成读取认证，验证备份用户级别和CDN编号。 |
| enforceQuota | CompletableFuture<QuotaResult> | 检查用户备份配额，验证对象大小，计算剩余配额，更新使用情况并返回结果。 |
| verifyPresentation | PresentationSignatureVerifier | 验证备份认证凭证展示，失败时记录指标并抛出未认证异常。 |
| deleteEntireBackup | CompletableFuture<Void> | 删除用户备份，先检查权限，再尝试删除，失败则直接删除CDN对象。 |
| checkBackupLevel | void | 检查备份用户权限，若低于要求则记录错误并抛出权限异常。 |
| copyToBackup | Flux<CopyResult> | 验证备份用户权限和配额后，执行备份拷贝，处理成功或失败情况，并更新配额。 |
| checkBackupCredentialType | void | 检查备份凭证类型，若不符则增加计数器并抛出未认证异常。 |
| encodeMediaIdForCdn | String | 用于测试的静态方法，将字节数组编码为CDN媒体ID的Base64 URL字符串。 |
| list | CompletionStage<ListMediaResult> | 列出用户媒体文件，验证备份级别，返回带长度的存储描述符和游标。 |
| rateLimitKey | String | 生成基于备份用户ID的速率限制密钥。 |
| createMessageBackupUploadDescriptor | CompletableFuture<BackupUploadDescriptor> | 该方法为认证用户生成消息备份上传描述符，检查备份级别和凭证类型后，添加消息备份并生成上传凭证。 |




