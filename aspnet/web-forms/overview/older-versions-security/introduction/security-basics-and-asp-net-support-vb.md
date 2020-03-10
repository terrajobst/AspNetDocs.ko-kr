---
uid: web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
title: 보안 기본 사항 및 ASP.NET 지원 (VB) | Microsoft Docs
author: rick-anderson
description: 웹 양식을 통해 방문자를 인증 하 고, partic에 대 한 액세스 권한을 부여 하는 방법을 탐색 하는 일련의 자습서에서 첫 번째 자습서입니다.
ms.author: riande
ms.date: 01/13/2008
ms.assetid: ab68a92b-fc81-40a4-a7dc-406625d2c5d4
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/security-basics-and-asp-net-support-vb
msc.type: authoredcontent
ms.openlocfilehash: 99e986013cb5a923ddb150022013e3a75852ce55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464447"
---
# <a name="security-basics-and-aspnet-support-vb"></a>보안 기본 사항 및 ASP.NET 지원(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial01_Basics_vb.pdf)

> 이 자습서는 웹 양식을 통해 방문자를 인증 하 고, 특정 페이지 및 기능에 대 한 액세스 권한을 부여 하 고, ASP.NET 응용 프로그램에서 사용자 계정을 관리 하는 방법을 탐색 하는 일련의 자습서에서 첫 번째 자습서입니다.

## <a name="introduction"></a>소개

포럼, 전자 상거래 사이트, 온라인 전자 메일 웹 사이트, 포털 웹 사이트 및 소셜 네트워크 사이트는 모두 공통적으로 제공 되는 점은 무엇 인가요? 모두 *사용자 계정을*제공 합니다. 사용자 계정을 제공 하는 사이트는 다양 한 서비스를 제공 해야 합니다. 최소한 새 방문자가 계정을 만들 수 있어야 하며 방문자가 로그인 할 수 있어야 합니다. 이러한 웹 응용 프로그램은 로그인 한 사용자에 따라 결정을 내릴 수 있습니다. 일부 페이지 또는 작업은 로그인 한 사용자 또는 특정 사용자 하위 집합으로 제한 될 수 있습니다. 다른 페이지는 로그인 한 사용자와 관련 된 정보를 표시 하거나 사용자가 페이지를 보고 있는 항목에 따라 더 많은 정보를 표시할 수 있습니다.

이 자습서는 웹 양식을 통해 방문자를 인증 하 고, 특정 페이지 및 기능에 대 한 액세스 권한을 부여 하 고, ASP.NET 응용 프로그램에서 사용자 계정을 관리 하는 방법을 탐색 하는 일련의 자습서에서 첫 번째 자습서입니다. 이러한 자습서를 통해 다음을 수행 하는 방법을 살펴보겠습니다.

- 웹 사이트에 대 한 사용자 식별 및 로그인
- ASP를 사용 합니다. 사용자 계정을 관리 하는 NET의 멤버 자격 프레임 워크
- 사용자 계정을 만들고, 업데이트 하 고, 삭제 합니다.
- 로그인 한 사용자에 따라 웹 페이지, 디렉터리 또는 특정 기능에 대 한 액세스 제한
- ASP를 사용 합니다. 사용자 계정을 역할과 연결 하는 NET의 역할 프레임 워크
- 사용자 역할 관리
- 로그인 한 사용자의 역할에 따라 웹 페이지, 디렉터리 또는 특정 기능에 대 한 액세스 제한
- ASP를 사용자 지정 하 고 확장 합니다. NET의 보안 웹 컨트롤

이러한 자습서는 간결 하 게 만들어 프로세스를 시각적으로 안내 하는 다양 한 스크린 샷를 제공 하는 단계별 지침을 제공 합니다. 각 자습서는 및 Visual Basic C# 버전에서 사용할 수 있으며, 사용 되는 전체 코드의 다운로드를 포함 합니다. 이 첫 번째 자습서에서는 높은 수준의 관점에서 보안 개념에 중점을 둔 것 이므로 연결 된 코드를 포함 하지 않습니다.

이 자습서에서는 폼 인증, 권한 부여, 사용자 계정 및 역할을 구현 하는 데 도움이 되는 중요 한 보안 개념과 ASP.NET에서 사용할 수 있는 기능에 대해 설명 합니다. 이제 시작하겠습니다.

> [!NOTE]
> 보안은 물리적, 기술 및 정책 결정에 걸친 응용 프로그램의 중요 한 측면으로, 높은 수준의 계획 및 도메인 지식이 필요 합니다. 이 자습서 시리즈는 보안 웹 응용 프로그램을 개발 하기 위한 가이드로 제공 되지 않습니다. 대신, 폼 인증, 권한 부여, 사용자 계정 및 역할에 특히 집중 합니다. 이러한 문제를 중심으로 하는 일부 보안 개념은이 시리즈에 설명 되어 있지만 다른 일부는 탐색 되지 않은 남아 있습니다.

## <a name="authentication-authorization-user-accounts-and-roles"></a>인증, 권한 부여, 사용자 계정 및 역할

인증, 권한 부여, 사용자 계정 및 역할은이 자습서 시리즈 전체에서 매우 자주 사용 되는 네 가지 용어 이므로 웹 보안의 컨텍스트 내에서 이러한 용어를 빠르게 정의 하려고 합니다. 인터넷과 같은 클라이언트 서버 모델에서는 서버에서 요청을 수행 하는 클라이언트를 식별 해야 하는 여러 가지 시나리오가 있습니다. *인증은* 클라이언트의 id를 확인 하는 프로세스입니다. 성공적으로 식별 된 클라이언트는 *인증*됨 이라고 합니다. 식별 되지 않은 클라이언트는 *인증* 되지 않았거나 *익명*이라고 합니다.

보안 인증 시스템에는 다음 세 가지 패싯 중 하나 이상이 포함 [됩니다. 사용자가 알고 있는 항목 또는 사용자가가지고](http://www.cs.cornell.edu/Courses/cs513/2005fa/NNLauthPeople.html)있는 항목입니다. 대부분의 웹 응용 프로그램은 암호나 PIN과 같이 클라이언트에서 인식 하는 항목을 사용 합니다. 사용자의 사용자 이름 및 암호를 식별 하는 데 사용 되는 정보 (예:)를 *자격 증명*이라고 합니다. 이 자습서 시리즈는 사용자가 웹 페이지 양식에 자격 증명을 제공 하 여 사이트에 로그인 하는 인증 모델인 *폼 인증*에 중점을 둔 것입니다. 이전에는이 인증 유형을 모두 제공 했습니다. 모든 전자 상거래 사이트로 이동 합니다. 체크 아웃할 준비가 되 면 웹 페이지의 텍스트 상자에 사용자 이름과 암호를 입력 하 여 로그인 하 라는 메시지가 표시 됩니다.

클라이언트를 식별 하는 것 외에도 서버에서 요청 하는 클라이언트에 따라 액세스할 수 있는 리소스나 기능을 제한 해야 할 수 있습니다. *권한 부여* 는 특정 사용자에 게 특정 리소스 또는 기능에 액세스할 수 있는 권한이 있는지 여부를 확인 하는 프로세스입니다.

*사용자 계정은* 특정 사용자에 대 한 정보를 유지 하기 위한 저장소입니다. 사용자 계정에는 사용자의 로그인 이름 및 암호와 같이 사용자를 고유 하 게 식별 하는 정보가 최소한 포함 되어야 합니다. 이러한 필수 정보와 함께 사용자 계정에는 사용자의 전자 메일 주소와 같은 항목이 포함 될 수 있습니다. 계정을 만든 날짜와 시간입니다. 마지막으로 로그인 한 날짜와 시간입니다. 성과 이름 전화 번호; 우편 주소입니다. 폼 인증을 사용 하는 경우 사용자 계정 정보는 일반적으로 Microsoft SQL Server와 같은 관계형 데이터베이스에 저장 됩니다.

사용자 계정을 지 원하는 웹 응용 프로그램은 필요에 따라 사용자를 *역할로*그룹화 할 수 있습니다. 역할은 단순히 사용자에 게 적용 되는 레이블이 며 권한 부여 규칙과 페이지 수준 기능을 정의 하기 위한 추상화를 제공 합니다. 예를 들어 웹 사이트에는 관리자가 아닌 사용자가 특정 웹 페이지 집합에 액세스할 수 없도록 하는 권한 부여 규칙을 포함 하는 관리자 역할이 포함 될 수 있습니다. 또한 관리자가 아닌 사용자가 모든 사용자가 액세스할 수 있는 다양 한 페이지에서 추가 데이터를 표시 하거나 관리자 역할의 사용자가 방문할 때 추가 기능을 제공할 수 있습니다. 역할을 사용 하 여 사용자 단위 대신 역할 단위로 이러한 권한 부여 규칙을 정의할 수 있습니다.

## <a name="authenticating-users-in-an-aspnet-application"></a>ASP.NET 응용 프로그램에서 사용자 인증

사용자가 브라우저의 주소 창에 URL을 입력 하거나 링크를 클릭 하면 브라우저에서 웹 서버에 대 한 [HTTP (하이퍼텍스트 전송 프로토콜)](http://en.wikipedia.org/wiki/HTTP) 요청을 ASP.NET 페이지, 이미지, JavaScript 파일 또는 다른 유형의 콘텐츠로 만듭니다. 웹 서버는 요청 된 콘텐츠를 반환 합니다. 이렇게 하는 경우 요청을 수행한 사람과 요청 된 콘텐츠를 검색할 수 있는 권한이 있는지 여부를 포함 하 여 요청에 대 한 여러 가지 사항을 결정 해야 합니다.

기본적으로 브라우저는 모든 종류의 식별 정보가 부족 한 HTTP 요청을 보냅니다. 그러나 브라우저가 인증 정보를 포함 하는 경우 웹 서버는 인증 워크플로를 시작 합니다. 그러면 요청 하는 클라이언트를 식별 하려고 시도 합니다. 인증 워크플로의 단계는 웹 응용 프로그램에서 사용 하는 인증 유형에 따라 달라 집니다. ASP.NET는 Windows, Passport 및 forms의 세 가지 인증 유형을 지원 합니다. 이 자습서 시리즈는 폼 인증을 중심으로 하지만 Windows 인증 사용자 저장소와 워크플로를 비교 하 고 대비 하는 데 1 분 정도 걸릴 수 있습니다.

### <a name="authentication-via-windows-authentication"></a>Windows 인증을 통한 인증

Windows 인증 워크플로는 다음 인증 방법 중 하나를 사용 합니다.

- 기본 인증
- 다이제스트 인증
- Windows 통합 인증

이 세 가지 기술은 거의 동일한 방식으로 작동 합니다. 권한이 없는 익명 요청이 도착 하면 웹 서버는 계속 하기 위해 권한 부여가 필요 함을 나타내는 HTTP 응답을 다시 보냅니다. 그러면 브라우저에서 사용자의 사용자 이름과 암호를 묻는 모달 대화 상자가 표시 됩니다 (그림 1 참조). 그런 다음 HTTP 헤더를 통해 웹 서버에이 정보를 다시 보냅니다.

![사용자에 게 자격 증명을 묻는 모달 대화 상자가 표시 됩니다.](security-basics-and-asp-net-support-vb/_static/image1.png)

**그림 1**: 사용자에 게 자격 증명을 요청 하는 모달 대화 상자

제공 된 자격 증명은 웹 서버의 Windows 사용자 저장소에 대해 유효성이 검사 됩니다. 즉, 웹 응용 프로그램의 인증 된 각 사용자는 조직에 Windows 계정이 있어야 합니다. 이는 인트라넷 시나리오에서 일반적입니다. 실제로 인트라넷 설정에서 Windows 통합 인증을 사용 하는 경우 브라우저는 네트워크에 로그온 하는 데 사용 되는 자격 증명을 웹 서버에 자동으로 제공 하므로 그림 1에 표시 된 대화 상자는 표시 되지 않습니다. Windows 인증은 인트라넷 응용 프로그램에 적합 하지만, 사이트에서 등록 하는 모든 사용자와 각 사용자에 대해 Windows 계정을 만들지 않기 때문에 일반적으로 인터넷 응용 프로그램에 대 한 작업.

### <a name="authentication-via-forms-authentication"></a>폼 인증을 통한 인증

반면에 폼 인증은 인터넷 웹 응용 프로그램에 적합 합니다. 폼 인증은 사용자에 게 웹 양식을 통해 자격 증명을 입력 하 라는 메시지를 표시 하 여 사용자를 식별 합니다. 따라서 사용자가 권한이 없는 리소스에 액세스 하려고 하면 자격 증명을 입력할 수 있는 로그인 페이지로 자동 리디렉션됩니다. 그런 다음 사용자 지정 사용자 저장소 (일반적으로 데이터베이스)에 대해 제출 된 자격 증명의 유효성을 검사 합니다.

제출 된 자격 증명을 확인 한 후 사용자에 대 한 *폼 인증 티켓이* 생성 됩니다. 이 티켓은 사용자가 인증 되었으며 사용자 이름과 같은 식별 정보를 포함 하 고 있음을 나타냅니다. 폼 인증 티켓은 일반적으로 클라이언트 컴퓨터에 쿠키로 저장 됩니다. 따라서 웹 사이트에 대 한 후속 방문은 HTTP 요청에 폼 인증 티켓을 포함 하 여 웹 응용 프로그램이 로그인 한 후 사용자를 식별할 수 있도록 합니다.

그림 2에서는 상위 수준 유리한 지점에서의 폼 인증 워크플로를 보여 줍니다. ASP.NET의 인증 및 권한 부여 조각이 두 개의 개별 엔터티로 작동 하는지 확인 합니다. 폼 인증 시스템은 사용자를 식별 하거나 익명으로 보고 합니다. 권한 부여 시스템은 사용자에 게 요청 된 리소스에 대 한 액세스 권한이 있는지 여부를 결정 합니다. 사용자가 인증 되지 않은 경우 (예: ProtectedPage를 익명으로 방문 하려고 할 때) 권한 부여 시스템은 사용자가 거부 되었음을 보고 하 여 폼 인증 시스템이 사용자를 로그인 페이지로 자동으로 리디렉션합니다.

사용자가 성공적으로 로그인 하면 후속 HTTP 요청은 폼 인증 티켓을 포함 합니다. 폼 인증 시스템은 사용자를 식별 합니다. 사용자는 요청 된 리소스에 액세스할 수 있는지 여부를 결정 하는 권한 부여 시스템입니다.

![폼 인증 워크플로](security-basics-and-asp-net-support-vb/_static/image2.png)

**그림 2**: 폼 인증 워크플로

다음 두 자습서, 폼 인증 및 폼 인증 구성에[대 한 개요](an-overview-of-forms-authentication-vb.md) [및 고급 항목](forms-authentication-configuration-and-advanced-topics-vb.md)에서 폼 인증에 대해 훨씬 더 자세히 살펴보겠습니다. ASP에 대 한 자세한 정보. NET의 인증 옵션 [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)을 참조 하세요.

## <a name="limiting-access-to-web-pages-directories-and-page-functionality"></a>웹 페이지, 디렉터리 및 페이지 기능에 대 한 액세스 제한

ASP.NET에는 특정 사용자에 게 특정 파일이 나 디렉터리에 액세스할 수 있는 권한이 있는지 여부를 확인 하는 두 가지 방법이 있습니다.

- **파일 권한 부여** -ASP.NET 페이지와 웹 서비스는 웹 서버의 파일 시스템에 있는 파일로 구현 되기 때문에 이러한 파일에 대 한 액세스는 Access Control 목록 (acl)을 통해 지정할 수 있습니다. Acl은 Windows 계정에 적용 되는 권한 이므로 파일 권한 부여는 Windows 인증에서 가장 일반적으로 사용 됩니다. 폼 인증을 사용 하는 경우 사이트를 방문 하는 사용자에 관계 없이 모든 운영 체제 및 파일 시스템 수준 요청은 동일한 Windows 계정에서 실행 됩니다.
- **Url 권한**부여-url 권한 부여를 사용 하 여 페이지 개발자는 web.config에서 권한 부여 규칙을 지정 합니다. 이러한 권한 부여 규칙은 응용 프로그램의 특정 페이지 또는 디렉터리에 대 한 액세스가 허용 되거나 거부 되는 사용자 또는 역할을 지정 합니다.

파일 권한 부여 및 URL 권한 부여는 특정 ASP.NET 페이지 또는 특정 디렉터리의 모든 ASP.NET 페이지에 액세스 하기 위한 권한 부여 규칙을 정의 합니다. 이러한 기술을 사용 하 여 특정 사용자에 대 한 특정 페이지에 대 한 요청을 거부 하거나 사용자 집합에 대 한 액세스를 허용 하 고 다른 사람에 대 한 액세스를 거부 하도록 ASP.NET에 지시할 수 있습니다. 모든 사용자가 페이지에 액세스할 수 있지만 페이지의 기능이 사용자에 따라 달라 지는 시나리오는 어떻습니까? 예를 들어, 사용자 계정을 지 원하는 많은 사이트에는 인증 된 사용자와 익명 사용자에 대해 서로 다른 콘텐츠나 데이터를 표시 하는 페이지가 있습니다. 익명 사용자에 게 사이트에 로그인 하는 링크가 표시 될 수 있지만, 인증 된 사용자에 게는 로그 아웃 링크와 함께 환영 합니다. *사용자 이름과* 같은 메시지가 대신 표시 됩니다. 또 다른 예: 경매 사이트에서 항목을 볼 때 bidder 인지 또는 항목 경매에 따라 다른 정보를 볼 수 있습니다.

이러한 페이지 수준 조정은 선언적으로 또는 프로그래밍 방식으로 수행할 수 있습니다. 익명의 인증 된 사용자가 아닌 다른 콘텐츠를 표시 하려면 [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 을 페이지로 끌어다 놓고 해당 AnonymousTemplate 및 LoggedInTemplate 템플릿에 적절 한 콘텐츠를 입력 하기만 하면 됩니다. 또는 현재 요청이 인증 되었는지, 사용자가 누구 인지, 사용자가 속한 역할 (있는 경우)을 프로그래밍 방식으로 확인할 수 있습니다. 이 정보를 사용 하 여 페이지에서 표 또는 패널의 열을 표시 하거나 숨길 수 있습니다.

이 시리즈에는 권한 부여에 초점을 맞춘 세 가지 자습서가 포함 되어 있습니다. ***사용자 기반 권한 부여***는 특정 사용자 계정에 대 한 디렉터리의 페이지 또는 페이지에 대 한 액세스를 제한 하는 방법을 조사 합니다. 역할 ***기반 권한 부여*** 는 역할 수준에서 권한 부여 규칙을 제공 하는 것을 확인 합니다. 마지막으로, ***현재 로그인 한 사용자를 기준으로 콘텐츠 표시*** 자습서에서는 페이지를 방문 하는 사용자에 따라 특정 페이지의 내용 및 기능을 수정 하는 방법을 살펴봅니다. ASP에 대 한 자세한 정보. NET의 인증 옵션 [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)를 참조 하세요.

## <a name="user-accounts-and-roles"></a>사용자 계정 및 역할

ASP. NET의 폼 인증은 사용자가 사이트에 로그인 할 수 있는 인프라를 제공 하 고 페이지 방문 간에 해당 인증 된 상태를 기억 합니다. 및 URL 권한 부여는 ASP.NET 응용 프로그램의 특정 파일 또는 폴더에 대 한 액세스를 제한 하기 위한 프레임 워크를 제공 합니다. 그러나 두 기능 모두 사용자 계정 정보를 저장 하거나 역할을 관리 하는 수단을 제공 하지 않습니다.

ASP.NET 2.0 이전에는 개발자가 자신의 고유한 사용자 및 역할 저장소를 만들 책임이 있었습니다. 사용자 인터페이스를 디자인 하 고 로그인 페이지와 같은 필수 사용자 계정 관련 페이지와 새 계정을 만드는 데 필요한 코드를 작성 하기 위한 후크에도 있습니다. ASP.NET에 기본 제공 되는 사용자 계정 프레임 워크가 없는 경우 사용자 계정을 구현 하는 각 개발자는 암호 또는 기타 중요 한 정보를 저장 하는 어떻게 할까요?와 같은 질문에 대 한 고유한 설계 결정을 내려야 합니다. 암호 길이 및 강도와 관련 하 여 어떤 지침을 적용 해야 하나요?

현재 ASP.NET 응용 프로그램에서 사용자 계정을 구현 하는 것은 *멤버 프레임 워크* 및 기본 제공 로그인 웹 컨트롤 덕분에 훨씬 더 간단 합니다. Membership framework는 필수적인 사용자 계정 관련 작업을 수행 하는 기능을 제공 하는 [system.web. Security 네임 스페이스](https://msdn.microsoft.com/library/system.web.security.aspx) 의 몇 가지 클래스입니다. 멤버 프레임 프레임 워크의 키 클래스는 다음과 같은 메서드를 포함 하는 [멤버 자격 클래스](https://msdn.microsoft.com/library/system.web.security.membership.aspx)입니다.

- CreateUser
- DeleteUser
- GetAllUsers
- GetUser
- UpdateUser
- ValidateUser

멤버 자격 프레임 워크는 멤버 프레임 워크의 API를 구현과 완전히 분리 하는 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)을 사용 합니다. 이를 통해 개발자는 공용 API를 사용할 수 있지만 응용 프로그램의 사용자 지정 요구를 충족 하는 구현을 사용할 수 있습니다. 즉, 멤버 자격 클래스는 프레임 워크의 필수 기능 (메서드, 속성 및 이벤트)을 정의 하지만 실제로는 구현 세부 정보를 제공 하지 않습니다. 대신, 멤버 자격 클래스의 메서드는 구성 된 공급자를 호출 하 여 실제 작업을 수행 합니다. 예를 들어 멤버 자격 클래스의 CreateUser 메서드를 호출 하는 경우 멤버 자격 클래스는 사용자 저장소의 세부 정보를 알지 못합니다. 사용자가 데이터베이스 또는 XML 파일이 나 다른 저장소에서 유지 관리 되 고 있는지 여부를 알 수 없습니다. 멤버 자격 클래스는 웹 응용 프로그램의 구성을 검사 하 여 호출을 위임할 공급자를 결정 하 고, 해당 공급자 클래스는 실제로 적절 한 사용자 저장소에 새 사용자 계정을 만드는 작업을 담당 합니다. 이 상호 작용은 그림 3에 나와 있습니다.

Microsoft는 .NET Framework에 두 개의 멤버 자격 공급자 클래스를 제공 합니다.

- [ActiveDirectoryMembershipProvider](https://msdn.microsoft.com/library/system.web.security.activedirectorymembershipprovider.aspx) -ACTIVE DIRECTORY 및 ADAM (Active Directory 응용 프로그램 모드) 서버의 멤버 자격 API를 구현 합니다.
- [Sqlmembershipprovider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) -SQL Server 데이터베이스에서 멤버 자격 API를 구현 합니다.

이 자습서 시리즈는 SqlMembershipProvider만 중점적으로 다룹니다.

[공급자 모델 ![다른 구현이 프레임 워크에 원활 하 게 연결 될 수 있습니다.](security-basics-and-asp-net-support-vb/_static/image4.png)](security-basics-and-asp-net-support-vb/_static/image3.png)

**그림 03**: 공급자 모델을 사용 하면 다양 한 구현이 프레임 워크에 원활 하 게 연결 될 수 있습니다 ([전체 크기 이미지를 보려면 클릭](security-basics-and-asp-net-support-vb/_static/image5.png)).

공급자 모델의 혜택은 대체 구현을 Microsoft, 타사 공급 업체 또는 개별 개발자가 개발 하 고 멤버 자격 프레임 워크에 원활 하 게 연결할 수 있다는 것입니다. 예를 들어 microsoft는 [Microsoft Access 데이터베이스용 멤버 자격 공급자](https://download.microsoft.com/download/5/5/b/55bc291f-4316-4fd7-9269-dbf9edbaada8/sampleaccessproviders.vsi)를 출시 했습니다. 멤버 자격 공급자에 대 한 자세한 내용은 공급자 도구 설명을 포함 하는 [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)를 참조 하세요. 여기에는 공급자 모델에 대 한 설명서의 100 페이지 및 기본 제공 멤버 자격 공급자 (즉, ActiveDirectoryMembershipProvider 및 sqlmembershipprovider)의 전체 소스 코드가 포함 되어 있습니다.

ASP.NET 2.0에는 역할 프레임 워크도 도입 되었습니다. 멤버 프레임 워크와 마찬가지로 역할 프레임 워크는 공급자 모델 위에 빌드됩니다. 해당 API는 [Roles 클래스](https://msdn.microsoft.com/library/system.web.security.roles.aspx) 를 통해 노출 되 고 .NET Framework는 세 가지 공급자 클래스와 함께 제공 됩니다.

- [AuthorizationStoreRoleProvider](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx) -ACTIVE DIRECTORY 또는 ADAM과 같은 권한 부여 관리자 정책 저장소의 역할 정보를 관리 합니다.
- [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) -SQL Server 데이터베이스에서 역할을 구현 합니다.
- [WindowsTokenRoleProvider](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx) -방문자의 Windows 그룹을 기반으로 역할 정보를 연결 합니다. 이 메서드는 일반적으로 Windows 인증과 함께 사용 됩니다.

이 자습서 시리즈는 SqlRoleProvider만 중점적으로 다룹니다.

공급자 모델에는 단일 전방 연결 API (멤버 자격 및 역할 클래스)가 포함 되어 있으므로 구현 세부 정보에 대해 걱정할 필요 없이 해당 API에 대 한 기능을 빌드할 수 있습니다. 이러한 기능은 페이지에서 선택한 공급자에 의해 처리 됩니다. 개발. 이 통합 API를 통해 Microsoft 및 타사 공급 업체는 멤버 자격 및 역할 프레임 워크와 상호 작용 하는 웹 컨트롤을 빌드할 수 있습니다. ASP.NET는 일반적인 사용자 계정 사용자 인터페이스를 구현 하기 위한 다양 한 [로그인 웹 컨트롤과](https://msdn.microsoft.com/library/ms178329.aspx) 함께 제공 됩니다. 예를 들어, [로그인 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) 은 사용자에 게 자격 증명을 묻는 메시지를 표시 하 고, 유효성을 검사 한 다음 폼 인증을 통해이를 로깅합니다. [LoginView 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) 은 익명 사용자와 인증 된 사용자 또는 사용자의 역할에 따라 다른 태그를 표시 하기 위한 템플릿을 제공 합니다. [CreateUserWizard 컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.aspx) 은 새 사용자 계정을 만들기 위한 단계별 사용자 인터페이스를 제공 합니다.

아래에는 다양 한 로그인 컨트롤이 멤버 자격 및 역할 프레임 워크와 상호 작용 합니다. 코드를 한 줄도 작성 하지 않고도 대부분의 로그인 컨트롤을 구현할 수 있습니다. 이러한 컨트롤은 기능을 확장 하 고 사용자 지정 하는 기술을 포함 하 여 이후 자습서에서 더 자세히 살펴보겠습니다.

## <a name="summary"></a>요약

사용자 계정을 지 원하는 모든 웹 응용 프로그램에는 사용자가 로그인 하 고 페이지 방문 간에 로그인 상태를 유지 하는 기능 등의 유사한 기능이 필요 합니다. 새 방문자가 계정을 만들 수 있는 웹 페이지입니다. 사용자 또는 역할에 사용할 수 있는 리소스, 데이터 및 기능을 지정 하는 것이 페이지 개발자에 게 제공 되는 기능입니다. 사용자를 인증 하 고 권한을 부여 하 고 사용자 계정 및 역할을 관리 하는 작업은 폼 인증, URL 권한 부여 및 멤버 자격 및 역할 프레임 워크 덕분에 ASP.NET 응용 프로그램에서 매우 쉽게 수행할 수 있습니다.

다음 몇 가지 자습서를 진행 하는 과정에서 단계별 방식으로 작업 중인 웹 응용 프로그램을 구축 하 여 이러한 측면을 살펴보겠습니다. 다음 두 자습서에서는 폼 인증을 자세히 살펴봅니다. 방문자가 로그인 및 로그 아웃할 수 있도록 하는 웹 응용 프로그램을 빌드하는 동안 양식 인증 워크플로를 실행 하 고, 폼 인증 티켓을 알아본, 보안 문제를 설명 하 고, 폼 인증 시스템을 구성 하는 방법을 알아봅니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 2.0 멤버 자격, 역할, 폼 인증 및 보안 리소스](https://weblogs.asp.net/scottgu/ASP.NET-2.0-Membership_2C00_-Roles_2C00_-Forms-Authentication_2C00_-and-Security-Resources-)
- [ASP.NET 2.0 보안 지침](https://msdn.microsoft.com/library/ms998258.aspx)
- [ASP.NET 인증](https://msdn.microsoft.com/library/eeyk640h.aspx)
- [ASP.NET 권한 부여](https://msdn.microsoft.com/library/wce3kxhd.aspx)
- [ASP.NET Login 컨트롤 개요](https://msdn.microsoft.com/library/ms178329.aspx)
- [ASP.NET 2.0의 멤버 자격, 역할 및 프로필 검사](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [방법: 멤버 자격 및 역할을 사용 하 여 내 사이트 보호](https://asp.net/learn/videos/video-45.aspx) 화면이
- [멤버 자격 소개](https://msdn.microsoft.com/library/yh26yfzy.aspx)
- [MSDN 보안 개발자 센터](https://msdn.microsoft.com/security/default.aspx)
- [전문 ASP.NET 2.0 보안, 멤버 자격 및 역할 관리](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는이 자습서 시리즈를 많은 유용한 검토자가 검토 했습니다. 이 자습서의 선임 검토자는 Alicja Maziarz, John Suru 및 Teresa Murphy를 포함 합니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](forms-authentication-configuration-and-advanced-topics-cs.md)
> [다음](an-overview-of-forms-authentication-vb.md)
