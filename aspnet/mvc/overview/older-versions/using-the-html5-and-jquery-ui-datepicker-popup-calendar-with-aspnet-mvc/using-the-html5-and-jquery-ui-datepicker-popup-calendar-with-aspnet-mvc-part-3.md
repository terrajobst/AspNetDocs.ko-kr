---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-3 부 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup을 사용 하 여 작업 하는 방법에 대 한 기본 사항을 학습 합니다. ASP.NET m ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433217"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-3 부

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup 일정을 사용 하는 방법에 대 한 기본 사항을 설명 합니다.

## <a name="working-with-complex-types"></a>복합 형식 작업

이 섹션에서는 address 클래스를 만들고 템플릿을 만들어 표시 하는 방법을 알아봅니다.

*모델* 폴더에서 *Person.cs* 이라는 새 클래스 파일을 만듭니다. 여기에는 두 가지 형식, 즉 `Person` 클래스와 `Address` 클래스가 있습니다. `Person` 클래스에는 `Address`으로 형식화 된 속성이 포함 됩니다. `Address` 형식은 복합 형식입니다. 즉, `int`, `string`또는 `double`와 같은 기본 제공 형식 중 하나가 아닙니다. 대신 여러 속성을 포함 합니다. 새 클래스에 대 한 코드는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

`Movie` 컨트롤러에서 다음 `PersonDetail` 작업을 추가 하 여 person 인스턴스를 표시 합니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

그런 다음 `Movie` 컨트롤러에 다음 코드를 추가 하 여 일부 샘플 데이터로 `Person` 모델을 채웁니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

*Views\Movies\PersonDetail.cshtml* 파일을 열고 `PersonDetail` 뷰에 대해 다음 태그를 추가 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Ctrl + F5 키를 눌러 응용 프로그램을 실행 하 고 *영화/PersonDetail*로 이동 합니다.

이 스크린샷에서 볼 수 있듯이 `PersonDetail` 보기에는 `Address` 복합 형식이 포함 되어 있지 않습니다. (주소가 표시 되지 않습니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

`Address` 모델 데이터는 복합 유형 이므로 표시 되지 않습니다. 주소 정보를 표시 하려면 *Views\Movies\PersonDetail.cshtml* 파일을 다시 열고 다음 태그를 추가 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

현재 보기 `PersonDetail`의 전체 태그는 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

응용 프로그램을 다시 실행 하 고 `PersonDetail` 보기를 표시 합니다. 이제 주소 정보가 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>복합 형식에 대 한 템플릿 만들기

이 섹션에서는 `Address` 복합 유형을 렌더링 하는 데 사용 되는 템플릿을 만듭니다. `Address` 형식에 대 한 템플릿을 만들 때 ASP.NET MVC는 자동으로이를 사용 하 여 응용 프로그램의 모든 위치에서 주소 모델의 형식을 지정할 수 있습니다. 이렇게 하면 응용 프로그램의 한 곳에서 `Address` 형식의 렌더링을 제어 하는 방법을 제공 합니다.

*Views\Shared\DisplayTemplates* 폴더에서 **Address**라는 강력한 형식의 부분 뷰를 만듭니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

**추가**를 클릭 한 다음 새 *Views\Shared\DisplayTemplates\Address.cshtml* 파일을 엽니다. 새 뷰에는 다음과 같은 생성 된 태그가 포함 되어 있습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

응용 프로그램을 실행 하 고 `PersonDetail` 보기를 표시 합니다. 이번에는 방금 만든 `Address` 템플릿이 `Address` 복합 형식을 표시 하는 데 사용 되므로 다음과 같이 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>요약: 모델 표시 형식 및 템플릿을 지정 하는 방법

다음 방법을 사용 하 여 모델 속성에 대 한 서식 또는 템플릿을 지정할 수 있습니다.

- 모델의 속성에 `DisplayFormat` 특성을 적용 합니다. 예를 들어 다음 코드는 시간 없이 날짜를 표시 하도록 합니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- 모델의 속성에 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성을 적용 하 고 데이터 형식을 지정 합니다. 예를 들어 다음 코드는 시간 없이 날짜를 표시 하도록 합니다.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    응용 프로그램의 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에 *date. cshtml* 템플릿이 포함 되어 있으면 해당 템플릿이 `DateTime` 속성을 렌더링 하는 데 사용 됩니다. 그렇지 않으면 기본 제공 ASP.NET 템플릿 시스템은 속성을 날짜로 표시 합니다.
- 서식 지정 하려는 데이터 형식과 이름이 일치 하는 *Views\Shared\DisplayTemplates* 폴더 또는 *Views\Movies\DisplayTemplates* 폴더에 표시 템플릿 만들기 예를 들어 모델에 특성을 추가 하 고 뷰에 태그를 추가 하지 않고 모델에서 `DateTime` 속성을 렌더링 하는 데 *Views\Shared\DisplayTemplates\DateTime.cshtml* 를 사용 했습니다.
- 모델에서 [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) 특성을 사용 하 여 모델 속성을 표시 하는 템플릿을 지정 합니다.
- 보기에서 호출 [에 대 한 표시 템플릿 이름을 Html. displayfor](https://msdn.microsoft.com/library/ee407420.aspx) 명시적으로 추가 합니다.

사용 하는 방법은 응용 프로그램에서 수행 해야 하는 작업에 따라 다릅니다. 이러한 접근 방식을 혼합 하 여 필요한 형식 지정을 정확 하 게 수행 하는 것은 일반적이 지 않습니다.

다음 섹션에서는 기어를 전환 하 고 데이터를 표시 하는 방법을 사용자 지정 하 여 이동 하는 방법을 사용자 지정 합니다. 날짜를 지정 하는 정면 방법을 제공 하기 위해 응용 프로그램의 편집 뷰에 jQuery datepicker를 연결 합니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)
