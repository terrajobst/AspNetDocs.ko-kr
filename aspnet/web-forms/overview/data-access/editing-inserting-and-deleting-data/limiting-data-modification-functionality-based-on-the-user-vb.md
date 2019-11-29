---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
title: 사용자에 따라 데이터 수정 기능 제한 (VB) | Microsoft Docs
author: rick-anderson
description: 사용자가 데이터를 편집할 수 있도록 허용 하는 웹 응용 프로그램에서는 다른 사용자 계정에 다른 데이터 편집 권한이 있을 수 있습니다. 이 자습서에서는 다음 방법에 대해 살펴보겠습니다.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 9dc264a6-feb8-474b-8b91-008c50708065
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
msc.type: authoredcontent
ms.openlocfilehash: c257a930e4d27fcd42591a541e700786bf413bf0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627187"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-vb"></a>사용자에 따라 데이터 수정 기능 제한(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_VB.exe) 또는 [PDF 다운로드](limiting-data-modification-functionality-based-on-the-user-vb/_static/datatutorial23vb1.pdf)

> 사용자가 데이터를 편집할 수 있도록 허용 하는 웹 응용 프로그램에서는 다른 사용자 계정에 다른 데이터 편집 권한이 있을 수 있습니다. 이 자습서에서는 방문한 사용자에 따라 데이터 수정 기능을 동적으로 조정 하는 방법을 살펴보겠습니다.

## <a name="introduction"></a>소개

여러 웹 응용 프로그램에서 사용자 계정을 지원 하 고 로그인 한 사용자에 따라 다양 한 옵션, 보고서 및 기능을 제공 합니다. 예를 들어 microsoft의 자습서에서는 공급자 회사의 사용자가 사이트에 로그온 하 여 해당 제품에 대 한 일반 정보 (예: 회사 이름)를 업데이트 하 고 해당 제품에 대 한 일반 정보 (예: 회사 이름)를 업데이트 하려고 할 수 있습니다. 주소, 담당자 정보 등이 있습니다. 또한 회사의 사용자에 대 한 일부 사용자 계정을 포함 하 여 재고, 순서 다시 정렬 등의 제품 정보를 로그온 하 고 업데이트할 수 있습니다. 또한 웹 응용 프로그램은 익명 사용자가 방문 하도록 허용 하 고 (로그온 하지 않은 사용자) 데이터를 보기만 하도록 제한할 수 있습니다. 이러한 사용자 계정 시스템을 사용 하는 경우 현재 로그온 한 사용자에 게 적합 한 삽입, 편집 및 삭제 기능을 제공 하기 위해 ASP.NET 페이지의 데이터 웹 컨트롤이 필요 합니다.

이 자습서에서는 방문한 사용자에 따라 데이터 수정 기능을 동적으로 조정 하는 방법을 살펴보겠습니다. 특히 공급자가 제공 하는 제품을 나열 하는 GridView와 함께 편집 가능한 DetailsView에 공급자 정보를 표시 하는 페이지를 만듭니다. 페이지를 방문 하는 사용자가 회사에서 제공 하는 경우 다음을 수행할 수 있습니다. 공급자 정보를 봅니다. 해당 주소를 편집 합니다. 공급자가 제공 하는 모든 제품에 대 한 정보를 편집 합니다. 그러나 사용자가 특정 회사를 사용 하는 경우 사용자는 자신의 주소 정보만 보고 편집할 수 있으며, 단종 된 것으로 표시 되지 않은 제품만 편집할 수 있습니다.

[회사의 사용자가 모든 공급자 정보를 편집할 수 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image1.png)

**그림 1**: 회사의 사용자가 모든 공급자 정보를 편집할 수 있음 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image3.png))

[특정 공급자의 사용자 ![해당 정보만 보고 편집할 수 있습니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image4.png)

**그림 2**: 특정 공급자의 사용자만 해당 정보를 보고 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image6.png)).

S를 시작 하겠습니다.

> [!NOTE]
> ASP.NET 2.0 s 멤버 자격 시스템은 사용자 계정을 만들고, 관리 하 고, 유효성을 검사 하기 위한 표준화 된 확장 가능한 플랫폼을 제공 합니다. 멤버 자격 시스템에 대 한 검사는 이러한 자습서의 범위를 벗어나기 때문에이 자습서에서는 대신 익명 방문자가 특정 공급자나 회사에서 온 것인지 여부를 선택할 수 있도록 허용 하 여 멤버 자격을 "fakes" 합니다. 멤버 자격에 대 한 자세한 내용은 내 [검사 ASP.NET 2.0 s 멤버 자격, 역할 및 프로필](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) 문서 시리즈를 참조 하세요.

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>1 단계: 사용자가 자신의 액세스 권한을 지정할 수 있도록 허용

실제 웹 응용 프로그램에서 사용자 계정 정보는 회사 또는 특정 공급 업체에 대 한 작업 여부를 포함 하 고, 사용자가 사이트에 로그온 한 후에는 ASP.NET 페이지에서 프로그래밍 방식으로이 정보에 액세스할 수 있습니다. 이 정보는 ASP.NET 2.0 s 역할 시스템, 프로필 시스템을 통한 사용자 수준 계정 정보 또는 일부 사용자 지정 방법을 통해 캡처할 수 있습니다.

이 자습서의 목적은 로그온 한 사용자에 따라 데이터 수정 기능을 조정 하는 것을 보여 주기 위한 것 이며 ASP.NET 2.0 s 멤버 자격, 역할 및 프로필 시스템을 소개 하는 것은 아닙니다. 매우 단순한 메커니즘을 사용 하 여 페이지를 방문 하는 사용자에 대 한 기능-사용자가 공급자 정보를 보거나 편집할 수 있어야 하는지 여부를 표시 하 고, 사용자가 보고 편집할 수 있는 특정 공급자 정보를 표시 하는 데 사용할 수 있는 DropDownList입니다. 사용자가 모든 공급자 정보를 보고 편집할 수 있음을 표시 하는 경우 (기본값), 모든 공급자를 통해 페이지를 이동 하 고, 공급자의 주소 정보를 편집 하 고, 선택한 공급자가 제공 하는 모든 제품에 대 한 단위당 이름 및 수량을 편집할 수 있습니다. 사용자가 특정 공급 업체만 보고 편집할 수 있음을 표시 하는 경우에는 해당 공급자의 세부 정보 및 제품만 볼 수 있으며, *지원 되지* 않는 제품에 대 한 단위 정보만 업데이트할 수 있습니다.

이 자습서의 첫 번째 단계는이 DropDownList을 만들어 시스템의 suppliers로 채우는 것입니다. `EditInsertDelete` 폴더에서 `UserLevelAccess.aspx` 페이지를 열고 `ID` 속성이 `Suppliers`로 설정 된 DropDownList을 추가한 다음이 DropDownList을 `AllSuppliersDataSource`라는 새 ObjectDataSource에 바인딩합니다.

[AllSuppliersDataSource 라는 새 ObjectDataSource를 만들 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image7.png)

**그림 3**: 이름이 `AllSuppliersDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image9.png))

이 DropDownList에 모든 공급자를 포함 하려고 하므로 `SuppliersBLL` 클래스 s `GetSuppliers()` 메서드를 호출 하도록 ObjectDataSource를 구성 합니다. 또한 ObjectDataSource s `Update()` 메서드가 `SuppliersBLL` 클래스 s `UpdateSupplierAddress` 메서드에 매핑되는지 확인 합니다 .이 ObjectDataSource는 2 단계에서 추가 될 DetailsView에도 사용 됩니다.

ObjectDataSource 마법사를 완료 한 후 `CompanyName` 데이터 필드를 표시 하 고 `SupplierID` 데이터 필드를 각 `ListItem`에 대 한 값으로 사용 하도록 `Suppliers` DropDownList를 구성 하 여 단계를 완료 합니다.

[CompanyName 및 공급자 데이터 필드를 사용 하도록 공급자 DropDownList 구성 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image10.png)

**그림 4**: `CompanyName` 및 `SupplierID` 데이터 필드를 사용 하도록 `Suppliers` DropDownList 구성 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image12.png))

이 시점에서 DropDownList은 데이터베이스에 있는 공급자의 회사 이름을 나열 합니다. 그러나 "모든 공급자 표시/편집" 옵션도 DropDownList에 포함 해야 합니다. 이를 수행 하려면 `Suppliers` DropDownList s `AppendDataBoundItems` 속성을 `true`로 설정 하 고 `Text` 속성이 "Show/Edit ALL Suppliers"이 고 해당 값이 `-1`인 `ListItem`를 추가 합니다. 속성 창로 이동 하 여 DropDownList의 `Items` 속성에서 줄임표를 클릭 하 여 선언적 태그나 디자이너를 통해 직접 추가할 수 있습니다.

> [!NOTE]
> 데이터 바인딩된 DropDownList에 모두 선택 항목을 추가 하는 방법에 대 한 자세한 내용은 DropDownList 자습서를 사용 하 여 [*마스터/세부 정보 필터링*](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 을 참조 하세요.

`AppendDataBoundItems` 속성이 설정 되 고 `ListItem` 추가 된 후에는 DropDownList의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample1.aspx)]

그림 5는 브라우저를 통해 볼 때 현재 진행 상황을 보여 주는 스크린샷입니다.

[공급자 DropDownList에는 모든 ListItem 표시와 각 공급 업체에 대 한 하나를 포함 하는 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image13.png)

**그림 5**: `Suppliers` DropDownList에는 모든 `ListItem`표시와 각 공급 업체에 대 한 하나 ([전체 크기의 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image15.png))가 포함 되어 있습니다.

사용자가 선택을 변경한 직후에 사용자 인터페이스를 업데이트 하려고 하므로 `Suppliers` DropDownList s `AutoPostBack` 속성을 `true`로 설정 합니다. 2 단계에서는 DropDownList 선택 항목을 기반으로 공급자에 대 한 정보를 표시 하는 DetailsView 컨트롤을 만듭니다. 그런 다음 3 단계에서이 DropDownList s `SelectedIndexChanged` 이벤트에 대 한 이벤트 처리기를 만듭니다 .이 이벤트는 선택한 공급자에 따라 적절 한 공급자 정보를 DetailsView에 바인딩하는 코드를 추가 합니다.

## <a name="step-2-adding-a-detailsview-control"></a>2 단계: DetailsView 컨트롤 추가

에서 DetailsView을 사용 하 여 공급자 정보를 표시 해 보겠습니다. 모든 공급자를 보고 편집할 수 있는 사용자의 경우 DetailsView은 페이징을 지원 하 여 사용자가 한 번에 하나의 레코드를 사용 하 여 공급자 정보를 단계별로 실행할 수 있도록 합니다. 그러나 사용자가 특정 공급자에 대해 작업을 수행 하는 경우에는 DetailsView에 특정 공급자 정보만 표시 되 고 페이징 인터페이스는 포함 되지 않습니다. 두 경우 모두 DetailsView은 사용자가 공급자의 주소, 구/군/시 및 국가 필드를 편집할 수 있도록 해야 합니다.

`Suppliers` DropDownList 아래에 있는 페이지에 DetailsView을 추가 하 고, `ID` 속성을 `SupplierDetails`로 설정 하 고, 이전 단계에서 만든 `AllSuppliersDataSource` ObjectDataSource에 바인딩합니다. 다음으로는 DetailsView의 스마트 태그에서 페이징 사용 및 편집 사용 확인란을 선택 합니다.

> [!NOTE]
> DetailsView s 스마트 태그에 편집 사용 옵션이 표시 되지 않으면 ObjectDataSource s `Update()` 메서드를 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드에 매핑하지 않았기 때문입니다. 잠시 뒤로 이동 하 여이 구성을 변경 하세요. 그러면 편집 사용 옵션이 DetailsView의 스마트 태그에 표시 됩니다.

`SuppliersBLL` 클래스 s `UpdateSupplierAddress` 메서드는 `supplierID`, `address`, `city`및 `country`-DetailsView s BoundFields을 수정 하 여 `CompanyName` 및 `Phone` BoundFields가 읽기 전용인 경우에만 매개 변수 4 개를 허용 합니다. 또한 `SupplierID` BoundField를 모두 제거 합니다. 마지막으로 `AllSuppliersDataSource` ObjectDataSource의 `OldValuesParameterFormatString` 속성이 `original_{0}`으로 설정 되어 있습니다. 선언적 구문에서이 속성 설정을 완전히 제거 하거나 기본값인 `{0}`로 설정 합니다.

`SupplierDetails` DetailsView 및 `AllSuppliersDataSource` ObjectDataSource를 구성한 후에는 다음과 같은 선언 태그를 사용할 수 있습니다.

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample2.aspx)]

이 시점에서 DetailsView은 페이징할 수 있으며 선택한 공급자의 주소 정보는 `Suppliers` DropDownList에서 선택한 항목에 관계 없이 업데이트할 수 있습니다 (그림 6 참조).

[![공급자 정보를 볼 수 있으며 해당 주소가 업데이트 됩니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image16.png)

**그림 6**: 모든 공급자 정보를 볼 수 있으며 해당 주소를 업데이트할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image18.png)).

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>3 단계: 선택한 공급자 정보만 표시

현재 페이지에는 `Suppliers` DropDownList에서 특정 공급자가 선택 되었는지 여부에 관계 없이 모든 공급 업체에 대 한 정보가 표시 됩니다. 선택한 공급자에 대 한 공급자 정보만 표시 하려면 특정 공급자에 대 한 정보를 검색 하는 한 페이지에 다른 ObjectDataSource를 추가 해야 합니다.

페이지에 새 ObjectDataSource를 추가 하 `SingleSupplierDataSource`이름을로 지정 합니다. 스마트 태그에서 데이터 소스 구성 링크를 클릭 하 고 `SuppliersBLL` 클래스 s `GetSupplierBySupplierID(supplierID)` 메서드를 사용 하도록 합니다. `AllSuppliersDataSource` ObjectDataSource와 마찬가지로 `SingleSupplierDataSource` ObjectDataSource s `Update()` 메서드를 `SuppliersBLL` 클래스의 `UpdateSupplierAddress` 메서드에 매핑합니다.

[SingleSupplierDataSource ObjectDataSource를 구성 하 ![GetSupplierBySupplierID (공급자) 메서드를 사용 합니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image19.png)

**그림 7**: `GetSupplierBySupplierID(supplierID)` 메서드를 사용 하도록 `SingleSupplierDataSource` ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image21.png))

다음으로 `GetSupplierBySupplierID(supplierID)` 메서드 `supplierID` 입력 매개 변수에 대 한 매개 변수 원본을 지정 하 라는 메시지를 표시 합니다. DropDownList에서 선택한 공급자에 대 한 정보를 표시 하려고 하므로 `Suppliers` DropDownList s `SelectedValue` 속성을 매개 변수 원본으로 사용 합니다.

[공급자 DropDownList을 공급자 매개 변수 원본으로 사용 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image22.png)

**그림 8**: `supplierID` 매개 변수 소스로 `Suppliers` DropDownList 사용 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image24.png))

이 두 번째 ObjectDataSource가 추가 된 경우에도 DetailsView 컨트롤은 현재 `AllSuppliersDataSource` ObjectDataSource를 항상 사용 하도록 구성 되어 있습니다. 선택한 `Suppliers` DropDownList 항목에 따라 DetailsView에서 사용 하는 데이터 소스를 조정 하는 논리를 추가 해야 합니다. 이를 수행 하려면 Suppliers DropDownList에 대 한 `SelectedIndexChanged` 이벤트 처리기를 만듭니다. 이는 디자이너에서 DropDownList을 두 번 클릭 하 여 가장 쉽게 만들 수 있습니다. 이 이벤트 처리기는 사용할 데이터 원본을 결정 하 고 데이터를 DetailsView에 다시 바인딩해야 합니다. 이 작업은 다음 코드를 사용 하 여 수행 됩니다.

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample3.vb)]

"모든 공급자 표시/편집" 옵션이 선택 되어 있는지 여부를 확인 하 여 이벤트 처리기를 시작 합니다. 이 경우 `SupplierDetails` DetailsView s `DataSourceID`를 `AllSuppliersDataSource`로 설정 하 고 `PageIndex` 속성을 0으로 설정 하 여 공급자 집합의 첫 번째 레코드에 사용자를 반환 합니다. 그러나 사용자가 DropDownList에서 특정 공급자를 선택한 경우에는 DetailsView s `DataSourceID` `SingleSuppliersDataSource`에 할당 됩니다. 사용 되는 데이터 원본에 관계 없이 `SuppliersDetails` 모드는 읽기 전용 모드로 되돌아가고 `SuppliersDetails` 컨트롤의 `DataBind()` 메서드를 호출 하 여 데이터를 DetailsView에 다시 바인딩 합니다.

이 이벤트 처리기를 사용 하는 경우 "모든 공급자 표시/편집" 옵션이 선택 되어 있지 않으면 DetailsView 컨트롤에 선택한 공급자가 표시 됩니다 .이 경우에는 페이징 인터페이스를 통해 모든 공급자를 볼 수 있습니다. 그림 9에서는 "모든 공급자 표시/편집" 옵션이 선택 된 페이지를 보여 줍니다. 사용자가 공급자를 방문 하 고 업데이트할 수 있도록 페이징 인터페이스가 제공 됩니다. 그림 10에는 Ma Maison 공급자가 선택 된 페이지가 표시 됩니다. 이 경우 Ma Maison s 정보만 볼 수 있으며 편집할 수 있습니다.

[![모든 공급자 정보를 보고 편집할 수 있습니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image25.png)

**그림 9**: 모든 공급자 정보를 보고 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image27.png)).

[![선택한 공급자 정보만 보고 편집할 수 있습니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image28.png)

**그림 10**: 선택한 공급자 정보만 보고 편집할 수 있음 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image30.png))

> [!NOTE]
> 이 자습서에서는 `true` (기본값)로 설정 해야 합니다. 즉 `EnableViewState`, DropDownList s `SelectedIndex` 및 DetailsView s `DataSourceID` 속성의 변경 내용은 다시 게시 간에 기억 되기 때문입니다.

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>4 단계: 편집 가능한 GridView에 공급자 제품 나열

DetailsView이 완료 되 면 다음 단계는 선택한 공급자가 제공 하는 제품을 나열 하는 편집 가능한 GridView를 포함 하는 것입니다. 이 GridView는 `ProductName` 및 `QuantityPerUnit` 필드만 편집할 수 있도록 허용 해야 합니다. 또한 페이지를 방문 하는 사용자가 특정 공급자의 인 경우에는 중단 *되지* 않는 제품만 업데이트할 수 있어야 합니다. 이 작업을 수행 하려면 먼저 `ProductID`, `ProductName`및 `QuantityPerUnit` 필드를 입력으로 사용 하는 `ProductsBLL` 클래스 `UpdateProducts` 메서드의 오버 로드를 추가 해야 합니다. 이 프로세스를 다양 한 자습서에서 미리 살펴보았습니다. 따라서 `ProductsBLL`에 추가 해야 하는 코드를 살펴보겠습니다.

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample4.vb)]

이 오버 로드를 만든 후 GridView 컨트롤과 연결 된 ObjectDataSource를 추가할 준비가 되었습니다. 새 GridView를 페이지에 추가 하 고, 해당 `ID` 속성을 `ProductsBySupplier`로 설정 하 고, 새 ObjectDataSource `ProductsBySupplierDataSource`를 사용 하도록 구성 합니다. 이 GridView를 사용 하 여 선택한 공급자가 해당 제품을 나열 하려고 하므로 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드를 사용 합니다. 또한 방금 만든 새 `UpdateProduct` 오버 로드에 `Update()` 메서드를 매핑합니다.

[위에서 만든 UpdateProduct 오버 로드를 사용 하도록 ObjectDataSource를 구성 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image31.png)

**그림 11**: 위에서 만든 `UpdateProduct` 오버 로드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image33.png))

`GetProductsBySupplierID(supplierID)` 메서드 `supplierID` 입력 매개 변수에 대 한 매개 변수 원본을 선택 하 라는 메시지가 다시 표시 됩니다. DetailsView에서 선택한 공급자에 대 한 제품을 표시 하려고 하므로 `SuppliersDetails` DetailsView 컨트롤 s `SelectedValue` 속성을 매개 변수 원본으로 사용 합니다.

[SuppliersDetails DetailsView s SelectedValue 속성을 매개 변수 소스로 사용 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image34.png)

**그림 12**: `SuppliersDetails` DetailsView s `SelectedValue` 속성을 매개 변수 소스로 사용 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image36.png))

GridView로 돌아가면 `Discontinued` CheckBoxField를 읽기 전용으로 표시 하 여 `ProductName`, `QuantityPerUnit`및 `Discontinued`를 제외한 GridView 필드를 모두 제거 합니다. 또한 GridView s 스마트 태그에서 편집 사용 옵션을 선택 합니다. 이러한 변경 내용을 적용 한 후 GridView 및 ObjectDataSource의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample5.aspx)]

이전 ObjectDataSources 원본을 사용할 때와 마찬가지로이 1 개의 `OldValuesParameterFormatString` 속성이 `original_{0}`로 설정 되어 제품 이름 또는 단위당 수량을 업데이트 하려고 할 때 문제가 발생 합니다. 선언적 구문에서이 속성을 완전히 제거 하거나 기본값인 `{0}`로 설정 합니다.

이 구성이 완료 되 면 페이지에 GridView에서 선택한 공급자가 제공 하는 제품이 나열 됩니다 (그림 13 참조). 현재 *제품* 이름 또는 단위당 수량을 업데이트할 수 있습니다. 그러나 특정 공급자와 연결 된 사용자가 단종 된 제품에 대해 이러한 기능이 금지 되도록 페이지 논리를 업데이트 해야 합니다. 5 단계에서이 마지막 부분을 살펴보겠습니다.

[선택한 공급 업체에서 제공 하는 제품이 표시 ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image37.png)

**그림 13**: 선택한 공급자가 제공 하는 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image39.png)).

> [!NOTE]
> 이 편집 가능한 GridView를 추가 하면 GridView를 읽기 전용 상태로 되돌리기 위해 `Suppliers` DropDownList s `SelectedIndexChanged` 이벤트 처리기를 업데이트 해야 합니다. 그렇지 않고 제품 정보를 편집 하는 동안 다른 공급자를 선택 하는 경우 새 공급자에 대 한 GridView의 해당 인덱스도 편집할 수 있습니다. 이를 방지 하려면 `SelectedIndexChanged` 이벤트 처리기에서 GridView s `EditIndex` 속성을 `-1`로 설정 하기만 하면 됩니다.

또한 GridView의 뷰 상태를 사용 하도록 설정 하는 것이 중요 하다는 것을 기억 하십시오 (기본 동작). GridView s `EnableViewState` 속성을 `false`로 설정 하면 동시 사용자가 실수로 레코드를 삭제 하거나 편집 하는 위험을 발생 시킬 수 있습니다. 자세한 내용은 [경고: 편집 및/또는 삭제를 지원 하 고 해당 뷰 상태를 사용할 수 없는 ASP.NET 2.0 gridviews/DetailsView/FormViews의 동시성 문제](http://scottonwriting.net/sowblog/posts/10054.aspx) 를 참조 하세요.

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>5 단계: 모든 공급 업체 표시/편집이 선택 되지 않은 경우 중단 된 제품에 대 한 편집 허용 안 함

`ProductsBySupplier` GridView는 완전 하 게 작동 하지만 현재 특정 공급자의 사용자에 게 너무 많은 액세스 권한을 부여 합니다. 비즈니스 규칙에 따라 이러한 사용자는 중단 되지 않은 제품을 업데이트할 수 없습니다. 이를 적용 하기 위해 공급자의 사용자가 페이지를 방문할 때 지원 되지 않는 제품을 사용 하 여 해당 GridView 행에서 편집 단추를 숨기 거 나 비활성화할 수 있습니다.

GridView s `RowDataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트 처리기에서 사용자가 특정 공급자와 연결 되어 있는지 여부를 확인 해야 합니다 .이 자습서의 경우 Suppliers DropDownList s `SelectedValue` 속성을 선택 하 여 확인할 수 있습니다.-1이 아닌 경우에는 사용자가 특정 공급자와 연결 됩니다. 이러한 사용자에 게는 제품이 중단 되었는지 여부를 확인 해야 합니다. [*Gridview의 바닥글에 요약 정보 표시*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) 자습서에 설명 된 대로 `e.Row.DataItem` 속성을 통해 gridview 행에 바인딩된 실제 `ProductRow` 인스턴스에 대 한 참조를 가져올 수 있습니다. 제품이 더 이상 사용 되지 않는 경우 이전 자습서에 설명 된 기술을 사용 하 여 GridView의 CommandField에서 편집 단추에 대 한 프로그래밍 방식의 참조를 가져와 [*삭제할 때 클라이언트 쪽 확인을 추가할*](adding-client-side-confirmation-when-deleting-vb.md)수 있습니다. 참조가 있으면 단추를 숨기 거 나 사용 하지 않도록 설정할 수 있습니다.

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample6.vb)]

이 이벤트 처리기를 사용 하는 경우이 페이지를 특정 공급자의 사용자로 방문할 때 단종 된 제품은 편집할 수 없습니다. 이러한 제품에 대 한 편집 단추는 숨겨집니다. 예를 들어 Chef Anton s Gumbo Mix는 새로운 Orleans Cajun Delights 공급자에 대해 단종 된 제품입니다. 이 특정 공급자에 대 한 페이지를 방문 하면이 제품에 대 한 편집 단추가 표시 되지 않습니다 (그림 14 참조). 그러나 "모든 공급자 표시/편집"을 사용 하 여 방문할 때 편집 단추를 사용할 수 있습니다 (그림 15 참조).

[공급자 특정 사용자에 대 한 ![Chef Anton s Gumbo Mix의 편집 단추가 숨겨집니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image40.png)

**그림 14**: 공급자별 사용자의 경우 Chef Anton s Gumbo Mix의 편집 단추가 숨겨져 있습니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image42.png)).

[모든 공급자 사용자 표시/편집 ![Chef Anton s Gumbo Mix의 편집 단추가 표시 됩니다.](limiting-data-modification-functionality-based-on-the-user-vb/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image43.png)

**그림 15**: 모든 Suppliers 사용자를 표시 하거나 편집 하는 경우 Chef Anton s Gumbo Mix의 편집 단추가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](limiting-data-modification-functionality-based-on-the-user-vb/_static/image45.png)).

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>비즈니스 논리 계층에서 액세스 권한을 확인 하는 중

이 자습서에서 ASP.NET 페이지는 사용자가 볼 수 있는 정보와 업데이트할 수 있는 제품에 대 한 모든 논리를 처리 합니다. 이상적으로이 논리는 비즈니스 논리 계층에도 표시 됩니다. 예를 들어 모든 공급 업체를 반환 하는 `SuppliersBLL` 클래스 s `GetSuppliers()` 메서드는 현재 로그온 한 사용자가 특정 공급자와 연결 *되지* 않았는지 확인 하는 검사를 포함할 수 있습니다. 마찬가지로 `UpdateSupplierAddress` 방법은 현재 로그온 한 사용자가 회사에 대해 작업을 수행 하 고 (따라서 모든 공급자 주소 정보를 업데이트할 수 있음) 데이터를 업데이트할 공급자와 연결 되어 있는지 확인 하는 검사를 포함할 수 있습니다.

이러한 BLL 계층 검사는 여기에 포함 되지 않았습니다 .이 자습서에서는 사용자 권한이 페이지의 DropDownList (BLL 클래스에서 액세스할 수 없음)에 의해 결정 됩니다. 멤버 자격 시스템 또는 ASP.NET에서 제공 하는 기본 인증 체계 (예: Windows 인증) 중 하나를 사용 하는 경우 현재 로그온 한 사용자 정보 및 역할 정보를 BLL에서 액세스 하 여 이러한 액세스를 만들 수 있습니다. 프레젠테이션 및 BLL 계층 모두에서 권한 검사를 수행할 수 있습니다.

## <a name="summary"></a>요약

사용자 계정을 제공 하는 대부분의 사이트는 로그인 한 사용자에 따라 데이터 수정 인터페이스를 사용자 지정 해야 합니다. 관리자는 레코드를 삭제 하 고 편집할 수 있지만 관리자가 아닌 사용자는 자신이 만든 레코드만 업데이트 하거나 삭제 하도록 제한할 수 있습니다. 시나리오에 관계 없이 데이터 웹 컨트롤, ObjectDataSource 및 비즈니스 논리 계층 클래스를 확장 하 여 로그온 한 사용자에 따라 특정 기능을 추가 하거나 거부할 수 있습니다. 이 자습서에서는 사용자가 특정 공급자와 연결 되어 있는지 또는 회사에 대해 작동 하 고 있는지에 따라 볼 수 있는 데이터와 편집 가능한 데이터를 제한 하는 방법을 살펴보았습니다.

이 자습서에서는 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 데이터 삽입, 업데이트 및 삭제에 대 한 검사를 마칩니다. 다음 자습서 부터는 페이징 및 정렬 지원을 추가 하는 데 주의를 기울여야 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](adding-client-side-confirmation-when-deleting-vb.md)
