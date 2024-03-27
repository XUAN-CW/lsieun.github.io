---
title: "Java Cryptography"
image: /assets/images/java/crypto/java-crypto-cover.png
permalink: /java-crypto.html
---

Java Cryptography

密码测试：

- private key: privateKeyPass
- PKCS12 KeyStore: pkcs12StorePass
- JKS KeyStore: jksStorePass
- KeyPass: myKeyPass

## Bouncy Castle

- [PrimeKey](https://www.primekey.com/solutions/implementing-cryptography/)

## KeyStore

<table>
    <thead>
    <tr>
        <th>Basic</th>
        <th>API</th>
        <th>KeyTool</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>
{%
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/crypto/keystore/basic/'" |
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
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/crypto/keystore/java/'" |
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
assign filtered_posts = site.java |
where_exp: "item", "item.url contains '/java/crypto/keytool/'" |
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

## Reference

- [Java Security Standard Algorithm Names](https://docs.oracle.com/en/java/javase/21/docs/specs/security/standard-names.html)
- [Baeldung Security](https://www.baeldung.com/category/security)
    - [Java KeyStore API](https://www.baeldung.com/java-keystore)
- [Introduction to SSL in Java](https://www.baeldung.com/java-ssl)
- [KeyStore 加载 PublicKey/PrivateKey（公/私钥）证书](https://blog.csdn.net/xuri24/article/details/84302017)
- [Cheat Sheet - Java Keystores](https://megamorf.gitlab.io/cheat-sheets/java-keystores/)
- [NICS CRYPTOGRAPHY LIBRARY](https://www.nics.uma.es/developments/nics-cryptography-library/)
- [Cryptography Architecture Extensions](https://www.cs.fsu.edu/~jtbauer/cis3931/tutorial/security1.2/overview/index.html)
  讲 JCA 和 JCE 的关系
- [Exploring Java KeyStore & Keys](https://medium.com/javarevisited/exploring-java-keystore-keys-9eb4805fa4ec)
- [What is Keystore?](https://stackoverflow.com/questions/23202046/what-is-keystore)
- [Java Keytool - Generate CSR](https://support.globalsign.com/digital-certificates/digital-certificate-installation/java-keytool-generate-csr)
- [Java KeyStore](https://jenkov.com/tutorials/java-cryptography/keystore.html)

- [KeyStore Explorer](https://keystore-explorer.org/)

- Book
    - [Cryptography and Cryptanalysis in Java: Creating and Programming Advanced Algorithms with Java SE 17 LTS and Jakarta EE 10](https://www.oreilly.com/library/view/cryptography-and-cryptanalysis/9781484281055/)

