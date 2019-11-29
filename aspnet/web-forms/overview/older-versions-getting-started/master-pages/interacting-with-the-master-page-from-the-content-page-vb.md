---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
title: 콘텐츠 페이지에서 마스터 페이지와 상호 작용 (VB) | Microsoft Docs
author: rick-anderson
description: 콘텐츠 페이지의 코드에서 마스터 페이지의 메서드를 호출 하 고 속성을 설정 하는 방법을 검토 합니다.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 081fe010-ba0f-4e7d-b4ba-774840b601c2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-vb
msc.type: authoredcontent
ms.openlocfilehash: fe1f7b80b26ff25c1ce744e4f823e3fb35eea074
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577420"
---
# <a name="interacting-with-the-master-page-from-the-content-page-vb"></a>콘텐츠 페이지에서 마스터 페이지와 상호 작용(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_VB.pdf)

> 콘텐츠 페이지의 코드에서 마스터 페이지의 메서드를 호출 하 고 속성을 설정 하는 방법을 검토 합니다.

## <a name="introduction"></a>소개

지난 5 가지 자습서를 진행 하면서 마스터 페이지를 만들고, 콘텐츠 영역을 정의 하 고, ASP.NET 페이지를 마스터 페이지에 바인딩하고, 페이지 관련 콘텐츠를 정의 하는 방법을 살펴보았습니다. 방문자가 특정 콘텐츠 페이지를 요청 하면 콘텐츠 및 마스터 페이지의 태그는 런타임에 퓨즈 되어 통합 된 컨트롤 계층 구조가 렌더링 됩니다. 따라서 마스터 페이지와 해당 콘텐츠 페이지 중 하나가 상호 작용할 수 있는 한 가지 방법이 이미 표시 되어 있습니다. 콘텐츠 페이지는 마스터 페이지의 ContentPlaceHolder 컨트롤에 transfuse 태그를 출력 합니다.

아직 검토 해야 하는 것은 마스터 페이지와 콘텐츠 페이지가 프로그래밍 방식으로 상호 작용 하는 방법입니다. 콘텐츠 페이지는 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 태그를 정의 하는 것 외에도 마스터 페이지의 공용 속성에 값을 할당 하 고 해당 public 메서드를 호출할 수 있습니다. 마찬가지로 마스터 페이지는 해당 콘텐츠 페이지와 상호 작용할 수 있습니다. 마스터 페이지와 콘텐츠 페이지의 프로그래밍 방식 상호 작용은 선언적 마크업 간의 상호 작용 보다 일반적이 지 않지만 이러한 프로그래밍 조작이 필요한 많은 시나리오가 있습니다.

이 자습서에서는 콘텐츠 페이지가 프로그래밍 방식으로 마스터 페이지와 상호 작용 하는 방법을 살펴봅니다. 다음 자습서에서는 마스터 페이지가 유사한 콘텐츠 페이지와 상호 작용 하는 방법을 살펴보겠습니다.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>콘텐츠 페이지와 해당 마스터 페이지 간의 프로그래밍 방식 상호 작용 예제

페이지의 특정 영역을 페이지 단위로 구성 해야 하는 경우 ContentPlaceHolder 컨트롤을 사용 합니다. 하지만 대부분의 페이지에서 특정 출력을 내보내야 하는 상황에 대 한 자세한 내용을 보여 주기 위해 몇 페이지의 페이지를 사용자 지정 해야 하나요? [*여러 ContentPlaceHolders 표시자 및 기본 콘텐츠*](multiple-contentplaceholders-and-default-content-vb.md) 자습서에서 검사 한 예는 각 페이지에 로그인 인터페이스를 표시 하는 것을 포함 합니다. 대부분의 페이지에는 로그인 인터페이스가 포함 되어야 하지만 주 로그인 페이지 (`Login.aspx`)와 같은 소수의 페이지에 대해서는 표시 되지 않습니다. 계정 만들기 페이지 그리고 인증 된 사용자만 액세스할 수 있는 다른 페이지로 이동할 수 있습니다. [*여러 ContentPlaceHolders 표시자 및 기본 콘텐츠*](multiple-contentplaceholders-and-default-content-vb.md) 자습서에서는 마스터 페이지에서 ContentPlaceHolder의 기본 콘텐츠를 정의 하는 방법과 기본 콘텐츠가 필요 하지 않은 페이지에서 해당 콘텐츠를 재정의 하는 방법을 살펴보았습니다.

또 다른 옵션은 로그인 인터페이스를 표시 하거나 숨길지 여부를 나타내는 마스터 페이지 내에서 공용 속성 또는 메서드를 만드는 것입니다. 예를 들어 마스터 페이지에는 해당 값이 마스터 페이지에서 로그인 컨트롤의 `Visible` 속성을 설정 하는 데 사용 된 `ShowLoginUI` 이라는 public 속성이 포함 될 수 있습니다. 로그인 사용자 인터페이스를 표시 하지 않아야 하는 콘텐츠 페이지에서 프로그래밍 방식으로 `ShowLoginUI` 속성을 `False`로 설정할 수 있습니다.

콘텐츠 페이지에서 일부 작업이 의심할 된 후 마스터 페이지에 표시 되는 데이터를 새로 고쳐야 할 때 콘텐츠 및 마스터 페이지 상호 작용의 가장 일반적인 예가 발생 합니다. 특정 데이터베이스 테이블에서 가장 최근에 추가 된 5 개의 레코드를 표시 하는 GridView가 포함 된 마스터 페이지와 해당 내용 페이지 중 하나에 새 레코드를 동일한 테이블에 추가 하는 인터페이스가 포함 되어 있다고 가정 합니다.

사용자가 페이지를 방문 하 여 새 레코드를 추가 하는 경우 마스터 페이지에 표시 되는 가장 최근에 추가 된 5 개의 레코드가 보입니다. 새 레코드의 열에 대 한 값을 입력 한 후 폼을 전송 합니다. 마스터 페이지의 GridView가 `EnableViewState` 속성을 True (기본값)로 설정 했다고 가정 하면 해당 콘텐츠는 뷰 상태에서 다시 로드 되며, 결과적으로 새 레코드가 데이터베이스에 추가 된 경우에도 5 개의 동일한 레코드가 표시 됩니다. 이로 인해 사용자가 혼동 될 수 있습니다.

> [!NOTE]
> GridView의 뷰 상태를 사용 하지 않도록 설정 하 여 다시 게시할 때마다 기본 데이터 원본에 다시 바인딩하기도 불구 하 고, 데이터가 datab에 새 레코드가 추가 되는 경우 보다 이전에 페이지 수명 주기에서 GridView에 바인딩되므로 방금 추가 된 레코드만 표시 되지 않습니다. ase.

이를 해결 하려면 방금 추가 된 레코드가 다시 게시 될 때 마스터 페이지의 GridView에 표시 되도록 하려면 새 레코드가 데이터베이스에 추가 된 *후* 에 해당 데이터 원본에 다시 바인딩하기 위해 GridView에 지시 해야 합니다. 이렇게 하려면 새 레코드를 추가 하기 위한 인터페이스 (및 해당 이벤트 처리기)가 콘텐츠 페이지에 있지만 새로 고쳐야 하는 GridView가 마스터 페이지에 있으므로 콘텐츠와 마스터 페이지 간의 상호 작용이 필요 합니다.

콘텐츠 페이지의 이벤트 처리기에서 마스터 페이지의 표시를 새로 고치는 것이 콘텐츠 및 마스터 페이지 상호 작용에 대 한 가장 일반적인 요구 사항 중 하나 이기 때문에이 항목을 자세히 살펴보겠습니다. 이 자습서에 대 한 다운로드에는 웹 사이트의 `App_Data` 폴더에 `NORTHWIND.MDF` 이라는 Microsoft SQL Server 2005 Express Edition 데이터베이스가 포함 되어 있습니다. Northwind 데이터베이스는 가상 회사인 Northwind Traders의 제품, 직원 및 판매 정보를 저장 합니다.

1 단계에서는 마스터 페이지에서 GridView에 가장 최근에 추가 된 5 개 제품을 표시 하는 과정을 안내 합니다. 2 단계에서는 새 제품을 추가 하기 위한 콘텐츠 페이지를 만듭니다. 3 단계에서는 마스터 페이지에서 공용 속성 및 메서드를 만드는 방법에 대해 설명 하 고, 4 단계에서는 콘텐츠 페이지에서 이러한 속성 및 메서드를 프로그래밍 방식으로 인터페이스 하는 방법을 보여 줍니다.

> [!NOTE]
> 이 자습서에서는 ASP.NET의 데이터로 작업 하는 구체적인 방법을 설명 하지 않습니다. 데이터를 표시 하는 마스터 페이지를 설정 하 고 데이터를 삽입 하는 내용 페이지를 설정 하는 단계가 완료 되었지만 아직 breezy. 데이터 표시 및 삽입, SqlDataSource 및 GridView 컨트롤 사용에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 판독값 섹션의 리소스를 참조 하세요.

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>1 단계: 마스터 페이지에서 가장 최근에 추가 된 5 개 제품 표시

Site.master 마스터 페이지를 열고 레이블과 GridView 컨트롤을 `leftContent` `<div>`에 추가 합니다. 레이블의 `Text` 속성을 지우고 `EnableViewState` 속성을 `False`로 설정 하 고 `ID` 속성을 `GridMessage`로 설정 합니다. GridView의 `ID` 속성을 `RecentProducts`로 설정 합니다. 그런 다음 디자이너에서 GridView의 스마트 태그를 확장 하 고 새 데이터 원본에 바인딩하려를 선택 합니다. 그러면 데이터 소스 구성 마법사가 시작 됩니다. `App_Data` 폴더의 Northwind 데이터베이스가 Microsoft SQL Server 데이터베이스 이므로를 선택 하 여 SqlDataSource를 만들도록 선택 합니다 (그림 1 참조). SqlDataSource의 이름을 `RecentProductsDataSource`로 합니다.

[![GridView를 RecentProductsDataSource 라는 SqlDataSource 컨트롤에 바인딩합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image1.png)

**그림 01**: GridView를 `RecentProductsDataSource` 이라는 SqlDataSource 컨트롤에 바인딩 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image3.png))

다음 단계에서는 연결할 데이터베이스를 지정 하 라는 메시지를 표시 합니다. 드롭다운 목록에서 `NORTHWIND.MDF` 데이터베이스 파일을 선택 하 고 다음을 클릭 합니다. 이 데이터베이스를 처음 사용 했기 때문에 마법사는 `Web.config`에 연결 문자열을 저장 하도록 제공 합니다. `NorthwindConnectionString`이름을 사용 하 여 연결 문자열을 저장 하도록 합니다.

[Northwind 데이터베이스에 연결 ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image4.png)

**그림 02**: Northwind 데이터베이스에 연결 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image6.png))

데이터 원본 구성 마법사는 데이터를 검색 하는 데 사용 되는 쿼리를 지정할 수 있는 두 가지 방법을 제공 합니다.

- 사용자 지정 SQL 문 또는 저장 프로시저 지정
- 테이블이 나 뷰를 선택 하 고 반환할 열을 지정 하 여

가장 최근에 추가 된 제품 5 개만 반환 하려고 하기 때문에 사용자 지정 SQL 문을 지정 해야 합니다. 다음 `SELECT` 쿼리를 사용 합니다.

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample1.sql)]

`TOP 5` 키워드는 쿼리에서 처음 5 개의 레코드만 반환 합니다. `Products` 테이블의 기본 키 `ProductID`는 `IDENTITY` 열로, 테이블에 추가 된 각 새 제품이 이전 항목 보다 더 큰 값을 갖게 됩니다. 따라서 `ProductID` 기준으로 결과를 내림차순으로 정렬 하면 가장 최근에 생성 된 제품으로 시작 하는 제품이 반환 됩니다.

[![가장 최근에 추가 된 5 개 제품을 반환 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image7.png)

**그림 03**: 가장 최근에 추가 된 5 개 제품 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image9.png))을 반환 합니다.

마법사를 완료 한 후 Visual Studio에서 GridView에 대해 두 개의 BoundFields을 생성 하 여 데이터베이스에서 반환 된 `ProductName` 및 `UnitPrice` 필드를 표시 합니다. 이 시점에서 마스터 페이지의 선언적 태그는 다음과 유사한 태그를 포함 해야 합니다.

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample2.aspx)]

여기에서 볼 수 있듯이 태그에는 레이블 웹 컨트롤 (`GridMessage`)이 포함 됩니다. GridView `RecentProducts`두 개의 BoundFields를 포함 합니다. 가장 최근에 추가 된 5 개 제품을 반환 하는 SqlDataSource 컨트롤입니다.

이 GridView가 만들어지고 SqlDataSource 컨트롤이 구성 된 상태에서 브라우저를 통해 웹 사이트를 방문 합니다. 그림 4와 같이 가장 최근에 추가 된 5 개 제품을 나열 하는 표가 왼쪽 아래에 표시 됩니다.

[GridView ![가장 최근에 추가 된 5 개 제품을 표시 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image10.png)

**그림 04**: GridView에서 가장 최근에 추가 된 5 개 제품 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image12.png))을 표시 합니다.

> [!NOTE]
> GridView의 모양을 자유롭게 정리 합니다. 표시 되는 `UnitPrice` 값의 서식을 통화로 지정 하 고 배경색 및 글꼴을 사용 하 여 표의 모양을 개선 하는 것이 몇 가지 제안 사항입니다.

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>2 단계: 새 제품을 추가 하는 콘텐츠 페이지 만들기

다음 작업은 사용자가 `Products` 테이블에 새 제품을 추가할 수 있는 콘텐츠 페이지를 만드는 것입니다. `AddProduct.aspx`이라는 `Admin` 폴더에 새 콘텐츠 페이지를 추가 하 고 `Site.master` 마스터 페이지에 바인딩해야 합니다. 그림 5는이 페이지가 웹 사이트에 추가 된 후의 솔루션 탐색기을 보여 줍니다.

[관리 폴더에 새 ASP.NET 페이지를 추가 ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image13.png)

**그림 05**: `Admin` 폴더에 새 ASP.NET 페이지 추가 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image15.png))

[*마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 자습서에서 명시적으로 설정 하지 않은 경우 페이지의 제목을 생성 한 `BasePage` 라는 사용자 지정 기본 페이지 클래스를 만들었습니다. `AddProduct.aspx` 페이지의 코드 숨김으로 클래스로 이동 하 여 `BasePage` (`System.Web.UI.Page`대신)에서 파생 되도록 합니다.

마지막으로이 단원에 대 한 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. 컨트롤 ID 명명 문제 단원에 대 한 `<siteMapNode>` 아래에 다음 태그를 추가 합니다.

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample3.xml)]

그림 6에 표시 된 것 처럼이 `<siteMapNode>` 요소 추가는 단원 목록에 반영 됩니다.

`AddProduct.aspx`로 돌아갑니다. `MainContent` ContentPlaceHolder에 대 한 콘텐츠 컨트롤에서 DetailsView 컨트롤을 추가 하 고 이름을 `NewProduct`으로 만듭니다. DetailsView를 `NewProductDataSource`라는 새 SqlDataSource 컨트롤에 바인딩합니다. 1 단계의 SqlDataSource와 마찬가지로 Northwind 데이터베이스를 사용 하 고 사용자 지정 SQL 문을 지정 하도록 마법사를 구성 합니다. DetailsView은 데이터베이스에 항목을 추가 하는 데 사용 되므로 `SELECT` 문과 `INSERT` 문을 모두 지정 해야 합니다. 다음 `SELECT` 쿼리를 사용 합니다.

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample4.sql)]

그런 다음 삽입 탭에서 다음 `INSERT` 문을 추가 합니다.

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample5.sql)]

마법사를 완료 한 후 DetailsView의 스마트 태그로 이동 하 여 "삽입 사용" 확인란을 선택 합니다. 그러면 `ShowInsertButton` 속성이 True로 설정 된 DetailsView에 CommandField가 추가 됩니다. 이 DetailsView은 데이터를 삽입 하는 용도로만 사용 되므로 DetailsView의 `DefaultMode` 속성을 `Insert`로 설정 합니다.

이것이 전부입니다! 이 페이지를 테스트해 보겠습니다. 브라우저를 통해 `AddProduct.aspx`를 방문 하 고 이름 및 가격을 입력 합니다 (그림 6 참조).

[데이터베이스에 새 제품을 추가 ![](interacting-with-the-master-page-from-the-content-page-vb/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image16.png)

**그림 06**: 데이터베이스에 새 제품 추가 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image18.png))

새 제품의 이름과 가격을 입력 한 후에 삽입 단추를 클릭 합니다. 이렇게 하면 양식이 다시 게시 됩니다. 다시 게시 시 SqlDataSource 컨트롤의 `INSERT` 문이 실행 됩니다. 두 매개 변수는 DetailsView의 두 TextBox 컨트롤에 사용자가 입력 한 값으로 채워집니다. 아쉽게도 삽입이 발생 한 시각적 피드백이 없습니다. 새 레코드가 추가 되었는지 확인 하는 메시지가 표시 되는 것이 좋습니다. 독자를 위한 연습으로 남겨 둡니다. 또한 DetailsView에서 새 레코드를 추가한 후 마스터 페이지의 GridView는 이전과 동일한 5 개의 레코드를 계속 표시 합니다. 여기에는 단순히 추가 된 레코드만 포함 되지 않습니다. 이후 단계에서이를 해결 하는 방법을 살펴보겠습니다.

> [!NOTE]
> 삽입에 성공한 시각적 피드백의 일부를 추가 하는 것 외에도, 유효성 검사를 포함 하도록 DetailsView의 삽입 인터페이스를 업데이트 하는 것이 좋습니다. 현재는 유효성 검사를 수행 하지 않습니다. 사용자가 "너무 비쌉니다"와 같이 `UnitPrice` 필드에 대해 잘못 된 값을 입력 하면 시스템에서 해당 문자열을 10 진수로 변환 하려고 할 때 다시 게시 시 예외가 throw 됩니다. 삽입 인터페이스를 사용자 지정 하는 방법에 대 한 자세한 내용은 my [data tutorial 시리즈 작업](../../data-access/index.md)에서 [ *데이터 수정 인터페이스 사용자 지정* 자습서](https://asp.net/learn/data-access/tutorial-20-vb.aspx) 를 참조 하세요.

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>3 단계: 마스터 페이지에서 공용 속성 및 메서드 만들기

1 단계에서는 마스터 페이지에서 GridView 위에 `GridMessage` 이라는 레이블 웹 컨트롤을 추가 했습니다. 이 레이블은 선택적으로 메시지를 표시 하기 위한 것입니다. 예를 들어 `Products` 테이블에 새 레코드를 추가한 후 "*ProductName* 이 데이터베이스에 추가 되었습니다." 라는 메시지를 표시할 수 있습니다. 마스터 페이지에서이 레이블에 대 한 텍스트를 하드 코딩 하는 대신 콘텐츠 페이지에서 메시지를 사용자 지정할 수 있습니다.

레이블 컨트롤은 마스터 페이지 내에서 보호 된 멤버 변수로 구현 되기 때문에 콘텐츠 페이지에서 직접 액세스할 수 없습니다. 콘텐츠 페이지에서 마스터 페이지 내의 레이블을 사용 하려면 (또는 마스터 페이지의 모든 웹 컨트롤) 마스터 페이지에서 웹 컨트롤을 노출 하거나 해당 속성 중 하나에 대 한 프록시 역할을 하는 공용 속성을 만들어야 합니다.  날짜. 마스터 페이지의 코드 뒤 클래스에 다음 구문을 추가 하 여 레이블의 `Text` 속성을 노출 합니다.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample6.vb)]

콘텐츠 페이지에서 `Products` 테이블에 새 레코드가 추가 되 면 마스터 페이지의 GridView `RecentProducts`를 기본 데이터 원본에 다시 바인딩해야 합니다. GridView를 다시 바인딩하려면 `DataBind` 메서드를 호출 합니다. 마스터 페이지의 GridView는 콘텐츠 페이지에서 프로그래밍 방식으로 액세스할 수 없으므로 마스터 페이지에서 공용 메서드를 만들어야 합니다 .이 메서드를 호출 하면 데이터를 GridView에 다시 바인딩합니다. 마스터 페이지의 코드 숨김이 클래스에 다음 메서드를 추가 합니다.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample7.vb)]

`GridMessageText` 속성 및 `RefreshRecentProductsGrid` 메서드를 사용 하면 모든 콘텐츠 페이지에서 `GridMessage` 레이블의 `Text` 속성 값을 프로그래밍 방식으로 설정 하거나 읽거나 데이터를 `RecentProducts` GridView로 다시 바인딩할 수 있습니다. 4 단계에서는 콘텐츠 페이지에서 마스터 페이지의 공용 속성 및 메서드에 액세스 하는 방법을 살펴봅니다.

> [!NOTE]
> 마스터 페이지의 속성 및 메서드를 `Public`으로 표시 하는 것을 잊지 마세요. 이러한 속성 및 메서드를 `Public`로 명시적으로 표시 하지 않는 경우에는 콘텐츠 페이지에서 액세스할 수 없습니다.

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>4 단계: 콘텐츠 페이지에서 마스터 페이지의 Public 멤버 호출

이제 마스터 페이지에 필요한 공용 속성 및 메서드가 있으므로 `AddProduct.aspx` 콘텐츠 페이지에서 이러한 속성 및 메서드를 호출할 준비가 되었습니다. 특히 새 제품이 데이터베이스에 추가 된 후에는 마스터 페이지의 `GridMessageText` 속성을 설정 하 고 해당 `RefreshRecentProductsGrid` 메서드를 호출 해야 합니다. 모든 ASP.NET 데이터 웹 컨트롤은 다양 한 작업을 완료 하기 전후에 이벤트를 발생 시킵니다 .이를 통해 페이지 개발자는 작업 전후에 일부 프로그래밍 작업을 쉽게 수행할 수 있습니다. 예를 들어 최종 사용자가 DetailsView의 삽입 단추를 클릭 하면 다시 게시 될 때 DetailsView은 삽입 워크플로를 시작 하기 전에 `ItemInserting` 이벤트를 발생 시킵니다. 그런 다음 데이터베이스에 레코드를 삽입 합니다. 다음에는 DetailsView에서 `ItemInserted` 이벤트를 발생 시킵니다. 따라서 새 제품이 추가 된 후 마스터 페이지로 작업 하려면 DetailsView의 `ItemInserted` 이벤트에 대 한 이벤트 처리기를 만듭니다.

콘텐츠 페이지에서 마스터 페이지와 프로그래밍 방식으로 상호 작용 하는 방법에는 두 가지가 있습니다.

- `Page.Master` 속성을 사용 하 여 느슨한 형식의 참조를 마스터 페이지에 반환 하거나
- `@MasterType` 지시어를 통해 페이지의 마스터 페이지 형식 또는 파일 경로를 지정 합니다. 그러면 `Master`라는 페이지에 강력한 형식의 속성이 자동으로 추가 됩니다.

두 가지 방법을 살펴보겠습니다.

### <a name="using-the-loosely-typedpagemasterproperty"></a>느슨하게 형식화 된`Page.Master`속성 사용

모든 ASP.NET 웹 페이지는 `System.Web.UI` 네임 스페이스에 있는 `Page` 클래스에서 파생 되어야 합니다. `Page` 클래스는 페이지의 마스터 페이지에 대 한 참조를 반환 하는 [`Master` 속성](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) 을 포함 합니다. 페이지에 마스터 페이지가 없으면 `Master` `Nothing`반환 됩니다.

`Master` 속성은 모든 마스터 페이지가 파생 되는 기본 유형인 `System.Web.UI` 네임 스페이스에도 있는 [`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) 형식의 개체를 반환 합니다. 따라서 웹 사이트의 마스터 페이지에 정의 된 공용 속성 또는 메서드를 사용 하려면 `Master` 속성에서 반환 된 `MasterPage` 개체를 적절 한 형식으로 캐스팅 해야 합니다. `Site.master`마스터 페이지 파일의 이름을 지정 했기 때문에 코드 숨김이 `Site`이름이 지정 되었습니다. 따라서 다음 코드는 `Page.Master` 속성을 `Site` 클래스의 인스턴스로 캐스팅 합니다.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample8.vb)]

이제 느슨하게 형식화 된 `Page.Master` 속성을 사이트 형식으로 캐스트 했으므로 사이트에 관련 된 속성 및 메서드를 참조할 수 있습니다. 그림 7에 표시 된 것 처럼 공용 속성 `GridMessageText` IntelliSense 드롭다운에 표시 됩니다.

[![IntelliSense는 마스터 페이지의 공용 속성 및 메서드를 표시 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image19.png)

**그림 07**: IntelliSense에서 마스터 페이지의 공용 속성 및 메서드 표시 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image21.png))

> [!NOTE]
> 마스터 페이지 파일 `MasterPage.master`의 이름을 지정 하는 경우 마스터 페이지의 코드 숨김이 클래스 이름이 `MasterPage`됩니다. `System.Web.UI.MasterPage` 형식에서 `MasterPage` 클래스로 캐스팅 하는 경우 모호한 코드가 발생할 수 있습니다. 간단히 말해 캐스팅할 형식을 정규화 해야 합니다. 웹 사이트 프로젝트 모델을 사용 하는 경우에는 다소 복잡할 수 있습니다. 마스터 페이지를 만들 때 `MasterPage.master`이 아닌 다른 이름으로 지정 하는 것이 좋습니다. 마스터 페이지에 대 한 강력한 형식의 참조를 만들 수도 있습니다.

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>`@MasterType`지시어를 사용 하 여 강력한 형식의 참조 만들기

자세히 살펴보면 ASP.NET 페이지의 코드 숨김이 partial 클래스 임을 확인할 수 있습니다 (클래스 정의에서 `Partial` 키워드를 참고). Partial 클래스는 및 Visual Basic C# with.NET Framework 2.0에 도입 되었으며, 간단히 말해서 클래스의 멤버가 여러 파일에 대해 정의 될 수 있도록 합니다. 예를 들어 코드를 포함 하는 클래스 파일 `AddProduct.aspx.vb`에는 페이지 개발자 인 코드 ()가 포함 되어 있습니다. 코드 외에도 ASP.NET 엔진은에서 선언적 태그를 페이지의 클래스 계층 구조로 변환 하는 속성 및 이벤트 처리기를 사용 하 여 별도의 클래스 파일을 자동으로 만듭니다.

ASP.NET 페이지를 방문할 때마다 발생 하는 자동 코드 생성은 몇 가지 흥미로운 유용한 가능성을 마련 하는 방법입니다. 마스터 페이지의 경우 ASP.NET 엔진에 콘텐츠 페이지에서 사용 중인 마스터 페이지를 알려 주는 경우이를 위해 강력한 형식의 `Master` 속성이 생성 됩니다.

ASP.NET 엔진에 콘텐츠 페이지의 마스터 페이지 유형을 알리기 위해 [`@MasterType` 지시문](https://msdn.microsoft.com/library/ms228274.aspx) 을 사용 합니다. `@MasterType` 지시어는 마스터 페이지의 형식 이름 또는 해당 파일 경로 중 하나를 사용할 수 있습니다. `AddProduct.aspx` 페이지에서 `Site.master` 마스터 페이지로 사용 하도록 지정 하려면 `AddProduct.aspx`맨 위에 다음 지시문을 추가 합니다.

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample9.aspx)]

이 지시문은 ASP.NET 엔진이 `Master`라는 속성을 통해 마스터 페이지에 강력한 형식의 참조를 추가 하도록 지시 합니다. `@MasterType` 지시문을 사용 하면 캐스팅 없이 `Master` 속성을 통해 `Site.master` 마스터 페이지의 public 속성 및 메서드를 직접 호출할 수 있습니다.

> [!NOTE]
> `@MasterType` 지시문을 생략 하면 `Page.Master` 및 `Master` 구문이 느슨하게 형식화 된 개체를 페이지의 마스터 페이지에 반환 합니다. `@MasterType` 지시문을 포함 하는 경우 `Master`는 지정 된 마스터 페이지에 대 한 강력한 형식의 참조를 반환 합니다. 그러나 `Page.Master`는 여전히 느슨하게 형식화 된 참조를 반환 합니다. 이 경우와 `@MasterType` 지시문이 포함 된 경우 `Master` 속성을 구성 하는 방법에 대 한 자세한 내용은 [ASP.NET 2.0에서](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)Allen의 블로그`@MasterType` 항목을 참조 하세요 [.](http://odetocode.com/blogs/scott/default.aspx)

### <a name="updating-the-master-page-after-adding-a-new-product"></a>새 제품을 추가한 후 마스터 페이지 업데이트

이제 콘텐츠 페이지에서 마스터 페이지의 공용 속성 및 메서드를 호출 하는 방법을 배웠으므로 새 제품을 추가한 후 마스터 페이지가 새로 고쳐질 수 있도록 `AddProduct.aspx` 페이지를 업데이트할 준비가 되었습니다. 4 단계를 시작할 때 DetailsView 컨트롤의 `ItemInserting` 이벤트에 대 한 이벤트 처리기를 만들었습니다 .이 이벤트는 새 제품이 데이터베이스에 추가 된 후 즉시 실행 됩니다. 해당 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-vb[Main](interacting-with-the-master-page-from-the-content-page-vb/samples/sample10.vb)]

위의 코드는 느슨하게 형식화 된 `Page.Master` 속성과 강력한 형식의 `Master` 속성을 모두 사용 합니다. `GridMessageText` 속성은 "*ProductName* 에 추가 ..."로 설정 되어 있습니다. `e.Values` 컬렉션을 통해 바로 추가 된 제품의 값에 액세스할 수 있습니다. 여기에서 볼 수 있듯이 방금 추가 된 `ProductName` 값은 `e.Values("ProductName")`를 통해 액세스 됩니다.

그림 8에서는 새 제품 (Scott의 음료수)이 데이터베이스에 추가 된 직후의 `AddProduct.aspx` 페이지를 보여 줍니다. 방금 추가 된 제품 이름은 마스터 페이지의 레이블에 표시 되 고 제품 및 가격을 포함 하도록 GridView가 새로 고쳐 졌는 지 확인 합니다.

[마스터 페이지의 레이블 및 GridView ![에 추가 된 제품을 표시 합니다.](interacting-with-the-master-page-from-the-content-page-vb/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-vb/_static/image22.png)

**그림 08**: 마스터 페이지의 레이블 및 GridView에서 추가 된 제품을 표시 합니다 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-master-page-from-the-content-page-vb/_static/image24.png)).

## <a name="summary"></a>요약

이상적으로는 마스터 페이지와 해당 콘텐츠 페이지가 서로 완전히 분리 되며 상호 작용 수준이 필요 하지 않습니다. 마스터 페이지 및 콘텐츠 페이지는 해당 목표를 염두에 두어야 하지만 콘텐츠 페이지가 마스터 페이지와 상호 작용 해야 하는 여러 가지 일반적인 시나리오가 있습니다. 가장 일반적인 이유 중 하나는 콘텐츠 페이지에서 의심할 하는 작업에 따라 마스터 페이지 표시의 특정 부분을 업데이트 하는 것과 관련 된 것입니다.

좋은 소식은 콘텐츠 페이지를 프로그래밍 방식으로 마스터 페이지와 상호 작용 하는 것이 비교적 간단 하다는 것입니다. 먼저 콘텐츠 페이지에서 호출 해야 하는 기능을 캡슐화 하는 공용 속성 또는 메서드를 마스터 페이지에 만듭니다. 그런 다음 콘텐츠 페이지에서 느슨하게 형식화 된 `Page.Master` 속성을 통해 마스터 페이지의 속성 및 메서드에 액세스 하거나 `@MasterType` 지시어를 사용 하 여 마스터 페이지에 대 한 강력한 형식의 참조를 만듭니다.

다음 자습서에서는 마스터 페이지를 프로그래밍 방식으로 해당 콘텐츠 페이지와 상호 작용 하는 방법을 살펴봅니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [ASP.NET 마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 2.0의 `@MasterType`](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [콘텐츠 및 마스터 페이지 간에 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터 작업](../../data-access/index.md)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](control-id-naming-in-content-pages-vb.md)
> [다음](interacting-with-the-content-page-from-the-master-page-vb.md)
