---
ms.openlocfilehash: 2481b10abae9aefce2d5173d8071e4c2236db928
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048220"
---

> [!NOTE]
> 다양한 스키마 변경 작업은 EF Core SQLite 공급자에서 지원하지 않습니다. 예를 들어 열 추가는 지원되지만 열 제거는 지원되지 않습니다. 열을 제거 하려면 마이그레이션 만들어지는 경우 합니다 `ef migrations add` 명령이 성공 하지만 `ef database update` 명령이 실패 합니다. 수동으로 마이그레이션을 테이블 다시 빌드를 수행 하는 코드를 작성 하 여 이러한 제한 중 일부 문제를 해결할 수 있습니다. 테이블 다시 빌드에는 다음이 포함 됩니다.

>* 기존 테이블을 이름을 바꿉니다.
>* 새 테이블을 만드는 중입니다.
>* 이전 테이블에서 새 테이블에 데이터를 복사합니다.
>* 이전 테이블을 삭제 합니다.

자세한 내용은 다음 리소스를 참조하세요.
> * [SQLite EF Core 데이터베이스 공급자 제한 사항](/ef/core/providers/sqlite/limitations)
> * [마이그레이션 코드 사용자 지정](/ef/core/managing-schemas/migrations/#customize-migration-code)
> * [데이터 시드](/ef/core/modeling/data-seeding)