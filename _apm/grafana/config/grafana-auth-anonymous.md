---
title: "免密登录"
sequence: "119"
---

步骤：

- 第 1 步，创建 org
- 第 2 步，修改 `/etc/grafana/grafana.ini` 文件
- 第 3 步，重启 Grafana

## 创建组织

第 1 步，`Administration` --> `Organizations` --> `New org`：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-administration-organizations-new-org.png)
{:refdef}

第 2 步，输入名字：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-administration-organizations-org-name.png)
{:refdef}

第 3 步，设置 `Default preferences`：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-administration-organizations-default-preferences.png)
{:refdef}

## 切换组织

切换到 `stakeholder` 组织

第 1 种方式：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-dashboard-change-org.png)
{:refdef}

第 2 种方式：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-user-profile.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-user-profile-select-organisation.png)
{:refdef}

## 添加 Data Source 和 Dashboard

第 1 步，添加数据源：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/stakeholder-data-sources-prometheus.png)
{:refdef}

第 2 步，添加 Dashboard：

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/stakeholder-import-dashboard.png)
{:refdef}


## 开启匿名访问

要开启匿名访问，需要修改配置文件：

- 第 1 种方式，在容器内配置文件的路径：`/etc/grafana/grafana.ini`
- 第 2 种方式，在 Host 上配置文件的路径：`/opt/grafana/config/grafana.ini`

```text
#################################### Anonymous Auth ######################
[auth.anonymous]
# enable anonymous access
enabled = true

# specify organization name that should be used for unauthenticated users
org_name = stakeholder

# specify role for unauthenticated users
org_role = Viewer
```

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-config-anonymous-auth.png)
{:refdef}

## 重启 Grafana

```text
$ docker restart grafana
```

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-dashboard-auth-anonymous-view-01.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/grafana/grafana-dashboard-auth-anonymous-view-02.png)
{:refdef}
