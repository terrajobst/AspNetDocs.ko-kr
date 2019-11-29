---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
title: 여러 ContentPlaceHolders 표시자 및 기본 콘텐츠C#() | Microsoft Docs
author: rick-anderson
description: 콘텐츠 자리 표시자에서 기본 콘텐츠를 지정 하는 방법 뿐만 아니라 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법을 살펴봅니다.
ms.author: riande
ms.date: 05/21/2008
ms.assetid: b9b9798b-027d-46cc-9636-473378e437ac
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
msc.type: authoredcontent
ms.openlocfilehash: e902bcae05c0e7976a20293f2b01e5f2e2bee13a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639376"
---
# <a name="multiple-contentplaceholders-and-default-content-c"></a>여러 ContentPlaceHolders 및 기본 콘텐츠(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_CS.pdf)

> 콘텐츠 자리 표시자에서 기본 콘텐츠를 지정 하는 방법 뿐만 아니라 마스터 페이지에 여러 콘텐츠 자리 표시자를 추가 하는 방법을 살펴봅니다.

## <a name="introduction"></a>소개

이전 자습서에서는 마스터 페이지를 사용 하 여 ASP.NET 개발자가 일관 된 사이트 전체 레이아웃을 만드는 방법을 살펴보았습니다. 마스터 페이지는 페이지 별로 사용자 지정할 수 있는 모든 콘텐츠 페이지 및 영역에 공통적인 태그를 모두 정의 합니다. 이전 자습서에서는 간단한 마스터 페이지 (`Site.master`)와 두 개의 콘텐츠 페이지 (`Default.aspx` 및 `About.aspx`)를 만들었습니다. 마스터 페이지는 `head` 및 `MainContent`라는 두 개의 ContentPlaceHolders 표시자로 구성 되며, 각각 `<head>` 요소와 웹 폼에 있습니다. 콘텐츠 페이지에는 두 개의 콘텐츠 컨트롤이 있으므로 `MainContent`에 해당 하는 항목만 지정 합니다.

`Site.master`에서 두 ContentPlaceHolder 컨트롤을 복합적 마스터 페이지에는 여러 ContentPlaceHolders 표시 자가 포함 될 수 있습니다. 그리고 마스터 페이지에서 ContentPlaceHolder 컨트롤에 대 한 기본 태그를 지정할 수 있습니다. 그런 다음 콘텐츠 페이지에서 자체 태그를 선택적으로 지정 하거나 기본 태그를 사용할 수 있습니다. 이 자습서에서는 마스터 페이지에서 여러 콘텐츠 컨트롤 사용을 살펴보고 ContentPlaceHolder 컨트롤에서 기본 태그를 정의 하는 방법을 알아봅니다.

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>1 단계: 마스터 페이지에 추가 ContentPlaceHolder 컨트롤 추가

많은 웹 사이트 디자인에는 페이지 별로 사용자 지정 되는 여러 영역이 화면에 포함 되어 있습니다. `Site.master`이전 자습서에서 만든 마스터 페이지에는 `MainContent`이라는 웹 양식 내의 단일 ContentPlaceHolder 포함 됩니다. 특히이 ContentPlaceHolder는 `mainContent` `<div>` 요소 내에 있습니다.

그림 1에는 브라우저를 통해 볼 때 `Default.aspx` 표시 됩니다. 빨간색 원으로 표시 된 영역은 `MainContent`에 해당 하는 페이지 관련 태그입니다.

[원으로 표시 된 영역 ![페이지 별로 현재 사용자 지정 가능한 영역을 표시 합니다.](multiple-contentplaceholders-and-default-content-cs/_static/image2.png)](multiple-contentplaceholders-and-default-content-cs/_static/image1.png)

**그림 01**: 원으로 표시 된 영역에서 페이지 별로 현재 사용자 지정 가능한 영역 표시 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image3.png))

그림 1에 표시 된 영역 외에도 단원 및 뉴스 섹션 아래의 왼쪽 열에 페이지 특정 항목을 추가 해야 한다고 가정 합니다. 이를 위해 마스터 페이지에 또 다른 ContentPlaceHolder 컨트롤을 추가 합니다. 이를 수행 하려면 Visual Web Developer에서 `Site.master` 마스터 페이지를 연 다음 도구 상자의 ContentPlaceHolder 컨트롤을 News 섹션 뒤의 디자이너로 끌어 옵니다. ContentPlaceHolder의 `ID`를 `LeftColumnContent`로 설정 합니다.

[마스터 페이지의 왼쪽 열에 ContentPlaceHolder 컨트롤을 추가 ![](multiple-contentplaceholders-and-default-content-cs/_static/image5.png)](multiple-contentplaceholders-and-default-content-cs/_static/image4.png)

**그림 02**: 마스터 페이지의 왼쪽 열에 ContentPlaceHolder 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image6.png))

마스터 페이지에 `LeftColumnContent` ContentPlaceHolder를 추가 하면 `ContentPlaceHolderID` `LeftColumnContent`으로 설정 된 페이지에 콘텐츠 컨트롤을 포함 하 여 페이지 별로이 영역에 대 한 콘텐츠를 정의할 수 있습니다. 2 단계에서이 프로세스를 검토 합니다.

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>2 단계: 콘텐츠 페이지에서 새 ContentPlaceHolder에 대 한 콘텐츠 정의

웹 사이트에 새 콘텐츠 페이지를 추가 하면 Visual Web Developer에서 선택 된 마스터 페이지의 각 ContentPlaceHolder에 대해 페이지에 콘텐츠 컨트롤을 자동으로 만듭니다. 1 단계의 마스터 페이지에 `LeftColumnContent` ContentPlaceHolder를 추가 하면 새 ASP.NET 페이지에는 이제 3 개의 콘텐츠 컨트롤이 있습니다.

이를 설명 하려면 `Site.master` 마스터 페이지에 바인딩되는 `MultipleContentPlaceHolders.aspx` 이라는 루트 디렉터리에 새 콘텐츠 페이지를 추가 합니다. Visual Web Developer는 다음과 같은 선언 태그를 사용 하 여이 페이지를 만듭니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample1.aspx)]

`MainContent` ContentPlaceHolders 표시자 (`Content2`)를 참조 하는 콘텐츠 컨트롤에 일부 콘텐츠를 입력 합니다. 그런 다음 `Content3` 콘텐츠 컨트롤에 다음 태그를 추가 합니다 (`LeftColumnContent` ContentPlaceHolder 참조).

[!code-html[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample2.html)]

이 태그를 추가한 후 브라우저를 통해 페이지를 방문 합니다. 그림 3에 나와 있는 것 처럼 `Content3` 콘텐츠 컨트롤에 배치 된 태그는 News 섹션 (빨간색 원으로 표시 됨) 아래의 왼쪽 열에 표시 됩니다. `Content2`에 배치 된 태그는 페이지의 오른쪽 부분 (파란색 원으로 표시)에 표시 됩니다.

[이제 왼쪽 열에 News 섹션 아래의 페이지 관련 내용이 포함 된 ![](multiple-contentplaceholders-and-default-content-cs/_static/image8.png)](multiple-contentplaceholders-and-default-content-cs/_static/image7.png)

**그림 03**: 이제 왼쪽 열에 News 섹션 아래의 페이지 관련 내용이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image9.png)).

### <a name="defining-content-in-existing-content-pages"></a>기존 콘텐츠 페이지에서 콘텐츠 정의

새 콘텐츠 페이지를 만들 때 1 단계에서 추가한 ContentPlaceHolder 컨트롤이 자동으로 통합 됩니다. 그러나 두 개의 기존 콘텐츠 페이지 `About.aspx` 및 `Default.aspx`에는 `LeftColumnContent` ContentPlaceHolder에 대 한 콘텐츠 컨트롤이 없습니다. 이러한 두 개의 기존 페이지에서이 ContentPlaceHolder에 대 한 콘텐츠를 지정 하려면 콘텐츠 컨트롤을 직접 추가 해야 합니다.

대부분의 ASP.NET 웹 컨트롤과 달리 Visual Web Developer 도구 상자에는 콘텐츠 컨트롤 항목이 포함 되지 않습니다. 콘텐츠 컨트롤의 선언적 태그를 소스 뷰에 수동으로 입력할 수 있지만 더 쉽고 빠른 방법은 디자인 뷰를 사용 하는 것입니다. `About.aspx` 페이지를 열고 디자인 뷰로 전환 합니다. 그림 4에서 보여 주는 것 처럼 `LeftColumnContent` ContentPlaceHolder는 디자인 뷰에 표시 됩니다. 마우스를 가져가면 표시 되는 제목은 "왼쪽 열 내용 (마스터)"입니다. 제목에 "Master"가 포함 되어 있으면이 ContentPlaceHolder에 대 한 페이지에 정의 된 콘텐츠 컨트롤이 없음을 나타냅니다. `MainContent`에 대 한 경우와 같이 ContentPlaceHolder에 대 한 콘텐츠 컨트롤이 있으면 제목은 "*ContentPlaceHolderID* (Custom)"이 됩니다.

`LeftColumnContent` ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 `About.aspx`에 추가 하려면 ContentPlaceHolder의 스마트 태그를 확장 하 고 사용자 지정 콘텐츠 만들기 링크를 클릭 합니다.

[ContentPlaceHolder에 대 한 디자인 뷰에서는 왼쪽 Columncontent를 보여 줍니다. ![](multiple-contentplaceholders-and-default-content-cs/_static/image11.png)](multiple-contentplaceholders-and-default-content-cs/_static/image10.png)

**그림 04**: `About.aspx`의 디자인 뷰에 `LeftColumnContent` ContentPlaceHolder 표시 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image12.png))

사용자 지정 콘텐츠 만들기 링크를 클릭 하면 페이지에 필요한 콘텐츠 컨트롤이 생성 되 고 `ContentPlaceHolderID` 속성이 ContentPlaceHolder의 `ID`로 설정 됩니다. 예를 들어 `About.aspx`에서 `LeftColumnContent` 영역에 대 한 사용자 지정 콘텐츠 만들기 링크를 클릭 하면 페이지에 다음 선언적 태그가 추가 됩니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>콘텐츠 컨트롤 생략

ASP.NET에서는 모든 콘텐츠 페이지에 마스터 페이지에 정의 된 각 ContentPlaceHolder 및 모든에 대 한 콘텐츠 컨트롤을 포함할 필요가 없습니다. 콘텐츠 컨트롤을 생략 하면 ASP.NET 엔진은 마스터 페이지에서 ContentPlaceHolder 내에 정의 된 태그를 사용 합니다. 이 태그는 ContentPlaceHolder의 *기본 콘텐츠* 라고 하며, 일부 지역의 콘텐츠가 대부분의 페이지에서 공통적 이지만 소수의 페이지에 대해 사용자 지정 해야 하는 시나리오에서 유용 합니다. 3 단계에서는 마스터 페이지에서 기본 콘텐츠를 지정 하는 방법을 살펴봅니다.

현재 `Default.aspx`에는 `head` 및 `MainContent` ContentPlaceHolders 표시자에 대 한 두 개의 콘텐츠 컨트롤이 포함 되어 있습니다. `LeftColumnContent`에 대 한 콘텐츠 컨트롤이 없습니다. 따라서 `Default.aspx` 렌더링 되 면 `LeftColumnContent` ContentPlaceHolder의 기본 콘텐츠가 사용 됩니다. 이 ContentPlaceHolder에 대 한 기본 콘텐츠를 아직 정의 하지 않았기 때문에이 영역에 대 한 태그를 내보내지 않는 효과가 있습니다. 이 동작을 확인 하려면 브라우저를 통해 `Default.aspx`을 방문 하세요. 그림 5에 표시 된 것 처럼 News 섹션 아래의 왼쪽 열에는 태그를 내보내지 않습니다.

[![왼쪽 Columncontent ContentPlaceHolder에 대해 렌더링 된 콘텐츠가 없습니다.](multiple-contentplaceholders-and-default-content-cs/_static/image14.png)](multiple-contentplaceholders-and-default-content-cs/_static/image13.png)

**그림 05**: `LeftColumnContent` ContentPlaceHolder에 대해 렌더링 되는 콘텐츠 없음 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image15.png))

## <a name="step-3-specifying-default-content-in-the-master-page"></a>3 단계: 마스터 페이지에서 기본 콘텐츠 지정

일부 웹 사이트 디자인에는 하나 또는 두 개의 예외를 제외 하 고 사이트의 모든 페이지에 대해 내용이 동일한 지역이 포함 됩니다. 사용자 계정을 지 원하는 웹 사이트를 생각해 보세요. 이러한 사이트에는 방문자가 해당 자격 증명을 입력 하 여 사이트에 로그인 할 수 있는 로그인 페이지가 필요 합니다. 로그인 프로세스를 신속 하 게 진행 하기 위해 웹 사이트 디자이너에는 사용자가 로그인 페이지를 명시적으로 방문 하지 않고도 로그인 할 수 있도록 모든 페이지의 왼쪽 위 모서리에 사용자 이름 및 암호 텍스트 상자가 포함 될 수 있습니다. 이러한 사용자 이름 및 암호 텍스트 상자는 대부분의 페이지에서 유용 하지만 사용자의 자격 증명에 대 한 텍스트 상자를 이미 포함 하 고 있는 로그인 페이지에서 중복 됩니다.

이 디자인을 구현 하기 위해 마스터 페이지의 왼쪽 위 모퉁이에 ContentPlaceHolder 컨트롤을 만들 수 있습니다. 왼쪽 위 모서리에 사용자 이름 및 암호 텍스트 상자를 표시 해야 하는 각 페이지는이 ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 만들고 필요한 인터페이스를 추가 합니다. 반면에 로그인 페이지는이 ContentPlaceHolder에 대 한 콘텐츠 컨트롤 추가를 생략 하거나 태그를 정의 하지 않은 콘텐츠 컨트롤을 만듭니다. 이 방법의 단점은 로그인 페이지를 제외 하 고 사이트에 추가 하는 모든 페이지에 사용자 이름 및 암호 텍스트 상자를 추가 해야 한다는 것입니다. 이를 통해 문제를 요청 합니다. 이러한 텍스트 상자를 페이지 또는 둘에 추가 하는 것을 잊은 경우 인터페이스를 올바르게 구현 하지 않을 수 있습니다 (두 개의 텍스트 상자 대신 하나의 텍스트 상자를 추가 하는 것 처럼).

더 나은 솔루션은 사용자 이름 및 암호 텍스트 상자를 ContentPlaceHolder의 기본 콘텐츠로 정의 하는 것입니다. 이렇게 하면 사용자 이름 및 암호 텍스트 상자 (예를 들어 로그인 페이지)를 표시 하지 않는 일부 페이지에서이 기본 내용만 재정의 하면 됩니다. ContentPlaceHolder 컨트롤에 대 한 기본 콘텐츠를 지정 하는 방법을 보여 주기 위해 위에서 설명한 시나리오를 구현 해 보겠습니다.

> [!NOTE]
> 이 자습서의 나머지 부분에서는 로그인 페이지를 제외한 모든 페이지의 왼쪽 열에 로그인 인터페이스를 포함 하도록 웹 사이트를 업데이트 합니다. 그러나이 자습서에서는 사용자 계정을 지원 하도록 웹 사이트를 구성 하는 방법을 검토 하지 않습니다. 이 항목에 대 한 자세한 내용은 내 [양식 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 자습서를 참조 하세요.

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>ContentPlaceHolder 추가 및 기본 콘텐츠 지정

`Site.master` 마스터 페이지를 열고 `DateDisplay` 레이블과 단원 섹션 사이에 다음 태그를 왼쪽 열에 추가 합니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample4.aspx)]

이 태그를 추가한 후에는 마스터 페이지의 디자인 뷰 그림 6과 같이 표시 됩니다.

[![마스터 페이지에 로그인 컨트롤이 포함 되어 있습니다.](multiple-contentplaceholders-and-default-content-cs/_static/image17.png)](multiple-contentplaceholders-and-default-content-cs/_static/image16.png)

**그림 06**: 마스터 페이지에 로그인 컨트롤이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image18.png)).

이 ContentPlaceHolder `QuickLoginUI`에는 로그인 웹 컨트롤이 기본 콘텐츠로 포함 됩니다. 로그인 컨트롤은 로그인 단추와 함께 사용자 이름 및 암호를 입력 하 라는 메시지를 표시 하는 사용자 인터페이스를 표시 합니다. 로그인 단추를 클릭 하면 로그인 컨트롤이 멤버 자격 API에 대 한 사용자 자격 증명의 유효성을 내부적으로 검사 합니다. 실제로이 로그인 제어를 사용 하려면 멤버 자격을 사용 하도록 사이트를 구성 해야 합니다. 이 항목은이 자습서의 범위를 벗어났습니다. 사용자 계정을 지 원하는 웹 응용 프로그램을 빌드하는 방법에 대 한 자세한 내용은 내 [양식 인증, 권한 부여, 사용자 계정 및 역할](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) 자습서를 참조 하세요.

언제 든 지 자유롭게 로그인 컨트롤의 동작이 나 모양을 사용자 지정할 수 있습니다. `TitleText` 및 `FailureAction`의 두 속성을 설정 했습니다. 기본적으로 "로그인"으로 설정 되는 `TitleText` 속성 값은 컨트롤의 사용자 인터페이스 맨 위에 표시 됩니다. "로그인" 텍스트가 `<h3>` 요소로 표시 되도록이 속성을 설정 했습니다. `FailureAction` 속성은 사용자의 자격 증명이 잘못 된 경우 수행할 작업을 나타냅니다. 기본값은 `Refresh`값으로, 사용자를 동일한 페이지에 유지 하 고 로그인 컨트롤 내에 오류 메시지를 표시 합니다. `RedirectToLoginPage`로 변경 했으며, 잘못 된 자격 증명이 있는 경우 사용자를 로그인 페이지로 보냅니다. 사용자가 다른 페이지에서 로그인을 시도 하지만 로그인 페이지에 왼쪽 열에 쉽게 맞지 않는 추가 지침과 옵션이 포함 될 수 있기 때문에 사용자가 로그인 페이지로 전송 하는 것이 좋습니다. 예를 들어, 로그인 페이지에 잊어버린 암호를 검색 하거나 새 계정을 만드는 옵션이 포함 될 수 있습니다.

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>로그인 페이지 만들기 및 기본 콘텐츠 재정의

마스터 페이지가 완료 되 면 다음 단계는 로그인 페이지를 만드는 것입니다. `Login.aspx`이라는 사이트의 루트 디렉터리에 ASP.NET 페이지를 추가 하 여 `Site.master` 마스터 페이지에 바인딩합니다. 이렇게 하면 `Site.master`에 정의 된 각 ContentPlaceHolders 표시자 마다 하나씩 4 개의 콘텐츠 컨트롤이 있는 페이지가 만들어집니다.

`MainContent` 콘텐츠 컨트롤에 로그인 컨트롤을 추가 합니다. 마찬가지로 `LeftColumnContent` 영역에 콘텐츠를 자유롭게 추가할 수 있습니다. 그러나 `QuickLoginUI` ContentPlaceHolder의 콘텐츠 컨트롤은 비워 두어야 합니다. 그러면 로그인 컨트롤이 로그인 페이지의 왼쪽 열에 표시 되지 않습니다.

`MainContent` 및 `LeftColumnContent` 영역에 대 한 콘텐츠를 정의한 후에는 로그인 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample5.aspx)]

그림 7에서는 브라우저를 통해 볼 때이 페이지를 보여 줍니다. 이 페이지는 `QuickLoginUI` ContentPlaceHolder의 콘텐츠 컨트롤을 지정 하기 때문에 마스터 페이지에 지정 된 기본 콘텐츠를 재정의 합니다. 이렇게 하면 마스터 페이지의 디자인 뷰에 표시 되는 로그인 컨트롤이이 페이지에서 렌더링 되지 않습니다 (그림 6 참조).

[Represses QuickLoginUI ContentPlaceHolder의 기본 콘텐츠를 로그인 페이지를 ![합니다.](multiple-contentplaceholders-and-default-content-cs/_static/image20.png)](multiple-contentplaceholders-and-default-content-cs/_static/image19.png)

**그림 07**: 로그인 페이지가 `QuickLoginUI` ContentPlaceHolder의 기본 콘텐츠를 Represses ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image21.png))

### <a name="using-the-default-content-in-new-pages"></a>새 페이지에서 기본 콘텐츠 사용

로그인 페이지를 제외한 모든 페이지의 왼쪽 열에 로그인 컨트롤을 표시 하려고 합니다. 이를 위해 로그인 페이지를 제외한 모든 콘텐츠 페이지는 `QuickLoginUI` ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 생략 해야 합니다. 콘텐츠 컨트롤을 생략 하면 ContentPlaceHolder의 기본 콘텐츠가 대신 사용 됩니다.

`Default.aspx`, `About.aspx`및 `MultipleContentPlaceHolders.aspx` 등의 기존 콘텐츠 페이지에는 해당 ContentPlaceHolder 컨트롤을 마스터 페이지에 추가 하기 전에 만들어진 `QuickLoginUI`에 대 한 콘텐츠 컨트롤이 포함 되어 있지 않습니다. 따라서 이러한 기존 페이지를 업데이트할 필요가 없습니다. 그러나 웹 사이트에 추가 된 새 페이지에는 기본적으로 `QuickLoginUI` ContentPlaceHolder에 대 한 콘텐츠 컨트롤이 포함 됩니다. 따라서 로그인 페이지의 경우와 같이 ContentPlaceHolder의 기본 콘텐츠를 재정의 하지 않으려면 새 콘텐츠 페이지를 추가할 때마다 이러한 콘텐츠 컨트롤을 제거 해야 합니다.

콘텐츠 컨트롤을 제거 하려면 소스 뷰에서 선언적 태그를 수동으로 삭제 하거나, 디자인 뷰에서 스마트 태그의 마스터의 콘텐츠 링크에 대 한 기본값을 선택할 수 있습니다. 어느 방법이 든 페이지에서 콘텐츠 컨트롤을 제거 하 고 동일한 결과를 생성 합니다.

그림 8에는 브라우저를 통해 볼 때 `Default.aspx` 표시 됩니다. `Default.aspx`에는 `head` 및 `MainContent`에 대 한 선언적 태그에 두 개의 콘텐츠 컨트롤만 지정 되어 있습니다. 따라서 `LeftColumnContent` 및 `QuickLoginUI` ContentPlaceHolders 표시자에 대 한 기본 콘텐츠가 표시 됩니다.

[![왼쪽 열 내용 및 QuickLoginUI ContentPlaceHolders 표시자에 대 한 기본 콘텐츠가 표시 됩니다.](multiple-contentplaceholders-and-default-content-cs/_static/image23.png)](multiple-contentplaceholders-and-default-content-cs/_static/image22.png)

**그림 08**: `LeftColumnContent` 및 `QuickLoginUI` contentplaceholders 표시자에 대 한 기본 콘텐츠가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](multiple-contentplaceholders-and-default-content-cs/_static/image24.png)).

## <a name="summary"></a>요약

ASP.NET 마스터 페이지 모델을 사용 하면 마스터 페이지에서 임의 개수의 ContentPlaceHolders 표시자를 사용할 수 있습니다. 더 많은 내용, ContentPlaceHolders 표시자는 콘텐츠 페이지에 해당 콘텐츠 컨트롤이 없는 경우에 내보내지는 기본 콘텐츠를 포함 합니다. 이 자습서에서는 마스터 페이지에 추가 ContentPlaceHolder 컨트롤을 포함 하는 방법 및 새 ASP.NET 페이지에서 이러한 새 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤을 정의 하는 방법을 살펴보았습니다. 또한 ContentPlaceHolder에서 기본 콘텐츠를 지정 하는 방법에 대해 살펴보았습니다 .이는 소수의 페이지만 특정 지역 내에서 표준화 된 콘텐츠를 사용자 지정 해야 하는 경우에 유용 합니다.

다음 `head` 자습서에서는 ContentPlaceHolder에 대해 자세히 설명 하 고, 제목, 메타 태그 및 기타 HTML 헤더를 페이지 단위로 선언적으로 정의 하는 방법을 보여 줍니다.

행복 한 프로그래밍

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Suchi Banerjee. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](creating-a-site-wide-layout-using-master-pages-cs.md)
> [다음](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
