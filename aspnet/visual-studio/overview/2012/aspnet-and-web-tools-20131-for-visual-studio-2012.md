---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 ASP.NET 및 Web Tools 2013.1에 대 한 릴리스 정보 | Microsoft Docs
author: microsoft
description: 이 문서에서는 Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1 릴리스를 설명 합니다.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467105"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012용 ASP.NET 및 Web Tools 2013.1 릴리스 정보

[Microsoft](https://github.com/microsoft) 에서

> 이 문서에서는 Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1 릴리스를 설명 합니다.

## <a name="contents"></a>콘텐츠

- [설치 참고 사항](#install)
- [소프트웨어 요구 사항](#requirements)
- Visual Studio 2012 ASP.NET 및 Web Tools 2013.1의 새로운 기능

    - [부트스트랩](#bootstrap)
    - [템플릿](#templates)

        - [ASP.NET MVC 5 템플릿](#mvc5template)
        - [ASP.NET Web API 2 템플릿](#apitemplate)
        - [항목 템플릿](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET 스 캐 폴딩](#scaffold)
    - [Razor 편집기](#razor)
    - [NuGet 2.7](#nuget)
- 알려진 문제 및 주요 변경 내용

    - [ASP.NET 스 캐 폴딩](#issuescaffolding)

        - [MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류](#404issue)
        - [스 캐 폴드 항목을 추가한 후 웹에 대 한 Visual Studio Express 2012의 작동이 중지 됨](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [With 또는 F5를 사용 하 여 cshtml 파일을 보면 서버 오류가 발생 합니다.](#browseissue)
        - [Url 재작성 및 물결표 (~)](#rewriteissue)
    - [템플릿](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>설치 참고 사항

[설치](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012의 ASP.NET 및 Web Tools 2013.1입니다.

<a id="requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

웹에 대해 Visual Studio 2012 또는 Visual Studio Express 2012이 있어야 합니다.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Visual Studio 2012 ASP.NET 및 Web Tools 2013.1의 새로운 기능

<a id="bootstrap"></a>
### <a name="bootstrap"></a>부트스트랩

MVC 5 컨트롤러 및 뷰를 스 캐 폴드 뷰의 태그는 [부트스트랩](http://getbootstrap.com/)을 사용 합니다.

<a id="templates"></a>
### <a name="templates"></a>템플릿

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>ASP.NET MVC 5 템플릿

새 MVC 5 템플릿을 추가 했습니다. 최신 MVC 5 NuGet 패키지를 참조 하 고 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 추가할 수 있습니다.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>ASP.NET Web API 2 템플릿

새 Web API 2 템플릿을 추가 했습니다. 최신 Web API 2 NuGet 패키지를 참조 하 고 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 추가할 수 있습니다.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>항목 템플릿

MVC 5 뷰, 웹 페이지 (Razor 3) 및 Web API 2 컨트롤러에 대 한 새 항목 템플릿을 추가 했습니다. 새 항목을 추가 하는 동안 프로젝트에 관련 NuGet 패키지를 설치 합니다.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Entity Framework를 사용 하 여 MVC 또는 Web API 컨트롤러를 스 캐 폴드 때 프레임 워크 6을 사용 합니다. Entity Framework에 대 한 자세한 내용은 [Entity Framework 버전 기록](https://msdn.com/data/jj574253)을 참조 하세요.

Visual Studio 2012에 대 한 Entity Framework 6 도구를 다운로드 하 여 설치할 수도 있습니다. [Get Entity Framework](https://msdn.com/data/ee712906#tooling)를 참조 하세요.

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

ASP.NET 스 캐 폴딩은 ASP.NET 웹 응용 프로그램에 대 한 코드 생성 프레임 워크입니다. 이를 통해 데이터 모델과 상호 작용 하는 상용구 코드를 프로젝트에 쉽게 추가할 수 있습니다.

이전 버전의 Visual Studio에서 스 캐 폴딩은 ASP.NET MVC 프로젝트로 제한 되었습니다. 이 업데이트를 통해 이제 Web Forms를 포함 하 여 모든 ASP.NET 프로젝트에 스 캐 폴딩을 사용할 수 있습니다. 이 업데이트는 Web Forms 프로젝트에 대 한 페이지 생성을 지원 하지 않지만 프로젝트에 MVC 종속성을 추가 하 여 Web Forms에서 스 캐 폴딩을 계속 사용할 수 있습니다. Web Forms에 대 한 페이지 생성 지원은 향후 업데이트에서 추가 될 예정입니다.

스 캐 폴딩을 사용 하는 경우 모든 필수 종속성이 프로젝트에 설치 되어 있는지 확인 합니다. 예를 들어 ASP.NET Web Forms 프로젝트로 시작한 다음 스 캐 폴딩을 사용 하 여 Web API 컨트롤러를 추가 하는 경우 필요한 NuGet 패키지와 참조가 프로젝트에 자동으로 추가 됩니다.

Web Forms 프로젝트에 MVC 스 캐 폴딩을 추가 하려면 **새 스 캐 폴드 항목** 을 추가 하 고 대화 상자 창에서 **mvc 5 종속성** 을 선택 합니다. MVC 스 캐 폴딩에 대 한 두 가지 옵션이 있습니다. 최소 및 전체. 최소를 선택 하면 ASP.NET MVC에 대 한 NuGet 패키지 및 참조만 프로젝트에 추가 됩니다. 전체 옵션을 선택 하는 경우 최소 종속성 뿐만 아니라 MVC 프로젝트에 필요한 콘텐츠 파일이 추가 됩니다.

비동기 컨트롤러 스 캐 폴딩에 대 한 지원은 Entity Framework 6의 새로운 비동기 기능을 사용 합니다.

자세한 내용 및 자습서는 [ASP.NET 스 캐 폴딩 개요](../2013/aspnet-scaffolding-overview.md)를 참조 하세요. 이러한 자습서는 Visual Studio 2013를 사용 하 여 스 캐 폴딩을 보여 주지만 Visual Studio 2012 용 ASP.NET 및 Web Tools 2013.1에도 적용 됩니다.

<a id="razor"></a>
### <a name="razor-editor"></a>Razor 편집기

이 업데이트를 사용 하면 이제 Visual Studio 2012에서 Razor 3 도구/편집을 지원 합니다.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2.7에는 [nuget 2.7 릴리스 정보](http://docs.nuget.org/docs/release-notes/nuget-2.7)에 자세히 설명 되어 있는 다양 한 새 기능 집합이 포함 되어 있습니다.

이 버전의 NuGet은 사용자가 NuGet이 누락 된 패키지를 복원 하는 것을 명시적으로 허용 하지 않아도 됩니다. NuGet 2.7을 설치 하는 경우 사용자는 누락 된 패키지를 자동으로 복원 하도록 암시적으로 동의 합니다. 사용자는 Visual Studio의 NuGet 설정을 통해 패키지 복원을 명시적으로 옵트아웃 (opt out) 할 수 있습니다. 이렇게 변경 하면 패키지 복원의 작동 방식이 간소화 됩니다.

## <a name="known-issues-and-breaking-changes"></a>알려진 문제 및 주요 변경 내용

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET 스 캐 폴딩

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>MVC 및 Web API 스 캐 폴딩-HTTP 404, 찾을 수 없음 오류

프로젝트에 스 캐 폴드 항목을 추가할 때 오류가 발생 하는 경우 프로젝트가 일관 되지 않은 상태로 남아 있을 수 있습니다. 스 캐 폴딩의 변경 내용 중 일부는 롤백되고, 설치 된 NuGet 패키지와 같은 다른 변경 내용은 롤백되지 않습니다. 라우팅 구성 변경 내용이 롤백되면 사용자는 스 캐 폴드 항목으로 이동할 때 HTTP 404 오류를 받게 됩니다.

MVC에 대 한이 오류를 해결 하려면 새 스 캐 폴드 항목을 추가 하 고 MVC 5 종속성 (최소 또는 전체)을 선택 합니다. 이 프로세스는 프로젝트에 필요한 모든 변경 내용을 추가 합니다.

Web API에 대해이 오류를 해결 하려면:

1. 다음 WebApiConfig 클래스를 프로젝트에 추가 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. 다음과 같이 Global.asax의 응용 프로그램\_Start 메서드에서 WebApiConfig을 구성 합니다.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>스 캐 폴드 항목을 추가한 후 웹에 대 한 Visual Studio Express 2012의 작동이 중지 됨

Entity Framework를 사용 하 여 스 캐 폴드 항목 (예: 작업을 사용 하는 웹 API 2 컨트롤러, Entity Framework을 사용 하는 웹 API 2 컨트롤러)을 추가한 후 2012 Visual Studio Express 웹에 대 한 작업을 중지 하는 경우 어셈블리의 네이티브 이미지를 로드 하지 못할 수 Visual Studio Express 있습니다 System.web. 확장명에 따라 달라 집니다.

이 문제를 해결 하려면 Visual Studio Express를 구성 하 여 system.string의 MSIL 이미지를 사용 합니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. %ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE 또는% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (64 비트 Windows의 경우)로 이동 합니다.
3. 텍스트 편집기에서 VWDExpress을 엽니다.
4. &lt;구성&gt;/&lt;runtime&gt; 요소 아래에 다음 줄을 추가 합니다.  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. 웹에 대해 Visual Studio Express 2012을 다시 시작 합니다.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>With 또는 F5를 사용 하 여 cshtml 파일을 보면 서버 오류가 발생 합니다.

Visual Studio 2012 (또는 Visual Studio 2012에서 Visual Studio 2013 만든 MVC 5 프로젝트를 사용 하 여)에서 MVC 5 프로젝트를 만들 때 Browse With 또는 F5 키를 사용 하 여 cshtml 파일을 보려고 하면 **'/' 응용 프로그램에서 상태-서버 오류가**발생 한다는 오류가 표시 됩니다. 서버에서 `http://localhost:XXXX/Views/../XXXX.cshtml`로 이동 하려고 합니다.

이 문제를 해결 하려면 프로젝트의 **시작 작업** 설정을 **특정 페이지로**변경 합니다. 페이지에 대 한 값을 제공할 필요는 없습니다.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

이렇게 변경한 후에는 F5 키를 선택 하 여 응용 프로그램의 루트 (`http://localhost:XXXX`)로 이동 합니다. 이 동작은 **현재 페이지** 설정이 열린 페이지를 시작 하는 VISUAL STUDIO 2013의 MVC 5 프로젝트 동작과 동일 하지 않습니다.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Url 재작성 및 물결표 (~)

ASP.NET Razor 3 또는 ASP.NET MVC 5로 업그레이드 한 후에는 URL 다시 쓰기를 사용 하는 경우 물결표 (~) 표기법이 더 이상 제대로 작동 하지 않을 수 있습니다. URL 재작성은 &lt;/&gt;, &lt;스크립트/&gt;&lt;링크/&gt;와 같은 HTML 요소의 물결표 (~) 표기법에 영향을 주므로 물결표는 더 이상 루트 디렉터리에 매핑되지 않습니다.

예를 들어 **asp.net/content** 에 대 한 요청을 **asp.net**에 다시 작성 하는 경우 href = "~/content/"/&gt; &lt;의 href 특성은 **/** 대신 **/content/content/** 로 확인 됩니다. 이러한 변경을 방지 하기 위해 각 웹 페이지나 global.asax의 **응용 프로그램\_BeginRequest** 에서 **IIS\_WasUrlRewritten** context를 false로 설정할 수 있습니다.

<a id="templateissue"></a>
### <a name="templates"></a>템플릿

Windows 8.1 또는 Windows Server 2012 r 2에서 Visual Studio 2012을 사용 하 여 ASP.NET MVC 프로젝트를 만들 때 Visual Studio에는 "ASP.NET 4.5에 대 한 웹 구성 [url]이 실패 했습니다." 라는 오류 메시지가 표시 됩니다.

![구성 오류](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Visual Studio 2012은 이러한 Windows 릴리스에 설치 될 때 ASP.NET 4.5 기능을 사용 하도록 설정 하지 않기 때문에이 오류가 표시 됩니다. ASP.NET 4.5를 사용 하도록 설정 하려면 [Windows 기능 사용/사용 안 함](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)에 설명 된 단계를 수행 합니다.

![Windows 기능 설정 또는 해제](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

또는 명령줄을 통해 ASP.NET 4.5을 사용 하도록 설정할 수 있습니다.

1. 관리자 모드에서 명령 프롬프트를 엽니다.
2. ASP.NET 4.5를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
