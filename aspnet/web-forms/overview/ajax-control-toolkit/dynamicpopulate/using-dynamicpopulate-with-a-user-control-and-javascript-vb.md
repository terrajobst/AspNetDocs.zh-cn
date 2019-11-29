---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 将通过 dynamicpopulate 与用户控件和 JavaScript 一起使用（VB） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599117"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>通过用户控件和 JavaScript 使用 DynamicPopulate (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。 还可以使用自定义客户端 JavaScript 代码触发填充。 但当扩展器驻留在用户控件中时，必须特别小心。

## <a name="overview"></a>概述

ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。 还可以使用自定义客户端 JavaScript 代码触发填充。 但当扩展器驻留在用户控件中时，必须特别小心。

## <a name="steps"></a>步骤

首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulateExtender` 控件调用的方法。 Web 服务实现 `getDate()` 方法，该方法需要一个名为 `contextKey`的字符串类型参数，因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。 下面是以下列三种格式之一检索当前日期的代码（文件 `DynamicPopulate.vb.asmx`）：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

在下一步中，创建一个新的用户控件（`.ascx` 文件），该控件的第一行由以下声明表示：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

&lt;`label`&gt; 元素将用于显示来自服务器的数据。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

另外，在用户控件文件中，我们将使用三个单选按钮，每个按钮表示 web 服务支持的三种可能日期格式之一。 当用户单击某个单选按钮时，浏览器将执行如下所示的 JavaScript 代码：

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

此代码访问 `DynamicPopulateExtender` （不要担心奇怪的 ID，稍后将在此进行介绍）并触发数据的动态填充。 在当前单选按钮的上下文中，`this.value` 引用 `format1`的值，`format2` 或 `format3` web 方法所需的内容。

用户控件中唯一缺少的内容是将单选按钮链接到 web 服务的 `DynamicPopulateExtender` 控件。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

同样，您可以记下控件中使用的奇怪 ID： `mcd1$myDate` 而不是 `myDate`。 以前，`mcd1_dpe1` 使用的 JavaScript 代码访问 `DynamicPopulateExtender` 而不是 `dpe1`。此命名策略是在用户控件中使用 `DynamicPopulateExtender` 时的特殊要求。 而且，您必须以特定方式嵌入用户控件，才能使其全部工作。 创建新的 ASP.NET 页面，并为刚刚实现的用户控件注册标记前缀：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

然后，在新页上包含 ASP.NET AJAX `ScriptManager` 控件：

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

最后，将用户控件添加到页面。 你只需设置其 `ID` 属性（当然还 `runat="server"`），但你还必须将其设置为特定名称： `mcd1`，因为这是在用户控件内使用 JavaScript 访问它所使用的前缀。

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

就是这么简单！ 页面按预期方式工作：用户单击某个单选按钮，工具箱中的控件将调用 web 服务并以所需格式显示当前日期。

[![单选按钮驻留在用户控件中](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

单选按钮位于用户控件中（[单击以查看完全大小的图像](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一部分](dynamically-populating-a-control-using-javascript-code-vb.md)
