---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 在 ASP.NET 网页（Razor）网站中创建和使用帮助器 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中创建帮助程序。 帮助器是一个可重用的组件，其中包含代码和到性能的标记 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454304"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET 网页（Razor）网站中创建和使用 Helper

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中创建帮助程序。 *帮助器*是一种可重用的组件，其中包括用于执行可能比较繁琐或复杂的任务的代码和标记。
> 
> **你将学习的内容：** 
> 
> - 如何创建和使用简单的帮助器。
> 
> 下面是本文中介绍的 ASP.NET 功能：
> 
> - `@helper` 语法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="overview-of-helpers"></a>帮助器概述

如果需要在站点中的不同页面上执行相同的任务，则可以使用帮助程序。 ASP.NET 网页包括多个帮助程序，你可以下载和安装更多的帮助程序。 （ [ASP.NET API 快速参考](https://go.microsoft.com/fwlink/?LinkId=202907)中列出了 ASP.NET 网页中的内置帮助程序列表。）如果现有的帮助程序都不能满足您的需要，您可以创建自己的帮助程序。

利用帮助程序，可以在多个页中使用通用代码块。 假设你经常需要在页面中创建与普通段落分开设置的注释项。 也许会将便笺创建为样式为带有边框的框的 `<div>` 元素。 您不必在每次要显示便笺时将此同一标记添加到页面，而是可以将标记打包为帮助程序。 然后，你可以在所需的任何位置使用一行代码插入注释。

使用与此类似的帮助程序使每个页面中的代码更简单且更易于阅读。 它还使您可以更轻松地维护站点，因为如果您需要更改便笺的外观，则可以在一个位置更改标记。

## <a name="creating-a-helper"></a>创建帮助程序

此过程说明如何创建创建注释的帮助器，如刚才所述。 这是一个简单的示例，但自定义帮助器可以包含所需的任何标记和 ASP.NET 代码。

1. 在网站的根文件夹中，创建名为 "*应用\_* 的文件夹"。 这是 ASP.NET 中的保留文件夹名称，你可以在其中将代码用于组件（如帮助程序）。
2. 在*应用\_代码*文件夹中，创建一个新的*cshtml*文件并将其命名为*MyHelpers*。
3. 将现有内容替换为以下内容：

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    代码使用 `@helper` 语法来声明名为 `MakeNote`的新帮助器。 此特定帮助器使你可以传递一个名为 `content` 的参数，该参数可以包含文本和标记的组合。 帮助器使用 `@content` 变量将字符串插入到便笺正文中。

    请注意，该文件命名为*MyHelpers*，但该帮助程序名为 `MakeNote`。 可以将多个自定义帮助程序放入单个文件中。
4. 保存并关闭文件。

## <a name="using-the-helper-in-a-page"></a>在页面中使用帮助器

1. 在根文件夹中，创建名为*TestHelper*的新空白文件。
2. 向文件中添加以下代码：

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    若要调用创建的帮助程序，请使用 `@` 后跟帮助器是的文件名、点，然后是帮助程序名称。 （如果应用中有多个文件夹 *\_代码*文件夹，则可以使用语法 `@FolderName.FileName.HelperName` 在任何嵌套文件夹级别中调用帮助程序）。 在括号内的引号内添加的文本是帮助程序将在网页中作为注释的一部分显示的文本。
3. 保存页面并在浏览器中运行它。 帮助器生成注释项权限，在这两个段落之间调用帮助程序：。

    ![显示浏览器中页的屏幕截图，以及帮助器生成的标记如何在指定文本周围放置一个框。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>其他资源

[作为 Razor helper 的水平菜单](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。 Mike Pope 的此博客文章演示了如何使用标记、CSS 和代码将水平菜单创建为帮助器。

[在 WebMatrix 和 ASP.NET MVC3 的 ASP.NET 网页帮助程序中利用 HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。 Sam Abraham 的此博客条目显示了一个帮助器，用于呈现 HTML5 `Canvas` 元素。

[WebMatrix 中 @Helpers 和 @Functions 之间的差异](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。 Mike Brind 的此博客文章介绍 `@helper` 语法和 `@function` 语法，以及何时使用它们。
