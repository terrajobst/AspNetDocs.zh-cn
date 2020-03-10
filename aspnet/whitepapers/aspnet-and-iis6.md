---
uid: whitepapers/aspnet-and-iis6
title: 运行带有 IIS 6.0 的 ASP.NET 1.1 |Microsoft Docs
author: rick-anderson
description: 虽然 Windows Server 2003 同时包含 IIS 6.0 和 ASP.NET 1.1，但默认情况下这些组件处于禁用状态。 本白皮书介绍了如何启用 IIS 6.0 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78419846"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="d9016-104">通过 IIS 6.0 运行 ASP.NET 1.1</span><span class="sxs-lookup"><span data-stu-id="d9016-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="d9016-105">虽然 Windows Server 2003 同时包含 IIS 6.0 和 ASP.NET 1.1，但默认情况下这些组件处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="d9016-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="d9016-106">本白皮书介绍了如何启用 IIS 6.0 和 ASP.NET 1.1，并建议使用几个配置设置来获得 IIS 和 ASP.NET 的最佳性能。</span><span class="sxs-lookup"><span data-stu-id="d9016-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="d9016-107">适用于 ASP.NET 1.1 和 IIS 6.0。</span><span class="sxs-lookup"><span data-stu-id="d9016-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="d9016-108">ASP.NET 1.1 附带 Windows Server 2003，其中还包括最新版本的 Internet Information Server （IIS）版本6.0。</span><span class="sxs-lookup"><span data-stu-id="d9016-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="d9016-109">IIS 6.0 和 ASP.NET 1.1 设计为无缝集成，而 ASP.NET 现在默认为新的 IIS 6.0 工作进程模型。</span><span class="sxs-lookup"><span data-stu-id="d9016-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="d9016-110">默认情况下未安装 ASP.NET 1。1</span><span class="sxs-lookup"><span data-stu-id="d9016-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="d9016-111">与早期版本的 Microsoft 服务器操作系统不同，默认情况下不启用 Internet Information Server （IIS）;也不是 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="d9016-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="d9016-112">有两个选项可用于启用 IIS：</span><span class="sxs-lookup"><span data-stu-id="d9016-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="d9016-113">启用 IIS，选项 #1-配置服务器向导</span><span class="sxs-lookup"><span data-stu-id="d9016-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="d9016-114">Windows Server 2003 提供了一个新的 "配置您的服务器向导"，以帮助您以所需的模式正确配置您的服务器。</span><span class="sxs-lookup"><span data-stu-id="d9016-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="d9016-115">若要启动向导-注意若要运行向导，必须以管理员身份登录： "开始" |程序 |"管理工具"，然后选择 "配置服务器"。</span><span class="sxs-lookup"><span data-stu-id="d9016-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="d9016-116">选择后，您应该会看到 "配置您的服务器向导" 打开屏幕：</span><span class="sxs-lookup"><span data-stu-id="d9016-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="d9016-117">单击 "下一 &gt;"：</span><span class="sxs-lookup"><span data-stu-id="d9016-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="d9016-118">单击 "下一 &gt;"</span><span class="sxs-lookup"><span data-stu-id="d9016-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="d9016-119">在此屏幕上，需要选择 "应用程序服务器（IIS、ASP.NET）" 作为要配置的选项。</span><span class="sxs-lookup"><span data-stu-id="d9016-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="d9016-120">单击 "下一 &gt;"。</span><span class="sxs-lookup"><span data-stu-id="d9016-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="d9016-121">选择将服务器配置为应用程序服务器后，将显示此屏幕，提示应安装的其他功能。</span><span class="sxs-lookup"><span data-stu-id="d9016-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="d9016-122">默认情况下，这两个选项都处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="d9016-122">Neither option is selected by default.</span></span> <span data-ttu-id="d9016-123">若要自动启用 ASP.NET，需要选择 "启用 ASP"。NET "。</span><span class="sxs-lookup"><span data-stu-id="d9016-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="d9016-124">单击 "下一 &gt;"。</span><span class="sxs-lookup"><span data-stu-id="d9016-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="d9016-125">此屏幕显示要安装的选项。</span><span class="sxs-lookup"><span data-stu-id="d9016-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="d9016-126">单击 "下一 &gt;"。</span><span class="sxs-lookup"><span data-stu-id="d9016-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="d9016-127">当你选择的选项正在安装时，你将看到此屏幕。</span><span class="sxs-lookup"><span data-stu-id="d9016-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="d9016-128">安装服务时，显示其他对话框是正常现象。</span><span class="sxs-lookup"><span data-stu-id="d9016-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="d9016-129">系统还会提示你输入 Windows 2003 服务器安装 CD 的位置。</span><span class="sxs-lookup"><span data-stu-id="d9016-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="d9016-130">完成后单击 "下一 &gt;"。</span><span class="sxs-lookup"><span data-stu-id="d9016-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="d9016-131">单击 "完成"-Windows Server 2003 现已配置为支持 IIS 6.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="d9016-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="d9016-132">启用 IIS，选项 #2-手动配置 IIS 和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="d9016-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="d9016-133">如果您不希望使用 "配置您的服务器向导"，则可以选择使用控制面板中的 "添加或删除程序" 来安装 IIS 6.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="d9016-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="d9016-134">首先，打开 "控制面板"：</span><span class="sxs-lookup"><span data-stu-id="d9016-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="d9016-135">接下来，单击 "添加/删除 Windows 组件"，这将打开 "Windows 组件向导"：</span><span class="sxs-lookup"><span data-stu-id="d9016-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="d9016-136">突出显示并选中 "应用程序服务器"，然后单击 "详细信息"</span><span class="sxs-lookup"><span data-stu-id="d9016-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="d9016-137">鼠标</span><span class="sxs-lookup"><span data-stu-id="d9016-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="d9016-138">若要安装 ASP.NET，请选中 "ASP"。NET "。</span><span class="sxs-lookup"><span data-stu-id="d9016-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="d9016-139">单击 "确定" 以返回到 Windows 组件向导。</span><span class="sxs-lookup"><span data-stu-id="d9016-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="d9016-140">在 Windows 组件向导中单击 "下一 &gt;" 开始安装：</span><span class="sxs-lookup"><span data-stu-id="d9016-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="d9016-141">安装服务时，显示其他对话框是正常现象。</span><span class="sxs-lookup"><span data-stu-id="d9016-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="d9016-142">系统还会提示你输入 Windows 2003 服务器安装 CD 的位置。</span><span class="sxs-lookup"><span data-stu-id="d9016-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="d9016-143">安装完成后，你将看到 "Windows 组件向导" 的最后一个屏幕：</span><span class="sxs-lookup"><span data-stu-id="d9016-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="d9016-144">IIS 6.0 和 ASP.NET 1.1 现在已配置并且可用。</span><span class="sxs-lookup"><span data-stu-id="d9016-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="d9016-145">建议的设置</span><span class="sxs-lookup"><span data-stu-id="d9016-145">Recommended Settings</span></span>

<span data-ttu-id="d9016-146">当使用 IIS 6.0 运行 ASP.NET 1.1 时，建议使用几个配置设置从 ASP.NET 获得最佳性能：</span><span class="sxs-lookup"><span data-stu-id="d9016-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="d9016-147">配置工作进程内存限制</span><span class="sxs-lookup"><span data-stu-id="d9016-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="d9016-148">配置工作进程回收</span><span class="sxs-lookup"><span data-stu-id="d9016-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="d9016-149">配置工作进程内存限制</span><span class="sxs-lookup"><span data-stu-id="d9016-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="d9016-150">默认情况下，IIS 6.0 不会对允许 IIS 使用的内存量设置限制。</span><span class="sxs-lookup"><span data-stu-id="d9016-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="d9016-151">ASP.NET.NET 的缓存功能依赖于内存的限制，因此缓存可以主动地从内存中删除未使用的项。</span><span class="sxs-lookup"><span data-stu-id="d9016-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="d9016-152">建议配置 IIS 6.0 的内存回收功能。</span><span class="sxs-lookup"><span data-stu-id="d9016-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="d9016-153">若要配置此打开的 Internet Information Services 管理器（开始 |程序 |管理工具 |Internet Information Services）。</span><span class="sxs-lookup"><span data-stu-id="d9016-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="d9016-154">打开后，展开 "应用程序池" 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d9016-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="d9016-155">对于每个应用程序池：</span><span class="sxs-lookup"><span data-stu-id="d9016-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="d9016-156">右键单击应用程序池，例如 "DefaultAppPool"，然后选择 "属性"：</span><span class="sxs-lookup"><span data-stu-id="d9016-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="d9016-157">接下来，单击 "最大使用的内存（mb）：" 以启用内存回收。</span><span class="sxs-lookup"><span data-stu-id="d9016-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="d9016-158">此值不应大于服务器上的物理（非虚拟）内存量，良好的近似值是物理内存的60%，即，对于具有512MB 的物理内存的服务器，选择310。</span><span class="sxs-lookup"><span data-stu-id="d9016-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="d9016-159">使用2GB 地址空间时，还建议最大值不能超过800MB。</span><span class="sxs-lookup"><span data-stu-id="d9016-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="d9016-160">如果服务器的内存地址空间为3GB，则工作进程的最大内存限制可以高达1，800MB：</span><span class="sxs-lookup"><span data-stu-id="d9016-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="d9016-161">单击 "应用"，然后单击 "确定" 退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="d9016-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="d9016-162">对所有可用的应用程序池重复此操作。</span><span class="sxs-lookup"><span data-stu-id="d9016-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="d9016-163">配置辅助角色回收</span><span class="sxs-lookup"><span data-stu-id="d9016-163">Configuring worker recycling</span></span>

<span data-ttu-id="d9016-164">默认情况下，IIS 6.0 配置为每29小时回收其工作进程。</span><span class="sxs-lookup"><span data-stu-id="d9016-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="d9016-165">这对运行 ASP.NET 的应用程序来说有点迫切，建议禁用自动工作进程回收。</span><span class="sxs-lookup"><span data-stu-id="d9016-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="d9016-166">若要禁用自动工作进程回收，请先打开 Internet Information Services Manager （开始 |程序 |管理工具 |Internet Information Services）。</span><span class="sxs-lookup"><span data-stu-id="d9016-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="d9016-167">打开后，展开 "应用程序池" 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d9016-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="d9016-168">对于每个应用程序池：</span><span class="sxs-lookup"><span data-stu-id="d9016-168">For each application pool:</span></span>

1. <span data-ttu-id="d9016-169">右键单击应用程序池，例如 "DefaultAppPool"，然后选择 "属性"：</span><span class="sxs-lookup"><span data-stu-id="d9016-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="d9016-170">取消选中 "回收工作进程（分钟）："：</span><span class="sxs-lookup"><span data-stu-id="d9016-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="d9016-171">单击 "应用"，然后单击 "确定" 退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="d9016-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="d9016-172">对所有可用的应用程序池重复此操作。</span><span class="sxs-lookup"><span data-stu-id="d9016-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="d9016-173">授予对文件系统的写访问权限</span><span class="sxs-lookup"><span data-stu-id="d9016-173">Granting write access to the file system</span></span>

<span data-ttu-id="d9016-174">如果你的应用程序需要对文件系统的写入访问权限，并且你使用的是 NTFS，则需要修改文件夹或文件上的访问控制列表（ACL），以授予对的 ASP.NET 访问权限。</span><span class="sxs-lookup"><span data-stu-id="d9016-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="d9016-175">例如，若要授予 ASP.NET 对 c:\inetpub\wwwroot 的写入访问权限，请先打开资源管理器，然后导航到该目录：</span><span class="sxs-lookup"><span data-stu-id="d9016-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="d9016-176">接下来，右键单击目录，例如 "wwwroot"，然后选择 "属性"。</span><span class="sxs-lookup"><span data-stu-id="d9016-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="d9016-177">"属性" 对话框打开后，选择 "安全" 选项卡：</span><span class="sxs-lookup"><span data-stu-id="d9016-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="d9016-178">C:\inetpub\wwwroot\ 目录是一个特殊的目录，其中已授予特殊 IIS 6.0 组 "IIS\_WPG" 的读取 &amp; 执行、列出文件夹内容和读取权限。</span><span class="sxs-lookup"><span data-stu-id="d9016-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="d9016-179">但是，若要授予写入权限，需要单击 "写入时允许" 复选框：</span><span class="sxs-lookup"><span data-stu-id="d9016-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="d9016-180">IIS 6.0 现在对此文件夹具有写入权限。</span><span class="sxs-lookup"><span data-stu-id="d9016-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="d9016-181">若要授予对其他文件夹的写权限，请按照以下步骤进行操作：注意，如果 IIS\_WPG 组尚不存在，则可能需要将其添加。</span><span class="sxs-lookup"><span data-stu-id="d9016-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="d9016-182">为 IIS\_WPG 授予写入权限将允许任何 ASP.NET 应用程序写入此目录。</span><span class="sxs-lookup"><span data-stu-id="d9016-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="d9016-183">支持 SQL Server 的集成身份验证</span><span class="sxs-lookup"><span data-stu-id="d9016-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="d9016-184">集成身份验证允许 SQL Server 利用 Windows NT 身份验证来验证 SQL Server 登录帐户。</span><span class="sxs-lookup"><span data-stu-id="d9016-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="d9016-185">这允许用户绕过标准 SQL Server 登录过程。</span><span class="sxs-lookup"><span data-stu-id="d9016-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="d9016-186">使用此方法，网络用户无需提供单独的登录标识或密码即可访问 SQL Server 数据库，因为 SQL Server 从 Windows NT 网络安全过程获取用户和密码信息。</span><span class="sxs-lookup"><span data-stu-id="d9016-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="d9016-187">为 ASP.NET 应用程序选择 "集成身份验证" 是一个不错的选择，因为你的应用程序的连接字符串中没有存储任何凭据。</span><span class="sxs-lookup"><span data-stu-id="d9016-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="d9016-188">相反，用于连接到 SQL 的连接字符串将如下所示：</span><span class="sxs-lookup"><span data-stu-id="d9016-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="d9016-189">此连接字符串通知 SQL Server 使用尝试访问 SQL Server 的应用程序的 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="d9016-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="d9016-190">对于 ASP.NET/IIS 6，这是 IIS\_WPG 组中的帐户。</span><span class="sxs-lookup"><span data-stu-id="d9016-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="d9016-191">若要在 SQL Server 与 ASP.NET 之间启用集成身份验证，需要首先确保已将 SQL Server 配置为使用集成身份验证或混合模式身份验证-请检查你的 DBA 以确定这一点。</span><span class="sxs-lookup"><span data-stu-id="d9016-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="d9016-192">如果 SQL Server 采用这两种模式之一，则可以使用集成身份验证。</span><span class="sxs-lookup"><span data-stu-id="d9016-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="d9016-193">打开 SQL Server Enterprise 管理器（开始 |程序 |Microsoft SQL Server |企业管理器）中，选择适当的服务器，然后展开 "安全性" 文件夹：</span><span class="sxs-lookup"><span data-stu-id="d9016-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="d9016-194">如果未列出 "BUILTINT\IIS\_WPG" 组，请右键单击 "登录名"，然后选择 "新建 Login：</span><span class="sxs-lookup"><span data-stu-id="d9016-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="d9016-195">在 "名称：" 文本框中，输入 "[Server/Domain Name] \IIS\_WPG" 或单击省略号按钮以打开 Windows NT 用户/组选取器：</span><span class="sxs-lookup"><span data-stu-id="d9016-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="d9016-196">选择当前计算机的 IIS\_WPG 组，然后单击 "添加"，然后单击 "确定" 以关闭选取器。</span><span class="sxs-lookup"><span data-stu-id="d9016-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="d9016-197">然后还需要设置默认数据库和访问数据库的权限。</span><span class="sxs-lookup"><span data-stu-id="d9016-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="d9016-198">若要设置默认数据库，请从下拉列表中选择，例如 "Northwind：</span><span class="sxs-lookup"><span data-stu-id="d9016-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="d9016-199">接下来，单击 "数据库访问" 选项卡：</span><span class="sxs-lookup"><span data-stu-id="d9016-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="d9016-200">单击要允许访问的每个数据库的 "允许" 复选框。</span><span class="sxs-lookup"><span data-stu-id="d9016-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="d9016-201">还需要选择数据库角色，检查 db\_所有者将确保您的登录名具有管理和使用所选数据库所需的所有权限。</span><span class="sxs-lookup"><span data-stu-id="d9016-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="d9016-202">单击 "确定" 退出属性对话框。</span><span class="sxs-lookup"><span data-stu-id="d9016-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="d9016-203">现在，你的 ASP.NET 应用程序已配置为支持集成 SQL Server 身份验证。</span><span class="sxs-lookup"><span data-stu-id="d9016-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="d9016-204">不要在 IIS 6.0 本机模式下运行 ASP.NET 1。0</span><span class="sxs-lookup"><span data-stu-id="d9016-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="d9016-205">Iis 6.0 上的 ASP.NET 1.0 仅在 IIS 5 兼容模式下受支持。</span><span class="sxs-lookup"><span data-stu-id="d9016-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="d9016-206">若要将 ASP.NET 1.0 配置为在 IIS 5.0 兼容模式下运行，请打开 Internet 服务管理器并右键单击 "网站"，然后选择 "属性"：</span><span class="sxs-lookup"><span data-stu-id="d9016-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="d9016-207">切换到 "服务" 选项卡并检查？在 IIS 5.0 隔离模式下运行 WWW 服务？：</span><span class="sxs-lookup"><span data-stu-id="d9016-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
