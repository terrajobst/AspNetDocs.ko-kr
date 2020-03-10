---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
title: 모델에 유효성 검사 추가 (C#) | Microsoft Docs
author: Rick-Anderson
description: 컨트롤러 만들기
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 9af927e2-1c3b-43d9-917d-1df75be3c482
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 19d86dc0df931a9d135e46209559892b77626cf6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498827"
---
# <a name="adding-validation-to-the-model-c"></a>모델에 유효성 검사 추가(C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> 이 항목과 함께 사용할 수 있는 C# 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다. [버전을 C# 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic 선호 하는 경우이 자습서의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.

이 섹션에서는 `Movie` 모델에 유효성 검사 논리를 추가 하 고, 사용자가 응용 프로그램을 사용 하 여 동영상을 만들거나 편집 하려고 할 때마다 유효성 검사 규칙이 적용 되도록 합니다.

## <a name="keeping-things-dry"></a>작업 건조 유지

ASP.NET MVC의 핵심 디자인 개념 중 하나는 마른 ("반복 금지")입니다. ASP.NET MVC는 기능이 나 동작을 한 번만 지정한 다음 응용 프로그램의 모든 위치에 반영 되도록 권장 합니다. 이렇게 하면 작성 해야 하는 코드의 양이 줄어들고 작성 하는 코드를 훨씬 쉽게 유지 관리할 수 있습니다.

ASP.NET MVC 및 Entity Framework Code First에서 제공 하는 유효성 검사 지원은 작동 중인 마른 원칙의 좋은 예입니다. 모델 클래스의 한 위치에서 유효성 검사 규칙을 선언적으로 지정할 수 있으며, 이러한 규칙은 응용 프로그램의 모든 위치에서 적용 됩니다.

영화 응용 프로그램에서이 유효성 검사 지원을 활용할 수 있는 방법을 살펴보겠습니다.

## <a name="adding-validation-rules-to-the-movie-model"></a>무비 모델에 유효성 검사 규칙 추가

먼저 `Movie` 클래스에 유효성 검사 논리를 추가 합니다.

*Movie.cs* 파일을 엽니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스를 참조 하는 파일의 맨 위에 `using` 문을 추가 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

네임 스페이스는 .NET Framework의 일부입니다. 클래스 또는 속성에 선언적으로 적용할 수 있는 유효성 검사 특성의 기본 제공 집합을 제공 합니다.

이제 `Movie` 클래스를 업데이트 하 여 기본 제공 [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)및 [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) 유효성 검사 특성을 활용 합니다. 특성을 적용할 위치의 예로 다음 코드를 사용 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs)]

이 유효성 검사 특성은 적용되는 모델 속성에 시행하려는 동작을 지정합니다. `Required` 특성은 속성에 값이 있어야 함을 나타냅니다. 이 샘플에서 동영상은 유효 하려면 `Title`, `ReleaseDate`, `Genre`및 `Price` 속성에 대 한 값이 있어야 합니다. `Range` 특성은 지정한 범위 내로 값을 제한합니다. `StringLength` 특성을 사용하면 문자열 속성의 최대 길이와, 그리고 필요에 따라 최소 길이를 설정할 수 있습니다.

Code First를 사용 하면 응용 프로그램에서 데이터베이스의 변경 내용을 저장 하기 전에 모델 클래스에서 지정 하는 유효성 검사 규칙이 적용 됩니다. 예를 들어, 몇 가지 필수 `Movie` 속성 값이 누락 되 고 가격이 0 (유효한 범위를 벗어남) 이기 때문에 아래 코드는 `SaveChanges` 메서드가 호출 될 때 예외를 throw 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample3.cs)]

.NET Framework에 의해 자동으로 적용 되는 유효성 검사 규칙이 있으면 응용 프로그램을 더욱 강력 하 게 만들 수 있습니다. 또한 무언가의 유효성 검사를 잊거나, 실수로 데이터베이스에 불량 데이터가 들어가지 않도록 할 수 있습니다.

다음은 업데이트 된 *Movie.cs* 파일에 대 한 전체 코드 목록입니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC의 유효성 검사 오류 UI

응용 프로그램을 다시 실행 하 고/또는 *비디오* URL로 이동 합니다.

**동영상 만들기** 링크를 클릭 하 여 새 동영상을 추가 합니다. 양식에서 잘못 된 값을 입력 한 다음 **만들기** 단추를 클릭 합니다.

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

양식에서 자동으로 배경색을 사용 하 여 잘못 된 데이터를 포함 하 고 각 텍스트 상자 옆에 적절 한 유효성 검사 오류 메시지를 내보낸 텍스트 상자를 강조 표시 하는 방법을 확인 합니다. 오류 메시지는 `Movie` 클래스에 주석을 달 때 지정한 오류 문자열과 일치 합니다. 오류는 클라이언트 쪽 (JavaScript 사용) 및 서버 쪽 (사용자가 JavaScript를 사용 하지 않도록 설정한 경우) 모두에 적용 됩니다.

실제 혜택은이 유효성 검사 UI를 사용 하도록 설정 하기 위해 `MoviesController` 클래스 또는 *Create. cshtml* 뷰에서 코드 한 줄을 변경할 필요가 없다는 것입니다. 이 자습서의 앞부분에서 만든 컨트롤러 및 뷰는 `Movie` 모델 클래스에서 특성을 사용 하 여 지정한 유효성 검사 규칙을 자동으로 선택 합니다.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Create View 및 Create Action 메서드에서 유효성 검사를 수행 하는 방법

컨트롤러나 보기의 코드를 전혀 수정하지 않고도 어떻게 유효성 검사 UI가 생성되는지 궁금할 것입니다. 다음 목록에서는 `MovieController` 클래스의 `Create` 메서드를 보여 줍니다. 이 자습서의 앞부분에서 만든 방법에서 변경 되지 않았습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

첫 번째 작업 메서드는 초기 만들기 폼을 표시 합니다. 두 번째는 폼 게시를 처리 합니다. 두 번째 `Create` 메서드 `ModelState.IsValid`를 호출 하 여 영화에 유효성 검사 오류가 있는지 여부를 확인 합니다. 이 메서드를 호출하면 개체에 적용된 모든 유효성 검사 특성이 평가됩니다. 개체에 유효성 검사 오류가 있는 경우 `Create` 메서드는 폼을 보다 합니다. 오류가 없으면 메서드가 데이터베이스에 새 영화를 저장합니다.

다음은이 자습서의 앞부분에서 스 캐 폴드 하는 *Create. cshtml* 보기 템플릿입니다. 이 항목은 위 두 작업 메서드에서 최초 양식을 표시하고 오류 시 다시 표시하기 위해 사용됩니다.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

코드에서 `Html.EditorFor` 도우미를 사용 하 여 각 `Movie` 속성의 `<input>` 요소를 출력 하는 방법을 확인 합니다. 이 도우미 옆은 `Html.ValidationMessageFor` 도우미 메서드에 대 한 호출입니다. 이러한 두 도우미 메서드는 컨트롤러에서 뷰에 전달 되는 모델 개체 (이 경우에는 `Movie` 개체)를 사용 합니다. 모델에 지정 된 유효성 검사 특성을 자동으로 검색 하 고 오류 메시지를 적절 하 게 표시 합니다.

이 방법에 대 한 유용한 정보는 컨트롤러와 Create view 템플릿에서 적용 되는 실제 유효성 검사 규칙이 나 표시 되는 특정 오류 메시지에 대 한 정보를 인식 하지 못하는 것입니다. 유효성 검사 규칙 및 오류 문자열은 `Movie` 클래스에서만 지정됩니다.

유효성 검사 논리를 나중에 변경 하려면 정확 하 게 한 곳에서 수행할 수 있습니다. 모든 유효성 검사 논리가 한 곳에서 정의되어 모든 곳에서 사용되므로 애플리케이션의 서로 다른 부분이 규칙 적용 방법에 부합하는지 우려하지 않아도 됩니다. 이렇게 하면 코드가 매우 깔끔해지고 유지 관리 및 확장이 간편합니다. 또한 반복 금지 원칙에 완전히 부합하게 됩니다.

## <a name="adding-formatting-to-the-movie-model"></a>동영상 모델에 서식 추가

*Movie.cs* 파일을 엽니다. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스는 기본 제공 유효성 검사 특성 집합 외에도 서식 특성을 제공 합니다. [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성과 [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 열거형 값을 릴리스 날짜 및 가격 필드에 적용 합니다. 다음 코드에서는 적절 한 [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성이 있는 `ReleaseDate` 및 `Price` 속성을 보여 줍니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs)]

또는 [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) 값을 명시적으로 설정할 수 있습니다. 다음 코드에서는 날짜 형식 문자열 (즉, "d")이 포함 된 릴리스 날짜 속성을 보여 줍니다. 이를 사용 하 여 릴리스 날짜의 일부로 시간을 원하지 않도록 지정 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample8.cs)]

다음 코드는 `Price` 속성의 형식을 통화로 지정 합니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

전체 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

응용 프로그램을 실행 하 고 `Movies` 컨트롤러로 이동 합니다.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

이 시리즈의 다음 부분에서는 애플리케이션을 검토하고 자동 생성된 `Details` 및 `Delete` 메서드를 몇 가지 개선합니다.

> [!div class="step-by-step"]
> [이전](adding-a-new-field.md)
> [다음](improving-the-details-and-delete-methods.md)
