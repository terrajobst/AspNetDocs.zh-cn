---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自承载 ASP.NET Web API 1 （C#）-ASP.NET 4。x
author: MikeWasson
description: 代码教程介绍了如何在控制台应用程序中承载 web API。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421370"
---
# <a name="self-host-aspnet-web-api-1-c"></a>自承载 ASP.NET Web API 1 （C#）

作者： [Mike Wasson](https://github.com/MikeWasson)

> 本教程介绍如何在控制台应用程序中承载 web API。 ASP.NET Web API 不需要 IIS。 你可以在自己的主机进程中自承载 web API。 
> 
> **新应用程序应使用 OWIN 到自承载 Web API。** 请参阅[使用 OWIN ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>创建控制台应用程序项目

启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Windows**"。 在项目模板列表中，选择 "**控制台应用程序**"。 将项目命名为 &quot;SelfHost&quot; 并单击 **"确定"** 。

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>设置目标框架（Visual Studio 2010）

如果使用的是 Visual Studio 2010，请将目标框架更改为 .NET Framework 4.0。 （默认情况下，项目模板以[.Net Framework 客户端配置文件](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)为目标。）

在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。 在 "**目标框架**" 下拉列表中，将 "目标框架" 更改为 .NET Framework 4.0。 出现应用更改提示时，单击 **"是"** 。

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>安装 NuGet 包管理器

NuGet 包管理器是将 Web API 程序集添加到 non-ASP.NET 项目的最简单方法。

若要检查是否安装了 NuGet 包管理器，请单击 Visual Studio 中的 "**工具**" 菜单。 如果你看到名为 " **Nuget 包管理器**" 的菜单项，则具有 Nuget 包管理器。

安装 NuGet 包管理器：

1. 启动 Visual Studio。
2. 在“工具”菜单上，选择“扩展和更新”。
3. 在 "**扩展和更新**" 对话框中，选择 "**联机**"。
4. 如果看不到 "NuGet 程序包管理器"，请在 "搜索" 框中键入 "nuget 包管理器"。
5. 选择 NuGet 包管理器，然后单击 "**下载**"。
6. 下载完成后，系统会提示你进行安装。
7. 安装完成后，系统可能会提示你重启 Visual Studio。

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>添加 Web API NuGet 包

安装 NuGet 包管理器后，将 Web API 自承载包添加到项目。

1. 从 "**工具**" 菜单中选择 " **NuGet 包管理器**"。 *注意*：如果看不到此菜单项，请确保已正确安装 NuGet 包管理器。
2. 选择 "**管理解决方案的 NuGet 包**"
3. 在 "**管理 NugGet 包**" 对话框中，选择 "**联机**"。
4. 在搜索框中，键入 "WebApi"&quot;&quot;。
5. 选择 ASP.NET Web API 己方主机包，然后单击 "**安装**"。
6. 安装包后，单击 "**关闭**" 以关闭对话框。

> [!NOTE]
> 请确保安装名为 WebApi 的包，而不是 AspNetWebApi. SelfHost。

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>创建模型和控制器

本教程使用与[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程相同的模型和控制器类。

添加一个名为 `Product`的公共类。

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

添加一个名为 `ProductsController`的公共类。 从**ApiController**派生此类。

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

有关此控制器中代码的详细信息，请参阅[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。 此控制器定义三个 GET 操作：

| URI | 说明 |
| --- | --- |
| /api/products | 获取所有产品的列表。 |
| /api/products/*id* | 按 ID 获取产品。 |
| /api/products/？ category =*类别* | 按类别获取产品列表。 |

## <a name="host-the-web-api"></a>承载 Web API

打开文件 Program.cs 并添加以下 using 语句：

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

将以下代码添加到**Program**类。

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>可有可无添加 HTTP URL 命名空间保留

此应用程序侦听 `http://localhost:8080/`。 默认情况下，侦听特定的 HTTP 地址需要管理员权限。 因此，当你运行本教程时，你可能会收到以下错误： "HTTP 无法注册 URL http://+:8080/" 可通过两种方法来避免此错误：

- 以提升的管理员权限运行 Visual Studio，或
- 使用 dism.exe 为你的帐户授予保留 URL 的权限。

若要使用 dism.exe，请使用管理员权限打开命令提示符，然后输入以下命令：

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

其中，*计算机 \* 是你的用户帐户。

完成自承载后，请确保删除该保留：

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>从客户端应用程序调用 Web API （C#）

让我们编写一个简单的控制台应用程序来调用 web API。

向解决方案添加新的控制台应用程序项目：

- 在解决方案资源管理器中，右键单击解决方案并选择 "**添加新项目**"。
- 创建一个名为 &quot;ClientApp&quot;的新控制台应用程序。

![](self-host-a-web-api/_static/image5.png)

使用 NuGet 包管理器添加 ASP.NET Web API 核心库包：

- 从 "工具" 菜单中选择 " **NuGet 包管理器**"。
- 选择 "**管理解决方案的 NuGet 包**"
- 在 "**管理 NuGet 包**" 对话框中，选择 "**联机**"。
- 在搜索框中，键入 "WebApi"&quot;&quot;。
- 选择 Microsoft ASP.NET Web API 客户端库 "包，然后单击"**安装**"。

将 ClientApp 中的引用添加到 SelfHost 项目：

- 在解决方案资源管理器中，右键单击 ClientApp 项目。
- 选择“添加引用”。
- 在 "**引用管理器**" 对话框中的 "**解决方案**" 下，选择 "**项目**"。
- 选择 SelfHost 项目。
- 单击“确定”。

![](self-host-a-web-api/_static/image6.png)

打开客户端/Program .cs 文件。 添加以下 **using** 语句：

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

添加静态**HttpClient**实例：

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

添加以下方法以列出所有产品，按 ID 列出产品，并按类别列出产品。

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

上述每种方法都遵循相同的模式：

1. 调用**HttpClient GetAsync**将 GET 请求发送到相应的 URI。
2. 调用**HttpResponseMessage. EnsureSuccessStatusCode**。 如果 HTTP 响应状态是错误代码，则此方法将引发异常。
3. 调用**ReadAsAsync&lt;t&gt;** 从 HTTP 响应反序列化 CLR 类型。 此方法是在**HttpContentExtensions**中定义的扩展方法。

**GetAsync**和**ReadAsAsync**方法都是异步的。 它们返回表示异步操作的**任务**对象。 获取**Result**属性会阻止线程，直到操作完成。

有关使用 HttpClient 的详细信息，包括如何发出非阻塞调用，请参阅[从 .Net 客户端调用 WEB API](../advanced/calling-a-web-api-from-a-net-client.md)。

在调用这些方法之前，请将 HttpClient 实例上的 BaseAddress 属性设置为 "`http://localhost:8080`"。 例如:

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

这应输出以下。 （请记得先运行 SelfHost 应用程序。）

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
