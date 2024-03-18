---
title: "Difference Between a Java Keystore and a Truststore"
sequence: "104"
---

## Concepts

In most cases, we use a **keystore** and a **truststore** when our application needs to communicate over SSL/TLS.

Usually, these are **password-protected files** that sit on the same file system as our running application.
The default format used for these files was `JKS` until **Java 8**.

Since **Java 9**, the default keystore format is `PKCS12`.

The biggest difference between `JKS` and `PKCS12` is that **JKS is a format specific to Java**,
while **`PKCS12` is a standardized and language-neutral way of storing encrypted private keys and certificates.**

## Java KeyStore

**A Java keystore stores private key entries, certificates with public keys, or just secret keys**.
It stores each by an alias for ease of lookup.

Usually, **we'll use a keystore when we're a server and want to use HTTPS.**
During an SSL handshake, the server looks up the private key from the keystore,
and presents its corresponding public key and certificate to the client.

Similarly, if the client also needs to authenticate itself,
a situation called **mutual authentication**,
then the client also has a keystore and also presents its public key and certificate.

There's no default keystore, so if we want to use an encrypted channel,
we'll have to set `javax.net.ssl.keyStore` and `javax.net.ssl.keyStorePassword`.
If our keystore format is different from the default,
we could use `javax.net.ssl.keyStoreType` to customize it.

Of course, **we can use these keys to service other needs as well.**
Private keys can sign or decrypt data, and public keys can verify or encrypt data.
Secret keys can perform these functions as well.
A keystore is a place that we can hold onto these keys.

## Java TrustStore

A truststore is the opposite.
While a **keystore** typically holds onto certificates that identify us,
a **truststore** holds onto certificates that identify others.

In Java, we use it to trust the third party we're about to communicate with.

Take our earlier example. If a client talks to a Java-based server over HTTPS,
the **server** will look up the associated key from its **keystore** and
present the **public key** and **certificate** to the client.

```text
server --> keystore --> public key + certificate
```

We, the client, then look up the associated certificate in our **truststore**.
If the certificate or Certificate Authorities presented by the external server isn't in our truststore,
we'll get an `SSLHandshakeException`, and the connection won't be set up successfully.

```text
client --> truststore --> CA public certificate
```

Java has bundled a truststore called `cacerts`, and it resides in the `$JAVA_HOME/jre/lib/security` directory.

It contains default, trusted Certificate Authorities:

```text
$ keytool -list -keystore cacerts
Enter keystore password:
Keystore type: JKS
Keystore provider: SUN

Your keystore contains 92 entries

verisignclass2g2ca [jdk], 2018-06-13, trustedCertEntry,
Certificate fingerprint (SHA1): B3:EA:C4:47:76:C9:C8:1C:EA:F2:9D:95:B6:CC:A0:08:1B:67:EC:9D
```

We can see here that the truststore contains 92 trusted certificate entries and
one of the entries is the `verisignclass2gca` entry.
This means that the JVM will automatically trust certificates signed by `verisignclass2g2ca`.

We can override the default truststore location via the `javax.net.ssl.trustStore` property.
Similarly, we can set `javax.net.ssl.trustStorePassword` and `javax.net.ssl.trustStoreType`
to specify the truststore's password and type.

## Reference

- [Difference Between a Java Keystore and a Truststore](https://www.baeldung.com/java-keystore-truststore-difference)
- [Java KeyStore API](https://www.baeldung.com/java-keystore)
