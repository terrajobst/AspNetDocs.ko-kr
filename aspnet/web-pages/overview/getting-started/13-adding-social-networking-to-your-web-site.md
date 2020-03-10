---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: ASP.NET 웹 페이지 (Razor) 사이트에 소셜 네트워킹 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 소셜 네트워킹 서비스와 사이트를 통합 하는 방법에 대해 설명 합니다. 이 장에서 사용자는 웹 사이트에 책갈피를 지정 하 고 연결 하는 방법을 배웁니다.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422957"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에 소셜 네트워킹 추가

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET 웹 페이지 (Razor) 웹 사이트의 페이지에 Facebook, Twitter, Reddit 및 Digg에 대 한 소셜 네트워킹 링크를 추가 하는 방법과 Twitter 피드, Xbox 게이머 카드 및 Gravatar 이미지를 포함 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - 사용자가 사이트에 책갈피를 지정 하 고 연결 하도록 하는 방법입니다.
> - Twitter 피드를 추가 하는 방법
> - 페이지에 Facebook **Like** 단추를 추가 하는 방법입니다.
> - Gravatar.com 이미지를 렌더링 하는 방법입니다.
> - 사이트에서 Xbox 게이머 카드를 표시 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - ASP.NET 웹 도우미 라이브러리 (NuGet 패키지)
>   
> 
> 이 자습서는 ASP.NET 웹 도우미 라이브러리를 사용 하는 파트를 제외 하 고는 ASP.NET 웹 페이지 3 에서도 작동 합니다.

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>소셜 네트워킹 사이트에서 웹 사이트 연결

사용자가 사이트에서 무언가를 사용 하는 경우 친구와 공유 하는 경우가 많습니다. 사용자가 클릭 하 여 Digg, Reddit, Facebook, Twitter 또는 유사한 사이트의 페이지를 공유할 수 있는 문자 모양 (아이콘)을 표시 하 여이 작업을 쉽게 수행할 수 있습니다.

이러한 문자 모양을 표시 하려면 페이지에 `LinkSharecode` 도우미를 추가 합니다. 페이지를 방문 하는 사람은 개별 문자 모양을 클릭할 수 있습니다. 해당 소셜 네트워킹 사이트의 계정이 있는 경우 해당 사이트의 페이지에 대 한 링크를 게시할 수 있습니다.

![그림 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).- *listlinkshare. cshtml* 라는 페이지를 만들고 다음 태그를 추가 합니다.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    이 예에서는 `LinkShare` 도우미가 실행 될 때 페이지 제목이 매개 변수로 전달 되 고이는 페이지 제목을 소셜 네트워킹 사이트에 전달 합니다. 그러나 원하는 모든 문자열을 전달할 수 있습니다. 또한이 예제에서는 목록에 포함할 소셜 네트워킹 사이트를 지정 합니다. 사이트와 관련 된 소셜 네트워킹 사이트를 지정할 수 있습니다.
2. 브라우저에서 *Listlinkshare. cshtml* 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.)
3. 등록 한 사이트 중 하나에 대 한 문자 모양을 클릭 합니다. 링크를 누르면 링크를 공유할 수 있는 선택한 소셜 네트워크 사이트의 페이지로 이동 합니다. 예를 들어 Reddit 링크를 클릭 하면 Reddit 웹 사이트의 `submit to reddit` 페이지로 이동 합니다.

     ![그림 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>Twitter 피드 추가

Twitter API의 현재 버전과 호환 되는 Twitter 도우미를 사용 하는 방법에 대 한 자세한 내용은 [twitter 도우미](../ui-layouts-and-themes/twitter-helper.md)를 참조 하세요. 이 예제에서는 여러 페이지의 코드를 쉽게 다시 사용할 수 있도록 자체 도우미를 작성 하는 방법을 보여 줍니다.

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>&quot; 단추와 같은 Facebook &quot;표시

경우에 따라 도우미에 의존 하지 않고 소셜 네트워킹 공급자에서 직접 코드를 가져오는 것이 가장 좋습니다. 이는 소셜 네트워크 공급자가 도우미가 업데이트 되는 것 보다 더 빠르게 해당 옵션을 업데이트 하는 경우에 특히 그렇습니다.

사이트에 Facebook 기능 (예: Like 단추)을 추가 하려면 [developers.facebook.com](https://developers.facebook.com/) 사이트에서 코드 조각을 검색할 수 있습니다. Facebook 사이트에서 해당 도구를 사용 하 여 사이트와 관련 된 코드 조각을 생성 합니다.

다음 강조 표시 된 코드는 developers.facebook.com 사이트의 유사 단추 도구에서 검색 된 코드입니다. 사용자 고유의 앱 ID를 제공 해야 합니다.

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Gravatar 이미지 렌더링

*Gravatar* (전 세계적으로 인식 되는 아바타&quot;)는 여러 웹 사이트에서 아바타 &#8212; &quot;(사용자를 나타내는 이미지)로 사용할 수 있는 이미지입니다. 예를 들어 Gravatar는 포럼 게시물, 블로그 설명 등의 사람을 식별할 수 있습니다. [http://www.gravatar.com/](http://www.gravatar.com/)의 Gravatar 웹 사이트에서 자신의 Gravatar를 등록할 수 있습니다. 웹 사이트의 사용자 이름 또는 전자 메일 주소 옆에 이미지를 표시 하려면 Gravatar 도우미를 사용할 수 있습니다.

이 예제에서는 자신을 나타내는 단일 Gravatar를 사용 합니다. Gravatar를 사용 하는 또 다른 방법은 사용자가 사이트에 등록할 때 Gravatar 주소를 지정할 수 있도록 하는 것입니다. (사용자가 [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격을 추가](https://go.microsoft.com/fwlink/?LinkId=202904)하도록 등록 하는 방법을 알아볼 수 있습니다.) 그런 다음 해당 사용자에 대 한 정보를 표시할 때마다 사용자 이름을 표시 하는 위치에 Gravatar를 추가할 수 있습니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
2. *Gravatar*라는 새 웹 페이지를 만듭니다.
3. 파일에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    `Gravatar.GetHtml` 메서드는 페이지에 Gravatar 이미지를 표시 합니다. 이미지의 크기를 변경 하려면 숫자를 두 번째 매개 변수로 포함 하면 됩니다. 기본 크기는 80입니다. 80 보다 작은 숫자는 이미지를 더 작게 만듭니다. 80 보다 큰 숫자는 이미지를 더 크게 만듭니다.
4. `Gravatar.GetHtml` 메서드에서 `<Your Gravatar account here>`을 Gravatar 계정에 사용 하는 전자 메일 주소로 바꿉니다. Gravatar 계정이 없는 경우에는 사용자의 전자 메일 주소를 사용할 수 있습니다.
5. 브라우저에서 페이지를 실행 합니다. 이 페이지에는 지정한 전자 메일 주소에 대 한 두 개의 Gravatar 이미지가 표시 됩니다. 두 번째 이미지는 첫 번째 이미지 보다 작습니다. 

    ![그림 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Xbox 게이머 카드 표시

사용자가 Microsoft Xbox 게임을 온라인으로 재생 하는 경우 각 사용자에 게는 고유한 ID가 있습니다. 통계는 각 플레이어에 대해 평판, 게이머 점수 및 최근에 재생 된 게임을 보여 주는 게이머 카드 형식으로 유지 됩니다. Xbox 게이머 라면 `GamerCard` 도우미를 사용 하 여 사이트의 페이지에 게이머 카드를 표시할 수 있습니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
2. *Xboxgamer. cshtml* 이라는 새 페이지를 만들고 다음 태그를 추가 합니다.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    `GamerCard.GetHtml` 속성을 사용 하 여 표시할 게이머 카드의 별칭을 지정 합니다.
3. 브라우저에서 페이지를 실행 합니다. 지정 된 Xbox 게이머 카드가 페이지에 표시 됩니다.

    ![그림 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
