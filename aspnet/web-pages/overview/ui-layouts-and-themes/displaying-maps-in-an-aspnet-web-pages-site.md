---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 在 ASP.NET 网页（Razor）站点中显示地图 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何基于必应、Google、Ma 提供的映射服务，在 ASP.NET 网页（Razor）网站的页面上显示交互式地图。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518720"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET 网页（Razor）站点中显示地图

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何基于必应、Google、MapQuest 和 Yahoo 提供的映射服务，在 ASP.NET 网页（Razor）网站中的页面上显示交互式地图。
> 
> 学习内容：
> 
> - 如何生成基于地址的映射。
> - 如何基于纬度和经度坐标生成地图。
> - 如何注册必应地图开发人员帐户并获取用于 Bing 地图的密钥。
> 
> 这是本文中介绍的 ASP.NET 功能：
> 
> - `Maps` 帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - WebMatrix 2
>   
> 
> 本教程还适用于 WebMatrix 3。

在网页中，可以使用 `Maps` 帮助程序在页面上显示地图。 您可以基于一个地址或一组经度和纬度坐标生成地图。 利用 `Maps` 类，您可以调入常用的地图引擎，包括必应、Google、MapQuest 和 Yahoo。

无论调用哪个映射引擎，添加到页的映射的步骤都是相同的。 你只需添加一个 JavaScript 文件引用，该引用使可用方法显示映射，然后调用 `Maps` 帮助器的方法。

根据所使用的 `Maps` 帮助器方法选择映射服务。 可以使用以下任一操作：

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>安装所需的组件

若要显示地图，需要以下各项：

- `Maps` 帮助程序。 此帮助程序位于 ASP.NET Web 帮助程序库的第2版中。 如果尚未添加库，则可以将其作为 NuGet 包安装在站点中。 有关详细信息，请参阅[在 ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)。 （在库中，搜索 `microsoft-web-helpers` 包。）
- JQuery 库。 一些 WebMatrix 站点模板已在其*脚本*文件夹中包含 jQuery 库。 如果你没有这些库，则可以直接从[jQuery.org](http://jQuery.org)网站下载最新 jQuery library。 或者，你可以使用模板创建新站点（例如，"**入门网站**" 模板），然后将该站点中的 jQuery 文件复制到当前站点。

最后，如果要使用 Bing 地图，必须首先创建一个（免费）帐户并获取一个密钥。 若要获取密钥，请执行以下步骤：

1. 在[Bing Maps 开发人员帐户](https://www.microsoft.com/maps/developers/web.aspx)上创建帐户。 还必须有 Microsoft 帐户（Windows Live ID）。

    可以指定要使用密钥进行**评估/测试**。 如果你使用 WebMatrix 和 IIS Express 在你自己的计算机上测试 mapping 函数，请在 "**站点**" 工作区中，记下站点的 URL （例如，`http://localhost:50408`，尽管你的端口号可能会不同）。 注册时，可以使用此*localhost*地址作为站点。
2. 注册帐户后，请前往 Bing 地图帐户中心，并单击 "**创建" 或 "查看密钥**"：

    ![映射-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. 记录必应创建的密钥。

## <a name="creating-a-map-based-on-an-address-using-google"></a>基于地址创建地图（使用 Google）

下面的示例演示如何创建基于地址呈现地图的页面。 此示例演示如何使用 Google Maps。

1. 在站点的根目录中创建一个名为 MapAddress 的文件 *。* 此页将根据您传递给它的地址生成一个映射。
2. 将以下代码复制到文件中，并覆盖现有内容。

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    请注意页面的以下功能：

    - `<head>` 元素中的 `<script>` 元素。 在此示例中，`<script>` 元素引用 */selfservice/scripts/jquery-1.10.2.min.js 1.6.4*文件，这是 jquery library 版本1.6.4 的缩小（压缩）版本。 请注意，该引用假设 *.js*文件位于您的网站的*Scripts*文件夹中。 

        > [!NOTE]
        > 如果使用的是不同版本的 jQuery library，只需确保正确指向该版本即可。
    - 对页面正文中的 `@Maps.GetGoogleHtml` 的调用。 若要映射地址，必须传递地址字符串。 其他地图引擎的方法的工作方式类似（`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`）。
3. 运行该页并输入地址。 页面将显示一个基于 Google Maps 的地图，其中显示指定的位置。

     ![映射-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>基于纬度和经度坐标创建地图（使用必应）

此示例演示如何基于坐标创建地图。 此示例演示如何使用 Bing 地图以及如何包含必应关键字。 （也可以在不使用必应密钥的情况下，基于使用其他地图引擎的坐标创建地图。）

1. 在站点的根目录中创建一个名为*MapCoordinates*的文件，并将现有内容替换为以下代码和标记：

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. 将 `your-key-here` 替换为之前生成的 Bing 地图密钥。
3. 运行*MapCoordinates*页，输入纬度和经度坐标，然后单击**地图！** 按钮。 （如果您不知道任何坐标，请尝试以下。 这是 Microsoft Redmond 校园的位置。）

   - 纬度：47.6781005859375
   - 经度：-122.158317565918

     该页使用您指定的坐标来显示。

     ![映射-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[Microsoft Maps API 参考](https://msdn.microsoft.com/library/gg427611.aspx)
