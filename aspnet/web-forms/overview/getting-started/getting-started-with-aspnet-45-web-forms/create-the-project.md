---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: 프로젝트 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74576062"
---
# <a name="create-the-project"></a>프로젝트 만들기

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 ASP.NET의 기능에 익숙해질 수 있도록 Visual Studio에서 기본 프로젝트를 만들고, 검토 하 고, 실행 합니다. 또한 Visual Studio 환경을 검토할 것입니다.

## <a name="what-youll-learn"></a>학습 내용:

- 새 Web Forms 프로젝트를 만드는 방법
- Web Forms 프로젝트의 파일 구조입니다.
- Visual Studio에서 프로젝트를 실행 하는 방법을 설명 합니다.
- 기본 Web forms 응용 프로그램의 다양 한 기능
- Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항입니다.

## <a name="creating-the-project"></a>프로젝트 만들기

1. Visual Studio를 엽니다.
2. Visual Studio의 **파일** 메뉴에서 **새 프로젝트** 를 선택 합니다. 

    ![프로젝트 만들기-새 프로젝트 메뉴 항목](create-the-project/_static/image1.png)
3. 왼쪽에 있는  **C# Visual** -&gt; **웹** 템플릿 그룹 &gt; -**템플릿을** 선택 합니다.
4. 가운데 열에서 **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.  
 이 자습서 시리즈는 .NET Framework 4.5.2를 사용 합니다.
5. 프로젝트 이름을 *WingtipToys* 로 선택 하 고 **확인** 단추를 선택 합니다. 

    ![프로젝트 만들기-새 프로젝트 대화 상자](create-the-project/_static/image2.png)

    > [!NOTE]
    > 이 자습서 시리즈의 프로젝트 이름은 **WingtipToys**입니다. 자습서 시리즈 전체에서 제공 된 코드가 예상 대로 작동 하도록이 *정확한* 프로젝트 이름을 사용 하는 것이 좋습니다.

6. **인증 변경** 단추를 클릭 합니다. **개별 사용자 계정을** 선택 하 고 **확인** 단추를 클릭 합니다.

7. **Web Forms** 템플릿을 선택 하 고 **확인** 단추를 클릭 합니다.

    ![프로젝트 만들기-새 프로젝트 템플릿](create-the-project/_static/image3.png)

프로젝트를 만드는 데 약간의 시간이 걸립니다. 준비가 되 면 **default.aspx 페이지를 엽니다.**

![프로젝트 만들기-새 프로젝트 템플릿](create-the-project/_static/image4.png)

가운데 창의 아래쪽에 있는 옵션을 선택 하 여 **디자인** 뷰와 **소스** 뷰 간을 전환할 수 있습니다. **디자인** 뷰는 ASP.NET 웹 페이지, 마스터 페이지, 콘텐츠 페이지, HTML 페이지 및 사용자 정의 컨트롤을 옆의 WYSIWYG 뷰를 사용 하 여 표시 합니다. **원본** 뷰 사용자가 편집할 수 있는 웹 페이지에 대 한 HTML 태그를 표시 합니다.

> [!TIP] 
> 
> **ASP.NET 프레임 워크 이해**
> 
> ASP.NET Web Forms를 사용하면 친숙한 끌어서 놓기, 이벤트 기반 모델을 사용하여 동적 웹 사이트를 구축할 수 있습니다. 디자인 화면과 수백 개의 컨트롤 및 구성 요소를 통해 데이터 액세스가 포함된 강력하고 정교한 UI 기반 사이트를 신속하게 구축할 수 있습니다. 정문 장난감 매장은 ASP.NET Web Forms를 기반으로 하지만이 자습서 시리즈에서 학습 하는 대부분의 개념은 모든 ASP.NET에 적용 됩니다.
> 
> ASP.NET는 다음과 같은 네 가지 기본 개발 프레임 워크를 제공 합니다.
> 
> - [ASP.NET Web Forms](../../../index.md)  
>  Web Forms 프레임 워크는 Microsoft Windows Forms (WinForms) 및 WPF/XAML/Silverlight와 같은 선언적 및 제어 기반 프로그래밍을 선호 하는 개발자를 대상으로 합니다. 이 모델은 WYSIWYG 디자이너 기반 개발 모델을 제공 하므로 웹 개발을 위한 RAD (신속한 응용 프로그램 개발) 환경을 찾고 있는 개발자와 인기 있습니다. 웹 프로그래밍을 처음 사용 하 고 기존 Microsoft RAD 클라이언트 개발 도구 (예: Visual Basic 및 시각적 개체 C#)에 익숙한 경우 HTML 및 JavaScript를 사용 하지 않고도 웹 응용 프로그램을 신속 하 게 빌드할 수 있습니다.
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC는 테스트 구동 방식 개발, 관심사 분리, IoC (종속성 주입) 및 DI (종속성 주입)와 같은 패턴 및 원칙에 관심이 있는 개발자를 대상으로 합니다. 이 프레임 워크는 웹 응용 프로그램의 비즈니스 논리 계층을 프레젠테이션 계층과 분리 하는 것을 권장 합니다.
> - [ASP.NET 웹 페이지 2](../../../../web-pages/index.md)  
>  ASP.NET 웹 페이지는 PHP의 줄을 따라 간단한 웹 개발 스토리를 원하는 개발자를 대상으로 합니다. 웹 페이지 모델에서는 HTML 페이지를 만든 다음 해당 태그가 렌더링 되는 방식을 동적으로 제어 하기 위해 서버 기반 코드를 페이지에 추가 합니다. 웹 페이지는 특히 간단한 프레임 워크로 설계 되었으며 HTML을 알고 있는 사용자를 위해 ASP.NET에 가장 쉬운 진입점 이며, 학생 또는 취미와 같은 광범위 한 프로그래밍 환경을 제공 하지 않을 수 있습니다. ASP.NET 사용을 시작 하는 데 PHP 또는 유사한 프레임 워크를 알고 있는 웹 개발자에 게 좋은 방법 이기도 합니다.
> - [ASP.NET 단일 페이지 응용 프로그램](../../../../single-page-application/index.md)  
>  ASP.NET SPA(단일 페이지 애플리케이션)는 HTML 5, CSS 3 및 JavaScript를 사용하여 중요한 클라이언트 쪽 상호 작용을 포함하는 애플리케이션을 빌드할 수 있도록 도와줍니다. ASP.NET 및 Web Tools 2012.2 업데이트는 node.js 및 ASP.NET Web API를 사용 하 여 단일 페이지 응용 프로그램을 빌드하기 위한 새 템플릿을 제공 합니다. 새 SPA 템플릿 외에도 새로운 커뮤니티에서 만든 SPA 템플릿도 다운로드할 수 있습니다.
> 
> ASP.NET는 네 가지 주요 개발 프레임 워크 외에도,이 자습서 시리즈에서 다루지는 않지만 이해 하는 데 중요 한 추가 기술을 제공 합니다.
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -브라우저 및 모바일 장치를 비롯 한 광범위 한 클라이언트에 연결 되는 HTTP 서비스를 빌드하기 위한 프레임 워크입니다.
> - [ASP.NET SignalR](../../../../signalr/index.md) -실시간 웹 기능을 쉽게 개발할 수 있도록 하는 라이브러리입니다.

### <a name="reviewing-the-project"></a>프로젝트 검토

Visual Studio에서 **솔루션 탐색기** 창을 사용 하 여 프로젝트에 대 한 파일을 관리할 수 있습니다. **솔루션 탐색기**에서 응용 프로그램에 추가 된 폴더를 살펴보겠습니다. 웹 응용 프로그램 템플릿은 기본 폴더 구조를 추가 합니다.

![프로젝트 만들기-솔루션 탐색기](create-the-project/_static/image5.png)

Visual Studio는 프로젝트에 대 한 몇 가지 초기 폴더와 파일을 만듭니다. 이 자습서의 뒷부분에서 작업 하는 첫 번째 파일은 다음과 같습니다.

| **파일** | **용도** |
| --- | --- |
| *Default.aspx* | 일반적으로 응용 프로그램이 브라우저에서 실행 될 때 표시 되는 첫 번째 페이지입니다. |
| *사이트 마스터* | 일관 된 레이아웃을 만들고 응용 프로그램의 페이지에 대해 표준 동작을 사용할 수 있는 페이지입니다. |
| *Global.asax* | ASP.NET 또는 HTTP 모듈에서 발생 한 응용 프로그램 수준 및 세션 수준 이벤트에 응답 하는 코드를 포함 하는 선택적 파일입니다. |
| *Web.config* | 응용 프로그램에 대 한 구성 데이터입니다. |

### <a name="running-the-default-web-application"></a>기본 웹 응용 프로그램 실행

기본 웹 응용 프로그램은 기본 제공 기능 및 지원에 따라 다양 한 환경을 제공 합니다. 기본 Web forms 프로젝트를 변경 하지 않으면 로컬 웹 브라우저에서 응용 프로그램을 실행할 준비가 된 것입니다.

1. Visual Studio에서 ***f5*** 키를 누릅니다.   
 응용 프로그램이 작성 되 고 웹 브라우저에 표시 됩니다.  

    ![프로젝트 기본 페이지 만들기](create-the-project/_static/image6.png)
2. 실행 중인 응용 프로그램 검토를 완료 했으면 브라우저 창을 닫습니다.

기본 웹 응용 프로그램에는 세 가지 기본 웹 응용 프로그램 ( *default.aspx (Home* ), *.aspx*및 *연락처 .aspx*)이 있습니다. 이러한 각 페이지는 위쪽 탐색 모음에서 연결할 수 있습니다. 계정 폴더, Register .aspx 페이지 및 login.aspx 페이지에는 두 개의 추가 페이지가 포함 되어 있습니다. 이 두 페이지에서는 ASP.NET의 멤버 자격 기능을 사용 하 여 사용자 자격 증명을 만들고 저장 하 고 유효성을 검사할 수 있습니다.

## <a name="aspnet-web-forms-background"></a>ASP.NET Web Forms 배경

ASP.NET Web Forms은 서버에서 실행 되는 코드가 브라우저 또는 클라이언트 장치에 웹 페이지 출력을 동적으로 생성 하는 Microsoft ASP.NET 기술을 기반으로 하는 페이지입니다. ASP.NET Web Forms 페이지는 스타일, 레이아웃 등과 같은 기능에 대 한 올바른 브라우저 호환 HTML을 자동으로 렌더링 합니다. Web Forms Microsoft Visual Basic 및 Microsoft Visual C#과 같은 .net 공용 언어 런타임에서 지 원하는 모든 언어와 호환 됩니다. 또한 Web Forms는 관리 되는 환경, 형식 안전성 및 상속과 같은 이점을 제공 하는 [Microsoft .NET 프레임 워크](https://msdn.microsoft.com/vstudio/aa496123)를 기반으로 합니다.

ASP.NET Web Forms 페이지가 실행 되 면 페이지는 일련의 처리 단계를 수행 하는 수명 주기를 거칩니다. 이러한 단계에는 초기화, 컨트롤 인스턴스화, 상태 복원 및 유지 관리, 이벤트 처리기 코드 실행, 렌더링 등이 포함 됩니다. ASP.NET Web Forms의 기능을 좀 더 잘 이해 하 게 되 면 [ASP.NET 페이지 수명 주기](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx) 를 이해 하 여 원하는 효과에 대 한 적절 한 수명 주기 단계에서 코드를 작성할 수 있도록 하는 것이 중요 합니다.

웹 서버는 페이지에 대 한 요청을 받으면 페이지를 찾아 처리 하 고 브라우저에 보낸 다음 모든 페이지 정보를 삭제 합니다. 사용자가 같은 페이지를 다시 요청 하면 서버에서 전체 시퀀스를 반복 하 여 페이지를 처음부터 다시 처리 합니다. 다른 방법으로 서버에 처리 된 페이지의 메모리가 없는 경우-페이지는 상태 비저장입니다. ASP.NET 페이지 프레임 워크는 페이지 및 해당 컨트롤의 상태를 유지 관리 하는 작업을 자동으로 처리 하 고, 응용 프로그램 관련 정보의 상태를 유지 관리 하는 명시적인 방법을 제공 합니다.

> [!TIP] 
> 
> **Web Forms 응용 프로그램 템플릿의 웹 응용 프로그램 기능**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿은 다양 한 기본 제공 기능 집합을 제공 합니다. 이 도구는 *홈페이지로* *된 .Aspx 페이지* , *연락처 .aspx* 페이지를 제공할 뿐만 아니라 사용자를 등록 하 고 사용자의 웹 사이트에 로그인 할 수 있도록 자격 증명을 저장 하는 멤버 자격 기능도 포함 하 고 있습니다. 이 개요에서는 ASP.NET Web Forms 응용 프로그램 템플릿에 포함 된 기능과 정문 장난감 응용 프로그램에서 이러한 기능을 사용 하는 방법에 대해 자세히 설명 합니다.
> 
> **멤버 자격**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx) Id는 응용 프로그램에서 만든 데이터베이스에 사용자의 자격 증명을 저장 합니다. 사용자가 로그인 하면 응용 프로그램은 데이터베이스를 읽어 자격 증명의 유효성을 검사 합니다. 프로젝트의 *계정* 폴더에는 등록, 로그인, 암호 변경, 액세스 권한 부여의 여러 부분을 구현 하는 파일이 포함 되어 있습니다. 또한 ASP.NET Web Forms는 OAuth 및 Openid connect를 지원 합니다. 이러한 향상 된 인증 기능을 통해 사용자는 Facebook, Twitter, Windows Live, Google 등의 계정에서 기존 자격 증명을 사용 하 여 사이트에 로그인 할 수 있습니다.
> 
> ![프로젝트 솔루션 탐색기 만들기 (ASP.NET Identity)](create-the-project/_static/image7.png)
> 
> 기본적으로 템플릿은 SQL Server Express LocalDB의 인스턴스에 기본 데이터베이스 이름을 사용 하 여 멤버 자격 데이터베이스를 만듭니다. 여기에는 웹 Visual Studio Express 2013와 함께 제공 되는 개발 데이터베이스 서버가 있습니다.
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx) 는 SQL Server 데이터베이스의 프로그래밍 기능을 많이 포함 하는 SQL Server의 경량 버전입니다. SQL Server Express LocalDB는 사용자 모드에서 실행 되며 설치 필수 구성 요소에 대 한 간단한 목록이 포함 된, 구성이 필요 없는 빠른 설치가 있습니다. Microsoft SQL Server에서 데이터베이스 또는 Transact-sql 코드를 SQL Server Express LocalDB에서 SQL Server로 이동 하 고 업그레이드 단계 없이 SQL Azure 수 있습니다. 따라서 SQL Server Express LocalDB는 모든 버전의 SQL Server를 대상으로 하는 응용 프로그램을 위한 개발자 환경으로 사용할 수 있습니다. SQL Server Express LocalDB를 사용 하면 저장 프로시저, 사용자 정의 함수 및 집계, .NET Framework 통합, 공간 형식 및 SQL Server Compact에서 사용할 수 없는 기타 기능을 사용할 수 있습니다.
> 
> **마스터 페이지**
> 
> [ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/wtxbf3hh.aspx) 는 응용 프로그램의 모든 페이지에 대 한 일관 된 모양 및 동작을 정의 합니다. 마스터 페이지의 레이아웃은 개별 콘텐츠 페이지의 내용과 병합 되어 사용자에 게 표시 되는 최종 페이지를 생성 합니다. 정문 장난감 응용 프로그램에서, 정문 장난감 웹 사이트의 모든 페이지가 동일한 독특한 로고 및 탐색 모음을 공유 하도록 *site.master* 마스터 페이지를 수정 합니다.
> 
> **HTML5**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿은 최신 버전의 HTML 태그 언어인 [HTML5](http://www.w3schools.com/html/html5_intro.asp)를 지원 합니다. HTML5는 웹 사이트를 쉽게 만들 수 있도록 하는 새로운 요소와 기능을 지원 합니다.
> 
> **Modernizr**
> 
> HTML5를 지원 하지 않는 브라우저의 경우 [Modernizr](http://www.modernizr.com/)를 사용할 수 있습니다. Modernizr는 브라우저에서 HTML5 기능을 지원 하는지 여부를 검색할 수 있는 오픈 소스 JavaScript 라이브러리 이며 그렇지 않은 경우 사용 하도록 설정 합니다. ASP.NET Web Forms 응용 프로그램 템플릿에서 Modernizr은 NuGet 패키지로 설치 됩니다.
> 
> **부트스트랩**
> 
> Visual Studio 2013 프로젝트 템플릿은 Twitter를 사용 하 여 생성 된 레이아웃 및 테마 프레임 워크인 [부트스트랩](http://getbootstrap.com/)을 사용 합니다. 부트스트랩은 CSS3를 사용 하 여 반응 형 디자인을 제공 합니다. 즉, 레이아웃이 여러 브라우저 창 크기에 맞게 동적으로 조정 될 수 있습니다. 부트스트랩의 테마 기능을 사용 하 여 응용 프로그램의 모양과 느낌을 쉽게 변경할 수도 있습니다. 기본적으로 Visual Studio 2013의 ASP.NET 웹 응용 프로그램 템플릿은 부트스트랩을 NuGet 패키지로 포함 합니다.
> 
> **NuGet 패키지**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿에는 [NuGet](http://www.nuget.org/) 패키지 집합이 포함 되어 있습니다. 이러한 패키지는 오픈 소스 라이브러리 및 도구의 형태로 구성 요소화 된 기능을 제공 합니다. 응용 프로그램을 만들고 테스트 하는 데 도움이 되는 다양 한 패키지가 있습니다. Visual Studio를 사용 하면 NuGet 패키지를 쉽게 추가, 제거 및 업데이트할 수 있습니다. 개발자는 NuGet에도 패키지를 만들고 추가할 수 있습니다.
> 
> ![프로젝트-NuGet 대화 상자 만들기](create-the-project/_static/image8.png)
> 
> 패키지를 설치할 때 NuGet은 파일을 솔루션에 복사 하 고 웹 응용 프로그램과 연결 된 구성 변경 및 참조 추가와 같은 필요한 변경 내용을 자동으로 만듭니다. 라이브러리를 제거 하려는 경우 NuGet은 파일을 제거 하 고 프로젝트에서 수행 되는 모든 변경 내용을 취소 하 여 사용자가 더 이상 남아 있지 않도록 합니다. NuGet은 Visual Studio의 **도구** 메뉴에서 사용할 수 있습니다.
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/) 는 신속한 웹 개발을 위한 HTML 문서 트래버스, 이벤트 처리, 애니메이션 및 Ajax 상호 작용을 간소화 하는 빠르고 간결한 JavaScript 라이브러리입니다. JQuery JavaScript 라이브러리는 ASP.NET Web Forms 응용 프로그램 템플릿에 NuGet 패키지로 포함 되어 있습니다.
> 
> **조심 스럽게 유효성 검사**
> 
> 기본 제공 유효성 검사기 컨트롤이 클라이언트 쪽 유효성 검사 논리에 대해 적합 하지 않은 JavaScript를 사용 하도록 구성 되었습니다. 이렇게 하면 페이지 태그에서 인라인으로 렌더링 된 JavaScript의 양이 크게 줄어들고 전체 페이지 크기가 줄어듭니다. 응용 프로그램의 루트에 있는 web.config 파일의 &lt;appSettings&gt; 요소에 있는 설정을 기반으로 ASP.NET Web Forms 응용 프로그램 템플릿에 대 한 비-유효성 검사를 전역적으로 *추가 합니다.*
> 
> **Entity Framework Code First**
> 
> ASP.NET Web Forms 응용 프로그램 템플릿의 기능 외에도, 정문 장난감 응용 프로그램은 데이터 작업 시 코드 중심 개발을 가능 하 게 하는 NuGet 라이브러리인 [Entity Framework Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)를 사용 합니다. 간단히 말해서, 작성 하는 코드에 따라 응용 프로그램의 데이터베이스 부분을 만듭니다. Entity Framework를 사용 하 여 데이터를 강력한 형식의 개체로 검색 하 고 조작 합니다. 이를 통해 데이터에 액세스 하는 방법에 대 한 세부 정보가 아닌 응용 프로그램의 비즈니스 논리에 집중할 수 있습니다.
> 
> ASP.NET Web Forms 템플릿에 포함 된 설치 된 라이브러리와 패키지에 대 한 자세한 내용은 설치 된 NuGet 패키지의 목록을 참조 하세요. 이렇게 하려면 Visual Studio에서 새 Web Forms 프로젝트를 만들고 **도구** > **nuget 패키지 관리자** > **솔루션용 nuget 패키지 관리**를 선택한 다음 **Nuget 패키지 관리** 대화 상자에서 **설치 된 패키지** 를 선택 합니다.

### <a name="touring-visual-studio"></a>여행용 Visual Studio

Visual Studio의 주 창에는 **솔루션 탐색기**, **서버 탐색기** (Express의**데이터베이스 탐색기** ), **속성 창**, **도구 상자**, **도구 모음**및 **문서 창이**포함 됩니다.

![프로젝트-NuGet 대화 상자 만들기](create-the-project/_static/image9.png)

Visual Studio에 대 한 자세한 내용은 visual [Web Developer의 시각적 가이드](https://msdn.microsoft.com/library/ee410104.aspx)를 참조 하세요.

## <a name="summary"></a>요약

이 자습서에서는 기본 Web Forms 응용 프로그램을 만들어 검토 하 고 실행 했습니다. 기본 Web forms 응용 프로그램의 다양 한 기능을 검토 하 고 Visual Studio 환경을 사용 하는 방법에 대 한 몇 가지 기본 사항을 배웠습니다. 다음 자습서에서는 데이터 액세스 계층을 만듭니다.

## <a name="additional-resources"></a>추가 리소스

[적절 한 프로그래밍 모델 선택](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
웹 [응용 프로그램 프로젝트와 웹 사이트 프로젝트 비교](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web Forms 페이지 개요](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [이전](introduction-and-overview.md)
> [다음](create_the_data_access_layer.md)
