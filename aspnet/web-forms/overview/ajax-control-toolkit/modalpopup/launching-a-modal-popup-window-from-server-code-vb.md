---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
title: 서버 코드에서 모달 팝업 창 시작 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오에서는
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 36ca81d7-906d-4db2-952b-add18a4ff421
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/launching-a-modal-popup-window-from-server-code-vb
msc.type: authoredcontent
ms.openlocfilehash: 1368a78d35ac6461bbc2e852e468f42eef2c0d2c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496961"
---
# <a name="launching-a-modal-popup-window-from-server-code-vb"></a>서버 코드에서 모달 팝업 창 시작(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup1VB.pdf)

> AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오의 경우에는 서버 쪽에서 모달 팝업을 여는 것이 필요 합니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 그러나 일부 시나리오의 경우에는 서버 쪽에서 모달 팝업을 여는 것이 필요 합니다.

## <a name="steps"></a>단계

먼저, ModalPopup 컨트롤이 작동 하는 방법을 보여 주기 위해 ASP.NET Button 웹 컨트롤이 필요 합니다. 새 페이지의 &lt;폼&gt; 요소에 이러한 단추를 추가 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample1.aspx)]

그런 다음 만들려는 팝업에 대 한 태그가 필요 합니다. `<asp:Panel>` 컨트롤로 정의 하 고 단추 컨트롤이 포함 되어 있는지 확인 합니다. ModalPopup 컨트롤은 이러한 단추를 팝업을 닫기 위한 기능을 제공 합니다. 그렇지 않은 경우에는 쉽게 사라질 수 있는 방법이 없습니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample2.aspx)]

그런 다음 ASP.NET AJAX Toolkit의 ModalPopup 컨트롤을 페이지에 추가 합니다. 컨트롤을 로드 하는 단추에 대 한 속성을 설정 하 고 단추를 사라지게 하는 단추와 실제 팝업의 ID를 설정 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample3.aspx)]

ASP.NET AJAX를 기반으로 하는 모든 웹 페이지와 마찬가지로 스크립트 관리자는 다음과 같은 다양 한 대상 브라우저에 필요한 JavaScript 라이브러리를 로드 하는 데 필요 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample4.aspx)]

브라우저에서 예제를 실행 합니다. 단추를 클릭 하면 모달 팝업이 나타납니다. 서버 쪽 코드를 사용 하 여 동일한 결과를 얻기 위해 새 단추가 필요 합니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample5.aspx)]

여기에서 볼 수 있듯이 단추를 클릭 하면 포스트백이 생성 되 고 서버에서 `ServerButton_Click()` 메서드가 실행 됩니다. 이 메서드에서 `launchModal()` 이라는 JavaScript 함수는 정확 하 게 실행 됩니다. 페이지가 로드 되 면 JavaScript 함수가 실행 됩니다.

[!code-aspx[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample6.aspx)]

`launchModal()` 작업은 ModalPopup을 표시 하는 것입니다. `launchModal()` 함수는 전체 HTML 페이지가 로드 된 후에 실행 됩니다. 그러나이 시점에서 ASP.NET AJAX 프레임 워크는 아직 완전히 로드 되지 않았습니다. 따라서 `launchModal()` 함수는 ModalPopup 컨트롤이 나중에 표시 되어야 하는 변수만 설정 합니다.

[!code-html[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample7.html)]

`pageLoad()` JavaScript 함수는 ASP.NET AJAX가 완전히 로드 된 후 실행 되는 특수 함수입니다. 따라서이 함수에 코드를 추가 하 여 ModalPopup 컨트롤을 표시 하지만 `launchModal()` 이전에 호출 된 경우에만 표시 됩니다.

[!code-javascript[Main](launching-a-modal-popup-window-from-server-code-vb/samples/sample8.js)]

`$find()` 함수는 페이지에서 명명 된 요소를 찾고 서버측 ID를 매개 변수로 예상 합니다. 따라서 `$find("mpe")`는 ModalPopup 컨트롤의 클라이언트 표현을 반환 합니다. 해당 `show()` 메서드를 사용 하면 팝업이 표시 됩니다.

[단추 중 하나를 클릭 하면 모달 팝업이 나타납니다 ![](launching-a-modal-popup-window-from-server-code-vb/_static/image2.png)](launching-a-modal-popup-window-from-server-code-vb/_static/image1.png)

단추 중 하나를 클릭 하면 모달 팝업이 나타납니다 ([전체 크기 이미지를 보려면 클릭](launching-a-modal-popup-window-from-server-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](positioning-a-modalpopup-cs.md)
> [다음](using-modalpopup-with-a-repeater-control-vb.md)
