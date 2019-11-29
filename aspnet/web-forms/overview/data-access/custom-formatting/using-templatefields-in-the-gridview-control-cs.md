---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: GridView 컨트롤에서 서식 필드 사용 (C#) | Microsoft Docs
author: rick-anderson
description: 융통성을 제공 하기 위해 GridView는 템플릿을 사용 하 여 렌더링 하는 Templatefield로 변환을 제공 합니다. 템플릿에는 정적 HTML, 웹 컨트롤 등이 혼합 되어 포함 될 수 있습니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ec17a16d7bb487d1c5cacf2d5971bbeffc1ba031
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627776"
---
# <a name="using-templatefields-in-the-gridview-control-c"></a>GridView 컨트롤에서 TemplateFields 사용(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe) 또는 [PDF 다운로드](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> 융통성을 제공 하기 위해 GridView는 템플릿을 사용 하 여 렌더링 하는 Templatefield로 변환을 제공 합니다. 템플릿에는 정적 HTML, 웹 컨트롤 및 데이터 바인딩 구문이 혼합 되어 포함 될 수 있습니다. 이 자습서에서는 Templatefield로 변환를 사용 하 여 GridView 컨트롤을 사용 하 여 더 높은 수준의 사용자 지정을 수행 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

GridView는 데이터 표시 방법과 함께 렌더링 된 출력에 포함할 `DataSource` 속성을 나타내는 필드 집합으로 구성 됩니다. 가장 간단한 필드 형식은 데이터 값을 텍스트로 표시 하는 BoundField입니다. 다른 필드 형식은 대체 HTML 요소를 사용 하 여 데이터를 표시 합니다. 예를 들어, CheckBoxField는 지정 된 데이터 필드의 값에 따라 선택 된 상태를 갖는 checkbox로 렌더링 합니다. ImageField는 지정 된 데이터 필드를 기반으로 하는 이미지 소스가 있는 이미지를 렌더링 합니다. Hyperlink 필드 및 ButtonField 필드 형식을 사용 하 여 기본 데이터 필드 값에 의존 하는 상태를 가진 하이퍼링크 및 단추를 렌더링할 수 있습니다.

CheckBoxField, ImageField, hyperlink 필드 및 ButtonField 필드 형식은 데이터의 대체 보기를 허용 하지만 여전히 서식 지정에 대해 매우 제한적입니다. CheckBoxField는 단일 확인란만 표시할 수 있지만 ImageField는 단일 이미지만 표시할 수 있습니다. 특정 필드에서 다른 데이터 필드 값에 따라 일부 텍스트, 확인란 *및* 이미지를 표시 해야 하는 경우 어떻게 되나요? 또는 확인란, 이미지, 하이퍼링크 또는 단추가 아닌 다른 웹 컨트롤을 사용 하 여 데이터를 표시 하려는 경우 어떻게 하나요? 또한 BoundField는 단일 데이터 필드에 대 한 표시를 제한 합니다. 단일 GridView 열에 두 개 이상의 데이터 필드 값을 표시 하려는 경우 어떻게 하나요?

이러한 수준의 유연성을 수용 하기 위해 GridView는 *템플릿을*사용 하 여 렌더링 하는 templatefield로 변환을 제공 합니다. 템플릿에는 정적 HTML, 웹 컨트롤 및 데이터 바인딩 구문이 혼합 되어 포함 될 수 있습니다. 또한 Templatefield로 변환에는 다양 한 상황에 대 한 렌더링을 사용자 지정 하는 데 사용할 수 있는 다양 한 템플릿이 있습니다. 예를 들어 `ItemTemplate`는 기본적으로 각 행에 대 한 셀을 렌더링 하는 데 사용 되지만 `EditItemTemplate` 템플릿을 사용 하 여 데이터를 편집할 때 인터페이스를 사용자 지정할 수 있습니다.

이 자습서에서는 Templatefield로 변환를 사용 하 여 GridView 컨트롤을 사용 하 여 더 높은 수준의 사용자 지정을 수행 하는 방법을 살펴봅니다. [이전 자습서](custom-formatting-based-upon-data-cs.md) 에서는 `DataBound` 및 `RowDataBound` 이벤트 처리기를 사용 하 여 기본 데이터를 기반으로 서식을 지정 하는 방법을 살펴보았습니다. 기본 데이터를 기반으로 서식 지정을 사용자 지정 하는 또 다른 방법은 템플릿 내에서 서식 지정 메서드를 호출 하는 것입니다. 이 자습서에서는이 방법에 대해서도 살펴보겠습니다.

이 자습서에서는 템플릿 필드를 사용 하 여 직원 목록의 모양을 사용자 지정 합니다. 특히, 모든 직원을 나열 하지만 직원의 성과 이름을 한 열에 표시 하 고, 일정 컨트롤에서 고용 날짜를 표시 하 고, 회사에서 사용 된 일 수를 나타내는 상태 열을 표시 합니다.

[표시를 사용자 지정 하는 데 사용 되는 세 가지 템플릿 필드 ![](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**그림 1**: 표시를 사용자 지정 하는 데 사용 되는 세 가지 템플릿 필드 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image3.png))

## <a name="step-1-binding-the-data-to-the-gridview"></a>1 단계: 데이터를 GridView에 바인딩

서식 파일 필드를 사용 하 여 모양을 사용자 지정 해야 하는 보고 시나리오에서는 먼저 단순히 BoundFields를 포함 하는 GridView 컨트롤을 만든 다음 새 템플릿 필드를 추가 하거나 기존 BoundFields를로 변환 하 여 시작 하는 것이 가장 쉽습니다. 필요에 따라 템플릿 필드 따라서 디자이너를 통해 페이지에 GridView를 추가 하 고 직원 목록을 반환 하는 ObjectDataSource에 바인딩하여이 자습서를 시작 해 보겠습니다. 이러한 단계에서는 각 직원 필드에 대해 BoundFields를 사용 하 여 GridView를 만듭니다.

`GridViewTemplateField.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 옵니다. GridView의 스마트 태그에서 `EmployeesBLL` 클래스의 `GetEmployees()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤을 추가 하도록 선택 합니다.

[GetEmployees () 메서드를 호출 하는 새 ObjectDataSource 컨트롤을 추가 ![](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**그림 2**: `GetEmployees()` 메서드를 호출 하는 새 ObjectDataSource 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image6.png))

이러한 방식으로 GridView를 바인딩하면 `EmployeeID`, `LastName`, `FirstName`, `Title`, `HireDate`, `ReportsTo`, `Country`등의 각 직원 속성에 대해 BoundField가 자동으로 추가 됩니다. 이 보고서에서는 `EmployeeID`, `ReportsTo`또는 `Country` 속성을 표시 하지 않습니다. 이러한 BoundFields을 제거 하려면 다음을 수행할 수 있습니다.

- 필드 대화 상자를 사용 하 여 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여이 대화 상자를 표시 합니다. 다음으로 왼쪽 아래 목록에서 BoundFields를 선택 하 고 red X 단추를 클릭 하 여 BoundField를 제거 합니다.
- 원본 뷰에서 직접 GridView의 선언 구문을 편집 하 고 제거 하려는 BoundField에 대 한 `<asp:BoundField>` 요소를 삭제 합니다.

`EmployeeID`, `ReportsTo`및 `Country` BoundFields를 제거한 후 GridView의 태그는 다음과 같습니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

잠시 시간을 들 여 브라우저에서 진행률을 확인 하세요. 이 시점에서 각 직원과 4 개의 열에 대 한 레코드가 포함 된 테이블이 표시 됩니다. 하나는 직원의 성에 대 한 레코드이 고, 그 중 하나는 이름이 고, 다른 하나는 직함입니다.

[LastName, FirstName, Title 및 HireDate 필드가 각 직원에 대해 표시 ![](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**그림 3**: 각 직원에 대해 `LastName`, `FirstName`, `Title`및 `HireDate` 필드가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image9.png)).

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>2 단계: 단일 열에 성과 이름을 표시 합니다.

현재 각 직원의 성과 이름이 별도의 열에 표시 됩니다. 대신 단일 열로 결합 하는 것이 좋을 수 있습니다. 이를 위해 Templatefield로 변환를 사용 해야 합니다. 새 Templatefield로 변환을 추가 하 고, 필요한 태그 및 데이터 바인딩 구문을 추가 하 고, `FirstName`를 삭제 하 고, BoundFields `LastName`를 삭제 `FirstName` 하거나, `LastName` 값을 포함 하도록 Templatefield로 변환을 편집한 후 `LastName` BoundField를 제거할 수 있습니다.

두 방법 모두 동일한 결과를 얻을 수 있지만, BoundField의 모양과 기능을 모방 하기 위해 변환에서 `ItemTemplate`를 자동으로 추가 하 고 웹 컨트롤과 `EditItemTemplate` 데이터 바인딩 구문을 사용 하 여 자동으로 BoundFields를 템플릿 필드로 변환 하는 것과 같습니다. 이는 변환 프로세스에서 몇 가지 작업을 수행 하기 때문에 Templatefield로 변환를 사용 하 여 더 많은 작업을 수행 해야 한다는 이점도 있습니다.

기존 BoundField을 Templatefield로 변환로 변환 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 필드 대화 상자를 만듭니다. 왼쪽 아래 모퉁이의 목록에서 변환할 BoundField을 선택한 다음 오른쪽 아래 모서리에 있는 "이 필드를 Templatefield로 변환로 변환" 링크를 클릭 합니다.

[필드 대화 상자에서 BoundField을 Templatefield로 변환로 변환 ![](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**그림 4**: 필드 대화 상자에서 BoundField을 templatefield로 변환로 변환 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image12.png))

계속 해 서 `FirstName` BoundField를 Templatefield로 변환로 변환 합니다. 이 변경 후에는 디자이너에 perceptive 차이점이 없습니다. BoundField을 Templatefield로 변환로 변환 하면 BoundField의 모양과 느낌을 유지 관리 하는 Templatefield로 변환 생성 되기 때문입니다. 디자이너에서이 시점에는 시각적 차이가 없지만이 변환 프로세스는 BoundField의 선언적 구문 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />`를 다음 Templatefield로 변환 구문으로 대체 했습니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

여기에서 볼 수 있듯이 Templatefield로 변환는 `Text` 속성이 `FirstName` 데이터 필드의 값으로 설정 된 레이블이 있는 `ItemTemplate`와 `Text` 속성이 `FirstName` 데이터 필드로 설정 된 TextBox 컨트롤과 `EditItemTemplate`를 포함 하는 두 개의 템플릿으로 구성 됩니다. 데이터 바인딩 구문-`<%# Bind("fieldName") %>`-데이터 필드 *`fieldName`* 지정 된 웹 컨트롤 속성에 바인딩되어 있음을 나타냅니다.

이 Templatefield로 변환에 `LastName` 데이터 필드 값을 추가 하려면 `ItemTemplate`에 다른 Label 웹 컨트롤을 추가 하 고 `Text` 속성을 `LastName`에 바인딩해야 합니다. 이는 직접 수행 하거나 디자이너를 통해 수행할 수 있습니다. 이렇게 하려면 적절 한 선언적 구문을 `ItemTemplate`에 추가 하기만 하면 됩니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

디자이너를 통해 추가 하려면 GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 합니다. GridView의 템플릿 편집 인터페이스가 표시 됩니다. 이 인터페이스의 스마트 태그는 GridView의 템플릿 목록입니다. 이 시점에는 하나의 Templatefield로 변환 있기 때문에 드롭다운 목록에 나열 된 유일한 템플릿은 `EmptyDataTemplate` 및 `PagerTemplate`와 함께 `FirstName` Templatefield로 변환에 대 한 템플릿입니다. 지정 된 경우 `EmptyDataTemplate` 템플릿은 GridView에 바인딩된 데이터에 결과가 없는 경우 GridView의 출력을 렌더링 하는 데 사용 됩니다. 지정 된 경우 `PagerTemplate`는 페이징을 지 원하는 GridView의 페이징 인터페이스를 렌더링 하는 데 사용 됩니다.

[디자이너를 통해 GridView의 템플릿을 편집할 수 ![](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**그림 5**: 디자이너를 통해 GridView의 템플릿을 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image15.png)).

또한 `FirstName` Templatefield로 변환 `LastName` 표시 하려면 레이블 컨트롤을 도구 상자에서 GridView의 템플릿 편집 인터페이스에 있는 `FirstName` Templatefield로 변환의 `ItemTemplate` 끌어 옵니다.

[FirstName Templatefield로 변환의 ItemTemplate에 Label 웹 컨트롤을 추가 ![](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**그림 6**: `FirstName` Templatefield로 변환의 ItemTemplate에 Label 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image18.png))

이 시점에서 Templatefield로 변환에 추가 된 레이블 웹 컨트롤의 `Text` 속성은 "레이블"으로 설정 됩니다. 이 속성을 변경 하 여이 속성이 `LastName` 데이터 필드의 값에 바인딩되어야 합니다. 이를 수행 하려면 레이블 컨트롤의 스마트 태그를 클릭 하 고 데이터 바인딩 편집 옵션을 선택 합니다.

[레이블의 스마트 태그에서 데이터 바인딩 편집 옵션을 선택 ![.](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**그림 7**: 레이블의 스마트 태그에서 데이터 바인딩 편집 옵션 선택 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image21.png))

그러면 데이터 바인딩 대화 상자가 표시 됩니다. 여기에서 왼쪽의 목록에서 데이터 바인딩에 참여할 속성을 선택 하 고 오른쪽의 드롭다운 목록에서 데이터를 바인딩할 필드를 선택할 수 있습니다. 왼쪽에서 `Text` 속성을 선택 하 고 오른쪽에서 `LastName` 필드를 선택 하 고 확인을 클릭 합니다.

[텍스트 속성을 LastName 데이터 필드에 ![바인딩합니다.](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**그림 8**: `LastName` 데이터 필드에 `Text` 속성 바인딩 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image24.png))

> [!NOTE]
> 데이터 바인딩 대화 상자를 사용 하 여 양방향 데이터 바인딩을 수행할지 여부를 지정할 수 있습니다. 이 확인란을 선택 하지 않으면 데이터 바인딩 구문이 `<%# Bind("LastName")%>`대신 사용 됩니다 `<%# Eval("LastName")%>`. 이 자습서에서는 어떤 방법으로도 충분 합니다. 데이터를 삽입 하 고 편집할 때 양방향 데이터 바인딩은 중요 합니다. 그러나 단순히 데이터를 표시 하는 경우에도 두 방법 중 하나는 동일 하 게 작동 합니다. 이후 자습서에서 양방향 데이터 바인딩을 자세히 설명 합니다.

잠시 시간을 사용 하 여 브라우저를 통해이 페이지를 봅니다. 여기에서 볼 수 있듯이 GridView에는 네 개의 열이 포함 되어 있습니다. 그러나 `FirstName` 열에는 `FirstName` 및 `LastName` 데이터 필드 값이 *모두* 나열 됩니다.

[FirstName 및 LastName 값이 모두 단일 열에 표시 ![](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**그림 9**: `FirstName` 및 `LastName` 값이 모두 단일 열에 표시 됨 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image27.png))

이 첫 번째 단계를 완료 하려면 BoundField `LastName`를 제거 하 고 `FirstName` Templatefield로 변환의 `HeaderText` 속성 이름을 "Name"으로 바꿉니다. 이러한 변경 후 GridView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]

[각 사원의 성과 이름이 한 열에 표시 ![](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**그림 10**: 각 직원의 성과 이름이 하나의 열에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image30.png)).

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>3 단계: 달력 컨트롤을 사용 하 여`HiredDate`필드 표시

GridView에서 데이터 필드 값을 텍스트로 표시 하는 것은 BoundField를 사용 하는 것 만큼 간단 합니다. 그러나 특정 시나리오의 경우 데이터는 단순히 텍스트 대신 특정 웹 컨트롤을 사용 하 여 가장 잘 표현 됩니다. 이러한 데이터 표시는 템플릿 필드를 사용 하 여 사용자 지정할 수 있습니다. 예를 들어 직원의 고용 날짜를 텍스트로 표시 하는 대신 달력 [컨트롤](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)을 사용 하 여 고용 날짜가 강조 표시 된 달력을 표시할 수 있습니다.

이를 수행 하려면 먼저 `HiredDate` BoundField를 Templatefield로 변환로 변환 합니다. GridView의 스마트 태그로 이동 하 고 열 편집 링크를 클릭 하 여 필드 대화 상자를 만들면 됩니다. `HiredDate` BoundField를 선택 하 고 "이 필드를 Templatefield로 변환로 변환"을 클릭 합니다.

[HiredDate BoundField를 Templatefield로 변환으로 변환 ![](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**그림 11**: `HiredDate` BoundField을 templatefield로 변환로 변환 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image33.png))

2 단계에서 살펴본 것 처럼이 경우 BoundField이 `ItemTemplate` 포함 된 Templatefield로 변환로 대체 되 고 `EditItemTemplate` 데이터 바인딩 `<%# Bind("HiredDate")%>`구문을 사용 하 여 `Text` 속성이 `HiredDate` 값에 바인딩되는 레이블 및 텍스트 상자가 사용 됩니다.

텍스트를 달력 컨트롤로 바꾸려면 레이블을 제거 하 고 달력 컨트롤을 추가 하 여 템플릿을 편집 합니다. 디자이너에서 GridView의 스마트 태그에서 템플릿 편집을 선택 하 고 드롭다운 목록에서 `HireDate` Templatefield로 변환의 `ItemTemplate`를 선택 합니다. 그런 다음 레이블 컨트롤을 삭제 하 고 달력 컨트롤을 도구 상자에서 템플릿 편집 인터페이스로 끌어 옵니다.

[HireDate Templatefield로 변환의 ItemTemplate에 Calendar 컨트롤을 추가 ![](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**그림 12**: `HireDate` templatefield로 변환의 `ItemTemplate`에 일정 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image36.png))

이 시점에서 GridView의 각 행은 `HiredDate` Templatefield로 변환에 달력 컨트롤을 포함 합니다. 그러나 employee의 실제 `HiredDate` 값은 달력 컨트롤의 아무 곳에 나 설정 되지 않으므로 각 달력 컨트롤이 기본값을 설정 하 여 현재 월 및 날짜를 표시 합니다. 이를 해결 하려면 각 직원의 `HiredDate`을 Calendar 컨트롤의 [SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx) 및 [VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx) 속성에 할당 해야 합니다.

Calendar 컨트롤의 스마트 태그에서 데이터 바인딩 편집을 선택 합니다. 그런 다음 `SelectedDate` 및 `VisibleDate` 속성을 `HiredDate` 데이터 필드에 바인딩합니다.

[SelectedDate 및 VisibleDate 속성을 HiredDate 데이터 필드에 바인딩 ![](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**그림 13**: `SelectedDate` 및 `VisibleDate` 속성을 `HiredDate` 데이터 필드에 바인딩 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image39.png))

> [!NOTE]
> 달력 컨트롤의 선택 된 날짜를 반드시 표시 해야 하는 것은 아닙니다. 예를 들어 달력은 선택한 날짜로 1999 년 8<sup>월 1 일을 가질</sup>수 있지만 현재 월과 연도를 표시 합니다. 선택한 날짜와 표시 날짜는 달력 컨트롤의 `SelectedDate` 및 `VisibleDate` 속성에 의해 지정 됩니다. 직원의 `HiredDate`을 선택 하 고 표시 되는지 확인 하려면 이러한 속성을 모두 `HireDate` 데이터 필드에 바인딩해야 합니다.

브라우저에서 페이지를 볼 때 달력에는 직원 고용 날짜의 월이 표시 되 고 해당 날짜가 선택 됩니다.

[직원의 HiredDate이 달력 컨트롤에 표시 ![](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**그림 14**: 달력 컨트롤에 직원의 `HiredDate` 표시 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image42.png))

> [!NOTE]
> 지금까지 살펴본 모든 예제와 반대로이 자습서에서는이 GridView에 대해 `EnableViewState` 속성을 `false`로 설정 *하지* 않았습니다. 이렇게 결정 하는 이유는 달력 컨트롤의 날짜를 클릭 하면 포스트백이 발생 하므로 달력의 선택 된 날짜를 단순히 클릭 한 날짜로 설정 하기 때문입니다. 그러나 GridView의 뷰 상태를 사용할 수 없는 경우에는 각 다시 게시에서 GridView의 데이터를 기본 데이터 원본에 다시 바인딩할 수 있습니다. 그러면 사용자가 선택한 날짜를 덮어써서 달력의 선택한 날짜가 직원의 `HireDate`으로 *다시* 설정 됩니다.

이 자습서에서는 사용자가 직원의 `HireDate`를 업데이트할 수 없기 때문에 불과할 토론입니다. 날짜를 선택할 수 없도록 달력 컨트롤을 구성 하는 것이 가장 좋을 수 있습니다. 이 자습서에서는 특정 기능을 제공 하기 위해 뷰 상태를 사용 하도록 설정 해야 하는 상황을 보여 줍니다.

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>4 단계: 직원이 회사에 근무 하는 일 수 표시

지금까지 템플릿 필드의 두 가지 응용 프로그램을 살펴보았습니다.

- 두 개 이상의 데이터 필드 값을 하나의 열로 결합
- 텍스트 대신 웹 컨트롤을 사용 하 여 데이터 필드 값 표현

세 번째 템플릿 필드 사용은 GridView의 기본 데이터에 대 한 메타 데이터를 표시 하는 것입니다. 예를 들어 직원 채용 날짜를 표시 하는 것 외에도 작업에 포함 된 총 일 수를 표시 하는 열이 있을 수 있습니다.

그러나 기본 데이터를 데이터베이스에 저장 된 형식과 다르게 표시 해야 하는 경우에도 다른 템플릿 필드를 사용 하는 경우가 있습니다. `Employees` 테이블에 `M` 문자를 저장 하는 `Gender` 필드가 있거나 직원의 성별을 나타내는 `F` 있는 것으로 가정 합니다. 이 정보를 웹 페이지에 표시 하는 경우 "M" 또는 "F"와는 달리 성별을 "남성" 또는 "여성"으로 표시 하는 것이 좋습니다.

ASP.NET 페이지의 코드를 만든 클래스 (또는 `static` 메서드로 구현 되는 별도의 클래스 라이브러리)에서 서식 *지정 메서드* 를 만들어 이러한 두 가지 시나리오를 처리할 수 있습니다. 이러한 서식 지정 메서드는 앞에서 살펴본 것과 동일한 데이터 바인딩 구문을 사용 하 여 템플릿에서 호출 됩니다. 서식 지정 메서드는 원하는 수의 매개 변수를 사용할 수 있지만 문자열을 반환 해야 합니다. 이 반환 된 문자열은 템플릿에 삽입 되는 HTML입니다.

이러한 개념을 설명 하기 위해 자습서를 늘려 직원이 작업에서 발생 한 총 일 수를 나열 하는 열을 표시 해 보겠습니다. 이 형식 지정 메서드는 `Northwind.EmployeesRow` 개체를 사용 하 여 직원이 문자열로 사용 된 일 수를 반환 합니다. 이 메서드는 ASP.NET 페이지의 코드 뒤 클래스에 추가할 수 있지만 템플릿에서 액세스할 수 있도록 `protected` 또는 `public`로 표시 되어야 *합니다* .

[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

`HiredDate` 필드에 `NULL` 데이터베이스 값이 포함 될 수 있으므로 먼저 계산을 계속 하기 전에 값이 `NULL` 되지 않도록 해야 합니다. `HiredDate` 값이 `NULL`경우 "알 수 없음" 문자열을 반환 합니다. `NULL`되지 않은 경우 현재 시간과 `HiredDate` 값 간의 차이를 계산 하 고 일 수를 반환 합니다.

이 메서드를 활용 하려면 데이터 바인딩 구문을 사용 하 여 GridView의 Templatefield로 변환에서 호출 해야 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 고 새 Templatefield로 변환를 추가 하 여 GridView에 새 Templatefield로 변환를 추가 합니다.

[새 Templatefield로 변환를 GridView에 추가 ![](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**그림 15**: GridView에 새 templatefield로 변환 추가 ([전체 크기 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image45.png))

이 new Templatefield로 변환의 `HeaderText` 속성을 "작업에서 일"로 설정 하 고 해당 `ItemStyle`의 `HorizontalAlign` 속성을 `Center`로 설정 합니다. 템플릿에서 `DisplayDaysOnJob` 메서드를 호출 하려면 `ItemTemplate`를 추가 하 고 다음 데이터 바인딩 구문을 사용 합니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem`는 `GridViewRow`에 바인딩된 `DataSource` 레코드에 해당 하는 `DataRowView` 개체를 반환 합니다. 해당 `Row` 속성은 `DisplayDaysOnJob` 메서드로 전달 되는 강력한 형식의 `Northwind.EmployeesRow`을 반환 합니다. 이 데이터 바인딩 구문은 아래 선언 구문에서와 같이 `ItemTemplate`에 직접 표시 되거나 Label 웹 컨트롤의 `Text` 속성에 할당 될 수 있습니다.

> [!NOTE]
> 또는 `EmployeesRow` 인스턴스를 전달 하는 대신 `<%# DisplayDaysOnJob(Eval("HireDate")) %>`를 사용 하 여 `HireDate` 값을 전달 하면 됩니다. 그러나 `Eval` 메서드는 `object`를 반환 하므로 대신 `object`형식의 입력 매개 변수를 허용 하도록 `DisplayDaysOnJob` 메서드 시그니처를 변경 해야 합니다. `Employees` 테이블의 `HireDate` 열에 `NULL` 값이 포함 될 수 있으므로 `DateTime`에 대 한 `Eval("HireDate")` 호출을 무조건 캐스팅할 수 없습니다. 따라서 `DisplayDaysOnJob` 메서드에 대 한 입력 매개 변수로 `object`를 수락 하 고, 데이터베이스 `NULL` 값 (`Convert.IsDBNull(objectToCheck)`를 사용 하 여 수행할 수 있음)이 있는지 확인 한 다음 그에 따라 계속 진행 해야 합니다.

이러한 미묘한 이유로 인해 전체 `EmployeesRow` 인스턴스를 전달 하도록 옵트인 했습니다. 다음 자습서에서는 형식 지정 메서드에 입력 매개 변수를 전달 하는 데 `Eval("columnName")` 구문을 사용 하기 위한 더 많은 맞춤 예제를 확인할 수 있습니다.

다음은 Templatefield로 변환이 추가 되 고 `ItemTemplate`에서 호출 된 `DisplayDaysOnJob` 메서드인 GridView에 대 한 선언적 구문을 보여 줍니다.

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

그림 16은 브라우저를 통해 볼 때 완료 된 자습서를 보여 줍니다.

[직원 들이 작업에 대해 발생 한 일 수를 ![표시 합니다.](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**그림 16**: 작업에서 직원이 표시 된 일 수 ([전체 이미지를 보려면 클릭](using-templatefields-in-the-gridview-control-cs/_static/image48.png))

## <a name="summary"></a>요약

GridView 컨트롤의 Templatefield로 변환를 사용 하면 다른 필드 컨트롤에서 사용할 수 있는 것 보다 더 많은 유연성을 제공 하 여 데이터를 표시할 수 있습니다. 템플릿 필드는 다음과 같은 상황에 적합 합니다.

- 하나의 GridView 열에 여러 데이터 필드를 표시 해야 합니다.
- 데이터는 일반 텍스트가 아닌 웹 컨트롤을 사용 하 여 가장 잘 표현 됩니다.
- 출력은 메타 데이터를 표시 하거나 데이터를 다시 포맷 하는 등의 기본 데이터에 따라 달라 집니다.

데이터 표시를 사용자 지정 하는 것 외에도 다음 자습서에서 볼 수 있는 것 처럼 데이터를 편집 하 고 삽입 하는 데 사용 되는 사용자 인터페이스를 사용자 지정 하는 데에도 템플릿 필드가 사용 됩니다.

다음 두 자습서에서는 DetailsView에서 템플릿 필드 사용을 참조 하 여 템플릿을 계속 탐색 합니다. 다음으로, 필드 대신 템플릿을 사용 하 여 데이터의 레이아웃 및 구조에 더 많은 유연성을 제공 하는 FormView로 전환 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dan Jagers입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](custom-formatting-based-upon-data-cs.md)
> [다음](using-templatefields-in-the-detailsview-control-cs.md)
