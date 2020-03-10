---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
title: 添加模型（C#） |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 42355b95-5f1f-413e-8d16-14cdfaaefcd8
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a5f494eaa05bcfcd9d49873db728d71c1fd332c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434894"
---
# <a name="adding-a-model-c"></a>添加模型 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/adding-a-model.md)。

## <a name="adding-a-model"></a>添加模型

在本部分中，你将添加一些用于在数据库中管理电影的类。 这些类将是 ASP.NET MVC 应用程序的 "模型" 部分。

您将使用一种称为实体框架的 .NET Framework 数据访问技术来定义和使用这些模型类。 实体框架（通常称为 EF）支持名为*Code First*的开发模式。 Code First 允许通过编写简单的类来创建模型对象。 （这些类也称为 POCO 类，来自 "纯旧 CLR 对象"）。然后，你可以从类动态创建数据库，这样就可以实现非常干净且快速的开发工作流。

## <a name="adding-model-classes"></a>添加模型类

在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。

![](adding-a-model/_static/image1.png)

将*类*命名为 "Movie"。

[![CreateMovieClass](adding-a-model/_static/image3.png)](adding-a-model/_static/image2.png)

将以下五个属性添加到 `Movie` 类：

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

我们将使用 `Movie` 类来表示数据库中的影片。 `Movie` 对象的每个实例都对应于数据库表中的一行，而 `Movie` 类的每个属性都将映射到该表中的列。

在同一文件中，添加以下 `MovieDBContext` 类：

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 类表示实体框架的电影数据库上下文，用于处理数据库中 `Movie` 类实例的提取、存储和更新。 `MovieDBContext` 从实体框架提供的 `DbContext` 基类派生。 有关 `DbContext` 和 `DbSet`的详细信息，请参阅[实体框架的工作效率改进](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)。

为了能够引用 `DbContext` 和 `DbSet`，需要在文件的顶部添加以下 `using` 语句：

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

完整的*Movie.cs*文件如下所示。

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>创建连接字符串并使用 SQL Server Compact

你创建的 `MovieDBContext` 类将处理连接到数据库的任务，并将 `Movie` 对象映射到数据库记录。 但您可能会问的一个问题是如何指定它将连接到的数据库。 可以通过在应用程序的*web.config 文件中*添加连接信息来实现此目的。

打开应用程序根*web.config*文件。 （而不是*Views*文件夹中的*web.config 文件。* ）下图显示了*web.config*文件;打开以红色*圆圈表示的 web.config 文件*。

![](adding-a-model/_static/image4.png)

将以下连接字符串添加到*web.config 文件中的 `<connectionStrings>`* 元素。

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

下面的示例演示了*web.config 文件的*一部分，并添加了新的连接字符串：

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

这少量的代码和 XML 是您需要编写的所有内容，以表示和将电影数据存储在数据库中。

接下来，您将生成一个新的 `MoviesController` 类，该类可用于显示电影数据并允许用户创建新的电影节目表。

> [!div class="step-by-step"]
> [上一页](adding-a-view.md)
> [下一页](accessing-your-models-data-from-a-controller.md)
