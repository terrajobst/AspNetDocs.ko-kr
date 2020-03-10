---
uid: web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
title: JavaScript에서 패널 축소 및 확장 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 확장 하는 기능을 제공 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: de5500be-75e5-461a-8064-b70ae52ea6a4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/collapsiblepanel/collapsing-and-expanding-a-panel-from-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: bed14d82394d28336493bec10e31ddb4d411a192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497717"
---
# <a name="collapsing-and-expanding-a-panel-from-javascript-c"></a>JavaScript에서 패널 축소 및 확장(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/8/a/a/8aab3c3e-de6f-463f-805c-5fda567eef6e/CollapsiblePanel1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/collapsiblepanel1CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 다시 확장할 수 있는 기능을 제공 합니다. 이러한 두 작업은 사용자 지정 JavaScript 코드에서 트리거될 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 CollapsiblePanel 컨트롤은 패널을 확장 하 고 콘텐츠를 축소 하 고 다시 확장할 수 있는 기능을 제공 합니다. 이러한 두 작업은 사용자 지정 JavaScript 코드에서 트리거될 수도 있습니다.

## <a name="steps"></a>단계

먼저 새 ASP.NET 페이지를 만들고 하나의 `<form>` 요소 내에 `ScriptManager`를 포함 합니다. 그러면 컨트롤 도구 키트에 필요한 ASP.NET AJAX 라이브러리가 로드 됩니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample1.aspx)]

그런 다음 축소/확장 효과를 볼 수 있도록 몇 가지 텍스트가 포함 된 패널을 만듭니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample2.aspx)]

여기에서 볼 수 있듯이 패널은 여기에 표시 되는 CSS 클래스를 참조 합니다. 기본적으로 배경색과 패널의 너비를 정의 합니다.

[!code-css[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample3.css)]

`CollapsiblePanelExtender` 컨트롤에는 `TargetControlID` 특성이 필요 하므로 toolkit에서 요청 시 축소 하거나 확장할 패널을 알 수 있습니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample4.aspx)]

아쉽게도 extender는 현재 패널을 축소 하거나 확장 하기 위한 특정 API를 노출 하지 않지만 일부 문서화 되지 않은 메서드는이 작업을 수행 합니다. 먼저 페이지에 세 개의 HTML 단추를 추가 합니다. 그러면이 페이지에 클라이언트 쪽 JavaScript를 트리거하여 패널의 내용을 축소 하거나 확장 합니다.

[!code-aspx[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample5.aspx)]

클라이언트 쪽 JavaScript 코드 (`<script type="text/javascript">`시작)에서는 `$find()` 메서드를 사용 하 여 `CollapsiblePanelExtender`에 액세스 해야 합니다. `$find("cpe")`은이에 대 한 참조를 반환 합니다. 여기서 특정 메서드는 현재 작업을 해결 합니다.

패널을 열기 (확장) 하는 메서드를 `_doOpen()`이라고 합니다. 다음 코드는 첫 번째 단추를 클릭할 때 호출 되는 `doOpen()` 함수를 구현 합니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample6.js)]

패널을 닫거나 축소 하려면 `_doClose()` 메서드를 실행 해야 합니다. 따라서 사용자가 두 번째 단추를 클릭 하면 다음 JavaScript 코드가 호출 됩니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample7.js)]

세 번째 단추는 패널의 상태를 축소 됨에서 확장 됨으로 전환 하 고 그 반대의 경우도 마찬가지입니다. `CollapsiblePanelExtender`는이 패널의 상태를 반대로 하는 `toggle()` 메서드를 노출 합니다. 그러나 `toggle()` 메서드에서 내부적으로 사용 하는 다른 방법도 있습니다. `CollapsiblePanelExtender()`의 `get_Collapsed()` 메서드는 패널이 축소 되었는지 여부를 알려 줍니다. 이 함수의 반환 값에 따라 패널은 확장 (`_doOpen()` 메서드) 또는 축소 (`_doClose()`) 메서드 중 하나가 됩니다.

[!code-javascript[Main](collapsing-and-expanding-a-panel-from-javascript-cs/samples/sample8.js)]

[세 번째 단추가 ![패널의 상태를 축소 됨에서 확장 후 뒤로 변경 합니다.](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image2.png)](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image1.png)

세 번째 단추는 패널의 상태를 축소 됨에서 확장 됨과 뒤로 변경 ([전체 크기 이미지를 보려면 클릭](collapsing-and-expanding-a-panel-from-javascript-cs/_static/image3.png)) 합니다.

> [!div class="step-by-step"]
> [다음](collapsing-and-expanding-a-panel-from-javascript-vb.md)
