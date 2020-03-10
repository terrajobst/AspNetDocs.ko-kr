---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: Visual Studio 2013 릴리스 정보에 대 한 ASP.NET 및 Web Tools 2013.2 Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505451"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>Visual Studio 2013용 ASP.NET 및 Web Tools 2013.2 릴리스 정보

[Microsoft](https://github.com/microsoft) 에서

## <a name="installation-notes"></a>설치 참고 사항

Visual Studio 2013.2에 대 한 ASP.NET 및 Web Tools는 기본 설치 관리자에 번들로 제공 되며 [Visual Studio 2013 업데이트 2](https://go.microsoft.com/fwlink/?LinkId=390521)의 일부로 다운로드할 수 있습니다.

## <a name="documentation"></a>문서화

Visual Studio 2013.2 ASP.NET 및 Web Tools에 대 한 자습서 및 기타 정보는 [ASP.NET 웹 사이트](https://www.asp.net/)에서 확인할 수 있습니다.

## <a name="software-requirements"></a>소프트웨어 요구 사항

Visual Studio 2013.2에 대 한 ASP.NET 및 Web Tools Visual Studio 2013 필요 합니다.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Visual Studio 2013.2에 대 한 ASP.NET 및 Web Tools의 새로운 기능

다음 섹션에서는 릴리스에 도입 된 기능에 대해 설명 합니다.

- [ASP.NET 프로젝트 템플릿 하나](#oneaspnet)
- [IIS Express에서 웹 응용 프로그램을 시작할 때 SSL 지원](#ssl)
- [Visual Studio 웹 편집기의 향상 된 기능](#vswebeditor)
- [브라우저 링크](#browserlink)
- [Visual Studio의 Azure App Service Web Apps 지원](#waws)
- [새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기](#AzureResources)
- [웹 게시 향상](#webpublish)
- [ASP.NET 스 캐 폴딩](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [ASP.NET Web Forms](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET Web API 2.1.2](#webapi)
- [ASP.NET 웹 페이지 3.1.2](#webpages)
- [Entity Framework 6.1](#ef)
- [ASP.NET Identity 2.0.0](#identity)
- [Microsoft OWIN 구성 요소](#owin)
- [ASP.NET SignalR 2.0.2](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>ASP.NET 프로젝트 템플릿 하나

- 계정 확인 및 암호 재설정을 지원 하도록 ASP.NET 프로젝트 템플릿을 업데이트 합니다.
- 온-프레미스 조직 계정을 사용한 인증을 지원 하도록 ASP.NET Web API 템플릿을 업데이트 합니다.
- 이제 ASP.NET SPA 템플릿에 MVC 및 서버 쪽 보기를 기반으로 하는 인증이 포함 되어 있습니다. 템플릿에는 인증 된 사용자만 액세스할 수 있는 WebAPI 컨트롤러가 있습니다.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>IIS Express에서 웹 응용 프로그램을 시작할 때 SSL 지원

Localhost에서 HTTPS를 검색 하 고 디버그할 때 보안 경고가 나타나지 않게 하려면 Internet Explorer 및 Chrome에서 자체 서명 된 IIS express SSL 인증서를 신뢰할 수 있도록 하는 대화 상자를 추가 했습니다.

예를 들어 웹 프로젝트 속성은 SSL을 사용 하도록 설정할 수 있습니다. F4를 클릭 하 여 속성 대화 상자를 표시 합니다. **SSL 사용** 을 true로 변경 합니다. SSL URL을 복사합니다.

![SSL 사용 속성](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

웹 프로젝트 속성 페이지 웹 탭을 HTTPS 기반 URL을 사용 하도록 설정 합니다. 이전에 SSL 웹 사이트를 만들지 않은 경우에는 SSL URL이 `https://localhost:44300/` 됩니다.

![프로젝트 URL 설정 (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Ctrl+F5를 눌러 애플리케이션을 실행합니다. 지침에 따라 IIS Express 생성 된 자체 서명 된 인증서를 신뢰 합니다.

![SSL 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Localhost를 나타내는 인증서를 설치 하려면 **보안 경고** 대화 상자를 읽은 다음 **예** 를 클릭 합니다.

![보안 경고](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

브라우저에서 인증서 경고 없이 사이트가 IE 또는 Chrome으로 표시 됩니다.

![경고가 없는 HTTPS 페이지](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox는 자체 인증서 저장소를 사용 하므로 경고가 표시 됩니다.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Visual Studio 웹 편집기의 향상 된 기능

- **새 json 프로젝트 항목 및 편집기**: Visual STUDIO에 json 프로젝트 항목 및 편집기를 추가 했습니다. 현재 JSON 편집기 기능에는 색 지정, 구문 유효성 검사, 중괄호 완성, 개요, 도구 옵션 설정 등이 포함 됩니다.

    ![JSON 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense는 이제 [JSON 스키마](http://json-schema.org/) v3 및 v4를 지원 합니다. 기존 스키마를 선택 하거나, 로컬 스키마 경로를 편집 하거나, 프로젝트 JSON 파일을 끌어 놓는 방법으로 상대 경로를 가져오도록 스키마 콤보 상자가 있습니다.

    ![JSON Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![JSON 스키마 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **SCSS (New Sass) 편집기**: VS2013 RTM에서 추가 했으며 이제 Sass 프로젝트 항목 및 편집기가 있습니다. Sass 편집기 기능은 LESS 편집기와 유사 하며, 색 지정, 변수 및 Mixin IntelliSense, 주석/주석 제거, 요약 정보, 서식 지정, 구문 유효성 검사, 개요, goto 정의, 색 선택, 도구 옵션 설정 등을 포함 합니다.

    ![새 항목 추가: SCSS 스타일 시트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![스타일 시트 편집기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **HTML, Razor, CSS, LESS 및 Sass 문서에서 새 URL 선택:** VS 2013는 Web Forms 페이지 외부에서 URL을 선택 하지 않은 상태로 제공 됩니다. HTML, Razor, CSS, LESS 및 Sass 편집기에 대 한 새 URL 선택기는 '.. '를 이해 하는 대화 상자를 사용 하지 않는 흐름 입력 선택기입니다. 및는 img 태그 및 링크에 대 한 파일 목록을 적절 하 게 필터링 합니다.

    ![이미지 태그의 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![보기에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![CSS에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **더 많은 기능을 추가 하 여 더 작은 편집기로 업데이트**
- **Intellisense 업그레이드 녹아웃**: vs Intellisense "ko-편집기 viewModel:" 구문에 대해 비표준 녹아웃 구문을 추가 했습니다. 다음 형식으로 주석을 사용 하 여 페이지의 여러 뷰 모델에 바인딩하는 데 사용할 수 있습니다.

    ![Intellisense 녹아웃](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    또한 중첩 된 ViewModel IntelliSense에 대 한 지원도 추가 되어 ViewModel에서 깊게 중첩 된 개체를 살펴볼 수 있습니다.

    `<div data-bind="text: foo.bar.baz.etc" />`

    표시 되는 IntelliSense는 JavaScript 개체의 전체 IntelliSense입니다.

    ![전체 JavaScript 개체를 표시 하는 Intellisense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **HTML, Razor, CSS, LESS 및 Sass 문서에서 새 url을 선택**합니다. VS 2013는 Web Forms 페이지 외부에서 URL을 선택 하지 않은 상태로 제공 됩니다. HTML, Razor, CSS, LESS 및 Sass 편집기에 대 한 새 URL 선택기는 '.. '를 이해 하는 대화 상자를 사용 하지 않는 흐름 입력 선택기입니다. 및는 img 태그 및 링크에 대 한 파일 목록을 적절 하 게 필터링 합니다.

    ![이미지 태그의 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![보기에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![CSS에 대 한 URL 선택기](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>브라우저 링크

- 이제 브라우저 링크에서 HTTPS 연결을 지원 하며, 브라우저에서 인증서를 신뢰할 수 있는 한 대시보드에서 다른 연결을 사용 하는 것을 나열 합니다.
- 정적 HTML 원본 매핑
- 데이터 매핑을 위한 SPA 지원
- 매핑 데이터 자동 업데이트

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Visual Studio의 Azure App Service Web Apps 지원

- **Azure 로그인을 지원 합니다.**
- **웹 앱에 대 한 원격 디버깅 및 원격 보기**: 이제 서버 탐색기에서 웹 앱 콘텐츠 파일의 Azure App Service 및 원격 보기 [에서 웹 앱에 대 한 원격 디버깅](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) 을 지원 합니다.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>새 웹 프로젝트를 만들 때 원격 Azure 리소스 만들기

새 웹 응용 프로그램 대화 상자에서 Azure ["원격 리소스 만들기"](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) 확인란을 추가 했습니다. 이를 선택 하면 새 웹 응용 프로그램을 만들고, 테스트를 위해 Azure 게시 사이트를 설정 하 고, 몇 가지 간단한 단계로 게시 프로필을 만드는 환경을 통합할 수 있습니다.

![Azure 리소스를 사용 하는 새 프로젝트](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Azure에 게시](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>웹 게시 향상

- 게시를 위한 사용자 환경을 개선 합니다.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

- **열거형 지원:** 모델에서 열거형을 사용 하는 경우 MVC 스 캐 폴더은 열거형에 대 한 드롭다운을 생성 합니다. MVC의 Enum 도우미를 사용 합니다.
- **부트스트랩 지원**: 부트스트랩 클래스를 사용 하도록 MVC 스 캐 폴딩의 템플릿에 대 한 editorfor 업데이트 했습니다.
- **패키지 지원**: Mvc 및 Web api SCAFFOLDERS는 Mvc 및 web api 용 5.1 패키지를 추가 합니다.

다음 스크린샷은 스 캐 폴딩 모델을 보여 줍니다.

- 모델 코드:

     ![모델 코드](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- 모델 코드를 컴파일하고 마우스 오른쪽 단추를 클릭 한 다음 **추가**, **새 스 캐 폴드 항목**을 선택 합니다.

     ![새 스 캐 폴드 항목 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- **Entity Framework를 사용 하 여 뷰가 있는 MVC5 Controller를 선택 합니다**.

     ![뷰가 포함 된 새 MVC5 controller 추가](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- 모델을 사용 하 여 **컨트롤러 추가** :

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- 생성 된 코드를 확인 합니다. 예를 들어 Views/WeekdayModels/EnumDropDownListFor에는 `@Html.EnumDropDownListFor`포함 되어 있습니다. ![View에는가 포함 되어 있습니다](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png)
- 페이지를 실행 하 여 생성 된 열거 combobox를 확인 합니다. 값이 null 일 수 있는 경우 콤보 상자에 대해 빈 문자열을 선택할 수 있습니다. 예를 들어 **만들기** 페이지에는 다음이 표시 됩니다.

    ![빈 문자열을 허용 하는 콤보 상자](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM은 4 월 2014 일에 출시 될 예정입니다. 릴리스 정보에 대 한 자세한 내용은 다음을 참조 하세요 .이 변경 내용에 대 한 자세한 내용은 [전체 릴리스](http://docs.nuget.org/docs/release-notes/nuget-2.8) 정보를 두드러진 몇 가지.

- **대상 Windows Phone 8.1 응용 프로그램**: 이제 NuGet 2.8.1 대상 프레임 워크 모니커 ' WindowsPhoneApp ', ' WPA ', ' WindowsPhoneApp81 ' 및 ' WPA81 '를 사용 하 여 Windows Phone 8.1 응용 프로그램을 대상으로 지원 합니다.

- **종속성에 대 한 패치 해결**: 패키지 종속성을 확인할 때 NuGet은 패키지의 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 했습니다. 그러나 주 버전과 부 버전이 달리 패치 버전은 항상 가장 높은 버전으로 확인 되었습니다. 이 동작은 잘 악의적 종속성이 포함 된 패키지를 설치 하는 것이 적합 하지 않습니다.
- **DependencyVersion 스위치**: NuGet 2.8은 종속성 확인을 위한 *기본* 동작을 변경 하지만 패키지 관리자 콘솔에서-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 정확 하 게 제어할 수 있습니다. 스위치를 사용 하면 가능한 가장 낮은 버전 (기본 동작), 가능한 가장 높은 버전 또는 가장 높은 부 또는 패치 버전으로 종속성을 확인할 수 있습니다. 이 스위치는 powershell 명령에서 설치 패키지에 대해서만 작동 합니다.
- **DependencyVersion Attribute**: 위에서 설명한-DependencyVersion 스위치 외에도 nuget은 설치-패키지 호출에-DependencyVersion 스위치를 지정 하지 않은 경우 기본값을 정의 하는 nuget 파일에 새 특성을 설정 하는 기능을 허용 합니다. 이 값은 또한 패키지 설치 작업에 대 한 NuGet 패키지 관리자 대화 상자에서 적용 됩니다. 이 값을 설정 하려면 아래 특성을 nuget.exe 파일에 추가 합니다.

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **-WhatIf를 사용 하 여 Nuget 작업 미리 보기**: 일부 NuGet 패키지는 심층 종속성 그래프를 포함할 수 있습니다. 따라서 설치, 제거 또는 업데이트 작업을 수행 하는 동안에는 먼저 어떻게 되는지 확인 하는 데 도움이 될 수 있습니다. NuGet 2.8은 명령이 적용 되는 패키지의 전체 클로저를 시각화할 수 있도록 표준 PowerShell-what if if 스위치를 설치 패키지, 제거 패키지 및 업데이트 패키지 명령에 추가 합니다.
- **패키지 다운 그레이드**: 새 기능을 조사 하 여 안정적인 최신 버전으로 롤백하는 것을 결정 하기 위해 시험판 버전의 패키지를 설치 하는 것은 드문 일이 아닙니다. NuGet 2.8 이전 버전은 시험판 패키지와 해당 종속성을 제거한 후 이전 버전을 설치 하는 여러 단계로 이루어진 프로세스 였습니다. 그러나 NuGet 2.8에서 업데이트 패키지는 이제 전체 패키지 닫기 (예: 패키지의 종속성 트리)를 이전 버전으로 롤백합니다.
- **개발 종속성**: 개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 다양 한 유형의 기능을 NuGet 패키지로 제공할 수 있습니다. 이러한 구성 요소는 새 패키지를 개발 하는 데 사용할 수 있는 반면 나중에 게시 될 때 새 패키지의 종속성으로 간주 되지 않아야 합니다. NuGet 2.8을 사용 하면 패키지에서 nuspec 파일을 developmentDependency로 스스로 식별할 수 있습니다. 설치 된 경우이 메타 데이터는 패키지가 설치 된 프로젝트의 패키지 .config 파일에도 추가 됩니다. Nuget.exe 팩을 실행 하는 동안 해당 패키지 .config 파일이 NuGet 종속성에 대해 나중에 분석 되는 경우 개발 종속성으로 표시 된 종속성을 제외 합니다.
- 여러 **플랫폼에 대 한 개별 패키지 .Config 파일**: 여러 대상 플랫폼용 응용 프로그램을 개발 하는 경우 각 빌드 환경에 대해 서로 다른 프로젝트 파일을 포함 하는 것이 일반적입니다. 또한 패키지 마다 다양 한 플랫폼에 대 한 다양 한 지원 수준이 있기 때문에 다양 한 프로젝트 파일에서 다른 NuGet 패키지를 사용 하는 것이 일반적입니다. NuGet 2.8은 플랫폼별 프로젝트 파일 마다 다른 패키지 .config 파일을 만들어이 시나리오에 대 한 향상 된 지원을 제공 합니다.
- **로컬 캐시로 대체**: nuget 패키지는 일반적으로 네트워크 연결을 사용 하 여 [nuget 갤러리](http://www.nuget.org) 와 같은 원격 갤러리에서 사용 되지만 클라이언트가 연결 되지 않은 많은 시나리오가 있습니다. 네트워크에 연결 되지 않은 경우 NuGet 클라이언트는 패키지를 성공적으로 설치할 수 없습니다. 해당 패키지는 로컬 NuGet 캐시의 클라이언트 컴퓨터에 이미 있는 경우에도 마찬가지입니다. NuGet 2.8은 패키지 관리자 콘솔에 자동 캐시 대체를 추가 합니다.

    캐시 대체 (fallback) 기능에는 특정 명령 인수가 필요 하지 않습니다. 또한 cache fallback은 현재 패키지 관리자 콘솔 에서만 작동 합니다 .이 동작은 현재 패키지 관리자 대화 상자에서 작동 하지 않습니다.
- **버그 수정**: 업데이트-패키지-다시 설치 명령에서 수행 되는 주요 버그 수정 사항 중 하나는 성능 향상입니다.

    이러한 기능 외에도이 NuGet 릴리스에는 기타 많은 버그 수정이 포함 되어 있습니다. 릴리스에서 해결 된 총 181 개의 문제가 있습니다. NuGet 2.8에서 수정 된 작업 항목의 전체 목록은이 릴리스에 대 한 [Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) 를 확인 하세요.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET 웹 양식

- 이제 Web Forms 템플릿에는 ASP.NET Identity에 대 한 계정 확인 및 암호 재설정을 수행 하는 방법이 나와 있습니다.
- Entity Framework 6의 엔터티 데이터 소스 컨트롤 및 Dynamic Data 공급자입니다. 자세한 내용은 MSDN 블로그 [Dynamic Data provider And EntityDataSource control for Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx)을 참조 하세요.

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [특성 라우팅 개선 사항](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [편집기 템플릿에 대 한 부트스트랩 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [뷰에서 열거형 지원](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [MinLength/MaxLength 특성을 지원 하지 않습니다.](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [조심 스럽게 Ajax에서 ' this ' 컨텍스트 지원](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET Web API 2.1.2

- [전역 오류 처리](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [특성 라우팅 향상](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [도움말 페이지 개선 사항](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [IgnoreRoute 지원](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON 미디어 형식 포맷터](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [비동기 필터에 대 한 지원 향상](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [클라이언트 서식 라이브러리에 대 한 쿼리 구문 분석](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET 웹 페이지 3.1.2

- 다양 한 [버그 수정](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6.1

런타임 및 도구 모두에 대해 Entity Framework 버전 6.1로 업데이트 되었습니다. EF (Entity Framework) 6.1는 Entity Framework 6의 사소한 업데이트 이며 많은 버그 수정과 새로운 기능을 포함 합니다. 새 기능에 대 한 설명서 링크를 비롯 하 여 EF 6.1에 대 한 자세한 내용은 [Entity Framework 버전 기록](https://msdn.microsoft.com/data/jj574253)을 참조 하세요. 이 릴리스의 새로운 기능은 다음과 같습니다.

- **도구 통합** 은 새 EF 모델을 만드는 일관 된 방법을 제공 합니다. 이 기능은 ADO.NET 엔터티 데이터 모델 마법사를 확장 하 여 기존 데이터베이스에서 리버스 엔지니어링을 비롯 한 Code First 모델 만들기를 지원 합니다. 이러한 기능은 이전에 EF Power Tools의 베타 품질로 제공 되었습니다.
- **트랜잭션 커밋 실패를 처리** 하면 새로 도입 된 트랜잭션 작업 가로채기 기능을 사용 하는 새 [CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) 이 제공 됩니다. **CommitFailureHandler** 는 트랜잭션을 커밋하는 동안 연결 오류를 자동으로 복구할 수 있도록 합니다.
- **Indexattribute** 를 사용 하면 Code First 모델의 속성에 특성을 배치 하 여 인덱스를 지정할 수 있습니다. 그러면 Code First는 데이터베이스에 해당 인덱스를 만듭니다.
- **공용 매핑 API는** 속성 및 형식이 데이터베이스의 열과 테이블에 매핑되는 방법에 대 한 정보에 대 한 액세스를 제공 합니다. 이전 릴리스에서이 API는 내부용입니다.
- **앱/web.config 파일을 통해 인터셉터를 구성 하는 기능**(응용 프로그램을 다시 컴파일하지 않고 인터셉터를 추가할 수 있음)
- **Databaselogger** 모든 데이터베이스 작업을 파일에 쉽게 기록할 수 있게 해 주는 새로운 인터셉터입니다. 이전 기능과 함께이 기능을 사용 하면 다시 컴파일하지 않아도 배포 된 응용 프로그램에 대 한 데이터베이스 작업의 로깅을 쉽게 전환할 수 있습니다.
- **마이그레이션 모델 변경 검색** 은 스 캐 폴드 마이그레이션의 정확성을 높이기 위해 개선 되었습니다. 변경 내용 검색 프로세스의 성능도 크게 향상 되었습니다.
- 초기화 중 데이터베이스 작업 감소, LINQ 쿼리의 null 같음 비교에 대 한 최적화, 더 많은 시나리오에서 더 빠른 보기 생성 (모델 생성), 여러 연결이 있는 추적 된 엔터티의 보다 효율적인 구체화 등의 **성능 향상**

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0.0

- **2 단계 인증**: ASP.NET Identity 이제 2 단계 인증을 지원 합니다. 2 단계 인증은 암호가 손상 되는 경우 사용자 계정에 대 한 추가 보안 계층을 제공 합니다. 또한 두 개의 요소 코드에 대 한 무차별 암호 대입 공격을 방지 합니다.
- **계정 잠금:** 사용자가 암호 또는 2 단계 코드를 잘못 입력 하는 경우 사용자를 잠그는 방법을 제공 합니다. 잘못 된 시도 수와 사용자에 대 한 timespan timespan을 구성할 수 있습니다. 개발자는 필요에 따라 특정 사용자 계정에 대 한 계정 잠금을 해제할 수 있습니다.
- **계정 확인:** 이제 ASP.NET Identity 시스템에서 계정 확인을 지원 합니다. 오늘날 대부분의 웹 사이트에서 매우 일반적인 시나리오입니다. 웹 사이트에 새 계정을 등록 하는 경우 웹 사이트에서 작업을 수행 하기 전에 전자 메일을 확인 해야 합니다. 전자 메일 확인은 위조 된 계정이 생성 되지 않도록 하기 때문에 유용 합니다. 이 기능은 포럼 사이트, 은행, 전자 상거래 또는 소셜 웹 사이트와 같은 웹 사이트의 사용자와 통신 하는 방법으로 전자 메일을 사용 하는 경우에 매우 유용 합니다.
- **암호 재설정:** 암호 재설정은 사용자가 암호를 잊어버린 경우 암호를 재설정할 수 있는 기능입니다.
- **보안 스탬프 (모든 위치에서 로그 아웃):** 사용자가 암호를 변경 하거나 연결 된 로그인 (예: Facebook, Google, Microsoft 계정 등)을 제거 하는 등의 기타 보안 관련 정보를 변경 하는 경우 사용자에 대 한 보안 토큰을 다시 생성 하는 방법을 지원 합니다. 이전 암호를 사용 하 여 생성 된 토큰을 무효화 하려면이를 수행 해야 합니다. 샘플 프로젝트에서 사용자의 암호를 변경 하는 경우 사용자에 대 한 새 토큰이 생성 되 고 이전 토큰은 무효화 됩니다. 이 기능은 사용자가 암호를 변경 하는 경우이 응용 프로그램에 로그인 한 모든 위치 (다른 모든 브라우저)에서 로그 아웃 되기 때문에 응용 프로그램에 대 한 추가 보안 계층을 제공 합니다.
- **사용자 및 역할의 기본 키 형식을 확장할 수 있도록 설정**: ASP.NET Identity 1.0에서 테이블 사용자 및 역할에 대 한 기본 키의 유형은 문자열입니다. 즉, Entity Framework를 사용 하 여 SQL Server에 ASP.NET Identity 시스템이 지속 된 경우 nvarchar를 사용 하 게 됩니다. Stack Overflow에 대 한이 기본 구현과 들어오는 피드백을 기준으로 많은 토론이 있었습니다. 사용자 및 역할 테이블의 기본 키를 지정할 수 있는 확장성 후크를 제공 합니다. 이 확장성 후크는 응용 프로그램을 마이그레이션하는 경우 사용자 id를 저장 하는 응용 프로그램이 Guid 또는 정수 인 경우에 특히 유용 합니다.
- **사용자 및 역할에 대 한 Iqueryable 지원**: 사용자 저장소 및 역할 저장소의 iqueryable에 대 한 지원이 추가 되어 사용자 및 역할의 목록을 쉽게 가져올 수 있습니다.
- **UserManager를 통한 삭제 작업 지원**
- **사용자 이름 인덱싱**: ASP.NET Identity Entity Framework 구현에서는 EF 6.1.0에서 새 indexattribute를 사용 하 여 사용자 이름에 고유한 인덱스를 추가 했습니다. 이렇게 하면 사용자 이름은 항상 고유 하 고 중복 된 사용자 이름으로 끝날 수 있는 경합 상태가 발생 하지 않습니다.
- **향상 된 암호 유효성 검사기:** ASP.NET Identity 1.0에서 제공 된 암호 유효성 검사기는 최소 길이를 확인 하는 매우 기본적인 암호 유효성 검사기 였습니다. 암호의 복잡성을 보다 강력 하 게 제어할 수 있는 새로운 암호 유효성 검사기가 있습니다. 이 암호의 모든 설정을 사용 하는 경우에도 사용자 계정에 대해 2 단계 인증을 사용 하도록 설정 하는 것이 좋습니다.
- **IdentityFactory 미들웨어/CreatePerOwinContext**:

    - **사용자 관리자**: 팩터리 구현을 사용 하 여 OWIN 컨텍스트에서 usermanager의 인스턴스를 가져올 수 있습니다. 이 패턴은 로그인 및 SignOut에 대 한 OWIN 컨텍스트를 가져오는 데 사용 하는 것과 유사 합니다. 이 방법은 응용 프로그램에 대 한 요청당 UserManager 인스턴스를 가져오는 데 권장 되는 방법입니다.
    - **Dbcontextfactory**: ASP.NET Identity은 SQL Server에서 id 시스템을 유지 하기 위해 Entity Framework를 사용 합니다. 이렇게 하려면 Id 시스템에 ApplicationDbContext에 대 한 참조가 있습니다. DbContextFactory 미들웨어는 응용 프로그램에서 사용할 수 있는 요청당 ApplicationDbContext의 인스턴스를 반환 합니다.
- **ASP.NET Identity 샘플 nuget 패키지**: 샘플 nuget 패키지를 사용 하면 ASP.NET Identity에 대 한 샘플을 보다 쉽게 설치 하 고 실행할 수 있으며 모범 사례를 따를 수 있습니다. 샘플 ASP.NET MVC 응용 프로그램입니다. 프로덕션 환경에 배포 하기 전에 응용 프로그램에 맞게 코드를 수정 하세요. 이 샘플은 빈 ASP.NET 응용 프로그램에 설치 해야 합니다. 패키지에 대 한 자세한 내용은 [ASP.NET Identity의 RTM 발표](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx) 블로그 게시물을 참조 하세요. 2.0.0

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Microsoft OWIN 구성 요소

이 릴리스에서 수정 된 많은 버그가 있습니다. 자세한 내용은 [2.1.0 릴리스에 대 한 릴리스](https://katanaproject.codeplex.com/releases/view/113281) 정보를 참조 하세요.

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>ASP.NET SignalR 2.0.2

이 릴리스에서 수정 된 많은 버그가 있습니다. 자세한 내용은 [2.0.2 릴리스에 대 한 릴리스](https://github.com/SignalR/SignalR/releases/tag/2.0.2) 정보를 참조 하세요.
