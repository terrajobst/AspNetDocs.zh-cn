---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中将 async 和存储过程与 EF 配合使用
description: 在本教程中，您将了解如何实现异步编程模型并了解如何使用存储过程。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471386"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>教程：在 ASP.NET MVC 应用中将 async 和存储过程与 EF 配合使用

在前面的教程中，您学习了如何使用同步编程模型读取和更新数据。 在本教程中，您将了解如何实现异步编程模型。 异步代码有助于提高应用程序的性能，因为它可以更好地利用服务器资源。

在本教程中，你还将了解如何在实体上使用存储过程执行插入、更新和删除操作。

最后，将应用程序重新部署到 Azure，以及自首次部署后实现的所有数据库更改。

下图是一些将会用到的页面。

![部门页面](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![创建部门](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 了解异步代码
> * 创建部门控制器
> * 使用存储过程
> * 部署到 Azure

## <a name="prerequisites"></a>系统必备

* [更新相关数据](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>为什么使用异步代码

Web 服务器的可用线程是有限的，而在高负载情况下的可能所有线程都被占用。 当发生这种情况的时候，服务器就无法处理新请求，直到线程被释放。 使用同步代码时，可能会出现多个线程被占用但不能执行任何操作的情况，因为它们正在等待 I/O 完成。 使用异步代码时，当进程正在等待 I/O 完成，服务器可以将其线程释放用于处理其他请求。 因此，异步代码使服务器资源的使用效率更高，并使服务器能够处理更多的流量，而无需延迟。

在较早版本的 .NET 中，编写和测试异步代码非常复杂、容易出错且难以调试。 在 .NET 4.5 中，编写、测试和调试异步代码非常简单，通常应该编写异步代码，除非您有理由不这样做。 异步代码会引入少量的开销，但对于低流量情况，性能下降可能会忽略不计，而在高流量情况下，可能会显著提高性能。

有关异步编程的详细信息，请参阅[使用 .net 4.5 的异步支持以避免阻止调用](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)。

## <a name="create-department-controller"></a>创建部门控制器

使用与之前相同的控制器相同的方式创建部门控制器，但这次请选择 "**使用异步控制器操作**" 复选框。

以下突出显示了向同步代码添加的 `Index` 方法的同步代码，以使其实现异步操作：

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

应用了四项更改，使实体框架的数据库查询异步执行：

- 方法标记有 `async` 关键字，该关键字告诉编译器为方法体的各部分生成回调并自动创建返回的 `Task<ActionResult>` 对象。
- 返回类型已从 `ActionResult` 更改为 `Task<ActionResult>`。 `Task<T>` 类型表示正在进行的工作与类型 `T`的结果。
- `await` 关键字已应用于 web 服务调用。 当编译器在幕后看到此关键字时，它会将方法拆分为两个部分。 第一个部分以异步方式启动的操作结束。 第二部分放入回调方法，该方法将在操作完成时调用。
- 调用 `ToList` 扩展方法的异步版本。

为什么 `departments.ToList` 语句已修改但不是 `departments = db.Departments` 语句？ 原因在于，只有导致查询或命令发送到数据库的语句以异步方式执行。 `departments = db.Departments` 语句设置查询，但在调用 `ToList` 方法之前不会执行查询。 因此，仅异步执行 `ToList` 方法。

在 `Details` 方法和 `HttpGet` `Edit` 和 `Delete` 方法中，`Find` 方法是导致查询发送到数据库的方法，因此这是异步执行的方法：

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

在 `Create`、`HttpPost Edit`和 `DeleteConfirmed` 方法中，这是导致执行命令的 `SaveChanges` 方法调用，而不是仅导致内存中的实体被修改的语句（例如 `db.Departments.Add(department)`）。

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

打开*Views\Department\Index.cshtml*，将模板代码替换为以下代码：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

此代码会将标题从 "索引" 更改为 "部门"，将管理员名称移动到右侧，并提供管理员的全名。

在 "创建"、"删除"、"详细信息" 和 "编辑" 视图中，将 "`InstructorID`" 字段的标题更改为 "Administrator"，这与在课程视图中将 "部门名称" 字段更改为 "部门" 的方式相同。

在 "创建" 和 "编辑" 视图中，使用以下代码：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

在 "删除" 和 "详细信息" 视图中，使用以下代码：

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

运行应用程序，然后单击 "**部门**" 选项卡。

一切与其他控制器中的工作方式相同，但在此控制器中，所有 SQL 查询都以异步方式执行。

使用实体框架的异步编程时需要注意的一些事项：

- 异步代码不是线程安全的。 换言之，换言之，不要尝试使用同一个上下文实例并行执行多个操作。
- 如果你想要利用异步代码的性能优势，请确保你所使用的任何库和包在它们调用导致 Entity Framework 数据库查询方法时也使用异步。

## <a name="use-stored-procedures"></a>使用存储过程

某些开发人员和 Dba 更喜欢使用存储过程来访问数据库。 在的早期版本中实体框架可以通过[执行原始 SQL 查询](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)来检索数据，但不能指示 EF 使用存储过程进行更新操作。 在 EF 6 中，可以轻松地将 Code First 配置为使用存储过程。

1. 在*DAL\SchoolContext.cs*中，将突出显示的代码添加到 `OnModelCreating` 方法。

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    此代码指示实体框架在 `Department` 实体上使用存储过程执行插入、更新和删除操作。
2. 在 "包管理控制台" 中，输入以下命令：

    `add-migration DepartmentSP`

    打开*迁移\\&lt;时间戳&gt;\_DepartmentSP.cs*查看创建 Insert、Update 和 Delete 存储过程的 `Up` 方法中的代码：

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. 在 "包管理控制台" 中，输入以下命令：

     `update-database`
4. 在调试模式下运行应用程序，单击 "**部门**" 选项卡，然后单击 "**新建**"。
5. 为新部门输入数据，然后单击 "**创建**"。

6. 在 Visual Studio 中，查看 "**输出**" 窗口中的日志，以查看是否已使用存储过程插入新的 "部门" 行。

     ![部门插入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First 创建默认存储过程名称。 如果使用的是现有数据库，则可能需要自定义存储过程的名称，以使用数据库中已定义的存储过程。 有关如何执行此操作的信息，请参阅[实体框架 Code First 插入/更新/删除存储过程](https://msdn.microsoft.com/data/dn468673)。

如果要自定义生成的存储过程的功能，则可以编辑基架代码，以便 `Up` 方法创建存储过程。 这样一来，每当运行迁移时，所做的更改都会反映出来，并将在部署后在生产环境中自动运行时应用于生产数据库。

如果要更改在以前的迁移过程中创建的现有存储过程，则可以使用 "添加-迁移" 命令生成空白迁移，然后手动编写调用[AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)方法的代码。

## <a name="deploy-to-azure"></a>部署到 Azure

本部分要求你已完成本系列的[迁移和部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中的可选将**应用部署到 Azure**部分。 如果已通过删除本地项目中的数据库解决了迁移错误，请跳过此部分。

1. 在 Visual Studio 中，在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”。
2. 单击“发布”。

    Visual Studio 将应用程序部署到 Azure，并在默认浏览器中打开应用程序，该应用程序在 Azure 中运行。
3. 测试应用程序以验证其是否正常工作。

    首次运行访问数据库的页时，实体框架将运行所需的所有迁移 `Up` 方法，使数据库与当前数据模型保持最新。 你现在可以使用自上次部署以来添加的所有网页，包括你在本教程中添加的部门页面。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 了解异步代码
> * 创建了部门控制器
> * 使用的存储过程
> * 部署到 Azure

转到下一篇文章，了解当多个用户同时更新同一实体时如何处理冲突。
> [!div class="nextstepaction"]
> [处理并发](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
