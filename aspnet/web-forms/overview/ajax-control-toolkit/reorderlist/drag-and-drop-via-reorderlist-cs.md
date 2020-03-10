---
uid: web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
title: ReorderList를 통해 끌어서 놓기 (C#) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록의 현재 순서는 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6350ee8e-11d6-4aff-b51c-942878014835
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/reorderlist/drag-and-drop-via-reorderlist-cs
msc.type: authoredcontent
ms.openlocfilehash: 2fc6d55a290cbb58bea36d8145d814e337bbd931
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446009"
---
# <a name="drag-and-drop-via-reorderlist-c"></a>ReorderList를 통해 끌어서 놓기(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/ReorderList5.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/reorderlist5CS.pdf)

> AJAX 컨트롤 도구 키트의 ReorderList 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록의 현재 순서는 서버에 유지 됩니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 `ReorderList` 컨트롤은 끌어서 놓기를 통해 사용자가 다시 정렬할 수 있는 목록을 제공 합니다. 목록의 현재 순서는 서버에 유지 됩니다.

## <a name="steps"></a>단계

`ReorderList` 컨트롤은 데이터베이스의 데이터를 목록에 바인딩하는 것을 지원 합니다. 무엇 보다도, 목록 요소 순서에 대 한 변경 내용을 데이터 저장소에 다시 쓸 수 있도록 지원 합니다.

이 샘플에서는 Microsoft SQL Server 2005 Express Edition을 데이터 저장소로 사용 합니다. 데이터베이스는 express edition을 포함 하 여 Visual Studio 설치의 선택적 (및 무료) 부분입니다. [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064)에서 별도의 다운로드로 사용할 수도 있습니다. 이 샘플에서는 SQL Server 2005 Express Edition 인스턴스가 `SQLEXPRESS` 호출 되 고 웹 서버와 같은 컴퓨터에 있는 것으로 가정 합니다. 이는 기본 설정 이기도 합니다. 설정이 다른 경우 데이터베이스에 대 한 연결 정보를 조정 해야 합니다.

데이터베이스를 설정 하는 가장 쉬운 방법은 Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en) )를 사용 하는 것입니다. 서버에 연결 하 여 `Databases`를 두 번 클릭 하 고 새 데이터베이스를 만듭니다 (마우스 오른쪽 단추를 클릭 하 고 `New Database`를 선택) `Tutorials`.

이 데이터베이스에서 다음 네 개의 열을 사용 하 여 `AJAX` 라는 새 테이블을 만듭니다.

- `id` (기본 키, 정수, id, NULL 아님)
- `char` (char (1), NULL)
- `description` (varchar (50), NULL)
- `position` (int, NULL)

[AJAX 테이블의 레이아웃 ![](drag-and-drop-via-reorderlist-cs/_static/image2.png)](drag-and-drop-via-reorderlist-cs/_static/image1.png)

AJAX 테이블의 레이아웃 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image3.png))

그런 다음 두 개의 값으로 테이블을 채웁니다. `position` 열에는 요소의 정렬 순서가 포함 됩니다.

[AJAX 테이블의 초기 데이터 ![](drag-and-drop-via-reorderlist-cs/_static/image5.png)](drag-and-drop-via-reorderlist-cs/_static/image4.png)

AJAX 테이블의 초기 데이터 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image6.png))

다음 단계에서는 새 데이터베이스와 해당 테이블과 통신 하는 `SqlDataSource` 컨트롤을 생성 해야 합니다. 데이터 원본은 `SELECT` 및 `UPDATE` SQL 명령을 지원 해야 합니다. 목록 요소의 순서가 나중에 변경 되는 경우 `ReorderList` 컨트롤은 데이터 원본의 `Update` 명령에 새 위치와 요소의 ID로 두 값을 자동으로 전송 합니다. 따라서 데이터 원본에는 다음 두 값에 대 한 `<UpdateParameters>` 섹션이 필요 합니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample1.aspx)]

`ReorderList` 컨트롤은 다음 특성을 설정 해야 합니다.

- `AllowReorder`: 목록 항목을 다시 정렬할 수 있는지 여부
- `DataSourceID`: 데이터 원본의 ID
- `DataKeyField`: 데이터 원본에 있는 기본 키 열의 이름입니다.
- `SortOrderField`: 목록 항목에 대 한 정렬 순서를 제공 하는 데이터 원본 열입니다.

`<DragHandleTemplate>` 및 `<ItemTemplate>` 섹션에서 목록의 레이아웃을 세밀 하 게 조정할 수 있습니다. 또한 다음과 같이 `Eval()` 메서드를 사용 하 여 데이터 바인딩을 수행할 수 있습니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample2.aspx)]

다음 CSS 스타일 정보 (`ReorderList` 컨트롤의 `<DragHandleTemplate>` 섹션에서 참조 됨)는 끌기 핸들을 가리킬 때 마우스 포인터가 적절 하 게 변경 되도록 합니다.

[!code-css[Main](drag-and-drop-via-reorderlist-cs/samples/sample3.css)]

마지막으로 `ScriptManager` 컨트롤은 페이지에 대 한 ASP.NET AJAX를 초기화 합니다.

[!code-aspx[Main](drag-and-drop-via-reorderlist-cs/samples/sample4.aspx)]

브라우저에서이 예제를 실행 하 고 목록 항목을 약간 다시 정렬 합니다. 그런 다음 페이지를 다시 로드 하거나 데이터베이스를 확인 합니다. 변경 된 위치는 유지 관리 되 고 데이터베이스의 `position` 열 값 및 태그를 사용 하 여 코드 없이 모두 반영 됩니다.

[새 목록 항목 순서에 따라 데이터베이스의 데이터 변경 내용 ![](drag-and-drop-via-reorderlist-cs/_static/image8.png)](drag-and-drop-via-reorderlist-cs/_static/image7.png)

데이터베이스의 데이터는 새 목록 항목 순서에 따라 변경 됩니다 ([전체 크기 이미지를 보려면 클릭](drag-and-drop-via-reorderlist-cs/_static/image9.png)).

> [!div class="step-by-step"]
> [이전](using-postbacks-with-reorderlist-cs.md)
> [다음](using-postbacks-with-reorderlist-vb.md)
