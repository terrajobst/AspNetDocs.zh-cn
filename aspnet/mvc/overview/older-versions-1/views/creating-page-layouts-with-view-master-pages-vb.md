---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 用查看母版页创建页面布局（VB） |Microsoft Docs
author: microsoft
description: 在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。 您可以使用 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 97c0ecf1953cc54030656dd710a5150243877110
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593944"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>使用视图母版页创建页面布局 (VB)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。 例如，您可以使用视图母版页来定义两列的页面布局，并为 web 应用程序中的所有页面使用两列布局。

## <a name="creating-page-layouts-with-view-master-pages"></a>用查看母版页创建页面布局

在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。 例如，您可以使用视图母版页来定义两列的页面布局，并为 web 应用程序中的所有页面使用两列布局。

还可以利用 "查看母版页" 在应用程序的多个页面上共享公共内容。 例如，您可以将您的网站徽标、导航链接和横幅广告置于视图母版页中。 这样，应用程序中的每个页面都将自动显示此内容。

在本教程中，您将了解如何创建新的视图母版页，并基于母版页创建新的视图内容页。

### <a name="creating-a-view-master-page"></a>创建视图母版页

首先，让我们创建一个定义两列布局的视图母版页。 通过右键单击 Views\Shared 文件夹，选择菜单选项 "**添加"、"新建项**"，然后选择 "Mvc 视图母版页" 模板（请参阅图1），可将新的视图母版页添加到 mvc 项目。

[添加视图母版页 ![](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**图 01**：添加视图母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-vb/_static/image3.png)）

您可以在一个应用程序中创建多个视图母版页。 每个视图母版页都可以定义不同的页面布局。 例如，您可能希望某些页面具有两列布局，而其他页面具有三列布局。

视图母版页的外观非常类似于标准的 ASP.NET MVC 视图。 但与普通视图不同，视图母版页包含一个或多个 `<asp:ContentPlaceHolder>` 标记。 `<contentplaceholder>` 标记用于标记可以在单个内容页中重写的母版页区域。

例如，列表1中的 "视图" 母版页定义一个两列的布局。 它包含两个 `<contentplaceholder>` 标记。 每个列一个 `<ContentPlaceHolder>`。

**列表1– `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

列表1中的 "视图" 母版页的主体包含两个对应于两个列的 `<div>` 标记。 级联样式表列类可应用于这两个 `<div>` 标记。 此类是在母版页顶部声明的样式表中定义的。 可以通过切换到设计视图预览视图母版页的呈现方式。 单击源代码编辑器左下角的 "设计" 选项卡（参见图2）。

[在设计器中预览母版页 ![](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**图 02**：在设计器中预览母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-vb/_static/image6.png)）

### <a name="creating-a-view-content-page"></a>创建视图内容页

创建视图母版页后，可以创建一个或多个基于视图母版页的视图内容页。 例如，您可以通过右键单击 Views\Home 文件夹，选择 "**添加"、"新建项**"，选择 " **MVC 视图内容页**" 模板，输入名称 ""，然后单击 "添加" 按钮（见图3），为 Home 控制器创建索引视图内容页。

[![添加视图内容页](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**图 03**：添加视图内容页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-vb/_static/image9.png)）

单击 "添加" 按钮后，将出现一个新对话框，您可以在其中选择要与 "查看内容" 页关联的视图母版页（参见图4）。 你可以导航到在上一部分中创建的 "母版视图" 母版页。

[![选择母版页](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**图 04**：选择一个母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-vb/_static/image12.png)）

基于网站母版页创建新的视图内容页后，将获取列表2中的文件。

**列表2– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

请注意，此视图包含与 "查看母版页" 中每个 `<asp:ContentPlaceHolder>` 标记对应的 `<asp:Content>` 标记。 每个 `<asp:Content>` 标记都包含一个 ContentPlaceHolderID 属性，该属性指向其重写的特定 `<asp:ContentPlaceHolder>`。

此外，请注意，列表2中的内容视图页面不包含任何正常的打开和关闭 HTML 标记。 例如，它不包含开始和关闭 `<html>` 或 `<head>` 标记。 所有正常的开始标记和结束标记都包含在 "视图" 母版页中。

您要在 "视图内容" 页中显示的任何内容都必须放置在 `<asp:Content>` 标记中。 如果将任何 HTML 或其他内容放置在这些标记之外，则在您尝试查看该页面时，您将收到错误消息。

您无需覆盖内容视图页面中母版页的每个 `<asp:ContentPlaceHolder>` 标记。 仅当要将标记替换为特定内容时，才需要覆盖 `<asp:ContentPlaceHolder>` 标记。

例如，列表3中修改的索引视图仅包含两个 `<asp:Content>` 标记。 每个 `<asp:Content>` 标记都包含一些文本。

**列表 3-`Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

当请求列表3中的视图时，它将呈现图5中的页面。 请注意，视图呈现了包含两个列的页。 此外，请注意，"查看内容" 页中的内容将与 "视图" 母版页中的内容合并。

[!["索引视图内容" 页](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**图 05**：索引视图内容页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-vb/_static/image15.png)）

### <a name="modifying-view-master-page-content"></a>修改视图母版页内容

与查看母版页一起使用时，几乎立即遇到的一个问题是在请求不同的视图内容页时修改视图母版页内容的问题。 例如，你希望你的 web 应用程序中的每个页面都具有唯一的标题。 但是，该标题在 "视图" 母版页中声明，而不是在 "查看内容" 页中声明。 那么，如何为每个视图内容页自定义页面标题呢？

可以通过两种方式来修改视图内容页显示的标题。 首先，可以将页面标题分配给在视图内容页顶部声明的 `<%@ page %>` 指令的 title 属性。 例如，如果要将页标题 "超级优秀网站" 分配给索引视图，则可以在索引视图的顶部包含以下指令：

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

当向浏览器呈现索引视图时，所需标题会显示在浏览器标题栏中：

[![浏览器标题栏](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

若要使 title 属性正常工作，必须满足主视图页面的一项重要要求。 "视图" 母版页必须包含 `<head runat="server">` 标记，而不是其标题的常规 `<head>` 标记。 如果 `<head>` 标记不包括 runat = "server" 属性，则不会显示标题。 默认视图母版页包含所需的 `<head runat="server">` 标记。

修改单独视图内容页中的母版页内容的另一种方法是在 `<asp:ContentPlaceHolder>` 标记中包装要修改的区域。 例如，假设您不仅要更改标题，还需要更改由主视图页面呈现的元标记。 列表4中的母版视图页面在其 `<head>` 标记内包含一个 `<asp:ContentPlaceHolder>` 标记。

**列表 4-`Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

请注意，列表4中的 `<asp:ContentPlaceHolder>` 标记包含默认内容：默认标题和默认 meta 标记。 如果在单个视图内容页中不覆盖此 `<asp:ContentPlaceHolder>` 标记，则将显示默认内容。

列表5中的内容视图页面会重写 `<asp:ContentPlaceHolder>` 标记，以便显示自定义标题和自定义元标记。

**列表5– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>总结

本教程提供了查看母版页和查看内容页的基本简介。 已了解如何创建新的视图母版页，并基于这些页面创建视图内容页。 还介绍了如何从特定的视图内容页修改视图母版页的内容。

> [!div class="step-by-step"]
> [上一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [下一页](passing-data-to-view-master-pages-vb.md)
