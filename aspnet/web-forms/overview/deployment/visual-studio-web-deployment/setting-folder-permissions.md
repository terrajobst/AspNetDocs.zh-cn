---
uid: web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
title: 使用 Visual Studio 的 ASP.NET Web 部署：设置文件夹权限 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9715a121-fa55-4f1b-a5d2-fb3f6cd8be8f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/setting-folder-permissions
msc.type: authoredcontent
ms.openlocfilehash: 410525bb2e3f6e5a0be6d7d6b33fb3a40509041a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465062"
---
# <a name="aspnet-web-deployment-using-visual-studio-setting-folder-permissions"></a><span data-ttu-id="c05fc-103">使用 Visual Studio 的 ASP.NET Web 部署：设置文件夹权限</span><span class="sxs-lookup"><span data-stu-id="c05fc-103">ASP.NET Web Deployment using Visual Studio: Setting Folder Permissions</span></span>

<span data-ttu-id="c05fc-104">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c05fc-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="c05fc-105">下载初学者项目</span><span class="sxs-lookup"><span data-stu-id="c05fc-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="c05fc-106">本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。</span><span class="sxs-lookup"><span data-stu-id="c05fc-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="c05fc-107">有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="c05fc-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="c05fc-108">概述</span><span class="sxs-lookup"><span data-stu-id="c05fc-108">Overview</span></span>

<span data-ttu-id="c05fc-109">在本教程中，您将设置已部署网站中的*Elmah*文件夹的文件夹权限，以便应用程序可以在该文件夹中创建日志文件。</span><span class="sxs-lookup"><span data-stu-id="c05fc-109">In this tutorial, you set folder permissions for the *Elmah* folder in the deployed web site so that the application can create log files in that folder.</span></span>

<span data-ttu-id="c05fc-110">使用 Visual Studio 开发服务器（Cassini）或 IIS Express 在 Visual Studio 中测试 web 应用程序时，应用程序将在您的标识下运行。</span><span class="sxs-lookup"><span data-stu-id="c05fc-110">When you test a web application in Visual Studio using the Visual Studio Development Server (Cassini) or IIS Express, the application runs under your identity.</span></span> <span data-ttu-id="c05fc-111">您很可能是开发计算机上的管理员，并且具有完全权限，可以对任何文件夹中的任何文件执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="c05fc-111">You are most likely an administrator on your development computer and have full authority to do anything to any file in any folder.</span></span> <span data-ttu-id="c05fc-112">但是，当应用程序在 IIS 下运行时，它将在为该站点分配到的应用程序池定义的标识下运行。</span><span class="sxs-lookup"><span data-stu-id="c05fc-112">But when an application runs under IIS, it runs under the identity defined for the application pool that the site is assigned to.</span></span> <span data-ttu-id="c05fc-113">这通常是一个具有有限权限的系统定义的帐户。</span><span class="sxs-lookup"><span data-stu-id="c05fc-113">This is typically a system-defined account that has limited permissions.</span></span> <span data-ttu-id="c05fc-114">默认情况下，它对 web 应用程序的文件和文件夹具有 "读取" 和 "执行" 权限，但它没有写入访问权限。</span><span class="sxs-lookup"><span data-stu-id="c05fc-114">By default it has read and execute permissions on your web application's files and folders, but it doesn't have write access.</span></span>

<span data-ttu-id="c05fc-115">如果你的应用程序创建或更新文件（这是 web 应用程序中的常见需求），这会成为一个问题。</span><span class="sxs-lookup"><span data-stu-id="c05fc-115">This becomes an issue if your application creates or updates files, which is a common need in web applications.</span></span> <span data-ttu-id="c05fc-116">在 Contoso 大学应用程序中，Elmah 在*elmah*文件夹中创建 XML 文件，以便保存有关错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c05fc-116">In the Contoso University application, Elmah creates XML files in the *Elmah* folder in order to save details about errors.</span></span> <span data-ttu-id="c05fc-117">即使你不使用类似于 Elmah 的内容，你的网站也可能允许用户上传文件或执行其他将数据写入你站点中的文件夹的任务。</span><span class="sxs-lookup"><span data-stu-id="c05fc-117">Even if you don't use something like Elmah, your site might let users upload files or perform other tasks that write data to a folder in your site.</span></span>

<span data-ttu-id="c05fc-118">提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="c05fc-118">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="test-error-logging-and-reporting"></a><span data-ttu-id="c05fc-119">测试错误日志记录和报告</span><span class="sxs-lookup"><span data-stu-id="c05fc-119">Test error logging and reporting</span></span>

<span data-ttu-id="c05fc-120">若要查看应用程序在 IIS 中不能正常运行的方式（尽管在 Visual Studio 中对其进行测试时也是如此），则可能导致由 Elmah 记录的错误，并打开 Elmah 错误日志以查看详细信息。</span><span class="sxs-lookup"><span data-stu-id="c05fc-120">To see how the application doesn't work correctly in IIS (although it did when you tested it in Visual Studio), you can cause an error that would normally be logged by Elmah, and then open the Elmah error log to see the details.</span></span> <span data-ttu-id="c05fc-121">如果 Elmah 无法创建 XML 文件并存储错误详细信息，则会看到一个空错误报告。</span><span class="sxs-lookup"><span data-stu-id="c05fc-121">If Elmah was unable to create an XML file and store the error details, you see an empty error report.</span></span>

<span data-ttu-id="c05fc-122">打开浏览器并中转到 `http://localhost/ContosoUniversity`，然后请求无效的 URL，如*Studentsxxx*。</span><span class="sxs-lookup"><span data-stu-id="c05fc-122">Open a browser and go to `http://localhost/ContosoUniversity`, and then request an invalid URL like *Studentsxxx.aspx*.</span></span> <span data-ttu-id="c05fc-123">由于 Web.config 文件中的 `customErrors` 设置为 "RemoteOnly"，并且在本地运行 IIS，因此会看到系统生成的错误页，而不是*GenericErrorPage*页：</span><span class="sxs-lookup"><span data-stu-id="c05fc-123">You see a system-generated error page instead of the *GenericErrorPage.aspx* page because the `customErrors` setting in the Web.config file is "RemoteOnly" and you are running IIS locally:</span></span>

![HTTP 404 错误页](setting-folder-permissions/_static/image1.png)

<span data-ttu-id="c05fc-125">现在，请运行*Elmah*以查看错误报告。</span><span class="sxs-lookup"><span data-stu-id="c05fc-125">Now run *Elmah.axd* to see the error report.</span></span> <span data-ttu-id="c05fc-126">使用管理员帐户凭据（&quot;管理员&quot; 和 &quot;devpwd&quot;）登录后，将看到一个空错误日志页面，因为 Elmah 无法在*elmah*文件夹中创建 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="c05fc-126">After you log in with the administrator account credentials (&quot;admin&quot; and &quot;devpwd&quot;), you see an empty error log page because Elmah was unable to create an XML file in the *Elmah* folder:</span></span>

![错误日志为空](setting-folder-permissions/_static/image2.png)

## <a name="set-write-permission-on-the-elmah-folder"></a><span data-ttu-id="c05fc-128">对 Elmah 文件夹设置写入权限</span><span class="sxs-lookup"><span data-stu-id="c05fc-128">Set write permission on the Elmah folder</span></span>

<span data-ttu-id="c05fc-129">您可以手动设置文件夹权限，也可以将其设置为部署过程的自动部分。</span><span class="sxs-lookup"><span data-stu-id="c05fc-129">You can set folder permissions manually or you can make it an automatic part of the deployment process.</span></span> <span data-ttu-id="c05fc-130">将其设置为自动需要复杂的 MSBuild 代码，因此，在首次部署时只需执行此操作，请执行以下步骤以手动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="c05fc-130">Making it automatic requires complex MSBuild code, and since you only have to do this the first time you deploy, the following steps how to do it manually.</span></span> <span data-ttu-id="c05fc-131">（有关如何创建此部分部署过程的信息，请参阅在 Sayed Hashimi 的博客上[设置对 Web 发布的文件夹权限](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)。）</span><span class="sxs-lookup"><span data-stu-id="c05fc-131">(For information about how to make this part of the deployment process, see [Setting Folder Permissions on Web Publish](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) on Sayed Hashimi's blog.)</span></span>

1. <span data-ttu-id="c05fc-132">在**文件资源管理器**中，导航到*C:\inetpub\wwwroot\ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="c05fc-132">In **File Explorer**, navigate to *C:\inetpub\wwwroot\ContosoUniversity*.</span></span> <span data-ttu-id="c05fc-133">右键单击 " *Elmah* " 文件夹，选择 "**属性**"，然后选择 "**安全**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="c05fc-133">Right-click the *Elmah* folder, select **Properties**, and then select the **Security** tab.</span></span>
2. <span data-ttu-id="c05fc-134">单击“编辑”。</span><span class="sxs-lookup"><span data-stu-id="c05fc-134">Click **Edit**.</span></span>
3. <span data-ttu-id="c05fc-135">在 " **Elmah 的权限**" 对话框中，选择 " **DefaultAppPool**"，然后选中 "**允许**" 列中的 "**写入**" 复选框。</span><span class="sxs-lookup"><span data-stu-id="c05fc-135">In the **Permissions for Elmah** dialog box, select **DefaultAppPool**, and then select the **Write** check box in the **Allow** column.</span></span>

    ![ELMAH 文件夹的权限](setting-folder-permissions/_static/image3.png)

    <span data-ttu-id="c05fc-137">（如果在 "**组或用户名**" 列表中看不到 " **DefaultAppPool** "，则可能使用了一些其他方法，而不是本教程中指定的方法在计算机上设置 IIS 和 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="c05fc-137">(If you don't see **DefaultAppPool** in the **Group or user names** list, you probably used some other method than the one specified in this tutorial to set up IIS and ASP.NET 4 on your computer.</span></span> <span data-ttu-id="c05fc-138">在这种情况下，请查看分配给 Contoso 大学应用程序的应用程序池使用的标识，并向该标识授予写入权限。</span><span class="sxs-lookup"><span data-stu-id="c05fc-138">In that case, find out what identity is used by the application pool assigned to the Contoso University application, and grant write permission to that identity.</span></span> <span data-ttu-id="c05fc-139">请参阅本教程末尾的链接 "关于应用程序池标识"。在两个对话框中单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="c05fc-139">See the links about application pool identities at the end of this tutorial.) Click **OK** in both dialog boxes.</span></span>

## <a name="retest-error-logging-and-reporting"></a><span data-ttu-id="c05fc-140">重新测试错误日志记录和报告</span><span class="sxs-lookup"><span data-stu-id="c05fc-140">Retest error logging and reporting</span></span>

<span data-ttu-id="c05fc-141">通过相同方式（请求错误的 URL）再次导致错误的测试，并运行 "**错误日志**" 页。</span><span class="sxs-lookup"><span data-stu-id="c05fc-141">Test by causing an error again in the same way (request a bad URL) and run the **Error Log** page.</span></span> <span data-ttu-id="c05fc-142">这次，此错误将显示在该页上。</span><span class="sxs-lookup"><span data-stu-id="c05fc-142">This time the error appears on the page.</span></span>

![ELMAH 错误日志页](setting-folder-permissions/_static/image4.png)

## <a name="summary"></a><span data-ttu-id="c05fc-144">摘要</span><span class="sxs-lookup"><span data-stu-id="c05fc-144">Summary</span></span>

<span data-ttu-id="c05fc-145">你现在已经完成了在本地计算机上的 IIS 中正常工作所需的所有任务。</span><span class="sxs-lookup"><span data-stu-id="c05fc-145">You have now completed all of the tasks necessary to get Contoso University working correctly in IIS on your local computer.</span></span> <span data-ttu-id="c05fc-146">在下一教程中，你将通过将网站部署到 Azure 使其公开发布。</span><span class="sxs-lookup"><span data-stu-id="c05fc-146">In the next tutorial, you will make the site publicly available by deploying it to Azure.</span></span>

## <a name="more-information"></a><span data-ttu-id="c05fc-147">详细信息</span><span class="sxs-lookup"><span data-stu-id="c05fc-147">More information</span></span>

<span data-ttu-id="c05fc-148">在此示例中，Elmah 无法保存日志文件的原因相当明显。</span><span class="sxs-lookup"><span data-stu-id="c05fc-148">In this example, the reason why Elmah was unable to save log files was fairly obvious.</span></span> <span data-ttu-id="c05fc-149">在出现问题的原因不太明显的情况下，可以使用 IIS 跟踪;请参阅 IIS.net 站点上的[使用 IIS 7 中的跟踪对失败请求进行故障排除](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)。</span><span class="sxs-lookup"><span data-stu-id="c05fc-149">You can use IIS tracing in cases where the cause of the problem is not so obvious; see [Troubleshooting Failed Requests Using Tracing in IIS 7](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis) on the IIS.net site.</span></span>

<span data-ttu-id="c05fc-150">有关如何向应用程序池标识授予权限的详细信息，请参阅 IIS.net 站点上的[文件系统 acl 中](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)的[应用程序池标识](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)和 IIS 中的安全内容。</span><span class="sxs-lookup"><span data-stu-id="c05fc-150">For more information about how to grant permissions to application pool identities, see [Application Pool Identities](https://www.iis.net/learn/manage/configuring-security/application-pool-identities) and [Secure Content in IIS Through File System ACLs](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls) on the IIS.net site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c05fc-151">[上一页](deploying-to-iis.md)
> [下一页](deploying-to-production.md)</span><span class="sxs-lookup"><span data-stu-id="c05fc-151">[Previous](deploying-to-iis.md)
[Next](deploying-to-production.md)</span></span>
