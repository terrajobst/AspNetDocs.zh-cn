---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 通过多种方式增强服务器控件。 在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 200 的方式的一些体系结构更改 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521090"
---
# <a name="server-controls"></a><span data-ttu-id="201a3-104">服务器控件</span><span class="sxs-lookup"><span data-stu-id="201a3-104">Server Controls</span></span>

<span data-ttu-id="201a3-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="201a3-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="201a3-106">ASP.NET 2.0 通过多种方式增强服务器控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="201a3-107">在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="201a3-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

<span data-ttu-id="201a3-108">ASP.NET 2.0 通过多种方式增强服务器控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="201a3-109">在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="201a3-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="201a3-110">视图状态</span><span class="sxs-lookup"><span data-stu-id="201a3-110">View state</span></span>

<span data-ttu-id="201a3-111">ASP.NET 2.0 中视图状态的主要变化是大小大幅降低。</span><span class="sxs-lookup"><span data-stu-id="201a3-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="201a3-112">假设只有一个日历控件的页面。</span><span class="sxs-lookup"><span data-stu-id="201a3-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="201a3-113">下面是 ASP.NET 1.1 中的视图状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="201a3-114">下面是 ASP.NET 2.0 中相同页面上的视图状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="201a3-115">这是一种非常重要的变化，考虑到视图状态是在网络上来回进行的，此更改可使开发人员大大提高性能。</span><span class="sxs-lookup"><span data-stu-id="201a3-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="201a3-116">视图状态的减小很大程度上取决于我们在内部处理它的方式。</span><span class="sxs-lookup"><span data-stu-id="201a3-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="201a3-117">请记住，视图状态为 Base64 编码的字符串。</span><span class="sxs-lookup"><span data-stu-id="201a3-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="201a3-118">为了更好地了解 ASP.NET 2.0 中视图状态的变化，我们来看看上述示例中的解码值。</span><span class="sxs-lookup"><span data-stu-id="201a3-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="201a3-119">下面是1.1 视图状态解码：</span><span class="sxs-lookup"><span data-stu-id="201a3-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="201a3-120">这看起来可能有点像杂乱，但这里有一种模式。</span><span class="sxs-lookup"><span data-stu-id="201a3-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="201a3-121">在 ASP.NET 1.x 中，我们使用了单个字符来识别数据类型，使用 &lt;&gt; 字符来识别分隔值。</span><span class="sxs-lookup"><span data-stu-id="201a3-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="201a3-122">上面视图状态示例中的 "t" 表示三态。</span><span class="sxs-lookup"><span data-stu-id="201a3-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="201a3-123">三元包含一对 Arraylist （"l" 表示 ArrayList。）其中一个 Arraylist 包含值为1的 Int32 （"i"），而另一个包含其他三元。</span><span class="sxs-lookup"><span data-stu-id="201a3-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="201a3-124">三元包含一对 Arraylist 等。需要记住的重要一点是，我们使用包含对的 Triplets，通过字母标识数据类型，并使用 &lt; 和 &gt; 字符作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="201a3-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="201a3-125">在 ASP.NET 2.0 中，解码的视图状态看起来有点不同。</span><span class="sxs-lookup"><span data-stu-id="201a3-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="201a3-126">你应注意到已解码视图状态的外观发生了重大更改。</span><span class="sxs-lookup"><span data-stu-id="201a3-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="201a3-127">此更改具有多个体系结构 connect-through。</span><span class="sxs-lookup"><span data-stu-id="201a3-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="201a3-128">ASP.NET 1.x 中的视图状态使用 LosFormatter 来序列化数据。</span><span class="sxs-lookup"><span data-stu-id="201a3-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="201a3-129">在2.0 中，我们使用新的 ObjectStateFormatter 类。</span><span class="sxs-lookup"><span data-stu-id="201a3-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="201a3-130">此类专门用于帮助序列化和反序列化视图状态和控件状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="201a3-131">（下一节将介绍控件状态。）通过更改进行序列化和反序列化的方法，可以获得许多好处。</span><span class="sxs-lookup"><span data-stu-id="201a3-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="201a3-132">最显著的一点是，与使用 LosFormatter 的情况不同的是，ObjectStateFormatter 使用 BinaryWriter。</span><span class="sxs-lookup"><span data-stu-id="201a3-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="201a3-133">这允许 ASP.NET 2.0 存储视图状态一系列字节而不是字符串。</span><span class="sxs-lookup"><span data-stu-id="201a3-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="201a3-134">例如，使用整数。</span><span class="sxs-lookup"><span data-stu-id="201a3-134">Take, for example, an integer.</span></span> <span data-ttu-id="201a3-135">在 ASP.NET 1.1 中，需要4个字节的视图状态的整数。</span><span class="sxs-lookup"><span data-stu-id="201a3-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="201a3-136">在 ASP.NET 2.0 中，同一整数仅需要1个字节。</span><span class="sxs-lookup"><span data-stu-id="201a3-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="201a3-137">为了减少存储的视图状态量，已进行了其他增强。</span><span class="sxs-lookup"><span data-stu-id="201a3-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="201a3-138">例如，现在使用 Environment.tickcount 而不是字符串存储 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="201a3-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="201a3-139">就像这一切都不够，只需特别注意的是，在1.x 中，视图状态的最大使用者之一就是 DataGrid 和类似控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="201a3-140">控件（如视图状态所处的数据网格）的主要缺点是它通常包含大量重复的信息。</span><span class="sxs-lookup"><span data-stu-id="201a3-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="201a3-141">在 ASP.NET 1.x 中，重复的信息完全存储在一起，从而导致臃肿的视图状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="201a3-142">在 ASP.NET 2.0 中，我们使用新的 IndexedString 类来存储此类数据。</span><span class="sxs-lookup"><span data-stu-id="201a3-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="201a3-143">如果字符串重复，只需将 IndexedString 的标记和索引存储在正在运行的 IndexedString 对象的表中。</span><span class="sxs-lookup"><span data-stu-id="201a3-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="201a3-144">控件状态</span><span class="sxs-lookup"><span data-stu-id="201a3-144">Control State</span></span>

<span data-ttu-id="201a3-145">开发人员对视图状态的主要牢骚之一是它添加到 HTTP 有效负载的大小。</span><span class="sxs-lookup"><span data-stu-id="201a3-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="201a3-146">如前文所述，视图状态的最大使用者之一是 DataGrid 控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="201a3-147">为了避免 DataGrid 生成大量的视图状态，许多开发人员只是对该控件禁用了视图状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="201a3-148">遗憾的是，这种解决方案并不总是很好。</span><span class="sxs-lookup"><span data-stu-id="201a3-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="201a3-149">ASP.NET 1.x 中的视图状态不仅包含正确的控件功能所必需的数据。</span><span class="sxs-lookup"><span data-stu-id="201a3-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="201a3-150">它还包含有关控件的 UI 状态的信息。</span><span class="sxs-lookup"><span data-stu-id="201a3-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="201a3-151">这意味着，如果你希望允许在 DataGrid 上进行分页，则必须启用视图状态，即使你不需要视图状态包含的所有 UI 信息。</span><span class="sxs-lookup"><span data-stu-id="201a3-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="201a3-152">这是一个全或无意义的方案。</span><span class="sxs-lookup"><span data-stu-id="201a3-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="201a3-153">在 ASP.NET 2.0 中，控件状态通过引入控件状态来解决该问题。</span><span class="sxs-lookup"><span data-stu-id="201a3-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="201a3-154">控件状态包含对于控件的适当功能绝对必要的数据。</span><span class="sxs-lookup"><span data-stu-id="201a3-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="201a3-155">与视图状态不同，控件状态无法禁用。</span><span class="sxs-lookup"><span data-stu-id="201a3-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="201a3-156">因此，非常重要的一点是，严格控制以控件状态存储的数据。</span><span class="sxs-lookup"><span data-stu-id="201a3-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="201a3-157">控件状态与视图状态一起保留在 \_\_VIEWSTATE 隐藏窗体字段中。</span><span class="sxs-lookup"><span data-stu-id="201a3-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>

<span data-ttu-id="201a3-158">此视频是有关视图状态和控件状态的演练。</span><span class="sxs-lookup"><span data-stu-id="201a3-158">This video is a walkthrough of view state and control state.</span></span>

![](server-controls/_static/image1.png)

[<span data-ttu-id="201a3-159">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="201a3-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)

<span data-ttu-id="201a3-160">为了使服务器控件能够读取和写入控件状态，必须执行三个步骤。</span><span class="sxs-lookup"><span data-stu-id="201a3-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="201a3-161">步骤1：调用 RegisterRequiresControlState 方法</span><span class="sxs-lookup"><span data-stu-id="201a3-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="201a3-162">RegisterRequiresControlState 方法通知 ASP.NET 控件需要保持控件状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="201a3-163">它采用一个类型为控件的参数，该参数是正在注册的控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="201a3-164">请务必注意，注册不会从请求请求中保留。</span><span class="sxs-lookup"><span data-stu-id="201a3-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="201a3-165">因此，如果控件要保持控件状态，则必须在每个请求上调用此方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="201a3-166">建议在 OnInit 中调用方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="201a3-167">步骤2：重写 SaveControlState</span><span class="sxs-lookup"><span data-stu-id="201a3-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="201a3-168">SaveControlState 方法会在最后一次回发后保存控件的控件状态更改。</span><span class="sxs-lookup"><span data-stu-id="201a3-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="201a3-169">它返回表示控件状态的对象。</span><span class="sxs-lookup"><span data-stu-id="201a3-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="201a3-170">步骤3：重写 LoadControlState</span><span class="sxs-lookup"><span data-stu-id="201a3-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="201a3-171">LoadControlState 方法将已保存状态加载到控件中。</span><span class="sxs-lookup"><span data-stu-id="201a3-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="201a3-172">方法采用一个类型为 Object 的参数，该参数保存控件的已保存状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="201a3-173">完全符合 XHTML 标准</span><span class="sxs-lookup"><span data-stu-id="201a3-173">Full XHTML Compliance</span></span>

<span data-ttu-id="201a3-174">任何 Web 开发人员都知道 Web 应用程序中标准的重要性。</span><span class="sxs-lookup"><span data-stu-id="201a3-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="201a3-175">为了维护基于标准的开发环境，ASP.NET 2.0 完全符合 XHTML 标准。</span><span class="sxs-lookup"><span data-stu-id="201a3-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="201a3-176">因此，在支持 HTML 4.0 或更高版本的浏览器中，将根据 XHTML 标准呈现所有标记。</span><span class="sxs-lookup"><span data-stu-id="201a3-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="201a3-177">ASP.NET 1.1 中的 DOCTYPE 定义如下所示：</span><span class="sxs-lookup"><span data-stu-id="201a3-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="201a3-178">在 ASP.NET 2.0 中，默认 DOCTYPE 定义如下所示：</span><span class="sxs-lookup"><span data-stu-id="201a3-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="201a3-179">如果选择，则可以通过配置文件中的 xhtmlConformance 节点更改默认的 XHTML 符合性。</span><span class="sxs-lookup"><span data-stu-id="201a3-179">If you choose, you can alter the default XHTML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="201a3-180">例如，web.config 文件中的以下节点会将 XHTML 符合性更改为 XHTML 1.0 Strict：</span><span class="sxs-lookup"><span data-stu-id="201a3-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="201a3-181">如果选择此项，还可以将 ASP.NET 配置为使用 ASP.NET 1.x 中使用的旧配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="201a3-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="201a3-182">使用适配器的自适应呈现</span><span class="sxs-lookup"><span data-stu-id="201a3-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="201a3-183">在 ASP.NET 1.x 中，配置文件包含一个填充 HttpBrowserCapabilities 对象的 &lt;browserCaps&gt; 部分。</span><span class="sxs-lookup"><span data-stu-id="201a3-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="201a3-184">此对象允许开发人员确定哪个设备发出特定请求并适当地呈现代码。</span><span class="sxs-lookup"><span data-stu-id="201a3-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="201a3-185">在 ASP.NET 2.0 中，模型已改进，现在使用新的 ControlAdapter 类。</span><span class="sxs-lookup"><span data-stu-id="201a3-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="201a3-186">ControlAdapter 类重写控件生命周期中的事件，并基于用户代理的功能控制控件的呈现。</span><span class="sxs-lookup"><span data-stu-id="201a3-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="201a3-187">特定用户代理的功能由存储在 c:\windows\microsoft.net\framework\v2.0. 中的浏览器定义文件（扩展名为 .browser 的文件）定义\*\*\*\*\CONFIG\Browsers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="201a3-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="201a3-188">ControlAdapter 类是一个抽象类。</span><span class="sxs-lookup"><span data-stu-id="201a3-188">The ControlAdapter class is an abstract class.</span></span>

<span data-ttu-id="201a3-189">与 &lt;中的 browserCaps&gt; 部分非常类似，浏览器定义文件使用正则表达式来分析用户代理字符串，以便识别请求的浏览器。</span><span class="sxs-lookup"><span data-stu-id="201a3-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="201a3-190">它们定义了该用户代理的特定功能。</span><span class="sxs-lookup"><span data-stu-id="201a3-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="201a3-191">ControlAdapter 通过 Render 方法呈现控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="201a3-192">因此，如果重写 Render 方法，则不应调用基类上的 Render。</span><span class="sxs-lookup"><span data-stu-id="201a3-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="201a3-193">这样做可能会导致呈现发生两次，一次针对适配器，一次用于控件本身。</span><span class="sxs-lookup"><span data-stu-id="201a3-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="201a3-194">开发自定义适配器</span><span class="sxs-lookup"><span data-stu-id="201a3-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="201a3-195">可以通过从 ControlAdapter 继承来开发您自己的自定义适配器。</span><span class="sxs-lookup"><span data-stu-id="201a3-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="201a3-196">此外，如果页面需要适配器，则可以从抽象类 PageAdapter 继承。</span><span class="sxs-lookup"><span data-stu-id="201a3-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="201a3-197">通过浏览器定义文件中的 &lt;controlAdapters&gt; 元素，可以将控件映射到自定义适配器。</span><span class="sxs-lookup"><span data-stu-id="201a3-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="201a3-198">例如，以下来自浏览器定义文件的 XML 将 Menu 控件映射到 MenuAdapter 类：</span><span class="sxs-lookup"><span data-stu-id="201a3-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="201a3-199">使用此模型，控件开发人员可以很轻松地以特定设备或浏览器为目标。</span><span class="sxs-lookup"><span data-stu-id="201a3-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="201a3-200">对于开发人员而言，对每个设备上页面的呈现方式进行完全控制也非常简单。</span><span class="sxs-lookup"><span data-stu-id="201a3-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="201a3-201">每设备渲染</span><span class="sxs-lookup"><span data-stu-id="201a3-201">Per-Device Rendering</span></span>

<span data-ttu-id="201a3-202">可以使用浏览器特定的前缀，为每个设备指定 ASP.NET 2.0 中的服务器控件属性。</span><span class="sxs-lookup"><span data-stu-id="201a3-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="201a3-203">例如，下面的代码将更改标签的文本，具体取决于浏览页面所使用的设备。</span><span class="sxs-lookup"><span data-stu-id="201a3-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="201a3-204">当从 Internet Explorer 浏览包含此标签的页面时，标签将显示 "您正在从 Internet Explorer 浏览" 的文本。</span><span class="sxs-lookup"><span data-stu-id="201a3-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="201a3-205">从 Firefox 浏览该页面时，标签将显示 "正在从 Firefox 浏览" 的文本。</span><span class="sxs-lookup"><span data-stu-id="201a3-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="201a3-206">从任何其他设备浏览该页面时，它将显示 "正在从未知设备进行浏览。"</span><span class="sxs-lookup"><span data-stu-id="201a3-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="201a3-207">可使用此特殊语法指定任何属性。</span><span class="sxs-lookup"><span data-stu-id="201a3-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="201a3-208">设置焦点</span><span class="sxs-lookup"><span data-stu-id="201a3-208">Setting Focus</span></span>

<span data-ttu-id="201a3-209">ASP.NET 1.x 开发人员经常会询问如何对特定控件设置初始焦点。</span><span class="sxs-lookup"><span data-stu-id="201a3-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="201a3-210">例如，在登录页上，在首次加载页面时，使 "用户 ID" 文本框获得焦点非常有用。</span><span class="sxs-lookup"><span data-stu-id="201a3-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="201a3-211">在 ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="201a3-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="201a3-212">尽管此类脚本是一项简单的任务，但由于 SetFocus 方法，它在 ASP.NET 2.0 中不再是必需的。</span><span class="sxs-lookup"><span data-stu-id="201a3-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="201a3-213">SetFocus 方法采用一个参数，该参数指示应该接收焦点的控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="201a3-214">此参数可以是控件的客户端 ID，也可以是作为控件对象的服务器控件的名称。</span><span class="sxs-lookup"><span data-stu-id="201a3-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="201a3-215">例如，若要在第一次加载页面时将初始焦点设置为一个名为 txtUserID 的 TextBox 控件，请将以下代码添加到页面\_负载：</span><span class="sxs-lookup"><span data-stu-id="201a3-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="201a3-216">--或</span><span class="sxs-lookup"><span data-stu-id="201a3-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="201a3-217">ASP.NET 2.0 使用 Webresource 处理程序（前面讨论过）来呈现设置焦点的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="201a3-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="201a3-218">客户端函数的名称是 WebForm\_AutoFocus，如下所示：</span><span class="sxs-lookup"><span data-stu-id="201a3-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="201a3-219">此外，还可以使用控件的焦点方法将初始焦点设置到该控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="201a3-220">焦点方法派生自 Control 类，可用于所有 ASP.NET 2.0 控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="201a3-221">还可以在发生验证错误时将焦点设置到特定控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="201a3-222">将在后面的模块中介绍。</span><span class="sxs-lookup"><span data-stu-id="201a3-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="201a3-223">ASP.NET 2.0 中的新服务器控件</span><span class="sxs-lookup"><span data-stu-id="201a3-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="201a3-224">下面是 ASP.NET 2.0 中的新服务器控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="201a3-225">我们将在后面的模块中详细介绍其中一些内容。</span><span class="sxs-lookup"><span data-stu-id="201a3-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="201a3-226">ImageMap 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-226">ImageMap Control</span></span>

<span data-ttu-id="201a3-227">ImageMap 控件使你可以向映像添加热点，使其可以发起回发或导航到 URL。</span><span class="sxs-lookup"><span data-stu-id="201a3-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="201a3-228">有三种可用的热点类型;CircleHotSpot、RectangleHotSpot 和 PolygonHotSpot。</span><span class="sxs-lookup"><span data-stu-id="201a3-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="201a3-229">通过 Visual Studio 中的集合编辑器或以编程方式在代码中添加热点。</span><span class="sxs-lookup"><span data-stu-id="201a3-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="201a3-230">没有用户界面可用于绘制图像上的热点。</span><span class="sxs-lookup"><span data-stu-id="201a3-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="201a3-231">必须以声明方式指定作用点的坐标、大小或半径。</span><span class="sxs-lookup"><span data-stu-id="201a3-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="201a3-232">设计器中也没有热点的直观表示形式。</span><span class="sxs-lookup"><span data-stu-id="201a3-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="201a3-233">如果将作用点配置为导航到 URL，则 URL 是通过作用点的 NavigateUrl 属性指定的。</span><span class="sxs-lookup"><span data-stu-id="201a3-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="201a3-234">对于回发热点，PostBackValue 属性允许您传递回发中可在服务器端代码中检索的字符串。</span><span class="sxs-lookup"><span data-stu-id="201a3-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>

![Visual Studio 中的作用点集合编辑器](server-controls/_static/image1.jpg)

<span data-ttu-id="201a3-236">**图 1**： Visual Studio 中的热点集合编辑器</span><span class="sxs-lookup"><span data-stu-id="201a3-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>

## <a name="bulletedlist-control"></a><span data-ttu-id="201a3-237">BulletedList 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-237">BulletedList Control</span></span>

<span data-ttu-id="201a3-238">BulletedList 控件是可以轻松地进行数据绑定的项目符号列表。</span><span class="sxs-lookup"><span data-stu-id="201a3-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="201a3-239">可以通过 BulletStyle 属性对该列表进行排序（编号）或无序。</span><span class="sxs-lookup"><span data-stu-id="201a3-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="201a3-240">列表中的每一项都由一个列表项对象表示。</span><span class="sxs-lookup"><span data-stu-id="201a3-240">Each item in the list is represented by a ListItem object.</span></span>

![Visual Studio 中的 BulletedList 控件](server-controls/_static/image1.gif)

<span data-ttu-id="201a3-242">**图 2**： Visual Studio 中的 BulletedList 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>

## <a name="hiddenfield-control"></a><span data-ttu-id="201a3-243">HiddenField 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-243">HiddenField Control</span></span>

<span data-ttu-id="201a3-244">HiddenField 控件向页面中添加一个隐藏的窗体字段，此字段的值在服务器端代码中可用。</span><span class="sxs-lookup"><span data-stu-id="201a3-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="201a3-245">在 post 后，隐藏的窗体字段的值通常应保持不变。</span><span class="sxs-lookup"><span data-stu-id="201a3-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="201a3-246">但是，恶意用户可能会在回发之前更改值。</span><span class="sxs-lookup"><span data-stu-id="201a3-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="201a3-247">如果发生这种情况，HiddenField 控件将引发 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="201a3-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="201a3-248">如果 HiddenField 控件中包含敏感信息，并且要确保它保持不变，应在代码中处理 ValueChanged 事件。</span><span class="sxs-lookup"><span data-stu-id="201a3-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="201a3-249">FileUpload 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-249">FileUpload Control</span></span>

<span data-ttu-id="201a3-250">ASP.NET 2.0 中的 FileUpload 控件使你可以通过 ASP.NET 页将文件上传到 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="201a3-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="201a3-251">此控件非常类似于 ASP.NET 1.x HtmlInputFile 类，但有一些例外情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="201a3-252">在 ASP.NET 1.x 中，建议检查 PostedFile 属性是否为 null，以确定是否有合适的文件。</span><span class="sxs-lookup"><span data-stu-id="201a3-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="201a3-253">ASP.NET 2.0 中的 FileUpload 控件添加了一个新的 HasFile 属性，你可以将其用于相同的目的，而且效率更高。</span><span class="sxs-lookup"><span data-stu-id="201a3-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="201a3-254">PostedFile 属性仍可用于访问 HttpPostedFile 对象，但 HttpPostedFile 的某些功能现在可在 FileUpload 控件的内部使用。</span><span class="sxs-lookup"><span data-stu-id="201a3-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="201a3-255">例如，若要将上载的文件保存在 ASP.NET 1.x 中，请对 HttpPostedFile 对象调用 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="201a3-256">使用 ASP.NET 2.0 中的 FileUpload 控件，可以对 FileUpload 控件本身调用 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="201a3-257">2\.0 行为的另一个重大更改（并且可能是最重大的更改）是不再需要在保存之前将整个上载的文件加载到内存中。</span><span class="sxs-lookup"><span data-stu-id="201a3-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="201a3-258">在1.x 中，上传的任何文件都将在写入磁盘之前完全保存在内存中。</span><span class="sxs-lookup"><span data-stu-id="201a3-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="201a3-259">此体系结构阻止上传大型文件。</span><span class="sxs-lookup"><span data-stu-id="201a3-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="201a3-260">在 ASP.NET 2.0 中，httpRuntime 元素的 requestLengthDiskThreshold 属性允许你配置在将缓冲区中的缓冲区中包含多少 Kb，然后再将其写入磁盘。</span><span class="sxs-lookup"><span data-stu-id="201a3-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="201a3-261">**重要**说明： MSDN 文档（和其他位置的文档）指定此值以字节（而非 kb）为单位，默认值为256。</span><span class="sxs-lookup"><span data-stu-id="201a3-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="201a3-262">实际以 Kb 为单位指定该值，默认值为80。</span><span class="sxs-lookup"><span data-stu-id="201a3-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="201a3-263">通过将默认值设置为80K，我们确保缓冲区不会在大型对象堆上结束。</span><span class="sxs-lookup"><span data-stu-id="201a3-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="201a3-264">向导控件</span><span class="sxs-lookup"><span data-stu-id="201a3-264">Wizard Control</span></span>

<span data-ttu-id="201a3-265">使用面板或从页面传输到页面时，ASP.NET 开发人员努力尝试使用一系列 "页面" 收集信息非常常见。</span><span class="sxs-lookup"><span data-stu-id="201a3-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="201a3-266">通常情况下，这是一项令人沮丧的工作，非常耗时。</span><span class="sxs-lookup"><span data-stu-id="201a3-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="201a3-267">新向导控件通过允许用户熟悉的向导界面中的线性和非线性步骤，解决了问题。</span><span class="sxs-lookup"><span data-stu-id="201a3-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="201a3-268">该向导控件在一系列步骤中提供输入窗体。</span><span class="sxs-lookup"><span data-stu-id="201a3-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="201a3-269">每个步骤都是由控件的 StepType 属性指定的特定类型。</span><span class="sxs-lookup"><span data-stu-id="201a3-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="201a3-270">可用步骤类型如下：</span><span class="sxs-lookup"><span data-stu-id="201a3-270">The available step types are as follows:</span></span>

| <span data-ttu-id="201a3-271">**步骤类型**</span><span class="sxs-lookup"><span data-stu-id="201a3-271">**Step Type**</span></span> | <span data-ttu-id="201a3-272">**解释**</span><span class="sxs-lookup"><span data-stu-id="201a3-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="201a3-273">自动</span><span class="sxs-lookup"><span data-stu-id="201a3-273">Auto</span></span> | <span data-ttu-id="201a3-274">向导会根据步骤在步骤层次结构内的位置自动确定步骤类型。</span><span class="sxs-lookup"><span data-stu-id="201a3-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="201a3-275">Start</span><span class="sxs-lookup"><span data-stu-id="201a3-275">Start</span></span> | <span data-ttu-id="201a3-276">第一步，通常用于提供介绍性语句。</span><span class="sxs-lookup"><span data-stu-id="201a3-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="201a3-277">步骤</span><span class="sxs-lookup"><span data-stu-id="201a3-277">Step</span></span> | <span data-ttu-id="201a3-278">正常步骤。</span><span class="sxs-lookup"><span data-stu-id="201a3-278">A normal step.</span></span> |
| <span data-ttu-id="201a3-279">完成</span><span class="sxs-lookup"><span data-stu-id="201a3-279">Finish</span></span> | <span data-ttu-id="201a3-280">最后一个步骤，通常用于显示完成向导的按钮。</span><span class="sxs-lookup"><span data-stu-id="201a3-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="201a3-281">完成</span><span class="sxs-lookup"><span data-stu-id="201a3-281">Complete</span></span> | <span data-ttu-id="201a3-282">显示消息 "成功" 或 "失败"。</span><span class="sxs-lookup"><span data-stu-id="201a3-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="201a3-283">向导控件使用 ASP.NET 控件状态来跟踪其状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="201a3-284">因此，可以将 EnableViewState 属性设置为 false，无需任何不利。</span><span class="sxs-lookup"><span data-stu-id="201a3-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>

<span data-ttu-id="201a3-285">此视频是向导控件的演练。</span><span class="sxs-lookup"><span data-stu-id="201a3-285">This video is a walkthrough of the Wizard control.</span></span>

![](server-controls/_static/image2.png)

[<span data-ttu-id="201a3-286">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="201a3-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a><span data-ttu-id="201a3-287">本地化控件</span><span class="sxs-lookup"><span data-stu-id="201a3-287">Localize Control</span></span>

<span data-ttu-id="201a3-288">"本地化" 控件类似于 "文本" 控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="201a3-289">但 "本地化" 控件具有一个**模式**属性，该属性控制向其添加标记的方式。</span><span class="sxs-lookup"><span data-stu-id="201a3-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="201a3-290">Mode 属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="201a3-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="201a3-291">**模式**</span><span class="sxs-lookup"><span data-stu-id="201a3-291">**Mode**</span></span> | <span data-ttu-id="201a3-292">**解释**</span><span class="sxs-lookup"><span data-stu-id="201a3-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="201a3-293">Transform</span><span class="sxs-lookup"><span data-stu-id="201a3-293">Transform</span></span> | <span data-ttu-id="201a3-294">根据发出请求的浏览器的协议来转换标记。</span><span class="sxs-lookup"><span data-stu-id="201a3-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="201a3-295">直通</span><span class="sxs-lookup"><span data-stu-id="201a3-295">PassThrough</span></span> | <span data-ttu-id="201a3-296">标记按原样呈现。</span><span class="sxs-lookup"><span data-stu-id="201a3-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="201a3-297">编码</span><span class="sxs-lookup"><span data-stu-id="201a3-297">Encode</span></span> | <span data-ttu-id="201a3-298">添加到控件的标记使用 Server.htmlencode 进行编码。</span><span class="sxs-lookup"><span data-stu-id="201a3-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="201a3-299">查看和查看控件</span><span class="sxs-lookup"><span data-stu-id="201a3-299">MultiView and View Controls</span></span>

<span data-ttu-id="201a3-300">多视图控件用作视图控件的容器，而视图控件充当其他控件的容器（与面板控件非常相似）。</span><span class="sxs-lookup"><span data-stu-id="201a3-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="201a3-301">查看视图控件中的每个视图都由单个视图控件表示。</span><span class="sxs-lookup"><span data-stu-id="201a3-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="201a3-302">此视图中的第一个视图控件是 view 0，第二个视图控件是 view 1，依此类推。您可以通过指定 "ActiveViewIndex" 控件的 "视图" 来切换视图。</span><span class="sxs-lookup"><span data-stu-id="201a3-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="201a3-303">替换控件</span><span class="sxs-lookup"><span data-stu-id="201a3-303">Substitution Control</span></span>

<span data-ttu-id="201a3-304">替换控件与 ASP.NET 缓存结合使用。</span><span class="sxs-lookup"><span data-stu-id="201a3-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="201a3-305">如果你想要利用缓存，但你有一些必须在每个请求上更新的页面（换句话说，是从缓存中免除的部分），则替换组件会提供一个很好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="201a3-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="201a3-306">控件实际上不会自行呈现任何输出。</span><span class="sxs-lookup"><span data-stu-id="201a3-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="201a3-307">而是绑定到服务器端代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="201a3-308">请求页面时，将调用方法，而返回的标记将替换为替换控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="201a3-309">通过方法**名称**属性指定替换控件所绑定到的方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="201a3-310">该方法必须满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="201a3-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="201a3-311">它必须是静态的（在 VB 中共享）方法。</span><span class="sxs-lookup"><span data-stu-id="201a3-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="201a3-312">它接受一个类型为 HttpContext 的参数。</span><span class="sxs-lookup"><span data-stu-id="201a3-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="201a3-313">它将返回一个字符串，该字符串表示应该替换页面上的控件的标记。</span><span class="sxs-lookup"><span data-stu-id="201a3-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="201a3-314">替换控件不能修改该页上的任何其他控件，但它可以通过其参数访问当前 HttpContext。</span><span class="sxs-lookup"><span data-stu-id="201a3-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="201a3-315">GridView 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-315">GridView Control</span></span>

<span data-ttu-id="201a3-316">GridView 控件是对 DataGrid 控件的替换。</span><span class="sxs-lookup"><span data-stu-id="201a3-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="201a3-317">稍后的模块中将更详细地介绍此控件。</span><span class="sxs-lookup"><span data-stu-id="201a3-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="201a3-318">DetailsView 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-318">DetailsView Control</span></span>

<span data-ttu-id="201a3-319">使用 DetailsView 控件可以显示数据源中的单个记录，还可以编辑或删除该记录。</span><span class="sxs-lookup"><span data-stu-id="201a3-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="201a3-320">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="201a3-321">FormView 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-321">FormView Control</span></span>

<span data-ttu-id="201a3-322">FormView 控件用于在可配置接口中显示数据源中的单个记录。</span><span class="sxs-lookup"><span data-stu-id="201a3-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="201a3-323">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="201a3-324">AccessDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-324">AccessDataSource Control</span></span>

<span data-ttu-id="201a3-325">AccessDataSource 控件用于对 Access 数据库进行数据绑定。</span><span class="sxs-lookup"><span data-stu-id="201a3-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="201a3-326">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="201a3-327">ObjectDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-327">ObjectDataSource Control</span></span>

<span data-ttu-id="201a3-328">ObjectDataSource 控件用于支持三层体系结构，使控件可以数据绑定到中间层业务对象，而不是将控件直接绑定到数据源的两层模型。</span><span class="sxs-lookup"><span data-stu-id="201a3-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="201a3-329">稍后的模块中将对此进行更详细的讨论。</span><span class="sxs-lookup"><span data-stu-id="201a3-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="201a3-330">XmlDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-330">XmlDataSource Control</span></span>

<span data-ttu-id="201a3-331">XmlDataSource 控件用于将数据绑定到 XML 数据源。</span><span class="sxs-lookup"><span data-stu-id="201a3-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="201a3-332">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="201a3-333">SiteMapDataSource 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="201a3-334">SiteMapDataSource 控件根据站点地图提供站点导航控件的数据绑定。</span><span class="sxs-lookup"><span data-stu-id="201a3-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="201a3-335">稍后的模块中将对此进行更详细的讨论。</span><span class="sxs-lookup"><span data-stu-id="201a3-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="201a3-336">SiteMapPath 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-336">SiteMapPath Control</span></span>

<span data-ttu-id="201a3-337">SiteMapPath 控件显示一系列通常称为痕迹导航的导航链接。</span><span class="sxs-lookup"><span data-stu-id="201a3-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="201a3-338">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="201a3-339">Menu 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-339">Menu Control</span></span>

<span data-ttu-id="201a3-340">Menu 控件使用 DHTML 显示动态菜单。</span><span class="sxs-lookup"><span data-stu-id="201a3-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="201a3-341">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="201a3-342">TreeView 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-342">TreeView Control</span></span>

<span data-ttu-id="201a3-343">TreeView 控件用于显示数据的分层树视图。</span><span class="sxs-lookup"><span data-stu-id="201a3-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="201a3-344">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="201a3-345">登录控件</span><span class="sxs-lookup"><span data-stu-id="201a3-345">Login Control</span></span>

<span data-ttu-id="201a3-346">登录控件提供了用于登录到网站的机制。</span><span class="sxs-lookup"><span data-stu-id="201a3-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="201a3-347">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="201a3-348">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-348">LoginView Control</span></span>

<span data-ttu-id="201a3-349">登录视图控件允许基于用户的登录状态显示不同的模板。</span><span class="sxs-lookup"><span data-stu-id="201a3-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="201a3-350">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="201a3-351">PasswordRecovery 控件</span><span class="sxs-lookup"><span data-stu-id="201a3-351">PasswordRecovery Control</span></span>

<span data-ttu-id="201a3-352">PasswordRecovery 控件用于检索 ASP.NET 应用程序的用户的忘记密码。</span><span class="sxs-lookup"><span data-stu-id="201a3-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="201a3-353">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="201a3-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="201a3-354">LoginStatus</span></span>

<span data-ttu-id="201a3-355">LoginStatus 控件显示用户的登录状态。</span><span class="sxs-lookup"><span data-stu-id="201a3-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="201a3-356">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="201a3-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="201a3-357">LoginName</span></span>

<span data-ttu-id="201a3-358">LoginName 控件在登录到 ASP.NET 应用程序后显示用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="201a3-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="201a3-359">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="201a3-360">CreateUserWizard</span><span class="sxs-lookup"><span data-stu-id="201a3-360">CreateUserWizard</span></span>

<span data-ttu-id="201a3-361">CreateUserWizard 是一个可配置的向导，它使用户能够创建 ASP.NET 成员资格帐户，以便在 ASP.NET 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="201a3-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="201a3-362">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="201a3-363">ChangePassword</span><span class="sxs-lookup"><span data-stu-id="201a3-363">ChangePassword</span></span>

<span data-ttu-id="201a3-364">ChangePassword 控件允许用户为 ASP.NET 应用程序更改其密码。</span><span class="sxs-lookup"><span data-stu-id="201a3-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="201a3-365">稍后的模块中更详细地介绍了这种情况。</span><span class="sxs-lookup"><span data-stu-id="201a3-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="201a3-366">各种 Webpart</span><span class="sxs-lookup"><span data-stu-id="201a3-366">Various WebParts</span></span>

<span data-ttu-id="201a3-367">ASP.NET 2.0 附带了各种 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="201a3-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="201a3-368">稍后的模块中将详细介绍这些内容。</span><span class="sxs-lookup"><span data-stu-id="201a3-368">These will be covered in detail in a later module.</span></span>
