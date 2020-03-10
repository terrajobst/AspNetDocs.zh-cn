---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: 动态填充控件（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430556"
---
# <a name="dynamically-populating-a-control-c"></a>动态填充控件 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)

> ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。 本教程演示如何对此进行设置。

## <a name="steps"></a>步骤

首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulate`要调用的方法。 Web 服务类需要 `Microsoft.Web.Script.Services`中定义的 `ScriptService` 特性;否则，ASP.NET AJAX 无法为 web 服务创建客户端 JavaScript 代理，而 `DynamicPopulate`需要这样做。

Web 方法必须预期一个 string 类型的参数（称为 `contextKey`），因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。 以下 web 服务以 `contextKey` 参数表示的格式返回当前日期：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

然后，web 服务将另存为 `DynamicPopulate.cs.asmx`。 或者，您可以使用 `DynamicPopulate` 控件将 `getDate()` 方法作为实际 ASP.NET 页中的页方法实现。

在下一步中，创建一个新的 ASP.NET 文件。 与往常一样，第一步是将 `ScriptManager` 包含在当前页面中，以加载 ASP.NET AJAX 库并使控件工具包工作：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

然后，添加 "标签" 控件（例如，使用同一名称的 HTML 控件，或 &lt;`asp:Label` /&gt; web 控件中），后者稍后会显示 web 服务调用的结果。

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

HTML 按钮（作为 HTML 控件，因为我们不需要回发到服务器）将用于触发动态填充：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

最后，我们需要 `DynamicPopulateExtender` 控件来连接问题。 将设置以下属性（`ID` 和 `runat`=`"server"`）：

- `TargetControlID` 在何处放置 web 服务调用的结果
- web 服务的 `ServicePath` 路径（如果要使用 page 方法，则省略）
- web 方法或页方法 `ServiceMethod` 名称
- `ContextKey` 要发送到 web 服务的上下文信息
- 触发 web 服务调用的 `PopulateTriggerControlID` 元素
- `ClearContentsDuringUpdate` 在 web 服务调用期间是否清空目标元素

正如您所看到的那样，控件需要一些信息，但将所有内容放在适当的位置都是非常简单的。 下面是当前方案中 `DynamicPopulateExtender` 控件的标记：

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

在浏览器中运行 "ASP.NET" 页，然后单击该按钮;您将收到以月/日为年份的当前日期。

[![单击该按钮将从服务器中检索日期](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)

单击该按钮将从服务器中检索日期（[单击查看完全大小的图像](dynamically-populating-a-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一部分](dynamically-populating-a-control-using-javascript-code-cs.md)
