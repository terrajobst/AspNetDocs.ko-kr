---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619234"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [개요](#overview)
- [설치 참고 사항](#installation-notes)
- [소프트웨어 요구 사항](#software-requirements)
- [문서](#documentation)
- [지원](#support)
- [ASP.NET MVC 2 프로젝트를 ASP.NET MVC 3 Tools 업데이트로 업그레이드](#upgrading)
- [ASP.NET MVC 3 도구 업데이트 (4 월 12 일, 2011)](#tu-changes)

    - [이제 "컨트롤러 추가" 대화 상자에서 뷰 및 데이터 액세스 코드를 사용 하 여 컨트롤러를 스 캐 폴드 수 있습니다.](#tu-AddControllerDialog)
    - ["ASP.NET MVC 3 새 프로젝트" 대화 상자에 대 한 향상 된 기능](#tu-ImprovementsNewDialogBox)
    - [이제 프로젝트 템플릿에 Modernizr 1.7이 포함 됩니다.](#tu-Modernizr)
    - [프로젝트 템플릿에는 jQuery, jQuery UI 및 jQuery 유효성 검사의 업데이트 된 버전이 포함 되어 있습니다.](#tu-UpdatedJQuery)
    - [이제 프로젝트 템플릿에 ADO.NET Entity Framework 4.1이 미리 설치 된 NuGet 패키지로 포함 됩니다.](#tu-EF)
    - [프로젝트 템플릿에 JavaScript 라이브러리가 사전 설치 된 NuGet 패키지로 포함 되어 있습니다.](#tu-JavaScriptLibsNuget)
    - [알려진 문제](#tu-KI)
- [ASP.NET MVC 3 RTM (1 월 13 일 2011)](#MVC3RTM)

    - [변경: jQuery UI의 버전을 1.8.7로 업데이트 함](#RTM-1)
    - [변경: 기본 ModelMetadataProvider를 다시 DataAnnotationsModelMetadataProvider로 변경 했습니다.](#RTM-2)
    - [수정 됨: 공백을 포함 하는 Razor 식의 일부를 붙여넣은 결과가 반전 됩니다.](#RTM-3)
    - [수정 됨: 편집기에서 열린 Razor 파일의 이름을 바꾸면 구문 색 지정 및 IntelliSense가 비활성화 됩니다.](#RTM-4)
    - [알려진 문제](#RTM-KI)
    - [주요 변경 내용](#RTM-BC)
- [ASP.NET MVC 3 릴리스 후보 2 (12 월 10 일, 2010)](#_Toc2)

    - [JQuery 1.4.4, jQuery Validation 1.7 및 jQuery UI 1.8.6 y UI 1.8.6를 포함 하도록 프로젝트 템플릿이 변경 됨](#_Toc2_1)
    - ["AdditionalMetadataAttribute" 클래스를 추가 했습니다.](#_Toc2_2)
    - [향상 된 뷰 스 캐 폴딩](#_Toc2_3)
    - [Html Raw 메서드를 추가 했습니다.](#_Toc2_3)
    - ["Controller. ViewModel" 속성 및 "View" 속성이 "ViewBag"로 바뀜](#_Toc2_4)
    - ["ControllerSessionStateAttribute" 클래스가 "SessionStateAttribute"로 이름이 변경 되었습니다.](#_Toc2_5)
    - [RemoteAttribute "Fields" 속성의 이름을 "AdditionalFields"로 바꿨습니다.](#_Toc2_6)
    - ["SkipRequestValidationAttribute"에서 "AllowHtmlAttribute"로 이름이 변경 되었습니다.](#_Toc2_7)
    - [첫 번째 유용한 오류 메시지를 표시 하도록 "Html ValidationMessage" 메서드를 변경 했습니다.](#_Toc2_8)
    - [문서에 공백을 추가 하지 않도록 @model 선언을 수정 했습니다.](#_Toc2_9)
    - [엔진 특정 파일 이름을 지원 하기 위한 엔진을 보기 위해 "FileExtensions" 속성이 추가 됨](#_Toc2_10)
    - ["For" 특성의 올바른 값을 내보내도록 "LabelFor" 도우미를 수정 했습니다.](#_Toc2_11)
    - [모델 바인딩 중에 명시적 값에 우선 순위를 부여 하는 "RenderAction" 메서드를 수정 했습니다.](#_Toc2_12)
    - [주요 변경 내용](#_Toc2_BC)
    - [알려진 문제](#_Toc2_KI)
- [ASP.NET MVC 3 릴리스 후보 (11 월 9 일, 2010)](#TOC_ASP_NET_3_RC)

    - [ASP.NET MVC 3 RC의 새로운 기능](#_Toc276711785)
    - [NuGet 패키지 관리자](#_Toc276711786)
    - ["새 프로젝트" 대화 상자 개선](#_Toc276711787)
    - [Sessionless 컨트롤러](#_Toc276711788)
    - [새 유효성 검사 특성](#_Toc276711789)
    - ["LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드](#_Toc276711790)
    - [자식 작업 출력 캐싱](#_Toc276711791)
    - ["보기 추가" 대화 상자 개선 사항](#_Toc276711792)
    - [세부적인 요청 유효성 검사](#_Toc276711793)
    - [주요 변경 내용](#_Toc276711794)
    - [알려진 문제](#_Toc276711795)
- [ASP. MVC 3 베타 정보 (10 월 6 일, 2010)](#TOC_ASP_NET_3_Beta)

    - [ASP.NET MVC 3 Beta의 새로운 기능](#0.1__Toc274034215)
    - [NuPack 패키지 관리자](#0.1__Toc274034216)
    - [향상 된 새 프로젝트 대화 상자](#0.1__Toc274034217)
    - [Razor 뷰에서 강력한 형식의 모델을 지정 하는 간단한 방법](#0.1__Toc274034218)
    - [새 ASP.NET 웹 페이지 도우미 메서드 지원](#0.1__Toc274034219)
    - [추가 종속성 주입 지원](#0.1__Toc274034220)
    - [방해가 되지 않는 jQuery 기반 Ajax에 대 한 새로운 지원](#0.1__Toc274034221)
    - [비-jQuery 유효성 검사에 대 한 새로운 지원](#0.1__Toc274034222)
    - [클라이언트 유효성 검사 및 없는 JavaScript에 대 한 새로운 응용 프로그램 전체 플래그](#0.1__Toc274034223)
    - [뷰가 실행 되기 전에 실행 되는 코드에 대 한 새로운 지원](#0.1__Toc274034224)
    - [VBHTML Razor 구문에 대 한 새로운 지원](#0.1__Toc274034225)
    - [ValidateInputAttribute에 대 한 보다 세부적인 제어](#0.1__Toc274034226)
    - [도우미는 익명 개체를 사용 하 여 지정 된 HTML 특성 이름에 대해 밑줄로 하이픈을 변환 합니다.](#0.1__Toc274034227)
    - [버그 수정](#0.1__Toc274034228)
    - [주요 변경 내용](#0.1__Toc274034229)
    - [알려진 문제](#0.1__Toc274034230)
- [내용을](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>개요

이 문서에서는 Visual Studio 2010 용 ASP.NET MVC 3 RTM 릴리스에 대해 설명 합니다. ASP.NET MVC는 MVC (모델-뷰-컨트롤러) 패턴을 사용 하는 웹 응용 프로그램을 개발 하기 위한 프레임 워크입니다. ASP.NET MVC 3 설치 관리자에는 다음 구성 요소가 포함 되어 있습니다.

- ASP.NET MVC 3 런타임 구성 요소
- ASP.NET MVC 3 Visual Studio 2010 도구
- 런타임 구성 요소 ASP.NET 웹 페이지
- ASP.NET 웹 페이지 Visual Studio 2010 도구
- .NET 용 Microsoft 패키지 관리자 (NuGet)
- Razor 구문에 대 한 지원을 사용 하도록 설정 하는 Visual Studio 2010에 대 한 업데이트입니다. 자세한 내용은 기술 자료 문서 2483190를 참조 하십시오.

ASP.NET MVC 3의 시험판 버전 각각에 대한 릴리스 정보의 전체 집합은 다음 URL의 ASP.NET 웹 사이트에서 찾을 수 있습니다.

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>설치 참고 사항

웹 플랫폼 설치 관리자 (웹 PI)를 사용 하 여 ASP.NET MVC 3 RTM을 설치 하려면 다음 페이지를 방문 하세요.

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

또는 다음 페이지에서 Visual Studio 2010 용 ASP.NET MVC 3 RTM 설치 관리자를 다운로드할 수 있습니다.

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3을 설치 하 고 ASP.NET MVC 2와 나란히 실행할 수 있습니다.

<a id="software-requirements"></a>
## <a name="software-requirements"></a>소프트웨어 요구 사항

ASP.NET MVC 3 런타임 구성 요소에는 다음 소프트웨어가 필요 합니다.

- .NET Framework 버전 4입니다. 

    ASP.NET MVC 3 Visual Studio 2010 도구에는 다음 소프트웨어가 필요 합니다.
- Visual Studio 2010 또는 Visual Web Developer 2010 Express

<a id="documentation"></a>
## <a name="documentation"></a>Documentation

ASP.NET MVC에 대 한 설명서는 다음 URL의 MSDN 웹 사이트에서 제공 됩니다.

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

ASP.NET MVC에 대 한 자습서 및 기타 정보는 다음 URL에 있는 ASP.NET 웹 사이트의 MVC 페이지에서 사용할 수 있습니다.

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>지원

이 릴리스는 완전히 지원되는 릴리스입니다. 기술 지원을 받는 방법에 대 한 정보는 [Microsoft 지원 웹 사이트](https://support.microsoft.com/)에서 찾을 수 있습니다.

ASP.NET 커뮤니티 회원이 비공식적인 지원을 자주 제공할 수 있는 ASP.NET MVC 포럼에 이 릴리스에 관한 질문을 자유롭게 게시할 수도 있습니다.

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 2 프로젝트를 ASP.NET MVC 3 Tools 업데이트로 업그레이드

ASP.NET MVC 3은 동일한 컴퓨터에 ASP.NET MVC 2와 함께 설치할 수 있습니다. 그러면 ASP.NET MVC 2 응용 프로그램을 ASP.NET MVC 3으로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.

기존 ASP.NET MVC 2 응용 프로그램을 버전 3으로 수동으로 업그레이드 하려면 다음을 수행 합니다.

1. 컴퓨터에 빈 ASP.NET MVC 3 프로젝트를 새로 만듭니다. 이 프로젝트에는 업그레이드에 필요한 일부 파일이 포함됩니다.
2. 다음 파일을 ASP.NET MVC 3 프로젝트에서 ASP.NET MVC 2 프로젝트의 해당 위치로 복사합니다. jQuery 라이브러리에 대한 모든 참조를 새 파일 이름(jQuery-1.5.1.js)의 계정으로 업데이트해야 합니다. 

    - /Views/Web.config
    - /packages.config
    - /scripts/\*
    - /Content/themes/\*입니다.\*
3. 빈 ASP.NET MVC 3 프로젝트 솔루션의 루트에 있는 *패키지* 폴더를 솔루션의 루트에 복사 합니다 .이 폴더는 솔루션의 .sln 파일이 있는 디렉터리에 있습니다.
4. ASP.NET MVC 2 프로젝트에 영역이 포함 되어 있는 경우 각 영역의 *Views* 폴더에/Views/Web.config 파일을 복사 합니다.
5. ASP.NET MVC 2 프로젝트의 Web.config 파일에서 전역으로 ASP.NET MVC 버전을 검색 하 고 바꿉니다. 다음을 찾습니다. 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    다음으로 바꿉니다.

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. 솔루션 탐색기에서 버전 2의 DLL을 가리키는 *system.web* 에 대 한 참조를 삭제 한 다음, system.web (v 3.0.0.0) *에 대 한* 참조를 추가 합니다.
7. System.web 및 System.web .dll에 대 한 참조를 추가 합니다. 이러한 어셈블리는 다음 폴더에 있습니다. 

    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET MVC 3\Assemblies
    - %ProgramFiles%\ Microsoft ASP.NET\ASP.NET Web Pages\v1.0\Assemblies
8. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭한 다음 프로젝트 언로드를 선택합니다. 그런 다음 프로젝트 이름을 다시 마우스 오른쪽 단추로 클릭 하 고 *ProjectName*. .csproj 편집을 선택 합니다.
9. *Projecttypeguids* 요소를 찾아서 {F85E285D-A4E0-4152-9332-AB1D724D3325}을 {E53F8FEA-EAE0-44A6-8774-FFD645390401}로 바꿉니다.
10. 변경 사항을 저장하고 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 프로젝트 다시 로드를 선택합니다.
11. 응용 프로그램의 루트 web.config 파일에서 다음 설정을 *어셈블리* 섹션에 추가 합니다. 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. 프로젝트에서 ASP.NET MVC 2를 사용 하 여 컴파일된 타사 라이브러리를 참조 하는 경우에는 *구성* 섹션의 응용 프로그램 루트에 있는 web.config 파일에 다음 강조 표시 된 *bindingRedirect* 요소를 추가 합니다. 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>ASP.NET MVC 3 도구 업데이트의 변경 내용

이 섹션에서는 ASP.NET MVC 3 RTM 릴리스 이후 ASP.NET MVC 3 Tools 업데이트 릴리스에 적용 된 변경 내용에 대해 설명 합니다.

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>"컨트롤러 추가" 대화 상자에서 컨트롤러를 뷰 및 데이터 액세스 코드와 함께 스캐폴딩할 수 있습니다.

스캐폴딩은 컨트롤러와 응용 프로그램 뷰를 빠르게 생성하는 방법입니다. 코드를 생성 한 후에는 해당 코드를 편집 하 여 프로젝트의 요구 사항을 충족할 수 있습니다.

ASP.NET MVC 3의 *컨트롤러 추가* 대화 상자를 시작 하려면 *솔루션 탐색기*의 *컨트롤러* 폴더를 마우스 오른쪽 단추로 클릭 하 고 *추가*를 클릭 한 다음 *컨트롤러*를 클릭 합니다. 이 대화 상자는 추가적인 스캐폴딩 옵션을 제공하도록 향상되었습니다.

![](mvc3-release-notes/_static/image1.png)

기본적으로 사용할 수 있는 세 개의 스캐폴딩 템플릿이 있습니다.

#### <a name="empty-controller"></a>빈 컨트롤러

이 템플릿은 빈 컨트롤러 파일을 생성합니다. 이 템플릿은 이전 버전의 ASP.NET MVC에서 *create, edit, details 및 delete 시나리오에 대 한 동작 추가* 를 확인 하는 것과 동일 합니다. 이 템플릿을 선택하면 다른 추가 옵션은 사용할 수 없습니다.

#### <a name="controller-with-empty-readwrite-actions"></a>빈 읽기/쓰기 동작이 포함된 컨트롤러

이 템플릿은 필요한 모든 작업 메서드를 포함하되 메서드에 구현 코드가 없는 컨트롤러 파일을 생성합니다. 이 템플릿은 이전 버전의 ASP.NET MVC에서 *create, edit, details 및 delete 시나리오에 대 한 작업 추가* 를 확인 하는 것과 같습니다. 이 템플릿을 선택하면 다른 추가 옵션은 사용할 수 없습니다.

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>Entity Framework를 사용하며 읽기/쓰기 동작 및 보기가 포함된 컨트롤러

이 템플릿을 사용하면 작업 데이터 입력 사용자 인터페이스를 빠르게 생성할 수 있습니다. 이 템플릿은 다음과 같은 일반 요구 사항 및 시나리오 범위를 처리하는 코드를 생성합니다.

- *데이터 액세스*. 생성된 코드는 데이터베이스의 엔터티를 읽고 씁니다. 기존 데이터 컨텍스트 클래스를 선택 하거나 템플릿에서 새 *DbContext* 클래스를 생성 하도록 허용 하는 경우 Entity Framework Code First 접근 방식으로 작동 합니다. 또한 기존 *ObjectContext* 클래스를 선택 하는 경우 Entity Framework Database First 또는 Model First 접근 방식으로 작동 합니다.
- *유효성 검사*. 생성된 코드는 사용자의 모델 클래스에서 선언한 규칙에 따라 폼 전송의 유효성을 검사할 수 있도록 ASP.NET MVC 모델 바인딩 및 메타데이터 기능을 사용합니다. 여기에는 *필수* 및 *stringlength* 특성, 사용자 지정 유효성 검사 규칙 등의 기본 제공 유효성 검사 규칙이 포함 됩니다.
- *일 대 다 관계*입니다. 모델 클래스 간에 일대다 외래 키 관계를 정의하면 생성된 코드는 관련 엔터티를 선택하는 드롭다운 목록을 생성합니다. 예를 들어 다음 Entity Framework Code First 규칙에 따라 다음과 같은 모델 클래스를 정의할 수 있습니다. 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    그런 다음 *product* 클래스의 컨트롤러를 스 캐 폴드 하면 해당 뷰를 통해 사용자가 각 *제품* 인스턴스에 대 한 *범주* 개체를 선택할 수 있습니다.

    이 템플릿은 *컨트롤러 추가* 대화 상자에서 추가 옵션을 사용 하도록 설정 합니다. *모델 클래스*의 경우 사용자가 만들거나 편집할 수 있는 데이터 형식을 결정 하는 솔루션의 모든 모델 클래스를 선택할 수 있습니다.
- Entity Framework Code First를 사용하려는 경우 아무 모델 클래스나 선택할 수 있습니다.
- Entity Framework Database First 또는 Entity Framework Model First를 사용하는 경우 개념 모델에서 정의한 엔터티 클래스를 선택하십시오.

*데이터 컨텍스트 클래스*의 경우 다음과 같이 선택할 수 있습니다.

- Code First를 사용 하 고 기존 데이터 컨텍스트 클래스가 없는 경우 * * 새 데이터 컨텍스트 * *를 선택 합니다. 데이터 컨텍스트 클래스가 생성됩니다.
- Code First를 사용하려고 하는데 기존 데이터 컨텍스트 클래스가 있는 경우 여기에서 선택합니다. 선택한 모델 클래스를 유지하도록 업데이트됩니다.
- Database First 또는 Model First를 사용하는 경우 여기서 개체 컨텍스트 클래스를 선택합니다.

뷰의 경우 사용할 뷰 엔진을 선택하거나, 뷰를 스캐폴딩하고 싶지 않으면 없음을 선택합니다.

생성 된 뷰에 대 한 추가 옵션을 지정 하 여 고급 옵션을 선택할 수 있습니다. 예를 들어 사용할 레이아웃 또는 마스터 페이지를 선택할 수 있습니다.

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>"ASP.NET MVC 3 새 프로젝트" 대화 상자에서 향상된 기능

새 ASP.NET MVC 3 프로젝트를 만드는 데 사용 하는 대화 상자에는 아래에 나와 있는 것 처럼 여러 가지 향상 된 기능이 포함 되어 있습니다.

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>새 "인트라넷 프로젝트" 템플릿

프로젝트 템플릿 목록에는 새 인트라넷 응용 프로그램 템플릿이 포함되어 있습니다. 이 템플릿에는 폼 인증 대신 Windows 인증을 사용하여 웹 응용 프로그램을 개발하는 설정이 포함되어 있습니다. 인트라넷 응용 프로그램에는 프로젝트 템플릿에서 캡슐화 할 수 없는 일부 IIS 설정이 필요 하므로 템플릿에는 IIS에서 프로젝트 템플릿을 작동 시키는 방법에 대 한 지침이 포함 된 추가 정보 파일이 포함 되어 있습니다. 새 인트라넷 응용 프로그램 템플릿에 대 한 설명서는 다음 URL의 MSDN 웹 사이트에서 제공 됩니다.

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>이제 프로젝트 템플릿에서 HTML5를 사용할 수 있습니다.

이제 새 프로젝트 대화 상자에는 프로젝트 템플릿에 HTML5 특정 기능을 추가할 수 있는 옵션이 포함되어 있습니다. 옵션을 선택 하면 새 HTML5 `<header>`, `<footer>`및 `<navigation>` 요소가 포함 된 보기가 생성 됩니다.

이전 버전의 브라우저에서는 HTML5 특정 태그를 지원하지 않습니다. 이러한 제한 사항을 해결하기 위해 HTML5 프로젝트 템플릿에는 Modernizr 라이브러리에 대한 참조가 포함되어 있습니다. (다음 섹션을 참조하십시오.)

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>프로젝트 템플릿에는 Modernizr 1.7이 포함되어 있습니다.

Modernizr은 이러한 기능을 아직 지원 하지 않는 브라우저에서 CSS 3 및 HTML5를 지원할 수 있도록 하는 JavaScript 라이브러리입니다. 이 라이브러리는 ASP.NET MVC 3 프로젝트용 템플릿에서 미리 설치 된 NuGet 패키지로 포함 되어 있습니다. Modernizr에 대 한 자세한 내용은 [http://www.modernizr.com/](http://www.modernizr.com/)를 참조 하세요.

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>프로젝트 템플릿에는 jQuery, jQuery UI 및 jQuery 유효성 검사의 업데이트 버전이 포함됩니다.

프로젝트 템플릿에 jQuery 스크립트의 다음 버전이 포함되었습니다.

- jQuery 1.5.1
- jQuery 유효성 검사 1.8
- jQuery UI 1.8.11

이 라이브러리는 사전 설치된 NuGet 패키지로 포함되어 있습니다.

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>프로젝트 템플릿에 ADO.NET Entity Framework 4.1이 사전 설치된 NuGet 패키지로 포함되어 있습니다.

ADO.NET Entity Framework 4.1에는 Code First 기능이 포함 되어 있습니다. Code First는 기존 Database First 및 Model First 패턴에 대안을 제공하는 ADO.NET Entity Framework를 위한 새로운 개발 패턴입니다.

Code First는 Visual Basic 또는 C#로 작성된 POCO 클래스("일반 이전 CLR 개체")를 사용하여 사용자의 모델을 정의하는 데 중점을 두고 있습니다. 이러한 클래스는 기존 데이터베이스에 매핑되거나 데이터베이스 스키마를 생성하는데 사용될 수 있습니다. *Dataannotations* 특성을 사용 하거나 흐름 api를 사용 하 여 추가 구성을 제공할 수 있습니다.

ASP.NET MVC에서 코드 Firstwith에 대 한 설명서는 다음 Url의 ASP.NET 웹 사이트에서 사용할 수 있습니다.

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>프로젝트 템플릿에 JavaScript 라이브러리가 사전 설치된 NuGet 패키지로 포함됩니다.

새 ASP.NET MVC 3 프로젝트를 만들 때 프로젝트에는 프로젝트 템플릿의 Scripts 폴더에 스크립트를 직접 추가 하는 대신 NuGet을 사용 하 여 설치 하 여 이전에 언급 한 JavaScript 파일 (예: Modernizr 라이브러리)이 포함 됩니다. 컨텐트에. 이를 통해 새로운 스크립트 버전이 출시되면 NuGet을 사용하여 스크립트를 최신 버전으로 업데이트할 수 있습니다.

예를 들어 새 jQuery 릴리스 빈도가 제공된 경우 프로젝트 템플릿에 포함된 jQuery 버전은 어느 시점에서 만료됩니다. 그러나 jQuery가 설치된 NuGet 패키지에 포함되어 있기 때문에 사용자는 jQuery의 새 버전이 나왔을 때 NuGet 대화 상자로 알림을 받게 됩니다.

JQuery는 파일 이름에 버전 번호를 포함 하므로 jQuery를 최신 버전으로 업데이트 하려면 새 파일 이름을 사용 하기 위해 jQuery 파일을 참조 하는 `<script>` 태그도 업데이트 해야 합니다. 포함된 기타 스크립트 라이브러리는 스크립트 이름에 버전 번호를 포함하지 않으므로 최신 버전으로 더욱 쉽게 업데이트할 수 있습니다.

<a id="tu-KI"></a>
## <a name="known-issues"></a>알려진 문제점

- 경우에 따라 "설치 하지 못했습니다 (오류 코드 0x80070643)" 오류 메시지와 함께 설치에 실패할 수 있습니다. 이 문제를 해결 하는 방법에 대 한 자세한 내용은 [기술 자료 문서 2531566](https://support.microsoft.com/kb/2531566)를 참조 하십시오.
- 컨트롤러를 추가하기 위해 스캐폴딩하면 Entity Framework에서 지원되는 엔터티 상속을 활용하는 엔터티를 스캐폴딩하지 않습니다. 예를 들어 *학생* 클래스에서 상속 되는 기본 *Person* 클래스가 지정 된 경우 *학생* 클래스의 스 캐 폴딩은 컴파일되지 않는 코드를 생성 합니다.
- 솔루션 폴더 내에 새 ASP.NET MVC 3 프로젝트를 만들면 *NullReferenceException* 오류가 발생 합니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만든 다음 솔루션 폴더로 이동 하는 것입니다.
- ReSharper가 설치된 경우 IntelliSense for Razor 구문을 사용할 수 없습니다. ReSharper이 설치 되어 있고 ASP.NET MVC 3에서 Razor IntelliSense 지원을 활용 하려는 경우 지금 함께 사용 하는 방법을 설명 하는 [Razor intellisense 및 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) On Hadi 빌드의 블로그 항목을 참조 하세요.
- 설치하는 동안 EULA 동의 대화 상자에 사용 조건이 표시됩니다.
- Razor 뷰 (cshtml 또는 *)를 편집 하는 경우 vbhtml* 파일), 뷰입니다. ASP.NET MVC 3에는 Razor 보기에 대 한 코드 조각이 포함 되어 있지 않습니다. ASP.NET MVC에 대 한 코드 조각 선택은 다음에 대 한 코드 조각을 표시 합니다.
- Visual Studio가 설치 되어 있지 않은 컴퓨터에 visual Web Developer Express 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Studio를 설치 하는 경우 ASP.NET MVC 3을 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자에 의해 업그레이드 되는 구성 요소를 공유 합니다. Visual Web Developer Express가 없는 컴퓨터에 Visual Studio 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Web Developer Express를 설치 하는 경우에도 동일한 문제가 적용 됩니다.

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>ASP.NET MVC 3 RTM의 변경 내용

이 섹션에서는 RC2 릴리스 이후 ASP.NET MVC 3 RTM 릴리스에서 적용 되는 변경 내용 및 버그 수정을 설명 합니다.

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>변경: jQuery UI의 버전을 1.8.7로 업데이트 함

최신 버전의 jQuery UI 라이브러리를 포함 하도록 Visual Studio 용 ASP.NET MVC 프로젝트 템플릿이 업데이트 되었습니다. 템플릿에는 jQuery UI에 필요한 리소스 파일의 최소 집합 (예: 연결 된 CSS 및 이미지 파일)도 포함 됩니다.

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>변경: 기본 ModelMetadataProvider를 다시 DataAnnotationsModelMetadataProvider로 변경 했습니다.

ASP.NET MVC 3의 RC2 릴리스에는 기존 *DataAnnotationsModelMetadataProvider* 클래스 위에 캐싱을 제공 하 여 성능 향상을 제공 하는 *CachedDataAnnotationsMetadataProvider* 클래스가 도입 되었습니다. 그러나이 구현에서 일부 버그가 보고 되었으므로 변경 내용이 되돌려 [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack)에서 사용할 수 있는 MVC 퓨처 프로젝트로 이동 되었습니다.

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>수정 됨: 공백을 포함 하는 Razor 식의 일부를 붙여넣은 결과가 반전 됩니다.

ASP.NET MVC 3의 시험판 버전에서는 공백이 포함 된 Razor 식의 일부를 Razor 파일에 붙여넣으면 결과 식이 반전 됩니다. 예를 들어 다음 Razor 코드 블록을 살펴보십시오.

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

첫 번째 메서드에서 "first param" 텍스트를 선택 하 여 두 번째 메서드에 인수로 붙여넣으면 결과는 다음과 같습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

올바른 동작은 붙여넣기 작업으로 인해 다음과 같은 결과가 발생 한다는 것입니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

이 문제는 RTM 릴리스에서 수정 되어 붙여넣기 작업 중에 식이 올바르게 유지 됩니다.

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>수정 됨: 편집기에서 열린 Razor 파일의 이름을 바꾸면 구문 색 지정 및 IntelliSense가 비활성화 됩니다.

편집기 창에서 파일을 여는 동안 솔루션 탐색기를 사용 하 여 Razor 파일의 이름을 바꾸면 구문이 강조 표시 되 고 IntelliSense가 해당 파일에 대 한 작업을 중지 합니다. 이 문제는 이름 바꾸기 후 강조 표시와 IntelliSense를 유지 하기 위해 수정 되었습니다.

<a id="RTM-KI"></a>
## <a name="known-issues"></a>알려진 문제점

- NuGet 패키지 관리자 콘솔이 열려 있는 상태에서 Visual Studio 2010 SP1 Beta를 닫으면 Visual Studio가 작동을 중단 하 고 다시 시작을 시도 합니다. 이 문제는 Visual Studio 2010 s p 1의 RTM 릴리스에서 수정 될 예정입니다.
- ASP.NET MVC 3 설치 관리자는 초기 버전의 NuGet 패키지 관리자만 설치할 수 있습니다. 초기 버전을 설치한 후에는 Visual Studio 확장 관리자를 사용 하 여 NuGet을 설치 하 고 업데이트할 수 있습니다. NuGet이 이미 설치 되어 있는 경우 Visual Studio 확장 갤러리로 이동 하 여 최신 버전의 NuGet로 업데이트 합니다.
- 솔루션 폴더 내에 새 ASP.NET MVC 3 프로젝트를 만들면 *NullReferenceException* 오류가 발생 합니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만든 다음 솔루션 폴더로 이동 하는 것입니다.
- 설치 관리자가 ASP.NET MVC의 이전 버전 보다 훨씬 더 오래 걸릴 수 있습니다. 이는 Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.
- ReSharper가 설치된 경우 IntelliSense for Razor 구문을 사용할 수 없습니다. ReSharper이 설치 되어 있고 ASP.NET MVC 3에서 Razor IntelliSense 지원을 활용 하려는 경우 지금 함께 사용 하는 방법을 설명 하는 [Razor intellisense 및 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) On Hadi 빌드의 블로그 항목을 참조 하세요.
- ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CCSHTML 및 VBHTML 뷰는 빌드 작업을 올바르게 설정 하지 않으므로 프로젝트가 게시 될 때 이러한 뷰 유형이 생략 됩니다. 이러한 파일에 대 한 빌드 작업 값은 "Content"로 설정 해야 합니다. ASP.NET MVC 3 RTM은 새 파일에 대해이 문제를 해결 하지만 시험판 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일의 설정을 수정 하지는 않습니다.
- ![](mvc3-release-notes/_static/image3.png)
- 설치하는 동안 EULA 동의 대화 상자에 사용 조건이 표시됩니다.
- Razor 뷰 (cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러로 이동 메뉴 항목을 사용할 수 없으며 코드 조각이 없습니다.
- Visual Studio가 설치 되어 있지 않은 컴퓨터에 visual Web Developer Express 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Studio를 설치 하는 경우 ASP.NET MVC 3을 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자에 의해 업그레이드 되는 구성 요소를 공유 합니다. Visual Web Developer Express가 없는 컴퓨터에 Visual Studio 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Web Developer Express를 설치 하는 경우에도 동일한 문제가 적용 됩니다.

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>주요 변경 내용

- ASP.NET MVC의 이전 버전에서는 몇 가지 경우를 제외 하 고 작업 필터가 요청당 생성 됩니다. 이 동작은 보장 된 동작이 아니지만 단순히 구현 세부 정보 이며 필터에 대 한 계약은 상태 비저장을 고려해 야 합니다. ASP.NET MVC 3에서 필터는 더 적극적으로 캐시 됩니다. 따라서 인스턴스 상태를 부적절 하 게 저장 하는 모든 사용자 지정 작업 필터는 중단 될 수 있습니다.
- *순서* 값이 같은 예외 필터에 대 한 예외 필터 실행 순서가 변경 되었습니다. ASP.NET MVC 2 및 이전 버전에서 작업 메서드에 대 한 것과 동일한 *순서* 값을 가진 컨트롤러의 예외 필터는 작업 메서드의 예외 필터 보다 먼저 실행 됩니다. 이는 일반적으로 예외 필터가 지정 된 *순서* 값 없이 적용 되는 경우입니다. ASP.NET MVC 3에서 가장 구체적인 예외 핸들러가 가장 먼저 실행 되도록이 순서는 반대입니다. 이전 버전과 마찬가지로 *Order* 속성이 명시적으로 지정 된 경우 필터는 지정 된 순서로 실행 됩니다.
- *FileExtensions* 라는 새 속성이 *Virtualpathproviderviewengine* 기본 클래스에 추가 되었습니다. ASP.NET가 경로를 기준으로 뷰를 조회 하는 경우 (이름 아님)이 새 속성으로 지정 된 목록에 파일 확장명을 포함 하는 뷰만 고려 됩니다. 이는 웹 폼 보기에 사용자 지정 파일 확장명을 사용 하도록 설정 하 고 공급자가 이름이 아닌 전체 경로를 사용 하 여 해당 뷰를 참조 하는 응용 프로그램의 주요 변경 내용입니다. 해결 방법은 사용자 지정 파일 확장명을 포함 하도록 *FileExtensions* 속성의 값을 수정 하는 것입니다.
- *IControllerFactory* 인터페이스를 직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현은이 릴리스에서 인터페이스에 추가 된 새 *Getcontrollersessionbehavior* 메서드의 구현을 제공 해야 합니다. 일반적으로이 인터페이스를 직접 구현 하지 말고 *Defaultcontrollerfactory*에서 클래스를 파생 하는 것이 좋습니다.

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>ASP.NET MVC 3 RC2의 변경 내용

이 섹션에서는 RC 릴리스 이후 ASP.NET MVC 3 RC2 릴리스에 적용 된 변경 내용 (새로운 기능 및 버그 수정)에 대해 설명 합니다.

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>JQuery 1.4.4, jQuery Validation 1.7 및 jQuery UI 1.8.6를 포함 하도록 프로젝트 템플릿이 변경 됨

ASP.NET MVC 3에 대 한 프로젝트 템플릿에는 이제 jQuery, jQuery Validation 및 jQuery UI의 최신 버전이 포함 되어 있습니다. jQuery UI는 프로젝트 템플릿에 새로 추가 된 기능으로, 유용한 사용자 인터페이스 위젯을 제공 합니다. JQuery UI에 대 한 자세한 내용은 [http://jqueryui.com/](http://jqueryui.com/)홈 페이지를 참조 하세요.

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>"AdditionalMetadataAttribute" 클래스를 추가 했습니다.

*Additionalmetadataattribute* 클래스를 사용 하 여 모델 속성에 대 한 *Modelmetadata. additionalvalues* 사전을 채울 수 있습니다.

예를 들어 뷰 모델에 관리자 에게만 표시 되어야 하는 속성이 있다고 가정 합니다. 다음 예제와 같이 AdminOnly를 키로 사용 하 고 true를 값으로 사용 하 여 새 특성으로 해당 모델에 주석을 달 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

이 메타 데이터는 제품 뷰 모델을 렌더링할 때 모든 표시 또는 편집기 템플릿에서 사용할 수 있습니다. 응용 프로그램 개발자는 메타 데이터 정보를 해석할 수 있습니다.

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>향상 된 뷰 스 캐 폴딩

스 캐 폴딩 뷰에 사용 되는 T4 템플릿은 이제 *TextBoxFor*와 같은 도우미 대신 *editorfor* 같은 템플릿 도우미 메서드에 대 한 호출을 생성 합니다. 이렇게 변경 하면 뷰 추가 대화 상자에서 뷰를 생성할 때 데이터 주석 특성의 형태로 모델의 메타 데이터에 대 한 지원이 향상 됩니다.

추가 뷰 스 캐 폴딩에는 규칙에 따라 모델에 대 한 기본 키 정보의 향상 된 검색 및 사용도 포함 됩니다. 예를 들어 뷰 추가 대화 상자는이 정보를 사용 하 여 기본 키 값이 편집 가능한 양식 필드로 스 캐 폴드 되지 않도록 합니다.

기본 편집 및 만들기 템플릿은 클라이언트 유효성 검사에 필요한 jQuery 스크립트에 대 한 참조를 포함 합니다.

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>Html Raw 메서드를 추가 했습니다.

기본적으로 Razor 뷰 엔진은 모든 값을 HTML로 인코딩합니다. 예를 들어 다음 코드 조각은 페이지에 `<strong>Hello World!</strong>`표시 되도록 인사말 변수 내부에서 HTML을 인코딩합니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

새 *Html Raw* 메서드는 콘텐츠를 안전 하다 고 알려진 경우 인코딩되지 않은 Html을 표시 하는 간단한 방법을 제공 합니다. 다음 예제에서는 동일한 문자열을 표시 하지만 문자열이 태그로 렌더링 됩니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>"Controller. ViewModel" 속성 및 "View" 속성이 "ViewBag"로 바뀜

이전에는 *컨트롤러* 의 *ViewModel* 속성이 뷰의 *view* 속성에 속하는지를. 이러한 두 속성은 동적 속성 접근자 구문을 사용 하 여 *ViewDataDictionary* 개체의 값에 액세스 하는 방법을 제공 합니다. 혼동을 피하고 일관성을 유지 하기 위해 두 속성의 이름이 동일 하 게 변경 되었습니다.

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>"ControllerSessionStateAttribute" 클래스가 "SessionStateAttribute"로 이름이 변경 되었습니다.

*Controllersessionstateattribute* 클래스는 ASP.NET MVC 3의 RC 릴리스에서 도입 되었습니다. 속성이 더 간결 하 게 변경 되었습니다.

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>RemoteAttribute "Fields" 속성의 이름을 "AdditionalFields"로 바꿨습니다.

*Remoteattribute* 클래스의 *Fields* 속성으로 인해 사용자 간에 혼동이 발생 했습니다. 이 속성의 이름을 *Additionalfields* 로 바꾸면 의도를 명확 하 게 할 수 있습니다.

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>"SkipRequestValidationAttribute"에서 "AllowHtmlAttribute"로 이름이 변경 되었습니다.

*SkipRequestValidationAttribute* 특성의 이름을 *AllowHtmlAttribute* 로 변경 하 여 의도 된 용도를 더 잘 나타낼 수 있습니다.

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>첫 번째 유용한 오류 메시지를 표시 하도록 "Html ValidationMessage" 메서드를 변경 했습니다.

첫 번째 오류를 표시 하는 대신 첫 번째 유용한 오류 메시지를 표시 하도록 *Html ValidationMessage* 메서드를 수정 했습니다.

모델을 바인딩하는 동안 모델 자체 ( *IValidatableObject*를 구현 하는 경우), 속성에 적용 된 유효성 검사 특성, 속성에 액세스 하는 동안 throw 된 예외에서 비롯 하 여 속성에 대 한 오류 메시지가 포함 된 여러 소스에서 *modelstate* 사전을 채울 수 있습니다.

*Html. validationmessage* 메서드는 유효성 검사 메시지를 표시할 때 예외를 포함 하는 모델 상태 항목을 건너뜁니다. 이러한 항목은 일반적으로 최종 사용자에 게 적합 하지 않기 때문입니다. 대신 메서드는 예외와 연결 되지 않은 첫 번째 유효성 검사 메시지를 검색 하 고 해당 메시지를 표시 합니다. 이러한 메시지를 찾을 수 없는 경우 기본값은 첫 번째 예외와 연결 된 일반 오류 메시지입니다.

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>문서에 공백을 추가 하지 않도록 @model 선언을 수정 했습니다.

이전 릴리스에서는 뷰의 맨 위에 있는 `@model` 선언에서 렌더링 된 HTML 출력에 빈 줄을 추가 했습니다. 이는 선언에 공백이 발생 하지 않도록 수정 되었습니다.

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>엔진 특정 파일 이름을 지원 하기 위한 엔진을 보기 위해 "FileExtensions" 속성이 추가 됨

뷰 엔진은 다음 예제와 같이 명시적 뷰 경로를 사용 하 여 뷰를 반환할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

첫 번째 뷰 엔진은 항상 뷰를 렌더링 하려고 시도 합니다. 기본적으로 Web Forms 뷰 엔진은 첫 번째 뷰 엔진입니다. Web Forms 엔진이 Razor 뷰를 렌더링할 수 없기 때문에 오류가 발생 합니다. 이제 뷰 엔진에는 지원 되는 파일 확장명을 지정 하는 데 사용 되는 *FileExtensions* 속성이 있습니다. ASP.NET가 뷰 엔진이 파일을 렌더링할 수 있는지 여부를 결정 하는 경우이 속성을 확인 합니다. 이는 주요 변경 내용입니다. 자세한 내용은이 문서의 [주요 변경 내용](#_Toc2_BC) 섹션에 포함 되어 있습니다.

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>"For" 특성의 올바른 값을 내보내도록 "LabelFor" 도우미를 수정 했습니다.

메서드가 해당 ID 대신 *입력* 요소의 *이름* 특성과 일치 하는 특성 *에 대해* 을 *렌더링 한 경우* 버그가 수정 되었습니다. W3C에 따르면 *for* 특성은 *입력* 요소의 ID와 일치 해야 합니다.

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>모델 바인딩 중에 명시적 값에 우선 순위를 부여 하는 "RenderAction" 메서드를 수정 했습니다.

이전 버전에서는 *renderaction* 메서드에 전달 된 명시적 값이 자식 작업 내에서 모델 바인딩 중에 현재 폼 값을 무시 하 고 있습니다. 수정은 모델 바인딩 중에 명시적 값이 우선적으로 적용 되도록 합니다.

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>주요 변경 내용

- ASP.NET MVC의 이전 버전에서는 몇 가지 경우를 제외 하 고 요청 별로 작업 필터가 생성 되었습니다. 이 동작은 보장 된 동작이 아니지만 단순히 구현 세부 정보 이며 필터에 대 한 계약은 상태 비저장을 고려해 야 합니다. ASP.NET MVC 3에서 필터는 더 적극적으로 캐시 됩니다. 따라서 인스턴스 상태를 부적절 하 게 저장 하는 모든 사용자 지정 작업 필터는 중단 될 수 있습니다.
- *순서* 값이 같은 예외 필터에 대 한 예외 필터 실행 순서가 변경 되었습니다. ASP.NET MVC 2 및 이전 버전에서는 작업 메서드에 대 한 예외 필터 보다 먼저 작업 메서드의 *순서* 값이 동일한 컨트롤러의 예외 필터가 실행 되었습니다. 이는 일반적으로 예외 필터가 지정 된 *순서* 값 없이 적용 된 경우입니다. ASP.NET MVC 3에서 가장 구체적인 예외 핸들러가 가장 먼저 실행 되도록이 순서는 반대입니다. 이전 버전과 마찬가지로 *Order* 속성이 명시적으로 지정 된 경우 필터는 지정 된 순서로 실행 됩니다.
- *FileExtensions* 라는 새 속성이 *Virtualpathproviderviewengine* 기본 클래스에 추가 되었습니다. ASP.NET가 경로를 기준으로 뷰를 조회 하는 경우 (이름 아님)이 새 속성으로 지정 된 목록에 파일 확장명을 포함 하는 뷰만 고려 됩니다. 이는 웹 폼 보기에 사용자 지정 파일 확장명을 사용 하도록 설정 하 고 공급자가 이름이 아닌 전체 경로를 사용 하 여 해당 뷰를 참조 하는 응용 프로그램의 주요 변경 내용입니다. 해결 방법은 사용자 지정 파일 확장명을 포함 하도록 *FileExtensions* 속성의 값을 수정 하는 것입니다.
- *IControllerFactory* 인터페이스를 직접 구현 하는 사용자 지정 컨트롤러 팩터리 구현은이 릴리스에서 인터페이스에 추가 된 새 *Getcontrollersessionbehavior* 메서드의 구현을 제공 해야 합니다. 일반적으로이 인터페이스를 직접 구현 하지 말고 *Defaultcontrollerfactory*에서 클래스를 파생 하는 것이 좋습니다.

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>알려진 문제점

- ASP.NET MVC 3 설치 관리자는 초기 버전의 NuGet 패키지 관리자만 설치할 수 있습니다. 초기 버전을 설치한 후에는 Visual Studio 확장 관리자를 사용 하 여 NuGet을 설치 하 고 업데이트할 수 있습니다. NuGet이 이미 설치 되어 있는 경우 Visual Studio 확장 갤러리로 이동 하 여 최신 버전의 NuGet로 업데이트 합니다.
- 솔루션 폴더 내에 새 ASP.NET MVC 3 프로젝트를 만들면 *NullReferenceException* 오류가 발생 합니다. 해결 방법은 솔루션의 루트에 ASP.NET MVC 3 프로젝트를 만든 다음 솔루션 폴더로 이동 하는 것입니다.
- 설치 관리자가 ASP.NET MVC의 이전 버전 보다 훨씬 더 오래 걸릴 수 있습니다. 이는 Visual Studio 2010의 구성 요소를 업데이트 하기 때문입니다.
- ReSharper가 설치된 경우 IntelliSense for Razor 구문을 사용할 수 없습니다. ReSharper가 설치 되어 있고 ASP.NET MVC 3 r c 2에서 Razor IntelliSense 지원을 활용 하려는 경우 지금 함께 사용 하는 방법을 설명 하는 [Razor intellisense 및 ReSharper](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) On Hadi 빌드의 블로그 항목을 참조 하세요.
- ASP.NET MVC 3의 베타 버전을 사용 하 여 만든 CSHTML 및 VBHTML 뷰는 빌드 작업을 올바르게 설정 하지 않으므로 프로젝트가 게시 될 때 이러한 뷰 형식이 생략 됩니다. 이러한 파일에 대 한 *빌드 작업* 값은 내용 "으로 설정 해야 합니다. ASP.NET MVC 3 r c 2는 새 파일에 대해이 문제를 해결 하지만 베타 버전을 사용 하 여 만든 프로젝트에 대 한 기존 파일의 설정을 수정 하지는 않습니다.![](mvc3-release-notes/_static/image4.png)
- 설치하는 동안 EULA 동의 대화 상자에 사용 조건이 표시됩니다.
- Razor 뷰 (cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러로 이동 메뉴 항목을 사용할 수 없으며 코드 조각이 없습니다.
- Visual Studio가 설치 되어 있지 않은 컴퓨터에 visual Web Developer Express 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Studio를 설치 하는 경우 ASP.NET MVC 3을 다시 설치 해야 합니다. Visual Studio 및 Visual Web Developer Express는 ASP.NET MVC 3 설치 관리자에 의해 업그레이드 되는 구성 요소를 공유 합니다. Visual Web Developer Express가 없는 컴퓨터에 Visual Studio 용 ASP.NET MVC 3을 설치한 후 나중에 Visual Web Developer Express를 설치 하는 경우에도 동일한 문제가 적용 됩니다.
- ASP.NET MVC 3 RC 2를 설치 하면 NuGet이 아직 설치 되지 않은 경우 업데이트 되지 않습니다. NuGet을 업그레이드 하려면 Visual Studio 확장 관리자로 이동 하 고 사용 가능한 업데이트로 표시 되어야 합니다. NuGet을 최신 릴리스로 업그레이드할 수 있습니다.

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 릴리스 후보

ASP.NET MVC 릴리스 후보는 2010 년 11 월 9 일에 출시 되었습니다.

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>ASP.NET MVC 3 RC의 새로운 기능

이 섹션에서는 Beta 릴리스 이후 ASP.NET MVC 3 RC 릴리스에 도입 된 기능을 설명 합니다.

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>NuGet 패키지 관리자

ASP.NET MVC 3에는 라이브러리 및 도구를 Visual Studio 프로젝트에 추가 하기 위한 통합 패키지 관리 도구인 NuGet 패키지 관리자 (이전의 NuPack)가 포함 되어 있습니다. 이 도구는 개발자가 소스 트리로 라이브러리를 가져오기 위해 오늘 수행 하는 단계를 자동화 합니다.

Visual studio의 상황에 맞는 메뉴에서 및 PowerShell cmdlet 집합을 사용 하 여 NuGet을 명령줄 도구로 사용 하 고 Visual Studio 2010 내에서 통합 콘솔 창으로 작업할 수 있습니다.

NuGet에 대 한 자세한 내용은 [Nuget 설명서](https://docs.microsoft.com/nuget/)를 참조 하세요.

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>"새 프로젝트" 대화 상자 개선

새 프로젝트를 만들 때 이제 새 프로젝트 대화 상자를 사용 하 여 ASP.NET MVC 프로젝트 형식 뿐만 아니라 뷰 엔진을 지정할 수 있습니다.

![](mvc3-release-notes/_static/image5.png)

이 릴리스에는 대화 상자에 나열 된 템플릿 및 뷰 엔진의 목록 수정에 대 한 지원이 포함 되어 있습니다.

기본 템플릿은 다음과 같습니다.

비어 있음 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조, 기본 ASP.NET MVC 스타일을 포함 하는 사이트 .css 파일 및 기본 JavaScript 파일이 포함 된 Scripts 디렉터리를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 최소 파일 집합을 포함 합니다.

인터넷 응용 프로그램. ASP.NET MVC와 함께 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.

대화 상자에 표시 되는 프로젝트 템플릿 목록은 Windows 레지스트리에 지정 되어 있습니다.

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>Sessionless 컨트롤러

새 *Controllersessionstateattribute* 를 사용 하면 [SessionState](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) 를 지정 하 여 컨트롤러에 대 한 세션 상태 동작을 보다 세부적으로 제어할 수 있습니다.

다음 예에서는 컨트롤러에 대 한 모든 요청에 대 한 세션 상태를 해제 하는 방법을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

다음 예제에서는 컨트롤러에 대 한 모든 요청에 대해 읽기 전용 세션 상태를 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>새 유효성 검사 특성

#### <a name="compareattribute"></a>CompareAttribute

새 *compareattribute* 유효성 검사 특성을 사용 하 여 두 가지 모델 속성의 값을 비교할 수 있습니다. 다음 예에서는 *comparepassword* 속성이 유효 하려면 *암호* 필드와 일치 해야 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

새 *Remoteattribute* 유효성 검사 특성은 jQuery 유효성 검사 플러그 인의 원격 유효성 검사기를 활용 하 여 클라이언트 쪽 유효성 검사가 실제 유효성 검사 논리를 수행 하는 서버에서 메서드를 호출할 수 있도록 합니다.

다음 예제에서 *UserName* 속성에는 *remoteattribute* 가 적용 됩니다. 편집 뷰에서이 속성을 편집 하는 경우 클라이언트 유효성 검사는이 필드의 유효성을 검사 하기 위해 users *컨트롤러* 클래스에서 *UserNameAvailable* 이라는 동작을 호출 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

다음 예에서는 해당 하는 컨트롤러를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

기본적으로 특성이 적용 되는 속성 이름은 작업 메서드에 쿼리 문자열 매개 변수로 전달 됩니다.

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>"LabelFor" 및 "LabelForModel" 메서드에 대 한 새 오버 로드

레이블 텍스트를 지정할 수 있는 및 *Labelformodel* *메서드에 대해 새* 오버 로드가 추가 되었습니다. 다음 예제에서는 이러한 오버 로드를 사용 하는 방법을 보여 줍니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>자식 작업 출력 캐싱

*Outputcacheattribute* 는 *html renderaction* 또는 *html. action* 도우미 메서드를 사용 하 여 호출 되는 자식 작업의 출력 캐싱을 지원 합니다. 다음 예에서는 다른 작업을 호출 하는 뷰를 보여 줍니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

*GetDate* 작업은 *outputcacheattribute*로 주석이 추가 됩니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

이 코드가 실행 될 때 Html. Action ("GetDate")에 대 한 호출의 결과는 100 초 동안 캐시 됩니다.

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>"보기 추가" 대화 상자 개선 사항

강력한 형식의 뷰를 추가 하는 경우 뷰 추가 대화 상자는 이제 많은 핵심 .NET Framework 유형과 같은 이전 버전 보다 더 이상 적용 되지 않는 형식을 필터링 합니다. 또한 이제 목록이 정규화 된 형식 이름이 아니라 클래스 이름으로 정렬 되어 형식을 더 쉽게 찾을 수 있습니다. 예를 들어 다음 예제와 같이 형식 이름이 표시 됩니다.

ClassName (네임 스페이스)

이전 릴리스에서는 다음과 같이 표시 됩니다.

Namespace. ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>세부적인 요청 유효성 검사

*Validateinputattribute* 의 *Exclude* 속성이 더 이상 존재 하지 않습니다. 대신 모델 바인딩 중에 모델의 특정 속성에 대 한 요청 유효성 검사를 건너뛰도록 하려면 새 *SkipRequestValidationAttribute*를 사용 합니다.

예를 들어, 작업 메서드가 블로그 게시물을 편집 하는 데 사용 된다고 가정 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

다음 예제에서는 블로그 게시물에 대 한 뷰 모델을 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

사용자가 Description 속성에 대 한 일부 태그를 제출 하는 경우 요청 유효성 검사로 인해 모델 바인딩이 실패 합니다. 블로그 게시물 설명에 대 한 모델 바인딩 중에 요청 유효성 검사를 사용 하지 않도록 설정 하려면 다음 예제와 같이 속성에 *SkipRequpestValidationAttribute* 을 적용 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

또는 모델의 모든 속성에 대해 요청 유효성 검사를 해제 하려면 값이 *false* 인 *validateinputattribute* 를 동작 메서드에 적용 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>주요 변경 내용

- *순서* 값이 같은 예외 필터에 대 한 예외 필터 실행 순서가 변경 되었습니다. ASP.NET MVC 2 및 이전 버전에서 작업 메서드의 순서와 동일한 *순서* 를 가진 컨트롤러의 예외 필터는 작업 메서드의 예외 필터 보다 먼저 실행 되었습니다. 이는 일반적으로 예외 필터가 지정 된 *순서* 값 없이 적용 된 경우입니다. ASP.NET MVC 3에서 가장 구체적인 예외 핸들러가 가장 먼저 실행 되도록이 순서는 반대입니다. 이전 버전과 마찬가지로 *Order* 속성이 명시적으로 지정 된 경우 필터는 지정 된 순서로 실행 됩니다.
- *Virtualpathproviderviewengine* 기본 클래스에 *FileExtensions* 라는 새 속성을 추가 했습니다. 경로를 기준으로 뷰를 조회 하는 경우 (이름으로는 아님)이 새 속성으로 지정 된 목록에 파일 확장명을 포함 하는 뷰만 고려 됩니다. 이는 사용자 지정 빌드 공급자를 등록 하 여 웹 폼 보기에 사용자 지정 파일 확장명을 사용 하도록 설정 하 고 이름이 아니라 전체 경로를 사용 하 여 해당 뷰를 참조 하는 사용자에 대 한 주요 변경 내용입니다. 해결 방법은 사용자 지정 파일 확장명을 포함 하도록 *FileExtensions* 속성의 값을 수정 하는 것입니다.

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>알려진 문제점

- 설치 관리자는 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 ASP.NET MVC의 이전 버전 보다 훨씬 더 오래 걸릴 수 있습니다.
- 강력한 형식의 뷰 스 캐 폴드 쓰기 전용 속성을 선택 하는 경우 뷰 추가 스 캐 폴딩입니다. 이는 항상 스 캐 폴딩에서 무시 해야 합니다. 뷰 추가 대화 상자는 또한 "편집" 또는 "만들기" 뷰를 생성할 때 읽기 전용 속성을 스 캐 폴드 합니다. 읽기 전용 속성은 표시 및 목록 뷰에만 스 캐 폴드 합니다.
- ASP.NET MVC 3이 비동기 CTP와 함께 설치 된 경우 디버깅이 작동 하지 않습니다. ASP.NET MVC 3은 비동기 CTP와 나란히 설치할 수 없습니다. 디버깅을 복구 하려면 비동기 CTP를 제거 합니다. 자세한 내용은 ASP.NET MVC 3 RC의 모든 부분을 제거 하는 방법에 대 한 [블로그 게시물](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) 을 참조 하세요.
- Resharper가 설치 되어 있으면 Razor Intellisense가 작동 하지 않습니다. ReSharper가 설치 되어 있고 ASP.NET MVC 3 RC에서 Razor intellisense 지원을 활용 하려는 경우 지금 함께 사용 하는 방법을 설명 하는 JetBrains의 [이 블로그 게시물](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) 을 참조 하세요.
- ASP.NET MVC 3의 Beta를 사용 하 여 만든 CSHTML 및 VBHTML 뷰에는 게시에서이를 생략 하는 빌드 작업이 올바르게 수행 되지 않습니다. 이러한 파일에 대 한 *빌드 작업* 을 "콘텐츠"로 설정 해야 합니다. ASP.NET MVC 3 RC는 새 파일에 대해이 문제를 해결 하지만 베타를 사용 하 여 만든 프로젝트에 대 한 기존 파일의 설정을 수정 하지는 않습니다.
- 설치 관리자는 Visual Studio 2010의 구성 요소를 업데이트 하기 때문에 ASP.NET MVC의 이전 버전 보다 훨씬 더 오래 걸릴 수 있습니다.
- "Edit" 강력한 형식의 뷰 스 캐 폴드 읽기 전용 속성을 선택 하는 경우 뷰 추가 스 캐 폴딩입니다. 마찬가지로 쓰기 전용 속성은 "표시" 스 캐 폴드 됩니다.
- 설치하는 동안 EULA 동의 대화 상자에 사용 조건이 표시됩니다.
- Visual Studio Async CTP를 설치 하면 ASP.NET MVC 3 도구 설치의 일부로 포함 된 Razor 릴리스와 충돌 합니다. Visual Studio Async CTP와 Razor 릴리스를 모두 동일한 컴퓨터에 설치 하지 않아야 합니다.
- Razor 뷰 (cshtml 파일)를 편집 하는 경우 Visual Studio에서 컨트롤러로 이동 메뉴 항목을 사용할 수 없으며 코드 조각이 없습니다.

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 베타

ASP.NET MVC 3 Beta는 2010 년 10 월 6 일에 출시 되었습니다. 다음은 베타 릴리스와 관련 된 정보 이며 위의 ASP.NET MVC 3 릴리스 후보 섹션에서 참조 하는 모든 업데이트 또는 변경 내용이 적용 됩니다.

## <a id="0.1__Toc274034215"></a>New Featuresin ASP.NET MVC 3 Beta

<a id="0.1__Default_validation_system"></a>이 섹션에서는 ASP.NET MVC 3 베타 릴리스에 도입 된 기능을 설명 합니다.

### <a id="0.1__Toc274034216"></a>NuGet 패키지 관리자

ASP.NET MVC 3에는 라이브러리 및 도구를 Visual Studio 프로젝트에 추가 하기 위한 통합 패키지 관리 도구인 NuGet 패키지 관리자가 포함 되어 있습니다. 대부분의 경우 개발자가 소스 트리로 라이브러리를 가져오기 위해 오늘 수행 하는 단계를 자동화 합니다.

Visual studio의 상황에 맞는 메뉴 및 PowerShell cmdlet 집합을 사용 하 여 NuGet을 명령줄 도구로 사용 하 고 Visual Studio 2010 내에서 통합 콘솔 창으로 작업할 수 있습니다.

NuGet에 대 한 자세한 내용은 [Nuget 설명서](https://docs.microsoft.com/nuget/)를 참조 하세요.

### <a id="0.1__Toc274034217"></a>향상 된 새 프로젝트 대화 상자

새 프로젝트를 만들 때 이제 새 프로젝트 대화 상자를 사용 하 여 ASP.NET MVC 프로젝트 형식 뿐만 아니라 뷰 엔진을 지정할 수 있습니다.

![](mvc3-release-notes/_static/image6.png)

이 릴리스에는 대화 상자에 나열 된 템플릿 및 뷰 엔진의 목록을 수정 하는 기능이 포함 되어 있지 않습니다.

기본 템플릿은 다음과 같습니다.

비어 있음 ASP.NET MVC 프로젝트에 대 한 기본 디렉터리 구조, 기본 ASP.NET MVC 스타일을 포함 하는 작은 사이트 .css 파일, 기본 JavaScript 파일이 포함 된 Scripts 디렉터리를 포함 하 여 ASP.NET MVC 프로젝트에 대 한 최소 파일 집합을 포함 합니다.

인터넷 응용 프로그램. ASP.NET MVC 내에서 멤버 자격 공급자를 사용 하는 방법을 보여 주는 샘플 기능을 포함 합니다.

### <a id="0.1__Toc274034218"></a>Razor 뷰에서 강력한 형식의 모델을 지정 하는 간단한 방법

강력한 형식의 Razor 뷰에 대해 모델 유형을 지정 하는 방법은 새 @model 지시어를 사용 하 여 간소화 된 Razor 뷰를 사용 하 고, 그렇지 않은 경우에는 @ModelType 지시문을 사용 합니다. 이전 버전의 ASP.NET MVC에서는 다음과 같은 방법으로 Razor 뷰에 대해 강력한 형식의 모델을 지정 합니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

이 릴리스에서는 다음 구문을 사용할 수 있습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>새 ASP.NET 웹 페이지 도우미 메서드 지원

새 ASP.NET 웹 페이지 기술에는 자주 사용 되는 기능을 뷰와 컨트롤러에 추가 하는 데 유용한 도우미 메서드 집합이 포함 되어 있습니다. ASP.NET MVC 3은 컨트롤러 및 뷰 (해당 하는 경우) 내에서 이러한 도우미 메서드를 사용할 수 있도록 지원 합니다. 이러한 메서드는 System.web. 도우미 어셈블리에 포함 됩니다. 다음 표에서는 ASP.NET 웹 페이지 도우미 메서드 중 몇 가지를 보여 줍니다.

| **도움말** | **설명** |
| --- | --- |
| 차트 | 뷰 내에서 차트를 렌더링 합니다. Chart. ToWebImage, Chart. Save 및 Chart. Write와 같은 메서드를 포함 합니다. |
| 암호화 | 는 해싱 알고리즘을 사용 하 여 적절 한 솔트된 및 해시 된 암호를 만듭니다. |
| WebGrid | 개체의 컬렉션 (일반적으로 데이터베이스의 데이터)을 표로 렌더링 합니다. 페이징 및 정렬을 지원 합니다. |
| WebImage | 이미지를 렌더링 합니다. |
| 웹 메일 | 이메일 메시지를 보냅니다. |

도우미 및 기본 구문을 나열 하는 빠른 참조 항목은 다음 URL에서 ASP.NET Razor 구문 설명서의 일부로 제공 됩니다.

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>추가 종속성 주입 지원

ASP.NET MVC 3 Preview 1 릴리스를 기반으로 하는 현재 릴리스에는 두 개의 새로운 서비스와 4 개의 기존 서비스에 대 한 추가 지원과 종속성 확인 및 Common Service Locator에 대 한 지원이 향상 되었습니다.

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>세분화 된 컨트롤러 인스턴스화에 대 한 새 IControllerActivator 인터페이스

새 IControllerActivator 인터페이스는 종속성 주입을 통해 컨트롤러를 인스턴스화하는 방법에 대 한 보다 세분화 된 제어를 제공 합니다. 다음 예제에서는 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

이를 컨트롤러 팩터리의 역할과 대조 합니다. 컨트롤러 팩터리는 컨트롤러 유형을 찾고 해당 컨트롤러 유형의 인스턴스를 인스턴스화하는 역할을 하는 IControllerFactory 인터페이스의 구현입니다.

컨트롤러 활성기는 컨트롤러 형식의 인스턴스를 인스턴스화하는 역할만 담당 합니다. 컨트롤러 유형 조회를 수행 하지 않습니다. 적절 한 컨트롤러 유형을 찾은 후 컨트롤러 팩터리는 IControllerActivator의 인스턴스에 위임 하 여 컨트롤러의 실제 인스턴스화를 처리 해야 합니다.

DefaultControllerFactory 클래스에는 IControllerFactory 인스턴스를 허용 하는 새 생성자가 있습니다. 이렇게 하면 기본 컨트롤러 유형 조회 동작을 재정의 하지 않고도 컨트롤러 만들기의 이러한 측면을 관리 하는 종속성 주입을 적용할 수 있습니다.

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>IServiceLocator 인터페이스가 되며 idependencyresolver로 대체 되었습니다.

커뮤니티 피드백에 따라 ASP.NET MVC 3 Beta 릴리스는 IServiceLocator 인터페이스 사용을 ASP.NET MVC의 요구 사항과 관련 된 슬림 되며 idependencyresolver 인터페이스로 대체 했습니다. 다음 예에서는 새 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

이 변경의 일부로 ServiceLocator 클래스도 DependencyResolver 클래스로 대체 되었습니다. 종속성 확인자를 등록 하는 것은 이전 버전의 ASP.NET MVC와 비슷합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

이 인터페이스의 구현은 요청 된 형식에 대해 등록 된 서비스를 제공 하기 위해 단순히 기본 종속성 주입 컨테이너에 위임 해야 합니다.

요청 된 형식의 등록 된 서비스가 없는 경우 ASP.NET MVC는 GetService에서 null을 반환 하 고 GetServices에서 빈 컬렉션을 반환 하기 위해이 인터페이스의 구현이 필요 합니다.

새 DependencyResolver 클래스를 사용 하면 새 되며 idependencyresolver 인터페이스 또는 IServiceLocator (Common Service Locator) 인터페이스를 구현 하는 클래스를 등록할 수 있습니다. 일반 서비스 로케이터에 대 한 자세한 내용은 [GitHub의 CommonServiceLocator](https://github.com/unitycontainer/commonservicelocator)를 참조 하세요.

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>세분화 된 뷰 페이지 인스턴스화에 대 한 새 IViewActivator 인터페이스

새 IViewPageActivator 인터페이스는 종속성 주입을 통해 뷰 페이지를 인스턴스화하는 방법을 보다 세밀 하 게 제어할 수 있습니다. 이는 WebFormView 인스턴스와 RazorView 인스턴스 모두에 적용 됩니다. 다음 예에서는 새 인터페이스를 보여 줍니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

이러한 클래스는 이제 IViewPageActivator 생성자 인수를 수락 합니다 .이 인수를 사용 하면 ViewPage, ViewUserControl 및 WebViewPage 형식이 인스턴스화되는 방식을 제어 하는 종속성 주입을 사용할 수 있습니다.

#### <a name="new-dependency-resolver-support-for-existing-services"></a>기존 서비스에 대 한 새 종속성 해결 프로그램 지원

새 릴리스에는 다음 서비스에 대 한 종속성 확인 지원이 포함 됩니다.

- 모델 유효성 검사 공급자 ModelValidatorProvider를 구현 하는 클래스는 종속성 확인자에 등록할 수 있으며 시스템은 클라이언트 및 서버 쪽 유효성 검사를 지원 하기 위해이 클래스를 사용 합니다.
- 모델 메타 데이터 공급자입니다. ModelMetadataProvider를 구현 하는 단일 클래스를 종속성 확인자에 등록 하 고 시스템에서 템플릿 및 유효성 검사 시스템에 대 한 메타 데이터를 제공 하는 데 사용할 수 있습니다.
- 값 공급자. ValueProviderFactory를 구현 하는 클래스는 종속성 확인자에 등록할 수 있으며 시스템은이를 사용 하 여 컨트롤러 및 모델 바인딩 중에 사용 되는 값 공급자를 만듭니다.
- 모델 바인더입니다. IModelBinderProvider를 구현 하는 클래스를 종속성 확인자에 등록 하 고 시스템에서이를 사용 하 여 모델 바인딩 시스템에서 사용 하는 모델 바인더를 만들 수 있습니다.

### <a id="0.1__Toc274034221"></a>방해가 되지 않는 jQuery 기반 Ajax에 대 한 새로운 지원

ASP.NET MVC는 다음과 같은 Ajax 도우미 메서드를 포함 합니다.

- Ajax. a.
- RouteLink
- Html.beginform
- BeginRouteForm

이러한 메서드는 JavaScript를 사용 하 여 전체 포스트백을 사용 하는 대신 서버에서 작업 메서드를 호출 합니다. 이 기능은 사용 하지 않는 방식으로 jQuery를 활용 하도록 업데이트 되었습니다. 인라인 클라이언트 스크립트를 intrusively 내보내는 대신 이러한 도우미 메서드는 *데이터 ajax* 접두사를 사용 하 여 HTML5 특성을 내보내 태그의 동작을 분리 합니다. 그런 다음 적절 한 JavaScript 파일을 참조 하 여 동작을 태그에 적용 합니다. 다음 JavaScript 파일이 참조 되는지 확인 합니다.

- jquery-1.10.2.min.js 1.4.1
- jquery.

이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿의 Web.config 파일에서 기본적으로 사용 하도록 설정 되어 있지만 기존 프로젝트에 대해서는 기본적으로 사용 되지 않습니다. 자세한 내용은이 문서의 뒷부분에 나오는 [클라이언트 유효성 검사 및 없는 JavaScript에 대 한 응용 프로그램 전체 플래그 추가](#0.1_AddedApplicationWideFlagsForClientValida) 를 참조 하세요.

### <a id="0.1__Toc274034222"></a>비-jQuery 유효성 검사에 대 한 새로운 지원

기본적으로 ASP.NET MVC 3 Beta는 클라이언트 쪽 유효성 검사를 수행 하기 위해 잘못 된 방식으로 jQuery 유효성 검사를 사용 합니다. 유사 하지 않은 클라이언트 유효성 검사를 사용 하려면 보기 내에서 다음과 같은 호출을 수행 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

이렇게 하려면 ViewContext UnobtrusiveJavaScriptEnabled 속성이 true로 설정 되어 있어야 합니다 .이 작업은 다음 호출을 수행 하 여 수행할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

또한 다음 JavaScript 파일이 참조 되는지 확인 합니다.

- jquery-1.10.2.min.js 1.4.1
- jquery. js를 확인 합니다.
- jquery. 유효성을 검사 합니다.

이 기능은 ASP.NET MVC 3 새 프로젝트 템플릿의 Web.config 파일에서 기본적으로 사용 하도록 설정 되어 있지만 기존 프로젝트에 대해서는 기본적으로 사용 되지 않습니다. 자세한 내용은이 문서의 뒷부분에 나오는 [클라이언트 유효성 검사 및 없는 JavaScript에 대 한 새로운 응용 프로그램 전체 플래그](#0.1_AddedApplicationWideFlagsForClientValida) 를 참조 하세요.

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>클라이언트 유효성 검사 및 없는 JavaScript에 대 한 새로운 응용 프로그램 전체 플래그

다음 예제와 같이 HtmlHelper 클래스의 정적 멤버를 사용 하 여 클라이언트 유효성 검사 및 비 표시 JavaScript를 전역적으로 사용 하거나 사용 하지 않도록 설정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

기본 프로젝트 템플릿을 사용 하면 기본적으로 JavaScript를 사용 하지 않아도 됩니다. 다음 설정을 사용 하 여 응용 프로그램의 루트 web.config 파일에서 이러한 기능을 사용 하거나 사용 하지 않도록 설정할 수도 있습니다.

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

기본적으로 이러한 기능을 사용 하도록 설정할 수 있기 때문에 다음 예제와 같이 기본 설정을 재정의할 수 있도록 하는 새 오버 로드가 HtmlHelper 클래스에 도입 되었습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

이전 버전과의 호환성을 위해 두 기능 모두 기본적으로 사용 하지 않도록 설정 되어 있습니다.

### <a id="0.1__Toc274034224"></a>뷰가 실행 되기 전에 실행 되는 코드에 대 한 새로운 지원

이제 Views 디렉터리에 \_viewstart. cshtml (또는 \_viewstart. vbhtml) 이라는 파일을 배치 하 고 해당 디렉터리와 하위 디렉터리의 여러 뷰 간에 공유 될 코드를 추가할 수 있습니다. 예를 들어 ~/Views 폴더의 \_viewstart. cshtml 페이지에 다음 코드를 넣을 수 있습니다.

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

이렇게 하면 Views 폴더와 모든 하위 폴더에 있는 모든 보기에 대 한 레이아웃 페이지가 재귀적으로 설정 됩니다. 뷰가 렌더링 되는 동안 \_viewstart. cshtml 파일의 코드는 뷰 코드가 실행 되기 전에 실행 됩니다. \_viewstart. cshtml 코드는 해당 폴더의 모든 뷰에 적용 됩니다.

기본적으로 \_viewstart. cshtml 파일의 코드는 모든 하위 폴더의 보기에도 적용 됩니다. 그러나 개별 하위 폴더에는 자체 버전의 \_viewstart. cshtml 파일을 사용할 수 있습니다. 이 경우 로컬 버전이 우선적으로 적용 됩니다. 예를 들어 HomeController에 대 한 모든 뷰에 공통적으로 적용 되는 코드를 실행 하려면 ~/Views/Home 폴더에 \_viewstart. cshtml 파일을 배치 합니다.

### <a id="0.1__Toc274034225"></a>VBHTML Razor 구문에 대 한 새로운 지원

이전 ASP.NET MVC 미리 보기에는 Razor 구문 기반으로 하는 보기 C#에 대 한 지원이 포함 되어 있습니다. 이러한 뷰는. cshtml 파일 확장명을 사용 합니다. Razor를 지원 하기 위해 진행 중인 작업의 일환으로 ASP.NET MVC 3 Beta는 파일 확장명을 사용 하는 Visual Basic에서 Razor 구문에 대 한 지원을 도입 했습니다.

VBHTML 페이지에서 Visual Basic 구문을 사용 하는 방법에 대 한 소개는 다음 URL의 자습서를 참조 하세요.

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>ValidateInputAttribute에 대 한 보다 세부적인 제어

ASP.NET MVC는 항상 ValidateInputAttribute 클래스를 포함 하 고 있습니다 .이 클래스는 핵심 ASP.NET 요청 유효성 검사 인프라를 호출 하 여 들어오는 요청에 악성 입력이 포함 되지 않도록 합니다. 기본적으로 입력 유효성 검사를 사용 합니다. 다음 예제와 같이 ValidateInputAttribute 특성을 사용 하 여 요청 유효성 검사를 사용 하지 않도록 설정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

그러나 대부분의 웹 응용 프로그램은 HTML을 허용 해야 하는 개별 양식 필드를 포함 하지만 나머지 필드는 그렇지 않습니다. 이제 ValidateInputAttribute 클래스를 사용 하 여 요청 유효성 검사에 포함 되지 않아야 하는 필드 목록을 지정할 수 있습니다.

예를 들어 블로그 엔진을 개발 하는 경우 본문 및 요약 필드에서 태그를 허용 하는 것이 좋습니다. 이러한 필드는 각각 속성 이름 ("Body" 및 "Summary")에 해당 하는 name 특성을 가진 두 개의 input 요소로 표시 될 수 있습니다. 이러한 필드에 대해서만 요청 유효성 검사를 사용 하지 않도록 설정 하려면 다음 예제와 같이 ValidateInput 클래스의 Exclude 속성에 이름을 쉼표로 구분 하 여 지정 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>도우미는 익명 개체를 사용 하 여 지정 된 HTML 특성 이름에 대해 밑줄로 하이픈을 변환 합니다.

도우미 메서드를 사용 하면 다음 예제와 같이 익명 개체를 사용 하 여 특성 이름/값 쌍을 지정할 수 있습니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

ASP.NET의 속성 이름에는 하이픈을 사용할 수 없기 때문에이 방법을 사용 하면 특성 이름에 하이픈을 사용할 수 없습니다. 그러나 사용자 지정 HTML5 특성에는 하이픈이 중요 합니다. 예를 들어 HTML5는 "data-" 접두사를 사용 합니다.

이와 동시에 HTML의 특성 이름에는 밑줄을 사용할 수 없지만 속성 이름 내에서는 사용할 수 있습니다. 따라서 익명 개체를 사용 하 여 특성을 지정 하 고 특성 이름에 밑줄이 포함 된 경우 도우미 메서드는 밑줄을 하이픈으로 변환 합니다. 예를 들어 다음 도우미 구문은 밑줄을 사용 합니다.

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

이전 예제에서는 도우미가 실행 될 때 다음 태그를 렌더링 합니다.

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>버그 수정

이제 EditorFor 및 DisplayFor 템플릿 도우미의 기본 개체 템플릿은 Displayfor. Order 속성에 지정 된 순서를 지원 합니다. 이전 버전에서는 주문 설정이 사용 되지 않았습니다.

이제 클라이언트 유효성 검사에서 유효성 검사 특성이 적용 된 재정의 된 속성의 유효성 검사를 지원 합니다.

JsonValueProviderFactory는 이제 기본적으로 등록 됩니다.

## <a id="0.1__Toc274034229"></a>주요 변경 내용

순서 값이 같은 예외 필터에 대 한 예외 필터 실행 순서가 변경 되었습니다. ASP.NET MVC 2 및 이전 버전에서는 작업 메서드의 예외 필터 보다 먼저 작업 메서드의 순서와 동일한 순서를 사용 하 여 컨트롤러에서 예외 필터를 실행 했습니다. 이는 일반적으로 예외 필터가 지정 된 순서 값 없이 적용 된 경우입니다. ASP.NET MVC 3에서 가장 구체적인 예외 핸들러가 가장 먼저 실행 되도록이 순서는 반대입니다. 이전 버전과 마찬가지로 Order 속성이 명시적으로 지정 된 경우 필터는 지정 된 순서로 실행 됩니다.

## <a id="0.1__Toc274034230"></a>알려진 문제

설치하는 동안 EULA 동의 대화 상자에 사용 조건이 표시됩니다.

Razor 뷰에는 IntelliSense 지원 또는 구문 강조 표시가 없습니다. Visual Studio의 Razor 구문에 대 한 지원이 이후 릴리스의 일부로 포함 될 것으로 예상 됩니다.

Razor 보기 (CSHTML 파일) <a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a> 를 편집 하는 경우 Visual Studio에서 컨트롤러로 이동 메뉴 항목을 사용할 수 없으며 코드 조각이 없습니다.

@model 구문을 사용 하 여 강력한 형식의 CSHTML 뷰를 지정 하는 경우 형식에 대 한 언어별 바로 가기가 인식 되지 않습니다. 예를 들어 @model int는 작동 하지 않지만 @model Int32가 작동 합니다. 이 버그에 대 한 해결 방법은 모델 형식을 지정할 때 실제 형식 이름을 사용 하는 것입니다.

@model 구문을 사용 하 여 강력한 형식의 CSHTML 뷰 (또는 강력한 형식의 VBHTML 뷰를 지정 하는 @ModelType)를 지정 하는 경우 nullable 형식 및 배열 선언이 지원 되지 않습니다. 예를 들어 @model int? 은 지원 되지 않습니다. 대신 `@model Nullable<Int32>`를 사용 합니다. 문자열 [] @model 구문도 지원 되지 않습니다. 대신 `@model IList<string>`를 사용 합니다.

ASP.NET MVC 2 프로젝트를 ASP.NET MVC 3으로 업그레이드 하는 경우 web.config 파일의 appSettings 섹션에 다음을 추가 해야 합니다.

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

Web.config에서 사용 되는 폼 인증 설정을 무시 하 고 폼 인증에서 항상 인증 되지 않은 사용자를 ~/Account/Login으로 리디렉션하는 알려진 문제가 있습니다. 해결 방법은 다음 앱 설정을 추가 하는 것입니다.

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>내용을

© 2011 Microsoft Corporation. 모든 권리 보유. 이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 비롯한 본 문서의 정보 및 언급된 내용은 예고 없이 변경될 수 있습니다. 본 문서 사용에 따른 위험은 사용자가 감수해야 합니다.

이 문서는 귀하에게 Microsoft 제품의 어떠한 지적 재산에 대한 법적 권리도 부여하지 않습니다. 귀하는 참조를 위해 내부적으로 이 문서를 복사하고 사용할 수 있습니다.
