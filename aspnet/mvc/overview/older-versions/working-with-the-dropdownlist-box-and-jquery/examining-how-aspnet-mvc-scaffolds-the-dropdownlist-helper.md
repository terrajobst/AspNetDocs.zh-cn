---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: 检查 ASP.NET MVC 如何基架 DropDownList 帮助器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457604"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>检查 ASP.NET MVC 如何支持 DropDownList 帮助程序

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。 将控制器命名为**StoreManagerController**。 设置 "**添加控制器**" 对话框的选项，如下图所示。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

编辑*StoreManager\Index.cshtml*视图并删除 `AlbumArtUrl`。 删除 `AlbumArtUrl` 将使演示更具可读性。 完成的代码如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

打开*Controllers\StoreManagerController.cs*文件并找到 `Index` 方法。 添加 `OrderBy` 子句以便按价格对唱片集排序。 完整的代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

按价格排序会使测试数据库更改变得更加容易。 在测试 "编辑" 和 "创建" 方法时，可以使用低价位，因此保存的数据将首先显示。

打开*StoreManager\Edit.cshtml*文件。 在图例标记后面添加以下行。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

下面的代码显示了此更改的上下文：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

需要 `AlbumId` 才能对唱片集记录进行更改。

按 Ctrl+F5 运行应用程序。 选择 "**管理**" 链接，然后选择 "**新建" 链接**创建新的唱片集。 验证唱片集信息已保存。 编辑唱片集并验证所做的更改是否已保存。

### <a name="the-album-schema"></a>唱片集架构

MVC 基架机制创建的 `StoreManager` 控制器允许对音乐存储数据库中的唱集进行 CRUD （创建、读取、更新、删除）访问。 唱片集信息的架构如下所示：

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` 表未存储唱片集流派和说明，它将外键存储到 `Genres` 表。 `Genres` 表包含流派名称和说明。 同样，`Albums` 表不包含唱片集艺术家名称，而是 `Artists` 表的外键。 `Artists` 表包含艺术家的姓名。 如果检查 `Albums` 表中的数据，则可以看到每一行都包含 `Genres` 表的外键和 `Artists` 表的外键。 下图显示了 `Albums` 表中的一些表数据。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML 选择标记

HTML `<select>` 元素（由 HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper 创建）用于显示值的完整列表（例如，流派列表）。 对于编辑窗体，当当前值已知时，选择列表可以显示当前值。 当我们将选定值设置为**喜剧**时，我们看到了这一点。 选择列表是显示类别或外键数据的理想选择。 流派外键的 `<select>` 元素显示了可能的流派名称的列表，但当您保存窗体时，将用流派外键值而不是显示的流派名称更新 "流派" 属性。 在下图中，所选的流派为**Disco** ，并且艺术家为**Donna 夏令时**。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>检查 ASP.NET MVC 基架代码

打开*Controllers\StoreManagerController.cs*文件并找到 `HTTP GET Create` 方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` 方法将两个[SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx)对象添加到 `ViewBag`，一个对象包含流派信息，另一个用于包含艺术家信息。 上面使用的[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)构造函数重载采用三个参数：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *项*：一个[IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) ，其中包含列表中的项。 在上面的示例中，`db.Genres`返回的流派列表。
2. *dataValueField*：包含密钥值的**IEnumerable**列表中属性的名称。 在上面的示例中，`GenreId` 和 `ArtistId`。
3. *dataTextField*： **IEnumerable**列表中包含要显示的信息的属性的名称。 在 "艺术家" 和 "流派" 表中，将使用 "`name`" 字段。

打开*Views\StoreManager\Create.cshtml*文件并检查 "流派" 字段的 `Html.DropDownList` 帮助程序标记。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

第一行显示 "创建" 视图采用 `Album` 模型。 在上面所示的 `Create` 方法中，未传递任何模型，因此视图将获取**null** `Album` 模型。 此时，我们将创建一个新的唱片集，因此没有任何 `Album` 数据。

上面所示的[DropDownList](https://msdn.microsoft.com/library/dd492948.aspx)重载使用字段的名称来绑定到模型。 它还使用此名称来查找包含[SelectList](https://msdn.microsoft.com/library/dd505286.aspx)对象的**ViewBag**对象。 如果使用此重载，则需要将**ViewBag SelectList**对象命名 `GenreId`。 第二个参数（`String.Empty`）是在没有选中任何项时要显示的文本。 这正是我们在创建新唱片集时所希望的。 如果删除了第二个参数，并使用了以下代码：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

选择列表将默认为示例中的第一个元素或摇滚。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

检查 `HTTP POST Create` 方法。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

`Create` 方法的此重载采用 `album` 对象，该对象由发布的窗体值创建的 ASP.NET MVC 模型绑定系统。 提交新的唱片集时，如果模型状态有效并且没有数据库错误，则会将该新的唱片集添加到该数据库中。 下图显示了如何创建新的唱片集。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

您可以使用[fiddler 工具](http://www.fiddler2.com/fiddler2/)来检查 ASP.NET MVC 模型绑定用来创建唱片集对象的已发布的窗体值。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png) 列中的一个值匹配。

### <a name="refactoring-the-viewbag-selectlist-creation"></a>重构 ViewBag SelectList 创建

`Edit` 方法和 `HTTP POST Create` 方法都具有相同的代码，可以在**ViewBag**中设置**SelectList** 。 在[晾干](http://en.wikipedia.org/wiki/Don't_repeat_yourself)精神中，我们将重构此代码。 稍后我们将使用此重构代码。

创建新方法，将流派和艺术家**SelectList**添加到**ViewBag**中。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

使用对 `SetGenreArtistViewBag` 方法的调用，将每个 `Create` 和 `Edit` 方法中的 `ViewBag` 替换为两行。 完成的代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

创建新的唱片集并编辑唱片集来验证更改是否正常工作。

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>将 SelectList 显式传递给 DropDownList

ASP.NET MVC 基架创建的创建和编辑视图使用以下**DropDownList**重载：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

"创建" 视图的 `DropDownList` 标记如下所示。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

由于 `SelectList` 的 `ViewBag` 属性名为 `GenreId`， **DropDownList** helper 将使用**ViewBag**中的 `GenreId`**SelectList** 。 在以下**DropDownList**重载中，`SelectList` 显式传入。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

打开*Views\StoreManager\Edit.cshtml*文件，并使用上面的重载更改**DropDownList**调用以显式传入**SelectList**。 为 "流派" 类别执行此操作。 完成的代码如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

运行应用程序，并单击 "**管理**" 链接，然后导航到 "爵士乐" 唱片集并选择 "**编辑**" 链接。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

显示 "摇滚"，而不是显示与当前所选流派相同的爵士乐。 当字符串参数（要绑定的属性）和**SelectList**对象具有相同的名称时，不会使用所选值。 如果未提供选定值，浏览器将默认为**SelectList**中的第一个元素（在上面的示例中为 "**摇滚**"）。 这是**DropDownList**帮助器的已知限制。

打开*Controllers\StoreManagerController.cs*文件，并将**SelectList**对象名称更改为 `Genres` 和 `Artists`。 完成的代码如下所示：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

名称流派和艺术家是类别的更好的名称，因为它们不仅包含每个类别的 ID。 之前已支付的重构。 我们所做的更改与 `SetGenreArtistViewBag` 方法隔离，而不是以四种方法更改**ViewBag** 。

更改 "创建" 和 "编辑" 视图中的**DropDownList**调用，以使用新的**SelectList**名称。 编辑视图的新标记如下所示：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

Create view 需要空字符串，以防止显示 SelectList 中的第一项。

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

创建新的唱片集并编辑唱片集来验证更改是否正常工作。 通过选择一个具有 "摇滚" 流派的唱片集来测试编辑代码。

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>将视图模型与 DropDownList Helper 一起使用

在名为 `AlbumSelectListViewModel`的 Viewmodel 文件夹中创建一个新类。 将 `AlbumSelectListViewModel` 类中的代码替换为以下代码：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` 构造函数采用唱片集、艺术家和流派列表，并创建包含唱片集的对象和流派和艺术家的 `SelectList`。

生成项目，以便在下一步中创建视图时，可以使用 `AlbumSelectListViewModel`。

向 `StoreManagerController`中添加 `EditVM` 方法。 完成的代码如下所示。

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

右键单击 `AlbumSelectListViewModel`，选择 "**解析**"，然后**使用 viewmodel;** 。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

或者，您可以添加以下 using 语句：

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

右键单击 `EditVM`，然后选择 "**添加视图**"。 使用如下所示的选项。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

选择 "**添加**"，然后将*Views\StoreManager\EditVM.cshtml*文件的内容替换为以下内容：

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` 标记与原始 `Edit` 标记非常相似，但有以下例外情况。

- `Edit` 视图中的模型属性的格式为 `model.property`（例如 `model.Title`）。 `EditVm` 视图中的模型属性的格式为 `model.Album.property`（例如 `model.Album.Title`）。 这是因为 `EditVM` 视图向 `Album`传递了一个容器，而不是 `Edit` 视图中的 `Album`。
- **DropDownList**第二个参数来自视图模型，而不是**ViewBag**。
- `EditVM` 视图中的**html.beginform** helper 显式回发到 `Edit` 操作方法。 通过回发到 `Edit` 操作，我们无需编写 `HTTP POST EditVM` 操作，并可重复使用 `HTTP POST` `Edit` 操作。

运行应用程序并编辑唱片集。 更改 URL 以使用 `EditVM`。 更改字段并单击 "**保存**" 按钮以验证代码是否正常工作。

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>应使用哪种方法？

这三种方法都是可接受的。 许多开发人员更喜欢使用 `ViewBag`将 `SelectList` 显式传递到 `DropDownList` 中。 此方法具有增加的优点，使你可以灵活地为集合使用更合适的名称。 需要注意的一点是，您不能将 `ViewBag SelectList` 对象命名为与 model 属性相同的名称。

某些开发人员倾向于使用 ViewModel 方法。 其他人将更详细的标记和生成的 HTML 用于 ViewModel 方法。

在本部分中，我们了解了将**DropDownList**与类别数据结合使用的三种方法。 在下一部分中，我们将介绍如何添加新类别。

> [!div class="step-by-step"]
> [上一页](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [下一页](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
