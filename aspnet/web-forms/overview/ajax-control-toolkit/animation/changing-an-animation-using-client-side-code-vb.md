---
uid: web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
title: 클라이언트 쪽 코드를 사용 하 여 애니메이션 변경 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션을 사용할 수도 있습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a7fe5de5-a964-4780-ae5e-70821dfb50a0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/changing-an-animation-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: cce0a5a901f71edd40eada59ac7eeba93222e2b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78430991"
---
# <a name="changing-an-animation-using-client-side-code-vb"></a>클라이언트 쪽 코드를 사용하여 애니메이션 변경(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation11.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation11VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션을 변경할 수도 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](changing-an-animation-using-client-side-code-vb/samples/sample3.css)]

실제 애니메이션은 HTML 단추를 통해 시작 됩니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample4.aspx)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.

[!code-aspx[Main](changing-an-animation-using-client-side-code-vb/samples/sample5.aspx)]

`AnimationExtender` 컨트롤 내에 `<Animations>` 노드가 없습니다. 사용자 지정 JavaScript 코드는 컨트롤과 함께 사용 되는 애니메이션을 제공 하는 데 사용 됩니다.

`AnimationExtender`의 서버 API와 마찬가지로 extender에 아직 애니메이션을 할당 하는 쉬운 방법은 없습니다. 그러나 extender는 다양 한 이벤트 (`OnClick`, `OnLoad`등)에 등록 된 애니메이션을 읽고 쓰는 여러 메서드를 노출 합니다. 예를 들어 다음과 같은 노래를 선택할 수 있다.

- `get_OnClick()`
- `set_OnClick()`
- `get_OnLoad()`
- `set_OnLoad()`
- `...`

`get_*()` 함수의 반환 값 형식 및 `set_*()` 함수에 대 한 인수 형식은 JSON 문자열이 며 XML 태그가 무엇 인지에 대 한 개체 표현을 제공 합니다. 현재에서는 개체를 전달할 방법이 없지만 지정 된 애니메이션 (`get_OnXXXBehavior()` 메서드)에서 개체를 읽을 수 있습니다.

다음은 단추에 의해 트리거되는 애니메이션을 나타내는 JSON 문자열 (구분 기호를 사용 하 여 깔끔하게 형식이 지정 되지 않음)이 고, 패널 크기를 조정 하 여 패널에 애니메이션을 적용 하 고 동시에 페이드 아웃 하는 것입니다.

[!code-json[Main](changing-an-animation-using-client-side-code-vb/samples/sample6.json)]

다음 JavaScript 코드는이 JSON descripting을 현재 extender의 `OnClick` 애니메이션에 할당 하 고 실행 합니다.

[!code-html[Main](changing-an-animation-using-client-side-code-vb/samples/sample7.html)]

[마우스를 클릭 하지 않고 매우 작은 태그를 사용 하 여 애니메이션이 즉시 실행 ![](changing-an-animation-using-client-side-code-vb/_static/image2.png)](changing-an-animation-using-client-side-code-vb/_static/image1.png)

애니메이션은 마우스 클릭 없이 (또는 매우 작은 태그를 사용 하 여) 즉시 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](changing-an-animation-using-client-side-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](executing-animations-using-client-side-code-vb.md)
> [다음](animating-an-updatepanel-control-vb.md)
