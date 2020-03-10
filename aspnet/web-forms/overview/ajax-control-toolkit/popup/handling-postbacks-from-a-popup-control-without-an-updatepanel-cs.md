---
uid: web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
title: UpdatePanel을 사용 하지 않고 Popup 컨트롤에서 포스트백 처리C#() | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. Su에서 포스트백이 발생 하는 경우 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 25444121-5a72-4dac-8e50-ad2b7ac667af
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/handling-postbacks-from-a-popup-control-without-an-updatepanel-cs
msc.type: authoredcontent
ms.openlocfilehash: 9c4c59bb9dbd3e2ba2b3b81ecf76271f21673bce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496505"
---
# <a name="handling-postbacks-from-a-popup-control-without-an-updatepanel-c"></a>UpdatePanel을 사용하지 않고 팝업 컨트롤에서 포스트백 처리(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl3.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol3CS.pdf)

> AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 이러한 패널에서 포스트백이 발생 하 고 페이지에 여러 패널이 있으면 클릭 한 패널을 확인 하기가 어렵습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 이러한 패널에서 포스트백이 발생 하 고 페이지에 여러 패널이 있으면 클릭 한 패널을 확인 하기가 어렵습니다.

## <a name="steps"></a>단계

포스트백과 함께 `PopupControl`를 사용할 때 페이지에 `UpdatePanel` 없는 경우, 컨트롤 도구 키트는 팝업을 트리거한 클라이언트 요소를 확인 하는 방법을 제공 하지 않습니다 .이는 다시 게시를 발생 시킨 클라이언트 요소를 확인 하는 방법을 제공 하지 않습니다. 그러나 작은 트릭은이 시나리오에 대 한 해결 방법을 제공 합니다.

먼저, 다음은 기본 설정입니다. 두 텍스트 상자는 동일한 팝업 인 달력을 트리거합니다. 텍스트 상자와 팝업을 함께 표시 하는 두 가지 `PopupControlExtenders`입니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample1.aspx)]

기본적인 개념은 popup을 시작한 텍스트 상자를 포함 하는 &lt;`form`&gt; 요소에 숨겨진 양식 필드를 추가 하는 것입니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample2.aspx)]

페이지가 로드 되 면 JavaScript 코드는 두 텍스트 상자 모두에 이벤트 처리기를 추가 합니다. 사용자가 텍스트 상자를 클릭할 때마다 숨겨진 폼 필드에 해당 이름이 기록 됩니다.

[!code-html[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample3.html)]

서버 쪽 코드에서 숨김 필드의 값을 읽어야 합니다. 숨겨진 양식 필드는 조작 하기는 쉽지 않으므로 숨겨진 값의 유효성을 검사 하는 허용 목록 접근 방식이 필요 합니다. 올바른 텍스트 상자를 확인 한 후에는 달력의 날짜가 해당 텍스트 상자에 기록 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/samples/sample4.aspx)]

[사용자가 텍스트 상자를 클릭할 때 달력이 표시 되는 ![](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image2.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image1.png)

사용자가 텍스트 상자를 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image3.png)).

[날짜를 클릭 ![텍스트 상자에 배치 됩니다.](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image5.png)](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image4.png)

날짜를 클릭 하면 텍스트 상자에 배치 됩니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-popup-control-without-an-updatepanel-cs/_static/image6.png)).

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
> [다음](using-multiple-popup-controls-vb.md)
