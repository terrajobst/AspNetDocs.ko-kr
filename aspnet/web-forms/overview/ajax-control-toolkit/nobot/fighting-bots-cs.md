---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: 싸 봇 (C#) | Microsoft Docs
author: wenz
description: 자동화 된 bot plaster 웹 로그 및 기타 웹 사이트를 사용 하 여 사용자 개입 없이 주석 양식을 제출 합니다. ASP.NET AJAX Con의 NoBot 컨트롤
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606431"
---
# <a name="fighting-bots-c"></a>대체 봇(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> 자동화 된 bot plaster 웹 로그 및 기타 웹 사이트를 사용 하 여 사용자 개입 없이 주석 양식을 제출 합니다. ASP.NET AJAX 컨트롤 도구 키트의 NoBot 컨트롤은 이러한 봇을 지 원하는 데 도움이 될 수 있습니다.

## <a name="overview"></a>개요

자동화 된 bot plaster 웹 로그 및 기타 웹 사이트를 사용 하 여 사용자 개입 없이 주석 양식을 제출 합니다. ASP.NET AJAX 컨트롤 도구 키트의 NoBot 컨트롤은 이러한 봇을 지 원하는 데 도움이 될 수 있습니다.

## <a name="steps"></a>단계

Bot 봇의 일반적인 방법 중 하나는 CAPTCHAs 완전히 자동화 된 Public Turing test를 사용 하 여 컴퓨터와 사람을 분리 하는 것입니다. Turing 테스트는 원래 통신 파트너가 사람이 나 컴퓨터 인지 여부를 결정 해야 하는 테스트 였습니다. 웹에서 CAPTCHA는 일반적으로 일부 문자가 비틀어 진 이미지로 구성 됩니다. 그 이유는 사람이 이미지의 문자를 읽을 수 있는 반면 OCR 알고리즘은 실패 한다는 것입니다.

이 방법에는 몇 가지 장점과 단점이 있지만이에 대 한 설명은이 자습서의 범위를 벗어나는 것입니다. 그러나 ASP.NET AJAX 컨트롤 도구 키트에는 `NoBot`유사한 방법을 제공 하는 컨트롤이 있습니다. CAPTCHA 보다 더 쉽게 극복할 수 있습니다. 그러나 대부분의 스팸 시도 `NoBot`를 방해 하는 경우 성공으로 간주 되는 블로그 등의 웹 사이트에서는 사용 하기 쉽고 정의 요금를 사용 하는 것이 좋습니다.

다음 조건 중 하나 이상이 충족 되는 경우 `NoBot`는 현재 ASP.NET 웹 폼의 포스트백을 가로챕니다.

- 브라우저에서 javascript 퍼즐을 해결 하지 못했습니다 (예를 들어 JavaScript가 비활성화 된 경우).
- 사용자가 폼을 빠르게 제출 함
- 클라이언트 IP 주소가 특정 기간 내에 너무 자주 양식을 전송 했습니다.

이러한 조건을 확인 하기 위해 `NoBot` 컨트롤에는 다음과 같은 특성이 필요 합니다 (모두 선택 사항).

- 다시 게시 사이의 최소 시간 (초)을 `ResponseMinimumDelaySeconds` 합니다.
- 한 IP의 다시 게시를 측정 하는 `CutoffWindowSeconds` 시간 간격입니다.
- 시간 간격 당 최대 시간 (초)을 `CutoffMaximumInstances` 합니다.

다음 태그는 다시 게시 사이에 최소 2 초가 경과 하 고 30 초 간격 내에 다시 게시를 5 개만 수행 하도록 요구 합니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

그런 다음 ASP.NET AJAX 라이브러리가 로드 되 고 Control Toolkit를 사용할 수 있도록 페이지에 `ScriptManager`를 포함 해야 합니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

서버 쪽에서 대부분의 검사 `NoBot` 수행 되므로 이러한 유효성 검사의 결과를 확인 해야 합니다. `NoBot`의 `IsValid()` 메서드를 호출 하 여이 작업을 수행할 수 있습니다. `NoBotState`형식의 인수 하나 (`out` 매개 변수/`ByRef` 매개 변수)가 있습니다. 해당 문자열 표현에는 확인이 실패 한 이유가 포함 되 고, 그렇지 않으면 `Valid` 있습니다. 다음 코드는 `NoBot`결과에 따라 메시지를 출력 합니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

마지막으로 제출할 폼과 메시지를 출력 하는 label 요소가 필요 합니다.

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

이 스크립트를 실행 하 고 JavaScript를 비활성화 하거나 처음 2 초 이내에 양식을 제출 하거나 30 초 이내에 폼을 7 번 전송 하면 오류 메시지가 표시 됩니다. 그러나이 컨트롤은 약 90-95%의 사용자만 JavaScript를 활성화 했기 때문에이 컨트롤을 사용 하는 것이 좋습니다. 따라서 5-10%의 사용자는 `NoBot`테스트에 실패 합니다.

[이 오류 메시지 ![봇에 의해 발생 했을 수 있습니다.](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

이 오류 메시지는 bot로 인해 발생 했을 수 있습니다 ([전체 크기 이미지를 보려면 클릭](fighting-bots-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](fighting-bots-vb.md)
