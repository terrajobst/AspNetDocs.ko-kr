---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 형식화 된 데이터 집합의 Tableadapter에 대 한 기존 저장 프로시저 사용 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 TableAdapter 마법사를 사용 하 여 새 저장 프로시저를 생성 하는 방법에 대해 알아보았습니다. 이 자습서에서는 동일한 TableAdapter를 확인 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: e35c3d6a98516a07f6119e6cb9dbeb99bc28fe33
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74613862"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>형식화된 데이터 세트의 TableAdapter에 대한 기존 저장 프로시저 사용(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip) 또는 [PDF 다운로드](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> 이전 자습서에서는 TableAdapter 마법사를 사용 하 여 새 저장 프로시저를 생성 하는 방법에 대해 알아보았습니다. 이 자습서에서는 동일한 TableAdapter 마법사에서 기존 저장 프로시저를 사용할 수 있는 방법에 대해 알아봅니다. 데이터베이스에 새 저장 프로시저를 수동으로 추가 하는 방법에 대해서도 알아봅니다.

## <a name="introduction"></a>소개

[이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 에서는 저장 프로시저를 사용 하 여 임시 SQL 문이 아닌 데이터에 액세스 하도록 형식화 된 데이터 집합의 tableadapter를 구성 하는 방법을 살펴보았습니다. 특히 TableAdapter 마법사에서 이러한 저장 프로시저를 자동으로 만드는 방법을 살펴보았습니다. 레거시 응용 프로그램을 ASP.NET 2.0로 포팅 하거나 기존 데이터 모델에 대 한 ASP.NET 2.0 웹 사이트를 빌드할 때 데이터베이스에 필요한 저장 프로시저가 이미 포함 되어 있을 수 있습니다. 또는 저장 프로시저를 자동으로 생성 하는 TableAdapter 마법사 이외의 일부 도구를 사용 하거나 저장 프로시저를 직접 만들 수 있습니다.

이 자습서에서는 기존 저장 프로시저를 사용 하도록 TableAdapter를 구성 하는 방법을 살펴봅니다. Northwind 데이터베이스에는 몇 가지 기본 제공 저장 프로시저 집합만 포함 되어 있으므로 Visual Studio 환경을 통해 데이터베이스에 새 저장 프로시저를 수동으로 추가 하는 데 필요한 단계를 살펴볼 것입니다. S를 시작 하겠습니다.

> [!NOTE]
> [트랜잭션 내에서 데이터베이스 수정 내용 래핑](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 자습서에서는 트랜잭션을 지원 하기 위해 TableAdapter에 메서드를 추가 했습니다 (`BeginTransaction`, `CommitTransaction`등). 또는 데이터 액세스 계층 코드를 수정 하지 않아도 되는 저장 프로시저 내에서 트랜잭션을 완전히 관리할 수 있습니다. 이 자습서에서는 트랜잭션 범위 내에서 저장 프로시저를 실행 하는 데 사용 되는 T-sql 명령을 살펴보겠습니다.

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>1 단계: Northwind 데이터베이스에 저장 프로시저 추가

Visual Studio를 사용 하면 데이터베이스에 새 저장 프로시저를 쉽게 추가할 수 있습니다. `Products` 테이블의 모든 열을 반환 하는 새 저장 프로시저를 Northwind 데이터베이스에 추가 하 여 특정 `CategoryID` 값이 있는 테이블을 만듭니다. 서버 탐색기 창에서 Northwind 데이터베이스를 확장 하 여 해당 폴더 (데이터베이스 다이어그램, 테이블, 뷰 등)가 표시 되도록 합니다. 이전 자습서에서 살펴본 것 처럼 저장 프로시저 폴더에는 데이터베이스의 기존 저장 프로시저가 포함 됩니다. 새 저장 프로시저를 추가 하려면 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 새 저장 프로시저 추가 옵션을 선택 하면 됩니다.

[저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저를 추가 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**그림 1**: 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 저장 프로시저 추가 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png))

그림 1에 나와 있는 것 처럼 새 저장 프로시저 추가 옵션을 선택 하면 Visual Studio에서 저장 프로시저를 만드는 데 필요한 SQL 스크립트의 개요와 함께 스크립트 창이 열립니다. 이 스크립트를 실행 하 고 실행 하 여 저장 프로시저를 데이터베이스에 추가 하는 작업입니다.

다음 스크립트를 입력 합니다.

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

이 스크립트는 실행 될 때 `Products_SelectByCategoryID`라는 Northwind 데이터베이스에 새 저장 프로시저를 추가 합니다. 이 저장 프로시저는 `int`형식의 단일 입력 매개 변수 (`@CategoryID`)를 수락 하 고 일치 하는 `CategoryID` 값을 사용 하 여 해당 제품에 대 한 모든 필드를 반환 합니다.

이 `CREATE PROCEDURE` 스크립트를 실행 하 고 데이터베이스에 저장 프로시저를 추가 하려면 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 누릅니다. 이렇게 하면 저장 프로시저 폴더가 새로 고쳐지고 새로 만든 저장 프로시저가 표시 됩니다. 또한 창의 스크립트는 `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID`에서 `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`로 미묘한 변경 됩니다. `CREATE PROCEDURE` 새 저장 프로시저를 데이터베이스에 추가 하 고 `ALTER PROCEDURE`는 기존 저장 프로시저를 업데이트 합니다. 스크립트의 시작이 `ALTER PROCEDURE`변경 되었으므로 저장 프로시저 입력 매개 변수 또는 SQL 문을 변경 하 고 저장 아이콘을 클릭 하면 저장 프로시저가 이러한 변경 내용으로 업데이트 됩니다.

그림 2에서는 `Products_SelectByCategoryID` 저장 프로시저를 저장 한 후의 Visual Studio를 보여 줍니다.

[저장 프로시저 Products_SelectByCategoryID를 데이터베이스에 추가 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**그림 2**: 저장 프로시저 `Products_SelectByCategoryID` 데이터베이스에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)).

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>2 단계: 기존 저장 프로시저를 사용 하도록 TableAdapter 구성

이제 `Products_SelectByCategoryID` 저장 프로시저를 데이터베이스에 추가 했으므로 해당 메서드 중 하나가 호출 될 때이 저장 프로시저를 사용 하도록 데이터 액세스 계층을 구성할 수 있습니다. 특히 방금 만든 `Products_SelectByCategoryID` 저장 프로시저를 호출 하는 `NorthwindWithSprocs` 형식화 된 데이터 집합의 `ProductsTableAdapter`에 `GetProductsByCategoryID(<_i22_>categoryID)<!--_i22_-->` 메서드를 추가 합니다.

`NorthwindWithSprocs` 데이터 집합을 열어 시작 합니다. `ProductsTableAdapter`를 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 하 여 TableAdapter 쿼리 구성 마법사를 시작 합니다. [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) 에서는 TableAdapter가 새 저장 프로시저를 만들도록 옵트인 했습니다. 그러나이 자습서에서는 새 TableAdapter 메서드를 기존 `Products_SelectByCategoryID` 저장 프로시저에 연결 하려고 합니다. 따라서 마법사의 첫 번째 단계에서 기존 저장 프로시저 사용 옵션을 선택 하 고 다음을 클릭 합니다.

[![기존 저장 프로시저 사용 옵션을 선택 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**그림 3**: 기존 저장 프로시저 사용 옵션 선택 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png))

다음 화면에서는 데이터베이스의 저장 프로시저를 사용 하 여 채워진 드롭다운 목록을 제공 합니다. 저장 프로시저를 선택 하면 왼쪽에 입력 매개 변수가 표시 되 고 오른쪽에는 반환 된 데이터 필드가 표시 됩니다. 목록에서 `Products_SelectByCategoryID` 저장 프로시저를 선택 하 고 다음을 클릭 합니다.

[Products_SelectByCategoryID 저장 프로시저를 선택 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**그림 4**: `Products_SelectByCategoryID` 저장 프로시저 선택 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png))

다음 화면에서는 저장 프로시저에서 반환 되는 데이터 종류를 묻고 여기에서 대답은 TableAdapter s 메서드에서 반환 하는 형식을 결정 합니다. 예를 들어 테이블 형식 데이터가 반환 되는 것으로 표시 되는 경우이 메서드는 저장 프로시저에서 반환 하는 레코드로 채워진 `ProductsDataTable` 인스턴스를 반환 합니다. 반대로이 저장 프로시저가 단일 값을 반환 하는 것으로 표시 되는 경우, TableAdapter는 저장 프로시저에서 반환 된 첫 번째 레코드의 첫 번째 열에 값이 할당 된 `Object`을 반환 합니다.

`Products_SelectByCategoryID` 저장 프로시저는 특정 범주에 속하는 모든 제품을 반환 하기 때문에 첫 번째 응답 표 형식 데이터를 선택 하 고 다음을 클릭 합니다.

[저장 프로시저에서 테이블 형식 데이터를 반환 함을 나타내는 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**그림 5**: 저장 프로시저에서 테이블 형식 데이터를 반환 하도록 지정 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png))

그 다음에는 사용할 메서드 패턴과 이러한 메서드의 이름을 차례로 지정 해야 합니다. DataTable 채우기 및 DataTable 옵션 반환 옵션을 모두 선택 된 상태로 두고 메서드 이름을 `FillByCategoryID` 및 `GetProductsByCategoryID`으로 바꿉니다. 그런 후 다음을 클릭 하 여 마법사에서 수행할 작업의 요약을 검토 합니다. 모든 항목이 올바르면 마침을 클릭 합니다.

[![메서드 이름 FillByCategoryID 및 GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**그림 6**: 메서드 이름 `FillByCategoryID` 및 `GetProductsByCategoryID` ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))

> [!NOTE]
> 방금 생성, `FillByCategoryID` 및 `GetProductsByCategoryID`TableAdapter 메서드는 `Integer`형식의 입력 매개 변수를 필요로 합니다. 이 입력 매개 변수 값은 `@CategoryID` 매개 변수를 통해 저장 프로시저에 전달 됩니다. `Products_SelectByCategory` 저장 프로시저의 매개 변수를 수정 하는 경우 이러한 TableAdapter 메서드에 대 한 매개 변수도 업데이트 해야 합니다. [이전 자습서](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)에서 설명한 대로이 작업은 매개 변수 컬렉션에서 매개 변수를 수동으로 추가 또는 제거 하거나 TableAdapter 마법사를 다시 실행 하 여 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>3 단계: BLL에`GetProductsByCategoryID(categoryID)`메서드 추가

`GetProductsByCategoryID` DAL 메서드가 완료 되 면 다음 단계는 비즈니스 논리 계층에서이 메서드에 대 한 액세스를 제공 하는 것입니다. `ProductsBLLWithSprocs` 클래스 파일을 열고 다음 메서드를 추가 합니다.

[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

이 BLL 메서드는 단순히 `ProductsTableAdapter` s `GetProductsByCategoryID` 메서드에서 반환 된 `ProductsDataTable` 반환 합니다. `DataObjectMethodAttribute` 특성은 ObjectDataSource s 데이터 원본 구성 마법사에서 사용 하는 메타 데이터를 제공 합니다. 특히이 메서드는 선택 탭의 드롭다운 목록에 표시 됩니다.

## <a name="step-4-displaying-products-by-category"></a>4 단계: 범주별 제품 표시

새로 추가 된 `Products_SelectByCategoryID` 저장 프로시저 및 해당 DAL 및 BLL 메서드를 테스트 하려면 DropDownList 및 GridView를 포함 하는 ASP.NET 페이지를 만들어 보겠습니다. DropDownList에는 데이터베이스의 모든 범주가 나열 되 고 GridView에는 선택한 범주에 속한 제품이 표시 됩니다.

> [!NOTE]
> 이전 자습서에서 Dropdownlist를 사용 하 여 마스터/세부 인터페이스를 만들었습니다. 이러한 마스터/세부 정보 보고서를 구현 하는 방법에 대 한 자세한 내용은 DropDownList 자습서를 [사용 하 여 마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) 을 참조 하세요.

`AdvancedDAL` 폴더에서 `ExistingSprocs.aspx` 페이지를 열고 도구 상자의 DropDownList를 디자이너로 끌어 옵니다. DropDownList s `ID` 속성을 `Categories`로 설정 하 고 `AutoPostBack` 속성을 `True`로 설정 합니다. 그런 다음 해당 스마트 태그에서 DropDownList을 `CategoriesDataSource`라는 새 ObjectDataSource에 바인딩합니다. `CategoriesBLL` 클래스 s `GetCategories` 메서드에서 데이터를 검색 하도록 ObjectDataSource를 구성 합니다. 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 합니다.

[범주 Bll 클래스의 GetCategories 메서드에서 데이터를 검색 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**그림 7**: `CategoriesBLL` 클래스 s `GetCategories` 메서드에서 데이터 검색 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**그림 8**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png))

ObjectDataSource 마법사를 완료 한 후에는 `CategoryName` 데이터 필드를 표시 하 고 `CategoryID` 필드를 각 `ListItem`에 대 한 `Value` 사용 하도록 DropDownList을 구성 합니다.

이 시점에서 DropDownList 및 ObjectDataSource s 선언 태그는 다음과 유사 합니다.

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

그런 다음 GridView를 디자이너에 끌어 DropDownList 아래에 배치 합니다. GridView s `ID`를 `ProductsByCategory`로 설정 하 고 스마트 태그에서 `ProductsByCategoryDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsByCategoryDataSource` ObjectDataSource를 구성 하 여 `ProductsBLLWithSprocs` 클래스를 사용 하 고 `GetProductsByCategoryID(categoryID)` 메서드를 사용 하 여 해당 데이터를 검색 하도록 합니다. 이 GridView는 데이터를 표시 하는 데만 사용 되므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 하 고 다음을 클릭 합니다.

[ProductsBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**그림 9**: `ProductsBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png))

[GetProductsByCategoryID (categoryID) 메서드에서 데이터를 검색 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**그림 10**: `GetProductsByCategoryID(categoryID)` 메서드에서 데이터 검색 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png))

선택 탭에서 선택한 메서드에 매개 변수가 필요 하므로 마법사의 마지막 단계에서 매개 변수 원본에 대 한 메시지를 표시 합니다. 매개 변수 소스 드롭다운 목록을 제어로 설정 하 고 ControlID 드롭다운 목록에서 `Categories` 컨트롤을 선택 합니다. 마침을 클릭하여 마법사를 완료합니다.

[DropDownList 범주를 categoryID 매개 변수의 소스로 사용 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**그림 11**: `categoryID` 매개 변수의 소스로 `Categories` DropDownList 사용 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png))

ObjectDataSource 마법사가 완료 되 면 Visual Studio에서 각 제품 데이터 필드에 대 한 BoundFields 및 CheckBoxField를 추가 합니다. 이러한 필드는 적절 하 게 사용자 지정할 수 있습니다.

브라우저를 통해 페이지를 방문 합니다. 페이지를 방문할 때 음료 범주가 선택 되 고 표에 해당 제품이 나열 됩니다. 그림 12와 같이 드롭다운 목록을 대체 범주로 변경 하면 다시 게시를 수행 하 고 새로 선택한 범주의 제품을 사용 하 여 그리드를 다시 로드 합니다.

[생성 범주의 제품이 표시 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**그림 12**: 생성 범주의 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)).

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>5 단계: 트랜잭션 범위 내에서 저장 프로시저 s 문 래핑

[트랜잭션 내에서 데이터베이스 수정 내용 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서는 트랜잭션 범위 내에서 일련의 데이터베이스 수정 문을 수행 하는 기술에 대해 설명 했습니다. 트랜잭션의 파라솔에서 수행 된 수정 내용이 모두 성공 하거나 모두 실패 하 여 원자성을 보장 합니다. 트랜잭션을 사용 하는 방법은 다음과 같습니다.

- `System.Transactions` 네임 스페이스의 클래스 사용
- 데이터 액세스 계층에 `SqlTransaction`와 같은 ADO.NET 클래스를 사용 하는 경우
- 저장 프로시저 내에서 직접 T-sql 트랜잭션 명령 추가

*트랜잭션 내에서 데이터베이스 수정 내용 래핑* 자습서에서는 DAL의 ADO.NET 클래스를 사용 했습니다. 이 자습서의 나머지 부분에서는 저장 프로시저 내에서 T-sql 명령을 사용 하 여 트랜잭션을 관리 하는 방법을 살펴봅니다.

트랜잭션을 수동으로 시작, 커밋 및 롤백하는 세 가지 주요 SQL 명령은 각각 `BEGIN TRANSACTION`, `COMMIT TRANSACTION`및 `ROLLBACK TRANSACTION`입니다. ADO.NET 접근 방식과 마찬가지로 저장 프로시저 내에서 트랜잭션을 사용 하는 경우에는 다음 패턴을 적용 해야 합니다.

1. 트랜잭션의 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계의 문 중 하나에 오류가 있는 경우 트랜잭션을 롤백합니다.
4. 2 단계의 모든 문이 오류 없이 완료 되 면 트랜잭션을 커밋합니다.

이 패턴은 다음 템플릿을 사용 하 여 T-sql 구문에서 구현할 수 있습니다.

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

이 템플릿은 SQL Server 2005에 대 한 새로운 구문의 `TRY...CATCH` 블록을 정의 하 여 시작 합니다. Visual Basic의 `Try...Catch` 블록과 마찬가지로 SQL `TRY...CATCH` 블록은 `TRY` 블록의 문을 실행 합니다. 문에서 오류가 발생 하면 컨트롤이 `CATCH` 블록으로 즉시 전송 됩니다.

트랜잭션을 구성을 하는 SQL 문을 실행 하는 동안 오류가 발생 하지 않는 경우 `COMMIT TRANSACTION` 문은 변경 내용을 커밋하고 트랜잭션을 완료 합니다. 그러나 문 중 하나에서 오류가 발생 하는 경우 `CATCH` 블록의 `ROLLBACK TRANSACTION` 트랜잭션이 시작 되기 전의 상태로 데이터베이스를 반환 합니다. 또한 저장 프로시저는 [RAISERROR 명령을](https://msdn.microsoft.com/library/ms178592.aspx)사용 하 여 오류를 발생 시킵니다. 그러면 응용 프로그램에서 `SqlException` 발생 합니다.

> [!NOTE]
> `TRY...CATCH` 블록은 SQL Server 2005의 새로운 버전 이므로 이전 버전의 Microsoft SQL Server를 사용 하는 경우 위의 템플릿이 작동 하지 않습니다. SQL Server 2005을 사용 하지 않는 경우 다른 버전의 SQL Server 사용할 템플릿에 대 한 [SQL Server 저장 프로시저의 트랜잭션 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) 를 참조 하세요.

구체적인 예를 살펴보겠습니다. `Categories` 테이블과 `Products` 테이블 사이에 foreign key 제약 조건이 있습니다. 즉, `Products` 테이블의 각 `CategoryID` 필드가 `CategoryID` 테이블의 `Categories` 값에 매핑되어야 합니다. 연결 된 제품을 포함 하는 범주를 삭제 하려고 시도 하는 등이 제약 조건을 위반 하는 동작은 foreign key 제약 조건 위반을 발생 시킬 수 있습니다. 이를 확인 하려면 이진 데이터 작업 섹션 (`~/BinaryData/UpdatingAndDeleting.aspx`)에서 기존 이진 데이터 업데이트 및 삭제 예제를 다시 방문 합니다. 이 페이지에는 시스템의 각 범주가 편집 및 삭제 단추와 함께 나열 됩니다 (그림 13 참조). 예를 들어 음료와 같은 관련 제품을 포함 하는 범주를 삭제 하려고 하면 foreign key 제약 조건 위반으로 인해 삭제가 실패 합니다 (그림 14 참조).

[편집 및 삭제 단추가 있는 GridView에 각 범주가 표시 ![](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**그림 13**: 각 범주는 편집 및 삭제 단추가 있는 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)).

[![기존 제품을 포함 하는 범주를 삭제할 수 없습니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**그림 14**: 기존 제품을 포함 하는 범주를 삭제할 수 없음 ([전체 크기 이미지를 보려면 클릭](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png))

그러나 연결 된 제품이 있는지 여부에 관계 없이 범주를 삭제할 수 있도록 허용 하려고 합니다. 제품을 삭제 하는 범주는 기존 제품을 삭제 하는 것을 가정 합니다. 다른 옵션은 단순히 products `CategoryID` 값을 `NULL`로 설정 하는 것입니다. 이 기능은 foreign key 제약 조건의 cascade 규칙을 통해 구현할 수 있습니다. 또는 `@CategoryID` 입력 매개 변수를 허용 하는 저장 프로시저를 만들고, 호출 되는 경우 연결 된 모든 제품과 지정 된 범주를 명시적으로 삭제 합니다.

이러한 저장 프로시저의 첫 번째 시도는 다음과 같습니다.

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

이 작업은 연결 된 제품 및 범주를 명확 하 게 삭제 하지만 트랜잭션 상위에서이를 수행 하지는 않습니다. 특정 `@CategoryID` 값의 삭제를 금지 하는 `Categories`에 대 한 다른 foreign key 제약 조건이 있다고 가정 합니다. 이 경우 범주를 삭제 하기 전에 모든 제품을 삭제 하는 것이 문제입니다. 이러한 범주의 경우이 저장 프로시저는 모든 제품을 제거 하 고, 범주가 남아 있는 동안에도 다른 테이블에는 관련 레코드가 있기 때문입니다.

그러나 저장 프로시저가 트랜잭션 범위 내에서 래핑된 경우에는 `Products` 테이블에 대 한 삭제가 `Categories`에 대해 실패 한 삭제를 롤백합니다. 다음 저장 프로시저 스크립트는 트랜잭션을 사용 하 여 두 `DELETE` 문 간의 원자성을 보장 합니다.

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

`Categories_Delete` 저장 프로시저를 Northwind 데이터베이스에 추가 합니다. 데이터베이스에 저장 프로시저를 추가 하는 방법에 대 한 자세한 내용은 1 단계를 다시 참조 하세요.

## <a name="step-6-updating-thecategoriestableadapter"></a>6 단계:`CategoriesTableAdapter` 업데이트

데이터베이스에 `Categories_Delete` 저장 프로시저를 추가 했지만 현재 DAL은 임시 SQL 문을 사용 하 여 삭제를 수행 하도록 구성 되어 있습니다. `CategoriesTableAdapter`를 업데이트 하 고 대신 `Categories_Delete` 저장 프로시저를 사용 하도록 지시 해야 합니다.

> [!NOTE]
> 이 자습서의 앞부분에서는 `NorthwindWithSprocs` 데이터 집합으로 작업 했습니다. 그러나 해당 데이터 집합에는 단일 엔터티 `ProductsDataTable`만 있으며 범주를 사용 해야 합니다. 따라서이 자습서의 나머지 부분에서는 `Northwind` 데이터 집합을 참조 하는 데이터 액세스 계층에 대해 이야기 했을 때 처음에 [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서 만든 것입니다.

Northwind 데이터 집합을 열고 `CategoriesTableAdapter`를 선택한 다음 속성 창로 이동 합니다. 속성 창는 TableAdapter에서 사용 되는 `InsertCommand`, `UpdateCommand`, `DeleteCommand`및 `SelectCommand`와 해당 이름 및 연결 정보를 나열 합니다. `DeleteCommand` 속성을 확장 하 여 세부 정보를 확인 합니다. 그림 15에 표시 된 것 처럼 `DeleteCommand` s `CommandType` 속성은 텍스트로 설정 됩니다 .이 속성은 `CommandText` 속성의 텍스트를 임시 SQL 쿼리로 보내도록 지시 합니다.

![디자이너에서 CategoriesTableAdapter를 선택 하 여 속성 창에서 해당 속성을 확인 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**그림 15**: 디자이너에서 `CategoriesTableAdapter`를 선택 하 여 속성 창에서 속성 보기

이러한 설정을 변경 하려면 속성 창에서 (DeleteCommand) 텍스트를 선택 하 고 드롭다운 목록에서 (새로 만들기)를 선택 합니다. 이렇게 하면 `CommandText`, `CommandType`및 `Parameters` 속성에 대 한 설정이 지워집니다. 그런 다음 `CommandType` 속성을 `StoredProcedure`로 설정 하 고 `CommandText`에 대 한 저장 프로시저의 이름 (`dbo.Categories_Delete`)을 입력 합니다. 이 순서로 속성을 입력 한 다음 `CommandType` 먼저 입력 한 다음 `CommandText` 하면 Visual Studio에서 자동으로 매개 변수 컬렉션을 채웁니다. 이러한 속성을이 순서로 입력 하지 않는 경우 매개 변수 컬렉션 편집기를 통해 수동으로 매개 변수를 추가 해야 합니다. 두 경우 모두 매개 변수 속성에서 줄임표를 클릭 하 여 매개 변수 컬렉션 편집기를 표시 하 여 올바른 매개 변수 설정이 변경 되었는지 확인 하는 것이 좋습니다 (그림 16 참조). 대화 상자에 매개 변수가 표시 되지 않는 경우 `@CategoryID` 매개 변수를 수동으로 추가 합니다. `@RETURN_VALUE` 매개 변수를 추가할 필요가 없습니다.

![매개 변수 설정이 올바른지 확인 합니다.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**그림 16**: 매개 변수 설정이 올바른지 확인

DAL이 업데이트 되 면 범주를 삭제 하면 연결 된 모든 제품이 자동으로 삭제 되 고 트랜잭션 상위에서이를 수행 합니다. 이를 확인 하려면 기존 이진 데이터 업데이트 및 삭제 페이지로 돌아가서 범주 중 하나에 대 한 삭제 단추를 클릭 합니다. 마우스를 한 번 클릭 하면 범주와 관련 된 모든 제품이 삭제 됩니다.

> [!NOTE]
> 선택한 범주와 함께 여러 제품을 삭제 하는 `Categories_Delete` 저장 프로시저를 테스트 하기 전에 데이터베이스의 백업 복사본을 만드는 것이 좋습니다. `App_Data`에서 `NORTHWND.MDF` 데이터베이스를 사용 하는 경우 Visual Studio를 닫고 `App_Data`의 MDF 및 LDF 파일을 다른 폴더에 복사 하면 됩니다. 기능을 테스트 한 후 Visual Studio를 닫고 `App_Data`의 현재 MDF 및 LDF 파일을 백업 복사본으로 바꿔서 데이터베이스를 복원할 수 있습니다.

## <a name="summary"></a>요약

TableAdapter s 마법사는 자동으로 저장 프로시저를 생성 하지만 이러한 저장 프로시저를 이미 만들었거나 수동으로 또는 다른 도구를 사용 하 여 만들려고 할 수 있는 경우가 있습니다. 이러한 시나리오를 수용할 수 있도록 TableAdapter는 기존 저장 프로시저를 가리키도록 구성할 수도 있습니다. 이 자습서에서는 Visual Studio 환경을 통해 데이터베이스에 저장 프로시저를 수동으로 추가 하는 방법과 TableAdapter의 메서드를 이러한 저장 프로시저에 연결 하는 방법을 살펴보았습니다. 또한 저장 프로시저 내에서 트랜잭션을 시작, 커밋 및 롤백하는 데 사용 되는 T-sql 명령 및 스크립트 패턴을 검토 했습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Geisenow, S ren Jacob Lauritsen 및 Teresa Murphy 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [다음](updating-the-tableadapter-to-use-joins-vb.md)
