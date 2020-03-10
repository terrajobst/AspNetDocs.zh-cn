---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 成员身份 |Microsoft Docs
author: microsoft
description: ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。 ASP.NET Forms 身份验证提供了一种简便的方法来 incorp 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521702"
---
# <a name="membership"></a><span data-ttu-id="4fb1d-104">成员身份</span><span class="sxs-lookup"><span data-stu-id="4fb1d-104">Membership</span></span>

<span data-ttu-id="4fb1d-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4fb1d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4fb1d-106">ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="4fb1d-107">ASP.NET Forms 身份验证提供了一种方便的方法，可将登录窗体合并到 ASP.NET 应用程序中，并针对数据库或其他数据存储来验证用户。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>

<span data-ttu-id="4fb1d-108">ASP.NET 成员资格建立在 ASP.NET 1.x 中窗体身份验证模型成功的基础之上。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="4fb1d-109">ASP.NET Forms 身份验证提供了一种方便的方法，可将登录窗体合并到 ASP.NET 应用程序中，并针对数据库或其他数据存储来验证用户。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="4fb1d-110">使用 FormsAuthentication 类的成员可以处理用于身份验证的 cookie，检查有效的登录名，记录用户，等等。但是，在 ASP.NET 1.x 应用程序中实现 Forms 身份验证可能需要相当多的代码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="4fb1d-111">ASP.NET 2.0 中的成员资格是单独使用窗体身份验证的主要进步。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="4fb1d-112">（与 Forms 身份验证结合使用时，成员资格最可靠，但不要求使用窗体身份验证。）如您所见，您可以使用 ASP.NET 成员身份和 ASP.NET 2.0 中的登录控件来实现功能强大的成员资格系统，而无需编写大量代码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="4fb1d-113">在 ASP.NET 2.0 中实现成员资格</span><span class="sxs-lookup"><span data-stu-id="4fb1d-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="4fb1d-114">成员资格通过以下四个步骤实现。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="4fb1d-115">请记住，有许多子步骤以及可实现的可选配置也是如此。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="4fb1d-116">这些步骤旨在说明配置成员身份的大图。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="4fb1d-117">创建成员资格数据库（如果 SQL Server 用作成员资格存储区。）</span><span class="sxs-lookup"><span data-stu-id="4fb1d-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="4fb1d-118">指定应用程序配置文件中的成员资格选项。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="4fb1d-119">（默认情况下启用成员身份。）</span><span class="sxs-lookup"><span data-stu-id="4fb1d-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="4fb1d-120">确定要使用的成员资格存储区的类型。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="4fb1d-121">选项包括：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-121">Options are:</span></span> 

    - <span data-ttu-id="4fb1d-122">Microsoft SQL Server （版本7.0 或更高版本）</span><span class="sxs-lookup"><span data-stu-id="4fb1d-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="4fb1d-123">Active Directory 存储</span><span class="sxs-lookup"><span data-stu-id="4fb1d-123">Active Directory Store</span></span>
    - <span data-ttu-id="4fb1d-124">自定义成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="4fb1d-124">Custom membership provider</span></span>
4. <span data-ttu-id="4fb1d-125">为 ASP.NET Forms 身份验证配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="4fb1d-126">同样，成员资格旨在利用 Forms 身份验证，但不要求使用窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="4fb1d-127">定义成员身份的用户帐户，并根据需要配置角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="4fb1d-128">创建成员资格数据库</span><span class="sxs-lookup"><span data-stu-id="4fb1d-128">Creating the Membership Database</span></span>

<span data-ttu-id="4fb1d-129">如果使用 SQL Server 7.0 或更高版本作为成员资格存储区，则可以使用 aspnet\_regsql 实用工具（最轻松地从 Visual Studio .NET 2005 命令提示符获取）来配置数据库。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-129">If you're using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="4fb1d-130">Aspnet\_regsql 实用工具可用作命令提示符工具或通过 GUI 向导。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="4fb1d-131">向导方法是配置数据库的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="4fb1d-132">若要访问该向导，只需运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="4fb1d-133">运行该命令后，将显示 ASP.NET SQL Server 安装向导，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>

![](membership/_static/image1.jpg)

<span data-ttu-id="4fb1d-134">**图1**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-134">**Figure 1**</span></span>

<span data-ttu-id="4fb1d-135">ASP.NET SQL Server 安装向导将在您在向导中指定的实例中创建网站。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="4fb1d-136">但是，ASP.NET 将使用 machine.config 文件中的连接字符串连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="4fb1d-137">默认情况下，此连接字符串将指向 SQL Server 2005 实例，因此，如果使用 SQL Server 2000 或 SQL Server 7.0 实例，则需要修改 machine.config 文件中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="4fb1d-138">可在此处找到该连接字符串：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="4fb1d-139">遗憾的是，如果不修改连接字符串，ASP.NET 将不会给您带来描述性错误。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-139">Unfortunately, if you don't modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="4fb1d-140">这只是因为您并未创建数据库。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-140">It will just continue to complain saying that you haven't created the database.</span></span> <span data-ttu-id="4fb1d-141">在上面的示例中，我修改了指向本地 SQL Server 2000 实例的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="4fb1d-142">指定配置并添加用户和角色</span><span class="sxs-lookup"><span data-stu-id="4fb1d-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="4fb1d-143">配置成员身份的下一步是将所需的信息添加到应用程序的 web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="4fb1d-144">在 ASP.NET 1.x 中，修改 web.config 文件有时很难，因为使用的是 lowerCamelCase，而缺少 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="4fb1d-145">Visual Studio .NET 2005 通过为配置文件使用 Intellisense 使任务更容易，但通过提供用于编辑配置文件的 Web 界面，ASP.NET 2.0 进一步提高了一步。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="4fb1d-146">可以通过单击解决方案资源管理器工具栏上的 "ASP.NET 配置" 按钮来启动 Web 界面，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="4fb1d-147">还可以通过在插入登录控件时显示的弹出窗口启动 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>

![](membership/_static/image2.jpg)

<span data-ttu-id="4fb1d-148">**图2**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-148">**Figure 2**</span></span>

<span data-ttu-id="4fb1d-149">这将启动如下所示的 ASP.NET 网站管理工具。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="4fb1d-150">ASP.NET 网站管理是一个四个选项卡界面，可让你轻松管理应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="4fb1d-151">提供以下选项卡：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-151">The following tabs are available:</span></span>

- <span data-ttu-id="4fb1d-152">**Home**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-152">**Home**</span></span>
- <span data-ttu-id="4fb1d-153">**安全**配置用户、角色和访问权限。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="4fb1d-154">**应用程序**配置应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="4fb1d-155">**提供程序**配置和测试应用程序成员资格提供程序。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="4fb1d-156">网站管理工具可让你轻松地创建新用户、创建新角色以及管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="4fb1d-157">此功能在 Windows 界面中不可用。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="4fb1d-158">Windows 界面允许你轻松定义授权设置，以及添加、删除和管理不在网站管理工具中的提供程序和功能。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="4fb1d-159">若要启动 Windows 界面，请打开 Internet Information Services 管理单元，右键单击应用程序，然后选择 "属性"。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="4fb1d-160">单击 "ASP.NET" 选项卡，然后单击 "编辑配置" 按钮。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="4fb1d-161">（若要启用 "编辑配置" 按钮，应用程序必须在 ASP.NET 2.0 下运行。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="4fb1d-162">也可以在 ASP.NET 对话框中配置 ASP.NET 版本。）将显示 ASP.NET 配置设置对话框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>

![](membership/_static/image3.jpg)

<span data-ttu-id="4fb1d-163">**图3**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-163">**Figure 3**</span></span>

<span data-ttu-id="4fb1d-164">在 "常规" 选项卡上，将列出连接字符串和应用程序设置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="4fb1d-165">斜体中的任何设置都是在父配置文件（machine.config 或更高级别的 web.config）中定义的，而斜体的设置则来自应用程序配置文件。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="4fb1d-166">如果在应用程序级别添加、删除或编辑设置，则 ASP.NET 将在应用程序级别的 web.config 中添加、删除或修改设置，而不是从继承它的配置文件中移除设置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="4fb1d-167">"身份验证" 选项卡如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="4fb1d-168">这是你将在其中配置成员资格设置的位置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="4fb1d-169">可以在此处配置窗体身份验证设置、成员资格提供程序和角色提供程序。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>

![](membership/_static/image4.jpg)

<span data-ttu-id="4fb1d-170">**图4**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-170">**Figure 4**</span></span>

## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="4fb1d-171">在应用程序中实现成员资格</span><span class="sxs-lookup"><span data-stu-id="4fb1d-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="4fb1d-172">在应用程序中实现 ASP.NET 2.0 成员身份的最简单方法是使用提供的登录控件。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="4fb1d-173">此方法允许实现 ASP.NET 2.0 成员资格的基本知识，无需编写任何代码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="4fb1d-174">ASP.NET 2.0 中提供以下登录控件：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="4fb1d-175">登录控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-175">Login Control</span></span>

<span data-ttu-id="4fb1d-176">Login 控件提供一个接口，供某人登录到你的成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="4fb1d-177">它提供 "用户名" 和 "密码" 文本框，以及一个 "登录" 按钮。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-177">It provides you with a username and password textbox and a login button.</span></span> <span data-ttu-id="4fb1d-178">许多其他常见功能，如用于注册尚未执行此操作的人员的链接、允许用户在后续访问时自动登录的复选框、密码提示的链接等。登录控件的所有功能都可通过控件的属性进行自定义。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="4fb1d-179">在 ASP.NET 1.x 中，开发人员在使用窗体身份验证时，必须编写大量代码来执行查找。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="4fb1d-180">借助 ASP.NET 2.0 成员身份，无需编写任何代码即可验证用户。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="4fb1d-181">ASP.NET 会自动为用户执行查找。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="4fb1d-182">（如果在不使用 ASP.NET 成员身份的情况下使用登录控件，则可以使用**OnAuthenticate**方法来验证用户。）</span><span class="sxs-lookup"><span data-stu-id="4fb1d-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="4fb1d-183">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-183">LoginView Control</span></span>

<span data-ttu-id="4fb1d-184">登录视图控件是默认情况下提供两个模板的模板化控件。AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="4fb1d-185">显示的模板取决于用户是否登录到成员身份系统。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="4fb1d-186">此控件通常用于在用户尚未登录时显示登录控件，并在用户登录时显示 LoginStatus 控件和/或其他登录控件。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="4fb1d-187">如果在 ASP.NET 应用程序中使用角色管理，则登录视图控件可以基于用户角色显示特定模板。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="4fb1d-188">（稍后将详细介绍 ASP.NET 角色管理。）</span><span class="sxs-lookup"><span data-stu-id="4fb1d-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="4fb1d-189">PasswordRecovery 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-189">PasswordRecovery Control</span></span>

<span data-ttu-id="4fb1d-190">PasswordRecovery 控件允许用户使用其当前密码或重置其密码来接收电子邮件。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="4fb1d-191">明文和加密密码可以恢复，并通过电子邮件发送给用户。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="4fb1d-192">如果对密码进行哈希处理，则无法对其进行恢复。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="4fb1d-193">用户需要执行密码重置。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="4fb1d-194">LoginStatus 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-194">LoginStatus Control</span></span>

<span data-ttu-id="4fb1d-195">LoginStatus 控件用于向未登录的用户以及当前登录的用户显示一条注销指示器的登录指示器。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="4fb1d-196">IsAuthenticated 属性用于确定要显示的指示器。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="4fb1d-197">LoginStatus 控件显示的指示器可以是文本（通过**LoginText**和**LogoutText**属性实现）或图像（通过**LoginImageUrl**和**LogoutImageUrl**属性来实现）。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="4fb1d-198">当用户通过 LoginStatus 控件注销时，他（她）将重定向到**LogoutPageUrl**属性指定的 URL。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="4fb1d-199">如果未设置该属性，则刷新当前页面。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="4fb1d-200">由于站点可能受到 Forms 身份验证的保护，因此刷新当前页面会将用户重定向到站点的登录页。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="4fb1d-201">LoginName 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-201">LoginName Control</span></span>

<span data-ttu-id="4fb1d-202">LoginName 控件显示当前登录到网站的用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="4fb1d-203">CreateUserWizard 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-203">CreateUserWizard Control</span></span>

<span data-ttu-id="4fb1d-204">CreateUserWizard 控件为用户提供了一种方便的方法来注册你的成员资格系统。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="4fb1d-205">可以通过如下所示的接口添加步骤（作为 WizardSteps 的集合实现）。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>

![](membership/_static/image5.jpg)

<span data-ttu-id="4fb1d-206">**图5**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-206">**Figure 5**</span></span>

<span data-ttu-id="4fb1d-207">CreateUserWizard 是一个模板化控件，该控件派生自 Wizard 类并提供以下模板：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="4fb1d-208">**System.windows.controls.headereditemscontrol.headertemplate**此模板控制向导的标题外观。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="4fb1d-209">**SidebarTemplate**此模板控制向导边栏的外观。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="4fb1d-210">**StartNavigationTemplate**此模板控制导航在开始步骤中的外观。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="4fb1d-211">**StepNavigationTemplate**当不在开始或完成步骤中时，此模板控制导航区域的外观。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="4fb1d-212">**FinishNavigationTemplate**此模板控制在完成步骤时导航区域的外观。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="4fb1d-213">此外，对于添加到向导的每个步骤，ASP.NET 将创建一个自定义模板，该模板包含该步骤的 System.windows.controls.contentcontrol.contenttemplate 和 CustomNavigationTemplate。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="4fb1d-214">有关自定义 CreateUserWizard 的完整详细信息，请参阅 VS.NET 2005 文档：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="4fb1d-215">ChangePassword 控件</span><span class="sxs-lookup"><span data-stu-id="4fb1d-215">ChangePassword Control</span></span>

<span data-ttu-id="4fb1d-216">ChangePassword 控件允许用户更改其密码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="4fb1d-217">如果 DisplayUserName 属性为 true （默认值为 false），则用户可以在未登录时更改其密码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="4fb1d-218">如果用户已登录，并且 DisplayUserName 属性为 true，*则用户将*可以更改未登录的另一个用户的密码，以使用户知道该用户的用户 ID。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="4fb1d-219">请记住，如果你希望用户能够在无需登录的情况下更改密码，则需要确保显示 ChangePassword 控件的页面允许匿名访问。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="4fb1d-220">很明显，用户必须提供旧密码才能更改密码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="4fb1d-221">角色管理</span><span class="sxs-lookup"><span data-stu-id="4fb1d-221">Role Management</span></span>

<span data-ttu-id="4fb1d-222">使用角色管理，可以将用户分配到特定角色，然后根据该角色限制对特定文件或文件夹的访问。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="4fb1d-223">角色管理还提供了一个 API，使你能够以编程方式确定 someones 角色或确定特定角色中的所有用户并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="4fb1d-224">角色管理并不是 ASP.NET 成员身份的要求，也不要求成员身份来使用角色管理。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="4fb1d-225">但是，这两个方法都非常合适，开发人员可能会将它们彼此结合使用。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="4fb1d-226">若要在应用程序中启用角色管理，请在 web.config 文件中进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="4fb1d-227">当**cacheRolesInCookie**属性设置为 true 时，ASP.NET 会在客户端上的 cookie 中缓存用户角色成员身份。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="4fb1d-228">这允许在不调用 RoleProvider 的情况下进行角色查找。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="4fb1d-229">使用此属性时，鼓励开发人员确保将**cookieProtection**属性设置为 All。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="4fb1d-230">（这是默认设置。）这可确保 cookie 数据已加密，并有助于确保 cookie 内容未被更改。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents haven't been altered.</span></span> <span data-ttu-id="4fb1d-231">可以使用网站管理工具添加角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="4fb1d-232">它允许你轻松定义角色、根据这些角色配置对站点各部分的访问权限，并将用户分配到角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>

![](membership/_static/image6.jpg)

<span data-ttu-id="4fb1d-233">**图6**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-233">**Figure 6**</span></span>

<span data-ttu-id="4fb1d-234">如上所示，只需输入角色的名称，然后单击 "添加角色" 即可添加新角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="4fb1d-235">可以通过在现有角色列表中单击相应的链接来管理或删除现有角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="4fb1d-236">管理角色时，可以添加或删除用户，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-236">When you manage a role, you can add or remove users as shown below.</span></span>

![](membership/_static/image7.jpg)

<span data-ttu-id="4fb1d-237">**图7**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-237">**Figure 7**</span></span>

<span data-ttu-id="4fb1d-238">通过选中 "用户处于角色中" 复选框，你可以轻松地将用户添加到特定角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="4fb1d-239">ASP.NET 将自动用适当的条目更新你的成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="4fb1d-240">你还需要为应用程序配置访问规则。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="4fb1d-241">ASP.NET 1.x 开发人员熟悉了如何通过 web.config 文件中的 &lt;authorization&gt; 元素来执行此操作，并且 ASP.NET 2.0 中仍提供该选项。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="4fb1d-242">但是，使用网站管理工具管理访问规则更为容易，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>

![](membership/_static/image8.jpg)

<span data-ttu-id="4fb1d-243">**图8**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-243">**Figure 8**</span></span>

<span data-ttu-id="4fb1d-244">在这种情况下，将突出显示 "管理" 文件夹（由于该工具以浅灰色突出显示它很难查看），并且已授予管理员角色访问权限。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="4fb1d-245">拒绝所有其他用户。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-245">All other users are denied.</span></span> <span data-ttu-id="4fb1d-246">你可以单击 head 图标以选择一个规则，然后使用 "上移" 和 "下移" 按钮来排列规则。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="4fb1d-247">与 ASP.NET &lt;授权&gt; 元素一样，规则按它们出现的顺序进行处理。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="4fb1d-248">换句话说，如果上面的快照中的规则顺序已撤消，则任何人都无法访问管理文件夹，因为 ASP.NET 将遇到的第一个规则是 "拒绝每个人" 文件夹的规则。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="4fb1d-249">ASP.NET 2.0 将 web.config 文件添加到要为其指定访问规则的文件夹。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="4fb1d-250">可以通过配置文件或网站管理工具编辑访问规则。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="4fb1d-251">换句话说，网站管理工具只是一个接口，通过它可以在用户友好的环境中编辑配置文件。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="4fb1d-252">在代码中使用角色</span><span class="sxs-lookup"><span data-stu-id="4fb1d-252">Using Roles in Code</span></span>

<span data-ttu-id="4fb1d-253">从版本1.x 开始，角色管理的 API 尚未更改。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="4fb1d-254">**IsInRole**方法用于确定用户是否属于特定角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="4fb1d-255">ASP.NET 还会将 RolePrincipal 实例创建为当前上下文的成员。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="4fb1d-256">RolePrincipal 对象可用于获取用户所属的所有角色，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="4fb1d-257">将 RoleGroups 与登录视图控件一起使用</span><span class="sxs-lookup"><span data-stu-id="4fb1d-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="4fb1d-258">现在，你已了解角色管理和成员身份，接下来我们将简要介绍登录视图控件如何利用 ASP.NET 2.0 中的此功能。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="4fb1d-259">如前所述，登录视图控件是模板化控件，默认情况下包含两个模板;AnonymousTemplate 和 LoggedInTemplate。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="4fb1d-260">在 "登录视图任务" 对话框中，可以使用以下链接（如下所示）编辑 RoleGroups。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>

![](membership/_static/image9.jpg)

<span data-ttu-id="4fb1d-261">**图9**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-261">**Figure 9**</span></span>

<span data-ttu-id="4fb1d-262">每个 RoleGroup 对象都包含一个字符串数组，用于定义 RoleGroup 应用于哪些角色。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="4fb1d-263">若要将新的 RoleGroup 添加到登录视图控件，请单击 "编辑 RoleGroups" 链接。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="4fb1d-264">在上面的图像中，可以看到我为管理员添加了新的 RoleGroup。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="4fb1d-265">通过从 "视图" 下拉列表中选择 "RoleGroup （RoleGroup [0]"），我可以配置只向管理员角色的成员显示的模板。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="4fb1d-266">在下图中，我添加了一个新的 RoleGroup，适用于 "销售" 角色和 "分发" 角色的成员。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="4fb1d-267">这会将第二个 RoleGroup 添加到 "登录视图任务" 对话框中的 "视图" 下拉列表中，任何添加到该模板的内容都将由 "销售" 或 "分发" 角色中的任何用户看到</span><span class="sxs-lookup"><span data-stu-id="4fb1d-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>

![](membership/_static/image10.jpg)

<span data-ttu-id="4fb1d-268">**图10**</span><span class="sxs-lookup"><span data-stu-id="4fb1d-268">**Figure 10**</span></span>

## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="4fb1d-269">重写现有成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="4fb1d-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="4fb1d-270">可以通过几种方式来扩展 ASP.NET 成员身份的功能。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="4fb1d-271">首先，可以通过从 SqlMembershipProvider 类继承并重写其方法来更改现有功能。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="4fb1d-272">例如，如果你想要在创建用户时实现自己的功能，则可以创建你自己的从 SqlMembershipProvider 继承的类，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="4fb1d-273">另一方面，如果要创建自己的提供程序（例如，将成员身份信息存储在 Access 数据库中），则可以创建自己的提供程序。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="4fb1d-274">创建自己的成员资格提供程序</span><span class="sxs-lookup"><span data-stu-id="4fb1d-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="4fb1d-275">若要创建自己的成员资格提供程序，首先需要创建一个从 MembershipProvider 类继承的类。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="4fb1d-276">如果使用的是 VB.NET，Visual Studio 2005 将为需要重写的所有方法添加存根。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="4fb1d-277">如果你使用C#的是，则它将添加存根。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="4fb1d-278">需要重写以下项：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-278">You will need to override the following:</span></span>

- <span data-ttu-id="4fb1d-279">ApplicationName 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-279">ApplicationName property</span></span>
- <span data-ttu-id="4fb1d-280">ChangePassword 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-280">ChangePassword function</span></span>
- <span data-ttu-id="4fb1d-281">ChangePasswordQuestionAndAnswer 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="4fb1d-282">CreateUser 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-282">CreateUser function</span></span>
- <span data-ttu-id="4fb1d-283">DeleteUser 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-283">DeleteUser function</span></span>
- <span data-ttu-id="4fb1d-284">EnablePasswordReset 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="4fb1d-285">EnablePasswordRetrieval 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="4fb1d-286">FindUsersByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="4fb1d-287">FindUsersByName 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-287">FindUsersByName function</span></span>
- <span data-ttu-id="4fb1d-288">GetAllUsers 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-288">GetAllUsers function</span></span>
- <span data-ttu-id="4fb1d-289">GetNumberOfUsersOnline 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="4fb1d-290">GetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-290">GetPassword function</span></span>
- <span data-ttu-id="4fb1d-291">GetUser 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-291">GetUser function</span></span>
- <span data-ttu-id="4fb1d-292">GetUserNameByEmail 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="4fb1d-293">MaxInvalidPasswordAttempts 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="4fb1d-294">MinRequiredNonAlphanumericCharacters 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="4fb1d-295">MinRequiredPasswordLength 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="4fb1d-296">PasswordAttemptWindow 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="4fb1d-297">PasswordFormat 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-297">PasswordFormat property</span></span>
- <span data-ttu-id="4fb1d-298">PasswordStrengthRegularExpression 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="4fb1d-299">RequiresQuestionAndAnswer 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="4fb1d-300">RequiresUniqueEmail 属性</span><span class="sxs-lookup"><span data-stu-id="4fb1d-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="4fb1d-301">ResetPassword 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-301">ResetPassword function</span></span>
- <span data-ttu-id="4fb1d-302">解锁用户函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-302">Unlock user function</span></span>
- <span data-ttu-id="4fb1d-303">UpdateUser 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-303">UpdateUser function</span></span>
- <span data-ttu-id="4fb1d-304">System.web.security.membership.validateuser 函数</span><span class="sxs-lookup"><span data-stu-id="4fb1d-304">ValidateUser function</span></span>

<span data-ttu-id="4fb1d-305">这相当于作为C#开发人员实现的列表。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="4fb1d-306">你可能会发现，无需任何实现即可在 VB.NET 中创建类，然后使用 .NET 反射器或类似的工具将代码转换C#为。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="4fb1d-307">应将连接字符串和其他属性设置为 Initialize 方法中的默认值。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="4fb1d-308">（当在运行时加载提供程序时，将触发 Initialize 方法。）Initialize 方法的第二个参数的类型为 NameValueCollection，是对 &lt;添加与 web.config 文件中的自定义提供程序相关联&gt; 元素的引用。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="4fb1d-309">该条目如下所示：</span><span class="sxs-lookup"><span data-stu-id="4fb1d-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="4fb1d-310">下面是 Initialize 方法的示例。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="4fb1d-311">若要在用户提交登录窗体时验证用户，你需要使用 System.web.security.membership.validateuser 方法。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="4fb1d-312">当用户在登录控件中单击 "登录" 按钮时，将激发此方法。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="4fb1d-313">您将在此方法中放置执行用户查找的代码。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="4fb1d-314">正如您所看到的，编写自己的成员资格提供程序并不困难，并允许您扩展 ASP.NET 2.0 的这一功能强大的功能。</span><span class="sxs-lookup"><span data-stu-id="4fb1d-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>
