---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 중첩 된 마스터 페이지C#() | Microsoft Docs
author: rick-anderson
description: 한 마스터 페이지를 다른 마스터 페이지에 중첩 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 67093266567a97cd22b353115616484fd9ef155e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463625"
---
# <a name="nested-master-pages-c"></a>중첩 마스터 페이지(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 한 마스터 페이지를 다른 마스터 페이지에 중첩 하는 방법을 보여 줍니다.

## <a name="introduction"></a>소개

지난 9 개 자습서를 진행 하는 과정에서 마스터 페이지를 사용 하 여 사이트 전체 레이아웃을 구현 하는 방법을 살펴보았습니다. 간단히 말해서, 마스터 페이지를 사용 하면 페이지 개발자가 콘텐츠 페이지 별로 사용자 지정할 수 있는 특정 영역과 함께 마스터 페이지에서 일반 태그를 정의할 수 있습니다. 마스터 페이지의 ContentPlaceHolder 컨트롤은 사용자 지정 가능한 영역을 의미 합니다. ContentPlaceHolder 컨트롤에 대 한 사용자 지정 태그는 콘텐츠 컨트롤을 통해 콘텐츠 페이지에 정의 됩니다.

지금까지 살펴본 마스터 페이지 기술은 전체 사이트에서 단일 레이아웃을 사용 하는 경우에 유용 합니다. 그러나 많은 규모의 웹 사이트에는 다양 한 섹션에서 사용자 지정 된 사이트 레이아웃이 있습니다. 예를 들어 병원 직원이 환자 정보, 활동 및 요금 청구를 관리 하는 데 사용 하는 의료 보험 응용 프로그램을 생각해 보세요. 이 응용 프로그램에는 다음과 같은 세 가지 유형의 웹 페이지가 있을 수 있습니다.

- 직원 구성원이 가용성을 업데이트 하거나 일정을 보거나 휴가 시간을 요청할 수 있는 구성원 관련 페이지를 담당 합니다.
- 직원 구성원이 특정 환자에 대 한 정보를 보거나 편집 하는 환자 별 페이지
- 회계사가 현재 클레임 상태와 재무 보고서를 검토 하는 청구 별 페이지

모든 페이지는 위쪽에 있는 메뉴 및 맨 아래에 자주 사용 되는 일련의 링크와 같은 공통 레이아웃을 공유할 수 있습니다. 하지만 직원, 환자 및 청구 관련 페이지는이 일반 레이아웃을 사용자 지정 해야 할 수 있습니다. 예를 들어 모든 직원 관련 페이지에는 현재 로그온 한 사용자의 사용 가능 여부와 매일 일정을 보여 주는 일정 및 작업 목록이 포함 되어 있을 것입니다. 모든 환자 관련 페이지에서 정보를 편집 중인 환자에 대 한 이름, 주소 및 보험 정보를 표시 해야 하는 경우가 있을 수 있습니다.

*중첩 된 마스터 페이지*를 사용 하 여 이러한 사용자 지정 레이아웃을 만들 수 있습니다. 위의 시나리오를 구현 하기 위해 먼저 사용자 지정할 수 있는 영역을 정의 하는 ContentPlaceHolders 표시자를 사용 하 여 사이트 전체 레이아웃, 메뉴 및 바닥글 콘텐츠를 정의 하는 마스터 페이지를 만듭니다. 그런 다음 각각의 웹 페이지 유형별로 하나씩 세 개의 중첩 된 마스터 페이지를 만듭니다. 각 중첩 된 마스터 페이지는 마스터 페이지를 사용 하는 콘텐츠 페이지 유형 사이에서 콘텐츠를 정의 합니다. 즉, 환자 별 콘텐츠 페이지의 중첩 된 마스터 페이지에는 편집 중인 환자에 대 한 정보를 표시 하는 태그 및 프로그래밍 논리가 포함 됩니다. 새 환자 관련 페이지를 만들 때이 중첩 된 마스터 페이지에 바인딩합니다.

이 자습서에서는 먼저 중첩 된 마스터 페이지의 이점을 강조 표시 합니다. 그런 다음 중첩 된 마스터 페이지를 만들고 사용 하는 방법을 보여 줍니다.

> [!NOTE]
> .NET Framework 버전 2.0부터 중첩 된 마스터 페이지를 사용할 수 있습니다. 그러나 Visual Studio 2005에는 중첩 된 마스터 페이지에 대 한 디자인 타임 지원이 포함 되지 않았습니다. Visual Studio 2008은 중첩 된 마스터 페이지에 다양 한 디자인 타임 환경을 제공 한다는 것이 좋습니다. 중첩 된 마스터 페이지를 사용 하려는 경우 Visual Studio 2005을 계속 사용 하려면 [Scott Guthrie](https://weblogs.asp.net/scottgu/)의 블로그 항목, [VS 2005 디자인 타임의 중첩 된 마스터 페이지에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)을 확인 하세요.

## <a name="the-benefits-of-nested-master-pages"></a>중첩 된 마스터 페이지의 이점

대부분의 웹 사이트에는 중요 한 사이트 디자인 뿐만 아니라 특정 페이지 유형에 특정 한 사용자 지정 디자인이 있습니다. 예를 들어 데모 웹 응용 프로그램에서 기본적인 관리 섹션 (`~/Admin` 폴더의 페이지)을 만들었습니다. 현재 `~/Admin` 폴더의 웹 페이지는 사용자의 선택에 따라 관리 섹션 (`Site.master` 또는 `Alternate.master`)에 없는 페이지와 동일한 마스터 페이지를 사용 합니다.

> [!NOTE]
> 지금은 사이트에 `Site.master`마스터 페이지가 하나만 있는 것으로 가정 합니다. 이 자습서의 뒷부분에 나오는 "관리 섹션에 대해 중첩 된 마스터 페이지 사용"으로 시작 하는 두 개 이상의 마스터 페이지로 중첩 된 마스터 페이지를 사용 하는 것이 좋습니다.

다른 방법으로 사이트의 다른 페이지에 표시 되지 않는 추가 정보 또는 링크를 포함 하도록 관리 페이지의 레이아웃을 사용자 지정 하 라는 메시지가 표시 된다고 가정 합니다. 이 요구 사항을 구현 하는 방법에는 다음 네 가지가 있습니다.

1. 관리 관련 정보 및 `~/Admin` 폴더의 모든 콘텐츠 페이지에 대 한 링크를 수동으로 추가 합니다.
2. 관리 섹션 관련 정보 및 링크를 포함 하도록 `Site.master` 마스터 페이지를 업데이트 한 다음, 관리 페이지 중 하나를 방문 하 고 있는지 여부에 따라 이러한 섹션을 표시 하거나 숨기려면 마스터 페이지에 코드를 추가 합니다.
3. 관리 섹션에 대해 특별히 새 마스터 페이지를 만들고 `Site.master`에서 태그를 복사 하 고 관리 섹션 관련 정보 및 링크를 추가한 다음 `~/Admin` 폴더의 콘텐츠 페이지를 업데이트 하 여이 새 마스터 페이지를 사용 합니다.
4. `Site.master`에 바인딩하고 `~/Admin` 폴더의 콘텐츠 페이지에서이 새 중첩 된 마스터 페이지를 사용 하도록 하는 중첩 된 마스터 페이지를 만듭니다. 이 중첩 된 마스터 페이지에는 관리 페이지에만 적용 되는 추가 정보 및 링크만 포함 되며 `Site.master`에 이미 정의 되어 있는 태그는 반복할 필요가 없습니다.

첫 번째 옵션은 가장 palatable입니다. 마스터 페이지를 사용 하는 전체 지점은 일반적인 태그를 수동으로 복사 하 여 새 ASP.NET 페이지에 붙여 넣을 필요가 없습니다. 두 번째 옵션은 허용 되지만 응용 프로그램을 유지 관리 하는 경우에만 표시 되는 태그를 사용 하 여 마스터 페이지의 상태를 변경 하 고, 이러한 태그를 해결 하기 위해 마스터 페이지를 편집 하는 개발자가 필요 하며, 정확히, 특정 태그는 숨겨진 경우에만 표시 됩니다. 이 방법을 사용 하면이 단일 마스터 페이지에서 수용 해야 하는 더 많은 유형의 웹 페이지에서 사용자 지정을 수행 하는 것이 더 어렵습니다.

세 번째 옵션은 두 번째 옵션으로 표시 되는 복잡 하 고 복잡 한 문제를 제거 합니다. 그러나이 옵션의 세 가지 주요 단점은 `Site.master`에서 일반적인 레이아웃을 복사 하 여 새 관리 섹션인 마스터 페이지에 붙여 넣는 것입니다. 나중에 사이트 전체 레이아웃을 변경 하려는 경우 두 위치에서 변경 해야 합니다.

네 번째 옵션인 중첩 된 마스터 페이지에서는 두 번째 및 세 번째 옵션을 제공 합니다. 사이트 전체 레이아웃 정보는 최상위 마스터 페이지인 하나의 파일에서 유지 관리 되는 반면 특정 지역과 관련 된 콘텐츠는 서로 다른 파일로 구분 됩니다.

이 자습서에서는 간단한 중첩 된 마스터 페이지를 만들고 사용 하는 방법을 살펴봅니다. 새 최상위 마스터 페이지, 두 개의 중첩 된 마스터 페이지 및 두 개의 콘텐츠 페이지를 만듭니다. "관리 섹션에 대해 중첩 된 마스터 페이지 사용"부터 중첩 된 마스터 페이지 사용을 포함 하도록 기존 마스터 페이지 아키텍처를 업데이트 하는 것을 확인 합니다. 특히 중첩 된 마스터 페이지를 만들고이를 사용 하 여 `~/Admin` 폴더의 콘텐츠 페이지에 대 한 추가 사용자 지정 콘텐츠를 포함 합니다.

## <a name="step-1-creating-a-simple-top-level-master-page"></a>1 단계: 간단한 최상위 마스터 페이지 만들기

기존 마스터 페이지 중 하나를 기반으로 하는 중첩 된 마스터를 만든 다음 기존 콘텐츠 페이지를 업데이트 하 여 최상위 마스터 페이지 대신이 새 중첩 마스터 페이지를 사용 하면 기존 콘텐츠 페이지에 이미 특정 최상위 마스터 페이지에 정의 된 ContentPlaceHolder 컨트롤입니다. 따라서 중첩 된 마스터 페이지에도 동일한 이름을 가진 동일한 ContentPlaceHolder 컨트롤이 포함 되어야 합니다. 또한 특정 데모 응용 프로그램에는 사용자의 기본 설정에 따라 콘텐츠 페이지에 동적으로 할당 되는 두 개의 마스터 페이지 (`Site.master` 및 `Alternate.master`)가 있으며,이는이 복잡성을 추가로 추가 합니다. 이 자습서의 뒷부분에서 중첩 된 마스터 페이지를 사용 하도록 기존 응용 프로그램을 업데이트 하는 방법에 대해 살펴보겠습니다 .이에 대해서는 먼저 간단한 중첩 된 마스터 페이지 예제에 집중 하겠습니다.

`NestedMasterPages` 이라는 새 폴더를 만든 다음 `Simple.master`라는 폴더에 새 마스터 페이지 파일을 추가 합니다. 이 폴더 및 파일이 추가 된 후의 솔루션 탐색기 스크린샷은 그림 1을 참조 하세요. 솔루션 탐색기에서 `AlternateStyles.css` 스타일 시트 파일을 디자이너로 끌어 옵니다. 이렇게 하면 `<link>` 요소가 `<head>` 요소의 스타일 시트 파일에 추가 되 고, 그 후에 마스터 페이지의 `<head>` 요소의 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

그런 다음 `Simple.master`웹 폼에 다음 태그를 추가 합니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

이 태그는 페이지 맨 위에 있는 "중첩 된 마스터 페이지 (단순)" 라는 링크를 짙은 배경에 진한 흰색 글꼴로 표시 합니다. `MainContent` ContentPlaceHolder입니다. 그림 1에서는 Visual Studio 디자이너에서 로드 될 때 `Simple.master` 마스터 페이지를 보여 줍니다.

[중첩 된 마스터 페이지 ![관리 섹션의 페이지와 관련 된 콘텐츠를 정의 합니다.](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**그림 01**: 중첩 된 마스터 페이지는 관리 섹션 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image3.png))의 페이지와 관련 된 콘텐츠를 정의 합니다.

## <a name="step-2-creating-a-simple-nested-master-page"></a>2 단계: 간단한 중첩 된 마스터 페이지 만들기

`Simple.master`에는 두 가지 ContentPlaceHolder 컨트롤이 포함 되어 있습니다. `MainContent` ContentPlaceHolder는 웹 양식 내에서 `<head>` 요소의 `head` ContentPlaceHolder와 함께 추가 됩니다. 콘텐츠 페이지를 만들고 `Simple.master`에 바인딩하는 경우 콘텐츠 페이지에 두 ContentPlaceHolders 표시자를 참조 하는 두 개의 콘텐츠 컨트롤이 있습니다. 마찬가지로 중첩 된 마스터 페이지를 만들고 `Simple.master` 바인딩하는 경우 중첩 된 마스터 페이지에는 두 개의 콘텐츠 컨트롤이 있습니다.

`SimpleNested.master`이라는 `NestedMasterPages` 폴더에 새 중첩 된 마스터 페이지를 추가 해 보겠습니다. `NestedMasterPages` 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 새 항목을 선택 합니다. 그러면 그림 2에 표시 된 새 항목 추가 대화 상자가 표시 됩니다. 마스터 페이지 템플릿 유형을 선택 하 고 새 마스터 페이지의 이름을 입력 합니다. 새 마스터 페이지가 중첩 된 마스터 페이지 여야 함을 나타내려면 "마스터 페이지 선택" 확인란을 선택 합니다.

그런 다음 추가 단추를 클릭 합니다. 그러면 마스터 페이지에 콘텐츠 페이지를 바인딩할 때 표시 되는 것과 동일한 마스터 페이지 선택 대화 상자가 표시 됩니다 (그림 3 참조). `NestedMasterPages` 폴더에서 `Simple.master` 마스터 페이지를 선택 하 고 확인을 클릭 합니다.

> [!NOTE]
> 웹 사이트 프로젝트 모델 대신 웹 응용 프로그램 프로젝트 모델을 사용 하 여 ASP.NET 웹 사이트를 만든 경우 그림 2에 표시 된 새 항목 추가 대화 상자에 "마스터 페이지 선택" 확인란이 표시 되지 않습니다. 웹 응용 프로그램 프로젝트 모델을 사용할 때 중첩 된 마스터 페이지를 만들려면 마스터 페이지 템플릿 대신 중첩 된 마스터 페이지 템플릿을 선택 해야 합니다. 중첩 된 마스터 페이지 템플릿을 선택 하 고 추가를 클릭 하면 그림 3에 표시 된 것과 같은 마스터 페이지 선택 대화 상자가 표시 됩니다.

[![&quot;마스터 페이지 선택&quot; 확인란을 선택 하 여 중첩 된 마스터 페이지를 추가 합니다.](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**그림 02**: "마스터 페이지 선택" 확인란을 선택 하 여 중첩 된 마스터 페이지 추가 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image6.png))

[중첩 된 마스터 페이지를 간단한 마스터 페이지에 ![바인딩합니다.](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**그림 03**: 중첩 된 마스터 페이지를 `Simple.master` 마스터 페이지에 바인딩 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image9.png))

아래에 표시 된 중첩 된 마스터 페이지의 선언 태그에는 최상위 마스터 페이지의 두 ContentPlaceHolder 컨트롤을 참조 하는 두 개의 콘텐츠 컨트롤이 포함 되어 있습니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

`<%@ Master %>` 지시어를 제외 하 고, 중첩 된 마스터 페이지의 초기 선언 태그는 콘텐츠 페이지를 동일한 최상위 마스터 페이지에 바인딩할 때 처음 생성 된 태그와 동일 합니다. 콘텐츠 페이지의 `<%@ Page %>` 지시문 처럼 여기에 `<%@ Master %>` 지시문은 중첩 된 마스터 페이지의 부모 마스터 페이지를 지정 하는 `MasterPageFile` 특성을 포함 합니다. 중첩 된 마스터 페이지와 동일한 최상위 마스터 페이지에 바인딩된 콘텐츠 페이지의 주요 차이점은 중첩 된 마스터 페이지에 ContentPlaceHolder 컨트롤을 포함할 수 있다는 것입니다. 중첩 된 마스터 페이지의 ContentPlaceHolder 컨트롤은 콘텐츠 페이지가 태그를 사용자 지정할 수 있는 영역을 정의 합니다.

"Hello, from SimpleNested!" 라는 텍스트가 표시 되도록이 중첩 된 마스터 페이지를 업데이트 합니다. `MainContent` ContentPlaceHolder 컨트롤에 해당 하는 콘텐츠 컨트롤입니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

이러한 추가 작업을 수행한 후에는 중첩 된 마스터 페이지를 저장 한 다음 `Default.aspx`이라는 `NestedMasterPages` 폴더에 새 콘텐츠 페이지를 추가 하 고 `SimpleNested.master` 마스터 페이지에 바인딩합니다. 이 페이지를 추가할 때 콘텐츠 컨트롤이 포함 되어 있지 않은 것을 볼 수 있습니다 (그림 4 참조). 콘텐츠 페이지는 *부모* 마스터 페이지의 contentplaceholders 표시자에만 액세스할 수 있습니다. `SimpleNested.master`에 ContentPlaceHolder 컨트롤이 포함 되어 있지 않습니다. 따라서이 마스터 페이지에 바인딩된 콘텐츠 페이지에는 콘텐츠 컨트롤을 포함할 수 없습니다.

[새 콘텐츠 페이지에 콘텐츠 컨트롤이 포함 되어 있지 ![](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**그림 04**: 새 콘텐츠 페이지에 콘텐츠 컨트롤 없음 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image12.png))

ContentPlaceHolder 컨트롤을 포함 하도록 중첩 된 마스터 페이지 (`SimpleNested.master`)를 업데이트 해야 합니다. 일반적으로 중첩 된 마스터 페이지는 부모 마스터 페이지에서 정의 된 각 ContentPlaceHolder에 대 한 ContentPlaceHolder를 포함 하 여 해당 자식 마스터 페이지 또는 콘텐츠 페이지가 최상위 마스터 페이지의 ContentPlaceHolder와 함께 작동 하도록 할 수 있습니다. 제어가.

두 콘텐츠 컨트롤에 ContentPlaceHolder를 포함 하도록 `SimpleNested.master` 마스터 페이지를 업데이트 합니다. ContentPlaceHolder 컨트롤에 콘텐츠 컨트롤이 참조 하는 ContentPlaceHolder 컨트롤과 동일한 이름을 지정 합니다. 즉, `Simple.master`의 `MainContent` ContentPlaceHolder를 참조 하는 `SimpleNested.master` 콘텐츠 컨트롤에 `MainContent` 이라는 ContentPlaceHolder 컨트롤을 추가 합니다. 콘텐츠 컨트롤에서 `head` ContentPlaceHolder를 참조 하는 동일한 작업을 수행 합니다.

> [!NOTE]
> 중첩 된 마스터 페이지에서 ContentPlaceHolder 컨트롤의 이름을 최상위 마스터 페이지의 ContentPlaceHolders 표시자와 동일 하 게 지정 하는 것이 좋지만이 명명 대칭은 필요 하지 않습니다. 중첩 된 마스터 페이지의 ContentPlaceHolder 컨트롤에 원하는 이름을 지정할 수 있습니다. 그러나 최상위 마스터 페이지와 중첩 된 마스터 페이지에서 동일한 이름을 사용 하는 경우 어떤 ContentPlaceHolders 표시 자가 페이지 영역에 해당 하는지 쉽게 기억할 수 있습니다.

이러한 추가 작업을 수행한 후 `SimpleNested.master` 마스터 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

방금 만든 `Default.aspx` 콘텐츠 페이지를 삭제 한 다음 다시 추가 하 여 `SimpleNested.master` 마스터 페이지에 바인딩합니다. 이번에는 Visual Studio가 `Default.aspx`에 두 콘텐츠 컨트롤을 추가 하 여 이제 `SimpleNested.master`에 정의 된 ContentPlaceHolders 표시자를 참조 합니다 (그림 6 참조). "Hello, from default.aspx!" 텍스트를 추가 합니다. `MainContent`를 참조 하는 콘텐츠 컨트롤입니다.

그림 5에는 여기에 포함 된 세 가지 엔터티 (`Simple.master`, `SimpleNested.master`및 `Default.aspx`와 서로 관련 된 방법이 나와 있습니다. 다이어그램에 표시 된 것 처럼 중첩 된 마스터 페이지는 부모의 ContentPlaceHolder에 대 한 콘텐츠 컨트롤을 구현 합니다. 콘텐츠 페이지에서 이러한 영역에 액세스할 수 있어야 하는 경우 중첩 된 마스터 페이지는 콘텐츠 컨트롤에 고유한 ContentPlaceHolders 표시자를 추가 해야 합니다.

[최상위 수준 및 중첩 된 마스터 페이지 ![콘텐츠 페이지의 레이아웃을 지시 합니다.](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**그림 05**: 최상위 및 중첩 마스터 페이지에서 콘텐츠 페이지의 레이아웃 결정 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image15.png))

이 동작은 콘텐츠 페이지 또는 마스터 페이지가 부모 마스터 페이지의 cognizant 하는 방법을 보여 줍니다. 이 동작은 Visual Studio 디자이너에도 표시 됩니다. 그림 6에서는 `Default.aspx`에 대 한 디자이너를 보여 줍니다. 디자이너는 콘텐츠 페이지에서 편집할 수 있는 지역이 명확 하 게 표시 되는 반면, 어떤 부분은 중첩 된 마스터 페이지에서 편집할 수 없는 영역이 명확 하 게 표시 되는 것이 아니라 최상위 마스터 페이지에서 어떤 지역이 어떤 영역 인지 명확 하지 않습니다.

[현재 콘텐츠 페이지에 중첩 된 마스터 페이지의 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤이 포함 되어 ![](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**그림 06**: 이제 콘텐츠 페이지에 중첩 된 마스터 페이지의 contentplaceholders 표시자에 대 한 콘텐츠 컨트롤 포함 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image18.png))

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>3 단계: 간단한 중첩 된 두 번째 마스터 페이지 추가

중첩 된 마스터 페이지의 장점에는 중첩 된 마스터 페이지가 여러 개 있을 때 더 분명 하 게 나타납니다. 이 혜택을 설명 하려면 `NestedMasterPages` 폴더에 중첩 된 다른 마스터 페이지를 만듭니다. 새 중첩 된 마스터 페이지의 이름을 `SimpleNestedAlternate.master` 하 여 `Simple.master` 마스터 페이지에 바인딩합니다. 2 단계에서 했던 것 처럼 중첩 된 마스터 페이지의 두 콘텐츠 컨트롤에 ContentPlaceHolder 컨트롤을 추가 합니다. 또한 "Hello, in SimpleNestedAlternate!" 텍스트를 추가 합니다. 최상위 마스터 페이지의 `MainContent` ContentPlaceHolder에 해당 하는 콘텐츠 컨트롤입니다. 이렇게 변경한 후에는 새 중첩 된 마스터 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

`NestedMasterPages` 폴더에 `Alternate.aspx` 라는 콘텐츠 페이지를 만들고 `SimpleNestedAlternate.master` 중첩 된 마스터 페이지에 바인딩합니다. "Hello, from from from!" 텍스트를 추가 합니다. `MainContent`에 해당 하는 콘텐츠 컨트롤입니다. 그림 7에는 Visual Studio Designer를 통해 볼 때 `Alternate.aspx` 표시 됩니다.

[![대체 .aspx는 SimpleNestedAlternate 마스터 페이지에 바인딩되어 있습니다.](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**그림 07**: `Alternate.aspx` `SimpleNestedAlternate.master` 마스터 페이지에 바인딩 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image21.png))

그림 7의 디자이너를 그림 6의 디자이너와 비교 합니다. 두 콘텐츠 페이지는 최상위 마스터 페이지 (`Simple.master`)에 정의 된 동일한 레이아웃을 공유 합니다. 즉, "중첩 된 마스터 페이지 자습서 (Simple)" 제목이 있습니다. 그러나 모두 부모 마스터 페이지에 정의 된 고유한 내용 ("Hello, from SimpleNested!")이 있습니다. 그림 6 및 "Hello, in SimpleNestedAlternate!" 그림 7에 있습니다. 여기에서 이러한 차이점은 간단 하지만,이 예제를 확장 하 여 보다 의미 있는 차이점을 포함할 수 있습니다. 예를 들어 `SimpleNested.master` 페이지에는 해당 콘텐츠 페이지에 대 한 옵션이 포함 된 메뉴가 포함 될 수 있지만 `SimpleNestedAlternate.master`에는 해당 콘텐츠 페이지와 관련 된 정보가 있을 수 있습니다.

이제는 중요 한 사이트 레이아웃을 변경 해야 한다고 가정 합니다. 예를 들어 모든 콘텐츠 페이지에 대 한 일반 링크 목록을 추가 하려고 한다고 가정 합니다. 이를 위해 최상위 마스터 페이지를 업데이트 `Simple.master`합니다. 모든 변경 내용은 중첩 된 마스터 페이지에 즉시 반영 되 고 확장을 통해 해당 콘텐츠 페이지에 반영 됩니다.

가장 중요 한 사이트 레이아웃을 변경할 수 있는 편의성을 보여 주기 위해 `Simple.master` 마스터 페이지를 열고 `topContent`와 `mainContent` `<div>` 요소 사이에 다음 태그를 추가 합니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

그러면 `Simple.master`, `SimpleNested.master`또는 `SimpleNestedAlternate.master`에 바인딩되는 모든 페이지의 맨 위에 두 개의 링크가 추가 됩니다. 이러한 변경 내용은 모든 중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 즉시 적용 됩니다. 그림 8에는 브라우저를 통해 볼 때 `Alternate.aspx` 표시 됩니다. 페이지 위쪽에 링크를 추가 합니다 (그림 7 참조).

[최상위 마스터 페이지로 변경 된 ![중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 즉시 반영 됩니다.](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**그림 08**: 최상위 마스터 페이지로 변경 된 내용을 중첩 된 마스터 페이지 및 해당 콘텐츠 페이지에 즉시 반영 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image24.png))

## <a name="using-a-nested-master-page-for-the-administration-section"></a>관리 섹션에 대해 중첩 된 마스터 페이지 사용

이 시점에서 중첩 된 마스터 페이지의 장점을 확인 하 고 ASP.NET 응용 프로그램에서이를 만들고 사용 하는 방법을 살펴보았습니다. 그러나 1, 2, 3 단계의 예는 새 최상위 마스터 페이지, 새 중첩 마스터 페이지 및 새 콘텐츠 페이지를 만드는 것과 관련이 있습니다. 기존 최상위 마스터 페이지 및 콘텐츠 페이지가 있는 웹 사이트에 새 중첩 된 마스터 페이지를 추가 하는 방법

중첩 된 마스터 페이지를 기존 웹 사이트에 통합 하 고 기존 콘텐츠 페이지와 연결 하는 것은 처음부터 시작 하는 것 보다 약간 더 많은 노력이 필요 합니다. 4, 5, 6, 7 단계에서는 관리자에 대 한 지침을 포함 하 고 `~/Admin` 폴더의 ASP.NET 페이지에서 사용 되는 `AdminNested.master` 이라는 새로운 중첩 된 마스터 페이지를 포함 하도록 데모 응용 프로그램을 보강 하 여 이러한 문제를 살펴봅니다.

중첩 된 마스터 페이지를 데모 응용 프로그램에 통합 하면 다음과 같은 문제가 있습니다.

- `~/Admin` 폴더의 기존 콘텐츠 페이지에는 마스터 페이지의 특정 요구 사항이 있습니다. 처음에는 특정 ContentPlaceHolder 컨트롤이 있는 것으로 간주 됩니다. 또한 `~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지는 마스터 페이지의 public `RefreshRecentProductsGrid` 메서드를 호출 하거나, `GridMessageText` 속성을 설정 하거나, 해당 `PricesDoubled` 이벤트에 대 한 이벤트 처리기를 포함 합니다. 따라서 중첩 된 마스터 페이지는 동일한 ContentPlaceHolders 표시자와 public 멤버를 제공 해야 합니다.
- 이전 자습서에서는 세션 변수에 따라 `Page` 개체의 `MasterPageFile` 속성을 동적으로 설정 하도록 `BasePage` 클래스를 향상 시켰습니다. 중첩 된 마스터 페이지를 사용할 때 동적 마스터 페이지를 지 원하는 방법

이러한 두 가지 문제는 중첩 된 마스터 페이지를 빌드하고 기존 콘텐츠 페이지에서 사용 하기 때문에 발생 합니다. 이러한 문제를 조사 하 고 surmount 합니다.

## <a name="step-4-creating-the-nested-master-page"></a>4 단계: 중첩 된 마스터 페이지 만들기

첫 번째 작업은 관리 섹션의 페이지에서 사용할 중첩 된 마스터 페이지를 만드는 것입니다. 2 단계에서 살펴본 것 처럼 새 중첩 된 마스터 페이지를 추가 하는 경우 중첩 된 마스터 페이지의 부모 마스터 페이지를 지정 해야 합니다. 그러나 두 개의 최상위 마스터 페이지인 `Site.master`와 `Alternate.master`있습니다. 이전 자습서에서 `Alternate.master`를 만들었으며 `Alternate.master` 세션 변수의 값에 따라 런타임에 Page 개체의 `MasterPageFile` 속성을 `Site.master` 또는 `MyMasterPage`로 설정 하는 코드를 `BasePage` 클래스에 작성 했습니다.

중첩 된 마스터 페이지를 적절 한 최상위 마스터 페이지를 사용 하도록 구성 하려면 어떻게 해야 하나요? 다음 두 가지 옵션이 있습니다.

- 두 개의 중첩 된 마스터 페이지, `AdminNestedSite.master` 및 `AdminNestedAlternate.master`을 만들고 최상위 마스터 페이지 `Site.master` 및 `Alternate.master`에 각각 바인딩합니다. `BasePage`에서 `Page` 개체의 `MasterPageFile`를 적절 한 중첩 마스터 페이지로 설정 합니다.
- 단일 중첩 마스터 페이지를 만들고 콘텐츠 페이지에서이 특정 마스터 페이지를 사용 하도록 합니다. 그런 다음 런타임에 중첩 된 마스터 페이지의 `MasterPageFile` 속성을 적절 한 최상위 마스터 페이지로 설정 해야 합니다. (지금까지 파악 했을 수 있으므로 마스터 페이지에도 `MasterPageFile` 속성이 있습니다.)

두 번째 옵션을 사용 하겠습니다. `AdminNested.master`이라는 `~/Admin` 폴더에 중첩 된 단일 마스터 페이지 파일을 만듭니다. `Site.master`와 `Alternate.master`는 ContentPlaceHolder 컨트롤의 집합을 동일 하 게 유지 하기 때문에 사용자가 바인딩하는 마스터 페이지는 중요 하지 않지만 일관성을 위해 `Site.master`에 바인딩하는 것이 좋습니다.

[중첩 된 마스터 페이지를 ~/Admin 폴더에 추가 ![합니다.](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**그림 09**: 중첩 된 마스터 페이지를 `~/Admin` 폴더에 추가 합니다. ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image27.png))

중첩 된 마스터 페이지는 네 개의 ContentPlaceHolder 컨트롤이 포함 된 마스터 페이지에 바인딩되기 때문에 Visual Studio에서는 네 개의 콘텐츠 컨트롤을 새 중첩 된 마스터 페이지 파일의 초기 태그에 추가 합니다. 2 단계와 3 단계에서와 같이 각 콘텐츠 컨트롤에 ContentPlaceHolder 컨트롤을 추가 하 여 최상위 마스터 페이지의 ContentPlaceHolder 컨트롤과 동일한 이름을 제공 합니다. 또한 `MainContent` ContentPlaceHolder에 해당 하는 콘텐츠 컨트롤에 다음 태그를 추가 합니다.

[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

그런 다음 `Styles.css` 및 `AlternateStyles.css` CSS 파일에 `instructions` CSS 클래스를 정의 합니다. 다음 CSS 규칙은 `instructions` 클래스를 사용 하 여 스타일을 지정 하는 HTML 요소가 밝은 노랑 배경색과 검정 실선 테두리와 함께 표시 되도록 합니다.

[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

이 태그는 중첩 된 마스터 페이지에 추가 되었으므로이 중첩 된 마스터 페이지를 사용 하는 페이지 (즉, 관리 섹션의 페이지)에만 표시 됩니다.

중첩 된 마스터 페이지를 추가 하 고 나면 해당 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

각 콘텐츠 컨트롤에는 ContentPlaceHolder 컨트롤이 있으며 ContentPlaceHolder 컨트롤의 `ID` 속성에는 최상위 마스터 페이지의 해당 ContentPlaceHolder 컨트롤과 동일한 값이 할당 됩니다. 또한 관리 섹션 관련 태그는 `MainContent` ContentPlaceHolder 표시 됩니다.

그림 10에는 Visual Studio의 디자이너를 통해 볼 때 중첩 된 마스터 페이지 `AdminNested.master` 표시 되어 있습니다. `MainContent` 콘텐츠 컨트롤의 맨 위에 있는 노란색 상자에서 지침을 확인할 수 있습니다.

[중첩 된 마스터 페이지를 ![하 여 관리자에 대 한 지침을 포함 하도록 최상위 마스터 페이지를 확장 합니다.](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**그림 10**: 중첩 된 마스터 페이지는 관리자에 대 한 지침을 포함 하도록 최상위 마스터 페이지를 확장 합니다. ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image30.png))

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>5 단계: 새 중첩 된 마스터 페이지를 사용 하도록 기존 콘텐츠 페이지 업데이트

새 콘텐츠 페이지를 관리 섹션에 추가할 때마다 방금 만든 `AdminNested.master` 마스터 페이지에 바인딩해야 합니다. 그러나 기존 콘텐츠 페이지는 어떻습니까? 현재 사이트의 모든 콘텐츠 페이지는 `BasePage` 클래스에서 파생 되며 런타임에 프로그래밍 방식으로 콘텐츠 페이지의 마스터 페이지를 설정 합니다. 이는 관리 섹션의 콘텐츠 페이지에 대해 원하는 동작이 아닙니다. 대신 이러한 콘텐츠 페이지에서 항상 `AdminNested.master` 페이지를 사용 하려고 합니다. 런타임에 오른쪽 최상위 콘텐츠 페이지를 선택 하는 것은 중첩 된 마스터 페이지의 책임입니다.

이 원하는 동작을 수행 하는 가장 좋은 방법은 `BasePage` 클래스를 확장 하는 `AdminBasePage` 이라는 새로운 사용자 지정 기본 페이지 클래스를 만드는 것입니다. 그런 다음 `SetMasterPageFile`를 재정의 하 고 `Page` 개체의 `MasterPageFile`를 하드 코드 된 값 "~/Admin/AdminNested.master"로 설정할 수 있습니다. `AdminBasePage` 이러한 방식으로 `AdminBasePage`에서 파생 되는 모든 페이지는 `AdminNested.master`를 사용 하는 반면 `BasePage`에서 파생 되는 모든 페이지는 `MyMasterPage` 세션 변수의 값을 기반으로 하 여 `MasterPageFile` 속성을 "~/Site.master" 또는 "~/Alternate.master"로 동적으로 설정 합니다.

`AdminBasePage.cs`이라는 `App_Code` 폴더에 새 클래스 파일을 추가 하 여 시작 합니다. `BasePage` `AdminBasePage` 확장 한 다음 `SetMasterPageFile` 메서드를 재정의 합니다. 이 메서드에서 `MasterPageFile` "~/Admin/AdminNested.master" 값을 할당 합니다. 이러한 변경을 수행한 후 클래스 파일은 다음과 같이 표시 됩니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

이제 관리 섹션의 기존 콘텐츠 페이지가 `BasePage`대신 `AdminBasePage`에서 파생 되어야 합니다. `~/Admin` 폴더의 각 콘텐츠 페이지에 대 한 코드를 사용 하는 클래스 파일로 이동 하 고이 변경 내용을 적용 합니다. 예를 들어 `~/Admin/Default.aspx`에서 코드 숨김이 클래스 선언을 다음과 같이 변경 합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

아래와 같이 변경합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

그림 11에서는 최상위 마스터 페이지 (`Site.master` 또는 `Alternate.master`), 중첩 된 마스터 페이지 (`AdminNested.master`) 및 관리 섹션 콘텐츠 페이지가 서로 관련 되는 방법을 보여 줍니다.

[중첩 된 마스터 페이지 ![관리 섹션의 페이지와 관련 된 콘텐츠를 정의 합니다.](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**그림 11**: 중첩 된 마스터 페이지는 관리 섹션 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image33.png))의 페이지와 관련 된 콘텐츠를 정의 합니다.

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>6 단계: 마스터 페이지의 공용 메서드 및 속성 미러링

`~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지는 마스터 페이지와 프로그래밍 방식으로 상호 작용 합니다. `~/Admin/AddProduct.aspx`는 마스터 페이지의 공용 `RefreshRecentProductsGrid` 메서드를 호출 하 고 해당 `GridMessageText` 속성을 설정 합니다. `~/Admin/Products.aspx`에 `PricesDoubled` 이벤트에 대 한 이벤트 처리기가 있습니다. 이전 자습서에서는 이러한 public 멤버를 정의 하는 추상 `BaseMasterPage` 클래스를 만들었습니다.

`~/Admin/AddProduct.aspx` 및 `~/Admin/Products.aspx` 페이지에서는 해당 마스터 페이지가 `BaseMasterPage` 클래스에서 파생 되는 것으로 가정 합니다. 그러나 `AdminNested.master` 페이지는 현재 `System.Web.UI.MasterPage` 클래스를 확장 합니다. 따라서 `~/Admin/Products.aspx` 방문할 때 "' .asp ' 형식의 개체를 ' .asp. admin\_adminnested\_master ' 형식으로 ' BaseMasterPage ' 형식으로 캐스팅할 수 없습니다." 라는 메시지와 함께 `InvalidCastException` throw 됩니다.

이 문제를 해결 하려면 `AdminNested.master` 코드 숨김이 `BaseMasterPage`를 확장 해야 합니다. 에서 중첩 된 마스터 페이지의 코드 숨김이 클래스 선언을 업데이트 합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

아래와 같이 변경합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

아직 완료 되지 않았습니다. `BaseMasterPage` 클래스는 추상적 이므로 `abstract` 멤버 `RefreshRecentProductsGrid` 및 `GridMessageText`를 재정의 해야 합니다. 이러한 멤버는 최상위 마스터 페이지에서 사용자 인터페이스를 업데이트 하는 데 사용 됩니다. (실제로 `Site.master` 마스터 페이지는 이러한 메서드를 사용 하지만, 두 가지 모두를 `BaseMasterPage`확장 하므로 최상위 마스터 페이지는 이러한 메서드를 구현 합니다.)

이러한 멤버는 `AdminNested.master`에서 구현 해야 하지만, 이러한 모든 구현은 중첩 된 마스터 페이지에서 사용 하는 최상위 마스터 페이지에서 동일한 멤버를 호출 하기만 하면 됩니다. 예를 들어 관리 섹션의 콘텐츠 페이지에서 중첩 된 마스터 페이지의 `RefreshRecentProductsGrid` 메서드를 호출 하는 경우 모든 중첩 된 마스터 페이지는 그 다음에 `Site.master` 또는 `Alternate.master`의 `RefreshRecentProductsGrid` 메서드를 호출 해야 합니다.

이렇게 하려면 먼저 `AdminNested.master`맨 위에 다음 `@MasterType` 지시문을 추가 합니다.

[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

`@MasterType` 지시문은 `Master`라는 코드를 만든 클래스에 강력한 형식의 속성을 추가 합니다. 그런 다음 `RefreshRecentProductsGrid` 및 `GridMessageText` 멤버를 재정의 하 고 단순히 `Master`의 해당 메서드에 대 한 호출을 위임 합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

이 코드가 준비 되 면 관리 섹션에서 콘텐츠 페이지를 방문 하 여 사용할 수 있어야 합니다. 그림 12는 브라우저를 통해 볼 때 `~/Admin/Products.aspx` 페이지를 보여 줍니다. 여기에서 볼 수 있듯이 페이지에는 중첩 된 마스터 페이지에 정의 되어 있는 관리 지침 상자가 포함 되어 있습니다.

[관리 섹션의 콘텐츠 페이지 ![각 페이지의 맨 위에 지침이 포함 되어 있습니다.](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**그림 12**: 관리 섹션의 콘텐츠 페이지에는 각 페이지의 맨 위에 있는 지침이 포함 됩니다 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image36.png)).

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>7 단계: 런타임에 적절 한 최상위 마스터 페이지 사용

관리 섹션의 모든 콘텐츠 페이지가 완전히 작동 하지만 모두 동일한 최상위 마스터 페이지를 사용 하 고 `ChooseMasterPage.aspx`에서 사용자가 선택한 마스터 페이지를 무시 합니다. 이 동작은 중첩 된 마스터 페이지의 `<%@ Master %>` 지시문에 `Site.master` 정적으로 설정 된 `MasterPageFile` 속성이 있으므로 발생 합니다.

최종 사용자가 선택한 최상위 마스터 페이지를 사용 하려면 `AdminNested.master`의 `MasterPageFile` 속성을 `MyMasterPage` 세션 변수의 값으로 설정 해야 합니다. `BasePage`에서 콘텐츠 페이지의 `MasterPageFile` 속성을 설정 하므로 `BaseMasterPage` 또는 `AdminNested.master`의 코드 숨김이 클래스에서 중첩 된 마스터 페이지의 `MasterPageFile` 속성을 설정 하는 것으로 생각할 수 있습니다. 그러나이는 PreInit 단계의 끝에 `MasterPageFile` 속성을 설정 해야 하기 때문에 작동 하지 않습니다. 마스터 페이지에서 페이지 수명 주기를 프로그래밍 방식으로 탭 할 수 있는 가장 빠른 시간은 Init 단계 (PreInit 단계 이후에 발생)입니다.

따라서 콘텐츠 페이지에서 중첩 된 마스터 페이지의 `MasterPageFile` 속성을 설정 해야 합니다. `AdminNested.master` 마스터 페이지를 사용 하는 콘텐츠 페이지는 `AdminBasePage`에서 파생 됩니다. 따라서 여기에이 논리를 추가할 수 있습니다. 5 단계에서는 `SetMasterPageFile` 메서드를 제거 하 여 `Page` 개체의 `MasterPageFile` 속성을 "~/Admin/AdminNested.master"로 설정 합니다. 또한 `SetMasterPageFile` 업데이트 하 여 마스터 페이지의 `MasterPageFile` 속성을 세션에 저장 된 결과로 설정 합니다.

[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

이전 자습서에서 `BasePage` 클래스에 추가한 `GetMasterPageFileFromSession` 메서드는 세션 변수 값에 따라 적절 한 마스터 페이지 파일 경로를 반환 합니다.

이와 같이 변경 하면 사용자의 마스터 페이지 선택이 관리 섹션으로 전달 됩니다. 그림 13에는 그림 12와 동일한 페이지가 표시 되지만 사용자가 마스터 페이지 선택을 변경한 후에는 `Alternate.master`합니다.

[중첩 된 관리 페이지 ![사용자가 선택한 최상위 마스터 페이지 사용](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**그림 13**: 중첩 된 관리 페이지에서 사용자가 선택한 최상위 마스터 페이지 사용 ([전체 크기 이미지를 보려면 클릭](nested-master-pages-cs/_static/image39.png))

## <a name="summary"></a>요약

콘텐츠 페이지를 마스터 페이지에 바인딩하는 방법과 마찬가지로 자식 마스터 페이지를 부모 마스터 페이지에 바인딩하기 때문에 중첩 된 마스터 페이지를 만들 수 있습니다. 자식 마스터 페이지는 각 부모의 ContentPlaceHolders 표시자에 대 한 콘텐츠 컨트롤을 정의할 수 있습니다. 그런 다음 이러한 콘텐츠 컨트롤에 자체 ContentPlaceHolder 컨트롤 및 기타 태그를 추가할 수 있습니다. 중첩 된 마스터 페이지는 모든 페이지에서 중요 한 모양과 느낌을 공유 하는 많은 웹 응용 프로그램에서 매우 유용 하지만 사이트의 특정 섹션에는 고유한 사용자 지정이 필요 합니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [중첩 된 ASP.NET 마스터 페이지](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [중첩 된 마스터 페이지 및 VS 2005 디자인 타임에 대 한 팁](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 중첩 된 마스터 페이지 지원](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 에 줄을 놓습니다.

> [!div class="step-by-step"]
> [이전](specifying-the-master-page-programmatically-cs.md)
> [다음](creating-a-site-wide-layout-using-master-pages-vb.md)
