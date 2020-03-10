---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: ASP.NET 웹 페이지 (Razor) 사이트의 방문자 정보 (분석) 추적 | Microsoft Docs
author: Rick-Anderson
description: 웹 사이트를 시작한 후 웹 사이트 트래픽을 분석할 수 있습니다.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421457"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트의 방문자 정보 (분석) 추적

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 도우미를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 웹 사이트 분석을 추가 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 웹 사이트 트래픽에 대 한 정보를 분석 공급자에 게 보내는 방법입니다.
> 
> 다음은이 문서에 도입 된 ASP.NET 프로그래밍 기능입니다.
> 
> - `Analytics` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)

분석은 사용자가 사이트를 사용 하는 방법을 이해할 수 있도록 웹 사이트의 트래픽을 측정 하는 기술의 일반적인 용어입니다. Google, Yahoo, StatCounter 등의 서비스를 비롯 한 많은 분석 서비스를 사용할 수 있습니다.

분석의 작동 방식은 추적 하려는 사이트를 등록 하는 분석 공급자를 사용 하 여 계정을 등록 하는 것입니다. 공급자는 사용자 계정에 대 한 ID 또는 추적 코드를 포함 하는 JavaScript 코드의 코드 조각을 보냅니다. 추적 하려는 사이트의 웹 페이지에 JavaScript 코드 조각을 추가 합니다. 일반적으로 사이트의 모든 페이지에 표시 되는 바닥글 또는 레이아웃 페이지나 기타 HTML 태그에 분석 코드 조각을 추가 합니다. 사용자가 이러한 JavaScript 코드 조각 중 하나를 포함 하는 페이지를 요청 하면 코드 조각에서 현재 페이지에 대 한 정보를 분석 공급자에 게 보내고,이는 페이지에 대 한 다양 한 세부 정보를 기록 합니다.

사이트 통계를 확인 하려는 경우 분석 공급자의 웹 사이트에 로그인 합니다. 그러면 다음과 같이 사이트에 대 한 모든 종류의 보고서를 볼 수 있습니다.

- 개별 페이지에 대 한 페이지 보기 수입니다. 이를 통해 사이트를 방문 하는 사용자 수와 사이트의 가장 인기 있는 페이지를 알 수 있습니다.
- 사용자가 특정 페이지에 소비 하는 시간입니다. 이를 통해 홈 페이지에서 사용자의 관심을 유지 하는지 여부를 알 수 있습니다.
- 사용자가 사이트를 방문 하기 전에 방문한 사이트 이를 통해 트래픽이 링크에서 제공 되는지 검색에서 전송 되는지 여부를 파악할 수 있습니다.
- 사용자가 사이트를 방문 하는 경우와 기간을 유지 합니다.
- 방문자가 있는 국가
- 방문자가 사용 하는 브라우저 및 운영 체제

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a>도우미를 사용 하 여 페이지에 분석 추가

ASP.NET 웹 페이지에는 분석에 사용 되는 JavaScript 코드 조각을 쉽게 관리할 수 있게 해 주는 여러 분석 도우미 (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`및 `Analytics.GetStatCounterHtml`)가 포함 되어 있습니다. JavaScript 코드를 넣는 방법과 위치를 파악 하는 대신, 페이지에 도우미를 추가 하면 됩니다. 제공 해야 하는 유일한 정보는 계정 이름, ID 또는 추적 코드입니다. StatCounter의 경우 몇 가지 추가 값도 제공 해야 합니다.

이 절차에서는 `GetGoogleHtml` 도우미를 사용 하는 레이아웃 페이지를 만듭니다. 다른 분석 공급자 중 하나를 사용 하는 계정이 이미 있는 경우 해당 계정을 대신 사용 하 고 필요에 따라 약간의 조정을 수행할 수 있습니다.

> [!NOTE]
> 분석 계정을 만들 때 추적 하려는 사이트의 URL을 등록 합니다. 로컬 컴퓨터의 모든 항목을 테스트 하는 경우 실제 트래픽 (유일한 트래픽)을 추적 하지 않으므로 사이트 통계를 기록 하 고 볼 수 없습니다. 그러나이 절차에서는 페이지에 분석 도우미를 추가 하는 방법을 보여 줍니다. 사이트를 게시 하는 경우 라이브 사이트는 분석 공급자에 게 정보를 보냅니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).
2. Google Analytics를 사용 하 여 계정을 만들고 계정 이름을 기록 합니다.
3. *Analytics. cshtml* 이라는 레이아웃 페이지를 만들고 다음 태그를 추가 합니다.

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > `</body>` 태그 앞에 있는 웹 페이지의 본문에 `Analytics` 도우미에 대 한 호출을 넣어야 합니다. 그렇지 않으면 브라우저가 스크립트를 실행 하지 않습니다.

    다른 분석 공급자를 사용 하는 경우 대신 다음 도우미 중 하나를 사용 하세요.

    - (Yahoo) `@Analytics.GetYahooHtml("myaccount")`
    - (StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`
4. `myaccount`을 1 단계에서 만든 계정, ID 또는 추적 코드의 이름으로 바꿉니다.
5. 브라우저에서 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.)
6. 브라우저에서 페이지 소스를 봅니다. 렌더링 된 분석 코드를 볼 수 있습니다.

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. Google 분석 사이트에 로그인 하 고 사이트에 대 한 통계를 검토 합니다. 라이브 사이트에서 페이지를 실행 하는 경우 페이지 방문을 기록 하는 항목이 표시 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [Google 분석 사이트](https://www.google.com/analytics/)
- [Yahoo! 웹 분석 사이트](http://help.yahoo.com/l/us/yahoo/ywa/)
- [StatCounter 사이트](http://statcounter.com/)
