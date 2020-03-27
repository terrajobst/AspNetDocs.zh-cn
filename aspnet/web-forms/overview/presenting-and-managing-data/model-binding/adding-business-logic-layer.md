---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 向使用模型绑定和 web 窗体的项目添加业务逻辑层 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515426"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="e075f-104">向使用模型绑定和 web 窗体的项目添加业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="e075f-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="e075f-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e075f-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e075f-106">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="e075f-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="e075f-107">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="e075f-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="e075f-108">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="e075f-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="e075f-109">本教程演示如何通过业务逻辑层使用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="e075f-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="e075f-110">你将设置 OnCallingDataMethods 成员，以指定使用当前页以外的对象来调用数据方法。</span><span class="sxs-lookup"><span data-stu-id="e075f-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="e075f-111">本教程基于在序列的[前面](retrieving-data.md)部分中创建的项目构建。</span><span class="sxs-lookup"><span data-stu-id="e075f-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="e075f-112">可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="e075f-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="e075f-113">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="e075f-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="e075f-114">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="e075f-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="e075f-115">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="e075f-115">What you'll build</span></span>

<span data-ttu-id="e075f-116">通过模型绑定，可以将数据交互代码放入网页的代码隐藏文件中，也可以放在单独的业务逻辑类中。</span><span class="sxs-lookup"><span data-stu-id="e075f-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="e075f-117">前面的教程演示了如何使用代码隐藏文件来实现数据交互代码。</span><span class="sxs-lookup"><span data-stu-id="e075f-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="e075f-118">此方法适用于小型站点，但在维护大型站点时，这可能会导致代码重复并更难。</span><span class="sxs-lookup"><span data-stu-id="e075f-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="e075f-119">由于没有抽象层，因此也可能很难以编程方式测试驻留在代码隐藏文件中的代码。</span><span class="sxs-lookup"><span data-stu-id="e075f-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="e075f-120">为了集中数据交互代码，你可以创建一个包含用于与数据进行交互的所有逻辑的业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="e075f-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="e075f-121">然后从网页调用业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="e075f-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="e075f-122">本教程介绍如何将您在前面的教程中编写的所有代码移到业务逻辑层，然后使用这些页面中的代码。</span><span class="sxs-lookup"><span data-stu-id="e075f-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="e075f-123">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="e075f-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="e075f-124">将代码从代码隐藏文件移动到业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="e075f-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="e075f-125">更改数据绑定控件以调用业务逻辑层中的方法</span><span class="sxs-lookup"><span data-stu-id="e075f-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="e075f-126">创建业务逻辑层</span><span class="sxs-lookup"><span data-stu-id="e075f-126">Create business logic layer</span></span>

<span data-ttu-id="e075f-127">现在，您将创建从网页中调用的类。</span><span class="sxs-lookup"><span data-stu-id="e075f-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="e075f-128">此类中的方法与您在前面的教程中使用的方法类似，并包括值提供程序特性。</span><span class="sxs-lookup"><span data-stu-id="e075f-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="e075f-129">首先，添加一个名为**BLL**的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="e075f-129">First, add a new folder called **BLL**.</span></span>

![添加文件夹](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="e075f-131">在 BLL 文件夹中，创建一个名为**SchoolBL.cs**的新类。</span><span class="sxs-lookup"><span data-stu-id="e075f-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="e075f-132">它将包含最初驻留在代码隐藏文件中的所有数据操作。</span><span class="sxs-lookup"><span data-stu-id="e075f-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="e075f-133">方法与代码隐藏文件中的方法几乎相同，但会包含一些更改。</span><span class="sxs-lookup"><span data-stu-id="e075f-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="e075f-134">需要注意的最重要的更改是，您不再从**Page**类的实例中执行该代码。</span><span class="sxs-lookup"><span data-stu-id="e075f-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="e075f-135">Page 类包含**TryUpdateModel**方法和**ModelState**属性。</span><span class="sxs-lookup"><span data-stu-id="e075f-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="e075f-136">将此代码移到业务逻辑层后，将不再具有 Page 类的实例来调用这些成员。</span><span class="sxs-lookup"><span data-stu-id="e075f-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="e075f-137">若要解决此问题，必须将**ModelMethodContext**参数添加到访问 TryUpdateModel 或 ModelState 的任何方法。</span><span class="sxs-lookup"><span data-stu-id="e075f-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="e075f-138">使用此 ModelMethodContext 参数可以调用 TryUpdateModel 或检索 ModelState。</span><span class="sxs-lookup"><span data-stu-id="e075f-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="e075f-139">无需更改网页中的任何内容即可为此新参数提供帐户。</span><span class="sxs-lookup"><span data-stu-id="e075f-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="e075f-140">将 SchoolBL.cs 中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e075f-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="e075f-141">修改现有页面以从业务逻辑层检索数据</span><span class="sxs-lookup"><span data-stu-id="e075f-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="e075f-142">最后，通过将代码隐藏文件中的查询转换为使用业务逻辑层，将 pages. .aspx、AddStudent 和 default.aspx 页转换为。</span><span class="sxs-lookup"><span data-stu-id="e075f-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="e075f-143">在学生、AddStudent 和课程的代码隐藏文件中，删除或注释掉以下查询方法：</span><span class="sxs-lookup"><span data-stu-id="e075f-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="e075f-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="e075f-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="e075f-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="e075f-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="e075f-146">studentsGrid\_Deleteitem.php</span><span class="sxs-lookup"><span data-stu-id="e075f-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="e075f-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="e075f-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="e075f-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="e075f-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="e075f-149">你现在应在代码隐藏文件中没有代码，这与数据操作有关。</span><span class="sxs-lookup"><span data-stu-id="e075f-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="e075f-150">使用**OnCallingDataMethods**事件处理程序可以指定要用于数据方法的对象。</span><span class="sxs-lookup"><span data-stu-id="e075f-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="e075f-151">在 "student" 中，为该事件处理程序添加一个值，然后将数据方法的名称更改为业务逻辑类中的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="e075f-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="e075f-152">在 "student" 的代码隐藏文件中，为 CallingDataMethods 事件定义事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="e075f-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="e075f-153">在此事件处理程序中，您将指定数据操作的业务逻辑类。</span><span class="sxs-lookup"><span data-stu-id="e075f-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="e075f-154">在 AddStudent 中，进行类似的更改。</span><span class="sxs-lookup"><span data-stu-id="e075f-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="e075f-155">在 default.aspx 中，进行类似的更改。</span><span class="sxs-lookup"><span data-stu-id="e075f-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="e075f-156">运行应用程序，并注意所有页面的功能都与以前相同。</span><span class="sxs-lookup"><span data-stu-id="e075f-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="e075f-157">验证逻辑也能正常工作。</span><span class="sxs-lookup"><span data-stu-id="e075f-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e075f-158">结论</span><span class="sxs-lookup"><span data-stu-id="e075f-158">Conclusion</span></span>

<span data-ttu-id="e075f-159">在本教程中，您将重新构建应用程序以使用数据访问层和业务逻辑层。</span><span class="sxs-lookup"><span data-stu-id="e075f-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="e075f-160">您指定数据控件使用的对象不是数据操作的当前页。</span><span class="sxs-lookup"><span data-stu-id="e075f-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="e075f-161">上一篇</span><span class="sxs-lookup"><span data-stu-id="e075f-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
