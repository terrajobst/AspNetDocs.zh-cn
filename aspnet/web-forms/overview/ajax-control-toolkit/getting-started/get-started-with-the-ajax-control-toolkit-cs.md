---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: 开始使用 AJAX 控件工具包 (C#) |Microsoft Docs
author: microsoft
description: 了解所有需要了解开始使用 AJAX 控件工具包。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 3bbbe0c8240a2a77edee8d39a76bf865c95f345e
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59381089"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="c8b59-103">AJAX 控件工具包入门 (C#)</span><span class="sxs-lookup"><span data-stu-id="c8b59-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="c8b59-104">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="c8b59-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="c8b59-105">了解所有需要了解开始使用 AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="c8b59-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>


<span data-ttu-id="c8b59-106">AJAX 控件工具包包含 30 多个可用控件，可以在 ASP.NET 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="c8b59-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="c8b59-107">在本教程中，您将学习如何下载 AJAX 控件工具包和工具包控件添加到 Visual Studio/Visual Web Developer 速成版工具箱。</span><span class="sxs-lookup"><span data-stu-id="c8b59-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="c8b59-108">下载 AJAX 控件工具包</span><span class="sxs-lookup"><span data-stu-id="c8b59-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="c8b59-109">[AJAX 控件工具包](http://devexpress.com/act)由 ASP.NET 社区和 ASP.NET 团队的成员一个开放源代码项目开发。</span><span class="sxs-lookup"><span data-stu-id="c8b59-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 


[![D<span data-ttu-id="c8b59-110">ownloading AJAX 控件工具包]</span><span class="sxs-lookup"><span data-stu-id="c8b59-110">ownloading the AJAX Control Toolkit]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)

<span data-ttu-id="c8b59-111">**图 01**:下载 AJAX 控件工具包 ([单击此项可查看原尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="c8b59-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>


<span data-ttu-id="c8b59-112">下载文件后，你需要取消阻止文件。</span><span class="sxs-lookup"><span data-stu-id="c8b59-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="c8b59-113">右键单击该文件，选择属性，然后单击**解除阻止**按钮 （请参见图 2）。</span><span class="sxs-lookup"><span data-stu-id="c8b59-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>


[![U<span data-ttu-id="c8b59-114">nblocking AJAX 控件工具包 ZIP 文件]</span><span class="sxs-lookup"><span data-stu-id="c8b59-114">nblocking the AJAX Control Toolkit ZIP file]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)

<span data-ttu-id="c8b59-115">**图 02**:取消阻止 AJAX 控件工具包 ZIP 文件 ([单击此项可查看原尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="c8b59-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>


<span data-ttu-id="c8b59-116">取消阻止文件后，你可以解压缩该文件：右键单击该文件，然后选择**全部提取**菜单选项。</span><span class="sxs-lookup"><span data-stu-id="c8b59-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="c8b59-117">现在，我们已准备好工具包添加至 Visual Studio/Visual Web Developer 工具箱。</span><span class="sxs-lookup"><span data-stu-id="c8b59-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="c8b59-118">向工具箱添加 AJAX 控件工具包</span><span class="sxs-lookup"><span data-stu-id="c8b59-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="c8b59-119">使用 AJAX 控件工具包的最简单方法是工具包添加至您的 Visual Studio/Visual Web Developer 工具箱 （参见图 3）。</span><span class="sxs-lookup"><span data-stu-id="c8b59-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="c8b59-120">这样一来，您可以只需将工具包控件拖到页面时想要使用它。</span><span class="sxs-lookup"><span data-stu-id="c8b59-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>


[![A<span data-ttu-id="c8b59-121">JAX 控件工具包将出现在工具箱]</span><span class="sxs-lookup"><span data-stu-id="c8b59-121">JAX Control Toolkit appears in toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)

<span data-ttu-id="c8b59-122">**图 03**:AJAX 控件工具包将出现在工具箱 ([单击此项可查看原尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="c8b59-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>


<span data-ttu-id="c8b59-123">首先，需要将 AJAX 控件工具包选项卡添加到工具箱。</span><span class="sxs-lookup"><span data-stu-id="c8b59-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="c8b59-124">请按照下列步骤。</span><span class="sxs-lookup"><span data-stu-id="c8b59-124">Follow these steps.</span></span>

1. <span data-ttu-id="c8b59-125">通过选择菜单选项文件中，新的网站中创建新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="c8b59-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="c8b59-126">双击解决方案资源管理器窗口中的 Default.aspx，以在编辑器中打开该文件。</span><span class="sxs-lookup"><span data-stu-id="c8b59-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="c8b59-127">右键单击常规选项卡下的工具箱，然后选择菜单选项**添加选项卡**（请参阅图 4）。</span><span class="sxs-lookup"><span data-stu-id="c8b59-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="c8b59-128">输入名为 AJAX 控件工具包的新选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8b59-128">Enter a new tab named AJAX Control Toolkit.</span></span>


[![A<span data-ttu-id="c8b59-129">dding 新选项卡]</span><span class="sxs-lookup"><span data-stu-id="c8b59-129">dding a new tab]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)

<span data-ttu-id="c8b59-130">**图 04**:添加一个新选项卡 ([单击此项可查看原尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="c8b59-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>


<span data-ttu-id="c8b59-131">接下来，您需要将 AJAX 控件工具包控件添加到新的选项卡。请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="c8b59-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="c8b59-132">AJAX 控件工具包选项卡下方右键单击，然后选择菜单选项**选择项 （请参见图 5）**。</span><span class="sxs-lookup"><span data-stu-id="c8b59-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="c8b59-133">浏览到解压缩 AJAX 控件工具包和选择 AjaxControlToolkit.dll 程序集的位置。</span><span class="sxs-lookup"><span data-stu-id="c8b59-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>


[![C<span data-ttu-id="c8b59-134">要添加到工具箱的选择项]</span><span class="sxs-lookup"><span data-stu-id="c8b59-134">hoose items to add to the toolbox]</span></span>(get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)

<span data-ttu-id="c8b59-135">**图 05**:选择要添加到工具箱项 ([单击此项可查看原尺寸图像](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="c8b59-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>


<span data-ttu-id="c8b59-136">完成这些步骤后，所有工具包控件都将出现在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="c8b59-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="c8b59-137">升级到新版本的工具包</span><span class="sxs-lookup"><span data-stu-id="c8b59-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="c8b59-138">如果已使用较旧版本的工具包，现在需要将移动到更高版本的建议的步骤是：</span><span class="sxs-lookup"><span data-stu-id="c8b59-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="c8b59-139">二进制文件-从您网站的 Bin 文件夹中删除 AjaxControlToolkit.dll 程序集的旧版本。</span><span class="sxs-lookup"><span data-stu-id="c8b59-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="c8b59-140">工具箱项-删除 AJAX 控件工具包选项卡，然后按照上述步骤来重新创建具有 AjaxControlToolkit.dll 程序集的新版本的选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8b59-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="c8b59-141">下一步</span><span class="sxs-lookup"><span data-stu-id="c8b59-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)
