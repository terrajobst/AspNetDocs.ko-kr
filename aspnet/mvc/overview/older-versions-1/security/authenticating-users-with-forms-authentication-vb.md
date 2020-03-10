---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
title: 폼 인증을 사용 하 여 사용자 인증 (VB) | Microsoft Docs
author: microsoft
description: '[권한 부여] 특성을 사용 하 여 MVC 응용 프로그램에서 특정 페이지를 암호로 보호 하는 방법에 대해 알아봅니다. 웹 사이트 관리를 사용 하는 방법에 대해 알아봅니다.'
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 4341f5b1-6fe5-44c5-8b8a-18fa84f80177
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: a2c2140631d59a7f8b21aa73613a92ea5c7a91d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498935"
---
# <a name="authenticating-users-with-forms-authentication-vb"></a>폼 인증으로 사용자 인증(VB)

[Microsoft](https://github.com/microsoft) 에서

> [권한 부여] 특성을 사용 하 여 MVC 응용 프로그램에서 특정 페이지를 암호로 보호 하는 방법에 대해 알아봅니다. 웹 사이트 관리 도구를 사용 하 여 사용자 및 역할을 만들고 관리 하는 방법을 알아봅니다. 또한 사용자 계정 및 역할 정보가 저장 되는 위치를 구성 하는 방법을 알아봅니다.

이 자습서의 목표는 폼 인증을 사용 하 여 ASP.NET MVC 응용 프로그램에서 뷰를 암호로 보호 하는 방법을 설명 하는 것입니다. 웹 사이트 관리 도구를 사용 하 여 사용자 및 역할을 만드는 방법에 대해 알아봅니다. 또한 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 방지 하는 방법도 알아봅니다. 마지막으로 사용자 이름 및 암호를 저장 하는 위치를 구성 하는 방법을 알아봅니다.

#### <a name="using-the-web-site-administration-tool"></a>웹 사이트 관리 도구 사용

다른 작업을 수행 하기 전에 먼저 일부 사용자 및 역할을 만들어야 합니다. 새 사용자 및 역할을 만드는 가장 쉬운 방법은 Visual Studio 2008 웹 사이트 관리 도구를 사용 하는 것입니다. 메뉴 옵션 **프로젝트, ASP.NET 구성**을 선택 하 여이 도구를 시작할 수 있습니다. 또는 솔루션 탐색기 창의 맨 위에 표시 되는 전 세계에 있는 해머의 (약간의) 아이콘을 클릭 하 여 웹 사이트 관리 도구를 시작할 수 있습니다 (그림 1 참조).

**그림 1-웹 사이트 관리 도구 시작**

![clip_image002[4]](authenticating-users-with-forms-authentication-vb/_static/image1.jpg)

웹 사이트 관리 도구에서 보안 탭을 선택 하 여 새 사용자 및 역할을 만듭니다. **사용자 만들기** 링크를 클릭 하 여 Stephen 라는 새 사용자를 만듭니다 (그림 2 참조). Stephen 사용자에 게 원하는 암호를 제공 합니다 (예: *secret*).

**그림 2-새 사용자 만들기**

![clip_image004[4]](authenticating-users-with-forms-authentication-vb/_static/image2.jpg)

먼저 역할을 사용 하도록 설정 하 고 하나 이상의 역할을 정의 하 여 새 역할을 만듭니다. **역할 사용** 링크를 클릭 하 여 역할을 사용 하도록 설정 합니다. 그런 다음 **역할 만들기 또는 관리** 링크를 클릭 하 여 *관리자* 라는 역할을 만듭니다 (그림 3 참조).

**그림 3-새 역할 만들기**

![clip_image006[4]](authenticating-users-with-forms-authentication-vb/_static/image3.jpg)

마지막으로 Sally 이라는 새 사용자를 만들고 사용자 만들기 링크를 클릭 하 고 Sally를 만들 때 관리자를 선택 하 여 Sally를 관리자 역할에 연결 합니다 (그림 4 참조).

**그림 4-역할에 사용자 추가**

![clip_image008[4]](authenticating-users-with-forms-authentication-vb/_static/image4.jpg)

모든 작업이 완료 되 면 Stephen 및 Sally 라는 두 명의 새 사용자가 있어야 합니다. 또한 관리자 라는 새 역할이 있어야 합니다. Sally는 Administrators 역할의 멤버이 고 Stephen는 그렇지 않습니다.

#### <a name="requiring-authorization"></a>권한 부여 필요

사용자가 작업에 [권한 부여] 특성을 추가 하 여 사용자가 컨트롤러 작업을 호출 하기 전에 사용자를 인증 하도록 요구할 수 있습니다. [권한 부여] 특성을 개별 컨트롤러 작업에 적용 하거나, 전체 컨트롤러 클래스에이 특성을 적용할 수 있습니다.

예를 들어 목록 1의 컨트롤러는 CompanySecrets () 이라는 동작을 노출 합니다. 이 동작은 [권한 부여] 특성으로 데코레이팅 되므로 사용자를 인증 하지 않으면이 작업을 호출할 수 없습니다.

**목록 1 – Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample1.vb)]

브라우저의 주소 표시줄에 URL/Home/CompanySecrets을 입력 하 여 CompanySecrets () 작업을 호출 하 고 사용자가 인증 된 사용자가 아닌 경우에는 로그인 뷰로 자동으로 리디렉션됩니다 (그림 5 참조).

**그림 5-로그인 보기**

![clip_image010[4]](authenticating-users-with-forms-authentication-vb/_static/image5.jpg)

로그인 보기를 사용 하 여 사용자 이름 및 암호를 입력할 수 있습니다. 등록 된 사용자가 아닌 경우 **등록 링크를 클릭 하 여 등록** 보기로 이동할 수 있습니다 (그림 6 참조). 등록 보기를 사용 하 여 새 사용자 계정을 만들 수 있습니다.

**그림 6-레지스터 보기**

![clip_image012](authenticating-users-with-forms-authentication-vb/_static/image6.jpg)

성공적으로 로그인 하면 CompanySecrets 보기를 볼 수 있습니다 (그림 7 참조). 기본적으로 브라우저 창을 닫을 때까지 계속 로그인 됩니다.

**그림 7-CompanySecrets 뷰**

![clip_image014](authenticating-users-with-forms-authentication-vb/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>사용자 이름 또는 사용자 역할에의 한 권한 부여

[권한 부여] 특성을 사용 하 여 특정 사용자나 특정 사용자 역할 집합에 대 한 컨트롤러 작업에 대 한 액세스를 제한할 수 있습니다. 예를 들어 목록 2의 수정 된 홈 컨트롤러에는 StephenSecrets () 및 관리자 암호 () 라는 두 개의 새로운 동작이 포함 되어 있습니다.

**목록 2 – Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-forms-authentication-vb/samples/sample2.vb)]

사용자 이름이 Stephen 인 사용자만 StephenSecrets () 작업을 호출할 수 있습니다. 다른 모든 사용자는 로그인 뷰로 리디렉션됩니다. 사용자 속성은 쉼표로 구분 된 사용자 계정 이름 목록을 허용 합니다.

관리자 역할의 사용자만 관리자 암호 () 작업을 호출할 수 있습니다. 예를 들어 Sally가 Administrators 그룹의 멤버 이기 때문에 관리자 암호 () 작업을 호출할 수 있습니다. 다른 모든 사용자는 로그인 뷰로 리디렉션됩니다. Roles 속성은 쉼표로 구분 된 역할 이름 목록을 수락 합니다.

#### <a name="configuring-authentication"></a>인증 구성

이 시점에서 사용자 계정 및 역할 정보가 저장 되는 위치를 궁금할 수 있습니다. 기본적으로이 정보는 MVC 응용 프로그램의 App\_Data 폴더에 있는 ASPNETDB.MDF 라는 SQL Express 데이터베이스 (RANU)에 저장 됩니다. 이 데이터베이스는 멤버 자격 사용을 시작할 때 자동으로 ASP.NET 프레임 워크에 의해 생성 됩니다.

솔루션 탐색기 창에서 ASPNETDB.MDF 데이터베이스를 보려면 먼저 메뉴 옵션 프로젝트, 모든 파일 표시를 선택 해야 합니다.

응용 프로그램을 개발할 때 기본 SQL Express 데이터베이스를 사용 하는 것은 괜찮습니다. 그러나 프로덕션 응용 프로그램에 대해 기본 ASPNETDB.MDF 데이터베이스를 사용 하지 않을 가능성이 높습니다. 이 경우 다음 두 단계를 완료 하 여 사용자 계정 정보가 저장 되는 위치를 변경할 수 있습니다.

1. 프로덕션 데이터베이스에 애플리케이션 서비스 데이터베이스 개체 추가-프로덕션 데이터베이스를 가리키도록 응용 프로그램 연결 문자열 변경

첫 번째 단계는 필요한 모든 데이터베이스 개체 (테이블 및 저장 프로시저)를 프로덕션 데이터베이스에 추가 하는 것입니다. 이러한 개체를 새 데이터베이스에 추가 하는 가장 쉬운 방법은 ASP.NET SQL Server 설치 마법사를 사용 하는 것입니다 (그림 8 참조). Microsoft Visual Studio 2008 프로그램 그룹에서 Visual Studio 2008 명령 프롬프트를 열고 명령 프롬프트에서 다음 명령을 실행 하 여이 도구를 시작할 수 있습니다.

aspnet\_regsql

**그림 8-ASP.NET SQL Server 설치 마법사**

![clip_image016](authenticating-users-with-forms-authentication-vb/_static/image8.jpg)

ASP.NET SQL Server 설치 마법사를 사용 하 여 네트워크에서 SQL Server 데이터베이스를 선택 하 고 ASP.NET 응용 프로그램 서비스에 필요한 모든 데이터베이스 개체를 설치할 수 있습니다. 데이터베이스 서버가 로컬 컴퓨터에 있을 필요는 없습니다.

> [!NOTE]
> ASP.NET SQL Server 설치 마법사를 사용 하지 않으려는 경우 다음 폴더에 응용 프로그램 서비스 데이터베이스 개체를 추가 하는 SQL 스크립트를 찾을 수 있습니다.
> 
> 
> C:\Windows\Microsoft.NET\Framework\v2.0.50727

필요한 데이터베이스 개체를 만든 후에는 MVC 응용 프로그램에서 사용 하는 데이터베이스 연결을 수정 해야 합니다. 프로덕션 데이터베이스를 가리키도록 웹 구성 파일 (web.config)에서 ApplicationServices 연결 문자열을 수정 합니다. 예를 들어 목록 3의 수정 된 연결은 MyProductionDB 라는 데이터베이스를 가리킵니다 (원래 ApplicationServices 연결 문자열은 주석 처리 됨).

**목록 3 – web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-vb/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>데이터베이스 사용 권한 구성

통합 보안을 사용 하 여 데이터베이스에 연결 하는 경우 올바른 Windows 사용자 계정을 데이터베이스에 로그인으로 추가 해야 합니다. 올바른 계정은 ASP.NET 개발 서버를 사용 하는지 또는 인터넷 정보 서비스를 웹 서버로 사용 하는지에 따라 달라 집니다. 또한 올바른 사용자 계정은 운영 체제에 따라 달라 집니다.

ASP.NET 개발 서버 (Visual Studio에서 사용 하는 기본 웹 서버)를 사용 하는 경우 응용 프로그램은 Windows 사용자 계정의 컨텍스트 내에서 실행 됩니다. 이 경우 Windows 사용자 계정을 데이터베이스 서버 로그인으로 추가 해야 합니다.

또는 인터넷 정보 서비스를 사용 하는 경우 ASPNET 계정 또는 NT AUTHORITY/NETWORK 서비스 계정을 데이터베이스 서버 로그인으로 추가 해야 합니다. Windows XP를 사용 하는 경우 ASPNET 계정을 데이터베이스에 로그인으로 추가 합니다. Windows Vista 또는 Windows Server 2008와 같은 최신 운영 체제를 사용 하는 경우 NT AUTHORITY/NETWORK 서비스 계정을 데이터베이스 로그인으로 추가 합니다.

Microsoft SQL Server Management Studio를 사용 하 여 데이터베이스에 새 사용자 계정을 추가할 수 있습니다 (그림 9 참조).

**그림 9-새 Microsoft SQL Server 로그인 만들기**

![clip_image018](authenticating-users-with-forms-authentication-vb/_static/image9.jpg)

필요한 로그인을 만든 후에는 올바른 데이터베이스 역할을 사용 하 여 로그인을 데이터베이스 사용자에 매핑해야 합니다. 로그인을 두 번 클릭 하 고 사용자 매핑 탭을 선택 합니다. 하나 이상의 응용 프로그램 서비스 데이터베이스 역할을 선택 합니다. 예를 들어 사용자를 인증 하기 위해 BasicAccess 데이터베이스 역할\_aspnet\_멤버 자격을 사용 하도록 설정 해야 합니다. 새 사용자를 만들려면 aspnet\_멤버 자격\_FullAccess 데이터베이스 역할을 사용 하도록 설정 해야 합니다 (그림 10 참조).

**그림 10-애플리케이션 서비스 데이터베이스 역할 추가**

![clip_image020](authenticating-users-with-forms-authentication-vb/_static/image10.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드할 때 폼 인증을 사용 하는 방법을 알아보았습니다. 먼저 웹 사이트 관리 도구를 활용 하 여 새 사용자 및 역할을 만드는 방법을 알아보았습니다. 다음에는 [권한 부여] 특성을 사용 하 여 권한이 없는 사용자가 컨트롤러 작업을 호출 하지 못하도록 하는 방법을 배웠습니다. 마지막으로, 프로덕션 데이터베이스에 사용자 및 역할 정보를 저장 하도록 MVC 응용 프로그램을 구성 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](preventing-javascript-injection-attacks-cs.md)
> [다음](authenticating-users-with-windows-authentication-vb.md)
