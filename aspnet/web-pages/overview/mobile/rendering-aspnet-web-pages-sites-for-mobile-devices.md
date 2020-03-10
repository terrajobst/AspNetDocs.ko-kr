---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 모바일 장치용 Razor (ASP.NET 웹 페이지) 사이트 렌더링 | Microsoft Docs
author: Rick-Anderson
description: '이 문서에서는 모바일 장치에서 적절히 렌더링 되는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다. 학습 내용: 방법 ...'
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454355"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a>모바일 장치용 Razor (ASP.NET 웹 페이지) 사이트 렌더링

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 모바일 장치에서 적절히 렌더링 되는 ASP.NET 웹 페이지 (Razor) 사이트에서 페이지를 만드는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 명명 규칙을 사용 하 여 모바일 장치용으로 특별히 디자인 된 페이지를 지정 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

ASP.NET 웹 페이지를 사용 하 여 모바일 또는 기타 장치에서 콘텐츠를 렌더링 하기 위한 사용자 지정 디스플레이를 만들 수 있습니다.

ASP.NET 웹 페이지 사이트에서 장치별 페이지를 만드는 가장 간단한 방법은 파일 이름 지정 패턴을 사용 하는 것입니다. 예: 파일 *이름. Mobile. cshtml*. 두 버전의 페이지를 만들 수 있습니다. 예를 들어 한 페이지의 페이지를 만들 수 있습니다 (예: *myfile* 및 이름이 *myfile*). 런타임에 모바일 장치에서 *myfile. cshtml*를 요청 하면 ASP.NET는 *myfile*에서 콘텐츠를 렌더링 합니다. 그렇지 않으면 *MyFile* 이 렌더링 됩니다.

다음 예제에서는 모바일 장치에 대 한 콘텐츠 페이지를 추가 하 여 모바일 렌더링을 사용 하도록 설정 하는 방법을 보여 줍니다. 1 *. cshtml* 에는 콘텐츠와 탐색 사이드바가 포함 됩니다. 로 *이동 합니다. 휴대폰과* 동일한 콘텐츠를 포함 하지만 사이드바는 생략 합니다.

1. ASP.NET 웹 페이지 사이트에서 *파일 이름으로* 파일을 만들고 현재 콘텐츠를 다음 태그로 바꿉니다.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. 파일 이름으로 파일을 *만들고, 기존* 내용을 다음 태그로 바꿉니다. 더 작은 화면에서 렌더링 하기 쉽도록 페이지의 모바일 버전에 탐색 섹션이 생략 됩니다.

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. 바탕 화면 브라우저를 실행 하 고 1, *cshtml*로 이동 합니다. ![mobilesites](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. 모바일 브라우저 (또는 모바일 장치 에뮬레이터)를 실행 하 고, 1, *cshtml*로 이동 합니다. *. Mobile* 은 포함 하지 않습니다. URL의 일부로 포함 됩니다. 요청이 ASP.NET로 *이동* *하는 경우에도*는를 렌더링 합니다.

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> 모바일 페이지를 테스트 하려면 데스크톱 컴퓨터에서 실행 되는 모바일 장치 시뮬레이터를 사용할 수 있습니다. 이 도구를 사용 하면 모바일 장치 (일반적으로 훨씬 더 작은 표시 영역)에서 볼 수 있는 웹 페이지를 테스트할 수 있습니다. 시뮬레이터의 한 가지 예는 Mozilla Firefox 용 [사용자 에이전트 전환기 추가 기능이](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) 며,이 기능을 사용 하면 Firefox의 데스크톱 버전에서 다양 한 모바일 브라우저를 에뮬레이트할 수 있습니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[Windows Phone 에뮬레이터](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
