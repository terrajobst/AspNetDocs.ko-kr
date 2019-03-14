---
ms.openlocfilehash: 4d6b6309e6e15c364542b5d3ae296d53c6ea4358
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037400"
---
<span data-ttu-id="bbdb5-101">생성 된 Identity 데이터베이스 코드를 실행 하려면 [Entity Framework Core 마이그레이션은](/ef/core/managing-schemas/migrations/)합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb5-101">The generated Identity database code requires [Entity Framework Core Migrations](/ef/core/managing-schemas/migrations/).</span></span> <span data-ttu-id="bbdb5-102">마이그레이션을 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb5-102">Create a migration and update the database.</span></span> <span data-ttu-id="bbdb5-103">예를 들어, 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb5-103">For example, run the following commands:</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="bbdb5-104">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbdb5-104">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="bbdb5-105">Visual studio에서 **패키지 관리자 콘솔**:</span><span class="sxs-lookup"><span data-stu-id="bbdb5-105">In the Visual Studio **Package Manager Console**:</span></span>

```PMC
Add-Migration CreateIdentitySchema
Update-Database
```

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="bbdb5-106">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="bbdb5-106">.NET Core CLI</span></span>](#tab/netcore-cli)

```cli
dotnet ef migrations add CreateIdentitySchema
dotnet ef database update
```

------

<span data-ttu-id="bbdb5-107">에 대 한 "CreateIdentitySchema" name 매개 변수는 `Add-Migration` 임의의 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb5-107">The "CreateIdentitySchema" name parameter for the `Add-Migration` command is arbitrary.</span></span> <span data-ttu-id="bbdb5-108">`"CreateIdentitySchema"` 마이그레이션하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbdb5-108">`"CreateIdentitySchema"` describes the migration.</span></span>
