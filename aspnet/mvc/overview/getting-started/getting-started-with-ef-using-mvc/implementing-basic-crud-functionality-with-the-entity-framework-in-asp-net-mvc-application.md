---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 教程：通过 ASP.NET MVC 中的实体框架实现 CRUD 功能 |Microsoft Docs
description: 查看并自定义 MVC 基架自动在控制器和视图中创建的创建、读取、更新、删除（CRUD）代码。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471146"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>教程：通过 ASP.NET MVC 中的实体框架实现 CRUD 功能

在[上一教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)中，你创建了一个 MVC 应用程序，它使用实体框架（EF）6和 SQL Server LocalDB 来存储和显示数据。 在本教程中，您将查看并自定义 MVC 基架在控制器和视图中为您自动创建的创建、读取、更新、删除（CRUD）代码。

> [!NOTE]
> 为了在控制器和数据访问层之间创建一个抽象层，常见的做法是实现存储库模式。 为了使这些教程更简单，重点介绍如何使用 EF 6 本身，它们不使用存储库。 有关如何实现存储库的信息，请参阅[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)。

下面是你创建的网页的示例：

![学生详细信息页的屏幕截图。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![学生 "创建" 页的屏幕截图。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![学生删除页的屏幕截图。](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建详细信息页
> * 更新“创建”页
> * 更新 HttpPost Edit 方法
> * 更新“删除”页
> * 关闭数据库连接
> * 处理事务

## <a name="prerequisites"></a>系统必备

* [创建实体框架数据模型](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>创建详细信息页

学生 `Index` 的 "基架" 代码页遗留了 `Enrollments` 属性，因为该属性包含一个集合。 在 "`Details`" 页中，将在 HTML 表中显示集合的内容。

在*Controllers\StudentController.cs*中，`Details` 视图的操作方法使用[Find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx)方法检索单个 `Student` 实体。

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

键值作为 `id` 参数传递给方法，并来自索引页上**详细信息**超链接中的*路由数据*。

### <a name="tip-route-data"></a>提示：**路由数据**

路由数据是模型绑定器在路由表中指定的 URL 段中找到的数据。 例如，默认路由指定 `controller`、`action`和 `id` 段：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

在下面的 URL 中，默认路由映射 `Instructor` 作为 `controller`，`Index` 作为 `action`，1作为 `id`;这些是路由数据值。

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` 是一个查询字符串值。 如果将 `id` 作为查询字符串值传递，则模型绑定器也起作用：

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Url 是通过 Razor 视图中 `ActionLink` 语句创建的。 在下面的代码中，`id` 参数与默认路由匹配，因此 `id` 添加到路由数据。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

在下面的代码中，`courseID` 与默认路由中的参数不匹配，因此将其添加为查询字符串。

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>创建详细信息页

1. 打开*Views\Student\Details.cshtml*。

   每个字段都使用 `DisplayFor` 帮助器来显示，如以下示例中所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. 在 "`EnrollmentDate`" 字段之后，在 "结束 `</dl>` 标记之前，添加突出显示的代码以显示注册列表，如以下示例中所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    如果代码缩进在粘贴代码后出现错误，请按**ctrl**+**K**， **ctrl**+**D**对其进行格式化。

    此代码循环通过 `Enrollments` 导航属性中的实体。 对于属性中的每个 `Enrollment` 实体，它显示课程标题和分数。 课程标题将从存储在 `Enrollments` 实体的 `Course` 导航属性中的 `Course` 实体中进行检索。 在需要时，将自动从数据库中检索所有数据。 换句话说，你在此处使用延迟加载。 你没有为 `Courses` 导航属性指定*预先加载*，因此无法在获得学生的同一查询中检索注册。 相反，第一次尝试访问 `Enrollments` 导航属性时，会将新查询发送到数据库以检索数据。 可以在本系列后面的[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中详细了解延迟加载和预先加载。

3. 通过启动程序（**Ctrl**+**F5**），选择 "**学生**" 选项卡，然后单击 "Alexander Carson" 的 "**详细信息**" 链接，打开 "详细信息" 页。 （如果在*详细信息 cshtml*文件处于打开状态时按**Ctrl**+**F5** ，则会收到 HTTP 400 错误。 这是因为 Visual Studio 将尝试运行详细信息页，但它不是从指定要显示的学生的链接访问的。 如果发生这种情况，请从 URL 中删除 "学生/详细信息" 并重试，或关闭浏览器，右键单击项目，然后单击 "查看**浏览器中**的 > 视图"。）

    你将看到所选学生的课程和成绩列表。

4. 关闭浏览器。

## <a name="update-the-create-page"></a>更新“创建”页

1. 在*Controllers\StudentController.cs*中，将 <xref:System.Web.Mvc.HttpPostAttribute> `Create` 操作方法替换为以下代码。 此代码将添加一个 `try-catch` 块，并从基架方法的 <xref:System.Web.Mvc.BindAttribute> 属性中删除 `ID`：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    此代码会将 ASP.NET MVC 模型联编程序创建的 `Student` 实体添加到 `Students` 实体集，然后将更改保存到数据库。 *模型联编*程序是指使你可以更轻松地使用窗体提交的数据的 ASP.NET MVC 功能;模型联编程序将已发布的窗体值转换为 CLR 类型，并将其传递给参数中的操作方法。 在这种情况下，模型联编程序会使用 `Form` 集合中的属性值实例化 `Student` 实体。

    您从 Bind 属性中删除了 `ID`，因为 `ID` 是在插入行时 SQL Server 将自动设置的主键值。 用户的输入未设置 `ID` 值。

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>安全警告-`ValidateAntiForgeryToken` 特性有助于防止[跨站点请求伪造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻击。 它需要视图中相应的 `Html.AntiForgeryToken()` 语句，稍后会看到。

    `Bind` 特性是防止在创建方案中*过度发布*的一种方法。 例如，假设 `Student` 实体包含不希望此网页设置的 `Secret` 属性。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    即使网页上没有 `Secret` 字段，黑客也可以使用[fiddler](http://fiddler2.com/home)之类的工具或编写一些 JavaScript 来发布 `Secret` 窗体值。 如果没有 <xref:System.Web.Mvc.BindAttribute> 特性限制模型绑定器在创建 `Student` 实例时使用的字段<em>，</em>则模型绑定器将选取该 `Secret` 窗体值，并使用它来创建 `Student` 实体实例。 然后将在数据库中更新黑客为 `Secret` 表单字段指定的任意值。 下图显示了 fiddler 工具，将 `Secret` 字段（值为 "OverPost"）添加到已发布的窗体值。

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    然后值“OverPost”将成功添加到插入行的 `Secret` 属性，尽管你从未打算网页可设置该属性。

    最好是使用`Include`参数与`Bind`归于*允许列表*字段 还有可能要使用`Exclude`参数*阻止列表*你想要排除的字段。 `Include` 更为安全的原因是：向实体添加新属性时，新字段不会由 `Exclude` 列表自动保护。

    在编辑方案中，可以防止过多发布从数据库中首先读取实体，然后调用 `TryUpdateModel`，并传入显式允许的属性列表。 这是在这些教程中使用的方法。

    阻止许多开发人员首选的过多发布的另一种方法是使用视图模型，而不是使用模型绑定的实体类。 仅包含想要在视图模型中更新的属性。 MVC 模型联编程序完成后，可以选择使用[AutoMapper](http://automapper.org/)等工具将视图模型属性复制到实体实例。 使用 db。条目，以将其状态设置为 "未更改"，然后设置 "属性" （"属性名称"）。视图模型中包含的每个实体属性上的 IsModified 为 true。 此方法同时适用于编辑和创建方案。

    除了 `Bind` 属性，`try-catch` 块是对基架代码的唯一更改。 如果保存更改时捕获到来自 <xref:System.Data.DataException> 的异常，则会显示一般错误消息。 有时 <xref:System.Data.DataException> 异常是由应用程序外部的某些内容而非编程错误引起的，因此建议用户再次尝试。 尽管在本示例中未实现，但生产质量应用程序会记录异常。 有关详细信息，请参阅[监视和遥测（使用 Azure 构建真实世界云应用）](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)中的“见解记录”部分。

    *Views\Student\Create.cshtml*中的代码与在*详细信息*中看到的代码类似，不同之处在于 `EditorFor` 和 `ValidationMessageFor` 帮助程序用于每个字段，而不是 `DisplayFor`。 相关代码如下：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create. cshtml*还包括 `@Html.AntiForgeryToken()`，该属性与控制器中的 `ValidateAntiForgeryToken` 属性结合使用，以帮助防止[跨站点请求伪造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻击。

    *Create cshtml*中不需要进行任何更改。

2. 通过启动该程序，选择 "**学生**" 选项卡，然后单击 "**新建**"，运行此页。

3. 输入名称和无效日期，并单击 "**创建**" 以查看错误消息。

    这是默认情况下获取的服务器端验证。 在后面的教程中，你将了解如何添加为客户端验证生成代码的属性。 以下突出显示的代码显示了**Create**方法中的模型验证检查。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. 将日期更改为有效的值并单击 **Create**，查看在 **Index** 页上显示的新学生。

5. 关闭浏览器。

## <a name="update-httppost-edit-method"></a>Update HttpPost Edit 方法

1. 将 <xref:System.Web.Mvc.HttpPostAttribute> `Edit` 操作方法替换为以下代码：

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > 在*Controllers\StudentController.cs*中，`HttpGet Edit` 方法（没有 `HttpPost` 特性的方法）使用 `Find` 方法来检索所选 `Student` 实体，如在 `Details` 方法中看到的那样。 不需要更改此方法。

   这些更改实现了一种安全最佳做法来防止[过多发布](#overpost)，scaffolder 生成了 `Bind` 属性，并将模型联编程序创建的实体添加到了带有修改标志的实体集。 不再建议使用该代码，因为 `Bind` 特性会清除未列在 `Include` 参数中的字段中的任何预先存在的数据。 将来，将更新 MVC 控制器 scaffolder，以使其不会为编辑方法生成 `Bind` 特性。

   新代码读取现有实体，并调用 <xref:System.Web.Mvc.Controller.TryUpdateModel%2A> 从已发布表单数据中的用户输入更新字段。 实体框架的自动更改跟踪设置实体上的[EntityState](<xref:System.Data.EntityState.Modified>)标志。 调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法时，<xref:System.Data.EntityState.Modified> 标志将导致实体框架创建 SQL 语句以更新数据库行。 将忽略[并发冲突](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)，并更新数据库行的所有列，包括用户未更改的列。 （后面的教程演示如何处理并发冲突，如果您只想在数据库中更新单个字段，则可以将实体设置为[EntityState](<xref:System.Data.EntityState.Unchanged>) ，并将各字段设置为[EntityState](<xref:System.Data.EntityState.Modified>)。）

   若要防止过多发布，"编辑" 页要更新的字段在 `TryUpdateModel` 参数中列入白名单。 目前没有要保护的额外字段，但是列出希望模型绑定器绑定的字段可确保以后将字段添加到数据模型时，它们将自动受到保护，直到明确将其添加到此处为止。

   由于这些更改，HttpPost Edit 方法的方法签名与 HttpGet edit 方法相同;因此，已将方法重命名为 EditPost。

   > [!TIP]
   >
   > **实体状态和附加方法和 SaveChanges 方法**
   >
   > 数据库上下文跟踪内存中的实体是否与数据库中相应的行同步，并且此信息确定调用 `SaveChanges` 方法时会发生的情况。 例如，将新实体传递到[Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)方法时，该实体的状态将设置为 `Added`。 然后，当调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法时，数据库上下文会发出一个 SQL `INSERT` 命令。
   >
   > 实体可能处于以下[状态](xref:System.Data.EntityState)之一：
   >
   > - `Added`。 数据库中尚不存在实体。 `SaveChanges` 方法必须发出 `INSERT` 语句。
   > - `Unchanged`。 不需要通过 `SaveChanges` 方法对此实体执行操作。 从数据库读取实体时，实体将从此状态开始。
   > - `Modified`。 已修改实体的部分或全部属性值。 `SaveChanges` 方法必须发出 `UPDATE` 语句。
   > - `Deleted`。 已标记该实体进行删除。 `SaveChanges` 方法必须发出 `DELETE` 语句。
   > - `Detached`。 数据库上下文未跟踪该实体。
   >
   > 在桌面应用程序中，通常会自动设置状态更改。 在桌面类型的应用程序中，您可以读取实体并对其某些属性值进行更改。 这将使其实体状态自动更改为 `Modified`。 然后，在调用 `SaveChanges`时，实体框架将生成一个 SQL `UPDATE` 语句，该语句只更新您更改的实际属性。
   >
   > Web 应用的断开连接特性不允许此连续序列。 在呈现页面后，将释放读取实体的[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 。 调用 `HttpPost` `Edit` 操作方法时，将发出新的请求，并且你具有[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)的新实例，因此你必须手动将实体状态设置为 `Modified.` 然后在调用 `SaveChanges`时，实体框架将更新数据库行的所有列，因为上下文无法知道你更改了哪些属性。
   >
   > 如果你希望 SQL `Update` 语句仅更新用户实际更改的字段，则可以通过某种方式（例如隐藏字段）保存原始值，以便在调用 `HttpPost` `Edit` 方法时可用。 然后，你可以使用原始值创建一个 `Student` 实体，使用该实体的原始版本调用 `Attach` 方法，将该实体的值更新为新值，然后调用 `SaveChanges.` 有关详细信息，请参阅[实体状态和 SaveChanges](/ef/ef6/saving/change-tracking/entity-state)和[本地数据](/ef/ef6/querying/local-data)。

   *Views\Student\Edit.cshtml*中的 HTML 和 Razor 代码与你在*Create. cshtml*中看到的代码相似，无需进行任何更改。

2. 通过启动该程序，选择 "**学生**" 选项卡，然后单击**编辑**超链接来运行该页面。

3. 更改某些数据并单击“保存”。 你将在 "索引" 页中看到已更改的数据。

4. 关闭浏览器。

## <a name="update-the-delete-page"></a>更新“删除”页

在*Controllers\StudentController.cs*中，<xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法的模板代码使用 `Find` 方法来检索所选 `Student` 实体，如在 `Details` 和 `Edit` 方法中看到的那样。 但是，若要在调用 `SaveChanges` 失败时实现自定义错误消息，请将部分功能添加到此方法及其相应的视图中。

正如所看到的更新和创建操作，删除操作需要两个操作方法。 为响应 GET 请求而调用的方法会显示一个视图，该视图使用户有机会批准或取消删除操作。 如果用户批准，则创建 POST 请求。 发生这种情况时，将调用 `HttpPost` `Delete` 方法，然后该方法实际执行删除操作。

将 `try-catch` 块添加到 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 方法，以处理更新数据库时可能发生的任何错误。 如果发生错误，则 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 方法将调用 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法，并向其传递指示发生错误的参数。 然后，<xref:System.Web.Mvc.HttpGetAttribute> `Delete` 方法将重新出现确认页面以及错误消息，使用户有机会取消或重试。

1. 将 <xref:System.Web.Mvc.HttpGetAttribute> `Delete` 操作方法替换为以下代码，该代码可管理错误报告：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    此代码接受一个[可选参数](https://msdn.microsoft.com/library/dd264739.aspx)，该参数指示在保存更改失败后是否调用了方法。 如果在没有以前的失败的情况下调用 `HttpGet` `Delete` 方法，则 `false` 此参数。 当 `Delete` 方法 `HttpPost` 调用此方法以响应数据库更新错误时，该参数将 `true`，并向视图传递一条错误消息。

2. 将 <xref:System.Web.Mvc.HttpPostAttribute> `Delete` 操作方法（名为 `DeleteConfirmed`）替换为以下代码，这将执行实际的 delete 操作并捕获任何数据库更新错误。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    此代码检索所选的实体，然后调用[Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)方法，将实体的状态设置为 `Deleted`。 调用 `SaveChanges` 时，将生成 SQL `DELETE` 命令。 你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。 `HttpPost` 的名为的基架代码 `Delete` 方法 `DeleteConfirmed` 为 `HttpPost` 方法指定唯一签名。 （CLR 要求重载方法具有不同的方法参数。）签名是唯一的，可以坚持使用 MVC 约定，并为 `HttpPost` 和 `HttpGet` delete 方法使用相同的名称。

    如果提高大容量应用程序的性能是优先考虑的，则可以通过使用以下代码替换调用 `Find` 和 `Remove` 方法的代码行来避免不必要的 SQL 查询来检索行：

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    此代码仅使用主键值实例化一个 `Student` 实体，然后将实体状态设置为 `Deleted`。 这是 Entity Framework 删除实体需要执行的所有操作。

    如上所述，`HttpGet` `Delete` 方法不会删除数据。 执行删除操作以响应 GET 请求（或者，执行任何编辑操作、创建操作或更改数据的任何其他操作）会产生安全风险。 有关详细信息，请参阅[ASP.NET MVC Tip #46 —不要使用 "删除链接"，因为它们](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)在 Stephen Walther 的博客上创建安全漏洞。

3. 在*Views\Student\Delete.cshtml*中，在 `h2` 标题和 `h3` 标题之间添加一条错误消息，如以下示例中所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. 通过启动该程序，选择 "**学生**" 选项卡，然后单击 "**删除**" 超链接来运行该页面。

5. 在指出**是否确实要删除此**内容的页面上选择 "**删除**"。

    将显示 "索引" 页，其中没有已删除的学生。 （在[并发教程](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)中，你将看到一个用于操作的错误处理代码示例。）

## <a name="close-database-connections"></a>关闭数据库连接

若要关闭数据库连接并尽可能快地释放它们所占用的资源，请在完成后释放上下文实例。 这就是基架代码在*StudentController.cs*中 `StudentController` 类末尾提供[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法的原因，如以下示例中所示：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

基本 `Controller` 类已经实现了 `IDisposable` 接口，因此此代码只需将重写添加到 `Dispose(bool)` 方法以显式释放上下文实例。

## <a name="handle-transactions"></a>处理事务

默认情况下，Entity Framework 隐式实现事务。 如果对多个行或表进行了更改，然后调用 `SaveChanges`，实体框架将自动确保所有更改都成功或全部失败。 如果完成某些更改后发生错误，这些更改会自动回退。 对于需要更多控制&mdash;的情况，例如，如果想要包括在事务中的实体框架之外完成的操作&mdash;参阅使用[事务](/ef/ef6/saving/transactions)。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

现在，可以使用一组完整的页来执行 `Student` 实体的简单 CRUD 操作。 你使用了 MVC 帮助器来生成数据字段的 UI 元素。 有关 MVC 帮助器的详细信息，请参阅[使用 HTML 帮助器呈现表单](/previous-versions/aspnet/dd410596(v=vs.98))（这篇文章适用于 mvc 3，但对于 mvc 5 仍适用）。

可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他 EF 6 资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建了详细信息页
> * 已更新“创建”页
> * 更新了 HttpPost Edit 方法
> * 已更新“删除”页
> * 已关闭数据库连接
> * 处理的事务

转到下一篇文章，了解如何向项目添加排序、筛选和分页。
> [!div class="nextstepaction"]
> [排序、筛选和分页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
