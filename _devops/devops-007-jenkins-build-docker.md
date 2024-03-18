---
title: "自动构建 Docker 镜像"
sequence: "107"
---

## 源码

File: `docker/Dockerfile`

```text
FROM openjdk:8-slim
WORKDIR /usr/local
COPY myproject.jar .
CMD java -jar myproject.jar
```

## Jenkins 配置

第 1 步，在 `myproject-ci` 下选择 Configure：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-configure.png)
{:refdef}

第 2 步，在 Post-build Actions 部分，清空 Exec command，并点击 Add Transfer Set：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-044-exec-command-empty.png)
{:refdef}

第 3 步，配置 Transfer Set 的信息：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-045-transfer-set.png)
{:refdef}

第 4 步，在 `myproject-ci` 下，选择 Build Now：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-build-now.png)
{:refdef}


第 5 步，在 `WebServer` 服务器上验证：

```text
$ ls -l
total 4
-rw-rw-r--. 1 devops devops  6 Sep 14 19:27 abc.txt
drwxrwxr-x. 2 devops devops 24 Sep 14 19:27 docker
drwxrwxr-x. 2 devops devops 66 Sep 14 19:27 target
```

## 修改配置

第 1 步，在 `myproject-ci` 下选择 Configure：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-configure.png)
{:refdef}

第 2 步，移除 jar 文件的前缀。在 Transfer Set 部分，添加 Remove prefix：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-048-remove-prefix-target.png)
{:refdef}

第 3 步，移除 Dockerfile 的前缀。在 Transfer Set 部分，添加 Remove prefix：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-049-remove-prefix-docker.png)
{:refdef}

第 4 步，在 `myproject-ci` 下，选择 Build Now：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-build-now.png)
{:refdef}

第 5 步，在 `WebServer` 服务器上验证：

```text
$ ls -l
total 17340
-rw-rw-r--. 1 devops devops        6 Sep 14 19:34 abc.txt
-rw-rw-r--. 1 devops devops       87 Sep 14 19:34 Dockerfile
-rw-rw-r--. 1 devops devops 17744539 Sep 14 19:34 myproject.jar
```

## 构建 Docker 镜像

第 1 步，在 `myproject-ci` 下选择 Configure：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-configure.png)
{:refdef}

第 2 步，配置 Exec command：

```text
docker build -t lsieun/myproject:1.0 /home/devops/
docker rm -f myproject
docker run -d -p 80:80 --name myproject lsieun/myproject:1.0
```

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-050-exec-docker-build.png)
{:refdef}

第 3 步，在 `myproject-ci` 下，选择 Build Now：

{:refdef: style="text-align: center;"}
![](/assets/images/devops/jenkins/jenkins-myproject-ci-build-now.png)
{:refdef}

第 4 步，在 `WebServer` 服务器上验证：

```text
$ docker images
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
lsieun/myproject   1.0       b1b3e00a1803   2 minutes ago    313MB

$ docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                               NAMES
a8671e2be502   lsieun/myproject:1.0   "/bin/sh -c 'java -j…"   2 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   myproject
```

第 5 步，在浏览器访问：

```text
http://192.168.80.253/hello/world
```
