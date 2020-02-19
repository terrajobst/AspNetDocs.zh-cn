---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 向电影模型和表添加新字段（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457428"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a>向电影模型和表添加新字段 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。
> 
> 
> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

在本节中，您将对模型类进行一些更改，并了解如何更新数据库架构以匹配模型更改。

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先向现有 `Movie` 类添加新的 `Rating` 属性。 打开*Movie.cs*文件并添加 `Rating` 属性，如下所示：

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

完整的 `Movie` 类现在如以下代码所示：

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

使用 "**调试**&gt;**生成电影**" 菜单命令重新编译应用程序。

更新 `Model` 类后，还需要更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml*视图模板，以支持新的 `Rating` 属性。

打开 " *\Views\Movies\Index.cshtml* " 文件，然后在 " **Price** " 列之后添加 `<th>Rating</th>` 列标题。 然后，将 `<td>` 列添加到模板末尾附近，以呈现 `@item.Rating` 值。 更新后的*索引 cshtml*视图模板如下所示：

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

接下来，打开 *\Views\Movies\Create.cshtml*文件，并在窗体结尾附近添加以下标记。 这将呈现一个文本框，以便您可以在创建新电影时指定级别。

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>管理模型和数据库架构差异

现在，你已更新了应用程序代码，以支持新的 `Rating` 属性。

现在，运行应用程序并导航到 */Movies* URL。 不过，当你执行此操作时，你将看到以下错误：

![](adding-a-new-field/_static/image1.png)

出现此错误的原因是，应用程序中更新的 `Movie` 模型类现在与现有数据库的 `Movie` 表的架构不同。 （数据库表中没有 `Rating` 列。）

默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。 如果不同步，实体框架将引发错误。 这样就可以在开发时更轻松地跟踪问题，否则在运行时可能仅会发现（隐藏错误）。 同步检查功能导致显示您刚才看到的错误消息。

可以通过两种方法来解决该错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 在测试数据库上进行活动开发时，这种方法非常方便，因为它允许您将模型和数据库架构快速地一起发展。 不过，缺点在于丢失了数据库中的现有数据，因此*不*希望在生产数据库上使用此方法！
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。

对于本教程，我们将使用第一种方法，即在模型发生更改时，实体框架 Code First 自动重新创建数据库。

## <a name="automatically-re-creating-the-database-on-model-changes"></a>在模型更改时自动重新创建数据库

让我们更新应用程序，以便在更改应用程序的模型时，Code First 自动删除并重新创建数据库。

> [!NOTE] 
> 
> **警告**仅当使用的是开发或测试数据库，而*从不*在包含实际数据的生产数据库中时，才应启用此方法来自动删除并重新创建数据库。 在生产服务器上使用它可能会导致数据丢失。

在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后选择 "**类**"。

![](adding-a-new-field/_static/image2.png)

将类命名为 "MovieInitializer"。 更新 `MovieInitializer` 类，使其包含以下代码：

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

`MovieInitializer` 类指定如果模型类发生更改，则应删除模型所使用的数据库，并自动重新创建该数据库。 此代码包括一个 `Seed` 方法，用于指定在创建（或重新创建）时，可自动添加到数据库中的某些默认数据。 这提供了用一些示例数据填充数据库的有效方法，无需在每次进行模型更改时手动填充。

现在，您已定义了 `MovieInitializer` 类，您需要将其连接起来，以便每次应用程序运行时，它会检查模型类是否与数据库中的架构不同。 如果是这样，则可以运行初始值设定项来重新创建数据库以与模型匹配，然后用示例数据填充数据库。

打开位于 `MvcMovies` 项目的根目录的*global.asax*文件：

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

*Global.asax*文件包含定义项目的整个应用程序的类，并且包含在应用程序首次启动时运行的 `Application_Start` 事件处理程序。

让我们将两个 using 语句添加到文件的顶部。 第一个引用实体框架命名空间，第二个引用命名空间，其中 `MovieInitializer` 类所在：

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

然后查找 `Application_Start` 方法，并在方法的开头添加对 `Database.SetInitializer` 的调用，如下所示：

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

刚添加的 `Database.SetInitializer` 语句指示当架构和数据库不匹配时，应自动删除 `MovieDBContext` 实例使用的数据库，然后重新创建该数据库。 正如您所看到的，它还将用 `MovieInitializer` 类中指定的示例数据填充数据库。

关闭*global.asax*文件。

重新运行应用程序并导航到 */Movies* URL。 当应用程序启动时，它会检测到模型结构不再与数据库架构匹配。 它会自动重新创建数据库以与新模型结构匹配，并用示例影片填充数据库：

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

单击 "**新建**" 链接以添加新电影。 请注意，可以添加级别。

[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)

单击“创建”。 现在电影列表中显示了新电影，其中包括评分：

[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)

在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。 还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。

> [!div class="step-by-step"]
> [上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)
