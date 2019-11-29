---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
title: Repeater 컨트롤에서에 hovermenu 사용 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의에 hovermenu 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 specifi에 팝업이 표시 됩니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e7700e7b-edc3-4183-a713-70e507cc7490
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3e38b91d837c65191d4b3797fa31ef6112a1f070
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606707"
---
# <a name="using-hovermenu-with-a-repeater-control-c"></a>반복기 컨트롤에 HoverMenu 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1CS.pdf)

> AJAX 컨트롤 도구 키트의에 hovermenu 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 지정 된 위치에 팝업이 나타납니다. Repeater 내에서이 컨트롤을 사용할 수도 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 `HoverMenu` 컨트롤은 간단한 팝업 효과를 제공 합니다. 마우스 포인터를 요소 위로 가져가면 지정 된 위치에 팝업이 나타납니다. Repeater 내에서이 컨트롤을 사용할 수도 있습니다.

## <a name="steps"></a>단계

먼저 데이터 원본이 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다. AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다. 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다. 설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample1.aspx)]

그런 다음 페이지에 데이터 원본을 추가 합니다. 제한 된 양의 데이터를 사용 하기 위해 AdventureWorks 데이터베이스의 Vendor 테이블에서 처음 5 개 항목만 선택 합니다. Visual Studio assistant를 사용 하 여 데이터 소스를 만드는 경우 현재 버전의 버그는 테이블 이름 (`Vendor`)에 `Purchasing`접두사로 사용 하지 않습니다. 다음 태그는 올바른 구문을 보여 줍니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample2.aspx)]

다음으로, 모달 popup으로 사용 되는 패널을 추가 합니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample3.aspx)]

이제 `HoverMenuExtender`이 실행 됩니다. 데이터 소스에 있는 모든 요소가 자체 팝업을 가져오기 위해 extender의 `<ItemTemplate>` 섹션 안에 extender를 넣어야 합니다. 다음은 태그입니다.

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-cs/samples/sample4.aspx)]

이제 데이터 원본의 모든 항목에는 50 밀리초 (`PopDelay` 특성) 지연 후 오른쪽 (`PopupPosition` 특성)에 대 한 팝업이 표시 됩니다.

[가리키기 메뉴 ![repeater의 각 항목 옆에 표시 됩니다.](using-hovermenu-with-a-repeater-control-cs/_static/image2.png)](using-hovermenu-with-a-repeater-control-cs/_static/image1.png)

가리키기 메뉴가 repeater의 각 항목 옆에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-hovermenu-with-a-repeater-control-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](using-hovermenu-with-a-repeater-control-vb.md)
