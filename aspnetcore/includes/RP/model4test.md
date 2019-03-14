---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063984"
---
<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="c9ba3-101">测试应用</span><span class="sxs-lookup"><span data-stu-id="c9ba3-101">Test the app</span></span>

* <span data-ttu-id="c9ba3-102">运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。</span><span class="sxs-lookup"><span data-stu-id="c9ba3-102">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="c9ba3-103">测试“创建”链接。</span><span class="sxs-lookup"><span data-stu-id="c9ba3-103">Test the **Create** link.</span></span>

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="c9ba3-105">测试“编辑”、“详细信息”和“删除”链接。</span><span class="sxs-lookup"><span data-stu-id="c9ba3-105">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="c9ba3-106">如果收到以下错误，则验证是否已运行迁移并更新数据库：</span><span class="sxs-lookup"><span data-stu-id="c9ba3-106">If you get the following error, verify you have run migrations and updated the database:</span></span>

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
