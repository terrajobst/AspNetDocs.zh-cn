---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: 使用 TagBuilder 类生成 HTML 帮助程序（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 介绍了名为 TagBuilder 类的 ASP.NET MVC 框架中的有用实用工具类。 你可以使用 TagBuilder 类轻松 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485582"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a>使用 TagBuilder 类生成 HTML 帮助程序（VB）

作者： [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 介绍了名为 TagBuilder 类的 ASP.NET MVC 框架中的有用实用工具类。 可以使用 TagBuilder 类轻松生成 HTML 标记。

ASP.NET MVC 框架包含一类有用的实用工具类，该类可在生成 HTML 帮助器时使用。 作为类的名称，TagBuilder 类使你能够轻松地生成 HTML 标记。 本 brief 教程提供了 TagBuilder 类的概述，并介绍了如何在生成简单的 HTML 帮助器时使用此类，该帮助器将 HTML &lt;img&gt; 标记。

## <a name="overview-of-the-tagbuilder-class"></a>TagBuilder 类概述

TagBuilder 类包含在 System.web 命名空间中。 它有五种方法：

- AddCssClass （）–使你可以向标记添加新的*类 = ""* 特性。
- GenerateId （）–使你可以向标记添加 id 属性。 此方法自动替换 id 中的句点（默认情况下，句点替换为下划线）
- MergeAttribute （）–使你可以向标记添加特性。 此方法有多个重载。
- SetInnerText （）–使你能够设置标记的内部文本。 内部文本自动编码。
- ToString （）–使你能够呈现标记。 您可以指定是要创建普通标记、开始标记、结束标记还是自结束标记。

TagBuilder 类具有四个重要属性：

- 特性–表示标记的所有属性。
- IdAttributeDotReplacement –表示 GenerateId （）方法用来替换句号的字符（默认值为下划线）。
- InnerHTML –表示标记的内部内容。 将字符串分配给此属性不*会*对字符串进行 HTML 编码。
- TagName –表示标记的名称。

这些方法和属性为您生成一个 HTML 标记所需的所有基本方法和属性。 你实际上不需要使用 TagBuilder 类。 可以改用 StringBuilder 类。 但是，TagBuilder 类使你的生活变得更加简单。

## <a name="creating-an-image-html-helper"></a>创建图像 HTML 帮助器

当你创建 TagBuilder 类的实例时，会将你想要生成的标记的名称传递到 TagBuilder 构造函数。 接下来，可以调用 AddCssClass 和 MergeAttribute （）方法等方法来修改标记的属性。 最后，调用 ToString （）方法以呈现标记。

例如，列表1包含图像 HTML 帮助器。 图像帮助器在内部使用表示 HTML &lt;img&gt; 标记的 TagBuilder 来实现。

**列表1– Helpers\ImageHelper.vb**

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

列表1中的模块包含两个名为 Image （）的重载方法。 调用 Image （）方法时，可以传递表示一组 HTML 特性的对象。

请注意如何使用 MergeAttribute （）方法将 TagBuilder 属性（如 src 属性）添加到 TagBuilder。 另外请注意，TagBuilder MergeAttributes （）方法如何用于将属性集合添加到 TagBuilder。 MergeAttributes （）方法接受&lt;string、object&gt; 参数的字典。 RouteValueDictionary 类用于将表示属性集合的对象转换为字典&lt;string、Object&gt;。

创建图像帮助器后，可以像使用任何其他标准 HTML 帮助器一样在 ASP.NET MVC 视图中使用帮助器。 清单2中的视图使用图像帮助器来显示同一次 Xbox 的同一图像（参见图1）。 Image （）帮助器在带有和不带 HTML 特性集合的情况下调用。

**列表 2-Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

[!["新建项目" 对话框](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)

**图 01**：使用图像帮助器（[单击以查看完全大小的图像](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png)）

请注意，您必须导入与 "索引 .aspx" 视图顶部的图像帮助器关联的命名空间。 将通过以下指令导入帮助器：

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

在 Visual Basic 应用程序中，默认命名空间与应用程序的名称相同。

> [!div class="step-by-step"]
> [上一页](creating-custom-html-helpers-vb.md)
> [下一页](creating-page-layouts-with-view-master-pages-vb.md)
