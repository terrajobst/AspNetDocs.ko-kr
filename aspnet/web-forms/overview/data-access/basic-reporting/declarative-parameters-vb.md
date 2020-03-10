---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
title: 선언적 매개 변수 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 하드 코드 된 값으로 설정 된 매개 변수를 사용 하 여 DetailsView 컨트롤에 표시할 데이터를 선택 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: dc1234a3-114f-4c9a-8d25-50ca03cc8e8e
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
msc.type: authoredcontent
ms.openlocfilehash: cdc42752fc78d18366af037a81fe4ebe5a1646ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483131"
---
# <a name="declarative-parameters-vb"></a>선언적 매개 변수(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_5_VB.exe) 또는 [PDF 다운로드](declarative-parameters-vb/_static/datatutorial05vb1.pdf)

> 이 자습서에서는 하드 코드 된 값으로 설정 된 매개 변수를 사용 하 여 DetailsView 컨트롤에 표시할 데이터를 선택 하는 방법을 설명 합니다.

## <a name="introduction"></a>소개

[마지막 자습서](displaying-data-with-the-objectdatasource-vb.md) 에서는 `ProductsBLL` 클래스에서 `GetProducts()` 메서드를 호출한 ObjectDataSource 컨트롤에 바인딩되는 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 데이터를 표시 하는 방법을 살펴보았습니다. `GetProducts()` 메서드는 Northwind 데이터베이스의 `Products` 테이블의 모든 레코드로 채워진 강력한 형식의 DataTable을 반환 합니다. `ProductsBLL` 클래스에는 제품의 하위 집합 (`GetProductByProductID(productID)`, `GetProductsByCategoryID(categoryID)`및 `GetProductsBySupplierID(supplierID)`를 반환 하는 추가 메서드가 포함 되어 있습니다. 이 세 가지 메서드는 반환 된 제품 정보를 필터링 하는 방법을 나타내는 입력 매개 변수를 필요로 합니다.

ObjectDataSource를 사용 하 여 입력 매개 변수가 필요한 메서드를 호출할 수 있지만 이렇게 하려면 이러한 매개 변수의 값을 가져올 위치를 지정 해야 합니다. 매개 변수 값은 하드 코딩 되거나 querystring 값, 세션 변수, 페이지에 있는 웹 컨트롤의 속성 값 등을 비롯 한 다양 한 동적 소스에서 가져올 수 있습니다.

이 자습서에서는 먼저 하드 코드 된 값으로 설정 된 매개 변수를 사용 하는 방법을 보여 줍니다. 구체적으로, 특정 제품에 대 한 정보를 표시 하는 페이지에 DetailsView을 추가 하는 것을 확인할 수 있습니다. 즉, Chef Anton의 Gumbo Mix `ProductID` 5입니다. 다음으로는 웹 컨트롤을 기반으로 매개 변수 값을 설정 하는 방법을 알아봅니다. 특히 텍스트 상자를 사용 하 여 사용자가 국가를 입력할 수 있으며, 그 후에는 단추를 클릭 하 여 해당 국가의 공급자 목록을 볼 수 있습니다.

## <a name="using-a-hard-coded-parameter-value"></a>하드 코드 된 매개 변수 값 사용

첫 번째 예제에서는 `BasicReporting` 폴더의 `DeclarativeParams.aspx` 페이지에 DetailsView 컨트롤을 추가 하는 것부터 시작 합니다. DetailsView의 스마트 태그에서 드롭다운 목록에서 &lt;새 데이터 소스&gt;를 선택 하 고 ObjectDataSource를 추가 하도록 선택 합니다.

[페이지에 ObjectDataSource를 추가 ![](declarative-parameters-vb/_static/image2.png)](declarative-parameters-vb/_static/image1.png)

**그림 1**: 페이지에 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image3.png))

그러면 ObjectDataSource 컨트롤의 데이터 소스 선택 마법사가 자동으로 시작 됩니다. 마법사의 첫 번째 화면에서 `ProductsBLL` 클래스를 선택 합니다.

[ProductsBLL 클래스 ![선택 합니다.](declarative-parameters-vb/_static/image5.png)](declarative-parameters-vb/_static/image4.png)

**그림 2**: `ProductsBLL` 클래스 선택 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image6.png))

특정 제품에 대 한 정보를 표시 하려고 하므로 `GetProductByProductID(productID)` 방법을 사용 하고자 합니다.

[Getproductid Byproductid (productID) 메서드를 선택 ![](declarative-parameters-vb/_static/image8.png)](declarative-parameters-vb/_static/image7.png)

**그림 3**: `GetProductByProductID(productID)` 방법 선택 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image9.png))

선택한 메서드에 매개 변수가 포함 되어 있으므로 마법사의 화면이 하나 더 있습니다. 여기에는 매개 변수에 사용할 값을 정의 하 라는 메시지가 표시 됩니다. 왼쪽의 목록에는 선택한 메서드의 모든 매개 변수가 표시 됩니다. `GetProductByProductID(productID)` `productID`하나만 있습니다. 오른쪽에서 선택한 매개 변수의 값을 지정할 수 있습니다. 매개 변수 원본 드롭다운 목록에는 매개 변수 값에 사용할 수 있는 여러 소스가 나열 됩니다. 하드 코드 된 값 5를 `productID` 매개 변수에 대해 지정 하려고 하므로 매개 변수 원본을 None으로 그대로 두고 DefaultValue 텍스트 상자에 5를 입력 합니다.

[![는 하드 코드 된 매개 변수 값 5가 productID 매개 변수에 사용 됩니다.](declarative-parameters-vb/_static/image11.png)](declarative-parameters-vb/_static/image10.png)

**그림 4**: 하드 코드 된 매개 변수 값 5가 `productID` 매개 변수에 사용 됨 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image12.png))

데이터 소스 구성 마법사를 완료 한 후 ObjectDataSource 컨트롤의 선언적 태그는 `SelectMethod` 속성에 정의 된 메서드에 필요한 각 입력 매개 변수에 대 한 `SelectParameters` 컬렉션에 `Parameter` 개체를 포함 합니다. 이 예제에서 사용 하는 메서드에는 단일 입력 매개 변수 `parameterID`만 필요 하므로 여기에는 항목이 하나만 있습니다. `SelectParameters` 컬렉션은 `System.Web.UI.WebControls` 네임 스페이스의 `Parameter` 클래스에서 파생 되는 모든 클래스를 포함할 수 있습니다. 하드 코드 된 매개 변수 값의 경우 기본 `Parameter` 클래스가 사용 되지만 다른 매개 변수 소스 옵션의 경우 파생 `Parameter` 클래스가 사용 됩니다. 필요한 경우 고유한 [사용자 지정 매개 변수 형식을](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)만들 수도 있습니다.

[!code-aspx[Main](declarative-parameters-vb/samples/sample1.aspx)]

> [!NOTE]
> 사용자 컴퓨터에서 다음을 수행 하는 경우이 시점에 표시 되는 선언 태그에는 `InsertMethod`, `UpdateMethod`및 `DeleteMethod` 속성과 `DeleteParameters`값이 포함 될 수 있습니다. ObjectDataSource의 데이터 소스 선택 마법사는 삽입, 업데이트 및 삭제에 사용할 `ProductBLL`의 메서드를 자동으로 지정 하므로 이러한 메서드를 명시적으로 선택 하지 않으면 위의 태그에 포함 됩니다.

이 페이지를 방문할 때 데이터 웹 컨트롤은 ObjectDataSource의 `Select` 메서드를 호출 합니다 .이 메서드는 `productID` 입력 매개 변수에 대해 하드 코딩 된 값 5를 사용 하 여 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드를 호출 합니다. 이 메서드는 Chef Anton의 Gumbo 조합 (`ProductID` 5 인 제품)에 대 한 정보가 있는 단일 행을 포함 하는 강력한 형식의 `ProductDataTable` 개체를 반환 합니다.

[Chef Anton의 Gumbo 조합에 대 한 ![정보가 표시 됩니다.](declarative-parameters-vb/_static/image14.png)](declarative-parameters-vb/_static/image13.png)

**그림 5**: Chef Anton의 Gumbo 조합에 대 한 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image15.png)).

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>매개 변수 값을 웹 컨트롤의 속성 값으로 설정

페이지의 웹 컨트롤 값에 따라 ObjectDataSource의 매개 변수 값을 설정할 수도 있습니다. 이를 설명 하기 위해 사용자가 지정한 국가에 있는 모든 공급자를 나열 하는 GridView가 있습니다. 이를 수행 하려면 사용자가 국가 이름을 입력할 수 있는 페이지에 TextBox를 추가 합니다. 이 TextBox 컨트롤의 `ID` 속성을 `CountryName`로 설정 합니다. 또한 단추 웹 컨트롤을 추가 합니다.

[ID CountryName를 사용 하 여 페이지에 TextBox를 추가 ![](declarative-parameters-vb/_static/image17.png)](declarative-parameters-vb/_static/image16.png)

**그림 6**: `ID` `CountryName`를 사용 하 여 페이지에 TextBox 추가 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image18.png))

그런 다음 페이지에 GridView를 추가 하 고 스마트 태그에서 새 ObjectDataSource를 추가 하도록 선택 합니다. 공급자 정보를 표시 하려고 하므로 마법사의 첫 화면에서 `SuppliersBLL` 클래스를 선택 합니다. 두 번째 화면에서 `GetSuppliersByCountry(country)` 메서드를 선택 합니다.

[GetSuppliersByCountry (country) 메서드를 선택 ![](declarative-parameters-vb/_static/image20.png)](declarative-parameters-vb/_static/image19.png)

**그림 7**: `GetSuppliersByCountry(country)` 방법 선택 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image21.png))

`GetSuppliersByCountry(country)` 메서드에는 입력 매개 변수가 있으므로 마법사에는 매개 변수 값을 선택 하기 위한 최종 화면이 다시 포함 됩니다. 이번에는 매개 변수 소스를 Control로 설정 합니다. 이렇게 하면 ControlID 드롭다운 목록이 페이지에 있는 컨트롤의 이름으로 채워집니다. 목록에서 `CountryName` 컨트롤을 선택 합니다. 페이지를 처음 방문할 때 `CountryName` 텍스트 상자가 비어 있으므로 결과가 반환 되지 않고 아무것도 표시 되지 않습니다. 기본적으로 일부 결과를 표시 하려면 DefaultValue 텍스트 상자를 적절 하 게 설정 합니다.

[매개 변수 값을 CountryName 컨트롤 값으로 설정 ![](declarative-parameters-vb/_static/image23.png)](declarative-parameters-vb/_static/image22.png)

**그림 8**: 매개 변수 값을 `CountryName` 컨트롤 값으로 설정 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image24.png))

ObjectDataSource의 선언적 태그는 첫 번째 예제와 약간 다르며, 표준 `Parameter` 개체 대신 [Controlparameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) 를 사용 합니다. `ControlParameter`에는 웹 컨트롤의 `ID` 및 매개 변수 (`PropertyName`)에 사용할 속성 값을 지정 하는 추가 속성이 있습니다. 데이터 원본 구성 마법사는 텍스트 상자에서 매개 변수 값으로 `Text` 속성을 사용 하는 것을 확인할 수 있을 정도로 지능적입니다. 그러나 웹 컨트롤에서 다른 속성 값을 사용 하려는 경우에는 여기에서 `PropertyName` 값을 변경 하거나 마법사의 "고급 속성 표시" 링크를 클릭 하 여 변경할 수 있습니다.

[!code-aspx[Main](declarative-parameters-vb/samples/sample2.aspx)]

페이지를 방문할 때 `CountryName` TextBox가 비어 있는 경우 ObjectDataSource의 `Select` 메서드는 GridView에 의해 호출 되지만 `Nothing` 값이 `GetSuppliersByCountry(country)` 메서드에 전달 됩니다. TableAdapter는 `Nothing`을 데이터베이스 `NULL` 값 (`DBNull.Value`)으로 변환 하지만 `GetSuppliersByCountry(country)` 메서드에서 사용 하는 쿼리는 `NULL` 매개 변수에 `@CategoryID` 값이 지정 된 경우 값을 반환 하지 않도록 작성 됩니다. 간단히 말해서 공급자는 반환 되지 않습니다.

그러나 방문자가 국가에 들어가면 표시 되 고 Suppliers 표시 단추를 클릭 하 여 포스트백을 발생 한 후에는 ObjectDataSource의 `Select` 메서드가 다시 열리고 TextBox 컨트롤의 `Text` 값이 `country` 매개 변수로 전달 됩니다.

[캐나다에서 해당 공급 업체 ![표시 됩니다.](declarative-parameters-vb/_static/image26.png)](declarative-parameters-vb/_static/image25.png)

**그림 9**: 캐나다의 이러한 공급 업체 표시 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image27.png))

## <a name="showing-all-suppliers-by-default"></a>기본적으로 모든 공급자 표시

페이지를 처음 볼 때 공급 업체를 모두 표시 하는 대신 먼저 *모든* 공급자를 표시 하 여 사용자가 텍스트 상자에 국가 이름을 입력 하 여 목록을 줄이려면 상당한 수 있습니다. 텍스트 상자가 비어 있으면 `SuppliersBLL` 클래스의 `GetSuppliersByCountry(country)` 메서드가 *`country`* 입력 매개 변수에 대해 `Nothing` 전달 됩니다. 그런 다음이 `Nothing` 값은 DAL의 `GetSupplierByCountry(country)` 메서드로 전달 되며, 다음 쿼리에서 `@Country` 매개 변수에 대 한 데이터베이스 `NULL` 값으로 변환 됩니다.

[!code-sql[Main](declarative-parameters-vb/samples/sample3.sql)]

`Country` 열에 `NULL` 값이 있는 레코드의 경우에도 식 `Country = NULL` 항상 False를 반환 합니다. 따라서 레코드가 반환 되지 않습니다.

Country TextBox가 비어 있을 때 *모든* 공급 업체를 반환 하려면 BLL의 `GetSuppliersByCountry(country)` 메서드를 늘려 country 매개 변수가 `Nothing` 때 `GetSuppliers()` 메서드를 호출 하 고, 그렇지 않은 경우 DAL의 `GetSuppliersByCountry(country)` 메서드를 호출할 수 있습니다. Country가 지정 되지 않은 경우 모든 공급 업체를 반환 하는 것과 country 매개 변수가 포함 된 경우 공급자의 적절 한 하위 집합을 반환 하는 효과가 있습니다.

`SuppliersBLL` 클래스의 `GetSuppliersByCountry(country)` 메서드를 다음과 같이 변경 합니다.

[!code-vb[Main](declarative-parameters-vb/samples/sample4.vb)]

이 변경 내용으로 `DeclarativeParams.aspx` 페이지는 처음 방문할 때 (또는 `CountryName` TextBox가 비어 있을 때마다) 모든 공급 업체를 표시 합니다.

[이제 모든 공급 업체가 기본적으로 표시 ![](declarative-parameters-vb/_static/image29.png)](declarative-parameters-vb/_static/image28.png)

**그림 10**: 이제 모든 공급 업체가 기본적으로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](declarative-parameters-vb/_static/image30.png)).

## <a name="summary"></a>요약

입력 매개 변수를 사용 하 여 메서드를 사용 하려면 ObjectDataSource의 `SelectParameters` 컬렉션에서 매개 변수의 값을 지정 해야 합니다. 다른 형식의 매개 변수를 사용 하면 매개 변수 값을 다른 원본에서 가져올 수 있습니다. 기본 매개 변수 형식은 하드 코드 된 값을 사용 하지만, 코드 줄 없이 쉽게 또는 페이지의 웹 컨트롤에서 사용자가 입력 한 값을 사용 하 여 매개 변수 값을 가져올 수 있습니다.

이 자습서에서 살펴본 예제에서는 선언적 매개 변수 값을 사용 하는 방법을 보여 줍니다. 그러나 현재 날짜 및 시간과 같은 사용할 수 없는 매개 변수 원본을 사용 해야 하는 경우가 있을 수 있습니다. 또는 사이트에서 구성원 자격을 사용 하 고 있는 경우 방문자의 사용자 ID를 사용 해야 합니다. 이러한 시나리오의 경우 ObjectDataSource가 기본 개체의 메서드를 호출 하기 전에 프로그래밍 방식으로 매개 변수 값을 설정할 수 있습니다. [다음 자습서](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)에서이를 수행 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-data-with-the-objectdatasource-vb.md)
> [다음](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)
