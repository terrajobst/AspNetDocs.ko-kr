---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 맵 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Bing, Google, Ma ...에서 제공 하는 매핑 서비스를 기준으로 Razor (ASP.NET 웹 페이지) 웹 사이트의 페이지에 대화형 맵을 표시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518723"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 맵 표시

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Bing, Google, MapQuest 및 Yahoo에서 제공 하는 매핑 서비스를 기반으로 하는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 대화형 지도를 표시 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 주소를 기준으로 맵을 생성 하는 방법
> - 위도 및 경도 좌표를 기준으로 맵을 생성 하는 방법입니다.
> - Bing Maps 개발자 계정을 등록 하 고 Bing Maps에서 사용할 키를 가져오는 방법을 설명 합니다.
> 
> 다음은이 문서에서 소개 하는 ASP.NET 기능입니다.
> 
> - `Maps` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 2
>   
> 
> 이 자습서는 WebMatrix 3 에서도 작동 합니다.

웹 페이지에서 `Maps` 도우미를 사용 하 여 페이지에 지도를 표시할 수 있습니다. 주소 또는 경도 및 위도 좌표 집합을 기준으로 맵을 생성할 수 있습니다. `Maps` 클래스를 사용 하면 Bing, Google, MapQuest 및 Yahoo를 비롯 한 인기 있는 맵 엔진을 호출할 수 있습니다.

페이지에 매핑을 추가 하는 단계는 호출 하는 맵 엔진에 관계 없이 동일 합니다. 지도를 표시 하는 데 사용할 수 있는 메서드를 만든 다음 `Maps` 도우미의 메서드를 호출 하는 JavaScript 파일 참조를 추가 하기만 하면 됩니다.

사용 하는 `Maps` 도우미 방법을 기반으로 하는 맵 서비스를 선택 합니다. 다음 중 하나를 사용할 수 있습니다.

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a>필요한 부분 설치

지도를 표시 하려면 다음 부분이 필요 합니다.

- `Maps` 도우미입니다. 이 도우미는 ASP.NET 웹 도우미 라이브러리의 버전 2에 있습니다. 라이브러리를 아직 추가 하지 않은 경우 사이트에서 NuGet 패키지로 설치할 수 있습니다. 자세한 내용은 [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)를 참조 하세요. 갤러리에서 `microsoft-web-helpers` 패키지를 검색 합니다.
- JQuery 라이브러리입니다. 일부 WebMatrix 사이트 템플릿은 해당 *스크립트* 폴더에 jQuery 라이브러리를 이미 포함 하 고 있습니다. 이러한 라이브러리가 없으면 [jQuery.org](http://jQuery.org) 사이트에서 직접 최신 jQuery 라이브러리를 다운로드할 수 있습니다. 또는 템플릿을 사용 하 여 새 사이트 (예: **시작 사이트** 템플릿)를 만든 다음 해당 사이트의 jQuery 파일을 현재 사이트로 복사할 수 있습니다.

마지막으로, Bing maps를 사용 하려는 경우 먼저 (무료) 계정을 만들고 키를 가져와야 합니다. 키를 가져오려면 다음 단계를 수행 합니다.

1. [Bing Maps 개발자 계정](https://www.microsoft.com/maps/developers/web.aspx)에 계정을 만듭니다. Microsoft 계정 (Windows Live ID)도 있어야 합니다.

    **평가/테스트**에 키를 사용 하도록 지정할 수 있습니다. WebMatrix 및 IIS Express를 사용 하 여 자신의 컴퓨터에서 매핑 함수를 테스트 하는 경우 **사이트** 작업 영역으로 이동 하 여 사이트의 URL (예: 포트 번호가 다를 수 있지만 `http://localhost:50408`)을 기록해 둡니다. 등록할 때이 *localhost* 주소를 사이트로 사용할 수 있습니다.
2. 계정에 등록 한 후 Bing Maps 계정 센터로 이동 하 고 **키 만들기 또는 보기**를 클릭 합니다.

    ![매핑-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. Bing에서 만든 키를 기록 합니다.

## <a name="creating-a-map-based-on-an-address-using-google"></a>주소를 기준으로 맵 만들기 (Google 사용)

다음 예제에서는 주소를 기준으로 맵을 렌더링 하는 페이지를 만드는 방법을 보여 줍니다. 이 예제에서는 Google Maps를 사용 하는 방법을 보여 줍니다.

1. 사이트의 루트에 *Mapaddress. cshtml* 라는 파일을 만듭니다. 이 페이지는 전달 하는 주소를 기준으로 맵을 생성 합니다.
2. 다음 코드를 파일에 복사 하 여 기존 콘텐츠를 덮어씁니다.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    페이지의 다음 기능을 확인 합니다.

    - `<head>` 요소의 `<script>` 요소입니다. 예제에서 `<script>` 요소는 jQuery 라이브러리 버전 1.6.4의 압축 된 (압축) 버전인 *jquery-1.10.2.min.js 1.6.4* 파일을 참조 합니다. 참조에서는 *.js* 파일이 사이트의 *Scripts* 폴더에 있다고 가정 합니다. 

        > [!NOTE]
        > 다른 버전의 jQuery 라이브러리를 사용 하는 경우 해당 버전을 올바르게 가리키는지 확인 하세요.
    - 페이지 본문의 `@Maps.GetGoogleHtml`에 대 한 호출입니다. 주소를 매핑하려면 주소 문자열을 전달 해야 합니다. 다른 맵 엔진에 대 한 메서드는 비슷한 방식으로 작동 합니다 (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).
3. 페이지를 실행 하 고 주소를 입력 합니다. 이 페이지에는 사용자가 지정한 위치를 표시 하는 Google 지도를 기반으로 지도가 표시 됩니다.

     ![매핑-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a>위도 및 경도 좌표를 기준으로 지도 만들기 (Bing 사용)

이 예제에서는 좌표를 기준으로 지도를 만드는 방법을 보여 줍니다. 이 예에서는 Bing maps를 사용 하는 방법과 Bing 키를 포함 하는 방법을 보여 줍니다. (Bing 키를 사용 하지 않고 다른 맵 엔진을 사용 하 여 좌표를 기준으로 지도를 만들 수 있습니다.)

1. 사이트의 루트에 *Mapcoordinates. cshtml* 라는 파일을 만들고 기존 콘텐츠를 다음 코드 및 태그로 바꿉니다.

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. `your-key-here`를 앞에서 생성 한 Bing Maps 키로 바꿉니다.
3. *Mapcoordinates. cshtml* 페이지를 실행 하 고, 위도 및 경도 좌표를 입력 한 다음, **지도** 를 클릭 합니다. 단추를 선택합니다. (좌표를 모르는 경우 다음을 시도 하세요. Microsoft Redmond 캠퍼스의 위치입니다.)

   - 위도: 47.6781005859375
   - 경도:-122.158317565918

     지정한 좌표를 사용 하 여 페이지가 표시 됩니다.

     ![매핑-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[Microsoft Maps API 참조](https://msdn.microsoft.com/library/gg427611.aspx)
