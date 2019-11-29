---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: 数据绑定到可折叠面板（VB） |Microsoft Docs
author: wenz
description: AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常是用 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599948"
---
# <a name="databinding-to-an-accordion-vb"></a>数据绑定到 Accordion (VB)

作者： [Christian Wenz](https://github.com/wenz)

[下载代码](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常在页面本身内声明，但绑定到数据源可提供更大的灵活性。

## <a name="overview"></a>概述

AJAX 控件工具包中的可折叠控件提供多个窗格，并允许用户一次显示其中一个窗格。 面板通常在页面本身内声明，但绑定到数据源可提供更大的灵活性。

## <a name="steps"></a>步骤

首先，数据源是必需的。 此示例使用 AdventureWorks 数据库和 Microsoft SQL Server 2005 Express Edition。 数据库是 Visual Studio 安装（包括 express edition）的可选部分，也可在[https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)下单独下载。 AdventureWorks 数据库是 SQL Server 2005 示例和示例数据库（ [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)）的一部分。 最简单的数据库设置方法是使用 Microsoft SQL Server Management Studio Express （[https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)）并附加 `AdventureWorks.mdf` 数据库文件。

对于此示例，我们假定 SQL Server 2005 Express Edition 的实例 `SQLEXPRESS`，并驻留在与 web 服务器相同的计算机上;这也是默认设置。 如果你的设置不同，则必须修改数据库的连接信息。

若要激活 ASP.NET AJAX 和控件工具包的功能，必须将 `ScriptManager` 控件放置在页面上的任何位置（但 `<form>` 元素中）：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

然后，将数据源添加到页面。 为了使用有限数量的数据，我们仅选择 AdventureWorks 数据库的供应商表中的前五个条目。 如果使用 Visual Studio 助手创建数据源，请记住，当前版本中的 bug 不会将表名称（`Vendor`）作为前缀，而 `Purchasing`。 下面的标记显示了正确的语法：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

请记住数据源的名称（ID）。 然后，必须在可折叠控件控件的 `DataSourceID` 属性中使用这种非常标识：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

在可折叠面板控件中，您可以为控件的各个部分提供模板，包括标题（`<HeaderTemplate>`）和内容（`<ContentTemplate>`）。 在这些元素中，只需使用 `DataBinder.Eval()` 方法从数据源输出数据：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

加载页面时，必须将数据源绑定到带有此服务器端代码的可折叠面板：

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

若要结束此示例，您需要定义在可折叠面板控件中引用的两个 CSS 类（在其属性中 `HeaderCssClass` 和 `ContentCssClass`）。 在页面的 "`<head>`" 部分中添加以下标记：

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

[![可折叠的数据直接来自数据源](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

可折叠的数据直接来自数据源（[单击查看完全大小的图像](databinding-to-an-accordion-vb/_static/image3.png)）

> [!div class="step-by-step"]
> [上一页](dynamically-adding-an-accordion-pane-cs.md)
> [下一页](dynamically-adding-an-accordion-pane-vb.md)
