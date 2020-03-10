---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
title: 콘텐츠 페이지에서 컨트롤 ID 이름 지정C#() | Microsoft Docs
author: rick-anderson
description: ContentPlaceHolder 컨트롤이 명명 컨테이너 역할을 하 여 프로그래밍 방식으로 컨트롤 작업을 어렵게 만드는 방법을 보여 줍니다 (FindControl를 통해).
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 1c7d0916-0988-4b4f-9a03-935e4b5af6af
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: e849e5860dc988e112cc3a65d976c16ecdf77416
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520187"
---
# <a name="control-id-naming-in-content-pages-c"></a>콘텐츠 페이지에서 컨트롤 ID 이름 지정(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_CS.pdf)

> ContentPlaceHolder 컨트롤이 명명 컨테이너 역할을 하 여 프로그래밍 방식으로 컨트롤을 사용 하기 어렵게 만드는 방법을 보여 줍니다 (FindControl를 통해). 이 문제와 해결 방법을 살펴봅니다. 또한 결과 ClientID 값에 프로그래밍 방식으로 액세스 하는 방법을 설명 합니다.

## <a name="introduction"></a>소개

모든 ASP.NET 서버 컨트롤에는 컨트롤을 고유 하 게 식별 하는 `ID` 속성이 포함 되며, 코드를 사용 하는 클래스에서 프로그래밍 방식으로 컨트롤에 액세스 하는 방법입니다. 마찬가지로 HTML 문서의 요소는 요소를 고유 하 게 식별 하는 `id` 특성을 포함할 수 있습니다. 이러한 `id` 값은 종종 클라이언트 쪽 스크립트에서 특정 HTML 요소를 프로그래밍 방식으로 참조 하는 데 사용 됩니다. 이 경우 ASP.NET 서버 컨트롤이 HTML로 렌더링 될 때 `ID` 값이 렌더링 된 HTML 요소의 `id` 값으로 사용 된다고 가정할 수 있습니다. 특정 상황에서는 렌더링 된 태그에서 단일 `ID` 값이 포함 된 단일 컨트롤이 여러 번 나타날 수 있기 때문에이는 반드시 그럴 필요는 없습니다. `ID` 값이 ProductName 인 레이블 웹 컨트롤과 함께 Templatefield로 변환를 포함 하는 GridView 컨트롤을 사용 합니다. GridView가 런타임에 데이터 원본에 바인딩되면이 레이블은 모든 GridView 행에 대해 한 번씩 반복 됩니다. 렌더링 된 각 레이블에는 고유한 `id` 값이 필요 합니다.

이러한 시나리오를 처리 하기 위해 ASP.NET를 사용 하면 특정 컨트롤을 명명 컨테이너로 표시할 수 있습니다. 명명 컨테이너는 새 `ID` 네임 스페이스로 사용 됩니다. 명명 컨테이너 내에 표시 되는 모든 서버 컨트롤에는 명명 컨테이너 컨트롤의 `ID` 접두사로 붙는 렌더링 된 `id` 값이 있습니다. 예를 들어 `GridView` 및 `GridViewRow` 클래스는 둘 다 명명 컨테이너입니다. 따라서 `ID` ProductName을 사용 하 여 GridView Templatefield로 변환에 정의 된 레이블 컨트롤에는 `GridViewID_GridViewRowID_ProductName`의 렌더링 `id` 값이 지정 됩니다. *GridViewRowID* 는 각 GridView 행에 대해 고유 하기 때문에 결과 `id` 값은 고유 합니다.

> [!NOTE]
> [`INamingContainer` 인터페이스](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx) 는 특정 ASP.NET 서버 컨트롤이 명명 컨테이너 역할을 하도록 지정 하는 데 사용 됩니다. `INamingContainer` 인터페이스는 서버 컨트롤에서 구현 해야 하는 메서드를 검사 하지 않습니다. 대신 마커로 사용 됩니다. 렌더링 된 태그를 생성할 때 컨트롤이이 인터페이스를 구현 하는 경우 ASP.NET 엔진은 자동으로 해당 `ID` 값에 해당 하위의 렌더링 된 `id` 특성 값에 접두사를 붙입니다. 이 프로세스는 2 단계에 자세히 설명 되어 있습니다.

명명 컨테이너는 렌더링 된 `id` 특성 값을 변경할 뿐만 아니라 컨트롤을 프로그래밍 방식으로 ASP.NET 페이지의 코드 숨김이 클래스에서 참조할 수 있는 방법에도 영향을 줍니다. `FindControl("controlID")` 메서드는 일반적으로 웹 컨트롤을 프로그래밍 방식으로 참조 하는 데 사용 됩니다. 그러나 `FindControl`은 명명 컨테이너를 통해 침투 하지 않습니다. 따라서 GridView 또는 다른 명명 컨테이너 내의 컨트롤을 참조 하는 데 `Page.FindControl` 메서드를 직접 사용할 수 없습니다.

Surmised 수 있듯이 마스터 페이지와 ContentPlaceHolders 표시자는 모두 명명 컨테이너로 구현 됩니다. 이 자습서에서는 마스터 페이지가 `FindControl`를 사용 하 여 콘텐츠 페이지 내에서 프로그래밍 방식으로 웹 컨트롤을 참조 하는 `id` 값 및 방법에 영향을 줍니다.

## <a name="step-1-adding-a-new-aspnet-page"></a>1 단계: 새 ASP.NET 페이지 추가

이 자습서에서 설명 하는 개념을 설명 하기 위해 웹 사이트에 새 ASP.NET 페이지를 추가 해 보겠습니다. 루트 폴더에 `IDIssues.aspx` 라는 새 콘텐츠 페이지를 만들어 `Site.master` 마스터 페이지에 바인딩합니다.

![콘텐츠 페이지 IDIssues를 루트 폴더에 추가 합니다.](control-id-naming-in-content-pages-cs/_static/image1.png)

**그림 01**: 루트 폴더에 `IDIssues.aspx` 콘텐츠 페이지 추가

Visual Studio는 각 마스터 페이지의 4 개 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤을 자동으로 만듭니다. [*여러 ContentPlaceHolders 표시자 및 기본 콘텐츠*](multiple-contentplaceholders-and-default-content-cs.md) 자습서에 설명 된 대로 콘텐츠 컨트롤이 표시 되지 않는 경우 마스터 페이지의 기본 ContentPlaceHolder 콘텐츠를 대신 내보냅니다. `QuickLoginUI` 및 `LeftColumnContent` ContentPlaceHolders 표시자에는이 페이지에 적합 한 기본 태그가 포함 되어 있으므로 `IDIssues.aspx`에서 해당 콘텐츠 컨트롤을 제거 하세요. 이 시점에서 콘텐츠 페이지의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample1.aspx)]

[*마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) 자습서에서 명시적으로 설정 하지 않은 경우 페이지의 제목을 자동으로 구성 하는 사용자 지정 기본 페이지 클래스 (`BasePage`)를 만들었습니다. `IDIssues.aspx` 페이지에서이 기능을 사용 하려면 페이지의 코드 숨김이 `BasePage` 클래스 (`System.Web.UI.Page`대신)에서 파생 되어야 합니다. 다음과 같이 코드를 정의 하는 클래스의 정의를 수정 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample2.cs)]

마지막으로이 새 단원에 대 한 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. `<siteMapNode>` 요소를 추가 하 고 `title` 및 `url` 특성을 각각 "Control ID 명명 문제" 및 `~/IDIssues.aspx`로 설정 합니다. 이러한 추가 작업을 수행한 후 `Web.sitemap` 파일의 태그가 다음과 같이 표시 됩니다.

[!code-xml[Main](control-id-naming-in-content-pages-cs/samples/sample3.xml)]

그림 2에 나와 있는 것 처럼 `Web.sitemap`의 새 사이트 맵 항목이 왼쪽 열에 있는 단원 섹션에 즉시 반영 됩니다.

![이제 단원 섹션에 &quot;컨트롤 ID 명명 문제에 대 한 링크가 포함 되어&quot;](control-id-naming-in-content-pages-cs/_static/image2.png)

**그림 02**: 단원 섹션에는 이제 "컨트롤 ID 명명 문제"에 대 한 링크가 포함 되어 있습니다.

## <a name="step-2-examining-the-renderedidchanges"></a>2 단계: 렌더링 된`ID`변경 내용 검사

ASP.NET 엔진이 서버 컨트롤의 렌더링 된 `id` 값에 대해 수행 하는 수정 사항을 더 잘 이해 하려면 `IDIssues.aspx` 페이지에 몇 가지 웹 컨트롤을 추가한 다음 브라우저에 전송 된 렌더링 된 태그를 확인 합니다. 특히 텍스트를 입력 하 고 텍스트 상자에 텍스트를 입력 하십시오. 페이지의 아래쪽에서 단추 웹 컨트롤과 Label 웹 컨트롤을 추가 합니다. 텍스트 상자의 `ID`와 `Columns` 속성을 각각 `Age` 및 3으로 설정 합니다. 단추의 `Text` 및 `ID` 속성을 "Submit"로 설정 하 고 `SubmitButton`합니다. 레이블의 `Text` 속성을 지우고 `ID`를 `Results`로 설정 합니다.

이 시점에서 콘텐츠 컨트롤의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample4.aspx)]

그림 3에서는 Visual Studio의 디자이너를 통해 볼 때의 페이지를 보여 줍니다.

[페이지에는 텍스트 상자, 단추 및 레이블의 세 가지 웹 컨트롤이 포함 ![합니다.](control-id-naming-in-content-pages-cs/_static/image4.png)](control-id-naming-in-content-pages-cs/_static/image3.png)

**그림 03**: 페이지에는 텍스트 상자, 단추 및 레이블의 세 가지 웹 컨트롤 ([전체 크기의 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image5.png))이 포함 되어 있습니다.

브라우저를 통해 페이지를 방문 하 여 HTML 소스를 봅니다. 아래 태그가 보여 주는 것 처럼 텍스트 상자, 단추 및 레이블 웹 컨트롤에 대 한 HTML 요소의 `id` 값은 웹 컨트롤의 `ID` 값과 페이지의 명명 컨테이너에 대 한 `ID` 값의 조합입니다.

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample5.html)]

이 자습서의 앞부분에서 설명한 것 처럼 마스터 페이지와 ContentPlaceHolders 표시자는 모두 명명 컨테이너 역할을 합니다. 따라서 둘 다 렌더링 된 `ID` 값을 중첩 된 컨트롤에 적용 합니다. 텍스트 상자의 `id` 특성을 사용 합니다 (예: `ctl00_MainContent_Age`). TextBox 컨트롤의 `ID` 값이 `Age`되었음을 기억 합니다. ContentPlaceHolder 컨트롤의 `ID` 값 `MainContent`접두사가 붙습니다. 또한이 값에는 마스터 페이지의 `ID` 값 `ctl00`접두사가 붙습니다. Net 효과는 마스터 페이지의 `ID` 값, ContentPlaceHolder 컨트롤 및 텍스트 상자 자체로 구성 된 `id` 특성 값입니다.

그림 4에서는이 동작을 보여 줍니다. `Age` 텍스트 상자의 렌더링 된 `id`를 확인 하려면 TextBox 컨트롤의 `ID` 값 `Age`를 사용 하 여 시작 합니다. 다음으로 컨트롤 계층 구조를 사용 합니다. 각 명명 컨테이너 (복숭아색 색이 있는 노드)에서 현재 렌더링 된 `id` 명명 컨테이너의 `id`접두사로 지정 합니다.

![렌더링 된 id 특성은 명명 컨테이너의 ID 값을 기반으로 합니다.](control-id-naming-in-content-pages-cs/_static/image6.png)

**그림 04**: 렌더링 된 `id` 특성은 명명 컨테이너의 `ID` 값을 기반으로 합니다.

> [!NOTE]
> 앞서 설명 했 듯이 렌더링 된 `id` 특성의 `ctl00` 부분은 마스터 페이지의 `ID` 값을 구성 하지만이 `ID` 값의 출처를 궁금할 수 있습니다. 마스터 또는 콘텐츠 페이지에서 아무 곳 이나 지정 하지 않았습니다. ASP.NET 페이지의 대부분 서버 컨트롤은 페이지의 선언적 태그를 통해 명시적으로 추가 됩니다. `MainContent` ContentPlaceHolder 컨트롤이 `Site.master`의 태그에 명시적으로 지정 되었습니다. `Age` 텍스트 상자가 태그 `IDIssues.aspx`정의 되었습니다. 속성 창 또는 선언적 구문을 통해 이러한 컨트롤 형식에 대 한 `ID` 값을 지정할 수 있습니다. 마스터 페이지 자체와 같은 다른 컨트롤은 선언적 태그에 정의 되어 있지 않습니다. 따라서 해당 `ID` 값이 자동으로 생성 되어야 합니다. ASP.NET 엔진은 Id가 명시적으로 설정 되지 않은 컨트롤에 대해 런타임에 `ID` 값을 설정 합니다. 명명 패턴 `ctlXX`를 사용 합니다. 여기서 *XX* 는 순차적으로 늘어나는 정수 값입니다.

마스터 페이지 자체가 명명 컨테이너 역할을 하기 때문에 마스터 페이지에 정의 된 웹 컨트롤은 특성 값 `id` 렌더링 된 것으로 변경 되었습니다. 예를 들어 마스터 페이지를 [*사용 하 여 사이트 전체 레이아웃 만들기*](creating-a-site-wide-layout-using-master-pages-cs.md) 자습서에서 마스터 페이지에 추가한 `DisplayDate` 레이블은 다음과 같이 렌더링 된 태그를 가집니다.

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample6.html)]

`id` 특성에는 마스터 페이지의 `ID` 값 (`ctl00`)과 레이블 웹 컨트롤 (`DateDisplay`)의 `ID` 값이 모두 포함 되어 있습니다.

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>3 단계:`FindControl`를 통해 프로그래밍 방식으로 웹 컨트롤 참조

모든 ASP.NET 서버 컨트롤에는 컨트롤의 하위 항목에서 *controlID*라는 컨트롤을 검색 하는 `FindControl("controlID")` 메서드가 포함 되어 있습니다. 이러한 컨트롤이 있는 경우 반환 됩니다. 일치 하는 컨트롤이 없으면 `FindControl`에서 `null`를 반환 합니다.

`FindControl`은 컨트롤에 액세스 해야 하지만 직접 참조 하지 않는 시나리오에서 유용 합니다. 예를 들어 GridView와 같은 데이터 웹 컨트롤을 사용할 때 GridView의 필드 내에 있는 컨트롤은 선언적 구문에서 한 번 정의 되지만 런타임에는 각 GridView 행에 대해 컨트롤의 인스턴스가 생성 됩니다. 따라서 런타임에 생성 된 컨트롤은 있지만 코드 숨김이 아닌 클래스에서 직접 참조를 사용할 수 없습니다. 따라서 `FindControl`를 사용 하 여 GridView의 필드 내에서 특정 컨트롤을 프로그래밍 방식으로 작업 해야 합니다. `FindControl` 사용 하 여 데이터 웹 컨트롤의 템플릿 내에서 컨트롤에 액세스 하는 방법에 대 한 자세한 내용은 [데이터를 기반으로 하는 사용자 지정 서식 지정](../../data-access/custom-formatting/custom-formatting-based-upon-data-cs.md)을 참조 하세요. 이 시나리오는 웹 컨트롤을 웹 폼에 동적으로 추가 하는 경우에 발생 합니다 .이 항목에서는 [Dynamic Data 항목 사용자 인터페이스 만들기](https://msdn.microsoft.com/library/aa479330.aspx)에 설명 되어 있습니다.

`FindControl` 메서드를 사용 하 여 콘텐츠 페이지에서 컨트롤을 검색 하는 방법을 보여 주려면 `SubmitButton`의 `Click` 이벤트에 대 한 이벤트 처리기를 만듭니다. 이벤트 처리기에서 다음 코드를 추가 합니다 .이 코드는 `FindControl` 메서드를 사용 하 여 프로그래밍 방식으로 `Age` TextBox 및 `Results` 레이블을 참조 하 고 사용자의 입력에 따라 `Results`에 메시지를 표시 합니다.

> [!NOTE]
> 물론이 예제에서는 `FindControl`를 사용 하 여 레이블 및 TextBox 컨트롤을 참조할 필요가 없습니다. `ID` 속성 값을 통해 직접 참조할 수 있습니다. 여기서 `FindControl`를 사용 하 여 콘텐츠 페이지에서 `FindControl`를 사용할 때 발생 하는 상황을 설명 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample7.cs)]

`FindControl` 메서드를 호출 하는 데 사용 되는 구문은 `SubmitButton_Click`처음 두 줄에 약간 차이가 있지만 의미 체계는 동일 합니다. 모든 ASP.NET 서버 컨트롤에 `FindControl` 메서드가 포함 되어 있음을 기억 하세요. 여기에는 모든 ASP.NET 코드 숨김이 클래스에서 파생 되어야 하는 `Page` 클래스가 포함 됩니다. 따라서 `FindControl("controlID")`를 호출 하는 것은 `Page.FindControl("controlID")`호출 하는 것과 같으며,이 경우에는 코드 숨김이 나 사용자 지정 기본 클래스에서 `FindControl` 메서드를 재정의 하지 않은 것으로 가정 합니다.

이 코드를 입력 한 후 브라우저를 통해 `IDIssues.aspx` 페이지를 방문 하 고 나이를 입력 한 후 "제출" 단추를 클릭 합니다. "제출" 단추를 클릭 하면 `NullReferenceException` 발생 합니다 (그림 5 참조).

[NullReferenceException이 발생 ![](control-id-naming-in-content-pages-cs/_static/image8.png)](control-id-naming-in-content-pages-cs/_static/image7.png)

**그림 05**: `NullReferenceException` 발생 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image9.png))

`SubmitButton_Click` 이벤트 처리기에 중단점을 설정 하면 `FindControl`에 대 한 두 호출이 모두 `null` 값을 반환 하는 것을 볼 수 있습니다. `Age` TextBox의 `Text` 속성에 액세스 하려고 하면 `NullReferenceException` 발생 합니다.

문제는 `Control.FindControl` *동일한 명명 컨테이너에*있는 *컨트롤*의 하위 항목만 검색 하는 것입니다. 마스터 페이지는 새 명명 컨테이너를 구성 하기 때문에 `Page.FindControl("controlID")`를 호출 하면 마스터 페이지 개체가 `ctl00`되지 않습니다. `Page` 개체를 `ctl00`마스터 페이지 개체의 부모로 표시 하는 컨트롤 계층 구조를 보려면 그림 4로 다시 참조 하세요. 따라서 `Results` 레이블 및 `Age` TextBox를 찾을 수 없으며 `ResultsLabel` 및 `AgeTextBox`에 `null`값이 할당 됩니다.

이 문제에 대 한 두 가지 해결 방법이 있습니다. 즉, 한 번에 하나의 명명 컨테이너를 적절 한 컨트롤로 드릴 다운할 수 있습니다. 또는 컨테이너의 명명을 permeates 하는 고유한 `FindControl` 메서드를 만들 수 있습니다. 이러한 각 옵션을 살펴보겠습니다.

### <a name="drilling-into-the-appropriate-naming-container"></a>적절 한 명명 컨테이너를 드릴업 합니다.

`FindControl`를 사용 하 여 `Results` 레이블 또는 `Age` 텍스트 상자를 참조 하려면 동일한 명명 컨테이너의 상위 컨트롤에서 `FindControl`를 호출 해야 합니다. 그림 4에 표시 된 것 처럼 `MainContent` ContentPlaceHolder 컨트롤은 동일한 명명 컨테이너에 있는 `Results` 또는 `Age`의 유일한 상위 항목입니다. 즉, 아래 코드 조각에 표시 된 것 처럼 `MainContent` 컨트롤에서 `FindControl` 메서드를 호출 하면 `Results` 또는 `Age` 컨트롤에 대 한 참조가 올바르게 반환 됩니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample8.cs)]

그러나 ContentPlaceHolder가 마스터 페이지에 정의 되어 있기 때문에 위의 구문을 사용 하 여 콘텐츠 페이지의 코드 숨김이 ContentPlaceHolder에서 `MainContent`를 사용할 수 없습니다. 대신 `FindControl`를 사용 하 여 `MainContent`에 대 한 참조를 가져와야 합니다. `SubmitButton_Click` 이벤트 처리기의 코드를 다음과 같이 수정 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample9.cs)]

브라우저를 통해 페이지를 방문 하는 경우 나이를 입력 하 고 "제출" 단추를 클릭 하면 `NullReferenceException` 발생 합니다. `SubmitButton_Click` 이벤트 처리기에 중단점을 설정 하면 `MainContent` 개체의 `FindControl` 메서드를 호출 하려고 할 때이 예외가 발생 하는 것을 볼 수 있습니다. `FindControl` 메서드가 "MainContent" 라는 개체를 찾을 수 없기 때문에 `MainContent` 개체가 `null` 되었습니다. 기본적인 이유는 `Results` 레이블 및 `Age` TextBox 컨트롤과 동일 합니다. `FindControl`는 컨트롤 계층 구조의 맨 위에서 검색을 시작 하 고 명명 컨테이너를 통과 하지 않지만 `MainContent` ContentPlaceHolder는 명명 컨테이너인 마스터 페이지 내에 있습니다.

`FindControl`를 사용 하 여 `MainContent`에 대 한 참조를 가져오려면 먼저 마스터 페이지 컨트롤에 대 한 참조가 필요 합니다. 마스터 페이지에 대 한 참조가 있으면 `FindControl`를 통해 `MainContent` ContentPlaceHolder에 대 한 참조를 가져올 수 있습니다. 여기서는 `FindControl`을 사용 하 여 `Results` 레이블 및 `Age` 텍스트 상자에 대 한 참조를 다시 사용할 수 있습니다. 그러나 마스터 페이지에 대 한 참조는 어떻게 얻을 수 있나요? 렌더링 된 태그에서 `id` 특성을 검사 하 여 마스터 페이지의 `ID` 값이 `ctl00`있음을 분명히 알 수 있습니다. 따라서 `Page.FindControl("ctl00")`를 사용 하 여 마스터 페이지에 대 한 참조를 가져온 다음 해당 개체를 사용 하 여 `MainContent`에 대 한 참조를 가져올 수 있습니다. 다음 코드 조각에서는이 논리를 보여 줍니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample10.cs)]

이 코드는 분명히 작동 하지만 마스터 페이지의 자동 생성 `ID` 항상 `ctl00`되는 것으로 가정 합니다. 자동 생성 된 값에 대해 가정 하는 것은 좋지 않습니다.

다행히 마스터 페이지에 대 한 참조는 `Page` 클래스의 `Master` 속성을 통해 액세스할 수 있습니다. 따라서 `MainContent` ContentPlaceHolder에 액세스 하기 위해 `FindControl("ctl00")`를 사용 하 여 마스터 페이지의 참조를 가져오는 대신 `Page.Master.FindControl("MainContent")`를 사용할 수 있습니다. 다음 코드를 사용 하 여 `SubmitButton_Click` 이벤트 처리기를 업데이트 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample11.cs)]

이번에는 브라우저를 통해 페이지를 방문 하 고 나이를 입력 한 다음 "제출" 단추를 클릭 하면 예상 대로 `Results` 레이블에 메시지가 표시 됩니다.

[사용자의 나이가 레이블에 표시 되는 ![](control-id-naming-in-content-pages-cs/_static/image11.png)](control-id-naming-in-content-pages-cs/_static/image10.png)

**그림 06**: 사용자의 나이가 레이블에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image12.png)).

### <a name="recursively-searching-through-naming-containers"></a>이름 지정 컨테이너를 통해 재귀적으로 검색

이전 코드 예제에서 마스터 페이지의 `MainContent` ContentPlaceHolder 컨트롤을 참조 하 고 `MainContent`에서 `Results` 레이블 및 `Age` TextBox 컨트롤을 참조 하는 이유는 `Control.FindControl` 메서드가 *컨트롤*의 명명 컨테이너 내 에서만 검색 하기 때문입니다. 서로 다른 두 명명 컨테이너의 두 컨트롤에 동일한 `ID` 값이 있을 수 있기 때문에 명명 컨테이너 내에 `FindControl`을 유지 하는 것은 대부분의 시나리오에서 유용 합니다. 해당 템플릿 필드 중 하나에 `ProductName` 이라는 레이블 웹 컨트롤을 정의 하는 GridView의 경우를 고려 합니다. 런타임에 데이터를 GridView에 바인딩하면 각 GridView 행에 대해 `ProductName` 레이블이 생성 됩니다. `FindControl` 모든 명명 컨테이너를 검색 하 고 `Page.FindControl("ProductName")`를 호출한 경우 `FindControl`에서 반환 해야 하는 레이블 인스턴스는 무엇 인가요? 첫 번째 GridView 행의 `ProductName` 레이블이 있나요? 마지막 행에 있는 항목

`Control.FindControl` 검색을 사용 하면 대부분의 경우 *컨트롤*의 명명 컨테이너를 사용 하는 것이 좋습니다. 그러나 모든 명명 컨테이너에서 고유한 `ID`를가지고 있으며 컨트롤 계층 구조에서 각 명명 컨테이너를 참조 하 여 컨트롤에 액세스할 필요가 없도록 하는 것과 같은 다른 경우가 있습니다. 모든 명명 컨테이너를 재귀적으로 검색 하는 `FindControl` variant를 사용 하는 것도 좋습니다. 아쉽게도 이러한 메서드는 .NET Framework에 포함 되지 않습니다.

좋은 소식은 모든 명명 컨테이너를 재귀적으로 검색 하는 자체 `FindControl` 메서드를 만들 수 있다는 것입니다. 실제로 *확장 메서드* 를 사용 하 여 `Control` 클래스에 `FindControlRecursive` 메서드를 표시 하 여 기존 `FindControl` 메서드와 함께 사용할 수 있습니다.

> [!NOTE]
> 확장 메서드는 C# 3.0 및 Visual Basic 9의 새로운 기능으로, .NET Framework 버전 3.5 및 Visual Studio 2008와 함께 제공 되는 언어입니다. 즉, 확장 메서드를 사용 하면 개발자가 특수 구문을 통해 기존 클래스 형식에 대 한 새 메서드를 만들 수 있습니다. 이 유용한 기능에 대 한 자세한 내용은 my 문서를 참조 하세요. [확장 메서드를 사용 하 여 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)을 참조 하세요.

확장 메서드를 만들려면 `PageExtensionMethods.cs`이라는 `App_Code` 폴더에 새 파일을 추가 합니다. `controlID`이라는 `string` 매개 변수를 입력으로 사용 하는 `FindControlRecursive` 라는 확장명 메서드를 추가 합니다. 확장 메서드가 제대로 작동 하려면 클래스 자체와 해당 확장 메서드가 `static`로 표시 되는 것이 중요 합니다. 또한 모든 확장 메서드는 첫 번째 매개 변수로 확장 메서드가 적용 되는 형식의 개체를 수락 해야 하며이 입력 매개 변수 앞에는 `this`키워드가와 야 합니다.

`PageExtensionMethods.cs` 클래스 파일에 다음 코드를 추가 하 여이 클래스와 `FindControlRecursive` 확장 메서드를 정의 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample12.cs)]

이 코드를 사용 하면 `IDIssues.aspx` 페이지의 코드를 사용 하는 클래스를 반환 하 고 현재 `FindControl` 메서드 호출을 주석 처리 합니다. `Page.FindControlRecursive("controlID")`에 대 한 호출로 대체 합니다. 확장 메서드에 대 한 자세한 내용은 IntelliSense 드롭다운 목록 내에 직접 표시 된다는 것입니다. 그림 7에 표시 된 것 처럼 Page와 enter period를 입력 하면 `FindControlRecursive` 메서드가 다른 `Control` 클래스 메서드와 함께 IntelliSense 드롭다운에 포함 됩니다.

[![확장 메서드는 IntelliSense 드롭다운에 포함 되어 있습니다.](control-id-naming-in-content-pages-cs/_static/image14.png)](control-id-naming-in-content-pages-cs/_static/image13.png)

**그림 07**: 확장 메서드가 IntelliSense 드롭다운에 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](control-id-naming-in-content-pages-cs/_static/image15.png)).

`SubmitButton_Click` 이벤트 처리기에 다음 코드를 입력 하 고 페이지를 방문 하 여 나이를 입력 하 고 "제출" 단추를 클릭 하 여 테스트 합니다. 그림 6에 표시 된 것 처럼 결과로 생성 되는 출력은 "사용 기간 이전!"의 메시지입니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample13.cs)]

> [!NOTE]
> 확장 메서드는 3.0 및 Visual Basic C# 9에 처음으로 사용 되므로 Visual Studio 2005를 사용 하는 경우 확장 메서드를 사용할 수 없습니다. 대신 도우미 클래스에서 `FindControlRecursive` 메서드를 구현 해야 합니다. [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx) 에는 [ASP.NET 메이저 Pages 및 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)의 블로그 게시물에 이러한 예가 있습니다.

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>4 단계: 클라이언트 쪽 스크립트에서 올바른`id`특성 값 사용

이 자습서의 소개에서 설명한 것 처럼 웹 컨트롤의 렌더링 된 `id` 특성은 클라이언트 쪽 스크립트에서 특정 HTML 요소를 프로그래밍 방식으로 참조 하는 데 사용 되는 경우가 많습니다. 예를 들어, 다음 JavaScript는 `id` 따라 HTML 요소를 참조 하 고 모달 메시지 상자에 해당 값을 표시 합니다.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample14.cs)]

명명 컨테이너를 포함 하지 않는 ASP.NET 페이지에서 렌더링 된 HTML 요소의 `id` 특성은 웹 컨트롤의 `ID` 속성 값과 동일 합니다. 이로 인해 JavaScript 코드에 `id` 특성 값을 하드 코드 하는 것이 좋습니다. 즉, 클라이언트 쪽 스크립트를 통해 `Age` TextBox 웹 컨트롤에 액세스 하려면 `document.getElementById("Age")`에 대 한 호출을 통해이 작업을 수행 합니다.

이 방법의 문제는 마스터 페이지 또는 기타 명명 컨테이너 컨트롤을 사용할 때 렌더링 된 HTML `id` 웹 컨트롤의 `ID` 속성과 동의어가 없다는 것입니다. 첫 번째는 브라우저를 통해 페이지를 방문 하 고 소스를 확인 하 여 실제 `id` 특성을 확인 하는 것입니다. 렌더링 된 `id` 값을 알고 있으면 `getElementById` 호출에 붙여넣어 클라이언트 쪽 스크립트를 통해 작업 해야 하는 HTML 요소에 액세스할 수 있습니다. 이 방법은 페이지의 컨트롤 계층 구조를 변경 하거나 명명 컨트롤의 `ID` 속성을 변경 하 여 결과 `id` 특성을 변경 하므로 JavaScript 코드가 손상 되기 때문에 이상적이 지 않습니다.

웹 컨트롤의 [`ClientID` 속성](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)을 통해 서버 쪽 코드에서 렌더링 되는 `id` 특성 값에 액세스할 수 있다는 것이 좋습니다. 이 속성을 사용 하 여 클라이언트 쪽 스크립트에서 사용 되는 `id` 특성 값을 확인 해야 합니다. 예를 들어 JavaScript 함수를 페이지에 추가 하려면 호출 되는 경우 모달 메시지 상자에 `Age` 텍스트 상자 값을 표시 하 고 `Page_Load` 이벤트 처리기에 다음 코드를 추가 합니다.

[!code-javascript[Main](control-id-naming-in-content-pages-cs/samples/sample15.js)]

위의 코드는 `getElementById`에 대 한 JavaScript 호출에 `Age` TextBox의 ClientID 속성 값을 삽입 합니다. 브라우저를 통해이 페이지를 방문 하 고 HTML 소스를 보면 다음 JavaScript 코드를 찾을 수 있습니다.

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample16.html)]

`getElementById`에 대 한 호출 내에 올바른 `id` 특성 값 `ctl00_MainContent_Age`표시 되는 방법을 확인 합니다. 이 값은 런타임에 계산 되기 때문에 페이지 컨트롤 계층 구조에 대 한 이후 변경 내용에 관계 없이 작동 합니다.

> [!NOTE]
> 이 JavaScript 예제에서는 서버 컨트롤에서 렌더링 한 HTML 요소를 올바르게 참조 하는 JavaScript 함수를 추가 하는 방법만 보여 줍니다. 이 함수를 사용 하려면 문서가 로드 될 때 또는 특정 사용자 작업이 transpires 때 함수를 호출 하기 위해 추가 JavaScript를 작성 해야 합니다. 이러한 항목 및 관련 항목에 대 한 자세한 내용은 [클라이언트 쪽 스크립트 작업](https://msdn.microsoft.com/library/aa479302.aspx)을 참조 하세요.

## <a name="summary"></a>요약

특정 ASP.NET 서버 컨트롤은 `FindControl` 메서드에서 canvassed 컨트롤의 범위 뿐만 아니라 해당 하위 컨트롤의 렌더링 된 `id` 특성 값에 영향을 주는 명명 컨테이너 역할을 합니다. 마스터 페이지와 관련 하 여 마스터 페이지와 해당 ContentPlaceHolder 컨트롤은 모두 명명 컨테이너입니다. 따라서 `FindControl`를 사용 하 여 콘텐츠 페이지 내에서 프로그래밍 방식으로 컨트롤을 참조 하려면 약간 더 많은 작업을 수행 해야 합니다. 이 자습서에서는 ContentPlaceHolder 컨트롤로 드릴 하 고 해당 `FindControl` 메서드를 호출 하는 두 가지 방법을 살펴보았습니다. 그리고 모든 명명 컨테이너를 재귀적으로 검색 하는 자체 `FindControl` 구현을 롤백합니다.

서버 쪽 문제를 명명 하는 컨테이너는 웹 컨트롤을 참조 하는 것과 관련해 서 소개 합니다. 또한 클라이언트 쪽 문제도 있습니다. 명명 컨테이너가 없을 경우 웹 컨트롤의 `ID` 속성 값과 렌더링 된 `id` 특성 값은 동일 합니다. 그러나 명명 컨테이너가 추가 되어 렌더링 된 `id` 특성에는 웹 컨트롤의 `ID` 값과 해당 컨트롤 계층의 상위 구조에 있는 명명 컨테이너가 모두 포함 됩니다. 이러한 명명 문제는 웹 컨트롤의 `ClientID` 속성을 사용 하 여 클라이언트 쪽 스크립트에서 렌더링 된 `id` 특성 값을 확인 하는 동안 문제가 되지 않습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 마스터 페이지 및 `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [Dynamic Data 항목 사용자 인터페이스 만들기](https://msdn.microsoft.com/library/aa479330.aspx)
- [확장 메서드를 사용 하 여 기본 형식 기능 확장](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [방법: ASP.NET 마스터 페이지 콘텐츠 참조](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [마스터 페이지: 팁, 요령 및 트랩](http://www.odetocode.com/articles/450.aspx)
- [클라이언트 쪽 스크립트 작업](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 Zack Jones와 Suchi 바의 Jee 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](urls-in-master-pages-cs.md)
> [다음](interacting-with-the-master-page-from-the-content-page-cs.md)
