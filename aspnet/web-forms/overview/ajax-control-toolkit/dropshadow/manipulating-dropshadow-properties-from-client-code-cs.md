---
uid: web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
title: 클라이언트 코드에서 DropShadow 속성 조작 (C#) | Microsoft Docs
author: wenz
description: DataList의 편집 인터페이스 사용자 지정
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c83ca3e6-c0bf-4158-a166-40c1ab0f33da
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dropshadow/manipulating-dropshadow-properties-from-client-code-cs
msc.type: authoredcontent
ms.openlocfilehash: 790f0d881e43518600968d6c175d4eaa53d0e5f9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574074"
---
# <a name="manipulating-dropshadow-properties-from-client-code-c"></a>클라이언트 코드에서 DropShadow 속성 조작(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/5/1/6/51652a81-500b-4f6b-88d3-617103e7941e/DropShadow2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dropshadow2CS.pdf)

> AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 DropShadow 컨트롤은 그림자가 있는 패널을 확장 합니다. 클라이언트 JavaScript 코드를 사용 하 여이 extender의 속성을 변경할 수도 있습니다.

## <a name="steps"></a>단계

코드는 일부 텍스트 줄이 포함 된 패널로 시작 합니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample1.aspx)]

연결 된 CSS 클래스는 패널에 멋진 배경색을 제공 합니다.

[!code-css[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample2.css)]

그림자 효과, 불투명도가 50%로 설정 된 패널을 확장 하는 `DropShadowExtender` 추가 됩니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample3.aspx)]

그런 다음 ASP.NET AJAX `ScriptManager` 컨트롤을 사용 하 여 컨트롤 도구 키트가 작동 하도록 합니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample4.aspx)]

다른 패널에는 그림자의 불투명도를 설정 하기 위한 두 가지 JavaScript 링크가 있습니다. 빼기 링크는 그림자의 불투명도를 줄이고 더하기 링크를 통해이를 늘립니다.

[!code-aspx[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample5.aspx)]

그러면 JavaScript 함수 `changeOpacity()` 먼저 페이지에서 `DropShadowExtender` 컨트롤을 찾아야 합니다. ASP.NET AJAX는 정확히 해당 작업에 대 한 `$find()` 메서드를 정의 합니다. 그런 다음 `get_Opacity()` 메서드는 현재 불투명도를 검색 하 고 `set_Opacity()` 메서드는이를 설정 합니다. JavaScript 코드는 현재 불투명도 값을 `<label>` 요소에 배치 합니다.

[!code-html[Main](manipulating-dropshadow-properties-from-client-code-cs/samples/sample6.html)]

[클라이언트 쪽에서 불투명도가 변경 ![](manipulating-dropshadow-properties-from-client-code-cs/_static/image2.png)](manipulating-dropshadow-properties-from-client-code-cs/_static/image1.png)

클라이언트 쪽에서 불투명도가 변경 됩니다 ([전체 크기 이미지를 보려면 클릭](manipulating-dropshadow-properties-from-client-code-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](adjusting-the-z-index-of-a-dropshadow-cs.md)
> [다음](adjusting-the-z-index-of-a-dropshadow-vb.md)
