---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 第3部分：创建管理控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447908"
---
# <a name="part-3-creating-an-admin-controller"></a>第3部分：创建管理控制器

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>添加管理控制器

在本部分中，我们将添加一个 Web API 控制器，该控制器支持对产品的 CRUD （创建、读取、更新和删除）操作。 控制器将使用实体框架与数据库层进行通信。 只有管理员才能使用该控制器。 客户将通过另一控制器访问产品。

在解决方案资源管理器中，右键单击 "控制器" 文件夹。 依次选择 "**添加**" 和 "**控制器**"。

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

在 "**添加控制器**" 对话框中，将控制器命名为 `AdminController`。 在 "**模板**" 下，选择 "使用实体框架&quot;&quot;API 控制器，其中包含读/写操作。 在 "**模型类**" 下，选择 "Product （ProductStore）"。 在 "**数据上下文**" 下，选择 "&lt;新建数据上下文&gt;"。

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> 如果 "**模型类**" 下拉端未显示任何模型类，请确保已编译该项目。 实体框架使用反射，因此它需要已编译的程序集。

选择 "&lt;新的数据上下文&gt;" 将打开 "**新建数据上下文**" 对话框。 将数据上下文命名为 `ProductStore.Models.OrdersContext`。

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

单击 **"确定"** 以关闭 "**新建数据上下文**" 对话框。 在 "**添加控制器**" 对话框中，单击 "**添加**"。

下面是已添加到项目的内容：

- 从**DbContext**派生的名为 `OrdersContext` 的类。 此类提供 POCO 模型和数据库之间的粘附。
- 名为 `AdminController`的 Web API 控制器。 此控制器支持对 `Product` 实例的 CRUD 操作。 它使用 `OrdersContext` 类与实体框架通信。
- Web.config 文件中的新数据库连接字符串。

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

打开 OrdersContext.cs 文件。 请注意，构造函数指定了数据库连接字符串的名称。 此名称是指添加到 web.config 的连接字符串。

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

向 `OrdersContext` 类添加以下属性：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**DbSet**表示可查询的一组实体。 下面是 `OrdersContext` 类的完整列表：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` 类定义了五种实现基本 CRUD 功能的方法。 每个方法都对应于客户端可以调用的 URI：

| 控制器方法 | 说明 | URI | HTTP 方法 |
| --- | --- | --- | --- |
| GetProducts | 获取所有产品。 | api/产品 | GET |
| GetProduct | 按 ID 查找产品。 | api/产品/*id* | GET |
| PutProduct | 更新产品。 | api/产品/*id* | PUT |
| PostProduct | 创建新产品。 | api/产品 | POST |
| DeleteProduct | 删除产品。 | api/产品/*id* | DELETE |

每个方法都调用到 `OrdersContext` 来查询数据库。 修改集合（PUT、POST 和 DELETE）调用 `db.SaveChanges` 的方法将更改保存到数据库中。 控制器是根据每个 HTTP 请求创建的，然后被释放，因此，在方法返回之前需要保存更改。

## <a name="add-a-database-initializer"></a>添加数据库初始值设定项

实体框架具有一项不错的功能，可让你在启动时填充数据库，并在模型发生更改时自动重新创建数据库。 此功能在开发期间很有用，因为您始终会有一些测试数据，即使您更改了模型也是如此。

在解决方案资源管理器中，右键单击 "模型" 文件夹，然后创建一个名为 "`OrdersContextInitializer`" 的新类。 粘贴以下实现：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

通过从**DropCreateDatabaseIfModelChanges**类继承，我们会告诉实体框架在修改 model 类时删除数据库。 当实体框架创建（或重新创建）数据库时，它将调用**Seed**方法来填充表。 我们使用**Seed**方法添加一些示例产品和示例订单。

此功能非常适合测试，但请勿在生产中使用**DropCreateDatabaseIfModelChanges**类，因为如果有人更改了模型类，就会丢失数据。

接下来，打开 global.asax 并将以下代码添加到**应用程序\_Start**方法：

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>向控制器发送请求

此时，我们尚未编写任何客户端代码，但可以使用 web 浏览器或 HTTP 调试工具（如[Fiddler](http://www.fiddler2.com/fiddler2/)）来调用 web API。 在 Visual Studio 中，按 F5 开始调试。 Web 浏览器将打开以 `http://localhost:*portnum*/`，其中*portnum*是某个端口号。

向 "`http://localhost:*portnum*/api/admin`发送 HTTP 请求。 第一次请求可能会很慢，因为实体框架需要创建并播种数据库。 响应应类似于以下内容：

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-2.md)
> [下一页](using-web-api-with-entity-framework-part-4.md)
