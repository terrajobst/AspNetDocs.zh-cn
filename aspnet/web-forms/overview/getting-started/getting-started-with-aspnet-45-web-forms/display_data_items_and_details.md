---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 显示数据项和详细信息 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 生成 ASP.NET Web 窗体应用程序的基础知识。
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520808"
---
# <a name="display-data-items-and-details"></a>显示数据项和详细信息

作者： [Erik Reitan](https://github.com/Erikre)

> 本教程系列介绍使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 构建 ASP.NET Web 窗体应用程序的基础知识。

在本教程中，你将了解如何通过 ASP.NET Web 窗体和实体框架 Code First 来显示数据项和数据项的详细信息。 本教程以上一 "UI 和导航" 教程为基础，作为 Wingtip 玩具商店教程系列的一部分。 完成本教程后，你将在*ProductsList*页上看到产品，并在*ProductDetails*页上看到产品的详细信息。

## <a name="youll-learn-how-to"></a>你将了解如何：

- 添加数据控件以显示数据库中的产品
- 将数据控件连接到所选数据
- 添加数据控件以显示数据库中的产品详细信息
- 从查询字符串中检索值，并使用该值来限制从数据库检索的数据。

### <a name="features-introduced-in-this-tutorial"></a>本教程中引入的功能：

- 模型绑定
- 值提供程序

## <a name="add-a-data-control"></a>添加数据控件

您可以使用几个不同的选项将数据绑定到服务器控件。 最常见的包括：

* 添加数据源控件
* 手动添加代码
* 使用模型绑定

### <a name="use-a-data-source-control-to-bind-data"></a>使用数据源控件绑定数据

通过添加数据源控件，可以将数据源控件链接到显示数据的控件。 利用此方法，你可以通过声明方式（而不是以编程方式）将服务器端控件连接到数据源。

### <a name="code-by-hand-to-bind-data"></a>手动绑定数据的代码

手动编码涉及：

1. 读取值
2. 检查其是否为 null
3. 将其转换为适当的类型
4. 检查转换是否成功
5. 在查询中使用值 

利用此方法，您可以完全控制数据访问逻辑。

### <a name="use-model-binding-to-bind-data"></a>使用模型绑定来绑定数据

模型绑定使你可以使用更少的代码绑定结果，并使你能够在整个应用程序中重复使用该功能。 它简化了使用以代码为中心的数据访问逻辑，同时还提供丰富的数据绑定框架。

## <a name="display-products"></a>显示产品

在本教程中，您将使用模型绑定来绑定数据。 若要将数据控件配置为使用模型绑定来选择数据，请将控件的 `SelectMethod` 属性设置为该页的代码中的方法名称。 数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。 无需显式调用 `DataBind` 方法。

1. 在**解决方案资源管理器**中，打开*ProductList*。
2. 将现有标记替换为以下标记：   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

此代码使用名为 `productList` 的**ListView**控件显示产品。

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

对于模板和样式，您可以定义**ListView**控件显示数据的方式。 这对于任何重复结构中的数据都很有用。 尽管此**ListView**示例只显示数据库数据，但你也可以不使用代码，使用户能够编辑、插入和删除数据，以及对数据进行排序和分页。

通过设置**ListView**控件中的 `ItemType` 属性，可使用数据绑定表达式 `Item` 并且控件成为强类型。 如前面的教程中所述，可以通过 IntelliSense 选择项对象详细信息，如指定 `ProductName`：

![显示数据项和详细信息-IntelliSense](display_data_items_and_details/_static/image1.png)

你还可以使用模型绑定来指定 `SelectMethod` 值。 此值（`GetProducts`）对应于要在下一步中向隐藏的代码中添加的方法。

### <a name="add-code-to-display-products"></a>添加用于显示产品的代码

在此步骤中，你将添加代码，以便用数据库中的产品数据填充**ListView**控件。 此代码支持显示所有产品和单个类别的产品。

1. 在**解决方案资源管理器**中，右键单击*ProductList* ，然后选择 "**查看代码**"。
2. 将*ProductList.aspx.cs*文件中的现有代码替换为以下代码：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

此代码显示**ListView**控件的 `ItemType` 属性在*ProductList*页中引用的 `GetProducts` 方法。 若要将结果限制为特定的数据库类别，代码在导航到*ProductList*页面时，将设置传递到*ProductList*页的查询字符串值中的 `categoryId` 值。 `System.Web.ModelBinding` 命名空间中的 `QueryStringAttribute` 类用于检索 `id`的查询字符串变量的值。 这将指示模型绑定在运行时尝试将值从查询字符串绑定到 `categoryId` 参数。

当有效类别作为查询字符串传递到页面时，查询的结果将限于数据库中与 `categoryId` 值匹配的那些产品。 例如，如果*ProductsList*页 URL 如下所示：

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

页面仅显示 `categoryId` 等于 `1`的产品。

如果调用*ProductList*页时未包含任何查询字符串，则会显示所有产品。

这些方法的值的源称为*值提供程序*（如*QueryString*），参数属性指示要使用的值提供程序的*属性*（如 `id`）。 ASP.NET 包括 Web 窗体应用程序中的所有典型用户输入源的值提供程序和相应属性，例如查询字符串、cookie、窗体值、控件、视图状态、会话状态和配置文件属性。 你还可以编写自定义值提供程序。

### <a name="run-the-application"></a>运行此应用程序

立即运行应用程序以查看所有产品或类别的产品。

1. 在 Visual Studio 中按**F5**运行应用程序。  
   浏览器将打开并显示*default.aspx*页。

2. 从 "产品类别导航" 菜单中选择 "**汽车**"。  
   *ProductList*页仅显示**汽车**类别产品。 在本教程的后面部分中，将显示产品详细信息。  

    ![显示数据项和详细信息-汽车](display_data_items_and_details/_static/image2.png)

3. 在顶部的导航菜单中选择 "**产品**"。  
   同样，将显示 " *ProductList* " 页，但这次它显示产品的整个列表。   

    ![显示数据项和详细信息-产品](display_data_items_and_details/_static/image3.png)

4. 关闭浏览器并返回到 Visual Studio。

### <a name="add-a-data-control-to-display-product-details"></a>添加数据控件以显示产品详细信息

接下来，您将修改在上一教程中添加的*ProductDetails*页面中的标记，以显示特定的产品信息。

1. 在**解决方案资源管理器**中，打开*ProductDetails*。

2. 将现有标记替换为以下标记：

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    此代码使用**FormView**控件显示特定产品的详细信息。 此标记使用方法，如用于在*ProductList*页中显示数据的方法。 **FormView**控件用于从数据源一次显示一条记录。 使用**FormView**控件时，可以创建模板来显示和编辑数据绑定值。 这些模板包含定义窗体外观和功能的控件、绑定表达式和格式设置。

将以前的标记连接到数据库需要其他代码。

1. 在**解决方案资源管理器**中，右键单击*ProductDetails* ，然后单击 "**查看代码**"。  
   将显示*ProductDetails.aspx.cs*文件。

2. 将现有代码替换为以下代码：   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

此代码检查 "`productID`" 查询字符串值。 如果找到有效的查询字符串值，将显示匹配的产品。 如果找不到该查询字符串，或者其值无效，则不会显示任何产品。

### <a name="run-the-application"></a>运行此应用程序

现在可以运行应用程序，以查看基于产品 ID 显示的单个产品。

1. 在 Visual Studio 中按**F5**运行应用程序。  
   浏览器将打开并显示*default.aspx*页。

2. 从类别导航菜单中选择 " **Boats** "。  
   将显示*ProductList*页。

3. 从产品列表中选择 "**纸张船**"。
   将显示*ProductDetails*页。

    ![显示数据项和详细信息-产品](display_data_items_and_details/_static/image4.png)
    
4. 关闭浏览器。

## <a name="additional-resources"></a>其他资源

[通过模型绑定和 web 窗体检索和显示数据](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>后续步骤

在本教程中，你添加了标记和代码以显示产品和产品详细信息。 已了解强类型化数据控件、模型绑定和值提供程序。 在下一教程中，你将向 Wingtip 玩具示例应用程序添加购物车。 

> [!div class="step-by-step"]
> [上一页](ui_and_navigation.md)
> [下一页](shopping-cart.md)
