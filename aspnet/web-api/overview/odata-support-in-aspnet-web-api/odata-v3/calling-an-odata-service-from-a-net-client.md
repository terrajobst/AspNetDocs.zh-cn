---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: 从 .NET 客户端调用 OData 服务（C#） |Microsoft Docs
author: MikeWasson
description: 本教程演示如何从C#客户端应用程序调用 OData 服务。 本教程中使用的软件版本 Visual Studio 2013 （使用视觉对象 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498164"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>从 .NET 客户端调用 OData 服务 (C#)

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 本教程演示如何从C#客户端应用程序调用 OData 服务。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) （适用于 Visual Studio 2012）
> - [WCF Data Services 客户端库](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2。 （示例 OData 服务是使用 Web API 2 生成的，但是客户端应用程序不依赖于 Web API。）

在本教程中，我将逐步介绍如何创建一个调用 OData 服务的客户端应用程序。 OData 服务公开以下实体：

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

以下文章介绍如何在 Web API 中实现 OData 服务。 （但是，您不需要阅读它们来了解本教程。）

- [在 Web API 2 中创建 OData 终结点](creating-an-odata-endpoint.md)
- [Web API 2 中的 OData 实体关系](working-with-entity-relations.md)
- [Web API 2 中的 OData 操作](odata-actions.md)

## <a name="generate-the-service-proxy"></a>生成服务代理

第一步是生成服务代理。 服务代理是一个 .NET 类，用于定义用于访问 OData 服务的方法。 代理会将方法调用转换为 HTTP 请求。

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

首先，在 Visual Studio 中打开 "OData 服务" 项目。 在 IIS Express 中按 CTRL + F5 以本地方式运行该服务。 记下本地地址，包括 Visual Studio 分配的端口号。 创建代理时，将需要此地址。

接下来，打开 Visual Studio 的另一个实例，并创建一个控制台应用程序项目。 控制台应用程序将是我们的 OData 客户端应用程序。 （您也可以将该项目添加到与该服务相同的解决方案中。）

> [!NOTE]
> 其余步骤引用控制台项目。

在解决方案资源管理器中，右键单击 "**引用**"，然后选择 "**添加服务引用**"。

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

在 "**添加服务引用**" 对话框中，键入 OData 服务的地址：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

其中*port*是端口号。

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

对于 "**命名空间**"，键入 "ProductService"。 此选项定义代理类的命名空间。

单击 **“转到”** 。 Visual Studio 将读取 OData 元数据文档，以发现服务中的实体。

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

单击 **"确定"** 将代理类添加到项目。

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>创建服务代理类的实例

在 `Main` 方法中，创建代理类的新实例，如下所示：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

同样，使用服务运行时使用的实际端口号。 部署服务时，将使用实时服务的 URI。 不需要更新代理。

下面的代码将添加一个事件处理程序，用于将请求 Uri 打印到控制台窗口。 此步骤不是必需的，但请务必查看每个查询的 Uri。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>查询服务

下面的代码从 OData 服务获取产品列表。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

请注意，不需要编写任何代码来发送 HTTP 请求或分析响应。 在**foreach**循环中枚举 `Container.Products` 集合时，代理类会自动执行此类。

运行应用程序时，输出应如下所示：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

若要按 ID 获取实体，请使用 `where` 子句。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

本主题的其余部分不会显示整个 `Main` 函数，只是调用服务所需的代码。

## <a name="apply-query-options"></a>应用查询选项

OData 定义可用于对数据进行筛选、排序、分页等的[查询选项](../supporting-odata-query-options.md)。 在服务代理中，可以通过使用各种 LINQ 表达式来应用这些选项。

在本部分中，我将演示一些简单的示例。 有关更多详细信息，请参阅 MSDN 上的主题[LINQ 注意事项（WCF 数据服务）](https://msdn.microsoft.com/library/ee622463.aspx) 。

### <a name="filtering-filter"></a>筛选（$filter）

若要进行筛选，请使用 `where` 子句。 下面的示例按产品类别进行筛选。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

此代码对应于以下 OData 查询。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

请注意，代理将 `where` 子句转换为 OData `$filter` 表达式。

### <a name="sorting-orderby"></a>排序（$orderby）

若要进行排序，请使用 `orderby` 子句。 下面的示例按价格从高到低的顺序进行排序。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

下面是相应的 OData 请求。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>客户端分页（$skip 和 $top）

对于大型实体集，客户端可能需要限制结果的数目。 例如，客户端一次可能会显示10个条目。 这称为*客户端分页*。 （还有[服务器端分页](../supporting-odata-query-options.md#server-paging)，服务器将限制结果数。）若要执行客户端分页，请使用 LINQ **Skip**和**Take**方法。 下面的示例跳过前40个结果，并取下10。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

下面是相应的 OData 请求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>选择（$select）并展开（$expand）

若要包括相关实体，请使用 `DataServiceQuery<t>.Expand` 方法。 例如，若要包括每个 `Product`的 `Supplier`：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

下面是相应的 OData 请求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

若要更改响应的形状，请使用 LINQ **select**子句。 下面的示例只获取每个产品的名称，不包含其他属性。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

下面是相应的 OData 请求：

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 子句可以包括相关实体。 在这种情况下，请不要调用**Expand**;在这种情况下，代理将自动包括扩展。 下面的示例获取了每个产品的名称和供应商。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

下面是相应的 OData 请求。 请注意，它包含 **$expand**选项。

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

有关 $select 和 $expand 的详细信息，请参阅[在 WEB API 2 中使用 $select、$expand 和 $value](../using-select-expand-and-value.md)。

## <a name="add-a-new-entity"></a>添加新实体

若要将新实体添加到实体集，请调用 `AddToEntitySet`，其中*EntitySet*是实体集的名称。 例如，`AddToProducts` 向 `Products` 实体集添加新 `Product`。 生成代理时，WCF 数据服务会自动创建这些强类型的**AddTo**方法。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

若要在两个实体之间添加链接，请使用**AddLink**和**SetLink**方法。 以下代码将添加新的供应商和新产品，然后在它们之间创建链接。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

当导航属性是集合时，请使用**AddLink** 。 在此示例中，我们要将产品添加到供应商的 `Products` 集合。

当导航属性为单个实体时，请使用**SetLink** 。 在此示例中，我们将设置产品的 `Supplier` 属性。

## <a name="update--patch"></a>更新/修补

若要更新实体，请调用**UpdateObject**方法。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

在调用**SaveChanges**时执行更新。 默认情况下，WCF 发送 HTTP 合并请求。 **PatchOnUpdate**选项告知 WCF 改为发送 HTTP 修补程序。

> [!NOTE]
> 为什么要修补与合并？ 原始 HTTP 1.1 规范（[RCF 2616](http://tools.ietf.org/html/rfc2616)）未定义具有 "部分更新" 语义的任何 HTTP 方法。 为了支持部分更新，OData 规范定义了 MERGE 方法。 在2010中， [RFC 5789](http://tools.ietf.org/html/rfc5789)为部分更新定义了修补程序方法。 你可以在 WCF 数据服务博客上阅读此[博客文章](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)中的部分历史记录。 目前，修补程序优先于 MERGE。 Web API 基架创建的 OData 控制器支持这两种方法。

如果要替换整个实体（PUT 语义），请指定**带 savechangesoptions.replaceonupdate**选项。 这将导致 WCF 发送 HTTP PUT 请求。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>删除实体

若要删除实体，请调用**DeleteObject**。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>调用 OData 操作

在 OData 中，[操作](odata-actions.md)是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。

尽管 OData 元数据文档描述了这些操作，但 proxy 类不会为它们创建任何强类型化方法。 你仍可以使用泛型**Execute**方法调用 OData 操作。 但是，您需要了解参数的数据类型和返回值。

例如，`RateProduct` 操作使用 `Int32` 类型的名为 "分级" 的参数，并返回 `double`。 下面的代码演示如何调用此操作。

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

有关详细信息，请参阅[调用服务操作和操作](https://msdn.microsoft.com/library/hh230677.aspx)。

一种选择是扩展**容器类**，以提供调用该操作的强类型方法：

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
