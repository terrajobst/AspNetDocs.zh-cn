---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 通过模型绑定和 web 窗体更新、删除和创建数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474134"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>通过模型绑定和 web 窗体更新、删除和创建数据

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 本教程介绍如何通过模型绑定创建、更新和删除数据。 你将设置以下属性：
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> 这些属性将接收处理相应操作的方法的名称。 在该方法中，将提供用于与数据进行交互的逻辑。
> 
> 本教程基于在序列的第[一部分](retrieving-data.md)中创建的项目构建。
> 
> 可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。

## <a name="what-youll-build"></a>要生成的内容

在本教程中，你将：

1. 添加动态数据模板
2. 启用通过模型绑定方法更新和删除数据
3. 应用数据验证规则-启用在数据库中创建新记录

## <a name="add-dynamic-data-templates"></a>添加动态数据模板

为了提供最佳用户体验并最大程度减少代码重复，你将使用动态数据模板。 你可以通过安装 NuGet 包轻松将预先生成的动态数据模板集成到现有站点。

从 "**管理 NuGet 包**" 中安装**DynamicDataTemplatesCS**。

![动态数据模板](updating-deleting-and-creating-data/_static/image1.png)

请注意，你的项目现在包括一个名为**DynamicData**的文件夹。 在该文件夹中，你将找到自动应用于 web 窗体中的动态控件的模板。

![动态数据文件夹](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>启用更新和删除

使用户能够更新和删除数据库中的记录与检索数据的过程非常相似。 在 " **UpdateMethod** " 和 " **DeleteMethod** " 属性中，指定执行这些操作的方法的名称。 使用 GridView 控件，还可以指定 "编辑" 和 "删除" 按钮的自动生成。 以下突出显示的代码显示了向 GridView 代码添加的内容。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

在代码隐藏文件中，添加用于**system.web. Entity**的 using 语句。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

然后，添加以下更新和删除方法。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel**方法将匹配的数据绑定值从 web 窗体应用到数据项。 根据 id 参数的值检索数据项。

## <a name="enforce-validation-requirements"></a>强制执行验证要求

在更新数据时，将自动强制应用到 Student 类中的 "名字"、"姓氏" 和 "年" 属性的验证特性。 DynamicField 控件基于验证特性添加客户端和服务器验证程序。 FirstName 和 LastName 属性都是必需的。 FirstName 长度不能超过20个字符，并且 LastName 长度不能超过40个字符。 Year 必须是 AcademicYear 枚举的有效值。

如果用户违反其中一项验证要求，则不会继续更新。 若要查看错误消息，请将 ValidationSummary 控件添加到 GridView 之上。 若要显示模型绑定中的验证错误，请将**ShowModelStateErrors**属性设置为**true**。 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

运行 web 应用程序，并更新和删除任何记录。

![更新数据](updating-deleting-and-creating-data/_static/image3.png)

请注意，在编辑模式下，Year 属性的值将自动呈现为下拉列表。 Year 属性是一个枚举值，枚举值的动态数据模板指定下拉列表以进行编辑。 可以通过在**DynamicData**/**FieldTemplates**文件夹中打开**枚举\_编辑 .ascx**文件来找到该模板。

如果提供了有效值，则更新成功完成。 如果违反其中一项验证要求，则更新不会继续，并且会在网格上方显示错误消息。

![错误消息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>添加新记录

GridView 控件不包含**InsertMethod**属性，因此不能用于添加具有模型绑定的新记录。 可以在**FormView**、 **DetailsView**或**ListView**控件中找到 InsertMethod 属性。 在本教程中，您将使用 FormView 控件来添加新记录。

首先，将一个链接添加到要创建的新页面，以便添加新记录。 在 ValidationSummary 上，添加：

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

新链接将出现在 "学生" 页的内容顶部。

![新建链接](updating-deleting-and-creating-data/_static/image5.png)

然后，使用母版页添加新的 web 窗体，并将其命名为**AddStudent**。 选择 "站点" 作为母版页。

您将使用**DynamicEntity**控件呈现添加新学生的字段。 DynamicEntity 控件呈现在 ItemType 属性中指定的类中可编辑的属性。 StudentID 属性标记有 **[ScaffoldColumn （false）]** 属性，因此不会呈现。 在 AddStudent 页的 MainContent 占位符中，添加以下代码。

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

在代码隐藏文件（AddStudent.aspx.cs）中，为**ContosoUniversityModelBinding**命名空间添加**using**语句。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

然后，添加以下方法，以指定如何为 "取消" 按钮插入新记录和事件处理程序。

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

保存所有更改。

运行 web 应用程序并创建新的学生。

![添加新的学生](updating-deleting-and-creating-data/_static/image6.png)

单击 "**插入**"，可以看到已创建新的学生。

![显示新的学生](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>结论

在本教程中，你已启用更新、删除和创建数据。 在与数据进行交互时，已确保应用验证规则。

在本系列的下一个[教程](sorting-paging-and-filtering-data.md)中，您将启用排序、分页和筛选数据。

> [!div class="step-by-step"]
> [上一页](retrieving-data.md)
> [下一页](sorting-paging-and-filtering-data.md)
