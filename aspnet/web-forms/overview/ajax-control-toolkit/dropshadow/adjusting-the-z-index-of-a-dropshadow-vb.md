---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
title: DropShadow의 Z-인덱스 조정 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 그러나이 그림자는 다른 컨트롤과 충돌 하는 경우가 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ecb004b5-82c0-44fb-bcaf-233fffac6195
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/adjusting-the-z-index-of-a-dropshadow-vb
msc.type: authoredcontent
ms.openlocfilehash: 10495a9590ce1f25e9e3fa218ac5144268f50711
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497513"
---
# <a name="adjusting-the-z-index-of-a-dropshadow-vb"></a>DropShadow의 Z-인덱스 조정(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow1VB.pdf)

> AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 그러나이 그림자는 ASP.NET Menu 컨트롤과 같은 다른 컨트롤과 충돌 하는 경우도 있습니다. 메뉴 항목이 표시 되 면 드롭 그림자 뒤에 표시 됩니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 그러나이 그림자는 ASP.NET Menu 컨트롤과 같은 다른 컨트롤과 충돌 하는 경우도 있습니다. 메뉴 항목이 표시 되 면 드롭 그림자 뒤에 표시 됩니다.

## <a name="steps"></a>단계

코드는 패널 자체를 사용 하 여 시작 됩니다 효과를 표시 하는 데 충분 한 텍스트를 포함 하는 충분 한 텍스트를 포함 합니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample1.aspx)]

다른 패널은 `panelShadow` 패널 바로 앞에 배치 됩니다. 메뉴 항목이 가로 방향으로 표시 되는 메뉴를 포함 합니다. 즉, 메뉴 항목이 `dropShadow` 패널에 표시 됩니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample2.aspx)]

그런 다음, 그림자 효과를 적용 하 여 `panelShadow` 패널을 확장 하기 위해 `DropShadowExtender` 추가 됩니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample3.aspx)]

마지막으로 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하면 컨트롤 도구 키트가 작동 합니다.

[!code-aspx[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample4.aspx)]

이 스크립트를 실행 하면 패널 아래에 메뉴 항목이 표시 됩니다. 그러나이 메뉴는 `panel` CSS 클래스를 사용 하 여 요소가 다른 패널 앞에 표시 되도록 하는 두 가지 작업을 정의 하기만 하면 됩니다.

- 상대 위치 지정
- 양의 z-인덱스

[!code-css[Main](adjusting-the-z-index-of-a-dropshadow-vb/samples/sample5.css)]

그러면 `DropShadowExtender` 컨트롤이 메뉴 컨트롤과 더 이상 충돌 하지 않습니다.

[이전 ![: 메뉴 항목이 표시 되지 않습니다.](adjusting-the-z-index-of-a-dropshadow-vb/_static/image2.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image1.png)

이전: 메뉴 항목이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-vb/_static/image3.png))

[![후: 메뉴 항목이 표시 됩니다.](adjusting-the-z-index-of-a-dropshadow-vb/_static/image5.png)](adjusting-the-z-index-of-a-dropshadow-vb/_static/image4.png)

이후: 메뉴 항목이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adjusting-the-z-index-of-a-dropshadow-vb/_static/image6.png)).

> [!div class="step-by-step"]
> [이전](manipulating-dropshadow-properties-from-client-code-cs.md)
> [다음](manipulating-dropshadow-properties-from-client-code-vb.md)
