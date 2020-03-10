---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中使用 EF 更新相关数据
description: 在本教程中，你将更新相关数据。 对于大多数关系，可以通过更新外键字段或导航属性来完成此操作。
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499298"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>教程：在 ASP.NET MVC 应用中使用 EF 更新相关数据

在上一教程中，您显示了相关数据。 在本教程中，你将更新相关数据。 对于大多数关系，可以通过更新外键字段或导航属性来完成此操作。 对于多对多关系，实体框架不会直接公开联接表，因此你可以在相应的导航属性中添加和删除实体。

下图是一些将会用到的页面。

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![讲师编辑课程](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

在本教程中，你将了解：

> [!div class="checklist"]
> * 自定义课程页面
> * 将 office 添加到讲师页
> * 向指导员页面添加课程
> * 更新 DeleteConfirmed
> * 向创建页添加办公室位置和课程

## <a name="prerequisites"></a>系统必备

* [读取相关数据](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>自定义课程页面

创建新的课程实体时，新实体必须与现有院系有关系。 为此，基架代码需包括控制器方法、创建视图和编辑视图，且视图中应包括用于选择院系的下拉列表。 下拉列表设置 `Course.DepartmentID` 外键属性，这就是用适当的 `Department` 实体加载 `Department` 导航属性所需的全部实体框架。 将用到基架代码，但需对其稍作更改，以便添加错误处理和对下拉列表进行排序。

在*CourseController.cs*中，删除四个 `Create` 和 `Edit` 方法，并将其替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

将以下 `using` 语句添加到文件的开头：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` 方法获取按名称排序的所有部门的列表，为下拉列表创建一个 `SelectList` 集合，并将该集合传递到 `ViewBag` 属性中的视图。 该方法可以使用可选的 `selectedDepartment` 参数，而调用的代码可以通过该参数来指定呈现下拉列表时被选择的项。 视图会将名称 `DepartmentID` 传递给[DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) helper，然后，帮助者知道在 `ViewBag` 对象中查找名为 `DepartmentID`的 `SelectList`。

`HttpGet` `Create` 方法调用 `PopulateDepartmentsDropDownList` 方法，而不设置所选的项，因为对于新课程，该部门尚未建立：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` 方法根据已分配给要编辑的课程的部门 ID 设置所选项目：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

`Create` 和 `Edit` 的 `HttpPost` 方法还包括在发生错误后重新显示该页时设置选定项的代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

此代码可确保在重新显示页面以显示错误消息时，选择的任何部门始终处于选中状态。

课程视图已基架 "部门" 字段的下拉列表，但不需要此字段的 DepartmentID 标题，因此，对*Views\Course\Create.cshtml*文件进行以下突出显示的更改以更改标题。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

在*Views\Course\Edit.cshtml*中进行相同的更改。

通常，scaffolder 不会基架主键，因为键值是由数据库生成的，不能更改，并且不是向用户显示的有意义的值。 对于课程实体，scaffolder 确实包括 `CourseID` 字段的文本框，因为它知道 `DatabaseGeneratedOption.None` 属性意味着用户应该能够输入主键值。 但它并不了解这一点，因为数字对于您想要在其他视图中看到的是有意义的，因此您需要手动添加它。

在*Views\Course\Edit.cshtml*中，在 "**标题**" 字段之前添加课程编号字段。 由于它是主键，因此将显示，但不能更改它。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

在 "编辑" 视图中，课程编号已经有一个隐藏字段（`Html.HiddenFor` 帮助程序）。 添加*html.labelfor*帮助程序不会消除隐藏字段的需要，因为当用户单击 "编辑" 页上的 "**保存**" 时，不会在已发布数据中包含课程编号。

在*Views\Course\Delete.cshtml*和*Views\Course\Details.cshtml*中，将部门名称标题从 "名称" 更改为 "部门"，然后在 "**标题**" 字段之前添加课程编号字段。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

运行 "**创建**" 页（显示 "课程索引" 页，单击 "**新建**"），然后为新课程输入数据：

| “值” | 设置 |
| ----- | ------- |
| 数字 | 输入*1000*。 |
| 标题 | 输入*代数*。 |
| 学分 | 输入*4*。 |
|Department | 选择 "**数学**"。 |

单击 **“创建”** 。 将显示 "课程索引" 页，新课程将添加到列表中。 索引页列表中的院系名称来自导航属性，表明已正确建立关系。

运行 "**编辑**" 页（显示 "课程索引" 页，然后单击 "**编辑**"）。

更改页面上的数据，然后单击“保存”。 将显示 "课程索引" 页和更新的课程数据。

## <a name="add-office-to-instructors-page"></a>将 office 添加到讲师页

编辑讲师记录时，有时希望能更新讲师的办公室分配。 `Instructor` 实体与 `OfficeAssignment` 实体之间存在一对零或一对多的关系，这意味着您必须处理以下情况：

- 如果用户清除办公室分配并且它最初具有值，则必须删除并删除 `OfficeAssignment` 实体。
- 如果用户输入 office 分配值并且它最初为空，则必须创建新的 `OfficeAssignment` 实体。
- 如果用户更改了 office 分配的值，则必须更改现有 `OfficeAssignment` 实体中的值。

打开*InstructorController.cs*并查看 `HttpGet` `Edit` 方法：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

此处的基架代码不是你所需的代码。 它为下拉列表设置数据，但您需要的是文本框。 将此方法替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

此代码删除 `ViewBag` 语句，并为关联的 `OfficeAssignment` 实体添加预先加载。 不能使用 `Find` 方法执行预先加载，因此使用 `Where` 和 `Single` 方法来选择讲师。

将 `HttpPost` `Edit` 方法替换为以下代码。 处理 office 分配更新的：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

对 `RetryLimitExceededException` 的引用需要 `using` 语句;若要添加它，请将鼠标悬停在 `RetryLimitExceededException`上。 将显示以下消息： "![ 重试异常消息](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

选择 "**显示潜在修补程序**，然后**使用**"

![解决重试异常](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

该代码执行以下操作：

- 将方法名称更改为 `EditPost`，因为签名现在与 `HttpGet` 方法相同（`ActionName` 特性指定仍使用/Edit/URL）。
- 使用 `Instructor` 导航属性的预先加载从数据库获取当前的 `OfficeAssignment` 实体。 这与您在 `HttpGet` `Edit` 方法中所执行的操作相同。
- 用模型绑定器中的值更新检索到的 `Instructor` 实体。 使用的[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx)重载使你能够将你要包括的属性*列入*允许列表。 这可以防止过度发布，如[第二个教程中所](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)述。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- 如果办公室位置为空，则将 `Instructor.OfficeAssignment` 属性设置为 null，以便删除 `OfficeAssignment` 表中的相关行。

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- 将更改保存到数据库。

在*Views\Instructor\Edit.cshtml*中，在 "**雇佣日期**" 字段的 `div` 元素之后，添加一个用于编辑办公室位置的新字段：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

运行页面（选择 "**讲师**" 选项卡，然后单击 "在讲师上**编辑**"）。 更改“办公室位置”，然后单击“保存”。

## <a name="add-courses-to-instructors-page"></a>向指导员页面添加课程

讲师可能教授任意数量的课程。 现在，你将通过添加使用一组复选框来更改课程分配的功能，来增强讲师编辑页面。

`Course` 和 `Instructor` 实体之间的关系是多对多，这意味着您不能直接访问联接表中的外键属性。 相反，您可以在 `Instructor.Courses` 导航属性中添加和移除实体。

用于更改讲师所对应的课程的 UI 是一组复选框。 该复选框中会显示数据库中的所有课程，选中讲师当前对应的课程即可。 用户可以通过选择或清除复选框来更改课程分配。 如果课程数量很大，您可能想要使用不同的方法来显示视图中的数据，但您可以使用相同的方法来处理导航属性，以便创建或删除关系。

若要为复选框列表的视图提供数据，将使用视图模型类。 在*viewmodel*文件夹中创建*AssignedCourseData.cs* ，并将现有代码替换为以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

在*InstructorController.cs*中，将 `HttpGet` `Edit` 方法替换为以下代码。 突出显示所作更改。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

该代码为 `Courses` 导航属性添加了预先加载，并调用新的 `PopulateAssignedCourseData` 方法使用 `AssignedCourseData` 视图模型类为复选框数组提供信息。

`PopulateAssignedCourseData` 方法中的代码读取所有 `Course` 实体，以便使用视图模型类加载课程列表。 对每门课程而言，该代码都会检查讲师的 `Courses` 导航属性中是否存在该课程。 若要在检查是否将课程分配给讲师时创建高效的查找，则分配给讲师的课程将被放入[HashSet](https://msdn.microsoft.com/library/bb359438.aspx)集合。 对于指定讲师的课程，`Assigned` 属性设置为 `true`。 视图将使用此属性来确定应将哪些复选框显示为选中状态。 最后，将列表传递到 `ViewBag` 属性中的视图。

接下来，添加用户单击“保存”时执行的代码。 将 `EditPost` 方法替换为以下代码，该代码调用更新 `Instructor` 实体的 `Courses` 导航属性的新方法。 突出显示所作更改。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

方法签名与 `HttpGet` `Edit` 方法不同，因此方法名称从 `EditPost` 返回到 `Edit`。

因为视图没有 `Course` 实体的集合，模型绑定器无法自动更新 `Courses` 导航属性。 你将在新的 `UpdateInstructorCourses` 方法中执行该操作，而不是使用模型联编程序来更新 `Courses` 导航属性。 为此，需要从模型绑定中排除 `Courses` 属性。 这不需要对调用[TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx)的代码进行任何更改，因为你使用的是*允许列表*重载，而 `Courses` 不在包含列表中。

如果未选择任何复选框，`UpdateInstructorCourses` 中的代码将使用空集合初始化 `Courses` 导航属性：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

之后，代码会循环访问数据库中的所有课程，并逐一检查当前分配给讲师的课程和视图中处于选中状态的课程。 为便于高效查找，后两个集合存储在 `HashSet` 对象中。

如果某课程的复选框处于选中状态，但该课程不在 `Instructor.Courses` 导航属性中，则会将该课程添加到导航属性中的集合中。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

如果某课程的复选框未处于选中状态，但该课程存在 `Instructor.Courses` 导航属性中，则会从导航属性中删除该课程。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

在*Views\Instructor\Edit.cshtml*中，通过将以下代码添加到 "`OfficeAssignment`" 字段的 `div` 元素之后，在 "**保存**" 按钮的 `div` 元素之前添加以下代码，添加一个包含复选框数组的 "**课程**" 字段：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

在粘贴代码后，如果分行符和缩进在此处看起来不像，请手动修复所有内容，使其看起来就像你在此处看到的内容。 缩进不一定要完美，但 `@</tr><tr>`、`@:<td>`、`@:</td>` 和 `@</tr>` 行必须各成一行（如下所示），否则会出现运行时错误。

此代码将创建一个具有三列的 HTML 表。 每个列中都有一个复选框，随后是一段由课程编号和标题组成的描述文字。 所有复选框都具有相同的名称（"selectedCourses"），这会通知模型绑定器将这些复选框视为组。 每个复选框的 `value` 属性都设置为页面发布时 `CourseID.` 的值，模型联编程序将一个数组传递到控制器，该控制器仅包含所选复选框的 `CourseID` 值。

最初呈现复选框时，分配给讲师的课程的这些复选框具有 `checked` 属性，这些属性将选择这些复选框（将其显示为选中状态）。

更改课程分配后，你需要能够在站点返回 `Index` 页面时验证所做的更改。 因此，您需要在该页面的表中添加一列。 在这种情况下，您无需使用 `ViewBag` 对象，因为您要显示的信息已位于作为模型传递到页面的 `Instructor` 实体的 `Courses` 导航属性中。

在*Views\Instructor\Index.cshtml*中，在 " **Office** " 标题后面添加一个**课程**标题，如以下示例中所示：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

然后，在 "办公室位置详细信息" 单元之后立即添加一个新的详细信息单元：

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

运行 "**讲师索引**" 页，查看分配给每个指导员的课程。

单击指导员上的 "**编辑**" 以查看 "编辑" 页。

更改某些课程分配，并单击 "**保存**"。 所作更改将反映在索引页上。

 注意：如果有有限数量的课程，此处用于编辑讲师课程数据的方法很有用。 若是远大于此的集合，则需要使用不同的 UI 和不同的更新方法。

## <a name="update-deleteconfirmed"></a>更新 DeleteConfirmed

在*InstructorController.cs*中，删除 `DeleteConfirmed` 方法并在其位置插入以下代码。

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

此代码进行以下更改：

- 如果将指导员指定为任何部门的管理员，则将从该部门中删除讲师分配。 如果不使用此代码，如果您尝试删除已分配为部门管理员的指导员，会出现引用完整性错误。

此代码不会处理一个以管理员身份分配给多个部门的指导员方案。 在上一教程中，您将添加代码以防止发生该方案。

## <a name="add-office-location-and-courses-to-the-create-page"></a>向创建页添加办公室位置和课程

在*InstructorController.cs*中，删除 `HttpGet` 并 `HttpPost` `Create` 方法，然后在其位置添加以下代码：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

此代码类似于您在编辑方法中看到的内容，但最初并未选择任何课程。 `HttpGet` `Create` 方法调用 `PopulateAssignedCourseData` 方法，这并不是因为可能选择了课程，但为了为视图中的 `foreach` 循环提供空集合（否则，视图代码将引发空引用异常）。

在用于检查验证错误并将新的指导员添加到数据库的模板代码之前，HttpPost Create 方法会将每个选定的课程添加到课程导航属性。 即使存在模型错误，也会添加课程，以便在出现模型错误时（例如，用户输入无效日期），以便在使用错误消息重新显示页面时，所做的任何课程选择都将自动还原。

请注意，为了能够向 `Courses` 导航属性添加课程，必须将该属性初始化为空集合：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

除了在控制器代码中进行此操作之外，还可以在“导师”模型中进行此操作，方法是将该属性更改为不存在集合时自动创建集合，如以下示例所示：

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

如果通过这种方式修改 `Courses` 属性，则可以删除控制器中的显式属性初始化代码。

在*Views\Instructor\Create.cshtml*中，在 "雇佣日期" 字段之后、"**提交**" 按钮之前添加 "办公室位置" 文本框和课程复选框。

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

在粘贴代码后，请按照之前对 "编辑" 页的操作修复分行符和缩进。

运行 "创建" 页并添加一个指导员。

<a id="transactions"></a>

## <a name="handling-transactions"></a>处理翻译

如[基本 CRUD 功能教程](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)中所述，默认情况下实体框架隐式实现事务。 对于需要更多控制的情况下（例如，如果想要包括在事务中的实体框架之外完成的操作），请参阅 MSDN 上的[使用事务](https://msdn.microsoft.com/data/dn456843)。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

## <a name="next-step"></a>下一步

在本教程中，你将了解：

> [!div class="checklist"]
> * 自定义课程页面
> * 已将 office 添加到讲师页
> * 向讲师页添加了课程
> * 已更新 DeleteConfirmed
> * 在 "创建" 页中添加了办公位置和课程

转到下一篇文章，了解如何实现异步编程模型。
> [!div class="nextstepaction"]
> [异步编程模型](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
