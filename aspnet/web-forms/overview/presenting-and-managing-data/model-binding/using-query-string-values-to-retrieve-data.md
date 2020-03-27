---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 使用查询字符串值通过模型绑定和 web 窗体筛选数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519080"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>使用查询字符串值通过模型绑定和 web 窗体筛选数据

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 本教程介绍如何在查询字符串中传递值，并使用该值通过模型绑定来检索数据。
> 
> 本教程基于在序列的[前面](retrieving-data.md)部分中创建的项目构建。
> 
> 可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，你将：

1. 添加新页面以显示学生的已注册课程
2. 根据查询字符串中的值检索所选学生的已注册课程
3. 使用从网格视图到新页面的查询字符串值添加超链接

本教程中的步骤与您在前面的[教程](sorting-paging-and-filtering-data.md)中执行的步骤非常相似，可以根据下拉列表中的用户选择筛选显示的学生。 在本教程中，您在 select 方法中使用了**control**特性来指定参数值来自控件。 在本教程中，您将使用 select 方法中的**QueryString**特性来指定参数值来自查询字符串。

## <a name="add-new-page-for-displaying-a-students-courses"></a>添加新页面以显示学生的课程

添加新的 web 窗体，该窗体使用网站母版页，并为页面**课程**命名。

在 " **default.aspx** " 文件中，添加 "网格" 视图以显示所选学生的课程。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>定义 select 方法

在**Courses.aspx.cs**中，您将用在网格视图的**SelectMethod**属性中指定的名称添加 select 方法。 在该方法中，你将定义用于检索学生课程的查询，并指定参数来自与参数名称相同的查询字符串值。

首先，必须添加以下**using**语句。

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

然后，将以下代码添加到 Courses.aspx.cs：

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString 属性表示将名为 StudentID 的查询字符串值自动分配给此方法中的参数。

## <a name="add-hyperlink-with-query-string-value"></a>添加带查询字符串值的超链接

在 "student" 的 "网格" 视图中，您将添加链接到您的新课程页面的超链接字段。 超链接将包含一个包含学生 id 的查询字符串值。

在 "student" 中，将以下字段添加到 "网格" 视图中紧靠总信用额度字段下方的列。

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

运行应用程序，并注意 "网格" 视图现在包含 "课程" 链接。

![添加超链接](using-query-string-values-to-retrieve-data/_static/image1.png)

单击其中一个链接时，将看到该学生注册的课程。

![显示课程](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>结论

在本教程中，你添加了一个带有查询字符串值的链接。 你将查询字符串值用于 select 方法中的参数值。

在下一[教程](adding-business-logic-layer.md)中，你将代码从代码隐藏文件移动到业务逻辑层和数据访问层。

> [!div class="step-by-step"]
> [上一页](integrating-jquery-ui.md)
> [下一页](adding-business-logic-layer.md)
