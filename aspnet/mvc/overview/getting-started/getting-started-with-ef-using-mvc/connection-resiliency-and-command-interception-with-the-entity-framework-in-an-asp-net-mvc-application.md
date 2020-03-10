---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: '자습서: ASP.NET MVC 앱에서 EF를 사용 하 여 연결 복원 력 및 명령 가로채기 사용'
author: tdykstra
description: 이 자습서에서는 연결 복원 력 및 명령 가로채기를 사용 하는 방법에 대해 알아봅니다. Entity Framework 6의 두 가지 중요 한 기능입니다.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471401"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱에서 Entity Framework와 연결 복원 력 및 명령 가로채기 사용

지금까지 응용 프로그램은 개발 컴퓨터의 IIS Express에서 로컬로 실행 되었습니다. 다른 사용자가 인터넷을 통해 실제 응용 프로그램을 사용할 수 있도록 하려면 웹 호스팅 공급자에 배포 하 고 데이터베이스 서버에 데이터베이스를 배포 해야 합니다.

이 자습서에서는 연결 복원 력 및 명령 가로채기를 사용 하는 방법에 대해 알아봅니다. 이는 클라우드 환경에 배포할 때 특히 중요 한 Entity Framework 6의 중요 한 기능입니다. 연결 복원 력 (일시적 오류에 대 한 자동 재시도) 및 명령 가로채기 (데이터베이스에 전송 된 모든 SQL 쿼리 catch)입니다. 로그 또는 변경 합니다.

이 연결 복원 력 및 명령 가로채기 자습서는 선택 사항입니다. 이 자습서를 건너뛰면 다음 자습서에서 몇 가지 사소한 조정 작업을 수행 해야 합니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 연결 복원 력 사용
> * 명령 가로채기 사용
> * 새 구성 테스트

## <a name="prerequisites"></a>사전 요구 사항

* [정렬, 필터링 및 페이징](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>연결 복원 력 사용

Windows Azure에 응용 프로그램을 배포 하는 경우 데이터베이스를 Windows Azure SQL Database 클라우드 데이터베이스 서비스로 배포 합니다. 일반적으로는 웹 서버와 데이터베이스 서버가 동일한 데이터 센터에서 직접 연결 되는 경우를 제외 하 고는 클라우드 데이터베이스 서비스에 연결 하는 경우 일시적 연결 오류가 더 자주 발생 합니다. 클라우드 웹 서버와 클라우드 데이터베이스 서비스가 동일한 데이터 센터에서 호스트 되는 경우에도 부하 분산 장치와 같은 문제가 발생할 수 있는 네트워크 연결 사이에 더 많은 네트워크 연결이 있습니다.

또한 클라우드 서비스는 일반적으로 다른 사용자가 공유 하 여 응답성이 영향을 받을 수 있음을 의미 합니다. 데이터베이스에 대 한 액세스는 제한 될 수 있습니다. 제한은 Service Level Agreement(서비스 수준 약정) (SLA)에서 허용 하는 것 보다 더 자주 액세스 하려고 할 때 데이터베이스 서비스에서 예외를 throw 하는 것을 의미 합니다.

클라우드 서비스에 액세스할 때 발생 하는 대부분의 연결 문제는 일시적입니다. 즉, 짧은 시간에 자체적으로 해결 됩니다. 따라서 데이터베이스 작업을 시도 하 고 일반적으로 일시적인 오류 유형을 가져오는 경우 잠시 대기 후 작업을 다시 시도 하 고 작업이 성공할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 게 훨씬 더 나은 환경을 제공할 수 있습니다. 이러한 작업은 대부분 고객에 게 표시 되지 않습니다. Entity Framework 6의 연결 복원 력 기능은 실패 한 SQL 쿼리를 다시 시도 하는 프로세스를 자동화 합니다.

특정 데이터베이스 서비스에 대해 연결 복원 기능을 적절 하 게 구성 해야 합니다.

- 일시적으로 발생할 수 있는 예외를 알아야 합니다. 예를 들어 프로그램 버그로 인 한 오류가 아닌 네트워크 연결의 일시적인 손실로 인 한 오류를 다시 시도 하려고 합니다.
- 실패 한 작업 다시 시도 사이에 적절 한 시간 동안 기다려야 합니다. 사용자가 응답을 대기 하는 온라인 웹 페이지에 비해 일괄 처리 프로세스에 대 한 재시도 사이에서 더 오래 기다릴 수 있습니다.
- 이를 위해서는 적절 한 횟수 만큼 다시 시도해 야 합니다. 온라인 응용 프로그램에서 원하는 일괄 처리 프로세스에서 더 많은 시간을 다시 시도할 수 있습니다.

Entity Framework 공급자가 지 원하는 모든 데이터베이스 환경에 대해 이러한 설정을 수동으로 구성할 수 있지만 일반적으로 Windows Azure SQL Database를 사용 하는 온라인 응용 프로그램에서 잘 작동 하는 기본값은 이미 구성 되어 있습니다. 이러한 설정은 Contoso 대학 응용 프로그램에 대해 구현 하는 설정입니다.

연결 복원 력을 사용 하도록 설정 하려면 [Dbconfiguration](https://msdn.microsoft.com/data/jj680699.aspx) 클래스에서 파생 되는 어셈블리에 클래스를 만들고, 해당 클래스에서 SQL Database *실행 전략*을 설정 합니다. 즉, EF에서 *재시도 정책*에 대 한 다른 용어를 사용 합니다.

1. DAL 폴더에 *SchoolConfiguration.cs*라는 클래스 파일을 추가 합니다.
2. 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Entity Framework은 `DbConfiguration`에서 파생 되는 클래스에서 발견 되는 코드를 자동으로 실행 합니다. `DbConfiguration` 클래스를 사용 하 여 *web.config 파일에서* 다른 방법으로 수행 하는 구성 작업을 코드에서 수행할 수 있습니다. 자세한 내용은 [Entityframework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)을 참조 하세요.
3. *StudentController.cs*에서 `System.Data.Entity.Infrastructure`에 대 한 `using` 문을 추가 합니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. 대신 `RetryLimitExceededException` 예외를 catch 하도록 `DataException` 예외를 catch 하는 모든 `catch` 블록을 변경 합니다. 다음은 그 예입니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    `DataException`를 사용 하 여 친숙 한 "다시 시도" 메시지를 제공 하기 위해 일시적일 수 있는 오류를 식별 하려고 했습니다. 하지만 이제 다시 시도 정책을 설정 했으므로 일시적으로 발생 하는 오류는 이미 시도 되었고 여러 번 실패 한 경우 반환 되는 실제 예외는 `RetryLimitExceededException` 예외에 래핑됩니다.

자세한 내용은 [Entity Framework 연결 복원 력/재시도 논리](https://msdn.microsoft.com/data/dn456835)를 참조 하세요.

## <a name="enable-command-interception"></a>명령 가로채기 사용

이제 다시 시도 정책을 설정 했으므로 테스트 하 여 예상 대로 작동 하는지 확인 하는 방법을 확인 해야 합니다. 특히 로컬에서 실행 하는 경우 일시적 오류가 발생 하는 것은 쉽지 않으며, 실제 일시적인 오류를 자동화 된 단위 테스트에 통합 하는 것이 특히 어렵습니다. 연결 복원 력 기능을 테스트 하려면 Entity Framework SQL Server으로 보내고 SQL Server 응답을 일반적으로 일시적인 예외 형식으로 바꾸는 쿼리를 가로챌 수 있는 방법이 필요 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하기 위해 쿼리 가로채기를 사용할 수도 있습니다. 데이터베이스 서비스와 같은 [외부 서비스에 대 한 모든 호출의 대기 시간 및 성공 또는 실패를 기록 합니다](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) . EF6는 로깅을 용이 하 게 할 수 있는 [전용 로깅 API](https://msdn.microsoft.com/data/dn469464) 를 제공 하지만 자습서의이 섹션에서는 로깅 및 일시적인 오류 시뮬레이션 모두에서 Entity Framework의 [가로채기 기능](https://msdn.microsoft.com/data/dn469464) 을 직접 사용 하는 방법을 알아봅니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

로깅을 사용 하는 [가장 좋은 방법은](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) 진단 또는 로깅 클래스를 하드 코딩 하는 대신 인터페이스를 사용 하 여 수행 하는 것입니다. 이렇게 하면 나중에이 작업을 수행 해야 하는 경우 로깅 메커니즘을 보다 쉽게 변경할 수 있습니다. 따라서이 섹션에서는 로깅 인터페이스와이 인터페이스를 구현 하는 클래스를 만듭니다. >

1. 프로젝트에 폴더를 만들고 이름을 *Logging*으로 만듭니다.
2. *로깅* 폴더에서 *ILogger.cs*라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    인터페이스는 로그의 상대적인 중요도를 나타내는 세 가지 추적 수준과 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 디자인 된 추적 수준을 제공 합니다. 로깅 메서드에는 예외를 전달할 수 있는 오버 로드가 있습니다. 이는 응용 프로그램의 각 로깅 메서드 호출에서 수행 되는 작업을 수행 하는 대신, 스택 추적 및 내부 예외를 포함 하는 예외 정보를 인터페이스를 구현 하는 클래스에서 안정적으로 기록 하는 것입니다.

    TraceApi 메서드를 사용 하면 SQL Database와 같은 외부 서비스에 대 한 각 호출의 대기 시간을 추적할 수 있습니다.
3. *로깅* 폴더에서 *Logger.cs*라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    구현에서는 시스템 진단을 사용 하 여 추적을 수행 합니다. 이는 추적 정보를 쉽게 생성 하 고 사용할 수 있도록 하는 .NET의 기본 제공 기능입니다. 파일에 로그를 기록 하거나 (예:) Azure에서 blob 저장소에 기록 하는 데 사용할 수 있는 "수신기"가 많이 있습니다. 자세한 내용은 [Visual Studio의 Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)에서 일부 옵션 및 기타 리소스에 대 한 링크를 참조 하세요. 이 자습서에서는 Visual Studio **출력** 창 에서만 로그를 확인 합니다.

    프로덕션 응용 프로그램에서는 시스템 진단과 다른 패키지를 추적 하는 것이 좋습니다. ILogger 인터페이스를 사용 하면이 작업을 수행 하기로 결정 한 경우 다른 추적 메커니즘으로 비교적 쉽게 전환할 수 있습니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음에는 데이터베이스에 쿼리를 보낼 때마다 호출 되는 Entity Framework 클래스를 만듭니다. 하나는 일시적인 오류를 시뮬레이션 하 고 다른 하나는 로깅을 수행 합니다. 이러한 인터셉터 클래스는 `DbCommandInterceptor` 클래스에서 파생 되어야 합니다. 쿼리에서 쿼리가 실행 될 때 자동으로 호출 되는 메서드 재정의를 작성 합니다. 이러한 방법으로 데이터베이스에 전송 되는 쿼리를 검사 하거나 로깅할 수 있으며, 쿼리를 데이터베이스로 전달 하기 전에 쿼리를 변경 하거나 데이터베이스에 전송 하기 전에 쿼리를 변경 하 여 Entity Framework 수 있습니다.

1. 데이터베이스로 전송 되는 모든 SQL 쿼리를 기록 하는 인터셉터 클래스를 만들려면 *DAL* 폴더에 *SchoolInterceptorLogging.cs* 라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    성공 쿼리 또는 명령의 경우이 코드는 대기 시간 정보와 함께 정보 로그를 작성 합니다. 예외에 대해 오류 로그를 만듭니다.
2. **검색** 상자에 "Throw"를 입력할 때 더미 일시적인 오류를 생성 하는 인터셉터 클래스를 만들려면 *DAL* 폴더에 *SchoolInterceptorTransientErrors.cs* 라는 클래스 파일을 만들고 템플릿 코드를 다음 코드로 바꿉니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    이 코드는 여러 행의 데이터를 반환할 수 있는 쿼리에 대해 호출 되는 `ReaderExecuting` 메서드만 재정의 합니다. 다른 형식의 쿼리에 대 한 연결 복원 력을 확인 하려면 로깅 인터셉터와 마찬가지로 `NonQueryExecuting` 및 `ScalarExecuting` 메서드를 재정의할 수도 있습니다.

    학생 페이지를 실행 하 고 검색 문자열로 "Throw"를 입력 하는 경우이 코드는 일반적으로 일시적으로 알려진 형식인 오류 번호 20에 대 한 더미 SQL Database 예외를 만듭니다. 현재 일시적인 것으로 인식 되는 기타 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 및 40613 이지만 SQL Database의 새 버전에서 변경 될 수 있습니다.

    이 코드는 쿼리를 실행 하 고 쿼리 결과를 다시 전달 하는 대신 Entity Framework 하는 예외를 반환 합니다. 임시 예외는 네 번 반환 된 다음 쿼리를 데이터베이스에 전달 하는 일반적인 절차로 되돌아갑니다.

    모든 항목이 기록 되기 때문에, Entity Framework에서 쿼리를 실행 하는 데 마지막으로 실행을 시도 하는 것을 확인할 수 있으며, 응용 프로그램의 유일한 차이점은 쿼리 결과가 포함 된 페이지를 렌더링 하는 데 시간이 더 오래 걸리기 때문입니다.

    Entity Framework을 다시 시도 하는 횟수는 구성 가능 합니다. 이 코드는 SQL Database 실행 정책에 대 한 기본값 이므로 네 번 지정 합니다. 실행 정책을 변경 하면 일시적인 오류가 생성 되는 횟수를 지정 하는 코드도 여기에서 변경 됩니다. Entity Framework에서 `RetryLimitExceededException` 예외를 throw 하도록 코드를 변경 하 여 더 많은 예외를 생성할 수도 있습니다.

    검색 상자에 입력 하는 값은 `command.Parameters[0]` 및 `command.Parameters[1]`에 있습니다. 하나는 이름에 사용 되 고, 다른 하나는 이름으로 사용 됩니다. 값 "% Throw%"가 발견 되 면 일부 학생이 검색 되어 반환 될 수 있도록 "Throw"가 해당 매개 변수에서 "a"로 바뀝니다.

    응용 프로그램 UI에 대 한 일부 입력을 변경 하는 방법에 따라 연결 복원 력을 테스트 하는 편리한 방법일 뿐입니다. 또한 *Dbinterception. Add* 메서드에 대 한 주석 뒷부분에 설명 된 대로 모든 쿼리 또는 업데이트에 대 한 일시적인 오류를 생성 하는 코드를 작성할 수도 있습니다.
3. Global.asax *에서 다음*`using` 문을 추가 합니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. `Application_Start` 메서드에 강조 표시 된 줄을 추가 합니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    이러한 코드 줄은 Entity Framework 데이터베이스에 쿼리를 보낼 때 인터셉터 코드를 실행 하는 데 발생 합니다. 일시적인 오류 시뮬레이션 및 로깅에 대 한 별도의 인터셉터 클래스를 만들었으므로 독립적으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

    코드의 아무 곳에서 나 `DbInterception.Add` 메서드를 사용 하 여 인터셉터를 추가할 수 있습니다. `Application_Start` 메서드에 있을 필요는 없습니다. 또 다른 옵션은 이전에 실행 정책을 구성 하기 위해 만든 DbConfiguration 클래스에이 코드를 배치 하는 것입니다.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    이 코드를 배치할 때마다 동일한 인터셉터에 대 한 `DbInterception.Add`를 두 번 이상 실행 하지 않도록 주의 하거나 추가 인터셉터 인스턴스를 가져옵니다. 예를 들어 로깅 인터셉터를 두 번 추가 하면 모든 SQL 쿼리에 대해 두 개의 로그가 표시 됩니다.

    인터셉터는 등록 순서 (`DbInterception.Add` 메서드가 호출 되는 순서)로 실행 됩니다. 이 순서는 인터셉터에서 수행 하는 작업에 따라 달라질 수 있습니다. 예를 들어 인터셉터는 `CommandText` 속성에서 가져오는 SQL 명령을 변경할 수 있습니다. SQL 명령을 변경 하는 경우 다음 인터셉터는 원래 SQL 명령이 아닌 변경 된 SQL 명령을 가져옵니다.

    UI에 다른 값을 입력 하 여 일시적인 오류를 발생 시킬 수 있는 방법으로 일시적인 오류 시뮬레이션 코드를 작성 했습니다. 다른 방법으로, 특정 매개 변수 값을 확인 하지 않고 항상 일시적인 예외 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에만 인터셉터를 추가할 수 있습니다. 그러나이 작업을 수행 하는 경우에는 데이터베이스 초기화가 완료 될 때까지 인터셉터를 추가 하지 마세요. 즉, 임시 오류 생성을 시작 하기 전에 엔터티 집합 중 하나에 대 한 쿼리와 같은 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework는 데이터베이스 초기화 중에 여러 쿼리를 실행 하 고 트랜잭션에서 실행 되지 않으므로 초기화 하는 동안 오류가 발생 하면 컨텍스트가 일관 되지 않은 상태가 될 수 있습니다.

## <a name="test-the-new-configuration"></a>새 구성 테스트

1. **F5** 키를 눌러 디버그 모드에서 응용 프로그램을 실행 한 다음 **학생** 탭을 클릭 합니다.
2. Visual Studio **출력** 창을 살펴보면 추적 출력을 볼 수 있습니다. 로 거에 의해 기록 된 로그를 가져오려면 일부 JavaScript 오류를 이전에 스크롤해야 할 수 있습니다.

    데이터베이스에 전송 된 실제 SQL 쿼리를 볼 수 있습니다. 시작 하 고 데이터베이스 버전 및 마이그레이션 기록 테이블을 확인 하는 Entity Framework 몇 가지 초기 쿼리 및 명령이 표시 됩니다 (다음 자습서의 마이그레이션에 대해 알아봅니다). 페이징에 대 한 쿼리를 보고, 학생 수를 확인 하 고, 마지막으로 학생 데이터를 가져오는 쿼리를 볼 수 있습니다.

    ![일반 쿼리에 대 한 로깅](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. **학생** 페이지에서 검색 문자열로 "Throw"를 입력 하 고 **검색**을 클릭 합니다.

    ![검색 문자열 Throw](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Entity Framework 쿼리를 여러 번 다시 시도 하는 동안 브라우저가 몇 초 동안 중단 된 것 처럼 보입니다. 첫 번째 다시 시도는 매우 신속 하 게 발생 하며, 다시 시도 하기 전에 대기가 늘어납니다. 다시 시도 하기 전에 대기 하는이 프로세스를 *지 수 백오프*라고 합니다.

    페이지가 표시 되 면 이름에 "a"가 있는 학생을 표시 하 고, 출력 창을 보면 동일한 쿼리가 5 번 시도 되었음을 알 수 있으며, 처음 네 번은 일시적 예외가 반환 됩니다. 각 일시적 오류에 대해 `SchoolInterceptorTransientErrors` 클래스에서 일시적인 오류를 생성할 때 작성 하는 로그가 표시 됩니다 ("명령에 대 한 임시 오류 반환"). `SchoolInterceptorLogging` 예외를 발생 하면 기록 된 로그가 표시 됩니다.

    ![재시도를 표시 하는 로깅 출력](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    검색 문자열을 입력 한 후에는 학생 데이터를 반환 하는 쿼리를 매개 변수화 합니다.

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    매개 변수 값을 로깅하지는 않지만 그렇게 할 수 있습니다. 매개 변수 값을 확인 하려는 경우 인터셉터 메서드에서 가져오는 `DbCommand` 개체의 `Parameters` 속성에서 매개 변수 값을 가져오는 로깅 코드를 작성할 수 있습니다.

    응용 프로그램을 중지 하 고 다시 시작 하지 않으면이 테스트를 반복할 수 없습니다. 응용 프로그램을 한 번 실행 하 여 연결 복원 력을 여러 번 테스트할 수 있게 하려는 경우 `SchoolInterceptorTransientErrors`에서 오류 카운터를 다시 설정 하는 코드를 작성할 수 있습니다.
4. 실행 전략 (다시 시도 정책)의 차이점을 확인 하려면 *SchoolConfiguration.cs*의 `SetExecutionStrategy` 줄을 주석으로 처리 하 고, 디버그 모드에서 학생 페이지를 다시 실행 하 고, "Throw"를 다시 검색 합니다.

    이번에는 처음 생성 된 예외에서 디버거가 처음으로 쿼리를 실행 하려고 할 때 즉시 디버거가 중지 됩니다.

    ![더미 예외](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. *SchoolConfiguration.cs*에서 *setexecutionstrategy* 줄의 주석 처리를 제거 합니다.

## <a name="get-the-code"></a>코드 가져오기

[완료 된 프로젝트 다운로드](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 데이터 액세스-권장 리소스](../../../../whitepapers/aspnet-data-access-content-map.md)에서 다른 Entity Framework 리소스에 대 한 링크를 찾을 수 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 연결 복원 력 사용
> * 사용 하도록 설정 된 명령 가로채기
> * 새 구성 테스트

Code First 마이그레이션 및 Azure 배포에 대해 자세히 알아보려면 다음 문서로 이동 합니다.
> [!div class="nextstepaction"]
> [Code First 마이그레이션 및 Azure 배포](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
