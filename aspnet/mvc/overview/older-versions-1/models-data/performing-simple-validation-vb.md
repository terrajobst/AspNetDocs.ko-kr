---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: 간단한 유효성 검사 수행 (VB) | Microsoft Docs
author: StephenWalther
description: ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 모델 상태와 유효성 검사 HTML 도우미를 소개 합니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 46925f22b7dfc23f2bb89b8d2fff0cbd8ae49062
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436667"
---
# <a name="performing-simple-validation-vb"></a>간단한 유효성 검사 수행(VB)

[Stephen Walther](https://github.com/StephenWalther)

> ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 모델 상태 및 유효성 검사 HTML 도우미를 소개 합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법을 설명 하는 것입니다. 예를 들어 사용자가 필수 필드에 대 한 값을 포함 하지 않는 양식을 전송 하지 못하도록 하는 방법을 알아봅니다. 모델 상태와 유효성 검사 HTML 도우미를 사용 하는 방법에 대해 알아봅니다.

## <a name="understanding-model-state"></a>모델 상태 이해

모델 상태 (모델 상태 사전)를 사용 하 여 유효성 검사 오류를 나타냅니다. 예를 들어 목록 1의 Create () 동작은 product 클래스를 데이터베이스에 추가 하기 전에 Product 클래스의 속성에 대 한 유효성을 검사 합니다.

컨트롤러에 유효성 검사 또는 데이터베이스 논리를 추가 하는 것을 권장 하지 않습니다. 컨트롤러는 응용 프로그램 흐름 제어와 관련 된 논리를 포함 해야 합니다. 작업을 단순하게 유지 하기 위한 바로 가기를 작성 하 고 있습니다.

**목록 1-Controller\entstomom.xml**

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

목록 1에서 Product 클래스의 Name, Description 및 UnitsInStock 속성에 대 한 유효성을 검사 합니다. 이러한 속성 중 하나라도 유효성 검사 테스트에 실패 하면 모델 상태 사전 (컨트롤러 클래스의 ModelState 속성으로 표시 됨)에 오류가 추가 됩니다.

모델 상태에 오류가 있으면 ModelState. IsValid 속성은 false를 반환 합니다. 이 경우 새 제품을 만들기 위한 HTML 양식이 다시 표시 됩니다. 그렇지 않으면 유효성 검사 오류가 없는 경우 새 제품이 데이터베이스에 추가 됩니다.

## <a name="using-the-validation-helpers"></a>유효성 검사 도우미 사용

ASP.NET MVC 프레임 워크에는 Html. ValidationMessage () 도우미와 ValidationSummary () 도우미 라는 두 가지 유효성 검사 도우미가 포함 되어 있습니다. 뷰에 이러한 두 도우미를 사용 하 여 유효성 검사 오류 메시지를 표시 합니다.

Html ValidationMessage () 및 ValidationSummary () 도우미는 ASP.NET MVC 스 캐 폴딩에 의해 자동으로 생성 되는 만들기 및 편집 뷰에서 사용 됩니다. Create view를 생성 하려면 다음 단계를 수행 합니다.

1. 제품 컨트롤러에서 만들기 () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **보기 추가** 를 선택 합니다 (그림 1 참조).
2. **보기 추가** 대화 상자에서 **강력한 형식의 뷰 만들기** 확인란을 선택 합니다 (그림 2 참조).
3. **데이터 클래스 보기** 드롭다운 목록에서 Product 클래스를 선택 합니다.
4. **콘텐츠 보기** 드롭다운 목록에서 만들기를 선택 합니다.
5. **추가** 단추를 클릭합니다.

뷰를 추가 하기 전에 응용 프로그램을 빌드해야 합니다. 그렇지 않으면 클래스 목록이 **데이터 클래스 보기** 드롭다운 목록에 표시 되지 않습니다.

[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)

**그림 01**: 보기 추가 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image2.png))

[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)

**그림 02**: 강력한 형식의 뷰 만들기 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image4.png))

이러한 단계를 완료 한 후 목록 2에서 만들기 보기를 가져옵니다.

**목록 2-Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

목록 2에서는 html 양식 바로 위에 ValidationSummary () 도우미가 호출 됩니다. 이 도우미는 유효성 검사 오류 메시지 목록을 표시 하는 데 사용 됩니다. ValidationSummary () 도우미는 오류를 글머리 기호 목록으로 렌더링 합니다.

Html 양식 필드 옆에 Html. ValidationMessage () 도우미가 호출 됩니다. 이 도우미는 폼 필드 바로 옆에 오류 메시지를 표시 하는 데 사용 됩니다. 목록 2의 경우 오류가 발생 하면 Html. ValidationMessage () 도우미에 별표가 표시 됩니다.

그림 3의 페이지는 양식이 누락 된 필드와 잘못 된 값으로 제출 될 때 유효성 검사 도우미에서 렌더링 하는 오류 메시지를 보여 줍니다.

[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)

**그림 03**: 문제가 있는 생성 된 Create view ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image6.png))

유효성 검사 오류가 있는 경우에도 HTML 입력 필드의 모양이 수정 됩니다. Html. textbox () 도우미는 Html. TextBox () 도우미에 의해 렌더링 된 속성과 관련 된 유효성 검사 오류가 있을 때 *class = "입력-오류"* 특성을 렌더링 합니다.

유효성 검사 오류의 모양을 제어 하는 데 사용 되는 세 가지 css 스타일 시트 클래스가 있습니다.

- 입력-유효성 검사-오류-Html. TextBox () 도우미에 의해 렌더링 된 &lt;입력&gt; 태그에 적용 됩니다.
- 필드-유효성 검사-오류-Html. ValidationMessage () 도우미에 의해 렌더링 된 &lt;범위&gt; 태그에 적용 됩니다.
- 유효성 검사-요약-오류-ValidationSummary () 도우미에 의해 렌더링 된 &lt;ul&gt; 태그에 적용 됩니다.

이러한 css 스타일 시트 클래스를 수정할 수 있으므로 Content 폴더에 있는 사이트 .css 파일을 수정 하 여 유효성 검사 오류의 모양을 수정할 수 있습니다.

> [!NOTE] 
> 
> HtmlHelper 클래스는 유효성 검사 관련 CSS 클래스의 이름을 검색 하기 위한 읽기 전용 정적 속성을 포함 합니다. 이러한 정적 속성의 이름은 ValidationInputCssClassName, ValidationFieldCssClassName 및 ValidationSummaryCssClassName입니다.

## <a name="prebinding-validation-and-postbinding-validation"></a>Prebinding 유효성 검사 및 사후 바인딩 유효성 검사

제품을 만들기 위한 HTML 양식을 제출 하 고 price 필드에 대해 잘못 된 값을 입력 하 고 UnitsInStock 필드에 값을 입력 하지 않은 경우 그림 4에 표시 된 유효성 검사 메시지를 받게 됩니다. 이러한 유효성 검사 오류 메시지는 어디에서 제공 되나요?

[새 프로젝트 대화 상자 ![](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)

**그림 04**: 사전 바인딩 유효성 검사 오류 ([전체 크기 이미지를 보려면 클릭](performing-simple-validation-vb/_static/image8.png))

실제로는 HTML 양식 필드가 클래스에 바인딩되고 폼 필드가 클래스에 바인딩된 후에 생성 된 유효성 검사 오류 메시지의 두 가지 유형이 있습니다. 즉, prebinding 유효성 검사 오류와 postbinding 유효성 검사 오류가 있습니다.

목록 1에서 제품 컨트롤러에 의해 노출 되는 만들기 () 작업은 Product 클래스의 인스턴스를 허용 합니다. Create 메서드의 시그니처는 다음과 같습니다.

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

만들기 양식의 HTML 양식 필드 값은 모델 바인더 라는 항목에 따라 제품 Tocreate 클래스에 바인딩됩니다. 기본 모델 바인더는 양식 필드를 폼 속성에 바인딩할 수 없는 경우 자동으로 모델 상태에 오류 메시지를 추가 합니다.

기본 모델 바인더는 "apple" 문자열을 Product 클래스의 Price 속성에 바인딩할 수 없습니다. Decimal 속성에는 문자열을 할당할 수 없습니다. 따라서 모델 바인더는 모델 상태에 오류를 추가 합니다.

또한 기본 모델 바인더는 nothing 값을 허용 하지 않는 속성에 Nothing 값을 할당할 수 없습니다. 특히 모델 바인더는 UnitsInStock 속성에 Nothing 값을 할당할 수 없습니다. 다시 한 번 모델 바인더는이를 제공 하 고 모델 상태에 오류 메시지를 추가 합니다.

이러한 prebinding 오류 메시지의 모양을 사용자 지정 하려면 이러한 메시지에 대 한 리소스 문자열을 만들어야 합니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET MVC 프레임 워크에서 유효성 검사의 기본 메커니즘을 설명 하는 것 이었습니다. 모델 상태와 유효성 검사 HTML 도우미를 사용 하는 방법을 배웠습니다. 또한 prebinding과 postbinding 유효성 검사의 차이점에 대해 설명 했습니다. 다른 자습서에서는 컨트롤러 및 모델 클래스에서 유효성 검사 코드를 이동 하는 다양 한 전략에 대해 설명 합니다.

> [!div class="step-by-step"]
> [이전](displaying-a-table-of-database-data-vb.md)
> [다음](validating-with-the-idataerrorinfo-interface-vb.md)
