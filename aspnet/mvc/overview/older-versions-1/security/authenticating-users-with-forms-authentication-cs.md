---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: 通过 Forms 身份验证对用户C#进行身份验证（） |Microsoft Docs
author: microsoft
description: 了解如何使用 [授权] 特性来保护 MVC 应用程序中的特定页面。 了解如何使用网站管理 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435446"
---
# <a name="authenticating-users-with-forms-authentication-c"></a><span data-ttu-id="a96d9-104">使用 Forms 身份验证对用户进行身份验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="a96d9-104">Authenticating Users with Forms Authentication (C#)</span></span>

<span data-ttu-id="a96d9-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="a96d9-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="a96d9-106">了解如何使用 [授权] 特性来保护 MVC 应用程序中的特定页面。</span><span class="sxs-lookup"><span data-stu-id="a96d9-106">Learn how to use the [Authorize] attribute to password protect particular pages in your MVC application.</span></span> <span data-ttu-id="a96d9-107">了解如何使用网站管理工具来创建和管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-107">You learn how to use the Web Site Administration Tool to create and manage users and roles.</span></span> <span data-ttu-id="a96d9-108">你还将了解如何配置存储用户帐户和角色信息的位置。</span><span class="sxs-lookup"><span data-stu-id="a96d9-108">You also learn how to configure where user account and role information is stored.</span></span>

<span data-ttu-id="a96d9-109">本教程的目的是说明如何使用窗体身份验证来保护 ASP.NET MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="a96d9-109">The goal of this tutorial is to explain how you can use Forms authentication to password protect the views in your ASP.NET MVC applications.</span></span> <span data-ttu-id="a96d9-110">了解如何使用网站管理工具来创建用户和角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-110">You learn how to use the Web Site Administration Tool to create users and roles.</span></span> <span data-ttu-id="a96d9-111">你还将了解如何防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-111">You also learn how to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="a96d9-112">最后，你将了解如何配置存储用户名和密码的位置。</span><span class="sxs-lookup"><span data-stu-id="a96d9-112">Finally, you learn how to configure where user names and passwords are stored.</span></span>

#### <a name="using-the-web-site-administration-tool"></a><span data-ttu-id="a96d9-113">使用网站管理工具</span><span class="sxs-lookup"><span data-stu-id="a96d9-113">Using the Web Site Administration Tool</span></span>

<span data-ttu-id="a96d9-114">在执行其他操作之前，应首先创建一些用户和角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-114">Before we do anything else, we should start by creating some users and roles.</span></span> <span data-ttu-id="a96d9-115">创建新用户和角色的最简单方法是利用 Visual Studio 2008 网站管理工具。</span><span class="sxs-lookup"><span data-stu-id="a96d9-115">The easiest way to create new users and roles is to take advantage of the Visual Studio 2008 Web Site Administration Tool.</span></span> <span data-ttu-id="a96d9-116">你可以通过选择 "**项目"、"ASP.NET 配置**" 菜单选项来启动此工具。</span><span class="sxs-lookup"><span data-stu-id="a96d9-116">You can launch this tool by selecting the menu option **Project, ASP.NET Configuration**.</span></span> <span data-ttu-id="a96d9-117">或者，您可以通过单击 "解决方案资源管理器" 窗口顶部的 "hammer" 旁边的 "（有点可怕的）" 图标来启动网站管理工具（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-117">Alternatively, you can launch the Web Site Administration Tool by clicking the (somewhat scary) icon of the hammer hitting the world that appears at the top of the Solution Explorer window (see Figure 1).</span></span>

<span data-ttu-id="a96d9-118">**图 1-启动网站管理工具**</span><span class="sxs-lookup"><span data-stu-id="a96d9-118">**Figure 1 – Launching the Web Site Administration Tool**</span></span>

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

<span data-ttu-id="a96d9-120">在网站管理工具中，通过选择 "安全" 选项卡来创建新的用户和角色。单击 "**创建用户**" 链接，创建名为 Stephen 的新用户（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-120">Within the Web Site Administration Tool, you create new users and roles by selecting the Security tab. Click the **Create user** link to create a new user named Stephen (see Figure 2).</span></span> <span data-ttu-id="a96d9-121">为 Stephen 用户提供所需的任何密码（例如， *secret*）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-121">Provide the Stephen user with any password that you want (for example, *secret*).</span></span>

<span data-ttu-id="a96d9-122">**图2–创建新用户**</span><span class="sxs-lookup"><span data-stu-id="a96d9-122">**Figure 2 – Creating a new user**</span></span>

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

<span data-ttu-id="a96d9-124">首先要启用角色并定义一个或多个角色，从而创建新的角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-124">You create new roles by first enabling roles and defining one or more roles.</span></span> <span data-ttu-id="a96d9-125">通过单击 "**启用角色**" 链接启用角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-125">Enable roles by clicking the **Enable roles** link.</span></span> <span data-ttu-id="a96d9-126">接下来，通过单击 "**创建或管理角色**" 链接，创建名为 "*管理员*" 的角色（请参阅图3）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-126">Next, create a role named *Administrators* by clicking the **Create or Manage roles** link (see Figure 3).</span></span>

<span data-ttu-id="a96d9-127">**图 3-创建新角色**</span><span class="sxs-lookup"><span data-stu-id="a96d9-127">**Figure 3 – Creating a new role**</span></span>

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

<span data-ttu-id="a96d9-129">最后，创建一个名为 Sally 的新用户，并在创建 Sally 时单击 "创建用户" 链接并选择 "管理员"，将 Sally 关联到管理员角色（请参阅图4）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-129">Finally, create a new user named Sally and associate Sally with the Administrators role by clicking the Create User link and selecting Administrators when creating Sally (see Figure 4).</span></span>

<span data-ttu-id="a96d9-130">**图 4-将用户添加到角色**</span><span class="sxs-lookup"><span data-stu-id="a96d9-130">**Figure 4 – Adding a user to a role**</span></span>

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

<span data-ttu-id="a96d9-132">完成所有工作后，应该有两个名为 "Stephen" 和 "Sally" 的新用户。</span><span class="sxs-lookup"><span data-stu-id="a96d9-132">When all is said and done, you should have two new users named Stephen and Sally.</span></span> <span data-ttu-id="a96d9-133">还应具有名为管理员的新角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-133">You should also have a new role named Administrators.</span></span> <span data-ttu-id="a96d9-134">Sally 是 "管理员" 角色的成员，而 "Stephen" 不是。</span><span class="sxs-lookup"><span data-stu-id="a96d9-134">Sally is a member of the Administrators role and Stephen is not.</span></span>

#### <a name="requiring-authorization"></a><span data-ttu-id="a96d9-135">需要授权</span><span class="sxs-lookup"><span data-stu-id="a96d9-135">Requiring Authorization</span></span>

<span data-ttu-id="a96d9-136">您可以通过将 [授权] 特性添加到操作，要求用户先进行身份验证，然后才能调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-136">You can require a user to be authenticated before the user invokes a controller action by adding the [Authorize] attribute to the action.</span></span> <span data-ttu-id="a96d9-137">可以将 [授权] 属性应用于单个控制器操作，也可以将此属性应用于整个控制器类。</span><span class="sxs-lookup"><span data-stu-id="a96d9-137">You can apply the [Authorize] attribute to an individual controller action or you can apply this attribute to an entire controller class.</span></span>

<span data-ttu-id="a96d9-138">例如，列表1中的控制器公开一个名为 CompanySecrets （）的操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-138">For example, the controller in Listing 1 exposes an action named CompanySecrets().</span></span> <span data-ttu-id="a96d9-139">由于此操作是使用 [授权] 特性修饰的，因此除非用户经过身份验证，否则无法调用此操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-139">Because this action is decorated with the [Authorize] attribute, this action cannot be invoked unless a user is authenticated.</span></span>

<span data-ttu-id="a96d9-140">**列表1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="a96d9-140">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

<span data-ttu-id="a96d9-141">如果通过在浏览器的地址栏中输入 URL/Home/CompanySecrets 来调用 CompanySecrets （）操作，并且不是经过身份验证的用户，则会自动重定向到登录视图（参见图5）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-141">If you invoke the CompanySecrets() action by entering the URL /Home/CompanySecrets in the address bar of your browser, and you are not an authenticated user, then you will be redirected to the Login view automatically (see Figure 5).</span></span>

<span data-ttu-id="a96d9-142">**图5–登录视图**</span><span class="sxs-lookup"><span data-stu-id="a96d9-142">**Figure 5 – The Login view**</span></span>

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

<span data-ttu-id="a96d9-144">您可以使用登录视图输入您的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="a96d9-144">You can use the Login view to enter your user name and password.</span></span> <span data-ttu-id="a96d9-145">如果你不是已注册的用户，你可以单击 "**注册**" 链接以导航到 "注册" 视图（参见图6）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-145">If you are not a registered user then you can click the **register** link to navigate to the Register view (see Figure 6).</span></span> <span data-ttu-id="a96d9-146">您可以使用注册视图创建新的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="a96d9-146">You can use the Register view to create a new user account.</span></span>

<span data-ttu-id="a96d9-147">**图 6-注册视图**</span><span class="sxs-lookup"><span data-stu-id="a96d9-147">**Figure 6 – The Register view**</span></span>

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

<span data-ttu-id="a96d9-149">成功登录后，可以看到 "CompanySecrets" 视图（参见图7）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-149">After you successfully log in, you can see the CompanySecrets view (see Figure 7).</span></span> <span data-ttu-id="a96d9-150">默认情况下，你将继续登录到你关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="a96d9-150">By default, you will continue to be logged in until you close your browser window.</span></span>

<span data-ttu-id="a96d9-151">**图7– CompanySecrets 视图**</span><span class="sxs-lookup"><span data-stu-id="a96d9-151">**Figure 7 – The CompanySecrets view**</span></span>

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a><span data-ttu-id="a96d9-153">按用户名或用户角色授权</span><span class="sxs-lookup"><span data-stu-id="a96d9-153">Authorizing by User Name or User Role</span></span>

<span data-ttu-id="a96d9-154">您可以使用 [授权] 属性将对控制器操作的访问限制为特定的一组用户或一组特定的用户角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-154">You can use the [Authorize] attribute to restrict access to a controller action to a particular set of users or a particular set of user roles.</span></span> <span data-ttu-id="a96d9-155">例如，清单2中修改后的主控制器包含两个名为 StephenSecrets （）和 AdministratorSecrets （）的新操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-155">For example, the modified Home controller in Listing 2 contains two new actions named StephenSecrets() and AdministratorSecrets().</span></span>

<span data-ttu-id="a96d9-156">**列表 2-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="a96d9-156">**Listing 2 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

<span data-ttu-id="a96d9-157">只有具有 user name Stephen 的用户可以调用 StephenSecrets （）操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-157">Only a user with the user name Stephen can invoke the StephenSecrets() action.</span></span> <span data-ttu-id="a96d9-158">所有其他用户都将重定向到登录视图。</span><span class="sxs-lookup"><span data-stu-id="a96d9-158">All other users get redirected to the Login view.</span></span> <span data-ttu-id="a96d9-159">Users 属性接受以逗号分隔的用户帐户名称列表。</span><span class="sxs-lookup"><span data-stu-id="a96d9-159">The Users property accepts a comma separated list of user account names.</span></span>

<span data-ttu-id="a96d9-160">只有管理员角色中的用户可以调用 AdministratorSecrets （）操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-160">Only users in the Administrators role can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="a96d9-161">例如，由于 Sally 是 Administrators 组的成员，因此她可以调用 AdministratorSecrets （）操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-161">For example, because Sally is a member of the Administrators group, she can invoke the AdministratorSecrets() action.</span></span> <span data-ttu-id="a96d9-162">所有其他用户都将重定向到登录视图。</span><span class="sxs-lookup"><span data-stu-id="a96d9-162">All other users get redirected to the Login view.</span></span> <span data-ttu-id="a96d9-163">Role 属性接受以逗号分隔的角色名称列表。</span><span class="sxs-lookup"><span data-stu-id="a96d9-163">The Roles property accepts a comma separated list of role names.</span></span>

#### <a name="configuring-authentication"></a><span data-ttu-id="a96d9-164">配置身份验证</span><span class="sxs-lookup"><span data-stu-id="a96d9-164">Configuring Authentication</span></span>

<span data-ttu-id="a96d9-165">此时，您可能想知道用户帐户和角色信息的存储位置。</span><span class="sxs-lookup"><span data-stu-id="a96d9-165">At this point, you might be wondering where the user account and role information is being stored.</span></span> <span data-ttu-id="a96d9-166">默认情况下，此信息存储在一个名为 ASPNETDB.MDF 的 SQL Express 数据库中，该数据库位于 MVC 应用程序的应用\_Data 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a96d9-166">By default, the information is stored in a (RANU) SQL Express database named ASPNETDB.mdf located in your MVC application's App\_Data folder.</span></span> <span data-ttu-id="a96d9-167">此数据库由 ASP.NET 框架在你开始使用成员身份时自动生成。</span><span class="sxs-lookup"><span data-stu-id="a96d9-167">This database is generated by the ASP.NET framework automatically when you start using membership.</span></span>

<span data-ttu-id="a96d9-168">若要在 "解决方案资源管理器" 窗口中查看 ASPNETDB.MDF 数据库，首先需要选择 "菜单" "项目" "项目" "显示所有文件"。</span><span class="sxs-lookup"><span data-stu-id="a96d9-168">In order to see the ASPNETDB.mdf database in the Solution Explorer window, you first need to select the menu option Project, Show All Files.</span></span>

<span data-ttu-id="a96d9-169">开发应用程序时，使用默认的 SQL Express 数据库是正确的。</span><span class="sxs-lookup"><span data-stu-id="a96d9-169">Using the default SQL Express database is fine when developing an application.</span></span> <span data-ttu-id="a96d9-170">不过，您很可能不希望对生产应用程序使用默认的 ASPNETDB.MDF 数据库。</span><span class="sxs-lookup"><span data-stu-id="a96d9-170">Most likely, however, you won't want to use the default ASPNETDB.mdf database for a production application.</span></span> <span data-ttu-id="a96d9-171">在这种情况下，你可以通过完成以下两个步骤来更改存储用户帐户信息的位置：</span><span class="sxs-lookup"><span data-stu-id="a96d9-171">In that case, you can change where user account information is stored by completing the following two steps:</span></span>

1. <span data-ttu-id="a96d9-172">将应用程序服务数据库对象添加到生产数据库-更改应用程序的连接字符串以指向生产数据库</span><span class="sxs-lookup"><span data-stu-id="a96d9-172">Add the Application Services database objects to your production database - Change your application connection string to point to your production database</span></span>

<span data-ttu-id="a96d9-173">第一步是将所有必要的数据库对象（表和存储过程）添加到生产数据库中。</span><span class="sxs-lookup"><span data-stu-id="a96d9-173">The first step is to add all of the necessary database objects (tables and stored procedures) to your production database.</span></span> <span data-ttu-id="a96d9-174">将这些对象添加到新数据库的最简单方法是使用 ASP.NET SQL Server 安装向导（见图8）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-174">The easiest way to add these objects to a new database is to take advantage of the ASP.NET SQL Server Setup Wizard (see Figure 8).</span></span> <span data-ttu-id="a96d9-175">若要启动此工具，可以从 Microsoft Visual Studio 2008 程序组打开 Visual Studio 2008 命令提示符，然后从命令提示符处执行以下命令：</span><span class="sxs-lookup"><span data-stu-id="a96d9-175">You can launch this tool by opening the Visual Studio 2008 Command Prompt from the Microsoft Visual Studio 2008 program group and executing the following command from the command prompt:</span></span>

<span data-ttu-id="a96d9-176">aspnet\_regsql</span><span class="sxs-lookup"><span data-stu-id="a96d9-176">aspnet\_regsql</span></span>

<span data-ttu-id="a96d9-177">**图8– ASP.NET SQL Server 安装向导**</span><span class="sxs-lookup"><span data-stu-id="a96d9-177">**Figure 8 – The ASP.NET SQL Server Setup Wizard**</span></span>

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

<span data-ttu-id="a96d9-179">使用 ASP.NET SQL Server 安装向导，可以选择网络上的 SQL Server 数据库，并安装 ASP.NET 应用程序服务所需的所有数据库对象。</span><span class="sxs-lookup"><span data-stu-id="a96d9-179">The ASP.NET SQL Server Setup Wizard enables you to select a SQL Server database on your network and install all of the database objects required by the ASP.NET application services.</span></span> <span data-ttu-id="a96d9-180">不需要在本地计算机上安装数据库服务器。</span><span class="sxs-lookup"><span data-stu-id="a96d9-180">The database server is not required to be located on your local machine.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a96d9-181">如果不想使用 ASP.NET SQL Server 安装向导，则可以在以下文件夹中找到用于添加应用程序服务数据库对象的 SQL 脚本：</span><span class="sxs-lookup"><span data-stu-id="a96d9-181">If you don't want to use the ASP.NET SQL Server Setup Wizard, then you can find SQL scripts for adding the application services database objects in the following folder:</span></span>
> 
> > <span data-ttu-id="a96d9-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span><span class="sxs-lookup"><span data-stu-id="a96d9-182">C:\Windows\Microsoft.NET\Framework\v2.0.50727</span></span>

<span data-ttu-id="a96d9-183">创建所需的数据库对象后，需要修改 MVC 应用程序使用的数据库连接。</span><span class="sxs-lookup"><span data-stu-id="a96d9-183">After you create the necessary database objects, you need to modify the database connection used by your MVC application.</span></span> <span data-ttu-id="a96d9-184">修改 web 配置（web.config）文件中的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 连接字符串，使其指向生产数据库。</span><span class="sxs-lookup"><span data-stu-id="a96d9-184">Modify the ApplicationServices connection string in your web configuration (web.config) file so that it points to the production database.</span></span> <span data-ttu-id="a96d9-185">例如，列表3中的已修改连接指向名为 MyProductionDB 的数据库（原始 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 连接字符串已被注释掉）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-185">For example, the modified connection in Listing 3 points to a database named MyProductionDB (the original ApplicationServices connection string has been commented out).</span></span>

<span data-ttu-id="a96d9-186">**列表 3-web.config**</span><span class="sxs-lookup"><span data-stu-id="a96d9-186">**Listing 3 – Web.config**</span></span>

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a><span data-ttu-id="a96d9-187">配置数据库权限</span><span class="sxs-lookup"><span data-stu-id="a96d9-187">Configuring Database Permissions</span></span>

<span data-ttu-id="a96d9-188">如果使用集成安全性来连接到数据库，则需要将正确的 Windows 用户帐户作为登录名添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="a96d9-188">If you use Integrated Security to connect to your database then you will need to add the correct Windows user account as a login to your database.</span></span> <span data-ttu-id="a96d9-189">正确的帐户取决于你使用的是 ASP.NET 开发服务器还是 Internet Information Services 作为你的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="a96d9-189">The correct account depends on whether you are using the ASP.NET Development Server or Internet Information Services as your web server.</span></span> <span data-ttu-id="a96d9-190">正确的用户帐户也依赖于您的操作系统。</span><span class="sxs-lookup"><span data-stu-id="a96d9-190">The correct user account also depends on your operating system.</span></span>

<span data-ttu-id="a96d9-191">如果使用的是 ASP.NET 开发服务器（Visual Studio 使用的默认 web 服务器），则应用程序将在 Windows 用户帐户的上下文中执行。</span><span class="sxs-lookup"><span data-stu-id="a96d9-191">If you are using the ASP.NET Development Server (the default web server used by Visual Studio) then your application executes within the context of your Windows user account.</span></span> <span data-ttu-id="a96d9-192">在这种情况下，你需要添加 Windows 用户帐户作为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="a96d9-192">In that case, you need to add your Windows user account as a database server login.</span></span>

<span data-ttu-id="a96d9-193">或者，如果使用 Internet Information Services，则需要添加 ASPNET 帐户或 NT 颁发机构/网络服务帐户作为数据库服务器登录名。</span><span class="sxs-lookup"><span data-stu-id="a96d9-193">Alternatively, if you are using Internet Information Services then you need to add either the ASPNET account or the NT AUTHORITY/NETWORK SERVICE account as a database server login.</span></span> <span data-ttu-id="a96d9-194">如果使用的是 Windows XP，请将 ASPNET 帐户作为登录名添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="a96d9-194">If you are using Windows XP then add the ASPNET account as a login to your database.</span></span> <span data-ttu-id="a96d9-195">如果你使用的是更新的操作系统（例如 Windows Vista 或 Windows Server 2008），则添加 NT 颁发机构/网络服务帐户作为数据库登录名。</span><span class="sxs-lookup"><span data-stu-id="a96d9-195">If you are using a more recent operating system, such as Windows Vista or Windows Server 2008, then add the NT AUTHORITY/NETWORK SERVICE account as the database login.</span></span>

<span data-ttu-id="a96d9-196">您可以使用 Microsoft SQL Server Management Studio 将新用户帐户添加到数据库（请参阅图9）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-196">You can add a new user account to your database by using Microsoft SQL Server Management Studio (see Figure 9).</span></span>

<span data-ttu-id="a96d9-197">**图9–创建新的 Microsoft SQL Server 登录名**</span><span class="sxs-lookup"><span data-stu-id="a96d9-197">**Figure 9 – Creating a new Microsoft SQL Server login**</span></span>

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

<span data-ttu-id="a96d9-199">创建所需的登录名后，需要将登录名映射到具有正确数据库角色的数据库用户。</span><span class="sxs-lookup"><span data-stu-id="a96d9-199">After you create the required login, you need to map the login to a database user with the right database roles.</span></span> <span data-ttu-id="a96d9-200">双击该登录名，然后选择 "用户映射" 选项卡。选择一个或多个应用程序服务数据库角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-200">Double-click the login and select the User Mapping tab. Select one or more application services database roles.</span></span> <span data-ttu-id="a96d9-201">例如，要对用户进行身份验证，你需要启用 aspnet\_成员身份\_BasicAccess 数据库角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-201">For example, in order to authenticate users, you need to enable the aspnet\_Membership\_BasicAccess database role.</span></span> <span data-ttu-id="a96d9-202">若要创建新用户，你需要启用 aspnet\_成员身份\_FullAccess 数据库角色（请参阅图10）。</span><span class="sxs-lookup"><span data-stu-id="a96d9-202">In order to create new users, you need to enable the aspnet\_Membership\_FullAccess database role (see Figure 10).</span></span>

<span data-ttu-id="a96d9-203">**图 10-添加应用程序服务数据库角色**</span><span class="sxs-lookup"><span data-stu-id="a96d9-203">**Figure 10 – Adding Application Services database roles**</span></span>

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a><span data-ttu-id="a96d9-205">摘要</span><span class="sxs-lookup"><span data-stu-id="a96d9-205">Summary</span></span>

<span data-ttu-id="a96d9-206">在本教程中，已了解如何在生成 ASP.NET MVC 应用程序时使用 Forms 身份验证。</span><span class="sxs-lookup"><span data-stu-id="a96d9-206">In this tutorial, you learned how to use Forms authentication when building an ASP.NET MVC application.</span></span> <span data-ttu-id="a96d9-207">首先，您学习了如何通过利用网站管理工具来创建新用户和角色。</span><span class="sxs-lookup"><span data-stu-id="a96d9-207">First, you learned how to create new users and roles by taking advantage of the Web Site Administration Tool.</span></span> <span data-ttu-id="a96d9-208">接下来，您学习了如何使用 [授权] 属性来防止未经授权的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a96d9-208">Next, you learned how to use the [Authorize] attribute to prevent unauthorized users from invoking controller actions.</span></span> <span data-ttu-id="a96d9-209">最后，你已了解如何将 MVC 应用程序配置为将用户和角色信息存储在生产数据库中。</span><span class="sxs-lookup"><span data-stu-id="a96d9-209">Finally, you learned how to configure your MVC application to store user and role information in a production database.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a96d9-210">下一部分</span><span class="sxs-lookup"><span data-stu-id="a96d9-210">Next</span></span>](authenticating-users-with-windows-authentication-cs.md)
