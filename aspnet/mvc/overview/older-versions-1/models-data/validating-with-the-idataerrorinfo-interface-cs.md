---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: IDataErrorInfo 인터페이스를 사용 하 여C#유효성 검사 () | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436349"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a>IDataErrorInfo 인터페이스를 사용한 유효성 검사(C#)

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther는 모델 클래스에서 IDataErrorInfo 인터페이스를 구현 하 여 사용자 지정 유효성 검사 오류 메시지를 표시 하는 방법을 보여 줍니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는 것입니다. 사용자가 필요한 양식 필드에 값을 제공 하지 않고 HTML 양식을 전송 하지 못하도록 하는 방법에 대해 알아봅니다. 이 자습서에서는 IErrorDataInfo 인터페이스를 사용 하 여 유효성 검사를 수행 하는 방법에 대해 알아봅니다.

## <a name="assumptions"></a>가정

이 자습서에서는 MoviesDB 데이터베이스와 영화 데이터베이스 테이블을 사용 합니다. 이 테이블에는 다음 열이 있습니다.

<a id="0.5_table01"></a>

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| Id | Int | False |
| 제목 | Nvarchar(100) | False |
| 감독 | Nvarchar(100) | False |
| DateReleased | DateTime | False |

이 자습서에서는 Microsoft Entity Framework를 사용 하 여 내 데이터베이스 모델 클래스를 생성 합니다. Entity Framework에서 생성 된 Movie 클래스는 그림 1에 표시 됩니다.

[Movie 엔터티 ![](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)

**그림 01**: 동영상 엔터티 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))

> [!NOTE] 
> 
> Entity Framework를 사용 하 여 데이터베이스 모델 클래스를 생성 하는 방법에 대 한 자세한 내용은 Entity Framework를 사용 하 여 모델 클래스 만들기의 자습서를 참조 하세요.

## <a name="the-controller-class"></a>Controller 클래스

Home 컨트롤러를 사용 하 여 영화를 나열 하 고 새 영화를 만듭니다. 이 클래스의 코드는 목록 1에 포함 되어 있습니다.

**목록 1-Controllers\ homecontroller.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

목록 1의 홈 컨트롤러 클래스는 두 개의 Create () 작업을 포함 합니다. 첫 번째 작업은 새 동영상을 만들기 위한 HTML 양식을 표시 합니다. 두 번째 Create () 작업은 데이터베이스에 새 동영상을 실제로 삽입 하는 작업을 수행 합니다. 두 번째 Create () 작업은 첫 번째 Create () 작업에 의해 표시 되는 양식이 서버에 전송 될 때 호출 됩니다.

두 번째 Create () 작업에는 다음 코드 줄이 포함 되어 있습니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

유효성 검사 오류가 있는 경우 IsValid 속성은 false를 반환 합니다. 이 경우 동영상을 만들기 위한 HTML 양식이 포함 된 Create 뷰가 다시 표시 됩니다.

## <a name="creating-a-partial-class"></a>Partial 클래스 만들기

Movie 클래스는 Entity Framework에서 생성 됩니다. 솔루션 탐색기 창에서 MoviesDBModel 파일을 확장 하 고 코드 편집기에서 MoviesDBModel.Designer.cs 파일을 여는 경우 Movie 클래스에 대 한 코드를 볼 수 있습니다 (그림 2 참조).

[Movie 엔터티에 대 한 코드 ![](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)

**그림 02**: 동영상 엔터티에 대 한 코드 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))

Movie 클래스는 partial 클래스입니다. 즉, 동일한 이름으로 다른 partial 클래스를 추가 하 여 Movie 클래스의 기능을 확장할 수 있습니다. 새 partial 클래스에 유효성 검사 논리를 추가 합니다.

목록 2의 클래스를 모델 폴더에 추가 합니다.

**목록 2-Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

목록 2의 클래스에는 *partial* 한정자가 포함 되어 있습니다. 이 클래스에 추가 하는 메서드나 속성은 Entity Framework에서 생성 된 Movie 클래스의 일부가 됩니다.

## <a name="adding-onchanging-and-onchanged-partial-methods"></a>OnChanging 및 Onchanging 부분 메서드 추가

Entity Framework에서 엔터티 클래스를 생성 하는 경우 Entity Framework는 부분 메서드를 클래스에 자동으로 추가 합니다. Entity Framework는 클래스의 각 속성에 해당 하는 OnChanging 및 Onchanging 부분 메서드를 생성 합니다.

Movie 클래스의 경우 Entity Framework은 다음 메서드를 만듭니다.

- OnIdChanging
- OnIdChanged
- OnTitleChanging
- OnTitleChanged
- OnDirectorChanging
- OnDirectorChanged
- OnDateReleasedChanging
- OnDateReleasedChanged

OnChanging 메서드는 해당 속성이 변경 되기 직전에 호출 됩니다. OnChanged 메서드는 속성이 변경 된 직후에 호출 됩니다.

이러한 부분 메서드를 활용 하 여 영화 클래스에 유효성 검사 논리를 추가할 수 있습니다. 목록 3의 업데이트 동영상 클래스는 제목 및 감독 속성에 비어 있지 않은 값이 할당 되었는지 확인 합니다.

> [!NOTE] 
> 
> 부분 메서드 (partial method)는 구현 하지 않아도 되는 클래스에 정의 된 메서드입니다. 부분 메서드를 구현 하지 않는 경우 컴파일러는 메서드 시그니처와 해당 메서드에 대 한 모든 호출을 제거 하 여 부분 메서드와 관련 된 런타임 비용이 발생 하지 않도록 합니다. Visual Studio Code 편집기에서 *partial 키워드 뒤에 공백을* 입력 하 여 부분 메서드를 추가 하 여 구현할 부분 목록을 볼 수 있습니다.

**목록 3-Models\Movie.cs**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

예를 들어 Title 속성에 빈 문자열을 할당 하려고 하면 \_오류 라는 사전에 오류 메시지가 할당 됩니다.

이 시점에서 Title 속성에 빈 문자열을 할당 하면 실제로는 발생 하지 않으며 전용 \_오류 필드에 오류가 추가 됩니다. ASP.NET MVC 프레임 워크에 이러한 유효성 검사 오류를 노출 하려면 IDataErrorInfo 인터페이스를 구현 해야 합니다.

## <a name="implementing-the-idataerrorinfo-interface"></a>IDataErrorInfo 인터페이스 구현

IDataErrorInfo 인터페이스는 첫 번째 버전 이후 .NET framework의 일부입니다. 이 인터페이스는 매우 간단한 인터페이스입니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

클래스가 IDataErrorInfo 인터페이스를 구현 하는 경우 ASP.NET MVC 프레임 워크는 클래스의 인스턴스를 만들 때이 인터페이스를 사용 합니다. 예를 들어 Home controller Create () 작업은 Movie 클래스의 인스턴스를 허용 합니다.

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

ASP.NET MVC 프레임 워크는 모델 바인더 (DefaultModelBinder)를 사용 하 여 Create () 작업에 전달 되는 동영상의 인스턴스를 만듭니다. 모델 바인더는 HTML 양식 필드를 Movie 개체의 인스턴스에 바인딩하여 Movie 개체의 인스턴스를 만드는 역할을 담당 합니다.

DefaultModelBinder는 클래스가 IDataErrorInfo 인터페이스를 구현 하는지 여부를 검색 합니다. 클래스가이 인터페이스를 구현 하는 경우 모델 바인더는 클래스의 각 속성에 대해 IDataErrorInfo를 호출 합니다. 인덱서가 오류 메시지를 반환 하는 경우 모델 바인더는이 오류 메시지를 자동으로 모델 상태에 추가 합니다.

DefaultModelBinder도 IDataErrorInfo 속성을 확인 합니다. 이 속성은 클래스와 연결 된 속성이 아닌 특정 유효성 검사 오류를 나타내기 위한 것입니다. 예를 들어 Movie 클래스의 여러 속성 값에 따라 달라 지는 유효성 검사 규칙을 적용 하는 것이 좋습니다. 이 경우 오류 속성에서 유효성 검사 오류를 반환 합니다.

목록 4의 업데이트 된 동영상 클래스는 IDataErrorInfo 인터페이스를 구현 합니다.

**목록 4-Models\Movie.cs (구현 IDataErrorInfo)**

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

목록 4에서 인덱서 속성은 \_errors 컬렉션에서 인덱서에 전달 된 속성 이름에 해당 하는 키가 포함 되어 있는지 확인 합니다. 속성과 연결 된 유효성 검사 오류가 없으면 빈 문자열이 반환 됩니다.

수정 된 Movie 클래스를 사용 하는 방식으로 홈 컨트롤러를 수정할 필요가 없습니다. 그림 3에 표시 된 페이지는 제목 또는 감독 양식 필드에 값을 입력 하지 않은 경우 발생 하는 상황을 보여 줍니다.

[작업 메서드 자동 생성 ![](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)

**그림 03**: 누락 된 값이 있는 폼 ([전체 크기 이미지를 보려면 클릭](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))

DateReleased 값의 유효성이 자동으로 검사 됩니다. DateReleased 속성은 NULL 값을 허용 하지 않으므로 DefaultModelBinder는 값이 없는 경우이 속성에 대 한 유효성 검사 오류를 자동으로 생성 합니다. DateReleased 속성에 대 한 오류 메시지를 수정 하려면 사용자 지정 모델 바인더를 만들어야 합니다.

## <a name="summary"></a>요약

이 자습서에서는 IDataErrorInfo 인터페이스를 사용 하 여 유효성 검사 오류 메시지를 생성 하는 방법을 배웠습니다. 먼저 Entity Framework에서 생성 된 부분 동영상 클래스의 기능을 확장 하는 부분 동영상 클래스를 만들었습니다. 다음으로, 영화 클래스 OnTitleChanging () 및 OnDirectorChanging () 부분 메서드에 유효성 검사 논리를 추가 했습니다. 마지막으로 ASP.NET MVC 프레임 워크에 이러한 유효성 검사 메시지를 노출 하기 위해 IDataErrorInfo 인터페이스를 구현 했습니다.

> [!div class="step-by-step"]
> [이전](performing-simple-validation-cs.md)
> [다음](validating-with-a-service-layer-cs.md)
