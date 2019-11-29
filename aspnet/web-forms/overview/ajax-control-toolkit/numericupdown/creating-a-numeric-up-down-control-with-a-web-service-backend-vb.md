---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
title: 웹 서비스 백 엔드를 사용 하 여 숫자 위로/아래로 컨트롤 만들기 (VB) | Microsoft Docs
author: wenz
description: 사용자가 확인란에 값을 입력 하는 대신 Windows 및 기타 운영 체제에 있는 숫자 위로/아래로 컨트롤을 사용 하 여 더 많은 기간을 입증할 수 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: afa59dfa-fef1-43d3-8fdd-aea3be36ed3c
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-vb
msc.type: authoredcontent
ms.openlocfilehash: 2bf6e1b27180589d39e308de62b5be1f47fa8fe2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606352"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-vb"></a>웹 서비스 백 엔드를 사용하여 숫자 위로/아래로 컨트롤 만들기(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1VB.pdf)

> 사용자가 확인란에 값을 입력 하는 대신 Windows 및 기타 운영 체제에 있는 숫자 위로/아래로 컨트롤을 사용 하면 더욱 편안 하 게 입증할 수 있습니다. 기본적으로 NumericUpDown 컨트롤은 항상 값을 1 씩 늘리거나 줄일 수 있지만 웹 서비스는 더 많은 유연성을 증명 합니다.

## <a name="overview"></a>개요

사용자가 확인란에 값을 입력 하는 대신 Windows 및 기타 운영 체제에 있는 숫자 위로/아래로 컨트롤을 사용 하면 더욱 편안 하 게 입증할 수 있습니다. 기본적으로 `NumericUpDown` 컨트롤은 항상 값을 1 씩 늘리거나 줄일 수 있지만 웹 서비스는 더 많은 유연성을 증명 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 도구 키트에는 텍스트 상자에 자동으로 두 개의 단추를 추가 하는 `NumericUpDown` extender가 포함 되어 있습니다. 하나는 해당 값을 늘리기 위한 것입니다. 그러나 컨트롤은 웹 서비스 호출 (또는 페이지 메서드 호출)도 지원 합니다. 위로 또는 아래로 단추를 클릭할 때마다 JavaScript 코드는 웹 서버에 연결 하 고 여기에서 메서드를 실행 합니다. 메서드 시그니처는 다음과 같습니다.

[!code-vb[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample1.vb)]

`current` 인수는 텍스트 상자의 현재 값입니다. `tag` 특성은 `NumericUpDown` extender의 속성으로 설정할 수 있는 추가 컨텍스트 데이터입니다 (필수는 아님).

이 샘플의 경우 숫자 위로/아래로 컨트롤은 2의 거듭제곱 인 1, 2, 4, 8, 16, 32, 64 등의 값만 허용 합니다. 따라서 사용자가 값을 늘려야 할 때 실행 되는 메서드는 이전 값을 두 배로 늘려야 합니다. 다른 메서드는 값을 2로 나누려고 합니다. 다음은 전체 웹 서비스입니다.

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample2.aspx)]

마지막으로 새 ASP.NET 페이지를 만듭니다. 일반적으로 `ScriptManager` 컨트롤, `TextBox` 컨트롤 및 `NumericUpDownExtender` 컨트롤이 필요 합니다. 후자의 경우에는 웹 서비스 정보를 제공 해야 합니다.

- 다운 웹 메서드 또는 페이지 메서드의 `ServiceDownMethod` 이름
- 다운 서비스 메서드를 사용 하 여 웹 서비스에 대 한 경로를 `ServiceDownPath` 합니다. 페이지 메서드를 사용 하는 경우 생략
- `ServiceUpMethod` up 웹 메서드 또는 page 메서드의 이름입니다.
- up service 메서드를 사용 하 여 웹 서비스에 대 한 경로를 `ServiceUpPath` 합니다. 페이지 메서드를 사용 하는 경우 생략

다음은 페이지에 대 한 전체 태그입니다.

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/samples/sample3.aspx)]

페이지를 실행 하는 경우 위쪽 단추를 클릭할 때 텍스트 상자의 값이 항상 두 배가 되는 방식을 확인 하 고 아래쪽 단추를 클릭할 때 반 됩니다.

[![2의 거듭제곱 번호만 표시 됩니다.](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image1.png)

2의 거듭제곱 번호만 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-numeric-up-down-control-with-a-web-service-backend-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](creating-a-numeric-up-down-control-with-a-web-service-backend-cs.md)
