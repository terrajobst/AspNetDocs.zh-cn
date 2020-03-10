---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005 中的改进 |Microsoft Docs
author: microsoft
description: Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464648"
---
# <a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="9e09e-103">Visual Studio 2005 中的改进</span><span class="sxs-lookup"><span data-stu-id="9e09e-103">Improvements in Visual Studio 2005</span></span>

<span data-ttu-id="9e09e-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="9e09e-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="9e09e-105">Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>

<span data-ttu-id="9e09e-106">Visual Studio 2005 为 Web 应用程序开发人员提供了对 Web 项目的改进和增强功能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="9e09e-107">与 Visual Studio .NET 2002 和2003一样强大，处理 Web 项目的方式有很多投诉。</span><span class="sxs-lookup"><span data-stu-id="9e09e-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="9e09e-108">Visual Studio 2005 添加了大量新功能，以解决这些投诉。</span><span class="sxs-lookup"><span data-stu-id="9e09e-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="9e09e-109">对于更喜欢 Visual Studio .NET 2003 处理 Web 应用程序的编译方式的用户，请参阅[Web 应用程序项目](https://go.microsoft.com/fwlink/?LinkId=57870)。</span><span class="sxs-lookup"><span data-stu-id="9e09e-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="9e09e-110">在此模块中，我们在 Web 项目的创建、管理和开发方面做了改进。</span><span class="sxs-lookup"><span data-stu-id="9e09e-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="9e09e-111">在更高版本的模块中，在生成 Web 项目和部署它们方面做了改进。</span><span class="sxs-lookup"><span data-stu-id="9e09e-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="9e09e-112">FrontPage 服务器扩展</span><span class="sxs-lookup"><span data-stu-id="9e09e-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="9e09e-113">需要在框中 FrontPage 服务器扩展 Visual Studio .NET 2002 和2003，才能创建或生成 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="9e09e-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="9e09e-114">开发人员可在两种不同的访问模式（FrontPage 服务器扩展或文件访问模式）之间进行选择，这两种模式都 FrontPage 服务器扩展来执行任务，例如在 IIS 中设置应用程序根目录等。</span><span class="sxs-lookup"><span data-stu-id="9e09e-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="9e09e-115">Visual Studio 2005 消除了对本地项目 FrontPage 服务器扩展的依赖。</span><span class="sxs-lookup"><span data-stu-id="9e09e-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="9e09e-116">Visual Studio 2005 现在直接访问 IIS 元数据库，而不是使用 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="9e09e-117">Visual Studio 2005 还添加了对允许远程项目访问的 FTP 支持，而无需 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="9e09e-118">对于想要在项目中使用 FrontPage 服务器扩展的开发人员，此选项仍然可用。</span><span class="sxs-lookup"><span data-stu-id="9e09e-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="9e09e-119">但是，根据 ASP.NET 开发人员社区提供的强大反馈，这并不是必需的。</span><span class="sxs-lookup"><span data-stu-id="9e09e-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-120">远程项目创建、打开等仍需要 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="9e09e-121">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="9e09e-121">ASP.NET Development Server</span></span>

<span data-ttu-id="9e09e-122">Visual Studio 2005 附带了一个名为 ASP.NET 开发服务器的新 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="9e09e-123">（此 Web 服务器以前称为 Cassini。）</span><span class="sxs-lookup"><span data-stu-id="9e09e-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="9e09e-124">ASP.NET 开发服务器有多个优点。</span><span class="sxs-lookup"><span data-stu-id="9e09e-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="9e09e-125">非管理员现在可以针对 Web 服务器进行开发和调试。</span><span class="sxs-lookup"><span data-stu-id="9e09e-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="9e09e-126">ASP.NET 开发服务器将虚拟目录动态映射到文件系统中的任何位置，以实现灵活的项目位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="9e09e-127">Windows XP Professional 上已经使用 IIS 的用户现在可以创建新的 Web 应用程序，这些应用程序不会影响其在 IIS 中默认网站的文件或文件夹结构。</span><span class="sxs-lookup"><span data-stu-id="9e09e-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="9e09e-128">无需特殊配置即可利用 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="9e09e-129">当调试或浏览文件系统上承载的 Web 项目时，Visual Studio 2005 将自动启动随机端口上的 ASP.NET 开发服务器实例以处理请求。</span><span class="sxs-lookup"><span data-stu-id="9e09e-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="9e09e-130">详细信息将在本模块后面的 ASP.NET 开发服务器中介绍。</span><span class="sxs-lookup"><span data-stu-id="9e09e-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="9e09e-131">改进的文件管理</span><span class="sxs-lookup"><span data-stu-id="9e09e-131">Improved File Management</span></span>

<span data-ttu-id="9e09e-132">在 Visual Studio 2002 和2003中，为 Web 应用程序中的所有文件存储了一个C#项目文件（.vbproj for VB.NET 和 .csproj）。</span><span class="sxs-lookup"><span data-stu-id="9e09e-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="9e09e-133">解决方案资源管理器显示基于项目文件中的文件信息。</span><span class="sxs-lookup"><span data-stu-id="9e09e-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="9e09e-134">因此，在使用外部编辑器的情况下，解决方案资源管理器通常会显示不正确的信息。</span><span class="sxs-lookup"><span data-stu-id="9e09e-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="9e09e-135">Visual Studio 2002 和2003经常会覆盖文件更改或不显示最新版本的文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="9e09e-136">Visual Studio 2005 与项目文件不相同。</span><span class="sxs-lookup"><span data-stu-id="9e09e-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="9e09e-137">相反，它直接读取磁盘中的文件和文件夹信息，使项目中的文件显示准确。</span><span class="sxs-lookup"><span data-stu-id="9e09e-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="9e09e-138">由于 Visual Studio 2002 和2003中的 "引用" 文件夹并不表示你的 Web 应用程序中的实际文件夹，因此 Visual Studio 2005 还会删除解决方案资源管理器中的 "引用" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="9e09e-139">若要在 Visual Studio 2005 中访问你的项目的引用，你应使用项目的属性页。</span><span class="sxs-lookup"><span data-stu-id="9e09e-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="9e09e-140">创建 Web 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-140">Creating Web Projects</span></span>

<span data-ttu-id="9e09e-141">Web 开发人员在 Visual Studio 2005 中提供了许多可用于创建项目的新选项。</span><span class="sxs-lookup"><span data-stu-id="9e09e-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="9e09e-142">网站现在可以在文件系统中的任何位置创建，然后可以使用新 ASP.NET 开发服务器进行调试或浏览。</span><span class="sxs-lookup"><span data-stu-id="9e09e-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="9e09e-143">开发人员还可以使用 FTP 创建新网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="9e09e-144">单击此处查看在 Visual Studio 2005 中创建 Web 项目的视频演练。</span><span class="sxs-lookup"><span data-stu-id="9e09e-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image1.png)

[<span data-ttu-id="9e09e-145">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="9e09e-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a><span data-ttu-id="9e09e-146">文件系统项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-146">File System Projects</span></span>

<span data-ttu-id="9e09e-147">如视频演练中所示，可以选择在本地计算机上或通过文件共享在远程位置的文件系统上创建网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="9e09e-148">使用 ASP.NET 开发服务器浏览和调试在文件系统上创建的网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-149">ASP.NET 开发服务器可能会对客户造成一些混淆。</span><span class="sxs-lookup"><span data-stu-id="9e09e-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="9e09e-150">如果在文件系统上的 IISs 目录结构（即 c：/inetpub/wwwroot）中创建 Web 项目，则在 Visual Studio 2005 中启动该网站时，该网站仍会通过 ASP.NET 开发服务器浏览。</span><span class="sxs-lookup"><span data-stu-id="9e09e-150">If a Web project is created on the file system in IISs directory structure (i.e. c:/inetpub/wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="9e09e-151">因此，任何 IIS 配置（即身份验证方法）都不适用。</span><span class="sxs-lookup"><span data-stu-id="9e09e-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>

<span data-ttu-id="9e09e-152">默认 web 项目还会通过仅包括 default.aspx page、default.cs 文件和 App/_Data 文件夹来消除大量开销。</span><span class="sxs-lookup"><span data-stu-id="9e09e-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App/_Data folder.</span></span> <span data-ttu-id="9e09e-153">在需要时添加 web.config 和特殊文件夹（即 app/_code）。</span><span class="sxs-lookup"><span data-stu-id="9e09e-153">The web.config and special folders (i.e. app/_code) are added as they are needed.</span></span> <span data-ttu-id="9e09e-154">你的 web 项目仅包含所需的文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="9e09e-155">HTTP 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-155">HTTP Projects</span></span>

<span data-ttu-id="9e09e-156">HTTP 项目可以是在本地 IIS 网站或远程网站上创建的项目。</span><span class="sxs-lookup"><span data-stu-id="9e09e-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="9e09e-157">默认项目位置为 `http://localhost`。</span><span class="sxs-lookup"><span data-stu-id="9e09e-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="9e09e-158">如果单击 "浏览" 按钮，则有两个 HTTP 选项： "本地 IIS" 和 "远程站点"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="9e09e-159">这两个选项的主要区别是在 "选择位置" 对话框和文件复制到 Web 服务器的方式中显示网站信息的方法。</span><span class="sxs-lookup"><span data-stu-id="9e09e-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="9e09e-160">本地 IIS 选项读取本地计算机上的元数据库中的站点信息，并使用文件系统复制文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="9e09e-161">远程站点选项使用 FrontPage 服务器扩展，并使用 HTTP 和 FrontPage 服务器扩展 RPC 调用复制站点信息和文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-162">不会再使用 vs # # #/_tmp .htm 文件和 get/_aspx/_ver 来确定版本信息。</span><span class="sxs-lookup"><span data-stu-id="9e09e-162">The vs###/_tmp.htm file and get/_aspx/_ver.aspx are no longer used to determine version information.</span></span>

<span data-ttu-id="9e09e-163">默认的 HTTP 选项为 "本地 IIS"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="9e09e-164">此选项将读取 IIS 元数据库，以确定哪些网站可用以及要在其中创建内容的位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="9e09e-165">通过在树视图中选择其他文件夹或虚拟目录，可以选择该文件夹或虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="9e09e-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="9e09e-166">你还可以创建一个新的虚拟目录，将文件夹标记为应用程序，以及从此对话框中删除现有虚拟目录。</span><span class="sxs-lookup"><span data-stu-id="9e09e-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>

!["选择位置" 对话框](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="9e09e-168">**图 1**： "选择位置" 对话框</span><span class="sxs-lookup"><span data-stu-id="9e09e-168">**Figure 1**: The Choose Location Dialog</span></span>

<span data-ttu-id="9e09e-169">与 Visual Studio 的早期版本不同，如果选中 "**使用安全套接字层**" 复选框，SSL 证书与要浏览的 URL 不匹配，则会显示一个安全警报对话框，询问你是否要继续。</span><span class="sxs-lookup"><span data-stu-id="9e09e-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="9e09e-170">使用 Visual Studio .NET 2003，如果证书不是匹配的证书，则创建项目将失败。</span><span class="sxs-lookup"><span data-stu-id="9e09e-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>

![与 SSL 证书有关的安全警报](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="9e09e-172">**图 2**：与 SSL 证书有关的安全警报</span><span class="sxs-lookup"><span data-stu-id="9e09e-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>

### <a name="note-on-host-headers"></a><span data-ttu-id="9e09e-173">主机标头上的说明</span><span class="sxs-lookup"><span data-stu-id="9e09e-173">Note on Host Headers</span></span>

<span data-ttu-id="9e09e-174">如果要在绑定到特定 IP 的站点上创建 Web 应用程序，则需要确保配置了主机标头。</span><span class="sxs-lookup"><span data-stu-id="9e09e-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="9e09e-175">否则，Visual Studio 将在 `http://localhost`创建网站，但在从 IDE 中浏览或调试该站点时，该 IP 地址将无法正确解析。</span><span class="sxs-lookup"><span data-stu-id="9e09e-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="9e09e-176">如果选择 "远程站点" 选项，则对话框将更改为允许您输入新网站的目标 URL。</span><span class="sxs-lookup"><span data-stu-id="9e09e-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="9e09e-177">此 URL 必须位于启用了 FrontPage 服务器扩展的服务器上。</span><span class="sxs-lookup"><span data-stu-id="9e09e-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="9e09e-178">如果要使用 FrontPage 服务器扩展使用本地 Web 服务器，可以使用 "远程站点" 选项并指定本地 URL。</span><span class="sxs-lookup"><span data-stu-id="9e09e-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>

![在远程服务器上创建网站](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="9e09e-180">**图 3**：在远程服务器上创建网站</span><span class="sxs-lookup"><span data-stu-id="9e09e-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>

<span data-ttu-id="9e09e-181">通过 SSL 在远程站点上创建应用程序时，如果 SSL 证书不匹配，确认对话框与使用本地 IIS 选项时显示的对话框略有不同。</span><span class="sxs-lookup"><span data-stu-id="9e09e-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>

![远程站点安全警报](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="9e09e-183">**图 4**：远程站点安全警报</span><span class="sxs-lookup"><span data-stu-id="9e09e-183">**Figure 4**: The Remote Site Security Alert</span></span>

<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="9e09e-184">FTP</span><span class="sxs-lookup"><span data-stu-id="9e09e-184">FTP</span></span>

<span data-ttu-id="9e09e-185">Visual Studio 2005 引入了通过 FTP 创建网站的选项。</span><span class="sxs-lookup"><span data-stu-id="9e09e-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="9e09e-186">使用此选项时，IDE 将在本地用户临时文件夹中创建文件，然后使用 FTP 将文件移动到 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-187">临时文件夹位置为 "c：/文档和设置/&lt;用户&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="9e09e-187">The temp folder location is c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="9e09e-188">使用 FTP 选项时，将显示 "选择位置" 对话框。</span><span class="sxs-lookup"><span data-stu-id="9e09e-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="9e09e-189">按如下所示，在此对话框中输入所需的 FTP 连接信息。</span><span class="sxs-lookup"><span data-stu-id="9e09e-189">You enter the required FTP connection information into this dialog as shown below.</span></span>

![FTP 的 "选择位置" 对话框](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="9e09e-191">**图 5**： FTP 的 "选择位置" 对话框</span><span class="sxs-lookup"><span data-stu-id="9e09e-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>

## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="9e09e-192">Lab：设置 FTP 站点和创建项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="9e09e-193">以下步骤将配置 FTP 站点，使用户拥有一个只能通过 FTP 上传到的位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="9e09e-194">安装 FTP 服务</span><span class="sxs-lookup"><span data-stu-id="9e09e-194">Install the FTP Service</span></span>

1. <span data-ttu-id="9e09e-195">打开 "添加/删除程序"，选择 "添加/删除 Windows 组件"</span><span class="sxs-lookup"><span data-stu-id="9e09e-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="9e09e-196">选择 Internet Information Services （Windows 2003 上的应用程序服务器）并单击 "**详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="9e09e-197">检查**文件传输协议（FTP）服务**，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="9e09e-198">单击 "**下一步**" 以安装 FTP 服务。</span><span class="sxs-lookup"><span data-stu-id="9e09e-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="9e09e-199">为内容创建新文件夹</span><span class="sxs-lookup"><span data-stu-id="9e09e-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="9e09e-200">在 Windows 资源管理器中，在 c：/inetpub/wwwroot 内创建名为**User1**的新文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-200">In Windows Explorer, create a new folder called **User1** inside of c:/inetpub/wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="9e09e-201">配置文件夹和文件夹的权限。</span><span class="sxs-lookup"><span data-stu-id="9e09e-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="9e09e-202">从 "管理工具" 打开 Internet Information Services 管理单元。</span><span class="sxs-lookup"><span data-stu-id="9e09e-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="9e09e-203">你现在会在 "计算机名" 节点下有一个 "FTP 站点" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="9e09e-204">展开 " **FTP 站点**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="9e09e-205">右键单击**默认 FTP 站点**，依次选择 "**新建**" 和 "**虚拟目录**"，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="9e09e-206">输入**User1**作为虚拟目录名称，并单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="9e09e-207">为路径输入**c：/inetpub/wwwroot/User1** ，然后单击 "**下一步**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-207">Enter **c:/inetpub/wwwroot/User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="9e09e-208">单击 "**下一步**"，然后单击 "**完成**" 完成向导。</span><span class="sxs-lookup"><span data-stu-id="9e09e-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="9e09e-209">右键单击 "默认 FTP 站点" 下的**User1**虚拟目录，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="9e09e-210">选中 "**写入**" 复选框，并单击 **"确定"** 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9e09e-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="9e09e-211">右键单击 "**默认 FTP 站点**"，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="9e09e-212">在 "**安全帐户**" 选项卡上，取消选中 "**允许匿名连接**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="9e09e-213">询问是否要继续，请单击对话框中的 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="9e09e-214">单击 **“确定”** ，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9e09e-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="9e09e-215">展开 **"网站" 节点下**的 "**默认**网站"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="9e09e-216">右键单击**User1**目录，然后选择 "**属性**"</span><span class="sxs-lookup"><span data-stu-id="9e09e-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="9e09e-217">在 "**应用程序设置**" 部分中，单击 "**创建**" 将文件夹标记为应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="9e09e-218">单击 **“确定”** ，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="9e09e-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="9e09e-219">关闭 "Internet Information Services" 管理单元。</span><span class="sxs-lookup"><span data-stu-id="9e09e-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="9e09e-220">创建 web 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-220">Create web project</span></span>

1. <span data-ttu-id="9e09e-221">打开 Visual Studio 2005。</span><span class="sxs-lookup"><span data-stu-id="9e09e-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="9e09e-222">从 "**文件**" 菜单中选择 "**新建**网站"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="9e09e-223">在 "**位置**" 下拉列表中，选择 " **FTP**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="9e09e-224">单击“浏览”。</span><span class="sxs-lookup"><span data-stu-id="9e09e-224">Click **Browse**.</span></span>
5. <span data-ttu-id="9e09e-225">在 "**服务器**" 文本框中输入**localhost** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="9e09e-226">在 "目录" 文本框中输入**User1** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="9e09e-227">单击“打开”。</span><span class="sxs-lookup"><span data-stu-id="9e09e-227">Click **Open**.</span></span> <span data-ttu-id="9e09e-228">将在 "新建网站" 对话框中输入 FTP 位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="9e09e-229">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="9e09e-229">Click **OK**.</span></span>
9. <span data-ttu-id="9e09e-230">在 "FTP 登录" 对话框中取消选中 "**匿名登录**"，输入你的凭据，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="9e09e-231">项目的 URL 是什么？</span><span class="sxs-lookup"><span data-stu-id="9e09e-231">What is the URL for the project?</span></span> <span data-ttu-id="9e09e-232">（项目的 URL 将显示在解决方案资源管理器中。）</span><span class="sxs-lookup"><span data-stu-id="9e09e-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="9e09e-233">在 "**生成**" 菜单中，选择 "**构建网站**" 或 "**生成解决方案**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="9e09e-234">在解决方案资源管理器中右键单击 "default.aspx"，然后选择 "**在浏览器中查看**"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="9e09e-235">在 "要求提供网站 URL" 对话框中，输入 URL 的 `http://localhost/user1`，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-236">如果收到一个错误，指示无法加载类型/_Default，请确保在您的网站上运行 ASP.NET 2.0，而不是较早的版本。</span><span class="sxs-lookup"><span data-stu-id="9e09e-236">If you get a error indicating an inability to load the type /_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="9e09e-237">可以在 Internet Information Services 的 "ASP.NET" 选项卡中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="9e09e-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>

## <a name="opening-web-projects"></a><span data-ttu-id="9e09e-238">打开 Web 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-238">Opening Web Projects</span></span>

<span data-ttu-id="9e09e-239">打开 Web 项目类似于创建项目。</span><span class="sxs-lookup"><span data-stu-id="9e09e-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="9e09e-240">以下各部分将介绍在 IDE 中工作时要保持引人注目的区域。</span><span class="sxs-lookup"><span data-stu-id="9e09e-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="9e09e-241">还介绍了如何使用 HTTP 和 FTP 来处理 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="9e09e-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="9e09e-242">若要打开 Web 项目，请从 "文件" 菜单中选择 "打开网站"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="9e09e-243">系统将提示您前面介绍的 "选择位置" 对话框，您可以使用相同的四个选项： "文件系统"、"本地 IIS"、"FTP" 和 "远程站点"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="9e09e-244">文件系统</span><span class="sxs-lookup"><span data-stu-id="9e09e-244">File System</span></span>

<span data-ttu-id="9e09e-245">如前文所述，Visual Studio 不再使用项目文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="9e09e-246">因此，如果您选择从文件系统打开网站，则实际上可以选择所需的任何文件夹，即使您选择的文件夹不是最初在 Visual Studio 中创建的 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="9e09e-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="9e09e-247">例如，你可以选择将 "我的文档" 文件夹作为网站打开，Visual Studio 会将其打开并显示你的文件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e09e-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>

![作为网站打开的文档](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="9e09e-249">**图 6**：作为网站打开的*文档*</span><span class="sxs-lookup"><span data-stu-id="9e09e-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>

<span data-ttu-id="9e09e-250">由于 Visual Studio 仅在必要时才会创建其他文件和文件夹，因此，不会将其他文件或文件夹添加到打开的位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="9e09e-251">此体系结构的副作用是它阻止你将网站嵌套在文件系统上。</span><span class="sxs-lookup"><span data-stu-id="9e09e-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="9e09e-252">例如，请考虑以下目录结构。</span><span class="sxs-lookup"><span data-stu-id="9e09e-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="9e09e-253">C：/MyWebSite Web 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-253">Web project at C:/MyWebSite</span></span>

<span data-ttu-id="9e09e-254">C：/MyWebSite/嵌套的另一个 web 项目</span><span class="sxs-lookup"><span data-stu-id="9e09e-254">Another web project at C:/MyWebSite/Nested</span></span>

<span data-ttu-id="9e09e-255">当你在 c：/MyWebSite 打开网站时，嵌套文件夹将显示为该应用程序的子文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-255">When you open the Web site at c:/MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="9e09e-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="9e09e-256">HTTP</span></span>

<span data-ttu-id="9e09e-257">通过 HTTP 打开网站时，将从 IIS 元数据库（本地 IIS）或使用 FrontPage 服务器扩展（远程站点）读取设置。如果有嵌套的 web 应用程序，则这些应用程序也会显示为应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="9e09e-258">如果你熟悉如何在 FrontPage 中使用 web 应用程序，则 Visual Studio 2005 中的行为是类似的。</span><span class="sxs-lookup"><span data-stu-id="9e09e-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="9e09e-259">即使对于嵌套在 IDE 中当前打开的应用程序下的应用程序，Visual Studio 也会显示一个图标，但不允许您展开这些应用程序来查看其内容。</span><span class="sxs-lookup"><span data-stu-id="9e09e-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="9e09e-260">不过，您可以双击它们以打开它们。</span><span class="sxs-lookup"><span data-stu-id="9e09e-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="9e09e-261">当你执行此操作时，会显示一个对话框，提示你打开 web 应用程序（并替换当前打开的解决方案），或者将 Web 应用程序添加到当前解决方案。</span><span class="sxs-lookup"><span data-stu-id="9e09e-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>

![双击嵌套应用程序图标会显示此对话框](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="9e09e-263">**图 7**：双击嵌套应用程序图标会显示此对话框</span><span class="sxs-lookup"><span data-stu-id="9e09e-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="9e09e-264">FTP 站点</span><span class="sxs-lookup"><span data-stu-id="9e09e-264">FTP Site</span></span>

<span data-ttu-id="9e09e-265">通过 FTP 打开站点时，所有文件都将以本地方式复制到 temp 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="9e09e-266">本地存储位置的完整路径会显示在项目的 "属性" 窗格中，并使用以下格式创建。</span><span class="sxs-lookup"><span data-stu-id="9e09e-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="9e09e-267">C：/Documents and Settings/&lt;用户&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;应用程序名称&gt;</span><span class="sxs-lookup"><span data-stu-id="9e09e-267">C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;application name&gt;</span></span>

<span data-ttu-id="9e09e-268">使用 FTP 时，Visual Studio 将需要为你的项目指定基 URL，以便你可以浏览该 URL，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e09e-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="9e09e-269">如果未指定基 URL，则 Visual Studio 将在您第一次尝试浏览网站中的页面时向您询问。</span><span class="sxs-lookup"><span data-stu-id="9e09e-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>

![指定 FTP 站点的基 URL](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="9e09e-271">**图 8**：指定 FTP 站点的基 URL</span><span class="sxs-lookup"><span data-stu-id="9e09e-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>

## <a name="improvements-in-compilation"></a><span data-ttu-id="9e09e-272">编译中的改进</span><span class="sxs-lookup"><span data-stu-id="9e09e-272">Improvements in Compilation</span></span>

<span data-ttu-id="9e09e-273">在 Visual Studio 2005 中使用 Web 应用程序比以前的版本更快。</span><span class="sxs-lookup"><span data-stu-id="9e09e-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="9e09e-274">这是由于编译体系结构中的更改所致。</span><span class="sxs-lookup"><span data-stu-id="9e09e-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="9e09e-275">在 Visual Studio 2002 和2003中，Web 应用程序编译到一个主程序集中，该程序集驻留在/bin 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="9e09e-276">在 Visual Studio 2005 中，添加了应用/_Code 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-276">In Visual Studio 2005, an App/_Code folder was added.</span></span> <span data-ttu-id="9e09e-277">类和其他非 UI 代码添加到 App/_Code 文件夹。</span><span class="sxs-lookup"><span data-stu-id="9e09e-277">Classes and other non-UI code are added to the App/_Code folder.</span></span> <span data-ttu-id="9e09e-278">当 Visual Studio 生成项目时，应用/_Code 文件夹中的所有文件都将编译为单个应用/_Code .dll 文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-278">When Visual Studio builds the project, all files in the App/_Code folder are compiled into a single App/_Code.dll file.</span></span> <span data-ttu-id="9e09e-279">此更改的结果是，后续版本比以前版本更快。</span><span class="sxs-lookup"><span data-stu-id="9e09e-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-280">MSBuild 命令行实用工具也可用于生成 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="9e09e-281">此工具将在模块9中介绍。</span><span class="sxs-lookup"><span data-stu-id="9e09e-281">That tool will be covered in module 9.</span></span>

<span data-ttu-id="9e09e-282">另一种编译增强功能是 "生成" 菜单上的 "新建生成页" 选项。</span><span class="sxs-lookup"><span data-stu-id="9e09e-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="9e09e-283">利用此功能，开发人员可以仅重新生成当前页面（同时，还可重新生成依赖项），以便可以更快地编译更改。</span><span class="sxs-lookup"><span data-stu-id="9e09e-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="9e09e-284">由于C#出于更新 intellisense 等目的而不提供后台编译，因此它们将从该功能中受益，因为它只是重新生成单个页面就可以快速更新 intellisense。</span><span class="sxs-lookup"><span data-stu-id="9e09e-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="9e09e-285">项目的生成属性允许您配置在执行启动页之前发生的生成类型。</span><span class="sxs-lookup"><span data-stu-id="9e09e-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="9e09e-286">开发人员可以选择仅生成当前页面，以便 Visual Studio 可以在代码更改后更快速地开始调试应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>

!["生成" 页启动操作](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="9e09e-288">**图 9**： "生成" 页的 "启动" 操作</span><span class="sxs-lookup"><span data-stu-id="9e09e-288">**Figure 9**: The Build Page Start Action</span></span>

<span data-ttu-id="9e09e-289">Visual Studio 和 ASP.NET 体系结构的另一个强大增强功能位于 "编辑并继续" 区域。</span><span class="sxs-lookup"><span data-stu-id="9e09e-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="9e09e-290">在 Visual Studio 2005 中，开发人员可以开始调试项目，并对项目进行代码更改而无需分离调试器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="9e09e-291">事实上，您可以通过任意方式开始调试项目、添加新类、向该类添加代码、将代码添加到创建该类的新实例并执行该类的方法的代码，所有这些都不需要分离调试器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="9e09e-292">执行新的代码就像刷新浏览器一样简单！</span><span class="sxs-lookup"><span data-stu-id="9e09e-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="9e09e-293">单击此处查看 Visual Studio 2005 中 "编辑并继续" 功能的视频演练。</span><span class="sxs-lookup"><span data-stu-id="9e09e-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>

![](improvements-in-visual-studio-2005/_static/image2.png)

[<span data-ttu-id="9e09e-294">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="9e09e-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

<span data-ttu-id="9e09e-295">ASP.NET 2.0 和 Visual Studio 2005 中的强大的 "编辑并继续" 功能是因为 ASP.NET 应用程序的体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="9e09e-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="9e09e-296">在 ASP.NET 1.x 中，在 Visual Studio 2002/2003 中创建的应用程序编译为存储在/bin 文件夹中的主程序集。</span><span class="sxs-lookup"><span data-stu-id="9e09e-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="9e09e-297">应用程序的所有类、页等都编译到了一个 DLL 中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="9e09e-298">然后，在运行时，ASP.NET 将编译页面内的所有控件、标记和 ASP.NET 代码，并将这些 Dll 复制到 ASP.NET 临时文件夹中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="9e09e-299">在 Visual Studio 2005 中，使用 ASP.NET 2.0，上面的两个编译模型大纲（一个用于 Visual Studio，另一个用于运行时的 ASP.NET）已合并到一个公共编译模型中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="9e09e-300">这意味着，在开发阶段（而不是运行时），所有编译问题都将被捕获。</span><span class="sxs-lookup"><span data-stu-id="9e09e-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="9e09e-301">它还允许对用户控件和母版页等功能进行设计和 IntelliSense 支持。</span><span class="sxs-lookup"><span data-stu-id="9e09e-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="9e09e-302">单击此处查看用户控件设计器支持的视频演练。</span><span class="sxs-lookup"><span data-stu-id="9e09e-302">Click here to see a video walkthrough of designer support for user controls.</span></span>

![](improvements-in-visual-studio-2005/_static/image3.png)

[<span data-ttu-id="9e09e-303">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="9e09e-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> <span data-ttu-id="9e09e-304">从页面中删除用户控件时，@Register 指令将保留在标记中，并且应手动删除，以避免在从网站中删除用户控件时出现分析器错误。</span><span class="sxs-lookup"><span data-stu-id="9e09e-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>

<span data-ttu-id="9e09e-305">Visual Studio 编译模型中的另一项改进是 "发布网站" 功能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="9e09e-306">由于发布功能对网站进行预编译，开发人员可享受到无需编译任何需求的附加性能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="9e09e-307">它还将应用/_Code 文件夹中的所有源代码预编译为 DLL，以便不需要部署任何源代码。</span><span class="sxs-lookup"><span data-stu-id="9e09e-307">It also precompiles all source code in the App/_Code folder into a DLL so that no source code has to be deployed.</span></span>

!["发布网站" 对话框](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="9e09e-309">**图 10**： "发布网站" 对话框</span><span class="sxs-lookup"><span data-stu-id="9e09e-309">**Figure 10**: The Publish Web Site Dialog</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-310">Aspnet/_compile .exe 实用程序还可以用于预编译 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-310">The aspnet/_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="9e09e-311">此工具将在模块9中介绍。</span><span class="sxs-lookup"><span data-stu-id="9e09e-311">That tool will be covered in module 9.</span></span>

<span data-ttu-id="9e09e-312">发布网站时，预编译文件存储在临时 ASP.NET Files 文件夹中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e09e-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="9e09e-313">具有*编译*文件扩展名的文件是为特定 dll 定义依赖项的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="9e09e-314">任何 Webform 或用户控件都编译为以*App/_Web/_* 开头的随机 dll。</span><span class="sxs-lookup"><span data-stu-id="9e09e-314">Any Webform or user controls are compiled into random DLLs that begin with *App/_Web/_*.</span></span>

<span data-ttu-id="9e09e-315">如果选中 "*允许更新此预编译站点以便进行更新*" 复选框，则 Webforms 和用户控件内的标记将不会预先编译为 DLL，使你可以在部署后进行更改。</span><span class="sxs-lookup"><span data-stu-id="9e09e-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="9e09e-316">如果你想要锁定标记，以便不允许对部署内容所做的更改，请取消选中此框。</span><span class="sxs-lookup"><span data-stu-id="9e09e-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="9e09e-317">"*使用固定命名和单页程序集*" 复选框允许您禁用批处理编译，以便将每个页编译为一个固定名称的程序集。</span><span class="sxs-lookup"><span data-stu-id="9e09e-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="9e09e-318">如果将此框保留为未选中状态，则可以利用批处理编译。</span><span class="sxs-lookup"><span data-stu-id="9e09e-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="9e09e-319">"对*预编译程序集启用强命名*" 复选框允许您对预编译的程序集进行强命名。</span><span class="sxs-lookup"><span data-stu-id="9e09e-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-320">在 ASP.NET 1.x 中，必须将具有强名称的程序集安装到全局程序集缓存（GAC）中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="9e09e-321">在 ASP.NET 2.0 中，无需将强名称程序集安装到 GAC 中。</span><span class="sxs-lookup"><span data-stu-id="9e09e-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>

![ASP.NET 应用程序预编译文件](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="9e09e-323">**图 11**： ASP.NET 应用程序预编译文件</span><span class="sxs-lookup"><span data-stu-id="9e09e-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-324">在上面的应用程序中，没有 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="9e09e-325">如果有，则在发布网站进程后，它将被称为*PrecompiledApp。*</span><span class="sxs-lookup"><span data-stu-id="9e09e-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>

## <a name="improvements-in-deployment"></a><span data-ttu-id="9e09e-326">部署中的改进</span><span class="sxs-lookup"><span data-stu-id="9e09e-326">Improvements in Deployment</span></span>

<span data-ttu-id="9e09e-327">与 Visual Studio 2002 和2003一样，Visual Studio 2005 还提供了一个复制项目功能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="9e09e-328">但是，该功能已在 Visual Studio 2005 中 beefed，现在称为 "复制网站"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="9e09e-329">"复制网站" 对话框拆分为左框架和右框架。</span><span class="sxs-lookup"><span data-stu-id="9e09e-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="9e09e-330">左框架称为源网站，右侧框架称为 "远程网站"。</span><span class="sxs-lookup"><span data-stu-id="9e09e-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="9e09e-331">其中一件事可能会混淆某些开发人员，正确框架中显示的站点不一定是远程站点。</span><span class="sxs-lookup"><span data-stu-id="9e09e-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="9e09e-332">它可以是本地文件系统上的站点或 IIS 的本地实例。</span><span class="sxs-lookup"><span data-stu-id="9e09e-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="9e09e-333">此外，左侧框架中显示的网站不一定是源网站，因为对话框允许您从远程网站*向*源网站发布。</span><span class="sxs-lookup"><span data-stu-id="9e09e-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="9e09e-334">如果要将项目复制到远程网站，则必须在该站点上安装 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="9e09e-335">如果没有，则需要使用 FTP 进行连接。</span><span class="sxs-lookup"><span data-stu-id="9e09e-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="9e09e-336">另一方面，如果要将项目复制到本地 IIS 实例，则不需要 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-337">如果尝试在本地 IIS 实例上创建新的网站，并安装 FrontPage 2002 服务器扩展，则将收到一条错误消息，告知你在 SharePoint 服务器上不支持创建网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="9e09e-338">在这种情况下，你可以选择安装 FrontPage 2000 服务器扩展或删除 FrontPage 服务器扩展。</span><span class="sxs-lookup"><span data-stu-id="9e09e-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>

<span data-ttu-id="9e09e-339">单击此处查看 "复制网站" 功能的视频演练。</span><span class="sxs-lookup"><span data-stu-id="9e09e-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>

![](improvements-in-visual-studio-2005/_static/image4.png)

[<span data-ttu-id="9e09e-340">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="9e09e-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a><span data-ttu-id="9e09e-341">调试改进</span><span class="sxs-lookup"><span data-stu-id="9e09e-341">Improvements in Debugging</span></span>

<span data-ttu-id="9e09e-342">在 Visual Studio 2005 中进行调试有四项重要改进。</span><span class="sxs-lookup"><span data-stu-id="9e09e-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="9e09e-343">不能以非管理员身份在本地调试。</span><span class="sxs-lookup"><span data-stu-id="9e09e-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="9e09e-344">默认情况下，编译元素的 Debug 属性为 false。</span><span class="sxs-lookup"><span data-stu-id="9e09e-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="9e09e-345">远程调试设置和配置比以往更容易。</span><span class="sxs-lookup"><span data-stu-id="9e09e-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="9e09e-346">你现在可以调试通过 FTP 位置打开的网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="9e09e-347">作为非管理员调试</span><span class="sxs-lookup"><span data-stu-id="9e09e-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="9e09e-348">添加 ASP.NET 开发服务器允许非管理员轻松地立即调试 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="9e09e-349">当调试在本地文件系统上运行的 ASP.NET 应用程序时，Visual Studio 将在登录用户的上下文中启动 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="9e09e-350">然后，该用户可以调试该应用程序，而无需进行任何其他配置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="9e09e-351">默认情况下，调试为 False</span><span class="sxs-lookup"><span data-stu-id="9e09e-351">Debug is False by Default</span></span>

<span data-ttu-id="9e09e-352">在 ASP.NET 1.x 中，web.config 文件的*编译*元素中的*debug*属性默认设置为*true* 。</span><span class="sxs-lookup"><span data-stu-id="9e09e-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="9e09e-353">在将应用程序部署到生产环境之前，始终建议开发人员将此特性设置为*false* ，但由于大多数开发人员并不完全了解将 debug 特性设置为 true 的结果，因此它们只是原样保留原样。</span><span class="sxs-lookup"><span data-stu-id="9e09e-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="9e09e-354">将 debug 属性设置为 true 时，最严重的问题是它禁用了网络批处理编译模型。</span><span class="sxs-lookup"><span data-stu-id="9e09e-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="9e09e-355">因此，每个页面都编译为单独的 DLL。</span><span class="sxs-lookup"><span data-stu-id="9e09e-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="9e09e-356">如果 Web 应用程序由数千个页面（而非闻所未闻）组成，这意味着该应用程序将创建数千个小的 Dll。</span><span class="sxs-lookup"><span data-stu-id="9e09e-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="9e09e-357">虽然这些 Dll 大小较小，但不会将其加载到内存中的任何特定位置。</span><span class="sxs-lookup"><span data-stu-id="9e09e-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="9e09e-358">因此，它们会导致系统内存碎片，并可能导致 OutOfMemoryException。</span><span class="sxs-lookup"><span data-stu-id="9e09e-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="9e09e-359">在 ASP.NET 2.0 中，debug 属性默认设置为 false。</span><span class="sxs-lookup"><span data-stu-id="9e09e-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="9e09e-360">正如您所看到的，当开发人员在 Visual Studio 2005 中调试 ASP.NET 应用程序时，系统将提示他们添加启用了调试的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="9e09e-361">这样做会产生与 ASP.NET 1.x 相同的缺点，但现在，开发人员可以清楚地警告，在将应用程序移至生产环境之前，应将该属性重置为 false。</span><span class="sxs-lookup"><span data-stu-id="9e09e-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="9e09e-362">远程调试设置和配置</span><span class="sxs-lookup"><span data-stu-id="9e09e-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="9e09e-363">在 Visual Studio 2002/2003 中，远程调试依赖于计算机调试管理器（wsdl.exe）和 vs7jit 进程。</span><span class="sxs-lookup"><span data-stu-id="9e09e-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="9e09e-364">因此，对于客户来说，排除远程调试问题通常是一个黑框，对于 PSS，这通常不是很好的做法。</span><span class="sxs-lookup"><span data-stu-id="9e09e-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="9e09e-365">Visual Studio 2005 消除了对 mdm 和 vs7jit 进程的依赖。</span><span class="sxs-lookup"><span data-stu-id="9e09e-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="9e09e-366">相反，它现在使用远程调试监视器服务（msvsmon）。</span><span class="sxs-lookup"><span data-stu-id="9e09e-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="9e09e-367">在 Visual Studio 2005 中远程调试的要求非常简单。</span><span class="sxs-lookup"><span data-stu-id="9e09e-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="9e09e-368">在调试之前，需要在远程服务器上运行 msvsmon。</span><span class="sxs-lookup"><span data-stu-id="9e09e-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="9e09e-369">你可以从 Visual Studio CD 安装远程调试监视器，也可以直接从共享运行 msvsmon，无需在 Web 服务器上安装任何内容。</span><span class="sxs-lookup"><span data-stu-id="9e09e-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="9e09e-370">运行 msvsmon 时，可能会抱怨阻止远程调试的端口。</span><span class="sxs-lookup"><span data-stu-id="9e09e-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="9e09e-371">幸运的是，你可以直接在警告对话框内取消阻止端口，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e09e-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>

![通知： Windows 防火墙正在阻止远程调试](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="9e09e-373">**图 12**：通知： Windows 防火墙正在阻止远程调试</span><span class="sxs-lookup"><span data-stu-id="9e09e-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>

<span data-ttu-id="9e09e-374">取消阻止调试所需的端口后，会看到远程调试监视器，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e09e-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="9e09e-375">通过此接口，你可以轻松监视连接和更改调试权限。</span><span class="sxs-lookup"><span data-stu-id="9e09e-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>

![远程调试监视器](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="9e09e-377">**图 13**：远程调试监视器</span><span class="sxs-lookup"><span data-stu-id="9e09e-377">**Figure 13**: The Remote Debugging Monitor</span></span>

<span data-ttu-id="9e09e-378">还可以远程调试通过 FTP 打开的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="9e09e-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="9e09e-379">步骤与前面介绍的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="9e09e-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="9e09e-380">但是，您需要指定一个基 URL 来浏览该模块，如上文所述。</span><span class="sxs-lookup"><span data-stu-id="9e09e-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="9e09e-381">实验室2</span><span class="sxs-lookup"><span data-stu-id="9e09e-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="9e09e-382">用 Visual Studio 2005 进行远程调试</span><span class="sxs-lookup"><span data-stu-id="9e09e-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="9e09e-383">此实验室将引导你完成使用 Visual Studio 2005 的远程调试。</span><span class="sxs-lookup"><span data-stu-id="9e09e-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="9e09e-384">单击此处查看此实验的视频演练。</span><span class="sxs-lookup"><span data-stu-id="9e09e-384">Click here for a video walkthrough of this lab.</span></span>

![](improvements-in-visual-studio-2005/_static/image5.png)

[<span data-ttu-id="9e09e-385">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="9e09e-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

<span data-ttu-id="9e09e-386">此实验要求您具有两台计算机，一个运行 Visual Studio 2005，另一个运行 IIS 5 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="9e09e-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="9e09e-387">打开 Visual Studio 2005 并在远程服务器上创建一个新网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-388">您可以在远程 IIS 实例或 FTP 上创建网站。</span><span class="sxs-lookup"><span data-stu-id="9e09e-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>

1. <span data-ttu-id="9e09e-389">在远程 Web 服务器上，使用 UNC 路径在开发计算机上查找 msvsmon 并执行它。</span><span class="sxs-lookup"><span data-stu-id="9e09e-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="9e09e-390">Msvsmon 的默认位置为//server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote 调试器/x86。</span><span class="sxs-lookup"><span data-stu-id="9e09e-390">The default location for msvsmon.exe is //server/c$/Program Files/Microsoft Visual Studio 8/Common7/IDE/Remote Debugger/x86.</span></span>
2. <span data-ttu-id="9e09e-391">如果系统提示您解除阻止用于远程调试的端口，请执行此操作。</span><span class="sxs-lookup"><span data-stu-id="9e09e-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="9e09e-392">从开发计算机中，打开 default.aspx 的代码隐藏，并在 Page/_Load 方法中设置断点。</span><span class="sxs-lookup"><span data-stu-id="9e09e-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page/_Load method.</span></span>
4. <span data-ttu-id="9e09e-393">开始从开发计算机进行调试。</span><span class="sxs-lookup"><span data-stu-id="9e09e-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="9e09e-394">应该按预期命中断点。</span><span class="sxs-lookup"><span data-stu-id="9e09e-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="9e09e-395">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="9e09e-395">ASP.NET Development Server</span></span>

<span data-ttu-id="9e09e-396">如前所述，Visual Studio 2005 附带了一个名为 ASP.NET 开发服务器的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-396">As we've already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="9e09e-397">（ASP.NET 开发服务器有时称为 Cassini。）此 Web 服务器是浏览和调试在文件系统上运行的 Web 应用程序的便捷方法。</span><span class="sxs-lookup"><span data-stu-id="9e09e-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="9e09e-398">ASP.NET 开发服务器是受限制的 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="9e09e-399">它不允许远程连接，它不允许任何用户，而不是启动 Web 服务器的用户的任何请求。</span><span class="sxs-lookup"><span data-stu-id="9e09e-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="9e09e-400">它也不具备提供 ASP 页的功能。</span><span class="sxs-lookup"><span data-stu-id="9e09e-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="9e09e-401">仅提供 ASP.NET 资源和 HTML 资源（包括图像、CSS 文件等）。</span><span class="sxs-lookup"><span data-stu-id="9e09e-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="9e09e-402">ASP.NET 开发服务器可以通过命令行启动，方法是运行位于 c：/Windows/Webdev.webserver.exe/Framework/v2.0/v2.0/ */* / */* /\* 的文件。</span><span class="sxs-lookup"><span data-stu-id="9e09e-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:/Windows/Microsoft.NET/Framework/v2.0./*/*/*/*/\*.</span></span> <span data-ttu-id="9e09e-403">以下对话框显示可用的参数。</span><span class="sxs-lookup"><span data-stu-id="9e09e-403">The following dialog displays the parameters that are available.</span></span>

![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="9e09e-404">**图14**</span><span class="sxs-lookup"><span data-stu-id="9e09e-404">**Figure 14**</span></span>

> [!NOTE]
> <span data-ttu-id="9e09e-405">通过命令行显式启动时不支持 ASP.NET 开发服务器。</span><span class="sxs-lookup"><span data-stu-id="9e09e-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>
