---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
title: ELMAH를 사용 하 여 오류 세부 정보 로깅 (VB) | Microsoft Docs
author: rick-anderson
description: 오류 로깅 모듈 및 처리기 (ELMAH)는 프로덕션 환경에서 런타임 오류를 기록 하는 또 다른 방법을 제공 합니다. ELMAH는 무료 오픈 소스 오류입니다 ...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: a5f0439f-18b2-4c89-96ab-75b02c616f46
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-vb
msc.type: authoredcontent
ms.openlocfilehash: 46b7fc22807c8cb9f47ff035639815d7b6104735
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622430"
---
# <a name="logging-error-details-with-elmah-vb"></a>ELMAH를 사용하여 오류 세부 정보 로깅(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_vb.pdf)

> 오류 로깅 모듈 및 처리기 (ELMAH)는 프로덕션 환경에서 런타임 오류를 기록 하는 또 다른 방법을 제공 합니다. ELMAH는 오류 필터링과 같은 기능, 웹 페이지에서 오류 로그를 확인 하는 기능, RSS 피드를 포함 하는 무료 오픈 소스 오류 로깅 라이브러리 또는 쉼표로 구분 된 파일로 다운로드 하는 기능을 포함 합니다. 이 자습서에서는 ELMAH를 다운로드 하 고 구성 하는 과정을 안내 합니다.

## <a name="introduction"></a>소개

[위의 자습서](logging-error-details-with-asp-net-health-monitoring-vb.md) 에서는 ASP를 검사 했습니다. 광범위 한 웹 이벤트를 기록 하기 위한 기본 제공 라이브러리를 제공 하는 NET의 상태 모니터링 시스템입니다. 많은 개발자가 상태 모니터링을 사용 하 여 처리 되지 않은 예외의 세부 정보를 기록 하 고 전자 메일로 보냅니다. 그러나이 시스템에는 몇 가지 어려움 사항이 있습니다. 무엇 보다도, 기록 된 이벤트에 대 한 정보를 보기 위한 일종의 사용자 인터페이스가 없습니다. 10 개의 마지막 오류에 대 한 요약을 보거나 지난 주에 발생 한 오류에 대 한 세부 정보를 보려면 데이터베이스를 poke 하거나 전자 메일 받은 편지함을 검색 하거나 `aspnet_WebEvent_Events` 테이블의 정보를 표시 하는 웹 페이지를 작성 해야 합니다.

또 다른 어려움은 상태 모니터링의 복잡성을 중심으로 합니다. 상태 모니터링을 사용 하 여 여러 이벤트의 다양 한을 기록할 수 있으며, 이벤트를 기록 하는 방법과 시기를 설명 하는 다양 한 옵션이 있으므로 상태 모니터링 시스템을 올바르게 구성 하는 작업은 번거로운 작업 일 수 있습니다. 마지막으로 호환성 문제가 있습니다. 상태 모니터링은 2.0 버전의 .NET Framework에 먼저 추가 되었으므로 ASP.NET 버전 1.x를 사용 하 여 빌드된 이전 웹 응용 프로그램에서는 사용할 수 없습니다. 또한 이전 자습서에서 데이터베이스에 오류 정보를 기록 하는 데 사용한 `SqlWebEventProvider` 클래스는 Microsoft SQL Server 데이터베이스 에서만 작동 합니다. XML 파일이 나 Oracle 데이터베이스와 같은 대체 데이터 저장소에 오류를 기록해 야 하는 경우에는 사용자 지정 로그 공급자 클래스를 만들어야 합니다.

상태 모니터링 시스템에 대 한 대안은 [Atif Aziz](http://www.raboof.com/)에서 만든 무료 오픈 소스 오류 로깅 시스템용 오류 로깅 모듈 및 처리기 (ELMAH)입니다. 두 시스템 간의 가장 주목할 만한 차이점은 웹 페이지 및 RSS 피드에 오류 목록과 특정 오류에 대 한 세부 정보를 표시 하는 것입니다. ELMAH는 오류만 기록 하므로 상태 모니터링 보다 구성 하기가 더 쉽습니다. 또한 ELMAH는 ASP.NET 1.x, ASP.NET 2.0 및 ASP.NET 3.5 응용 프로그램에 대 한 지원을 포함 하 고 다양 한 로그 원본 공급자와 함께 제공 됩니다.

이 자습서에서는 ASP.NET 응용 프로그램에 ELMAH를 추가 하는 것과 관련 된 단계를 안내 합니다. 시작 하겠습니다.

> [!NOTE]
> 상태 모니터링 시스템과 ELMAH는 모두 자체 장단점이 있습니다. 두 시스템을 사용해 보고 사용자의 요구에 가장 적합 한 것을 결정 하는 것이 좋습니다.

## <a name="adding-elmah-to-an-aspnet-web-application"></a>ASP.NET 웹 응용 프로그램에 ELMAH 추가

ELMAH를 새로운 또는 기존 ASP.NET 응용 프로그램에 통합 하는 것은 5 분이 소요 되는 쉽고 간단한 프로세스입니다. 간단히 말해서 간단한 4 단계를 포함 합니다.

1. ELMAH를 다운로드 하 고 웹 응용 프로그램에 `Elmah.dll` 어셈블리를 추가 합니다.
2. `Web.config`에서 ELMAH의 HTTP 모듈 및 처리기를 등록 합니다.
3. ELMAH의 구성 옵션을 지정 합니다.
4. 필요한 경우 오류 로그 원본 인프라를 만듭니다.

이러한 4 단계를 한 번에 하나씩 살펴보겠습니다.

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>1 단계: ELMAH 프로젝트 파일 다운로드 및 웹 응용 프로그램에`Elmah.dll`추가

작성할 당시에 최신 버전인 ELMAH 1.0 베타 3 (빌드 10617)이이 자습서에서 제공 하는 다운로드에 포함 되어 있습니다. 또는 [ELMAH 웹 사이트](https://code.google.com/p/elmah/) 를 방문 하 여 최신 버전을 가져오거나 소스 코드를 다운로드할 수 있습니다. 데스크톱의 폴더에 대 한 ELMAH 다운로드를 추출 하 고 ELMAH 어셈블리 파일 (`Elmah.dll`)을 찾습니다.

> [!NOTE]
> `Elmah.dll` 파일은 다운로드의 `Bin` 폴더에 있으며, 다른 .NET Framework 버전에 대 한 하위 폴더와 릴리스 및 디버그 빌드에 대 한 하위 폴더가 있습니다. 적절 한 프레임 워크 버전에 대 한 릴리스 빌드를 사용 합니다. 예를 들어 ASP.NET 3.5 웹 응용 프로그램을 빌드하는 경우 `Bin\net-3.5\Release` 폴더에서 `Elmah.dll` 파일을 복사 합니다.

그런 다음 솔루션 탐색기에서 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 참조 추가를 선택 하 여 Visual Studio를 열고 프로젝트에 어셈블리를 추가 합니다. 이렇게 하면 참조 추가 대화 상자가 나타납니다. 찾아보기 탭으로 이동 하 여 `Elmah.dll` 파일을 선택 합니다. 이 작업을 수행 하면 웹 응용 프로그램의 `Bin` 폴더에 `Elmah.dll` 파일이 추가 됩니다.

> [!NOTE]
> WAP (웹 응용 프로그램 프로젝트) 형식은 솔루션 탐색기에 `Bin` 폴더를 표시 하지 않습니다. 대신 References 폴더 아래에 이러한 항목을 나열 합니다.

`Elmah.dll` 어셈블리에는 ELMAH 시스템에서 사용 하는 클래스가 포함 되어 있습니다. 이러한 클래스는 다음 세 가지 범주 중 하나에 속합니다.

- **Http 모듈** -http 모듈은 `Error` 이벤트와 같은 `HttpApplication` 이벤트에 대 한 이벤트 처리기를 정의 하는 클래스입니다. ELMAH에는 여러 HTTP 모듈이 포함 되어 있으며 가장 germane 세 가지는 다음과 같습니다. 

    - `ErrorLogModule`-로그 원본에 대해 처리 되지 않은 예외를 기록 합니다.
    - `ErrorMailModule`-처리 되지 않은 예외의 세부 정보를 전자 메일 메시지로 보냅니다.
    - `ErrorFilterModule`-개발자 지정 필터를 적용 하 여 기록 되는 예외 및 무시 되는 예외를 확인 합니다.
- **Http 처리기** -http 처리기는 특정 형식의 요청에 대 한 태그 생성을 담당 하는 클래스입니다. ELMAH에는 오류 정보를 웹 페이지, RSS 피드 또는 쉼표로 구분 된 파일 (CSV)으로 렌더링 하는 HTTP 처리기가 포함 되어 있습니다.
- **오류 로그 원본** -기본적으로 ELMAH는 메모리, Microsoft SQL Server 데이터베이스, Microsoft Access 데이터베이스, Oracle 데이터베이스, XML 파일, SQLite 데이터베이스 또는 Vista DB 데이터베이스에 오류를 기록할 수 있습니다. 상태 모니터링 시스템과 마찬가지로 ELMAH 아키텍처는 공급자 모델을 사용 하 여 빌드 되었으므로 필요한 경우 고유한 사용자 지정 로그 원본 공급자를 만들고 원활 하 게 통합할 수 있습니다.

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>2 단계: ELMAH의 HTTP 모듈 및 처리기 등록

`Elmah.dll` 파일에는 처리 되지 않은 예외를 자동으로 기록 하 고 웹 페이지에서 오류 정보를 표시 하는 데 필요한 HTTP 모듈 및 처리기가 포함 되어 있지만 웹 응용 프로그램의 구성에 명시적으로 등록 해야 합니다. `ErrorLogModule` HTTP 모듈이 등록 되 면 `HttpApplication`의 `Error` 이벤트를 구독 합니다. 이 이벤트가 발생할 때마다 `ErrorLogModule`는 지정 된 로그 원본에 예외의 세부 정보를 기록 합니다. 다음 섹션인 "ELMAH 구성"에서 로그 원본 공급자를 정의 하는 방법을 알아봅니다. `ErrorLogPageFactory` HTTP 처리기 팩터리는 웹 페이지에서 오류 로그를 볼 때 태그를 생성 합니다.

HTTP 모듈 및 처리기를 등록 하는 특정 구문은 사이트를 켜는 웹 서버에 따라 달라 집니다. ASP.NET 개발 서버 및 Microsoft의 IIS 버전 6.0 및 이전 버전의 경우 HTTP 모듈 및 처리기는 `<system.web>` 요소 내에 표시 되는 `<httpModules>` 및 `<httpHandlers>` 섹션에 등록 됩니다. IIS 7.0를 사용 하는 경우 `<system.webServer>` 요소의 `<modules>` 및 `<handlers>` 섹션에 등록 해야 합니다. 다행히 사용 중인 웹 서버에 관계 없이 *두 위치 모두* 에서 HTTP 모듈 및 처리기를 정의할 수 있습니다. 이 옵션은 사용 중인 웹 서버에 관계 없이 개발 및 프로덕션 환경에서 동일한 구성을 사용할 수 있도록 하는 가장 이식 가능한 것입니다.

먼저 `ErrorLogModule` HTTP 모듈을 등록 하 고 `<system.web>`의 `<httpModules>` 및 `<httpHandlers>` 섹션에서 `ErrorLogPageFactory` HTTP 처리기를 등록 합니다. 구성에서 이러한 두 요소를 이미 정의한 경우에는 ELMAH의 HTTP 모듈 및 처리기에 대 한 `<add>` 요소를 포함 하기만 하면 됩니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample1.xml)]

그런 다음 `<system.webServer>` 요소에 ELMAH의 HTTP 모듈 및 처리기를 등록 합니다. 이전 처럼이 요소가 구성에 아직 없는 경우 추가 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample2.xml)]

기본적으로 IIS 7은 불만 섹션에 HTTP 모듈 및 처리기가 등록 된 경우 `<system.web>`에 합니다. `<validation>` 요소의 `validateIntegratedModeConfiguration` 특성은 IIS 7에 이러한 오류 메시지를 표시 하지 않도록 지시 합니다.

`ErrorLogPageFactory` HTTP 처리기를 등록 하는 구문은 `elmah.axd`로 설정 된 `path` 특성을 포함 합니다. 이 특성은 `elmah.axd` 페이지에 대 한 요청이 도착 하는 경우 `ErrorLogPageFactory` HTTP 처리기에서 요청을 처리 하도록 웹 응용 프로그램에 알립니다. 이 자습서의 뒷부분에 나오는 작업에서 `ErrorLogPageFactory` HTTP 처리기가 표시 됩니다.

### <a name="step-3-configuring-elmah"></a>3 단계: ELMAH 구성

ELMAH는 `<elmah>`이라는 사용자 지정 구성 섹션의 웹 사이트 `Web.config` 파일에서 해당 구성 옵션을 찾습니다. `Web.config`에서 사용자 지정 섹션을 사용 하려면 먼저 `<configSections>` 요소에 정의 해야 합니다. `Web.config` 파일을 열고 `<configSections>`에 다음 태그를 추가 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample3.xml)]

> [!NOTE]
> ASP.NET 1.x 응용 프로그램에 대해 ELMAH를 구성 하는 경우 위의 `<section>` 요소에서 `requirePermission="false"` 특성을 제거 합니다.

위의 구문은 `<security>`, `<errorLog>`, `<errorMail>`및 `<errorFilter>`사용자 지정 `<elmah>` 섹션과 하위 섹션을 등록 합니다.

그런 다음 `<elmah>` 섹션을 `Web.config`에 추가 합니다. 이 섹션은 `<system.web>` 요소와 같은 수준에 표시 되어야 합니다. `<elmah>` 섹션 내에서 다음과 같은 `<security>` 및 `<errorLog>` 섹션을 추가 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample4.xml)]

`<security>` 섹션의 `allowRemoteAccess` 특성은 원격 액세스가 허용 되는지 여부를 나타냅니다. 이 값을 0으로 설정 하면 오류 로그 웹 페이지만 로컬로 볼 수 있습니다. 이 특성을 1로 설정 하면 원격 및 로컬 방문자 모두에 대해 오류 로그 웹 페이지가 활성화 됩니다. 지금은 원격 방문자에 대 한 오류 로그 웹 페이지를 사용 하지 않도록 설정 하겠습니다. 이러한 작업을 수행 하는 보안 문제에 대해 논의할 기회가 있으면 나중에 원격 액세스를 허용 합니다.

`<errorLog>` 섹션에서는 오류 정보를 기록 하는 위치를 결정 하는 오류 로그 원본을 정의 합니다. 상태 모니터링 시스템의 `<providers>` 섹션과 유사 합니다. 위의 구문은 `SqlErrorLog` 클래스를 오류 로그 원본으로 지정 합니다 .이 오류는 `connectionStringName` 특성 값으로 지정 된 Microsoft SQL Server 데이터베이스에 오류를 기록 합니다.

> [!NOTE]
> ELMAH는 XML 파일, Microsoft Access 데이터베이스, Oracle 데이터베이스 및 기타 데이터 저장소에 오류를 기록 하는 데 사용할 수 있는 추가 오류 로그 공급자를 제공 합니다. 이러한 대체 오류 로그 공급자를 사용 하는 방법에 대 한 자세한 내용은 ELMAH 다운로드와 함께 제공 되는 샘플 `Web.config` 파일을 참조 하세요.

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>4 단계: 오류 로그 원본 인프라 만들기

ELMAH의 `SqlErrorLog` 공급자는 지정 된 Microsoft SQL Server 데이터베이스에 오류 정보를 기록 합니다. `SqlErrorLog` 공급자는이 데이터베이스에 `ELMAH_Error` 라는 테이블이 있고 `ELMAH_GetErrorsXml`, `ELMAH_GetErrorXml`및 `ELMAH_LogError`라는 세 개의 저장 프로시저를 포함 합니다. ELMAH 다운로드에는이 테이블 및 저장 프로시저를 만들기 위한 T-sql을 포함 하는 `db` 폴더에 `SQLServer.sql` 라는 파일이 포함 되어 있습니다. `SqlErrorLog` 공급자를 사용 하려면 데이터베이스에서 다음 문을 실행 해야 합니다.

**그림 1** 과 **2** 는 `SqlErrorLog` 공급자에 필요한 데이터베이스 개체가 추가 된 후 Visual Studio의 데이터베이스 탐색기을 보여 줍니다.

[![](logging-error-details-with-elmah-vb/_static/image2.png)](logging-error-details-with-elmah-vb/_static/image1.png)

**그림 1**: `SqlErrorLog` 공급자가 `ELMAH_Error` 테이블에 오류 기록

[![](logging-error-details-with-elmah-vb/_static/image4.png)](logging-error-details-with-elmah-vb/_static/image3.png)

**그림 2**: `SqlErrorLog` 공급자가 세 개의 저장 프로시저를 사용 합니다.

## <a name="elmah-in-action"></a>ELMAH 동작

이 시점에서 ELMAH를 웹 응용 프로그램에 추가 하 고, `ErrorLogModule` HTTP 모듈 및 `ErrorLogPageFactory` HTTP 처리기를 등록 하 고, `Web.config`에서 ELMAH의 구성 옵션을 지정 하 고, `SqlErrorLog` 오류 로그 공급자에 필요한 데이터베이스 개체를 추가 했습니다. 이제 ELMAH 작업을 확인할 준비가 되었습니다. 책 리뷰 웹 사이트를 방문 하 여 `Genre.aspx?ID=foo`, `NoSuchPage.aspx`와 같은 존재 하지 않는 페이지와 같은 런타임 오류를 생성 하는 페이지를 방문 하세요. 이러한 페이지를 방문할 때 표시 되는 내용은 `<customErrors>` 구성과 로컬에서 또는 원격으로 방문 하 고 있는지 여부에 따라 달라 집니다. (이 항목의 리프레셔에 대 한 [ *사용자 지정 오류 페이지 표시* 자습서](displaying-a-custom-error-page-vb.md) 를 다시 참조 하세요.)

ELMAH는 처리 되지 않은 예외가 발생할 때 사용자에 게 표시 되는 내용에 영향을 주지 않습니다. 단지 세부 정보를 기록 합니다. 이 오류 로그는 웹 사이트의 루트에서 `elmah.axd` 웹 페이지에서 액세스할 수 있습니다 (예: `http://localhost/BookReviews/elmah.axd`). 이 파일은 프로젝트에 실제로 존재 하지는 않지만 `elmah.axd`에 대 한 요청이 들어오면 런타임에서는 `ErrorLogPageFactory` HTTP 처리기로 디스패치 합니다. 그러면 브라우저에 다시 전송 된 태그가 생성 됩니다.

> [!NOTE]
> `elmah.axd` 페이지를 사용 하 여 ELMAH에서 테스트 오류를 생성 하도록 지시할 수도 있습니다. `elmah.axd/test` (예: `http://localhost/BookReviews/elmah.axd/test`)를 방문 하면 ELMAH는 "이는 안전 하 게 무시할 수 있는 테스트 예외입니다." 라는 오류 메시지를 포함 하는 `Elmah.TestException`형식의 예외를 throw 합니다.

**그림 3** 에서는 개발 환경에서 `elmah.axd`를 방문할 때 발생 하는 오류 로그를 보여 줍니다.

[![](logging-error-details-with-elmah-vb/_static/image6.png)](logging-error-details-with-elmah-vb/_static/image5.png)

**그림 3**: 웹 페이지에서 오류 로그를 표시 `Elmah.axd`  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image7.png))

**그림 3** 의 오류 로그에는 6 개의 오류 항목이 포함 되어 있습니다. 각 항목에는 HTTP 상태 코드 (404 또는 500, 이러한 오류의 경우), 형식, 설명, 오류가 발생 했을 때 로그온 한 사용자의 이름 및 날짜와 시간이 포함 됩니다. 세부 정보 링크를 클릭 하면 오류가 발생 했을 때의 서버 변수 값과 함께 오류 정보 노랑 화면 ( **그림 4**참조)에 표시 된 것과 동일한 오류 메시지를 포함 하는 페이지가 표시 됩니다 ( **그림 5**참조). 오류 정보가 저장 된 원시 XML을 볼 수도 있습니다. 여기에는 HTTP POST 헤더의 값과 같은 추가 정보가 포함 됩니다.

[![](logging-error-details-with-elmah-vb/_static/image9.png)](logging-error-details-with-elmah-vb/_static/image8.png)

**그림 4**: 오류 세부 정보 보기  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image10.png))

[![](logging-error-details-with-elmah-vb/_static/image12.png)](logging-error-details-with-elmah-vb/_static/image11.png)

**그림 5**: 오류 발생 시 서버 변수 컬렉션의 값 탐색  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image13.png))

ELMAH를 프로덕션 웹 사이트에 배포 하는 작업은 다음과 같습니다.

- 프로덕션의 `Bin` 폴더에 `Elmah.dll` 파일 복사
- ELMAH 관련 구성 설정을 프로덕션에 사용 되는 `Web.config` 파일로 복사
- 프로덕션 데이터베이스에 오류 로그 원본 인프라 추가

이전 자습서에서는 개발에서 프로덕션으로 파일을 복사 하는 기술에 대해 살펴보았습니다. 프로덕션 데이터베이스에서 오류 로그 원본 인프라를 가져오는 가장 쉬운 방법은 SQL Server Management Studio를 사용 하 여 프로덕션 데이터베이스에 연결한 다음 `SqlServer.sql` 스크립트 파일을 실행 하 여 필요한 테이블 및 저장 프로시저를 만드는 것입니다.

### <a name="viewing-the-error-details-page-on-production"></a>프로덕션에서 오류 정보 페이지 보기

프로덕션에 사이트를 배포한 후 프로덕션 웹 사이트를 방문 하 여 처리 되지 않은 예외를 생성 합니다. 개발 환경에서와 같이 ELMAH는 처리 되지 않은 예외가 발생할 때 표시 되는 오류 페이지에 영향을 주지 않습니다. 대신 단지 오류를 기록 합니다. 프로덕션 환경에서 오류 로그 페이지 (`elmah.axd`)를 방문 하려고 하면 **그림 6**에 표시 된 금지 된 페이지를 제공할 됩니다.

[![](logging-error-details-with-elmah-vb/_static/image15.png)](logging-error-details-with-elmah-vb/_static/image14.png)

**그림 6**: 기본적으로 원격 방문자가 오류 로그 웹 페이지를 볼 수 없음  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image16.png))

ELMAH 구성의 `<security>` 섹션에서 `allowRemoteAccess` 특성을 0으로 설정 하면 원격 사용자가 오류 로그를 볼 수 없습니다. 오류 정보에서 보안 취약점 또는 기타 중요 한 정보를 확인할 수 있으므로 익명 방문자가 오류 로그를 볼 수 없도록 하는 것이 중요 합니다. 이 특성을 1로 설정 하 고 오류 로그에 대 한 원격 액세스를 사용 하도록 결정 한 경우에는 권한 있는 방문자만 액세스할 수 있도록 `elmah.axd` 경로를 잠가야 합니다. 이는 `Web.config` 파일에 `<location>` 요소를 추가 하 여 수행할 수 있습니다.

다음 구성은 관리자 역할의 사용자만 오류 로그 웹 페이지에 액세스할 수 있도록 허용 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample5.xml)]

> [!NOTE]
> 관리자 역할 및 시스템의 세 사용자 (Scott, Jisun 및 Alice)가 [ *애플리케이션 서비스 자습서를 사용 하는 웹 사이트 구성* ](configuring-a-website-that-uses-application-services-vb.md)에 추가 되었습니다. Scott 및 Jisun 사용자는 관리자 역할의 멤버입니다. 인증 및 권한 부여에 대 한 자세한 내용은 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 참조 하세요.

이제 원격 사용자가 프로덕션 환경에서 오류 로그를 볼 수 있습니다. 오류 로그 웹 페이지의 스크린 샷에 대해서는 **그림 3**, **4**및 **5** 를 다시 참조 하세요. 그러나 익명 또는 비관리자 사용자가 오류 로그 페이지를 보려고 하면 **그림 7** 에 표시 된 것 처럼 자동으로 로그인 페이지 (`Login.aspx`)로 리디렉션됩니다.

[![](logging-error-details-with-elmah-vb/_static/image18.png)](logging-error-details-with-elmah-vb/_static/image17.png)

**그림 7**: 권한이 없는 사용자가 자동으로 로그인 페이지로 리디렉션됩니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image19.png))

### <a name="programmatically-logging-errors"></a>프로그래밍 방식으로 오류 로깅

ELMAH의 `ErrorLogModule` HTTP 모듈은 지정 된 로그 원본에 처리 되지 않은 예외를 자동으로 기록 합니다. 또는 `ErrorSignal` 클래스와 해당 `Raise` 메서드를 사용 하 여 처리 되지 않은 예외를 발생 시 키 지 않고도 오류를 기록할 수 있습니다. `Raise` 메서드는 `Exception` 개체로 전달 되 고, 예외가 throw 되 고 처리 되지 않고 ASP.NET 런타임에 도달 했을 때로 기록 됩니다. 그러나이 차이점은 `Raise` 메서드가 호출 된 후 요청이 정상적으로 계속 실행 되는 반면 throw 된 처리 되지 않은 예외는 요청의 정상적인 실행을 중단 하 고 ASP.NET 런타임이 구성 된 오류 페이지를 표시 하도록 하는 것입니다.

`ErrorSignal` 클래스는 실패할 수 있는 일부 동작이 있지만 해당 오류가 수행 되는 전체 작업에 치명적이 지 않은 경우에 유용 합니다. 예를 들어, 웹 사이트에는 사용자의 입력을 받아 데이터베이스에 저장 한 다음 사용자에 게 정보가 처리 되었음을 알리는 전자 메일을 보내는 양식이 포함 될 수 있습니다. 정보를 데이터베이스에 성공적으로 저장 했지만 전자 메일 메시지를 보낼 때 오류가 발생 하는 경우 어떻게 되나요? 한 가지 옵션은 예외를 throw 하 고 오류 페이지로 사용자를 보내는 것입니다. 그러나 이렇게 하면 사용자가 입력 한 정보가 저장 되지 않은 것으로 간주 될 수 있습니다. 또 다른 방법은 전자 메일 관련 오류를 기록 하는 것 이지만 사용자의 경험을 변경 하는 것은 아닙니다. 이 경우 `ErrorSignal` 클래스가 유용 합니다.

[!code-vb[Main](logging-error-details-with-elmah-vb/samples/sample6.vb)]

## <a name="error-notification-via-email"></a>전자 메일을 통한 오류 알림

데이터베이스에 오류를 기록 하는 것과 함께 ELMAH는 지정 된 받는 사람에 게 오류 정보를 전자 메일로 보내기 위해 구성할 수도 있습니다. 이 기능은 `ErrorMailModule` HTTP 모듈에서 제공 합니다. 따라서 전자 메일을 통해 오류 정보를 보내려면이 HTTP 모듈을 `Web.config`에 등록 해야 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample7.xml)]

그런 다음 `<elmah>` 요소의 `<errorMail>` 섹션에서 전자 메일의 보낸 사람 및 받는 사람, 제목 및 전자 메일이 비동기식으로 전송 되는지 여부를 나타내는 오류 전자 메일에 대 한 정보를 지정 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample8.xml)]

위의 설정이 적용 된 상태에서 런타임 오류가 발생할 때마다 ELMAH는 오류 세부 정보를 사용 하 여 support@example.com 전자 메일을 보냅니다. ELMAH의 오류 전자 메일에는 오류 정보 웹 페이지에 표시 된 것과 같은 정보, 오류 메시지, 스택 추적 및 서버 변수가 포함 되어 있습니다 ( **그림 4** 및 **5**참조). 오류 전자 메일에는 첨부 파일 (`YSOD.html`)로 서의 예외 정보 노랑 화면 ()도 포함 됩니다.

**그림 8** 에서는 `Genre.aspx?ID=foo`를 방문 하 여 생성 된 ELMAH의 오류 전자 메일을 보여 줍니다. **그림 8** 에는 오류 메시지 및 스택 추적만 표시 되지만 서버 변수는 전자 메일의 본문에 추가로 포함 됩니다.

[![](logging-error-details-with-elmah-vb/_static/image21.png)](logging-error-details-with-elmah-vb/_static/image20.png)

**그림 8**: 전자 메일을 통해 오류 정보를 보내도록 ELMAH를 구성할 수 있습니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-elmah-vb/_static/image22.png))

## <a name="only-logging-errors-of-interest"></a>관심 있는 오류만 기록

기본적으로 ELMAH는 404 및 기타 HTTP 오류를 포함 하 여 처리 되지 않은 모든 예외에 대 한 세부 정보를 기록 합니다. 오류 필터링을 사용 하 여 이러한 오류 또는 다른 유형의 오류를 무시 하도록 ELMAH에 지시할 수 있습니다. 필터링 논리는 `Web.config`에 등록 하 여 필터링 논리를 사용 해야 하는 ELMAH의 `ErrorFilterModule` HTTP 모듈을 통해 수행 됩니다. 필터링 규칙은 `<errorFilter>` 섹션에서 지정 합니다.

다음 태그는 ELMAH에서 404 오류를 기록 하지 않도록 지시 합니다.

[!code-xml[Main](logging-error-details-with-elmah-vb/samples/sample9.xml)]

> [!NOTE]
> 오류 필터링을 사용 하려면 `ErrorFilterModule` HTTP 모듈을 등록 해야 합니다.

`<test>` 섹션 내의 `<equal>` 요소를 assertion 이라고 합니다. 어설션이 true로 평가 되 면 오류가 ELMAH 로그에서 필터링 됩니다. `<greater>`, `<greater-or-equal>`, `<not-equal>`, `<lesser>`, `<lesser-or-equal>`등을 비롯 한 다른 어설션을 사용할 수 있습니다. `<and>` 및 `<or>` 부울 연산자를 사용 하 여 어설션을 결합할 수도 있습니다. 무엇 보다도 간단한 JavaScript 식을 어설션으로 포함 하거나 또는 Visual Basic에서 C# 사용자 고유의 어설션을 작성할 수도 있습니다.

ELMAH의 오류 필터링 기능에 대 한 자세한 내용은 [elmah wiki](https://code.google.com/p/elmah/w/list)의 [오류 필터링 섹션](https://code.google.com/p/elmah/wiki/ErrorFiltering) 을 참조 하십시오.

## <a name="summary"></a>요약

ELMAH는 ASP.NET 웹 응용 프로그램에서 오류를 기록 하는 간단 하 고 강력한 메커니즘을 제공 합니다. Microsoft의 상태 모니터링 시스템과 마찬가지로 ELMAH는 데이터베이스에 오류를 기록 하 고 전자 메일을 통해 개발자에 게 오류 정보를 보낼 수 있습니다. 상태 모니터링 시스템과 달리 ELMAH에는 Microsoft SQL Server, Microsoft Access, Oracle, XML 파일 등 다양 한 오류 로그 데이터 저장소에 대 한 기본 지원이 포함 됩니다. 또한 ELMAH는 오류 로그를 확인 하 고 웹 페이지에서 특정 오류에 대 한 세부 정보를 `elmah.axd`하는 기본 메커니즘을 제공 합니다. `elmah.axd` 페이지는 또한 오류 정보를 RSS 피드 또는 쉼표로 구분 된 값 파일 (CSV)로 렌더링할 수 있습니다 .이 파일은 Microsoft Excel을 사용 하 여 읽을 수 있습니다. 선언적 또는 프로그래밍 방식 어설션을 사용 하 여 로그에서 오류를 필터링 하도록 ELMAH에 지시할 수도 있습니다. 및 ELMAH는 ASP.NET 버전 1.x 응용 프로그램에서 사용할 수 있습니다.

배포 된 모든 응용 프로그램에는 처리 되지 않은 예외를 자동으로 기록 하 고 개발 팀에 알림을 보내기 위한 몇 가지 메커니즘이 있어야 합니다. 상태 모니터링 또는 ELMAH를 사용 하 여이를 수행 하는지 여부를 나타냅니다. 즉, 상태 모니터링 또는 ELMAH를 사용 하는지에 관계 없이 거의 중요 하지 않습니다. 두 시스템을 평가한 다음 사용자의 요구에 가장 적합 한 시스템을 선택 합니다. 근본적으로 중요 한 점은 프로덕션 환경에서 처리 되지 않은 예외를 기록 하기 위해 일부 메커니즘을 배치 하는 것입니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ELMAH-오류 로깅 모듈 및 처리기](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 프로젝트 페이지](https://code.google.com/p/elmah/) (소스 코드, 샘플, wiki)
- [ELMAH를 웹 응용 프로그램에 연결 하 여 처리 되지 않은 예외 Catch](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx) (비디오)
- [보안 오류 로그 페이지](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [HTTP 모듈 및 처리기를 사용 하 여 플러그형 ASP.NET 구성 요소 만들기](https://msdn.microsoft.com/library/aa479332.aspx)
- [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [이전](logging-error-details-with-asp-net-health-monitoring-vb.md)
> [다음](precompiling-your-website-vb.md)
