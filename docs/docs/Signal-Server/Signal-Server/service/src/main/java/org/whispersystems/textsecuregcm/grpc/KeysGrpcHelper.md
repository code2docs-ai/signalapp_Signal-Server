# 基础信息

|      |      |
|------|------|
| 名称 | KeysGrpcHelper |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/grpc/KeysGrpcHelper.java |
| 包名 | org.whispersystems.textsecuregcm.grpc |
| 依赖项 | ['com.google.protobuf.ByteString', 'io.grpc.Status', 'org.signal.chat.common.EcPreKey', 'org.signal.chat.common.EcSignedPreKey', 'org.signal.chat.common.KemSignedPreKey', 'org.signal.chat.keys.GetPreKeysResponse', 'org.whispersystems.textsecuregcm.entities.ECPreKey', 'org.whispersystems.textsecuregcm.entities.ECSignedPreKey', 'org.whispersystems.textsecuregcm.entities.KEMSignedPreKey', 'org.whispersystems.textsecuregcm.identity.IdentityType', 'org.whispersystems.textsecuregcm.storage.Account', 'org.whispersystems.textsecuregcm.storage.Device', 'org.whispersystems.textsecuregcm.storage.KeysManager', 'reactor.core.publisher.Flux', 'reactor.core.publisher.Mono', 'reactor.util.function.Tuple2', 'reactor.util.function.Tuples'] |
| 概述说明 | KeysGrpcHelper类通过getPreKeys获取目标账户预密钥，支持所有或指定设备，返回EC和KEM预密钥。 |

# 说明

KeysGrpcHelper类中的getPreKeys方法用于获取目标账户的预密钥，支持获取所有设备或指定设备的预密钥。该方法返回的响应包含EC（椭圆曲线）和KEM（密钥封装机制）两种类型的预密钥。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| KeysGrpcHelper | class | KeysGrpcHelper类通过getPreKeys方法获取目标账户的预密钥，支持所有设备或指定设备，并返回包含EC和KEM预密钥的响应。 |



## 类 KeysGrpcHelper

|      |      |
|------|------|
| 访问范围 | None |
| 类型 | class |
| 名称 | KeysGrpcHelper |
| 说明 | KeysGrpcHelper类通过getPreKeys方法获取目标账户的预密钥，支持所有设备或指定设备，并返回包含EC和KEM预密钥的响应。 |


### UML类图

```mermaid
classDiagram
    class KeysGrpcHelper {
        +byte ALL_DEVICES
        +Mono~GetPreKeysResponse~ getPreKeys(Account targetAccount, IdentityType identityType, byte targetDeviceId, KeysManager keysManager)
    }

    class Account {
        +List~Device~ getDevices()
        +Optional~Device~ getDevice(byte deviceId)
        +IdentityKey getIdentityKey(IdentityType identityType)
        +Identifier getIdentifier(IdentityType identityType)
    }

    class Device {
        +int getId()
    }

    class KeysManager {
        +CompletableFuture~ECPreKey~ takeEC(Identifier identifier, int deviceId)
        +CompletableFuture~ECSignedPreKey~ getEcSignedPreKey(Identifier identifier, int deviceId)
        +CompletableFuture~KEMSignedPreKey~ takePQ(Identifier identifier, int deviceId)
    }

    class GetPreKeysResponse {
        +Builder newBuilder()
        +Builder putAllPreKeys(Map~Integer, PreKeyBundle~ preKeyBundles)
        +Builder setIdentityKey(ByteString identityKey)
    }

    class PreKeyBundle {
        +Builder newBuilder()
        +Builder setEcOneTimePreKey(EcPreKey ecPreKey)
        +Builder setEcSignedPreKey(EcSignedPreKey ecSignedPreKey)
        +Builder setKemOneTimePreKey(KemSignedPreKey kemSignedPreKey)
    }

    class EcPreKey {
        +Builder newBuilder()
        +Builder setKeyId(int keyId)
        +Builder setPublicKey(ByteString publicKey)
    }

    class ECSignedPreKey {
        +Builder newBuilder()
        +Builder setKeyId(int keyId)
        +Builder setPublicKey(ByteString publicKey)
        +Builder setSignature(ByteString signature)
    }

    class KemSignedPreKey {
        +Builder newBuilder()
        +Builder setKeyId(int keyId)
        +Builder setPublicKey(ByteString publicKey)
        +Builder setSignature(ByteString signature)
    }

    class IdentityKey {
        +byte[] serialize()
    }

    class Identifier {
    }

    class IdentityType {
    }

    KeysGrpcHelper --> Account : 依赖
    KeysGrpcHelper --> KeysManager : 依赖
    Account --> Device : 依赖
    Account --> IdentityKey : 依赖
    Account --> Identifier : 依赖
    KeysManager --> Identifier : 依赖
    GetPreKeysResponse --> PreKeyBundle : 依赖
    PreKeyBundle --> EcPreKey : 依赖
    PreKeyBundle --> ECSignedPreKey : 依赖
    PreKeyBundle --> KemSignedPreKey : 依赖
```

这段代码定义了一个 `KeysGrpcHelper` 类，用于处理与密钥管理相关的 gRPC 请求。`getPreKeys` 方法根据目标账户、设备ID和密钥管理器，获取并构建预密钥响应。该方法通过 Flux 和 Mono 处理异步操作，最终返回一个包含预密钥的 `GetPreKeysResponse` 对象。代码涉及多个类，如 `Account`、`Device`、`KeysManager` 等，它们共同协作完成密钥的获取和响应构建。


### 内部方法调用关系图

```mermaid
graph TD
    A["类KeysGrpcHelper"]
    B["静态常量: byte ALL_DEVICES = 0"]
    C["静态方法: Mono<GetPreKeysResponse> getPreKeys(Account targetAccount, IdentityType identityType, byte targetDeviceId, KeysManager keysManager)"]
    D["获取设备列表: Flux<Device> devices"]
    E["判断targetDeviceId == ALL_DEVICES"]
    F["获取所有设备: Flux.fromIterable(targetAccount.getDevices())"]
    G["获取指定设备: Flux.from(Mono.justOrEmpty(targetAccount.getDevice(targetDeviceId)))"]
    H["设备列表为空: switchIfEmpty(Mono.error(Status.NOT_FOUND.asException()))"]
    I["处理每个设备: flatMap(device -> Flux.merge(...))"]
    J["获取ECPreKey: Mono.fromFuture(() -> keysManager.takeEC(...))"]
    K["获取ECSignedPreKey: Mono.fromFuture(() -> keysManager.getEcSignedPreKey(...))"]
    L["获取KEMSignedPreKey: Mono.fromFuture(() -> keysManager.takePQ(...))"]
    M["合并结果: flatMap(Mono::justOrEmpty)"]
    N["构建GetPreKeysResponse.PreKeyBundle: reduce(...)"]
    O["处理ECPreKey: builder.setEcOneTimePreKey(...)"]
    P["处理ECSignedPreKey: builder.setEcSignedPreKey(...)"]
    Q["处理KEMSignedPreKey: builder.setKemOneTimePreKey(...)"]
    R["抛出异常: throw new AssertionError(...)"]
    S["映射设备ID: map(builder -> Tuples.of((int) device.getId(), builder.build()))"]
    T["收集结果: collectMap(Tuple2::getT1, Tuple2::getT2)"]
    U["构建最终响应: map(preKeyBundles -> GetPreKeysResponse.newBuilder().setIdentityKey(...).putAllPreKeys(...).build())"]

    A --> B
    A --> C
    C --> D
    D --> E
    E -->|是| F
    E -->|否| G
    D --> H
    H --> I
    I --> J
    I --> K
    I --> L
    J --> M
    K --> M
    L --> M
    M --> N
    N -->|ECPreKey| O
    N -->|ECSignedPreKey| P
    N -->|KEMSignedPreKey| Q
    N -->|其他| R
    N --> S
    S --> T
    T --> U
```

这段代码是`KeysGrpcHelper`类中的一个静态方法`getPreKeys`，用于获取指定账户的预密钥。方法首先根据设备ID获取设备列表，然后为每个设备获取不同类型的预密钥（ECPreKey、ECSignedPreKey、KEMSignedPreKey），并将这些预密钥合并构建成一个`GetPreKeysResponse`对象返回。流程图展示了从设备获取到最终响应构建的完整流程。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| ALL_DEVICES = 0 | byte | 定义静态常量ALL_DEVICES，值为0。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| getPreKeys | Mono<GetPreKeysResponse> | 获取目标账户设备的预密钥，合并并构建响应。 |




