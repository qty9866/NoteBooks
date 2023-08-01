# Go语言容器实战

## 1. 微服务介绍与容器化入门

- #### **什么是微服务**

  - 是一种架构模式
  - 相比于单体架构，微服务架构更加独立，能够单独的更新和发布
  - 微服务仅仅用于一个特定的业务功能

- #### `DDD` (Domain Driven Design)

  - 领域驱动设计
  - 康威定律：**组织---对应--->微服务拆分**

- #### `DDD`的作用

  - 有助于指导我们确定系统边界
  - 能够聚焦在系统核心元素上
  - 帮助我们拆分系统

- #### `DDD`常用概念

  - 领域：领域是有范围边界的，也可以说是有边界的
  - 核心域：核心域是业务系统的核心价值
  - 通用子域：所有子域的消费者，提供着通用服务
  - 支撑子域：专注于业务系统的某一特定业务

- #### 界限上下文

  - 方式：领域+上下文
  - 目的：不在于如何划分边界，为在于如何控制边界

- #### 领域模型

  - 理解：领域模型是对于我们软件系统中要解决的问题的抽象表达
  - 领域：反映的是我们业务上要解决的问题

- #### **四层架构**

![](C:\Users\Hud\Desktop\文件（需要）\截图\四层架构.png)

- #### 微服务架构

  ![](C:\Users\Hud\Desktop\文件（需要）\截图\微服务架构.png)

- #### RPC(Remote Procedure Call)

  - 远程过程调用
  - 包含了传输协议&编码（对象序列号）协议
  - 允许运行于一台计算机的程序调用另一台计算机的子程序（Redis）

- #### GRPC

  - 高性能、开源、通用的RPC框架
  - 基于HTTP 2.0 协议标准的设计开发
  - 支持多语言，默认采用Protocol Buffers数据序列化协议

- #### GRPC基本调用流程

  ![](C:\Users\Hud\Desktop\文件（需要）\截图\GRPC基本调用流程.png)

![](C:\Users\Hud\Desktop\文件（需要）\截图\grpc调用.png)

- #### 什么是Protocol Buffers?

  - 是一种轻便高效的序列化结构化数据的协议
  - 通常用在存储数据和需要远程数据通信的程序上
  - 跨语言，更小更快也更简单

- #### 为什么要使用Protocol Buffers？

  - 加速站点之间的传输速度
  - 解决数据之间传输不规范问题

- #### Protocol Buffers常用概念

  - Message 定义：描述了一个请求或响应的消息格式
  -  字段标识：消息的定义中，每个字段都有一个惟一的数值标签
  - 常用的数据类型：`double`，`float`，`int32/64`，`bool`，`string`，`bytes`
  - Service 服务定义：在Service中可以定义一个`RPC`服务接口

- #### Protocol Buffers Message中字段修饰符

  - singular：表示成员有0个或者1个，一般省略不写
  - repeated：表示该字段可以包含0~N个元素（理解为Go中的数组或者切片）

  ```protobuf
  syntax = "proto3";
  
  package go.micro.service.product;
  
  service Product{
      rpc AddProduct(ProductInfo) returns(ResponseProduct){}
  }
  
  message ProductInfo {
      int64 id = 1 ;    // 1:字段标识符
      string product_name = 2;  //尽量1~15
  }
  
  message ResponseProduct {
      int64 product_id = 1;
  }
  ```

- #### Micro是什么

  - 用来构建和管理分布式程序的系统
  - Runtime（运行时）：用来配置管理、认证，网络等
  - Clients（多语言客户端）：支持多语言访问服务端
  - Framework（程序开发框架）：用来方便编写微服务

- #### Micro中Runtime介绍

  - 工具集，工具名称是“micro”

  - 官方docker版本是

    ```bash
    docker pull micro/micro
    ```

- Runtime的组成

  - api：api网关
  - broker：允许异步消息的消息代理
  - network：通过微网络构建多云网络
  - new：服务模板生成器
  - proxy：建立在Go Micro上的透明服务代理