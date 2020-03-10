---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
title: ColorPicker 컨트롤 Extender (C#) 사용 Microsoft Docs
author: microsoft
description: ColorPicker는 팝업 컨트롤에서 UI를 사용 하 여 클라이언트측 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. ASP.NET에 연결할 수 있습니다.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 0d86a1e7-a910-4ab2-b85c-7a9ea6906c39
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-cs
msc.type: authoredcontent
ms.openlocfilehash: ac510ab353878038c1c7a103bfbf6d32fb1b2686
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497621"
---
# <a name="using-the-colorpicker-control-extender-c"></a>ColorPicker 컨트롤 Extender (C#) 사용

[Microsoft](https://github.com/microsoft) 에서

> ColorPicker는 팝업 컨트롤에서 UI를 사용 하 여 클라이언트측 색 선택 기능을 제공 하는 ASP.NET AJAX extender입니다. 모든 ASP.NET TextBox 컨트롤에 연결할 수 있습니다. 메서드.

이 자습서의 목표는 AJAX 컨트롤 Toolkit ColorPicker 컨트롤 extender를 사용 하는 방법을 설명 하는 것입니다. ColorPicker 컨트롤 extender는 색을 선택할 수 있는 팝업 대화 상자를 표시 합니다. ColorPicker는 사용자가 색을 선택할 수 있는 직관적인 사용자 인터페이스를 제공 하려는 경우에 유용 합니다.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>ColorPicker 컨트롤 Extender를 사용 하 여 TextBox 컨트롤 확장

예를 들어 방문자가 사용자 지정 된 비즈니스 카드를 만들 수 있는 웹 사이트를 만들려고 한다고 가정 합니다. 방문자는 명함 텍스트를 입력 하 고 색을 선택할 수 있습니다. 목록 1의 ASP.NET 페이지에는 txt, Text 및 Txt를 색으로 지정 된 두 개의 TextBox 컨트롤이 있습니다. 양식을 제출 하면 선택한 값이 표시 됩니다 (그림 1 참조).

[비즈니스 카드를 만들기 위한 단순 양식 ![](using-the-colorpicker-control-extender-cs/_static/image1.jpg)](using-the-colorpicker-control-extender-cs/_static/image1.png)

**그림 01**: 회사 카드를 만드는 간단한 양식 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image2.png))

**목록 1-CreateCard .aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample1.aspx)]

목록 1의 양식은 작동 하지만 뛰어난 사용자 환경을 제공 하지 않습니다. 사용자가 텍스트 상자에 색을 입력 해야 합니다. 사용자가 특별 한 색 (예: pea green의 오른쪽 음영)을 원하는 경우에는 사용자가 도움말이 없는 HTML 색 코드를 확인 해야 합니다.

ColorPicker 컨트롤 extender를 사용 하 여 더 나은 사용자 환경을 만들 수 있습니다. 텍스트 상자 컨트롤에 포커스를 이동할 때 ColorPicker는 색 대화 상자를 표시 합니다 (그림 2 참조).

[ColorPicker 컨트롤 Extender를 ![합니다.](using-the-colorpicker-control-extender-cs/_static/image2.jpg)](using-the-colorpicker-control-extender-cs/_static/image3.png)

**그림 02**: Colorpicker 컨트롤 Extender ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image4.png))

목록 1의 양식과 함께 ColorPicker 컨트롤 extender를 사용 하려면 두 단계를 완료 해야 합니다.

1. 페이지에 ScriptManager 컨트롤 추가
2. 페이지에 ColorPicker 컨트롤 extender 추가

ColorPicker를 사용 하려면 페이지에 ScriptManager를 추가 해야 합니다. ScriptManager를 추가 하는 좋은 장소는 서버 쪽 &lt;양식&gt; 태그를 여는 것입니다. ScriptManager를 도구 상자에서 페이지로 끌어올 수 있습니다 (ScriptManager는 AJAX 확장 탭 아래에 있음). 또는 서버 쪽 양식 열기 태그 아래에서 소스 뷰에 다음 태그를 입력할 수 있습니다.

&lt;asp: ScriptManager ID = "ScriptManager1" runat = "server"/&gt;

ColorPicker 컨트롤 extender를 페이지에 추가 하는 가장 쉬운 방법은 디자인 뷰입니다. Txt카드 색 텍스트 상자 위로 마우스를 가져가면 스마트 작업 옵션이 표시 되어 extender를 추가할 수 있습니다 (그림 3 참조). 이 옵션을 선택 하면 Extender 마법사가 나타납니다 (그림 4 참조).

[extender를 추가 ![](using-the-colorpicker-control-extender-cs/_static/image3.jpg)](using-the-colorpicker-control-extender-cs/_static/image5.png)

**그림 03**: extender 추가 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image6.png))

[Extender 마법사를 사용 하 여 컨트롤 extender를 선택 ![](using-the-colorpicker-control-extender-cs/_static/image4.jpg)](using-the-colorpicker-control-extender-cs/_static/image7.png)

**그림 04**: extender 마법사를 사용 하 여 컨트롤 extender 선택 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image8.png))

Colorpicker extender를 선택 하 여 ColorPicker 색 텍스트 상자를 ColorPicker extender로 확장할 수 있습니다. 확인을 클릭하여 대화 상자를 닫습니다.

이러한 변경을 수행한 후에는 페이지의 소스가 목록 2 처럼 보입니다.

목록 2-CreateCard (ColorPicker 사용)

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample2.aspx)]

이제 페이지에 txtCardColor TextBox 컨트롤 바로 아래에 표시 되는 Color Kerextender 컨트롤이 포함 되어 있습니다. ColorPickerExtender 컨트롤은 색 선택 대화 상자를 표시 하도록 Txt의 색 컨트롤을 확장 합니다.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>단추를 사용 하 여 색 선택 대화 상자 시작

ColorPicker extender는 다음 속성을 지원 합니다.

- PopupButtonId-색 선택 대화 상자를 표시 하는 페이지의 단추 ID입니다.
- PopupPosition-색 선택 대화 상자의 대상 컨트롤에 상대적인 위치입니다. 가능한 값은 Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right 및 Left (기본값은 BottomLeft)입니다.
- SampleControlId-선택한 색을 표시 하는 컨트롤의 ID입니다.
- SelectedColor-ColorPicker에서 선택한 첫 번째 색입니다.

이러한 속성을 사용 하 여 색 선택 대화 상자를 표시 하는 방법과 선택한 색을 표시 하는 방법을 사용자 지정할 수 있습니다. 목록 3의 페이지는 이러한 속성 중 일부를 사용 하는 방법을 보여 줍니다.

**목록 3-CreateCardButton**

[!code-aspx[Main](using-the-colorpicker-control-extender-cs/samples/sample3.aspx)]

목록 3의 페이지에는 선택 색 단추가 있습니다 (그림 5 참조). 이 단추를 클릭 하면 텍스트 상자 위에 색 선택 대화 상자가 나타납니다. 대화 상자에서 색을 선택 하면 선택한 색이 lblSample Label 컨트롤의 배경색으로 나타납니다.

ColorPicker PopupButtonID 속성은 색 선택 단추를 ColorPicker extender와 연결 하는 데 사용 됩니다. PopupButtonID 속성에 대 한 값을 제공 하면 대상 컨트롤에 포커스가 있을 때 색 선택 대화 상자가 더 이상 표시 되지 않습니다. 대화 상자를 표시 하려면 단추를 클릭 해야 합니다.

SampleControlID 속성은 선택 된 색을 표시 하는 컨트롤을 ColorPicker와 연결 하는 데 사용 됩니다. ColorPicker는이 컨트롤의 배경색을 현재 선택 된 색으로 변경 합니다.

[단추를 사용 하 여 색 선택 대화 상자를 표시 ![](using-the-colorpicker-control-extender-cs/_static/image5.jpg)](using-the-colorpicker-control-extender-cs/_static/image9.png)

**그림 05**: 단추를 사용 하 여 색 선택 대화 상자 표시 ([전체 크기 이미지를 보려면 클릭](using-the-colorpicker-control-extender-cs/_static/image10.png))

## <a name="summary"></a>요약

이 자습서에서는 ColorPicker 컨트롤 extender를 사용 하 여 팝업 색 선택 대화 상자를 표시 하는 방법을 배웠습니다. 먼저 포커스가 TextBox 컨트롤로 이동 될 때 대화 상자를 표시할 수 있는 방법을 살펴보았습니다. 다음으로 단추를 클릭할 때 색 선택 대화 상자를 표시 하는 단추를 만드는 방법을 알아보았습니다.

> [!div class="step-by-step"]
> [다음](using-the-colorpicker-control-extender-vb.md)
