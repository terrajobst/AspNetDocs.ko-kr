---
uid: web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
title: 애니메이션 중 작업 비활성화 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 작업을 지원 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a86c0276-6481-46ee-8b4f-8c2009399ee9
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/disabling-actions-during-animation-vb
msc.type: authoredcontent
ms.openlocfilehash: 4924d4f70099255b930d53f6a72e810be7a47485
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606831"
---
# <a name="disabling-actions-during-animation-vb"></a>애니메이션 중에 작업 사용 안 함(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation7.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation7VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 마우스 클릭과 같은 동작을 지원 합니다. 그러나 마우스 클릭으로 애니메이션을 시작 하는 경우 애니메이션 중 마우스 클릭을 사용 하지 않도록 설정 하는 것이 좋습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 또한 마우스 클릭과 같은 동작을 지원 합니다. 그러나 마우스 클릭으로 애니메이션을 시작 하는 경우 애니메이션 중 마우스 클릭을 사용 하지 않도록 설정 하는 것이 좋습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 HTML 단추에 적용 됩니다.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample2.aspx)]

단추를 사용 하 여 포스트백을 만들지 않기 때문에 웹 컨트롤 대신 HTML 컨트롤을 사용 합니다. 클라이언트 쪽 애니메이션을 시작 하기만 하면 됩니다.

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample3.aspx)]

`<Animations>` 노드 내에서 `<OnClick>` 마우스 클릭을 처리할 올바른 요소입니다. 그러나 애니메이션을 수행 하는 동안에도 단추를 클릭할 수 있습니다. `<EnableAction>` 요소는이를 처리할 수 있습니다. `Enabled="false"`를 설정 하면 애니메이션의 일부로 단추가 사용 되지 않습니다. 여러 개별 애니메이션 (단추 및 실제 애니메이션 사용 안 함)을 사용 하 고 있으므로 단일 애니메이션을 하나로 붙이려면 `<Parallel>` 요소가 필요 합니다. `AnimationExtender`에 대 한 전체 태그는 다음과 같습니다.

[!code-aspx[Main](disabling-actions-during-animation-vb/samples/sample4.aspx)]

목록의 끝에 있는 다음 XML 요소를 사용 하 여 애니메이션 뒤에 단추를 다시 사용 하도록 설정할 수도 있습니다.

[!code-xml[Main](disabling-actions-during-animation-vb/samples/sample5.xml)]

그러나 지정 된 시나리오에서는 단추가 페이드 아웃 되어 애니메이션의 끝에 표시 되지 않으므로이는 쓸모가 없습니다.

[![애니메이션이 실행 되는 즉시 단추를 사용할 수 없습니다.](disabling-actions-during-animation-vb/_static/image2.png)](disabling-actions-during-animation-vb/_static/image1.png)

애니메이션을 실행 하는 즉시 단추를 사용할 수 없습니다 ([전체 크기 이미지를 보려면 클릭](disabling-actions-during-animation-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](animating-in-response-to-user-interaction-vb.md)
> [다음](triggering-an-animation-in-another-control-vb.md)
