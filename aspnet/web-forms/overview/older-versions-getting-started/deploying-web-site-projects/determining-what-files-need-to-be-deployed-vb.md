---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-vb
title: 배포 해야 하는 파일 결정 (VB) | Microsoft Docs
author: rick-anderson
description: 개발 환경에서 프로덕션 환경으로 배포 해야 하는 파일은 ASP.NET 응용 프로그램을 빌드 했는지 여부에 따라 달라 집니다.
ms.author: riande
ms.date: 04/01/2009
ms.assetid: ea918f62-c9d6-4a7f-9bc6-e054d3764b2c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-vb
msc.type: authoredcontent
ms.openlocfilehash: a11dadfda8b6a189acedd7ac723d85f8b2084324
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515735"
---
# <a name="determining-what-files-need-to-be-deployed-vb"></a>배포할 파일 확인(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_vb.pdf)

> 개발 환경에서 프로덕션 환경으로 배포 해야 하는 파일은 웹 사이트 모델이 나 웹 응용 프로그램 모델을 사용 하 여 ASP.NET 응용 프로그램을 빌드 했는지 여부에 따라 달라 집니다. 이러한 두 프로젝트 모델에 대해 자세히 알아보고 프로젝트 모델이 배포에 어떤 영향을 주는지 알아보세요.

## <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램을 배포 하는 경우 개발 환경에서 프로덕션 환경으로 ASP.NET 관련 파일을 복사 해야 합니다. ASP.NET 관련 파일에는 ASP.NET 웹 페이지 태그와 코드, 클라이언트 및 서버 쪽 지원 파일이 포함 되어 있습니다. 클라이언트 쪽 지원 파일은 웹 페이지에서 참조 되 고 브라우저 이미지, CSS 파일 및 JavaScript 파일로 직접 전송 되는 파일입니다 (예:). 서버 쪽 지원 파일에는 서버측에서 요청을 처리 하는 데 사용 되는 파일이 포함 됩니다. 여기에는 구성 파일, 웹 서비스, 클래스 파일, 형식화 된 데이터 집합 및 LINQ to SQL 파일이 포함 됩니다.

일반적으로 모든 클라이언트 쪽 지원 파일은 개발 환경에서 프로덕션 환경으로 복사 되어야 하지만 복사 되는 서버 쪽 지원 파일은 서버 쪽 코드를 어셈블리 (`.dll` 파일)로 명시적으로 컴파일하거나 이러한 어셈블리가 자동으로 생성 되는지 여부에 따라 달라 집니다. 이 자습서에서는 코드를 어셈블리로 명시적으로 컴파일하거나이 컴파일 단계가 자동으로 수행 되는 경우 배포 해야 하는 파일을 강조 표시 합니다.

## <a name="explicit-compilation-versus-automatic-compilation"></a>명시적 컴파일과 자동 컴파일 비교

ASP.NET 웹 페이지는 선언적 태그와 소스 코드로 구분 됩니다. 선언적 태그 부분에는 HTML, 웹 컨트롤 및 데이터 바인딩 구문이 포함 되어 있습니다. 코드 부분에는 Visual Basic 또는 C# 코드로 작성 된 이벤트 처리기가 포함 되어 있습니다. 태그 및 코드 부분은 일반적으로 다른 파일로 구분 됩니다. `WebPage.aspx`는 코드를 저장 하 `WebPage.aspx.vb`는 동안 선언적 태그를 포함 합니다.

텍스트 속성이 페이지가 로드 되는 현재 날짜 및 시간으로 설정 된 레이블 컨트롤을 포함 하는 `Clock.aspx` 라는 ASP.NET 페이지를 살펴보겠습니다. `Clock.aspx`의 선언 태그 부분은 레이블 웹 컨트롤 `<asp:Label runat="server" id="TimeLabel" />`에 대 한 태그를 포함 하는 반면, 코드 부분 (`Clock.aspx.vb`)에는 다음 코드를 포함 하는 `Page_Load` 이벤트 처리기가 있습니다.

[!code-vb[Main](determining-what-files-need-to-be-deployed-vb/samples/sample1.vb)]

ASP.NET 엔진이이 페이지에 대 한 요청을 처리 하기 위해 먼저 페이지의 코드 부분 ( *`WebPage`* `.aspx.vb` 파일)을 컴파일해야 합니다. 이 컴파일은 명시적 또는 자동으로 발생할 수 있습니다.

컴파일이 명시적으로 수행 되는 경우 전체 응용 프로그램의 소스 코드는 응용 프로그램의 `Bin` 디렉터리에 있는 하나 이상의 어셈블리 (`.dll` 파일)로 컴파일됩니다. 컴파일이 자동으로 발생 하는 경우에는 기본적으로 자동 생성 된 어셈블리가 `Temporary ASP.NET Files` 폴더에 배치 됩니다 .이 위치는 `%WINDOWS%\Microsoft.NET\Framework\<version>`에서 찾을 수 있습니다. 하지만이 위치는 `Web.config`의 [&lt;컴파일&gt; 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 를 통해 구성할 수 있습니다. 명시적 컴파일을 사용 하면 ASP.NET 응용 프로그램의 코드를 어셈블리로 컴파일하기 위한 몇 가지 작업을 수행 해야 하며,이 단계는 배포 전에 발생 합니다. 자동 컴파일을 사용 하면 리소스에 처음 액세스할 때 웹 서버에서 컴파일 프로세스가 발생 합니다.

사용 하는 컴파일 모델에 관계 없이 모든 ASP.NET 페이지 (`WebPage.aspx` 파일)의 태그 부분은 프로덕션 환경으로 복사 해야 합니다. 명시적 컴파일을 사용 하면 `Bin` 폴더의 어셈블리를 복사 해야 하지만 ASP.NET 페이지의 코드 부분 (`WebPage.aspx.vb` 파일)은 복사할 필요가 없습니다. 자동 컴파일을 사용 하는 경우 코드를 표시 하 고 페이지를 방문할 때 자동으로 컴파일할 수 있도록 코드 부분 파일을 복사 해야 합니다. 각 ASP.NET 웹 페이지의 태그 부분에는 페이지의 연결 된 코드가 이미 명시적으로 컴파일 되었는지 아니면 자동으로 컴파일되어야 하는지 여부를 나타내는 특성이 포함 된 `@Page` 지시문이 포함 되어 있습니다. 따라서 프로덕션 환경에서는 컴파일 모델을 원활 하 게 사용할 수 있으며 명시적 또는 자동 컴파일을 사용 하도록 지정 하기 위해 특별 한 구성 설정을 적용할 필요가 없습니다.

표 1에서는 명시적 컴파일과 자동 컴파일을 사용할 때 배포할 다른 파일을 요약 합니다. 사용 된 컴파일 모델에 관계 없이 해당 폴더가 있으면 항상 `Bin` 폴더에 어셈블리를 배포 해야 합니다. `Bin` 폴더에는 명시적 컴파일 모델을 사용할 때 컴파일된 소스 코드를 포함 하는 웹 응용 프로그램과 관련 된 어셈블리가 포함 됩니다. `Bin` 디렉터리에는 다른 프로젝트의 어셈블리와 사용 중일 수 있는 오픈 소스 또는 타사 어셈블리도 포함 되며, 이러한 어셈블리는 프로덕션 서버에 있어야 합니다. 따라서 일반적으로는 배포할 때 프로덕션에 `Bin` 폴더를 복사 합니다. (자동 컴파일 모델을 사용 하 고 외부 어셈블리를 사용 하지 않는 경우 `Bin` 디렉터리가 없는 것입니다.

| **컴파일 모델** | **태그 부분 파일을 배포 하 시겠습니까?** | **소스 코드 파일을 배포 하 시겠습니까?** | **`Bin` 디렉터리에 어셈블리를 배포 하 시겠습니까?** |
| --- | --- | --- | --- |
| 명시적 컴파일 | yes | 예 | yes |
| 자동 컴파일 | yes | yes | 예 (있는 경우) |

**표 1: 배포 하는 파일은 사용 되는 컴파일 모델에 따라 달라 집니다.**

## <a name="taking-a-trip-down-memory-lane"></a>메모리 레인 다운 수행

사용 되는 컴파일 방식은 ASP.NET 응용 프로그램이 Visual Studio에서 관리 되는 방식에 따라 부분적으로 달라 집니다. 이후. 2000 년의 NET 개시에는 visual studio의 네 가지 버전 (visual studio .NET 2002, visual Studio .NET 2003, Visual Studio 2005 및 Visual Studio 2008)이 있습니다. *웹 응용 프로그램 프로젝트* 모델을 사용 하 여 Visual Studio .net 2002 및 2003에서 관리 되는 ASP.NET 응용 프로그램입니다. 웹 응용 프로그램 프로젝트 모델의 핵심 기능은 다음과 같습니다.

- 프로젝트를 구성을 하는 파일은 단일 프로젝트 파일에 정의 되어 있습니다. 프로젝트 파일에 정의 되어 있지 않은 파일은 Visual Studio에서 웹 응용 프로그램의 일부로 간주 되지 않습니다.
- 명시적 컴파일을 사용 합니다. 프로젝트를 빌드하면 프로젝트 내의 코드 파일이 `Bin` 폴더에 배치 된 단일 어셈블리로 컴파일됩니다.

Microsoft에서 Visual Studio 2005을 릴리스할 때 웹 응용 프로그램 프로젝트 모델에 대 한 지원을 삭제 하 고 웹 사이트 프로젝트 모델로 대체 했습니다. 웹 사이트 프로젝트 모델은 *웹 응용 프로그램 프로젝트* 모델과 다음과 같은 방식으로 구분 됩니다.

- 프로젝트 파일을 출력 하는 단일 프로젝트 파일을 사용 하는 대신 파일 시스템이 대신 사용 됩니다. 즉, 웹 응용 프로그램 폴더 (또는 하위 폴더) 내의 모든 파일은 프로젝트의 일부로 간주 됩니다.
- Visual Studio에서 프로젝트를 빌드하면 `Bin` 디렉터리에 어셈블리가 생성 되지 않습니다. 대신, 웹 사이트 프로젝트를 빌드하면 컴파일 시간 오류가 보고 됩니다.
- 자동 컴파일을 지원 합니다. 웹 사이트 프로젝트는 일반적으로 코드를 미리 컴파일할 수 있지만 (명시적 컴파일) 태그와 소스 코드를 프로덕션 환경으로 복사 하 여 배포 합니다.

Microsoft는 Visual Studio 2005 서비스 팩 1을 릴리스할 때 웹 응용 프로그램 프로젝트 모델을 다시 합니다. 그러나 Visual Web Developer는 웹 사이트 프로젝트 모델만 계속 지원 합니다. 좋은 소식은 Visual Web Developer 2008 서비스 팩 1을 사용 하 여이 제한이 삭제 되었다는 것입니다. 현재는 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 Visual Studio (및 Visual Web Developer)에서 ASP.NET 응용 프로그램을 만들 수 있습니다. 두 모델 모두 장단점이 있습니다. 웹 [응용 프로그램 프로젝트 소개: 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트 비교](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5) 를 참조 하 여 두 모델을 비교 하 고 상황에 가장 적합 한 프로젝트 모델을 결정 하는 데 도움을 줍니다.

## <a name="exploring-the-sample-web-application"></a>샘플 웹 응용 프로그램 탐색

이 자습서에 대 한 다운로드에는 책 리뷰 라는 ASP.NET 응용 프로그램이 포함 되어 있습니다. Websites가 온라인 커뮤니티와 함께 책 리뷰를 공유 하도록 만들 수 있는 취미 웹 사이트를 모방 합니다. 이 ASP.NET 웹 응용 프로그램은 매우 간단 하며 다음 리소스로 구성 됩니다.

- 응용 프로그램의 구성 파일을 `Web.config`합니다.
- 마스터 페이지 (`Site.master`)입니다.
- 7 가지 ASP.NET 페이지:

    - ~/`Default.aspx`-사이트 홈페이지입니다.
    - ~/`About.aspx`-"사이트 정보" 페이지
    - ~/`Fiction/Default.aspx`-검토 한 fiction 책을 나열 하는 페이지입니다.

        - ~/`Fiction/Blaze.aspx`-Richard Bachman novel *레이즈*리뷰입니다.
    - ~/`Tech/Default.aspx`-검토 된 기술 서적 목록을 표시 하는 페이지입니다.

        - ~/`Tech/CYOW.aspx`- *자체 웹 사이트 만들기*를 검토 합니다.
        - ~/`Tech/TYASP35.aspx`- *24 시간 이내에 ASP.NET 3.5를 알려*주는 검토.
- `Styles` 폴더의 세 가지 CSS 파일
- 이미지 파일 4 개 (ASP.NET)는 모두 `Images` 폴더에 있는 세 개의 검토 된 설명서에 포함 된 로고와 이미지를 제공 합니다.
- `Web.sitemap` 파일은 사이트 맵을 정의 하 고 루트 디렉터리의 `Default.aspx` 페이지와 `Fiction` 및 `Tech` 폴더에 메뉴를 표시 하는 데 사용 됩니다.
- 기본 `Page` 클래스를 정의 하는 `BasePage.vb` 라는 클래스 파일입니다. 이 클래스는 사이트 맵에서 페이지의 위치를 기준으로 `Title` 속성을 자동으로 설정 하 여 `Page` 클래스의 기능을 확장 합니다. 간단히 말해서 `BasePage` (`System.Web.UI.Page`대신)를 확장 하는 모든 ASP.NET 코드를 포함 하는 클래스의 제목은 사이트 맵의 해당 위치에 따라 값으로 설정 됩니다. 예를 들어 ~/`Tech/CYOW.aspx` 페이지를 볼 때 제목은 "Home: 기술: 사용자의 웹 사이트 만들기"로 설정 됩니다.

그림 1에서는 브라우저를 통해 볼 때 책 리뷰 웹 사이트의 스크린샷을 보여 줍니다. 여기서는 *ASP.NET 3.5 (24 시간)에*대 한 책을 검토 하는 ~/Tech/TYASP35.aspx 페이지가 표시 됩니다. 페이지의 위쪽에 있는 이동 경로 및 왼쪽 열에 있는 메뉴는 `Web.sitemap`에 정의 된 사이트 맵 구조를 기반으로 합니다. 오른쪽 위 모퉁이에 있는 이미지는 `Images` 폴더에 있는 책 표지 이미지 중 하나입니다. 웹 사이트의 모양과 느낌은 `Styles` 폴더의 CSS 파일에 의해 표시 되는 css 스타일 시트 규칙을 통해 정의 되며, 주요 페이지 레이아웃은 `Site.master`마스터 페이지에 정의 되어 있습니다.

[책 리뷰 웹 사이트를 ![하 여 다양 한 제목의 리뷰를 제공 합니다.](determining-what-files-need-to-be-deployed-vb/_static/image2.png)](determining-what-files-need-to-be-deployed-vb/_static/image1.png)

**그림 1**: 책 리뷰 웹 사이트에서 다양 한 제목의 리뷰를 제공 합니다 ([전체 크기 이미지를 보려면 클릭](determining-what-files-need-to-be-deployed-vb/_static/image3.png)).

이 응용 프로그램은 데이터베이스를 사용 하지 않습니다. 각 검토는 응용 프로그램에서 별도의 웹 페이지로 구현 됩니다. 이 자습서와 다음 몇 가지 자습서에서는 데이터베이스가 없는 웹 응용 프로그램을 배포 하는 과정을 안내 합니다. 그러나 이후 자습서에서는이 응용 프로그램을 개선 하 여 데이터베이스 내에 검토, 판독기 설명 및 기타 정보를 저장 하 고, 데이터 기반 웹 응용 프로그램을 올바르게 배포 하기 위해 수행 해야 하는 단계를 살펴봅니다.

> [!NOTE]
> 이러한 자습서는 웹 호스트 공급자를 사용 하 여 ASP.NET 응용 프로그램을 호스트 하는 데 중점을 두고 ASP와 같은 보조 항목을 탐색 하지 않습니다. 네트워크의 사이트 맵 시스템 또는 기본 페이지 클래스를 사용 합니다. 이러한 기술에 대 한 자세한 내용 및 자습서 전체에서 다루는 다른 항목의 배경 정보는 각 자습서의 끝에 있는 추가 정보 섹션을 참조 하세요.

이 자습서의 다운로드에는 웹 응용 프로그램의 복사본 두 개가 있으며, 각각 다른 Visual Studio 프로젝트 형식으로 구현 됩니다. BookReviewsWAP, 웹 응용 프로그램 프로젝트 및 BookReviewsWSP 웹 사이트 프로젝트입니다. 두 프로젝트는 Visual Web Developer 2008 s p 1을 사용 하 여 만들어졌으며 ASP.NET 3.5 SP1을 사용 합니다. 이러한 프로젝트를 사용 하려면 먼저 바탕 화면에 콘텐츠 압축을 푸는 것이 시작 됩니다. 웹 응용 프로그램 프로젝트 (BookReviewsWAP)를 열려면 `BookReviewsWAP` 폴더로 이동한 다음 솔루션 파일 `BookReviewsWAP.sln`을 두 번 클릭 합니다. 웹 사이트 프로젝트 (BookReviewsWSP)를 열려면 Visual Studio를 시작한 다음 파일 메뉴에서 웹 사이트 열기 옵션을 선택 하 고 바탕 화면에서 `BookReviewsWSP` 폴더로 이동한 다음 확인을 클릭 합니다.

이 자습서의 나머지 두 섹션에서는 응용 프로그램을 배포할 때 프로덕션 환경에 복사 해야 하는 파일을 살펴봅니다. 다음 두 자습서- [*FTP를 사용 하 여 사이트 배포*](deploying-your-site-using-an-ftp-client-vb.md) 및 [*Visual Studio를 사용 하 여 사이트 배포*](deploying-your-site-using-visual-studio-vb.md) -웹 호스트 공급자에 이러한 파일을 복사 하는 다양 한 방법을 보여 줍니다.

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>웹 응용 프로그램 프로젝트에 대해 배포할 파일 결정

웹 응용 프로그램 프로젝트 모델은 명시적 컴파일을 사용 합니다. 프로젝트의 소스 코드는 응용 프로그램을 빌드할 때마다 단일 어셈블리로 컴파일됩니다. 이 컴파일에는 `BasePage.vb` 클래스 뿐만 아니라 ASP.NET 페이지의 코드 숨김이 파일 (~/`Default.aspx.vb`, ~/`About.aspx.vb`등)이 포함 됩니다. 결과 어셈블리는 `BookReviewsWAP.dll` 이름이 지정 되 고 응용 프로그램의 `Bin` 디렉터리에 있습니다.

그림 2에서는 책 리뷰 웹 응용 프로그램 프로젝트를 구성 하는 파일을 보여 줍니다.

[솔루션 탐색기 ![웹 응용 프로그램 프로젝트를 구성 하는 파일을 나열 합니다.](determining-what-files-need-to-be-deployed-vb/_static/image5.png)](determining-what-files-need-to-be-deployed-vb/_static/image4.png)

**그림 2**: 웹 응용 프로그램 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기

> [!NOTE]
> 그림 2에서 볼 수 있듯이 ASP.NET 페이지의 코드 숨김이 Visual Basic 웹 응용 프로그램 프로젝트에 대 한 솔루션 탐색기에 표시 되지 않습니다. 페이지의 코드 숨김으로 클래스를 보려면 솔루션 탐색기 페이지를 마우스 오른쪽 단추로 클릭 하 고 코드 보기를 선택 합니다.

웹 응용 프로그램 프로젝트 모델을 사용 하 여 개발 된 ASP.NET 응용 프로그램을 배포 하려면 먼저 응용 프로그램을 빌드하여 어셈블리에 최신 소스 코드를 명시적으로 컴파일해야 합니다. 다음으로 프로덕션 환경에 다음 파일을 복사 합니다.

- ~/`Default.aspx`, ~/`About.aspx`등의 모든 ASP.NET 페이지에 대 한 선언적 태그가 포함 된 파일입니다. 또한 모든 마스터 페이지 및 사용자 정의 컨트롤에 대 한 선언 태그를 복사 합니다.
- `Bin` 폴더의 어셈블리 (`.dll` 파일)입니다. 프로그램 데이터베이스 파일 (`.pdb`) 또는 `Bin` 디렉터리에서 찾을 수 있는 XML 파일을 복사할 필요가 없습니다.

ASP.NET 페이지의 소스 코드 파일을 프로덕션 환경으로 복사할 필요는 없으며, `BasePage.vb` 클래스 파일도 복사 하지 않아도 됩니다.

> [!NOTE]
> 그림 2에 나와 있는 것 처럼 `BasePage` 클래스는 프로젝트에서 `HelperClasses`라는 폴더에 배치 된 클래스 파일로 구현 됩니다. 프로젝트가 컴파일될 때 `BasePage.vb` 파일의 코드는 ASP.NET 페이지의 코드 숨김이 아닌 클래스와 함께 `BookReviewsWAP.dll`단일 어셈블리로 컴파일됩니다. ASP.NET에는 웹 사이트 프로젝트용 클래스 파일을 저장 하도록 디자인 된 `App_Code` 라는 특수 폴더가 있습니다. `App_Code` 폴더의 코드는 자동으로 컴파일되므로 웹 응용 프로그램 프로젝트와 함께 사용 하면 안 됩니다. 대신 응용 프로그램의 클래스 파일을 `HelperClasses`, `Classes`또는 이와 비슷한 일반 폴더에 두어야 합니다. 또는 별도의 클래스 라이브러리 프로젝트에 클래스 파일을 저장할 수 있습니다.

ASP.NET 관련 태그 파일 및 어셈블리를 `Bin` 폴더에 복사 하는 것 외에도 클라이언트 쪽 지원 파일 (이미지 및 CSS 파일) 뿐만 아니라 다른 서버 쪽 지원 파일, `Web.config` 및 `Web.sitemap`도 복사 해야 합니다. 이러한 클라이언트 및 서버 쪽 지원 파일은 명시적 또는 자동 컴파일을 사용 하는지 여부에 관계 없이 프로덕션 환경에 복사 해야 합니다.

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>웹 사이트 프로젝트 파일에 배포할 파일 확인

웹 사이트 프로젝트 모델은 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 사용할 수 없는 기능인 자동 컴파일을 지원 합니다. 명시적 컴파일을 사용 하면 프로젝트의 소스 코드를 어셈블리로 컴파일하고 해당 어셈블리를 프로덕션 환경에 복사 해야 합니다. 반면에 자동 컴파일을 사용 하면 소스 코드를 프로덕션 환경에 복사 하 고 필요에 따라 요청 시 런타임에 의해 컴파일됩니다.

Visual Studio의 빌드 메뉴 옵션은 웹 응용 프로그램 프로젝트와 웹 사이트 프로젝트 모두에 표시 됩니다. 웹 응용 프로그램 프로젝트를 빌드하면 프로젝트의 소스 코드를 `Bin` 디렉터리에 있는 단일 어셈블리로 컴파일합니다. 웹 사이트 프로젝트를 빌드하면 컴파일 시간 오류가 발생 하지만 어셈블리는 생성 되지 않습니다. 웹 사이트 프로젝트 모델을 사용 하 여 개발 된 ASP.NET 응용 프로그램을 배포 하려면 적절 한 파일을 프로덕션 환경에 복사 하기만 하면 됩니다. 그러나 먼저 프로젝트를 빌드하여 컴파일 시간 오류가 없는지 확인 하는 것이 좋습니다.

그림 3에서는 책 리뷰 웹 사이트 프로젝트를 구성 하는 파일을 보여 줍니다.

[솔루션 탐색기 ![웹 사이트 프로젝트를 구성 하는 파일을 나열 합니다.](determining-what-files-need-to-be-deployed-vb/_static/image7.png)](determining-what-files-need-to-be-deployed-vb/_static/image6.png)

**그림 3**: 웹 사이트 프로젝트를 구성 하는 파일을 나열 하는 솔루션 탐색기

웹 사이트 프로젝트를 배포 하려면 모든 ASP.NET 관련 파일을 프로덕션 환경으로 복사 해야 합니다. ASP.NET 페이지, 마스터 페이지 및 사용자 정의 컨트롤에 대 한 태그 페이지를 해당 코드 파일과 함께 포함 합니다. 또한 `BasePage.vb`와 같은 클래스 파일도 복사 해야 합니다. `BasePage.vb` 파일은 클래스 파일의 웹 사이트 프로젝트에 사용 되는 특수 ASP.NET 폴더인 `App_Code` 폴더에 있습니다. 개발 환경에서 `App_Code` 폴더의 클래스 파일을 프로덕션의 `App_Code` 폴더에 복사 해야 하므로 특수 폴더는 프로덕션 환경 에서도 만들어야 합니다.

ASP.NET 태그 및 소스 코드 파일을 복사 하는 것 외에도 클라이언트 쪽 지원 파일 (이미지 및 CSS 파일) 뿐만 아니라 다른 서버 쪽 지원 파일, `Web.config` 및 `Web.sitemap`도 복사 해야 합니다.

> [!NOTE]
> 웹 사이트 프로젝트는 명시적 컴파일을 사용할 수도 있습니다. 이후 자습서에서는 웹 사이트 프로젝트를 명시적으로 컴파일하는 방법에 대해 살펴봅니다.

## <a name="summary"></a>요약

ASP.NET 응용 프로그램을 배포 하면 개발 환경에서 프로덕션 환경으로 필요한 파일을 복사 하는 작업이 수반 됩니다. 동기화 해야 하는 정확한 파일 집합은 ASP.NET 응용 프로그램의 코드가 명시적 또는 자동으로 컴파일되는지 여부에 따라 달라 집니다. 사용 된 컴파일 전략은 Visual Studio가 웹 응용 프로그램 프로젝트 모델 또는 웹 사이트 프로젝트 모델을 사용 하 여 ASP.NET 응용 프로그램을 관리 하도록 구성 되었는지 여부에 따라 영향을 받습니다.

웹 응용 프로그램 프로젝트 모델은 명시적 컴파일을 사용 하 고 프로젝트의 코드를 `Bin` 폴더의 단일 어셈블리로 컴파일합니다. 응용 프로그램을 배포할 때 ASP.NET 페이지의 태그 부분과 `Bin` 폴더의 내용을 프로덕션 환경으로 푸시 해야 합니다. 예를 들어 응용 프로그램의 소스 코드는 프로덕션 환경으로 복사할 필요가 없습니다. 예를 들어 코드 파일 및 코드 숨김이 클래스입니다.

웹 사이트 프로젝트 모델은 나중에 자습서에서 볼 수 있듯이 웹 사이트 프로젝트를 명시적으로 컴파일할 수 있지만 기본적으로 자동 컴파일을 사용 합니다. 자동 컴파일을 사용 하는 ASP.NET 응용 프로그램을 배포 하려면 *태그 부분과 소스* 코드를 프로덕션 환경에 복사 해야 합니다. 코드는 처음으로 요청 될 때 프로덕션 환경에서 자동으로 컴파일됩니다.

이제 개발 환경과 프로덕션 환경 간에 동기화 해야 하는 파일을 검사 했으므로 서적 검토 응용 프로그램을 웹 호스트 공급자에 배포할 준비가 되었습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 컴파일 개요](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 사용자 정의 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [ASP를 검사 합니다. 네트워크의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [웹 응용 프로그램 프로젝트 소개](https://msdn.microsoft.com/library/aa730880.aspx)
- [마스터 페이지 자습서](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [페이지 간에 코드 공유](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [ASP.NET 페이지의 코드 숨김으로 클래스에 대 한 사용자 지정 기본 클래스 사용](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005의 웹 사이트 프로젝트 시스템: 어떻게 되나요?](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [연습: Visual Studio에서 웹 사이트 프로젝트를 웹 응용 프로그램 프로젝트로 변환](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [이전](asp-net-hosting-options-vb.md)
> [다음](deploying-your-site-using-an-ftp-client-vb.md)
