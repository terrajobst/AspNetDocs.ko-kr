---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
title: Repeater (C#)에서 단일 단추 사용 | Microsoft Docs
author: wenz
description: 사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다. 예 인 경우에만 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: a973ed3e-400c-4925-ace2-0b086b479301
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-cs
msc.type: authoredcontent
ms.openlocfilehash: 468a830f01c48dc39b22bc5d826f80533df65c1a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574387"
---
# <a name="using-a-confirmbutton-in-a-repeater-c"></a>Repeater에 ConfirmButton 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1CS.pdf)

> 사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다. 예를 클릭 한 경우에만 단추의 동작이 실행 되 고, 그렇지 않으면 취소 됩니다. 이는 리피터 에서도 가능 합니다.

## <a name="overview"></a>개요

사용자가 단추 (LinkButton 컨트롤 포함)를 클릭 하면 AJAX 컨트롤 Toolkit의 [사용자] 단추 extender가 예/아니요 팝업을 만듭니다. 예를 클릭 한 경우에만 단추의 동작이 실행 되 고, 그렇지 않으면 취소 됩니다. 이는 리피터 에서도 가능 합니다.

## <a name="steps"></a>단계

먼저 데이터 원본이 필요 합니다. 이 샘플에서는 AdventureWorks 데이터베이스와 Microsoft SQL Server 2005 Express Edition을 사용 합니다. 데이터베이스는 Visual Studio 설치 (express edition 포함)의 선택적 부분이 며 [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다. AdventureWorks 데이터베이스는 SQL Server 2005 샘플 및 예제 데이터베이스 ( [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)에서 다운로드)의 일부입니다. 데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en))를 사용 하 고 `AdventureWorks.mdf` 데이터베이스 파일을 연결 하는 것입니다.

이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다. 설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample1.aspx)]

그런 다음 데이터 원본이 필요 합니다. 편의상 AdventureWorks 공급 업체 테이블의 처음 5 개 항목만 검색 됩니다. Visual Studio 마법사를 사용 하 여 데이터 소스를 만들 때 현재 테이블 이름 (`Vendors`)에는 `Purchasing`접두사가 올바르게 붙지 않습니다. 올바른 태그는 다음과 같습니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample2.aspx)]

그러면이 데이터 원본을 repeater 내에서 사용할 수 있습니다. 일반적으로 `DataBinder.Eval()` 메서드는 데이터 소스에서 데이터를 검색 합니다. 그런 다음 데이터 원본의 모든 항목에 대해 표시 되도록 `ConfirmButtonExtender` 컨트롤을 repeater의 `<ItemTemplate>` 섹션에 배치 해야 합니다.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-cs/samples/sample3.aspx)]

[데이터 원본의 각 항목 옆에 확인 단추가 표시 ![](using-a-confirmbutton-in-a-repeater-cs/_static/image2.png)](using-a-confirmbutton-in-a-repeater-cs/_static/image1.png)

확인 단추는 데이터 원본의 각 항목 옆에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-a-confirmbutton-in-a-repeater-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](using-a-confirmbutton-in-a-repeater-vb.md)
