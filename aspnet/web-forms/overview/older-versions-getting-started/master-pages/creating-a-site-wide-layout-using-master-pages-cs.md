---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
title: 마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기C#() | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 마스터 페이지 기본 사항을 보여 줍니다. 즉, 마스터 페이지 란 무엇 이며, 마스터 페이지를 만드는 방법, 콘텐츠 자리 표시자는 어떻게 해야 하나요?
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 78f8d194-03b9-44a5-8255-90e7cd1c2ee1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a5e85c443a2a3642ec185ab1897c43cdb2ab1f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507335"
---
# <a name="creating-a-site-wide-layout-using-master-pages-c"></a>마스터 페이지를 사용하여 사이트 전체 레이아웃 만들기(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_CS.pdf)

> 이 자습서에서는 마스터 페이지 기본 사항을 보여 줍니다. 즉, 마스터 페이지 란 무엇 이며, 마스터 페이지를 만드는 방법, 콘텐츠 자리 표시자, 마스터 페이지를 사용 하는 ASP.NET 페이지를 만드는 방법, 마스터 페이지를 수정 하는 방법은 연결 된 콘텐츠 페이지 등에 자동으로 반영 됩니다.

## <a name="introduction"></a>소개

잘 디자인 된 웹 사이트의 한 가지 특성은 일관 된 사이트 전체 페이지 레이아웃입니다. [www.asp.net](www.asp.net) 웹 사이트를 예로 들어 보겠습니다. 이 문서를 작성할 당시에는 페이지의 위쪽과 아래쪽에 있는 모든 페이지의 내용이 동일 합니다. 그림 1에 나와 있는 것 처럼 각 페이지의 맨 위에는 Microsoft 커뮤니티 목록과 함께 회색 막대가 표시 됩니다. 그 아래에 사이트 로고, 사이트가 번역 된 언어 목록 및 핵심 섹션인 홈, 시작, 학습, 다운로드 등이 있습니다. 마찬가지로 페이지의 맨 아래 www.asp.net , 저작권, 개인정보취급방침 대 한 링크에 광고 정보를 포함 합니다.

[www.asp.net 웹 사이트 ![모든 페이지에서 일관 된 모양과 느낌을 적용 합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image1.png)

<strong>그림 01</strong>: Www.asp.net 웹 사이트는 모든 페이지에서 일관 된 모양과 느낌을 적용 합니다 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image3.png)).

잘 디자인 된 사이트의 또 다른 특성은 사이트의 모양을 변경할 수 있는 편리한 방법입니다. 그림 1은 3 월 2008 www.asp.net 홈 페이지를 보여 주지만, 현재와이 자습서의 게시 사이에서 모양과 느낌이 변경 되었을 수 있습니다. 아마도 위쪽의 메뉴 항목이 확장 되어 MVC 프레임 워크에 대 한 새 섹션이 포함 됩니다. 또는 다른 색, 글꼴 및 레이아웃을 사용 하는 완전히 새로운 디자인을 발표 수 있습니다. 이러한 변경 내용을 전체 사이트에 적용 하는 것은 사이트를 구성 하는 수천 개의 웹 페이지를 수정할 필요가 없는 빠르고 간단한 프로세스 여야 합니다.

*마스터 페이지*를 사용 하 여 ASP.NET에서 사이트 전체 페이지 템플릿을 만들 수 있습니다. 간단히 말해서, 마스터 페이지는 콘텐츠 페이지 별로 사용자 지정할 수 있는 영역 뿐만 아니라 모든 *콘텐츠 페이지* 간에 공통적인 태그를 정의 하는 특수 한 유형의 ASP.NET 페이지입니다. 콘텐츠 페이지는 마스터 페이지에 바인딩되는 ASP.NET 페이지입니다. 마스터 페이지의 레이아웃 또는 서식이 변경 될 때마다 모든 콘텐츠 페이지의 출력이 즉시 업데이트 되므로 단일 파일 (즉, 마스터 페이지)을 업데이트 하 고 배포 하는 것 만큼 쉽게 사이트 전체의 모양 변경을 적용할 수 있습니다.

마스터 페이지를 사용 하 여 탐색 하는 일련의 자습서에서 첫 번째 자습서입니다. 이 자습서 시리즈에서는 다음을 수행 합니다.

- 마스터 페이지 및 연결 된 콘텐츠 페이지 만들기를 검토 합니다.
- 다양 한 팁, 요령 및 트랩에 대해 논의 합니다.
- 일반적인 마스터 페이지 문제를 확인 하 고 해결 방법을 살펴보세요.
- 콘텐츠 페이지에서 마스터 페이지에 액세스 하는 방법 및 그 반대로
- 런타임에 콘텐츠 페이지의 마스터 페이지를 지정 하는 방법을 알아봅니다.
- 기타 고급 마스터 페이지 항목입니다.

이러한 자습서는 간결 하 게 만들어 프로세스를 시각적으로 안내 하는 다양 한 스크린 샷를 제공 하는 단계별 지침을 제공 합니다. 각 자습서는 및 Visual Basic C# 버전에서 사용할 수 있으며, 사용 되는 전체 코드의 다운로드를 포함 합니다.

이 개최 자습서에서는 마스터 페이지 기본 사항에 대해 살펴봅니다. 마스터 페이지의 작동 방식에 대해 설명 하 고, Visual Web Developer를 사용 하 여 마스터 페이지 및 연결 된 콘텐츠 페이지 만들기를 살펴보고, 마스터 페이지의 변경 내용이 해당 콘텐츠 페이지에 즉시 반영 되는 방식을 확인 합니다. 이제 시작하겠습니다.

## <a name="understanding-how-master-pages-work"></a>마스터 페이지의 작동 방식 이해

일관 된 사이트 전체 페이지 레이아웃을 사용 하 여 웹 사이트를 구축 하려면 각 웹 페이지에서 사용자 지정 콘텐츠 외에도 일반적인 서식 마크업 태그를 내보내야 합니다. 예를 들어 www.asp.net의 각 자습서 또는 포럼 게시물에 고유한 내용이 있는 경우 이러한 각 페이지는 홈, 시작, 학습 등 최상위 섹션 링크를 표시 하는 일련의 공통 `<div>` 요소를 렌더링 합니다.

일관 된 모양과 느낌을 가진 웹 페이지를 만드는 다양 한 기술이 있습니다. Naive 일반적인 레이아웃 태그를 모든 웹 페이지에 복사 하 여 붙여 넣는 것이 좋습니다. 그러나이 방법에는 여러 가지 단점이 있습니다. 처음에는 새 페이지를 만들 때마다 공유 콘텐츠를 복사 하 여 페이지에 붙여 넣어야 합니다. 실수로 공유 태그의 하위 집합만 새 페이지로 복사할 수 있으므로 이러한 복사 및 붙여넣기 작업은 오류에 ripe 됩니다. 또한이 접근 방식을 사용 하면 사이트의 모든 단일 페이지를 편집 하 여 새로운 모양과 느낌을 사용 하기 때문에 기존 사이트 전체 모양을 새로운 것으로 대체 합니다.

ASP.NET 버전 2.0 이전에는 페이지 개발자가 일반적으로 [사용자 컨트롤](https://msdn.microsoft.com/library/y6wb1a0e.aspx) 에 일반적인 태그를 배치한 다음 이러한 사용자 정의 컨트롤을 각 및 모든 페이지에 추가 했습니다. 이 접근 방식을 사용 하면 페이지 개발자가 모든 새 페이지에 사용자 정의 컨트롤을 수동으로 추가 해야 하지만, 공용 태그를 업데이트할 때 수정 해야 하는 사용자 컨트롤만 업데이트할 때 보다 쉽게 사이트 전체를 수정할 수 있습니다. 불행 하 게 Visual Studio .NET 2002 및 2003-ASP.NET 1.x 응용 프로그램을 만드는 데 사용 되는 Visual Studio 버전으로, 디자인 뷰에서 회색 상자로 렌더링 된 사용자 정의 컨트롤입니다. 따라서이 방법을 사용 하는 페이지 개발자는 WYSIWYG 디자인 타임 환경을 사용 하지 않았습니다.

사용자 정의 컨트롤을 사용 하는 경우 *마스터 페이지*의 도입으로 ASP.NET 버전 2.0 및 Visual Studio 2005에서 해결 되었습니다. 마스터 페이지는 사이트 전체의 태그와 연결 된 *콘텐츠 페이지* 에서 사용자 지정 태그를 정의 하는 *영역* 을 모두 정의 하는 특별 한 유형의 ASP.NET 페이지입니다. 1 단계에서 볼 수 있듯이 이러한 지역은 ContentPlaceHolder 컨트롤에 의해 정의 됩니다. ContentPlaceHolder 컨트롤은 콘텐츠 페이지에서 사용자 지정 콘텐츠를 삽입할 수 있는 마스터 페이지의 컨트롤 계층 구조에서 위치를 나타냅니다.

> [!NOTE]
> ASP.NET 버전 2.0 이후에는 마스터 페이지의 핵심 개념 및 기능이 변경 되지 않았습니다. 그러나 Visual Studio 2008는 Visual Studio 2005에 없는 기능인 중첩 된 마스터 페이지에 대 한 디자인 타임 지원을 제공 합니다. 이후 자습서에서 중첩 된 마스터 페이지를 사용 하는 방법을 살펴보겠습니다.

그림 2 www.asp.net 에 대 한 마스터 페이지 모양을 보여 줍니다. 마스터 페이지는 각 페이지의 위쪽, 아래쪽 및 오른쪽에 있는 태그와 각 개별 웹 페이지에 대 한 고유한 콘텐츠가 있는 왼쪽 가운데에 있는 ContentPlaceHolder 공통 사이트 전체 레이아웃을 정의 합니다.

![마스터 페이지는 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역을 정의 합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image4.png)

**그림 02**: 마스터 페이지에서 콘텐츠 페이지 별로 사이트 전체 레이아웃 및 편집 가능한 영역을 정의 합니다.

마스터 페이지를 정의한 후에는 checkbox의 눈금을 통해 새 ASP.NET 페이지에 바인딩할 수 있습니다. 이러한 ASP.NET 페이지-콘텐츠 페이지 라고 합니다. 각 마스터 페이지의 ContentPlaceHolder 컨트롤에 대 한 콘텐츠 컨트롤을 포함 합니다. 콘텐츠 페이지를 브라우저를 통해 방문할 때 ASP.NET 엔진은 마스터 페이지의 컨트롤 계층 구조를 만들고 콘텐츠 페이지의 컨트롤 계층 구조를 적절 한 위치에 삽입 합니다. 이 결합 된 컨트롤 계층은 렌더링 되 고 결과 HTML이 최종 사용자의 브라우저에 반환 됩니다. 따라서 콘텐츠 페이지는 ContentPlaceHolder 컨트롤 외부의 마스터 페이지에 정의 된 공통 태그와 자체 콘텐츠 컨트롤 내에 정의 된 페이지 관련 태그를 모두 내보냅니다. 그림 3에서는 이러한 개념을 보여 줍니다.

[요청 된 페이지의 태그가 마스터 페이지에 퓨즈 ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image5.png)

**그림 03**: 요청 된 페이지의 태그가 마스터 페이지에 퓨즈 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image7.png))

마스터 페이지의 작동 방식에 대해 설명 했으므로 이제 Visual Web Developer를 사용 하 여 마스터 페이지 및 연결 된 콘텐츠 페이지를 만드는 방법을 살펴보겠습니다.

> [!NOTE]
> 가장 광범위 한 대상 그룹에 도달 하기 위해이 자습서 시리즈 전반에서 빌드하는 ASP.NET 웹 사이트는 Microsoft의 무료 버전의 Visual Studio 2008, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)를 사용 하 여 ASP.NET 3.5을 사용 하 여 생성 됩니다. ASP.NET 3.5로 아직 업그레이드 하지 않은 경우 걱정 하지 마세요 .이 자습서에서 설명 하는 개념은 ASP.NET 2.0 및 Visual Studio 2005에서 동일 하 게 작동 합니다. 그러나 일부 데모 응용 프로그램은 .NET Framework 버전 3.5에 대 한 새로운 기능을 사용할 수 있습니다. 3.5 관련 기능을 사용 하는 경우 버전 2.0에서 유사한 기능을 구현 하는 방법을 설명 하는 메모를 포함 합니다. 각 자습서에서 다운로드할 수 있는 데모 응용 프로그램은 .NET Framework 버전 3.5을 대상으로 하며,이로 인해 3.5 관련 구성 요소와 ASP.NET 페이지의 코드 숨김으로 된 `using` 문에서 3.5 관련 네임 스페이스에 대 한 참조가 `Web.config` 파일에 포함 됩니다. 긴 스토리는 컴퓨터에 .NET 3.5을 설치 해야 하는 경우 먼저 `Web.config`에서 3.5 관련 태그를 제거 하지 않으면 다운로드할 수 있는 웹 응용 프로그램이 작동 하지 않습니다. 이 항목에 대 한 자세한 내용은 [개로 나누어서 ASP.NET Version 3.5 's `Web.config` File](http://www.4guysfromrolla.com/articles/121207-1.aspx) 을 참조 하세요. 3\.5 관련 네임 스페이스를 참조 하는 `using` 문도 제거 해야 합니다.

## <a name="step-1-creating-a-master-page"></a>1 단계: 마스터 페이지 만들기

마스터 및 콘텐츠 페이지 만들기 및 사용을 살펴보기 전에 먼저 ASP.NET 웹 사이트가 필요 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이렇게 하려면 Visual Web Developer를 시작한 다음 파일 메뉴로 이동 하 고 새 웹 사이트를 선택 하 여 새 웹 사이트 대화 상자를 표시 합니다 (그림 4 참조). ASP.NET 웹 사이트 템플릿을 선택 하 고, 위치 드롭다운 목록을 파일 시스템으로 설정 하 고, 웹 사이트를 저장할 폴더를 선택 하 고, 언어를로 C#설정 합니다. 그러면 `Default.aspx` ASP.NET 페이지, `App_Data` 폴더 및 `Web.config` 파일이 포함 된 새 웹 사이트가 만들어집니다.

> [!NOTE]
> Visual Studio는 웹 사이트 프로젝트와 웹 응용 프로그램 프로젝트의 두 가지 모드의 프로젝트 관리를 지원 합니다. 웹 사이트 프로젝트는 프로젝트 파일을 포함 하지 않지만, 웹 응용 프로그램 프로젝트는 Visual Studio .NET 2002/2003에서 프로젝트 아키텍처를 모방 합니다. 즉, 프로젝트 파일을 포함 하 고 프로젝트의 소스 코드를 단일 어셈블리로 컴파일하고 `/bin` 폴더에 배치 합니다. [웹 응용 프로그램 프로젝트 모델](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) 은 서비스 팩 1로 다시 도입 되었지만 Visual Studio 2005는 처음에만 지원 되는 웹 사이트 프로젝트입니다. Visual Studio 2008는 두 프로젝트 모델을 제공 합니다. 그러나 Visual Web Developer 2005 및 2008 버전은 웹 사이트 프로젝트만 지원 합니다. 이 자습서 시리즈의 데모에는 웹 사이트 프로젝트 모델을 사용 합니다. Express 이외의 버전을 사용 중이 고 웹 응용 프로그램 프로젝트 모델을 대신 사용 하려는 경우에는 자유롭게 수행할 수 있지만 화면에 표시 되는 내용과 표시 된 스크린 샷 및 instructio 단계 사이에 약간의 차이가 있을 수 있습니다. 이러한 자습서에서 제공 하는 ns입니다.

[새 파일 시스템 기반 웹 사이트 ![만들기](creating-a-site-wide-layout-using-master-pages-cs/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image8.png)

**그림 04**: 새 파일 시스템 기반 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image10.png))

그런 다음 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고, 새 항목 추가를 선택 하 고, 마스터 페이지 템플릿을 선택 하 여 루트 디렉터리에서 사이트에 마스터 페이지를 추가 합니다. 마스터 페이지는 확장 `.master`로 끝납니다. 새 마스터 페이지의 이름을 `Site.master` 하 고 추가를 클릭 합니다.

[Site .master 라는 마스터 페이지를 웹 사이트에 추가 ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image11.png)

**그림 05**: `Site.master` 이라는 마스터 페이지를 웹 사이트에 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image13.png))

Visual Web Developer를 통해 새 마스터 페이지 파일을 추가 하면 다음과 같은 선언 태그를 사용 하 여 마스터 페이지를 만듭니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample1.aspx)]

선언 태그의 첫 번째 줄은 [`@Master` 지시문](https://msdn.microsoft.com/library/ms228176.aspx)입니다. `@Master` 지시문은 ASP.NET 페이지에 표시 되는 [`@Page` 지시문](https://msdn.microsoft.com/library/ydy4x04a.aspx) 과 비슷합니다. 이 클래스는 서버 쪽 언어 (C#)와 마스터 페이지의 코드 숨김이 클래스의 위치 및 상속에 대 한 정보를 정의 합니다.

`DOCTYPE` 및 페이지의 선언적 태그가 `@Master` 지시문 아래에 나타납니다. 이 페이지에는 다음과 같은 네 가지 서버 쪽 컨트롤과 함께 정적 HTML이 포함 됩니다.

- **웹 폼 (`<form runat="server">`)** -모든 ASP.NET 페이지는 일반적으로 web form을 포함 하 고 있으며, 마스터 페이지에는 웹 양식 내에 표시 되어야 하는 웹 컨트롤이 포함 될 수 있으므로 웹 폼을 각 콘텐츠 페이지에 추가 하지 않고 마스터 페이지에 추가 해야 합니다.
- **`ContentPlaceHolder1`이라는 ContentPlaceHolder 컨트롤** -이 ContentPlaceHolder 컨트롤은 웹 폼에 표시 되 고 콘텐츠 페이지의 사용자 인터페이스에 대 한 영역으로 사용 됩니다.
- **서버 쪽 `<head>` 요소** -`<head>` 요소에는 서버 쪽 코드를 통해 액세스할 수 있도록 하는 `runat="server"` 특성이 있습니다. `<head>` 요소는 페이지의 제목과 기타 `<head>`관련 태그를 프로그래밍 방식으로 추가 하거나 조정할 수 있도록 이러한 방식으로 구현 됩니다. 예를 들어, ASP.NET 페이지의 `Title` 속성을 설정 하면 `<head>` 서버 컨트롤에 의해 렌더링 되는 `<title>` 요소가 변경 됩니다.
- **`head`이라는 ContentPlaceHolder 컨트롤** -이 ContentPlaceHolder 컨트롤은 `<head>` 서버 컨트롤 내에 표시 되며 `<head>` 요소에 선언적으로 콘텐츠를 추가 하는 데 사용할 수 있습니다.

이 기본 마스터 페이지 선언 태그는 사용자 고유의 마스터 페이지를 디자인 하기 위한 시작 점으로 사용 됩니다. 자유롭게 HTML을 편집 하거나 마스터 페이지에 웹 컨트롤 또는 ContentPlaceHolders 표시자를 추가 합니다.

> [!NOTE]
> 마스터 페이지를 디자인할 때 마스터 페이지에 웹 양식이 있고이 웹 폼에 하나 이상의 ContentPlaceHolder 컨트롤이 표시 되는지 확인 합니다.

### <a name="creating-a-simple-site-layout"></a>간단한 사이트 레이아웃 만들기

`Site.master`의 기본 선언적 태그를 확장 하 여 모든 페이지를 공유 하는 사이트 레이아웃을 만들 수 있습니다. 공통 헤더 탐색, 뉴스 및 기타 사이트 전체 콘텐츠가 있는 왼쪽 열 "Powered by Microsoft ASP.NET" 아이콘을 표시 하는 바닥글 그림 6에는 브라우저를 통해 해당 콘텐츠 페이지 중 하나를 볼 때 마스터 페이지의 최종 결과가 나와 있습니다. 그림 6의 빨간색 원 안의 지역은 방문한 페이지 (`Default.aspx`)와 관련이 있습니다. 다른 콘텐츠는 마스터 페이지에서 정의 되므로 모든 콘텐츠 페이지에서 일관성이 유지 됩니다.

[마스터 페이지 ![위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의 합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image14.png)

**그림 06**: 마스터 페이지는 위쪽, 왼쪽 및 아래쪽 부분에 대 한 태그를 정의 합니다 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image16.png)).

그림 6에 표시 된 사이트 레이아웃을 얻으려면 다음 선언 태그를 포함 하도록 `Site.master` 마스터 페이지를 업데이트 하는 것으로 시작 합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample2.aspx)]

마스터 페이지의 레이아웃은 일련의 `<div>` HTML 요소를 사용 하 여 정의 됩니다. `topContent` `<div>`는 각 페이지의 맨 위에 표시 되는 태그를 포함 하는 반면, `mainContent`, `leftContent`및 `footerContent` `<div>`를 사용 하 여 페이지의 내용, 왼쪽 열 및 "전원 Microsoft ASP.NET" 아이콘을 각각 표시 합니다. 이러한 `<div>` 요소를 추가 하는 것 외에도 기본 ContentPlaceHolder 컨트롤의 `ID` 속성을 `ContentPlaceHolder1`에서 `MainContent`로 바꾸었습니다.

이러한 다양 한 `<div>` 요소에 대 한 서식 지정 및 레이아웃 규칙은 [css (Css 스타일 시트)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) 파일 `Styles.css`에 있습니다 .이 파일은 마스터 페이지의 &lt;헤드&gt; 요소에서 &lt;링크&gt; 요소를 통해 지정 됩니다. 이러한 다양 한 규칙은 위에서 언급 한 각 `<div>` 요소의 모양과 느낌을 정의 합니다. 예를 들어 "마스터 페이지 자습서" 텍스트와 링크를 표시 하는 `topContent` `<div>` 요소에는 다음과 같이 `Styles.css`에 지정 된 서식 규칙이 있습니다.

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample3.css)]

컴퓨터를 함께 사용할 경우이 자습서의 코드를 다운로드 하 여 프로젝트에 `Styles.css` 파일을 추가 해야 합니다. 마찬가지로, 이미지 라는 폴더를 만들고 다운로드 한 demo 웹 사이트의 "전원 공급 Microsoft ASP.NET" 아이콘을 프로젝트에 복사 해야 합니다.

> [!NOTE]
> CSS 및 웹 페이지 서식 지정에 대 한 설명은이 문서의 범위를 벗어나는 것입니다. CSS에 대 한 자세한 내용은 [W3Schools.com](http://www.w3schools.com/)에서 [css 자습서](http://www.w3schools.com/css/default.asp) 를 확인 하세요. 또한이 자습서와 함께 제공 되는 코드를 다운로드 하 고 `Styles.css`에서 CSS 설정을 사용 하 여 다양 한 서식 지정 규칙의 효과를 확인 하는 것이 좋습니다.

### <a name="creating-a-master-page-using-an-existing-design-template"></a>기존 디자인 템플릿을 사용 하 여 마스터 페이지 만들기

몇 년 동안 중소 규모 회사를 위한 수많은 ASP.NET 웹 응용 프로그램을 빌드 했습니다. 일부 클라이언트에는 사용 하려는 기존 사이트 레이아웃이 있습니다. 다른 사람들은 특정 조항이 불법 그래픽 디자이너를 고용 했습니다. 몇 가지 위임 웹 사이트 레이아웃을 디자인 합니다. 그림 6에 설명 된 대로 프로그래머는 웹 사이트의 레이아웃을 디자인 하는 데 도움이 되는 것 처럼 일반적으로 회계사가 세금을 수술 하는 동안 오픈 하트를 수행 하는 것이 좋습니다.

다행히 무료 HTML 디자인 템플릿을 제공 하는 수많은 웹 사이트가 있습니다. Google은 검색 용어 "무료 웹 사이트 템플릿"에 대해 600만 개 보다 많은 결과를 반환 했습니다. 즐겨 찾는 항목 중 하나는 [OpenDesigns.org](http://opendesigns.org/)입니다. 원하는 웹 사이트 템플릿을 찾았으면 CSS 파일 및 이미지를 웹 사이트 프로젝트에 추가 하 고 템플릿의 HTML을 마스터 페이지에 통합 합니다.

> [!NOTE]
> Microsoft는 Visual Studio의 새 웹 사이트 대화 상자에 통합 되는 다양 한 [무료 ASP.NET 디자인 시작 키트 템플릿도](https://msdn.microsoft.com/asp.net/aa336613.aspx) 제공 합니다.

## <a name="step-2-creating-associated-content-pages"></a>2 단계: 연결 된 콘텐츠 페이지 만들기

마스터 페이지를 만든 경우 마스터 페이지에 바인딩되는 ASP.NET 페이지 만들기를 시작할 준비가 되었습니다. 이러한 페이지를 *콘텐츠 페이지*라고 합니다.

프로젝트에 새 ASP.NET 페이지를 추가 하 고 `Site.master` 마스터 페이지에 바인딩합니다. 솔루션 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가 옵션을 선택 합니다. 웹 양식 템플릿을 선택 하 고 이름 `About.aspx`입력 한 다음 그림 7에 표시 된 것 처럼 "마스터 페이지 선택" 확인란을 선택 합니다. 이렇게 하면 사용할 마스터 페이지를 선택할 수 있는 마스터 페이지 선택 대화 상자 (그림 8 참조)가 표시 됩니다.

> [!NOTE]
> 웹 사이트 프로젝트 모델 대신 웹 응용 프로그램 프로젝트 모델을 사용 하 여 ASP.NET 웹 사이트를 만든 경우 그림 7에 표시 된 새 항목 추가 대화 상자에 "마스터 페이지 선택" 확인란이 표시 되지 않습니다. 웹 응용 프로그램 프로젝트 모델을 사용할 때 콘텐츠 페이지를 만들려면 web Form 템플릿 대신 웹 콘텐츠 양식 템플릿을 선택 해야 합니다. 웹 콘텐츠 양식 서식 파일을 선택 하 고 추가를 클릭 한 후 그림 8에 표시 된 것과 같은 마스터 페이지 선택 대화 상자가 표시 됩니다.

[새 콘텐츠 페이지 ![추가](creating-a-site-wide-layout-using-master-pages-cs/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image17.png)

**그림 07**: 새 콘텐츠 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image19.png))

[![사이트 마스터 마스터 페이지를 선택 합니다.](creating-a-site-wide-layout-using-master-pages-cs/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image20.png)

**그림 08**: `Site.master` 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image22.png))

다음 선언적 태그가 보여 주는 것 처럼 새 콘텐츠 페이지에는 마스터 페이지의 ContentPlaceHolder 컨트롤 각각에 대 한 콘텐츠 컨트롤 및 마스터 페이지를 가리키는 `@Page` 지시문이 포함 되어 있습니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample4.aspx)]

> [!NOTE]
> 1 단계에서 "간단한 사이트 레이아웃 만들기" 섹션의 이름을 `MainContent``ContentPlaceHolder1`. 이와 같은 방식으로이 ContentPlaceHolder 컨트롤의 `ID` 이름을 변경 하지 않은 경우 콘텐츠 페이지의 선언적 태그는 위에 표시 된 태그와 약간 다를 수 있습니다. 즉, 두 번째 콘텐츠 컨트롤의 `ContentPlaceHolderID`은 마스터 페이지에서 해당 ContentPlaceHolder 컨트롤의 `ID`를 반영 합니다.

콘텐츠 페이지를 렌더링할 때 ASP.NET 엔진은 마스터 페이지의 ContentPlaceHolder 컨트롤을 사용 하 여 페이지의 콘텐츠 컨트롤을 퓨즈 해야 합니다. ASP.NET 엔진은 `@Page` 지시어의 `MasterPageFile` 특성에서 콘텐츠 페이지의 마스터 페이지를 결정 합니다. 위의 태그에서 볼 수 있듯이이 콘텐츠 페이지는 `~/Site.master`에 바인딩되어 있습니다.

마스터 페이지에는 두 개의 ContentPlaceHolder 컨트롤 `head` 있고 `MainContent`는 Visual Web Developer에서 두 개의 콘텐츠 컨트롤을 생성 했습니다. 각 콘텐츠 컨트롤은 `ContentPlaceHolderID` 속성을 통해 특정 ContentPlaceHolder을 참조 합니다.

마스터 페이지는 이전 사이트 전체 템플릿 기법을 기준으로 하는 경우 디자인 타임 지원과 함께 제공 됩니다. 그림 9에서는 Visual Web Developer의 디자인 뷰를 통해 볼 때 `About.aspx` 콘텐츠 페이지를 보여 줍니다. 마스터 페이지 콘텐츠는 표시 되지만 회색으로 표시 되 고 수정할 수 없습니다. 그러나 마스터 페이지의 ContentPlaceHolders 표시자에 해당 하는 콘텐츠 컨트롤은 편집할 수 있습니다. 다른 ASP.NET 페이지와 마찬가지로 소스 또는 디자인 뷰를 통해 웹 컨트롤을 추가 하 여 콘텐츠 페이지의 인터페이스를 만들 수 있습니다.

[콘텐츠 페이지의 디자인 뷰에 페이지 별 및 마스터 페이지 내용이 모두 표시 ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image23.png)

**그림 09**: 콘텐츠 페이지의 디자인 뷰에는 페이지 관련 및 마스터 페이지 내용이 모두 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image25.png)).

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>콘텐츠 페이지에 태그 및 웹 컨트롤 추가

잠시 시간을 사용 하 여 `About.aspx` 페이지에 대 한 콘텐츠를 만듭니다. 그림 10에서 볼 수 있듯이 "작성자 정보" 머리글과 몇 가지 텍스트 단락을 입력 했지만 웹 컨트롤도 자유롭게 추가할 수 있습니다. 이 인터페이스를 만든 후 브라우저를 통해 `About.aspx` 페이지를 방문 합니다.

[![브라우저를 통해 About .aspx 페이지를 방문 하세요.](creating-a-site-wide-layout-using-master-pages-cs/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image26.png)

**그림 10**: 브라우저를 통해 `About.aspx` 페이지 방문 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image28.png))

요청 된 콘텐츠 페이지와 연결 된 마스터 페이지는 웹 서버에서 전체적으로 전체적으로 렌더링 된다는 것을 이해 하는 것이 중요 합니다. 그러면 최종 사용자의 브라우저가 결과, 퓨즈 HTML로 전송 됩니다. 이를 확인 하려면 보기 메뉴로 이동 하 여 소스를 선택 하 여 브라우저에서 받은 HTML을 봅니다. 단일 창에서 두 개의 다른 웹 페이지를 표시 하는 데 사용할 수 있는 다른 기술 기술은 없습니다.

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>마스터 페이지를 기존 ASP.NET 페이지에 바인딩

이 단계에서 살펴본 것 처럼 ASP.NET 웹 응용 프로그램에 새 콘텐츠 페이지를 추가 하는 것은 "마스터 페이지 선택" 확인란을 선택 하 고 마스터 페이지를 선택 하는 것 만큼 쉽습니다. 아쉽게도 기존 ASP.NET 페이지를 마스터 페이지로 변환 하는 것은 쉽지 않습니다.

마스터 페이지를 기존 ASP.NET 페이지에 바인딩하려면 다음 단계를 수행 해야 합니다.

1. ASP.NET 페이지의 `@Page` 지시문에 `MasterPageFile` 특성을 추가 하 여 적절 한 마스터 페이지로 가리킵니다.
2. 마스터 페이지의 각 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤을 추가 합니다.
3. ASP.NET 페이지의 기존 콘텐츠를 선택적으로 잘라내어 적절 한 콘텐츠 컨트롤에 붙여넣습니다. ASP.NET 페이지에 `DOCTYPE`, `<html>` 요소 및 웹 양식과 같이 이미 마스터 페이지로 표현 된 태그가 포함 되어 있기 때문에 "선택적" 이라고 합니다.

이 프로세스에 대 한 단계별 지침은 스크린샷과 함께 [마스터 페이지 및 사이트 탐색 자습서를 사용 하 여](http://webproject.scottgu.com/CSharp/MasterPages/MasterPages.aspx) [Scott Guthrie](https://weblogs.asp.net/scottgu/)에서 확인 하세요. "`Default.aspx` 업데이트 및 마스터 페이지를 사용 하는 `DataSample.aspx`" 섹션에서는 이러한 단계를 자세히 설명 합니다.

기존 ASP.NET 페이지를 콘텐츠 페이지로 변환 하는 것 보다 새 콘텐츠 페이지를 만드는 것이 훨씬 쉽기 때문에 새 ASP.NET 웹 사이트를 만들 때마다 사이트에 마스터 페이지를 추가 하는 것이 좋습니다. 모든 새 ASP.NET 페이지를이 마스터 페이지에 바인딩합니다. 초기 마스터 페이지가 매우 단순 하거나 일반 인지 걱정 하지 마세요. 나중에 마스터 페이지를 업데이트할 수 있습니다.

> [!NOTE]
> 새 ASP.NET 응용 프로그램을 만들 때 Visual Web Developer는 마스터 페이지에 바인딩되지 않은 `Default.aspx` 페이지를 추가 합니다. 기존 ASP.NET 페이지를 콘텐츠 페이지로 변환 하는 방법을 연습 하려면 계속 진행 하 여 `Default.aspx`합니다. 또는 `Default.aspx`를 삭제 한 다음 다시 추가할 수 있지만 이번에는 "마스터 페이지 선택" 확인란을 선택 합니다.

## <a name="step-3-updating-the-master-pages-markup"></a>3 단계: 마스터 페이지의 태그 업데이트

마스터 페이지의 주요 이점 중 하나는 단일 마스터 페이지를 사용 하 여 사이트의 다양 한 페이지에 대 한 전체 레이아웃을 정의할 수 있다는 것입니다. 따라서 사이트의 모양과 느낌을 업데이트 하려면 단일 파일 (마스터 페이지)을 업데이트 해야 합니다.

이 동작을 설명 하기 위해 마스터 페이지를 업데이트 하 여 왼쪽 열 맨 위에 현재 날짜를 포함 해 보겠습니다. `DateDisplay` 이라는 레이블을 `leftContent` `<div>`에 추가 합니다.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample5.aspx)]

그런 다음 마스터 페이지에 대 한 `Page_Load` 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample6.cs)]

위의 코드에서는 레이블의 `Text` 속성을 요일, 월 이름 및 두 자리 일로 서식이 지정 된 현재 날짜 및 시간으로 설정 합니다 (그림 11 참조). 이 변경으로 콘텐츠 페이지 중 하나를 다시 방문 하세요. 그림 11에서 볼 수 있듯이 결과 태그는 마스터 페이지에 변경 내용을 포함 하도록 즉시 업데이트 됩니다.

[콘텐츠 페이지를 볼 때 마스터 페이지의 변경 내용이 반영 ![](creating-a-site-wide-layout-using-master-pages-cs/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image29.png)

**그림 11**: 마스터 페이지에 대 한 변경 내용은 콘텐츠 페이지를 볼 때 반영 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-site-wide-layout-using-master-pages-cs/_static/image31.png)).

> [!NOTE]
> 이 예제에서 보여 주는 것 처럼 마스터 페이지에는 서버측 웹 컨트롤, 코드 및 이벤트 처리기가 포함 될 수 있습니다.

## <a name="summary"></a>요약

마스터 페이지를 사용 하면 ASP.NET 개발자가 쉽게 업데이트할 수 있는 일관 된 사이트 전체 레이아웃을 디자인할 수 있습니다. Visual Web Developer에서 다양 한 디자인 타임 지원을 제공 하므로 마스터 페이지와 연결 된 콘텐츠 페이지를 만드는 것은 표준 ASP.NET 페이지를 만드는 것 만큼 간단 합니다.

이 자습서에서 만든 마스터 페이지 예제에는 두 개의 ContentPlaceHolder 컨트롤 `head` 및 `MainContent`있습니다. 그러나 콘텐츠 페이지의 `MainContent` ContentPlaceHolder 컨트롤에 대해서만 태그를 지정 했습니다. 다음 자습서에서는 콘텐츠 페이지에서 여러 콘텐츠 컨트롤 사용을 살펴봅니다. 또한 마스터 페이지 내에서 콘텐츠 컨트롤에 대 한 기본 태그를 정의 하 고 마스터 페이지에 정의 된 기본 태그를 사용 하 고 콘텐츠 페이지에서 사용자 지정 태그를 제공 하는 방법을 설정 하는 방법을 알아봅니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET for Designer: 무료 디자인 템플릿 및 웹 표준을 사용 하 여 ASP.NET Websites 빌드에 대 한 지침](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 마스터 페이지 개요](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [CSS (css 스타일) 자습서](http://www.w3schools.com/css/default.asp)
- [페이지 제목 동적 설정](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET의 마스터 페이지](http://www.odetocode.com/articles/419.aspx)
- [마스터 페이지 빠른 시작 자습서](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [다음](multiple-contentplaceholders-and-default-content-cs.md)
