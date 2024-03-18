---
title: "Docker Repo"
sequence: "docker"
---

## Nexus 配置

### 添加 Blob

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-001-create-blob-store.png)
{:refdef}

### 添加 Docker Proxy

> 测试阿里云没有成功，测试 163 成功了

第 1 步，输入名称，并勾选匿名访问：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-002-create-docker-proxy.png)
{:refdef}

第 2 步，输入地址：

```text
https://hub-mirror.c.163.com
```

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-003-create-docker-proxy.png)
{:refdef}

第 3 步，选择 Blob Store：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-004-create-docker-proxy.png)
{:refdef}

第 4 步，添加认证信息

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-004-create-docker-proxy-auth.png)
{:refdef}

### 添加 Docker Hosted

第 1 步，输入 Name，并允许匿名访问：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-005-create-docker-hosted.png)
{:refdef}

第 2 步，选择 Blob store：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-006-create-docker-hosted.png)
{:refdef}

### 添加 Docker Group

第 1 步，输入 Name：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-007-create-docker-group.png)
{:refdef}

第 2 步，选择 Blob store：

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-008-create-docker-group.png)
{:refdef}

### Docker Bearer Token Realm

{:refdef: style="text-align: center;"}
![](/assets/images/nexus3/docker/docker-repo-009-docker-bearer-token-realm.png)
{:refdef}

## Docker 配置

```text
$ vi /etc/docker/daemon.json
```

```json
{
  "registry-mirrors": [
    "https://docker.lsieun.com",
    "https://mezagd1y.mirror.aliyuncs.com",
    "https://registry.aliyuncs.com"
  ],
  "debug": true
}
```

```text
$ sudo systemctl restart docker
```

```text
$ docker login docker.lsieun.cn
```

## Reference

- [Nexus3最佳实践系列：搭建Docker私有仓库](https://zhang.ge/5139.html)
