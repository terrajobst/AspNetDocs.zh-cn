---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 在 ASP.NET Web API 1-ASP.NET 4.x 中启用 CRUD 操作
author: MikeWasson
description: 本教程介绍如何使用 ASP.NET Web API for ASP.NET 4.x 支持 HTTP 服务中的 CRUD 操作。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600335"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>在 ASP.NET Web API 1 中启用 CRUD 操作

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> 本教程演示如何使用 ASP.NET Web API for ASP.NET 4.x 支持 HTTP 服务中的 CRUD 操作。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Visual Studio 2012
> - Web API 1 （也适用于 Web API 2）

CRUD 代表 &quot;创建、读取、更新和删除，&quot; 这四个基本数据库操作。 许多 HTTP 服务还通过 REST 或 REST 等 Api 对 CRUD 操作进行建模。

在本教程中，你将构建一个非常简单的 web API 来管理产品列表。 每个产品都将包含一个名称、价格和类别（如 &quot;玩具&quot; 或 &quot;硬件&quot;）和产品 ID。

产品 API 将公开以下方法。

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 获取所有产品的列表 | GET | /api/products |
| 按 ID 获取产品 | GET | /api/products/*id* |
| 按类别获取产品 | GET | /api/products？ category =*类别* |
| 创建新产品 | POST | /api/products |
| 更新产品 | PUT | /api/products/*id* |
| 删除产品 | 删除 | /api/products/*id* |

请注意，某些 Uri 包含 "路径" 中的产品 ID。 例如，若要获取 ID 为28的产品，客户端将为 `http://hostname/api/products/28`发送 GET 请求。

### <a name="resources"></a>资源

产品 API 定义两种资源类型的 Uri：

| 资源 | URI |
| --- | --- |
| 所有产品的列表。 | /api/products |
| 单个产品。 | /api/products/*id* |

### <a name="methods"></a>方法

四个主要 HTTP 方法（GET、PUT、POST 和 DELETE）可以映射到 CRUD 操作，如下所示：

- GET 检索指定 URI 处的资源的表示形式。 GET 应在服务器上没有副作用。
- PUT 在指定的 URI 上更新资源。 如果服务器允许客户端指定新的 uri，则 PUT 还可用于在指定的 URI 处创建新的资源。 对于本教程，API 不支持通过 PUT 进行创建。
- POST 会创建一个新的资源。 服务器分配新对象的 URI，并在响应消息中返回此 URI。
- DELETE 删除指定 URI 处的资源。

注意： PUT 方法将替换整个 product 实体。 也就是说，客户端应发送已更新产品的完整表示形式。 如果希望支持部分更新，则最好选择 PATCH 方法。 本教程不实现修补程序。

## <a name="create-a-new-web-api-project"></a>创建新的 Web API 项目

首先运行 Visual Studio，然后从**起始**页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 将项目命名为 &quot;ProductStore&quot; 并单击 **"确定"** 。

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Web API** "，然后单击 **"确定"** 。

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>添加模型

模型是表示应用程序中的数据的对象。 在 ASP.NET Web API 中，可以使用强类型化的 CLR 对象作为模型，它们会自动序列化为客户端的 XML 或 JSON。

对于 ProductStore API，我们的数据包含产品，因此，我们将创建一个名为 `Product`的新类。

如果解决方案资源管理器尚不可见，请单击 "**查看**" 菜单，然后选择 "**解决方案资源管理器**"。 在解决方案资源管理器中，右键单击 "**模型**" 文件夹。 从上下文菜单中，选择 "**添加**"，然后选择 "**类**"。 将类命名为 &quot;产品&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

将以下属性添加到 `Product` 类。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>添加存储库

我们需要存储产品集合。 最好将集合与我们的服务实现分离。 这样，我们就可以更改后备存储，而无需重写服务类。 这种类型的设计称为*存储库*模式。 首先定义存储库的泛型接口。

在解决方案资源管理器中，右键单击 "**模型**" 文件夹。 选择 "**添加**"，然后选择 "**新建项**"。

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

在 "**模板**" 窗格中，选择 "**已安装模板**" 并展开C#节点。 在C#下，选择 "**代码**"。 在代码模板列表中，选择 "**接口**"。 将接口命名 &quot;IProductRepository&quot;。

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

添加以下实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

现在，将另一个类添加到名为 &quot;化 productrepository 的模型文件夹中。此类&quot; 将实现 `IProductRepository` 接口。 添加以下实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

存储库将列表保存在本地内存中。 这对于教程来说是可以的，但在实际的应用程序中，你应将数据存储在外部、数据库或云存储中。 存储库模式使稍后可以更轻松地更改实现。

## <a name="adding-a-web-api-controller"></a>添加 Web API 控制器

如果你使用了 ASP.NET MVC，则已熟悉控制器。 在 ASP.NET Web API 中，*控制器*是处理来自客户端的 HTTP 请求的类。 "新建项目" 向导在创建项目时为您创建了两个控制器。 若要查看它们，请展开解决方案资源管理器中的 "控制器" 文件夹。

- HomeController 是传统的 ASP.NET MVC 控制器。 它负责为网站提供 HTML 页面，而不是直接与 web API 相关。
- ValuesController 是 WebAPI 控制器的示例。

在解决方案资源管理器中右键单击该文件，然后选择 "删除"，以删除 ValuesController **。** 现在，添加一个新的控制器，如下所示：

在**解决方案资源管理器**中，右键单击 "控制器" 文件夹。 选择 "**添加**"，然后选择 "**控制器**"。

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

在 "**添加控制器**" 向导中，将控制器命名为 &quot;ProductsController&quot;。 在 "**模板**" 下拉列表中，选择 "**空 API 控制器**"。 然后单击 **“添加”** 。

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> 不需要将控制器放入名为控制器的文件夹中。 文件夹名称不重要;它只是一种用于组织源文件的简便方法。

**添加控制器**向导将在 "控制器" 文件夹中创建一个名为 "ProductsController.cs" 的文件。 如果此文件尚未打开，请双击该文件将其打开。 添加以下**using**语句：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

添加用于保存**IProductRepository**实例的字段。

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> 在控制器中调用 `new ProductRepository()` 不是最佳设计，因为它将控制器与 `IProductRepository`的特定实现联系在一起。 有关更好的方法，请参阅[使用 WEB API 依赖关系解析程序](../advanced/dependency-injection.md)。

## <a name="getting-a-resource"></a>获取资源

ProductStore API 将公开几个 &quot;将&quot; 操作作为 HTTP GET 方法进行读取。 每个操作都对应于 `ProductsController` 类中的一个方法。

| 操作 | HTTP 方法 | 相对 URI |
| --- | --- | --- |
| 获取所有产品的列表 | GET | /api/products |
| 按 ID 获取产品 | GET | /api/products/*id* |
| 按类别获取产品 | GET | /api/products？ category =*类别* |

若要获取所有产品的列表，请将以下方法添加到 `ProductsController` 类：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

方法名称以 &quot;Get&quot;开始，因此按约定映射到获取请求。 此外，因为该方法没有参数，它将映射到路径中不包含 *&quot;id&quot;* 段的 URI。

若要按 ID 获取产品，请将以下方法添加到 `ProductsController` 类：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

此方法名称还从 &quot;Get&quot;开始，但该方法具有一个名为*id*的参数。此参数映射到 URI 路径 &quot;id&quot; 段。 ASP.NET Web API 框架自动将该 ID 转换为参数的正确数据类型（**int**）。

如果*id*无效，GetProduct 方法将引发**带有 httpresponseexception**类型的异常。 此异常将由框架转换为404（未找到）错误。

最后，添加一个方法，按类别查找产品：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

如果请求 URI 具有查询字符串，则 Web API 会尝试将查询参数与控制器方法的参数匹配。 因此，"api/products？ category =*category*" 形式的 URI 将映射到此方法。

## <a name="creating-a-resource"></a>创建资源

接下来，我们将向 `ProductsController` 类添加一个方法来创建新产品。 下面是方法的简单实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

请注意有关此方法的两个事项：

- 方法名称以 &quot;Post ...&quot;开头。 若要创建新产品，客户端将发送 HTTP POST 请求。
- 方法采用 Product 类型的参数。 在 Web API 中，具有复杂类型的参数将从请求正文反序列化。 因此，我们希望客户端以 XML 或 JSON 格式发送 product 对象的序列化表示形式。

此实现将起作用，但并不完整。 理想情况下，我们希望 HTTP 响应包括以下内容：

- **响应代码：** 默认情况下，Web API 框架将响应状态代码设置为200（OK）。 但根据 HTTP/1.1 协议，当 POST 请求导致资源创建时，服务器应使用状态201（已创建）进行回复。
- **位置：** 当服务器创建资源时，它应在响应的 Location 标头中包含新资源的 URI。

ASP.NET Web API 可以轻松地操作 HTTP 响应消息。 下面是改进的实现：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

请注意，方法返回类型现在为**HttpResponseMessage**。 通过返回**HttpResponseMessage**而不是产品，我们可以控制 HTTP 响应消息的详细信息，包括状态代码和位置标头。

**CreateResponse**方法创建**HttpResponseMessage** ，并将产品对象的序列化表示形式自动写入响应消息的正文中。

> [!NOTE]
> 此示例不验证 `Product`。 有关模型验证的信息，请参阅[中的模型验证 ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。

## <a name="updating-a-resource"></a>更新资源

使用 PUT 更新产品非常简单：

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

方法名称以 &quot;Put ...&quot;开头，因此 Web API 会将其与 PUT 请求相匹配。 方法采用两个参数：产品 ID 和更新的产品。 *Id*参数是从 URI 路径获取的， *product*参数是从请求正文反序列化的。 默认情况下，ASP.NET Web API 框架从路由使用简单的参数类型，并从请求正文获取复杂类型。

## <a name="deleting-a-resource"></a>删除资源

若要删除资源，请定义 "Delete ..."付款方式.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

如果 DELETE 请求成功，则它可以返回状态200（OK），其中包含描述状态的实体正文;如果删除仍处于挂起状态，则为状态202（已接受）;或状态204（无内容），无实体正文。 在这种情况下，`DeleteProduct` 方法具有 `void` 返回类型，因此 ASP.NET Web API 会自动将其转换为状态代码204（无内容）。
