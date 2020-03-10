---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: 数据存储选项（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 9357ed5aef39bed501cdac9ac26d46c884d4fae0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500828"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>数据存储选项（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

大多数人都可用于关系数据库，并且在设计云应用时往往会忽略其他数据存储选项。 结果可能是性能不佳、开销较高或更糟，因为[NoSQL](http://en.wikipedia.org/wiki/NoSQL) （非关系）数据库可以比关系数据库更有效地处理一些任务。 当客户要求我们帮助解决重要的数据存储问题时，通常是因为它们有一个 NoSQL 选项可以更好地工作的关系数据库。 在这些情况下，如果客户在将应用部署到生产环境之前已经实现了 NoSQL 解决方案，则会更好一些。

另一方面，假如 NoSQL 数据库可以很好地完成一切，就是个错误。 对于所有数据存储任务，不提供单个最佳的数据管理选项;不同的数据管理解决方案针对不同的任务进行了优化。 大多数实际的云应用程序都有多种数据存储需求，并且通常通过组合多个数据存储解决方案来提供最佳服务。

本章的目的是让你更广泛地了解云应用可用的数据存储选项，并提供有关如何选择适合你的方案的基本指导。 在开发应用程序之前，最好了解可用的选项，并考虑它们的优势和劣势。 在生产应用中更改数据存储选项可能极其困难，如在飞机飞行时必须更改 jet 引擎。

## <a name="data-storage-options-on-azure"></a>Azure 上的数据存储选项

云使使用各种关系和 NoSQL 数据存储变得相对容易。 下面是一些可以在 Azure 中使用的数据存储平台。

![](data-storage-options/_static/image1.png)

该表显示了四种类型的 NoSQL 数据库：

- [键/值数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec7)为每个键值存储单个序列化的对象。 它们适用于存储大量数据，其中你希望为每个给定键值获取一个项，并且不必对该项的其他属性进行查询。

    [Azure Blob 存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/)是一个键/值数据库，其功能类似于云中的文件存储，其键值对应于文件夹和文件名。 按文件的文件夹和文件名检索文件，而不是通过搜索文件内容中的值。

    [Azure 表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)也是键/值数据库。 每个值都称为*实体*（类似于通过分区键和行键标识的行）并包含多个*属性*（与列相似，但并不是表中的所有实体都必须共享相同的列）。 对键以外的列进行查询非常低效，应避免这样做。 例如，你可以存储用户配置文件数据，其中一个分区存储有关单个用户的信息。 可以将用户名、密码哈希、出生日期等数据存储在一个实体的单独属性中，或存储在同一分区中的单独实体。 但您不希望查询具有给定的出生日期范围的所有用户，也不能在您的配置文件表和另一个表之间执行联接查询。 与关系数据库相比，表存储具有更高的可缩放性和更低的成本，但它不支持复杂的查询或联接。
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8)是键/值数据库，其中的值是*文档*。 此处的 "文档" 不能用于 Word 或 Excel 文档，而是指命名字段和值的集合，其中任何一个都可以是子文档。 例如，在订单历史记录表中，订单文档可能具有订单号、订单日期和客户字段;"客户" 字段可能有 "名称" 和 "地址" 字段。 数据库采用 XML、YAML、JSON 或 BSON 等格式编码字段数据;也可以使用纯文本。 除了键/值数据库外，一项功能是能够查询非键字段并定义辅助索引，从而使查询更有效。 此功能使文档数据库更适合于需要基于比文档键的值更复杂的条件检索数据的应用程序。 例如，在销售订单历史记录文档数据库中，您可以对各种字段进行查询，如产品 ID、客户 ID、客户名称等。 [MongoDB](http://www.mongodb.org/)是一个流行的文档数据库。
- [列系列数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec9)是键/值数据存储，使你能够将数据存储结构到称为列系列的相关列的集合中。 例如，人口普查数据库可能有一组列用于人员姓名（名字、中间名、姓氏）、一个组作为人员地址，一个组用于个人的个人资料信息（DOB、性别等）。 然后，该数据库可以将每个列系列存储在一个单独的分区中，同时为同一个键的一个人员保留所有数据。 然后，你可以读取所有配置文件信息，而无需通读所有名称和地址信息。 [Cassandra](http://cassandra.apache.org/)是一种常用的列系列数据库。
- [图形数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec10)以对象和关系的集合的形式存储信息。 Graph 数据库的目的是使应用程序能够有效地执行遍历对象网络的查询和它们之间的关系。 例如，对象可以是人力资源数据库中的员工，并且你可能希望使“查找直接或间接为 Scott 工作的所有员工”这类查询更为容易。 [Neo4j](http://www.neo4j.org/)是一个流行的图形数据库。

与关系数据库相比，NoSQL 选项为存储和分析非结构化数据提供了更大的可伸缩性和成本效益。 其缺点是它们不提供关系数据库的丰富的 queryability 和强大的数据完整性功能。 NoSQL 适用于 IIS 日志数据，这涉及到大容量，无需联接查询。 NoSQL 不适用于银行交易，这需要绝对的数据完整性，并涉及到与其他与帐户相关的数据的多个关系。

另外还有一个名为[NewSQL](http://en.wikipedia.org/wiki/NewSQL)的数据库平台，它将 NoSQL 数据库的可伸缩性与关系数据库的 queryability 和事务完整性结合起来。 NewSQL 数据库设计用于分布式存储和查询处理，这通常很难在 "OldSQL" 数据库中实现。 [NuoDB](http://www.nuodb.com/)是可在 Azure 上使用的 NewSQL 数据库的示例。

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop 和 MapReduce

可在 NoSQL 数据库中存储的大量数据很难及时有效地进行分析。 为此，可以使用实现[MapReduce](http://en.wikipedia.org/wiki/MapReduce)功能的类似于[Hadoop](http://hadoop.apache.org/)的框架。 从本质上讲，MapReduce 过程如下所示：

- 只需选择只需分析的数据，即可限制需要处理的数据的大小。 例如，你想要了解你的用户群的组成部分，只需从用户配置文件数据存储中选择出生年份即可。
- 将数据分解为各个部分，并将其发送到不同的计算机进行处理。 计算机 A 计算的人数为1950-1959 天，计算机 B 为1960-1969，等等。这组计算机称为*Hadoop 群集*。
- 完成对部件的处理后，将每个部分的结果一起放在一起。 现在，你可以获得一个相对较短的列表，其中包含每个出生年份的用户数，并且此总体列表中计算百分比的任务是可管理的。

在 Azure 上， [HDInsight](https://azure.microsoft.com/services/hdinsight/)可让你使用 Hadoop 的强大功能处理、分析大数据并从中获取新的见解。 例如，你可以使用它来分析 web 服务器日志：

- 启用 web 服务器日志记录到存储帐户。 这将设置 Azure 以便将日志写入到应用程序的每个 HTTP 请求的 Blob 服务。 Blob 服务基本上是云文件存储，它与 HDInsight 完美集成。

    ![日志到 Blob 存储](data-storage-options/_static/image2.png)
- 当应用程序获得流量时，web 服务器 IIS 日志将写入 Blob 存储。

    ![Web 服务器日志](data-storage-options/_static/image3.png)
- 在门户中，单击 "**新建**" " - **Data Services** - **hdinsight** - "**快速创建**"，并指定 hdinsight 群集名称、群集大小（hdinsight 群集数据节点数）以及 hdinsight 群集的用户名和密码。

    ![HDInsight](data-storage-options/_static/image4.png)

你现在可以设置 MapReduce 作业来分析日志，并获得如下问题的答案：

- 我的应用程序获得最多或最少流量的时间是多少？
- 我的流量来自哪个国家/地区？
- 我的流量所源自的区域的平均邻近收入是多少。 （有一个公共数据集，它为你提供按 IP 地址显示的邻居收入，你可以将其与 web 服务器日志中的 IP 地址匹配。）
- 邻近收入如何与站点中的特定页面或产品关联？

然后，可以根据客户感兴趣或可能购买特定产品的可能性，使用这些问题的答案来确定广告目标。

如 "[自动完成一切" 一章](automate-everything.md)中所述，可以在门户中执行的大多数功能都可以自动执行，其中包括设置和执行 HDInsight 分析作业。 典型的 HDInsight 脚本可能包含以下步骤：

- 预配 HDInsight 群集，并将其链接到存储帐户以进行 Blob 存储输入。
- 将 MapReduce 作业可执行文件（.jar 或 .exe 文件）上传到 HDInsight 群集。
- 提交将输出数据存储到 Blob 存储的 MapReduce。
- 等待作业完成。
- 删除 HDInsight 群集。
- 访问 Blob 存储的输出。

通过运行执行所有此功能的脚本，可以最大程度地减少预配 HDInsight 群集的时间，从而最大限度地降低成本。

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>平台即服务（PaaS）和基础结构即服务（IaaS）

前面列出的数据存储选项包括平台即服务（PaaS）和基础结构即服务（IaaS）解决方案。 PaaS 意味着我们管理硬件和软件基础结构，而你只使用服务。 SQL 数据库是 Azure 的一项 PaaS 功能。 您要求提供数据库，并在幕后 Azure 设置和配置 Vm，并在这些 Vm 上设置数据库。 你不能直接访问 Vm，无需对其进行管理。IaaS 是指设置、配置和管理在我们的数据中心基础结构中运行的 Vm，并将所需的任何内容放在其中。 我们为常见 VM 配置提供预配置的 VM 映像库。 例如，你可以为 Windows Server 2008、Windows Server 2012、BizTalk Server、Oracle WebLogic Server、Oracle Database 等安装预配置的 VM 映像。

Azure 提供的 PaaS 数据解决方案包括：

- Azure SQL 数据库（以前称为 SQL Azure）。 基于 SQL Server 的云关系数据库。
- Azure 表存储。 键/值 NoSQL 数据库。
- Azure Blob 存储。 云中的文件存储。

对于 IaaS，你可以运行可加载到 VM 的任何内容，例如：

- 关系数据库（例如 SQL Server、Oracle、MySQL、SQL Compact、SQLite 或 Postgres）。
- 键/值数据存储，如 Memcached、Redis、Cassandra 和 Riak。
- 列数据存储，如 HBase。
- 文档数据库（如 MongoDB、RavenDB 和 CouchDB）。
- 图形数据库，如 Neo4j。

![Azure 上的数据存储选项](data-storage-options/_static/image5.png)

IaaS 选项可为你提供几乎无限制的数据存储选项，其中许多选项非常易于使用，因为你可以使用预配置的映像创建 Vm。 例如，在管理门户中，转到 "**虚拟机**"，单击 "**映像**" 选项卡，然后单击 "**浏览 VM 仓库**"。

![浏览 VM 仓库](data-storage-options/_static/image6.png)

然后，你将看到[数百个预配置的 VM 映像](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)列表，你可以从已预安装数据库管理系统（如 MongoDB、Neo4J、Redis、Cassandra 或 CouchDB）的映像创建 VM：

![VM 仓库中的 MongoDB](data-storage-options/_static/image7.png)

Azure 使 IaaS 数据存储选项尽可能易用，但 PaaS 产品/服务具有许多优点，使其更加经济高效，并且适用于多种方案：

- 无需创建 Vm，只需使用门户或脚本即可设置数据存储。 如果需要 200 tb 的数据存储，只需单击一个按钮或运行命令，并在几秒钟后即可使用。
- 无需管理或修补服务所使用的 Vm;Microsoft 将自动为你执行此功能。-无需担心为缩放或高可用性设置基础结构。Microsoft 将为你处理所有这些。
- 无需购买许可证;许可费用包括在服务费用内。
- 仅为所用的部分付费。

Azure 中的 PaaS 数据存储选项包含由第三方提供商提供的产品/服务。 例如，可以从 Azure 应用商店中选择[MongoLab 外接程序](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/)，将 MongoDB 数据库配置为服务。

## <a name="choosing-a-data-storage-option"></a>选择数据存储选项

没有一种方法适用于所有方案。 如果有人说这项技术是一项技术，要问的第一件事是 "问题是什么？"，因为不同的解决方案针对不同的内容进行了优化。 关系模型有一些明确的优点;这就是为什么要如此长的原因。 但是，也可以使用 NoSQL 解决方案来解决 SQL 的停机。

通常，我们最能看到的是一个复合方法，在该方法中，你可以在单个解决方案中使用 SQL 和 NoSQL。 即使有人说他们正在使用 NoSQL，如果你深入了解他们正在执行的操作，你通常会发现他们正在使用几个不同的 NoSQL 框架：他们将[CouchDB](http://wiki.apache.org/couchdb/Introduction)、 [Redis](http://redis.io/)和[Riak](http://basho.com/riak/)用于不同的用途。 即使 Facebook 广泛使用 NoSQL，也会为服务的不同部分使用不同的 NoSQL 框架。 混合和匹配数据存储方法的灵活性是非常有用的云，因为它可以轻松地使用多个数据解决方案，并将其集成到一个应用中。

下面是选择方法时要考虑的一些问题：

| 数据语义 | -什么是核心数据存储和数据访问语义（你是在存储关系数据还是非结构化数据）？ 非结构化数据（例如媒体文件）最适合 blob 存储;相关数据的集合，例如产品、库存、供应商、客户订单等，最适合用于关系数据库。 |
| --- | --- |
| 查询支持 | -查询数据的难易程度如何？ -可以有效地询问哪些类型的问题？ 键/值数据存储非常适合于获取单个行的键值，但对于复杂的查询，则不是这样。 对于始终获取某个特定用户的数据的用户配置文件数据存储，键/值数据存储可以正常工作;对于要根据各种产品属性获得不同分组的产品目录，关系数据库的工作方式可能更好。 NoSQL 数据库可以有效地存储大量数据，但必须围绕应用查询数据的方式来构建数据库，这使得即席查询更难完成。 使用关系数据库，您可以构建几乎任何类型的查询。 |
| 函数投影 | -是否可以在服务器端执行问题、聚合等？ 如果从 SQL 中的表运行 SELECT COUNT （\*），则它将在服务器上非常高效地执行所有工作，并返回我要查找的数字。 如果我希望从 NoSQL 数据存储中进行与不支持聚合的相同计算，则这是一种低效的 "未绑定查询"，可能会超时。即使查询成功，也必须将服务器中的所有数据检索到客户端，并对客户端上的行进行计数。 -可以使用哪些语言或表达式类型？ 使用关系数据库时，可以使用 SQL。 使用一些 NoSQL 数据库（如 Azure 表存储）时，我将使用[OData](http://www.odata.org/)，我所做的只是对主键和获取投影进行筛选（选择可用字段的子集）。 |
| 易于缩放性 | -数据需要多长时间进行缩放？ -平台是否本身实现了向外扩展？ -添加/删除容量（大小和吞吐量）的难易程度如何？ 关系数据库和表不会自动分区以使它们可伸缩，因此难以扩展到超出某些限制。 Azure 表存储之类的 NoSQL 数据存储在本质上将所有内容分区，几乎没有添加分区的限制。 可以轻松地将表存储放大到 200 tb，但 Azure SQL 数据库的最大数据库大小为 500 gb。 您可以通过将关系数据分区到多个数据库中来对其进行缩放，但将应用程序设置为支持该模型涉及许多编程工作。 |
| 检测和可管理性 | -检测、监视和管理平台有多简单？ 你需要了解有关数据存储的运行状况和性能的信息，因此你需要了解平台为你提供的最新度量值，以及你需要自行开发的指标。 |
| 操作 | -在 Azure 上部署和运行平台的难易程度如何？ PaaS? IaaS? Linux? 可以轻松地在 Azure 上设置表存储和 SQL 数据库。 不是内置 Azure PaaS 解决方案的平台需要进行更多的工作。 |
| API 支持 | -可用来轻松使用平台的 API？ 对于 Azure 表服务，有一个具有支持 .NET 4.5 异步编程模型的 .NET API 的 SDK。 如果你正在编写 .NET 应用程序，则与另一个键/值列数据存储平台（其中没有 API 或不太全面的数据存储平台）相比，编写和测试 Azure 表服务的代码要容易得多。 |
| 事务完整性和数据一致性 | -为了保证数据一致性，平台是否支持事务？ 为了跟踪发送的批量电子邮件，性能和低数据存储成本可能比对数据平台中的事务或引用完整性的自动支持更重要，使 Azure 表服务成为一个不错的选择。 为了跟踪银行帐户余额或采购订单，提供强事务性保证的关系数据库平台是更好的选择。 |
| 业务连续性 | -备份、还原和灾难恢复的难易程度如何？ 更早或更高的生产数据会损坏，你将需要一个撤消函数。 关系数据库通常具有更细化的还原功能，如能够还原到某个时间点。 了解你正在考虑的每个平台中提供了哪些还原功能，这是一个重要的考虑因素。 |
| 成本 | -如果有多个平台可支持你的数据工作负荷，它们会如何以成本进行比较？ 例如，如果使用 ASP.NET Identity，则可以将用户配置文件数据存储在 Azure 表服务或 Azure SQL 数据库中。 如果不需要 SQL 数据库的丰富查询功能，可以在部分中选择 Azure 表，因为对于给定量的存储，它的成本要低得多。 |

我们通常建议你在选择数据存储解决方案之前，了解每个类别中的问题的答案。

此外，工作负载可能具有某些平台比其他平台更好地支持的特定要求。 例如:

- 您的应用程序需要审核功能吗？
- 你的数据寿命需求是什么？你需要自动存档或清除功能吗？
- 您是否有特殊的安全需求？ 例如，数据包括 PII （个人身份信息），但必须确保从查询结果中排除 PII。
- 如果出于法规或技术方面的原因，某些数据无法存储在云中，可能需要一个云数据存储平台，用于与本地存储集成。

## <a name="demo--using-sql-database-in-azure"></a>演示–使用 Azure 中的 SQL 数据库

Fix It 应用使用关系数据库来存储任务。 "[自动完成所有操作" 一章](automate-everything.md)中所示的环境创建 Windows PowerShell 脚本将创建两个 SQL 数据库实例。 单击 " **SQL 数据库**" 选项卡即可在门户中查看这些项。

![门户中的 SQL 数据库](data-storage-options/_static/image8.png)

使用门户可以轻松创建数据库。

单击 "**新数据服务**" " -- **SQL 数据库** -- "**快速创建**"，输入数据库名称，选择你的帐户中已有的服务器或创建一个新服务器，然后单击"**创建 SQL 数据库**"。

![新 SQL 数据库](data-storage-options/_static/image9.png)

请等待几秒钟，Azure 中有一个供你使用的数据库。

![已创建新的 SQL 数据库](data-storage-options/_static/image10.png)

因此，Azure 会在本地环境中花费一整天或一周或更长时间才能完成。 由于可以在脚本中轻松地自动创建数据库，或者通过使用管理 API，可以通过将数据分散到多个数据库来动态扩展，只要对应用程序进行了编程。

这是我们的平台即服务模型的示例。 您无需管理服务器。 您无需担心备份的存在。 它在高可用性中运行-数据库中的数据会自动复制到三台服务器。 如果某个计算机出现故障，我们将自动进行故障转移，而不会丢失任何数据。 服务器会定期进行修补，无需担心。

单击某个按钮，即可获取所需的确切连接字符串，并且可以立即开始使用新数据库。

![连接字符串](data-storage-options/_static/image11.png)

该仪表板显示连接历史记录和使用的存储量。

![SQL 数据库仪表板](data-storage-options/_static/image12.png)

你可以在门户中管理数据库，或使用熟悉的 SQL Server 工具（包括 SQL Server Management Studio （SSMS）和 Visual Studio tools SQL Server 对象资源管理器（SSOX）和服务器资源管理器。

![SSOX](data-storage-options/_static/image13.png)

另一种好的做法是定价模型。 你可以开始使用一个免费的 20 MB 数据库进行开发，而生产数据库每月大约 $5。 只需为实际存储在数据库中的数据量付费，而不是最大容量。 无需购买许可证。

SQL 数据库易于扩展。 对于 Fix It 应用，我们在自动化脚本中创建的数据库的上限为 1 g。 如果要将其扩展到 150 g，只需转到门户并更改该设置，或执行 REST API 命令，然后，你就可以使用 150 g 数据库将数据部署到中。

![SQL 数据库版本和大小](data-storage-options/_static/image14.png)

这就是云的强大功能，可快速轻松地构建基础结构并立即开始使用。

Fix It 应用使用两个 SQL 数据库，一个用于成员身份（身份验证和授权），另一个用于数据，而这是设置它并对其进行缩放所需的所有操作。 你以前看到过如何通过 Windows PowerShell 脚本预配数据库，现在你还了解了在门户中执行此操作是多么容易。

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>使用 ADO.NET 进行实体框架与直接数据库访问

Fix It 应用通过使用 Microsoft 推荐用于 .NET 应用程序的 ORM （对象关系映射器）实体框架来访问这些数据库。 ORM 是一个极佳的工具，可帮助开发人员工作效率，但在某些情况下，生产力会降低性能下降。 在实际的云应用程序中，你不会在使用 EF 或直接使用 ADO.NET 之间进行选择，而是使用这两种方法。 大多数情况下，当你编写适用于数据库的代码时，获得最大性能并不重要，你可以利用实体框架所获得的简化的编码和测试。 在 EF 开销会导致无法接受的性能的情况下，你可以使用 ADO.NET 编写和执行你自己的查询，理想情况下，可以调用存储过程。

无论使用哪种方法访问数据库，都需要尽可能少地使用 "交互成本"。 换言之，如果您可以在一个较大的查询结果集中获取所需的所有数据，而不是在数十个或几百个较小的结果集中，这通常是最好的做法。 例如，如果您需要列出学生和他们所注册的课程，通常最好在一个联接查询中获取所有数据，而不是在一个查询中获取学生，并对每个学生的课程执行单独的查询。

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>Fix It 应用中的 SQL 数据库和实体框架

在 Fix It 应用中，从实体框架 `DbContext` 类派生的 `FixItContext` 类标识数据库并指定数据库中的表。 上下文指定任务的实体集（表），代码将传入到上下文中的连接字符串名称。 该名称是指在 web.config 文件中定义的连接字符串。

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

*Web.config 文件中*的连接字符串名为 appdb （此处指向本地开发数据库）：

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

实体框架基于 `FixItTask` 实体类中包含的属性创建*FixItTasks*表。 这是一个简单的 POCO （普通旧 CLR 对象）类，这意味着它不会从实体框架继承，也不会依赖于。 但实体框架知道如何创建基于表的表，并对其执行 CRUD （创建-读取-更新-删除）操作。

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 表](data-storage-options/_static/image15.png)

Fix It 应用程序包括一个存储库接口，该接口用于用于处理数据存储的 CRUD 操作。

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

请注意，存储库方法都是异步的，因此可以通过完全异步方式完成所有数据访问。

存储库实现调用实体框架 async 方法来处理数据，包括 LINQ 查询以及用于插入、更新和删除操作。 下面是用于查找 Fix It 任务的代码示例。

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

你会注意到，这里还有一些计时和错误日志记录代码，我们将在稍后的 "[监视和遥测" 一章](monitoring-and-telemetry.md)中对此进行介绍。

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>在 Azure 中选择 SQL 数据库（PaaS）与 VM （IaaS）中的 SQL Server

SQL Server 和 Azure SQL 数据库的一大好处是，这两个数据库的核心编程模型都是相同的。 您可以在两种环境中使用大多数相同的技能。 甚至可以在开发中使用 SQL Server 数据库，并在云中使用 SQL 数据库实例，这就是 Fix It 应用的设置方式。

作为替代方法，可以在本地运行的云中运行相同的 SQL Server，只需要将其安装在 IaaS Vm 上即可。 对于一些旧版应用程序，在虚拟机中运行 SQL Server 可能是更好的解决方案。 由于 SQL Server 数据库在专用 VM 上运行，因此它比共享服务器上运行的 SQL 数据库数据库提供更多的资源。 这意味着 SQL Server 数据库可能会更大，并且仍能正常运行。 通常，数据库的大小和表大小越小，用于 SQL 数据库（PaaS）的用例就越好。

下面是有关如何在这两种模型之间进行选择的一些准则。

| Azure SQL 数据库 (PaaS) | 虚拟机（IaaS）中的 SQL Server |
| --- | --- |
| **专业人员**-无需创建或管理 vm、更新或修补 OS 或 SQL;Azure 会为你实现此功能。 -具有数据库级 SLA 的内置高可用性。 -低总拥有成本（TCO），因为你只需为你使用的内容付费（无需许可证）。 -适用于处理大量较小的数据库（每个数据库&lt;= 500 GB）。 -轻松动态创建新数据库以启用横向扩展。 | ***优点***-功能与本地 SQL Server 兼容。 -可以通过虚拟机级别的 SLA 在 2 + Vm 中实现 SQL Server[高可用性](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx)。 -你可以完全控制如何管理 SQL。 -可以重新使用已拥有的 SQL 许可证，也可以按小时支付一次。 -适用于处理较少但更大（1 TB +）的数据库。 |
| **缺点**-与本地 SQL Server （缺少[CLR 集成](https://technet.microsoft.com/library/ms131102.aspx)、 [TDE](https://technet.microsoft.com/library/bb934049.aspx)、[压缩支持](https://technet.microsoft.com/library/cc280449.aspx)、 [SQL SERVER REPORTING SERVICES](https://technet.microsoft.com/library/ms159106.aspx)等）相比，数据库大小限制为500gb。 | ***缺点***-更新/修补程序（OS 和 SQL）你负责创建和管理数据库，这是你的责任磁盘 IOPS （每秒输入/输出操作数），其限制为大约8000（通过16个数据驱动器）。 |

如果想要在 VM 中使用 SQL Server，可以使用自己的 SQL Server 许可证，也可以按小时支付一次。 例如，在门户中或通过 REST API 可以使用 SQL Server 映像创建新 VM。

![创建具有 SQL Server 的 VM](data-storage-options/_static/image16.png)

![SQL Server VM 映像列表](data-storage-options/_static/image17.png)

创建具有 SQL Server 映像的 VM 时，将根据 VM 的使用情况，按小时对 SQL Server 许可证成本进行评级。 如果你的项目只会运行几个月，则按小时支付会更便宜。 如果你认为你的项目将持续几年，则按你通常的方式购买许可证会成本更低。

## <a name="summary"></a>摘要

通过云计算，可以很好地混合和匹配数据存储方法，以最大程度地满足应用程序的需求。 如果要构建一个新的应用程序，请仔细考虑此处列出的问题，以选择在应用程序增长时将继续正常工作的方法。 [下一章](data-partitioning-strategies.md)将介绍一些可用于合并多个数据存储方法的分区策略。

## <a name="resources"></a>资源

有关更多信息，请参见以下资源。

选择数据库平台：

- [针对高度可扩展的解决方案的数据访问：使用 SQL、NoSQL 和 Polyglot 暂留](https://aka.ms/dag-doc)。 电子书： Microsoft 模式和实践，深入探讨适用于云应用程序的不同类型的数据存储。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/ff898430.aspx)。 请参阅数据一致性入门，数据复制和同步指南，索引表模式，具体化视图模式。
- [基本：一种 Acid 替代方法](http://queue.acm.org/detail.cfm?id=1394128)。 有关数据一致性和可伸缩性之间的权衡的文章。
- 7[周内的七个数据库：现代数据库和 NoSQL 移动的指南](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)。 Eric Redmond 和 Jim 的书籍。 强烈建议你自行介绍目前可用的数据存储平台范围。

在 SQL Server 和 SQL 数据库之间进行选择：

- [SQL 数据库高级预览版指南](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)。 介绍 SQL 数据库 Premium，并指导你如何通过 SQL 数据库 Web 版和企业版来选择它。
- [指导原则和限制（AZURE SQL Database）](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)。 门户页面，链接到有关 SQL 数据库限制的文档，其中包括侧重于 SQL 数据库不支持的 SQL Server 功能的文档。
- [Azure 虚拟机中的 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)。 门户页面，链接到有关在 Azure 中运行 SQL Server 的文档。
- [Scott Guthrie 介绍 Azure 中的 SQL 数据库](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)。 Scott Guthrie 的 SQL 数据库6分钟视频简介。
- [Azure 虚拟机中 SQL Server 的应用程序模式和开发策略](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)。

在 ASP.NET Web 应用中使用实体框架和 SQL 数据库

- [使用 MVC 5 入门与 EF 6 一起使用](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 九部分教程系列，逐步讲解如何构建使用 EF 的 MVC 应用，并将数据库部署到 Azure 和 SQL 数据库。
- [使用 Visual Studio 的 ASP.NET Web 部署](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 十二部分教程系列，更深入地介绍了如何使用 EF Code First 部署数据库。
- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 5 应用程序部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)网站。 逐步教程，逐步讲解如何创建使用身份验证的 web 应用，将应用程序表存储在成员资格数据库中，修改数据库架构，并将应用部署到 Azure。
- [ASP.NET 数据访问内容映射](https://go.microsoft.com/fwlink/p/?LinkId=282414)。 链接到用于使用 EF 和 SQL 数据库的资源。

在 Azure 上使用 MongoDB：

- [MongoLab-Azure 上的 MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)。 有关在 Azure 上运行 MongoDB 的文档的门户页。
- [创建连接到在 azure 中的虚拟机上运行的 MongoDB 的 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)网站。 介绍如何在 ASP.NET web 应用程序中使用 MongoDB 数据库的分步教程。

HDInsight （Azure 上的 Hadoop）：

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)。 [Azure](https://azure.microsoft.com/)网站上的 HDInsight 文档门户。
- [Hadoop 和 HDInsight： Azure 中的大数据](https://msdn.microsoft.com/magazine/dn385705.aspx)。 MSDN 杂志文章： Bruno Terkaly 和 Ricardo Villalobos，介绍 Azure 上的 Hadoop。
- [Microsoft 模式和实践-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅 MapReduce 模式。

> [!div class="step-by-step"]
> [上一页](single-sign-on.md)
> [下一页](data-partitioning-strategies.md)
