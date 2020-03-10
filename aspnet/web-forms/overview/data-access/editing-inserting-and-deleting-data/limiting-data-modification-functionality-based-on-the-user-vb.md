---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
title: 限制基于用户的数据修改功能（VB） |Microsoft Docs
author: rick-anderson
description: 在允许用户编辑数据的 web 应用程序中，不同的用户帐户可能具有不同的数据编辑权限。 在本教程中，我们将探讨如何
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 9dc264a6-feb8-474b-8b91-008c50708065
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
msc.type: authoredcontent
ms.openlocfilehash: c257a930e4d27fcd42591a541e700786bf413bf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491918"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-vb"></a>限制基于用户的数据修改功能 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_VB.exe)或[下载 PDF](limiting-data-modification-functionality-based-on-the-user-vb/_static/datatutorial23vb1.pdf)

> 在允许用户编辑数据的 web 应用程序中，不同的用户帐户可能具有不同的数据编辑权限。 在本教程中，我们将检查如何根据访问用户动态调整数据修改功能。

## <a name="introduction"></a>简介

许多 web 应用程序都支持用户帐户，并基于登录用户提供不同的选项、报表和功能。 例如，在我们的教程中，我们可能希望允许供应商公司的用户登录到站点，并更新有关其产品的一般信息-每个单位的名称和数量，或许还包括供应商信息，如公司名称、地址、联系人信息，等等。 此外，我们可能希望为公司中的人员包含某些用户帐户，以便他们能够登录和更新产品信息，如股票、重新排序级别等。 我们的 web 应用程序还可能允许匿名用户访问（没有登录的人员），但会将其限制为仅查看数据。 使用此类用户帐户系统时，我们希望 ASP.NET 页面中的数据 Web 控件能够提供适用于当前已登录用户的插入、编辑和删除功能。

在本教程中，我们将检查如何根据访问用户动态调整数据修改功能。 具体而言，我们将创建一个页面，该页面将在可编辑的 DetailsView 中显示供应商信息，并使用一个 GridView 列出供应商提供的产品。 如果访问该页面的用户来自我们的公司，他们可以：查看任何供应商的信息;编辑其地址;和编辑供应商提供的任何产品的信息。 但是，如果用户来自特定的公司，则他们只能查看和编辑其自己的地址信息，并且只能编辑未标记为 "已停用" 的产品。

[![公司的用户可以编辑任何供应商的信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image1.png)

**图 1**：我们的公司中的用户可以编辑任何供应商的信息（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image3.png)）

[![特定供应商提供的用户只能查看和编辑其信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image4.png)

**图 2**：特定供应商提供的用户只能查看和编辑其信息（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image6.png)）

让我们开始吧！

> [!NOTE]
> ASP.NET 2.0 s 成员资格系统提供了一种标准化的可扩展平台，用于创建、管理和验证用户帐户。 由于对成员资格系统的检查超出了这些教程的范围，因此本教程会允许匿名访问者选择是来自特定供应商还是来自公司，而不是 "fakes" 成员资格。 有关成员身份的详细信息，请参阅我的[检查 ASP.NET 2.0 s 成员资格、角色和配置文件](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)文章系列。

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>步骤1：允许用户指定其访问权限

在实际的 web 应用程序中，用户的帐户信息将包括用户是否适用于公司或特定的供应商，并且用户登录到站点后，可以通过 ASP.NET 页面以编程方式访问此信息。 此信息可通过 ASP.NET 2.0 s 角色系统捕获，作为通过配置文件系统的用户级帐户信息，或通过某些自定义方式捕获。

由于本教程的目的是演示如何基于已登录用户调整数据修改功能，而不是展示 ASP.NET 2.0 s 的成员资格、角色和配置文件系统，因此我们将使用一种非常简单的机制来确定用户访问页面的功能-用户可从该 DropDownList 指示他们是否应该能够查看和编辑任何供应商信息，或者他们可以查看和编辑哪些特定的供应商信息。 如果用户指示她可以查看和编辑所有供应商信息（默认值），则她可以逐页浏览所有供应商、编辑任何供应商的地址信息，并编辑所选供应商提供的任何产品的名称和数量。 但是，如果用户指示她只可以查看和编辑特定供应商，则她只可以查看该供应商的详细信息和产品，并且只能为*未*停用的产品更新名称和数量。

本教程的第一步是创建此 DropDownList，并将其填充到系统中的供应商。 打开 `EditInsertDelete` 文件夹中的 "`UserLevelAccess.aspx`" 页，添加其 `ID` 属性设置为 `Suppliers`的 DropDownList，并将此 DropDownList 绑定到名为 `AllSuppliersDataSource`的新 ObjectDataSource。

[![创建一个名为 AllSuppliersDataSource 的新 ObjectDataSource](limiting-data-modification-functionality-based-on-the-user-vb/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image7.png)

**图 3**：创建名为 `AllSuppliersDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image9.png)）

由于我们希望此 DropDownList 包含所有供应商，因此请将 ObjectDataSource 配置为调用 `SuppliersBLL` 类 `GetSuppliers()` 方法。 此外，请确保将 ObjectDataSource `Update()` 方法映射到 `SuppliersBLL` 类 `UpdateSupplierAddress` 方法，因为此 ObjectDataSource 还将由我们在步骤2中添加的 DetailsView 使用。

完成 ObjectDataSource 向导后，通过配置 `Suppliers` DropDownList 来完成这些步骤，以便显示 `CompanyName` 数据字段并使用 `SupplierID` 数据字段作为每个 `ListItem`的值。

[![将供应商 DropDownList 配置为使用 "公司名称" 和 "供应商" 数据字段](limiting-data-modification-functionality-based-on-the-user-vb/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image10.png)

**图 4**：将 `Suppliers` DropDownList 配置为使用 "`CompanyName`" 和 "`SupplierID` 数据" 字段（[单击以查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image12.png)）

此时，DropDownList 列出了数据库中供应商的公司名称。 但是，我们还需要在 DropDownList 中包含 "显示/编辑所有供应商" 选项。 若要实现此目的，请将 `Suppliers` DropDownList s `AppendDataBoundItems` 属性设置为 `true`，然后添加 `Text` 属性为 "显示/编辑所有供应商" 的 `ListItem`，其值为 `-1`。 这可以通过声明性标记直接添加，也可以通过设计器添加，方法是转到属性窗口并单击 DropDownList s `Items` 属性中的省略号。

> [!NOTE]
> 若要详细了解如何将 Select All 项添加到数据绑定 DropDownList，请参阅使用 DropDownList 教程返回到[*大纲/详细信息筛选*](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)。

设置 `AppendDataBoundItems` 属性并添加 `ListItem` 后，DropDownList 的声明性标记应如下所示：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample1.aspx)]

图5显示了通过浏览器查看当前进度的屏幕截图。

[![供应商 DropDownList 包含 "显示所有项"，每个供应商对应一个](limiting-data-modification-functionality-based-on-the-user-vb/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image13.png)

**图 5**： `Suppliers` DropDownList 包含 "全部显示" `ListItem`，并为每个供应商提供一个（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image15.png)）

由于我们希望在用户更改其选择后立即更新用户界面，因此请将 `Suppliers` DropDownList s `AutoPostBack` 属性设置为 "`true`"。 在步骤2中，我们将创建一个 DetailsView 控件，该控件将基于 DropDownList 选择显示供应商的信息。 然后，在步骤3中，我们将为此 DropDownList `SelectedIndexChanged` 事件创建事件处理程序，我们将添加代码，用于根据所选供应商将相应的供应商信息绑定到 DetailsView。

## <a name="step-2-adding-a-detailsview-control"></a>步骤2：添加 DetailsView 控件

让我们使用 DetailsView 来显示供应商信息。 对于可以查看和编辑所有供应商的用户，DetailsView 将支持分页，并允许用户一次单步执行一条记录的供应商信息。 但是，如果用户适用于特定的供应商，则 DetailsView 只显示该特定供应商的信息，而不包括寻呼接口。 在任一情况下，DetailsView 都需要允许用户编辑供应商的地址、城市和国家/地区字段。

将 DetailsView 添加到 `Suppliers` DropDownList 下的页，将其 `ID` 属性设置为 `SupplierDetails`，并将其绑定到在上一步中创建的 `AllSuppliersDataSource` ObjectDataSource。 接下来，选中 "启用分页" 和 "启用编辑" 复选框。

> [!NOTE]
> 如果未在 DetailsView s 智能标记中看到 "启用编辑" 选项，则这是因为未将 ObjectDataSource `Update()` 方法映射到 `SuppliersBLL` 类 s `UpdateSupplierAddress` 方法。 请花点时间返回并进行此配置更改，之后 DetailsView s 智能标记中应显示 "启用编辑" 选项。

由于 `SuppliersBLL` 类 `UpdateSupplierAddress` 方法仅接受四个参数： `supplierID`、`address`、`city`和 `country` 修改 DetailsView s 的 BoundFields，以使 `CompanyName` 和 `Phone` BoundFields 为只读。 此外，`SupplierID` 完全删除的 BoundField。 最后，`AllSuppliersDataSource` ObjectDataSource 当前将其 `OldValuesParameterFormatString` 属性设置为 "`original_{0}`"。 请花点时间从声明性语法中删除此属性设置，或将其设置为默认值 `{0}`。

配置 `SupplierDetails` DetailsView 并 `AllSuppliersDataSource` ObjectDataSource 后，我们将获得以下声明性标记：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample2.aspx)]

此时，DetailsView 可以分页到，并且所选供应商的地址信息可以更新，而不管 `Suppliers` DropDownList 中所做的选择（参见图6）。

[![可以查看任何供应商信息，并更新其地址](limiting-data-modification-functionality-based-on-the-user-vb/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image16.png)

**图 6**：可以查看所有供应商信息，并更新其地址（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image18.png)）

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>步骤3：仅显示所选供应商的信息

页面当前显示所有供应商的信息，无论是否从 `Suppliers` DropDownList 中选择了特定的供应商。 为了只显示所选供应商的供应商信息，我们需要向页面中添加另一个 ObjectDataSource，其中一个用于检索有关特定供应商的信息。

将新的 ObjectDataSource 添加到页面，并将其命名为 `SingleSupplierDataSource`。 在其智能标记中，单击 "配置数据源" 链接，并使其使用 `SuppliersBLL` 类 `GetSupplierBySupplierID(supplierID)` 方法。 与 `AllSuppliersDataSource` ObjectDataSource 一样，将 `SingleSupplierDataSource` ObjectDataSource s `Update()` 方法映射到 `SuppliersBLL` 类 `UpdateSupplierAddress` 方法。

[![将 SingleSupplierDataSource ObjectDataSource 配置为使用 GetSupplierBySupplierID （供应商）方法](limiting-data-modification-functionality-based-on-the-user-vb/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image19.png)

**图 7**：将 `SingleSupplierDataSource` ObjectDataSource 配置为使用 `GetSupplierBySupplierID(supplierID)` 方法（[单击查看完全大小的映像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image21.png)）

接下来，系统将提示您指定 `GetSupplierBySupplierID(supplierID)` 方法 s `supplierID` 输入参数的参数源。 由于我们要显示从 DropDownList 中选择的供应商的信息，因此请使用 `Suppliers` DropDownList s `SelectedValue` 属性作为参数源。

[![使用供应商 DropDownList 作为供应商参数源](limiting-data-modification-functionality-based-on-the-user-vb/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image22.png)

**图 8**：使用 `Suppliers` DropDownList 作为 `supplierID` 参数源（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image24.png)）

即使添加了此第二个 ObjectDataSource，DetailsView 控件当前也配置为始终使用 `AllSuppliersDataSource` ObjectDataSource。 我们需要添加逻辑来调整 DetailsView 所使用的数据源，具体取决于所选的 `Suppliers` DropDownList 项。 为此，请为 DropDownList 供应商创建一个 `SelectedIndexChanged` 事件处理程序。 通过双击设计器中的 DropDownList，可以轻松地创建此项。 此事件处理程序需要确定要使用的数据源，并必须将数据重新绑定到 DetailsView。 这是通过以下代码完成的：

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample3.vb)]

此事件处理程序首先确定是否选择了 "显示/编辑所有供应商" 选项。 如果是，则它将 `SupplierDetails` DetailsView s `DataSourceID` 设置为 `AllSuppliersDataSource`，并通过将 `PageIndex` 属性设置为0，将用户返回到供应商组中的第一条记录。 但是，如果用户从 DropDownList 中选择了特定的供应商，则将 `DataSourceID` DetailsView s 分配给 `SingleSuppliersDataSource`。 无论使用何种数据源，都将 `SuppliersDetails` 模式恢复为只读模式，并通过调用 `SuppliersDetails` 控制 s `DataBind()` 方法将数据重新绑定到 DetailsView。

使用此事件处理程序后，DetailsView 控件现在会显示选定的供应商，除非选择了 "显示/编辑所有供应商" 选项，在这种情况下，所有供应商都可以通过分页界面查看。 图9显示了选中 "显示/编辑所有供应商" 选项的页面;请注意，存在分页接口，允许用户访问和更新任何供应商。 图10显示了选定了 Ma Maison 供应商的页面。 在这种情况下，仅可查看和编辑 Ma Maison 的信息。

[![可以查看和编辑所有供应商信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image25.png)

**图 9**：所有供应商信息都可以查看和编辑（[单击查看完全尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image27.png)）

[仅 ![可以查看和编辑所选供应商的信息](limiting-data-modification-functionality-based-on-the-user-vb/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image28.png)

**图 10**：只可以查看和编辑所选供应商的信息（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image30.png)）

> [!NOTE]
> 对于本教程，必须将 "DropDownList" 和 "DetailsView" 控制 `EnableViewState` 设置为 `true` （默认值），因为 DropDownList s `SelectedIndex` 和 DetailsView s `DataSourceID` 属性 s 更改必须在回发之间保留。

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>步骤4：在可编辑的 GridView 中列出供应商产品

完成 DetailsView 后，下一步是包含可编辑的 GridView，其中列出了所选供应商提供的产品。 此 GridView 应该只允许对 `ProductName` 和 `QuantityPerUnit` 字段进行编辑。 而且，如果访问此页的用户来自特定的供应商，则只允许更新那些*不*停用的产品。 为实现此目的，我们需要首先添加 `ProductsBLL` 类 `UpdateProducts` 方法的重载，该重载只采用 `ProductID`、`ProductName`和 `QuantityPerUnit` 字段作为输入。 在许多教程中，我们提前完成了这一过程，因此，只需查看此处的代码即可 `ProductsBLL`：

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample4.vb)]

创建了此重载后，便可以添加 GridView 控件及其关联的 ObjectDataSource。 向页面添加一个新的 GridView，将其 `ID` 属性设置为 `ProductsBySupplier`，并将其配置为使用名为 `ProductsBySupplierDataSource`的新 ObjectDataSource。 由于我们希望此 GridView 按所选供应商列出这些产品，因此请使用 `ProductsBLL` 类 s `GetProductsBySupplierID(supplierID)` 方法。 还将 `Update()` 方法映射到刚刚创建的新 `UpdateProduct` 重载。

[![将 ObjectDataSource 配置为使用刚创建的 UpdateProduct 重载](limiting-data-modification-functionality-based-on-the-user-vb/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image31.png)

**图 11**：将 ObjectDataSource 配置为使用刚创建的 `UpdateProduct` 重载（[单击查看完全大小的映像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image33.png)）

系统将提示为 `GetProductsBySupplierID(supplierID)` 方法 s `supplierID` 输入参数选择参数源。 由于我们希望在 DetailsView 中显示所选供应商的产品，因此，请使用 `SuppliersDetails` DetailsView 控件 s `SelectedValue` 属性作为参数源。

[![使用 SuppliersDetails DetailsView s SelectedValue 属性作为参数源](limiting-data-modification-functionality-based-on-the-user-vb/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image34.png)

**图 12**：使用 `SuppliersDetails` DetailsView s `SelectedValue` 属性作为参数源（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image36.png)）

返回到 GridView，删除除 `ProductName`、`QuantityPerUnit`和 `Discontinued`之外的所有 GridView 字段，并将 `Discontinued` CheckBoxField 标记为只读。 另外，请检查 GridView s 智能标记的启用编辑选项。 进行这些更改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample5.aspx)]

与我们以前的 Objectdatasource 一样，这一 `OldValuesParameterFormatString` 属性设置为 `original_{0}`，这会在尝试更新产品的名称或数量时导致问题。 从声明性语法中删除此属性或将其设置为默认值 `{0}`。

完成此配置后，我们的页面现在会列出在 GridView 中选择的供应商提供的产品（参见图13）。 当前可以更新每个单位的*任何*产品名称或数量。 但是，我们需要更新页面逻辑，以便对与特定供应商相关联的用户禁止使用此类功能。 我们将在步骤5中处理这最后一段。

[显示选定供应商提供的产品 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image37.png)

**图 13**：显示了所选供应商提供的产品（[单击以查看完全尺寸的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image39.png)）

> [!NOTE]
> 添加此可编辑的 GridView 后，应该更新 `Suppliers` DropDownList s `SelectedIndexChanged` 事件处理程序，以使 GridView 返回到只读状态。 否则，如果在编辑产品信息的过程中选择了不同的供应商，则新供应商的 GridView 中对应的索引也可以编辑。 若要防止出现这种情况，只需在 `SelectedIndexChanged` 事件处理程序中将 GridView s `EditIndex` 属性设置为 `-1`。

另外，请记住，必须启用 GridView 的视图状态（默认行为）。 如果将 GridView `EnableViewState` 属性设置为 "`false`"，则可能会遇到使并发用户无意中删除或编辑记录的风险。 有关详细信息，请参阅[ASP.NET 2.0 GridViews/DetailsView/FormViews 的并发问题，其中支持编辑和/或删除并禁用了其视图状态](http://scottonwriting.net/sowblog/posts/10054.aspx)。

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>步骤5：不选择 "显示/编辑所有供应商" 时不允许编辑已停用的产品

尽管 `ProductsBySupplier` GridView 完全正常运行，但它目前对来自特定供应商的用户授予过多的访问权限。 根据我们的业务规则，此类用户应该不能更新废止的产品。 若要强制执行此方法，可以在用户从供应商处访问该页面时，隐藏（或禁用）这些 GridView 行中的 "编辑" 按钮。

为 GridView `RowDataBound` 事件创建事件处理程序。 在此事件处理程序中，我们需要确定用户是否与特定的供应商相关联，在本教程中，可以通过检查供应商 DropDownList s `SelectedValue` 属性来确定该用户是否已与该供应商相关联，如果它不是-1，则用户与特定的供应商相关联。 对于此类用户，我们需要确定产品是否已停止使用。 我们可以通过 `e.Row.DataItem` 属性获取对绑定到 GridView 行的实际 `ProductRow` 实例的引用，如在[ *"GridView" 页脚教程中显示摘要信息*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)中所述。 如果产品已停止使用，我们可以使用上一教程中所述的技术，使用上一教程中所述的技术[ *，在 GridView*](adding-client-side-confirmation-when-deleting-vb.md)s CommandField 中获取对 "编辑" 按钮的编程参考。 获得引用后，可以隐藏或禁用该按钮。

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample6.vb)]

使用此事件处理程序时，如果以用户身份从特定供应商处访问此页，则不能编辑这些产品，因为对这些产品隐藏 "编辑" 按钮。 例如，Chef Anton s Gumbo Mix 是新奥尔良 Cajun 乐趣供应商停产的产品。 在访问此特定供应商的页面时，将隐藏该产品的 "编辑" 按钮（见图14）。 但是，当使用 "显示/编辑所有供应商" 进行访问时，可以使用 "编辑" 按钮（见图15）。

[![对于特定于供应商的用户，将隐藏 Chef Anton s Gumbo 混合的 "编辑" 按钮](limiting-data-modification-functionality-based-on-the-user-vb/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image40.png)

**图 14**：对于特定于供应商的用户，Chef Anton s Gumbo Mix 的 "编辑" 按钮已隐藏（[单击查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image42.png)）

[![显示/编辑所有供应商用户，则显示 Chef Anton s Gumbo 混合的 "编辑" 按钮](limiting-data-modification-functionality-based-on-the-user-vb/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image43.png)

**图 15**：对于 "显示/编辑所有供应商用户"，将显示 "Chef Anton s Gumbo 混合" 编辑按钮（[单击以查看完全大小的图像](limiting-data-modification-functionality-based-on-the-user-vb/_static/image45.png)）

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>检查业务逻辑层中的访问权限

在本教程中，"ASP.NET" 页处理有关用户可以查看的信息以及可更新的产品的所有逻辑。 理想情况下，此逻辑也会出现在业务逻辑层中。 例如，`SuppliersBLL` 类 `GetSuppliers()` 方法（返回所有供应商）可能包含检查以确保当前登录的用户*不*与特定的供应商相关联。 同样，`UpdateSupplierAddress` 方法可能包括检查以确保当前登录的用户适用于我们的公司（因此可以更新所有供应商地址信息）或与要更新其数据的供应商相关联。

我在本教程中并未包括此类 BLL 层检查，因为在本教程中，用户的权限由 DropDownList 上的一个非层次，而 BLL 类无法访问。 当使用 ASP.NET （如 Windows 身份验证）提供的成员资格系统或现成的身份验证方案之一时，可以从 BLL 访问当前登录的用户的信息和角色信息，从而进行此类访问可在表示层和 BLL 层上检查权限。

## <a name="summary"></a>摘要

大多数提供用户帐户的站点都需要基于登录用户自定义数据修改接口。 管理用户可以删除和编辑任何记录，而非管理用户可能被限制为仅更新或删除他们自行创建的记录。 无论方案是哪种情况，都可以通过扩展数据 Web 控件、ObjectDataSource 和业务逻辑层类来添加或拒绝基于登录用户的某些功能。 在本教程中，我们了解了如何根据用户是否与特定的供应商相关联，或是否为公司工作，来限制可查看和可编辑的数据。

本教程介绍了如何使用 GridView、DetailsView 和 FormView 控件来插入、更新和删除数据。 从下一教程开始，我们将重点介绍如何添加分页和排序支持。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](adding-client-side-confirmation-when-deleting-vb.md)
