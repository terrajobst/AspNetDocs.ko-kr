---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
title: 보기 마스터 페이지를 사용 하 여 페이지 레이아웃 만들기 (VB) | Microsoft Docs
author: microsoft
description: 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다. ...를 사용 하 여
ms.author: riande
ms.date: 10/16/2008
ms.assetid: d34f90a1-6de3-482a-a326-f87fdcbaaaff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 97c0ecf1953cc54030656dd710a5150243877110
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593927"
---
# <a name="creating-page-layouts-with-view-master-pages-vb"></a>보기 마스터 페이지를 사용하여 페이지 레이아웃 만들기(VB)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_VB.pdf)

> 이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다. 예를 들어, 뷰 마스터 페이지를 사용 하 여 2 열 페이지 레이아웃을 정의 하 고 웹 응용 프로그램의 모든 페이지에 대해 2 열 레이아웃을 사용할 수 있습니다.

## <a name="creating-page-layouts-with-view-master-pages"></a>보기 마스터 페이지를 사용 하 여 페이지 레이아웃 만들기

이 자습서에서는 보기 마스터 페이지를 활용 하 여 응용 프로그램에서 여러 페이지에 대 한 공통 페이지 레이아웃을 만드는 방법에 대해 알아봅니다. 예를 들어, 뷰 마스터 페이지를 사용 하 여 2 열 페이지 레이아웃을 정의 하 고 웹 응용 프로그램의 모든 페이지에 대해 2 열 레이아웃을 사용할 수 있습니다.

또한 보기 마스터 페이지를 활용 하 여 응용 프로그램의 여러 페이지에서 공통 콘텐츠를 공유할 수 있습니다. 예를 들어 보기 마스터 페이지에서 웹 사이트 로고, 탐색 링크 및 배너 광고를 저장할 수 있습니다. 이렇게 하면 응용 프로그램의 모든 페이지가이 콘텐츠를 자동으로 표시 합니다.

이 자습서에서는 새 보기 마스터 페이지를 만들고 마스터 페이지를 기준으로 새 콘텐츠 보기 페이지를 만드는 방법에 대해 알아봅니다.

### <a name="creating-a-view-master-page"></a>보기 마스터 페이지 만들기

2 열 레이아웃을 정의 하는 보기 마스터 페이지를 만들어 시작 해 보겠습니다. Views\Shared 폴더를 마우스 오른쪽 단추로 클릭 하 고, 메뉴 옵션 **추가, 새 항목**을 차례로 선택 하 고, Mvc 뷰 마스터 페이지 템플릿을 선택 하 여 mvc 프로젝트에 새 뷰 마스터 페이지를 추가 합니다 (그림 1 참조).

[보기 마스터 페이지를 추가 ![](creating-page-layouts-with-view-master-pages-vb/_static/image2.png)](creating-page-layouts-with-view-master-pages-vb/_static/image1.png)

**그림 01**: 보기 마스터 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image3.png))

응용 프로그램에서 둘 이상의 뷰 마스터 페이지를 만들 수 있습니다. 각 보기 마스터 페이지는 다른 페이지 레이아웃을 정의할 수 있습니다. 예를 들어, 특정 페이지에 2 열 레이아웃 및 다른 페이지를 포함 하 여 3 열 레이아웃을 사용할 수 있습니다.

보기 마스터 페이지는 표준 ASP.NET MVC 뷰와 매우 유사 하 게 보입니다. 그러나 기본 보기와 달리 보기 마스터 페이지에는 하나 이상의 `<asp:ContentPlaceHolder>` 태그가 포함 됩니다. `<contentplaceholder>` 태그는 개별 콘텐츠 페이지에서 재정의할 수 있는 마스터 페이지 영역을 표시 하는 데 사용 됩니다.

예를 들어 1을 나열 하는 보기 마스터 페이지는 2 열 레이아웃을 정의 합니다. 두 개의 `<contentplaceholder>` 태그를 포함 합니다. 각 열에 대해 하나의 `<ContentPlaceHolder>` 합니다.

**목록 1 – `Views\Shared\Site.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample1.aspx)]

목록 1에 있는 보기 마스터 페이지의 본문에는 두 열에 해당 하는 두 개의 `<div>` 태그가 있습니다. Css 스타일 시트 열 클래스는 두 `<div>` 태그에 모두 적용 됩니다. 이 클래스는 마스터 페이지의 맨 위에 선언 된 스타일 시트에 정의 됩니다. 디자인 뷰로 전환 하 여 보기 마스터 페이지가 렌더링 되는 방식을 미리 볼 수 있습니다. 소스 코드 편집기의 왼쪽 아래에 있는 디자인 탭을 클릭 합니다 (그림 2 참조).

[디자이너에서 마스터 페이지 미리 보기 ![](creating-page-layouts-with-view-master-pages-vb/_static/image5.png)](creating-page-layouts-with-view-master-pages-vb/_static/image4.png)

**그림 02**: 디자이너에서 마스터 페이지 미리 보기 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image6.png))

### <a name="creating-a-view-content-page"></a>콘텐츠 보기 페이지 만들기

보기 마스터 페이지를 만든 후에는 보기 마스터 페이지를 기준으로 하나 이상의 콘텐츠 페이지를 만들 수 있습니다. 예를 들어 Views\Home 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 항목**, **MVC 뷰 콘텐츠 페이지** 템플릿을 차례로 선택 하 고 이름으로 .aspx를 입력 한 다음 추가 단추를 클릭 하 여 홈 컨트롤러에 대 한 인덱스 보기 콘텐츠 페이지를 만들 수 있습니다 (그림 3 참조).

[콘텐츠 보기 페이지를 추가 ![](creating-page-layouts-with-view-master-pages-vb/_static/image8.png)](creating-page-layouts-with-view-master-pages-vb/_static/image7.png)

**그림 03**: 콘텐츠 보기 페이지 추가 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image9.png))

추가 단추를 클릭 하면 보기 마스터 페이지를 선택 하 여 콘텐츠 보기 페이지와 연결할 수 있는 새 대화 상자가 나타납니다 (그림 4 참조). 이전 섹션에서 만든 Site. 마스터 뷰 마스터 페이지로 이동할 수 있습니다.

[마스터 페이지를 선택 ![](creating-page-layouts-with-view-master-pages-vb/_static/image11.png)](creating-page-layouts-with-view-master-pages-vb/_static/image10.png)

**그림 04**: 마스터 페이지 선택 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image12.png))

사이트. 마스터 마스터 페이지를 기준으로 새 콘텐츠 보기 페이지를 만든 후에는 목록 2에 파일을 가져옵니다.

**목록 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample2.aspx)]

이 뷰에는 보기 마스터 페이지의 각 `<asp:ContentPlaceHolder>` 태그에 해당 하는 `<asp:Content>` 태그가 포함 되어 있습니다. 각 `<asp:Content>` 태그는 재정의 하는 특정 `<asp:ContentPlaceHolder>`를 가리키는 ContentPlaceHolderID 특성을 포함 합니다.

또한 목록 2의 콘텐츠 보기 페이지에는 일반 여는 태그와 닫는 HTML 태그가 포함 되지 않습니다. 예를 들어 열기 및 닫기 `<html>` 또는 `<head>` 태그가 포함 되지 않습니다. 모든 일반 여는 태그와 닫는 태그는 보기 마스터 페이지에 포함 되어 있습니다.

콘텐츠 보기 페이지에 표시 하려는 콘텐츠는 `<asp:Content>` 태그 안에 배치 해야 합니다. HTML 또는 기타 콘텐츠를 이러한 태그 외부에 두면 페이지를 보려고 할 때 오류가 발생 합니다.

콘텐츠 뷰 페이지에서 마스터 페이지의 모든 `<asp:ContentPlaceHolder>` 태그를 재정의할 필요는 없습니다. 태그를 특정 콘텐츠로 바꾸려는 경우에만 `<asp:ContentPlaceHolder>` 태그를 재정의 해야 합니다.

예를 들어 목록 3의 수정 된 인덱스 뷰에는 두 개의 `<asp:Content>` 태그만 있습니다. 각 `<asp:Content>` 태그에는 일부 텍스트가 포함 됩니다.

**목록 3 – `Views\Home\Index.aspx (modified)`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample3.aspx)]

목록 3의 보기가 요청 되 면 그림 5에서 페이지가 렌더링 됩니다. 뷰는 두 개의 열이 있는 페이지를 렌더링 합니다. 또한 콘텐츠 보기 페이지의 콘텐츠가 보기 마스터 페이지의 내용과 병합 됩니다.

[인덱스 보기 콘텐츠 페이지 ![](creating-page-layouts-with-view-master-pages-vb/_static/image14.png)](creating-page-layouts-with-view-master-pages-vb/_static/image13.png)

**그림 05**: 인덱스 뷰 콘텐츠 페이지 ([전체 크기 이미지를 보려면 클릭](creating-page-layouts-with-view-master-pages-vb/_static/image15.png))

### <a name="modifying-view-master-page-content"></a>보기 마스터 페이지 내용 수정

보기 마스터 페이지를 사용할 때 발생 하는 문제 중 하나는 다른 보기 콘텐츠 페이지가 요청 될 때 보기 마스터 페이지 내용을 수정 하는 문제입니다. 예를 들어 웹 응용 프로그램의 각 페이지에 고유한 제목을 지정할 수 있습니다. 그러나 제목은 뷰 마스터 페이지에서 선언 되 고 콘텐츠 보기 페이지에는 선언 되지 않습니다. 따라서 각 콘텐츠 보기 페이지에 대 한 페이지 제목을 사용자 지정 하려면 어떻게 해야 하나요?

콘텐츠 보기 페이지에 표시 되는 제목을 수정할 수 있는 두 가지 방법이 있습니다. 먼저 콘텐츠 보기 페이지의 맨 위에 선언 된 `<%@ page %>` 지시문의 title 특성에 페이지 제목을 할당할 수 있습니다. 예를 들어 인덱스 뷰에 페이지 제목 "Super 유용한 웹 사이트"를 할당 하려는 경우 인덱스 뷰의 맨 위에 다음 지시문을 포함할 수 있습니다.

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample4.aspx)]

인덱스 뷰가 브라우저에 렌더링 되 면 원하는 제목이 브라우저 제목 표시줄에 표시 됩니다.

[![브라우저 제목 표시줄](creating-page-layouts-with-view-master-pages-vb/_static/image17.png)](creating-page-layouts-with-view-master-pages-vb/_static/image16.png)

마스터 뷰 페이지는 제목 특성이 작동 하기 위해 충족 해야 하는 한 가지 중요 한 요구 사항이 있습니다. 보기 마스터 페이지에는 헤더에 대 한 일반 `<head>` 태그가 아닌 `<head runat="server">` 태그가 포함 되어야 합니다. `<head>` 태그에 runat = "server" 특성이 포함 되지 않은 경우 제목이 표시 되지 않습니다. 기본 보기 마스터 페이지는 필수 `<head runat="server">` 태그를 포함 합니다.

개별 콘텐츠 보기 페이지에서 마스터 페이지 콘텐츠를 수정 하는 다른 방법은 `<asp:ContentPlaceHolder>` 태그에서 수정 하려는 영역을 래핑하는 것입니다. 예를 들어 마스터 뷰 페이지에서 렌더링 되는 제목 뿐만 아니라 meta 태그도 변경 하려고 한다고 가정 합니다. 목록 4의 마스터 뷰 페이지에는 `<head>` 태그 안에 `<asp:ContentPlaceHolder>` 태그가 있습니다.

**목록 4 – `Views\Shared\Site2.master`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample5.aspx)]

목록 4의 `<asp:ContentPlaceHolder>` 태그에는 기본 내용 (기본 제목 및 기본 메타 태그)이 포함 되어 있습니다. 개별 콘텐츠 보기 페이지에서이 `<asp:ContentPlaceHolder>` 태그를 재정의 하지 않으면 기본 콘텐츠가 표시 됩니다.

목록 5의 콘텐츠 뷰 페이지는 사용자 지정 제목 및 사용자 지정 메타 태그를 표시 하기 위해 `<asp:ContentPlaceHolder>` 태그를 재정의 합니다.

**목록 5 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-vb/samples/sample6.aspx)]

### <a name="summary"></a>요약

이 자습서에서는 마스터 페이지 보기 및 콘텐츠 페이지 보기에 대 한 기본 소개를 제공 했습니다. 새 보기 마스터 페이지를 만들고 이러한 페이지를 기반으로 보기 콘텐츠 페이지를 만드는 방법을 알아보았습니다. 또한 특정 콘텐츠 보기 페이지에서 보기 마스터 페이지의 내용을 수정 하는 방법도 살펴보았습니다.

> [!div class="step-by-step"]
> [이전](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
> [다음](passing-data-to-view-master-pages-vb.md)
