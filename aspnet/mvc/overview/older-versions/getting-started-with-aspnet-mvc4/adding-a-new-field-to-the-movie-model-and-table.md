---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 向电影模型和表添加新字段 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457695"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>向电影模型和表添加新字段

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本节中，您将使用 Entity Framework Code First 迁移将某些更改迁移到模型类，以便将更改应用到数据库。

默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。 如果不同步，实体框架将引发错误。 这样就可以在开发时更轻松地跟踪问题，否则在运行时可能仅会发现（隐藏错误）。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>设置模型更改的 Code First 迁移

如果使用的是 Visual Studio 2012，请双击 "解决方案资源管理器中的"*电影 .mdf* "文件以打开" 数据库工具 "。 Web Visual Studio Express 将显示数据库资源管理器，Visual Studio 2012 将显示 "服务器资源管理器"。 如果使用的是 Visual Studio 2010，请使用 SQL Server 对象资源管理器。

在数据库工具（数据库资源管理器、服务器资源管理器或 SQL Server 对象资源管理器）中，右键单击 `MovieDBContext`，然后选择 "**删除**" 以删除电影数据库。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

向后导航到解决方案资源管理器。 右键单击 "*电影 .mdf* " 文件，然后选择 "**删除**" 以删除电影数据库。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

生成应用程序，以确保没有任何错误。

在“工具”菜单中，单击“NuGet 包管理器”，然后单击“包管理器控制台”。

![添加包手册](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

在 `PM>` 提示符下的 "**包管理器控制台**" 窗口中，输入 "MovieDBContext"。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

"**启用-迁移**" 命令（如上所示）在新的 "*迁移*" 文件夹中创建*Configuration.cs*文件。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio 将打开*Configuration.cs*文件。 将*Configuration.cs*文件中的 `Seed` 方法替换为以下代码：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

右键单击 `Movie` 下面的红色波浪线，然后选择 "**解析**"，然后**使用** **MvcMovie;**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

这样做将添加以下 using 语句：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Code First 迁移将在每次迁移后调用 `Seed` 方法（即，在包管理器控制台中调用**更新数据库**），此方法将更新已插入的行，如果它们尚不存在，则将其插入。

**按 CTRL-SHIFT-B 生成项目。** （如果此时不生成，以下步骤将会失败。）

下一步是创建用于初始迁移的 `DbMigration` 类。 此迁移用于创建新的数据库，这就是在上一步中删除了*movie .mdf*文件的原因。

在 "**包管理器控制台**" 窗口中，输入 "添加迁移初始" 命令以创建初始迁移。 名称 "初始" 是任意名称，用于命名创建的迁移文件。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First 迁移在 "*迁移*" 文件夹（名称为 *{日期戳}\_Initial.cs* ）中创建另一个类文件，并且此类包含用于创建数据库架构的代码。 迁移文件名预先修复了时间戳，以帮助进行排序。 检查 *{日期戳}\_Initial.cs*文件，其中包含为 Movie DB 创建电影表的说明。 当你在下面的说明中更新数据库时，此 *{日期戳}\_Initial.cs*文件将运行，并创建数据库架构。 然后， **Seed**方法将运行以用测试数据填充数据库。

在 "**程序包管理器控制台**" 中，输入命令 "更新数据库" 以创建数据库并运行**Seed**方法。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

如果您收到一条错误消息，指示表已存在并且无法创建，则可能是您在删除数据库之后和执行 `update-database`之前运行了该应用程序。 在这种情况下，请再次删除*电影 .mdf*文件，然后重试 `update-database` 命令。 如果仍出现错误，请删除 "迁移" 文件夹和 "内容"，然后从本页顶部的说明开始（删除 ""，然后继续执行 "启用-*迁移"）* 。

运行应用程序并导航到 */Movies* URL。 将显示种子数据。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先向现有 `Movie` 类添加新的 `Rating` 属性。 打开*Models\Movie.cs*文件并添加 `Rating` 属性，如下所示：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

完整的 `Movie` 类现在如以下代码所示：

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

使用 "**生成**" &gt;生成**电影**"菜单命令或按 CTRL-SHIFT-B 生成应用程序。

现在，你已更新 `Model` 类，还需要更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml*视图模板，才能在浏览器视图中显示新的 `Rating` 属性。

打开 "<em>\Views\Movies\Index.cshtml</em> " 文件，然后在 " <strong>Price</strong> " 列之后添加 `<th>Rating</th>` 列标题。 然后，将 `<td>` 列添加到模板末尾附近，以呈现 `@item.Rating` 值。 更新后的<em>索引 cshtml</em>视图模板如下所示：

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

接下来，打开 *\Views\Movies\Create.cshtml*文件，并在窗体结尾附近添加以下标记。 这将呈现一个文本框，以便您可以在创建新电影时指定级别。

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

现在，你已更新了应用程序代码，以支持新的 `Rating` 属性。

现在，运行应用程序并导航到 */Movies* URL。 不过，当你执行此操作时，你将看到以下错误之一：

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

出现此错误的原因是，应用程序中更新的 `Movie` 模型类现在与现有数据库的 `Movie` 表的架构不同。 （数据库表中没有 `Rating` 列。）

可通过几种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 对测试数据库进行活动开发时，此方法非常方便;它使您可以将模型和数据库架构快速地一起发展。 不过，缺点在于丢失了数据库中的现有数据，因此*不*希望在生产数据库上使用此方法！ 通过使用初始值设定项，可使用测试数据自动设定数据库种子，这通常是开发应用程序的高效方法。 有关实体框架数据库初始值设定项的详细信息，请参阅 Tom Dykstra 的[ASP.NET MVC/实体框架教程](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。
3. 使用 Code First 迁移更新数据库架构。

本教程使用 Code First 迁移。

更新种子方法，使其为新列提供一个值。 打开 Migrations\Configuration.cs 文件，并向每个电影对象添加分级字段。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

生成解决方案，然后打开 "**包管理器控制台**" 窗口，并输入以下命令：

`add-migration AddRatingMig`

`add-migration` 命令通知迁移框架检查当前的电影模型和当前的 movie DB 架构，并创建必要的代码以将数据库迁移到新模型。 AddRatingMig 是任意的，用于对迁移文件进行命名。 为迁移步骤使用有意义的名称会很有帮助。

此命令完成后，Visual Studio 将打开定义新的 `DbMigration` 派生类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

生成解决方案，然后在 "**包管理器控制台**" 窗口中输入 "更新数据库" 命令。

下图显示了 "**包管理器控制台**" 窗口中的输出（预先计算 AddRatingMig 的日期戳将有所不同）。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

重新运行应用程序并导航到/Movies URL。 您可以看到新的 "分级" 字段。

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

单击 "**新建**" 链接以添加新电影。 请注意，可以添加级别。

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

单击“创建”。 现在电影列表中显示了新电影，其中包括评分：

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

还应将 "`Rating`" 字段添加到 "编辑"、"详细信息" 和 "SearchIndex" 视图模板。

您可以在 "**包管理器控制台**" 窗口中再次输入 "更新数据库" 命令，而且不会进行任何更改，因为架构与模型匹配。

在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。 还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。

> [!div class="step-by-step"]
> [上一页](examining-the-edit-methods-and-edit-view.md)
> [下一页](adding-validation-to-the-model.md)
