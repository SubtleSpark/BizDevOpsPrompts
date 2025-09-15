# API接口分析演示

这是基于接口逻辑可视化的演示文档，展示如何将复杂的API接口逻辑通过图表清晰地呈现出来。

## 演示接口：订单支付处理

### 接口基础信息
- **接口路径**：POST /api/v1/orders/pay
- **服务名称**：订单服务
- **功能描述**：处理订单支付请求，调用支付服务完成扣款
- **请求参数**：
  - orderId：string - 订单ID
  - paymentMethod：string - 支付方式（alipay/wechat/card）
  - amount：number - 支付金额（分为单位）
- **响应结构**：
  - success：boolean - 支付是否成功
  - orderId：string - 订单ID
  - paymentId：string - 支付流水号
  - message：string - 处理结果描述

## 技术调用时序图（完整流程）

```mermaid
sequenceDiagram
    participant OrderService as 订单服务
    participant MySQL as 主数据库
    participant PaymentService as 支付服务
    participant Redis as 缓存服务
    participant RocketMQ as 消息队列
    
    Note over OrderService: 业务决策节点：开始处理订单支付请求
    
    OrderService->>MySQL: [DB-Query] orders表<br/>查询订单基础信息<br/>输入：orderId
    MySQL-->>OrderService: 返回：订单记录(status, amount, userId)
    
    Note over OrderService: 业务决策节点：验证订单状态
    alt 订单状态检查
        Note over OrderService: 业务决策：订单状态不允许支付
        OrderService-->>OrderService: 返回错误：订单状态异常
    else 订单状态正常
        Note over OrderService: 业务决策：调用支付服务处理扣款
        
        OrderService->>PaymentService: [API] POST /payment/charge<br/>调用支付服务扣款<br/>输入：orderId, amount, paymentMethod
        PaymentService-->>OrderService: 返回：支付结果(paymentId, status)
        
        Note over OrderService: 业务决策节点：根据支付结果处理订单
        alt 支付成功
            Note over OrderService: 业务决策：更新订单状态并发送通知
            
            par 并行处理支付成功任务
                OrderService->>MySQL: [DB-Update] orders表<br/>更新订单状态为已支付<br/>条件：orderId, paymentId
            and 缓存订单状态
                OrderService->>Redis: [Redis] order:status:{orderId}<br/>缓存订单支付状态<br/>数据：支付成功状态, TTL=7200s
            and 发送支付成功通知
                OrderService->>RocketMQ: [MQ] topic:order.payment tag:success<br/>发送支付成功通知<br/>消息：orderId, userId, paymentId
            end
            
        else 支付失败
            Note over OrderService: 业务决策：记录支付失败并通知
            
            par 并行处理支付失败任务
                OrderService->>MySQL: [DB-Update] orders表<br/>更新订单状态为支付失败<br/>条件：orderId, failReason
            and 缓存失败状态
                OrderService->>Redis: [Redis] order:status:{orderId}<br/>缓存订单失败状态<br/>数据：支付失败状态, TTL=1800s
            and 发送支付失败通知
                OrderService->>RocketMQ: [MQ] topic:order.payment tag:failed<br/>发送支付失败通知<br/>消息：orderId, userId, failReason
            end
        end
    end
```

## 业务逻辑流程图（简化版）

注意：此流程图从上方技术时序图中提取，只保留业务决策节点。

```mermaid
flowchart TD
    A[订单支付请求] --> B{验证订单状态:订单可支付?}
    B -->|否| C[返回订单状态异常错误]
    B -->|是| D[调用支付服务处理扣款]
    D --> E{支付处理结果:支付成功?}
    E -->|成功| F[更新订单状态为已支付]
    E -->|失败| G[记录支付失败原因]
    F --> H[发送支付成功通知]
    G --> I[发送支付失败通知]
```

**从时序图提取对应关系**：
- B节点 ↔️ 时序图中"业务决策节点：验证订单状态"
- D节点 ↔️ 时序图中"业务决策：调用支付服务处理扣款"
- E节点 ↔️ 时序图中"业务决策节点：根据支付结果处理订单"
- F节点 ↔️ 时序图中"业务决策：更新订单状态并发送通知"
- G节点 ↔️ 时序图中"业务决策：记录支付失败并通知"
- H/I节点 ↔️ 时序图中支付成功/失败分支的通知处理

## 关键业务逻辑说明

- **状态验证**：先验证订单是否处于可支付状态
- **外部调用**：通过RPC调用支付服务处理实际扣款
- **状态更新**：根据支付结果同步更新订单状态
- **异步通知**：通过消息队列发送处理结果通知
