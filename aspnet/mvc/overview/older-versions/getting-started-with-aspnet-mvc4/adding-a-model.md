---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 添加模型 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457799"
---
# <a name="adding-a-model"></a>添加模型

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本部分中，你将添加一些用于在数据库中管理电影的类。 这些类将作为 ASP.NET MVC 应用程序&quot; 一部分的 &quot;模型。

您将使用一种称为[实体框架](https://msdn.microsoft.com/library/bb399572(VS.110).aspx)的 .NET Framework 数据访问技术来定义和使用这些模型类。 实体框架（通常称为 EF）支持名为*Code First*的开发模式。 Code First 允许通过编写简单的类来创建模型对象。 （这些类也称为 POCO 类，来自 &quot;纯传统 CLR 对象。&quot;）然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。

## <a name="adding-model-classes"></a>添加模型类

在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。

![](adding-a-model/_static/image1.png)

输入 &quot;Movie&quot;的*类*名。

将以下五个属性添加到 `Movie` 类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用 `Movie` 类来表示数据库中的影片。 `Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。

在同一文件中，添加以下 `MovieDBContext` 类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。 `MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。

为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `using` 语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完整的*Movie.cs*文件如下所示。 （已删除多个不需要的 using 语句。）

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>创建连接字符串并使用 SQL Server LocalDB

你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。 但您可能会问的一个问题是如何指定它将连接到的数据库。 可以通过在应用程序的*web.config 文件中*添加连接信息来实现此目的。

打开应用程序根*web.config*文件。 （而不是*Views*文件夹中的*web.config 文件。* ）打开以红色列出的*web.config*文件。

![](adding-a-model/_static/image2.png)

将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

这少量的代码和 XML 是您需要编写的所有内容，以表示和将电影数据存储在数据库中。

接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)
