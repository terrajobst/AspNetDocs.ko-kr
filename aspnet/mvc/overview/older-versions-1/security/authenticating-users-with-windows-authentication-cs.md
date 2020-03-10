---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
title: Windows 인증을 사용 하 여C#사용자 인증 () | Microsoft Docs
author: microsoft
description: MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 대해 알아봅니다. 응용 프로그램의 웹 공동에서 Windows 인증을 사용 하도록 설정 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 418bb07e-f369-4119-b4b0-08f890f7abb2
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bb3909bff2791c15a8737fc12cac69f79b55733f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506249"
---
# <a name="authenticating-users-with-windows-authentication-c"></a>Windows 인증으로 사용자 인증(C#)

[Microsoft](https://github.com/microsoft) 에서

> MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 대해 알아봅니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법 및 IIS를 사용 하 여 인증을 구성 하는 방법을 알아봅니다. 마지막으로 [권한 부여] 특성을 사용 하 여 특정 Windows 사용자 또는 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 하는 방법을 알아봅니다.

이 자습서의 목표는 인터넷 정보 서비스에 기본 제공 되는 보안 기능을 활용 하 여 MVC 응용 프로그램에서 뷰를 암호로 보호 하는 방법을 설명 하는 것입니다. 특정 windows 사용자 또는 특정 Windows 그룹의 멤버인 사용자만 컨트롤러 작업을 호출 하도록 허용 하는 방법에 대해 알아봅니다.

내부 회사 웹 사이트 (인트라넷 사이트)를 구축 하 고 사용자가 웹 사이트에 액세스할 때 표준 Windows 사용자 이름 및 암호를 사용할 수 있도록 하려면 Windows 인증을 사용 하는 것이 좋습니다. 바깥쪽 연결 웹 사이트 (인터넷 웹 사이트)를 빌드하는 경우 폼 인증을 대신 사용 하는 것이 좋습니다.

#### <a name="enabling-windows-authentication"></a>Windows 인증 사용

새 ASP.NET MVC 응용 프로그램을 만들 때 Windows 인증은 기본적으로 사용 되지 않습니다. 폼 인증은 MVC 응용 프로그램에 사용할 수 있는 기본 인증 유형입니다. MVC 응용 프로그램의 웹 구성 (web.config) 파일을 수정 하 여 Windows 인증을 사용 하도록 설정 해야 합니다. &lt;인증&gt; 섹션을 찾아 다음과 같은 폼 인증 대신 Windows를 사용 하도록 수정 합니다.

[!code-xml[Main](authenticating-users-with-windows-authentication-cs/samples/sample1.xml)]

Windows 인증을 사용 하도록 설정 하면 웹 서버에서 사용자 인증을 담당 하 게 됩니다. 일반적으로 ASP.NET MVC 응용 프로그램을 만들고 배포할 때 사용 하는 두 가지 유형의 웹 서버가 있습니다.

첫째, MVC 응용 프로그램을 개발 하는 동안 Visual Studio에 포함 된 ASP.NET Development 웹 서버를 사용 합니다. 기본적으로 ASP.NET Development 웹 서버는 현재 Windows 계정 (Windows에 로그인 하는 데 사용한 모든 계정)의 컨텍스트에서 모든 페이지를 실행 합니다.

ASP.NET Development 웹 서버는 NTLM 인증도 지원 합니다. 솔루션 탐색기 창에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 하 여 NTLM 인증을 사용 하도록 설정할 수 있습니다. 그런 다음 웹 탭을 선택 하 고 NTLM 확인란을 선택 합니다 (그림 1 참조).

**그림 1-ASP.NET Development 웹 서버에 대 한 NTLM 인증 사용**

![clip_image002](authenticating-users-with-windows-authentication-cs/_static/image1.jpg)

프로덕션 웹 응용 프로그램의 경우 웹 서버로 IIS를 사용 합니다. IIS는 다음과 같은 여러 유형의 인증을 지원 합니다.

- 기본 인증 – HTTP 1.0 프로토콜의 일부로 정의 됩니다. 인터넷을 통해 사용자 이름 및 암호를 일반 텍스트 (Base64 인코딩)로 보냅니다. -다이제스트 인증 – 인터넷을 통해 암호 자체가 아닌 암호의 해시를 보냅니다. -통합 Windows (NTLM) 인증 – Windows를 사용 하 여 인트라넷 환경에서 사용할 최적의 인증 유형입니다. -인증서 인증 – 클라이언트 쪽 인증서를 사용 하 여 인증을 사용 하도록 설정 합니다. 인증서가 Windows 사용자 계정에 매핑됩니다.

> [!NOTE] 
> 
> 이러한 여러 유형의 인증에 대 한 자세한 개요는 [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)를 참조 하세요.

인터넷 정보 서비스 관리자를 사용 하 여 특정 유형의 인증을 사용 하도록 설정할 수 있습니다. 모든 운영 체제의 경우 모든 유형의 인증을 사용할 수 있는 것은 아닙니다. 또한 Windows Vista에서 IIS 7.0를 사용 하는 경우 인터넷 정보 서비스 Manager에 표시 되기 전에 다른 유형의 Windows 인증을 사용 하도록 설정 해야 합니다. **제어판, 프로그램, 프로그램 및 기능을 열고 Windows 기능을 설정 하거나 해제**하 고 인터넷 정보 서비스 노드를 확장 합니다 (그림 2 참조).

**그림 2-Windows IIS 기능 사용**

![clip_image004](authenticating-users-with-windows-authentication-cs/_static/image2.jpg)

인터넷 정보 서비스를 사용 하 여 다양 한 유형의 인증을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 예를 들어 그림 3에서는 IIS 7.0를 사용할 때 익명 인증을 사용 하지 않도록 설정 하 고 Windows 통합 (NTLM) 인증을 사용 하도록 설정 합니다.

**그림 3-Windows 통합 인증 사용**

![clip_image006](authenticating-users-with-windows-authentication-cs/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>Windows 사용자 및 그룹 권한 부여

Windows 인증을 사용 하도록 설정한 후에는 [권한 부여] 특성을 사용 하 여 컨트롤러나 컨트롤러 작업에 대 한 액세스를 제어할 수 있습니다. 이 특성은 전체 MVC 컨트롤러 또는 특정 컨트롤러 작업에 적용할 수 있습니다.

예를 들어 목록 1의 홈 컨트롤러는 Index (), CompanySecrets () 및 StephenSecrets () 라는 세 개의 동작을 노출 합니다. 모든 사용자가 Index () 작업을 호출할 수 있습니다. 그러나 Windows 로컬 관리자 그룹의 멤버만 CompanySecrets () 작업을 호출할 수 있습니다. 마지막으로 Stephen (Redmond 도메인) 라는 Windows 도메인 사용자만 StephenSecrets () 작업을 호출할 수 있습니다.

**목록 1 – Controllers\ homecontroller.cs**

[!code-csharp[Main](authenticating-users-with-windows-authentication-cs/samples/sample2.cs)]

> [!NOTE] 
> 
> Windows Vista 또는 Windows Server 2008를 사용 하는 경우 Windows UAC (사용자 계정 컨트롤) 때문에 로컬 Administrators 그룹은 다른 그룹과 다르게 동작 합니다. [권한 부여] 특성은 컴퓨터의 UAC 설정을 수정 하지 않는 한 로컬 관리자 그룹의 구성원을 올바르게 인식 하지 못합니다.

적절 한 권한이 없는 컨트롤러 작업을 호출 하려고 할 때 발생 하는 작업은 사용 하도록 설정 된 인증 유형에 따라 달라 집니다. 기본적으로 ASP.NET 개발 서버 사용 하는 경우 빈 페이지를 가져옵니다. 이 페이지는 **401 인증 되지 않은** HTTP 응답 상태를 제공 합니다.

반면에 익명 인증을 사용 하지 않도록 설정 하 고 기본 인증을 사용 하는 IIS를 사용 하는 경우 보호 된 페이지를 요청할 때마다 로그인 대화 상자를 계속 표시 합니다 (그림 4 참조).

**그림 4-기본 인증 로그인 대화 상자**

![clip_image008](authenticating-users-with-windows-authentication-cs/_static/image4.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램의 컨텍스트에서 Windows 인증을 사용 하는 방법에 대해 설명 했습니다. 응용 프로그램의 웹 구성 파일 내에서 Windows 인증을 사용 하도록 설정 하는 방법 및 IIS를 사용 하 여 인증을 구성 하는 방법을 배웠습니다. 마지막으로 [권한 부여] 특성을 사용 하 여 특정 Windows 사용자 또는 그룹에 대 한 컨트롤러 작업에 대 한 액세스를 제한 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-forms-authentication-cs.md)
> [다음](preventing-javascript-injection-attacks-cs.md)
