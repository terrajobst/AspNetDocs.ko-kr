---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
title: 서로 다른 여러 애니메이션 실행 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. Severa을 실행할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 21ece509-79cc-4d9d-892d-7b6e9c4d3502
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-after-each-other-vb
msc.type: authoredcontent
ms.openlocfilehash: 5034fe905299d4559b713dd841cb166886179c39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483983"
---
# <a name="executing-several-animations-after-each-other-vb"></a>여러 애니메이션을 순차적으로 실행(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation3.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation3VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이를 통해 여러 애니메이션을 차례로 실행할 수 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이를 통해 여러 애니메이션을 차례로 실행할 수 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](executing-several-animations-after-each-other-vb/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample4.aspx)]

`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 일반적으로 `<OnLoad>`는 하나의 애니메이션만 허용 합니다. 애니메이션 프레임 워크를 사용 하면 `<Sequence>` 요소를 사용 하 여 여러 애니메이션을 하나로 조인할 수 있습니다. `<Sequence>` 내의 모든 애니메이션은 그 다음에 실행 됩니다. 다음은 `AnimationExtender` 컨트롤에 사용할 수 있는 태그입니다. 먼저 패널의 너비를 높이 거 나 높이를 줄입니다.

[!code-aspx[Main](executing-several-animations-after-each-other-vb/samples/sample5.aspx)]

이 스크립트를 실행 하면 패널의 크기가 더 넓어집니다.

[처음 ![너비가 증가 합니다.](executing-several-animations-after-each-other-vb/_static/image2.png)](executing-several-animations-after-each-other-vb/_static/image1.png)

먼저 너비가 증가 합니다 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image3.png)).

[![높이가 감소 합니다.](executing-several-animations-after-each-other-vb/_static/image5.png)](executing-several-animations-after-each-other-vb/_static/image4.png)

그러면 높이가 줄어듭니다 ([전체 크기 이미지를 보려면 클릭](executing-several-animations-after-each-other-vb/_static/image6.png)).

> [!div class="step-by-step"]
> [이전](executing-several-animations-at-the-same-time-vb.md)
> [다음](animation-depending-on-a-condition-vb.md)
