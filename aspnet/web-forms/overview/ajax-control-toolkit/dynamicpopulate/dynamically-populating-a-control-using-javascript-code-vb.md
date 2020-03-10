---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: 使用 JavaScript 代码动态填充控件（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497378"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>使用 JavaScript 代码动态填充控件 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。 还可以使用自定义客户端 JavaScript 代码触发填充。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。 还可以使用自定义客户端 JavaScript 代码触发填充。

## <a name="steps"></a>步骤

首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulateExtender` 控件调用的方法。 Web 服务实现 `getDate()` 方法，该方法需要一个名为 `contextKey`的字符串类型参数，因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。 下面是以下列三种格式之一检索当前日期的代码（文件 `DynamicPopulate.vb.asmx`）：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

在下一步中，创建一个新的 ASP.NET 网站，并从 ASP.NET AJAX ScriptManager 控件开始：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

然后，添加 "标签" 控件（例如，使用同一名称的 HTML 控件或 `<asp:Label />` web 控件），稍后会显示 web 服务调用的结果。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

接下来，请提供 `DynamicPopulateExtender` 控件并提供 web 服务信息、目标控件，但不能使用自定义 JavaScript 来触发填充的控件的名称。

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

立即到 JavaScript 部分。 ASP.NET AJAX 库定义的 `$find()` 函数返回对 ASP.NET AJAX 控件工具包（如 `DynamicPopulateExtender`）的服务器端对象的引用。 在当前文件中，`$find("dpe")` 返回对页中一个 `DynamicPopulateExtender` 控件的引用。 它公开一个称为 `populate()` 的方法，该方法将触发动态填充过程。 `populate()` 方法需要一个参数：作为 `getDate()` web 方法的参数的上下文键。 例如，`$find("dpe").populate("format1")` 会用月格式的当前日期填充标签。

为了使示例更灵活，用户现在可以在几种日期格式之间进行选择。 对于其中的每个，将显示单选按钮。 用户单击某个单选按钮后，JavaScript 代码将使用所选日期格式动态填充该标签。 这些单选按钮如下所示：

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

请注意，在单选按钮的上下文中，JavaScript 表达式 `this.value` 引用当前按钮的值，这恰好与 `getDate()` 方法可以使用的信息完全相同。

[![单击该按钮将以指定的格式从服务器中检索日期](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

单击该按钮将以指定的格式从服务器中检索日期（[单击查看完全大小的图像](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](dynamically-populating-a-control-vb.md)
> [下一页](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
