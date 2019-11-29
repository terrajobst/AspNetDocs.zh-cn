---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 通过 ASP.NET MVC 应用程序中的实体框架实现基本的 CRUD 功能（第2个，共10个） |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595327"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>通过 ASP.NET MVC 应用程序中的实体框架实现基本的 CRUD 功能（第2项，共10个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载完成的项目](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 你可以从头开始学习本系列教程，也可以从此处[下载入门项目](building-the-ef5-mvc4-chapter-downloads.md)。
> 
> > [!NOTE] 
> > 
> > 如果遇到无法解决的问题，请[下载已完成的章节](building-the-ef5-mvc4-chapter-downloads.md)并尝试重现你的问题。 通常可以通过将代码与已完成的代码进行比较，查找问题的解决方案。 有关一些常见错误以及如何解决这些错误，请参阅[错误和解决方法。](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

在上一教程中，你创建了一个 MVC 应用程序，它使用实体框架和 SQL Server LocalDB 来存储和显示数据。 在本教程中，您将查看并自定义 MVC 基架在控制器和视图中为您自动创建的 CRUD （创建、读取、更新和删除）代码。

> [!NOTE]
> 为了在控制器和数据访问层之间创建一个抽象层，常见的做法是实现存储库模式。 为了简单起见，在本系列的后续教程中，你将不会实现存储库。

在本教程中，你将创建以下网页：

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>创建详细信息页

学生 `Index` 的 "基架" 代码页遗留了 `Enrollments` 属性，因为该属性包含一个集合。 在 "`Details`" 页中，将在 HTML 表中显示集合的内容。

 在*Controllers\StudentController.cs*中，`Details` 视图的操作方法使用 `Find` 方法检索单个 `Student` 实体。 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 键值作为 `id` 参数传递给方法，并来自索引页上**详细信息**超链接中的路由数据。 

1. 打开*Views\Student\Details.cshtml*。 每个字段都使用 `DisplayFor` 帮助器来显示，如以下示例中所示： 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. 在 "`EnrollmentDate`" 字段之后，在 "结束 `fieldset` 标记之前，添加代码以显示注册列表，如以下示例中所示：

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    此代码循环通过 `Enrollments` 导航属性中的实体。 对于属性中的每个 `Enrollment` 实体，它显示课程标题和分数。 课程标题将从存储在 `Enrollments` 实体的 `Course` 导航属性中的 `Course` 实体中进行检索。 在需要时，将自动从数据库中检索所有数据。 （换言之，在此处使用延迟加载。 你没有为 `Courses` 导航属性指定*预先加载*，因此首次尝试访问该属性时，会将查询发送到数据库以检索数据。 你可以在本系列后面的[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中详细了解延迟加载和预先加载。）
3. 选择 "**学生**" 选项卡，然后单击 "Alexander Carson" 的 "**详细信息**" 链接，运行页面。 将看到所选学生的课程和年级列表：

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>更新 "创建" 页

1. 在*Controllers\StudentController.cs*中，将 `HttpPost``Create` 操作方法替换为以下代码，以将 `try-catch` 块和[Bind 特性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)添加到基架方法： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    此代码会将 ASP.NET MVC 模型联编程序创建的 `Student` 实体添加到 `Students` 实体集，然后将更改保存到数据库。 （*模型绑定*器是指使你可以更轻松地处理窗体提交的数据的 ASP.NET MVC 功能; 模型联编程序将已发布的表单值转换为 CLR 类型，并将其传递给参数中的操作方法。 在这种情况下，模型绑定器使用 `Form` 集合中的属性值实例化 `Student` 实体。）

    `ValidateAntiForgeryToken` 特性有助于防止[跨站点请求伪造](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md)攻击。

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. 选择 "**学生**" 选项卡，然后单击 "**新建**"，运行页面。

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    默认情况下，某些数据验证起作用。 输入名称和无效日期，并单击 "**创建**" 以查看错误消息。

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    以下突出显示的代码显示了模型验证检查。

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    将日期更改为有效的值（例如9/1/2005），然后单击 "**创建**" 以查看新学生出现在 "**索引**" 页中。

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>更新编辑帖子页面

在*Controllers\StudentController.cs*中，`HttpGet` `Edit` 方法（没有 `HttpPost` 特性的方法）使用 `Find` 方法来检索所选 `Student` 实体，正如你在 `Details` 方法中看到的那样。 不需要更改此方法。

但是，将 `HttpPost` `Edit` 操作方法替换为以下代码，以添加 `try-catch` 块和[Bind 特性](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

此代码类似于您在 `HttpPost` `Create` 方法中看到的内容。 但是，此代码不会将模型联编程序创建的实体添加到实体集，而是在实体上设置一个标志，指示该实体已更改。 调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法时，[修改后](https://msdn.microsoft.com/library/system.data.entitystate.aspx)的标志将导致实体框架创建 SQL 语句以更新数据库行。 将更新数据库行的所有列，包括用户未更改的列，并忽略并发冲突。 （你将在本系列的后续教程中了解如何处理并发。）

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>实体状态和附加方法和 SaveChanges 方法

数据库上下文跟踪内存中的实体是否与数据库中相应的行同步，并且此信息确定调用 `SaveChanges` 方法时会发生的情况。 例如，将新实体传递到[Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx)方法时，该实体的状态将设置为 `Added`。 然后，当调用[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法时，数据库上下文会发出一个 SQL `INSERT` 命令。

实体可能处于[以下状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)之一：

- `Added`。 数据库中尚不存在实体。 `SaveChanges` 方法必须发出 `INSERT` 语句。
- `Unchanged`。 不需要通过 `SaveChanges` 方法对此实体执行操作。 从数据库读取实体时，实体将从此状态开始。
- `Modified`。 已修改实体的部分或全部属性值。 `SaveChanges` 方法必须发出 `UPDATE` 语句。
- `Deleted`。 已标记该实体进行删除。 `SaveChanges` 方法必须发出 `DELETE` 语句。
- `Detached`。 数据库上下文未跟踪该实体。

在桌面应用程序中，通常会自动设置状态更改。 在桌面类型的应用程序中，您可以读取实体并对其某些属性值进行更改。 这将使其实体状态自动更改为 `Modified`。 然后，在调用 `SaveChanges`时，实体框架将生成一个 SQL `UPDATE` 语句，该语句只更新您更改的实际属性。

Web 应用的断开连接特性不允许此连续序列。 在呈现页面后，将释放读取实体的[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) 。 调用 `HttpPost` `Edit` 操作方法时，将发出新的请求，并且你具有[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)的新实例，因此你必须手动将实体状态设置为 `Modified.` 然后在调用 `SaveChanges`时，实体框架将更新数据库行的所有列，因为上下文无法知道你更改了哪些属性。

如果你希望 SQL `Update` 语句仅更新用户实际更改的字段，则可以通过某种方式（例如隐藏字段）保存原始值，以便在调用 `HttpPost` `Edit` 方法时可用。 然后，你可以使用原始值创建一个 `Student` 实体，使用该实体的原始版本调用 `Attach` 方法，将该实体的值更新为新值，然后调用 `SaveChanges.` 有关详细信息，请参阅 MSDN 数据开发中心中的[实体状态和 SaveChanges](https://msdn.microsoft.com/data/jj592676)和[本地数据](https://msdn.microsoft.com/data/jj592872)。

*Views\Student\Edit.cshtml*中的代码类似于你在*Create. cshtml*中看到的内容，不需要进行任何更改。

选择 "**学生**" 选项卡，然后单击 "**编辑**" 超链接，运行页面。

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

更改某些数据并单击“保存”。 你将在 "索引" 页中看到已更改的数据。

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>更新 "删除" 页

在*Controllers\StudentController.cs*中，`HttpGet` `Delete` 方法的模板代码使用 `Find` 方法来检索所选 `Student` 实体，如在 `Details` 和 `Edit` 方法中看到的那样。 但是，若要在调用 `SaveChanges` 失败时实现自定义错误消息，请将部分功能添加到此方法及其相应的视图中。

正如所看到的更新和创建操作，删除操作需要两个操作方法。 为响应 GET 请求而调用的方法会显示一个视图，该视图使用户有机会批准或取消删除操作。 如果用户批准，则创建 POST 请求。 发生这种情况时，将调用 `HttpPost` `Delete` 方法，然后该方法实际执行删除操作。

将 `try-catch` 块添加到 `HttpPost` `Delete` 方法，以处理更新数据库时可能发生的任何错误。 如果发生错误，则 `HttpPost` `Delete` 方法将调用 `HttpGet` `Delete` 方法，并向其传递指示发生错误的参数。 然后，`HttpGet Delete` 方法将重新出现确认页面以及错误消息，从而向用户提供取消或重试的机会。

1. 将 `HttpGet` `Delete` 操作方法替换为以下代码，该代码可管理错误报告： 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    此代码接受一个[可选](https://msdn.microsoft.com/library/dd264739.aspx)的布尔参数，该参数指示在保存更改失败后是否调用了它。 如果在没有以前的失败的情况下调用 `HttpGet` `Delete` 方法，则 `false` 此参数。 当 `Delete` 方法 `HttpPost` 调用此方法以响应数据库更新错误时，该参数将 `true`，并向视图传递一条错误消息。
2. 将 `HttpPost` `Delete` 操作方法（名为 `DeleteConfirmed`）替换为以下代码，这将执行实际的 delete 操作并捕获任何数据库更新错误。

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     此代码检索所选的实体，然后调用[Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx)方法，将实体的状态设置为 `Deleted`。 调用 `SaveChanges` 时，将生成 SQL `DELETE` 命令。 你还将操作方法名称从 `DeleteConfirmed` 更改为了 `Delete`。 `HttpPost` 的名为的基架代码 `Delete` 方法 `DeleteConfirmed` 为 `HttpPost` 方法指定唯一签名。 （CLR 要求重载方法具有不同的方法参数。）签名是唯一的，可以坚持使用 MVC 约定，并为 `HttpPost` 和 `HttpGet` delete 方法使用相同的名称。

     如果在大容量应用程序中提高性能是一项优先级，则可以通过将调用 `Find` 的代码行替换为下面的代码并将其 `Remove` 方法替换为以下代码，从而避免不必要的 SQL 查询：

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     此代码仅使用主键值实例化一个 `Student` 实体，然后将实体状态设置为 `Deleted`。 这是 Entity Framework 删除实体需要执行的所有操作。

     如上所述，`HttpGet` `Delete` 方法不会删除数据。 执行删除操作以响应 GET 请求（或者，执行任何编辑操作、创建操作或更改数据的任何其他操作）会产生安全风险。 有关详细信息，请参阅[ASP.NET MVC Tip #46 —不要使用 "删除链接"，因为它们](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx)在 Stephen Walther 的博客上创建安全漏洞。
3. 在*Views\Student\Delete.cshtml*中，在 `h2` 标题和 `h3` 标题之间添加一条错误消息，如以下示例中所示：

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     通过选择 "**学生**" 选项卡并单击 "**删除**" 超链接来运行页面：

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. 单击“删除”。 将显示不含已删除学生的索引页。 （你将在本系列后面的[处理并发](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程中看到一个操作中的错误处理代码示例。）

## <a name="ensuring-that-database-connections-are-not-left-open"></a>确保数据库连接未处于打开状态

若要确保数据库连接正常关闭并释放它们所占用的资源，您应该看到已释放上下文实例的数据库连接。 这就是基架代码在*StudentController.cs*中 `StudentController` 类末尾提供[Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx)方法的原因，如以下示例中所示：

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

基本 `Controller` 类已经实现了 `IDisposable` 接口，因此此代码只需将重写添加到 `Dispose(bool)` 方法以显式释放上下文实例。

## <a name="summary"></a>总结

现在，可以使用一组完整的页来执行 `Student` 实体的简单 CRUD 操作。 你使用了 MVC 帮助器来生成数据字段的 UI 元素。 有关 MVC 帮助器的详细信息，请参阅[使用 HTML 帮助器呈现窗体](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx)（此页面适用于 mvc 3，但仍与 mvc 4 相关）。

在下一教程中，您将通过添加排序和分页来扩展 "索引" 页的功能。

可在[ASP.NET 数据访问内容映射](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

> [!div class="step-by-step"]
> [上一页](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [下一页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
