---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 第2部分：数据访问层 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第2部分介绍如何添加数据访问层。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462650"
---
# <a name="part-2-data-access-layer"></a><span data-ttu-id="7ba48-104">第2部分：数据访问层</span><span class="sxs-lookup"><span data-stu-id="7ba48-104">Part 2: Data Access Layer</span></span>

<span data-ttu-id="7ba48-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="7ba48-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="7ba48-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="7ba48-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="7ba48-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="7ba48-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="7ba48-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="7ba48-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="7ba48-109">第2部分介绍如何添加数据访问层。</span><span class="sxs-lookup"><span data-stu-id="7ba48-109">Part 2 covers adding the data access layer.</span></span>

## <a id="_Toc260221668"></a><span data-ttu-id="7ba48-110">添加数据访问层</span><span class="sxs-lookup"><span data-stu-id="7ba48-110">Adding the Data Access Layer</span></span>

<span data-ttu-id="7ba48-111">电子商务应用程序将依赖于两个数据库。</span><span class="sxs-lookup"><span data-stu-id="7ba48-111">Our ecommerce application will depend on two databases.</span></span>

<span data-ttu-id="7ba48-112">对于客户信息，我们将使用标准的 ASP.NET 成员资格数据库。</span><span class="sxs-lookup"><span data-stu-id="7ba48-112">For customer information we'll use the standard ASP.NET Membership database.</span></span> <span data-ttu-id="7ba48-113">对于购物车和产品目录，我们将按如下所示实现 SQL Express 数据库。</span><span class="sxs-lookup"><span data-stu-id="7ba48-113">For our shopping cart and product catalog we'll implement a SQL Express database as follows.</span></span>

![](tailspin-spyworks-part-2/_static/image1.jpg)

<span data-ttu-id="7ba48-114">在应用程序的应用程序\_Data 文件夹中创建数据库（.mdf）后，我们可以继续使用 .NET 实体框架创建数据访问层。</span><span class="sxs-lookup"><span data-stu-id="7ba48-114">Having created the database (Commerce.mdf) in the application's App\_Data folder we can proceed to create our Data Access Layer using the .NET Entity Framework.</span></span>

<span data-ttu-id="7ba48-115">我们将创建一个名为 "Data\_Access" 的文件夹，并右键单击该文件夹并选择 "添加新项"。</span><span class="sxs-lookup"><span data-stu-id="7ba48-115">We'll create a folder named "Data\_Access" and them right click on that folder and select "Add New Item".</span></span>

<span data-ttu-id="7ba48-116">在 "已安装的模板" 项中，选择 "ADO.NET 实体数据模型" 输入 EDM\_Commerce 作为名称，然后单击 "添加" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7ba48-116">In the "Installed Templates" item and then select "ADO.NET Entity Data Model" enter EDM\_Commerce.edmx as the name and click the "Add" button.</span></span>

![](tailspin-spyworks-part-2/_static/image2.jpg)

<span data-ttu-id="7ba48-117">选择 "从数据库生成"。</span><span class="sxs-lookup"><span data-stu-id="7ba48-117">Choose "Generate from Database".</span></span>

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

<span data-ttu-id="7ba48-118">保存并生成。</span><span class="sxs-lookup"><span data-stu-id="7ba48-118">Save and build.</span></span>

<span data-ttu-id="7ba48-119">现在，我们已准备好添加第一个功能–产品类别菜单。</span><span class="sxs-lookup"><span data-stu-id="7ba48-119">Now we are ready to add our first feature – a product category menu.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7ba48-120">[上一页](tailspin-spyworks-part-1.md)
> [下一页](tailspin-spyworks-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="7ba48-120">[Previous](tailspin-spyworks-part-1.md)
[Next](tailspin-spyworks-part-3.md)</span></span>
