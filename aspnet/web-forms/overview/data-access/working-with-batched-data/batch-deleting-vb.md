---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
title: 批处理删除（VB） |Microsoft Docs
author: rick-anderson
description: 了解如何在一个操作中删除多个数据库记录。 在用户界面层中，我们构建了一个在早期 tut 中创建的增强 GridView 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4fb72f75-32ab-4bf7-a764-be20367be726
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 0974a16764eee2ef03cf36b4b15f9ef41f99982b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78476456"
---
# <a name="batch-deleting-vb"></a>批量删除 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_VB.zip)或[下载 PDF](batch-deleting-vb/_static/datatutorial65vb1.pdf)

> 了解如何在一个操作中删除多个数据库记录。 在上一教程中创建的增强 GridView 的用户界面层中。 在数据访问层中，我们将多个删除操作打包到一个事务中，以确保所有删除操作成功或回滚所有删除操作。

## <a name="introduction"></a>简介

[前面的教程](batch-updating-vb.md)探讨了如何使用完全可编辑的 GridView 创建批处理编辑界面。 在用户经常编辑多个记录的情况下，批处理编辑接口需要的回发和键盘到鼠标的上下文切换更少，从而提高最终用户的工作效率。 此方法同样适用于用户经常在一次删除多个记录的页面。

使用了联机电子邮件客户端的任何人都已熟悉最常见的一批删除接口：网格中每行的复选框以及相应的 "删除所有选中项" 按钮（参见图1）。 本教程非常简短，因为我们已经在创建基于 web 的界面和一种方法将一系列记录作为单个原子操作来删除。 在[复选框的 "添加 gridview" 列](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)教程中，我们创建了一个包含一列 Checkbox 的 GridView，并在[事务中包装数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)中，我们在 BLL 中创建了一个方法，该方法使用事务来删除 `ProductID` 值的 `List<T>`。 在本教程中，我们将生成并合并以前的体验，以创建工作批删除示例。

[每行 ![都包含一个复选框](batch-deleting-vb/_static/image1.gif)](batch-deleting-vb/_static/image1.png)

**图 1**：每行都包含一个复选框（[单击查看完全尺寸的图像](batch-deleting-vb/_static/image2.png)）

## <a name="step-1-creating-the-batch-deleting-interface"></a>步骤1：创建批处理删除接口

由于我们已在添加 "复选框" 教程的 "[添加 GridView" 列](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)中创建了批处理删除界面，因此我们只需将其复制到 `BatchDelete.aspx` 而不是从头开始创建。 首先打开 `BatchData` 文件夹中的 "`BatchDelete.aspx`" 页，并打开 `EnhancedGridView` 文件夹中的 "`CheckBoxField.aspx`" 页。 从 "`CheckBoxField.aspx`" 页上，中转到 "源" 视图，然后复制 `<asp:Content>` 标记之间的标记，如图2所示。

[![将 CheckBoxField 的声明性标记复制到剪贴板](batch-deleting-vb/_static/image2.gif)](batch-deleting-vb/_static/image3.png)

**图 2**：将 `CheckBoxField.aspx` 的声明性标记复制到剪贴板（[单击以查看完全大小的图像](batch-deleting-vb/_static/image4.png)）

接下来，`BatchDelete.aspx` 中的 "源" 视图，并将剪贴板的内容粘贴到 `<asp:Content>` 标记中。 此外，请从 `CheckBoxField.aspx.vb` 中的代码隐藏类中复制并粘贴代码，使其在 `BatchDelete.aspx.vb` 中的代码隐藏类（`DeleteSelectedProducts` "`Click`" 事件处理程序、`ToggleCheckState` 方法和 `Click` 和 `CheckAll` 的事件处理程序）中。`UncheckAll` 复制此内容后，`BatchDelete.aspx` 页 s 代码隐藏类应包含以下代码：

[!code-vb[Main](batch-deleting-vb/samples/sample1.vb)]

复制声明性标记和源代码后，请花点时间通过浏览器查看 `BatchDelete.aspx` 来测试。 你应该会看到一个 gridview，其中列出了 GridView 中的前十个产品，每行都列出了产品的名称、类别和价格以及复选框。 应有三个按钮：选中 "全部"、"取消选中" 和 "删除所选产品"。 单击 "全部选中" 按钮将选中所有复选框，而取消选中 "全部" 将清除所有复选框。 单击 "删除所选产品" 会显示一条消息，其中列出了所选产品的 `ProductID` 值，但并不实际删除产品。

[![CheckBoxField 中的接口已移动到 BatchDeleting](batch-deleting-vb/_static/image3.gif)](batch-deleting-vb/_static/image5.png)

**图 3**： `CheckBoxField.aspx` 的接口已移动到 `BatchDeleting.aspx` （[单击以查看完全大小的图像](batch-deleting-vb/_static/image6.png)）

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>步骤2：使用事务删除选中的产品

将批处理删除接口成功复制到 `BatchDeleting.aspx`后，剩下的就是更新代码，以便使用 `ProductsBLL` 类中的 `DeleteProductsWithTransaction` 方法删除已选中的产品。 此方法在[事务教程内的包装数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)中添加，接受作为其输入 `List(Of T)` `ProductID` 值，并删除事务范围内的每个相应 `ProductID`。

`DeleteSelectedProducts` 按钮 `Click` 事件处理程序当前使用以下 `For Each` 循环遍历每个 GridView 行：

[!code-vb[Main](batch-deleting-vb/samples/sample2.vb)]

对于每一行，将以编程方式引用 `ProductSelector` 复选框 Web 控件。 如果已选中此选项，则将从 `DataKeys` 集合中检索行 `ProductID`，并更新 `DeleteResults` 标签 `Text` 属性，以包括一条消息，指示已选择要删除的行。

在注释掉对 `ProductsBLL` 类 `Delete` 方法的调用时，上面的代码并不会实际删除任何记录。如果要应用此 delete 逻辑，代码将删除产品，但不会删除原子操作。 也就是说，如果序列中的前几个删除操作成功，但之后的几个删除失败（可能是由于外键约束冲突），则会引发异常，但已删除的那些产品仍将被删除。

为了确保原子性，我们需要改用 `ProductsBLL` 类的 `DeleteProductsWithTransaction` 方法。 由于此方法接受 `ProductID` 值的列表，因此，需要先从网格中编译此列表，然后将其作为参数传递。 首先创建 `Integer`类型的 `List(Of T)` 的实例。 在 `For Each` 循环中，我们需要将所选产品 `ProductID` 值添加到此 `List(Of T)`。 循环之后，必须将此 `List(Of T)` 传递到 `ProductsBLL` 类 s `DeleteProductsWithTransaction` 方法。 将 `DeleteSelectedProducts` "按钮 s `Click` 事件处理程序更新为以下代码：

[!code-vb[Main](batch-deleting-vb/samples/sample3.vb)]

更新后的代码创建 `Integer` （`productIDsToDelete`）类型的 `List(Of T)`，并用要删除的 `ProductID` 值填充该类型。 `For Each` 循环后，如果至少选择了一个产品，将调用 `ProductsBLL` 类 `DeleteProductsWithTransaction` 方法并传递此列表。 还会显示 `DeleteResults` 标签，并将数据重新绑定到 GridView （以便新删除的记录不再作为网格中的行出现）。

图4显示了选择删除多行后的 GridView。 图5在单击 "删除所选产品" 按钮后立即显示屏幕。 请注意，在图5中，已删除记录的 `ProductID` 值将显示在 GridView 下的标签中，这些行不再位于 GridView 中。

[将删除所选产品 ![](batch-deleting-vb/_static/image4.gif)](batch-deleting-vb/_static/image7.png)

**图 4**：选定的产品将被删除（[单击以查看完全大小的图像](batch-deleting-vb/_static/image8.png)）

[![已删除的产品 ProductID 值列在 GridView 下面](batch-deleting-vb/_static/image5.gif)](batch-deleting-vb/_static/image9.png)

**图 5**：已删除的产品 `ProductID` 值列在 GridView 下面（[单击以查看完全大小的图像](batch-deleting-vb/_static/image10.png)）

> [!NOTE]
> 若要测试 `DeleteProductsWithTransaction` 方法的原子性，请在 "`Order Details`" 表中为产品手动添加一个条目，然后尝试删除该产品（以及其他产品）。 尝试删除具有关联顺序的产品时，将会收到外键约束冲突，但请注意其他选定的产品删除如何回滚。

## <a name="summary"></a>摘要

创建批处理删除接口涉及到添加一个包含复选框列和一个按钮 Web 控件的 GridView，单击该按钮时，将删除所有选定的行作为单个原子操作。 在本教程中，我们通过将两个前几个教程中完成的工作拼凑在一起来构建此类接口，[添加了一个 "GridView" 列并将](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md)[数据库中的数据库修改包装](wrapping-database-modifications-within-a-transaction-vb.md)起来。 在第一个教程中，我们创建了一个包含 checkbox 列的 GridView，并在其中实现了一个方法，该方法是在对 `ProductID` 值 `List(Of T)` 传递的情况下，在事务范围内删除了这些值。

在下一教程中，我们将创建一个接口，用于执行批量插入。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Hilton Giesenow 和 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](batch-updating-vb.md)
> [下一页](batch-inserting-vb.md)
