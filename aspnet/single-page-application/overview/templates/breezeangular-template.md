---
uid: single-page-application/overview/templates/breezeangular-template
title: 轻松/角度模板 |Microsoft Docs
author: madskristensen
description: 轻松/角度单页面应用程序模板
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467186"
---
# <a name="breezeangular-template"></a><span data-ttu-id="5c13e-103">Breeze/Angular 模板</span><span class="sxs-lookup"><span data-stu-id="5c13e-103">Breeze/Angular template</span></span>

<span data-ttu-id="5c13e-104">作者： [Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="5c13e-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="5c13e-105">Ward 电铃编写了简单/角度 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="5c13e-105">The Breeze/Angular MVC Template was written by Ward Bell</span></span>
> 
> [<span data-ttu-id="5c13e-106">下载轻松/角度 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="5c13e-106">Download the Breeze/Angular MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=286437)

<span data-ttu-id="5c13e-107">[AngularJS](http://angularjs.org)是 Google 的开源库，用于构建单页应用程序（spa）。</span><span class="sxs-lookup"><span data-stu-id="5c13e-107">[AngularJS](http://angularjs.org) is an open source library from Google for building Single Page Applications (SPAs).</span></span> <span data-ttu-id="5c13e-108">它提供数据绑定、依赖关系注入和屏幕管理。</span><span class="sxs-lookup"><span data-stu-id="5c13e-108">It offers data binding, dependency injection, and screen management.</span></span> <span data-ttu-id="5c13e-109">将其与[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)、用于数据建模和数据管理的另一个开源库相结合，并为强大的 HTML/JavaScript 客户端应用程序提供重要的组成部分。</span><span class="sxs-lookup"><span data-stu-id="5c13e-109">Combine it with [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), another open source library for data modeling and data management, and you have the essential ingredients for a great HTML/JavaScript client app.</span></span>

<span data-ttu-id="5c13e-110">"轻松/角 SPA" 模板是 ASP.NET 和 Web 工具2012.2 更新中包含的[KNOCKOUTJS SPA 模板](../introduction/knockoutjs-template.md)上的一个变体。</span><span class="sxs-lookup"><span data-stu-id="5c13e-110">The Breeze/Angular SPA template is a variation on the [KnockoutJS SPA template](../introduction/knockoutjs-template.md) included in the ASP.NET and Web Tools 2012.2 Update.</span></span> <span data-ttu-id="5c13e-111">如果有 Visual Studio，则会在60秒内启动并运行一个示例 SPA。</span><span class="sxs-lookup"><span data-stu-id="5c13e-111">If you've got Visual Studio, you'll have an example SPA up and running in less than 60 seconds.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

<span data-ttu-id="5c13e-112">表面，应用程序看起来与 KnockoutJS SPA 模板非常类似。</span><span class="sxs-lookup"><span data-stu-id="5c13e-112">Outwardly, the application looks the very similar to the KnockoutJS SPA template.</span></span> <span data-ttu-id="5c13e-113">但在这种情况下，它的差别很大。</span><span class="sxs-lookup"><span data-stu-id="5c13e-113">But it's quite different under the hood.</span></span> <span data-ttu-id="5c13e-114">KnockoutJS 模板对数据绑定和原始 AJAX 使用挖空以实现数据访问。</span><span class="sxs-lookup"><span data-stu-id="5c13e-114">The KnockoutJS template uses Knockout for data binding and raw AJAX for data access.</span></span> <span data-ttu-id="5c13e-115">轻松/角度模板使用角度进行数据绑定，并使数据访问更加轻松。</span><span class="sxs-lookup"><span data-stu-id="5c13e-115">The Breeze/Angular template uses Angular for data binding and Breeze for data access.</span></span> <span data-ttu-id="5c13e-116">这些库可实现其他功能，包括页面导航和历史记录。</span><span class="sxs-lookup"><span data-stu-id="5c13e-116">These libraries enable additional capabilities, including page navigation and history.</span></span>

<span data-ttu-id="5c13e-117">下面是应用程序的 "关于" 页：</span><span class="sxs-lookup"><span data-stu-id="5c13e-117">Here is the application's About page:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

<span data-ttu-id="5c13e-118">此页显示当前用户会话期间运行的事件日志，包括：</span><span class="sxs-lookup"><span data-stu-id="5c13e-118">This page displays a running log of events during the current user session, including:</span></span>

- <span data-ttu-id="5c13e-119">分页.</span><span class="sxs-lookup"><span data-stu-id="5c13e-119">Paging.</span></span> <span data-ttu-id="5c13e-120">请注意在 #2 和 #7 创建 Todo 控制器。</span><span class="sxs-lookup"><span data-stu-id="5c13e-120">Note the Todo controller creation at #2 and #7.</span></span>
- <span data-ttu-id="5c13e-121">远程查询（#3）和本地缓存查询（#7）。</span><span class="sxs-lookup"><span data-stu-id="5c13e-121">Remote queries (#3) and local cache queries (#7).</span></span>
- <span data-ttu-id="5c13e-122">保存新的（#5、#6）和已修改（#4）实体。</span><span class="sxs-lookup"><span data-stu-id="5c13e-122">Saving new (#5, #6) and modified (#4) entities.</span></span>
- <span data-ttu-id="5c13e-123">已在客户端上验证更改（#9），因此用户可以在将更改提交到数据库之前更正错误。</span><span class="sxs-lookup"><span data-stu-id="5c13e-123">Changes validated on the client (#9), so the user can correct mistakes before committing changes to the database.</span></span>

<span data-ttu-id="5c13e-124">此模板中还有更多内容可供浏览，其中包括：</span><span class="sxs-lookup"><span data-stu-id="5c13e-124">There's more to explore in this template, including:</span></span>

- <span data-ttu-id="5c13e-125">动态加载 HTML 视图模板。</span><span class="sxs-lookup"><span data-stu-id="5c13e-125">Dynamic loading of HTML view templates.</span></span>
- <span data-ttu-id="5c13e-126">通过角 "指令" 自定义数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5c13e-126">Custom data binding through Angular "directives."</span></span>
- <span data-ttu-id="5c13e-127">模块化和依赖关系注入。</span><span class="sxs-lookup"><span data-stu-id="5c13e-127">Modularity and dependency injection.</span></span>
- <span data-ttu-id="5c13e-128">查询筛选器、排序、分页、预测和包含相关实体。</span><span class="sxs-lookup"><span data-stu-id="5c13e-128">Query filters, sorts, paging, projections, and inclusion of related entities.</span></span>
- <span data-ttu-id="5c13e-129">跨多个屏幕共享数据。</span><span class="sxs-lookup"><span data-stu-id="5c13e-129">Sharing data across multiple screens.</span></span>
- <span data-ttu-id="5c13e-130">将多个更改保存为一个事务。</span><span class="sxs-lookup"><span data-stu-id="5c13e-130">Saving multiple changes as a single transaction.</span></span>
- <span data-ttu-id="5c13e-131">从服务器自动传播到 JavaScript 客户端的验证规则。</span><span class="sxs-lookup"><span data-stu-id="5c13e-131">Validation rules propagated automatically from the server to the JavaScript client.</span></span>

<span data-ttu-id="5c13e-132">让我们开始吧。</span><span class="sxs-lookup"><span data-stu-id="5c13e-132">Let's get started.</span></span>

## <a name="create-a-breezeangular-template-project"></a><span data-ttu-id="5c13e-133">创建一个简单的模板项目</span><span class="sxs-lookup"><span data-stu-id="5c13e-133">Create a Breeze/Angular Template Project</span></span>

<span data-ttu-id="5c13e-134">单击上面的 "下载" 按钮，下载并安装模板。</span><span class="sxs-lookup"><span data-stu-id="5c13e-134">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="5c13e-135">模板打包为 Visual Studio 扩展（VSIX）文件。</span><span class="sxs-lookup"><span data-stu-id="5c13e-135">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="5c13e-136">可能需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="5c13e-136">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="5c13e-137">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="5c13e-137">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="5c13e-138">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="5c13e-138">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="5c13e-139">在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="5c13e-139">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="5c13e-140">命名项目并单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="5c13e-140">Name the project and click **OK**.</span></span>

<span data-ttu-id="5c13e-141">在 "**新建项目**" 向导中，选择 "**轻松角 SPA**"。</span><span class="sxs-lookup"><span data-stu-id="5c13e-141">In the **New Project** wizard, select **Breeze Angular SPA**.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

<span data-ttu-id="5c13e-142">按 Ctrl-F5 以生成并运行应用程序而不进行调试，或按 F5 运行调试。</span><span class="sxs-lookup"><span data-stu-id="5c13e-142">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

<span data-ttu-id="5c13e-143">当应用程序首次运行时，它将显示登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="5c13e-143">When the application first runs, it displays a login screen.</span></span> <span data-ttu-id="5c13e-144">单击 "注册" 链接和新页面 glides 进入 "查看"，可在其中输入用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="5c13e-144">Click the "Sign up" link and a new page glides into view, where you can enter a username and password.</span></span> <span data-ttu-id="5c13e-145">（登录名和注册页是使用 ASP.NET MVC 生成的。）提交注册表单后，服务器会生成 TodoList，其中包含两个适用于你的帐户的项目。</span><span class="sxs-lookup"><span data-stu-id="5c13e-145">(The login and registration pages are built using ASP.NET MVC.) When you submit the registration form, the server generates a TodoList with two items for your account.</span></span> <span data-ttu-id="5c13e-146">然后，它会显示一个黄色便笺。</span><span class="sxs-lookup"><span data-stu-id="5c13e-146">Then it presents them to you on a yellow note.</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

<span data-ttu-id="5c13e-147">现在你处于 SPA 的土地。</span><span class="sxs-lookup"><span data-stu-id="5c13e-147">Now you are in the land of SPA.</span></span> <span data-ttu-id="5c13e-148">在客户端上，在操作 Todo 时所看到和管理的所有内容都将在客户端上呈现并管理。</span><span class="sxs-lookup"><span data-stu-id="5c13e-148">Everything you see and experience while manipulating Todos is rendered and managed on the client with the help of Knockout and Breeze.</span></span> <span data-ttu-id="5c13e-149">以用户身份浏览应用 。</span><span class="sxs-lookup"><span data-stu-id="5c13e-149">Explore the app as a user …</span></span> <span data-ttu-id="5c13e-150">但对于开发人员而言，</span><span class="sxs-lookup"><span data-stu-id="5c13e-150">but with a developer's eye.</span></span> <span data-ttu-id="5c13e-151">使用浏览器中的开发人员工具来捕获网络流量。</span><span class="sxs-lookup"><span data-stu-id="5c13e-151">Use the developer tools in your browser to capture the network traffic.</span></span> <span data-ttu-id="5c13e-152">（在 Internet Explorer 中：按 F12，选择 "**网络**" 选项卡，然后单击 "**开始捕获**"。）现在，请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="5c13e-152">(In Internet Explorer: Press F12, select the **Network** tab, and click **Start capturing**.) Now try the following:</span></span>

- <span data-ttu-id="5c13e-153">添加新的 Todo 项。</span><span class="sxs-lookup"><span data-stu-id="5c13e-153">Add a new Todo item.</span></span>
- <span data-ttu-id="5c13e-154">单击标签，然后编辑 Todo 项标题</span><span class="sxs-lookup"><span data-stu-id="5c13e-154">Click the label and edit the Todo item title</span></span>
- <span data-ttu-id="5c13e-155">选中复选框可将项目标记为已完成。</span><span class="sxs-lookup"><span data-stu-id="5c13e-155">Check a checkbox to mark the item done.</span></span> <span data-ttu-id="5c13e-156">请注意，textbox 处于禁用状态，因此不能再编辑标题。</span><span class="sxs-lookup"><span data-stu-id="5c13e-156">Notice that the textbox is disabled, so the title is no longer editable.</span></span>
- <span data-ttu-id="5c13e-157">单击标签右侧的 "x"。</span><span class="sxs-lookup"><span data-stu-id="5c13e-157">Click the ‘x' to the right of the label.</span></span> <span data-ttu-id="5c13e-158">该项将消失，并从数据库中删除。</span><span class="sxs-lookup"><span data-stu-id="5c13e-158">The item disappears and is deleted from the database.</span></span>
- <span data-ttu-id="5c13e-159">选取另一项并清除其标题。</span><span class="sxs-lookup"><span data-stu-id="5c13e-159">Pick another item and clear its title.</span></span> <span data-ttu-id="5c13e-160">您将收到一个验证错误，指出标题是必需的。</span><span class="sxs-lookup"><span data-stu-id="5c13e-160">You'll get a validation error that the title is required.</span></span> <span data-ttu-id="5c13e-161">短暂暂停后，将还原以前的标题。</span><span class="sxs-lookup"><span data-stu-id="5c13e-161">After a brief pause, the previous title is restored.</span></span>
- <span data-ttu-id="5c13e-162">键入十分长标题。</span><span class="sxs-lookup"><span data-stu-id="5c13e-162">Type in a ridiculously long title.</span></span> <span data-ttu-id="5c13e-163">你会收到其他验证错误，指出标题太长。</span><span class="sxs-lookup"><span data-stu-id="5c13e-163">You'll get a different validation error that the title is too long.</span></span>
- <span data-ttu-id="5c13e-164">单击 "添加待办事项列表" 按钮。</span><span class="sxs-lookup"><span data-stu-id="5c13e-164">Click the "Add Todo List" button.</span></span> <span data-ttu-id="5c13e-165">新列表将显示在上一个列表的左侧。</span><span class="sxs-lookup"><span data-stu-id="5c13e-165">A new list appears to the left of the previous list.</span></span>
- <span data-ttu-id="5c13e-166">播放 TodoList 标题，触发其所需和长度的验证。</span><span class="sxs-lookup"><span data-stu-id="5c13e-166">Play with the TodoList title, triggering its required and length validations.</span></span>
- <span data-ttu-id="5c13e-167">在标题文本框中单击以清除错误消息。</span><span class="sxs-lookup"><span data-stu-id="5c13e-167">Click in the title textbox to clear the error message.</span></span>
- <span data-ttu-id="5c13e-168">单击右上角圆圈中的 "x" 以删除 TodoList 及其 todo。</span><span class="sxs-lookup"><span data-stu-id="5c13e-168">Click the "x" in the circle in the upper right corner to delete the TodoList and its todos.</span></span>
- <span data-ttu-id="5c13e-169">单击右上角的 "关于" 链接可查看这些活动的日志。</span><span class="sxs-lookup"><span data-stu-id="5c13e-169">Click the "About" link in the upper right to see a log of these activities.</span></span>

<span data-ttu-id="5c13e-170">验证逻辑通过简单地执行客户端。</span><span class="sxs-lookup"><span data-stu-id="5c13e-170">The validation logic is performed client-side by Breeze.</span></span> <span data-ttu-id="5c13e-171">服务器模型类上的验证特性传播到客户端，并在客户端与服务器联系之前自动执行。</span><span class="sxs-lookup"><span data-stu-id="5c13e-171">Validation attributes on the server model classes are propagated to the client and executed automatically before the client contacts the server.</span></span>

<span data-ttu-id="5c13e-172">查看网络流量。</span><span class="sxs-lookup"><span data-stu-id="5c13e-172">Review the network traffic.</span></span> <span data-ttu-id="5c13e-173">请注意，当出错时，没有对服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="5c13e-173">Notice that there were no calls to the server when Breeze detected an error.</span></span> <span data-ttu-id="5c13e-174">每个有效的更改都导致向 "/api/Todo/SaveChanges" 发出 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="5c13e-174">Each valid change resulted in a POST request to "/api/Todo/SaveChanges".</span></span> <span data-ttu-id="5c13e-175">轻松绑定更改，并将其作为单个请求发送到 Web API 控制器的 `SaveChanges` 方法。</span><span class="sxs-lookup"><span data-stu-id="5c13e-175">Breeze bundles the changes and sends them together as a single request to the Web API controller's `SaveChanges` method.</span></span> <span data-ttu-id="5c13e-176">这不同于 KnockoutJS SPA 模板，后者分别对每个项发出 PUT、POST 和 DELETE 请求。</span><span class="sxs-lookup"><span data-stu-id="5c13e-176">That's different from KnockoutJS SPA template, which makes PUT, POST, and DELETE requests for each item individually.</span></span>

<span data-ttu-id="5c13e-177">另外，请注意，当你在 TodoList 和 About 页面之间切换时，没有任何网络流量。</span><span class="sxs-lookup"><span data-stu-id="5c13e-177">Also, notice there is no network traffic when you switch between the TodoList and About pages.</span></span> <span data-ttu-id="5c13e-178">这是因为该查询已被限制为本地简单缓存。</span><span class="sxs-lookup"><span data-stu-id="5c13e-178">That's because the query has been constrained to the local Breeze cache.</span></span>

## <a name="peek-inside"></a><span data-ttu-id="5c13e-179">查看内部</span><span class="sxs-lookup"><span data-stu-id="5c13e-179">Peek inside</span></span>

<span data-ttu-id="5c13e-180">此应用程序具有客户端和服务器端。</span><span class="sxs-lookup"><span data-stu-id="5c13e-180">This application has a client side and a server side.</span></span> <span data-ttu-id="5c13e-181">客户端堆栈包含一小部分 HTML 和应用程序 JavaScript 模块（在 "应用" 文件夹中）和第三方 JavaScript 库（在 "脚本" 文件夹中）的组合。</span><span class="sxs-lookup"><span data-stu-id="5c13e-181">The client-side stack consists of a little HTML and a combination of application JavaScript modules (in the "app" folder) plus third-party JavaScript libraries (in the "Scripts" folder).</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

<span data-ttu-id="5c13e-182">UI 体系结构将视图的 HTML 小组件与控制器中的支持表示代码分开。</span><span class="sxs-lookup"><span data-stu-id="5c13e-182">The UI architecture separates the HTML widgets of the views from the supporting presentation code in the controllers.</span></span> <span data-ttu-id="5c13e-183">角数据绑定系统协调视图和控制器，以便每个视图和控制器都可以执行其作业，而无需对其他项进行深入了解。</span><span class="sxs-lookup"><span data-stu-id="5c13e-183">The Angular data-binding system coordinates views and controllers so that each can do its job without intimate knowledge of the other.</span></span>

<span data-ttu-id="5c13e-184">控制器要求数据上下文获取并保存模型实体。</span><span class="sxs-lookup"><span data-stu-id="5c13e-184">The controller asks the data context to acquire and save the model entities.</span></span> <span data-ttu-id="5c13e-185">数据上下文将大部分工作委托给很多工作，这将从 JSON 查询结果构造自我跟踪模型对象。</span><span class="sxs-lookup"><span data-stu-id="5c13e-185">The data context delegates most of the work to Breeze, which constructs self-tracking model objects from JSON query results.</span></span>

<span data-ttu-id="5c13e-186">服务器端堆栈包含某些开发人员代码和三个原则 .NET 库： Web API、实体框架和 Breeze.NET：</span><span class="sxs-lookup"><span data-stu-id="5c13e-186">The server-side stack consists of some developer code and three principle .NET libraries: Web API, Entity Framework, and Breeze.NET:</span></span>

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

<span data-ttu-id="5c13e-187">基本体系结构与 KnockoutJS SPA 模板相同。</span><span class="sxs-lookup"><span data-stu-id="5c13e-187">The basic architecture is the same as the KnockoutJS SPA template.</span></span> <span data-ttu-id="5c13e-188">但是，实现要简单得多：删除了 Dto，并且大部分实体框架详细信息已委派给 Breeze.NET。</span><span class="sxs-lookup"><span data-stu-id="5c13e-188">However, the implementation is much simpler: The DTOs were deleted, and most of the Entity Framework details have been delegated to Breeze.NET.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c13e-189">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5c13e-189">Next Steps</span></span>

<span data-ttu-id="5c13e-190">我们建议您浏览代码，指导您在简单的网站上对客户端和服务器堆栈的[广泛讨论](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa)。</span><span class="sxs-lookup"><span data-stu-id="5c13e-190">We suggest that you explore the code, guided by the [extensive discussion](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) of both the client and the server stacks on the Breeze website.</span></span>

<span data-ttu-id="5c13e-191">你可以尝试通过简单的客户端查询进行播放;添加一些筛选器和排序。</span><span class="sxs-lookup"><span data-stu-id="5c13e-191">You might try playing with Breeze client-side query; add some filters and sorts.</span></span> <span data-ttu-id="5c13e-192">可以添加更多的模型属性和更多的实体，以更好地体验端到端 SPA 开发。</span><span class="sxs-lookup"><span data-stu-id="5c13e-192">You might add more model properties and more entities to get a better feel for end-to-end SPA development.</span></span> <span data-ttu-id="5c13e-193">当你确信设计时，可以排除 Todo 功能并将其替换为你自己的功能。</span><span class="sxs-lookup"><span data-stu-id="5c13e-193">When you are confident of the design, you can tear out the Todo features and replace them with your own.</span></span>

<span data-ttu-id="5c13e-194">祝你编码愉快！</span><span class="sxs-lookup"><span data-stu-id="5c13e-194">Happy coding!</span></span>
