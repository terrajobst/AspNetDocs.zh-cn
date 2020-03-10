---
uid: single-page-application/overview/templates/backbonejs-template
title: 骨干模板 |Microsoft Docs
author: madskristensen
description: 骨干的 SPA SPA 模板
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449774"
---
# <a name="backbone-template"></a><span data-ttu-id="0a144-103">Backbone 模板</span><span class="sxs-lookup"><span data-stu-id="0a144-103">Backbone Template</span></span>

<span data-ttu-id="0a144-104">作者： [Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="0a144-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="0a144-105">主干 SPA 模板由 Kazi Manzur Rashid 编写</span><span class="sxs-lookup"><span data-stu-id="0a144-105">The Backbone SPA Template was written by Kazi Manzur Rashid</span></span>
> 
> [<span data-ttu-id="0a144-106">下载骨干 SPA 模板</span><span class="sxs-lookup"><span data-stu-id="0a144-106">Download the Backbone.js SPA Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=293631)

<span data-ttu-id="0a144-107">骨干的 SPA 模板旨在让你快速开始使用骨干构建交互式客户端 web 应用[。](http://backbonejs.org/)</span><span class="sxs-lookup"><span data-stu-id="0a144-107">The Backbone.js SPA template is designed to get you started quickly building interactive client-side web apps using [Backbone.js.](http://backbonejs.org/)</span></span>

<span data-ttu-id="0a144-108">此模板提供了用于在 ASP.NET MVC 中开发主干 node.js 应用程序的初始主干。</span><span class="sxs-lookup"><span data-stu-id="0a144-108">The template provides an initial skeleton for developing a Backbone.js application in ASP.NET MVC.</span></span> <span data-ttu-id="0a144-109">它提供基本的用户登录功能，包括用户注册、登录、密码重置和具有基本电子邮件模板的用户确认。</span><span class="sxs-lookup"><span data-stu-id="0a144-109">Out of the box it provides basic user login functionality, including user sign-up, sign-in, password reset, and user confirmation with basic email templates.</span></span>

<span data-ttu-id="0a144-110">要求：</span><span class="sxs-lookup"><span data-stu-id="0a144-110">Requirements:</span></span>

- [<span data-ttu-id="0a144-111">ASP.NET 和 Web 工具2012.2 更新</span><span class="sxs-lookup"><span data-stu-id="0a144-111">ASP.NET and Web Tools 2012.2 update</span></span>](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a><span data-ttu-id="0a144-112">创建主干模板项目</span><span class="sxs-lookup"><span data-stu-id="0a144-112">Create a Backbone Template Project</span></span>

<span data-ttu-id="0a144-113">单击上面的 "下载" 按钮，下载并安装模板。</span><span class="sxs-lookup"><span data-stu-id="0a144-113">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="0a144-114">模板打包为 Visual Studio 扩展（VSIX）文件。</span><span class="sxs-lookup"><span data-stu-id="0a144-114">The template is packaged as a Visual Studio Extension (VSIX) file.</span></span> <span data-ttu-id="0a144-115">可能需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0a144-115">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="0a144-116">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="0a144-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="0a144-117">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="0a144-117">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="0a144-118">在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="0a144-118">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="0a144-119">命名项目并单击 **“确定”** 。</span><span class="sxs-lookup"><span data-stu-id="0a144-119">Name the project and click **OK**.</span></span>

![](backbonejs-template/_static/image1.png)

<span data-ttu-id="0a144-120">在 "**新建项目**" 向导中，选择 "骨干 SPA 项目"。</span><span class="sxs-lookup"><span data-stu-id="0a144-120">In the **New Project** wizard, select Backbone.js SPA Project.</span></span>

![](backbonejs-template/_static/image2.png)

<span data-ttu-id="0a144-121">按 Ctrl-F5 以生成并运行应用程序而不进行调试，或按 F5 运行调试。</span><span class="sxs-lookup"><span data-stu-id="0a144-121">Press Ctrl-F5 to build and run the application without debugging, or press F5 to run with debugging.</span></span>

![](backbonejs-template/_static/image3.png)

<span data-ttu-id="0a144-122">单击 "我的帐户" 会打开登录页：</span><span class="sxs-lookup"><span data-stu-id="0a144-122">Clicking "My Account" brings up the login page:</span></span>

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a><span data-ttu-id="0a144-123">演练：客户端代码</span><span class="sxs-lookup"><span data-stu-id="0a144-123">Walkthrough: Client Code</span></span>

<span data-ttu-id="0a144-124">让我们从客户端开始。</span><span class="sxs-lookup"><span data-stu-id="0a144-124">Let's starts with the client side.</span></span> <span data-ttu-id="0a144-125">客户端应用程序脚本位于 ~/Scripts/application 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0a144-125">The client application scripts are located in the ~/Scripts/application folder.</span></span> <span data-ttu-id="0a144-126">应用程序是用[TypeScript](http://www.typescriptlang.org/) （ts 文件）编写的，这些文件编译为 JavaScript （.js 文件）。</span><span class="sxs-lookup"><span data-stu-id="0a144-126">The application is written in [TypeScript](http://www.typescriptlang.org/) (.ts files) which are compiled into JavaScript (.js files).</span></span>

<span data-ttu-id="0a144-127">**应用程序**</span><span class="sxs-lookup"><span data-stu-id="0a144-127">**Application**</span></span>

<span data-ttu-id="0a144-128">`Application` 是在 application. ts 中定义的。</span><span class="sxs-lookup"><span data-stu-id="0a144-128">`Application` is defined in application.ts.</span></span> <span data-ttu-id="0a144-129">此对象初始化应用程序并充当根命名空间。</span><span class="sxs-lookup"><span data-stu-id="0a144-129">This object initializes the application and acts as the root namespace.</span></span> <span data-ttu-id="0a144-130">它保留在应用程序之间共享的配置和状态信息，例如用户是否已登录。</span><span class="sxs-lookup"><span data-stu-id="0a144-130">It maintains configuration and state information that is shared across the application, such as whether the user is signed in.</span></span>

<span data-ttu-id="0a144-131">`application.start` 方法创建模式视图，并为应用程序级事件附加事件处理程序，如用户登录。</span><span class="sxs-lookup"><span data-stu-id="0a144-131">The `application.start` method creates the modal views and attaches event handlers for application-level events, such as user sign-in.</span></span> <span data-ttu-id="0a144-132">接下来，它会创建默认路由器，并检查是否指定了任何客户端 URL。</span><span class="sxs-lookup"><span data-stu-id="0a144-132">Next, it creates the default router and checks whether any client-side URL is specified.</span></span> <span data-ttu-id="0a144-133">如果不是，则它将重定向到默认 url （#！/）。</span><span class="sxs-lookup"><span data-stu-id="0a144-133">If not, it redirects to the default url (#!/).</span></span>

<span data-ttu-id="0a144-134">**事件**</span><span class="sxs-lookup"><span data-stu-id="0a144-134">**Events**</span></span>

<span data-ttu-id="0a144-135">开发松散耦合组件时，事件始终很重要。</span><span class="sxs-lookup"><span data-stu-id="0a144-135">Events are always important when developing loosely coupled components.</span></span> <span data-ttu-id="0a144-136">应用程序通常会执行多个操作来响应用户操作。</span><span class="sxs-lookup"><span data-stu-id="0a144-136">Applications often perform multiple operations in response to a user action.</span></span> <span data-ttu-id="0a144-137">骨干提供内置事件，其中包含模型、集合和视图等组件。</span><span class="sxs-lookup"><span data-stu-id="0a144-137">Backbone provides built-in events with components such as Model, Collection, and View.</span></span> <span data-ttu-id="0a144-138">该模板使用 "发布/订阅" 模型，而不是创建这些组件之间的依赖关系，而是使用 "发布/订阅" 模型：在事件中定义的 `events` 对象充当用于发布和订阅应用程序事件的事件中心。</span><span class="sxs-lookup"><span data-stu-id="0a144-138">Instead of creating inter-dependencies among these components, the template uses a "pub/sub" model: The `events` object, defined in events.ts, acts as an event hub for publishing and subscribing to application events.</span></span> <span data-ttu-id="0a144-139">`events` 对象是单一实例。</span><span class="sxs-lookup"><span data-stu-id="0a144-139">The `events` object is a singleton.</span></span> <span data-ttu-id="0a144-140">下面的代码演示如何订阅事件，并触发事件：</span><span class="sxs-lookup"><span data-stu-id="0a144-140">The following code shows how to subscribe to an event and then trigger the event:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

<span data-ttu-id="0a144-141">**路由器**</span><span class="sxs-lookup"><span data-stu-id="0a144-141">**Router**</span></span>

<span data-ttu-id="0a144-142">在主干 node.js 中，路由器提供了用于路由客户端页以及将它们连接到操作和事件的方法。</span><span class="sxs-lookup"><span data-stu-id="0a144-142">In Backbone.js, a router provides methods for routing client-side pages and connecting them to actions and events.</span></span> <span data-ttu-id="0a144-143">此模板定义了路由器中的单个路由器。</span><span class="sxs-lookup"><span data-stu-id="0a144-143">The template defines a single router, in router.ts.</span></span> <span data-ttu-id="0a144-144">路由器创建 activable 视图，并在切换视图时维持状态。</span><span class="sxs-lookup"><span data-stu-id="0a144-144">The router creates the activable views and maintains the state when switching views.</span></span> <span data-ttu-id="0a144-145">（下一节介绍了 Activable 视图。）最初，该项目有两个虚拟视图： "主页" 和 "关于"。</span><span class="sxs-lookup"><span data-stu-id="0a144-145">(Activable views are described in the next section.) Initially, the project has two dummy views, Home and About.</span></span> <span data-ttu-id="0a144-146">它还具有一个 NotFound 视图，如果该路由是未知的，则会显示此视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-146">It also has a NotFound view, which is displayed if the route is not known.</span></span>

<span data-ttu-id="0a144-147">**Views**</span><span class="sxs-lookup"><span data-stu-id="0a144-147">**Views**</span></span>

<span data-ttu-id="0a144-148">视图在 ~/Scripts/application/views. 中定义。</span><span class="sxs-lookup"><span data-stu-id="0a144-148">The views are defined in ~/Scripts/application/views.</span></span> <span data-ttu-id="0a144-149">有两种类型的视图： activable 视图和模式对话框视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-149">There are two kinds of views, activable views and modal dialog views.</span></span> <span data-ttu-id="0a144-150">Activable 视图由路由器调用。</span><span class="sxs-lookup"><span data-stu-id="0a144-150">Activable views are invoked by the router.</span></span> <span data-ttu-id="0a144-151">显示 activable 视图时，所有其他 activable 视图都将变为非活动状态。</span><span class="sxs-lookup"><span data-stu-id="0a144-151">When an activable view is shown, all other activable views become inactive.</span></span> <span data-ttu-id="0a144-152">若要创建 activable 视图，请使用 `Activable` 对象扩展视图：</span><span class="sxs-lookup"><span data-stu-id="0a144-152">To create an activable view, extend the view with the `Activable` object:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

<span data-ttu-id="0a144-153">通过扩展 `Activable` 向视图添加两个新方法 `activate` 和 `deactivate`。</span><span class="sxs-lookup"><span data-stu-id="0a144-153">Extending with `Activable` adds two new methods to the view, `activate` and `deactivate`.</span></span> <span data-ttu-id="0a144-154">路由器调用这些方法来激活和停用视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-154">The router calls these methods to activate and deactive the view.</span></span>

<span data-ttu-id="0a144-155">模式视图以[Twitter 启动](https://twitter.github.com/bootstrap/)模式对话框的形式实现。</span><span class="sxs-lookup"><span data-stu-id="0a144-155">Modal views are implemented as [Twitter Bootstrap](https://twitter.github.com/bootstrap/) modal dialogs.</span></span> <span data-ttu-id="0a144-156">`Membership` 视图和 `Profile` 视图都是模式视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-156">The `Membership` and `Profile` views are modal views.</span></span> <span data-ttu-id="0a144-157">所有应用程序事件都可以调用模型视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-157">Model views can be invoked by any application events.</span></span> <span data-ttu-id="0a144-158">例如，在 "`Navigation`" 视图中，单击 "我的帐户" 链接将显示 "`Membership`" 视图或 "`Profile`" 视图，具体取决于用户是否已登录。</span><span class="sxs-lookup"><span data-stu-id="0a144-158">For example, in the `Navigation` view, clicking the "My Account" link shows either the `Membership` view or the `Profile` view, depending on whether the user is logged in.</span></span> <span data-ttu-id="0a144-159">`Navigation` 将 click 事件处理程序附加到具有 `data-command` 属性的任何子元素。</span><span class="sxs-lookup"><span data-stu-id="0a144-159">The `Navigation` attaches click event handlers to any child elements that have the `data-command` attribute.</span></span> <span data-ttu-id="0a144-160">HTML 标记如下所示：</span><span class="sxs-lookup"><span data-stu-id="0a144-160">Here is the HTML markup:</span></span>

[!code-html[Main](backbonejs-template/samples/sample3.html)]

<span data-ttu-id="0a144-161">下面是用于挂钩事件的导航中的代码：</span><span class="sxs-lookup"><span data-stu-id="0a144-161">Here is the code in navigation.ts to hook up the events:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

<span data-ttu-id="0a144-162">Models</span><span class="sxs-lookup"><span data-stu-id="0a144-162">**Models**</span></span>

<span data-ttu-id="0a144-163">模型在 ~/Scripts/application/models. 中定义。</span><span class="sxs-lookup"><span data-stu-id="0a144-163">The models are defined in ~/Scripts/application/models.</span></span> <span data-ttu-id="0a144-164">这些模型都有三个基本功能：默认属性、验证规则和服务器端终结点。</span><span class="sxs-lookup"><span data-stu-id="0a144-164">The models all have three basic things: default attributes, validation rules, and a server-side end point.</span></span> <span data-ttu-id="0a144-165">下面是一个典型示例：</span><span class="sxs-lookup"><span data-stu-id="0a144-165">Here is a typical example:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

<span data-ttu-id="0a144-166">**插件**</span><span class="sxs-lookup"><span data-stu-id="0a144-166">**Plug-ins**</span></span>

<span data-ttu-id="0a144-167">~/Scripts/application/lib 文件夹包含几个方便的 jQuery 插件。此形式的 ts 文件定义用于处理窗体数据的插件。</span><span class="sxs-lookup"><span data-stu-id="0a144-167">The ~/Scripts/application/lib folder contains a few handy jQuery plug-ins. The form.ts file defines a plug-in for working with form data.</span></span> <span data-ttu-id="0a144-168">通常，您需要序列化或反序列化窗体数据，并显示任何模型验证错误。</span><span class="sxs-lookup"><span data-stu-id="0a144-168">Often you need to serialize or deserialize form data and show any model validation errors.</span></span> <span data-ttu-id="0a144-169">Ts 插件的方法 `serializeFields`、`deserializeFields`和 `showFieldErrors`。</span><span class="sxs-lookup"><span data-stu-id="0a144-169">The form.ts plug-in has methods such as `serializeFields`, `deserializeFields`, and `showFieldErrors`.</span></span> <span data-ttu-id="0a144-170">下面的示例演示如何将窗体序列化到模型。</span><span class="sxs-lookup"><span data-stu-id="0a144-170">The following example shows how to serialize a form to a model.</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

<span data-ttu-id="0a144-171">Flashbar 插件向用户提供各种类型的反馈消息。</span><span class="sxs-lookup"><span data-stu-id="0a144-171">The flashbar.ts plug-in gives various kinds of feedback messages to the user.</span></span> <span data-ttu-id="0a144-172">方法 `$.showSuccessbar`、`$.showErrorbar` 和 `$.showInfobar`。</span><span class="sxs-lookup"><span data-stu-id="0a144-172">The methods are `$.showSuccessbar`, `$.showErrorbar` and `$.showInfobar`.</span></span> <span data-ttu-id="0a144-173">在后台，它使用 Twitter 启动警报显示有效果很好的消息。</span><span class="sxs-lookup"><span data-stu-id="0a144-173">Behind the scenes, it uses Twitter Bootstrap alerts to show nicely animated messages.</span></span>

<span data-ttu-id="0a144-174">尽管 API 略有不同，但 confirm 插件会替换浏览器的 "确认" 对话框：</span><span class="sxs-lookup"><span data-stu-id="0a144-174">The confirm.ts plug-in replaces the browser's confirm dialog, although the API is somewhat different:</span></span>

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a><span data-ttu-id="0a144-175">演练：服务器代码</span><span class="sxs-lookup"><span data-stu-id="0a144-175">Walkthrough: Server Code</span></span>

<span data-ttu-id="0a144-176">现在让我们看看服务器端。</span><span class="sxs-lookup"><span data-stu-id="0a144-176">Now let's look at the server side.</span></span>

<span data-ttu-id="0a144-177">**Controllers**</span><span class="sxs-lookup"><span data-stu-id="0a144-177">**Controllers**</span></span>

<span data-ttu-id="0a144-178">在单页面应用程序中，服务器仅在用户界面中扮演小型角色。</span><span class="sxs-lookup"><span data-stu-id="0a144-178">In a single page application, the server plays only a small role in the user interface.</span></span> <span data-ttu-id="0a144-179">通常，服务器会呈现初始页面，然后发送和接收 JSON 数据。</span><span class="sxs-lookup"><span data-stu-id="0a144-179">Typically, the server renders the initial page and then sends and receives JSON data.</span></span>

<span data-ttu-id="0a144-180">模板具有两个 MVC 控制器： `HomeController` 呈现初始页面，`SupportsController` 用于确认新用户帐户和重置密码。</span><span class="sxs-lookup"><span data-stu-id="0a144-180">The template has two MVC controllers: `HomeController` renders the initial page, and `SupportsController` is used to confirm new user accounts and reset passwords.</span></span> <span data-ttu-id="0a144-181">模板中的所有其他控制器均为发送和接收 JSON 数据 ASP.NET Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="0a144-181">All other controllers in the template are ASP.NET Web API controllers, which send and receive JSON data.</span></span> <span data-ttu-id="0a144-182">默认情况下，控制器使用新的 `WebSecurity` 类来执行用户相关的任务。</span><span class="sxs-lookup"><span data-stu-id="0a144-182">By default, the controllers use the new `WebSecurity` class to perform user-related tasks.</span></span> <span data-ttu-id="0a144-183">但是，它们还具有可选的构造函数，可让你为这些任务传入委托。</span><span class="sxs-lookup"><span data-stu-id="0a144-183">However, they also have optional constructors that let you pass in delegates for these tasks.</span></span> <span data-ttu-id="0a144-184">这使测试变得更加容易，并使你可以使用 IoC 容器将 `WebSecurity` 替换为其他内容。</span><span class="sxs-lookup"><span data-stu-id="0a144-184">This makes testing easier, and lets you replace `WebSecurity` with something else, by using an IoC Container.</span></span> <span data-ttu-id="0a144-185">下面是一个示例：</span><span class="sxs-lookup"><span data-stu-id="0a144-185">Here is an example:</span></span>

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a><span data-ttu-id="0a144-186">视图</span><span class="sxs-lookup"><span data-stu-id="0a144-186">Views</span></span>

<span data-ttu-id="0a144-187">视图设计为模块化：页面的每个部分都有其自己的专用视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-187">The views are designed to be modular: Each section of a page has its own dedicated view.</span></span> <span data-ttu-id="0a144-188">在单页面应用程序中，常见的情况是包含没有任何对应控制器的视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-188">In a single page application, it is common to include views that do not have any corresponding controller.</span></span> <span data-ttu-id="0a144-189">您可以通过调用 `@Html.Partial('myView')`来包含视图，但这会变得枯燥乏味。</span><span class="sxs-lookup"><span data-stu-id="0a144-189">You can include a view by calling `@Html.Partial('myView')`, but this gets tedious.</span></span> <span data-ttu-id="0a144-190">为了使此操作变得更简单，模板定义了一个帮助器方法 `IncludeClientViews`，该方法呈现指定文件夹中的所有视图：</span><span class="sxs-lookup"><span data-stu-id="0a144-190">To make this easier, the template defines a helper method, `IncludeClientViews`, that renders all of the views in a specified folder:</span></span>

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

<span data-ttu-id="0a144-191">如果未指定文件夹名称，则默认文件夹名称为 "ClientViews"。</span><span class="sxs-lookup"><span data-stu-id="0a144-191">If the folder name is not specified, the default folder name is "ClientViews".</span></span> <span data-ttu-id="0a144-192">如果客户端视图还使用分部视图，请使用下划线字符命名分部视图（例如 `_SignUp`）。</span><span class="sxs-lookup"><span data-stu-id="0a144-192">If your client view also uses partial views, name the partial view with an underscore character (for example, `_SignUp`).</span></span> <span data-ttu-id="0a144-193">`IncludeClientViews` 方法排除名称以下划线开头的任何视图。</span><span class="sxs-lookup"><span data-stu-id="0a144-193">The `IncludeClientViews` method excludes any views whose name starts with an underscore.</span></span> <span data-ttu-id="0a144-194">若要在客户端视图中包含分部视图，请调用 `Html.ClientView('SignUp')` 而不是 `Html.Partial('_SignUp')`。</span><span class="sxs-lookup"><span data-stu-id="0a144-194">To include a partial view in the client view, call `Html.ClientView('SignUp')` instead of `Html.Partial('_SignUp')`.</span></span>

<span data-ttu-id="0a144-195">**发送电子邮件**</span><span class="sxs-lookup"><span data-stu-id="0a144-195">**Sending Email**</span></span>

<span data-ttu-id="0a144-196">若要发送电子邮件，模板需要使用[邮政](http://aboutcode.net/postal)。</span><span class="sxs-lookup"><span data-stu-id="0a144-196">To send email, the template uses [Postal](http://aboutcode.net/postal).</span></span> <span data-ttu-id="0a144-197">不过，从代码的其余部分中提取邮政的 `IMailer` 接口，因此你可以轻松地将其替换为另一实现。</span><span class="sxs-lookup"><span data-stu-id="0a144-197">However, Postal is abstracted from the rest of the code with the `IMailer` interface, so you can easily replace it with another implementation.</span></span> <span data-ttu-id="0a144-198">电子邮件模板位于 "视图"/"电子邮件" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="0a144-198">The email templates are located in the Views/Emails folder.</span></span> <span data-ttu-id="0a144-199">发件人的电子邮件地址是在 web.config 文件中的**appSettings**节的 `sender.email` 项中指定的。</span><span class="sxs-lookup"><span data-stu-id="0a144-199">The sender's email address is specified in the web.config file, in the `sender.email` key of the **appSettings** section.</span></span> <span data-ttu-id="0a144-200">此外，当在 web.config 中 `debug="true"` 时，应用程序不需要用户电子邮件确认即可加快开发速度。</span><span class="sxs-lookup"><span data-stu-id="0a144-200">Also, when `debug="true"` in web.config, the application does not require user email confirmation, to speed up development.</span></span>

## <a name="github"></a><span data-ttu-id="0a144-201">GitHub</span><span class="sxs-lookup"><span data-stu-id="0a144-201">GitHub</span></span>

<span data-ttu-id="0a144-202">还可在[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)上找到主干 SPA 模板。</span><span class="sxs-lookup"><span data-stu-id="0a144-202">You can also find the Backbone.js SPA template on [GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).</span></span>
