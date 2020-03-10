---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: '방법: ASP.NET Web Forms/MVC 응용 프로그램에 모바일 페이지 추가 | Microsoft Docs'
author: rick-anderson
description: ASP.NET Web Forms/MVC 응용 프로그램에서 모바일 장치에 최적화 된 페이지를 제공 하는 다양 한 방법에 대해 설명 하 고 아키텍처를 제안 하는 방법입니다.
ms.author: riande
ms.date: 01/20/2011
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 63c555358d06a9506bb5c8c993800c3307108192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462215"
---
# <a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>방법: ASP.NET Web Forms/MVC 응용 프로그램에 모바일 페이지 추가

> **적용 대상**
> 
> - ASP.NET Web Forms 버전 4.0
> - ASP.NET MVC 버전 3.0
> 
> **요약**
> 
> ASP.NET Web Forms/MVC 응용 프로그램에서 모바일 장치에 최적화 된 페이지를 제공 하는 다양 한 방법을 설명 하 고 다양 한 장치를 대상으로 하는 경우 고려해 야 할 아키텍처와 디자인 문제를 제안 하는 방법입니다. 또한이 문서에서는 ASP.NET 2.0에서 3.5로 ASP.NET 모바일 컨트롤이 더 이상 사용 되지 않는 이유와 일부 최신 대안에 대해 설명 합니다.

## <a name="contents"></a>콘텐츠

- 개요
- 아키텍처 옵션
- 브라우저 및 장치 검색
- ASP.NET Web Forms 응용 프로그램에서 모바일 관련 페이지를 제공할 수 있는 방법
- ASP.NET MVC 응용 프로그램에서 모바일 관련 페이지를 제공 하는 방법
- 추가 리소스

ASP.NET Web Forms 및 MVC에 대 한이 백서 기술을 보여 주는 다운로드 가능한 코드 샘플은 [ASP.NET를 사용 하 여 사이트 Mobile Apps &](https://docs.microsoft.com/aspnet/mobile/overview)를 참조 하세요.

## <a name="overview"></a>개요

모바일 장치 – 스마트폰, 기능 휴대폰 및 태블릿 – 웹에 액세스 하는 수단으로 계속 해 서 성장 하 고 있습니다. 이는 많은 웹 개발자와 웹 지향 기업의 경우 해당 장치를 사용 하 여 방문자에 게 유용한 검색 환경을 제공 하는 것이 더 중요 합니다.

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>이전 버전의 ASP.NET 지원 되는 모바일 브라우저

ASP.NET 버전 2.0 ~ 3.5에 포함 된 *모바일 컨트롤* *: system.web. ASP.NET 어셈블리 및* *MobileControls* 네임 스페이스의 모바일 장치에 대 한 서버 컨트롤 집합입니다. 어셈블리는 여전히 ASP.NET 4에 포함 되어 있지만 더 이상 사용 되지 않습니다. 개발자는이 문서에서 설명 하는 것과 같은 최신 방법으로 마이그레이션하는 것이 좋습니다.

ASP.NET 모바일 컨트롤이 사용 되지 않는 것으로 표시 되는 이유는 해당 디자인이 2005 이전에 일반적인 휴대폰을 중심으로 하는 것입니다. 컨트롤은 주로 해당 연대의 WAP 브라우저에 대해 일반 HTML이 아닌 WML 또는 cHTML 태그를 렌더링 하도록 디자인 되었습니다. 그러나 HTML은 이제 모바일 및 데스크톱 브라우저에서 사용할 수 있는 태그 언어가 되기 때문에 WAP, WML 및 cHTML은 더 이상 대부분의 프로젝트와 관련이 없습니다.

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>지금 모바일 장치를 지 원하는 문제

모바일 브라우저는 일반적으로 HTML을 지원 하지만 뛰어난 모바일 검색 환경을 만들기 위해 많은 문제를 해결 해야 합니다.

- ***화면 크기*** -모바일 장치는 폼에서 현저 하 게 다르며 화면에는 데스크톱 모니터 보다 훨씬 더 작은 경우가 많습니다. 따라서 완전히 다른 페이지 레이아웃을 디자인 해야 할 수도 있습니다.
- ***입력 방법*** – 일부 장치는 키패드, 일부는 styluses, 다른 일부는 터치를 사용 합니다. 여러 탐색 메커니즘과 데이터 입력 메서드를 고려해 야 할 수 있습니다.
- ***표준 준수*** – 대부분의 모바일 브라우저는 최신 HTML, CSS 또는 JavaScript 표준을 지원 하지 않습니다.
- ***대역폭*** – 셀룰러 데이터 네트워크 성능은 무분별 달라 지 며 일부 최종 사용자는 메가바이트 단위로 요금을 부과 하는 tariffs에 있습니다.

단일 크기에 맞는 솔루션이 없습니다. 응용 프로그램은 액세스 하는 장치에 따라 다르게 표시 되 고 작동 해야 합니다. 원하는 모바일 지원 수준에 따라 웹 개발자가 데스크톱 "browser 스타워즈"가 있었던 것 보다 더 큰 과제가 될 수 있습니다.

개발자는 처음에는 일반적으로 대부분의 매우 정교한 스마트폰 (예: Windows Phone 7, iPhone 또는 Android)을 지 원하는 것으로 생각 하 고, 일반적으로는 개발자가 개인적으로 디바이스가. 그러나 더 저렴 한 휴대폰은 매우 인기 있는 것 이며, 소유자가 웹을 탐색 하는 데 사용 합니다. 특히 휴대폰을 광대역 연결 보다 더 쉽게 가져올 수 있습니다. 비즈니스는 가능한 고객을 고려 하 여 지원할 장치 범위를 결정 해야 합니다. Luxury health spa에 대 한 온라인 브로슈어를 작성 하는 경우 고급 스마트폰을 대상으로 하는 비즈니스 의사 결정을 내릴 수 있습니다. 반면, 영화에 대 한 티켓 예약 시스템을 만드는 경우에는 더 강력 하지 않은 기능을 갖춘 방문자를 고려해 야 합니다. 폰.

## <a name="architectural-options"></a>아키텍처 옵션

ASP.NET Web Forms 또는 MVC의 특정 기술 세부 정보를 얻기 전에 웹 개발자는 일반적으로 다음과 같은 세 가지 주요 방법으로 모바일 브라우저를 지원할 수 있습니다.

1. ***아무 작업도 수행 하지 않음 –*** 단순히 표준 데스크톱 지향 웹 응용 프로그램을 만들고 모바일 브라우저를 사용 하 여 해당 응용 프로그램을 사용 하는 것이 좋습니다. 

    - **장점은**구현 및 유지 관리를 위한 가장 저렴 한 옵션입니다. 추가 작업은 없습니다.
    - **단점**: 최종 사용자에 게 가장 나쁜 환경을 제공 합니다. 

        - 최신 스마트폰은 데스크톱 브라우저 뿐만 아니라 HTML만 렌더링할 수 있지만 사용자는 계속 해 서 확대/축소 하 고 가로 및 세로로 스크롤해야 작은 화면에서 콘텐츠를 사용할 수 있습니다. 이는 최적이 아닙니다.
        - 이전 장치 및 기능 휴대폰은 적절 한 방식으로 태그를 렌더링 하지 못할 수 있습니다.
        - 최신 태블릿 장치 에서도 (화면이 노트북 화면과 크게 클 수 있음) 다른 상호 작용 규칙이 적용 됩니다. 터치 기반 입력은 더 큰 단추와 링크를 사용 하 여 가장 잘 작동 하며, 플라이 아웃 메뉴 위에 마우스 커서를 올려 놓을 수 있는 방법은 없습니다.
2. ***클라이언트에서 문제를 해결***  합니다. CSS 및 [프로그레시브 기능 향상](http://en.wikipedia.org/wiki/Progressive_enhancement) 을 신중 하 게 사용 하면 브라우저에서 실행 중인 모든 항목에 맞게 태그, 스타일 및 스크립트를 만들 수 있습니다. 예를 들어 [CSS 3 미디어 쿼리](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)를 사용 하면 화면이 선택 된 임계값 보다 좁은 장치에서 단일 열 레이아웃으로 전환 되는 다중 열 레이아웃을 만들 수 있습니다. 

    - **장점**: 사용 중인 특정 장치에 대해 렌더링을 최적화 하 고, 사용 중인 화면 및 입력 특성에 따라 알 수 없는 이후 장치에 대해서도 렌더링 합니다.
    - **장점**: 모든 장치 유형에 서 서버 쪽 논리를 쉽게 공유할 수 있습니다 (코드 또는 활동의 최소 중복).
    - **단점**: 모바일 장치는 데스크톱 장치와는 달리 다른 정보를 표시 하는 데스크톱 페이지와 완전히 다를 수 있습니다. 이러한 변형은 특히, 일관 되지 않은 이전 장치에서 CSS 규칙을 해석 하는 방법을 고려 하 여 CSS를 통해 강력 하 게 구현 하기에 비효율적 이거나 불가능 합니다. 이는 CSS 3 특성의 경우 특히 그렇습니다.
    - **단점**: 다양 한 장치에 대 한 다양 한 서버 쪽 논리 및 워크플로를 지원 하지 않습니다. 예를 들어 CSS만 사용 하 여 모바일 사용자를 위한 간단한 쇼핑 카트 체크 아웃 워크플로를 구현할 수 없습니다.
    - **단점**: 비효율적인 대역폭 사용. 대상 장치에서 해당 정보의 하위 집합만 사용 하는 경우에도 서버는 가능한 모든 장치에 적용 되는 태그와 스타일을 전송 해야 할 수 있습니다.
3. ***서버에서 문제 해결* -** 서버에서 장치에 액세스 하는 항목을 알고 있는 경우 또는 최소한 해당 장치의 특성 (예: 화면 크기 및 입력 방법) 및 모바일 장치 인지 여부를 알고 있으면 다른 논리를 실행 하 고 다른 HTML 태그를 출력할 수 있습니다. 

    - **장점:** 최대 유연성. 모바일에 대 한 서버 쪽 논리를 변경 하거나 원하는 장치별 레이아웃에 대 한 태그를 최적화 하는 방법에는 제한이 없습니다.
    - **장점:** 효율적인 대역폭 사용. 대상 장치에서 사용할 태그 및 스타일 정보를 전송 하기만 하면 됩니다.
    - **단점:** 는 경우에 따라 활동이 나 코드를 반복 해 서 수행 합니다 (예: Web Forms 페이지 또는 MVC 뷰의 유사 하지만 약간 다른 복사본을 만들 수 있음). 가능 하면 일반적인 논리를 기본 계층 이나 서비스로 제한 하지만, UI 코드 또는 태그의 일부는 중복 된 다음 병렬로 유지 해야 할 수 있습니다.
    - **단점:** 장치 검색은 간단 하지 않습니다. 이 파일에는 알려진 장치 유형 및 해당 특징 (항상 완벽 하 게 최신이 아닐 수 있음)의 목록 또는 데이터베이스가 필요 하며 들어오는 모든 요청을 정확 하 게 일치 시 키 지 않을 수 있습니다. 이 문서에서는 몇 가지 옵션과 그에 대 한 몇 가지 사항을 설명 합니다.

최상의 결과를 얻기 위해 대부분의 개발자는 옵션 (2) 및 (3)을 결합 해야 합니다. 보조 스타일 차이는 CSS 또는 JavaScript를 사용 하 여 클라이언트에서 가장 잘 수용 되지만 데이터, 워크플로 또는 태그의 주요 차이점은 서버 쪽 코드에서 가장 효과적으로 구현 됩니다.

### <a name="this-paper-focuses-on-server-side-techniques"></a>이 문서에서는 서버 쪽 기술에 대해 중점적으로 설명 합니다.

ASP.NET Web Forms 및 MVC는 모두 주로 서버 쪽 기술 이므로이 백서에서는 모바일 브라우저에 대해 다른 태그와 논리를 생성할 수 있는 서버 쪽 기술에 초점을 둡니다. 물론,이를 클라이언트 쪽 기술 (예: CSS 3 미디어 쿼리, 프로그레시브 향상 JavaScript)과 결합할 수도 있지만이는 ASP.NET 개발에 비해 웹 디자인의 문제입니다.

## <a name="browser-and-device-detection"></a>브라우저 및 장치 검색

모바일 장치를 지 원하는 모든 서버 쪽 기술의 핵심 필수 구성 요소는 방문자가 사용 하 고 있는 장치를 알고 있어야 합니다. 실제로 해당 장치에 대 한 제조업체 및 모델 번호를 알고 있으면 장치 *특성* 을 알고 있는 것 보다 훨씬 더 효율적입니다. 특성에는 다음이 포함 될 수 있습니다.

- 모바일 장치 인가요?
- 입력 방법 (마우스/키보드, 터치, 키패드, 조이스틱 ...)
- 화면 크기 (물리적 및 픽셀 단위)
- 지원 되는 미디어 및 데이터 형식
- 기타

모델 번호의 특징에 따라 결정을 내리는 것이 더 효율적 이므로 향후 장치를 처리 하는 것이 더 효율적입니다.

### <a name="using-aspnets-built-in-browser-detection-support"></a>ASP 사용. NET의 기본 제공 브라우저 검색 지원

ASP.NET Web Forms 및 MVC 개발자는 *요청 .browser* 개체의 속성을 검사 하 여 방문 브라우저의 중요 한 특성을 즉시 검색할 수 있습니다. 예를 들어 다음을 참조 하세요.

- Request.Browser.IsMobileDevice
- Request.Browser.MobileDeviceManufacturer, Request.Browser.MobileDeviceModel
- Request.Browser.ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ... 기타 여러 항목

내부적으로 ASP.NET 플랫폼은 브라우저 정의 XML 파일 집합의 정규식과 들어오는 *사용자 에이전트* (UA) HTTP 헤더를 일치 시킵니다. 기본적으로 플랫폼에는 여러 일반적인 모바일 장치에 대 한 정의가 포함 되어 있으며 인식 하려는 다른 사용자에 대 한 사용자 지정 브라우저 정의 파일을 추가할 수 있습니다. 자세한 내용은 MSDN 페이지 [ASP.NET 웹 서버 컨트롤 및 브라우저 기능](https://msdn.microsoft.com/library/x3k2ssx2.aspx)을 참조 하세요.

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>51Degrees.mobi Foundation을 통해 WURFL 장치 데이터베이스 사용

ASP. 네트워크의 기본 제공 브라우저 검색 지원은 많은 응용 프로그램에서 충분 합니다. 두 가지 주요 사례는 충분 하지 않을 수 있습니다.

- ***최신 장치를 인식 하려고***합니다 (브라우저 정의 파일을 수동으로 만들지 않음). .NET 4의 브라우저 정의 파일은 Windows Phone 7, Android 휴대폰, Opera 모바일 브라우저 또는 Apple Ipad을 인식 하기에 충분 하지 않습니다.
- ***장치 기능에 대 한 자세한 정보가 필요***합니다. 장치의 입력 방법 (예: 터치 vs 키패드) 또는 브라우저에서 지 원하는 오디오 형식에 대해 알아야 할 수 있습니다. 이 정보는 표준 브라우저 정의 파일에서 사용할 수 없습니다.

[Wurfl ( *무선 유니버설 리소스 파일* ) 프로젝트](http://wurfl.sourceforge.net/) 는 현재 사용 중인 모바일 장치에 대해 훨씬 더 최신 정보 및 자세한 정보를 유지 관리 합니다.

.NET 개발자를 위한 훌륭한 소식은 ASP입니다. NET의 브라우저 검색 기능은 확장 가능 하므로 이러한 문제를 해결 하기 위해 향상 시킬 수 있습니다. 예를 들어 오픈 소스 [*51Degrees.mobi Foundation*](https://github.com/51Degrees/dotNET-Device-Detection) 라이브러리를 프로젝트에 추가할 수 있습니다. ASP.NET IHttpModule 또는 브라우저 기능 공급자 (Web Forms 및 MVC 응용 프로그램 모두에서 사용 가능)는 WURFL 데이터를 직접 읽고 ASP에 후크합니다. NET의 기본 제공 브라우저 검색 메커니즘입니다. 모듈을 설치한 후에는 요청이 갑자기 더 정확 하 고 자세한 정보를 포함 하 게 됩니다. *브라우저* 는 앞에서 언급 한 많은 장치를 올바르게 인식 하 고 해당 기능 (입력 방법 등의 추가 기능 포함)을 나열 합니다. 자세한 내용은 프로젝트 설명서를 참조 하십시오.

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>응용 프로그램 Web Forms 모바일 관련 페이지를 제공 하는 방법

기본적으로 일반적인 모바일 장치에 새로운 Web Forms 응용 프로그램을 표시 하는 방법은 다음과 같습니다.

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

물론 레이아웃은 매우 편리 하지 않습니다 .이 페이지는 작은 세로 중심 화면이 아닌 가로 방향의 가로 방향의 모니터를 위해 설계 되었습니다. 무엇을 할 수 있나요?

이 문서 앞부분에서 설명한 것 처럼 모바일 장치에 맞게 페이지를 조정 하는 여러 가지 방법이 있습니다. 일부 기술은 서버 기반 이며 다른 기술은 클라이언트에서 실행 됩니다.

### <a name="creating-a-mobile-specific-master-page"></a>모바일 관련 마스터 페이지 만들기

사용자의 요구 사항에 따라 모든 방문자에 게 동일한 Web Forms를 사용할 수 있지만 두 개의 마스터 페이지가 있습니다. 하나는 데스크톱 방문자 용 이며 다른 하나는 모바일 방문자를 위한 것입니다. 이를 통해 페이지 논리를 복제 하지 않고도 CSS 스타일 시트 또는 최상위 HTML 태그를 모바일 장치에 맞게 변경할 수 있습니다.

이렇게 하는 것이 쉽습니다. 예를 들어 다음과 같은 PreInit 처리기를 웹 폼에 추가할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

이제 응용 프로그램의 최상위 폴더에 Mobile. Master 라는 마스터 페이지를 만듭니다 .이 페이지는 모바일 장치를 검색할 때 사용 됩니다. 필요한 경우 모바일 마스터 페이지에서 모바일 관련 CSS 스타일 시트를 참조할 수 있습니다. 데스크톱 방문자에 게는 모바일 컴퓨터가 아닌 기본 마스터 페이지가 계속 표시 됩니다.

### <a name="creating-independent-mobile-specific-web-forms"></a>독립적인 모바일 관련 Web Forms 만들기

유연성을 최대화 하기 위해 서로 다른 장치 유형에 대해 별도의 마스터 페이지를 추가 하는 것 보다 훨씬 더 많은 일을 할 수 있습니다. 두 개의 *완전히 분리 된 Web Forms 페이지* 집합을 구현할 수 있습니다. 하나는 데스크톱 브라우저용으로 설정 하 고 다른 하나는 모바일에 대해 설정 합니다. 이는 모바일 방문자에 게 매우 다른 정보나 워크플로를 제공 하려는 경우에 가장 잘 작동 합니다. 이 섹션의 나머지 부분에서는이 방법에 대해 자세히 설명 합니다.

데스크톱 브라우저용으로 디자인 된 Web Forms 응용 프로그램이 있다고 가정 하 고, 계속 하는 가장 쉬운 방법은 프로젝트 내에서 "Mobile" 이라는 하위 폴더를 만들고 모바일 페이지를 빌드하는 것입니다. 다른 Web Forms 응용 프로그램에 사용 하는 것과 동일한 기술을 모두 사용 하 여 자체 마스터 페이지, 스타일 시트 및 페이지를 사용 하 여 전체 하위 사이트를 생성할 수 있습니다. 데스크톱 사이트의 *모든* 페이지에 대 한 모바일 기능을 반드시 만들 필요는 없습니다. 모바일 방문자에 게 적합 한 기능 하위 집합을 선택할 수 있습니다.

원하는 경우 모바일 페이지에서 일반 정적 리소스 (예: 이미지, JavaScript 또는 CSS 파일)를 일반 페이지와 공유할 수 있습니다. "모바일" 폴더는 IIS에서 호스팅될 때 별도의 응용 프로그램으로 표시 *되지* 않으므로 (Web Forms 페이지의 단순한 하위 폴더), 동일한 구성, 세션 데이터 및 기타 인프라를 데스크톱 페이지로 모두 공유 합니다.

> [!NOTE]
> 이 접근 방식에는 일반적으로 일부 코드 중복이 포함 됩니다. (모바일 페이지는 데스크톱 페이지와 일부 유사성을 공유할 가능성이 있습니다.) 일반적인 비즈니스 논리 또는 데이터 액세스 코드를 공유 된 기본 계층 또는 서비스에 포함 하는 것이 중요 합니다. 그렇지 않으면 응용 프로그램을 만들고 유지 관리 하는 데 드는 노력을 두는 것이 좋습니다.

#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>모바일 방문자를 모바일 페이지로 리디렉션

모바일 방문자를 검색 세션의 *첫 번째* 요청 (세션의 모든 요청이 아닌)에 대 한 모바일 페이지로 리디렉션하는 것이 편리한 경우가 종종 있습니다.

- 그러면 모바일 방문자가 원하는 경우 데스크톱 페이지에 쉽게 액세스할 수 있습니다. "데스크톱 버전"으로 이동 하는 링크를 마스터 페이지에 놓기만 하면 됩니다. 방문자는 세션에서 더 이상 첫 번째 요청이 아니기 때문에 모바일 페이지로 다시 리디렉션되지 않습니다.
- 이를 통해 사이트의 데스크톱 및 모바일 파트 간에 공유 되는 동적 리소스에 대 한 요청을 방해 하는 위험을 피할 수 있습니다. 예를 들어 사이트의 데스크톱 및 모바일 부분이 IFRAME 또는 특정 Ajax 처리기에 표시 되는 일반적인 웹 양식이 있는 경우를 들 수 있습니다.

이렇게 하려면 **세션\_시작** 메서드에 리디렉션 논리를 배치 하면 됩니다. 예를 들어 Global.asax.cs 파일에 다음 메서드를 추가 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증은 인증 프로세스 중 및 후에 방문자를 리디렉션할 수 있는 위치에 대 한 특정 가정을 수행 합니다.

- 사용자를 인증 해야 하는 경우 양식 인증은 데스크톱 로그인 페이지 ( *하나의* 로그인 URL만 사용 하기 때문에 데스크톱 또는 모바일 사용자 인지 여부에 관계 없이)로 리디렉션합니다. 모바일 로그인 페이지의 스타일을 다르게 지정할 경우 모바일 사용자를 별도의 모바일 로그인 페이지로 리디렉션하는 바탕 화면 로그인 페이지를 개선 해야 합니다. 예를 들어 다음 코드를 **데스크톱** 로그인 페이지 코드 숨김으로 추가 합니다. 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- 사용자가 성공적으로 로그인 한 후에는 폼 인증이 기본적으로 바탕 화면 홈 페이지로 리디렉션됩니다 ( *하나의* 기본 페이지 개념도 있으므로). 로그인에 성공한 후 모바일 홈 페이지로 리디렉션하기 위해 모바일 로그인 페이지를 개선 해야 합니다. 예를 들어 **모바일** 로그인 페이지 코드 숨김으로 다음 코드를 추가 합니다. 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  이 코드는 기본 프로젝트 템플릿과 같이 페이지에 LoginUser 이라는 로그인 서버 컨트롤이 있다고 가정 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱 사용

출력 캐싱을 사용 하는 경우에는 기본적으로 데스크톱 사용자가 특정 URL (출력이 캐시 되도록 하는)을 방문한 다음 캐시 된 데스크톱 출력을 받는 모바일 사용자를 사용할 수 있습니다. 이 경고는 장치 유형별로 마스터 페이지를 변경 하거나 장치 유형별으로 완전히 분리 된 Web Forms를 구현 하는 경우에 적용 됩니다.

문제를 방지 하려면 방문자가 모바일 장치를 사용 하는지 여부에 따라 캐시 항목을 변경 하도록 ASP.NET에 지시할 수 있습니다. 다음과 같이 VaryByCustom 매개 변수를 페이지의 OutputCache 선언에 추가 합니다.

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

다음으로 Global.asax.cs 파일에 다음 메서드 재정의를 추가 하 여 *isMobileDevice* 를 사용자 지정 캐시 매개 변수로 정의 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

이렇게 하면 페이지의 모바일 방문자가 이전에 데스크톱 방문자가 캐시에 넣은 출력을 받지 않게 됩니다.

### <a name="a-working-example"></a>작업 예제

이러한 기술을 작동 하는지 확인 하려면 백서 [코드 샘플](https://docs.microsoft.com/aspnet/mobile/overview)을 다운로드 하세요. Web Forms 샘플 응용 프로그램은 mobile 사용자를 mobile 이라는 하위 폴더의 모바일 특정 페이지 집합으로 자동으로 리디렉션합니다. 이러한 페이지의 태그 및 스타일 지정은 다음 스크린샷에서 볼 수 있는 것 처럼 모바일 브라우저에 대해 더 잘 최적화 되었습니다.

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

모바일 브라우저에서 태그 및 CSS를 최적화 하는 방법에 대 한 자세한 내용은이 문서의 뒷부분에 나오는 "모바일 브라우저의 모바일 페이지 스타일 지정" 섹션을 참조 하세요.

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>ASP.NET MVC 응용 프로그램에서 모바일 관련 페이지를 제공 하는 방법

모델-뷰 컨트롤러 패턴은 보기의 프레젠테이션 논리에서 응용 프로그램 논리 (컨트롤러)를 분리 다음 방법 중 하나를 선택 하 여 서버 쪽 코드의 모바일 지원 기능을 처리할 수 있습니다.

1. **데스크톱 및 모바일 브라우저에 대해 동일한 컨트롤러와 보기를 사용 *, 장치 유형 *에 따라 다른 Razor 레이아웃을 사용 하 여 보기를 렌더링 합니다.** 이 옵션은 모든 장치에서 동일한 데이터를 표시 하 고 다른 CSS 스타일 시트를 제공 하거나 모바일에 대 한 몇 가지 최상위 HTML 요소를 변경 하는 경우에 가장 적합 합니다.
2. ***데스크톱과 모바일 브라우저에 동일한 컨트롤러를 사용 하지만 장치 유형에 따라 서로 다른 보기를 렌더링***합니다. 이 옵션은 거의 동일한 데이터를 표시 하 고 최종 사용자에 게 동일한 워크플로를 제공 하지만 사용 중인 장치에 맞게 매우 다른 HTML 태그를 렌더링 하려는 경우에 가장 적합 합니다.
3. **데스크톱 및 모바일 브라우저를 위한 별도의 영역을 만들어 각 *에 대 한 독립적인 컨트롤러 및 뷰를 구현할 *.** 이 옵션은 서로 다른 정보를 포함 하 고 사용자가 장치 유형에 대해 최적화 된 여러 워크플로를 통해 사용자를 안내 하는 매우 다양 한 화면을 표시 하는 경우에 가장 적합 합니다 일부 코드를 반복 하는 것을 의미할 수도 있지만 일반적인 논리를 기본 계층 이나 서비스로 구분 하 여이를 최소화할 수 있습니다.

**첫 번째** 옵션을 사용 하 고 장치 유형별 Razor 레이아웃만 변경 하려는 경우 매우 쉽습니다. 다음과 같이 \_ViewStart. cshtml 파일을 수정 하면 됩니다.

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

이제 페이지 구조와 모바일 장치에 최적화 된 CSS 규칙을 사용 하 여 \_LayoutMobile. cshtml 이라는 모바일 관련 레이아웃을 만들 수 있습니다.

방문자의 장치 유형에 따라 **두 번째** 옵션인 완전히 다른 보기를 렌더링 하려면 [Scott Hanselman의 블로그 게시물](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx)을 참조 하세요.

이 문서의 나머지 부분에서는 모바일 방문자에 게 제공 되는 기능의 하위 집합을 정확 하 게 제어할 수 있도록 모바일 장치에 대 한 별도의 컨트롤러 *및* 보기를 만드는 **세 번째** 옵션을 중점적으로 설명 합니다.

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>ASP.NET MVC 응용 프로그램 내에서 모바일 영역 설정

일반적인 방법으로 기존 ASP.NET MVC 응용 프로그램에 "Mobile" 이라는 영역을 추가할 수 있습니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 한 다음 à 영역 추가를 선택 합니다. 그런 다음 ASP.NET MVC 응용 프로그램 내의 다른 영역에 대 한 컨트롤러 및 뷰를 추가할 수 있습니다. 예를 들어 모바일 방문자를 위한 홈페이지 역할을 하는 HomeController 라는 새 컨트롤러를 모바일 영역에 추가 합니다.

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>URL/모바일이 모바일 홈 페이지에 도달 하는지 확인

URL/Mobile에서 모바일 영역 내 HomeController의 인덱스 작업에 도달 하 게 하려면 라우팅 구성을 약간 변경 해야 합니다. 먼저 MobileAreaRegistration 클래스를 업데이트 하 여 다음 코드와 같이 HomeController가 모바일 영역의 기본 컨트롤러 인지를 업데이트 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

이는 이제 "홈"이 모바일 페이지의 암시적 기본 컨트롤러 이름이 기 때문에 모바일 홈 페이지가/Mobile/Home이 아닌/Smobile에 배치 됩니다.

다음으로 응용 프로그램에 두 번째 HomeController를 추가 하 여 (즉, 기존 데스크톱을 비롯 한 모바일 응용 프로그램) 일반 데스크톱 홈페이지를 중단 했습니다. "*이름이 ' Home ' 인 컨트롤러와 일치 하는 형식을 여러 개 찾았습니다*. 오류가 발생 하 여 실패 합니다. 이 문제를 해결 하려면 Global.asax.cs에서 최상위 라우팅 구성 ()을 업데이트 하 여 모호성이 있을 때 desktop HomeController에 우선 순위를 적용 하도록 지정 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

이제 오류가 발생 하 고 URL http:\/\/해당 *사이트*/가 데스크톱 홈 페이지에 도달 하 고, http:\/\/*사이트*/mobile/가 모바일 홈 페이지에 연결 됩니다.

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>모바일 방문자를 모바일 영역으로 리디렉션

ASP.NET MVC에는 다양 한 확장성 지점이 있으므로 리디렉션 논리를 삽입할 수 있는 여러 가지 방법이 있습니다. 한 가지 간단한 옵션은 다음 조건이 충족 되는 경우 리디렉션을 수행 하는 필터 특성 [RedirectMobileDevicesToMobileArea]을 만드는 것입니다.

1. 사용자 세션의 첫 번째 요청 (예: Session. IsNewSession은 true와 같음)
2. 요청은 모바일 브라우저에서 제공 됩니다. 즉, IsMobileDevice는 true와 같습니다.
3. 사용자가 모바일 영역에서 리소스를 아직 요청 하지 않습니다 (즉, URL의 *경로* 부분이/mobile로 시작 하지 않음).

이 백서에 포함 된 다운로드 가능한 샘플에는이 논리의 구현이 포함 되어 있습니다. 이는 AuthorizeAttribute에서 파생 된 권한 부여 필터로 구현 됩니다. 즉, 출력 캐싱을 사용 하는 경우에도 제대로 작동할 수 있습니다. 그렇지 않으면 데스크톱 방문자가 특정 URL에 처음으로 액세스 하는 경우 데스크톱 출력이 캐시 된 다음에 제공 됩니다. 이후 모바일 방문자).

필터 이므로 특정 컨트롤러 및 작업에 적용 하도록 선택할 수 있습니다 (예:).

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… 또는 Global.asax.cs 파일에서 MVC 3 *전역 필터로* 모든 컨트롤러 및 작업에 적용할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

다운로드 가능한 샘플은 또한 모바일 영역 내의 특정 위치로 리디렉션되는이 특성의 서브 클래스를 만들 수 있는 방법을 보여 줍니다. 즉, 예를 들어 다음을 수행할 수 있습니다.

- 위에서 설명한 대로 전역 필터를 등록 하 여 모바일 방문자를 기본적으로 모바일 홈 페이지로 보냅니다.
- 또한 모바일 방문자가 요청한 제품 페이지의 모바일 버전으로 이동 하는 "제품 보기" 작업에 특수 [RedirectMobileDevicesToMobileProductPage] 필터를 적용 합니다.
- 또한 특정 작업에 필터의 다른 특수 서브 클래스를 적용 하 여 모바일 방문자를 해당 모바일 페이지로 리디렉션합니다.

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>모바일 페이지를 준수 하도록 폼 인증 구성

폼 인증을 사용 하는 경우 사용자가 로그인 해야 하는 경우 사용자가 단일 특정 "로그온" URL로 자동으로 리디렉션됩니다 .이 URL은 기본적으로 **/Account/logon**로 설정 됩니다. 즉, 모바일 사용자는 데스크톱 "로그온" 작업으로 리디렉션될 수 있습니다.

이 문제를 방지 하려면 모바일 사용자를 모바일 "로그온" 작업으로 다시 리디렉션할 수 있도록 데스크톱 "로그온" 작업에 논리를 추가 합니다. 기본 ASP.NET MVC 응용 프로그램 템플릿을 사용 하는 경우 다음과 같이 AccountController의 LogOn 작업을 업데이트 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… 그런 다음 모바일 영역에서 AccountController 라는 컨트롤러에 대해 적절 한 모바일 관련 "로그온" 작업을 구현 합니다.

### <a name="working-with-output-caching"></a>출력 캐싱 사용

[OutputCache] 필터를 사용 하는 경우 장치 유형에 따라 캐시 항목을 다르게 적용 해야 합니다. 예를 들어 다음을 작성 합니다.

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

그런 다음 Global.asax.cs 파일에 다음 메서드를 추가 합니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

이렇게 하면 페이지의 모바일 방문자가 이전에 데스크톱 방문자가 캐시에 넣은 출력을 받지 않게 됩니다.

### <a name="a-working-example"></a>작업 예제

이러한 기술을 작동 하는 것을 보려면 [이 백서의 코드 관련 샘플](https://docs.microsoft.com/aspnet/mobile/overview)을 다운로드 하세요. 이 샘플에는 위에 설명 된 방법을 사용 하 여 모바일 장치를 지원 하도록 향상 된 ASP.NET MVC 3 (릴리스 후보) 응용 프로그램이 포함 되어 있습니다.

## <a name="further-guidance-and-suggestions"></a>추가 지침 및 제안 사항

다음 논의는이 문서에서 설명 하는 기술을 사용 하는 Web Forms 및 MVC 개발자 모두에 게 적용 됩니다.

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>51Degrees.mobi Foundation을 사용 하 여 리디렉션 논리 향상

이 문서에 표시 된 리디렉션 논리는 응용 프로그램에 대해 완벽 하 게 충분할 수 있지만 세션을 사용 하지 않도록 설정 해야 하는 경우 또는 쿠키를 거부 하는 모바일 브라우저 (세션을 포함할 수 없음)에서 지정 된 요청이 있는지 여부를 알 수 없기 때문에 작동 하지 않습니다. 해당 방문자의 첫 번째 항목입니다.

오픈 소스 51Degrees.mobi Foundation이 ASP의 정확도를 향상 시키는 방법을 이미 배웠습니다. NET의 브라우저 검색 또한 모바일 방문자를 Web.config에 구성 된 특정 위치로 리디렉션하는 기능을 기본적으로 제공 합니다. 방문자의 HTTP 헤더 및 IP 주소 해시에 대 한 임시 로그를 저장 하 여 ASP.NET 세션 (및 쿠키)에 의존 하지 않고 작업을 수행할 수 있으므로 각 요청이 지정 된 vistor의 첫 번째 요청 인지 여부를 알 수 있습니다.

Web.config 파일의 fiftyOne 섹션에 추가 되는 다음 요소는 검색 된 모바일 장치에서 첫 번째 요청을 페이지로 리디렉션합니다. ~/Mobile/Default.aspx. 모바일 폴더의 페이지에 대 한 모든 요청은 장치 유형에 관계 없이 리디렉션되지 *않습니다* . 모바일 장치가 20 분 이상 동안 비활성 상태 이면 장치는 기억나지 않으며 이후 요청은 리디렉션의 용도에 따라 새 서비스로 처리 됩니다.

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

자세한 내용은 [51Degrees.mobi Foundation 설명서](https://github.com/51Degrees/dotNET-Device-Detection)를 참조 하세요.

> [!NOTE]
> ASP.NET MVC 응용 프로그램에서 51Degrees.mobi Foundation의 리디렉션 기능을 사용할 *수* 있지만 라우팅 매개 변수를 사용 하거나 MVC 필터를 동작에 배치 하는 것이 아니라 일반 url을 기준으로 리디렉션 구성을 정의 해야 합니다. 이는 작성 시점에 51Degrees.mobi Foundation이 필터나 라우팅을 인식 하지 못하기 때문입니다.

### <a name="disabling-transcoders-and-proxy-servers"></a>트랜스코더 및 프록시 서버 사용 안 함

모바일 네트워크 운영자는 모바일 인터넷에 대 한 접근 방식에 두 가지 광범위 한 목표가 있습니다.

1. 가능한 한 많은 관련 콘텐츠 제공
2. 제한 된 무선 네트워크 대역폭을 공유할 수 있는 고객 수를 최대화 합니다.

대부분의 웹 페이지는 대규모의 데스크톱 크기 화면과 빠른 고정 회선 광대역 연결을 위해 설계 되었으므로 많은 연산자는 웹 콘텐츠를 동적으로 변경 하는 *트랜스코더* 또는 *프록시 서버* 를 사용 합니다. 더 작은 화면에 맞게 HTML 태그 또는 CSS를 수정할 수 있습니다 (특히 복잡 한 레이아웃을 처리할 수 있는 처리 능력이 없는 "기능 폰"의 경우). 또한 페이지 배달 속도를 향상 시키기 위해 이미지를 다시 압축 하거나 품질을 대폭 줄일 수 있습니다.

그러나 모바일에 최적화 된 버전의 사이트를 생성 하는 데 필요한 작업을 수행한 경우에는 네트워크 운영자가 더 이상 충돌 하지 않도록 해야 합니다. ASP.NET 웹 폼의 Load 이벤트\_페이지에 다음 줄을 추가할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

또는 ASP.NET MVC 컨트롤러의 경우 다음 메서드 재정의를 추가 하 여 해당 컨트롤러의 모든 작업에 적용 되도록 할 수 있습니다.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

결과 HTTP 메시지는 W3C 규격 트랜스코더 및 프록시에 콘텐츠를 변경 하지 않도록 알립니다. 물론, 모바일 네트워크 운영자가이 메시지를 존중 한다는 보장이 없습니다.

### <a name="styling-mobile-pages-for-mobile-browsers"></a>모바일 브라우저의 모바일 페이지 스타일 지정

제대로 작동 하는 HTML 마크업의 종류 또는 특정 장치에서 유용성을 최대화 하는 웹 디자인 기술은이 문서의 범위를 벗어났습니다. 불안정 한 HTML 또는 CSS 위치 지정 트릭을 사용 하지 않고 모바일 크기의 화면에 최적화 된 충분히 간단한 레이아웃을 찾을 수 있습니다. 그러나 기억해 야 할 중요 한 기술 중 하나는 *뷰포트 메타 태그*입니다.

데스크톱 모니터를 위한 웹 페이지를 작성 하는 데 필요한 특정 최신 모바일 브라우저는 "뷰포트" 라고도 하는 가상 캔버스에서 페이지를 렌더링 합니다 (예: 가상 viewport는 iPhone에서 980 픽셀 너비이 고, 기본적으로 Opera Mobile에서는 850 픽셀 너비). 화면의 실제 픽셀에 맞게 결과를 축소 합니다. 그러면 사용자가 해당 뷰포트를 확대 하 고 이동할 수 있습니다. 이렇게 하면 브라우저에서 원하는 레이아웃으로 페이지를 표시할 수 있다는 이점이 있지만 확대/축소 및 이동에 대 한 단점은 사용자에 게 불편 합니다. 모바일을 위해 디자인 하는 경우 확대/축소 또는 가로 스크롤이 필요 하지 않도록 좁은 화면을 디자인 하는 것이 좋습니다.

모바일 브라우저에 지정 하는 방법은 표준이 아닌 *뷰포트* 메타 태그를 통해 뷰포트의 너비를 지정 하는 방법입니다. 예를 들어 페이지의 헤드 섹션에 다음을 추가 하는 경우

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… 그러면 smartphone 브라우저를 지 원하는 경우 480 픽셀 너비의 가상 캔버스에서 페이지가 레이아웃 됩니다. 즉, HTML 요소가 너비를 백분율로 정의 하는 경우이 백분율은 기본 뷰포트 너비가 아니라이 480 픽셀 너비와 관련 하 여 해석 됩니다. 따라서 사용자는 가로 방향으로 확대/축소 하 고 이동 하 여 모바일 검색 환경을 크게 향상 시킬 가능성이 적습니다.

뷰포트 너비를 장치의 실제 픽셀과 일치 시키려면 다음을 지정할 수 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

이 작업이 제대로 작동 하려면 요소를 명시적으로 사용 하 여 해당 너비를 초과 하지 않도록 해야 합니다 (예: *width* 특성 또는 CSS 속성 사용). 그렇지 않은 경우에도 브라우저에서 더 큰 뷰포트를 사용 하도록 강제 해야 합니다. 참고 항목: [비표준 뷰포트 태그에 대 한 자세한 내용](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html)

대부분의 최신 스마트폰은 *이중 방향을*지원 합니다. 즉, 가로 또는 세로 모드로 유지할 수 있습니다. 그러므로 화면 너비를 픽셀 단위로 가정 하지 않는 것이 중요 합니다. 사용자가 페이지에 있는 동안 장치를 다시 설정할 수 있으므로 화면 너비가 고정 되어 있다고 가정해 서는 안 됩니다.

이전 Windows Mobile 및 Blackberry 장치는 콘텐츠를 모바일에 최적화 하 여 변환 하지 않아야 함을 알리기 위해 페이지 헤더에서 다음 메타 태그를 수락할 수도 있습니다.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>추가 리소스

모바일 ASP.NET 웹 응용 프로그램을 테스트 하는 데 사용할 수 있는 모바일 장치 에뮬레이터 및 시뮬레이터 목록은 [테스트를 위해 인기 있는 모바일 장치 시뮬레이션](../mobile/device-simulators.md)페이지를 참조 하세요.

## <a name="credits"></a>크레딧

- 기본 작성자: 고 Sanderson
- 검토자/추가 콘텐츠 작성자: James Rosewell, Mikael Söderström, Scott Hanselman, Scott 헌터
