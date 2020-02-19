---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 소개 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456335"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 소개(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.

이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.

이 항목과 함께 사용할 수 있는 VB 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다. [여기에서 VB 버전을 다운로드](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)합니다. CSharp를 선호 하는 경우이 자습서의 [csharp 버전](../cs/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.

## <a name="what-youll-build"></a>만들 내용

데이터베이스에서 동영상 만들기, 편집 및 나열을 지 원하는 간단한 동영상 목록 응용 프로그램을 구현 합니다. 다음은 빌드할 응용 프로그램의 두 가지 스크린샷입니다. 여기에는 데이터베이스의 영화 목록을 표시 하는 페이지가 포함 되어 있습니다.

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

응용 프로그램을 사용 하 여 영화를 추가, 편집 및 삭제할 수 있을 뿐 아니라 개별 항목에 대 한 세부 정보를 볼 수도 있습니다. 모든 데이터 입력 시나리오에는 데이터베이스에 저장 된 데이터가 올바른지 확인 하기 위한 유효성 검사가 포함 됩니다.

[CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)![

## <a name="skills-youll-learn"></a>학습할 기술

다음 내용을 학습하게 됩니다.

- 새 ASP.NET MVC 프로젝트를 만드는 방법
- Entity Framework 코드를 사용 하 여 새 데이터베이스를 만드는 방법-우선
- ASP.NET MVC 컨트롤러 및 뷰를 만드는 방법
- 데이터를 검색 하 고 표시 하는 방법
- 데이터를 편집 하 고 데이터 유효성 검사를 사용 하도록 설정 하는 방법

## <a name="getting-started"></a>시작하기

먼저 Visual Web Developer 2010 Express (short의 경우 "VWD")를 실행 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다.

Visual Web Developer는 IDE (통합 개발 환경)입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다. Visual Web Developer에는 제공 되는 다양 한 옵션을 보여 주는 도구 모음이 있습니다. IDE에서 작업을 수행 하는 다른 방법을 제공 하는 메뉴도 있습니다. 예를 들어 **시작** 페이지에서 **새 프로젝트** 를 선택 하는 대신 메뉴를 사용 하 여 **파일** &gt; **새 프로젝트**를 선택할 수 있습니다.

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>첫 번째 응용 프로그램 만들기

Visual Basic 또는 시각적 개체 C# 중 하나를 프로그래밍 언어로 사용 하 여 응용 프로그램을 만들 수 있습니다. 이 자습서에서는 왼쪽에서 Visual Basic를 선택한 다음 **ASP.NET MVC 3 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 "MvcMovie"로 지정한 다음 **확인**을 클릭 합니다.

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

**새 ASP.NET MVC 3 프로젝트** 대화 상자에서 **인터넷 응용 프로그램**을 선택 합니다. 기본 뷰 엔진으로 **Razor** 를 남겨 둡니다.

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

**확인**을 클릭합니다. Visual Web Developer는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 했으므로 이제는 작업을 수행 하지 않고 작업 중인 응용 프로그램이 있습니다. 이는 간단한 "Hello World!"입니다. 프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

**디버그** 메뉴에서 **디버깅 시작**을 선택합니다.

![](intro-to-aspnet-mvc-3/_static/image11.png)

디버깅을 시작 하는 바로 가기 키는 F5입니다.

F5 키를 누르면 Visual Web Developer에서 개발 웹 서버를 시작 하 고 웹 응용 프로그램을 실행 합니다. 그러면 VWD에서 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄에 `localhost` 표시 되 고 `example.com`와 같은 것은 아닙니다. `localhost`은 항상 자신의 로컬 컴퓨터를 가리키지만이 경우에는 방금 빌드한 응용 프로그램을 실행 하는 것입니다. VWD에서 웹 프로젝트를 실행 하면 프로젝트에 대해 임의의 포트가 사용 됩니다. 아래 이미지에서 임의의 포트 번호는 43246입니다. 프로젝트에서 다른 포트 번호를 사용할 수 있습니다.

![](intro-to-aspnet-mvc-3/_static/image12.png)

기본적으로이 기본 템플릿은 방문할 두 페이지와 기본 로그인 페이지를 제공 합니다. 이 응용 프로그램의 작동 방식을 변경 하 고 프로세스에서 ASP.NET MVC에 대해 약간의 방법을 살펴보겠습니다. 브라우저를 닫고 일부 코드를 변경 하겠습니다.

> [!div class="step-by-step"]
> [다음](adding-a-controller.md)
