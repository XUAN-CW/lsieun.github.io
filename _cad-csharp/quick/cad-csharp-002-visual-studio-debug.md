---
title: "Visual Studio 中调试 AutoCAD 插件"
sequence: "102"
---

## 代码示例

```csharp
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.EditorInput;
using Autodesk.AutoCAD.Runtime;

namespace Lsieun.Cad.Basic
{
    public class QuickStart
    {
        [CommandMethod("CmdHello")]
        public void CmdHello()
        {
            Editor editor = Application.DocumentManager.MdiActiveDocument.Editor;
            editor.WriteMessage("Hello AutoCAD 二次开发");
        }

        [CommandMethod("CmdSum")]
        public void CmdSum() 
        {
            int n = 100;
            int sum = 0;    // 这里可以打上断点
            for (int i = 1; i <= n; i++) {
                sum += i;
            }

            string msg = "从 1 到 " + n + " 的和是 " + sum;

            Editor editor = Application.DocumentManager.MdiActiveDocument.Editor;
            editor.WriteMessage(msg);
        }
    }
}
```

## 调试

第 1 步，在 Visual Studio 的项目上右键选择 Properties：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-017-visual-studio-2019-project-properties.png)
{:refdef}

第 2 步，在 Debug 选项卡，选择 external program：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-018-visual-studio-2019-debug-external-program.png)
{:refdef}

第 3 步，选择 `Debug -> Start Debugging` 会启动 AutoCAD：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-019-visual-studio-2019-start-debugging.png)
{:refdef}

第 4 步，在 AutoCAD 中，再执行 `NETLOAD` 对 dll 进行加载。

## 警告信息及处理

在 ErrorList 中，可以看到警告信息：

```text
There was a mismatch between the processor architecture of the project being built "MSIL" and
the processor architecture of the reference "acmgd", "AMD64".
This mismatch may cause runtime failures.			
```

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-020-visual-studio-2019-warning-amd64.png)
{:refdef}

修改项目属性中 `Build -> Platform target` 为 `x64`：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-021-visual-studio-2019-build-platform-target-x64.png)
{:refdef}

## 文件加载安全问题

在加载 dll 文件时，会提示安全问题：

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-022-autocad-load-dll-security.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-030-options.png)
{:refdef}

{:refdef: style="text-align: center;"}
![](/assets/images/cad/csharp/quick/dev-031-trusted-location.png)
{:refdef}

