---
uid: web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
title: 목록에서 애니메이션 하나 선택 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 프레임 워크도 허용 (.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 06a776fe-7c73-4ca7-8e02-5260a86edc03
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/picking-one-animation-out-of-a-list-cs
msc.type: authoredcontent
ms.openlocfilehash: 2bc203d694792716bbf4f7d7b8d152c589bf99b1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483845"
---
# <a name="picking-one-animation-out-of-a-list-c"></a>목록에서 애니메이션 하나 선택(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation5.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation5CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 프레임 워크를 사용 하면 일부 JavaScript 코드의 평가에 따라 프로그래머가 애니메이션 목록에서 하나의 애니메이션을 선택할 수 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 프레임 워크를 사용 하면 일부 JavaScript 코드의 평가에 따라 프로그래머가 애니메이션 목록에서 하나의 애니메이션을 선택할 수 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](picking-one-animation-out-of-a-list-cs/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory을 제공 하 여 페이지에 `AnimationExtender`를 추가 `runat="server":`

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample4.aspx)]

`<Animations>` 노드 내에서 `<OnLoad>`를 사용 하 여 페이지가 완전히 로드 되 면 애니메이션을 실행 합니다. `<Case>` 요소는 일반적인 애니메이션 중 하나가 아니라 재생 됩니다. 해당 SelectScript 특성의 값이 계산 됩니다. 반환 값은 숫자 여야 합니다. 이 숫자에 따라 &lt;Case&gt; 내의 subanimations 중 하나가 실행 됩니다. 예를 들어 SelectScript가 2로 계산 되는 경우 컨트롤 도구 키트는 &lt;Case&gt; 내에서 세 번째 애니메이션을 실행 합니다 (계산은 0부터 시작).

다음 태그는 세 개의 하위 애니메이션 (너비 크기 조정, 높이 크기 조정 및 페이드 아웃)을 정의 합니다. JavaScript 코드 (`Math.floor(3 * Math.random())`)는 0과 2 사이의 숫자를 선택 하 여 세 가지 애니메이션 중 하나가 실행 되도록 합니다.

[!code-aspx[Main](picking-one-animation-out-of-a-list-cs/samples/sample5.aspx)]

[가능한 세 가지 애니메이션 중 하나를 ![합니다. 즉, 패널은 더 넓어집니다.](picking-one-animation-out-of-a-list-cs/_static/image2.png)](picking-one-animation-out-of-a-list-cs/_static/image1.png)

가능한 세 가지 애니메이션 중 하나: 패널이 더 넓게 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](picking-one-animation-out-of-a-list-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](animation-depending-on-a-condition-cs.md)
> [다음](animating-in-response-to-user-interaction-cs.md)
