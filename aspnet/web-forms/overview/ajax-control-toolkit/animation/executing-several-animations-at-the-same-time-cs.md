---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
title: 동시에 여러 애니메이션 실행 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. Severa을 실행할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 219149e1-3ee9-4b79-8fe4-7433f6b7d15b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-several-animations-at-the-same-time-cs
msc.type: authoredcontent
ms.openlocfilehash: fe71feccbcbc4ee8e9cdc09d6220de6a53dd2d2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483971"
---
# <a name="executing-several-animations-at-the-same-time-c"></a>동시에 여러 애니메이션 실행 (C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation2CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이를 통해 여러 애니메이션을 병렬 방식으로 실행할 수 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 이를 통해 여러 애니메이션을 병렬 방식으로 실행할 수 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](executing-several-animations-at-the-same-time-cs/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample4.aspx)]

`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. 일반적으로 `<OnLoad>`는 하나의 애니메이션만 허용 합니다. 애니메이션 프레임 워크를 사용 하면 `<Parallel>` 요소를 사용 하 여 여러 애니메이션을 하나로 조인할 수 있습니다. `<Parallel>` 내의 모든 애니메이션은 동시에 실행 됩니다.

다음은 `AnimationExtender` 컨트롤에 사용할 수 있는 태그 이며, 동시에 패널을 페이드 아웃 하 고 크기를 조정 합니다.

[!code-aspx[Main](executing-several-animations-at-the-same-time-cs/samples/sample5.aspx)]

그리고 실제로이 스크립트를 실행 하면 패널이 표시 되 고 크기를 조정 하 여 (너비를 tripling 하 고 높이를 나누어) 동시에 페이드 아웃 합니다.

[패널을 페이드 아웃 하 고 크기를 조정 하는 ![(브라우저의 렌더링 엔진 덕분에 콘텐츠 포함)](executing-several-animations-at-the-same-time-cs/_static/image2.png)](executing-several-animations-at-the-same-time-cs/_static/image1.png)

패널을 페이드 아웃 하 고 크기를 조정 합니다 (브라우저의 렌더링 엔진 덕분에 콘텐츠 포함). ([전체 이미지를 보려면 클릭](executing-several-animations-at-the-same-time-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](adding-animation-to-a-control-cs.md)
> [다음](executing-several-animations-after-each-other-cs.md)
