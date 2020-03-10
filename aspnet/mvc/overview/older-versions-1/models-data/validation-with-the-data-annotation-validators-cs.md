---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: 데이터 주석 유효성 검사기를 사용한 유효성C#검사 () | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하세요. 다른 유형의 유효성 검사기를 사용 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: e154384c08adf0c14920afff85e983a67b41707c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435983"
---
# <a name="validation-with-the-data-annotation-validators-c"></a>데이터 주석 유효성 검사기를 사용한 유효성 검사(C#)

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하려면 데이터 주석 모델 바인더를 활용 하세요. 다양 한 종류의 유효성 검사기 특성을 사용 하 고 Microsoft Entity Framework에서 작업 하는 방법을 알아봅니다.

이 자습서에서는 데이터 주석 유효성 검사기를 사용 하 여 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 알아봅니다. 데이터 주석 유효성 검사기를 사용 하는 경우의 장점은 필수 또는 StringLength 특성과 같은 하나 이상의 특성을 클래스 속성에 추가 하 여 유효성 검사를 수행할 수 있다는 것입니다.

데이터 주석 유효성 검사기를 사용 하려면 먼저 데이터 주석 모델 바인더를 다운로드 해야 합니다. CodePlex 웹 사이트에서 [여기](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)를 클릭 하 여 데이터 주석 모델 바인더 샘플을 다운로드할 수 있습니다.

데이터 주석 모델 바인더는 Microsoft ASP.NET MVC 프레임 워크의 공식 부분이 아니라는 것을 이해 하는 것이 중요 합니다. Microsoft ASP.NET MVC 팀에서 데이터 주석 모델 바인더를 만들었으므로 Microsoft는이 자습서에서 설명 하 고 사용 된 데이터 주석 모델 바인더에 대 한 공식적인 제품 지원을 제공 하지 않습니다.

## <a name="using-the-data-annotation-model-binder"></a>데이터 주석 모델 바인더 사용

ASP.NET MVC 응용 프로그램에서 데이터 주석 모델 바인더를 사용 하려면 먼저 System.componentmodel 어셈블리와 어셈블리에 대 한 참조를 추가 해야 합니다 .이를 위해 먼저 참조를 추가 해야 합니다. 메뉴 옵션 **프로젝트, 참조 추가를**선택 합니다. 그런 다음 **찾아보기** 탭을 클릭 하 여 데이터 주석 모델 바인더 샘플을 다운로드 하 고 압축을 푼 위치를 찾습니다 ( **그림 1**참조).

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

**그림 1**: 데이터 주석 모델 바인더에 대 한 참조 추가 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-cs/_static/image3.png))

System.componentmodel 어셈블리와 어셈블리를 둘 다 선택 하 고 확인 단추를 클릭 합니다 ( **확인** 단추를 클릭 합니다.

데이터 주석 모델 바인더를 사용 하 여 .NET Framework 서비스 팩 1에 포함 된 System.componentmodel 어셈블리를 사용할 수 없습니다. 데이터 주석 모델 바인더 샘플 다운로드에 포함 된 System.componentmodel 어셈블리의 버전을 사용 해야 합니다.

마지막으로, Global.asax 파일에 DataAnnotations 모델 바인더를 등록 해야 합니다. 응용 프로그램\_Start () 메서드가 다음과 같이 표시 되도록 Application\_Start () 이벤트 처리기에 다음 코드 줄을 추가 합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

이 코드 줄은 ataAnnotationsModelBinder를 전체 ASP.NET MVC 응용 프로그램에 대 한 기본 모델 바인더로 등록 합니다.

## <a name="using-the-data-annotation-validator-attributes"></a>데이터 주석 유효성 검사기 특성 사용

데이터 주석 모델 바인더를 사용 하는 경우 유효성 검사 특성을 사용 하 여 유효성 검사를 수행 합니다. System.componentmodel 네임 스페이스는 다음과 같은 유효성 검사기 특성을 포함 합니다.

- 범위 – 속성 값이 지정 된 값 범위에 속하는지 여부를 확인할 수 있습니다.
- RegularExpression – 속성 값이 지정 된 정규식 패턴과 일치 하는지 여부를 확인할 수 있습니다.
- 필수 – 필요에 따라 속성을 표시할 수 있습니다.
- StringLength – 문자열 속성의 최대 길이를 지정할 수 있습니다.
- 유효성 검사 – 모든 유효성 검사기 특성에 대 한 기본 클래스입니다.

> [!NOTE] 
> 
> 유효성 검사 요구가 표준 유효성 검사기에서 충족 되지 않는 경우에는 항상 기본 유효성 검사 특성에서 새 유효성 검사기 특성을 상속 하 여 사용자 지정 유효성 검사기 특성을 만들 수 있습니다.

**목록 1** 의 Product 클래스는 이러한 유효성 검사기 특성을 사용 하는 방법을 보여 줍니다. Name, Description 및 UnitPrice 속성은 필수로 표시 됩니다. 이름 속성의 문자열 길이는 10 자 미만 이어야 합니다. 마지막으로 단가 속성은 통화 금액을 나타내는 정규식 패턴과 일치 해야 합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

**목록 1**: Models\product.cs

Product 클래스는 DisplayName 특성과 같은 추가 특성을 사용 하는 방법을 보여 줍니다. DisplayName 특성을 사용 하면 오류 메시지에 속성이 표시 될 때 속성의 이름을 수정할 수 있습니다. "UnitPrice 필드가 필요 합니다." 라는 오류 메시지를 표시 하는 대신 "Price 필드가 필요 합니다." 라는 오류 메시지를 표시할 수 있습니다.

> [!NOTE] 
> 
> 유효성 검사기에 표시 되는 오류 메시지를 완전히 사용자 지정 하려면 다음과 같이 유효성 검사기의 ErrorMessage 속성에 사용자 지정 오류 메시지를 할당 하면 됩니다. `<Required(ErrorMessage:="This field needs a value!")>`

목록 **2**에서 만들기 () 컨트롤러 작업과 함께 **목록 1** 에서 Product 클래스를 사용할 수 있습니다. 이 컨트롤러 작업은 모델 상태에 오류가 있을 때 Create view를 표시 합니다.

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

**목록 2**: 제어기

마지막으로 만들기 () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **보기 추가**를 선택 하 여 **목록 3** 에서 보기를 만들 수 있습니다. Product 클래스를 사용 하 여 모델 클래스로 강력한 형식의 뷰를 만듭니다. 콘텐츠 보기 드롭다운 목록에서 **만들기** 를 선택 합니다 ( **그림 2**참조).

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

**그림 2**: Create View 추가

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

**목록 3**: Views\Product\Create.aspx

> [!NOTE] 
> 
> **보기 추가** 메뉴 옵션으로 생성 된 만들기 폼에서 Id 필드를 제거 합니다. Id 필드는 id 열에 해당 하기 때문에 사용자가이 필드에 대 한 값을 입력할 수 없도록 합니다.

제품을 만들기 위한 양식을 제출 하 고 필수 필드에 대 한 값을 입력 하지 않으면 **그림 3** 의 유효성 검사 오류 메시지가 표시 됩니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

**그림 3**: 필수 필드 누락

잘못 된 통화 금액을 입력 하면 **그림 4** 의 오류 메시지가 표시 됩니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

**그림 4**: 통화 금액이 잘못 되었습니다.

## <a name="using-data-annotation-validators-with-the-entity-framework"></a>Entity Framework에서 데이터 주석 유효성 검사기 사용

Microsoft Entity Framework를 사용 하 여 데이터 모델 클래스를 생성 하는 경우에는 클래스에 유효성 검사기 특성을 직접 적용할 수 없습니다. Entity Framework Designer는 모델 클래스를 생성 하므로 다음에 디자이너에서 변경 작업을 수행 하면 모델 클래스의 모든 변경 내용을 덮어쓰게 됩니다.

Entity Framework에서 생성 된 클래스에 유효성 검사기를 사용 하려면 메타 데이터 클래스를 만들어야 합니다. 실제 클래스에 유효성 검사기를 적용 하는 대신 메타 데이터 클래스에 유효성 검사기를 적용 합니다.

예를 들어 Entity Framework를 사용 하 여 동영상 클래스를 만들었다고 가정 합니다 ( **그림 5**참조). 또한 영화 제목 및 감독 속성에 필수 속성을 만들려고 한다고 가정 합니다. 이 경우 **목록 4**에서 partial 클래스 및 메타 데이터 클래스를 만들 수 있습니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

**그림 5**: Entity Framework에서 생성 된 동영상 클래스

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

**목록 4**: Models\Movie.cs

**목록 4** 의 파일에는 Movie 및 MovieMetaData 라는 두 개의 클래스가 있습니다. Movie 클래스는 partial 클래스입니다. DataModel 파일에 포함 된 Entity Framework에서 생성 된 partial 클래스에 해당 합니다.

현재 .NET framework는 부분 속성을 지원 하지 않습니다. 따라서 **목록 4**에서 파일에 정의 된 movie 클래스의 속성에 유효성 검사기 특성을 적용 하 여 DataModel 파일에 정의 된 movie 클래스의 속성에 유효성 검사기 특성을 적용할 수 없습니다.

Movie partial 클래스는 MovieMetaData 클래스를 가리키는 MetadataType 특성으로 데코 레이트 됩니다. MovieMetaData 클래스는 Movie 클래스의 속성에 대 한 프록시 속성을 포함 합니다.

유효성 검사기 특성은 MovieMetaData 클래스의 속성에 적용 됩니다. Title, Director 및 DateReleased 속성은 모두 필수 속성으로 표시 됩니다. 디렉터 속성은 5 자 미만의 문자열을 할당 해야 합니다. 마지막으로 DisplayName 특성은 DateReleased 속성에 적용 되어 "출시 날짜 필드는 필수입니다."와 같은 오류 메시지를 표시 합니다. "DateReleased 필드가 필요 합니다." 라는 오류는 발생 하지 않습니다.

> [!NOTE] 
> 
> MovieMetaData 클래스의 프록시 속성은 Movie 클래스의 해당 속성과 동일한 형식을 나타낼 필요가 없습니다. 예를 들어 Director 속성은 Movie 클래스의 문자열 속성 및 MovieMetaData 클래스의 개체 속성입니다.

**그림 6** 의 페이지에서는 영화 속성에 대해 잘못 된 값을 입력할 때 반환 되는 오류 메시지를 보여 줍니다.

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

**그림 6**: Entity Framework에 유효성 검사기 사용 ([전체 크기 이미지를 보려면 클릭](validation-with-the-data-annotation-validators-cs/_static/image14.png))

## <a name="summary"></a>요약

이 자습서에서는 데이터 주석 모델 바인더를 활용 하 여 ASP.NET MVC 응용 프로그램 내에서 유효성 검사를 수행 하는 방법을 알아보았습니다. 필수 및 StringLength 특성과 같은 다양 한 유형의 유효성 검사기 특성을 사용 하는 방법을 배웠습니다. Microsoft Entity Framework로 작업할 때 이러한 특성을 사용 하는 방법도 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-a-service-layer-cs.md)
> [다음](creating-model-classes-with-the-entity-framework-vb.md)
