---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048220"
---

> [!NOTE]
> <span data-ttu-id="938f4-101">다양한 스키마 변경 작업은 EF Core SQLite 공급자에서 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-101">Many schema change operations are not supported by the EF Core SQLite provider.</span></span> <span data-ttu-id="938f4-102">예를 들어 열 추가는 지원되지만 열 제거는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-102">For example, adding a column is supported, but removing a column is not supported.</span></span> <span data-ttu-id="938f4-103">열을 제거 하려면 마이그레이션 만들어지는 경우 합니다 `ef migrations add` 명령이 성공 하지만 `ef database update` 명령이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-103">If a migration is created to remove a column, the `ef migrations add` command succeeds but the `ef database update` command fails.</span></span> <span data-ttu-id="938f4-104">수동으로 마이그레이션을 테이블 다시 빌드를 수행 하는 코드를 작성 하 여 이러한 제한 중 일부 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-104">Some of these limitations can be overcome by manually writing migrations code to perform a table rebuild.</span></span> <span data-ttu-id="938f4-105">테이블 다시 빌드에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-105">A table rebuild involves:</span></span>

>* <span data-ttu-id="938f4-106">기존 테이블을 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-106">Renaming the existing table.</span></span>
>* <span data-ttu-id="938f4-107">새 테이블을 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-107">Creating a new table.</span></span>
>* <span data-ttu-id="938f4-108">이전 테이블에서 새 테이블에 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-108">Copying data from the old table to the new table.</span></span>
>* <span data-ttu-id="938f4-109">이전 테이블을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="938f4-109">Dropping the old table.</span></span>

<span data-ttu-id="938f4-110">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="938f4-110">For more information, see the following resources:</span></span>
> * [<span data-ttu-id="938f4-111">SQLite EF Core 데이터베이스 공급자 제한 사항</span><span class="sxs-lookup"><span data-stu-id="938f4-111">SQLite EF Core Database Provider Limitations</span></span>](/ef/core/providers/sqlite/limitations)
> * [<span data-ttu-id="938f4-112">마이그레이션 코드 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="938f4-112">Customize migration code</span></span>](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [<span data-ttu-id="938f4-113">데이터 시드</span><span class="sxs-lookup"><span data-stu-id="938f4-113">Data seeding</span></span>](/ef/core/modeling/data-seeding)