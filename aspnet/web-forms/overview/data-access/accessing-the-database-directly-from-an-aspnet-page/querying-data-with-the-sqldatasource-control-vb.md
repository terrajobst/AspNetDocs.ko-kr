---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
title: SqlDataSource 컨트롤을 사용 하 여 데이터 쿼리 (VB) | Microsoft Docs
author: rick-anderson
description: 위의 자습서에서는 ObjectDataSource 컨트롤을 사용 하 여 데이터 액세스 계층에서 프레젠테이션 계층을 완전히 분리 했습니다. 이 강사를 시작 하는 중 ...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: b12f752d-3502-40a4-b695-fc7b7d08cfd3
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 199ddb46e877c3a0937672d33241a240660684da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74606109"
---
# <a name="querying-data-with-the-sqldatasource-control-vb"></a>SqlDataSource 컨트롤을 사용하여 데이터 쿼리(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_VB.exe) 또는 [PDF 다운로드](querying-data-with-the-sqldatasource-control-vb/_static/datatutorial47vb1.pdf)

> 위의 자습서에서는 ObjectDataSource 컨트롤을 사용 하 여 데이터 액세스 계층에서 프레젠테이션 계층을 완전히 분리 했습니다. 이 자습서부터 시작 하 여, 프레젠테이션 및 데이터 액세스를 엄격 하 게 분리 하지 않아도 되는 간단한 응용 프로그램에 대해 SqlDataSource 컨트롤을 사용할 수 있는 방법을 알아봅니다.

## <a name="introduction"></a>소개

지금까지 검토 한 모든 자습서는 프레젠테이션, 비즈니스 논리 및 데이터 액세스 계층으로 구성 된 계층화 된 아키텍처를 사용 했습니다. DAL (데이터 액세스 계층)은 첫 번째 자습서 ([데이터 액세스 계층 생성](../introduction/creating-a-data-access-layer-vb.md)) 및 비즈니스 논리 계층 ([비즈니스 논리 계층 생성](../introduction/creating-a-business-logic-layer-vb.md))에서 작성 되었습니다. ObjectDataSource를 사용 하 여 [데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 자습서부터 ASP.NET 2.0 s 새 ObjectDataSource 컨트롤을 사용 하 여 프레젠테이션 계층에서 아키텍처와 선언적으로 인터페이스 하는 방법을 살펴보았습니다.

지금 까지의 모든 자습서에서는 아키텍처를 사용 하 여 데이터 작업을 수행 했지만 아키텍처를 우회 하 여 ASP.NET 페이지에서 직접 데이터베이스 데이터를 액세스, 삽입, 업데이트 및 삭제할 수 있습니다. 이렇게 하면 특정 데이터베이스 쿼리와 비즈니스 논리가 웹 페이지에 직접 배치 됩니다. 응용 프로그램의 성공, 업데이트 및 유지 관리를 위해 계층화 된 아키텍처를 디자인, 구현 및 사용 하는 것은 응용 프로그램의 성공, 업데이트 및 유지 관리에 매우 중요 합니다. 그러나 매우 간단한 일회용 응용 프로그램을 만드는 경우 강력한 아키텍처를 개발 하는 것은 불필요 합니다.

ASP.NET 2.0는 [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)및 [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)의 5 가지 기본 제공 데이터 소스 컨트롤을 제공 합니다. SqlDataSource를 사용 하 여 Microsoft SQL Server, Microsoft Access, Oracle, MySQL 등을 비롯 한 관계형 데이터베이스에서 직접 데이터에 액세스 하 고 수정할 수 있습니다. 이 자습서 및 다음 세 가지에서는 sqldatasource 컨트롤을 사용 하 여 작업 하는 방법, 데이터베이스 데이터를 쿼리하고 필터링 하는 방법, SqlDataSource를 사용 하 여 데이터를 삽입, 업데이트 및 삭제 하는 방법을 살펴보겠습니다.

![ASP.NET 2.0에는 5 가지 기본 제공 데이터 원본 컨트롤이 포함 되어 있습니다.](querying-data-with-the-sqldatasource-control-vb/_static/image1.gif)

**그림 1**: ASP.NET 2.0에는 5 가지 기본 제공 데이터 원본 컨트롤이 포함 되어 있습니다.

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>ObjectDataSource 및 SqlDataSource 비교

개념적으로 ObjectDataSource 컨트롤과 SqlDataSource 컨트롤은 단순히 데이터에 대 한 프록시입니다. ObjectDataSource를 사용 하 여 [데이터 표시](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) 에 설명 된 것 처럼 objectdatasource에는 데이터를 제공 하는 개체 형식 및 내부 개체 형식에서 데이터를 선택, 삽입, 업데이트 및 삭제 하기 위해 호출할 메서드를 나타내는 속성이 있습니다. ObjectDataSource 속성이 구성 되 면 GridView, DetailsView 또는 DataList와 같은 데이터 웹 컨트롤을 컨트롤에 바인딩할 수 있습니다. 이때 ObjectDataSource s `Select()`, `Insert()`, `Delete()`및 `Update()` 메서드를 사용 하 여 기본 아키텍처와 상호 작용할 수 있습니다.

SqlDataSource는 동일한 기능을 제공 하지만 개체 라이브러리가 아닌 관계형 데이터베이스에 대해 작동 합니다. SqlDataSource를 사용 하 여 데이터를 삽입, 업데이트, 삭제 및 검색 하기 위해 실행할 데이터베이스 연결 문자열과 임시 SQL 쿼리 또는 저장 프로시저를 지정 해야 합니다. SqlDataSource s `Select()`, `Insert()`, `Update()`및 `Delete()` 메서드를 호출 하면 지정 된 데이터베이스에 연결 하 여 적절 한 SQL 쿼리를 실행 합니다. 다음 다이어그램에 나와 있는 것 처럼 이러한 메서드는 데이터베이스에 연결 하 고 쿼리를 실행 하 고 결과를 반환 하는 grunt 작업을 수행 합니다.

![SqlDataSource는 데이터베이스에 대 한 프록시로 사용 됩니다.](querying-data-with-the-sqldatasource-control-vb/_static/image2.gif)

**그림 2**: SqlDataSource는 데이터베이스에 대 한 프록시로 사용 됩니다.

> [!NOTE]
> 이 자습서에서는 데이터베이스에서 데이터를 검색 하는 방법을 집중적으로 설명 합니다. SqlDataSource 컨트롤 자습서를 사용 하 여 [데이터 삽입, 업데이트 및 삭제](inserting-updating-and-deleting-data-with-the-sqldatasource-vb.md) 에서 삽입, 업데이트 및 삭제를 지원 하도록 sqldatasource를 구성 하는 방법을 살펴보겠습니다.

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 및 AccessDataSource 컨트롤

SqlDataSource 컨트롤 외에도 ASP.NET 2.0에는 AccessDataSource 컨트롤이 포함 되어 있습니다. 이러한 두 가지 다른 컨트롤은 ASP.NET 2.0의 새로운 개발자를 위한 것으로, AccessDataSource 컨트롤이 Microsoft SQL Server만 사용 하도록 디자인 된 SqlDataSource 컨트롤을 사용 하 여 Microsoft 액세스와 독점적으로 작동 하도록 설계 되었습니다. AccessDataSource은 Microsoft Access에서 특별히 작동 하도록 설계 되었지만, SqlDataSource 컨트롤은 .NET을 통해 액세스할 수 있는 *모든* 관계형 데이터베이스에서 작동 합니다. 여기에는 Microsoft SQL Server, Microsoft Access, Oracle, Informix, MySQL, PostgreSQL 등의 다양 한 OleDb 또는 ODBC 규격 데이터 저장소가 포함 됩니다.

AccessDataSource 및 SqlDataSource 컨트롤의 유일한 차이점은 데이터베이스 연결 정보를 지정 하는 방법입니다. AccessDataSource 컨트롤에는 Access 데이터베이스 파일에 대 한 파일 경로만 필요 합니다. 반면에 SqlDataSource에는 완전 한 연결 문자열이 필요 합니다.

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>1 단계: SqlDataSource 웹 페이지 만들기

SqlDataSource 컨트롤을 사용 하 여 데이터베이스 데이터를 직접 사용 하는 방법에 대 한 탐색을 시작 하기 전에 먼저이 자습서와 다음 3 개에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `SqlDataSource`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](querying-data-with-the-sqldatasource-control-vb/_static/image3.gif)

**그림 3**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `SqlDataSource` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](querying-data-with-the-sqldatasource-control-vb/_static/image5.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image4.gif)

**그림 4**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image6.gif))

마지막으로, 이러한 4 개의 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히 DataList 및 Repeater `<siteMapNode>`에 사용자 지정 단추를 추가한 후 다음 태그를 추가 합니다.

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample1.sql)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 자습서 편집, 삽입 및 삭제를 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 SqlDataSource 자습서에 대 한 항목이 포함 되어 있습니다.](querying-data-with-the-sqldatasource-control-vb/_static/image7.gif)

**그림 5**: 이제 사이트 맵에 SqlDataSource 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>2 단계: SqlDataSource 컨트롤 추가 및 구성

먼저 `SqlDataSource` 폴더에서 `Querying.aspx` 페이지를 열고 디자인 뷰로 전환 합니다. SqlDataSource 컨트롤을 도구 상자에서 디자이너로 끌고 `ID`를 `ProductsDataSource`로 설정 합니다. ObjectDataSource와 마찬가지로 SqlDataSource는 렌더링 된 출력을 생성 하지 않으므로 디자인 화면에 회색 상자로 표시 됩니다. SqlDataSource를 구성 하려면 SqlDataSource s 스마트 태그에서 데이터 원본 구성 링크를 클릭 합니다.

![SqlDataSource s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image8.gif)

**그림 6**: SqlDataSource의 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다.

이렇게 하면 SqlDataSource 컨트롤의 데이터 소스 구성 마법사가 열립니다. 마법사의 단계는 ObjectDataSource 제어와 다르지만 최종 목표는 데이터 원본을 통해 데이터를 검색, 삽입, 업데이트 및 삭제 하는 방법에 대 한 세부 정보를 제공 하는 것과 같습니다. SqlDataSource의 경우 사용할 기본 데이터베이스를 지정 하 고 임시 SQL 문이나 저장 프로시저를 제공 해야 합니다.

첫 번째 마법사 단계에서는 데이터베이스를 묻는 메시지를 표시 합니다. 드롭다운 목록에는 웹 응용 프로그램 `App_Data` 폴더에 있는 데이터베이스와 서버 탐색기의 데이터 연결 노드에 추가 된 데이터베이스가 포함 됩니다. `App_Data` 폴더의 `NORTHWIND.MDF` 데이터베이스에 대 한 연결 문자열을 프로젝트 `Web.config` 파일에 이미 추가 했으므로 드롭다운 목록에는 `NORTHWINDConnectionString`해당 연결 문자열에 대 한 참조가 포함 되어 있습니다. 드롭다운 목록에서이 항목을 선택 하 고 다음을 클릭 합니다.

![드롭다운 목록에서 NORTHWINDConnectionString를 선택 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image9.gif)

**그림 7**: 드롭다운 목록에서 `NORTHWINDConnectionString` 선택

데이터베이스를 선택 하면 마법사에서 데이터를 반환 하는 쿼리를 요청 합니다. 반환할 테이블이 나 뷰의 열을 지정 하거나 사용자 지정 SQL 문을 입력 하거나 저장 프로시저를 지정할 수 있습니다. 사용자 지정 SQL 문 또는 저장 프로시저 지정 및 테이블에서 열 지정 또는 보기 라디오 단추를 통해이 선택 사이를 전환할 수 있습니다.

> [!NOTE]
> 이 첫 번째 예에서는 테이블 또는 뷰에서 열 지정 옵션을 사용 합니다. 이 자습서의 뒷부분에서 마법사로 돌아가 사용자 지정 SQL 문 또는 저장 프로시저 지정 옵션을 탐색 합니다.

그림 8에서는 테이블 또는 뷰에서 열 지정 라디오 단추를 선택할 때 Select 문 구성 화면을 보여 줍니다. 드롭다운 목록에는 Northwind 데이터베이스에 있는 테이블 및 뷰 집합이 포함 되어 있으며,이 목록에는 선택한 테이블 또는 뷰 s 열이 아래에 있는 확인란 목록에 표시 됩니다. 이 예에서는 s를 사용 하 여 `Products` 테이블에서 `ProductID`, `ProductName`및 `UnitPrice` 열을 반환 합니다. 그림 8에 나와 있는 것 처럼 이러한 항목을 선택 하면 마법사에서 결과 SQL 문을 `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`표시 합니다.

![Products 테이블에서 데이터 반환](querying-data-with-the-sqldatasource-control-vb/_static/image10.gif)

**그림 8**: `Products` 테이블에서 데이터 반환

마법사에서 `Products` 테이블의 `ProductID`, `ProductName`및 `UnitPrice` 열을 반환 하도록 구성한 후에는 다음 단추를 클릭 합니다. 이 마지막 화면에서는 이전 단계에서 구성 된 쿼리 결과를 검토할 수 있는 기회를 제공 합니다. 쿼리 테스트 단추를 클릭 하면 구성 된 `SELECT` 문이 실행 되 고 결과가 표에 표시 됩니다.

![쿼리 테스트 단추를 클릭 하 여 선택 쿼리를 검토 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image11.gif)

**그림 9**: 쿼리 테스트 단추를 클릭 하 `SELECT` 쿼리를 검토 합니다.

마법사를 완료하려면 마침을 클릭합니다.

ObjectDataSource와 마찬가지로, SqlDataSource 마법사는 컨트롤 속성 ( [`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx) 및 [`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx) 속성)에 값을 할당 하기만 합니다. 마법사를 완료 한 후에는 SqlDataSource 컨트롤의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample2.aspx)]

`ConnectionString` 속성은 데이터베이스에 연결 하는 방법에 대 한 정보를 제공 합니다. 이 속성에는 하드 코드 된 전체 연결 문자열 값을 할당 하거나 `Web.config`연결 문자열을 가리킬 수 있습니다. Web.config에서 연결 문자열 값을 참조 하려면 `<%$ expressionPrefix:expressionValue %>`구문을 사용 합니다. 일반적으로 *Expressionprefix* 는 ConnectionStrings이 고 *expressionprefix* 는 `Web.config` [`<connectionStrings>` 섹션](https://msdn.microsoft.com/library/bf7sd233.aspx)에 있는 연결 문자열의 이름입니다. 그러나 구문을 사용 하 여 리소스 파일에서 `<appSettings>` 요소나 콘텐츠를 참조할 수 있습니다. 이 구문에 대 한 자세한 내용은 [ASP.NET 식 개요](https://msdn.microsoft.com/library/d5bd1tad.aspx) 를 참조 하세요.

`SelectCommand` 속성은 데이터를 반환 하기 위해 실행할 임시 SQL 문이나 저장 프로시저를 지정 합니다.

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 SqlDataSource에 바인딩

SqlDataSource가 구성 되 면 GridView 또는 DetailsView과 같은 데이터 웹 컨트롤에 바인딩될 수 있습니다. 이 자습서에서는 s를 GridView에 표시 합니다. 도구 상자에서 GridView를 페이지로 끌어온 다음 GridView의 스마트 태그에 있는 드롭다운 목록에서 데이터 원본을 선택 하 여 `ProductsDataSource` SqlDataSource에 바인딩합니다.

[GridView를 추가 ![SqlDataSource 컨트롤에 바인딩](querying-data-with-the-sqldatasource-control-vb/_static/image13.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image12.gif)

**그림 10**: GridView를 추가 하 고 SqlDataSource 컨트롤에 바인딩 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image14.gif))

GridView s 스마트 태그의 드롭다운 목록에서 SqlDataSource 컨트롤을 선택 하면 Visual Studio에서 데이터 소스 컨트롤에서 반환 하는 각 열에 대해 BoundField 또는 CheckBoxField를 GridView에 자동으로 추가 합니다. SqlDataSource는 `UnitPrice` `ProductName``ProductID`3 개의 데이터베이스 열을 반환 하므로 GridView에는 세 개의 필드가 있습니다.

잠시 후 GridView s BoundFields를 구성 합니다. `ProductName` field s `HeaderText` 속성을 Product Name으로 변경 하 고 `UnitPrice` 필드를 Price로 변경 합니다. 또한 `UnitPrice` 필드의 서식을 통화로 지정 합니다. 이러한 수정 작업을 수행한 후 GridView의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample3.aspx)]

브라우저를 통해이 페이지를 방문 하세요. 그림 11에 나와 있는 것 처럼 GridView는 각 제품 `ProductID`, `ProductName`및 `UnitPrice` 값을 나열 합니다.

[GridView ![각 제품의 ProductID, ProductName 및 UnitPrice 값을 표시 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image16.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image15.gif)

**그림 11**: GridView는 각 제품 `ProductID`, `ProductName`및 `UnitPrice` 값을 표시 합니다 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image17.gif)).

페이지를 방문한 후 GridView는 해당 데이터 소스 컨트롤 `Select()` 메서드를 호출 합니다. ObjectDataSource 컨트롤을 사용 하는 경우 `ProductsBLL` 클래스 `GetProducts()` 메서드 라고 합니다. 그러나 SqlDataSource를 사용 하는 경우 `Select()` 메서드는 지정 된 데이터베이스에 대 한 연결을 설정 하 고 `SelectCommand` (이 예에서는`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`)를 발급 합니다. SqlDataSource는 GridView가 반환 하는 결과를 반환 합니다. 그러면 gridview에서 반환 된 각 데이터베이스 레코드에 대 한 행을 만듭니다.

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>기본 제공 데이터 웹 컨트롤 기능 및 SqlDataSource 컨트롤

일반적으로 데이터 웹 컨트롤에 내재 된 기능 (페이징, 정렬, 편집, 삭제, 삽입 등)은 데이터 웹 컨트롤에만 적용 되며 사용 되는 데이터 소스 컨트롤에는 종속 되지 않습니다. 즉, GridView는 ObjectDataSource 또는 SqlDataSource에 바인딩되어 있는지 여부에 관계 없이 기본 제공 페이징, 정렬, 편집 및 삭제를 활용할 수 있습니다. 그러나 특정 데이터 웹 컨트롤 기능은 사용 하는 데이터 소스 컨트롤이 나 데이터 소스 컨트롤의 구성에 따라 구분 됩니다.

예를 들어 [많은 양의 데이터를 효율적으로 페이징](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-vb.md) 하는 자습서에서는 기본적으로 데이터 웹 컨트롤에 대 한 페이징 논리가 기본 데이터 원본에서 *모든* 레코드를 반환 하는 방법에 대해 설명 했습니다. 그러면 현재 페이지 인덱스와 페이지당 표시할 레코드 수에 해당 하는 레코드의 naively 해당 하위 집합만 표시 됩니다. 이 모델은 충분히 큰 결과 집합을 페이징할 때 매우 비효율적입니다. 다행히 ObjectDataSource는 표시할 레코드의 정확한 하위 집합만 반환 하는 사용자 지정 페이징을 지원 하도록 구성할 수 있습니다. 그러나 SqlDataSource 컨트롤에는 사용자 지정 페이징을 구현 하기 위한 속성이 없습니다.

페이징 및 정렬이 있는 또 다른 미묘한는 SqlDataSource와 함께 발생 합니다. 기본적으로 SqlDataSource에서 반환 된 데이터는 GridView를 통해 페이징 하거나 정렬할 수 있습니다. 이를 보여 주려면 `Querying.aspx`의 GridView s 스마트 태그에서 페이징 사용 및 정렬 사용 옵션을 선택 하 고 예상 대로 작동 하는지 확인 합니다.

SqlDataSource가 데이터베이스 데이터를 느슨하게 형식화 된 데이터 집합으로 검색 하기 때문에 정렬 및 페이징이 작동 합니다. 쿼리에서 반환 된 레코드의 총 수는 데이터 집합에서 페이징을 구현 하는 데 필수적인 부분을 이것이 winmd 수 있습니다. 또한 데이터 집합의 결과는 DataView를 통해 정렬할 수 있습니다. 이러한 기능은 GridView에서 페이징 또는 정렬 된 데이터를 요청할 때 SqlDataSource에서 자동으로 사용 됩니다.

SqlDataSource는 [`DataSourceMode` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx) 을 `DataSet` (기본값)에서 `DataReader`로 변경 하 여 데이터 집합 대신 DataReader를 반환 하도록 구성할 수 있습니다. Datareader를 예상 하는 기존 코드에 SqlDataSource를 전달 하는 경우 DataReader를 사용 하는 것이 좋습니다. 또한 DataReaders는 데이터 집합 보다 훨씬 더 간단한 개체 이기 때문에 더 나은 성능을 제공 합니다. 그러나 이러한 변경을 수행 하는 경우에는 SqlDataSource가 쿼리에 의해 반환 된 레코드 수를 확인할 수 없고 DataReader에서 반환 된 데이터를 정렬 하는 기술을 제공 하지 않기 때문에 데이터 웹 컨트롤이 정렬과 페이지를 모두 사용 하지 못합니다.

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>4 단계: 사용자 지정 SQL 문 또는 저장 프로시저 사용

SqlDataSource 컨트롤을 구성 하는 경우 데이터를 반환 하는 데 사용 되는 쿼리는 두 가지 방법 중 하나를 사용 하 여 사용자 지정 SQL 문 또는 저장 프로시저 또는 기존 테이블 또는 뷰의 열로 지정할 수 있습니다. 2 단계에서는 `Products` 테이블에서 열을 선택 하는 것을 검토 했습니다. 사용자 지정 SQL 문을 사용 하 여 살펴보겠습니다.

`Querying.aspx` 페이지에 다른 GridView 컨트롤을 추가 하 고 스마트 태그의 드롭다운 목록에서 새 데이터 소스를 만들도록 선택 합니다. 그런 다음 데이터베이스에서 데이터를 끌어올 것임을 지정 합니다. 이렇게 하면 새 SqlDataSource 컨트롤이 생성 됩니다. 컨트롤의 이름을 `ProductsWithCategoryInfoDataSource`합니다.

![ProductsWithCategoryInfoDataSource 라는 새 SqlDataSource 컨트롤을 만듭니다.](querying-data-with-the-sqldatasource-control-vb/_static/image18.gif)

**그림 12**: `ProductsWithCategoryInfoDataSource` 라는 새 SqlDataSource 컨트롤 만들기

다음 화면에서는 데이터베이스를 지정 하 라는 메시지를 표시 합니다. 그림 7에 나와 있는 것 처럼 드롭다운 목록에서 `NORTHWINDConnectionString`을 선택 하 고 다음을 클릭 합니다. Select 문 구성 화면에서 사용자 지정 SQL 문 또는 저장 프로시저 지정 라디오 단추를 선택 하 고 다음을 클릭 합니다. 그러면 선택, 업데이트, 삽입 및 삭제 레이블이 지정 된 탭을 제공 하는 사용자 지정 문 또는 저장 프로시저 정의 화면이 표시 됩니다. 각 탭에서 텍스트 상자에 사용자 지정 SQL 문을 입력 하거나 드롭다운 목록에서 저장 프로시저를 선택할 수 있습니다. 이 자습서에서는 사용자 지정 SQL 문 입력을 살펴보겠습니다. 다음 자습서에는 저장 프로시저를 사용 하는 예가 포함 되어 있습니다.

![사용자 지정 SQL 문을 입력 하거나 저장 프로시저를 선택 하십시오.](querying-data-with-the-sqldatasource-control-vb/_static/image19.gif)

**그림 13**: 사용자 지정 SQL 문 입력 또는 저장 프로시저 선택

사용자 지정 SQL 문은 텍스트 상자에 직접 입력 하거나 쿼리 작성기 단추를 클릭 하 여 그래픽으로 생성할 수 있습니다. 쿼리 작성기 또는 텍스트 상자에서 다음 쿼리를 사용 하 여 `JOIN` 테이블에서 제품 `CategoryName`를 검색 하는 `Categories`를 사용 하 여 `Products` 테이블에서 `ProductID` 및 `ProductName` 필드를 반환 합니다.

[!code-sql[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample4.sql)]

![쿼리 작성기를 사용 하 여 쿼리를 그래픽으로 생성할 수 있습니다.](querying-data-with-the-sqldatasource-control-vb/_static/image20.gif)

**그림 14**: 쿼리 작성기를 사용 하 여 쿼리를 그래픽으로 생성할 수 있습니다.

쿼리를 지정한 후 다음을 클릭 하 여 쿼리 테스트 화면으로 이동 합니다. 마침을 클릭 하 여 SqlDataSource 마법사를 완료 합니다.

마법사를 완료 한 후 GridView에는 쿼리에서 반환 된 `ProductID`, `ProductName`및 `CategoryName` 열을 표시 하 고 다음과 같은 선언 태그를 표시 하는 세 개의 BoundFields 추가 됩니다.

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-vb/samples/sample5.aspx)]

[GridView ![각 제품의 ID, 이름 및 연결 된 범주 이름을 표시 합니다.](querying-data-with-the-sqldatasource-control-vb/_static/image22.gif)](querying-data-with-the-sqldatasource-control-vb/_static/image21.gif)

**그림 15**: GridView는 각 제품의 ID, 이름 및 연결 된 범주 이름을 표시 합니다 ([전체 크기 이미지를 보려면 클릭](querying-data-with-the-sqldatasource-control-vb/_static/image23.gif)).

## <a name="summary"></a>요약

이 자습서에서는 SqlDataSource 컨트롤을 사용 하 여 데이터를 쿼리하고 표시 하는 방법을 살펴보았습니다. ObjectDataSource와 마찬가지로, SqlDataSource는 프록시 역할을 하 여 데이터에 액세스 하는 선언적 방법을 제공 합니다. 해당 속성은 연결할 데이터베이스와 실행할 SQL `SELECT` 쿼리를 지정 합니다. 속성 창 또는 데이터 원본 구성 마법사를 사용 하 여 지정할 수 있습니다.

이 자습서에서 검사 한 `SELECT` 쿼리 예제는 지정 된 쿼리의 모든 레코드를 반환 했습니다. 그러나 SqlDataSource 컨트롤에는 해당 값을 프로그래밍 방식으로 할당 하거나 지정 된 소스에서 자동으로 가져오는 매개 변수가 있는 `WHERE` 절이 포함 될 수 있습니다. 다음 자습서에서 매개 변수가 있는 쿼리를 만들고 사용 하는 방법을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [관계형 데이터베이스 데이터 액세스](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 컨트롤 개요](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 빠른 시작 자습서: SqlDataSource 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 요소](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [데이터베이스 연결 문자열 참조](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 김소미 Connery, Bernadette Leigh 및 David Suru입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)
> [다음](using-parameterized-queries-with-the-sqldatasource-vb.md)
