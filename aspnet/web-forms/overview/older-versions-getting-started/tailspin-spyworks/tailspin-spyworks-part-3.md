---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第3部分：布局和类别菜单 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第3部分介绍添加布局和类别菜单。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519098"
---
# <a name="part-3-layout-and-category-menu"></a>第3部分：布局和类别菜单

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第3部分介绍添加布局和类别菜单。

## <a id="_Toc260221669"></a>添加一些布局和类别菜单

在我们的站点母版页中，我们将为左侧列添加一个 div，其中包含我们的产品类别菜单。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

请注意，所需的对齐和其他格式将由我们添加到我们的 Style .css 文件的 CSS 类提供。

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

"产品类别" 菜单将在运行时动态创建，方法是查询商业数据库中的现有产品类别，并创建菜单项和相应的链接。

为实现此目的，我们将使用两个 ASP。网络强大的数据控件。 "实体数据源" 控件和 "ListView" 控件。

![](tailspin-spyworks-part-3/_static/image1.jpg)

让我们切换到 "设计视图"，并使用帮助程序来配置控件。

![](tailspin-spyworks-part-3/_static/image2.jpg)

让我们将 EntityDataSource ID 属性设置为 EDS\_类别\_"菜单，然后单击" 配置数据源 "。

![](tailspin-spyworks-part-3/_static/image3.jpg)

选择为我们的 Commerce 数据库创建实体数据源模型时为我们创建的 CommerceEntities 连接，然后单击 "下一步"。

![](tailspin-spyworks-part-3/_static/image4.jpg)

选择 "类别" 实体集名称，并将其余选项保留为默认值。 单击 "完成"。

现在，让我们将放置在页面上的 ListView 控件实例的 ID 属性设置为 ListView\_ProductsMenu 并激活其帮助程序。

![](tailspin-spyworks-part-3/_static/image5.jpg)

尽管我们可以使用控件选项来设置数据项显示和格式的格式，但我们的菜单创建只需要简单标记，因此我们将在源视图中输入代码。

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

请注意 "Eval" 语句： &lt;% # Eval （"类别名称"）%&gt;

ASP.NET 语法 &lt;% #%&gt; 是一种简写约定，它指示运行时执行中包含的任何内容并在行中输出结果。

语句 Eval （"类别名称"）指示，对于数据项的绑定集合中的当前项，提取实体模型项名称 "类别名称" 的值。 这是一种非常强大的功能。

现在，让我们运行应用程序。

![](tailspin-spyworks-part-3/_static/image6.jpg)

请注意，我们的产品类别菜单现在显示，当鼠标悬停在某个类别菜单项上时，将会看到菜单项链接指向我们尚未实现的名为 ProductsList 的页，并且我们已经生成了一个包含 类别 id。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-2.md)
> [下一页](tailspin-spyworks-part-4.md)
