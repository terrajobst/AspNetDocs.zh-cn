---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: 创建 OData v4 客户端应用（C#） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448118"
---
# <a name="create-an-odata-v4-client-app-c"></a>创建 OData v4 客户端应用 (C#)

作者： [Mike Wasson](https://github.com/MikeWasson)

在上一教程中，你创建了支持 CRUD 操作的基本 OData 服务。 现在，让我们为该服务创建一个客户端。

启动 Visual Studio 的新实例，并创建新的控制台应用程序项目。 在 "**新建项目**" 对话框中，选择 "**安装**&gt;**模板**&gt;  **C# Visual** &gt; **Windows 桌面**"，然后选择 "**控制台应用程序**" 模板。 将项目命名为 &quot;ProductsApp&quot;。

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> 你还可以将控制台应用添加到包含 OData 服务的同一 Visual Studio 解决方案中。

## <a name="install-the-odata-client-code-generator"></a>安装 OData 客户端代码生成器

在“工具”菜单上，选择“扩展和更新”。 选择 "**联机**&gt; **Visual Studio 库**"。 在搜索框中，搜索 "&quot;OData 客户端代码生成器"&quot;。 单击 "**下载**" 以安装 VSIX。 系统可能会提示你重启 Visual Studio。

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>在本地运行 OData 服务

从 Visual Studio 运行 ProductService 项目。 默认情况下，Visual Studio 会将浏览器启动到应用程序根目录。 记下 URI;你将在下一步中需要此项。 使应用程序保持运行。

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> 如果将这两个项目放在同一解决方案中，请确保在不调试的情况下运行 ProductService 项目。 在下一步中，你将需要在修改控制台应用程序项目时保持该服务处于运行状态。

## <a name="generate-the-service-proxy"></a>生成服务代理

服务代理是一个 .NET 类，用于定义用于访问 OData 服务的方法。 代理会将方法调用转换为 HTTP 请求。 您将通过运行[T4 模板](https://msdn.microsoft.com/library/bb126445.aspx)来创建代理类。

右键单击项目。 选择“添加” **“新项”** &gt;。

![](create-an-odata-v4-client-app/_static/image5.png)

在 "**添加新项**" 对话框中，选择 "  **C#视觉对象项**&gt;**代码**&gt; **OData 客户端**"。 将模板命名 &quot;ProductClient.tt&quot;。 单击 "**添加**"，然后单击安全警告。

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

此时，您将收到一个错误，您可以忽略该错误。 Visual Studio 会自动运行该模板，但模板首先需要一些配置设置。

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

打开文件 ProductClient。在 `Parameter` 元素中，从 ProductService 项目中粘贴 URI （上一步）。 例如:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

再次运行模板。 在解决方案资源管理器中，右键单击 ProductClient.tt 文件并选择 "**运行自定义工具**"。

此模板创建一个名为 ProductClient.cs 的代码文件，用于定义代理。 开发应用时，如果更改 OData 终结点，请再次运行模板以更新代理。

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>使用服务代理调用 OData 服务

打开文件 Program.cs，并将样板代码替换为以下代码。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

将*serviceUri*的值替换为前面的服务 URI。

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

运行应用时，它应输出以下内容：

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
