---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 启动类检测 |Microsoft Docs
author: Praburaj
description: 本教程介绍如何配置加载的 OWIN startup 类。 有关 OWIN 的详细信息，请参阅项目 Katana 概述。 本教程为 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500180"
---
# <a name="owin-startup-class-detection"></a>OWIN 启动类检测

> 本教程介绍如何配置加载的 OWIN startup 类。 有关 OWIN 的详细信息，请参阅[项目 Katana 概述](an-overview-of-project-katana.md)。 本教程由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）编写。
>
> ## <a name="prerequisites"></a>系统必备
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>OWIN 启动类检测

 每个 OWIN 应用程序都有一个 startup 类，您可以在其中为应用程序管道指定组件。 可以通过不同的方式将启动类连接到运行时，具体取决于所选的托管模型（Owinhost.exe、IIS 和 IIS Express）。 本教程中所示的 startup 类可用于每个托管应用程序。 使用以下方法之一将 startup 类与宿主运行时连接：

1. **命名约定**： Katana 在与程序集名称或全局命名空间匹配的命名空间中查找名为 `Startup` 的类。
2. **OwinStartup 特性**：这是大多数开发人员用来指定 startup 类的方法。 以下属性会将 startup 类设置为 `StartupDemo` 命名空间中的 `TestStartup` 类。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` 特性将重写命名约定。 你还可以使用此特性指定友好名称，但是，使用友好名称还需要使用配置文件中的 `appSetting` 元素。
3. **配置文件中的 appSetting 元素**： `appSetting` 元素将重写 `OwinStartup` 属性和命名约定。 可以有多个启动类（每个类都使用 `OwinStartup` 属性），并配置将使用类似于下面的标记在配置文件中加载的启动类：

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   以下显式指定 startup 类和程序集的键也可以使用：

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   配置文件中的以下 XML 指定友好的启动类名称 `ProductionConfiguration`。

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   以上标记必须与以下 `OwinStartup` 特性一起使用，该特性指定友好名称并导致 `ProductionStartup2` 类运行。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. 若要禁用 OWIN 启动发现，请在 web.config 文件中添加值为 `"false"` 的 `appSetting owin:AutomaticAppStartup`。

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>使用 OWIN 启动创建 ASP.NET Web 应用

1. 创建一个空的 Asp.Net web 应用程序并将其命名为**StartupDemo**。 -使用 NuGet 包管理器安装 `Microsoft.Owin.Host.SystemWeb`。 从 "**工具**" 菜单中，依次选择 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。 输入以下命令：

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. 添加 OWIN startup 类。 在 Visual Studio 2017 中，右键单击项目并选择 "**添加类**"。-在 "**添加新项**" 对话框中，在搜索字段中输入*OWIN* ，将名称更改为 Startup.cs，然后选择 "**添加**"。

     ![](owin-startup-class-detection/_static/image1.png)

   下次要添加*Owin Startup 类*时，它将在 "**添加**" 菜单中可用。

     ![](owin-startup-class-detection/_static/image2.png)

   或者，您可以右键单击该项目并选择 "**添加**"，然后选择 "**新建项**"，然后选择 " **Owin Startup 类**"。

     ![](owin-startup-class-detection/_static/image3.png)

- 将*Startup.cs*文件中生成的代码替换为以下代码：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` lambda 表达式用于向 OWIN 管道注册指定的中间件组件。 在这种情况下，我们将在响应传入请求之前设置传入请求的日志记录。 `next` 参数是管道中的下一个组件的委托（ [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt;[任务](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;）。 `app.Run` lambda 表达式将管道与传入请求挂钩，并提供响应机制。
     > [!NOTE]
     > 在上面的代码中，我们已注释掉 `OwinStartup` 属性，我们将依赖于运行名为 `Startup` 的类的约定。-按***F5***运行该应用程序。 命中刷新几次。

    ![](owin-startup-class-detection/_static/image4.png) 注意：本教程的图像中显示的数字与你看到的数字不匹配。 毫秒字符串用于在刷新页面时显示新的响应。
  可以在 "**输出**" 窗口中查看跟踪信息。

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>添加更多启动类

在本部分中，我们将添加另一个启动类。 可以向应用程序添加多个 OWIN startup 类。 例如，你可能想要创建启动类以进行开发、测试和生产。

1. 创建新的 OWIN Startup 类并将其命名为 `ProductionStartup`。
2. 将生成的代码替换为以下内容：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. 按 Ctrl F5 运行该应用程序。 `OwinStartup` 属性指定运行生产启动类。

    ![](owin-startup-class-detection/_static/image6.png)
4. 创建另一个 OWIN Startup 类并将其命名 `TestStartup`。
5. 将生成的代码替换为以下内容：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   上述 `OwinStartup` 特性重载将 `TestingConfiguration` 指定为 Startup 类的*友好*名称。
6. 打开 web.config*文件，* 并添加 OWIN 应用启动密钥，该密钥指定 startup 类的友好名称：

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. 按 Ctrl F5 运行该应用程序。 应用设置元素使用引用单元格，并运行测试配置。

    ![](owin-startup-class-detection/_static/image7.png)
8. 从 `TestStartup` 类的 `OwinStartup` 特性中删除*友好*名称。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. *将 web.config 文件中*的 OWIN 应用启动密钥替换为以下内容：

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 将每个类中的 `OwinStartup` 属性还原为 Visual Studio 生成的默认属性代码：

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    下面的每个 OWIN 应用启动密钥将导致生产类运行。

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    最后一个启动密钥指定启动配置方法。 以下 OWIN 应用启动键允许你将配置类的名称更改为 `MyConfiguration`。

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>使用 Owinhost.exe

1. 将 web.config 文件替换为以下标记：

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   最后一个键为 wins，因此在这种情况下，指定 `TestStartup`。
2. 从 PMC 安装 Owinhost.exe：

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. 导航到应用程序文件夹（包含*web.config 文件的*文件夹），并在命令提示符下键入：

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   命令窗口将显示：

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. 使用 URL `http://localhost:5000/`启动浏览器。

    ![](owin-startup-class-detection/_static/image8.png)

   Owinhost.exe 遵循上面列出的启动约定。
5. 在命令窗口中，按 Enter 退出 Owinhost.exe。
6. 在 `ProductionStartup` 类中，添加以下 OwinStartup 属性，该属性指定*ProductionConfiguration*的友好名称。

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. 在命令提示符下，键入：

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   将加载生产启动类。
    ![](owin-startup-class-detection/_static/image9.png)

   我们的应用程序具有多个启动类，在此示例中，我们已将要加载的启动类推迟到运行时。
8. 测试以下运行时启动选项：

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
