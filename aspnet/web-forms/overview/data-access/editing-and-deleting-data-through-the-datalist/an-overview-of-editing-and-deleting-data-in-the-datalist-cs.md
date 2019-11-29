---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
title: DataList에서 데이터 편집 및 삭제 개요 (C#) | Microsoft Docs
author: rick-anderson
description: DataList에는 기본 제공 되는 편집 및 삭제 기능이 없으므로이 자습서에서는 o 편집 및 삭제를 지 원하는 DataList를 만드는 방법을 알아봅니다.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: c3b0c86e-fe98-41ee-b26f-ca38cddaa75e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 481c9a14b1ebfe36ffcddd0237701bc04266e393
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74629342"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-c"></a>DataList에서 데이터 편집 및 삭제 개요 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_CS.exe) 또는 [PDF 다운로드](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/datatutorial36cs1.pdf)

> DataList에는 기본 제공 되는 편집 및 삭제 기능이 없으므로이 자습서에서는 기본 데이터의 편집 및 삭제를 지 원하는 DataList를 만드는 방법을 알아봅니다.

## <a name="introduction"></a>소개

[데이터 삽입, 업데이트 및 삭제](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) 자습서의 개요에서는 응용 프로그램 아키텍처, ObjectDataSource 및 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 데이터를 삽입, 업데이트 및 삭제 하는 방법을 살펴보았습니다. ObjectDataSource와 이러한 세 가지 데이터 웹 컨트롤을 사용 하 여 간단한 데이터 수정 인터페이스를 구현 하는 것은 단순히 스마트 태그에서 확인란을 선택 하는 것입니다. 코드를 작성할 필요가 없습니다.

그러나 DataList에는 GridView 컨트롤에서 고유 하 게 기본 제공 되는 편집 및 삭제 기능이 없습니다. 이러한 누락 된 기능은 DataList가 ASP.NET의 이전 버전에서의 유물 이라는 사실 때문에 선언적 데이터 소스 컨트롤 및 코드 없는 데이터 수정 페이지를 사용할 수 없는 경우에 발생 합니다. ASP.NET 2.0의 DataList는 GridView와 동일한 기본 데이터 수정 기능을 제공 하지 않지만 ASP.NET 1.x 기술을 사용 하 여 이러한 기능을 포함할 수 있습니다. 이 방법에는 약간의 코드가 필요 하지만이 자습서에서 볼 수 있듯이 DataList에는이 프로세스에 도움이 되는 몇 가지 이벤트와 속성이 있습니다.

이 자습서에서는 기본 데이터의 편집 및 삭제를 지 원하는 DataList를 만드는 방법을 알아봅니다. 이후 자습서에서는 입력 필드 유효성 검사, 데이터 액세스 또는 비즈니스 논리 계층에서 발생 하는 예외 처리 등을 비롯 하 여 고급 편집 및 삭제 시나리오를 살펴봅니다.

> [!NOTE]
> DataList와 마찬가지로 Repeater 컨트롤에는 삽입, 업데이트 또는 삭제를 위한 기본 기능을 사용할 권한이 없습니다. 이러한 기능을 추가할 수 있지만 DataList에는 이러한 기능 추가를 간소화 하는 Repeater에서 찾을 수 없는 속성 및 이벤트가 포함 됩니다. 따라서이 자습서와 편집 및 삭제를 확인 하는 이후 항목은 DataList에만 중점을 둡니다.

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>1 단계: 자습서 웹 페이지 편집 및 삭제 만들기

DataList에서 데이터를 업데이트 하 고 삭제 하는 방법에 대 한 탐색을 시작 하기 전에 먼저 웹 사이트 프로젝트에서이 자습서에 필요한 ASP.NET 페이지를 만든 다음 몇 가지를 살펴보겠습니다. `EditDeleteDataList`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image1.png)

**그림 1**: 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `EditDeleteDataList` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image4.png))

마지막으로 `Web.sitemap` 파일에 페이지를 항목으로 추가 합니다. 특히, DataList 및 Repeater `<siteMapNode>`를 사용 하 여 마스터/세부 정보 보고서 뒤에 다음 태그를 추가 합니다.

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 DataList 편집 및 삭제 자습서에 대 한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 DataList 편집 및 삭제 자습서에 대 한 항목이 포함 됩니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image5.png)

**그림 3**: 이제 사이트 맵에 DataList 편집 및 삭제 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>2 단계: 데이터 업데이트 및 삭제 기술 검사

GridView를 사용 하 여 데이터를 쉽게 편집 하 고 삭제할 수 있으므로 gridview와 ObjectDataSource가 함께 작동 하기 때문입니다. [삽입, 업데이트 및 삭제 자습서와 관련 된 이벤트 검사](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) 에 설명 된 대로 행의 업데이트 단추를 클릭 하면 GridView는 양방향 데이터 바인딩을 사용 하는 필드를 objectdatasource의 `UpdateParameters` 컬렉션에 자동으로 할당 한 다음 objectdatasource `Update()` 메서드를 호출 합니다.

Sadly DataList는 이러한 기본 제공 기능을 제공 하지 않습니다. 사용자 값이 ObjectDataSource 매개 변수에 할당 되 고 해당 `Update()` 메서드가 호출 되었는지 확인 하는 것은 사용자의 책임입니다. 이러한 노력을 지원 하기 위해 DataList는 다음과 같은 속성 및 이벤트를 제공 합니다.

- **[`DataKeyField` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx) 은** 업데이트 하거나 삭제할 때 DataList에서 각 항목을 고유 하 게 식별할 수 있어야 합니다. 표시 된 데이터의 기본 키 필드로이 속성을 설정 합니다. 이렇게 하면 DataList s [`DataKeys` 컬렉션이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx) 각 datalist 항목에 대해 지정 된 `DataKeyField` 값으로 채워집니다.
- **[`EditCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx) 는** `CommandName` 속성이 Edit로 설정 된 단추, LinkButton 또는 ImageButton이 클릭 될 때 발생 합니다.
- **[`CancelCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx) 는** `CommandName` 속성이 취소로 설정 된 단추, LinkButton 또는 ImageButton이 클릭 될 때 발생 합니다.
- **[`UpdateCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx) 는** `CommandName` 속성이 업데이트로 설정 되어 있는 단추, LinkButton 또는 ImageButton이 클릭 될 때 발생 합니다.
- **[`DeleteCommand` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx) 는** `CommandName` 속성이 삭제로 설정 된 단추, LinkButton 또는 ImageButton이 클릭 될 때 발생 합니다.

이러한 속성 및 이벤트를 사용 하 여 DataList에서 데이터를 업데이트 하 고 삭제 하는 데 사용할 수 있는 네 가지 방법이 있습니다.

1. **ASP.NET** 1.X를 사용 하면 ASP.NET 2.0 및 ObjectDataSources 원본 이전에 DataList가 존재 하 고 프로그래밍 방식으로 데이터를 완전히 업데이트 하 고 삭제할 수 있었습니다. 이 기법은 ObjectDataSource를 모두 ditches 하 고, 표시할 데이터를 검색 하 고, 레코드를 업데이트 하거나 삭제할 때 비즈니스 논리 계층에서 직접 DataList에 데이터를 바인딩해야 합니다.
2. DataList의 고유 편집 및 삭제 기능을 **선택, 업데이트 및 삭제 하는 데 페이지에서 단일 ObjectDataSource 컨트롤을 사용** 하면 해당 기능을 추가할 수 있는 이유가 없습니다. 이 방법을 사용 하는 경우 GridView 예제에서와 마찬가지로 ObjectDataSource를 사용 하지만, ObjectDataSource s 매개 변수를 설정 하 고 `Update()` 메서드를 호출 하는 DataList s `UpdateCommand` 이벤트에 대 한 이벤트 처리기를 만들어야 합니다.
3. **ObjectDataSource 컨트롤을 사용 하 여 선택 하 고, 옵션 2를 사용할 때 BLL에 대해 직접 업데이트 및 삭제** 하는 경우 `UpdateCommand` 이벤트에서 코드를 작성 하 고 매개 변수 값을 할당 하는 등의 코드를 작성 해야 합니다. 대신, 선택에 대해 ObjectDataSource를 사용 하는 것과 함께 사용할 수 있지만, BLL에 대 한 호출을 직접 업데이트 하 고 삭제 합니다 (예: 옵션 1). 사용자의 의견에 따라 BLL과 직접 상호 작용 하 여 데이터를 업데이트 하면 ObjectDataSource s `UpdateParameters`를 할당 하 고 해당 `Update()` 메서드를 호출 하는 것 보다 더 읽기 쉬운 코드가 됩니다.
4. **여러 ObjectDataSources 원본을 통해 선언적 방법을 사용 하** 는 경우 앞의 세 가지 방법에는 약간의 코드가 필요 합니다. 가능한 한 많은 선언 구문을 계속 사용 하는 경우 마지막 옵션은 페이지에 여러 ObjectDataSources 원본을 포함 하는 것입니다. 첫 번째 ObjectDataSource는 BLL에서 데이터를 검색 하 여 DataList에 바인딩합니다. 업데이트를 위해 다른 ObjectDataSource가 추가 되지만 DataList s `EditItemTemplate`내에서 직접 추가 됩니다. 지원 삭제를 포함 하기 위해 `ItemTemplate`에 다른 ObjectDataSource가 필요 합니다. 이 방법에서는 이러한 포함 된 ObjectDataSource s를 `ControlParameters` 사용 하 여 ObjectDataSource s 매개 변수를 사용자 입력 컨트롤에 선언적으로 바인딩할 수 있습니다 (DataList s `UpdateCommand` 이벤트 처리기에서 프로그래밍 방식으로 지정 하는 대신). 이 방법은 포함 된 ObjectDataSource s `Update()` 또는 `Delete()` 명령을 호출 하는 데 필요한 약간의 코드가 필요 하지만 다른 세 가지 방법 보다 훨씬 더 적습니다. 여기에서 단점은 여러 ObjectDataSources 원본이 전체 가독성에서 detracting 페이지를 복잡 하 게 하는 것입니다.

이러한 방법 중 하나를 사용 하는 경우에만 이러한 방법 중 하나를 사용 하는 것이 가장 유연 하 고 DataList가 원래이 패턴을 수용 하도록 디자인 되었기 때문에 옵션 1을 선택 합니다. ASP.NET 2.0 데이터 소스 컨트롤을 사용 하도록 DataList가 확장 된 동안에는 공식적인 ASP.NET 2.0 데이터 웹 컨트롤 (GridView, DetailsView 및 FormView)의 확장성 지점이 나 기능이 모두 포함 되어 있지 않습니다. 하지만 옵션 2 ~ 4는 가치가 없는 경우에도 그렇지 않습니다.

이 및 이후 자습서 편집 및 삭제에서는 데이터를 검색 하는 데 ObjectDataSource를 사용 하 여 데이터를 업데이트 하 고 삭제할 수 있습니다 (옵션 3).

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>3 단계: DataList 추가 및 ObjectDataSource 구성

이 자습서에서는 제품 정보를 나열 하 고 각 제품에 대해 사용자에 게 이름 및 가격을 편집 하 고 제품을 완전히 삭제 하는 기능을 제공 하는 DataList를 만듭니다. 특히, ObjectDataSource를 사용 하 여 표시할 레코드를 검색 하지만 BLL과 직접 상호 작용 하 여 업데이트 및 삭제 작업을 수행 합니다. DataList에 대 한 편집 및 삭제 기능을 구현 하는 것에 대해 걱정 하기 전에 먼저 페이지를 가져와 읽기 전용 인터페이스에 제품을 표시 해 보겠습니다. 이전 자습서에서 이러한 단계를 검토 했으므로 빠르게 진행 합니다.

먼저 `EditDeleteDataList` 폴더에서 `Basics.aspx` 페이지를 열고 디자인 뷰에서 페이지에 DataList를 추가 합니다. 다음으로, DataList s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 제품 데이터로 작업 하는 중 이므로 `ProductsBLL` 클래스를 사용 하도록 구성 합니다. *모든* 제품을 검색 하려면 선택 탭에서 `GetProducts()` 메서드를 선택 합니다.

[ProductsBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image6.png)

**그림 4**: `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image8.png))

[GetProducts () 메서드를 사용 하 여 제품 정보를 반환 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image9.png)

**그림 5**: `GetProducts()` 메서드를 사용 하 여 제품 정보 반환 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image11.png))

GridView와 마찬가지로 DataList는 새 데이터를 삽입 하기 위해 디자인 되지 않았습니다. 따라서 삽입 탭의 드롭다운 목록에서 (없음) 옵션을 선택 합니다. 업데이트 및 삭제가 BLL을 통해 프로그래밍 방식으로 수행 되므로 업데이트 및 삭제 탭에서 (없음)을 선택 합니다.

[ObjectDataSource의 삽입, 업데이트 및 삭제 탭에 있는 드롭다운 목록이 (없음)로 설정 되어 있는지 확인 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image12.png)

**그림 6**: OBJECTDATASOURCE의 삽입, 업데이트 및 삭제 탭에 있는 드롭다운 목록이 (없음)로 설정 되었는지 확인 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image14.png))

ObjectDataSource를 구성한 후 마침을 클릭 하 여 디자이너로 돌아갑니다. 이전 예제에서 살펴본 것 처럼 ObjectDataSource 구성을 완료할 때 Visual Studio에서는 각 데이터 필드를 표시 하는 DropDownList에 대 한 `ItemTemplate`를 자동으로 만듭니다. 이 `ItemTemplate`를 제품 이름 및 가격만 표시 하는 것으로 바꿉니다. 또한 `RepeatColumns` 속성을 2로 설정 합니다.

> [!NOTE]
> *데이터 삽입, 업데이트 및 삭제* 자습서의 개요에서 설명 했 듯이 objectdatasource를 사용 하 여 데이터를 수정 하는 경우에는 objectdatasource의 선언적 태그에서 `OldValuesParameterFormatString` 속성을 제거 해야 합니다 (또는 `{0}`기본값으로 다시 설정). 그러나이 자습서에서는 데이터 검색에만 ObjectDataSource를 사용 합니다. 따라서 ObjectDataSource s `OldValuesParameterFormatString` 속성 값을 수정할 필요가 없습니다 (이 작업을 수행 하지는 않음).

기본 DataList `ItemTemplate`를 사용자 지정 된 것으로 바꾸면 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample2.aspx)]

잠시 시간을 내 서 브라우저를 통해 진행 상황을 확인 하세요. 그림 7에 표시 된 것 처럼 DataList는 두 열의 제품 이름 및 단가를 표시 합니다.

[두 열 DataList에 제품 이름 및 가격이 표시 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image15.png)

**그림 7**: 제품 이름과 가격은 2 열 DataList에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image17.png)).

> [!NOTE]
> DataList에는 업데이트 및 삭제 프로세스에 필요한 여러 속성이 있으며 이러한 값이 뷰 상태에 저장 됩니다. 따라서 데이터 편집 또는 삭제를 지 원하는 DataList를 빌드하는 경우에는 DataList s 뷰 상태를 설정 하는 것이 중요 합니다.  
>   
> Astute reader는 편집 가능한 GridViews, DetailsViews 및 FormViews를 만들 때 뷰 상태를 사용 하지 않도록 설정할 수 있음을 회수할 수 있습니다. 이는 ASP.NET 2.0 웹 컨트롤에 뷰 상태와 같은 다시 게시 간에 상태를 유지 하지만 필수적인 것으로 간주 되는 *컨트롤 상태*를 포함할 수 있기 때문입니다.

GridView에서 뷰 상태를 사용 하지 않도록 설정 하면 단순한 상태 정보는 생략 되지만 편집 및 삭제에 필요한 상태를 포함 하는 컨트롤 상태를 유지 관리 합니다. ASP.NET 1.x 시간 범위에서 만들어진 DataList는 컨트롤 상태를 활용 하지 않으므로 뷰 상태를 사용 하도록 설정 해야 합니다. 컨트롤 상태 및 뷰 상태와의 차이점에 대 한 자세한 내용은 [컨트롤 상태 및 뷰 상태](https://msdn.microsoft.com/library/1whwt1k7.aspx) 를 참조 하세요.

## <a name="step-4-adding-an-editing-user-interface"></a>4 단계: 편집 사용자 인터페이스 추가

GridView 컨트롤은 필드의 컬렉션 (BoundFields, CheckBoxFields, 템플릿 필드 등)으로 구성 됩니다. 이러한 필드는 모드에 따라 렌더링 된 태그를 조정할 수 있습니다. 예를 들어 읽기 전용 모드에서 BoundField은 데이터 필드 값을 텍스트로 표시 합니다. 편집 모드에서는 `Text` 속성에 데이터 필드 값이 할당 된 TextBox 웹 컨트롤을 렌더링 합니다.

반면에 DataList는 템플릿을 사용 하 여 해당 항목을 렌더링 합니다. 읽기 전용 항목은 `ItemTemplate`를 사용 하 여 렌더링 되는 반면 편집 모드의 항목은 `EditItemTemplate`를 통해 렌더링 됩니다. 이 시점에서 DataList에는 `ItemTemplate`있습니다. 항목 수준 편집 기능을 지원 하려면 편집 가능한 항목에 대해 표시할 태그를 포함 하는 `EditItemTemplate`를 추가 해야 합니다. 이 자습서에서는 제품 이름 및 단가를 편집 하기 위해 TextBox 웹 컨트롤을 사용 합니다.

`EditItemTemplate`은 선언적으로 또는 디자이너를 통해 만들 수 있습니다 (DataList의 스마트 태그에서 템플릿 편집 옵션을 선택 하 여). 템플릿 편집 옵션을 사용 하려면 먼저 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 드롭다운 목록에서 `EditItemTemplate` 항목을 선택 합니다.

[![DataList s EditItemTemplate 작업을 수행 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image18.png)

**그림 8**: DataList s `EditItemTemplate` 작업 옵트인 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image20.png))

그런 다음 Product name: 및 Price:를 입력 하 고 도구 상자에서 두 TextBox 컨트롤을 디자이너의 `EditItemTemplate` 인터페이스로 끌어 옵니다. 텍스트 상자 `ID` 속성을 `ProductName`로 설정 하 고 `UnitPrice`합니다.

[제품 이름 및 가격에 대 한 텍스트 상자를 추가 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image21.png)

**그림 9**: 제품 이름 및 가격에 대 한 텍스트 상자 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image23.png))

해당 제품 데이터 필드 값을 두 텍스트 상자의 `Text` 속성에 바인딩해야 합니다. 그림 10에 표시 된 것 처럼 텍스트 상자 스마트 태그에서 데이터 바인딩 편집 링크를 클릭 하 고 적절 한 데이터 필드를 `Text` 속성에 연결 합니다.

> [!NOTE]
> `UnitPrice` 데이터 필드를 price TextBox s `Text` 필드에 바인딩하는 경우 통화 값 (`{0:C}`) 또는 일반 숫자 (`{0:N}`)로 서식을 지정 하거나 서식 지정을 그대로 유지할 수 있습니다.

![ProductName 및 UnitPrice 데이터 필드를 텍스트 상자의 텍스트 속성에 바인딩](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image24.png)

**그림 10**: `ProductName` 및 `UnitPrice` 데이터 필드를 텍스트 상자의 `Text` 속성에 바인딩

그림 10의 데이터 바인딩 편집 대화 상자에는 GridView 또는 DetailsView에서 Templatefield로 변환를 편집할 때 표시 되는 양방향 데이터 바인딩 확인란이 포함 되어 *있지* 않습니다. 양방향 데이터 바인딩 기능을 통해 입력 웹 컨트롤에 입력 한 값이 해당 ObjectDataSource s `InsertParameters`에 자동으로 할당 되거나 데이터를 삽입 하거나 업데이트할 때 `UpdateParameters` 수 있습니다. DataList는이 자습서의 뒷부분에서 볼 수 있듯이 양방향 데이터 바인딩을 지원 하지 않습니다. 사용자가 변경을 수행 하 고 데이터를 업데이트할 준비가 된 후에는 프로그래밍 방식으로 이러한 텍스트 `Text` 상자에 액세스 하 고 해당 값을 `ProductsBLL` 클래스의 적절 한 `UpdateProduct` 메서드에 전달 해야 합니다.

마지막으로 `EditItemTemplate`에 업데이트 및 취소 단추를 추가 해야 합니다. 정보 DataList 자습서를 사용 [하 여 마스터 레코드의 글머리 기호 목록을 사용 하 여 마스터/세부 정보](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) 에서 살펴본 것 처럼 `CommandName` 속성이 설정 된 단추, LinkButton 또는 ImageButton을 Repeater 또는 datalist 내에서 클릭 하면 Repeater 또는 datalist s `ItemCommand` 이벤트가 발생 합니다. DataList의 경우 `CommandName` 속성이 특정 값으로 설정 된 경우에도 추가 이벤트가 발생할 수 있습니다. 특수 `CommandName` 속성 값에는 다른 값이 포함 됩니다.

- Cancel `CancelCommand` 이벤트를 발생 시킵니다.
- 편집 `EditCommand` 이벤트를 발생 시킵니다.
- 업데이트는 `UpdateCommand` 이벤트를 발생 시킵니다.

이러한 이벤트는 `ItemCommand` 이벤트 *와 함께* 발생 합니다.

`CommandName`를 업데이트 하도록 설정 하 고 다른 s를 취소로 설정 하는 두 개의 단추 웹 컨트롤 `EditItemTemplate`에 추가 합니다. 이러한 두 단추 웹 컨트롤을 추가한 후 디자이너는 다음과 같이 표시 됩니다.

[EditItemTemplate에 업데이트 및 취소 단추를 추가 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image25.png)

**그림 11**: `EditItemTemplate`에 업데이트 및 취소 단추 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image27.png))

`EditItemTemplate` 완료 되 면 DataList s 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>5 단계: 시작 편집 모드로 배관 추가

이 시점에서 DataList는 `EditItemTemplate`를 통해 정의 된 편집 인터페이스를 포함 합니다. 그러나 현재 사용자가 페이지를 방문 하 여 제품 정보를 편집 하 고 있음을 나타낼 수 있는 방법은 없습니다. 클릭 하면 편집 모드에서 DataList 항목을 렌더링 하는 각 제품에 편집 단추를 추가 해야 합니다. 디자이너를 통해 또는 선언적으로 편집 단추를 `ItemTemplate`에 추가 하 여 시작 합니다. 편집 단추 s `CommandName` 속성을 편집으로 설정 해야 합니다.

이 편집 단추를 추가한 후 잠시 시간을 내 서 브라우저를 통해 페이지를 봅니다. 또한 각 제품 목록에는 편집 단추가 포함 됩니다.

[EditItemTemplate에 업데이트 및 취소 단추를 추가 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image28.png)

**그림 12**: `EditItemTemplate`에 업데이트 및 취소 단추 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image30.png))

단추를 클릭 하면 포스트백이 발생 하지만 제품 목록을 편집 모드로 전환 *하지* 는 않습니다. 제품을 편집 가능 하 게 만들려면 다음을 수행 해야 합니다.

1. DataList s [`EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 을 편집 단추를 방금 클릭 한 `DataListItem`의 인덱스로 설정 합니다.
2. 데이터를 DataList에 다시 바인딩합니다. DataList가 다시 렌더링 되 면 `ItemIndex` `EditItemIndex` DataList s에 해당 하는 `DataListItem` `EditItemTemplate`를 사용 하 여 렌더링 됩니다.

편집 단추를 클릭할 때 DataList s `EditCommand` 이벤트가 발생 하므로 다음 코드를 사용 하 여 `EditCommand` 이벤트 처리기를 만듭니다.

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample4.cs)]

`EditCommand` 이벤트 처리기는 `DataListCommandEventArgs` 형식의 개체에서 두 번째 입력 매개 변수로 전달 됩니다. 여기에는 편집 단추가 클릭 된 `DataListItem`에 대 한 참조 (`e.Item`)가 포함 됩니다. 이벤트 처리기는 먼저 DataList s `EditItemIndex`를 편집 가능한 `DataListItem` `ItemIndex`으로 설정한 다음 DataList s `DataBind()` 메서드를 호출 하 여 데이터를 DataList에 다시 바인딩합니다.

이 이벤트 처리기를 추가한 후 브라우저에서 페이지를 다시 방문 합니다. [편집] 단추를 클릭 하면 클릭 된 제품을 편집할 수 있게 됩니다 (그림 13 참조).

[편집 단추를 클릭 하면 제품을 편집할 수 있게 됩니다 ![](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image31.png)

**그림 13**: 편집 단추를 클릭 하면 제품을 편집할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image33.png)).

## <a name="step-6-saving-the-user-s-changes"></a>6 단계: 사용자 변경 내용 저장

이 시점에서는 편집 된 제품의 업데이트 또는 취소 단추를 클릭 해도 아무 작업도 수행 되지 않습니다. 이 기능을 추가 하려면 DataList s `UpdateCommand`에 대 한 이벤트 처리기를 만들고 이벤트를 `CancelCommand` 해야 합니다. 편집 된 제품의 취소 단추를 클릭할 때 실행 되는 `CancelCommand` 이벤트 처리기를 만들고 DataList를 미리 편집 상태로 되돌리는 것이 좋습니다.

DataList가 읽기 전용 모드에서 모든 항목을 렌더링 하도록 하려면 다음을 수행 해야 합니다.

1. DataList s [`EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 을 존재 하지 않는 `DataListItem` 인덱스의 인덱스로 설정 합니다. `DataListItem` 인덱스가 `0`에서 시작 되기 때문에 `-1`은 안전 하 게 선택할 수 있습니다.
2. 데이터를 DataList에 다시 바인딩합니다. `DataListItem` `ItemIndex`는 DataList s `EditItemIndex`에 해당 하므로 전체 DataList는 읽기 전용 모드에서 렌더링 됩니다.

다음 이벤트 처리기 코드를 사용 하 여 이러한 단계를 수행할 수 있습니다.

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample5.cs)]

이 외에도 취소 단추를 클릭 하면 DataList가 사전 편집 상태로 돌아갑니다.

완료 해야 하는 마지막 이벤트 처리기는 `UpdateCommand` 이벤트 처리기입니다. 이 이벤트 처리기는 다음을 수행 해야 합니다.

1. 사용자가 입력 한 제품 이름과 가격 뿐만 아니라 편집 된 제품 `ProductID`에 프로그래밍 방식으로 액세스 합니다.
2. `ProductsBLL` 클래스에서 적절 한 `UpdateProduct` 오버 로드를 호출 하 여 업데이트 프로세스를 시작 합니다.
3. DataList s [`EditItemIndex` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx) 을 존재 하지 않는 `DataListItem` 인덱스의 인덱스로 설정 합니다. `DataListItem` 인덱스가 `0`에서 시작 되기 때문에 `-1`은 안전 하 게 선택할 수 있습니다.
4. 데이터를 DataList에 다시 바인딩합니다. `DataListItem` `ItemIndex`는 DataList s `EditItemIndex`에 해당 하므로 전체 DataList는 읽기 전용 모드에서 렌더링 됩니다.

1 단계와 2 단계는 사용자의 변경 내용을 저장 하는 작업을 담당 합니다. 3 단계와 4 단계는 변경 내용이 저장 되 고 `CancelCommand` 이벤트 처리기에서 수행 되는 단계와 동일한 경우 DataList를 미리 편집 상태로 되돌립니다.

업데이트 된 제품 이름 및 가격을 얻으려면 `FindControl` 메서드를 사용 하 여 `EditItemTemplate`내에서 TextBox 웹 컨트롤을 프로그래밍 방식으로 참조 해야 합니다. 또한 편집 된 제품 `ProductID` 값을 가져와야 합니다. 처음에 ObjectDataSource를 DataList에 바인딩하는 경우 Visual Studio에서 DataList s `DataKeyField` 속성을 데이터 소스의 기본 키 값 (`ProductID`)에 할당 합니다. 그런 다음이 값을 DataList s `DataKeys` 컬렉션에서 검색할 수 있습니다. 잠시 `DataKeyField` 속성이 `ProductID`로 설정 되었는지 확인 합니다.

다음 코드는 네 단계를 구현 합니다.

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample6.cs)]

이벤트 처리기는 `DataKeys` 컬렉션에서 편집 된 제품 `ProductID`을 읽어 시작 합니다. 그런 다음 `EditItemTemplate`의 두 텍스트 상자가 참조 되 고 `Text` 속성은 지역 변수 `productNameValue` 및 `unitPriceValue`에 저장 됩니다. `Decimal.Parse()` 메서드를 사용 하 여 `UnitPrice` 텍스트 상자에서 값을 읽을 수 있습니다. 그러면 입력 된 값에 통화 기호가 포함 된 경우에도 `Decimal` 값으로 올바르게 변환 될 수 있습니다.

> [!NOTE]
> 텍스트 상자 텍스트 속성에 값이 지정 된 경우에만 `ProductName` 및 `UnitPrice` 텍스트 상자의 값이 productNameValue 및 unitPriceValue 변수에 할당 됩니다. 그렇지 않으면 `Nothing`의 값이 변수에 사용 됩니다 .이 값은 데이터베이스 `NULL` 값으로 데이터를 업데이트 하는 효과가 있습니다. 즉, 코드에서 빈 문자열을 GridView, DetailsView 및 FormView 컨트롤의 편집 인터페이스에 대 한 기본 동작인 데이터베이스 `NULL` 값으로 변환 합니다.

값을 읽은 후에는 제품 이름, 가격 및 `ProductID`를 전달 하 여 `ProductsBLL` 클래스 s `UpdateProduct` 메서드가 호출 됩니다. 이벤트 처리기는 `CancelCommand` 이벤트 처리기와 정확히 동일한 논리를 사용 하 여 DataList를 사전 편집 상태로 반환 하 여 완료 합니다.

`EditCommand`, `CancelCommand`및 `UpdateCommand` 이벤트 처리기가 완료 되 면 방문자는 제품의 이름과 가격을 편집할 수 있습니다. 그림 14-16에서는이 편집 워크플로를 실행 중인 것으로 표시 합니다.

[페이지를 처음 방문할 때 ![모든 제품이 읽기 전용 모드입니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image34.png)

**그림 14**: 페이지를 처음 방문할 때 모든 제품이 읽기 전용 모드에 있습니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image36.png)).

[제품 이름 또는 가격을 업데이트 ![편집 단추를 클릭 합니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image37.png)

**그림 15**: 제품 이름 또는 가격을 업데이트 하려면 편집 단추를 클릭 합니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image39.png)).

[값을 변경한 후 ![업데이트를 클릭 하 여 읽기 전용 모드로 돌아갑니다.](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image40.png)

**그림 16**: 값을 변경한 후 업데이트를 클릭 하 여 읽기 전용 모드로 돌아갑니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image42.png)).

## <a name="step-7-adding-delete-capabilities"></a>7 단계: 삭제 기능 추가

DataList에 삭제 기능을 추가 하는 단계는 편집 기능을 추가 하는 단계와 비슷합니다. 간단히 클릭 하면 `ItemTemplate`에 삭제 단추를 추가 해야 합니다.

1. `DataKeys` 컬렉션을 통해 해당 제품 `ProductID`을 읽습니다.
2. `ProductsBLL` 클래스 `DeleteProduct` 메서드를 호출 하 여 삭제를 수행 합니다.
3. 데이터를 DataList에 다시 바인딩합니다.

`ItemTemplate`에 삭제 단추를 추가 하 여를 시작 하겠습니다.

이 단추를 클릭 하면 편집, 업데이트 또는 취소 `CommandName` 있는 단추가 추가 이벤트와 함께 DataList s `ItemCommand` 이벤트를 발생 시킵니다. 예를 들어 `EditCommand` 이벤트를 사용 하는 경우에도이 이벤트가 발생 합니다. 마찬가지로 `CommandName` 속성이 Delete로 설정 되어 있는 DataList의 단추, LinkButton 또는 ImageButton은 `ItemCommand`와 함께 `DeleteCommand` 이벤트를 발생 시킵니다.

`ItemTemplate`의 편집 단추 옆에 있는 삭제 단추를 추가 하 여 `CommandName` 속성을 Delete로 설정 합니다. 이 단추를 추가한 후에는 DataList s `ItemTemplate` 선언 구문이 다음과 같이 표시 됩니다.

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample7.aspx)]

다음으로 다음 코드를 사용 하 여 DataList s `DeleteCommand` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample8.cs)]

삭제 단추를 클릭 하면 포스트백이 발생 하 고 DataList s `DeleteCommand` 이벤트가 발생 합니다. 이벤트 처리기에서 클릭 한 제품 `ProductID` 값은 `DataKeys` 컬렉션에서 액세스할 수 있습니다. 그런 다음 `ProductsBLL` 클래스 `DeleteProduct` 메서드를 호출 하 여 제품을 삭제 합니다.

제품을 삭제 한 후에는 데이터를 DataList (`DataList1.DataBind()`)에 다시 바인딩하는 것이 중요 합니다. 그렇지 않으면 DataList가 방금 삭제 된 제품을 계속 표시 합니다.

## <a name="summary"></a>요약

DataList에는 점이 없고 GridView에서 사용할 수 있는 지원 삭제를 클릭 하 고 편집을 클릭 하 여 이러한 기능을 포함 하도록 확장 될 수 있습니다. 이 자습서에서는 삭제할 수 있고 이름과 가격을 편집할 수 있는 두 개의 열로 이루어진 제품 목록을 만드는 방법에 대해 살펴보았습니다. 편집 및 삭제 지원을 추가 하는 것은 `ItemTemplate` 및 `EditItemTemplate`에 적절 한 웹 컨트롤을 포함 하 고, 해당 이벤트 처리기를 만들고, 사용자 입력 및 기본 키 값을 읽고, 비즈니스 논리 계층과 상호 작용 하는 것입니다.

DataList에 기본 편집 및 삭제 기능을 추가 했지만 고급 기능이 부족 합니다. 예를 들어 입력 필드 유효성 검사가 없습니다. 사용자가 너무 비싼 가격을 입력 하는 경우에는 너무 많은 비용이 `Decimal`으로 변환 하려고 할 때 `Decimal.Parse`에서 예외가 throw 됩니다. 마찬가지로 비즈니스 논리 또는 데이터 액세스 계층에서 데이터를 업데이트 하는 데 문제가 있는 경우 사용자에 게 표준 오류 화면이 표시 됩니다. 삭제 단추에 대 한 일종의 확인 없이 제품을 실수로 삭제 하는 것은 모두 너무 많습니다.

이후 자습서에서는 편집 사용자 환경을 개선 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones, 켄은 Pespisa 및 Randy Schmidt입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](performing-batch-updates-cs.md)
