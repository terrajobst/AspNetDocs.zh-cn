---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX 控件工具包入门 |Microsoft Docs
author: microsoft
description: 了解开始使用 AJAX 控件工具包所需的所有知识。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497138"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>AJAX 控件工具包入门 (VB)

由[Microsoft](https://github.com/microsoft)

> 了解开始使用 AJAX 控件工具包所需的所有知识。

AJAX 控件工具包包含30多个免费控件，可以在 ASP.NET 应用程序中使用。 在本教程中，您将了解如何下载 AJAX 控件工具包并将工具包控件添加到您的 Visual Studio/Visual Web Developer Express 工具箱。

## <a name="downloading-the-ajax-control-toolkit"></a>下载 AJAX 控件工具包

[AJAX 控件工具包](http://devexpress.com/act)是由 ASP.NET 社区和 ASP.NET 团队成员开发的开源项目。

[![下载 AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**图 01**：下载 AJAX 控件工具包（[单击以查看完全大小的映像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)）

下载文件后，需要取消阻止此文件。 右键单击该文件，选择 "属性"，然后单击 "**取消阻止**" 按钮（参见图2）。

[![取消阻止 AJAX 控件工具包 ZIP 文件](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**图 02**：取消阻止 AJAX 控件工具包 ZIP 文件（[单击以查看完全大小的映像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)）

取消阻止该文件后，可以将该文件解压缩：右键单击该文件，然后选择 "**全部提取**" 菜单选项。 现在，我们已准备好将工具包添加到 Visual Studio/Visual Web Developer 工具箱。

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>将 AJAX 控件工具包添加到工具箱

使用 AJAX 控件工具包的最简单方法是将工具包添加到 Visual Studio/Visual Web Developer 工具箱（请参阅图3）。 这样一来，只需将工具包控件拖动到页面上即可。

[工具箱中显示 ![AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**图 03**：在工具箱中显示 AJAX 控件工具包（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)）

首先，需要将 AJAX 控件工具包选项卡添加到 "工具箱"。 请执行下列步骤。

1. 通过选择 "菜单" "文件" "新建网站" 来创建新的 ASP.NET 网站。 在 "解决方案资源管理器" 窗口中双击 "default.aspx"，以在编辑器中打开文件。
2. 右键单击 "常规" 选项卡下的 "工具箱"，然后选择 "添加" 菜单选项**卡**（请参阅图4）。
3. 输入名为 AJAX 控件工具包的新选项卡。

[添加新选项卡 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**图 04**：添加新选项卡（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)）

接下来，需要将 AJAX 控件工具包控件添加到新选项卡。请执行以下步骤：

- 右键单击 "AJAX 控件工具包" 选项卡，然后选择菜单选项 "**选择项" （参见图5）** 。
- 浏览到您解压缩 AJAX 控件工具包的位置，并选择 AjaxControlToolkit 程序集。

[![选择要添加到工具箱中的项](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**图 05**：选择要添加到 "工具箱" 的项（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)）

完成这些步骤后，所有工具包控件都将显示在工具箱中。

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>升级到新版本的工具包

如果你使用的是较旧版本的工具包，而现在需要迁移到更高版本，则建议执行以下步骤：

- 二进制文件-从网站 Bin 文件夹中删除旧版本的 AjaxControlToolkit 程序集。
- 工具箱项-删除 "AJAX 控件工具包" 选项卡，然后执行上述步骤，用 AjaxControlToolkit 程序集的新版本重新创建该选项卡。

> [!div class="step-by-step"]
> [上一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一页](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)
