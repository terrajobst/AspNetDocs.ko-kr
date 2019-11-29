---
uid: web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
title: 다른 컨트롤에서 애니메이션 트리거 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 일반적으로 시작 하는 중 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5d99c2b-d8ee-413c-80d5-c120cffb0a4c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/triggering-an-animation-in-another-control-cs
msc.type: authoredcontent
ms.openlocfilehash: e0a1f8986047da04db6fde8e54b6fd0ac6ee2603
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599632"
---
# <a name="triggering-an-animation-in-another-control-c"></a>다른 컨트롤에서 애니메이션 트리거(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation8.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation8CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 일반적으로 애니메이션 시작은 동일한 컨트롤의 사용자 상호 작용에 의해 트리거됩니다. 그러나 한 컨트롤과 상호 작용 한 다음 다른 컨트롤을 애니메이션으로 사용할 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 일반적으로 애니메이션 시작은 동일한 컨트롤의 사용자 상호 작용에 의해 트리거됩니다. 그러나 한 컨트롤과 상호 작용 한 다음 다른 컨트롤을 애니메이션으로 사용할 수도 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](triggering-an-animation-in-another-control-cs/samples/sample3.css)]

패널에 대 한 애니메이션 효과를 시작 하기 위해 HTML 단추가 사용 됩니다. 사용자가 해당 단추를 클릭할 때 포스트백을 원하지 않으므로 `<input type="button" />`는 `<asp:Button />`를 통해 favoured 됩니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample4.aspx)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다. 패널의 ID (애니메이션 효과를 주는 요소)가 아니라 단추 ID (애니메이션을 트리거하는 요소)로 `TargetControlID`를 설정 하는 것이 중요 합니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample5.aspx)]

`<Animations>` 노드 내에서 애니메이션을 평소와 같이 삽입 합니다. 단추가 아니라 패널을 변경 하기 위해 `AnimationExtender`내의 모든 애니메이션 요소에 대해 `AnimationTarget` 특성을 설정 합니다. `AnimationTarget`의 값은 패널의 ID입니다. 이렇게 하면 애니메이션은 트리거 단추가 아니라 패널에서 발생 합니다. 이 시나리오에 대 한 `AnimationExtender` 태그는 다음과 같습니다.

[!code-aspx[Main](triggering-an-animation-in-another-control-cs/samples/sample6.aspx)]

개별 애니메이션이 표시 되는 특별 한 순서를 확인 합니다. 먼저 애니메이션을 실행 하면 단추가 비활성화 됩니다. `<EnableAction>` 요소에 `AnimationTarget` 특성이 없으므로이 애니메이션은 원래 컨트롤 (단추)에 적용 됩니다. 다음 두 애니메이션 단계는 병렬로 수행 해야 합니다 (`<Parallel>` 요소). 둘 다 `AnimationTarget` 특성이 `"Panel1"`로 설정 되어 있으므로 패널에 애니메이션을 적용 하는 것은 단추가 아닙니다.

[단추를 마우스 클릭 ![하면 패널 애니메이션이 시작 됩니다.](triggering-an-animation-in-another-control-cs/_static/image2.png)](triggering-an-animation-in-another-control-cs/_static/image1.png)

단추를 마우스 클릭 하면 패널 애니메이션이 시작 됩니다 ([전체 크기 이미지를 보려면 클릭](triggering-an-animation-in-another-control-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](disabling-actions-during-animation-cs.md)
> [다음](modifying-animations-from-the-server-side-cs.md)
