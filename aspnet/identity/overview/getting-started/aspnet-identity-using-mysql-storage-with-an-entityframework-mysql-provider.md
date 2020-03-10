---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ASP.NET Identity：将 MySQL 存储用于 EntityFramework MySQL 提供程序（C#）-ASP.NET 4。x
author: maumar
description: 本教程介绍如何使用 EntityFramework （SQL 客户端提供程序）将用于 ASP.NET Identity 的默认数据存储机制替换为 MySQL 签约 。
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471872"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a><span data-ttu-id="f06f4-103">ASP.NET Identity：将 MySQL 存储用于 EntityFramework MySQL 提供程序（C#）</span><span class="sxs-lookup"><span data-stu-id="f06f4-103">ASP.NET Identity: Using MySQL Storage with an EntityFramework MySQL Provider (C#)</span></span>

<span data-ttu-id="f06f4-104">作者： [Maurycy Markowski](https://github.com/maumar)， [Raquel Soares De Almeida](https://github.com/raquelsa)， [Robert mcmurray 有关](https://github.com/rmcmurray)</span><span class="sxs-lookup"><span data-stu-id="f06f4-104">by [Maurycy Markowski](https://github.com/maumar), [Raquel Soares De Almeida](https://github.com/raquelsa), [Robert McMurray](https://github.com/rmcmurray)</span></span>

> <span data-ttu-id="f06f4-105">本教程介绍如何使用 EntityFramework （SQL 客户端提供程序）将[**ASP.NET Identity**](introduction-to-aspnet-identity.md)的默认数据存储机制替换为 MySQL 提供程序。</span><span class="sxs-lookup"><span data-stu-id="f06f4-105">This tutorial shows you how to replace the default data storage mechanism for [**ASP.NET Identity**](introduction-to-aspnet-identity.md) with EntityFramework (SQL client provider) with a MySQL provider.</span></span>

<span data-ttu-id="f06f4-106">本教程将介绍以下主题：</span><span class="sxs-lookup"><span data-stu-id="f06f4-106">The following topics will be covered in this tutorial:</span></span>

- <span data-ttu-id="f06f4-107">在 Azure 上创建 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="f06f4-107">Creating a MySQL database on Azure</span></span>
- <span data-ttu-id="f06f4-108">使用 Visual Studio 2013 MVC 模板创建 MVC 应用程序</span><span class="sxs-lookup"><span data-stu-id="f06f4-108">Creating an MVC application using Visual Studio 2013 MVC template</span></span>
- <span data-ttu-id="f06f4-109">将 EntityFramework 配置为使用 MySQL 数据库提供程序</span><span class="sxs-lookup"><span data-stu-id="f06f4-109">Configuring EntityFramework to work with a MySQL database provider</span></span>
- <span data-ttu-id="f06f4-110">运行应用程序以验证结果</span><span class="sxs-lookup"><span data-stu-id="f06f4-110">Running the application to verify the results</span></span>

<span data-ttu-id="f06f4-111">在本教程结束时，将拥有一个 MVC 应用程序，其中包含使用 Azure 中托管的 MySQL 数据库的 ASP.NET Identity 存储。</span><span class="sxs-lookup"><span data-stu-id="f06f4-111">At the end of this tutorial, you will have an MVC application with the ASP.NET Identity store that is using a MySQL database that is hosted in Azure.</span></span>

## <a name="creating-a-mysql-database-instance-on-azure"></a><span data-ttu-id="f06f4-112">在 Azure 上创建 MySQL 数据库实例</span><span class="sxs-lookup"><span data-stu-id="f06f4-112">Creating a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="f06f4-113">登录到 [Azure 门户](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="f06f4-113">Log in to the [Azure Portal](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409).</span></span>
2. <span data-ttu-id="f06f4-114">单击页面底部的 "**新建**"，然后选择 "**存储**"：</span><span class="sxs-lookup"><span data-stu-id="f06f4-114">Click **NEW** at the bottom of the page, and then select **STORE**:</span></span>

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. <span data-ttu-id="f06f4-115">在 "**选择和外接程序**" 向导中，选择 " **ClearDB MySQL 数据库**"，然后单击框架底部的 "**下一步**" 箭头：</span><span class="sxs-lookup"><span data-stu-id="f06f4-115">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database**, and then click the **Next** arrow at the bottom of the frame:</span></span>

   <span data-ttu-id="f06f4-116">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-116">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-117">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-117">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)</span></span>
4. <span data-ttu-id="f06f4-118">保留默认的 "**免费**计划"，将**名称**更改为**IdentityMySQLDatabase**，选择离你最近的区域，然后单击框架底部的**下一步**箭头：</span><span class="sxs-lookup"><span data-stu-id="f06f4-118">Keep the default **Free** plan, change the **NAME** to **IdentityMySQLDatabase**, select the region that is nearest to you, and then click the **Next** arrow at the bottom of the frame:</span></span>

   <span data-ttu-id="f06f4-119">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-119">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-120">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-120">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)</span></span>
5. <span data-ttu-id="f06f4-121">单击 "**购买**" 复选标记以完成数据库创建。</span><span class="sxs-lookup"><span data-stu-id="f06f4-121">Click the **PURCHASE** checkmark to complete the database creation.</span></span>

   <span data-ttu-id="f06f4-122">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-122">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-123">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-123">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)</span></span>
6. <span data-ttu-id="f06f4-124">在创建数据库后，可以从管理门户中的“外接程序”选项卡管理该数据库。</span><span class="sxs-lookup"><span data-stu-id="f06f4-124">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span> <span data-ttu-id="f06f4-125">若要检索数据库的连接信息，请单击页面底部的 "**连接信息**"：</span><span class="sxs-lookup"><span data-stu-id="f06f4-125">To retrieve the connection information for your database, click **CONNECTION INFO** at the bottom of the page:</span></span>

   <span data-ttu-id="f06f4-126">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-126">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-127">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-127">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)</span></span>
7. <span data-ttu-id="f06f4-128">通过单击**CONNECTIONSTRING**字段的复制按钮并保存来复制连接字符串;稍后在本教程中，你将在 MVC 应用程序中使用此信息：</span><span class="sxs-lookup"><span data-stu-id="f06f4-128">Copy the connection string by clicking on the copy button by the **CONNECTIONSTRING** field and save it; you will use this information later in this tutorial for your MVC application:</span></span>

   <span data-ttu-id="f06f4-129">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-129">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-130">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-130">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)</span></span>

## <a name="creating-an-mvc-application-project"></a><span data-ttu-id="f06f4-131">创建 MVC 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="f06f4-131">Creating an MVC application project</span></span>

<span data-ttu-id="f06f4-132">若要完成本教程的此部分中的步骤，首先需要安装[Visual Studio Express 2013 For Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。</span><span class="sxs-lookup"><span data-stu-id="f06f4-132">To complete the steps in this section of the tutorial, you will first need to install [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566).</span></span> <span data-ttu-id="f06f4-133">安装 Visual Studio 后，请使用以下步骤创建新的 MVC 应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="f06f4-133">Once Visual Studio has been installed, use the following steps to create a new MVC application project:</span></span>

1. <span data-ttu-id="f06f4-134">打开 Visual Studio 2103。</span><span class="sxs-lookup"><span data-stu-id="f06f4-134">Open Visual Studio 2103.</span></span>
2. <span data-ttu-id="f06f4-135">在**起始**页上单击 "**新建项目**"，或者单击 "**文件**" 菜单，然后单击 "**新建项目**"：</span><span class="sxs-lookup"><span data-stu-id="f06f4-135">Click **New Project** from the **Start** page, or you can click the **File** menu and then **New Project**:</span></span>

   <span data-ttu-id="f06f4-136">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-136">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-137">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)</span><span class="sxs-lookup"><span data-stu-id="f06f4-137">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)</span></span>
3. <span data-ttu-id="f06f4-138">当显示 "**新建项目**" 对话框时，展开模板列表中的 "**视觉C#对象**"，然后单击 " **web**"，然后选择 " **ASP.NET Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="f06f4-138">When the **New Project** dialog box is displayed, expand **Visual C#** in the list of templates, then click **Web**, and select **ASP.NET Web Application**.</span></span> <span data-ttu-id="f06f4-139">将项目命名为 " **IdentityMySQLDemo** "，然后单击 **"确定"** ：</span><span class="sxs-lookup"><span data-stu-id="f06f4-139">Name your project **IdentityMySQLDemo** and then click **OK**:</span></span>

   <span data-ttu-id="f06f4-140">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-140">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-141">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-141">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)</span></span>
4. <span data-ttu-id="f06f4-142">在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC** templatewith" 默认选项;这会将**各个用户帐户**配置为身份验证方法。</span><span class="sxs-lookup"><span data-stu-id="f06f4-142">In the **New ASP.NET Project** dialog, select the **MVC** templatewith the default options; this will configure **Individual User Accounts** as the authentication method.</span></span> <span data-ttu-id="f06f4-143">单击“确定”：</span><span class="sxs-lookup"><span data-stu-id="f06f4-143">Click **OK**:</span></span>

   <span data-ttu-id="f06f4-144">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-144">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-145">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-145">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)</span></span>

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a><span data-ttu-id="f06f4-146">将 EntityFramework 配置为使用 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="f06f4-146">Configure EntityFramework to work with a MySQL database</span></span>

### <a name="update-the-entity-framework-assembly-for-your-project"></a><span data-ttu-id="f06f4-147">更新项目的实体框架程序集</span><span class="sxs-lookup"><span data-stu-id="f06f4-147">Update the Entity Framework assembly for your project</span></span>

<span data-ttu-id="f06f4-148">从 Visual Studio 2013 模板创建的 MVC 应用程序包含对[EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework)包的引用，但由于该程序集的版本包含显著的性能改进，因此对该程序集进行了更新。</span><span class="sxs-lookup"><span data-stu-id="f06f4-148">The MVC application that was created from the Visual Studio 2013 template contains a reference to the [EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework) package, but there have been updates to that assembly since its release which contain significant performance improvements.</span></span> <span data-ttu-id="f06f4-149">若要在应用程序中使用这些最新的更新，请使用以下步骤。</span><span class="sxs-lookup"><span data-stu-id="f06f4-149">In order to use these latest updates in your application, use the following steps.</span></span>

1. <span data-ttu-id="f06f4-150">在 Visual Studio 中打开 MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="f06f4-150">Open your MVC project in Visual Studio.</span></span>
2. <span data-ttu-id="f06f4-151">单击 "**工具**"，然后单击 " **NuGet 程序包管理器**"，然后单击 "**程序包管理器控制台**"：</span><span class="sxs-lookup"><span data-stu-id="f06f4-151">Click **Tools**, then click **NuGet Package Manager**, and then click **Package Manager Console**:</span></span>

   <span data-ttu-id="f06f4-152">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-152">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-153">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-153">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)</span></span>
3. <span data-ttu-id="f06f4-154">**程序包管理器控制台**将显示在 Visual Studio 的底部。</span><span class="sxs-lookup"><span data-stu-id="f06f4-154">The **Package Manager Console** will appear in the bottom section of Visual Studio.</span></span> <span data-ttu-id="f06f4-155">键入 &quot;**更新-Package EntityFramework**&quot; 并按 enter：</span><span class="sxs-lookup"><span data-stu-id="f06f4-155">Type &quot;**Update-Package EntityFramework**&quot; and press Enter:</span></span>

   <span data-ttu-id="f06f4-156">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-156">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-157">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-157">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)</span></span>

### <a name="install-the-mysql-provider-for-entityframework"></a><span data-ttu-id="f06f4-158">安装适用于 EntityFramework 的 MySQL 提供程序</span><span class="sxs-lookup"><span data-stu-id="f06f4-158">Install the MySQL provider for EntityFramework</span></span>

<span data-ttu-id="f06f4-159">为了使 EntityFramework 能够连接到 MySQL 数据库，需要安装 MySQL 提供程序。</span><span class="sxs-lookup"><span data-stu-id="f06f4-159">In order for EntityFramework to connect to MySQL database, you need to install a MySQL provider.</span></span> <span data-ttu-id="f06f4-160">为此，请打开 "**程序包管理器控制台**"，然后键入 &quot;**安装-Package MySql.** &quot;，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="f06f4-160">To do so, open the **Package Manager Console** and type &quot;**Install-Package MySql.Data.Entity -Pre**&quot;, and then press Enter.</span></span>

> [!NOTE]
> <span data-ttu-id="f06f4-161">这是程序集的预发布版本，因此它可能包含 bug。</span><span class="sxs-lookup"><span data-stu-id="f06f4-161">This is a pre-release version of the assembly, and as such it may contain bugs.</span></span> <span data-ttu-id="f06f4-162">不应在生产中使用提供程序的预发布版本。</span><span class="sxs-lookup"><span data-stu-id="f06f4-162">You should not use a pre-release version of the provider in production.</span></span>

<span data-ttu-id="f06f4-163">[单击下图以将其展开。]</span><span class="sxs-lookup"><span data-stu-id="f06f4-163">[Click the following image to expand it.]</span></span>

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a><span data-ttu-id="f06f4-164">对应用程序的 web.config 文件进行项目配置更改</span><span class="sxs-lookup"><span data-stu-id="f06f4-164">Making project configuration changes to the Web.config file for your application</span></span>

<span data-ttu-id="f06f4-165">在本部分中，你将配置实体框架以使用刚刚安装的 MySQL 提供程序，注册 MySQL 提供程序工厂，并添加 Azure 中的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f06f4-165">In this section you will configure the Entity Framework to use the MySQL provider that you just installed, register the MySQL provider factory, and add your connection string from Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="f06f4-166">下面的示例包含用于 MySql 的特定程序集版本。</span><span class="sxs-lookup"><span data-stu-id="f06f4-166">The following examples contain a specific assembly version for MySql.Data.dll.</span></span> <span data-ttu-id="f06f4-167">如果程序集版本发生更改，你将需要修改版本正确的适当配置设置。</span><span class="sxs-lookup"><span data-stu-id="f06f4-167">If the assembly version changes, you will need to modify the appropriate configuration settings with the correct version.</span></span>

1. <span data-ttu-id="f06f4-168">在 Visual Studio 2013 中打开项目的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="f06f4-168">Open the Web.config file for your project in Visual Studio 2013.</span></span>
2. <span data-ttu-id="f06f4-169">找到以下配置设置，这些设置为实体框架定义默认的数据库提供程序和工厂：</span><span class="sxs-lookup"><span data-stu-id="f06f4-169">Locate the following configuration settings, which define the default database provider and factory for the Entity Framework:</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. <span data-ttu-id="f06f4-170">将这些配置设置替换为以下内容，这会将实体框架配置为使用 MySQL 提供程序：</span><span class="sxs-lookup"><span data-stu-id="f06f4-170">Replace those configuration settings with the following, which will configure the Entity Framework to use the MySQL provider:</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. <span data-ttu-id="f06f4-171">找到 &lt;connectionStrings&gt; 部分，并将其替换为以下代码，此代码将定义托管在 Azure 上的 MySQL 数据库的连接字符串（请注意，providerName 值也已从原始值更改）：</span><span class="sxs-lookup"><span data-stu-id="f06f4-171">Locate the &lt;connectionStrings&gt; section and replace it with the following code, which will define the connection string for your MySQL database that is hosted on Azure (note that providerName value has also been changed from the original):</span></span>

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a><span data-ttu-id="f06f4-172">添加自定义 MigrationHistory 上下文</span><span class="sxs-lookup"><span data-stu-id="f06f4-172">Adding custom MigrationHistory context</span></span>

<span data-ttu-id="f06f4-173">实体框架 Code First 使用**MigrationHistory**表跟踪模型更改，并确保数据库架构和概念架构之间的一致性。</span><span class="sxs-lookup"><span data-stu-id="f06f4-173">Entity Framework Code First uses a **MigrationHistory** table to keep track of model changes and to ensure the consistency between the database schema and conceptual schema.</span></span> <span data-ttu-id="f06f4-174">但是，默认情况下，此表不适用于 MySQL，因为主密钥太大。</span><span class="sxs-lookup"><span data-stu-id="f06f4-174">However, this table does not work for MySQL by default because the primary key is too large.</span></span> <span data-ttu-id="f06f4-175">若要纠正这种情况，需要为该表缩减密钥大小。</span><span class="sxs-lookup"><span data-stu-id="f06f4-175">To remedy this situation, you will need to shrink the key size for that table.</span></span> <span data-ttu-id="f06f4-176">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="f06f4-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="f06f4-177">此表的架构信息是在**HistoryContext**中捕获的，可以将其修改为任何其他**DbContext**。</span><span class="sxs-lookup"><span data-stu-id="f06f4-177">The schema information for this table is captured in a **HistoryContext**, which can be modified as any other **DbContext**.</span></span> <span data-ttu-id="f06f4-178">为此，请将名为**MySqlHistoryContext.cs**的新类文件添加到项目中，并将其内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f06f4-178">To do so, add a new class file named **MySqlHistoryContext.cs** to the project, and replace its contents with the following code:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. <span data-ttu-id="f06f4-179">接下来，需要将实体框架配置为使用修改后的**HistoryContext**而不是默认值。</span><span class="sxs-lookup"><span data-stu-id="f06f4-179">Next you will need to configure Entity Framework to use the modified **HistoryContext**, rather than default one.</span></span> <span data-ttu-id="f06f4-180">这可以通过使用基于代码的配置功能来实现。</span><span class="sxs-lookup"><span data-stu-id="f06f4-180">This can be done by leveraging code-based configuration features.</span></span> <span data-ttu-id="f06f4-181">为此，请将名为**MySqlConfiguration.cs**的新类文件添加到项目中，并将其内容替换为：</span><span class="sxs-lookup"><span data-stu-id="f06f4-181">To do so, add new class file named **MySqlConfiguration.cs** to your project and replace its contents with:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a><span data-ttu-id="f06f4-182">为 ApplicationDbContext 创建自定义 EntityFramework 初始值设定项</span><span class="sxs-lookup"><span data-stu-id="f06f4-182">Creating a custom EntityFramework initializer for ApplicationDbContext</span></span>

<span data-ttu-id="f06f4-183">本教程中介绍的 MySQL 提供程序当前不支持实体框架迁移，因此你需要使用模型初始值设定项来连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="f06f4-183">The MySQL provider that is featured in this tutorial does not currently support Entity Framework migrations, so you will need to use model initializers in order to connect to the database.</span></span> <span data-ttu-id="f06f4-184">由于本教程使用的是 Azure 上的 MySQL 实例，因此你将需要创建一个自定义实体框架初始值设定项。</span><span class="sxs-lookup"><span data-stu-id="f06f4-184">Because this tutorial is using a MySQL instance on Azure, you will need to create a custom Entity Framework initializer.</span></span>

> [!NOTE]
> <span data-ttu-id="f06f4-185">如果要连接到 Azure 上的 SQL Server 实例，或者使用在本地托管的数据库，则不需要执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="f06f4-185">This step is not required if you are connecting to a SQL Server instance on Azure or if you are using a database that is hosted on premises.</span></span>

<span data-ttu-id="f06f4-186">若要为 MySQL 创建自定义实体框架初始值设定项，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="f06f4-186">To create a custom Entity Framework initializer for MySQL, use the following steps:</span></span>

1. <span data-ttu-id="f06f4-187">将名为**MySqlInitializer.cs**的新类文件添加到项目中，并将其内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="f06f4-187">Add a new class file named **MySqlInitializer.cs** to the project, and replace it's contents with the following code:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. <span data-ttu-id="f06f4-188">打开项目的**IdentityModels.cs**文件，该文件位于 "**模型**" 目录中，并将其内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="f06f4-188">Open the **IdentityModels.cs** file for your project, which is located in the **Models** directory, and replace it's contents with the following:</span></span>

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a><span data-ttu-id="f06f4-189">运行应用程序并验证数据库</span><span class="sxs-lookup"><span data-stu-id="f06f4-189">Running the application and verifying the database</span></span>

<span data-ttu-id="f06f4-190">完成前面几节中的步骤后，应测试数据库。</span><span class="sxs-lookup"><span data-stu-id="f06f4-190">Once you have completed the steps in the preceding sections, you should test your database.</span></span> <span data-ttu-id="f06f4-191">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="f06f4-191">To do so, use the following steps:</span></span>

1. <span data-ttu-id="f06f4-192">按**Ctrl + F5**生成并运行 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f06f4-192">Press **Ctrl + F5** to build and run the web application.</span></span>
2. <span data-ttu-id="f06f4-193">单击页面顶部的 "**注册**" 选项卡：</span><span class="sxs-lookup"><span data-stu-id="f06f4-193">Click the **Register** tab on the top of the page:</span></span>

   <span data-ttu-id="f06f4-194">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-194">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-195">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="f06f4-195">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)</span></span>
3. <span data-ttu-id="f06f4-196">输入新用户名和密码，然后单击 "**注册**"：</span><span class="sxs-lookup"><span data-stu-id="f06f4-196">Enter a new user name and password, and then click **Register**:</span></span>

   <span data-ttu-id="f06f4-197">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-197">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-198">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-198">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)</span></span>
4. <span data-ttu-id="f06f4-199">此时，将在 MySQL 数据库上创建 ASP.NET Identity 表，并注册该用户并将其记录到应用程序中：</span><span class="sxs-lookup"><span data-stu-id="f06f4-199">At this point the ASP.NET Identity tables are created on the MySQL Database, and the user is registered and logged into the application:</span></span>

   <span data-ttu-id="f06f4-200">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-200">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-201">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)</span><span class="sxs-lookup"><span data-stu-id="f06f4-201">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)</span></span>

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a><span data-ttu-id="f06f4-202">安装 MySQL 工作台工具以验证数据</span><span class="sxs-lookup"><span data-stu-id="f06f4-202">Installing MySQL Workbench tool to verify the data</span></span>

1. <span data-ttu-id="f06f4-203">从[mysql 下载页面](http://dev.mysql.com/downloads/windows/installer/)安装**mysql 工作台**工具</span><span class="sxs-lookup"><span data-stu-id="f06f4-203">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="f06f4-204">在安装向导中： "**功能选择**" 选项卡上，选择 "**应用程序**" 部分下的**MySQL 工作台**。</span><span class="sxs-lookup"><span data-stu-id="f06f4-204">In the installation wizard: **Feature Selection** tab, select **MySQL Workbench** under **applications** section.</span></span>
3. <span data-ttu-id="f06f4-205">启动应用并使用在本教程的 begging 中创建的 Azure MySQL 数据库中的连接字符串数据添加新连接。</span><span class="sxs-lookup"><span data-stu-id="f06f4-205">Launch the app and add a new connection using the connection string data from the Azure MySQL database you created at the begging of this tutorial.</span></span>
4. <span data-ttu-id="f06f4-206">建立连接后，检查在 IdentityMySQLDatabase 上创建的**ASP.NET Identity**表 **。**</span><span class="sxs-lookup"><span data-stu-id="f06f4-206">After establishing the connection, inspect the **ASP.NET Identity** tables created on the **IdentityMySQLDatabase.**</span></span>
5. <span data-ttu-id="f06f4-207">你将看到，创建了所有 ASP.NET Identity 必需的表，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="f06f4-207">You will see that all ASP.NET Identity required tables are created as shown in the image below:</span></span>

   <span data-ttu-id="f06f4-208">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-208">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-209">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)</span><span class="sxs-lookup"><span data-stu-id="f06f4-209">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)</span></span>
6. <span data-ttu-id="f06f4-210">检查**aspnetusers**表中的实例，以便在注册新用户时检查条目。</span><span class="sxs-lookup"><span data-stu-id="f06f4-210">Inspect the **aspnetusers** table for instance to check for the entries as you register new users.</span></span>

   <span data-ttu-id="f06f4-211">[单击下图以将其展开。</span><span class="sxs-lookup"><span data-stu-id="f06f4-211">[Click the following image to expand it.</span></span> <span data-ttu-id="f06f4-212">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="f06f4-212">] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)</span></span>
