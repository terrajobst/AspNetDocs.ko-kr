---
uid: web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
title: 컨트롤에 애니메이션 추가 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이 자습서에서는 다음 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c120187e-963e-4439-bb85-32771bc7f1f4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/adding-animation-to-a-control-vb
msc.type: authoredcontent
ms.openlocfilehash: efaee9c1665d795dc1a889b9ac9f25dd1c08f4e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484127"
---
# <a name="adding-animation-to-a-control-vb"></a>컨트롤에 애니메이션 추가(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation1VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이 자습서에서는 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

첫 번째 단계는 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 하는 것입니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample1.aspx)]

이 시나리오의 애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스는 배경색 및 너비를 정의 합니다.

[!code-css[Main](adding-animation-to-a-control-vb/samples/sample3.css)]

다음으로 `AnimationExtender`필요 합니다. `ID` 및 일반적인 `runat="server"`를 제공한 후에는 패널에서 애니메이션 효과를 적용할 컨트롤에 `TargetControlID` 특성을 설정 해야 합니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample4.aspx)]

전체 애니메이션은 현재 Visual Studio의 IntelliSense에서 완전히 지원 되지 않는 XML 구문을 사용 하 여 선언적으로 적용 됩니다. 루트 노드는이 노드 내에 `<Animations>;` 되며, 몇 가지 이벤트를 사용 하 여 애니메이션이 적용 되는 시기를 결정할 수 있습니다.

- `OnClick` (마우스 클릭)
- `OnHoverOut` (마우스가 컨트롤을 벗어나면)
- `OnHoverOver` (마우스로 컨트롤을 가리킬 때 `OnHoverOut` 애니메이션 중지)
- `OnLoad` (페이지가 로드 된 경우)
- `OnMouseOut` (마우스가 컨트롤을 벗어나면)
- `OnMouseOver` (마우스로 컨트롤을 가리킬 때 `OnMouseOut` 애니메이션을 중지 하지 않음)

프레임 워크는 각각 자체 XML 요소로 표시 되는 애니메이션 집합과 함께 제공 됩니다. 선택 항목은 다음과 같습니다.

- `<Color>` (색 변경)
- `<FadeIn>` (페이딩)
- `<FadeOut>` (페이드 아웃)
- `<Property>` (컨트롤의 속성 변경)
- `<Pulse>` (pulsating)
- `<Resize>` (크기 변경)
- `<Scale>` (크기를 비례적으로 변경)

이 예제에서는 패널이 페이드 아웃 됩니다. 애니메이션은 1.5 초 (`Duration` 특성)를 사용 하 여 24 개의 프레임 (애니메이션 단계)/초 (`Fps` 특성)를 표시 합니다. `AnimationExtender` 컨트롤의 전체 태그는 다음과 같습니다.

[!code-aspx[Main](adding-animation-to-a-control-vb/samples/sample5.aspx)]

이 스크립트를 실행 하면 패널이 표시 되 고 1 ~ 50 초 안에 페이드 아웃 됩니다.

[패널이 페이드 아웃 된 ![](adding-animation-to-a-control-vb/_static/image2.png)](adding-animation-to-a-control-vb/_static/image1.png)

패널이 페이드 아웃 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-animation-to-a-control-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](dynamically-controlling-updatepanel-animations-cs.md)
> [다음](executing-several-animations-at-the-same-time-vb.md)
