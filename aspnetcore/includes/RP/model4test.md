---
ms.openlocfilehash: 22c540058e0b3b9ae612f1b2612cecc08627ea2b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57063990"
---
<a name="test"></a>
### <a name="test-the-app"></a><span data-ttu-id="a365e-101">앱 테스트</span><span class="sxs-lookup"><span data-stu-id="a365e-101">Test the app</span></span>

* <span data-ttu-id="a365e-102">앱을 실행하고 브라우저에서 `/Movies`를 URL에 추가합니다(`http://localhost:port/movies`).</span><span class="sxs-lookup"><span data-stu-id="a365e-102">Run the app and append `/Movies` to the URL in the browser (`http://localhost:port/movies`).</span></span>
* <span data-ttu-id="a365e-103">**만들기** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a365e-103">Test the **Create** link.</span></span>

  ![페이지 만들기](../../tutorials/razor-pages/model/_static/conan.png)

<a name="scaffold"></a>

* <span data-ttu-id="a365e-105">**편집**, **세부 정보** 및 **삭제** 링크를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="a365e-105">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="a365e-106">다음 오류가 표시되면 마이그레이션을 실행했고 데이터베이스를 업데이트했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a365e-106">If you get the following error, verify you have run migrations and updated the database:</span></span>

```
An unhandled exception occurred while processing the request.
SqliteException: SQLite Error 1: 'no such table: Movie'.
Microsoft.Data.Sqlite.SqliteException.ThrowExceptionForRC(int rc, sqlite3 db)
```
