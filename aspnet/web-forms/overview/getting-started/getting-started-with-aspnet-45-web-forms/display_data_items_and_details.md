---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 데이터 항목 및 세부 정보 표시 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈는 ASP.NET 4.7 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 보여줍니다.
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520811"
---
# <a name="display-data-items-and-details"></a>데이터 항목 및 세부 정보 표시

[Erik Reitan](https://github.com/Erikre)

> 이 자습서 시리즈에서는 ASP.NET 4.7 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 구축 하는 기본 사항을 설명 합니다.

이 자습서에서는 ASP.NET Web Forms를 사용 하 여 데이터 항목 및 데이터 항목 정보를 표시 하 고 Code First Entity Framework 하는 방법을 알아봅니다. 이 자습서는 정문 장난감 스토어 자습서 시리즈의 일부로 이전 "UI 및 탐색" 자습서를 기반으로 합니다. 이 자습서를 완료 한 후에는 *ProductsList* 페이지의 제품 및 제품 *세부 정보 .aspx* 페이지에 대 한 제품 정보를 볼 수 있습니다.

## <a name="youll-learn-how-to"></a>이 문서에서 배울 내용은 다음과 같습니다.

- 데이터 컨트롤을 추가 하 여 데이터베이스의 제품 표시
- 선택한 데이터에 데이터 컨트롤 연결
- 데이터베이스의 제품 정보를 표시 하는 데이터 컨트롤 추가
- 쿼리 문자열에서 값을 검색 하 고 해당 값을 사용 하 여 데이터베이스에서 검색 되는 데이터를 제한 합니다.

### <a name="features-introduced-in-this-tutorial"></a>이 자습서에 도입 된 기능은 다음과 같습니다.

- 모델 바인딩
- 값 공급자

## <a name="add-a-data-control"></a>데이터 컨트롤 추가

몇 가지 다른 옵션을 사용 하 여 데이터를 서버 컨트롤에 바인딩할 수 있습니다. 가장 일반적인 경우는 다음과 같습니다.

* 데이터 소스 컨트롤 추가
* 코드를 직접 추가
* 모델 바인딩 사용

### <a name="use-a-data-source-control-to-bind-data"></a>데이터 소스 컨트롤을 사용 하 여 데이터 바인딩

데이터 소스 컨트롤을 추가 하면 데이터 소스 컨트롤을 데이터를 표시 하는 컨트롤에 연결할 수 있습니다. 이 방법을 사용 하면 프로그래밍 방식으로 서버 쪽 컨트롤을 데이터 원본에 연결 하는 대신 선언적으로 사용할 수 있습니다.

### <a name="code-by-hand-to-bind-data"></a>데이터를 바인딩하기 위한 코딩

직접 코딩에는 다음이 포함 됩니다.

1. 값 읽기
2. Null 인지 확인
3. 적절 한 형식으로 변환
4. 변환 성공 확인 중
5. 쿼리에서 값 사용 

이 방법을 사용 하면 데이터 액세스 논리를 완전히 제어할 수 있습니다.

### <a name="use-model-binding-to-bind-data"></a>모델 바인딩을 사용 하 여 데이터 바인딩

모델 바인딩을 사용 하면 훨씬 더 작은 코드를 사용 하 여 결과를 바인딩하고 응용 프로그램 전체에서 기능을 재사용할 수 있습니다. 풍부한 데이터 바인딩 프레임 워크를 제공 하는 동시에 코드 중심 데이터 액세스 논리를 사용 하는 작업을 간소화 합니다.

## <a name="display-products"></a>제품 표시

이 자습서에서는 모델 바인딩을 사용 하 여 데이터를 바인딩합니다. 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 컨트롤의 `SelectMethod` 속성을 페이지 코드의 메서드 이름으로 설정 합니다. 데이터 컨트롤은 페이지 수명 주기에서 적절 한 시간에 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다. `DataBind` 메서드를 명시적으로 호출할 필요가 없습니다.

1. **솔루션 탐색기**에서 *ProductList*을 엽니다.
2. 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

이 코드는 `productList` 이라는 **ListView** 컨트롤을 사용 하 여 제품을 표시 합니다.

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

템플릿과 스타일을 사용 하 여 **ListView** 컨트롤에서 데이터를 표시 하는 방법을 정의 합니다. 반복 구조의 데이터에 유용 합니다. 이 **ListView** 예제는 단순히 데이터베이스 데이터를 표시 하지만, 코드를 사용 하지 않고도 사용자가 데이터를 편집, 삽입 및 삭제 하 고 데이터를 정렬 하 고 페이지를 지정할 수 있습니다.

**ListView** 컨트롤에서 `ItemType` 속성을 설정 하 여 데이터 바인딩 식 `Item`를 사용할 수 있으며 컨트롤이 강력한 형식으로 설정 됩니다. 이전 자습서에서 설명한 대로 IntelliSense를 사용 하 여 항목 개체 세부 정보를 선택할 수 있습니다 (예: `ProductName`지정).

![데이터 항목 및 세부 정보 표시-IntelliSense](display_data_items_and_details/_static/image1.png)

모델 바인딩을 사용 하 여 `SelectMethod` 값을 지정 하는 것도 있습니다. 이 값 (`GetProducts`)은 다음 단계에서 제품을 표시 하기 위해 코드 숨김으로 추가 하는 방법에 해당 합니다.

### <a name="add-code-to-display-products"></a>제품을 표시 하는 코드 추가

이 단계에서는 **ListView** 컨트롤을 데이터베이스의 제품 데이터로 채우는 코드를 추가 합니다. 이 코드는 모든 제품 및 개별 범주 제품 표시를 지원 합니다.

1. **솔루션 탐색기**에서 *ProductList* 를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 선택 합니다.
2. *ProductList.aspx.cs* 파일의 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

이 코드는 *ProductList* 페이지에서 **ListView** 컨트롤의 `ItemType` 속성이 참조 하는 `GetProducts` 메서드를 보여 줍니다. 특정 데이터베이스 범주에 대 한 결과를 제한 하기 위해 코드는 *ProductList* 페이지를 탐색할 때 *ProductList* 페이지에 전달 된 쿼리 문자열 값에서 `categoryId` 값을 설정 합니다. `System.Web.ModelBinding` 네임 스페이스의 `QueryStringAttribute` 클래스는 `id`쿼리 문자열 변수의 값을 검색 하는 데 사용 됩니다. 이렇게 하면 런타임에 쿼리 문자열의 값을 `categoryId` 매개 변수에 바인딩하기 위해 모델 바인딩이 수행 됩니다.

유효한 범주가 페이지에 쿼리 문자열로 전달 되는 경우 쿼리 결과는 데이터베이스에서 `categoryId` 값과 일치 하는 제품으로 제한 됩니다. 예를 들어, *ProductsList* 페이지 URL은 다음과 같습니다.

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

이 페이지에는 `categoryId` `1`와 같은 제품만 표시 됩니다.

*ProductList* 페이지가 호출 될 때 쿼리 문자열이 포함 되지 않은 경우 모든 제품이 표시 됩니다.

이러한 메서드에 대 한 값의 소스를 *값 공급자* (예: *QueryString*) 라고 하며 사용할 값 공급자를 나타내는 매개 변수 특성을 *값 공급자 특성* (예: `id`) 이라고 합니다. ASP.NET에는 쿼리 문자열, 쿠키, 폼 값, 컨트롤, 뷰 상태, 세션 상태 및 프로필 속성과 같은 Web Forms 응용 프로그램에서 사용자 입력의 일반적인 모든 원본에 대 한 값 공급자 및 해당 특성이 포함 됩니다. 사용자 지정 값 공급자를 작성할 수도 있습니다.

### <a name="run-the-application"></a>애플리케이션 실행

이제 응용 프로그램을 실행 하 여 모든 제품 또는 범주의 제품을 볼 수 있습니다.

1. Visual Studio에서 **f5** 키를 눌러 응용 프로그램을 실행 합니다.  
   브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*

2. 제품 범주 탐색 메뉴에서 **자동차** 를 선택 합니다.  
   *ProductList* 페이지에는 **자동차** 범주 제품만 표시 됩니다. 이 자습서의 뒷부분에서는 제품 세부 정보를 표시 합니다.  

    ![데이터 항목 및 세부 정보 표시-자동차](display_data_items_and_details/_static/image2.png)

3. 위쪽의 탐색 메뉴에서 **제품** 을 선택 합니다.  
   *ProductList* 페이지가 표시 되지만 이번에는 전체 제품 목록이 표시 됩니다.   

    ![데이터 항목 및 세부 정보 표시-제품](display_data_items_and_details/_static/image3.png)

4. 브라우저를 닫고 Visual Studio로 돌아갑니다.

### <a name="add-a-data-control-to-display-product-details"></a>제품 정보를 표시 하는 데이터 컨트롤 추가

다음으로, 이전 자습서에서 추가한 제품 *세부 정보 .aspx* 페이지의 태그를 수정 하 여 특정 제품 정보를 표시 합니다.

1. **솔루션 탐색기**에서 *제품 세부 정보 .aspx*를 엽니다.

2. 기존 태그를 다음 태그로 바꿉니다.

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    이 코드는 **FormView** 컨트롤을 사용 하 여 특정 제품 정보를 표시 합니다. 이 태그는 *ProductList* 페이지에 데이터를 표시 하는 데 사용 되는 메서드와 같은 메서드를 사용 합니다. **FormView** 컨트롤은 데이터 소스에서 한 번에 하나의 레코드를 표시 하는 데 사용 됩니다. **FormView** 컨트롤을 사용 하는 경우 데이터 바인딩된 값을 표시 하 고 편집 하는 템플릿을 만듭니다. 이러한 템플릿에는 폼의 모양과 기능을 정의 하는 컨트롤, 바인딩 식 및 형식이 포함 되어 있습니다.

이전 태그를 데이터베이스에 연결 하려면 추가 코드가 필요 합니다.

1. **솔루션 탐색기**에서 *제품 세부 정보 .aspx* 를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다.  
   *ProductDetails.aspx.cs* 파일이 표시 됩니다.

2. 기존 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

이 코드는 "`productID`" 쿼리 문자열 값을 확인 합니다. 올바른 쿼리 문자열 값이 발견 되 면 일치 하는 제품이 표시 됩니다. 쿼리 문자열을 찾을 수 없거나 해당 값이 유효 하지 않으면 제품이 표시 되지 않습니다.

### <a name="run-the-application"></a>애플리케이션 실행

이제 응용 프로그램을 실행 하 여 제품 ID에 따라 표시 된 개별 제품을 볼 수 있습니다.

1. Visual Studio에서 **f5** 키를 눌러 응용 프로그램을 실행 합니다.  
   브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*

2. 범주 탐색 메뉴에서 **배** 를 선택 합니다.  
   *ProductList* 페이지가 표시 됩니다.

3. 제품 목록에서 **Paper 보트** 를 선택 합니다.
   *제품 세부 정보 .aspx* 페이지가 표시 됩니다.

    ![데이터 항목 및 세부 정보 표시-제품](display_data_items_and_details/_static/image4.png)
    
4. 브라우저를 닫습니다.

## <a name="additional-resources"></a>추가 리소스

[모델 바인딩 및 web forms를 사용 하 여 데이터 검색 및 표시](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>다음 단계

이 자습서에서는 제품 및 제품 세부 정보를 표시 하는 태그와 코드를 추가 했습니다. 강력한 형식의 데이터 컨트롤, 모델 바인딩 및 값 공급자에 대해 알아보았습니다. 다음 자습서에서는 정문 장난감 샘플 응용 프로그램에 쇼핑 카트를 추가 합니다. 

> [!div class="step-by-step"]
> [이전](ui_and_navigation.md)
> [다음](shopping-cart.md)
