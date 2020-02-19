---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456538"
---
# <a name="adding-a-model"></a>添加模型

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

在本部分中，你将添加一些用于在数据库中管理电影的类。 这些类将作为 ASP.NET MVC 应用&quot; 一部分的 &quot;模型。

您将使用一种称为[实体框架](https://docs.microsoft.com/ef/)的 .NET Framework 数据访问技术来定义和使用这些模型类。 实体框架（通常称为 EF）支持名为*Code First*的开发模式。 Code First 允许通过编写简单的类来创建模型对象。 （这些类也称为 POCO 类，来自 &quot;纯传统 CLR 对象。&quot;）然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。 如果需要首先创建数据库，仍可以遵循本教程来了解 MVC 和 EF 应用程序开发。 然后，你可以遵循 Tom Fizmakens [ASP.NET 基架](xref:visual-studio/overview/2013/aspnet-scaffolding-overview)教程，其中介绍了数据库优先方法。

## <a name="adding-model-classes"></a>添加模型类

在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。

![](adding-a-model/_static/image1.png)

输入 &quot;Movie&quot;的*类*名。

将以下五个属性添加到 `Movie` 类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用 `Movie` 类来表示数据库中的影片。 `Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。

注意：若要使用 System.web 和相关类，需要安装[实体框架 NuGet 包](https://www.nuget.org/packages/EntityFramework/)。） 请单击链接获取进一步的说明。

在同一文件中，添加以下 `MovieDBContext` 类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。 `MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。

为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `using` 语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

您可以通过手动添加 using 语句来实现此目的，也可以将鼠标悬停在红色波浪线上，单击 `Show potential fixes` 并单击 `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

注意：已删除多个未使用的 `using` 语句。 Visual Studio 会将未使用的依赖项显示为灰色。 您可以通过将鼠标悬停在灰色依赖项上来删除未使用的依赖项，单击 `Show potential fixes` 并单击 "**删除未使用的 using**

![](adding-a-model/_static/image3.png)

最后，我们添加了一个模型（MVC 中的 M）。 在下一部分中，你将使用数据库连接字符串。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](creating-a-connection-string.md)
