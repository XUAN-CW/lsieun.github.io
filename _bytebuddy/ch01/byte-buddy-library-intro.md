---
title: "ByteBuddy 类库介绍"
sequence: "101"
---

## 功能介绍

**ByteBuddy is a library for generating Java classes dynamically at run-time.**

ByteBuddy 的主要功能：在 JVM 的运行过程（run-time）中，ByteBuddy 可以动态的（dynamically）生成 Java 类（generating Java classes）。

## 基本信息

ByteBuddy 作者：Rafael Winterhalter

ByteBuddy 开始时间：2014 年

ByteBuddy 网站：

```text
https://bytebuddy.net/
```

ByteBuddy Github 地址:

```text
https://github.com/raphw/byte-buddy/
```

ByteBuddy Logo：

{:refdef: style="text-align: center;"}
![](/assets/images/bytebuddy/byte-buddy-logo.png)
{:refdef}

## 类库依赖

**Byte Buddy is written on top of ASM**, a mature and well-tested library for reading and writing compiled Java classes.

在这里我们希望大家意识到：ByteBuddy 并不是一个独立的类库，它需要依赖于 ASM 类库。

{:refdef: style="text-align: center;"}
![](/assets/images/bytebuddy/bytebuddy-depends-on-asm.png)
{:refdef}

## 调用关系

一般情况下，我们编写 `.java` 文件，然后使用编译器（`javac`）来生成 `.class` 文件：

{:refdef: style="text-align: center;"}
![From Java to Class](/assets/images/java/javac-from-dot-java-to-dot-class.jpeg)
{:refdef}

当我们使用 ByteBuddy 来生成 `.class` 文件时，其整体思路如下：

{:refdef: style="text-align: center;"}
![](/assets/images/bytebuddy/java-bytebuddy-asm-classfile.png)
{:refdef}

- 起点和终点：Java 语言是我们开始的起点，最终生成的 ClassFile（`.class`）是我们的终点
- 过程：我们使用 Java 语言调用 ByteBuddy 的 API；ByteBuddy 会进一步调用 ASM 的 API；最后，ASM 来负责生成真正的 `.class` 文件。

## 总结

本文内容总结如下：

- 第一点，ByteBuddy 的**主要功能**：ByteBuddy 可以动态的生成 Java 类。
- 第二点，ByteBuddy 的**工作流程**：Java --> ByteBuddy --> ASM --> ClassFile

