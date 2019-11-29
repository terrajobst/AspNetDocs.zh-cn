---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: 在 Repeater 中使用 ConfirmButton （VB） |Microsoft Docs
author: wenz
description: 当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。 仅在 "是" 时 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599307"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a>在 Repeater 中使用 ConfirmButton (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> 当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。 仅当单击 "是" 时，才会执行该按钮的操作，否则取消该操作。 这也可能出现在中继器中。

## <a name="overview"></a>概述

当用户单击按钮（包括 LinkButton 控件）时，AJAX 控件工具包中的 ConfirmButton 扩展器将创建 "是/否" 弹出窗口。 仅当单击 "是" 时，才会执行该按钮的操作，否则取消该操作。 这也可能出现在中继器中。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。 最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。

对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

然后需要数据源。 为了简单起见，只检索 AdventureWorks 的 "供应商" 表中的前五个条目。 请注意，使用 Visual Studio 向导创建数据源时，表名称（`Vendors`）当前没有正确地以 `Purchasing`为前缀。 以下标记是正确的：

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

然后，可以在中继器内使用此数据源。 与往常一样，`DataBinder.Eval()` 方法从数据源中检索数据。 然后，必须将 `ConfirmButtonExtender` 控件放置在 repeater 的 `<ItemTemplate>` 部分中，以便将其显示在数据源中的每个条目中。

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

[!["确认" 按钮显示在数据源中的每个条目旁边](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

"确认" 按钮显示在数据源中的每个条目旁边（[单击以查看完全大小的图像](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一部分](using-a-confirmbutton-in-a-repeater-cs.md)
