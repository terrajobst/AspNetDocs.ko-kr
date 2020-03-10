---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
title: 사용자 상호 작용에 대 한 응답으로 애니메이션 효과 주기 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션은 별이 될 수 있습니다 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c8204c05-ec27-40fe-933d-88e4e727a482
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-in-response-to-user-interaction-vb
msc.type: authoredcontent
ms.openlocfilehash: 629d79505cebd49c2f05333bfbf78166f80fc6cb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497927"
---
# <a name="animating-in-response-to-user-interaction-vb"></a>사용자 상호 작용에 대한 응답으로 애니메이션(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation6.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation6VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션은 자동으로 시작 되거나 사용자 상호 작용 (예: 마우스로 클릭)에 의해 트리거될 수 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션은 자동으로 시작 되거나 사용자 상호 작용 (예: 마우스로 클릭)에 의해 트리거될 수 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](animating-in-response-to-user-interaction-vb/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample4.aspx)]

`<Animations>` 노드 내에는 사용자 상호 작용을 통해 애니메이션을 시작 하는 5 가지 방법이 있습니다. 누락 된 요소는 전체 페이지가 완전히 로드 된 후 실행 되는 `<OnLoad>`입니다.

- `<OnClick>` (컨트롤에서 마우스 클릭)
- `<OnHoverOut>` (마우스가 컨트롤을 벗어납니다.)
- `<OnHoverOver>` (마우스 마우스로 컨트롤 가리키기, `<OnHoverOut>` 애니메이션 중지)
- `<OnMouseOut>` (마우스가 컨트롤을 벗어나면)
- `<OnMouseOver>` (`<OnMouseOut>` 애니메이션을 중지 하지 않고 컨트롤을 마우스로 가리키기)

이 시나리오에서는 `<OnClick>` 사용 됩니다. 사용자가 패널을 클릭 하면 크기가 조정 되 고 동시에 페이드 아웃 됩니다.

[!code-aspx[Main](animating-in-response-to-user-interaction-vb/samples/sample5.aspx)]

[마우스 클릭 ![애니메이션 시작](animating-in-response-to-user-interaction-vb/_static/image2.png)](animating-in-response-to-user-interaction-vb/_static/image1.png)

마우스 클릭으로 애니메이션 시작 ([전체 크기 이미지를 보려면 클릭](animating-in-response-to-user-interaction-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](picking-one-animation-out-of-a-list-vb.md)
> [다음](disabling-actions-during-animation-vb.md)
