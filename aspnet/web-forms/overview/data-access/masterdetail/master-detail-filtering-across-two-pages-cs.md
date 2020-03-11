---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: 두 페이지에 걸쳐 마스터/세부 정보C#필터링 () | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 GridView를 사용 하 여 데이터베이스의 공급자를 나열 하는 방법으로이 패턴을 구현 합니다. GridView의 각 공급자 행에는 뷰가 포함 됩니다.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: ccb3bfa5f215ba6e65b8a10b40041d5c2896c7e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424877"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>두 페이지에 걸쳐 마스터/세부 정보 필터링(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe) 또는 [PDF 다운로드](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> 이 자습서에서는 GridView를 사용 하 여 데이터베이스의 공급자를 나열 하는 방법으로이 패턴을 구현 합니다. GridView의 각 공급자 행에는 클릭 하면 사용자가 선택한 공급자에 대 한 제품을 나열 하는 별도의 페이지로 이동 하는 제품 보기 링크가 포함 됩니다.

## <a name="introduction"></a>소개

이전 두 자습서에서는 Dropdownlist를 사용 하 여 ["마스터" 레코드를 표시 하 고 GridView 또는 DetailsView 컨트롤](master-detail-filtering-with-two-dropdownlists-cs.md) 을 사용 하 여 "세부 정보"를 표시 하는 [단일 웹 페이지에서 마스터/세부 보고서를 표시](master-detail-filtering-with-a-dropdownlist-cs.md) 하는 방법을 살펴보았습니다. 마스터/세부 정보 보고서에 사용 되는 또 다른 일반적인 패턴은 한 웹 페이지에 마스터 레코드를 포함 하 고 다른 하나에는 세부 정보를 표시 하는 것입니다. [ASP.NET 포럼과](https://forums.asp.net/)같은 포럼 웹 사이트는 실제로이 패턴의 좋은 예입니다. ASP.NET 포럼은 시작, Web Forms, 데이터 프레젠테이션 컨트롤 등을 비롯 한 다양 한 포럼으로 구성 됩니다. 각 포럼은 많은 스레드로 구성 되며 각 스레드는 여러 개의 게시물로 구성 됩니다. ASP.NET 포럼 홈페이지에 포럼이 나열 됩니다. 포럼을 클릭 하면 해당 포럼의 스레드를 나열 하는 `ShowForum.aspx` 페이지로 whisks. 마찬가지로 스레드를 클릭 하면 클릭 된 스레드에 대 한 게시물이 표시 되는 `ShowPost.aspx`로 이동 합니다.

이 자습서에서는 GridView를 사용 하 여 데이터베이스의 공급자를 나열 하는 방법으로이 패턴을 구현 합니다. GridView의 각 공급자 행에는 클릭 하면 사용자가 선택한 공급자에 대 한 제품을 나열 하는 별도의 페이지로 이동 하는 제품 보기 링크가 포함 됩니다.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>1 단계:`Filtering`폴더에`SupplierListMaster.aspx`및`ProductsForSupplierDetails.aspx`페이지 추가

세 번째 자습서에서 페이지 레이아웃을 정의할 때 `BasicReporting`, `Filtering`및 `CustomFormatting` 폴더에 많은 "시작" 페이지가 추가 되었습니다. 그러나이 자습서에서는이 자습서에 대 한 시작 페이지를 추가 하지 않았으므로 `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx``Filtering` 폴더에 새 페이지 두 개를 추가 합니다. `SupplierListMaster.aspx`은 선택한 공급자에 대 한 제품을 표시 `ProductsForSupplierDetails.aspx`는 동안 "마스터" 레코드 (공급 업체)를 나열 합니다.

이러한 두 개의 새 페이지를 만들 때 `Site.master` 마스터 페이지와 연결 해야 합니다.

![SupplierListMaster 및 ProductsForSupplierDetails 페이지를 필터링 폴더에 추가 합니다.](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**그림 1**: `Filtering` 폴더에 `SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx` 페이지 추가

또한 프로젝트에 새 페이지를 추가 하는 경우에는 `Web.sitemap`사이트 맵 파일을 업데이트 해야 합니다. 이 자습서에서는 다음 XML 콘텐츠를 필터링 보고서 `<siteMapNode>` 요소의 자식으로 사용 하 여 사이트 맵에 `SupplierListMaster.aspx` 페이지를 추가 하기만 하면 됩니다.

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> ASP.NET [Allen](http://odetocode.com/Blogs/scott/)의 무료 Visual Studio [사이트 맵 매크로](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)를 사용 하 여 새 페이지를 추가할 때 사이트 맵 파일을 업데이트 하는 프로세스를 자동화할 수 있습니다.

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>2 단계:`SupplierListMaster.aspx`에서 공급자 목록 표시

`SupplierListMaster.aspx` 및 `ProductsForSupplierDetails.aspx` 페이지를 만들었으면 다음 단계는 `SupplierListMaster.aspx`에서 공급자의 GridView를 만드는 것입니다. 페이지에 GridView를 추가 하 고 새 ObjectDataSource에 바인딩합니다. 이 ObjectDataSource는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드를 사용 하 여 모든 공급자를 반환 해야 합니다.

[SuppliersBLL 클래스 ![선택 합니다.](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**그림 2**: `SuppliersBLL` 클래스 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image4.png))

[GetSuppliers () 메서드를 사용 하도록 ObjectDataSource를 구성 ![](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**그림 3**: `GetSuppliers()` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image7.png))

클릭 하면 사용자가 querystring을 통해 선택한 행의 `SupplierID` 값을 전달 하는 `ProductsForSupplierDetails.aspx` 하는 각 GridView 행에 Products 보기 라는 링크가 포함 되어야 합니다. 예를 들어 사용자가 도쿄 Traders 공급 업체에 대 한 제품 보기 링크 (`SupplierID` 값이 4 인 경우)를 클릭 하면 `ProductsForSupplierDetails.aspx?SupplierID=4`으로 전송 됩니다.

이렇게 하려면 하이퍼링크 [필드](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) 를 gridview에 추가 하 여 각 gridview 행에 하이퍼링크를 추가 합니다. GridView의 스마트 태그에서 열 편집 링크를 클릭 하 여 시작 합니다. 다음으로 왼쪽 위의 목록에서 hyperlink 필드를 선택 하 고 추가를 클릭 하 여 GridView의 필드 목록에 하이퍼링크 필드를 포함 합니다.

[GridView에 하이퍼링크 필드 추가 ![](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**그림 4**: GridView에 하이퍼링크 필드 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image10.png))

각 GridView 행의 링크를 사용 하 여 동일한 텍스트 또는 URL 값을 사용 하거나 각 특정 행에 바인딩된 데이터 값에 대해 이러한 값을 기준으로 하 여 하이퍼링크 필드를 구성할 수 있습니다. 모든 행에서 정적 값을 지정 하려면 하이퍼링크 필드의 `Text` 또는 `NavigateUrl` 속성을 사용 합니다. 모든 행에 대해 링크 텍스트를 동일 하 게 하려면 하이퍼링크 필드의 `Text` 속성을 제품 보기로 설정 합니다.

[제품을 보기 위해 하이퍼링크 필드의 Text 속성을 설정 ![](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**그림 5**: 하이퍼링크 필드의 `Text` 속성을 설정 하 여 제품 보기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image13.png))

GridView 행에 바인딩된 내부 데이터를 기반으로 하는 텍스트 또는 URL 값을 설정 하려면 `DataTextField` 또는 `DataNavigateUrlFields` 속성에서 텍스트 또는 URL 값을 끌어올 데이터 필드를 지정 합니다. `DataTextField`는 단일 데이터 필드에만 설정할 수 있습니다. 그러나 `DataNavigateUrlFields`를 쉼표로 구분 된 데이터 필드 목록으로 설정할 수 있습니다. 현재 행의 데이터 필드 값과 일부 정적 태그를 조합 하 여 텍스트 또는 URL의 기반을 설정 해야 하는 경우가 많습니다. 예를 들어이 자습서에서는 하이퍼링크 필드의 링크 URL을 `ProductsForSupplierDetails.aspx?SupplierID=supplierID`합니다. 여기서 *`supplierID`* 는 각 GridView의 row's `SupplierID` 값입니다. 여기에는 정적 및 데이터 기반 값이 모두 필요 합니다. 즉, 링크 URL의 `ProductsForSupplierDetails.aspx?SupplierID=` 부분이 정적 이지만 *`supplierID`* 부분은 값이 각 행의 고유한 `SupplierID` 값 이기 때문에 데이터를 기반으로 합니다.

정적 및 데이터 기반 값의 조합을 나타내려면 `DataTextFormatString` 및 `DataNavigateUrlFormatString` 속성을 사용 합니다. 이러한 속성에서 필요에 따라 정적 태그를 입력 한 다음 `DataTextField` 또는 `DataNavigateUrlFields` 속성에 지정 된 필드의 값을 표시할 `{0}` 표식을 사용 합니다. `DataNavigateUrlFields` 속성에 여러 필드가 지정 된 경우 첫 번째 필드 값을 삽입 하려는 `{0}`를 사용 하 고, 두 번째 필드 값에 `{1}` 하는 등의 방법을 사용 합니다.

이를 자습서에 적용 하면 `DataNavigateUrlFields` 속성이 `SupplierID`로 설정 되어야 합니다 .이는 행 단위로 사용자 지정 해야 하는 값이 포함 된 데이터 필드 이며 `DataNavigateUrlFormatString` 속성을 `ProductsForSupplierDetails.aspx?SupplierID={0}`합니다.

[공급자에 따라 적절 한 링크 URL을 포함 하도록 hyperlink 필드를 구성 ![](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**그림 6**: `SupplierID`에 따라 적절 한 링크 URL을 포함 하도록 hyperlink 필드 구성 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image16.png))

하이퍼링크 필드를 추가한 후 GridView의 필드를 자유롭게 사용자 지정 하 고 순서를 변경할 수 있습니다. 다음 태그는 일부 사소한 필드 수준 사용자 지정을 만든 후 GridView를 보여 줍니다.

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

잠시 시간을 사용 하 여 브라우저를 통해 `SupplierListMaster.aspx` 페이지를 봅니다. 그림 7에 표시 된 것 처럼 페이지에는 제품 보기 링크를 비롯 한 모든 공급 업체가 나열 되어 있습니다. 제품 보기 링크를 클릭 하면 querystring에서 공급자의 `SupplierID`를 전달 하는 `ProductsForSupplierDetails.aspx`으로 이동 합니다.

[각 공급 업체 행 ![제품 보기 링크를 포함 합니다.](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**그림 7**: 각 공급 업체 행에 제품 보기 링크가 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image19.png)).

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>3 단계:`ProductsForSupplierDetails.aspx`에 공급자 제품 나열

이 시점에서 `SupplierListMaster.aspx` 페이지는 `ProductsForSupplierDetails.aspx`으로 사용자를 보내고 선택한 공급자의 `SupplierID`를 querystring에 전달 합니다. 자습서의 마지막 단계는 `SupplierID` querystring을 통해 전달 된 `SupplierID`와 일치 하는 `ProductsForSupplierDetails.aspx`의 GridView에 제품을 표시 하는 것입니다. 이를 수행 하려면 `ProductsBLL` 클래스에서 `GetProductsBySupplierID(supplierID)` 메서드를 호출 하 `ProductsBySupplierDataSource` 라는 새 ObjectDataSource 컨트롤을 사용 하 여 `ProductsForSupplierDetails.aspx` 페이지에 GridView를 추가 합니다.

[ProductsBySupplierDataSource 라는 새 ObjectDataSource를 추가 ![](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**그림 8**: 이름이 `ProductsBySupplierDataSource` 새 ObjectDataSource 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image22.png))

[ProductsBLL 클래스 ![선택 합니다.](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**그림 9**: `ProductsBLL` 클래스 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image25.png))

[GetProductsBySupplierID (공급자) 메서드를 ObjectDataSource에서 호출 하는 ![](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**그림 10**: ObjectDataSource에서 `GetProductsBySupplierID(supplierID)` 메서드 호출 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image28.png))

데이터 원본 구성 마법사의 마지막 단계에서는 `GetProductsBySupplierID(supplierID)` 메서드의 *`supplierID`* 매개 변수 원본을 제공 하도록 요청 합니다. Querystring 값을 사용 하려면 매개 변수 원본을 QueryString으로 설정 하 고 QueryStringField textbox (`SupplierID`)에서 사용할 querystring 값의 이름을 입력 합니다.

[![공급자 매개 변수 값을 공급자 Querystring 값으로 채웁니다.](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**그림 11**: `SupplierID` Querystring 값에서 *`supplierID`* 매개 변수 값 채우기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image31.png))

이제 모든 작업을 마쳤습니다. 그림 12는 `SupplierListMaster.aspx`에서 도쿄 Traders 링크를 클릭 하 여 방문한 `ProductsForSupplierDetails.aspx` 페이지를 보여 줍니다.

[도쿄 Traders에서 제공 하는 제품이 표시 ![](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**그림 12**: 도쿄 Traders에서 제공 하는 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image34.png)).

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>`ProductsForSupplierDetails.aspx`에서 공급자 정보 표시

그림 12와 같이 `ProductsForSupplierDetails.aspx` 페이지에는 querystring에 지정 된 `SupplierID`에서 제공 하는 제품이 나열 됩니다. 그러나이 페이지로 직접 전송 된 누군가가 그림 12는 도쿄 상인의 제품을 표시 한다는 것을 알 수 없습니다. 이를 해결 하기 위해이 페이지에도 공급자 정보를 표시할 수 있습니다.

Products GridView 위에 FormView를 추가 하 여 시작 합니다. `SuppliersBLL` 클래스의 `GetSupplierBySupplierID(supplierID)` 메서드를 호출 하 `SuppliersDataSource` 라는 새 ObjectDataSource 컨트롤을 만듭니다.

[SuppliersBLL 클래스 ![선택 합니다.](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**그림 13**: `SuppliersBLL` 클래스 선택 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image37.png))

[GetSupplierBySupplierID (공급자) 메서드를 ObjectDataSource에서 호출 하는 ![](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**그림 14**: ObjectDataSource가 `GetSupplierBySupplierID(supplierID)` 메서드를 호출 하도록 합니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image40.png)).

`ProductsBySupplierDataSource`와 마찬가지로 *`supplierID`* 매개 변수에 `SupplierID` querystring 값 값을 할당 합니다.

[![공급자 매개 변수 값을 공급자 Querystring 값으로 채웁니다.](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**그림 15**: `SupplierID` Querystring 값에서 *`supplierID`* 매개 변수 값 채우기 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image43.png))

디자인 뷰에서 ObjectDataSource를 ObjectDataSource에 바인딩하는 경우 Visual Studio는 ObjectDataSource에서 반환 된 각 데이터 필드에 대해 레이블 및 TextBox 웹 컨트롤을 사용 하 여 FormView의 `ItemTemplate`, `InsertItemTemplate`및 `EditItemTemplate`를 자동으로 만듭니다. 공급자 정보를 표시 하기만 하면 `InsertItemTemplate`를 제거 하 고 `EditItemTemplate`수 있습니다. 그런 다음 `<h3>` 요소에 공급자의 회사 이름을 표시 하 고 회사 이름 아래에 주소, 도시, 국가 및 전화 번호를 표시 하도록 ItemTemplate을 편집 합니다. 또는 "[ObjectDataSource를 사용 하 여 데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)" 자습서에서 수행한 것 처럼 FormView의 `DataSourceID`를 수동으로 설정 하 고 `ItemTemplate` 태그를 만들 수 있습니다.

이러한 편집 후에는 FormView의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

그림 16은 위에서 설명한 공급자 정보가 포함 된 후 `ProductsForSupplierDetails.aspx` 페이지의 스크린샷을 보여 줍니다.

[제품 목록에 공급자에 대 한 요약이 포함 된 ![](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**그림 16**: 제품 목록에 공급자에 대 한 요약이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image46.png)).

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>`ProductsForSupplierDetails.aspx`UI에 대 한 최종 접촉 적용

이 보고서에 대 한 사용자 환경을 개선 하려면 `ProductsForSupplierDetails.aspx` 페이지에 추가 해야 하는 몇 가지 추가 사항이 있습니다. 현재 사용자가 `ProductsForSupplierDetails.aspx` 페이지에서 공급자 목록으로 다시 이동할 수 있는 유일한 방법은 해당 브라우저의 뒤로 단추를 클릭 하는 것입니다. `SupplierListMaster.aspx`에 다시 연결 되는 하이퍼링크 컨트롤을 `ProductsForSupplierDetails.aspx` 페이지에 추가 하 여 사용자가 마스터 목록으로 돌아갈 수 있는 다른 방법을 제공 합니다.

[![하이퍼링크 컨트롤을 추가 하 여 사용자를 SupplierListMaster로 다시 이동 합니다.](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**그림 17**: 사용자가 `SupplierListMaster.aspx`으로 다시 이동 하는 하이퍼링크 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image49.png))

사용자가 제품을 포함 하지 않은 공급자에 대 한 제품 보기 링크를 클릭 하면 `ProductsForSupplierDetails.aspx` `ProductsBySupplierDataSource` ObjectDataSource에서 결과가 반환 되지 않습니다. ObjectDataSource에 바인딩된 GridView는 사용자의 브라우저에서 페이지의 빈 영역을 생성 하는 태그를 렌더링 하지 않습니다. 선택한 공급자와 연결 된 제품이 없는 사용자에 게 더 명확 하 게 전달 하기 위해 GridView의 `EmptyDataText` 속성을 이러한 상황이 발생할 때 표시 하려는 메시지로 설정할 수 있습니다. 이 속성을 "이 공급자가 제공 하는 제품이 없습니다."로 설정 했습니다.

기본적으로 Northwinds 데이터베이스의 모든 공급 업체는 하나 이상의 제품을 제공 합니다. 그러나이 자습서에서는 공급자 Escargots Nouveaux이 더 이상 제품과 연결 되지 않도록 `Products` 테이블을 수동으로 수정 했습니다. 그림 18에서는 이러한 변경이 적용 된 후의 Escargots Nouveaux에 대 한 세부 정보 페이지를 보여 줍니다.

[![사용자에 게 공급 업체가 제품을 제공 하지 않는다는 것을 알 수 있습니다.](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**그림 18**: 공급 업체가 제품을 제공 하지 않는다는 알림이 사용자에 게[표시 됨 (전체 크기 이미지를 보려면 클릭](master-detail-filtering-across-two-pages-cs/_static/image52.png))

## <a name="summary"></a>요약

마스터/세부 정보 보고서에는 단일 페이지에 마스터 및 세부 레코드가 모두 표시 될 수 있지만 대부분의 웹 사이트에서는 두 개의 웹 페이지에서 분리 됩니다. 이 자습서에서는 "마스터" 웹 페이지에서 GridView에 나열 된 공급자와 "세부 정보" 페이지에 나열 된 관련 제품을 포함 하 여 이러한 마스터/세부 정보 보고서를 구현 하는 방법을 살펴보았습니다. 마스터 웹 페이지의 각 공급자 행에는 행의 `SupplierID` 값을 따라 전달 된 세부 정보 페이지에 대 한 링크가 포함 되어 있습니다. 이러한 행 관련 링크는 GridView의 하이퍼링크 필드를 사용 하 여 쉽게 추가할 수 있습니다.

세부 정보 페이지에서 지정 된 공급자에 대 한 제품 검색은 `ProductsBLL` 클래스의 `GetProductsBySupplierID(supplierID)` 메서드를 호출 하 여 수행 되었습니다. 쿼리 문자열을 매개 변수 소스로 사용 하 여 *`supplierID`* 매개 변수 값을 선언적으로 지정 했습니다. 또한 FormView를 사용 하 여 세부 정보 페이지에 공급자 세부 정보를 표시 하는 방법을 살펴보았습니다.

[다음 자습서](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 는 마스터/세부 정보 보고서에 대 한 마지막 자습서입니다. 각 행에 선택 단추가 있는 GridView의 제품 목록을 표시 하는 방법을 살펴보겠습니다. 선택 단추를 클릭 하면 동일한 페이지의 DetailsView 컨트롤에 해당 제품의 세부 정보가 표시 됩니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Gid Esenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](master-detail-filtering-with-two-dropdownlists-cs.md)
> [다음](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
