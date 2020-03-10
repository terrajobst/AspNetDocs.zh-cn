---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的操作和函数 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，操作和函数是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。 本教程演示如何 。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448058"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>使用 ASP.NET Web API 2.2 的 OData v4 中的操作和函数

作者： [Mike Wasson](https://github.com/MikeWasson)

> 在 OData 中，操作和函数是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。 本教程演示如何使用 Web API 2.2 将操作和函数添加到 OData v4 终结点。 本教程基于[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)教程
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
> - Web API 2。2
> - OData v4
> - Visual Studio 2013 （[在此处](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下载 Visual Studio 2017）
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>教程版本
>
> 对于 OData 版本3，请参阅[ASP.NET Web API 2 中的 Odata 操作](../odata-v3/odata-actions.md)。

*操作*和*函数*之间的区别在于操作可能有副作用，而函数不会有副作用。 操作和函数都可以返回数据。 操作的一些用途包括：

- 复杂事务。
- 一次操作多个实体。
- 仅允许更新实体的某些属性。
- 发送的数据不是实体。

函数可用于返回与实体或集合不直接对应的信息。

操作（或函数）可以面向单个实体或集合。 在 OData 术语中，这是*绑定*。 你还可以 &quot;未绑定的&quot; 操作/函数，这些操作在服务上被称为静态操作。

## <a name="example-adding-an-action"></a>示例：添加操作

让我们定义一个操作来对产品进行评级。

> [!NOTE]
> 本教程基于教程[使用 ASP.NET Web API 2 创建 OData V4 终结点](create-an-odata-v4-endpoint.md)

首先，添加一个 `ProductRating` 模型来表示评级。

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

同时，将**DbSet**添加到 `ProductsContext` 类，以便 EF 将在数据库中创建一个分级表。

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>向 EDM 添加操作

在 WebApiConfig.cs 中，添加以下代码：

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

**EntityTypeConfiguration**方法将操作添加到实体数据模型（EDM）。 **参数**方法为操作指定类型化参数。

此代码还设置 EDM 的命名空间。 命名空间之所以重要，是因为操作的 URI 包含完全限定的操作名称：

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> 在典型的 IIS 配置中，此 URL 中的点将导致 IIS 返回错误404。 可以通过将以下部分添加到 web.config 文件来解决此问题：

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>为操作添加控制器方法

若要启用 &quot;速率&quot; 操作，请将以下方法添加到 `ProductsController`：

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

请注意，方法名称与操作名称匹配。 **[HttpPost]** 特性指定方法是 HTTP POST 方法。

若要调用该操作，客户端将发送 HTTP POST 请求，如下所示：

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

&quot;速率&quot; 操作绑定到产品实例，因此操作的 URI 是附加到实体 URI 的完全限定的操作名称。 （请记住，我们将 EDM 命名空间设置为 &quot;ProductService&quot;，因此完全限定的操作名称 &quot;ProductService&quot;。）

请求正文包含操作参数作为 JSON 有效负载。 Web API 会自动将 JSON 负载转换为**ODataActionParameters**对象，该对象只是参数值的字典。 使用此字典可以访问控制器方法中的参数。

如果客户端发送的操作参数格式不正确，则**ModelState**的值为 false。 检查控制器方法中的此标志，并在**IsValid**为 false 时返回错误。

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>示例：添加函数

现在，让我们添加一个返回最昂贵的产品的 OData 函数。 与前面一样，第一步是将函数添加到 EDM。 在 WebApiConfig.cs 中，添加以下代码。

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

在这种情况下，该函数将绑定到 Products 集合，而不是单独的产品实例。 客户端通过发送 GET 请求来调用函数：

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

下面是此函数的控制器方法：

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

请注意，方法名称与函数名称匹配。 **[HttpGet]** 特性指定方法是 HTTP GET 方法。

下面是 HTTP 响应：

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>示例：添加未绑定函数

上一个示例是绑定到集合的函数。 在下面的示例中，我们将创建一个*未绑定*的函数。 未绑定函数将作为服务的静态操作调用。 在此示例中，函数将返回给定邮政编码的增值税。

在 Webapiconfig.cs 文件中，将函数添加到 EDM：

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

请注意，我们将直接在**ODataModelBuilder**（而不是实体类型或集合）上调用**函数**。 这会告知模型生成器该函数未绑定。

下面是实现函数的控制器方法：

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

将此方法放在哪个 Web API 控制器上并不重要。 可以将其放在 `ProductsController`中，也可以定义一个单独的控制器。 **[ODataRoute]** 特性定义函数的 URI 模板。

下面是客户端请求的示例：

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

HTTP 响应：

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
