---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: ObjectDataSource를 사용 하 여 데이터 캐싱 (VB) | Microsoft Docs
author: rick-anderson
description: 캐싱은 속도가 느리고 빠른 웹 응용 프로그램 간의 차이를 의미할 수 있습니다. 이 자습서는 ASP.NET의 캐싱을 자세히 확인 하는 4 개 중 첫 번째입니다.
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 16f20d9a0f4f677073174d680418b278dba40b07
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74612172"
---
# <a name="caching-data-with-the-objectdatasource-vb"></a>ObjectDataSource를 사용하여 데이터 캐싱(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe) 또는 [PDF 다운로드](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> 캐싱은 속도가 느리고 빠른 웹 응용 프로그램 간의 차이를 의미할 수 있습니다. 이 자습서는 ASP.NET의 캐싱을 자세히 살펴보는 4 중 첫 번째입니다. 캐싱에 대 한 주요 개념 및 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층에 캐싱을 적용 하는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

컴퓨터 과학에서 *캐싱은* 액세스 하는 데 더 빠른 위치에 복사본을 얻고 저장 하는 데 비용이 많이 드는 데이터 또는 정보를 가져오는 프로세스입니다. 데이터 기반 응용 프로그램의 경우 크고 복잡 한 쿼리는 일반적으로 대부분의 응용 프로그램 실행 시간을 사용 합니다. 이러한 응용 프로그램의 성능은 응용 프로그램의 메모리에 비용이 많이 드는 데이터베이스 쿼리 결과를 저장 하 여 자주 향상 될 수 있습니다.

ASP.NET 2.0는 다양 한 캐싱 옵션을 제공 합니다. 전체 웹 페이지 또는 사용자 정의 컨트롤의 렌더링 된 태그는 *출력 캐싱을*통해 캐시 될 수 있습니다. ObjectDataSource 및 SqlDataSource 컨트롤은 캐싱 기능도 제공 하므로 데이터를 컨트롤 수준에서 캐시할 수 있습니다. 및 ASP.NET s *데이터 캐시* 는 페이지 개발자가 프로그래밍 방식으로 개체를 캐시 하는 데 사용할 수 있는 풍부한 캐싱 API를 제공 합니다. 이 자습서 및 다음 세 가지에서는 데이터 캐시 뿐만 아니라 ObjectDataSource s 캐싱 기능을 사용 하 여 살펴보겠습니다. 또한 시작 시 응용 프로그램 전체 데이터를 캐시 하는 방법 및 SQL 캐시 종속성을 사용 하 여 캐시 된 데이터를 최신 상태로 유지 하는 방법을 알아봅니다. 이러한 자습서에서는 출력 캐싱을 탐색 하지 않습니다. 출력 캐싱에 대 한 자세한 내용은 [ASP.NET 2.0의 출력 캐싱](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)을 참조 하세요.

캐싱은 프레젠테이션 계층을 통해 데이터 액세스 계층에서 아키텍처의 어느 위치에 나 적용할 수 있습니다. 이 자습서에서는 ObjectDataSource 컨트롤을 통해 프레젠테이션 계층에 캐싱을 적용 하는 방법을 살펴보겠습니다. 다음 자습서에서는 비즈니스 논리 계층에서 데이터 캐싱을 살펴보겠습니다.

## <a name="key-caching-concepts"></a>키 캐싱 개념

캐싱은 더 효율적으로 액세스할 수 있는 위치에 복사본을 생성 하 고 저장 하는 데 비용이 많이 드는 데이터를 활용 하 여 응용 프로그램의 전반적인 성능 및 확장성을 크게 향상 시킬 수 있습니다. 캐시에는 실제 기본 데이터의 복사본만 포함 되므로 기본 데이터가 *변경 되 면 오래 되거나 오래*된 상태가 될 수 있습니다. 이를 위해 페이지 개발자는 다음 중 하나를 사용 하 여 캐시 항목이 캐시에서 *제거* 되는 기준을 나타낼 수 있습니다.

- **시간 기반 조건** 절대 또는 슬라이딩 기간 동안 항목을 캐시에 추가할 수 있습니다. 예를 들어, 페이지 개발자는 60 초의 기간을 나타낼 수 있습니다. 절대 기간을 사용 하는 경우 캐시 된 항목은 액세스 빈도에 관계 없이 캐시에 추가 된 후 60 초 후에 제거 됩니다. 슬라이딩 기간을 사용 하면 캐시 된 항목이 마지막 액세스 후 60 초 후에 제거 됩니다.
- **종속성 기반 조건-** 캐시에 추가 될 때 종속성을 항목과 연결할 수 있습니다. 항목의 종속성이 변경 되 면 캐시에서 제거 됩니다. 종속성은 파일, 다른 캐시 항목 또는 둘의 조합일 수 있습니다. ASP.NET 2.0는 또한 개발자가 캐시에 항목을 추가 하 고 기본 데이터베이스 데이터가 변경 될 때 해당 항목을 제거 하도록 하는 SQL 캐시 종속성을 허용 합니다. 향후 [Sql 캐시 종속성 사용](using-sql-cache-dependencies-vb.md) 자습서에서 sql 캐시 종속성을 검토 합니다.

지정 된 제거 조건에 관계 없이 시간 기반 또는 종속성 기반 조건이 충족 되기 전에 캐시의 항목이 *청소* 될 수 있습니다. 캐시가 용량에 도달 하면 기존 항목을 제거 해야 새 항목을 추가할 수 있습니다. 결과적으로 캐시 된 데이터를 프로그래밍 방식으로 작업 하는 경우 캐시 된 데이터가 항상 존재 하지 않을 수 있다고 가정 하는 것이 중요 합니다. 다음 자습서 인 *아키텍처의 데이터 캐싱*에서 프로그래밍 방식으로 캐시의 데이터에 액세스할 때 사용할 패턴을 살펴보겠습니다.

캐싱은 응용 프로그램에서 더 많은 성능을 제공 하는 경제적 수단을 제공 합니다. 이 문서에서 명확히 [Smith](http://aspadvice.com/blogs/ssmith/) 는 [ASP.NET 캐싱: 기술 및 모범 사례](https://msdn.microsoft.com/library/aa478965.aspx)를 참조 하세요.

캐싱은 많은 시간과 분석을 요구 하지 않고 충분 한 성능을 제공 하는 좋은 방법일 수 있습니다. 메모리는 저렴 하므로, 코드 또는 데이터베이스를 최적화 하는 데 하루 또는 일주일을 소비 하는 대신 30 초 동안 출력을 캐싱하여 필요한 성능을 얻을 수 있는 경우 캐싱 솔루션 (30 초 이전 데이터가 양호 하다 고 가정)을 수행 하 고 이동 합니다. 결국 잘못 된 설계로 인해 사용자가 올바르게 구성 될 수 있으므로 응용 프로그램을 올바르게 디자인 하는 것이 좋습니다. 그러나 지금 충분 한 성능을 제공 해야 하는 경우 캐싱은 좋은 [접근 방식]이 될 수 있으므로 나중에 응용 프로그램을 리팩터링 하는 시간을 확보할 수 있습니다.

캐싱은 있는 이점은 성능 향상을 제공할 수 있지만, 실시간으로 업데이트 되는 데이터를 사용 하는 응용 프로그램 또는 곧 오래 지속 되는 데이터를 사용할 수 없는 경우와 같은 일부 상황에서는 적용 되지 않습니다. 하지만 대부분의 응용 프로그램에서는 캐싱이 사용 되어야 합니다. ASP.NET 2.0의 캐싱에 대 한 자세한 배경 정보는 [ASP.NET 2.0 빠른 시작 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/)의 [성능에 대 한 캐싱](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) 섹션을 참조 하세요.

## <a name="step-1-creating-the-caching-web-pages"></a>1 단계: 캐싱 웹 페이지 만들기

ObjectDataSource의 캐싱 기능에 대 한 탐색을 시작 하기 전에 먼저이 자습서와 다음 3 개에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `Caching`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**그림 1**: 캐싱 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `Caching` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[![그림 2: Default.aspx에 SectionLevelTutorialListing 사용자 정의 컨트롤 추가](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image4.png))

마지막으로, 이러한 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히, 이진 데이터 작업 후 다음 태그를 추가 `<siteMapNode>`합니다.

[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 캐싱 자습서에 대 한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 캐싱 자습서에 대 한 항목이 포함 되어 있습니다.](caching-data-with-the-objectdatasource-vb/_static/image5.png)

**그림 3**: 이제 사이트 맵에 캐싱 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>2 단계: 웹 페이지에서 제품 목록 표시

이 자습서에서는 ObjectDataSource 컨트롤의 기본 제공 캐싱 기능을 사용 하는 방법을 살펴봅니다. 그러나 이러한 기능을 살펴보기 전에 먼저 작업할 페이지가 필요 합니다. 에서 GridView를 사용 하 여 `ProductsBLL` 클래스에서 ObjectDataSource로 검색 되는 제품 정보를 나열 하는 웹 페이지를 만들어 보겠습니다.

먼저 `Caching` 폴더에서 `ObjectDataSource.aspx` 페이지를 엽니다. GridView를 도구 상자에서 디자이너로 끌고, 해당 `ID` 속성을 `Products`로 설정 하 고, 스마트 태그에서를 선택 하 여 `ProductsDataSource`라는 새 ObjectDataSource 컨트롤에 바인딩합니다. `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource를 구성 합니다.

[ProductsBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**그림 4**: `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image8.png))

이 페이지에 대해에서 GridView에 캐시 된 데이터가 GridView 인터페이스를 통해 수정 될 때 발생 하는 작업을 검토할 수 있도록 편집 가능한 GridView를 만들어 보겠습니다. 선택 탭의 드롭다운 목록을 기본값인 `GetProducts()`로 설정 된 채로 두고 업데이트 탭에서 선택한 항목을 입력 매개 변수로 `productName`, `unitPrice`및 `productID`을 허용 하는 `UpdateProduct` 오버 로드로 변경 합니다.

[![업데이트 탭 드롭다운 목록을 적절 한 UpdateProduct 오버 로드로 설정 합니다.](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**그림 5**: 업데이트 탭의 드롭다운 목록을 적절 한 `UpdateProduct` 오버 로드로 설정 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image11.png))

마지막으로 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 하 고 마침을 클릭 합니다. 데이터 소스 구성 마법사가 완료 되 면 Visual Studio에서는 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`로 설정 합니다. [데이터 삽입, 업데이트 및 삭제에 대 한 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 에서 설명한 것 처럼이 속성은 선언적 구문에서 제거 하거나 업데이트 워크플로를 오류 없이 계속 진행 하기 위해 기본값인 `{0}`로 다시 설정 해야 합니다.

또한 마법사가 완료 되 면 Visual Studio에서 각 제품 데이터 필드에 대 한 필드를 GridView에 추가 합니다. `ProductName`, `CategoryName`및 `UnitPrice` BoundFields를 제외한 모든을 제거 합니다. 그런 다음 이러한 각 BoundFields의 `HeaderText` 속성을 각각 Product, Category 및 Price로 업데이트 합니다. `ProductName` 필드가 필요 하므로 BoundField을 Templatefield로 변환로 변환 하 고 `EditItemTemplate`에 RequiredFieldValidator를 추가 합니다. 마찬가지로 `UnitPrice` BoundField을 Templatefield로 변환로 변환 하 고, 사용자가 입력 한 값이 0 보다 크거나 같은 유효한 통화 값이 되도록 CompareValidator를 추가 합니다. 이러한 수정 외에도 `UnitPrice` 값을 오른쪽에 정렬 하거나 읽기 전용 및 편집 인터페이스에서 `UnitPrice` 텍스트의 서식을 지정 하는 등의 미적 변경 작업을 자유롭게 수행할 수 있습니다.

GridView의 스마트 태그에서 편집 사용 확인란을 선택 하 여 GridView를 편집 가능 하도록 설정 합니다. 또한 페이징 사용 및 정렬 사용 확인란을 선택 합니다.

> [!NOTE]
> GridView 편집 인터페이스를 사용자 지정 하는 방법에 대 한 검토가 필요 한가요? 그렇다면 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md) 자습서를 다시 참조 하세요.

[편집, 정렬 및 페이징을 위한 GridView 지원 사용 ![](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**그림 6**: 편집, 정렬 및 페이징에 대해 GridView 지원 사용 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image14.png))

이러한 GridView를 수정한 후 GridView와 ObjectDataSource의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

그림 7에 표시 된 것 처럼 편집 가능한 GridView에는 데이터베이스에 있는 각 제품의 이름, 범주 및 가격이 나열 됩니다. 잠시 페이지의 기능을 테스트 하 여 결과를 정렬 하 고, 페이지를 이동 하 고, 레코드를 편집 합니다.

[각 제품 이름, 범주 및 가격은 정렬 가능 하 고 페이징할 수 있는 편집 가능한 GridView에 나열 ![.](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**그림 7**: 각 제품의 이름, 범주 및 가격은 정렬 가능 하 고 페이징할 수 있는 편집 가능한 GridView ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image17.png))에 나열 되어 있습니다.

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>3 단계: ObjectDataSource에서 데이터를 요청 하는 경우 검사

`Products` GridView는 `ProductsDataSource` ObjectDataSource의 `Select` 메서드를 호출 하 여 표시할 데이터를 검색 합니다. 이 ObjectDataSource는 비즈니스 논리 계층 s `ProductsBLL` 클래스의 인스턴스를 만들고 해당 `GetProducts()` 메서드를 호출 합니다. 그러면이 메서드는 데이터 액세스 계층 s `ProductsTableAdapter` s `GetProducts()` 메서드를 호출 합니다. DAL 메서드는 Northwind 데이터베이스에 연결 하 여 구성 된 `SELECT` 쿼리를 실행 합니다. 그런 다음이 데이터는 DAL로 반환 되 고 `NorthwindDataTable`에 패키지 됩니다. DataTable 개체는 BLL로 반환 됩니다. 그러면 ObjectDataSource로 반환 됩니다. 그러면 GridView로 반환 됩니다. 그런 다음 GridView는 DataTable의 각 `DataRow`에 대 한 `GridViewRow` 개체를 만들고 각 `GridViewRow`는 궁극적으로 클라이언트에 반환 되 고 방문자의 브라우저에 표시 되는 HTML로 렌더링 됩니다.

이러한 이벤트 시퀀스는 각각 GridView가 기본 데이터에 바인딩해야 할 때마다 발생 합니다. 페이지를 처음 방문할 때, GridView를 정렬할 때 또는 기본 제공 되는 인터페이스 편집 또는 삭제를 통해 GridView의 데이터를 수정 하는 경우에 발생 합니다. GridView의 뷰 상태가 사용 하지 않도록 설정 된 경우 GridView는 각 및 다시 게시에도 다시 바인딩 됩니다. 또한 GridView는 해당 `DataBind()` 메서드를 호출 하 여 데이터에 명시적으로 데이터를 바인딩할 수 있습니다.

데이터베이스에서 데이터를 검색 하는 빈도를 충분히 이해 하려면 데이터를 다시 검색 하는 경우를 나타내는 메시지를 표시 합니다. `ODSEvents`라는 GridView 위에 Label 웹 컨트롤을 추가 합니다. `Text` 속성을 지우고 `EnableViewState` 속성을 `False`로 설정 합니다. 레이블 아래에서 단추 웹 컨트롤을 추가 하 고 해당 `Text` 속성을 다시 게시로 설정 합니다.

[GridView 위의 페이지에 레이블 및 단추를 추가 ![](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**그림 8**: GridView 위의 페이지에 레이블 및 단추 추가 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image20.png))

데이터 액세스 워크플로를 실행 하는 동안 ObjectDataSource s `Selecting` 이벤트는 기본 개체가 만들어지고 구성 된 메서드가 호출 되기 전에 발생 합니다. 이 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

ObjectDataSource에서 데이터에 대 한 아키텍처를 요청 하면 레이블이 실행 되는 이벤트 선택이 표시 됩니다.

브라우저에서이 페이지를 방문 하세요. 페이지를 처음 방문할 때 발생 한 이벤트 선택 텍스트가 표시 됩니다. 다시 게시 단추를 클릭 하면 텍스트가 사라집니다. 즉, GridView s `EnableViewState` 속성이 `True`(기본값)로 설정 되어 있다고 가정 합니다. 다시 게시 시 GridView가 해당 뷰 상태에서 다시 생성 되므로 데이터에 대 한 ObjectDataSource로 전환 되지 않기 때문입니다. 그러나 데이터를 정렬, 페이징 또는 편집 하면 GridView가 해당 데이터 원본에 다시 바인딩하기 때문에 발생 한 이벤트 선택 텍스트가 다시 나타납니다.

[![GridView를 데이터 원본에 바인딩할 때마다 발생 하는 이벤트 선택이 표시 됩니다.](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**그림 9**: GridView가 데이터 원본에 바인딩 될 때마다 발생 하는 이벤트 선택이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image23.png)).

[다시 게시 단추를 클릭 하면 해당 뷰 상태에서 GridView가 다시 생성 됩니다 ![](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**그림 10**: 포스트백 단추를 클릭 하면 해당 뷰 상태에서 GridView가 재구성 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image26.png)).

데이터가 페이징 되거나 정렬 될 때마다 데이터베이스 데이터를 검색 하는 것은 불필요 한 것 처럼 보일 수 있습니다. 모든 경우 기본 페이징이 다시 사용 되므로 ObjectDataSource는 첫 번째 페이지를 표시할 때 모든 레코드를 검색 했습니다. GridView에서 정렬과 페이징을 지원 하지 않는 경우에도 모든 사용자가 페이지를 처음 방문할 때마다 데이터베이스에서 데이터를 검색 해야 하며, 뷰 상태가 사용 하지 않도록 설정 된 경우에는 모든 사용자가 다시 게시할 때마다 데이터를 검색 해야 합니다. 그러나 GridView가 모든 사용자에 게 동일한 데이터를 표시 하는 경우 이러한 추가 데이터베이스 요청은 불필요 합니다. `GetProducts()` 메서드에서 반환 된 결과를 캐시 하지 않고 GridView를 해당 캐시 된 결과에 바인딩 하는 이유는 무엇 인가요?

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>4 단계: ObjectDataSource를 사용 하 여 데이터 캐싱

몇 가지 속성만 설정 하면 ASP.NET 데이터 캐시에 검색 된 데이터를 자동으로 캐시 하도록 ObjectDataSource를 구성할 수 있습니다. 다음 목록에는 ObjectDataSource의 캐시 관련 속성이 요약 되어 있습니다.

- 캐싱을 사용 하려면 `True` [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) 로 설정 해야 합니다. 기본값은 `False`입니다.
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) 데이터를 캐시 하는 시간 (초)입니다. 기본값은 0입니다. ObjectDataSource는 `EnableCaching` `True` 되 고 `CacheDuration` 0 보다 큰 값으로 설정 된 경우에만 데이터를 캐시 합니다.
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) 은 `Absolute` 또는 `Sliding`로 설정할 수 있습니다. `Absolute`경우 ObjectDataSource는 `CacheDuration` 초 동안 검색 된 데이터를 캐시 합니다. `Sliding`경우 데이터는 `CacheDuration` 초 동안 액세스 되지 않은 후에만 만료 됩니다. 기본값은 `Absolute`입니다.
- [Cachekeydependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) 이 속성을 사용 하 여 ObjectDataSource s 캐시 항목을 기존 캐시 종속성에 연결 합니다. ObjectDataSource s 데이터 항목은 연결 된 `CacheKeyDependency`를 만료 시켜 캐시에서 중간에 제거할 수 있습니다. 이 속성은 sql 캐시 종속성을 ObjectDataSource s 캐시와 연결 하는 데 가장 일반적으로 사용 됩니다. [Sql 캐시 종속성 자습서를 사용 하 여](using-sql-cache-dependencies-vb.md) 나중에 살펴볼 항목입니다.

에서 `ProductsDataSource` ObjectDataSource를 구성 하 여 해당 데이터를 30 초 동안 절대 크기로 캐시 하도록 합니다. ObjectDataSource s `EnableCaching` 속성을 `True`로 설정 하 고 `CacheDuration` 속성을 30으로 설정 합니다. `CacheExpirationPolicy` 속성을 기본값인 `Absolute`으로 설정 된 상태로 둡니다.

[데이터를 30 초로 캐시 하도록 ObjectDataSource를 구성 ![](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**그림 11**: 데이터를 30 초로 캐시 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](caching-data-with-the-objectdatasource-vb/_static/image29.png))

변경 내용을 저장 하 고 브라우저에서이 페이지를 다시 방문 합니다. 처음으로 페이지를 방문할 때 데이터가 캐시에 없기 때문에 발생 한 이벤트 선택 텍스트가 표시 됩니다. 그러나 다시 게시 단추를 클릭 하거나, 페이지를 정렬 하거나, 편집 또는 취소 단추를 클릭 하 여 트리거하는 이후 포스트백은 발생 하는 이벤트 발생 텍스트를 다시 표시 *하지* 않습니다. 이는 ObjectDataSource가 기본 개체에서 데이터를 가져오는 경우에만 `Selecting` 이벤트가 발생 하기 때문입니다. 데이터를 데이터 캐시에서 끌어올 경우 `Selecting` 이벤트가 발생 하지 않습니다.

30 초 후에는 캐시에서 데이터가 제거 됩니다. ObjectDataSource s `Insert`, `Update`또는 `Delete` 메서드를 호출 하는 경우에도 캐시에서 데이터가 제거 됩니다. 따라서 30 초가 경과 하거나 업데이트 단추를 클릭 하 여 정렬, 페이징 또는 편집 또는 취소 단추를 클릭 하면 ObjectDataSource가 기본 개체에서 데이터를 가져오고 `Selecting` 이벤트가 발생할 때 발생 하는 이벤트 선택 텍스트를 표시 합니다. 반환 된 결과는 데이터 캐시에 다시 배치 됩니다.

> [!NOTE]
> ObjectDataSource가 캐시 된 데이터와 함께 작동 하는 경우에도 이벤트가 자주 발생 하는 텍스트를 자주 선택 하는 것이 확인 되 면 메모리 제약 조건 때문일 수 있습니다. 사용 가능한 메모리가 충분 하지 않은 경우 ObjectDataSource에 의해 캐시에 추가 된 데이터가 청소 되었을 수 있습니다. ObjectDataSource가 데이터를 올바르게 캐시 하거나 데이터를 산발적으로 캐시 하지 않는 것으로 나타나는 경우 일부 응용 프로그램을 닫아 메모리를 확보 한 다음 다시 시도 하십시오.

그림 12에서는 ObjectDataSource s 캐싱 워크플로를 보여 줍니다. 발생 한 이벤트 선택 텍스트가 화면에 표시 되 면 데이터가 캐시에 없고 원본 개체에서 검색 되어야 하기 때문입니다. 그러나이 텍스트가 없으면 캐시에서 데이터를 사용할 수 있기 때문입니다. 캐시에서 데이터가 반환 될 때 원본 개체에 대 한 호출이 없으므로 데이터베이스 쿼리가 실행 되지 않습니다.

![ObjectDataSource는 데이터 캐시에서 해당 데이터를 저장 하 고 검색 합니다.](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**그림 12**: ObjectDataSource는 데이터 캐시에서 데이터를 저장 하 고 검색 합니다.

각 ASP.NET 응용 프로그램에는 모든 페이지와 방문자에서 공유 하는 자체 데이터 캐시 인스턴스가 있습니다. 즉, ObjectDataSource에 의해 데이터 캐시에 저장 된 데이터는 페이지를 방문 하는 모든 사용자에 게 공유 됩니다. 이를 확인 하려면 브라우저에서 `ObjectDataSource.aspx` 페이지를 엽니다. 페이지를 처음 방문 하면 이전 테스트에 의해 캐시에 추가 된 데이터가 이미 제거 된 것으로 가정 하 여 이벤트가 발생 한 선택 텍스트가 나타납니다. 두 번째 브라우저 인스턴스를 열고 URL을 복사 하 여 첫 번째 브라우저 인스턴스에 복사 하 여 붙여넣습니다. 두 번째 브라우저 인스턴스에서는 첫 번째 이벤트와 동일한 캐시 된 데이터를 사용 하기 때문에 발생 한 이벤트 선택 텍스트가 표시 되지 않습니다.

검색 된 데이터를 캐시에 삽입할 때 ObjectDataSource는 `CacheDuration` 및 `CacheExpirationPolicy` 속성 값을 포함 하는 캐시 키 값을 사용 합니다. ObjectDataSource에서 사용 되는 기본 비즈니스 개체의 형식입니다 .이 형식은 [`TypeName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) (이 예제에서는`ProductsBLL`)을 통해 지정 됩니다. `SelectMethod` 속성의 값과 `SelectParameters` 컬렉션에 있는 매개 변수의 이름 및 값입니다. [사용자 지정 페이징을](../paging-and-sorting/paging-and-sorting-report-data-vb.md)구현할 때 사용 되는 `StartRowIndex` 및 `MaximumRows` 속성의 값입니다.

이러한 속성을 조합 하 여 캐시 키 값을 사용 하면 이러한 값이 변경 될 때 고유한 캐시 항목이 됩니다. 예를 들어 이전 자습서에서는 지정 된 범주에 대 한 모든 제품을 반환 하는 `ProductsBLL` 클래스 `GetProductsByCategoryID(categoryID)`를 사용 하는 방법을 살펴보았습니다. 한 명의 사용자가 페이지로 이동 하 여 `CategoryID` 1 인 음료를 볼 수 있습니다. ObjectDataSource가 캐시에 있는 동안 다른 사용자가 조미료를 볼 수 있도록 해당 `SelectParameters` 결과를 캐시 하는 경우에는 다른 사용자가를 볼 때 조미료 보다는 캐시 된 음료 제품을 볼 수 있습니다. `SelectParameters`값을 포함 하는 이러한 속성에 의해 캐시 키를 변경 하 여 ObjectDataSource는 음료와 조미료에 대 한 별도의 캐시 항목을 유지 관리 합니다.

## <a name="stale-data-concerns"></a>부실 데이터 문제

ObjectDataSource는 `Insert`, `Update`또는 `Delete` 메서드 중 하나가 호출 될 때 캐시에서 해당 항목을 자동으로 임의로 합니다. 이렇게 하면 페이지를 통해 데이터를 수정할 때 캐시 엔트리를 지워 부실 데이터를 보호할 수 있습니다. 그러나 캐시를 사용 하 여 오래 된 데이터를 표시 하는 경우에도 ObjectDataSource를 사용할 수 있습니다. 가장 간단한 경우는 데이터베이스에서 직접 데이터를 변경 하기 때문입니다. 아마도 데이터베이스 관리자는 데이터베이스의 일부 레코드를 수정 하는 스크립트를 실행 한 것입니다.

이 시나리오는 보다 미묘한 방법으로 펼침 수도 있습니다. ObjectDataSource는 데이터 수정 메서드 중 하나를 호출할 때 캐시에서 해당 항목을 임의로 하 고, 제거 된 항목은 속성 값의 ObjectDataSource s 특정 조합 (`CacheDuration`, `TypeName`, `SelectMethod`등)을 위한 것입니다. 다른 `SelectMethods` 또는 `SelectParameters`를 사용 하는 두 개의 ObjectDataSources 원본이 있지만 동일한 데이터를 계속 업데이트할 수 있는 경우 하나의 ObjectDataSource에서 행을 업데이트 하 고 자체 캐시 항목을 무효화할 수 있지만 두 번째 ObjectDataSource의 해당 행은 캐시 된에서 계속 제공 됩니다. 이 기능을 표시 하는 페이지를 만들 것을 권장 합니다. 캐싱을 사용 하 고 `ProductsBLL` 클래스 s `GetProducts()` 메서드에서 데이터를 가져오도록 구성 된 ObjectDataSource에서 데이터를 가져오는 편집 가능한 GridView를 표시 하는 페이지를 만듭니다. 이 페이지에 편집 가능한 GridView 및 ObjectDataSource를 추가 합니다. 그러나이 두 번째 ObjectDataSource에는 `GetProductsByCategoryID(categoryID)` 메서드를 사용 합니다. 두 ObjectDataSources 원본 `SelectMethod` 속성이 다르기 때문에 각 데이터 원본에는 고유한 캐시 된 값이 있습니다. 한 표에서 제품을 편집 하는 경우 다음에 데이터를 다른 그리드 (페이징, 정렬 등)로 다시 바인딩할 때는 이전에 캐시 된 데이터를 계속 제공 하 고 다른 그리드에서 수행한 변경 내용을 반영 하지 않습니다.

즉, 오래 된 데이터를 사용할 수 있는 경우에만 시간 기반 expiries을 사용 하 고, 데이터의 새로 고침은 중요 한 시나리오에 짧은 expiries를 사용 합니다. 부실 데이터를 사용할 수 없는 경우은 선형화 캐싱을 사용 하거나 SQL 캐시 종속성을 사용 합니다 (다시 캐싱이 되는 데이터베이스 데이터 라고 가정). 이후 자습서에서 SQL 캐시 종속성을 살펴보겠습니다.

## <a name="summary"></a>요약

이 자습서에서는 ObjectDataSource s 기본 제공 캐싱 기능을 검사 했습니다. 몇 가지 속성만 설정 하면 지정 된 `SelectMethod`에서 반환 된 결과를 ASP.NET 데이터 캐시로 캐시 하도록 ObjectDataSource에 지시할 수 있습니다. `CacheDuration` 및 `CacheExpirationPolicy` 속성은 항목이 캐시 되는 기간과 절대 또는 슬라이딩 만료 인지 여부를 나타냅니다. `CacheKeyDependency` 속성은 모든 ObjectDataSource s 캐시 항목을 기존 캐시 종속성에 연결 합니다. 이는 시간 기반 만료에 도달 하기 전에 캐시에서 ObjectDataSource 항목을 제거 하는 데 사용할 수 있으며 일반적으로 SQL 캐시 종속성과 함께 사용 됩니다.

ObjectDataSource는 단순히 데이터 캐시에 값을 캐시 하므로 ObjectDataSource의 기본 제공 기능을 프로그래밍 방식으로 복제할 수 있습니다. ObjectDataSource는이 기능을 즉시 제공 하므로 프레젠테이션 계층에서이 작업을 수행 하는 것은 적합 하지 않지만 별도의 아키텍처 계층에서 캐싱 기능을 구현할 수 있습니다. 이렇게 하려면 ObjectDataSource에서 사용 하는 것과 동일한 논리를 반복 해야 합니다. 다음 자습서의 아키텍처 내에서 프로그래밍 방식으로 데이터 캐시를 사용 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 캐싱: 기술 및 모범 사례](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework 응용 프로그램에 대 한 캐싱 아키텍처 가이드](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2.0의 출력 캐싱](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murphy입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](using-sql-cache-dependencies-cs.md)
> [다음](caching-data-in-the-architecture-vb.md)
