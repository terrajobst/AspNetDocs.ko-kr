---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044080"
---
## <a name="add-initial-migration-and-update-the-database"></a>초기 마이그레이션을 추가 하 고 데이터베이스를 업데이트 합니다.

* 명령 프롬프트를 열고 프로젝트 디렉터리로 이동 합니다. (포함 하는 디렉터리를 *Startup.cs* 파일).

* 명령 프롬프트에서 다음 명령을 실행합니다.

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  [.NET core](/dotnet/core/tools/index) .NET의 플랫폼 간 구현입니다. 다음이 명령을 수행할 다음과 같습니다.

  * [dotnet restore](/dotnet/core/tools/dotnet-restore): 에 지정 된 NuGet 패키지를 다운로드 합니다 *.csproj* 파일입니다.
  * `dotnet ef migrations add Initial` Entity Framework.NET Core CLI 마이그레이션 명령을 실행 하 고 초기 마이그레이션을 만듭니다. "추가" 후 마이그레이션에 할당 하는 이름입니다. 여기에 이름을 지정 마이그레이션 "초기" 초기 데이터베이스 마이그레이션은 이기 때문입니다. 이 작업을 만듭니다는 *데이터/Migrations/\<날짜-시간 > _Initial.cs* 추가할 마이그레이션 명령이 포함 된 파일을 *영화* 테이블을 데이터베이스.
  * `dotnet ef database update`  방금 만든 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.

다음 자습서에서는 데이터베이스 및 연결 문자열에 대해 알아봅니다. 데이터 모델 변경 내용에 대해 알아봅니다 합니다 [필드를 추가](xref:tutorials/first-mvc-app/new-field) 자습서입니다.
