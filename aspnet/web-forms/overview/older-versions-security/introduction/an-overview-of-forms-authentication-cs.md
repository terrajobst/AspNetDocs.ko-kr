---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
title: 폼 인증 개요 (C#) | Microsoft Docs
author: rick-anderson
description: 사용자 지정 경로 만들기
ms.author: riande
ms.date: 01/14/2008
ms.assetid: de2d65b9-aadc-42ba-abe1-4e87e66521a0
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 009c3f84e00d648ede4a15e530ceac2d23e01eec
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620746"
---
# <a name="an-overview-of-forms-authentication-c"></a>폼 인증 개요 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_cs.pdf)

> 이 자습서에서는 구현에 대 한 단순한 토론을 사용 합니다. 특히 폼 인증을 구현 하는 방법을 살펴보겠습니다. 이 자습서에서 생성 하기 시작 하는 웹 응용 프로그램은 간단한 폼 인증에서 멤버 자격 및 역할로 이동 하는 이후 자습서에서 계속 빌드됩니다.
> 
> 이 항목에 대 한 자세한 내용은 [ASP.NET에서 기본 폼 인증 사용](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)을 참조 하세요.

## <a name="introduction"></a>소개

[이전 자습서](security-basics-and-asp-net-support-cs.md) 에서는 ASP.NET에서 제공 하는 다양 한 인증, 권한 부여 및 사용자 계정 옵션에 대해 설명 했습니다. 이 자습서에서는 구현에 대 한 단순한 토론을 사용 합니다. 특히 폼 인증을 구현 하는 방법을 살펴보겠습니다. 이 자습서에서 생성 하기 시작 하는 웹 응용 프로그램은 간단한 폼 인증에서 멤버 자격 및 역할로 이동 하는 이후 자습서에서 계속 빌드됩니다.

이 자습서는 이전 자습서에서 다루는 토픽 인 forms 인증 워크플로를 자세히 살펴보는 것으로 시작 합니다. 다음으로 폼 인증의 개념을 시연 하는 데 사용할 ASP.NET 웹 사이트를 만들게 됩니다. 다음으로 폼 인증을 사용 하 고, 간단한 로그인 페이지를 만들고, 사용자가 인증 되었는지 여부를 확인 하는 방법 및 사용자가 로그인 한 사용자 이름을 코드에서 확인 하는 방법을 확인 합니다.

웹 응용 프로그램에서 폼 인증 워크플로를 사용 하도록 설정 하 고 로그인 및 로그 오프 페이지를 만드는 것은 사용자 계정을 지원 하 고 웹 페이지를 통해 사용자를 인증 하는 ASP.NET 응용 프로그램을 구축 하는 모든 중요 한 단계입니다. 이로 인해 이러한 자습서는 서로를 기반으로 하기 때문에 이전 프로젝트에서 폼 인증을 구성 하는 경험이 이미 있는 경우에도이 자습서를 계속 진행 하기 전에 전체에서이 자습서를 진행 하는 것이 좋습니다.

## <a name="understanding-the-forms-authentication-workflow"></a>폼 인증 워크플로 이해

ASP.NET 런타임이 ASP.NET 페이지 또는 ASP.NET 웹 서비스와 같은 ASP.NET 리소스에 대 한 요청을 처리 하는 경우 요청은 수명 주기 동안 여러 이벤트를 발생 시킵니다. 요청의 시작 및 최소 끝에서 발생 하는 이벤트, 요청이 인증 되 고 권한이 부여 되 면 발생 하는 이벤트, 처리 되지 않은 예외 발생 시 발생 한 이벤트 등이 있습니다. 이벤트의 전체 목록을 보려면 [HttpApplication 개체의 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx)를 참조 하세요.

*HTTP 모듈* 은 요청 수명 주기의 특정 이벤트에 대 한 응답으로 코드가 실행 되는 관리 되는 클래스입니다. ASP.NET는 백그라운드에서 필수 작업을 수행 하는 다양 한 HTTP 모듈과 함께 제공 됩니다. 특히 논의와 관련 된 두 가지 기본 제공 HTTP 모듈은 다음과 같습니다.

- **[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** – 일반적으로 사용자의 쿠키 컬렉션에 포함 되는 폼 인증 티켓을 검사 하 여 사용자를 인증 합니다. 폼 인증 티켓이 없는 경우 사용자는 익명입니다.
- **[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** – 현재 사용자에 게 요청 된 URL에 액세스할 수 있는 권한이 있는지 여부를 확인 합니다. 이 모듈은 응용 프로그램의 구성 파일에 지정 된 권한 부여 규칙을 확인 하 여 권한을 확인 합니다. ASP.NET에는 요청 된 파일 Acl을 참조 하 여 권한을 결정 하는 [`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) 포함 되어 있습니다.

`FormsAuthenticationModule`는 `UrlAuthorizationModule` (및 `FileAuthorizationModule`)를 실행 하기 전에 사용자를 인증 하려고 시도 합니다. 요청 하는 사용자에 게 요청 된 리소스에 대 한 액세스 권한이 없는 경우 권한 부여 모듈은 요청을 종료 하 고 [HTTP 401 권한 없음](http://www.checkupdown.com/status/E401.html) 상태를 반환 합니다. Windows 인증 시나리오에서 HTTP 401 상태가 브라우저에 반환 됩니다. 이 상태 코드를 사용 하면 브라우저에서 모달 대화 상자를 통해 사용자에 게 자격 증명을 입력 하 라는 메시지를 표시 합니다. 그러나 폼 인증을 사용 하는 경우 FormsAuthenticationModule에서이 상태를 검색 하 고이를 수정 하 여 사용자를 대신 로그인 페이지로 리디렉션하도록 ( [http 302 리디렉션](http://www.checkupdown.com/status/E302.html) 상태를 통해) Http 401 권한 없음 상태가 브라우저로 전송 되지 않습니다.

로그인 페이지의 책임은 사용자의 자격 증명이 유효한 지 확인 하 고, 그렇다면 폼 인증 티켓을 만들고 사용자를 방문 하려고 했던 페이지로 다시 리디렉션하는 것입니다. 인증 티켓은 `FormsAuthenticationModule`에서 사용자를 식별 하는 데 사용 하는 웹 사이트의 페이지에 대 한 후속 요청에 포함 됩니다.

![폼 인증 워크플로](an-overview-of-forms-authentication-cs/_static/image1.png)

**그림 1**: 폼 인증 워크플로

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>페이지 방문 간 인증 티켓 기억

로그인 한 후에는 사용자가 사이트를 찾아볼 때 로그인 상태를 유지 하도록 각 요청에서 폼 인증 티켓을 웹 서버로 다시 전송 해야 합니다. 이는 일반적으로 사용자의 쿠키 컬렉션에 인증 티켓을 배치 하 여 수행 됩니다. [쿠키](http://en.wikipedia.org/wiki/HTTP_cookie) 는 사용자의 컴퓨터에 상주 하며 쿠키를 만든 웹 사이트에 대 한 각 요청에서 HTTP 헤더에 전송 되는 작은 텍스트 파일입니다. 따라서 폼 인증 티켓을 만들어 브라우저의 쿠키에 저장 한 후에는 해당 사이트에 대 한 각 후속 방문에서 요청과 함께 인증 티켓을 전송 하 여 사용자를 식별 합니다.

쿠키의 한 가지 측면은 브라우저에서 쿠키를 삭제 하는 날짜와 시간인 만료입니다. 폼 인증 쿠키가 만료 되 면 사용자는 더 이상 인증할 수 없으므로 익명이 됩니다. 사용자가 공용 터미널에서 방문 하는 경우 브라우저를 닫을 때 인증 티켓이 만료 되 게 할 수 있습니다. 그러나 홈에서 방문할 때 동일한 사용자가 사이트를 방문할 때마다 다시 로그인 하지 않아도 되도록 브라우저를 다시 시작 하는 동안 인증 티켓이 기억 되도록 할 수 있습니다. 이러한 결정은 사용자가 로그인 페이지에서 "사용자 이름" 확인란을 선택 하는 경우가 많습니다. 3 단계에서는 로그인 페이지에서 "암호 기억을" 확인란을 구현 하는 방법을 살펴봅니다. 다음 자습서에서는 인증 티켓 시간 제한 설정을 자세히 다룹니다.

> [!NOTE]
> 웹 사이트에 로그온 하는 데 사용 된 사용자 에이전트가 쿠키를 지원 하지 않을 수 있습니다. 이러한 경우 ASP.NET은 쿠키 없는 폼 인증 티켓을 사용할 수 있습니다. 이 모드에서 인증 티켓은 URL로 인코딩됩니다. 다음 자습서에서 쿠키 없는 인증 티켓이 사용 되는 경우와 이러한 티켓이 만들어지고 관리 되는 방식을 살펴보겠습니다.

### <a name="the-scope-of-forms-authentication"></a>폼 인증의 범위

`FormsAuthenticationModule`는 ASP.NET 런타임의 일부인 관리 코드입니다. Microsoft의 [인터넷 정보 서비스 (iis)](https://www.iis.net/) 웹 서버 버전 7 이전에는 IIS의 HTTP 파이프라인과 ASP.NET 런타임의 파이프라인 사이에 별도의 장애가 있었습니다. 간단히 말해서 IIS 6 및 이전 버전에서 `FormsAuthenticationModule`는 요청이 IIS에서 ASP.NET 런타임으로 위임 된 경우에만 실행 됩니다. 기본적으로 IIS는 HTML 페이지와 CSS 및 이미지 파일과 같은 정적 콘텐츠 자체를 처리 하 고 .aspx, .asmx 또는 .ashx의 확장명이 있는 페이지가 요청 될 때 ASP.NET 런타임에 대 한 요청만 전달 합니다.

그러나 IIS 7에서는 통합 IIS 및 ASP.NET 파이프라인을 사용할 수 있습니다. 몇 가지 구성 설정을 사용 하 여 IIS 7을 설치 하 여 *모든* 요청에 대해 FormsAuthenticationModule를 호출할 수 있습니다. 또한 IIS 7에서는 모든 형식의 파일에 대해 URL 권한 부여 규칙을 정의할 수 있습니다. 자세한 내용은 [IIS6와 Iis7 보안 간의 변경 내용](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [웹 플랫폼 보안](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)및 [IIS7 URL 권한 부여 이해](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization)를 참조 하세요.

긴 스토리는 IIS 7 이전의 버전에서 폼 인증만 사용 하 여 ASP.NET 런타임에 의해 처리 되는 리소스를 보호할 수 있습니다. 마찬가지로 URL 권한 부여 규칙도 ASP.NET 런타임에 의해 처리 되는 리소스에만 적용 됩니다. 그러나 IIS 7에서는 FormsAuthenticationModule 및 UrlAuthorizationModule을 IIS의 HTTP 파이프라인에 통합 하 여이 기능을 모든 요청으로 확장할 수 있습니다.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>1 단계:이 자습서 시리즈에 대 한 ASP.NET 웹 사이트 만들기

가장 광범위 한 대상 그룹에 도달 하기 위해이 시리즈 전체에 구축 될 ASP.NET 웹 사이트는 Microsoft의 무료 버전인 Visual Studio 2008, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)를 사용 하 여 생성 됩니다. [Microsoft SQL Server 2005 Express Edition](https://msdn.microsoft.com/sql/Aa336346.aspx) 데이터베이스에서 `SqlMembershipProvider` 사용자 저장소를 구현 합니다. Visual Studio 2005 또는 Visual Studio 2008 또는 SQL Server의 다른 버전을 사용 하는 경우에는 걱정 하지 마세요. 단계가 거의 동일 하 고 사소한 차이점을 지적 하지 않습니다.

> [!NOTE]
> 각 자습서에서 사용 되는 데모 웹 응용 프로그램은 다운로드로 제공 됩니다. 다운로드 가능한이 응용 프로그램은 .NET Framework 버전 3.5을 대상으로 하는 Visual Web Developer 2008를 사용 하 여 만들어졌습니다. 응용 프로그램은 .NET 3.5를 대상으로 하기 때문에 Web.config 파일에는 3.5 관련 추가 구성 요소가 포함 됩니다. 긴 스토리는 컴퓨터에 .NET 3.5을 설치 해야 하는 경우 먼저 Web.config에서 3.5 관련 태그를 제거 하지 않으면 다운로드할 수 있는 웹 응용 프로그램이 작동 하지 않습니다.

폼 인증을 구성 하기 전에 먼저 ASP.NET 웹 사이트가 필요 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이렇게 하려면 Visual Web Developer를 시작한 다음 파일 메뉴로 이동 하 여 새 웹 사이트를 선택 하 고 새 웹 사이트 대화 상자를 표시 합니다. ASP.NET 웹 사이트 템플릿을 선택 하 고, 위치 드롭다운 목록을 파일 시스템으로 설정 하 고, 웹 사이트를 저장할 폴더를 선택 하 고, 언어를로 C#설정 합니다. Default.aspx ASP.NET 페이지, 앱\_데이터 폴더 및 Web.config 파일을 사용 하 여 새 웹 사이트를 만듭니다.

> [!NOTE]
> Visual Studio는 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트의 두 가지 모드의 프로젝트 관리를 지원 합니다. 웹 사이트 프로젝트는 프로젝트 파일을 포함 하지 않지만, 웹 응용 프로그램 프로젝트는 Visual Studio .NET 2002/2003의 프로젝트 아키텍처를 모방 합니다. 즉, 프로젝트 파일을 포함 하 고 프로젝트의 소스 코드를 단일 어셈블리로 컴파일합니다 .이는 기능 폴더에 배치 됩니다. 웹 응용 프로그램 프로젝트 모델은 서비스 팩 1로 다시 도입 되었지만 Visual Studio 2005는 처음에만 지원 되는 웹 사이트 프로젝트입니다. Visual Studio 2008는 두 프로젝트 모델을 제공 합니다. 그러나 Visual Web Developer 2005 및 2008 버전은 웹 사이트 프로젝트만 지원 합니다. 웹 사이트 프로젝트 모델을 사용 합니다. Express 이외의 버전을 사용 중이 고 [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880%28vs.80%29.aspx) 을 대신 사용 하려는 경우에는 자유롭게 수행할 수 있지만 화면에 표시 되는 내용과 이러한 자습서에서 제공 하는 스크린 샷 및 지침과 함께 수행 해야 하는 단계에 약간의 차이가 있을 수 있습니다.

[새 파일 시스템 기반 웹 사이트 ![만들기](an-overview-of-forms-authentication-cs/_static/image3.png)](an-overview-of-forms-authentication-cs/_static/image2.png)

**그림 2**: 새 파일 시스템 기반 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image4.png))

### <a name="adding-a-master-page"></a>마스터 페이지 추가

그런 다음, 루트 디렉터리의 site. master에 새 마스터 페이지를 추가 합니다. [마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) 를 사용 하면 페이지 개발자가 ASP.NET 페이지에 적용할 수 있는 사이트 전체 템플릿을 정의할 수 있습니다. 마스터 페이지의 주요 혜택은 사이트의 전반적인 모양을 단일 위치에 정의 하 여 사이트의 레이아웃을 쉽게 업데이트 하거나 수정할 수 있다는 것입니다.

[Site .master 라는 마스터 페이지를 웹 사이트에 추가 ![](an-overview-of-forms-authentication-cs/_static/image6.png)](an-overview-of-forms-authentication-cs/_static/image5.png)

**그림 3**: Site.master 라는 마스터 페이지를 웹 사이트에 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image7.png))

마스터 페이지에서 사이트 전체 페이지 레이아웃을 정의 합니다. 디자인 뷰를 사용 하 여 필요한 모든 레이아웃 또는 웹 컨트롤을 추가 하거나 소스 뷰에서 직접 태그를 추가할 수 있습니다. *[ASP.NET 2.0 tutorial 시리즈의 데이터로 작업](../../data-access/index.md)* 하는 데 사용 되는 레이아웃이 모방 되도록 마스터 페이지의 레이아웃을 구성 했습니다 (그림 4 참조). 마스터 페이지는 파일 스타일 (이 자습서의 관련 다운로드에 포함 됨)에 정의 된 css 설정을 사용 하 여 위치를 지정 하 고 스타일을 지정 하기 위해 css [스타일 시트](http://www.w3schools.com/css/default.asp) 를 사용 합니다. 아래 표시 된 태그를 알 수 없는 경우에도 CSS 규칙은 &lt;div&gt;콘텐츠의 위치가 왼쪽에 표시 되 고 너비가 200 픽셀인 고정 너비를 갖도록 정의 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample1.aspx)]

마스터 페이지는 정적 페이지 레이아웃 및 마스터 페이지를 사용 하는 ASP.NET 페이지에서 편집할 수 있는 영역을 모두 정의 합니다. 이러한 콘텐츠 편집 가능한 영역은 `ContentPlaceHolder` 컨트롤로 표시 됩니다 .이 컨트롤은 콘텐츠 &lt;div&gt;내에서 볼 수 있습니다. 마스터 페이지에는 단일 `ContentPlaceHolder` (MainContent)가 있지만 마스터 페이지의 ContentPlaceHolders 표시자는 여러 개 있을 수 있습니다.

위에 입력 된 태그를 사용 하 여 디자인 뷰로 전환 하면 마스터 페이지의 레이아웃이 표시 됩니다. 이 마스터 페이지를 사용 하는 모든 ASP.NET 페이지는 `MainContent` 영역에 대 한 태그를 지정 하는 기능과 함께이 균일 한 레이아웃을 갖게 됩니다.

[디자인 뷰를 통해 볼 때 마스터 페이지 ![](an-overview-of-forms-authentication-cs/_static/image9.png)](an-overview-of-forms-authentication-cs/_static/image8.png)

**그림 4**: 디자인 뷰를 통해 볼 때 마스터 페이지 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image10.png))

### <a name="creating-content-pages"></a>콘텐츠 페이지 만들기

이 시점에서 웹 사이트에 default.aspx 페이지가 있지만 방금 만든 마스터 페이지를 사용 하지 않습니다. 웹 페이지의 선언적 태그를 조작 하 여 마스터 페이지를 사용할 수 있지만 페이지에 콘텐츠가 포함 되어 있지 않으면 페이지를 삭제 하 고 프로젝트에 다시 추가 하 여 사용할 마스터 페이지를 지정 하는 것이 더 쉽습니다. 따라서 프로젝트에서 default.aspx를 삭제 하 여 시작 합니다.

그런 다음 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 Default.aspx 라는 새 Web Form을 추가 하도록 선택 합니다. 이번에는 "마스터 페이지 선택" 확인란을 선택 하 고 목록에서 site.master 마스터 페이지를 선택 합니다.

[새 default.aspx 페이지를 추가 ![마스터 페이지를 선택 하도록 선택](an-overview-of-forms-authentication-cs/_static/image12.png)](an-overview-of-forms-authentication-cs/_static/image11.png)

**그림 5**: 마스터 페이지를 선택 하도록 선택 하는 새 Default.aspx 페이지 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image13.png))

![사이트 마스터 마스터 페이지 사용](an-overview-of-forms-authentication-cs/_static/image14.png)

**그림 6**: Site.master 마스터 페이지 사용

> [!NOTE]
> 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 새 항목 추가 대화 상자에는 "마스터 페이지 선택" 확인란이 포함 되지 않습니다. 대신 "웹 콘텐츠 폼" 형식의 항목을 추가 해야 합니다. "웹 콘텐츠 폼" 옵션을 선택 하 고 추가를 클릭 하면 Visual Studio는 그림 6에 표시 된 것과 동일한 마스터 선택 대화 상자를 표시 합니다.

새 default.aspx 페이지의 선언적 태그에는 마스터 페이지 파일의 경로 및 마스터 페이지의 MainContent ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 지정 하는 @Page 지시문만 포함 되어 있습니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample2.aspx)]

지금은 default.aspx를 비워 둡니다. 이 자습서의 뒷부분에서 콘텐츠를 추가 하는 것으로 돌아갑니다.

> [!NOTE]
> 마스터 페이지에는 메뉴 또는 다른 탐색 인터페이스에 대 한 섹션이 포함 되어 있습니다. 이후 자습서에서 이러한 인터페이스를 만들게 됩니다.

## <a name="step-2-enabling-forms-authentication"></a>2 단계: 폼 인증 사용

ASP.NET 웹 사이트를 만든 후 다음 작업은 폼 인증을 사용 하도록 설정 하는 것입니다. 응용 프로그램의 인증 구성은 Web.config의 [`<authentication>` 요소](https://msdn.microsoft.com/library/532aee0e.aspx) 를 통해 지정 됩니다. `<authentication>` 요소는 응용 프로그램에서 사용 하는 인증 모델을 지정 하는 mode 라는 단일 특성을 포함 합니다. 이 특성에는 다음 네 가지 값 중 하나를 사용할 수 있습니다.

- **Windows** – 이전 자습서에서 설명한 대로 응용 프로그램이 Windows 인증을 사용 하는 경우 방문자를 인증 하는 것은 웹 서버의 책임 이며 일반적으로 기본, 다이제스트 또는 windows 통합 인증을 통해 수행 됩니다.
- **양식**– 사용자가 웹 페이지의 양식을 통해 인증 됩니다.
- **Passport**– 사용자는 Microsoft passport 네트워크를 사용 하 여 인증 됩니다.
- **없음**– 인증 모델이 사용 되지 않습니다. 모든 방문자는 익명입니다.

기본적으로 ASP.NET 응용 프로그램은 Windows 인증을 사용 합니다. 인증 유형을 폼 인증으로 변경 하려면 `<authentication>` 요소의 mode 특성을 Forms로 수정 해야 합니다.

프로젝트에 Web.config 파일이 아직 포함 되어 있지 않은 경우 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 웹 구성 파일을 추가 하 여 지금 프로젝트를 추가 합니다.

[![프로젝트에 Web.config가 아직 포함 되지 않은 경우 지금 추가 합니다.](an-overview-of-forms-authentication-cs/_static/image16.png)](an-overview-of-forms-authentication-cs/_static/image15.png)

**그림 7**: 프로젝트에 Web.config가 아직 포함 되지 않은 경우 지금 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image17.png))

그런 다음 `<authentication>` 요소를 찾아 폼 인증을 사용 하도록 업데이트 합니다. 이렇게 변경 하면 Web.config 파일의 태그가 다음과 같이 표시 됩니다.

[!code-xml[Main](an-overview-of-forms-authentication-cs/samples/sample3.xml)]

> [!NOTE]
> Web.config는 XML 파일 이므로 대/소문자를 구분 하는 것이 중요 합니다. Mode 특성을 대문자 "F"를 사용 하 여 양식으로 설정 해야 합니다. "Forms"와 같은 다른 대/소문자 구분을 사용 하는 경우 브라우저를 통해 사이트를 방문할 때 구성 오류가 표시 됩니다.

`<authentication>` 요소는 폼 인증 관련 설정이 포함 된 `<forms>` 자식 요소를 선택적으로 포함할 수 있습니다. 지금은 기본 폼 인증 설정만 사용 하겠습니다. 다음 자습서에서 `<forms>` 자식 요소에 대해 좀 더 자세히 살펴보겠습니다.

## <a name="step-3-building-the-login-page"></a>3 단계: 로그인 페이지 빌드

폼 인증을 지원 하기 위해 웹 사이트에 로그인 페이지가 필요 합니다. "폼 인증 워크플로 이해" 섹션에서 설명한 대로 `FormsAuthenticationModule`는 사용자가 볼 수 있는 권한이 없는 페이지에 액세스 하려고 시도 하는 경우 사용자를 로그인 페이지로 자동으로 리디렉션합니다. 또한 로그인 페이지에 대 한 링크를 익명 사용자에 게 표시 하는 웹 컨트롤 ASP.NET 있습니다. 이는 "로그인 페이지의 URL은 무엇 인가요?" 라는 질문을 그렇다면.

기본적으로 폼 인증 시스템은 로그인 페이지의 이름을 login.aspx로 지정 하 고 웹 응용 프로그램의 루트 디렉터리에 배치 합니다. 다른 로그인 페이지 URL을 사용 하려면 web.config에 해당 URL을 지정 하면 됩니다. 다음 자습서에서이 작업을 수행 하는 방법을 알아봅니다.

로그인 페이지에는 세 가지 책임이 있습니다.

1. 방문자가 자격 증명을 입력할 수 있도록 허용 하는 인터페이스를 제공 합니다.
2. 제출 된 자격 증명이 유효한 지 확인 합니다.
3. 폼 인증 티켓을 만들어 사용자를 "로그인" 합니다.

### <a name="creating-the-login-pages-user-interface"></a>로그인 페이지의 사용자 인터페이스 만들기

첫 번째 작업을 시작 해 보겠습니다. ASP.NET 라는 사이트의 루트 디렉터리에 새 페이지를 추가 하 고이 페이지를 사이트. 마스터 마스터 페이지에 연결 합니다.

[ASP.NET 라는 새 페이지를 추가 합니다. ![](an-overview-of-forms-authentication-cs/_static/image19.png)](an-overview-of-forms-authentication-cs/_static/image18.png)

**그림 8**: Login.aspx 라는 새 ASP.NET 페이지 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image20.png))

일반적인 로그인 페이지 인터페이스는 두 개의 텍스트 상자, 즉 사용자 이름, 암호 및 양식을 전송 하는 단추 등으로 구성 됩니다. 웹 사이트에는 "me me" 확인란이 포함 되어 있습니다 .이 확인란을 선택 하면 브라우저 다시 시작 전체에서 결과 인증 티켓이 지속 됩니다.

Login.aspx에 두 개의 텍스트 상자를 추가 하 고 해당 `ID` 속성을 각각 사용자 이름 및 암호로 설정 합니다. 또한 암호의 `TextMode` 속성을 Password로 설정 합니다. 다음으로 CheckBox 컨트롤을 추가 하 고 해당 `ID` 속성을 RememberMe로 설정 하 고 `Text` 속성을 "기억을 Me"로 설정 합니다. 그런 다음 `Text` 속성이 "로그인"으로 설정 된 LoginButton 이라는 단추를 추가 합니다. 마지막으로 Label 웹 컨트롤을 추가 하 고 해당 `ID` 속성을 InvalidCredentialsMessage로 설정 하 고, 해당 `Text` 속성을 "사용자 이름 또는 암호가 잘못 되었습니다. 다시 시도 하세요. ", `ForeColor` 속성을 Red로, `Visible` 속성을 False로 설정 하십시오.

이 시점에서 화면은 그림 9의 화면과 유사 하 게 표시 되 고 페이지의 선언적 구문은 다음과 같아야 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample4.aspx)]

[로그인 페이지에는 두 개의 텍스트 상자, 확인란, 단추 및 레이블이 포함 됩니다 ![](an-overview-of-forms-authentication-cs/_static/image22.png)](an-overview-of-forms-authentication-cs/_static/image21.png)

**그림 9**: 로그인 페이지에는 두 개의 텍스트 상자, 확인란, 단추 및 레이블 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image23.png))이 포함 되어 있습니다.

마지막으로 LoginButton의 Click 이벤트에 대 한 이벤트 처리기를 만듭니다. 디자이너에서 단추 컨트롤을 두 번 클릭 하 여이 이벤트 처리기를 만듭니다.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>제공 된 자격 증명이 유효한 지 확인 하는 중

이제 단추의 Click 이벤트 처리기에서 작업 2를 구현 해야 합니다. 제공 된 자격 증명이 유효한 지 여부를 확인 합니다. 이를 위해서는 제공 된 자격 증명이 알려진 자격 증명과 일치 하는지 확인할 수 있도록 모든 사용자 자격 증명을 보유 하는 사용자 저장소가 있어야 합니다.

ASP.NET 2.0 이전에는 개발자가 자체 사용자 저장소를 구현 하 고 코드를 작성 하 여 저장소에 대해 제공 된 자격 증명의 유효성을 검사 했습니다. 대부분의 개발자는 데이터베이스에서 사용자 저장소를 구현 하 여 사용자 이름, 암호, 전자 메일, LastLoginDate 등의 열이 있는 사용자 라는 테이블을 만듭니다. 이 테이블에는 사용자 계정 마다 하나의 레코드가 포함 됩니다. 사용자가 제공한 자격 증명을 확인 하려면 데이터베이스에 일치 하는 사용자 이름을 쿼리하고 데이터베이스의 암호가 제공 된 암호를 속하는지를 확인 해야 합니다.

ASP.NET 2.0를 사용 하는 개발자는 멤버 자격 공급자 중 하나를 사용 하 여 사용자 저장소를 관리 해야 합니다. 이 자습서 시리즈에서는 사용자 저장소에 SQL Server 데이터베이스를 사용 하는 SqlMembershipProvider를 사용 합니다. SqlMembershipProvider를 사용 하는 경우 공급자가 필요로 하는 테이블, 뷰 및 저장 프로시저를 포함 하는 특정 데이터베이스 스키마를 구현 해야 합니다. ***SQL Server의 멤버 자격 스키마 만들기*** 자습서에서이 스키마를 구현 하는 방법을 살펴보겠습니다. 멤버 자격 공급자를 사용 하는 경우 사용자 자격 증명의 유효성을 검사 하는 것은 사용자 *이름* 및 *암호* 조합의 유효성을 나타내는 부울 값을 반환 하는 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx)의 [validateuser (*username*, *password*) 메서드](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)를 호출 하는 것 만큼 간단 합니다. SqlMembershipProvider의 사용자 저장소를 아직 구현 하지 않았으므로 지금은 멤버 자격 클래스의 ValidateUser 메서드를 사용할 수 없습니다.

사용자 지정 사용자 데이터베이스 테이블 (SqlMembershipProvider를 구현한 후에는 사용 되지 않음)을 빌드하는 대신 로그인 페이지 내에서 유효한 자격 증명을 하드 코딩 하겠습니다. LoginButton의 Click 이벤트 처리기에서 다음 코드를 추가 합니다.

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample5.cs)]

여기에서 볼 수 있듯이 세 개의 유효한 사용자 계정 (Scott, Jisun 및 Sam)과 세 가지 모두 동일한 암호 ("암호")가 있습니다. 이 코드는 사용자 및 암호 배열을 반복 하 여 유효한 사용자 이름과 암호를 찾습니다. 사용자 이름과 암호가 모두 유효한 경우 사용자에 게 로그인 한 후 해당 페이지로 리디렉션해야 합니다. 자격 증명이 유효 하지 않은 경우 InvalidCredentialsMessage 레이블을 표시 합니다.

사용자가 유효한 자격 증명을 입력 하면 "적절 한 페이지"로 리디렉션됩니다. 하지만 적절 한 페이지는 무엇 인가요? 사용자가 볼 수 있는 권한이 없는 페이지를 방문 하면 FormsAuthenticationModule가 자동으로 로그인 페이지로 리디렉션됩니다. 이렇게 하면 ReturnUrl 매개 변수를 통해 querystring에 요청 된 URL이 포함 됩니다. 즉, 사용자가 ProtectedPage를 방문 하려고 했 고이 작업을 수행할 수 있는 권한이 없는 경우 FormsAuthenticationModule는 다음으로 리디렉션됩니다.

Login.aspx? ReturnUrl = ProtectedPage

성공적으로 로그인 되 면 사용자는 ProtectedPage로 다시 리디렉션됩니다. 또는 사용자가 자신의 volition의 로그인 페이지를 방문할 수도 있습니다. 이 경우 사용자를 로그인 한 후 루트 폴더의 Default.aspx 페이지로 보내야 합니다.

### <a name="logging-in-the-user"></a>사용자 로그인

제공 된 자격 증명이 유효 하다 고 가정 하면 폼 인증 티켓을 만들어 사용자에 게 사이트에 로그인 해야 합니다. FormsAuthentication [네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 의 [클래스](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) 는 폼 인증 시스템을 통해 사용자를 로그인 및 로그 아웃 하는 다양 한 메서드를 제공 합니다. FormsAuthentication 클래스에는 몇 가지 메서드가 있지만이 분기 시점에 관심이 있는 세 가지는 다음과 같습니다.

- [GetAuthCookie (*username*, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) – 제공 된 이름 *사용자 이름*에 대 한 폼 인증 티켓을 만듭니다. 그런 다음,이 메서드는 인증 티켓의 콘텐츠를 포함 하는 되어 개체를 만들고 반환 합니다. *Persistcookie* 가 true 이면 영구 쿠키가 생성 됩니다.
- [SetAuthCookie (*username*, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) – getauthcookie (*username*, *persistcookie*) 메서드를 호출 하 여 폼 인증 쿠키를 생성 합니다. 그런 다음이 메서드는 GetAuthCookie에서 반환 된 쿠키를 쿠키 컬렉션에 추가 합니다 (쿠키 기반 폼 인증이 사용 되는 경우). 그렇지 않으면이 메서드는 쿠키 없는 티켓 논리를 처리 하는 내부 클래스를 호출 합니다.
- [RedirectFromLoginPage (*username*, *persistcookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) –이 메서드는 setauthcookie (*username*, *persistcookie*)를 호출한 다음 해당 페이지로 사용자를 리디렉션합니다.

GetAuthCookie는 쿠키 컬렉션에 쿠키를 쓰기 전에 인증 티켓을 수정 해야 하는 경우에 유용 합니다. SetAuthCookie는 폼 인증 티켓을 만들고 쿠키 컬렉션에 추가 하지만 사용자를 적절 한 페이지로 리디렉션하지 않으려는 경우에 유용 합니다. 로그인 페이지에 보관 하거나 일부 대체 페이지로 보낼 수 있습니다.

사용자를 로그인 하 여 적절 한 페이지로 리디렉션하도록 했으므로 RedirectFromLoginPage을 사용 하겠습니다. LoginButton의 Click 이벤트 처리기를 업데이트 하 여 주석 처리 된 두 개의 TODO 줄을 다음 코드 줄로 바꿉니다.

RedirectFromLoginPage (FormsAuthentication, RememberMe. Checked);

폼 인증 티켓을 만들 때 폼 인증 티켓 *사용자 이름* 매개 변수에 대 한 사용자 이름 텍스트 상자 텍스트 속성과 *persistcookie* 매개 변수에 대 한 rememberme 확인란의 선택 됨 상태를 사용 합니다.

로그인 페이지를 테스트 하려면 브라우저에서 방문해 보세요. "맞습니다"의 사용자 이름 및 "잘못 된" 암호와 같은 잘못 된 자격 증명을 입력 하 여 시작 합니다. 로그인 단추를 클릭 하면 다시 게시가 발생 하 고 InvalidCredentialsMessage 레이블이 표시 됩니다.

[잘못 된 자격 증명을 입력할 때 InvalidCredentialsMessage 레이블이 표시 ![](an-overview-of-forms-authentication-cs/_static/image25.png)](an-overview-of-forms-authentication-cs/_static/image24.png)

**그림 10**: 잘못 된 자격 증명을 입력할 때 InvalidCredentialsMessage 레이블 표시 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image26.png))

그런 다음 유효한 자격 증명을 입력 하 고 로그인 단추를 클릭 합니다. 이번에는 포스트백이 발생할 때 폼 인증 티켓이 만들어지고 Default.aspx로 다시 자동으로 리디렉션됩니다. 현재 로그인 되어 있음을 나타낼 수 있는 시각적 단서가 없지만이 시점에서 웹 사이트에 로그인 했습니다. 4 단계에서는 사용자가 로그인 했는지 여부를 프로그래밍 방식으로 확인 하는 방법 및 페이지를 방문 하는 사용자를 식별 하는 방법을 알아봅니다.

5 단계에서는 사용자를 웹 사이트에서 로그 아웃 하는 기술을 살펴봅니다.

### <a name="securing-the-login-page"></a>로그인 페이지 보안

사용자가 자격 증명을 입력 하 고 로그인 페이지 양식을 전송 하면 암호를 포함 한 자격 증명은 인터넷을 통해 웹 서버에 *일반 텍스트로*전송 됩니다. 즉, 네트워크 트래픽이 사용자 이름 및 암호를 볼 수 있음을 의미 합니다. 이를 방지 하기 위해서는 [SSL (Secure Socket 레이어)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer)을 사용 하 여 네트워크 트래픽을 암호화 해야 합니다. 이렇게 하면 웹 서버에서 받을 때까지 브라우저를 떠날 때 자격 증명 (전체 페이지의 HTML 태그)이 암호화 됩니다.

웹 사이트에 중요 한 정보가 포함 되어 있지 않으면 로그인 페이지 및 사용자 암호를 일반 텍스트로 전송 하 여 전송 하는 다른 페이지에서 SSL을 사용 해야 합니다. 기본적으로 암호화 되 고 디지털 서명 되어 변조를 방지 하기 때문에 폼 인증 티켓의 보안을 걱정할 필요가 없습니다. 폼 인증 티켓 보안에 대 한 자세한 설명은 다음 자습서에서 제공 됩니다.

> [!NOTE]
> 많은 금융 및 의료 websites는 인증 된 사용자가 액세스할 수 있는 *모든* 페이지에서 SSL을 사용 하도록 구성 됩니다. 이러한 웹 사이트를 빌드하는 경우 폼 인증 티켓이 보안 연결을 통해서만 전송 되도록 폼 인증 시스템을 구성할 수 있습니다. 다음 자습서, *[폼 인증 구성 및 고급 항목](forms-authentication-configuration-and-advanced-topics-cs.md)* 에서 다양 한 폼 인증 구성 옵션을 살펴보겠습니다.

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>4 단계: 인증 된 방문자 검색 및 Id 확인

이 시점에서 폼 인증을 사용 하도록 설정 하 고 기초적인 로그인 페이지를 만들었지만 사용자의 인증 여부를 확인 하는 방법을 아직 확인 하지 않았습니다. 특정 시나리오에서는 인증 된 사용자 또는 익명 사용자가 페이지를 방문 하 고 있는지 여부에 따라 다른 데이터 또는 정보를 표시 하려고 할 수 있습니다. 또한 인증 된 사용자의 id를 알고 있어야 합니다.

기존 default.aspx 페이지를 확대 하 여 이러한 기술을 설명 해 보겠습니다. Default.aspx에서 이름이 AuthenticatedMessagePanel이 고 이름이 AnonymousMessagePanel 인 두 개의 패널 컨트롤을 추가 합니다. 첫 번째 패널에 WelcomeBackMessage 라는 레이블 컨트롤을 추가 합니다. 두 번째 패널에서 HyperLink 컨트롤을 추가 하 고 Text 속성을 "로그인"으로 설정 하 고 해당 NavigateUrl 속성을 "~/Login.aspx"로 설정 합니다. 이 시점에서 default.aspx의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample6.aspx)]

지금까지 짐작할 수 있듯이, 여기서의 아이디어는 인증 된 방문자에 게 AuthenticatedMessagePanel을 표시 하 고 익명 방문자에 게 AnonymousMessagePanel만 표시 하는 것입니다. 이를 수행 하려면 사용자의 로그인 여부에 따라 이러한 패널의 표시 속성을 설정 해야 합니다.

[요청. IsAuthenticated 속성](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) 은 요청이 인증 되었는지 여부를 나타내는 부울 값을 반환 합니다. \_Load 이벤트 처리기 코드 페이지에 다음 코드를 입력 합니다.

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample7.cs)]

이 코드가 준비 되 면 브라우저를 통해 default.aspx를 방문 합니다. 아직 로그인 하지 않은 경우 로그인 페이지에 대 한 링크가 표시 됩니다 (그림 11 참조). 이 링크를 클릭 하 고 사이트에 로그인 합니다. 3 단계에서 확인 한 것 처럼 자격 증명을 입력 한 후에는 default.aspx로 돌아갑니다. 하지만 이번에는 페이지에 "환영 합니다."가 표시 됩니다. 메시지 (그림 12 참조).

![익명으로 방문할 때 로그인 링크가 표시 됩니다.](an-overview-of-forms-authentication-cs/_static/image27.png)

**그림 11**: 익명으로 방문할 때 로그인 링크가 표시 됩니다.

![인증 된 사용자에 게 표시 됩니다.](an-overview-of-forms-authentication-cs/_static/image28.png)

**그림 12**: 인증 된 사용자에 게는 "환영 합니다."가 표시 됩니다. 메시지

현재 로그온 한 사용자의 id를 [HttpContext 개체](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)의 [user 속성](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx)을 통해 확인할 수 있습니다. HttpContext 개체는 현재 요청에 대 한 정보를 나타내며, 응답, 요청 및 세션과 같은 일반적인 ASP.NET 개체의 홈입니다. User 속성은 현재 HTTP 요청의 보안 컨텍스트를 나타내며 [IPrincipal 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx)를 구현 합니다.

사용자 속성은 FormsAuthenticationModule에 의해 설정 됩니다. 특히 FormsAuthenticationModule가 들어오는 요청에서 폼 인증 티켓을 찾으면 새 GenericPrincipal 개체를 만들어 사용자 속성에 할당 합니다.

보안 주체 개체 (예: GenericPrincipal)는 사용자의 id와 해당 id가 속한 역할에 대 한 정보를 제공 합니다. IPrincipal 인터페이스는 두 개의 구성원을 정의 합니다.

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) – 보안 주체가 지정 된 역할에 속하는지 여부를 나타내는 부울 값을 반환 하는 메서드입니다.
- [Id](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) – [IIdentity 인터페이스](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx)를 구현 하는 개체를 반환 하는 속성입니다. IIdentity 인터페이스는 [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [Isauthenticated](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)및 [Name](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx)의 세 가지 속성을 정의 합니다.

다음 코드를 사용 하 여 현재 방문자의 이름을 확인할 수 있습니다.

문자열 Currentusers Name = User.Identity.Name;

폼 인증을 사용 하는 경우 GenericPrincipal의 Identity 속성에 대해 [FormsIdentity 개체가](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) 생성 됩니다. FormsIdentity 클래스는 항상 AuthenticationType 속성에 대해 "Forms" 문자열을 반환 하 고 IsAuthenticated 속성에 대해 true를 반환 합니다. Name 속성은 폼 인증 티켓을 만들 때 지정 된 사용자 이름을 반환 합니다. FormsIdentity는 이러한 세 가지 속성 외에도 [티켓 속성](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx)을 통해 기본 인증 티켓에 대 한 액세스를 포함 합니다. 티켓 속성은 [양식 Authenticationticket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)형식의 개체를 반환 합니다. 여기에는 만료, Ispersistent, IssueDate, Name 등의 속성이 있습니다.

여기에서 중요 한 점은 FormsAuthentication (*username*, *Persistcookie*), FormsAuthentication. setauthcookie (*username*, *persistcookie*) 및 FormsAuthentication (*username*, *persistcookie*) 메서드에 지정 된 *username* 매개 변수가 User.Identity.Name에서 반환 하는 값과 동일 하다는 것입니다. 또한 이러한 메서드에서 만든 인증 티켓은 FormsIdentity 개체로 캐스팅 한 후 티켓 속성에 액세스 하 여 사용할 수 있습니다.

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample8.cs)]

Default.aspx에서 더 많은 개인 설정 된 메시지를 제공 하겠습니다. WelcomeBackMessage 레이블의 Text 속성에 "환영 뒤로, *username*!" 문자열이 할당 되도록 페이지\_Load 이벤트 처리기를 업데이트 합니다.

WelcomeBackMessage = "환영", + User.Identity.Name + "!";

그림 13에서는 사용자의 Scott로 로그인 할 때 이러한 수정의 영향을 보여 줍니다.

![환영 메시지에는 현재 로그인 한 사용자의 이름이 포함 됩니다.](an-overview-of-forms-authentication-cs/_static/image29.png)

**그림 13**: 환영 메시지에는 현재 로그인 한 사용자의 이름이 포함 됩니다.

### <a name="using-the-loginview-and-loginname-controls"></a>LoginView 및 LoginName 컨트롤 사용

서로 다른 콘텐츠를 인증 된 사용자로 표시 하는 것이 일반적인 요구 사항입니다. 현재 로그온 한 사용자의 이름을 표시 합니다. 이러한 이유로 ASP.NET에는 그림 13에 표시 된 것과 동일한 기능을 제공 하지만 한 줄의 코드를 작성할 필요 없이 두 개의 웹 컨트롤이 포함 되어 있습니다.

[LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 은 인증 된 사용자와 익명 사용자에 게 서로 다른 데이터를 쉽게 표시할 수 있게 해 주는 템플릿 기반 웹 컨트롤입니다. LoginView에는 미리 정의 된 두 개의 템플릿이 포함 되어 있습니다.

- AnonymousTemplate –이 템플릿에 추가 된 태그는 익명 방문자 에게만 표시 됩니다.
- LoggedInTemplate –이 템플릿의 태그는 인증 된 사용자 에게만 표시 됩니다.

사이트의 마스터 페이지인 site.master에 LoginView 컨트롤을 추가 해 보겠습니다. 그러나 LoginView 컨트롤을 추가 하는 대신 새 ContentPlaceHolder 컨트롤을 추가 하 고이 새 ContentPlaceHolder에 LoginView 컨트롤을 추가 해 보겠습니다. 이 결정에 대 한 근거는 곧 파악 될 것입니다.

> [!NOTE]
> AnonymousTemplate 및 LoggedInTemplate 외에도 LoginView 컨트롤에는 역할별 템플릿이 포함 될 수 있습니다. 역할 관련 템플릿은 지정 된 역할에 속하는 사용자 에게만 태그를 표시 합니다. 이후 자습서에서 LoginView 컨트롤의 역할 기반 기능을 살펴보겠습니다.

LoginContent 라는 ContentPlaceHolder를 탐색 &lt;div&gt; 요소 내의 마스터 페이지에 추가 하 여 시작 합니다. 단순히 도구 상자에서 소스 뷰로 ContentPlaceHolder 컨트롤을 끌어와 "TODO: Menu to here ..." 바로 위에 결과 태그를 배치할 수 있습니다. 본문.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample9.aspx)]

다음으로, LoginContent ContentPlaceHolder 내에 LoginView 컨트롤을 추가 합니다. 마스터 페이지의 ContentPlaceHolder 컨트롤에 배치 된 콘텐츠는 ContentPlaceHolder에 대 한 *기본 콘텐츠로* 간주 됩니다. 즉,이 마스터 페이지를 사용 하는 ASP.NET 페이지는 각 ContentPlaceHolder에 대 한 고유한 콘텐츠를 지정 하거나 마스터 페이지의 기본 콘텐츠를 사용할 수 있습니다.

LoginView 및 기타 로그인 관련 컨트롤은 도구 상자의 로그인 탭에 있습니다.

![도구 상자의 LoginView 컨트롤](an-overview-of-forms-authentication-cs/_static/image30.png)

**그림 14**: 도구 상자의 LoginView 컨트롤

다음으로 LoginView 컨트롤 바로 뒤에 두 개의 &lt;br/&gt; 요소를 추가 하지만 여전히 ContentPlaceHolder 내에 있습니다. 이 시점에서 탐색 &lt;div&gt; 요소의 태그는 다음과 같습니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample10.aspx)]

LoginView의 템플릿은 디자이너 또는 선언적 태그에서 정의할 수 있습니다. Visual Studio의 디자이너에서 LoginView의 스마트 태그를 확장 합니다 .이 태그는 드롭다운 목록에서 구성 된 템플릿을 나열 합니다. AnonymousTemplate에 "Hello, 낯선" 텍스트를 입력 합니다. 그런 다음 하이퍼링크 컨트롤을 추가 하 고 Text 및 NavigateUrl 속성을 각각 "로그인" 및 "~/Login.aspx"로 설정 합니다.

AnonymousTemplate을 구성한 후 LoggedInTemplate로 전환 하 고 "환영 back" 텍스트를 입력 합니다. 그런 다음 도구 상자의 LoginName 컨트롤을 LoggedInTemplate로 끌어 "환영 뒤로" 텍스트 바로 뒤에 배치 합니다. 이름을 암시 하는 [LoginName 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx)은 현재 로그인 한 사용자의 이름을 표시 합니다. 내부적으로 LoginName 컨트롤은 단순히 User.Identity.Name 속성을 출력 합니다.

LoginView의 템플릿 추가 후 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample11.aspx)]

사이트. 마스터 마스터 페이지를 추가 하면 사용자가 인증 되었는지 여부에 따라 웹 사이트의 각 페이지에 다른 메시지가 표시 됩니다. 그림 15에서는 사용자 Jisun을 통해 브라우저를 통해 방문할 때 default.aspx 페이지를 보여 줍니다. "환영, Jisun" 메시지는 왼쪽에 있는 마스터 페이지의 탐색 섹션 (방금 추가한 LoginView 컨트롤을 통해) 및 Default.aspx의 콘텐츠 영역 (Panel 컨트롤 및 프로그래밍 논리를 통해)에서 한 번 반복 됩니다.

![LoginView 컨트롤 표시](an-overview-of-forms-authentication-cs/_static/image31.png)

**그림 15**: LoginView 컨트롤은 "환영 뒤로, Jisun"를 표시 합니다.

마스터 페이지에 LoginView를 추가 했으므로 사이트의 모든 페이지에 표시 될 수 있습니다. 그러나이 메시지를 표시 하지 않으려는 웹 페이지가 있을 수 있습니다. 로그인 페이지에 대 한 링크가 없는 것 처럼 보일 수 있으므로 이러한 페이지 중 하나는 로그인 페이지입니다. LoginView 컨트롤을 마스터 페이지의 ContentPlaceHolder에 배치 했으므로 콘텐츠 페이지에서이 기본 태그를 재정의할 수 있습니다. Login.aspx를 열고 디자이너로 이동 합니다. 마스터 페이지에서 LoginContent ContentPlaceHolder에 대 한 Login .aspx의 콘텐츠 컨트롤을 명시적으로 정의 하지 않았으므로 로그인 페이지에이 ContentPlaceHolder에 대 한 마스터 페이지의 기본 태그가 표시 됩니다. 디자이너를 통해이를 확인할 수 있습니다. LoginContent ContentPlaceHolder는 기본 태그 (LoginView 컨트롤)를 표시 합니다.

[로그인 페이지 ![마스터 페이지의 LoginContent ContentPlaceHolder에 대 한 기본 콘텐츠를 표시 합니다.](an-overview-of-forms-authentication-cs/_static/image33.png)](an-overview-of-forms-authentication-cs/_static/image32.png)

**그림 16**: 로그인 페이지에 마스터 페이지의 LoginContent ContentPlaceHolder에 대 한 기본 내용이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image34.png)).

LoginContent ContentPlaceHolder에 대 한 기본 태그를 재정의 하려면 디자이너에서 해당 영역을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 사용자 지정 콘텐츠 만들기 옵션을 선택 하면 됩니다. Visual Studio 2008을 사용 하는 경우 ContentPlaceHolder에는 스마트 태그가 포함 되어 있으며이 태그가 선택 되 면 동일한 옵션을 제공 합니다. 그러면 페이지의 태그에 새 콘텐츠 컨트롤이 추가 되므로이 페이지에 대 한 사용자 지정 콘텐츠를 정의할 수 있습니다. 여기에서 사용자 지정 메시지를 추가할 수 있습니다 (예: "로그인 ..."). 단,이 메시지는 비워 둡니다.

> [!NOTE]
> Visual Studio 2005에서 사용자 지정 콘텐츠를 만들면 ASP.NET 페이지에 빈 콘텐츠 컨트롤이 생성 됩니다. 그러나 Visual Studio 2008에서 사용자 지정 콘텐츠를 만들면 마스터 페이지의 기본 콘텐츠가 새로 생성 된 콘텐츠 컨트롤에 복사 됩니다. Visual Studio 2008을 사용 하는 경우 새 콘텐츠 컨트롤을 만든 후 마스터 페이지에서 복사 된 콘텐츠를 지워야 합니다.

그림 17은 이러한 변경을 수행한 후 브라우저에서 방문할 때의 login.aspx 페이지를 보여 줍니다. Default.aspx를 방문할 때 처럼 왼쪽 탐색 &lt;div&gt;에는 "Hello, 낯선" 또는 "환영 뒤로, *사용자 이름*" 메시지가 없습니다.

[로그인 페이지 ![기본 LoginContent ContentPlaceHolder의 태그를 숨깁니다.](an-overview-of-forms-authentication-cs/_static/image36.png)](an-overview-of-forms-authentication-cs/_static/image35.png)

**그림 17**: 로그인 페이지에서 기본 LoginContent ContentPlaceHolder의 태그를 숨깁니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image37.png)).

## <a name="step-5-logging-out"></a>5 단계: 로그 아웃

3 단계에서는 사용자를 사이트에 로그인 하기 위한 로그인 페이지를 작성 하는 방법을 알아보았습니다. 하지만 사용자를 로그 아웃 하는 방법을 아직 확인 하지 않았습니다. 사용자를 로그인 하는 데 사용 되는 메서드 외에도 FormsAuthentication 클래스는 [SignOut 메서드](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx)를 제공 합니다. SignOut 메서드는 단순히 폼 인증 티켓을 제거 하 여 사용자를 사이트에서 로그 아웃 합니다.

로그 아웃 링크를 제공 하는 것은 ASP.NET에서 사용자를 로그 아웃 하도록 특별히 디자인 된 컨트롤을 포함 하는 일반적인 기능입니다. [LoginStatus 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) 은 사용자의 인증 상태에 따라 "Login" LinkButton 또는 "Logout" LinkButton를 표시 합니다. "로그인" LinkButton는 익명 사용자에 대해 렌더링 되는 반면, 인증 된 사용자에 게는 "로그 아웃" LinkButton 표시 됩니다. "로그인" 및 "로그 아웃" Linkbutton 텍스트는 LoginStatus의 LoginText 및 Logintext 속성을 통해 구성할 수 있습니다.

"Login" LinkButton를 클릭 하면 다시 게시가 발생 하며,이는 로그인 페이지에 리디렉션이 실행 되는 것입니다. "Logout" LinkButton을 클릭 하면 LoginStatus 컨트롤이 FormsAuthentication 메서드를 호출한 다음 사용자를 페이지로 리디렉션합니다. 로그 오프 한 사용자는 LogoutAction 속성에 따라 다음과 같은 세 가지 값 중 하나에 할당 될 수 있는 페이지를 리디렉션할 수 있습니다.

- 새로 고침 – 기본값 사용자를 단지 방문한 페이지로 리디렉션합니다. 방문한 페이지가 익명 사용자를 허용 하지 않는 경우 FormsAuthenticationModule는 자동으로 사용자를 로그인 페이지로 리디렉션합니다.

여기서 리디렉션이 수행 되는 이유에 대해 궁금한 점이 있을 수 있습니다. 사용자가 동일한 페이지에 유지 하려는 경우 명시적 리디렉션이 필요한 이유는 무엇 인가요? 그 이유는 "로그 오프" LinkButton 클릭 하면 사용자에 게 쿠키 컬렉션에 폼 인증 티켓이 남아 있기 때문입니다. 따라서 다시 게시 요청은 인증 된 요청입니다. LoginStatus 컨트롤은 SignOut 메서드를 호출 하지만 FormsAuthenticationModule가 사용자를 인증 한 후에 발생 합니다. 따라서 명시적 리디렉션으로 인해 브라우저가 페이지를 다시 요청 합니다. 브라우저에서 페이지를 다시 요청 하는 시점에 폼 인증 티켓이 제거 되었으므로 들어오는 요청은 익명입니다.

- 리디렉션-사용자가 LoginStatus의 LogoutPageUrl 속성에 지정 된 URL로 리디렉션됩니다.
- RedirectToLoginPage – 사용자가 로그인 페이지로 리디렉션됩니다.

마스터 페이지에 LoginStatus 컨트롤을 추가 하 고 리디렉션 옵션을 사용 하도록 구성 하 여 로그 아웃 되었음을 확인 하는 메시지를 표시 하는 페이지로 사용자를 보냅니다. 먼저 Logout 이라는 루트 디렉터리에 페이지를 만듭니다. 이 페이지를 사이트 마스터 페이지와 연결 하는 것을 잊지 마세요. 다음으로, 로그 아웃 되었음을 사용자에 게 설명 하는 메시지를 페이지 태그에 입력 합니다.

그런 다음, Site. 마스터 마스터 페이지로 돌아가서 LoginContent ContentPlaceHolder의 LoginView 아래에 LoginStatus 컨트롤을 추가 합니다. LoginStatus 컨트롤의 LogoutAction 속성을 Redirect로 설정 하 고 LogoutPageUrl 속성을 "~/Logout.aspx"로 설정 합니다.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample12.aspx)]

LoginStatus는 LoginView 컨트롤 외부에 있기 때문에 익명 및 인증 된 사용자 모두에 게 표시 되지만 LoginStatus가 "Login" 또는 "Logout" LinkButton를 올바르게 표시 하기 때문에이는 정상입니다. LoginStatus 컨트롤을 추가 하면 AnonymousTemplate의 "로그인" 하이퍼링크가 불필요 하므로 제거 합니다.

그림 18은 Jisun을 취소 한 경우 default.aspx를 보여 줍니다. 왼쪽 열에는 로그 아웃 링크와 함께 "환영 back, Jisun" 메시지가 표시 됩니다. 로그 아웃 LinkButton을 클릭 하면 포스트백이 발생 하 고 시스템에서 Jisun이 취소 된 다음,이를 Logout으로 리디렉션합니다. 그림 19에 나와 있는 것 처럼 Jisun이 이미 로그 아웃 되었으며 익명으로 인 한 것입니다. 따라서 왼쪽 열에는 "환영 합니다." 라는 텍스트와 로그인 페이지에 대 한 링크가 표시 됩니다.

[default.aspx에 표시 되는 ![](an-overview-of-forms-authentication-cs/_static/image39.png)](an-overview-of-forms-authentication-cs/_static/image38.png)

**그림 18**: default.aspx는 "LinkButton" ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image40.png))와 함께 "시작, Jisun"을 표시 합니다.

[![로그 아웃 .aspx 표시](an-overview-of-forms-authentication-cs/_static/image42.png)](an-overview-of-forms-authentication-cs/_static/image41.png)

**그림 19**: LinkButton는 "로그인" ([전체 크기 이미지를 보려면 클릭](an-overview-of-forms-authentication-cs/_static/image43.png))과 함께 "환영 합니다."를 표시 합니다.

> [!NOTE]
> 마스터 페이지의 LoginContent ContentPlaceHolder (예: 4 단계에서 login.aspx에 대해 했던 것 처럼)를 숨기도록 Logout 페이지를 사용자 지정 하는 것이 좋습니다. 그 이유는 LoginStatus 컨트롤에 의해 렌더링 된 "로그인" LinkButton ("Hello," 아래에 있는)가 사용자를 ReturnUrl querystring 매개 변수에 현재 URL을 전달 하는 로그인 페이지로 보내는 이유입니다. 즉, 로그 아웃 한 사용자가이 LoginStatus의 "Login" LinkButton를 클릭 한 다음 로그인 하면 사용자를 쉽게 혼동할 수 있도록 하는 Logout으로 다시 리디렉션됩니다.

## <a name="summary"></a>요약

이 자습서에서는 폼 인증 워크플로를 검사 한 다음 ASP.NET 응용 프로그램에서 폼 인증을 구현 하도록 시작 했습니다. 폼 인증은 양식 인증 티켓을 기반으로 사용자를 식별 하 고 권한 없는 사용자를 로그인 페이지로 리디렉션하는 두 가지 책임이 있는 FormsAuthenticationModule에서 제공 합니다.

.NET Framework의 FormsAuthentication 클래스에는 폼 인증 티켓을 만들고, 검사 하 고, 제거 하는 메서드가 포함 되어 있습니다. IsAuthenticated 속성 및 User 개체는 요청이 인증 되었는지 여부를 확인 하는 추가 프로그래밍 기능을 제공 하 고 사용자 id에 대 한 정보를 제공 합니다. LoginView, LoginStatus 및 LoginName 웹 컨트롤도 있습니다 .이 컨트롤을 사용 하 여 개발자는 많은 일반적인 로그인 관련 작업을 빠르게 수행할 수 있습니다. 이러한 및 기타 로그인 관련 웹 컨트롤은 이후 자습서에서 더 자세히 살펴보겠습니다.

이 자습서에서는 폼 인증에 대 한 간단한 개요를 제공 했습니다. 다양 한 구성 옵션을 검토 하거나, 쿠키 없는 폼 인증 티켓이 작동 하는 방식을 확인 하거나, ASP.NET에서 폼 인증 티켓의 콘텐츠를 보호 하는 방법을 살펴보세요. [다음 자습서](forms-authentication-configuration-and-advanced-topics-cs.md)에서는 이러한 항목과 기타 항목에 대해 설명 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [IIS6와 IIS7 보안 간의 변경 내용](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Login ASP.NET 컨트롤](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [전문 ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [`<authentication>` 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [`<authentication>`에 대 한 `<forms>` 요소](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 학습

- [ASP.NET에서 기본 폼 인증 사용](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는이 자습서 시리즈를 많은 유용한 검토자가 검토 했습니다. 이 자습서의 선임 검토자는 Alicja Maziarz, John Suru 및 Teresa Murphy를 포함 합니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](security-basics-and-asp-net-support-cs.md)
> [다음](forms-authentication-configuration-and-advanced-topics-cs.md)
