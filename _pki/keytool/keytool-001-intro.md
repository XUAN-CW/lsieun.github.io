---
title: "keytool Intro"
sequence: "101"
---

## What Is keytool?

keytool 位于 `${JDK_HOME}/bin`目录。

keytool 的主要作用是 **manage keys and certificates** and **store them in a keystore**

查看帮助：

```text
$ keytool --help
$ keytool -genkeypair --help
```

默认情况下，keystore 存储在 `${HOME}/.keystore` 文件：

```text
$ ls -l ${HOME}/.keystore
-rw-rw-r--. 1 devops devops 2710 Jul  4 08:25 /home/devops/.keystore
```

## Creating a Self-Signed Certificate

In order to **generate the certificate**, we're going to use `keytool` command with the `-genkeypair` option:

```text
$ keytool -genkeypair -keyalg RSA -keysize 2048 -alias <alias> -keypass <keypass> -validity <validity> -storepass <storepass>
```

- `alias` – the name for our certificate
- `keypass` – the password of the certificate. We'll need this password to have access to the private key of our certificate
- `validity` – the time (in days) of the validity of our certificate
- `storepass` – the password for the keystore. This will be the password of the keystore if the store doesn't exist

```text
$ keytool -genkeypair -keyalg RSA -keysize 2048 -alias lsieun.com -keypass 123456 -validity 365 -storepass abcdef
```

```text
$ keytool -genkeypair -keyalg RSA -alias myalias -keystore keystore.p12 -storetype PKCS12 -keypass mykeypassword -storepass mystorepassword
```

```text
$ keytool -genkeypair -keyalg RSA
Enter keystore password: abcdef 
Re-enter new password: abcdef
What is your first and last name?
  [Unknown]:  Sen Liu
What is the name of your organizational unit?
  [Unknown]:  IT
What is the name of your organization?
  [Unknown]:  Fruit Ltd
What is the name of your City or Locality?
  [Unknown]:  BaoDing
What is the name of your State or Province?
  [Unknown]:  HeBei
What is the two-letter country code for this unit?
  [Unknown]:  CN
Is CN=Sen Liu, OU=IT, O=Fruit Ltd, L=BaoDing, ST=HeBei, C=CN correct?
  [no]:  yes

Generating 2,048 bit RSA key pair and self-signed certificate (SHA256withRSA) with a validity of 90 days
	for: CN=Sen Liu, OU=IT, O=Fruit Ltd, L=BaoDing, ST=HeBei, C=CN
```

```text
$ keytool -list -v 
Enter keystore password:  
Keystore type: PKCS12
Keystore provider: SUN

Your keystore contains 1 entry
```

## Listing Certificates in the Keystore

```text
$ keytool -list -storepass <storepass>
```

```text
$ keytool -list -v -storepass <storepass>
```

## Reference

- [Introduction to keytool](https://www.baeldung.com/keytool-intro)
