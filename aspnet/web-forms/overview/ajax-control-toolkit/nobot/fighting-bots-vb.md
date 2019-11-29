---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
title: 反击 Bot （VB） |Microsoft Docs
author: wenz
description: 自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。 ASP.NET 中的 NoBot 控件 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9803150-452d-4521-97e3-d75d5599383c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-vb
msc.type: authoredcontent
ms.openlocfilehash: a8ca71b96cb84c97b1a60ae6a3d1a129cd1b0b10
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606397"
---
# <a name="fighting-bots-vb"></a>外部测试机器人 (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0VB.pdf)

> 自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。 ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。

## <a name="overview"></a>概述

自动机器人 plaster 网络日志和其他具有垃圾邮件的网站，无需任何用户交互即可提交注释表单。 ASP.NET AJAX 控件工具包中的 NoBot 控件可帮助抵御这些机器人。

## <a name="steps"></a>步骤

抵御 bot 的一种常见方法是使用 CAPTCHAs 完全自动化的公共把测试来区分计算机和人。 把测试最初是一种测试，在此测试中，有人需要确定通信合作伙伴是否是人或计算机。 在 web 中，CAPTCHA 通常包含一个图像，其中包含一些扭曲的字母。 其思想是，只有人可以读取图像上的字母，而 OCR 算法将会失败。

此方法有几个优点和缺点，但本教程的讨论范围之外对此进行了讨论。 但 ASP.NET AJAX 控件工具包中有一个控件，它提供类似的方法： `NoBot`。 与 CAPTCHA 相比，此方法更易于克服，但在博客上非常易于使用和费用，如果大多数垃圾邮件尝试失效（`NoBot` 控制可执行此操作），则会将其视为成功。

如果至少满足以下条件之一，`NoBot` 会截获当前 ASP.NET web 窗体的回发：

- 浏览器未能解决 JavaScript 谜题（例如，在停用 JavaScript 时）
- 用户已将窗体提交到快速
- 在特定时间段内，客户端 IP 地址的提交时间太长。

若要检查这些情况，`NoBot` 控件需要这些属性（它们都是可选的）：

- 回发之间 `ResponseMinimumDelaySeconds` 最小秒数
- `CutoffWindowSeconds` 时间间隔，其中一个 IP 的回发是度量值
- 每个时间间隔 `CutoffMaximumInstances` 最大秒数

以下标记要求在两次回发之间至少经过两秒钟的时间，并且在30秒的时间间隔内只有5次回发或更少：

[!code-aspx[Main](fighting-bots-vb/samples/sample1.aspx)]

然后，请务必将 `ScriptManager` 包含在页面中，以便加载 ASP.NET AJAX 库，并且可以使用控制工具包：

[!code-aspx[Main](fighting-bots-vb/samples/sample2.aspx)]

由于大部分检查 `NoBot` 都是在服务器端进行的，因此您需要检查这些验证的结果。 可以通过调用 `NoBot`的 `IsValid()` 方法来完成此操作。 它有一个参数（作为 `out` 参数/`ByRef` 参数），该参数的类型为 `NoBotState`。 它的字符串表示形式包含检查失败的原因，否则 `Valid`。 下面的代码根据 `NoBot`的结果输出一条消息：

[!code-aspx[Main](fighting-bots-vb/samples/sample3.aspx)]

最后，需要提交一个窗体，并使用 label 元素输出该消息，并且已完成！

[!code-aspx[Main](fighting-bots-vb/samples/sample4.aspx)]

如果在前两秒内运行此脚本并停用 JavaScript 或提交窗体，或在三十秒内提交窗体7次，将收到一条错误消息。 不过，请明智地使用此控制，因为只有大约90-95% 的用户激活了 JavaScript，因此5-10% 的用户将 `NoBot`的测试失败。

[![此错误消息可能是由机器人引起的](fighting-bots-vb/_static/image2.png)](fighting-bots-vb/_static/image1.png)

此错误消息可能是由机器人引起的（[单击查看完全大小的映像](fighting-bots-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一部分](fighting-bots-cs.md)
