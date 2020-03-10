---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 使用 ASP.NET Web API 2.2 创建 OData v4 终结点 |Microsoft Docs
author: MikeWasson
description: Open Data Protocol （OData）是 web 的数据访问协议。 OData 通过 CRUD 操作提供一种统一的方法来查询和操作数据集 。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484496"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>使用 ASP.NET Web API 创建 OData v4 终结点 

> Open Data Protocol （OData）是 web 的数据访问协议。 OData 通过 CRUD 操作（创建、读取、更新和删除）提供了一种统一的方法来查询和操作数据集。
>
> ASP.NET Web API 支持协议的 v3 和 v4。 甚至可以使用与 v3 终结点并行运行的 v4 终结点。
>
> 本教程演示如何创建支持 CRUD 操作的 OData v4 终结点。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - Web API 5。2
> - OData v4
> - Visual Studio 2017 （下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/)）
> - Entity Framework 6
> - .NET 4.7.2
>
> ## <a name="tutorial-versions"></a>教程版本
>
> 对于 OData 版本3，请参阅[创建 odata V3 终结点](../odata-v3/creating-an-odata-endpoint.md)。

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

在 Visual Studio 的 "**文件**" 菜单中，选择 "**新建**" &gt;**项目**"。

展开 "**已安装**&gt; **Visual C#**  &gt; **web**"，然后选择 " **ASP.NET Web 应用程序（.NET Framework）** " 模板。 将项目命名为 &quot;ProductService&quot;。

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

选择“确定”。

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

选择“空”模板。 在 "**添加文件夹和核心引用：** " 下，选择 " **Web API**"。 选择“确定”。

## <a name="install-the-odata-packages"></a>安装 OData 包

从“工具”菜单中，选择“NuGet 包管理器” **“包管理器控制台”** &gt;。 在 "程序包管理器控制台" 窗口中，键入：

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

此命令安装最新的 OData NuGet 包。

## <a name="add-a-model-class"></a>添加模型类

*模型*是表示应用程序中的数据实体的对象。

在解决方案资源管理器中，右键单击“模型”文件夹。 从上下文菜单中，选择 "**添加**&gt;**类**"。

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 按照约定，模型类放置在 "模型" 文件夹中，但你无需在自己的项目中遵循此约定。

将此类命名为 `Product`。 在 Product.cs 文件中，将样板代码替换为以下代码：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` 属性是实体键。 客户端可以按键查询实体。 例如，若要获取 ID 为5的产品，请 `/Products(5)`URI。 `Id` 属性还将是后端数据库中的主键。

## <a name="enable-entity-framework"></a>启用实体框架

对于本教程，我们将使用实体框架（EF） Code First 创建后端数据库。

> [!NOTE]
> Web API OData 不需要 EF。 使用任何可以将数据库实体转换为模型的数据访问层。

首先，安装适用于 EF 的 NuGet 包。 从“工具”菜单中，选择“NuGet 包管理器” **“包管理器控制台”** &gt;。 在 "程序包管理器控制台" 窗口中，键入：

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

打开 web.config 文件，并将以下部分添加到**configuration**元素中的**configSections**元素之后。

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

此设置将添加 LocalDB 数据库的连接字符串。 在本地运行应用程序时，将使用此数据库。

接下来，将名为 `ProductsContext` 的类添加到模型文件夹中：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

在构造函数中，`"name=ProductsContext"` 提供连接字符串的名称。

## <a name="configure-the-odata-endpoint"></a>配置 OData 终结点

打开文件应用\_Start/Webapiconfig.cs。 添加以下**using**语句：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

然后，将以下代码添加到**Register**方法：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

此代码执行两项操作：

- 创建实体数据模型（EDM）。
- 添加路由。

EDM 是数据的抽象模型。 EDM 用于创建服务元数据文档。 **ODataConventionModelBuilder**类使用默认命名约定创建 EDM。 此方法需要最少的代码。 如果要对 EDM 进行更多的控制，可以使用**ODataModelBuilder**类来创建 edm，方法是显式添加属性、键和导航属性。

*路由*通知 Web API 如何将 HTTP 请求路由到终结点。 若要创建 OData v4 路由，请调用**MapODataServiceRoute**扩展方法。

如果应用程序有多个 OData 终结点，请为每个终结点创建一个单独的路由。 为每个路由指定唯一的路由名称和前缀。

## <a name="add-the-odata-controller"></a>添加 OData 控制器

*控制器*是处理 HTTP 请求的类。 为 OData 服务中的每个实体集创建一个单独的控制器。 在本教程中，你将为 `Product` 实体创建一个控制器。

在解决方案资源管理器中，右键单击 "控制器" 文件夹，然后选择 "**添加**&gt;**类**"。 将此类命名为 `ProductsController`。

> [!NOTE]
> 此适用于 OData v3 的版本使用**添加控制器**基架。 当前没有适用于 OData v4 的基架。

将 ProductsController.cs 中的样板代码替换为以下代码。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

控制器使用 `ProductsContext` 类通过 EF 访问数据库。 请注意，控制器会重写**dispose**方法以释放**ProductsContext**。

这是控制器的起点。 接下来，我们将添加所有 CRUD 操作的方法。

## <a name="query-the-entity-set"></a>查询实体集

将以下方法添加到 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

`Get` 方法的无参数版本将返回整个产品集合。 带有*键*参数的 `Get` 方法按其键（在本例中为 `Id` 属性）查找产品。

**[EnableQuery]** 属性允许客户端使用查询选项（如 $filter、$sort 和 $page）来修改查询。 有关详细信息，请参阅[支持 OData 查询选项](../supporting-odata-query-options.md)。

## <a name="add-an-entity-to-the-entity-set"></a>将实体添加到实体集

若要使客户端能够将新产品添加到数据库，请将以下方法添加到 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>更新实体

OData 支持使用两种不同的语义来更新实体、修补和 PUT。

- 修补程序执行部分更新。 客户端仅指定要更新的属性。
- PUT 替换整个实体。

PUT 的缺点在于，客户端必须为实体中的所有属性发送值，包括未更改的值。 [OData 规范](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)指出此修补程序是首选的。

在任何情况下，以下是修补和 PUT 方法的代码：

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

对于修补程序，控制器使用**增量&lt;t&gt;** 类型跟踪所做的更改。

## <a name="delete-an-entity"></a>删除实体

若要使客户端能够从数据库中删除产品，请将以下方法添加到 `ProductsController`。

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
