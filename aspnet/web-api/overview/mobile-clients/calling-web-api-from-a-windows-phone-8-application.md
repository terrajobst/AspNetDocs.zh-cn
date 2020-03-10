---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: 从 Windows Phone 8 应用程序调用 Web API （C#）-ASP.NET 4。x
author: rmcmurray
description: 代码教程：在 ASP.NET 4.x 中创建 ASP.NET Web API 应用程序，该应用程序向 Windows Phone 8 应用程序提供书籍目录。
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498212"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a><span data-ttu-id="e0b97-103">从 Windows Phone 8 应用程序调用 Web API (C#)</span><span class="sxs-lookup"><span data-stu-id="e0b97-103">Calling Web API from a Windows Phone 8 Application (C#)</span></span>

<span data-ttu-id="e0b97-104">作者： [Robert mcmurray 有关](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="e0b97-104">by [Robert McMurray](https://github.com/rmcmurray)</span></span>

<span data-ttu-id="e0b97-105">在本教程中，你将了解如何创建一个完整的端到端方案，该方案包含一个 ASP.NET Web API 应用程序，该方案向 Windows Phone 8 应用程序提供书籍目录。</span><span class="sxs-lookup"><span data-stu-id="e0b97-105">In this tutorial, you will learn how to create a complete end-to-end scenario consisting of an ASP.NET Web API application that provides a catalog of books to a Windows Phone 8 application.</span></span>

### <a name="overview"></a><span data-ttu-id="e0b97-106">概述</span><span class="sxs-lookup"><span data-stu-id="e0b97-106">Overview</span></span>

<span data-ttu-id="e0b97-107">RESTful 服务（如 ASP.NET Web API）通过抽象服务器端和客户端应用程序的体系结构，为开发人员简化了基于 HTTP 的应用程序的创建过程。</span><span class="sxs-lookup"><span data-stu-id="e0b97-107">RESTful services like ASP.NET Web API simplify the creation of HTTP-based applications for developers by abstracting the architecture for server-side and client-side applications.</span></span> <span data-ttu-id="e0b97-108">Web API 开发人员只需为其应用程序发布必要的 HTTP 方法（例如： GET、POST、PUT、DELETE）和客户端应用程序开发人员只需使用其应用程序所需的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="e0b97-108">Instead of creating a proprietary socket-based protocol for communication, Web API developers simply need to publish the requisite HTTP methods for their application, (for example: GET, POST, PUT, DELETE), and client application developers only need to consume the HTTP methods that are necessary for their application.</span></span>

<span data-ttu-id="e0b97-109">本端到端教程介绍如何使用 Web API 创建以下项目：</span><span class="sxs-lookup"><span data-stu-id="e0b97-109">In this end-to-end tutorial, you will learn how to use Web API to create the following projects:</span></span>

- <span data-ttu-id="e0b97-110">在[本教程的第一部分](#STEP1)中，你将创建一个 ASP.NET Web API 应用程序，该应用程序支持用于管理书籍目录的所有创建、读取、更新和删除（CRUD）操作。</span><span class="sxs-lookup"><span data-stu-id="e0b97-110">In the [first part of this tutorial](#STEP1), you will create an ASP.NET Web API application that supports all of the Create, Read, Update, and Delete (CRUD) operations to manage a book catalog.</span></span> <span data-ttu-id="e0b97-111">此应用程序将使用 MSDN 的[示例 XML 文件（books.xml）](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="e0b97-111">This application will use the [Sample XML File (books.xml)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) from MSDN.</span></span>
- <span data-ttu-id="e0b97-112">在[本教程的第二部分](#STEP2)中，你将创建一个交互式 Windows Phone 8 应用程序，该应用程序从 Web API 应用程序检索数据。</span><span class="sxs-lookup"><span data-stu-id="e0b97-112">In the [second part of this tutorial](#STEP2), you will create an interactive Windows Phone 8 application that retrieves the data from your Web API application.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="e0b97-113">系统必备</span><span class="sxs-lookup"><span data-stu-id="e0b97-113">Prerequisites</span></span>

- <span data-ttu-id="e0b97-114">Visual Studio 2013 安装了 Windows Phone 8 SDK</span><span class="sxs-lookup"><span data-stu-id="e0b97-114">Visual Studio 2013 with the Windows Phone 8 SDK installed</span></span>
- <span data-ttu-id="e0b97-115">Windows 8 或更高版本位于安装了 Hyper-v 的64位系统上</span><span class="sxs-lookup"><span data-stu-id="e0b97-115">Windows 8 or later on a 64-bit system with Hyper-V installed</span></span>
- <span data-ttu-id="e0b97-116">有关其他要求的列表，请参阅[WINDOWS PHONE SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471)下载页面上的 "*系统要求*" 部分。</span><span class="sxs-lookup"><span data-stu-id="e0b97-116">For a list of additional requirements, see the *System Requirements* section on the [Windows Phone SDK 8.0](https://www.microsoft.com/download/details.aspx?id=35471) download page.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b97-117">如果要在本地系统上测试 Web API 与 Windows Phone 8 项目之间的连接，则需按照将 *[Windows Phone 8 模拟器连接到本地计算机上的 WEB Api 应用程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的说明设置测试环境。</span><span class="sxs-lookup"><span data-stu-id="e0b97-117">If you are going to test the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a><span data-ttu-id="e0b97-118">步骤1：创建 Web API 书店项目</span><span class="sxs-lookup"><span data-stu-id="e0b97-118">Step 1: Creating the Web API Bookstore Project</span></span>

<span data-ttu-id="e0b97-119">本端到端教程的第一步是创建一个支持所有 CRUD 操作的 Web API 项目;请注意，你将在本教程的[第2步](#STEP2)中将 Windows Phone 应用程序项目添加到此解决方案。</span><span class="sxs-lookup"><span data-stu-id="e0b97-119">The first step of this end-to-end tutorial is to create a Web API project that supports all of the CRUD operations; note that you will add the Windows Phone application project to this solution in [Step 2](#STEP2) of this tutorial.</span></span>

1. <span data-ttu-id="e0b97-120">打开**Visual Studio 2013**。</span><span class="sxs-lookup"><span data-stu-id="e0b97-120">Open **Visual Studio 2013**.</span></span>
2. <span data-ttu-id="e0b97-121">依次单击 "**文件**"、"**新建**"、"**项目**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-121">Click **File**, then **New**, and then **Project**.</span></span>
3. <span data-ttu-id="e0b97-122">显示 "**新建项目**" 对话框时，依次展开 "**已安装**"、"**模板**"、" **C#Visual**" 和 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-122">When the **New Project** dialog box is displayed, expand **Installed**, then **Templates**, then **Visual C#**, and then **Web**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="e0b97-123">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-123">Click image to expand</span></span>                                                                |

4. <span data-ttu-id="e0b97-124">突出显示 " **ASP.NET Web 应用程序**"，输入**书店**作为项目名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="e0b97-124">Highlight **ASP.NET Web Application**, enter **BookStore** for the project name, and then click **OK**.</span></span>
5. <span data-ttu-id="e0b97-125">在 "**新建 ASP.NET 项目**" 对话框出现时，选择 " **Web API** " 模板，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="e0b97-125">When the **New ASP.NET Project** dialog box is displayed, select the **Web API** template, and then click **OK**.</span></span>

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                <span data-ttu-id="e0b97-126">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-126">Click image to expand</span></span>                                                                |

6. <span data-ttu-id="e0b97-127">当 Web API 项目打开时，从项目中删除示例控制器：</span><span class="sxs-lookup"><span data-stu-id="e0b97-127">When the Web API project opens, remove the sample controller from the project:</span></span>

    1. <span data-ttu-id="e0b97-128">展开 "解决方案资源管理器" 中的 "**控制器**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e0b97-128">Expand the **Controllers** folder in the solution explorer.</span></span>
    2. <span data-ttu-id="e0b97-129">右键单击 " **ValuesController.cs** " 文件，然后单击 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-129">Right-click the **ValuesController.cs** file, and then click **Delete**.</span></span>
    3. <span data-ttu-id="e0b97-130">系统提示确认删除时，单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="e0b97-130">Click **OK** when prompted to confirm the deletion.</span></span>
7. <span data-ttu-id="e0b97-131">将 XML 数据文件添加到 Web API 项目;此文件包含书店目录的内容：</span><span class="sxs-lookup"><span data-stu-id="e0b97-131">Add an XML data file to the Web API project; this file contains the contents of the bookstore catalog:</span></span>

   1. <span data-ttu-id="e0b97-132">在 "解决方案资源管理器" 中右键单击**应用\_Data**文件夹，然后单击 "**添加**"，然后单击 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-132">Right-click the **App\_Data** folder in the solution explorer, then click **Add**, and then click **New Item**.</span></span>
   2. <span data-ttu-id="e0b97-133">当显示 "**添加新项**" 对话框时，突出显示**XML 文件**模板。</span><span class="sxs-lookup"><span data-stu-id="e0b97-133">When the **Add New Item** dialog box is displayed, highlight the **XML File** template.</span></span>
   3. <span data-ttu-id="e0b97-134">将文件命名为**books.xml**，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-134">Name the file **Books.xml**, and then click **Add**.</span></span>
   4. <span data-ttu-id="e0b97-135">打开**books.xml**文件后，将文件中的代码替换为 MSDN 上的示例**books.xml**文件中的 xml：</span><span class="sxs-lookup"><span data-stu-id="e0b97-135">When the **Books.xml** file is opened, replace the code in the file with the XML from the sample **books.xml** file on MSDN:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. <span data-ttu-id="e0b97-136">保存并关闭该 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-136">Save and close the XML file.</span></span>

8. <span data-ttu-id="e0b97-137">将书店模型添加到 Web API 项目;此模型包含书店应用程序的创建、读取、更新和删除（CRUD）逻辑：</span><span class="sxs-lookup"><span data-stu-id="e0b97-137">Add the bookstore model to the Web API project; this model contains the Create, Read, Update, and Delete (CRUD) logic for the bookstore application:</span></span>

   1. <span data-ttu-id="e0b97-138">在 "解决方案资源管理器" 中，右键单击 "**模型**" 文件夹，单击 "**添加**"，然后单击 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-138">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   2. <span data-ttu-id="e0b97-139">显示 "**添加新项**" 对话框时，将类文件命名为 " **BookDetails.cs**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-139">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   3. <span data-ttu-id="e0b97-140">打开**BookDetails.cs**文件时，将文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e0b97-140">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. <span data-ttu-id="e0b97-141">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-141">Save and close the **BookDetails.cs** file.</span></span>

9. <span data-ttu-id="e0b97-142">将书店控制器添加到 Web API 项目：</span><span class="sxs-lookup"><span data-stu-id="e0b97-142">Add the bookstore controller to the Web API project:</span></span>

   1. <span data-ttu-id="e0b97-143">右键单击 "解决方案资源管理器" 中的 "**控制器**" 文件夹，然后单击 "**添加**"，然后单击 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-143">Right-click the **Controllers** folder in the solution explorer, then click **Add**, and then click **Controller**.</span></span>
   2. <span data-ttu-id="e0b97-144">显示 "**添加基架**" 对话框时，突出显示 " **Web API 2 控制器-空**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-144">When the **Add Scaffold** dialog box is displayed, highlight **Web API 2 Controller - Empty**, and then click **Add**.</span></span>
   3. <span data-ttu-id="e0b97-145">显示 "**添加控制器**" 对话框后，将控制器命名为 " **BooksController**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-145">When the **Add Controller** dialog box is displayed, name the controller **BooksController**, and then click **Add**.</span></span>
   4. <span data-ttu-id="e0b97-146">打开**BooksController.cs**文件时，将文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e0b97-146">When the **BooksController.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. <span data-ttu-id="e0b97-147">保存并关闭**BooksController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-147">Save and close the **BooksController.cs** file.</span></span>

10. <span data-ttu-id="e0b97-148">生成 Web API 应用程序以检查是否有错误。</span><span class="sxs-lookup"><span data-stu-id="e0b97-148">Build the Web API application to check for errors.</span></span>

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a><span data-ttu-id="e0b97-149">步骤2：添加 Windows Phone 8 书店目录项目</span><span class="sxs-lookup"><span data-stu-id="e0b97-149">Step 2: Adding the Windows Phone 8 Bookstore Catalog Project</span></span>

<span data-ttu-id="e0b97-150">此端到端方案的下一步是为 Windows Phone 8 创建目录应用程序。</span><span class="sxs-lookup"><span data-stu-id="e0b97-150">The next step of this end-to-end scenario is to create the catalog application for Windows Phone 8.</span></span> <span data-ttu-id="e0b97-151">此应用程序将使用默认用户界面的*Windows Phone 数据绑定应用*程序模板，它将使用在本教程的[第1步](#STEP1)中创建的 Web API 应用程序作为数据源。</span><span class="sxs-lookup"><span data-stu-id="e0b97-151">This application will use the *Windows Phone Databound App* template for the default user interface, and it will use the Web API application that you created in [Step 1](#STEP1) of this tutorial as the data source.</span></span>

1. <span data-ttu-id="e0b97-152">右键单击 "解决方案资源管理器" 中的 "**书店**解决方案"，然后依次单击 "**添加**" 和 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-152">Right-click the **BookStore** solution in the in the solution explorer, then click **Add**, and then **New Project**.</span></span>
2. <span data-ttu-id="e0b97-153">显示 "**新建项目**" 对话框时，依次展开 "**已安装**" 和 " **C#Visual**"，然后**Windows Phone**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-153">When the **New Project** dialog box is displayed, expand **Installed**, then **Visual C#**, and then **Windows Phone**.</span></span>
3. <span data-ttu-id="e0b97-154">突出显示**Windows Phone 的数据绑定应用程序**，输入 " **BookCatalog** " 作为名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="e0b97-154">Highlight **Windows Phone Databound App**, enter **BookCatalog** for the name, and then click **OK**.</span></span>
4. <span data-ttu-id="e0b97-155">将 Json.NET NuGet 包添加到**BookCatalog**项目：</span><span class="sxs-lookup"><span data-stu-id="e0b97-155">Add the Json.NET NuGet package to the **BookCatalog** project:</span></span>

    1. <span data-ttu-id="e0b97-156">在 "解决方案资源管理器" 中，右键单击**BookCatalog**项目的 "**引用**"，然后单击 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-156">Right-click **References** for the **BookCatalog** project in the solution explorer, and then click **Manage NuGet Packages**.</span></span>
    2. <span data-ttu-id="e0b97-157">当显示 "**管理 NuGet 包**" 对话框时，展开 "**联机**" 部分，然后突出显示 " **nuget.org**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-157">When the **Manage NuGet Packages** dialog box is displayed, expand the **Online** section, and highlight **nuget.org**.</span></span>
    3. <span data-ttu-id="e0b97-158">在搜索字段中输入**Json.NET** ，然后单击搜索图标。</span><span class="sxs-lookup"><span data-stu-id="e0b97-158">Enter **Json.NET** in the search field and click the search icon.</span></span>
    4. <span data-ttu-id="e0b97-159">突出显示搜索结果中的**Json.NET** ，然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-159">Highlight **Json.NET** in the search results, and then click **Install**.</span></span>
    5. <span data-ttu-id="e0b97-160">安装完成后，单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-160">When the installation has completed, click **Close**.</span></span>
5. <span data-ttu-id="e0b97-161">将**BookDetails**模型添加到**BookCatalog**项目;这包含书店类的通用模型：</span><span class="sxs-lookup"><span data-stu-id="e0b97-161">Add the **BookDetails** model to the **BookCatalog** project; this contains a generic model of the bookstore class:</span></span>

   1. <span data-ttu-id="e0b97-162">右键单击解决方案资源管理器中的**BookCatalog**项目，然后单击 "**添加**"，然后单击 "**新建文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-162">Right-click the **BookCatalog** project in the solution explorer, then click **Add**, and then click **New Folder**.</span></span>
   2. <span data-ttu-id="e0b97-163">命名新文件夹**模型**。</span><span class="sxs-lookup"><span data-stu-id="e0b97-163">Name the new folder **Models**.</span></span>
   3. <span data-ttu-id="e0b97-164">在 "解决方案资源管理器" 中，右键单击 "**模型**" 文件夹，单击 "**添加**"，然后单击 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-164">Right-click the **Models** folder in the solution explorer, then click **Add**, and then click **Class**.</span></span>
   4. <span data-ttu-id="e0b97-165">显示 "**添加新项**" 对话框时，将类文件命名为 " **BookDetails.cs**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="e0b97-165">When the **Add New Item** dialog box is displayed, name the class file **BookDetails.cs**, and then click **Add**.</span></span>
   5. <span data-ttu-id="e0b97-166">打开**BookDetails.cs**文件时，将文件中的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e0b97-166">When the **BookDetails.cs** file is opened, replace the code in the file with the following:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. <span data-ttu-id="e0b97-167">保存并关闭**BookDetails.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-167">Save and close the **BookDetails.cs** file.</span></span>

6. <span data-ttu-id="e0b97-168">更新**MainViewModel.cs**类，使其包含与书店 Web API 应用程序通信的功能：</span><span class="sxs-lookup"><span data-stu-id="e0b97-168">Update the **MainViewModel.cs** class to include the functionality to communicate with the BookStore Web API application:</span></span>

   1. <span data-ttu-id="e0b97-169">展开 "解决方案资源管理器" 中的**viewmodel**文件夹，然后双击**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-169">Expand the **ViewModels** folder in the solution explorer, and then double-click the **MainViewModel.cs** file.</span></span>
   2. <span data-ttu-id="e0b97-170">在打开**MainViewModel.cs**文件时，将文件中的代码替换为以下代码：请注意，需要将 `apiUrl` 常量的值更新为你的 Web API 的实际 URL：</span><span class="sxs-lookup"><span data-stu-id="e0b97-170">When the **MainViewModel.cs** file is opened, replace the code in the file with the following; note that you will need to update the value of the `apiUrl` constant with the actual URL of your Web API:</span></span> 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. <span data-ttu-id="e0b97-171">保存并关闭**MainViewModel.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-171">Save and close the **MainViewModel.cs** file.</span></span>

7. <span data-ttu-id="e0b97-172">更新**MainPage**文件以自定义应用程序名称：</span><span class="sxs-lookup"><span data-stu-id="e0b97-172">Update the **MainPage.xaml** file to customize the application name:</span></span>

   1. <span data-ttu-id="e0b97-173">双击 "解决方案资源管理器" 中的**MainPage**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-173">Double-click the **MainPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="e0b97-174">在打开**MainPage**文件时，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="e0b97-174">When the **MainPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. <span data-ttu-id="e0b97-175">将这些行替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e0b97-175">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. <span data-ttu-id="e0b97-176">保存并关闭**MainPage**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-176">Save and close the **MainPage.xaml** file.</span></span>

8. <span data-ttu-id="e0b97-177">更新**DetailsPage**文件以自定义显示的项：</span><span class="sxs-lookup"><span data-stu-id="e0b97-177">Update the **DetailsPage.xaml** file to customize the displayed items:</span></span>

   1. <span data-ttu-id="e0b97-178">双击 "解决方案资源管理器" 中的**DetailsPage**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-178">Double-click the **DetailsPage.xaml** file in the solution explorer.</span></span>
   2. <span data-ttu-id="e0b97-179">在打开**DetailsPage**文件时，找到以下代码行：</span><span class="sxs-lookup"><span data-stu-id="e0b97-179">When the **DetailsPage.xaml** file is opened, locate the following lines of code:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. <span data-ttu-id="e0b97-180">将这些行替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e0b97-180">Replace those lines with the following:</span></span> 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. <span data-ttu-id="e0b97-181">保存并关闭**DetailsPage**文件。</span><span class="sxs-lookup"><span data-stu-id="e0b97-181">Save and close the **DetailsPage.xaml** file.</span></span>

9. <span data-ttu-id="e0b97-182">构建 Windows Phone 应用程序以检查是否有错误。</span><span class="sxs-lookup"><span data-stu-id="e0b97-182">Build the Windows Phone application to check for errors.</span></span>

### <a name="step-3-testing-the-end-to-end-solution"></a><span data-ttu-id="e0b97-183">步骤3：测试端到端解决方案</span><span class="sxs-lookup"><span data-stu-id="e0b97-183">Step 3: Testing the End-to-End Solution</span></span>

<span data-ttu-id="e0b97-184">如本教程的 "*先决条件*" 部分中所述，当你在本地系统上测试 Web API 与 Windows Phone 8 项目之间的连接时，你将需要按照将 *[Windows Phone 8 仿真程序连接到本地计算机上的 Web api 应用程序](https://go.microsoft.com/fwlink/?LinkId=324014)* 一文中的说明设置你的测试环境。</span><span class="sxs-lookup"><span data-stu-id="e0b97-184">As mentioned in the *Prerequisites* section of this tutorial, when you are testing the connectivity between Web API and Windows Phone 8 projects on your local system, you will need to follow the instructions in the *[Connecting the Windows Phone 8 Emulator to Web API Applications on a Local Computer](https://go.microsoft.com/fwlink/?LinkId=324014)* article to set up your testing environment.</span></span>

<span data-ttu-id="e0b97-185">配置测试环境后，需要将 Windows Phone 应用程序设置为启动项目。</span><span class="sxs-lookup"><span data-stu-id="e0b97-185">Once you have the testing environment configured, you will need to set the Windows Phone application as the startup project.</span></span> <span data-ttu-id="e0b97-186">为此，请在 "解决方案资源管理器" 中突出显示**BookCatalog**应用程序，然后单击 "**设为启动项目**"：</span><span class="sxs-lookup"><span data-stu-id="e0b97-186">To do so, highlight the **BookCatalog** application in the solution explorer, and then click **Set as StartUp Project**:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| <span data-ttu-id="e0b97-187">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-187">Click image to expand</span></span> |

<span data-ttu-id="e0b97-188">按 F5 时，Visual Studio 将启动 Windows Phone 模拟器，这将显示 &quot;请等待&quot; 消息，同时从 Web API 检索应用程序数据：</span><span class="sxs-lookup"><span data-stu-id="e0b97-188">When you press F5, Visual Studio will start both the Windows Phone Emulator, which will display a &quot;Please Wait&quot; message while the application data is retrieved from your Web API:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| <span data-ttu-id="e0b97-189">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-189">Click image to expand</span></span> |

<span data-ttu-id="e0b97-190">如果一切成功，应会看到目录显示：</span><span class="sxs-lookup"><span data-stu-id="e0b97-190">If everything is successful, you should see the catalog displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| <span data-ttu-id="e0b97-191">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-191">Click image to expand</span></span> |

<span data-ttu-id="e0b97-192">如果点击任何书籍标题，应用程序会显示书籍说明：</span><span class="sxs-lookup"><span data-stu-id="e0b97-192">If you tap on any book title, the application will display the book description:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| <span data-ttu-id="e0b97-193">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-193">Click image to expand</span></span> |

<span data-ttu-id="e0b97-194">如果应用程序无法与 Web API 通信，则将显示一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="e0b97-194">If the application cannot communicate with your Web API, an error message will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| <span data-ttu-id="e0b97-195">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-195">Click image to expand</span></span> |

<span data-ttu-id="e0b97-196">如果点击错误消息，将显示有关错误的任何其他详细信息：</span><span class="sxs-lookup"><span data-stu-id="e0b97-196">If you tap on the error message, any additional details about the error will be displayed:</span></span>

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 <span data-ttu-id="e0b97-197">单击图像进行扩展</span><span class="sxs-lookup"><span data-stu-id="e0b97-197">Click image to expand</span></span>                                                                 |
