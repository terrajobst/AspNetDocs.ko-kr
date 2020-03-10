---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 웹 페이지 Twitter 도우미 | Microsoft Docs
author: Rick-Anderson
description: 이 항목 및 응용 프로그램에서는 WebMatrix 3 프로젝트에 Twitter 도우미를 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미를 호출 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518621"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>ASP.NET 웹 페이지와 Twitter 도우미

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Twitter 도우미는 사용 되지 않습니다. 웹 사이트용 Twitter의 최신 engagement 도구는 [웹 사이트에 대 한 Twitter 개요](https://developer.twitter.com/en/docs/twitter-for-websites/overview)를 참조 하세요.

> 이 항목 및 응용 프로그램에서는 WebMatrix 3 프로젝트에 Twitter 도우미를 추가 하는 방법을 보여 줍니다. Twitter 도우미 코드를 포함 하 고 도우미 메서드를 호출 하는 방법을 보여 줍니다.
> 
> Tian 파일에 대 한이 코드는 Microsoft의 **이동** 에 의해 개발 되었습니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

## <a name="introduction"></a>소개

이 항목에서는 응용 프로그램에 Twitter 도우미를 추가 하 고 Razor 구문를 사용 하 여 도우미 메서드를 호출 하는 방법을 보여 줍니다. Twitter 도우미를 사용 하면 응용 프로그램에 Twitter 단추와 위젯을 쉽게 통합할 수 있습니다. 사용자의 타임 라인 또는 해시 태그에 대 한 검색 결과와 같은 Twitter 위젯을 사용 하려면 먼저 [twitter에서 위젯을](https://twitter.com/settings/widgets)만들어야 합니다. 위젯을 만든 후에는 위젯 id를 받게 됩니다. 위젯을 표시 하는 도우미 메서드를 호출할 때이 위젯 id를 매개 변수로 전달 합니다.

이 항목은 Twitter API 버전 1.1에 대해 작성 되었습니다. Twitter API가 변경 되 면 프로젝트에 Twitter 도우미 코드를 직접 추가 하 여 도우미 코드를 업데이트할 수 있습니다.

WebMatrix 설치에 대 한 자세한 내용은 [ASP.NET 웹 페이지 2 소개-시작 하기](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)를 참조 하세요.

## <a name="add-twitter-helper-to-your-project"></a>프로젝트에 Twitter 도우미 추가

Twitter 도우미를 추가 하려면 먼저 **App\_Code** 라는 폴더를 프로젝트에 추가 합니다. 그런 다음 **Twitter. cshtml**라는 파일을 만듭니다.

![App_Code 폴더](twitter-helper/_static/image1.png)

Twitter의 기본 코드를 다음 코드로 바꿉니다.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>웹 페이지에서 Twitter 메서드를 호출 합니다.

다음 예제에서는 프로젝트의 페이지에서 Twitter 도우미 메서드를 사용 하는 방법을 보여 줍니다. 프로젝트에서 매개 변수 값을 요구 사항과 관련 된 값으로 바꿀 수 있습니다. 제공 된 위젯 id를 사용 하 여 메서드의 작동 방식을 탐색할 수 있지만 프로젝트의 위젯을 직접 생성할 수 있습니다.

아래에 표시 된 매개 변수 중 일부가 필요 하지 않습니다. 선택적 매개 변수는 단추 또는 위젯이 표시 되는 방식을 사용자 지정 하는 데 사용 됩니다. 예를 들어 팔 로우 단추를 사용 하려면 사용자 이름만 입력 하면 됩니다. 그러나이 예에서는 팔로 워 수를 포함 하는 방법 및 단추와 언어의 크기를 지정 하는 방법을 보여 줍니다.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>결과 확인

위의 코드는 다음과 같은 단추 및 위젯을 생성 합니다. 이러한 단추와 위젯은 스크린샷이 아닌 완벽 하 게 작동 합니다. Language 매개 변수가 **es**로 설정 되었으므로 다음 단추가 스페인어로 표시 됩니다.

### <a name="follow-button"></a>팔 로우 단추

[@aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>트 윗 단추

[트 윗](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="user-timeline-profile"></a>사용자 타임 라인 (프로필)

[트 윗 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>즐겨찾기

[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 즐겨찾기 트 윗](https://twitter.com/Microsoft/favorites)

### <a name="list"></a>목록

[@Microsoft/MS\_소비자\_밴드에서 트 윗](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>검색

[&quot;#asp .net&quot;에 대 한 트 윗](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`
