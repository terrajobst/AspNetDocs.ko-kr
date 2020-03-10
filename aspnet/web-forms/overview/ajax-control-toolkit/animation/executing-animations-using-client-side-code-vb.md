---
uid: web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
title: 클라이언트 쪽 코드를 사용 하 여 애니메이션 실행 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션 실행 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f7073f50-d765-456d-9957-926ce60f35f6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/executing-animations-using-client-side-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 7ef36900d20d8d07c3c6f3b63ce96568a377a0ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484007"
---
# <a name="executing-animations-using-client-side-code-vb"></a>클라이언트 쪽 코드를 사용하여 애니메이션 실행(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation10.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation10VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행을 트리거할 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 애니메이션 실행을 트리거할 수도 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](executing-animations-using-client-side-code-vb/samples/sample3.css)]

그런 다음 `ID`, `TargetControlID` 특성 및 obligatory `runat="server"`를 제공 하 여 페이지에 `AnimationExtender`를 추가 합니다.

[!code-aspx[Main](executing-animations-using-client-side-code-vb/samples/sample4.aspx)]

`<Animations>` 노드 내에서 `<OnClick>`를 사용 하 여 사용자가 패널을 클릭 하면 애니메이션을 실행 합니다. 병렬로 실행 되는 두 개의 애니메이션을 추가 합니다.

[!code-xml[Main](executing-animations-using-client-side-code-vb/samples/sample5.xml)]

데모용으로이 애니메이션 및 컨트롤 도구 키트를 사용 하 여 만든 다른 모든 애니메이션은 페이지가 실행 되 면 JavaScript 코드를 사용 하 여 실행 됩니다. 먼저 `AnimationExtender` 컨트롤에 액세스할 수 있어야 합니다. ASP.NET AJAX 라이브러리는이 작업에 대 한 `$find()` 함수를 제공 합니다.

[!code-csharp[Main](executing-animations-using-client-side-code-vb/samples/sample6.cs)]

`AnimationExtender` 컨트롤은 XML 태그에 사용 되는 이벤트 처리기와 동일한 이름을 가진 메서드 (`OnClick()`, `OnLoad()`등)를 포함 하 여 다양 한 API를 노출 합니다. 예를 들어 `OnClick()` 메서드 호출은 `AnimationExtender` 컨트롤의 `<OnClick>` 요소 내에서 애니메이션을 실행 합니다.

[!code-javascript[Main](executing-animations-using-client-side-code-vb/samples/sample7.js)]

페이지가 완전히 로드 된 후 패널의 클릭을 에뮬레이트하는 전체 클라이언트 쪽 JavaScript 코드는 페이지와 포함 된 모든 JavaScript 라이브러리가 로드 된 후 ASP.NET AJAX에 의해 호출 되는 `pageLoad()` 함수 이름이 사용 됨을 확인 합니다.

[!code-html[Main](executing-animations-using-client-side-code-vb/samples/sample8.html)]

[마우스를 클릭 하지 않고 애니메이션이 즉시 실행 ![](executing-animations-using-client-side-code-vb/_static/image2.png)](executing-animations-using-client-side-code-vb/_static/image1.png)

마우스 클릭 없이 애니메이션이 즉시 실행 됩니다 ([전체 크기 이미지를 보려면 클릭](executing-animations-using-client-side-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](modifying-animations-from-the-server-side-vb.md)
> [다음](changing-an-animation-using-client-side-code-vb.md)
