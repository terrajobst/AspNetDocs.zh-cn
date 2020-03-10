---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第4部分：模型和数据访问 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第4部分介绍了模型和数据访问。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451016"
---
# <a name="part-4-models-and-data-access"></a>第4部分：模型和数据访问

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。
> 
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第4部分介绍了模型和数据访问。

到目前为止，我们只是将控制器中的 "虚拟数据" 传递到我们的视图模板。 现在，我们已准备好挂钩实际数据库。 在本教程中，我们将介绍如何使用 SQL Server Compact 版（通常称为 SQL CE）作为数据库引擎。 SQL CE 是一个基于文件的免费嵌入式数据库，不需要任何安装或配置，这使得本地开发非常方便。

## <a name="database-access-with-entity-framework-code-first"></a>使用实体框架代码的数据库访问-第一项

我们将使用 ASP.NET MVC 3 项目中包含的实体框架（EF）支持来查询和更新数据库。 EF 是一个灵活的对象关系映射（ORM）数据 API，使开发人员能够以面向对象的方式查询和更新存储在数据库中的数据。

实体框架版本4支持称为 "代码优先" 的开发模式。 代码优先允许您通过编写简单的类（也称为 "纯旧式" CLR 对象中的 POCO）来创建模型对象，甚至可以通过类动态创建数据库。

### <a name="changes-to-our-model-classes"></a>对模型类的更改

在本教程的实体框架中，我们将利用数据库创建功能。 不过，在这样做之前，让我们对我们的模型类进行一些小的更改，以便添加到我们稍后将使用的一些功能。

#### <a name="adding-the-artist-model-classes"></a>添加艺术家模型类

我们的唱集将与艺术家相关联，因此，我们将添加一个用于描述艺术家的简单模型类。 使用如下所示的代码，将一个新类添加到名为 Artist.cs 的模型文件夹中。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>更新模型类

更新唱片集类，如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

接下来，对流派类进行以下更新。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a>添加应用\_Data 文件夹

我们会将一个应用\_数据目录添加到项目中，以便保存 SQL Server Express 数据库文件。 应用\_数据是 ASP.NET 中的一个特殊目录，它已经具有数据库访问的正确安全访问权限。 从 "项目" 菜单中，选择 "添加 ASP.NET 文件夹"，然后选择 "应用\_数据"。

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>在 web.config 文件中创建连接字符串

我们将在网站的配置文件中添加几行，以便实体框架知道如何连接到数据库。 双击位于项目根目录中的 web.config 文件。

![](mvc-music-store-part-4/_static/image2.png)

滚动到此文件的底部，并将 &lt;connectionStrings&gt; 部分直接添加到最后一行的上方，如下所示。

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>添加上下文类

右键单击 "模型" 文件夹，并添加名为 MusicStoreEntities.cs 的新类。

![](mvc-music-store-part-4/_static/image3.png)

此类将表示实体框架数据库上下文，并将为我们处理创建、读取、更新和删除操作。 此类的代码如下所示。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

就是这样-没有其他配置、特殊接口等。通过扩展 DbContext 基类，我们的 MusicStoreEntities 类能够处理我们的数据库操作。 至此，我们已经知道了，接下来，让我们将更多属性添加到我们的模型类，以利用数据库中的一些附加信息。

### <a name="adding-our-store-catalog-data"></a>添加我们的商店目录数据

我们将利用实体框架的一项功能，该功能可将 "种子" 数据添加到新创建的数据库中。 这将使用流派、艺术家和专辑列表预填充我们的商店目录。 MvcMusicStore-Assets 下载-其中包含我们在本教程前面部分使用的站点设计文件，其中包含一个带有此种子数据的类文件，位于名为 Code 的文件夹中。

在 "代码/模型" 文件夹中，找到 "SampleData.cs" 文件并将其放入项目中的 "模型" 文件夹，如下所示。

![](mvc-music-store-part-4/_static/image4.png)

现在，我们需要添加一行代码，告诉实体框架此 SampleData 类。 双击项目根目录中的 Global.asa 文件以将其打开，然后将以下行添加到应用程序\_Start 方法的顶部。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

此时，我们已完成为项目配置实体框架所需的工作。

## <a name="querying-the-database"></a>查询数据库

现在，让我们更新 StoreController，以便不使用 "虚拟数据" 调用数据库来查询其所有信息。 首先，在**StoreController**上声明一个字段，以保存名为 StoreDB 的 MusicStoreEntities 类的实例：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>更新存储索引以查询数据库

MusicStoreEntities 类由实体框架维护，并为数据库中的每个表公开一个集合属性。 让我们更新 StoreController 的索引操作，以检索数据库中的所有流派。 以前，我们通过对字符串数据进行硬编码来完成此操作。 现在，可以改为仅使用实体框架上下文 Generes 集合：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

我们的视图模板不需要进行任何更改，因为我们仍将返回以前返回的相同 StoreIndexViewModel-我们现在只从数据库返回实时数据。

当我们再次运行该项目并访问 "/Store" URL 时，我们现在会看到数据库中所有流派的列表：

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>更新存储浏览和详细信息以使用实时数据

使用/Store/Browse？流派 = *[部分流派]* 操作方法时，我们将按名称搜索流派。 我们只需要一个结果，因为对于同一流派名称，我们不应该有两个条目，因此，我们可以使用。LINQ 中的 Single （）扩展，用于查询相应的流派对象，如下所示（不要再键入）：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

单个方法采用 Lambda 表达式作为参数，该参数指定我们想要一个流派对象，使其名称与我们定义的值匹配。 在上面的示例中，我们将加载一个名称值与 Disco 匹配的单一流派对象。

我们将利用一项实体框架功能，使我们能够在检索流派对象时，指出我们想要加载的其他相关实体。 此功能称为查询结果调整，使我们可以减少访问数据库以检索所需的所有信息所需的次数。 我们想要为我们检索的流派预先提取唱集，因此我们将更新查询，使其包括在流派中。包括（"唱片集"）表示我们还需要相关唱片集。 这会更有效，因为它将在单个数据库请求中检索流派和唱片集数据。

通过这种说明，我们更新的 "浏览控制器" 操作的外观如下：

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

现在，我们可以更新应用商店浏览视图，以显示每个流派中可用的唱片集。 打开视图模板（在/Views/Store/Browse.cshtml 中找到），并按如下所示添加相册的项目符号列表。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

运行应用程序并浏览到/Store/Browse？流派 = 爵士乐显示，当前正在从数据库中提取结果，并显示所选流派中的所有唱片集。

![](mvc-music-store-part-4/_static/image2.jpg)

我们将对/Store/Details/[id] URL 进行相同的更改，并将我们的虚拟数据替换为加载其 ID 与参数值匹配的唱片集的数据库查询。

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

运行应用程序并浏览到/Store/Details/1 表明现在正在从数据库中提取结果。

![](mvc-music-store-part-4/_static/image5.png)

现在我们的商店详细信息页已设置为按唱片集 ID 显示唱片集，接下来，我们将**浏览**视图更新为链接到详细信息视图。 我们将使用 Html.actionlink，与从存储索引链接到在上一部分末尾浏览存储的操作完全一样。 浏览视图的完整源如下所示。

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

现在，我们可以从应用商店页浏览到流派页面，其中列出了可用的唱片集，然后单击唱片集查看该唱片集的详细信息。

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-3.md)
> [下一页](mvc-music-store-part-5.md)
