---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063984"
---
<a name="test"></a>
### <a name="test-the-app"></a>测试应用

* 运行应用并将 `/Movies` 追加到浏览器中的 URL (`http://localhost:port/movies`)。
* 测试“创建”链接。

  ![创建页面](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* 测试“编辑”、“详细信息”和“删除”链接。

如果收到以下错误，则验证是否已运行迁移并更新数据库：

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
