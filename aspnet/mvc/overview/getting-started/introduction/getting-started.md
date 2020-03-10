---
uid: mvc/overview/getting-started/introduction/getting-started
title: 入门与 ASP.NET MVC 5 |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487952"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 入门

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

本教程介绍使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)生成 ASP.NET MVC 5 web 应用程序的基础知识。 本教程的最终源代码位于[GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)上。

本教程作者： [Scott Guthrie](https://weblogs.asp.net/scottgu/) （twitter[@scottgu](https://twitter.com/scottgu) ）、 [scott Hanselman](http://www.hanselman.com/blog/) （Twitter： [@shanselman](https://twitter.com/shanselman) ）和[Rick Anderson](https://twitter.com/RickAndMSFT) （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）

需要一个 Azure 帐户才能将此应用部署到 Azure：

- 可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。
- 可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - MSDN 订阅每月提供可用来试用付费版 Azure 服务的信用额度。

## <a name="get-started"></a>入门

首先[安装 Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 然后打开 Visual Studio。

Visual Studio 是一个 IDE，或集成的开发环境。 就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。 在 Visual Studio 中，底部有一个列表，其中显示了可供你使用的各种选项。 还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。 例如，你可以使用菜单栏并选择 "**文件**" > "**新建项目**"，而不是在**起始页**上选择 "**新建项目**"。

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>创建你的第一个应用

在 "**开始" 页**上，选择 "**新建项目**"。 在 "**新建项目**" 对话框中，选择左侧的**视觉对象C#** 类别，然后选择 " **web**"，然后选择 " **ASP.NET Web 应用程序（.NET Framework）** " 项目模板。 将项目命名为 "MvcMovie"，然后选择 **"确定**"。

![](getting-started/_static/image2.png)

在 "**新建 ASP.NET Web 应用程序**" 对话框中，选择 " **MVC** "，然后选择 **"确定"** 。

![](getting-started/_static/image3.png)

Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！ 这是一个简单的 "Hello World！" 项目，这是启动应用程序的好地方。

![](getting-started/_static/image4.png)

按 **F5** 启动调试。 按**F5**时，Visual Studio 将启动[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)并运行你的 web 应用。 然后，Visual Studio 会启动浏览器并打开应用程序的主页。 请注意，浏览器的地址栏会显示 `localhost:port#`，而不是类似 `example.com`。 这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。 当 Visual Studio 运行 web 项目时，会将随机端口用于 web 服务器。 在下图中，端口号为1234。 运行应用程序时，将看到不同的端口号。

![](getting-started/_static/image5.png)

立即将此默认模板提供给您 `Home`、`Contact`和 `About` 页面。 下图不显示 "**主页**"、"**关于**" 和 "**联系人**" 链接。 根据浏览器窗口的大小，可能需要单击导航图标才能看到这些链接。

![](getting-started/_static/image6.png)

该应用程序还为注册和登录提供支持。 下一步是更改此应用程序的工作原理，并了解 ASP.NET MVC 的一些相关信息。 关闭 ASP.NET MVC 应用程序并更改某些代码。

有关当前教程的列表，请参阅[MVC 推荐的文章](../mvc-learning-sequence.md)。

## <a name="see-this-app-running-on-azure"></a>查看此应用在 Azure 上运行

要查看作为实时 web 应用运行的已完成站点吗？ 只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果还没有帐户，请使用以下选项之一创建一个帐户：

- [免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。
- [激活 Visual studio 订阅者权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)-你的 visual studio 订阅每月为你提供可用于付费 Azure 服务的信用额度。

> [!div class="step-by-step"]
> [下一部分](adding-a-controller.md)
