---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 将社交网络添加到 ASP.NET 网页（Razor）站点 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何将站点与社交网络服务集成。 在本章中，你将了解如何允许人员将你的网站做成书签/链接 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422954"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>将社交网络添加到 ASP.NET 网页（Razor）站点

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何将适用于 Facebook、Twitter、Reddit 和 Digg 的社交网络链接添加到 ASP.NET 网页（Razor）网站中的页面，以及如何包含 Twitter 源、Xbox 游戏者卡和 Gravatar 映像。
> 
> 学习内容：
> 
> - 如何让用户加入书签/链接您的网站。
> - 如何添加 Twitter 源。
> - 如何将**类似于**Facebook 的按钮添加到页面中。
> - 如何呈现 Gravatar.com 图像。
> - 如何在你的站点上显示 Xbox 游戏者卡。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）2
> - ASP.NET Web 帮助程序库（NuGet 包）
>   
> 
> 本教程还适用于 ASP.NET 网页3，但使用 ASP.NET Web Helper Library 的部分除外。

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>链接社交网站上的网站

如果用户赞了网站上的内容，通常需要与朋友分享。 可以通过显示用户可单击以在 Digg、Reddit、Facebook、Twitter 或类似站点上共享页面的字形（图标）来简化此过程。

若要显示这些字形，请将 `LinkSharecode` 帮助器添加到页面。 访问页面的用户可以单击单个字形。 如果他们具有使用该社交网络站点的帐户，则他们可以在该站点上发布指向页面的链接。

![图片1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. 如在[ASP.NET 网页站点中安装帮助](https://go.microsoft.com/fwlink/?LinkId=252372)程序中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。-创建名为*ListLinkShare*的页并添加以下标记：

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    在此示例中，当 `LinkShare` 帮助程序运行时，会将页标题作为参数传递，进而会将页面标题传递到社交网络站点。 但是，可以传入任何所需的字符串。 此示例还指定要包含在列表中的社交网络站点。 你可以指定与你的网站相关的社交网络站点。
2. 在浏览器中运行*ListLinkShare*页。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）
3. 单击要注册的某个网站的标志符号。 该链接会将你转到所选社交网络站点上可共享链接的页面。 例如，如果单击 "Reddit" 链接，则转到 Reddit 网站上的 "`submit to reddit`" 页。

     ![图片2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>添加 Twitter 源

有关使用与当前版本的 Twitter API 兼容的 Twitter 帮助器的信息，请参阅[twitter 帮助](../ui-layouts-and-themes/twitter-helper.md)程序。 此示例演示如何编写您自己的帮助程序，以便您可以轻松地重复使用多个页面中的代码。

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>显示 Facebook &quot;如&quot; 按钮

在某些情况下，最好的选择是直接从社交网络提供商处获取代码，而不是依赖于帮助者。 如果社交网络提供程序更新其选项的速度比助手更新的速度更快，则更是如此。

若要将 Facebook 功能（如 "赞" 按钮）添加到站点，你可以从[developers.facebook.com](https://developers.facebook.com/)站点检索代码片段。 在 Facebook 网站上，使用其工具生成与你的网站相关的代码片段。

以下突出显示的代码是从 developers.facebook.com 站点上的 "Like" 按钮工具检索到的代码。 你必须提供自己的应用 ID。

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>呈现 Gravatar 图像

*Gravatar* （一种 &quot;全局识别的头像&quot;）是一个图像，可以在多个网站上用作你&#8212;的头像，即表示你的映像。 例如，Gravatar 可以标识论坛帖子中的人员、博客评论等。 （你可以在[http://www.gravatar.com/](http://www.gravatar.com/)上的 Gravatar 网站注册自己的 Gravatar。）如果要在网站上的人员姓名或电子邮件地址旁显示图像，则可以使用 Gravatar 帮助程序。

在此示例中，你将使用代表自己的单个 Gravatar。 使用 Gravatar 的另一种方法是让用户在网站上注册时指定其 Gravatar 地址。 （您可以了解如何让人们注册[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。）然后，只要显示该用户的信息，只需将 Gravatar 添加到显示该用户名称的位置即可。

1. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
2. 创建名为*Gravatar*的新网页。
3. 将以下标记添加到文件中： 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` 方法显示页面上的 Gravatar 图像。 若要更改图像的大小，可以将数字包含为第二个参数。 默认大小为80。 小于80的数字使图像更小。 大于80的数字会使图像变大。
4. 在 `Gravatar.GetHtml` 方法中，将 `<Your Gravatar account here>` 替换为用于 Gravatar 帐户的电子邮件地址。 （如果没有 Gravatar 帐户，可以使用该用户的电子邮件地址。）
5. 在浏览器中运行页。 该页为你指定的电子邮件地址显示两个 Gravatar 图像。 第二个图像小于第一个图像。 

    ![图片4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>显示 Xbox 游戏玩家卡

当人们联机玩 Microsoft Xbox 游戏时，每个用户都有唯一的 ID。 将以游戏者卡的形式为每个玩家保留统计信息，其中显示了其信誉、游戏玩家评分和最近玩的游戏。 如果你是 Xbox 游戏者，则可以使用 `GamerCard` 帮助程序在站点的页面上显示你的游戏者卡。

1. 根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。
2. 创建名为*XboxGamer*的新页面，并添加以下标记。

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    使用 `GamerCard.GetHtml` 属性指定要显示的游戏玩家卡的别名。
3. 在浏览器中运行页。 页面将显示您指定的 Xbox 游戏玩家卡。

    ![图片 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
