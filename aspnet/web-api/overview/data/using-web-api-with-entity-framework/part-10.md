---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 将应用发布到 Azure Azure App Service |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504758"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>将应用发布到 Azure Azure App Service

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

最后一步是将应用程序发布到 Azure。 在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。

![](part-10/_static/image1.png)

单击 "**发布**" 将调用 "**发布 Web** " 对话框。 如果在首次创建项目时选中了 "**在云中托管**"，则已配置连接和设置。 在这种情况下，只需单击 "**设置**" 选项卡并选中 &quot;执行 Code First 迁移&quot;"。 （如果你未在云中检查 "在**云中托管**"，请按照[下一节](#new-website)中的步骤进行操作。）

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

若要部署应用，请单击 "**发布**"。 您可以在 " **Web 发布活动**" 窗口中查看发布进度。 （从 "**视图**" 菜单中选择 "**其他窗口**"，然后选择 " **Web 发布活动**"。）

![](part-10/_static/image4.png)

当 Visual Studio 完成应用程序部署时，默认浏览器会自动打开到已部署网站的 URL，你创建的应用程序现在正在云中运行。 浏览器地址栏中的 URL 显示正在从 Internet 加载该站点。

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>部署到新网站

如果在首次创建项目时未选中 "**在云中托管**"，则可以立即配置新的 web 应用。 在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。 选择 "**配置文件**" 选项卡，然后单击 " **Microsoft Azure 网站**"。 如果你当前未登录到 Azure，系统将提示你登录。

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

在 "**现有网站**" 对话框中，单击 "**新建**"。

![](part-10/_static/image9.png)

输入站点名称。 选择 Azure 订阅和区域。 在 "**数据库服务器**" 下，选择 "**创建新服务器**"，或选择现有服务器。 单击 **“创建”** 。

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

单击 "**设置**" 选项卡，检查 &quot;"执行 Code First 迁移&quot;"。 然后单击“发布”。

> [!div class="step-by-step"]
> [上一页](part-9.md)
