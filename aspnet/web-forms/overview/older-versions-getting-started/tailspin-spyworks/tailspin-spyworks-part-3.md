---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 第3部分：布局和类别菜单 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第3部分介绍添加布局和类别菜单。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519098"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="208c2-104">第3部分：布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="208c2-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="208c2-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="208c2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="208c2-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="208c2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="208c2-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="208c2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="208c2-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="208c2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="208c2-109">第3部分介绍添加布局和类别菜单。</span><span class="sxs-lookup"><span data-stu-id="208c2-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="208c2-110">添加一些布局和类别菜单</span><span class="sxs-lookup"><span data-stu-id="208c2-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="208c2-111">在我们的站点母版页中，我们将为左侧列添加一个 div，其中包含我们的产品类别菜单。</span><span class="sxs-lookup"><span data-stu-id="208c2-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="208c2-112">请注意，所需的对齐和其他格式将由我们添加到我们的 Style .css 文件的 CSS 类提供。</span><span class="sxs-lookup"><span data-stu-id="208c2-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="208c2-113">"产品类别" 菜单将在运行时动态创建，方法是查询商业数据库中的现有产品类别，并创建菜单项和相应的链接。</span><span class="sxs-lookup"><span data-stu-id="208c2-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="208c2-114">为实现此目的，我们将使用两个 ASP。网络强大的数据控件。</span><span class="sxs-lookup"><span data-stu-id="208c2-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="208c2-115">"实体数据源" 控件和 "ListView" 控件。</span><span class="sxs-lookup"><span data-stu-id="208c2-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="208c2-116">让我们切换到 "设计视图"，并使用帮助程序来配置控件。</span><span class="sxs-lookup"><span data-stu-id="208c2-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="208c2-117">让我们将 EntityDataSource ID 属性设置为 EDS\_类别\_"菜单，然后单击" 配置数据源 "。</span><span class="sxs-lookup"><span data-stu-id="208c2-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="208c2-118">选择为我们的 Commerce 数据库创建实体数据源模型时为我们创建的 CommerceEntities 连接，然后单击 "下一步"。</span><span class="sxs-lookup"><span data-stu-id="208c2-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="208c2-119">选择 "类别" 实体集名称，并将其余选项保留为默认值。</span><span class="sxs-lookup"><span data-stu-id="208c2-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="208c2-120">单击 "完成"。</span><span class="sxs-lookup"><span data-stu-id="208c2-120">Click "Finish".</span></span>

<span data-ttu-id="208c2-121">现在，让我们将放置在页面上的 ListView 控件实例的 ID 属性设置为 ListView\_ProductsMenu 并激活其帮助程序。</span><span class="sxs-lookup"><span data-stu-id="208c2-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="208c2-122">尽管我们可以使用控件选项来设置数据项显示和格式的格式，但我们的菜单创建只需要简单标记，因此我们将在源视图中输入代码。</span><span class="sxs-lookup"><span data-stu-id="208c2-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="208c2-123">请注意 "Eval" 语句： &lt;% # Eval （"类别名称"）%&gt;</span><span class="sxs-lookup"><span data-stu-id="208c2-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="208c2-124">ASP.NET 语法 &lt;% #%&gt; 是一种简写约定，它指示运行时执行中包含的任何内容并在行中输出结果。</span><span class="sxs-lookup"><span data-stu-id="208c2-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="208c2-125">语句 Eval （"类别名称"）指示，对于数据项的绑定集合中的当前项，提取实体模型项名称 "类别名称" 的值。</span><span class="sxs-lookup"><span data-stu-id="208c2-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="208c2-126">这是一种非常强大的功能。</span><span class="sxs-lookup"><span data-stu-id="208c2-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="208c2-127">现在，让我们运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="208c2-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="208c2-128">请注意，我们的产品类别菜单现在显示，当鼠标悬停在某个类别菜单项上时，将会看到菜单项链接指向我们尚未实现的名为 ProductsList 的页，并且我们已经生成了一个包含 类别 id。</span><span class="sxs-lookup"><span data-stu-id="208c2-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="208c2-129">[上一页](tailspin-spyworks-part-2.md)
> [下一页](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="208c2-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>
