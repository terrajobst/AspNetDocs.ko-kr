---
uid: aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
title: ASP.NET에서 수행할 수 없는 작업 및 수행 하는 작업 Microsoft Docs
author: Rick-Anderson
description: 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자가 수행 하는 몇 가지 일반적인 실수에 대해 설명 합니다. 이러한 동작을 방지 하기 위해 수행 해야 할 작업에 대 한 권장 사항을 제공 합니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: c39b9965-545c-4b04-8f55-21be7f28a9e5
msc.legacyurl: /aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
msc.type: authoredcontent
ms.openlocfilehash: 980d3544df70643043391e6573803ce21b3a824f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500135"
---
# <a name="what-not-to-do-in-aspnet-and-what-to-do-instead"></a>ASP.NET에서 하지 말아야 하는 일과 해야 하는 일

> 이 항목에서는 ASP.NET 웹 프로젝트 내에서 사용자가 수행 하는 몇 가지 일반적인 실수에 대해 설명 합니다. 이러한 일반적인 실수를 방지 하기 위해 수행 해야 하는 작업에 대 한 권장 사항을 제공 합니다. **Damian Edwards** 의 개발자 회의에서 [프레젠테이션을](http://vimeo.com/68390507) 기반으로 합니다.

## <a name="disclaimer"></a>고지 사항

이 항목은 응용 프로그램의 보안 및 효율성을 보장 하기 위한 전체 가이드로 제공 되지 않습니다. 이 항목에 설명 되어 있지 않은 보안 및 성능에 대 한 모범 사례를 따라야 합니다. .NET 클래스 및 프로세스와 관련 된 일반적인 실수를 방지 하는 방법만 제안 합니다.

## <a name="overview"></a>개요

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [표준 준수](#standards)

    - [제어 어댑터](#adapters)
    - [컨트롤의 스타일 속성](#styleprop)
    - [페이지 및 컨트롤 콜백](#callback)
    - [브라우저 기능 검색](#browsercap)
- [보안](#security)

    - [요청 유효성 검사](#validation)
    - [쿠키 없는 폼 인증 및 세션](#cookieless)
    - [EnableViewStateMac](#viewstatemac)
    - [보통 신뢰](#medium)
    - [&lt;appSettings&gt;](#appsettings)
    - [UrlPathEncode](#urlpathencode)
- [안정성 및 성능](#performance)

    - [PreSendRequestHeaders 및 보도 Endrequestcontent](#presend)
    - [Web Forms를 사용 하는 비동기 페이지 이벤트](#asyncevents)
    - [시작 및 잊어버린 작업](#fire)
    - [요청 엔터티 본문](#requestentity)
    - [응답. 리디렉션 및 응답. 끝](#redirect)
    - [EnableViewState 및 ViewStateMode](#viewstatemode)
    - [SqlMembershipProvider](#sqlprovider)
    - [장기 실행 요청 (> 110 초)](#long)

<a id="standards"></a>

## <a name="standards-compliance"></a>표준 준수

<a id="adapters"></a>

### <a name="control-adapters"></a>제어 어댑터

권장 사항: 적응 렌더링에 컨트롤 어댑터 사용을 중지 하 고 대신 CSS 미디어 쿼리 및 표준 규격 HTML을 사용 합니다.

컨트롤 어댑터는 다른 장치 및 환경에 맞게 사용자 지정 된 프레젠테이션 코드를 렌더링 하기 위해 .NET 2.0에서 도입 되었습니다. 이제 CSS 및 HTML을 사용 하 여이 적응형 렌더링을 수행할 수 있습니다. 컨트롤 어댑터 사용을 중지 하 고 기존 어댑터를 CSS 및 HTML로 변환 해야 합니다.

자세한 내용은 [미디어 쿼리](http://www.w3.org/TR/css3-mediaqueries/) 및 [방법: ASP.NET Web Forms/MVC 응용 프로그램에 모바일 페이지 추가](../../../whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application.md)를 참조 하세요.

<a id="styleprop"></a>

### <a name="style-properties-on-controls"></a>컨트롤의 스타일 속성

권장 사항: 컨트롤 태그에서 스타일 값 설정을 중지 하 고 대신 CSS 스타일 시트에서 형식 지정 값을 설정 합니다.

웹 서버 컨트롤에는 인라인 스타일 속성을 설정 하는 데 사용할 수 있는 수십 개의 속성이 포함 되어 있습니다. 예를 들어 ForeColor 속성은 컨트롤에 대 한 텍스트의 색을 설정 합니다. CSS 스타일 시트를 통해 이와 동일한 효과를 보다 효율적으로 수행할 수 있습니다. 스타일 시트를 사용 하면 스타일 값을 중앙 집중화 하 고 응용 프로그램 전체에서 이러한 값을 설정 하지 않을 수 있습니다.

다음 예제에서는 텍스트를 빨강으로 설정 하는 CSS 클래스를 보여 줍니다.

[!code-css[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample1.css)]

다음 예제에서는 CSS 클래스를 동적으로 적용 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample2.cs)]

<a id="callback"></a>

### <a name="page-and-control-callbacks"></a>페이지 및 컨트롤 콜백

권장 사항: 페이지 및 컨트롤 콜백 사용을 중지 하 고 대신 AJAX, UpdatePanel, MVC 동작 메서드, Web API 또는 SignalR 중 하나를 사용 합니다.

이전 버전의 ASP.NET에서는 페이지 및 컨트롤 콜백 메서드를 사용 하 여 전체 페이지를 새로 고치지 않고 웹 페이지의 일부를 업데이트할 수 있습니다. 이제 [AJAX](../../../ajax/index.md), [UpdatePanel](https://msdn.microsoft.com/library/bb386454.aspx), [MVC](../../../mvc/index.md), [Web API](../../../web-api/index.md) 또는 [SignalR](../../../signalr/index.md)를 통해 부분 페이지 업데이트를 수행할 수 있습니다. 친숙 한 Url 및 라우팅 문제를 일으킬 수 있으므로 콜백 메서드 사용을 중지 해야 합니다. 기본적으로 컨트롤은 콜백 메서드를 사용 하지 않지만 컨트롤에서이 기능을 사용 하도록 설정한 경우에는 사용 하지 않도록 설정 해야 합니다.

<a id="browsercap"></a>

### <a name="browser-capability-detection"></a>브라우저 기능 검색

권장 사항: 정적 브라우저 기능 검색 사용을 중지 하 고 대신 동적 기능 검색을 사용 합니다.

이전 버전의 ASP.NET에서는 각 브라우저에 대해 지원 되는 기능이 XML 파일에 저장 되었습니다. 정적 조회를 통해 기능 지원을 검색 하는 것은 최상의 방법이 아닙니다. 이제 [Modernizr](http://modernizr.com/)와 같은 기능 검색 프레임 워크를 사용 하 여 브라우저의 지원 되는 기능을 동적으로 검색할 수 있습니다. 기능 검색은 메서드 또는 속성을 사용한 다음 브라우저에서 원하는 결과를 생성 한 것인지 확인 하 여 지원을 결정 합니다. 기본적으로 Modernizr는 웹 응용 프로그램 템플릿에 포함 되어 있습니다.

<a id="security"></a>

## <a name="security"></a>보안

<a id="validation"></a>

### <a name="request-validation"></a>요청 유효성 검사

권장 사항: 사용자 입력의 유효성을 검사 하 고 사용자의 출력을 인코딩합니다.

요청 유효성 검사는 각 요청을 검사 하 고 인식 된 위협이 발견 되는 경우 요청을 중지 하는 ASP.NET의 기능입니다. 사이트 간 스크립팅 공격 으로부터 응용 프로그램을 보호 하기 위한 요청 유효성 검사에 의존 하지 않습니다. 대신 사용자의 모든 입력에 대 한 유효성을 검사 하 고 출력을 인코딩합니다. 일부 제한 된 경우에는 정규식을 사용 하 여 입력의 유효성을 검사할 수 있지만 더 복잡 한 경우에는 값이 허용 되는 값과 일치 하는지 확인 하는 .NET 클래스를 사용 하 여 사용자 입력의 유효성을 검사 해야 합니다.

다음 예제에서는 Uri 클래스에서 정적 메서드를 사용 하 여 사용자가 제공한 Uri가 유효한 지 여부를 확인 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample3.cs)]

그러나 Uri를 충분히 확인 하려면 `http` 또는 `https`를 지정 하는지 여부도 확인 해야 합니다. 다음 예에서는 인스턴스 메서드를 사용 하 여 Uri가 유효한 지 확인 합니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample4.cs)]

사용자 입력을 HTML로 렌더링 하거나 SQL 쿼리에서 사용자 입력을 포함 하기 전에 값을 인코딩하여 악성 코드가 포함 되지 않도록 합니다.

아래와 같이 &lt;%:%&gt; 구문을 사용 하 여 태그의 값을 HTML로 인코딩할 수 있습니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample5.aspx?highlight=1)]

또는 Razor 구문 아래와 같이 @로 HTML을 인코딩할 수 있습니다.

[!code-cshtml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample6.cshtml?highlight=1)]

다음 예제에서는 코드 숨김으로 값을 HTML로 인코딩하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample7.cs)]

SQL 명령에 대 한 값을 안전 하 게 인코딩하려면 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)와 같은 명령 매개 변수를 사용 합니다. <a id="cookieless"></a>

### <a name="cookieless-forms-authentication-and-session"></a>쿠키 없는 폼 인증 및 세션

권장 사항: 쿠키가 필요 합니다.

쿼리 문자열에 인증 정보를 전달 하는 것은 안전 하지 않습니다. 따라서 응용 프로그램에 인증이 포함 되어 있으면 쿠키가 필요 합니다. 쿠키가 중요 한 정보를 저장 하는 경우 쿠키에 대해 SSL을 요구 하는 것이 좋습니다.

다음 예제에서는 폼 인증에 SSL을 통해 전송 되는 쿠키가 필요한 경우 Web.config 파일에를 지정 하는 방법을 보여 줍니다.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample8.xml)]

<a id="viewstatemac"></a>

### <a name="enableviewstatemac"></a>EnableViewStateMac

권장 사항: false로 설정 하지 않습니다.

기본적으로 EnableViewStateMac는 true로 설정 됩니다. 응용 프로그램에서 뷰 상태를 사용 하지 않는 경우에도 EnableViewStateMac을 false로 설정 하지 마십시오. 이 값을 false로 설정 하면 응용 프로그램이 교차 사이트 스크립팅에 취약 해질 수 있습니다.

ASP.NET 4.5.2부터 런타임은 **EnableViewStateMac = true**를 적용 합니다. False로 설정한 경우에도 런타임은이 값을 무시 하 고 값을 true로 설정 하 여 진행 합니다. 자세한 내용은 [ASP.NET 4.5.2 및 EnableViewStateMac](https://blogs.msdn.com/b/webdev/archive/2014/05/07/asp-net-4-5-2-and-enableviewstatemac.aspx)를 참조 하세요.

다음 예제에서는 EnableViewStateMac를 true로 설정 하는 방법을 보여 줍니다. 이 값은 기본적으로 true 이므로 실제로이 값을 true로 설정할 필요가 없습니다. 그러나 응용 프로그램의 모든 페이지에서이 값을 false로 설정한 경우에는이 값을 즉시 수정 해야 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample9.aspx)]

<a id="medium"></a>

### <a name="medium-trust"></a>보통 신뢰

권장 사항: 보안 경계로 보통 신뢰 수준 또는 다른 신뢰 수준에 의존 하지 않습니다.

부분 신뢰는 응용 프로그램을 적절 하 게 보호 하지 않으므로 사용 하면 안 됩니다. 대신 완전 신뢰를 사용 하 고 신뢰할 수 없는 응용 프로그램을 별도의 응용 프로그램 풀에서 격리 합니다. 또한 고유한 id로 각 응용 프로그램 풀을 실행 합니다. 자세한 내용은 [ASP.NET 부분 신뢰에서 응용 프로그램 격리를 보장 하지 않음](https://support.microsoft.com/kb/2698981)을 참조 하세요.

<a id="appsettings"></a>

### <a name="ltappsettingsgt"></a>&lt;appSettings&gt;

권장 사항: &lt;appSettings&gt; 요소에서 보안 설정을 사용 하지 않도록 설정 하지 마십시오.

AppSettings 요소에는 보안 업데이트에 필요한 여러 값이 포함 되어 있습니다. 이러한 값은 변경 하거나 사용 하지 않도록 설정 하면 안 됩니다. 업데이트를 배포할 때 이러한 값을 사용 하지 않도록 설정 해야 하는 경우 배포를 완료 한 후 즉시 다시 사용 하도록 설정 합니다.

자세한 내용은 [ASP.NET AppSettings 요소](https://msdn.microsoft.com/library/hh975440.aspx)를 참조 하세요.

<a id="urlpathencode"></a>

### <a name="urlpathencode"></a>UrlPathEncode

권장 사항: 대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx) 를 사용 합니다.

UrlPathEncode 메서드가 매우 특정 브라우저 호환성 문제를 해결 하기 위해 .NET Framework에 추가 되었습니다. URL을 적절 하 게 인코딩하지 않고 교차 사이트 스크립팅 으로부터 응용 프로그램을 보호 하지 않습니다. 응용 프로그램에서 사용 하면 안 됩니다. 대신 [UrlEncode](https://msdn.microsoft.com/library/zttxte6w.aspx)를 사용 합니다.

다음 예제에서는 인코딩된 URL을 하이퍼링크 컨트롤에 대 한 쿼리 문자열 매개 변수로 전달 하는 방법을 보여 줍니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample10.cs)]

<a id="performance"></a>

## <a name="reliability-and-performance"></a>안정성 및 성능

<a id="presend"></a>

### <a name="presendrequestheaders-and-presendrequestcontent"></a>PreSendRequestHeaders 및 보도 Endrequestcontent

권장 사항: 관리 되는 모듈에서는 이러한 이벤트를 사용 하지 마십시오. 대신, 필요한 작업을 수행 하는 네이티브 IIS 모듈을 작성 합니다. [네이티브 코드 HTTP 모듈 만들기](https://msdn.microsoft.com/library/ms693629.aspx)를 참조 하세요.

네이티브 IIS 모듈과 함께 [PreSendRequestHeaders](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestheaders.aspx) 및 [보도 endrequestcontent](https://msdn.microsoft.com/library/system.web.httpapplication.presendrequestcontent.aspx) 이벤트를 사용할 수 있습니다.
> [!WARNING]
> `IHttpModule`를 구현 하는 관리 되는 모듈에 `PreSendRequestHeaders` 및 `PreSendRequestContent`를 사용 하지 마십시오. 이러한 속성을 설정 하면 비동기 요청을 사용 하 여 문제가 발생할 수 있습니다. 애플리케이션 요청 라우팅 (ARR) 및 websocket의 조합을 w3wp 충돌을 일으킬 수 있는 액세스 위반 예외가 발생할 수 있습니다. 예를 들어 iiscore! W3_CONTEXT_BASE::GetIsLastNotification + 68 iiscore.dll에서 액세스 위반 예외 (0xC0000005) 발생 했습니다.

<a id="asyncevents"></a>

### <a name="asynchronous-page-events-with-web-forms"></a>Web forms를 사용 하는 비동기 페이지 이벤트

권장 사항: Web Forms에서는 페이지 수명 주기 이벤트에 대해 비동기 void 메서드를 작성 하지 말고 비동기 코드에 [RegisterAsyncTask](https://msdn.microsoft.com/library/system.web.ui.page.registerasynctask.aspx) 를 사용 합니다.

**비동기 및** **void**로 페이지 이벤트를 표시 하면 비동기 코드가 완료 된 시간을 확인할 수 없습니다. 대신 RegisterAsyncTask를 사용 하 여 비동기 코드를 실행 하 여 완료를 추적할 수 있습니다.

다음 예제에서는 비동기 코드를 포함 하는 단추 클릭 처리기를 보여 줍니다. 이 예제에는 비동기 작업의 간단한 예제로만 제공 되 고 권장 되는 방법이 아닌 문자열 값을 비동기적으로 읽는 작업이 포함 됩니다.

[!code-csharp[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample11.cs)]

비동기 작업을 사용 하는 경우 Web.config 파일에서 Http 런타임 대상 프레임 워크를 4.5 이상으로 설정 합니다. 대상 프레임 워크를 4.5로 설정 하면 .NET 4.5에 추가 된 새 동기화 컨텍스트가 설정 됩니다. 이 값은 Visual Studio의 새 프로젝트에서 기본적으로 설정 되지만 기존 프로젝트로 작업 하는 경우에는 설정 되지 않습니다.

[!code-xml[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample12.xml)]

<a id="fire"></a>

### <a name="fire-and-forget-work"></a>시작 및 잊어버린 작업

권장 사항: ASP.NET 내에서 요청을 처리 하는 경우 시작 및 제거 작업을 시작 하지 않습니다 (예: QueueUserWorkItem 메서드 호출 또는 대리자를 반복적으로 호출 하는 타이머 만들기).

응용 프로그램에서 ASP.NET 내에 실행 되는 화재 및 잊은 작업을 수행 하는 경우 응용 프로그램이 동기화 되지 않을 수 있습니다. 언제 든 지 앱 도메인을 제거할 수 있으며,이는 진행 중인 프로세스가 응용 프로그램의 현재 상태와 더 이상 일치 하지 않을 수 있음을 의미 합니다.

이러한 유형의 작업은 ASP.NET 외부에서 이동 해야 합니다. Azure에서 웹 작업, Windows 서비스 또는 작업자 역할을 사용 하 여 진행 중인 작업을 수행 하 고 다른 프로세스에서 해당 코드를 실행할 수 있습니다.

ASP.NET 내에서이 작업을 수행 해야 하는 경우 [WebBackgrounder](http://www.nuget.org/packages/webbackgrounder) 라는 Nuget 패키지를 추가 하 여 코드를 실행할 수 있습니다.

<a id="requestentity"></a>

### <a name="request-entity-body"></a>요청 엔터티 본문

권장 사항: 처리기의 실행 이벤트 전에 InputStream 또는 요청을 읽지 마십시오.

InputStream에서 읽어야 하는 가장 빠른는 처리기의 실행 이벤트 중입니다. MVC에서 컨트롤러는 처리기 이며 작업 메서드가 실행 될 때 실행 이벤트입니다. Web Forms에서 페이지는 처리기이 고 execute 이벤트는 페이지. Init 이벤트가 발생 하는 경우입니다. 실행 이벤트 보다 이전 요청 엔터티 본문을 읽는 경우 요청 처리에 방해가 됩니다.

실행 이벤트 전에 요청 엔터티 본문을 읽어야 하는 경우 [GetBufferlessInputStream](https://msdn.microsoft.com/library/ff406798.aspx) 또는 [GetBufferedInputStream](https://msdn.microsoft.com/library/system.web.httprequest.getbufferedinputstream.aspx)중 하나를 사용 합니다. GetBufferlessInputStream를 사용 하는 경우 요청에서 원시 스트림을 가져오고 전체 요청을 처리 하는 책임이 있다고 가정 합니다. GetBufferlessInputStream를 호출한 후 InputStream 및 ASP.NET를 사용 하 여 채워지지 않았기 때문에를 사용할 수 없습니다. GetBufferedInputStream를 사용 하는 경우 요청에서 스트림의 복사본을 가져옵니다. ASP.NET는 다른 복사본을 채우기 때문에 InputStream 및 요청에서 나중에 계속 사용할 수 있습니다.

<a id="redirect"></a>

### <a name="responseredirect-and-responseend"></a>응답. 리디렉션 및 응답. 끝

권장 사항: [Response (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx)를 호출한 후 스레드를 처리 하는 방법의 차이를 알고 있어야 합니다.

[Response. Redirect (String)](https://msdn.microsoft.com/library/t9dwyts4.aspx) 메서드는 response 메서드를 호출 합니다. 동기 프로세스에서 Request. Redirect를 호출 하면 현재 스레드가 즉시 중단 됩니다. 그러나 비동기 프로세스에서 Response를 호출 하면 현재 스레드가 중단 되지 않으므로 코드 실행이 요청에 대해 계속 실행 됩니다. 비동기 프로세스에서 코드 실행을 중지 하려면 메서드에서 작업을 반환 해야 합니다.

MVC 프로젝트에서는 Response를 호출 하면 안 됩니다. 대신 RedirectResult를 반환 합니다.

<a id="viewstatemode"></a>

### <a name="enableviewstate-and-viewstatemode"></a>EnableViewState 및 ViewStateMode

권장 사항: view 상태를 사용 하는 컨트롤에 대해 세부적인 제어를 제공 하려면 EnableViewState 대신 ViewStateMode를 사용 합니다.

Page 지시문에서 EnableViewState를 false로 설정 하면 페이지 내의 모든 컨트롤에 대해 뷰 상태가 사용 하지 않도록 설정 되 고 사용 하도록 설정할 수 없습니다. 페이지의 특정 컨트롤에만 뷰 상태를 사용 하려면 페이지에 대해 ViewStateMode를 사용 안 함으로 설정 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample13.aspx)]

그런 다음 뷰 상태를 실제로 필요로 하는 컨트롤에 대해서만 ViewStateMode를 사용으로 설정 합니다.

[!code-aspx[Main](what-not-to-do-in-aspnet-and-what-to-do-instead/samples/sample14.aspx)]

필요한 컨트롤에 대해서만 뷰 상태를 사용 하도록 설정 하면 웹 페이지의 뷰 상태 크기를 축소할 수 있습니다.

<a id="sqlprovider"></a>

### <a name="sqlmembershipprovider"></a>SqlMembershipProvider

권장 사항: Universal Providers을 사용 합니다.

현재 프로젝트 템플릿에서 SqlMembershipProvider는 NuGet 패키지로 사용할 수 있는 [ASP.NET Universal Providers](http://www.nuget.org/packages/Microsoft.AspNet.Providers)으로 대체 되었습니다. 이전 버전의 템플릿으로 빌드된 프로젝트에서 SqlMembershipProvider를 사용 하는 경우 Universal Providers로 전환 해야 합니다. Universal Providers은 Entity Framework에서 지원 되는 모든 데이터베이스에서 작동 합니다.

자세한 내용은 [ASP.NET Universal Providers 소개](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)를 참조 하세요.

<a id="long"></a>

### <a name="long-running-requests-110-seconds"></a>장기 실행 요청 (> 110 초)

권장 사항: 연결 된 클라이언트에 대해 [websocket](https://msdn.microsoft.com/library/system.net.websockets.websocket.aspx) 또는 [SignalR](../../../signalr/index.md) 를 사용 하 고 비동기 i/o 작업을 사용 합니다.

장기 실행 요청을 실행 하면 웹 응용 프로그램에서 예기치 않은 결과가 발생 하 고 성능이 저하 될 수 있습니다. 요청에 대 한 기본 시간 제한 설정은 110 초입니다. 장기 실행 요청에서 세션 상태를 사용 하는 경우 ASP.NET는 110 초 후 세션 개체에 대 한 잠금을 해제 합니다. 그러나 잠금이 해제 되 고 작업이 성공적으로 완료 되지 않을 수 있는 경우 응용 프로그램은 세션 개체에 대 한 작업 중간에 있을 수 있습니다. 첫 번째 요청이 실행 되는 동안 사용자의 두 번째 요청이 차단 된 경우 두 번째 요청은 일관 되지 않은 상태에서 세션 개체에 액세스할 수 있습니다.

응용 프로그램에 차단 (또는 동기) i/o 작업이 포함 된 경우 응용 프로그램이 응답 하지 않습니다.

성능을 향상 시키려면 .NET Framework에서 비동기 i/o 작업을 사용 합니다. 또한 클라이언트를 서버에 연결 하는 데 Websocket 또는 SignalR를 사용 합니다. 이러한 기능은 장기 실행 요청을 효율적으로 처리할 수 있도록 설계 되었습니다.
