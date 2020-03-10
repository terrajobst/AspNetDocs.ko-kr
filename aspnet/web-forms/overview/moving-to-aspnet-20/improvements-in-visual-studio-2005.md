---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: Visual Studio 2005의 향상 된 기능 | Microsoft Docs
author: microsoft
description: Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 64215d556ded0850537a13856fe69b094116ebca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464651"
---
# <a name="improvements-in-visual-studio-2005"></a>Visual Studio 2005의 개선 사항

[Microsoft](https://github.com/microsoft) 에서

> Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다.

Visual Studio 2005는 웹 프로젝트의 향상 된 기능 및 향상 된 기능 목록을 제공 하는 웹 응용 프로그램 개발자를 제공 합니다. Visual Studio .NET 2002 및 2003의 장점은 웹 프로젝트를 처리 하는 방식에 많은 불만 사항이 있었습니다. Visual Studio 2005는 이러한 불만을 해결 하기 위해 많은 수의 새로운 기능을 추가 합니다. Visual Studio .NET 2003에서 웹 응용 프로그램의 컴파일을 처리 하는 방법을 선호 하는 경우 [웹 응용 프로그램 프로젝트](https://go.microsoft.com/fwlink/?LinkId=57870)를 참조 하세요.

이 모듈에서는 웹 프로젝트 작성, 관리 및 개발에 대 한 향상 된 기능을 다룹니다. 이후 모듈에서는 웹 프로젝트 빌드 및 배포의 향상 된 기능을 잘 다룹니다.

## <a name="frontpage-server-extensions"></a>FrontPage Server Extensions

웹 프로젝트를 만들거나 빌드하기 위해 Visual Studio .NET 2002 및 2003이 상자에 FrontPage Server Extensions. 개발자는 두 가지 액세스 모드 (FrontPage Server Extensions 또는 파일 액세스 모드) 중에서 선택 하 여 IIS에서 응용 프로그램 루트를 설정 하는 등의 작업을 수행 하는 데 FrontPage Server Extensions 사용 했습니다.

Visual Studio 2005는 로컬 프로젝트에 대 한 FrontPage Server Extensions의 의존도를 제거 합니다. 이제 Visual Studio 2005은 FrontPage Server Extensions를 사용 하는 대신 IIS 메타 베이스에 직접 액세스 합니다. Visual Studio 2005에는 FrontPage Server Extensions 없이 원격 프로젝트에 액세스할 수 있도록 하는 FTP에 대 한 지원도 추가 되었습니다.

프로젝트에서 FrontPage Server Extensions를 사용 하려는 개발자의 경우에도 옵션을 사용할 수 있습니다. 그러나 ASP.NET 개발자 커뮤니티의 강력한 피드백을 기반으로 하는 것은 요구 사항이 아닙니다.

> [!NOTE]
> 원격 프로젝트를 만들고 여는 등의 경우에도 FrontPage Server Extensions 필요 합니다.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

Visual Studio 2005는 ASP.NET 개발 서버 라는 새 웹 서버와 함께 제공 됩니다. 이 웹 서버는 이전에 Cassini로 알려져 있었습니다.

ASP.NET 개발 서버에는 여러 가지 이점이 있습니다.

- 이제 관리자가 아닌 관리자가 웹 서버에 대해 개발 하 고 디버그할 수 있습니다.
- ASP.NET 개발 서버은 유연한 프로젝트 위치를 허용 하는 파일 시스템의 임의 위치에 가상 디렉터리를 동적으로 매핑합니다.
- 이미 IIS를 사용 하 고 있는 Windows XP Professional의 사용자는 IIS에서 기본 웹 사이트의 파일 또는 폴더 구조에 영향을 주지 않는 새 웹 응용 프로그램을 만들 수 있습니다.

ASP.NET 개발 서버를 활용 하기 위해 특별 한 구성이 필요 하지 않습니다. 파일 시스템에서 호스팅되는 웹 프로젝트를 디버깅 하거나 검색할 때 Visual Studio 2005는 요청을 처리 하기 위해 임의의 포트에서 ASP.NET 개발 서버의 인스턴스를 자동으로 시작 합니다.

자세한 내용은이 모듈의 뒷부분에 나오는 ASP.NET 개발 서버에 설명 되어 있습니다.

## <a name="improved-file-management"></a>향상 된 파일 관리

Visual Studio 2002 및 2003에서는 웹 응용 프로그램의 모든 파일에 대 한 정보를 저장 하 C#는 프로젝트 파일 (VB.NET 및 .csproj의 경우 .vbproj)이 저장 됩니다. 솔루션 탐색기 표시는 프로젝트 파일의 파일 정보를 기반으로 합니다. 이로 인해 솔루션 탐색기는 외부 편집기를 사용한 경우에 부정확 한 정보를 표시 하는 경우가 많습니다. Visual Studio 2002 및 2003은 파일 변경 내용을 덮어쓰거나 파일의 최신 버전을 표시 하지 않는 경우가 많습니다.

Visual Studio 2005는 프로젝트 파일을 사용 하지 않습니다. 대신 디스크에서 직접 파일 및 폴더 정보를 읽고 프로젝트의 파일을 정확 하 게 표시 합니다. Visual Studio 2002 및 2003의 참조 폴더는 웹 응용 프로그램의 실제 폴더를 나타내지 않으므로 Visual Studio 2005는 솔루션 탐색기에서 참조 폴더를 제거 합니다. Visual Studio 2005에서 프로젝트에 대 한 참조에 액세스 하려면 프로젝트의 속성 페이지를 사용 해야 합니다.

## <a name="creating-web-projects"></a>웹 프로젝트 만들기

웹 개발자는 Visual Studio 2005에서 프로젝트를 만드는 데 사용할 수 있는 여러 가지 새로운 옵션을 제공 합니다. 이제 파일 시스템의 모든 위치에서 웹 사이트를 만들 수 있으며, 새 ASP.NET 개발 서버를 사용 하 여 디버깅 하거나 검색할 수 있습니다. 또한 개발자는 FTP를 사용 하 여 새 웹 사이트를 만들 수 있습니다.

Visual Studio 2005에서 웹 프로젝트를 만드는 비디오 연습을 보려면 여기를 클릭 하세요.

![](improvements-in-visual-studio-2005/_static/image1.png)

[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)

### <a name="file-system-projects"></a>파일 시스템 프로젝트

비디오 연습에서 살펴본 것 처럼 로컬 컴퓨터 또는 파일 공유를 통해 원격 위치에서 파일 시스템에 웹 사이트를 만들도록 선택할 수 있습니다. ASP.NET 개발 서버를 사용 하 여 파일 시스템에 생성 된 웹 사이트를 검색 하 고 디버그할 수 있습니다.

> [!NOTE]
> ASP.NET 개발 서버는 고객이 일부 혼동을 일으킬 수 있습니다. 웹 프로젝트가 IISs 디렉터리 구조 (예: c:/inetpub/wwwroot)에서 파일 시스템에 생성 되는 경우 Visual Studio 2005 내에서 시작할 때 웹 사이트는 ASP.NET 개발 서버를 통해 계속 검색 됩니다. 따라서 모든 IIS 구성 (즉, 인증 방법)은 적용 되지 않습니다.

또한 기본 웹 프로젝트는 default.aspx 페이지, default.cs 파일 및 App/_Data 폴더만 포함 하 여 많은 오버 헤드를 제거 합니다. Web.config와 특수 폴더 (즉, 앱/_code)가 필요에 따라 추가 됩니다. 웹 프로젝트에는 필요한 파일과 폴더만 포함 됩니다.

### <a name="http-projects"></a>HTTP 프로젝트

HTTP 프로젝트는 로컬 IIS 웹 사이트 또는 원격 웹 사이트에 생성 되는 프로젝트 일 수 있습니다. 기본 프로젝트 위치는 `http://localhost`입니다. 찾아보기 단추를 클릭 하면 두 가지 HTTP 옵션인 로컬 IIS와 원격 사이트가 있습니다. 이러한 두 옵션의 주요 차이점은 위치 선택 대화 상자와 웹 서버에 파일을 복사 하는 방법에 웹 사이트 정보가 표시 되는 방법입니다.

로컬 IIS 옵션은 로컬 컴퓨터의 메타 베이스에서 사이트 정보를 읽고 파일 시스템을 사용 하 여 파일을 복사 합니다. 원격 사이트 옵션은 FrontPage Server Extensions를 사용 하 고 사이트 정보 및 파일은 HTTP 및 FrontPage Server Extensions RPC 호출을 사용 하 여 복사 됩니다.

> [!NOTE]
> Vs # # #/_tmp .htm 파일 및 get/_aspx/_ver는 더 이상 버전 정보를 확인 하는 데 사용 되지 않습니다.

기본 HTTP 옵션은 로컬 IIS입니다. 이 옵션은 IIS 메타 베이스를 읽어 사용 가능한 사이트와 콘텐츠를 만들 위치를 확인 합니다. 트리 보기에서 선택 하 여 다른 폴더 또는 가상 디렉터리를 선택할 수 있습니다. 새 가상 디렉터리를 만들고, 폴더를 응용 프로그램으로 표시 하 고,이 대화 상자에서 기존 가상 디렉터리를 삭제할 수도 있습니다.

![위치 선택 대화 상자](improvements-in-visual-studio-2005/_static/image1.gif)

**그림 1**: 위치 선택 대화 상자

이전 버전의 Visual Studio와 달리 **SSL(Secure Sockets Layer) 사용** 확인란을 선택 하 고 SSL 인증서가 검색 중인 URL과 일치 하지 않는 경우 계속할지 여부를 묻는 보안 경고 대화 상자가 표시 됩니다. Visual Studio .NET 2003을 사용 하 여 인증서가 일치 하는 인증서가 아닌 경우 프로젝트를 만들 수 없습니다.

![SSL 인증서에 대 한 보안 경고](improvements-in-visual-studio-2005/_static/image2.gif)

**그림 2**: SSL 인증서에 대 한 보안 경고

### <a name="note-on-host-headers"></a>호스트 헤더에 대 한 참고

특정 IP에 바인딩된 사이트에서 웹 응용 프로그램을 만드는 경우 호스트 헤더가 구성 되어 있는지 확인 해야 합니다. 그렇지 않으면 Visual Studio는 `http://localhost`에서 사이트를 만들지만 IDE 내에서 사이트를 검색 하거나 디버그할 때 IP 주소는 올바르게 확인 되지 않습니다.

원격 사이트 옵션을 선택 하는 경우 대화 상자를 변경 하 여 새 웹 사이트의 대상 URL을 입력할 수 있습니다. 이 URL은 FrontPage Server Extensions 사용 하도록 설정 된 서버에 있어야 합니다. FrontPage Server Extensions를 사용 하 여 로컬 웹 서버를 사용 하려는 경우 원격 사이트 옵션을 사용 하 고 로컬 URL을 지정할 수 있습니다.

![원격 서버에서 웹 사이트 만들기](improvements-in-visual-studio-2005/_static/image1.jpg)

**그림 3**: 원격 서버에 웹 사이트 만들기

SSL을 통해 원격 사이트에서 응용 프로그램을 만들 때 SSL 인증서가 일치 하지 않으면 로컬 IIS 옵션을 사용할 때 표시 되는 대화 상자와는 확인 대화 상자가 약간 다릅니다.

![원격 사이트 보안 경고](improvements-in-visual-studio-2005/_static/image3.gif)

**그림 4**: 원격 사이트 보안 경고

<a id="_Toc116100243"></a>

#### <a name="ftp"></a>FTP

Visual Studio 2005에서는 FTP를 통해 웹 사이트를 만드는 옵션을 소개 합니다. 이 옵션을 사용 하는 경우 IDE는 사용자 임시 폴더에 로컬로 파일을 만든 다음 FTP를 사용 하 여 FTP 위치로 파일을 이동 합니다.

> [!NOTE]
> 임시 폴더 위치는 c:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;응용 프로그램 이름&gt;

FTP 옵션을 사용 하는 경우 위치 선택 대화 상자가 표시 됩니다. 아래와 같이 필요한 FTP 연결 정보를이 대화 상자에 입력 합니다.

![FTP에 대 한 위치 선택 대화 상자](improvements-in-visual-studio-2005/_static/image2.jpg)

**그림 5**: FTP에 대 한 위치 선택 대화 상자

## <a name="lab-setup-ftp-site-and-create-a-project"></a>랩: FTP 사이트를 설정 하 고 프로젝트 만들기

다음 단계는 ftp 사이트를 구성 하 여 사용자가 FTP를 통해 업로드할 수 있는 위치를 갖도록 합니다.

### <a name="install-the-ftp-service"></a>FTP 서비스 설치

1. 프로그램 추가/제거를 열고 Windows 구성 요소 추가/제거를 선택 합니다.
2. 인터넷 정보 서비스 (Windows 2003의 응용 프로그램 서버)를 선택 하 고 **세부 정보**를 클릭 합니다.
3. **파일 전송 프로토콜 (FTP) 서비스** 를 확인 하 고 **확인**을 클릭 합니다.
4. **다음** 을 클릭 하 여 FTP 서비스를 설치 합니다.

### <a name="create-a-new-folder-for-content"></a>콘텐츠에 대 한 새 폴더 만들기

1. Windows 탐색기에서 c:/inetpub/wwwroot 내부에 **User1** 이라는 새 폴더를 만듭니다.

#### <a name="configure-folders-and-permissions-on-folders"></a>폴더 및 폴더에 대 한 사용 권한을 구성 합니다.

1. 관리 도구에서 인터넷 정보 서비스 스냅인을 엽니다. 이제 컴퓨터 이름 노드 아래에 FTP 사이트 폴더가 표시 됩니다.
2. **FTP 사이트**를 확장 합니다.
3. **기본 FTP 사이트**를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**, **가상 디렉터리**를 차례로 선택한 후 **다음**을 클릭 합니다.
4. 가상 디렉터리 이름으로 **User1** 을 입력 하 고 **다음**을 클릭 합니다.
5. 경로에 **c:/inetpub/wwwroot/User1** 을 입력 하 고 **다음**을 클릭 합니다.
6. **다음** 을 클릭 하 고 **마침** 을 클릭 하 여 마법사를 완료 합니다.
7. 기본 FTP 사이트에서 **User1** 가상 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.
8. **쓰기** 확인란을 선택 하 고 **확인** 을 클릭 하 여 대화 상자를 닫습니다.
9. **기본 FTP 사이트** 를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.
10. **보안 계정** 탭에서 **익명 연결 허용**을 선택 취소 합니다.
11. 계속할 것인지 묻는 대화 상자에서 **예** 를 클릭 합니다.
12. **확인**을 클릭하여 대화 상자를 닫습니다.
13. **웹 사이트** 노드 아래에서 **기본 웹 사이트** 를 확장 합니다.
14. **User1** 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 선택 합니다.
15. **응용 프로그램 설정** 섹션에서 **만들기** 를 클릭 하 여 폴더를 응용 프로그램으로 표시 합니다.
16. **확인**을 클릭하여 대화 상자를 닫습니다.
17. 인터넷 정보 서비스 스냅인을 닫습니다.

### <a name="create-web-project"></a>웹 프로젝트 만들기

1. Visual Studio 2005을 엽니다.
2. **파일** 메뉴에서 **새 웹 사이트**를 선택 합니다.
3. **위치** 드롭다운에서 **FTP**를 선택 합니다.
4. **찾아보기**를 클릭합니다.
5. **서버** 텍스트 상자에 **localhost** 를 입력 합니다.
6. 디렉터리 텍스트 상자에 **User1** 을 입력 합니다.
7. **열기**를 클릭합니다. FTP 위치가 새 웹 사이트 대화 상자에 입력 됩니다.
8. **확인**을 클릭합니다.
9. FTP 로그온 대화 상자에서 **익명 로그온** 을 선택 취소 하 고 자격 증명을 입력 한 다음 **확인**을 클릭 합니다.
10. 프로젝트에 대 한 URL은 무엇 인가요? 프로젝트에 대 한 URL은 솔루션 탐색기 표시 됩니다.
11. **빌드** 메뉴에서 **웹 사이트 빌드** 또는 **솔루션 빌드**를 선택 합니다.
12. 솔루션 탐색기에서 default.aspx를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택 합니다.
13. 웹 사이트 URL 필요 대화 상자에서 URL에 `http://localhost/user1`를 입력 하 고 **확인**을 클릭 합니다.

> [!NOTE]
> 형식/_Default를 로드할 수 없음을 나타내는 오류가 발생 하는 경우 웹 사이트에서 ASP.NET 2.0를 실행 하 고 있고 이전 버전은 실행 하 고 있지 않은지 확인 하세요. 인터넷 정보 서비스의 ASP.NET 탭에서이 작업을 수행할 수 있습니다.

## <a name="opening-web-projects"></a>웹 프로젝트 열기

웹 프로젝트를 여는 것은 프로젝트를 만드는 것과 비슷합니다. 다음 섹션에서는 IDE 내에서 작업 하는 동안에 대 한 영역을 유지 하기 위한 영역을 호출 합니다. 또한 HTTP 및 FTP를 사용 하 여 웹 프로젝트 작업을 다룹니다.

웹 프로젝트를 열려면 파일 메뉴에서 웹 사이트 열기를 선택 합니다. 이전에 설명한 것과 동일한 위치 선택 대화 상자가 표시 되며, 파일 시스템, 로컬 IIS, FTP 및 원격 사이트와 같은 네 가지 옵션을 사용할 수 있습니다.

<a id="_Toc116100245"></a>

## <a name="file-system"></a>파일 시스템

이 모듈의 앞에서 설명한 것 처럼 Visual Studio에서는 더 이상 프로젝트 파일을 사용 하지 않습니다. 따라서 파일 시스템에서 웹 사이트를 열도록 선택 하는 경우에는 선택한 폴더가 Visual Studio에서 처음에 웹 프로젝트로 생성 되지 않은 경우에도 원하는 폴더를 선택할 수 있습니다. 예를 들어 내 문서 폴더를 웹 사이트로 열도록 선택할 수 있습니다. 그러면 Visual Studio에서 해당 폴더를 열고 아래와 같이 파일을 표시 합니다.

![웹 사이트로 열린 내 문서](improvements-in-visual-studio-2005/_static/image3.jpg)

**그림 6**: 웹 사이트로 열린 *내 문서*

Visual Studio는 필요한 경우에만 추가 파일 및 폴더를 만들기 때문에 사용자가 여는 위치에 추가 파일이 나 폴더가 추가 되지 않습니다. 이 아키텍처의 부작용은 파일 시스템에서 웹 사이트를 중첩 하지 못하도록 하는 것입니다. 예를 들어 다음 디렉터리 구조를 살펴보세요.

C:/MyWebSite의 웹 프로젝트

C:/MyWebSite/Nested의 다른 웹 프로젝트

C:/MyWebSite에서 웹 사이트를 열면 중첩 된 폴더가 해당 응용 프로그램의 하위 폴더로 표시 됩니다.

<a id="_Toc116100246"></a>

## <a name="http"></a>HTTP

HTTP를 통해 웹 사이트를 열 때 IIS 메타 베이스 (로컬 IIS) 또는 FrontPage Server Extensions (원격 사이트)를 사용 하 여 설정을 읽습니다. 중첩 된 웹 응용 프로그램이 있는 경우 이러한 응용 프로그램을 응용 프로그램으로 식별 하는 아이콘으로 표시 됩니다. FrontPage에서 웹 응용 프로그램을 사용 하는 방법을 잘 알고 있다면 Visual Studio 2005의 동작이 비슷합니다.

Visual Studio는 현재 IDE 내에서 열려 있는 응용 프로그램 아래에 중첩 된 응용 프로그램에 대 한 아이콘을 표시 하지만 해당 콘텐츠를 볼 수 있도록 확장할 수는 없습니다. 그러나 해당 항목을 두 번 클릭 하 여 열 수 있습니다. 이렇게 하면 웹 응용 프로그램을 열 수 있는 대화 상자가 표시 되 고 (현재 열려 있는 솔루션을 대체 함) 웹 응용 프로그램을 현재 솔루션에 추가 하 라는 대화 상자가 표시 됩니다.

![중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자가 표시 됩니다.](improvements-in-visual-studio-2005/_static/image4.jpg)

**그림 7**: 중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자가 표시 됩니다.

<a id="_Toc116100247"></a>

## <a name="ftp-site"></a>FTP 사이트

FTP를 통해 사이트를 열 때 파일은 모두 임시 폴더에 로컬로 복사 됩니다. 로컬 저장소 위치의 전체 경로는 프로젝트에 대 한 속성 창에 표시 되며 다음 형식을 사용 하 여 만들어집니다.

C:/Documents and Settings/&lt;User&gt;/Local Settings/Temp/VWDWebCache/&lt;Server&gt;/_&lt;응용 프로그램 이름&gt;

FTP를 사용 하는 경우 Visual Studio는 아래와 같이 찾아볼 수 있도록 프로젝트의 기본 URL을 지정 해야 합니다. 기본 URL을 지정 하지 않으면 웹 사이트의 페이지를 처음으로 탐색 하려고 할 때 Visual Studio에서 해당 URL을 요청 합니다.

![FTP 사이트에 대 한 기본 URL 지정](improvements-in-visual-studio-2005/_static/image5.jpg)

**그림 8**: FTP 사이트에 대 한 기본 URL 지정

## <a name="improvements-in-compilation"></a>컴파일의 향상 된 기능

Visual Studio 2005에서 웹 응용 프로그램을 사용 하는 것은 이전 버전 보다 훨씬 빠릅니다. 이는 컴파일 아키텍처의 변경 내용에 대 한 부분이 많지 않기 때문입니다.

Visual Studio 2002 및 2003에서 웹 응용 프로그램은 웹 응용 프로그램 폴더에 상주 하는 하나의 주 어셈블리로 컴파일됩니다. Visual Studio 2005에서 앱/_Code 폴더가 추가 되었습니다. 클래스 및 기타 비 UI 코드는 App/_Code 폴더에 추가 됩니다. Visual Studio에서 프로젝트를 빌드하면 App/_Code 폴더의 모든 파일이 단일 앱/_Code .dll 파일로 컴파일됩니다. 이러한 변경으로 인해 이후 빌드는 이전 버전 보다 훨씬 더 빠릅니다.

> [!NOTE]
> MSBuild 명령줄 유틸리티를 사용 하 여 ASP.NET 웹 응용 프로그램을 빌드할 수도 있습니다. 이 도구는 모듈 9에서 다룹니다.

또 다른 컴파일 기능은 빌드 메뉴의 새 빌드 페이지 옵션입니다. 이 기능을 사용 하면 개발자는 변경 내용을 보다 신속 하 게 컴파일할 수 있도록 현재 페이지 (물론, 및 종속성)만 다시 빌드할 수 있습니다. 는 C# intellisense를 업데이트할 목적으로 백그라운드 컴파일을 제공 하지 않기 때문에이 기능을 사용 하면 단일 페이지를 간단 하 게 다시 작성 하 여 intellisense를 빠르게 업데이트할 수 있으므로이 기능을 사용 하는 것은 매우 유용 합니다.

프로젝트에 대 한 빌드 속성을 사용 하 여 시작 페이지를 실행 하기 전에 발생 하는 빌드 유형을 구성할 수 있습니다. 개발자는 Visual Studio에서 코드 변경 후 더 빠르게 응용 프로그램 디버깅을 시작할 수 있도록 현재 페이지만 빌드하도록 선택할 수 있습니다.

![빌드 페이지 시작 작업](improvements-in-visual-studio-2005/_static/image6.jpg)

**그림 9**: 빌드 페이지 시작 작업

Visual Studio 및 ASP.NET 아키텍처의 또 다른 향상 된 기능은 편집 하며 계속 하기 영역에 있습니다. Visual Studio 2005에서 개발자는 프로젝트 디버깅을 시작 하 고 디버거를 분리 하지 않고 프로젝트에서 코드를 변경할 수 있습니다. 실제로 디버거를 분리 하지 않고 프로젝트 디버깅을 시작 하 고, 새 클래스를 추가 하 고, 해당 클래스에 코드를 추가 하 고, 해당 클래스의 새 인스턴스를 만들고 클래스의 메서드를 실행 하는 코드를 페이지에 추가할 수 있습니다. 새 코드를 실행 하는 것은 브라우저를 새로 고치는 것 만큼 쉽습니다.

Visual Studio 2005에서 편집 하며 계속 하기 기능의 비디오 연습을 보려면 여기를 클릭 하세요.

![](improvements-in-visual-studio-2005/_static/image2.png)

[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)

ASP.NET 2.0 및 Visual Studio 2005의 강력한 편집 및 계속 기능은 ASP.NET 응용 프로그램에 대 한 아키텍처 변경 때문에 발생 합니다. ASP.NET 1.x에서 Visual Studio 2002/2003에서 만든 응용 프로그램은 해당 응용 프로그램 폴더에 저장 된 주 어셈블리로 컴파일됩니다. 응용 프로그램의 모든 클래스, 페이지 등은 해당 DLL로 컴파일 되었습니다. 그런 다음 런타임에 ASP.NET는 모든 컨트롤, 태그 및 ASP.NET 코드를 페이지 내에서 컴파일하고 이러한 Dll을 ASP.NET 임시 폴더에 복사 합니다.

Visual Studio 2005에서 ASP.NET 2.0을 사용 하는 경우 위의 두 가지 컴파일 모델 개요 (Visual Studio 용 one 개와 런타임에 하나는 ASP.NET)가 하나의 일반적인 컴파일 모델에 병합 되었습니다. 즉, 모든 컴파일 문제는 이제 런타임 대신 개발 단계에서 catch 됩니다. 또한 사용자 컨트롤 및 마스터 페이지와 같은 기능에 대 한 디자이너 및 IntelliSense 지원을 사용할 수 있습니다.

사용자 정의 컨트롤에 대 한 디자이너 지원 비디오 연습을 보려면 여기를 클릭 하세요.

![](improvements-in-visual-studio-2005/_static/image3.png)

[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)

> [!NOTE]
> 사용자 정의 컨트롤이 페이지에서 제거 되 면 @Register 지시문은 태그에 남아 있으므로 사용자 정의 컨트롤이 웹 사이트에서 삭제 되는 경우 파서 오류를 방지 하기 위해 수동으로 제거 해야 합니다.

Visual Studio 컴파일 모델의 또 다른 향상 된 기능은 웹 사이트 게시 기능입니다. 게시 기능은 웹 사이트를 미리 컴파일하 므로 개발자는 필요에 따라 아무것도 컴파일하지 않고도 추가 된 성능을 누릴 수 있습니다. 또한 응용 프로그램/_Code 폴더의 모든 소스 코드를 DLL로 미리 컴파일하며 소스 코드를 배포할 필요가 없습니다.

![웹 사이트 게시 대화 상자](improvements-in-visual-studio-2005/_static/image7.jpg)

**그림 10**: 웹 사이트 게시 대화 상자

> [!NOTE]
> Aspnet/_compile 유틸리티를 사용 하 여 ASP.NET 웹 응용 프로그램을 미리 컴파일할 수도 있습니다. 이 도구는 모듈 9에서 다룹니다.

웹 사이트를 게시할 때 미리 컴파일된 파일은 아래와 같이 임시 ASP.NET Files 폴더에 저장 됩니다. 파일 확장명이 *.compiled* 인 파일은 특정 dll에 대 한 종속성을 정의 하는 XML 파일입니다. 모든 Webform 또는 사용자 정의 컨트롤은 *App/_Web/_* 로 시작 하는 임의의 dll로 컴파일됩니다.

*미리 컴파일된이 사이트를 업데이트할 수 있도록 허용* 확인란을 선택 하지 않으면 Webforms 및 사용자 정의 컨트롤 내부의 태그가 DLL로 미리 컴파일되지 않으므로 배포 후에 변경 내용을 적용할 수 있습니다. 배포 된 콘텐츠를 변경할 수 없도록 태그를 잠그려면이 확인란의 선택을 취소 합니다.

*고정 이름 지정 및 단일 페이지 어셈블리 사용* 확인란을 사용 하면 각 페이지가 고정 된 이름의 어셈블리로 컴파일되도록 일괄 컴파일을 사용 하지 않도록 설정할 수 있습니다. 이 확인란을 선택 하지 않은 상태로 두면 일괄 컴파일을 활용할 수 있습니다.

*미리 컴파일된 어셈블리에서 강력한 이름 지정* 확인란을 사용 하면 미리 컴파일된 어셈블리를 강력한 이름으로 지정할 수 있습니다.

> [!NOTE]
> ASP.NET 1.x에서 강력한 이름의 어셈블리는 GAC (전역 어셈블리 캐시)에 설치 되어야 합니다. ASP.NET 2.0에서는 강력한 이름의 어셈블리를 GAC에 설치할 필요가 없습니다.

![ASP.NET 응용 프로그램 미리 컴파일된 파일](improvements-in-visual-studio-2005/_static/image8.jpg)

**그림 11**: 미리 컴파일된 파일 ASP.NET 응용 프로그램

> [!NOTE]
> 위의 응용 프로그램에 web.config 파일이 없습니다. 웹 사이트를 게시 한 후에는 *PrecompiledApp* 가 호출 된 것입니다.

## <a name="improvements-in-deployment"></a>배포의 향상 된 기능

Visual Studio 2002 및 2003와 마찬가지로 Visual Studio 2005는 프로젝트 복사 기능을 제공 합니다. 그러나이 기능은 Visual Studio 2005에 포함 되어 있으며 이제 웹 사이트 복사 라고 합니다.

웹 사이트 복사 대화 상자는 왼쪽 프레임 및 오른쪽 프레임으로 분할 됩니다. 왼쪽 프레임을 원본 웹 사이트 라고 하며, 오른쪽 프레임을 원격 웹 사이트 라고 합니다. 일부 개발자와 혼동 될 수 있는 한 가지는 오른쪽 프레임에 표시 되는 사이트가 반드시 원격 사이트 일 필요는 없다는 점입니다. 로컬 파일 시스템 또는 IIS의 로컬 인스턴스에 있는 사이트 일 수 있습니다. 또한 대화 상자를 사용 하 여 원격 *웹 사이트에서* 원본 웹 사이트로 게시할 수 있으므로 왼쪽 프레임에 표시 되는 사이트는 반드시 원본 웹 사이트가 될 필요는 없습니다.

프로젝트를 원격 웹 사이트에 복사 하는 경우 해당 사이트에 FrontPage Server Extensions 설치 되어 있어야 합니다. 그렇지 않은 경우 FTP를 사용 하 여 연결 해야 합니다. 반면, 프로젝트를 로컬 IIS 인스턴스에 복사 하는 경우 FrontPage Server Extensions 필요 하지 않습니다.

> [!NOTE]
> 로컬 IIS 인스턴스에서 새 웹 사이트를 만들려고 하 고 FrontPage 2002 Server Extensions가 설치 된 경우 SharePoint 서버에서 웹 사이트를 만드는 것이 지원 되지 않음을 알리는 오류 메시지가 표시 됩니다. 이 경우 FrontPage 2000 서버 확장을 설치 하거나 FrontPage Server Extensions를 제거 하는 옵션이 있습니다.

웹 사이트 복사 기능의 비디오 연습을 보려면 여기를 클릭 하세요.

![](improvements-in-visual-studio-2005/_static/image4.png)

[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/copysite1.wmv)

## <a name="improvements-in-debugging"></a>디버깅의 향상 된 기능

Visual Studio 2005의 디버깅에는 네 가지 주요 향상 기능이 있습니다.

- 관리자가 아닌 관리자로 로컬로 디버그할 수 있습니다.
- 컴파일 요소의 Debug 특성은 이제 기본적으로 false입니다.
- 원격 디버깅을 설치 하 고 구성 하는 것이 이전 보다 쉬워졌습니다.
- 이제 FTP 위치를 통해 열린 웹 사이트를 디버그할 수 있습니다.

## <a name="debugging-as-a-non-administrator"></a>비관리자로 디버깅

ASP.NET 개발 서버를 추가 하 여 관리자가 아닌 ASP.NET 응용 프로그램을 즉시 쉽게 디버그할 수 있습니다. 로컬 파일 시스템에서 실행 되는 ASP.NET 응용 프로그램을 디버그 하는 경우 Visual Studio는 로그온 한 사용자의 컨텍스트에서 ASP.NET 개발 서버를 시작 합니다. 그러면 해당 사용자가 추가 구성 없이 해당 응용 프로그램을 디버그할 수 있습니다.

## <a name="debug-is-false-by-default"></a>디버그는 기본적으로 False입니다.

ASP.NET 1.x에서 web.config 파일의 *컴파일* 요소에 있는 *debug* 특성은 기본적으로 *true* 로 설정 되었습니다. 개발자는 응용 프로그램을 프로덕션에 배포 하기 전에이 특성을 *false* 로 설정 하는 것이 항상 권장 됩니다. 그러나 대부분의 개발자는 debug 특성을 true로 설정 된 상태로 유지 하는 결과를 완전히 이해 하지 못하기 때문에 단순히 그대로 둡니다.

Debug 특성을 true로 설정 하는 경우 가장 심각한 문제는 안전망 batch 컴파일 모델을 사용 하지 않도록 설정 하는 것입니다. 따라서 각 페이지는 별도의 DLL로 컴파일됩니다. 웹 응용 프로그램이 수천 개의 페이지로 구성 된 경우 (어떤 방법으로도 적도 되지 않음) 해당 응용 프로그램에서 수천 개의 작은 Dll이 생성 됩니다. 이러한 Dll의 크기는 작지만 메모리의 특정 위치로 로드 되지 않습니다. 따라서 시스템 메모리에서 조각화를 발생 하 고 OutOfMemoryException 발생에 기여할 수 있습니다.

ASP.NET 2.0에서 debug 특성은 기본적으로 false로 설정 됩니다. 앞서 살펴본 바와 같이 개발자가 Visual Studio 2005에서 ASP.NET 응용 프로그램을 디버그할 때 디버깅을 사용 하도록 설정 된 web.config 파일을 추가 하 라는 메시지가 표시 됩니다. 이렇게 하면 ASP.NET 1.x에 있는 것과 동일한 단점이 발생 하지만, 이제 응용 프로그램을 프로덕션 환경으로 이동 하기 전에 개발자에 게 특성을 false로 다시 설정 해야 한다는 경고 메시지가 표시 됩니다.

## <a name="remote-debugging-setup-and-configuration"></a>원격 디버깅 설정 및 구성

Visual Studio 2002/2003에서 원격 디버깅은 컴퓨터 디버그 관리자 (mdm .exe) 및 vs7jit 프로세스에 의존 합니다. 이로 인해 원격 디버깅 문제를 해결 하는 것은 종종 고객을 위한 블랙 박스 이며 PSS의 경우 훨씬 더 좋은 경우가 많았습니다.

Visual Studio 2005는 mdm .exe 및 vs7jit 프로세스에 대 한 의존도를 제거 합니다. 대신, 이제 원격 디버그 모니터 서비스 (msvsmon.exe)를 사용 합니다.

Visual Studio 2005 원격으로 디버깅 하는 데 필요한 요구 사항은 매우 간단 합니다. 디버깅 하기 전에 원격 서버에서 msvsmon.exe를 실행 해야 합니다. Visual Studio CD에서 원격 디버그 모니터를 설치 하거나, 웹 서버에 아무것도 설치 하지 않고 공유에서 msvsmon.exe를 실행 하기만 하면 됩니다.

Msvsmon.exe를 실행 하는 경우 원격 디버깅을 위해 차단 되는 포트에 대 한 문제가 발생할 수 있습니다. 다행히 아래와 같이 경고 대화 상자 내에서 적절 한 포트를 쉽게 차단 해제할 수 있습니다.

![Windows 방화벽이 원격 디버깅을 차단 하 고 있음을 알립니다.](improvements-in-visual-studio-2005/_static/image9.jpg)

**그림 12**: Windows 방화벽이 원격 디버깅을 차단 한다는 알림

디버깅에 필요한 포트를 차단 해제 한 후에는 아래와 같이 원격 디버깅 모니터 표시 됩니다. 이 인터페이스에서 연결을 모니터링 하 고 디버깅 권한을 쉽게 변경할 수 있습니다.

![원격 디버깅 모니터](improvements-in-visual-studio-2005/_static/image10.jpg)

**그림 13**: 원격 디버깅 모니터

FTP를 통해 열린 웹 응용 프로그램을 원격으로 디버그할 수도 있습니다. 단계는 앞에서 설명한 것과 동일 합니다. 그러나이 모듈의 앞부분에서 설명한 대로 FTP 프로젝트를 검색 하는 데 사용할 기본 URL을 지정 해야 합니다.

## <a name="lab-2"></a>랩 2

## <a name="remote-debugging-with-visual-studio-2005"></a>Visual Studio 2005을 사용 하 여 원격 디버깅

이 랩에서는 Visual Studio 2005을 사용 하 여 원격으로 디버깅 하는 과정을 안내 합니다.

이 랩의 비디오 연습을 보려면 여기를 클릭 하세요.

![](improvements-in-visual-studio-2005/_static/image5.png)

[전체 화면 비디오 열기](improvements-in-visual-studio-2005/_static/remdebug1.wmv)

이 랩에서는 두 대의 컴퓨터가 있어야 합니다. 하나는 Visual Studio 2005를 실행 하 고 다른 하나는 IIS를 실행 하는 경우입니다.

1. Visual Studio 2005을 열고 원격 서버에 새 웹 사이트를 만듭니다.

> [!NOTE]
> 원격 IIS 인스턴스나 FTP를 통해 웹 사이트를 만들 수 있습니다.

1. 원격 웹 서버에서 UNC 경로를 사용 하 여 개발 컴퓨터의 msvsmon.exe를 찾아 실행 합니다.  
 Msvsmon.exe의 기본 위치는 server/c $/Program Files/Microsoft Visual Studio 8/Common7/IDE/원격 디버거/x86입니다.
2. 원격 디버깅을 위해 포트를 차단 해제 하 라는 메시지가 표시 되 면이를 수행 합니다.
3. 개발 컴퓨터에서 default.aspx에 대 한 코드 숨김으로 열고 페이지/_Load 메서드에서 중단점을 설정 합니다.
4. 개발 컴퓨터에서 디버깅을 시작 합니다.

중단점은 예상 대로 적중 해야 합니다.

## <a name="aspnet-development-server"></a>ASP.NET Development Server

이미 논의 한 대로 Visual Studio 2005는 ASP.NET 개발 서버 라는 웹 서버와 함께 제공 됩니다. ASP.NET 개발 서버는 경우에 따라 Cassini 라고도 합니다. 이 웹 서버는 파일 시스템에서 실행 되는 웹 응용 프로그램을 찾아보고 디버그 하는 편리한 방법입니다.

ASP.NET 개발 서버 제한 된 웹 서버입니다. 원격 연결을 허용 하지 않습니다. 웹 서버를 시작한 사용자가 아닌 다른 사용자의 요청은 허용 되지 않습니다. 또한 ASP 페이지를 제공할 수 있는 기능이 없습니다. ASP.NET 리소스와 HTML 리소스 (이미지, CSS 파일 등 포함)만 제공 됩니다.

C:/Windows/Microsoft .NET/Framework/v2.0/ */* / */* /*에 있는 webdev .exe 파일을 실행 하 여 명령줄을 통해 ASP.NET 개발 서버를 시작할 수 있습니다. 다음 대화 상자에는 사용할 수 있는 매개 변수가 표시 됩니다.

![](improvements-in-visual-studio-2005/_static/image11.jpg)

**그림 14**

> [!NOTE]
> 명령줄을 통해 명시적으로 시작 된 경우에는 ASP.NET 개발 서버 지원 되지 않습니다.
