---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
title: 마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정 (C#) | Microsoft Docs
author: rick-anderson
description: 콘텐츠 페이지에서 마스터 페이지의 다양 한 &lt;헤드&gt; 요소를 정의 하는 다양 한 기술을 살펴봅니다.
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 0aa1c84f-c9e2-4699-b009-0e28643ecbc6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs
msc.type: authoredcontent
ms.openlocfilehash: a4ec96a5b90f664655d554c064f9d50e76ad2d58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474533"
---
# <a name="specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-c"></a>마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_03_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_03_CS.pdf)

> 콘텐츠 페이지에서 마스터 페이지의 다양 한 &lt;헤드&gt; 요소를 정의 하는 다양 한 기술을 살펴봅니다.

## <a name="introduction"></a>소개

Visual Studio 2008에서 만든 새 마스터 페이지에는 기본적으로 두 개의 ContentPlaceHolder 컨트롤이 있습니다. 하나는 명명 된 head이 고 `<head>` 요소에 있습니다. 및는 웹 폼 내에 배치 된 `ContentPlaceHolder1`합니다. `ContentPlaceHolder1` 목적은 웹 양식에서 페이지 단위로 사용자 지정할 수 있는 영역을 정의 하는 것입니다. `head` ContentPlaceHolder를 사용 하면 페이지에서 `<head>` 섹션에 사용자 지정 콘텐츠를 추가할 수 있습니다. 물론 이러한 두 ContentPlaceHolders 표시자를 수정 하거나 제거 하 고 추가 ContentPlaceHolder를 마스터 페이지에 추가할 수 있습니다. 현재 마스터 페이지 `Site.master`에는 ContentPlaceHolder 컨트롤이 4 개 있습니다.

HTML `<head>` 요소는 문서 자체의 일부가 아닌 웹 페이지 문서에 대 한 정보에 대 한 리포지토리로 사용 됩니다. 여기에는 웹 페이지의 제목, 검색 엔진 또는 내부 크롤러가 사용 하는 메타 정보, RSS 피드, JavaScript, CSS 파일 등의 외부 리소스에 대 한 링크가 포함 됩니다. 이 정보 중 일부는 웹 사이트의 모든 페이지와 관련이 있을 수 있습니다. 예를 들어 모든 ASP.NET 페이지에 대해 동일한 CSS 규칙 및 JavaScript 파일을 전역으로 가져올 수 있습니다. 그러나 `<head>` 요소에는 페이지 별로 관련 된 부분이 있습니다. 페이지 제목은 소수 예제입니다.

이 자습서에서는 마스터 페이지와 해당 콘텐츠 페이지에서 전역 및 페이지 관련 `<head>` 섹션 태그를 정의 하는 방법을 살펴봅니다.

## <a name="examining-the-master-pagesheadsection"></a>마스터 페이지의`<head>`섹션 검사

Visual Studio 2008에서 만든 기본 마스터 페이지 파일은 해당 `<head>` 섹션에 다음 태그를 포함 합니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample1.aspx)]

`<head>` 요소는 정적 HTML이 아닌 서버 컨트롤 임을 나타내는 `runat="server"` 특성을 포함 합니다. 모든 ASP.NET 페이지는 `System.Web.UI` 네임 스페이스에 있는 [`Page` 클래스](https://msdn.microsoft.com/library/system.web.ui.page.aspx)에서 파생 됩니다. 이 클래스에는 페이지의 `<head>` 영역에 대 한 액세스를 제공 하는 `Header` 속성이 포함 되어 있습니다. [`Header` 속성](https://msdn.microsoft.com/library/system.web.ui.page.header.aspx) 을 사용 하 여 ASP.NET 페이지의 제목을 설정 하거나 렌더링 된 `<head>` 섹션에 추가 태그를 추가할 수 있습니다. 그런 다음 페이지의 `Page_Load` 이벤트 처리기에서 약간의 코드를 작성 하 여 콘텐츠 페이지의 `<head>` 요소를 사용자 지정할 수 있습니다. 1 단계에서 프로그래밍 방식으로 페이지 제목을 설정 하는 방법을 살펴봅니다.

위의 `<head>` 요소에 표시 된 태그에는 head 라는 ContentPlaceHolder 컨트롤이 포함 되어 있습니다. 콘텐츠 페이지에서 프로그래밍 방식으로 `<head>` 요소에 사용자 지정 콘텐츠를 추가할 수 있으므로이 ContentPlaceHolder 컨트롤은 필요 하지 않습니다. 그러나 정적 태그를 프로그래밍 방식이 아닌 해당 콘텐츠 컨트롤에 선언적으로 추가할 수 있으므로 콘텐츠 페이지가 `<head>` 요소에 정적 태그를 추가 해야 하는 경우에 유용 합니다.

`<title>` 요소와 헤드 ContentPlaceHolder 외에도 마스터 페이지의 `<head>` 요소는 모든 페이지에 공통적인 `<head>`수준 태그를 포함 해야 합니다. 이 웹 사이트에서 모든 페이지는 `Styles.css` 파일에 정의 된 CSS 규칙을 사용 합니다. 따라서 [*마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기*](creating-a-site-wide-layout-using-master-pages-cs.md) 자습서에서 `<head>` 요소를 업데이트 하 여 해당 `<link>` 요소를 포함 합니다. `Site.master` 마스터 페이지의 현재 `<head>` 태그는 다음과 같습니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample2.aspx)]

## <a name="step-1-setting-a-content-pages-title"></a>1 단계: 콘텐츠 페이지의 제목 설정

웹 페이지의 제목은 `<title>` 요소를 통해 지정 됩니다. 각 페이지의 제목을 적절 한 값으로 설정 하는 것이 중요 합니다. 페이지를 방문 하면 브라우저의 제목 표시줄에 해당 제목이 표시 됩니다. 또한 페이지의 책갈피를 만들면 브라우저에서 페이지의 제목을 책갈피의 제안 된 이름으로 사용 합니다. 또한 많은 검색 엔진은 검색 결과를 표시할 때 페이지의 제목을 표시 합니다.

> [!NOTE]
> 기본적으로 Visual Studio는 마스터 페이지의 `<title>` 요소를 "제목이 없는 페이지"로 설정 합니다. 마찬가지로 새 ASP.NET 페이지에는 `<title>` "제목 없음 페이지"로 설정 되어 있습니다. 페이지의 제목을 적절 한 값으로 설정 하는 것을 잊은 경우에는 인터넷에 "제목 없음 페이지" 라는 제목의 많은 페이지가 있습니다. Google에서이 제목을 사용 하 여 웹 페이지를 검색 하면 약 246만 결과가 반환 됩니다. Microsoft 에서도 "제목 없음 페이지" 라는 제목의 웹 페이지를 게시할 수 있습니다. 이 문서를 작성할 당시 Google 검색은 Microsoft.com 도메인에 해당 웹 페이지 236를 보고 했습니다.

ASP.NET 페이지는 다음 방법 중 하나로 제목을 지정할 수 있습니다.

- `<title>` 요소 내에 값을 직접 배치 하 여
- `<%@ Page %>` 지시문에 `Title` 특성 사용
- `Page.Title="title"` 또는 `Page.Header.Title="title"`와 같은 코드를 사용 하 여 페이지의 `Title` 속성을 프로그래밍 방식으로 설정 합니다.

콘텐츠 페이지는 마스터 페이지에 정의 된 대로 `<title>` 요소를 포함 하지 않습니다. 따라서 콘텐츠 페이지의 제목을 설정 하려면 `<%@ Page %>` 지시문의 `Title` 특성을 사용 하거나 프로그래밍 방식으로 설정할 수 있습니다.

### <a name="setting-the-pages-title-declaratively"></a>페이지의 제목을 선언적으로 설정

콘텐츠 페이지의 제목은 [`<%@ Page %>` 지시문](https://msdn.microsoft.com/library/ydy4x04a.aspx)의 `Title` 특성을 통해 선언적으로 설정할 수 있습니다. 이 속성은 `<%@ Page %>` 지시문을 직접 수정 하거나 속성 창를 통해 설정할 수 있습니다. 두 가지 방법을 살펴보겠습니다.

소스 뷰에서 페이지의 선언 태그 맨 위에 있는 `<%@ Page %>` 지시문을 찾습니다. `Default.aspx`에 대 한 `<%@ Page %>` 지시어는 다음과 같습니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample3.aspx)]

`<%@ Page %>` 지시어는 페이지를 구문 분석 하 고 컴파일할 때 ASP.NET 엔진에서 사용 하는 페이지 관련 특성을 지정 합니다. 여기에는 마스터 페이지 파일, 해당 코드 파일의 위치 및 기타 정보 중에 해당 제목이 포함 됩니다.

기본적으로 새 콘텐츠 페이지를 만들 때 Visual Studio는 `Title` 특성을 제목 없는 페이지로 설정 합니다. `Default.aspx`의 `Title` 특성을 "제목 없음 페이지"에서 "마스터 페이지 자습서"로 변경한 다음 브라우저를 통해 페이지를 봅니다. 그림 1에는 새 페이지 제목을 반영 하는 브라우저의 제목 표시줄이 표시 됩니다.

![이제 브라우저의 제목 표시줄에 &quot;제목 없는 페이지가 아닌 &quot;마스터 페이지 자습서&quot; 표시 됩니다&quot;](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image1.png)

**그림 01**: 브라우저의 제목 표시줄에 "제목 없음 페이지" 대신 "마스터 페이지 자습서"가 표시 됩니다.

페이지의 제목을 속성 창 설정할 수도 있습니다. 속성 창의 드롭다운 목록에서 문서를 선택 하 여 `Title` 속성을 포함 하는 페이지 수준 속성을 로드 합니다. 그림 2는 `Title` "마스터 페이지 자습서"로 설정 된 후의 속성 창 보여 줍니다.

![속성 창에서 제목을 구성할 수도 있습니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image2.png)

**그림 02**: 속성 창에서 제목을 구성할 수 있습니다.

### <a name="setting-the-pages-title-programmatically"></a>프로그래밍 방식으로 페이지의 제목 설정

ASP.NET 엔진에서 페이지가 렌더링 되 면 마스터 페이지의 `<head runat="server">` 태그가 [`HtmlHead` 클래스](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.aspx) 인스턴스로 변환 됩니다. `HtmlHead` 클래스에는 렌더링 된 `<title>` 요소에 반영 되는 값을 갖는 [`Title` 속성이](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlhead.title.aspx) 있습니다. 이 속성은 `Page.Header.Title`를 통해 ASP.NET 페이지의 코드 숨김이 클래스에서 액세스할 수 있습니다. 이 동일한 속성은 `Page.Title`를 통해 액세스할 수도 있습니다.

페이지의 제목을 프로그래밍 방식으로 설정 하려면 `About.aspx` 페이지의 코드 숨김으로 클래스를 탐색 하 고 페이지 `Load` 이벤트에 대 한 이벤트 처리기를 만듭니다. 그런 다음 페이지의 제목을 "Master Page 자습서:: About:: *date*"로 설정 합니다. 여기서 *date* 는 현재 날짜입니다. 이 코드를 추가 하면 `Page_Load` 이벤트 처리기가 다음과 같이 표시 됩니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample4.cs)]

그림 3에는 `About.aspx` 페이지를 방문할 때 브라우저의 제목 표시줄이 표시 됩니다.

![페이지의 제목은 프로그래밍 방식으로 설정 되 고 현재 날짜를 포함 합니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image3.png)

**그림 03**: 프로그래밍 방식으로 페이지의 제목을 설정 하 고 현재 날짜를 포함 합니다.

## <a name="step-2-automatically-assigning-a-page-title"></a>2 단계: 페이지 제목 자동 할당

1 단계에서 살펴본 것 처럼 페이지의 제목은 선언적으로 또는 프로그래밍 방식으로 설정할 수 있습니다. 그러나 제목을 명확 하 게 설명 하는 내용으로 변경 하는 것을 잊은 경우에는 페이지에 "제목 없음" 페이지가 표시 됩니다. 이상적으로는 해당 값을 명시적으로 지정 하지 않는 경우 페이지의 제목이 자동으로 설정 됩니다. 예를 들어 런타임에 페이지 제목이 "제목이 없는 페이지" 인 경우 제목이 자동으로 ASP.NET 페이지의 파일 이름과 동일 하 게 업데이트 되도록 할 수 있습니다. 좋은 소식은 약간의 사전 작업으로 제목을 자동으로 할당할 수 있다는 것입니다.

모든 ASP.NET 웹 페이지는 `System.Web.UI` 네임 스페이스의 `Page` 클래스에서 파생 됩니다. `Page` 클래스는 ASP.NET 페이지에 필요한 최소한의 기능을 정의 하 고 `IsPostBack`, `IsValid`, `Request`, `Response`등의 필수 속성을 다른 여러 항목으로 노출 합니다. 웹 응용 프로그램의 모든 페이지에는 추가 기능이 나 기능이 필요 합니다. 이를 제공 하는 일반적인 방법은 사용자 지정 기본 페이지 클래스를 만드는 것입니다. 사용자 지정 기본 페이지 클래스는 `Page` 클래스에서 파생 되 고 추가 기능을 포함 하는 사용자가 만드는 클래스입니다. 이 기본 클래스를 만든 후에는 `Page` 클래스가 아니라 ASP.NET 페이지가 해당 페이지에서 파생 되도록 하 여 ASP.NET 페이지에 확장 된 기능을 제공할 수 있습니다.

이 단계에서는 제목이 명시적으로 설정 되지 않은 경우 페이지의 제목을 자동으로 ASP.NET 페이지의 파일 이름으로 설정 하는 기본 페이지를 만듭니다. 3 단계에서는 사이트 맵을 기반으로 페이지의 제목을 설정 하는 방법을 살펴봅니다.

> [!NOTE]
> 사용자 지정 기본 페이지 클래스 만들기 및 사용에 대 한 철저 한 검사는이 자습서 시리즈의 범위를 벗어나는 것입니다. 자세한 내용은 [ASP.NET Pages의 코드 숨김이 클래스에 대 한 사용자 지정 기본 클래스 사용](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)을 참조 하세요.

### <a name="creating-the-base-page-class"></a>기본 페이지 클래스 만들기

첫 번째 작업은 기본 페이지 클래스를 만드는 것입니다 .이 클래스는 `Page` 클래스를 확장 하는 클래스입니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 ASP.NET 폴더 추가를 선택한 다음 `App_Code`을 선택 하 여 프로젝트에 `App_Code` 폴더를 추가 합니다. 그런 다음 `App_Code` 폴더를 마우스 오른쪽 단추로 클릭 하 고 `BasePage.cs`라는 새 클래스를 추가 합니다. 그림 4는 `App_Code` 폴더 및 `BasePage.cs` 클래스가 추가 된 후의 솔루션 탐색기을 보여 줍니다.

![App_Code 폴더와 BasePage 라는 클래스를 추가 합니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image4.png)

**그림 04**: `App_Code` 폴더와 `BasePage` 라는 클래스를 추가 합니다.

> [!NOTE]
> Visual Studio는 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트의 두 가지 모드의 프로젝트 관리를 지원 합니다. `App_Code` 폴더는 웹 사이트 프로젝트 모델에서 사용할 수 있도록 디자인 되었습니다. 웹 응용 프로그램 프로젝트 모델을 사용 하는 경우 `Classes`와 같이 `App_Code`아닌 다른 폴더에 `BasePage.cs` 클래스를 저장 합니다. 이 항목에 대 한 자세한 내용은 웹 [사이트 프로젝트를 웹 응용 프로그램 프로젝트로 마이그레이션](http://webproject.scottgu.com/CSharp/Migration2/Migration2.aspx)을 참조 하세요.

사용자 지정 기본 페이지는 ASP.NET 페이지의 코드 숨김이 아닌 클래스의 기본 클래스 역할을 하기 때문에 `Page` 클래스를 확장 해야 합니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample5.cs)]

ASP.NET 페이지가 요청 될 때마다 요청 된 페이지의 culminating가 HTML로 렌더링 되는 일련의 단계를 진행 합니다. `Page` 클래스의 `OnEvent` 메서드를 재정의 하 여 단계를 선택할 수 있습니다. 기본 페이지의 경우 `LoadComplete` 단계에서 명시적으로 지정 하지 않은 경우 (`Load` 단계 후에 발생할 수 있음) 자동으로 제목을 설정 합니다.

이 작업을 수행 하려면 `OnLoadComplete` 메서드를 재정의 하 고 다음 코드를 입력 합니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample6.cs)]

`OnLoadComplete` 메서드는 `Title` 속성을 아직 명시적으로 설정 하지 않은 경우를 확인 하 여 시작 합니다. `Title` 속성이 `null`이거나 빈 문자열 이거나 "제목이 없는 페이지" 값을 가지는 경우 요청 된 ASP.NET 페이지의 파일 이름에 할당 됩니다. 요청 된 ASP.NET 페이지의 실제 경로 `C:\MySites\Tutorial03\Login.aspx`(예: `Request.PhysicalPath` 속성을 통해 액세스할 수 있습니다. `Path.GetFileNameWithoutExtension` 메서드는 파일 이름 부분만 가져오는 데 사용 되며,이 파일 이름은 `Page.Title` 속성에 할당 됩니다.

> [!NOTE]
> 제목 형식을 개선 하기 위해이 논리를 향상 시킬 수 있도록 초대 합니다. 예를 들어 페이지의 파일 이름이 `Company-Products.aspx`되는 경우 위의 코드는 "회사 제품" 제목을 생성 하지만, 대시는 "회사 제품"과 같이 공백으로 대체 되는 것이 좋습니다. 또한 대/소문자가 변경 될 때마다 공백을 추가 하는 것이 좋습니다. 즉, 파일 이름 `OurBusinessHours.aspx`를 "업무 시간"의 제목으로 변환 하는 코드를 추가 하는 것이 좋습니다.

### <a name="having-the-content-pages-inherit-the-base-page-class"></a>콘텐츠 페이지가 기본 페이지 클래스를 상속 하는 경우

이제 `Page` 클래스 대신 사용자 지정 기본 페이지 (`BasePage`)에서 파생 되도록 사이트의 ASP.NET 페이지를 업데이트 해야 합니다. 이 작업을 수행 하려면 각 코드를 가져온 클래스로 이동 하 여에서 클래스 선언을 변경 합니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample7.cs)]

아래와 같이 변경합니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample8.cs)]

그런 다음 브라우저를 통해 사이트를 방문 합니다. `Default.aspx` 또는 `About.aspx`와 같이 제목이 명시적으로 설정 된 페이지를 방문 하는 경우에는 명시적으로 지정 된 제목이 사용 됩니다. 그러나 제목이 기본값 ("제목 없음" 페이지)에서 변경 되지 않은 페이지를 방문 하는 경우 기본 페이지 클래스는 제목을 페이지의 파일 이름으로 설정 합니다.

그림 5에는 브라우저를 통해 볼 때 `MultipleContentPlaceHolders.aspx` 페이지가 표시 됩니다. 제목은 페이지의 파일 이름 (확장명 보다 낮음), "MultipleContentPlaceHolders"입니다.

[![제목이 명시적으로 지정 되지 않은 경우 페이지의 파일 이름이 자동으로 사용 됩니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image6.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image5.png)

**그림 05**: 제목을 명시적으로 지정 하지 않으면 페이지의 파일 이름이 자동으로 사용 됩니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image7.png)).

## <a name="step-3-basing-the-page-title-on-the-site-map"></a>3 단계: 사이트 맵의 페이지 제목 기반

ASP.NET는 페이지 개발자가 사이트 맵에 대 한 정보 (예: SiteMapPath)를 표시 하기 위해 웹 컨트롤과 함께 외부 리소스 (예: XML 파일 또는 데이터베이스 테이블)에서 계층적 사이트 맵을 정의할 수 있게 해 주는 강력한 사이트 맵 프레임 워크를 제공 합니다. 메뉴 및 TreeView 컨트롤).

사이트 맵 구조는 ASP.NET 페이지의 코드 숨겨진 클래스에서 프로그래밍 방식으로 액세스할 수도 있습니다. 이러한 방식으로 페이지의 제목을 사이트 맵에서 해당 노드의 제목으로 자동으로 설정할 수 있습니다. 2 단계에서 만든 `BasePage` 클래스를 개선 하 여이 기능을 제공 하도록 하겠습니다. 하지만 먼저 사이트에 대 한 사이트 맵을 만들어야 합니다.

> [!NOTE]
> 이 자습서에서는 독자가 이미 ASP에 대해 잘 알고 있다고 가정 합니다. 네트워크의 사이트 맵 기능. 사이트 맵 사용에 대 한 자세한 내용은 내 다중 파트 문서 시리즈, ASP 검토를 참조 하세요 [. 네트워크의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx).

### <a name="creating-the-site-map"></a>사이트 맵 만들기

사이트 맵 시스템은 [공급자 모델](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)위에 구축 됩니다 .이 모델은 메모리와 영구 저장소 간에 사이트 맵 정보를 serialize 하는 논리에서 사이트 맵 API를 분리 합니다. .NET Framework는 기본 사이트 맵 공급자 인 [`XmlSiteMapProvider` 클래스](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)와 함께 제공 됩니다. 이름에서 알 `XmlSiteMapProvider` XML 파일을 사이트 맵 저장소로 사용 합니다. 이 공급자를 사용 하 여 사이트 맵을 정의 해 보겠습니다.

먼저 `Web.sitemap`이라는 웹 사이트의 루트 폴더에 사이트 맵 파일을 만듭니다. 이를 수행 하려면 솔루션 탐색기에서 웹 사이트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 사이트 맵 템플릿을 선택 합니다. 파일 이름이 `Web.sitemap` 인지 확인 하 고 추가를 클릭 합니다.

[웹 사이트의 루트 폴더에 web.sitemap 이라는 파일을 추가 ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image9.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image8.png)

**그림 06**: 웹 사이트의 루트 폴더에 `Web.sitemap` 이라는 파일 추가 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image10.png))

`Web.sitemap` 파일에 다음 XML을 추가 합니다.

[!code-xml[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample9.xml)]

이 XML은 그림 7에 표시 된 계층적 사이트 맵 구조를 정의 합니다.

![사이트 맵은 현재 3 개의 사이트 맵 노드로 구성 되어 있습니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image11.png)

**그림 07**: 사이트 맵은 현재 3 개의 사이트 맵 노드로 구성 되어 있습니다.

새 예제를 추가 하는 이후 자습서에서 사이트 맵 구조를 업데이트 합니다.

### <a name="updating-the-master-page-to-include-navigation-web-controls"></a>마스터 페이지를 업데이트 하 여 탐색 웹 컨트롤 포함

이제 사이트 맵을 정의 했으므로 탐색 웹 컨트롤을 포함 하도록 마스터 페이지를 업데이트 해 보겠습니다. 특히 사이트 맵에 정의 된 각 노드에 대 한 목록 항목을 사용 하 여 순서가 지정 되지 않은 목록을 렌더링 하는 단원 섹션의 왼쪽 열에 ListView 컨트롤을 추가 해 보겠습니다.

> [!NOTE]
> ListView 컨트롤은 ASP.NET 버전 3.5의 새로운 버전입니다. 이전 버전의 ASP.NET를 사용 하는 경우에는 Repeater 컨트롤을 대신 사용 합니다. ListView 컨트롤에 대 한 자세한 내용은 [ASP.NET 3.5의 listview 및 DataPager 컨트롤 사용](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)을 참조 하세요.

단원을 단원에서 순서가 지정 되지 않은 기존 목록 태그를 제거 하 여 시작 합니다. 그런 다음 도구 상자에서 ListView 컨트롤을 끌어 단원 제목 아래에 놓습니다. ListView는 다른 뷰 컨트롤인 GridView, DetailsView 및 FormView와 함께 도구 상자의 데이터 섹션에 있습니다. ListView의 ID 속성을 `LessonsList`로 설정 합니다.

데이터 소스 구성 마법사에서 ListView를 `LessonsDataSource`라는 새 SiteMapDataSource 컨트롤에 바인딩하려를 선택 합니다. SiteMapDataSource 컨트롤은 사이트 맵 시스템에서 계층 구조를 반환 합니다.

[SiteMapDataSource 컨트롤을 LessonsList ListView 컨트롤에 바인딩 ![](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image13.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image12.png)

**그림 08**: `LessonsList` ListView 컨트롤에 SiteMapDataSource 컨트롤 바인딩 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image14.png))

SiteMapDataSource 컨트롤을 만든 후에는 ListView의 템플릿을 정의 하 여 SiteMapDataSource 컨트롤에서 반환 하는 각 노드에 대 한 목록 항목을 포함 하는 순서가 지정 되지 않은 목록을 렌더링 해야 합니다. 다음 템플릿 태그를 사용 하 여이 작업을 수행할 수 있습니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample10.aspx)]

`LayoutTemplate`는 순서가 지정 되지 않은 목록 (`<ul>...</ul>`)에 대 한 태그를 생성 하는 반면 `ItemTemplate`는 SiteMapDataSource에서 반환 된 각 항목을 특정 단원에 대 한 링크를 포함 하는 목록 항목 (`<li>`)으로 렌더링 합니다.

ListView의 템플릿을 구성한 후에는 웹 사이트를 방문 하세요. 그림 9에 나와 있는 것 처럼 단원 섹션에는 홈의 단일 글머리 기호 항목이 포함 되어 있습니다. 여러 ContentPlaceHolder 컨트롤에 대 한 정보 및 사용 단원은 어디에 있나요? SiteMapDataSource는 계층적 데이터 집합을 반환 하도록 설계 되었지만 ListView 컨트롤은 계층의 단일 수준만 표시할 수 있습니다. 따라서 SiteMapDataSource에서 반환한 사이트 맵 노드의 첫 번째 수준만 표시 됩니다.

[단원을 ![단일 목록 항목이 포함 되어 있습니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image16.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image15.png)

**그림 09**: 단원 섹션에는 단일 목록 항목 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image17.png))이 포함 되어 있습니다.

여러 수준을 표시 하려면 `ItemTemplate`내에서 여러 Listview를 중첩할 수 있습니다. 이 기법은 [데이터 자습서 시리즈 작업](../../data-access/index.md)의 [ *마스터 페이지 및 사이트 탐색* 자습서](../../data-access/introduction/master-pages-and-site-navigation-cs.md) 에서 검토 되었습니다. 그러나이 자습서 시리즈의 경우 사이트 맵에는 홈 (최상위 수준)의 두 수준만 포함 됩니다. 그리고 각 단원을 홈의 자식으로 만듭니다. 중첩 된 ListView를 만드는 대신 SiteMapDataSource 속성을 `false`로 [`ShowStartingNode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) 설정 하 여 시작 노드를 반환 하지 않도록에 지시할 수 있습니다. 결과적으로 SiteMapDataSource는 사이트 맵 노드의 두 번째 계층을 반환 하는 것으로 시작 됩니다.

이 변경 내용으로 ListView는 About and Using Multiple ContentPlaceHolder Controls 단원에 대 한 글머리 기호 항목을 표시 하지만 홈에 대 한 글머리 기호 항목은 생략 합니다. 이를 해결 하기 위해 `LayoutTemplate`에서 홈에 대 한 글머리 기호 항목을 명시적으로 추가할 수 있습니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample11.aspx)]

SiteMapDataSource를 구성 하 여 시작 노드를 생략 하 고 홈 글머리 기호 항목을 명시적으로 추가 하 여 단원 섹션에서 이제 원하는 출력을 표시 합니다.

[단원을 ![홈 및 각 자식 노드에 대 한 글머리 기호 항목이 포함 되어 있습니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image19.png)](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image18.png)

**그림 10**: 단원 섹션에는 홈 및 각 자식 노드에 대 한 글머리 기호 항목이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image20.png)).

### <a name="setting-the-title-based-on-the-site-map"></a>사이트 맵 기반 제목 설정

사이트 맵이 준비 되 면 사이트 맵에 지정 된 제목을 사용 하도록 `BasePage` 클래스를 업데이트할 수 있습니다. 2 단계에서와 같이 페이지의 제목이 페이지 개발자에 의해 명시적으로 설정 되지 않은 경우에만 사이트 맵 노드의 제목을 사용 합니다. 요청 하는 페이지에 명시적으로 설정 된 페이지 제목이 없고 사이트 맵에서 찾을 수 없는 경우 2 단계에서 했던 것 처럼 요청 된 페이지의 파일 이름 (확장 보다 낮음)을 사용 하도록 대체 합니다. 그림 11에서는 이러한 결정 프로세스를 보여 줍니다.

![명시적으로 설정 된 페이지 제목이 없으면 해당 하는 사이트 맵 노드의 제목이 사용 됩니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image21.png)

**그림 11**: 명시적으로 설정 된 페이지 제목이 없으면 해당 하는 사이트 맵 노드의 제목이 사용 됩니다.

`BasePage` 클래스의 `OnLoadComplete` 메서드를 업데이트 하 여 다음 코드를 포함 합니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample12.cs)]

이전 처럼 `OnLoadComplete` 메서드는 페이지의 제목이 명시적으로 설정 되었는지 여부를 확인 하 여 시작 합니다. `Page.Title` `null`이거나, 빈 문자열 이거나, "제목이 없는 페이지" 값이 할당 된 경우 코드에서 자동으로 `Page.Title`에 값을 할당 합니다.

사용할 제목을 결정 하려면 [`SiteMap` 클래스](https://msdn.microsoft.com/library/system.web.sitemap.aspx)의 [`CurrentNode` 속성](https://msdn.microsoft.com/library/system.web.sitemap.currentnode.aspx)을 참조 하 여 코드를 시작 합니다. `CurrentNode` 현재 요청 된 페이지에 해당 하는 사이트 맵의 [`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) 인스턴스를 반환 합니다. 현재 요청 된 페이지가 사이트 맵 내에 있는 것으로 가정 하면 `SiteMapNode`의 `Title` 속성이 페이지의 제목에 할당 됩니다. 현재 요청 된 페이지가 사이트 맵에 없으면 `CurrentNode` `null` 반환 되 고 요청 된 페이지의 파일 이름이 제목으로 사용 됩니다 (2 단계에서 수행 됨).

그림 12는 브라우저를 통해 볼 때 `MultipleContentPlaceHolders.aspx` 페이지를 보여 줍니다. 이 페이지의 제목을 명시적으로 설정 하지 않았으므로 해당 하는 사이트 맵 노드의 제목이 대신 사용 됩니다.

![사이트 맵에서 MultipleContentPlaceHolders 페이지의 제목을 가져옵니다.](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/_static/image22.png)

**그림 12**: 사이트 맵에서 `MultipleContentPlaceHolders.aspx` 페이지의 제목 가져오기

## <a name="step-4-adding-other-page-specific-markup-to-theheadsection"></a>4 단계:`<head>`섹션에 다른 페이지 관련 태그 추가

1, 2, 3 단계에서는 페이지 별로 `<title>` 요소를 사용자 지정 하는 방법을 살펴보았습니다. `<title>`외에도 `<head>` 섹션에는 `<meta>` 요소와 `<link>` 요소가 포함 될 수 있습니다. 이 자습서의 앞부분에서 설명한 것 처럼 `Site.master`의 `<head>` 섹션에는 `Styles.css``<link>` 요소가 포함 됩니다. 이 `<link>` 요소는 마스터 페이지 내에서 정의 되므로 모든 콘텐츠 페이지의 `<head>` 섹션에 포함 됩니다. 그러나 페이지 별로 `<meta>` 및 `<link>` 요소를 추가 하는 방법은 무엇입니까?

`<head>` 섹션에 페이지 관련 콘텐츠를 추가 하는 가장 쉬운 방법은 마스터 페이지에서 ContentPlaceHolder 컨트롤을 만드는 것입니다. 이러한 ContentPlaceHolder (명명 된 `head`)가 이미 있습니다. 따라서 사용자 지정 `<head>` 태그를 추가 하려면 페이지에 해당 하는 콘텐츠 컨트롤을 만들고 태그를 여기에 추가 합니다.

페이지에 사용자 지정 `<head>` 태그를 추가 하는 방법을 보여 주기 위해 현재 콘텐츠 페이지 집합에 `<meta>` description 요소를 포함 하겠습니다. `<meta>` description 요소는 웹 페이지에 대 한 간략 한 설명을 제공 합니다. 대부분의 검색 엔진은 검색 결과를 표시할 때이 정보를 특정 형식으로 통합 합니다.

`<meta>` description 요소의 형태는 다음과 같습니다.

[!code-html[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample13.html)]

콘텐츠 페이지에이 태그를 추가 하려면 마스터 페이지의 head ContentPlaceHolder에 매핑되는 콘텐츠 컨트롤에 위의 텍스트를 추가 합니다. 예를 들어 `Default.aspx`에 대 한 `<meta>` description 요소를 정의 하려면 다음 태그를 추가 합니다.

[!code-aspx[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample14.aspx)]

Head ContentPlaceHolder는 HTML 페이지의 본문 내에 있지 않기 때문에 콘텐츠 컨트롤에 추가 된 태그는 디자인 뷰 표시 되지 않습니다. `<meta>` 설명 요소를 보려면 브라우저를 통해 `Default.aspx`을 방문 하세요. 페이지가 로드 된 후 소스를 확인 하 고 `<head>` 섹션에 콘텐츠 컨트롤에 지정 된 태그가 포함 되어 있는지 확인 합니다.

잠시 `About.aspx`, `MultipleContentPlaceHolders.aspx`및 `Login.aspx`에 `<meta>` 설명 요소를 추가 합니다.

### <a name="programmatically-adding-markup-to-theheadregion"></a>프로그래밍 방식으로`<head>`영역에 태그 추가

헤드 ContentPlaceHolder를 사용 하면 사용자 지정 태그를 마스터 페이지의 `<head>` 영역에 선언적으로 추가할 수 있습니다. 사용자 지정 태그를 프로그래밍 방식으로 추가할 수도 있습니다. `Page` 클래스의 `Header` 속성은 마스터 페이지 (`<head runat="server">`)에 정의 된 `HtmlHead` 인스턴스를 반환 한다는 것을 기억 하세요.

`<head>` 영역에 프로그래밍 방식으로 콘텐츠를 추가 하는 것은 추가할 콘텐츠가 동적인 경우에 유용 합니다. 아마도 페이지를 방문 하는 사용자를 기반으로 합니다. 데이터베이스에서 끌어오는 것일 수 있습니다. 이유에 관계 없이 다음과 같이 컨트롤 컬렉션에 컨트롤을 추가 하 여 `HtmlHead`에 콘텐츠를 추가할 수 있습니다.

[!code-csharp[Main](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs/samples/sample15.cs)]

위의 코드는 `<head>` 영역에 `<meta>` keywords 요소를 추가 합니다 .이 요소는 페이지를 설명 하는 키워드의 쉼표로 구분 된 목록을 제공 합니다. `<meta>` 태그를 추가 하려면 [`HtmlMeta`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmlmeta.aspx) 인스턴스를 만들고 해당 `Name` 및 `Content` 속성을 설정한 다음 `Header`의 `Controls` 컬렉션에 추가 합니다. 마찬가지로 `<link>` 요소를 프로그래밍 방식으로 추가 하려면 [`HtmlLink`](https://msdn.microsoft.com/library/system.web.ui.htmlcontrols.htmllink.aspx) 개체를 만들고 해당 속성을 설정한 다음 `Header`의 `Controls` 컬렉션에 추가 합니다.

> [!NOTE]
> 임의의 태그를 추가 하려면 [`LiteralControl`](https://msdn.microsoft.com/library/system.web.ui.literalcontrol.aspx) 인스턴스를 만들고 해당 `Text` 속성을 설정한 다음 `Header`의 `Controls` 컬렉션에 추가 합니다.

## <a name="summary"></a>요약

이 자습서에서는 페이지 별로 `<head>` 지역 태그를 추가 하는 다양 한 방법을 살펴보았습니다. 마스터 페이지에는 ContentPlaceHolder `HtmlHead` 인스턴스 (`<head runat="server">`)가 포함 되어야 합니다. `HtmlHead` 인스턴스를 사용 하면 콘텐츠 페이지에서 프로그래밍 방식으로 `<head>` 영역에 액세스 하 고 페이지의 제목을 선언적으로 설정 하 고 프로그래밍 방식으로 설정할 수 있습니다. ContentPlaceHolder 컨트롤을 사용 하면 콘텐츠 컨트롤을 통해 사용자 지정 태그를 `<head>` 섹션에 선언적으로 추가할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET에서 페이지의 제목 동적 설정](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP를 검사 합니다. 네트워크의 사이트 탐색](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [HTML Meta 태그를 사용 하는 방법](http://searchenginewatch.com/showPage.html?page=2167931)
- [ASP.NET의 마스터 페이지](http://www.odetocode.com/articles/419.aspx)
- [ASP.NET 3.5의 ListView 및 DataPager 컨트롤 사용](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [ASP.NET 페이지의 코드 숨김으로 클래스에 대 한 사용자 지정 기본 클래스 사용](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)

### <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Zack Jones 및 Suchi Banerjee입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](multiple-contentplaceholders-and-default-content-cs.md)
> [다음](urls-in-master-pages-cs.md)
