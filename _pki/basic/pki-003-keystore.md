---
title: "KeyStore: JKS + PKCS12"
sequence: "103"
---

A **Java KeyStore** is a container of security certificates that we can use when writing Java code.

Java KeyStores hold one or more certificates with their matching private keys and
are created using `keytool` which comes with the JDK.



- Java 8 及以前的版本，默认使用 JKS 格式
- Java 9 及以后的版本，默认使用 PKCS12 格式

## JKS 与 PKCS 的区别

The JKS file format is a **proprietary format** that is specifically for use in Java programs.

`PKCS#12` KeyStores are **non-proprietary** and are increasing in popularity.

## cacerts

By default, Java has a keystore file located at `JAVA_HOME/jre/lib/security/cacerts`.
We can access this keystore using the default keystore password `changeit`.

在 JDK 17 中，`cacerts` 位于：

```text
JDK_HOME/lib/security/cacerts
```

第一种方式，查看内容（任意目录）：

```text
$ keytool -list -cacerts
```

第二种方式，在 `JDK_HOME/lib/security/` 目录

```text
$ keytool -list -keystore cacerts 
Warning: use -cacerts option to access cacerts keystore
Enter keystore password: changeit
```

