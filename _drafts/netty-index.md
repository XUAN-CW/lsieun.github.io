---
title: "Netty"
image: /assets/images/netty/netty-cover.png
permalink: /netty.html
---

Netty is a non-blocking I/O client-server framework.

- Netty 基础
- Netty 常用协议
- Netty 优化
- Netty 源码解析

## Netty 基础

### 初始 Netty

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Basic</th>
        <th style="text-align: center;">Example</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/basic/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/example/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### Netty 核心组件

只有 `ChannelHandler` 是需要我们自己去编写的。

- [Netty 核心组件概览]({% link _netty/component/netty-component-index.md %})

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Data</th>
        <th style="text-align: center;" colspan="3">Network Layer</th>
        <th style="text-align: center;">Application Logic</th>
    </tr>
    <tr>
        <th style="text-align: center;">ByteBuf</th>
        <th style="text-align: center;">EventLoop</th>
        <th style="text-align: center;">Channel</th>
        <th style="text-align: center;">Future & Promise</th>
        <th style="text-align: center;">Handler & Pipeline</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/bytebuf/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/eventloop/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/channel/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/future/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/component/handler/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### 处理器详解

<table>
    <thead>
    <tr>
        <th style="text-align: center;">状态：连接和关闭</th>
        <th style="text-align: center;" colspan="3">数据：切割和转换</th>
    </tr>
    <tr>
        <th style="text-align: center;">网络连接（Connection）</th>
        <th style="text-align: center;">数据帧（Frame）</th>
        <th style="text-align: center;">解码器（Codec）</th>
        <th style="text-align: center;">序列化（Serialization）</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/handler/connection/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/handler/frame/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/handler/codec/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/handler/serde/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

## Netty 常用协议

### HTTP

<table>
    <thead>
    <tr>
        <th style="text-align: center;">SSL/TLS</th>
        <th style="text-align: center;">HTTP</th>
        <th style="text-align: center;">HTTP2</th>
        <th style="text-align: center;">HTTP3</th>
        <th style="text-align: center;">WebSocket</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/ssl/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/http/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/http2/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/http3/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/websocket/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### UDP

<table>
    <thead>
    <tr>
        <th style="text-align: center;">UDP</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/protocol/udp/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

## Netty 优化

### 选项参数

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Server</th>
        <th style="text-align: center;">Client</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/option/server/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/option/client/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### Extra

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Extra</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/extra/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

## Netty 源码解析

- [黑马 Netty 源码](https://www.bilibili.com/video/BV1py4y1E7oA?p=139)
- [Netty源码深入剖析](https://www.bilibili.com/video/BV1rS4y1v7Zw/)
- [尚硅谷Netty视频教程（B站超火，好评如潮）](https://www.bilibili.com/video/BV1DJ411m7NR/)
- [Netty开发实战 - 1](https://www.bilibili.com/video/BV1Fb4y137LD/)
- [Netty开发实战 - 2](https://www.bilibili.com/video/BV1Xk4y157XG/)


- [Netty4源码分析](https://www.zhihu.com/column/c_1715435263956979712)
- [Netty 核心原理剖析与 RPC 实践](https://www.bilibili.com/video/BV1e24y1z7eJ/)
- [Netty高手教程](https://www.bilibili.com/video/BV1uP411Q7aT/)
- [吃透netty，从原理到实战（2024最新版）](https://www.bilibili.com/video/BV16w4m1Z7ED/)
- [Netty源码剖析](https://www.bilibili.com/video/BV1yk4y117ae/)
- [Netty高手教程（源码剖析+多个项目实战）](https://www.bilibili.com/video/BV1uP411Q7aT/)
- [Netty全套教程](https://www.bilibili.com/video/BV1xq4y1q7Jj/)
- [深入理解netty](https://www.bilibili.com/video/BV1c4411J7Ty/)

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Basic</th>
        <th style="text-align: center;">Bootstrap</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/basic/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/bootstrap/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### EventLoop

<table>
    <thead>
    <tr>
        <th style="text-align: center;">Basic</th>
        <th style="text-align: center;">Selector</th>
        <th style="text-align: center;">Thread</th>
        <th style="text-align: center;">Task & TaskQueue</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/eventloop/basic/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/eventloop/selector/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/eventloop/thread/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
        <td>
{%
assign filtered_posts = site.netty |
where_exp: "item", "item.url contains '/netty/src/eventloop/task/'" |
sort: "sequence"
%}
<ol>
    {% for post in filtered_posts %}
    {% assign num = post.sequence | abs %}
    <li>
        <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
    {% endfor %}
</ol>
        </td>
    </tr>
    </tbody>
</table>

### 参考图

<table>
    <thead>
    <tr>
        <th style="text-align: center;">BootStrap</th>
        <th style="text-align: center;">Channel</th>
        <th style="text-align: center;">EventLoop</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
            <ul>
                <li><a href="/assets/images/netty/bootstrap/netty-invoke-java-nio-1.svg">Netty 调用 Java NIO（第一版）</a></li>
                <li><a href="/assets/images/netty/bootstrap/netty-invoke-java-nio-2.svg">Netty 调用 Java NIO（第二版）</a></li>
            </ul>
        </td>
        <td>
            <ul>
                <li><a href="/assets/images/netty/channel/netty-channel-classes-hierarchy.svg">Channel 类继承关系图</a></li>
            </ul>
        </td>
        <td>
            <ul>
                <li><a href="/assets/images/netty/eventloop/netty-eventloop-classes.svg">EventLoop 类继承关系图</a></li>
                <li><a href="/assets/images/netty/eventloop/thread/netty-eventloop-thread-1.svg">EventLoop 创建新线程1</a></li>
                <li><a href="/assets/images/netty/eventloop/thread/netty-eventloop-thread-2.svg">EventLoop 创建新线程2</a></li>
            </ul>
        </td>
    </tr>
    </tbody>
</table>

## Reference

- [lsieun/learn-java-netty](https://github.com/lsieun/learn-java-netty)

- [Netty](https://netty.io/)
    - [User guide for 4.x](https://netty.io/wiki/user-guide-for-4.x.html)

- [GitHub: netty/netty](https://github.com/netty/netty)
    - [4.1.x 示例](https://github.com/netty/netty/tree/4.1/example/src/main/java/io/netty/example)

- [Baeldung Tag: Netty](https://www.baeldung.com/tag/netty)
    - [Introduction to Netty](https://www.baeldung.com/netty)
    - [HTTP Server with Netty](https://www.baeldung.com/java-netty-http-server)
    - [HTTP/2 in Netty](https://www.baeldung.com/netty-http2)

- [Netty data model, threading, and gotchas](https://medium.com/@akhaku/netty-data-model-threading-and-gotchas-cab820e4815a)


- [Netty案例 的相关内容](https://cn.aliyun.com/sswb/389811.html)
- [netty 实现一个断点续传下载工具~支持http,websocket协议~](https://blog.csdn.net/myth_g/article/details/104007384)
- [Netty实现HTTP协议下的断点续传](https://zhoutzzz.top/archives/netty-shi-xian-http-xie-yi-xia-de-duan-dian-xu-chuan)
- [netty案例，netty4.1中级拓展篇四《Netty传输文件、分片发送、断点续传》](https://bbs.huaweicloud.com/blogs/262673)
- [netty文件上传断点续传的演示](https://blog.csdn.net/shuixiou1/article/details/114947474)
- [netty案例，netty4.1中级拓展篇四《Netty传输文件、分片发送、断点续传》](https://developer.aliyun.com/article/854004)
- [netty文件上传断点续传的演示](https://blog.csdn.net/shuixiou1/article/details/114947474)
- [Netty实战: HTTP文件列表服务器](https://developer.aliyun.com/article/1469464)
- [netty 详解（四）netty 开发 WebSocket 长连接程序](https://www.cnblogs.com/xy-ouyang/p/12825111.html)
- [Netty 轻松实现文件上传功能](https://m.jb51.net/article/216822.htm)
- Zero Copy
    - [Is Netty's Zero Copy different from OS level Zero Copy?](https://stackoverflow.com/questions/20727615/is-nettys-zero-copy-different-from-os-level-zero-copy)
- 上传下载
    - [netty下载大文件](https://juejin.cn/s/netty%E4%B8%8B%E8%BD%BD%E5%A4%A7%E6%96%87%E4%BB%B6)
    - [Netty 4中ChunkedWriteHandler与HttpContentCompressor冲突导致不压缩的问题](https://blog.csdn.net/flyinmind/article/details/130243747)
    - [Netty - How to combine ChunkedWriteHandler with HttpContentCompressor](https://stackoverflow.com/questions/18982925/netty-how-to-combine-chunkedwritehandler-with-httpcontentcompressor)
    - [Resumable File Download Protocol](https://stackoverflow.com/questions/6872342/resumable-file-download-protocol)
- WebSocket
    - [Netty websocket chat](https://danielzielinskitech.medium.com/netty-websocket-chat-cb06061d8274)
- 源码分析
    - [Netty源码分析-ChunkedFile和ChunkedWriteHandler](https://blog.csdn.net/nimasike/article/details/105741173)
    - [Netty源码分析-ChunkedFile和ChunkedWriteHandler](https://blog.51cto.com/u_11868971/4907471)

- [Build Your Own Netty — Foreword](https://kezhenxu94.medium.com/build-your-own-netty-foreword-8bc1f9129221)
- [Build Your Own Netty — Start from BIO](https://kezhenxu94.medium.com/build-your-own-netty-start-from-bio-437ab5bbe000)

- [Keith](https://medium.com/@xuezhongyu01)
    - [Netty Source Code Analysis-Packet Sticking And Unpacking Issues](https://towardsdev.com/netty-source-code-analysis-packet-sticking-and-unpacking-issues-068be62b0cee)
    - [Netty Source Code Analysis-ByteBuf](https://towardsdev.com/netty-source-code-analysis-bytebuf-ab279d9f082d)
    - [Netty Source Code Analysis — NioEventLoop Event Processing](https://blog.stackademic.com/netty-source-code-analysis-nioeventloop-event-processing-95fbccd1e837)
    - [Netty Source Code Analysis-Accept Process Analysis](https://towardsdev.com/netty-source-code-analysis-accept-process-analysis-a0cf0e29357c)
    - [Netty Source Code Analysis — Register Analysis](https://towardsdev.com/netty-source-code-analysis-register-analysis-fe6fe7983481)
    - [Netty Source Code Analysis-EventLoop Class Relationship](https://towardsdev.com/netty-source-code-analysis-eventloop-class-relationship-b0305aaa29d5)
    - [Netty Source Code Analysis-ChannelHandler](https://towardsdev.com/netty-source-code-analysis-channelhandler-a001bba4a62c)
    - [Netty Source Code Analysis — Bootstrap Server](https://towardsdev.com/netty-source-code-analysis-bootstrap-server-36c0a3d3bd6d)
    - [Netty Source Code Analysis — Bootstrap Client](https://towardsdev.com/netty-source-code-analysis-bootstrap-client-eb4aebaaaa26)
    - [Analyzing the unSafe.write Method in Netty Source Code](https://aws.plainenglish.io/analyzing-the-unsafe-write-method-in-netty-source-code-c0082835b281)
    - [Understanding the Acceptance Process in Netty: A Deep Dive into the Source Code](https://medium.com/javarevisited/understanding-the-acceptance-process-in-netty-a-deep-dive-into-the-source-code-a6dfc28bc48a)
    - [Thoughts On Netty Source Code Reading —How To Deal With Time-Consuming Business](https://medium.com/illumination/thoughts-on-netty-source-code-reading-how-to-deal-with-time-consuming-business-58c9f4a7edc5)
    - [Netty Tutorial: EchoServer](https://medium.com/backenders-club/netty-tutorial-echoserver-93e57400e34a)
    - [Netty High-Performance Way FastThreadLocal Source Code Analysis](https://medium.com/the-random-nerdiness-collective/netty-high-performance-way-fastthreadlocal-source-code-analysis-8be4f05bc234)
    - [Netty Memory Recycling Strategy—noCleaner](https://aws.plainenglish.io/netty-memory-recycling-strategy-nocleaner-f39da85498cf)
    - [Netty Core Component Pipeline Source Code Analysis (2) A Requested Pipeline Journey](https://aws.plainenglish.io/netty-core-component-pipeline-source-code-analysis-2-a-requested-pipeline-journey-3fd3a9983782)
    - [Netty Accepts Request Process Source Code Analysis (based on 4.1.23)](https://medium.com/javarevisited/netty-accepts-request-process-source-code-analysis-based-on-4-1-23-e7b74b76376e)
    - [Netty outbound buffer ChannelOutboundBuffer source code analysis](https://aws.plainenglish.io/netty-outbound-buffer-channeloutboundbuffer-source-code-analysis-176c6ecbb00)
    - [Implement a simple RPC with Netty yourself](https://aws.plainenglish.io/implement-a-simple-rpc-with-netty-yourself-e37cec418048)
    - [Netty Learning Journey — — Introduction to ByteBuf Source Code](https://medium.com/the-random-nerdiness-collective/netty-learning-journey-introduction-to-bytebuf-source-code-d1eda7d40933)
    - [Netty Learning Journey: ByteBuf Internal Structure and API Learning in ByteBuf](https://medium.com/illumination/netty-learning-journey-bytebuf-internal-structure-and-api-learning-in-bytebuf-f39612ab4762)

- [Understanding the Netty Network Framework](https://dlcoder.medium.com/understanding-the-netty-network-framework-5647e505d01e)
- [Netty #01 Discard, Echo Service](https://medium.com/@jc3wrld999/netty-1-discard-echo-service-3f1467af5284)
- [A Tour of Netty](https://medium.com/geekculture/a-tour-of-netty-5020ecee5494)
- [Netty object pool & recycling](https://medium.com/@ramu.ramaiah/netty-object-pool-recycling-68e0f35775cd)
- [Memory management for high performance Java applications](https://medium.com/@ramu.ramaiah/memory-management-for-high-performance-java-applications-a797bb09984a)
- [Are you tired of Java Frameworks Yet?](https://raypvn.medium.com/are-you-tired-of-java-frameworks-yet-3af36d1d134)
- [Netty reloading SSL/TLS certificate](https://goldius.medium.com/netty-reloading-ssl-tls-certificate-2078cdf6bfc1)
- [Netty NIO Distilled](https://medium.com/swlh/netty-nio-distilled-c1f053911950)
- [Netty Simple TCP Server](https://thebackendguy.medium.com/netty-simple-tcp-server-51fa8537fad5)

- [黑马程序员Netty全套教程](https://www.bilibili.com/video/BV1py4y1E7oA/)
    - [文档](https://nyimac.gitee.io/2021/04/25/Netty%E5%9F%BA%E7%A1%80/)

- [GitHub: beardlessCat/im](https://github.com/beardlessCat/im)

- [木心](https://www.cnblogs.com/xy-ouyang)
    - [netty 详解（一）架构设计、异步模型、任务队列、入门案例](https://www.cnblogs.com/xy-ouyang/p/12820107.html)
    - [netty 详解（二）netty 实现群聊](https://www.cnblogs.com/xy-ouyang/p/12824998.html)
    - [netty 详解（三）netty 心跳检测机制案例](https://www.cnblogs.com/xy-ouyang/p/12825058.html)
    - [netty 详解（四）netty 开发 WebSocket 长连接程序](https://www.cnblogs.com/xy-ouyang/p/12825111.html)
    - [netty 详解（五）netty 使用 protobuf 序列化](https://www.cnblogs.com/xy-ouyang/p/12825132.html)
    - [netty 详解（六）netty 自定义编码解码器](https://www.cnblogs.com/xy-ouyang/p/12827228.html)
    - [netty 详解（七）netty 自定义协议解决 TCP 粘包和拆包](https://www.cnblogs.com/xy-ouyang/p/12829165.html)
    - [netty 详解（八）基于 Netty 模拟实现 RPC](https://www.cnblogs.com/xy-ouyang/p/12829211.html)

- [Netty demos. （Netty 案例大全）](https://github.com/waylau/netty-4-user-guide-demos)
- [JMCuixy/NettyDemo](https://github.com/JMCuixy/NettyDemo)
    - [example](https://github.com/JMCuixy/NettyDemo/tree/master/src/main/java/org/netty/demo)

- [Netty 系列八（基于 WebSocket 的简单聊天室）](https://www.cnblogs.com/jmcui/p/9600533.html)
- [Netty 系列九（支持UDP协议）](https://www.cnblogs.com/jmcui/p/9636505.html)

- [StudyNotes](https://bright-boy.gitee.io/technical-notes/#/)
    - [来自于尚硅谷Netty精讲](https://bright-boy.gitee.io/technical-notes/#/%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/%E5%B0%9A%E7%A1%85%E8%B0%B7Netty)
    - [来自于黑马Netty精讲](https://bright-boy.gitee.io/technical-notes/#/%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/netty)
    - [Socket基础](https://bright-boy.gitee.io/technical-notes/#/%E7%BD%91%E7%BB%9C%E7%BC%96%E7%A8%8B/socket)
