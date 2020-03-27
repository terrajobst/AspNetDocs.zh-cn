---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 在模型绑定和 web 窗体中对数据进行排序、分页和筛选 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441062"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>通过模型绑定和 web 窗体对数据进行排序、分页和筛选

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 本教程介绍如何通过模型绑定来添加数据的排序、分页和筛选。
> 
> 本教程基于在序列的第[一部分](retrieving-data.md)中创建的项目构建。
> 
> 可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，你将：

1. 启用数据的排序和分页
2. 启用基于用户所选内容的数据筛选

## <a name="add-sorting"></a>添加排序

在 GridView 中启用排序非常简单。 在 Student 文件中，只需在 GridView 中将**AllowSorting**设置为**true**即可。 不需要为每个列设置**SortExpression**值，因为 DataField 会自动使用。 GridView 修改查询以包括按选定值对数据进行排序。 以下突出显示的代码显示了为启用排序需要进行的添加。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

运行 web 应用程序，并按不同列中的值测试学生记录排序。

![对学生进行排序](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>添加分页

启用分页也非常简单。 在 GridView 中，将**AllowPaging**属性设置为**true** ，并将**PageSize**属性设置为要在每页上显示的记录数。 在本教程中，可以将其设置为4。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

运行 web 应用程序，请注意，现在将记录分成多个页面，而在单个页面上只显示4条记录。

![添加分页](sorting-paging-and-filtering-data/_static/image4.png)

延迟的查询执行会提高应用程序的效率。 GridView 会修改查询以仅检索当前页的记录，而不是检索整个数据集。

## <a name="filter-records-by-user-selection"></a>按用户选择筛选记录

模型绑定添加了多个属性，使您可以指定如何在模型绑定方法中设置参数的值。 这些属性位于**ModelBinding**命名空间中。 这些权限包括：

- 控件
- Cookie
- 窗体
- 配置文件
- QueryString
- RouteData
- 会话
- UserProfile
- ViewState

在本教程中，您将使用控件的值来筛选在 GridView 中显示的记录。 将**控件**特性添加到之前创建的查询方法。 在[后面](using-query-string-values-to-retrieve-data.md)的教程中，你要将**QueryString**特性应用于参数以指定参数值来自查询字符串值。

首先，在 ValidationSummary 上方添加一个下拉列表，用于筛选显示的学生。

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

在代码隐藏文件中，修改 select 方法以接收来自控件的值，并将参数的名称设置为提供该值的控件的名称。

必须为**ModelBinding**命名空间添加**using**语句以解析控件属性。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

下面的代码演示了选择方法重新工作，以根据下拉列表的值筛选返回的数据。 在参数之前添加控件特性会将此参数的值指定为具有相同名称的控件。

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

运行 web 应用程序并从下拉列表中选择不同的值，以筛选学生列表。

![筛选学生](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>结论

在本教程中，将对数据进行排序和分页。 还启用了按控件的值筛选数据。

在下一[教程](integrating-jquery-ui.md)中，你将通过将 JQuery UI 小组件集成到动态数据模板来增强 UI。

> [!div class="step-by-step"]
> [上一页](updating-deleting-and-creating-data.md)
> [下一页](integrating-jquery-ui.md)
