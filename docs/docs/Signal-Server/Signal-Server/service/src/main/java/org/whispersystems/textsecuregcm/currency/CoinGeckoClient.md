# 基础信息

|      |      |
|------|------|
| 名称 | CoinGeckoClient |
| 编码语言 | .java |
| 代码路径 | Signal-Server/service/src/main/java/org/whispersystems/textsecuregcm/currency/CoinGeckoClient.java |
| 包名 | org.whispersystems.textsecuregcm.currency |
| 依赖项 | ['com.fasterxml.jackson.core.JsonProcessingException', 'com.fasterxml.jackson.core.type.TypeReference', 'com.google.common.annotations.VisibleForTesting', 'java.io.IOException', 'java.math.BigDecimal', 'java.net.URI', 'java.net.http.HttpClient', 'java.net.http.HttpRequest', 'java.net.http.HttpResponse', 'java.util.Locale', 'java.util.Map', 'org.slf4j.Logger', 'org.slf4j.LoggerFactory', 'org.whispersystems.textsecuregcm.util.SystemMapper'] |
| 概述说明 | CoinGeckoClient类用于获取加密货币现货价格，支持HTTP请求、API密钥和货币符号映射。 |

# 说明

CoinGeckoClient类是一个用于获取加密货币现货价格的工具，它集成了HTTP请求功能，支持API密钥的使用，并提供了货币符号的映射功能，以便准确识别和查询不同加密货币的价格信息。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| CoinGeckoClient | class | CoinGeckoClient类用于获取加密货币现货价格，包含HTTP请求、API密钥和货币符号映射。 |



## 类 CoinGeckoClient

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | CoinGeckoClient |
| 说明 | CoinGeckoClient类用于获取加密货币现货价格，包含HTTP请求、API密钥和货币符号映射。 |


### UML类图

```mermaid
classDiagram
    class CoinGeckoClient {
        -HttpClient httpClient
        -String apiKey
        -Map~String, String~ currencyIdsBySymbol
        -Logger logger
        -TypeReference~Map~String, Map~String, BigDecimal~~~ RESPONSE_TYPE
        +CoinGeckoClient(HttpClient httpClient, String apiKey, Map~String, String~ currencyIdsBySymbol)
        +BigDecimal getSpotPrice(String currency, String base) throws IOException
        +static Map~String, Map~String, BigDecimal~~ parseResponse(String responseJson) throws JsonProcessingException
        +static BigDecimal extractConversionRate(Map~String, BigDecimal~ response, String destinationCurrency) throws IOException
    }
    class HttpClient {
        <<Interface>>
        +HttpResponse~String~ send(HttpRequest request, HttpResponse.BodyHandler~String~ handler) throws IOException, InterruptedException
    }
    class HttpRequest {
        +static Builder newBuilder()
    }
    class HttpResponse {
        +String body()
        +int statusCode()
    }
    class JsonProcessingException {
        <<Exception>>
    }
    class IOException {
        <<Exception>>
    }
    CoinGeckoClient --> HttpClient : 依赖
    CoinGeckoClient --> HttpRequest : 依赖
    CoinGeckoClient --> HttpResponse : 依赖
    CoinGeckoClient --> JsonProcessingException : 依赖
    CoinGeckoClient --> IOException : 依赖
```

类图描述：
`CoinGeckoClient` 类用于与 CoinGecko API 进行交互，获取加密货币的现货价格。它依赖于 `HttpClient` 来发送 HTTP 请求，并使用 `HttpRequest` 和 `HttpResponse` 处理请求和响应。类中包含解析 JSON 响应和提取转换率的方法，并处理可能出现的 `JsonProcessingException` 和 `IOException` 异常。


### 内部方法调用关系图

```mermaid
graph TD
    A["类CoinGeckoClient"]
    B["属性: HttpClient httpClient"]
    C["属性: String apiKey"]
    D["属性: Map<String, String> currencyIdsBySymbol"]
    E["静态属性: Logger logger"]
    F["静态属性: TypeReference<Map<String, Map<String, BigDecimal>>> RESPONSE_TYPE"]
    G["构造方法: CoinGeckoClient(HttpClient httpClient, String apiKey, Map<String, String> currencyIdsBySymbol)"]
    H["方法: BigDecimal getSpotPrice(String currency, String base)"]
    I["方法: static Map<String, Map<String, BigDecimal>> parseResponse(String responseJson)"]
    J["方法: static BigDecimal extractConversionRate(Map<String, BigDecimal> response, String destinationCurrency)"]
    K["步骤: 检查currencyIdsBySymbol是否包含currency"]
    L["步骤: 创建URI quoteUri"]
    M["步骤: 发送HTTP请求"]
    N["步骤: 检查HTTP响应状态码"]
    O["步骤: 解析响应并提取转换率"]
    P["步骤: 处理InterruptedException异常"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    H --> K
    K -->|"否"| P
    K -->|"是"| L
    L --> M
    M --> N
    N -->|"成功"| O
    N -->|"失败"| P
    O --> I
    O --> J
```

**描述：**  
该流程图描述了`CoinGeckoClient`类的主要结构和功能。`CoinGeckoClient`类用于通过HTTP请求获取加密货币的现货价格。流程从`getSpotPrice`方法开始，首先检查传入的货币符号是否有效，然后构建请求URI并发送HTTP请求。根据响应状态码，决定是否继续解析响应并提取转换率，或者在请求失败时抛出异常。流程图还展示了类的构造方法和两个静态辅助方法`parseResponse`和`extractConversionRate`的调用关系。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| httpClient | HttpClient | 私有且不可变的HttpClient实例。 |
| currencyIdsBySymbol | Map<String, String> | 私有映射存储货币符号与ID对应关系。 |
| apiKey | String | 声明一个私有的不可变字符串变量apiKey。 |
| logger = LoggerFactory.getLogger(CoinGeckoClient.class) | Logger | CoinGeckoClient类中定义了一个静态且私有的Logger实例。 |
| RESPONSE_TYPE = new TypeReference<>() {} | TypeReference<Map<String, Map<String, BigDecimal>>> | 定义静态常量RESPONSE_TYPE，用于映射字符串键到嵌套的字符串与BigDecimal映射。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| extractConversionRate | BigDecimal | 从响应中提取指定货币的汇率，若不存在则抛出异常。 |
| getSpotPrice | BigDecimal | 获取指定货币的实时价格，处理异常和响应状态码。 |
| parseResponse | Map<String, Map<String,BigDecimal>> | 解析JSON响应并返回映射类型结果。 |




