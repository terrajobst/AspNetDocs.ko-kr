---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: 여러 Popup 컨트롤 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. M ...을 사용 하는 것도 가능 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496427"
---
# <a name="using-multiple-popup-controls-c"></a>여러 팝업 컨트롤 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 또한 한 페이지에서 둘 이상의 popup 컨트롤을 사용할 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 PopupControl extender는 다른 컨트롤이 활성화 될 때 팝업을 쉽게 트리거하는 방법을 제공 합니다. 또한 한 페이지에서 둘 이상의 popup 컨트롤을 사용할 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

다음으로 팝업으로 사용 되는 패널을 추가 합니다. 현재 시나리오에서 패널은 `Calendar` 컨트롤을 포함 합니다. 달력의 포스트백으로 인 한 페이지 새로 고침을 방지 하기 위해 패널은 `UpdatePanel` 컨트롤 내에 배치 됩니다.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

페이지에는 두 개의 텍스트 상자도 있습니다. 텍스트 상자를 활성화 한 후에는 각 입력란에 대 한 달력 팝업이 표시 됩니다.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

이제 `PopupControlExtender`를 사용 하 여 두 개의 텍스트 상자를 확장 합니다. `TargetControlID` 특성은 extender에 연결 된 컨트롤의 ID를 제공 합니다. `PopupControlID` 특성에는 팝업 패널의 ID가 포함 됩니다. 이 경우 두 extender는 동일한 패널을 표시 하지만 다른 패널도 가능 합니다.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

이제 텍스트 필드를 클릭할 때마다 필드 아래에 달력이 표시 되어 날짜를 선택할 수 있습니다. 선택한 날짜를 텍스트 상자에 다시 가져오는 것은 다른 자습서에서 설명 합니다.

[사용자가 텍스트 상자를 클릭할 때 달력이 표시 되는 ![](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

사용자가 텍스트 상자를 클릭 하면 달력이 나타납니다 ([전체 크기 이미지를 보려면 클릭](using-multiple-popup-controls-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)
