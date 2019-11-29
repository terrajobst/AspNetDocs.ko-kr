---
uid: web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
title: 상호 배타적인 확인란 만들기 (VB) | Microsoft Docs
author: wenz
description: 옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다. 그러나 그룹에서 하나의 라디오 단추를 선택 하면 단점이 있습니다,...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e9dd1d5a-a1db-4114-981d-6a91acb1d709
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/mutuallyexclusivecheckbox/creating-mutually-exclusive-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: f33936dd4d71f6bbf08f02966eefe44c8c152eba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606490"
---
# <a name="creating-mutually-exclusive-checkboxes-vb"></a>상호 배타적인 확인란 만들기(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/MutuallyExclusiveCheckBox0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/mutuallyexclusivecheckbox0VB.pdf)

> 옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다. 하지만 그룹에서 하나의 라디오 단추를 선택한 후에는 모든 라디오 단추를 선택 취소할 수는 없습니다. 확인란은 언제 든 지 선택 취소할 수 있지만 함께 사용할 수는 없습니다. 이 자습서에서는 두 가지 방법, 즉 함께 사용할 수 없는 확인란을 모두 제공 합니다.

## <a name="overview"></a>개요

옵션 집합 중 하나만 선택할 수 있는 경우 라디오 단추가 일반적으로 사용 됩니다. 하지만 그룹에서 하나의 라디오 단추를 선택한 후에는 모든 라디오 단추를 선택 취소할 수는 없습니다. 확인란은 언제 든 지 선택 취소할 수 있지만 함께 사용할 수는 없습니다. 이 자습서에서는 두 가지 방법, 즉 함께 사용할 수 없는 확인란을 모두 제공 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 도구 키트는 MutuallyExclusiveCheckBox extender를 포함 합니다. 이를 통해 프로그래머는 모든 확인란을 그룹 이름 (`Key` 특성)에 할당할 수 있습니다. 동일한 그룹 내의 모든 확인란은 한 번에 하나만 선택할 수 있습니다.

새 ASP.NET 페이지에 두 개의 확인란을 추가 하는 것부터 시작 해 보겠습니다. 더 많은 작업을 수행할 수 있지만 두 가지 모두 원칙을 보여 줄 수 있습니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample1.aspx)]

두 확인란 모두 MutuallyExclusiveCheckBoxExtender 컨트롤을 페이지에 배치 해야 합니다. HTML 라디오 단추 요소의 값 특성이 자신이 속한 그룹을 표시 하는 것과 동일한 경우 두 키 특성의 값은 동일 해야 합니다. Extender의 TargetControlID 속성은 확인란의 ID를 가리킵니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample2.aspx)]

마지막으로 ASP.NET AJAX 컨트롤 Toolkit의 모든 요소에 필요한 ASP.NET AJAX `ScriptManager`를 포함 합니다.

[!code-aspx[Main](creating-mutually-exclusive-checkboxes-vb/samples/sample3.aspx)]

페이지를 저장 하 고 실행 합니다. 확인란을 선택 하 고 선택 취소할 수 있지만 두 확인란을 모두 선택할 수 있습니다.

[한 번에 하나의 확인란을 확인할 수 ![.](creating-mutually-exclusive-checkboxes-vb/_static/image2.png)](creating-mutually-exclusive-checkboxes-vb/_static/image1.png)

한 번에 하나의 확인란만 확인할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-mutually-exclusive-checkboxes-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](creating-mutually-exclusive-checkboxes-cs.md)
