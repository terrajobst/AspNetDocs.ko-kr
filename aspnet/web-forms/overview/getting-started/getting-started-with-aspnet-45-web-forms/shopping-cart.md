---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 쇼핑 카트 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: d3b619ebd9448d30857ffbaf17fd245b1d54a662
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521117"
---
# <a name="shopping-cart"></a>쇼핑 카트

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 정문 장난감 sample ASP.NET Web Forms 응용 프로그램에 쇼핑 카트를 추가 하는 데 필요한 비즈니스 논리에 대해 설명 합니다. 이 자습서는 이전 자습서 인 "데이터 항목 및 세부 정보 표시"를 기반으로 하며, 정문 장난감 매장 자습서 시리즈의 일부입니다. 이 자습서를 완료 하면 샘플 앱의 사용자가 쇼핑 카트에 제품을 추가, 제거 및 수정할 수 있습니다.

## <a name="what-youll-learn"></a>학습할 내용:

1. 웹 응용 프로그램에 대 한 쇼핑 카트를 만드는 방법입니다.
2. 사용자가 쇼핑 카트에 항목을 추가할 수 있도록 하는 방법입니다.
3. [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) 컨트롤을 추가 하 여 쇼핑 카트 정보를 표시 하는 방법입니다.
4. 주문 합계를 계산 하 고 표시 하는 방법입니다.
5. 쇼핑 카트에 항목을 제거 하 고 업데이트 하는 방법입니다.
6. 쇼핑 카트 카운터를 포함 하는 방법입니다.

## <a name="code-features-in-this-tutorial"></a>이 자습서의 코드 기능:

1. Entity Framework Code First
2. 데이터 주석
3. 강력한 형식의 데이터 컨트롤
4. 모델 바인딩

## <a name="creating-a-shopping-cart"></a>쇼핑 카트 만들기

이 자습서 시리즈의 앞부분에서는 데이터베이스에서 제품 데이터를 보기 위한 페이지와 코드를 추가 했습니다. 이 자습서에서는 사용자가 구매 하고자 하는 제품을 관리 하는 쇼핑 카트를 만듭니다. 사용자는 등록 되거나 로그인 되지 않은 경우에도 쇼핑 카트에 항목을 찾아보고 추가할 수 있습니다. 쇼핑 카트 액세스를 관리 하기 위해 사용자가 처음으로 장바구니에 액세스할 때 GUID (globally unique identifier)를 사용 하 여 사용자에 게 고유한 `ID`를 할당 합니다. ASP.NET 세션 상태를 사용 하 여이 `ID`을 저장 합니다.

> [!NOTE] 
> 
> ASP.NET 세션 상태는 사용자가 사이트를 떠난 후 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하는 것은 대규모 사이트에서 성능에 영향을 미칠 수 있지만 세션 상태를 사용 하는 경우 데모용으로 효과적입니다. 정문 장난감 샘플 프로젝트는 외부 공급자 없이 세션 상태를 사용 하는 방법을 보여 줍니다 .이 경우 세션 상태는 사이트를 호스트 하는 웹 서버에서 in-process로 저장 됩니다. 응용 프로그램의 여러 인스턴스 또는 여러 서버에서 여러 응용 프로그램 인스턴스를 실행 하는 사이트를 제공 하는 대규모 사이트의 경우에는 **Windows Azure Cache Service**를 사용 하는 것이 좋습니다. 이 Cache Service는 웹 사이트 외부에 있는 분산 캐싱 서비스를 제공 하 여 in-process 세션 상태를 사용 하는 문제를 해결 합니다. 자세한 내용은 [Windows Azure 웹 사이트에서 ASP.NET 세션 상태를 사용 하는 방법](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)을 참조 하십시오.

### <a name="add-cartitem-as-a-model-class"></a>모델 클래스로 CartItem 추가

이 자습서 시리즈의 앞부분에서는 *모델* 폴더에 `Category` 및 `Product` 클래스를 만들어 범주 및 제품 데이터에 대 한 스키마를 정의 했습니다. 이제 새 클래스를 추가 하 여 쇼핑 카트에 대 한 스키마를 정의 합니다. 이 자습서의 뒷부분에서는 `CartItem` 테이블에 대 한 데이터 액세스를 처리 하는 클래스를 추가 합니다. 이 클래스는 쇼핑 카트에 항목을 추가, 제거 및 업데이트 하는 비즈니스 논리를 제공 합니다.

1. *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** -&gt; **새 항목**을 선택 합니다. 

    ![쇼핑 카트-새 항목](shopping-cart/_static/image1.png)
2. **새 항목 추가** 대화 상자가 표시됩니다. **코드**를 선택한 다음 **클래스**를 선택 합니다. 

    ![쇼핑 카트-새 항목 추가 대화 상자](shopping-cart/_static/image2.png)
3. 새 클래스의 이름을 *CartItem.cs*로 합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일이 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` 클래스에는 사용자가 쇼핑 카트에 추가 하는 각 제품을 정의 하는 스키마가 포함 되어 있습니다. 이 클래스는이 자습서 시리즈의 앞부분에서 만든 다른 스키마 클래스와 유사 합니다. 규칙에 따라 Entity Framework Code First `CartItem` 테이블의 기본 키가 `CartItemId` 또는 `ID`가 될 것으로 예상 합니다. 그러나이 코드는 데이터 주석 `[Key]` 특성을 사용 하 여 기본 동작을 재정의 합니다. ItemId 속성의 `Key` 특성은 `ItemID` 속성이 기본 키가 되도록 지정 합니다.

`CartId` 속성은 구매할 항목과 연결 된 사용자의 `ID`를 지정 합니다. 사용자가 쇼핑 카트에 액세스할 때 `ID`이 사용자를 만드는 코드를 추가 합니다. 이 `ID`는 ASP.NET 세션 변수로도 저장 됩니다.

### <a name="update-the-product-context"></a>제품 컨텍스트 업데이트

`CartItem` 클래스를 추가 하는 것 외에도 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 데이터베이스 컨텍스트 클래스를 업데이트 해야 합니다. 이렇게 하려면 새로 만든 `CartItem` 모델 클래스를 `ProductContext` 클래스에 추가 합니다.

1. **솔루션 탐색기**의 *모델* 폴더에서 *ProductContext.cs* 파일을 찾아 엽니다.
2. 다음과 같이 강조 표시 된 코드를 *ProductContext.cs* 파일에 추가 합니다.  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

이 자습서 시리즈의 앞에서 설명한 것 처럼 *ProductContext.cs* 파일의 코드는 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 `System.Data.Entity` 네임 스페이스를 추가 합니다. 이 기능에는 강력한 형식의 개체를 사용 하 여 데이터를 쿼리, 삽입, 업데이트 및 삭제 하는 기능이 포함 됩니다. `ProductContext` 클래스는 새로 추가 된 `CartItem` 모델 클래스에 대 한 액세스 권한을 추가 합니다.

### <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리 관리

다음으로 새 *논리* 폴더에 `ShoppingCart` 클래스를 만듭니다. `ShoppingCart` 클래스는 `CartItem` 테이블에 대 한 데이터 액세스를 처리 합니다. 또한 클래스에는 쇼핑 카트에 항목을 추가, 제거 및 업데이트 하는 비즈니스 논리가 포함 됩니다.

추가 될 쇼핑 카트 논리에는 다음 작업을 관리 하는 기능이 포함 됩니다.

1. 쇼핑 카트에 항목 추가
2. 쇼핑 카트에 항목 제거
3. 쇼핑 카트 ID 가져오기
4. 쇼핑 카트에 항목 검색
5. 모든 쇼핑 카트 항목의 금액 합계
6. 쇼핑 카트 데이터 업데이트

쇼핑 카트 페이지 (*ShoppingCart*) 및 쇼핑 카트 클래스를 함께 사용 하 여 쇼핑 카트 데이터에 액세스할 수 있습니다. 쇼핑 카트 페이지에 사용자가 쇼핑 카트에 추가 하는 모든 항목이 표시 됩니다. 쇼핑 카트 페이지 및 클래스 외에도 쇼핑 카트에 제품을 추가 하는 페이지 (고 간에*카트 .aspx*)를 만듭니다. ProductList 페이지에 코드를 추가 하 고 사용자가 장바구니에 제품을 추가할 수 있도록 *이 페이지에* 대 한 링크를 제공 하는 페이지에 코드를 추가 *합니다.*

다음 다이어그램은 사용자가 쇼핑 카트에 제품을 추가할 때 발생 하는 기본 프로세스를 보여 줍니다.

![쇼핑 카트-쇼핑 카트에 추가](shopping-cart/_static/image3.png)

사용자가 *ProductList* 페이지나 *제품 세부 정보 .Aspx* 페이지에서 **카트에 추가** 링크를 클릭 하면 응용 프로그램에서 ShoppingCart 페이지로 이동 *하 여 자동* 으로 페이지로 이동 합니다. ShoppingCart 클래스에서 메서드를 호출 하 여 선택 제품을 쇼핑 카트에 *추가 합니다.* *ShoppingCart* 페이지에는 쇼핑 카트에 추가 된 제품이 표시 됩니다.

#### <a name="creating-the-shopping-cart-class"></a>쇼핑 카트 클래스 만들기

`ShoppingCart` 클래스는 응용 프로그램에서 별도의 폴더에 추가 되므로 모델 (모델 폴더), 페이지 (루트 폴더) 및 논리 (논리 폴더)를 명확 하 게 구분할 수 있습니다.

1. **솔루션 탐색기**에서 **WingtipToys**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 폴더**&gt;**추가**-를 선택 합니다. 새 폴더의 이름을 *논리*로 합니다.
2. *논리* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.
3. *ShoppingCartActions.cs*라는 새 클래스 파일을 추가 합니다.
4. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart` 방법을 사용 하면 제품 `ID`를 기반으로 개별 제품을 쇼핑 카트에 포함할 수 있습니다. 제품을 카트에 추가 하거나 카트에 해당 제품에 대 한 항목이 이미 포함 된 경우 수량이 증가 합니다.

`GetCartId` 메서드는 사용자에 대 한 카트 `ID`를 반환 합니다. 카트 `ID`은 사용자가 쇼핑 카트에 있는 항목을 추적 하는 데 사용 됩니다. 사용자에 게 기존 카트 `ID`없는 경우 새 카트 `ID` 만들어집니다. 사용자가 등록 된 사용자로 로그인 한 경우에는 카트 `ID` 사용자 이름으로 설정 됩니다. 그러나 사용자가 로그인 하지 않은 경우에는 카트 `ID` 고유 값 (GUID)으로 설정 됩니다. GUID를 사용 하면 세션에 따라 각 사용자에 대해 하나의 카트만 생성 됩니다.

`GetCartItems` 메서드는 사용자에 대 한 쇼핑 카트 항목의 목록을 반환 합니다. 이 자습서의 뒷부분에서는 `GetCartItems` 메서드를 사용 하 여 쇼핑 카트에 카트 항목을 표시 하는 데 모델 바인딩이 사용 됨을 확인 합니다.

### <a name="creating-the-add-to-cart-functionality"></a>카트 추가 기능 만들기

앞에서 설명한 것 처럼 사용자의 쇼핑 카트에 새 제품을 추가 하는 데 사용 되는 라는 처리 페이지를 만듭니다 *.* 이 페이지는 방금 만든 `ShoppingCart` 클래스에서 `AddToCart` 메서드를 호출 합니다. 지 수 *카트 .aspx* 페이지에 제품 `ID` 전달 될 것으로 간주 됩니다. 이 제품 `ID`는 `ShoppingCart` 클래스에서 `AddToCart` 메서드를 호출할 때 사용 됩니다.

> [!NOTE] 
> 
> 페이지 UI (*AddToCart.aspx.cs* *)가*아니라이 페이지에 대 한 코드 숨김이 수정 됩니다.

#### <a name="to-create-the-add-to-cart-functionality"></a>카트 추가 기능을 만들려면 다음을 수행 합니다.

1. **솔루션 탐색기**에서 **WingtipToys**프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** -&gt; **새 항목**을 클릭 합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 표준 새 페이지 (Web Form)를 라는 응용 프로그램에 추가 *합니다.* 

    ![쇼핑 카트-Web Form 추가](shopping-cart/_static/image4.png)
3. **솔루션 탐색기**에서 마우스 오른쪽 단추를 클릭 하 고 **코드 보기**를 클릭 *합니다.* *AddToCart.aspx.cs* 코드 숨겨진 파일이 편집기에서 열립니다.
4. *AddToCart.aspx.cs* 코드에서 기존 코드를 다음으로 바꿉니다.   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

고 간에 *카트 .aspx* 페이지가 로드 되 면 쿼리 문자열에서 product `ID`가 검색 됩니다. 다음으로,이 자습서의 앞부분에서 추가한 `AddToCart` 메서드를 호출 하는 데 사용 되는 쇼핑 카트 클래스의 인스턴스를 만듭니다. *ShoppingCartActions.cs* 파일에 포함 된 `AddToCart` 메서드는 선택한 제품을 쇼핑 카트에 추가 하거나 선택한 제품의 제품 수량을 증가 시키는 논리를 포함 합니다. 제품을 장바구니에 추가 하지 않은 경우에는 데이터베이스가 데이터베이스의 `CartItem` 테이블에 추가 됩니다. 제품이 이미 쇼핑 카트에 추가 되었고 사용자가 동일한 제품의 추가 항목을 추가 하는 경우 제품 수량이 `CartItem` 테이블에서 증가 합니다. 마지막으로 페이지는 다음 단계에서 추가할 *ShoppingCart* 페이지로 다시 리디렉션됩니다. 그러면 사용자가 카트에 있는 업데이트 된 항목 목록을 볼 수 있습니다.

앞에서 설명한 대로 사용자 `ID`는 특정 사용자와 연결 된 제품을 식별 하는 데 사용 됩니다. 이 `ID`은 사용자가 쇼핑 카트에 제품을 추가할 때마다 `CartItem` 테이블의 행에 추가 됩니다.

### <a name="creating-the-shopping-cart-ui"></a>쇼핑 카트 UI 만들기

*ShoppingCart* 페이지에 사용자가 쇼핑 카트에 추가한 제품이 표시 됩니다. 또한 쇼핑 카트에 항목을 추가, 제거 및 업데이트할 수 있는 기능도 제공 합니다.

1. **솔루션 탐색기**에서 **WingtipToys**을 마우스 오른쪽 단추로 클릭 하 고 **추가** -&gt; **새 항목**을 클릭 합니다.  
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 마스터 페이지를 **사용 하 여 Web form**을 선택 하 여 마스터 페이지를 포함 하는 새 페이지 (web form)를 추가 합니다. 새 페이지 이름을 *ShoppingCart*로 합니다.
3. 마스터 페이지를 새로 만든 *.aspx* 페이지에 연결 **하려면 site.master를 선택 합니다** .
4. *ShoppingCart* 페이지에서 기존 태그를 다음 태그로 바꿉니다.   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart* 페이지에는 `CartList`라는 **GridView** 컨트롤이 포함 되어 있습니다. 이 컨트롤은 모델 바인딩을 사용 하 여 쇼핑 카트 데이터를 데이터베이스에서 **GridView** 컨트롤로 바인딩합니다. **GridView** 컨트롤의 `ItemType` 속성을 설정 하는 경우 컨트롤의 태그에서 데이터 바인딩 `Item` 식을 사용할 수 있으며 컨트롤이 강력한 형식이 됩니다. 이 자습서 시리즈의 앞부분에서 설명한 것 처럼 IntelliSense를 사용 하 여 `Item` 개체의 세부 정보를 선택할 수 있습니다. 모델 바인딩을 사용 하 여 데이터를 선택 하도록 데이터 컨트롤을 구성 하려면 컨트롤의 `SelectMethod` 속성을 설정 합니다. 위의 태그에서 `CartItem` 개체의 목록을 반환 하는 GetShoppingCartItems 메서드를 사용 하도록 `SelectMethod`를 설정 합니다. **GridView** 데이터 컨트롤은 페이지 수명 주기에서 적절 한 시간에 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다. `GetShoppingCartItems` 메서드를 계속 추가 해야 합니다.

#### <a name="retrieving-the-shopping-cart-items"></a>쇼핑 카트 항목 검색

그런 다음 *ShoppingCart.aspx.cs* 코드 숨김으로 코드를 추가 하 여 쇼핑 카트 UI를 검색 하 고 채웁니다.

1. **솔루션 탐색기**에서 *ShoppingCart* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **코드 보기**를 클릭 합니다. *ShoppingCart.aspx.cs* 코드 숨겨진 파일이 편집기에서 열립니다.
2. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

위에서 설명한 것 처럼 `GridView` 데이터 컨트롤은 페이지 수명 주기에서 적절 한 시간에 `GetShoppingCartItems` 메서드를 호출 하 고 반환 된 데이터를 자동으로 바인딩합니다. `GetShoppingCartItems` 메서드는 `ShoppingCartActions` 개체의 인스턴스를 만듭니다. 그런 다음 코드는 해당 인스턴스를 사용 하 여 `GetCartItems` 메서드를 호출 하 여 카트에 있는 항목을 반환 합니다.

### <a name="adding-products-to-the-shopping-cart"></a>쇼핑 카트에 제품 추가

*ProductList* 또는 제품 *세부 정보 .aspx* 페이지가 표시 되 면 사용자가 링크를 사용 하 여 제품을 쇼핑 카트에 추가할 수 있습니다. 링크를 클릭 하면 응용 프로그램에서이 페이지를 이동 *합니다.* 이 자습서의 앞부분에서 추가한 `ShoppingCart` 클래스에서 `AddToCart` 메서드가 호출 *됩니다.*

이제 *ProductList* 페이지와 *제품 세부 정보 .aspx* 페이지 모두에 **카트에 추가** 링크를 추가 합니다. 이 링크에는 데이터베이스에서 검색 된 제품 `ID` 포함 됩니다.

1. **솔루션 탐색기**에서 *ProductList*라는 페이지를 찾아 엽니다.
2. 노란색으로 강조 표시 된 태그를 *ProductList* 페이지에 추가 하 여 전체 페이지가 다음과 같이 표시 되도록 합니다.  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>쇼핑 카트 테스트

응용 프로그램을 실행 하 여 쇼핑 카트에 제품을 추가 하는 방법을 확인 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.  
 프로젝트가 데이터베이스를 다시 만들면 브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
2. 범주 탐색 메뉴에서 **자동차** 를 선택 합니다.  
 *ProductList* 페이지는 "자동차" 범주에 포함 된 제품만 표시 합니다. 

    ![쇼핑 카트-자동차](shopping-cart/_static/image5.png)
3. 표시 되는 첫 번째 제품 옆에 있는 **카트에 추가** 링크를 클릭 합니다 (컨버터블 자동차).   
 *ShoppingCart* 페이지가 표시 되 고 쇼핑 카트에 선택 항목이 표시 됩니다. 

    ![쇼핑 카트-카트](shopping-cart/_static/image6.png)
4. 범주 탐색 메뉴에서 **평면** 을 선택 하 여 추가 제품을 봅니다.
5. 나열 된 첫 번째 제품 옆에 있는 **카트에 추가** 링크를 클릭 합니다.  
 추가 항목이 포함 된 *ShoppingCart* 페이지가 표시 됩니다.
6. 브라우저를 닫습니다.

### <a name="calculating-and-displaying-the-order-total"></a>주문 합계 계산 및 표시

쇼핑 카트에 제품을 추가 하는 것 외에도 `ShoppingCart` 클래스에 `GetTotal` 메서드를 추가 하 고 쇼핑 카트 페이지에 총 주문 금액을 표시 합니다.

1. **솔루션 탐색기**에서 *논리* 폴더에 있는 *ShoppingCartActions.cs* 파일을 엽니다.
2. 노란색으로 강조 표시 된 다음 `GetTotal` 메서드를 `ShoppingCart` 클래스에 추가 하 여 클래스가 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

먼저 `GetTotal` 메서드는 사용자에 대 한 쇼핑 카트의 ID를 가져옵니다. 그런 다음, 메서드는 제품 가격과 카트에 나열 된 각 제품의 제품 수량을 곱하여 카트 합계를 가져옵니다.

> [!NOTE] 
> 
> 위의 코드는 nullable 형식 "`int?`"을 사용 합니다. Nullable 형식은 기본 형식의 모든 값과 null 값을 나타낼 수 있습니다. 자세한 내용은 [Nullable 형식 사용](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)을 참조 하세요.

### <a name="modify-the-shopping-cart-display"></a>쇼핑 카트 표시 수정

다음에는 *ShoppingCart* 페이지의 코드를 수정 하 여 `GetTotal` 메서드를 호출 하 고 페이지가 로드 될 때 *ShoppingCart* 페이지에 해당 합계를 표시 합니다.

1. **솔루션 탐색기**에서 *ShoppingCart* 페이지를 마우스 오른쪽 단추로 클릭 하 고 **코드 보기**를 선택 합니다.
2. *ShoppingCart.aspx.cs* 파일에서 노란색으로 강조 표시 된 다음 코드를 추가 하 여 `Page_Load` 처리기를 업데이트 합니다.   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

*ShoppingCart* 페이지가 로드 되 면 쇼핑 카트 개체를 로드 한 다음 `ShoppingCart` 클래스의 `GetTotal` 메서드를 호출 하 여 쇼핑 카트 합계를 검색 합니다. 장바구니를 비워 두면 해당 효과에 대 한 메시지가 표시 됩니다.

### <a name="testing-the-shopping-cart-total"></a>쇼핑 카트 합계 테스트

지금 응용 프로그램을 실행 하 여 쇼핑 카트에 제품을 추가할 수 있을 뿐만 아니라 쇼핑 카트 합계를 볼 수 있습니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.  
 브라우저가 열리고 *Default.aspx* 페이지가 표시됩니다.
2. 범주 탐색 메뉴에서 **자동차** 를 선택 합니다.
3. 첫 번째 제품 옆에 있는 **카트에 추가** 링크를 클릭 합니다.   
 *ShoppingCart* 페이지가 주문 합계와 함께 표시 됩니다. 

    ![쇼핑 카트-카트 합계](shopping-cart/_static/image7.png)
4. 카트에 다른 제품 (예: 평면)을 추가 합니다.
5. *ShoppingCart* 페이지에는 추가한 모든 제품의 업데이트 된 합계가 표시 됩니다. 

    ![쇼핑 카트-여러 제품](shopping-cart/_static/image8.png)
6. 브라우저 창을 닫아 실행 중인 응용 프로그램을 중지 합니다.

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>쇼핑 카트에 업데이트 및 체크 아웃 단추 추가

사용자가 쇼핑 카트를 수정할 수 있도록 하려면 쇼핑 카트 페이지에 **업데이트** 단추와 **체크 아웃** 단추를 추가 합니다. 이 자습서 시리즈의 뒷부분에서는 **체크 아웃** 단추가 사용 되지 않습니다.

1. **솔루션 탐색기**에서 웹 응용 프로그램 프로젝트의 루트에 있는 *ShoppingCart* 페이지를 엽니다.
2. **업데이트** 단추와 **체크 아웃** 단추를 *ShoppingCart* 페이지에 추가 하려면 다음 코드에 표시 된 것 처럼 기존 태그에 노란색으로 강조 표시 된 태그를 추가 합니다.   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

사용자가 **업데이트** 단추를 클릭 하면 `UpdateBtn_Click` 이벤트 처리기가 호출 됩니다. 이 이벤트 처리기는 다음 단계에서 추가할 코드를 호출 합니다.

그런 다음 *ShoppingCart.aspx.cs* 파일에 포함 된 코드를 업데이트 하 여 장바구니 항목을 반복 하 고 `RemoveItem` 및 `UpdateItem` 메서드를 호출할 수 있습니다.

1. **솔루션 탐색기**에서 웹 응용 프로그램 프로젝트의 루트에 있는 *ShoppingCart.aspx.cs* 파일을 엽니다.
2. 노란색으로 강조 표시 된 다음 코드 섹션을 *ShoppingCart.aspx.cs* 파일에 추가 합니다.   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

사용자가 *ShoppingCart* 페이지에서 **업데이트** 단추를 클릭 하면 UpdateCartItems 메서드가 호출 됩니다. UpdateCartItems 메서드는 쇼핑 카트에 있는 각 항목에 대 한 업데이트 된 값을 가져옵니다. 그런 다음 UpdateCartItems 메서드는 다음 단계에서 추가 및 설명 된 `UpdateShoppingCartDatabase` 메서드를 호출 하 여 쇼핑 카트에 항목을 추가 하거나 제거 합니다. 쇼핑 카트에 업데이트를 반영 하도록 데이터베이스를 업데이트 한 후에는 **gridview**에 대 한 `DataBind` 메서드를 호출 하 여 쇼핑 카트 페이지에서 **gridview** 컨트롤이 업데이트 됩니다. 또한 쇼핑 카트 페이지의 총 주문 금액이 업데이트 되어 업데이트 된 항목 목록을 반영 합니다.

### <a name="updating-and-removing-shopping-cart-items"></a>쇼핑 카트 항목 업데이트 및 제거

*ShoppingCart* 페이지에서 항목의 수량을 업데이트 하 고 항목을 제거 하기 위한 컨트롤이 추가 된 것을 볼 수 있습니다. 이제 이러한 컨트롤이 작동 하 게 만드는 코드를 추가 합니다.

1. **솔루션 탐색기**에서 *논리* 폴더에 있는 *ShoppingCartActions.cs* 파일을 엽니다.
2. 노란색으로 강조 표시 된 다음 코드를 *ShoppingCartActions.cs* 클래스 파일에 추가 합니다.   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

*ShoppingCart.aspx.cs* 페이지의 `UpdateCartItems` 메서드에서 호출 되는 `UpdateShoppingCartDatabase` 메서드는 쇼핑 카트에 항목을 업데이트 하거나 제거 하는 논리를 포함 합니다. `UpdateShoppingCartDatabase` 메서드는 쇼핑 카트 목록 내의 모든 행을 반복 합니다. 쇼핑 카트 항목이 제거 됨으로 표시 되었거나 수량이 1 보다 작은 경우 `RemoveItem` 메서드가 호출 됩니다. 그렇지 않으면 `UpdateItem` 메서드가 호출 될 때 쇼핑 카트 항목에 업데이트가 있는지 확인 됩니다. 쇼핑 카트 항목이 제거 되거나 업데이트 된 후에는 데이터베이스 변경 내용이 저장 됩니다.

`ShoppingCartUpdates` 구조는 모든 쇼핑 카트 항목을 저장 하는 데 사용 됩니다. `UpdateShoppingCartDatabase` 메서드는 `ShoppingCartUpdates` 구조를 사용 하 여 업데이트 또는 제거 해야 하는 항목이 있는지 확인 합니다.

다음 자습서에서는 제품을 구매한 후에 `EmptyCart` 메서드를 사용 하 여 쇼핑 카트를 삭제 합니다. 그러나 지금은 *ShoppingCartActions.cs* 파일에 추가한 `GetCount` 메서드를 사용 하 여 쇼핑 카트에 있는 항목 수를 확인 합니다.

### <a name="adding-a-shopping-cart-counter"></a>쇼핑 카트 카운터 추가

사용자가 쇼핑 카트에 있는 총 항목 수를 볼 수 있도록 하려면 *사이트. 마스터* 페이지에 카운터를 추가 합니다. 이 카운터는 장바구니에 대 한 링크로도 작동 합니다.

1. **솔루션 탐색기**에서 *사이트 마스터* 페이지를 엽니다.
2. 다음과 같이 표시 되도록 노란색의 탐색 섹션에 표시 된 대로 쇼핑 카트 카운터 링크를 추가 하 여 태그를 수정 합니다.  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. 다음으로 노란색으로 강조 표시 된 코드를 다음과 같이 추가 하 여 *Site.Master.cs* 파일의 코드를 업데이트 합니다.  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

페이지가 HTML로 렌더링 되기 전에 `Page_PreRender` 이벤트가 발생 합니다. `Page_PreRender` 처리기에서 쇼핑 카트의 총 수는 `GetCount` 메서드를 호출 하 여 결정 됩니다. 반환 된 값은 *Site. Master* 페이지의 태그에 포함 된 `cartCount` 범위에 추가 됩니다. `<span>` 태그를 사용 하면 내부 요소가 제대로 렌더링 됩니다. 사이트의 페이지가 표시 되 면 장바구니 합계가 표시 됩니다. 사용자는 쇼핑 카트 합계를 클릭 하 여 장바구니를 표시할 수도 있습니다.

## <a name="testing-the-completed-shopping-cart"></a>완성 된 쇼핑 카트 테스트

지금 응용 프로그램을 실행 하 여 쇼핑 카트에 항목을 추가, 삭제 및 업데이트할 수 있는 방법을 확인할 수 있습니다. 쇼핑 카트 합계는 쇼핑 카트에 있는 모든 항목의 총 비용을 반영 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.  
 브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
2. 범주 탐색 메뉴에서 **자동차** 를 선택 합니다.
3. 첫 번째 제품 옆에 있는 **카트에 추가** 링크를 클릭 합니다.   
 *ShoppingCart* 페이지가 주문 합계와 함께 표시 됩니다.
4. 범주 탐색 메뉴에서 **평면** 을 선택 합니다.
5. 첫 번째 제품 옆에 있는 **카트에 추가** 링크를 클릭 합니다.
6. 쇼핑 카트에 있는 첫 번째 항목의 수량을 3으로 설정 하 고 두 번째 항목의 **항목 제거** 확인란을 선택 합니다.<a id="a"></a>
7. **업데이트** 단추를 클릭 하 여 쇼핑 카트 페이지를 업데이트 하 고 새 주문 합계를 표시 합니다. 

    ![쇼핑 카트-카트 업데이트](shopping-cart/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 정문 장난감 Web Forms 샘플 응용 프로그램에 대 한 쇼핑 카트를 만들었습니다. 이 자습서를 진행 하는 동안 Entity Framework Code First, 데이터 주석, 강력한 형식의 데이터 컨트롤 및 모델 바인딩을 사용 했습니다.

쇼핑 카트는 사용자가 구매 하도록 선택한 항목의 추가, 삭제 및 업데이트를 지원 합니다. 쇼핑 카트 기능을 구현 하는 것 외에도 **GridView** 컨트롤에서 쇼핑 카트 항목을 표시 하 고 주문 합계를 계산 하는 방법을 배웠습니다.

실제 비즈니스 응용 프로그램에서 설명 된 기능이 작동 하는 방식을 이해 하기 위해 [nopCommerce](https://github.com/nopSolutions/nopCommerce) -ASP.NET 기반 오픈 소스 전자 상거래 장바구니의 예제를 볼 수 있습니다. 처음에는 MVC로 이동 하 여 ASP.NET Core 하는 데 Web Forms를 기반으로 합니다.

## <a name="addition-information"></a>추가 정보

[ASP.NET 세션 상태 개요](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [이전](display_data_items_and_details.md)
> [다음](checkout-and-payment-with-paypal.md)
