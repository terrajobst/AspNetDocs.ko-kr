---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 주요 변경 내용 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ...를 사용 하 여 만든 응용 프로그램에 잠재적으로 영향을 줄 수 있는 .NET Framework 버전 4 릴리스에 대 한 변경 내용을 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439511"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 주요 변경 내용

> 이 문서에서는 ASP.NET 4 Beta 1 및 Beta 2 릴리스를 비롯 하 여 이전 릴리스를 사용 하 여 만든 응용 프로그램에 잠재적으로 영향을 줄 수 있는 .NET Framework 버전 4 릴리스에 대 한 변경 내용을 설명 합니다.
> 
> [이 백서 다운로드](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>콘텐츠

[Web.config 파일의 ControlRenderingCompatibilityVersion 설정](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode 변경 내용](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode 및 UrlEncode는 이제 작은따옴표를 인코딩합니다.](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET 페이지 (.aspx) 파서가 더 엄격 합니다.](#0.1__Toc256770144 "_Toc256770144")  
[브라우저 정의 파일 업데이트 됨](#0.1__Toc256770145 "_Toc256770145")  
[루트 웹 구성 파일에서 Web.config를 제거 했습니다.](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 요청 유효성 검사](#0.1__Toc256770147 "_Toc256770147")  
[기본 해싱 알고리즘이 이제 HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[New ASP.NET 4 루트 구성과 관련 된 구성 오류](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 2.0 또는 ASP.NET 3.5 응용 프로그램에서 ASP.NET 4 자식 응용 프로그램이 시작 되지 않음](#0.1__Toc256770150 "_Toc256770150")  
[SharePoint가 설치 된 컴퓨터에서 ASP.NET 4 웹 사이트를 시작 하지 못함](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest 속성은 더 이상 PathInfo 값을 포함 하지 않습니다.](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 응용 프로그램은 eurl을 참조 하는 HttpException 오류를 생성할 수 있습니다.](#0.1__Toc256770153 "_Toc256770153")  
[IIS 7 또는 IIS 7.5 통합 모드의 기본 문서에서는 이벤트 처리기가 발생 하지 않을 수 있습니다.](#0.1__Toc256770154 "_Toc256770154")  
[ASP.NET CAS (코드 액세스 보안) 구현에 대 한 변경 내용](#0.1__Toc256770155 "_Toc256770155")  
[MembershipUser 네임 스페이스의 기타 형식이 이동 되었습니다.](#0.1__Toc256770156 "_Toc256770156")  
[HTTP 헤더 \* 변경 내용이 변경 되는 출력 캐싱](#0.1__Toc256770157 "_Toc256770157")  
[Passport의 system.web. 보안 형식은 사용 되지 않습니다.](#0.1__Toc256770158 "_Toc256770158")  
[PopOutImageUrl 속성은 ASP.NET 4에서 이미지를 렌더링 하지 못합니다.](#0.1__Toc256770159 "_Toc256770159")  
[StaticPopOutImageUrl 및 DynamicPopOutImageUrl는 경로에 백슬래시가 포함 될 때 이미지를 렌더링 하지 못합니다.](#0.1__Toc256770160 "_Toc256770160")  
[내용을](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config 파일의 ControlRenderingCompatibilityVersion 설정

ASP.NET 컨트롤은 태그 렌더링 방법을 보다 정확 하 게 지정할 수 있도록 .NET Framework 버전 4에서 수정 되었습니다. 이전 버전의 .NET Framework에서 일부 컨트롤은 사용 하지 않도록 설정 된 태그를 내보냈습니다. 기본적으로 ASP.NET 4이 형식의 태그는 더 이상 생성 되지 않습니다.

Visual Studio 2010을 사용 하 여 응용 프로그램을 ASP.NET 2.0 또는 ASP.NET 3.5에서 업그레이드 하는 경우이 도구는 레거시 렌더링을 유지 하는 설정을 `Web.config` 파일에 자동으로 추가 합니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 애플리케이션 풀을 변경하여 애플리케이션을 업그레이드하는 경우 ASP.NET은 기본적으로 새 렌더링 모드를 사용합니다. 새 렌더링 모드를 사용 하지 않도록 설정 하려면 `Web.config` 파일에 다음 설정을 추가 합니다.

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

새 동작에서 제공 하는 주요 렌더링 변경 내용은 다음과 같습니다.

- **Image** 및 **ImageButton** 컨트롤은 더 이상 `border="0"` 특성을 렌더링 하지 않습니다.
- 이 클래스에서 파생 된 **BaseValidator** 클래스 및 유효성 검사 컨트롤은 더 이상 기본적으로 빨간색 텍스트를 렌더링 하지 않습니다.
- **HtmlForm** 컨트롤은 **name** 특성을 렌더링 하지 않습니다.
- **테이블** 컨트롤은 더 이상 `border="0"` 특성을 렌더링 하지 않습니다.
- 사용자 입력 용으로 설계 되지 않은 컨트롤 (예: **레이블** 컨트롤)은 **사용** 속성이 **false** 로 설정 된 경우 (또는 컨테이너 컨트롤에서이 설정을 상속 하는 경우) 더 이상 `disabled="disabled"` 특성을 렌더링 하지 않습니다.

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode 변경 내용

ASP.NET 4의 **Clientidmode** 설정을 사용 하면 ASP.NET가 HTML 요소에 대 한 **id** 특성을 생성 하는 방법을 지정할 수 있습니다. 이전 버전의 ASP.NET에서 기본 동작은 **Clientidmode**의 **autoid** 설정에 해당 합니다. 그러나 이제 기본 설정을 **예측할**수 있습니다.

Visual Studio 2010을 사용 하 여 응용 프로그램을 ASP.NET 2.0 또는 ASP.NET 3.5에서 업그레이드 하는 경우이 도구는 이전 버전의 .NET Framework 동작을 유지 하는 설정을 `Web.config` 파일에 자동으로 추가 합니다. 그러나 .NET Framework 4를 대상으로 하도록 IIS에서 애플리케이션 풀을 변경하여 애플리케이션을 업그레이드하는 경우 ASP.NET은 기본적으로 새 모드를 사용합니다. 새 클라이언트 ID 모드를 사용 하지 않도록 설정 하려면 `Web.config` 파일에 다음 설정을 추가 합니다.

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode 및 UrlEncode는 이제 작은따옴표를 인코딩합니다.

ASP.NET 4에서는 **Httputility** 및 **HttpServerUtility** 클래스의 **HtmlEncode** 및 **UrlEncode** 메서드가 다음과 같이 작은따옴표 문자 (')를 인코딩하기 위해 업데이트 되었습니다.

- **HtmlEncode** 메서드는 작은따옴표의 인스턴스를 '로 인코딩합니다.
- **UrlEncode** 메서드는 작은따옴표의 인스턴스를 %27로 인코딩합니다.

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET 페이지 (.aspx) 파서가 더 엄격 합니다.

ASP.NET 페이지 (`.aspx` 파일) 및 사용자 정의 컨트롤 (`.ascx` 파일)에 대 한 페이지 파서는 ASP.NET 4에서 더 엄격 하며, 잘못 된 태그의 추가 인스턴스를 거부 합니다. 예를 들어 다음 두 코드 조각은 ASP.NET의 이전 릴리스에서 성공적으로 구문 분석 하지만 이제는 ASP.NET 4에서 파서 오류가 발생 합니다.

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

**HiddenField** 태그의 끝에 잘못 된 세미콜론이 있습니다.

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

**CssClass** 특성에 실행 되는 닫히지 않은 **스타일** 특성을 확인 합니다.

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>브라우저 정의 파일 업데이트 됨

브라우저 정의 파일은 새롭고 업데이트된 브라우저 및 디바이스에 대한 정보를 포함하도록 업데이트되었습니다. Netscape Navigator와 같은 오래된 브라우저와 디바이스는 제거되었으며 Google Chrome 및 Apple iPhone과 같은 최신 브라우저와 디바이스가 추가되었습니다.

애플리케이션에 제거된 브라우저 정의 중 하나를 상속하는 사용자 지정 브라우저 정의가 포함되어 있으면 오류가 표시됩니다. 예를 들어 `App_Browsers` 폴더에 IE2 브라우저 정의에서 상속 되는 브라우저 정의가 포함 된 경우 다음과 같은 구성 오류 메시지가 표시 됩니다.

- ID가 ' IE2 ' 인 browser 또는 게이트웨이 요소를 찾을 수 없습니다.

> [!NOTE]
> 페이지의 **요청. browser** 속성에 의해 노출 되는 **httpbrowsercapabilities** 개체는 브라우저 정의 파일에 의해 결정 됩니다. 따라서 ASP.NET 4에서이 개체의 속성에 액세스 하 여 반환 되는 정보는 이전 버전의 ASP.NET에서 반환 된 정보와 다를 수 있습니다.

다음 폴더에서 브라우저 정의 파일을 복사 하 여 이전 브라우저 정의 파일을 되돌릴 수 있습니다.

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

ASP.NET 4의 해당 `\CONFIG\Browsers` 폴더에 파일을 복사 합니다. 파일을 복사한 후에는 Aspnet\_의 브라우저 명령줄 도구를 실행 합니다.

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>루트 웹 구성 파일에서 Web.config를 제거 했습니다.

이전 버전의 ASP.NET에서는 어셈블리에 대 한 참조가의 **어셈블리** 섹션에 있는 루트 `Web.config` 파일에 포함 되었습니다. 성능을 향상 시키기 위해이 어셈블리에 대 한 참조가 제거 되었습니다.

ASP.NET 4에는 System.web .dll 어셈블리가 포함 되어 있지만 사용 되지 않습니다. System.string 어셈블리의 형식을 사용 하려면이 어셈블리에 대 한 참조를 루트 `Web.config` 파일이 나 응용 프로그램 `Web.config` 파일에 추가 합니다. 예를 들어, (사용 되지 않음) ASP.NET 모바일 컨트롤 중 하나를 사용 하려는 경우에는 `Web.config` 파일에 System.web 어셈블리에 대 한 참조를 추가 해야 합니다.

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 요청 유효성 검사

ASP.NET의 요청 유효성 검사 기능은 XSS (사이트 간 스크립팅) 공격에 대해 특정 수준의 기본 보호를 제공 합니다. 이전 버전의 ASP.NET에서는 요청 유효성 검사가 기본적으로 사용 하도록 설정 되었습니다. 그러나 ASP.NET 페이지 (`.aspx` 파일 및 해당 클래스 파일)에만 적용 되 고 해당 페이지가 실행 중일 때만 적용 됩니다.

ASP.NET 4에서 요청 유효성 검사는 기본적으로 HTTP 요청의 **BeginRequest** 단계 전에 활성화 되기 때문에 모든 요청에 대해 사용 하도록 설정 됩니다. 따라서 요청 유효성 검사는 .aspx 페이지 요청 뿐 아니라 모든 ASP.NET 리소스에 대 한 요청에 적용 됩니다. 여기에는 웹 서비스 호출 및 사용자 지정 HTTP 처리기와 같은 요청이 포함 됩니다. 사용자 지정 HTTP 모듈이 HTTP 요청의 콘텐츠를 읽는 경우에도 요청 유효성 검사가 활성화 됩니다.

결과적으로 이전에 오류를 트리거하지 않은 요청에 대 한 요청 유효성 검사 오류가 발생할 수 있습니다. ASP.NET 2.0 요청 유효성 검사 기능의 동작으로 되돌리려면 `Web.config` 파일에 다음 설정을 추가 합니다.

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

그러나 기존 처리기, 모듈 또는 기타 사용자 지정 코드가 XSS 공격 벡터가 될 수 있는 안전 하지 않은 HTTP 입력에 액세스 하는지 여부를 확인 하려면 요청 유효성 검사 오류를 분석 하는 것이 좋습니다.

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>기본 해싱 알고리즘이 이제 HMACSHA256

ASP.NET은 암호화 및 해시 알고리즘을 모두 사용하여 양식 인증 쿠키 및 보기 상태와 같은 데이터를 보호합니다. 기본적으로 ASP.NET 4는 이제 쿠키 및 뷰 상태에 대 한 해시 작업에 HMACSHA256 알고리즘을 사용 합니다. 이전 버전의 ASP.NET에서는 이전 HMACSHA1 알고리즘을 사용 했습니다.

Forms 인증 쿠키와 같은 데이터가 across.NET Framework 버전에서 작동 해야 하는 혼합 ASP.NET 2.0/o s p. n e t 4 환경을 실행 하는 경우 응용 프로그램에 영향을 줄 수 있습니다. 이전 HMACSHA1 알고리즘을 사용 하도록 ASP.NET 4 웹 응용 프로그램을 구성 하려면 `Web.config` 파일에 다음 설정을 추가 합니다.

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>New ASP.NET 4 루트 구성과 관련 된 구성 오류

.NET Framework 4 (그리고 따라서 ASP.NET 4)에 대 한 루트 구성 파일 (`machine.config` 파일 및 루트 `Web.config` 파일)은 응용 프로그램 `Web.config` 파일에 ASP.NET 3.5에서 발견 된 대부분의 상용구 구성 정보를 포함 하도록 업데이트 되었습니다. 관리 되는 IIS 7 및 IIS 7.5 구성 시스템의 복잡성 때문에 ASP.NET 4에서 ASP.NET 3.5 응용 프로그램을 실행 하 고 IIS 7 및 IIS 7.5를 실행 하면 ASP.NET 또는 IIS 구성 오류가 발생할 수 있습니다.

ASP.NET 3.5 응용 프로그램을 Visual Studio 2010의 프로젝트 업그레이드 도구를 사용 하 여 ASP.NET 4로 업그레이드 하는 것이 좋습니다 (실용적 인 경우). Visual Studio 2010는 ASP.NET 3.5 응용 프로그램의 `Web.config` 파일을 자동으로 수정 하 여 ASP.NET 4에 대 한 적절 한 설정을 포함 합니다.

그러나 다시 컴파일하지 않고 .NET Framework 4를 사용 하 여 ASP.NET 3.5 응용 프로그램을 실행 하는 것은 지원 되는 시나리오입니다. 이 경우 .NET Framework 4 및 IIS 7 또는 IIS 7.5에서 응용 프로그램을 실행 하기 전에 응용 프로그램의 `Web.config` 파일을 수동으로 수정 해야 할 수 있습니다.

다음 두 섹션에서는 다른 소프트웨어 조합에 대해 수행 해야 하는 변경 사항을 설명 합니다.

**Windows Vista SP1 또는 Windows Server 2008 SP1 (핫픽스 KB958854 또는 s p 2가 설치 되어 있지 않음)** 이 구성에서 IIS 7 구성 시스템은 응용 프로그램 수준 `Web.config` 파일을 ASP.NET 2.0 `machine.config` 파일과 비교 하 여 응용 프로그램의 관리 되는 구성을 잘못 병합 합니다. 따라서 3.5 이상 버전의 응용 프로그램 수준 `Web.config` .NET Framework 파일에는 IIS 7 유효성 검사에 실패 하지 않도록 하려면 **system.web. extensions** 구성 섹션 정의 (요소)가 있어야 합니다.

그러나 Visual Studio 2008에 도입 된 원래 상용구 구성 섹션 정의와 정확 하 게 일치 하지 않는 응용 프로그램 수준 `Web.config` 파일 항목을 수동으로 수정 하면 ASP.NET 구성 오류가 발생 합니다. Visual Studio 2008에 의해 생성 된 기본 구성 항목은 제대로 작동 합니다. 일반적인 문제는 `Web.config` 파일을 수동으로 수정 하 여 다양 한 구성 섹션 정의에 있는 **allowDefinition** 및 **requirepermission** 구성 특성을 생략 하는 것입니다. 이로 인해 응용 프로그램 수준 `Web.config` 파일의 간략 한 구성 섹션과 ASP.NET 4 `machine.config` 파일의 전체 정의가 일치 하지 않습니다. 따라서 런타임에 ASP.NET 4 구성 시스템은 구성 오류를 throw 합니다.

**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2 및 핫픽스 KB958854 설치 된 windows Vista SP1 및 Windows Server 2008 SP1.**

이 시나리오에서 IIS 7 및 IIS 7.5 네이티브 구성 시스템은 관리 되는 구성 섹션 처리기에 대해 정의 된 **형식** 특성에서 텍스트 비교를 수행 하므로 구성 오류를 반환 합니다. Visual Studio 2008 및 Visual Studio 2008 s p 1에서 생성 되는 모든 `Web.config` 파일에는 시스템의 형식 문자열에 "3.5"가 포함 되어 있기 때문 **입니다.** ASP.NET 4 `machine.config` 파일에는 동일한 구성 섹션 처리기에 대 한 **type** 특성에 "4.0"가 있으므로, Visual Studio 2008 또는 visual studio 2008 s p 1에서 생성 되는 응용 프로그램은 항상 iis 7 및 iis 7.5에서 구성 유효성 검사에 실패 합니다.

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>이러한 문제 해결

첫 번째 시나리오에 대 한 해결 방법은 Visual Studio 2008에 의해 자동으로 생성 된 `Web.config` 파일의 상용구 구성 텍스트를 포함 하 여 응용 프로그램 수준 `Web.config` 파일을 업데이트 하는 것입니다.

첫 번째 시나리오에 대 한 대체 해결 방법은 컴퓨터에 Vista 또는 Windows Server 2008 서비스 팩 2를 설치 하거나 핫픽스 KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854))를 설치 하 여 IIS 구성 시스템의 잘못 된 구성-병합 동작을 수정 하는 것입니다. 그러나 이러한 작업 중 하나를 수행한 후에는 두 번째 시나리오에 대해 설명 된 문제로 인해 응용 프로그램에 구성 오류가 발생할 수 있습니다.

두 번째 시나리오에 대 한 해결 방법은 응용 프로그램 수준 `Web.config` 파일에서 모든 **system.web** 구성 섹션 정의 및 구성 섹션 그룹 정의를 삭제 하거나 주석 처리 하는 것입니다. 이러한 정의는 일반적으로 응용 프로그램 수준 `Web.config` 파일의 맨 위에 있으며 **Configsections** 요소 및 해당 자식으로 식별할 수 있습니다.

두 시나리오 모두 필요 하지는 않지만 **codedom** 섹션을 수동으로 삭제 하는 것이 좋습니다.

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 2.0 또는 ASP.NET 3.5 응용 프로그램에서 ASP.NET 4 자식 응용 프로그램이 시작 되지 않음

이전 버전의 ASP.NET을 실행하는 애플리케이션의 자식으로서 구성된 ASP.NET 4 애플리케이션은 구성 또는 컴파일 오류로 인해 시작하지 못할 수 있습니다. 다음 예에서는 영향을 받는 응용 프로그램에 대 한 디렉터리 구조를 보여 줍니다.

`/parentwebapp` (ASP.NET 2.0 또는 ASP.NET 3.5를 사용 하도록 구성 됨)  
`/childwebapp` (ASP.NET 4를 사용 하도록 구성 됨)

`childwebapp` 폴더의 응용 프로그램은 IIS 7 또는 IIS 7.5에서 시작 되지 않으며 구성 오류를 보고 합니다. 오류 텍스트에는 다음과 비슷한 메시지가 포함 됩니다.

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

IIS 6에서는 `childwebapp` 폴더의 응용 프로그램도 시작 되지 않지만 다른 오류를 보고 합니다. 예를 들어 오류 텍스트에 다음을 사용할 수 있습니다.

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

이러한 시나리오는 `parentwebapp` 폴더에 있는 부모 응용 프로그램의 구성 정보가 `childwebapp` 폴더의 자식 웹 응용 프로그램에서 사용 되는 최종 병합 구성 설정을 결정 하는 구성 정보 계층 구조의 일부 이기 때문에 발생 합니다. ASP.NET 4 웹 응용 프로그램이 IIS 7 (또는 IIS 7.5)에서 실행 되는지 아니면 iis 6에서 실행 되는지에 따라 IIS 구성 시스템 또는 ASP.NET 4 컴파일 시스템에서 오류를 반환 합니다.

이 문제를 해결 하 고 자식 ASP.NET 4 응용 프로그램을 작동 하도록 설정 하기 위해 수행 해야 하는 단계는 ASP.NET 4 응용 프로그램이 IIS 6에서 실행 되는지 아니면 iis 7 (또는 IIS 7.5)에서 실행 되는지에 따라 달라 집니다.

### <a name="step-1-iis-7-or-iis-75-only"></a>1 단계 (IIS 7 또는 IIS 7.5에만 해당)

이 단계는 IIS 7 또는 IIS 7.5를 실행 하는 운영 체제 (Windows Vista, Windows Server 2008, Windows 7 및 Windows Server 2008 R2 포함) 에서만 필요 합니다.

부모 응용 프로그램의 `Web.config` 파일 (ASP.NET 2.0 또는 ASP.NET 3.5를 실행 하는 응용 프로그램)의 **Configsections** 정의를 the.NET Framework 2.0의 루트 `Web.config` 파일로 이동 합니다. IIS 7 및 IIS 7.5 네이티브 구성 시스템은 구성 파일의 계층 구조를 병합할 때 **Configsections** 요소를 검색 합니다. **Configsections** 정의를 부모 웹 응용 프로그램의 `Web.config` 파일에서 루트 `Web.config` 파일로 이동 하면 자식 ASP.NET 4 응용 프로그램에 대해 발생 하는 구성 병합 프로세스에서 요소를 효과적으로 숨깁니다.

32 비트 운영 체제 또는 32 비트 응용 프로그램 풀의 경우 ASP.NET 2.0 및 ASP.NET 3.5에 대 한 루트 `Web.config` 파일은 일반적으로 다음 폴더에 있습니다.

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

64 비트 운영 체제 또는 64 비트 응용 프로그램 풀의 경우 ASP.NET 2.0 및 ASP.NET 3.5에 대 한 루트 `Web.config` 파일은 일반적으로 다음 폴더에 있습니다.

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

64 비트 컴퓨터에서 32 비트 및 64 비트 웹 응용 프로그램을 모두 실행 하는 경우에는 **Configsections** 요소를 32 비트 및 64 비트 시스템 모두의 루트 `Web.config` 파일로 이동 해야 합니다.

**Configsections** 요소를 루트 `Web.config` 파일에 배치 하는 경우 섹션을 **구성** 요소 바로 다음에 붙여 넣습니다. 다음 예제에서는 요소 이동을 완료 했을 때 루트 `Web.config` 파일의 위쪽 부분이 어떻게 표시 되는지 보여 줍니다.

> [!NOTE]
> 다음 예제에서 줄은 가독성을 위해 래핑됩니다.

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>2 단계 (모든 IIS 버전)

이 단계는 ASP.NET 4 자식 웹 응용 프로그램이 IIS 6 또는 iis 7 (또는 IIS 7.5)에서 실행 되 고 있는지 여부에 관계 없이 필요 합니다.

ASP.NET 2 또는 ASP.NET 3.5를 실행 하는 부모 웹 응용 프로그램의 `Web.config` 파일에서 구성 항목이 부모 웹 응용 프로그램에만 적용 된다는 것을 명시적으로 지정 하는 **location** 태그를 추가 합니다 (IIS 및 ASP.NET 구성 시스템 모두에 대해). 다음 예제에서는 추가할 **location** 요소의 구문을 보여 줍니다.

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

다음 예제에서는 **위치** 태그를 사용 하 여 **appSettings** 섹션으로 시작 하 고 **system.webserver** 섹션으로 끝나는 모든 구성 섹션을 래핑하는 방법을 보여 줍니다.

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

1 단계와 2 단계를 완료 하면 자식 ASP.NET 4 웹 응용 프로그램이 오류 없이 시작 됩니다.

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>SharePoint가 설치 된 컴퓨터에서 ASP.NET 4 웹 사이트를 시작 하지 못함

SharePoint를 실행 하는 웹 서버에는 SharePoint 웹 사이트의 루트에 배포 되는 `Web.config` 파일이 있습니다 (예: 기본 웹 사이트의 `c:\inetpub\wwwroot\web.config`). 이 `Web.config` 파일에서 SharePoint는 WSS\_최소한 이라는 사용자 지정 부분 신뢰 수준을 설정 합니다.

이 유형의 SharePoint 웹 사이트의 자식으로 배포 된 ASP.NET 4 웹 사이트를 실행 하려고 하면 다음과 같은 오류가 표시 됩니다.

`Could not find permission set named 'ASP.NET'.`

이 오류는 ASP.NET 4 CAS (코드 액세스 보안) 인프라에서 이름이 ASP.NET 인 권한 집합을 검색 하기 때문에 발생 합니다. 그러나 WSS\_에 의해 참조 되는 부분 신뢰 구성 파일에는 해당 이름의 사용 권한 집합이 포함 되어 있지 않습니다.

현재 ASP.NET과 호환 되는 SharePoint 버전은 사용할 수 없습니다. 따라서 ASP.NET 4 웹 사이트를 SharePoint 웹 사이트 아래에 자식 사이트로 실행 해서는 안 됩니다.

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest 속성은 더 이상 PathInfo 값을 포함 하지 않습니다.

이전 버전의 ASP.NET에는 **HttpRequest**, **HttpRequest, AppRelativeCurrentExecutionFilePath**및 **HttpRequest**파일 경로를 비롯 한 다양 한 파일 경로 관련 속성에서 반환 된 값에 **pathinfo** 값이 포함 되었습니다. ASP.NET 4는 이러한 속성의 반환 값에 **Pathinfo** 값을 더 이상 포함 하지 않습니다. 대신, **pathinfo** 정보는 **HttpRequest**에서 사용할 수 있습니다. 예를 들어 다음과 같은 URL 조각을 가정해 보겠습니다.

`/testapp/Action.mvc/SomeAction`

이전 버전의 ASP.NET에서 **HttpRequest** 속성 값은 다음과 같습니다.

**HttpRequest**: `/testapp/Action.mvc/SomeAction`

**HttpRequest**: (비어 있음)

ASP.NET 4에서 **HttpRequest** 속성의 값은 다음과 같습니다.

**HttpRequest**: `/testapp/Action.mvc`

**HttpRequest**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 응용 프로그램은 eurl을 참조 하는 HttpException 오류를 생성할 수 있습니다.

IIS 6에서 ASP.NET 4를 사용하도록 설정한 경우 IIS 6(Windows Server 2003 또는 Windows Server 2003 R2)에서 실행되는 ASP.NET 2.0 애플리케이션에서 다음과 같은 오류가 발생할 수 있습니다.

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

이 오류는 ASP.NET에서 웹 사이트가 ASP.NET 4를 사용 하도록 구성 된 것을 감지 했을 때 ASP.NET 4의 네이티브 구성 요소는 추가 처리를 위해 확장명 없는 URL을 ASP.NET의 관리 되는 부분에 전달 하기 때문에 발생 합니다. 그러나 ASP.NET 4 웹 사이트 아래에 있는 가상 디렉터리가 ASP.NET 2.0를 사용 하도록 구성 된 경우이 방식으로 확장명 없는 URL을 처리 하면 "eurl. t a l l" 문자열이 포함 된 수정 된 URL이 생성 됩니다. 그러면이 수정 된 URL이 ASP.NET 2.0 응용 프로그램으로 전송 됩니다. ASP.NET 2.0은 "eurl" 형식을 인식할 수 없습니다. 따라서 ASP.NET 2.0는 `eurl.axd` 라는 파일을 찾고 실행 합니다. 이러한 파일이 없기 때문에 요청이 실패 하 고 **httpexception** 예외가 발생 합니다.

다음 옵션 중 하나를 사용 하 여이 문제를 해결할 수 있습니다.

### <a name="option-1"></a>옵션 1

웹 사이트를 실행 하기 위해 ASP.NET 4가 필요 하지 않은 경우 ASP.NET 2.0을 대신 사용 하도록 사이트를 다시 매핑합니다.

### <a name="option-2"></a>옵션 2

웹 사이트를 실행 하기 위해 ASP.NET 4가 필요한 경우 자식 ASP.NET 2.0 가상 디렉터리를 ASP.NET 2.0에 매핑된 다른 웹 사이트로 이동 합니다.

### <a name="option-3"></a>옵션 3

웹 사이트를 ASP.NET 2.0로 다시 매핑하지 않거나 가상 디렉터리의 위치를 변경 하는 것이 실용적이 지 않은 경우 ASP.NET 4에서 확장명 없는 URL 처리를 명시적으로 사용 하지 않도록 설정 합니다. 이렇게 하려면 다음 절차를 수행합니다.

1. Windows 레지스트리에서 다음 노드를 엽니다.

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. **EnableExtensionlessUrls**라는 새 **DWORD** 값을 만듭니다.
2. **EnableExtensionlessUrls** 을 0으로 설정 합니다. 이렇게 하면 확장명 없는 URL 동작이 사용 되지 않습니다.
3. 레지스트리 값을 저장 하 고 레지스트리 편집기를 닫습니다.
4. **Iisreset** 명령줄 도구를 실행 하면 IIS가 새 레지스트리 값을 읽습니다.

> [!NOTE]
> **EnableExtensionlessUrls** 를 1로 설정 하면 확장명 없는 URL 동작을 사용할 수 있습니다. 값이 지정 되지 않은 경우이 설정이 기본 설정입니다.

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>IIS 7 또는 IIS 7.5 통합 모드의 기본 문서에서는 이벤트 처리기가 발생 하지 않을 수 있습니다.

ASP.NET 4에는 확장명 없는 URL이 기본 문서로 확인 될 때 HTML **양식** 요소의 **작업** 특성이 렌더링 되는 방식을 변경 하는 수정이 포함 되어 있습니다. 기본 문서를 확인 하는 확장명 없는 URL의 예를 [http://contoso.com/](http://contoso.com/)하 여 [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)에 대 한 요청을 생성 합니다.

ASP.NET 4는 이제 기본 문서가 매핑된 확장명 없는 URL에 대 한 요청이 있을 때 HTML **양식** 요소의 **동작** 특성 값을 빈 문자열로 렌더링 합니다. 예를 들어 ASP.NET의 이전 릴리스에서는 [http://contoso.com](http://contoso.com) 에 대 한 요청으로 인해 `Default.aspx`요청이 발생 합니다. 이 문서에서 다음 예제와 같이 여는 **양식** 태그가 렌더링 됩니다.

`<form action="Default.aspx" />`

ASP.NET 4에서는 [http://contoso.com](http://contoso.com) 에 대 한 요청으로 인해 `Default.aspx`요청도 발생 합니다. 그러나 이제 ASP.NET은 다음 예제와 같이 HTML 여는 **form** 태그를 렌더링 합니다.

`<form action="" />`

**작업** 특성이 렌더링 되는 방법의 이러한 차이로 인해 IIS 및 ASP.NET에서 양식 게시물이 처리 되는 방식이 약간 변경 될 수 있습니다. **Action** 특성이 빈 문자열이 면 IIS **defaultdocumentmodule** 개체는 `Default.aspx`에 대 한 자식 요청을 만듭니다. 대부분의 상황에서이 자식 요청은 응용 프로그램 코드에 투명 하며 `Default.aspx` 페이지는 정상적으로 실행 됩니다.

그러나 관리 코드와 IIS 7 또는 IIS 7.5 통합 모드 간의 잠재적 상호 작용으로 인해 관리되는 .aspx 페이지가 자식 요청 중에 제대로 작동하지 않을 수 있습니다. 다음 조건이 발생 하면 `Default.aspx` 문서에 대 한 자식 요청으로 인해 오류가 발생 하거나 예기치 않은 동작이 발생 합니다.

1. .Aspx 페이지는 **form** 요소의 **action** 특성이 ""로 설정 된 상태로 브라우저에 전송 됩니다.
2. 양식이 ASP.NET에 다시 게시 됩니다.
3. 관리 되는 HTTP 모듈은 엔터티 본문의 일부를 읽습니다. 예를 들어 모듈은 **요청. Form** 또는 **request. Params**를 읽습니다. 이렇게 하면 POST 요청의 엔터티 본문이 관리되는 메모리로 읽힙니다. 결과적으로 IIS 7 또는 IIS 7.5 통합 모드에서 실행 중인 모든 네이티브 코드 모듈에서 더 이상 엔터티 본문을 사용할 수 없습니다.
4. IIS **Defaultdocumentmodule** 개체는 궁극적으로 실행 되 고 `Default.aspx` 문서에 대 한 자식 요청을 만듭니다. 그러나 엔터티 본문은 이미 관리 코드에 의해 읽혔기 때문에 자식 요청에 보낼 수 있는 엔터티 본문이 없습니다.
5. HTTP 파이프라인이 자식 요청에 대해 실행 될 때 `.aspx` 파일에 대 한 처리기는 처리기 실행 단계에서 실행 됩니다.
6. 엔터티 본문이 없으므로 폼 변수는 없으며 뷰 상태는 없으므로 .aspx 페이지 처리기에서 발생 해야 하는 이벤트 (있는 경우)를 결정 하는 데 사용할 수 있는 정보가 없습니다. 그 결과, 영향을 받는 .aspx 페이지의 포스트백 이벤트 처리기는 실행되지 않습니다.

다음과 같은 방법으로이 동작을 해결할 수 있습니다.

- 기본 문서 요청 중 요청 엔터티 본문에 액세스 하는 HTTP 모듈을 식별 하 고 관리 되는 요청에 대해서만 실행 되도록 구성할 수 있는지 여부를 확인 합니다. IIS 7 및 IIS 7.5에 대 한 통합 모드에서는 모듈의 **system.webserver/modules** 항목에 다음 특성을 추가 하 여 HTTP 모듈을 관리 되는 요청에 대해서만 실행 되도록 표시할 수 있습니다.

- `precondition="managedHandler"`

- 이 설정은 IIS 7 및 IIS 7.5에서 관리 되는 요청이 아닌 것으로 확인 하는 요청에 대해 모듈을 사용 하지 않도록 설정 합니다. 기본 문서 요청의 경우 첫 번째 요청은 확장명 없는 URL입니다. 따라서 IIS는 초기 요청 처리 중에 관리 되는 처리기의 사전 조건으로 표시 된 관리 되는 모듈을 실행 하지 않습니다. 따라서 관리 되는 모듈은 실수로 엔터티 본문을 읽지 않으므로 엔터티 본문을 계속 사용할 수 있으며 자식 요청 및 기본 문서에 함께 전달 됩니다.

- 모든 요청에 대해 문제가 있는 HTTP 모듈을 실행 해야 하는 경우 (정적 파일의 경우, 관리 되는 요청에 대해 **Defaultdocumentmodule** 개체로 확인 되는 확장명 없는 url의 경우) 페이지의 **HtmlForm** 컨트롤의 **Action** 속성을 비어 있지 않은 문자열로 명시적으로 설정 하 여 영향을 받는 .aspx 페이지를 수정 합니다. 예를 들어 기본 문서가 `Default.aspx`이면 페이지의 코드를 수정 하 여 **HtmlForm** 컨트롤의 **작업** 속성을 "default.aspx"로 명시적으로 설정 합니다.

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>ASP.NET CAS (코드 액세스 보안) 구현에 대 한 변경 내용

ASP.NET 2.0 및 3.5에 추가 된 ASP.NET 기능을 확장 하 여 .NET Framework 1.1 및 2.0 CAS (코드 액세스 보안) 모델을 사용 합니다. 그러나 ASP.NET 4의 CAS 구현은 크게 개선되었습니다. 결과적으로, GAC (전역 어셈블리 캐시)에서 실행 되는 신뢰할 수 있는 코드를 사용 하는 부분 신뢰 ASP.NET 응용 프로그램은 다양 한 보안 예외로 인해 실패할 수 있습니다. 컴퓨터 CAS 정책에 대 한 광범위 한 수정 작업을 사용 하는 부분 신뢰 응용 프로그램 에서도 보안 예외가 발생할 수 있습니다.

다음 예제와 같이 **트러스트** 구성 요소의 new **legacyCasModel** 특성을 사용 하 여 부분 신뢰 ASP.NET 4 응용 프로그램을 ASP.NET 1.1 및 2.0의 동작으로 되돌릴 수 있습니다.

`<trust level= "Medium" legacyCasModel="true" />`

레거시 CAS 모델로 되돌리면 다음과 같은 이전 CAS 동작을 사용할 수 있습니다.

- 컴퓨터 CAS 정책이 적용 됩니다.
- 단일 응용 프로그램 도메인에 여러 다른 권한 집합이 허용 됩니다.
- ASP.NET 또는 다른 .NET Framework 코드만 스택에 있을 때 호출 되는 GAC의 어셈블리에는 명시적 권한 어설션이 필요 하지 않습니다.

.NET Framework 4에서는 한 가지 시나리오를 되돌릴 수 없습니다. 웹이 아닌 부분 신뢰 응용 프로그램은 더 이상 System.web 및 System.object의 특정 Api를 호출할 수 없습니다. 이전 버전의 .NET Framework에서는 비 웹 부분 신뢰 응용 프로그램에 **AspNetHostingPermission** 권한이 명시적으로 부여 될 수 있었습니다. 그런 다음 이러한 응용 프로그램은 system.web. **HttpUtility**의 형식, **\*** 네임 스페이스 및 멤버 자격, 역할 및 프로필과 관련 된 형식을 사용할 수 있습니다. 웹이 아닌 부분 신뢰 응용 프로그램에서 이러한 형식을 호출 하는 것은 .NET Framework 4에서 더 이상 지원 되지 않습니다.

> [!NOTE]
> **HtmlEncode** 및 **htmldecode** 클래스가 새 .NET Framework 4 **webutility.htmldecode** 클래스로 이동 되었습니다 (영문 **).** 사용 중인 유일한 ASP.NET 기능 이라면 새 **webutility.htmldecode** 클래스를 대신 사용 하도록 응용 프로그램 코드를 수정 합니다.

다음은 ASP.NET 4의 기본 CAS 구현 변경 내용에 대 한 개략적인 요약입니다.

- ASP.NET 응용 프로그램 도메인은 이제 유형이 같은 응용 프로그램 도메인입니다. 응용 프로그램 도메인에서는 부분 신뢰 및 완전 신뢰 권한 집합만 사용할 수 있습니다.
- ASP.NET 부분 신뢰 권한 부여 집합은 엔터프라이즈 수준, 컴퓨터 수준 또는 사용자 수준 CAS 정책과 독립적입니다.
- 3\.5 및 3.5 s p 1에서 제공 되는 ASP.NET 어셈블리는 .NET Framework 4 투명도 모델을 사용 하도록 변환 되었습니다.
- ASP.NET **AspNetHostingPermission** 특성을 사용 하는 것은 상당히 감소 되었습니다. 이 특성의 대부분의 인스턴스는 public ASP.NET Api에서 제거 되었습니다.
- ASP.NET 빌드 공급자가 만든 동적으로 컴파일된 어셈블리가 명시적으로 어셈블리를 투명 하 게 표시 하도록 업데이트 되었습니다.
- 모든 ASP.NET 어셈블리는 이제 웹 호스팅 환경 에서만 APTCA 특성이 적용 되도록 표시 됩니다. ClickOnce와 같은 부분적으로 신뢰할 수 있는 비 웹 호스팅 환경에서는 ASP.NET 어셈블리를 호출할 수 없습니다.

New ASP.NET 4 code access security model에 대 한 자세한 내용은 MSDN 웹 사이트의 [ASP.NET 응용 프로그램에서 코드 액세스 보안 사용](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) 을 참조 하세요.

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>MembershipUser 네임 스페이스의 기타 형식이 이동 되었습니다.

ASP.NET 멤버 자격에 사용 되는 일부 형식이 `System.Web.dll`에서 새 어셈블리로 이동 되었습니다. 클라이언트 형식 및 확장된 .NET Framework SKU 형식 간 아키텍처 계층화 종속성을 해결하기 위해 형식을 이동했습니다.

ASP.NET 컴파일 시스템에서 기본적으로 사용 되는 참조 된 어셈블리 목록에 system.web. p s d. .dll을 추가 했기 때문에 웹 사이트 프로젝트에는 이러한 형식을 이동한 결과로 발생 하는 문제가 없습니다. 이전 버전의 ASP.NET를 사용 하 여 만든 웹 사이트 프로젝트를 Visual Studio 2010에서 ASP.NET 4로 업그레이드 하는 경우 프로젝트는 오류 없이 컴파일됩니다.

마찬가지로, ASP.NET의 이전 버전에서 만든 웹 응용 프로그램 프로젝트를 Visual Studio 2010에서 열어 ASP.NET 4로 업그레이드 하는 경우에는 업그레이드 프로세스에서 프로젝트에 System.web. c o n t e r. d a t e r .dll에 대 한 참조를 추가 합니다. 따라서 업그레이드 된 웹 응용 프로그램 프로젝트도 오류 없이 컴파일됩니다.

이전 버전의 ASP.NET를 사용 하 여 만든 컴파일된 (이진) 파일도 ASP.NET 4에서 오류 없이 실행 됩니다. 멤버 자격 형식이 다른 어셈블리로 이동 된 경우에도 마찬가지입니다. 형식 전달 정보는 이러한 형식에 대 한 런타임 참조를 형식의 새 위치로 자동으로 라우팅하는 ASP.NET 4 버전의 `System.Web.dll`에 추가 되었습니다.

그러나 특정 멤버 자격 형식을 사용 하 고 이전 버전의 ASP.NET에서 업그레이드 한 클래스 라이브러리는 ASP.NET 4 프로젝트에서 사용 될 때 컴파일되지 않습니다. 예를 들어 클래스 라이브러리 프로젝트는 다음과 같은 오류를 컴파일하고 보고 하지 못할 수 있습니다.

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

클래스 라이브러리 프로젝트의 참조를 System.object에 추가 하면이 문제를 해결할 수 있습니다.

다음 목록에서는 `System.Web.dll`에서 System.object로 이동 된 *system.web. s* e r e.

- *MembershipCreateStatus.*
- *CreateUserException입니다.*
- *System.web.security.membershippasswordexception.*
- *MembershipPasswordFormat.*
- *System.web.*
- *MembershipProviderCollection.*
- *MembershipUser.*
- *MembershipUserCollection.*
- *MembershipValidatePasswordEventHandler.*
- *ValidatePasswordEventArgs.*
- *RoleProvider.*
- <a id="0.1_a"></a>*MembershipPasswordCompatibilityMode.*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>HTTP 헤더 \* 변경 내용이 변경 되는 출력 캐싱

ASP.NET 1.0에서 버그는 `Location="ServerAndClient"` 지정 된 캐시 된 페이지를 출력-캐시 설정으로 발생 하 여 응답에서 `Vary:*` HTTP 헤더를 내보냅니다. 이로 인해 클라이언트 브라우저가 페이지를 로컬에 캐시하지 못했습니다.

ASP.NET 1.1에서 **HttpCachePolicy SetOmitVaryStar** 메서드를 추가 했습니다 .이 메서드를 호출 하 여 `Vary:*` 헤더를 표시 하지 않을 수 있습니다. 내보낸 HTTP 헤더를 변경 하는 것이 당시에 잠재적으로 변경 되는 것으로 간주 되므로이 메서드를 선택 했습니다. 그러나 개발자가 ASP.NET의 동작을 혼동 하 고 버그 보고서는 개발자가 기존 **SetOmitVaryStar** 동작을 인식 하지 못하는 것으로 제안 합니다.

ASP.NET 4에서는 근본 문제를 해결 하기 위한 결정을 내려야 합니다. `Vary:*` HTTP 헤더는 다음 지시문을 지정 하는 응답에서 더 이상 내보내지 않습니다.

`<%@OutputCache Location="ServerAndClient" %>`

따라서 `Vary:*` 헤더를 표시 하지 않기 위해 **SetOmitVaryStar** 가 더 이상 필요 하지 않습니다.

페이지의 **@ OutputCache** 지시문에 `Location="ServerAndClient"`를 지정 하는 응용 프로그램에서는 이제 **Location** 특성 값의 이름으로 암시 된 동작이 표시 됩니다. 즉, **SetOmitVaryStar** 메서드를 호출 하지 않고도 브라우저에서 페이지를 캐시할 수 있습니다.

응용 프로그램의 페이지가 `Vary:*`를 내보내야 하는 경우 다음 예제와 같이 **Appendheader** 메서드를 호출 합니다.

`HttpResponse.AppendHeader("Vary","*");`

또는 출력 캐싱 **위치** 특성의 값을 "Server"로 변경할 수 있습니다.

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport의 system.web. 보안 형식은 사용 되지 않습니다.

ASP.NET 2.0에 기본 제공 되는 Passport 지원은 Passport (현재 LiveID)의 변경으로 인해 몇 년 동안 사용 되지 않으며 지원 되지 않습니다. 결과적으로 ObsoleteAttribute의 Passport와 관련 된 5 가지 형식이 **이제는** 특성으로 표시 됩니다.

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>PopOutImageUrl 속성은 ASP.NET 4에서 이미지를 렌더링 하지 못합니다.

ASP.NET 3.5에서는 *MenuItem. PopOutImageUrl* 속성을 사용 하 여 메뉴 항목에 동적 하위 메뉴가 있음을 나타내기 위해 메뉴 항목에 표시 되는 이미지의 URL을 지정할 수 있습니다. 다음 예제에서는 ASP.NET 3.5의 태그에서이 속성을 지정 하는 방법을 보여 줍니다.

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

ASP.NET 4의 디자인 변경으로 인해 *MenuItem* 클래스에 대해 속성이 설정 된 경우 *PopOutImageUrl* 에 대 한 출력이 렌더링 되지 않습니다. 대신 *StaticPopOutImageUrl* 속성 또는 *DynamicPopOutImageUrl* 속성을 사용 하 여 *메뉴* 컨트롤에서 직접 이미지 URL을 지정 해야 합니다. 정적 메뉴로 작업 하는 경우 *StaticPopOutImageUrl* 속성은 다음 예제와 같이 정적 메뉴 항목에 하위 메뉴가 있음을 나타내기 위해 표시 되는 이미지의 URL을 지정 합니다.

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

동적 메뉴를 사용 하 여 작업 하는 경우 DynamicPopOutImageUrl 속성을 사용 하 여 동적 메뉴 항목에 하위 메뉴가 있음을 나타내는 이미지의 URL을 지정 합니다 *.* 다음 예제는 이전 예제와 유사 하지만 동적 메뉴에 대해 *DynamicPopOutImageUrl* 속성을 설정 하는 방법을 보여 줍니다.

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

*DynamicPopOutImageUrl* 속성이 설정 되어 있지 않고 *DynamicEnableDefaultPopOutImage* 속성이 *false*로 설정 되어 있으면 이미지가 표시 되지 않습니다. 마찬가지로 *StaticPopOutImageUrl* 속성이 설정 되어 있지 않고 *StaticEnableDefaultPopOutImage* 속성이 *false*로 설정 된 경우 이미지가 표시 되지 않습니다.

이러한 속성에 대 한 경로를 설정 하는 경우 백슬래시 (\)) 대신 슬래시 (/)를 사용 합니다. 자세한 내용은 StaticPopOutImageUrl 및 DynamicPopOutImageUrl를 참조 하세요. 경로에이 문서의 다른 위치에 [백슬래시가 포함 되어 있는 경우 이미지를 렌더링 하지 못합니다](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu StaticPopOutImageUrl_and_Menu입니다.") .

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>StaticPopOutImageUrl 및 DynamicPopOutImageUrl는 경로에 백슬래시가 포함 될 때 이미지를 렌더링 하지 못합니다.

ASP.NET 4에서 *StaticPopOutImageUrl* 및 *DynamicPopOutImageUrl* 속성을 사용 하 여 지정 하는 이미지는 경로에 backlashes (\)포함 되어 있는 경우에는 렌더링 되지 않습니다. 이는 이전 버전의 ASP.NET에서 변경 된 내용입니다.

다음 *Menu* 컨트롤 태그 예제에서는 백슬래시가 포함 된 경로를 사용 하 여 *StaticPopOutImageUrl* 속성을 설정 하는 방법을 보여 줍니다. ASP.NET 4에서 속성에 지정 된 이미지는 렌더링 되지 않습니다.

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

이 문제를 해결 하려면 *StaticPopOutImageUrl* 및 *DynamicPopOutImageUrl* 속성에 지정 된 경로 값을 슬래시 (/)를 사용 하도록 변경 합니다. 다음 예에서는 이러한 변경을 보여 줍니다.

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

*PopOutImageUrl* 속성이 변경 되었으므로 이전 버전의 ASP.NET에서 ASP.NET 4로 마이그레이션한 응용 프로그램도 영향을 받을 수 있습니다. 자세한 내용은이 문서의 다른 위치에서 [PopOutImageUrl 속성이 ASP.NET 4에서 이미지를 렌더링 하지 못합니다](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem PopOutImageUrl_Propert") .를 참조 하세요.

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.

이 백서는 정보를 제공할 목적으로만 사용됩니다. MICROSOFT는 이 문서에 포함된 정보와 관련하여 명시적이든 암시적이든 어떠한 보증도 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.

Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.

별도로 언급 하지 않는 한, 용례에 사용 된 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트는 실제 데이터가 아닙니다. 어떠한 실제 회사, 조직, 제품, 도메인 이름, 전자 메일에도 연결 되지 않습니다. 주소, 로고, 사람, 장소 또는 이벤트를 작성 하거나 유추 해야 합니다.

© 2010 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 인용된 실제 회사와 제품 이름은 해당 소유자의 상표일 수 있습니다.
