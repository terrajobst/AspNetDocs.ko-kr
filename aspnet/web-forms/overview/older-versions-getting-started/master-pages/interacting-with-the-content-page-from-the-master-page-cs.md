---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
title: 마스터 페이지에서 콘텐츠 페이지와 상호 작용 (C#) | Microsoft Docs
author: rick-anderson
description: 마스터 페이지의 코드에서 콘텐츠 페이지의 메서드를 호출 하 고 속성을 설정 하는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 3282df5e-516c-4972-8666-313828b90fb5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 2cf57665aa584285351d874267949d61db69c7fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501167"
---
# <a name="interacting-with-the-content-page-from-the-master-page-c"></a>마스터 페이지에서 콘텐츠 페이지와 상호 작용(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_CS.pdf)

> 마스터 페이지의 코드에서 콘텐츠 페이지의 메서드를 호출 하 고 속성을 설정 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

이전 자습서에서는 콘텐츠 페이지를 프로그래밍 방식으로 마스터 페이지와 상호 작용 하는 방법을 살펴보았습니다. 가장 최근에 추가 된 5 개 제품에 나열 된 GridView 컨트롤을 포함 하도록 마스터 페이지를 업데이트 했습니다. 그런 다음 사용자가 새 제품을 추가할 수 있는 콘텐츠 페이지를 만들었습니다. 새 제품을 추가할 때 콘텐츠 페이지는 방금 추가 된 제품을 포함 하도록 GridView를 새로 고치도록 마스터 페이지에 지시 하는 데 필요 합니다. 이 기능은 GridView에 바인딩된 데이터를 새로 고친 후 콘텐츠 페이지에서 해당 메서드를 호출 하는 마스터 페이지에 공용 메서드를 추가 하 여 수행 되었습니다.

콘텐츠 페이지에서 가장 일반적으로 발생 하는 콘텐츠 및 마스터 페이지 상호 작용의 형태입니다. 그러나 마스터 페이지에서 현재 콘텐츠 페이지의 작업을 rouse 수 있으며, 사용자가 콘텐츠 페이지에도 표시 되는 데이터를 수정할 수 있는 사용자 인터페이스 요소를 마스터 페이지에 포함 하는 경우 이러한 기능이 필요할 수 있습니다. GridView 컨트롤의 제품 정보를 표시 하는 콘텐츠 페이지와 클릭 하면 모든 제품의 가격을 두 배로 늘리는 단추 컨트롤이 포함 된 마스터 페이지를 살펴보겠습니다. 이전 자습서의 예제와 마찬가지로, 새 가격을 표시 하도록 이중 가격 단추를 클릭 한 후 GridView를 새로 고쳐야 하지만,이 시나리오에서는 콘텐츠 페이지를 작업으로 rouse는 데 필요한 마스터 페이지입니다.

이 자습서에서는 콘텐츠 페이지에서 마스터 페이지 호출 기능을 정의 하는 방법을 설명 합니다.

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>이벤트 및 이벤트 처리기를 통해 프로그래밍 방식으로 상호 작용 Instigating

마스터 페이지에서 콘텐츠 페이지 기능을 호출 하는 것은 다른 방법 보다 더 어렵습니다. 콘텐츠 페이지에는 단일 마스터 페이지가 있으므로 콘텐츠 페이지에서 프로그래밍 방식으로 상호 작용을 instigating 때 어떤 공용 메서드 및 속성이 삭제 되는지 알고 있습니다. 그러나 마스터 페이지에는 각각 고유한 속성 및 메서드 집합을 포함 하는 다양 한 콘텐츠 페이지가 있을 수 있습니다. 이렇게 하면 런타임 시까지 호출 될 내용 페이지를 모를 때 콘텐츠 페이지에서 일부 작업을 수행 하기 위해 마스터 페이지에서 코드를 작성할 수 있나요?

Button 컨트롤과 같은 ASP.NET 웹 컨트롤을 고려 합니다. 단추 컨트롤은 원하는 수의 ASP.NET 페이지에 나타날 수 있으며, 클릭 된 페이지에 경고할 수 있는 메커니즘이 필요 합니다. 이는 *이벤트*를 사용 하 여 수행 됩니다. 특히 단추 컨트롤이 클릭 될 때 `Click` 이벤트를 발생 시킵니다. 단추를 포함 하는 ASP.NET 페이지는 *이벤트 처리기*를 통해 해당 알림에 선택적으로 응답할 수 있습니다.

동일한 패턴을 사용 하 여 해당 콘텐츠 페이지에서 마스터 페이지 트리거 기능을 사용할 수 있습니다.

1. 마스터 페이지에 이벤트를 추가 합니다.
2. 마스터 페이지가 해당 콘텐츠 페이지와 통신 해야 할 때마다 이벤트를 발생 시킵니다. 예를 들어 마스터 페이지가 해당 콘텐츠 페이지에 사용자가 두 배로 증가 하는 것을 경고 해야 하는 경우 가격은 두 배가 되 면 즉시 이벤트가 발생 합니다.
3. 일부 작업을 수행 해야 하는 해당 콘텐츠 페이지에서 이벤트 처리기를 만듭니다.

이 자습서의 나머지 부분에서는 소개에 설명 된 예제를 구현 합니다. 즉, 데이터베이스의 제품을 나열 하는 콘텐츠 페이지와 가격을 double 하는 단추 컨트롤이 포함 된 마스터 페이지입니다.

## <a name="step-1-displaying-products-in-a-content-page"></a>1 단계: 콘텐츠 페이지에서 제품 표시

비즈니스의 첫 번째 순서는 Northwind 데이터베이스의 제품을 나열 하는 콘텐츠 페이지를 만드는 것입니다. (이전 자습서의 프로젝트에 Northwind 데이터베이스를 추가 하 여 [*콘텐츠 페이지에서 마스터 페이지와 상호 작용*](interacting-with-the-master-page-from-the-content-page-cs.md)했습니다.) 먼저 `Products.aspx`이라는 `~/Admin` 폴더에 새 ASP.NET 페이지를 추가 하 고 `Site.master` 마스터 페이지에 바인딩해야 합니다. 그림 1에서는이 페이지가 웹 사이트에 추가 된 후의 솔루션 탐색기 보여 줍니다.

[관리 폴더에 새 ASP.NET 페이지를 추가 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image1.png)

**그림 01**: `Admin` 폴더에 새 ASP.NET 페이지 추가 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image3.png))

[*마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서에서 명시적으로 설정 하지 않은 경우 페이지의 제목을 생성 하는 `BasePage` 이라는 사용자 지정 기본 페이지 클래스를 만들었습니다. `Products.aspx` 페이지의 코드 숨김으로 클래스로 이동 하 여 `BasePage` (`System.Web.UI.Page`대신)에서 파생 되도록 합니다.

마지막으로이 단원에 대 한 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. 마스터 페이지 상호 작용 단원에 대 한 콘텐츠 `<siteMapNode>` 아래에 다음 태그를 추가 합니다.

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample1.xml)]

이 `<siteMapNode>` 요소를 추가 하는 방법은 단원 목록에 반영 되어 있습니다 (그림 5 참조).

`Products.aspx`로 돌아갑니다. `MainContent`에 대 한 콘텐츠 컨트롤에서 GridView 컨트롤을 추가 하 고 이름을 `ProductsGrid`로 만듭니다. GridView를 `ProductsDataSource`라는 새 SqlDataSource 컨트롤에 바인딩합니다.

[GridView를 새 SqlDataSource 컨트롤에 바인딩 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image4.png)

**그림 02**: GridView를 새 SqlDataSource 컨트롤에 바인딩 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image6.png))

Northwind 데이터베이스를 사용 하도록 마법사를 구성 합니다. 이전 자습서를 수행한 경우에는 `Web.config`에 `NorthwindConnectionString` 라는 연결 문자열이 이미 있어야 합니다. 그림 3에 표시 된 것 처럼 드롭다운 목록에서이 연결 문자열을 선택 합니다.

[Northwind 데이터베이스를 사용 하도록 SqlDataSource를 구성 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image7.png)

**그림 03**: Northwind 데이터베이스를 사용 하도록 SqlDataSource 구성 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image9.png))

그런 다음 드롭다운 목록에서 Products 테이블을 선택 하 고 `ProductName` 및 `UnitPrice` 열을 반환 하 여 데이터 소스 컨트롤의 `SELECT` 문을 지정 합니다 (그림 4 참조). 다음을 클릭 하 고 마침을 클릭 하 여 데이터 원본 구성 마법사를 완료 합니다.

[Products 테이블에서 ProductName 및 UnitPrice 필드를 반환 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image10.png)

**그림 04**: `Products` 테이블의 `ProductName` 및 `UnitPrice` 필드 반환 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image12.png))

이제 모든 작업을 마쳤습니다. 마법사를 완료 한 후 Visual Studio에서는 두 개의 BoundFields를 GridView에 추가 하 여 SqlDataSource 컨트롤에서 반환 된 두 필드를 미러링합니다. GridView 및 SqlDataSource 컨트롤의 태그는 다음과 같습니다. 그림 5는 브라우저를 통해 볼 때의 결과를 보여 줍니다.

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample2.aspx)]

[각 제품 및 해당 가격이 GridView에 나열 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image13.png)

**그림 05**: 각 제품과 가격은 GridView에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image15.png)).

> [!NOTE]
> GridView의 모양을 자유롭게 정리 합니다. 표시 되는 UnitPrice 값의 서식을 통화로 지정 하 고 배경색 및 글꼴을 사용 하 여 표의 모양을 개선 하는 것도 여기에 포함 됩니다. ASP.NET에서 데이터를 표시 하 고 서식 지정 하는 방법에 대 한 자세한 내용은 [데이터 자습서 시리즈 작업](../../data-access/index.md)을 참조 하세요.

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>2 단계: 마스터 페이지에 이중 가격 단추 추가

다음 작업은 클릭 하면 데이터베이스에 있는 모든 제품의 가격을 두 배로 하는 단추 웹 컨트롤을 마스터 페이지에 추가 하는 것입니다. `Site.master` 마스터 페이지를 열고 도구 상자의 단추를 디자이너로 끌어 온 다음 이전 자습서에서 추가한 `RecentProductsDataSource` SqlDataSource 컨트롤 아래에 배치 합니다. 단추의 `ID` 속성을 `DoublePrice`로 설정 하 고 `Text` 속성을 "이중 제품 가격"으로 설정 합니다.

다음으로, `DoublePricesDataSource`의 이름을 지정 하 여 SqlDataSource 컨트롤을 마스터 페이지에 추가 합니다. 이 SqlDataSource는 `UPDATE` 문을 실행 하 여 모든 가격을 두 배로 하는 데 사용 됩니다. 특히 `ConnectionString` 및 `UpdateCommand` 속성을 적절 한 연결 문자열과 `UPDATE` 문으로 설정 해야 합니다. 그런 다음 `DoublePrice` 단추를 클릭 하면이 SqlDataSource 컨트롤의 `Update` 메서드를 호출 해야 합니다. `ConnectionString` 및 `UpdateCommand` 속성을 설정 하려면 SqlDataSource 컨트롤을 선택한 다음 속성 창으로 이동 합니다. `ConnectionString` 속성은 드롭다운 목록에서 `Web.config`에 이미 저장 되어 있는 연결 문자열을 나열 합니다. 그림 6에 표시 된 것 처럼 `NorthwindConnectionString` 옵션을 선택 합니다.

[NorthwindConnectionString를 사용 하도록 SqlDataSource를 구성 ![](interacting-with-the-content-page-from-the-master-page-cs/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image16.png)

**그림 06**: `NorthwindConnectionString`을 사용 하도록 SqlDataSource 구성 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image18.png))

`UpdateCommand` 속성을 설정 하려면 속성 창에서 UpdateQuery 옵션을 찾습니다. 이 속성을 선택 하면 타원이 있는 단추가 표시 됩니다. 그림 7에 표시 된 명령 및 매개 변수 편집기 대화 상자를 표시 하려면이 단추를 클릭 합니다. 대화 상자의 텍스트 상자에 다음 `UPDATE` 문을 입력 합니다.

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample3.sql)]

이 문은 실행 될 때 `Products` 테이블의 각 레코드에 대 한 `UnitPrice` 값을 두 배로 받습니다.

[SqlDataSource의 UpdateCommand 속성 ![설정](interacting-with-the-content-page-from-the-master-page-cs/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image19.png)

**그림 07**: SqlDataSource의 `UpdateCommand` 속성 설정 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image21.png))

이러한 속성을 설정한 후에는 Button 및 SqlDataSource 컨트롤의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample4.aspx)]

`DoublePrice` 단추를 클릭 하면 `Update` 메서드를 호출 하는 것만 남았습니다. `DoublePrice` 단추에 대 한 `Click` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample5.cs)]

이 기능을 테스트 하려면 1 단계에서 만든 `~/Admin/Products.aspx` 페이지를 방문 하 고 "이중 제품 가격" 단추를 클릭 합니다. 단추를 클릭 하면 포스트백이 발생 하 고 `DoublePrice` 단추의 `Click` 이벤트 처리기가 실행 되어 모든 제품의 가격이 배가 됩니다. 그러면 페이지가 다시 렌더링 되 고 태그가 반환 되 고 브라우저에 다시 표시 됩니다. 그러나 콘텐츠 페이지의 GridView에는 "이중 제품 가격" 단추가 클릭 되기 전과 동일한 가격이 나열 됩니다. 이는 처음에 GridView에 로드 된 데이터의 상태가 뷰 상태에 저장 되기 때문입니다. 그렇지 않으면 지시 하지 않는 한 다시 게시 시 다시 로드 되지 않습니다. 다른 페이지를 방문 하 여 `~/Admin/Products.aspx` 페이지로 돌아가면 업데이트 된 가격이 표시 됩니다.

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>3 단계: 가격이 두 배가 될 때 이벤트 발생

`~/Admin/Products.aspx` 페이지의 GridView에는 즉시 가격이 두 배가 반영 되지 않으므로 사용자는 "이중 제품 가격" 단추를 클릭 하지 않았거나 작동 하지 당연히 생각할 수 있습니다. 단추를 몇 번 더 클릭 하 여 가격을 다시 두 번 시도할 수 있습니다. 이 문제를 해결 하려면 콘텐츠 페이지에서 표가 두 배가 되는 즉시 새 가격을 표시 해야 합니다.

이 자습서의 앞부분에서 설명한 것 처럼 사용자가 `DoublePrice` 단추를 클릭할 때마다 마스터 페이지에서 이벤트를 발생 시켜야 합니다. 이벤트는 특정 클래스 (이벤트 게시자)가 다른 클래스 집합 (이벤트 구독자)에 게 다른 클래스 집합을 알리는 방법입니다. 이 예제에서 마스터 페이지는 이벤트 게시자입니다. `DoublePrice` 단추를 클릭 했을 때 관심 있는 콘텐츠 페이지는 구독자입니다.

클래스는 발생 하는 이벤트에 대 한 응답으로 실행 되는 메서드인 *이벤트 처리기*를 만들어 이벤트를 구독 합니다. 게시자는 *이벤트 대리자*를 정의 하 여 발생 하는 이벤트를 정의 합니다. 이벤트 대리자는 이벤트 처리기에서 허용 해야 하는 입력 매개 변수를 지정 합니다. .NET Framework에서 이벤트 대리자는 값을 반환 하지 않고 두 개의 입력 매개 변수를 허용 합니다.

- 이벤트 소스를 식별 하는 `Object`및
- 에서 파생 된 클래스 `System.EventArgs`

이벤트 처리기에 전달 되는 두 번째 매개 변수에는 이벤트에 대 한 추가 정보가 포함 될 수 있습니다. 기본 `EventArgs` 클래스가 정보를 함께 전달 하지 않지만 .NET Framework에는 `EventArgs`를 확장 하 고 추가 속성을 포함 하는 여러 클래스가 포함 됩니다. 예를 들어 `CommandEventArgs` 인스턴스는 `Command` 이벤트에 응답 하는 이벤트 처리기에 전달 되 고 두 개의 정보 속성인 `CommandArgument` 및 `CommandName`를 포함 합니다.

> [!NOTE]
> 이벤트 생성, 발생 및 처리에 대 한 자세한 내용은 간단한 영어로 표시 되는 이벤트 [및 대리자](https://msdn.microsoft.com/library/17sde2xt.aspx) 및 [이벤트 대리자](http://www.codeproject.com/KB/cs/eventdelegates.aspx)를 참조 하십시오.

이벤트를 정의 하려면 다음 구문을 사용 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample6.cs)]

사용자가 `DoublePrice` 단추를 클릭 하 고 다른 추가 정보를 함께 전달 하지 않아도 되는 경우에만 콘텐츠 페이지에 경고를 발생 시킬 수 있으므로 이벤트 대리자 `EventHandler`를 사용할 수 있습니다 .이 대리자는 두 번째 매개 변수로 `System.EventArgs`형식의 개체를 수락 하는 이벤트 처리기를 정의 합니다. 마스터 페이지에서 이벤트를 만들려면 마스터 페이지의 코드 뒤에 다음 코드 줄을 추가 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample7.cs)]

위의 코드는 `PricesDoubled`이라는 마스터 페이지에 공용 이벤트를 추가 합니다. 이제 가격이 두 배가 된 후에이 이벤트를 발생 시켜야 합니다. 이벤트를 발생 시키려면 다음 구문을 사용 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample8.cs)]

여기서 *발신자* 및 *eventArgs* 는 구독자의 이벤트 처리기에 전달 하려는 값입니다.

다음 코드를 사용 하 여 `DoublePrice` `Click` 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample9.cs)]

이전 처럼 `Click` 이벤트 처리기는 `DoublePricesDataSource` SqlDataSource 컨트롤의 `Update` 메서드를 호출 하 여 모든 제품의 가격을 두 배로 시작 합니다. 다음에는 이벤트 처리기에 두 가지 추가 사항이 있습니다. 먼저 `RecentProducts` GridView의 데이터를 새로 고칩니다. 이 GridView는 이전 자습서의 마스터 페이지에 추가 되었으며 최근에 추가 된 5 개 제품을 표시 합니다. 이 표를 새로 고쳐 이러한 5 개 제품에 대 한 단 두 개의 가격이 표시 되도록 해야 합니다. 그런 다음 `PricesDoubled` 이벤트가 발생 합니다. 마스터 페이지 자체 (`this`)에 대 한 참조가 이벤트 소스로 이벤트 처리기에 전송 되 고 빈 `EventArgs` 개체가 이벤트 인수로 전송 됩니다.

## <a name="step-4-handling-the-event-in-the-content-page"></a>4 단계: 콘텐츠 페이지에서 이벤트 처리

이 시점에서 `DoublePrice` 단추 컨트롤을 클릭할 때마다 마스터 페이지가 `PricesDoubled` 이벤트를 발생 시킵니다. 그러나이는 전투의 절반에 불과합니다. 구독자에서 이벤트를 처리 해야 합니다. 이벤트 처리기를 만들고 이벤트를 발생 시킬 때 이벤트 처리기가 실행 되도록 이벤트 처리기를 만들고 이벤트 연결 코드를 추가 하는 두 단계로 이루어집니다.

먼저 `Master_PricesDoubled`이라는 이벤트 처리기를 만듭니다. 마스터 페이지에서 `PricesDoubled` 이벤트를 정의 하는 방법 때문에 이벤트 처리기의 두 입력 매개 변수는 각각 `Object` 및 `EventArgs`형식 이어야 합니다. 이벤트 처리기에서 `ProductsGrid` GridView의 `DataBind` 메서드를 호출 하 여 데이터를 표에 다시 바인딩합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample10.cs)]

이벤트 처리기에 대 한 코드가 완성 되었지만 마스터 페이지의 `PricesDoubled` 이벤트를이 이벤트 처리기에 연결 해야 합니다. 구독자는 다음 구문을 통해 이벤트를 이벤트 처리기에 연결할 수 있습니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample11.cs)]

*게시자* 는 이벤트 *eventName*을 제공 하는 개체에 대 한 참조 이며 *methodName* 은 *eventdelegate*에 해당 하는 서명이 있는 구독자에 정의 된 이벤트 처리기의 이름입니다. 즉, 이벤트 대리자가 `EventHandler`되는 경우 *methodName* 은 값을 반환 하지 않는 구독자의 메서드 이름 이어야 하 고 각각 `Object` 및 `EventArgs`형식의 두 입력 매개 변수를 허용 합니다.

이 이벤트 연결 코드는 첫 번째 페이지 방문 및 후속 포스트백에서 실행 되어야 하며, 이벤트가 발생할 수 있는 시점 보다 이전 페이지 수명 주기에서 발생 해야 합니다. 이벤트 배선 코드를 추가 하는 데 좋은 시간은 PreInit 단계에 있습니다 .이 단계는 페이지 수명 주기 초기에 발생 합니다.

`~/Admin/Products.aspx`를 열고 `Page_PreInit` 이벤트 처리기를 만듭니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample12.cs)]

이 배선 코드를 완료 하려면 콘텐츠 페이지에서 마스터 페이지에 대 한 프로그래밍 방식 참조가 필요 합니다. 위의 자습서에 설명 된 것 처럼이 작업을 수행 하는 방법에는 두 가지가 있습니다.

- 느슨하게 형식화 된 `Page.Master` 속성을 적절 한 마스터 페이지 형식으로 캐스팅 하거나
- `.aspx` 페이지에 `@MasterType` 지시문을 추가한 다음 강력한 형식의 `Master` 속성을 사용 합니다.

후자를 사용 하는 방법을 살펴보겠습니다. 페이지의 선언적 태그 위에 다음 `@MasterType` 지시문을 추가 합니다.

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample13.aspx)]

그런 다음 `Page_PreInit` 이벤트 처리기에서 다음 이벤트 배선 코드를 추가 합니다.

[!code-csharp[Main](interacting-with-the-content-page-from-the-master-page-cs/samples/sample14.cs)]

이 코드를 사용 하면 `DoublePrice` 단추를 클릭할 때마다 콘텐츠 페이지의 GridView가 새로 고쳐집니다.

그림 8 및 9에서는이 동작을 보여 줍니다. 그림 8에서는 처음 방문할 때 페이지를 보여 줍니다. `RecentProducts` GridView (마스터 페이지의 왼쪽 열에 있는)와 `ProductsGrid` GridView (내용 페이지)의 가격 값을 확인 합니다. 그림 9는 `DoublePrice` 단추를 클릭 하면 바로 동일한 화면을 보여 줍니다. 여기에서 볼 수 있듯이 새 가격은 두 GridViews에 즉시 반영 됩니다.

[초기 가격 값을 ![합니다.](interacting-with-the-content-page-from-the-master-page-cs/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image22.png)

**그림 08**: 초기 가격 값 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image24.png))

[![하는 두 개의 가격이 모두 GridViews에 표시 됩니다.](interacting-with-the-content-page-from-the-master-page-cs/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-cs/_static/image25.png)

**그림 09**: Gridviews에 표시 되는 두 개의 가격 ([전체 크기 이미지를 보려면 클릭](interacting-with-the-content-page-from-the-master-page-cs/_static/image27.png))

## <a name="summary"></a>요약

이상적으로는 마스터 페이지와 해당 콘텐츠 페이지가 서로 완전히 분리 되며 상호 작용 수준이 필요 하지 않습니다. 그러나 마스터 페이지 또는 콘텐츠 페이지에서 수정할 수 있는 데이터를 표시 하는 마스터 페이지 또는 콘텐츠 페이지가 있는 경우에는 표시를 업데이트할 수 있도록 데이터를 수정할 때 마스터 페이지에서 콘텐츠 페이지에 경고를 표시 하거나 그 반대로 표시 해야 할 수 있습니다. 이전 자습서에서는 콘텐츠 페이지를 프로그래밍 방식으로 마스터 페이지와 상호 작용 하는 방법을 살펴보았습니다. 이 자습서에서는 마스터 페이지가 상호 작용을 시작 하는 방법을 살펴보았습니다.

콘텐츠 또는 마스터 페이지에서 콘텐츠 및 마스터 페이지를 프로그래밍 방식으로 조작할 수 있지만 사용 되는 상호 작용 패턴은 발생에 따라 달라 집니다. 차이점은 콘텐츠 페이지에 마스터 페이지가 하나 있지만 마스터 페이지에 다양 한 콘텐츠 페이지가 있을 수 있기 때문입니다. 마스터 페이지가 콘텐츠 페이지와 직접 상호 작용 하는 대신 마스터 페이지에서 이벤트를 발생 시켜 일부 작업이 수행 되었음을 알리는 것이 더 좋습니다. 작업에 대 한 중요 한 콘텐츠 페이지에서는 이벤트 처리기를 만들 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET에서 데이터 액세스 및 업데이트](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [이벤트 및 대리자](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [콘텐츠 및 마스터 페이지 간에 정보 전달](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [ASP.NET 자습서에서 데이터 작업](../../data-access/index.md)

### <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Suchi Banerjee. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](interacting-with-the-master-page-from-the-content-page-cs.md)
> [다음](master-pages-and-asp-net-ajax-cs.md)
