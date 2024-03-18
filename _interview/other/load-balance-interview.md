---
title: "负载均衡"
sequence: "101"
---

## 负载均衡

- 硬件 负载均衡：F5
- 软件 负载均衡

## 四层和七层

### 概念

负载均衡主要分为四层和七层负载均衡，对应 osi 七层模型的四层和七层。

四层负载均衡工作在 OSI 模型的**传输层**，由于在传输层，只有 TCP/UDP 协议，这两种协议中除了包含源 IP、目标 IP 以外，还包含源端口号及目的端口号。

四层负载均衡服务器在接受到客户端请求后，以后通过修改数据包的地址信息（IP+ 端口号）将流量转发到应用服务器。

七层负载均衡工作在 OSI 模型的**应用层**，应用层协议较多，常用 http、radius、dns 等。
七层负载就可以基于这些协议来负载。这些应用层协议中会包含很多有意义的内容。
比如同一个 Web 服务器的负载均衡，除了根据 IP 加端口进行负载外，还可根据七层的 URL、浏览器类别、语言来决定是否要进行负载均衡。

简单来说，四层就是基于**IP+ 端口**的负载均衡；七层就是基于**URL**等应用层信息的负载均衡。

### 具体

- 四层代理（TCP）：LVS
- 七层代理（HTTP）：Nginx

|      | 四层负载均衡            | 七层负载均衡                |
|------|-------------------|-----------------------|
| 功能性  | 少                 | 多，支持资源压缩、更多策略         |
| 执行效率 | 高                 | 相对较低                  |
| 作用协议 | TCP               | HTTP、FTP、SMTP         |
| 应用场景 | 实时应用集群，大规模集群间数据交互 | Web 应用集群，需要更多额外功能的应用集群 |


## Nginx

Nginx 是一款轻量级的 Web 反向代理服务器，是目前使用最多的软件负载均衡器。

### Nginx 五种负载均衡策略

- 轮询策略（默认）
- 权重策略
- IP_HASH
- URL_HASH（第三方）
- FAIR（第三方）

## 客户端负载均衡器

- 服务器端负载均衡器
  - Nginx/F5/HaProxy，不支持动态扩展（例如，添加一个 Tomcat，需要修改 Nginx 的配置）