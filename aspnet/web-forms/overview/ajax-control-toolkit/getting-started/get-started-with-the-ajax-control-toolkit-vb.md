---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: AJAX 控件工具包入门 |Microsoft Docs
author: microsoft
description: 了解开始使用 AJAX 控件工具包所需的所有知识。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497138"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a><span data-ttu-id="8820e-103">AJAX 控件工具包入门 (VB)</span><span class="sxs-lookup"><span data-stu-id="8820e-103">Get Started with the AJAX Control Toolkit (VB)</span></span>

<span data-ttu-id="8820e-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8820e-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="8820e-105">了解开始使用 AJAX 控件工具包所需的所有知识。</span><span class="sxs-lookup"><span data-stu-id="8820e-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="8820e-106">AJAX 控件工具包包含30多个免费控件，可以在 ASP.NET 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="8820e-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="8820e-107">在本教程中，您将了解如何下载 AJAX 控件工具包并将工具包控件添加到您的 Visual Studio/Visual Web Developer Express 工具箱。</span><span class="sxs-lookup"><span data-stu-id="8820e-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="8820e-108">下载 AJAX 控件工具包</span><span class="sxs-lookup"><span data-stu-id="8820e-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="8820e-109">[AJAX 控件工具包](http://devexpress.com/act)是由 ASP.NET 社区和 ASP.NET 团队成员开发的开源项目。</span><span class="sxs-lookup"><span data-stu-id="8820e-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span>

<span data-ttu-id="8820e-110">[![下载 AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8820e-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)</span></span>

<span data-ttu-id="8820e-111">**图 01**：下载 AJAX 控件工具包（[单击以查看完全大小的映像](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="8820e-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))</span></span>

<span data-ttu-id="8820e-112">下载文件后，需要取消阻止此文件。</span><span class="sxs-lookup"><span data-stu-id="8820e-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="8820e-113">右键单击该文件，选择 "属性"，然后单击 "**取消阻止**" 按钮（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="8820e-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="8820e-114">[![取消阻止 AJAX 控件工具包 ZIP 文件](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8820e-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)</span></span>

<span data-ttu-id="8820e-115">**图 02**：取消阻止 AJAX 控件工具包 ZIP 文件（[单击以查看完全大小的映像](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="8820e-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))</span></span>

<span data-ttu-id="8820e-116">取消阻止该文件后，可以将该文件解压缩：右键单击该文件，然后选择 "**全部提取**" 菜单选项。</span><span class="sxs-lookup"><span data-stu-id="8820e-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="8820e-117">现在，我们已准备好将工具包添加到 Visual Studio/Visual Web Developer 工具箱。</span><span class="sxs-lookup"><span data-stu-id="8820e-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="8820e-118">将 AJAX 控件工具包添加到工具箱</span><span class="sxs-lookup"><span data-stu-id="8820e-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="8820e-119">使用 AJAX 控件工具包的最简单方法是将工具包添加到 Visual Studio/Visual Web Developer 工具箱（请参阅图3）。</span><span class="sxs-lookup"><span data-stu-id="8820e-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="8820e-120">这样一来，只需将工具包控件拖动到页面上即可。</span><span class="sxs-lookup"><span data-stu-id="8820e-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="8820e-121">[工具箱中显示 ![AJAX 控件工具包](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8820e-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)</span></span>

<span data-ttu-id="8820e-122">**图 03**：在工具箱中显示 AJAX 控件工具包（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="8820e-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png))</span></span>

<span data-ttu-id="8820e-123">首先，需要将 AJAX 控件工具包选项卡添加到 "工具箱"。</span><span class="sxs-lookup"><span data-stu-id="8820e-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="8820e-124">请执行下列步骤。</span><span class="sxs-lookup"><span data-stu-id="8820e-124">Follow these steps.</span></span>

1. <span data-ttu-id="8820e-125">通过选择 "菜单" "文件" "新建网站" 来创建新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="8820e-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="8820e-126">在 "解决方案资源管理器" 窗口中双击 "default.aspx"，以在编辑器中打开文件。</span><span class="sxs-lookup"><span data-stu-id="8820e-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="8820e-127">右键单击 "常规" 选项卡下的 "工具箱"，然后选择 "添加" 菜单选项**卡**（请参阅图4）。</span><span class="sxs-lookup"><span data-stu-id="8820e-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="8820e-128">输入名为 AJAX 控件工具包的新选项卡。</span><span class="sxs-lookup"><span data-stu-id="8820e-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="8820e-129">[添加新选项卡 ![](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8820e-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)</span></span>

<span data-ttu-id="8820e-130">**图 04**：添加新选项卡（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="8820e-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))</span></span>

<span data-ttu-id="8820e-131">接下来，需要将 AJAX 控件工具包控件添加到新选项卡。请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8820e-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="8820e-132">右键单击 "AJAX 控件工具包" 选项卡，然后选择菜单选项 "**选择项" （参见图5）** 。</span><span class="sxs-lookup"><span data-stu-id="8820e-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="8820e-133">浏览到您解压缩 AJAX 控件工具包的位置，并选择 AjaxControlToolkit 程序集。</span><span class="sxs-lookup"><span data-stu-id="8820e-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="8820e-134">[![选择要添加到工具箱中的项](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8820e-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)</span></span>

<span data-ttu-id="8820e-135">**图 05**：选择要添加到 "工具箱" 的项（[单击以查看完全大小的图像](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="8820e-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png))</span></span>

<span data-ttu-id="8820e-136">完成这些步骤后，所有工具包控件都将显示在工具箱中。</span><span class="sxs-lookup"><span data-stu-id="8820e-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="8820e-137">升级到新版本的工具包</span><span class="sxs-lookup"><span data-stu-id="8820e-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="8820e-138">如果你使用的是较旧版本的工具包，而现在需要迁移到更高版本，则建议执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8820e-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="8820e-139">二进制文件-从网站 Bin 文件夹中删除旧版本的 AjaxControlToolkit 程序集。</span><span class="sxs-lookup"><span data-stu-id="8820e-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="8820e-140">工具箱项-删除 "AJAX 控件工具包" 选项卡，然后执行上述步骤，用 AjaxControlToolkit 程序集的新版本重新创建该选项卡。</span><span class="sxs-lookup"><span data-stu-id="8820e-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8820e-141">[上一页](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [下一页](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8820e-141">[Previous](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
[Next](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)</span></span>
