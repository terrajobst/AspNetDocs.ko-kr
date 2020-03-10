---
uid: web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
title: 조건에 따른 애니메이션 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션의 여부입니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b7a28c0d-efb9-443a-80a4-1a5ee54671cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/animation-depending-on-a-condition-cs
msc.type: authoredcontent
ms.openlocfilehash: 476b0cf80fa7c04cd8b8f9a92060ddabb9d14c13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484169"
---
# <a name="animation-depending-on-a-condition-c"></a>조건에 따른 애니메이션(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation4.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation4CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션의 실행 여부는 일부 JavaScript 코드 형식의 조건에 따라서도 달라질 수 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션의 실행 여부는 일부 JavaScript 코드 형식의 조건에 따라서도 달라질 수 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](animation-depending-on-a-condition-cs/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample4.aspx)]

`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. `<Condition>` 요소는 일반적인 애니메이션 중 하나가 아니라 재생 됩니다. `ConditionScript` 특성의 값으로 제공 되는 JavaScript 코드는 런타임에 실행 됩니다. True로 평가 되 면 애니메이션이 실행 되 고, 그렇지 않으면가 실행 되지 않습니다. 다음 태그는 두 개의 애니메이션을 제공 하며, 각 애니메이션은 무작위으로 50%의 사례에서 실행 됩니다. `<OnLoad>`내에는 애니메이션이 하나만 있을 수 있으므로 `<Sequence>` 요소를 사용 하 여 두 `<Condition>` 애니메이션이 함께 조인 됩니다.

[!code-aspx[Main](animation-depending-on-a-condition-cs/samples/sample5.aspx)]

`ConditionScript` 특성에서 보다 작음 부호 (`<`)는 이스케이프 되어야 합니다 (). 이 스크립트를 실행 하는 경우 애니메이션을 실행 하지 않거나 둘 중 하나 또는 둘 다 수행 합니다.

[패널의 크기를 조정 하지 않고 페이드 아웃 하면 두 번째 애니메이션이 실행 되므로 첫 번째 애니메이션이 실행 되지 않는 ![](animation-depending-on-a-condition-cs/_static/image2.png)](animation-depending-on-a-condition-cs/_static/image1.png)

패널은 크기를 조정 하지 않고 페이드 아웃 되기 때문에 첫 번째 애니메이션이 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](animation-depending-on-a-condition-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](executing-several-animations-after-each-other-cs.md)
> [다음](picking-one-animation-out-of-a-list-cs.md)
