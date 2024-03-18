---
title: "不重启 AutoCAD"
sequence: "103"
---

## Lsieun.Cad.Bridge

### 新加一个项目

第 1 步，新建一个项目

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-022-vs-add-new-project.png)
{:refdef}

第 2 步，选择项目类型为 Class Library：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-023-add-new-class-library.png)
{:refdef}

第 3 步，配置项目名称：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-024-configure-project.png)
{:refdef}

### 添加引用

第 1 步，为 `Lsieun.Cad.Bridge` 项目添加引用：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-025-add-reference.png)
{:refdef}

第 2 步，选择 3 个 dll 文件：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-026-select-dll.png)
{:refdef}

第 3 步，将 Copy Local 属性设置为 False：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-027-dll-copy-local-false.png)
{:refdef}

### 编写代码

```csharp
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.EditorInput;
using Autodesk.AutoCAD.Runtime;
using System;
using System.IO;
using System.Reflection;

namespace Lsieun.Cad.Bridge
{
    public class SimpleBridge
    {
        [CommandMethod("LSIEUN")]
        public void WalkThrough()
        {
            // 第 1 步，准备参数
            string dllName = "Lsieun.Cad.Basic.dll";
            string className = "Lsieun.Cad.Basic.QuickStart";
            string methodName = "CmdHello";

            // 第 2 步，进行反射
            var adapterFileInfo = new FileInfo(Assembly.GetExecutingAssembly().Location);
            var targetFilePath = Path.Combine(adapterFileInfo.DirectoryName, dllName);
            var targetAssembly = Assembly.Load(File.ReadAllBytes(targetFilePath));
            var targetType = targetAssembly.GetType(className);
            var targetMethod = targetType.GetMethod(methodName);
            var targetObject = Activator.CreateInstance(targetType);

            Action cmd = () => targetMethod.Invoke(targetObject, null);

            try
            {
                cmd?.Invoke();
            }
            catch (System.Exception ex)
            {
                string msg = ex.Message;
                Editor editor = Application.DocumentManager.MdiActiveDocument.Editor;
                editor.WriteMessage(msg);
            }
        }
    }
}
```

## Lsieun.Cad.Basic

第 1 步，修改 `Lsieun.Cad.Basic` 的属性：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-028-cad-basic-properties.png)
{:refdef}

第 2 步，在 `Build` 选项卡，将 `Lsieun.Cad.Basic.dll` 生成到 `..\Lsieun.Cad.Bridge\bin\Debug\` 目录：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-029-cad-basic-output-path.png)
{:refdef}

## 构建解决方案

第 1 步，选择 `Build -> Build Solution`：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-032-build-solution.png)
{:refdef}

第 2 步，在 Output 中可以看到生成了两个 dll 文件：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-033-output-dll.png)
{:refdef}

第 3 步，在 `Lsieun.Cad.Bridge\bin\Debug` 目录中，也可以看到这两个文件：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-034-two-dll-libraries.png)
{:refdef}

## AutoCAD 测试

在 AutoCAD 中，输入 `NETLOAD` 命令，然后选择 `Lsieun.Cad.Bridge.dll` 文件进行测试。

