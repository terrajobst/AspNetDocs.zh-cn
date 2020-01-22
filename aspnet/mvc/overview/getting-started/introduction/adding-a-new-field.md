---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 添加新字段 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: d79655bfadff83095bf4cb84445f5efaf44d6a89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519071"
---
# <a name="adding-a-new-field"></a>添加新字段

作者： [Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](index.md)]

在本节中，您将使用 Entity Framework Code First 迁移将某些更改迁移到模型类，以便将更改应用到数据库。

默认情况下，当你使用实体框架 Code First 来自动创建数据库时（如在本教程前面的步骤中所做的那样），Code First 将向数据库中添加一个表，以帮助跟踪数据库的架构是否与生成它的模型类的架构同步。 如果不同步，实体框架将引发错误。 这样就可以在开发时更轻松地跟踪问题，否则在运行时可能仅会发现（隐藏错误）。

## <a name="setting-up-code-first-migrations-for-model-changes"></a>设置模型更改的 Code First 迁移

导航到解决方案资源管理器。 右键单击 "*电影 .mdf* " 文件，然后选择 "**删除**" 以删除电影数据库。 如果看不到 "*电影 .mdf* " 文件，请单击红色框中显示的 "**显示所有文件**" 图标。

![](adding-a-new-field/_static/image1.png)

生成应用程序，以确保没有任何错误。

在“工具”菜单中，单击“NuGet 包管理器”，然后单击“包管理器控制台”。

![添加包手册](adding-a-new-field/_static/image2.png)

在 "**包管理器控制台**" 窗口中，在 `PM>` 提示符下输入

Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext

![](adding-a-new-field/_static/image3.png)

"**启用-迁移**" 命令（如上所示）在新的 "*迁移*" 文件夹中创建*Configuration.cs*文件。

![](adding-a-new-field/_static/image4.png)

Visual Studio 将打开*Configuration.cs*文件。 将*Configuration.cs*文件中的 `Seed` 方法替换为以下代码：

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

将鼠标悬停在 `Movie` 下面的红色波浪线上，然后单击 "`Show Potential Fixes`，然后单击"**使用** **MvcMovie "。**

![](adding-a-new-field/_static/image5.png)

这样做将添加以下 using 语句：

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Code First 迁移将在每次迁移后调用 `Seed` 方法（即，在包管理器控制台中调用**更新数据库**），此方法将更新已插入的行，如果它们尚不存在，则将其插入。
> 
> 以下代码中的[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法执行 "upsert" 操作：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> 由于[种子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法随每个迁移一起运行，因此您不能只插入数据，因为在第一个创建数据库的迁移之后，您尝试添加的行将已存在。 如果尝试插入已存在的行，"[upsert](http://en.wikipedia.org/wiki/Upsert)" 操作将会阻止发生的错误，但会覆盖在测试应用程序时对数据所做的任何更改。 对于某些表中的测试数据，您可能不希望发生这种情况：在某些情况下，当您在测试时更改数据时，您希望在数据库更新后更改保持不变。 在这种情况下，需要执行条件插入操作：仅在不存在行时插入行。   
> 
> 传递给[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的第一个参数指定要用于检查行是否已存在的属性。 对于所提供的测试电影数据，`Title` 属性可用于此目的，因为列表中的每个标题都是唯一的：
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> 此代码假设标题是唯一的。 如果手动添加重复标题，则在下次执行迁移时，将会出现以下异常。   
> 
> *序列包含多个元素*  
> 
> 有关[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的详细信息，请参阅[使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

**按 CTRL-SHIFT-B 生成项目。** （如果此时不生成，以下步骤将会失败。）

下一步是创建用于初始迁移的 `DbMigration` 类。 此迁移创建新的数据库，这就是在上一步中删除了*movie .mdf*文件的原因。

在 "**程序包管理器控制台**" 窗口中，输入命令 `add-migration Initial` 以创建初始迁移。 名称 "初始" 是任意名称，用于命名创建的迁移文件。

![](adding-a-new-field/_static/image6.png)

Code First 迁移在 "*迁移*" 文件夹（名称为 *{日期戳}\_Initial.cs* ）中创建另一个类文件，并且此类包含用于创建数据库架构的代码。 迁移文件名预先修复了时间戳，以帮助进行排序。 检查 *{日期戳}\_Initial.cs*文件，其中包含为电影数据库创建 `Movies` 表的说明。 当你在下面的说明中更新数据库时，此 *{日期戳}\_Initial.cs*文件将运行，并创建数据库架构。 然后， **Seed**方法将运行以用测试数据填充数据库。

在 "**包管理器控制台**" 中，输入用于创建数据库的命令 `update-database`，并运行 `Seed` 方法。

![](adding-a-new-field/_static/image7.png)

如果您收到一条错误消息，指示表已存在并且无法创建，则可能是您在删除数据库之后和执行 `update-database`之前运行了该应用程序。 在这种情况下，请再次删除*电影 .mdf*文件，然后重试 `update-database` 命令。 如果仍出现错误，请删除 "迁移" 文件夹和 "内容"，然后从本页顶部的说明开始（删除 ""，然后继续执行 "启用-*迁移"）* 。 如果仍出现错误，请打开 SQL Server 对象资源管理器并从列表中删除数据库。

运行应用程序并导航到 */Movies* URL。 将显示种子数据。

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>向电影模型添加分级属性

首先向现有 `Movie` 类添加新的 `Rating` 属性。 打开*Models\Movie.cs*文件并添加 `Rating` 属性，如下所示：

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

完整的 `Movie` 类现在如以下代码所示：

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

构建应用程序（Ctrl + Shift + B）。

因为你已将新字段添加到`Movie`类，你还需要更新绑定允许列表以便将包含此新属性。 更新 `Create` 和 `Edit` 操作方法的 `bind` 属性，以包括 `Rating` 属性：

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

还需要更新视图模板，以便在浏览器视图中显示、创建和编辑新的 `Rating` 属性。

打开 *\Views\Movies\Index.cshtml* 文件，并添加`<th>Rating</th>`列标题之后**价格**列。 然后，将 `<td>` 列添加到模板末尾附近，以呈现 `@item.Rating` 值。 下面是哪些更新 *Index.cshtml* 视图模板如下所示：

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

接下来，打开 *\Views\Movies\Create.cshtml*文件并添加 "`Rating`" 字段，其中包含以下突出显示的标记。 这将呈现一个文本框，以便您可以在创建新电影时指定级别。

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

现在，你已更新了应用程序代码，以支持新的 `Rating` 属性。

运行应用程序并导航到 */Movies* URL。 不过，当你执行此操作时，你将看到以下错误之一：

![](adding-a-new-field/_static/image9.png)  
  
创建数据库后，支持 "MovieDBContext" 上下文的模型已发生更改。 请考虑使用 Code First 迁移更新数据库（ https://go.microsoft.com/fwlink/?LinkId=238269) 。

![](adding-a-new-field/_static/image10.png)

出现此错误的原因是，应用程序中更新的 `Movie` 模型类现在与现有数据库的 `Movie` 表的架构不同。 （数据库表中没有 `Rating` 列。）

可通过几种方法解决此错误：

1. 让 Entity Framework 自动丢弃，并基于新的模型类架构重新创建数据库。 在测试数据库上进行开发时，此方法在开发周期早期很方便；通过它可以一起快速改进模型和数据库架构。 缺点，不过，是会丢失数据库中的现有数据，因此您 *不* 需要生产数据库上使用此方法 ！ 使用初始值设定项，以使用测试数据自动设定数据库种子，这通常是开发应用程序的有效方式。 有关实体框架数据库初始值设定项的详细信息，请参阅[ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
2. 对现有数据库架构进行显式修改，使它与模型类相匹配。 此方法的优点是可以保留数据。 可以手动或通过创建数据库更改脚本进行此更改。
3. 使用 Code First 迁移更新数据库架构。

本教程使用 Code First 迁移。

更新种子方法，使其为新列提供一个值。 打开 Migrations\Configuration.cs 文件，并向每个电影对象添加分级字段。

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

生成解决方案，然后打开 "**包管理器控制台**" 窗口，并输入以下命令：

`add-migration Rating`

`add-migration` 命令通知迁移框架检查当前的电影模型和当前的 movie DB 架构，并创建必要的代码以将数据库迁移到新模型。 名称*级别*是任意的，用于对迁移文件进行命名。 为迁移步骤使用有意义的名称会很有帮助。

此命令完成后，Visual Studio 将打开定义新的 `DbMigration` 派生类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

生成解决方案，然后在 "**包管理器控制台**" 窗口中输入 `update-database` 命令。

下图显示了 "**包管理器控制台**" 窗口中的输出（预先计算*评分*的日期戳将有所不同）。

![](adding-a-new-field/_static/image11.png)

重新运行应用程序并导航到/Movies URL。 您可以看到新的 "分级" 字段。

![](adding-a-new-field/_static/image12.png)

单击 "**新建**" 链接以添加新电影。 请注意，可以添加级别。

![7_CreateRioII](adding-a-new-field/_static/image13.png)

单击 **“创建”** 。 现在电影列表中显示了新电影，其中包括评分：

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

现在，项目正在使用迁移，因此在添加新字段或更新架构时，无需删除数据库。 在下一部分中，我们将进行更多架构更改，并使用迁移来更新数据库。

还应将 "`Rating`" 字段添加到 "编辑"、"详细信息" 和 "删除" 视图模板。

您可以在 "**包管理器控制台**" 窗口中再次输入 "更新数据库" 命令，而不会运行任何迁移代码，因为该架构与该模型匹配。 但是，运行 "更新数据库" 将再次运行 `Seed` 方法，如果更改了任何种子数据，则这些更改将丢失，因为 `Seed` 方法 upsert 数据。 若要详细了解 Tom Dykstra 的热门[ASP.NET MVC/实体框架教程](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)中的 `Seed` 方法。

在本部分中，您将了解如何修改模型对象并使数据库与更改保持同步。 还了解了使用示例数据填充新创建的数据库的方法，以便可以试用方案。 这只是 Code First 的简要介绍，请参阅为[ASP.NET MVC 应用程序创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，以获取有关主题的更完整教程。 接下来，让我们看看如何将更丰富的验证逻辑添加到模型类，并实现一些业务规则。

> [!div class="step-by-step"]
> [上一页](adding-search.md)
> [下一页](adding-validation.md)
