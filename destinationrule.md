

配置示例如下：

```
  trafficPolicy:  
    loadBalancer:  
      simple: ROUND_ROBIN  
    connectionPool:  
      http:  
        http1MaxPendingRequests: 1024  
        maxRequestsPerConnection: 10  
      tcp:  
        maxConnections: 1024  
    outlierDetection:  
      consecutiveErrors: 10  
      interval: 10s  
      baseEjectionTime: 1m  
      maxEjectionPercent: 100  
```

在这个示例中，`trafficPolicy` 属性包含了以下设置：

1. `loadBalancer`: 定义负载均衡策略。在此示例中，使用 `simple: ROUND_ROBIN` 设置，表示使用轮询（round-robin）策略进行负载均衡。

2. ```
   connectionPool
   ```

   : 定义连接池设置。在此示例中，有两部分设置：

   - ```
     http
     ```

     : 针对 HTTP 连接的设置。

     - `http1MaxPendingRequests`: 允许的最大挂起请求数（默认值为 1024）。
     - `maxRequestsPerConnection`: 每个连接允许的最大请求数（默认值为 1024）。

   - ```
     tcp
     ```

     : 针对 TCP 连接的设置。

     - `maxConnections`: 允许的最大连接数（默认值为 1024）。

3. ```
   outlierDetection
   ```

   : 定义异常检测策略。在此示例中，有以下设置：

   - `consecutiveErrors`: 连续出错次数阈值。当实例连续出错次数超过阈值时，将被暂时从负载均衡池中移除（默认值为 5）。

   - `interval`: 异常检测扫描间隔（默认值为 10s）。

   - `baseEjectionTime`: 实例被移除负载均衡池的最小持续时间（默认值为 30s）。

   - `maxEjectionPercent`: 可被移除负载均衡池的最大实例百分比（默认值为 10%）。

     通过在 `DestinationRule` 配置中定义 `trafficPolicy`，您可以为特定服务指定全局的流量策略，从而提高应用程序的性能、可用性和容错能力。根据您的需求和场景调整这些设置以获得最佳效果。