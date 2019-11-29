---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-cs
title: 역할 기반 권한 부여 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 역할 프레임 워크가 사용자의 역할을 보안 컨텍스트와 연결 하는 방법을 살펴봅니다. 그런 다음 역할 기반 URL을 적용 하는 방법을 검토 합니다.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 4d9b63fa-c3d4-4e85-82b1-26ae3ba3ca1c
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-cs
msc.type: authoredcontent
ms.openlocfilehash: 46153ab310bdee814baaa53c372fb92f8a23ce11
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619657"
---
# <a name="role-based-authorization-c"></a>역할 기반 권한 부여(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.11.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_cs.pdf)

> 이 자습서에서는 역할 프레임 워크가 사용자의 역할을 보안 컨텍스트와 연결 하는 방법을 살펴봅니다. 그런 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 검토 합니다. 이를 통해 표시 되는 데이터와 ASP.NET 페이지에서 제공 하는 기능을 변경 하기 위해 선언적이 고 프로그래밍 방식으로 사용 하는 방법을 살펴보겠습니다.

## <a name="introduction"></a>소개

<a id="_msoanchor_1"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서에서는 URL 권한 부여를 사용 하 여 특정 페이지 집합을 방문할 수 있는 사용자를 지정 하는 방법을 살펴보았습니다. `Web.config`에서 약간 약간의 태그만 사용 하 여 인증 된 사용자만 페이지를 방문 하도록 ASP.NET에 지시할 수 있습니다. 또는 사용자에 게 Tito와 Bob이 허용 되었거나 Sam을 제외한 모든 인증 된 사용자만 허용 됨을 나타낼 수 있습니다.

URL 권한 부여 외에도 사용자 방문에 따라 페이지에서 제공 되는 데이터 및 표시 되는 데이터를 제어 하는 선언적 및 프로그래밍 방식의 기법을 살펴보았습니다. 특히 현재 디렉터리의 콘텐츠를 나열 하는 페이지를 만들었습니다. 누구나이 페이지를 방문할 수 있지만 인증 된 사용자만 파일의 내용을 볼 수 있으며, 파일을 삭제할 수 있습니다.

사용자를 기준으로 권한 부여 규칙을 적용 하는 것은 장부의 영향을 크게 증가 시킬 수 있습니다. 더 쉽게 관리할 수 있는 방법은 역할 기반 권한 부여를 사용 하는 것입니다. 좋은 소식은 권한 부여 규칙을 적용 하는 데 필요한 도구가 사용자 계정에 대해 수행 하는 역할과 동일 하 게 잘 작동 한다는 것입니다. URL 권한 부여 규칙은 사용자 대신 역할을 지정할 수 있습니다. 인증 된 사용자와 익명 사용자에 대해 서로 다른 출력을 렌더링 하는 LoginView 컨트롤은 로그인 한 사용자의 역할에 따라 다른 콘텐츠를 표시 하도록 구성할 수 있습니다. 및 역할 API에는 로그인 한 사용자의 역할을 결정 하는 메서드가 포함 되어 있습니다.

이 자습서에서는 역할 프레임 워크가 사용자의 역할을 보안 컨텍스트와 연결 하는 방법을 살펴봅니다. 그런 다음 역할 기반 URL 권한 부여 규칙을 적용 하는 방법을 검토 합니다. 이를 통해 표시 되는 데이터와 ASP.NET 페이지에서 제공 하는 기능을 변경 하기 위해 선언적이 고 프로그래밍 방식으로 사용 하는 방법을 살펴보겠습니다. 시작 하겠습니다.

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>사용자의 보안 컨텍스트와 역할을 연결 하는 방법 이해

요청은 ASP.NET 파이프라인에 진입할 때마다 요청자를 식별 하는 정보를 포함 하는 보안 컨텍스트와 연결 됩니다. 폼 인증을 사용 하는 경우 인증 티켓이 id 토큰으로 사용 됩니다. <a id="_msoanchor_2"> </a> [*폼 인증*](../introduction/an-overview-of-forms-authentication-cs.md) 및 <a id="_msoanchor_3"> </a> [*폼 인증 구성 및 고급 토픽*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서의 개요에서 설명한 것 처럼 `FormsAuthenticationModule`은 [`AuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)중에 수행 되는 요청자의 id를 확인 합니다.

만료 되지 않은 유효한 인증 티켓이 발견 되 면 `FormsAuthenticationModule`는 요청자의 id를 확인 하기 위해이를 디코딩합니다. 새 `GenericPrincipal` 개체를 만들고이 개체를 `HttpContext.User` 개체에 할당 합니다. `GenericPrincipal`와 같은 보안 주체의 목적은 인증 된 사용자의 이름 및 해당 사용자가 속한 역할을 식별 하는 것입니다. 이는 모든 보안 주체 개체에 `Identity` 속성과 `IsInRole(roleName)` 메서드가 있다는 사실에 의해 명백 합니다. 그러나 `FormsAuthenticationModule`는 역할 정보를 기록 하는 데 관심이 없으며, 만든 `GenericPrincipal` 개체는 역할을 지정 하지 않습니다.

역할 프레임 워크를 사용 하는 경우 [`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) HTTP 모듈이 `FormsAuthenticationModule` 후에의 단계를 수행 하 고 [`PostAuthenticateRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)중에 인증 된 사용자의 역할을 식별 합니다 .이 이벤트는 `AuthenticateRequest` 이벤트 후에 발생 합니다. 요청을 인증 된 사용자에서 보낸 경우 `RoleManagerModule` `FormsAuthenticationModule`에서 만든 `GenericPrincipal` 개체를 덮어쓰고 [`RolePrincipal` 개체로](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx)바꿉니다. `RolePrincipal` 클래스는 역할 API를 사용 하 여 사용자가 속한 역할을 결정 합니다.

그림 1에서는 폼 인증 및 역할 프레임 워크를 사용할 때 ASP.NET 파이프라인 워크플로를 보여 줍니다. `FormsAuthenticationModule` 먼저 실행 되 고, 사용자가 인증 티켓을 통해 사용자를 식별 하 고, 새 `GenericPrincipal` 개체를 만듭니다. 그런 다음 `RoleManagerModule`는의 단계를 수행 하 고 `GenericPrincipal` 개체를 `RolePrincipal` 개체로 덮어씁니다.

익명 사용자가 사이트를 방문 하는 경우 `FormsAuthenticationModule` 또는 `RoleManagerModule`는 주 개체를 만듭니다.

[폼 인증 및 역할 프레임 워크를 사용 하는 경우 인증 된 사용자에 대 한 ASP.NET 파이프라인 이벤트를 ![합니다.](role-based-authorization-cs/_static/image2.png)](role-based-authorization-cs/_static/image1.png)

**그림 1**: 폼 인증 및 역할 프레임 워크를 사용 하는 경우 인증 된 사용자에 대 한 ASP.NET 파이프라인 이벤트 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image3.png))

### <a name="caching-role-information-in-a-cookie"></a>쿠키에서 역할 정보 캐싱

`RolePrincipal` 개체의 `IsInRole(roleName)` 메서드는 `Roles.GetRolesForUser`를 호출 하 여 사용자가 *roleName*의 멤버 인지 여부를 확인 하기 위해 사용자에 대 한 역할을 가져옵니다. `SqlRoleProvider`사용 하는 경우 역할 저장소 데이터베이스에 대 한 쿼리가 생성 됩니다. 역할 기반 URL 권한 부여 규칙을 사용 하는 경우 역할 기반 URL 권한 부여 규칙에 의해 보호 되는 페이지에 대 한 모든 요청에 대해 `RolePrincipal`의 `IsInRole` 메서드가 호출 됩니다. 모든 요청에 대해 데이터베이스에서 역할 정보를 조회 해야 하는 대신, 역할 프레임 워크에는 쿠키에 사용자의 역할을 캐시 하는 옵션이 포함 되어 있습니다.

역할 프레임 워크가 사용자의 역할을 쿠키에 캐시 하도록 구성 된 경우 `RoleManagerModule` ASP.NET 파이프라인의 [`EndRequest` 이벤트](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)중에 쿠키를 만듭니다. 이 쿠키는 `PostAuthenticateRequest`의 후속 요청에 사용 됩니다 .이는 `RolePrincipal` 개체를 만든 시간입니다. 쿠키가 유효 하 고 만료 되지 않은 경우에는 쿠키의 데이터가 구문 분석 되 고 사용자의 역할을 채우는 데 사용 되므로 `Roles` 클래스를 호출 하 여 사용자의 역할을 결정 하지 않아도 `RolePrincipal` 저장 됩니다. 그림 2에서는이 워크플로를 보여 줍니다.

[![사용자의 역할 정보를 쿠키에 저장 하 여 성능을 향상 시킬 수 있습니다.](role-based-authorization-cs/_static/image5.png)](role-based-authorization-cs/_static/image4.png)

**그림 2**: 사용자의 역할 정보를 쿠키에 저장 하 여 성능을 향상 시킬 수 있습니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image6.png)).

기본적으로 역할 캐시 쿠키 메커니즘은 사용 하지 않도록 설정 되어 있습니다. `Web.config`에서 `<roleManager>` 구성 태그를 통해 사용 하도록 설정할 수 있습니다. [`<roleManager>` 요소](https://msdn.microsoft.com/library/ms164660.aspx) 를 사용 하 여 <a id="_msoanchor_4"> </a> [*역할 만들기 및 관리*](creating-and-managing-roles-cs.md) 자습서에서 역할 공급자를 지정 하는 방법을 설명 했으므로 응용 프로그램의 `Web.config` 파일에이 요소가 이미 있어야 합니다. 역할 캐시 쿠키 설정은 `<roleManager>` 요소의 특성으로 지정 되며 표 1에 요약 되어 있습니다.

> [!NOTE]
> 표 1에 나열 된 구성 설정은 결과 역할 캐시 쿠키의 속성을 지정 합니다. 쿠키, 작동 방법 및 다양 한 속성에 대 한 자세한 내용은 [이 쿠키 자습서](http://www.quirksmode.org/js/cookies.html)를 참조 하세요.

| <strong>Property</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>설명</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              쿠키 캐싱이 사용 되는지 여부를 나타내는 부울 값입니다. 기본값은 `false`입니다.                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     역할 캐시 쿠키의 이름입니다. 기본값은 "입니다. 역할을 합니다. "                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                역할 이름 쿠키의 경로입니다. 개발자는 path 특성을 사용 하 여 쿠키 범위를 특정 디렉터리 계층으로 제한할 수 있습니다. 기본값은 "/" 이며,이는 브라우저에서 도메인에 대 한 모든 요청에 인증 티켓 쿠키를 보내도록 알려 줍니다.                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               역할 캐시 쿠키를 보호 하는 데 사용 되는 기술을 나타냅니다. 허용 되는 값은 `All` (기본값)입니다. `Encryption`; `None`; 및를 `Validation`합니다. 이러한 보호 수준에 대 한 자세한 <a id="_anchor_5"> </a>내용은 [*Forms 인증 구성 및 고급 항목*](../introduction/forms-authentication-configuration-and-advanced-topics-cs.md) 자습서의 3 단계를 다시 참조 하세요.                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   인증 쿠키를 전송 하는 데 SSL 연결이 필요한 지 여부를 나타내는 부울 값입니다. 기본값은 `false`여야 합니다.                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  단일 세션 중에 사용자가 사이트를 방문할 때마다 쿠키의 시간 제한이 다시 설정 되는지 여부를 나타내는 부울 값입니다. 기본값은 `false`여야 합니다. 이 값은 `createPersistentCookie`이 `true`으로 설정 된 경우에만 관련이 있습니다.                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         인증 티켓 쿠키가 만료 되는 시간 (분)을 지정 합니다. 기본값은 `30`여야 합니다. 이 값은 `createPersistentCookie`이 `true`으로 설정 된 경우에만 관련이 있습니다.                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   역할 캐시 쿠키가 세션 쿠키 인지 아니면 영구 쿠키 인지를 지정 하는 부울 값입니다. `false` (기본값) 이면 브라우저를 닫을 때 삭제 되는 세션 쿠키가 사용 됩니다. `true`경우 영구 쿠키가 사용 됩니다. `cookieSlidingExpiration`값에 따라이 값이 생성 된 후 또는 이전에 방문한 후의 시간 (분) `cookieTimeout` 만료 됩니다.                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 쿠키의 도메인 값을 지정 합니다. 기본값은 빈 문자열입니다 .이 문자열을 사용 하면 브라우저가 발급 된 도메인 (예: www.yourdomain.com)을 사용 합니다. 이 경우 admin.yourdomain.com와 같은 하위 도메인에 대 한 요청을 만들 때 쿠키가 전송 <strong>되지</strong> 않습니다. 모든 하위 도메인에 쿠키를 전달 하려면 `domain` 특성을 "yourdomain.com"로 설정 하 여 사용자 지정 해야 합니다.                                                                                                                                                 |
|    `maxCachedResults`     | 쿠키에 캐시 되는 최대 역할 이름 수를 지정 합니다. 기본값은 25입니다. `RoleManagerModule`는 `maxCachedResults` 역할에 속하는 사용자에 대 한 쿠키를 만들지 않습니다. 따라서 `RolePrincipal` 개체의 `IsInRole` 메서드에서는 `Roles` 클래스를 사용 하 여 사용자의 역할을 결정 합니다. `maxCachedResults` 존재 하는 이유는 많은 사용자 에이전트가 4096 바이트 보다 큰 쿠키를 허용 하지 않기 때문입니다. 따라서이 캡은 이러한 크기 제한을 초과 하는 가능성을 줄이기 위한 것입니다. 역할 이름이 매우 긴 경우 더 작은 `maxCachedResults` 값을 지정 하는 것을 고려할 수 있습니다. contrariwise 역할 이름이 매우 짧은 경우이 값을 늘릴 수 있습니다. |

**표 1:** 역할 캐시 쿠키 구성 옵션

비영구 역할 캐시 쿠키를 사용 하도록 응용 프로그램을 구성 해 보겠습니다. 이 작업을 수행 하려면 `Web.config`에서 `<roleManager>` 요소를 업데이트 하 여 다음과 같은 쿠키 관련 특성을 포함 합니다.

[!code-xml[Main](role-based-authorization-cs/samples/sample1.xml)]

`cacheRolesInCookie`, `createPersistentCookie`및 `cookieProtection`의 세 가지 특성을 추가 하 여 `<roleManager>` 요소를 업데이트 했습니다. `cacheRolesInCookie`를 `true`로 설정 하면 `RoleManagerModule`에서 각 요청에 대 한 사용자의 역할 정보를 조회 하지 않고 쿠키에 사용자 역할을 자동으로 캐시 합니다. `createPersistentCookie` 및 `cookieProtection` 특성을 명시적으로 `false` 및 `All`로 각각 설정 합니다. 기술적으로는 이러한 특성에 대 한 값을 기본값에 할당 했기 때문에 이러한 특성에 대 한 값을 지정할 필요가 없지만, 영구 쿠키를 사용 하지 않고 쿠키를 암호화 하 고 유효성을 검사 하는 것을 명시적으로 명확 하 게 하려면 여기에 입력 합니다.

이것이 전부입니다! 예측이 역할 프레임 워크는 사용자의 역할을 쿠키에 캐시 합니다. 사용자의 브라우저에서 쿠키를 지원 하지 않거나 쿠키를 삭제 하거나 손실 하는 경우에는 큰 문제가 없습니다. `RolePrincipal` 개체는 쿠키를 사용 하지 않는 경우 (또는 유효 하지 않거나 만료 된 경우)에만 `Roles` 클래스를 사용 합니다.

> [!NOTE]
> Microsoft의 패턴 &amp; 영구 역할 캐시 쿠키를 사용 하는 것은 권장 되지 않습니다. 역할 캐시 쿠키의 소유는 역할 멤버 자격을 증명 하는 데 충분 하므로 해커가 유효한 사용자의 쿠키에 대 한 액세스 권한을 얻을 수 있으면 해당 사용자를 가장할 수 있습니다. 쿠키가 사용자의 브라우저에서 지속 되 면 이러한 상황이 발생할 가능성이 높아집니다. 이 보안 권장 사항 및 기타 보안 고려 사항에 대 한 자세한 내용은 [ASP.NET 2.0에 대 한 보안 질문 목록을](https://msdn.microsoft.com/library/ms998375.aspx)참조 하세요.

## <a name="step-1-defining-role-based-url-authorization-rules"></a>1 단계: 역할 기반 URL 권한 부여 규칙 정의

<a id="_msoanchor_6"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서에서 설명 하는 것 처럼 URL 권한 부여는 사용자 또는 역할별 역할 별로 페이지 집합에 대 한 액세스를 제한 하는 수단을 제공 합니다. URL 권한 부여 규칙은 `<allow>` 및 `<deny>` 자식 요소와 함께 [`<authorization>` 요소](https://msdn.microsoft.com/library/8d82143t.aspx) 를 사용 하 여 `Web.config`에서 주석으로 처리 됩니다. 이전 자습서에서 설명한 사용자 관련 권한 부여 규칙 외에도 각 `<allow>` 및 `<deny>` 자식 요소에는 다음이 포함 될 수 있습니다.

- 특정 역할
- 쉼표로 구분 된 역할 목록

예를 들어 URL 권한 부여 규칙은 관리자 및 감독자 역할의 사용자에 게 액세스 권한을 부여 하지만 다른 모든 사용자에 대 한 액세스를 거부 합니다.

[!code-xml[Main](role-based-authorization-cs/samples/sample2.xml)]

위의 태그에서 `<allow>` 요소는 Administrators 및 감독자 역할이 허용 되는 상태를 표시 합니다. `<deny>` 요소는 *모든* 사용자가 거부 되었음을 지시 합니다.

`ManageRoles.aspx`, `UsersAndRoles.aspx`및 `CreateUserWizardWithRoles.aspx` 페이지를 관리자 역할의 사용자만 액세스할 수 있도록 응용 프로그램을 구성 하 고, `RoleBasedAuthorization.aspx` 페이지는 모든 방문자에 게 계속 액세스할 수 있습니다.

이를 수행 하려면 먼저 `Roles` 폴더에 `Web.config` 파일을 추가 합니다.

[역할 디렉터리에 web.config 파일을 추가 ![](role-based-authorization-cs/_static/image8.png)](role-based-authorization-cs/_static/image7.png)

**그림 3**: `Roles` 디렉터리에 `Web.config` 파일 추가 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image9.png))

그런 다음 `Web.config`에 다음 구성 태그를 추가 합니다.

[!code-xml[Main](role-based-authorization-cs/samples/sample3.xml)]

`<system.web>` 섹션의 `<authorization>` 요소는 Administrators 역할의 사용자만 `Roles` 디렉터리의 ASP.NET 리소스에 액세스할 수 있음을 나타냅니다. `<location>` 요소는 `RoleBasedAuthorization.aspx` 페이지에 대 한 URL 권한 부여 규칙의 대체 집합을 정의 하 여 모든 사용자가 페이지를 방문할 수 있도록 합니다.

`Web.config`에 대 한 변경 내용을 저장 한 후 관리자 역할에 없는 사용자로 로그인 한 다음 보호 된 페이지 중 하나를 방문 하십시오. `UrlAuthorizationModule`는 요청한 리소스를 방문할 권한이 없다는 것을 감지 합니다. 따라서 `FormsAuthenticationModule` 로그인 페이지로 리디렉션됩니다. 그러면 로그인 페이지가 `UnauthorizedAccess.aspx` 페이지로 리디렉션됩니다 (그림 4 참조). <a id="_msoanchor_7"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서의 2 단계에서 로그인 페이지에 추가 된 코드 때문에 로그인 페이지의이 최종 리디렉션은 `UnauthorizedAccess.aspx` 발생 합니다. 특히,이 매개 변수는 사용자가 볼 권한이 없는 페이지를 보려고 시도한 후에 사용자가 로그인 페이지에 도착 했음을 나타내므로 로그인 페이지는 모든 인증 된 사용자를 `ReturnUrl` `UnauthorizedAccess.aspx`으로 자동 리디렉션합니다.

[![관리자 역할의 사용자만 보호 된 페이지를 볼 수 있습니다.](role-based-authorization-cs/_static/image11.png)](role-based-authorization-cs/_static/image10.png)

**그림 4**: 관리자 역할의 사용자만 보호 된 페이지를 볼 수 있음 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image12.png))

로그 오프 한 다음 관리자 역할에 있는 사용자로 로그인 합니다. 이제 세 개의 보호 된 페이지를 볼 수 있습니다.

[![Tito는 관리자 역할에 있기 때문에 UsersAndRoles 페이지를 방문할 수 있습니다.](role-based-authorization-cs/_static/image14.png)](role-based-authorization-cs/_static/image13.png)

**그림 5**: `UsersAndRoles.aspx` 페이지를 방문 하 여 관리자 역할을 할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image15.png)).

> [!NOTE]
> 역할 또는 사용자에 대해 URL 권한 부여 규칙을 지정 하는 경우 규칙은 위에서 아래로 한 번에 하나씩 분석 된다는 점을 명심 해야 합니다. 일치 항목이 발견 되는 즉시 사용자에 게 일치 항목을 `<allow>` 또는 `<deny>` 요소에서 찾을 수 있는지에 따라 액세스 권한이 부여 되거나 거부 됩니다. **일치 항목을 찾을 수 없는 경우 사용자에 게 액세스 권한이 부여 됩니다.** 따라서 하나 이상의 사용자 계정에 대 한 액세스를 제한 하려는 경우 URL 권한 부여 구성에서 `<deny>` 요소를 마지막 요소로 사용 해야 합니다. **URL 권한 부여 규칙에`<deny>`요소가 포함 되지 않은 경우** **모든 사용자에 게 액세스 권한이 부여 됩니다.** URL 권한 부여 규칙을 분석 하는 방법에 대 한 자세한 내용은 <a id="_msoanchor_8"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서의 "`UrlAuthorizationModule` 권한 부여 규칙을 사용 하 여 액세스 권한을 부여 하거나 거부 하는 방법" 섹션을 참조 하세요.

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>2 단계: 현재 로그인 한 사용자의 역할을 기준으로 기능 제한

URL 권한 부여를 사용 하면 허용 되는 id와 특정 페이지 (또는 폴더 및 해당 하위 폴더의 모든 페이지)를 볼 때 거부 된 id를 명시 하는 정교 하지 않은 권한 부여 규칙을 쉽게 지정할 수 있습니다. 그러나 특정 한 경우에는 모든 사용자가 페이지를 방문 하도록 허용할 수 있지만 방문 사용자의 역할에 따라 페이지의 기능을 제한 하는 것이 좋습니다. 이 경우 사용자의 역할에 따라 데이터를 표시 하거나 숨기 거 나 특정 역할에 속한 사용자에 게 추가 기능을 제공할 수 있습니다.

이러한 미세 수준 역할 기반 권한 부여 규칙은 선언적으로 또는 프로그래밍 방식으로 구현 하거나 둘 중 일부를 조합 하 여 구현할 수 있습니다. 다음 섹션에서는 LoginView 컨트롤을 통해 선언적 미세 인증을 구현 하는 방법을 알아봅니다. 다음에는 프로그래밍 방식으로 살펴볼 것입니다. 그러나 세분화 된 권한 부여 규칙을 적용 하는 방법에 대 한 자세한 내용은 먼저 해당 기능이 방문 하는 사용자의 역할에 따라 달라 지는 페이지를 만들어야 합니다.

GridView에서 시스템의 모든 사용자 계정을 나열 하는 페이지를 만들어 보겠습니다. GridView에는 각 사용자의 사용자 이름, 전자 메일 주소, 마지막 로그인 날짜 및 사용자에 대 한 설명이 포함 됩니다. 각 사용자 정보를 표시 하는 것 외에도 GridView에는 편집 및 삭제 기능이 포함 됩니다. 처음에는 모든 사용자가 사용할 수 있는 편집 및 삭제 기능을 사용 하 여이 페이지를 만들게 됩니다. "LoginView 컨트롤 사용" 및 "프로그래밍 방식으로 기능 제한" 섹션에서 방문 사용자의 역할에 따라 이러한 기능을 사용 하거나 사용 하지 않도록 설정 하는 방법을 확인할 수 있습니다.

> [!NOTE]
> 빌드 하려는 ASP.NET 페이지에서 GridView 컨트롤을 사용 하 여 사용자 계정을 표시 합니다. 이 자습서 시리즈는 폼 인증, 권한 부여, 사용자 계정 및 역할에 중점을 둘 수 있으므로 GridView 컨트롤의 내부 작업에 대해 너무 많은 시간을 할애 하지 않으려고 합니다. 이 자습서에서는이 페이지를 설정 하는 방법에 대 한 구체적인 단계별 지침을 제공 하지만 특정 항목을 선택 하는 이유와 렌더링 된 출력에 적용 되는 특정 속성에 대 한 자세한 내용은 설명 하지 않습니다. GridView 컨트롤을 철저 하 게 검사 하려면 ASP.NET 2.0 자습서 시리즈 *[의 데이터로 작업](../../data-access/index.md)* 을 확인 하세요.

먼저 `Roles` 폴더에서 `RoleBasedAuthorization.aspx` 페이지를 엽니다. 페이지에서 GridView를 디자이너로 끌어 `ID`를 `UserGrid`로 설정 합니다. 잠시 후 `Membership.GetAllUsers` 메서드를 호출 하 고 결과 `MembershipUserCollection` 개체를 GridView에 바인딩하는 코드를 작성 합니다. `MembershipUserCollection`는 시스템의 각 사용자 계정에 대 한 `MembershipUser` 개체를 포함 합니다. `MembershipUser` 개체에는 `UserName`, `Email`, `LastLoginDate`등의 속성이 있습니다.

사용자 계정을 표에 바인딩하는 코드를 작성 하기 전에 먼저 GridView의 필드를 정의 해 보겠습니다. GridView의 스마트 태그에서 "열 편집" 링크를 클릭 하 여 필드 대화 상자를 시작 합니다 (그림 6 참조). 여기에서 왼쪽 아래에 있는 "필드 자동 생성" 확인란의 선택을 취소 합니다. 이 GridView에서 편집 및 삭제 기능을 포함 하려고 하므로 CommandField를 추가 하 고 해당 `ShowEditButton` 및 `ShowDeleteButton` 속성을 True로 설정 합니다. 다음으로 `UserName`, `Email`, `LastLoginDate`및 `Comment` 속성을 표시 하는 네 개의 필드를 추가 합니다. 편집 가능한 두 필드 (`Email` 및 `Comment`)에 대해 두 개의 읽기 전용 속성 (`UserName` 및 `LastLoginDate`) 및 템플릿 필드에 대해 BoundField를 사용 합니다.

첫 번째 BoundField에 `UserName` 속성이 표시 되도록 합니다. `HeaderText` 및 `DataField` 속성을 "UserName"으로 설정 합니다. 이 필드는 편집할 수 없으므로 `ReadOnly` 속성을 True로 설정 합니다. `HeaderText`를 "마지막 로그인"으로 설정 하 고 해당 `DataField`를 "LastLoginDate"로 설정 하 여 `LastLoginDate` BoundField를 구성 합니다. 날짜 및 시간 대신 날짜만 표시 되도록이 BoundField의 출력 형식을 지정 하겠습니다. 이를 수행 하려면이 BoundField의 `HtmlEncode` 속성을 False로 설정 하 고 `DataFormatString` 속성을 "{0:d}"로 설정 합니다. 또한 `ReadOnly` 속성을 True로 설정 합니다.

두 개의 템플릿 필드의 `HeaderText` 속성을 "Email" 및 "Comment"로 설정 합니다.

[필드 대화 상자를 통해 GridView의 필드를 구성할 수 ![.](role-based-authorization-cs/_static/image17.png)](role-based-authorization-cs/_static/image16.png)

**그림 6**: 필드 대화 상자를 통해 GridView의 필드를 구성할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image18.png)).

이제 "전자 메일" 및 "주석" 템플릿 필드에 대 한 `ItemTemplate` 및 `EditItemTemplate`를 정의 해야 합니다. 각 `ItemTemplate`에 Label 웹 컨트롤을 추가 하 고 `Text` 속성을 `Email` 및 `Comment` 속성에 각각 바인딩합니다.

"Email" Templatefield로 변환의 경우 `Email` 이라는 텍스트 상자를 `EditItemTemplate`에 추가 하 고 양방향 데이터 바인딩을 사용 하 여 `Text` 속성을 `Email` 속성에 바인딩합니다. 전자 메일 속성을 편집 하는 방문자가 유효한 전자 메일 주소를 입력 했는지 확인 하려면 RequiredFieldValidator 및 RegularExpressionValidator을 `EditItemTemplate`에 추가 합니다. "Comment" Templatefield로 변환 `EditItemTemplate`에 `Comment` 라는 여러 줄 텍스트 상자를 추가 합니다. 텍스트 상자의 `Columns`와 `Rows` 속성을 각각 40 및 4로 설정 하 고, 양방향 데이터 바인딩을 사용 하 여 `Text` 속성을 `Comment` 속성에 바인딩합니다.

이러한 템플릿 필드를 구성한 후에는 해당 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](role-based-authorization-cs/samples/sample4.aspx)]

사용자 계정을 편집 하거나 삭제 하는 경우 해당 사용자의 `UserName` 속성 값을 알고 있어야 합니다. Gridview의 `DataKeys` 컬렉션을 통해이 정보를 사용할 수 있도록 GridView의 `DataKeyNames` 속성을 "UserName"으로 설정 합니다.

마지막으로 페이지에 ValidationSummary 컨트롤을 추가 하 고 해당 `ShowMessageBox` 속성을 True로 설정 하 고 `ShowSummary` 속성을 False로 설정 합니다. 이러한 설정을 사용 하면 사용자가 누락 되거나 잘못 된 전자 메일 주소를 사용 하 여 사용자 계정을 편집 하려고 하는 경우 ValidationSummary가 클라이언트 쪽 경고를 표시 합니다.

[!code-aspx[Main](role-based-authorization-cs/samples/sample5.aspx)]

이제이 페이지의 선언적 태그를 완료 했습니다. 다음 작업은 사용자 계정 집합을 GridView에 바인딩하는 것입니다. `Membership.GetAllUsers`에서 반환 하는 `MembershipUserCollection`을 `UserGrid` GridView에 바인딩하는 `RoleBasedAuthorization.aspx` 페이지의 코드 숨김이 클래스에 `BindUserGrid` 라는 메서드를 추가 합니다. 첫 번째 페이지의 `Page_Load` 이벤트 처리기에서이 메서드를 호출 합니다.

[!code-csharp[Main](role-based-authorization-cs/samples/sample6.cs)]

이 코드가 준비 되 면 브라우저를 통해 페이지를 방문 하세요. 그림 7에 표시 된 것 처럼 시스템의 각 사용자 계정에 대 한 정보를 나열 하는 GridView가 표시 되어야 합니다.

[UserGrid GridView ![시스템의 각 사용자에 대 한 정보를 나열 합니다.](role-based-authorization-cs/_static/image20.png)](role-based-authorization-cs/_static/image19.png)

**그림 7**: GridView `UserGrid` 시스템의 각 사용자에 대 한 정보 나열 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image21.png))

> [!NOTE]
> `UserGrid` GridView는 비페이징 인터페이스의 모든 사용자를 나열 합니다. 이 간단한 그리드 인터페이스는 수십 명 이상의 사용자가 있는 시나리오에 적합 하지 않습니다. 한 가지 옵션은 페이징을 사용 하도록 GridView를 구성 하는 것입니다. `Membership.GetAllUsers` 메서드에는 두 개의 오버 로드가 있습니다. 하나는 입력 매개 변수를 허용 하지 않고 모든 사용자를 반환 하 고, 다른 하나는 페이지 인덱스와 페이지 크기에 대 한 정수 값을 사용 하 고 지정 된 사용자 하위 집합만 반환 합니다. 두 번째 오버 로드는 *모든* 사용자가 아닌 사용자 계정의 정확한 하위 집합만 반환 하기 때문에 사용자를 보다 효율적으로 페이징 하는 데 사용할 수 있습니다. 사용자 계정이 수천 개인 경우 필터 기반 인터페이스를 사용 하는 것이 좋습니다. 예를 들어 사용자 이름이 선택한 문자로 시작 하는 사용자만 표시 됩니다. [`Membership.FindUsersByName method`](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) 는 필터 기반 사용자 인터페이스를 작성 하는 데 적합 합니다. 이후 자습서에서 이러한 인터페이스를 빌드하는 방법을 살펴보겠습니다.

GridView 컨트롤은 SqlDataSource 또는 ObjectDataSource와 같이 올바르게 구성 된 데이터 소스 컨트롤에 컨트롤이 바인딩될 때 기본 제공 편집 및 삭제 지원을 제공 합니다. 그러나 `UserGrid` GridView는 해당 데이터를 프로그래밍 방식으로 바인딩합니다. 따라서 이러한 두 가지 작업을 수행 하는 코드를 작성 해야 합니다. 특히, 방문자가 GridView의 편집, 취소, 업데이트 또는 삭제 단추를 클릭할 때 발생 하는 GridView의 `RowEditing`, `RowCancelingEdit`, `RowUpdating`및 `RowDeleting` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다.

먼저 GridView의 `RowEditing`, `RowCancelingEdit`및 `RowUpdating` 이벤트에 대 한 이벤트 처리기를 만든 후 다음 코드를 추가 합니다.

[!code-csharp[Main](role-based-authorization-cs/samples/sample7.cs)]

`RowEditing` 및 `RowCancelingEdit` 이벤트 처리기는 GridView의 `EditIndex` 속성을 설정한 다음 사용자 계정 목록을 표에 다시 바인딩합니다. `RowUpdating` 이벤트 처리기에서 흥미로운 항목이 발생 합니다. 이 이벤트 처리기는 먼저 데이터가 유효한 지 확인 한 다음 편집 된 사용자 계정의 `UserName` 값을 `DataKeys` 컬렉션에서 가져와 합니다. 그런 다음 두 개의 템플릿 필드 (`EditItemTemplate`)의 `Email` 및 `Comment` 텍스트 상자를 프로그래밍 방식으로 참조 합니다. 해당 `Text` 속성은 편집 된 전자 메일 주소와 주석을 포함 합니다.

멤버 자격 API를 통해 사용자 계정을 업데이트 하려면 먼저 `Membership.GetUser(userName)`에 대 한 호출을 통해 사용자 정보를 가져와야 합니다. 그러면 반환 된 `MembershipUser` 개체의 `Email` 및 `Comment` 속성이 편집 인터페이스에서 두 텍스트 상자에 입력 된 값으로 업데이트 됩니다. 마지막으로 이러한 수정 내용은 [`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx)에 대 한 호출과 함께 저장 됩니다. `RowUpdating` 이벤트 처리기는 GridView를 사전 편집 인터페이스로 되돌리면 완료 됩니다.

그런 다음 `RowDeleting` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](role-based-authorization-cs/samples/sample8.cs)]

위의 이벤트 처리기는 먼저 GridView의 `DataKeys` collection에서 `UserName` 값을 수집 합니다. 그런 다음이 `UserName` 값은 멤버 자격 클래스의 [`DeleteUser` 메서드에](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)전달 됩니다. `DeleteUser` 메서드는 관련 된 멤버 자격 데이터 (예:이 사용자가 속한 역할)를 포함 하 여 시스템에서 사용자 계정을 삭제 합니다. `EditIndex` 사용자를 삭제 한 후에는 사용자가 삭제를 클릭 하 여 다른 행이 편집 모드에 있는 동안에는 사용자가 삭제를 클릭 한 경우에는-1로 설정 되 고 `BindUserGrid` 메서드가 호출 됩니다.

> [!NOTE]
> 사용자 계정을 삭제 하기 전에는 삭제 단추에 사용자의 확인이 필요 하지 않습니다. 계정이 실수로 삭제 될 가능성을 줄이기 위해 일종의 사용자 확인을 추가 하는 것이 좋습니다. 동작을 확인 하는 가장 쉬운 방법 중 하나는 클라이언트 쪽 확인 대화 상자를 통하는 것입니다. 이 기술에 대 한 자세한 내용은 [삭제할 때 클라이언트 쪽 확인 추가](https://asp.net/learn/data-access/tutorial-42-cs.aspx)를 참조 하세요.

이 페이지가 예상 대로 작동 하는지 확인 합니다. 사용자의 전자 메일 주소와 의견을 편집 하 고 모든 사용자 계정을 삭제할 수 있어야 합니다. `RoleBasedAuthorization.aspx` 페이지에는 모든 사용자가 액세스할 수 있으므로 익명 방문자 라도이 페이지를 방문 하 여 사용자 계정을 편집 하 고 삭제할 수 있습니다. 감독자 및 관리자 역할의 사용자만 사용자의 이메일 주소와 의견을 편집할 수 있으며 관리자만 사용자 계정을 삭제할 수 있도록이 페이지를 업데이트 해 보겠습니다.

"LoginView 컨트롤 사용" 섹션에서는 LoginView 컨트롤을 사용 하 여 사용자의 역할과 관련 된 지침을 표시 하는 방법을 보여 줍니다. 관리자 역할의 사용자가이 페이지를 방문 하는 경우 사용자를 편집 하 고 삭제 하는 방법에 대 한 지침이 표시 됩니다. 감독자 역할의 사용자가이 페이지에 도달 하면 사용자 편집에 대 한 지침이 표시 됩니다. 그리고 방문자가 익명 이거나 감독자 또는 관리자 역할에 속하지 않는 경우 사용자 계정 정보를 편집 하거나 삭제할 수 없다는 메시지가 표시 됩니다. "프로그래밍 방식 제한 기능" 섹션에서 사용자의 역할에 따라 편집 및 삭제 단추를 프로그래밍 방식으로 표시 하거나 숨기는 코드를 작성 합니다.

### <a name="using-the-loginview-control"></a>LoginView 컨트롤 사용

이전 자습서에서 살펴본 것 처럼 LoginView 컨트롤은 인증 된 사용자와 익명 사용자에 대해 서로 다른 인터페이스를 표시 하는 데 유용 하지만 LoginView 컨트롤을 사용 하 여 사용자의 역할에 따라 다른 태그를 표시할 수도 있습니다. LoginView 컨트롤을 사용 하 여 방문한 사용자의 역할에 따라 다른 지침을 표시 해 보겠습니다.

`UserGrid` GridView 위에 LoginView를 추가 하 여 시작 합니다. 앞에서 설명한 대로 LoginView 컨트롤에는 두 개의 기본 제공 템플릿 인 `AnonymousTemplate`와 `LoggedInTemplate`있습니다. 사용자 정보를 편집 하거나 삭제할 수 없음을 사용자에 게 알리는 두 템플릿 모두에 간단한 메시지를 입력 합니다.

[!code-aspx[Main](role-based-authorization-cs/samples/sample9.aspx)]

`AnonymousTemplate` 및 `LoggedInTemplate`외에도 LoginView 컨트롤에는 역할 관련 템플릿인 *Rolegroups*가 포함 될 수 있습니다. 각 RoleGroup에는 단일 속성인 `Roles`이 포함 되어 있습니다 .이 속성은 RoleGroup이 적용 되는 역할을 지정 합니다. `Roles` 속성은 단일 역할 (예: "Administrators") 또는 쉼표로 구분 된 역할 목록 (예: "Administrators, 감독자")으로 설정할 수 있습니다.

RoleGroups를 관리 하려면 컨트롤의 스마트 태그에서 "RoleGroups 편집" 링크를 클릭 하 여 Rolegroups 컬렉션 편집기를 엽니다. 두 개의 새 RoleGroups를 추가 합니다. 첫 번째 RoleGroup의 `Roles` 속성을 "Administrators"로, 두 번째는 "감독자"로 설정 합니다.

[RoleGroup 컬렉션 편집기를 통해 LoginView의 역할별 템플릿을 관리 하는 ![](role-based-authorization-cs/_static/image23.png)](role-based-authorization-cs/_static/image22.png)

**그림 8**: Rolegroup 컬렉션 편집기를 통해 LoginView의 역할별 템플릿 관리 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image24.png))

확인을 클릭 하 여 RoleGroup 컬렉션 편집기를 닫습니다. 이렇게 하면 LoginView의 선언적 태그가 업데이트 되어 RoleGroup 컬렉션 편집기에 정의 된 각 RoleGroup에 대 한 `<asp:RoleGroup>` 자식 요소가 포함 된 `<RoleGroups>` 섹션이 포함 됩니다. 또한 LoginView의 스마트 태그에 있는 "Views" 드롭다운 목록에는 처음에 `AnonymousTemplate` 및 `LoggedInTemplate`만 나열 됩니다. 이제 추가 된 RoleGroups도 포함 됩니다.

감독자 역할의 사용자에 게는 사용자 계정을 편집 하는 방법에 대 한 지침이 표시 되 고 관리자 역할의 사용자에 게는 편집 및 삭제 지침이 표시 되도록 RoleGroups를 편집 합니다. 이러한 변경을 수행한 후에는 LoginView의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](role-based-authorization-cs/samples/sample10.aspx)]

이러한 변경을 수행한 후에는 페이지를 저장 하 고 브라우저를 통해 방문 합니다. 먼저 익명 사용자로 페이지를 방문 합니다. "시스템에 로그인 하지 않았습니다." 라는 메시지가 표시 됩니다. 따라서 사용자 정보를 편집 하거나 삭제할 수 없습니다. " 그런 다음 인증 된 사용자로 로그인 하지만 감독자 또는 관리자 역할에는 없습니다. 이번에는 "사용자가 감독자 또는 관리자 역할의 구성원이 아닙니다." 라는 메시지가 표시 됩니다. 따라서 사용자 정보를 편집 하거나 삭제할 수 없습니다. "

다음으로, 감독자 역할의 구성원 인 사용자로 로그인 합니다. 이번에는 감독자 역할 관련 메시지가 표시 됩니다 (그림 9 참조). 그리고 관리자 역할의 사용자로 로그인 하는 경우 관리자 역할 관련 메시지가 표시 됩니다 (그림 10 참조).

[![Bruce는 감독자 역할 관련 메시지를 표시 합니다.](role-based-authorization-cs/_static/image26.png)](role-based-authorization-cs/_static/image25.png)

**그림 9**: 감독자 역할 특정 메시지 표시 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image27.png))

[![Tito는 관리자 역할 관련 메시지를 표시 합니다.](role-based-authorization-cs/_static/image29.png)](role-based-authorization-cs/_static/image28.png)

**그림 10**: 관리자 역할 관련 메시지 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image30.png))가 표시 됩니다.

그림 9 및 10의 스크린 샷 처럼 LoginView는 여러 템플릿이 적용 되는 경우에도 하나의 템플릿만 렌더링 합니다. Bruce와 Tito가 모두 로그인 되어 있지만 LoginView은 일치 하는 RoleGroup만 렌더링 하 고 `LoggedInTemplate`는 렌더링 하지 않습니다. 또한 Tito는 관리자와 감독자 역할 모두에 속하지만 LoginView 컨트롤은 감독자 1 대신 관리자 역할 관련 템플릿을 렌더링 합니다.

그림 11에서는 LoginView 컨트롤에서 렌더링할 템플릿을 결정 하는 데 사용 하는 워크플로를 보여 줍니다. 하나 이상의 RoleGroup이 지정 된 경우 LoginView 템플릿은 일치 하는 *첫 번째* rolegroup을 렌더링 합니다. 즉, 감독자 RoleGroup을 첫 번째 RoleGroup으로 배치 하 고 관리자를 두 번째로 배치 했다면 Tito이 페이지를 방문 하면 감독자 메시지가 표시 됩니다.

[LoginView 컨트롤의 워크플로를 ![하 여 렌더링할 템플릿 결정](role-based-authorization-cs/_static/image32.png)](role-based-authorization-cs/_static/image31.png)

**그림 11**: 렌더링할 템플릿을 결정 하는 LoginView 컨트롤의 워크플로 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image33.png))

### <a name="programmatically-limiting-functionality"></a>프로그래밍 방식으로 기능 제한

LoginView 컨트롤은 페이지를 방문 하는 사용자의 역할에 따라 다른 명령을 표시 하지만 편집 및 취소 단추는 모두에 게 표시 됩니다. 감독자 또는 관리자 역할이 아닌 익명 방문자와 사용자에 대 한 편집 및 삭제 단추를 프로그래밍 방식으로 숨기는 것이 필요 합니다. 관리자가 아닌 모든 사용자에 대 한 삭제 단추를 숨겨야 합니다. 이를 수행 하기 위해 필요한 경우 CommandField의 Edit 및 Delete Linkbutton를 프로그래밍 방식으로 참조 하는 코드를 작성 하 고 `Visible` 속성을 `false`로 설정 합니다.

CommandField에서 프로그래밍 방식으로 컨트롤을 참조 하는 가장 쉬운 방법은 먼저 템플릿으로 변환 하는 것입니다. 이를 수행 하려면 GridView의 스마트 태그에서 "열 편집" 링크를 클릭 하 고 현재 필드 목록에서 CommandField를 선택한 다음 "이 필드를 Templatefield로 변환으로 변환" 링크를 클릭 합니다. 이렇게 하면 CommandField가 `ItemTemplate` 및 `EditItemTemplate`있는 Templatefield로 변환으로 전환 됩니다. `ItemTemplate`에는 `EditItemTemplate` 업데이트 및 취소 Linkbutton 있는 동안 편집 및 삭제 Linkbutton 포함 됩니다.

[CommandField를 Templatefield로 변환으로 변환 ![](role-based-authorization-cs/_static/image35.png)](role-based-authorization-cs/_static/image34.png)

**그림 12**: Commandfield를 templatefield로 변환으로 변환 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image36.png))

`ID` 속성을 `EditButton` 및 `DeleteButton`값으로 설정 하 여 `ItemTemplate`편집 및 삭제 Linkbutton를 업데이트 합니다.

[!code-aspx[Main](role-based-authorization-cs/samples/sample11.aspx)]

데이터가 GridView에 바인딩될 때마다 GridView는 `DataSource` 속성의 레코드를 열거 하 고 해당 `GridViewRow` 개체를 생성 합니다. `GridViewRow` 개체가 만들어질 때마다 `RowCreated` 이벤트가 발생 합니다. 권한 없는 사용자에 대 한 편집 및 삭제 단추를 숨기려면이 이벤트에 대 한 이벤트 처리기를 만들고 Linkbutton 편집 및 삭제를 프로그래밍 방식으로 참조 하 여 `Visible` 속성을 적절 하 게 설정 해야 합니다.

이벤트 처리기 `RowCreated` 이벤트를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](role-based-authorization-cs/samples/sample12.cs)]

`RowCreated` 이벤트는 헤더, 바닥글, 호출기 인터페이스 등을 비롯 한 *모든* GridView 행에 대해 발생 합니다. 편집 모드에 있지 않은 데이터 행을 처리 하는 경우에만 편집 및 삭제 Linkbutton를 프로그래밍 방식으로 참조 하려고 합니다. 편집 모드의 행에는 편집 및 삭제 대신 업데이트 및 취소 단추가 있기 때문입니다. 이 검사는 `if` 문에 의해 처리 됩니다.

편집 모드에 있지 않은 데이터 행을 처리 하는 경우에는 편집 및 삭제 Linkbutton이 참조 되 고 해당 `Visible` 속성은 `User` 개체의 `IsInRole(roleName)` 메서드에서 반환 된 부울 값을 기반으로 설정 됩니다. 사용자 개체는 `RoleManagerModule`에서 만든 보안 주체를 참조 합니다. 따라서 `IsInRole(roleName)` 메서드는 Roles API를 사용 하 여 현재 방문자가 *roleName*에 속하는지 여부를 확인 합니다.

> [!NOTE]
> 역할 클래스를 직접 사용 하 여 `User.IsInRole(roleName)`에 대 한 호출을 [`Roles.IsUserInRole(roleName)` 메서드에](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx)대 한 호출로 바꿀 수 있습니다. 이 예제에서는 역할 API를 직접 사용 하는 것 보다 효율적 이기 때문에 principal 개체의 `IsInRole(roleName)` 메서드를 사용 하기로 결정 했습니다. 이 자습서의 앞부분에서 사용자의 역할을 쿠키에 캐시 하도록 역할 관리자를 구성 했습니다. 이 캐시 된 쿠키 데이터는 주 서버의 `IsInRole(roleName)` 메서드가 호출 되는 경우에만 사용 됩니다. 역할 API에 대 한 직접 호출에는 항상 역할 저장소에 대 한 마이그레이션이 포함 됩니다. 역할이 쿠키에 캐시 되지 않은 경우에도 요청 하는 동안 처음으로 호출 될 때 해당 결과를 캐시 하기 때문에 주 개체의 `IsInRole(roleName)` 메서드를 호출 하는 것이 더 효율적입니다. 반면에 역할 API는 캐싱을 수행 하지 않습니다. `RowCreated` 이벤트는 GridView의 모든 행에 대해 한 번만 발생 하기 때문에 `User.IsInRole(roleName)`를 사용 하면 역할 저장소에 대 한 한 번의 이동이 포함 되지만, `Roles.IsUserInRole(roleName)` *n* 번의 이동이 필요 합니다. 여기서 *n* 은 그리드에 표시 되는 사용자 계정 수입니다.

이 페이지를 방문 하는 사용자가 Administrators 또는 감독자 역할에 있는 경우 편집 단추의 `Visible` 속성이 `true`로 설정 됩니다. 그렇지 않으면 `false`로 설정 됩니다. 사용자가 관리자 역할에 있는 경우에만 Delete 단추의 `Visible` 속성이 `true`로 설정 됩니다.

브라우저를 통해이 페이지를 테스트 합니다. 페이지를 익명 방문자로 방문 하거나 감독자 또는 관리자가 아닌 사용자로 방문 하는 경우 CommandField는 비어 있습니다. 여전히 존재 하지만 편집 또는 삭제 단추가 없는 씬 슬라이버로 사용 됩니다.

> [!NOTE]
> 비관리자 및 비관리자가 페이지를 방문 하는 경우 CommandField를 모두 숨길 수 있습니다. 독자를 위한 연습으로 남겨 둡니다.

[비 감독자 및 비관리자에 대해 편집 및 삭제 단추가 숨겨진 ![](role-based-authorization-cs/_static/image38.png)](role-based-authorization-cs/_static/image37.png)

**그림 13**: 비 감독자 및 비관리자에 대해 편집 및 삭제 단추가 숨겨짐 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image39.png))

감독자 역할 (관리자 역할에는 아님)에 속하는 사용자가 방문 하는 경우에만 편집 단추를 볼 수 있습니다.

[![편집 단추를 감독자에 게 사용할 수 있는 동안에는 삭제 단추가 숨겨집니다.](role-based-authorization-cs/_static/image41.png)](role-based-authorization-cs/_static/image40.png)

**그림 14**: 감독자에 대해 편집 단추를 사용할 수 있는 경우 삭제 단추가 숨겨집니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image42.png)).

그리고 관리자가 방문 하는 경우 편집 및 삭제 단추에 대 한 액세스 권한이 있습니다.

[편집 및 삭제 단추 ![관리자만 사용할 수 있음](role-based-authorization-cs/_static/image44.png)](role-based-authorization-cs/_static/image43.png)

**그림 15**: 관리자만 편집 및 삭제 단추를 사용할 수 있음 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image45.png))

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>3 단계: 클래스 및 메서드에 역할 기반 권한 부여 규칙 적용

2 단계에서는 감독자 및 관리자 역할의 사용자에 대 한 편집 기능을 제한 하 고 관리자만 기능을 삭제 합니다. 이는 프로그래밍 기법을 통해 권한이 없는 사용자에 대해 연결 된 사용자 인터페이스 요소를 숨겨서 수행 했습니다. 이러한 측정값은 권한 없는 사용자가 권한 있는 작업을 수행할 수 없음을 보장 하지 않습니다. 나중에 추가 되거나 권한이 없는 사용자에 대해 숨기지 않는 사용자 인터페이스 요소가 있을 수 있습니다. 또는 해커는 ASP.NET 페이지에서 원하는 메서드를 실행 하는 다른 방법을 발견할 수 있습니다.

권한이 없는 사용자가 특정 기능의 특정 부분에 액세스할 수 없도록 하는 쉬운 방법은 해당 클래스 또는 메서드를 [`PrincipalPermission` 특성](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx)으로 데코레이팅 하는 것입니다. .NET 런타임이 클래스를 사용 하거나 해당 메서드 중 하나를 실행 하는 경우 현재 보안 컨텍스트에 권한이 있는지 확인 합니다. `PrincipalPermission` 특성은 이러한 규칙을 정의할 수 있는 메커니즘을 제공 합니다.

<a id="_msoanchor_9"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서에서 `PrincipalPermission` 특성을 다시 사용 하는 방법을 살펴보았습니다. 구체적으로, GridView의 `SelectedIndexChanged` 및 `RowDeleting` 이벤트 처리기를 데코레이팅하는 방법에 대해 살펴보았습니다 .이는 인증 된 사용자 및 Tito에 의해서만 실행 될 수 있도록 합니다. `PrincipalPermission` 특성은 역할에 대해서만 작동 합니다.

GridView의 `RowUpdating` 및 `RowDeleting` 이벤트 처리기에 `PrincipalPermission` 특성을 사용 하 여 권한이 없는 사용자에 대 한 실행을 금지 하는 방법을 살펴보겠습니다. 각 함수 정의 위에 적절 한 특성을 추가 하기만 하면 됩니다.

[!code-csharp[Main](role-based-authorization-cs/samples/sample13.cs)]

`RowUpdating` 이벤트 처리기에 대 한 특성은 Administrators 또는 감독자 역할의 사용자만 이벤트 처리기를 실행할 수 있도록 지시 합니다. 여기서 `RowDeleting` 이벤트 처리기의 특성은 관리자 역할의 사용자만 실행 하도록 제한 합니다.

> [!NOTE]
> `PrincipalPermission` 특성은 `System.Security.Permissions` 네임 스페이스에서 클래스로 표현 됩니다. 이 네임 스페이스를 가져오려면 코드 뒤 클래스 파일의 맨 위에 `using System.Security.Permissions` 문을 추가 해야 합니다.

관리자가 아닌 관리자가 `RowDeleting` 이벤트 처리기를 실행 하려고 하거나 비관리자 또는 비관리자가 `RowUpdating` 이벤트 처리기를 실행 하려고 하는 경우 .NET 런타임에서 `SecurityException`을 발생 시킵니다.

[![보안 컨텍스트가 메서드를 실행할 수 있는 권한이 없으면 SecurityException이 Throw 됩니다.](role-based-authorization-cs/_static/image47.png)](role-based-authorization-cs/_static/image46.png)

**그림 16**: 보안 컨텍스트에 메서드를 실행할 수 있는 권한이 없는 경우 `SecurityException`이 throw 됩니다 ([전체 크기 이미지를 보려면 클릭](role-based-authorization-cs/_static/image48.png)).

ASP.NET 페이지 외에도 많은 응용 프로그램에는 비즈니스 논리 및 데이터 액세스 계층과 같은 다양 한 계층을 포함 하는 아키텍처가 있습니다. 이러한 계층은 일반적으로 클래스 라이브러리로 구현 되며 비즈니스 논리 및 데이터 관련 기능을 수행 하기 위한 구현 클래스와 메서드를 제공 합니다. `PrincipalPermission` 특성은 이러한 계층에 권한 부여 규칙을 적용 하는 데에도 유용 합니다.

`PrincipalPermission` 특성을 사용 하 여 클래스 및 메서드에 대 한 권한 부여 규칙을 정의 하는 방법에 대 한 자세한 내용은 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목 [`PrincipalPermissionAttributes`를 사용 하 여 비즈니스 및 데이터 계층에 권한 부여 규칙 추가 ](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)를 참조 하세요.

## <a name="summary"></a>요약

이 자습서에서는 사용자의 역할에 따라 거칠게 및 미세 수준 권한 부여 규칙을 지정 하는 방법을 살펴보았습니다. ASP. NET의 URL 권한 부여 기능을 사용 하면 페이지 개발자가 페이지에 대 한 액세스가 허용 되거나 거부 되는 id를 지정할 수 있습니다. <a id="_msoanchor_10"> </a> [*사용자 기반 권한 부여*](../membership/user-based-authorization-cs.md) 자습서에서 살펴본 것 처럼 URL 권한 부여 규칙은 사용자를 기준으로 적용할 수 있습니다. 또한이 자습서의 1 단계에서 살펴본 것 처럼 역할 별로 적용할 수 있습니다.

미세 수준 권한 부여 규칙은 선언적으로 또는 프로그래밍 방식으로 적용할 수 있습니다. 2 단계에서는 LoginView 컨트롤의 RoleGroups 기능을 사용 하 여 방문한 사용자의 역할에 따라 다른 출력을 렌더링 하는 방법을 살펴보았습니다. 또한 사용자가 특정 역할에 속하는지 여부를 프로그래밍 방식으로 확인 하는 방법과 페이지의 기능을 적절 하 게 조정 하는 방법도 살펴보았습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [`PrincipalPermissionAttributes`를 사용 하 여 비즈니스 및 데이터 계층에 권한 부여 규칙 추가](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [ASP.NET 2.0의 멤버 자격, 역할 및 프로필 검사: 역할 작업](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [ASP.NET 2.0에 대 한 보안 질문 목록](https://msdn.microsoft.com/library/ms998375.aspx)
- [`<roleManager>` 요소에 대 한 기술 설명서](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>작성자 정보

Scott Mitchell는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 *[24 시간 이내에 ASP.NET 2.0을 sams teach yourself](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 것입니다. Scott은 [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별 해 주셔서 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 Suchi Banerjee 및 Teresa Murphy를 포함 합니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](assigning-roles-to-users-cs.md)
> [다음](creating-and-managing-roles-vb.md)
