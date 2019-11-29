---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: 使用 Web API 2 创建 OData v3 终结点 |Microsoft Docs
author: MikeWasson
description: Open Data Protocol （OData）是 web 的数据访问协议。 OData 提供一种统一的方法来构建数据、查询数据和操作数据 。
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600423"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>使用 Web API 2 创建 OData v3 终结点

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [Open Data Protocol](http://www.odata.org/) （OData）是 web 的数据访问协议。 OData 提供一种统一的方式来构建数据、查询数据，以及通过 CRUD 操作（创建、读取、更新和删除）操作数据集。 OData 同时支持 AtomPub （XML）和 JSON 格式。 OData 还定义了公开数据相关元数据的方法。 客户端可以使用元数据来发现数据集的类型信息和关系。
>
> ASP.NET Web API 使你可以轻松地为数据集创建 OData 终结点。 你可以精确控制终结点支持的 OData 操作。 可以托管多个 OData 终结点和非 OData 终结点。 您可以完全控制您的数据模型、后端业务逻辑和数据层。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData 版本3
> - Entity Framework 6
> - [Fiddler Web 调试代理（可选）](http://www.fiddler2.com)
>
> [ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)中添加了 Web API OData 支持。 不过，本教程使用在 Visual Studio 2013 中添加的基架。

在本教程中，你将创建一个客户端可以查询的简单 OData 终结点。 你还将为终结C#点创建客户端。 完成本教程后，下一组教程介绍如何添加更多功能，包括实体关系、操作和 $expand/$select。

- [创建 Visual Studio 项目](#create-project)
- [添加实体模型](#add-model)
- [添加 OData 控制器](#add-controller)
- [添加 EDM 和路由](#edm)
- [播种数据库（可选）](#seed-db)
- [浏览 OData 终结点](#explore)
- [OData 序列化格式](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

在本教程中，你将创建支持基本 CRUD 操作的 OData 终结点。 终结点将公开单个资源，即产品列表。 稍后的教程将添加更多功能。

启动 Visual Studio，然后从起始页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开视觉对象C#节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 选择 **"ASP.NET Web 应用程序"** 模板。

![](creating-an-odata-endpoint/_static/image1.png)

在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。 在 &quot;添加文件夹和核心引用 ...&quot;，检查**WEB API**。 单击“确定”。

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>添加实体模型

模型是表示应用程序中的数据的对象。 对于本教程，我们需要一个表示产品的模型。 模型对应于 OData 实体类型。

在解决方案资源管理器中，右键单击 "模型" 文件夹。 从上下文菜单中，选择 "**添加**"，然后选择 "**类**"。

![](creating-an-odata-endpoint/_static/image3.png)

在 "**添加新**项" 对话框中，将类命名为 &quot;产品&quot;。

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 按照约定，将模型类置于 model 文件夹中。 你不必在自己的项目中遵循此约定，但我们将在本教程中使用它。

在 Product.cs 文件中，添加以下类定义：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 属性将为实体键。 客户端可以按 ID 查询产品。 此字段还将是后端数据库中的主键。

立即生成项目。 在下一步中，我们将使用一些使用反射查找产品类型的 Visual Studio 基架。

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>添加 OData 控制器

*控制器*是处理 HTTP 请求的类。 为 OData 服务中的每个实体集定义单独的控制器。 在本教程中，我们将创建单个控制器。

在解决方案资源管理器中，右键单击 "控制器" 文件夹。 选择 "**添加**"，然后选择 "**控制器**"。

![](creating-an-odata-endpoint/_static/image5.png)

在 "**添加基架**" 对话框中，选择 "包含操作 &quot;Web API 2 OData 控制器"，并使用实体框架&quot;。

![](creating-an-odata-endpoint/_static/image6.png)

在 "**添加控制器**" 对话框中，将控制器命名为 "ProductsController"。 选中 "&quot;使用异步控制器操作"&quot; 复选框。 在 "**模型**" 下拉列表中，选择 "产品类"。

![](creating-an-odata-endpoint/_static/image7.png)

单击 "**新建数据上下文 ...** " 按钮。 保留数据上下文类型的默认名称，然后单击 "**添加**"。

![](creating-an-odata-endpoint/_static/image8.png)

在 "添加控制器" 对话框中单击 "添加" 以添加控制器。

![](creating-an-odata-endpoint/_static/image9.png)

注意：如果收到一条错误消息，提示 &quot;获取类型时出错 ...&quot;，请确保在添加 Product 类后生成了 Visual Studio 项目。 基架使用反射来查找类。

![](creating-an-odata-endpoint/_static/image10.png)

基架将两个代码文件添加到项目中：

- Products.cs 定义用于实现 OData 终结点的 Web API 控制器。
- ProductServiceContext.cs 提供使用实体框架查询基础数据库的方法。

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>添加 EDM 和路由

在解决方案资源管理器中，展开 "应用\_启动" 文件夹，然后打开名为 "WebApiConfig.cs" 的文件。 此类包含 Web API 的配置代码。 将此代码替换为以下代码：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

此代码执行两项操作：

- 为 OData 终结点创建实体数据模型（EDM）。
- 为终结点添加路由。

EDM 是数据的抽象模型。 EDM 用于创建元数据文档和定义服务的 Uri。 **ODataConventionModelBuilder**使用一组默认命名约定 EDM 创建 edm。 此方法需要最少的代码。 如果要对 EDM 进行更多的控制，可以使用**ODataModelBuilder**类来创建 edm，方法是显式添加属性、键和导航属性。

**EntitySet**方法将实体集添加到 EDM：

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

字符串 "Products" 定义实体集的名称。 控制器的名称必须与实体集的名称匹配。 在本教程中，实体集命名为 "Products"，控制器命名为 `ProductsController`。 如果已将该实体集命名为 "ProductSet"，则会将该控制器命名为 `ProductSetController`。 请注意，终结点可以有多个实体集。 为每个实体集调用**EntitySet&lt;t&gt;** ，并定义相应的控制器。

**MapODataRoute**方法为 OData 终结点添加路由。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

第一个参数是路由的友好名称。 你的服务的客户端看不到此名称。 第二个参数是终结点的 URI 前缀。 在给定此代码的情况下，Products 实体集的 URI 为 http://<em>hostname</em>/odata/Products。 你的应用程序可以有多个 OData 终结点。 对于每个终结点，调用<strong>MapODataRoute</strong>并提供唯一的路由名称和唯一的 URI 前缀。

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>播种数据库（可选）

在此步骤中，您将使用实体框架来为数据库提供一些测试数据。 此步骤是可选的，但它允许立即测试 OData 终结点。

从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“包管理器控制台”窗口中，输入以下命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

这会添加一个名为迁移的文件夹和一个名为 Configuration.cs 的代码文件。

![](creating-an-odata-endpoint/_static/image12.png)

打开此文件，并将以下代码添加到 `Configuration.Seed` 方法。

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

在 "程序包管理器控制台" 窗口中，输入以下命令：

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

这些命令生成用于创建数据库的代码，然后执行该代码。

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>浏览 OData 终结点

在本部分中，我们将使用[Fiddler Web 调试代理](http://www.fiddler2.com)将请求发送到终结点并检查响应消息。 这将帮助你了解 OData 终结点的功能。

在 Visual Studio 中，按 F5 开始调试。 默认情况下，Visual Studio 会打开浏览器以 `http://localhost:*port*`，其中*port*是在项目设置中配置的端口号。

可以在项目设置中更改端口号。 在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。 在 "属性" 窗口中，选择 " **Web**"。 在 "**项目 Url**" 下输入端口号。

### <a name="service-document"></a>服务文档

*服务文档*包含 OData 终结点的实体集的列表。 若要获取服务文档，请将 GET 请求发送到服务的根 URI。

使用 Fiddler 在 "**编辑器**" 选项卡中输入以下 URI： `http://localhost:port/odata/`，其中*port*是端口号。

![](creating-an-odata-endpoint/_static/image13.png)

单击 "**执行**" 按钮。 Fiddler 将 HTTP GET 请求发送到应用程序。 应会在 "Web 会话" 列表中看到响应。 如果一切正常，状态代码将为200。

![](creating-an-odata-endpoint/_static/image14.png)

双击 "Web 会话" 列表中的响应，查看 "检查器" 选项卡中响应消息的详细信息。

![](creating-an-odata-endpoint/_static/image15.png)

原始 HTTP 响应消息应如下所示：

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

默认情况下，Web API 以 AtomPub 格式返回服务文档。 若要请求 JSON，请将以下标头添加到 HTTP 请求：

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

现在 HTTP 响应包含 JSON 有效负载：

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>服务元数据文档

*服务元数据文档*使用名为概念架构定义语言（CSDL）的 XML 语言描述服务的数据模型。 元数据文档显示服务中数据的结构，并可用于生成客户端代码。

若要获取元数据文档，请将 GET 请求发送到 `http://localhost:port/odata/$metadata`。 下面是本教程中所示的终结点的元数据。

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>实体集

若要获取 Products 实体集，请将 GET 请求发送到 `http://localhost:port/odata/Products`。

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>实体

若要获取单个产品，请将 GET 请求发送到 `http://localhost:port/odata/Products(1)`，其中 "1" 是产品 ID。

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData 序列化格式

OData 支持多种序列化格式：

- Atom Pub （XML）
- JSON "light" （在 OData v3 中引入）
- JSON "verbose" （OData v2）

默认情况下，Web API 使用 AtomPubJSON "light" 格式。

若要获取 AtomPub 格式，请将 Accept 标头设置为 "application/atom + xml"。 下面是一个示例响应正文：

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

您可以看到 Atom 格式的一个明显缺点：它比 JSON 光更详细。 但是，如果你有一个了解 AtomPub 的客户端，则客户端可能更倾向于使用 JSON 格式。

下面是同一实体的 JSON 轻型版本：

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON 轻型格式是在 OData 协议版本3中引入的。 为实现向后兼容性，客户端可以请求较旧的 "详细" JSON 格式。 若要请求详细的 JSON，请将 Accept 标头设置为 `application/json;odata=verbose`。 下面是详细版本：

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

此格式将更多的元数据传递到响应正文中，这可能会在整个会话中产生相当大的开销。 此外，它还通过将对象包装在名为 "d" 的属性中来添加间接级别。

## <a name="next-steps"></a>后续步骤

- [添加实体关系](working-with-entity-relations.md)
- [添加 OData 操作](odata-actions.md)
- [从 .NET 客户端调用 OData 服务](calling-an-odata-service-from-a-net-client.md)
