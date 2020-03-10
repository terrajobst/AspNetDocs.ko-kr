---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData 사용 및 ViewModel 클래스 구현 | Microsoft Docs
author: microsoft
description: 6 단계에서는 다양 한 양식 편집 시나리오에 대 한 지원을 사용 하도록 설정 하는 방법을 보여 주고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법에 대해 설명 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435533"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData 사용 및 ViewModel 클래스 구현

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 6 단계입니다.
> 
> 6 단계에서는 다양 한 양식 편집 시나리오에 대 한 지원을 사용 하도록 설정 하는 방법을 보여 주고 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법, 즉 ViewData 및 ViewModel에 대해 설명 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>Nerddinner Step 6: ViewData 및 ViewModel

몇 가지 폼 게시 시나리오를 다루고, CRUD (만들기, 업데이트 및 삭제) 지원을 구현 하는 방법에 대해 설명 했습니다. 이제 microsoft는이에 대 한 자세한 내용을 제공 하 고 풍부한 양식 편집 시나리오에 대 한 지원을 제공 합니다. 이 작업을 수행 하는 동안 컨트롤러에서 뷰로 데이터를 전달 하는 데 사용할 수 있는 두 가지 방법, 즉 ViewData 및 ViewModel에 대해 설명 합니다.

### <a name="passing-data-from-controllers-to-view-templates"></a>컨트롤러에서 뷰로 데이터 전달-템플릿

MVC 패턴의 정의 특성 중 하나는 엄격한 "문제의 분리"는 응용 프로그램의 여러 구성 요소 간에 강제 적용 하는 데 도움이 됩니다. 모델, 컨트롤러 및 뷰는 각각 잘 정의 된 역할과 책임을 가지 며 잘 정의 된 방식으로 서로 통신 합니다. 이렇게 하면 테스트 용이성과 코드 재사용을 높일 수 있습니다.

컨트롤러 클래스는 클라이언트에 게 다시 HTML 응답을 렌더링 하기로 결정 하는 경우 응답을 렌더링 하는 데 필요한 모든 데이터를 뷰 템플릿에 명시적으로 전달 해야 합니다. 뷰 템플릿은 데이터 검색 또는 응용 프로그램 논리를 수행 하면 안 되며, 대신 컨트롤러에 의해 전달 되는 모델/데이터의 중심으로 렌더링 코드를 포함 하도록 제한 해야 합니다.

이제, 이제는 인덱스 (), Edit (), Create () 및 Delete ()의 경우에는 인덱스 ()의 경우에는 단일 Dinner 개체와 Index ()의 대/소문자를 구분 하 여 인덱스 ()의 경우에는 단순 하 고 간편 하 게 모델 데이터를 볼 수 있습니다. 응용 프로그램에 더 많은 UI 기능을 추가할 때 이러한 데이터를 포함 하 여 보기 템플릿 내에서 HTML 응답을 렌더링 해야 하는 경우가 많습니다. 예를 들어 편집 및 만든 뷰 내에서 "Country" 필드를 dropdownlist의 HTML textbox로 변경 하는 것이 좋습니다. 보기 템플릿에서 국가 이름 드롭다운 목록을 하드 코딩 하는 대신, 동적으로 채우는 지원 되는 국가 목록에서 생성할 수 있습니다. Microsoft는 컨트롤러에서 보기 템플릿에 Dinner 개체 *와* 지원 되는 국가 목록을 모두 전달 하는 방법이 필요 합니다.

이를 수행할 수 있는 두 가지 방법을 살펴보겠습니다.

### <a name="using-the-viewdata-dictionary"></a>ViewData 사전 사용

컨트롤러 기본 클래스는 컨트롤러에서 뷰로 추가 데이터 항목을 전달 하는 데 사용할 수 있는 "ViewData" 사전 속성을 노출 합니다.

예를 들어 편집 보기 내에서 "국가" 텍스트 상자를 dropdownlist에 대 한 HTML textbox로 변경 하려는 시나리오를 지원 하기 위해 Edit () 작업 메서드를 업데이트 하 여 m으로 사용할 수 있는 SelectList 개체를 전달할 수 있습니다. odel의 국가입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

위의 SelectList의 생성자는 현재 선택 된 값 뿐만 아니라 드롭다운 목록을 채울 군 목록을 사용 합니다.

그런 다음 이전에 사용한 Html. TextBox () 도우미 메서드 대신 Html. DropDownList () 도우미 메서드를 사용 하도록 편집 .aspx 뷰 템플릿을 업데이트할 수 있습니다.

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

위의 Html. DropDownList () 도우미 메서드는 두 개의 매개 변수를 사용 합니다. 첫 번째는 출력할 HTML 폼 요소의 이름입니다. 두 번째는 ViewData 사전을 통해 전달 된 "SelectList" 모델입니다. C# "As" 키워드를 사용 하 여 사전 내에서 형식을 selectlist로 캐스팅 합니다.

이제 응용 프로그램을 실행 하 고 브라우저 내에서 */Dinners/Edit/1* URL에 액세스할 때 편집 UI가 텍스트 상자 대신 국가의 dropdownlist을 표시 하도록 업데이트 되었음을 알 수 있습니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

또한 오류가 발생 하는 경우에는 HTTP-POST 편집 메서드에서 편집 뷰 템플릿을 렌더링 하므로,이 메서드를 업데이트 하 여 뷰 템플릿이 오류 시나리오에서 렌더링 될 때 SelectList를 ViewData에 추가 하도록 할 수 있습니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

그리고 이제 microsoft의 DinnersController 편집 시나리오에서 DropDownList을 지원 합니다.

### <a name="using-a-viewmodel-pattern"></a>ViewModel 패턴 사용

ViewData 사전 접근 방식은 매우 빠르고 간편 하 게 구현할 수 있는 이점을 제공 합니다. 그러나 오타는 컴파일 시간에 catch 되지 않는 오류가 발생할 수 있기 때문에 일부 개발자는 문자열 기반 사전을 사용 하지 않아도 됩니다. 또한 형식화 되지 않은 ViewData 사전은 "as" 연산자를 사용 하거나 보기 템플릿과 같이 C# 강력한 형식의 언어를 사용할 때 캐스팅 해야 합니다.

사용할 수 있는 대체 방법은 종종 "ViewModel" 패턴 이라고 합니다. 이 패턴을 사용 하는 경우 특정 뷰 시나리오에 최적화 된 강력한 형식의 클래스를 만들고, 뷰 템플릿에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다. 그러면 컨트롤러 클래스는 이러한 뷰 최적화 클래스를 채우고 사용할 뷰 템플릿으로 전달할 수 있습니다. 이렇게 하면 보기 템플릿 내에서 형식 안전성, 컴파일 시간 검사 및 편집기 intellisense를 사용할 수 있습니다.

예를 들어 dinner form 편집 시나리오를 사용 하도록 설정 하기 위해 아래와 같이 두 가지 강력한 형식의 속성을 노출 하는 "' d Innerformviewmodel" 클래스를 만들 수 있습니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

그러면 Edit () 작업 메서드를 업데이트 하 여 리포지토리에서 검색 하는 Dinner object를 사용 하 여이를 만들 수 있습니다. 그런 다음 뷰 템플릿에 전달 합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

그런 다음, 다음과 같이 편집 .aspx 페이지의 맨 위에 있는 "inherits" 특성을 변경 하 여 "Dinner" 개체 대신 "' ' ' '

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

이 작업을 수행 하면 보기 템플릿 내에서 "모델" 속성의 intellisense가 전달 하 고 있는 다음의 개체 모델을 반영 하도록 업데이트 됩니다.

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

그런 다음 보기 코드를 업데이트 하 여 작업을 수행할 수 있습니다. 만드는 입력 요소의 이름을 변경 하지 않는 방법에 대 한 자세한 내용은 아래를 참조 하세요. 양식 요소는 여전히 "Title", "Country"로 이름이 지정 되지만, 다음은 d c t i t e m e n t i t e s t e m. t e r 클래스를 사용 하 여 값을 검색 하도록 HTML 도우미

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

또한 렌더링 오류가 발생할 경우에는 Edit post 메서드를 업데이트 하 여 d Innerformviewmodel 클래스를 사용 합니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

또한 Create () 작업 메서드를 업데이트 하 여 동일한 단일 d *Innerformviewmodel* 클래스를 다시 사용 하도록 할 수 있습니다. 다음은 HTTP GET 구현입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

다음은 HTTP POST 만들기 메서드의 구현입니다.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

이제 편집 및 만들기 화면이 모두 국가를 선택할 수 있는 드롭다운 목록을 지원 합니다.

### <a name="custom-shaped-viewmodel-classes"></a>사용자 지정 모양 ViewModel 클래스

위의 시나리오에서, microsoft의 DinnerFormViewModel 클래스는 지원 되는 SelectList 모델 속성과 함께 Dinner model 개체를 속성으로 직접 노출 합니다. 이 접근 방식은 보기 템플릿 내에서 만들려는 HTML UI가 도메인 모델 개체와 비교적 긴밀 하 게 일치 하는 시나리오에서 제대로 작동 합니다.

이 경우에 해당 하지 않는 시나리오의 경우 사용할 수 있는 한 가지 옵션은 개체 모델이 뷰에서 사용 하기에 최적화 되어 있고 기본 도메인 모델 개체와 완전히 다를 수 있는 사용자 지정 모양 ViewModel 클래스를 만드는 것입니다. 예를 들어 여러 모델 개체에서 수집 된 여러 속성 이름 및/또는 집계 속성을 잠재적으로 노출할 수 있습니다.

사용자 지정 모양 ViewModel 클래스를 사용 하 여 컨트롤러에서 뷰로 데이터를 전달 하 고 컨트롤러의 동작 메서드에 다시 게시 된 양식 데이터를 처리할 수 있습니다. 이후 시나리오에서는 동작 메서드가 폼 게시 데이터를 사용 하 여 ViewModel 개체를 업데이트 한 다음 ViewModel 인스턴스를 사용 하 여 실제 도메인 모델 개체를 매핑하거나 검색 하는 경우가 있을 수 있습니다.

사용자 지정 모양 ViewModel 클래스는 상당한 유연성을 제공할 수 있으며, 보기 템플릿 내에서 렌더링 코드를 찾을 때 또는 작업 메서드 내에서 폼 게시 코드를 찾을 때마다 너무 복잡 해지기 시작 합니다. 이는 종종 도메인 모델이 생성 하는 UI와 일치 하지 않으며 중간 사용자 지정 모양 ViewModel 클래스가 도움이 될 수 있다는 것입니다.

### <a name="next-step"></a>다음 단계

이제 부분 및 마스터 페이지를 사용 하 여 응용 프로그램에서 UI를 다시 사용 하 고 공유 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [다음](re-use-ui-using-master-pages-and-partials.md)
