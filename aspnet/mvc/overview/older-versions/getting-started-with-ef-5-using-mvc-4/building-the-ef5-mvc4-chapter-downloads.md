---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 为 EF 5 MVC 4 教程构建章节下载 |Microsoft Docs
author: Rick-Anderson
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 10237af40e3914b65e5181f17555697e86adea4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485120"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a><span data-ttu-id="bede9-103">为 EF 5 MVC 4 教程构建章节下载</span><span class="sxs-lookup"><span data-stu-id="bede9-103">Building the Chapter Downloads for the EF 5 MVC 4 Tutorials</span></span>

<span data-ttu-id="bede9-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="bede9-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[<span data-ttu-id="bede9-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="bede9-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> <span data-ttu-id="bede9-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。</span><span class="sxs-lookup"><span data-stu-id="bede9-106">The Contoso University sample web application demonstrates how to create ASP.NET MVC 4 applications using the Entity Framework 5 Code First and Visual Studio 2012.</span></span> <span data-ttu-id="bede9-107">若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="bede9-107">For information about the tutorial series, see [the first tutorial in the series](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

## <a name="building-the-chapter-downloads"></a><span data-ttu-id="bede9-108">生成章节下载</span><span class="sxs-lookup"><span data-stu-id="bede9-108">Building the Chapter Downloads</span></span>

1. <span data-ttu-id="bede9-109">下载并解压缩项目示例 zip 文件。</span><span class="sxs-lookup"><span data-stu-id="bede9-109">Download and unzip the  project sample zip file.</span></span> <span data-ttu-id="bede9-110">在解压缩的下载包中，你将找到其他 zip 文件，每个章节完成一个。</span><span class="sxs-lookup"><span data-stu-id="bede9-110">In the unzipped download package, you will find additional zip files, one for the completion of each chapter.</span></span>
2. <span data-ttu-id="bede9-111">右键单击所需的 zip 文件，单击 "**属性**"，然后单击 "**取消阻止**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="bede9-111">Right click on the desired zip file, click **Properties**, and click the **Unblock** button.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. <span data-ttu-id="bede9-112">解压缩文件。</span><span class="sxs-lookup"><span data-stu-id="bede9-112">Unzip the file.</span></span>
4. <span data-ttu-id="bede9-113">双击*CUx*文件以启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bede9-113">Double-click the *CUx.sln* file to launch Visual Studio.</span></span>
5. <span data-ttu-id="bede9-114">从 "**工具**" 菜单中依次单击 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="bede9-114">From the **Tools** menu, click **NuGet Package Manager**, then **Package Manager Console**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. <span data-ttu-id="bede9-115">在 "程序包管理器控制台" （PMC）中，单击 "**还原**"。</span><span class="sxs-lookup"><span data-stu-id="bede9-115">In the Package Manager Console (PMC), click **Restore**.</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. <span data-ttu-id="bede9-116">退出 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bede9-116">Exit Visual Studio.</span></span>
8. <span data-ttu-id="bede9-117">重新启动 Visual Studio，打开在上述步骤中关闭的解决方案文件。</span><span class="sxs-lookup"><span data-stu-id="bede9-117">Restart Visual Studio, opening the solution file you closed in the step above.</span></span>
9. <span data-ttu-id="bede9-118">在 "程序包管理器控制台" （PMC）中，输入 `Update-Database` 命令：</span><span class="sxs-lookup"><span data-stu-id="bede9-118">In the Package Manager Console (PMC), enter the `Update-Database` command:</span></span>  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > <span data-ttu-id="bede9-119">如果收到以下错误信息：</span><span class="sxs-lookup"><span data-stu-id="bede9-119">If you get the following error:</span></span>  
    >   
    >  <span data-ttu-id="bede9-120">*术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。检查名称的拼写，如果包含路径，请验证路径是否正确，然后重试。*</span><span class="sxs-lookup"><span data-stu-id="bede9-120">*The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.*</span></span>  
    > <span data-ttu-id="bede9-121">退出并重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="bede9-121">Exit and restart Visual Studio.</span></span>

    <span data-ttu-id="bede9-122">每个迁移将运行，种子方法将运行。</span><span class="sxs-lookup"><span data-stu-id="bede9-122">Each migration will run, then the seed method will run.</span></span> <span data-ttu-id="bede9-123">你现在可以运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="bede9-123">You can now run the app.</span></span>

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [<span data-ttu-id="bede9-124">上一页</span><span class="sxs-lookup"><span data-stu-id="bede9-124">Previous</span></span>](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
