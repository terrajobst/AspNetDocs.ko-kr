---
uid: web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
title: UpdatePanel 컨트롤에 애니메이션 적용 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 의 내용에 대 한
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 4c306a2c-92b6-4904-b70b-365b847334fe
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animating-an-updatepanel-control-vb
msc.type: authoredcontent
ms.openlocfilehash: d66dda923940a328c0757049c9d8bfa3b2d2b9fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607103"
---
# <a name="animating-an-updatepanel-control-vb"></a>UpdatePanel 컨트롤 애니메이션(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/UpdatePanelAnimation1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/updatepanelanimation1VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. UpdatePanel의 콘텐츠에는 애니메이션 프레임 워크 (UpdatePanelAnimation)에 크게 의존 하는 특수 extender가 있습니다. 이 자습서에서는 UpdatePanel에 대해 이러한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. `UpdatePanel`콘텐츠의 경우 애니메이션 프레임 워크 (`UpdatePanelAnimation`)를 많이 사용 하는 특수 extender가 있습니다. 이 자습서에서는 `UpdatePanel`에 대 한 애니메이션을 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

첫 번째 단계는 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 하는 것입니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample1.aspx)]

이 시나리오의 애니메이션은 `UpdatePanel`에 있는 ASP.NET `Wizard` 웹 컨트롤에 적용 됩니다. 다시 게시를 트리거하기 위한 충분 한 옵션을 제공 하는 세 가지 (임의) 단계가 있습니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample2.aspx)]

`UpdatePanelAnimationExtender` 컨트롤에 필요한 태그는 `AnimationExtender`에 사용 되는 태그와 매우 비슷합니다. `TargetControlID` 특성에서 애니메이션 효과를 주는 `UpdatePanel`의 `ID`를 제공 합니다. `UpdatePanelAnimationExtender` 컨트롤 내에서 `<Animations>` 요소는 애니메이션에 대 한 XML 태그를 포함 합니다. 그러나 `AnimationExtender`에 비해 이벤트 및 이벤트 처리기의 양은 제한 됩니다. `UpdatePanels`의 경우 두 가지 중 하나만 존재 합니다.

- UpdatePanel이 업데이트 된 경우 `<OnUpdated>`
- UpdatePanel 업데이트를 시작 하는 `<OnUpdating>`

이 시나리오에서는 다시 게시 후 `UpdatePanel`의 새 콘텐츠가 페이드 인 됩니다. 이에 대 한 필수 태그는 다음과 같습니다.

[!code-aspx[Main](animating-an-updatepanel-control-vb/samples/sample3.aspx)]

이제 UpdatePanel 내에서 포스트백이 발생할 때마다 패널의 새 내용이 매끄럽게 페이드 인 됩니다.

[![다음 마법사 단계가 페이드 인 됩니다.](animating-an-updatepanel-control-vb/_static/image2.png)](animating-an-updatepanel-control-vb/_static/image1.png)

다음 마법사 단계가 페이드 인 됩니다 ([전체 크기 이미지를 보려면 클릭](animating-an-updatepanel-control-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](changing-an-animation-using-client-side-code-vb.md)
> [다음](dynamically-controlling-updatepanel-animations-vb.md)
