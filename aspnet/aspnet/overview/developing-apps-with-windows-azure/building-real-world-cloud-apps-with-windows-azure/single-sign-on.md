---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 单一登录（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585285"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="09cd8-104">单一登录（通过 Azure 构建实际的云应用）</span><span class="sxs-lookup"><span data-stu-id="09cd8-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="09cd8-105">作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="09cd8-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="09cd8-106">[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="09cd8-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="09cd8-107">**使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="09cd8-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="09cd8-108">它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。</span><span class="sxs-lookup"><span data-stu-id="09cd8-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="09cd8-109">有关电子书的信息，请参阅[第一章](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="09cd8-110">开发云应用程序时需要考虑许多安全问题，但对于此系列，我们将重点介绍一种：单一登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="09cd8-111">用户经常问的问题是： "我主要为公司的员工构建应用;我如何将这些应用程序托管在云中，并使他们能够使用在本地环境中运行的应用程序时所用的相同安全模型？</span><span class="sxs-lookup"><span data-stu-id="09cd8-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="09cd8-112">启用此方案的一种方式称为 Azure Active Directory （Azure AD）。</span><span class="sxs-lookup"><span data-stu-id="09cd8-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="09cd8-113">Azure AD 使你能够通过 Internet 提供企业业务线（LOB）应用，并使你能够将这些应用程序提供给业务合作伙伴。</span><span class="sxs-lookup"><span data-stu-id="09cd8-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="09cd8-114">Azure AD 简介</span><span class="sxs-lookup"><span data-stu-id="09cd8-114">Introduction to Azure AD</span></span>

<span data-ttu-id="09cd8-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/)在云中提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="09cd8-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="09cd8-116">关键功能包括：</span><span class="sxs-lookup"><span data-stu-id="09cd8-116">Key features include the following:</span></span>

- <span data-ttu-id="09cd8-117">它与本地 Active Directory 集成。</span><span class="sxs-lookup"><span data-stu-id="09cd8-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="09cd8-118">它支持应用的单一登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="09cd8-119">它支持开放标准，如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [WS 送送](http://en.wikipedia.org/wiki/WS-Federation)和[OAuth 2.0](http://oauth.net/2/)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="09cd8-120">它支持企业[关系图 REST API](https://msdn.microsoft.com/library/hh974476.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="09cd8-121">假设你有一个本地 Windows Server Active Directory 环境，你可以使用它来使员工登录 Intranet 应用：</span><span class="sxs-lookup"><span data-stu-id="09cd8-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="09cd8-122">您可以使用哪些 Azure AD 在云中创建目录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="09cd8-123">这是一项免费功能，易于设置。</span><span class="sxs-lookup"><span data-stu-id="09cd8-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="09cd8-124">它可以完全独立于本地 Active Directory;你可以将所需的任何人置于 Internet 应用中并对其进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="09cd8-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="09cd8-126">也可以将其与本地 AD 集成。</span><span class="sxs-lookup"><span data-stu-id="09cd8-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 和 WAAD 集成](single-sign-on/_static/image3.png)

<span data-ttu-id="09cd8-128">现在，可以在本地进行身份验证的所有员工还可以通过 Internet 进行身份验证–无需打开防火墙或在数据中心部署任何新服务器。</span><span class="sxs-lookup"><span data-stu-id="09cd8-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="09cd8-129">你可以继续利用你知道和使用的所有现有 Active Directory 环境，为你的内部应用程序使用单一登录功能。</span><span class="sxs-lookup"><span data-stu-id="09cd8-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="09cd8-130">在 AD 和 Azure AD 之间建立此连接后，你还可以让你的 web 应用和移动设备对云中的员工进行身份验证，并可以启用第三方应用（例如 Office 365、SalesForce.com 或 Google apps），以接受你的员工凭据。</span><span class="sxs-lookup"><span data-stu-id="09cd8-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="09cd8-131">如果你使用的是 Office 365，则已设置了 Azure AD，因为 Office 365 使用 Azure AD 进行身份验证和授权。</span><span class="sxs-lookup"><span data-stu-id="09cd8-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![第三方应用](single-sign-on/_static/image4.png)

<span data-ttu-id="09cd8-133">这种方法的优点在于，无论你的组织是添加还是删除用户，或者用户更改密码，都可以使用你今天在本地环境中使用的相同过程。</span><span class="sxs-lookup"><span data-stu-id="09cd8-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="09cd8-134">所有本地 AD 更改都会自动传播到云环境。</span><span class="sxs-lookup"><span data-stu-id="09cd8-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="09cd8-135">如果你的公司使用或转到 Office 365，好消息是你将 Azure AD 自动设置，因为 Office 365 使用 Azure AD 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="09cd8-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="09cd8-136">因此，您可以在自己的应用程序中轻松地使用 Office 365 使用的相同身份验证。</span><span class="sxs-lookup"><span data-stu-id="09cd8-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="09cd8-137">设置 Azure AD 租户</span><span class="sxs-lookup"><span data-stu-id="09cd8-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="09cd8-138">Azure AD 目录称为 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)，设置租户非常简单。</span><span class="sxs-lookup"><span data-stu-id="09cd8-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="09cd8-139">我们将向你演示如何在 Azure 管理门户中完成此操作，以便阐释概念，但正如其他门户功能，你也可以通过使用脚本或管理 API 来执行此操作。</span><span class="sxs-lookup"><span data-stu-id="09cd8-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="09cd8-140">在管理门户中，单击 "Active Directory" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="09cd8-140">In the management portal click the Active Directory tab.</span></span>

![门户中的 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="09cd8-142">你的 Azure 帐户会自动拥有一个 Azure AD 租户，你可以单击页面底部的 "**添加**" 按钮创建其他目录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="09cd8-143">例如，你可能需要一个用于测试环境，一个用于生产环境。</span><span class="sxs-lookup"><span data-stu-id="09cd8-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="09cd8-144">仔细考虑新目录的名称。</span><span class="sxs-lookup"><span data-stu-id="09cd8-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="09cd8-145">如果使用目录的名称，然后对其中一个用户再次使用该名称，这可能会造成混淆。</span><span class="sxs-lookup"><span data-stu-id="09cd8-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![添加目录](single-sign-on/_static/image6.png)

<span data-ttu-id="09cd8-147">门户完全支持创建、删除和管理此环境中的用户。</span><span class="sxs-lookup"><span data-stu-id="09cd8-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="09cd8-148">例如，若要添加用户，请单击 "**用户**" 选项卡，然后单击 "**添加用户**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="09cd8-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![“添加用户”按钮](single-sign-on/_static/image7.png)

![添加用户对话框](single-sign-on/_static/image8.png)

<span data-ttu-id="09cd8-151">你可以创建仅在此目录中存在的新用户，也可以将 Microsoft 帐户注册为此目录中的用户，或者在此目录中以用户的身份注册或其他 Azure AD 目录中的用户。</span><span class="sxs-lookup"><span data-stu-id="09cd8-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="09cd8-152">（在实际目录中，默认域为 ContosoTest.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="09cd8-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="09cd8-153">你还可以使用自己选择的域，如 contoso.com。）</span><span class="sxs-lookup"><span data-stu-id="09cd8-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![用户类型](single-sign-on/_static/image9.png)

![添加用户对话框](single-sign-on/_static/image10.png)

<span data-ttu-id="09cd8-156">您可以将用户分配到角色。</span><span class="sxs-lookup"><span data-stu-id="09cd8-156">You can assign the user to a role.</span></span>

![用户配置文件](single-sign-on/_static/image11.png)

<span data-ttu-id="09cd8-158">使用临时密码创建帐户。</span><span class="sxs-lookup"><span data-stu-id="09cd8-158">And the account is created with a temporary password.</span></span>

![临时密码](single-sign-on/_static/image12.png)

<span data-ttu-id="09cd8-160">你以这种方式创建的用户可以使用此云目录立即登录到你的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="09cd8-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="09cd8-161">不过，企业单一登录的好处是 "**目录集成**" 选项卡：</span><span class="sxs-lookup"><span data-stu-id="09cd8-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![目录集成选项卡](single-sign-on/_static/image13.png)

<span data-ttu-id="09cd8-163">如果启用 "目录集成" 和 "[下载工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)"，则可以将此云目录与已在组织内部使用的现有本地 Active Directory 同步。</span><span class="sxs-lookup"><span data-stu-id="09cd8-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="09cd8-164">然后，存储在目录中的所有用户将显示在此云目录中。</span><span class="sxs-lookup"><span data-stu-id="09cd8-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="09cd8-165">你的云应用现在可以使用其现有 Active Directory 凭据对你的所有员工进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="09cd8-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="09cd8-166">所有这些都是免费的–同步工具和 Azure AD 本身。</span><span class="sxs-lookup"><span data-stu-id="09cd8-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="09cd8-167">此工具是一个易于使用的向导，如您在这些屏幕截图中看到的那样。</span><span class="sxs-lookup"><span data-stu-id="09cd8-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="09cd8-168">这些不是完整的说明，只是显示基本过程的示例。</span><span class="sxs-lookup"><span data-stu-id="09cd8-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="09cd8-169">有关操作方法的详细信息，请参阅本章末尾的[资源](#resources)部分中的链接。</span><span class="sxs-lookup"><span data-stu-id="09cd8-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image14.png)

<span data-ttu-id="09cd8-171">单击 "**下一步**"，然后输入 Azure Active Directory 凭据。</span><span class="sxs-lookup"><span data-stu-id="09cd8-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image15.png)

<span data-ttu-id="09cd8-173">单击 "**下一步**"，然后输入本地 AD 凭据。</span><span class="sxs-lookup"><span data-stu-id="09cd8-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image16.png)

<span data-ttu-id="09cd8-175">单击 "**下一步**"，然后指示是否要在云中存储 AD 密码的哈希。</span><span class="sxs-lookup"><span data-stu-id="09cd8-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image17.png)

<span data-ttu-id="09cd8-177">可以存储在云中的密码哈希是单向哈希;实际密码永远不会存储在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="09cd8-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="09cd8-178">如果决定不在云中存储哈希，则必须使用[Active Directory 联合身份验证服务](https://technet.microsoft.com/library/hh831502.aspx)（ADFS）。</span><span class="sxs-lookup"><span data-stu-id="09cd8-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="09cd8-179">[选择是否使用 ADFS 时，还需要考虑其他因素](https://technet.microsoft.com/library/jj573653.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="09cd8-180">ADFS 选项需要几个附加的配置步骤。</span><span class="sxs-lookup"><span data-stu-id="09cd8-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="09cd8-181">如果选择在云中存储哈希，则完成后，当单击 "**下一步**" 时，该工具将开始同步目录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image18.png)

<span data-ttu-id="09cd8-183">几分钟后你就会完成。</span><span class="sxs-lookup"><span data-stu-id="09cd8-183">And in a few minutes you're done.</span></span>

![WAAD 同步工具配置向导](single-sign-on/_static/image19.png)

<span data-ttu-id="09cd8-185">只需在组织中的一个域控制器上运行，在 Windows 2003 或更高版本上运行。</span><span class="sxs-lookup"><span data-stu-id="09cd8-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="09cd8-186">且无需重新启动。</span><span class="sxs-lookup"><span data-stu-id="09cd8-186">And no need to reboot.</span></span> <span data-ttu-id="09cd8-187">完成后，你的所有用户都位于云中，你可以使用 SAML、OAuth 或 WS-ADDRESSING 从任何 web 或移动应用程序进行单一登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="09cd8-188">有时，我们会询问您如何保护这一点– Microsoft 是否将其用于自己的敏感业务数据？</span><span class="sxs-lookup"><span data-stu-id="09cd8-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="09cd8-189">答案是肯定的。</span><span class="sxs-lookup"><span data-stu-id="09cd8-189">And the answer is yes we do.</span></span> <span data-ttu-id="09cd8-190">例如，如果你转到[https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)的内部 Microsoft SharePoint 站点，则系统会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 登录](single-sign-on/_static/image20.png)

<span data-ttu-id="09cd8-192">Microsoft 已启用 ADFS，因此，当你输入 Microsoft ID 时，会重定向到 ADFS 登录页。</span><span class="sxs-lookup"><span data-stu-id="09cd8-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 登录](single-sign-on/_static/image21.png)

<span data-ttu-id="09cd8-194">输入存储在内部 Microsoft AD 帐户中的凭据后，即可访问此内部应用程序。</span><span class="sxs-lookup"><span data-stu-id="09cd8-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 站点](single-sign-on/_static/image22.png)

<span data-ttu-id="09cd8-196">我们使用的是 AD 登录服务器，主要是因为在 Azure AD 可用之前已设置了 ADFS，但登录过程正在云中的 Azure AD 目录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="09cd8-197">我们在云中提供重要文档、源代码管理、性能管理文件、销售报表等，并使用完全相同的解决方案来保护它们。</span><span class="sxs-lookup"><span data-stu-id="09cd8-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="09cd8-198">创建使用 Azure AD 进行单一登录的 ASP.NET 应用</span><span class="sxs-lookup"><span data-stu-id="09cd8-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="09cd8-199">通过 Visual Studio，可以轻松地创建使用 Azure AD 进行单一登录的应用程序，就像从几个屏幕截图中看到的一样。</span><span class="sxs-lookup"><span data-stu-id="09cd8-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="09cd8-200">创建新的 ASP.NET 应用程序（MVC 或 Web 窗体）时，ASP.NET Identity 默认的身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="09cd8-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="09cd8-201">若要将其更改为 Azure AD，请单击 "**更改身份验证**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="09cd8-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![更改身份验证](single-sign-on/_static/image23.png)

<span data-ttu-id="09cd8-203">选择 "组织帐户"，输入你的域名，然后选择 "单一登录"。</span><span class="sxs-lookup"><span data-stu-id="09cd8-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![配置身份验证对话框](single-sign-on/_static/image24.png)

<span data-ttu-id="09cd8-205">还可以为应用程序提供目录数据的读取或读/写权限。</span><span class="sxs-lookup"><span data-stu-id="09cd8-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="09cd8-206">如果执行此操作，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)查找用户的电话号码，找出用户的电话号码、上次登录时间等。</span><span class="sxs-lookup"><span data-stu-id="09cd8-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="09cd8-207">这就是您需要做的一切-Visual Studio 要求提供 Azure AD 租户管理员的凭据，然后为新应用程序配置您的项目和 Azure AD 租户。</span><span class="sxs-lookup"><span data-stu-id="09cd8-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="09cd8-208">运行该项目时，你将看到一个登录页，你可以使用 Azure AD 目录中用户的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![组织帐户登录](single-sign-on/_static/image25.png)

![已登录](single-sign-on/_static/image26.png)

<span data-ttu-id="09cd8-211">将应用部署到 Azure 时，你只需选择 "**启用组织身份验证**" 复选框，再一次，Visual Studio 会立即处理所有配置。</span><span class="sxs-lookup"><span data-stu-id="09cd8-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![发布网站](single-sign-on/_static/image27.png)

<span data-ttu-id="09cd8-213">这些屏幕快照来自完整的分步教程，该教程演示如何生成使用 Azure AD 身份验证的应用程序：[使用 Azure Active Directory 开发 ASP.NET 应用](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)程序。</span><span class="sxs-lookup"><span data-stu-id="09cd8-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="09cd8-214">总结</span><span class="sxs-lookup"><span data-stu-id="09cd8-214">Summary</span></span>

<span data-ttu-id="09cd8-215">在本章中，你已了解到 Azure Active Directory、Visual Studio 和 ASP.NET，使你可以轻松地在组织的用户的 Internet 应用程序中设置单一登录。</span><span class="sxs-lookup"><span data-stu-id="09cd8-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="09cd8-216">用户可以使用在内部网络中使用 Active Directory 登录所用的相同凭据登录到 Internet 应用。</span><span class="sxs-lookup"><span data-stu-id="09cd8-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="09cd8-217">[下一章](data-storage-options.md)介绍适用于云应用程序的数据存储选项。</span><span class="sxs-lookup"><span data-stu-id="09cd8-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="09cd8-218">资源</span><span class="sxs-lookup"><span data-stu-id="09cd8-218">Resources</span></span>

<span data-ttu-id="09cd8-219">有关更多信息，请参见以下资源：</span><span class="sxs-lookup"><span data-stu-id="09cd8-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="09cd8-220">[Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="09cd8-221">Windowsazure.com 网站上 Azure AD 文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="09cd8-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="09cd8-222">有关分步教程，请参阅**开发**部分。</span><span class="sxs-lookup"><span data-stu-id="09cd8-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="09cd8-223">[Azure 多重身份验证](https://docs.microsoft.com/azure/multi-factor-authentication/)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="09cd8-224">有关 Azure 中多重身份验证的文档的门户页。</span><span class="sxs-lookup"><span data-stu-id="09cd8-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="09cd8-225">[组织帐户身份验证选项](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="09cd8-226">Visual Studio 2013 "新建项目" 对话框中 Azure AD 身份验证选项的说明。</span><span class="sxs-lookup"><span data-stu-id="09cd8-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="09cd8-227">[Microsoft 模式和实践-联合身份验证模式](https://msdn.microsoft.com/library/dn589790.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="09cd8-228">[如何：安装 Azure Active Directory 同步工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="09cd8-229">[Active Directory 联合身份验证服务2.0 内容映射](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="09cd8-230">有关 ADFS 2.0 的文档的链接。</span><span class="sxs-lookup"><span data-stu-id="09cd8-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="09cd8-231">[Windows Azure AD 应用程序中基于角色和基于 ACL 的授权](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="09cd8-232">示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="09cd8-232">Sample application.</span></span>
- <span data-ttu-id="09cd8-233">[Azure Active Directory 图形 API 博客](https://blogs.msdn.com/b/aadgraphteam/)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="09cd8-234">[混合标识基础结构中 BYOD 和目录集成中的访问控制](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。</span><span class="sxs-lookup"><span data-stu-id="09cd8-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="09cd8-235">Tech Ed 2014 讲座视频，通过 Gayana Bagdasaryan。</span><span class="sxs-lookup"><span data-stu-id="09cd8-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="09cd8-236">[上一页](web-development-best-practices.md)
> [下一页](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="09cd8-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
