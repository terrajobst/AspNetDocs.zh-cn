---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 通过数据批注验证程序进行验证（VB） |Microsoft Docs
author: microsoft
description: 利用数据批注模型绑定器在 ASP.NET MVC 应用程序中执行验证。 了解如何使用不同类型的验证程序 。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435938"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a>使用数据注释验证程序进行验证 (VB)

由[Microsoft](https://github.com/microsoft)

> 利用数据批注模型绑定器在 ASP.NET MVC 应用程序中执行验证。 了解如何使用不同类型的验证程序属性并在 Microsoft 实体框架中处理它们。

在本教程中，将了解如何使用数据批注验证程序在 ASP.NET MVC 应用程序中执行验证。 使用数据批注验证程序的优点在于，只需将一个或多个属性（如 Required 或 StringLength 属性）添加到类属性即可执行验证。

在可以使用数据批注验证程序之前，必须下载数据批注模型联编程序。 通过单击[此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)，可以从 CodePlex 网站下载数据批注模型绑定器示例。

必须了解的是，数据批注模型联编程序不是 Microsoft ASP.NET MVC 框架的官方部分。 尽管数据批注模型联编程序由 Microsoft ASP.NET MVC 团队创建，但对于本教程中介绍和使用的数据批注模型联编程序，Microsoft 不提供正式的产品支持。

## <a name="using-the-data-annotation-model-binder"></a>使用数据批注模型联编程序

若要在 ASP.NET MVC 应用程序中使用数据批注模型联编程序，首先需要添加对 DataAnnotations 程序集和 System.componentmodel. DataAnnotations 程序集的引用的引用。 选择菜单选项 "**项目"、"添加引用"** 。 接下来，单击 "**浏览**" 选项卡，然后浏览到数据批注模型绑定器示例的下载位置（和解压 **）。**

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

**图 1**：添加对数据批注模型联编程序的引用（[单击查看完全大小的图像](validation-with-the-data-annotation-validators-vb/_static/image3.png)）

同时选择 DataAnnotations 程序集和 DataAnnotations 程序集，然后单击 **"确定" （"确定"** 按钮）。

不能将 .NET Framework Service Pack 1 随附的 DataAnnotations 程序集用于数据批注模型联编程序。 必须使用数据批注模型绑定器示例下载中包含的 System.componentmodel. DataAnnotations 程序集版本。

最后，需要在 global.asax 文件中注册 DataAnnotations 模型联编程序。 将以下代码行添加到应用程序\_Start （）事件处理程序，使应用程序\_Start （）方法如下所示：

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

下面这行代码会将 DataAnnotationsModelBinder 注册为整个 ASP.NET MVC 应用程序的默认模型联编程序。

## <a name="using-the-data-annotation-validator-attributes"></a>使用数据批注验证程序特性

使用数据批注模型绑定器时，将使用验证程序特性来执行验证。 System.componentmodel. DataAnnotations 命名空间包括以下验证程序特性：

- 范围–用于验证属性的值是否在指定的值范围之间。
- RegularExpression –用于验证属性的值是否与指定的正则表达式模式匹配。
- 必需–使你能够根据需要标记属性。
- StringLength-用于指定字符串属性的最大长度。
- 验证–所有验证程序特性的基类。

> [!NOTE] 
> 
> 如果任何标准验证程序都不满足您的验证需求，则您始终可以通过从基本验证属性继承新的验证程序属性，来创建自定义验证程序特性。

**列表 1**中的 Product 类演示了如何使用这些验证程序特性。 "名称"、"说明" 和 "单价" 属性标记为 "必需"。 Name 属性的字符串长度必须小于10个字符。 最后，"单价" 属性必须与表示货币金额的正则表达式模式匹配。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

**列表 1**： Models\Product.vb

Product 类阐释了如何使用另一个特性： DisplayName 特性。 当属性显示在错误消息中时，DisplayName 特性使你可以修改属性的名称。 您可以显示错误消息 "需要此价格字段"，而不是显示错误消息 "需要单价字段"。

> [!NOTE] 
> 
> 如果要完全自定义验证程序所显示的错误消息，可以将自定义错误消息分配给验证程序的 ErrorMessage 属性，如下所示： `<Required(ErrorMessage:="This field needs a value!")>`

您可以在列表**1**中使用 Product 类，并在**列表 2**中使用 Create （）控制器操作。 当模型状态包含任何错误时，此控制器操作会重新显示 "创建" 视图。

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

**列表 2**： Controllers\ProductController.vb

最后，您可以通过右键单击 Create （）操作并选择菜单选项 "**添加视图**"，在**列表 3**中创建视图。 使用 Product 类作为模型类创建强类型视图。 从 "查看内容" 下拉列表中选择 "**创建**" （参见**图 2**）。

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

**图 2**：添加 "创建" 视图

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

**列表 3**： Views\Product\Create.aspx

> [!NOTE] 
> 
> 从 "**添加视图**" 菜单选项生成的创建窗体中删除 Id 字段。 由于 Id 字段对应于标识列，因此不希望允许用户为此字段输入值。

如果您提交用于创建产品的表单，并且没有为必填字段输入值，则将显示**图 3**中的验证错误消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

**图 3**：缺少必填字段

如果输入的货币金额无效，则会显示**图 4**中的错误消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

**图 4**：货币金额无效

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>将数据批注验证程序用于实体框架

如果使用 Microsoft 实体框架生成数据模型类，则不能将验证程序特性直接应用于类。 由于 Entity Framework Designer 会生成模型类，因此，在设计器中进行任何更改时，对模型类所做的任何更改都将被覆盖。

如果要将验证程序与实体框架生成的类一起使用，则需要创建元数据类。 将验证程序应用于元数据类，而不是将验证程序应用于实际的类。

例如，假设您已使用实体框架创建了一个 Movie 类（见**图 5**）。 而且，假设要使影片标题和控制器属性为必填属性。 在这种情况下，可以在**列表 4**中创建分部类和元数据类。

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

**图 5**：由实体框架生成的 Movie 类

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

**列表 4**： Models\Movie.vb

**列表 4**中的文件包含两个名为 "Movie" 和 "MovieMetaData" 的类。 Movie 类是一个分部类。 它对应于 DataModel 文件中包含的实体框架生成的分部类。

目前，.NET framework 不支持部分属性。 因此，无法将验证程序特性应用于 DataModel 文件中定义的 Movie 类的属性，方法是将验证程序特性应用到在**列表 4**中定义的电影类的属性。

请注意，Movie 分部类使用指向 MovieMetaData 类的 MetadataType 特性进行修饰。 MovieMetaData 类包含 Movie 类的属性的代理属性。

验证程序属性应用于 MovieMetaData 类的属性。 Title、Director 和 DateReleased 属性都标记为必需属性。 必须为 Director 属性分配一个包含少于5个字符的字符串。 最后，将 DisplayName 特性应用到 DateReleased 属性，以显示一条错误消息，如 "所需的日期字段为必填字段"。 而不是 "DateReleased" 字段是必需的。

> [!NOTE] 
> 
> 请注意，MovieMetaData 类中的代理属性不需要与 Movie 类中的相应属性表示相同的类型。 例如，Director 属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。

**图 6**中的页说明了为电影属性输入无效值时返回的错误消息。

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

**图 6**：在实体框架中使用验证器（[单击查看完全大小的图像](validation-with-the-data-annotation-validators-vb/_static/image14.png)）

## <a name="summary"></a>摘要

在本教程中，已学习如何利用数据批注模型联编程序在 ASP.NET MVC 应用程序中执行验证。 已了解如何使用不同类型的验证程序属性，如 Required 和 StringLength 属性。 还了解了如何在使用 Microsoft 实体框架时使用这些属性。

> [!div class="step-by-step"]
> [上一页](validating-with-a-service-layer-vb.md)
