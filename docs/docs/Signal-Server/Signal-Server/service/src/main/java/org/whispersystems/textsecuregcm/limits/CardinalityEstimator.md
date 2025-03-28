# 基础信息

|      |      |
|------|------|
| 名称 | CardinalityEstimator |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/limits/CardinalityEstimator.java |
| 包名 | org.whispersystems.textsecuregcm.limits |
| 依赖项 | ['com.google.common.annotations.VisibleForTesting', 'io.micrometer.core.instrument.Metrics', 'io.micrometer.core.instrument.Tags', 'java.time.Duration', 'java.util.concurrent.CompletableFuture', 'java.util.concurrent.CompletionStage', 'org.whispersystems.textsecuregcm.metrics.MetricsUtil', 'org.whispersystems.textsecuregcm.redis.FaultTolerantRedisClusterClient', 'org.whispersystems.textsecuregcm.util.Util'] |
| 概述说明 | CardinalityEstimator类通过Redis集群操作HyperLogLog，异步添加元素并更新本地计数。 |

# 说明

CardinalityEstimator类主要用于估算唯一元素的数量，它通过Redis集群操作HyperLogLog数据结构来实现这一功能。该类支持异步添加元素，并在添加后更新本地计数，从而高效地处理大规模数据的唯一性估算任务。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| CardinalityEstimator | class | CardinalityEstimator类用于估算唯一元素数量，通过Redis集群操作HyperLogLog数据结构，支持异步添加元素并更新本地计数。 |



## 类 CardinalityEstimator

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | CardinalityEstimator |
| 说明 | CardinalityEstimator类用于估算唯一元素数量，通过Redis集群操作HyperLogLog数据结构，支持异步添加元素并更新本地计数。 |


### UML类图

```mermaid
classDiagram
    class CardinalityEstimator {
        -double uniqueElementCount
        -FaultTolerantRedisClusterClient redisCluster
        -String hllName
        -Duration period
        +CardinalityEstimator(FaultTolerantRedisClusterClient redisCluster, String name, Duration period)
        +void add(String element)
        +CompletionStage~Void~ addAsync(String element)
        +long estimate()
    }

    class FaultTolerantRedisClusterClient {
        // 依赖的Redis集群客户端
    }

    CardinalityEstimator --> FaultTolerantRedisClusterClient : 依赖
```

**描述：**  
`CardinalityEstimator` 类用于估计集合中唯一元素的数量，通过 Redis 的 HyperLogLog 数据结构实现。它包含一个 `FaultTolerantRedisClusterClient` 实例，用于与 Redis 集群进行交互。`add` 方法用于同步添加元素，`addAsync` 方法用于异步添加元素，并更新本地唯一元素计数。`estimate` 方法用于返回当前估计的唯一元素数量。


### 内部方法调用关系图

```mermaid
graph TD
    A["类CardinalityEstimator"]
    B["属性: volatile double uniqueElementCount"]
    C["属性: final FaultTolerantRedisClusterClient redisCluster"]
    D["属性: final String hllName"]
    E["属性: final Duration period"]
    F["构造方法: CardinalityEstimator(FaultTolerantRedisClusterClient redisCluster, String name, Duration period)"]
    G["方法: void add(String element)"]
    H["方法: CompletionStage<Void> addAsync(String element)"]
    I["方法: long estimate()"]
    J["Metrics.gauge(MetricsUtil.name(getClass(), 'unique'), Tags.of('metricName', name), this, obj -> obj.uniqueElementCount)"]
    K["addAsync(element).toCompletableFuture().join()"]
    L["redisCluster.withCluster(connection -> connection.async().pfadd(hllName, element))"]
    M["thenCompose(modCount -> { if (modCount == 0) { return CompletableFuture.completedFuture(false); } return connection.async().pfcount(hllName).thenCompose(count -> { uniqueElementCount = count; return connection.async().ttl(hllName).thenApply(ttl -> ttl == -1); }); })"]
    N["thenCompose(isNewHll -> { if (!isNewHll) { return CompletableFuture.completedFuture(null); } return connection.async().expire(hllName, period).thenRun(Util.NOOP); })"]
    O["return (long) this.uniqueElementCount"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    F --> J
    G --> K
    H --> L
    L --> M
    M --> N
    I --> O
```

这段代码实现了一个基数估计器（CardinalityEstimator），用于估计集合中唯一元素的数量。它通过Redis的HyperLogLog数据结构来高效地计算基数，并在需要时更新本地视图和设置TTL。代码中包含了构造方法、添加元素的方法、异步添加元素的方法以及用于测试的估计方法。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| redisCluster | FaultTolerantRedisClusterClient | 私有终态的容错Redis集群客户端实例。 |
| hllName | String | 私有不可变字符串变量hllName。 |
| period | Duration | 私有不可变时间周期变量。 |
| uniqueElementCount | double | 私有易变双精度变量用于存储唯一元素数量。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| add | void | 异步添加元素并同步等待完成。 |
| estimate | long | 测试可见方法，返回唯一元素计数的长整型估计值。 |
| addAsync | CompletionStage<Void> | 异步添加元素到Redis集群的HyperLogLog，更新基数并设置TTL。 |




