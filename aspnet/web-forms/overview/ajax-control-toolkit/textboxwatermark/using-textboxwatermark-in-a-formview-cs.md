---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
title: 在 FormView （C#）中使用 TextBoxWatermark |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，我 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e6ee90bf-32a5-4987-a384-15cc7dd30c8a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-cs
msc.type: authoredcontent
ms.openlocfilehash: 13ac0da5ca53756aa7c660cdc47c96f0c865b006
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78508838"
---
# <a name="using-textboxwatermark-in-a-formview-c"></a>在 FormView 中使用 TextBoxWatermark (C#)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1CS.pdf)

> AJAX 控件工具包中的 TextBoxWatermark 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，它会被清空。 如果用户离开该框而不输入文本，则会重新出现预填充文本。 在 FormView 控件中也可以这样做。

## <a name="overview"></a>概述

AJAX 控件工具包中的 `TextBoxWatermark` 控件扩展了文本框，以便在框中显示文本。 当用户在框中单击时，它会被清空。 如果用户离开该框而不输入文本，则会重新出现预填充文本。 这也可能出现在 `FormView` 控件中。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。 最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。

对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample1.aspx)]

然后，将数据源添加到支持 `DELETE`、`INSERT` 和 `UPDATE` SQL 语句的页面。 如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。 下面的标记显示了正确的语法：

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample2.aspx)]

请记住数据源的名称（`ID`），因为它将在 `FormView` 控件的 `DataSourceID` 属性中使用。 `FormView` 的 `<InsertItemTemplate>` 部分包含一个文本框，该文本框由 `TextBoxWatermarkExtender` 控件扩展。 确保扩展程序位于模板内，而不是位于该模板之外。

[!code-aspx[Main](using-textboxwatermark-in-a-formview-cs/samples/sample3.aspx)]

现在，当用户更改为 `FormView` 控件的插入模式时，新供应商的文本字段将预先填充，因为 `TextBoxWatermarkExtender` 控件。 在文本框内单击，使填充文本消失。

[![字段中的水印来自扩展器](using-textboxwatermark-in-a-formview-cs/_static/image2.png)](using-textboxwatermark-in-a-formview-cs/_static/image1.png)

该字段中的水印来自扩展器（[单击查看完全大小的图像](using-textboxwatermark-in-a-formview-cs/_static/image3.png)）

> [!div class="step-by-step"]
> [下一部分](using-textboxwatermark-with-validation-controls-cs.md)
