---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
title: ReorderList와 함께 다시 게시 사용 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록이 다시 정렬 될 때마다 po ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e5b6ed70-19ed-4024-ba4f-6d78e8acdc0f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/using-postbacks-with-reorderlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 5d6075e40df2c32df6c0d801243eff98fa7790b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78445931"
---
# <a name="using-postbacks-with-reorderlist-vb"></a>ReorderList에 포스트백 사용(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList4.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist4VB.pdf)

> AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 `ReorderList` 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록이 다시 정렬 될 때마다 포스트백은 서버에 변경 내용을 알립니다.

## <a name="steps"></a>단계

`ReorderList` 컨트롤에 사용할 수 있는 데이터 소스는 여러 가지가 있습니다. 하나는 `XmlDataSource` 컨트롤을 사용 하는 것입니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample1.aspx)]

이 XML을 `ReorderList` 컨트롤에 바인딩하고 다시 게시를 사용 하도록 설정 하려면 다음 특성을 설정 해야 합니다.

- `DataSourceID`: 데이터 원본의 ID
- `SortOrderField`: 정렬할 속성
- `AllowReorder`: 사용자가 목록 요소를 다시 정렬할 수 있는지 여부
- `PostBackOnReorder`: 목록이 다시 정렬 될 때마다 다시 게시를 만들지 여부

다음은 컨트롤에 대 한 적절 한 태그입니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample2.aspx)]

`ReorderList` 컨트롤 내에서 `Eval()` 메서드를 사용 하 여 데이터 소스의 특정 데이터를 바인딩할 수 있습니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample3.aspx)]

페이지의 임의 위치에서 마지막으로 다시 정렬 하는 동안 레이블이 정보를 포함 합니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample4.aspx)]

이 레이블은 서버 쪽 코드의 텍스트로 채워지고 다시 게시를 처리 합니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample5.aspx)]

마지막으로 ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하기 위해 페이지에 `ScriptManager` 컨트롤을 넣어야 합니다.

[!code-aspx[Main](using-postbacks-with-reorderlist-vb/samples/sample6.aspx)]

[각 다시 정렬을 ![포스트백이 트리거됩니다.](using-postbacks-with-reorderlist-vb/_static/image2.png)](using-postbacks-with-reorderlist-vb/_static/image1.png)

다시 정렬 하면 다시 게시가 트리거됩니다 ([전체 크기 이미지를 보려면 클릭](using-postbacks-with-reorderlist-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](drag-and-drop-via-reorderlist-cs.md)
> [다음](drag-and-drop-via-reorderlist-vb.md)
