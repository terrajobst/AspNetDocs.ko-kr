---
uid: web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
title: ModalPopup에서 포스트백 처리 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. Pos를 사용 하는 경우 특별 한 주의를 기울여야 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7963890b-4ea3-4a1c-b65d-6098a3d56f62
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/modalpopup/handling-postbacks-from-a-modalpopup-cs
msc.type: authoredcontent
ms.openlocfilehash: 20073d156b4bd5ce67a47d2511b28594b70ce260
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599075"
---
# <a name="handling-postbacks-from-a-modalpopup-c"></a>ModalPopup에서 포스트백 처리(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/2/4/0/24052038-f942-4336-905b-b60ae56f0dd5/ModalPopup3.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/modalpopup3CS.pdf)

> AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때는 특별히 주의를 기울여야 합니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 ModalPopup 컨트롤은 클라이언트 쪽을 사용 하 여 모달 팝업을 만드는 간단한 방법을 제공 합니다. 팝업 내에서 다시 게시를 만들 때는 특별히 주의를 기울여야 합니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample1.aspx)]

다음으로, 모달 popup으로 사용 되는 패널을 추가 합니다. 여기에서 사용자는 이름 및 전자 메일 주소를 입력할 수 있습니다. 단추는 팝업을 닫고 정보를 저장 하는 데 사용 됩니다. 이 단추를 클릭할 때 포스트백이 발생 하도록 `OnClick` 특성이 설정 되어 있는지 확인 합니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample2.aspx)]

페이지 자체는 이름 및 전자 메일 주소와 정확히 동일한 정보에 대 한 두 개의 레이블로 구성 됩니다. 단추는 모달 팝업을 트리거하는 데 사용 됩니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample3.aspx)]

팝업이 표시 되도록 하려면 `ModalPopupExtender` 컨트롤을 추가 합니다. `PopupControlID` 특성을 패널의 ID로 설정 하 고 단추 ID로 `TargetControlID` 합니다.

[!code-aspx[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample4.aspx)]

이제 모달 팝업 내의 `Save` 단추를 클릭할 때마다 서버측 `SaveData()` 메서드가 실행 됩니다. 여기에서 입력 한 데이터를 데이터 저장소에 저장할 수 있습니다. 간단히 하기 위해 새 데이터는 레이블에 출력 됩니다.

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample5.cs)]

또한 모달 팝업 내의 textbox 컨트롤은 현재 이름과 전자 메일로 채워야 합니다. 그러나 포스트백이 발생 하지 않는 경우에만이 작업이 필요 합니다. 포스트백이 있으면 ASP.NET viewstate 기능에서 자동으로 텍스트 상자를 적절 한 값으로 채웁니다.

[!code-csharp[Main](handling-postbacks-from-a-modalpopup-cs/samples/sample6.cs)]

[모달 popup을 ![포스트백이 발생 합니다.](handling-postbacks-from-a-modalpopup-cs/_static/image2.png)](handling-postbacks-from-a-modalpopup-cs/_static/image1.png)

모달 popup에서 포스트백을 발생 시킵니다 ([전체 크기 이미지를 보려면 클릭](handling-postbacks-from-a-modalpopup-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](using-modalpopup-with-a-repeater-control-cs.md)
> [다음](positioning-a-modalpopup-cs.md)
