---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 웹 페이지 (Razor) 문제 해결 가이드 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지)를 사용 하 여 작업할 때 발생할 수 있는 문제 및 제안 된 몇 가지 솔루션을 설명 합니다. Software 버전 ASP.NET Web Pag ...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473381"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET 웹 페이지(Razor) 문제 해결 가이드

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지)를 사용 하 여 작업할 때 발생할 수 있는 문제 및 제안 된 몇 가지 솔루션을 설명 합니다.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 및 ASP.NET 웹 페이지 1.0 에서도 작동 합니다.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [페이지 실행 문제](#Issues_Running_.cshtml_Pages)
- [Razor 코드 문제](#IssuesWithRazorCode)
- [보안 및 멤버 자격과 관련 된 문제](#membership)
- [전자 메일 보내기 문제](#email)
- [추가 리소스](#AdditionalResources)

일반적인 질문은 [ASP.NET 웹 페이지 (Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)를 참조 하세요.

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>페이지 실행 문제

여러 가지 문제로 인해 *. cshtml* 및 *.* t o l s 페이지가 제대로 실행 되지 않을 수 있습니다. 이 섹션에는 일반적인 오류 메시지 및 가능한 원인이 나와 있습니다.

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP 오류 403-사용 권한 없음: 액세스가 거부 되었습니다.

*제공한 자격 증명을 사용 하 여이 디렉터리 또는 페이지를 볼 수 있는 권한이 없습니다.*

이 오류는 서버에서 올바른 버전의 .NET Framework를 실행 하지 않는 경우에 발생할 수 있습니다. 서버를 실행 하는 컴퓨터 (로컬 또는 원격)에 적어도 .NET Framework 4가 설치 되어 있는지 확인 합니다. 또한 응용 프로그램 자체가 올바른 버전을 실행 하도록 구성 되었는지 확인 합니다.

WebMatrix에서 작업 하는 동안이 문제가 로컬로 표시 되 면 **사이트** 작업 영역을 클릭 한 다음 Treeview에서 **설정**을 클릭 합니다. **.NET Framework 버전 선택** 목록에서 **.Net 4 (통합)** 를 선택 합니다. 이 버전이 이미 설정 되어 있는 경우 관리자 권한으로 WebMatrix를 실행 해 보세요.

웹 사이트의 루트에 하나 이상의 *cshtml* 파일이 있는지 확인 합니다.

웹 서버가 원격 서버에 있는 경우이 오류가 표시 되 면 서버 관리자에 게 문의 하십시오. 서버에 .NET Framework 4 이상이 설치 되어 있는지 확인 합니다. 또한 해당 버전의 the.NET Framework를 사용 하도록 구성 된 응용 프로그램 풀에서 응용 프로그램이 실행 되 고 있는지 확인 합니다.

서버에 대 한 제어 권한이 있는 경우 올바른 버전의 .NET Framework를 실행 하 고 있는지 확인 합니다. `aspnet_regiis -iru` 명령을 실행 하 여 설치를 복구 해 볼 수도 있습니다. 예를 들어 .NET Framework를 설치한 후 IIS를 설치 하는 경우 IIS는 ASP.NET 페이지를 실행 하도록 올바르게 구성 되지 않습니다. 자세한 내용은 [ASP.NET Iis 등록 도구 (Aspnet\_regiis .exe)](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)를 참조 하세요.

### <a name="http-error-40314---forbidden"></a>HTTP 오류 403.14-사용할 수 없음

*웹 서버가이 디렉터리의 내용을 나열 하지 않도록 구성 되어 있습니다.*

이 오류는 보호 되는 리소스 (예: *web.config* 파일) 또는 보호 되는 폴더 (예: *앱\_데이터* 또는 *앱\_코드*)에 있는 리소스를 요청 하는 경우 발생할 수 있습니다.

### <a name="http-error-40417---not-found"></a>HTTP 오류 404.17-찾을 수 없음

*요청 된 콘텐츠는 스크립트로 표시 되며 정적 파일 처리기에서 제공 되지 않습니다.*

이 오류는 .NET Framework 4 이상을 사용 하도록 서버가 올바르게 구성 되어 있지 않아 `@{ }` 블록의 코드를 인식 하지 못하는 경우에 발생할 수 있습니다. 앞의 *HTTP 오류 403-사용 권한 없음: 액세스가 거부*됨에 대 한 설명을 참조 하세요.

### <a name="http-error-4047---not-found"></a>HTTP 오류 404.7-찾을 수 없음

*파일 확장명을 거부 하도록 요청 필터링 모듈이 구성 되어 있습니다.*

이 오류는 서버가 서버에서 명시적으로 차단 *된 경우에* 발생할 수 있습니다. 이 문제는 Url이 확장을 포함 하지 않는 경우에도 작동 하지만 *.* a u 또는 *.* 가능한 해결 방법은 사이트의 *web.config* 파일에서 확장을 다시 사용 하도록 설정 하는 것입니다. 다음 예제에서는 *. cshtml* 확장명을 사용 하도록 설정 하는 방법을 보여 줍니다.

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP 오류 404.8-찾을 수 없음

*HiddenSegment 섹션을 포함 하는 URL의 경로를 거부 하도록 요청 필터링 모듈이 구성 되어 있습니다.*

이 오류는 보호 되는 리소스 (예: *web.config* 파일) 또는 보호 되는 폴더 (예: *앱\_데이터* 또는 *앱\_코드*)에 있는 리소스를 요청 하는 경우 발생할 수 있습니다.

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>이 유형의 페이지는 제공 되지 않습니다 ('/' 응용 프로그램의 서버 오류).

HTTP 오류 404.17에 대 한 앞부분의 설명을 참조 하세요.

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor 코드 문제

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>'*Class*' 이름이 현재 컨텍스트에 없습니다.

이 오류가 표시 되는 이유는 `class` 도우미를 참조 하지만 도우미가 설치 되어 있지 않기 때문입니다. 예를 들어 도우미를 사용 하려고 하지만 NuGet에서 패키지를 설치 하지 않은 경우이 오류가 표시 됩니다. WebMatrix의 갤러리를 사용 하 여 도우미를 찾아서 설치 합니다.

도우미가 설치 되어 있지만 페이지에서 인식 되지 않는 경우 코드에 `using` 문 추가를 추가 해 봅니다. `using` 문에서 도우미가 포함 된 네임 스페이스를 참조 합니다. 예를 들어, ASP.NET 웹 도우미 패키지에 있는 기본 도우미는 `System.Web.Helpers` 네임 스페이스에 있습니다. 도우미를 사용 하려는 페이지 맨 위에 다음 줄을 추가 합니다.

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>보안 및 멤버 자격과 관련 된 문제

ASP.NET 웹 페이지 (Razor)에서 기본 제공 보안 (멤버 자격) 시스템을 사용 하는 경우 다음과 같은 문제가 발생할 수 있습니다.

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>이 메서드를 호출 하려면 "Membership. Provider" 속성이 "ExtendedMembershipProvider"의 인스턴스여야 합니다.

이 오류는 `AspNetSqlMembershipProvider` 클래스가 구성 되지 않았음을 나타낼 수 있습니다. 증상은 사이트가 로컬에서 제대로 작동 하지만 호스팅 공급자의 서버에 게시할 때이 오류를 throw 한다는 것입니다. 이 문제에 대 한 한 가지 해결 방법은 사이트의 *web.config* 파일에 다음을 추가 하 여 명시적 멤버 자격을 명시적으로 사용 하도록 설정 하는 것입니다.

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>전자 메일 보내기 문제

전자 메일을 보낼 때 발생 하는 문제는 디버깅 하기 어려울 수 있습니다. 초기 문제는 SMTP 서버에 연결할 수 없다는 것입니다. 연결에 성공 하면 ASP.NET는 메시지를 SMTP 서버에 전달 합니다. 그러나 메시지 자체에는 SMTP 서버에서 메시지를 보내지 못하도록 하는 문제가 있을 수 있습니다.

응용 프로그램에서 전자 메일을 성공적으로 보내지 않는 경우 다음을 시도 합니다.

- SMTP 서버 이름은 `smtp.provider.com` 또는 `smtp.provider.net`와 같은 경우가 많습니다. 그러나 호스팅 공급자에 사이트를 게시 하는 경우 해당 지점에서 SMTP 서버 이름이 `localhost`될 수 있습니다. 이 문제는 게시 하 고 사이트를 공급자 서버에서 실행 한 후 SMTP 서버가 응용 프로그램의 관점에서 로컬 일 수 있기 때문에 발생 합니다. 서버 이름을 변경 하면 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 하는 것일 수 있습니다.
- 포트 번호는 일반적으로 25입니다. 그러나 일부 공급자는 포트 587 또는 다른 포트를 사용 해야 합니다. SMTP 서버의 소유자에 게 사용할 포트 번호를 확인 합니다.
- 올바른 자격 증명을 사용 하는지 확인 합니다. 호스팅 공급자에 사이트를 게시 한 경우 공급자가 특별히 표시 한 자격 증명을 전자 메일에 사용 합니다. 이러한 자격 증명은 게시 하는 데 사용 하는 자격 증명과 다를 수 있습니다.
- 자격 증명이 필요 하지 않은 경우도 있습니다. 개인 ISP를 사용 하 여 전자 메일을 전송 하는 경우 전자 메일 공급자가 이미 자격 증명을 알고 있을 수 있습니다. 게시 한 후 로컬 컴퓨터에서 테스트 하는 경우와 다른 자격 증명을 사용 해야 할 수 있습니다.
- 전자 메일 공급자가 암호화를 사용 하는 경우 `WebMail.EnableSsl`를 `true`로 설정 합니다.

전자 메일을 보내는 동안 오류가 발생 하는 경우 다음과 같은 표준 ASP.NET 오류 메시지가 표시 될 수 있습니다.

![전자 메일에 문제가 있는 경우 ASP.NET 오류 메시지](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

다음 예제와 같이 `try-catch` 블록을 사용 하 여 전자 메일 보내기와 관련 된 문제를 디버그할 수도 있습니다. `try-catch` 블록을 사용 하는 경우 ASP.NET는 표준 오류 메시지를 표시 하지 않습니다. 대신 블록의 `catch` 부분에서 오류를 캡처할 수 있습니다.

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

`your-SMTP-server-name`에 대 한 적절 한 값으로 대체 합니다. 이러한 방식으로 표시 될 수 있는 오류 메시지는 다음과 같습니다.

- *메일을 보내지 못했습니다.*

    또는

    *시간이 지난 후 연결 된 파티가 적절 하 게 응답 하지 않거나 연결 된 호스트가 응답 하지 않아 연결을 설정 하지 못하여 연결 하지 못했습니다.*

    이 오류는 일반적으로 응용 프로그램이 SMTP 서버에 연결할 수 없음을 의미 합니다. 서버 이름 및 포트 번호를 확인 합니다.
- *사서함을 사용할 수 없습니다. 서버 응답: 5.1.0 &lt;someuser@invaliddomain&gt; 발신자가 거부 됨: 발신자 도메인이 잘못 되었습니다.*

    이 메시지는 `From` 주소가 올바르지 않거나 누락 된 것을 나타낼 수 있습니다.
- *지정 된 문자열이 전자 메일 주소에 필요한 형식이 아닙니다.*

    이 오류는 `To` 또는 `From` 속성의 값이 전자 메일 주소로 인식 되지 않음을 나타낼 수 있습니다. ASP.NET 전자 메일 주소가 유효한 지, *name@domain.com* 와 같은 올바른 형식 인지 확인할 수 없습니다.

> [!NOTE]
> 라이브 사이트에 페이지를 게시 하기 전에 오류 (`@errorMessage`)를 표시 하는 태그를 제거 합니다. 사용자가 서버에서 가져오는 오류 메시지를 볼 수 있도록 하는 것은 좋지 않습니다.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지(Razor) FAQ](https://go.microsoft.com/fwlink/?LinkId=253000)

ASP.NET 웹 사이트의 [WebMatrix 및 ASP.NET 웹 페이지](https://forums.asp.net/1224.aspx/1?WebMatrix) 포럼
