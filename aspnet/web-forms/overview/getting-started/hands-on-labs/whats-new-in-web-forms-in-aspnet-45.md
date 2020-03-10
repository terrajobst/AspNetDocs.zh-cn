---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5 中 Web 窗体的新增功能 |Microsoft Docs
author: rick-anderson
description: ASP.NET Web 窗体的新版本引入了大量改进，重点是改进使用数据时的用户体验。 在以前版本的中 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421922"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a><span data-ttu-id="f72df-104">ASP.NET 4.5 中 Web 窗体的新增功能</span><span class="sxs-lookup"><span data-stu-id="f72df-104">What's New in Web Forms in ASP.NET 4.5</span></span>

<span data-ttu-id="f72df-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="f72df-105">by [Web Camps Team](https://twitter.com/webcamps)</span></span>

> <span data-ttu-id="f72df-106">ASP.NET Web 窗体的新版本引入了大量改进，重点是改进使用数据时的用户体验。</span><span class="sxs-lookup"><span data-stu-id="f72df-106">The new version of ASP.NET Web Forms introduces a number of improvements focused on improving user experience when working with data.</span></span>
> 
> <span data-ttu-id="f72df-107">在以前版本的 Web 窗体中，当使用数据绑定来发出对象成员的值时，您使用的是数据绑定表达式 Bind （）或 Eval （）。</span><span class="sxs-lookup"><span data-stu-id="f72df-107">In previous versions of Web Forms, when using data-binding to emit the value of an object member, you used the data-binding expressions Bind() or Eval().</span></span> <span data-ttu-id="f72df-108">在 ASP.NET 的新版本中，可以使用新的 ItemType 属性声明控件将绑定到的数据类型。</span><span class="sxs-lookup"><span data-stu-id="f72df-108">In the new version of ASP.NET, you are able to declare what type of data a control is going to be bound to by using a new ItemType property.</span></span> <span data-ttu-id="f72df-109">通过设置此属性，你可以使用强类型化的变量来获得 Visual Studio 开发体验的全部优势，例如 IntelliSense、成员导航和编译时检查。</span><span class="sxs-lookup"><span data-stu-id="f72df-109">Setting this property will enable you to use a strongly-typed variable to receive the full benefits of the Visual Studio development experience, such as IntelliSense, member navigation, and compile-time checking.</span></span>
> 
> <span data-ttu-id="f72df-110">通过数据绑定控件，你现在还可以指定你自己的自定义方法用于选择、更新、删除和插入数据，从而简化了页面控件和应用程序逻辑之间的交互。</span><span class="sxs-lookup"><span data-stu-id="f72df-110">With the data-bound controls, you can now also specify your own custom methods for selecting, updating, deleting and inserting data, simplifying the interaction between the page controls and your application logic.</span></span> <span data-ttu-id="f72df-111">此外，已向 ASP.NET 添加了模型绑定功能，这意味着您可以将页面中的数据直接映射到方法类型参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-111">Additionally, model binding capabilities have been added to ASP.NET, which means you can map data from the page directly into method type parameters.</span></span>
> 
> <span data-ttu-id="f72df-112">通过最新版本的 Web 窗体验证用户输入也应该更简单。</span><span class="sxs-lookup"><span data-stu-id="f72df-112">Validating user input should also be easier with the latest version of Web Forms.</span></span> <span data-ttu-id="f72df-113">你现在可以使用**system.componentmodel. DataAnnotations**命名空间中的验证属性批注模型类，并请求你的所有站点控件使用该信息验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="f72df-113">You can now annotate your model classes with validation attributes from the **System.ComponentModel.DataAnnotations** namespace and request that all your site controls validate user input using that information.</span></span> <span data-ttu-id="f72df-114">Web 窗体中的客户端验证现在与 jQuery 集成，提供更清晰的客户端代码和非引人注目的 JavaScript 功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-114">Client-side validation in Web Forms is now integrated with jQuery, providing cleaner client-side code and unobtrusive JavaScript features.</span></span>
> 
> <span data-ttu-id="f72df-115">在 "请求验证" 区域中，已进行了改进，使你可以更轻松地关闭对应用程序特定部分的请求验证或读取无效的请求数据。</span><span class="sxs-lookup"><span data-stu-id="f72df-115">In the request validation area, improvements have been made to make it easier to selectively turn off request validation for specific parts of your applications or read invalidated request data.</span></span>
> 
> <span data-ttu-id="f72df-116">对 Web 窗体服务器控件进行了一些改进，以利用 HTML5 的新功能：</span><span class="sxs-lookup"><span data-stu-id="f72df-116">Some improvements have been made to Web Forms server controls to take advantage of new features of HTML5:</span></span>
> 
> - <span data-ttu-id="f72df-117">已更新 TextBox 控件的 TextMode 属性，以支持新的 HTML5 输入类型（如电子邮件、日期时间等）。</span><span class="sxs-lookup"><span data-stu-id="f72df-117">The TextMode property of the TextBox control has been updated to support the new HTML5 input types like email, datetime, and so on.</span></span>
> - <span data-ttu-id="f72df-118">FileUpload 控件现在支持支持此 HTML5 功能的浏览器中的多个文件上传。</span><span class="sxs-lookup"><span data-stu-id="f72df-118">The FileUpload control now supports multiple file uploads from browsers that support this HTML5 feature.</span></span>
> - <span data-ttu-id="f72df-119">验证程序控件现在支持验证 HTML5 输入元素。</span><span class="sxs-lookup"><span data-stu-id="f72df-119">Validator controls now support validating HTML5 input elements.</span></span>
> - <span data-ttu-id="f72df-120">具有表示 URL 的特性的新 HTML5 元素现在支持 runat =&quot;server&quot;。</span><span class="sxs-lookup"><span data-stu-id="f72df-120">New HTML5 elements that have attributes that represent a URL now support runat=&quot;server&quot;.</span></span> <span data-ttu-id="f72df-121">因此，可以在 URL 路径中使用 ASP.NET 约定，如 ~ 运算符来表示应用程序根（例如 &lt;视频 runat =&quot;server&quot; src =&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;）。</span><span class="sxs-lookup"><span data-stu-id="f72df-121">As a result, you can use ASP.NET conventions in URL paths, like the ~ operator to represent the application root (for example, &lt;video runat=&quot;server&quot; src=&quot;~/myVideo.wmv&quot;&gt;&lt;/video&gt;).</span></span>
> - <span data-ttu-id="f72df-122">已修复 UpdatePanel 控件以支持发布 HTML5 输入字段。</span><span class="sxs-lookup"><span data-stu-id="f72df-122">The UpdatePanel control has been fixed to support posting HTML5 input fields.</span></span>
> 
> <span data-ttu-id="f72df-123">在官方 ASP.NET 门户中，可以在 ASP.NET WebForms 4.5 中找到新功能的更多示例： [ASP.NET 4.5 和 Visual Studio 2012 中的新增](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)功能</span><span class="sxs-lookup"><span data-stu-id="f72df-123">In the official ASP.NET portal you can find more examples of the new features in ASP.NET WebForms 4.5: [What's New in ASP.NET 4.5 and Visual Studio 2012](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385)</span></span>
> 
> <span data-ttu-id="f72df-124">所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)提供。</span><span class="sxs-lookup"><span data-stu-id="f72df-124">All sample code and snippets are included in the Web Camps Training Kit, available at [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="f72df-125">目标</span><span class="sxs-lookup"><span data-stu-id="f72df-125">Objectives</span></span>

<span data-ttu-id="f72df-126">在本动手实验中，您将了解如何：</span><span class="sxs-lookup"><span data-stu-id="f72df-126">In this hands-on lab, you will learn how to:</span></span>

- <span data-ttu-id="f72df-127">使用强类型化的数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="f72df-127">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="f72df-128">在 Web 窗体中使用新的模型绑定功能</span><span class="sxs-lookup"><span data-stu-id="f72df-128">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="f72df-129">使用值提供程序将页面数据映射到代码隐藏方法</span><span class="sxs-lookup"><span data-stu-id="f72df-129">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="f72df-130">使用数据批注进行用户输入验证</span><span class="sxs-lookup"><span data-stu-id="f72df-130">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="f72df-131">通过 Web 窗体中的 jQuery 利用不引人注目的客户端验证</span><span class="sxs-lookup"><span data-stu-id="f72df-131">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="f72df-132">实现精细请求验证</span><span class="sxs-lookup"><span data-stu-id="f72df-132">Implement granular request validation</span></span>
- <span data-ttu-id="f72df-133">在 Web 窗体中实现异步页面处理</span><span class="sxs-lookup"><span data-stu-id="f72df-133">Implement asynchronous page processing in Web Forms</span></span>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="f72df-134">系统必备</span><span class="sxs-lookup"><span data-stu-id="f72df-134">Prerequisites</span></span>

<span data-ttu-id="f72df-135">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="f72df-135">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="f72df-136">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="f72df-136">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="f72df-137">安装</span><span class="sxs-lookup"><span data-stu-id="f72df-137">Setup</span></span>

<span data-ttu-id="f72df-138">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="f72df-138">**Installing Code Snippets**</span></span>

<span data-ttu-id="f72df-139">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="f72df-139">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="f72df-140">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="f72df-140">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="f72df-141">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。</span><span class="sxs-lookup"><span data-stu-id="f72df-141">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="f72df-142">练习</span><span class="sxs-lookup"><span data-stu-id="f72df-142">Exercises</span></span>

<span data-ttu-id="f72df-143">本动手实验包括以下练习：</span><span class="sxs-lookup"><span data-stu-id="f72df-143">This hands-on lab includes the following exercises:</span></span>

1. [<span data-ttu-id="f72df-144">练习1： ASP.NET Web 窗体中的模型绑定</span><span class="sxs-lookup"><span data-stu-id="f72df-144">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>](#Exercise1)
2. [<span data-ttu-id="f72df-145">练习2：数据验证</span><span class="sxs-lookup"><span data-stu-id="f72df-145">Exercise 2: Data Validation</span></span>](#Exercise2)
3. [<span data-ttu-id="f72df-146">练习3： ASP.NET Web 窗体中的异步页面处理</span><span class="sxs-lookup"><span data-stu-id="f72df-146">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="f72df-147">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-147">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="f72df-148">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="f72df-148">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="f72df-149">完成本实验的估计时间： **60 分钟**。</span><span class="sxs-lookup"><span data-stu-id="f72df-149">Estimated time to complete this lab: **60 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a><span data-ttu-id="f72df-150">练习1： ASP.NET Web 窗体中的模型绑定</span><span class="sxs-lookup"><span data-stu-id="f72df-150">Exercise 1: Model Binding in ASP.NET Web Forms</span></span>

<span data-ttu-id="f72df-151">ASP.NET Web 窗体的新版本引入了大量增强功能，重点是改进处理数据时的体验。</span><span class="sxs-lookup"><span data-stu-id="f72df-151">The new version of ASP.NET Web Forms introduces a number of enhancements focused on improving the experience when working with data.</span></span> <span data-ttu-id="f72df-152">在此练习中，您将了解强类型化数据控件和模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-152">Throughout this exercise, you will learn about strongly typed data-controls and model binding.</span></span>

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a><span data-ttu-id="f72df-153">任务 1-使用强类型数据绑定</span><span class="sxs-lookup"><span data-stu-id="f72df-153">Task 1 - Using Strongly-Typed Data-Bindings</span></span>

<span data-ttu-id="f72df-154">在此任务中，您将发现 ASP.NET 4.5 中提供了新的强类型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-154">In this task, you will discover the new strongly-typed bindings available in ASP.NET 4.5.</span></span>

1. <span data-ttu-id="f72df-155">打开位于**Source/Ex1-ModelBinding/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-155">Open the **Begin** solution located at **Source/Ex1-ModelBinding/Begin/** folder.</span></span>

   1. <span data-ttu-id="f72df-156">在继续之前，需要下载一些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="f72df-156">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f72df-157">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-157">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f72df-158">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f72df-158">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f72df-159">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-159">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f72df-160">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="f72df-160">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f72df-161">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="f72df-161">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f72df-162">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="f72df-162">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f72df-163">打开 " **Customers** " 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-163">Open the **Customers.aspx** page.</span></span> <span data-ttu-id="f72df-164">在主控件中放置未编号的列表，并在内包含一个用于列出每个客户的 repeater 控件。</span><span class="sxs-lookup"><span data-stu-id="f72df-164">Place an unnumbered list in the main control and include a repeater control inside for listing each customer.</span></span> <span data-ttu-id="f72df-165">将 repeater 名称设置为**customersRepeater** ，如以下代码所示。</span><span class="sxs-lookup"><span data-stu-id="f72df-165">Set the repeater name to **customersRepeater** as shown in the following code.</span></span>

    <span data-ttu-id="f72df-166">在以前版本的 Web 窗体中，当使用数据绑定在要进行数据绑定的对象上发出成员的值时，应使用数据绑定表达式和对 Eval 方法的调用，并将成员的名称作为字符串进行传递。</span><span class="sxs-lookup"><span data-stu-id="f72df-166">In previous versions of Web Forms, when using data-binding to emit the value of a member on an object you're data-binding to, you would use a data-binding expression, along with a call to the Eval method, passing in the name of the member as a string.</span></span>

    <span data-ttu-id="f72df-167">在运行时，对 Eval 的这些调用将对当前绑定的对象使用反射来读取具有给定名称的成员的值，并在 HTML 中显示结果。</span><span class="sxs-lookup"><span data-stu-id="f72df-167">At runtime, these calls to Eval will use reflection against the currently bound object to read the value of the member with the given name, and display the result in the HTML.</span></span> <span data-ttu-id="f72df-168">利用这种方法，可以非常轻松地对任意 unshaped 的数据进行数据绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-168">This approach makes it very easy to data-bind against arbitrary, unshaped data.</span></span>

    <span data-ttu-id="f72df-169">遗憾的是，您在 Visual Studio 中丢失了许多优秀的开发时体验功能，其中包括用于成员名称的 IntelliSense、对导航的支持（如中转到定义）和编译时检查。</span><span class="sxs-lookup"><span data-stu-id="f72df-169">Unfortunately, you lose many of the great development-time experience features in Visual Studio, including IntelliSense for member names, support for navigation (like Go To Definition), and compile-time checking.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. <span data-ttu-id="f72df-170">打开**Customers.aspx.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="f72df-170">Open the **Customers.aspx.cs** file.</span></span>
4. <span data-ttu-id="f72df-171">添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f72df-171">Add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. <span data-ttu-id="f72df-172">在**页面\_Load**方法中，添加代码以用客户列表填充中继器。</span><span class="sxs-lookup"><span data-stu-id="f72df-172">In the **Page\_Load** method, add code to populate the repeater with the list of customers.</span></span>

    <span data-ttu-id="f72df-173">（代码段- *Web 窗体 Ex01-绑定客户数据源*）</span><span class="sxs-lookup"><span data-stu-id="f72df-173">(Code Snippet - *Web Forms Lab - Ex01 - Bind Customers Data Source*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    <span data-ttu-id="f72df-174">解决方案结合使用 EntityFramework 和 CodeFirst 来创建和访问数据库。</span><span class="sxs-lookup"><span data-stu-id="f72df-174">The solution uses EntityFramework together with CodeFirst to create and access the database.</span></span> <span data-ttu-id="f72df-175">在下面的代码中，customersRepeater 绑定到一个具体化查询，该查询将返回数据库中的所有客户。</span><span class="sxs-lookup"><span data-stu-id="f72df-175">In the following code, the customersRepeater is bound to a materialized query that returns all the customers from the database.</span></span>
6. <span data-ttu-id="f72df-176">按**F5**运行解决方案并访问 "**客户**" 页，查看操作中的中继器。</span><span class="sxs-lookup"><span data-stu-id="f72df-176">Press **F5** to run the solution and go to the **Customers** page to see the repeater in action.</span></span> <span data-ttu-id="f72df-177">当解决方案使用 CodeFirst 时，在运行应用程序时，将创建数据库并将其填充到本地 SQL Express 实例中。</span><span class="sxs-lookup"><span data-stu-id="f72df-177">As the solution is using CodeFirst, the database will be created and populated in your local SQL Express instance when running the application.</span></span>

    <span data-ttu-id="f72df-178">![使用中继器列出客户](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "使用中继器列出客户")</span><span class="sxs-lookup"><span data-stu-id="f72df-178">![Listing the customers with a repeater](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Listing the customers with a repeater")</span></span>

    <span data-ttu-id="f72df-179">*使用中继器列出客户*</span><span class="sxs-lookup"><span data-stu-id="f72df-179">*Listing the customers with a repeater*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-180">在 Visual Studio 2012 中，IIS Express 是默认的 Web 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-180">In Visual Studio 2012, IIS Express is the default Web development server.</span></span>
7. <span data-ttu-id="f72df-181">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f72df-181">Close the browser and go back to Visual Studio.</span></span>
8. <span data-ttu-id="f72df-182">现在，将该实现替换为使用强类型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-182">Now replace the implementation to use strongly typed bindings.</span></span> <span data-ttu-id="f72df-183">打开 " **customer .aspx** " 页，并在 repeater 中使用 "新建**ItemType** " 属性将 "**客户**类型" 设置为 "绑定类型"。</span><span class="sxs-lookup"><span data-stu-id="f72df-183">Open the **Customers.aspx** page and use the new **ItemType** attribute in the repeater to set the **Customer** type as the binding type.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    <span data-ttu-id="f72df-184">ItemType 属性使你能够声明控件将绑定到的数据类型，并允许在数据绑定控件内使用强类型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-184">The ItemType property enables you to declare which type of data the control is going to be bound to and allows you to use strongly-typed binding inside the data-bound control.</span></span>
9. <span data-ttu-id="f72df-185">将 ItemTemplate 内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-185">Replace the ItemTemplate content with the following code.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    <span data-ttu-id="f72df-186">上面的方法的一个缺点是对 Eval （）和 Bind （）的调用是后期绑定的，也就是说，传递字符串来表示属性名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-186">One downside with the above approaches is that the calls to Eval() and Bind() are late-bound - meaning you pass strings to represent the property names.</span></span> <span data-ttu-id="f72df-187">这意味着，你不会获得有关成员名称、对代码导航的支持（如 "转到定义"）和编译时检查支持的 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="f72df-187">This means you don't get Intellisense for the member names, support for code navigation (like Go To Definition), nor compile-time checking support.</span></span>

    <span data-ttu-id="f72df-188">设置 ItemType 属性会导致在数据绑定表达式的作用域中生成两个新的类型化变量： **Item**和**BindItem**。</span><span class="sxs-lookup"><span data-stu-id="f72df-188">Setting the ItemType property causes two new typed variables to be generated in the scope of the data-binding expressions: **Item** and **BindItem**.</span></span> <span data-ttu-id="f72df-189">您可以在数据绑定表达式中使用这些强类型化变量，并获得 Visual Studio 开发体验的全部好处。</span><span class="sxs-lookup"><span data-stu-id="f72df-189">You can use these strongly typed variables in the data-binding expressions and get the full benefits of the Visual Studio development experience.</span></span>

    <span data-ttu-id="f72df-190">表达式中使用的 &quot; **：** &quot; 将自动对输出进行 HTML 编码，以避免安全问题（例如跨站点脚本攻击）。</span><span class="sxs-lookup"><span data-stu-id="f72df-190">The &quot;**:** &quot; used in the expression will automatically HTML-encode the output to avoid security issues (for example, cross-site scripting attacks).</span></span> <span data-ttu-id="f72df-191">自 .NET 4 后，此批注可用于响应写入，但现在也可用于数据绑定表达式。</span><span class="sxs-lookup"><span data-stu-id="f72df-191">This notation was available since .NET 4 for response writing, but now is also available in data-binding expressions.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-192">项成员适用于单向绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-192">The Item member works for one-way binding.</span></span> <span data-ttu-id="f72df-193">如果要执行双向绑定，请使用**BindItem**成员。</span><span class="sxs-lookup"><span data-stu-id="f72df-193">If you want to perform two-way binding use the **BindItem** member.</span></span>

    <span data-ttu-id="f72df-194">![强类型绑定中的 IntelliSense 支持](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "强类型绑定中的 IntelliSense 支持")</span><span class="sxs-lookup"><span data-stu-id="f72df-194">![IntelliSense support in strongly-typed binding](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "IntelliSense support in strongly-typed binding")</span></span>

    <span data-ttu-id="f72df-195">*强类型绑定中的 IntelliSense 支持*</span><span class="sxs-lookup"><span data-stu-id="f72df-195">*IntelliSense support in strongly-typed binding*</span></span>
10. <span data-ttu-id="f72df-196">按**F5**运行解决方案并中转到 "客户" 页，以确保更改按预期方式工作。</span><span class="sxs-lookup"><span data-stu-id="f72df-196">Press **F5** to run the solution and go to the Customers page to make sure the changes work as expected.</span></span>

    <span data-ttu-id="f72df-197">![列出客户详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "列出客户详细信息")</span><span class="sxs-lookup"><span data-stu-id="f72df-197">![Listing customer details](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "Listing customer details")</span></span>

    <span data-ttu-id="f72df-198">*列出客户详细信息*</span><span class="sxs-lookup"><span data-stu-id="f72df-198">*Listing customer details*</span></span>
11. <span data-ttu-id="f72df-199">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f72df-199">Close the browser and go back to Visual Studio.</span></span>

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a><span data-ttu-id="f72df-200">任务 2-Web 窗体中的模型绑定简介</span><span class="sxs-lookup"><span data-stu-id="f72df-200">Task 2 - Introducing Model Binding in Web Forms</span></span>

<span data-ttu-id="f72df-201">在以前版本的 ASP.NET Web 窗体中，当你想要执行双向数据绑定（检索和更新数据）时，你需要使用数据源对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-201">In previous versions of ASP.NET Web Forms, when you wanted to perform two-way data-binding, both retrieving and updating data, you needed to use a Data Source object.</span></span> <span data-ttu-id="f72df-202">这可以是对象数据源、SQL 数据源、LINQ 数据源等。</span><span class="sxs-lookup"><span data-stu-id="f72df-202">This could be an Object Data Source, a SQL Data Source, a LINQ Data Source and so on.</span></span> <span data-ttu-id="f72df-203">但是，如果您的方案需要用于处理数据的自定义代码，则需要使用对象数据源，这会带来一些缺点。</span><span class="sxs-lookup"><span data-stu-id="f72df-203">However if your scenario required custom code for handling the data, you needed to use the Object Data Source and this brought some drawbacks.</span></span> <span data-ttu-id="f72df-204">例如，你需要避免复杂类型，并在执行验证逻辑时需要处理异常。</span><span class="sxs-lookup"><span data-stu-id="f72df-204">For example, you needed to avoid complex types and you needed to handle exceptions when executing validation logic.</span></span>

<span data-ttu-id="f72df-205">在新版本的 ASP.NET Web 窗体中，数据绑定控件支持模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-205">In the new version of ASP.NET Web Forms the data-bound controls support model binding.</span></span> <span data-ttu-id="f72df-206">这意味着，你可以直接在数据绑定控件中指定 select、update、insert 和 delete 方法，以便从代码隐藏文件或其他类调用逻辑。</span><span class="sxs-lookup"><span data-stu-id="f72df-206">This means that you can specify select, update, insert and delete methods directly in the data-bound control to call logic from your code-behind file or from another class.</span></span>

<span data-ttu-id="f72df-207">要了解这一点，你将使用一个 GridView 来列出使用新**SelectMethod**属性的产品类别。</span><span class="sxs-lookup"><span data-stu-id="f72df-207">To learn about this, you will use a GridView to list the product categories using the new **SelectMethod** attribute.</span></span> <span data-ttu-id="f72df-208">使用此属性可以指定用于检索 GridView 数据的方法。</span><span class="sxs-lookup"><span data-stu-id="f72df-208">This attribute enables you to specify a method for retrieving the GridView data.</span></span>

1. <span data-ttu-id="f72df-209">打开 " **default.aspx** " 页并包含**GridView**。</span><span class="sxs-lookup"><span data-stu-id="f72df-209">Open the **Products.aspx** page and include a **GridView**.</span></span> <span data-ttu-id="f72df-210">按如下所示配置 GridView，使用强类型绑定并启用排序和分页。</span><span class="sxs-lookup"><span data-stu-id="f72df-210">Configure the GridView as shown below to use strongly-typed bindings and enable sorting and paging.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. <span data-ttu-id="f72df-211">使用新的**SelectMethod**属性可将 GridView 配置为调用**GetCategories**方法来选择数据。</span><span class="sxs-lookup"><span data-stu-id="f72df-211">Use the new **SelectMethod** attribute to configure the GridView to call a **GetCategories** method to select the data.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. <span data-ttu-id="f72df-212">打开**Products.aspx.cs**代码隐藏文件，并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f72df-212">Open the **Products.aspx.cs** code-behind file and add the following using statements.</span></span>

    <span data-ttu-id="f72df-213">（代码段- *Web 窗体 Ex01-命名空间*）</span><span class="sxs-lookup"><span data-stu-id="f72df-213">(Code Snippet - *Web Forms Lab - Ex01 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. <span data-ttu-id="f72df-214">在**Products**类中添加私有成员，并分配**ProductsContext**的新实例。</span><span class="sxs-lookup"><span data-stu-id="f72df-214">Add a private member in the **Products** class and assign a new instance of **ProductsContext**.</span></span> <span data-ttu-id="f72df-215">此属性将存储可用于连接到数据库的实体框架数据上下文。</span><span class="sxs-lookup"><span data-stu-id="f72df-215">This property will store the Entity Framework data context that enables you to connect to the database.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. <span data-ttu-id="f72df-216">使用 LINQ 创建**GetCategories**方法以检索类别列表。</span><span class="sxs-lookup"><span data-stu-id="f72df-216">Create a **GetCategories** method to retrieve the list of categories using LINQ.</span></span> <span data-ttu-id="f72df-217">该查询将包含**products**属性，以便 GridView 可以显示每个类别的产品数量。</span><span class="sxs-lookup"><span data-stu-id="f72df-217">The query will include the **Products** property so the GridView can show the amount of products for each category.</span></span> <span data-ttu-id="f72df-218">请注意，该方法返回一个原始 IQueryable 对象，该对象表示稍后要在页面生命周期中执行的查询。</span><span class="sxs-lookup"><span data-stu-id="f72df-218">Notice that the method returns a raw IQueryable object that represent the query to be executed later on the page lifecycle.</span></span>

    <span data-ttu-id="f72df-219">（代码段- *Web 窗体 Ex01-GetCategories*）</span><span class="sxs-lookup"><span data-stu-id="f72df-219">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > <span data-ttu-id="f72df-220">在以前版本的 ASP.NET Web 窗体中，通过在对象数据源上下文中使用自己的存储库逻辑启用排序和分页，需要编写自己的自定义代码并接收所有必需的参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-220">In previous versions of ASP.NET Web Forms, enabling sorting and paging using your own repository logic within an Object Data Source context, required to write your own custom code and receive all the necessary parameters.</span></span> <span data-ttu-id="f72df-221">现在，由于数据绑定方法可以返回 IQueryable，这表示仍在执行查询，ASP.NET 可以负责修改查询以添加正确的排序和分页参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-221">Now, as the data-binding methods can return IQueryable and this represents a query still to be executed, ASP.NET can take care of modifying the query to add the proper sorting and paging parameters.</span></span>
6. <span data-ttu-id="f72df-222">按**F5**开始调试站点并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-222">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f72df-223">应会看到 GridView 用 GetCategories 方法返回的类别填充。</span><span class="sxs-lookup"><span data-stu-id="f72df-223">You should see that the GridView is populated with the categories returned by the GetCategories method.</span></span>

    <span data-ttu-id="f72df-224">![使用模型绑定填充 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "使用模型绑定填充 GridView")</span><span class="sxs-lookup"><span data-stu-id="f72df-224">![Populating a GridView using model binding](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "Populating a GridView using model binding")</span></span>

    <span data-ttu-id="f72df-225">*使用模型绑定填充 GridView*</span><span class="sxs-lookup"><span data-stu-id="f72df-225">*Populating a GridView using model binding*</span></span>
7. <span data-ttu-id="f72df-226">按**SHIFT**+**F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="f72df-226">Press **SHIFT**+**F5** Stop debugging.</span></span>

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a><span data-ttu-id="f72df-227">任务 3-模型绑定中的值提供程序</span><span class="sxs-lookup"><span data-stu-id="f72df-227">Task 3 - Value Providers in Model Binding</span></span>

<span data-ttu-id="f72df-228">模型绑定不仅使你能够指定自定义方法来直接在数据绑定控件中处理数据，而且还允许你将页面中的数据映射到这些方法中的参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-228">Model binding not only enables you to specify custom methods to work with your data directly in the data-bound control, but also allows you to map data from the page into parameters from these methods.</span></span> <span data-ttu-id="f72df-229">在 method 参数上，可以使用值提供程序特性来指定值的数据源。</span><span class="sxs-lookup"><span data-stu-id="f72df-229">On the method parameter, you can use value provider attributes to specify the value's data source.</span></span> <span data-ttu-id="f72df-230">例如:</span><span class="sxs-lookup"><span data-stu-id="f72df-230">For example:</span></span>

- <span data-ttu-id="f72df-231">页面上的控件</span><span class="sxs-lookup"><span data-stu-id="f72df-231">Controls on the page</span></span>
- <span data-ttu-id="f72df-232">查询字符串值</span><span class="sxs-lookup"><span data-stu-id="f72df-232">Query string values</span></span>
- <span data-ttu-id="f72df-233">查看数据</span><span class="sxs-lookup"><span data-stu-id="f72df-233">View data</span></span>
- <span data-ttu-id="f72df-234">会话状态</span><span class="sxs-lookup"><span data-stu-id="f72df-234">Session state</span></span>
- <span data-ttu-id="f72df-235">Cookie</span><span class="sxs-lookup"><span data-stu-id="f72df-235">Cookies</span></span>
- <span data-ttu-id="f72df-236">已发布的表单数据</span><span class="sxs-lookup"><span data-stu-id="f72df-236">Posted form data</span></span>
- <span data-ttu-id="f72df-237">视图状态</span><span class="sxs-lookup"><span data-stu-id="f72df-237">View state</span></span>
- <span data-ttu-id="f72df-238">同时支持自定义值提供程序</span><span class="sxs-lookup"><span data-stu-id="f72df-238">Custom value providers are supported as well</span></span>

<span data-ttu-id="f72df-239">如果使用了 ASP.NET MVC 4，则会注意到模型绑定支持类似。</span><span class="sxs-lookup"><span data-stu-id="f72df-239">If you have used ASP.NET MVC 4, you will notice the model binding support is similar.</span></span> <span data-ttu-id="f72df-240">实际上，这些功能是从 ASP.NET MVC 获取的，并移**到了 system.web**程序集中，也可以在 Web 窗体上使用这些功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-240">Indeed, these features were taken from ASP.NET MVC and moved into the **System.Web** assembly to be able to use them on Web Forms as well.</span></span>

<span data-ttu-id="f72df-241">在此任务中，您将更新 GridView 以便按每个类别的产品数量来筛选结果，并通过模型绑定接收筛选器参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-241">In this task, you will update the GridView to filter its results by the amount of products for each category, receiving the filter parameter with model binding.</span></span>

1. <span data-ttu-id="f72df-242">返回到 " **Products** " 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-242">Go back to the **Products.aspx** page.</span></span>
2. <span data-ttu-id="f72df-243">在 GridView 顶部，添加一个**标签**和一个**ComboBox** ，为每个类别选择产品数，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f72df-243">At the top of the GridView, add a **Label** and a **ComboBox** to select the number of products for each category as shown below.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. <span data-ttu-id="f72df-244">向 GridView 添加**EmptyDataTemplate** ，以便在不存在具有所选产品数的类别时显示一条消息。</span><span class="sxs-lookup"><span data-stu-id="f72df-244">Add an **EmptyDataTemplate** to the GridView to show a message when there are no categories with the selected number of products.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. <span data-ttu-id="f72df-245">打开**Products.aspx.cs**代码隐藏并添加以下 using 语句。</span><span class="sxs-lookup"><span data-stu-id="f72df-245">Open the **Products.aspx.cs** code-behind and add the following using statement.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. <span data-ttu-id="f72df-246">修改**GetCategories**方法以接收整数**minProductsCount**参数并筛选返回的结果。</span><span class="sxs-lookup"><span data-stu-id="f72df-246">Modify the **GetCategories** method to receive an integer **minProductsCount** argument and filter the returned results.</span></span> <span data-ttu-id="f72df-247">为此，请将方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-247">To do this, replace the method with the following code.</span></span>

    <span data-ttu-id="f72df-248">（代码段- *Web 窗体 Ex01-GetCategories 2*）</span><span class="sxs-lookup"><span data-stu-id="f72df-248">(Code Snippet - *Web Forms Lab - Ex01 - GetCategories 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    <span data-ttu-id="f72df-249">**MinProductsCount**参数上的新 **[Control]** 属性将使 ASP.NET 知道其值必须使用页面中的控件填充。</span><span class="sxs-lookup"><span data-stu-id="f72df-249">The new **[Control]** attribute on the **minProductsCount** argument will let ASP.NET know its value must be populated using a control in the page.</span></span> <span data-ttu-id="f72df-250">ASP.NET 将查找与参数名称（minProductsCount）匹配的任何控件，并执行所需的映射和转换，以用控件值填充参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-250">ASP.NET will look for any control matching the name of the argument (minProductsCount) and perform the necessary mapping and conversion to fill the parameter with the control value.</span></span>

    <span data-ttu-id="f72df-251">此外，特性还提供了一个重载构造函数，该构造函数使你能够指定从何处获取该值的控件。</span><span class="sxs-lookup"><span data-stu-id="f72df-251">Alternatively, the attribute provides an overloaded constructor that enables you to specify the control from where to get the value.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-252">数据绑定功能的一个目标是减少需要为页面交互编写的代码量。</span><span class="sxs-lookup"><span data-stu-id="f72df-252">One goal of the data-binding features is to reduce the amount of code that needs to be written for page interaction.</span></span> <span data-ttu-id="f72df-253">除了 [Control] 值提供程序外，你还可以在方法参数中使用其他模型绑定提供程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-253">Apart from the [Control] value provider, you can use other model-binding providers in your method parameters.</span></span> <span data-ttu-id="f72df-254">其中一些部分在任务介绍中列出。</span><span class="sxs-lookup"><span data-stu-id="f72df-254">Some of them are listed in the task introduction.</span></span>
6. <span data-ttu-id="f72df-255">按**F5**开始调试站点并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-255">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f72df-256">在下拉列表中选择多个产品，并注意 GridView 现在的更新方式。</span><span class="sxs-lookup"><span data-stu-id="f72df-256">Select a number of products in the drop-down list and notice how the GridView is now updated.</span></span>

    <span data-ttu-id="f72df-257">![使用下拉列表值筛选 GridView](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "使用下拉列表值筛选 GridView")</span><span class="sxs-lookup"><span data-stu-id="f72df-257">![Filtering the GridView with a drop-down list value](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "Filtering the GridView with a drop-down list value")</span></span>

    <span data-ttu-id="f72df-258">*使用下拉列表值筛选 GridView*</span><span class="sxs-lookup"><span data-stu-id="f72df-258">*Filtering the GridView with a drop-down list value*</span></span>
7. <span data-ttu-id="f72df-259">停止调试。</span><span class="sxs-lookup"><span data-stu-id="f72df-259">Stop debugging.</span></span>

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a><span data-ttu-id="f72df-260">任务 4-使用模型绑定进行筛选</span><span class="sxs-lookup"><span data-stu-id="f72df-260">Task 4 - Using Model Binding for Filtering</span></span>

<span data-ttu-id="f72df-261">在此任务中，您将添加第二个子 GridView，以显示所选类别中的产品。</span><span class="sxs-lookup"><span data-stu-id="f72df-261">In this task, you will add a second, child GridView to show the products within the selected category.</span></span>

1. <span data-ttu-id="f72df-262">打开 " **default.aspx** " 页，并将 "GridView" 类别更新为 "自动生成" 选择按钮。</span><span class="sxs-lookup"><span data-stu-id="f72df-262">Open the **Products.aspx** page and update the categories GridView to auto-generate the Select button.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. <span data-ttu-id="f72df-263">在底部添加名为**productsGrid**的第二个**GridView** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-263">Add a second **GridView** named **productsGrid** at the bottom.</span></span> <span data-ttu-id="f72df-264">将**ItemType**设置为**WebFormsLab**，将**DataKeyNames**设置为**ProductId** ，将**SelectMethod**设置为**GetProducts**。</span><span class="sxs-lookup"><span data-stu-id="f72df-264">Set the **ItemType** to **WebFormsLab.Model.Product**, the **DataKeyNames** to **ProductId** and the **SelectMethod** to **GetProducts**.</span></span> <span data-ttu-id="f72df-265">将**AutoGenerateColumns**设置为**false** ，并添加 ProductId、ProductName、Description 和单价的列。</span><span class="sxs-lookup"><span data-stu-id="f72df-265">Set **AutoGenerateColumns** to **false** and add the columns for ProductId, ProductName, Description and UnitPrice.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. <span data-ttu-id="f72df-266">打开**Products.aspx.cs**代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="f72df-266">Open the **Products.aspx.cs** code-behind file.</span></span> <span data-ttu-id="f72df-267">实现**GetProducts**方法，以从类别 GridView 接收类别 ID 并筛选产品。</span><span class="sxs-lookup"><span data-stu-id="f72df-267">Implement the **GetProducts** method to receive the category ID from the category GridView and filter the products.</span></span> <span data-ttu-id="f72df-268">模型绑定将使用**categoriesGrid**中的选定行设置参数值。</span><span class="sxs-lookup"><span data-stu-id="f72df-268">Model binding will set the parameter value using the selected row in the **categoriesGrid**.</span></span> <span data-ttu-id="f72df-269">由于参数名称和控件名称不匹配，因此应在控件值提供程序中指定控件的名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-269">Since the argument name and control name do not match, you should specify the name of the control in the Control value provider.</span></span>

    <span data-ttu-id="f72df-270">（代码段- *Web 窗体 Ex01-GetProducts*）</span><span class="sxs-lookup"><span data-stu-id="f72df-270">(Code Snippet - *Web Forms Lab - Ex01 - GetProducts*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > <span data-ttu-id="f72df-271">此方法可以更轻松地对这些方法进行单元测试。</span><span class="sxs-lookup"><span data-stu-id="f72df-271">This approach makes it easier to unit test these methods.</span></span> <span data-ttu-id="f72df-272">在未执行 Web 窗体的单元测试上下文上，[Control] 特性不会执行任何特定操作。</span><span class="sxs-lookup"><span data-stu-id="f72df-272">On a unit test context, where Web Forms is not executing, the [Control] attribute will not perform any specific action.</span></span>
4. <span data-ttu-id="f72df-273">打开 " **products** " 页，找到 "产品" GridView。</span><span class="sxs-lookup"><span data-stu-id="f72df-273">Open the **Products.aspx** page and locate the products GridView.</span></span> <span data-ttu-id="f72df-274">更新 "产品" GridView 以显示用于编辑所选产品的链接。</span><span class="sxs-lookup"><span data-stu-id="f72df-274">Update the products GridView to show a link for editing the selected product.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. <span data-ttu-id="f72df-275">打开**ProductDetails**页代码隐藏，并将**SelectProduct**方法替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-275">Open the **ProductDetails.aspx** page code-behind and replace the **SelectProduct** method with the following code.</span></span>

    <span data-ttu-id="f72df-276">（代码段- *Web 窗体 Ex01-SelectProduct 方法*）</span><span class="sxs-lookup"><span data-stu-id="f72df-276">(Code Snippet - *Web Forms Lab - Ex01 - SelectProduct Method*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="f72df-277">请注意， **[QueryString]** 特性用于通过查询字符串中的 productId 参数填充方法参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-277">Notice that the **[QueryString]** attribute is used to fill the method parameter from a productId parameter in the query string.</span></span>
6. <span data-ttu-id="f72df-278">按**F5**开始调试站点并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-278">Press **F5** to start debugging the site and go to the Products page.</span></span> <span data-ttu-id="f72df-279">从 "类" GridView 中选择任意类别，并注意 "产品" GridView 已更新。</span><span class="sxs-lookup"><span data-stu-id="f72df-279">Select any category from the categories GridView and notice that the products GridView is updated.</span></span>

    <span data-ttu-id="f72df-280">![显示所选类别的产品](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "显示所选类别的产品")</span><span class="sxs-lookup"><span data-stu-id="f72df-280">![Showing products from the selected category](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "Showing products from the selected category")</span></span>

    <span data-ttu-id="f72df-281">*显示所选类别的产品*</span><span class="sxs-lookup"><span data-stu-id="f72df-281">*Showing products from the selected category*</span></span>
7. <span data-ttu-id="f72df-282">单击产品上的 "**查看**" 链接，打开 "ProductDetails" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-282">Click the **View** link on a product to open the ProductDetails.aspx page.</span></span>

    <span data-ttu-id="f72df-283">请注意，页面使用来自查询字符串的 productId 参数从 SelectMethod 检索产品。</span><span class="sxs-lookup"><span data-stu-id="f72df-283">Notice that the page is retrieving the product with the SelectMethod using the productId parameter from the query string.</span></span>

    <span data-ttu-id="f72df-284">![查看产品详细信息](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "查看产品详细信息")</span><span class="sxs-lookup"><span data-stu-id="f72df-284">![Viewing the product details](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "Viewing the product details")</span></span>

    <span data-ttu-id="f72df-285">*查看产品详细信息*</span><span class="sxs-lookup"><span data-stu-id="f72df-285">*Viewing the product details*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-286">在下一练习中将实现键入 HTML 说明的功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-286">The ability to type an HTML description will be implemented in the next exercise.</span></span>

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a><span data-ttu-id="f72df-287">任务 5-对更新操作使用模型绑定</span><span class="sxs-lookup"><span data-stu-id="f72df-287">Task 5 - Using Model Binding for Update Operations</span></span>

<span data-ttu-id="f72df-288">在上一任务中，你已使用了模型绑定来选择数据，在此任务中，你将了解如何在更新操作中使用模型绑定。</span><span class="sxs-lookup"><span data-stu-id="f72df-288">In the previous task, you have used model binding mainly for selecting data, in this task you will learn how to use model binding in update operations.</span></span>

<span data-ttu-id="f72df-289">你将更新 "GridView" 类别以允许用户更新类别。</span><span class="sxs-lookup"><span data-stu-id="f72df-289">You will update the categories GridView to let the user update categories.</span></span>

1. <span data-ttu-id="f72df-290">打开 " **Products** " 页，并将 "GridView" 类别更新为 "自动生成编辑" 按钮，然后使用 new **UpdateMethod**属性指定**UpdateCategory**方法来更新所选项目。</span><span class="sxs-lookup"><span data-stu-id="f72df-290">Open the **Products.aspx** page and update the categories GridView to auto-generate the Edit button and use the new **UpdateMethod** attribute to specify an **UpdateCategory** method to update the selected item.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    <span data-ttu-id="f72df-291">GridView 中的 DataKeyNames 属性定义了唯一标识模型绑定对象的成员，因此，这是 update 方法至少应接收的参数。</span><span class="sxs-lookup"><span data-stu-id="f72df-291">The DataKeyNames attribute in the GridView define which are the members that uniquely identify the model-bound object and therefore, which are the parameters the update method should at least receive.</span></span>
2. <span data-ttu-id="f72df-292">打开**Products.aspx.cs**代码隐藏文件并实现**UpdateCategory**方法。</span><span class="sxs-lookup"><span data-stu-id="f72df-292">Open the **Products.aspx.cs** code-behind file and implement the **UpdateCategory** method.</span></span> <span data-ttu-id="f72df-293">方法应接收类别 ID 以加载当前类别，并填充 GridView 中的值，然后更新类别。</span><span class="sxs-lookup"><span data-stu-id="f72df-293">The method should receive the category ID to load the current category, populate the values from the GridView and then update the category.</span></span>

    <span data-ttu-id="f72df-294">（代码段- *Web 窗体 Ex01-UpdateCategory*）</span><span class="sxs-lookup"><span data-stu-id="f72df-294">(Code Snippet - *Web Forms Lab - Ex01 - UpdateCategory*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    <span data-ttu-id="f72df-295">Page 类中的新**TryUpdateModel**方法负责使用页面中控件的值填充模型对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-295">The new **TryUpdateModel** method in the Page class is responsible of populating the model object using the values from the controls in the page.</span></span> <span data-ttu-id="f72df-296">在这种情况下，它会将正在编辑的当前 GridView 行中的更新值替换为**category**对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-296">In this case, it will replace the updated values from the current GridView row being edited into the **category** object.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-297">下一步将说明如何使用 ModelState 在编辑对象时验证用户输入的数据。</span><span class="sxs-lookup"><span data-stu-id="f72df-297">The next exercise will explain the usage of the ModelState.IsValid for validating the data entered by the user when editing the object.</span></span>
3. <span data-ttu-id="f72df-298">运行站点并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-298">Run the site and go to the Products page.</span></span> <span data-ttu-id="f72df-299">编辑类别。</span><span class="sxs-lookup"><span data-stu-id="f72df-299">Edit a category.</span></span> <span data-ttu-id="f72df-300">键入新名称，然后单击 "**更新**" 以保存更改。</span><span class="sxs-lookup"><span data-stu-id="f72df-300">Type a new name and then click **Update** to persist the changes.</span></span>

    <span data-ttu-id="f72df-301">![编辑类别](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "编辑类别")</span><span class="sxs-lookup"><span data-stu-id="f72df-301">![Editing categories](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "Editing categories")</span></span>

    <span data-ttu-id="f72df-302">*编辑类别*</span><span class="sxs-lookup"><span data-stu-id="f72df-302">*Editing categories*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a><span data-ttu-id="f72df-303">练习2：数据验证</span><span class="sxs-lookup"><span data-stu-id="f72df-303">Exercise 2: Data Validation</span></span>

<span data-ttu-id="f72df-304">在此练习中，您将了解 ASP.NET 4.5 中的新数据验证功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-304">In this exercise, you will learn about the new data validation features in ASP.NET 4.5.</span></span> <span data-ttu-id="f72df-305">你将在 Web 窗体中查看新的非引人注目验证功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-305">You will check out the new unobtrusive validation features in Web Forms.</span></span> <span data-ttu-id="f72df-306">您将使用应用程序模型类中的数据注释进行用户输入验证，最后，您将学习如何打开或关闭对页面中各个控件的请求验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-306">You will use data annotations in the application model classes for user input validation, and finally, you will learn how to turn on or off request validation to individual controls in a page.</span></span>

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a><span data-ttu-id="f72df-307">任务 1-不引人注目的验证</span><span class="sxs-lookup"><span data-stu-id="f72df-307">Task 1 - Unobtrusive Validation</span></span>

<span data-ttu-id="f72df-308">包含复杂数据（包括验证程序）的窗体往往会在页面中生成太多 JavaScript 代码，这可能表示约60% 的代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-308">Forms with complex data including validators tend to generate too much JavaScript code in the page, which can represent about 60% of the code.</span></span> <span data-ttu-id="f72df-309">启用非引人注目验证后，HTML 代码将显示为 "整洁" 和 "整齐"。</span><span class="sxs-lookup"><span data-stu-id="f72df-309">With unobtrusive validation enabled, your HTML code will look cleaner and tidier.</span></span>

<span data-ttu-id="f72df-310">在本部分中，将在 ASP.NET 中启用不引人注目的验证，以比较两个配置生成的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-310">In this section, you will enable unobtrusive validation in ASP.NET to compare the HTML code generated by both configurations.</span></span>

1. <span data-ttu-id="f72df-311">打开**Visual Studio 2012**并打开位于此实验室的**Source\Ex2-Validation\Begin**文件夹中的 "**开始**" 解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-311">Open **Visual Studio 2012** and open the **Begin** solution located in the **Source\Ex2-Validation\Begin** folder of this lab.</span></span> <span data-ttu-id="f72df-312">或者，你可以继续在上一个练习中使用现有解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-312">Alternatively, you can continue working on your existing solution from the previous exercise.</span></span>

   1. <span data-ttu-id="f72df-313">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f72df-313">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f72df-314">为此，请在解决方案资源管理器中，单击 " **WebFormsLab** " 项目 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-314">To do this, in the Solution Explorer, click the **WebFormsLab** project **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f72df-315">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f72df-315">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f72df-316">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-316">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f72df-317">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="f72df-317">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f72df-318">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="f72df-318">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f72df-319">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="f72df-319">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f72df-320">按**F5**启动 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-320">Press **F5** to start the web application.</span></span> <span data-ttu-id="f72df-321">中转到 "客户" 页，然后单击 "**添加新客户**" 链接。</span><span class="sxs-lookup"><span data-stu-id="f72df-321">Go to the Customers page and click the **Add a New Customer** link.</span></span>
3. <span data-ttu-id="f72df-322">右键单击浏览器页，然后选择 "**查看源**" 选项以打开应用程序生成的 HTML 代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-322">Right-click on the browser page, and select **View Source** option to open the HTML code generated by the application.</span></span>

    <span data-ttu-id="f72df-323">![显示页面 HTML 代码](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "显示页面 HTML 代码")</span><span class="sxs-lookup"><span data-stu-id="f72df-323">![Showing the page HTML code](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "Showing the page HTML code")</span></span>

    <span data-ttu-id="f72df-324">*显示页面 HTML 代码*</span><span class="sxs-lookup"><span data-stu-id="f72df-324">*Showing the page HTML code*</span></span>
4. <span data-ttu-id="f72df-325">滚动页面源代码，注意 ASP.NET 已在页面中注入了 JavaScript 代码和数据验证器以执行验证并显示 "错误列表"。</span><span class="sxs-lookup"><span data-stu-id="f72df-325">Scroll through the page source code and notice that ASP.NET has injected JavaScript code and data validators in the page to perform the validations and show the error list.</span></span>

    <span data-ttu-id="f72df-326">![在 CustomerDetails 页中验证 JavaScript 代码](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "在 CustomerDetails 页中验证 JavaScript 代码")</span><span class="sxs-lookup"><span data-stu-id="f72df-326">![Validation JavaScript code in CustomerDetails page](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "Validation JavaScript code in CustomerDetails page")</span></span>

    <span data-ttu-id="f72df-327">*在 CustomerDetails 页中验证 JavaScript 代码*</span><span class="sxs-lookup"><span data-stu-id="f72df-327">*Validation JavaScript code in CustomerDetails page*</span></span>
5. <span data-ttu-id="f72df-328">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f72df-328">Close the browser and go back to Visual Studio.</span></span>
6. <span data-ttu-id="f72df-329">现在，您将启用非引人注目的验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-329">Now you will enable unobtrusive validation.</span></span> <span data-ttu-id="f72df-330">打开**web.config**并在**AppSettings**节中找到**ValidationSettings： UnobtrusiveValidationMode**键 **。**</span><span class="sxs-lookup"><span data-stu-id="f72df-330">Open **Web.Config** and locate **ValidationSettings:UnobtrusiveValidationMode** key in the **AppSettings** section **.**</span></span> <span data-ttu-id="f72df-331">将键值设置为**WebForms**。</span><span class="sxs-lookup"><span data-stu-id="f72df-331">Set the key value to **WebForms**.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > <span data-ttu-id="f72df-332">你还可以在 "&quot;" 页中设置此属性 **\_Load**&quot; 事件，以防只为某些页面启用不引人注目的验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-332">You can also set this property in the &quot;**Page\_Load**&quot; event in case you want to enable Unobtrusive Validation only for some pages.</span></span>
7. <span data-ttu-id="f72df-333">打开**CustomerDetails**并按**F5**启动 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-333">Open **CustomerDetails.aspx** and press **F5** to start the Web application.</span></span>
8. <span data-ttu-id="f72df-334">按 F12 键打开 IE 开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="f72df-334">Press the F12 key to open the IE developer tools.</span></span> <span data-ttu-id="f72df-335">开发人员工具打开后，选择 "脚本" 选项卡。从菜单中选择 " **CustomerDetails** "，并注意在页面上运行 jQuery 所需的脚本已从本地站点加载到浏览器中。</span><span class="sxs-lookup"><span data-stu-id="f72df-335">Once the developer tools is open, select the script tab. Select **CustomerDetails.aspx** from the menu and take note that the scripts required to run jQuery on the page have been loaded into the browser from the local site.</span></span>

    <span data-ttu-id="f72df-336">![直接从本地 IIS 服务器加载 jQuery JavaScript 文件](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "直接从本地 IIS 服务器加载 jQuery JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="f72df-336">![Loading the jQuery JavaScript files directly from the local IIS server](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "Loading the jQuery JavaScript files directly from the local IIS server")</span></span>

    <span data-ttu-id="f72df-337">*直接从本地 IIS 服务器加载 jQuery JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="f72df-337">*Loading the jQuery JavaScript files directly from the local IIS server*</span></span>
9. <span data-ttu-id="f72df-338">关闭浏览器以返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f72df-338">Close the browser to return to Visual Studio.</span></span> <span data-ttu-id="f72df-339">再次打开 " **Master** " 文件并找到**ScriptManager**。</span><span class="sxs-lookup"><span data-stu-id="f72df-339">Open the **Site.Master** file again and locate the **ScriptManager**.</span></span> <span data-ttu-id="f72df-340">添加属性**EnableCdn**属性，其值**为 True**。</span><span class="sxs-lookup"><span data-stu-id="f72df-340">Add the attribute **EnableCdn** property with the value **True**.</span></span> <span data-ttu-id="f72df-341">这将强制从联机 URL 而不是从本地站点的 URL 加载 jQuery。</span><span class="sxs-lookup"><span data-stu-id="f72df-341">This will force jQuery to be loaded from the online URL, not from the local site's URL.</span></span>
10. <span data-ttu-id="f72df-342">在 Visual Studio 中打开**CustomerDetails** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-342">Open **CustomerDetails.aspx** in Visual Studio.</span></span> <span data-ttu-id="f72df-343">按 F5 键以运行站点。</span><span class="sxs-lookup"><span data-stu-id="f72df-343">Press the F5 key to run the site.</span></span> <span data-ttu-id="f72df-344">Internet Explorer 打开后，按 F12 键打开开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="f72df-344">Once Internet Explorer opens, press the F12 key to open the developer tools.</span></span> <span data-ttu-id="f72df-345">选择 "**脚本**" 选项卡，然后查看下拉列表。</span><span class="sxs-lookup"><span data-stu-id="f72df-345">Select the **Script** tab, and then take a look at the drop-down list.</span></span> <span data-ttu-id="f72df-346">请注意，jQuery JavaScript 文件不再从本地站点加载，而是从联机 jQuery CDN 中加载。</span><span class="sxs-lookup"><span data-stu-id="f72df-346">Note the jQuery JavaScript files are no longer being loaded from the local site, but rather from the online jQuery CDN.</span></span>

    <span data-ttu-id="f72df-347">![正在从 CDN 加载 jQuery JavaScript 文件](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "正在从 CDN 加载 jQuery JavaScript 文件")</span><span class="sxs-lookup"><span data-stu-id="f72df-347">![Loading the jQuery JavaScript files from the CDN](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "Loading the jQuery JavaScript files from the CDN")</span></span>

    <span data-ttu-id="f72df-348">*正在从 CDN 加载 jQuery JavaScript 文件*</span><span class="sxs-lookup"><span data-stu-id="f72df-348">*Loading the jQuery JavaScript files from the CDN*</span></span>
11. <span data-ttu-id="f72df-349">使用浏览器中的 "查看源" 选项再次打开 HTML 页源代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-349">Open the HTML page source code again using the View source option in the browser.</span></span> <span data-ttu-id="f72df-350">请注意，启用非引人注目验证 ASP.NET 已将插入的 JavaScript 代码替换为数据 \*特性。</span><span class="sxs-lookup"><span data-stu-id="f72df-350">Notice that by enabling the unobtrusive validation ASP.NET has replaced the injected JavaScript code with data- \*attributes.</span></span>

    <span data-ttu-id="f72df-351">![非引人注目的验证代码](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "非引人注目的验证代码")</span><span class="sxs-lookup"><span data-stu-id="f72df-351">![Unobtrusive validation code](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "Unobtrusive validation code")</span></span>

    <span data-ttu-id="f72df-352">*非引人注目的验证代码*</span><span class="sxs-lookup"><span data-stu-id="f72df-352">*Unobtrusive validation code*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-353">在此示例中，您看到了如何将带有数据批注的验证摘要简化为仅有少量的 HTML 和 JavaScript 行。</span><span class="sxs-lookup"><span data-stu-id="f72df-353">In this example, you saw how a validation summary with Data annotations was simplified to only a few HTML and JavaScript lines.</span></span> <span data-ttu-id="f72df-354">以前，如果不进行非引人注目的验证，添加的验证控件就越多，JavaScript 验证代码也就越大。</span><span class="sxs-lookup"><span data-stu-id="f72df-354">Previously, without unobtrusive validation, the more validation controls you add, the bigger your JavaScript validation code will grow.</span></span>

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a><span data-ttu-id="f72df-355">任务 2-通过数据批注验证模型</span><span class="sxs-lookup"><span data-stu-id="f72df-355">Task 2 - Validating the Model with Data Annotations</span></span>

<span data-ttu-id="f72df-356">ASP.NET 4.5 引入了针对 Web 窗体的数据批注验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-356">ASP.NET 4.5 introduces data annotations validation for Web Forms.</span></span> <span data-ttu-id="f72df-357">你现在可以在模型类中定义约束并跨所有 web 应用程序使用它们，而无需对每个输入进行验证控制。</span><span class="sxs-lookup"><span data-stu-id="f72df-357">Instead of having a validation control on each input, you can now define constraints in your model classes and use them across all your web application.</span></span> <span data-ttu-id="f72df-358">在本部分中，您将学习如何使用数据批注来验证新的/编辑客户窗体。</span><span class="sxs-lookup"><span data-stu-id="f72df-358">In this section, you will learn how to use data annotations for validating a new/edit customer form.</span></span>

1. <span data-ttu-id="f72df-359">打开**CustomerDetail**页。</span><span class="sxs-lookup"><span data-stu-id="f72df-359">Open **CustomerDetail.aspx** page.</span></span> <span data-ttu-id="f72df-360">请注意，" **EditItemTemplate** " 和 "**则**" 部分中的 customer first name 和 second name 使用 RequiredFieldValidator 控件进行验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-360">Notice that the customer first name and second name in the **EditItemTemplate** and **InsertItemTemplate** sections are validated using a RequiredFieldValidator controls.</span></span> <span data-ttu-id="f72df-361">每个验证程序都与特定的条件相关联，因此，需要将任意数量的验证程序包含为要检查的条件。</span><span class="sxs-lookup"><span data-stu-id="f72df-361">Each validator is associated to a particular condition, so you need to include as many validators as conditions to check.</span></span>
2. <span data-ttu-id="f72df-362">添加数据批注来验证 Customer 模型类。</span><span class="sxs-lookup"><span data-stu-id="f72df-362">Add data annotations to validate the Customer model class.</span></span> <span data-ttu-id="f72df-363">打开**模型**文件夹中的**Customer.cs**类，并使用数据批注特性*修饰*每个属性。</span><span class="sxs-lookup"><span data-stu-id="f72df-363">Open **Customer.cs** class in the **Model** folder and *decorate* each property using data annotation attributes.</span></span>

    <span data-ttu-id="f72df-364">（代码段- *Web 窗体 Ex02-数据批注*）</span><span class="sxs-lookup"><span data-stu-id="f72df-364">(Code Snippet - *Web Forms Lab - Ex02 - Data Annotations*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > <span data-ttu-id="f72df-365">.NET Framework 4.5 已扩展现有数据批注集合。</span><span class="sxs-lookup"><span data-stu-id="f72df-365">.NET Framework 4.5 has extended the existing data annotation collection.</span></span> <span data-ttu-id="f72df-366">下面是一些可以使用的数据批注： [CreditCard]、[Phone]、[EmailAddress]、[Range]、[Compare]、[Url]、[FileExtensions]、[Required]、 [Key]、[RegularExpression]。</span><span class="sxs-lookup"><span data-stu-id="f72df-366">These are some of the data annotations you can use: [CreditCard], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].</span></span>
    > 
    > <span data-ttu-id="f72df-367">一些用法示例：</span><span class="sxs-lookup"><span data-stu-id="f72df-367">Some usage examples:</span></span>
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > <span data-ttu-id="f72df-369">您还可以在每个属性中定义自己的错误消息。</span><span class="sxs-lookup"><span data-stu-id="f72df-369">You can also define your own error messages within each attribute.</span></span>
3. <span data-ttu-id="f72df-370">打开**CustomerDetails** ，并删除 FormView 控件的 EditItemTemplate 和则部分中的第一个和最后一个名称字段的所有 RequiredFieldValidators。</span><span class="sxs-lookup"><span data-stu-id="f72df-370">Open **CustomerDetails.aspx** and remove all the RequiredFieldValidators for the first and last name fields in the in EditItemTemplate and InsertItemTemplate sections of the FormView control.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > <span data-ttu-id="f72df-371">使用数据批注的一个优点是，验证逻辑不会在应用程序页中重复。</span><span class="sxs-lookup"><span data-stu-id="f72df-371">One advantage of using data annotations is that validation logic is not duplicated in your application pages.</span></span> <span data-ttu-id="f72df-372">在模型中定义一次，并在操作数据的所有应用程序页中使用它。</span><span class="sxs-lookup"><span data-stu-id="f72df-372">You define it once in the model, and use it across all the application pages that manipulate data.</span></span>
4. <span data-ttu-id="f72df-373">打开**CustomerDetails**代码隐藏并找到 SaveCustomer 方法。</span><span class="sxs-lookup"><span data-stu-id="f72df-373">Open **CustomerDetails.aspx** code-behind and locate the SaveCustomer method.</span></span> <span data-ttu-id="f72df-374">当插入新客户并从 FormView 控制值接收 Customer 参数时，将调用此方法。</span><span class="sxs-lookup"><span data-stu-id="f72df-374">This method is called when inserting a new customer and receives the Customer parameter from the FormView control values.</span></span> <span data-ttu-id="f72df-375">当页控件和参数对象之间的映射发生时，ASP.NET 将对所有数据批注特性执行模型验证，并在 ModelState 字典中填充遇到的错误（如果有）。</span><span class="sxs-lookup"><span data-stu-id="f72df-375">When the mapping between the page controls and the parameter object occurs, ASP.NET will execute the model validation against all the data annotation attributes and fill the ModelState dictionary with the errors encountered, if any.</span></span>

    <span data-ttu-id="f72df-376">如果模型中的所有字段在执行验证后均有效，则 ModelState 将仅返回 true。</span><span class="sxs-lookup"><span data-stu-id="f72df-376">The ModelState.IsValid will only return true if all the fields on your model are valid after performing the validation.</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. <span data-ttu-id="f72df-377">在 CustomerDetails 页的末尾添加一个**ValidationSummary**控件以显示模型错误的列表。</span><span class="sxs-lookup"><span data-stu-id="f72df-377">Add a **ValidationSummary** control at the end of the CustomerDetails page to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    <span data-ttu-id="f72df-378">**ShowModelStateErrors**是 ValidationSummary 控件上的新属性，当设置为**true**时，控件将显示 ModelState 字典中的错误。</span><span class="sxs-lookup"><span data-stu-id="f72df-378">The **ShowModelStateErrors** is a new property on the ValidationSummary control that when set to **true**, the control will show the errors from the ModelState dictionary.</span></span> <span data-ttu-id="f72df-379">这些错误来自数据批注验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-379">These errors come from the data annotations validation.</span></span>
6. <span data-ttu-id="f72df-380">按**F5**运行 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-380">Press **F5** to run the Web application.</span></span> <span data-ttu-id="f72df-381">用一些错误值填写窗体，并单击 "**保存**" 以执行验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-381">Complete the form with some erroneous values and click **Save** to execute validation.</span></span> <span data-ttu-id="f72df-382">请注意底部的 "错误摘要"。</span><span class="sxs-lookup"><span data-stu-id="f72df-382">Notice the error summary at the bottom.</span></span>

    <span data-ttu-id="f72df-383">![数据批注验证](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "数据批注验证")</span><span class="sxs-lookup"><span data-stu-id="f72df-383">![Validation with Data Annotations](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "Validation with Data Annotations")</span></span>

    <span data-ttu-id="f72df-384">*数据批注验证*</span><span class="sxs-lookup"><span data-stu-id="f72df-384">*Validation with Data Annotations*</span></span>

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a><span data-ttu-id="f72df-385">任务 3-处理 ModelState 的自定义数据库错误</span><span class="sxs-lookup"><span data-stu-id="f72df-385">Task 3 - Handling Custom Database Errors with ModelState</span></span>

<span data-ttu-id="f72df-386">在以前版本的 Web 窗体中，处理数据库错误（如太长的字符串或唯一键冲突）可能涉及在你的存储库代码中引发异常，然后在代码隐藏中处理异常以显示错误。</span><span class="sxs-lookup"><span data-stu-id="f72df-386">In previous version of Web Forms, handling database errors such as a too long string or a unique key violation could involve throwing exceptions in your repository code and then handling the exceptions on your code-behind to display an error.</span></span> <span data-ttu-id="f72df-387">需要大量代码来执行相对简单的操作。</span><span class="sxs-lookup"><span data-stu-id="f72df-387">A great amount of code is required to do something relatively simple.</span></span>

<span data-ttu-id="f72df-388">在 Web 窗体4.5 中，可以通过一致的方式将 ModelState 对象用于显示页面上的错误，不管是从模型还是从数据库。</span><span class="sxs-lookup"><span data-stu-id="f72df-388">In Web Forms 4.5, the ModelState object can be used to display the errors on the page, either from your model or from the database, in a consistent manner.</span></span>

<span data-ttu-id="f72df-389">在此任务中，您将添加代码来正确处理数据库异常，并使用 ModelState 对象向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="f72df-389">In this task, you will add code to properly handle database exceptions and show the appropriate message to the user using the ModelState object.</span></span>

1. <span data-ttu-id="f72df-390">在应用程序仍在运行时，尝试使用重复的值更新类别的名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-390">While the application is still running, try to update the name of a category using a duplicated value.</span></span>

    <span data-ttu-id="f72df-391">![更新具有重复名称的类别](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "更新具有重复名称的类别")</span><span class="sxs-lookup"><span data-stu-id="f72df-391">![Updating a category with a duplicated name](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "Updating a category with a duplicated name")</span></span>

    <span data-ttu-id="f72df-392">*更新具有重复名称的类别*</span><span class="sxs-lookup"><span data-stu-id="f72df-392">*Updating a category with a duplicated name*</span></span>

    <span data-ttu-id="f72df-393">请注意，由于 "**类别名称**" 列 &quot;唯一&quot; 约束，将引发异常。</span><span class="sxs-lookup"><span data-stu-id="f72df-393">Notice that an exception is thrown due to the &quot;unique&quot; constraint of the **CategoryName** column.</span></span>

    <span data-ttu-id="f72df-394">![重复类别名称的异常](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "重复类别名称的异常")</span><span class="sxs-lookup"><span data-stu-id="f72df-394">![Exception for duplicated category names](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "Exception for duplicated category names")</span></span>

    <span data-ttu-id="f72df-395">*重复类别名称的异常*</span><span class="sxs-lookup"><span data-stu-id="f72df-395">*Exception for duplicated category names*</span></span>
2. <span data-ttu-id="f72df-396">停止调试。</span><span class="sxs-lookup"><span data-stu-id="f72df-396">Stop debugging.</span></span> <span data-ttu-id="f72df-397">在**Products.aspx.cs**代码隐藏文件中，更新**UpdateCategory**方法以处理 db 引发的异常。SaveChanges （）方法调用，并将错误添加到**ModelState**对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-397">In the **Products.aspx.cs** code-behind file, update the **UpdateCategory** method to handle the exceptions thrown by the db.SaveChanges() method call and add an error to the **ModelState** object.</span></span>

    <span data-ttu-id="f72df-398">新的**TryUpdateModel**方法使用用户提供的窗体数据更新从数据库检索的类别对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-398">The new **TryUpdateModel** method updates the category object retrieved from the database using the form data provided by the user.</span></span>

    <span data-ttu-id="f72df-399">（代码段- *Web 窗体 Ex02-UpdateCategory 处理错误*）</span><span class="sxs-lookup"><span data-stu-id="f72df-399">(Code Snippet - *Web Forms Lab - Ex02 - UpdateCategory Handle Errors*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > <span data-ttu-id="f72df-400">理想情况下，您必须确定 DbUpdateException 的原因，并检查根本原因是否违反了唯一键约束。</span><span class="sxs-lookup"><span data-stu-id="f72df-400">Ideally, you would have to identify the cause of the DbUpdateException and check if the root cause is the violation of a unique key constraint.</span></span>
3. <span data-ttu-id="f72df-401">打开 " **default.aspx** "，然后在 "类别" GridView 下面添加**ValidationSummary**控件，以显示模型错误的列表。</span><span class="sxs-lookup"><span data-stu-id="f72df-401">Open **Products.aspx** and add a **ValidationSummary** control below the categories GridView to show the list of model errors.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. <span data-ttu-id="f72df-402">运行站点并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-402">Run the site and go to the Products page.</span></span> <span data-ttu-id="f72df-403">尝试使用重复的值更新类别的名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-403">Try to update the name of a category using an duplicated value.</span></span>

    <span data-ttu-id="f72df-404">请注意，已处理异常并且错误消息显示在**ValidationSummary**控件中。</span><span class="sxs-lookup"><span data-stu-id="f72df-404">Notice that the exception was handled and the error message appears in the **ValidationSummary** control.</span></span>

    <span data-ttu-id="f72df-405">![类别重复错误](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "类别重复错误")</span><span class="sxs-lookup"><span data-stu-id="f72df-405">![Duplicated category error](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "Duplicated category error")</span></span>

    <span data-ttu-id="f72df-406">*类别重复错误*</span><span class="sxs-lookup"><span data-stu-id="f72df-406">*Duplicated category error*</span></span>

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a><span data-ttu-id="f72df-407">任务 4-ASP.NET Web 窗体4.5 中的请求验证</span><span class="sxs-lookup"><span data-stu-id="f72df-407">Task 4 - Request Validation in ASP.NET Web Forms 4.5</span></span>

<span data-ttu-id="f72df-408">ASP.NET 中的请求验证功能针对跨站点脚本（XSS）攻击提供一定程度的默认保护。</span><span class="sxs-lookup"><span data-stu-id="f72df-408">The request validation feature in ASP.NET provides a certain level of default protection against cross-site scripting (XSS) attacks.</span></span> <span data-ttu-id="f72df-409">在以前版本的 ASP.NET 中，请求验证在默认情况下处于启用状态，并且只能为整个页面禁用。</span><span class="sxs-lookup"><span data-stu-id="f72df-409">In previous versions of ASP.NET, request validation was enabled by default and could only be disabled for an entire page.</span></span> <span data-ttu-id="f72df-410">使用新版本的 ASP.NET Web 窗体，你现在可以对单个控件禁用请求验证，执行延迟请求验证或访问未经验证的请求数据（如果你这样做，请注意）。</span><span class="sxs-lookup"><span data-stu-id="f72df-410">With the new version of ASP.NET Web Forms you can now disable the request validation for a single control, perform lazy request validation or access un-validated request data (be careful if you do so!).</span></span>

1. <span data-ttu-id="f72df-411">按**Ctrl + F5**以启动站点而不进行调试，并中转到 "产品" 页。</span><span class="sxs-lookup"><span data-stu-id="f72df-411">Press **Ctrl+F5** to start the site without debugging and go to the Products page.</span></span> <span data-ttu-id="f72df-412">选择一个类别，然后单击任意产品上的 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="f72df-412">Select a category and then click the **Edit** link on any of the products.</span></span>
2. <span data-ttu-id="f72df-413">键入一个说明，其中包含可能危险的内容，例如，HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="f72df-413">Type a description containing potentially dangerous content, for instance including HTML tags.</span></span> <span data-ttu-id="f72df-414">请注意因请求验证而引发的异常。</span><span class="sxs-lookup"><span data-stu-id="f72df-414">Take notice of the exception thrown due to the request validation.</span></span>

    <span data-ttu-id="f72df-415">![编辑具有潜在危险内容的产品](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "编辑具有潜在危险内容的产品")</span><span class="sxs-lookup"><span data-stu-id="f72df-415">![Editing a product with potentially dangerous content](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "Editing a product with potentially dangerous content")</span></span>

    <span data-ttu-id="f72df-416">*编辑具有潜在危险内容的产品*</span><span class="sxs-lookup"><span data-stu-id="f72df-416">*Editing a product with potentially dangerous content*</span></span>

    <span data-ttu-id="f72df-417">![由于请求验证而引发的异常](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "由于请求验证而引发的异常")</span><span class="sxs-lookup"><span data-stu-id="f72df-417">![Exception thrown due to request validation](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "Exception thrown due to request validation")</span></span>

    <span data-ttu-id="f72df-418">*由于请求验证而引发的异常*</span><span class="sxs-lookup"><span data-stu-id="f72df-418">*Exception thrown due to request validation*</span></span>
3. <span data-ttu-id="f72df-419">关闭页面，并在 Visual Studio 中按**SHIFT + F5**停止调试。</span><span class="sxs-lookup"><span data-stu-id="f72df-419">Close the page and, in Visual Studio, press **SHIFT+F5** to stop debugging.</span></span>
4. <span data-ttu-id="f72df-420">打开 " **ProductDetails** " 页，找到 "**说明**" 文本框。</span><span class="sxs-lookup"><span data-stu-id="f72df-420">Open the **ProductDetails.aspx** page and locate the **Description** TextBox.</span></span>
5. <span data-ttu-id="f72df-421">向文本框中添加新的 " **ValidateRequestMode** " 属性，并将其值设置为 "**已禁用**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-421">Add the new **ValidateRequestMode** property to the TextBox and set its value to **Disabled**.</span></span>

    <span data-ttu-id="f72df-422">新的**ValidateRequestMode**属性允许您在每个控件上按粒度禁用请求验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-422">The new **ValidateRequestMode** attribute allows you to disable the request validation granularly on each control.</span></span> <span data-ttu-id="f72df-423">当你想要使用可能接收 HTML 代码的输入，但想要在页面的其余部分保持验证工作时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="f72df-423">This is useful when you want to use an input that may receive HTML code, but want to keep the validation working for the rest of the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. <span data-ttu-id="f72df-424">按**F5**运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-424">Press **F5** to run the web application.</span></span> <span data-ttu-id="f72df-425">再次打开 "编辑产品" 页，并完成包含 HTML 标记的产品说明。</span><span class="sxs-lookup"><span data-stu-id="f72df-425">Open the edit product page again and complete a product description including HTML tags.</span></span> <span data-ttu-id="f72df-426">请注意，现在可以将 HTML 内容添加到说明中。</span><span class="sxs-lookup"><span data-stu-id="f72df-426">Notice that you can now add HTML content to the description.</span></span>

    <span data-ttu-id="f72df-427">![已对产品说明禁用请求验证](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "已对产品说明禁用请求验证")</span><span class="sxs-lookup"><span data-stu-id="f72df-427">![Request validation disabled for the product description](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "Request validation disabled for the product description")</span></span>

    <span data-ttu-id="f72df-428">*已对产品说明禁用请求验证*</span><span class="sxs-lookup"><span data-stu-id="f72df-428">*Request validation disabled for the product description*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-429">在生产应用程序中，您应该净化用户输入的 HTML 代码，以确保仅输入安全 HTML 标记（例如，没有&gt; 标记的 &lt;脚本）。</span><span class="sxs-lookup"><span data-stu-id="f72df-429">In a production application, you should sanitize the HTML code entered by the user to make sure only safe HTML tags are entered (for example, there are no &lt;script&gt; tags).</span></span> <span data-ttu-id="f72df-430">为此，可以使用[Microsoft Web 保护库](https://www.nuget.org/packages/AntiXSS)。</span><span class="sxs-lookup"><span data-stu-id="f72df-430">To do this, you can use [Microsoft Web Protection Library](https://www.nuget.org/packages/AntiXSS).</span></span>
7. <span data-ttu-id="f72df-431">再次编辑该产品。</span><span class="sxs-lookup"><span data-stu-id="f72df-431">Edit the product again.</span></span> <span data-ttu-id="f72df-432">在 "名称" 字段中键入 HTML 代码，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-432">Type HTML code in the Name field and click **Save**.</span></span> <span data-ttu-id="f72df-433">请注意，仅对 "说明" 字段禁用请求验证，其余字段仍将根据潜在的危险内容进行验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-433">Notice that Request Validation is only disabled for the Description field and the rest of the fields re still validated against the potentially dangerous content.</span></span>

    <span data-ttu-id="f72df-434">![在其余字段中启用了请求验证](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "在其余字段中启用了请求验证")</span><span class="sxs-lookup"><span data-stu-id="f72df-434">![Request validation enabled in the rest of the fields](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "Request validation enabled in the rest of the fields")</span></span>

    <span data-ttu-id="f72df-435">*在其余字段中启用了请求验证*</span><span class="sxs-lookup"><span data-stu-id="f72df-435">*Request validation enabled in the rest of the fields*</span></span>

    <span data-ttu-id="f72df-436">ASP.NET Web Forms 4.5 包括一种新的请求验证模式，用于延迟执行请求验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-436">ASP.NET Web Forms 4.5 includes a new request validation mode to perform request validation lazily.</span></span> <span data-ttu-id="f72df-437">当请求验证模式设置为**4.5**时，如果一段代码访问*请求。窗体 [&quot;键&quot;]* ，ASP.NET 4.5 的请求验证仅对窗体集合中的特定元素触发请求验证。</span><span class="sxs-lookup"><span data-stu-id="f72df-437">With the request validation mode set to **4.5**, if a piece of code accesses *Request.Form[&quot;key&quot;]*, ASP.NET 4.5's request validation will only trigger request validation for that specific element in the form collection.</span></span>

    <span data-ttu-id="f72df-438">此外，ASP.NET 4.5 现在包含 Microsoft 反 XSS 库 v4.0 提供的核心编码例程。</span><span class="sxs-lookup"><span data-stu-id="f72df-438">Additionally, ASP.NET 4.5 now includes core encoding routines from the Microsoft Anti-XSS Library v4.0.</span></span> <span data-ttu-id="f72df-439">在新的**AntiXss**命名空间中找到的新*AntiXssEncoder*类型实现了 anti-spam 编码例程。</span><span class="sxs-lookup"><span data-stu-id="f72df-439">The Anti-XSS encoding routines are implemented by the new *AntiXssEncoder* type found in the new **System.Web.Security.AntiXss** namespace.</span></span> <span data-ttu-id="f72df-440">如果将**encoderType**参数配置为使用*AntiXssEncoder*，则 ASP.NET 中的所有输出编码会自动使用新的编码例程。</span><span class="sxs-lookup"><span data-stu-id="f72df-440">With the **encoderType** parameter configured to use *AntiXssEncoder*, all output encoding within ASP.NET automatically uses the new encoding routines.</span></span>
8. <span data-ttu-id="f72df-441">ASP.NET 4.5 请求验证还支持对请求数据进行未经验证的访问。</span><span class="sxs-lookup"><span data-stu-id="f72df-441">ASP.NET 4.5 request validation also supports un-validated access to request data.</span></span> <span data-ttu-id="f72df-442">ASP.NET 4.5 将新的集合属性添加到名为**未经验证**的**HttpRequest**对象。</span><span class="sxs-lookup"><span data-stu-id="f72df-442">ASP.NET 4.5 adds a new collection property to the **HttpRequest** object called **Unvalidated**.</span></span> <span data-ttu-id="f72df-443">导航到**HttpRequest**时，可以访问请求数据的所有常见部分，包括 Forms、Querystring、Cookie、url 等。</span><span class="sxs-lookup"><span data-stu-id="f72df-443">When you navigate into **HttpRequest.Unvalidated** you have access to all of the common pieces of request data, including Forms, QueryStrings, Cookies, URLs, and so on.</span></span>

    <span data-ttu-id="f72df-444">![未经验证对象](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "未经验证对象")</span><span class="sxs-lookup"><span data-stu-id="f72df-444">![Request.Unvalidated object](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "Request.Unvalidated object")</span></span>

    <span data-ttu-id="f72df-445">*未经验证对象*</span><span class="sxs-lookup"><span data-stu-id="f72df-445">*Request.Unvalidated object*</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-446">**请谨慎使用 HttpRequest 属性！**</span><span class="sxs-lookup"><span data-stu-id="f72df-446">**Please use the HttpRequest.Unvalidated property with caution!**</span></span> <span data-ttu-id="f72df-447">请确保仔细对原始请求数据执行自定义验证，以确保不会将危险文本作为往返，并将其呈现给不太严格的客户！</span><span class="sxs-lookup"><span data-stu-id="f72df-447">Make sure you carefully perform custom validation on the raw request data to ensure that dangerous text is not round-tripped and rendered back to unsuspecting customers!</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a><span data-ttu-id="f72df-448">练习3： ASP.NET Web 窗体中的异步页面处理</span><span class="sxs-lookup"><span data-stu-id="f72df-448">Exercise 3: Asynchronous Page Processing in ASP.NET Web Forms</span></span>

<span data-ttu-id="f72df-449">在此练习中，将引入 ASP.NET Web 窗体中的新的异步页处理功能。</span><span class="sxs-lookup"><span data-stu-id="f72df-449">In this exercise, you will be introduced to the new asynchronous page processing features in ASP.NET Web Forms.</span></span>

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a><span data-ttu-id="f72df-450">任务 1-更新产品详细信息页以上传和显示图像</span><span class="sxs-lookup"><span data-stu-id="f72df-450">Task 1 - Updating the Product Details Page to Upload and Show Images</span></span>

<span data-ttu-id="f72df-451">在此任务中，你将更新 "产品详细信息" 页，以允许用户为产品指定图像 URL，并将其显示在只读视图中。</span><span class="sxs-lookup"><span data-stu-id="f72df-451">In this task, you will update the product details page to allow the user to specify an image URL for the product and display it in the read-only view.</span></span> <span data-ttu-id="f72df-452">您将通过同步下载指定映像的本地副本。</span><span class="sxs-lookup"><span data-stu-id="f72df-452">You will create a local copy of the specified image by downloading it synchronously.</span></span> <span data-ttu-id="f72df-453">在下一任务中，您将更新此实现以使其以异步方式运行。</span><span class="sxs-lookup"><span data-stu-id="f72df-453">In the next task, you will update this implementation to make it work asynchronously.</span></span>

1. <span data-ttu-id="f72df-454">打开**Visual Studio 2012**并从该实验室的文件夹中加载位于**Source\Ex3-Async\Begin**的**开始**解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-454">Open **Visual Studio 2012** and load the **Begin** solution located in **Source\Ex3-Async\Begin** from this lab's folder.</span></span> <span data-ttu-id="f72df-455">或者，你可以继续处理前面练习中的现有解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-455">Alternatively, you can continue working on your existing solution from the previous exercises.</span></span>

   1. <span data-ttu-id="f72df-456">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="f72df-456">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="f72df-457">为此，请在解决方案资源管理器中单击 " **WebFormsLab** " 项目，并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-457">To do this, in the Solution Explorer, click the **WebFormsLab** project and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f72df-458">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="f72df-458">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="f72df-459">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-459">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="f72df-460">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="f72df-460">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="f72df-461">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="f72df-461">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="f72df-462">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="f72df-462">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="f72df-463">打开**ProductDetails**页源，并在 FormView 的 ItemTemplate 中添加一个字段，以显示产品映像。</span><span class="sxs-lookup"><span data-stu-id="f72df-463">Open the **ProductDetails.aspx** page source and add a field in the FormView's ItemTemplate to show the product image.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. <span data-ttu-id="f72df-464">添加字段以指定 FormView 的 EditTemplate 中的图像 URL。</span><span class="sxs-lookup"><span data-stu-id="f72df-464">Add a field to specify the image URL in the FormView's EditTemplate.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. <span data-ttu-id="f72df-465">打开**ProductDetails.aspx.cs**代码隐藏文件，并添加以下命名空间指令。</span><span class="sxs-lookup"><span data-stu-id="f72df-465">Open the **ProductDetails.aspx.cs** code-behind file and add the following namespace directives.</span></span>

    <span data-ttu-id="f72df-466">（代码段- *Web 窗体 Ex03-命名空间*）</span><span class="sxs-lookup"><span data-stu-id="f72df-466">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. <span data-ttu-id="f72df-467">创建**UpdateProductImage**方法，将远程映像存储在本地**images**文件夹中，并使用新的映像位置值更新 product 实体。</span><span class="sxs-lookup"><span data-stu-id="f72df-467">Create an **UpdateProductImage** method to store remote images in the local **Images** folder and update the product entity with the new image location value.</span></span>

    <span data-ttu-id="f72df-468">（代码段- *Web 窗体 Ex03-UpdateProductImage*）</span><span class="sxs-lookup"><span data-stu-id="f72df-468">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. <span data-ttu-id="f72df-469">更新**UpdateProduct**方法，以调用**UpdateProductImage**方法。</span><span class="sxs-lookup"><span data-stu-id="f72df-469">Update the **UpdateProduct** method to call the **UpdateProductImage** method.</span></span>

    <span data-ttu-id="f72df-470">（代码段- *Web 窗体 Ex03-UpdateProductImage 调用*）</span><span class="sxs-lookup"><span data-stu-id="f72df-470">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Call*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. <span data-ttu-id="f72df-471">运行应用程序并尝试上传产品的映像。</span><span class="sxs-lookup"><span data-stu-id="f72df-471">Run the application and try to upload an image for a product.</span></span> <span data-ttu-id="f72df-472">例如，可以使用 Office 剪贴画中的以下图像 URL： [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span><span class="sxs-lookup"><span data-stu-id="f72df-472">For example, you can use the following image URL from Office Clip Arts: [[http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)</span></span>

    <span data-ttu-id="f72df-473">![为产品设置图像](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "为产品设置图像")</span><span class="sxs-lookup"><span data-stu-id="f72df-473">![Setting an image for a product](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "Setting an image for a product")</span></span>

    <span data-ttu-id="f72df-474">*为产品设置图像*</span><span class="sxs-lookup"><span data-stu-id="f72df-474">*Setting an image for a product*</span></span>

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a><span data-ttu-id="f72df-475">任务 2-将异步处理添加到产品详细信息页</span><span class="sxs-lookup"><span data-stu-id="f72df-475">Task 2 - Adding Asynchronous Processing to the Product Details Page</span></span>

<span data-ttu-id="f72df-476">在此任务中，你将更新产品详细信息页，使其以异步方式运行。</span><span class="sxs-lookup"><span data-stu-id="f72df-476">In this task, you will update the product details page to make it work asynchronously.</span></span> <span data-ttu-id="f72df-477">你将通过使用 ASP.NET 4.5 异步页面处理来增强长时间运行的任务-映像下载过程。</span><span class="sxs-lookup"><span data-stu-id="f72df-477">You will enhance a long running task - the image download process - by using ASP.NET 4.5 asynchronous page processing.</span></span>

<span data-ttu-id="f72df-478">Web 应用程序中的异步方法可用于优化使用 ASP.NET 线程池的方式。</span><span class="sxs-lookup"><span data-stu-id="f72df-478">Asynchronous methods in web applications can be used to optimize the way ASP.NET thread pools are used.</span></span> <span data-ttu-id="f72df-479">在 ASP.NET 中，线程池中有有限数量的线程用于参与请求，因此，当所有线程都处于繁忙状态时，ASP.NET 将开始拒绝新请求，发送应用程序错误消息并使站点不可用。</span><span class="sxs-lookup"><span data-stu-id="f72df-479">In ASP.NET there are a limited number of threads in the thread pool for attending requests, thus, when all the threads are busy, ASP.NET starts to reject new requests, sends application error messages and makes your site unavailable.</span></span>

<span data-ttu-id="f72df-480">您的网站上的耗时操作非常适合用于异步编程，因为它们长时间占用了分配的线程。</span><span class="sxs-lookup"><span data-stu-id="f72df-480">Time-consuming operations on your web site are great candidates for asynchronous programming because they occupy the assigned thread for a long time.</span></span> <span data-ttu-id="f72df-481">这包括长时间运行的请求、包含大量不同元素的页和需要脱机操作的页，例如查询数据库或访问外部 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-481">This includes long running requests, pages with lots of different elements and pages that require offline operations, such querying a database or accessing an external web server.</span></span> <span data-ttu-id="f72df-482">优点在于，如果对这些操作使用异步方法，则在页正在处理时，线程将被释放并返回到线程池，并可用于参与到新的页面请求。</span><span class="sxs-lookup"><span data-stu-id="f72df-482">The advantage is that if you use asynchronous methods for these operations, while the page is processing, the thread is freed and returned to the thread pool and can be used to attend to a new page request.</span></span> <span data-ttu-id="f72df-483">这意味着，此页将在线程池的一个线程中开始处理，并可能在异步处理完成后在另一个线程中完成处理。</span><span class="sxs-lookup"><span data-stu-id="f72df-483">This means, the page will start processing in one thread from the thread pool and might complete processing in a different one, after the async processing completes.</span></span>

1. <span data-ttu-id="f72df-484">打开**ProductDetails**页。</span><span class="sxs-lookup"><span data-stu-id="f72df-484">Open the **ProductDetails.aspx** page.</span></span> <span data-ttu-id="f72df-485">在**Page**元素中添加**Async**特性，并将其设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="f72df-485">Add the **Async** attribute in the **Page** element and set it to **true**.</span></span> <span data-ttu-id="f72df-486">此属性告知 ASP.NET 实现 IHttpAsyncHandler 接口。</span><span class="sxs-lookup"><span data-stu-id="f72df-486">This attribute tells ASP.NET to implement the IHttpAsyncHandler interface.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. <span data-ttu-id="f72df-487">在页面底部添加标签以显示运行页面的线程的详细信息。</span><span class="sxs-lookup"><span data-stu-id="f72df-487">Add a Label at the bottom of the page to show the details of the threads running the page.</span></span>

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. <span data-ttu-id="f72df-488">打开**ProductDetails.aspx.cs**并添加以下命名空间指令。</span><span class="sxs-lookup"><span data-stu-id="f72df-488">Open up **ProductDetails.aspx.cs** and add the following namespace directives.</span></span>

    <span data-ttu-id="f72df-489">（代码段- *Web 窗体 Ex03-命名空间 2*）</span><span class="sxs-lookup"><span data-stu-id="f72df-489">(Code Snippet - *Web Forms Lab - Ex03 - Namespaces 2*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. <span data-ttu-id="f72df-490">修改**UpdateProductImage**方法以使用异步任务下载映像。</span><span class="sxs-lookup"><span data-stu-id="f72df-490">Modify the **UpdateProductImage** method to download the image with an asynchronous task.</span></span> <span data-ttu-id="f72df-491">将**WebClient** **DownloadFile**方法替换为**DownloadFileTaskAsync**方法，并包含**await**关键字。</span><span class="sxs-lookup"><span data-stu-id="f72df-491">You will replace the **WebClient** **DownloadFile** method with the **DownloadFileTaskAsync** method and include the **await** keyword.</span></span>

    <span data-ttu-id="f72df-492">（代码段- *Web 窗体 Ex03-UpdateProductImage Async*）</span><span class="sxs-lookup"><span data-stu-id="f72df-492">(Code Snippet - *Web Forms Lab - Ex03 - UpdateProductImage Async*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    <span data-ttu-id="f72df-493">Onendselect 注册要在不同的线程中执行的新页面异步任务。</span><span class="sxs-lookup"><span data-stu-id="f72df-493">The RegisterAsyncTask registers a new page asynchronous task to be executed in a different thread.</span></span> <span data-ttu-id="f72df-494">它将接收包含要执行的任务（t）的 lambda 表达式。</span><span class="sxs-lookup"><span data-stu-id="f72df-494">It receives a lambda expression with the Task (t) to be executed.</span></span> <span data-ttu-id="f72df-495">**DownloadFileTaskAsync**方法中的**await**关键字将方法的其余部分转换为在**DownloadFileTaskAsync**方法完成后异步调用的回调。</span><span class="sxs-lookup"><span data-stu-id="f72df-495">The **await** keyword in the **DownloadFileTaskAsync** method converts the remainder of the method into a callback that is invoked asynchronously after the **DownloadFileTaskAsync** method has completed.</span></span> <span data-ttu-id="f72df-496">ASP.NET 将自动维护所有 HTTP 请求的原始值，从而恢复方法的执行。</span><span class="sxs-lookup"><span data-stu-id="f72df-496">ASP.NET will resume the execution of the method by automatically maintaining all the HTTP request original values.</span></span> <span data-ttu-id="f72df-497">.NET 4.5 中的新异步编程模型使你能够编写类似于同步代码的异步代码，并让编译器处理回调函数或继续代码的复杂性。</span><span class="sxs-lookup"><span data-stu-id="f72df-497">The new asynchronous programming model in .NET 4.5 enables you to write asynchronous code that looks very much like synchronous code, and let the compiler handle the complications of callback functions or continuation code.</span></span>
    > [!NOTE]
    > <span data-ttu-id="f72df-498">自 .NET 2.0 起，Onendselect 和 PageAsyncTask 已可用。</span><span class="sxs-lookup"><span data-stu-id="f72df-498">RegisterAsyncTask and PageAsyncTask were already available since .NET 2.0.</span></span> <span data-ttu-id="f72df-499">Await 关键字是 .NET 4.5 异步编程模型中的新，可与 .NET WebClient 对象中的新 TaskAsync 方法一起使用。</span><span class="sxs-lookup"><span data-stu-id="f72df-499">The await keyword is new from the .NET 4.5 asynchronous programming model and can be used together with the new TaskAsync methods from the .NET WebClient object.</span></span>
5. <span data-ttu-id="f72df-500">添加代码以显示启动并完成执行代码的线程。</span><span class="sxs-lookup"><span data-stu-id="f72df-500">Add code to display the threads on which the code started and finished executing.</span></span> <span data-ttu-id="f72df-501">为此，请将**UpdateProductImage**方法更新为以下代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-501">To do this, update the **UpdateProductImage** method with the following code.</span></span>

    <span data-ttu-id="f72df-502">（代码段- *Web 窗体 Ex03-显示线程*）</span><span class="sxs-lookup"><span data-stu-id="f72df-502">(Code Snippet - *Web Forms Lab - Ex03 - Show threads*)</span></span>

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. <span data-ttu-id="f72df-503">打开**网站的 web.config 文件。**</span><span class="sxs-lookup"><span data-stu-id="f72df-503">Open the web site's **Web.config** file.</span></span> <span data-ttu-id="f72df-504">添加以下 appSetting 变量。</span><span class="sxs-lookup"><span data-stu-id="f72df-504">Add the following appSetting variable.</span></span>

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. <span data-ttu-id="f72df-505">按**F5**运行应用程序并上传产品的映像。</span><span class="sxs-lookup"><span data-stu-id="f72df-505">Press **F5** to run the application and upload an image for the product.</span></span> <span data-ttu-id="f72df-506">请注意，代码启动和完成的线程 ID 可能不同。</span><span class="sxs-lookup"><span data-stu-id="f72df-506">Notice the threads ID where the code started and finished may be different.</span></span> <span data-ttu-id="f72df-507">这是因为异步任务在 ASP.NET 线程池的单独线程上运行。</span><span class="sxs-lookup"><span data-stu-id="f72df-507">This is because asynchronous tasks run on a separate thread from ASP.NET thread pool.</span></span> <span data-ttu-id="f72df-508">任务完成后，ASP.NET 会将任务放回队列中并分配任何可用线程。</span><span class="sxs-lookup"><span data-stu-id="f72df-508">When the task completes, ASP.NET puts the task back in the queue and assigns any of the available threads.</span></span>

    <span data-ttu-id="f72df-509">![异步下载图像](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "异步下载图像")</span><span class="sxs-lookup"><span data-stu-id="f72df-509">![Downloading an image asynchronously](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "Downloading an image asynchronously")</span></span>

    <span data-ttu-id="f72df-510">*异步下载图像*</span><span class="sxs-lookup"><span data-stu-id="f72df-510">*Downloading an image asynchronously*</span></span>

> [!NOTE]
> <span data-ttu-id="f72df-511">此外，你可以遵循[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序](#AppendixB)，将此应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f72df-511">Additionally, you can deploy this application to Azure following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="f72df-512">摘要</span><span class="sxs-lookup"><span data-stu-id="f72df-512">Summary</span></span>

<span data-ttu-id="f72df-513">在此动手实验中，已解决并演示了以下概念：</span><span class="sxs-lookup"><span data-stu-id="f72df-513">In this hands-on lab, the following concepts have been addressed and demonstrated:</span></span>

- <span data-ttu-id="f72df-514">使用强类型化的数据绑定表达式</span><span class="sxs-lookup"><span data-stu-id="f72df-514">Use strongly-typed data-binding expressions</span></span>
- <span data-ttu-id="f72df-515">在 Web 窗体中使用新的模型绑定功能</span><span class="sxs-lookup"><span data-stu-id="f72df-515">Use new model binding features in Web Forms</span></span>
- <span data-ttu-id="f72df-516">使用值提供程序将页面数据映射到代码隐藏方法</span><span class="sxs-lookup"><span data-stu-id="f72df-516">Use value providers for mapping page data to code-behind methods</span></span>
- <span data-ttu-id="f72df-517">使用数据批注进行用户输入验证</span><span class="sxs-lookup"><span data-stu-id="f72df-517">Use Data Annotations for user input validation</span></span>
- <span data-ttu-id="f72df-518">通过 Web 窗体中的 jQuery 利用不引人注目的客户端验证</span><span class="sxs-lookup"><span data-stu-id="f72df-518">Take advantage of unobtrusive client-side validation with jQuery in Web Forms</span></span>
- <span data-ttu-id="f72df-519">实现精细请求验证</span><span class="sxs-lookup"><span data-stu-id="f72df-519">Implement granular request validation</span></span>
- <span data-ttu-id="f72df-520">在 Web 窗体中实现异步页面处理</span><span class="sxs-lookup"><span data-stu-id="f72df-520">Implement asynchronous page processing in Web Forms</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="f72df-521">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="f72df-521">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="f72df-522">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-522">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="f72df-523">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="f72df-523">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="f72df-524">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="f72df-524">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="f72df-525">或者，如果你已经安装了 Web 平台安装程序，则可以打开它，并<em>使用 AZURE SDK&quot;搜索 Visual Studio Express 2012 For web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="f72df-525">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="f72df-526">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-526">Click on **Install Now**.</span></span> <span data-ttu-id="f72df-527">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="f72df-527">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="f72df-528">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-528">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="f72df-529">![安装 Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="f72df-529">![Install Visual Studio Express](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="f72df-530">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="f72df-530">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="f72df-531">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="f72df-531">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    <span data-ttu-id="f72df-533">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="f72df-533">*Accepting the license terms*</span></span>
5. <span data-ttu-id="f72df-534">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="f72df-534">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    <span data-ttu-id="f72df-536">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="f72df-536">*Installation progress*</span></span>
6. <span data-ttu-id="f72df-537">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-537">When the installation completes, click **Finish**.</span></span>

    ![安装完成](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    <span data-ttu-id="f72df-539">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="f72df-539">*Installation completed*</span></span>
7. <span data-ttu-id="f72df-540">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-540">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="f72df-541">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="f72df-541">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    <span data-ttu-id="f72df-543">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="f72df-543">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f72df-544">附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="f72df-544">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="f72df-545">本附录将演示如何从 Azure 门户创建新网站，以及如何利用 Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-545">This appendix will show you how to create a new web site from the Azure Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a><span data-ttu-id="f72df-546">任务 1-从 Azure 门户创建新网站</span><span class="sxs-lookup"><span data-stu-id="f72df-546">Task 1 - Creating a New Web Site from the Azure Portal</span></span>

1. <span data-ttu-id="f72df-547">请使用[Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="f72df-547">Go to the [Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-548">借助 Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。</span><span class="sxs-lookup"><span data-stu-id="f72df-548">With Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="f72df-549">你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。</span><span class="sxs-lookup"><span data-stu-id="f72df-549">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="f72df-550">![登录到 Windows Azure 门户](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "登录到 Microsoft Azure 门户")</span><span class="sxs-lookup"><span data-stu-id="f72df-550">![Log on to Windows Azure portal](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="f72df-551">*登录到门户*</span><span class="sxs-lookup"><span data-stu-id="f72df-551">*Log on to the Portal*</span></span>
2. <span data-ttu-id="f72df-552">单击命令栏上的 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-552">Click **New** on the command bar.</span></span>

    <span data-ttu-id="f72df-553">![创建新网站](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "创建新网站")</span><span class="sxs-lookup"><span data-stu-id="f72df-553">![Creating a new Web Site](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="f72df-554">*创建新网站*</span><span class="sxs-lookup"><span data-stu-id="f72df-554">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="f72df-555">单击 "**计算** | **网站**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-555">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="f72df-556">然后选择 "**快速创建**" 选项。</span><span class="sxs-lookup"><span data-stu-id="f72df-556">Then select **Quick Create** option.</span></span> <span data-ttu-id="f72df-557">为新网站提供可用 URL，并单击 "**创建**网站"。</span><span class="sxs-lookup"><span data-stu-id="f72df-557">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-558">Azure 是在云中运行的 web 应用程序的宿主，你可以控制和管理这些应用程序。</span><span class="sxs-lookup"><span data-stu-id="f72df-558">Azure is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="f72df-559">使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f72df-559">The Quick Create option allows you to deploy a completed web application to the Azure from outside the portal.</span></span> <span data-ttu-id="f72df-560">它不包括设置数据库的步骤。</span><span class="sxs-lookup"><span data-stu-id="f72df-560">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="f72df-561">![使用 "快速创建" 创建新网站](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "使用“快速创建”创建新网站")</span><span class="sxs-lookup"><span data-stu-id="f72df-561">![Creating a new Web Site using Quick Create](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="f72df-562">*使用 "快速创建" 创建新网站*</span><span class="sxs-lookup"><span data-stu-id="f72df-562">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="f72df-563">请**等到新网站创建完毕。**</span><span class="sxs-lookup"><span data-stu-id="f72df-563">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="f72df-564">创建网站后，单击 " **URL** " 列下的链接。</span><span class="sxs-lookup"><span data-stu-id="f72df-564">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="f72df-565">检查新网站是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="f72df-565">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="f72df-566">![浏览到新网站](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "浏览到新网站")</span><span class="sxs-lookup"><span data-stu-id="f72df-566">![Browsing to the new web site](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="f72df-567">*浏览到新网站*</span><span class="sxs-lookup"><span data-stu-id="f72df-567">*Browsing to the new web site*</span></span>

    <span data-ttu-id="f72df-568">![网站正在运行](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "网站正在运行")</span><span class="sxs-lookup"><span data-stu-id="f72df-568">![Web site running](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "Web site running")</span></span>

    <span data-ttu-id="f72df-569">*网站正在运行*</span><span class="sxs-lookup"><span data-stu-id="f72df-569">*Web site running*</span></span>
6. <span data-ttu-id="f72df-570">返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。</span><span class="sxs-lookup"><span data-stu-id="f72df-570">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="f72df-571">![打开网站管理页](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "打开网站管理页")</span><span class="sxs-lookup"><span data-stu-id="f72df-571">![Opening the web site management pages](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="f72df-572">*打开网站管理页*</span><span class="sxs-lookup"><span data-stu-id="f72df-572">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="f72df-573">在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。</span><span class="sxs-lookup"><span data-stu-id="f72df-573">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-574">*发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 Azure 所需的所有信息。</span><span class="sxs-lookup"><span data-stu-id="f72df-574">The *publish profile* contains all of the information required to publish a web application to Azure for each enabled publication method.</span></span> <span data-ttu-id="f72df-575">发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。</span><span class="sxs-lookup"><span data-stu-id="f72df-575">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="f72df-576">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f72df-576">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Azure.</span></span>

    <span data-ttu-id="f72df-577">![下载网站发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "下载网站发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f72df-577">![Downloading the web site publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="f72df-578">*下载网站发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f72df-578">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="f72df-579">将发布配置文件下载到已知位置。</span><span class="sxs-lookup"><span data-stu-id="f72df-579">Download the publish profile file to a known location.</span></span> <span data-ttu-id="f72df-580">在本练习中，你将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f72df-580">Further in this exercise you will see how to use this file to publish a web application to Azure from Visual Studio.</span></span>

    <span data-ttu-id="f72df-581">![正在保存发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "正在保存发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f72df-581">![Saving the publish profile file](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "Saving the publish profile")</span></span>

    <span data-ttu-id="f72df-582">*正在保存发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f72df-582">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="f72df-583">任务 2-配置数据库服务器</span><span class="sxs-lookup"><span data-stu-id="f72df-583">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="f72df-584">如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-584">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="f72df-585">如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。</span><span class="sxs-lookup"><span data-stu-id="f72df-585">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="f72df-586">你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-586">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="f72df-587">可以在 Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 Azure 管理门户中查看 sql 数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-587">You can view the SQL Database servers from your subscription in the Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="f72df-588">如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。</span><span class="sxs-lookup"><span data-stu-id="f72df-588">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="f72df-589">记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。</span><span class="sxs-lookup"><span data-stu-id="f72df-589">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="f72df-590">请不要创建数据库，因为它将在后面的阶段创建。</span><span class="sxs-lookup"><span data-stu-id="f72df-590">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="f72df-591">![SQL 数据库服务器仪表板](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL 数据库服务器仪表板")</span><span class="sxs-lookup"><span data-stu-id="f72df-591">![SQL Database Server Dashboard](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="f72df-592">*SQL 数据库服务器仪表板*</span><span class="sxs-lookup"><span data-stu-id="f72df-592">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="f72df-593">在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。</span><span class="sxs-lookup"><span data-stu-id="f72df-593">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="f72df-594">为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](whats-new-in-web-forms-in-aspnet-45/_static/image39.png)" 按钮。</span><span class="sxs-lookup"><span data-stu-id="f72df-594">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) button.</span></span>

    ![添加客户端 IP 地址](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    <span data-ttu-id="f72df-596">*添加客户端 IP 地址*</span><span class="sxs-lookup"><span data-stu-id="f72df-596">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="f72df-597">将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。</span><span class="sxs-lookup"><span data-stu-id="f72df-597">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![确认更改](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    <span data-ttu-id="f72df-599">*确认更改*</span><span class="sxs-lookup"><span data-stu-id="f72df-599">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="f72df-600">任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序</span><span class="sxs-lookup"><span data-stu-id="f72df-600">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="f72df-601">返回到 ASP.NET MVC 4 解决方案。</span><span class="sxs-lookup"><span data-stu-id="f72df-601">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="f72df-602">在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-602">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="f72df-603">![发布应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "发布应用程序")</span><span class="sxs-lookup"><span data-stu-id="f72df-603">![Publishing the Application](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "Publishing the Application")</span></span>

    <span data-ttu-id="f72df-604">*发布网站*</span><span class="sxs-lookup"><span data-stu-id="f72df-604">*Publishing the web site*</span></span>
2. <span data-ttu-id="f72df-605">导入您在第一个任务中保存的发布配置文件。</span><span class="sxs-lookup"><span data-stu-id="f72df-605">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="f72df-606">![导入发布配置文件](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "导入发布配置文件")</span><span class="sxs-lookup"><span data-stu-id="f72df-606">![Importing the publish profile](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "Importing the publish profile")</span></span>

    <span data-ttu-id="f72df-607">*导入发布配置文件*</span><span class="sxs-lookup"><span data-stu-id="f72df-607">*Importing publish profile*</span></span>
3. <span data-ttu-id="f72df-608">单击 "**验证连接**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-608">Click **Validate Connection**.</span></span> <span data-ttu-id="f72df-609">验证完成后，单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-609">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f72df-610">验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。</span><span class="sxs-lookup"><span data-stu-id="f72df-610">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="f72df-611">![正在验证连接](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "正在验证连接")</span><span class="sxs-lookup"><span data-stu-id="f72df-611">![Validating connection](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "Validating connection")</span></span>

    <span data-ttu-id="f72df-612">*正在验证连接*</span><span class="sxs-lookup"><span data-stu-id="f72df-612">*Validating connection*</span></span>
4. <span data-ttu-id="f72df-613">在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="f72df-613">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="f72df-614">![Web 部署配置](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web 部署配置")</span><span class="sxs-lookup"><span data-stu-id="f72df-614">![Web deploy configuration](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "Web deploy configuration")</span></span>

    <span data-ttu-id="f72df-615">*Web 部署配置*</span><span class="sxs-lookup"><span data-stu-id="f72df-615">*Web deploy configuration*</span></span>
5. <span data-ttu-id="f72df-616">按如下所示配置数据库连接：</span><span class="sxs-lookup"><span data-stu-id="f72df-616">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="f72df-617">在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。</span><span class="sxs-lookup"><span data-stu-id="f72df-617">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="f72df-618">在 "**用户名**" 中键入服务器管理员登录名。</span><span class="sxs-lookup"><span data-stu-id="f72df-618">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="f72df-619">在 "**密码**" 中键入服务器管理员登录密码。</span><span class="sxs-lookup"><span data-stu-id="f72df-619">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="f72df-620">键入新的数据库名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-620">Type a new database name.</span></span>

     <span data-ttu-id="f72df-621">![正在配置目标连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "正在配置目标连接字符串")</span><span class="sxs-lookup"><span data-stu-id="f72df-621">![Configuring destination connection string](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="f72df-622">*正在配置目标连接字符串*</span><span class="sxs-lookup"><span data-stu-id="f72df-622">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="f72df-623">然后单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-623">Then click **OK**.</span></span> <span data-ttu-id="f72df-624">系统提示创建数据库时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-624">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="f72df-625">![创建数据库](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "创建数据库字符串")</span><span class="sxs-lookup"><span data-stu-id="f72df-625">![Creating the database](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "Creating the database string")</span></span>

    <span data-ttu-id="f72df-626">*创建数据库*</span><span class="sxs-lookup"><span data-stu-id="f72df-626">*Creating the database*</span></span>
7. <span data-ttu-id="f72df-627">将用于连接到 Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。</span><span class="sxs-lookup"><span data-stu-id="f72df-627">The connection string you will use to connect to SQL Database in Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="f72df-628">再单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-628">Then click **Next**.</span></span>

    <span data-ttu-id="f72df-629">![指向 SQL 数据库的连接字符串](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "指向 SQL 数据库的连接字符串")</span><span class="sxs-lookup"><span data-stu-id="f72df-629">![Connection string pointing to SQL Database](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="f72df-630">*指向 SQL 数据库的连接字符串*</span><span class="sxs-lookup"><span data-stu-id="f72df-630">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="f72df-631">在 "**预览**" 页上，单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="f72df-631">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="f72df-632">![发布 web 应用程序](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "发布 web 应用程序")</span><span class="sxs-lookup"><span data-stu-id="f72df-632">![Publishing the web application](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "Publishing the web application")</span></span>

    <span data-ttu-id="f72df-633">*发布 web 应用程序*</span><span class="sxs-lookup"><span data-stu-id="f72df-633">*Publishing the web application*</span></span>
9. <span data-ttu-id="f72df-634">发布过程完成后，您的默认浏览器将打开已发布的网站。</span><span class="sxs-lookup"><span data-stu-id="f72df-634">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="f72df-635">附录 C：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="f72df-635">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="f72df-636">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="f72df-636">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="f72df-637">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="f72df-637">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="f72df-638">![使用 Visual Studio code 代码段将代码插入到项目中](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="f72df-638">![Using Visual Studio code snippets to insert code into your project](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="f72df-639">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="f72df-639">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="f72df-640">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="f72df-640">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="f72df-641">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="f72df-641">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="f72df-642">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="f72df-642">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="f72df-643">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="f72df-643">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="f72df-644">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="f72df-644">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="f72df-645">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="f72df-645">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="f72df-646">![开始键入代码片段名称](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="f72df-646">![Start typing the snippet name](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "Start typing the snippet name")</span></span>

<span data-ttu-id="f72df-647">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="f72df-647">*Start typing the snippet name*</span></span>

<span data-ttu-id="f72df-648">![按 Tab 键以选择突出显示的代码段](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="f72df-648">![Press Tab to select the highlighted snippet](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="f72df-649">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="f72df-649">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="f72df-650">![再次按 Tab 键，代码片段将展开](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="f72df-650">![Press Tab again and the snippet will expand](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="f72df-651">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="f72df-651">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="f72df-652">***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2.</span><span class="sxs-lookup"><span data-stu-id="f72df-652">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="f72df-653">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="f72df-653">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="f72df-654">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="f72df-654">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="f72df-655">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="f72df-655">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="f72df-656">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="f72df-656">![Right-click where you want to insert the code snippet and select Insert Snippet](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="f72df-657">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="f72df-657">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="f72df-658">![通过单击从列表中选择相关的代码片段](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="f72df-658">![Pick the relevant snippet from the list, by clicking on it](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="f72df-659">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="f72df-659">*Pick the relevant snippet from the list, by clicking on it*</span></span>
