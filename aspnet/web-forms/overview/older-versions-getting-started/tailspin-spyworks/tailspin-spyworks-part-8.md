---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 第8部分：最终页面、异常处理和结论 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第8部分添加联系人页，"关于" 页和 "异常"。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474338"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>第8部分：最终页面、异常处理和结论

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第8部分添加联系人页、关于页和异常处理。 这是序列的结论。

## <a id="_Toc260221680"></a>联系人页（从 ASP.NET 发送电子邮件）

创建名为 ContactUs 的新页

使用设计器创建以下窗体，以特殊说明将 ToolkitScriptManager 和 Editor 控件包含在 AjaxControlToolkit 中。 .

![](tailspin-spyworks-part-8/_static/image1.jpg)

双击 "提交" 按钮以在代码隐藏文件中生成一个 click 事件处理程序，并实现一个方法以将联系人信息作为电子邮件发送。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

此代码要求 web.config 文件包含配置节中的条目，该条目指定用于发送邮件的 SMTP 服务器。

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>关于页面

创建一个名为 "AboutUs" 的页面，并添加所需的任何内容。

## <a id="_Toc260221682"></a>全局异常处理程序

最后，在整个应用程序中，我们引发了异常，并且在某些情况下，冷还会导致在 web 应用程序中出现未经处理的异常。

我们永远不希望向网站访问者显示未处理的异常。

![](tailspin-spyworks-part-8/_static/image2.jpg)

除了造成严重的用户体验，未经处理的异常也可能是安全问题。

为了解决此问题，我们将实现一个全局异常处理程序。

为此，请打开 global.asax 文件，并记下预先生成的事件处理程序。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

添加代码以实现应用程序\_错误处理程序，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

然后向解决方案添加一个名为 "Error" 的页，并添加此标记段。

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

现在，在页面\_Load 事件处理程序从 Request 对象中提取错误消息。

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>结论

我们已看到，ASP.NET WebForms 可让你轻松地创建具有数据库访问权限、成员资格、AJAX 等的复杂网站。 速度非常快。

希望本教程提供了开始构建自己的 ASP.NET WebForms 应用程序所需的工具！

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-7.md)
