---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 数据源控件 |Microsoft Docs
author: microsoft
description: ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。 但是，这并不是用户友好的，因为它可能已经 ...。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519350"
---
# <a name="data-source-controls"></a><span data-ttu-id="4218c-104">数据源控件</span><span class="sxs-lookup"><span data-stu-id="4218c-104">Data Source Controls</span></span>

<span data-ttu-id="4218c-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4218c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4218c-106">ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。</span><span class="sxs-lookup"><span data-stu-id="4218c-106">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="4218c-107">但是，它并不像用户那样友好，因为它可能已经存在。</span><span class="sxs-lookup"><span data-stu-id="4218c-107">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="4218c-108">它仍需要大量的代码来从其获取有用的功能。</span><span class="sxs-lookup"><span data-stu-id="4218c-108">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="4218c-109">这就是在1.x 中的所有数据访问工作中的模型。</span><span class="sxs-lookup"><span data-stu-id="4218c-109">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="4218c-110">ASP.NET 1.x 中的 DataGrid 控件在 Web 应用程序中对数据访问进行了很大的改进。</span><span class="sxs-lookup"><span data-stu-id="4218c-110">The DataGrid control in ASP.NET 1.x marked a great improvement in data access in Web applications.</span></span> <span data-ttu-id="4218c-111">但是，它并不像用户那样友好，因为它可能已经存在。</span><span class="sxs-lookup"><span data-stu-id="4218c-111">However, it wasn't as user-friendly as it could have been.</span></span> <span data-ttu-id="4218c-112">它仍需要大量的代码来从其获取有用的功能。</span><span class="sxs-lookup"><span data-stu-id="4218c-112">It still required a considerable amount of code to obtain much useful functionality from it.</span></span> <span data-ttu-id="4218c-113">这就是在1.x 中的所有数据访问工作中的模型。</span><span class="sxs-lookup"><span data-stu-id="4218c-113">Such is the model in all data access endeavors in 1.x.</span></span>

<span data-ttu-id="4218c-114">ASP.NET 2.0 在部分中与数据源控件进行寻址。</span><span class="sxs-lookup"><span data-stu-id="4218c-114">ASP.NET 2.0 addresses this with in part with data source controls.</span></span> <span data-ttu-id="4218c-115">ASP.NET 2.0 中的数据源控件为开发人员提供了用于检索数据、显示数据和编辑数据的声明性模型。</span><span class="sxs-lookup"><span data-stu-id="4218c-115">The data source controls in ASP.NET 2.0 provide developers with a declarative model for retrieving data, displaying data, and editing data.</span></span> <span data-ttu-id="4218c-116">数据源控件的用途是为数据绑定控件提供一致的数据表示形式，而不考虑这些数据的源。</span><span class="sxs-lookup"><span data-stu-id="4218c-116">The purpose of data source controls is to provide a consistent representation of data to data-bound controls regardless of the source of those data.</span></span> <span data-ttu-id="4218c-117">ASP.NET 2.0 中数据源控件的核心是 DataSourceControl 抽象类。</span><span class="sxs-lookup"><span data-stu-id="4218c-117">At the heart of the data source controls in ASP.NET 2.0 is the DataSourceControl abstract class.</span></span> <span data-ttu-id="4218c-118">DataSourceControl 类提供了 IDataSource 接口和 IListSource 接口的基实现，后者允许您将数据源控件指定为数据绑定控件的数据源（通过 new DataSourceId 属性）稍后讨论）并公开作为列表的数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-118">The DataSourceControl class provides a base implementation of the IDataSource interface and the IListSource interface, the latter of which allows you to assign the data source control as the DataSource of a data-bound control (via the new DataSourceId property discussed later) and expose the data therein as a list.</span></span> <span data-ttu-id="4218c-119">数据源控件中的每个数据列表都作为 DataSourceView 对象公开。</span><span class="sxs-lookup"><span data-stu-id="4218c-119">Each list of data from a data source control is exposed as a DataSourceView object.</span></span> <span data-ttu-id="4218c-120">对 DataSourceView 实例的访问由 IDataSource 接口提供。</span><span class="sxs-lookup"><span data-stu-id="4218c-120">Access to the DataSourceView instances is provided by the IDataSource interface.</span></span> <span data-ttu-id="4218c-121">例如，GetViewNames 方法返回一个 ICollection，该 ICollection 允许您枚举与特定数据源控件关联的 DataSourceViews，而 GetView 方法允许您按名称访问特定的 DataSourceView 实例。</span><span class="sxs-lookup"><span data-stu-id="4218c-121">For example, the GetViewNames method returns an ICollection that allows you to enumerate the DataSourceViews associated with a particular data source control, and the GetView method allows you to access a particular DataSourceView instance by name.</span></span>

<span data-ttu-id="4218c-122">数据源控件没有用户界面。</span><span class="sxs-lookup"><span data-stu-id="4218c-122">Data source controls have no user-interface.</span></span> <span data-ttu-id="4218c-123">它们是作为服务器控件实现的，因此它们可以支持声明性语法，以便它们可以访问页状态（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="4218c-123">They are implemented as server controls so that they can support declarative syntax and so that they have access to page state if desired.</span></span> <span data-ttu-id="4218c-124">数据源控件不会将任何 HTML 标记呈现给客户端。</span><span class="sxs-lookup"><span data-stu-id="4218c-124">Data source controls do not render any HTML markup to the client.</span></span>

> [!NOTE]
> <span data-ttu-id="4218c-125">正如您稍后将看到的那样，还可以使用数据源控件获取缓存权益。</span><span class="sxs-lookup"><span data-stu-id="4218c-125">As you'll see later, there are also caching benefits obtained by using data source controls.</span></span>

## <a name="storing-connection-strings"></a><span data-ttu-id="4218c-126">存储连接字符串</span><span class="sxs-lookup"><span data-stu-id="4218c-126">Storing Connection Strings</span></span>

<span data-ttu-id="4218c-127">在了解如何配置数据源控件之前，应介绍 ASP.NET 2.0 中关于连接字符串的新功能。</span><span class="sxs-lookup"><span data-stu-id="4218c-127">Before we get into looking at how to configure data source controls, we should cover a new capability in ASP.NET 2.0 concerning connection strings.</span></span> <span data-ttu-id="4218c-128">ASP.NET 2.0 在配置文件中引入了一个新的节，使你能够轻松地存储可在运行时动态读取的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-128">ASP.NET 2.0 introduces a new section in the configuration file that allows you to easily store connection strings that can be read dynamically at runtime.</span></span> <span data-ttu-id="4218c-129">&lt;connectionStrings&gt; "部分，可以轻松地存储连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-129">The &lt;connectionStrings&gt; section makes it easy to store connection strings.</span></span>

<span data-ttu-id="4218c-130">下面的代码片段将添加新的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-130">The snippet below adds a new connection string.</span></span>

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="4218c-131">与 &lt;appSettings&gt; 部分一样，&lt;connectionStrings&gt; 部分显示在配置文件中的 &lt;system.web&gt; 节之外。</span><span class="sxs-lookup"><span data-stu-id="4218c-131">Just as with the &lt;appSettings&gt; section, the &lt;connectionStrings&gt; section appears outside of the &lt;system.web&gt; section in the configuration file.</span></span>

<span data-ttu-id="4218c-132">若要使用此连接字符串，可以在设置服务器控件的 ConnectionString 属性时使用以下语法。</span><span class="sxs-lookup"><span data-stu-id="4218c-132">To use this connection string, you can use the following syntax when setting the ConnectionString attribute of a server control.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

<span data-ttu-id="4218c-133">还可以加密 &lt;connectionStrings&gt; 部分，以便不公开敏感信息。</span><span class="sxs-lookup"><span data-stu-id="4218c-133">The &lt;connectionStrings&gt; section can also be encrypted so that sensitive information is not exposed.</span></span> <span data-ttu-id="4218c-134">此功能将在后面的模块中介绍。</span><span class="sxs-lookup"><span data-stu-id="4218c-134">That ability will be covered in a later module.</span></span>

## <a name="caching-data-sources"></a><span data-ttu-id="4218c-135">缓存数据源</span><span class="sxs-lookup"><span data-stu-id="4218c-135">Caching Data Sources</span></span>

<span data-ttu-id="4218c-136">每个 DataSourceControl 都提供四个用于配置缓存的属性;EnableCaching、CacheDuration、CacheExpirationPolicy 和 CacheKeyDependency。</span><span class="sxs-lookup"><span data-stu-id="4218c-136">Each DataSourceControl provides four properties for configuring caching; EnableCaching, CacheDuration, CacheExpirationPolicy, and CacheKeyDependency.</span></span>

## <a name="enablecaching"></a><span data-ttu-id="4218c-137">EnableCaching</span><span class="sxs-lookup"><span data-stu-id="4218c-137">EnableCaching</span></span>

<span data-ttu-id="4218c-138">EnableCaching 是一个布尔属性，用于确定是否为数据源控件启用缓存。</span><span class="sxs-lookup"><span data-stu-id="4218c-138">EnableCaching is a Boolean property that determines whether or not caching is enabled for the data source control.</span></span>

## <a name="cacheduration-property"></a><span data-ttu-id="4218c-139">CacheDuration 属性</span><span class="sxs-lookup"><span data-stu-id="4218c-139">CacheDuration Property</span></span>

<span data-ttu-id="4218c-140">CacheDuration 属性设置缓存保持有效的秒数。</span><span class="sxs-lookup"><span data-stu-id="4218c-140">The CacheDuration property sets the number of seconds that the cache remains valid.</span></span> <span data-ttu-id="4218c-141">将此属性设置为**0**会使缓存保持有效，直到显式失效。</span><span class="sxs-lookup"><span data-stu-id="4218c-141">Setting this property to **0** causes the cache to remain valid until explicitly invalidated.</span></span>

## <a name="cacheexpirationpolicy-property"></a><span data-ttu-id="4218c-142">CacheExpirationPolicy 属性</span><span class="sxs-lookup"><span data-stu-id="4218c-142">CacheExpirationPolicy Property</span></span>

<span data-ttu-id="4218c-143">CacheExpirationPolicy 属性可以设置为 "**绝对**" 或 "**可调**"。</span><span class="sxs-lookup"><span data-stu-id="4218c-143">The CacheExpirationPolicy property can be set to either **Absolute** or **Sliding**.</span></span> <span data-ttu-id="4218c-144">如果将其设置为 "绝对"，则表示缓存数据所用的最长时间是 CacheDuration 属性指定的秒数。</span><span class="sxs-lookup"><span data-stu-id="4218c-144">Setting it to Absolute means that the maximum amount of time that the data will be cached is the number of seconds specified by the CacheDuration property.</span></span> <span data-ttu-id="4218c-145">通过将其设置为滑动，可在执行每个操作时重置过期时间。</span><span class="sxs-lookup"><span data-stu-id="4218c-145">By setting it to Sliding, the expiration time is reset when each operation is performed.</span></span>

## <a name="cachekeydependency-property"></a><span data-ttu-id="4218c-146">CacheKeyDependency 属性</span><span class="sxs-lookup"><span data-stu-id="4218c-146">CacheKeyDependency Property</span></span>

<span data-ttu-id="4218c-147">如果为 CacheKeyDependency 属性指定了字符串值，ASP.NET 将基于该字符串设置新的缓存依赖项。</span><span class="sxs-lookup"><span data-stu-id="4218c-147">If a string value is specified for the CacheKeyDependency property, ASP.NET will set up a new cache dependency based on that string.</span></span> <span data-ttu-id="4218c-148">这样，只需更改或删除 CacheKeyDependency，便可显式使缓存失效。</span><span class="sxs-lookup"><span data-stu-id="4218c-148">This allows you to explicitly invalidate the cache by simply changing or removing the CacheKeyDependency.</span></span>

<span data-ttu-id="4218c-149">**重要提示**：如果启用模拟，并且对数据源和/或数据内容的访问基于客户端标识，则建议通过将 EnableCaching 设置为 False 来禁用缓存。</span><span class="sxs-lookup"><span data-stu-id="4218c-149">**Important**: If impersonation is enabled and access to the data source and/or content of data are based upon client identity, it is recommended that caching be disabled by setting EnableCaching to False.</span></span> <span data-ttu-id="4218c-150">如果在此方案中启用了缓存，而用户不是最初请求数据发出请求的用户，则不会强制执行对数据源的授权。</span><span class="sxs-lookup"><span data-stu-id="4218c-150">If caching is enabled in this scenario and a user other than the user who originally requested the data issues a request, authorization to the data source is not enforced.</span></span> <span data-ttu-id="4218c-151">数据将直接从缓存进行提供。</span><span class="sxs-lookup"><span data-stu-id="4218c-151">The data will simply be served from cache.</span></span>

## <a name="the-sqldatasource-control"></a><span data-ttu-id="4218c-152">SqlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="4218c-152">The SqlDataSource Control</span></span>

<span data-ttu-id="4218c-153">SqlDataSource 控件允许开发人员访问任何支持 ADO.NET 的关系数据库中存储的数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-153">The SqlDataSource control allows a developer to access data stored in any relational database that supports ADO.NET.</span></span> <span data-ttu-id="4218c-154">它可以使用 SqlClient 提供程序访问一个 SQL Server 数据库、一个提供程序、一个 System.data.oracleclient 提供程序或一个访问 Oracle 的提供程序的访问接口。</span><span class="sxs-lookup"><span data-stu-id="4218c-154">It can use the System.Data.SqlClient provider to access a SQL Server database, the System.Data.OleDb provider, the System.Data.Odbc provider, or the System.Data.OracleClient provider to access Oracle.</span></span> <span data-ttu-id="4218c-155">因此，SqlDataSource 并不是只用于访问 SQL Server 数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-155">Therefore, the SqlDataSource is certainly not only used for accessing data in a SQL Server database.</span></span>

<span data-ttu-id="4218c-156">为了使用 SqlDataSource，只需为 ConnectionString 属性提供一个值并指定一个 SQL 命令或存储过程。</span><span class="sxs-lookup"><span data-stu-id="4218c-156">In order to use the SqlDataSource, you simply provide a value for the ConnectionString property and specify a SQL command or stored procedure.</span></span> <span data-ttu-id="4218c-157">SqlDataSource 控件负责处理基础 ADO.NET 体系结构。</span><span class="sxs-lookup"><span data-stu-id="4218c-157">The SqlDataSource control takes care of working with the underlying ADO.NET architecture.</span></span> <span data-ttu-id="4218c-158">它将打开连接，查询数据源或执行存储过程，返回数据，然后关闭连接。</span><span class="sxs-lookup"><span data-stu-id="4218c-158">It opens the connection, queries the data source or executes the stored procedure, returns the data, and then closes the connection for you.</span></span>

> [!NOTE]
> <span data-ttu-id="4218c-159">由于 DataSourceControl 类会自动为你关闭连接，因此它应减少通过泄漏数据库连接生成的客户调用的数量。</span><span class="sxs-lookup"><span data-stu-id="4218c-159">Because the DataSourceControl class automatically closes the connection for you, it should reduce the number of customer calls generated by leaking database connections.</span></span>

<span data-ttu-id="4218c-160">下面的代码片段使用存储在配置文件中的连接字符串，将 DropDownList 控件绑定到 SqlDataSource 控件，如上所示。</span><span class="sxs-lookup"><span data-stu-id="4218c-160">The code snippet below binds a DropDownList control to a SqlDataSource control using the connection string that is stored in the configuration file as shown above.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

<span data-ttu-id="4218c-161">如上图所示，SqlDataSource 的 DataSourceMode 属性指定了数据源的模式。</span><span class="sxs-lookup"><span data-stu-id="4218c-161">As illustrated above, the DataSourceMode property of the SqlDataSource specifies the mode for the data source.</span></span> <span data-ttu-id="4218c-162">在上面的示例中，DataSourceMode 设置为 DataReader。</span><span class="sxs-lookup"><span data-stu-id="4218c-162">In the example above, the DataSourceMode is set to DataReader.</span></span> <span data-ttu-id="4218c-163">在这种情况下，SqlDataSource 将使用只进和只读游标返回 IDataReader 对象。</span><span class="sxs-lookup"><span data-stu-id="4218c-163">In that case, the SqlDataSource will return an IDataReader object using a forward-only and read-only cursor.</span></span> <span data-ttu-id="4218c-164">返回的对象的指定类型由所使用的提供程序控制。</span><span class="sxs-lookup"><span data-stu-id="4218c-164">The specified type of object that is returned is controlled by the provider that is used.</span></span> <span data-ttu-id="4218c-165">在这种情况下，我使用的是 web.config 文件的 &lt;connectionStrings&gt; 部分中指定的 SqlClient 提供程序。</span><span class="sxs-lookup"><span data-stu-id="4218c-165">In this case, I'm using the System.Data.SqlClient provider as specified in the &lt;connectionStrings&gt; section of the web.config file.</span></span> <span data-ttu-id="4218c-166">因此，返回的对象将为 SqlDataReader 类型。</span><span class="sxs-lookup"><span data-stu-id="4218c-166">Therefore, the object that is returned will be of type SqlDataReader.</span></span> <span data-ttu-id="4218c-167">通过指定数据集的 DataSourceMode 值，可将数据存储在服务器上的数据集中。</span><span class="sxs-lookup"><span data-stu-id="4218c-167">By specifying a DataSourceMode value of DataSet, the data can be stored in a DataSet on the server.</span></span> <span data-ttu-id="4218c-168">此模式允许添加排序、分页等功能。如果我已将 SqlDataSource 数据绑定到 GridView 控件，我将选择数据集模式。</span><span class="sxs-lookup"><span data-stu-id="4218c-168">This mode allows you to add features such as sorting, paging, etc. If I had been data-binding the SqlDataSource to a GridView control, I would have chosen the DataSet mode.</span></span> <span data-ttu-id="4218c-169">但对于 DropDownList，DataReader 模式是正确的选择。</span><span class="sxs-lookup"><span data-stu-id="4218c-169">However, in the case of a DropDownList, the DataReader mode is the correct choice.</span></span>

> [!NOTE]
> <span data-ttu-id="4218c-170">缓存 SqlDataSource 或 AccessDataSource 时，DataSourceMode 属性必须设置为 DataSet。</span><span class="sxs-lookup"><span data-stu-id="4218c-170">When caching a SqlDataSource or an AccessDataSource, the DataSourceMode property must be set to DataSet.</span></span> <span data-ttu-id="4218c-171">如果使用 DataReader 的 DataSourceMode 启用缓存，则会出现异常。</span><span class="sxs-lookup"><span data-stu-id="4218c-171">An exception will occur if you enable caching with a DataSourceMode of DataReader.</span></span>

## <a name="sqldatasource-properties"></a><span data-ttu-id="4218c-172">SqlDataSource 属性</span><span class="sxs-lookup"><span data-stu-id="4218c-172">SqlDataSource Properties</span></span>

<span data-ttu-id="4218c-173">下面是 SqlDataSource 控件的某些属性。</span><span class="sxs-lookup"><span data-stu-id="4218c-173">The following are some of the properties of the SqlDataSource control.</span></span>

### <a name="cancelselectonnullparameter"></a><span data-ttu-id="4218c-174">CancelSelectOnNullParameter</span><span class="sxs-lookup"><span data-stu-id="4218c-174">CancelSelectOnNullParameter</span></span>

<span data-ttu-id="4218c-175">一个布尔值，指定在其中一个参数为 null 时是否取消 select 命令。</span><span class="sxs-lookup"><span data-stu-id="4218c-175">A Boolean value that specifies whether a select command is canceled if one of the parameters is null.</span></span> <span data-ttu-id="4218c-176">默认值为 True。</span><span class="sxs-lookup"><span data-stu-id="4218c-176">True by default.</span></span>

### <a name="conflictdetection"></a><span data-ttu-id="4218c-177">ConflictDetection</span><span class="sxs-lookup"><span data-stu-id="4218c-177">ConflictDetection</span></span>

<span data-ttu-id="4218c-178">在多个用户可能同时更新数据源的情况下，ConflictDetection 属性决定了 SqlDataSource 控件的行为。</span><span class="sxs-lookup"><span data-stu-id="4218c-178">In a situation where multiple users may be updating a data source at the same time, the ConflictDetection property determines the behavior of the SqlDataSource control.</span></span> <span data-ttu-id="4218c-179">此属性的计算结果为 ConflictOptions 枚举的值之一。</span><span class="sxs-lookup"><span data-stu-id="4218c-179">This property evaluates to one of the values of the ConflictOptions enumeration.</span></span> <span data-ttu-id="4218c-180">这些值为**CompareAllValues**和**OverwriteChanges**。</span><span class="sxs-lookup"><span data-stu-id="4218c-180">Those values are **CompareAllValues** and **OverwriteChanges**.</span></span> <span data-ttu-id="4218c-181">如果设置为 OverwriteChanges，则最后一次将数据写入数据源的用户会覆盖以前的所有更改。</span><span class="sxs-lookup"><span data-stu-id="4218c-181">If set to OverwriteChanges, the last person to write data to the data source overwrites any previous changes.</span></span> <span data-ttu-id="4218c-182">但是，如果将 ConflictDetection 属性设置为 CompareAllValues，则会为 SelectCommand 返回的列创建参数，同时还会创建参数来保存每个列中的原始值，从而使 SqlDataSource 成为确定在执行 SelectCommand 后值是否已更改。</span><span class="sxs-lookup"><span data-stu-id="4218c-182">However, if the ConflictDetection property is set to CompareAllValues, parameters get created for the columns returned by the SelectCommand and parameters are also created to hold the original values in each of those columns allowing the SqlDataSource to determine whether or not the values have changed since the SelectCommand was executed.</span></span>

### <a name="deletecommand"></a><span data-ttu-id="4218c-183">DeleteCommand</span><span class="sxs-lookup"><span data-stu-id="4218c-183">DeleteCommand</span></span>

<span data-ttu-id="4218c-184">设置或获取从数据库中删除行时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-184">Sets or gets the SQL string used when deleting rows from the database.</span></span> <span data-ttu-id="4218c-185">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-185">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="deletecommandtype"></a><span data-ttu-id="4218c-186">DeleteCommandType</span><span class="sxs-lookup"><span data-stu-id="4218c-186">DeleteCommandType</span></span>

<span data-ttu-id="4218c-187">设置或获取删除命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。</span><span class="sxs-lookup"><span data-stu-id="4218c-187">Sets or gets the type of delete command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="deleteparameters"></a><span data-ttu-id="4218c-188">DeleteParameters</span><span class="sxs-lookup"><span data-stu-id="4218c-188">DeleteParameters</span></span>

<span data-ttu-id="4218c-189">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 DeleteCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="4218c-189">Returns the parameters that are used by the DeleteCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="oldvaluesparameterformatstring"></a><span data-ttu-id="4218c-190">OldValuesParameterFormatString</span><span class="sxs-lookup"><span data-stu-id="4218c-190">OldValuesParameterFormatString</span></span>

<span data-ttu-id="4218c-191">当 ConflictDetection 属性设置为 CompareAllValues 时，此属性用于指定原始值参数的格式。</span><span class="sxs-lookup"><span data-stu-id="4218c-191">This property is used to specify the format of the original value parameters in cases where the ConflictDetection property is set to CompareAllValues.</span></span> <span data-ttu-id="4218c-192">默认值为 {0} 这意味着原始值参数将采用与原始参数相同的名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-192">The default is {0} which means that original value parameters will take the same name as the original parameter.</span></span> <span data-ttu-id="4218c-193">换言之，如果字段名称为 "雇员 Id"，则原始值参数将 @EmployeeID。</span><span class="sxs-lookup"><span data-stu-id="4218c-193">In other words, if the field name is EmployeeID, the original value parameter would be @EmployeeID.</span></span>

### <a name="selectcommand"></a><span data-ttu-id="4218c-194">SelectCommand</span><span class="sxs-lookup"><span data-stu-id="4218c-194">SelectCommand</span></span>

<span data-ttu-id="4218c-195">设置或获取用于从数据库检索数据的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-195">Sets or gets the SQL string that is used to retrieve data from the database.</span></span> <span data-ttu-id="4218c-196">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-196">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="selectcommandtype"></a><span data-ttu-id="4218c-197">SelectCommandType</span><span class="sxs-lookup"><span data-stu-id="4218c-197">SelectCommandType</span></span>

<span data-ttu-id="4218c-198">设置或获取 select 命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。</span><span class="sxs-lookup"><span data-stu-id="4218c-198">Sets or gets the type of select command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="selectparameters"></a><span data-ttu-id="4218c-199">SelectParameters</span><span class="sxs-lookup"><span data-stu-id="4218c-199">SelectParameters</span></span>

<span data-ttu-id="4218c-200">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 SelectCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="4218c-200">Returns the parameters that are used by the SelectCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

### <a name="sortparametername"></a><span data-ttu-id="4218c-201">SortParameterName</span><span class="sxs-lookup"><span data-stu-id="4218c-201">SortParameterName</span></span>

<span data-ttu-id="4218c-202">获取或设置在对数据源控件检索到的数据进行排序时使用的存储过程参数的名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-202">Gets or sets the name of a stored procedure parameter that is used when sorting data retrieved by the data source control.</span></span> <span data-ttu-id="4218c-203">仅当 SelectCommandType 设置为 StoredProcedure 时才有效。</span><span class="sxs-lookup"><span data-stu-id="4218c-203">Valid only when SelectCommandType is set to StoredProcedure.</span></span>

### <a name="sqlcachedependency"></a><span data-ttu-id="4218c-204">SqlCacheDependency</span><span class="sxs-lookup"><span data-stu-id="4218c-204">SqlCacheDependency</span></span>

<span data-ttu-id="4218c-205">用分号分隔的字符串，用于指定 SQL Server 缓存依赖项中使用的数据库和表。</span><span class="sxs-lookup"><span data-stu-id="4218c-205">A semi-colon delimited string specifying the databases and tables used in a SQL Server cache dependency.</span></span> <span data-ttu-id="4218c-206">（SQL 缓存依赖关系将在后面的模块中讨论。）</span><span class="sxs-lookup"><span data-stu-id="4218c-206">(SQL cache dependencies will be discussed in a later module.)</span></span>

### <a name="updatecommand"></a><span data-ttu-id="4218c-207">UpdateCommand</span><span class="sxs-lookup"><span data-stu-id="4218c-207">UpdateCommand</span></span>

<span data-ttu-id="4218c-208">设置或获取更新数据库中的数据时使用的 SQL 字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-208">Sets or gets the SQL string that is used when updating data in the database.</span></span> <span data-ttu-id="4218c-209">这可以是 SQL 查询或存储过程名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-209">This can either be a SQL query or a stored procedure name.</span></span>

### <a name="updatecommandtype"></a><span data-ttu-id="4218c-210">UpdateCommandType</span><span class="sxs-lookup"><span data-stu-id="4218c-210">UpdateCommandType</span></span>

<span data-ttu-id="4218c-211">设置或获取更新命令的类型（SQL 查询（Text）或存储过程（StoredProcedure））。</span><span class="sxs-lookup"><span data-stu-id="4218c-211">Sets or gets the type of update command, either a SQL query (Text) or a stored procedure (StoredProcedure).</span></span>

### <a name="updateparameters"></a><span data-ttu-id="4218c-212">UpdateParameters</span><span class="sxs-lookup"><span data-stu-id="4218c-212">UpdateParameters</span></span>

<span data-ttu-id="4218c-213">返回与 SqlDataSource 控件关联的 SqlDataSourceView 对象的 UpdateCommand 使用的参数。</span><span class="sxs-lookup"><span data-stu-id="4218c-213">Returns the parameters that are used by the UpdateCommand of the SqlDataSourceView object associated with the SqlDataSource control.</span></span>

## <a name="the-accessdatasource-control"></a><span data-ttu-id="4218c-214">AccessDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="4218c-214">The AccessDataSource Control</span></span>

<span data-ttu-id="4218c-215">AccessDataSource 控件派生自 SqlDataSource 类，用于将数据绑定到 Microsoft Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="4218c-215">The AccessDataSource control derives from the SqlDataSource class and is used to data-bind to a Microsoft Access database.</span></span> <span data-ttu-id="4218c-216">AccessDataSource 控件的 ConnectionString 属性为只读属性。</span><span class="sxs-lookup"><span data-stu-id="4218c-216">The ConnectionString property for the AccessDataSource control is a read-only property.</span></span> <span data-ttu-id="4218c-217">"数据文件" 属性不使用 ConnectionString 属性，而是指向 Access 数据库，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4218c-217">Instead of using the ConnectionString property, the DataFile property is used to point to the Access Database as shown below.</span></span>

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

<span data-ttu-id="4218c-218">AccessDataSource 将始终将基 SqlDataSource 的 ProviderName 设置为，并使用 OLE DB 提供程序连接到数据库中。</span><span class="sxs-lookup"><span data-stu-id="4218c-218">The AccessDataSource will always set the ProviderName of the base SqlDataSource to System.Data.OleDb and connects to the database using the Microsoft.Jet.OLEDB.4.0 OLE DB provider.</span></span> <span data-ttu-id="4218c-219">不能使用 AccessDataSource 控件连接到受密码保护的访问数据库。</span><span class="sxs-lookup"><span data-stu-id="4218c-219">You cannot use the AccessDataSource control to connect to a password-protected Access database.</span></span> <span data-ttu-id="4218c-220">如果必须连接到受密码保护的数据库，则应使用 SqlDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-220">If you have to connect to a password protected database, you should use the SqlDataSource control.</span></span>

> [!NOTE]
> <span data-ttu-id="4218c-221">应将存储在网站中的数据库放置在应用\_数据目录中。</span><span class="sxs-lookup"><span data-stu-id="4218c-221">Access databases stored within the Web site should be placed in the App\_Data directory.</span></span> <span data-ttu-id="4218c-222">ASP.NET 不允许浏览该目录中的文件。</span><span class="sxs-lookup"><span data-stu-id="4218c-222">ASP.NET does not allow files in this directory to be browsed.</span></span> <span data-ttu-id="4218c-223">使用 Access 数据库时，需要将应用程序的 "读取" 和 "写入" 权限授予\_Data directory。</span><span class="sxs-lookup"><span data-stu-id="4218c-223">You will need to grant the process account Read and Write permissions to the App\_Data directory when using Access databases.</span></span>

## <a name="the-xmldatasource-control"></a><span data-ttu-id="4218c-224">XmlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="4218c-224">The XmlDataSource Control</span></span>

<span data-ttu-id="4218c-225">XmlDataSource 用于将 XML 数据绑定到数据绑定控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-225">The XmlDataSource is used to data-bind XML data to data-bound controls.</span></span> <span data-ttu-id="4218c-226">您可以使用数据文件属性绑定到 XML 文件，也可以使用数据属性绑定到 XML 字符串。</span><span class="sxs-lookup"><span data-stu-id="4218c-226">You can bind to an XML file using the DataFile property or you can bind to an XML string using the Data property.</span></span> <span data-ttu-id="4218c-227">XmlDataSource 将 XML 特性公开为可绑定的字段。</span><span class="sxs-lookup"><span data-stu-id="4218c-227">The XmlDataSource exposes XML attributes as bindable fields.</span></span> <span data-ttu-id="4218c-228">如果需要绑定到不表示为属性的值，则需要使用 XSL 转换。</span><span class="sxs-lookup"><span data-stu-id="4218c-228">In cases where you need to bind to values that are not represented as attributes, you will need to use an XSL transform.</span></span> <span data-ttu-id="4218c-229">还可以使用 XPath 表达式来筛选 XML 数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-229">You can also use XPath expressions to filter XML data.</span></span>

<span data-ttu-id="4218c-230">请看下面的 XML 文件：</span><span class="sxs-lookup"><span data-stu-id="4218c-230">Consider the following XML file:</span></span>

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

<span data-ttu-id="4218c-231">请注意，XmlDataSource 使用*人员/人员*的 XPath 属性来仅筛选 &lt;人员&gt; 节点。</span><span class="sxs-lookup"><span data-stu-id="4218c-231">Notice that the XmlDataSource uses an XPath property of *People/Person* in order to filter on just the &lt;Person&gt; nodes.</span></span> <span data-ttu-id="4218c-232">然后，DropDownList 使用 DataTextField 属性，将数据绑定到 LastName 特性。</span><span class="sxs-lookup"><span data-stu-id="4218c-232">The DropDownList then data-binds to the LastName attribute using the DataTextField property.</span></span>

<span data-ttu-id="4218c-233">尽管 XmlDataSource 控件主要用于数据绑定到只读 XML 数据，但可以编辑 XML 数据文件。</span><span class="sxs-lookup"><span data-stu-id="4218c-233">While the XmlDataSource control is primarily used to data-bind to read-only XML data, it is possible to edit the XML data file.</span></span> <span data-ttu-id="4218c-234">请注意，在这种情况下，XML 文件中的信息的自动插入、更新和删除操作不会自动发生，与其他数据源控件的操作一样。</span><span class="sxs-lookup"><span data-stu-id="4218c-234">Note that in such cases, automatic insertion, updating, and deletion of information in the XML file does not happen automatically as it does with other data source controls.</span></span> <span data-ttu-id="4218c-235">相反，您必须编写代码以使用 XmlDataSource 控件的以下方法手动编辑数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-235">Instead, you will have to write code to manually edit the data using the following methods of the XmlDataSource control.</span></span>

### <a name="getxmldocument"></a><span data-ttu-id="4218c-236">GetXmlDocument</span><span class="sxs-lookup"><span data-stu-id="4218c-236">GetXmlDocument</span></span>

<span data-ttu-id="4218c-237">检索包含由 XmlDataSource 检索到的 XML 代码的 XML。</span><span class="sxs-lookup"><span data-stu-id="4218c-237">Retrieves an XmlDocument object containing the XML code retrieved by the XmlDataSource.</span></span>

### <a name="save"></a><span data-ttu-id="4218c-238">保存</span><span class="sxs-lookup"><span data-stu-id="4218c-238">Save</span></span>

<span data-ttu-id="4218c-239">将内存中的 Xml 存储回数据源。</span><span class="sxs-lookup"><span data-stu-id="4218c-239">Saves the in-memory XmlDocument back to the data source.</span></span>

<span data-ttu-id="4218c-240">请注意，Save 方法仅在满足以下两个条件时才起作用：</span><span class="sxs-lookup"><span data-stu-id="4218c-240">It's important to realize that the Save method will only work when the following two conditions are met:</span></span>

1. <span data-ttu-id="4218c-241">XmlDataSource 使用数据文件属性来绑定到 XML 文件，而不是绑定到内存中 XML 数据的数据属性。</span><span class="sxs-lookup"><span data-stu-id="4218c-241">The XmlDataSource is using the DataFile property to bind to an XML file instead of the Data property to bind to in-memory XML data.</span></span>
2. <span data-ttu-id="4218c-242">不通过 Transform 或 TransformFile 属性指定转换。</span><span class="sxs-lookup"><span data-stu-id="4218c-242">No transformation is specified via the Transform or TransformFile property.</span></span>

<span data-ttu-id="4218c-243">另请注意，当多个用户同时调用时，Save 方法可能产生意外结果。</span><span class="sxs-lookup"><span data-stu-id="4218c-243">Note also that the Save method can yield unexpected results when called by multiple users concurrently.</span></span>

## <a name="the-objectdatasource-control"></a><span data-ttu-id="4218c-244">ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="4218c-244">The ObjectDataSource Control</span></span>

<span data-ttu-id="4218c-245">我们已涵盖到目前为止的数据源控件是两层应用程序的最佳选择，其中的数据源控件直接与数据存储进行通信。</span><span class="sxs-lookup"><span data-stu-id="4218c-245">The data source controls that we have covered up to this point are excellent choices for two-tier applications where the data source control communicates directly to the data store.</span></span> <span data-ttu-id="4218c-246">但是，许多实际应用程序是多层应用程序，其中的数据源控件可能需要与业务对象通信，而该对象又会与数据层通信。</span><span class="sxs-lookup"><span data-stu-id="4218c-246">However, many real-world applications are multi-tier applications where a data source control might need to communicate to a business object which, in turn, communicates with the data layer.</span></span> <span data-ttu-id="4218c-247">在这些情况下，ObjectDataSource 会很好地填充帐单。</span><span class="sxs-lookup"><span data-stu-id="4218c-247">In these situations, the ObjectDataSource fills the bill nicely.</span></span> <span data-ttu-id="4218c-248">ObjectDataSource 与源对象一起工作。</span><span class="sxs-lookup"><span data-stu-id="4218c-248">The ObjectDataSource works in conjunction with a source object.</span></span> <span data-ttu-id="4218c-249">如果对象具有实例方法而不是静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将创建源对象的实例，调用指定的方法，并在单个请求的范围内释放对象实例。</span><span class="sxs-lookup"><span data-stu-id="4218c-249">The ObjectDataSource control will create an instance of the source object, call the specified method, and dispose of the object instance all within the scope of a single request, if your object has instance methods instead of static methods (Shared in Visual Basic).</span></span> <span data-ttu-id="4218c-250">因此，您的对象必须是无状态的。</span><span class="sxs-lookup"><span data-stu-id="4218c-250">Therefore, your object must be stateless.</span></span> <span data-ttu-id="4218c-251">也就是说，你的对象应获取并释放单个请求范围内的所有所需资源。</span><span class="sxs-lookup"><span data-stu-id="4218c-251">That is, your object should acquire and release all required resources within the span of a single request.</span></span> <span data-ttu-id="4218c-252">可以通过处理 ObjectDataSource 控件的 ObjectCreating 事件来控制如何创建源对象。</span><span class="sxs-lookup"><span data-stu-id="4218c-252">You can control how the source object is created by handling the ObjectCreating event of the ObjectDataSource control.</span></span> <span data-ttu-id="4218c-253">您可以创建源对象的实例，然后将 ObjectDataSourceEventArgs 类的 ObjectInstance 属性设置为该实例。</span><span class="sxs-lookup"><span data-stu-id="4218c-253">You can create an instance of the source object, and then set the ObjectInstance property of the ObjectDataSourceEventArgs class to that instance.</span></span> <span data-ttu-id="4218c-254">ObjectDataSource 控件将使用在 ObjectCreating 事件中创建的实例，而不是自己创建实例。</span><span class="sxs-lookup"><span data-stu-id="4218c-254">The ObjectDataSource control will use the instance that is created in the ObjectCreating event instead of creating an instance on its own.</span></span>

<span data-ttu-id="4218c-255">如果 ObjectDataSource 控件的源对象公开可调用以检索和修改数据的公共静态方法（在 Visual Basic 中共享），则 ObjectDataSource 控件将直接调用这些方法。</span><span class="sxs-lookup"><span data-stu-id="4218c-255">If the source object for an ObjectDataSource control exposes public static methods (Shared in Visual Basic) that can be called to retrieve and modify data, an ObjectDataSource control will call those methods directly.</span></span> <span data-ttu-id="4218c-256">如果 ObjectDataSource 控件必须创建源对象的实例才能进行方法调用，则该对象必须包含不带任何参数的公共构造函数。</span><span class="sxs-lookup"><span data-stu-id="4218c-256">If an ObjectDataSource control must create an instance of the source object in order to make method calls, the object must include a public constructor that takes no parameters.</span></span> <span data-ttu-id="4218c-257">当 ObjectDataSource 控件创建源对象的新实例时，将调用此构造函数。</span><span class="sxs-lookup"><span data-stu-id="4218c-257">The ObjectDataSource control will call this constructor when it creates a new instance of the source object.</span></span>

<span data-ttu-id="4218c-258">如果源对象不包含没有参数的公共构造函数，则可以创建将由 ObjectCreating 事件中的 ObjectDataSource 控件使用的源对象的实例。</span><span class="sxs-lookup"><span data-stu-id="4218c-258">If the source object does not contain a public constructor without parameters, you can create an instance of the source object that will be used by the ObjectDataSource control in the ObjectCreating event.</span></span>

## <a name="specifying-object-methods"></a><span data-ttu-id="4218c-259">指定对象方法</span><span class="sxs-lookup"><span data-stu-id="4218c-259">Specifying Object Methods</span></span>

<span data-ttu-id="4218c-260">ObjectDataSource 控件的源对象可以包含任意数量的用于选择、插入、更新或删除数据的方法。</span><span class="sxs-lookup"><span data-stu-id="4218c-260">The source object for an ObjectDataSource control can contain any number of methods that are used to select, insert, update, or delete data.</span></span> <span data-ttu-id="4218c-261">根据方法的名称，ObjectDataSource 控件调用这些方法，如使用 ObjectDataSource 控件的 SelectMethod、InsertMethod、UpdateMethod 或 DeleteMethod 属性标识。</span><span class="sxs-lookup"><span data-stu-id="4218c-261">These methods are called by the ObjectDataSource control based on the name of the method, as identified by using either the SelectMethod, InsertMethod, UpdateMethod, or DeleteMethod property of the ObjectDataSource control.</span></span> <span data-ttu-id="4218c-262">源对象还可以包含可选的 SelectCount 方法，该方法由 ObjectDataSource 控件使用 SelectCountMethod 属性标识，该方法返回数据源中对象的总数的计数。</span><span class="sxs-lookup"><span data-stu-id="4218c-262">The source object can also include an optional SelectCount method, which is identified by the ObjectDataSource control using the SelectCountMethod property, that returns the count of the total number of objects at the data source.</span></span> <span data-ttu-id="4218c-263">在调用 Select 方法以检索数据源中用于分页的记录总数后，ObjectDataSource 控件将调用 SelectCount 方法。</span><span class="sxs-lookup"><span data-stu-id="4218c-263">The ObjectDataSource control will call the SelectCount method after a Select method has been called to retrieve the total number of records at the data source for use when paging.</span></span>

## <a name="lab-using-data-source-controls"></a><span data-ttu-id="4218c-264">使用数据源控件的实验室</span><span class="sxs-lookup"><span data-stu-id="4218c-264">Lab Using Data Source Controls</span></span>

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a><span data-ttu-id="4218c-265">练习 1-通过 SqlDataSource 控件显示数据</span><span class="sxs-lookup"><span data-stu-id="4218c-265">Exercise 1 - Displaying Data with the SqlDataSource Control</span></span>

<span data-ttu-id="4218c-266">以下练习使用 SqlDataSource 控件连接到 Northwind 数据库。</span><span class="sxs-lookup"><span data-stu-id="4218c-266">The following exercise uses the SqlDataSource control to connect to the Northwind database.</span></span> <span data-ttu-id="4218c-267">它假定您有权访问 SQL Server 2000 实例上的 Northwind 数据库。</span><span class="sxs-lookup"><span data-stu-id="4218c-267">It assumes that you have access to the Northwind database on a SQL Server 2000 instance.</span></span>

1. <span data-ttu-id="4218c-268">创建一个新的 ASP.NET 网站。</span><span class="sxs-lookup"><span data-stu-id="4218c-268">Create a new ASP.NET Web site.</span></span>
2. <span data-ttu-id="4218c-269">添加新的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="4218c-269">Add a new web.config file.</span></span>

    1. <span data-ttu-id="4218c-270">在解决方案资源管理器中右键单击该项目，然后单击 "添加新项"。</span><span class="sxs-lookup"><span data-stu-id="4218c-270">Right-click on the project in Solution Explorer and click Add New Item.</span></span>
    2. <span data-ttu-id="4218c-271">从模板列表中选择 "Web 配置文件"，然后单击 "添加"。</span><span class="sxs-lookup"><span data-stu-id="4218c-271">Choose Web Configuration File from the list of templates and click Add.</span></span>
3. <span data-ttu-id="4218c-272">编辑 &lt;connectionStrings&gt; "部分，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4218c-272">Edit the &lt;connectionStrings&gt; section as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. <span data-ttu-id="4218c-273">切换到代码视图，并将 ConnectionString 属性和 SelectCommand 属性添加到 &lt;asp： SqlDataSource&gt; 控件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4218c-273">Switch to Code view and add a ConnectionString attribute and a SelectCommand attribute to the &lt;asp:SqlDataSource&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. <span data-ttu-id="4218c-274">在设计视图中，添加一个新的 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-274">From Design view, add a new GridView control.</span></span>
6. <span data-ttu-id="4218c-275">从 "GridView 任务" 菜单中的 "选择数据源" 下拉列表中，选择 "SqlDataSource1"。</span><span class="sxs-lookup"><span data-stu-id="4218c-275">From the Choose Data Source dropdown in the GridView Tasks menu, choose SqlDataSource1.</span></span>
7. <span data-ttu-id="4218c-276">右键单击 "default.aspx"，然后从菜单中选择 "在浏览器中查看"。</span><span class="sxs-lookup"><span data-stu-id="4218c-276">Right-click on Default.aspx and choose View in Browser from the menu.</span></span> <span data-ttu-id="4218c-277">系统提示保存时单击 "是"。</span><span class="sxs-lookup"><span data-stu-id="4218c-277">Click Yes when prompted to save.</span></span>
8. <span data-ttu-id="4218c-278">GridView 显示 Products 表中的数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-278">The GridView displays the data from the Products table.</span></span>

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a><span data-ttu-id="4218c-279">练习 2-用 SqlDataSource 控件编辑数据</span><span class="sxs-lookup"><span data-stu-id="4218c-279">Exercise 2 - Editing Data with the SqlDataSource Control</span></span>

<span data-ttu-id="4218c-280">以下练习演示了如何使用声明性语法对 DropDownList 控件进行数据绑定，并允许编辑 DropDownList 控件中显示的数据。</span><span class="sxs-lookup"><span data-stu-id="4218c-280">The following exercise demonstrates how to data bind a DropDownList control using the declarative syntax and allows you to edit the data presented in the DropDownList control.</span></span>

1. <span data-ttu-id="4218c-281">在设计视图中，从 default.aspx 删除 GridView 控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-281">In Design view, delete the GridView control from Default.aspx.</span></span> 

    <span data-ttu-id="4218c-282">**重要说明**：将 SqlDataSource 控件保留在页面上。</span><span class="sxs-lookup"><span data-stu-id="4218c-282">**Important**: Leave the SqlDataSource control on the page.</span></span>
2. <span data-ttu-id="4218c-283">将 DropDownList 控件添加到 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="4218c-283">Add a DropDownList control to Default.aspx.</span></span>
3. <span data-ttu-id="4218c-284">切换到 "源" 视图。</span><span class="sxs-lookup"><span data-stu-id="4218c-284">Switch to Source view.</span></span>
4. <span data-ttu-id="4218c-285">向 &lt;asp： DropDownList&gt; 控件添加 DataSourceId、DataTextField 和 DataValueField 属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4218c-285">Add a DataSourceId, DataTextField, and DataValueField attribute to the &lt;asp:DropDownList&gt; control as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. <span data-ttu-id="4218c-286">保存 default.aspx 并在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="4218c-286">Save Default.aspx and view it in the browser.</span></span> <span data-ttu-id="4218c-287">请注意，DropDownList 包含 Northwind 数据库中的所有产品。</span><span class="sxs-lookup"><span data-stu-id="4218c-287">Note that the DropDownList contains all of the products from the Northwind database.</span></span>
6. <span data-ttu-id="4218c-288">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="4218c-288">Close the browser.</span></span>
7. <span data-ttu-id="4218c-289">在 default.aspx 的 "源" 视图中，在 DropDownList 控件下方添加一个新的 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-289">In Source view of Default.aspx, add a new TextBox control below the DropDownList control.</span></span> <span data-ttu-id="4218c-290">将文本框的 "ID" 属性更改为 "txtProductName"。</span><span class="sxs-lookup"><span data-stu-id="4218c-290">Change the ID property of the TextBox to txtProductName.</span></span>
8. <span data-ttu-id="4218c-291">在 TextBox 控件下，添加一个新的按钮控件。</span><span class="sxs-lookup"><span data-stu-id="4218c-291">Under the TextBox control, add a new Button control.</span></span> <span data-ttu-id="4218c-292">将按钮的 ID 属性更改为 btnUpdate，并将 Text 属性更改为 "**更新产品名称**"。</span><span class="sxs-lookup"><span data-stu-id="4218c-292">Change the ID property of the Button to btnUpdate and the Text property to **Update Product Name**.</span></span>
9. <span data-ttu-id="4218c-293">在 default.aspx 的 "源" 视图中，将 UpdateCommand 属性和两个新 UpdateParameters 添加到 SqlDataSource 标记，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4218c-293">In Source view of Default.aspx, add an UpdateCommand property and two new UpdateParameters to the SqlDataSource tag as follows:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > <span data-ttu-id="4218c-294">请注意，在此代码中添加了两个更新参数（ProductName 和 ProductID）。</span><span class="sxs-lookup"><span data-stu-id="4218c-294">Note that there are two update parameters (ProductName and ProductID) added in this code.</span></span> <span data-ttu-id="4218c-295">这些参数将映射到 txtProductName 文本框的 Text 属性和 ddlProducts DropDownList 的 SelectedValue 属性。</span><span class="sxs-lookup"><span data-stu-id="4218c-295">These parameters are mapped to the Text property of the txtProductName TextBox and the SelectedValue property of the ddlProducts DropDownList.</span></span>
10. <span data-ttu-id="4218c-296">切换到设计视图，然后双击按钮控件添加事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="4218c-296">Switch to Design view and double-click on the Button control to add an event handler.</span></span>
11. <span data-ttu-id="4218c-297">将以下代码添加到 btnUpdate\_单击 "代码"：</span><span class="sxs-lookup"><span data-stu-id="4218c-297">Add the following code to the btnUpdate\_Click code:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. <span data-ttu-id="4218c-298">右键单击 "default.aspx"，然后选择在浏览器中查看它。</span><span class="sxs-lookup"><span data-stu-id="4218c-298">Right-click on Default.aspx and choose to view it in the browser.</span></span> <span data-ttu-id="4218c-299">出现提示时单击 "是" 以保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="4218c-299">Click Yes when prompted to save all changes.</span></span>
13. <span data-ttu-id="4218c-300">ASP.NET 2.0 分部类允许在运行时进行编译。</span><span class="sxs-lookup"><span data-stu-id="4218c-300">ASP.NET 2.0 partial classes allow for compilation at runtime.</span></span> <span data-ttu-id="4218c-301">为了查看代码更改生效，无需生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="4218c-301">It is not necessary to build an application in order to see code changes take effect.</span></span>
14. <span data-ttu-id="4218c-302">从 DropDownList 中选择一个产品。</span><span class="sxs-lookup"><span data-stu-id="4218c-302">Select a product from the DropDownList.</span></span>
15. <span data-ttu-id="4218c-303">在文本框中为所选产品输入新名称，然后单击 "更新" 按钮。</span><span class="sxs-lookup"><span data-stu-id="4218c-303">Enter a new name for the selected product in the TextBox and then click the Update button.</span></span>
16. <span data-ttu-id="4218c-304">在数据库中更新产品名称。</span><span class="sxs-lookup"><span data-stu-id="4218c-304">The product name is updated in the database.</span></span>

## <a name="exercise-3-using-the-objectdatasource-control"></a><span data-ttu-id="4218c-305">练习3使用 ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="4218c-305">Exercise 3 Using the ObjectDataSource Control</span></span>

<span data-ttu-id="4218c-306">本练习将演示如何使用 ObjectDataSource 控件和源对象与 Northwind 数据库进行交互。</span><span class="sxs-lookup"><span data-stu-id="4218c-306">This exercise will demonstrate how to use the ObjectDataSource control and a source object to interact with the Northwind database.</span></span>

1. <span data-ttu-id="4218c-307">右键单击 "解决方案资源管理器中的项目，然后单击" 添加新项 "。</span><span class="sxs-lookup"><span data-stu-id="4218c-307">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
2. <span data-ttu-id="4218c-308">在 "模板" 列表中选择 "Web 窗体"。</span><span class="sxs-lookup"><span data-stu-id="4218c-308">Select Web Form in the templates list.</span></span> <span data-ttu-id="4218c-309">将名称更改为 default.aspx，然后单击 "添加"。</span><span class="sxs-lookup"><span data-stu-id="4218c-309">Change the name to object.aspx and click Add.</span></span>
3. <span data-ttu-id="4218c-310">右键单击 "解决方案资源管理器中的项目，然后单击" 添加新项 "。</span><span class="sxs-lookup"><span data-stu-id="4218c-310">Right-click on the project in Solution Explorer and click on Add New Item.</span></span>
4. <span data-ttu-id="4218c-311">在 "模板" 列表中选择 "类"。</span><span class="sxs-lookup"><span data-stu-id="4218c-311">Select Class in the templates list.</span></span> <span data-ttu-id="4218c-312">将类的名称更改为 NorthwindData.cs，然后单击 "添加"。</span><span class="sxs-lookup"><span data-stu-id="4218c-312">Change the name of the class to NorthwindData.cs and click Add.</span></span>
5. <span data-ttu-id="4218c-313">系统提示将类添加到应用\_代码文件夹时，单击 "是"。</span><span class="sxs-lookup"><span data-stu-id="4218c-313">Click Yes when prompted to add the class to the App\_Code folder.</span></span>
6. <span data-ttu-id="4218c-314">将以下代码添加到 NorthwindData.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="4218c-314">Add the following code to the NorthwindData.cs file:</span></span> 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. <span data-ttu-id="4218c-315">将以下代码添加到对象的源视图：</span><span class="sxs-lookup"><span data-stu-id="4218c-315">Add the following code to the Source view of object.aspx:</span></span> 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. <span data-ttu-id="4218c-316">保存所有文件并浏览对象 .aspx。</span><span class="sxs-lookup"><span data-stu-id="4218c-316">Save all files and browse object.aspx.</span></span>
9. <span data-ttu-id="4218c-317">通过查看详细信息、编辑员工、添加员工和删除员工，与界面进行交互。</span><span class="sxs-lookup"><span data-stu-id="4218c-317">Interact with the interface by viewing details, editing employees, adding employees, and deleting employees.</span></span>
