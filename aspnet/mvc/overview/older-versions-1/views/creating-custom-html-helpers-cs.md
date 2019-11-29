---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 사용자 지정 HTML 도우미 만들기C#() | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하 여 ...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594501"
---
# <a name="creating-custom-html-helpers-c"></a>사용자 지정 HTML 도우미 만들기(C#)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> 이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하면 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력 크기를 줄일 수 있습니다.

이 자습서의 목표는 MVC 뷰 내에서 사용할 수 있는 사용자 지정 HTML 도우미를 만들 수 있는 방법을 보여 주는 것입니다. HTML 도우미를 활용 하면 표준 HTML 페이지를 만들기 위해 수행 해야 하는 HTML 태그의 번거로운 입력 크기를 줄일 수 있습니다.

이 자습서의 첫 번째 부분에서는 ASP.NET MVC 프레임 워크에 포함 된 기존 HTML 도우미 중 일부를 설명 합니다. 다음으로, 사용자 지정 HTML 도우미를 만드는 두 가지 방법에 대해 설명 합니다. 정적 메서드를 만들고 확장 메서드를 만들어 사용자 지정 HTML 도우미를 만드는 방법을 설명 합니다.

## <a name="understanding-html-helpers"></a>HTML 도우미 이해

HTML 도우미는 문자열을 반환 하는 메서드 일 뿐입니다. 문자열은 원하는 모든 형식의 콘텐츠를 나타낼 수 있습니다. 예를 들어 html 도우미를 사용 하 여 HTML `<input>` 및 `<img>` 태그와 같은 표준 HTML 태그를 렌더링할 수 있습니다. HTML 도우미를 사용 하 여 탭 스트립 또는 데이터베이스 데이터의 HTML 테이블과 같은 보다 복잡 한 콘텐츠를 렌더링할 수도 있습니다.

ASP.NET MVC 프레임 워크에는 다음과 같은 표준 HTML 도우미 집합이 포함 되어 있습니다 (완전 한 목록이 아님).

- Html.actionlink ()
- Html.beginform ()
- Html. CheckBox ()
- Html DropDownList ()
- .Html. EndForm ()
- Html. Hidden ()
- Html. ListBox ()
- Html. Password ()
- Html. RadioButton ()
- Html. TextArea ()
- Html. TextBox ()

예를 들어 목록 1의 양식을 살펴보겠습니다. 이 폼은 두 가지 표준 HTML 도우미의 도움으로 렌더링 됩니다 (그림 1 참조). 이 폼에서는 `Html.BeginForm()` 및 `Html.TextBox()` 도우미 메서드를 사용 하 여 간단한 HTML 폼을 렌더링 합니다.

[HTML 도우미를 사용 하 여 렌더링 된 ![페이지](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**그림 01**: HTML 도우미를 사용 하 여 렌더링 된 페이지 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image3.png))

**목록 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Html.beginform () 도우미 메서드는 여는 태그와 닫는 HTML `<form>` 태그를 만드는 데 사용 됩니다. `Html.BeginForm()` 메서드는 using 문 내에서 호출 됩니다. Using 문은 `<form>` 태그가 using 블록의 끝에서 닫히도록 합니다.

Using 블록을 만드는 대신 Html. EndForm () 도우미 메서드를 호출 하 여 `<form>` 태그를 닫을 수 있습니다. 가장 직관적으로 보이는 여는 태그와 닫는 `<form>` 태그를 만드는 방법을 사용 합니다.

`Html.TextBox()` 도우미 메서드는 목록 1에서 HTML `<input>` 태그를 렌더링 하는 데 사용 됩니다. 브라우저에서 소스 보기를 선택 하면 목록 2에 HTML 소스가 표시 됩니다. 원본에는 표준 HTML 태그가 포함 되어 있습니다.

> [!IMPORTANT]
> `Html.TextBox()`HTML 도우미는 `<% %>` 태그 대신 `<%= %>` 태그로 렌더링 됩니다. 등호를 포함 하지 않으면 브라우저에 아무것도 렌더링 되지 않습니다.

ASP.NET MVC 프레임 워크에는 작은 도우미 집합이 포함 되어 있습니다. 사용자 지정 HTML 도우미를 사용 하 여 MVC 프레임 워크를 확장 해야 하는 경우가 많습니다. 이 자습서의 나머지 부분에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법에 대해 알아봅니다.

**목록 2 – `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>정적 메서드를 사용 하 여 HTML 도우미 만들기

새 HTML 도우미를 만드는 가장 쉬운 방법은 문자열을 반환 하는 정적 메서드를 만드는 것입니다. 예를 들어 HTML `<label>` 태그를 렌더링 하는 새 HTML 도우미를 만들도록 결정 한다고 가정 합니다. 목록 2에서 클래스를 사용 하 여 `<label>`를 렌더링할 수 있습니다.

**목록 2 – `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

목록 2의 클래스에 대 한 특별 한 사항은 없습니다. `Label()` 메서드는 단순히 문자열을 반환 합니다.

목록 3의 수정 된 인덱스 뷰는 `LabelHelper`을 사용 하 여 HTML `<label>` 태그를 렌더링 합니다. 뷰에는 `Application1.Helpers` 네임 스페이스를 가져오는 `<%@ imports %>` 지시문이 포함 되어 있습니다.

**목록 2 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>확장 메서드를 사용 하 여 HTML 도우미 만들기

ASP.NET MVC 프레임 워크에 포함 된 표준 HTML 도우미와 같은 방식으로 작동 하는 HTML 도우미를 만들려는 경우에는 확장 메서드를 만들어야 합니다. 확장 메서드를 사용 하 여 기존 클래스에 새 메서드를 추가할 수 있습니다. HTML 도우미 메서드를 만들 때 뷰의 Html 속성이 나타내는 HtmlHelper 클래스에 새 메서드를 추가 합니다.

목록 3의 클래스는 `Label()`이라는 `HtmlHelper` 클래스에 확장 메서드를 추가 합니다. 이 클래스에 대해 몇 가지 주의 해야 할 사항이 있습니다. 먼저 클래스가 정적 클래스 인지 확인 합니다. 정적 클래스를 사용 하 여 확장 메서드를 정의 해야 합니다.

둘째, `Label()` 메서드의 첫 번째 매개 변수가 `this`키워드 앞에와 야 합니다. 확장 메서드의 첫 번째 매개 변수는 확장 메서드가 확장 하는 클래스를 나타냅니다.

**목록 3 – `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

확장 메서드를 만들고 응용 프로그램을 성공적으로 빌드한 후에는 Visual Studio Intellisense에 클래스의 다른 모든 메서드와 같은 확장 메서드가 표시 됩니다 (그림 2 참조). 유일한 차이점은 확장 메서드가 해당 기호 옆에 특수 기호 (아래쪽 화살표 아이콘)와 함께 표시 된다는 것입니다.

[Html. Label () 확장 메서드를 사용 하 여 ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**그림 02**: Html. Label () 확장 메서드 사용 ([전체 크기 이미지를 보려면 클릭](creating-custom-html-helpers-cs/_static/image6.png))

목록 4의 수정 된 인덱스 뷰는 Html. Label () 확장 메서드를 사용 하 여 모든 `<label>` 태그를 렌더링 합니다.

**목록 4 – `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>요약

이 자습서에서는 사용자 지정 HTML 도우미를 만드는 두 가지 방법을 배웠습니다. 먼저 문자열을 반환 하는 정적 메서드를 만들어 사용자 지정 `Label()` HTML 도우미를 만드는 방법을 알아보았습니다. 다음으로 `HtmlHelper` 클래스에서 확장 메서드를 만들어 사용자 지정 `Label()` HTML 도우미 메서드를 만드는 방법을 알아보았습니다.

이 자습서에서는 매우 간단한 HTML 도우미 메서드를 작성 하는 데 초점을 두었습니다. HTML 도우미는 원하는 대로 복잡할 수 있습니다. 트리 뷰, 메뉴 또는 데이터베이스 데이터의 테이블과 같은 다양 한 콘텐츠를 렌더링 하는 HTML 도우미를 작성할 수 있습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-views-overview-cs.md)
> [다음](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
