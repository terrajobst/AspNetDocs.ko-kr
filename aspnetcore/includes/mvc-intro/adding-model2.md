---
ms.openlocfilehash: f323482d6f8bfaebf7bf6673d5fb91608430760a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57044080"
---
## <a name="add-initial-migration-and-update-the-database"></a><span data-ttu-id="4e0f3-101">초기 마이그레이션을 추가 하 고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-101">Add initial migration and update the database</span></span>

* <span data-ttu-id="4e0f3-102">명령 프롬프트를 열고 프로젝트 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-102">Open a command prompt and navigate to the project directory.</span></span> <span data-ttu-id="4e0f3-103">(포함 하는 디렉터리를 *Startup.cs* 파일).</span><span class="sxs-lookup"><span data-stu-id="4e0f3-103">(The directory containing the *Startup.cs* file).</span></span>

* <span data-ttu-id="4e0f3-104">명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-104">Run the following commands in the command prompt:</span></span>

  ```console
  dotnet restore
  dotnet ef migrations add Initial
  dotnet ef database update
  ```
  
  <span data-ttu-id="4e0f3-105">[.NET core](/dotnet/core/tools/index) .NET의 플랫폼 간 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-105">[.NET Core](/dotnet/core/tools/index) is a cross-platform implementation of .NET.</span></span> <span data-ttu-id="4e0f3-106">다음이 명령을 수행할 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-106">Here is what these commands do:</span></span>

  * <span data-ttu-id="4e0f3-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): 에 지정 된 NuGet 패키지를 다운로드 합니다 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-107">[dotnet restore](/dotnet/core/tools/dotnet-restore): Downloads the NuGet packages specified in the *.csproj* file.</span></span>
  * <span data-ttu-id="4e0f3-108">`dotnet ef migrations add Initial` Entity Framework.NET Core CLI 마이그레이션 명령을 실행 하 고 초기 마이그레이션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-108">`dotnet ef migrations add Initial` Runs the Entity Framework .NET Core CLI migrations command and creates the initial migration.</span></span> <span data-ttu-id="4e0f3-109">"추가" 후 마이그레이션에 할당 하는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-109">The parameter after "add" is a name that you assign to the migration.</span></span> <span data-ttu-id="4e0f3-110">여기에 이름을 지정 마이그레이션 "초기" 초기 데이터베이스 마이그레이션은 이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-110">Here you're naming the migration "Initial" because it's the initial database migration.</span></span> <span data-ttu-id="4e0f3-111">이 작업을 만듭니다는 *데이터/Migrations/\<날짜-시간 > _Initial.cs* 추가할 마이그레이션 명령이 포함 된 파일을 *영화* 테이블을 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-111">This operation creates the *Data/Migrations/\<date-time>_Initial.cs* file containing the migration commands to add the *Movie* table to the database.</span></span>
  * <span data-ttu-id="4e0f3-112">`dotnet ef database update`  방금 만든 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-112">`dotnet ef database update`  Updates the database with the migration we just created.</span></span>

<span data-ttu-id="4e0f3-113">다음 자습서에서는 데이터베이스 및 연결 문자열에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-113">You'll learn about the database and connection string in the next tutorial.</span></span> <span data-ttu-id="4e0f3-114">데이터 모델 변경 내용에 대해 알아봅니다 합니다 [필드를 추가](xref:tutorials/first-mvc-app/new-field) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="4e0f3-114">You'll learn about data model changes in the [Add a field](xref:tutorials/first-mvc-app/new-field) tutorial.</span></span>
