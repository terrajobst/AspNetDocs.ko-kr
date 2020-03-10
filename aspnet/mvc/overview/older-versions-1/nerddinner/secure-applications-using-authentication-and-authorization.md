---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 인증 및 권한 부여를 사용 하 여 응용 프로그램 보호 | Microsoft Docs
author: microsoft
description: 9 단계에서는 사용자가 사이트에 등록 하 고 로그인 하 여 만들 수 있도록 하는 인증 및 권한 부여를 추가 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486425"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>인증 및 권한 부여를 사용하여 애플리케이션 보호

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 9 단계입니다.
> 
> 9 단계에서는 사용자가 새 dinners를 만들기 위해 사이트에 등록 하 고 로그인 해야 하며 dinner a를 호스트 하는 사용자만 나중에 편집할 수 있도록 사용자가 사이트를 등록 하 고 로그인 해야 하는 경우에 인증 및 권한 부여를 추가 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner Step 9: 인증 및 권한 부여

이제, microsoft의 사용자가 사이트를 방문 하는 모든 사용자에 게 저녁의 세부 정보를 만들고 편집할 수 있는 권한을 부여 합니다. 사용자가 새 dinners를 만들기 위해 사이트에 등록 하 고 로그인 해야 하 고 저녁을 호스트 하는 사용자만 나중에 편집할 수 있도록 제한을 추가 하 여이를 변경해 보겠습니다.

이를 사용 하도록 설정 하려면 인증 및 권한 부여를 사용 하 여 응용 프로그램을 보호 합니다.

### <a name="understanding-authentication-and-authorization"></a>인증 및 권한 부여 이해

*인증은* 응용 프로그램에 액세스 하는 클라이언트의 id를 식별 하 고 유효성을 검사 하는 프로세스입니다. 좀 더 간단 하 게 말해 최종 사용자가 웹 사이트를 방문할 때 사용자를 식별 하는 것입니다. ASP.NET는 브라우저 사용자를 인증 하는 여러 방법을 지원 합니다. 인터넷 웹 응용 프로그램의 경우 사용 되는 가장 일반적인 인증 방법을 "폼 인증" 이라고 합니다. 폼 인증을 통해 개발자는 응용 프로그램 내에서 HTML 로그인 양식을 작성 한 후 데이터베이스 또는 다른 암호 자격 증명 저장소에 대해 최종 사용자가 제출한 사용자 이름/암호의 유효성을 검사할 수 있습니다. 사용자 이름/암호 조합이 올바르면 개발자가 ASP.NET에 게 암호화 된 HTTP 쿠키를 발급 하 여 향후 요청에서 사용자를 식별 하도록 요청할 수 있습니다. Microsoft는 동료 Ddinner 응용 프로그램에서 폼 인증을 사용 합니다.

*권한 부여* 는 인증 된 사용자에 게 특정 URL/리소스에 대 한 액세스 권한이 있는지 또는 일부 동작을 수행할 권한이 있는지를 확인 하는 프로세스입니다. 예를 들어, 내 동료 Ddinner 응용 프로그램 내에서 로그인 한 사용자만 */Dinners/Create* URL에 액세스 하 고 새 Dinners을 만들 수 있도록 권한을 부여 하려고 합니다. 또한 식사를 호스트 하는 사용자만 편집할 수 있도록 권한 부여 논리를 추가 하 고 다른 모든 사용자에 대 한 편집 액세스를 거부할 수 있습니다.

### <a name="forms-authentication-and-the-accountcontroller"></a>폼 인증 및 AccountController

ASP.NET MVC에 대 한 기본 Visual Studio 프로젝트 템플릿은 새 ASP.NET MVC 응용 프로그램을 만들 때 폼 인증을 자동으로 활성화 합니다. 또한 미리 작성 된 계정 로그인 페이지 구현을 프로젝트에 자동으로 추가 하 여 사이트 내에서 보안을 매우 쉽게 통합할 수 있습니다.

기본 site.master 마스터 페이지는 사이트에 액세스 하는 사용자가 인증 되지 않은 경우 사이트의 오른쪽 위에 "로그온" 링크를 표시 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

"로그온" 링크를 클릭 하면 사용자가 */Srvlogon* URL로 이동 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

등록 하지 않은 방문자는 "등록" 링크를 클릭 하 여이 작업을 수행할 수 있습니다 .이 링크를 선택 하면 */Dl/dlurl* 로 이동 하 여 계정 세부 정보를 입력할 수 있습니다.

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

"등록" 단추를 클릭 하면 ASP.NET 멤버 자격 시스템 내에 새 사용자가 생성 되 고 폼 인증을 사용 하 여 사이트에 대해 사용자가 인증 됩니다.

사용자가 로그인 하면 site.master는 페이지의 오른쪽 위를 변경 하 여 "시작 [사용자 이름]!"을 출력 합니다. "로그온" 하는 대신 "로그 오프" 링크를 렌더링 합니다. "로그 오프" 링크를 클릭 하면 사용자가 로그 아웃 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

위의 로그인, 로그 아웃 및 등록 기능은 프로젝트를 만들 때 Visual Studio에서 프로젝트에 추가한 AccountController 클래스 내에서 구현 됩니다. AccountController의 UI는 \Views\Account 디렉터리 내에서 뷰 템플릿을 사용 하 여 구현 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

AccountController 클래스는 ASP.NET Forms 인증 시스템을 사용 하 여 암호화 된 인증 쿠키를 발급 하 고 ASP.NET Membership API를 사용 하 여 사용자 이름/암호를 저장 하 고 유효성을 검사 합니다. ASP.NET Membership API는 확장 가능 하며 모든 암호 자격 증명 저장소를 사용할 수 있도록 합니다. ASP.NET는 SQL database 내에 사용자 이름/암호를 저장 하거나 Active Directory 내에 저장 하는 기본 제공 멤버 자격 공급자 구현 기능을 제공 합니다.

프로젝트의 루트에 있는 "web.config" 파일을 열고 그 안에 있는 &lt;멤버 자격&gt; 섹션을 검색 하 여 팀에서 사용 해야 하는 멤버 자격 공급자를 구성할 수 있습니다. 프로젝트를 만들 때 추가 된 기본 web.config는 SQL 멤버 자격 공급자를 등록 하 고 "ApplicationServices" 라는 연결 문자열을 사용 하 여 데이터베이스 위치를 지정 하도록 구성 합니다.

Web.config 파일의 &lt;connectionStrings&gt; 섹션에 지정 된 기본 "ApplicationServices" 연결 문자열은 SQL Express를 사용 하도록 구성 됩니다. 이름이 "ASPNETDB.MDF" 인 SQL Express 데이터베이스를 가리킵니다. MDF "응용 프로그램의" App\_Data "디렉터리에 있습니다. 응용 프로그램 내에서 멤버 자격 API를 처음 사용 하는 경우이 데이터베이스가 존재 하지 않는 경우 ASP.NET는 자동으로 데이터베이스를 만들고 해당 데이터베이스 내에서 적절 한 멤버 자격 데이터베이스 스키마를 프로 비전 합니다.

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

SQL Express를 사용 하는 대신 전체 SQL Server 인스턴스를 사용 하거나 원격 데이터베이스에 연결 하려는 경우 web.config 파일 내에서 "ApplicationServices" 연결 문자열을 업데이트 하 고 적절 한 멤버 자격 스키마를 확인 해야 합니다. 가 가리키는 데이터베이스에 추가 되었습니다. \Windows\Microsoft.NET\Framework\v2.0.50727\ 디렉터리 내에서 "aspnet\_regsql" 유틸리티를 실행 하 여 멤버 자격 및 기타 ASP.NET 응용 프로그램 서비스에 대 한 적절 한 스키마를 데이터베이스에 추가할 수 있습니다.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>[권한 부여] 필터를 사용 하 여/Dinners/Create URL 권한 부여

이제는 코드를 작성 하 여 지 어 Ddinner 응용 프로그램에 대 한 보안 인증 및 계정 관리 구현을 사용할 필요가 없습니다. 사용자는 응용 프로그램에 새 계정을 등록 하 고 사이트의 로그인/로그 아웃을 수행할 수 있습니다.

이제 응용 프로그램에 권한 부여 논리를 추가 하 고 방문자의 인증 상태 및 사용자 이름을 사용 하 여 사이트 내에서 수행할 수 있는 작업을 제어할 수 있습니다. 먼저 DinnersController 클래스의 "만들기" 작업 메서드에 권한 부여 논리를 추가 합니다. 특히 */Dinners/Create* URL에 액세스 하는 사용자가 로그인 해야 합니다. 로그인 하지 않은 경우 로그인 페이지로 리디렉션하여 로그인 할 수 있습니다.

이 논리를 구현 하는 것은 매우 쉽습니다. 다음과 같이 만들기 작업 메서드에 [권한 부여] 필터 특성을 추가 하기만 하면 됩니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC는 작업 메서드에 선언적으로 적용할 수 있는 재사용 가능한 논리를 구현 하는 데 사용할 수 있는 "작업 필터"를 만드는 기능을 지원 합니다. [권한 부여] 필터는 ASP.NET MVC에서 제공 하는 기본 제공 작업 필터 중 하나 이며 개발자가 작업 메서드 및 컨트롤러 클래스에 권한 부여 규칙을 선언적으로 적용할 수 있도록 합니다.

위와 같이 매개 변수 없이 적용 하는 경우 [권한 부여] 필터는 동작 메서드 요청을 만드는 사용자에 게 로그인 해야 하는 것을 적용 하 고 브라우저를 로그인 URL로 자동으로 리디렉션합니다. 이 리디렉션 작업을 수행할 때 원래 요청 된 URL은 querystring 인수로 전달 됩니다 (예:/Account/dv? ReturnUrl =% 2fDinners% 2fCreate). 그러면 AccountController가 로그인 한 후 사용자를 원래 요청 된 URL로 다시 리디렉션합니다.

[권한 부여] 필터는 선택적으로 사용자를 로그인 하 고 허용 된 사용자 목록 또는 허용 된 보안 역할의 멤버에 로그인 하도록 요구 하는 데 사용할 수 있는 "사용자" 또는 "역할" 속성을 지정 하는 기능을 지원 합니다. 예를 들어 아래 코드에서는 두 개의 특정 사용자 "scottgu" 및 "billg"를 사용 하 여/Dinners/Create URL에 액세스할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

코드 내에 특정 사용자 이름을 포함 하는 것은 유지 관리 하기가 매우 용이 합니다. 더 나은 방법은 코드에서 확인 하는 상위 수준 "역할"을 정의한 다음 데이터베이스 또는 active directory 시스템을 사용 하 여 사용자를 역할에 매핑하는 것입니다 (실제 사용자 매핑 목록을 코드에서 외부에 저장할 수 있도록 함). ASP.NET에는 기본 제공 역할 관리 API 뿐만 아니라이 사용자/역할 매핑을 수행 하는 데 도움이 되는 역할 공급자의 기본 제공 집합 (SQL 및 Active Directory 포함)이 포함 되어 있습니다. 그런 다음 특정 "관리자" 역할 내의 사용자만/Dinners/Create URL에 액세스할 수 있도록 코드를 업데이트할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Dinners를 만들 때 User.Identity.Name 속성 사용

컨트롤러 기본 클래스에 노출 된 User.Identity.Name 속성을 사용 하 여 요청에 대해 현재 로그인 한 사용자의 사용자 이름을 검색할 수 있습니다.

이전에는 Create () 작업 메서드의 HTTP POST 버전을 구현 했을 때 Dinner a의 "HostedBy" 속성을 정적 문자열로 하드 코딩 했습니다. 이제이 코드를 업데이트 하 여 User.Identity.Name 속성을 대신 사용 하 고, Dinner a를 만드는 호스트에 대해 RSVP를 자동으로 추가할 수 있습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

[권한 부여] 특성을 Create () 메서드에 추가 했으므로 ASP.NET MVC는/Dinners/Create URL을 방문 하는 사용자가 사이트에 로그인 한 경우에만 동작 메서드가 실행 되도록 합니다. 이와 같이 User.Identity.Name 속성 값에는 항상 유효한 사용자 이름이 포함 됩니다.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Dinners를 편집할 때 User.Identity.Name 속성 사용

이제 자신이 호스트 하는 dinners 속성만 편집할 수 있도록 사용자를 제한 하는 권한 부여 논리를 추가 하겠습니다.

이를 지원 하기 위해 먼저 "IsHostedBy (사용자 이름)" 도우미 메서드를 Dinner object (이전에 빌드한 Dinner.cs partial 클래스 내)에 추가 합니다. 이 도우미 메서드는 제공 된 사용자 이름이 Dinner HostedBy 속성과 일치 하는지 여부에 따라 true 또는 false를 반환 하 고, 대/소문자를 구분 하지 않는 문자열 비교를 수행 하는 데 필요한 논리를 캡슐화 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

그런 다음, DinnersController 클래스 내의 Edit () 작업 메서드에 [권한 부여] 특성을 추가 합니다. 이렇게 하면 */Dinners/Edit/[id]* URL을 요청 하는 사용자가 로그인 해야 합니다.

그런 다음 IsHostedBy (username) 도우미 메서드를 사용 하 여 로그인 한 사용자가 Dinner host와 일치 하는지 확인 하는 코드를 편집 메서드에 추가할 수 있습니다. 사용자가 호스트가 아닌 경우 "InvalidOwner" 보기를 표시 하 고 요청을 종료 합니다. 이 작업을 수행 하는 코드는 다음과 같습니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

그런 다음 \Views\Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가&gt;보기 메뉴 명령을 선택 하 여 새 "InvalidOwner" 보기를 만들 수 있습니다. 다음 오류 메시지로 채웁니다.

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

사용자가 자신이 소유 하지 않은 저녁을 편집 하려고 하면 다음과 같은 오류 메시지가 표시 됩니다.

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

컨트롤러 내의 Delete () 작업 메서드에 대해 동일한 단계를 반복 하 여 Dinners 삭제 권한도 잠글 수 있으며 저녁의 호스트만 삭제할 수 있습니다.

### <a name="showinghiding-edit-and-delete-links"></a>편집 및 삭제 링크 표시/숨기기

세부 정보 URL에서 DinnersController 클래스의 편집 및 삭제 작업 메서드에 연결 하 고 있습니다.

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

현재 세부 정보 URL의 방문자가 저녁의 호스트 인지 여부에 관계 없이 편집 및 삭제 작업 링크를 표시 합니다. 이를 변경해 보겠습니다. 그러면 방문한 사용자가 저녁의 소유자 인 경우에만 링크가 표시 됩니다.

DinnersController 내의 Details () 작업 메서드는 Dinner object를 검색 한 다음이를 모델 개체로 모델 개체로 전달 합니다.

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

아래와 같이 IsHostedBy () 도우미 메서드를 사용 하 여 편집 및 삭제 링크를 조건부로 표시/숨기기 위해 뷰 템플릿을 업데이트할 수 있습니다.

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>다음 단계

이제 AJAX를 사용 하 여 인증 된 사용자에 게 RSVP for dinners를 사용 하도록 설정할 수 있는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](implement-efficient-data-paging.md)
> [다음](use-ajax-to-deliver-dynamic-updates.md)
