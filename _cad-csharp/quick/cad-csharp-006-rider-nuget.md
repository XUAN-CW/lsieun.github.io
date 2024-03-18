---
title: "Rider + Nuget"
sequence: "106"
---

## 添加 AutoCAD 依赖

第 1 步，在 Dependencies 上右键选择 **Manage NuGet Packages**：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/rider/rider-manage-nuget-packages.png)
{:refdef}

第 2 步，搜索 **AutoCAD-2014.Net.Base**，并添加到当前项目：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/rider/rider-add-autocad-2014-packages.png)
{:refdef}

第 3 步，确认安装：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/rider/rider-install-autocad-2014-confirm.png)
{:refdef}

第 4 步，选中刚添加了 10 个 AutoCAD 相关的 Assembly，右键选择 **Properties**：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/rider/rider-autocad-2014-assembly-properties.png)
{:refdef}

第 5 步，在 Reference Properties 中，取消 **Copy local** 的勾选状态：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/rider/rider-autocad-2014-assembly-copy-local-false.png)
{:refdef}



