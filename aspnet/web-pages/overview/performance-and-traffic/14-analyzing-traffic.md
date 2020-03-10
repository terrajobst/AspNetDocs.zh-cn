---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 跟踪 ASP.NET 网页（Razor）网站的访问者信息（分析） |Microsoft Docs
author: Rick-Anderson
description: 获得网站后，你可能想要分析你的网站流量。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421454"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>跟踪 ASP.NET 网页（Razor）网站的访问者信息（分析）

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 helper 将网站分析添加到 ASP.NET 网页（Razor）网站中的页面。
> 
> 学习内容：
> 
> - 如何将有关网站流量的信息发送到分析提供程序。
> 
> 下面是本文中引入的 ASP.NET 编程功能：
> 
> - `Analytics` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - ASP.NET Web 帮助程序库（NuGet 包）

分析是对你的网站上的流量进行度量的一项通用术语，你可以了解人们如何使用该网站。 许多 analytics 服务都可用，包括 Google、Yahoo、StatCounter 等服务。

分析的工作方式是使用分析提供程序注册一个帐户，你可以在其中注册要跟踪的站点。提供程序会向你发送 JavaScript 代码片段，其中包含你的帐户的 ID 或跟踪代码。 将 JavaScript 代码片段添加到要跟踪的网站上的网页中。（通常将分析代码片段添加到页脚或布局页，或添加到站点中每个页面上的其他 HTML 标记。）当用户请求包含其中一个 JavaScript 代码段的页面时，该代码段会将有关当前页的信息发送到分析提供程序，该提供程序记录有关该页的各种详细信息。

若要查看站点统计信息，请登录到 analytics 提供商的网站。 然后，您可以查看有关您的站点的所有种类的报告，例如：

- 单个页面的页面视图数。 这会告诉你（大致）有多少人在访问该站点，网站上的哪些页面最受欢迎。
- 用户在特定页面上花费的时间。 这可以告诉你主页是否有兴趣。
- 用户访问你的站点之前，他们在访问的站点。 这可以帮助您了解您的流量是来自链接、搜索还是来自搜索。
- 当用户访问你的网站时，他们会持续多长时间。
- 访问者的国家/地区。
- 你的访问者所使用的浏览器和操作系统。

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>使用 Helper 向页面添加分析

ASP.NET 网页包括多个分析帮助程序（`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`和 `Analytics.GetStatCounterHtml`），使你可以轻松地管理用于分析的 JavaScript 代码段。 你只需将帮助程序添加到页面，而不是找出如何以及在何处放置 JavaScript 代码。 你需要提供的唯一信息是你的帐户名称、ID 或跟踪代码。 （对于 StatCounter，还必须提供一些额外的值。）

在此过程中，您将创建一个使用 `GetGoogleHtml` 帮助器的布局页。 如果已经有一个具有其他分析提供程序的帐户，则可以改为使用该帐户，并根据需要进行细微调整。

> [!NOTE]
> 创建 analytics 帐户时，将注册要跟踪的站点的 URL。 如果要测试本地计算机上的所有内容，则不会跟踪实际流量（唯一的流量是你的），因此你将无法记录和查看站点统计信息。 但此过程显示了如何将分析帮助器添加到页面。 当你发布站点时，实时网站会将信息发送到你的分析提供程序。

1. 如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。
2. 使用 Google Analytics 创建帐户并记录帐户名称。
3. 创建名为 " *Analytics* " 的布局页并添加以下标记：

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > 必须将对 `Analytics` 帮助程序的调用放入网页（`</body>` 标记之前）的正文中。 否则，浏览器不会运行该脚本。

    如果使用的是其他分析提供程序，请改用以下帮助器之一：

    - （Yahoo） `@Analytics.GetYahooHtml("myaccount")`
    - （StatCounter） `@Analytics.GetStatCounterHtml("project", "security")`
4. 将 `myaccount` 替换为在步骤1中创建的帐户、ID 或跟踪代码的名称。
5. 在浏览器中运行页。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）
6. 在浏览器中查看页面源。 你将能够看到呈现的分析代码：

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. 登录到 Google Analytics 站点并检查站点的统计信息。 如果在实时站点上运行该页面，则会看到一个记录访问页面的条目。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [Google Analytics 网站](https://www.google.com/analytics/)
- [Yahoo！ Web Analytics 网站](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 站点](http://statcounter.com/)
