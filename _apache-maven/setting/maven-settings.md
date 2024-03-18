---
title: "Maven Settings"
sequence: "104"
---

Open the `settings.xml` file in the `.m2` subfolder of your `HOME` folder, if it exists:

```text

```

Otherwise, open the `settings.xml` file in the `conf` folder of your Maven installation (as defined in `M2_HOME`).

## 两个配置文件

### Maven Global Settings

The `/conf` folder of the Maven installation directory contains a `settings.xml` file
that can be edited to customize some configuration properties used during our builds.
This file is also referred to as the **Maven Global Settings** file.

### Maven Local Settings

We can override these settings in a `settings.xml` file that we can create in the `~/.m2/` folder.
While the Global Settings file is used by all the users of the same machine,
the file under `~/.m2/` is used only by the local user, and it is called the **Maven Local Settings** file.

## 配置哪些内容

In the Maven settings, we can specify some properties and flags, as follows:

The path of the local repository. This is `~/.m2/repository` by default.

```text
<localRepository>/path/to/local/repo</localRepository>
```

The offline flag prevents Maven from connecting to remote repositories
(useful in case of network problems).

```text
<offline>false</offline>
```

The `<proxies>` element allows us to configure proxies used to connect to the network.

```xml
<proxies>
    <!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
    -->
    <proxy>
        <id>optional</id>
        <active>true</active>
        <protocol>http</protocol>
        <username>proxyuser</username>
        <password>proxypass</password>
        <host>proxy.host.net</host>
        <port>80</port>
        <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
</proxies>
```

The `<servers>` element allows us to specify the credentials of the Maven repositories
to which we want to deploy our artifacts.

```xml
<!-- servers
 | This is a list of authentication profiles, keyed by the server-id used within the system.
 | Authentication profiles can be used whenever maven must make a connection to a remote server.
 |-->
<servers>
    <!-- server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |
    -->
    <server>
        <id>deploymentRepo</id>
        <username>repouser</username>
        <password>repopwd</password>
    </server>

    <!-- Another sample, using keys to authenticate. -->
    <server>
        <id>siteServer</id>
        <privateKey>/path/to/private/key</privateKey>
        <passphrase>optional; leave empty if not used.</passphrase>
    </server>
</servers>
```

The `<profiles>` element is similar to the one that we can specify in our POMs.
This element should be used very carefully
because a project should not depend too much on settings specified outside of its POM.

```xml

<profiles>
    <!-- profile
     | Specifies a set of introductions to the build process, to be activated using one or more of the
     | mechanisms described above. For inheritance purposes, and to activate profiles via <activatedProfiles/>
     | or the command line, profiles have to have an ID that is unique.
     |
     | An encouraged best practice for profile identification is to use a consistent naming convention
     | for profiles, such as 'env-dev', 'env-test', 'env-production', 'user-jdcasey', 'user-brett', etc.
     | This will make it more intuitive to understand what the set of introduced profiles is attempting
     | to accomplish, particularly when you only have a list of profile id's for debug.
     |
     | This profile example uses the JDK version to trigger activation, and provides a JDK-specific repo.
    -->
    <profile>
        <id>jdk-1.4</id>

        <activation>
            <jdk>1.4</jdk>
        </activation>

        <repositories>
            <repository>
                <id>jdk14</id>
                <name>Repository for JDK 1.4 builds</name>
                <url>http://www.myhost.com/maven/jdk14</url>
                <layout>default</layout>
                <snapshotPolicy>always</snapshotPolicy>
            </repository>
        </repositories>
    </profile>

    <!--
     | Here is another profile, activated by the system property 'target-env' with a value of 'dev',
     | which provides a specific path to the Tomcat instance. To use this, your plugin configuration
     | might hypothetically look like:
     |
     | ...
     | <plugin>
     |   <groupId>org.myco.myplugins</groupId>
     |   <artifactId>myplugin</artifactId>
     |
     |   <configuration>
     |     <tomcatLocation>${tomcatPath}</tomcatLocation>
     |   </configuration>
     | </plugin>
     | ...
     |
     | NOTE: If you just wanted to inject this configuration whenever someone set 'target-env' to
     |       anything, you could just leave off the <value/> inside the activation-property.
     |
    -->
    <profile>
        <id>env-dev</id>

        <activation>
            <property>
                <name>target-env</name>
                <value>dev</value>
            </property>
        </activation>

        <properties>
            <tomcatPath>/path/to/tomcat/instance</tomcatPath>
        </properties>
    </profile>
</profiles>
```

In order to see the result of the merging between the local and Global Settings,  
we can use the Maven Help Plugin, as follows:

```text
mvn help:effective-settings
```

## Reference

- [Settings Reference](https://maven.apache.org/settings.html)
