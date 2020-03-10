---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: 介绍 ASP.NET 网页-显示数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何在 WebMatrix 中创建数据库，以及如何在使用 ASP.NET 网页（Razor）时在页面中显示数据库数据。 它假定 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421484"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="cdf85-104">介绍 ASP.NET 网页-显示数据</span><span class="sxs-lookup"><span data-stu-id="cdf85-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>

<span data-ttu-id="cdf85-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="cdf85-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="cdf85-106">本教程演示如何在 WebMatrix 中创建数据库，以及如何在使用 ASP.NET 网页（Razor）时在页面中显示数据库数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="cdf85-107">它假定您已完成了关于[ASP.NET 网页编程的介绍](../introducing-razor-syntax-c.md)。</span><span class="sxs-lookup"><span data-stu-id="cdf85-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="cdf85-108">学习内容：</span><span class="sxs-lookup"><span data-stu-id="cdf85-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="cdf85-109">如何使用 WebMatrix 工具创建数据库表和数据库表。</span><span class="sxs-lookup"><span data-stu-id="cdf85-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="cdf85-110">如何使用 WebMatrix 工具向数据库添加数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="cdf85-111">如何在页面上显示数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="cdf85-112">如何在 ASP.NET 网页中运行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="cdf85-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="cdf85-113">如何自定义 `WebGrid` 帮助程序以更改数据显示以及添加分页和排序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="cdf85-114">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="cdf85-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="cdf85-115">WebMatrix 数据库工具。</span><span class="sxs-lookup"><span data-stu-id="cdf85-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="cdf85-116">`WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-116">`WebGrid` helper.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="cdf85-117">你将生成</span><span class="sxs-lookup"><span data-stu-id="cdf85-117">What You'll Build</span></span>

<span data-ttu-id="cdf85-118">在上一教程中，你已引入 ASP.NET 网页（*cshtml*文件）、Razor 语法的基础知识和帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="cdf85-119">在本教程中，您将开始创建将用于序列的其余部分的实际 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="cdf85-120">该应用程序是一个简单的电影应用程序，可让你查看、添加、更改和删除有关电影的信息。</span><span class="sxs-lookup"><span data-stu-id="cdf85-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="cdf85-121">完成本教程后，你将能够查看类似于此页面的电影列表：</span><span class="sxs-lookup"><span data-stu-id="cdf85-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![WebGrid 显示，其中包括设置为 CSS 类名称的参数](displaying-data/_static/image1.png)

<span data-ttu-id="cdf85-123">但若要开始，必须创建数据库。</span><span class="sxs-lookup"><span data-stu-id="cdf85-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="cdf85-124">数据库简介</span><span class="sxs-lookup"><span data-stu-id="cdf85-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="cdf85-125">本教程仅提供数据库的 briefest 简介。</span><span class="sxs-lookup"><span data-stu-id="cdf85-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="cdf85-126">如果你有数据库经验，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="cdf85-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="cdf85-127">数据库包含一个或多个表，其中包含 &mdash; 的信息，例如，客户、订单和供应商的表，或者学生、教师、班级和成绩。</span><span class="sxs-lookup"><span data-stu-id="cdf85-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="cdf85-128">从结构上来说，数据库表类似于电子表格。</span><span class="sxs-lookup"><span data-stu-id="cdf85-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="cdf85-129">假设一个典型的通讯簿。</span><span class="sxs-lookup"><span data-stu-id="cdf85-129">Imagine a typical address book.</span></span> <span data-ttu-id="cdf85-130">对于通讯簿中的每个条目（即，对于每个人），都有几个信息，如名字、姓氏、地址、电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="cdf85-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![作为简单网格的示例数据库表](displaying-data/_static/image2.png)

<span data-ttu-id="cdf85-132">（行有时称为*记录*，列有时称为*字段*。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="cdf85-133">对于大多数数据库表，表必须具有一个包含唯一值（如客户编号、帐号等）的列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="cdf85-134">此值称为表的*主键*，你可以使用它来标识表中的每一行。</span><span class="sxs-lookup"><span data-stu-id="cdf85-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="cdf85-135">在此示例中，ID 列是前面示例中所示的通讯簿的主键。</span><span class="sxs-lookup"><span data-stu-id="cdf85-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="cdf85-136">您在 web 应用程序中执行的大部分工作都包含从数据库读取信息，并将信息显示在页面上。</span><span class="sxs-lookup"><span data-stu-id="cdf85-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="cdf85-137">您还将经常收集用户的信息并将其添加到数据库中，或者您将修改数据库中已经存在的记录。</span><span class="sxs-lookup"><span data-stu-id="cdf85-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="cdf85-138">（在本教程集的过程中，我们将介绍所有这些操作。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="cdf85-139">数据库工作可能避免它过度，并需要专门的知识。</span><span class="sxs-lookup"><span data-stu-id="cdf85-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="cdf85-140">但对于本教程，你必须仅了解基本概念，这些概念将在你开始时进行说明。</span><span class="sxs-lookup"><span data-stu-id="cdf85-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="cdf85-141">创建数据库</span><span class="sxs-lookup"><span data-stu-id="cdf85-141">Creating a Database</span></span>

<span data-ttu-id="cdf85-142">WebMatrix 包含一些工具，使您可以轻松地创建数据库并在数据库中创建表。</span><span class="sxs-lookup"><span data-stu-id="cdf85-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="cdf85-143">（数据库的结构称为数据库的*架构*。）对于本教程集，你将创建一个数据库，该数据库中只有一个表 &mdash; 电影中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="cdf85-144">打开 WebMatrix （如果尚未这样做），并打开在上一教程中创建的 WebPagesMovies 站点。</span><span class="sxs-lookup"><span data-stu-id="cdf85-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="cdf85-145">在左窗格中，单击 "**数据库**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="cdf85-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 数据库工作区选项卡](displaying-data/_static/image3.png)

<span data-ttu-id="cdf85-147">功能区更改为显示与数据库相关的任务。</span><span class="sxs-lookup"><span data-stu-id="cdf85-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="cdf85-148">在功能区中，单击 "**新建数据库**"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-148">In the ribbon, click **New Database**.</span></span>

![WebMatrix 功能区中的 "新建数据库" 按钮](displaying-data/_static/image4.png)

<span data-ttu-id="cdf85-150">WebMatrix 创建一个与你的站点 &mdash; *WebPagesMovies*同名的 SQL Server CE 数据库（ *.sdf*文件）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="cdf85-151">（您不需要这样做，但您可以将该文件重命名为您喜欢的任何内容，前提是它具有 *.sdf*扩展名。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="cdf85-152">创建表</span><span class="sxs-lookup"><span data-stu-id="cdf85-152">Creating a Table</span></span>

<span data-ttu-id="cdf85-153">在功能区中，单击 "**新建表**"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="cdf85-154">WebMatrix 在新选项卡中打开表设计器。（如果 "新表" 选项不可用，请确保在左侧树视图中选择了 "新建数据库"。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

![WebMatrix 功能区中的 "新建表" 按钮](displaying-data/_static/image5.png)

<span data-ttu-id="cdf85-156">在顶部的文本框（其中水印显示 "输入表名称"）中，输入 "电影"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![在 WebMatrix 数据库设计器中输入表名称](displaying-data/_static/image6.png)

<span data-ttu-id="cdf85-158">表名下的窗格是定义单个列的位置。</span><span class="sxs-lookup"><span data-stu-id="cdf85-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="cdf85-159">对于本教程中的*电影*表，只需创建几列： *ID*、*标题*、*流派*和*年份*。</span><span class="sxs-lookup"><span data-stu-id="cdf85-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="cdf85-160">在 "**名称**" 框中，输入 "ID"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="cdf85-161">此处输入值会激活新列的所有控件。</span><span class="sxs-lookup"><span data-stu-id="cdf85-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="cdf85-162">选择 "**数据类型**" 列表，并选择**int**。此值指定 ID 列将包含整数（数字）数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf85-163">我们不会在此处（很多）调用此方法，但你可以使用标准的 Windows 键盘笔势在此网格中导航。</span><span class="sxs-lookup"><span data-stu-id="cdf85-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="cdf85-164">例如，可以在字段之间进行制表符，只需开始键入即可选择列表中的项，依此类推。</span><span class="sxs-lookup"><span data-stu-id="cdf85-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>

<span data-ttu-id="cdf85-165">选项卡 "超过**默认值**" 框（即将其留空）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="cdf85-166">按 Tab**键 "为主键**" 复选框并将其选中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="cdf85-167">此选项告知数据库*ID*列将包含标识单个行的数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="cdf85-168">（也就是说，每行在 ID 列中都有一个唯一的值，您可以使用该 ID 列查找该行。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="cdf85-169">选择 "**为标识**" 选项。</span><span class="sxs-lookup"><span data-stu-id="cdf85-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="cdf85-170">此选项告知数据库它应该为每个新行自动生成下一个序列号。</span><span class="sxs-lookup"><span data-stu-id="cdf85-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="cdf85-171">（仅当你还选择了 "**是主键**" 选项时，"**为标识**" 选项才起作用。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="cdf85-172">单击下一个网格行，或按 Tab 两次以完成当前行。</span><span class="sxs-lookup"><span data-stu-id="cdf85-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="cdf85-173">笔势将保存当前行并启动下一个行。</span><span class="sxs-lookup"><span data-stu-id="cdf85-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="cdf85-174">请注意，"**默认值**" 列现在显示**Null**。</span><span class="sxs-lookup"><span data-stu-id="cdf85-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="cdf85-175">（默认值为 Null，表示为。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="cdf85-176">定义完新**ID**列后，设计器将如下图所示：</span><span class="sxs-lookup"><span data-stu-id="cdf85-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![为电影表定义 ID 列后，WebMatrix 数据库设计器](displaying-data/_static/image7.png)

<span data-ttu-id="cdf85-178">若要创建下一列，请单击 "**名称**" 列中的框。</span><span class="sxs-lookup"><span data-stu-id="cdf85-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="cdf85-179">输入列的 "Title"，然后为 "**数据类型**" 值选择 " **nvarchar** "。</span><span class="sxs-lookup"><span data-stu-id="cdf85-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="cdf85-180">**Nvarchar**的 "var" 部分告知数据库，此列的数据将是字符串，其大小可能因记录而异。</span><span class="sxs-lookup"><span data-stu-id="cdf85-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="cdf85-181">（"N" 前缀表示 "国家"，这表示该字段可以保存任何字母或书写系统的字符数据，也就是说，该字段包含 Unicode 数据。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="cdf85-182">选择 " **nvarchar**" 时，将显示另一个框，您可以在其中输入字段的最大长度。</span><span class="sxs-lookup"><span data-stu-id="cdf85-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="cdf85-183">输入50，假设要在本教程中使用的电影标题不会超过50个字符。</span><span class="sxs-lookup"><span data-stu-id="cdf85-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="cdf85-184">跳过**默认值**并清除 "**允许 null**值" 选项。</span><span class="sxs-lookup"><span data-stu-id="cdf85-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="cdf85-185">您不希望数据库允许将任何电影输入到没有标题的数据库中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="cdf85-186">完成并转到下一行后，设计器将如下图所示：</span><span class="sxs-lookup"><span data-stu-id="cdf85-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![定义电影表的 "标题" 列后 WebMatrix 数据库设计器](displaying-data/_static/image8.png)

<span data-ttu-id="cdf85-188">重复上述步骤以创建名为 "流派" 的列，长度除外，将其设置为 "仅 30"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="cdf85-189">创建另一个名为 "Year" 的列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-189">Create another column named "Year."</span></span> <span data-ttu-id="cdf85-190">对于 "数据类型"，请选择 " **nchar** （而非**nvarchar**）"，并将长度设置为4。</span><span class="sxs-lookup"><span data-stu-id="cdf85-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="cdf85-191">对于年份，你将使用如 "1995" 或 "2010" 这样的4位数字，因此你不需要可变大小的列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="cdf85-192">完成的设计如下所示：</span><span class="sxs-lookup"><span data-stu-id="cdf85-192">Here's what the finished design looks like:</span></span>

![为电影表定义所有字段后，WebMatrix 数据库设计器](displaying-data/_static/image9.png)

<span data-ttu-id="cdf85-194">按 Ctrl + S 或单击快速访问工具栏中的 "**保存**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="cdf85-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="cdf85-195">关闭 "数据库设计器"，关闭该选项卡。</span><span class="sxs-lookup"><span data-stu-id="cdf85-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="cdf85-196">添加一些示例数据</span><span class="sxs-lookup"><span data-stu-id="cdf85-196">Adding Some Example Data</span></span>

<span data-ttu-id="cdf85-197">在本系列教程的后面部分中，你将创建一个可在表单中输入新电影的页面。</span><span class="sxs-lookup"><span data-stu-id="cdf85-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="cdf85-198">不过，现在可以添加一些示例数据，然后您可以在页面上显示这些数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="cdf85-199">请注意，在 WebMatrix 的 "**数据库**" 工作区中，有一个树显示你之前创建的 *.sdf*文件。</span><span class="sxs-lookup"><span data-stu-id="cdf85-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="cdf85-200">打开新的 *.sdf*文件的节点，然后打开 "**表**" 节点。</span><span class="sxs-lookup"><span data-stu-id="cdf85-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![将树打开到电影表格的 WebMatrix 数据库工作区](displaying-data/_static/image10.png)

<span data-ttu-id="cdf85-202">右键单击 "**电影**" 节点，然后选择 "**数据**"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="cdf85-203">WebMatrix 打开一个网格，你可以在其中输入*电影*表的数据：</span><span class="sxs-lookup"><span data-stu-id="cdf85-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix 中的数据库输入网格（空）](displaying-data/_static/image11.png)

<span data-ttu-id="cdf85-205">单击 "**标题**" 列并输入 "当 Harry 满足 Sally 时"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="cdf85-206">转到 "**流派**" 列（可以使用 Tab 键），然后输入 "Romantic 喜剧"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="cdf85-207">转到**Year**列并输入 "1989"：</span><span class="sxs-lookup"><span data-stu-id="cdf85-207">Move to the **Year** column and enter "1989":</span></span>

![在 WebMatrix 中包含一条记录的数据库输入网格](displaying-data/_static/image12.png)

<span data-ttu-id="cdf85-209">按 Enter，WebMatrix 保存新电影。</span><span class="sxs-lookup"><span data-stu-id="cdf85-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="cdf85-210">请注意， **ID**列已填充。</span><span class="sxs-lookup"><span data-stu-id="cdf85-210">Notice that the **ID** column has been filled in.</span></span>

![WebMatrix 中的数据库条目网格，其中包含一条记录和自动生成的 ID](displaying-data/_static/image13.png)

<span data-ttu-id="cdf85-212">输入另一个电影（例如，"不带风"、"Drama"、"1939"）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="cdf85-213">ID 列再次填充：</span><span class="sxs-lookup"><span data-stu-id="cdf85-213">The ID column is filled in again:</span></span>

![具有两个记录和自动生成的 Id 的 WebMatrix 中的数据库输入网格](displaying-data/_static/image14.png)

<span data-ttu-id="cdf85-215">输入第三个电影（例如 "Ghostbusters"、"喜剧"）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="cdf85-216">作为实验，将**Year**列保留为空白，然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="cdf85-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="cdf85-217">由于未选择 "**允许 Null 值**" 选项，数据库显示错误：</span><span class="sxs-lookup"><span data-stu-id="cdf85-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![如果必需的列值为空，则显示 "无效数据" 错误](displaying-data/_static/image15.png)

<span data-ttu-id="cdf85-219">单击 **"确定**" 返回并修复该条目（"Ghostbusters" 的年份为1984），然后按 enter。</span><span class="sxs-lookup"><span data-stu-id="cdf85-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="cdf85-220">填写几个电影，直到有8个或如此。</span><span class="sxs-lookup"><span data-stu-id="cdf85-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="cdf85-221">（输入8使稍后可以更轻松地使用分页。</span><span class="sxs-lookup"><span data-stu-id="cdf85-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="cdf85-222">但如果这太多，请只输入几部分。）实际数据并不重要。</span><span class="sxs-lookup"><span data-stu-id="cdf85-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![具有任意记录的 WebMatrix 中的数据库条目网格](displaying-data/_static/image16.png)

<span data-ttu-id="cdf85-224">如果输入了所有电影，但没有出现任何错误，则 ID 值为顺序值。</span><span class="sxs-lookup"><span data-stu-id="cdf85-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="cdf85-225">如果尝试保存未完成的电影记录，则 ID 号可能不是连续的。</span><span class="sxs-lookup"><span data-stu-id="cdf85-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="cdf85-226">如果是这样，那就没关系。</span><span class="sxs-lookup"><span data-stu-id="cdf85-226">If so, that's okay.</span></span> <span data-ttu-id="cdf85-227">这些数字没有任何固有含义，唯一重要的是，它们在*电影*表中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="cdf85-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="cdf85-228">关闭包含数据库设计器的选项卡。</span><span class="sxs-lookup"><span data-stu-id="cdf85-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="cdf85-229">现在，您可以转到在网页上显示此数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="cdf85-230">使用 WebGrid Helper 在页中显示数据</span><span class="sxs-lookup"><span data-stu-id="cdf85-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="cdf85-231">若要在页面中显示数据，请使用 `WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="cdf85-232">此帮助器在网格或表中生成显示（行和列）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="cdf85-233">如您所见，您可以通过格式设置和其他功能优化网格。</span><span class="sxs-lookup"><span data-stu-id="cdf85-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="cdf85-234">若要运行网格，必须编写几行代码。</span><span class="sxs-lookup"><span data-stu-id="cdf85-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="cdf85-235">对于您在本教程中执行的几乎所有数据访问，这几个行都将用作一种模式。</span><span class="sxs-lookup"><span data-stu-id="cdf85-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="cdf85-236">实际上有许多选项可用于在页面上显示数据;`WebGrid` 帮助程序只是一个。</span><span class="sxs-lookup"><span data-stu-id="cdf85-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="cdf85-237">对于本教程，我们选择了它，因为这是最简单的显示数据的方法，因为它相当灵活。</span><span class="sxs-lookup"><span data-stu-id="cdf85-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="cdf85-238">在下一教程中，你将了解如何使用更多的 "手动" 方法来处理页面中的数据，这使你可以更直接地控制如何显示数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>

<span data-ttu-id="cdf85-239">在 WebMatrix 的左窗格中，单击 "**文件**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="cdf85-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="cdf85-240">你创建的新数据库位于*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="cdf85-241">如果文件夹尚不存在，则 WebMatrix 将为新数据库创建该文件夹。</span><span class="sxs-lookup"><span data-stu-id="cdf85-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="cdf85-242">（如果您以前安装了帮助程序，则可能存在该文件夹。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="cdf85-243">在树视图中，选择网站的根目录。</span><span class="sxs-lookup"><span data-stu-id="cdf85-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="cdf85-244">您必须选择网站的根目录;否则，可能会将新文件添加到应用\_Data 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="cdf85-245">在功能区中，单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="cdf85-246">在 "**选择文件类型**" 框中，选择 " **CSHTML**"。</span><span class="sxs-lookup"><span data-stu-id="cdf85-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="cdf85-247">在 "**名称**" 框中，将新页面命名为 "电影. cshtml"：</span><span class="sxs-lookup"><span data-stu-id="cdf85-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

![显示 "电影" 页面的 "选择文件类型" 对话框](displaying-data/_static/image17.png)

<span data-ttu-id="cdf85-249">单击“确定”按钮。</span><span class="sxs-lookup"><span data-stu-id="cdf85-249">Click the **OK** button.</span></span> <span data-ttu-id="cdf85-250">WebMatrix 打开一个新文件，其中包含某些主干元素。</span><span class="sxs-lookup"><span data-stu-id="cdf85-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="cdf85-251">首先，您将编写一些代码以从数据库中获取数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="cdf85-252">然后，您将向页添加标记以实际显示数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="cdf85-253">编写数据查询代码</span><span class="sxs-lookup"><span data-stu-id="cdf85-253">Writing the Data Query Code</span></span>

<span data-ttu-id="cdf85-254">在页面顶部的 "`@{`" 和 "`}`" 字符之间，输入以下代码。</span><span class="sxs-lookup"><span data-stu-id="cdf85-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="cdf85-255">（请确保在左大括号和右大括号之间输入此代码。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="cdf85-256">第一行打开之前创建的数据库，该数据库始终是执行数据库操作之前的第一个步骤。</span><span class="sxs-lookup"><span data-stu-id="cdf85-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="cdf85-257">通知要打开的数据库 `Database.Open` 方法名称。</span><span class="sxs-lookup"><span data-stu-id="cdf85-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="cdf85-258">请注意，名称中不包含 *.sdf。*</span><span class="sxs-lookup"><span data-stu-id="cdf85-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="cdf85-259">`Open` 方法假定它正在查找 *.sdf*文件（即*WebPagesMovies*），并且 *.Sdf*文件位于*应用\_Data*文件夹中。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="cdf85-260">（如前所述，我们记下*应用\_Data*文件夹，这种情况是 ASP.NET 对该名称进行假设的地方之一。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="cdf85-261">打开数据库时，会将对该数据库的引用放入名为 `db`的变量中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="cdf85-262">（可将其命名为任意名称。）`db` 变量是结束与数据库的交互的方式。</span><span class="sxs-lookup"><span data-stu-id="cdf85-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="cdf85-263">第二行实际使用 `Query` 方法提取数据库数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="cdf85-264">请注意此代码的工作原理： `db` 变量具有对打开的数据库的引用，并且通过使用 `db` 变量（`db.Query`）调用 `Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="cdf85-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="cdf85-265">查询本身就是 SQL `Select` 语句。</span><span class="sxs-lookup"><span data-stu-id="cdf85-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="cdf85-266">（有关 SQL 的简短背景，请参阅后面的说明。）在语句中，`Movies` 标识要查询的表。</span><span class="sxs-lookup"><span data-stu-id="cdf85-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="cdf85-267">`*` 字符指定查询应返回表中的所有列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="cdf85-268">（还可以单独列出列，用逗号分隔。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="cdf85-269">查询的结果（如果有）将返回并在 `selectedData` 变量中可用。</span><span class="sxs-lookup"><span data-stu-id="cdf85-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="cdf85-270">同样，该变量可以命名为任意名称。</span><span class="sxs-lookup"><span data-stu-id="cdf85-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="cdf85-271">最后，第三行告诉 ASP.NET 你想要使用 `WebGrid` 帮助器的实例。</span><span class="sxs-lookup"><span data-stu-id="cdf85-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="cdf85-272">您可以使用 `new` 关键字创建（*实例化*） helper 对象，并通过 `selectedData` 变量向其传递查询结果。</span><span class="sxs-lookup"><span data-stu-id="cdf85-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="cdf85-273">新的 `WebGrid` 对象和数据库查询的结果都在 `grid` 变量中可用。</span><span class="sxs-lookup"><span data-stu-id="cdf85-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="cdf85-274">需要一段时间才能实际在页面中显示数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="cdf85-275">在此阶段，数据库已打开，你已获得所需的数据，并且已为该数据准备好 `WebGrid` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="cdf85-276">接下来，在页面中创建标记。</span><span class="sxs-lookup"><span data-stu-id="cdf85-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="cdf85-277">**结构化查询语言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="cdf85-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="cdf85-278">SQL 是在大多数关系数据库中用于管理数据库中的数据的一种语言。</span><span class="sxs-lookup"><span data-stu-id="cdf85-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="cdf85-279">它包含的命令可用于检索和更新数据，并允许您创建、修改和管理数据库表中的数据。</span><span class="sxs-lookup"><span data-stu-id="cdf85-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="cdf85-280">SQL 不同于编程语言（例如C#）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="cdf85-281">对于 SQL，你会告诉数据库你所需的内容，数据库的工作是确定如何获取数据或执行任务。</span><span class="sxs-lookup"><span data-stu-id="cdf85-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="cdf85-282">下面是一些 SQL 命令的示例和它们的作用：</span><span class="sxs-lookup"><span data-stu-id="cdf85-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="cdf85-283">第一个 `Select` 语句获取 "*电影*" 表中的所有列（由 `*`指定）。</span><span class="sxs-lookup"><span data-stu-id="cdf85-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="cdf85-284">第二个 `Select` 语句从*产品*表中的价格列值大于10的记录中提取 ID、名称和价格列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="cdf85-285">命令根据 Name 列的值以字母顺序返回结果。</span><span class="sxs-lookup"><span data-stu-id="cdf85-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="cdf85-286">如果没有任何记录与价格条件匹配，则该命令返回空集。</span><span class="sxs-lookup"><span data-stu-id="cdf85-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="cdf85-287">此命令在*Product*表中插入一条新记录，将 "名称" 列设置为 "新月形面包"，将 "说明" 列设置为 "a 不可靠感到满意"，并将价格设置为1.99。</span><span class="sxs-lookup"><span data-stu-id="cdf85-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="cdf85-288">请注意，在指定非数值时，该值括在单引号（而不是双引号）中，如中C#所示。</span><span class="sxs-lookup"><span data-stu-id="cdf85-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="cdf85-289">用引号将文本或日期值括起来，而不是用引号将其引起来。</span><span class="sxs-lookup"><span data-stu-id="cdf85-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="cdf85-290">此命令删除*Product*表中的记录，其到期日期列早于2008年1月1日。</span><span class="sxs-lookup"><span data-stu-id="cdf85-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="cdf85-291">（该命令假定*Product*表具有这样的列。）此处以 MM/DD/YYYY 格式输入日期，但应以用于区域设置的格式输入。</span><span class="sxs-lookup"><span data-stu-id="cdf85-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="cdf85-292">`Insert` 和 `Delete` 命令不返回结果集。</span><span class="sxs-lookup"><span data-stu-id="cdf85-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="cdf85-293">相反，它们将返回一个数字，该数字告诉你命令所影响的记录数。</span><span class="sxs-lookup"><span data-stu-id="cdf85-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="cdf85-294">对于某些操作（例如插入和删除记录），请求操作的进程必须在数据库中具有适当的权限。</span><span class="sxs-lookup"><span data-stu-id="cdf85-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="cdf85-295">这就是为什么在连接到数据库时，生产数据库经常必须提供用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="cdf85-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="cdf85-296">有许多 SQL 命令，但它们都遵循您在此处看到的命令。</span><span class="sxs-lookup"><span data-stu-id="cdf85-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="cdf85-297">您可以使用 SQL 命令来创建数据库表，计算表中的记录数，计算价格，以及执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="cdf85-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="cdf85-298">添加标记以显示数据</span><span class="sxs-lookup"><span data-stu-id="cdf85-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="cdf85-299">在 `<head>` 元素中，将 `<title>` 元素的内容设置为 "影片"：</span><span class="sxs-lookup"><span data-stu-id="cdf85-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="cdf85-300">在页面的 `<body>` 元素中，添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="cdf85-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="cdf85-301">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="cdf85-301">That's it.</span></span> <span data-ttu-id="cdf85-302">`grid` 变量是在前面的代码中创建 `WebGrid` 对象时创建的值。</span><span class="sxs-lookup"><span data-stu-id="cdf85-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="cdf85-303">在 WebMatrix 树视图中，右键单击页面并选择 "**在浏览器中启动"** 。</span><span class="sxs-lookup"><span data-stu-id="cdf85-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="cdf85-304">你将看到类似于此页面的内容：</span><span class="sxs-lookup"><span data-stu-id="cdf85-304">You'll see something like this page:</span></span>

![电影表中的默认 WebGrid helper 输出](displaying-data/_static/image18.png)

<span data-ttu-id="cdf85-306">单击列标题链接可按该列进行排序。</span><span class="sxs-lookup"><span data-stu-id="cdf85-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="cdf85-307">通过单击标题，就是**WebGrid**帮助程序中内置的一项功能。</span><span class="sxs-lookup"><span data-stu-id="cdf85-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="cdf85-308">如名称所示，`GetHtml` 方法会生成显示数据的标记。</span><span class="sxs-lookup"><span data-stu-id="cdf85-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="cdf85-309">默认情况下，`GetHtml` 方法会生成 HTML `<table>` 元素。</span><span class="sxs-lookup"><span data-stu-id="cdf85-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="cdf85-310">（如果需要，可以通过在浏览器中查看页面源来验证呈现。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="cdf85-311">修改网格的外观</span><span class="sxs-lookup"><span data-stu-id="cdf85-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="cdf85-312">像您一样使用 `WebGrid` 帮助程序非常简单，但生成的显示是普通的。</span><span class="sxs-lookup"><span data-stu-id="cdf85-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="cdf85-313">`WebGrid` 帮助程序具有各种选项，可用于控制数据的显示方式。</span><span class="sxs-lookup"><span data-stu-id="cdf85-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="cdf85-314">本教程中的内容太多，但本部分介绍其中一些选项。</span><span class="sxs-lookup"><span data-stu-id="cdf85-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="cdf85-315">本系列后面的教程将介绍一些其他选项。</span><span class="sxs-lookup"><span data-stu-id="cdf85-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="cdf85-316">指定要显示的单个列</span><span class="sxs-lookup"><span data-stu-id="cdf85-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="cdf85-317">若要开始，可以指定只显示某些列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="cdf85-318">默认情况下，正如您所看到的，该网格显示了*电影*表中的所有四个列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="cdf85-319">在 "*影院*" 文件中，将刚才添加的 `@grid.GetHtml()` 标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="cdf85-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="cdf85-320">若要告知帮助器显示哪些列，请为 `GetHtml` 方法包含 `columns` 参数，并传入一组列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="cdf85-321">在集合中，指定要包含的每一列。</span><span class="sxs-lookup"><span data-stu-id="cdf85-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="cdf85-322">您可以通过包含 `grid.Column` 对象来指定要显示的单个列，并传入所需的数据列的名称。</span><span class="sxs-lookup"><span data-stu-id="cdf85-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="cdf85-323">（这些列必须包括在 SQL 查询结果中— `WebGrid` 帮助程序不能显示查询未返回的列。）</span><span class="sxs-lookup"><span data-stu-id="cdf85-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="cdf85-324">再次在浏览器中启动 "在浏览器中显示 *" 页面，* 此时会显示如下所示的显示内容（请注意，未显示 ID 列）：</span><span class="sxs-lookup"><span data-stu-id="cdf85-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![仅显示所选列的 WebGrid 显示](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="cdf85-326">更改网格的外观</span><span class="sxs-lookup"><span data-stu-id="cdf85-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="cdf85-327">还有其他几个选项可用于显示列，其中一些选项将在本集中的后续教程中进行探讨。</span><span class="sxs-lookup"><span data-stu-id="cdf85-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="cdf85-328">现在，本部分将介绍如何将网格作为一个整体进行样式。</span><span class="sxs-lookup"><span data-stu-id="cdf85-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="cdf85-329">在页面的 `<head>` 部分中，紧靠在关闭 `</head>` 标记之前，添加以下 `<style>` 元素：</span><span class="sxs-lookup"><span data-stu-id="cdf85-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="cdf85-330">此 CSS 标记定义名为 `grid`、`head`等的类。</span><span class="sxs-lookup"><span data-stu-id="cdf85-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="cdf85-331">你还可以将这些样式定义放在单独的 *.css*文件中，并将其链接到该页。</span><span class="sxs-lookup"><span data-stu-id="cdf85-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="cdf85-332">（事实上，您将在本教程的后面部分执行此操作。）但为了简化本教程，它们位于显示数据的同一页面中。</span><span class="sxs-lookup"><span data-stu-id="cdf85-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="cdf85-333">现在，可以获取 `WebGrid` 帮助器来使用这些样式类。</span><span class="sxs-lookup"><span data-stu-id="cdf85-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="cdf85-334">帮助器有许多属性（例如 `tableStyle`），只是为了实现此目的，即向它们分配一个 CSS 样式类名称，并且该类名称呈现为帮助器呈现的标记的一部分。</span><span class="sxs-lookup"><span data-stu-id="cdf85-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="cdf85-335">更改 `grid.GetHtml` 标记，使其现在类似于以下代码：</span><span class="sxs-lookup"><span data-stu-id="cdf85-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="cdf85-336">新增功能是你已将 `tableStyle`、`headerStyle`和 `alternatingRowStyle` 参数添加到 `GetHtml` 方法。</span><span class="sxs-lookup"><span data-stu-id="cdf85-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="cdf85-337">已将这些参数设置为稍后添加的 CSS 样式的名称。</span><span class="sxs-lookup"><span data-stu-id="cdf85-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="cdf85-338">运行该页面，此时你会看到一个看起来比之前更简单的网格：</span><span class="sxs-lookup"><span data-stu-id="cdf85-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![WebGrid 显示，其中包括设置为 CSS 类名称的参数](displaying-data/_static/image20.png)

<span data-ttu-id="cdf85-340">若要查看 `GetHtml` 方法的生成内容，可以在浏览器中查看页面的源。</span><span class="sxs-lookup"><span data-stu-id="cdf85-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="cdf85-341">本文不会详细介绍，但重要的一点是，通过指定 `tableStyle`的参数，导致网格生成如下所示的 HTML 标记：</span><span class="sxs-lookup"><span data-stu-id="cdf85-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="cdf85-342">`<table>` 标记添加了一个 `class` 属性，该属性引用前面添加的其中一个 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="cdf85-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="cdf85-343">此代码显示了基本模式 &mdash; 不同的 `GetHtml` 方法参数可让你引用该方法随后随标记一起生成的 CSS 类。</span><span class="sxs-lookup"><span data-stu-id="cdf85-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="cdf85-344">CSS 类的作用由您决定。</span><span class="sxs-lookup"><span data-stu-id="cdf85-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="cdf85-345">添加分页</span><span class="sxs-lookup"><span data-stu-id="cdf85-345">Adding Paging</span></span>

<span data-ttu-id="cdf85-346">作为本教程的最后一个任务，您将向网格中添加分页。</span><span class="sxs-lookup"><span data-stu-id="cdf85-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="cdf85-347">现在，不会出现一次显示所有电影的问题。</span><span class="sxs-lookup"><span data-stu-id="cdf85-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="cdf85-348">但如果添加了数百个电影，则页面显示将变长。</span><span class="sxs-lookup"><span data-stu-id="cdf85-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="cdf85-349">在页代码中，将创建 `WebGrid` 对象的行更改为以下代码：</span><span class="sxs-lookup"><span data-stu-id="cdf85-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="cdf85-350">与之前的唯一区别在于，你添加了一个设置为3的 `rowsPerPage` 参数。</span><span class="sxs-lookup"><span data-stu-id="cdf85-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="cdf85-351">运行页面。</span><span class="sxs-lookup"><span data-stu-id="cdf85-351">Run the page.</span></span> <span data-ttu-id="cdf85-352">网格每次显示3行，还显示允许您在数据库中浏览电影的导航链接：</span><span class="sxs-lookup"><span data-stu-id="cdf85-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![分页显示 WebGrid](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="cdf85-354">下一步</span><span class="sxs-lookup"><span data-stu-id="cdf85-354">Coming Up Next</span></span>

<span data-ttu-id="cdf85-355">在下一教程中，您将学习如何使用 Razor 和C#代码来获取窗体中的用户输入。</span><span class="sxs-lookup"><span data-stu-id="cdf85-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="cdf85-356">将搜索框添加到 "电影" 页，以便可以按标题或流派查找电影。</span><span class="sxs-lookup"><span data-stu-id="cdf85-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="cdf85-357">"完成电影列表" 页面</span><span class="sxs-lookup"><span data-stu-id="cdf85-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="cdf85-358">其他资源</span><span class="sxs-lookup"><span data-stu-id="cdf85-358">Additional Resources</span></span>

- [<span data-ttu-id="cdf85-359">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="cdf85-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="cdf85-360">[上一页](intro-to-web-pages-programming.md)
> [下一页](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="cdf85-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
