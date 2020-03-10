---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: 将 Web API 2 与实体框架6一起使用 |Microsoft Docs
author: MikeWasson
description: 本教程将教你使用 ASP.NET Web API 后端创建 web 应用程序的基础知识。 本教程使用实体框架6作为数据布局 。
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504836"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>通过 Entity Framework 6 使用 Web API 2

[下载完成的项目](https://github.com/MikeWasson/BookService)

> 本教程介绍使用 ASP.NET Web API 后端创建 web 应用程序的基础知识。 本教程将实体框架6用于数据层，并为客户端 JavaScript 应用程序使用 "挖空"。 本教程还演示了如何将应用部署到 Azure App Service Web Apps。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - Web API 2。1
> - Visual Studio 2017 （下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)）
> - Entity Framework 6
> - .NET 4.7
> - [挖空 .js](http://knockoutjs.com/) 3。1

本教程将 ASP.NET Web API 2 与实体框架6一起使用，以创建操作后端数据库的 Web 应用程序。 下面是你将创建的应用程序的屏幕截图。

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

应用使用单页应用程序（SPA）设计。 "单页应用程序" 是 web 应用程序的常规术语，用于加载单个 HTML 页面，然后动态更新页面，而不是加载新页面。 初始页面加载后，应用将通过 AJAX 请求与服务器进行通信。 AJAX 请求返回 JSON 数据，应用使用这些数据来更新 UI。

AJAX 并不新，但现在有了 JavaScript 框架，可以更轻松地构建和维护大型的 SPA 应用程序。 本教程使用的是[挖空](http://knockoutjs.com/)的，但你可以使用任何 JavaScript 客户端框架。

下面是此应用程序的主要构建基块：

- ASP.NET MVC 创建 HTML 页面。
- ASP.NET Web API 处理 AJAX 请求并返回 JSON 数据。
- 挖空 node.js 数据-将 HTML 元素绑定到 JSON 数据。
- 实体框架与数据库进行通信。

## <a name="see-this-app-running-on-azure"></a>查看此应用在 Azure 上运行

要查看作为实时 web 应用运行的已完成站点吗？ 可以通过选择以下按钮将应用程序的完整版本部署到 Azure 帐户。

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

需要一个 Azure 帐户才能将此解决方案部署到 Azure。 如果还没有帐户，可以使用以下选项：

- [免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。
- [激活 msdn 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-msdn 订阅每月提供可用于付费 Azure 服务的信用额度。

## <a name="create-the-project"></a>创建项目

打开 Visual Studio。 从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。 （或在 "开始" 页上选择 "**新建项目**"。）

在 "**新建项目**" 对话框中，在左窗格中选择 " **web** "，并在中间窗格中选择 " **ASP.NET web 应用程序（.NET Framework）** "。 将项目命名为**BookService** ，然后选择 **"确定"** 。

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web API** " 模板。

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

选择“确定”创建项目。

## <a name="configure-azure-settings-optional"></a>配置 Azure 设置（可选）

创建项目后，可以随时选择部署到 Azure App Service Web 应用。 

1. 在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。

2. 在出现的窗口中，选择 "**启动**"。 此时将显示 "**选取发布目标**" 对话框。

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. 选择“创建配置文件”。 “创建应用服务”对话框随即显示。

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   接受默认值，或者为应用程序名称、资源组、托管计划、Azure 订阅和地理区域输入不同的值。 

4. 选择 "**创建 SQL 数据库**"。 此时将显示 "**配置 SQL Server** " 对话框。 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   接受默认值或输入不同的值。 输入新数据库的**管理员用户名**和**管理员密码**。 完成后，选择 **"确定"** 。 再次出现 "**创建应用服务**" 页。

5. 选择 "**创建**" 以创建配置文件。 将在右下角显示一条消息，指示部署正在进行中。 一小段时间后，将重新出现 "**发布**" 窗口。

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    你创建的用于部署应用程序的配置文件现已可用。 

> [!div class="step-by-step"]
> [下一部分](part-2.md)
