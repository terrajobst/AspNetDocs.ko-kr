---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
title: 마스터 페이지 및 ASP.NET AJAX (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션을 설명 합니다. Scriptmanagerproxy 컨트롤용 클래스를 사용 하 여를 찾습니다. 다양 한 JS 파일이 로드 되는 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0ee9318c-29bb-4d58-b1dc-94e575b8ae10
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
msc.type: authoredcontent
ms.openlocfilehash: 7be4ff422b91321ff83ed1f1c731c9a0bfe768f1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637767"
---
# <a name="master-pages-and-aspnet-ajax-vb"></a>마스터 페이지 및 ASP.NET AJAX(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_VB.pdf)

> ASP.NET AJAX 및 마스터 페이지를 사용 하기 위한 옵션을 설명 합니다. Scriptmanagerproxy 컨트롤용 클래스를 사용 하 여를 찾습니다. 마스터 페이지 또는 콘텐츠 페이지에서 ScriptManager를 사용 하는지에 따라 다양 한 JS 파일이 로드 되는 방법에 대해 설명 합니다.

## <a name="introduction"></a>소개

지난 몇 년간 많은 개발자가 AJAX 사용 웹 응용 프로그램을 개발 했습니다. AJAX 사용 웹 사이트는 다양 한 관련 웹 기술을 사용 하 여 응답성이 뛰어난 사용자 환경을 제공 합니다. AJAX를 사용 하는 ASP.NET 응용 프로그램을 만드는 것은 Microsoft의 ASP.NET AJAX 프레임 워크 덕분에 놀라울 만큼 쉽습니다. ASP.NET AJAX는 ASP.NET 3.5 및 Visual Studio 2008에 기본 제공 됩니다. ASP.NET 2.0 응용 프로그램에 대 한 별도의 다운로드로도 제공 됩니다.

ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 페이지를 빌드하는 경우 프레임 워크를 사용 하는 모든 페이지 및 각 페이지에 정확히 하나의 ScriptManager 컨트롤을 추가 해야 합니다. 이름에서 알 수 있듯이 ScriptManager는 AJAX 사용 웹 페이지에서 사용 되는 클라이언트 쪽 스크립트를 관리 합니다. 최소한 ScriptManager는 ASP.NET AJAX 클라이언트 라이브러리를 구성을 JavaScript 파일을 다운로드 하도록 브라우저에 지시 하는 HTML을 내보냅니다. 또한 사용자 지정 JavaScript 파일, 스크립트 사용 웹 서비스 및 사용자 지정 응용 프로그램 서비스 기능을 등록 하는 데 사용할 수 있습니다.

사이트에서 마스터 페이지 (예:)를 사용 하는 경우 모든 단일 콘텐츠 페이지에 ScriptManager 컨트롤을 추가 하지 않아도 됩니다. 대신, 마스터 페이지에 ScriptManager 컨트롤을 추가할 수 있습니다. 이 자습서에서는 마스터 페이지에 ScriptManager 컨트롤을 추가 하는 방법을 보여 줍니다. 또한 Scriptmanagerproxy 컨트롤용 컨트롤을 사용 하 여 특정 콘텐츠 페이지에서 사용자 지정 스크립트 및 스크립트 서비스를 등록 하는 방법을 살펴봅니다.

> [!NOTE]
> 이 자습서에서는 ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 응용 프로그램 디자인 또는 빌드를 탐색 하지 않습니다. AJAX를 사용 하는 방법에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 정보 섹션에 나열 된 리소스 뿐만 아니라 ASP.NET AJAX 비디오 및 자습서를 참조 하세요.

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>ScriptManager 컨트롤에서 내보낸 태그 검사

ScriptManager 컨트롤은 ASP.NET AJAX 클라이언트 라이브러리를 구성을 JavaScript 파일을 다운로드 하도록 브라우저에 지시 하는 태그를 내보냅니다. 또한이 라이브러리를 초기화 하는 페이지에 약간의 인라인 JavaScript를 추가 합니다. 다음 태그는 ScriptManager 컨트롤을 포함 하는 페이지의 렌더링 된 출력에 추가 되는 내용을 보여 줍니다.

[!code-html[Main](master-pages-and-asp-net-ajax-vb/samples/sample1.html)]

`<script src="url"></script>` 태그는 브라우저에 *url*에서 JavaScript 파일을 다운로드 하 고 실행 하도록 지시 합니다. ScriptManager는 이러한 태그 3 개를 내보냅니다. 하나는 파일 `WebResource.axd`를 참조 하 고 다른 두 파일은 파일 `ScriptResource.axd`참조 합니다. 이러한 파일은 웹 사이트의 파일로 실제로 존재 하지는 않습니다. 대신 이러한 파일 중 하나에 대 한 요청이 웹 서버에 도착 하면 ASP.NET 엔진은 querystring을 검사 하 고 적절 한 JavaScript 콘텐츠를 반환 합니다. 이러한 세 개의 외부 JavaScript 파일에서 제공 하는 스크립트는 ASP.NET AJAX 프레임 워크의 클라이언트 라이브러리를 구성 합니다. ScriptManager가 내보내는 다른 `<script>` 태그는이 라이브러리를 초기화 하는 인라인 스크립트를 포함 합니다.

ASP.NET AJAX 프레임 워크를 사용 하는 페이지에는 ScriptManager에서 내보낸 외부 스크립트 참조 및 인라인 스크립트를 사용 하는 것이 중요 하지만 프레임 워크를 사용 하지 않는 페이지에는 필요 하지 않습니다. 따라서 ASP.NET AJAX 프레임 워크를 사용 하는 페이지에 ScriptManager만 추가 하는 것이 이상적입니다. 이 방법은 충분 하지만 프레임 워크를 사용 하는 페이지가 많은 경우 모든 페이지에 ScriptManager 컨트롤을 추가 하는 것이 가장 좋습니다 (반복 작업). 또는 마스터 페이지에 ScriptManager를 추가한 다음이 필요한 스크립트를 모든 콘텐츠 페이지에 삽입할 수 있습니다. 이 접근 방식을 사용 하는 경우 마스터 페이지에 이미 포함 되어 있으므로 ASP.NET AJAX 프레임 워크를 사용 하는 새 페이지에 ScriptManager를 추가 해야 할 필요가 없습니다. 1 단계에서는 마스터 페이지에 ScriptManager를 추가 하는 과정을 안내 합니다.

> [!NOTE]
> 마스터 페이지의 사용자 인터페이스 내에 AJAX 기능을 포함 하려는 경우에는 아무 것도 선택 하지 않아도 됩니다. 마스터 페이지에 ScriptManager를 포함 해야 합니다.

마스터 페이지에 ScriptManager를 추가할 때의 단점 중 하나는 필요한 지 여부에 관계 없이 *모든* 페이지에서 위의 스크립트를 내보내는 것입니다. 이렇게 하면 ScriptManager가 포함 된 (마스터 페이지를 통해) ASP.NET AJAX 프레임 워크의 기능을 사용 하지 않는 페이지에 대 한 대역폭이 낭비 될 수 있습니다. 그러나 얼마나 많은 대역폭이 낭비 되나요?

- ScriptManager에서 내보낸 실제 콘텐츠 (위에 표시 됨)는 1KB 보다 약간의 합계를 가집니다.
- 그러나 `<script>` 요소가 참조 하는 세 개의 외부 스크립트 파일은 압축 되지 않은 데이터의 약 450KB로 구성 됩니다. gzip 압축을 사용 하는 웹 사이트에서이 총 대역폭은 100KB 근처에서 감소할 수 있습니다. 그러나 이러한 스크립트 파일은 1 년 동안 브라우저에서 캐시 됩니다. 즉, 한 번 다운로드 하 여 사이트의 다른 페이지에서 다시 사용할 수 있어야 합니다.

최상의 경우에는 스크립트 파일이 캐시 될 때 총 비용은 무시할 수 있는 1KB입니다. 그러나 최악의 경우는 스크립트 파일을 아직 다운로드 하지 않은 상태에서 웹 서버를 사용 하 여 압축 형식을 사용 하지 않는 경우입니다 .이는 450KB 주위에 도달 하는 대역폭입니다.  전화 접속 모뎀을 통한 사용자 그 이유는 외부 스크립트 파일이 브라우저에서 캐시 되기 때문에이 최악의 시나리오는 자주 발생 하지 않기 때문입니다.

> [!NOTE]
> 마스터 페이지에 ScriptManager 컨트롤을 배치 하는 것이 불편 하면 웹 폼 (마스터 페이지의 `<form runat="server">` 태그)을 고려해 야 합니다. 다시 게시 모델을 사용 하는 모든 ASP.NET 페이지에는 정확히 하나의 웹 폼이 포함 되어야 합니다. Web Form을 추가 하면 추가 콘텐츠가 추가 됩니다. 많은 숨겨진 양식 필드, `<form>` 태그 자체 및 필요한 경우 스크립트에서 포스트백을 시작 하기 위한 JavaScript 함수를 추가 합니다. 이 태그는 다시 게시 되지 않는 페이지에는 필요 하지 않습니다. 이 불필요 한 태그는 마스터 페이지에서 Web Form을 제거 하 고이를 필요로 하는 각 콘텐츠 페이지에 수동으로 추가 하 여 제거할 수 있습니다. 그러나 마스터 페이지에 웹 양식을 추가 하는 경우의 이점은 특정 콘텐츠 페이지에 불필요 하 게 추가 하는 것 보다 단점 보다 더 큽니다.

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>1 단계: 마스터 페이지에 ScriptManager 컨트롤 추가

ASP.NET AJAX 프레임 워크를 사용 하는 모든 웹 페이지는 정확히 하나의 ScriptManager 컨트롤을 포함 해야 합니다. 이 요구 사항으로 인해 일반적으로 모든 콘텐츠 페이지에 ScriptManager 컨트롤이 자동으로 포함 되도록 마스터 페이지에 단일 ScriptManager 컨트롤을 저장 하는 것이 좋습니다. 또한 ScriptManager는 UpdatePanel 및 UpdateProgress 컨트롤과 같은 ASP.NET AJAX 서버 컨트롤 앞에와 야 합니다. 따라서 웹 폼 내의 ContentPlaceHolder 컨트롤 앞에 ScriptManager를 배치 하는 것이 가장 좋습니다.

`Site.master` 마스터 페이지를 열고 웹 `<div id="topContent">` 폼 내의 페이지에 ScriptManager 컨트롤을 추가 합니다 (그림 1 참조). Visual Web Developer 2008 또는 Visual Studio 2008를 사용 하는 경우에는 ScriptManager 컨트롤이 AJAX 확장 탭의 도구 상자에 있습니다. Visual Studio 2005을 사용 하는 경우 먼저 ASP.NET AJAX 프레임 워크를 설치 하 고 도구 상자에 컨트롤을 추가 해야 합니다. ASP.NET AJAX 다운로드 페이지를 방문 하 여 ASP.NET 2.0에 대 한 프레임 워크를 가져옵니다.

페이지에 ScriptManager를 추가한 후 해당 `ID` `ScriptManager1`에서 `MyManager`로 변경 합니다.

[마스터 페이지에 ScriptManager를 추가 ![](master-pages-and-asp-net-ajax-vb/_static/image2.png)](master-pages-and-asp-net-ajax-vb/_static/image1.png)

**그림 01**: 마스터 페이지에 ScriptManager 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image3.png))

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>2 단계: 콘텐츠 페이지에서 ASP.NET AJAX 프레임 워크 사용

이제 ScriptManager 컨트롤을 마스터 페이지에 추가 하면 ASP.NET AJAX framework 기능을 모든 콘텐츠 페이지에 추가할 수 있습니다. Northwind 데이터베이스에서 무작위로 선택 된 제품을 표시 하는 새 ASP.NET 페이지를 만들어 보겠습니다. ASP.NET AJAX 프레임 워크의 Timer 컨트롤을 사용 하 여 15 초 마다이 표시를 업데이트 하 고 새 제품을 표시 합니다.

먼저 `ShowRandomProduct.aspx`이라는 루트 디렉터리에 새 페이지를 만듭니다. 이 새 페이지를 `Site.master` 마스터 페이지에 바인딩해야 합니다.

[웹 사이트에 새 ASP.NET 페이지 추가 ![](master-pages-and-asp-net-ajax-vb/_static/image5.png)](master-pages-and-asp-net-ajax-vb/_static/image4.png)

**그림 02**: 웹 사이트에 새 ASP.NET 페이지 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image6.png))

마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정 [SKM1] 자습서에서는 명시적으로 설정 하지 않은 경우 페이지의 제목을 생성 한 `BasePage` 이라는 사용자 지정 기본 페이지 클래스를 만들었습니다. `ShowRandomProduct.aspx` 페이지의 코드 숨김으로 클래스로 이동 하 여 `BasePage` (`System.Web.UI.Page`대신)에서 파생 되도록 합니다.

마지막으로이 단원에 대 한 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. 마스터 페이지 상호 작용 단원에 대 한 `<siteMapNode>` 아래에 다음 태그를 추가 합니다.

[!code-xml[Main](master-pages-and-asp-net-ajax-vb/samples/sample2.xml)]

이 `<siteMapNode>` 요소를 추가 하는 방법은 단원 목록에 반영 되어 있습니다 (그림 5 참조).

### <a name="displaying-a-randomly-selected-product"></a>임의로 선택 된 제품 표시

`ShowRandomProduct.aspx`로 돌아갑니다. 디자이너에서 도구 상자의 UpdatePanel 컨트롤을 `MainContent` 콘텐츠 컨트롤로 끌고 `ID` 속성을 `ProductPanel`로 설정 합니다. UpdatePanel은 부분 페이지 포스트백을 통해 비동기적으로 업데이트 될 수 있는 화면 영역을 나타냅니다.

첫 번째 작업은 UpdatePanel 내에서 무작위로 선택 된 제품에 대 한 정보를 표시 하는 것입니다. DetailsView 컨트롤을 UpdatePanel으로 끌어 시작 합니다. DetailsView 컨트롤의 `ID` 속성을 `ProductInfo`로 설정 하 고 `Height` 및 `Width` 속성을 지웁니다. DetailsView의 스마트 태그를 확장 하 고 데이터 소스 선택 드롭다운 목록에서 DetailsView을 `RandomProductDataSource`라는 새 SqlDataSource 컨트롤에 바인딩하려면 선택 합니다.

[새 SqlDataSource 컨트롤에 DetailsView ![바인딩](master-pages-and-asp-net-ajax-vb/_static/image8.png)](master-pages-and-asp-net-ajax-vb/_static/image7.png)

**그림 03**: 새 SqlDataSource 컨트롤에 DetailsView 바인딩 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image9.png))

`NorthwindConnectionString` (콘텐츠 페이지에서 마스터 페이지와 상호 작용 [SKM2] 자습서에서 만든)를 통해 Northwind 데이터베이스에 연결 하도록 SqlDataSource 컨트롤을 구성 합니다. Select 문을 구성할 때 사용자 지정 SQL 문을 지정 하도록 선택 하 고 다음 쿼리를 입력 합니다.

[!code-sql[Main](master-pages-and-asp-net-ajax-vb/samples/sample3.sql)]

`SELECT` 절의 `TOP 1` 키워드는 쿼리에서 반환한 첫 번째 레코드만 반환 합니다. `NEWID()` 함수는 새 GUID (globally unique identifier) 값을 생성 하며, `ORDER BY` 절에서 테이블의 레코드를 임의 순서로 반환 하는 데 사용할 수 있습니다.

[SqlDataSource를 구성 하 ![임의로 선택 된 단일 레코드를 반환 합니다.](master-pages-and-asp-net-ajax-vb/_static/image11.png)](master-pages-and-asp-net-ajax-vb/_static/image10.png)

**그림 04**: 임의로 선택 된 단일 레코드를 반환 하도록 SqlDataSource 구성 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image12.png))

마법사를 완료 한 후 Visual Studio에서 위의 쿼리에서 반환 된 두 개의 열에 대해 BoundField를 만듭니다. 이 시점에서 페이지의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample4.aspx)]

그림 5에는 브라우저를 통해 볼 때 `ShowRandomProduct.aspx` 페이지가 표시 됩니다. 브라우저의 새로 고침 단추를 클릭 하 여 페이지를 다시 로드 합니다. 임의로 선택 된 새 레코드의 `ProductName` 및 `UnitPrice` 값이 표시 됩니다.

[![임의의 제품 이름과 가격이 표시 됩니다.](master-pages-and-asp-net-ajax-vb/_static/image14.png)](master-pages-and-asp-net-ajax-vb/_static/image13.png)

**그림 05**: 임의의 제품 이름 및 가격이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image15.png)).

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>15 초 마다 자동으로 새 제품 표시

ASP.NET AJAX 프레임 워크에는 지정 된 시간에 다시 게시를 수행 하는 타이머 컨트롤이 포함 되어 있습니다. 다시 게시 시 타이머의 `Tick` 이벤트가 발생 합니다. Timer 컨트롤이 UpdatePanel 내에 배치 되 면 부분 페이지 포스트백이 트리거됩니다 .이 경우 DetailsView에 데이터를 다시 바인딩하고 임의로 선택 된 새 제품을 표시할 수 있습니다.

이를 수행 하려면 도구 상자에서 타이머를 끌어서 UpdatePanel에 놓습니다. 타이머의 `ID` `Timer1`에서 `ProductTimer`로, `Interval` 속성은 6만에서 15000로 변경 합니다. `Interval` 속성은 다시 게시 사이의 시간 (밀리초)을 나타냅니다. 15000으로 설정 하면 타이머에서 15 초 마다 부분 페이지 포스트백을 트리거합니다. 이 시점에서 타이머의 선언 태그는 다음과 같이 표시 됩니다.

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample5.aspx)]

타이머의 `Tick` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이 이벤트 처리기에서 DetailsView의 `DataBind` 메서드를 호출 하 여 데이터를 DetailsView에 다시 바인딩해야 합니다. 이렇게 하면 DetailsView에서 데이터 원본 제어의 데이터를 다시 검색 하도록 지시 합니다. 그러면 새로 무작위로 선택 된 레코드가 선택 되 고 표시 됩니다 (브라우저의 새로 고침 단추를 클릭 하 여 페이지를 다시 로드 하는 경우 처럼).

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample6.vb)]

이것이 전부입니다! 브라우저를 통해 페이지를 다시 방문 합니다. 처음에는 임의의 제품 정보가 표시 됩니다. 화면을 patiently 하는 경우 15 초 후에 새 제품 magically에 대 한 정보가 기존 디스플레이를 대체 하는 것을 알 수 있습니다.

여기에서 발생 하는 상황을 더 잘 확인 하려면 표시를 마지막으로 업데이트 한 시간을 표시 하는 레이블 컨트롤을 UpdatePanel에 추가 해 보겠습니다. UpdatePanel 내에 Label 웹 컨트롤을 추가 하 고, 해당 `ID` `LastUpdateTime`로 설정 하 고, 해당 `Text` 속성의 선택을 취소 합니다. 그런 다음 UpdatePanel의 `Load` 이벤트에 대 한 이벤트 처리기를 만들고 레이블에 현재 시간을 표시 합니다. (전체 또는 부분 페이지 포스트백 마다 UpdatePanel의 `Load` 이벤트가 발생 합니다.)

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample7.vb)]

이 변경이 완료 되 면 페이지에 현재 표시 된 제품이 로드 된 시간이 포함 됩니다. 그림 6에서는 처음 방문할 때 페이지를 보여 줍니다. 그림 7에는 타이머 컨트롤에 "선택"가 있고 새 제품에 대 한 정보를 표시 하기 위해 UpdatePanel이 새로 고쳐진 후 15 초 페이지가 표시 됩니다.

[임의로 선택 된 제품이 페이지 로드에 표시 ![](master-pages-and-asp-net-ajax-vb/_static/image17.png)](master-pages-and-asp-net-ajax-vb/_static/image16.png)

**그림 06**: 임의로 선택 된 제품이 페이지 로드에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image18.png)).

[새로 무작위로 선택 된 제품이 15 초 마다 ![표시 됩니다.](master-pages-and-asp-net-ajax-vb/_static/image20.png)](master-pages-and-asp-net-ajax-vb/_static/image19.png)

**그림 07**: 15 초 마다 무작위로 선택 된 새 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image21.png)).

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>3 단계: Scriptmanagerproxy 컨트롤용 컨트롤 사용

ASP.NET AJAX framework 클라이언트 라이브러리에 필요한 스크립트를 포함 하는 것과 함께 ScriptManager는 사용자 지정 JavaScript 파일, 스크립트 사용 웹 서비스에 대 한 참조, 사용자 지정 인증, 권한 부여 및 프로필 서비스를 등록할 수도 있습니다. 일반적으로 이러한 사용자 지정은 특정 페이지에만 적용 됩니다. 그러나 사용자 지정 스크립트 파일, 웹 서비스 참조 또는 인증, 권한 부여 또는 프로필 서비스를 마스터 페이지의 ScriptManager에서 참조 하는 경우 웹 사이트의 모든 페이지에 포함 됩니다.

페이지 단위에 따라 ScriptManager 관련 사용자 지정 항목을 추가 하려면 Scriptmanagerproxy 컨트롤용 컨트롤을 사용 합니다. 콘텐츠 페이지에 Scriptmanagerproxy 컨트롤용를 추가 하 고 Scriptmanagerproxy 컨트롤용에서 사용자 지정 JavaScript 파일, 웹 서비스 참조 또는 인증, 권한 부여 또는 프로필 서비스를 등록할 수 있습니다. 이렇게 하면 특정 콘텐츠 페이지에 대해 이러한 서비스를 등록 하는 효과가 있습니다.

> [!NOTE]
> ASP.NET 페이지에는 ScriptManager 컨트롤이 하나만 있을 수 있습니다. 따라서 ScriptManager 컨트롤이 마스터 페이지에 이미 정의 되어 있는 경우에는 콘텐츠 페이지에 ScriptManager 컨트롤을 추가할 수 없습니다. Scriptmanagerproxy 컨트롤용의 유일한 용도는 개발자가 마스터 페이지에서 ScriptManager를 정의할 수 있는 방법을 제공 하는 것 이지만 페이지 별로 ScriptManager 사용자 지정 항목을 추가할 수 있는 기능도 있습니다.

Scriptmanagerproxy 컨트롤용 컨트롤의 작동을 확인 하려면 클라이언트 쪽 스크립트를 사용 하 여 타이머 컨트롤을 일시 중지 하거나 다시 시작 하는 단추를 포함 하도록 `ShowRandomProduct.aspx`에서 UpdatePanel을 보강 합니다. Timer 컨트롤에는이 원하는 기능을 구현 하는 데 사용할 수 있는 세 가지 클라이언트 쪽 메서드가 있습니다.

- `_startTimer()`-타이머 컨트롤을 시작 합니다.
- `_raiseTick()`-Timer 컨트롤을 "tick"로 설정 하 여 서버에서 다시 게시 하 고 Tick 이벤트를 발생 시킵니다.
- `_stopTimer()`-타이머 컨트롤을 중지 합니다.

`timerEnabled` 라는 변수와 `ToggleTimer`라는 함수를 사용 하 여 JavaScript 파일을 만들어 보겠습니다. `timerEnabled` 변수는 타이머 컨트롤을 현재 사용할 수 있는지 여부를 나타냅니다. 기본값은 true입니다. `ToggleTimer` 함수는 두 개의 입력 매개 변수를 허용 합니다. 일시 중지/다시 시작 단추에 대 한 참조와 타이머 컨트롤의 클라이언트 쪽 `id` 값입니다. 이 함수는 `timerEnabled`값을 전환 하 고, 타이머 컨트롤에 대 한 참조를 가져오고, 타이머를 시작 하거나 중지 하 고 (`timerEnabled`값에 따라), 단추의 표시 텍스트를 "일시 중지" 또는 "다시 시작"으로 업데이트 합니다. 이 함수는 일시 중지/다시 시작 단추를 클릭할 때마다 호출 됩니다.

먼저 `Scripts`이라는 웹 사이트에서 새 폴더를 만듭니다. 그런 다음 JScript 파일 형식의 `TimerScript.js` 라는 스크립트 폴더에 새 파일을 추가 합니다.

[Scripts 폴더에 새 JavaScript 파일을 추가 ![](master-pages-and-asp-net-ajax-vb/_static/image23.png)](master-pages-and-asp-net-ajax-vb/_static/image22.png)

**그림 08**: `Scripts` 폴더에 새 JavaScript 파일 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image24.png))

[새 JavaScript 파일이 웹 사이트에 추가 ![](master-pages-and-asp-net-ajax-vb/_static/image26.png)](master-pages-and-asp-net-ajax-vb/_static/image25.png)

**그림 09**: 새 JavaScript 파일이 웹 사이트에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image27.png)).

다음으로 `TimerScript.js` 파일에 다음 스크립트를 추가 합니다.

[!code-csharp[Main](master-pages-and-asp-net-ajax-vb/samples/sample8.cs)]

이제 `ShowRandomProduct.aspx`에서이 사용자 지정 JavaScript 파일을 등록 해야 합니다. `ShowRandomProduct.aspx`로 돌아가서 페이지에 Scriptmanagerproxy 컨트롤용 컨트롤을 추가 합니다. 해당 `ID` `MyManagerProxy`로 설정 합니다. 사용자 지정 JavaScript 파일을 등록 하려면 디자이너에서 Scriptmanagerproxy 컨트롤용 컨트롤을 선택 하 고 속성 창로 이동 합니다. 속성 중 하나에는 Scripts 라는 제목의 제목이 있습니다. 이 속성을 선택 하면 그림 10에 표시 된 System.web.ui.scriptreference 컬렉션 편집기가 표시 됩니다. 추가 단추를 클릭 하 여 새 스크립트 참조를 포함 한 다음 경로 속성: `~/Scripts/TimerScript.js`에서 스크립트 파일의 경로를 입력 합니다.

[Scriptmanagerproxy 컨트롤용 컨트롤에 스크립트 참조를 추가 ![](master-pages-and-asp-net-ajax-vb/_static/image29.png)](master-pages-and-asp-net-ajax-vb/_static/image28.png)

**그림 10**: scriptmanagerproxy 컨트롤용 컨트롤에 스크립트 참조 추가 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image30.png))

스크립트 참조를 추가한 후에는 다음 태그 조각이 보여 주는 것 처럼 Scriptmanagerproxy 컨트롤용 컨트롤의 선언적 태그가 단일 `ScriptReference` 항목을 포함 하는 `<Scripts>` 컬렉션을 포함 하도록 업데이트 됩니다.

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample9.aspx)]

`ScriptReference` 항목은 JavaScript 파일에 대 한 참조를 렌더링 된 태그에 포함 하도록 Scriptmanagerproxy 컨트롤용에 지시 합니다. 즉, Scriptmanagerproxy 컨트롤용에서 사용자 지정 스크립트를 등록 하면 `ShowRandomProduct.aspx` 페이지의 렌더링 된 출력에는 `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`다른 `<script src="url"></script>` 태그가 포함 됩니다.

이제 `ShowRandomProduct.aspx` 페이지에서 클라이언트 스크립트의 `TimerScript.js`에 정의 된 `ToggleTimer` 함수를 호출할 수 있습니다. UpdatePanel 내에 다음 HTML을 추가 합니다.

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample10.aspx)]

그러면 "Pause" 라는 텍스트가 포함 된 단추가 표시 됩니다. 클릭 될 때마다 JavaScript 함수 `ToggleTimer` 호출 되어 단추에 대 한 참조와 타이머 컨트롤의 `id` 값 (`ProductTimer`)을 전달 합니다. Timer 컨트롤의 `id` 값을 가져오는 구문을 확인 합니다. `<%=ProductTimer.ClientID%>` `ProductTimer` Timer 컨트롤의 `ClientID` 속성 값을 내보냅니다. 콘텐츠 페이지에서 컨트롤 ID 이름 지정 [SKM3] 자습서에서는 서버 쪽 `ID` 값과 결과 클라이언트 쪽 `id` 값 간의 차이와 `ClientID` 클라이언트 쪽 `id`를 반환 하는 방법에 대해 설명 했습니다.

그림 11에서는 브라우저를 통해 처음 방문할 때이 페이지를 보여 줍니다. 타이머가 현재 실행 되 고 있으며 15 초 마다 표시 된 제품 정보를 업데이트 합니다. 그림 12는 일시 중지 단추를 클릭 한 후의 화면을 보여 줍니다. 일시 중지 단추를 클릭 하면 타이머가 중지 되 고 단추의 텍스트가 "Resume"으로 업데이트 됩니다. 사용자가 다시 시작을 클릭 하면 제품 정보를 새로 고치고 15 초 마다 새로 고침을 계속 합니다.

[![일시 중지 단추를 클릭 하 여 타이머 컨트롤을 중지 합니다.](master-pages-and-asp-net-ajax-vb/_static/image32.png)](master-pages-and-asp-net-ajax-vb/_static/image31.png)

**그림 11**: 일시 중지 단추를 클릭 하 여 타이머 컨트롤 중지 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image33.png))

[![다시 시작 단추를 클릭 하 여 타이머를 다시 시작 합니다.](master-pages-and-asp-net-ajax-vb/_static/image35.png)](master-pages-and-asp-net-ajax-vb/_static/image34.png)

**그림 12**: 타이머를 다시 시작 하려면 [다시 시작] 단추를 클릭 하십시오 ([전체 크기 이미지를 보려면 클릭](master-pages-and-asp-net-ajax-vb/_static/image36.png)).

## <a name="summary"></a>요약

ASP.NET AJAX 프레임 워크를 사용 하 여 AJAX 사용 웹 응용 프로그램을 빌드하는 경우 모든 AJAX 사용 웹 페이지에 ScriptManager 컨트롤이 포함 되어야 합니다. 이 프로세스를 용이 하 게 하기 위해 각 및 모든 콘텐츠 페이지에 ScriptManager를 추가 해야 하는 대신 마스터 페이지에 ScriptManager를 추가할 수 있습니다. 1 단계에서는 마스터 페이지에 ScriptManager를 추가 하는 방법을 보여 주었습니다. 2 단계에서는 콘텐츠 페이지에서 AJAX 기능을 구현 하는 방법을 살펴보았습니다.

사용자 지정 스크립트, 스크립트 사용 웹 서비스에 대 한 참조 또는 특정 콘텐츠 페이지에 사용자 지정 된 인증, 권한 부여 또는 프로필 서비스를 추가 해야 하는 경우 콘텐츠 페이지에 Scriptmanagerproxy 컨트롤용 컨트롤을 추가 하 고 다음을 구성 합니다. 사용자 지정 3 단계에서는 Scriptmanagerproxy 컨트롤용를 사용 하 여 특정 콘텐츠 페이지에서 사용자 지정 JavaScript 파일을 등록 하는 방법을 살펴보았습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET AJAX 프레임 워크](../../../../ajax/index.md)
- [ASP.NET AJAX 자습서](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 비디오](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX를 사용 하 여 대화형 사용자 인터페이스 빌드](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [NEWID를 사용 하 여 레코드를 임의로 정렬](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [Timer 컨트롤 사용](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](interacting-with-the-content-page-from-the-master-page-vb.md)
> [다음](specifying-the-master-page-programmatically-vb.md)
