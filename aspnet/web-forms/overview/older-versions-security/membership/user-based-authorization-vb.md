---
uid: web-forms/overview/older-versions-security/membership/user-based-authorization-vb
title: 사용자 기반 권한 부여 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 다양 한 기술을 통해 페이지에 대 한 액세스를 제한 하 고 페이지 수준 기능을 제한 하는 방법을 살펴보겠습니다.
ms.author: riande
ms.date: 01/18/2008
ms.assetid: bc937e9d-5c14-4fc4-aec7-440da924dd18
msc.legacyurl: /web-forms/overview/older-versions-security/membership/user-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: dfac0c6fa955e59c6ea996533f2447e89ec8d468
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588208"
---
# <a name="user-based-authorization-vb"></a>사용자 기반 권한 부여(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_07_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial07_UserAuth_vb.pdf)

> 이 자습서에서는 다양 한 기술을 통해 페이지에 대 한 액세스를 제한 하 고 페이지 수준 기능을 제한 하는 방법을 살펴보겠습니다.

## <a name="introduction"></a>소개

사용자 계정을 제공 하는 대부분의 웹 응용 프로그램은 특정 방문자가 사이트 내의 특정 페이지에 액세스 하지 못하도록 제한 하는 과정을 포함 합니다. 예를 들어 대부분의 온라인 messageboard 사이트에서 모든 사용자 (익명 및 인증 됨)는 messageboard의 게시물을 볼 수 있지만, 인증 된 사용자만 웹 페이지를 방문 하 여 새 게시물을 만들 수 있습니다. 그리고 특정 사용자 (또는 특정 사용자 집합)만 액세스할 수 있는 관리 페이지가 있을 수 있습니다. 또한 페이지 수준 기능은 사용자 마다 다를 수 있습니다. 게시물 목록을 볼 때 인증 된 사용자는 각 게시물의 등급을 매기는 인터페이스를 표시 하는 반면,이 인터페이스는 익명 방문자에 게 제공 되지 않습니다.

ASP.NET를 사용 하면 사용자 기반 권한 부여 규칙을 쉽게 정의할 수 있습니다. `Web.config`의 특정 웹 페이지 또는 전체 디렉터리는 지정 된 사용자의 하위 집합에만 액세스할 수 있도록 잠글 수 있습니다. 페이지 수준 기능을 사용 하거나 사용 하지 않도록 설정 하거나 사용 하지 않도록 설정할 수 있습니다.

이 자습서에서는 다양 한 기술을 통해 페이지에 대 한 액세스를 제한 하 고 페이지 수준 기능을 제한 하는 방법을 살펴보겠습니다. 시작 하겠습니다.

## <a name="a-look-at-the-url-authorization-workflow"></a>URL 권한 부여 워크플로 살펴보기

[*폼 인증 개요 개요*](../introduction/an-overview-of-forms-authentication-vb.md) 에서 설명한 것 처럼 ASP.NET 런타임이 ASP.NET 리소스에 대 한 요청을 처리 하면 해당 수명 주기 동안 요청이 여러 이벤트를 발생 시킵니다. *HTTP 모듈* 은 요청 수명 주기의 특정 이벤트에 대 한 응답으로 코드가 실행 되는 관리 되는 클래스입니다. ASP.NET는 백그라운드에서 필수 작업을 수행 하는 다양 한 HTTP 모듈과 함께 제공 됩니다.

이러한 HTTP 모듈 중 하나를 [`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)합니다. 이전 자습서에서 설명한 대로 `FormsAuthenticationModule`의 기본 기능은 현재 요청의 id를 확인 하는 것입니다. 쿠키에 있거나 URL에 포함 된 폼 인증 티켓을 검사 하 여이를 수행 합니다. 이 확인은 [`AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)중에 발생 합니다.

또 다른 중요 한 HTTP 모듈은 [`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx) [`AuthorizeRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx) 에 대 한 응답으로 발생 합니다 .이는 `AuthenticateRequest` 이벤트 후에 발생 합니다. `UrlAuthorizationModule`는 `Web.config`에서 구성 태그를 검사 하 여 현재 id에 지정 된 페이지를 방문할 권한이 있는지 여부를 확인 합니다. 이 프로세스를 *URL 권한 부여*라고 합니다.

1 단계에서 URL 권한 부여 규칙에 대 한 구문을 검토 하지만 먼저 요청에 대 한 권한이 있는지 여부에 따라 `UrlAuthorizationModule`에서 수행 하는 작업을 살펴보겠습니다. `UrlAuthorizationModule` 요청에 권한이 부여 된 것으로 확인 되 면 아무 작업도 수행 하지 않고 해당 수명 주기 동안 요청이 계속 됩니다. 그러나 요청에 권한이 부여 *되지 않은* 경우 `UrlAuthorizationModule`는 수명 주기를 중단 하 고 `Response` 개체에 [HTTP 401 권한 없음](http://www.checkupdown.com/status/E401.html) 상태를 반환 하도록 지시 합니다. 폼 인증을 사용 하는 경우이 http 401 상태는 클라이언트에 반환 되지 않습니다. `FormsAuthenticationModule`에서 HTTP 401 상태를 검색 302 하는 경우이를 로그인 페이지로 [리디렉션합니다](http://www.checkupdown.com/status/E302.html) .

그림 1에서는 ASP.NET 파이프라인, `FormsAuthenticationModule`및 권한이 없는 요청이 도착 했을 때의 `UrlAuthorizationModule` 워크플로를 보여 줍니다. 특히 그림 1은 익명 사용자에 대 한 액세스를 거부 하는 페이지인 `ProtectedPage.aspx`에 대 한 익명 방문자의 요청을 보여 줍니다. 방문자가 익명 이기 때문에 `UrlAuthorizationModule`은 요청을 중단 하 고 HTTP 401 권한 없음 상태를 반환 합니다. 그런 다음 `FormsAuthenticationModule`는 401 상태를 로그인 페이지로 302 리디렉션으로 변환 합니다. 로그인 페이지를 통해 사용자가 인증 되 면 `ProtectedPage.aspx`으로 리디렉션됩니다. 이번에는 `FormsAuthenticationModule` 인증 티켓에 따라 사용자를 식별 합니다. 이제 방문자가 인증 되었으므로 `UrlAuthorizationModule`는 페이지에 대 한 액세스를 허용 합니다.

[폼 인증 및 URL 권한 부여 워크플로를 ![합니다.](user-based-authorization-vb/_static/image2.png)](user-based-authorization-vb/_static/image1.png)

**그림 1**: 폼 인증 및 URL 권한 부여 워크플로 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image3.png))

그림 1에서는 익명 방문자가 익명 사용자가 사용할 수 없는 리소스에 액세스 하려고 할 때 발생 하는 상호 작용을 보여 줍니다. 이 경우 익명 방문자가 querystring에서 지정 된 방문 하려던 페이지가 있는 로그인 페이지로 리디렉션됩니다. 사용자가 성공적으로 로그온 하면 처음에 보려고 했던 리소스로 자동으로 다시 리디렉션됩니다.

익명 사용자가 무단으로 요청 하는 경우이 워크플로는 간단 하며 방문자가 발생 한 이유와 이유를 쉽게 파악할 수 있습니다. 그러나 `FormsAuthenticationModule`는 인증 된 사용자가 요청한 경우에도 인증 되지 않은 사용자를 로그인 *페이지로 리디렉션합니다.* 인증 된 사용자가 권한이 없는 페이지를 방문 하려고 하면이로 인해 사용자 환경이 혼란 스 러 울 수 있습니다.

ASP.NET 페이지 `OnlyTito.aspx`를 Tito로만 accessibly 하기 위해 웹 사이트에 URL 권한 부여 규칙이 구성 되어 있다고 가정 합니다. 이제 Sam이 사이트를 방문 하 여 로그온 한 후 `OnlyTito.aspx`방문 하려고 한다고 가정 합니다. `UrlAuthorizationModule`는 요청 수명 주기를 중지 하 고 HTTP 401 권한 없음 상태를 반환 합니다 .이 상태는 `FormsAuthenticationModule` 검색 한 후 Sam을 로그인 페이지로 리디렉션합니다. Sam은 이미 로그인 했으므로 로그인 페이지로 다시 전송 된 이유를 궁금할 수 있습니다. 그녀의 로그인 자격 증명이 손실 되었거나 잘못 된 자격 증명을 입력 했을 수 있습니다. Sam이 로그인 페이지에서 자격 증명을 후 하는 경우 (다시) 로그온 하 여 `OnlyTito.aspx`으로 리디렉션됩니다. `UrlAuthorizationModule`는 Sam이이 페이지를 방문할 수 없다는 것을 감지 하 여 로그인 페이지로 반환 됩니다.

그림 2에서는 이러한 혼란 스러운 워크플로를 보여 줍니다.

[기본 워크플로를 ![하면 혼동 될 수 있습니다.](user-based-authorization-vb/_static/image5.png)](user-based-authorization-vb/_static/image4.png)

**그림 2**: 기본 워크플로는 혼동 될 수 있습니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image6.png)).

그림 2에 설명 된 워크플로를 통해 대부분의 컴퓨터에 많은 방문자가 신속 하 게 befuddle 수 있습니다. 2 단계에서 이러한 혼란 스 사이클을 방지 하는 방법을 살펴보겠습니다.

> [!NOTE]
> ASP.NET는 두 가지 메커니즘을 사용 하 여 현재 사용자가 특정 웹 페이지에 액세스할 수 있는지 여부를 확인 합니다. URL 권한 부여 및 파일 권한 부여입니다. 파일 권한 부여는 요청 된 파일 Acl을 확인 하 여 권한을 결정 하는 [`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx)에 의해 구현 됩니다. Acl은 Windows 계정에 적용 되는 권한 이므로 파일 권한 부여는 Windows 인증에서 가장 일반적으로 사용 됩니다. 폼 인증을 사용 하는 경우 사이트를 방문 하는 사용자에 관계 없이 모든 운영 체제 및 파일 시스템 수준 요청은 동일한 Windows 계정에서 실행 됩니다. 이 자습서 시리즈는 폼 인증을 중심으로 하므로 파일 권한 부여에 대해서는 다루지 않습니다.

### <a name="the-scope-of-url-authorization"></a>URL 권한 부여 범위

`UrlAuthorizationModule`는 ASP.NET 런타임의 일부인 관리 코드입니다. Microsoft의 [인터넷 정보 서비스 (iis)](https://www.iis.net/) 웹 서버 버전 7 이전에는 IIS의 HTTP 파이프라인과 ASP.NET 런타임의 파이프라인 사이에 별도의 장애가 있었습니다. 간단히 말해서 IIS 6 및 이전 버전에서는 ASP. NET `UrlAuthorizationModule`는 요청이 IIS에서 ASP.NET 런타임으로 위임 된 경우에만 실행 됩니다. 기본적으로 IIS는 HTML 페이지와 CSS, JavaScript, 이미지 파일 등의 정적 콘텐츠 자체를 처리 하 고 `.aspx`, `.asmx`또는 `.ashx`의 확장명이 있는 페이지가 요청 된 경우에만 ASP.NET 런타임으로 요청을 전달 합니다.

그러나 IIS 7에서는 통합 IIS 및 ASP.NET 파이프라인을 사용할 수 있습니다. 몇 가지 구성 설정을 사용 하 여 모든 요청에 대해 URL 권한 부여 규칙을 정의할 수 있는 *모든* 요청에 대해 `UrlAuthorizationModule`를 호출 하는 IIS 7을 설치할 수 있습니다. 또한 IIS 7에는 자체 URL 권한 부여 엔진이 포함 되어 있습니다. ASP.NET integration 및 IIS 7의 기본 URL 인증 기능에 대 한 자세한 내용은 [IIS7 Url 권한 부여 이해](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)를 참조 하세요. ASP.NET 및 IIS 7 통합에 대 한 자세한 내용은 Shahram Khosravi의 서적, *전문 IIS 7 및 ASP.NET 통합 프로그래밍* (ISBN: 978-0470152539)의 복사본을 선택 하세요.

간단히 말해서 IIS 7 이전 버전에서 URL 권한 부여 규칙은 ASP.NET 런타임에 의해 처리 되는 리소스에만 적용 됩니다. 그러나 IIS 7을 사용 하면 IIS의 기본 URL 권한 부여 기능을 사용 하거나 ASP를 통합할 수 있습니다. NET은 IIS의 HTTP 파이프라인에 `UrlAuthorizationModule` 하 여이 기능을 모든 요청으로 확장 합니다.

> [!NOTE]
> ASP에 대 한 몇 가지 사소한 차이점이 있습니다. NET의 `UrlAuthorizationModule` 및 IIS 7의 URL 권한 부여 기능은 권한 부여 규칙을 처리 합니다. 이 자습서에서는 IIS 7의 URL 권한 부여 기능 또는 `UrlAuthorizationModule`와 비교 하 여 권한 부여 규칙을 구문 분석 하는 방법의 차이점을 검사 하지 않습니다. 이러한 항목에 대 한 자세한 내용은 MSDN 또는 [www.iis.net](https://www.iis.net/)에서 IIS 7 설명서를 참조 하십시오.

## <a name="step-1-defining-url-authorization-rules-inwebconfig"></a>1 단계:`Web.config`에서 URL 권한 부여 규칙 정의

`UrlAuthorizationModule`는 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙에 따라 특정 id에 대해 요청 된 리소스에 대 한 액세스를 허용 하거나 거부할지를 결정 합니다. 권한 부여 규칙은 `<allow>` 및 `<deny>` 자식 요소 형식으로 [`<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 에서 주석으로 처리 됩니다. 각 `<allow>` 및 `<deny>` 자식 요소는 다음을 지정할 수 있습니다.

- 특정 사용자
- 쉼표로 구분 된 사용자 목록입니다.
- 모든 익명 사용자는 물음표 (?)로 표시 됩니다.
- 별표 (\*)로 표시 된 모든 사용자

다음 태그는 URL 권한 부여 규칙을 사용 하 여 사용자에 게 Tito와 Scott을 허용 하 고 다른 모든 항목을 거부 하는 방법을 보여 줍니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample1.xml)]

`<allow>` 요소는 사용자에 게 허용 되는 사용자 (Tito와 Scott)를 정의 하는 반면 `<deny>` 요소는 *모든* 사용자가 거부 됨을 지시 합니다.

> [!NOTE]
> 또한 `<allow>` 및 `<deny>` 요소는 역할에 대 한 권한 부여 규칙을 지정할 수 있습니다. 이후 자습서에서 역할 기반 권한 부여를 살펴보겠습니다.

다음 설정은 익명 방문자를 비롯 하 여 Sam 이외의 사용자에 게 액세스 권한을 부여 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample2.xml)]

인증 된 사용자만 허용 하려면 모든 익명 사용자에 대 한 액세스를 거부 하는 다음 구성을 사용 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample3.xml)]

권한 부여 규칙은 `Web.config`의 `<system.web>` 요소 내에 정의 되며 웹 응용 프로그램의 모든 ASP.NET 리소스에 적용 됩니다. 응용 프로그램에는 다양 한 섹션에 대 한 서로 다른 권한 부여 규칙이 있을 때가 있습니다. 예를 들어, 전자 상거래 사이트에서 모든 방문자는 제품을 정독 하 고, 제품 리뷰를 참조 하 고, 카탈로그를 검색 하는 등의 방법을 사용할 수 있습니다. 그러나 인증 된 사용자만이 체크 아웃 또는 페이지에 연결 하 여 한 번의 배송 기록을 관리할 수 있습니다. 또한 사이트에는 사이트 관리자와 같은 선택 사용자만 액세스할 수 있는 부분이 있을 수 있습니다.

ASP.NET를 사용 하면 사이트의 서로 다른 파일 및 폴더에 대 한 다양 한 권한 부여 규칙을 쉽게 정의할 수 있습니다. 루트 폴더의 `Web.config` 파일에 지정 된 권한 부여 규칙은 사이트의 모든 ASP.NET 리소스에 적용 됩니다. 그러나 `<authorization>` 섹션에 `Web.config`를 추가 하 여 특정 폴더에 대해 이러한 기본 권한 부여 설정을 재정의할 수 있습니다.

인증 된 사용자만 `Membership` 폴더의 ASP.NET 페이지를 방문할 수 있도록 웹 사이트를 업데이트 해 보겠습니다. 이를 수행 하려면 `Membership` 폴더에 `Web.config` 파일을 추가 하 고 익명 사용자를 거부 하도록 권한 부여 설정을 설정 해야 합니다. 솔루션 탐색기에서 `Membership` 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 항목 추가 메뉴를 선택한 다음 `Web.config`라는 새 웹 구성 파일을 추가 합니다.

[멤버 자격 폴더에 web.config 파일을 추가 ![](user-based-authorization-vb/_static/image8.png)](user-based-authorization-vb/_static/image7.png)

**그림 3**: `Membership` 폴더에 `Web.config` 파일 추가 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image9.png))

이 시점에서 프로젝트는 두 개의 `Web.config` 파일을 포함 해야 합니다. 하나는 루트 디렉터리에 있고 하나는 `Membership` 폴더에 있습니다.

[이제 응용 프로그램에 두 개의 Web.config 파일이 포함 되어 있어야 합니다. ![](user-based-authorization-vb/_static/image11.png)](user-based-authorization-vb/_static/image10.png)

**그림 4**: 이제 응용 프로그램에 두 개의 `Web.config` 파일이 포함 되어 있어야 합니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image12.png)).

익명 사용자에 대 한 액세스를 금지 하도록 `Membership` 폴더의 구성 파일을 업데이트 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample4.xml)]

이것이 전부입니다!

이 변경 내용을 테스트 하려면 브라우저에서 홈 페이지를 방문 하 여 로그 아웃 되었는지 확인 합니다. ASP.NET 응용 프로그램의 기본 동작은 모든 방문자를 허용 하는 것이 고, 루트 디렉터리의 `Web.config` 파일에 대 한 권한 부여 수정 작업을 수행 하지 않았기 때문에, 루트 디렉터리의 파일을 익명 방문자로 방문할 수 있습니다.

왼쪽 열에 있는 사용자 계정 만들기 링크를 클릭 합니다. 그러면 `~/Membership/CreatingUserAccounts.aspx`으로 이동 합니다. `Membership` 폴더의 `Web.config` 파일은 익명 액세스를 금지 하는 권한 부여 규칙을 정의 하므로 `UrlAuthorizationModule`에서 요청을 중단 하 고 HTTP 401 권한 없음 상태를 반환 합니다. `FormsAuthenticationModule`는이를 302 리디렉션 상태로 수정 하 여 로그인 페이지로 보냅니다. 액세스 하려는 페이지 (`CreatingUserAccounts.aspx`)는 `ReturnUrl` querystring 매개 변수를 통해 로그인 페이지로 전달 됩니다.

[![는 URL 권한 부여 규칙에서 익명 액세스를 금지 하므로 로그인 페이지로 리디렉션됩니다.](user-based-authorization-vb/_static/image14.png)](user-based-authorization-vb/_static/image13.png)

**그림 5**: URL 권한 부여 규칙이 익명 액세스를 금지 하므로 로그인 페이지로 리디렉션됩니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image15.png)).

성공적으로 로그인 하면 `CreatingUserAccounts.aspx` 페이지로 리디렉션됩니다. 이번에는 `UrlAuthorizationModule`가 더 이상 익명이 아니기 때문에 페이지에 대 한 액세스를 허용 합니다.

### <a name="applying-url-authorization-rules-to-a-specific-location"></a>특정 위치에 URL 권한 부여 규칙 적용

`Web.config`의 `<system.web>` 섹션에 정의 된 권한 부여 설정은 해당 디렉터리 및 해당 하위 디렉터리에 있는 모든 ASP.NET 리소스에 적용 됩니다 (다른 `Web.config` 파일에서 다른 방법으로 재정의 될 때까지). 그러나 일부 경우에는 지정 된 디렉터리의 모든 ASP.NET 리소스가 특정 한 두 페이지를 제외 하 고 특정 권한 부여 구성을 갖도록 할 수 있습니다. 이렇게 하려면 `Web.config`에서 `<location>` 요소를 추가 하 고, 권한 부여 규칙이 다른 파일을 가리키고, 포함 된 고유한 권한 부여 규칙을 정의 하면 됩니다.

`<location>` 요소를 사용 하 여 특정 리소스에 대 한 구성 설정을 재정의 하는 방법에 대해 설명 하기 위해 Tito에서 `CreatingUserAccounts.aspx`를 방문할 수 있도록 권한 부여 설정을 사용자 지정 하겠습니다. 이 작업을 수행 하려면 `Membership` 폴더의 `Web.config` 파일에 `<location>` 요소를 추가 하 고 다음과 같이 표시 되도록 태그를 업데이트 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample5.xml)]

`<system.web>`의 `<authorization>` 요소는 `Membership` 폴더와 해당 하위 폴더의 ASP.NET 리소스에 대 한 기본 URL 권한 부여 규칙을 정의 합니다. `<location>` 요소를 사용 하면 특정 리소스에 대해 이러한 규칙을 재정의할 수 있습니다. 위의 태그에서 `<location>` 요소는 `CreatingUserAccounts.aspx` 페이지를 참조 하 고 Tito를 허용 하 고 다른 모든 사용자를 거부 하는 등의 권한 부여 규칙을 지정 합니다.

이 권한 부여 변경을 테스트 하려면 먼저 익명 사용자로 웹 사이트를 방문 하세요. `UserBasedAuthorization.aspx`와 같이 `Membership` 폴더의 모든 페이지를 방문 하려고 하면 `UrlAuthorizationModule` 요청을 거부 하 고 로그인 페이지로 리디렉션됩니다. 로 로그인 한 후에는 `CreatingUserAccounts.aspx`를 *제외 하* 고 `Membership` 폴더의 모든 페이지를 방문할 수 있습니다. 사용자로 로그온 한 `CreatingUserAccounts.aspx` 방문 하려고 시도 하면 무단 액세스 시도로 인해 로그인 페이지로 다시 리디렉션됩니다.

> [!NOTE]
> `<location>` 요소는 구성의 `<system.web>` 요소 외부에 표시 되어야 합니다. 재정의 하려는 권한 부여 설정이 포함 된 각 리소스에 대해 별도의 `<location>` 요소를 사용 해야 합니다.

### <a name="a-look-at-how-theurlauthorizationmoduleuses-the-authorization-rules-to-grant-or-deny-access"></a>`UrlAuthorizationModule`권한 부여 규칙을 사용 하 여 액세스 권한을 부여 하거나 거부 하는 방법에 대해 살펴봅니다.

`UrlAuthorizationModule`은 한 번에 하나씩 URL 권한 부여 규칙을 분석 하 여 특정 URL에 대 한 특정 id에 대 한 권한을 부여할 것인지 여부를 결정 합니다. 일치 항목이 발견 되는 즉시 사용자에 게 일치 항목을 `<allow>` 또는 `<deny>` 요소에서 찾을 수 있는지에 따라 액세스 권한이 부여 되거나 거부 됩니다. <strong>일치 항목을 찾을 수 없는 경우 사용자에 게 액세스 권한이 부여 됩니다.</strong> 따라서 액세스를 제한 하려는 경우에는 URL 권한 부여 구성에서 `<deny>` 요소를 마지막 요소로 사용 해야 합니다. <strong>`<deny>`</strong>요소를 생략 하면 <strong>모든 사용자에 게 액세스 권한이 부여 됩니다.</strong>

`UrlAuthorizationModule`에서 권한을 확인 하는 데 사용 하는 프로세스를 보다 잘 이해 하려면이 단계 앞부분에서 살펴본 URL 권한 부여 규칙 예제를 참조 하십시오. 첫 번째 규칙은 Tito와 Scott에 게 액세스를 허용 하는 `<allow>` 요소입니다. 두 번째 규칙은 모든 사용자에 대 한 액세스를 거부 하는 `<deny>` 요소입니다. 익명 사용자가 방문 하는 경우 `UrlAuthorizationModule`는 Scott 또는 Tito를 요청 하 여 시작 합니다. 분명히 대답은 아니요 이므로 두 번째 규칙으로 진행 됩니다. 모든 사람 집합에 익명이 있나요? 여기에서 답은 예 이므로 `<deny>` 규칙이 적용 되 고 방문자가 로그인 페이지로 리디렉션됩니다. 마찬가지로 Jisun이 방문 하는 경우에는 `UrlAuthorizationModule`에서 시작 하 여 Scott 또는 Tito를 요청 하 여 시작 합니다. 이는 그렇지 않기 때문에 두 번째 질문으로 진행 되 고, 모든 사람 집합에서 Jisun이 `UrlAuthorizationModule`? 그는 그에 대 한 액세스가 거부 되었습니다. 마지막으로,이를 방문 하는 경우 `UrlAuthorizationModule`에 의해 제기 되는 첫 번째 질문은 찬성 대답 이므로 Tito에는 액세스 권한이 부여 됩니다.

`UrlAuthorizationModule`은 위에서 아래로 권한 부여 규칙을 처리 하 여 모든 일치 항목에서 중지 하므로 보다 구체적인 규칙을 보다 구체적인 규칙 보다 먼저 배치 하는 것이 중요 합니다. 즉, Jisun 및 익명 사용자를 금지 하 고 다른 모든 인증 된 사용자를 허용 하는 권한 부여 규칙을 정의 하기 위해 가장 구체적인 규칙 (Jisun에 영향을 주는 규칙)부터 시작 하 여 더 낮은 특정 규칙 (다른 모든 것을 허용 하는 규칙)으로 시작 합니다. 인증 된 사용자 이지만 모든 익명 사용자를 거부 합니다. 다음 URL 권한 부여 규칙은 먼저 Jisun을 거부 하 고 익명 사용자를 거부 하 여이 정책을 구현 합니다. 이러한 `<deny>` 문이 모두 일치 하지 않기 때문에 Jisun 이외의 모든 인증 된 사용자에 게 액세스 권한이 부여 됩니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample6.xml)]

## <a name="step-2-fixing-the-workflow-for-unauthorized-authenticated-users"></a>2 단계: 승인 되지 않은 인증 된 사용자에 대 한 워크플로 수정

이 자습서의 앞부분에서 설명한 대로 URL 권한 부여 워크플로 살펴보기 섹션에서 transpires 권한이 없는 요청이 발생 하면 `UrlAuthorizationModule` 요청을 중단 하 고 HTTP 401 권한 없음 상태를 반환 합니다. 이 401 상태는 `FormsAuthenticationModule`에서 사용자를 로그인 페이지로 보내는 302 리디렉션 상태로 수정 됩니다. 이 워크플로는 사용자가 인증 된 경우에도 모든 권한이 없는 요청에서 발생 합니다.

인증 된 사용자를 로그인 페이지에 반환 하는 것은 시스템에 이미 로그인 했으므로 혼동 될 수 있습니다. 약간의 작업을 통해 제한 된 페이지에 액세스를 시도 하는 것을 설명 하는 페이지에 대 한 권한이 없는 요청을 하는 인증 된 사용자를 리디렉션하여이 워크플로를 개선할 수 있습니다.

`UnauthorizedAccess.aspx`이라는 웹 응용 프로그램의 루트 폴더에 새 ASP.NET 페이지를 만들어 시작 합니다. 이 페이지를 `Site.master` 마스터 페이지와 연결 하는 것을 잊지 마세요. 이 페이지를 만든 후에는 마스터 페이지의 기본 콘텐츠가 표시 되도록 `LoginContent` ContentPlaceHolder를 참조 하는 콘텐츠 컨트롤을 제거 합니다. 다음으로, 사용자가 보호 된 리소스에 액세스 하려고 시도 하는 상황을 설명 하는 메시지를 추가 합니다. 이러한 메시지를 추가한 후에는 `UnauthorizedAccess.aspx` 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample7.aspx)]

이제 인증 된 사용자가 무단 요청을 수행할 경우 로그인 페이지 대신 `UnauthorizedAccess.aspx` 페이지로 전송 되도록 워크플로를 변경 해야 합니다. 로그인 페이지에 대 한 권한이 없는 요청을 리디렉션하는 논리는 `FormsAuthenticationModule` 클래스의 private 메서드 내에 있으므로이 동작을 사용자 지정할 수 없습니다. 그러나 필요한 경우 사용자를 `UnauthorizedAccess.aspx`로 리디렉션하는 사용자 고유의 논리를 로그인 페이지에 추가 하는 것도 가능 합니다.

`FormsAuthenticationModule`는 권한이 없는 방문자를 로그인 페이지로 리디렉션하는 경우에는 이름이 `ReturnUrl`인 querystring에 요청 된 권한 없는 URL을 추가 합니다. 예를 들어 인증 되지 않은 사용자가 `OnlyTito.aspx`를 방문 하려고 하면 `FormsAuthenticationModule` `Login.aspx?ReturnUrl=OnlyTito.aspx`으로 리디렉션됩니다. 따라서 `ReturnUrl` 매개 변수를 포함 하는 querystring을 가진 인증 된 사용자가 로그인 페이지에 도달 하면이 인증 되지 않은 사용자는 볼 수 있는 권한이 없는 페이지를 방문 하려고 시도 했음을 알 수 있습니다. 이 경우 `UnauthorizedAccess.aspx`로 리디렉션하려고 합니다.

이 작업을 수행 하려면 로그인 페이지의 `Page_Load` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample8.vb)]

위의 코드는 인증 된 권한 없는 사용자를 `UnauthorizedAccess.aspx` 페이지로 리디렉션합니다. 이 논리를 작동 하는 것을 보려면 익명 방문자로 사이트를 방문 하 고 왼쪽 열에서 사용자 계정 만들기 링크를 클릭 합니다. 이렇게 하면 1 단계에서 Tito에 대 한 액세스만 허용 하도록 구성 된 `~/Membership/CreatingUserAccounts.aspx` 페이지로 이동 됩니다. 익명 사용자는 금지 되어 있으므로 `FormsAuthenticationModule` 로그인 페이지로 다시 리디렉션됩니다.

이 시점에서 익명 이므로 `Request.IsAuthenticated` `False`를 반환 하 고 `UnauthorizedAccess.aspx`으로 리디렉션되지 않습니다. 대신 로그인 페이지가 표시 됩니다. Bruce와 같이 Tito 이외의 사용자로 로그인 합니다. 적절 한 자격 증명을 입력 한 후에는 로그인 페이지를 다시 `~/Membership/CreatingUserAccounts.aspx`으로 리디렉션합니다. 그러나이 페이지는 Tito 에서만 액세스할 수 있으므로이 페이지를 볼 수 없으며 로그인 페이지로 즉시 반환 됩니다. 그러나 이번에는 `Request.IsAuthenticated` `True` (`ReturnUrl` 및 querystring 매개 변수가 존재 함)를 반환 하므로 `UnauthorizedAccess.aspx` 페이지로 리디렉션됩니다.

[인증 ![권한이 없는 사용자는 UnauthorizedAccess로 리디렉션됩니다.](user-based-authorization-vb/_static/image17.png)](user-based-authorization-vb/_static/image16.png)

**그림 6**: 인증 됨, 권한이 없는 사용자가 `UnauthorizedAccess.aspx`로 리디렉션 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image18.png))

이 사용자 지정 된 워크플로는 그림 2에 나와 있는 주기를 짧게 하 여 보다 합리적이 고 간단한 사용자 환경을 제공 합니다.

## <a name="step-3-limiting-functionality-based-on-the-currently-logged-in-user"></a>3 단계: 현재 로그인 한 사용자에 따라 기능 제한

URL 권한 부여를 사용 하면 정교 하지 않은 권한 부여 규칙을 쉽게 지정할 수 있습니다. 1 단계에서 살펴본 것 처럼 URL 권한 부여를 사용 하면 허용 되는 id와 특정 페이지 또는 폴더의 모든 페이지를 볼 수 없도록 거부 된 id를 간략하게 수 있습니다. 그러나 특정 시나리오에서는 모든 사용자가 페이지를 방문 하도록 허용할 수 있지만 해당 페이지를 방문 하는 사용자에 따라 페이지의 기능을 제한할 수 있습니다.

인증 된 방문자가 제품을 검토할 수 있도록 하는 전자 상거래 웹 사이트의 경우를 고려 합니다. 익명 사용자가 제품의 페이지를 방문 하면 제품 정보만 표시 되 고 검토를 남길 기회가 제공 되지 않습니다. 그러나 동일한 페이지를 방문 하는 인증 된 사용자는 검토 인터페이스를 볼 수 있습니다. 인증 된 사용자가이 제품을 아직 검토 하지 않은 경우 인터페이스를 사용 하 여 검토를 제출할 수 있습니다. 그렇지 않으면 이전에 제출 된 검토를 표시 합니다. 이 시나리오에 대 한 단계를 수행 하기 위해 제품 페이지에 추가 정보가 표시 되 고 전자 상거래 회사에서 작업 하는 사용자에 게 확장 기능이 제공 될 수 있습니다. 예를 들어 제품 페이지에서 재고를 재고 목록으로 나열 하 고 직원 들이 방문할 때 제품의 가격과 설명을 편집 하는 옵션을 포함할 수 있습니다.

이러한 미세 수준 권한 부여 규칙은 선언적으로 또는 프로그래밍 방식으로 구현 하거나 둘 중 일부를 조합 하 여 구현할 수 있습니다. 다음 섹션에서는 LoginView 컨트롤을 통해 미세 인증을 구현 하는 방법을 알아봅니다. 다음에는 프로그래밍 방식으로 살펴볼 것입니다. 그러나 세분화 된 권한 부여 규칙을 적용 하는 방법에 대 한 자세한 내용은 먼저 해당 기능이 있는 사용자에 따라 달라 지는 페이지를 만들어야 합니다.

GridView 내의 특정 디렉터리에 있는 파일을 나열 하는 페이지를 만들어 보겠습니다. GridView에는 각 파일의 이름, 크기 및 기타 정보를 나열 하는 것과 함께 Linkbutton의 두 열이 포함 됩니다. 하나는 뷰이 고 하나는 Delete입니다. LinkButton 보기를 클릭 하면 선택한 파일의 내용이 표시 됩니다. Delete LinkButton를 클릭 하면 파일이 삭제 됩니다. 처음에는 모든 사용자가 해당 보기 및 삭제 기능을 사용할 수 있도록이 페이지를 만들어 보겠습니다. LoginView 컨트롤을 사용 하 고 프로그래밍 방식으로 기능을 제한 섹션에서는 페이지를 방문 하는 사용자에 따라 이러한 기능을 사용 하거나 사용 하지 않도록 설정 하는 방법을 알아봅니다.

> [!NOTE]
> 빌드 하려는 ASP.NET 페이지에서 GridView 컨트롤을 사용 하 여 파일 목록을 표시 합니다. 이 자습서 시리즈는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 둘 수 있으므로 GridView 컨트롤의 내부 작업에 대해 너무 많은 시간을 할애 하지 않으려고 합니다. 이 자습서에서는이 페이지를 설정 하는 방법에 대 한 구체적인 단계별 지침을 제공 하지만 특정 항목을 선택 하는 이유와 렌더링 된 출력에 적용 되는 특정 속성에 대 한 자세한 내용은 설명 하지 않습니다. GridView 컨트롤을 철저 하 게 검사 하려면 *[ASP.NET 2.0 자습서 시리즈의 데이터로 작업](../../data-access/index.md)* 을 참조 하세요.

먼저 `Membership` 폴더에서 `UserBasedAuthorization.aspx` 파일을 열고 `FilesGrid`라는 페이지에 GridView 컨트롤을 추가 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 필드 대화 상자를 시작 합니다. 여기에서 왼쪽 아래 모서리에 있는 필드 자동 생성 확인란의 선택을 취소 합니다. 그런 다음 왼쪽 위 모서리에서 선택 단추, 삭제 단추 및 두 개의 BoundFields를 추가 합니다 (선택 및 삭제 단추는 CommandField type 아래에 있음). 선택 단추의 `SelectText` 속성을 View로 설정 하 고, 첫 번째 BoundField의 `HeaderText` 및 `DataField` 속성을 Name으로 설정 합니다. 두 번째 BoundField의 `HeaderText` 속성을 크기 (바이트)로 설정 하 고 `DataField` 속성을 Length로 설정 하 고 `DataFormatString` 속성을 {0:N0}로 설정 하 고 해당 `HtmlEncode` 속성을 False로 설정 합니다.

GridView의 열을 구성한 후 확인을 클릭 하 여 필드 대화 상자를 닫습니다. 속성 창에서 GridView의 `DataKeyNames` 속성을 `FullName`로 설정 합니다. 이 시점에서 GridView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample9.aspx)]

GridView의 태그가 만들어지면 특정 디렉터리에 있는 파일을 검색 하 고 GridView에 바인딩하는 코드를 작성할 준비가 되었습니다. 페이지의 `Page_Load` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample10.vb)]

위의 코드는 [`DirectoryInfo` 클래스](https://msdn.microsoft.com/library/system.io.directoryinfo.aspx) 를 사용 하 여 응용 프로그램의 루트 폴더에 있는 파일 목록을 가져옵니다. [`GetFiles()` 메서드](https://msdn.microsoft.com/library/system.io.directoryinfo.getfiles.aspx) 는 디렉터리의 모든 파일을 [`FileInfo` 개체](https://msdn.microsoft.com/library/system.io.fileinfo.aspx)배열로 반환 합니다. 그러면이 파일은 GridView에 바인딩됩니다. `FileInfo` 개체에는 `Name`, `Length`, `IsReadOnly`등 다른 속성 모음이 있습니다. 선언 태그에서 볼 수 있듯이 GridView는 `Name` 및 `Length` 속성만 표시 합니다.

> [!NOTE]
> `DirectoryInfo` 및 `FileInfo` 클래스는 [`System.IO` 네임 스페이스](https://msdn.microsoft.com/library/system.io.aspx)에 있습니다. 따라서 이러한 클래스 이름 앞에 네임 스페이스 이름을 사용 하거나 네임 스페이스를 클래스 파일 (`Imports System.IO`을 통해)로 가져와야 합니다.

잠시 시간을 내 서 브라우저를 통해이 페이지를 방문 하세요. 응용 프로그램의 루트 디렉터리에 있는 파일의 목록이 표시 됩니다. 뷰를 클릭 하거나 Linkbutton을 삭제 하면 다시 게시가 발생 하지만 필요한 이벤트 처리기를 아직 만들지 않았기 때문에 아무 동작도 발생 하지 않습니다.

[![GridView에서 웹 응용 프로그램의 루트 디렉터리에 있는 파일을 나열 합니다.](user-based-authorization-vb/_static/image20.png)](user-based-authorization-vb/_static/image19.png)

**그림 7**: GridView는 웹 응용 프로그램의 루트 디렉터리에 있는 파일을 나열 합니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image21.png)).

선택한 파일의 콘텐츠를 표시 하는 방법이 필요 합니다. Visual Studio로 돌아가서 GridView 위에 `FileContents` 이라는 텍스트 상자를 추가 합니다. `TextMode` 속성을 `MultiLine`로 설정 하 고 해당 `Columns` 및 `Rows` 속성을 각각 95% 및 10으로 설정 합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample11.aspx)]

다음으로 GridView의 [`SelectedIndexChanged` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindexchanged.aspx) 에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample12.vb)]

이 코드는 GridView의 `SelectedValue` 속성을 사용 하 여 선택한 파일의 전체 파일 이름을 확인 합니다. 내부적으로는 `DataKeys` 컬렉션을 참조 하 여 `SelectedValue`를 가져오기 때문에이 단계 앞부분에서 설명한 대로 GridView의 `DataKeyNames` 속성을 Name으로 설정 해야 합니다. [`File` 클래스](https://msdn.microsoft.com/library/system.io.file.aspx) 는 선택한 파일의 내용을 문자열로 읽어 `FileContents` 텍스트 상자의 `Text` 속성에 할당 하 여 페이지에서 선택한 파일의 내용을 표시 하는 데 사용 됩니다.

[선택한 파일의 내용이 텍스트 상자에 표시 ![](user-based-authorization-vb/_static/image23.png)](user-based-authorization-vb/_static/image22.png)

**그림 8**: 선택한 파일의 내용이 텍스트 상자에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image24.png)).

> [!NOTE]
> HTML 태그를 포함 하는 파일의 내용을 확인 한 후 파일을 보거나 삭제 하려고 하면 `HttpRequestValidationException` 오류가 표시 됩니다. 이는 포스트백 시 텍스트 상자 내용이 웹 서버로 다시 전송 되기 때문에 발생 합니다. 기본적으로 ASP.NET는 잠재적으로 위험한 포스트백 콘텐츠 (예: HTML 태그)가 검색 될 때마다 `HttpRequestValidationException` 오류를 발생 시킵니다. 이 오류가 발생 하지 않도록 하려면 `@Page` 지시문에 `ValidateRequest="false"`를 추가 하 여 페이지에 대 한 요청 유효성 검사를 해제 합니다. 요청 유효성 검사의 이점 및 사용 하지 않도록 설정할 때 수행 해야 하는 예방 조치에 대 한 자세한 내용은 [요청 유효성 검사-스크립트 공격 방지](https://asp.net/learn/whitepapers/request-validation/)를 참조 하세요.

마지막으로 GridView의 [`RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx)에 대해 다음 코드를 사용 하 여 이벤트 처리기를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample13.vb)]

코드는 실제로 파일을 삭제 *하지 않고* `FileContents` 텍스트 상자에서 삭제할 파일의 전체 이름을 표시 합니다.

[삭제 단추를 클릭 하 ![파일을 실제로 삭제 하지는 않습니다.](user-based-authorization-vb/_static/image26.png)](user-based-authorization-vb/_static/image25.png)

**그림 9**: 삭제 단추를 클릭 해도 파일이 실제로 삭제 되지 않음 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image27.png))

1 단계에서는 익명 사용자가 `Membership` 폴더의 페이지를 볼 수 없도록 URL 권한 부여 규칙을 구성 했습니다. 보다 확실 한 인증을 위해 익명 사용자가 `UserBasedAuthorization.aspx` 페이지를 방문 하 고 제한 된 기능을 사용할 수 있도록 합니다. 이 페이지를 모든 사용자가 액세스할 수 있는 상태로 열려면 `Membership` 폴더의 `Web.config` 파일에 다음 `<location>` 요소를 추가 합니다.

[!code-xml[Main](user-based-authorization-vb/samples/sample14.xml)]

이 `<location>` 요소를 추가한 후에는 사이트에서 로그 아웃 하 여 새 URL 권한 부여 규칙을 테스트 합니다. 익명 사용자는 `UserBasedAuthorization.aspx` 페이지를 방문할 수 있습니다.

현재는 인증 된 사용자 또는 익명 사용자가 `UserBasedAuthorization.aspx` 페이지를 방문 하 여 파일을 보거나 삭제할 수 있습니다. 즉, 인증 된 사용자만 파일의 콘텐츠를 볼 수 있고 Tito는 파일을 삭제할 수 있게 합니다. 이러한 미세 수준 권한 부여 규칙은 선언적으로 또는 두 방법의 조합을 통해 적용할 수 있습니다. 선언적 방법을 사용 하 여 파일의 내용을 볼 수 있는 사용자를 제한 하겠습니다. 프로그래밍 방식을 사용 하 여 파일을 삭제할 수 있는 사용자를 제한 합니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤 사용

이전 자습서에서 살펴본 것 처럼 LoginView 컨트롤은 인증 된 사용자와 익명 사용자에 대해 서로 다른 인터페이스를 표시 하는 데 유용 하며 익명 사용자가 액세스할 수 없는 기능을 숨기는 간편한 방법을 제공 합니다. 익명 사용자는 파일을 보거나 삭제할 수 없으므로 인증 된 사용자가 페이지를 방문 하는 경우에만 `FileContents` 텍스트 상자를 표시 해야 합니다. 이렇게 하려면 LoginView 컨트롤을 페이지에 추가 하 고 이름을 `LoginViewForFileContentsTextBox`로 `FileContents` 한 다음 텍스트 상자의 선언 태그를 LoginView 컨트롤의 `LoggedInTemplate`로 이동 합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample15.aspx)]

LoginView의 템플릿에 있는 웹 컨트롤은 더 이상 코드 지향 클래스에서 직접 액세스할 수 없습니다. 예를 들어 `FilesGrid` GridView의 `SelectedIndexChanged` 및 `RowDeleting` 이벤트 처리기는 현재 다음과 같은 코드를 사용 하 여 `FileContents` TextBox 컨트롤을 참조 합니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample16.aspx)]

그러나이 코드는 더 이상 유효 하지 않습니다. `FileContents` TextBox를 `LoggedInTemplate`으로 이동 하 여 텍스트 상자를 직접 액세스할 수 없습니다. 대신 `FindControl("controlId")` 메서드를 사용 하 여 프로그래밍 방식으로 컨트롤을 참조 해야 합니다. 다음과 같이 텍스트 상자를 참조 하도록 `FilesGrid` 이벤트 처리기를 업데이트 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample17.vb)]

텍스트 상자를 LoginView의 `LoggedInTemplate`로 이동 하 고 페이지의 코드를 업데이트 하 여 `FindControl("controlId")` 패턴을 사용 하 여 텍스트 상자를 참조 한 후에는 해당 페이지를 익명 사용자로 방문 합니다. 그림 10에 표시 된 것 처럼 `FileContents` TextBox는 표시 되지 않습니다. 그러나 뷰 LinkButton는 계속 표시 됩니다.

[![LoginView 컨트롤은 인증 된 사용자에 대 한 FileContents TextBox만 렌더링 합니다.](user-based-authorization-vb/_static/image29.png)](user-based-authorization-vb/_static/image28.png)

**그림 10**: LoginView 컨트롤이 인증 된 사용자에 대 한 `FileContents` TextBox만 렌더링 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image30.png))

익명 사용자에 대 한 보기 단추를 숨기는 한 가지 방법은 GridView 필드를 Templatefield로 변환 변환 하는 것입니다. 이렇게 하면 LinkButton 뷰의 선언적 태그가 포함 된 템플릿이 생성 됩니다. 그런 다음 Templatefield로 변환에 LoginView 컨트롤을 추가 하 고 LinkButton를 LoginView의 `LoggedInTemplate`내에 저장 하 여 익명 방문자의 보기 단추를 숨길 수 있습니다. 이를 수행 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 필드 대화 상자를 시작 합니다. 그런 다음 왼쪽 아래 모퉁이의 목록에서 선택 단추를 선택 하 고이 필드를 Templatefield로 변환로 변환 링크를 클릭 합니다. 이렇게 하면 필드의 선언적 태그가 다음과 같이 수정 됩니다.

[!code-aspx[Main](user-based-authorization-vb/samples/sample18.aspx)]

 받는 사람: 

[!code-aspx[Main](user-based-authorization-vb/samples/sample19.aspx)]

 이 시점에서 LoginView을 Templatefield로 변환에 추가할 수 있습니다. 다음 태그는 인증 된 사용자에 대 한 뷰 LinkButton 표시 합니다. 

[!code-aspx[Main](user-based-authorization-vb/samples/sample20.aspx)]

그림 11에 표시 된 것 처럼 열 내의 뷰 Linkbutton이 숨겨진 경우에도 결과는 보기 열이 표시 되지 않습니다. 다음 섹션에서는 LinkButton 뿐 아니라 전체 GridView 열을 숨기는 방법을 살펴보겠습니다.

[LoginView 컨트롤 ![익명 방문자의 Linkbutton 보기를 숨깁니다.](user-based-authorization-vb/_static/image32.png)](user-based-authorization-vb/_static/image31.png)

**그림 11**: LoginView 컨트롤은 익명 방문자에 대 한 뷰 Linkbutton을 숨깁니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image33.png)).

### <a name="programmatically-limiting-functionality"></a>프로그래밍 방식으로 기능 제한

일부 경우에는 기능을 페이지에 제한 하기 위한 선언적 기술이 충분 하지 않습니다. 예를 들어 특정 페이지 기능의 가용성은 해당 페이지를 방문 하는 사용자가 익명 인지 아니면 인증 되었는지를 초과 하는 조건에 따라 달라질 수 있습니다. 이러한 경우 다양 한 사용자 인터페이스 요소를 프로그래밍 방식으로 표시 하거나 숨길 수 있습니다.

프로그래밍 방식으로 기능을 제한 하려면 다음 두 가지 작업을 수행 해야 합니다.

1. 페이지를 방문 하는 사용자가 해당 기능에 액세스할 수 있는지 여부를 확인 합니다.
2. 사용자가 문제의 기능에 액세스할 수 있는지 여부에 따라 프로그래밍 방식으로 사용자 인터페이스를 수정 합니다.

이러한 두 태스크의 적용을 보여 주기 위해 Tito가 GridView에서 파일을 삭제 하도록 허용 하기만 하면 됩니다. 첫 번째 작업은 페이지를 방문 하 고 있는지 여부를 확인 하는 것입니다. 이를 확인 한 후 GridView의 Delete 열을 숨기 거 나 표시 해야 합니다. GridView의 열은 해당 `Columns` 속성을 통해 액세스할 수 있습니다. 열은 `Visible` 속성이 `True` (기본값)로 설정 된 경우에만 렌더링 됩니다.

데이터를 GridView에 바인딩하기 전에 `Page_Load` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample21.vb)]

[*폼 인증 자습서 개요*](../introduction/an-overview-of-forms-authentication-vb.md) 에서 설명한 것 처럼 `User.Identity.Name`는 id의 이름을 반환 합니다. 이는 로그인 컨트롤에 입력 한 사용자 이름에 해당 합니다. 페이지를 방문 하는 것 이라면 GridView의 두 번째 열 `Visible` 속성이 `True`로 설정 됩니다. 그렇지 않으면 `False`로 설정 됩니다. 결과적으로 Tito이 아닌 다른 사용자가 인증 된 다른 사용자 또는 익명 사용자로 페이지를 방문 하는 경우 삭제 열은 렌더링 되지 않습니다 (그림 12 참조). 그러나 Tito 페이지를 방문 하는 경우 삭제 열이 있습니다 (그림 13 참조).

[Tito 이외의 다른 사람이 방문 하는 경우 (예: Bruce) 삭제 열이 렌더링 되지 ![](user-based-authorization-vb/_static/image35.png)](user-based-authorization-vb/_static/image34.png)

**그림 12**: Tito (예: bruce)가 아닌 다른 사용자가 방문 하는 경우 삭제 열은 렌더링 되지 않습니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image36.png)).

[Tito에 대해 Delete 열이 렌더링 ![](user-based-authorization-vb/_static/image38.png)](user-based-authorization-vb/_static/image37.png)

**그림 13**: tito에 대해 삭제 열 렌더링 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image39.png))

## <a name="step-4-applying-authorization-rules-to-classes-and-methods"></a>4 단계: 클래스 및 메서드에 권한 부여 규칙 적용

3 단계에서는 익명 사용자가 파일의 내용을 볼 수 없으며, 파일을 삭제 하는 것을 허용 하지 않습니다. 이는 선언적 및 프로그래밍 기법을 통해 권한 없는 방문자에 대 한 연결 된 사용자 인터페이스 요소를 숨겨서 수행 했습니다. 간단한 예제에서는 사용자 인터페이스 요소를 올바르게 숨기는 것은 간단 하지만 동일한 기능을 수행 하는 다양 한 방법이 있을 수 있는 보다 복잡 한 사이트에 대 한 정보는 무엇 인가요? 해당 기능을 권한 없는 사용자로 제한 하면 적용 가능한 모든 사용자 인터페이스 요소를 숨기 거 나 사용 하지 않도록 설정 하는 것을 잊은 경우 어떻게 되나요?

권한이 없는 사용자가 특정 기능의 특정 부분에 액세스할 수 없도록 하는 쉬운 방법은 해당 클래스 또는 메서드를 [`PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)으로 데코레이팅 하는 것입니다. .NET 런타임에서 클래스를 사용 하거나 해당 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트에 클래스를 사용 하거나 메서드를 실행할 수 있는 권한이 있는지 확인 합니다. `PrincipalPermission` 특성은 이러한 규칙을 정의할 수 있는 메커니즘을 제공 합니다.

GridView의 `SelectedIndexChanged`에 `PrincipalPermission` 특성을 사용 하 고 이벤트 처리기를 `RowDeleting` 하 여 익명 사용자 및 Tito 이외의 사용자가 각각 실행 하지 못하도록 하는 방법을 보여 줍니다. 각 함수 정의 위에 적절 한 특성을 추가 하기만 하면 됩니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample22.vb)]

`SelectedIndexChanged` 이벤트 처리기에 대 한 특성은 인증 된 사용자만 이벤트 처리기를 실행할 수 있도록 지시 합니다. 여기서 `RowDeleting` 이벤트 처리기의 특성은 실행을 Tito로 제한 합니다.

> [!NOTE]
> 특성은 클래스, 메서드, 속성 또는 이벤트에 적용할 수 있습니다. 특성을 추가할 때 클래스, 메서드, 속성 또는 이벤트 선언 문의 일부 여야 합니다. Visual Basic는 줄 바꿈을 문 구분 기호로 사용 하므로 특성은 선언과 같은 줄에 표시 되거나 줄 연속 문자 (밑줄)를 사용 하 여 바로 위에 표시 되어야 합니다. 위의 코드 조각에서 줄 연속 문자를 사용 하 여 한 줄에 특성을 추가 하 고 메서드 선언을 다른 줄에 추가 합니다.

이 `RowDeleting` 이벤트 처리기 또는 인증 되지 않은 사용자가 `SelectedIndexChanged` 이벤트 처리기를 실행 하려고 시도 하는 경우, .NET 런타임에서 `SecurityException`발생 합니다.

[![보안 컨텍스트가 메서드를 실행할 수 있는 권한이 없으면 SecurityException이 Throw 됩니다.](user-based-authorization-vb/_static/image41.png)](user-based-authorization-vb/_static/image40.png)

**그림 14**: 보안 컨텍스트에 메서드를 실행할 수 있는 권한이 없는 경우 `SecurityException`이 throw 됩니다 ([전체 크기 이미지를 보려면 클릭](user-based-authorization-vb/_static/image42.png)).

> [!NOTE]
> 여러 보안 컨텍스트에서 클래스 또는 메서드에 액세스 하도록 허용 하려면 클래스 또는 메서드를 각 보안 컨텍스트의 `PrincipalPermission` 특성으로 데코 레이트 합니다. 즉, Tito와 Bruce 모두 `RowDeleting` 이벤트 처리기를 실행할 수 있도록 하려면 *두 개의* `PrincipalPermission` 특성을 추가 합니다.

[!code-vb[Main](user-based-authorization-vb/samples/sample23.vb)]

ASP.NET 페이지 외에도 많은 응용 프로그램에는 비즈니스 논리 및 데이터 액세스 계층과 같은 다양 한 계층을 포함 하는 아키텍처가 있습니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 되며 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 구현 클래스와 메서드를 제공 합니다. `PrincipalPermission` 특성은 이러한 계층에 권한 부여 규칙을 적용 하는 데 유용 합니다.

`PrincipalPermission` 특성을 사용 하 여 클래스 및 메서드에 대 한 권한 부여 규칙을 정의 하는 방법에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [`PrincipalPermissionAttributes`를 사용 하 여 비즈니스 및 데이터 계층에 권한 부여 규칙 추가 ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)를 참조 하세요.

## <a name="summary"></a>요약

이 자습서에서는 사용자 기반 권한 부여 규칙을 적용 하는 방법을 살펴보았습니다. ASP를 살펴보세요. NET의 URL 권한 부여 프레임 워크입니다. 각 요청에서 ASP.NET 엔진의 `UrlAuthorizationModule`는 응용 프로그램의 구성에 정의 된 URL 권한 부여 규칙을 검사 하 여 해당 id가 요청 된 리소스에 액세스할 수 있는 권한이 있는지 여부를 확인 합니다. 간단히 말해서 URL 권한 부여를 사용 하면 특정 페이지 또는 특정 디렉터리에 있는 모든 페이지에 대 한 권한 부여 규칙을 쉽게 지정할 수 있습니다.

URL 권한 부여 프레임 워크는 페이지 별로 권한 부여 규칙을 적용 합니다. URL 권한 부여를 사용 하면 요청 하는 id에 특정 리소스에 액세스할 수 있는 권한이 부여 됩니다. 그러나 많은 시나리오에서 보다 세부적인 권한 부여 규칙을 호출 합니다. 페이지에 액세스할 수 있는 사용자를 정의 하는 대신 모든 사람이 페이지에 액세스 하도록 허용 하 고 다른 데이터를 표시 하거나 페이지를 방문 하는 사용자에 따라 다른 기능을 제공 해야 할 수 있습니다. 페이지 수준 권한 부여는 권한이 없는 사용자가 금지 기능에 액세스 하지 못하도록 하기 위해 특정 사용자 인터페이스 요소를 숨기는 것을 포함 합니다. 또한 특성을 사용 하 여 클래스에 대 한 액세스를 제한 하 고 특정 사용자에 대 한 메서드를 실행할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [`PrincipalPermissionAttributes`를 사용 하 여 비즈니스 및 데이터 계층에 권한 부여 규칙 추가](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [IIS6와 IIS7 보안 간의 변경 내용](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [특정 파일 및 하위 디렉터리 구성](https://msdn.microsoft.com/library/6hbkh9s7.aspx)
- [사용자에 따라 데이터 수정 기능 제한](../../data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb.md)
- [LoginView 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/loginview.aspx)
- [IIS7 URL 권한 부여 이해](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)
- [`UrlAuthorizationModule` 기술 문서](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)
- [ASP.NET 2.0에서 데이터 작업](../../data-access/index.md)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](validating-user-credentials-against-the-membership-user-store-vb.md)
> [다음](storing-additional-user-information-vb.md)
