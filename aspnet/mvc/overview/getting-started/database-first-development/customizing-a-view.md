---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 教程：通过 ASP.NET MVC 应用自定义 EF Database First 的视图
description: 本教程重点介绍如何更改自动生成的视图以增强演示。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471518"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="f8060-103">教程：通过 ASP.NET MVC 应用自定义 EF Database First 的视图</span><span class="sxs-lookup"><span data-stu-id="f8060-103">Tutorial: Customize view for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="f8060-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="f8060-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="f8060-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="f8060-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="f8060-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="f8060-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="f8060-107">本教程重点介绍如何更改自动生成的视图以增强演示。</span><span class="sxs-lookup"><span data-stu-id="f8060-107">This tutorial focuses on changing the automatically-generated views to enhance the presentation.</span></span>

<span data-ttu-id="f8060-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="f8060-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8060-109">向 "学生详细信息" 页添加课程</span><span class="sxs-lookup"><span data-stu-id="f8060-109">Add courses to the student detail page</span></span>
> * <span data-ttu-id="f8060-110">确认已将课程添加到页面</span><span class="sxs-lookup"><span data-stu-id="f8060-110">Confirm that the courses are added to the page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8060-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="f8060-111">Prerequisites</span></span>

* [<span data-ttu-id="f8060-112">更改数据库</span><span class="sxs-lookup"><span data-stu-id="f8060-112">Change the database</span></span>](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a><span data-ttu-id="f8060-113">向学生详细信息添加课程</span><span class="sxs-lookup"><span data-stu-id="f8060-113">Add courses to student detail</span></span>

<span data-ttu-id="f8060-114">生成的代码为应用程序提供了一个很好的起点，但它并不一定提供您的应用程序所需的所有功能。</span><span class="sxs-lookup"><span data-stu-id="f8060-114">The generated code provides a good starting point for your application but it does not necessarily provide all of the functionality that you need in your application.</span></span> <span data-ttu-id="f8060-115">你可以自定义代码来满足应用程序的特定要求。</span><span class="sxs-lookup"><span data-stu-id="f8060-115">You can customize the code to meet the particular requirements of your application.</span></span> <span data-ttu-id="f8060-116">目前，应用程序不会显示所选学生的已注册课程。</span><span class="sxs-lookup"><span data-stu-id="f8060-116">Currently, your application does not display the enrolled courses for the selected student.</span></span> <span data-ttu-id="f8060-117">在本部分中，你将向学生的**详细信息**视图中添加每个学生的已注册课程。</span><span class="sxs-lookup"><span data-stu-id="f8060-117">In this section, you will add the enrolled courses for each student to the **Details** view for the student.</span></span>

<span data-ttu-id="f8060-118"> > *详细信息，*  > **学生**打开**视图**。</span><span class="sxs-lookup"><span data-stu-id="f8060-118">Open **Views** > **Students** > *Details.cshtml*.</span></span> <span data-ttu-id="f8060-119">在最后一个 &lt;/dl&gt; 标记下，但在结束 &lt;/div&gt; 标记之前，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="f8060-119">Below the last &lt;/dl&gt; tag, but before the closing &lt;/div&gt; tag, add the following code.</span></span>

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

<span data-ttu-id="f8060-120">此代码将创建一个表，该表为所选学生的注册表中的每个记录显示一行。</span><span class="sxs-lookup"><span data-stu-id="f8060-120">This code creates a table that displays a row for each record in the Enrollment table for the selected student.</span></span> <span data-ttu-id="f8060-121">**显示**方法为表示表达式的对象（modelItem）呈现 HTML。</span><span class="sxs-lookup"><span data-stu-id="f8060-121">The **Display** method renders HTML for the object (modelItem) that represents the expression.</span></span> <span data-ttu-id="f8060-122">您可以使用显示方法（而不是只是将属性值嵌入到代码中）以确保值基于其类型和该类型的模板正确地进行格式设置。</span><span class="sxs-lookup"><span data-stu-id="f8060-122">You use the Display method (rather than simply embedding the property value in the code) to make sure the value is formatted correctly based on its type and the template for that type.</span></span> <span data-ttu-id="f8060-123">在此示例中，每个表达式都将返回循环中的当前记录的单个属性，并且值是呈现为文本的基元类型。</span><span class="sxs-lookup"><span data-stu-id="f8060-123">In this example, each expression returns a single property from the current record in the loop, and the values are primitive types which are rendered as text.</span></span>

## <a name="confirm-courses-are-added"></a><span data-ttu-id="f8060-124">确认添加课程</span><span class="sxs-lookup"><span data-stu-id="f8060-124">Confirm courses are added</span></span>

<span data-ttu-id="f8060-125">运行该解决方案。</span><span class="sxs-lookup"><span data-stu-id="f8060-125">Run the solution.</span></span> <span data-ttu-id="f8060-126">单击 "**学生列表**"，然后选择其中一个学生的 "**详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="f8060-126">Click **List of students** and select **Details** for one of the students.</span></span> <span data-ttu-id="f8060-127">你将看到已注册的课程已包含在视图中。</span><span class="sxs-lookup"><span data-stu-id="f8060-127">You will see the enrolled courses have been included in the view.</span></span>

![学生注册](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a><span data-ttu-id="f8060-129">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f8060-129">Next steps</span></span>
<span data-ttu-id="f8060-130">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="f8060-130">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8060-131">向学生详细信息页添加了课程</span><span class="sxs-lookup"><span data-stu-id="f8060-131">Added courses to the student detail page</span></span>
> * <span data-ttu-id="f8060-132">已确认将课程添加到页面</span><span class="sxs-lookup"><span data-stu-id="f8060-132">Confirmed that the courses are added to the page</span></span>

<span data-ttu-id="f8060-133">转到下一教程，了解如何添加数据批注来指定验证要求和显示格式。</span><span class="sxs-lookup"><span data-stu-id="f8060-133">Advance to the next tutorial to learn how to add data annotations to specify validation requirements and display formatting.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f8060-134">增强数据验证</span><span class="sxs-lookup"><span data-stu-id="f8060-134">Enhance data validation</span></span>](enhancing-data-validation.md)
