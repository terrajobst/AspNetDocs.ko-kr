---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: '반복 #3-양식 유효성 검사 추가C#() | Microsoft Docs'
author: microsoft
description: 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 emai의 유효성을 검사 합니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: af2e86e820f60f0a3d8e3db8f78eba67ef63579a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437987"
---
# <a name="iteration-3--add-form-validation-c"></a>반복 #3-양식 유효성 검사 추가C#()

by [Microsoft](https://github.com/microsoft)

[코드 다운로드](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (C#)

이 자습서 시리즈에서는 전체 연락처 관리 응용 프로그램을 처음부터 끝까지 빌드 합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 (이름, 전화 번호 및 전자 메일 주소)를 사용자 목록으로 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 각 반복을 통해 응용 프로그램을 점진적으로 개선 합니다. 이 여러 반복 방법의 목표는 각 변경의 이유를 이해할 수 있게 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업에 대 한 지원을 추가 합니다. 만들기, 읽기, 업데이트 및 삭제 (CRUD)

- 반복 #2-응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

- 반복 #4-응용 프로그램이 느슨하게 결합 되도록 합니다. 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

- 반복 #6-테스트 기반 개발을 사용 합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="this-iteration"></a>이 반복

Contact Manager 응용 프로그램의이 두 번째 반복에서는 기본 양식 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드에 대 한 값을 입력 하지 않고 연락처를 제출 하지 못하도록 합니다. 전화 번호 및 전자 메일 주소의 유효성도 검사 합니다 (그림 1 참조).

[새 프로젝트 대화 상자 ![](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**그림 01**: 유효성 검사가 있는 폼 ([전체 크기 이미지를 보려면 클릭](iteration-3-add-form-validation-cs/_static/image2.png))

이 반복에서는 컨트롤러 작업에 직접 유효성 검사 논리를 추가 합니다. 일반적으로 ASP.NET MVC 응용 프로그램에 유효성 검사를 추가 하는 것은 권장 되는 방법이 아닙니다. 응용 프로그램의 유효성 검사 논리를 별도의 [서비스 계층](http://martinfowler.com/eaaCatalog/serviceLayer.html)에 저장 하는 것이 더 나은 방법입니다. 다음 반복에서는 응용 프로그램을 보다 쉽게 관리할 수 있도록 Contact Manager 응용 프로그램을 리팩터링 합니다.

이 반복에서 작업을 단순하게 유지 하기 위해 모든 유효성 검사 코드를 직접 작성 합니다. 유효성 검사 코드를 직접 작성 하는 대신 유효성 검사 프레임 워크를 활용할 수 있습니다. 예를 들어 Microsoft Enterprise Library Validation Application Block (VAB)을 사용 하 여 ASP.NET MVC 응용 프로그램에 대 한 유효성 검사 논리를 구현할 수 있습니다. 유효성 검사 응용 프로그램 블록에 대해 자세히 알아보려면 다음을 참조 하세요.

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>만들기 뷰에 유효성 검사 추가

만들기 보기에 유효성 검사 논리를 추가 하 여를 시작 하겠습니다. 다행히 Visual Studio를 사용 하 여 Create view를 생성 했으므로 Create view에는 유효성 검사 메시지를 표시 하는 데 필요한 모든 사용자 인터페이스 논리가 이미 포함 되어 있습니다. 만들기 보기는 목록 1에 포함 되어 있습니다.

**목록 1-\Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

HTML 양식 바로 위에 표시 되는 ValidationSummary () 도우미 메서드에 대 한 호출을 확인 합니다. 유효성 검사 오류 메시지가 있는 경우이 메서드는 글머리 기호 목록에 유효성 검사 메시지를 표시 합니다.

또한 각 폼 필드 옆에 표시 되는 Html. ValidationMessage ()를 호출 합니다. ValidationMessage () 도우미는 개별 유효성 검사 오류 메시지를 표시 합니다. 목록 1의 경우 유효성 검사 오류가 있을 때 별표가 표시 됩니다.

마지막으로, 도우미에서 표시 하는 속성과 관련 된 유효성 검사 오류가 있을 때 Html TextBox () 도우미는 Css 스타일 시트 클래스를 자동으로 렌더링 합니다. Html. TextBox () 도우미는 **입력-유효성 검사 오류**라는 클래스를 렌더링 합니다.

새 ASP.NET MVC 응용 프로그램을 만들 때 Content 폴더에 Site. .css 이라는 스타일 시트가 자동으로 만들어집니다. 이 스타일 시트에는 유효성 검사 오류 메시지의 모양과 관련 된 CSS 클래스에 대 한 다음 정의가 포함 되어 있습니다.

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

필드 유효성 검사 오류 클래스는 Html. ValidationMessage () 도우미에 의해 렌더링 되는 출력의 스타일을 사용 하는 데 사용 됩니다. 입력 유효성 검사 오류 클래스는 Html. TextBox () 도우미에 의해 렌더링 되는 textbox (input)의 스타일을 사용 하는 데 사용 됩니다. 유효성 검사 요약-errors 클래스는 ValidationSummary () 도우미에 의해 렌더링 된 순서가 지정 되지 않은 목록의 스타일을 지정 하는 데 사용 됩니다.

> [!NOTE] 
> 
> 이 섹션에서 설명 하는 스타일 시트 클래스를 수정 하 여 유효성 검사 오류 메시지의 모양을 사용자 지정할 수 있습니다.

## <a name="adding-validation-logic-to-the-create-action"></a>만들기 작업에 유효성 검사 논리 추가

이제 메시지를 생성 하는 논리를 작성 하지 않았으므로 Create view는 유효성 검사 오류 메시지를 표시 하지 않습니다. 유효성 검사 오류 메시지를 표시 하려면 모델 상태에 오류 메시지를 추가 해야 합니다.

> [!NOTE] 
> 
> UpdateModel () 메서드는 폼 필드의 값을 속성에 할당 하는 동안 오류가 발생 하는 경우 자동으로 모델 상태에 오류 메시지를 추가 합니다. 예를 들어 날짜/시간 값을 허용 하는 생년월일 속성에 "apple" 문자열을 할당 하려고 하면 UpdateModel () 메서드는 ModelState에 오류를 추가 합니다.

목록 2의 수정 된 Create () 메서드는 새 연락처가 데이터베이스에 삽입 되기 전에 Contact 클래스 속성의 유효성을 검사 하는 새 섹션을 포함 합니다.

**목록 2-Controllers\ContactController.cs (유효성 검사를 사용 하 여 만들기)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

Validate 섹션은 다음과 같이 4 개의 고유한 유효성 검사 규칙을 적용 합니다.

- FirstName 속성의 길이는 0 보다 커야 하며 공백으로만 구성 될 수 없습니다.
- LastName 속성의 길이는 0 보다 커야 하며 공백으로만 구성 될 수 없습니다.
- Phone 속성의 값이 0 보다 큰 경우 Phone 속성은 정규식과 일치 해야 합니다.
- 전자 메일 속성의 값이 0 보다 큰 경우 email 속성은 정규식과 일치 해야 합니다.

유효성 검사 규칙 위반이 발생 하면 AddModelError () 메서드를 사용 하 여 ModelState에 오류 메시지가 추가 됩니다. ModelState에 메시지를 추가 하는 경우 속성 이름 및 유효성 검사 오류 메시지의 텍스트를 제공 합니다. 이 오류 메시지는 ValidationSummary () 및 Html. ValidationMessage () 도우미 메서드에 의해 뷰에 표시 됩니다.

유효성 검사 규칙이 실행 된 후 ModelState의 IsValid 속성이 확인 됩니다. IsValid 속성은 ModelState에 유효성 검사 오류 메시지가 추가 된 경우 false를 반환 합니다. 유효성 검사에 실패 하면 오류 메시지와 함께 만들기 양식이 다시 표시 됩니다.

> [!NOTE] 
> 
> http://regexlib.com에서 정규식 리포지토리의 전화 번호와 전자 메일 주소를 확인 하는 정규식을 얻었습니다. [ ](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>편집 작업에 유효성 검사 논리 추가

Edit () 작업은 연락처를 업데이트 합니다. Edit () 작업은 Create () 동작과 정확히 동일한 유효성 검사를 수행 해야 합니다. 동일한 유효성 검사 코드를 복제 하는 대신 Create () 및 Edit () 작업이 모두 동일한 유효성 검사 메서드를 호출 하도록 Contact controller를 리팩터링 해야 합니다.

수정 된 연락처 컨트롤러 클래스는 목록 3에 포함 되어 있습니다. 이 클래스에는 Create () 및 Edit () 작업 내에서 호출 되는 새 ValidateContact () 메서드가 있습니다.

**Listing 3 - Controllers\ContactController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 기본 폼 유효성 검사를 추가 했습니다. 유효성 검사 논리를 통해 사용자는 FirstName 및 LastName 속성에 대 한 값을 제공 하지 않고 새 연락처를 제출 하거나 기존 연락처를 편집할 수 없습니다. 또한 사용자는 유효한 전화 번호와 전자 메일 주소를 제공 해야 합니다.

이 반복에서는 가장 쉬운 방법으로 연락처 관리자 응용 프로그램에 유효성 검사 논리를 추가 했습니다. 그러나 유효성 검사 논리를 컨트롤러 논리로 혼합 하면 장기적으로 문제가 발생 합니다. 응용 프로그램은 시간에 따라 유지 관리 하 고 수정 하기가 더 어려워집니다.

다음 반복에서는 컨트롤러의 유효성 검사 논리 및 데이터베이스 액세스 논리를 리팩터링 합니다. 여러 소프트웨어 디자인 원칙을 활용 하 여 더 느슨하게 결합 되 고 더 쉽게 관리할 수 있는 응용 프로그램을 만들 수 있습니다.

> [!div class="step-by-step"]
> [이전](iteration-2-make-the-application-look-nice-cs.md)
> [다음](iteration-4-make-the-application-loosely-coupled-cs.md)
