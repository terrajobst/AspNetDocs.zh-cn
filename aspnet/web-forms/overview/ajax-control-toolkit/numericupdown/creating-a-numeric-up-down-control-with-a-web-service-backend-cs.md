---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: 使用 Web 服务后端创建数字向上/向下控件（C#） |Microsoft Docs
author: wenz
description: 不允许用户在复选框中键入值，而是将数字向上/向下控件（在 Windows 和其他操作系统上存在）视为更多的 c 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598878"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a>使用 Web 服务后端创建数字增大/减小控件 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)

> 不允许用户在复选框中键入值，而是在 Windows 和其他操作系统上的数字向上/向下控制（存在于 Windows 和其他操作系统上）可以更舒适地证明。 默认情况下，NumericUpDown 控件始终将值增大或减小1，但 web 服务的灵活性更高。

## <a name="overview"></a>概述

不允许用户在复选框中键入值，而是在 Windows 和其他操作系统上的数字向上/向下控制（存在于 Windows 和其他操作系统上）可以更舒适地证明。 默认情况下，`NumericUpDown` 控件始终将值增加或减少1，但 web 服务将获得更大的灵活性。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含自动将两个按钮添加到文本框的 `NumericUpDown` 扩展器：一个用于增加其值，一个用于减小值。 但是，该控件还支持 web 服务调用（或 page 方法调用）。 当单击 "上移" 或 "下移" 按钮时，JavaScript 代码会连接到 web 服务器并在其中执行方法。 方法签名如下所示：

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

`current` 参数是文本框中的当前值;`tag` 属性是其他上下文数据，可将其设置为 `NumericUpDown` 扩展器的属性（但不是必需的）。

对于本示例，数值向上/向下控件应仅允许作为2：1、2、4、8、16、32、64等的幂的值。 因此，当用户想要增加值时，所执行的方法必须翻倍旧值;另一种方法必须将值除以2。 下面是完整的 web 服务：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

最后，创建新的 ASP.NET 页。 通常，您需要 `ScriptManager` 控件、`TextBox` 控件和 `NumericUpDownExtender` 控件。 对于后者，你必须提供 web 服务信息：

- web 方法或页方法的 `ServiceDownMethod` 名称
- 通过服务方法 `ServiceDownPath` web 服务的路径;如果使用 page 方法，则省略
- 向上 web 方法或页方法 `ServiceUpMethod` 名称
- 具有 up 服务方法的 web 服务 `ServiceUpPath` 路径;如果使用 page 方法，则省略

下面是页面的完整标记：

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

如果运行该页面，请注意在单击上方按钮时文本框中的值始终是双精度值，单击下方的按钮时，该按钮的值将减半。

[仅 ![显示2的幂的数字](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

仅显示2的幂的数字（[单击以查看完全大小的图像](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)
