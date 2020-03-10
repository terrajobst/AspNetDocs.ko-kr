---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
title: 파일 업로드 중C#() | Microsoft Docs
author: rick-anderson
description: '사용자가 웹 사이트 (예: Word 또는 PDF 문서)에 이진 파일을 업로드할 수 있도록 하는 방법에 대해 알아봅니다.'
ms.author: riande
ms.date: 03/27/2007
ms.assetid: b381b1da-feb3-4776-bc1b-75db53eb90ab
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
msc.type: authoredcontent
ms.openlocfilehash: 4e3e32a829de386a681504c8d5d61dd258b8b2e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441695"
---
# <a name="uploading-files-c"></a>파일 업로드(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_CS.exe) 또는 [PDF 다운로드](uploading-files-cs/_static/datatutorial54cs1.pdf)

> 사용자가 파일 시스템 또는 데이터베이스에 저장 될 수 있는 웹 사이트에 사용자가 Word 또는 PDF 문서와 같은 이진 파일을 업로드할 수 있도록 하는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

지금까지 검토 한 모든 자습서는 텍스트 데이터를 사용 하 여 독점적으로 작업 했습니다. 그러나 많은 응용 프로그램에는 텍스트와 이진 데이터를 모두 캡처하는 데이터 모델이 있습니다. 온라인에 연결 된 사이트를 사용 하면 사용자가 그림을 업로드 하 여 프로필에 연결할 수 있습니다. 채용 웹 사이트에서 사용자가 Microsoft Word 또는 PDF 문서로 이력서를 업로드할 수 있습니다.

이진 데이터를 사용 하면 새로운 챌린지 집합이 추가 됩니다. 응용 프로그램에서 이진 데이터를 저장 하는 방법을 결정 해야 합니다. 사용자가 컴퓨터에서 파일을 업로드할 수 있도록 새 레코드를 삽입 하는 데 사용 되는 인터페이스를 업데이트 해야 하며, 레코드의 연결 된 이진 데이터를 다운로드 하는 방법을 표시 하거나 제공 하기 위해 추가 단계를 수행 해야 합니다. 이 자습서 및 다음 세 가지는 이러한 문제를 장애물 하는 방법을 살펴보겠습니다. 이 자습서의 끝 부분에서는 사진 및 PDF 브로슈어를 각 범주와 연결 하는 완전 한 기능을 갖춘 응용 프로그램을 빌드 했습니다. 이 특정 자습서에서는 이진 데이터를 저장 하는 다양 한 기술을 살펴보고 사용자가 자신의 컴퓨터에서 파일을 업로드 하 고 웹 서버 s 파일 시스템에 저장 하도록 설정 하는 방법을 살펴봅니다.

> [!NOTE]
> 응용 프로그램 데이터 모델의 일부인 이진 데이터는 [BLOB](http://en.wikipedia.org/wiki/Binary_large_object)(Binary Large OBject)의 머리글자어 라고도 합니다. 이러한 자습서에서는 BLOB 이라는 용어는 동의어 이지만 용어 이진 데이터를 사용 하도록 선택 했습니다.

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>1 단계: 이진 데이터 웹 페이지 작업 만들기

이진 데이터에 대 한 지원 추가와 관련 된 문제를 살펴보기 전에 먼저이 자습서와 다음 3 개에 필요한 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어 보겠습니다. `BinaryData`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![이진 데이터 관련 자습서에 대 한 ASP.NET 페이지 추가](uploading-files-cs/_static/image1.gif)

**그림 1**: 이진 데이터 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `BinaryData` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](uploading-files-cs/_static/image2.gif)](uploading-files-cs/_static/image1.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image2.png))

마지막으로, 이러한 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히 GridView `<siteMapNode>`을 향상 한 후 다음 태그를 추가 합니다.

[!code-xml[Main](uploading-files-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 이진 데이터 작업 자습서에 대 한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 이진 데이터 사용 자습서에 대 한 항목이 포함 되어 있습니다.](uploading-files-cs/_static/image3.gif)

**그림 3**: 이제 사이트 맵에 이진 데이터 사용 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>2 단계: 이진 데이터를 저장할 위치 결정

응용 프로그램 데이터 모델과 연결 된 이진 데이터는 웹 서버 파일 시스템에서 데이터베이스에 저장 된 파일에 대 한 참조를 사용 하 여 두 위치 중 하나에 저장 될 수 있습니다. 또는 데이터베이스 자체 내에서 직접 (그림 4 참조). 각 접근 방식에는 고유한 장점 및 단점 집합이 있으며,이에 대 한 자세한 논의는 유용 합니다.

[이진 데이터를 파일 시스템에 저장 하거나 데이터베이스에 직접 저장할 수 ![.](uploading-files-cs/_static/image4.gif)](uploading-files-cs/_static/image3.png)

**그림 4**: 이진 데이터를 파일 시스템에 저장 하거나 데이터베이스에 직접 저장할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image4.png)).

Northwind 데이터베이스를 확장 하 여 각 제품에 그림을 연결 한다고 가정 합니다. 한 가지 옵션은 이러한 이미지 파일을 웹 서버의 파일 시스템에 저장 하 고 `Products` 테이블에 경로를 기록 하는 것입니다. 이 방법을 사용 하는 경우 `varchar(200)`형식의 `Products` 테이블에 `ImagePath` 열을 추가 합니다. 사용자가 Chai에 대 한 그림을 업로드 한 경우 해당 그림은 웹 서버의 파일 `~/Images/Tea.jpg`시스템에 저장 될 수 있습니다. 여기서 `~`는 응용 프로그램의 실제 경로를 나타냅니다. 즉, 웹 사이트가 실제 경로 `C:\Websites\Northwind\`를 기반으로 하는 경우 `~/Images/Tea.jpg` `C:\Websites\Northwind\Images\Tea.jpg`와 동일 합니다. 이미지 파일을 업로드 한 후에는 해당 `ImagePath` 열이 새 이미지의 경로를 참조 하도록 `Products` 테이블에서 Chai 레코드를 업데이트 합니다. 모든 제품 이미지가 응용 프로그램의 `Images` 폴더에 배치 되도록 결정 한 경우 `~/Images/Tea.jpg` 또는 `Tea.jpg`를 사용할 수 있습니다.

이진 데이터를 파일 시스템에 저장 하는 경우의 주요 이점은 다음과 같습니다.

- **구현 용이성** , 데이터베이스에 직접 저장 된 이진 데이터를 저장 하 고 검색 하는 것은 파일 시스템을 통해 데이터로 작업 하는 경우 보다 더 많은 코드가 포함 됩니다. 또한 사용자가 이진 데이터를 보거나 다운로드 하려면 해당 데이터에 대 한 URL을 제공 해야 합니다. 데이터가 웹 서버의 파일 시스템에 있는 경우 URL은 간단 합니다. 그러나 데이터가 데이터베이스에 저장 되어 있는 경우에는 데이터베이스에서 데이터를 검색 하 고 반환 하는 웹 페이지를 만들어야 합니다.
- **이진 데이터에** 대 한 광범위 한 액세스 데이터베이스에서 데이터를 끌어올 수 없는 다른 서비스 또는 응용 프로그램에서 이진 데이터에 액세스할 수 있어야 합니다. 예를 들어, 각 제품과 연결 된 이미지를 [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol)를 통해 사용자가 사용할 수 있도록 해야 할 수도 있습니다 .이 경우 파일 시스템에 이진 데이터를 저장 하려고 합니다.
- **성능** 이진 데이터가 파일 시스템에 저장 된 경우 데이터베이스 서버와 웹 서버 간의 수요 및 네트워크 정체는 이진 데이터가 데이터베이스 내에 직접 저장 된 경우 보다 낮습니다.

이진 데이터를 파일 시스템에 저장 하는 경우의 주요 단점은 데이터베이스에서 데이터를 분리는 것입니다. `Products` 테이블에서 레코드를 삭제 하면 웹 서버의 파일 시스템에 있는 관련 파일이 자동으로 삭제 되지 않습니다. 파일을 삭제 하려면 추가 코드를 작성 해야 합니다. 그렇지 않으면 파일 시스템은 사용 하지 않는 분리 된 파일로 복잡해 집니다. 또한 데이터베이스를 백업할 때에는 연결 된 이진 데이터를 파일 시스템에도 백업 해야 합니다. 다른 사이트 또는 서버로 데이터베이스를 이동 하면 비슷한 문제가 발생 합니다.

또는 `varbinary`형식의 열을 만들어 Microsoft SQL Server 2005 데이터베이스에 이진 데이터를 직접 저장할 수 있습니다. 다른 가변 길이 데이터 형식과 마찬가지로이 열에 보유할 수 있는 이진 데이터의 최대 길이를 지정할 수 있습니다. 예를 들어 최대 5000 바이트를 예약 하려면 `varbinary(5000)`을 사용 합니다. `varbinary(MAX)` 최대 저장소 크기 (약 2gb)를 허용 합니다.

이진 데이터를 데이터베이스에 직접 저장 하는 경우의 주요 이점은 이진 데이터와 데이터베이스 레코드를 긴밀 하 게 결합 하는 것입니다. 이렇게 하면 데이터베이스 관리 작업 (예: 백업 또는 데이터베이스를 다른 사이트 또는 서버로 이동)이 매우 간단해 집니다. 또한 레코드를 삭제 하면 해당 하는 이진 데이터가 자동으로 삭제 됩니다. 또한 데이터베이스에 이진 데이터를 저장 하면 더 미묘한 이점이 있습니다. 자세히 토론 하려면 [ASP.NET 2.0을 사용 하 여 데이터베이스에 직접 이진 파일 저장](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx) 을 참조 하세요.

> [!NOTE]
> Microsoft SQL Server 2000 이전 버전에서 `varbinary` 데이터 형식의 최대 제한은 8000 바이트입니다. 최대 2gb의 이진 데이터를 저장 하려면 [`image` 데이터 형식을](https://msdn.microsoft.com/library/ms187993.aspx) 대신 사용 해야 합니다. 그러나 SQL Server 2005에 `MAX` 추가 되어 `image` 데이터 형식은 더 이상 사용 되지 않습니다. 이전 버전과의 호환성을 위해 계속 지원 되지만, `image` 데이터 형식이 이후 버전의 SQL Server에서 제거 될 것 이라고 발표 했습니다.

이전 데이터 모델로 작업 하는 경우 `image` 데이터 형식이 표시 될 수 있습니다. Northwind 데이터베이스 s `Categories` 테이블에는 범주에 대 한 이미지 파일의 이진 데이터를 저장 하는 데 사용할 수 있는 `Picture` 열이 있습니다. Northwind 데이터베이스의 루트는 Microsoft Access와 이전 버전의 SQL Server 이므로이 열은 `image`유형입니다.

이 자습서 및 다음 세 가지 방법에서는 두 가지 방법을 모두 사용 합니다. `Categories` 테이블에는 범주에 대 한 이미지의 이진 내용을 저장 하기 위한 `Picture` 열이 이미 있습니다. `BrochurePath`추가 열을 추가 하 여 인쇄 품질, 범주에 대 한 세련 된 개요를 제공 하는 데 사용할 수 있는 웹 서버 파일 시스템에 PDF 경로를 저장 합니다.

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>3 단계:`Categories`테이블에`BrochurePath`열 추가

현재 Categories 테이블에는 `CategoryID`, `CategoryName`, `Description`및 `Picture`의 4 개 열만 있습니다. 이러한 필드 외에도 범주 브로슈어 (있는 경우)를 가리키는 새 필드를 추가 해야 합니다. 이 열을 추가 하려면 서버 탐색기로 이동 하 여 테이블로 드릴 다운 하 고 `Categories` 테이블을 마우스 오른쪽 단추로 클릭 한 다음 테이블 정의 열기를 선택 합니다 (그림 5 참조). 서버 탐색기 표시 되지 않으면 보기 메뉴에서 서버 탐색기 옵션을 선택 하거나 Ctrl + Alt + S를 누르면 됩니다.

`BrochurePath` 라는 `Categories` 테이블에 새 `varchar(200)` 열을 추가 하 고 `NULL`을 허용 하 고 저장 아이콘을 클릭 하거나 Ctrl + S를 누릅니다.

[BrochurePath 열을 Categories 테이블에 추가 ![](uploading-files-cs/_static/image5.gif)](uploading-files-cs/_static/image5.png)

**그림 5**: `Categories` 테이블에 `BrochurePath` 열 추가 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image6.png))

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>4 단계:`Picture`및`BrochurePath`열을 사용 하도록 아키텍처 업데이트

DAL (데이터 액세스 계층)의 `CategoriesDataTable`에는 현재 `CategoryID`, `CategoryName`, `Description`및 `NumberOfProducts`정의 된 4 개의 `DataColumn` 정의 되어 있습니다. [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-cs.md) 자습서에서 원래이 DataTable을 디자인할 때 `CategoriesDataTable`에는 처음 3 개의 열만 있습니다. `NumberOfProducts` 열은 [세부 정보 DataList 자습서를 사용 하 여 마스터 레코드의 글머리 기호 목록을 사용 하 여 마스터/세부](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 정보에 추가 되었습니다.

*데이터 액세스 계층 만들기*에 설명 된 대로 형식화 된 데이터 집합의 datatable는 비즈니스 개체를 구성 합니다. Tableadapter는 데이터베이스와 통신 하 고 비즈니스 개체를 쿼리 결과로 채우는 일을 담당 합니다. `CategoriesDataTable`는 다음과 같은 세 가지 데이터 검색 방법이 있는 `CategoriesTableAdapter`채워집니다.

- `GetCategories()` TableAdapter 주 쿼리를 실행 하 고 `Categories` 테이블의 모든 레코드에 대 한 `CategoryID`, `CategoryName`및 `Description` 필드를 반환 합니다. 기본 쿼리는 자동 생성 `Insert` 및 `Update` 메서드에서 사용 됩니다.
- `GetCategoryByCategoryID(categoryID)`은 `CategoryID`가 *categoryID*와 동일한 범주의 `CategoryID`, `CategoryName`및 `Description` 필드를 반환 합니다.
- `GetCategoriesAndNumberOfProducts()`-`Categories` 테이블의 모든 레코드에 대 한 `CategoryID`, `CategoryName`및 `Description` 필드를 반환 합니다. 또한는 하위 쿼리를 사용 하 여 각 범주와 관련 된 제품 수를 반환 합니다.

이러한 쿼리는 `Categories` 테이블 s `Picture` 또는 `BrochurePath` 열을 반환 하지 않습니다. 및는 이러한 필드에 대해 `DataColumn` `CategoriesDataTable` 제공 하지 않습니다. 그림 및 `BrochurePath` 속성을 사용 하려면 먼저 `CategoriesDataTable`에 추가한 다음 이러한 열을 반환 하도록 `CategoriesTableAdapter` 클래스를 업데이트 해야 합니다.

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>`Picture`및`BrochurePath``DataColumn` 추가

이러한 두 열을 `CategoriesDataTable`에 추가 하 여 시작 합니다. `CategoriesDataTable` s 헤더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 추가를 선택한 다음 열 옵션을 선택 합니다. 이렇게 하면 `Column1`라는 DataTable에 새 `DataColumn` 만들어집니다. 이 열의 이름을 `Picture`로 바꿉니다. 속성 창에서 `DataColumn` s `DataType` 속성을 `System.Byte[]`로 설정 합니다 .이 속성은 드롭다운 목록에서 옵션이 아닙니다. 입력 해야 합니다.

[데이터 형식이 system.string [] 인 DataColumn 이름이 지정 된 그림을 만듭니다 ![](uploading-files-cs/_static/image6.gif)](uploading-files-cs/_static/image7.png)

**그림 6**: `DataType` `System.Byte[]` 인 `Picture` 라는 `DataColumn` 만들기 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image8.png))

DataTable에 다른 `DataColumn`를 추가 하 고 기본 `DataType` 값 (`System.String`)을 사용 하 여 `BrochurePath` 이름을 지정 합니다.

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>TableAdapter의`Picture`및`BrochurePath`값 반환

이러한 두 `DataColumn` s `CategoriesDataTable`에 추가 되 면 `CategoriesTableAdapter`를 업데이트할 준비가 된 것입니다. 주 TableAdapter 쿼리에서 이러한 열 값을 모두 반환 했을 수 있지만이는 `GetCategories()` 메서드가 호출 될 때마다 이진 데이터를 다시 가져옵니다. 대신, `BrochurePath` 다시 가져와서 특정 범주 `Picture` 열을 반환 하는 추가 데이터 검색 메서드를 만들도록 주 TableAdapter 쿼리를 업데이트 해 보겠습니다.

주 TableAdapter 쿼리를 업데이트 하려면 `CategoriesTableAdapter` s 헤더를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 구성 옵션을 선택 합니다. 이렇게 하면 몇 가지 이전 자습서에서 살펴본 테이블 어댑터 구성 마법사가 나타납니다. `BrochurePath`를 다시 가져오려면 쿼리를 업데이트 하 고 [마침]을 클릭 하십시오.

[SELECT 문에서 열 목록을 업데이트 ![BrochurePath도 반환 됩니다.](uploading-files-cs/_static/image7.gif)](uploading-files-cs/_static/image9.png)

**그림 7**: `BrochurePath`을 반환 하도록 `SELECT` 문에서 열 목록 업데이트 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image10.png))

TableAdapter에 대해 임시 SQL 문을 사용 하는 경우 주 쿼리에서 열 목록을 업데이트 하면 TableAdapter의 모든 `SELECT` 쿼리 메서드에 대 한 열 목록이 업데이트 됩니다. 즉, `GetCategoryByCategoryID(categoryID)` 메서드가 `BrochurePath` 열을 반환 하도록 업데이트 되었으므로 의도 한 것이 될 수 있습니다. 그러나 `GetCategoriesAndNumberOfProducts()` 메서드에서 열 목록을 업데이트 하 여 각 범주에 대 한 제품 수를 반환 하는 하위 쿼리를 제거 합니다. 따라서이 메서드 `SELECT` 쿼리를 업데이트 해야 합니다. `GetCategoriesAndNumberOfProducts()` 메서드를 마우스 오른쪽 단추로 클릭 하 고 구성을 선택한 다음 `SELECT` 쿼리를 원래 값으로 되돌립니다.

[!code-sql[Main](uploading-files-cs/samples/sample2.sql)]

다음으로, 특정 범주 `Picture` 열 값을 반환 하는 새 TableAdapter 메서드를 만듭니다. `CategoriesTableAdapter` s 헤더를 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가 옵션을 선택 하 여 TableAdapter 쿼리 구성 마법사를 시작 합니다. 이 마법사의 첫 번째 단계에서는 임시 SQL 문, 새 저장 프로시저 또는 기존 항목을 사용 하 여 데이터를 쿼리해야 하는지 묻는 메시지를 표시 합니다. SQL 문 사용을 선택 하 고 다음을 클릭 합니다. 행을 반환할 것 이므로 두 번째 단계에서 행을 반환 하는 옵션을 선택 합니다.

[![SQL 문 사용 옵션을 선택 합니다.](uploading-files-cs/_static/image8.gif)](uploading-files-cs/_static/image11.png)

**그림 8**: SQL 문 사용 옵션 선택 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image12.png))

[![쿼리는 Categories 테이블에서 레코드를 반환 하므로 행을 반환 하는 SELECT를 선택 합니다.](uploading-files-cs/_static/image9.gif)](uploading-files-cs/_static/image13.png)

**그림 9**: 쿼리에서 Categories 테이블의 레코드를 반환 하기 때문에 행을 반환 하는 선택 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image14.png))을 선택 합니다.

세 번째 단계에서 다음 SQL 쿼리를 입력 하 고 다음을 클릭 합니다.

[!code-sql[Main](uploading-files-cs/samples/sample3.sql)]

마지막 단계는 새 메서드의 이름을 선택 하는 것입니다. `FillCategoryWithBinaryDataByCategoryID` 및 `GetCategoryWithBinaryDataByCategoryID`를 사용 하 여 DataTable을 채우고 DataTable 패턴을 반환 합니다. 마침을 클릭하여 마법사를 완료합니다.

[![TableAdapter의 메서드 이름을 선택 합니다.](uploading-files-cs/_static/image10.gif)](uploading-files-cs/_static/image15.png)

**그림 10**: TableAdapter의 메서드 이름 선택 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image16.png))

> [!NOTE]
> 테이블 어댑터 쿼리 구성 마법사를 완료 한 후 새 명령 텍스트에서 주 쿼리의 스키마와 다른 스키마가 있는 데이터를 반환 한다는 것을 알리는 대화 상자가 표시 될 수 있습니다. 간단히 말해서, 마법사는 TableAdapter의 주 쿼리 `GetCategories()` 방금 만든 스키마와 다른 스키마를 반환 한다는 것을 주목 합니다. 하지만이 메시지는 무시 해도 됩니다.

또한 임시 SQL 문을 사용 하 고 마법사를 사용 하 여 나중에 TableAdapter 주 쿼리를 변경 하는 경우 주 쿼리의 해당 열만 포함 하도록 `GetCategoryWithBinaryDataByCategoryID` 메서드 `SELECT` 문 열 목록을 수정 합니다. 즉, 쿼리에서 `Picture` 열을 제거 합니다.)를 고려해 야 합니다. `Picture` 열을 반환 하도록 열 목록을 수동으로 업데이트 해야 합니다 .이 단계에서는 이전에 `GetCategoriesAndNumberOfProducts()` 메서드를 사용 했을 때와 비슷합니다.

`CategoriesDataTable`에 두 개의 `DataColumn` s를 추가 하 고 `GetCategoryWithBinaryDataByCategoryID` 메서드를 `CategoriesTableAdapter`에 추가한 후에는 형식화 된 데이터 집합 디자이너의 이러한 클래스가 그림 11의 스크린샷 처럼 보입니다.

![데이터 집합 디자이너에는 새 열과 메서드가 포함 되어 있습니다.](uploading-files-cs/_static/image11.gif)

**그림 11**: 새 열과 메서드를 포함 하는 데이터 집합 디자이너

## <a name="updating-the-business-logic-layer-bll"></a>BLL (비즈니스 논리 계층) 업데이트

DAL이 업데이트 되 면 새 `CategoriesTableAdapter` 메서드에 대 한 메서드를 포함 하도록 BLL (비즈니스 논리 계층)을 보강 하는 것만 남았습니다. `CategoriesBLL` 클래스에 다음 메서드를 추가합니다.

[!code-csharp[Main](uploading-files-cs/samples/sample4.cs)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>5 단계: 클라이언트에서 웹 서버로 파일 업로드

이진 데이터를 수집 하는 경우이 데이터는 최종 사용자가 제공 하는 경우가 많습니다. 이 정보를 캡처하려면 사용자가 자신의 컴퓨터에서 웹 서버로 파일을 업로드할 수 있어야 합니다. 그런 다음 업로드 된 데이터를 데이터 모델과 통합 해야 합니다 .이 경우 파일을 웹 서버의 파일 시스템에 저장 하 고 데이터베이스의 파일에 경로를 추가 하거나 이진 콘텐츠를 데이터베이스에 직접 쓸 수 있습니다. 이 단계에서는 사용자가 자신의 컴퓨터에서 서버로 파일을 업로드할 수 있도록 허용 하는 방법을 살펴보겠습니다. 다음 자습서에서는 업로드 된 파일을 데이터 모델과 통합 하는 데 주의를 기울여야 합니다.

ASP.NET 2.0 s new [FileUpload 웹 컨트롤](https://msdn.microsoft.com/library/ms227677(VS.80).aspx) 은 사용자가 자신의 컴퓨터에서 웹 서버로 파일을 보낼 수 있는 메커니즘을 제공 합니다. FileUpload 컨트롤은 `type` 특성이 file로 설정 된 `<input>` 요소로 렌더링 합니다. 브라우저는 찾아보기 단추를 사용 하 여 텍스트 상자로 표시 합니다. 찾아보기 단추를 클릭 하면 사용자가 파일을 선택할 수 있는 대화 상자가 나타납니다. 양식이 다시 게시 되 면 선택한 파일의 내용이 다시 게시와 함께 전송 됩니다. 서버 쪽에서 업로드 된 파일에 대 한 정보는 FileUpload 컨트롤의 속성을 통해 액세스할 수 있습니다.

파일 업로드를 시연 하려면 `BinaryData` 폴더에서 `FileUpload.aspx` 페이지를 열고, 도구 상자에서 FileUpload 컨트롤을 디자이너로 끌고, 컨트롤의 `ID` 속성을 `UploadTest`로 설정 합니다. 그런 다음, 해당 `ID`을 설정 하 고 `Text` 속성을 설정 하 여 선택한 파일을 `UploadButton` 및 업로드 하는 단추 웹 컨트롤을 추가 합니다. 마지막으로 단추 아래에 Label 웹 컨트롤을 놓고 `Text` 속성을 지우고 `ID` 속성을 `UploadDetails`로 설정 합니다.

[FileUpload 컨트롤을 ASP.NET 페이지에 추가 ![](uploading-files-cs/_static/image12.gif)](uploading-files-cs/_static/image17.png)

**그림 12**: ASP.NET 페이지에 FileUpload 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image18.png))

그림 13에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 찾아보기 단추를 클릭 하면 파일 선택 대화 상자가 표시 되어 사용자가 컴퓨터에서 파일을 선택할 수 있습니다. 파일이 선택 되 면 선택한 파일 업로드 단추를 클릭 하면 선택한 파일의 이진 콘텐츠를 웹 서버로 전송 하는 포스트백이 발생 합니다.

[![사용자가 컴퓨터에서 서버로 업로드할 파일을 선택할 수 있습니다.](uploading-files-cs/_static/image13.gif)](uploading-files-cs/_static/image19.png)

**그림 13**: 사용자는 컴퓨터에서 서버로 업로드할 파일을 선택할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image20.png)).

다시 게시 하는 경우 업로드 된 파일을 파일 시스템에 저장 하거나, 해당 이진 데이터를 스트림을 통해 직접 작업을 수행할 수 있습니다. 이 예에서는 `~/Brochures` 폴더를 만들고 업로드 된 파일을 저장 합니다. 먼저 `Brochures` 폴더를 루트 디렉터리의 하위 폴더로 사이트에 추가 합니다. 다음으로 `UploadButton` s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](uploading-files-cs/samples/sample5.cs)]

FileUpload 컨트롤은 업로드 된 데이터를 사용 하기 위한 다양 한 속성을 제공 합니다. 예를 들어 [`HasFile` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx) 은 파일이 사용자에 의해 업로드 되었는지 여부를 나타내며 [`FileBytes` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx) 은 업로드 된 이진 데이터에 대 한 액세스를 바이트 배열로 제공 합니다. `Click` 이벤트 처리기는 파일이 업로드 되었는지 확인 하 여 시작 합니다. 파일이 업로드 된 경우에는 업로드 된 파일의 이름, 크기 (바이트) 및 해당 콘텐츠 형식에 레이블이 표시 됩니다.

> [!NOTE]
> 사용자가 파일을 업로드 하도록 하려면 `HasFile` 속성을 확인 하 고 `false`되는 경우 경고를 표시 하거나 대신 [Requiredfieldvalidator 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx) 을 사용할 수 있습니다.

FileUpload s `SaveAs(filePath)`는 업로드 된 파일을 지정 된 파일 *경로*에 저장 합니다. *filePath* 는 *가상* *경로* (`/Brochures/SomeFile.pdf`)가 아닌 *실제 경로* (`C:\Websites\Brochures\SomeFile.pdf`) 여야 합니다. [`Server.MapPath(virtPath)` 메서드](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx) 는 가상 경로를 사용 하 여 해당 하는 실제 경로를 반환 합니다. 여기에서 가상 경로는 `~/Brochures/fileName`됩니다. 여기서 *fileName* 은 업로드 된 파일의 이름입니다. 가상 및 실제 경로와 `Server.MapPath`사용에 대 한 자세한 내용은 node.js [사용](http://www.4guysfromrolla.com/webtech/121799-1.shtml) 을 참조 하세요.

`Click` 이벤트 처리기를 완료 한 후 잠시 브라우저에서 페이지를 테스트 합니다. 찾아보기 단추를 클릭 하 고 하드 드라이브에서 파일을 선택한 다음 선택한 파일 업로드 단추를 클릭 합니다. 다시 게시 하면 선택한 파일의 내용이 웹 서버로 전송 됩니다. 그러면 해당 파일을 `~/Brochures` 폴더에 저장 하기 전에 파일에 대 한 정보가 표시 됩니다. 파일을 업로드 한 후에 Visual Studio로 돌아가서 솔루션 탐색기에서 새로 고침 단추를 클릭 합니다. 방금 업로드 한 파일이 ~/Hs 폴더에 표시 됩니다.

[EvolutionValley 파일이 웹 서버에 업로드 ![](uploading-files-cs/_static/image14.gif)](uploading-files-cs/_static/image21.png)

**그림 14**: `EvolutionValley.jpg` 파일을 웹 서버에 업로드 했습니다 ([전체 크기 이미지를 보려면 클릭](uploading-files-cs/_static/image22.png)).

![EvolutionValley가 ~/Hl 폴더에 저장 되었습니다.](uploading-files-cs/_static/image15.gif)

**그림 15**: `EvolutionValley.jpg` `~/Brochures` 폴더에 저장 됨

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>업로드 된 파일을 파일 시스템에 저장 하는 경우의 미묘한

웹 서버의 파일 시스템에 업로드 파일을 저장할 때 해결 해야 하는 여러 가지 미묘한 내용이 있습니다. 먼저 보안 문제가 있습니다. 파일 시스템에 파일을 저장 하려면 ASP.NET 페이지를 실행 하는 보안 컨텍스트에 쓰기 권한이 있어야 합니다. ASP.NET Development 웹 서버는 현재 사용자 계정의 컨텍스트에서 실행 됩니다. Microsoft s 인터넷 정보 서비스 (IIS)를 웹 서버로 사용 하는 경우 보안 컨텍스트는 IIS 및 해당 구성의 버전에 따라 달라 집니다.

파일을 파일 시스템에 저장 하는 또 다른 문제는 파일의 이름을 지정 하는 것입니다. 현재 페이지에는 클라이언트 컴퓨터의 파일과 동일한 이름을 사용 하 여 업로드 된 모든 파일이 `~/Brochures` 디렉터리에 저장 됩니다. 사용자 A가 `Brochure.pdf`이름의 브로슈어를 업로드 하는 경우이 파일은 `~/Brochure/Brochure.pdf`으로 저장 됩니다. 그러나 나중에 사용자 B가 동일한 파일 이름 (`Brochure.pdf`)을 가진 다른 브로슈어 파일을 업로드 하는 경우는 어떻게 되나요? 이제 코드를 사용 하 여 user A s 파일은 사용자 B s 업로드로 덮어쓰여집니다.

파일 이름 충돌을 해결 하는 방법에는 여러 가지가 있습니다. 한 가지 옵션은 이름이 같은 파일이 이미 있는 경우 파일을 업로드 하는 것을 금지 하는 것입니다. 이 방법을 사용 하면 사용자 B가 `Brochure.pdf`파일을 업로드 하려고 할 때 시스템은 파일을 저장 하지 않고 대신 사용자 B에 게 파일 이름을 바꾸고 다시 시도 하 라는 메시지를 표시 합니다. 또 다른 방법은 고유한 파일 이름을 사용 하 여 파일을 저장 하는 것입니다 .이는 [guid (globally unique identifier](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) ) 또는 해당 데이터베이스 레코드의 기본 키 열에 있는 값이 될 수 있습니다 (업로드가 데이터 모델의 특정 행과 연결 된 것으로 가정). 다음 자습서에서는 이러한 옵션에 대해 자세히 설명 합니다.

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>매우 많은 양의 이진 데이터와 관련 된 과제

이러한 자습서에서는 캡처된 이진 데이터의 크기가 적당 하다 고 가정 합니다. 몇 메가바이트 이상의 이진 데이터 파일에 대 한 작업에는 이러한 자습서의 범위를 벗어나는 새로운 과제가 도입 됩니다. 예를 들어, ASP.NET는 `Web.config`의 [`<httpRuntime>` 요소](https://msdn.microsoft.com/library/e1f13641.aspx) 를 통해 구성할 수 있지만 기본적으로는 4mb 이상의 업로드를 거부 합니다. IIS는 자체 파일 업로드 크기 제한도 적용 합니다. 자세한 내용은 [IIS 업로드 파일 크기](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) 를 참조 하십시오. 또한 많은 파일을 업로드 하는 데 걸리는 시간이 기본 110 초를 초과 하면 ASP.NET가 요청을 대기 합니다. 또한 많은 파일을 사용할 때 발생 하는 메모리 및 성능 문제가 있습니다.

FileUpload 컨트롤은 대량 파일 업로드에 적합 하지 않습니다. 파일의 콘텐츠를 서버에 게시 하면 최종 사용자가 업로드가 진행 되 고 있는지 확인 하지 않고 patiently 대기 해야 합니다. 몇 초 안에 업로드할 수 있는 작은 파일을 처리할 경우에는 문제가 되지 않지만 업로드 하는 데 몇 분이 걸릴 수 있는 큰 파일을 처리할 때 문제가 될 수 있습니다. 큰 업로드를 처리 하는 데 더 적합 한 다양 한 타사 파일 업로드 컨트롤이 있으며 이러한 공급 업체 대부분은 진행률 표시기와 훨씬 더 세련 된 사용자 환경을 제공 하는 ActiveX 업로드 관리자를 제공 합니다.

응용 프로그램에서 규모가 많은 파일을 처리 해야 하는 경우 문제를 자세히 조사 하 고 특정 요구 사항에 적합 한 솔루션을 찾아야 합니다.

## <a name="summary"></a>요약

이진 데이터를 캡처해야 하는 응용 프로그램을 빌드하면 많은 과제가 발생 합니다. 이 자습서에서는 처음 두 가지를 살펴보았습니다. 이진 데이터를 저장할 위치를 결정 하 고 사용자가 웹 페이지를 통해 이진 콘텐츠를 업로드할 수 있습니다. 다음 세 가지 자습서를 통해 업로드 된 데이터를 데이터베이스의 레코드와 연결 하는 방법 뿐만 아니라 텍스트 데이터 필드와 함께 이진 데이터를 표시 하는 방법을 확인할 수 있습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [대량 값 데이터 형식 사용](https://msdn.microsoft.com/library/ms178158.aspx)
- [FileUpload 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [ASP.NET 2.0 FileUpload Server 컨트롤](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [파일 업로드의 어두운 쪽](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Teresa Murphy 및 Bernadette Leigh입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](displaying-binary-data-in-the-data-web-controls-cs.md)
