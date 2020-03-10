---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET 拒绝了对 IIS 目录的访问 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍当 ASP.NET 应用程序的请求返回 "拒绝访问 DirectoryName 目录" 时必须执行的操作。 无法进行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518570"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="6907e-104">ASP.NET 拒绝了对 IIS 目录的访问</span><span class="sxs-lookup"><span data-stu-id="6907e-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="6907e-105">本白皮书介绍当 ASP.NET 应用程序的请求返回 "拒绝访问*DirectoryName*目录" 时必须执行的操作。</span><span class="sxs-lookup"><span data-stu-id="6907e-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="6907e-106">未能开始监视目录更改。 "</span><span class="sxs-lookup"><span data-stu-id="6907e-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="6907e-107">适用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="6907e-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="6907e-108">现在，使用在本地计算机上注册为 "ASPNET" 帐户的特权较低的 windows 帐户运行 ASP.NET V1 RTM。</span><span class="sxs-lookup"><span data-stu-id="6907e-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="6907e-109">在某些锁定的系统上，默认情况下，此帐户不能访问网站的内容目录、应用程序根目录或网站根目录。</span><span class="sxs-lookup"><span data-stu-id="6907e-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="6907e-110">在这种情况下，当从给定的 web 应用程序请求页面时，你将收到以下错误：</span><span class="sxs-lookup"><span data-stu-id="6907e-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="6907e-111">若要解决此问题，需要更改相应目录上的安全权限。</span><span class="sxs-lookup"><span data-stu-id="6907e-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="6907e-112">具体而言，ASP.NET 需要对网站根目录（例如： c:\inetpub\wwwroot 或你可能已在 IIS 中配置的任何备用网站目录）的 ASPNET 帐户的读取、执行和列表访问权限，内容目录和应用程序根目录以便监视配置文件更改。</span><span class="sxs-lookup"><span data-stu-id="6907e-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="6907e-113">应用程序根目录对应于 IIS 管理工具（inetmgr）中与应用程序虚拟目录关联的文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="6907e-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="6907e-114">例如，请考虑 wwwroot 文件夹下的以下应用程序层次结构。</span><span class="sxs-lookup"><span data-stu-id="6907e-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="6907e-115">在此示例中，ASPNET 帐户需要在 myapp 和 wwwroot 目录中为内容定义以上的读取权限。</span><span class="sxs-lookup"><span data-stu-id="6907e-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="6907e-116">根文件夹中的单个继承 ACL 也可以选择性地用于这两个目录（如果它们是嵌套的）。</span><span class="sxs-lookup"><span data-stu-id="6907e-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="6907e-117">若要将权限添加到目录，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="6907e-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="6907e-118">使用 Windows 资源管理器导航到目录</span><span class="sxs-lookup"><span data-stu-id="6907e-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="6907e-119">右键单击目录文件夹，然后选择 "属性"</span><span class="sxs-lookup"><span data-stu-id="6907e-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="6907e-120">导航到属性对话框上的 "安全" 选项卡</span><span class="sxs-lookup"><span data-stu-id="6907e-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="6907e-121">单击 "添加" 按钮，然后输入计算机名称，后跟 ASPNET 帐户名称。</span><span class="sxs-lookup"><span data-stu-id="6907e-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="6907e-122">例如，在名为 "webdev.webserver.exe" 的计算机上，输入 webdev\ASPNET 并单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="6907e-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="6907e-123">确保 ASPNET 帐户选中 "读取 &amp; 执行"、"列出文件夹内容" 和 "读取" 复选框。</span><span class="sxs-lookup"><span data-stu-id="6907e-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="6907e-124">单击 "确定" 以关闭对话框并保存更改。</span><span class="sxs-lookup"><span data-stu-id="6907e-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="6907e-125">如果需要，可以使用随 Windows 一起提供的脚本或 "cacls .exe" 工具自动执行这些更改。</span><span class="sxs-lookup"><span data-stu-id="6907e-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="6907e-126">有关 ASPNET 帐户的详细信息，请参阅[FAQ 文档](https://go.microsoft.com/fwlink/?LinkId=5828)。</span><span class="sxs-lookup"><span data-stu-id="6907e-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="6907e-127">如果某个给定的 web 应用程序依赖于对特定文件夹或文件具有 "写入" 或 "修改" 权限，则可以按照相同的过程来授予此权限，并选中 "写入" 和/或 "修改" 复选框。</span><span class="sxs-lookup"><span data-stu-id="6907e-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="6907e-128">在 "允许每个人或用户组读取对这些目录的访问权限（这是默认配置）" 的计算机上，不会遇到任何问题，也不需要上述步骤。</span><span class="sxs-lookup"><span data-stu-id="6907e-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
