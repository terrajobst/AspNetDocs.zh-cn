---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第6部分： ASP.NET 成员身份 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第6部分添加 ASP.NET 成员身份。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454880"
---
# <a name="part-6-aspnet-membership"></a>第6部分： ASP.NET 成员身份

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第6部分添加 ASP.NET 成员身份。

## <a id="_Toc260221672"></a>使用 ASP.NET 成员身份

![](tailspin-spyworks-part-6/_static/image1.png)

单击 "安全"

![](tailspin-spyworks-part-6/_static/image1.jpg)

请确保使用的是窗体身份验证。

![](tailspin-spyworks-part-6/_static/image2.jpg)

使用 "创建用户" 链接创建几个用户。

![](tailspin-spyworks-part-6/_static/image3.jpg)

完成后，请参阅 "解决方案资源管理器" 窗口并刷新视图。

![](tailspin-spyworks-part-6/_static/image2.png)

请注意，ASPNETDB.MDF。已创建 MDF 精细。 此文件包含支持核心 ASP.NET 服务（如成员身份）的表。

现在，我们可以开始实现结帐过程。

首先创建一个 "CheckOut" 页。

只应将 "CheckOut" 页提供给已登录的用户，这样我们就可以将访问权限限制为已登录的用户，并将不登录的用户重定向到登录页。

为此，我们将以下内容添加到 web.config 文件的配置节。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

ASP.NET Web 窗体应用程序的模板会自动将身份验证部分添加到 web.config 文件中，并建立默认登录页。

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

当用户登录时，必须修改登录 .aspx 代码隐藏文件，以迁移匿名购物车。 按如下所示\_Load 事件更改页面。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

然后，添加类似于下面的 "LoggedIn" 事件处理程序，将会话名称设置为新登录的用户，并通过在 MyShoppingCart 类中调用 MigrateCart 方法，将购物车中的临时会话 id 更改为该用户的会话 id。 （在 .cs 文件中实现）

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

实现如下所示的 MigrateCart （）方法。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

在签出 .aspx 中，我们将使用 EntityDataSource 和 GridView 在我们的 "购物车" 页中。

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

请注意，我们的 GridView 控件指定了一个名为 MyList 的 "ondatabound" 事件处理程序\_RowDataBound，因此让我们按如下所示实现此事件处理程序。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

此方法会在每行被绑定时保留购物车的运行总计，并更新 GridView 的底部行。

在此阶段，我们已实现了要放置的订单的 "评审" 演示。

让我们通过在页面\_Load 事件中添加几行代码来处理空购物车方案：

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

当用户单击 "提交" 按钮时，将在提交按钮单击事件处理程序中执行以下代码。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

订单提交过程的 "肉类" 将在我们的 MyShoppingCart 类的订单（）方法中实现。

订单将：

- 获取购物车中的所有行项，并使用它们创建新订单记录和关联的 OrderDetails 记录。
- 计算寄送日期。
- 清除购物车。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

在此示例应用程序中，我们只需将两天加到当前日期即可计算发货日期。

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

现在，运行应用程序将允许我们测试从一开始到完成的购物过程。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-5.md)
> [下一页](tailspin-spyworks-part-7.md)
