---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
title: 更多模式和指导（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7e97cfc3-d830-4002-8ff7-5790d1ff49e6
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/more-patterns-and-guidance
msc.type: authoredcontent
ms.openlocfilehash: 57e32bf7568ecb0eb22f0f2b585310dcab2d5d43
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457071"
---
# <a name="more-patterns-and-guidance-building-real-world-cloud-apps-with-azure"></a>更多模式和指导（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

现在，你已看到13个模式，这些模式提供了有关如何在云计算中取得成功的指导。 这些只是适用于云应用的几种模式。 下面是一些更多的云计算主题和可帮助解决这些问题的资源：

- 将现有的本地应用程序迁移到云。 

    - 将[应用程序移动到云](https://msdn.microsoft.com/library/ff728592.aspx)。 Microsoft 模式和实践的电子书。 还可用作[硬拷贝平装](https://www.amazon.com/dp/1621140202)。
    - [迁移 Microsoft 的 ASP.NET 和 IIS.NET](https://go.microsoft.com/fwlink/?LinkId=400656)。 Robert Mcmurray 有关的案例研究。
    - [将第4个 &amp; Mayor 移动到 Azure 网站](http://www.jeff.wilcox.name/2013/04/4thandmayor-azure-websites/)。 Jeff Wilcox chronicling 的博客文章，将 web 应用从 Amazon Web Services 移动到 Azure App Service 中的 Web 应用。
    - [将应用迁移到 Azure：哪些更改？](https://azure.microsoft.com/documentation/videos/web-sites-internals-and-the-file-system/) Stefan Schackow 的简短视频说明 Azure App Service 中 Web 应用中的文件系统访问。
    - [Azure 混合云](https://www.amazon.com/dp/B00EOP4UQW)。 硬拷贝书籍或电子书作者： Danny Garber、Jamal Malik 和 Adam Fazio。
- 云应用程序独有的安全、身份验证和授权问题

    - [Azure 安全指南](https://azure.microsoft.com/blog/2014/02/10/best-practices-windows-azure-websites-waws/)
    - [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅看门模式-联合身份模式。
    - [Azure 网络安全](https://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx)。 白皮书： Ashin Palekar 讲述。

另请参阅[Microsoft 模式和实践的](https://msdn.microsoft.com/library/dn568099.aspx)其他云计算模式和指南-Azure 指南。

<a id="resources"></a>
## <a name="resources"></a>资源

本电子书中的每个章节都提供了指向资源的链接，以获取有关该特定主题的详细信息。 以下列表提供了一些链接，这些链接指向使用 Azure 成功进行云开发的最佳做法和建议的模式。

文档

- [在 Azure 云服务上设计大规模服务的最佳实践](https://msdn.microsoft.com/library/windowsazure/jj717232.aspx)。 通过标记 Simm 和 Michael Thomassy 的白皮书。
- [防故障：弹性云体系结构的指南](https://msdn.microsoft.com/library/windowsazure/jj853352.aspx)。 白皮书 by Marc Mercuri、Ulrich Homann 和 Andrew Townhill。 防故障视频系列的网页版本。
- [Azure 指南](https://azure.microsoft.com/develop/net/guidance/)与开发 Azure 应用程序相关的官方文档的门户页。

视频

- [用 Azure 构建实际的云应用-第1部分](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324)和[第 2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)部分。 此电子书所基于的 Guthrie 的视频。 2013年9月，在澳大利亚致辞提供。 在2013年6月，： [NDC 第1部分](http://vimeo.com/68215538)（ [NDC 第2部分](http://vimeo.com/68215602)）的挪威开发人员大会（NDC）提供了同一演示的早期版本。
- [故障安全：构建可缩放且可复原的云服务](https://channel9.msdn.com/Series/FailSafe)。 九部分视频系列： Ulrich Homann、Marc Mercuri 和 Mark Simm。 显示了一个关于如何构建云应用程序的400级别视图。 此系列重点介绍建议模式背后的理论和原因;有关详细操作方法的详细信息，请参阅通过标记 Simm 构建大系列。
- [构建大：从 Azure 客户了解的课程-第1部分](https://channel9.msdn.com/Events/Build/2012/3-029)和[第2部分](https://channel9.msdn.com/Events/Build/2012/3-030)。 由两部分组成的视频系列 Simon Davies 并标记 Simm，这与故障保护系列类似，但更适用于实际实现。

代码示例

- [此电子书附带的 Fix It 应用程序](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4?cdn_id=2013-12-03-002)。
- [适用于 Visual Studio 2012 的C# Azure 中的云服务基础知识](https://aka.ms/csf)。 Microsoft 代码库站点中可下载的项目，包括 Microsoft 客户咨询团队（CAT）开发的代码和文档。 演示了提倡中的许多最佳实践，并构建了大量视频系列和故障安全白皮书。 代码库页面还通过项目的作者链接到广泛的文档--请参阅项目说明顶部附近的蓝色框中的 "[云服务基础 wiki 集合](https://social.technet.microsoft.com/wiki/contents/articles/17987.cloud-service-fundamentals.aspx)" 链接。 此项目和该项目的文档仍在不断开发，这使它成为比类似但更早的白皮书更多的主题的信息。

硬拷贝书籍

- [云计算宝典](https://www.amazon.com/dp/0470903562)。 作者： Barrie Sosinsky。
- [发布！设计和部署生产就绪软件](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)。 Michael nygard T。
- [云体系结构模式：使用 Microsoft Azure](http://shop.oreilly.com/product/0636920023777.do)。 按帐单 Wilder。
- [Windows Azure 平台](https://www.amazon.com/dp/1430235632)。 作者： Tejaswi Redkar。
- [用于启动的 Windows Azure 编程模式](https://www.amazon.com/dp/1849685606)。 作者： Riccardo Becker。
- [Microsoft Windows Azure 开发指南](https://www.amazon.com/dp/1849682224)。 作者： Neil Mackenzie。

最后，当你开始构建真实的应用程序并在 Azure 中运行这些应用程序时，可能需要专家的帮助。 你可以在社区网站（如[azure 论坛或 StackOverflow](https://azure.microsoft.com/support/forums/)）中提问问题，也可以直接与 Microsoft 联系以获取 azure 支持。 Microsoft 提供了多个 Azure 技术支持级别：有关选项的摘要和比较，请参阅[Azure 支持](https://azure.microsoft.com/support/plans/)。

<a id="acknowledgments"></a>
## <a name="acknowledgments"></a>致谢

此内容由 Tom Dykstra、Rick Anderson 和 Mike Wasson 编写。 大多数原始内容来自[Scott Guthrie](https://weblogs.asp.net/scottgu/)，他又从标记 Simm 和 Microsoft 客户咨询团队（CAT）的材料中进行了研究。

Microsoft 的许多其他同事在草稿和代码上查看和注释：

- Tim Ammann-已查看自动化章节。
- Christopher Bennage-已查看并测试修复它的代码。
- Ryan Berry-已查看 CD/CI 章节。
- Vittorio Bertocci-已查看 SSO 章节。
- 丽丽 Clayton-帮助解决 PowerShell 脚本中的技术问题。
- Conor Cunningham-查看了数据存储选项章节。
- Carlos Farre-经过审核和测试，解决了安全问题。
- Larry Franks-查看了遥测和监视章节。
- Jonathan Gao-查看数据存储选项章节的 Hadoop 和 MapReduce 部分。
- Sidney Higa-回顾了所有章节。
- Gordon Hogenson-已查看源代码管理章节。
- Tamra Myers-查看的数据存储选项、blob 和队列章节。
- Pranav Rastogi 撰写-已查看 SSO 章节。
- 6月 Blender Rogers-向 PowerShell 自动化脚本添加了错误处理和帮助。
- Mani Subramanian-回顾了所有章节，并 led 介绍了 Fix It 代码的代码评审和测试过程。
- Shaun Tinline-jones-已查看数据分区章节。
- Selcin Tukarslan 的章节介绍了 SQL 数据库和 SQL Server。
- Edward Wu 为 SSO 提供的示例代码。
- Guang 脱离-已编写 PowerShell 自动化脚本。

[Microsoft 开发人员指南咨询委员会](https://aka.ms/DGAC)（DGAC）的成员还在草稿上查看和注释：

- Jean-Luc Boucho
- Catalin Gheorghiu
- Wouter de Kort
- Carlos dos Santos
- Neil Mackenzie
- Dennis Persson
- Sunil Sabat
- [Aleksey Sinyagin](http://www.linkedin.com/in/sinyagin)
- 帐单 Wagner
- Michael 木材

DGAC 的其他成员已查看并注释初步概述：

- Damir Arh
- Edward Bakker
- Srdjan Bozovic
- Tao-ming Man 更改
- Gianni Rosa Gallina
- 圣保罗 Morgado
- Jason Oliveira
- Alberto Poblacion
- Ryan Riley
- Perez Jones Tsisah
- Roger Whitehead
- Pawel Wilkosz

> [!div class="step-by-step"]
> [上一页](queue-centric-work-pattern.md)
> [下一页](the-fix-it-sample-application.md)
