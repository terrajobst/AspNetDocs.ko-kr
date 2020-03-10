---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: ASP.NET 웹 페이지 (Razor) 사이트에 비디오 표시 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 Razor 구문 페이지를 사용 하 여 ASP.NET 웹 페이지에 비디오를 표시 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510383"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 비디오 표시

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 비디오 (미디어) 플레이어를 사용 하 여 사용자가 사이트에 저장 된 비디오를 볼 수 있도록 하는 방법을 설명 합니다. Razor 구문 ASP.NET 웹 페이지를 사용 하면 Flash ( *.swf*), Media Player ( *.Wmv*) 및 Silverlight ( *.xap*) 비디오를 재생할 수 있습니다.
> 
> 학습할 내용:
> 
> - 비디오 플레이어를 선택 하는 방법
> - 웹 페이지에 비디오를 추가 하는 방법
> - 비디오 플레이어 특성을 설정 하는 방법
> 
> 다음은이 문서에서 소개 하는 ASP.NET Razor 페이지 기능입니다.
> 
> - `Video` 도우미입니다.
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

## <a name="introduction"></a>소개

사이트에 비디오를 표시 하는 것이 좋습니다. 이 작업을 수행 하는 한 가지 방법은 YouTube와 같이 이미 비디오가 있는 사이트에 연결 하는 것입니다. 이러한 사이트의 비디오를 자체 페이지에 직접 포함 하려는 경우 일반적으로 사이트에서 HTML 태그를 가져온 다음 페이지에 복사할 수 있습니다. 예를 들어 다음 예제에서는 YouTube 비디오를 포함 하는 방법을 보여 줍니다.

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

자신의 웹 사이트에 있는 비디오를 재생 하려는 경우 (공용 비디오 공유 사이트가 아님) 다음과 같은 포함 태그를 사용 하 여 직접 연결할 수 없습니다. 그러나 미디어 플레이어를 페이지에서 직접 렌더링 하는 `Video` 도우미를 사용 하 여 사이트에서 비디오를 재생할 수 있습니다.

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a>비디오 플레이어 선택

비디오 파일에는 많은 형식이 있으며 각 형식에는 일반적으로 다른 플레이어와 플레이어를 구성 하는 다른 방법이 필요 합니다. ASP.NET Razor 페이지에서 `Video` 도우미를 사용 하 여 웹 페이지에서 비디오를 재생할 수 있습니다. `Video` 도우미는 웹 페이지에 비디오를 추가 하는 데 일반적으로 사용 되는 `object` 및 `embed` HTML 요소를 자동으로 생성 하므로 웹 페이지에 비디오를 포함 하는 프로세스를 간소화 합니다.

`Video` 도우미는 다음과 같은 미디어 플레이어를 지원 합니다.

- Adobe Flash
- Windows MediaPlayer
- Microsoft Silverlight

### <a name="the-flash-player"></a>플래시 플레이어

`Video` 도우미의 `Flash` 플레이어를 사용 하면 웹 페이지에서 Flash 비디오 ( *.swf* 파일)를 재생할 수 있습니다. 최소한 비디오 파일의 경로를 제공 해야 합니다. 아무 것도 지정 하지 않고 경로를 지정 하는 경우 플레이어는 현재 버전의 Flash에서 설정 된 기본값을 사용 합니다. 일반적인 기본 설정은 다음과 같습니다.

- 비디오는 기본 너비와 높이를 사용 하 여 배경색 없이 표시 됩니다.
- 페이지가 로드 되 면 비디오가 자동으로 재생 됩니다.
- 비디오는 명시적으로 중지 될 때까지 지속적으로 반복 됩니다.
- 비디오를 축소 하 여 특정 크기에 맞게 비디오를 자르는 것이 아니라 비디오를 모두 표시 합니다.
- 비디오는 창에서 재생 됩니다.

### <a name="the-mediaplayer-player"></a>MediaPlayer 플레이어

`Video` 도우미의 `MediaPlayer` 플레이어를 사용 하면 웹 페이지에서 Windows Media 비디오 ( *.wmv* 파일), windows media 오디오 ( *.wma* 파일) 및 mp3 ( *. mp3* 파일)를 재생할 수 있습니다. 재생할 미디어 파일의 경로를 포함 해야 합니다. 다른 모든 매개 변수는 선택 사항입니다. 경로만 지정 하는 경우 플레이어는 다음과 같이 현재 버전의 MediaPlayer에 설정 된 기본 설정을 사용 합니다.

- 비디오는 기본 너비와 높이를 사용 하 여 표시 됩니다.
- 페이지가 로드 되 면 비디오가 자동으로 재생 됩니다.
- 비디오가 한 번 재생 됩니다 (반복 하지 않음).
- 플레이어는 사용자 인터페이스에 컨트롤의 전체 집합을 표시 합니다.
- 비디오는 창에서 재생 됩니다.

### <a name="the-silverlight-player"></a>Silverlight 플레이어

`Video` 도우미의 `Silverlight` 플레이어를 사용 하 여 Windows Media 비디오 ( *.wmv* 파일), Windows Media 오디오 ( *.wma* 파일) 및 mp3 ( *. mp3* 파일)를 재생할 수 있습니다. Silverlight 기반 응용 프로그램 패키지 ( *.xap* 파일)를 가리키도록 path 매개 변수를 설정 해야 합니다. 또한 width 및 height 매개 변수를 설정 해야 합니다. 모든 다른 매개 변수는 선택 사항입니다. 비디오 용 Silverlight 플레이어를 사용 하는 경우 필수 매개 변수만 설정 하면 Silverlight 플레이어에서 배경색 없이 비디오를 표시 합니다.

> [!NOTE]
> Silverlight를 아직 모르는 경우: *.xap* 파일은 *.xaml* 파일의 레이아웃 지침, 어셈블리의 관리 코드 및 선택적 리소스를 포함 하는 압축 된 파일입니다. Visual Studio에서 *.xap* 파일을 Silverlight 응용 프로그램 프로젝트로 만들 수 있습니다.

`Silverlight` 비디오 플레이어는 플레이어에 대해 제공 하는 설정과 *.xap* 파일에 제공 되는 설정을 모두 사용 합니다.

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a>MIME 형식
> 
> 브라우저에서 파일을 다운로드할 때 브라우저는 파일 형식이 렌더링 되는 문서에 대해 지정 된 MIME 형식과 일치 하는지 확인할 수 있습니다. MIME 형식은 파일의 콘텐츠 형식 또는 미디어 형식입니다. `Video` 도우미는 다음과 같은 MIME 형식을 사용 합니다.
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a>플래시 (.swf) 비디오 재생

이 절차에서는 *.sample*이라는 Flash 비디오를 재생 하는 방법을 보여 줍니다. 이 절차에서는 사용자가 사이트에 *미디어* 라는 폴더를가지고 있으며 해당 폴더에 *.swf* 파일이 있다고 가정 합니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)의 설명에 따라 웹 사이트에 ASP.NET 웹 도우미 라이브러리를 추가 합니다 (아직 추가 하지 않은 경우).
2. 웹 사이트에서 페이지를 추가 하 고 이름을 *FlashVideo*로 다시 만듭니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 페이지가 표시 되 고 비디오가 자동으로 재생 됩니다. 

    ![이미지로](10-working-with-video/_static/image1.jpg "-1 ch08_video")

Flash 비디오에 대 한 `quality` 매개 변수를 `low`, `autolow`, `autohigh`, `medium`, `high`및 `best`로 설정할 수 있습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

다음과 같이 설정할 수 있는 `scale` 매개 변수를 사용 하 여 특정 크기에서 재생 되도록 플래시 비디오를 변경할 수 있습니다.

- `showall`입니다. 이렇게 하면 원래 가로 세로 비율을 유지 하면서 전체 비디오가 표시 됩니다. 그러나 각 면에 테두리가 표시 될 수 있습니다.
- `noorder`입니다. 이는 원래 가로 세로 비율을 유지 하면서 비디오를 확장 하지만 잘릴 수 있습니다.
- `exactfit`입니다. 이렇게 하면 원래 가로 세로 비율을 유지 하지 않고 전체 비디오가 표시 되지만 왜곡이 발생할 수 있습니다.

`scale` 매개 변수를 지정 하지 않으면 전체 비디오가 표시 되 고 원래 가로 세로 비율이 자르기 없이 유지 됩니다. 다음 예제에서는 `scale` 매개 변수를 사용 하는 방법을 보여 줍니다.

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

Flash player는 `windowMode`라는 비디오 모드 설정을 지원 합니다. `window`, `opaque`및 `transparent`로 설정할 수 있습니다. 기본적으로 `windowMode`은 웹 페이지의 별도 창에 비디오를 표시 하는 `window`로 설정 됩니다. `opaque` 설정은 웹 페이지의 비디오 뒤에 나오는 모든 항목을 숨깁니다. `transparent` 설정을 사용 하면 비디오의 일부가 투명 하다 고 가정 하는 웹 페이지의 배경이 비디오를 통해 표시 될 수 있습니다.

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a>MediaPlayer ( *.wmv*) 비디오 재생

다음 절차에서는 *media* 폴더에 있는 *Sample .Wmv* 라는 창 미디어 비디오를 재생 하는 방법을 보여 줍니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
2. *MediaPlayerVideo*라는 새 페이지를 만듭니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. 비디오가 자동으로 로드 되 고 재생 됩니다. 

    ![이미지로](10-working-with-video/_static/image2.jpg "-2 ch08_video")

비디오를 자동으로 재생 하는 횟수를 나타내는 정수로 `playCount`를 설정할 수 있습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

`uiMode` 매개 변수를 사용 하 여 사용자 인터페이스에 표시 되는 컨트롤을 지정할 수 있습니다. `uiMode`을 `invisible`, `none`, `mini`또는 `full`로 설정할 수 있습니다. `uiMode` 매개 변수를 지정 하지 않으면 비디오 창 뿐만 아니라 상태 창, 검색 표시줄, 컨트롤 단추 및 볼륨 컨트롤과 함께 비디오가 표시 됩니다. 플레이어를 사용 하 여 오디오 파일을 재생 하는 경우에도 이러한 컨트롤이 표시 됩니다. `uiMode` 매개 변수를 사용 하는 방법의 예는 다음과 같습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

기본적으로 오디오는 비디오가 재생 될 때 켜 있습니다. `mute` 매개 변수를 true로 설정 하 여 오디오를 음소거 할 수 있습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

`volume` 매개 변수를 0에서 100 사이의 값으로 설정 하 여 MediaPlayer 비디오의 오디오 수준을 제어할 수 있습니다. 기본값은 50입니다. 예를 들면 다음과 같습니다.

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a>Silverlight 비디오 재생

이 절차에서는 *Media*라는 폴더에 있는 Silverlight *.xap* 페이지에 포함 된 비디오를 재생 하는 방법을 보여 줍니다.

1. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
2. *SilverlightVideo*라는 새 페이지를 만듭니다.
3. 페이지에 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. 브라우저에서 페이지를 실행 합니다. 

    ![이미지로](10-working-with-video/_static/image3.jpg "-3 ch08_video")

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[Silverlight 개요](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)

[Flash 개체 및 EMBED 태그 특성](http://kb2.adobe.com/cps/127/tn_12701.html)

[Windows Media Player 11 SDK 매개 변수 태그](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)
