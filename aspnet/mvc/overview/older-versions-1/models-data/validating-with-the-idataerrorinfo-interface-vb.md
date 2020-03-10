---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
title: 用 IDataErrorInfo 接口进行验证（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何通过在模型类中实现 IDataErrorInfo 接口来显示自定义验证错误消息。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3a8a9d9f-82dd-4959-b7c6-960e9ce95df1
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 8ff3adc5db8114dcca2c66d937e1706f0bac0d30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436298"
---
# <a name="validating-with-the-idataerrorinfo-interface-vb"></a>使用 IDataErrorInfo 接口进行验证 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 演示了如何通过在模型类中实现 IDataErrorInfo 接口来显示自定义验证错误消息。

本教程的目的是介绍一种在 ASP.NET MVC 应用程序中执行验证的方法。 了解如何在不为所需的窗体域提供值的情况下，防止某人提交 HTML 表单。 在本教程中，将了解如何使用 IErrorDataInfo 接口执行验证。

## <a name="assumptions"></a>假设

在本教程中，我将使用 MoviesDB 数据库和电影数据库表。 此表包含以下列：

<a id="0.6_table01"></a>

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(100) | False |
| 导演 | Nvarchar(100) | False |
| DateReleased | DateTime | False |

在本教程中，我将使用 Microsoft 实体框架生成数据库模型类。 实体框架生成的 Movie 类如图1所示。

[!["电影" 实体](validating-with-the-idataerrorinfo-interface-vb/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image1.png)

**图 01**：电影实体（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image2.png)）

> [!NOTE] 
> 
> 若要了解有关使用实体框架生成数据库模型类的详细信息，请参阅我的教程使用实体框架创建模型类。

## <a name="the-controller-class"></a>控制器类

我们使用 Home 控制器来列出电影并创建新电影。 此类的代码包含在列表1中。

**列表 1-Controllers\HomeController.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample1.vb)]

列表1中的 Home 控制器类包含两个 Create （）操作。 第一个操作显示用于创建新电影的 HTML 窗体。 第二个 Create （）操作执行将新电影插入到数据库中的实际操作。 当第一个 Create （）操作显示的窗体提交给服务器时，将调用第二个 Create （）操作。

请注意，第二个 Create （）操作包含以下代码行：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample2.vb)]

当存在验证错误时，IsValid 属性返回 false。 在这种情况下，将重新显示包含用于创建电影的 HTML 窗体的 "创建" 视图。

## <a name="creating-a-partial-class"></a>创建分部类

Movie 类由实体框架生成。 如果在 "解决方案资源管理器" 窗口中展开 "MoviesDBModel" 文件，然后在代码编辑器中打开 MoviesDBModel 文件（参见图2），则可以查看 Movie 类的代码。

[!["电影" 实体的代码](validating-with-the-idataerrorinfo-interface-vb/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image3.png)

**图 02**：电影实体的代码（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image4.png)）

Movie 类是一个分部类。 这意味着，我们可以添加具有相同名称的另一个分部类，以扩展 Movie 类的功能。 我们会将验证逻辑添加到新的分部类。

将清单2中的类添加到 "模型" 文件夹。

**列表 2-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample3.vb)]

请注意，"清单 2" 中的类包括*partial*修饰符。 你添加到此类的任何方法或属性都将成为实体框架生成的 Movie 类的一部分。

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>添加 OnChanging 和 OnChanged 分部方法

当实体框架生成实体类时，实体框架会自动向类中添加分部方法。 实体框架生成与类的每个属性相对应的 OnChanging 和 OnChanged 分部方法。

对于 Movie 类，实体框架会创建以下方法：

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

在相应属性更改之前，先调用 OnChanging 方法。 更改属性后，将立即调用 OnChanged 方法。

您可以利用这些分部方法将验证逻辑添加到 Movie 类中。 清单3中的 update Movie 类验证是否为 Title 和 Director 属性分配了非空值。

> [!NOTE] 
> 
> 分部方法是在类中定义的不需要实现的方法。 如果未实现分部方法，则编译器会删除方法签名和对方法的所有调用，因此没有与分部方法关联的运行时开销。 在 Visual Studio Code 编辑器中，可以通过键入关键字*partial*后面跟一个空格来添加分部方法，以便查看要实现的分区列表。

**列表 3-Models\Movie.vb**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample4.vb)]

例如，如果尝试将空字符串分配给 Title 属性，则会将错误消息分配给名为 \_错误的字典。

此时，将空字符串分配给 Title 属性并将错误添加到 "私有 \_错误" 字段时，实际上不会发生任何操作。 我们需要实现 IDataErrorInfo 接口，将这些验证错误公开给 ASP.NET MVC 框架。

## <a name="implementing-the-idataerrorinfo-interface"></a>实现 IDataErrorInfo 接口

自第一版以来，IDataErrorInfo 接口已是 .NET framework 的一部分。 此接口是一个非常简单的接口：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample5.vb)]

如果类实现 IDataErrorInfo 接口，则 ASP.NET MVC 框架将在创建类的实例时使用此接口。 例如，"主控制器创建（）" 操作接受 Movie 类的实例：

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample6.vb)]

ASP.NET MVC 框架使用模型绑定器（DefaultModelBinder）创建传递到 Create （）操作的电影的实例。 模型联编程序负责通过将 HTML 窗体字段绑定到 Movie 对象的实例来创建 Movie 对象的实例。

DefaultModelBinder 检测类是否实现 IDataErrorInfo 接口。 如果类实现此接口，则模型绑定器将为类的每个属性调用 IDataErrorInfo。 如果索引器返回错误消息，则模型联编程序会自动将此错误消息添加到模型状态。

DefaultModelBinder 还会检查 IDataErrorInfo 属性。 此属性用于表示与类关联的非属性特定的验证错误。 例如，你可能希望强制实施依赖于 Movie 类的多个属性的值的验证规则。 在这种情况下，您将从 Error 属性返回一个验证错误。

列表4中更新后的 Movie 类实现 IDataErrorInfo 接口。

**列表 4-Models\Movie.vb （实现 IDataErrorInfo）**

[!code-vb[Main](validating-with-the-idataerrorinfo-interface-vb/samples/sample7.vb)]

在列表4中，索引器属性检查 \_错误集合，以查看它是否包含与传递给索引器的属性名称对应的键。 如果没有与属性关联的验证错误，则返回空字符串。

无需以任何方式修改 Home 控制器即可使用修改后的 Movie 类。 图3中所示的页说明了在没有为标题或主管窗体字段输入值时将发生的情况。

[![自动创建操作方法](validating-with-the-idataerrorinfo-interface-vb/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-vb/_static/image5.png)

**图 03**：缺少值的窗体（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-vb/_static/image6.png)）

请注意，DateReleased 值会自动进行验证。 由于 DateReleased 属性不接受 NULL 值，因此当 DefaultModelBinder 没有值时，它会自动为此属性生成一个验证错误。 如果要修改 DateReleased 属性的错误消息，则需要创建自定义模型绑定器。

## <a name="summary"></a>摘要

在本教程中，您学习了如何使用 IDataErrorInfo 接口生成验证错误消息。 首先，我们创建了一个部分电影类，该类用于扩展由实体框架生成的部分电影类的功能。 接下来，我们向 Movie 类 OnTitleChanging （）和 OnDirectorChanging （）分部方法添加了验证逻辑。 最后，我们实现了 IDataErrorInfo 接口，以便将这些验证消息公开给 ASP.NET MVC 框架。

> [!div class="step-by-step"]
> [上一页](performing-simple-validation-vb.md)
> [下一页](validating-with-a-service-layer-vb.md)
