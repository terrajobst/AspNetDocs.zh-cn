---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |Microsoft Docs
author: microsoft
description: 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件来复制常见页面 elem 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457580"
---
# <a name="master-pages"></a><span data-ttu-id="7754b-104">母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-104">Master Pages</span></span>

<span data-ttu-id="7754b-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7754b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7754b-106">成功的网站的关键组件之一是一致的外观。</span><span class="sxs-lookup"><span data-stu-id="7754b-106">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="7754b-107">在 ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="7754b-107">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="7754b-108">虽然这无疑是一个可行的解决方案，但使用用户控件确实存在一些缺点。</span><span class="sxs-lookup"><span data-stu-id="7754b-108">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="7754b-109">例如，对用户控件位置的更改需要对一个站点中的多个页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="7754b-109">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="7754b-110">在将用户控件插入页面后，还不会在设计视图中呈现这些控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-110">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="7754b-111">成功的网站的关键组件之一是一致的外观。</span><span class="sxs-lookup"><span data-stu-id="7754b-111">One of the key components to a successful Web site is a consistent look and feel.</span></span> <span data-ttu-id="7754b-112">在 ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制常见页面元素。</span><span class="sxs-lookup"><span data-stu-id="7754b-112">In ASP.NET 1.x, developers used user controls to replicate common page elements across a Web application.</span></span> <span data-ttu-id="7754b-113">虽然这无疑是一个可行的解决方案，但使用用户控件确实存在一些缺点。</span><span class="sxs-lookup"><span data-stu-id="7754b-113">While that is certainly a workable solution, using user controls does have some drawbacks.</span></span> <span data-ttu-id="7754b-114">例如，对用户控件位置的更改需要对一个站点中的多个页面进行更改。</span><span class="sxs-lookup"><span data-stu-id="7754b-114">For example, a change in position of a user control requires a change to multiple pages across a site.</span></span> <span data-ttu-id="7754b-115">在将用户控件插入页面后，还不会在设计视图中呈现这些控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-115">User controls are also not rendered in Design view after being inserted on a page.</span></span>

<span data-ttu-id="7754b-116">ASP.NET 2.0 将母版页作为一种保持一致的外观和感觉的方式引入，你很快就会看到，母版页表示对用户控件方法的重大改进。</span><span class="sxs-lookup"><span data-stu-id="7754b-116">ASP.NET 2.0 introduces Master pages as a way of maintaining a consistent look and feel, and as you'll soon see, Master pages represent a significant improvement over the user control method.</span></span>

## <a name="why-master-pages"></a><span data-ttu-id="7754b-117">母版页的原因</span><span class="sxs-lookup"><span data-stu-id="7754b-117">Why Master Pages?</span></span>

<span data-ttu-id="7754b-118">您可能想知道为什么在 ASP.NET 2.0 中需要母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-118">You may be wondering why master pages were needed in ASP.NET 2.0.</span></span> <span data-ttu-id="7754b-119">毕竟，网站开发人员已在 ASP.NET 1.x 中使用用户控件在页面之间共享内容区域。</span><span class="sxs-lookup"><span data-stu-id="7754b-119">After all, Web site developers are already using user controls in ASP.NET 1.x to share content areas between pages.</span></span> <span data-ttu-id="7754b-120">由于用户控件是创建通用布局的最佳解决方案，因此实际上有多种原因。</span><span class="sxs-lookup"><span data-stu-id="7754b-120">There are actually several reasons why user controls are a less-than-optimal solution for creating a common layout.</span></span>

<span data-ttu-id="7754b-121">用户控件并不实际定义页面布局。</span><span class="sxs-lookup"><span data-stu-id="7754b-121">User controls don't actually define page layout.</span></span> <span data-ttu-id="7754b-122">相反，它们定义了页面部分的布局和功能。</span><span class="sxs-lookup"><span data-stu-id="7754b-122">Instead, they define the layout and functionality for a portion of a page.</span></span> <span data-ttu-id="7754b-123">这两者之间的区别非常重要，因为它使用户控制解决方案的可管理性更难。</span><span class="sxs-lookup"><span data-stu-id="7754b-123">The distinction between these two is important because it makes manageability of a user control solution much more difficult.</span></span> <span data-ttu-id="7754b-124">例如，要更改用户控件在页面上的位置，则必须编辑显示用户控件的实际页面。</span><span class="sxs-lookup"><span data-stu-id="7754b-124">For example, when you want to change the position of a user control on your page, you must edit the actual page on which the user control appears.</span></span> <span data-ttu-id="7754b-125">如果只有几个页面，但在大型站点中，这种方法很快就会成为站点管理工作的麻烦！</span><span class="sxs-lookup"><span data-stu-id="7754b-125">Thats fine if you have only a few pages, but in large sites, it quickly becomes a site management nightmare!</span></span>

<span data-ttu-id="7754b-126">使用用户控件定义通用布局的另一个缺点是，ASP.NET 本身的体系结构。</span><span class="sxs-lookup"><span data-stu-id="7754b-126">Another drawback of using user controls for defining a common layout is rooted in the architecture of ASP.NET itself.</span></span> <span data-ttu-id="7754b-127">如果更改了用户控件的任何公共成员，则需要重新编译使用该用户控件的所有页。</span><span class="sxs-lookup"><span data-stu-id="7754b-127">If any public member of a user control is changed, it requires you to recompile all of the pages that use the user control.</span></span> <span data-ttu-id="7754b-128">接下来，ASP.NET 将在首次访问页面时重新 JIT。</span><span class="sxs-lookup"><span data-stu-id="7754b-128">In turn, ASP.NET will then re-JIT your pages when they are first accessed.</span></span> <span data-ttu-id="7754b-129">同样，这会为较大的站点生成不可缩放的体系结构和站点管理问题。</span><span class="sxs-lookup"><span data-stu-id="7754b-129">This, once again, produces a non-scalable architecture and a site management problem for larger sites.</span></span>

<span data-ttu-id="7754b-130">这两个问题（及更多）都通过 ASP.NET 2.0 中的母版页得到了良好的处理。</span><span class="sxs-lookup"><span data-stu-id="7754b-130">Both of these problems (and many more) are nicely addressed by master pages in ASP.NET 2.0.</span></span>

## <a name="how-master-pages-work"></a><span data-ttu-id="7754b-131">母版页的工作方式</span><span class="sxs-lookup"><span data-stu-id="7754b-131">How Master Pages Work</span></span>

<span data-ttu-id="7754b-132">母版页类似于其他页面的模板。</span><span class="sxs-lookup"><span data-stu-id="7754b-132">A master page is analogous to a template for other pages.</span></span> <span data-ttu-id="7754b-133">应在其他页面之间共享的页面元素（例如菜单、边框等）添加到母版页中。</span><span class="sxs-lookup"><span data-stu-id="7754b-133">Page elements that should be shared among other pages (i.e. menus, borders, etc.) are added to the master page.</span></span> <span data-ttu-id="7754b-134">将新页面添加到站点时，可以将它们与母版页关联。</span><span class="sxs-lookup"><span data-stu-id="7754b-134">When new pages are added to the site, you can associate them with a master page.</span></span> <span data-ttu-id="7754b-135">与母版页关联的页称为 "**内容页**"。</span><span class="sxs-lookup"><span data-stu-id="7754b-135">A page that is associated with a master page is called a **content page**.</span></span> <span data-ttu-id="7754b-136">默认情况下，内容页将从母版页获得外观。</span><span class="sxs-lookup"><span data-stu-id="7754b-136">By default, a content page takes on the appearance from the master page.</span></span> <span data-ttu-id="7754b-137">但是，在创建母版页时，可以定义页面中内容页可以替换为其自身内容的部分。</span><span class="sxs-lookup"><span data-stu-id="7754b-137">However, when you create a master page, you can define portions of the page that the content page can replace with its own content.</span></span> <span data-ttu-id="7754b-138">使用 ASP.NET 2.0 中引入的新控件定义这些部分。**ContentPlaceHolder**控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-138">These portions are defined using a new control introduced in ASP.NET 2.0; the **ContentPlaceHolder** control.</span></span>

<span data-ttu-id="7754b-139">一个母版页可以包含任意数量的 ContentPlaceHolder 控件（或全部无）。在 "内容" 页上，ContentPlaceHolder 控件中的内容显示在**内容**控件中，另一个新控件 ASP.NET 2.0。</span><span class="sxs-lookup"><span data-stu-id="7754b-139">A master page can contain any number of ContentPlaceHolder controls (or none at all.) On the content page, the content from the ContentPlaceHolder controls appears inside of **Content** controls, another new control in ASP.NET 2.0.</span></span> <span data-ttu-id="7754b-140">默认情况下，内容页内容控件为空，因此你可以提供自己的内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-140">By default, the content pages Content controls are empty so that you can provide your own content.</span></span> <span data-ttu-id="7754b-141">如果要使用内容控件中的母版页的内容，则可以执行此操作，如本模块后面的内容所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-141">If you want to use the content from the master page inside of the Content controls, you can do so as you will see later in this module.</span></span> <span data-ttu-id="7754b-142">内容控件通过内容控件的 ContentPlaceHolderID 特性映射到 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-142">The Content control is mapped to the ContentPlaceHolder control via the ContentPlaceHolderID attribute of the Content control.</span></span> <span data-ttu-id="7754b-143">下面的代码将内容控件映射到母版页上名为 mainBody 的 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-143">The code below maps a Content control to a ContentPlaceHolder control called mainBody on a master page.</span></span>

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="7754b-144">你通常会听到人们将母版页描述为其他页面的基类。</span><span class="sxs-lookup"><span data-stu-id="7754b-144">You will often hear people describe master pages as being a base class for other pages.</span></span> <span data-ttu-id="7754b-145">事实上，事实不是这样。</span><span class="sxs-lookup"><span data-stu-id="7754b-145">Thats actually not true.</span></span> <span data-ttu-id="7754b-146">母版页和内容页之间的关系不是继承之一。</span><span class="sxs-lookup"><span data-stu-id="7754b-146">The relationship between master pages and content pages is not one of inheritance.</span></span>

<span data-ttu-id="7754b-147">**图 1**显示了在 Visual Studio 2005 中显示的母版页和关联的内容页。</span><span class="sxs-lookup"><span data-stu-id="7754b-147">**Figure 1** shows a master page and an associated content page as they appear in Visual Studio 2005.</span></span> <span data-ttu-id="7754b-148">你可以在母版页和内容页中的相应内容控件中查看 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-148">You can see the ContentPlaceHolder control in the master page and the corresponding Content control in the content page.</span></span> <span data-ttu-id="7754b-149">请注意，ContentPlaceHolder 外部的母版页内容可见，但在内容页中显示为灰色。</span><span class="sxs-lookup"><span data-stu-id="7754b-149">Notice that the master pages content that is outside of the ContentPlaceHolder is visible but grayed out in the content page.</span></span> <span data-ttu-id="7754b-150">内容页仅可以 supplanted ContentPlaceHolder 内的内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-150">Only the content inside of the ContentPlaceHolder can be supplanted by the content page.</span></span> <span data-ttu-id="7754b-151">来自母版页的所有其他内容都是不可变的。</span><span class="sxs-lookup"><span data-stu-id="7754b-151">All other content that comes from the master page is immutable.</span></span>

![母版页及其关联的内容页](master-pages/_static/image1.jpg)

<span data-ttu-id="7754b-153">**图 1**：母版页及其关联的内容页</span><span class="sxs-lookup"><span data-stu-id="7754b-153">**Figure 1**: A master page and its associated content page</span></span>

## <a name="creating-a-master-page"></a><span data-ttu-id="7754b-154">创建母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-154">Creating a Master Page</span></span>

<span data-ttu-id="7754b-155">若要创建新的母版页：</span><span class="sxs-lookup"><span data-stu-id="7754b-155">To create a new master page:</span></span>

1. <span data-ttu-id="7754b-156">打开 Visual Studio 2005 并创建新网站。</span><span class="sxs-lookup"><span data-stu-id="7754b-156">Open Visual Studio 2005 and create a new Web site.</span></span>
2. <span data-ttu-id="7754b-157">单击 "文件"、"新建"、"文件"。</span><span class="sxs-lookup"><span data-stu-id="7754b-157">Click File, New, File.</span></span>
3. <span data-ttu-id="7754b-158">从 "添加新项" 对话框中选择 "主文件"，如**图 2**所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-158">Choose Master File from the Add New Item dialog as shown in **figure 2**.</span></span>
4. <span data-ttu-id="7754b-159">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="7754b-159">Click Add.</span></span>

![创建新的母版页](master-pages/_static/image2.jpg)

<span data-ttu-id="7754b-161">**图 2**：创建新的母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-161">**Figure 2**: Creating a New Master Page</span></span>

<span data-ttu-id="7754b-162">请注意，母版页的文件扩展名为*master*。</span><span class="sxs-lookup"><span data-stu-id="7754b-162">Notice that the file extension for a master page is *.master*.</span></span> <span data-ttu-id="7754b-163">这是母版页不同于普通页面的方法之一。</span><span class="sxs-lookup"><span data-stu-id="7754b-163">This is one of the ways that a master page differs from an ordinary page.</span></span> <span data-ttu-id="7754b-164">另一个主要区别是，在代替 @Page 指令时，母版页包含 @Master 指令。</span><span class="sxs-lookup"><span data-stu-id="7754b-164">The other primary difference is that in lieu of a @Page directive, the master page contains a @Master directive.</span></span> <span data-ttu-id="7754b-165">切换到刚刚创建的母版页的 "源" 视图，然后查看代码。</span><span class="sxs-lookup"><span data-stu-id="7754b-165">Switch to Source View for the master page you've just created and review the code.</span></span>

<span data-ttu-id="7754b-166">默认情况下，新的母版页将具有一个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-166">A new master page will have one ContentPlaceHolder control by default.</span></span> <span data-ttu-id="7754b-167">在大多数情况下，首先创建公共页面元素，然后插入需要自定义内容的 ContentPlaceHolder 控件，这样做会更有意义。</span><span class="sxs-lookup"><span data-stu-id="7754b-167">In most cases, it makes more sense to create the common page elements first and then insert ContentPlaceHolder controls where custom content is desired.</span></span> <span data-ttu-id="7754b-168">在这些情况下，开发人员需要删除默认的 ContentPlaceHolder 控件并在开发页面时插入新控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-168">In those cases, developers will want to delete the default ContentPlaceHolder control and insert new ones as the page is developed.</span></span> <span data-ttu-id="7754b-169">尽管 ContentPlaceHolder 控件确实显示大小调整控点，但无法调整其大小。</span><span class="sxs-lookup"><span data-stu-id="7754b-169">ContentPlaceHolder controls are not resizable despite the fact that they do display sizing handles.</span></span> <span data-ttu-id="7754b-170">ContentPlaceHolder 控件根据其所包含的内容自动调整大小，但有一个例外;如果将 ContentPlaceHolder 控件放置在块元素（例如表单元）内，则它将根据元素的大小进行调整。</span><span class="sxs-lookup"><span data-stu-id="7754b-170">The ContentPlaceHolder control sizes automatically based upon the content that it contains with one exception; if you place a ContentPlaceHolder control inside of a block element such as a table cell, it will size according to the size of the element.</span></span>

## <a name="lab-1-working-with-master-pages"></a><span data-ttu-id="7754b-171">实验室1使用母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-171">Lab 1 Working with Master Pages</span></span>

<span data-ttu-id="7754b-172">在此实验室中，您将创建一个新的母版页，并定义三个 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-172">In this lab, you will create a new master page and define three ContentPlaceHolder controls.</span></span> <span data-ttu-id="7754b-173">然后，将创建一个新的内容页并替换至少一个 ContentPlaceHolder 控件中的内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-173">You will then create a new Content page and replace the content from at least one of the ContentPlaceHolder controls.</span></span>

1. <span data-ttu-id="7754b-174">创建一个母版页并插入 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-174">Create a master page and insert ContentPlaceHolder controls.</span></span> 

    1. <span data-ttu-id="7754b-175">如上所述，创建新的母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-175">Create a new master page as described above.</span></span>
    2. <span data-ttu-id="7754b-176">删除默认的 ContentPlaceHolder 控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-176">Delete the default ContentPlaceHolder control.</span></span>
    3. <span data-ttu-id="7754b-177">通过单击控件的灰色上边框来选择 ContentPlaceHolder 控件，然后按键盘上的 DEL 键将其删除。</span><span class="sxs-lookup"><span data-stu-id="7754b-177">Select the ContentPlaceHolder control by clicking the shaded top border of the control and then delete it by hitting the DEL key on your keyboard.</span></span>
    4. <span data-ttu-id="7754b-178">使用*标头和端*模板插入新表，如图3所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-178">Insert a new table using the *Header and side* template as shown in figure 3.</span></span> <span data-ttu-id="7754b-179">将宽度和高度分别更改为90%，使整个表在设计器中可见。</span><span class="sxs-lookup"><span data-stu-id="7754b-179">Change the width and height to 90% each so that the entire table is visible in the designer.</span></span>

![](master-pages/_static/image3.jpg)

<span data-ttu-id="7754b-180">**图3**</span><span class="sxs-lookup"><span data-stu-id="7754b-180">**Figure 3**</span></span>

1. <span data-ttu-id="7754b-181">将光标置于表的每个单元格中，并将*valign*属性设置为*top*。</span><span class="sxs-lookup"><span data-stu-id="7754b-181">Place the cursor into each cell of the table and set the *valign* property to *top*.</span></span>
2. <span data-ttu-id="7754b-182">从 "工具箱" 中，将 "ContentPlaceHolder" 控件插入到表的顶部单元格中（标题单元格）。</span><span class="sxs-lookup"><span data-stu-id="7754b-182">From the Toolbox, insert a ContentPlaceHolder control in the top cell of the table (the header cell.)</span></span>
3. <span data-ttu-id="7754b-183">插入此 ContentPlaceHolder 控件时，你会注意到，行高会占用整个页面，如图4所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-183">When you insert this ContentPlaceHolder control, you will notice that the row height will take up almost the entire page as shown in figure 4.</span></span> <span data-ttu-id="7754b-184">此时，不要担心这一点。</span><span class="sxs-lookup"><span data-stu-id="7754b-184">Don't be concerned about that at this point.</span></span>

![空格与 ContentPlaceHolder 位于同一单元中](master-pages/_static/image1.gif)

<span data-ttu-id="7754b-186">**图 4**：空白空间与 ContentPlaceHolder 位于同一单元中</span><span class="sxs-lookup"><span data-stu-id="7754b-186">**Figure 4**: The empty space is in the same cell as the ContentPlaceHolder</span></span>

1. <span data-ttu-id="7754b-187">将 ContentPlaceHolder 控件放在其他两个单元格中。</span><span class="sxs-lookup"><span data-stu-id="7754b-187">Place a ContentPlaceHolder control in the other two cells.</span></span> <span data-ttu-id="7754b-188">插入其他 ContentPlaceHolder 控件后，表单元格的大小应与预期的大小相同。</span><span class="sxs-lookup"><span data-stu-id="7754b-188">Once the other ContentPlaceHolder controls have been inserted, the size of the table cells should be as you would expect.</span></span> <span data-ttu-id="7754b-189">该页现在应类似于**图 5**所示的页面。</span><span class="sxs-lookup"><span data-stu-id="7754b-189">The page should now look like the page shown in **figure 5**.</span></span>

![具有所有 ContentPlaceHolder 控件的主节点。](master-pages/_static/image2.gif)

<span data-ttu-id="7754b-192">**图 5**：包含所有 ContentPlaceHolder 控件的主节点。</span><span class="sxs-lookup"><span data-stu-id="7754b-192">**Figure 5**: The Master with all ContentPlaceHolder controls.</span></span> <span data-ttu-id="7754b-193">请注意，标题单元格的单元格高度现在就是</span><span class="sxs-lookup"><span data-stu-id="7754b-193">Notice that the cell height for the header cell is now what it should be</span></span>

1. <span data-ttu-id="7754b-194">在三个 ContentPlaceHolder 控件中的每个控件中输入一些所选文本。</span><span class="sxs-lookup"><span data-stu-id="7754b-194">Enter some text of your choice into each of the three ContentPlaceHolder controls.</span></span>
2. <span data-ttu-id="7754b-195">将母版页保存为 exercise1。</span><span class="sxs-lookup"><span data-stu-id="7754b-195">Save the master page as exercise1.master.</span></span>
3. <span data-ttu-id="7754b-196">创建新的 Web 窗体，并将其与 exercise1 母版页关联。</span><span class="sxs-lookup"><span data-stu-id="7754b-196">Create a new Web Form and associate it with the exercise1.master master page.</span></span>
4. <span data-ttu-id="7754b-197">在 Visual Studio 2005 中选择 "文件"、"新建" 和 "文件"。</span><span class="sxs-lookup"><span data-stu-id="7754b-197">Select File, New, File in Visual Studio 2005.</span></span>
5. <span data-ttu-id="7754b-198">在 "添加新项" 对话框中选择 " **Web 窗体**"。</span><span class="sxs-lookup"><span data-stu-id="7754b-198">Select **Web Form** in the Add New Item dialog.</span></span>
6. <span data-ttu-id="7754b-199">请确保选中 "选择母版页" 复选框，如图6所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-199">Make sure that the Select master page checkbox is checked as shown in figure 6.</span></span>

![添加新的内容页](master-pages/_static/image3.gif)

<span data-ttu-id="7754b-201">**图 6**：添加新的内容页</span><span class="sxs-lookup"><span data-stu-id="7754b-201">**Figure 6**: Adding a new Content Page</span></span>

1. <span data-ttu-id="7754b-202">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="7754b-202">Click Add.</span></span>
2. <span data-ttu-id="7754b-203">在 "选择母版页" 对话框中选择 "exercise1"，如图7所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-203">Select exercise1.master in the Select a master page dialog as shown in figure 7.</span></span>
3. <span data-ttu-id="7754b-204">单击 "确定" 以添加新的内容页面。</span><span class="sxs-lookup"><span data-stu-id="7754b-204">Click OK to add the new content page.</span></span>

<span data-ttu-id="7754b-205">新的内容页将显示在 Visual Studio 中，其中，母版页上的每个 ContentPlaceHolder 控件都有一个内容控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-205">The new content page appears in Visual Studio with one Content control for each ContentPlaceHolder control on the master page.</span></span> <span data-ttu-id="7754b-206">默认情况下，内容控件为空，以便您可以添加自己的内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-206">By default, the Content controls are empty so that you can add your own content.</span></span> <span data-ttu-id="7754b-207">如果希望它们使用母版页上的 ContentPlaceHolder 控件中的内容，只需单击智能标记符号（控件右上角的小黑色箭头），然后从智能标记中选择 "*默认为主控内容*"，如**图 8**所示。</span><span class="sxs-lookup"><span data-stu-id="7754b-207">If you'd like for them to use the content from the ContentPlaceHolder control on the master page, simply click on the smart tag symbol (the small black arrow in the upper-right corner of the control) and choose *Default to Masters Content* from the smart tag as shown in **figure 8**.</span></span> <span data-ttu-id="7754b-208">当你执行此操作时，菜单项会更改以*创建自定义内容*。</span><span class="sxs-lookup"><span data-stu-id="7754b-208">When you do so, the menu item changes to *Create Custom Content*.</span></span> <span data-ttu-id="7754b-209">在该点单击该点将从母版页中删除内容，以便为该特定内容控件定义自定义内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-209">Clicking it at that point removes the content from the master page allowing you to define custom content for that particular Content control.</span></span>

![将内容控件设置为默认母版页内容](master-pages/_static/image4.gif)

<span data-ttu-id="7754b-211">**图 7**：将内容控件设置为默认为母版页内容</span><span class="sxs-lookup"><span data-stu-id="7754b-211">**Figure 7**: Setting a Content Control to Default to the Master Pages Content</span></span>

## <a name="connecting-master-page-and-content-pages"></a><span data-ttu-id="7754b-212">连接母版页和内容页</span><span class="sxs-lookup"><span data-stu-id="7754b-212">Connecting Master Page and Content Pages</span></span>

<span data-ttu-id="7754b-213">可以通过以下四种不同方式之一配置母版页和内容页之间的关联：</span><span class="sxs-lookup"><span data-stu-id="7754b-213">The association between a master page and a content page can be configured in one of four different ways:</span></span>

- <span data-ttu-id="7754b-214">@Page 指令的<strong>MasterPageFile</strong>特性</span><span class="sxs-lookup"><span data-stu-id="7754b-214">The <strong>MasterPageFile</strong> attribute of the @Page directive</span></span>
- <span data-ttu-id="7754b-215">在代码中设置**MasterPageFile**属性。</span><span class="sxs-lookup"><span data-stu-id="7754b-215">Setting the **Page.MasterPageFile** property in code.</span></span>
- <span data-ttu-id="7754b-216">**&lt;页面**在应用程序配置文件（应用程序的根文件夹中的 web.config）&gt;元素</span><span class="sxs-lookup"><span data-stu-id="7754b-216">The **&lt;pages&gt;** element in the applications configuration file (web.config in the root folder of the application)</span></span>
- <span data-ttu-id="7754b-217">**&lt;页面&gt;** 子文件夹配置文件中的元素（子文件夹中的 web.config）</span><span class="sxs-lookup"><span data-stu-id="7754b-217">The **&lt;pages&gt;** element in a subfolders configuration file (web.config in a subfolder)</span></span>

## <a name="masterpagefile-attribute"></a><span data-ttu-id="7754b-218">MasterPageFile 特性</span><span class="sxs-lookup"><span data-stu-id="7754b-218">MasterPageFile Attribute</span></span>

<span data-ttu-id="7754b-219">使用 MasterPageFile 属性可以轻松地将母版页应用到特定的 ASP.NET 页面。</span><span class="sxs-lookup"><span data-stu-id="7754b-219">The MasterPageFile attribute makes it easy to apply a master page to a particular ASP.NET page.</span></span> <span data-ttu-id="7754b-220">当您在练习1中选中 "**选择母版页**" 复选框时，也可以使用此方法来应用母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-220">It is also the method used to apply the master page when you check the **Select Master Page** checkbox as you did in Exercise 1.</span></span>

## <a name="setting-pagemasterpagefile-in-code"></a><span data-ttu-id="7754b-221">在代码中设置 MasterPageFile</span><span class="sxs-lookup"><span data-stu-id="7754b-221">Setting Page.MasterPageFile in Code</span></span>

<span data-ttu-id="7754b-222">通过在代码中设置 MasterPageFile 属性，您可以在运行时将特定母版页应用于内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-222">By setting the MasterPageFile property in code, you can apply a particular master page to your content at runtime.</span></span> <span data-ttu-id="7754b-223">当你可能需要根据用户角色或某些其他条件应用特定母版页时，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="7754b-223">This is useful in cases where you may need to apply a specific master page based upon a users role or some other criteria.</span></span> <span data-ttu-id="7754b-224">必须在 PreInit 方法中设置 MasterPageFile 属性。</span><span class="sxs-lookup"><span data-stu-id="7754b-224">The MasterPageFile property must be set in the PreInit method.</span></span> <span data-ttu-id="7754b-225">如果在 PreInit 方法之后设置，则会引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="7754b-225">If it is set after the PreInit method, an InvalidOperationException will be thrown.</span></span> <span data-ttu-id="7754b-226">在其上设置此属性的页面上，还必须将内容控件作为页面的顶级控件。</span><span class="sxs-lookup"><span data-stu-id="7754b-226">The page on which this property is being set must also have a Content control as the top-level control for the page.</span></span> <span data-ttu-id="7754b-227">否则，在设置 MasterPageFile 属性时，将引发 HttpException。</span><span class="sxs-lookup"><span data-stu-id="7754b-227">Otherwise an HttpException will be thrown when the MasterPageFile property is set.</span></span>

## <a name="using-the-ltpagesgt-element"></a><span data-ttu-id="7754b-228">使用 &lt;pages&gt; 元素</span><span class="sxs-lookup"><span data-stu-id="7754b-228">Using the &lt;pages&gt; Element</span></span>

<span data-ttu-id="7754b-229">通过在 web.config 文件的 &lt;pages&gt; 元素中设置 masterPageFile 属性，可以为页面配置母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-229">You can configure a master page for your pages by setting the masterPageFile attribute in the &lt;pages&gt; element of the web.config file.</span></span> <span data-ttu-id="7754b-230">使用此方法时，请记住，在应用程序结构中较低的 web.config 文件可以重写此设置。</span><span class="sxs-lookup"><span data-stu-id="7754b-230">When using this method, keep in mind that web.config files lower in the application structure can override this setting.</span></span> <span data-ttu-id="7754b-231">@Page 指令中设置的任何 MasterPageFile 属性还将重写此设置。</span><span class="sxs-lookup"><span data-stu-id="7754b-231">Any MasterPageFile attribute set in a @Page directive will also override this setting.</span></span> <span data-ttu-id="7754b-232">通过使用 &lt;pages&gt; 元素，可以轻松创建在特定文件夹或文件中需要重写的*主*母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-232">Using the &lt;pages&gt; element makes it simple to create a *master* master page that can be overridden if necessary in particular folders or files.</span></span>

## <a name="properties-in-master-pages"></a><span data-ttu-id="7754b-233">母版页中的属性</span><span class="sxs-lookup"><span data-stu-id="7754b-233">Properties in Master Pages</span></span>

<span data-ttu-id="7754b-234">母版页只需在母版页内使这些属性公开即可公开属性。</span><span class="sxs-lookup"><span data-stu-id="7754b-234">A master page can expose properties by simply making those properties public within the master page.</span></span> <span data-ttu-id="7754b-235">例如，下面的代码定义了一个名为 SomeProperty 的属性：</span><span class="sxs-lookup"><span data-stu-id="7754b-235">For example, the following code defines a property called SomeProperty:</span></span>

[!code-csharp[Main](master-pages/samples/sample2.cs)]

<span data-ttu-id="7754b-236">若要从 "内容" 页访问 SomeProperty 属性，需要使用 Master 属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7754b-236">To access the SomeProperty property from the Content page, you will need to use the Master property like so:</span></span>

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a><span data-ttu-id="7754b-237">嵌套母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-237">Nesting Master Pages</span></span>

<span data-ttu-id="7754b-238">母版页是确保大型 Web 应用程序的常见外观的理想解决方案。</span><span class="sxs-lookup"><span data-stu-id="7754b-238">Master pages are the perfect solution for ensuring a common look and feel across a large Web application.</span></span> <span data-ttu-id="7754b-239">但是，在某些情况下，大型站点的某些部分共享公共接口并不常见，而其他部分则共享不同的接口。</span><span class="sxs-lookup"><span data-stu-id="7754b-239">However, it's not uncommon to have certain parts of a large site share a common interface while other parts share a different interface.</span></span> <span data-ttu-id="7754b-240">为了满足这种需要，多个母版页是最佳解决方案。</span><span class="sxs-lookup"><span data-stu-id="7754b-240">To address that need, multiple master pages are the perfect solution.</span></span> <span data-ttu-id="7754b-241">但是，这仍不能解决这样一种情况：大型应用程序可能有某些组件（例如菜单）在所有页面和其他仅在站点的特定部分中共享的组件之间共享。</span><span class="sxs-lookup"><span data-stu-id="7754b-241">However, that still doesn't address the fact that a large application may have certain components (such as a menu, for example) that are shared among all pages and other components that are shared only among certain sections of the site.</span></span> <span data-ttu-id="7754b-242">对于这种情况，嵌套的母版页非常适合需要。</span><span class="sxs-lookup"><span data-stu-id="7754b-242">For that type of situation, nested master pages fill the need nicely.</span></span> <span data-ttu-id="7754b-243">正如您所看到的，普通的母版页包含一个母版页和一个内容页面。</span><span class="sxs-lookup"><span data-stu-id="7754b-243">As you've seen, a normal master page consists of a master page and a content page.</span></span> <span data-ttu-id="7754b-244">在嵌套的母版页情况下，有两个母版页;父主机和子主节点。</span><span class="sxs-lookup"><span data-stu-id="7754b-244">In a nested master page situation, there are two master pages; a parent master and a child master.</span></span> <span data-ttu-id="7754b-245">子母版页也是内容页，其母版页是父级母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-245">The child master page is also a content page and its master is the parent master page.</span></span>

<span data-ttu-id="7754b-246">下面是典型母版页的代码：</span><span class="sxs-lookup"><span data-stu-id="7754b-246">Here is the code for a typical master page:</span></span>

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

<span data-ttu-id="7754b-247">在嵌套的主方案中，这将是父主节点。</span><span class="sxs-lookup"><span data-stu-id="7754b-247">In a nested master scenario, this would be the parent master.</span></span> <span data-ttu-id="7754b-248">另一个母版页将使用此页作为其母版页，代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="7754b-248">Another master page would use this page as its master page, and that code would look like this:</span></span>

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

<span data-ttu-id="7754b-249">请注意，在这种情况下，子主节点也是父主节点的内容页。</span><span class="sxs-lookup"><span data-stu-id="7754b-249">Note that in this scenario, the child master is also a content page for the parent master.</span></span> <span data-ttu-id="7754b-250">所有子母版页的内容都显示在内容控件中，该控件从父级的 ContentPlaceHolder 控件获取其内容。</span><span class="sxs-lookup"><span data-stu-id="7754b-250">All of the child master's content appears inside of a Content control that gets its content from the parent's ContentPlaceHolder control.</span></span>

> [!NOTE]
> <span data-ttu-id="7754b-251">设计器支持不可用于嵌套母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-251">Designer support is not available for nested master pages.</span></span> <span data-ttu-id="7754b-252">使用嵌套母版进行开发时，需要使用源视图。</span><span class="sxs-lookup"><span data-stu-id="7754b-252">When you are developing using nested masters, you will need to use source view.</span></span>

<span data-ttu-id="7754b-253">此视频演示如何使用嵌套母版页。</span><span class="sxs-lookup"><span data-stu-id="7754b-253">This video shows a walkthrough of using nested master pages.</span></span>

![](master-pages/_static/image1.png)

[<span data-ttu-id="7754b-254">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="7754b-254">Open Full-Screen Video</span></span>](master-pages/_static/nested1.wmv)

![选择母版页](master-pages/_static/image4.jpg)

<span data-ttu-id="7754b-256">**图 8**：选择母版页</span><span class="sxs-lookup"><span data-stu-id="7754b-256">**Figure 8**: Selecting a Master Page</span></span>
