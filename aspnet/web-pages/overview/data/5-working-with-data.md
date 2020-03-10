---
uid: web-pages/overview/data/5-working-with-data
title: 在 ASP.NET 网页（Razor）站点中使用数据库的简介 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍了如何从数据库访问数据，并使用 ASP.NET 网页来显示数据。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474038"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="5f932-103">在 ASP.NET 网页（Razor）站点中使用数据库简介</span><span class="sxs-lookup"><span data-stu-id="5f932-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="5f932-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5f932-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5f932-105">本文介绍如何使用 Microsoft WebMatrix 工具在 ASP.NET 网页（Razor）网站中创建数据库，以及如何创建可用于显示、添加、编辑和删除数据的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="5f932-106">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="5f932-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="5f932-107">如何创建数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-107">How to create a database.</span></span>
> - <span data-ttu-id="5f932-108">如何连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-108">How to connect to a database.</span></span>
> - <span data-ttu-id="5f932-109">如何在网页中显示数据。</span><span class="sxs-lookup"><span data-stu-id="5f932-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="5f932-110">如何插入、更新和删除数据库记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="5f932-111">下面是本文中介绍的功能：</span><span class="sxs-lookup"><span data-stu-id="5f932-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="5f932-112">使用 Microsoft SQL Server Compact 版本的数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="5f932-113">使用 SQL 查询。</span><span class="sxs-lookup"><span data-stu-id="5f932-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="5f932-114">`Database` 类。</span><span class="sxs-lookup"><span data-stu-id="5f932-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5f932-115">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5f932-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5f932-116">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="5f932-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="5f932-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="5f932-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="5f932-118">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="5f932-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="5f932-119">你可以使用 ASP.NET 网页3和 Visual Studio 2013 （对于 Web 为 Visual Studio Express 2013）;但是，用户界面将有所不同。</span><span class="sxs-lookup"><span data-stu-id="5f932-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>

## <a name="introduction-to-databases"></a><span data-ttu-id="5f932-120">数据库简介</span><span class="sxs-lookup"><span data-stu-id="5f932-120">Introduction to Databases</span></span>

<span data-ttu-id="5f932-121">假设一个典型的通讯簿。</span><span class="sxs-lookup"><span data-stu-id="5f932-121">Imagine a typical address book.</span></span> <span data-ttu-id="5f932-122">对于通讯簿中的每个条目（即，对于每个人），都有几个信息，如名字、姓氏、地址、电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="5f932-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="5f932-123">图片数据的一种典型方式是使用行和列作为表。</span><span class="sxs-lookup"><span data-stu-id="5f932-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="5f932-124">在数据库术语中，每行通常称为记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="5f932-125">每个列（有时称为字段）都包含每个数据类型的值：名字、姓氏等。</span><span class="sxs-lookup"><span data-stu-id="5f932-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="5f932-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="5f932-126">**ID**</span></span> | <span data-ttu-id="5f932-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="5f932-127">**FirstName**</span></span> | <span data-ttu-id="5f932-128">**LastName**</span><span class="sxs-lookup"><span data-stu-id="5f932-128">**LastName**</span></span> | <span data-ttu-id="5f932-129">**地址**</span><span class="sxs-lookup"><span data-stu-id="5f932-129">**Address**</span></span> | <span data-ttu-id="5f932-130">**电子邮件**</span><span class="sxs-lookup"><span data-stu-id="5f932-130">**Email**</span></span> | <span data-ttu-id="5f932-131">**电话**</span><span class="sxs-lookup"><span data-stu-id="5f932-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5f932-132">1</span><span class="sxs-lookup"><span data-stu-id="5f932-132">1</span></span> | <span data-ttu-id="5f932-133">Jim</span><span class="sxs-lookup"><span data-stu-id="5f932-133">Jim</span></span> | <span data-ttu-id="5f932-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="5f932-134">Abrus</span></span> | <span data-ttu-id="5f932-135">210 100th St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="5f932-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="5f932-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="5f932-136">555 0100</span></span> |
| <span data-ttu-id="5f932-137">2</span><span class="sxs-lookup"><span data-stu-id="5f932-137">2</span></span> | <span data-ttu-id="5f932-138">Terry</span><span class="sxs-lookup"><span data-stu-id="5f932-138">Terry</span></span> | <span data-ttu-id="5f932-139">Adams</span><span class="sxs-lookup"><span data-stu-id="5f932-139">Adams</span></span> | <span data-ttu-id="5f932-140">1234主要圣西雅图 WA 99011</span><span class="sxs-lookup"><span data-stu-id="5f932-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="5f932-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="5f932-141">555 0101</span></span> |

<span data-ttu-id="5f932-142">对于大多数数据库表，表必须具有包含唯一标识符的列，如客户编号、帐户号等。这称为表的*主键*，你可以使用它来标识表中的每一行。</span><span class="sxs-lookup"><span data-stu-id="5f932-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="5f932-143">在此示例中，ID 列是通讯簿的主键。</span><span class="sxs-lookup"><span data-stu-id="5f932-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="5f932-144">通过这一对数据库的基本了解，你可以了解如何创建简单的数据库并执行一些操作，如添加、修改和删除数据。</span><span class="sxs-lookup"><span data-stu-id="5f932-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="5f932-145">**关系数据库**</span><span class="sxs-lookup"><span data-stu-id="5f932-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="5f932-146">可以通过多种方式存储数据，包括文本文件和电子表格。</span><span class="sxs-lookup"><span data-stu-id="5f932-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="5f932-147">但对于大多数业务用途，数据存储在关系数据库中。</span><span class="sxs-lookup"><span data-stu-id="5f932-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="5f932-148">本文不会深入到数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="5f932-149">但是，你可能会发现很少理解它们。</span><span class="sxs-lookup"><span data-stu-id="5f932-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="5f932-150">在关系数据库中，信息以逻辑方式划分为单独的表。</span><span class="sxs-lookup"><span data-stu-id="5f932-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="5f932-151">例如，学校的数据库可能包含学生的单独表和类产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="5f932-152">数据库软件（如 SQL Server）支持功能强大的命令，可让您动态建立表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="5f932-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="5f932-153">例如，您可以使用关系数据库建立学生与类之间的逻辑关系，以便创建计划。</span><span class="sxs-lookup"><span data-stu-id="5f932-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="5f932-154">将数据存储在单独的表中可降低表结构的复杂性，并减少在表中保留冗余数据的需要。</span><span class="sxs-lookup"><span data-stu-id="5f932-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="5f932-155">创建数据库</span><span class="sxs-lookup"><span data-stu-id="5f932-155">Creating a Database</span></span>

<span data-ttu-id="5f932-156">此过程说明如何使用 WebMatrix 中包含的 SQL Server Compact 数据库设计工具创建名为 SmallBakery 的数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="5f932-157">虽然您可以使用代码创建数据库，但使用 WebMatrix 等设计工具创建数据库表和数据库表更常见。</span><span class="sxs-lookup"><span data-stu-id="5f932-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="5f932-158">启动 WebMatrix，然后在 "快速入门" 页上，单击 "**从模板中选择站点**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="5f932-159">选择 "**空站点**"，然后在 "**站点名称**" 框中输入 "SmallBakery"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="5f932-160">在 WebMatrix 中创建并显示该站点。</span><span class="sxs-lookup"><span data-stu-id="5f932-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="5f932-161">在左窗格中，单击 "**数据库**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="5f932-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="5f932-162">在功能区中，单击 "**新建数据库**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="5f932-163">使用与你的站点相同的名称创建一个空数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="5f932-164">在左窗格中，展开 " **SmallBakery** " 节点，然后单击 "**表**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="5f932-165">在功能区中，单击 "**新建表**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="5f932-166">WebMatrix 打开表设计器。</span><span class="sxs-lookup"><span data-stu-id="5f932-166">WebMatrix opens the table designer.</span></span>

    ![[图像]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="5f932-168">单击 "**名称**" 列，并输入 &quot;Id&quot;。</span><span class="sxs-lookup"><span data-stu-id="5f932-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="5f932-169">在 "**数据类型**" 列中，选择**int**。</span><span class="sxs-lookup"><span data-stu-id="5f932-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="5f932-170">是否设置**为主键？** 并将 **？选项标识**为**Yes**。</span><span class="sxs-lookup"><span data-stu-id="5f932-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="5f932-171">如名称所示，**为 Primary key**告诉数据库这将是表的主键。</span><span class="sxs-lookup"><span data-stu-id="5f932-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="5f932-172">**Is Identity**告诉数据库自动为每个新记录创建一个 ID 号，并向其分配下一个顺序编号（从1开始）。</span><span class="sxs-lookup"><span data-stu-id="5f932-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="5f932-173">单击下一行。</span><span class="sxs-lookup"><span data-stu-id="5f932-173">Click in the next row.</span></span> <span data-ttu-id="5f932-174">编辑器会启动新的列定义。</span><span class="sxs-lookup"><span data-stu-id="5f932-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="5f932-175">对于 "名称" 值，请输入 &quot;名称&quot;。</span><span class="sxs-lookup"><span data-stu-id="5f932-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="5f932-176">对于 "**数据类型**"，请选择 "&quot;nvarchar&quot; 并将长度设置为50。</span><span class="sxs-lookup"><span data-stu-id="5f932-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="5f932-177">`nvarchar` 的*var*部分通知数据库，此列的数据将是字符串，其大小可能因记录而异。</span><span class="sxs-lookup"><span data-stu-id="5f932-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="5f932-178">（ *N*前缀表示*国家/地区*，表示该字段可以保存表示任何字母或书写系统&#8212;的字符数据，即，该字段包含 Unicode 数据。）</span><span class="sxs-lookup"><span data-stu-id="5f932-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="5f932-179">将 "**允许 Null 值**" 选项设置为 "**否**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="5f932-180">这会强制 "*名称*" 列不留空。</span><span class="sxs-lookup"><span data-stu-id="5f932-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="5f932-181">使用同一个过程创建一个名为*Description*的列。</span><span class="sxs-lookup"><span data-stu-id="5f932-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="5f932-182">将**数据类型**设置为 "nvarchar"，将50设置为长度，将 "**允许 null 值**" 设置为 "false"。</span><span class="sxs-lookup"><span data-stu-id="5f932-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="5f932-183">创建名为*Price*的列。</span><span class="sxs-lookup"><span data-stu-id="5f932-183">Create a column named *Price*.</span></span> <span data-ttu-id="5f932-184">将 **"数据类型" 设置为 "money"** 并将 "**允许 null** " 设置为 "false"。</span><span class="sxs-lookup"><span data-stu-id="5f932-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="5f932-185">在顶部的框中，将表命名为 &quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="5f932-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="5f932-186">完成后，定义将如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-186">When you're done, the definition will look like this:</span></span>

    ![[图像]](5-working-with-data/_static/image2.png)
17. <span data-ttu-id="5f932-188">按 Ctrl + S 保存表。</span><span class="sxs-lookup"><span data-stu-id="5f932-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="5f932-189">向数据库添加数据</span><span class="sxs-lookup"><span data-stu-id="5f932-189">Adding Data to the Database</span></span>

<span data-ttu-id="5f932-190">现在，你可以将一些示例数据添加到你稍后将在本文中使用的数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="5f932-191">在左窗格中，展开 " **SmallBakery** " 节点，然后单击 "**表**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="5f932-192">右键单击 Product 表，然后单击 "**数据**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="5f932-193">在 "编辑" 窗格中，输入以下记录：</span><span class="sxs-lookup"><span data-stu-id="5f932-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="5f932-194">**Name**</span><span class="sxs-lookup"><span data-stu-id="5f932-194">**Name**</span></span> | <span data-ttu-id="5f932-195">**描述**</span><span class="sxs-lookup"><span data-stu-id="5f932-195">**Description**</span></span> | <span data-ttu-id="5f932-196">**价值**</span><span class="sxs-lookup"><span data-stu-id="5f932-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="5f932-197">面包</span><span class="sxs-lookup"><span data-stu-id="5f932-197">Bread</span></span> | <span data-ttu-id="5f932-198">每日融入。</span><span class="sxs-lookup"><span data-stu-id="5f932-198">Baked fresh every day.</span></span> | <span data-ttu-id="5f932-199">2.99</span><span class="sxs-lookup"><span data-stu-id="5f932-199">2.99</span></span> |
    | <span data-ttu-id="5f932-200">草莓松饼</span><span class="sxs-lookup"><span data-stu-id="5f932-200">Strawberry Shortcake</span></span> | <span data-ttu-id="5f932-201">与我们的菜园 strawberries。</span><span class="sxs-lookup"><span data-stu-id="5f932-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="5f932-202">9.99</span><span class="sxs-lookup"><span data-stu-id="5f932-202">9.99</span></span> |
    | <span data-ttu-id="5f932-203">Apple 饼图</span><span class="sxs-lookup"><span data-stu-id="5f932-203">Apple Pie</span></span> | <span data-ttu-id="5f932-204">第二次仅限您母亲的饼图。</span><span class="sxs-lookup"><span data-stu-id="5f932-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="5f932-205">12.99</span><span class="sxs-lookup"><span data-stu-id="5f932-205">12.99</span></span> |
    | <span data-ttu-id="5f932-206">Pecan 饼图</span><span class="sxs-lookup"><span data-stu-id="5f932-206">Pecan Pie</span></span> | <span data-ttu-id="5f932-207">如果您喜欢 pecans，这就是您的。</span><span class="sxs-lookup"><span data-stu-id="5f932-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="5f932-208">10.99</span><span class="sxs-lookup"><span data-stu-id="5f932-208">10.99</span></span> |
    | <span data-ttu-id="5f932-209">柠檬饼图</span><span class="sxs-lookup"><span data-stu-id="5f932-209">Lemon Pie</span></span> | <span data-ttu-id="5f932-210">利用世界上最好的 lemons。</span><span class="sxs-lookup"><span data-stu-id="5f932-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="5f932-211">11.99</span><span class="sxs-lookup"><span data-stu-id="5f932-211">11.99</span></span> |
    | <span data-ttu-id="5f932-212">纸托蛋糕</span><span class="sxs-lookup"><span data-stu-id="5f932-212">Cupcakes</span></span> | <span data-ttu-id="5f932-213">你的孩子和你的孩子会喜欢这些。</span><span class="sxs-lookup"><span data-stu-id="5f932-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="5f932-214">7.99</span><span class="sxs-lookup"><span data-stu-id="5f932-214">7.99</span></span> |

    <span data-ttu-id="5f932-215">请记住，您不必为*Id*列输入任何内容。</span><span class="sxs-lookup"><span data-stu-id="5f932-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="5f932-216">创建*Id*列后，将其 "**为标识**" 属性设置为 "true"，这会使其自动填充。</span><span class="sxs-lookup"><span data-stu-id="5f932-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="5f932-217">输入完数据后，表设计器将如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[图像]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="5f932-219">关闭包含数据库数据的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5f932-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="5f932-220">显示数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="5f932-220">Displaying Data from a Database</span></span>

<span data-ttu-id="5f932-221">如果数据库中包含数据，则可以在 ASP.NET 网页中显示数据。</span><span class="sxs-lookup"><span data-stu-id="5f932-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="5f932-222">若要选择要显示的表行，请使用 SQL 语句，该语句是传递到数据库的命令。</span><span class="sxs-lookup"><span data-stu-id="5f932-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="5f932-223">在左窗格中，单击 "**文件**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="5f932-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="5f932-224">在网站的根目录中，创建一个名为*ListProducts*的新的 CSHTML 页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="5f932-225">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f932-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="5f932-226">在第一个代码块中，打开前面创建的*SmallBakery*文件（数据库）。</span><span class="sxs-lookup"><span data-stu-id="5f932-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="5f932-227">`Database.Open` 方法假定 *.sdf*文件位于网站的*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5f932-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="5f932-228">（请注意，不需要指定&#8212; .sdf 扩展名 *。* 实际上，如果您这样做，`Open` 方法将不起作用。）</span><span class="sxs-lookup"><span data-stu-id="5f932-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f932-229">*应用\_Data*文件夹是 ASP.NET 中用于存储数据文件的特殊文件夹。</span><span class="sxs-lookup"><span data-stu-id="5f932-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="5f932-230">有关详细信息，请参阅本文后面的[连接到数据库](#SB_ConnectingToADatabase)。</span><span class="sxs-lookup"><span data-stu-id="5f932-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="5f932-231">然后，使用以下 SQL `Select` 语句发出查询数据库的请求：</span><span class="sxs-lookup"><span data-stu-id="5f932-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="5f932-232">在语句中，`Product` 标识要查询的表。</span><span class="sxs-lookup"><span data-stu-id="5f932-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="5f932-233">`*` 字符指定查询应返回表中的所有列。</span><span class="sxs-lookup"><span data-stu-id="5f932-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="5f932-234">（如果只想查看某些列，也可以单独列出列，用逗号分隔）。`Order By` 子句指示在这种情况下，应&#8212;按*名称*列对数据进行排序的方式。</span><span class="sxs-lookup"><span data-stu-id="5f932-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="5f932-235">这意味着数据根据每行的 "*名称*" 列的值按字母顺序排序。</span><span class="sxs-lookup"><span data-stu-id="5f932-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="5f932-236">在页面的正文中，标记创建将用于显示数据的 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="5f932-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="5f932-237">在 `<tbody>` 元素中，使用 `foreach` 循环单独获取查询返回的每个数据行。</span><span class="sxs-lookup"><span data-stu-id="5f932-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="5f932-238">对于每个数据行，创建一个 HTML 表行（`<tr>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="5f932-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="5f932-239">然后，为每个列创建 HTML 表单元格（`<td>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="5f932-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="5f932-240">每次遍历循环时，数据库中的下一个可用行将位于 `row` 变量（在 `foreach` 语句中设置此项）。</span><span class="sxs-lookup"><span data-stu-id="5f932-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="5f932-241">若要从行中获取单个列，可以使用 `row.Name` 或 `row.Description`，或者使用所需的列名称。</span><span class="sxs-lookup"><span data-stu-id="5f932-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="5f932-242">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="5f932-242">Run the page in a browser.</span></span> <span data-ttu-id="5f932-243">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）页面将显示如下所示的列表：</span><span class="sxs-lookup"><span data-stu-id="5f932-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[图像]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="5f932-245">**结构化查询语言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="5f932-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="5f932-246">SQL 是在大多数关系数据库中用于管理数据库中的数据的一种语言。</span><span class="sxs-lookup"><span data-stu-id="5f932-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="5f932-247">它包含的命令可用于检索和更新数据，并允许您创建、修改和管理数据库表。</span><span class="sxs-lookup"><span data-stu-id="5f932-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="5f932-248">SQL 不同于编程语言（例如，您在 WebMatrix 中使用的语言），因为使用 SQL 时，这一理念是告诉数据库您所需的内容，而数据库的工作是确定如何获取数据或执行任务。</span><span class="sxs-lookup"><span data-stu-id="5f932-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="5f932-249">下面是一些 SQL 命令的示例和它们的作用：</span><span class="sxs-lookup"><span data-stu-id="5f932-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="5f932-250">如果 "*价格*" 的值大于10，则将从*Product*表的记录中提取*Id*、*名称*和*价格*列，并根据*Name*列的值以字母顺序返回结果。</span><span class="sxs-lookup"><span data-stu-id="5f932-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="5f932-251">此命令将返回一个结果集，其中包含满足条件的记录; 如果没有记录匹配，则返回空集。</span><span class="sxs-lookup"><span data-stu-id="5f932-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="5f932-252">这会在*Product*表中插入一条新记录，将*Name*列设置为 &quot;新月形面包&quot;，将*Description*列设置为 &quot;不可靠感到满意&quot;，并将价格设置为1.99。</span><span class="sxs-lookup"><span data-stu-id="5f932-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="5f932-253">此命令删除*Product*表中的记录，其到期日期列早于2008年1月1日。</span><span class="sxs-lookup"><span data-stu-id="5f932-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="5f932-254">（这假定*Product*表具有这样的列。）此处以 MM/DD/YYYY 格式输入日期，但应以用于区域设置的格式输入。</span><span class="sxs-lookup"><span data-stu-id="5f932-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="5f932-255">`Insert Into` 和 `Delete` 命令不返回结果集。</span><span class="sxs-lookup"><span data-stu-id="5f932-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="5f932-256">相反，它们将返回一个数字，该数字告诉你命令所影响的记录数。</span><span class="sxs-lookup"><span data-stu-id="5f932-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="5f932-257">对于某些操作（例如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="5f932-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="5f932-258">这就是在连接到数据库时，生产数据库经常必须提供用户名和密码的原因。</span><span class="sxs-lookup"><span data-stu-id="5f932-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="5f932-259">有多个 SQL 命令，但它们都遵循类似的模式。</span><span class="sxs-lookup"><span data-stu-id="5f932-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="5f932-260">您可以使用 SQL 命令来创建数据库表，计算表中的记录数，计算价格，以及执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="5f932-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

## <a name="inserting-data-in-a-database"></a><span data-ttu-id="5f932-261">在数据库中插入数据</span><span class="sxs-lookup"><span data-stu-id="5f932-261">Inserting Data in a Database</span></span>

<span data-ttu-id="5f932-262">本部分介绍如何创建一个页面，使用户能够向*产品*数据库表添加新产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="5f932-263">插入新产品记录后，页面将使用您在上一节中创建的*ListProducts*页面显示更新后的表。</span><span class="sxs-lookup"><span data-stu-id="5f932-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="5f932-264">此页包括验证以确保用户输入的数据对数据库有效。</span><span class="sxs-lookup"><span data-stu-id="5f932-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="5f932-265">例如，页面中的代码可确保已为所有必需列输入了值。</span><span class="sxs-lookup"><span data-stu-id="5f932-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="5f932-266">在网站中，创建一个名为*InsertProducts*的新的 CSHTML 文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="5f932-267">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f932-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="5f932-268">页面的正文包含一个 HTML 窗体，其中包含三个文本框，用户可以在其中输入名称、说明和价格。</span><span class="sxs-lookup"><span data-stu-id="5f932-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="5f932-269">当用户单击 "**插入**" 按钮时，页面顶部的代码会打开与*SmallBakery*数据库的连接。</span><span class="sxs-lookup"><span data-stu-id="5f932-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="5f932-270">然后，使用 `Request` 对象获取用户已提交的值，并将这些值分配给本地变量。</span><span class="sxs-lookup"><span data-stu-id="5f932-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="5f932-271">若要验证用户是否输入了每个所需列的值，需注册要验证的每个 `<input>` 元素：</span><span class="sxs-lookup"><span data-stu-id="5f932-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="5f932-272">`Validation` helper 检查已注册的每个字段中是否存在值。</span><span class="sxs-lookup"><span data-stu-id="5f932-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="5f932-273">您可以通过检查 `Validation.IsValid()`来测试所有字段是否通过验证，这通常是在处理您从用户那里获取的信息之前执行的：</span><span class="sxs-lookup"><span data-stu-id="5f932-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="5f932-274">（`&&` 运算符表示和，这是因为*这是一个窗体提交并且所有字段均已通过验证*。）</span><span class="sxs-lookup"><span data-stu-id="5f932-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="5f932-275">如果所有列均已验证（none 均为空），则继续并创建一个 SQL 语句来插入数据，然后执行该语句，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="5f932-276">要插入的值包括参数占位符（`@0`、`@1``@2`）。</span><span class="sxs-lookup"><span data-stu-id="5f932-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f932-277">作为安全预防措施，请始终使用参数将值传递给 SQL 语句，如前面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="5f932-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="5f932-278">这使您有机会验证用户的数据，并帮助防止尝试向数据库发送恶意命令（有时称为 SQL 注入式攻击）。</span><span class="sxs-lookup"><span data-stu-id="5f932-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="5f932-279">若要执行查询，请使用此语句，并向其传递包含用于替换占位符的值的变量：</span><span class="sxs-lookup"><span data-stu-id="5f932-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="5f932-280">执行 `Insert Into` 语句后，可以使用以下行将用户发送到列出产品的页面：</span><span class="sxs-lookup"><span data-stu-id="5f932-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="5f932-281">如果验证未成功，则会跳过插入。</span><span class="sxs-lookup"><span data-stu-id="5f932-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="5f932-282">相反，可以在页面中使用一个帮助器来显示累积的错误消息（如果有）：</span><span class="sxs-lookup"><span data-stu-id="5f932-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="5f932-283">请注意，标记中的样式块包含名为 `.validation-summary-errors`的 CSS 类定义。</span><span class="sxs-lookup"><span data-stu-id="5f932-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="5f932-284">这是默认情况下为包含任何验证错误的 `<div>` 元素使用的 CSS 类的名称。</span><span class="sxs-lookup"><span data-stu-id="5f932-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="5f932-285">在这种情况下，CSS 类指定验证摘要错误以红色和粗体显示，但你可以定义 `.validation-summary-errors` 类以显示你喜欢的任何格式。</span><span class="sxs-lookup"><span data-stu-id="5f932-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="5f932-286">测试插入页</span><span class="sxs-lookup"><span data-stu-id="5f932-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="5f932-287">查看浏览器中的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-287">View the page in a browser.</span></span> <span data-ttu-id="5f932-288">页面将显示类似于下图所示的窗体。</span><span class="sxs-lookup"><span data-stu-id="5f932-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[图像]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="5f932-290">输入所有列的值，但请确保将 " *Price* " 列留空。</span><span class="sxs-lookup"><span data-stu-id="5f932-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="5f932-291">单击“插入”。</span><span class="sxs-lookup"><span data-stu-id="5f932-291">Click **Insert**.</span></span> <span data-ttu-id="5f932-292">此页将显示一条错误消息，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="5f932-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="5f932-293">（不创建新记录。）</span><span class="sxs-lookup"><span data-stu-id="5f932-293">(No new record is created.)</span></span>

    ![[图像]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="5f932-295">完全填写表单，然后单击 "**插入**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="5f932-296">此时，将显示 " *ListProducts* " 页，并显示新记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="5f932-297">更新数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="5f932-297">Updating Data in a Database</span></span>

<span data-ttu-id="5f932-298">将数据输入到表中后，可能需要对其进行更新。</span><span class="sxs-lookup"><span data-stu-id="5f932-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="5f932-299">此过程说明如何创建两个与之前为数据插入创建的页面相似的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="5f932-300">第一页显示产品，并允许用户选择一个要更改的产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="5f932-301">在第二页中，用户可以实际进行编辑并保存。</span><span class="sxs-lookup"><span data-stu-id="5f932-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5f932-302">**重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。</span><span class="sxs-lookup"><span data-stu-id="5f932-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="5f932-303">有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅向[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="5f932-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="5f932-304">在网站中，创建一个名为*EditProducts*的新的 CSHTML 文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="5f932-305">将文件中的现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f932-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="5f932-306">此页与之前的*ListProducts*页之间的唯一区别是，此页中的 HTML 表包含一个额外的列，其中显示了 "**编辑**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5f932-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="5f932-307">单击此链接后，将转到*UpdateProducts*页（接下来将创建），可以在其中编辑选定的记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="5f932-308">查看创建**编辑**链接的代码：</span><span class="sxs-lookup"><span data-stu-id="5f932-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="5f932-309">这会创建一个 HTML `<a>` 元素，其 `href` 属性进行动态设置。</span><span class="sxs-lookup"><span data-stu-id="5f932-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="5f932-310">`href` 属性指定用户单击链接时要显示的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="5f932-311">它还将当前行的 `Id` 值传递到链接。</span><span class="sxs-lookup"><span data-stu-id="5f932-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="5f932-312">当页面运行时，页面源可能会包含如下所示的链接：</span><span class="sxs-lookup"><span data-stu-id="5f932-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="5f932-313">请注意，`href` 特性设置为 "`UpdateProducts/n`"，其中*n*是一个产品编号。</span><span class="sxs-lookup"><span data-stu-id="5f932-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="5f932-314">当用户单击其中一个链接时，生成的 URL 将如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="5f932-315">换言之，要编辑的产品编号将传入 URL。</span><span class="sxs-lookup"><span data-stu-id="5f932-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="5f932-316">查看浏览器中的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-316">View the page in a browser.</span></span> <span data-ttu-id="5f932-317">页面按如下格式显示数据：</span><span class="sxs-lookup"><span data-stu-id="5f932-317">The page displays the data in a format like this:</span></span>

    ![[图像]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="5f932-319">接下来，您将创建允许用户实际更新数据的页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="5f932-320">"更新" 页包括用于验证用户输入的数据的验证。</span><span class="sxs-lookup"><span data-stu-id="5f932-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="5f932-321">例如，页面中的代码可确保已为所有必需列输入了值。</span><span class="sxs-lookup"><span data-stu-id="5f932-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="5f932-322">在网站中，创建一个名为*UpdateProducts*的新的 CSHTML 文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="5f932-323">将文件中的现有标记替换为以下项。</span><span class="sxs-lookup"><span data-stu-id="5f932-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="5f932-324">页面正文包含一个 HTML 窗体，其中显示了产品以及用户可以对其进行编辑。</span><span class="sxs-lookup"><span data-stu-id="5f932-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="5f932-325">要使产品显示，请使用以下 SQL 语句：</span><span class="sxs-lookup"><span data-stu-id="5f932-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="5f932-326">这会选择其 ID 与 `@0` 参数中传递的值匹配的产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="5f932-327">（因为*Id*是主键，因此必须是唯一的，因此，只能通过这种方式选择一个产品记录。）若要获取要传递给此 `Select` 语句的 ID 值，可以使用以下语法读取作为 URL 的一部分传递到页面的值：</span><span class="sxs-lookup"><span data-stu-id="5f932-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="5f932-328">若要实际提取产品记录，可以使用 `QuerySingle` 方法，该方法将仅返回一条记录：</span><span class="sxs-lookup"><span data-stu-id="5f932-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="5f932-329">将单个行返回 `row` 变量。</span><span class="sxs-lookup"><span data-stu-id="5f932-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="5f932-330">可以从每个列中获取数据，并将其分配给本地变量，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="5f932-331">在窗体的标记中，这些值通过使用嵌入的代码自动显示在单独的文本框中，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="5f932-332">代码的该部分显示要更新的产品记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="5f932-333">显示记录后，用户可以编辑单独的列。</span><span class="sxs-lookup"><span data-stu-id="5f932-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="5f932-334">当用户通过单击 "**更新**" 按钮提交窗体时，`if(IsPost)` 块中的代码将运行。</span><span class="sxs-lookup"><span data-stu-id="5f932-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="5f932-335">这将从 `Request` 对象获取用户的值，将值存储在变量中，并验证是否已填充每个列。</span><span class="sxs-lookup"><span data-stu-id="5f932-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="5f932-336">如果验证通过，代码将创建以下 SQL Update 语句：</span><span class="sxs-lookup"><span data-stu-id="5f932-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="5f932-337">在 SQL `Update` 语句中，可以指定要更新的每个列以及要将其设置为的值。</span><span class="sxs-lookup"><span data-stu-id="5f932-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="5f932-338">在此代码中，将使用参数占位符指定值 `@0`、`@1`、`@2`等。</span><span class="sxs-lookup"><span data-stu-id="5f932-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="5f932-339">（如前文所述，为安全，应始终使用参数将值传递给 SQL 语句。）</span><span class="sxs-lookup"><span data-stu-id="5f932-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="5f932-340">调用 `db.Execute` 方法时，将按与 SQL 语句中的参数对应的顺序传递包含值的变量：</span><span class="sxs-lookup"><span data-stu-id="5f932-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="5f932-341">执行 `Update` 语句后，调用以下方法，以便将用户重定向回编辑页面：</span><span class="sxs-lookup"><span data-stu-id="5f932-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="5f932-342">其作用是用户在数据库中查看数据的更新列表，并可以编辑其他产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="5f932-343">保存页。</span><span class="sxs-lookup"><span data-stu-id="5f932-343">Save the page.</span></span>
7. <span data-ttu-id="5f932-344">运行*EditProducts*页（而不是 "更新" 页），然后单击 "**编辑**" 以选择要编辑的产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="5f932-345">随即显示 " *UpdateProducts* " 页，其中显示了所选的记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[图像]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="5f932-347">进行更改，然后单击 "**更新**"。</span><span class="sxs-lookup"><span data-stu-id="5f932-347">Make a change and click **Update**.</span></span> <span data-ttu-id="5f932-348">"产品" 列表将再次显示您更新的数据。</span><span class="sxs-lookup"><span data-stu-id="5f932-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="5f932-349">删除数据库中的数据</span><span class="sxs-lookup"><span data-stu-id="5f932-349">Deleting Data in a Database</span></span>

<span data-ttu-id="5f932-350">本部分说明如何允许用户从*产品*数据库表中删除产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="5f932-351">该示例由两个页面组成。</span><span class="sxs-lookup"><span data-stu-id="5f932-351">The example consists of two pages.</span></span> <span data-ttu-id="5f932-352">在第一页中，用户选择要删除的记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="5f932-353">然后，将在另一页中显示要删除的记录，让他们确认是否要删除该记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5f932-354">**重要提示**在生产网站中，通常会限制允许对数据进行更改的人员。</span><span class="sxs-lookup"><span data-stu-id="5f932-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="5f932-355">有关如何设置成员身份和授权用户在网站上执行任务的方式的信息，请参阅[将安全性和成员身份添加到 ASP.NET 网页站点](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="5f932-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="5f932-356">在网站中，创建一个名为*ListProductsForDelete*的新的 CSHTML 文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="5f932-357">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f932-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="5f932-358">此页面类似于前面的*EditProducts*页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="5f932-359">但是，它不会显示每个产品的**编辑**链接，而是显示 "**删除**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5f932-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="5f932-360">使用标记中的以下嵌入代码创建 "**删除**" 链接：</span><span class="sxs-lookup"><span data-stu-id="5f932-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="5f932-361">当用户单击链接时，这会创建如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="5f932-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="5f932-362">此 URL 调用名为*DeleteProduct*的页面（稍后将创建），并向其传递要删除的产品的 ID （此处为4）。</span><span class="sxs-lookup"><span data-stu-id="5f932-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="5f932-363">保存该文件，但将其保持打开状态。</span><span class="sxs-lookup"><span data-stu-id="5f932-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="5f932-364">创建另一个名为*DeleteProduct*的 CHTML 文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="5f932-365">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="5f932-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="5f932-366">此页面由*ListProductsForDelete*调用，并允许用户确认他们要删除产品。</span><span class="sxs-lookup"><span data-stu-id="5f932-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="5f932-367">若要列出要删除的产品，请使用以下代码获取要从 URL 中删除的产品的 ID：</span><span class="sxs-lookup"><span data-stu-id="5f932-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="5f932-368">然后，该页会要求用户单击某个按钮以实际删除该记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="5f932-369">这是一项重要的安全措施：在网站中执行敏感操作（如更新或删除数据）时，这些操作应始终使用 POST 操作完成，而不是 GET 操作。</span><span class="sxs-lookup"><span data-stu-id="5f932-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="5f932-370">如果你的站点已设置为可以使用 GET 操作执行删除操作，则任何人都可以传递类似 `http://<server>/DeleteProduct/4` 的 URL，并从数据库中删除所需的任何内容。</span><span class="sxs-lookup"><span data-stu-id="5f932-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="5f932-371">通过添加确认和编码页面，以便只能使用 POST 来执行删除操作，可将安全度量值添加到站点。</span><span class="sxs-lookup"><span data-stu-id="5f932-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="5f932-372">使用以下代码执行实际的删除操作，该操作首先确认这是 post 操作，并且该 ID 不为空：</span><span class="sxs-lookup"><span data-stu-id="5f932-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="5f932-373">此代码运行一个 SQL 语句，该语句删除指定的记录，然后将该用户重定向回列表页。</span><span class="sxs-lookup"><span data-stu-id="5f932-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="5f932-374">在浏览器中运行*ListProductsForDelete* 。</span><span class="sxs-lookup"><span data-stu-id="5f932-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[图像]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="5f932-376">单击其中一个产品的 "**删除**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5f932-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="5f932-377">随即显示 " *DeleteProduct* " 页，确认是否要删除该记录。</span><span class="sxs-lookup"><span data-stu-id="5f932-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="5f932-378">单击“删除”按钮。</span><span class="sxs-lookup"><span data-stu-id="5f932-378">Click the **Delete** button.</span></span> <span data-ttu-id="5f932-379">将删除产品记录，并使用更新的产品列表刷新页面。</span><span class="sxs-lookup"><span data-stu-id="5f932-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="5f932-380">连接到数据库</span><span class="sxs-lookup"><span data-stu-id="5f932-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="5f932-381">可以通过两种方式连接到数据库。</span><span class="sxs-lookup"><span data-stu-id="5f932-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="5f932-382">第一种方法是使用 `Database.Open` 方法并指定数据库文件的名称（更少为 *.sdf*扩展名）：</span><span class="sxs-lookup"><span data-stu-id="5f932-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="5f932-383">`Open` 方法假定。 *.sdf*文件位于网站的*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5f932-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="5f932-384">此文件夹专用于存放数据。</span><span class="sxs-lookup"><span data-stu-id="5f932-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="5f932-385">例如，它有适当的权限允许网站读取和写入数据，作为一种安全措施，WebMatrix 不允许从此文件夹访问文件。</span><span class="sxs-lookup"><span data-stu-id="5f932-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="5f932-386">第二种方法是使用连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5f932-386">The second way is to use a connection string.</span></span> <span data-ttu-id="5f932-387">连接字符串包含数据库连接方式的相关信息。</span><span class="sxs-lookup"><span data-stu-id="5f932-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="5f932-388">这可以包括文件路径，也可以包含本地或远程服务器上 SQL Server 数据库的名称，以及用于连接到该服务器的用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="5f932-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="5f932-389">（如果将数据保存在 SQL Server 的集中管理的版本中，如在托管提供商的站点上，则始终使用连接字符串指定数据库连接信息。）</span><span class="sxs-lookup"><span data-stu-id="5f932-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="5f932-390">在 WebMatrix 中，连接字符串通常存储*在名为 web.config 的*XML 文件中。顾名思义，你可以在网站的根目录中使用*web.config 文件来*存储站点的配置信息，包括站点可能需要的任何连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5f932-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="5f932-391">*Web.config 文件中*的连接字符串的示例可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="5f932-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="5f932-392">在此示例中，连接字符串指向在服务器上运行的 SQL Server 实例中的某个数据库（而不是本地 *.sdf*文件）。</span><span class="sxs-lookup"><span data-stu-id="5f932-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="5f932-393">你需要用适当的名称替换 `myServer` 和 `myDatabase`，并为 `username` 和 `password`指定 SQL Server 登录值。</span><span class="sxs-lookup"><span data-stu-id="5f932-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="5f932-394">（"用户名" 和 "密码" 值不一定与你的 Windows 凭据相同，或与你的托管提供商提供的用于登录到其服务器的值相同。</span><span class="sxs-lookup"><span data-stu-id="5f932-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="5f932-395">请与管理员联系以获取所需的确切值。）</span><span class="sxs-lookup"><span data-stu-id="5f932-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="5f932-396">`Database.Open` 方法非常灵活，因为它允许您传递数据库 *.sdf*文件的名称或存储在*web.config 文件中的连接*字符串的名称。</span><span class="sxs-lookup"><span data-stu-id="5f932-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="5f932-397">下面的示例演示如何使用前面示例中所示的连接字符串连接到数据库：</span><span class="sxs-lookup"><span data-stu-id="5f932-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="5f932-398">如上所述，使用 `Database.Open` 方法可以传递数据库名称或连接字符串，并且它将找出要使用的数据库名称或连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5f932-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="5f932-399">当你部署（发布）你的网站时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="5f932-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="5f932-400">当你在开发和测试网站时，可以在应用中使用 *.sdf*文件 *\_Data*文件夹。</span><span class="sxs-lookup"><span data-stu-id="5f932-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="5f932-401">然后，当你将站点移到生产服务器时，可以在*web.config 文件中*使用与 *.sdf*文件相同的连接字符串，但这&#8212;一切都不需要更改你的代码。</span><span class="sxs-lookup"><span data-stu-id="5f932-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="5f932-402">最后，如果要直接使用连接字符串，可以调用 `Database.OpenConnectionString` 方法，并向其传递实际的连接字符串，而不只是*web.config*文件中的连接字符串的名称。</span><span class="sxs-lookup"><span data-stu-id="5f932-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="5f932-403">此方法在以下情况下可能非常有用：由于某种原因，你无法访问连接字符串（或其中的值，如 *.sdf*文件名），直到页面运行为止。</span><span class="sxs-lookup"><span data-stu-id="5f932-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="5f932-404">但在大多数情况下，你可以使用本文中所述的 `Database.Open`。</span><span class="sxs-lookup"><span data-stu-id="5f932-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f932-405">其他资源</span><span class="sxs-lookup"><span data-stu-id="5f932-405">Additional Resources</span></span>

- [<span data-ttu-id="5f932-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="5f932-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="5f932-407">连接到 WebMatrix 中的 SQL Server 或 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="5f932-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="5f932-408">在 ASP.NET 网站中验证用户输入</span><span class="sxs-lookup"><span data-stu-id="5f932-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
