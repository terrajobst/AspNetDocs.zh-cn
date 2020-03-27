---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '迭代 #3 –添加窗体验证（VB） |Microsoft Docs'
author: microsoft
description: 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证 emai 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437966"
---
# <a name="iteration-3--add-form-validation-vb"></a>迭代 #3 –添加窗体验证（VB）

by [Microsoft](https://github.com/microsoft)

[下载代码](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序（VB）

在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。 联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。

我们通过多个迭代生成应用程序。 随着每次迭代，我们将逐步改进应用程序。 此多个迭代方法的目标是使您能够了解每个更改的原因。

- 迭代 #1-创建应用程序。 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

- 迭代 #2-使应用程序看起来不错。 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

- 迭代 #3-添加窗体验证。 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

- 迭代 #4-使应用程序松散耦合。 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 #5-创建单元测试。 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

- 迭代 #6-使用测试驱动开发。 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代 #7-添加 Ajax 功能。 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="this-iteration"></a>此迭代

在联系人管理器应用程序的第二次迭代中，我们添加了基本的窗体验证。 我们会在不输入所需表单域的值的情况下，阻止用户提交联系人。 我们还验证电话号码和电子邮件地址（请参阅图1）。

[!["新建项目" 对话框](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)

**图 01**：具有验证的窗体（[单击以查看完全大小的图像](iteration-3-add-form-validation-vb/_static/image2.png)）

在此迭代中，我们会将验证逻辑直接添加到控制器操作。 通常，不建议将验证添加到 ASP.NET MVC 应用程序。 更好的方法是将应用程序的验证逻辑放在单独的[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。 在下一次迭代中，我们重构联系人管理器应用程序，使应用程序更易于维护。

在这种情况下，为了简单起见，我们将手动编写所有验证代码。 我们可以利用验证框架，而不是自己编写验证代码。 例如，你可以使用 Microsoft 企业库验证应用程序块（VAB）来实现 ASP.NET MVC 应用程序的验证逻辑。 若要了解有关验证应用程序块的详细信息，请参阅：

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>将验证添加到创建视图

首先，让我们将验证逻辑添加到创建视图。 幸运的是，因为我们生成了带有 Visual Studio 的 "创建" 视图，所以 "创建" 视图已包含所有必要的用户界面逻辑来显示验证消息。 "创建" 视图包含在 "列表 1" 中。

**列表 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

字段验证-error 类用于为 ValidationMessage （） helper 呈现的输出绘制样式。 输入验证-错误类用于对由 Html. TextBox （） helper 呈现的文本框（输入）进行样式。 验证摘要-错误类用于对 ValidationSummary （）帮助程序呈现的无序列表进行样式。

> [!NOTE] 
> 
> 您可以修改本部分中所述的样式表类，以自定义验证错误消息的外观。

## <a name="adding-validation-logic-to-the-create-action"></a>将验证逻辑添加到创建操作

现在，Create view 从不显示验证错误消息，因为我们尚未编写用于生成任何消息的逻辑。 为了显示验证错误消息，需要将错误消息添加到 ModelState。

> [!NOTE] 
> 
> 将窗体字段的值分配给属性错误时，UpdateModel （）方法会自动将错误消息添加到 ModelState 中。 例如，如果您尝试将字符串 "apple" 分配给接受日期时间值的出生日期属性，则 UpdateModel （）方法会将错误添加到 ModelState 中。

清单2中修改的 Create （）方法包含一个新部分，该部分将在新联系人插入数据库之前验证 Contact 类的属性。

**列表 2-Controllers\ContactController.vb （通过验证创建）**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

"验证" 部分强制实施四个不同的验证规则：

- FirstName 属性的长度必须大于零（并且不能仅包含空格）
- LastName 属性的长度必须大于零（并且不能仅包含空格）
- 如果电话属性具有值（长度大于0），则电话属性必须与正则表达式匹配。
- 如果电子邮件属性的值（长度大于0），则 Email 属性必须与正则表达式匹配。

如果违反了验证规则，则会将错误消息添加到 ModelState 中的 AddModelError （）方法的帮助下。 将消息添加到 ModelState 时，请提供属性的名称和验证错误消息的文本。 此错误消息将通过 ValidationSummary （）和 ValidationMessage （）帮助程序方法显示在视图中。

执行验证规则后，将检查 ModelState 的 IsValid 属性。 当任何验证错误消息已添加到 ModelState 时，IsValid 属性返回 false。 如果验证失败，则会重新显示带有错误消息的 Create 窗体。

> [!NOTE] 
> 
> 我获取了用于在 [ *http://regexlib.com* ](http://regexlib.com) 中验证正则表达式存储库中的电话号码和电子邮件地址的正则表达式。

## <a name="adding-validation-logic-to-the-edit-action"></a>向编辑操作添加验证逻辑

Edit （）操作更新联系人。 Edit （）操作需要执行与 Create （）操作完全相同的验证。 我们应重构 Contact controller，使 Create （）和 Edit （）操作都调用同一验证方法，而不是复制相同的验证代码。

修改后的 Contact controller 类包含在列表3中。 此类有一个新的 ValidateContact （）方法，该方法在 Create （）和 Edit （）操作中调用。

**Listing 3 - Controllers\ContactController.vb**

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a>Summary

在此迭代中，我们向联系人管理器应用程序添加了基本的窗体验证。 我们的验证逻辑阻止用户提交新的联系人或编辑现有联系人，而不提供 FirstName 和 LastName 属性的值。 此外，用户必须提供有效的电话号码和电子邮件地址。

在此迭代中，我们以尽可能最简单的方式将验证逻辑添加到了联系人管理器应用程序。 但是，将我们的验证逻辑混合到我们的控制器逻辑将会在长期中产生问题。 随着时间的推移，我们的应用程序将更难以维护和修改。

在下一次迭代中，我们将从控制器重构验证逻辑和数据库访问逻辑。 我们将利用几项软件设计原则，使我们能够创建更松耦合、更易于维护的应用程序。

> [!div class="step-by-step"]
> [上一页](iteration-2-make-the-application-look-nice-vb.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-vb.md)
