---
uid: single-page-application/overview/templates/hottowel-template
title: Hot 수건 템플릿 | Microsoft Docs
author: madskristensen
description: HotTowel 템플릿
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467141"
---
# <a name="hot-towel-template"></a>Hot Towel 템플릿

[Mads Kristensen](https://github.com/madskristensen)

> 수건 MVC 템플릿은 John Papa에 의해 기록 됩니다.
> 
> 다운로드할 버전 선택:
> 
> [Visual Studio 2012 용 핫 수건 MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013에 대 한 Hot 수건 MVC 템플릿](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> Hot 수건: SPA로 이동 하지 않으려고 합니다.

SPA를 빌드하려고 하지만 시작할 위치를 결정할 수 없나요? 상시 수건를 사용 하 고 몇 초 안에 SPA 및 모든 도구를 구축 해야 합니다!

Hot 수건는 ASP.NET를 사용 하 여 SPA (단일 페이지 응용 프로그램)를 빌드하기 위한 좋은 시작점을 만듭니다. 기본적으로 코드에 대 한 모듈식 구조, 보기 탐색, 데이터 바인딩, 다양 한 데이터 관리 및 간단 하지만 세련 된 스타일을 제공 합니다. 핫 수건는 SPA를 구축 하는 데 필요한 모든 것을 제공 하므로, 앱에 집중할 수 있습니다.

> [John Papa의 비디오, 자습서 및 Pluralsight 과정](http://johnpapa.net/spa?vsix)에서 SPA를 구축 하는 방법에 대해 자세히 알아보세요.

## <a name="application-structure"></a>응용 프로그램 구조

Hot 수건 SPA는 응용 프로그램을 정의 하는 JavaScript 및 HTML 파일이 포함 된 앱 폴더를 제공 합니다.

앱 폴더 내:

- durandal
- services
- viewmodel
- 뷰

앱 폴더에는 모듈의 컬렉션이 포함 되어 있습니다. 이러한 모듈은 기능을 캡슐화 하 고 다른 모듈에 대 한 종속성을 선언 합니다. Views 폴더에는 응용 프로그램에 대 한 HTML이 포함 되며 viewmodel 폴더에는 보기에 대 한 프레젠테이션 논리 (일반적인 MVVM 패턴)가 포함 되어 있습니다. 서비스 폴더는 HTTP 데이터 검색 또는 로컬 저장소 상호 작용과 같이 응용 프로그램에 필요할 수 있는 모든 공통 서비스를 보관 하는 데 적합 합니다. 여러 viewmodel에서 서비스 모듈의 코드를 다시 사용 하는 것이 일반적입니다.

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC 서버 쪽 응용 프로그램 구조

핫 수건는 친숙 하 고 강력한 ASP.NET MVC 구조를 기반으로 합니다.

- 앱\_시작
- 콘텐츠
- Controllers
- 모델
- 스크립트
- 뷰

## <a name="featured-libraries"></a>주요 라이브러리

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET 웹 최적화-묶음 및 축소
- [간편](http://Breezejs.com) 하 게 .js-풍부한 데이터 관리
- [Durandal](http://Durandaljs.com) -탐색 및 뷰 컴퍼지션
- [.Js](http://Knockoutjs.com) -데이터 바인딩
- [Node.js 필요](http://requirejs.org) -AMD 및 최적화를 사용한 모듈화
- [To a](http://jpapa.me/c7toastr) 팝업 메시지
- [Twitter 부트스트랩](https://twitter.github.com/bootstrap/) -강력한 CSS 스타일 지정

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Visual Studio 2012 핫 수건 SPA 템플릿을 통해 설치

Hot 수건은 Visual Studio 2012 템플릿으로 설치할 수 있습니다. `File` | `New Project` 클릭 하 고 `ASP.NET MVC 4 Web Application`를 선택 합니다. 그런 다음 ' Hot 수건 단일 페이지 응용 프로그램 "템플릿을 선택 하 고 실행 합니다.

## <a name="installing-via-the-nuget-package"></a>NuGet 패키지를 통해 설치

Hot 수건는 기존의 빈 ASP.NET MVC 프로젝트를 보강 하는 NuGet 패키지 이기도 합니다. Nuget을 사용 하 여 설치 하 고 실행 하세요.

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>핫 수건에서 빌드하려면 어떻게 하나요?

단순히 코드 추가를 시작 합니다.

1. 사용자 고유의 서버 쪽 코드, 특히 Entity Framework 및 WebAPI를 추가 합니다 (이는 간단한 .js를 사용 하 여).
2. `App/views` 폴더에 보기 추가
3. `App/viewmodels` 폴더에 viewmodel 추가
4. HTML 추가 및 새 뷰에 데이터 바인딩 녹아웃
5. `shell.js`의 탐색 경로를 업데이트 합니다.

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript 연습

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index. cshtml는 MVC 응용 프로그램의 시작 경로 및 뷰입니다. 여기에는 모든 표준 meta 태그, css 링크 및 원하는 JavaScript 참조가 포함 됩니다. 본문에는 모든 콘텐츠 (보기)가 요청 될 때 배치 되는 단일 `<div>` 포함 되어 있습니다. `@Scripts.Render`를 사용 하 여 `main.js` 파일에 포함 된 응용 프로그램 코드에 대 한 입구 지점을 실행 해야 합니다. 앱이 로드 되는 동안 시작 화면을 만드는 방법을 보여 주기 위해 시작 화면이 제공 됩니다.

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>앱/기본 .js

`main.js` 파일에는 앱이 로드 되는 즉시 실행 되는 코드가 포함 되어 있습니다. 탐색 경로를 정의 하 고, 시작 뷰를 설정 하 고, 응용 프로그램의 데이터를 준비 하는 등의 설정/부트스트래핑을 수행 하려는 경우입니다.

`main.js` 파일은 응용 프로그램 시작에 도움이 되는 몇 가지 durandal 모듈을 정의 합니다. Define 문은 모듈 종속성을 확인 하는 데 도움이 되며 함수에 사용할 수 있습니다. 먼저 디버깅 메시지를 사용할 수 있으며,이는 응용 프로그램이 콘솔 창에 수행 중인 이벤트에 대 한 메시지를 보냅니다. 응용 프로그램 시작 코드는 응용 프로그램을 시작 하도록 durandal framework에 알립니다. 규칙은 durandal가 모든 뷰와 viewmodel 동일한 명명 된 폴더에 포함 되어 있음을 알 수 있도록 설정 됩니다. 마지막으로 `app.setRoot`는 미리 정의 된 `entrance` 애니메이션을 사용 하 여 `shell`을 로드 합니다.

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>뷰

보기는 `App/views` 폴더에 있습니다.

### <a name="shellhtml"></a>shell.html

`shell.html`는 HTML에 대 한 마스터 레이아웃을 포함 합니다. 다른 모든 보기는 `shell` 보기의 한쪽에 구성 됩니다. Hot 수건는 머리글, 콘텐츠 영역 및 바닥글의 세 가지 영역을 포함 하는 `shell`를 제공 합니다. 이러한 각 지역은 요청 시 내용 폼과 함께 로드 됩니다.

머리글 및 바닥글에 대 한 `compose` 바인딩은 각각 `nav` 및 `footer` 뷰를 가리키도록 핫 수건 하드 코딩 됩니다. `#content` 섹션의 작성 바인딩은 `router` 모듈의 활성 항목에 바인딩됩니다. 즉, 탐색 링크를 클릭 하면 해당 뷰가이 영역에 로드 됩니다.

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html`은 SPA에 대 한 탐색 링크를 포함 합니다. 예를 들어 메뉴 구조를 배치할 수 있습니다. 이는 `shell.js`에서 정의한 탐색을 표시 하는 데 사용 되는 데이터 바인딩 (녹아웃 사용)이 `router` 모듈에 자주 사용 됩니다. 녹아웃은 데이터 바인딩 특성을 검색 하 여 탐색 경로를 표시 하 고 `router` 모듈이 한 뷰에서 다른 뷰로 이동 하는 중에는 (Twitter 부트스트랩 사용) progressbar를 표시 하는 `shell` viewmodel에 바인딩합니다 (`router.isNavigating`참조).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>.html 및 details

이러한 보기에는 사용자 지정 보기에 대 한 HTML이 포함 되어 있습니다. `nav` 보기 메뉴의 `home` 링크를 클릭 하면 `home` 뷰가 `shell` 뷰의 콘텐츠 영역에 배치 됩니다. 이러한 보기를 사용자 지정 보기로 확대 하거나 바꿀 수 있습니다.

### <a name="footerhtml"></a>footer.html

`footer.html`는 바닥글에 `shell` 보기의 맨 아래에 나타나는 HTML을 포함 합니다.

## <a name="viewmodels"></a>ViewModels

ViewModels은 `App/viewmodels` 폴더에 있습니다.

### <a name="shelljs"></a>shell .js

`shell` viewmodel에는 `shell` 뷰에 바인딩된 속성 및 함수가 포함 되어 있습니다. 메뉴 탐색 바인딩이 발견 되는 경우가 종종 있습니다 (`router.mapNav` 논리 참조).

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>default.js 및 세부 정보 .js

이러한 viewmodel `home` 뷰에 바인딩되는 속성 및 함수를 포함 합니다. 또한 보기의 프레젠테이션 논리를 포함 하며 데이터와 뷰 간의 붙이기가 됩니다.

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>Services

서비스는 App/services 폴더에서 찾을 수 있습니다. 원격 데이터 가져오기 및 게시를 담당 하는 dataservice 모듈과 같은 향후 서비스를 배치할 수 있는 것이 가장 좋습니다.

### <a name="loggerjs"></a>logger.js

Hot 수건는 services 폴더에 `logger` 모듈을 제공 합니다. `logger` 모듈은 pop up 알림을에서 콘솔 및 사용자에 게 메시지를 로깅하는 데 적합 합니다.
