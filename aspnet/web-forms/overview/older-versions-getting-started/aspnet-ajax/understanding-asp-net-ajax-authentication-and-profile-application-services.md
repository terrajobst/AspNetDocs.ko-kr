---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
title: ASP.NET AJAX 인증 및 프로필 애플리케이션 서비스 이해 | Microsoft Docs
author: scottcate
description: 인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, 사용자 지정 사용자를 허용 하는 게이트웨이 서비스 ...
ms.author: riande
ms.date: 03/14/2008
ms.assetid: 6ab4efb6-aab6-45ac-ad2c-bdec5848ef9e
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-authentication-and-profile-application-services
msc.type: authoredcontent
ms.openlocfilehash: cab9acb1ffd75cca87f6c575a6abdd000235828e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635685"
---
# <a name="understanding-aspnet-ajax-authentication-and-profile-application-services"></a>ASP.NET AJAX 인증 및 프로필 애플리케이션 서비스 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial03_MSAjax_ASP.NET_Services_cs.pdf)

> 인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, ASP.NET에서 제공 하는 사용자 지정 사용자 프로필을 허용 하는 게이트웨이 서비스입니다. ASP.NET AJAX 인증 서비스의 사용은 표준 ASP.NET Forms 인증과 호환 되므로 현재 폼 인증을 사용 하는 응용 프로그램 (예: 로그인 제어)은 AJAX 인증 서비스로 업그레이드 하 여 중단 되지 않습니다.

## <a name="introduction"></a>소개

.NET Framework 3.5의 일부로 Microsoft에서 자동으로 환경 업그레이드를 제공 합니다. 새 개발 환경을 사용할 수 있을 뿐 아니라 새로운 LINQ (통합 언어 쿼리) 기능 및 기타 언어 향상 기능을 곧 사용할 수 있습니다. 또한 다른 도구 집합의 일부 익숙한 기능 (특히 ASP.NET AJAX 확장)은 .NET Framework 기본 클래스 라이브러리의 최고 수준의 멤버로 포함 됩니다. 이러한 확장을 통해 전체 페이지를 새로 고치지 않고도 페이지의 부분 렌더링, 클라이언트 스크립트를 통해 웹 서비스에 액세스 하는 기능 (ASP.NET 프로 파일링 API 포함) 및 광범위 한 클라이언트 쪽 API를 비롯 한 다양 한 새 리치 클라이언트 기능을 사용할 수 있습니다. ASP.NET 서버 쪽 컨트롤 집합에 표시 되는 많은 컨트롤 스키마를 미러링 하도록 디자인 되었습니다.

이 백서에서는 ASP.NET 프로 파일링 및 폼 인증 서비스를 구현 하 고 사용 하는 방법을 살펴봅니다. AJAX 확장 Microsoft ASP.NET AJAX 확장을 사용 하면 폼 인증을 쉽게 지원 하 고 프로 파일링 서비스는 웹 서비스 프록시 스크립트를 통해 노출 됩니다. AJAX 확장은 AuthenticationServiceManager 클래스를 통한 사용자 지정 인증도 지원 합니다.

이 백서는 Visual Studio 2008의 베타 2 릴리스와 .NET Framework 3.5을 기반으로 합니다. 또한이 백서에서는 visual Web Developer Express가 아닌 Visual Studio 2008 Beta 2를 사용 하 고 visual Studio의 사용자 인터페이스에 따라 연습을 제공 한다고 가정 합니다. 일부 코드 샘플은 Visual Web Developer Express에서 사용할 수 없는 프로젝트 템플릿을 활용할 수 있습니다.

## <a name="profiles-and-authentication"></a>*프로필 및 인증*

Microsoft ASP.NET 프로필 및 인증 서비스는 ASP.NET Forms 인증 시스템에서 제공 되며 ASP.NET의 표준 구성 요소입니다. ASP.NET AJAX 확장은 클라이언트 AJAX 라이브러리의 Sys. Services 네임 스페이스 아래에서 매우 간단한 모델을 통해 스크립트 프록시를 통해 이러한 서비스에 대 한 스크립트 액세스를 제공 합니다.

인증 서비스를 통해 사용자는 인증 쿠키를 수신 하기 위해 자격 증명을 제공할 수 있으며, ASP.NET에서 제공 하는 사용자 지정 사용자 프로필을 허용 하는 게이트웨이 서비스입니다. ASP.NET AJAX 인증 서비스의 사용은 표준 ASP.NET Forms 인증과 호환 되므로 현재 폼 인증을 사용 하는 응용 프로그램 (예: 로그인 제어)은 AJAX 인증 서비스로 업그레이드 하 여 중단 되지 않습니다.

프로필 서비스를 사용 하면 인증 서비스에서 제공 하는 멤버 자격에 따라 사용자 데이터를 자동으로 통합 하 고 저장할 수 있습니다. 저장 된 데이터는 web.config 파일에 의해 지정 되 고 다양 한 프로 파일링 서비스 공급자가 데이터 관리를 처리 합니다. 인증 서비스와 마찬가지로 AJAX 프로필 서비스는 표준 ASP.NET profile 서비스와 호환 되므로 ASP.NET Profile 서비스의 기능을 통합 하는 페이지는 AJAX 지원을 포함 하 여 중단 되어서는 안 됩니다.

ASP.NET 인증 및 프로 파일링 서비스를 응용 프로그램에 통합 하는 것은이 백서에서 다루지 않습니다. 항목에 대 한 자세한 내용은 MSDN Library 참조 문서 [https://msdn.microsoft.com/library/tw292whz.aspx](https://msdn.microsoft.com/library/tw292whz.aspx)에서 멤버 자격을 사용 하 여 사용자 관리를 참조 하세요. ASP.NET에는 ASP.NET 멤버 자격에 대 한 기본 인증 서비스 공급자 인 SQL Server를 사용 하 여 멤버 자격을 자동으로 설정 하는 유틸리티도 포함 되어 있습니다. 자세한 내용은 [https://msdn.microsoft.com/library/ms229862(vs.80).aspx](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)에서 ASP.NET SQL Server 등록 도구 (Aspnet\_ regsql .exe) 문서를 참조 하세요.

## <a name="using-the-aspnet-ajax-authentication-service"></a>*ASP.NET AJAX 인증 서비스 사용*

ASP.NET AJAX 인증 서비스를 web.config 파일에서 사용 하도록 설정 해야 합니다.

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample1.xml)]

인증 서비스를 사용 하려면 ASP.NET Forms 인증을 사용 하도록 설정 해야 하며 클라이언트 브라우저에서 쿠키를 사용 하도록 설정 해야 합니다. 쿠키가 없는 세션에는 URL 매개 변수가 필요 하므로 스크립트는 쿠키 없는 세션을 활성화할 수 없습니다.

AJAX 인증 서비스를 사용 하도록 설정 하 고 구성 하면 클라이언트 스크립트에서 해당 개체를 즉시 활용할 수 있습니다. 기본적으로 클라이언트 스크립트는 `login` 메서드와 `isLoggedIn` 속성을 활용 하려고 합니다. 다 수의 매개 변수를 받아들일 수 있는 login 메서드의 기본값을 제공 하는 몇 가지 속성이 있습니다.

*Sys.debug 서비스 멤버*

*로그인 방법:*

Login () 메서드는 사용자의 자격 증명을 인증 하는 요청을 시작 합니다. 이 메서드는 비동기적 이며 실행을 차단 하지 않습니다.

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| userName | 필수 인증할 사용자 이름입니다. |
| 암호 | 선택 사항입니다. 기본값은 null입니다. 사용자의 암호입니다. |
| isPersistent | 선택 사항입니다 (기본값은 false). 사용자의 인증 쿠키를 세션 간에 유지할지 여부를 지정 합니다. False 이면 브라우저가 닫히거나 세션이 만료 되 면 사용자가 로그 아웃 합니다. |
| redirectUrl | 선택 사항입니다. 기본값은 null입니다. 인증에 성공 하면 브라우저를 리디렉션할 URL입니다. 이 매개 변수가 null 또는 빈 문자열인 경우 리디렉션이 발생 하지 않습니다. |
| customInfo | 선택 사항입니다. 기본값은 null입니다. 이 매개 변수는 현재 사용 되지 않으며 나중에 사용 하도록 예약 되어 있습니다. |
| loginCompletedCallback | 선택 사항입니다. 기본값은 null입니다. 로그인이 성공적으로 완료 되었을 때 호출할 함수입니다. 지정 된 경우이 매개 변수는 defaultLoginCompleted 속성을 재정의 합니다. |
| failedCallback | 선택 사항입니다. 기본값은 null입니다. 로그인이 실패 했을 때 호출할 함수입니다. 지정 된 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다. |
| userContext | 선택 사항입니다. 기본값은 null입니다. 콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다. |

*반환 값:*

이 함수에는 반환 값이 포함 되지 않습니다. 그러나이 함수에 대 한 호출이 완료 되 면 많은 동작이 포함 됩니다.

- `redirectUrl` 매개 변수가 null 또는 빈 문자열이 아닌 경우 현재 페이지가 새로 고쳐지고 변경 됩니다.
- 그러나 매개 변수가 null 이거나 빈 문자열인 경우에는 `loginCompletedCallback` 매개 변수 또는 `defaultLoginCompletedCallback` 속성이 호출 됩니다.
- 웹 서비스에 대 한 호출이 실패 하면 `defaultFailedCallback` 속성의 `failedCallback` 매개 변수가 호출 됩니다.

*로그 아웃 방법:*

Logout () 메서드는 자격 증명 쿠키를 제거 하 고 웹 응용 프로그램에서 현재 사용자를 로그 아웃 합니다.

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| redirectUrl | 선택 사항입니다. 기본값은 null입니다. 인증에 성공 하면 브라우저를 리디렉션할 URL입니다. 이 매개 변수가 null 또는 빈 문자열인 경우 리디렉션이 발생 하지 않습니다. |
| logoutCompletedCallback | 선택 사항입니다. 기본값은 null입니다. 로그 아웃이 성공적으로 완료 되었을 때 호출할 함수입니다. 지정 된 경우이 매개 변수는 defaultLogoutCompleted 속성을 재정의 합니다. |
| failedCallback | 선택 사항입니다. 기본값은 null입니다. 로그인이 실패 했을 때 호출할 함수입니다. 지정 된 경우이 매개 변수는 defaultFailedCallback 속성을 재정의 합니다. |
| userContext | 선택 사항입니다. 기본값은 null입니다. 콜백 함수에 전달 되어야 하는 사용자 지정 사용자 컨텍스트 데이터입니다. |

*반환 값:*

이 함수에는 반환 값이 포함 되지 않습니다. 그러나이 함수에 대 한 호출이 완료 되 면 많은 동작이 포함 됩니다.

- `redirectUrl` 매개 변수가 null 또는 빈 문자열이 아닌 경우 현재 페이지가 새로 고쳐지고 변경 됩니다.
- 그러나 매개 변수가 null 이거나 빈 문자열인 경우에는 `logoutCompletedCallback` 매개 변수 또는 `defaultLogoutCompletedCallback` 속성이 호출 됩니다.
- 웹 서비스에 대 한 호출이 실패 하면 `defaultFailedCallback` 속성의 `failedCallback` 매개 변수가 호출 됩니다.

*defaultFailedCallback 속성 (get, set):*

이 속성은 웹 서비스와의 통신에 실패 한 경우 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample2.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| 오류 | 오류 정보를 지정 합니다. |
| userContext | Login 또는 logout 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLoginCompletedCallback 속성 (get, set):*

이 속성은 로그인 웹 서비스 호출이 완료 될 때 호출 되어야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample3.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| 유효한 자격 증명 | 사용자가 유효한 자격 증명을 제공 했는지 여부를 지정 합니다. 사용자가 성공적으로 로그인 한 경우 `true` 합니다. 그렇지 않으면 `false`합니다. |
| userContext | 로그인 함수가 호출 될 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLogoutCompletedCallback 속성 (get, set):*

이 속성은 로그 아웃 웹 서비스 호출이 완료 될 때 호출 되어야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample4.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| result | 이 매개 변수는 항상 `null`됩니다. 나중에 사용 하도록 예약 되어 있습니다. |
| userContext | 로그인 함수가 호출 될 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*isLoggedIn 속성 (get):*

이 속성은 사용자의 현재 인증 상태를 가져옵니다. 페이지 요청 중에 ScriptManager 개체에 의해 설정 됩니다.

이 속성은 사용자가 현재 로그인 한 경우 `true`를 반환 합니다. 그렇지 않으면 `false`을 반환 합니다.

*path 속성 (get, set):*

이 속성은 인증 웹 서비스의 위치를 프로그래밍 방식으로 결정 합니다. 이를 사용 하 여 기본 인증 공급자를 재정의 하 고 하나는 ScriptManager 컨트롤의 AuthenticationService 자식 노드의 Path 속성에서 선언적으로 설정할 수 있습니다. 자세한 내용은 사용자 지정 인증 서비스 공급자 사용을 참조 하세요. 항목을 참조 하십시오.

기본 인증 서비스의 위치는 변경 되지 않습니다. 그러나 ASP.NET AJAX를 사용 하면 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.

또한이 속성을 현재 사이트에서 스크립트 요청을 보내는 값으로 설정 하면 안 됩니다. 현재 응용 프로그램은 인증 자격 증명을 받지 않으므로 쓸모가 없습니다. 또한 기본 AJAX 기술은 교차 사이트 요청을 게시 해서는 안 되며 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.

이 속성은 인증 웹 서비스에 대 한 경로를 나타내는 `String` 개체입니다.

*timeout 속성 (get, set):*

이 속성은 로그인 요청이 실패 했다고 가정 하기 전에 인증 서비스를 대기 하는 시간을 결정 합니다. 호출이 완료 될 때까지 대기 하는 동안 제한 시간이 만료 되 면 요청-실패 콜백이 호출 되 고 호출이 완료 되지 않습니다.

이 속성은 인증 서비스의 결과를 대기 하는 시간 (밀리초)을 나타내는 `Number` 개체입니다.

*코드 샘플: 인증 서비스에 로그인*

다음 태그는 AuthenticationService 클래스의 login 및 logout 메서드에 대 한 간단한 스크립트 호출을 포함 하는 예제 ASP.NET 페이지입니다.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample5.aspx)]

## <a name="accessing-aspnet-profiling-data-via-ajax"></a>AJAX를 통해 ASP.NET 프로 파일링 데이터 액세스

또한 ASP.NET 프로 파일링 서비스는 ASP.NET AJAX 확장을 통해 노출 됩니다. ASP.NET 프로 파일링 서비스는 사용자 데이터를 저장 하 고 검색할 수 있는 풍부 하 고 세부적인 API를 제공 하므로이는 뛰어난 생산성 도구입니다.

프로필 서비스를 web.config에서 사용 하도록 설정 해야 합니다. 기본적으로는 그렇지 않습니다. 이렇게 하려면 web.config에서 `profileService` 자식 요소가 enabled = true로 지정 되었는지 확인 하 고 다음과 같이 읽거나 쓸 수 있는 속성을 지정 했는지 확인 합니다.

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample6.xml)]

또한 프로필 서비스를 구성 해야 합니다. 프로 파일링 서비스의 구성은이 백서에서 다루지 않지만 프로필 구성 설정에 정의 된 그룹은 그룹 이름의 하위 속성으로 액세스할 수 있다는 점에 유의 해야 합니다. 예를 들어, 다음 프로필 섹션을 지정 합니다.

[!code-xml[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample7.xml)]

클라이언트 스크립트는 ProfileService 클래스의 속성 필드의 속성으로 Name, Address. 줄 1, Line2, address. City 및 BackgroundColor에 액세스할 수 있습니다.

AJAX 프로 파일링 서비스가 구성 되 면 페이지에서 즉시 사용할 수 있게 됩니다. 하지만 사용 하기 전에 한 번 로드 해야 합니다.

*ProfileService 멤버*

*속성 필드:*

속성 필드는 모든 구성 된 프로필 데이터를 점-연산자 이름 규칙에서 참조할 수 있는 자식 속성으로 노출 합니다. 속성 그룹의 자식인 속성을 GroupName. PropertyName 이라고 합니다. 위에서 제공한 예제 프로필 구성에서 사용자의 상태를 가져오려면 다음 식별자를 사용할 수 있습니다.

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample8.cs)]

*로드 방법:*

서버에서 선택한 목록 또는 모든 속성을 로드 합니다.

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| propertyNames | 선택 사항입니다. 기본값은 null입니다. 서버에서 로드 되는 속성입니다. |
| loadCompletedCallback | 선택 사항입니다. 기본값은 null입니다. 로드가 완료 될 때 호출할 함수입니다. |
| failedCallback | 선택 사항입니다. 기본값은 null입니다. 오류가 발생 하는 경우 호출할 함수입니다. |
| userContext | 선택 사항입니다. 기본값은 null입니다. 콜백 함수에 전달할 컨텍스트 정보입니다. |

Load 함수에는 반환 값이 없습니다. 호출이 성공적으로 완료 되 면 `loadCompletedCallback` 매개 변수 또는 `defaultLoadCompletedCallback` 속성 중 하나를 호출 합니다. 호출이 실패 했거나 제한 시간이 만료 되 면 `failedCallback` 매개 변수 또는 `defaultFailedCallback` 속성이 호출 됩니다.

`propertyNames` 매개 변수를 지정 하지 않으면 모든 읽기 구성 속성이 서버에서 검색 됩니다.

*저장 방법:*

Save () 메서드는 지정 된 속성 목록 (또는 모든 속성)을 사용자의 ASP.NET 프로필에 저장 합니다.

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| propertyNames | 선택 사항입니다. 기본값은 null입니다. 서버에 저장 되는 속성입니다. |
| saveCompletedCallback | 선택 사항입니다. 기본값은 null입니다. 저장이 완료 될 때 호출할 함수입니다. |
| failedCallback | 선택 사항입니다. 기본값은 null입니다. 오류가 발생 하는 경우 호출할 함수입니다. |
| userContext | 선택 사항입니다. 기본값은 null입니다. 콜백 함수에 전달할 컨텍스트 정보입니다. |

저장 함수에 반환 값이 없습니다. 호출이 성공적으로 완료 되 면 `saveCompletedCallback` 매개 변수 또는 `defaultSaveCompletedCallback` 속성 중 하나를 호출 합니다. 호출이 실패 했거나 제한 시간이 만료 된 경우 `failedCallback` 또는 `defaultFailedCallback` 속성이 호출 됩니다.

`propertyNames` 매개 변수가 null 이면 모든 프로필 속성이 서버에 전송 되 고 서버는 저장할 수 있는 속성과 수행할 수 없는 속성을 결정 합니다.

*defaultFailedCallback 속성 (get, set):*

이 속성은 웹 서비스와의 통신에 실패 한 경우 호출 해야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample9.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| 오류 | 오류 정보를 지정 합니다. |
| userContext | Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultSaveCompleted 속성 (get, set):*

이 속성은 사용자의 프로필 데이터 저장이 완료 될 때 호출 되어야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample10.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| numPropsSaved | 저장 된 속성의 수를 지정 합니다. |
| userContext | Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*defaultLoadCompleted 속성 (get, set):*

이 속성은 사용자의 프로필 데이터 로드가 완료 될 때 호출 되어야 하는 함수를 지정 합니다. 대리자 (또는 함수 참조)를 받아야 합니다.

이 속성에 지정 된 함수 참조에는 다음 서명이 있어야 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample11.js)]

*변수의*

| **매개 변수 이름** | **임을** |
| --- | --- |
| numPropsLoaded | 로드 되는 속성 수를 지정 합니다. |
| userContext | Load 또는 save 함수를 호출할 때 제공 되는 사용자 컨텍스트 정보를 지정 합니다. |
| methodName | 호출 메서드의 이름입니다. |

*path 속성 (get, set):*

이 속성은 프로필 웹 서비스의 위치를 프로그래밍 방식으로 결정 합니다. 이를 사용 하 여 기본 프로필 서비스 공급자를 재정의 하 고 ScriptManager 컨트롤의 ProfileService 자식 노드의 Path 속성에서 set을 선언적으로 지정할 수 있습니다.

기본 프로필 서비스의 위치는 변경 되지 않습니다. 그러나 ASP.NET AJAX를 사용 하면 ASP.NET AJAX 인증 서비스 프록시와 동일한 클래스 인터페이스를 제공 하는 웹 서비스의 위치를 지정할 수 있습니다.

또한이 속성을 현재 사이트에서 스크립트 요청을 보내는 값으로 설정 하면 안 됩니다. 기술 기본 AJAX는 교차 사이트 요청을 게시 해서는 안 되며 클라이언트 브라우저에서 보안 예외를 생성할 수 있습니다.

이 속성은 프로필 웹 서비스에 대 한 경로를 나타내는 `String` 개체입니다.

*timeout 속성 (get, set):*

이 속성은 로드 또는 저장 요청이 실패 했다고 가정 하기 전에 프로필 서비스를 대기 하는 시간을 결정 합니다. 호출이 완료 될 때까지 대기 하는 동안 제한 시간이 만료 되 면 요청-실패 콜백이 호출 되 고 호출이 완료 되지 않습니다.

이 속성은 프로필 서비스의 결과를 대기 하는 시간 (밀리초)을 나타내는 `Number` 개체입니다.

*코드 샘플: 페이지 로드 시 프로필 데이터 로드*

다음 코드에서는 사용자가 인증 되었는지 여부를 확인 하 고,이 경우 사용자의 기본 배경색을 페이지의 기본 배경색으로 로드 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample12.js)]

## <a name="using-a-custom-authentication-service-provider"></a>*사용자 지정 인증 서비스 공급자 사용*

ASP.NET AJAX 확장을 사용 하면 사용자 지정 웹 서비스를 통해 기능을 노출 하 여 사용자 지정 스크립트 인증 서비스 공급자를 만들 수 있습니다. 웹 서비스는 사용 하기 위해 `Login` 및 `Logout`의 두 메서드를 노출 해야 합니다. 및 이러한 메서드는 기본 ASP.NET AJAX 인증 웹 서비스와 동일한 메서드 서명으로 지정 해야 합니다.

사용자 지정 웹 서비스를 만든 후에는 페이지에서 선언적으로 또는 코드에서 프로그래밍 방식으로 또는 클라이언트 스크립트를 통해 경로를 지정 해야 합니다.

*경로를 선언적으로 설정 하려면 다음을 수행 합니다.*

경로를 선언적으로 설정 하려면 ASP.NET 페이지에 ScriptManager 개체의 AuthenticationService 자식을 포함 합니다.

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample13.aspx)]

*코드에서 경로를 설정 하려면:*

경로를 프로그래밍 방식으로 설정 하려면 스크립트 관리자의 인스턴스를 통해 경로를 지정 합니다.

[!code-csharp[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample14.cs)]

*스크립트에서 경로를 설정 하려면:*

스크립트에서 프로그래밍 방식으로 경로를 설정 하려면 AuthenticationService 클래스의 `path` 속성을 활용 합니다.

[!code-javascript[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample15.js)]

*사용자 지정 인증용 샘플 웹 서비스*

[!code-aspx[Main](understanding-asp-net-ajax-authentication-and-profile-application-services/samples/sample16.aspx)]

## <a name="summary"></a>요약

ASP.NET services-특히 프로 파일링, 멤버 자격 및 인증 서비스는 클라이언트 브라우저에서 JavaScript에 쉽게 노출 됩니다. 이를 통해 개발자는 UpdatePanels와 같은 컨트롤에 의존 하지 않고 클라이언트 쪽 코드를 인증 메커니즘과 원활 하 게 통합할 수 있습니다. 웹 구성 설정을 활용 하 여 클라이언트 에서도 프로필 데이터를 보호할 수 있습니다. 기본적으로 사용할 수 있는 데이터가 없으며 개발자는 프로필 속성을 옵트인 (opt in) 해야 합니다.

또한 개발자는 동일한 메서드 서명을 사용 하 여 간단한 웹 서비스 구현을 만들어 이러한 내장 ASP.NET 서비스에 대 한 사용자 지정 스크립트 공급자를 만들 수 있습니다. 이러한 기술을 지원 하면 풍부한 클라이언트 응용 프로그램의 개발을 간소화 하는 동시에 개발자에 게 특정 요구를 충족 하는 다양 한 유연성을 제공 합니다.

## <a name="bio"></a>*약력*

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [이전](understanding-asp-net-ajax-updatepanel-triggers.md)
> [다음](understanding-asp-net-ajax-localization.md)
