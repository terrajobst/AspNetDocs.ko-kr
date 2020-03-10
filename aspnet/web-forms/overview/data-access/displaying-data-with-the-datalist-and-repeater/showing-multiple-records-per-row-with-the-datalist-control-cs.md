---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: DataList 컨트롤을 사용 하 여 행 마다 여러 레코드C#표시 () | Microsoft Docs
author: rick-anderson
description: 이 간단한 자습서에서는 RepeatColumns 및 RepeatDirection 속성을 통해 DataList의 레이아웃을 사용자 지정 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 09/13/2006
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3280a7b5f28207d3e640a6480f47869ce19692bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481109"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>DataList 컨트롤을 사용하여 행마다 여러 레코드 표시(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe) 또는 [PDF 다운로드](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> 이 간단한 자습서에서는 RepeatColumns 및 RepeatDirection 속성을 통해 DataList의 레이아웃을 사용자 지정 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

이전 두 자습서에서 살펴본 DataList 예제는 데이터 원본의 각 레코드를 단일 열 HTML `<table>`의 행으로 렌더링 했습니다. 이는 기본 DataList 동작 이지만 데이터 원본 항목이 다중 열 다중 행 테이블에 분산 되도록 DataList 표시를 쉽게 사용자 지정할 수 있습니다. 또한 모든 데이터 원본 항목이 단일 행, 다중 열 DataList에 표시 될 수 있습니다.

`RepeatColumns` 및 `RepeatDirection` 속성을 통해 DataList s 레이아웃을 사용자 지정할 수 있으며,이 속성은 렌더링 되는 열 수와 해당 항목이 세로 또는 가로로 배치 되는지 여부를 나타냅니다. 예를 들어 그림 1에는 세 개의 열이 있는 테이블에 제품 정보를 표시 하는 DataList가 표시 됩니다.

[DataList ![행당 세 가지 제품을 표시 합니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**그림 1**: DataList는 행당 세 가지 제품을 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png)).

DataList는 행당 여러 데이터 원본 항목을 표시 하 여 가로 화면 공간을 보다 효율적으로 활용할 수 있습니다. 이 간단한 자습서에서는 이러한 두 DataList 속성을 살펴봅니다.

## <a name="step-1-displaying-product-information-in-a-datalist"></a>1 단계: DataList에서 제품 정보 표시

`RepeatColumns` 및 `RepeatDirection` 속성을 검사 하기 전에 먼저 표준 단일 열 다중 행 테이블 레이아웃을 사용 하 여 제품 정보를 나열 하는 DataList를 페이지에 만듭니다. 이 예에서는 다음 태그를 사용 하 여 제품 이름, 범주 및 가격을 표시 합니다.

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

이전 예제에서 DataList에 데이터를 바인딩하는 방법을 알아보았습니다. 따라서 이러한 단계를 빠르게 진행 합니다. 먼저 `DataListRepeaterBasics` 폴더에서 `RepeatColumnAndDirection.aspx` 페이지를 열고 DataList를 도구 상자에서 디자이너로 끌어 옵니다. DataList s 스마트 태그에서 새 ObjectDataSource를 만들어 `ProductsBLL` 클래스 s `GetProducts` 메서드에서 데이터를 가져오도록 구성 하 고 마법사의 삽입, 업데이트 및 삭제 탭에서 (없음) 옵션을 선택 합니다.

새 ObjectDataSource를 만들어 DataList에 바인딩한 후 Visual Studio에서 각 제품 데이터 필드의 이름과 값을 표시 하는 `ItemTemplate`을 자동으로 만듭니다. 위에 표시 된 태그를 사용 하도록 해당 데이터 바인딩 구문을 사용 하 여 해당 `Text` 속성에 값을 할당 하는 레이블 컨트롤로 *Product name*, *Category Name*및 *Price* 텍스트를 대체 하 여 선언적 태그를 통해 직접 `ItemTemplate`를 조정 하거나 DataList s 스마트 태그의 템플릿 편집 옵션을 사용 합니다. `ItemTemplate`를 업데이트 한 후 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

`UnitPrice`에 대 한 `Eval` 데이터 바인딩 구문에 서식 지정자를 포함 하 여 반환 된 값을 `Eval("UnitPrice", "{0:C}").` 통화로 서식 지정 합니다.

잠시 시간을 들 여 브라우저에서 페이지를 방문 하세요. 그림 2에 나와 있는 것 처럼 DataList는 단일 열 다중 행 테이블로 렌더링 됩니다.

[![기본적으로 DataList는 단일 열 다중 행 테이블로 렌더링 됩니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**그림 2**: 기본적으로 DataList는 단일 열 다중 행 테이블로 렌더링 됩니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png)).

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>2 단계: DataList s 레이아웃 방향 변경

DataList의 기본 동작은 단일 열 다중 행 테이블에서 항목을 세로로 레이아웃 하는 것 이지만이 동작은 DataList s [`RepeatDirection` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)을 통해 쉽게 변경할 수 있습니다. `RepeatDirection` 속성은 `Horizontal` 또는 `Vertical` (기본값)의 두 가지 가능한 값 중 하나를 사용할 수 있습니다.

DataList는 `RepeatDirection` 속성을 `Vertical`에서 `Horizontal`으로 변경 하 여 데이터 원본 항목당 하나의 열을 만들어 해당 레코드를 단일 행으로 렌더링 합니다. 이러한 효과를 보여 주려면 디자이너에서 DataList를 클릭 한 다음 속성 창에서 `RepeatDirection` 속성을 `Vertical`에서 `Horizontal`로 변경 합니다. 이렇게 하면 디자이너에서 DataList s 레이아웃을 조정 하 여 단일 행의 다중 열 인터페이스를 만듭니다 (그림 3 참조).

[RepeatDirection 속성 ![DataList 항목의 레이아웃 방향을 결정 합니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**그림 3**: `RepeatDirection` 속성은 DataList 항목의 레이아웃 방향을 결정 합니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png)).

적은 양의 데이터를 표시할 때 단일 행의 다중 열 테이블이 화면 부동산을 최대화 하는 이상적인 방법일 수 있습니다. 그러나 큰 데이터 볼륨의 경우 단일 행에는 여러 열이 필요 하며,이는 화면에 맞출 수 있는 항목을 오른쪽으로 밀어 넣는 것입니다. 그림 4는 단일 행 DataList에서 렌더링 되는 제품을 보여 줍니다. 많은 제품이 있으므로 (80 초과) 사용자는 각 제품에 대 한 정보를 보기 위해 오른쪽으로 스크롤해야 합니다.

[충분 한 크기의 데이터 원본에 대 한 ![단일 열 DataList는 가로 스크롤이 필요 합니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**그림 4**: 충분 한 큰 데이터 원본의 경우 단일 열 DataList에 가로 스크롤이 필요 합니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png)).

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>3 단계: 다중 열 다중 행 테이블에서 데이터 표시

다중 열 다중 행 DataList를 만들려면 [`RepeatColumns` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx) 을 표시할 열 수로 설정 해야 합니다. 기본적으로 `RepeatColumns` 속성은 0으로 설정 됩니다. 그러면 DataList가 `RepeatDirection` 속성의 값에 따라 단일 행 이나 열에 모든 항목을 표시 합니다.

이 예에서는 테이블 행당 세 가지 제품을 표시 합니다. 따라서 `RepeatColumns` 속성을 3으로 설정 합니다. 이렇게 변경한 후에는 잠시 후 브라우저에서 결과를 확인 합니다. 그림 5와 같이 이제 제품이 3 개의 열로 된 다중 행 테이블에 나열 됩니다.

[![3 개 제품이 행당 표시 됩니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**그림 5**: 행 마다 세 개의 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png)).

`RepeatDirection` 속성은 DataList의 항목이 배치 되는 방법에 영향을 줍니다. 그림 5는 `RepeatDirection` 속성이 `Horizontal`로 설정 된 결과를 보여 줍니다. 처음 세 개 제품 Chai, 파일과 및 Aniseed Syrup은 왼쪽에서 오른쪽, 위쪽에서 아래쪽으로 배치 됩니다. 다음 세 가지 제품 (Chef Anton s Cajun Seasoning부터 시작)은 처음 3 개의 행 아래에 나타납니다. 그러나 `RepeatDirection` 속성을 다시 `Vertical`으로 변경 하면 그림 6에서 보여 주는 것 처럼 위에서 아래로, 왼쪽에서 오른쪽으로 이러한 제품을 레이아웃 합니다.

[여기 ![제품은 세로로 배치 됩니다.](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**그림 6**: 여기에서 제품이 세로로 배치 됩니다 ([전체 크기 이미지를 보려면 클릭](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png)).

결과 테이블에 표시 되는 행 수는 DataList에 바인딩된 총 레코드 수에 따라 달라 집니다. 정확 하 게,이 값은 `RepeatColumns` 속성 값으로 나눈 총 데이터 원본 항목 수의 상한입니다. `Products` 테이블에는 현재 3으로 나눌 수 있는 84 제품이 있으므로 28 개 행이 있습니다. 데이터 원본의 항목 수와 `RepeatColumns` 속성 값을 나눌 수 없는 경우 마지막 행 또는 열에 빈 셀이 포함 됩니다. `RepeatDirection`을 `Vertical`로 설정 하면 마지막 열에 빈 셀이 포함 됩니다. `RepeatDirection` `Horizontal`되 면 마지막 행에 빈 셀이 포함 됩니다.

## <a name="summary"></a>요약

기본적으로 DataList는 단일 열 다중 행 테이블에 항목을 나열 하며이는 단일 Templatefield로 변환를 사용 하 여 GridView의 레이아웃을 모방 합니다. 이 기본 레이아웃은 허용 되지만 행 마다 여러 데이터 원본 항목을 표시 하 여 화면 부동산을 최대화할 수 있습니다. 이를 수행 하려면 DataList s `RepeatColumns` 속성을 행당 표시할 열 수로 설정 하면 됩니다. 또한 DataList s `RepeatDirection` 속성을 사용 하 여 여러 열로 된 다중 행 테이블의 콘텐츠를 왼쪽에서 오른쪽, 위쪽에서 아래쪽으로, 왼쪽에서 오른쪽으로 왼쪽에서 오른쪽으로 배치 해야 하는지 여부를 나타낼 수 있습니다.

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 John Suru입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [다음](nested-data-web-controls-cs.md)
