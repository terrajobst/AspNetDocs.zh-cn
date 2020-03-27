---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 向使用模型绑定和 web 窗体的项目添加业务逻辑层 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515426"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>向使用模型绑定和 web 窗体的项目添加业务逻辑层

通过[Tom FitzMacken](https://github.com/tfitzmac)

> 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。 此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。
> 
> 本教程演示如何通过业务逻辑层使用模型绑定。 你将设置 OnCallingDataMethods 成员，以指定使用当前页以外的对象来调用数据方法。
> 
> 本教程基于在序列的[前面](retrieving-data.md)部分中创建的项目构建。
> 
> 可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。 可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。 它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。

## <a name="what-youll-build"></a>要生成的内容

通过模型绑定，可以将数据交互代码放入网页的代码隐藏文件中，也可以放在单独的业务逻辑类中。 前面的教程演示了如何使用代码隐藏文件来实现数据交互代码。 此方法适用于小型站点，但在维护大型站点时，这可能会导致代码重复并更难。 由于没有抽象层，因此也可能很难以编程方式测试驻留在代码隐藏文件中的代码。

为了集中数据交互代码，你可以创建一个包含用于与数据进行交互的所有逻辑的业务逻辑层。 然后从网页调用业务逻辑层。 本教程介绍如何将您在前面的教程中编写的所有代码移到业务逻辑层，然后使用这些页面中的代码。

在本教程中，你将：

1. 将代码从代码隐藏文件移动到业务逻辑层
2. 更改数据绑定控件以调用业务逻辑层中的方法

## <a name="create-business-logic-layer"></a>创建业务逻辑层

现在，您将创建从网页中调用的类。 此类中的方法与您在前面的教程中使用的方法类似，并包括值提供程序特性。

首先，添加一个名为**BLL**的新文件夹。

![添加文件夹](adding-business-logic-layer/_static/image1.png)

在 BLL 文件夹中，创建一个名为**SchoolBL.cs**的新类。 它将包含最初驻留在代码隐藏文件中的所有数据操作。 方法与代码隐藏文件中的方法几乎相同，但会包含一些更改。

需要注意的最重要的更改是，您不再从**Page**类的实例中执行该代码。 Page 类包含**TryUpdateModel**方法和**ModelState**属性。 将此代码移到业务逻辑层后，将不再具有 Page 类的实例来调用这些成员。 若要解决此问题，必须将**ModelMethodContext**参数添加到访问 TryUpdateModel 或 ModelState 的任何方法。 使用此 ModelMethodContext 参数可以调用 TryUpdateModel 或检索 ModelState。 无需更改网页中的任何内容即可为此新参数提供帐户。

将 SchoolBL.cs 中的代码替换为以下代码。

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>修改现有页面以从业务逻辑层检索数据

最后，通过将代码隐藏文件中的查询转换为使用业务逻辑层，将 pages. .aspx、AddStudent 和 default.aspx 页转换为。

在学生、AddStudent 和课程的代码隐藏文件中，删除或注释掉以下查询方法：

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_Deleteitem.php
- addStudentForm\_InsertItem
- coursesGrid\_GetData

你现在应在代码隐藏文件中没有代码，这与数据操作有关。

使用**OnCallingDataMethods**事件处理程序可以指定要用于数据方法的对象。 在 "student" 中，为该事件处理程序添加一个值，然后将数据方法的名称更改为业务逻辑类中的方法的名称。

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

在 "student" 的代码隐藏文件中，为 CallingDataMethods 事件定义事件处理程序。 在此事件处理程序中，您将指定数据操作的业务逻辑类。

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

在 AddStudent 中，进行类似的更改。

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

在 default.aspx 中，进行类似的更改。

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

运行应用程序，并注意所有页面的功能都与以前相同。 验证逻辑也能正常工作。

## <a name="conclusion"></a>结论

在本教程中，您将重新构建应用程序以使用数据访问层和业务逻辑层。 您指定数据控件使用的对象不是数据操作的当前页。

> [!div class="step-by-step"]
> [上一篇](using-query-string-values-to-retrieve-data.md)
