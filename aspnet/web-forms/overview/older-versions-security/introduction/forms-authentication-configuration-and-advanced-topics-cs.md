---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
title: 폼 인증 구성 및 고급 항목 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 다양 한 폼 인증 설정을 살펴보고 forms 요소를 통해 수정 하는 방법에 대해 알아봅니다. 자세한 내용은 다음을 설명 합니다.
ms.author: riande
ms.date: 01/14/2008
ms.assetid: b9c29865-a34e-48bb-92c0-c443a72cb860
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
msc.type: authoredcontent
ms.openlocfilehash: b296f31da1c73df97175d94402b4d618df425d8d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74579217"
---
# <a name="forms-authentication-configuration-and-advanced-topics-c"></a>폼 인증 구성 및 고급 항목(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_cs.pdf)

> 이 자습서에서는 다양 한 폼 인증 설정을 살펴보고 forms 요소를 통해 수정 하는 방법에 대해 알아봅니다. 이렇게 하려면 폼 인증 티켓의 시간 제한 값을 사용자 지정 하 고, 사용자 지정 URL (login.aspx 대신 login.aspx) 및 쿠키 없는 폼 인증 티켓이 포함 된 로그인 페이지를 사용 하는 방법을 자세히 살펴봅니다.

## <a name="introduction"></a>소개

[이전 자습서](an-overview-of-forms-authentication-cs.md) 에서는 ASP.NET 응용 프로그램에서 폼 인증을 구현 하는 데 필요한 단계에 대해 살펴보았습니다. web.config의 구성 설정을 지정 하 여 인증 된 사용자와 익명 사용자에 대해 서로 다른 콘텐츠를 표시 하는 로그인 페이지를 만듭니다. &lt;인증&gt; 요소의 mode 특성을 양식으로 설정 하 여 폼 인증을 사용 하도록 웹 사이트를 구성 했습니다. &lt;authentication&gt; 요소에는 선택적으로 폼 인증 설정의 분류를 지정할 수 있는 &lt;forms&gt; 자식 요소가 포함 될 수 있습니다.

이 자습서에서는 다양 한 폼 인증 설정을 검토 하 고 &lt;forms&gt; 요소를 통해 수정 하는 방법을 알아봅니다. 이렇게 하려면 폼 인증 티켓의 시간 제한 값을 사용자 지정 하 고, 사용자 지정 URL (login.aspx 대신 login.aspx) 및 쿠키 없는 폼 인증 티켓이 포함 된 로그인 페이지를 사용 하는 방법을 자세히 살펴봅니다. 또한 폼 인증 티켓의 구성을을 자세히 검토 하 고 ASP.NET에서 티켓의 데이터가 검사 및 변조 로부터 보호 되는지 확인 하는 데 필요한 예방 조치를 확인 합니다. 마지막으로, 폼 인증 티켓에 추가 사용자 데이터를 저장 하는 방법 및 사용자 지정 보안 주체 개체를 통해이 데이터를 모델링 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>1 단계: &lt;forms&gt; 구성 설정 검사

ASP.NET의 폼 인증 시스템은 응용 프로그램 별로 사용자 지정할 수 있는 다양 한 구성 설정을 제공 합니다. 여기에는 폼 인증 티켓의 수명과 같은 설정이 포함 됩니다. 티켓에 적용 되는 보호 종류는 무엇 인가요? 쿠키 없는 인증 티켓이 사용 되는 조건 로그인 페이지의 경로입니다. 및 기타 정보 기본값을 수정 하려면 [&lt;forms&gt; 요소](https://msdn.microsoft.com/library/1d3t3c61.aspx) 를 [&lt;인증&gt; 요소의](https://msdn.microsoft.com/library/532aee0e.aspx)자식으로 추가 하 여 다음과 같이 XML 특성으로 사용자 지정 하려는 속성 값을 지정 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample1.xml)]

표 1에는 &lt;forms&gt; 요소를 통해 사용자 지정할 수 있는 속성이 요약 되어 있습니다. Web.config는 XML 파일 이므로 왼쪽 열에 있는 특성 이름은 대/소문자를 구분 합니다.

| <strong>특성</strong> |                                                                                                                                                                                                                                     <strong>설명</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         쿠키         |                                                                                                                이 특성은 인증 티켓이 쿠키에 저장 되 고 URL에 포함 되는 조건을 지정 합니다. 허용 되는 값은 다음과 같습니다. UseCookies; UseUri; 자동 검색 및 UseDeviceProfile (기본값). 2 단계에서는이 설정을 자세히 검토 합니다.                                                                                                                |
|         defaultUrl         |                                                                                                                                                         Querystring에 지정 된 RedirectUrl 값이 없는 경우 로그인 페이지에서 로그인 한 후 사용자가 리디렉션되는 URL을 나타냅니다. 기본값은 default.aspx입니다.                                                                                                                                                         |
|           도메인           | 쿠키 기반 인증 티켓을 사용 하는 경우이 설정은 쿠키의 도메인 값을 지정 합니다. 기본값은 빈 문자열입니다 .이 문자열을 사용 하면 브라우저가 발급 된 도메인 (예: www.yourdomain.com)을 사용 합니다. 이 경우 admin.yourdomain.com와 같은 하위 도메인에 대 한 요청을 만들 때 쿠키가 전송 <strong>되지</strong> 않습니다. 모든 하위 도메인에 쿠키를 전달 하려면 도메인 특성을 yourdomain.com로 설정 하 여 사용자 지정 해야 합니다. |
|  enableCrossAppRedirects   |                                                                                                                                                                   동일한 서버에 있는 다른 웹 응용 프로그램의 Url로 리디렉션되는 경우 인증 된 사용자가 저장 되는지 여부를 나타내는 부울 값입니다. 기본값은 false입니다.                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      로그인 페이지의 URL입니다. 기본값은 login.aspx입니다.                                                                                                                                                                                                                      |
|            name            |                                                                                                                                                                                                   쿠키 기반 인증 티켓을 사용 하는 경우 쿠키의 이름입니다. 기본값은입니다. .ASPXAUTH.                                                                                                                                                                                                   |
|            경로            |                                                                             쿠키 기반 인증 티켓을 사용 하는 경우이 설정은 쿠키의 경로 특성을 지정 합니다. 개발자는 path 특성을 사용 하 여 쿠키 범위를 특정 디렉터리 계층으로 제한할 수 있습니다. 기본값은/입니다 .이 값은 브라우저에서 도메인에 대 한 모든 요청에 인증 티켓 쿠키를 보내도록 알려 줍니다.                                                                              |
|         보호         |                                                                                                                                            폼 인증 티켓을 보호 하는 데 사용 되는 기술을 나타냅니다. 허용 되는 값은 모두 (기본값)입니다. 암호화 없음을 및 유효성 검사. 이러한 설정은 3 단계에서 자세히 설명 합니다.                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                인증 쿠키를 전송 하는 데 SSL 연결이 필요한 지 여부를 나타내는 부울 값입니다. 기본값은 false입니다.                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 단일 세션 중에 사용자가 사이트를 방문할 때마다 인증 쿠키의 시간 제한이 다시 설정 되는지 여부를 나타내는 부울 값입니다. 기본값은 true입니다. 인증 티켓 시간 제한 정책은 티켓의 시간 제한 값 지정 섹션에 자세히 설명 되어 있습니다.                                                                                                 |
|          시간 제한           |                                                                                                                               인증 티켓 쿠키가 만료 되는 시간 (분)을 지정 합니다. 기본값은 30입니다. 인증 티켓 시간 제한 정책은 티켓의 시간 제한 값 지정 섹션에 자세히 설명 되어 있습니다.                                                                                                                               |

**표 1**: &lt;폼&gt; 요소의 특성에 대 한 요약

ASP.NET 2.0 이상에서 기본 폼 인증 값은 .NET Framework의 forms Authenticationconfiguration 클래스에 하드 코딩 됩니다. 모든 수정 사항은 web.config 파일의 응용 프로그램 별로 적용 해야 합니다. 이는 기본 폼 인증 값이 machine.config 파일에 저장 된 ASP.NET와 다르므로 machine.config를 통해 수정할 수 있습니다. ASP.NET 1.x의 항목에서 많은 폼 인증 시스템 설정의 기본값은 ASP.NET 2.0에서 ASP.NET 1.x의 경우 보다 그 이상 차이가 있다는 것을 언급 하는 것이 좋습니다. ASP.NET 1.x 환경에서 응용 프로그램을 마이그레이션하는 경우 이러한 차이를 파악 하는 것이 중요 합니다. 차이점 목록은 [&lt;forms&gt; 요소 기술 설명서](https://msdn.microsoft.com/library/1d3t3c61.aspx) 를 참조 하세요.

> [!NOTE]
> 시간 제한, 도메인, 경로 등의 여러 폼 인증 설정에서 결과 폼 인증 티켓 쿠키에 대 한 세부 정보를 지정 합니다. 쿠키, 작동 방법 및 다양 한 속성에 대 한 자세한 내용은 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)를 참조 하세요.

### <a name="specifying-the-tickets-timeout-value"></a>티켓의 시간 제한 값 지정

폼 인증 티켓은 id를 나타내는 토큰입니다. 쿠키 기반 인증 티켓을 사용 하면이 토큰은 쿠키 형식으로 유지 되 고 각 요청에서 웹 서버로 전송 됩니다. 기본적으로 토큰을 소유 하는 것은 사용자 *이름*으로, 사용자가 이미 로그인 한 상태이 고, 사용자의 id가 페이지 방문 간에 기억 될 수 있도록 사용 됩니다.

폼 인증 티켓에는 사용자의 id 뿐만 아니라 토큰의 무결성 및 보안을 보장 하는 데 도움이 되는 정보도 포함 되어 있습니다. 그 후에는 부정한 사용자가 위조 토큰을 만들거나 일부의 legit 토큰을 수정할 수 없도록 합니다.

티켓에 포함 된 이러한 정보 중 하나는 티켓이 더 이상 유효 하지 않은 날짜와 시간인 *만료*입니다. FormsAuthenticationModule는 인증 티켓을 확인할 때마다 티켓의 만료가 아직 통과 되지 않았는지 확인 합니다. 있는 경우 티켓을 무시 하 고 사용자를 익명으로 식별 합니다. 이러한 보호는 재생 공격 으로부터 보호 합니다. 만료 없이 해커가 자신의 컴퓨터에 물리적으로 액세스 하 고 쿠키를 통해 루 팅 하 여 사용자의 유효한 인증 티켓을 얻을 수 있는 경우,이 도난 인증 티켓을 사용 하 여 서버에 요청을 보낼 수 있습니다. 항목을 얻으세요. 만료는이 시나리오를 방해 하지 않지만 이러한 공격이 성공할 수 있는 기간을 제한 합니다.

> [!NOTE]
> 3 단계 인증 티켓을 보호 하기 위해 폼 인증 시스템에서 사용 하는 추가 기술에 대해 자세히 설명 합니다.

인증 티켓을 만들 때 폼 인증 시스템은 시간 제한 설정을 확인 하 여 만료를 확인 합니다. 표 1에 나와 있는 것 처럼 시간 제한 설정은 기본적으로 30 분으로 설정 됩니다. 즉, 폼 인증 티켓이 생성 될 때 만료 날짜 및 시간을 30 분으로 설정 합니다.

만료는 폼 인증 티켓이 만료 될 때 이후의 절대 시간을 정의 합니다. 그러나 일반적으로 개발자는 슬라이딩 만료를 구현 하려고 합니다. 하나는 사용자가 사이트를 다시 검토 때마다 다시 설정 됩니다. 이 동작은 slidingExpiration 설정에 따라 결정 됩니다. True (기본값)로 설정 된 경우 FormsAuthenticationModule가 사용자를 인증할 때마다 티켓 만료를 업데이트 합니다. False로 설정 된 경우 각 요청에서 만료가 업데이트 되지 않으므로 티켓이 처음 생성 된 시간 (분)을 기준으로 티켓이 만료 됩니다.

> [!NOTE]
> 인증 티켓에 저장 되는 만료 날짜 및 시간 값 (예: 8 월 2 일 11:34 오전 2008)입니다. 또한 날짜와 시간은 웹 서버의 현지 시간을 기준으로 합니다. 이러한 디자인 결정은 일광 절약 시간제 (DST)에 대 한 흥미로운 부작용을 가질 수 있습니다 .이는 미국의 클록이 한 시간 앞으로 이동 하는 경우입니다 .이는 웹 서버가 일광 절약 시간제가 관찰 되는 로캘에서 호스트 되는 것으로 가정 합니다. DST가 시작 되는 시간 근처에 30 분의 만료 된 ASP.NET 웹 사이트의 경우 발생 하는 상황을 고려 합니다 (오전 2:00 시). 방문자가 2008 년 3 월 11 일 오전 1:55에 사이트에 로그인 한다고 가정 합니다. 그러면 2:25 오전 11 시 2008에 만료 되는 폼 인증 티켓이 생성 됩니다 (앞으로 30 분). 그러나 2:00가 롤업되 면 클록은 DST로 인해 3:00 오전로 이동 합니다. 사용자가 로그인 한 후 6 분 후에 새 페이지를 로드 하는 경우 (오전 3:01 시) FormsAuthenticationModule는 티켓이 만료 되었음을 메모 하 고 사용자를 로그인 페이지로 리디렉션합니다. 이 및 기타 인증 티켓 시간 제한 oddities에 대 한 자세한 내용은 Stefan Schackow의 *전문 ASP.NET 2.0 보안, 멤버 자격 및 역할 관리* (ISBN: 978-0-7645-9698-8)의 복사본을 선택 합니다.

그림 1에서는 slidingExpiration가 false로 설정 되 고 timeout이 30으로 설정 된 경우의 워크플로를 보여 줍니다. 로그인 시 생성 된 인증 티켓에는 만료 날짜가 포함 되며,이 값은 후속 요청에서 업데이트 되지 않습니다. 티켓이 만료 된 것을 발견 하면 FormsAuthenticationModule는 삭제 하 고 요청을 익명으로 처리 합니다.

[slidingExpiration가 false 인 경우 폼 인증 티켓 만료의 그래픽 표시를 ![합니다.](forms-authentication-configuration-and-advanced-topics-cs/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image1.png)

**그림 01**: slidingExpiration이 False 인 경우 폼 인증 티켓 만료의 그래픽 표현 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image3.png))

그림 2에서는 slidingExpiration가 true로 설정 되 고 timeout이 30으로 설정 된 경우의 워크플로를 보여 줍니다. 만료 된 티켓을 사용 하 여 인증 된 요청이 수신 되 면 만료 시간은 나중 시간 (분)으로 업데이트 됩니다.

[slidingExpiration가 true 인 경우 폼 인증 티켓의 그래픽 표시를 ![합니다.](forms-authentication-configuration-and-advanced-topics-cs/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image4.png)

**그림 02**: slidingExpiration가 True 인 경우 폼 인증 티켓의 그래픽 표현 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image6.png))

쿠키 기반 인증 티켓 (기본값)을 사용 하는 경우 쿠키에 고유한 expiries 지정 될 수도 있으므로이 논의는 약간 더 복잡 합니다. 쿠키의 만료 (또는 해당 없음)는 쿠키를 소멸 시킬 때 브라우저에 지시 합니다. 쿠키가 만료 되지 않으면 브라우저가 종료 될 때 소멸 됩니다. 그러나 만료가 있으면 만료에 지정 된 날짜와 시간이 경과할 때까지 쿠키는 사용자의 컴퓨터에 저장 된 상태로 유지 됩니다. 브라우저에서 쿠키를 제거 하면 더 이상 웹 서버에 전송 되지 않습니다. 따라서 쿠키의 소멸은 사이트에서 로그 아웃 하는 사용자와 유사 합니다.

> [!NOTE]
> 물론 사용자는 자신의 컴퓨터에 저장 된 모든 쿠키를 사전에 제거할 수 있습니다. Internet Explorer 7에서 도구, 옵션으로 이동 하 여 검색 기록 섹션에서 삭제 단추를 클릭 합니다. 여기에서 쿠키 삭제 단추를 클릭 합니다.

폼 인증 시스템은 *Persistcookie* 매개 변수에 전달 된 값에 따라 세션 기반 또는 만료 기반 쿠키를 만듭니다. FormsAuthentication 클래스의 GetAuthCookie, SetAuthCookie 및 RedirectFromLoginPage 메서드는 두 개의 입력 매개 변수인 *username* 및 *persistcookie*를 사용 합니다. 이전 자습서에서 만든 로그인 페이지에는 영구 쿠키를 만들었는지 여부를 결정 하는 me me (암호 포함) 확인란이 포함 되어 있습니다. 영구 쿠키는 만료 기반입니다. 비영구 쿠키는 세션을 기반으로 합니다.

이미 설명한 timeout 및 slidingExpiration 개념은 세션 및 만료 기반 쿠키 모두에 동일 하 게 적용 됩니다. 실행에는 약간의 사소한 차이점이 있습니다. slidingTimeout가 true로 설정 된 만료 기반 쿠키를 사용 하는 경우 지정 된 시간의 절반 이상이 경과 된 경우에만 쿠키의 만료가 업데이트 됩니다.

슬라이딩 만료를 사용 하 여 1 시간 (60 분) 후 티켓 시간 제한이 되도록 웹 사이트의 인증 티켓 시간 제한 정책을 업데이트 해 보겠습니다. 이 변경 내용을 적용 하려면 Web.config 파일을 업데이트 하 여 다음 태그를 사용 하 여 &lt;인증&gt; 요소에 &lt;forms&gt; 요소를 추가 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Login.aspx 이외의 로그인 페이지 URL 사용

FormsAuthenticationModule는 권한이 없는 사용자를 로그인 페이지로 자동으로 리디렉션 하므로 로그인 페이지의 URL을 알아야 합니다. 이 URL은 &lt;forms&gt; 요소의 loginUrl 특성으로 지정 되며, 기본값은 login.aspx입니다. 기존 웹 사이트를 통해 이식 하는 경우 이미 다른 URL을 사용 하는 로그인 페이지가 있을 수 있습니다. 다른 URL은 이미 검색 엔진에 의해 책갈피를 설정 하 고 인덱싱됩니다. 기존 로그인 페이지의 이름을 login.aspx로 바꾸고 링크 및 사용자의 책갈피를 분리 하는 대신 loginUrl 특성을 수정 하 여 로그인 페이지를 가리키도록 할 수 있습니다.

예를 들어 로그인 페이지 이름이 login.aspx 인 사용자 디렉터리에 있는 경우 loginUrl 구성 설정을 ~/Users/SignIn.aspx와 같이 지정할 수 있습니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample3.xml)]

현재 응용 프로그램에는 login.aspx 라는 로그인 페이지가 이미 있으므로 &lt;forms&gt; 요소에 사용자 지정 값을 지정할 필요가 없습니다.

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>2 단계: 쿠키 없는 폼 인증 티켓 사용

기본적으로 폼 인증 시스템은 쿠키 컬렉션에 인증 티켓을 저장할지 여부를 결정 하 고 사이트를 방문 하는 사용자 에이전트에 따라 URL에 해당 티켓을 포함 합니다. Internet Explorer, Firefox, Opera 및 Safari와 같은 모든 기본 데스크톱 브라우저는 쿠키를 지원 하지만 일부 모바일 장치에서는 지원 하지 않습니다.

폼 인증 시스템에서 사용 하는 쿠키 정책은 &lt;forms&gt; 요소의 쿠키 없는 설정에 따라 달라 지 며 다음 네 값 중 하나를 할당할 수 있습니다.

- UseCookies-쿠키 기반 인증 티켓을 항상 사용 하도록 지정 합니다.
- UseUri-쿠키 기반 인증 티켓을 사용 하지 않음을 나타냅니다.
- 자동 검색-장치 프로필에서 쿠키를 지원 하지 않으면 쿠키 기반 인증 티켓이 사용 되지 않습니다. 장치 프로필에서 쿠키를 지 원하는 경우 검색 메커니즘을 사용 하 여 쿠키를 사용할 수 있는지 여부를 확인 합니다.
- UseDeviceProfile-기본값 는 장치 프로필에서 쿠키를 지 원하는 경우에만 쿠키 기반 인증 티켓을 사용 합니다. 검색 메커니즘이 사용 되지 않습니다.

자동 검색 및 UseDeviceProfile 설정은 쿠키 기반 또는 쿠키 없는 인증 티켓을 사용할지 여부를 확인의 *장치 프로필* 에 의존 합니다. ASP.NET은 쿠키를 지원 하는지 여부, 지원 되는 JavaScript 버전 등과 같은 다양 한 장치 및 해당 기능에 대 한 데이터베이스를 유지 관리 합니다. 장치가 웹 서버에서 웹 페이지를 요청할 때마다 장치 유형을 식별 하는 *사용자 에이전트* HTTP 헤더를 따라 보냅니다. ASP.NET는 제공 된 사용자 에이전트 문자열과 해당 데이터베이스에 지정 된 해당 프로필을 자동으로 일치 시킵니다.

> [!NOTE]
> 이 장치 기능 데이터베이스는 [브라우저 정의 파일 스키마](https://msdn.microsoft.com/library/ms228122.aspx)를 따르는 여러 XML 파일에 저장 됩니다. 기본 장치 프로필 파일 은%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers.에 있습니다. 응용 프로그램의 앱\_브라우저 폴더에 사용자 지정 파일을 추가할 수도 있습니다. 자세한 내용은 [방법: ASP.NET 웹 페이지에서 브라우저 종류 검색](https://msdn.microsoft.com/library/3yekbd5b.aspx)을 참조 하세요.

기본 설정은 UseDeviceProfile 이므로 프로필이 쿠키를 지원 하지 않는다는 것을 보고 하는 장치에서 사이트를 방문할 때 쿠키 없는 폼 인증 티켓이 사용 됩니다.

### <a name="encoding-the-authentication-ticket-in-the-url"></a>URL의 인증 티켓 인코딩

쿠키는 브라우저에서 특정 웹 사이트에 대 한 각 요청에 정보를 포함 하는 데 사용할 수 있는 기본 미디어 이며,이는 방문 장치에서 지 원하는 경우 기본 폼 인증 설정에서 쿠키를 사용 하는 것입니다. 쿠키가 지원 되지 않는 경우 클라이언트에서 서버로 인증 티켓을 전달 하는 대체 방법을 사용 해야 합니다. 쿠키를 사용 하지 않는 환경에서 사용 되는 일반적인 해결 방법은 쿠키 데이터를 URL로 인코딩하는 것입니다.

URL에 이러한 정보를 포함 하는 방법을 확인 하는 가장 좋은 방법은 사이트에서 쿠키 없는 인증 티켓을 강제로 사용 하도록 하는 것입니다. 이 작업은 쿠키 없는 구성 설정을 UseUri로 설정 하 여 수행할 수 있습니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample4.xml)]

이렇게 변경한 후에는 브라우저를 통해 사이트를 방문 하세요. 익명 사용자로 방문할 때 Url은 이전과 동일 하 게 표시 됩니다. 예를 들어 default.aspx 페이지를 방문할 때 브라우저의 주소 표시줄에 다음 URL이 표시 됩니다.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

그러나 로그인 할 때 폼 인증 티켓이 URL에 포함 됩니다. 예를 들어 로그인 페이지를 방문 하 고 Sam으로 로그인 한 후에는 default.aspx 페이지로 반환 되지만 URL은 다음과 같습니다.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

폼 인증 티켓이 URL 내에 포함 되었습니다. 문자열 (F (jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv)는 16 진수로 인코딩된 인증 티켓 정보를 나타내며 쿠키 내에 일반적으로 저장 되는 데이터와 동일 합니다.

쿠키 없는 인증 티켓이 작동 하려면 시스템에서 인증 티켓 데이터를 포함 하도록 페이지의 모든 Url을 인코딩해야 합니다. 그렇지 않으면 사용자가 링크를 클릭할 때 인증 티켓이 손실 됩니다. 다행히이 포함 논리는 자동으로 수행 됩니다. 이 기능을 설명 하려면 default.aspx 페이지를 열고 Text 및 NavigateUrl 속성을 테스트 링크와 SomePage로 각각 설정 하 여 하이퍼링크 컨트롤을 추가 합니다. SomePage 라는 프로젝트의 페이지는 정말로 중요 하지 않습니다.

Default.aspx에 변경 내용을 저장 한 다음 브라우저를 통해 방문 합니다. 폼 인증 티켓이 URL에 포함 되도록 사이트에 로그온 합니다. 그런 다음 default.aspx에서 링크 테스트 링크를 클릭 합니다. 경우 SomePage 라는 페이지가 없으면 404 오류가 발생 했지만 여기서 중요 한 것은 아닙니다. 대신 브라우저의 주소 표시줄에 집중 합니다. URL에 폼 인증 티켓이 포함 되어 있습니다.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

링크의 URL SomePage는 인증 티켓을 포함 하는 URL로 자동으로 변환 됩니다. 코드를 작성할 필요가 없습니다. 양식 인증 티켓은 `http://` 또는 `/`으로 시작 하지 않는 하이퍼링크의 URL에 자동으로 포함 됩니다. 응답이 호출에 표시 되는 것은 중요 하지 않습니다. 리디렉션, 하이퍼링크 컨트롤 또는 앵커 HTML 요소 (예: `<a href="...">...</a>`). URL이 `http://www.someserver.com/SomePage.aspx` 또는 `/SomePage.aspx`와 같은 것이 아닌 경우에는 폼 인증 티켓이 포함 됩니다.

> [!NOTE]
> 쿠키를 사용 하지 않는 폼 인증 티켓은 쿠키 기반 인증 티켓과 동일한 시간 제한 정책을 준수 합니다. 그러나 인증 티켓이 URL에 직접 포함 되어 있으므로 쿠키 없는 인증 티켓은 재생 공격에 더 취약 합니다. 웹 사이트를 방문 하 여 로그인 한 다음 전자 메일의 URL을 동료에 게 붙여 넣는 사용자를 가정 합니다. 만료 되기 전에 동료가 해당 링크를 클릭 하면 전자 메일을 보낸 사용자로 로그인 됩니다.

## <a name="step-3-securing-the-authentication-ticket"></a>3 단계: 인증 티켓 보안 설정

폼 인증 티켓이 쿠키에서 전송 되거나 URL 내에 직접 포함 되어 전송 됩니다. Id 정보 외에도 인증 티켓에는 4 단계에서 볼 수 있는 것 처럼 사용자 데이터가 포함 될 수 있습니다. 따라서 티켓의 데이터가 prying 눈동자에서 암호화 되는 것이 중요 합니다. 폼 인증 시스템이 티켓이 변조 되지 않았음을 보장할 수 있습니다.

티켓 데이터의 개인 정보 보호를 위해 폼 인증 시스템은 티켓 데이터를 암호화할 수 있습니다. 티켓 데이터를 암호화 하지 못하면 네트워크를 통해 잠재적으로 중요 한 정보가 일반 텍스트로 전송 됩니다.

티켓의 신뢰성을 보장 하려면 폼 인증 시스템에서 티켓의 *유효성을 검사* 해야 합니다. 유효성 검사는 특정 데이터 부분이 수정 되지 않았음을 확인 하 고 *[MAC (메시지 인증 코드)](http://en.wikipedia.org/wiki/Message_authentication_code)* 를 통해 수행 되는 동작입니다. 간단히 말해서 MAC은 유효성을 검사 해야 하는 데이터 (이 경우 티켓)를 식별 하는 작은 정보입니다. MAC이 나타내는 데이터가 수정 된 경우 MAC 및 데이터가 일치 하지 않습니다. 또한 해커는 데이터를 수정 하 고 수정 된 데이터에 해당 하는 고유한 MAC을 생성 하는 것이 어렵습니다.

티켓을 만들거나 수정 하는 경우 폼 인증 시스템은 MAC을 만들어 티켓의 데이터에 연결 합니다. 후속 요청이 도착 하면 폼 인증 시스템은 MAC 및 티켓 데이터를 비교 하 여 티켓 데이터의 신뢰성을 확인 합니다. 그림 3에서는이 워크플로를 그래픽으로 보여 줍니다.

[MAC을 통해 티켓의 신뢰성을 보장 ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image7.png)

**그림 03**: MAC을 통해 티켓의 신뢰성[확인 (전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image9.png))

인증 티켓에 적용 되는 보안 조치는 &lt;forms&gt; 요소의 보호 설정에 따라 달라 집니다. 보호 설정은 다음 세 가지 값 중 하나에 할당할 수 있습니다.

- 모두-티켓이 암호화 되 고 디지털 서명 됩니다 (기본값).
- 암호화 전용 암호화가 적용 됨-MAC이 생성 되지 않습니다.
- 없음-티켓이 암호화 되거나 디지털 서명 되지 않습니다.
- 유효성 검사-MAC이 생성 되지만 티켓 데이터는 네트워크를 통해 일반 텍스트로 전송 됩니다.

모든 설정을 사용 하는 것이 좋습니다.

### <a name="setting-the-validation-and-decryption-keys"></a>유효성 검사 및 암호 해독 키 설정

Forms 인증 시스템에서 인증 티켓을 암호화 하 고 유효성을 검사 하는 데 사용 하는 암호화 및 해시 알고리즘은 Web.config의 [&lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx) 를 통해 사용자 지정할 수 있습니다. 표 2에서는 &lt;machineKey&gt; 요소의 특성과 가능한 값을 간략하게 설명 합니다.

| **특성** | **설명** |
| --- | --- |
| 암호 해독 | 암호화에 사용 되는 알고리즘을 나타냅니다. 이 특성에는 다음 네 가지 값 중 하나를 사용할 수 있습니다.-Auto-기본값 decryptionKey 특성의 길이를 기준으로 알고리즘을 결정 합니다. -AES- [AES(Advanced Encryption Standard) (aes)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 알고리즘을 사용 합니다. -DES- [des (Data Encryption Standard)](http://en.wikipedia.org/wiki/Data_Encryption_Standard) 를 사용 합니다 .이 알고리즘은 계산 weak로 간주 되므로 사용해 서는 안 됩니다. -3DES-DES 알고리즘을 세 번 적용 하 여 작동 하는 [TRIPLE des](http://en.wikipedia.org/wiki/Triple_DES) 알고리즘을 사용 합니다. |
| decryptionKey | 암호화 알고리즘에서 사용 하는 비밀 키입니다. 이 값은 암호 해독의 값에 따라 적절 한 길이의 16 진수 문자열 이거나, 자동 생성 이거나, IsolateApps에 추가 된 값 이어야 합니다. IsolateApps를 추가 하면 ASP.NET가 각 응용 프로그램에 고유한 값을 사용 하도록 지시 합니다. 기본값은 자동 생성, IsolateApps입니다. |
| 유효성 검사 | 유효성 검사에 사용 되는 알고리즘을 나타냅니다. 이 특성에는 다음 네 가지 값 중 하나를 사용할 수 있습니다.-AES-AES(Advanced Encryption Standard) (AES) 알고리즘을 사용 합니다. -MD5- [md5 (메시지 다이제스트 5)](http://en.wikipedia.org/wiki/MD5) 알고리즘을 사용 합니다. -SHA1- [sha1](http://en.wikipedia.org/wiki/Sha1) 알고리즘 (기본값)을 사용 합니다. -3DES-Triple DES 알고리즘을 사용 합니다. |
| validationKey | 유효성 검사 알고리즘에서 사용 하는 비밀 키입니다. 이 값은 유효성 검사의 값에 따라 적절 한 길이의 16 진수 문자열 이거나, 자동 생성 이거나, IsolateApps에 추가 된 값 이어야 합니다. IsolateApps를 추가 하면 ASP.NET가 각 응용 프로그램에 고유한 값을 사용 하도록 지시 합니다. 기본값은 자동 생성, IsolateApps입니다. |

**표 2**: &lt;MachineKey&gt; 요소 특성

이러한 암호화 및 유효성 검사 옵션에 대 한 철저 한 논의와 다양 한 알고리즘의 장단점은이 자습서의 범위를 벗어나는 것입니다. 사용할 암호화 및 유효성 검사 알고리즘, 사용할 키 길이, 이러한 키를 생성 하는 최상의 방법에 대 한 지침을 포함 하 여 이러한 문제에 대 한 자세한 내용을 보려면 *Professional ASP.NET 2.0 보안, 멤버 자격 및 역할 관리*를 참조 하세요.

기본적으로 암호화 및 유효성 검사에 사용 되는 키는 각 응용 프로그램에 대해 자동으로 생성 되 고 이러한 키는 LSA (로컬 보안 기관)에 저장 됩니다. 간단히 말해서 기본 설정은 웹 서버 및 응용 프로그램 별로 고유한 키를 보장 합니다. 따라서 다음과 같은 두 가지 시나리오에서는이 기본 동작이 작동 하지 않습니다.

- **웹** 팜- [웹 팜](http://en.wikipedia.org/wiki/Web_farm) 시나리오에서 단일 웹 응용 프로그램은 확장성 및 중복성을 위해 여러 웹 서버에서 호스팅됩니다. 들어오는 각 요청은 팜의 서버로 디스패치 됩니다. 즉, 사용자 세션의 수명 동안 여러 서버를 사용 하 여 다양 한 요청을 처리할 수 있습니다. 따라서 각 서버는 동일한 암호화 및 유효성 검사 키를 사용 하 여 한 서버에서 생성, 암호화 및 유효성 검사 된 forms 인증 티켓을 해독 하 고 팜의 다른 서버에서 유효성을 검사할 수 있도록 해야 합니다.
- **크로스 응용 프로그램 티켓 공유** -단일 웹 서버는 여러 ASP.NET 응용 프로그램을 호스트할 수 있습니다. 이러한 여러 응용 프로그램이 단일 폼 인증 티켓을 공유 해야 하는 경우 암호화 및 유효성 검사 키가 일치 해야 합니다.

웹 팜 설정에서 작업 하거나 동일한 서버의 응용 프로그램 간에 인증 티켓을 공유 하는 경우 decryptionKey 및 validationKey 값이 일치 하도록 영향을 받는 응용 프로그램에서 &lt;machineKey&gt; 요소를 구성 해야 합니다.

위의 시나리오 중 어느 것도 샘플 응용 프로그램에 적용 되지 않지만 명시적인 decryptionKey 및 validationKey 값을 지정 하 고 사용할 알고리즘을 정의할 수 있습니다. &lt;machineKey&gt; 설정을 Web.config 파일에 추가 합니다.

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample5.xml)]

자세한 내용은 [How to: Configure MachineKey in ASP.NET 2.0](https://msdn.microsoft.com/library/ms998288.aspx)을 참조 하세요.

> [!NOTE]
> DecryptionKey 및 validationKey 값은 [Steve Gibson](http://www.grc.com/stevegibson.htm)의 [완벽 한 암호 웹 페이지](https://www.grc.com/passwords.htm)에서 가져온 것입니다 .이 페이지는 각 페이지에서 64의 임의의 16 진수 문자를 생성 합니다. 이러한 키가 프로덕션 응용 프로그램에 사용 될 가능성을 줄이기 위해 완벽 한 암호 페이지에서 임의로 생성 된 키로 위의 키를 바꾸는 것이 좋습니다.

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>4 단계: 티켓에 추가 사용자 데이터 저장

많은 웹 응용 프로그램은 현재 로그온 한 사용자에 대 한 정보를 표시 하거나 페이지의 표시를 기준으로 합니다. 예를 들어, 웹 페이지에는 사용자 이름과 각 페이지의 위쪽 모서리에 마지막으로 로그온 한 날짜가 표시 될 수 있습니다. 폼 인증 티켓에는 현재 로그온 한 사용자의 사용자 이름이 저장 되지만, 다른 정보가 필요 하면 해당 페이지는 사용자 저장소 (일반적으로 데이터베이스)로 이동 하 여 인증 티켓에 저장 되지 않은 정보를 조회 해야 합니다.

약간의 코드를 사용 하 여 폼 인증 티켓에 추가 사용자 정보를 저장할 수 있습니다. 이러한 데이터는 [양식 Authenticationticket 클래스](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx)의 [UserData 속성](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)을 통해 표현할 수 있습니다. 이는 일반적으로 필요한 사용자에 대 한 소량의 정보를 저장 하는 데 유용 합니다. UserData 속성에 지정 된 값은 인증 티켓 쿠키의 일부로 포함 되며, 다른 티켓 필드와 마찬가지로 폼 인증 시스템의 구성에 따라 암호화 되 고 유효성이 검사 됩니다. 기본적으로 UserData는 빈 문자열입니다.

인증 티켓에 사용자 데이터를 저장 하기 위해 사용자 관련 정보를 가져와 하 고 티켓에 저장 하는 코드를 로그인 페이지에 작성 해야 합니다. UserData는 문자열 형식의 속성이 기 때문에 저장 된 데이터는 문자열로 올바르게 serialize 되어야 합니다. 예를 들어 사용자 저장소에 각 사용자의 생년월일 및 채용 기관의 이름을 포함 하 고 이러한 두 속성 값을 인증 티켓에 저장 하려는 경우를 가정해 보겠습니다. 사용자의 생년월일 문자열을 파이프 (|)에 연결 하 고 그 뒤에 고용주 이름을 연결 하 여 이러한 값을 문자열로 serialize 할 수 있습니다. Northwind 상인에 대해 작동 하는 1974 년 8 월 15 일에 태어난 사용자의 경우 UserData 속성을 문자열: 1974-08-15 |로 할당 합니다. Northwind Traders.

티켓에 저장 된 데이터에 액세스 해야 할 때마다 현재 요청의 양식 Authenticationticket을 시도 하 고 UserData 속성을 deserialize 하 여 수행할 수 있습니다. 생년월일 및 고용주 이름 예의 경우 구분 기호 (|)에 따라 UserData 문자열을 두 개의 부분 문자열로 분할 합니다.

[![추가 사용자 정보를 인증 티켓에 저장할 수 있습니다.](forms-authentication-configuration-and-advanced-topics-cs/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image10.png)

**그림 04**: 추가 사용자 정보를 인증 티켓에 저장할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image12.png)).

### <a name="writing-information-to-userdata"></a>UserData에 정보 쓰기

아쉽게도 폼 인증 티켓에 사용자 관련 정보를 추가 하는 것은 어떤 경우에도 간단 하지 않습니다. 양식 Authenticationticket 클래스의 UserData 속성은 읽기 전용 이며,이 속성은 양식 Authenticationticket 클래스 생성자를 통해서만 지정할 수 있습니다. 생성자에서 UserData 속성을 지정 하는 경우에는 사용자 이름, 문제 날짜, 만료 등과 같은 티켓의 다른 값도 제공 해야 합니다. 이전 자습서에서 로그인 페이지를 만들 때 FormsAuthentication 클래스에서이를 모두 처리 했습니다. 양식 Authenticationticket에 UserData를 추가할 때 FormsAuthentication 클래스에서 이미 제공 하는 많은 기능을 복제 하는 코드를 작성 해야 합니다.

인증 티켓에 사용자에 대 한 추가 정보를 기록 하도록 login.aspx 페이지를 업데이트 하 여 UserData를 사용 하는 데 필요한 코드를 살펴보겠습니다. 사용자 저장소에는 사용자가 작업 하는 회사와 해당 제목에 대 한 정보를 포함 하 고 있으며 인증 티켓에서이 정보를 캡처해야 한다고 가정 합니다. 코드가 다음과 같이 표시 되도록 Login .aspx 페이지의 LoginButton Click 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample6.cs)]

이 코드를 한 번에 한 줄씩 단계별로 살펴보겠습니다. 메서드는 사용자, 암호, companyName 및 titleAtCompany의 네 가지 문자열 배열을 정의 하 여 시작 합니다. 이러한 배열에는 시스템의 사용자 계정에 대 한 사용자 이름, 암호, 회사 이름 및 제목이 포함 되며 세 가지 Scott, Jisun 및 Sam이 있습니다. 실제 응용 프로그램에서 이러한 값은 페이지의 소스 코드에서 하드 코드 되지 않고 사용자 저장소에서 쿼리 됩니다.

이전 자습서에서 제공 된 자격 증명이 유효한 경우 FormsAuthentication (RedirectFromLoginPage, RememberMe. Checked) 라고 하며,이는 다음 단계를 수행 합니다.

1. 폼 인증 티켓을 만듦
2. 적절 한 저장소에 티켓을 기록 합니다. 쿠키 기반 인증 티켓의 경우 브라우저의 쿠키 컬렉션이 사용 됩니다. 쿠키 없는 인증 티켓의 경우 티켓 데이터가 URL로 serialize 됩니다.
3. 사용자를 적절 한 페이지로 리디렉션

이러한 단계는 위의 코드에서 복제 됩니다. 첫째, 궁극적으로 UserData 속성에 저장 되는 문자열은 회사 이름과 제목을 결합 하 여 두 값을 파이프 문자 (|)로 구분 하 여 구성 됩니다.

문자열 userDataString = 문자열입니다. Concat (companyName [i], "|", titleAtCompany [i]);

그런 다음 FormsAuthentication 메서드를 호출 합니다 .이 메서드는 인증 티켓을 만들고, 구성 설정에 따라 암호화 하 고 유효성을 검사 하 고, 되어 개체에 배치 합니다.

되어 authCookie = FormsAuthentication. GetAuthCookie (UserName, RememberMe. Checked);

쿠키 내에 포함 된 FormAuthenticationTicket 작업을 수행 하려면 FormAuthentication 클래스의 [암호 해독 메서드](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)를 호출 하 여 쿠키 값을 전달 해야 합니다.

양식 Authenticationticket 티켓 = FormsAuthentication (authCookie. Value);

그런 다음 기존 양식 Authenticationticket의 값을 기반으로 *새* 양식 authenticationticket 인스턴스를 만듭니다. 그러나이 새 티켓에는 사용자 관련 정보 (userDataString)가 포함 됩니다.

양식 Authenticationticket newTicket = 새 양식 Authenticationticket (티켓) 버전, 티켓. 이름, 티켓. IssueDate, 티켓. 만료, 티켓. IsPersistent, userDataString);

그런 다음 [encrypt 메서드](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)를 호출 하 여 새 양식 authenticationticket 인스턴스를 암호화 하 고 유효성을 검사 하 고이 암호화 된 데이터와 유효성이 검사 된 데이터를 authcookie에 다시 넣습니다.

authCookie. Value = FormsAuthentication (newTicket);

마지막으로, authCookie는 Response 컬렉션에 추가 되 고 사용자를 보낼 적절 한 페이지를 결정 하기 위해 GetRedirectUrl 메서드가 호출 됩니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample7.cs)]

UserData 속성이 읽기 전용이 고 FormsAuthentication 클래스가 GetAuthCookie, SetAuthCookie 또는 RedirectFromLoginPage 메서드에서 UserData 정보를 지정 하는 메서드를 제공 하지 않기 때문에이 코드는 모두 필요 합니다.

> [!NOTE]
> 방금 검사 한 코드는 쿠키 기반 인증 티켓에 사용자 관련 정보를 저장 합니다. 폼 인증 티켓을 URL로 serialize 하는 클래스는 .NET Framework 내부에 있습니다. 긴 스토리는 사용자 데이터를 쿠키 없는 폼 인증 티켓에 저장할 수 없다는 것입니다.

### <a name="accessing-the-userdata-information"></a>UserData 정보 액세스

이 시점에서 각 사용자의 회사 이름과 제목은 로그인 할 때 폼 인증 티켓의 UserData 속성에 저장 됩니다. 이 정보는 사용자 저장소로 이동 하지 않고도 모든 페이지의 인증 티켓에서 액세스할 수 있습니다. UserData 속성에서이 정보를 검색 하는 방법을 설명 하기 위해 default.aspx를 업데이트 해 보겠습니다. 그러면 환영 메시지에 사용자의 이름 뿐만 아니라 회사에서 사용 하는 회사도 포함 될 수 있습니다.

현재 default.aspx에는 WelcomeBackMessage 이라는 레이블 컨트롤이 있는 AuthenticatedMessagePanel 패널이 포함 되어 있습니다. 이 패널은 인증 된 사용자 에게만 표시 됩니다. 다음과 같이 default.aspx의 페이지\_Load 이벤트 처리기에서 코드를 업데이트 합니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample8.cs)]

WelcomeBackMessage가 true 이면 먼저의 Text 속성이 환영 back, *username*으로 설정 됩니다. 그런 다음, 기본 양식 Authenticationticket에 액세스할 수 있도록 사용자 Id 속성을 FormsIdentity 개체로 캐스팅 합니다. 양식 Authenticationticket이 있으면 UserData 속성을 회사 이름 및 제목으로 deserialize 합니다. 이는 파이프 문자에서 문자열을 분할 하 여 수행 됩니다. 그러면 회사 이름과 제목이 WelcomeBackMessage 레이블에 표시 됩니다.

그림 5는 이러한 표시의 스크린샷을 보여 줍니다. Scott로 로그인 하면 Scott의 회사 및 직위를 포함 하는 환영 메시지를 표시 합니다.

[현재 로그온 한 사용자의 회사 및 타이틀 ![표시 됩니다.](forms-authentication-configuration-and-advanced-topics-cs/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image13.png)

**그림 05**: 현재 로그온 한 사용자의 회사 및 제목 표시 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image15.png))

> [!NOTE]
> 인증 티켓의 UserData 속성은 사용자 저장소에 대 한 캐시 역할을 합니다. 모든 캐시와 마찬가지로 기본 데이터를 수정할 때 업데이트 해야 합니다. 예를 들어 사용자가 프로필을 업데이트할 수 있는 웹 페이지가 있는 경우 사용자가 수행한 변경 내용을 반영 하도록 UserData 속성에 캐시 된 필드를 새로 고쳐야 합니다.

## <a name="step-5-using-a-custom-principal"></a>5 단계: 사용자 지정 보안 주체 사용

들어오는 각 요청에서 FormsAuthenticationModule는 사용자를 인증 하려고 시도 합니다. 만료 되지 않은 인증 티켓이 있는 경우 FormsAuthenticationModule는 새 GenericPrincipal 개체에 HttpContext 속성을 할당 합니다. 이 GenericPrincipal 개체는 폼 인증 티켓에 대 한 참조를 포함 하는 FormsIdentity 형식의 Id를 가집니다. GenericPrincipal 클래스는 IPrincipal을 구현 하는 클래스에 필요한 완전 한 최소 기능을 포함 합니다. Identity 속성과 IsInRole 메서드만 있습니다.

주 개체에는 사용자가 속한 역할을 나타내고 id 정보를 제공 하는 두 가지 책임이 있습니다. 이는 각각 IPrincipal 인터페이스의 IsInRole (*roleName*) 메서드와 Identity 속성을 통해 수행 됩니다. GenericPrincipal 클래스를 사용 하면 해당 생성자를 통해 역할 이름의 문자열 배열을 지정할 수 있습니다. IsInRole (*roleName*) 메서드는 전달 된 *roleName* 가 문자열 배열 내에 있는지만 확인 합니다. FormsAuthenticationModule은 GenericPrincipal을 만들 때 GenericPrincipal의 생성자에 빈 문자열 배열을 전달 합니다. 따라서 IsInRole에 대 한 모든 호출은 항상 false를 반환 합니다.

GenericPrincipal 클래스는 역할이 사용 되지 않는 대부분의 폼 기반 인증 시나리오에 대 한 요구 사항을 충족 합니다. 기본 역할 처리가 충분 하지 않거나 사용자 지정 IIdentity 개체를 사용자와 연결 해야 하는 경우에는 인증 워크플로 중에 사용자 지정 IPrincipal 개체를 만들어 HttpContext 속성에 할당할 수 있습니다.

> [!NOTE]
> 이후 자습서에서 볼 수 있듯이 ASP를 사용할 수 있습니다. NET의 Roles 프레임 워크를 사용 하도록 설정 하면 [roleprincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx) 형식의 사용자 지정 보안 주체 개체를 만들고 폼 인증 생성 genericprincipal 개체를 덮어씁니다. 역할 프레임 워크의 API와 인터페이스 하는 보안 주체의 IsInRole 메서드를 사용자 지정 하기 위해이를 수행 합니다.

역할을 아직 고려 하지 않았으므로이 분기 시점에서 사용자 지정 보안 주체를 만드는 것은 사용자 지정 IIdentity 개체를 보안 주체에 연결 하는 것입니다. 4 단계에서는 인증 티켓의 UserData 속성, 특히 사용자의 회사 이름 및 제목에 추가 사용자 정보를 저장 하는 방법을 살펴보았습니다. 그러나 UserData 정보는 인증 티켓을 통해서만 액세스할 수 있으며 직렬화 된 문자열로만 액세스할 수 있습니다. 즉, 언제 든 지 티켓에 저장 된 사용자 정보를 보려는 경우 UserData 속성을 구문 분석 해야 합니다.

IIdentity을 구현 하 고 CompanyName 및 Title 속성을 포함 하는 클래스를 만들어 개발자 환경을 개선할 수 있습니다. 이러한 방식으로 개발자는 UserData 속성을 구문 분석 하는 방법을 알 필요 없이 CompanyName 및 Title 속성을 통해 현재 로그온 한 사용자의 회사 이름 및 제목에 직접 액세스할 수 있습니다.

### <a name="creating-the-custom-identity-and-principal-classes"></a>사용자 지정 Id 및 보안 주체 클래스 만들기

이 자습서에서는 앱\_코드 폴더에 사용자 지정 principal 및 identity 개체를 만들어 보겠습니다. 먼저 프로젝트에 앱\_코드 폴더를 추가 하 고 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 ASP.NET 폴더 추가 옵션을 선택 하 고 앱\_코드를 선택 합니다. 앱\_코드 폴더는 웹 사이트와 관련 된 클래스 파일을 보관 하는 특수 한 ASP.NET 폴더입니다.

> [!NOTE]
> 응용 프로그램\_코드 폴더는 웹 사이트 프로젝트 모델을 통해 프로젝트를 관리할 때만 사용 해야 합니다. [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/asp.net/Aa336618.aspx)을 사용 하는 경우 표준 폴더를 만들고 해당 폴더에 클래스를 추가 합니다. 예를 들어 클래스 라는 새 폴더를 추가 하 고 여기에 코드를 저장할 수 있습니다.

다음으로 두 개의 새 클래스 파일을 App\_Code 폴더에 추가 합니다. 하나는 CustomIdentity.cs이 고 CustomPrincipal.cs는 이름이 지정 됩니다.

[CustomIdentity 및 CustomPrincipal 클래스를 프로젝트에 추가 ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image16.png)

**그림 06**: CustomIdentity 및 Customprincipal 클래스를 프로젝트에 추가 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image18.png))

CustomIdentity 클래스는 AuthenticationType, IsAuthenticated 및 Name 속성을 정의 하는 IIdentity 인터페이스를 구현 합니다. 이러한 필수 속성 외에도 기본 폼 인증 티켓과 사용자의 회사 이름 및 제목에 대 한 속성을 표시 하는 데 관심이 있습니다. CustomIdentity 클래스에 다음 코드를 입력 합니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample9.cs)]

클래스에는 양식 Authenticationticket 멤버 변수 (\_티켓)가 포함 되어 있으며 생성자를 통해이 티켓 정보를 제공 해야 합니다. 이 티켓 데이터는 id 이름을 반환 하는 데 사용 됩니다. UserData 속성은 CompanyName 및 Title 속성의 값을 반환 하기 위해 구문 분석 됩니다.

다음으로 CustomPrincipal 클래스를 만듭니다. 이 분기 시점 역할에는 관심이 없으므로 CustomPrincipal 클래스의 생성자는 CustomIdentity 개체만 허용 합니다. 해당 IsInRole 메서드는 항상 false를 반환 합니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample10.cs)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>들어오는 요청의 보안 컨텍스트에 CustomPrincipal 개체 할당

이제 사용자 지정 id를 사용 하는 사용자 지정 보안 주체 클래스 뿐만 아니라 CompanyName 및 Title 속성을 포함 하도록 기본 IIdentity 사양을 확장 하는 클래스가 있습니다. ASP.NET 파이프라인을 한 단계씩 실행 하 고 사용자 지정 보안 주체 개체를 들어오는 요청의 보안 컨텍스트에 할당할 준비가 되었습니다.

ASP.NET 파이프라인은 들어오는 요청을 받아서 여러 단계를 통해 처리 합니다. 각 단계에서 특정 이벤트가 발생 하 여 개발자가 ASP.NET 파이프라인을 탭 하 고 해당 수명 주기의 특정 지점에서 요청을 수정할 수 있습니다. 예를 들어 FormsAuthenticationModule는 ASP.NET가 [AuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)를 발생 시킬 때까지 대기 하며,이 시점에서 인증 티켓에 대 한 들어오는 요청을 검사 합니다. 인증 티켓이 있으면 GenericPrincipal 개체가 생성 되어 HttpContext 속성에 할당 됩니다.

AuthenticateRequest 이벤트가 발생 한 후 ASP.NET 파이프라인은 [PostAuthenticateRequest 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)를 발생 시킵니다. 여기서 FormsAuthenticationModule에 의해 생성 된 genericprincipal 개체를 customprincipal 개체의 인스턴스로 바꿀 수 있습니다. 그림 7은이 워크플로를 나타냅니다.

[GenericPrincipal이 PostAuthenticationRequest 이벤트에서 CustomPrincipal으로 대체 ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image19.png)

**그림 07**: genericprincipal이 PostAuthenticationRequest 이벤트에서 Customprincipal으로 대체 됨 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image21.png))

ASP.NET 파이프라인 이벤트에 대 한 응답으로 코드를 실행 하기 위해 global.asax에서 적절 한 이벤트 처리기를 만들거나 고유한 HTTP 모듈을 만들 수 있습니다. 이 자습서에서는 Global.asax에서 이벤트 처리기를 만들어 보겠습니다. 웹 사이트에 global.asax를 추가 하 여 시작 합니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 global.asax 라는 전역 응용 프로그램 클래스 형식의 항목을 추가 합니다.

[웹 사이트에 global.asax 파일을 추가 ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image22.png)

**그림 08**: 웹 사이트에 Global.asax 파일 추가 ([전체 크기 이미지를 보려면 클릭](forms-authentication-configuration-and-advanced-topics-cs/_static/image24.png))

기본 global.asax 템플릿에는 시작, 종료 및 [오류 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)를 비롯 한 다양 한 ASP.NET 파이프라인 이벤트에 대 한 이벤트 처리기가 포함 되어 있습니다. 이러한 이벤트 처리기는이 응용 프로그램에 필요 하지 않으므로 자유롭게 제거할 수 있습니다. 관심이 있는 이벤트는 PostAuthenticateRequest입니다. Global.asax 파일이 다음과 같이 표시 되도록 Global.asax 파일을 업데이트 합니다.

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample11.aspx)]

응용 프로그램\_OnPostAuthenticateRequest 메서드는 각 수신 페이지 요청에서 한 번씩 발생 하는 PostAuthenticateRequest 이벤트를 발생 시킬 때마다 실행 됩니다. 이벤트 처리기는 사용자가 인증 되었으며 폼 인증을 통해 인증 되었는지 여부를 확인 하 여 시작 합니다. 이 경우 새 CustomIdentity 개체가 만들어지고 생성자에서 현재 요청의 인증 티켓이 전달 됩니다. 다음에는 CustomPrincipal 개체가 만들어지고 생성자에서 방금 만든 CustomIdentity 개체를 전달 합니다. 마지막으로, 현재 요청의 보안 컨텍스트가 새로 만든 CustomPrincipal 개체에 할당 됩니다.

마지막 단계는 CustomPrincipal 개체와 요청의 보안 컨텍스트를 연결 하는 것입니다.-두 속성 (HttpContext 및 System.threading.thread.currentprincipal)에 보안 주체를 할당 합니다. 보안 컨텍스트가 ASP.NET에서 처리 되는 방식 때문에 이러한 두 할당이 필요 합니다. .NET Framework는 실행 중인 각 스레드와 보안 컨텍스트를 연결 합니다. 이 정보는 [스레드 개체](https://msdn.microsoft.com/library/system.threading.thread.aspx)의 [system.threading.thread.currentprincipal 속성](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)을 통해 IPrincipal 개체로 사용할 수 있습니다. ASP.NET에는 자체 보안 컨텍스트 정보 (HttpContext)가 있습니다.

특정 시나리오에서는 보안 컨텍스트를 결정할 때 System.threading.thread.currentprincipal 속성을 검사 합니다. 다른 시나리오에서는 Httpcontext.current가 사용 됩니다. 예를 들어 개발자가 클래스를 인스턴스화하거나 특정 메서드를 호출할 수 있는 사용자 또는 역할을 선언적으로 지정할 수 있도록 하는 .NET의 보안 기능이 있습니다 ( [Principal사용 특성을 사용 하 여 비즈니스 및 데이터 계층에 권한 부여 규칙 추가](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)참조). 이러한 선언적 기술은 내부적으로 System.threading.thread.currentprincipal 속성을 통해 보안 컨텍스트를 결정 합니다.

다른 시나리오에서는 Httpcontext.current 속성을 사용 합니다. 예를 들어 이전 자습서에서는이 속성을 사용 하 여 현재 로그온 한 사용자의 사용자 이름을 표시 했습니다. System.threading.thread.currentprincipal 및 Httpcontext.current 속성의 보안 컨텍스트 정보가 일치 하는지 명확 하 게 확인 해야 합니다.

ASP.NET 런타임은 이러한 속성 값을 자동으로 동기화 합니다. 그러나이 동기화는 AuthenticateRequest 이벤트 이후, PostAuthenticateRequest 이벤트 *이전* 에 발생 합니다. 따라서 PostAuthenticateRequest 이벤트에서 사용자 지정 보안 주체를 추가 하는 경우 System.threading.thread.currentprincipal 또는 System.threading.thread.currentprincipal와 HttpContext가 동기화 되지 않습니다. 사용자는 수동으로 할당 해야 합니다. 이 문제에 대 한 자세한 내용은 [system.threading.thread.currentprincipal 및](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) 를 참조 하세요.

### <a name="accessing-the-companyname-and-title-properties"></a>CompanyName 및 Title 속성 액세스

요청이 도착 하 고 ASP.NET 엔진에 디스패치 될 때마다 global.asax의 응용 프로그램\_OnPostAuthenticateRequest 이벤트 처리기가 발생 합니다. FormsAuthenticationModule에 의해 요청이 성공적으로 인증 되 면 이벤트 처리기는 폼 인증 티켓을 기반으로 CustomIdentity 개체를 사용 하 여 새 CustomPrincipal 개체를 만듭니다. 이 논리를 사용 하는 경우 현재 로그온 한 사용자의 회사 이름과 제목에 대 한 정보에 액세스 하는 것은 매우 간단 합니다.

Default.aspx의 페이지\_Load 이벤트 처리기로 돌아갑니다. 4 단계에서는 인증 티켓을 검색 하 고 사용자의 회사 이름과 제목을 표시 하기 위해 UserData 속성을 구문 분석 하는 코드를 작성 했습니다. 현재 사용 중인 CustomPrincipal 및 CustomIdentity 개체를 사용 하 여 티켓의 UserData 속성에서 값을 구문 분석할 필요가 없습니다. 대신 CustomIdentity 개체에 대 한 참조를 가져오고 해당 CompanyName 및 Title 속성을 사용 하면 됩니다.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample12.cs)]

## <a name="summary"></a>요약

이 자습서에서는 Web.config를 통해 폼 인증 시스템의 설정을 사용자 지정 하는 방법을 살펴보았습니다. 인증 티켓의 만료를 처리 하는 방법 및 암호화 및 유효성 검사 보호를 사용 하 여 검사 및 수정 으로부터 티켓을 보호 하는 방법을 살펴보았습니다. 마지막으로, 인증 티켓의 UserData 속성을 사용 하 여 추가 사용자 정보를 티켓 자체에 저장 하 고, 사용자 지정 principal 및 identity 개체를 사용 하 여 더 많은 개발자에 게 친숙 한 방식으로이 정보를 노출 하는 방법을 설명 했습니다.

이 자습서에서는 ASP.NET에서 폼 인증에 대 한 검사를 마칩니다. 다음 자습서에서는 멤버 자격 프레임 워크에 대 한 전환을 시작 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [개로 나누어서 폼 인증](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [설명: ASP.NET 2.0의 폼 인증](https://msdn.microsoft.com/library/aa480476.aspx)
- [방법: ASP.NET 2.0에서 폼 인증 보호](https://msdn.microsoft.com/library/ms998310.aspx)
- [전문 ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [로그인 컨트롤 보안](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;authentication&gt; 요소](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;인증을 위한 &lt;forms&gt; 요소&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; 요소](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [폼 인증 티켓 및 쿠키 이해](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 학습

- [폼 인증 속성을 변경 하는 방법](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [ASP.NET 응용 프로그램에서 쿠키 없는 인증을 설정 하 고 사용 하는 방법](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP 폼 로그인 재배치](../../../videos/authentication/asp-forms-login-relocation.md)
- [폼 로그인 사용자 지정 키 구성](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [인증 방법에 사용자 지정 데이터 추가](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [사용자 지정 보안 주체 개체 사용](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Alicja Maziarz입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](an-overview-of-forms-authentication-cs.md)
> [다음](security-basics-and-asp-net-support-vb.md)
