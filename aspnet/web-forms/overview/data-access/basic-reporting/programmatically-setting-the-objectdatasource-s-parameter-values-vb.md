---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 단일 입력 매개 변수를 수락 하 고 데이터를 반환 하는 DAL 및 BLL에 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는이 매개 변수를 설정 합니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: f1dd50f46528e8dd51f85e503604d3f0dbc21ad2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74602069"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>ObjectDataSource의 매개 변수 값을 프로그래밍 방식으로 설정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe) 또는 [PDF 다운로드](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> 이 자습서에서는 단일 입력 매개 변수를 수락 하 고 데이터를 반환 하는 DAL 및 BLL에 메서드를 추가 하는 방법을 살펴보겠습니다. 이 예제에서는이 매개 변수를 프로그래밍 방식으로 설정 합니다.

## <a name="introduction"></a>소개

[이전 자습서](declarative-parameters-vb.md)에서 살펴본 것 처럼 매개 변수 값을 ObjectDataSource의 메서드에 선언적으로 전달 하는 데 여러 가지 옵션을 사용할 수 있습니다. 매개 변수 값이 하드 코딩 된 경우, 페이지의 웹 컨트롤에서 제공 되거나 데이터 소스 `Parameter` 개체에서 읽을 수 있는 다른 소스에 있는 경우, 예를 들어 코드 줄을 작성 하지 않고 해당 값을 입력 매개 변수에 바인딩할 수 있습니다.

그러나 매개 변수 값이 기본 제공 데이터 원본 `Parameter` 개체 중 하나에서 이미 고려 되지 않은 일부 원본에서 제공 되는 경우가 있을 수 있습니다. 사이트에서 사용자 계정을 지 원하는 경우 현재 로그인 한 방문자의 사용자 ID를 기반으로 매개 변수를 설정 하는 것이 좋습니다. 또는 ObjectDataSource의 원본 개체의 메서드로 보내기 전에 매개 변수 값을 사용자 지정 해야 할 수도 있습니다.

Objectdatasource의 `Select` 메서드가 호출 될 때마다 ObjectDataSource는 먼저 [선택 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)를 발생 시킵니다. 그러면 ObjectDataSource의 내부 개체의 메서드가 호출 됩니다. 이 작업이 완료 되 면 ObjectDataSource의 [선택 된 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx) 발생 합니다 (그림 1에서는 이러한 이벤트 시퀀스를 보여 줍니다). ObjectDataSource의 기본 개체 메서드에 전달 된 매개 변수 값은 `Selecting` 이벤트에 대 한 이벤트 처리기에서 설정 하거나 사용자 지정할 수 있습니다.

[ObjectDataSource의 선택 된 이벤트와 기본 개체의 메서드를 호출 하기 전후에 발생 하는 이벤트를 선택 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**그림 1**: ObjectDataSource의 `Selected` 및 `Selecting` 이벤트는 기본 개체의 메서드를 호출 하기 전과 후에 발생 합니다 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png)).

이 자습서에서는 `Integer` 형식 `Month`단일 입력 매개 변수를 허용 하는 DAL 및 BLL에 메서드를 추가 하는 방법에 대해 설명 하 고, 지정 된 `Month`에서 채용 기념일이 있는 직원으로 채워진 `EmployeesDataTable` 개체를 반환 합니다. 이 예제에서는 현재 월을 기준으로이 매개 변수를 설정 하 여 "이번 달 직원 기념일" 목록을 표시 합니다.

시작 하겠습니다.

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>1 단계:`EmployeesTableAdapter`에 메서드 추가

첫 번째 예제에서는 지정 된 월에 `HireDate` 발생 한 직원을 검색 하는 수단을 추가 해야 합니다. 아키텍처에 따라이 기능을 제공 하려면 적절 한 SQL 문에 매핑되는 `EmployeesTableAdapter`에서 메서드를 먼저 만들어야 합니다. 이를 위해서는 먼저 Northwind 형식화 된 데이터 집합을 엽니다. `EmployeesTableAdapter` 레이블을 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 합니다.

[EmployeesTableAdapter에 새 쿼리를 추가 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**그림 2**: `EmployeesTableAdapter`에 새 쿼리 추가 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png))

행을 반환 하는 SQL 문을 추가 하려면 선택 합니다. `SELECT` 문 지정 화면에 도달 하면 `EmployeesTableAdapter`에 대 한 기본 `SELECT` 문이 이미 로드 됩니다. `WHERE` 절에를 추가 하기만 하면 됩니다. `WHERE DATEPART(m, HireDate) = @Month`. [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx) 는 `datetime` 형식의 특정 날짜 부분을 반환 하는 t-sql 함수입니다. 이 경우 `DATEPART`를 사용 하 여 `HireDate` 열의 월을 반환 합니다.

[HireDate 열이 @HiredBeforeDate 매개 변수 보다 작거나 같은 행만 반환 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**그림 3**: `HireDate` 열이 `@HiredBeforeDate` 매개 변수 보다 작거나 같은 행만 반환 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png))

마지막으로 `FillBy` 및 `GetDataBy` 메서드 이름을 각각 `FillByHiredDateMonth` 및 `GetEmployeesByHiredDateMonth`로 변경 합니다.

[![FillBy 및 GetDataBy 보다 더 적절 한 메서드 이름을 선택 합니다.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**그림 4**: `FillBy` 및 `GetDataBy` 보다 더 적합 한 방법 이름 선택 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png))

마침을 클릭 하 여 마법사를 완료 하 고 데이터 집합의 디자인 화면으로 돌아갑니다. 이제 `EmployeesTableAdapter`는 지정 된 월에 고용 된 직원에 게 액세스 하기 위한 새로운 메서드 집합을 포함 해야 합니다.

[새 메서드가 데이터 집합의 Design Surface에 표시 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**그림 5**: 데이터 집합의 Design Surface에 새 메서드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png)).

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층에`GetEmployeesByHiredDateMonth(month)`메서드 추가

응용 프로그램 아키텍처는 비즈니스 논리 및 데이터 액세스 논리에 별도의 계층을 사용 하기 때문에 DAL을 호출 하는 메서드를 BLL에 추가 하 여 지정 된 날짜 이전에 고용 된 직원을 검색 해야 합니다. `EmployeesBLL.vb` 파일을 열고 다음 메서드를 추가 합니다.

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

이 클래스의 다른 메서드와 마찬가지로 `GetEmployeesByHiredDateMonth(month)`는 DAL을 호출 하 고 결과를 반환 하기만 합니다.

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>3 단계: 채용 기념일이 이번 달 인 직원 표시

이 예제의 마지막 단계는 채용 기념일이 이번 달 인 직원을 표시 하는 것입니다. 먼저 `BasicReporting` 폴더의 `ProgrammaticParams.aspx` 페이지에 GridView를 추가 하 고 새 ObjectDataSource를 데이터 원본으로 추가 합니다. `GetEmployeesByHiredDateMonth(month)`로 설정 된 `SelectMethod`를 사용 하 여 `EmployeesBLL` 클래스를 사용 하도록 ObjectDataSource를 구성 합니다.

[EmployeesBLL 클래스를 사용 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**그림 6**: `EmployeesBLL` 클래스 사용 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png))

[GetEmployeesByHiredDateMonth (month) 메서드에서 Select를 ![합니다.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**그림 7**: `GetEmployeesByHiredDateMonth(month)` 메서드에서 선택 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png))

최종 화면은 `month` 매개 변수 값의 원본을 제공 하도록 요청 합니다. 이 값을 프로그래밍 방식으로 설정 하므로 매개 변수 원본을 기본 없음 옵션으로 설정 된 채로 두고 마침을 클릭 합니다.

[매개 변수 원본을 None으로 설정 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**그림 8**: 매개 변수 원본을 None으로 설정 된 상태로 유지 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png))

이렇게 하면 지정 된 값이 없는 ObjectDataSource의 `SelectParameters` 컬렉션에 `Parameter` 개체가 만들어집니다.

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

이 값을 프로그래밍 방식으로 설정 하려면 ObjectDataSource의 `Selecting` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이를 수행 하려면 디자인 뷰로 이동 하 여 ObjectDataSource를 두 번 클릭 합니다. 또는 ObjectDataSource를 선택 하 고 속성 창로 이동한 후 번개 아이콘을 클릭 합니다. 다음으로 `Selecting` 이벤트 옆의 텍스트 상자를 두 번 클릭 하거나 사용 하려는 이벤트 처리기의 이름을 입력 합니다. 세 번째 옵션으로 페이지의 코드 숨김이 클래스 맨 위에 있는 두 개의 드롭다운 목록에서 ObjectDataSource 및 해당 `Selecting` 이벤트를 선택 하 여 이벤트 처리기를 만들 수 있습니다.

![속성 창에서 번개 볼트 아이콘을 클릭 하 여 웹 컨트롤의 이벤트를 나열 합니다.](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**그림 9**: 속성 창에서 번개 볼트 아이콘을 클릭 하 여 웹 컨트롤의 이벤트 나열

세 가지 방법은 모두 ObjectDataSource의 `Selecting` 이벤트에 대 한 새 이벤트 처리기를 페이지의 코드 숨김이 클래스에 추가 합니다. 이 이벤트 처리기에서는 `e.InputParameters(parameterName)`를 사용 하 여 매개 변수 값을 읽고 쓸 수 있습니다. 여기서 *`parameterName`* 는 `<asp:Parameter>` 태그의 `Name` 특성 값입니다. `InputParameters`에서와 같이 `e.InputParameters(index)`컬렉션도 인덱싱할 수 서 수로 수 있습니다. `month` 매개 변수를 현재 달로 설정 하려면 `Selecting` 이벤트 처리기에 다음을 추가 합니다.

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

브라우저를 통해이 페이지를 방문 하는 경우 1994 이후 회사에 Callahan 한 명의 직원이이 월 (3 월)에 고용 된 것을 볼 수 있습니다.

[이 월에 해당 하는 기념일이 있는 직원 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**그림 10**: 이번 달의 월이 표시 된 직원 ([전체 크기 이미지를 보려면 클릭](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png))

## <a name="summary"></a>요약

ObjectDataSource의 매개 변수 값은 일반적으로 코드 줄을 요구 하지 않고 선언적으로 설정할 수 있지만 프로그래밍 방식으로 매개 변수 값을 설정 하는 것이 쉽습니다. 이렇게 하려면 기본 개체의 메서드를 호출 하기 전에 발생 하는 ObjectDataSource의 `Selecting` 이벤트에 대 한 이벤트 처리기를 만들고 `InputParameters` 컬렉션을 통해 하나 이상의 매개 변수에 대 한 값을 수동으로 설정 하기만 하면 됩니다.

이 자습서에서는 기본 보고 섹션을 마칩니다. [다음 자습서](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 에서는 방문자가 데이터를 필터링 하 고 마스터 보고서에서 세부 정보 보고서로 드릴 다운할 수 있도록 하는 기술을 살펴볼 수 있는 필터링 및 마스터-세부 정보 시나리오 섹션을 제공 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](declarative-parameters-vb.md)
