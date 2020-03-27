---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 将 JQuery UI Datepicker 与模型绑定和 web 窗体集成 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521978"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a><span data-ttu-id="1e895-104">将 JQuery UI Datepicker 与模型绑定和 web 窗体集成</span><span class="sxs-lookup"><span data-stu-id="1e895-104">Integrating JQuery UI Datepicker with model binding and web forms</span></span>

<span data-ttu-id="1e895-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1e895-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1e895-106">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="1e895-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="1e895-107">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="1e895-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="1e895-108">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="1e895-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="1e895-109">本教程演示如何将 JQuery UI [Datepicker 小组件](http://jqueryui.com/datepicker/)添加到 Web 窗体，并使用模型绑定来更新具有所选值的数据库。</span><span class="sxs-lookup"><span data-stu-id="1e895-109">This tutorial shows how to add the JQuery UI [Datepicker widget](http://jqueryui.com/datepicker/) to a Web Form, and use model binding to update the database with the selected value.</span></span>
> 
> <span data-ttu-id="1e895-110">本教程基于在序列的[第一个](retrieving-data.md)和[第二个](updating-deleting-and-creating-data.md)部分中创建的项目构建。</span><span class="sxs-lookup"><span data-stu-id="1e895-110">This tutorial builds on the project created in the [first](retrieving-data.md) and [second](updating-deleting-and-creating-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="1e895-111">可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="1e895-111">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="1e895-112">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1e895-112">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="1e895-113">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="1e895-113">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="1e895-114">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="1e895-114">What you'll build</span></span>

<span data-ttu-id="1e895-115">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="1e895-115">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="1e895-116">向模型添加属性以记录学生的注册日期</span><span class="sxs-lookup"><span data-stu-id="1e895-116">Add a property to your model to record the student's enrollment date</span></span>
2. <span data-ttu-id="1e895-117">允许用户使用 JQuery UI Datepicker 小组件选择注册日期</span><span class="sxs-lookup"><span data-stu-id="1e895-117">Enable the user to select the enrollment date using the JQuery UI Datepicker widget</span></span>
3. <span data-ttu-id="1e895-118">强制执行注册日期的验证规则</span><span class="sxs-lookup"><span data-stu-id="1e895-118">Enforce validation rules for the enrollment date</span></span>

<span data-ttu-id="1e895-119">使用 JQuery UI Datepicker 小组件，用户可以轻松地从日历中选择一个日期，该日期在用户与字段交互时弹出。</span><span class="sxs-lookup"><span data-stu-id="1e895-119">The JQuery UI Datepicker widget enables users to easily select a date from a calendar that pops up when the user interacts with the field.</span></span> <span data-ttu-id="1e895-120">与手动键入日期相比，使用此小组件的用户可以更方便地使用此小组件。</span><span class="sxs-lookup"><span data-stu-id="1e895-120">Using this widget can be more convenient for users than manually typing a date.</span></span> <span data-ttu-id="1e895-121">将 Datepicker 小组件集成到用于数据操作的模型绑定的页面只需少量的额外工作。</span><span class="sxs-lookup"><span data-stu-id="1e895-121">Integrating the Datepicker widget into a page that uses model binding for data operations requires only a small amount of additional work.</span></span>

## <a name="add-a-new-property-to-the-model"></a><span data-ttu-id="1e895-122">向模型添加新属性</span><span class="sxs-lookup"><span data-stu-id="1e895-122">Add a new property to the model</span></span>

<span data-ttu-id="1e895-123">首先，将 "**日期时间**" 属性添加到 "学生模型"，并将该更改迁移到数据库。</span><span class="sxs-lookup"><span data-stu-id="1e895-123">First, you will add a **Datetime** property to your Student model and migrate that change to the database.</span></span> <span data-ttu-id="1e895-124">打开**UniversityModels.cs**，并将突出显示的代码添加到 "学生" 模型。</span><span class="sxs-lookup"><span data-stu-id="1e895-124">Open **UniversityModels.cs**, and add the highlighted code to the Student model.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

<span data-ttu-id="1e895-125">包含**RangeAttribute**来强制执行属性的验证规则。</span><span class="sxs-lookup"><span data-stu-id="1e895-125">The **RangeAttribute** is included to enforce validation rules for the property.</span></span> <span data-ttu-id="1e895-126">对于本教程，我们假定 Contoso 大学在2013年1月1日成立，因此更早的注册日期无效。</span><span class="sxs-lookup"><span data-stu-id="1e895-126">For this tutorial, we will assume that Contoso University was founded on January 1st, 2013 and therefore earlier enrollment dates are not valid.</span></span>

<span data-ttu-id="1e895-127">在 "包管理" 窗口中，通过运行**AddEnrollmentDate**命令添加迁移。</span><span class="sxs-lookup"><span data-stu-id="1e895-127">In the Package Management window, add a migration by running the command **add-migration AddEnrollmentDate**.</span></span> <span data-ttu-id="1e895-128">请注意，迁移代码会将新的 Datetime 列添加到 Student 表中。</span><span class="sxs-lookup"><span data-stu-id="1e895-128">Notice that the migration code adds the new Datetime column to the Student table.</span></span> <span data-ttu-id="1e895-129">若要匹配在 RangeAttribute 中指定的值，请为新列添加默认值，如下面突出显示的代码所示。</span><span class="sxs-lookup"><span data-stu-id="1e895-129">To match the value you specified in the RangeAttribute, add a default value for the new column, as shown in the highlighted code below.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

<span data-ttu-id="1e895-130">保存对迁移文件的更改。</span><span class="sxs-lookup"><span data-stu-id="1e895-130">Save your change to the migration file.</span></span>

<span data-ttu-id="1e895-131">无需再次对数据进行种子设定。</span><span class="sxs-lookup"><span data-stu-id="1e895-131">You do not need to seed the data again.</span></span> <span data-ttu-id="1e895-132">因此，请在 "迁移" 文件夹中打开**Configuration.cs** ，删除或注释掉**Seed**方法中的代码。</span><span class="sxs-lookup"><span data-stu-id="1e895-132">Therefore, open **Configuration.cs** in the Migrations folder and remove or comment out the code in the **Seed** method.</span></span> <span data-ttu-id="1e895-133">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="1e895-133">Save and close the file.</span></span>

<span data-ttu-id="1e895-134">现在，运行命令**更新-数据库**。</span><span class="sxs-lookup"><span data-stu-id="1e895-134">Now, run the command **update-database**.</span></span> <span data-ttu-id="1e895-135">请注意，列现在存在于数据库中，所有现有记录都具有 EnrollmentDate 的默认值。</span><span class="sxs-lookup"><span data-stu-id="1e895-135">Notice that the column now exists in the database and all of the existing records have the default value for EnrollmentDate.</span></span>

## <a name="add-dynamic-controls-for-enrollment-date"></a><span data-ttu-id="1e895-136">为注册日期添加动态控件</span><span class="sxs-lookup"><span data-stu-id="1e895-136">Add dynamic controls for enrollment date</span></span>

<span data-ttu-id="1e895-137">现在，你将添加用于显示和编辑注册日期的控件。</span><span class="sxs-lookup"><span data-stu-id="1e895-137">You will now add controls for displaying and editing the enrollment date.</span></span> <span data-ttu-id="1e895-138">此时，通过文本框编辑值。</span><span class="sxs-lookup"><span data-stu-id="1e895-138">At this point, the value is edited through a text box.</span></span> <span data-ttu-id="1e895-139">稍后在本教程中，您将把文本框更改为 JQuery Datepicker 小组件。</span><span class="sxs-lookup"><span data-stu-id="1e895-139">Later in the tutorial, you will change the text box to the JQuery Datepicker widget.</span></span>

<span data-ttu-id="1e895-140">首先，请务必注意，无需对**AddStudent**文件进行任何更改。</span><span class="sxs-lookup"><span data-stu-id="1e895-140">First, it is important to note that you do not need to make any change to the **AddStudent.aspx** file.</span></span> <span data-ttu-id="1e895-141">DynamicEntity 控件将自动呈现新的属性。</span><span class="sxs-lookup"><span data-stu-id="1e895-141">The DynamicEntity control will automatically render the new property.</span></span>

<span data-ttu-id="1e895-142">打开 **"** student"，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="1e895-142">Open **Students.aspx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

<span data-ttu-id="1e895-143">运行应用程序，请注意，可以通过键入日期来设置注册日期的值。</span><span class="sxs-lookup"><span data-stu-id="1e895-143">Run the application and notice that you can set the value of the enrollment date by typing a date.</span></span> <span data-ttu-id="1e895-144">添加新学生时：</span><span class="sxs-lookup"><span data-stu-id="1e895-144">When adding a new student:</span></span>

![设置日期](integrating-jquery-ui/_static/image1.png)

<span data-ttu-id="1e895-146">或编辑现有值：</span><span class="sxs-lookup"><span data-stu-id="1e895-146">Or, editing an existing value:</span></span>

![编辑日期](integrating-jquery-ui/_static/image2.png)

<span data-ttu-id="1e895-148">键入日期是可行的，但它可能不是你希望提供的客户体验。</span><span class="sxs-lookup"><span data-stu-id="1e895-148">Typing the date works, but it might not be the customer experience you wish to provide.</span></span> <span data-ttu-id="1e895-149">在下一部分中，你将启用通过日历选择日期。</span><span class="sxs-lookup"><span data-stu-id="1e895-149">In the next section, you will enable selecting a date through a calendar.</span></span>

## <a name="install-nuget-package-to-work-with-jquery-ui"></a><span data-ttu-id="1e895-150">安装 NuGet 包以使用 JQuery UI</span><span class="sxs-lookup"><span data-stu-id="1e895-150">Install NuGet package to work with JQuery UI</span></span>

<span data-ttu-id="1e895-151">**汁 ui** NuGet 包可以轻松地将 JQuery UI 小组件集成到 web 应用程序中。</span><span class="sxs-lookup"><span data-stu-id="1e895-151">The **Juice UI** NuGet package enables easy integration of the JQuery UI widgets into your web application.</span></span> <span data-ttu-id="1e895-152">若要使用此包，请通过 NuGet 安装它。</span><span class="sxs-lookup"><span data-stu-id="1e895-152">To use this package, install it through NuGet.</span></span>

![添加汁 UI](integrating-jquery-ui/_static/image3.png)

<span data-ttu-id="1e895-154">安装的汁 UI 版本可能与应用程序中的 JQuery 版本冲突。</span><span class="sxs-lookup"><span data-stu-id="1e895-154">The version of Juice UI that you install may conflict with the version of JQuery in your application.</span></span> <span data-ttu-id="1e895-155">在继续学习本教程之前，请尝试运行你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e895-155">Before proceeding with this tutorial, try running your application.</span></span> <span data-ttu-id="1e895-156">如果遇到 JavaScript 错误，需协调 JQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="1e895-156">If you encounter a JavaScript error, you need to reconcile the JQuery version.</span></span> <span data-ttu-id="1e895-157">你可以将所需的 JQuery 版本添加到脚本文件夹（在编写本教程时为版本1.8.2），也可以在 Site 中添加。 master 指定 JQuery 文件的路径。</span><span class="sxs-lookup"><span data-stu-id="1e895-157">You can either add the expected version of JQuery to your Scripts folder (version 1.8.2 at time of writing this tutorial), or in Site.master specify the path to the JQuery file.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a><span data-ttu-id="1e895-158">自定义日期时间模板以包含 Datepicker 小组件</span><span class="sxs-lookup"><span data-stu-id="1e895-158">Customize DateTime template to include Datepicker widget</span></span>

<span data-ttu-id="1e895-159">将 Datepicker 小组件添加到动态数据模板，以编辑日期时间值。</span><span class="sxs-lookup"><span data-stu-id="1e895-159">You will add the Datepicker widget to the dynamic data template for editing a datetime value.</span></span> <span data-ttu-id="1e895-160">通过将小组件添加到模板中，它会自动呈现在用于添加新学生的表单和用于编辑学生的 "网格" 视图中。</span><span class="sxs-lookup"><span data-stu-id="1e895-160">By adding the widget to the template, it is automatically rendered in both the form for adding a new student and in the grid view for editing students.</span></span> <span data-ttu-id="1e895-161">打开**DateTime\_编辑 .ascx**，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="1e895-161">Open **DateTime\_Edit.ascx**, and add the following highlighted code.</span></span>

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

<span data-ttu-id="1e895-162">在代码隐藏文件中，您将设置 DatePicker 的最小和最大日期。</span><span class="sxs-lookup"><span data-stu-id="1e895-162">In the code-behind file, you will set the minimum and maximum dates for the DatePicker.</span></span> <span data-ttu-id="1e895-163">通过设置这些值，你将会阻止用户导航到无效日期。</span><span class="sxs-lookup"><span data-stu-id="1e895-163">By setting these values, you will prevent users from navigating to invalid dates.</span></span> <span data-ttu-id="1e895-164">如果提供了一个值，则将从 DateTime 属性的**RangeAttribute**中检索最小值和最大值。</span><span class="sxs-lookup"><span data-stu-id="1e895-164">You will retrieve the minimum and maximum values from the **RangeAttribute** on the DateTime property, if one is provided.</span></span> <span data-ttu-id="1e895-165">打开**DateTime\_Edit.ascx.cs**，并将以下突出显示的代码添加到页面\_Load 方法。</span><span class="sxs-lookup"><span data-stu-id="1e895-165">Open **DateTime\_Edit.ascx.cs**, and add the following highlighted code to the Page\_Load method.</span></span>

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

<span data-ttu-id="1e895-166">运行 web 应用程序并导航到 AddStudent 页。</span><span class="sxs-lookup"><span data-stu-id="1e895-166">Run the web application and navigate to the AddStudent page.</span></span> <span data-ttu-id="1e895-167">提供字段的值，请注意，当你单击 "注册日期" 文本框时，将显示 "日历"。</span><span class="sxs-lookup"><span data-stu-id="1e895-167">Provide values for the fields and notice that when you click on the text box for Enrollment Date, the calendar is displayed.</span></span>

![日期选取器](integrating-jquery-ui/_static/image4.png)

<span data-ttu-id="1e895-169">选择一个日期，然后单击 "**插入**"。</span><span class="sxs-lookup"><span data-stu-id="1e895-169">Pick a date, and click **Insert**.</span></span> <span data-ttu-id="1e895-170">RangeAttribute 在服务器上强制执行验证。</span><span class="sxs-lookup"><span data-stu-id="1e895-170">The RangeAttribute enforces validation on the server.</span></span> <span data-ttu-id="1e895-171">通过设置 Datepicker 上的 minDate 属性，还可以在客户端上应用验证。</span><span class="sxs-lookup"><span data-stu-id="1e895-171">By setting the minDate property on the Datepicker, you also apply validation on the client.</span></span> <span data-ttu-id="1e895-172">日历不允许用户导航到 minDate 值之前的日期。</span><span class="sxs-lookup"><span data-stu-id="1e895-172">The calendar does not let the user navigate to a date prior to the value of minDate.</span></span>

<span data-ttu-id="1e895-173">在网格视图中编辑记录时，也会显示该日历。</span><span class="sxs-lookup"><span data-stu-id="1e895-173">When you edit a record in the grid view, the calendar is also displayed.</span></span>

![GridView 中的 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a><span data-ttu-id="1e895-175">结论</span><span class="sxs-lookup"><span data-stu-id="1e895-175">Conclusion</span></span>

<span data-ttu-id="1e895-176">在本教程中，已学习如何将 JQuery 小组件合并到使用模型绑定的 web 窗体中。</span><span class="sxs-lookup"><span data-stu-id="1e895-176">In this tutorial, you learned how to incorporate a JQuery widget into a web form that uses model binding.</span></span>

<span data-ttu-id="1e895-177">在下一[教程](using-query-string-values-to-retrieve-data.md)中，您将在选择数据时使用查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="1e895-177">In the next [tutorial](using-query-string-values-to-retrieve-data.md), you will use a query string value when selecting data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e895-178">[上一页](sorting-paging-and-filtering-data.md)
> [下一页](using-query-string-values-to-retrieve-data.md)</span><span class="sxs-lookup"><span data-stu-id="1e895-178">[Previous](sorting-paging-and-filtering-data.md)
[Next](using-query-string-values-to-retrieve-data.md)</span></span>
