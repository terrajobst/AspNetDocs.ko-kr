---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
title: GridView에 단추 추가 및 응답 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 GridView 또는 DetailsView 컨트롤의 템플릿 및 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히, microsoft는
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 06c6bbd2-4bdc-435b-87a3-df2c868f4baa
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
msc.type: authoredcontent
ms.openlocfilehash: 8727d8faead02340d223c75845bf29f63d1a0834
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78442277"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-vb"></a>GridView에 단추를 추가하고 응답(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_VB.exe) 또는 [PDF 다운로드](adding-and-responding-to-buttons-to-a-gridview-vb/_static/datatutorial28vb1.pdf)

> 이 자습서에서는 GridView 또는 DetailsView 컨트롤의 템플릿 및 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히 사용자가 공급자를 통해 페이지를 이동할 수 있도록 하는 FormView가 있는 인터페이스를 빌드합니다.

## <a name="introduction"></a>소개

대부분의 보고 시나리오는 보고서 데이터에 대 한 읽기 전용 액세스를 포함 하지만 보고서에는 표시 되는 데이터에 따라 동작을 수행 하는 기능을 포함 하는 것이 일반적이 지 않습니다. 일반적으로이는 클릭 하면 다시 게시를 발생 시키고 일부 서버 쪽 코드를 호출 하는 보고서에 표시 되는 각 레코드에 Button, LinkButton 또는 ImageButton 웹 컨트롤을 추가 하는 것과 관련 된 것입니다. 레코드 별로 데이터를 편집 하 고 삭제 하는 것이 가장 일반적인 예입니다. 실제로 [데이터 삽입, 업데이트 및 삭제 자습서의 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 부터 편집 및 삭제는 코드를 한 줄도 작성 하지 않고도 GridView, DetailsView 및 FormView 컨트롤이 이러한 기능을 지원할 수 있도록 하는 것이 일반적입니다.

편집 및 삭제 단추 외에도 GridView, DetailsView 및 FormView 컨트롤에는 클릭할 때 일부 사용자 지정 서버 쪽 논리를 수행 하는 단추, Linkbutton 또는 ImageButtons이 포함 될 수 있습니다. 이 자습서에서는 GridView 또는 DetailsView 컨트롤의 템플릿 및 필드에 사용자 지정 단추를 추가 하는 방법을 살펴보겠습니다. 특히 사용자가 공급자를 통해 페이지를 이동할 수 있도록 하는 FormView가 있는 인터페이스를 빌드합니다. 지정 된 공급자의 경우 FormView는 클릭 하면 연결 된 모든 제품을 단종 됨으로 표시 하는 단추 웹 컨트롤과 함께 공급자에 대 한 정보를 표시 합니다. 또한 GridView는 선택한 공급자가 제공 하는 제품을 나열 하 고, 클릭 하는 경우 가격 및 할인 가격 단추가 포함 된 각 행을 나열 합니다 .이 단추를 클릭 하면 제품 s `UnitPrice` 10% 씩 증가 하거나 감소 합니다 (그림 1 참조).

[![FormView와 GridView 모두에 사용자 지정 작업을 수행 하는 단추가 포함 되어 있습니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image1.png)

**그림 1**: FormView와 GridView 모두에 사용자 지정 작업을 수행 하는 단추가 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image3.png)).

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>1 단계: 단추 자습서 웹 페이지 추가

사용자 지정 단추를 추가 하는 방법을 살펴보기 전에 먼저이 자습서에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `CustomButtons`이라는 새 폴더를 추가 하 여 시작 합니다. 다음으로 해당 폴더에 다음 두 개의 ASP.NET 페이지를 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `CustomButtons.aspx`

![사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image4.png)

**그림 2**: 사용자 지정 단추 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `CustomButtons` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image5.png)

**그림 3**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image7.png))

마지막으로 `Web.sitemap` 파일에 페이지를 항목으로 추가 합니다. 특히, 페이징 및 정렬 `<siteMapNode>`후에 다음 태그를 추가 합니다.

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 자습서 편집, 삽입 및 삭제를 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 사용자 지정 단추 자습서에 대 한 항목이 포함 됩니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image8.png)

**그림 4**: 이제 사이트 맵에 사용자 지정 단추 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>2 단계: 공급자를 나열 하는 FormView 추가

공급자를 나열 하는 FormView를 추가 하 여이 자습서를 시작 해 보세요. 소개에 설명 된 대로이 FormView를 사용 하면 사용자가 공급자를 통해 페이지를 이동 하 여 해당 공급자가 GridView에서 제공 하는 제품을 표시할 수 있습니다. 또한이 FormView에는 클릭 하면 모든 공급 업체 제품을 단종 됨으로 표시 하는 단추가 포함 됩니다. 사용자 지정 단추를 FormView에 추가 하기 전에 먼저 FormView를 만들어 공급자 정보를 표시 하도록 합니다.

먼저 `CustomButtons` 폴더에서 `CustomButtons.aspx` 페이지를 엽니다. 도구 상자에서 디자이너로 끌어온 다음 해당 `ID` 속성을 `Suppliers`으로 설정 하 여 페이지에 FormView를 추가 합니다. FormView의 스마트 태그에서 `SuppliersDataSource`라는 새 ObjectDataSource를 만들도록 옵트인 합니다.

[SuppliersDataSource 라는 새 ObjectDataSource를 만들 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image9.png)

**그림 5**: 이름이 `SuppliersDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image11.png))

이 새로운 ObjectDataSource를 구성 하 `SuppliersBLL` 클래스 s `GetSuppliers()` 메서드에서 쿼리 합니다 (그림 6 참조). 이 FormView는 공급자 정보를 업데이트 하기 위한 인터페이스를 제공 하지 않으므로 업데이트 탭의 드롭다운 목록에서 (없음) 옵션을 선택 합니다.

[SuppliersBLL 클래스 s GetSuppliers () 메서드를 사용 하도록 데이터 소스를 구성 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image12.png)

**그림 6**: `SuppliersBLL` 클래스 s `GetSuppliers()` 메서드를 사용 하도록 데이터 소스 구성 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image14.png))

ObjectDataSource를 구성 하 고 나면 Visual Studio에서 FormView에 대 한 `InsertItemTemplate`, `EditItemTemplate`및 `ItemTemplate` 생성 합니다. `InsertItemTemplate`를 제거 하 고 공급 업체의 회사 이름과 전화 번호를 표시 하도록 `ItemTemplate`를 `EditItemTemplate` 하 고 수정 합니다. 마지막으로 스마트 태그에서 페이징 사용 확인란을 선택 하거나 해당 `AllowPaging` 속성을 `True`로 설정 하 여 FormView에 대 한 페이징 지원을 설정 합니다. 이러한 변경 후 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample2.aspx)]

그림 7에서는 브라우저를 통해 볼 때 CustomButtons .aspx 페이지를 보여 줍니다.

[FormView ![현재 선택한 공급자의 CompanyName 및 Phone 필드를 나열 합니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image15.png)

**그림 7**: FormView에는 현재 선택 된 공급자의 `CompanyName` 및 `Phone` 필드가 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image17.png)).

## <a name="step-3-adding-a-gridview-that-lists-the-selected-supplier-s-products"></a>3 단계: 선택한 공급자 제품을 나열 하는 GridView 추가

FormView의 템플릿에 모든 제품 중단 단추를 추가 하기 전에 먼저 선택한 공급자가 제공 하는 제품을 나열 하는 FormView 아래에 GridView를 추가 하겠습니다. 이를 수행 하려면 페이지에 GridView를 추가 하 고 해당 `ID` 속성을 `SuppliersProducts`로 설정 하 고 `SuppliersProductsDataSource`라는 새 ObjectDataSource를 추가 합니다.

[SuppliersProductsDataSource 라는 새 ObjectDataSource를 만들 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image18.png)

**그림 8**: 이름이 `SuppliersProductsDataSource` 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image20.png))

ProductsBLL 클래스 s `GetProductsBySupplierID(supplierID)` 메서드를 사용 하도록이 ObjectDataSource를 구성 합니다 (그림 9 참조). 이 GridView는 제품 가격을 조정할 수 있지만 GridView에서 기본 제공 되는 편집 또는 삭제 기능을 사용 하지 않습니다. 따라서 ObjectDataSource s 업데이트, 삽입 및 삭제 탭에 대 한 드롭다운 목록을 (없음)으로 설정할 수 있습니다.

[ProductsBLL 클래스 s GetProductsBySupplierID (공급자) 메서드를 사용 하도록 데이터 소스를 구성 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image21.png)

**그림 9**: `ProductsBLL` 클래스 s `GetProductsBySupplierID(supplierID)` 메서드를 사용 하도록 데이터 소스 구성 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image23.png))

`GetProductsBySupplierID(supplierID)` 메서드는 입력 매개 변수를 허용 하므로 ObjectDataSource 마법사는이 매개 변수 값의 원본을 묻는 메시지를 표시 합니다. FormView에서 `SupplierID` 값을 전달 하려면 매개 변수 원본 드롭다운 목록을 Control로 설정 하 고 ControlID 드롭다운 목록을 `Suppliers` (2 단계에서 만든 FormView의 ID)로 설정 합니다.

[공급자 FormView 컨트롤에서 제공 되어야 하는 공급자 매개 변수를 나타내는 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image24.png)

**그림 10**: `Suppliers` FormView 컨트롤에서 *`supplierID`* 매개 변수를 가져와야 함을 나타냄 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image26.png))

ObjectDataSource 마법사를 완료 한 후 GridView에는 각 제품 데이터 필드에 대 한 BoundField 또는 CheckBoxField가 포함 됩니다. 이를 축소 하 여 `ProductName` 및 `UnitPrice` BoundFields를 `Discontinued` CheckBoxField와 함께 표시 합니다. 또한 텍스트의 서식을 통화로 지정 하도록 `UnitPrice` BoundField의 서식을 지정 합니다. GridView 및 `SuppliersProductsDataSource` ObjectDataSource s 선언 태그는 다음 태그와 유사 하 게 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample3.aspx)]

이 시점에서이 자습서는 마스터/세부 정보 보고서를 표시 하 여 사용자가 맨 위에 있는 FormView에서 공급자를 선택 하 고 맨 아래에 있는 GridView를 통해 해당 공급자가 제공 하는 제품을 볼 수 있도록 합니다. 그림 11은 FormView에서 도쿄 무역 공급자를 선택 하는 경우이 페이지의 스크린샷을 보여 줍니다.

[선택한 공급자 제품 ![GridView에 표시 됩니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image27.png)

**그림 11**: 선택한 공급자 제품이 GridView에 표시 됨 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image29.png))

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>4 단계: DAL 및 BLL 메서드를 만들어 공급자에 대 한 모든 제품 중단

FormView에 단추를 추가 하기 전에 클릭 하 여 모든 공급 업체의 제품을 중단 먼저이 작업을 수행 하는 DAL 및 BLL 모두에 메서드를 추가 해야 합니다. 특히이 메서드의 이름은 `DiscontinueAllProductsForSupplier(supplierID)`로 지정 됩니다. FormView s 단추를 클릭 하면 선택한 공급자를 전달 하 여 비즈니스 논리 계층에서이 메서드를 호출 합니다. `SupplierID`; 그러면 BLL은 해당 하는 데이터 액세스 계층 메서드를 호출 하 여 지정 된 공급 업체의 제품을 중단 하는 데이터베이스에 `UPDATE` 문을 실행 합니다.

이전 자습서에서 살펴본 것 처럼, DAL 메서드를 만든 다음 BLL 메서드를 만들고 마지막으로 ASP.NET 페이지에서 기능을 구현 하는 것부터 상향식 접근 방법을 사용 합니다. `App_Code/DAL` 폴더에서 `Northwind.xsd` 형식화 된 데이터 집합을 열고 `ProductsTableAdapter`에 새 메서드를 추가 합니다 (`ProductsTableAdapter`을 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택). 이렇게 하면 TableAdapter 쿼리 구성 마법사가 표시 되며,이 마법사에서 새 메서드를 추가 하는 과정을 안내 합니다. 먼저 DAL 메서드가 임시 SQL 문을 사용 한다는 것을 나타냅니다.

[임시 SQL 문을 사용 하 여 DAL 메서드를 만들 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image30.png)

**그림 12**: 임시 SQL 문을 사용 하 여 DAL 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image32.png))

다음으로 마법사에서 만들 쿼리 유형을 묻는 메시지를 표시 합니다. `DiscontinueAllProductsForSupplier(supplierID)` 메서드는 `Products` 데이터베이스 테이블을 업데이트 해야 하므로 지정 된 *`supplierID`* 에서 제공 하는 모든 제품에 대해 `Discontinued` 필드를 1로 설정 하 여 데이터를 업데이트 하는 쿼리를 만들어야 합니다.

[업데이트 쿼리 유형을 선택 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image33.png)

**그림 13**: 업데이트 쿼리 유형 선택 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image35.png))

다음 마법사 화면은 `Products` DataTable에 정의 된 각 필드를 업데이트 하는 TableAdapter s 기존 `UPDATE` 문을 제공 합니다. 이 쿼리 텍스트를 다음 문으로 바꿉니다.

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample4.sql)]

이 쿼리를 입력 하 고 다음을 클릭 하면 마지막 마법사 화면에서 새 메서드 이름 `DiscontinueAllProductsForSupplier`사용을 요청 합니다. 마침 단추를 클릭 하 여 마법사를 완료 합니다. 데이터 집합 디자이너로 돌아가면 `ProductsTableAdapter`에 `DiscontinueAllProductsForSupplier(@SupplierID)`라는 새 메서드가 표시 되어야 합니다.

[![새 DAL 메서드 이름 DiscontinueAllProductsForSupplier](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image36.png)

**그림 14**: 새 DAL 메서드 이름 `DiscontinueAllProductsForSupplier` ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image38.png))

데이터 액세스 계층에서 만든 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 사용 하 여 다음 태스크는 비즈니스 논리 계층에서 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 만드는 것입니다. 이 작업을 수행 하려면 `ProductsBLL` 클래스 파일을 열고 다음을 추가 합니다.

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample5.vb)]

이 메서드는 제공 된 *`supplierID`* 매개 변수 값을 따라 전달 하 여 DAL의 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 호출 합니다. 특정 상황에서 공급 업체 제품만 지원 하지 않는 비즈니스 규칙이 있는 경우 이러한 규칙을 BLL에서 구현 해야 합니다.

> [!NOTE]
> `ProductsBLL` 클래스의 `UpdateProduct` 오버 로드와 달리 `DiscontinueAllProductsForSupplier(supplierID)` 메서드 시그니처에는 `DataObjectMethodAttribute` 특성 (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`)이 포함 되지 않습니다. 이렇게 하면 업데이트 탭에 있는 ObjectDataSource s 데이터 원본 구성 마법사의 드롭다운 목록에서 `DiscontinueAllProductsForSupplier(supplierID)` 메서드가 제외 됩니다. ASP.NET 페이지의 이벤트 처리기에서 직접 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 호출 하기 때문에이 특성을 생략 했습니다.

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>5 단계: FormView에 모든 제품 중단 단추 추가

BLL 및 DAL의 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 사용 하 여 선택한 공급자에 대 한 모든 제품을 중단 하는 기능을 추가 하는 마지막 단계는 FormView s `ItemTemplate`에 단추 웹 컨트롤을 추가 하는 것입니다. 단추 텍스트를 사용 하 여 공급 업체의 전화 번호 아래에 이러한 단추를 추가 하 고 모든 제품 및 `ID` 속성 값 `DiscontinueAllProductsForSupplier`을 중단 합니다. FormView의 스마트 태그에서 템플릿 편집 링크를 클릭 하거나 (그림 15 참조) 선언적 구문을 통해 직접 디자이너를 통해이 단추 웹 컨트롤을 추가할 수 있습니다.

[![모든 제품 중단 단추 웹 컨트롤을 FormView s ItemTemplate에 추가 합니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image39.png)

**그림 15**: FormView s `ItemTemplate`에 모든 제품 중단 단추 웹 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image41.png))

페이지를 방문 하는 사용자가 단추를 클릭 하면 다시 게시 ensues 및 FormView s [`ItemCommand` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) 발생 합니다. 이 단추를 클릭 하는 것에 대 한 응답으로 사용자 지정 코드를 실행 하려면이 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다. 그러나 `ItemCommand` 이벤트는 FormView 내 *에서 Button,* LinkButton 또는 ImageButton 웹 컨트롤을 클릭할 때마다 발생 합니다. 즉, 사용자가 FormView에서 한 페이지에서 다른 페이지로 이동 하면 `ItemCommand` 이벤트가 발생 합니다. 사용자가 삽입, 업데이트 또는 삭제를 지 원하는 FormView에서 새로 만들기, 편집 또는 삭제를 클릭 하는 경우에도 마찬가지입니다.

클릭 한 단추에 관계 없이 `ItemCommand` 발생 하므로 이벤트 처리기에서 모든 제품 중단 단추를 클릭 했는지 또는 다른 단추 였는 지 여부를 확인 하는 방법이 필요 합니다. 이를 위해 단추 웹 컨트롤 s `CommandName` 속성을 일부 식별 값으로 설정할 수 있습니다. 단추를 클릭 하면이 `CommandName` 값이 `ItemCommand` 이벤트 처리기에 전달 되어 모든 제품 중단 단추가 클릭 된 단추 인지 여부를 확인할 수 있습니다. 모든 제품 중단 단추 `CommandName` 속성을 DiscontinueProducts로 설정 합니다.

마지막으로, 클라이언트 쪽 확인 대화 상자를 사용 하 여 사용자가 선택한 공급자의 제품을 정말로 중단 하려고 하는지 확인 합니다. 자습서를 [삭제할 때 클라이언트 쪽 확인 추가 확인](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb.md) 에서 살펴본 것 처럼 약간의 JavaScript를 사용 하 여이를 수행할 수 있습니다. 특히 웹 컨트롤의 OnClientClick 속성을 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');` 설정 합니다.

이러한 변경을 수행한 후에는 FormView의 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample6.aspx)]

다음으로, FormView s `ItemCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트 처리기에서는 먼저 모든 제품 중단 단추를 클릭 했는지 여부를 확인 해야 합니다. 이 경우 `ProductsBLL` 클래스의 인스턴스를 만들고 해당 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 호출 하 여 선택한 FormView의 `SupplierID`를 전달 합니다.

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample7.vb)]

Formview에서 현재 선택 된 공급자의 `SupplierID` [`SelectedValue` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)을 사용 하 여 액세스할 수 있습니다. `SelectedValue` 속성은 FormView에 표시 되는 레코드에 대 한 첫 번째 데이터 키 값을 반환 합니다. 데이터 키 값이 끌어오는 데이터 필드를 나타내는 FormView s [`DataKeyNames` 속성](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)은 2 단계에서 ObjectDataSource에 ObjectDataSource를 바인딩하는 경우 Visual Studio에서 자동으로 `SupplierID` 하도록 설정 되었습니다.

`ItemCommand` 이벤트 처리기를 만든 경우 잠시 시간을 걸리고 페이지를 테스트 합니다. Cooperativa de ' Las Cabras ' 공급자로 이동 합니다 (me의 FormView에서 다섯 번째 공급 업체). 이 공급 업체는 두 가지 제품인 Steso Cabrales와 Steso Manchego La Pastora를 제공 합니다 .이 두 제품은 모두 단종 *되지 않습니다* .

공동 운영, ' Las Cabras '가 비즈니스에 더 이상 없는 것으로 생각 하므로 제품이 중단 됩니다. 모든 제품 중단 단추를 클릭 합니다. 그러면 클라이언트 쪽 확인 대화 상자가 표시 됩니다 (그림 16 참조).

[![Coo Os Las Cabras는 두 개의 활성 제품을 제공 합니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image42.png)

**그림 16**: cooperativa De Cos Las Cabras는 두 개의 활성 제품 ([전체 크기 이미지를 보려면 클릭)을 제공 합니다](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image44.png).

클라이언트 쪽 확인 대화 상자에서 확인을 클릭 하면 양식 전송이 진행 되어 FormView s `ItemCommand` 이벤트가 발생 하는 포스트백이 발생 합니다. 그런 다음 만든 이벤트 처리기는 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 호출 하 고, 중단 Cabrales 및 Manchego La Pastora 제품을 모두 실행 합니다.

GridView의 뷰 상태를 사용 하지 않도록 설정한 경우에는 모든 다시 게시 시 GridView가 기본 데이터 저장소에 다시 바인딩 되므로 이러한 두 제품이 이제 중단 됩니다 (그림 17 참조). 그러나 GridView에서 뷰 상태를 사용 하지 않도록 설정한 경우이 변경을 수행한 후에는 데이터를 GridView에 수동으로 다시 바인딩해야 합니다. 이 작업을 수행 하려면 `DiscontinueAllProductsForSupplier(supplierID)` 메서드를 호출한 직후에 GridView의 `DataBind()` 메서드를 호출 하면 됩니다.

[모든 제품 중단 단추를 클릭 한 후에는 공급자 제품을 적절 하 게 업데이트 합니다. ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image45.png)

**그림 17**: 모든 제품 중단 단추를 클릭 하면 공급자 제품이 적절 하 게 업데이트 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image47.png)).

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-product-s-price"></a>6 단계: 제품 가격 조정을 위한 비즈니스 논리 계층에서 UpdateProduct 오버 로드 만들기

FormView의 모든 제품 중단 단추와 마찬가지로 GridView의 제품에 대 한 가격을 늘리거나 줄이는 단추를 추가 하려면 먼저 적절 한 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 해야 합니다. DAL에서 단일 제품 행을 업데이트 하는 메서드가 이미 있으므로 BLL에서 `UpdateProduct` 메서드에 대 한 새 오버 로드를 만들어 이러한 기능을 제공할 수 있습니다.

이전 `UpdateProduct` 오버 로드는 제품 필드를 스칼라 입력 값으로 결합 하 여 지정 된 제품에 대 한 필드만 업데이트 했습니다. 이 오버 로드의 경우에는이 표준에 따라 조금씩 다르며 대신 제품 `ProductID`을 전달 하 고, `UnitPrice` 조정 하는 데 필요한 백분율 (새로운 `UnitPrice`를 전달 하는 것과는 반대로)을 전달 합니다. 이 접근 방식을 사용 하면 현재 제품 `UnitPrice`를 확인 하는 것을 잊지 않아도 되므로 ASP.NET 페이지 코드를 작성 하는 데 필요한 코드를 단순화할 수 있습니다.

이 자습서에 대 한 `UpdateProduct` 오버 로드는 다음과 같습니다.

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample8.vb)]

이 오버 로드는 DAL s `GetProductByProductID(productID)` 메서드를 통해 지정 된 제품에 대 한 정보를 검색 합니다. 그런 다음 제품 `UnitPrice`에 데이터베이스 `NULL` 값이 할당 되었는지 확인 합니다. 이 경우 가격은 변경 되지 않은 상태로 유지 됩니다. 그러나`NULL` `UnitPrice` 값이 없는 경우 메서드는 지정 된 백분율 (`unitPriceAdjustmentPercent`)으로 제품의 `UnitPrice`를 업데이트 합니다.

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>7 단계: GridView에 증가 및 감소 단추 추가

GridView (및 DetailsView)는 모두 필드 컬렉션으로 구성 됩니다. BoundFields, CheckBoxFields 및 템플릿 필드 외에도 ASP.NET에는 각 행에 대 한 단추, LinkButton 또는 ImageButton이 있는 열로 렌더링 되는 ButtonField가 포함 되어 있습니다. FormView와 마찬가지로 GridView 페이징 단추, 편집 또는 삭제 단추, 정렬 단추 등에서 단추 *를 클릭 하면* 포스트백이 발생 하 고 gridview s [`RowCommand` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)발생 합니다.

ButtonField에는 각 단추 `CommandName` 속성에 지정 된 값을 할당 하는 `CommandName` 속성이 있습니다. FormView와 마찬가지로 `CommandName` 값은 `RowCommand` 이벤트 처리기에서 클릭 한 단추를 확인 하는 데 사용 됩니다.

2 개의 새 ButtonFields를 GridView에 추가 합니다. 하나는 단추 텍스트 가격과 10%이 고 다른 하나는 Price-10%입니다. 이러한 ButtonFields를 추가 하려면 GridView의 스마트 태그에서 열 편집 링크를 클릭 하 고 왼쪽 위에 있는 목록에서 Buttonfields 필드 유형을 선택한 다음 추가 단추를 클릭 합니다.

![GridView에 두 개의 ButtonFields를 추가 합니다.](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image48.png)

**그림 18**: GridView에 두 개의 buttonfields 추가

두 ButtonFields를 처음 두 개의 GridView 필드로 표시 되도록 이동 합니다. 그런 다음 이러한 두 ButtonFields의 `Text` 속성을 Price + 10% 및 Price-10%로 설정 하 고 `CommandName` 속성을 각각 IncreasePrice 및 DecreasePrice로 설정 합니다. 기본적으로 ButtonField는 단추의 열을 Linkbutton으로 렌더링 합니다. 그러나 ButtonField s [`ButtonType` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)을 통해 변경할 수 있습니다. 이러한 두 ButtonFields가 일반 푸시 단추로 렌더링 되도록 합니다. 따라서 `ButtonType` 속성을 `Button`로 설정 합니다. 그림 19에서는 이러한 변경이 수행 된 후의 필드 대화 상자를 보여 줍니다. 다음은 GridView의 선언적 태그입니다.

![ButtonFields Text, CommandName 및 ButtonType 속성 구성](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image49.png)

**그림 19**: buttonfields `Text`, `CommandName`및 `ButtonType` 속성 구성

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample9.aspx)]

이러한 ButtonFields를 만든 마지막 단계는 GridView s `RowCommand` 이벤트에 대 한 이벤트 처리기를 만드는 것입니다. 이 이벤트 처리기는 Price + 10% 또는 Price-10% 단추를 클릭 했기 때문에 발생 한 경우 단추를 클릭 한 행에 대 한 `ProductID`를 확인 한 다음 `ProductsBLL` 클래스 s `UpdateProduct` 메서드를 호출 하 여 적절 한 `UnitPrice` 비율 조정을 `ProductID`와 함께 전달 해야 합니다. 다음 코드에서는 이러한 작업을 수행 합니다.

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample10.vb)]

가격 + 10% 또는 가격-10% 단추가 클릭 된 행의 `ProductID`를 확인 하려면 GridView의 `DataKeys` 컬렉션을 참조 해야 합니다. 이 컬렉션은 각 GridView 행의 `DataKeyNames` 속성에 지정 된 필드의 값을 포함 합니다. ObjectDataSource를 GridView에 바인딩하는 경우 Visual Studio에서 GridView s `DataKeyNames` 속성이 ProductID로 설정 되었으므로 지정 된 *rowIndex*에 대해 `ProductID`을 제공 `DataKeys(rowIndex).Value`.

ButtonField는 `e.CommandArgument` 매개 변수를 통해 단추를 클릭 한 행의 *rowIndex* 에서 자동으로 전달 됩니다. 따라서 Price + 10% 또는 Price-10% 단추가 클릭 된 행의 `ProductID`를 확인 하려면 `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`를 사용 합니다.

모든 제품 중단 단추와 마찬가지로 GridView의 뷰 상태를 사용 하지 않도록 설정한 경우 모든 다시 게시 시 GridView가 기본 데이터 저장소에 다시 바인딩 되므로 다음을 클릭 하 여 발생 하는 가격 변경 내용을 반영 하도록 즉시 업데이트 됩니다. 단추 중 하나입니다. 그러나 GridView에서 뷰 상태를 사용 하지 않도록 설정한 경우이 변경을 수행한 후에는 데이터를 GridView에 수동으로 다시 바인딩해야 합니다. 이 작업을 수행 하려면 `UpdateProduct` 메서드를 호출한 직후에 GridView의 `DataBind()` 메서드를 호출 하면 됩니다.

그림 20은 Grandma 최소라의 Homestead에서 제공 하는 제품을 볼 때 페이지를 보여 줍니다. 그림 21은 Grandma의 Boysenberry 스프레드에서 Price + 10% 단추를 두 번 클릭 하 고 Northwoods Cranberry 기술인의 경우 가격-10% 단추를 한 번 클릭 한 후의 결과를 보여 줍니다.

[GridView에 가격 + 10% 및 가격-10% 단추가 포함 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image50.png)

**그림 20**: GridView는 가격 + 10% 및 가격-10% 단추 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image52.png))를 포함 합니다.

[가격 + 10% 및 가격-10% 단추를 통해 첫 번째 및 세 번째 제품의 가격이 업데이트 된 ![](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image53.png)

**그림 21**: 첫 번째와 세 번째 제품의 가격은 가격 + 10% 및 가격-10% 단추 ([전체 크기 이미지를 보려면 클릭](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image55.png))를 통해 업데이트 되었습니다.

> [!NOTE]
> GridView (및 DetailsView)에는 해당 템플릿 필드에 단추, Linkbutton 또는 ImageButtons가 추가 될 수도 있습니다. BoundField와 마찬가지로 이러한 단추를 클릭 하면 다시 게시를 유도 하 고 GridView s `RowCommand` 이벤트를 발생 시킵니다. 그러나 Templatefield로 변환에 단추를 추가 하는 경우 단추 `CommandArgument`는 ButtonFields를 사용할 때와 마찬가지로 행의 인덱스로 자동으로 설정 되지 않습니다. `RowCommand` 이벤트 처리기 내에서 클릭 된 단추의 행 인덱스를 확인 해야 하는 경우 다음과 같은 코드를 사용 하 여 Templatefield로 변환 내에서 해당 선언적 구문에서 단추 `CommandArgument` 속성을 수동으로 설정 해야 합니다.  
> `<asp:Button runat="server" ... CommandArgument='<%# CType(Container, GridViewRow).RowIndex %>' />`입니다.

## <a name="summary"></a>요약

GridView, DetailsView 및 FormView 컨트롤 모두 단추, Linkbutton 또는 ImageButtons를 포함할 수 있습니다. 이러한 단추를 클릭 하면 포스트백이 발생 하 고 FormView 및 DetailsView 컨트롤과 GridView의 `RowCommand` 이벤트에서 `ItemCommand` 이벤트가 발생 합니다. 이러한 데이터 웹 컨트롤에는 레코드 삭제 또는 편집과 같은 일반적인 명령 관련 동작을 처리 하는 기본 제공 기능이 있습니다. 그러나 클릭 하면 고유한 사용자 지정 코드를 실행 하 여 응답 하는 단추를 사용할 수도 있습니다.

이를 위해 `ItemCommand` 또는 `RowCommand` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. 이 이벤트 처리기에서는 먼저 들어오는 `CommandName` 값을 확인 하 여 클릭 한 단추를 확인 한 다음 적절 한 사용자 지정 작업을 수행 합니다. 이 자습서에서는 단추 및 ButtonFields를 사용 하 여 지정 된 공급자에 대 한 모든 제품을 중단 하거나 특정 제품의 가격을 10%로 늘리거나 줄이는 방법에 대해 살펴보았습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](adding-and-responding-to-buttons-to-a-gridview-cs.md)
