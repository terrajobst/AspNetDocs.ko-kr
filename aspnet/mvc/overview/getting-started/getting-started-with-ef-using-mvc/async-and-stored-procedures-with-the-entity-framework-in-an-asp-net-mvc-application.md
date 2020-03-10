---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 async 및 저장 프로시저 사용'
description: 이 자습서에서는 비동기 프로그래밍 모델을 구현 하 고 저장 프로시저를 사용 하는 방법을 알아봅니다.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471389"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 async 및 저장 프로시저 사용

이전 자습서에서는 동기 프로그래밍 모델을 사용 하 여 데이터를 읽고 업데이트 하는 방법을 알아보았습니다. 이 자습서에서는 비동기 프로그래밍 모델을 구현 하는 방법을 확인 합니다. 비동기 코드를 사용 하면 서버 리소스를 더 효율적으로 사용할 수 있으므로 응용 프로그램 성능이 향상 될 수 있습니다.

이 자습서에서는 엔터티에 대 한 삽입, 업데이트 및 삭제 작업에 저장 프로시저를 사용 하는 방법에 대해서도 설명 합니다.

마지막으로 응용 프로그램을 처음 배포할 때 구현한 모든 데이터베이스 변경 내용과 함께 Azure에 다시 배포 합니다.

다음 그림에서는 사용할 일부 페이지를 보여 줍니다.

![부서 페이지](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![부서 만들기](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 비동기 코드에 대 한 자세한 정보
> * 부서 컨트롤러 만들기
> * 저장 프로시저 사용
> * Deploy to Azure

## <a name="prerequisites"></a>사전 요구 사항

* [관련 데이터 업데이트](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a>비동기 코드를 사용 하는 이유

웹 서버에는 사용할 수 있는 스레드 수가 제한적이며, 로드 양이 많은 상황에서는 사용 가능한 모든 스레드가 사용될 수 있습니다. 이 경우 서버는 스레드가 해제될 때까지 새 요청을 처리할 수 없습니다. 동기 코드를 사용하면 I/O 완료를 대기하느라 작업을 실제로 수행하지 않는 동안에 많은 스레드가 정체될 수 있습니다. 비동기 코드를 사용하면 프로세스가 I/O 완료를 대기할 때 다른 요청을 처리하는 데 사용하도록 해당 스레드가 서버에서 해제됩니다. 결과적으로 비동기 코드를 사용 하면 서버 리소스를 더 효율적으로 사용할 수 있으며 서버는 지연 없이 더 많은 트래픽을 처리할 수 있습니다.

이전 버전의 .NET에서는 비동기 코드를 작성 하 고 테스트 하는 작업이 복잡 하 고 오류가 발생 하기 쉬우며 디버그 하기가 어렵습니다. .NET 4.5에서 비동기 코드를 작성, 테스트 및 디버깅 하는 것은 이유를 제외 하 고는 일반적으로 비동기 코드를 작성 하는 것 보다 훨씬 쉽습니다. 비동기 코드는 약간의 오버 헤드를 발생 시키지만 트래픽 트래픽이 적은 경우 성능이 저하 되는 반면, 트래픽이 많은 상황에서는 잠재적 성능 향상이 매우 중요 합니다.

비동기 프로그래밍에 대 한 자세한 내용은 [.net 4.5의 비동기 지원을 사용 하 여 호출 차단 방지](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)를 참조 하세요.

## <a name="create-department-controller"></a>부서 컨트롤러 만들기

이전 컨트롤러와 동일한 방식으로 부서 컨트롤러를 만듭니다. 단,이 시간을 제외 하 고는 **비동기 컨트롤러 작업 사용** 확인란을 선택 합니다.

다음 하이라이트는 비동기 작업을 수행 하기 위해 `Index` 메서드의 동기 코드에 추가 된 내용을 보여 줍니다.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

Entity Framework 데이터베이스 쿼리를 비동기적으로 실행할 수 있도록 네 가지 변경 사항이 적용 되었습니다.

- 메서드는 메서드 본문의 부분에 대 한 콜백을 생성 하 고 반환 되는 `Task<ActionResult>` 개체를 자동으로 만들도록 컴파일러에 지시 하는 `async` 키워드로 표시 됩니다.
- 반환 형식이 `ActionResult`에서 `Task<ActionResult>`로 변경 되었습니다. `Task<T>` 형식은 `T`형식의 결과를 사용 하 여 진행 중인 작업을 나타냅니다.
- `await` 키워드가 웹 서비스 호출에 적용 되었습니다. 컴파일러가이 키워드를 볼 때 백그라운드에서 메서드를 두 부분으로 분할 합니다. 첫 번째 부분은 비동기적으로 시작 되는 작업으로 끝납니다. 두 번째 부분은 작업이 완료 될 때 호출 되는 콜백 메서드에 배치 됩니다.
- `ToList` 확장 메서드의 비동기 버전이 호출 된 경우

`departments = db.Departments` 문이 아닌 `departments.ToList` 문이 수정 된 이유는 무엇 인가요? 그 이유는 쿼리 또는 명령을 데이터베이스로 전송 하는 문만 비동기적으로 실행 되기 때문입니다. `departments = db.Departments` 문은 쿼리를 설정 하지만 `ToList` 메서드가 호출 될 때까지 쿼리가 실행 되지 않습니다. 따라서 `ToList` 메서드만 비동기적으로 실행 됩니다.

`Details` 메서드와 `HttpGet` `Edit` 및 `Find` `Delete` 메서드에서는 쿼리를 데이터베이스에 전송 하는 데 사용할 수 있는 메서드가 있습니다 .이 메서드는 비동기 방식으로 실행 되는 메서드입니다.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

`Create`, `HttpPost Edit`및 `DeleteConfirmed` 메서드에서는 메모리에서 엔터티를 수정 하는 `db.Departments.Add(department)`와 같은 문이 아니라 명령이 실행 되도록 하는 `SaveChanges` 메서드 호출입니다.

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

*Views\Department\Index.cshtml*를 열고 템플릿 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

이 코드는 제목을 인덱스에서 부서로 변경 하 고, 관리자 이름을 오른쪽으로 이동 하 고, 관리자의 전체 이름을 제공 합니다.

만들기, 삭제, 세부 정보 및 편집 보기에서, 과정 보기에서 부서 이름 필드를 "부서"로 변경한 것과 같은 방식으로 `InstructorID` 필드의 캡션을 "Administrator"로 변경 합니다.

만들기 및 편집 뷰에서는 다음 코드를 사용 합니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

Delete 및 Details 뷰에서는 다음 코드를 사용 합니다.

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

응용 프로그램을 실행 하 고 **부서** 탭을 클릭 합니다.

모든 것이 다른 컨트롤러에서와 동일 하 게 작동 하지만이 컨트롤러에서는 모든 SQL 쿼리가 비동기적으로 실행 됩니다.

Entity Framework와 함께 비동기 프로그래밍을 사용 하는 경우 알아야 할 몇 가지 사항은 다음과 같습니다.

- 비동기 코드는 스레드로부터 안전 하지 않습니다. 즉, 동일한 컨텍스트 인스턴스를 사용 하 여 여러 작업을 병렬로 수행 하지 마세요.
- 비동기 코드의 성능 이점을 활용하려는 경우 사용 중인(예: 페이징) 라이브러리 패키지 또한 쿼리를 데이터베이스에 전송하도록 하는 Entity Framework 메서드를 호출하는 경우 비동기를 사용하는지 확인합니다.

## <a name="use-stored-procedures"></a>저장 프로시저 사용

일부 개발자와 Dba는 데이터베이스 액세스를 위해 저장 프로시저를 사용 하는 것을 선호 합니다. 이전 버전의 Entity Framework에서는 [원시 SQL 쿼리를 실행](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)하 여 저장 프로시저를 사용 하 여 데이터를 검색할 수 있지만 업데이트 작업에 저장 프로시저를 사용 하도록 EF에 지시할 수는 없습니다. EF 6에서 저장 프로시저를 사용 하도록 Code First를 쉽게 구성할 수 있습니다.

1. *DAL\SchoolContext.cs*에서 강조 표시 된 코드를 `OnModelCreating` 메서드에 추가 합니다.

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    이 코드는 `Department` 엔터티에 대 한 삽입, 업데이트 및 삭제 작업에 저장 프로시저를 사용 Entity Framework에 지시 합니다.
2. 패키지 관리 콘솔에서 다음 명령을 입력 합니다.

    `add-migration DepartmentSP`

    *마이그레이션\\&lt;타임 스탬프&gt;\_DepartmentSP.cs* 를 열어 삽입, 업데이트 및 삭제 저장 프로시저를 만드는 `Up` 메서드의 코드를 확인 합니다.

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. 패키지 관리 콘솔에서 다음 명령을 입력 합니다.

     `update-database`
4. 디버그 모드에서 응용 프로그램을 실행 하 고 **부서** 탭을 클릭 한 다음 **새로 만들기**를 클릭 합니다.
5. 새 부서에 대 한 데이터를 입력 한 다음 **만들기**를 클릭 합니다.

6. Visual Studio의 **출력** 창에서 로그를 확인 하 여 저장 프로시저가 새 부서 행을 삽입 하는 데 사용 되었는지 확인 합니다.

     ![부서 삽입 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Code First는 기본 저장 프로시저 이름을 만듭니다. 기존 데이터베이스를 사용 하는 경우 데이터베이스에 이미 정의 된 저장 프로시저를 사용 하기 위해 저장 프로시저 이름을 사용자 지정 해야 할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 자세한 내용은 [Entity Framework Code First 삽입/업데이트/삭제 저장 프로시저](https://msdn.microsoft.com/data/dn468673)를 참조 하세요.

생성 된 저장 프로시저를 사용자 지정 하려면 저장 프로시저를 만드는 마이그레이션 `Up` 메서드에 대 한 스 캐 폴드 코드를 편집 하면 됩니다. 이렇게 하면 마이그레이션이 실행 될 때마다 변경 내용이 반영 되 고 배포 후에 마이그레이션이 자동으로 실행 될 때 프로덕션 데이터베이스에 적용 됩니다.

이전 마이그레이션에서 만든 기존 저장 프로시저를 변경 하려는 경우 추가 마이그레이션 명령을 사용 하 여 빈 마이그레이션을 생성 한 다음 [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) 메서드를 호출 하는 코드를 수동으로 작성할 수 있습니다.

## <a name="deploy-to-azure"></a>Deploy to Azure

이 섹션에서는이 시리즈의 [마이그레이션 및 배포](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) 자습서에서 **Azure에 앱 배포** 섹션을 완료 해야 합니다. 로컬 프로젝트에서 데이터베이스를 삭제 하 여 마이그레이션 오류가 해결 된 경우이 섹션을 건너뜁니다.

1. Visual Studio의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **게시**를 선택합니다.
2. **게시**를 클릭합니다.

    Visual Studio는 Azure에 응용 프로그램을 배포 하 고, 응용 프로그램은 Azure에서 실행 되는 기본 브라우저에서 열립니다.
3. 응용 프로그램을 테스트 하 여 작동 하는지 확인 합니다.

    데이터베이스에 액세스 하는 페이지를 처음 실행 하는 경우 Entity Framework는 현재 데이터 모델을 사용 하 여 데이터베이스를 최신 상태로 만드는 데 필요한 모든 마이그레이션 `Up` 메서드를 실행 합니다. 이제이 자습서에서 추가한 부서 페이지를 포함 하 여 마지막으로 배포한 이후에 추가한 모든 웹 페이지를 사용할 수 있습니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 비동기 코드에 대해 알아보았습니다.
> * 부서 컨트롤러를 만듦
> * 사용 된 저장 프로시저
> * Azure에 배포

여러 사용자가 동시에 동일한 엔터티를 업데이트 하는 경우 충돌을 처리 하는 방법을 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [동시성 처리](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
