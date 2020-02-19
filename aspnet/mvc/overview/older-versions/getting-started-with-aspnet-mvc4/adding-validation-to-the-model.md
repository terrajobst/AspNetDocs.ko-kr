---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: 모델에 유효성 검사 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455960"
---
# <a name="adding-validation-to-the-model"></a>모델에 유효성 검사 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.

이 섹션에서는 `Movie` 모델에 유효성 검사 논리를 추가 하 고, 사용자가 응용 프로그램을 사용 하 여 동영상을 만들거나 편집 하려고 할 때마다 유효성 검사 규칙이 적용 되도록 합니다.

## <a name="keeping-things-dry"></a>작업 건조 유지

ASP.NET MVC의 핵심 디자인 개념 중 하나는 마른 (&quot;반복 금지&quot;)입니다. ASP.NET MVC는 기능이 나 동작을 한 번만 지정한 다음 응용 프로그램의 모든 위치에 반영 되도록 권장 합니다. 이렇게 하면 작성 해야 하는 코드의 양이 줄어들고 오류가 발생 하기 쉬우며 더 쉽게 유지 관리할 수 있는 코드를 만들 수 있습니다.

ASP.NET MVC 및 Entity Framework Code First에서 제공 하는 유효성 검사 지원은 작동 중인 마른 원칙의 좋은 예입니다. 모델 클래스의 한 위치에서 유효성 검사 규칙을 선언적으로 지정할 수 있으며, 규칙은 응용 프로그램의 모든 위치에서 적용 됩니다.

영화 응용 프로그램에서이 유효성 검사 지원을 활용할 수 있는 방법을 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>무비 모델에 유효성 검사 규칙 추가

먼저 `Movie` 클래스에 유효성 검사 논리를 추가 합니다.

*Movie.cs* 파일을 엽니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스를 참조 하는 파일의 맨 위에 `using` 문을 추가 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

네임 스페이스에는 `System.Web`포함 되어 있지 않습니다. DataAnnotations은 모든 클래스나 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 집합을 제공 합니다.

이제 `Movie` 클래스를 업데이트 하 여 기본 제공 [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)및 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성을 활용 합니다. 특성을 적용할 위치의 예로 다음 코드를 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

응용 프로그램을 실행 하면 다음 런타임 오류가 다시 표시 됩니다.

***' MovieDBContext ' 컨텍스트를 지 원하는 모델이 데이터베이스를 만든 이후 변경 되었습니다. Code First 마이그레이션를 사용 하 여 데이터베이스를 업데이트 하는 것이 좋습니다 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***

마이그레이션을 사용 하 여 스키마를 업데이트 합니다. 솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 열고 다음 명령을 입력 합니다.

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

이 명령이 완료 되 면 Visual Studio는 지정 된 이름 (*AddDataAnnotationsMig*)을 사용 하 여 새 `DbMigration` 파생 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 스키마 제약 조건을 업데이트 하는 코드를 볼 수 있습니다. `Title` 및 `Genre` 필드는 더 이상 null을 허용 하지 않습니다. 즉, 값을 입력 해야 하 고 `Rating` 필드의 최대 길이는 5입니다.

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 특성은 속성에 값이 있어야 함을 나타냅니다. 이 샘플에서 동영상은 유효 하려면 `Title`, `ReleaseDate`, `Genre`및 `Price` 속성에 대 한 값이 있어야 합니다. `Range` 특성은 지정한 범위 내로 값을 제한합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 그리고 필요에 따라 최소 길이를 설정할 수 있습니다. 내장 형식 (예: `decimal, int, float, DateTime`)은 기본적으로 필요 하며 `Required` 특성이 필요 하지 않습니다.

Code First를 사용 하면 응용 프로그램에서 데이터베이스의 변경 내용을 저장 하기 전에 모델 클래스에서 지정 하는 유효성 검사 규칙이 적용 됩니다. 예를 들어, 몇 가지 필수 `Movie` 속성 값이 누락 되 고 가격이 0 (유효한 범위를 벗어남) 이기 때문에 아래 코드는 `SaveChanges` 메서드가 호출 될 때 예외를 throw 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

.NET Framework에 의해 자동으로 적용 되는 유효성 검사 규칙이 있으면 응용 프로그램을 더욱 강력 하 게 만들 수 있습니다. 또한 무언가의 유효성 검사를 잊거나, 실수로 데이터베이스에 불량 데이터가 들어가지 않도록 할 수 있습니다.

다음은 업데이트 된 *Movie.cs* 파일에 대 한 전체 코드 목록입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC의 유효성 검사 오류 UI

응용 프로그램을 다시 실행 하 고/또는 *비디오* URL로 이동 합니다.

새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다. 양식에서 잘못 된 값을 입력 한 다음 **만들기** 단추를 클릭 합니다.

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> 소수점에 쉼표 (&quot;,&quot;)를 사용 하는 영어가 아닌 로캘에 대해 jQuery 유효성 검사를 지원 하려면 `Globalize.parseFloat`를 사용 하는 데 사용 되는 사용자 지정 *문화권/세계화* 파일 ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) 및 JavaScript *를 포함 해야 합니다.* 다음 코드는 &quot;fr-fr&quot; 문화권을 사용 하기 위해 Views\Movies\Edit.cshtml 파일을 수정 하는 방법을 보여 줍니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

양식에서 자동으로 빨간색 테두리 색을 사용 하 여 잘못 된 데이터를 포함 하 고 각 텍스트 상자 옆에 적절 한 유효성 검사 오류 메시지를 내보낸 텍스트 상자를 강조 표시 하는 방법을 확인 합니다. 오류는 클라이언트 쪽(JavaScript 및 jQuery 사용 시) 및 서버 쪽(사용자가 JavaScript를 사용하지 않도록 설정한 경우) 모두에서 발생합니다.

실제 혜택은이 유효성 검사 UI를 사용 하도록 설정 하기 위해 `MoviesController` 클래스 또는 *Create. cshtml* 뷰에서 코드 한 줄을 변경할 필요가 없다는 것입니다. 이 자습서에서 이전에 만든 컨트롤러 및 보기는 `Movie` 모델 클래스의 속성에 유효성 검사 특성을 사용하여 지정한 유효성 검사 규칙을 자동으로 가져옵니다.

`Title` 및 `Genre`속성에 대해 알고 있을 수 있습니다. ( **만들기** 단추를 눌러) 양식을 전송 하거나 입력 필드에 텍스트를 입력 하 고 제거할 때까지 필수 특성이 적용 되지 않습니다. 처음에는 비어 있는 필드 (예: Create view의 필드) 및 필수 특성만 있고 다른 유효성 검사 특성이 없는 필드의 경우 다음을 수행 하 여 유효성 검사를 트리거할 수 있습니다.

1. 필드에 탭을 삽입 합니다.
2. 텍스트를 입력 합니다.
3. 필드 밖을 탭합니다.
4. 필드에 다시 탭 합니다.
5. 텍스트를 제거 합니다.
6. 필드 밖을 탭합니다.

위의 시퀀스는 제출 단추를 클릭 하지 않고 필요한 유효성 검사를 트리거합니다. 필드를 입력 하지 않고 제출 단추를 누르기만 하면 클라이언트 쪽 유효성 검사가 트리거됩니다. 양식 데이터는 클라이언트 쪽 유효성 검사 오류가 없을 때까지 서버에 전송되지 않습니다. HTTP Post 메서드에 중단점을 배치 하거나 [fiddler 도구나](http://fiddler2.com/fiddler2/) IE 9 [F12 개발자 도구](https://msdn.microsoft.com/ie/aa740478)를 사용 하 여이를 테스트할 수 있습니다.

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View 및 Create Action 메서드에서 유효성 검사를 수행 하는 방법

컨트롤러나 보기의 코드를 전혀 수정하지 않고도 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록에서는 `MovieController` 클래스의 `Create` 메서드를 보여 줍니다. 이 자습서의 앞부분에서 만든 방법에서 변경 되지 않았습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

첫 번째(HTTP GET) `Create` 작업 메서드는 최초 Create 양식을 표시합니다. 두 번째(`[HttpPost]`) 버전은 양식 게시를 처리합니다. 두 번째 `Create` 메서드(`HttpPost` 버전)는 `ModelState.IsValid`를 호출하여 영화의 유효성 검사 오류 여부를 확인합니다. 이 메서드를 호출하면 개체에 적용된 모든 유효성 검사 특성이 평가됩니다. 개체에 유효성 검사 오류가 있으면 `Create` 메서드는 양식을 다시 표시합니다. 오류가 없으면 메서드가 데이터베이스에 새 영화를 저장합니다. 을 사용 하는 동영상 예제에서는 **클라이언트 쪽에서 유효성 검사 오류가 발견 되 면 양식이 서버에 게시 되지 않고 두 번째** `Create`**메서드가 호출 되지**않습니다. 브라우저에서 JavaScript를 사용 하지 않도록 설정 하는 경우 클라이언트 유효성 검사를 사용 하지 않도록 설정 하 고 HTTP POST `Create` 메서드에서 `ModelState.IsValid`를 호출 하 여 영화에 유효성 검사 오류가 있는지 여부를 확인 합니다.

`HttpPost Create` 메서드에서 중단점을 설정하고 메서드가 호출되지 않게 확인할 수 있으며, 유효성 검사 오류가 탐지되면 클라이언트 쪽 유효성 검사가 양식 데이터를 제출하지 않습니다. 브라우저에서 JavaScript를 사용하지 않고 오류가 있는 상태로 양식을 제출하면 중단점에 이르게 됩니다. JavaScript 없이도 여전히 완전한 유효성 검사가 가능합니다. 다음 그림에서는 Internet Explorer에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

다음 이미지는 FireFox 브라우저에서 JavaScript를 사용하지 않도록 설정하는 방법을 보여줍니다.

![](adding-validation-to-the-model/_static/image5.png)

다음 이미지에서는 Chrome 브라우저에서 JavaScript를 사용 하지 않도록 설정 하는 방법을 보여 줍니다.

![](adding-validation-to-the-model/_static/image6.png)

다음은이 자습서의 앞부분에서 스 캐 폴드 하는 *Create. cshtml* 보기 템플릿입니다. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

코드에서 `Html.EditorFor` 도우미를 사용 하 여 각 `Movie` 속성의 `<input>` 요소를 출력 하는 방법을 확인 합니다. 이 도우미 옆은 `Html.ValidationMessageFor` 도우미 메서드에 대 한 호출입니다. 이러한 두 도우미 메서드는 컨트롤러에서 뷰에 전달 되는 모델 개체 (이 경우에는 `Movie` 개체)를 사용 합니다. 모델에 지정 된 유효성 검사 특성을 자동으로 검색 하 고 오류 메시지를 적절 하 게 표시 합니다.

이 방법에 대 한 유용한 정보는 컨트롤러와 Create view 템플릿에서 적용 되는 실제 유효성 검사 규칙이 나 표시 되는 특정 오류 메시지에 대 한 정보를 인식 하지 못하는 것입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다. 이러한 동일한 유효성 검사 규칙은 편집 보기 및 모델을 편집 하는 사용자가 만들 수 있는 다른 모든 보기 템플릿에 자동으로 적용 됩니다.

유효성 검사 논리를 나중에 변경 하려면 모델에 유효성 검사 특성을 추가 하 여 정확히 한 곳에서 (이 예제에서는 `movie` 클래스) 유효성 검사 논리를 변경 합니다. 모든 유효성 검사 논리가 한 곳에서 정의되어 모든 곳에서 사용되므로 애플리케이션의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 또한 반복 금지 원칙에 완전히 부합하게 됩니다.

## <a name="adding-formatting-to-the-movie-model"></a>동영상 모델에 서식 추가

*Movie.cs* 파일을 열고 `Movie` 클래스를 검토합니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에도 서식 특성을 제공 합니다. 릴리스 날짜 및 가격 필드에 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 열거형 값을 이미 적용 했습니다. 다음 코드에서는 적절 한 [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성이 있는 `ReleaseDate` 및 `Price` 속성을 보여 줍니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성은 유효성 검사 특성이 아닙니다. 이러한 특성은 뷰 엔진에 HTML 렌더링 방법을 지시 하는 데 사용 됩니다. 위의 예제에서 `DataType.Date` 특성은 동영상 날짜를 시간 없이 날짜만 표시 합니다. 예를 들어 다음 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성은 데이터 형식에 대 한 유효성을 검사 하지 않습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

위에 나열 된 특성은 데이터의 서식을 지정 하는 뷰 엔진에 대 한 힌트를 제공 합니다 (및 URL에 대 한&gt; &lt;와 같은 특성을 제공 하 고 전자 메일의 경우 href =&quot;mailto:EmailAddress&quot;&gt;를 &lt;합니다. [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) 특성을 사용 하 여 데이터 형식의 유효성을 검사할 수 있습니다.

`DataType` 특성을 사용 하는 다른 방법으로 [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) 값을 명시적으로 설정할 수 있습니다. 다음 코드에서는 날짜 형식 문자열 (&quot;d&quot;)이 포함 된 릴리스 날짜 속성을 보여 줍니다. 이를 사용 하 여 릴리스 날짜의 일부로 시간을 원하지 않도록 지정 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

전체 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

응용 프로그램을 실행 하 고 `Movies` 컨트롤러로 이동 합니다. 릴리스 날짜와 가격은 깔끔하게 서식 지정 됩니다. 아래 이미지는 &quot;fr-fr&quot;를 사용 하는 릴리스 날짜 및 가격을 문화권으로 보여 줍니다.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

아래 이미지는 기본 문화권 (미국 영어)과 동일한 데이터를 표시 합니다.

![](adding-validation-to-the-model/_static/image8.png)

이 시리즈의 다음 부분에서는 애플리케이션을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field-to-the-movie-model-and-table.md)
> [다음](examining-the-details-and-delete-methods.md)
