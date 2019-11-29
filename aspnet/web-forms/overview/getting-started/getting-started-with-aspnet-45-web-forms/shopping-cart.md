---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 购物车 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 46264a0ab2244cff24761ce94b41722e61e3f426
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614929"
---
# <a name="shopping-cart"></a>购物车

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

本教程介绍将购物车添加到 Wingtip 玩具示例 ASP.NET Web 窗体应用程序所需的业务逻辑。 本教程基于前面的 "显示数据项和详细信息" 教程，是 Wingtip 玩具商店教程系列的一部分。 完成本教程后，你的示例应用程序的用户将能够在其购物车中添加、删除和修改产品。

## <a name="what-youll-learn"></a>你将学习的内容：

1. 如何为 web 应用程序创建购物车。
2. 如何使用户能够将物品添加到购物车。
3. 如何添加[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控件以显示购物车详情。
4. 如何计算并显示订单总计。
5. 如何删除和更新购物车中的项目。
6. 如何包含购物车计数器。

## <a name="code-features-in-this-tutorial"></a>本教程中的代码功能：

1. 实体框架 Code First
2. 数据注释
3. 强类型化数据控件
4. 模型绑定

## <a name="creating-a-shopping-cart"></a>创建购物车

在本系列教程的前面部分中，已添加了用于从数据库查看产品数据的页面和代码。 在本教程中，你将创建一个购物车来管理用户感兴趣的产品。 即使用户没有注册或登录，用户也能够浏览并向购物车添加商品。 若要管理购物车访问权限，请在用户首次访问购物车时，为用户分配唯一的 `ID`，使用全局唯一标识符（GUID）。 你将使用 ASP.NET 会话状态存储此 `ID`。

> [!NOTE] 
> 
> ASP.NET 会话状态是一个方便的位置，用于存储用户特定的信息，这些信息会在用户离开站点后过期。 尽管会话状态滥用可能会对较大的站点产生性能影响，但会话状态的使用非常适合用于演示目的。 Wingtip 玩具示例项目演示了如何在没有外部提供程序的情况下使用会话状态，在该提供程序中，会话状态存储在托管站点的 web 服务器上的进程中。 对于提供应用程序的多个实例的大型站点或在不同服务器上运行多个应用程序实例的站点，请考虑使用**Windows Azure Cache Service**。 此缓存服务提供网站外部的分布式缓存服务，并解决使用进程内会话状态的问题。 有关详细信息，请参阅[如何将 ASP.NET 会话状态用于 Microsoft Azure 网站](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。

### <a name="add-cartitem-as-a-model-class"></a>将 CartItem 添加为模型类

在本系列教程的前面部分，你通过在 "*模型*" 文件夹中创建 `Category` 和 `Product` 类来定义类别和产品数据的架构。 现在，添加一个新类来定义购物车的架构。 稍后在本教程中，您将添加一个类来处理对 `CartItem` 表的数据访问。 此类将提供业务逻辑，以便添加、删除和更新购物车中的项目。

1. 右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。 

    ![购物车-新项目](shopping-cart/_static/image1.png)
2. 随即出现“添加新项”对话框。 选择 "**代码**"，然后选择 "**类**"。 

    ![购物车-"添加新项" 对话框](shopping-cart/_static/image2.png)
3. 将此新类命名为*CartItem.cs*。
4. 单击 **添加**。  
   新的类文件将显示在编辑器中。
5. 将默认代码替换为以下代码：   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` 类包含将定义用户添加到购物车的每个产品的架构。 此类类似于在本教程系列中前面创建的其他架构类。 按照约定，实体框架 Code First 需要 `CartItem` 表的主键将 `CartItemId` 或 `ID`。 但是，代码使用数据批注 `[Key]` 特性来重写默认行为。 ItemId 属性的 `Key` 特性指定 `ItemID` 属性为主键。

`CartId` 属性指定与要购买的项关联的用户的 `ID`。 当用户访问购物车时，你将添加代码以创建此用户 `ID`。 此 `ID` 还将存储为 ASP.NET 会话变量。

### <a name="update-the-product-context"></a>更新产品上下文

除了添加 `CartItem` 类之外，您还需要更新管理实体类的数据库上下文类，并提供对数据库的数据访问。 为此，您需要将新创建的 `CartItem` 模型类添加到 `ProductContext` 类。

1. 在**解决方案资源管理器**中，查找并打开 "*模型*" 文件夹中的*ProductContext.cs*文件。
2. 将突出显示的代码添加到*ProductContext.cs*文件，如下所示：  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

如本系列教程前面所述， *ProductContext.cs*文件中的代码将添加 `System.Data.Entity` 命名空间，以便您可以访问实体框架的所有核心功能。 此功能包括使用强类型对象查询、插入、更新和删除数据的功能。 `ProductContext` 类添加对新添加的 `CartItem` 模型类的访问。

### <a name="managing-the-shopping-cart-business-logic"></a>管理购物车业务逻辑

接下来，你将在新的*逻辑*文件夹中创建 `ShoppingCart` 类。 `ShoppingCart` 类处理对 `CartItem` 表的数据访问。 类还将包括用于添加、删除和更新购物车中的项的业务逻辑。

你将添加的购物车逻辑将包含管理以下操作的功能：

1. 将商品添加到购物车
2. 从购物车中删除商品
3. 获取购物车 ID
4. 检索购物车中的物品
5. 总计购物车商品的总量
6. 更新购物车数据

购物车页面（*ShoppingCart*）和购物车类将一起用于访问购物车数据。 "购物车" 页将显示用户添加到购物车中的所有项目。 除了购物车页和类之外，你还将创建一个页面（*AddToCart*），用于将产品添加到购物车。 你还会将代码添加到*ProductList*页和*ProductDetails*页，该页面将提供指向*AddToCart*页的链接，以便用户可以将产品添加到购物车。

下图显示了用户向购物车添加产品时所发生的基本过程。

![购物车-添加到购物车](shopping-cart/_static/image3.png)

当用户单击*ProductList*页或*ProductDetails*页上的 "**添加到购物车**" 链接时，应用程序将导航到*AddToCart*页，然后自动定位到*ShoppingCart*页。 *AddToCart*页面通过调用 ShoppingCart 类中的方法将选择的产品添加到购物车。 *ShoppingCart*页将显示已添加到购物车中的产品。

#### <a name="creating-the-shopping-cart-class"></a>创建购物车类

`ShoppingCart` 类将添加到应用程序中的单独文件夹中，以便模型（模型文件夹）、页面（根文件夹）和逻辑（逻辑文件夹）之间存在明显的区别。

1. 在**解决方案资源管理器**中，右键单击**WingtipToys**项目，然后选择 "**添加**-&gt;**新文件夹**"。 将新文件夹命名为*逻辑*。
2. 右键单击*逻辑*文件夹，然后选择 "**添加** -&gt;**新项**"。
3. 添加一个名为*ShoppingCartActions.cs*的新类文件。
4. 将默认代码替换为以下代码：   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

利用 `AddToCart` 方法，可以根据产品 `ID`将各个产品包括在购物车中。 该产品将添加到购物车中，或者，如果该购物车中已包含该产品的物品，则该数量将递增。

`GetCartId` 方法返回用户的购物车 `ID`。 购物车 `ID` 用于跟踪用户在其购物车中的物品。 如果用户没有 `ID`的现有购物车，将为其创建新的 cart `ID`。 如果用户以注册用户身份登录，则会将购物车 `ID` 设置为他们的用户名。 但是，如果用户未登录，则购物车 `ID` 设置为唯一值（GUID）。 GUID 可确保为每个用户仅基于会话创建一个购物车。

`GetCartItems` 方法返回用户的购物车项列表。 在本教程的后面部分中，你将看到，使用 `GetCartItems` 方法在购物车中显示购物车项的模型绑定。

### <a name="creating-the-add-to-cart-functionality"></a>创建添加到购物车功能

如前文所述，你将创建一个名为*AddToCart*的处理页，该页面将用于向用户的购物车中添加新产品。 此页将调用刚才创建的 `ShoppingCart` 类中的 `AddToCart` 方法。 *AddToCart*页将预计向其传递产品 `ID`。 此产品 `ID` 将在 `ShoppingCart` 类中调用 `AddToCart` 方法时使用。

> [!NOTE] 
> 
> 你将修改此页面的代码隐藏（*AddToCart.aspx.cs*），而不是页面 UI （*AddToCart*）。

#### <a name="to-create-the-add-to-cart-functionality"></a>若要创建 "添加到购物车" 功能：

1. 在**解决方案资源管理器**中，右键单击**WingtipToys**项目，然后单击 "**添加** -" &gt;**新项**"。  
   随即出现“添加新项”对话框。
2. 将标准新页面（Web 窗体）添加到名为*AddToCart*的应用程序。 

    ![购物车-添加 Web 窗体](shopping-cart/_static/image4.png)
3. 在**解决方案资源管理器**中，右键单击 " *AddToCart* " 页，然后单击 "**查看代码**"。 *AddToCart.aspx.cs*代码隐藏文件在编辑器中打开。
4. 将*AddToCart.aspx.cs*代码隐藏中的现有代码替换为以下代码：   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

加载*AddToCart*页面后，将从查询字符串中检索 product `ID`。 接下来，将创建一个购物车类的实例，并使用该实例来调用你之前在本教程中添加的 `AddToCart` 方法。 *ShoppingCartActions.cs*文件中包含的 `AddToCart` 方法包含将所选产品添加到购物车或增加所选产品的产品数量的逻辑。 如果产品尚未添加到购物车中，则会将该产品添加到数据库的 `CartItem` 表。 如果产品已添加到购物车，并且用户添加了同一产品的其他项，则产品数量在 `CartItem` 表中递增。 最后，页面重定向回*ShoppingCart*页面，你将在下一步中添加该页面，用户可在其中查看购物车中的项目的更新列表。

如前所述，用户 `ID` 用于标识与特定用户关联的产品。 每次用户将产品添加到购物车时，此 `ID` 都会添加到 `CartItem` 表中的一行。

### <a name="creating-the-shopping-cart-ui"></a>创建购物车 UI

" *ShoppingCart* " 页将显示用户已添加到其购物车中的产品。 它还将提供在购物车中添加、删除和更新项的功能。

1. 在**解决方案资源管理器**中，右键单击**WingtipToys**，再单击 "**添加** -" &gt;**新项**"。  
   随即出现“添加新项”对话框。
2. 通过选择 "**使用母版页的 Web 窗体**"，添加包含母版页的新页面（Web 窗体）。 将新页面命名为*ShoppingCart*。
3. 选择 "**站点**" 以将母版页附加到新创建的 *.aspx*页面。
4. 在*ShoppingCart*页中，将现有标记替换为以下标记：   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart*页包含一个名为 `CartList`的**GridView**控件。 此控件使用模型绑定将购物车数据从数据库绑定到**GridView**控件。 设置**GridView**控件的 `ItemType` 属性时，数据绑定表达式 `Item` 在控件的标记中可用，并且控件将成为强类型。 如本系列教程前面所述，可以使用 IntelliSense 选择 `Item` 对象的详细信息。 若要将数据控件配置为使用模型绑定来选择数据，请设置控件的 `SelectMethod` 属性。 在上面的标记中，将 `SelectMethod` 设置为使用 GetShoppingCartItems 方法，该方法返回 `CartItem` 对象的列表。 **GridView**数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。 仍需添加 `GetShoppingCartItems` 方法。

#### <a name="retrieving-the-shopping-cart-items"></a>检索购物车商品

接下来，将代码添加到*ShoppingCart.aspx.cs*代码隐藏中以检索和填充购物车 UI。

1. 在**解决方案资源管理器**中，右键单击 " *ShoppingCart* " 页，然后单击 "**查看代码**"。 *ShoppingCart.aspx.cs*代码隐藏文件在编辑器中打开。
2. 将现有代码替换为以下代码：  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

如上所述，`GridView` 数据控件在页面生命周期中的适当时间调用 `GetShoppingCartItems` 方法，并自动绑定返回的数据。 `GetShoppingCartItems` 方法创建 `ShoppingCartActions` 对象的实例。 然后，该代码使用该实例通过调用 `GetCartItems` 方法返回购物车中的项。

### <a name="adding-products-to-the-shopping-cart"></a>将产品添加到购物车

当显示 " *ProductList* " 或 " *ProductDetails* " 页时，用户将能够使用链接将产品添加到购物车。 当他们单击此链接时，应用程序将导航到名为*AddToCart*的处理页。 *AddToCart*页将调用你之前在本教程中添加的 `ShoppingCart` 类中的 `AddToCart` 方法。

现在，将添加到 " *ProductList* " 页和 " *ProductDetails* " 页的 "**添加到购物车**" 链接。 此链接将包含从数据库中检索到的产品 `ID`。

1. 在**解决方案资源管理器**中，找到并打开名为*ProductList*的页。
2. 将黄色突出显示的标记添加到*ProductList*页面，使整个页面显示如下：  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>测试购物车

运行应用程序，了解如何将产品添加到购物车。

1. 按 **F5** 运行该应用程序。  
 在项目重新创建数据库后，浏览器将打开并显示*default.aspx*页。
2. 从类别导航菜单中选择 "**汽车**"。  
 随即显示 " *ProductList* " 页，其中仅显示 "汽车" 类别中包含的产品。 

    ![购物车-汽车](shopping-cart/_static/image5.png)
3. 单击列出的第一个产品旁边的 "**添加到购物车**" 链接（可转换的汽车）。   
 随即显示 " *ShoppingCart* " 页，其中显示购物车中的选择。 

    ![购物车-购物车](shopping-cart/_static/image6.png)
4. 通过从类别导航菜单中选择 "**平面**" 来查看其他产品。
5. 单击列出的第一个产品旁边的 "**添加到购物车**" 链接。  
 随即显示*ShoppingCart*页，其中包含附加项。
6. 关闭浏览器。

### <a name="calculating-and-displaying-the-order-total"></a>计算并显示订单总计

除了将产品添加到购物车外，还会将 `GetTotal` 方法添加到 `ShoppingCart` 类，并在购物车页中显示总订单量。

1. 在**解决方案资源管理器**中，打开*逻辑*文件夹中的*ShoppingCartActions.cs*文件。
2. 向 `ShoppingCart` 类添加以黄色突出显示的以下 `GetTotal` 方法，使类显示如下：   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

首先，`GetTotal` 方法获取用户的购物车的 ID。 然后，该方法通过将产品价格乘以购物车中列出的每个产品的产品数量，来获取购物车总计。

> [!NOTE] 
> 
> 上面的代码使用可以为 null 的类型 "`int?`"。 可以为 null 的类型可以表示基础类型的所有值，也可以表示为 null 值。 有关详细信息，请参阅[使用可以为 null 的类型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。

### <a name="modify-the-shopping-cart-display"></a>修改购物车显示

接下来，您将修改*ShoppingCart*页的代码，以调用 `GetTotal` 方法，并在加载页面时在*ShoppingCart*页上显示该总数。

1. 在**解决方案资源管理器**中，右键单击 " *ShoppingCart* " 页，然后选择 "**查看代码**"。
2. 在*ShoppingCart.aspx.cs*文件中，通过添加以下突出显示的代码来更新 `Page_Load` 处理程序：   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

加载*ShoppingCart*页面时，它会加载购物车对象，然后通过调用 `ShoppingCart` 类的 `GetTotal` 方法来检索购物车总计。 如果购物车为空，则显示一条指向该效果的消息。

### <a name="testing-the-shopping-cart-total"></a>测试购物车总计

立即运行该应用程序，了解如何将产品添加到购物车，但你可以看到购物车总计。

1. 按 **F5** 运行该应用程序。  
 浏览器将打开并显示*default.aspx*页。
2. 从类别导航菜单中选择 "**汽车**"。
3. 单击第一个产品旁边的 "**添加到购物车**" 链接。   
 将显示*ShoppingCart*页，其中包含订单总计。 

    ![购物车-购物车总计](shopping-cart/_static/image7.png)
4. 将一些其他产品（例如，飞机）添加到购物车。
5. 随即显示 " *ShoppingCart* " 页，其中包含已添加的所有产品的更新总计。 

    ![购物车-多个产品](shopping-cart/_static/image8.png)
6. 关闭浏览器窗口，停止正在运行的应用程序。

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>向购物车添加 "更新" 和 "签出" 按钮

若要允许用户修改购物车，你需要将 "**更新**" 按钮和 "**结帐**" 按钮添加到 "购物车" 页。 在本系列教程的后面部分中，将不使用 "**签出**" 按钮。

1. 在**解决方案资源管理器**中，打开 web 应用程序项目的根目录中的*ShoppingCart*页。
2. 若要将 "**更新**" 按钮和 "**签出**" 按钮添加到 " *ShoppingCart* " 页，请将黄色突出显示的标记添加到现有标记，如以下代码所示：   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

当用户单击 "**更新**" 按钮时，将调用 `UpdateBtn_Click` 事件处理程序。 此事件处理程序将调用你将在下一步中添加的代码。

接下来，你可以更新*ShoppingCart.aspx.cs*文件中包含的代码，以循环遍历购物车项并调用 `RemoveItem` 和 `UpdateItem` 方法。

1. 在**解决方案资源管理器**中，在 web 应用程序项目的根目录中打开*ShoppingCart.aspx.cs*文件。
2. 将以下代码段以黄色突出显示给*ShoppingCart.aspx.cs*文件：   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

当用户单击*ShoppingCart*页上的 "**更新**" 按钮时，将调用 UpdateCartItems 方法。 UpdateCartItems 方法获取购物车中每一项的更新值。 然后，UpdateCartItems 方法调用 `UpdateShoppingCartDatabase` 方法（在下一步中添加和说明），以添加或删除购物车中的商品。 更新数据库以反映购物车的更新后，会通过调用**gridview**的 `DataBind` 方法，在购物车页上更新**gridview**控件。 此外，还会更新 "购物车" 页上的总订单量，以反映项的更新列表。

### <a name="updating-and-removing-shopping-cart-items"></a>更新和删除购物车商品

在*ShoppingCart*页上，你可以看到已添加的控件，用于更新项的数量和删除项。 现在，添加将使这些控件工作的代码。

1. 在**解决方案资源管理器**中，打开*逻辑*文件夹中的*ShoppingCartActions.cs*文件。
2. 将以下突出显示的代码添加到*ShoppingCartActions.cs*类文件中：   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

从*ShoppingCart.aspx.cs*页上的 `UpdateCartItems` 方法调用的 `UpdateShoppingCartDatabase` 方法包含用于从购物车中更新或删除项的逻辑。 `UpdateShoppingCartDatabase` 方法将循环访问购物车列表中的所有行。 如果购物车项已标记为要删除，或数量小于1，则调用 `RemoveItem` 方法。 否则，在调用 `UpdateItem` 方法时，将检查购物车项的更新。 在删除或更新购物车项后，将保存数据库更改。

`ShoppingCartUpdates` 结构用于保存所有购物车商品。 `UpdateShoppingCartDatabase` 方法使用 `ShoppingCartUpdates` 结构来确定是否需要更新或移除任何项。

在下一教程中，你将使用 `EmptyCart` 方法在购买产品后清除购物车。 但现在，你将使用刚刚添加到*ShoppingCartActions.cs*文件的 `GetCount` 方法来确定购物车中有多少项。

### <a name="adding-a-shopping-cart-counter"></a>添加购物车计数器

若要允许用户查看购物车中的总项数，请将计数器添加到*网站母版页*。 此计数器还将充当购物车的链接。

1. 在**解决方案资源管理器**中，打开 "*网站母版页*"。
2. 通过将 "购物车计数器" 链接（如黄色中所示）添加到导航部分来修改标记，使其显示如下：  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 接下来，通过添加黄色突出显示的代码来更新*Site.Master.cs*文件的代码隐藏，如下所示：  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

在以 HTML 格式呈现页面之前，会引发 `Page_PreRender` 事件。 在 `Page_PreRender` 处理程序中，通过调用 `GetCount` 方法来确定购物车的总计数。 返回的值将添加到*网站*的标记中包含的 `cartCount` 范围。 `<span>` 标记允许正确呈现内部元素。 显示站点的任何页面时，将显示购物车总计。 用户还可以单击购物车总计来显示购物车。

## <a name="testing-the-completed-shopping-cart"></a>测试已完成的购物车

现在可以运行应用程序，了解如何添加、删除和更新购物车中的项目。 购物车总计将反映购物车中所有物品的总成本。

1. 按 **F5** 运行该应用程序。  
 浏览器将打开并显示*default.aspx*页。
2. 从类别导航菜单中选择 "**汽车**"。
3. 单击第一个产品旁边的 "**添加到购物车**" 链接。   
 将显示*ShoppingCart*页，其中包含订单总计。
4. 从类别导航菜单中选择 "**平面**"。
5. 单击第一个产品旁边的 "**添加到购物车**" 链接。
6. 将购物车中第一项的数量设置为3，并选中第二项的 "**删除项**" 复选框。<a id="a"></a>
7. 单击 "**更新**" 按钮更新 "购物车" 页，并显示新订单总计。 

    ![购物车-购物车更新](shopping-cart/_static/image9.png)

## <a name="summary"></a>总结

在本教程中，已创建 Wingtip 玩具 Web 窗体示例应用程序的购物车。 在本教程中，你使用了实体框架 Code First、数据批注、强类型化数据控件和模型绑定。

购物车支持添加、删除和更新用户选择购买的商品。 除了实现购物车功能外，还了解了如何在**GridView**控件中显示购物车项，并计算订单总计。

## <a name="addition-information"></a>附加信息

[ASP.NET 会话状态概述](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [上一页](display_data_items_and_details.md)
> [下一页](checkout-and-payment-with-paypal.md)
