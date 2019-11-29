---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: 将通过 hovermenu 与 Repeater 控件（C#）一起使用 |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的通过 hovermenu 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在特定上出现一个弹出窗口 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606695"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>通过 Repeater 控件使用 HoverMenu (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> AJAX 控件工具包中的通过 hovermenu 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在指定位置显示一个弹出窗口。 还可以在 repeater 中使用此控件。

## <a name="overview"></a>概述

AJAX 控件工具包中的 `HoverMenu` 控件提供了一个简单的弹出效果：当鼠标指针悬停在某个元素上时，将在指定位置显示一个弹出窗口。 还可以在 repeater 中使用此控件。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。 最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。

对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

然后，将数据源添加到页面。 为了使用有限数量的数据，我们仅选择 AdventureWorks 数据库的供应商表中的前五个条目。 如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。 下面的标记显示了正确的语法：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

接下来，添加一个面板作为模式弹出窗口：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

现在，`HoverMenuExtender` 进入播放。 为了使数据源中的每个元素均获取其弹出式窗口，必须将扩展器置于 repeater `<ItemTemplate>` 部分中。 此处为标记：

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

现在，数据源中的每个项都显示一个弹出窗口（`PopupPosition` 属性），延迟为50毫秒（`PopDelay` 属性）。

[![在 repeater 中的每一项旁边显示悬停菜单](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

悬停菜单显示在 repeater 中每个项的旁边（[单击以查看完全大小的图像](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一页](using-hovermenu-with-a-repeater-control-vb.md)
