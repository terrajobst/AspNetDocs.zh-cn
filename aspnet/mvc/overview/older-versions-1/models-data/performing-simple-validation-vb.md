---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 执行简单验证（VB） |Microsoft Docs
author: StephenWalther
description: 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 介绍了模型状态和验证 HTML 帮助器 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436664"
---
# <a name="performing-simple-validation-vb"></a>执行简单验证 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 介绍了模型状态和验证 HTML 帮助器。

本教程的目的是介绍如何在 ASP.NET MVC 应用程序中执行验证。 例如，您将了解如何防止某人提交不包含必填字段值的表单。 了解如何使用模型状态和验证 HTML 帮助器。

## <a name="understanding-model-state"></a>了解模型状态

您可以使用模型状态（或者更准确地说，模型状态字典）来表示验证错误。 例如，在将 Product 类添加到数据库之前，列表1中的 Create （）操作将验证 Product 类的属性。

我不建议将验证或数据库逻辑添加到控制器。 控制器仅应包含与应用程序流控制相关的逻辑。 我们将使用一种快捷方式，使其保持简单。

**列表 1-Controllers\ProductController.vb**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

在 "列表 1" 中，将验证 Product 类的 "名称"、"说明" 和 "库存量" 属性。 如果这些属性中的任何一个未能通过验证测试，则会将错误添加到模型状态字典（由控制器类的 ModelState 属性表示）。

如果模型状态中有任何错误，则 ModelState 属性返回 false。 在这种情况下，将重新显示用于创建新产品的 HTML 表单。 否则，如果没有验证错误，则会将新产品添加到数据库中。

## <a name="using-the-validation-helpers"></a>使用验证帮助器

ASP.NET MVC 框架包含两个验证帮助器： ValidationMessage （） helper 和 ValidationSummary （）帮助程序。 可在视图中使用这两个帮助器来显示验证错误消息。

ValidationMessage （）和 ValidationSummary （）帮助器用于 ASP.NET MVC 基架自动生成的 "创建" 和 "编辑" 视图。 按照以下步骤生成创建视图：

1. 右键单击产品控制器中的 "创建" （）操作，然后选择 "**添加视图**" 菜单选项（参见图1）。
2. 在 "**添加视图**" 对话框中，选中标记为 "**创建强类型视图**" 的复选框（参见图2）。
3. 从 "**查看数据类**" 下拉列表中，选择 "产品类"。
4. 从 "**查看内容**" 下拉列表中，选择 "创建"。
5. 单击“添加”按钮。

请确保在添加视图之前生成应用程序。 否则，类的列表将不会显示在 "**查看数据类**" 下拉列表中。

[!["新建项目" 对话框](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**图 01**：添加视图（[单击查看完全尺寸的图像](performing-simple-validation-vb/_static/image2.png)）

[!["新建项目" 对话框](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**图 02**：创建强类型视图（[单击查看完全大小的图像](performing-simple-validation-vb/_static/image4.png)）

完成这些步骤后，将获得列表2中的 "创建" 视图。

**列表 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

在列表2中，html 窗体上立即调用 ValidationSummary （）帮助程序。 此帮助程序用于显示验证错误消息的列表。 ValidationSummary （） helper 在项目符号列表中呈现错误。

在每个 HTML 窗体字段的旁边调用 ValidationMessage （）帮助程序。 此帮助器用于在窗体字段的旁边显示错误消息。 对于列表2，当出错时，ValidationMessage （） helper 会显示星号。

图3中的页说明了在使用缺失字段和无效值提交窗体时，验证帮助程序呈现的错误消息。

[!["新建项目" 对话框](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**图 03**：已提交的创建视图出现问题（[单击以查看完全大小的图像](performing-simple-validation-vb/_static/image6.png)）

请注意，当存在验证错误时，还会修改 HTML 输入字段的外观。 当存在与 Html. TextBox （） helper 呈现的属性关联的验证错误时，Html. TextBox （）帮助器将呈现*类 = "输入验证-错误"* 特性。

有三个用于控制验证错误外观的级联样式表类：

- 输入验证-错误-应用于 Html. TextBox （） helper 呈现&gt; 标记的 &lt;输入。
- 字段验证-错误-应用于 ValidationMessage （）帮助程序呈现&gt; 标记的 &lt;范围。
- 验证-摘要-错误-应用于 ValidationSummary （）帮助程序呈现的 &lt;ul&gt; 标记。

您可以修改这些级联样式表类，并因此通过修改位于 Content 文件夹中的 web.config 文件来修改验证错误的外观。

> [!NOTE] 
> 
> HtmlHelper 类包括只读静态属性，用于检索与验证相关的 CSS 类的名称。 这些静态属性名为 ValidationInputCssClassName、ValidationFieldCssClassName 和 ValidationSummaryCssClassName。

## <a name="prebinding-validation-and-postbinding-validation"></a>Prebinding 验证和 Postbinding 验证

如果您提交用于创建产品的 HTML 表单，并且您为 "价格" 字段输入的值无效，而 "库存" 字段没有值，则您将收到图4中显示的验证消息。 这些验证错误消息来自何处？

[!["新建项目" 对话框](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**图 04**： Prebinding 验证错误（[单击以查看完全大小的图像](performing-simple-validation-vb/_static/image8.png)）

实际上存在两种类型的验证错误消息：在将 HTML 窗体字段绑定到类之前生成的错误消息，以及在窗体字段绑定到类后生成的错误消息。 换句话说，存在 prebinding 验证错误和 postbinding 验证错误。

列表1中的产品控制器公开的 Create （）操作接受 Product 类的实例。 Create 方法的签名如下所示：

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

Create 窗体中的 HTML 窗体字段的值通过称为模型绑定器的内容绑定到 productToCreate 类。 当不能将窗体字段绑定到窗体属性时，默认模型联编程序会自动将错误消息添加到模型状态。

默认模型联编程序不能将字符串 "apple" 绑定到 Product 类的 Price 属性。 不能将字符串分配给 decimal 属性。 因此，模型联编程序将错误添加到模型状态。

默认的模型联编程序也不能将值 Nothing 赋给不接受非空值的属性。 具体而言，模型联编程序不能将值 Nothing 赋给 "库存" 属性。 同样，模型联编程序会提供并将错误消息添加到模型状态。

如果要自定义这些 prebinding 错误消息的外观，则需要为这些消息创建资源字符串。

## <a name="summary"></a>摘要

本教程的目的是介绍 ASP.NET MVC 框架中验证的基本机制。 已学习如何使用模型状态和验证 HTML 帮助器。 还介绍了 prebinding 和 postbinding 验证之间的区别。 在其他教程中，我们将讨论将验证代码移出控制器和模型类的各种策略。

> [!div class="step-by-step"]
> [上一页](displaying-a-table-of-database-data-vb.md)
> [下一页](validating-with-the-idataerrorinfo-interface-vb.md)
