---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第2部分：数据访问层 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第2部分介绍如何添加数据访问层。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462650"
---
# <a name="part-2-data-access-layer"></a>第2部分：数据访问层

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第2部分介绍如何添加数据访问层。

## <a id="_Toc260221668"></a>添加数据访问层

电子商务应用程序将依赖于两个数据库。

对于客户信息，我们将使用标准的 ASP.NET 成员资格数据库。 对于购物车和产品目录，我们将按如下所示实现 SQL Express 数据库。

![](tailspin-spyworks-part-2/_static/image1.jpg)

在应用程序的应用程序\_Data 文件夹中创建数据库（.mdf）后，我们可以继续使用 .NET 实体框架创建数据访问层。

我们将创建一个名为 "Data\_Access" 的文件夹，并右键单击该文件夹并选择 "添加新项"。

在 "已安装的模板" 项中，选择 "ADO.NET 实体数据模型" 输入 EDM\_Commerce 作为名称，然后单击 "添加" 按钮。

![](tailspin-spyworks-part-2/_static/image2.jpg)

选择 "从数据库生成"。

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

保存并生成。

现在，我们已准备好添加第一个功能–产品类别菜单。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-1.md)
> [下一页](tailspin-spyworks-part-3.md)
