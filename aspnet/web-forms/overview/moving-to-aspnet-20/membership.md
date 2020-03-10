---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: 멤버 자격 | Microsoft Docs
author: microsoft
description: ASP.NET 멤버 자격은 ASP.NET 1.x의 폼 인증 모델 성공을 기반으로 합니다. ASP.NET Forms 인증은 incorp에 편리 하 게 액세스할 수 있는 방법을 제공 합니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521705"
---
# <a name="membership"></a>멤버 자격

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 멤버 자격은 ASP.NET 1.x의 폼 인증 모델 성공을 기반으로 합니다. ASP.NET Forms 인증은 로그인 폼을 ASP.NET 응용 프로그램에 통합 하 고 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다.

ASP.NET 멤버 자격은 ASP.NET 1.x의 폼 인증 모델 성공을 기반으로 합니다. ASP.NET Forms 인증은 로그인 폼을 ASP.NET 응용 프로그램에 통합 하 고 데이터베이스 또는 다른 데이터 저장소에 대해 사용자의 유효성을 검사 하는 편리한 방법을 제공 합니다. FormsAuthentication 클래스의 멤버는 인증에 대 한 쿠키를 처리 하 고, 유효한 로그인을 확인 하 고, 사용자를 로그 아웃할 수 있도록 합니다. 그러나 ASP.NET 1.x 응용 프로그램에서 폼 인증을 구현 하려면 상당한 양의 코드가 필요할 수 있습니다.

ASP.NET 2.0의 멤버 자격은 폼 인증만 사용 하는 것이 매우 중요 합니다. (멤버 자격은 폼 인증과 함께 사용할 경우 가장 강력 하지만 폼 인증을 사용 하는 것은 요구 사항이 아닙니다.) 곧 볼 수 있듯이 ASP.NET 2.0에서 ASP.NET 멤버 자격과 로그인 컨트롤을 사용 하 여 많은 코드를 작성 하지 않고도 강력한 멤버 자격 시스템을 구현할 수 있습니다.

## <a name="implementing-membership-in-aspnet-20"></a>ASP.NET 2.0의 멤버 자격 구현

멤버 자격은 4 단계에 따라 구현 됩니다. 구현할 수 있는 선택적 구성 뿐만 아니라 관련 된 많은 하위 단계를 염두에 두어야 합니다. 이러한 단계는 멤버 자격 구성의 큰 그림을 보여 주기 위한 것입니다.

1. 멤버 자격 데이터베이스를 만듭니다 (SQL Server 멤버 자격 저장소로 사용 되는 경우).
2. 응용 프로그램 구성 파일에서 멤버 자격 옵션을 지정 합니다. 멤버 자격은 기본적으로 사용 하도록 설정 되어 있습니다.
3. 사용 하려는 멤버 자격 저장소의 유형을 결정 합니다. 사용할 수 있는 옵션은 다음과 같습니다. 

    - Microsoft SQL Server (버전 7.0 이상)
    - Active Directory 저장소
    - 사용자 지정 멤버 자격 공급자
4. ASP.NET Forms 인증에 대 한 응용 프로그램을 구성 합니다. 다시 한 번, 멤버 자격은 폼 인증을 활용 하도록 설계 되었지만 폼 인증을 사용 하는 것은 요구 사항이 아닙니다.
5. 멤버 자격에 대 한 사용자 계정을 정의 하 고 원하는 경우 역할을 구성 합니다.

## <a name="creating-the-membership-database"></a>멤버 자격 데이터베이스 만들기

SQL Server 7.0 이상을 구성원 자격 저장소로 사용 하는 경우 aspnet\_regsql 유틸리티 (Visual Studio .NET 2005 명령 프롬프트에서 가장 쉽게 사용 가능)를 사용 하 여 데이터베이스를 구성할 수 있습니다. Aspnet\_regsql 유틸리티는 명령 프롬프트 도구나 GUI 마법사를 통해 사용할 수 있습니다. 마법사 메서드는 데이터베이스를 구성 하는 가장 쉬운 방법입니다. 마법사에 액세스 하려면 다음 명령을 실행 하기만 하면 됩니다.

`aspnet_regsql W`

이 명령을 실행 하면 아래와 같이 ASP.NET SQL Server 설치 마법사가 표시 됩니다.

![](membership/_static/image1.jpg)

**그림 1**

ASP.NET SQL Server 설치 마법사는 마법사에서 지정한 인스턴스에 웹 사이트를 만듭니다. 그러나 ASP.NET는 machine.config 파일의 연결 문자열을 사용 하 여 데이터베이스에 연결 합니다. 기본적으로이 연결 문자열은 SQL Server 2005 인스턴스를 가리키기 때문에 SQL Server 2000 또는 SQL Server 7.0 인스턴스를 사용 하는 경우에는 machine.config 파일에서 연결 문자열을 수정 해야 합니다. 이 연결 문자열은 다음 위치에서 찾을 수 있습니다.

[!code-xml[Main](membership/samples/sample1.xml)]

그러나 연결 문자열을 수정 하지 않는 경우 ASP.NET는 설명이 포함 된 오류를 제공 하지 않습니다. 데이터베이스를 만들지 않았다는 것은 계속 해 서 진행 됩니다. 위의 경우 로컬 SQL Server 2000 인스턴스를 가리키도록 연결 문자열을 수정 했습니다.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>구성 지정 및 사용자 및 역할 추가

멤버 자격을 구성 하는 다음 단계는 응용 프로그램의 web.config 파일에 필요한 정보를 추가 하는 것입니다. ASP.NET 1.x에서는 lowerCamelCase 사용 및 Intellisense의 부족으로 인해 web.config 파일을 수정 하는 것이 어려운 경우도 있습니다. Visual Studio .NET 2005은 구성 파일에 대해 Intellisense를 사용 하 여 작업을 훨씬 쉽게 만들지만, ASP.NET 2.0은 구성 파일을 편집 하기 위한 웹 인터페이스를 제공 하 여 한 단계 더 진행 됩니다.

아래와 같이 솔루션 탐색기 도구 모음에서 ASP.NET 구성 단추를 클릭 하 여 웹 인터페이스를 시작할 수 있습니다. 로그인 컨트롤이 삽입 될 때 표시 되는 팝업을 통해 웹 인터페이스를 시작할 수도 있습니다.

![](membership/_static/image2.jpg)

**그림 2**

그러면 아래에 표시 된 ASP.NET 웹 사이트 관리 도구가 시작 됩니다. ASP.NET 웹 사이트 관리는 응용 프로그램 설정 관리를 용이 하 게 하는 네 개의 탭 인터페이스입니다. 다음 탭을 사용할 수 있습니다.

- **홈**
- **보안** 사용자, 역할 및 액세스를 구성 합니다.
- **응용 프로그램** 응용 프로그램 설정을 구성 합니다.
- **공급자** 응용 프로그램 멤버 자격 공급자를 구성 하 고 테스트 합니다.

웹 사이트 관리 도구를 사용 하면 쉽게 새 사용자를 만들고, 새 역할을 만들고, 사용자 및 역할을 관리할 수 있습니다. 이 기능은 Windows 인터페이스에서 사용할 수 없습니다. Windows 인터페이스를 사용 하면 권한 부여 설정을 쉽게 정의 하 고 웹 사이트 관리 도구에 없는 공급자 기능을 추가, 삭제 및 관리할 수 있습니다.

Windows 인터페이스를 시작 하려면 인터넷 정보 서비스 스냅인을 열고 응용 프로그램을 마우스 오른쪽 단추로 클릭 한 다음 속성을 선택 합니다. ASP.NET 탭을 클릭 한 다음 구성 편집 단추를 클릭 합니다. (편집 구성 단추를 사용 하도록 설정 하려면 ASP.NET 2.0에서 응용 프로그램을 실행 해야 합니다. ASP.NET 대화 상자 에서도 ASP.NET 버전을 구성할 수 있습니다. ASP.NET 구성 설정 대화 상자가 아래와 같이 표시 됩니다.

![](membership/_static/image3.jpg)

**그림 3**

일반 탭에서 연결 문자열 및 응용 프로그램 설정이 나열 됩니다. 기울임꼴의 모든 설정은 부모 구성 파일 (machine.config 또는 상위 수준에 있는 web.config)에서 정의 되 고 기울임꼴로 설정 되지 않은 설정은 응용 프로그램 구성 파일에서 정의 됩니다. 응용 프로그램 수준에서 설정을 추가, 제거 또는 편집 하는 경우 ASP.NET는 상속 된 구성 파일에서 설정을 제거 하는 대신 응용 프로그램 수준 web.config에서 설정을 추가, 제거 또는 수정 합니다.

인증 탭은 아래와 같습니다. 여기에서 멤버 자격 설정을 구성 합니다. 폼 인증 설정, 멤버 자격 공급자 및 역할 공급자는 여기에서 구성할 수 있습니다.

![](membership/_static/image4.jpg)

**그림 4**

## <a name="implementing-membership-in-your-application"></a>응용 프로그램의 멤버 자격 구현

응용 프로그램에서 ASP.NET 2.0 멤버 자격을 구현 하는 가장 쉬운 방법은 제공 된 로그온 컨트롤을 사용 하는 것입니다. 이 메서드를 사용 하면 코드를 작성 하지 않고도 ASP.NET 2.0 멤버 자격의 기본 사항을 구현할 수 있습니다.

ASP.NET 2.0에서 사용할 수 있는 로그온 제어는 다음과 같습니다.

## <a name="login-control"></a>Login 컨트롤

로그인 컨트롤은 사용자가 멤버 자격 시스템에 로그인 할 수 있는 인터페이스를 제공 합니다. 사용자 이름 및 암호 텍스트 상자와 로그인 단추를 제공 합니다. 아직 수행 하지 않은 사용자를 위해 등록 하는 링크와 같은 다른 많은 일반적인 기능, 사용자가 후속 방문 시 자동으로 로그인 할 수 있도록 하는 확인란, 암호 미리 알림 링크 등이 있습니다. Login 컨트롤의 모든 기능은 컨트롤의 속성을 통해 사용자 지정할 수 있습니다.

ASP.NET 1.x에서 개발자는 폼 인증을 사용할 때 조회를 수행 하는 데 상당한 양의 코드를 작성 해야 했습니다. ASP.NET 2.0 멤버 자격을 사용 하면 코드를 작성 하지 않고도 사용자의 유효성을 검사할 수 있습니다. ASP.NET는 자동으로 사용자의 조회를 수행 합니다. ASP.NET 멤버 자격을 사용 하지 않고 로그인 제어를 사용 하는 경우 **Onauthenticate** 메서드를 사용 하 여 사용자의 유효성을 검사할 수 있습니다.

## <a name="loginview-control"></a>LoginView 컨트롤

LoginView 컨트롤은 기본적으로 두 가지 템플릿을 제공 하는 템플릿 기반 컨트롤입니다. AnonymousTemplate 및 LoggedInTemplate입니다. 표시 되는 템플릿은 사용자가 멤버 자격 시스템에 로그인 했는지 여부에 따라 결정 됩니다. 이 컨트롤은 사용자가 로그인 했을 때 사용자가 아직 로그인 하지 않은 경우 로그인 컨트롤을 표시 하는 데 사용 되 고 LoginStatus 컨트롤 및/또는 기타 로그인 컨트롤을 표시 하는 데 주로 사용 됩니다. ASP.NET 응용 프로그램에서 역할 관리를 사용 하는 경우 LoginView 컨트롤은 사용자 역할에 따라 특정 템플릿을 표시할 수 있습니다. ASP.NET 역할 관리에 대 한 자세한 내용은 뒷부분에서 설명 합니다.

## <a name="passwordrecovery-control"></a>PasswordRecovery 제어

PasswordRecovery 컨트롤을 사용 하면 사용자가 자신의 현재 암호를 사용 하 여 전자 메일을 받거나 암호를 다시 설정할 수 있습니다. 일반 텍스트 및 암호화 된 암호를 복구 하 고 사용자에 게 전자 메일로 보낼 수 있습니다. 암호가 해시 되 면 복구할 수 없습니다. 대신 사용자가 암호 재설정을 수행 해야 합니다.

## <a name="loginstatus-control"></a>LoginStatus 컨트롤

LoginStatus 컨트롤은 로그인 하지 않은 사용자에 게 로그인 표시기를 표시 하는 데 사용 되며 현재 로그인 한 사용자에 게 로그 아웃 표시기를 표시 하는 데 사용 됩니다. 요청. IsAuthenticated 속성은 표시할 표시기를 결정 하는 데 사용 됩니다. LoginStatus 컨트롤에 의해 표시 되는 표시기는 텍스트 ( **Logintext** 및 **logintext** 속성을 통해 구현 됨) 또는 이미지 ( **LoginImageUrl** 및 **logououtageurl** 속성을 통해 구현 됨) 일 수 있습니다.

사용자가 LoginStatus 컨트롤을 통해 로그 아웃 하면 **Logoutpageurl** 속성에 지정 된 URL로 리디렉션됩니다. 해당 속성이 설정 되지 않은 경우 현재 페이지가 새로 고쳐집니다. 사이트는 폼 인증으로 보호 될 가능성이 높기 때문에 현재 페이지를 새로 고치면 사용자가 사이트의 로그인 페이지로 리디렉션됩니다.

## <a name="loginname-control"></a>LoginName 컨트롤

LoginName 컨트롤은 사이트에 현재 로그인 한 사용자의 사용자 이름을 표시 합니다.

## <a name="createuserwizard-control"></a>CreateUserWizard 컨트롤

CreateUserWizard 컨트롤은 사용자에 게 멤버 자격 시스템에 등록 하는 편리한 방법을 제공 합니다. 아래 표시 된 인터페이스를 통해 단계 (WizardSteps의 컬렉션으로 구현 됨)를 추가할 수 있습니다.

![](membership/_static/image5.jpg)

**그림 5**

CreateUserWizard는 마법사 클래스에서 파생 되는 템플릿 기반 컨트롤이 며 다음 템플릿을 제공 합니다.

- **HeaderTemplate** 이 템플릿은 마법사 헤더의 모양을 제어 합니다.
- **바 템플릿** 이 템플릿은 마법사의 세로 막대의 모양을 제어 합니다.
- **Startnavigationtemplate** 이 템플릿은 시작 단계에서 마법사의 탐색 모양을 제어 합니다.
- **Stepnavigationtemplate** 이 템플릿은 시작 또는 완료 단계에 있지 않을 때의 탐색 영역 모양을 제어 합니다.
- 이 **Navigationtemplate 템플릿** 이 템플릿은 마침 단계에서 탐색 영역의 모양을 제어 합니다.

또한 마법사에 추가 하는 각 단계에 대해 ASP.NET은 해당 단계에 대 한 System.windows.controls.contentcontrol.contenttemplate 및 CustomNavigationTemplate을 모두 포함 하는 사용자 지정 템플릿을 만듭니다. CreateUserWizard를 사용자 지정 하는 방법에 대 한 자세한 내용은 VS.NET 2005 설명서를 참조 하세요.

## <a name="changepassword-control"></a>ChangePassword 컨트롤

ChangePassword 컨트롤을 통해 사용자는 자신의 암호를 변경할 수 있습니다. DisplayUserName 속성이 true 인 경우 (기본적으로 false 임) 사용자는 로그인 하지 않을 때 자신의 암호를 변경할 수 있습니다. 사용자가 이미 로그인 *되어* 있고 displayusername 속성이 true 이면 사용자가 로그인 하지 않은 다른 사용자의 암호를 변경 하 여 해당 사용자의 사용자 ID를 알 수 있습니다.

사용자가 로그인 할 필요 없이 암호를 변경할 수 있도록 하려면 ChangePassword 컨트롤이 표시 되는 페이지에서 익명 액세스를 허용 하는지 확인 해야 합니다. 사용자는 암호를 변경 하기 위해 이전 암호를 제공 해야 합니다.

## <a name="role-management"></a>역할 관리

역할 관리를 사용 하면 특정 역할에 사용자를 할당 한 다음 해당 역할에 따라 특정 파일이 나 폴더에 대 한 액세스를 제한할 수 있습니다. 또한 역할 관리는 API를 제공 하 여 프로그래밍 방식으로 누군가가 역할을 확인 하거나 특정 역할의 모든 사용자를 확인 하 고 적절 하 게 응답할 수 있습니다.

역할 관리는 ASP.NET 멤버 자격의 요구 사항이 아니며 역할 관리를 사용 하기 위해 요구 사항에 대 한 멤버 자격이 아닙니다. 그러나 두 추가는 서로 적절 하며 개발자가 서로 함께 사용할 수 있습니다.

응용 프로그램에서 역할 관리를 사용 하도록 설정 하려면 web.config 파일을 다음과 같이 변경 합니다.

[!code-xml[Main](membership/samples/sample2.xml)]

**Cacherolesincookie** 특성을 true로 설정 하면 ASP.NET가 클라이언트의 쿠키에 사용자 역할 멤버 자격을 캐시 합니다. 이렇게 하면 RoleProvider를 호출 하지 않고 역할 조회가 발생할 수 있습니다. 이 특성을 사용 하는 경우 개발자는 **cookieProtection** 특성이 All로 설정 되어 있는지 확인 하는 것이 좋습니다. 이것은 기본 설정입니다. 이렇게 하면 쿠키 데이터가 암호화 되어 쿠키 내용이 변경 되지 않도록 할 수 있습니다. 웹 사이트 관리 도구를 사용 하 여 역할을 추가할 수 있습니다. 이를 통해 역할을 쉽게 정의 하 고, 해당 역할을 기반으로 사이트의 일부에 대 한 액세스를 구성 하 고, 사용자를 역할에 할당할 수 있습니다.

![](membership/_static/image6.jpg)

**그림 6**

위와 같이 단순히 역할의 이름을 입력 한 다음 역할 추가를 클릭 하 여 새 역할을 추가할 수 있습니다. 기존 역할 목록에서 적절 한 링크를 클릭 하 여 기존 역할을 관리 하거나 삭제할 수 있습니다.

역할을 관리 하는 경우 아래와 같이 사용자를 추가 하거나 제거할 수 있습니다.

![](membership/_static/image7.jpg)

**그림 7**

사용자가 역할에 있음 확인란을 선택 하 여 특정 역할에 사용자를 쉽게 추가할 수 있습니다. ASP.NET는 멤버 자격 데이터베이스를 적절 한 항목으로 자동으로 업데이트 합니다. 또한 응용 프로그램에 대 한 액세스 규칙을 구성 하려고 합니다. ASP.NET 1.x 개발자는 web.config 파일의 &lt;권한 부여&gt; 요소를 통해이 작업을 수행 하는 데 익숙합니다 .이 옵션은 ASP.NET 2.0에서 계속 사용할 수 있습니다. 그러나 아래와 같이 웹 사이트 관리 도구를 사용 하 여 액세스 규칙을 보다 쉽게 관리할 수 있습니다.

![](membership/_static/image8.jpg)

**그림 8**

이 경우 관리 폴더가 강조 표시 되 고 (도구에서 밝은 회색으로 강조 표시 되기 때문에 확인 하기 어려운) 관리자 역할에 액세스 권한이 부여 됩니다. 다른 모든 사용자는 거부 됩니다. 헤드 아이콘을 클릭 하 여 규칙을 선택한 다음 위로 이동 및 아래로 이동 단추를 사용 하 여 규칙을 정렬할 수 있습니다. ASP.NET &lt;authorization&gt; 요소와 마찬가지로 규칙은 표시 된 순서 대로 처리 됩니다. 즉, 위에서 샷의 규칙 순서가 반대로 바뀐 경우 ASP.NET에서 발생 하는 첫 번째 규칙은 폴더에 대 한 모든 사용자를 거부 하는 규칙 이기 때문에 관리 폴더에 액세스할 수 없습니다.

ASP.NET 2.0는 액세스 규칙을 지정 하는 폴더에 web.config 파일을 추가 합니다. 액세스 규칙은 구성 파일이 나 웹 사이트 관리 도구를 통해 편집할 수 있습니다. 즉, 웹 사이트 관리 도구는 단순히 사용자에 게 친숙 한 환경에서 구성 파일을 편집할 수 있는 인터페이스입니다.

## <a name="using-roles-in-code"></a>코드에서 역할 사용

버전 1.x 이후 역할 관리에 대 한 API가 변경 되지 않았습니다. **IsInRole** 메서드는 사용자가 특정 역할에 있는지 여부를 확인 하는 데 사용 됩니다.

[!code-csharp[Main](membership/samples/sample3.cs)]

또한 ASP.NET는 현재 컨텍스트의 멤버로 RolePrincipal 인스턴스를 만듭니다. RolePrincipal 개체를 사용 하 여 사용자가 속한 모든 역할을 다음과 같이 가져올 수 있습니다.

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>LoginView 컨트롤과 함께 RoleGroups 사용

이제 역할 관리 및 멤버 자격을 이해 했으므로 LoginView 컨트롤이 ASP.NET 2.0에서이 기능을 활용 하는 방법을 간략하게 설명 합니다. 앞에서 설명한 것 처럼 LoginView 컨트롤은 기본적으로 두 개의 템플릿을 포함 하는 템플릿 기반 컨트롤입니다. AnonymousTemplate 및 LoggedInTemplate입니다. LoginView 작업 대화 상자에는 RoleGroups를 편집할 수 있는 링크 (아래 참조)가 있습니다.

![](membership/_static/image9.jpg)

**그림 9**

각 RoleGroup 개체는 RoleGroup이 적용 되는 역할을 정의 하는 문자열의 배열을 포함 합니다. LoginView 컨트롤에 새 RoleGroup을 추가 하려면 Rolegroup 편집 링크를 클릭 합니다. 위의 그림에서 관리자에 대 한 새 RoleGroup을 추가 했을 수 있습니다. 보기 드롭다운에서 RoleGroup (RoleGroup [0])을 선택 하 여 관리자 역할의 구성원 에게만 표시 되는 템플릿을 구성할 수 있습니다. 아래 이미지에서 Sales 역할 및 배포 역할의 멤버에 적용 되는 새 RoleGroup을 추가 했습니다. 그러면 LoginView 작업 대화 상자의 보기 드롭다운에서 두 번째 RoleGroup을 추가 하 고 해당 템플릿에 추가 된 모든 항목은 판매 또는 배포 역할의 모든 사용자가 볼 수 있습니다.

![](membership/_static/image10.jpg)

**그림 10**

## <a name="overriding-the-existing-membership-provider"></a>기존 멤버 자격 공급자 재정의

ASP.NET 멤버 자격의 기능을 확장할 수 있는 몇 가지 방법이 있습니다. 먼저, 해당 클래스에서 상속 하 고 해당 메서드를 재정의 하 여 SqlMembershipProvider 클래스의 기존 기능을 명확히 변경할 수 있습니다. 예를 들어 사용자를 만들 때 고유한 기능을 구현 하려는 경우 다음과 같이 SqlMembershipProvider에서 상속 하는 고유한 클래스를 만들 수 있습니다.

[!code-csharp[Main](membership/samples/sample5.cs)]

반면에 사용자 고유의 공급자를 만들려고 할 때 (예: Access 데이터베이스에 멤버 자격 정보를 저장 하는 경우) 사용자 고유의 공급자를 만들 수 있습니다.

## <a name="creating-your-own-membership-provider"></a>사용자 고유의 멤버 자격 공급자 만들기

사용자 고유의 멤버 자격 공급자를 만들려면 먼저 MembershipProvider 클래스에서 상속 되는 클래스를 만들어야 합니다. VB.NET를 사용 하는 경우 Visual Studio 2005는 재정의 해야 하는 모든 메서드에 대 한 스텁을 추가 합니다. 를 사용 C#하는 경우 스텁을 추가 합니다.

다음을 재정의 해야 합니다.

- ApplicationName 속성
- ChangePassword 함수
- ChangePasswordQuestionAndAnswer 함수
- CreateUser 함수
- DeleteUser 함수
- EnablePasswordReset 속성
- EnablePasswordRetrieval 속성
- FindUsersByEmail 함수
- FindUsersByName 함수
- GetAllUsers 함수
- Getnumberofusers Online 함수
- GetPassword 함수
- GetUser 함수
- GetUserNameByEmail 함수
- MaxInvalidPasswordAttempts 속성
- MinRequiredNonAlphanumericCharacters 속성
- MinRequiredPasswordLength 속성
- PasswordAttemptWindow 속성
- PasswordFormat 속성
- PasswordStrengthRegularExpression 속성
- RequiresQuestionAndAnswer 속성
- RequiresUniqueEmail 속성
- ResetPassword 함수
- 사용자 함수 잠금 해제
- UpdateUser 함수
- ValidateUser 함수

C# 개발자로 구현할 목록을 있거나. 구현 없이 VB.NET에서 클래스를 만든 다음 .NET 반영자 나 이와 유사한 도구를 사용 하 여 코드를로 변환 하는 것이 더 쉬울 C#수 있습니다.

Initialize 메서드에서 연결 문자열 및 기타 속성을 기본값으로 설정 해야 합니다. Initialize 메서드는 런타임에 공급자가 로드 될 때 발생 합니다. Initialize 메서드의 두 번째 매개 변수는 NameValueCollection 형식입니다 .는 web.config 파일의 사용자 지정 공급자와 연결 된&gt; 요소를 추가 &lt;에 대 한 참조입니다. 해당 항목은 다음과 같습니다.

[!code-xml[Main](membership/samples/sample6.xml)]

Initialize 메서드의 예는 다음과 같습니다.

[!code-csharp[Main](membership/samples/sample7.cs)]

사용자가 로그인 양식을 제출할 때 사용자의 유효성을 검사 하려면 ValidateUser 메서드를 사용 해야 합니다. 이 메서드는 사용자가 로그인 컨트롤의 로그인 단추를 클릭할 때 발생 합니다. 이 메서드에서 사용자 조회를 수행 하는 코드를 저장 합니다.

여기에서 볼 수 있듯이 사용자 고유의 멤버 자격 공급자를 작성 하는 것은 어렵고 ASP.NET 2.0의 이러한 강력한 기능을 확장할 수 있습니다.
