---
uid: web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
title: 슬라이더 컨트롤 데이터 바인딩 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 현재 positio를 바인딩할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7f77869-aa1d-4025-924f-622c57112db6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/slider/databinding-the-slider-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ef547573f17f3265ad72717d3d3bbc622fd6894e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445913"
---
# <a name="databinding-the-slider-control-c"></a>슬라이더 컨트롤 데이터 바인딩(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/Slider0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/slider0CS.pdf)

> AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더의 현재 위치를 다른 ASP.NET 컨트롤에 바인딩할 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 슬라이더 컨트롤은 마우스를 사용 하 여 제어할 수 있는 그래픽 슬라이더를 제공 합니다. 슬라이더의 현재 위치를 다른 ASP.NET 컨트롤에 바인딩할 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample1.aspx)]

그런 다음 페이지에 두 개의 `TextBox` 컨트롤을 추가 합니다. 하나는 그래픽 슬라이더로 변환 되 고 다른 하나는 슬라이더의 위치를 보유 하 게 됩니다.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample2.aspx)]

다음 단계는 이미 마지막 단계입니다. ASP.NET AJAX 컨트롤 도구 키트의 `SliderExtender` 컨트롤은 첫 번째 텍스트 상자 밖의 슬라이더를 만들고 슬라이더 위치가 변경 될 때 두 번째 텍스트 상자를 자동으로 업데이트 합니다. 이 작업을 수행 하려면 `SliderExtender`의 `TargetControlID` 특성을 첫 번째 텍스트 상자의 ID로 설정 해야 합니다. `BoundControlID` 특성을 두 번째 텍스트 상자의 ID로 설정 해야 합니다.

[!code-aspx[Main](databinding-the-slider-control-cs/samples/sample3.aspx)]

브라우저에서 볼 수 있듯이 데이터 바인딩은 양방향으로 작동 합니다. 텍스트 상자에 새 값을 입력 하면 슬라이더의 위치가 업데이트 됩니다. 두 번째 텍스트 상자를 읽기 전용으로 설정 하는 경우 사용자가 해당 값을 수동으로 업데이트 하는 것이 더 어려워질 수 있도록 텍스트 필드에 weak 보호를 추가할 수 있습니다.

[![슬라이더와 텍스트 상자가 동기화 되어 있습니다.](databinding-the-slider-control-cs/_static/image2.png)](databinding-the-slider-control-cs/_static/image1.png)

슬라이더와 텍스트 상자가 동기화 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](databinding-the-slider-control-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](using-the-slider-control-with-auto-postback-cs.md)
> [다음](using-the-slider-control-with-auto-postback-vb.md)
