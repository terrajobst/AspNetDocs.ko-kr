---
uid: web-api/overview/security/enabling-cross-origin-requests-in-web-api
title: ASP.NET Web API 2에서 크로스-원본 요청을 사용 하도록 설정 Microsoft Docs
author: MikeWasson
description: ASP.NET Web API에서 CORS (원본 간 리소스 공유)를 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/29/2019
ms.assetid: 9b265a5a-6a70-4a82-adce-2d7c56ae8bdd
msc.legacyurl: /web-api/overview/security/enabling-cross-origin-requests-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: 9d3016d98fa6c3a55359c6dab0737407b29925f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447617"
---
# <a name="enable-cross-origin-requests-in-aspnet-web-api-2"></a>ASP.NET Web API 2에서 크로스-원본 요청을 사용 하도록 설정

[Mike Wasson](https://github.com/MikeWasson)

> 브라우저 보안은 웹 페이지에서 다른 도메인으로 AJAX 요청을 수행하지 못하도록 방지합니다. 이러한 제한을 *동일한 원본 정책*이라고 하며 악의적인 사이트에서 다른 사이트의 중요 한 데이터를 읽지 못하도록 방지 합니다. 그러나 경우에 따라 다른 사이트에서 web API를 호출 하도록 할 수도 있습니다.
>
> CORS ( [원본 간 리소스 공유](http://www.w3.org/TR/cors/) )는 서버에서 동일한 원본 정책을 완화할 수 있게 해 주는 W3C 표준입니다. CORS를 사용하면 서버에서 명시적으로 일부 원본 간 요청을 허용하는 한편 다른 요청은 거부할 수 있습니다. CORS는 [JSONP](http://en.wikipedia.org/wiki/JSONP)와 같은 이전 기술 보다 더 안전 하 고 유연 합니다. 이 자습서에서는 Web API 응용 프로그램에서 CORS를 사용 하도록 설정 하는 방법을 보여 줍니다.
>
> ## <a name="software-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어
>
> - [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - 웹 API 2.2

## <a name="introduction"></a>소개

이 자습서에서는 ASP.NET Web API의 CORS 지원에 대해 설명 합니다. 웹 API 컨트롤러를 호스트 하는 두 개의 ASP.NET 프로젝트와 WebService를 호출 하는 "WebClient" 라는 두 개의 프로젝트를 만들어 시작 합니다. 두 응용 프로그램이 서로 다른 도메인에서 호스트 되기 때문에 WebClient에서 WebService로의 AJAX 요청은 크로스-원본 요청입니다.

![](enabling-cross-origin-requests-in-web-api/_static/image1.png)

### <a name="what-is-same-origin"></a>"동일 원본"이란?

두 URL의 스키마, 호스트 및 포트가 모두 동일한 경우, 두 URL의 원본이 동일하다고 말합니다. ([RFC 6454](http://tools.ietf.org/html/rfc6454))

다음 두 URL은 동일한 원본입니다.

- `http://example.com/foo.html`
- `http://example.com/bar.html`

반면, 다음 URL들은 위의 두 URL과는 다른 원본입니다.

- `http://example.net`-다른 도메인
- `http://example.com:9000/foo.html`-다른 포트
- `https://example.com/foo.html`-다른 체계
- `http://www.example.com/foo.html`-다른 하위 도메인

> [!NOTE]
> Internet Explorer는 원본을 비교할 때 포트를 고려 하지 않습니다.

## <a name="create-the-webservice-project"></a>웹 서비스 프로젝트 만들기

> [!NOTE]
> 이 섹션에서는 Web API 프로젝트를 만드는 방법을 이미 알고 있다고 가정 합니다. 그렇지 않은 경우 [ASP.NET Web API 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)을 참조 하세요.

1. Visual Studio를 시작 하 고 새 **.NET Framework (ASP.NET Web Application)** 프로젝트를 만듭니다.
2. **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **빈** 프로젝트 템플릿을 선택 합니다. **에 대 한 폴더 및 핵심 참조 추가**에서 **Web API** 확인란을 선택 합니다.

   ![Visual Studio의 새 ASP.NET 프로젝트 대화 상자](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog.png)

3. 다음 코드를 사용 하 여 `TestController` 이라는 웹 API 컨트롤러를 추가 합니다.

   [!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample1.cs)]

4. 응용 프로그램을 로컬로 실행 하거나 Azure에 배포할 수 있습니다. (이 자습서의 스크린샷에서 앱은 Azure App Service Web Apps에 배포 됩니다.) Web API가 작동 하는지 확인 하려면 `http://hostname/api/test/`으로 이동 합니다. 여기서 *hostname* 은 응용 프로그램을 배포한 도메인입니다. 응답 텍스트 &quot;GET: 테스트 메시지&quot;표시 되어야 합니다.

   ![테스트 메시지를 표시 하는 웹 브라우저](enabling-cross-origin-requests-in-web-api/_static/image4.png)

## <a name="create-the-webclient-project"></a>WebClient 프로젝트 만들기

1. 다른 **.NET Framework (ASP.NET Web Application)** 프로젝트를 만들고 **MVC** 프로젝트 템플릿을 선택 합니다. 필요에 따라 **인증 > ** **인증 안 함**을 선택 합니다. 이 자습서에 대 한 인증이 필요 하지 않습니다.

   ![Visual Studio의 새 ASP.NET 프로젝트 대화 상자에서 MVC 템플릿](enabling-cross-origin-requests-in-web-api/_static/new-web-app-dialog-mvc.png)

2. **솔루션 탐색기**에서 파일 *Views/Home/Index. cshtml*를 엽니다. 이 파일의 코드를 다음으로 바꿉니다.

   [!code-cshtml[Main](enabling-cross-origin-requests-in-web-api/samples/sample2.cshtml?highlight=13)]

   *Serviceurl* 변수에서 WebService 앱의 URI를 사용 합니다.

3. 로컬에서 WebClient 앱을 실행 하거나 다른 웹 사이트에 게시 합니다.

"사용해 보세요." 단추를 클릭 하면 드롭다운 상자 (GET, POST 또는 PUT)에 나열 된 HTTP 메서드를 사용 하 여 AJAX 요청이 WebService 앱에 전송 됩니다. 이렇게 하면 서로 다른 크로스-원본 요청을 검사할 수 있습니다. 현재 WebService 앱은 CORS를 지원 하지 않으므로 단추를 클릭 하면 오류가 발생 합니다.

![브라우저에서 ' 사용해 보세요 ' 오류](enabling-cross-origin-requests-in-web-api/_static/image7.png)

> [!NOTE]
> [Fiddler](https://www.telerik.com/fiddler)와 같은 도구에서 HTTP 트래픽을 볼 경우 브라우저가 GET 요청을 보내고 요청이 성공 하지만 AJAX 호출에서 오류를 반환 하는 것을 볼 수 있습니다. 동일한 원본 정책이 브라우저에서 요청을 *보내지* 못하도록 하는 것을 이해 하는 것이 중요 합니다. 대신 응용 프로그램에서 *응답*을 볼 수 없습니다.

![웹 요청을 표시 하는 Fiddler 웹 디버거](enabling-cross-origin-requests-in-web-api/_static/image8.png)

## <a name="enable-cors"></a>CORS를 사용하도록 설정

이제 WebService 앱에서 CORS를 사용 하도록 설정 하겠습니다. 먼저 CORS NuGet 패키지를 추가 합니다. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](enabling-cross-origin-requests-in-web-api/samples/sample3.ps1)]

이 명령은 최신 패키지를 설치 하 고 핵심 웹 API 라이브러리를 비롯 한 모든 종속성을 업데이트 합니다. `-Version` 플래그를 사용 하 여 특정 버전을 대상으로 지정 합니다. CORS 패키지에는 Web API 2.0 이상이 필요 합니다.

File *App\_Start/WebApiConfig .cs*를 엽니다. **Webapiconfig. Register** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample4.cs?highlight=9)]

그런 다음 `TestController` 클래스에 **[EnableCors]** 특성을 추가 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample5.cs?highlight=3,7)]

*원본* 매개 변수의 경우 WebClient 응용 프로그램을 배포한 URI를 사용 합니다. 이렇게 하면 다른 모든 도메인 간 요청을 허용 하지 않고, WebClient의 크로스-원본 요청을 허용 합니다. 나중에 **[EnableCors]** 에 대 한 매개 변수를 자세히 설명 하겠습니다.

*원본* URL의 끝에 슬래시를 포함 하지 마십시오.

업데이트 된 웹 서비스 응용 프로그램을 다시 배포 합니다. WebClient를 업데이트할 필요가 없습니다. 이제 WebClient의 AJAX 요청이 성공 해야 합니다. GET, PUT 및 POST 메서드를 모두 사용할 수 있습니다.

![성공적인 테스트 메시지를 표시 하는 웹 브라우저](enabling-cross-origin-requests-in-web-api/_static/image9.png)

## <a name="how-cors-works"></a>CORS 작동 방법

이 섹션에서는 HTTP 메시지 수준에서 CORS 요청에 발생 하는 작업에 대해 설명 합니다. **[EnableCors]** 특성을 올바르게 구성 하 고 원하는 대로 작동 하지 않는 경우 문제를 해결할 수 있도록 CORS가 작동 하는 방식을 이해 하는 것이 중요 합니다.

CORS 명세에서는 교차 원본 요청을 활성화시키기 위한 용도로 몇 가지 새로운 HTTP 헤더들이 도입되었습니다. 브라우저에서 CORS를 지 원하는 경우 원본 간 요청에 대해 이러한 헤더를 자동으로 설정 합니다. JavaScript 코드에서 특별 한 작업을 수행할 필요가 없습니다.

원본 간 요청의 예는 다음과 같습니다. "원본" 헤더는 요청을 수행 하는 사이트의 도메인을 제공 합니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample6.cmd?highlight=5)]

서버에서 요청을 허용 하는 경우 액세스 제어 허용 원본 헤더를 설정 합니다. 이 헤더의 값이 원본 헤더와 일치 하거나 와일드 카드 값 "\*" 이며,이는 모든 원본이 허용 됨을 의미 합니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample7.cmd?highlight=5)]

응답에 액세스 제어 허용-원본 헤더가 포함 되어 있지 않으면 AJAX 요청이 실패 합니다. 특히 브라우저에서 요청을 허용 하지 않습니다. 서버에서 응답을 반환 하는 경우에도 브라우저는 클라이언트 응용 프로그램에서 응답을 사용할 수 있도록 설정 하지 않습니다.

**실행 전 요청**

일부 CORS 요청에 대해서는 브라우저에서 리소스에 대 한 실제 요청을 보내기 전에 "실행 전 요청" 이라는 추가 요청을 보냅니다.

다음 조건에 해당 하는 경우 브라우저에서 실행 전 요청을 건너뛸 수 있습니다.

- 요청 메서드는 *GET, HEAD* 또는 POST입니다.
- 응용 프로그램은 허용, 허용 언어, 콘텐츠 언어, 콘텐츠 형식 또는 마지막 이벤트 ID 이외의 요청 *헤더를 설정* 하지 않습니다.
- Content-type 헤더 (설정 된 경우)는 다음 중 하나입니다.

    - application/x-www-form-urlencoded
    - 다중 파트/폼 데이터
    - 텍스트/일반

요청 헤더에 대 한 규칙은 응용 프로그램이 **XMLHttpRequest** 개체에 대해 **setRequestHeader** 를 호출 하 여 설정 하는 헤더에 적용 됩니다. CORS 사양은 이러한 "author 요청 헤더"를 호출 합니다. 이 규칙은 *브라우저* 에서 설정할 수 있는 헤더 (예: 사용자 에이전트, 호스트 또는 콘텐츠 길이)에는 적용 되지 않습니다.

다음은 실행 전 요청의 예입니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample8.cmd?highlight=4-5)]

사전 비행 요청은 HTTP OPTIONS 메서드를 사용 합니다. 여기에는 두 가지 특수 헤더가 포함 됩니다.

- 액세스 제어-요청 메서드: 실제 요청에 사용 되는 HTTP 메서드입니다.
- 액세스 제어-요청 헤더: *응용 프로그램이* 실제 요청에 대해 설정한 요청 헤더의 목록입니다. 이 경우 브라우저에서 설정 하는 헤더는 포함 되지 않습니다.

서버에서 요청을 허용 한다고 가정 하는 예제 응답은 다음과 같습니다.

[!code-console[Main](enabling-cross-origin-requests-in-web-api/samples/sample9.cmd?highlight=6-7)]

응답에는 허용 되는 메서드를 나열 하는 액세스 제어-허용 메서드 헤더와 허용 되는 헤더를 나열 하는 액세스 제어-헤더 헤더가 포함 됩니다. 실행 전 요청이 성공 하는 경우 브라우저는 앞에서 설명한 대로 실제 요청을 보냅니다.

실행 전 옵션 요청 (예: [Fiddler](https://www.telerik.com/fiddler) 및 [postman](https://www.getpostman.com/))을 사용 하 여 끝점을 테스트 하는 데 일반적으로 사용 되는 도구는 기본적으로 필수 옵션 헤더를 보내지 않습니다. `Access-Control-Request-Method` 및 `Access-Control-Request-Headers` 헤더가 요청과 함께 전송 되 고 옵션 헤더가 IIS를 통해 앱에 도달 하는지 확인 합니다.

ASP.NET 앱이 옵션 요청을 수신 하 고 처리할 수 있도록 IIS를 구성 하려면 `<system.webServer><handlers>` 섹션에서 앱의 *web.config* 파일에 다음 구성을 추가 합니다.

```xml
<system.webServer>
  <handlers>
    <remove name="ExtensionlessUrlHandler-Integrated-4.0" />
    <remove name="OPTIONSVerbHandler" />
    <add name="ExtensionlessUrlHandler-Integrated-4.0" path="*." verb="*" type="System.Web.Handlers.TransferRequestHandler" preCondition="integratedMode,runtimeVersionv4.0" />
  </handlers>
</system.webServer>
```

`OPTIONSVerbHandler`를 제거 하면 IIS에서 옵션 요청을 처리할 수 없습니다. 기본 모듈 등록에서는 확장명 없는 Url을 사용 하 여 GET, HEAD, POST 및 DEBUG 요청만 허용 하기 때문에 `ExtensionlessUrlHandler-Integrated-4.0`를 대체 하 여 옵션 요청이 앱에 도달 하도록 허용 합니다.

## <a name="scope-rules-for-enablecors"></a>[EnableCors]에 대 한 범위 규칙

응용 프로그램의 모든 웹 API 컨트롤러에 대해 작업당 CORS를 사용 하도록 설정 하거나, 컨트롤러 당 작업을 수행할 수 있습니다.

**작업 당**

단일 작업에 대해 CORS를 사용 하도록 설정 하려면 동작 메서드에서 **[EnableCors]** 특성을 설정 합니다. 다음 예제에서는 `GetItem` 메서드에 대해서만 CORS를 사용 하도록 설정 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample10.cs)]

**컨트롤러 당**

컨트롤러 클래스에서 **[EnableCors]** 를 설정 하면 컨트롤러의 모든 작업에 적용 됩니다. 작업에 대해 CORS를 사용 하지 않도록 설정 하려면 **[DisableCors]** 특성을 작업에 추가 합니다. 다음 예에서는 `PutItem`를 제외 하 고 모든 메서드에 대해 CORS를 사용 하도록 설정 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample11.cs)]

**전역적으로**

응용 프로그램의 모든 Web API 컨트롤러에 대해 CORS를 사용 하도록 설정 하려면 **EnableCorsAttribute** 인스턴스를 **EnableCors** 메서드에 전달 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample12.cs)]

특성을 두 개 이상의 범위에서 설정 하는 경우 우선 순위는 다음과 같습니다.

1. 작업
2. 컨트롤러
3. Global

## <a name="set-the-allowed-origins"></a>허용되는 원본 설정하기

**[EnableCors]** 특성의 *원본* 매개 변수는 리소스에 액세스할 수 있는 원본을 지정 합니다. 값은 허용 된 원본에 대 한 쉼표로 구분 된 목록입니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample13.cs)]

와일드 카드 값 "\*"을 사용 하 여 모든 원본에서 요청을 허용할 수도 있습니다.

모든 원본의 요청을 허용하기 전에 신중히 고민하시기 바랍니다. 즉, 웹 사이트를 그대로 사용 하 여 웹 API에 대 한 AJAX 호출을 수행할 수 있습니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample14.cs)]

## <a name="set-the-allowed-http-methods"></a>허용되는 HTTP 메서드 설정하기

**[EnableCors]** 특성의 *메서드* 매개 변수는 리소스에 액세스할 수 있는 HTTP 메서드를 지정 합니다. 모든 메서드를 허용 하려면 "\*" 와일드 카드 값을 사용 합니다. 다음 예제에서는 GET 및 POST 요청만 허용 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample15.cs)]

## <a name="set-the-allowed-request-headers"></a>허용되는 요청 헤더 설정하기

이 문서에서는 이전에 실행 전 요청에 액세스 제어 요청 헤더 헤더를 포함 하 여 응용 프로그램에 의해 설정 된 HTTP 헤더를 나열 하는 방법에 대해 설명 했습니다 ("작성자 요청 헤더"). **[EnableCors]** 특성의 *headers* 매개 변수는 허용 되는 저자 요청 헤더를 지정 합니다. 모든 헤더를 허용 하려면 *헤더* 를 "\*"로 설정 합니다. 특정 헤더를 허용 목록 하려면 *헤더* 를 허용 된 헤더의 쉼표로 구분 된 목록으로 설정 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample16.cs)]

그러나 브라우저는 액세스 제어 요청 헤더를 설정 하는 방법과 완전히 일치 하지 않습니다. 예를 들어 Chrome에는 현재 "원본"이 포함 됩니다. FireFox에는 응용 프로그램에서 스크립트를 설정 하는 경우에도 "Accept"와 같은 표준 헤더가 포함 되지 않습니다.

*헤더* 를 "\*" 이외의 값으로 설정 하는 경우 "accept", "content-type" 및 "원본"을 포함 하 고 지원 하려는 사용자 지정 헤더를 포함 해야 합니다.

## <a name="set-the-allowed-response-headers"></a>허용 되는 응답 헤더 설정

기본적으로 브라우저는 응용 프로그램에 대 한 모든 응답 헤더를 노출 하지 않습니다. 기본적으로 사용 가능한 응답 헤더들은 다음과 같습니다.

- Cache-Control
- Content-Language
- 콘텐츠 형식
- 만료
- Last-Modified
- Pragma

CORS spec은 이러한 [간단한 응답 헤더](https://dvcs.w3.org/hg/cors/raw-file/tip/Overview.html#simple-response-header)를 호출 합니다. 응용 프로그램에서 다른 헤더를 사용할 수 있도록 하려면 **[EnableCors]** 의 *exposedHeaders* 매개 변수를 설정 합니다.

다음 예제에서 컨트롤러의 `Get` 메서드는 ' X-사용자 지정 헤더 ' 라는 사용자 지정 헤더를 설정 합니다. 기본적으로 브라우저는 크로스-원본 요청에서이 헤더를 노출 하지 않습니다. 헤더를 사용할 수 있도록 설정 하려면 *exposedHeaders*에 ' X X X-u r l '을 포함 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample17.cs)]

## <a name="pass-credentials-in-cross-origin-requests"></a>크로스-원본 요청에서 자격 증명 전달

CORS 요청에서 자격 증명(Credentials)은 특별한 처리를 해야 합니다. 기본적으로 브라우저는 원본 간 요청과 함께 자격 증명을 보내지 않습니다. 여기에서 말하는 자격 증명에는 쿠키뿐만 아니라 HTTP 인증 스킴도 포함됩니다. 크로스-원본 요청을 사용 하 여 자격 증명을 보내려면 클라이언트에서 **XMLHttpRequest** 를 설정 해야 합니다.

**XMLHttpRequest** 직접 사용:

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample18.cs)]

jQuery를 사용할 경우:

[!code-javascript[Main](enabling-cross-origin-requests-in-web-api/samples/sample19.js)]

또한 서버에서도 자격 증명을 허용해야만 합니다. Web API에서 원본 간 자격 증명을 허용 하려면 **[EnableCors]** 특성에서 **SupportsCredentials** 속성을 true로 설정 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample20.cs)]

이 속성이 true 이면 HTTP 응답에 액세스 제어-허용-자격 증명 헤더가 포함 됩니다. 이 헤더는 서버에서 원본 간 요청에 대 한 자격 증명을 허용 하도록 브라우저에 지시 합니다.

브라우저에서 자격 증명을 전송 하지만 응답에 유효한 액세스 제어-허용-자격 증명 헤더가 포함 되어 있지 않은 경우 브라우저는 응용 프로그램에 응답을 노출 하지 않으며 AJAX 요청이 실패 합니다.

**SupportsCredentials** 를 true로 설정 하는 경우에는 다른 도메인의 웹 사이트에서 사용자를 대신 하 여 사용자를 대신 하 여 사용자의 웹 API에 로그인 한 사용자의 자격 증명을 보낼 수 있다는 것을 의미 합니다. CORS 사양은 **SupportsCredentials** 가 true 인 경우 \*&quot;에 대 &quot;한 *원본* 설정이 잘못 되었음을 알려 주는 것입니다.

## <a name="custom-cors-policy-providers"></a>사용자 지정 CORS 정책 공급자

**[EnableCors]** 특성은 **ICorsPolicyProvider** 인터페이스를 구현 합니다. **특성** 에서 파생 되는 클래스를 만들고 **ICorsPolicyProvider**을 구현 하 여 사용자 고유의 구현을 제공할 수 있습니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample21.cs)]

이제 입력 하는 모든 위치 **[EnableCors]** 에 특성을 적용할 수 있습니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample22.cs)]

예를 들어 사용자 지정 CORS 정책 공급자가 구성 파일에서 설정을 읽을 수 있습니다.

특성을 사용 하는 대신 **ICorsPolicyProvider** 개체를 만드는 **ICorsPolicyProviderFactory** 개체를 등록할 수 있습니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample23.cs)]

**ICorsPolicyProviderFactory**를 설정 하려면 시작 시 다음과 같이 **SetCorsPolicyProviderFactory** 확장 메서드를 호출 합니다.

[!code-csharp[Main](enabling-cross-origin-requests-in-web-api/samples/sample24.cs)]

## <a name="browser-support"></a>브라우저 지원

Web API CORS 패키지는 서버 쪽 기술입니다. 사용자의 브라우저 에서도 CORS를 지원 해야 합니다. 다행히 모든 주요 브라우저의 현재 버전에는 [CORS에 대 한 지원이](http://caniuse.com/cors)포함 됩니다.
