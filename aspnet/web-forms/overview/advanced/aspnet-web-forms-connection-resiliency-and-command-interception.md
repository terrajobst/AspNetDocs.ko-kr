---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web Forms 연결 복원 력 및 명령 가로채기 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 연결 복원 력 및 명령 가로채기를 지원 하도록 샘플 응용 프로그램을 수정 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484235"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web Forms 연결 복원력 및 명령 인터셉션

[Erik Reitan](https://github.com/Erikre)

이 자습서에서는 연결 복원 력 및 명령 가로채기를 지원 하도록 정문 장난감 샘플 응용 프로그램을 수정 합니다. 연결 복원 력을 사용 하도록 설정 하면 클라우드 환경의 일반적인 오류가 발생할 때 정문 장난감 샘플 응용 프로그램에서 자동으로 데이터 호출을 다시 시도 합니다. 또한, 명령 가로채기를 구현 하 여 정문 장난감 샘플 응용 프로그램은 데이터베이스에 전송 된 모든 SQL 쿼리를 catch 하 여 로그 또는 변경 합니다.

> [!NOTE] 
> 
> 이 Web Forms 자습서는 Tom Dykstra의 다음 MVC 자습서를 기반으로 합니다.  
> [ASP.NET MVC 응용 프로그램의 Entity Framework 연결 복원 력 및 명령 가로채기](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>학습할 내용:

- 연결 복원 력을 제공 하는 방법
- 명령 가로채기를 구현 하는 방법입니다.

## <a name="prerequisites"></a>사전 요구 사항

시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) 또는 [Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework 자동으로 설치 됩니다.
- 정문 장난감 샘플 프로젝트에서이 자습서에 언급 된 기능을 구현할 수 있습니다. 다음 링크에서 다운로드 세부 정보를 제공 합니다.

    - [ASP.NET 4.5.1 Web Forms 시작-정문 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- 이 자습서를 완료 하기 전에 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)관련 자습서 시리즈를 검토 하는 것이 좋습니다. 자습서 시리즈는 **WingtipToys** 프로젝트 및 코드를 익히는 데 도움이 됩니다.

## <a name="connection-resiliency"></a>연결 복원력

Windows Azure에 응용 프로그램을 배포 하는 것을 고려 하는 경우, **windows** **Azure SQL Database**에 데이터베이스를 배포 하는 것이 좋습니다. 일반적으로는 웹 서버와 데이터베이스 서버가 동일한 데이터 센터에서 직접 연결 되는 경우를 제외 하 고는 클라우드 데이터베이스 서비스에 연결 하는 경우 일시적 연결 오류가 더 자주 발생 합니다. 클라우드 웹 서버와 클라우드 데이터베이스 서비스가 동일한 데이터 센터에서 호스트 되는 경우에도 부하 분산 장치와 같은 문제가 발생할 수 있는 네트워크 연결 사이에 더 많은 네트워크 연결이 있습니다.

또한 클라우드 서비스는 일반적으로 다른 사용자가 공유 하 여 응답성이 영향을 받을 수 있음을 의미 합니다. 데이터베이스에 대 한 액세스는 제한 될 수 있습니다. 제한은 *Service Level Agreement(서비스 수준 약정)* (SLA)에서 허용 하는 것 보다 더 자주 액세스 하려고 할 때 데이터베이스 서비스에서 예외를 throw 하는 것을 의미 합니다.

클라우드 서비스에 액세스할 때 발생 하는 대부분의 연결 문제는 일시적입니다. 즉, 짧은 시간에 자체적으로 해결 됩니다. 따라서 데이터베이스 작업을 시도 하 고 일반적으로 일시적인 오류 유형을 가져오는 경우 잠시 대기 후 작업을 다시 시도 하 고 작업이 성공할 수 있습니다. 자동으로 다시 시도 하 여 일시적인 오류를 처리 하는 경우 사용자에 게 훨씬 더 나은 환경을 제공할 수 있습니다. 이러한 작업은 대부분 고객에 게 표시 되지 않습니다. Entity Framework 6의 연결 복원 력 기능은 실패 한 SQL 쿼리를 다시 시도 하는 프로세스를 자동화 합니다.

특정 데이터베이스 서비스에 대해 연결 복원 기능을 적절 하 게 구성 해야 합니다.

1. 일시적으로 발생할 수 있는 예외를 알아야 합니다. 예를 들어 프로그램 버그로 인 한 오류가 아닌 네트워크 연결의 일시적인 손실로 인 한 오류를 다시 시도 하려고 합니다.
2. 실패 한 작업 다시 시도 사이에 적절 한 시간 동안 기다려야 합니다. 사용자가 응답을 대기 하는 온라인 웹 페이지에 비해 일괄 처리 프로세스에 대 한 재시도 사이에서 더 오래 기다릴 수 있습니다.
3. 이를 위해서는 적절 한 횟수 만큼 다시 시도해 야 합니다. 온라인 응용 프로그램에서 원하는 일괄 처리 프로세스에서 더 많은 시간을 다시 시도할 수 있습니다.

Entity Framework 공급자가 지 원하는 모든 데이터베이스 환경에 대해 이러한 설정을 수동으로 구성할 수 있습니다.

연결 복원 력을 사용 하도록 설정 하는 것은 `DbConfiguration` 클래스에서 파생 되는 어셈블리에 클래스를 만들고, 해당 클래스에서 Entity Framework 다시 시도 정책에 대 한 다른 용어를 설정 하는 SQL Database 실행 전략을 설정 하는 것입니다.

### <a name="implementing-connection-resiliency"></a>연결 복원 력 구현

1. [WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) 샘플 Web Forms 응용 프로그램을 다운로드 하 여 Visual Studio에서 엽니다.
2. **WingtipToys** 응용 프로그램의 *논리* 폴더에서 *WingtipToysConfiguration.cs*라는 클래스 파일을 추가 합니다.
3. 기존 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

Entity Framework은 `DbConfiguration`에서 파생 되는 클래스에서 발견 되는 코드를 자동으로 실행 합니다. `DbConfiguration` 클래스를 사용 하 여 *web.config 파일에서* 다른 방법으로 수행 하는 구성 작업을 코드에서 수행할 수 있습니다. 자세한 내용은 [Entityframework 코드 기반 구성](https://msdn.microsoft.com/data/jj680699)을 참조 하세요.

1. *논리* 폴더에서 *AddProducts.cs* 파일을 엽니다.
2. 노란색으로 강조 표시 된 것 처럼 `System.Data.Entity.Infrastructure`에 대 한 `using` 문을 추가 합니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. `AddProduct` 메서드에 `catch` 블록을 추가 하 여 `RetryLimitExceededException` 노란색으로 강조 표시 된 대로 기록 되도록 합니다.   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

`RetryLimitExceededException` 예외를 추가 하 여 더 나은 로깅을 제공 하거나 사용자에 게 프로세스를 다시 시도 하도록 선택할 수 있는 오류 메시지를 표시할 수 있습니다. `RetryLimitExceededException` 예외를 catch 하 여 일시적일 가능성이 있는 유일한 오류는 이미 시도 되었고 여러 번 실패 했습니다. 반환 되는 실제 예외는 `RetryLimitExceededException` 예외에 래핑됩니다. 또한 일반 catch 블록을 추가 했습니다. `RetryLimitExceededException` 예외에 대 한 자세한 내용은 [Entity Framework 연결 복원 력/재시도 논리](https://msdn.microsoft.com/data/dn456835)를 참조 하세요.

## <a name="command-interception"></a>명령 가로채기

이제 다시 시도 정책을 설정 했으므로 테스트 하 여 예상 대로 작동 하는지 확인 하는 방법을 확인 해야 합니다. 특히 로컬에서 실행 하는 경우 일시적 오류가 발생 하는 것은 쉽지 않으며, 실제 일시적인 오류를 자동화 된 단위 테스트에 통합 하는 것이 특히 어렵습니다. 연결 복원 력 기능을 테스트 하려면 Entity Framework SQL Server으로 보내고 SQL Server 응답을 일반적으로 일시적인 예외 형식으로 바꾸는 쿼리를 가로챌 수 있는 방법이 필요 합니다.

클라우드 응용 프로그램에 대 한 모범 사례를 구현 하기 위해 쿼리 가로채기를 사용할 수도 있습니다. 데이터베이스 서비스와 같은 외부 서비스에 대 한 모든 호출의 대기 시간 및 성공 또는 실패를 기록 합니다.

자습서의이 섹션에서는 로깅 및 일시적인 오류 시뮬레이션 모두에 Entity Framework의 [*가로채기 기능*](https://msdn.microsoft.com/data/dn469464) 을 사용 합니다.

### <a name="create-a-logging-interface-and-class"></a>로깅 인터페이스 및 클래스 만들기

로깅을 사용 하는 가장 좋은 방법은 `System.Diagnostics.Trace` 또는 로깅 클래스에 대해 하드 코딩 하는 대신 [`interface`](https://msdn.microsoft.com/library/ms173156.aspx) 를 사용 하 여 수행 하는 것입니다. 이렇게 하면 나중에이 작업을 수행 해야 하는 경우 로깅 메커니즘을 보다 쉽게 변경할 수 있습니다. 따라서이 섹션에서는 로깅 인터페이스와이 인터페이스를 구현 하는 클래스를 만듭니다.

위의 절차에 따라 Visual Studio에서 **WingtipToys** 샘플 응용 프로그램을 다운로드 하 여 열었습니다.

1. **WingtipToys** 프로젝트에서 폴더를 만들고이 폴더에 *로깅*이름을로 합니다.
2. *로깅* 폴더에서 *ILogger.cs* 라는 클래스 파일을 만들고 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   인터페이스는 로그의 상대적인 중요도를 나타내는 세 가지 추적 수준과 데이터베이스 쿼리와 같은 외부 서비스 호출에 대 한 대기 시간 정보를 제공 하도록 디자인 된 추적 수준을 제공 합니다. 로깅 메서드에는 예외를 전달할 수 있는 오버 로드가 있습니다. 이는 응용 프로그램의 각 로깅 메서드 호출에서 수행 되는 작업을 수행 하는 대신, 스택 추적 및 내부 예외를 포함 하는 예외 정보를 인터페이스를 구현 하는 클래스에서 안정적으로 기록 하는 것입니다.  
  
   `TraceApi` 메서드를 사용 하 여 SQL Database와 같은 외부 서비스에 대 한 각 호출의 대기 시간을 추적할 수 있습니다.
3. *로깅* 폴더에서 *Logger.cs* 라는 클래스 파일을 만들고 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

구현에서는 `System.Diagnostics`를 사용 하 여 추적을 수행 합니다. 이는 추적 정보를 쉽게 생성 하 고 사용할 수 있도록 하는 .NET의 기본 제공 기능입니다. 파일에 로그를 기록 하는 데 사용 하거나 Windows Azure에서 blob 저장소에 기록 하는 데 `System.Diagnostics` 사용할 수 있는 많은 &quot;수신기&quot; 있습니다. 자세한 내용은 [Visual Studio의 Microsoft Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)에서 일부 옵션 및 기타 리소스에 대 한 링크를 참조 하세요. 이 자습서에서는 Visual Studio **출력** 창 에서만 로그를 확인 합니다.

프로덕션 응용 프로그램에서는 `System.Diagnostics`아닌 추적 프레임 워크를 사용 하는 것이 좋습니다. `ILogger` 인터페이스를 사용 하 여이 작업을 수행 하기로 결정 한 경우에는 다른 추적 메커니즘으로 비교적 쉽게 전환할 수 있습니다.

### <a name="create-interceptor-classes"></a>인터셉터 클래스 만들기

다음에는 데이터베이스에 쿼리를 보낼 때마다 Entity Framework 호출 하는 클래스를 만듭니다. 하나는 일시적인 오류를 시뮬레이션 하 고 다른 하나는 로깅을 수행 합니다. 이러한 인터셉터 클래스는 `DbCommandInterceptor` 클래스에서 파생 되어야 합니다. 쿼리가 실행 될 때 자동으로 호출 되는 메서드 재정의를 작성 합니다. 이러한 방법으로 데이터베이스에 전송 되는 쿼리를 검사 하거나 로깅할 수 있으며, 쿼리를 데이터베이스로 전달 하기 전에 쿼리를 변경 하거나 데이터베이스에 전송 하기 전에 쿼리를 변경 하 여 Entity Framework 수 있습니다.

1. 데이터베이스로 전송 되기 전에 모든 SQL 쿼리를 기록 하는 인터셉터 클래스를 만들려면 *논리* 폴더에 *InterceptorLogging.cs* 라는 클래스 파일을 만들고 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   성공 쿼리 또는 명령의 경우이 코드는 대기 시간 정보와 함께 정보 로그를 작성 합니다. 예외에 대해 오류 로그를 만듭니다.
2. InterceptorTransientErrors.cs 라는 페이지의 **이름** 텍스트 상자에&quot; Throw *&quot;를 입력*하면 더미 일시적 오류를 생성 하는 인터셉터 클래스를 만들려면 *논리* 폴더에 라는 클래스 파일을 만들고 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    이 코드는 여러 행의 데이터를 반환할 수 있는 쿼리에 대해 호출 되는 `ReaderExecuting` 메서드만 재정의 합니다. 다른 형식의 쿼리에 대 한 연결 복원 력을 확인 하려면 로깅 인터셉터와 마찬가지로 `NonQueryExecuting` 및 `ScalarExecuting` 메서드를 재정의할 수도 있습니다.  
  
   나중에 "관리자"로 로그인 하 고 위쪽 탐색 모음에서 **관리자** 링크를 선택 합니다. 그런 다음 *adminpage .aspx* 페이지에서&quot;Throw &quot;라는 제품을 추가 합니다. 이 코드는 일반적으로 일시적으로 알려진 형식인 오류 번호 20에 대 한 더미 SQL Database 예외를 만듭니다. 현재 일시적인 것으로 인식 되는 기타 오류 번호는 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 및 40613 이지만 SQL Database의 새 버전에서 변경 될 수 있습니다. 제품의 이름이 "TransientErrorExample"로 바뀌고이는 *InterceptorTransientErrors.cs* 파일의 코드에서 수행할 수 있습니다.  
  
   이 코드는 쿼리를 실행 하 고 결과를 전달 하는 대신 Entity Framework 하는 예외를 반환 합니다. 임시 예외는 *네* 번 반환 된 다음 쿼리를 데이터베이스에 전달 하는 일반적인 절차로 되돌아갑니다.

    모든 항목이 기록 되기 때문에, Entity Framework에서 쿼리를 실행 하는 데 마지막으로 실행을 시도 하는 것을 확인할 수 있으며, 응용 프로그램의 유일한 차이점은 쿼리 결과가 포함 된 페이지를 렌더링 하는 데 시간이 더 오래 걸리기 때문입니다.  
  
   Entity Framework을 다시 시도 하는 횟수는 구성 가능 합니다. 이 코드는 SQL Database 실행 정책에 대 한 기본값 이므로 네 번 지정 합니다. 실행 정책을 변경 하면 일시적인 오류가 생성 되는 횟수를 지정 하는 코드도 여기에서 변경 됩니다. Entity Framework에서 `RetryLimitExceededException` 예외를 throw 하도록 코드를 변경 하 여 더 많은 예외를 생성할 수도 있습니다.
3. Global.asax *에서 다음*using 문을 추가 합니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 그런 다음 `Application_Start` 메서드에 강조 표시 된 줄을 추가 합니다.  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

이러한 코드 줄은 Entity Framework 데이터베이스에 쿼리를 보낼 때 인터셉터 코드를 실행 하는 데 발생 합니다. 일시적인 오류 시뮬레이션 및 로깅에 대 한 별도의 인터셉터 클래스를 만들었으므로 독립적으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다.   
  
 코드의 아무 곳에서 나 `DbInterception.Add` 메서드를 사용 하 여 인터셉터를 추가할 수 있습니다. `Application_Start` 메서드에 있을 필요는 없습니다. 또 다른 옵션은 `Application_Start` 메서드에 인터셉터를 추가 하지 않은 경우 *WingtipToysConfiguration.cs* 라는 클래스를 업데이트 하거나 추가 하 고 위의 코드를 `WingtipToysConfiguration` 클래스 생성자의 끝에 배치 하는 것입니다.

이 코드를 배치할 때마다 동일한 인터셉터에 대 한 `DbInterception.Add`를 두 번 이상 실행 하지 않도록 주의 하거나 추가 인터셉터 인스턴스를 가져옵니다. 예를 들어 로깅 인터셉터를 두 번 추가 하면 모든 SQL 쿼리에 대해 두 개의 로그가 표시 됩니다.

인터셉터는 등록 순서 (`DbInterception.Add` 메서드가 호출 되는 순서)로 실행 됩니다. 이 순서는 인터셉터에서 수행 하는 작업에 따라 달라질 수 있습니다. 예를 들어 인터셉터는 `CommandText` 속성에서 가져오는 SQL 명령을 변경할 수 있습니다. SQL 명령을 변경 하는 경우 다음 인터셉터는 원래 SQL 명령이 아닌 변경 된 SQL 명령을 가져옵니다.

UI에 다른 값을 입력 하 여 일시적인 오류를 발생 시킬 수 있는 방법으로 일시적인 오류 시뮬레이션 코드를 작성 했습니다. 다른 방법으로, 특정 매개 변수 값을 확인 하지 않고 항상 일시적인 예외 시퀀스를 생성 하는 인터셉터 코드를 작성할 수 있습니다. 그런 다음 일시적인 오류를 생성 하려는 경우에만 인터셉터를 추가할 수 있습니다. 그러나이 작업을 수행 하는 경우에는 데이터베이스 초기화가 완료 될 때까지 인터셉터를 추가 하지 마세요. 즉, 임시 오류 생성을 시작 하기 전에 엔터티 집합 중 하나에 대 한 쿼리와 같은 하나 이상의 데이터베이스 작업을 수행 합니다. Entity Framework는 데이터베이스 초기화 중에 여러 쿼리를 실행 하 고 트랜잭션에서 실행 되지 않으므로 초기화 하는 동안 오류가 발생 하면 컨텍스트가 일관 되지 않은 상태가 될 수 있습니다.

## <a name="test-logging-and-connection-resiliency"></a>테스트 로깅 및 연결 복원 력

1. Visual Studio에서 **f5** 키를 눌러 디버그 모드에서 응용 프로그램을 실행 한 다음 "Pa $ $word"를 암호로 사용 하 여 "Admin"으로 로그인 합니다.
2. 위쪽의 탐색 모음에서 **관리자** 를 선택 합니다.
3. 적절 한 설명, 가격 및 이미지 파일을 포함 하는 "Throw" 라는 새 제품을 입력 합니다.
4. **제품 추가** 단추를 누릅니다.  
   Entity Framework 쿼리를 여러 번 다시 시도 하는 동안 브라우저가 몇 초 동안 중단 된 것 처럼 보입니다. 첫 번째 다시 시도는 매우 신속 하 게 수행 된 후에 다시 시도 하기 전에 대기가 늘어납니다. 다시 시도 하기 전에 대기 하는이 프로세스를 *지 수 백오프* 라고 합니다.
5. 페이지를 더 이상 로드 하지 않을 때까지 기다립니다.
6. 프로젝트를 중지 하 고 Visual Studio **출력** 창을 살펴보면 추적 출력을 볼 수 있습니다. **디버그** -&gt; **Windows** -&gt; **출력**을 선택 하 여 **출력** 창을 찾을 수 있습니다. 로 거에 의해 기록 된 다른 여러 로그를 스크롤해야 할 수도 있습니다.  
  
   데이터베이스에 전송 된 실제 SQL 쿼리를 볼 수 있습니다. 시작 하 고 데이터베이스 버전 및 마이그레이션 기록 테이블을 확인 하는 Entity Framework 몇 가지 초기 쿼리와 명령이 표시 됩니다.   
    ![출력 창](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   응용 프로그램을 중지 하 고 다시 시작 하지 않으면이 테스트를 반복할 수 없습니다. 응용 프로그램을 한 번 실행 하 여 연결 복원 력을 여러 번 테스트할 수 있게 하려는 경우 `InterceptorTransientErrors`에서 오류 카운터를 다시 설정 하는 코드를 작성할 수 있습니다.
7. 실행 전략 (다시 시도 정책)의 차이점을 확인 하려면 *논리* 폴더의 *WingtipToysConfiguration.cs* 파일에 있는 `SetExecutionStrategy` 줄을 주석으로 처리 하 고, 디버그 모드에서 **관리** 페이지를 다시 실행 하 고, &quot;&quot;를 다시 Throw 하는 제품을 추가 합니다.  
  
   이번에는 처음 생성 된 예외에서 디버거가 처음으로 쿼리를 실행 하려고 할 때 즉시 디버거가 중지 됩니다.  
    ![디버깅-세부 정보 보기](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. *WingtipToysConfiguration.cs* 파일에서 `SetExecutionStrategy` 줄의 주석 처리를 제거 합니다.

## <a name="summary"></a>요약

이 자습서에서는 연결 복원 력 및 명령 가로채기를 지원 하도록 Web Forms 샘플 응용 프로그램을 수정 하는 방법을 살펴보았습니다.

## <a name="next-steps"></a>다음 단계

ASP.NET Web Forms에서 연결 복원 력 및 명령 가로채기를 검토 한 후 [ASP.NET 4.5의](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)ASP.NET Web Forms 항목 비동기 메서드를 검토 합니다. 이 항목에서는 Visual Studio를 사용 하 여 비동기 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
