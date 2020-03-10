---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 새 ASP.NET MVC 프로젝트 만들기 | Microsoft Docs
author: microsoft
description: 1 단계에서는 기본 사용자 Ddddinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469241"
---
# <a name="create-a-new-aspnet-mvc-project"></a>새 ASP.NET MVC 프로젝트 만들기

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 1 단계입니다.
> 
> 1 단계에서는 기본 사용자 Ddddinner 응용 프로그램 구조를 배치 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner 1 단계: 파일&gt;새 프로젝트

Visual Studio 2008 또는 무료 Visual Web Developer 2008 Express 내에서 **파일-&gt;새 프로젝트** 메뉴 항목을 선택 하 여 공동으로 사용 하는 ddinner 응용 프로그램을 시작 합니다.

그러면 "새 프로젝트" 대화 상자가 표시 됩니다. 새 ASP.NET MVC 응용 프로그램을 만들려면 대화 상자 왼쪽에 있는 "웹" 노드를 선택 하 고 오른쪽에 있는 "ASP.NET MVC 웹 응용 프로그램" 프로젝트 템플릿을 선택 합니다.

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*중요: ASP.NET MVC를 다운로드 하 고 설치 했는지 확인 하세요. 그렇지 않으면 새 프로젝트 대화 상자에 표시 되지 않습니다. [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx) 를 아직 설치 하지 않은 경우 V2를 사용할 수 있습니다. ASP.NET MVC는 "웹 플랫폼-&gt;프레임 워크 및 런타임" 섹션에서 사용할 수 있습니다.*

새 프로젝트의 이름을 "NerdDinner"로 지정한 다음 "확인" 단추를 클릭 하 여 만듭니다.

"확인"을 클릭 하면 Visual Studio에서 선택적으로 새 응용 프로그램에 대 한 단위 테스트 프로젝트를 만들라는 메시지를 표시 하는 추가 대화 상자를 표시 합니다. 이 단위 테스트 프로젝트를 사용 하면 응용 프로그램의 기능 및 동작을 확인 하는 자동화 된 테스트를 만들 수 있습니다 (이 자습서의 뒷부분에서 수행 하는 방법에 대해 설명).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

위의 대화 상자에 있는 "테스트 프레임 워크" 드롭다운에는 컴퓨터에 설치 된 사용 가능한 모든 ASP.NET MVC 단위 테스트 프로젝트 템플릿으로 채워집니다. NUnit, MBUnit 및 XUnit에 대해 버전을 다운로드할 수 있습니다. 기본 제공 Visual Studio 단위 테스트 프레임 워크도 지원 됩니다.

*참고: visual Studio 단위 테스트 프레임 워크는 Visual Studio 2008 Professional 이상 버전 에서만 사용할 수 있습니다. VS 2008 Standard Edition 또는 Visual Web Developer 2008 Express를 사용 하는 경우이 대화 상자가 표시 되려면 ASP.NET MVC 용 NUnit, MBUnit 또는 XUnit 확장을 다운로드 하 여 설치 해야 합니다. 테스트 프레임 워크가 설치 되지 않은 경우 대화 상자에 표시 되지 않습니다.*

만든 테스트 프로젝트에 대 한 기본 "가 나 Ddinner. 테스트" 이름을 사용 하 고 "Visual Studio 단위 테스트" 프레임 워크 옵션을 사용 합니다. "확인" 단추를 클릭 하면 Visual Studio에서 웹 응용 프로그램을 위한 프로젝트와 단위 테스트에 대해 하나씩 두 개의 프로젝트를 포함 하는 솔루션을 만듭니다.

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>해당 하는 NerdDinner 디렉터리 구조 검사

Visual Studio를 사용 하 여 새 ASP.NET MVC 응용 프로그램을 만들면 프로젝트에 많은 파일 및 디렉터리가 자동으로 추가 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image4.png)

ASP.NET MVC 프로젝트에는 기본적으로 다음 6 개의 최상위 디렉터리가 있습니다.

| **디렉터리** | **용도** |
| --- | --- |
| **/컨트롤러** | URL 요청을 처리 하는 컨트롤러 클래스를 배치 하는 위치 |
| **/모델** | 데이터를 나타내고 조작 하는 클래스를 배치 하는 위치 |
| **/Views** | 출력 렌더링을 담당 하는 UI 템플릿 파일을 배치 하는 위치 |
| **/Scripts** | JavaScript 라이브러리 파일 및 스크립트 (.js)를 배치 하는 위치 |
| **/콘텐츠** | CSS 및 이미지 파일을 저장 하는 위치 및 기타 비-동적/비 JavaScript 콘텐츠 |
| **/앱\_데이터** | 읽기/쓰기가 필요한 데이터 파일을 저장 하는 위치입니다. |

ASP.NET MVC는이 구조체를 요구 하지 않습니다. 실제로, 많은 응용 프로그램에서 작업 하는 개발자는 일반적으로 여러 프로젝트에서 응용 프로그램을 분할 하 여 보다 쉽게 관리할 수 있습니다. 예를 들어 데이터 모델 클래스는 대개 웹 응용 프로그램에서 별도의 클래스 라이브러리 프로젝트에 있습니다. 그러나 기본 프로젝트 구조는 응용 프로그램의 문제를 해결 하는 데 사용할 수 있는 유용한 기본 디렉터리 규칙을 제공 합니다.

/Controllers 디렉터리를 확장 하면 Visual Studio에서 기본적으로 프로젝트에 두 개의 컨트롤러 클래스인 HomeController 및 AccountController가 추가 된 것을 알 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image5.png)

/Sarys 디렉터리를 확장할 때/Home,/Account 및/Sshared 라는 세 개의 하위 디렉터리와 그 안에 포함 된 몇 가지 템플릿 파일도 프로젝트에 기본적으로 추가 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image6.png)

/Cer\\scripts 디렉터리를 확장 하면 응용 프로그램 내에서 ASP.NET AJAX 및 jQuery 지원을 사용할 수 있는 JavaScript 라이브러리 뿐만 아니라 사이트의 모든 HTML 스타일에 사용 되는 사이트 .css 파일을 찾을 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image7.png)

팀 프로젝트를 확장할 때 컨트롤러 클래스에 대 한 단위 테스트를 포함 하는 두 개의 클래스를 찾을 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio에서 추가 된 이러한 기본 파일은 작업 중인 응용 프로그램에 대 한 기본 구조를 제공 합니다. 홈 페이지, 정보 페이지, 계정 로그인/로그 아웃/등록 페이지 및 처리 되지 않은 오류 페이지 (모든 연결 및 사용)를 제공 합니다.

### <a name="running-the-nerddinner-application"></a>가 중 Ddinner 응용 프로그램 실행

**디버그&gt;디버깅 시작** 또는 **디버그-&gt;시작** 메뉴 항목을 선택 하 여 프로젝트를 실행할 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image9.png)

그러면 Visual Studio와 함께 제공 되는 기본 제공 ASP.NET 웹 서버가 시작 되 고 응용 프로그램이 실행 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image10.png)

다음은 실행 시 새 프로젝트 (URL: "/")의 홈 페이지입니다.

![](create-a-new-aspnet-mvc-project/_static/image11.png)

"정보" 탭을 클릭 하면 정보 페이지 (URL: "/Home/About")가 표시 됩니다.

![](create-a-new-aspnet-mvc-project/_static/image12.png)

오른쪽 위에 있는 "로그온" 링크를 클릭 하면 로그인 페이지로 이동 합니다 (URL: "/Account/dvlogs").

![](create-a-new-aspnet-mvc-project/_static/image13.png)

로그인 계정이 없는 경우 등록 링크를 클릭 하 여 (URL: "/Account/dv/register") 다음을 만들 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image14.png)

위의 홈, 정보 및 로그 아웃/등록 기능을 구현 하는 코드는 새 프로젝트를 만들 때 기본적으로 추가 되었습니다. 응용 프로그램의 시작 지점으로 사용 합니다.

### <a name="testing-the-nerddinner-application"></a>응용 프로그램의 내부 응용 프로그램 테스트

Professional Edition 이상 버전의 Visual Studio 2008을 사용 하는 경우 Visual Studio 내에서 기본 제공 단위 테스트 IDE를 사용 하 여 프로젝트를 테스트할 수 있습니다.

![](create-a-new-aspnet-mvc-project/_static/image15.png)

위의 옵션 중 하나를 선택 하면 IDE 내에서 "테스트 결과" 창이 열리며 기본 제공 기능을 다루는 새 프로젝트에 포함 된 27 단위 테스트에 대 한 통과/실패 상태를 제공 합니다.

![](create-a-new-aspnet-mvc-project/_static/image16.png)

이 자습서의 뒷부분에서는 자동화 된 테스트에 대해 자세히 설명 하 고 구현 하는 응용 프로그램 기능을 포함 하는 추가 단위 테스트를 추가 합니다.

### <a name="next-step"></a>다음 단계

이제 기본 응용 프로그램 구조가 준비 되었습니다. 이제 [응용 프로그램 데이터를 저장 하는 데이터베이스를 만들어](create-a-database.md)보겠습니다.

> [!div class="step-by-step"]
> [이전](introducing-the-nerddinner-tutorial.md)
> [다음](create-a-database.md)
