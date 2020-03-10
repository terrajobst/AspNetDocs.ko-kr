---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 구성 및 계측 | Microsoft Docs
author: microsoft
description: ASP.NET 2.0에는 구성 및 계측의 주요 변경 사항이 있습니다. 새 ASP.NET 구성 API를 통해 구성 변경을 pr으로 수행할 수 있습니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507881"
---
# <a name="configuration-and-instrumentation"></a>구성 및 계측

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 2.0에는 구성 및 계측의 주요 변경 사항이 있습니다. 새 ASP.NET 구성 API를 사용 하면 프로그래밍 방식으로 구성을 변경할 수 있습니다. 또한 많은 새 구성 설정이 새 구성 및 계측에 대해 허용 됩니다.

ASP.NET 2.0에는 구성 및 계측의 주요 변경 사항이 있습니다. 새 ASP.NET 구성 API를 사용 하면 프로그래밍 방식으로 구성을 변경할 수 있습니다. 또한 많은 새 구성 설정이 새 구성 및 계측에 대해 허용 됩니다.

이 모듈에서는 ASP.NET 구성 파일에 대 한 읽기 및 쓰기와 관련 된 구성 API를 ASP.NET 하는 방법에 대해 설명 합니다. 또한 ASP.NET 계측을 다룹니다. ASP.NET 추적에서 제공 되는 새로운 기능에 대해서도 설명 합니다.

## <a name="aspnet-configuration-api"></a>ASP.NET 구성 API

ASP.NET 구성 API를 사용 하면 단일 프로그래밍 인터페이스를 사용 하 여 응용 프로그램 구성 데이터를 개발, 배포 및 관리할 수 있습니다. 구성 파일에서 XML을 직접 편집 하지 않고 구성 API를 사용 하 여 프로그래밍 방식으로 complete ASP.NET 구성을 개발 하 고 수정할 수 있습니다. 또한 웹 기반 관리 도구 및 MMC (Microsoft Management Console) 스냅인에서 개발 하는 콘솔 응용 프로그램 및 스크립트에서 구성 API를 사용할 수 있습니다.

다음 두 가지 구성 관리 도구는 구성 API를 사용 하며 .NET Framework 버전 2.0에 포함 되어 있습니다.

- 구성 API를 사용 하 여 관리 작업을 간소화 하는 ASP.NET MMC 스냅인은 모든 수준의 구성 계층 구조에서 로컬 구성 데이터에 대 한 통합 보기를 제공 합니다.
- 호스트 된 사이트를 포함 하 여 로컬 및 원격 응용 프로그램의 구성 설정을 관리할 수 있는 웹 사이트 관리 도구입니다.

ASP.NET 구성 API는 웹 사이트 및 응용 프로그램을 프로그래밍 방식으로 구성 하는 데 사용할 수 있는 일련의 ASP.NET 관리 개체를 구성 합니다. 관리 개체는 .NET Framework 클래스 라이브러리로 구현 됩니다. 구성 API 프로그래밍 모델을 사용 하면 컴파일 타임에 데이터 형식을 적용 하 여 코드 일관성과 안정성을 보장할 수 있습니다. 응용 프로그램 구성을 쉽게 관리 하기 위해 구성 API를 사용 하면 데이터를 서로 다른 컬렉션으로 표시 하는 대신 단일 컬렉션으로 구성 계층의 모든 점에서 병합 된 데이터를 볼 수 있습니다. 구성 파일. 또한 구성 API를 사용 하면 구성 파일에서 XML을 직접 편집 하지 않고도 전체 응용 프로그램 구성을 조작할 수 있습니다. 마지막으로 API는 웹 사이트 관리 도구와 같은 관리 도구를 지원 하 여 구성 작업을 간소화 합니다. 구성 API는 컴퓨터에 구성 파일을 만들고 여러 컴퓨터에서 구성 스크립트를 실행 하는 것을 지원 하 여 배포를 간소화 합니다.

> [!NOTE]
> 구성 API는 IIS 응용 프로그램 만들기를 지원 하지 않습니다.

## <a name="working-with-local-and-remote-configuration-settings"></a>로컬 및 원격 구성 설정 사용

구성 개체는 컴퓨터와 같은 특정 물리적 엔터티 또는 응용 프로그램 또는 웹 사이트와 같은 논리적 엔터티에 적용 되는 구성 설정의 병합 된 보기를 나타냅니다. 지정 된 논리적 엔터티는 로컬 컴퓨터 또는 원격 서버에 있을 수 있습니다. 지정 된 엔터티에 대 한 구성 파일이 없는 경우 구성 개체는 machine.config 파일에 정의 된 대로 기본 구성 설정을 나타냅니다.

다음 클래스에서 열기 구성 방법 중 하나를 사용 하 여 구성 개체를 가져올 수 있습니다.

1. 엔터티가 클라이언트 응용 프로그램이 면 ConfigurationManager 클래스입니다.
2. 엔터티가 웹 응용 프로그램 인 경우 WebConfigurationManager 클래스입니다.

이러한 메서드는 구성 개체를 반환 하며,이 개체는 기본 구성 파일을 처리 하는 데 필요한 메서드 및 속성을 제공 합니다. 이러한 파일을 읽거나 쓰기 위해 액세스할 수 있습니다.

### <a name="reading"></a>읽기

GetSection 또는 GetSectionGroup 메서드를 사용 하 여 구성 정보를 읽습니다. 읽는 사용자 또는 프로세스에는 계층 구조의 모든 구성 파일에 대 한 읽기 권한이 있어야 합니다.

> [!NOTE]
> Path 매개 변수를 사용 하는 정적 GetSection 메서드를 사용 하는 경우 path 매개 변수는 코드가 실행 되 고 있는 응용 프로그램을 참조 해야 합니다. 그렇지 않으면 매개 변수는 무시 되 고 현재 실행 중인 응용 프로그램에 대 한 구성 정보가 반환 됩니다.

### <a name="writing"></a>쓰기

저장 방법 중 하나를 사용 하 여 구성 정보를 작성 합니다. 작성 하는 사용자 또는 프로세스에는 계층 내 모든 구성 파일에 대 한 읽기 권한 뿐만 아니라 현재 구성 계층 수준의 구성 파일 및 디렉터리에 대 한 쓰기 권한이 있어야 합니다.

지정 된 엔터티에 대 한 상속 된 구성 설정을 나타내는 구성 파일을 생성 하려면 다음 저장 구성 방법 중 하나를 사용 합니다.

1. 새 구성 파일을 만들기 위한 Save 메서드입니다.
2. 다른 위치에 새 구성 파일을 생성 하는 SaveAs 메서드입니다.

## <a name="configuration-classes-and-namespaces"></a>구성 클래스 및 네임 스페이스

많은 구성 클래스와 메서드는 서로 비슷합니다. 다음 표에서는 가장 일반적으로 사용 되는 구성 클래스 및 네임 스페이스에 대해 설명 합니다.

| **구성 클래스 또는 네임 스페이스** | **설명** |
| --- | --- |
| [System.object 구성](https://msdn.microsoft.com/library/system.configuration.aspx) 네임 스페이스 | 모든 .NET Framework 응용 프로그램에 대 한 기본 구성 클래스를 포함 합니다. 섹션 처리기 클래스는 GetSection 및 GetSectionGroup와 같은 메서드에서 섹션의 구성 데이터를 가져오는 데 사용 됩니다. 이러한 두 메서드는 static이 아닙니다. |
| System.object 구성 클래스 | 컴퓨터, 응용 프로그램, 웹 디렉터리 또는 기타 리소스에 대 한 구성 데이터 집합을 나타냅니다. 이 클래스에는 구성 설정을 업데이트 하 고 섹션 및 섹션 그룹에 대 한 참조를 얻기 위한 GetSection 및 GetSectionGroup와 같은 유용한 메서드가 포함 되어 있습니다. 이 클래스는 WebConfigurationManager 및 ConfigurationManager 클래스의 메서드와 같이 디자인 타임 구성 데이터를 가져오는 메서드의 반환 형식으로 사용 됩니다. |
| System.web. 구성 네임 스페이스 | [ASP.NET 구성 설정](https://msdn.microsoft.com/library/b5ysx397.aspx)에서 정의 된 ASP.NET 구성 섹션에 대 한 섹션 처리기 클래스를 포함 합니다. 섹션 처리기 클래스는 GetSection 및 GetSectionGroup와 같은 메서드에서 섹션의 구성 데이터를 가져오는 데 사용 됩니다. |
| System.Web.Configuration.WebConfigurationManager class | 런타임 및 디자인 타임 구성 설정에 대 한 참조를 얻기 위한 유용한 메서드를 제공 합니다. 이러한 메서드는 System.web. 구성 클래스를 반환 형식으로 사용 합니다. 이 클래스의 정적 GetSection 메서드 또는 ConfigurationManager 클래스의 비정적 GetSection 메서드를 서로 다른 방식으로 사용할 수 있습니다. 웹 응용 프로그램 구성의 경우 WebConfigurationManager 클래스 대신 ConfigurationManager 클래스를 사용할 것을 권장 합니다. |
| [System.object](https://msdn.microsoft.com/library/system.configuration.provider.aspx) 네임 스페이스 | 구성 공급자를 사용자 지정 하 고 확장 하는 방법을 제공 합니다. 구성 시스템의 모든 공급자 클래스에 대 한 기본 클래스입니다. |
| [System.web. Management](https://msdn.microsoft.com/library/system.web.management.aspx) 네임 스페이스 | 웹 응용 프로그램의 상태를 관리 및 모니터링 하기 위한 클래스와 인터페이스를 포함 합니다. 엄격히 말해서,이 네임 스페이스는 구성 API의 일부로 간주 되지 않습니다. 예를 들어 추적 및 이벤트 발생은이 네임 스페이스의 클래스에 의해 수행 됩니다. |
| [System.object](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) 네임 스페이스 | 응용 프로그램을 계측 하는 데 필요한 클래스를 제공 하 여 WMI (WMI(Windows Management Instrumentation))를 통해 잠재적 소비자에 게 관리 정보와 이벤트를 노출 합니다. ASP.NET 상태 모니터링은 WMI를 사용 하 여 이벤트를 전달 합니다. 엄격히 말해서,이 네임 스페이스는 구성 API의 일부로 간주 되지 않습니다. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET 구성 파일에서 읽기

WebConfigurationManager 클래스는 ASP.NET 구성 파일에서 읽기 위한 핵심 클래스입니다. ASP.NET 구성 파일을 읽는 데는 기본적으로 세 가지 단계가 있습니다.

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 구성 파일에서 원하는 정보를 읽습니다.

구성 개체가 특정 구성 파일을 나타내지 않는 경우 대신, 컴퓨터, 응용 프로그램 또는 웹 사이트의 구성에 대 한 병합 된 보기를 나타냅니다. 다음 코드 샘플에서는 *productinfo.webpart*이라는 웹 응용 프로그램의 구성을 나타내는 구성 개체를 인스턴스화합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> /ProductInfo 경로가 없는 경우 위의 코드는 machine.config 파일에 지정 된 대로 기본 구성을 반환 합니다.

구성 개체를 만든 후에는 GetSection 또는 GetSectionGroup 메서드를 사용 하 여 구성 설정을 자세히 살펴볼 수 있습니다. 다음 예제에서는 위의 Productinfo.webpart 응용 프로그램에 대 한 가장 설정에 대 한 참조를 가져옵니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET 구성 파일에 쓰기

구성 파일에서 읽는 것 처럼 WebConfigurationManager 클래스는 Asp.NET 구성 파일에 쓰기 위한 핵심 요소입니다. 또한 ASP.NET 구성 파일에 쓰기 위한 세 가지 단계가 있습니다.

1. OpenWebConfiguration 메서드를 사용 하 여 구성 개체를 가져옵니다.
2. 구성 파일에서 원하는 섹션에 대 한 참조를 가져옵니다.
3. 저장 또는 SaveAs 메서드를 사용 하 여 구성 파일에서 원하는 정보를 작성 합니다.

다음 코드는 &lt;컴파일&gt; 요소의 **debug** 특성을 false로 변경 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

이 코드가 실행 되 면 *webApp* 응용 프로그램의 web.config 파일에 대해 &lt;컴파일&gt; 요소의 **debug** 특성이 false로 설정 됩니다.

## <a name="systemwebmanagement-namespace"></a>System.Web.Management Namespace

ASP.NET 네임 스페이스는 응용 프로그램의 상태를 관리 및 모니터링 하기 위한 클래스와 인터페이스를 제공 합니다.

로깅은 이벤트를 공급자와 연결 하는 규칙을 정의 하 여 수행 됩니다. 규칙은 공급자에 게 전송 되는 이벤트의 유형을 정의 합니다. 다음 기본 이벤트를 로그에 사용할 수 있습니다.

| **WebBaseEvent** | 모든 이벤트에 대 한 기본 이벤트 클래스입니다. 이벤트 코드, 이벤트 정보 코드, 이벤트가 발생 한 날짜 및 시간, 시퀀스 번호, 이벤트 메시지 및 이벤트 세부 정보 등 모든 이벤트에 대 한 필수 속성을 포함 합니다. |
| --- | --- |
| **WebManagementEvent** | 응용 프로그램 수명, 요청, 오류 및 감사 이벤트와 같은 관리 이벤트에 대 한 기본 이벤트 클래스입니다. |
| **WebHeartbeatEvent** | 응용 프로그램에서 유용한 런타임 상태 정보를 캡처하기 위해 정기적으로 생성 하는 이벤트입니다. |
| **WebAuditEvent** | 권한 부여 실패, 암호 해독 실패 등의 조건을 표시 하는 데 사용 되는 보안 감사 이벤트에 대 한 기본 클래스입니다 *.* |
| **WebRequestEvent** | 모든 정보 요청 이벤트에 대 한 기본 클래스입니다. |
| **WebBaseErrorEvent** | 오류 조건을 나타내는 모든 이벤트에 대 한 기본 클래스입니다. |

사용 가능한 공급자 유형을 사용 하면 이벤트 출력을 이벤트 뷰어, SQL Server, WMI(Windows Management Instrumentation) (WMI) 및 전자 메일로 보낼 수 있습니다. 미리 구성 된 공급자 및 이벤트 매핑은 이벤트 출력을 기록 하는 데 필요한 작업량을 줄여 줍니다.

ASP.NET 2.0는 이벤트 로그 공급자를 사용 하 여 시작 및 중지와 같은 응용 프로그램 도메인을 기반으로 이벤트를 기록 하 고 처리 되지 않은 예외를 로깅합니다. 이렇게 하면 몇 가지 기본 시나리오를 처리할 수 있습니다. 예를 들어 응용 프로그램에서 예외를 throw 하지만 사용자가 오류를 저장 하지 않고 오류를 재현할 수 없다고 가정해 보겠습니다. 기본 이벤트 로그 규칙을 사용 하면 예외 및 스택 정보를 수집 하 여 발생 한 오류의 종류를 보다 잘 파악할 수 있습니다. 또 다른 예는 응용 프로그램이 세션 상태를 손실 하는 경우에 적용 됩니다. 이 경우 이벤트 로그를 확인 하 여 응용 프로그램 도메인의 재활용 여부와 응용 프로그램 도메인이 첫 번째 위치에서 중지 된 이유를 확인할 수 있습니다.

또한 상태 모니터링 시스템을 확장할 수 있습니다. 예를 들어 사용자 지정 웹 이벤트를 정의 하 고, 응용 프로그램 내에서이 이벤트를 발생 시킨 다음, 전자 메일 등의 공급자로 이벤트 정보를 전송 하는 규칙을 정의할 수 있습니다. 이를 통해 상태 모니터링 공급자에 계측을 쉽게 연결할 수 있습니다. 또 다른 예로, 주문이 처리 될 때마다 이벤트를 발생 시키고 각 이벤트를 SQL Server 데이터베이스로 전송 하는 규칙을 설정할 수 있습니다. 사용자가 행에서 여러 번 로그온 하지 못할 때 이벤트를 발생 시키고 전자 메일 기반 공급자를 사용 하도록 이벤트를 설정할 수도 있습니다.

기본 공급자 및 이벤트에 대 한 구성은 전역 Web.config 파일에 저장 됩니다. 전역 web.config 파일은 ASP.NET 1x의 machine.config 파일에 저장 된 모든 웹 기반 설정을 저장 합니다. 전역 web.config 파일은 다음 디렉터리에 있습니다.

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

전역 Web.config 파일의 &lt;healthMonitoring&gt; 섹션은 기본 구성 설정을 제공 합니다. 응용 프로그램의 Web.config 파일에 &lt;healthMonitoring&gt; 섹션을 구현 하 여 이러한 설정을 재정의 하거나 사용자 고유의 설정을 구성할 수 있습니다.

전역 Web.config 파일의 &lt;healthMonitoring&gt; 섹션에는 다음 항목이 포함 되어 있습니다.

| **providers** | 이벤트 뷰어, WMI 및 SQL Server에 대해 설정 된 공급자를 포함 합니다. |
| --- | --- |
| **eventMappings** | 다양 한 WebBase 클래스에 대 한 매핑을 포함 합니다. 사용자 고유의 이벤트 클래스를 생성 하는 경우이 목록을 확장할 수 있습니다. 사용자 고유의 이벤트 클래스를 생성 하면 정보를 전송 하는 공급자에 대 한 세부적인 세분성이 제공 됩니다. 예를 들어, 사용자 지정 이벤트를 전자 메일로 전송 하는 동안 처리 되지 않은 예외가 SQL Server로 전송 되도록 구성할 수 있습니다. |
| **역할** | EventMappings를 공급자에 연결 합니다. |
| **버퍼링** | SQL Server 및 전자 메일 공급자와 함께 사용 되어 이벤트를 공급자에 플러시하는 빈도를 결정 합니다. |

다음은 전역 Web.config 파일의 코드 예제입니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>이벤트 뷰어에 이벤트를 저장 하는 방법

앞서 설명한 것 처럼 이벤트 뷰어의 이벤트 로깅 공급자는 전역 web.config 파일에서 구성 됩니다. 기본적으로 **Webbaseerrorevent** 및 **WebFailureAuditEvent** 를 기반으로 하는 모든 이벤트가 로깅됩니다. 추가 정보를 이벤트 로그에 기록 하는 규칙을 추가할 수 있습니다. 예를 들어 모든*이벤트 (예*: **webbaseevent**를 기반으로 하는 모든 이벤트)를 기록 하려는 경우 web.config 파일에 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

이 규칙은 **모든** 이벤트 이벤트 맵을 이벤트 로그 공급자에 연결 합니다. EventMapping과 공급자는 모두 전역 Web.config 파일에 포함 되어 있습니다.

## <a name="how-to-store-events-to-sql-server"></a>SQL Server에 이벤트를 저장 하는 방법

이 메서드는 Aspnet\_regsql 도구에 의해 생성 되는 **aspnetdb.mdf** 데이터베이스를 사용 합니다. 기본 공급자는 LocalSqlServer 연결 문자열을 사용 합니다 .이 문자열은 App\_data 폴더 또는 SQL Server의 로컬 SQLExpress 인스턴스에 파일 기반 데이터베이스를 사용 합니다. LocalSqlServer 연결 문자열과 SqlProvider는 모두 전역 Web.config 파일에 구성 됩니다.

전역 Web.config 파일의 LocalSqlServer 연결 문자열은 다음과 같습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

다른 SQL Server 인스턴스를 사용 하려는 경우 Aspnet\_regsql 도구를 사용 해야 합니다 .이 도구 는%windir%\Microsoft.Net\Framework\v2.0.에서 찾을 수 있습니다.\* 폴더입니다. Aspnet\_regsql .exe 도구를 사용 하 여 SQL Server 인스턴스에서 사용자 지정 **aspnetdb.mdf** 데이터베이스를 생성 한 다음 응용 프로그램 구성 파일에 연결 문자열을 추가한 다음 새 연결 문자열을 사용 하 여 공급자를 추가 합니다. **Aspnetdb.mdf** 데이터베이스를 만든 후에는 Eventmapping을 sqlprovider에 연결 하는 규칙을 설정 해야 합니다.

기본 SqlProvider를 사용 하거나 고유한 공급자를 구성 하는 경우에는 이벤트 맵과 함께 공급자를 연결 하는 규칙을 추가 해야 합니다. 다음 규칙은 위에서 만든 새 공급자를 **All Events** 이벤트 맵에 연결 합니다. 이 규칙은 **Webbaseevent** 를 기준으로 모든 이벤트를 기록 하 고 MYASPNETDB 연결 문자열을 사용 하는 MySqlWebEventProvider에 보냅니다. 다음 코드는 공급자를 이벤트 맵과 연결 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

SQL Server에만 오류를 전송 하려는 경우 다음 규칙을 추가할 수 있습니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>WMI에 이벤트를 전달 하는 방법

WMI에 이벤트를 전달할 수도 있습니다. WMI 공급자는 기본적으로 전역 Web.config 파일에서 구성 됩니다.

다음 코드 예제에서는 WMI에 이벤트를 전달 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

EventMapping을 공급자에 연결 하는 규칙을 추가 하 고 이벤트를 수신 하는 WMI 수신기 응용 프로그램도 추가 해야 합니다. 다음 코드 예제에서는 WMI 공급자를 **모든 이벤트** 이벤트 맵에 연결 하는 규칙을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>전자 메일에 이벤트를 전달 하는 방법

이벤트를 전자 메일로 전달할 수도 있습니다. SQL Server 또는 이벤트 로그에 더 적합할 수 있는 많은 정보를 사용자에 게 보낼 수 있으므로 전자 메일 공급자에 매핑하는 이벤트 규칙에 주의 해야 합니다. 전자 메일 공급자에는 두 가지가 있습니다. SimpleMailWebEventProvider 및 TemplatedMailWebEventProvider. 각각은 "template" 및 "detailedTemplateErrors" 특성을 제외 하 고 동일한 구성 특성을 가지 며, 둘 다 TemplatedMailWebEventProvider 에서만 사용할 수 있습니다.

> [!NOTE]
> 이러한 전자 메일 공급자는 모두 구성 되어 있지 않습니다. Web.config 파일에 추가 해야 합니다.

이러한 두 메일 공급자의 주요 차이점은 SimpleMailWebEventProvider는 수정할 수 없는 일반 템플릿에서 전자 메일을 보내는 것입니다. 샘플 Web.config 파일은 다음 규칙을 사용 하 여 구성 된 공급자 목록에이 전자 메일 공급자를 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

전자 메일 공급자를 **모든 이벤트** 이벤트 맵에 연결 하기 위해 다음 규칙도 추가 됩니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 추적

ASP.NET 2.0에서는 세 가지 주요 추적 기능이 향상 되었습니다.

1. 통합 추적 기능
2. 추적 메시지에 대 한 프로그래밍 방식 액세스
3. 향상 된 응용 프로그램 수준 추적

## <a name="integrated-tracing-functionality"></a>통합 추적 기능

이제 ASP.NET 클래스에서 내보낸 메시지를 추적 출력으로 라우팅하고 ASP.NET 추적에서 내보낸 메시지를로 라우팅할 수 있습니다. ASP.NET 계측 이벤트를 System.object로 전달할 수도 있습니다. 이 기능은 &lt;trace&gt; 요소의 새 **writeToDiagnosticsTrace** 특성에 의해 제공 됩니다. 이 부울 값이 true 이면 추적 메시지를 표시 하도록 등록 된 모든 수신기에서 사용 하기 위해 ASP.NET 추적 메시지가 시스템 진단 추적 인프라에 전달 됩니다.

## <a name="programmatic-access-to-trace-messages"></a>추적 메시지에 대 한 프로그래밍 방식 액세스

ASP.NET 2.0를 사용 하면 **TraceContextRecord** 클래스와 **TraceRecords** collection을 통해 모든 추적 메시지에 프로그래밍 방식으로 액세스할 수 있습니다. 추적 메시지에 액세스 하는 가장 효율적인 방법은 새 **Tracefinished** 이벤트를 처리 하기 위해 **TraceContextEventHandler** 대리자 (ASP.NET 2.0에서 새로 만들기)를 등록 하는 것입니다. 그런 다음 원하는 대로 추적 메시지를 반복할 수 있습니다.

다음 코드 샘플에서는이를 보여 줍니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

위의 예제에서 TraceRecords 컬렉션을 반복 하 고 각 메시지를 응답 스트림에 씁니다.

## <a name="improved-application-level-tracing"></a>향상 된 응용 프로그램 수준 추적

응용 프로그램 수준 추적은 &lt;trace&gt; 요소의 새 **Mostststststststststststststststststststststststst** 이 특성은 가장 최근의 응용 프로그램 수준 추적 출력이 표시 되 고 requestLimit에서 표시 하는 제한을 초과 하는 오래 된 추적 데이터가 삭제 되는지 여부를 지정 합니다. False 이면 requestLimit 특성에 도달할 때까지 요청에 대 한 추적 데이터가 표시 됩니다.

## <a name="aspnet-command-line-tools"></a>ASP.NET 명령줄 도구

ASP.NET를 구성 하는 데 도움이 되는 몇 가지 명령줄 도구가 있습니다. ASP.NET 개발자는 aspnet\_regiis .exe 도구에 대해 잘 알고 있어야 합니다. ASP.NET 2.0는 구성에 도움이 되는 세 가지 다른 명령줄 도구를 제공 합니다.

사용할 수 있는 명령줄 도구는 다음과 같습니다.

| **도구** | **사용** |
| --- | --- |
| **aspnet\_regiis .exe** | IIS를 사용 하 여 ASP.NET를 등록할 수 있습니다. ASP.NET 2.0와 함께 제공 되는이 도구의 두 가지 버전이 있습니다. 하나는 32 비트 시스템 (프레임 워크 폴더)이 고 다른 하나는 64 비트 시스템 (Framework64 폴더)입니다. 64 비트 버전은 32 비트 OS에 설치 되지 않습니다. |
| **aspnet\_regsql .exe** | ASP.NET SQL Server 등록 도구는 ASP.NET의 SQL Server 공급자가 사용할 Microsoft SQL Server 데이터베이스를 만들거나 기존 데이터베이스에서 옵션을 추가 하거나 제거 하는 데 사용 됩니다. Aspnet\_regsql .exe 파일은 웹 서버의 [drive:] \WINDOWS\Microsoft.NET\Framework\versionNumber 폴더에 있습니다. |
| **aspnet\_regbrowsers .exe** | ASP.NET Browser 등록 도구는 모든 시스템 수준 브라우저 정의를 구문 분석 하 여 어셈블리로 컴파일하고 어셈블리를 전역 어셈블리 캐시에 설치 합니다. 이 도구는 브라우저 정의 파일 ()을 사용 합니다. 브라우저 파일)을 .NET Framework. %SystemRoot%\Microsoft.NET\Framework\version\ 디렉터리에서이 도구를 찾을 수 있습니다. |
| **aspnet\_컴파일러 .exe** | ASP.NET 컴파일 도구를 사용 하면 ASP.NET 웹 응용 프로그램을 현재 위치에서 또는 배포를 위해 프로덕션 서버와 같은 대상 위치로 컴파일할 수 있습니다. 응용 프로그램을 컴파일하는 동안 최종 사용자가 응용 프로그램에 대 한 첫 번째 요청에 지연이 발생 하지 않기 때문에 현재 위치의 컴파일을 통해 응용 프로그램 성능을 향상 시킬 수 있습니다. |

Aspnet\_regiis .exe 도구는 ASP.NET 2.0의 새로운 기능은 아니므로 여기서는 설명 하지 않습니다.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server 등록 도구-aspnet\_regsql .exe

ASP.NET SQL Server 등록 도구를 사용 하 여 여러 종류의 옵션을 설정할 수 있습니다. SQL 연결을 지정 하 고, SQL Server 사용 하 여 정보를 관리할 ASP.NET 응용 프로그램 서비스를 지정 하 고, SQL 캐시 종속성에 사용 되는 데이터베이스 또는 테이블을 표시 하 고, SQL Server를 사용 하 여 프로시저 및 세션 상태를 저장 하는 지원을 추가 하거나 제거할 수 있습니다.

여러 ASP.NET 응용 프로그램 서비스는 공급자를 사용 하 여 데이터 원본에서 데이터 저장 및 검색을 관리 합니다. 각 공급자는 데이터 원본에만 적용 됩니다. ASP.NET에는 다음과 같은 ASP.NET 기능을 위한 SQL Server 공급자가 포함 되어 있습니다.

- 멤버 자격 ( [Sqlmembershipprovider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) 클래스)
- 역할 관리 ( [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) 클래스)
- Profile ( [Sqlprofileprovider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) 클래스).
- 개인 설정 웹 파트 ( [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) 클래스)
- 웹 이벤트 ( [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) 클래스)

ASP.NET를 설치 하는 경우 서버에 대 한 Machine.config 파일에는 공급자를 사용 하는 각 ASP.NET 기능에 대해 SQL Server 공급자를 지정 하는 구성 요소가 포함 됩니다. 이러한 공급자는 기본적으로 SQL Server Express 2005의 로컬 사용자 인스턴스에 연결 하기 위해 구성 됩니다. 공급자가 사용 하는 기본 연결 문자열을 변경 하는 경우 컴퓨터 구성에서 구성 된 ASP.NET 기능을 사용 하려면 먼저 Aspnet\_를 사용 하 여 선택한 기능의 SQL Server 데이터베이스와 데이터베이스 요소를 설치 해야 합니다. SQL 등록 도구를 사용 하 여 지정 하는 데이터베이스가 아직 없는 경우 (명령줄에서 aspnetdb.mdf가 지정 되지 않은 경우 기본 데이터베이스를 사용 하는 경우), 현재 사용자는 스키마 e를 만들 뿐만 아니라 SQL Server에서 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 데이터베이스 내의 lements.

### <a name="sql-cache-dependency"></a>SQL 캐시 종속성

ASP.NET 출력 캐싱의 고급 기능은 SQL 캐시 종속성입니다. SQL 캐시 종속성은 두 가지 작업 모드를 지원 합니다. 하나는 테이블 폴링의 ASP.NET 구현을 사용 하 고 두 번째 모드는 SQL Server 2005의 쿼리 알림 기능을 사용 합니다. SQL 등록 도구는 작업의 테이블 폴링 모드를 구성 하는 데 사용할 수 있습니다.

### <a name="session-state"></a>세션 상태

기본적으로 세션 상태 값과 정보는 ASP.NET 프로세스 내의 메모리에 저장 됩니다. 또는 세션 데이터를 여러 웹 서버에서 공유할 수 있는 SQL Server 데이터베이스에 저장할 수 있습니다. SQL 등록 도구를 사용 하 여 세션 상태를 지정 하는 데이터베이스가 아직 없는 경우 현재 사용자는 데이터베이스 내에 스키마 요소를 만들 뿐만 아니라 SQL Server 데이터베이스를 만들 수 있는 권한이 있어야 합니다. 데이터베이스가 있는 경우 현재 사용자는 기존 데이터베이스에 스키마 요소를 만들 수 있는 권한이 있어야 합니다.

SQL Server에서 세션 상태 데이터베이스를 설치 하려면 Aspnet\_regsql 도구를 실행 하 고 명령에 다음 정보를 제공 합니다.

- **-S** 옵션을 사용 하는 SQL Server 인스턴스의 이름입니다.
- SQL Server를 실행 하는 컴퓨터에서 데이터베이스를 만들 수 있는 권한이 있는 계정에 대 한 로그온 자격 증명입니다. \- **E** 옵션을 사용 하 여 현재 로그온 한 사용자를 사용 하거나- **U** 옵션을 사용 하 여 암호를 지정 하는- **P** 옵션과 함께 사용자 ID를 지정 합니다.
- **-Ssadd** 명령줄 옵션을 통해 세션 상태 데이터베이스를 추가할 수 있습니다.

기본적으로 Aspnet\_regsql .exe 도구를 사용 하 여 SQL Server 2005 Express Edition를 실행 하는 컴퓨터에 세션 상태 데이터베이스를 설치할 수 없습니다.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET Browser 등록 도구-aspnet\_regbrowsers .exe

ASP.NET 버전 1.1에서 machine.config 파일에는 &lt;browserCaps&gt;라는 섹션이 포함 되어 있습니다. 이 섹션에는 정규식을 기반으로 다양 한 브라우저의 구성을 정의 하는 일련의 XML 항목이 포함 되어 있습니다. ASP.NET 버전 2.0의 경우 새입니다. 브라우저 파일은 XML 항목을 사용 하 여 특정 브라우저의 매개 변수를 정의 합니다. 새를 추가 하 여 새 브라우저에 정보를 추가 합니다. 시스템 의%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers에 있는 폴더에 대 한 브라우저 파일입니다.

응용 프로그램은 브라우저 정보를 필요로 할 때마다 .config 파일을 읽지 않으므로 새을 만들 수 있습니다. 브라우저 파일 및 Aspnet\_를 실행 하 여 어셈블리에 필요한 변경 내용을 추가 합니다. 이렇게 하면 서버에서 즉시 새 브라우저 정보에 액세스할 수 있으므로 정보를 선택 하기 위해 응용 프로그램을 종료할 필요가 없습니다. 응용 프로그램은 현재 HttpRequest의 Browser 속성을 통해 브라우저 기능에 액세스할 수 있습니다.

다음 옵션은 aspnet\_를 실행 하는 경우에 사용할 수 있습니다.

| **옵션** | **설명** |
| --- | --- |
| **-?** | 명령 창에 Aspnet\_regbbrowsers 도움말 텍스트를 표시 합니다. |
| **-i** | 런타임 브라우저 기능 어셈블리를 만들어 전역 어셈블리 캐시에 설치 합니다. |
| **-u** | 전역 어셈블리 캐시에서 런타임 브라우저 기능 어셈블리를 제거 합니다. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET 컴파일 도구-aspnet\_컴파일러 .exe

ASP.NET 컴파일 도구는 두 가지 일반적인 방법으로 사용할 수 있습니다. 여기서는 대상 출력 디렉터리가 지정 된 배포에 대 한 내부 컴파일 및 컴파일을 수행 합니다.

### <a name="compiling-an-application-in-place"></a>[원위치에서 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 컴파일 도구는 응용 프로그램을 원위치에서 컴파일할 수 있습니다. 즉, 응용 프로그램에 대 한 여러 요청 동작을 모방 하 여 정기적인 컴파일을 수행 합니다. 미리 컴파일된 사이트의 사용자는 첫 번째 요청에서 페이지를 컴파일하면 지연이 발생 하지 않습니다.

현재 위치에서 사이트를 미리 컴파일하면 다음 항목이 적용 됩니다.

- 사이트는 파일 및 디렉터리 구조를 유지 합니다.
- 서버의 사이트에서 사용 하는 모든 프로그래밍 언어에 대 한 컴파일러를 사용 해야 합니다.
- 파일이 컴파일되지 않으면 전체 사이트 컴파일이 실패 합니다.

새 소스 파일을 추가 하 고 나 서 응용 프로그램을 다시 컴파일할 수도 있습니다. **-C** 옵션을 포함 하지 않으면 도구는 새 파일이 나 변경 된 파일만 컴파일합니다.

> [!NOTE]
> 중첩 된 응용 프로그램을 포함 하는 응용 프로그램을 컴파일하면 중첩 된 응용 프로그램이 컴파일되지 않습니다. 중첩 된 응용 프로그램은 개별적으로 컴파일해야 합니다.

### <a name="compiling-an-application-for-deployment"></a>[배포용 응용 프로그램 컴파일](https://msdn.microsoft.com/library/ms229863.aspx)

TargetDir 매개 변수를 지정 하 여 배포용 응용 프로그램 (대상 위치로 컴파일)을 컴파일합니다. TargetDir는 웹 응용 프로그램의 최종 위치 이거나 컴파일된 응용 프로그램을 추가로 배포할 수 있습니다. **-U** 옵션을 사용 하면 컴파일된 응용 프로그램에서 특정 파일을 다시 컴파일하지 않고 변경할 수 있는 방식으로 응용 프로그램을 컴파일합니다. Aspnet\_컴파일러 .exe는 정적 및 동적 파일 형식을 구분 하 고 결과 응용 프로그램을 만들 때 서로 다르게 처리 합니다.

- 정적 파일 형식에는 연결 된 컴파일러 또는 빌드 공급자가 없는 파일 (예: .css, .gif, .htm, .html, .jpg, .js 등의 확장명이 있는 파일)이 있습니다. 이러한 파일은 대상 위치에 복사 되 고 디렉터리 구조의 상대 위치는 유지 됩니다.
- 동적 파일 형식은 ASP.NET와 같은 파일 이름 확장명을 사용 하는 파일 (예:, .ascx, .ashx, .aspx, .browser, .master 등)을 포함 하는 연결 된 컴파일러나 빌드 공급자를 포함 하는 형식입니다. ASP.NET 컴파일 도구는 이러한 파일에서 어셈블리를 생성 합니다. **-U** 옵션을 생략 하면이 도구는 파일 이름 확장명을 사용 하 여 파일을 만듭니다. 원본 소스 파일을 해당 어셈블리에 매핑하는 컴파일 되었습니다. 응용 프로그램 소스의 디렉터리 구조가 유지 되도록 하기 위해 도구는 대상 응용 프로그램의 해당 위치에 자리 표시자 파일을 생성 합니다.

컴파일된 응용 프로그램의 콘텐츠를 수정할 수 있음을 나타내려면 **-u** 옵션을 사용 해야 합니다. 그렇지 않으면 후속 수정 내용이 무시 되거나 런타임 오류가 발생 합니다.

다음 표에서는 **-u** 옵션을 포함 하는 경우 ASP.NET 컴파일 도구가 다른 파일 형식을 처리 하는 방법을 설명 합니다.

| **파일 유형** | **컴파일러 작업** |
| --- | --- |
| .ascx, .aspx, .master | 이러한 파일은 태그 및 소스 코드로 분할 됩니다. 여기에는 코드 숨김이 포함 되 고 &lt;스크립트 runat = "server"&gt; 요소로 묶인 모든 코드가 포함 됩니다. 소스 코드는 해싱 알고리즘에서 파생 되는 이름을 사용 하 여 어셈블리로 컴파일되며 어셈블리는 Bin 디렉터리에 배치 됩니다. **&lt;%** 및 **%&gt;** 대괄호 사이에 포함 된 코드 인 모든 인라인 코드는 태그와 함께 포함 되며 컴파일되지 않습니다. 소스 파일과 이름이 같은 새 파일이 생성 되어 태그를 포함 하 고 해당 출력 디렉터리에 배치 됩니다. |
| .ashx, .asmx | 이러한 파일은 컴파일되지 않으며 컴파일되지 않고 출력 디렉터리로 이동 합니다. 처리기 코드를 컴파일하려면 앱\_코드 디렉터리에 있는 소스 코드 파일에 코드를 저장 합니다. |
| .cs, .vb, .jsl, .cpp (앞에 나열 된 파일 형식에 대 한 코드 숨겨진 파일 포함 안 함) | 이러한 파일은 컴파일된 후 해당 파일을 참조 하는 어셈블리에 리소스로 포함 됩니다. 원본 파일이 출력 디렉터리에 복사 되지 않습니다. 참조 되지 않은 코드 파일은 컴파일되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 컴파일되지 않습니다. 이러한 파일은 해당 출력 디렉터리에 복사 됩니다. |
| 앱\_코드 하위 디렉터리의 소스 코드 파일 | 이러한 파일은 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. |
| 응용 프로그램의 .resx 및. 리소스 파일\_GlobalResources 하위 디렉터리 | 이러한 파일은 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 주 출력 디렉터리 아래에는 App\_GlobalResources 하위 디렉터리가 생성 되지 않으며 원본 디렉터리에 있는 .resx 또는 .resources 파일은 출력 디렉터리에 복사 되지 않습니다. |
| 응용 프로그램의 .resx 및 .resources 파일\_LocalResources 하위 디렉터리 | 이러한 파일은 컴파일되지 않으며 해당 출력 디렉터리에 복사 됩니다. |
| 앱\_테마 하위 디렉터리의 .skin 파일 | .Skin 파일 및 정적 테마 파일은 컴파일되지 않으며 해당 출력 디렉터리에 복사 됩니다. |
| .browser Web.config 정적 파일 형식 어셈블리가 Bin 디렉터리에 이미 있습니다. | 이러한 파일은 출력 디렉터리에 있는 그대로 복사 됩니다. |

다음 표에서는 **-u** 옵션을 생략할 때 ASP.NET 컴파일 도구에서 다른 파일 형식을 처리 하는 방법을 설명 합니다.

| **파일 유형** | **컴파일러 작업** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | 이러한 파일은 태그 및 소스 코드로 분할 됩니다. 여기에는 코드 숨김이 포함 되 고 &lt;스크립트 runat = "server"&gt; 요소로 묶인 모든 코드가 포함 됩니다. 소스 코드는 해싱 알고리즘에서 파생 되는 이름을 사용 하 여 어셈블리로 컴파일됩니다. 결과 어셈블리는 Bin 디렉터리에 배치 됩니다. **&lt;%** 및 **%&gt;** 대괄호 사이에 포함 된 코드 인 모든 인라인 코드는 태그와 함께 포함 되며 컴파일되지 않습니다. 컴파일러는 소스 파일과 이름이 같은 태그를 포함 하는 새 파일을 만듭니다. 이러한 결과 파일은 Bin 디렉터리에 배치 됩니다. 또한 컴파일러는 소스 파일과 이름이 같지만 확장명이 인 파일을 만듭니다. 매핑 정보를 포함 하는 컴파일 되었습니다. 여. 컴파일된 파일은 소스 파일의 원래 위치에 해당 하는 출력 디렉터리에 배치 됩니다. |
| .ascx | 이러한 파일은 태그와 소스 코드로 분할 됩니다. 소스 코드는 해싱 알고리즘에서 파생 되는 이름을 사용 하 여 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 태그 파일이 생성 되지 않습니다. |
| .cs, .vb, .jsl, .cpp (앞에 나열 된 파일 형식에 대 한 코드 숨겨진 파일 포함 안 함) | .Ascx, .ashx 또는 .aspx 파일에서 생성 된 어셈블리에서 참조 하는 소스 코드는 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 원본 파일이 복사 되지 않습니다. |
| 사용자 지정 파일 형식 | 이러한 파일은 동적 파일과 같이 컴파일됩니다. 기반으로 하는 파일의 형식에 따라 컴파일러는 출력 디렉터리에 매핑 파일을 저장할 수 있습니다. |
| 앱\_코드 하위 디렉터리의 파일 | 이 하위 디렉터리의 소스 코드 파일은 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. |
| GlobalResources 하위 디렉터리\_앱의 파일 | 이러한 파일은 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 주 출력 디렉터리 아래에는 App\_GlobalResources 하위 디렉터리가 생성 되지 않습니다. 구성 파일이 appliesTo = "All"을 지정 하는 경우 .resx 및 .resources 파일이 출력 디렉터리에 복사 됩니다. [Buildprovider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)에서 참조 하는 경우에는 복사 되지 않습니다. |
| 응용 프로그램의 .resx 및 .resources 파일\_LocalResources 하위 디렉터리 | 이러한 파일은 고유한 이름을 가진 어셈블리로 컴파일되며 Bin 디렉터리에 배치 됩니다. .Resx 또는. 리소스 파일은 출력 디렉터리에 복사 되지 않습니다. |
| 앱\_테마 하위 디렉터리의 .skin 파일 | 테마는 어셈블리로 컴파일되고 Bin 디렉터리에 배치 됩니다. 스텁 파일은 .skin 파일에 대해 생성 되 고 해당 출력 디렉터리에 배치 됩니다. .Css와 같은 정적 파일이 출력 디렉터리에 복사 됩니다. |
| .browser Web.config 정적 파일 형식 어셈블리가 Bin 디렉터리에 이미 있습니다. | 이러한 파일은 출력 디렉터리에 있는 그대로 복사 됩니다. |

### <a name="fixed-assembly-names"></a>[고정 어셈블리 이름](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Installer를 사용 하 여 웹 응용 프로그램을 배포 하는 등의 일부 시나리오에서는 일관 된 파일 이름과 내용을 사용 해야 하며, 어셈블리 또는 업데이트에 대 한 구성 설정을 식별 하는 일관 된 디렉터리 구조를 사용 해야 합니다. 이러한 경우 **-fixednames** 옵션을 사용 하 여 여러 페이지가 어셈블리로 컴파일되는를 사용 하는 대신 ASP.NET 컴파일 도구가 각 소스 파일에 대 한 어셈블리를 컴파일하도록 지정할 수 있습니다. 이렇게 하면 많은 수의 어셈블리가 생길 수 있으므로 확장성에 관심이 있는 경우에는이 옵션을 주의 해 서 사용 해야 합니다.

### <a name="strong-name-compilation"></a>[강력한 이름 컴파일](https://msdn.microsoft.com/library/ms229863.aspx##)

\_컴파일러 .exe를 사용 하 여 [강력한 이름 도구 (sn.exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) 를 별도로 사용 하지 않고도 강력한 이름의 어셈블리를 만들 수 있도록 **-aptca**, **-delaysign**, **-keycontainer** 및 **-keyfile** 옵션이 제공 됩니다. 이러한 옵션은 각각 **AllowPartiallyTrustedCallersAttribute**, **assemblydelaysignattribute**, **Assemblydelaysignattribute**및 **AssemblyKeyFileAttribute**에 해당 합니다.

이러한 특성에 대 한 설명은이 과정의 범위를 벗어납니다.

## <a name="labs"></a>랩

다음 labs는 각각 이전 랩을 기반으로 합니다. 이러한 작업은 순서 대로 수행 해야 합니다.

## <a name="lab-1-using-the-configuration-api"></a>랩 1: 구성 API 사용

1. *Mod9lab*라는 새 웹 사이트를 만듭니다.
2. 새 웹 구성 파일을 사이트에 추가 합니다.
3. Web.config 파일에 다음을 추가 합니다.

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

이렇게 하면 web.config 파일에 변경 내용을 저장할 수 있는 권한이 있게 됩니다.

1. Default.aspx에 새 레이블 컨트롤을 추가 하 고 ID를 **lblDebugStatus**로 변경 합니다.
2. Default.aspx에 새 단추 컨트롤을 추가 합니다.
3. 단추 컨트롤의 ID를 **btnToggleDebug** 로 변경 하 고 텍스트를 **디버그 상태를 전환**합니다.
4. Default.aspx의 코드 파일에 대 한 코드 뷰를 열고 다음과 같이 **system.web. 구성** 에 대 한 **using** 문을 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 클래스에 두 개의 private 변수를 추가 하 고 아래와 같이 페이지\_Init 메서드를 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 페이지\_로드에 다음 코드를 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Default.aspx를 저장 하 고 찾아봅니다. 레이블 컨트롤이 현재 디버그 상태를 표시 합니다.
2. 디자이너에서 Button 컨트롤을 두 번 클릭 하 고 Button 컨트롤의 Click 이벤트에 다음 코드를 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Default.aspx를 저장 하 고 찾아서 클릭 한 다음 단추를 클릭 합니다.
2. 각 단추를 클릭 한 후 web.config 파일을 열고 &lt;컴파일&gt; 섹션에서 **디버그** 특성을 관찰 합니다.

## <a name="lab-2-logging-application-restarts"></a>랩 2: 응용 프로그램 다시 시작 로깅

이 랩에서는 이벤트 뷰어에서 응용 프로그램 종료, 시작과 시작과 다시 컴파일의 로깅을 전환 하는 데 사용할 수 있는 코드를 만듭니다.

1. DropDownList을 default.aspx에 추가 하 고 ID를 ddlLogAppEvents로 변경 합니다.
2. DropDownList의 **AutoPostBack** 속성을 **true**로 설정 합니다.
3. DropDownList의 Items 컬렉션에 세 개의 항목을 추가 합니다. 첫 번째 항목의 **텍스트** 를 *선택* 하 고 값을-1로 설정 합니다. 두 번째 항목의 **텍스트** 와 **값** 을 **True로** 설정 하 고 세 번째 항목의 **텍스트** 와 **값** 을 **False로**설정 합니다.
4. Default.aspx에 새 레이블을 추가 합니다. ID를 **lblLogAppEvents**로 변경 합니다.
5. Default.aspx에 대 한 코드 숨김으로 보기를 열고 아래와 같이 HealthMonitoringSection 형식의 변수에 대 한 새 선언을 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. \_Init 페이지의 기존 코드에 다음 코드를 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList을 두 번 클릭 하 고 SelectedIndexChanged 이벤트에 다음 코드를 추가 합니다.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default.aspx를 찾아봅니다.
2. 드롭다운을 **False**로 설정 합니다.
3. 이벤트 뷰어에서 응용 프로그램 로그를 지웁니다.
4. 응용 프로그램에 대 한 디버그 특성을 변경 하려면 단추를 클릭 합니다.
5. 이벤트 뷰어에서 응용 프로그램 로그를 새로 고칩니다. 

    1. 이벤트가 기록 되었습니까?
    2. 무엇 인가?
6. 드롭다운을 True로 설정 **합니다.**
7. 응용 프로그램에 대 한 디버그 특성을 설정/해제 하려면 단추를 클릭 합니다.
8. 응용 프로그램 로그인 이벤트 뷰어를 새로 고칩니다. 

    1. 이벤트가 기록 되었습니까?
    2. 앱이 종료 된 이유는 무엇 인가요?
9. 로깅을 설정 및 해제 하 고 web.config 파일에 대 한 변경 내용을 확인 합니다.

## <a name="more-information"></a>추가 정보:

ASP.NET 2.0의 공급자 모델을 사용 하면 응용 프로그램 계측 뿐만 아니라 멤버 자격, 프로필 등의 다른 많은 용도로 사용자 고유의 공급자를 만들 수 있습니다. 응용 프로그램 이벤트를 텍스트 파일에 기록 하는 사용자 지정 공급자를 작성 하는 방법에 대 한 자세한 내용은 [이 링크](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)를 참조 하세요.
