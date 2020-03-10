---
uid: web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
title: 자동 포스트백에 슬라이더 컨트롤 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더를 autopost 하 게 만들 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4d85e9fb-91e6-41f2-9c13-754549b19c27
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/using-the-slider-control-with-auto-postback-cs
msc.type: authoredcontent
ms.openlocfilehash: 785d62108667fddac42994344cde265e82aca8f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445829"
---
# <a name="using-the-slider-control-with-auto-postback-c"></a>자동 포스트백에 슬라이더 컨트롤 사용 (C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/slider1CS.pdf)

> AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 값이 변경 되 면 슬라이더를 autopostback 할 수 있습니다.

## <a name="steps"></a>단계

변경 시 슬라이더가 자동으로 다시 게시 되도록 하기 위해 두 텍스트 상자에는 `AutoPostBack="true"`특성이 필요 합니다. 슬라이더 자체가 될 텍스트 상자와 슬라이더의 위치를 포함 하는 텍스트 상자가 필요 합니다. 이에 대 한 필수 태그는 다음과 같습니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample1.aspx)]

ASP.NET AJAX 컨트롤 도구 키트의 `SliderExtender` 컨트롤은 슬라이더 기능을 두 개의 텍스트 상자에 할당 합니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample2.aspx)]

추가 레이블 요소는 나중에 다시 게시를 사용자에 게 알리는 데 사용 됩니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample3.aspx)]

마지막으로 ASP.NET AJAX의 `ScriptManager` 제어는 컨트롤 Toolkit이 작동 하는 데 필요한 JavaScript를 로드 합니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample4.aspx)]

이제 슬라이더가 다시 게시 됩니다. 서버 쪽에서이 이벤트를 catch 하 고 처리할 수 있습니다.

[!code-aspx[Main](using-the-slider-control-with-auto-postback-cs/samples/sample5.aspx)]

[슬라이더를 이동 ![포스트백이 트리거됩니다.](using-the-slider-control-with-auto-postback-cs/_static/image2.png)](using-the-slider-control-with-auto-postback-cs/_static/image1.png)

슬라이더를 이동 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-cs/_static/image3.png)).

[이후에 ![이 변경 날짜는 레이블에 기록 됩니다.](using-the-slider-control-with-auto-postback-cs/_static/image5.png)](using-the-slider-control-with-auto-postback-cs/_static/image4.png)

그런 다음이 변경 날짜는 레이블에 기록 됩니다 ([전체 크기 이미지를 보려면 클릭](using-the-slider-control-with-auto-postback-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [다음](databinding-the-slider-control-cs.md)
