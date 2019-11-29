---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第1部分：概述和创建项目 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600326"
---
# <a name="part-1-overview-and-creating-the-project"></a><span data-ttu-id="144f0-102">第1部分：概述和创建项目</span><span class="sxs-lookup"><span data-stu-id="144f0-102">Part 1: Overview and Creating the Project</span></span>

<span data-ttu-id="144f0-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="144f0-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="144f0-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="144f0-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

<span data-ttu-id="144f0-105">实体框架是对象/关系映射框架。</span><span class="sxs-lookup"><span data-stu-id="144f0-105">Entity Framework is an object/relational mapping framework.</span></span> <span data-ttu-id="144f0-106">它将代码中的域对象映射到关系数据库中的实体。</span><span class="sxs-lookup"><span data-stu-id="144f0-106">It maps the domain objects in your code to entities in a relational database.</span></span> <span data-ttu-id="144f0-107">大多数情况下，你不必担心数据库层，因为实体框架会为你处理此层。</span><span class="sxs-lookup"><span data-stu-id="144f0-107">For the most part, you do not have to worry about the database layer, because Entity Framework takes care of it for you.</span></span> <span data-ttu-id="144f0-108">你的代码将操作这些对象，而更改将保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="144f0-108">Your code manipulates the objects, and changes are persisted to a database.</span></span>

## <a name="about-the-tutorial"></a><span data-ttu-id="144f0-109">关于教程</span><span class="sxs-lookup"><span data-stu-id="144f0-109">About the Tutorial</span></span>

<span data-ttu-id="144f0-110">在本教程中，你将创建一个简单的存储区应用程序。</span><span class="sxs-lookup"><span data-stu-id="144f0-110">In this tutorial, you will create a simple store application.</span></span> <span data-ttu-id="144f0-111">应用程序有两个主要部分。</span><span class="sxs-lookup"><span data-stu-id="144f0-111">There are two main parts to the application.</span></span> <span data-ttu-id="144f0-112">普通用户可以查看产品和创建订单：</span><span class="sxs-lookup"><span data-stu-id="144f0-112">Normal users can view products and create orders:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

<span data-ttu-id="144f0-113">管理员可以创建、删除或编辑产品：</span><span class="sxs-lookup"><span data-stu-id="144f0-113">Administrators can create, delete, or edit products:</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="144f0-114">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="144f0-114">Skills You'll Learn</span></span>

<span data-ttu-id="144f0-115">学习内容：</span><span class="sxs-lookup"><span data-stu-id="144f0-115">Here's what you'll learn:</span></span>

- <span data-ttu-id="144f0-116">如何对 ASP.NET Web API 使用实体框架。</span><span class="sxs-lookup"><span data-stu-id="144f0-116">How to use Entity Framework with ASP.NET Web API.</span></span>
- <span data-ttu-id="144f0-117">如何使用挖空创建动态客户端 UI。</span><span class="sxs-lookup"><span data-stu-id="144f0-117">How to use knockout.js to create a dynamic client UI.</span></span>
- <span data-ttu-id="144f0-118">如何使用 Web API 的 forms 身份验证对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="144f0-118">How to use forms authentication with Web API to authenticate users.</span></span>

<span data-ttu-id="144f0-119">尽管本教程是独立的，但你可能希望先阅读以下教程：</span><span class="sxs-lookup"><span data-stu-id="144f0-119">Although this tutorial is self-contained, you might want to read the following tutorials first:</span></span>

- [<span data-ttu-id="144f0-120">你的第一个 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="144f0-120">Your First ASP.NET Web API</span></span>](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [<span data-ttu-id="144f0-121">创建支持 CRUD 操作的 Web API</span><span class="sxs-lookup"><span data-stu-id="144f0-121">Creating a Web API that Supports CRUD Operations</span></span>](../creating-a-web-api-that-supports-crud-operations.md)

<span data-ttu-id="144f0-122">[ASP.NET MVC](../../../../mvc/index.md)的一些知识也很有用。</span><span class="sxs-lookup"><span data-stu-id="144f0-122">Some knowledge of [ASP.NET MVC](../../../../mvc/index.md) is also helpful.</span></span>

## <a name="overview"></a><span data-ttu-id="144f0-123">概述</span><span class="sxs-lookup"><span data-stu-id="144f0-123">Overview</span></span>

<span data-ttu-id="144f0-124">从较高层次来看，此应用程序的体系结构如下：</span><span class="sxs-lookup"><span data-stu-id="144f0-124">At a high level, here is the architecture of the application:</span></span>

- <span data-ttu-id="144f0-125">ASP.NET MVC 为客户端生成 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="144f0-125">ASP.NET MVC generates the HTML pages for the client.</span></span>
- <span data-ttu-id="144f0-126">ASP.NET Web API 公开对数据（产品和订单）的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="144f0-126">ASP.NET Web API exposes CRUD operations on the data (products and orders).</span></span>
- <span data-ttu-id="144f0-127">实体框架将 Web C# API 使用的模型转换为数据库实体。</span><span class="sxs-lookup"><span data-stu-id="144f0-127">Entity Framework translates the C# models used by Web API into database entities.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

<span data-ttu-id="144f0-128">下图显示了如何在应用程序的各个层上表示域对象：数据库层、对象模型，最后是用于通过 HTTP 将数据传输到客户端的网络格式。</span><span class="sxs-lookup"><span data-stu-id="144f0-128">The following diagram shows how the domain objects are represented at various layers of the application: The database layer, the object model, and finally the wire format, which is used to transmit data to the client via HTTP.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="144f0-129">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="144f0-129">Create the Visual Studio Project</span></span>

<span data-ttu-id="144f0-130">您可以使用 Visual Web Developer Express 或完整版 Visual Studio 创建教程项目。</span><span class="sxs-lookup"><span data-stu-id="144f0-130">You can create the tutorial project using either Visual Web Developer Express or the full version of Visual Studio.</span></span>

<span data-ttu-id="144f0-131">从**起始**页中，单击 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="144f0-131">From the **Start** page, click **New Project**.</span></span>

<span data-ttu-id="144f0-132">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="144f0-132">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="144f0-133">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="144f0-133">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="144f0-134">在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="144f0-134">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="144f0-135">将项目命名为 "ProductStore"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="144f0-135">Name the project "ProductStore" and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

<span data-ttu-id="144f0-136">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**"，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="144f0-136">In the **New ASP.NET MVC 4 Project** dialog, select **Internet Application** and click **OK**.</span></span>

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

<span data-ttu-id="144f0-137">"Internet 应用程序" 模板创建一个支持窗体身份验证的 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="144f0-137">The "Internet Application" template creates an ASP.NET MVC application that supports forms authentication.</span></span> <span data-ttu-id="144f0-138">如果现在运行应用程序，该应用程序已经有一些功能：</span><span class="sxs-lookup"><span data-stu-id="144f0-138">If you run the application now, it already has some features:</span></span>

- <span data-ttu-id="144f0-139">新用户可以通过单击右上角的 "注册" 链接进行注册。</span><span class="sxs-lookup"><span data-stu-id="144f0-139">New users can register by clicking the "Register" link in the upper right corner.</span></span>
- <span data-ttu-id="144f0-140">注册用户可以通过单击 "登录" 链接登录。</span><span class="sxs-lookup"><span data-stu-id="144f0-140">Registered users can log in by clicking the "Log in" link.</span></span>

<span data-ttu-id="144f0-141">成员资格信息保留在自动创建的数据库中。</span><span class="sxs-lookup"><span data-stu-id="144f0-141">Membership information is persisted in a database that gets created automatically.</span></span> <span data-ttu-id="144f0-142">有关 ASP.NET MVC 中 forms 身份验证的详细信息，请参阅[演练：在 ASP.NET mvc 中使用 Forms 身份验证](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="144f0-142">For more information about forms authentication in ASP.NET MVC, see [Walkthrough: Using Forms Authentication in ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).</span></span>

## <a name="update-the-css-file"></a><span data-ttu-id="144f0-143">更新 CSS 文件</span><span class="sxs-lookup"><span data-stu-id="144f0-143">Update the CSS File</span></span>

<span data-ttu-id="144f0-144">此步骤是表面的，但它会使页面呈现为之前的屏幕快照。</span><span class="sxs-lookup"><span data-stu-id="144f0-144">This step is cosmetic, but it will make the pages render like the earlier screen shots.</span></span>

<span data-ttu-id="144f0-145">在解决方案资源管理器中，展开 "Content" 文件夹，然后打开名为 "web.config" 的文件。</span><span class="sxs-lookup"><span data-stu-id="144f0-145">In Solution Explorer, expand the Content folder and open the file named Site.css.</span></span> <span data-ttu-id="144f0-146">添加以下 CSS 样式：</span><span class="sxs-lookup"><span data-stu-id="144f0-146">Add the following CSS styles:</span></span>

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [<span data-ttu-id="144f0-147">下一页</span><span class="sxs-lookup"><span data-stu-id="144f0-147">Next</span></span>](using-web-api-with-entity-framework-part-2.md)
