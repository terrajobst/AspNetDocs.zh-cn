---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 网页的 Twitter 帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 本主题和应用程序演示如何向 WebMatrix 3 项目添加 Twitter 帮助程序。 它包含 Twitter 帮助程序代码，并演示如何调用帮助器 。
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518618"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET 网页的 Twitter 帮助程序

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Twitter 帮助程序已过时。 对于 Twitter 最新的网站参与工具，请参阅[twitter For 网站概述](https://developer.twitter.com/en/docs/twitter-for-websites/overview)。

> 本主题和应用程序演示如何向 WebMatrix 3 项目添加 Twitter 帮助程序。 它包含 Twitter 帮助程序代码，并演示如何调用帮助程序方法。
> 
> Twitter 文件的此代码由 Microsoft 的**Tian Pan**开发。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="introduction"></a>简介

本主题演示如何将 Twitter 帮助程序添加到应用程序，并使用 Razor 语法调用帮助程序方法。 Twitter 帮助器使你可以轻松地在应用程序中包含 Twitter 按钮和小组件。 若要使用 Twitter 小组件（例如用户的时间线或井号标签的搜索结果），必须先[在 Twitter 上创建该小组件](https://twitter.com/settings/widgets)。 创建小组件后，将收到小组件 id。调用显示小组件的帮助器方法时，可以将此小组件 id 作为参数传递。

本主题是针对 Twitter API 版本1.1 编写的。 通过直接将 Twitter 帮助程序代码添加到你的项目，你可以在 Twitter API 发生更改时更新帮助器代码。

有关安装 WebMatrix 的信息，请参阅[ASP.NET 网页 2-入门简介](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。

## <a name="add-twitter-helper-to-your-project"></a>将 Twitter 帮助程序添加到项目

若要添加 Twitter 帮助程序，请首先向项目中添加一个名为 "**应用\_代码**" 的文件夹。 然后，创建一个名为**Twitter**的文件。

![App_Code 文件夹](twitter-helper/_static/image1.png)

将 Twitter 中的默认代码替换为以下代码。

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>从网页调用 Twitter 方法

下面的示例演示如何在项目的页中使用 Twitter 帮助器方法。 在您的项目中，您将需要将参数值替换为与您的需求相关的值。 您可以使用提供的小组件 id 来浏览这些方法的工作方式，但您需要为您的项目生成您自己的小组件。

并非下面显示的所有参数都是必需的。 可选参数用于自定义按钮或小组件的显示方式。 例如，"关注" 按钮只要求按用户名，但该示例显示如何包含关注者的数量，以及如何指定按钮的大小和语言。

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>查看结果

上面的代码生成以下按钮和小组件。 这些按钮和小组件是功能齐全的，而不是屏幕截图。 "关注" 按钮以西班牙语显示，因为 language 参数设置为**es**。

### <a name="follow-button"></a>跟随按钮

[遵循 @aspnet）](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>推文按钮

[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>用户时间线（配置文件）

[推文 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>收藏夹

[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 收藏的推文](https://twitter.com/Microsoft/favorites)

### <a name="list"></a>列表

[来自 @Microsoft/MS\_使用者\_波段的推文](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>搜索

[有关 .net&quot;&quot;#asp 的推文](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
