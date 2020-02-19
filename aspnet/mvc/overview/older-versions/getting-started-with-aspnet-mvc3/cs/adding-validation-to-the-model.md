---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 向模型添加验证（C#） |Microsoft Docs
author: Rick-Anderson
description: 创建控制器
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 19d86dc0df931a9d135e46209559892b77626cf6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457710"
---
# <a name="adding-validation-to-the-model-c"></a><span data-ttu-id="07b69-103">向模型添加验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="07b69-103">Adding Validation to the Model (C#)</span></span>

<span data-ttu-id="07b69-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="07b69-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="07b69-105">[此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="07b69-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="07b69-106">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="07b69-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="07b69-107">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="07b69-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="07b69-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="07b69-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="07b69-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="07b69-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="07b69-110">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="07b69-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="07b69-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="07b69-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="07b69-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="07b69-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="07b69-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="07b69-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="07b69-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="07b69-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="07b69-115">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="07b69-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="07b69-116">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="07b69-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="07b69-117">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="07b69-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="07b69-118">在本部分中，你将向 `Movie` 模型中添加验证逻辑，并确保每当用户尝试使用应用程序创建或编辑电影时，都会强制执行验证规则。</span><span class="sxs-lookup"><span data-stu-id="07b69-118">In this section you'll add validation logic to the `Movie` model, and you'll ensure that the validation rules are enforced any time a user attempts to create or edit a movie using the application.</span></span>

## <a name="keeping-things-dry"></a><span data-ttu-id="07b69-119">使东西干燥</span><span class="sxs-lookup"><span data-stu-id="07b69-119">Keeping Things DRY</span></span>

<span data-ttu-id="07b69-120">ASP.NET MVC 的核心设计原则之一是晾干（"不要自我重复"）。</span><span class="sxs-lookup"><span data-stu-id="07b69-120">One of the core design tenets of ASP.NET MVC is DRY ("Don't Repeat Yourself").</span></span> <span data-ttu-id="07b69-121">ASP.NET MVC 鼓励您仅指定一次功能或行为，然后让它在应用程序中的任何位置进行反映。</span><span class="sxs-lookup"><span data-stu-id="07b69-121">ASP.NET MVC encourages you to specify functionality or behavior only once, and then have it be reflected everywhere in an application.</span></span> <span data-ttu-id="07b69-122">这会减少编写所需的代码量，并使编写的代码更易于维护。</span><span class="sxs-lookup"><span data-stu-id="07b69-122">This reduces the amount of code you need to write and makes the code you do write much easier to maintain.</span></span>

<span data-ttu-id="07b69-123">ASP.NET MVC 和实体框架 Code First 提供的验证支持是有效的操作原理示例。</span><span class="sxs-lookup"><span data-stu-id="07b69-123">The validation support provided by ASP.NET MVC and Entity Framework Code First is a great example of the DRY principle in action.</span></span> <span data-ttu-id="07b69-124">您可以在一个位置以声明方式指定验证规则（在 model 类中），然后在应用程序的任何位置强制执行这些规则。</span><span class="sxs-lookup"><span data-stu-id="07b69-124">You can declaratively specify validation rules in one place (in the model class) and then those rules are enforced everywhere in the application.</span></span>

<span data-ttu-id="07b69-125">让我们看看如何在电影应用程序中利用此验证支持。</span><span class="sxs-lookup"><span data-stu-id="07b69-125">Let's look at how you can take advantage of this validation support in the movie application.</span></span>

## <a name="adding-validation-rules-to-the-movie-model"></a><span data-ttu-id="07b69-126">向影片模型添加验证规则</span><span class="sxs-lookup"><span data-stu-id="07b69-126">Adding Validation Rules to the Movie Model</span></span>

<span data-ttu-id="07b69-127">首先，将一些验证逻辑添加到 `Movie` 类。</span><span class="sxs-lookup"><span data-stu-id="07b69-127">You'll begin by adding some validation logic to the `Movie` class.</span></span>

<span data-ttu-id="07b69-128">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="07b69-128">Open the *Movie.cs* file.</span></span> <span data-ttu-id="07b69-129">在该文件的顶部添加引用[`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间的 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="07b69-129">Add a `using` statement at the top of the file that references the [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

<span data-ttu-id="07b69-130">命名空间是 .NET Framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="07b69-130">The namespace is part of the .NET Framework.</span></span> <span data-ttu-id="07b69-131">它提供了一组内置验证特性，可通过声明方式应用于任何类或属性。</span><span class="sxs-lookup"><span data-stu-id="07b69-131">It provides a built-in set of validation attributes that you can apply declaratively to any class or property.</span></span>

<span data-ttu-id="07b69-132">现在更新 `Movie` 类，以利用内置[`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)、 [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)和[`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx)验证特性。</span><span class="sxs-lookup"><span data-stu-id="07b69-132">Now update the `Movie` class to take advantage of the built-in [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx), and [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) validation attributes.</span></span> <span data-ttu-id="07b69-133">使用以下代码作为应用属性的示例。</span><span class="sxs-lookup"><span data-stu-id="07b69-133">Use the following code as an example of where to apply the attributes.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

<span data-ttu-id="07b69-134">验证特性指定要对应用这些特性的模型属性强制执行的行为。</span><span class="sxs-lookup"><span data-stu-id="07b69-134">The validation attributes specify behavior that you want to enforce on the model properties they are applied to.</span></span> <span data-ttu-id="07b69-135">`Required` 特性指示属性必须具有值;在此示例中，电影必须具有 `Title`、`ReleaseDate`、`Genre`和 `Price` 属性的值才能有效。</span><span class="sxs-lookup"><span data-stu-id="07b69-135">The `Required` attribute indicates that a property must have a value; in this sample, a movie has to have values for the `Title`, `ReleaseDate`, `Genre`, and `Price` properties in order to be valid.</span></span> <span data-ttu-id="07b69-136">`Range` 特性将值限制在指定范围内。</span><span class="sxs-lookup"><span data-stu-id="07b69-136">The `Range` attribute constrains a value to within a specified range.</span></span> <span data-ttu-id="07b69-137">`StringLength` 特性使你能够设置字符串属性的最大长度，以及可选的最小长度。</span><span class="sxs-lookup"><span data-stu-id="07b69-137">The `StringLength` attribute lets you set the maximum length of a string property, and optionally its minimum length.</span></span>

<span data-ttu-id="07b69-138">Code First 确保在应用程序将更改保存到数据库中之前，强制执行在模型类上指定的验证规则。</span><span class="sxs-lookup"><span data-stu-id="07b69-138">Code First ensures that the validation rules you specify on a model class are enforced before the application saves changes in the database.</span></span> <span data-ttu-id="07b69-139">例如，以下代码将在调用 `SaveChanges` 方法时引发异常，因为缺少几个必需的 `Movie` 属性值，并且价格为零（超出有效范围）。</span><span class="sxs-lookup"><span data-stu-id="07b69-139">For example, the code below will throw an exception when the `SaveChanges` method is called, because several required `Movie` property values are missing and the price is zero (which is out of the valid range).</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

<span data-ttu-id="07b69-140">验证规则由 .NET Framework 自动强制实施有助于提高应用程序的可靠性。</span><span class="sxs-lookup"><span data-stu-id="07b69-140">Having validation rules automatically enforced by the .NET Framework helps make your application more robust.</span></span> <span data-ttu-id="07b69-141">同时它能确保你无法忘记验证某些内容，并防止你无意中将错误数据导入数据库。</span><span class="sxs-lookup"><span data-stu-id="07b69-141">It also ensures that you can't forget to validate something and inadvertently let bad data into the database.</span></span>

<span data-ttu-id="07b69-142">下面是已更新的*Movie.cs*文件的完整代码列表：</span><span class="sxs-lookup"><span data-stu-id="07b69-142">Here's a complete code listing for the updated *Movie.cs* file:</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a><span data-ttu-id="07b69-143">ASP.NET MVC 中的验证错误 UI</span><span class="sxs-lookup"><span data-stu-id="07b69-143">Validation Error UI in ASP.NET MVC</span></span>

<span data-ttu-id="07b69-144">重新运行应用程序并导航到 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="07b69-144">Re-run the application and navigate to the */Movies* URL.</span></span>

<span data-ttu-id="07b69-145">单击 "**创建电影**" 链接以添加新电影。</span><span class="sxs-lookup"><span data-stu-id="07b69-145">Click the **Create Movie** link to add a new movie.</span></span> <span data-ttu-id="07b69-146">用一些无效值填写表单，然后单击 "**创建**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="07b69-146">Fill out the form with some invalid values and then click the **Create** button.</span></span>

<span data-ttu-id="07b69-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="07b69-147">[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)</span></span>

<span data-ttu-id="07b69-148">请注意表单如何自动使用背景色突出显示包含无效数据的文本框，并在每个文本框旁边发出适当的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="07b69-148">Notice how the form has automatically used a background color to highlight the text boxes that contain invalid data and has emitted an appropriate validation error message next to each one.</span></span> <span data-ttu-id="07b69-149">错误消息与您注释 `Movie` 类时指定的错误字符串匹配。</span><span class="sxs-lookup"><span data-stu-id="07b69-149">The error messages match the error strings you specified when you annotated the `Movie` class.</span></span> <span data-ttu-id="07b69-150">这两个错误都是在客户端（使用 JavaScript）和服务器端（如果用户禁用了 JavaScript）上进行的。</span><span class="sxs-lookup"><span data-stu-id="07b69-150">The errors are enforced both client-side (using JavaScript) and server-side (in case a user has JavaScript disabled).</span></span>

<span data-ttu-id="07b69-151">真正的好处是，您无需在 `MoviesController` 类中或在*Create. cshtml*视图中更改一行代码即可启用此验证 UI。</span><span class="sxs-lookup"><span data-stu-id="07b69-151">A real benefit is that you didn't need to change a single line of code in the `MoviesController` class or in the *Create.cshtml* view in order to enable this validation UI.</span></span> <span data-ttu-id="07b69-152">您在本教程前面创建的控制器和视图会自动选取在 `Movie` 模型类上使用特性指定的验证规则。</span><span class="sxs-lookup"><span data-stu-id="07b69-152">The controller and views you created earlier in this tutorial automatically picked up the validation rules that you specified using attributes on the `Movie` model class.</span></span>

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a><span data-ttu-id="07b69-153">如何在 "创建视图" 和 "创建操作" 方法中进行验证</span><span class="sxs-lookup"><span data-stu-id="07b69-153">How Validation Occurs in the Create View and Create Action Method</span></span>

<span data-ttu-id="07b69-154">你可能想知道在不对控制器或视图中的代码进行任何更新的情况下，验证 UI 是如何生成的。</span><span class="sxs-lookup"><span data-stu-id="07b69-154">You might wonder how the validation UI was generated without any updates to the code in the controller or views.</span></span> <span data-ttu-id="07b69-155">下一条列表显示了 `MovieController` 类中 `Create` 方法的外观。</span><span class="sxs-lookup"><span data-stu-id="07b69-155">The next listing shows what the `Create` methods in the `MovieController` class look like.</span></span> <span data-ttu-id="07b69-156">在本教程的前面部分中创建它们的方式没有改变。</span><span class="sxs-lookup"><span data-stu-id="07b69-156">They're unchanged from how you created them earlier in this tutorial.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

<span data-ttu-id="07b69-157">第一个操作方法显示初始 Create 窗体。</span><span class="sxs-lookup"><span data-stu-id="07b69-157">The first action method displays the initial Create form.</span></span> <span data-ttu-id="07b69-158">第二个处理窗体发布。</span><span class="sxs-lookup"><span data-stu-id="07b69-158">The second handles the form post.</span></span> <span data-ttu-id="07b69-159">第二个 `Create` 方法调用 `ModelState.IsValid` 以检查电影是否有任何验证错误。</span><span class="sxs-lookup"><span data-stu-id="07b69-159">The second `Create` method calls `ModelState.IsValid` to check whether the movie has any validation errors.</span></span> <span data-ttu-id="07b69-160">调用此方法将评估已应用于对象的任何验证特性。</span><span class="sxs-lookup"><span data-stu-id="07b69-160">Calling this method evaluates any validation attributes that have been applied to the object.</span></span> <span data-ttu-id="07b69-161">如果对象具有验证错误，则 `Create` 方法将重新出现该窗体。</span><span class="sxs-lookup"><span data-stu-id="07b69-161">If the object has validation errors, the `Create` method redisplays the form.</span></span> <span data-ttu-id="07b69-162">如果没有错误，此方法则将新电影保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="07b69-162">If there are no errors, the method saves the new movie in the database.</span></span>

<span data-ttu-id="07b69-163">下面是在本教程的前面部分中基架的*Create.* view 模板。</span><span class="sxs-lookup"><span data-stu-id="07b69-163">Below is the *Create.cshtml* view template that you scaffolded earlier in the tutorial.</span></span> <span data-ttu-id="07b69-164">以上所示的操作方法使用它来显示初始表单，并在发生错误时重新显示此表单。</span><span class="sxs-lookup"><span data-stu-id="07b69-164">It's used by the action methods shown above both to display the initial form and to redisplay it in the event of an error.</span></span>

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

<span data-ttu-id="07b69-165">请注意，代码如何使用 `Html.EditorFor` 帮助器来输出每个 `Movie` 属性的 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="07b69-165">Notice how the code uses an `Html.EditorFor` helper to output the `<input>` element for each `Movie` property.</span></span> <span data-ttu-id="07b69-166">此帮助器旁边的调用 `Html.ValidationMessageFor` 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="07b69-166">Next to this helper is a call to the `Html.ValidationMessageFor` helper method.</span></span> <span data-ttu-id="07b69-167">这两个帮助器方法使用由控制器传递到视图的模型对象（在本例中为 `Movie` 对象）。</span><span class="sxs-lookup"><span data-stu-id="07b69-167">These two helper methods work with the model object that's passed by the controller to the view (in this case, a `Movie` object).</span></span> <span data-ttu-id="07b69-168">它们会自动查找在模型上指定的验证属性，并根据需要显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="07b69-168">They automatically look for validation attributes specified on the model and display error messages as appropriate.</span></span>

<span data-ttu-id="07b69-169">这种方法的真正优点在于，控制器和 Create view 模板都不知道要强制执行的实际验证规则或显示的特定错误消息。</span><span class="sxs-lookup"><span data-stu-id="07b69-169">What's really nice about this approach is that neither the controller nor the Create view template knows anything about the actual validation rules being enforced or about the specific error messages displayed.</span></span> <span data-ttu-id="07b69-170">仅可在 `Movie` 类中指定验证规则和错误字符串。</span><span class="sxs-lookup"><span data-stu-id="07b69-170">The validation rules and the error strings are specified only in the `Movie` class.</span></span>

<span data-ttu-id="07b69-171">如果以后要更改验证逻辑，可以在一个位置刚好如此。</span><span class="sxs-lookup"><span data-stu-id="07b69-171">If you want to change the validation logic later, you can do so in exactly one place.</span></span> <span data-ttu-id="07b69-172">无需担心对应用程序的不同部分所强制执行规则的方式不一致 - 所有验证逻辑都将定义在一个位置并用于整个应用程序。</span><span class="sxs-lookup"><span data-stu-id="07b69-172">You won't have to worry about different parts of the application being inconsistent with how the rules are enforced — all validation logic will be defined in one place and used everywhere.</span></span> <span data-ttu-id="07b69-173">这使代码非常简洁，并且更易于维护和改进。</span><span class="sxs-lookup"><span data-stu-id="07b69-173">This keeps the code very clean, and makes it easy to maintain and evolve.</span></span> <span data-ttu-id="07b69-174">这意味着对 DRY 原则的完全遵守。</span><span class="sxs-lookup"><span data-stu-id="07b69-174">And it means that you'll be fully honoring the DRY principle.</span></span>

## <a name="adding-formatting-to-the-movie-model"></a><span data-ttu-id="07b69-175">向影片模型添加格式设置</span><span class="sxs-lookup"><span data-stu-id="07b69-175">Adding Formatting to the Movie Model</span></span>

<span data-ttu-id="07b69-176">打开 Movie.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="07b69-176">Open the *Movie.cs* file.</span></span> <span data-ttu-id="07b69-177">除了内置的验证特性集外， [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间还提供格式特性。</span><span class="sxs-lookup"><span data-stu-id="07b69-177">The [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provides formatting attributes in addition to the built-in set of validation attributes.</span></span> <span data-ttu-id="07b69-178">将[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性和[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)枚举值应用于发布日期和价格字段。</span><span class="sxs-lookup"><span data-stu-id="07b69-178">You'll apply the [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute and a [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) enumeration value to the release date and to the price fields.</span></span> <span data-ttu-id="07b69-179">下面的代码演示具有相应[`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)特性的 `ReleaseDate` 和 `Price` 属性。</span><span class="sxs-lookup"><span data-stu-id="07b69-179">The following code shows the `ReleaseDate` and `Price` properties with the appropriate [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

<span data-ttu-id="07b69-180">或者，您可以显式设置[`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx)值。</span><span class="sxs-lookup"><span data-stu-id="07b69-180">Alternatively, you could explicitly set a [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) value.</span></span> <span data-ttu-id="07b69-181">下面的代码显示具有日期格式字符串（即 "d"）的发布日期属性。</span><span class="sxs-lookup"><span data-stu-id="07b69-181">The following code shows the release date property with a date format string (namely, "d").</span></span> <span data-ttu-id="07b69-182">使用此来指定你不希望时间作为发布日期的一部分。</span><span class="sxs-lookup"><span data-stu-id="07b69-182">You'd use this to specify that you don't want to time as part of the release date.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

<span data-ttu-id="07b69-183">下面的代码将 `Price` 属性的格式设置为货币。</span><span class="sxs-lookup"><span data-stu-id="07b69-183">The following code formats the `Price` property as currency.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

<span data-ttu-id="07b69-184">完整的 `Movie` 类如下所示。</span><span class="sxs-lookup"><span data-stu-id="07b69-184">The complete `Movie` class is shown below.</span></span>

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

<span data-ttu-id="07b69-185">运行应用程序并浏览到 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="07b69-185">Run the application and browse to the `Movies` controller.</span></span>

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

<span data-ttu-id="07b69-187">在本系列的下一部分中，我们将回顾应用程序，并对自动生成的 `Details` 和 `Delete` 方法进行一些改进。</span><span class="sxs-lookup"><span data-stu-id="07b69-187">In the next part of the series, we'll review the application and make some improvements to the automatically generated `Details` and `Delete` methods.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="07b69-188">[上一页](adding-a-new-field.md)
> [下一页](improving-the-details-and-delete-methods.md)</span><span class="sxs-lookup"><span data-stu-id="07b69-188">[Previous](adding-a-new-field.md)
[Next](improving-the-details-and-delete-methods.md)</span></span>
