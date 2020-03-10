---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-cs
title: 사용자 지정 데이터베이스 기반 사이트 맵 공급자 빌드 (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET 2.0의 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색 합니다. XML 기반 공급자는 많은 소형 및 중간 siz에 적합 합니다.
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 04b7591d-106f-4f05-87e9-d416cb65a8a6
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-cs
msc.type: authoredcontent
ms.openlocfilehash: a3e27b37703b12c9796e8516f0d805aef1fdf8d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78495857"
---
# <a name="building-a-custom-database-driven-site-map-provider-c"></a>사용자 지정 데이터베이스 중심 사이트 맵 공급자 빌드(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_CS.zip) 또는 [PDF 다운로드](building-a-custom-database-driven-site-map-provider-cs/_static/datatutorial62cs1.pdf)

> ASP.NET 2.0의 기본 사이트 맵 공급자는 정적 XML 파일에서 해당 데이터를 검색 합니다. XML 기반 공급자는 중소 규모의 여러 웹 사이트에 적합 하지만 더 큰 규모의 웹 응용 프로그램에는 보다 동적인 사이트 맵이 필요 합니다. 이 자습서에서는 비즈니스 논리 계층에서 데이터를 검색 하는 사용자 지정 사이트 맵 공급자를 빌드하여 데이터베이스에서 데이터를 검색 합니다.

## <a name="introduction"></a>소개

ASP.NET 2.0 s 사이트 맵 기능을 사용 하면 페이지 개발자가 XML 파일 등의 일부 영구 미디어에서 웹 응용 프로그램의 사이트 맵을 정의할 수 있습니다. 일단 정의 되 면 [`System.Web` 네임 스페이스](https://msdn.microsoft.com/library/system.web.aspx) 의 [`SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx) 를 통해 또는 SiteMapPath, Menu 및 TreeView 컨트롤과 같은 다양 한 탐색 웹 컨트롤을 통해 프로그래밍 방식으로 사이트 맵 데이터에 액세스할 수 있습니다. 사이트 맵 시스템은 다른 사이트 맵 serialization 구현을 생성 하 고 웹 응용 프로그램에 연결할 수 있도록 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) 을 사용 합니다. ASP.NET 2.0와 함께 제공 되는 기본 사이트 맵 공급자는 XML 파일에서 사이트 맵 구조를 유지 합니다. [마스터 페이지 및 사이트 탐색](../introduction/master-pages-and-site-navigation-cs.md) 자습서로 돌아가서이 구조를 포함 하 고 각각의 새 자습서 섹션을 사용 하 여 해당 XML을 업데이트 한 `Web.sitemap` 라는 파일을 만들었습니다.

기본 XML 기반 사이트 맵 공급자는 이러한 자습서와 같이 사이트 맵 구조가 매우 정적인 경우 제대로 작동 합니다. 그러나 많은 경우에는 더 동적인 사이트 맵이 필요 합니다. 그림 1에 표시 된 사이트 맵을 고려 합니다. 여기서 각 범주와 제품은 웹 사이트의 구조에 섹션으로 표시 됩니다. 이 사이트 맵을 사용 하면 루트 노드에 해당 하는 웹 페이지를 방문 하면 모든 범주가 나열 될 수 있습니다. 반면 특정 범주에 속한 웹 페이지를 방문 하면 해당 범주의 제품이 표시 되 고 특정 제품의 웹 페이지를 볼 때 해당 제품의 세부 정보가 표시 됩니다.

[사이트 맵 구조를 구성을 범주 및 제품 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image1.png)

**그림 1**: 범주 및 제품이 사이트 맵 구조를 구성을 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image2.png))

이 범주 및 제품 기반 구조는 `Web.sitemap` 파일에 하드 코딩 될 수 있지만, 범주 또는 제품이 추가, 제거 또는 이름이 변경 될 때마다 파일을 업데이트 해야 합니다. 따라서 데이터베이스에서 구조를 검색 하거나 응용 프로그램 아키텍처의 비즈니스 논리 계층에서 이상적으로 사이트 맵 유지 관리를 크게 간소화할 수 있습니다. 이러한 방식으로 제품 및 범주가 추가, 이름 변경 또는 삭제 되 면 사이트 맵은 이러한 변경 내용을 반영 하도록 자동으로 업데이트 됩니다.

ASP.NET 2.0 s 사이트 맵 직렬화는 공급자 모델을 기반으로 하기 때문에 데이터베이스 또는 아키텍처와 같은 대체 데이터 저장소에서 데이터를 가져와 하는 고유한 사용자 지정 사이트 맵 공급자를 만들 수 있습니다. 이 자습서에서는 BLL에서 데이터를 검색 하는 사용자 지정 공급자를 빌드합니다. S를 시작 하겠습니다.

> [!NOTE]
> 이 자습서에서 만든 사용자 지정 사이트 맵 공급자는 응용 프로그램의 아키텍처 및 데이터 모델과 긴밀 하 게 연관 되어 있습니다. [SQL Server에 사이트 맵을 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 하는 Jeff Prosise와 문서 [를 대기 하는 SQL 사이트 맵 공급자는](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) SQL Server에서 사이트 맵 데이터를 저장 하는 일반화 된 방법을 검토 합니다.

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>1 단계: 사용자 지정 사이트 맵 공급자 웹 페이지 만들기

사용자 지정 사이트 맵 공급자 만들기를 시작 하기 전에 먼저이 자습서에 필요한 ASP.NET 페이지를 추가 해 보겠습니다. `SiteMapProvider`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

또한 `App_Code` 폴더에 `CustomProviders` 하위 폴더를 추가 합니다.

![사이트 맵 공급자 관련 자습서에 대 한 ASP.NET 페이지 추가](building-a-custom-database-driven-site-map-provider-cs/_static/image2.gif)

**그림 2**: 사이트 맵 공급자 관련 자습서에 대 한 ASP.NET 페이지 추가

이 섹션에 대 한 자습서는 하나만 있으므로 s 자습서를 나열 하는 `Default.aspx` 필요 하지 않습니다. 대신 `Default.aspx` GridView 컨트롤에 범주가 표시 됩니다. 이에 대해서는 2 단계에서 살펴보겠습니다.

다음에는 `Default.aspx` 페이지에 대 한 참조를 포함 하도록 `Web.sitemap`를 업데이트 합니다. 특히 캐싱 `<siteMapNode>`후에 다음 태그를 추가 합니다.

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 유일한 사이트 맵 공급자 자습서에 대 한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 사이트 맵 공급자 자습서에 대 한 항목이 포함 되어 있습니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image3.gif)

**그림 3**: 사이트 맵에 사이트 맵 공급자 자습서에 대 한 항목이 포함 되어 있습니다.

이 자습서에서는 사용자 지정 사이트 맵 공급자를 만들고 해당 공급자를 사용 하도록 웹 응용 프로그램을 구성 하는 방법을 보여 줍니다. 특히 그림 1에 나와 있는 것 처럼 각 범주 및 제품에 대 한 노드와 함께 루트 노드를 포함 하는 사이트 맵을 반환 하는 공급자를 빌드합니다. 일반적으로 사이트 맵의 각 노드는 URL을 지정할 수 있습니다. 사이트 맵의 경우 루트 노드 URL은 `~/SiteMapProvider/Default.aspx`되며 데이터베이스의 모든 범주가 나열 됩니다. 사이트 맵의 각 범주 노드에는 지정 된 *categoryID*의 모든 제품을 나열 하는 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`를 가리키는 URL이 있습니다. 마지막으로, 각 제품 사이트 맵 노드는 특정 제품의 세부 정보를 표시 하는 `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`을 가리킵니다.

시작 하려면 `Default.aspx`, `ProductsByCategory.aspx`및 `ProductDetails.aspx` 페이지를 만들어야 합니다. 이러한 페이지는 각각 2, 3 및 4 단계에서 완료 됩니다. 이 자습서의 위한 것는 사이트 맵 공급자에 포함 되어 있으며, 이전 자습서에서는 이러한 종류의 다중 페이지 마스터/세부 보고서를 만들기 때문에 2 ~ 4 단계를 진행 합니다. 여러 페이지에 걸쳐 있는 마스터/세부 보고서를 만드는 데 리프레셔가 필요한 경우 [두 페이지의 마스터/세부 정보 필터링](../masterdetail/master-detail-filtering-across-two-pages-cs.md) 자습서를 다시 참조 하세요.

## <a name="step-2-displaying-a-list-of-categories"></a>2 단계: 범주 목록 표시

`SiteMapProvider` 폴더에서 `Default.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 `ID`를 `Categories`로 설정 합니다. GridView의 스마트 태그에서 `CategoriesDataSource` 라는 새 ObjectDataSource에 바인딩하고 `CategoriesBLL` 클래스 s `GetCategories` 메서드를 사용 하 여 데이터를 검색 하도록 구성 합니다. 이 GridView는 범주를 표시 하기만 하 고 데이터 수정 기능을 제공 하지 않으므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.

[GetCategories 메서드를 사용 하 여 범주를 반환 하도록 ObjectDataSource를 구성 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image3.png)

**그림 4**: `GetCategories` 메서드를 사용 하 여 범주를 반환 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image4.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image5.png)

**그림 5**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image6.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서는 `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`및 `BrochurePath`에 대 한 BoundField를 추가 합니다. `CategoryName` 및 `Description` BoundFields 포함 하 고 `CategoryName` BoundField s `HeaderText` 속성을 Category로 업데이트 하도록 GridView를 편집 합니다.

다음으로, 하이퍼링크 필드를 추가 하 고 맨 왼쪽 필드에 배치 합니다. `DataNavigateUrlFields` 속성을 `CategoryID`로 설정 하 고 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`로 설정 합니다. 제품을 보려면 `Text` 속성을 설정 합니다.

![범주 GridView에 하이퍼링크 필드 추가](building-a-custom-database-driven-site-map-provider-cs/_static/image6.gif)

**그림 6**: `Categories` GridView에 하이퍼링크 필드 추가

ObjectDataSource를 만들고 GridView 필드를 사용자 지정한 후에 두 가지 컨트롤 선언 태그는 다음과 같습니다.

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample2.aspx)]

그림 7에는 브라우저를 통해 볼 때 `Default.aspx` 표시 됩니다. 범주 s 제품 보기 링크를 클릭 하면 3 단계에서 빌드할 `ProductsByCategory.aspx?CategoryID=categoryID`으로 이동 됩니다.

[각 범주가 제품 보기 링크와 함께 나열 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image7.png)

**그림 7**: 각 범주가 제품 보기 링크와 함께 나열 됨 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image8.png))

## <a name="step-3-listing-the-selected-category-s-products"></a>3 단계: 선택한 범주 제품 나열

`ProductsByCategory.aspx` 페이지를 열고 GridView를 추가 하 여 `ProductsByCategory`이름을 지정 합니다. 해당 스마트 태그에서 GridView를 `ProductsByCategoryDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsBLL` 클래스 s `GetProductsByCategoryID(categoryID)` 메서드를 사용 하도록 ObjectDataSource를 구성 하 고 업데이트, 삽입 및 삭제 탭에서 드롭다운 목록을 (없음)으로 설정 합니다.

[ProductsBLL 클래스 s GetProductsByCategoryID (categoryID) 메서드를 사용 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image9.png)

**그림 8**: `ProductsBLL` 클래스의 `GetProductsByCategoryID(categoryID)` 메서드 사용 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image10.png))

데이터 원본 구성 마법사의 마지막 단계에서는 *categoryID*의 매개 변수 원본을 확인 하는 메시지를 표시 합니다. 이 정보는 querystring 필드 `CategoryID`를 통해 전달 되므로 그림 9에 표시 된 것 처럼 드롭다운 목록에서 QueryString을 선택 하 고 QueryStringField 텍스트 상자에 CategoryID를 입력 합니다. 마침을 클릭하여 마법사를 완료합니다.

[categoryID 매개 변수에 대 한 CategoryID Querystring 필드를 사용 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image11.png)

**그림 9**: *categoryID* 매개 변수에 대 한 `CategoryID` Querystring 필드 사용 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image12.png))

마법사를 완료 한 후 Visual Studio에서 해당 BoundFields 및 CheckBoxField를 product 데이터 필드에 대 한 GridView에 추가 합니다. `ProductName`, `UnitPrice`및 `SupplierName` BoundFields를 제외한 모든을 제거 합니다. 이러한 세 가지 BoundFields `HeaderText` 속성을 사용자 지정 하 여 제품, 가격 및 공급자를 각각 읽습니다. `UnitPrice` BoundField를 통화로 지정 합니다.

다음으로, 하이퍼링크 필드를 추가 하 고 맨 왼쪽 위치로 이동 합니다. 세부 정보를 보려면 해당 `Text` 속성을 설정 하 고 `DataNavigateUrlFields` 속성을 `ProductID`로 설정 하 고 `DataNavigateUrlFormatString` 속성을 `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`로 설정 합니다.

![제품 세부 정보 .aspx를 가리키는 세부 정보 보기 하이퍼링크 필드를 추가 합니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image10.gif)

**그림 10**: `ProductDetails.aspx`를 가리키는 정보 보기 하이퍼링크 필드 추가

이러한 사용자 지정을 수행한 후 GridView와 ObjectDataSource의 선언 태그는 다음과 유사 합니다.

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample3.aspx)]

브라우저를 통해 `Default.aspx` 보기로 돌아가서 음료에 대 한 제품 보기 링크를 클릭 합니다. 그러면 `ProductsByCategory.aspx?CategoryID=1`로 이동 하 여 음료 범주에 속한 Northwind 데이터베이스의 제품에 대 한 이름, 가격 및 공급 업체를 표시 합니다 (그림 11 참조). 사용자를 범주 목록 페이지 (`Default.aspx`)로 반환 하 고 선택한 범주 이름과 설명을 표시 하는 DetailsView 또는 FormView 컨트롤로 사용자를 반환 하는 링크를 포함 하도록이 페이지를 더욱 향상 시킬 수 있습니다.

[음료 이름, 가격 및 공급자가 표시 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image13.png)

**그림 11**: 음료 이름, 가격 및 공급 업체 표시 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image14.png))

## <a name="step-4-showing-a-product-s-details"></a>4 단계: 제품 정보 표시

최종 페이지인 `ProductDetails.aspx`에서 선택한 제품 세부 정보를 표시 합니다. `ProductDetails.aspx`를 열고 DetailsView를 도구 상자에서 디자이너로 끌어 옵니다. DetailsView s `ID` 속성을 `ProductInfo` 설정 하 고 `Height` 및 `Width` 속성 값을 지웁니다. 해당 스마트 태그에서 DetailsView을 `ProductDataSource`라는 새 ObjectDataSource에 바인딩하고 `ProductsBLL` 클래스의 `GetProductByProductID(productID)` 메서드에서 해당 데이터를 가져오도록 ObjectDataSource를 구성 합니다. 2 단계와 3 단계에서 만든 이전 웹 페이지와 마찬가지로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 합니다.

[Getproductid Byproductid (productID) 메서드를 사용 하도록 ObjectDataSource를 구성 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image15.png)

**그림 12**: `GetProductByProductID(productID)` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image16.png))

데이터 원본 구성 마법사의 마지막 단계에서는 *productID* 매개 변수의 원본을 확인 하는 메시지를 표시 합니다. 이 데이터는 querystring 필드 `ProductID`를 통해 제공 되므로 드롭다운 목록을 QueryString으로 설정 하 고 QueryStringField textbox를 ProductID로 설정 합니다. 마지막으로 마침 단추를 클릭 하 여 마법사를 완료 합니다.

[productid 매개 변수를 구성 하 ![ProductID Querystring 필드에서 해당 값을 가져옵니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image17.png)

**그림 13**: *productID* 매개 변수가 `ProductID` Querystring 필드에서 해당 값을 가져오도록 구성 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image18.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio에서 product 데이터 필드에 대 한 DetailsView에 해당 BoundFields 및 CheckBoxField를 만듭니다. `ProductID`, `SupplierID`및 `CategoryID` BoundFields를 제거 하 고 나머지 필드를 적절히 구성 합니다. 몇 가지 미적 구성 후에는 DetailsView 및 ObjectDataSource s 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample4.aspx)]

이 페이지를 테스트 하려면 `Default.aspx`로 돌아가서 음료 범주에 대 한 제품 보기를 클릭 합니다. 음료 제품 목록에서 Chai Tea에 대 한 세부 정보 보기 링크를 클릭 합니다. 그러면 Chai Tea s 세부 정보를 표시 하는 `ProductDetails.aspx?ProductID=1`으로 이동 합니다 (그림 14 참조).

[![Chai Tea s 공급자, 범주, 가격 및 기타 정보가 표시 됩니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image19.png)

**그림 14**: Chai Tea s 공급자, 범주, 가격 및 기타 정보가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image20.png)).

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>5 단계: 사이트 맵 공급자의 내부 작업 이해

사이트 맵은 계층을 형성 하는 `SiteMapNode` 인스턴스의 컬렉션으로 웹 서버 메모리에 표시 됩니다. 루트 노드는 하나만 있어야 하 고 모든 루트 노드는 정확히 하나의 부모 노드를 포함 해야 하며 모든 노드에는 임의 개수의 자식이 있을 수 있습니다. 각 `SiteMapNode` 개체는 웹 사이트 구조에 있는 섹션을 나타냅니다. 이러한 섹션에는 일반적으로 해당 웹 페이지가 있습니다. 따라서 [`SiteMapNode` 클래스](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 에는 `SiteMapNode`가 나타내는 섹션에 대 한 정보를 제공 하는 `Title`, `Url`및 `Description`과 같은 속성이 있습니다. 계층의 각 `SiteMapNode`를 고유 하 게 식별 하는 `Key` 속성 뿐만 아니라 `ChildNodes`, `ParentNode`, `NextSibling`, `PreviousSibling`등을 설정 하는 데 사용 되는 속성도 있습니다.

그림 15에서는 그림 1의 일반적인 사이트 맵 구조를 보여 주지만 구현 세부 정보는 보다 자세히 설명 되어 있습니다.

[![각 SiteMapNode에는 제목, Url, 키 등의 속성이 있습니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image15.gif)

**그림 15**: 각 `SiteMapNode`에 `Title`, `Url`, `Key`등의 속성이 있는 경우 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image17.gif))

사이트 맵은 [`System.Web` 네임 스페이스](https://msdn.microsoft.com/library/system.web.aspx)의 [`SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx) 를 통해 액세스할 수 있습니다. 이 클래스 `RootNode` 속성은 사이트 맵 루트 `SiteMapNode` 인스턴스를 반환 합니다. `CurrentNode`는 `Url` 속성이 현재 요청 된 페이지의 URL과 일치 하는 `SiteMapNode` 반환 합니다. 이 클래스는 ASP.NET 2.0 s 탐색 웹 컨트롤에서 내부적으로 사용 됩니다.

`SiteMap` 클래스 s 속성에 액세스 하는 경우 일부 영구 미디어에서 메모리로 사이트 맵 구조를 직렬화 해야 합니다. 그러나 사이트 맵 serialization 논리는 `SiteMap` 클래스로 하드 코딩 되지 않습니다. 대신 런타임에 `SiteMap` 클래스가 serialization에 사용할 사이트 맵 *공급자* 를 결정 합니다. 기본적으로 [`XmlSiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx) 는 올바른 형식의 XML 파일에서 사이트 맵 s 구조를 읽는 데 사용 됩니다. 그러나 약간의 작업을 통해 사용자 지정 사이트 맵 공급자를 만들 수 있습니다.

모든 사이트 맵 공급자는 사이트 맵 공급자에 필요한 필수 메서드 및 속성을 포함 하는 [`SiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx)에서 파생 되어야 하지만 대부분의 구현 세부 정보는 생략 됩니다. 두 번째 클래스 [`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx)는 `SiteMapProvider` 클래스를 확장 하 고 필요한 기능의 보다 강력한 구현을 포함 합니다. 내부적으로 `StaticSiteMapProvider`는 사이트 맵의 `SiteMapNode` 인스턴스를 `Hashtable`에 저장 하 고 `RemoveNode(siteMapNode),`를 내부 `Clear()`에 추가 하 고 제거 하는 `AddNode(child, parent)`, `SiteMapNode`, `Hashtable`등의 메서드를 제공 합니다. `XmlSiteMapProvider`는 `StaticSiteMapProvider`에서 파생됩니다.

`StaticSiteMapProvider`를 확장 하는 사용자 지정 사이트 맵 공급자를 만들 때 재정의 해야 하는 두 가지 추상 메서드 [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx) 및 [`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx)있습니다. 이름에서 알 수 있듯이 `BuildSiteMap`은 영구 저장소에서 사이트 맵 구조를 로드 하 고 메모리에 생성 하는 일을 담당 합니다. `GetRootNodeCore`는 사이트 맵의 루트 노드를 반환 합니다.

웹 응용 프로그램에서 사이트 맵 공급자를 사용 하려면 먼저 응용 프로그램의 구성에 등록 해야 합니다. 기본적으로 `XmlSiteMapProvider` 클래스는 `AspNetXmlSiteMapProvider`이름을 사용 하 여 등록 됩니다. 추가 사이트 맵 공급자를 등록 하려면 `Web.config`에 다음 태그를 추가 합니다.

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample5.xml)]

*이름* 값은 사용자가 읽을 수 있는 이름을 공급자에 게 할당 하는 반면 *형식은* 사이트 맵 공급자의 정규화 된 형식 이름을 지정 합니다. 사용자 지정 사이트 맵 공급자를 만든 후 7 단계에서 *이름* 및 *형식* 값에 대 한 구체적인 값을 살펴보겠습니다.

사이트 맵 공급자 클래스는 `SiteMap` 클래스에서 처음 액세스할 때 인스턴스화되고 웹 응용 프로그램의 수명 동안 메모리에 남아 있습니다. 여러 동시 웹 사이트 방문자가 호출할 수 있는 사이트 맵 공급자의 인스턴스는 하나 뿐 이므로 공급자의 메서드는 *스레드로부터 안전*하 게 보호 되어야 합니다.

성능 및 확장성을 위해 메모리 내 사이트 맵 구조를 캐시 하 고 `BuildSiteMap` 메서드가 호출 될 때마다 다시 만드는 대신 캐시 된 구조체를 반환 하는 것이 중요 합니다. 페이지에서 사용 중인 탐색 컨트롤과 사이트 맵 구조의 깊이에 따라 사용자별로 페이지 요청당 여러 번 호출 될 수 `BuildSiteMap`. 어떤 경우 든 `BuildSiteMap`에서 사이트 맵 구조를 캐시 하지 않을 경우이를 호출할 때마다 아키텍처에서 제품 및 범주 정보를 다시 검색 해야 합니다 (데이터베이스에 대 한 쿼리가 발생 함). 이전 캐싱 자습서에서 설명한 바와 같이 캐시 된 데이터는 부실 해질 수 있습니다. 이를 위해 시간 또는 SQL 캐시 종속성 기반 expiries를 사용할 수 있습니다.

> [!NOTE]
> 사이트 맵 공급자는 선택적으로 [`Initialize` 메서드](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx)를 재정의할 수 있습니다. `Initialize`는 사이트 맵 공급자가 처음 인스턴스화될 때 호출 되며, `<add name="name" type="type" customAttribute="value" />`같은 `<add>` 요소의 `Web.config`에서 공급자에 할당 된 사용자 지정 특성을 전달 합니다. 페이지 개발자가 공급자 코드를 수정 하지 않고도 다양 한 사이트 맵 공급자 관련 설정을 지정할 수 있도록 하려는 경우에 유용 합니다. 예를 들어 아키텍처를 통하지 않고 데이터베이스에서 직접 범주 및 제품 데이터를 읽는 경우 페이지 개발자가 공급자 코드에서 하드 코딩 된 값을 사용 하는 대신 `Web.config`를 통해 데이터베이스 연결 문자열을 지정할 수 있습니다. 6 단계에서 빌드할 사용자 지정 사이트 맵 공급자는이 `Initialize` 메서드를 재정의 하지 않습니다. `Initialize` 방법을 사용 하는 예제는 SQL Server 문서에서 [Jeff Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s [저장 사이트 맵](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) 을 참조 하세요.

## <a name="step-6-creating-the-custom-site-map-provider"></a>6 단계: 사용자 지정 사이트 맵 공급자 만들기

Northwind 데이터베이스의 범주 및 제품에서 사이트 맵을 작성 하는 사용자 지정 사이트 맵 공급자를 만들려면 `StaticSiteMapProvider`를 확장 하는 클래스를 만들어야 합니다. 1 단계에서 `App_Code` 폴더에 `CustomProviders` 폴더를 추가 하 라는 메시지가 표시 되 면 `NorthwindSiteMapProvider`라는 폴더에 새 클래스를 추가 합니다. `NorthwindSiteMapProvider` 클래스에 다음 코드를 추가합니다.

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample6.cs)]

[`lock` 문으로](https://msdn.microsoft.com/library/c5kehkcz.aspx)시작 하는이 클래스 `BuildSiteMap` 메서드를 탐색 하는 것으로 시작 하겠습니다. `lock` 문은 한 번에 하나의 스레드만 입력할 수 있도록 하 여 코드에 대 한 액세스를 serialize 하 고 두 개의 동시 스레드가 다른 발가락 한 단계씩 실행 되지 않도록 합니다.

클래스 수준 `SiteMapNode` 변수 `root`는 사이트 맵 구조를 캐시 하는 데 사용 됩니다. 사이트 맵을 처음으로 생성 하거나 기본 데이터가 수정 된 후 처음으로 생성 되는 경우 `root` `null` 되 고 사이트 맵 구조가 생성 됩니다. 다음에이 메서드가 호출 될 때 `root` `null`되지 않도록 생성 프로세스 중에 사이트 맵 루트 노드가 `root`에 할당 됩니다. 따라서 `root` `null` 되지 않은 한, 사이트 맵 구조는 다시 만들 필요 없이 호출자에 게 반환 됩니다.

Root가 `null`되 면 제품 및 범주 정보에서 사이트 맵 구조가 생성 됩니다. 사이트 맵은 `SiteMapNode` 인스턴스를 만든 다음 `StaticSiteMapProvider` 클래스 s `AddNode` 메서드를 호출 하 여 계층 구조를 구성 하는 방식으로 작성 됩니다. `AddNode`는 내부 장부를 수행 하 여 `Hashtable`에 다양 한 `SiteMapNode` 인스턴스를 저장 합니다. 계층 구조 생성을 시작 하기 전에 `Clear` 메서드를 호출 하 여 시작 합니다. 그러면 내부 `Hashtable`에서 요소가 지워집니다. 그런 다음 `ProductsBLL` 클래스 s `GetProducts` 메서드와 결과 `ProductsDataTable`는 지역 변수에 저장 됩니다.

루트 노드를 만들고 `root`에 할당 하 여 사이트 맵 생성을 시작 합니다. 이 `BuildSiteMap` 전체에서 사용 되는 [`SiteMapNode` s 생성자](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx) 의 오버 로드는 다음 정보를 전달 합니다.

- 사이트 맵 공급자 (`this`)에 대 한 참조입니다.
- `SiteMapNode` s `Key`입니다. 이 필수 값은 각 `SiteMapNode`에 대해 고유 해야 합니다.
- `SiteMapNode` s `Url`입니다. `Url`는 선택 사항 이지만, 제공 되는 경우 각 `SiteMapNode` s `Url` 값은 고유 해야 합니다.
- 필요한 `SiteMapNode` s `Title`입니다.

`AddNode(root)` 메서드 호출은 `SiteMapNode` `root`를 사이트 맵에 루트로 추가 합니다. 그런 다음 `ProductsDataTable`의 각 `ProductRow`를 열거 합니다. 현재 제품 범주에 대 한 `SiteMapNode` 이미 있는 경우이를 참조 합니다. 그렇지 않으면 범주에 대 한 새 `SiteMapNode` 생성 되어 `AddNode(categoryNode, root)` 메서드 호출을 통해 `SiteMapNode``root`의 자식으로 추가 됩니다. 적절 한 범주 `SiteMapNode` 노드를 찾거나 만든 후에는 현재 제품에 대 한 `SiteMapNode` 만들어지고 `AddNode(productNode, categoryNode)`를 통해 `SiteMapNode` 범주의 자식으로 추가 됩니다. Product `SiteMapNode` s `Url` 속성이 `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`할당 된 동안에는 범주 `SiteMapNode` s `Url` 속성 값이 `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID` 됩니다.

> [!NOTE]
> `CategoryID`에 대 한 데이터베이스 `NULL` 값이 있는 제품은 `Title` 속성을 None으로 설정 하 고 `Url` 속성이 빈 문자열로 설정 되어 있는 범주 `SiteMapNode`으로 그룹화 됩니다. `ProductBLL` 클래스 s `GetProductsByCategory(categoryID)` 메서드에 현재 `NULL` `CategoryID` 값을 가진 제품만 반환 하는 기능이 없기 때문에 `Url`를 빈 문자열로 설정 하기로 결정 했습니다. 또한 탐색 컨트롤이 `Url` 속성에 대 한 값이 없는 `SiteMapNode`를 렌더링 하는 방법을 보여 주려고 합니다. 이 자습서를 확장 하는 것이 좋습니다 `SiteMapNode` s `Url` 속성이 `ProductsByCategory.aspx`를 가리키도록 하지만 `NULL` `CategoryID` 값이 있는 제품만 표시 되도록 합니다.

사이트 맵을 생성 한 후에는 `Categories`에 대 한 SQL 캐시 종속성을 사용 하 여 데이터 캐시에 임의의 개체를 추가 하 고 `AggregateCacheDependency` 개체를 통해 테이블을 `Products` 합니다. 이전 자습서에서 sql 캐시 종속성을 사용 하 *여 sql 캐시*종속성을 사용 하는 방법을 살펴보았습니다. 그러나 사용자 지정 사이트 맵 공급자는 아직 탐색 하기 위해 사용 하는 데이터 캐시 `Insert` 메서드의 오버 로드를 사용 합니다. 이 오버 로드는 캐시에서 개체가 제거 될 때 호출 되는 대리자를 최종 입력 매개 변수로 받아들입니다. 특히 `NorthwindSiteMapProvider` 클래스에서 아래로 정의 된 `OnSiteMapChanged` 메서드를 가리키는 새 [`CacheItemRemovedCallback` 대리자](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx) 를 전달 합니다.

> [!NOTE]
> 사이트 맵의 메모리 내 표현은 `root`클래스 수준 변수를 통해 캐시 됩니다. 사용자 지정 사이트 맵 공급자 클래스의 인스턴스가 하나 뿐이 고 해당 인스턴스가 웹 응용 프로그램의 모든 스레드 간에 공유 되므로이 클래스 변수는 캐시 역할을 합니다. `BuildSiteMap` 메서드는 데이터 캐시도 사용 하지만 `Categories` 또는 `Products` 테이블의 기본 데이터베이스 데이터가 변경 될 때 알림을 수신 하는 수단 으로만 사용 됩니다. 데이터 캐시에 저장 되는 값은 현재 날짜 및 시간입니다. 실제 사이트 맵 데이터는 데이터 캐시에 저장 *되지 않습니다* .

`BuildSiteMap` 메서드는 사이트 맵의 루트 노드를 반환 하 여 완료 됩니다.

나머지 방법은 매우 간단 합니다. `GetRootNodeCore`은 루트 노드를 반환 합니다. `BuildSiteMap` 루트를 반환 하므로 `GetRootNodeCore`는 단순히 `BuildSiteMap` s 반환 값을 반환 합니다. `OnSiteMapChanged` 메서드는 캐시 항목이 제거 될 때 `root`를 `null`으로 다시 설정 합니다. Root를 `null`으로 다시 설정 하면 다음에 `BuildSiteMap`를 호출할 때 사이트 맵 구조가 다시 작성 됩니다. 마지막으로 `CachedDate` 속성은 데이터 캐시에 저장 된 날짜 및 시간 값을 반환 합니다 (해당 값이 있는 경우). 이 속성은 페이지 개발자가 사이트 맵 데이터가 마지막으로 캐시 된 시기를 확인 하는 데 사용할 수 있습니다.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>7 단계:`NorthwindSiteMapProvider` 등록

웹 응용 프로그램에서 6 단계에서 만든 `NorthwindSiteMapProvider` 사이트 맵 공급자를 사용 하기 위해 `Web.config`의 `<siteMap>` 섹션에 등록 해야 합니다. 특히 `Web.config`의 `<system.web>` 요소 내에 다음 태그를 추가 합니다.

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample7.xml)]

이 태그는 다음 두 가지 작업을 수행 합니다. 첫 번째는 기본 제공 `AspNetXmlSiteMapProvider` 기본 사이트 맵 공급자 임을 나타냅니다. 그런 다음, 6 단계에서 만든 사용자 지정 사이트 맵 공급자를 사용자에 게 친숙 한 이름 Northwind로 등록 합니다.

> [!NOTE]
> 응용 프로그램의 `App_Code` 폴더에 있는 사이트 맵 공급자의 경우 `type` 특성의 값은 단순히 클래스 이름입니다. 또는 컴파일된 어셈블리가 웹 응용 프로그램의 `/Bin` 디렉터리에 배치 된 별도의 클래스 라이브러리 프로젝트에서 사용자 지정 사이트 맵 공급자를 만들었을 수도 있습니다. 이 경우 `type` 특성 값은 *네임 스페이스*입니다. *ClassName*, *AssemblyName*

`Web.config`를 업데이트 한 후 브라우저에서 자습서의 모든 페이지를 잠시 기다려 주십시오. 왼쪽의 탐색 인터페이스는 `Web.sitemap`에 정의 된 섹션과 자습서를 계속 표시 합니다. 이는 `AspNetXmlSiteMapProvider` 기본 공급자로 남아 있기 때문입니다. `NorthwindSiteMapProvider`사용 하는 탐색 사용자 인터페이스 요소를 만들기 위해 Northwind 사이트 맵 공급자를 사용 하도록 명시적으로 지정 해야 합니다. 8 단계에서이를 수행 하는 방법을 알아봅니다.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>8 단계: 사용자 지정 사이트 맵 공급자를 사용 하 여 사이트 맵 정보 표시

`Web.config`에서 만들고 등록 한 사용자 지정 사이트 맵 공급자를 사용 하 여 `SiteMapProvider` 폴더의 `Default.aspx`, `ProductsByCategory.aspx`및 `ProductDetails.aspx` 페이지에 탐색 컨트롤을 추가할 수 있습니다. `Default.aspx` 페이지를 열고 도구 상자에서 디자이너로 `SiteMapPath`을 끌어 옵니다. SiteMapPath 컨트롤은 도구 상자의 탐색 섹션에 있습니다.

[Default.aspx에 SiteMapPath을 추가 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image18.gif)

**그림 16**: `Default.aspx`에 SiteMapPath 추가 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image20.gif))

SiteMapPath 컨트롤은 사이트 맵 내의 현재 페이지 위치를 나타내는 이동 경로를 표시 합니다. 마스터 페이지 *및 사이트 탐색* 자습서에서 마스터 페이지 맨 위에 SiteMapPath을 추가 했습니다.

잠시 시간을 사용 하 여 브라우저를 통해이 페이지를 봅니다. 그림 16에서 추가 된 SiteMapPath은 기본 사이트 맵 공급자를 사용 하 여 `Web.sitemap`에서 데이터를 끌어옵니다. 따라서 breadcrumb은 오른쪽 위 모서리의 이동 경로와 마찬가지로 사이트 맵을 사용자 지정 하는 홈 &gt; 표시 합니다.

[이동 경로가 기본 사이트 맵 공급자를 사용 ![](building-a-custom-database-driven-site-map-provider-cs/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image21.gif)

**그림 17**: Breadcrumb이 기본 사이트 맵 공급자를 사용 합니다 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image23.gif)).

그림 16에서 SiteMapPath을 추가 하려면 6 단계에서 만든 사용자 지정 사이트 맵 공급자를 사용 하 고 [`SiteMapProvider` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) 을 Northwind로 설정 합니다 .이는 `Web.config`의 `NorthwindSiteMapProvider`에 할당 된 이름입니다. 아쉽게도 디자이너는 계속 해 서 기본 사이트 맵 공급자를 사용 하지만이 속성을 변경한 후 브라우저를 통해 페이지를 방문 하면 이동 경로가 이제 사용자 지정 사이트 맵 공급자를 사용 하는 것을 볼 수 있습니다.

[![이동 경로가 이제 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider를 사용 합니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image24.gif)

**그림 18**: 이제 이동 경로에서 사용자 지정 사이트 맵 공급자 `NorthwindSiteMapProvider` 사용 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image26.gif))

SiteMapPath 컨트롤은 `ProductsByCategory.aspx` 및 `ProductDetails.aspx` 페이지에서 더 많은 기능을 갖춘 사용자 인터페이스를 표시 합니다. 이러한 페이지에 SiteMapPath을 추가 하 여 Northwind에 대 한 `SiteMapProvider` 속성을 설정 합니다. `Default.aspx`에서 음료에 대 한 제품 보기 링크를 클릭 한 다음 Chai Tea에 대 한 세부 정보 보기 링크를 클릭 합니다. 그림 19와 같이 이동 경로에는 현재 사이트 맵 섹션 (Chai Tea) 및 해당 상위: 음료와 모든 범주가 포함 되어 있습니다.

[![이동 경로가 이제 사용자 지정 사이트 맵 공급자 NorthwindSiteMapProvider를 사용 합니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image21.png)

**그림 19**: 이제 이동 경로에서 사용자 지정 사이트 맵 공급자 `NorthwindSiteMapProvider` 사용 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image22.png))

메뉴 및 TreeView 컨트롤과 같이 SiteMapPath 외에 다른 탐색 사용자 인터페이스 요소를 사용할 수 있습니다. 이 자습서에 대 한 다운로드의 `Default.aspx`, `ProductsByCategory.aspx`및 `ProductDetails.aspx` 페이지 (예: 모든 포함 메뉴 컨트롤) (그림 20 참조). ASP.NET 2.0의 탐색 컨트롤 및 사이트 맵 시스템에 대 한 자세한 내용은 [ASP.NET 2.0 s 사이트 탐색 기능](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) 및 [ASP.NET 2.0 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/) 의 [사이트 탐색 컨트롤 사용](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) 섹션을 참조 하세요.

[메뉴 컨트롤 ![각 범주와 제품을 나열 합니다.](building-a-custom-database-driven-site-map-provider-cs/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-cs/_static/image28.gif)

**그림 20**: 메뉴 컨트롤은 각 범주 및 제품을 나열 합니다 ([전체 크기 이미지를 보려면 클릭](building-a-custom-database-driven-site-map-provider-cs/_static/image30.gif)).

이 자습서의 앞부분에서 설명한 것 처럼 `SiteMap` 클래스를 통해 프로그래밍 방식으로 사이트 맵 구조에 액세스할 수 있습니다. 다음 코드는 기본 공급자의 루트 `SiteMapNode`를 반환 합니다.

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample8.cs)]

`AspNetXmlSiteMapProvider`는 응용 프로그램의 기본 공급자 이므로 위의 코드는 `Web.sitemap`에 정의 된 루트 노드를 반환 합니다. 기본값이 아닌 사이트 맵 공급자를 참조 하려면 다음과 같이 `SiteMap` 클래스 [`Providers` 속성](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx) 을 사용 합니다.

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample9.cs)]

여기서 *name* 은 웹 응용 프로그램에 대 한 Northwind 사용자 지정 사이트 맵 공급자의 이름입니다.

사이트 맵 공급자에 해당 하는 멤버에 액세스 하려면 `SiteMap.Providers["name"]`를 사용 하 여 공급자 인스턴스를 검색 한 다음 적절 한 형식으로 캐스팅 합니다. 예를 들어, ASP.NET 페이지에 `NorthwindSiteMapProvider` s `CachedDate` 속성을 표시 하려면 다음 코드를 사용 합니다.

[!code-csharp[Main](building-a-custom-database-driven-site-map-provider-cs/samples/sample10.cs)]

> [!NOTE]
> SQL 캐시 종속성 기능을 테스트 해야 합니다. `Default.aspx`, `ProductsByCategory.aspx`및 `ProductDetails.aspx` 페이지를 방문한 후 편집, 삽입 및 삭제 섹션의 자습서 중 하나로 이동 하 여 범주 또는 제품의 이름을 편집 합니다. 그런 다음 `SiteMapProvider` 폴더에 있는 페이지 중 하나로 돌아갑니다. 기본 데이터베이스에 대 한 변경 내용을 확인 하기 위해 폴링 메커니즘에 충분 한 시간이 경과 되었다고 가정할 경우 새 제품 또는 범주 이름을 표시 하도록 사이트 맵을 업데이트 해야 합니다.

## <a name="summary"></a>요약

ASP.NET 2.0 s 사이트 맵 기능에는 `SiteMap` 클래스, 다양 한 기본 제공 탐색 웹 컨트롤 및 XML 파일에 유지 되는 사이트 맵 정보를 필요로 하는 기본 사이트 맵 공급자가 포함 되어 있습니다. 데이터베이스, 응용 프로그램 아키텍처 또는 원격 웹 서비스 등의 다른 원본에서 사이트 맵 정보를 사용 하려면 사용자 지정 사이트 맵 공급자를 만들어야 합니다. 여기에는 `SiteMapProvider` 클래스에서 직접 또는 간접적으로 파생 되는 클래스를 만드는 작업이 포함 됩니다.

이 자습서에서는 응용 프로그램 아키텍처에서 제품 및 범주 정보 추출에 대 한 사이트 맵을 기반으로 하는 사용자 지정 사이트 맵 공급자를 만드는 방법에 대해 살펴보았습니다. 공급자는 `StaticSiteMapProvider` 클래스를 확장 하 고, 데이터를 검색 하 고, 사이트 맵 계층 구조를 생성 하 고, 결과 구조를 클래스 수준 변수에 캐시 하는 `BuildSiteMap` 메서드를 수반. 기본 `Categories` 또는 `Products` 데이터가 수정 될 때 캐시 된 구조를 무효화 하기 위해 콜백 함수와 함께 SQL 캐시 종속성을 사용 했습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- SQL Server 및 [사용자가 기다리는 SQL 사이트 맵 공급자](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) [에 사이트 맵 저장](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/)
- [ASP.NET 2.0 s 공급자 모델 살펴보기](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [공급자 도구 키트](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [ASP.NET 2.0 s 사이트 탐색 기능 검사](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dave Gardner, Zack Jones, Teresa Murphy 및 Bernadette Leigh 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](building-a-custom-database-driven-site-map-provider-vb.md)
