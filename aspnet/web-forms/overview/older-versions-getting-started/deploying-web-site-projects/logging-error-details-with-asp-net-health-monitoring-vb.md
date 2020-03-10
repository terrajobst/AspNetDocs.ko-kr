---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
title: VB (ASP.NET Health Monitoring)를 사용 하 여 오류 세부 정보 로깅 | Microsoft Docs
author: rick-anderson
description: Microsoft의 상태 모니터링 시스템은 처리 되지 않은 예외를 포함 하 여 다양 한 웹 이벤트를 편리 하 고 사용자 지정할 수 있는 방법을 제공 합니다. 이 자습서에서는 thr를 안내 합니다.
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 09a6c74e-936a-4c04-8547-5bb313a4e4a3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
msc.type: authoredcontent
ms.openlocfilehash: f57aca41771adfd9a7c7f38da1916db9197262da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507599"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-vb"></a>ASP.NET 상태 모니터링을 사용하여 오류 세부 정보 로깅(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_vb.pdf)

> Microsoft의 상태 모니터링 시스템은 처리 되지 않은 예외를 포함 하 여 다양 한 웹 이벤트를 편리 하 고 사용자 지정할 수 있는 방법을 제공 합니다. 이 자습서에서는 상태 모니터링 시스템을 설정 하 여 데이터베이스에 처리 되지 않은 예외를 기록 하 고 전자 메일 메시지를 통해 개발자에 게 알리는 과정을 안내 합니다.

## <a name="introduction"></a>소개

로깅은 배포 된 응용 프로그램의 상태를 모니터링 하 고 발생할 수 있는 문제를 진단 하는 데 유용한 도구입니다. 배포 된 응용 프로그램에서 발생 하는 오류를 기록 하 여 해결할 수 있도록 하는 것이 특히 중요 합니다. ASP.NET 응용 프로그램에서 처리 되지 않은 예외가 발생할 때마다 `Error` 이벤트가 발생 합니다. [앞의 자습서](processing-unhandled-exceptions-vb.md) 에서는 `Error` 이벤트에 대 한 이벤트 처리기를 만들어 오류를 개발자에 게 알리고 세부 정보를 기록 하는 방법을 살펴보았습니다. 그러나 ASP에서이 작업을 수행할 수 있기 때문에 오류 정보를 기록 하 고 개발자에 게 알릴 `Error` 이벤트 처리기를 만들 필요가 없습니다. 네트워크의 *상태 모니터링 시스템*입니다.

상태 모니터링 시스템은 ASP.NET 2.0에서 도입 되었으며 응용 프로그램이 나 요청의 수명 중에 발생 하는 이벤트를 기록 하 여 배포 된 ASP.NET 응용 프로그램의 상태를 모니터링 하도록 설계 되었습니다. 상태 모니터링 시스템에서 기록 하는 이벤트는 *상태 모니터링 이벤트* 또는 *웹 이벤트*라고 하며 다음을 포함 합니다.

- 응용 프로그램을 시작 하거나 중지 하는 경우와 같은 응용 프로그램 수명 이벤트
- 실패 한 로그인 시도 및 실패 한 URL 권한 부여 요청을 비롯 한 보안 이벤트
- 처리 되지 않은 예외를 포함 한 응용 프로그램 오류, 뷰 상태 구문 분석 예외, 요청 유효성 검사 예외 및 컴파일 오류 (다른 오류 유형)

상태 모니터링 이벤트가 발생 하면 지정 된 *로그 원본*수에 관계 없이 기록 될 수 있습니다. 상태 모니터링 시스템은 웹 이벤트를 Microsoft SQL Server 데이터베이스, Windows 이벤트 로그 또는 전자 메일 메시지를 통해 기록 하는 로그 원본과 함께 제공 됩니다. 로그 원본을 직접 만들 수도 있습니다.

사용 되는 로그 원본과 함께 상태 모니터링 시스템 로그의 이벤트는 `Web.config`에 정의 되어 있습니다. 몇 줄의 구성 태그를 사용 하 여 상태 모니터링을 사용 하 여 처리 되지 않은 모든 예외를 데이터베이스에 기록 하 고 전자 메일을 통해 예외를 알릴 수 있습니다.

## <a name="exploring-the-health-monitoring-systems-configuration"></a>상태 모니터링 시스템의 구성 살펴보기

상태 모니터링 시스템의 동작은 구성 정보에 의해 정의 되며,이는 `Web.config`의 [`<healthMonitoring>` 요소](https://msdn.microsoft.com/library/2fwh2ss9.aspx) 에 있습니다. 이 구성 섹션에서는 다음과 같은 세 가지 중요 한 정보를 정의 합니다.

1. 발생 한 상태 모니터링 이벤트는
2. 로그 원본 및
3. (1)에 정의 된 각 상태 모니터링 이벤트는 (2)에 정의 된 로그 원본에 매핑됩니다.

이 정보는 각각 [`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx), [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)및 [`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)의 세 가지 자식 구성 요소를 통해 지정 됩니다.

기본 상태 모니터링 시스템 구성 정보는 `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` 폴더의 `Web.config` 파일에서 찾을 수 있습니다. 이 기본 구성 정보는 다음과 같이 간단 하 게 나타내기 위해 일부 태그가 제거 됩니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample1.xml)]

관심 있는 상태 모니터링 이벤트는 상태 모니터링 이벤트의 클래스에 대해 사용자에 게 친숙 한 이름을 제공 하는 `<eventMappings>` 요소에 정의 됩니다. 위의 태그에서 `<eventMappings>` 요소는 사용자에 게 친숙 한 이름 "모든 오류"를 `WebBaseErrorEvent` 유형의 상태 모니터링 이벤트에 할당 하 고 "실패 감사" 이름을 `WebFailureAuditEvent`유형의 상태 모니터링 이벤트에 할당 합니다.

`<providers>` 요소는 로그 소스를 정의 하 여 사용자에 게 친숙 한 이름을 제공 하 고 로그 소스 관련 구성 정보를 지정 합니다. 첫 번째 `<add>` 요소는 `EventLogWebEventProvider` 클래스를 사용 하 여 지정 된 상태 모니터링 이벤트를 기록 하는 "EventLogProvider" 공급자를 정의 합니다. `EventLogWebEventProvider` 클래스는 Windows 이벤트 로그에 이벤트를 기록 합니다. 두 번째 `<add>` 요소는 `SqlWebEventProvider` 클래스를 통해 Microsoft SQL Server 데이터베이스에 이벤트를 기록 하는 "SqlWebEventProvider" 공급자를 정의 합니다. "SqlWebEventProvider" 구성은 다른 구성 옵션 중에서 데이터베이스의 연결 문자열 (`connectionStringName`)을 지정 합니다.

`<rules>` 요소는 `<eventMappings>` 요소에 지정 된 이벤트를 `<providers>` 요소의 로그 소스에 매핑합니다. 기본적으로 ASP.NET 웹 응용 프로그램은 모든 처리 되지 않은 예외를 기록 하 고 Windows 이벤트 로그에 감사 실패를 기록 합니다.

## <a name="logging-events-to-a-database"></a>데이터베이스에 이벤트 로깅

응용 프로그램의 `Web.config` 파일에 `<healthMonitoring>` 섹션을 추가 하 여 웹 응용 프로그램을 기반으로 상태 모니터링 시스템의 기본 구성을 사용자 지정할 수 있습니다. `<add>` 요소를 사용 하 여 `<eventMappings>`, `<providers>`및 `<rules>` 섹션에 추가 요소를 포함할 수 있습니다. 기본 구성에서 설정을 제거 하려면 `<remove>` 요소를 사용 하거나 `<clear />`를 사용 하 여 이러한 섹션 중 하나에서 모든 기본값을 제거 합니다. `SqlWebEventProvider` 클래스를 사용 하 여 Microsoft SQL Server 데이터베이스에 처리 되지 않은 모든 예외를 기록 하도록 책 리뷰 웹 응용 프로그램을 구성 하겠습니다.

`SqlWebEventProvider` 클래스는 상태 모니터링 시스템의 일부 이며 지정 된 SQL Server 데이터베이스에 상태 모니터링 이벤트를 기록 합니다. `SqlWebEventProvider` 클래스는 지정 된 데이터베이스에 `aspnet_WebEvent_LogEvent`라는 저장 프로시저를 포함 하는 것으로 예상 합니다. 이 저장 프로시저는 이벤트의 세부 정보를 전달 하 고 이벤트 세부 정보를 저장 하는 작업을 수행 합니다. 이 저장 프로시저나 이벤트 세부 정보를 저장 하는 테이블을 만들 필요는 없습니다. `aspnet_regsql.exe` 도구를 사용 하 여 이러한 개체를 데이터베이스에 추가할 수 있습니다.

> [!NOTE]
> `aspnet_regsql.exe` 도구는 ASP에 대 한 지원을 추가할 때 [ *애플리케이션 서비스 자습서를 사용 하는 웹 사이트 구성* ](configuring-a-website-that-uses-application-services-vb.md) 에서 다시 설명 되었습니다. NET의 응용 프로그램 서비스입니다. 따라서 서적 검토 웹 사이트의 데이터베이스에는 이벤트 정보를 `aspnet_WebEvent_Events`라는 테이블에 저장 하는 `aspnet_WebEvent_LogEvent` 저장 프로시저가 이미 포함 되어 있습니다.

필요한 저장 프로시저와 테이블을 데이터베이스에 추가 하 고 나면 처리 되지 않은 모든 예외를 데이터베이스에 기록 하도록 상태 모니터링에 지시 하는 것만 남았습니다. 웹 사이트의 `Web.config` 파일에 다음 태그를 추가 하 여이 작업을 수행 합니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample2.xml)]

위의 상태 모니터링 구성 태그는 `<clear />` 요소를 사용 하 여 `<eventMappings>`, `<providers>`및 `<rules>` 섹션에서 미리 정의 된 상태 모니터링 구성 정보를 초기화 합니다. 그런 다음 각 섹션에 단일 항목을 추가 합니다.

- `<eventMappings>` 요소는 처리 되지 않은 예외가 발생할 때마다 발생 하는 "모든 오류" 라는 중요 한 단일 상태 모니터링 이벤트를 정의 합니다.
- `<providers>` 요소는 `SqlWebEventProvider` 클래스를 사용 하는 "SqlWebEventProvider" 라는 단일 로그 소스를 정의 합니다. `connectionStringName` 특성은 `<connectionStrings>` 섹션에 정의 된 연결 문자열의 이름인 "ReviewsConnectionString"로 설정 되어 있습니다.
- 마지막으로 &lt;rules&gt; 요소는 "모든 오류" 이벤트가 "SqlWebEventProvider" 공급자를 사용 하 여 기록 되어야 함을 transpires 나타냅니다.

이 구성 정보는 상태 모니터링 시스템에서 모든 처리 되지 않은 예외를 책 리뷰 데이터베이스에 기록 하도록 지시 합니다.

> [!NOTE]
> `WebBaseErrorEvent` 이벤트는 서버 오류에 대해서만 발생 합니다. 검색 되지 않는 ASP.NET 리소스에 대 한 요청과 같은 HTTP 오류에는 발생 하지 않습니다. 이는 서버와 HTTP 오류 모두에 대해 발생 하는 `HttpApplication` 클래스의 `Error` 이벤트 동작과 다릅니다.

작동 중인 상태 모니터링 시스템을 보려면 웹 사이트를 방문 하 여 `Genre.aspx?ID=foo`를 방문 하 여 런타임 오류를 생성 합니다. 적절 한 오류 페이지가 표시 됩니다. 예외 세부 정보는 주황색 화면 (로컬에서 방문 하는 경우) 또는 사용자 지정 오류 페이지 (프로덕션에서 사이트를 방문할 때)로 표시 됩니다. 내부적으로 상태 모니터링 시스템은 오류 정보를 데이터베이스에 기록 합니다. `aspnet_WebEvent_Events` 테이블에는 레코드가 하나 있어야 합니다 ( **그림 1**참조). 이 레코드는 방금 발생 한 런타임 오류에 대 한 정보를 포함 합니다.

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image1.png)

**그림 1**: 오류 세부 정보가 `aspnet_WebEvent_Events` 테이블에 기록 됨  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-asp-net-health-monitoring-vb/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>웹 페이지에서 오류 로그 표시

웹 사이트의 현재 구성을 사용 하 여 상태 모니터링 시스템은 처리 되지 않은 모든 예외를 데이터베이스에 기록 합니다. 그러나 상태 모니터링은 웹 페이지를 통해 오류 로그를 확인 하는 메커니즘을 제공 하지 않습니다. 그러나 데이터베이스에서이 정보를 표시 하는 ASP.NET 페이지를 작성할 수 있습니다. 잠시 후에는 오류 세부 정보를 전자 메일 메시지로 보낼 수 있습니다.

이러한 페이지를 만드는 경우 권한 있는 사용자만 오류 정보를 볼 수 있도록 허용 하는 단계를 수행 해야 합니다. 사이트에서 이미 사용자 계정을 사용 하는 경우 URL 권한 부여 규칙을 사용 하 여 페이지에 대 한 액세스를 특정 사용자나 역할로 제한할 수 있습니다. 로그인 한 사용자에 따라 웹 페이지에 대 한 액세스 권한을 부여 하거나 제한 하는 방법에 대 한 자세한 내용은 내 [웹 사이트 보안 자습서](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)를 참조 하십시오.

> [!NOTE]
> 이후 자습서에서는 ELMAH 라는 대체 오류 로깅 및 알림 시스템을 탐색 합니다. ELMAH에는 웹 페이지와 RSS 피드 모두에서 오류 로그를 볼 수 있는 기본 제공 메커니즘이 포함 되어 있습니다.

## <a name="logging-events-to-email"></a>전자 메일에 이벤트 로깅

상태 모니터링 시스템에는 전자 메일 메시지에 이벤트를 "기록" 하는 로그 원본 공급자가 포함 되어 있습니다. 로그 원본에는 전자 메일 메시지 본문의 데이터베이스에 기록 되는 것과 동일한 정보가 포함 됩니다. 이 로그 소스를 사용 하 여 특정 상태 모니터링 이벤트가 발생할 때 개발자에 게 알릴 수 있습니다.

책 리뷰 웹 사이트의 구성을 업데이트 하 여 예외가 발생할 때마다 전자 메일을 받을 수 있습니다. 이 작업을 수행 하려면 다음 세 가지 작업을 수행 해야 합니다.

1. 전자 메일을 보내도록 ASP.NET 웹 응용 프로그램을 구성 합니다. 이는 `<system.net>` 구성 요소를 통해 전자 메일 메시지를 보내는 방법을 지정 하 여 수행 됩니다. ASP.NET 응용 프로그램에서 전자 메일 메시지를 전송 하는 방법에 대 한 자세한 내용은 [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx) 및 시스템의 [FAQ](http://systemnetmail.com/)를 참조 하세요.
2. `<providers>` 요소에 전자 메일 로그 원본 공급자를 등록 합니다.
3. "모든 오류" 이벤트를 단계 (2)에 추가 된 로그 원본 공급자에 매핑하는 `<rules>` 요소에 항목을 추가 합니다.

상태 모니터링 시스템에는 `SimpleMailWebEventProvider` 및 `TemplatedMailWebEventProvider`의 두 가지 전자 메일 로그 원본 공급자 클래스가 포함 됩니다. [`SimpleMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx) 는 이벤트 세부 정보를 포함 하는 일반 텍스트 전자 메일 메시지를 보내고 메일 본문의 사용자 지정을 거의 제공 하지 않습니다. [`TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 를 사용 하 여 렌더링 된 태그가 전자 메일 메시지의 본문으로 사용 되는 ASP.NET 페이지를 지정 합니다. [`TemplatedMailWebEventProvider` 클래스](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) 를 사용 하면 전자 메일 메시지의 내용과 형식을 훨씬 더 강력 하 게 제어할 수 있지만 전자 메일 메시지의 본문을 생성 하는 ASP.NET 페이지를 만들어야 하기 때문에 좀 더 선행 작업이 필요 합니다. 이 자습서에서는 `SimpleMailWebEventProvider` 클래스를 사용 하는 방법을 집중적으로 설명 합니다.

`SimpleMailWebEventProvider` 클래스에 대 한 로그 원본을 포함 하도록 `Web.config` 파일에서 상태 모니터링 시스템의 `<providers>` 요소를 업데이트 합니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample3.xml)]

위의 태그는 `SimpleMailWebEventProvider` 클래스를 로그 원본 공급자로 사용 하 고이를 "EmailWebEventProvider" 라는 이름으로 할당 합니다. 또한 `<add>` 특성에는 전자 메일 메시지의 주소 및 원본 주소와 같은 추가 구성 옵션이 포함 되어 있습니다.

전자 메일 로그 원본이 정의 되 면 상태 모니터링 시스템에서이 원본을 사용 하 여 처리 되지 않은 예외를 "기록" 하도록 지시 하는 것만 남았습니다. `<rules>` 섹션에서 새 규칙을 추가 하 여이 작업을 수행 합니다.

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample4.xml)]

`<rules>` 섹션에는 이제 두 가지 규칙이 포함 되어 있습니다. 첫 번째 이름은 "모든 오류를 전자 메일로 보내기"로, 처리 되지 않은 모든 예외를 "EmailWebEventProvider" 로그 원본으로 보냅니다. 이 규칙은 웹 사이트의 오류에 대 한 세부 정보를 지정 된의 주소로 보내는 효과를 적용 합니다. "모든 오류 데이터베이스 오류" 규칙은 사이트의 데이터베이스에 오류 세부 정보를 기록 합니다. 따라서 사이트에서 처리 되지 않은 예외가 발생할 때마다 세부 정보는 모두 데이터베이스에 기록 되 고 지정 된 전자 메일 주소로 전송 됩니다.

**그림 2** 에서는 `Genre.aspx?ID=foo`을 방문할 때 `SimpleMailWebEventProvider` 클래스에서 생성 한 전자 메일을 보여 줍니다.

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image4.png)

**그림 2**: 오류 정보는 전자 메일 메시지로 전송 됩니다.  
([전체 크기 이미지를 보려면 클릭](logging-error-details-with-asp-net-health-monitoring-vb/_static/image6.png))

## <a name="summary"></a>요약

ASP.NET 상태 모니터링 시스템은 관리자가 배포 된 웹 응용 프로그램의 상태를 모니터링할 수 있도록 설계 되었습니다. 상태 모니터링 이벤트는 응용 프로그램이 중지 되는 경우, 사용자가 사이트에 성공적으로 로그인 한 경우 또는 처리 되지 않은 예외가 발생 한 경우와 같은 특정 작업이 펼침 때 발생 합니다. 이러한 이벤트는 개수에 관계 없이 로그 원본에 기록할 수 있습니다. 이 자습서에서는 처리 되지 않은 예외에 대 한 세부 정보를 데이터베이스와 전자 메일 메시지를 통해 기록 하는 방법을 살펴보았습니다.

이 자습서에서는 상태 모니터링을 사용 하 여 처리 되지 않은 예외를 기록 하는 방법에 중점을 두고 있지만 상태 모니터링은 배포 된 ASP.NET 응용 프로그램의 전반적인 상태를 측정 하 고 다양 한 상태 모니터링 이벤트와 로그 원본을 포함 합니다. 여기에서 탐색 했습니다. 그에 따라 필요에 따라 사용자 고유의 상태 모니터링 이벤트와 로그 원본을 만들 수 있습니다. 상태 모니터링에 대해 자세히 알아보려면 먼저 [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)의 [상태 모니터링 FAQ](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)를 참조 하세요. 이에 따라 [방법: ASP.NET 2.0에서 상태 모니터링 사용](https://msdn.microsoft.com/library/ms998306.aspx)을 참조 하세요.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 상태 모니터링 개요](https://msdn.microsoft.com/library/bb398933.aspx)
- [ASP.NET의 상태 모니터링 시스템 구성 및 사용자 지정](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [FAQ-ASP.NET 2.0의 상태 모니터링](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [방법: 상태 모니터링 알림에 대 한 전자 메일 보내기](https://msdn.microsoft.com/library/ms227553.aspx)
- [방법: ASP.NET에서 상태 모니터링 사용](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET의 상태 모니터링](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [이전](processing-unhandled-exceptions-vb.md)
> [다음](logging-error-details-with-elmah-vb.md)
