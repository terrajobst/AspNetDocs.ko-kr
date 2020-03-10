---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: 데이터 바인딩된 컨트롤 | Microsoft Docs
author: microsoft
description: 대부분의 ASP.NET 응용 프로그램은 백 엔드 데이터 원본에서 일정 수준의 데이터 표현을 사용 합니다. 데이터 바인딩된 컨트롤은 상호 작용 하는 pivotal 부분입니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 1154b38e0fa3d9d56cb407ae659c3b0d69871fda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78488873"
---
# <a name="data-bound-controls"></a>데이터 바인딩 컨트롤

[Microsoft](https://github.com/microsoft) 에서

> 대부분의 ASP.NET 응용 프로그램은 백 엔드 데이터 원본에서 일정 수준의 데이터 표현을 사용 합니다. 데이터 바인딩된 컨트롤은 동적 웹 응용 프로그램의 데이터와 상호 작용 하는 데 pivotal 된 부분입니다. ASP.NET 2.0에는 새로운 BaseDataBoundControl 클래스 및 선언적 구문을 비롯 하 여 데이터 바인딩된 컨트롤에 대 한 몇 가지 상당한 향상 된 기능이 도입 되었습니다.

대부분의 ASP.NET 응용 프로그램은 백 엔드 데이터 원본에서 일정 수준의 데이터 표현을 사용 합니다. 데이터 바인딩된 컨트롤은 동적 웹 응용 프로그램의 데이터와 상호 작용 하는 데 pivotal 된 부분입니다. ASP.NET 2.0에는 새로운 BaseDataBoundControl 클래스 및 선언적 구문을 비롯 하 여 데이터 바인딩된 컨트롤에 대 한 몇 가지 상당한 향상 된 기능이 도입 되었습니다.

BaseDataBoundControl는 DataBoundControl 클래스 및 HierarchicalDataBoundControl 클래스의 기본 클래스 역할을 합니다. 이 모듈에서는 DataBoundControl에서 파생 되는 다음 클래스에 대해 설명 합니다.

- AdRotator
- 목록 컨트롤
- GridView
- FormView
- DetailsView

HierarchicalDataBoundControl 클래스에서 파생 되는 다음 클래스에 대해서도 설명 합니다.

- TreeView
- 메뉴
- SiteMapPath

## <a name="databoundcontrol-class"></a>DataBoundControl 클래스

DataBoundControl 클래스는 테이블 형식 또는 목록 스타일 데이터와 상호 작용 하는 데 사용 되는 추상 클래스 (VB에서는 MustInherit로 표시 됨)입니다. 다음 컨트롤은 DataBoundControl에서 파생 되는 컨트롤 중 일부입니다.

## <a name="adrotator"></a>AdRotator

AdRotator 컨트롤을 사용 하면 특정 URL에 연결 된 웹 페이지에 그래픽 배너를 표시할 수 있습니다. 표시 되는 그래픽은 컨트롤에 대 한 속성을 사용 하 여 회전 됩니다. 페이지에 표시 되는 특정 광고의 빈도는 **노출** 속성을 사용 하 여 구성할 수 있으며, 광고는 키워드 필터링을 사용 하 여 필터링 할 수 있습니다.

AdRotator 컨트롤은 데이터에 대해 XML 파일 또는 데이터베이스의 테이블을 사용 합니다. 다음 특성은 XML 파일에서 AdRotator 컨트롤을 구성 하는 데 사용 됩니다.

### <a name="imageurl"></a>ImageUrl
광고에 대해 표시할 이미지의 URL입니다.

### <a name="navigateurl"></a>NavigateUrl
광고를 클릭 했을 때 사용자가 수행 해야 하는 URL입니다. URL로 인코딩해야 합니다.

### <a name="alternatetext"></a>AlternateText
도구 설명에 표시 되 고 화면 판독기에서 읽는 대체 텍스트입니다. ImageUrl에서 지정한 이미지를 사용할 수 없는 경우에도 표시 됩니다.

### <a name="keyword"></a>키워드
키워드 필터링을 사용 하는 경우 사용할 수 있는 키워드를 정의 합니다. 지정 된 경우 키워드 필터와 일치 하는 키워드가 있는 광고만 표시 됩니다.

### <a name="impressions"></a>갖게
특정 광고가 나타날 수 있는 빈도를 결정 하는 가중치입니다. 동일한 파일에서 다른 광고의 인상을 기준으로 합니다. XML 파일에 있는 모든 광고의 최대값은 20억4800만 1입니다.

### <a name="height"></a>높이
광고의 높이 (픽셀)입니다.

### <a name="width"></a>너비
광고의 너비 (픽셀)입니다.

> [!NOTE]
> Height 및 Width 특성은 AdRotator 컨트롤 자체의 높이와 너비를 재정의 합니다.

일반적인 XML 파일은 다음과 같습니다.

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

위의 예제에서 Contoso의 ad는 ASP.NET 웹 사이트에 대 한 광고로 두 번 나타날 가능성이 높습니다.

위의 XML 파일에서 광고를 표시 하려면 다음과 같이 AdRotator 컨트롤을 페이지에 추가 하 고 **AdvertisementFile** 속성을 XML 파일을 가리키도록 설정 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

데이터베이스 테이블을 AdRotator 컨트롤의 데이터 원본으로 사용 하도록 선택 하는 경우 먼저 다음 스키마를 사용 하 여 데이터베이스를 설정 해야 합니다.

| **열 이름** | **데이터 형식** | **설명** |
| --- | --- | --- |
| ID | int | 기본 키입니다. 이 열에는 임의의 이름을 사용할 수 있습니다. |
| ImageUrl | nvarchar (*길이*) | 광고에 대해 표시할 이미지의 상대 또는 절대 URL입니다. |
| NavigateUrl | nvarchar (*길이*) | 광고에 대 한 대상 URL입니다. 값을 제공 하지 않으면 광고가 하이퍼링크가 아닙니다. |
| AlternateText | nvarchar (*길이*) | 이미지를 찾을 수 없는 경우 표시 되는 텍스트입니다. 일부 브라우저에서는 텍스트가 도구 설명으로 표시 됩니다. 대체 텍스트는 그래픽을 볼 수 없는 사용자가 해당 설명을 소리내어 읽을 수 있도록 접근성에도 사용 됩니다. |
| 키워드 | nvarchar (*길이*) | 페이지를 필터링 할 수 있는 광고의 범주입니다. |
| 갖게 | int(4) | 광고가 표시 되는 빈도를 나타내는 숫자입니다. 숫자가 클수록 광고는 더 자주 표시 됩니다. XML 파일에 있는 모든 상대 값의 합계는 20억4800만-1을 초과 하지 않을 수 있습니다. |
| 너비 | int(4) | 이미지의 너비 (픽셀)입니다. |
| 높이 | int(4) | 이미지의 높이 (픽셀)입니다. |

다른 스키마를 사용 하는 데이터베이스가 이미 있는 경우에는 **AlternateTextField**, **ImageUrlField**및 **NavigateUrlField** 속성을 사용 하 여 AdRotator 특성을 기존 데이터베이스에 매핑할 수 있습니다. AdRotator 컨트롤의 데이터베이스에서 데이터를 표시 하려면 데이터 소스 컨트롤을 페이지에 추가 하 고, 데이터 소스 컨트롤이 데이터베이스를 가리키도록 연결 문자열을 구성 하 고, AdRotator 컨트롤의 **DataSourceID** 속성을 데이터 소스 컨트롤의 ID로 설정 합니다. 프로그래밍 방식으로 AdRotator 광고를 구성 해야 하는 경우 AdCreated 이벤트를 사용 합니다. AdCreated 이벤트는 두 개의 매개 변수를 사용 합니다. 하나는 개체이 고 다른 하나는 AdCreatedEventArgs 인스턴스입니다. AdCreatedEventArgs는 만들어지는 ad에 대 한 참조입니다.

다음 코드 조각에서는 광고에 대해 프로그래밍 방식으로 NavigateUrl 및 AlternateText를 설정 합니다.

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>목록 컨트롤

목록 컨트롤에는 ListBox, DropDownList, CheckBoxList, RadioButtonList 및 BulletedList가 포함 됩니다. 이러한 각 컨트롤은 데이터 소스에 바인딩된 데이터 일 수 있습니다. 데이터 원본에서 필드 하나를 표시 텍스트로 사용 하 고 선택적으로 두 번째 필드를 항목의 값으로 사용할 수 있습니다. 디자인 타임에 항목을 정적으로 추가 하 고 정적 항목과 데이터 원본에서 추가 된 동적 항목을 혼합할 수 있습니다.

목록 컨트롤에 데이터를 바인딩하려면 페이지에 데이터 소스 컨트롤을 추가 합니다. 데이터 소스 컨트롤에 대해 SELECT 명령을 지정한 다음 목록 컨트롤의 DataSourceID 속성을 데이터 소스 컨트롤의 ID로 설정 합니다. **DataTextField** 및 **datavaluefield** 속성을 사용 하 여 컨트롤의 표시 텍스트 및 값을 정의 합니다. 또한 다음과 같이 **DataTextFormatString** 속성을 사용 하 여 표시 텍스트의 모양을 제어할 수 있습니다.

| **식** | **설명** |
| --- | --- |
| 가격: {0:C} | 숫자/10 진수 데이터의 경우 리터럴 "Price:"와 통화 형식으로 숫자를 표시 합니다. 통화 형식은 **Page** 지시문 또는 web.config 파일의 culture 특성에 지정 된 문화권 설정에 따라 달라 집니다. |
| {0:D4} | 정수 데이터의 경우 는 10 진수와 함께 사용할 수 없습니다. 정수는 0부터 시작 하는 0으로 채워진 필드에 표시 됩니다. |
| {0:N2}% | 숫자 데이터의 경우 소수점이 하 두 자리까지 표시 된 숫자와 리터럴 "%"를 표시 합니다. |
| {0:000.0} | 숫자/10 진수 데이터의 경우 숫자는 하나의 소수 자릿수로 반올림 됩니다. 세 자리보다 작은 숫자는 0으로 채워집니다. |
| {0:D} | 날짜/시간 데이터의 경우 자세한 날짜 형식 ("목요일, 8 월 06, 1996")을 표시 합니다. 날짜 형식은 page 지시문 또는 Web.config 파일의 문화권 설정에 따라 달라집니다. |
| {0:d} | 날짜/시간 데이터의 경우 간단한 날짜 형식 ("12/31/99")을 표시 합니다. |
| {0:yy-MM-dd} | 날짜/시간 데이터의 경우 날짜를 숫자 연도-월-일 형식으로 표시 합니다 (96-08-06). |

## <a name="gridview"></a>GridView

GridView 컨트롤은 선언적 방법을 사용 하 여 표 형식 데이터 표시 및 편집을 허용 하며 DataGrid 컨트롤의 후속 작업입니다. GridView 컨트롤에서 사용할 수 있는 기능은 다음과 같습니다.

- SqlDataSource와 같은 데이터 소스 컨트롤에 바인딩합니다.
- 기본 제공 정렬 기능이 있습니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 기본 제공 행 선택 기능입니다.
- 동적으로 속성을 설정 하 고 이벤트를 처리 하는 등을 위해 GridView 개체 모델에 대 한 프로그래밍 방식 액세스
- 여러 키 필드입니다.
- 하이퍼링크 열에 대 한 여러 데이터 필드입니다.
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

**열 필드**

GridView 컨트롤의 각 열은 DataControlField 개체로 표현 됩니다. 기본적으로 AutoGenerateColumns 속성은 **true**로 설정 됩니다. 그러면 데이터 원본의 각 필드에 대해 AutoGeneratedField 개체가 만들어집니다. 각 필드는 데이터 원본에 각 필드가 표시 되는 순서 대로 GridView 컨트롤의 열로 렌더링 됩니다. **AutoGenerateColumns** 속성을 **false** 로 설정 하 고 고유한 열 필드 컬렉션을 정의 하 여 **GridView** 컨트롤에 표시 되는 열 필드를 수동으로 제어할 수도 있습니다. 열 필드 형식에 따라 컨트롤의 열의 동작을 결정 합니다.

다음 표에서 사용할 수 있는 다른 열 필드 유형을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본에서 필드의 값을 표시합니다. 이는 GridView 컨트롤의 기본 열 유형입니다. |
| ButtonField | GridView 컨트롤의 각 항목에 대 한 명령 단추를 표시 합니다. 이렇게 하면 추가 또는 제거 단추와 같은 사용자 지정 단추 컨트롤의 열을 만들 수 있습니다. |
| CheckBoxField | GridView 컨트롤의 각 항목에 대 한 확인란을 표시 합니다. 이 열 필드 형식은 부울 값을 사용 하 여 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | 작업 선택, 편집 또는 삭제 작업을 수행 하는 미리 정의 된 명령 단추를 표시 합니다. |
| HyperLinkField | 하이퍼링크로 데이터 원본의 필드의 값을 표시합니다. 이 열 필드 형식을 사용 하 여 두 번째 필드를 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | GridView 컨트롤의 각 항목에 대 한 이미지를 표시 합니다. |
| Templatefield로 변환 | 지정 된 템플릿에 따라 GridView 컨트롤의 각 항목에 대 한 사용자 정의 콘텐츠를 표시 합니다. 이 열 필드 형식을 사용 하면 사용자 지정 열 필드를 만들 수 있습니다. |

열 필드 컬렉션을 선언적으로 정의 하려면 먼저 GridView 컨트롤의 여는 태그와 닫는 태그 사이에 **&lt;열&gt;** 태그를 추가 합니다. 다음에는 여는 열과 닫는 **&lt;열&gt;** 태그 사이에 포함할 열 필드를 나열 합니다. 지정 된 열은 나열 된 순서 대로 Columns 컬렉션에 추가 됩니다. **Columns** 컬렉션은 컨트롤의 모든 열 필드를 저장 하 고 GridView 컨트롤의 열 필드를 프로그래밍 방식으로 관리할 수 있도록 합니다.

명시적으로 선언 된 열 필드를 자동으로 생성 된 열 필드와 함께에서 표시할 수 있습니다. 모두 사용 하는 명시적으로 선언 된 열 필드 뒤에 자동으로 생성 된 열 필드를 먼저 렌더링 됩니다.

## <a name="binding-to-data"></a>데이터 바인딩

GridView 컨트롤은 데이터 소스 제어 (예: **SqlDataSource**, **ObjectDataSource**등) 뿐만 아니라 system.object를 구현 하는 모든 데이터 소스 (예: System.object, collections 또는 system.object)에 바인딩될 수 있습니다 (예: system.object, collections). 다음 방법 중 하나를 사용 하 여 GridView 컨트롤을 적절 한 데이터 원본 형식에 바인딩합니다.

- 데이터 소스 컨트롤에 바인딩하려면 GridView 컨트롤의 DataSourceID 속성을 데이터 소스 컨트롤의 ID 값으로 설정 합니다. GridView 컨트롤은 지정 된 데이터 소스 컨트롤에 자동으로 바인딩되고 데이터 소스 컨트롤의 기능을 활용 하 여 정렬, 업데이트, 삭제 및 페이징 기능을 수행할 수 있습니다. 이것은 데이터 바인딩할 기본 방법입니다.
- System.object를 구현 하는 데이터 소스에 바인딩하려면 GridView 컨트롤의 DataSource 속성을 프로그래밍 방식으로 데이터 소스에 설정 하 고 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하는 경우 GridView 컨트롤은 기본 제공 정렬, 업데이트, 삭제 및 페이징 기능을 제공 하지 않습니다. 이 기능을 직접 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

GridView 컨트롤은 사용자가 컨트롤의 항목을 정렬 하 고, 업데이트 하 고, 삭제 하 고, 선택 하 고, 페이지를 이동할 수 있도록 하는 다양 한 기본 제공 기능을 제공 합니다. GridView 컨트롤이 데이터 소스 컨트롤에 바인딩되면 GridView 컨트롤이 데이터 소스 컨트롤의 기능을 활용 하 고 자동 정렬, 업데이트 및 삭제 기능을 제공할 수 있습니다.

> [!NOTE]
> GridView 컨트롤은 다른 형식의 데이터 원본에 대 한 정렬, 업데이트 및 삭제를 지원할 수 있습니다. 그러나 이러한 작업을 구현 하는 데 적절 한 이벤트 처리기를 제공 해야 합니다.

정렬을 사용 하면 사용자가 열 머리글을 클릭 하 여 특정 열에 대해 GridView 컨트롤의 항목을 정렬할 수 있습니다. 정렬을 사용 하려면 AllowSorting 속성을 **true**로 설정 합니다.

자동 업데이트, 삭제 및 선택 기능은 명령 이름이 "Edit", "Delete" 및 "Select" 인 **buttonfield** 또는 **templatefield로 변환** 열 필드의 단추가 각각 클릭 될 때 사용할 수 있습니다. AutoGenerateEditButton, AutoGenerateDeleteButton 또는 AutoGenerateSelectButton 속성이 각각 **true**로 설정 된 경우 GridView 컨트롤은 편집, 삭제 또는 선택 단추를 사용 하 여 **commandfield** 열 필드를 자동으로 추가할 수 있습니다.

> [!NOTE]
> 데이터 소스에 레코드를 삽입 하는 것은 GridView 컨트롤에서 직접 지원 되지 않습니다. 그러나 DetailsView 또는 FormView 컨트롤과 함께 GridView 컨트롤을 사용 하 여 레코드를 삽입할 수 있습니다.

GridView 컨트롤은 데이터 소스에 있는 모든 레코드를 동시에 표시 하는 대신 자동으로 레코드를 페이지로 분할할 수 있습니다. 페이징을 사용 하도록 설정 하려면 AllowPaging 속성을 **true**로 설정 합니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 파트에 대 한 스타일 속성을 설정 하 여 GridView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **Style 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | GridView 컨트롤의 교대로 반복 되는 데이터 행에 대 한 스타일 설정입니다. 이 속성을 설정 하면 행 스타일 설정과 **AlternatingRowStyle** 설정 사이에 데이터 행이 번갈아 표시 됩니다. |
| EditRowStyle | GridView 컨트롤에서 편집 중인 행의 스타일 설정입니다. |
| EmptyDataRowStyle | 데이터 원본에 레코드가 포함 되어 있지 않을 경우 GridView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | GridView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | GridView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| PagerStyle | GridView 컨트롤의 페이저 행에 대 한 스타일 설정입니다. |
| RowStyle | GridView 컨트롤의 데이터 행에 대 한 스타일 설정입니다. **AlternatingRowStyle** 속성도 설정 되어 있으면 **Rowstyle** 설정과 **AlternatingRowStyle** 설정 사이에 데이터 행이 번갈아 표시 됩니다. |
| SelectedRowStyle | GridView 컨트롤에서 선택한 행에 대 한 스타일 설정입니다. |

또한 표시 하거나 컨트롤의 다른 파트를 숨길 수 있습니다. 다음 표에서 표시 하거나 숨길는 부분을 제어 하는 속성을 보여 줍니다.

| **속성** | **설명** |
| --- | --- |
| ShowFooter | GridView 컨트롤의 바닥글 구역을 표시 하거나 숨깁니다. |
| ShowHeader | GridView 컨트롤의 머리글 구역을 표시 하거나 숨깁니다. |

### <a name="events"></a>이벤트

GridView 컨트롤은 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서는 GridView 컨트롤에서 지 원하는 이벤트를 보여 줍니다.

| **이벤트** | **설명** |
| --- | --- |
| PageIndexChanged | 페이저 단추 중 하나를 클릭 한 후 GridView 컨트롤이 페이징 작업을 처리 한 후에 발생 합니다. 이 이벤트는 사용자가 컨트롤에서 다른 페이지로 이동한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하면 GridView 컨트롤이 페이징 작업을 처리 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |
| RowCancelingEdit | 행의 취소 단추를 클릭 한 후 GridView 컨트롤이 편집 모드를 종료 하기 전에 발생 합니다. 이 이벤트는 대개 취소 작업을 중지 합니다. |
| RowCommand | GridView 컨트롤에서 단추를 클릭 하면 발생 합니다. 이 이벤트는 대개 컨트롤에서 단추를 클릭 하면 작업을 수행 합니다. |
| RowCreated | GridView 컨트롤에서 새 행을 만들 때 발생 합니다. 이 이벤트는 대개 행 만들어질 때 행의 내용을 수정 합니다. |
| RowDataBound | 데이터 행이 GridView 컨트롤의 데이터에 바인딩될 때 발생 합니다. 이 이벤트는 대개 행 데이터에 바인딩될 때 행의 내용을 수정 합니다. |
| RowDeleted | 행의 삭제 단추를 클릭 하면 GridView 컨트롤이 데이터 소스에서 레코드를 삭제 한 후에 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| RowDeleting | 행의 삭제 단추를 클릭 한 후 GridView 컨트롤이 데이터 소스에서 레코드를 삭제 하기 전에 발생 합니다. 이 이벤트는 삭제 작업을 취소 하는 경우가 많습니다. |
| RowEditing | 행의 편집 단추를 클릭 한 후 GridView 컨트롤이 편집 모드로 전환 되기 전에 발생 합니다. 이 이벤트는 편집 작업을 취소 하는 경우가 많습니다. |
| RowUpdated | 행의 업데이트 단추를 클릭 한 후 GridView 컨트롤이 행을 업데이트 한 후에 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| RowUpdating | 행의 업데이트 단추를 클릭 한 후 GridView 컨트롤이 행을 업데이트 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| SelectedIndexChanged | 행의 선택 단추를 클릭 한 후 GridView 컨트롤이 선택 작업을 처리 한 후에 발생 합니다. 이 이벤트는 대개 컨트롤에서 행을 선택한 후 작업을 수행 합니다. |
| SelectedIndexChanging | 행의 선택 단추를 클릭 한 후 GridView 컨트롤이 선택 작업을 처리 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 종종 선택 작업을 취소 하려면 사용 합니다. |
| 정렬 | 열을 정렬 하는 하이퍼링크를 클릭 하면 GridView 컨트롤이 정렬 작업을 처리 한 후에이 이벤트가 발생 합니다. 이 이벤트는 사용자가 하이퍼링크를 클릭 하 여 열을 정렬할 때 일반적으로 작업을 수행 하는 데 사용 됩니다. |
| 정렬 | 열을 정렬 하는 하이퍼링크를 클릭 하면 GridView 컨트롤이 정렬 작업을 처리 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 정렬 작업을 취소 하거나 정렬 루틴을 사용자 지정 하는 데 자주 사용 됩니다. |

## <a name="formview"></a>FormView

FormView 컨트롤은 데이터 소스에서 단일 레코드를 표시 하는 데 사용 됩니다. 이는 행 필드 대신 사용자 정의 템플릿을 표시 한다는 점을 제외 하 고 DetailsView 컨트롤과 유사 합니다. 사용자 고유의 템플릿 만들기 하면 더욱 유연 하 게 데이터가 표시 되는 방식을 제어 합니다. FormView 컨트롤은 다음과 같은 기능을 지원 합니다.

- SqlDataSource 및 ObjectDataSource와 같은 데이터 소스 컨트롤에 바인딩합니다.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 속성을 동적으로 설정 하 고 이벤트를 처리 하는 등의 방법으로 FormView 개체 모델에 대 한 프로그래밍 방식 액세스
- 사용자 정의 템플릿을, 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="templates"></a>템플릿

FormView 컨트롤에서 콘텐츠를 표시 하려면 컨트롤의 다른 파트에 대 한 템플릿을 만들어야 합니다. 대부분의 템플릿은 선택 사항입니다. 그러나 컨트롤이 구성 모드에 대 한 템플릿을 만들어야 합니다. 예를 들어 레코드 삽입을 지 원하는 FormView 컨트롤에는 삽입 항목 템플릿이 정의 되어 있어야 합니다. 다음 표에서 만들 수 있는 다양 한 템플릿을 나열 합니다.

| **템플릿 유형** | **설명** |
| --- | --- |
| EditItemTemplate | FormView 컨트롤이 편집 모드에 있을 때 데이터 행에 대 한 내용을 정의 합니다. 이 서식 파일에는 일반적으로 입력 컨트롤과 명령 단추가 있는 사용자가 기존 레코드를 편집할 수 포함 되어 있습니다. |
| EmptyDataTemplate | FormView 컨트롤이 레코드를 포함 하지 않는 데이터 소스에 바인딩될 때 표시 되는 빈 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 템플릿은 일반적으로 데이터 소스에 레코드가 없는지 사용자 경고는 콘텐츠를 포함 합니다. |
| FooterTemplate | 바닥글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿은 일반적으로 바닥글 행에 표시 하려는 모든 추가 콘텐츠를 포함 합니다. 대신 FooterText 속성을 설정 하 여 바닥글 행에 표시할 텍스트를 지정할 수 있습니다. |
| HeaderTemplate | 머리글 행에 대 한 콘텐츠를 정의합니다. 이 템플릿은 일반적으로 머리글 행에 표시 하려는 모든 추가 콘텐츠를 포함 합니다. 대신 HeaderText 속성을 설정 하 여 머리글 행에 표시할 텍스트를 지정할 수 있습니다. |
| ItemTemplate | FormView 컨트롤이 읽기 전용 모드에 있을 때 데이터 행에 대 한 콘텐츠를 정의 합니다. 이 템플릿은 일반적으로 기존 레코드의 값을 표시할 수 있는 콘텐츠를 포함 합니다. |
| InsertItemTemplate | FormView 컨트롤이 삽입 모드에 있을 때 데이터 행에 대 한 내용을 정의 합니다. 이 일반적으로 템플릿에 입력 컨트롤과 명령 단추가 있는 사용자는 새 레코드를 추가할 수 있습니다. |
| PagerTemplate | AllowPaging 속성이 **true**로 설정 된 경우 페이징 기능을 사용할 수 있을 때 표시 되는 페이저 행의 콘텐츠를 정의 합니다. 일반적으로이 템플릿을 다른 레코드를 탐색할 수 있는 사용자 컨트롤을 포함 합니다. |

항목 템플릿 편집 및 삽입 항목 템플릿이 입력된 컨트롤 양방향 바인딩 식을 사용 하 여 데이터 원본의 필드를 바인딩할 수 있습니다. 이렇게 하면 FormView 컨트롤이 업데이트 또는 삽입 작업에 대 한 입력 컨트롤의 값을 자동으로 추출할 수 있습니다. 또한 양방향 바인딩 식 편집 항목 템플릿에서 자동으로 필드의 원래 값을 표시 하려면 입력된 컨트롤을 수 있습니다.

### <a name="binding-to-data"></a>데이터 바인딩

FormView 컨트롤은 데이터 소스 제어 (예: **SqlDataSource**, AccessDataSource, **ObjectDataSource** 등) 또는 system.object를 구현 하는 모든 데이터 소스 (예: system.object, Collections, collections 및 system.object)에 바인딩될 수 있습니다 .이 컨트롤은. 다음 방법 중 하나를 사용 하 여 FormView 컨트롤을 적절 한 데이터 원본 형식에 바인딩합니다.

- 데이터 소스 컨트롤에 바인딩하려면 FormView 컨트롤의 DataSourceID 속성을 데이터 소스 컨트롤의 ID 값으로 설정 합니다. FormView 컨트롤이 지정 된 데이터 소스 컨트롤에 자동으로 바인딩되기 때문에 데이터 소스 컨트롤의 기능을 활용 하 여 삽입, 업데이트, 삭제 및 페이징 기능을 수행할 수 있습니다. 이것은 데이터 바인딩할 기본 방법입니다.
- **System.object** 를 구현 하는 데이터 소스에 바인딩하려면 FormView 컨트롤의 DataSource 속성을 프로그래밍 방식으로 데이터 원본으로 설정한 다음 DataBind 메서드를 호출 합니다. 이 메서드를 사용 하는 경우 FormView 컨트롤이 기본 제공 삽입, 업데이트, 삭제 및 페이징 기능을 제공 하지 않습니다. 적절 한 이벤트를 사용 하 여이 기능을 제공 해야 합니다.

## <a name="data-operations"></a>데이터 작업

FormView 컨트롤은 사용자가 컨트롤에서 항목을 업데이트, 삭제, 삽입 및 페이징 하는 데 사용할 수 있는 여러 가지 기본 제공 기능을 제공 합니다. FormView 컨트롤이 데이터 소스 컨트롤에 바인딩되면 FormView 컨트롤이 데이터 소스 컨트롤의 기능을 활용 하 고 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공할 수 있습니다. FormView 컨트롤은 다른 유형의 데이터 원본과의 업데이트, 삭제, 삽입 및 페이징 작업을 지원할 수 있습니다. 그러나 이러한 작업을 구현 하는 데 적절 한 이벤트 처리기를 제공 해야 합니다.

FormView 컨트롤은 템플릿을 사용 하기 때문에 업데이트, 삭제 또는 삽입 작업을 수행 하는 명령 단추를 자동으로 생성 하는 방법을 제공 하지 않습니다. 이러한 명령 단추에서 적절 한 템플릿을 수동으로 포함 해야 합니다. FormView 컨트롤은 **CommandName** 속성이 특정 값으로 설정 된 특정 단추를 인식 합니다. 다음 표에서는 FormView 컨트롤이 인식 하는 명령 단추를 보여 줍니다.

| **단추** | **Commandname 값** | **설명** |
| --- | --- | --- |
| 취소 | "취소" | 작업을 취소 하 고 사용자가 입력 한 값을 삭제 하려면 업데이트 또는 삽입 작업에 사용 합니다. 그러면 FormView 컨트롤이 DefaultMode 속성에 지정 된 모드로 돌아갑니다. |
| DELETE | "Delete" | 삭제 작업에 데이터 소스에서 표시 된 레코드를 삭제 하는 데 사용 합니다. ItemDeleting 및 Itemdeleting 이벤트를 발생 시킵니다. |
| 편집 | "Edit" | FormView 컨트롤을 편집 모드로 전환 하기 위해 업데이트 작업에 사용 됩니다. **EditItemTemplate** 속성에 지정 된 내용이 데이터 행에 대해 표시 됩니다. |
| 삽입 | "Insert" | 삽입 작업에 사용자가 입력 한 값을 사용 하 여 데이터 원본에 새 레코드를 삽입 하려고 하는 데 사용 합니다. ItemInserting 및 Iteminserting 이벤트를 발생 시킵니다. |
| 새로 만들기 | "New" | 삽입 작업에서 FormView 컨트롤을 삽입 모드로 전환 하는 데 사용 됩니다. **InsertItemTemplate** 속성에 지정 된 내용이 데이터 행에 대해 표시 됩니다. |
| 호출 | "Page" | 페이징 작업에서는 페이징을 수행 하는 페이저 행에 단추를 나타내는 하는 데 사용 합니다. 페이징 작업을 지정 하려면 단추의 **CommandArgument** 속성을 "Next", "Prev", "First", "Last" 또는 탐색할 페이지의 인덱스로 설정 합니다. PageIndexChanging 및 Pageindexchanging 이벤트를 발생 시킵니다. |
| 업데이트 | "업데이트" | 사용자가 입력 한 값을 사용 하 여 데이터 원본에 표시 된 레코드를 업데이트 하기 위해 업데이트 작업에 사용 합니다. ItemUpdating 및 ItemUpdated 이벤트를 발생 시킵니다. |

표시 된 레코드를 즉시 삭제 하는 삭제 단추와는 달리, 편집 또는 새로 만들기 단추를 클릭 하면 FormView 컨트롤이 각각 편집 또는 삽입 모드로 전환 됩니다. 편집 모드에서는 **EditItemTemplate** 속성에 포함 된 콘텐츠가 현재 데이터 항목에 대해 표시 됩니다. 일반적으로 항목 템플릿 편집 편집 단추를 업데이트 및 취소 단추를 사용 하 여 바뀝니다 되도록 정의 됩니다. 필드의 데이터 형식에 적합 한 입력 컨트롤 (예: TextBox 또는 CheckBox 컨트롤)은 사용자가 수정할 수 있는 필드의 값과 함께 일반적으로 표시 됩니다. 모든 변경 사항이 취소 단추를 클릭 데이터 원본에서 레코드를 업데이트 [업데이트] 단추를 클릭 합니다.

마찬가지로 컨트롤이 삽입 모드일 때 **InsertItemTemplate** 속성에 포함 된 콘텐츠가 데이터 항목에 대해 표시 됩니다. 삽입 항목 템플릿에 새 단추 삽입 및 취소 단추를 사용 하 여 대체 되 고 빈 입력된 컨트롤이 새 레코드에 대 한 값을 입력 하 여 사용자에 대해 표시 되는 일반적으로 정의 됩니다. 취소 단추를 클릭 하면 모든 변경 사항이 데이터 원본에서 레코드를 삽입 삽입 단추를 클릭 합니다.

FormView 컨트롤은 사용자가 데이터 소스의 다른 레코드를 탐색할 수 있도록 하는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이지 탐색 컨트롤을 포함 하는 FormView 컨트롤에 페이저 행이 표시 됩니다. 페이징을 사용 하도록 설정 하려면 **AllowPaging** 속성을 **true**로 설정 합니다. PagerStyle 및 PagerSettings 속성에 포함 된 개체의 속성을 설정 하 여 페이저 행을 사용자 지정할 수 있습니다. 기본 제공 페이저 행 UI를 사용 하는 대신 **PagerTemplate** 속성을 사용 하 여 ui를 직접 만들 수 있습니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 파트에 대 한 스타일 속성을 설정 하 여 FormView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **Style 속성** | **설명** |
| --- | --- |
| EditRowStyle | FormView 컨트롤이 편집 모드에 있을 때 데이터 행에 대 한 스타일 설정입니다. |
| EmptyDataRowStyle | 데이터 원본에 레코드가 포함 되어 있지 않은 경우 FormView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | FormView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | FormView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| InsertRowStyle | FormView 컨트롤이 삽입 모드일 때의 데이터 행에 대 한 스타일 설정입니다. |
| PagerStyle | 페이징 기능을 사용 하도록 설정한 경우 FormView 컨트롤에 표시 되는 페이저 행의 스타일 설정입니다. |
| RowStyle | FormView 컨트롤이 읽기 전용 모드에 있을 때의 데이터 행에 대 한 스타일 설정입니다. |

## <a name="events"></a>이벤트

FormView 컨트롤은 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서는 FormView 컨트롤에서 지 원하는 이벤트를 나열 합니다.

| **이벤트** | **설명** |
| --- | --- |
| ItemCommand | FormView 컨트롤의 단추를 클릭할 때 발생 합니다. 이 이벤트는 대개 컨트롤에서 단추를 클릭 하면 작업을 수행 합니다. |
| ItemCreated | FormView 컨트롤에서 모든 FormViewRow 개체를 만든 후에 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 삭제 단추 ( **CommandName** 속성이 "Delete"로 설정 된 단추)를 클릭 하면 FormView 컨트롤이 데이터 소스에서 레코드를 삭제 한 후에 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | [삭제] 단추를 클릭할 때 FormView 컨트롤이 데이터 소스에서 레코드를 삭제 하기 전에 발생 합니다. 이 이벤트는 삭제 작업을 취소 하려면 종종 사용 됩니다. |
| ItemInserted | 삽입 단추 ( **CommandName** 속성이 "Insert"로 설정 된 단추)를 클릭 하면 FormView 컨트롤이 레코드를 삽입 한 후에 발생 합니다. 이 이벤트는 대개 삽입 작업의 결과 확인 합니다. |
| ItemInserting | FormView 컨트롤이 레코드를 삽입 하기 전에 삽입 단추를 클릭 하면 발생 합니다. 이 이벤트는 삽입 작업을 취소 하려면 종종 사용 됩니다. |
| ItemUpdated | 업데이트 단추 ( **CommandName** 속성이 "업데이트"로 설정 된 단추)를 클릭 한 후 FormView 컨트롤이 행을 업데이트 한 후에 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | 업데이트 단추를 클릭할 때 FormView 컨트롤이 레코드를 업데이트 하기 전에 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| ModeChanged | FormView 컨트롤에서 편집, 삽입 또는 읽기 전용 모드로 모드를 변경한 후에 발생 합니다. 이 이벤트는 FormView 컨트롤에서 모드를 변경 하는 경우 작업을 수행 하는 데 주로 사용 됩니다. |
| ModeChanging | FormView 컨트롤이 편집, 삽입 또는 읽기 전용 모드로 모드를 변경 하기 전에 발생 합니다. 이 이벤트는 종종 모드 변경을 취소 하려면 사용 합니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭 하면 FormView 컨트롤이 페이징 작업을 처리 한 후에 발생 합니다. 이 이벤트는 사용자가 컨트롤의 다른 레코드를 탐색 한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하면 FormView 컨트롤이 페이징 작업을 처리 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |

## <a name="detailsview"></a>DetailsView

DetailsView 컨트롤은 테이블의 데이터 원본에서 단일 레코드를 표시 하는 데 사용 됩니다. 여기서 레코드의 각 필드는 테이블의 행에 표시 됩니다. 마스터-세부 시나리오에 대 한 GridView 컨트롤과 함께 사용할 수 있습니다. DetailsView 컨트롤은 다음과 같은 기능을 지원 합니다.

- SqlDataSource와 같은 데이터 소스 컨트롤에 바인딩합니다.
- 기본 제공 삽입 기능입니다.
- 기본 제공 업데이트 및 삭제 기능입니다.
- 기본 제공 페이징 기능입니다.
- 속성을 동적으로 설정 하 고 이벤트를 처리 하는 등을 위해 DetailsView 개체 모델에 대 한 프로그래밍 방식 액세스
- 테마 및 스타일을 통해 모양을 사용자 지정할 수 있습니다.

## <a name="row-fields"></a>행 필드

DetailsView 컨트롤의 각 데이터 행은 필드 컨트롤을 선언 하 여 만듭니다. 컨트롤의 행의 동작을 결정 하는 다른 행 필드 형식입니다. 필드 컨트롤은 DataControlField에서 파생 됩니다. 다음 표에서 사용할 수 있는 다른 행 필드 유형을 나열 합니다.

| **열 필드 형식** | **설명** |
| --- | --- |
| BoundField | 데이터 원본에서 필드의 값을 텍스트로 표시합니다. |
| ButtonField | DetailsView 컨트롤에 명령 단추를 표시 합니다. 이렇게 하면 추가 또는 제거 단추 등의 사용자 지정 단추 컨트롤을 사용 하 여 행을 표시할 수 있습니다. |
| CheckBoxField | DetailsView 컨트롤에 확인란을 표시 합니다. 이 행 필드 형식은 부울 값을 사용 하 여 필드를 표시 하려면 일반적으로 사용 됩니다. |
| CommandField | DetailsView 컨트롤에서 편집, 삽입 또는 삭제 작업을 수행 하는 기본 제공 명령 단추를 표시 합니다. |
| HyperLinkField | 하이퍼링크로 데이터 원본의 필드의 값을 표시합니다. 이 행 필드 형식을 사용 하면 두 번째 필드 하이퍼링크의 URL에 바인딩할 수 있습니다. |
| ImageField | DetailsView 컨트롤에 이미지를 표시 합니다. |
| Templatefield로 변환 | 지정 된 템플릿에 따라 DetailsView 컨트롤의 행에 대 한 사용자 정의 콘텐츠를 표시 합니다. 이 행 필드 형식에는 사용자 지정 행 필드를 만들 수 있습니다. |

기본적으로 AutoGenerateRows 속성은 **true**로 설정 됩니다 .이 속성은 데이터 소스에서 바인딩 가능한 형식의 각 필드에 대해 바인딩된 행 필드 개체를 자동으로 생성 합니다. 유효한 바인딩 가능한 형식은 String, DateTime, Decimal, Guid 및 기본 형식 집합입니다. 각 필드 데이터 소스의 각 필드 표시 되는 순서 대로 텍스트로 행에 표시 됩니다.

자동으로 생성 되는 행 레코드의 모든 필드를 표시 하는 빠르고 쉬운 방법을 제공 합니다. 그러나 DetailsView 컨트롤의 고급 기능을 사용 하려면 DetailsView 컨트롤에 포함할 행 필드를 명시적으로 선언 해야 합니다. 행 필드를 선언 하려면 먼저 **AutoGenerateRows** 속성을 **false**로 설정 합니다. 그런 다음 열기 및 닫기 **&lt;필드** 를 DetailsView 컨트롤의 여는 태그와 닫는 태그 사이에&gt;태그를 추가 합니다. 마지막으로 여는 태그와 닫는 **&lt;필드&gt;** 태그 사이에 포함 하려는 행 필드를 나열 합니다. 지정 된 행 필드는 나열 된 순서 대로 Fields 컬렉션에 추가 됩니다. **Fields** 컬렉션을 사용 하면 DetailsView 컨트롤의 행 필드를 프로그래밍 방식으로 관리할 수 있습니다.

> [!NOTE]
> 자동으로 생성 된 행 필드는 Fields 컬렉션에 추가 되지 않습니다.

## <a name="binding-to-data"></a>데이터 바인딩

DetailsView 컨트롤은 **SqlDataSource** 또는 AccessDataSource와 같은 데이터 소스 컨트롤에 바인딩하거나 system.object 및 system.object와 같은 system.web 인터페이스를 구현 하는 모든 데이터 소스에 바인딩할 수 있습니다 (예: system.object, Collections 및 system.object).

다음 방법 중 하나를 사용 하 여 DetailsView 컨트롤을 적절 한 데이터 원본 형식에 바인딩합니다.

- 데이터 소스 컨트롤에 바인딩하려면 DetailsView 컨트롤의 DataSourceID 속성을 데이터 소스 컨트롤의 ID 값으로 설정 합니다. DetailsView 컨트롤이 지정 된 데이터 소스 컨트롤에 자동으로 바인딩됩니다. 이것은 데이터 바인딩할 기본 방법입니다.
- **System.object의 IEnumerable** 인터페이스를 구현 하는 데이터 소스에 바인딩하려면 DetailsView 컨트롤의 DataSource 속성을 프로그래밍 방식으로 데이터 소스에 설정 하 고 DataBind 메서드를 호출 합니다.

## <a name="security"></a>보안

악성 클라이언트 스크립트 포함 될 수 있는 사용자 입력을 표시 하려면이 제어를 사용할 수 있습니다. 애플리케이션에서 표시 하기 전에 실행 스크립트, SQL 문 또는 다른 코드에 대 한 클라이언트에서 전송 되는 모든 정보를 확인 합니다. ASP.NET에서는 사용자 입력에서 차단 스크립트를 HTML 입력된 요청 유효성 검사 기능을 제공 합니다.

## <a name="data-operations"></a>데이터 작업

DetailsView 컨트롤은 사용자가 컨트롤에서 항목을 업데이트, 삭제, 삽입 및 페이징 하는 데 사용할 수 있는 기본 제공 기능을 제공 합니다. DetailsView 컨트롤이 데이터 소스 컨트롤에 바인딩되면 DetailsView 컨트롤이 데이터 소스 컨트롤의 기능을 활용 하 고 자동 업데이트, 삭제, 삽입 및 페이징 기능을 제공할 수 있습니다.

DetailsView 컨트롤은 다른 유형의 데이터 원본과의 업데이트, 삭제, 삽입 및 페이징 작업을 지원할 수 있습니다. 그러나 적절 한 이벤트 처리기에서 이러한 작업에 대 한 구현을 제공 해야 합니다.

DetailsView 컨트롤은 AutoGenerateEditButton, AutoGenerateDeleteButton 또는 AutoGenerateInsertButton 속성을 각각 **true**로 설정 하 여 편집, 삭제 또는 새로 만들기 단추를 사용 하 여 **commandfield** 행 필드를 자동으로 추가할 수 있습니다. 선택 된 레코드를 즉시 삭제 하는 삭제 단추와 달리, 편집 또는 새로 만들기 단추를 클릭 하면 DetailsView 컨트롤이 편집 또는 삽입 모드로 각각 이동 합니다. 편집 모드에 대 한 업데이트 및 취소 단추를 사용 하 여 편집 단추가 바뀝니다. 필드의 데이터 형식에 적합 한 입력 컨트롤 (예: TextBox 또는 CheckBox 컨트롤)은 사용자가 수정할 수 있는 필드의 값과 함께 표시 됩니다. 모든 변경 사항이 취소 단추를 클릭 데이터 원본에서 레코드를 업데이트 [업데이트] 단추를 클릭 합니다. 마찬가지로, 삽입 모드에서 새 단추 삽입 및 취소 단추를 사용 하 여 대체 되 고 새 레코드에 대 한 값을 입력 하 여 사용자에 대 한 빈 입력된 컨트롤이 표시 됩니다.

DetailsView 컨트롤은 사용자가 데이터 소스의 다른 레코드를 탐색할 수 있도록 하는 페이징 기능을 제공 합니다. 사용 하도록 설정 하면 페이지 탐색 컨트롤 페이저 행에 표시 됩니다. 페이징을 사용 하도록 설정 하려면 AllowPaging 속성을 **true**로 설정 합니다. PagerStyle 및 PagerSettings 속성을 사용 하 여 페이저 행을 사용자 지정할 수 있습니다.

## <a name="customizing-the-user-interface"></a>사용자 인터페이스 사용자 지정

컨트롤의 다른 파트에 대 한 스타일 속성을 설정 하 여 DetailsView 컨트롤의 모양을 사용자 지정할 수 있습니다. 다음 표에서 다양 한 스타일 속성을 나열합니다.

| **Style 속성** | **설명** |
| --- | --- |
| AlternatingRowStyle | DetailsView 컨트롤의 교대로 반복 되는 데이터 행에 대 한 스타일 설정입니다. 이 속성을 설정 하면 행 스타일 설정과 **AlternatingRowStyle** 설정 사이에 데이터 행이 번갈아 표시 됩니다. |
| CommandRowStyle | DetailsView 컨트롤의 기본 제공 명령 단추가 들어 있는 행의 스타일 설정입니다. |
| EditRowStyle | DetailsView 컨트롤이 편집 모드에 있을 때 데이터 행에 대 한 스타일 설정입니다. |
| EmptyDataRowStyle | 데이터 원본에 레코드가 포함 되어 있지 않을 때 DetailsView 컨트롤에 표시 되는 빈 데이터 행에 대 한 스타일 설정입니다. |
| FooterStyle | DetailsView 컨트롤의 바닥글 행에 대 한 스타일 설정입니다. |
| HeaderStyle | DetailsView 컨트롤의 머리글 행에 대 한 스타일 설정입니다. |
| InsertRowStyle | DetailsView 컨트롤이 삽입 모드일 때 데이터 행에 대 한 스타일 설정입니다. |
| PagerStyle | DetailsView 컨트롤의 페이저 행에 대 한 스타일 설정입니다. |
| RowStyle | DetailsView 컨트롤의 데이터 행에 대 한 스타일 설정입니다. **AlternatingRowStyle** 속성도 설정 되어 있으면 **Rowstyle** 설정과 **AlternatingRowStyle** 설정 사이에 데이터 행이 번갈아 표시 됩니다. |
| FieldHeaderStyle | DetailsView 컨트롤의 header 열에 대 한 스타일 설정입니다. |

## <a name="events"></a>이벤트

DetailsView 컨트롤은 프로그래밍할 수 있는 몇 가지 이벤트를 제공 합니다. 이렇게 하면 이벤트가 발생할 때마다 사용자 지정 루틴을 실행할 수 있습니다. 다음 표에서는 DetailsView 컨트롤에서 지 원하는 이벤트를 보여 줍니다. 또한 DetailsView 컨트롤은 기본 클래스에서 데이터 바인딩, 데이터 바인딩, 삭제 됨, Init, Load, PreRender 및 Render와 같은 이벤트를 상속 합니다.

| **이벤트** | **설명** |
| --- | --- |
| ItemCommand | DetailsView 컨트롤에서 단추를 클릭 하면 발생 합니다. |
| ItemCreated | DetailsView 컨트롤에 모든 DetailsViewRow 개체가 생성 된 후에 발생 합니다. 이 이벤트는 대개 표시 되기 전에 레코드의 값을 수정 합니다. |
| ItemDeleted | 삭제 단추를 클릭 하면 DetailsView 컨트롤이 데이터 소스에서 레코드를 삭제 한 후에 발생 합니다. 이 이벤트는 대개 삭제 작업의 결과 확인 합니다. |
| ItemDeleting | 삭제 단추를 클릭할 때 DetailsView 컨트롤이 데이터 소스에서 레코드를 삭제 하기 전에 발생 합니다. 이 이벤트는 삭제 작업을 취소 하려면 종종 사용 됩니다. |
| ItemInserted | 삽입 단추를 클릭할 때 DetailsView 컨트롤이 레코드를 삽입 한 후에 발생 합니다. 이 이벤트는 대개 삽입 작업의 결과 확인 합니다. |
| ItemInserting | 삽입 단추를 클릭할 때 DetailsView 컨트롤이 레코드를 삽입 하기 전에 발생 합니다. 이 이벤트는 삽입 작업을 취소 하려면 종종 사용 됩니다. |
| ItemUpdated | 업데이트 단추를 클릭 하면 DetailsView 컨트롤이 행을 업데이트 한 후에 발생 합니다. 이 이벤트는 대개 업데이트 작업의 결과 확인 합니다. |
| ItemUpdating | 업데이트 단추를 클릭 한 후 DetailsView 컨트롤이 레코드를 업데이트 하기 전에 발생 합니다. 이 이벤트는 업데이트 작업을 취소 하는 경우가 많습니다. |
| ModeChanged | DetailsView 컨트롤이 모드 (편집, 삽입 또는 읽기 전용 모드)를 변경한 후에 발생 합니다. 이 이벤트는 DetailsView 컨트롤이 모드를 변경 하는 경우 작업을 수행 하는 데 주로 사용 됩니다. |
| ModeChanging | DetailsView 컨트롤이 모드 (편집, 삽입 또는 읽기 전용 모드)를 변경 하기 전에 발생 합니다. 이 이벤트는 종종 모드 변경을 취소 하려면 사용 합니다. |
| PageIndexChanged | 페이저 단추 중 하나를 클릭 하면 DetailsView 컨트롤이 페이징 작업을 처리 한 후에 발생 합니다. 이 이벤트는 사용자가 컨트롤의 다른 레코드를 탐색 한 후 작업을 수행 해야 할 경우에 주로 사용 됩니다. |
| PageIndexChanging | 페이저 단추 중 하나를 클릭 하면 DetailsView 컨트롤이 페이징 작업을 처리 하기 전에이 이벤트가 발생 합니다. 이 이벤트는 페이징 작업을 취소 하는 경우가 많습니다. |

## <a name="the-menu-control"></a>메뉴 컨트롤

ASP.NET 2.0의 Menu 컨트롤은 완전 한 기능을 갖춘 탐색 시스템으로 설계 되었습니다. SiteMapDataSource와 같은 계층적 데이터 원본에 쉽게 데이터 바인딩할 수 있습니다.

Menu controls 구조는 선언적으로 또는 동적으로 정의할 수 있으며 단일 루트 노드와 임의 개수의 하위 노드로 구성 됩니다. 다음 코드는 메뉴 컨트롤에 대 한 메뉴를 선언적으로 정의 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

위의 예에서는 Home .aspx 노드가 루트 노드입니다. 다른 모든 노드는 다양 한 수준에서 루트 노드 내에 중첩 됩니다.

메뉴 컨트롤이 렌더링할 수 있는 메뉴에는 두 가지 유형이 있습니다. 정적 메뉴 및 동적 메뉴. 정적 메뉴는 항상 표시 되는 메뉴 항목으로 구성 됩니다. 동적 메뉴는 사용자가 마우스로 마우스로 가리킬 때만 표시 되는 메뉴 항목으로 구성 됩니다. 고객은 런타임에 데이터 바인딩된 메뉴를 사용 하 여 선언적으로 정의 된 메뉴와 동적 메뉴의 정적 메뉴를 혼동 하는 경우가 종종 있습니다. 실제로 동적 및 정적 메뉴는 채우기의 메서드와 관련이 없습니다. *정적* 및 *동적* 용어는 메뉴를 기본적으로 정적으로 표시할지 아니면 사용자가 작업을 수행 하는 경우에만 표시할지 여부를 나타냅니다.

**Staticdisplaylevels** 속성은 정적으로 표시 되는 메뉴의 수준 수를 구성 하는 데 사용 되므로 기본적으로 표시 됩니다. 위의 예제에서 **Staticdisplaylevels** 속성을 값 2로 설정 하면 메뉴에서 홈 노드, 음악 노드 및 영화 노드를 정적으로 표시 합니다. 사용자가 부모 노드를 가리키면 다른 모든 노드가 동적으로 표시 됩니다.

**Maximumdynamicdisplaylevels** 속성은 메뉴에 표시할 수 있는 최대 동적 수준 수를 구성 합니다. **Maximumdynamicdisplaylevels** 속성에 지정 된 값 보다 높은 수준의 동적 메뉴는 무시 됩니다.

> [!NOTE]
> MaximumDynamicDisplayLevels 속성으로 인해 메뉴가 렌더링 되지 않는 상황이 발생할 수 있습니다. 이러한 경우에는 고객 메뉴가 표시 될 수 있도록 속성이 충분히 설정 되었는지 확인 합니다.

## <a name="data-binding-the-menu-control"></a>메뉴 컨트롤에 데이터 바인딩

메뉴 컨트롤은 SiteMapDataSource 또는 XMLDataSource와 같은 모든 계층적 데이터 소스에 바인딩할 수 있습니다. SiteMapDataSource는 웹 사이트 파일 및 해당 스키마가 메뉴 컨트롤에 대해 알려진 API를 제공 하기 때문에 메뉴 컨트롤에 데이터를 바인딩하는 가장 일반적으로 사용 되는 방법입니다. 아래 목록에는 간단한 웹 사이트 맵 파일이 나와 있습니다.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

루트 siteMapNode 요소 (이 경우에는 Home 요소)가 하나 뿐입니다. 각 siteMapNode에 대해 여러 특성을 구성할 수 있습니다. 가장 일반적으로 사용 되는 특성은 다음과 같습니다.

- **url** 사용자가 메뉴 항목을 클릭할 때 표시 되는 URL을 지정 합니다. 이 특성이 없는 경우 클릭 하면 노드가 다시 게시 됩니다.
- **제목** 메뉴 항목에 표시 되는 텍스트를 지정 합니다.
- **설명** 노드에 대 한 설명서로 사용 됩니다. 또한 마우스를 노드 위에 놓았을 때 도구 설명으로 표시 합니다.
- **siteMapFile** 중첩 된 사이트맵를 허용 합니다. 이 특성은 올바른 형식의 ASP.NET 사이트 파일을 가리켜야 합니다.
- **역할** ASP.NET 보안 트리밍을 통해 노드의 모양을 제어할 수 있습니다.

이러한 특성은 모두 선택적 이지만 지정 되지 않은 경우 메뉴의 동작이 예상과 다를 수 있습니다. 예를 들어 *url* 특성을 지정 했지만 *description* 특성을 지정 하지 않으면 노드가 표시 되지 않으며 지정 된 url로 이동할 방법이 없습니다.

## <a name="controlling-a-menus-operation"></a>메뉴 작업 제어

ASP.NET Menu 컨트롤의 작업에 영향을 주는 몇 가지 속성이 있습니다. **방향** 속성인 **DisappearAfter** 속성, **Staticitemformatstring** 속성 및 **StaticPopoutImageUrl** 속성은 이러한 속성 중 일부에 불과합니다.

- **방향은** *가로* 또는 *세로로* 설정할 수 있으며 정적 메뉴 항목이 행에서 가로로 배치 되 고 세로로 배치 되는지 여부를 제어 합니다. 이 속성은 동적 메뉴에는 영향을 주지 않습니다.
- **DisappearAfter** 속성은 마우스를 이동한 후 동적 메뉴가 계속 표시 되는 기간을 구성 합니다. 값은 밀리초 단위로 지정 되며 기본값은 500입니다. 이 속성을-1 값으로 설정 하면 메뉴가 자동으로 사라지지 않습니다. 이 경우 사용자가 메뉴 외부를 클릭 하면 메뉴가 사라집니다.
- **Staticitemformatstring** 속성을 사용 하면 메뉴 시스템에서 일관성 있는 용어로를 쉽게 유지 관리할 수 있습니다. 이 속성을 지정 하는 경우 데이터 원본에 표시 되는 설명 대신 *{0}* 을 입력 해야 합니다. 예를 들어 실습 1에서 메뉴 항목을 선택 하 여 제품 페이지를 방문 하려면 StaticItemFormatString에 대 한 {0} 페이지를 방문 하세요. 런타임에 ASP.NET는 {0} 항목을 메뉴 항목에 대 한 올바른 설명으로 바꿉니다.
- **StaticPopoutImageUrl** 속성은 특정 메뉴 노드에 마우스로 가리키면 액세스할 수 있는 자식 노드가 있음을 나타내는 데 사용 되는 이미지를 지정 합니다. 동적 메뉴는 기본 이미지를 계속 사용 합니다.

## <a name="templated-menu-controls"></a>템플릿 메뉴 컨트롤

메뉴 컨트롤은 템플릿 기반 컨트롤이 며, 두 개의 다른 ItemTemplates을 허용 합니다. StaticItemTemplate 및 DynamicItemTemplate 이러한 템플릿을 사용 하 여 메뉴에 서버 컨트롤 또는 사용자 정의 컨트롤을 쉽게 추가할 수 있습니다.

Visual Studio .NET에서 템플릿을 편집 하려면 메뉴에서 스마트 태그 단추를 클릭 하 고 템플릿 편집을 선택 합니다. 그런 다음 StaticItemTemplate 또는 DynamicItemTemplate을 편집 하는 중에서 선택할 수 있습니다.

StaticItemTemplate에 추가 된 모든 컨트롤은 페이지가 로드 될 때 정적 메뉴에 표시 됩니다. DynamicItemTemplate에 추가 된 모든 컨트롤은 모든 팝업 메뉴에 표시 됩니다.

## <a name="menu-events"></a>메뉴 이벤트

메뉴 컨트롤에는 고유한 두 개의 이벤트가 있습니다. **MenuItemClicked** 및 **MenuItemDatabound** 이벤트입니다.

메뉴 항목을 클릭할 때 MenuItemClicked 이벤트가 발생 합니다. MenuItemDatabound 이벤트는 메뉴 항목이 데이터 바인딩된 경우 발생 합니다. 이벤트 처리기에 전달 되는 **Menueventargs** 는 item 속성을 통해 메뉴 항목에 대 한 액세스를 제공 합니다.

## <a name="controlling-a-menus-appearance"></a>메뉴 모양 제어

서식 메뉴에 사용할 수 있는 여러 스타일 중 하나 이상을 사용 하 여 메뉴 컨트롤의 모양에 영향을 줄 수도 있습니다. 이 중에는 **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **dynamicselectedstyle**및 **DynamicHoverStyle**가 있습니다. 이러한 속성은 표준 HTML 스타일 문자열을 사용 하 여 구성 됩니다. 예를 들어 다음은 동적 메뉴에 대 한 스타일에 영향을 줍니다.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> 가리키기 스타일을 사용 하는 경우에는 *runat* 요소가 *server*로 설정 된 페이지에 &lt;head&gt; 요소를 추가 해야 합니다.

메뉴 컨트롤은 ASP.NET 2.0 테마 사용도 지원 합니다.

## <a name="the-treeview-control"></a>TreeView 컨트롤

TreeView 컨트롤은 트리 형태의 구조에 데이터를 표시 합니다. Menu 컨트롤과 마찬가지로 SiteMapDataSource와 같은 모든 계층적 데이터 원본에 쉽게 데이터를 바인딩할 수 있습니다.

고객이 ASP.NET 2.0의 TreeView 컨트롤에 대해 질문할 수 있는 첫 번째 질문은 ASP.NET 1.x에서 사용할 수 있었던 TreeView IE WebControl와 관련 되어 있는지 여부입니다. 그것이 아니야. ASP.NET 2.0 TreeView 컨트롤은 처음부터 작성 되었으며 이전에 제공 된 IE TreeView WebControl에 비해 상당한 개선을 제공 합니다.

TreeView 컨트롤을 사이트 맵에 바인딩하는 방법에 대 한 자세한 내용은 메뉴 컨트롤과 정확히 동일한 방법으로 수행 됩니다. 그러나 TreeView 컨트롤의 작동 방식에는 몇 가지 고유한 차이점이 있습니다.

기본적으로 TreeView 컨트롤은 완전히 확장 된 상태로 표시 됩니다. 초기 로드 시 확장 수준을 변경 하려면 컨트롤의 **ExpandDepth** 속성을 수정 합니다. 이는 특정 노드 확장 시 TreeView가 데이터 바인딩된 경우에 특히 중요 합니다.

## <a name="databinding-the-treeview-control"></a>TreeView 컨트롤의 데이터 바인딩

TreeView는 메뉴 컨트롤과 달리 많은 양의 데이터를 처리 하는 데 적합 합니다. 따라서 SiteMapDataSource 또는 XMLDataSource에 데이터를 바인딩하는 것 외에도 TreeView는 데이터 집합 또는 다른 관계형 데이터에 바인딩되는 경우가 많습니다. TreeView 컨트롤이 많은 양의 데이터에 바인딩된 경우 실제로 컨트롤에 표시 되는 데이터에만 바인딩하는 것이 가장 좋습니다. 그러면 TreeView 노드가 확장 될 때 추가 데이터에 데이터를 바인딩할 수 있습니다.

이러한 경우 TreeView의 **PopulateOnDemand** 속성을 *true*로 설정 해야 합니다. 그런 다음 **TreeNodePopulate** 메서드에 대 한 구현을 제공 해야 합니다.

## <a name="data-binding-without-postback"></a>포스트백을 사용 하지 않는 데이터 바인딩

이전 예제에서 노드를 처음 확장 하면 페이지가 다시 게시 되 고 새로 고쳐집니다. 있거나이 예에서는 문제가 되지 않지만 많은 양의 데이터가 포함 된 프로덕션 환경에 있을 수 있습니다. 더 나은 시나리오는 TreeView에서 노드를 동적으로 채우지만 서버에 다시 게시 하지 않는 것입니다.

**PopulateNodesFromClient** 및 **PopulateOnDemand** 속성을 true로 설정 하 여 ASP.NET TreeView 컨트롤은 포스트백 없이 노드를 동적으로 채웁니다. 부모 노드가 확장 되 면 클라이언트에서 XMLHttp 요청이 수행 되 고 OnTreeNodePopulate 이벤트가 발생 합니다. 서버는 자식 노드에 데이터를 바인딩하는 데 사용 되는 XML 데이터 아일랜드를 사용 하 여 응답 합니다.

ASP.NET는이 기능을 구현 하는 클라이언트 코드를 동적으로 만듭니다. 스크립트를 포함 하는 &lt;스크립트&gt;은 (는) xml 파일을 가리키는 생성 됩니다. 예를 들어 아래 목록은 XMLHttp 요청을 생성 하는 스크립트 코드에 대 한 스크립트 링크를 보여 줍니다.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

위의 사용자 브라우저에서이 파일을 찾아 열면 XMLHttp 요청을 구현 하는 코드가 표시 됩니다. 이 메서드는 고객이 스크립트 파일을 수정 하지 못하도록 합니다.

## <a name="controlling-the-operation-of-the-treeview-control"></a>TreeView 컨트롤의 작업 제어

TreeView 컨트롤에는 컨트롤의 작업에 영향을 주는 몇 가지 속성이 있습니다. 가장 명백한 속성은 **Showcheckboxes**, **ShowExpandCollapse**및 **showcheckboxes**입니다.

**Showcheckboxes** 속성은 렌더링 시 노드에 확인란이 표시 되는지 여부에 영향을 줍니다. 이 속성의 유효한 값은 **None**, **Root**, **Parent**, **리프**및 **All**입니다. 다음과 같이 TreeView 컨트롤에 영향을 줍니다.

| **속성 값** | **효과** |
| --- | --- |
| None | 모든 노드에는 확인란이 표시 되지 않습니다. 이 값은 기본 설정입니다. |
| Root | 확인란은 루트 노드에만 표시 됩니다. |
| Parent | 자식 노드가 있는 노드에만 확인란이 표시 됩니다. 이러한 자식 노드는 부모 노드나 리프 노드가 될 수 있습니다. |
| 리프 | 자식 노드가 없는 노드에만 확인란이 표시 됩니다. |
| 모두 | 모든 노드에 확인란이 표시 됩니다. |

Checkbox를 사용 하는 경우 **CheckedNodes** 속성은 다시 게시 될 때 체크 인 된 TreeView 노드의 컬렉션을 반환 합니다.

**ShowExpandCollapse** 속성은 루트 및 부모 노드 옆에 있는 확장/축소 이미지의 모양을 제어 합니다. 이 속성을 **false**로 설정 하면 TreeView 노드가 하이퍼링크로 렌더링 되 고 링크를 클릭 하 여 확장/축소 됩니다.

**Showlines** 속성은 부모 노드를 자식 노드에 연결 하는 선을 표시할지 여부를 제어 합니다. **False** (기본값) 이면 줄이 표시 되지 않습니다. **True 이면**TreeView 컨트롤이 **LineImagesFolder** 속성으로 지정 된 폴더의 선 이미지를 사용 합니다.

TreeView 줄의 모양을 사용자 지정 하기 위해 Visual Studio .NET 2005에는 선 디자이너 도구가 포함 되어 있습니다. 아래와 같이 TreeView 컨트롤의 스마트 태그 단추를 사용 하 여이 도구에 액세스할 수 있습니다.

![](data-bound-controls/_static/image1.jpg)

**그림 1**

**선 이미지 사용자 지정** 메뉴 옵션을 선택 하면 선 디자이너 도구가 시작 되어 TreeView 선의 모양을 구성할 수 있습니다.

## <a name="treeview-events"></a>TreeView 이벤트

TreeView 컨트롤에는 다음과 같은 고유한 이벤트가 있습니다.

- SelectedNodeChanged는 **Selectaction** 속성에 따라 노드를 선택할 때 발생 합니다.
- TreeNodeCheckChanged는 노드 checkboxs 상태가 변경 될 때 발생 합니다.
- TreeNodeExpanded는 **Selectaction** 속성에 따라 노드가 확장 될 때 발생 합니다.
- TreeNodeCollapsed은 노드가 축소 될 때 발생 합니다.
- TreeNodeDataBound은 노드가 데이터 바인딩될 때 발생 합니다.
- TreeNodePopulate은 노드가 채워질 때 발생 합니다.

**Selectaction** 속성을 사용 하 여 노드를 선택할 때 발생 하는 이벤트를 구성할 수 있습니다. SelectAction 속성은 다음과 같은 작업을 제공 합니다.

- TreeNodeSelectAction는 노드가 선택 될 때 TreeNodeExpanded을 발생 시킵니다.
- TreeNodeSelectAction 노드를 선택 하면 이벤트가 발생 하지 않습니다.
- TreeNodeSelectAction 노드를 선택 하면 SelectedNodeChanged 이벤트를 발생 시킵니다.
- 노드가 선택 될 때 TreeNodeSelectAction 확장은 SelectedNodeChanged 이벤트와 TreeNodeExpanded 이벤트를 모두 발생 시킵니다.

## <a name="controlling-appearance-with-styles"></a>스타일을 사용 하 여 모양 제어

TreeView 컨트롤은 스타일을 사용 하 여 컨트롤의 모양을 제어 하기 위한 다양 한 속성을 제공 합니다. 사용할 수 있는 속성은 다음과 같습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| HoverNodeStyle | 마우스를 마우스로 가리킬 때 노드의 스타일을 제어 합니다. |
| LeafNodeStyle | 리프 노드의 스타일을 제어 합니다. |
| NodeStyle | 모든 노드의 스타일을 제어 합니다. 특정 노드 스타일 (예: LeafNodeStyle)은이 스타일을 재정의 합니다. |
| ParentNodeStyle | 모든 부모 노드의 스타일을 제어 합니다. |
| RootNodeStyle | 루트 노드의 스타일을 제어 합니다. |
| SelectedNodeStyle | 선택한 노드의 스타일을 제어 합니다. |

이러한 각 속성은 읽기 전용입니다. 그러나 각 속성은 **TreeNodeStyle** 개체를 반환 하 고, 해당 개체의 속성은 *속성-하위 속성* 형식을 사용 하 여 수정할 수 있습니다. 예를 들어 **Selectednodestyle**의 **ForeColor** 속성을 설정 하려면 다음 구문을 사용 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

위의 태그는 닫혀 있지 않습니다. 여기에 표시 된 선언적 구문을 사용할 때 HTML 코드에도 Treeview 만들기 노드가 포함 되기 때문입니다.

스타일 속성은 *속성. 하위 속성* 형식을 사용 하 여 코드에서 지정할 수도 있습니다. 예를 들어 코드에서 **Rootnodestyle** 의 **ForeColor** 속성을 설정 하려면 다음 구문을 사용 합니다.

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> 다른 스타일 속성의 포괄적인 목록은 TreeNodeStyle 개체에 대 한 MSDN 설명서를 참조 하십시오.

## <a name="the-sitemappath-control"></a>SiteMapPath 컨트롤

SiteMapPath 컨트롤은 ASP.NET 개발자를 위한 이동 bread-crumb 탐색 컨트롤을 제공 합니다. 다른 탐색 컨트롤과 마찬가지로 SiteMapDataSource 또는 XmlDataSource와 같은 계층적 데이터 원본에 쉽게 데이터 바인딩할 수 있습니다.

SiteMapPath 컨트롤은 SiteMapNodeItem 개체로 구성 됩니다. 노드에는 세 가지 유형이 있습니다. 루트 노드, 부모 노드 및 현재 노드. 루트 노드는 계층 구조의 맨 위에 있는 노드입니다. 현재 노드는 현재 페이지를 나타냅니다. 다른 모든 노드는 부모 노드입니다.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>SiteMapPath 컨트롤의 작업 제어

SiteMapPath 컨트롤의 작업을 제어 하는 속성은 다음과 같습니다.

| **속성** | **속성 설명** |
| --- | --- |
| ParentLevelsDisplayed | 표시 되는 부모 노드 수를 제어 합니다. 기본값은 표시 되는 부모 노드 수에 대 한 제한을 적용 하지 않는-1입니다. |
| PathDirection | SiteMapPath의 방향을 제어 합니다. 유효한 값은 RootToCurrent (기본값) 및 CurrentToRoot입니다. |
| PathSeparator | SiteMapPath 컨트롤에서 노드를 구분 하는 문자를 제어 하는 문자열입니다. 기본값은입니다. |
| RenderCurrentNodeAsLink | 현재 노드가 링크로 렌더링 되는지 여부를 제어 하는 부울 값입니다. 기본값은 False입니다. |
| SkipLinkText | 화면 판독기가 페이지를 볼 때 내게 필요한 옵션을 지원 합니다. 이 속성을 사용 하면 화면 판독기에서 SiteMapPath 컨트롤을 건너뛸 수 있습니다. 이 기능을 사용 하지 않도록 설정 하려면 속성을 System.string으로 설정 합니다. |

## <a name="templated-sitemappath-controls"></a>템플릿 SiteMapPath 컨트롤

SiteMapControl는 템플릿 기반 컨트롤이 며, 컨트롤을 표시 하는 데 사용할 다른 템플릿을 정의할 수 있습니다. SiteMapPath 컨트롤에서 템플릿을 편집 하려면 컨트롤에서 스마트 태그 단추를 클릭 하 고 메뉴에서 템플릿 편집을 선택 합니다. 사용 가능한 다른 템플릿 중에서 선택할 수 있는 아래와 같이 SiteMapTasks 메뉴가 표시 됩니다.

![](data-bound-controls/_static/image2.jpg)

**그림 2**

**Nodetemplate** 템플릿은 SiteMapPath의 모든 노드를 참조 합니다. 노드가 루트 노드이거나 현재 노드와 **rootnodetemplate** 또는 **currentnodetemplate** 이 구성 된 경우 nodetemplate이 재정의 됩니다.

## <a name="sitemappath-events"></a>SiteMapPath 이벤트

SiteMapPath 컨트롤에는 컨트롤 클래스에서 파생 되지 않은 두 개의 이벤트가 있습니다. **ItemCreated** 이벤트와 **itemdatabound 바인딩된** 이벤트입니다. ItemCreated 이벤트는 SiteMapPath 항목이 생성 될 때 발생 합니다. ItemDataBound은 SiteMapPath 노드의 데이터 바인딩 중에 DataBind 메서드를 호출할 때 발생 합니다. **SiteMapNodeItemEventArgs** 개체는 Item 속성을 통해 특정 SiteMapNodeItem에 대 한 액세스를 제공 합니다.

## <a name="controlling-appearance-with-styles"></a>스타일을 사용 하 여 모양 제어

다음 스타일은 SiteMapPath 컨트롤의 서식 지정에 사용할 수 있습니다.

| **속성 이름** | **컨트롤** |
| --- | --- |
| CurrentNodeStyle | 현재 노드의 텍스트 스타일을 제어 합니다. |
| RootNodeStyle | 루트 노드에 대 한 텍스트의 스타일을 제어 합니다. |
| NodeStyle | CurrentNodeStyle 또는 RootNodeStyle이 적용 되지 않는다고 가정 하 고 모든 노드에 대 한 텍스트 스타일을 제어 합니다. |

NodeStyle 속성은 CurrentNodeStyle 또는 RootNodeStyle에 의해 재정의 됩니다. 이러한 각 속성은 읽기 전용 이며 **스타일** 개체를 반환 합니다. 이러한 속성 중 하나를 사용 하 여 노드의 모양에 영향을 주려면 반환 되는 스타일 개체의 속성을 설정 해야 합니다. 예를 들어 아래 코드는 현재 노드의 forecolor 속성을 변경 합니다.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

속성은 다음과 같이 프로그래밍 방식으로 적용 될 수도 있습니다.

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> 템플릿이 적용 되는 경우 스타일은 적용 되지 않습니다.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>랩 1: ASP.NET Menu 컨트롤 구성

1. 새 웹 사이트를 만듭니다.
2. 파일, 새로 만들기, 파일을 차례로 선택 하 고 파일 템플릿 목록에서 사이트 맵을 선택 하 여 사이트 맵 파일을 추가 합니다.
3. 사이트 맵 (기본적으로 web.sitemap)을 열고 아래 목록과 같이 수정 합니다. 사이트 맵 파일에서 연결 하는 페이지는 존재 하지 않지만이 연습에서는 문제가 되지 않습니다.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. 디자인 뷰에서 기본 웹 폼을 엽니다.
5. 도구 상자의 탐색 섹션에서 페이지에 새 메뉴 컨트롤을 추가 합니다.
6. 도구 상자의 데이터 섹션에서 새 SiteMapDataSource를 추가 합니다. SiteMapDataSource는 사이트에서 web.sitemap 파일을 자동으로 사용 합니다. 웹 사이트 파일은 사이트의 루트 폴더에 *있어야* 합니다.
7. 메뉴 컨트롤을 클릭 한 다음 스마트 태그 단추를 클릭 하 여 메뉴 작업 대화 상자를 표시 합니다.
8. 데이터 원본 선택 드롭다운에서 SiteMapDataSource1를 선택 합니다.
9. 자동 서식 링크를 클릭 하 고 메뉴의 형식을 선택 합니다.
10. 속성 창에서 **Staticdisplaylevels** 속성을 2로 설정 합니다. 메뉴 컨트롤이 이제 디자이너에서 홈, 제품 및 서비스 노드를 표시 해야 합니다.
11. 브라우저에서 페이지를 탐색 하 여 메뉴를 사용 합니다. 사이트 맵에 추가 된 페이지는 실제로 존재 하지 않기 때문에 사용자가 해당 페이지를 탐색 하려고 하면 오류가 표시 됩니다.

StaticDisplayLevels 및 MaximumDynamicDisplayLevels 속성을 변경 하 여 실험 하 고 메뉴가 렌더링 되는 방식에 미치는 영향을 확인 합니다.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>랩 2: TreeView 컨트롤을 동적으로 바인딩

이 연습에서는 SQL Server 로컬에서 실행 중이 고 Northwind 데이터베이스가 SQL Server 인스턴스에 있는지를 전제로 합니다. 이러한 조건이 충족 되지 않으면 샘플에서 연결 문자열을 변경 하십시오. 트러스트 된 연결 대신 SQL Server 인증을 지정 해야 할 수도 있습니다.

1. 새 웹 사이트를 만듭니다.
2. Default.aspx의 코드 뷰로 전환 하 고 모든 코드를 아래 나열 된 코드로 바꿉니다. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. 페이지를 treeview .aspx로 저장 합니다.
4. 페이지를 탐색 합니다.
5. 페이지가 처음 표시 될 때 브라우저에서 페이지의 원본을 봅니다. 표시 되는 노드만 클라이언트에 전송 됩니다.
6. 임의의 노드 옆에 있는 더하기 기호를 클릭 합니다.
7. 페이지의 소스를 다시 봅니다. 이제 새로 표시 된 노드가 표시 됩니다.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>랩 3: GridView 및 DetailsView를 사용 하 여 데이터 보기 및 편집

1. 새 웹 사이트를 만듭니다.
2. 웹 사이트에 새 web.config를 추가 합니다.
3. 다음과 같이 web.config 파일에 연결 문자열을 추가 합니다. 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > 사용자 환경에 따라 연결 문자열을 변경 해야 할 수 있습니다.
4. web.config 파일을 저장한 다음 닫습니다.
5. Default.aspx를 열고 새 SqlDataSource 컨트롤을 추가 합니다.
6. SqlDataSource 컨트롤의 ID를 **Products**로 변경 합니다.
7. **SqlDataSource 작업** 메뉴에서 **데이터 소스 구성**을 클릭 합니다.
8. 연결 드롭다운에서 **Northwind** 를 선택 하 고 다음을 클릭 합니다.
9. **이름** 드롭다운에서 **Products** 를 선택 하 고 아래와 같이 **ProductID**, **ProductName**, **UnitPrice**및 **UnitsInStock** 확인란을 선택 합니다. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. **다음**을 클릭합니다.
11. **Finish**를 클릭합니다.
12. 원본 뷰로 전환 하 고 생성 된 코드를 검사 합니다. SqlDataSource 컨트롤에 추가 된 **SelectCommand**, **DeleteCommand**, **InsertCommand**및 **UpdateCommand** 를 확인 합니다. 또한 추가 된 매개 변수도 확인 합니다.
13. 디자인 뷰로 전환 하 여 페이지에 새 GridView 컨트롤을 추가 합니다.
14. **데이터 원본 선택** 드롭다운에서 **제품** 을 선택 합니다.
15. 아래와 같이 **페이징 사용** 및 **선택 사용** 을 선택 합니다. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. **열 편집** 링크를 클릭 하 고 **필드 자동 생성** 이 선택 되어 있는지 확인 합니다.
17. **확인**을 클릭합니다.
18. GridView 컨트롤이 선택 된 상태에서 속성 창의 **DataKeyNames** 속성 옆에 있는 단추를 클릭 합니다.
19. **사용 가능한 데이터 필드** 목록에서 **ProductID** 를 선택 하 고 **&gt;** 단추를 클릭 하 여 추가 합니다.
20. 확인을 클릭합니다.
21. 새 SqlDataSource 컨트롤을 페이지에 추가 합니다.
22. SqlDataSource 컨트롤의 ID를 **Details**로 변경 합니다.
23. SqlDataSource 작업 메뉴에서 **데이터 소스 구성**을 선택 합니다.
24. 드롭다운에서 **Northwind** 를 선택 하 고 **다음**을 클릭 합니다.
25. <strong>이름</strong> 드롭다운에서 <strong>Products</strong> 를 선택 하 고 listbox <strong>열</strong> 에서 <strong>\</strong * 확인란을 선택 합니다.
26. **WHERE** 단추를 클릭 합니다.
27. **열** 드롭다운에서 **ProductID** 를 선택 합니다.
28. 연산자 드롭다운에서 **=** 를 선택 합니다.
29. **원본** 드롭다운에서 **제어** 를 선택 합니다.
30. **컨트롤 ID** 드롭다운에서 **GridView1** 를 선택 합니다.
31. **추가** 단추를 클릭 하 여 where 절을 추가 합니다.
32. **확인**을 클릭합니다.
33. **고급** 단추를 클릭 하 고 **INSERT, UPDATE 및 DELETE 문 생성** 확인란을 선택 합니다.
34. **확인**을 클릭합니다.
35. **다음** 을 클릭 하 고 **마침**을 클릭 합니다.
36. 페이지에 DetailsView 컨트롤을 추가 합니다.
37. **데이터 원본 선택** 드롭다운에서 **자세히**를 선택 합니다.
38. 아래와 같이 **편집 사용** 확인란을 선택 합니다. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. 페이지를 저장 하 고 default.aspx를 찾아봅니다.
40. 다른 레코드 옆의 **선택** 링크를 클릭 하 여 DetailsView 업데이트를 자동으로 확인 합니다.
41. DetailsView 컨트롤에서 **편집** 링크를 클릭 합니다.
42. 레코드를 변경 하 고 **업데이트**를 클릭 합니다.
