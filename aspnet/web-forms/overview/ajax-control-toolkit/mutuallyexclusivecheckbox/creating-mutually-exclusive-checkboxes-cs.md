---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
title: 创建互斥复选框（C#） |Microsoft Docs
author: wenz
description: 如果只能选择一组选项中的一个选项，则通常会使用单选按钮。 但有一个缺点：选中组中的一个单选按钮后,。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8e11b813-ba0d-4c29-b0f8-f65db6dbef1e
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-cs
msc.type: authoredcontent
ms.openlocfilehash: ddc154601752cc856f00dd4f3207952ab7e0e3e0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606513"
---
# <a name="creating-mutually-exclusive-checkboxes-c"></a>创建互斥复选框 (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0CS.pdf)

> 如果只能选择一组选项中的一个选项，则通常会使用单选按钮。 但有一个缺点：选中组中的一个单选按钮后，不能取消选中所有单选按钮。 任何时候都可以取消选中复选框，但并不相互排斥。 本教程提供了这两种方法的最佳方案：互相排斥的复选框。

## <a name="overview"></a>概述

如果只能选择一组选项中的一个选项，则通常会使用单选按钮。 但有一个缺点：选中组中的一个单选按钮后，不能取消选中所有单选按钮。 任何时候都可以取消选中复选框，但并不相互排斥。 本教程提供了这两种方法的最佳方案：互相排斥的复选框。

## <a name="steps"></a>步骤

ASP.NET AJAX 控件工具包包含 MutuallyExclusiveCheckBox 扩展器。 这使程序员能够为组名称（`Key` 属性）分配任何复选框。 在同一组内的所有复选框中，一次只能选择一项。

首先，将两个复选框放在新的 ASP.NET 页上。 可能还有更多，但有两个足以说明这一原则：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample1.aspx)]

对于这两个复选框，必须在页面上放置一个 MutuallyExclusiveCheckBoxExtender 控件。 这两个键特性都需要具有相同的值，就像 HTML 单选按钮元素的值特性必须完全相同以指示它们所属的组。 扩展器的 TargetControlID 属性指向复选框的 ID。

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample2.aspx)]

最后，包括 ASP.NET AJAX 控件工具包的所有元素所需的 ASP.NET AJAX `ScriptManager`：

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-cs/samples/sample3.aspx)]

保存并运行页面：可以选中和取消选中这两个复选框，但不能同时选中两个复选框。

[一次只能检查一个 checkbox ![](creating-mutually-exclusive-checkboxes-cs/_static/image2.png)](creating-mutually-exclusive-checkboxes-cs/_static/image1.png)

一次只能检查一个复选框（[单击查看完全大小的图像](creating-mutually-exclusive-checkboxes-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](creating-mutually-exclusive-checkboxes-vb.md)
