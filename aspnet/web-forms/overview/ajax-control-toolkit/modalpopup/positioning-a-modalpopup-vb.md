---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
title: ModalPopup 위치 지정 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤은 다음을 제공 하지 않습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 8a07210c-eb0e-485e-9ee8-82a101520e65
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/positioning-a-modalpopup-vb
msc.type: authoredcontent
ms.openlocfilehash: fb79a08a339588ed8adc4b4236911819ea9286b4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496895"
---
# <a name="positioning-a-modalpopup-vb"></a>ModalPopup 위치 지정(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup4.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup4VB.pdf)

> AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤은 팝업을 배치 하는 기본 제공 기능을 제공 하지 않습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 컨트롤은 팝업을 배치 하는 기본 제공 기능을 제공 하지 않습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하기 위해 `ScriptManager`합니다. 컨트롤은 페이지의 아무 곳에 나 배치 되어야 합니다 (`<form>` 요소 내).

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample1.aspx)]

다음으로, 모달 popup으로 사용 되는 패널을 추가 합니다. 단추는 팝업을 닫는 데 사용 됩니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample2.aspx)]

팝업이 표시 될 때마다 페이지의 특정 위치에 배치 됩니다. 이 작업의 경우 클라이언트 쪽 JavaScript 함수가 생성 됩니다. 먼저 패널에 액세스 하려고 시도 합니다. 성공적으로 수행 되 면 패널의 위치는 CSS 및 JavaScript를 사용 하 여 설정 됩니다 (에서 팝업의 위치 변경). 그러나 `ModalPopupExtender` 컨트롤은 팝업도 배치 하려고 합니다. 따라서 JavaScript 코드는 각각 1/10 초 마다 팝업을 반복 해 서 배치 합니다.

[!code-html[Main](positioning-a-modalpopup-vb/samples/sample3.html)]

여기에서 볼 수 있듯이 `setTimeout()` JavaScript 메서드의 반환 값은 전역 변수에 저장 됩니다. 이렇게 하면 `clearTimeout()` 메서드를 사용 하 여 요청 시 팝업의 반복적인 배치를 중지할 수 있습니다.

[!code-javascript[Main](positioning-a-modalpopup-vb/samples/sample4.js)]

이제는이 작업을 수행 하는 데 필요한 모든 작업을 수행 하는 것이 좋습니다. 패널을 트리거하는 단추를 클릭 하면 `movePanel()` JavaScript 함수를 호출 해야 합니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample5.aspx)]

`stopMoving()` 함수는 팝업을 닫을 때 실행 됩니다 .이는 `ModalPopupExtender` 컨트롤에서 트리거될 수 있습니다.

[!code-aspx[Main](positioning-a-modalpopup-vb/samples/sample6.aspx)]

[모달 팝업이 지정 된 위치에 표시 ![](positioning-a-modalpopup-vb/_static/image2.png)](positioning-a-modalpopup-vb/_static/image1.png)

모달 팝업이 지정 된 위치에 나타납니다 ([전체 크기 이미지를 보려면 클릭](positioning-a-modalpopup-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](handling-postbacks-from-a-modalpopup-vb.md)
