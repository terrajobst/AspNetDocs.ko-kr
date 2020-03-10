---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: 데이터 액세스 계층 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78438377"
---
# <a name="create-the-data-access-layer"></a>데이터 액세스 레이어 만들기

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 ASP.NET Web Forms 및 Entity Framework Code First를 사용 하 여 데이터베이스에서 데이터를 만들고 액세스 하 고 검토 하는 방법을 설명 합니다. 이 자습서는 이전 자습서 "프로젝트 만들기"를 기반으로 하며, 정문 장난감 스토어 자습서 시리즈의 일부입니다. 이 자습서를 완료 하면 프로젝트의 *모델* 폴더에 있는 데이터 액세스 클래스의 그룹을 빌드할 수 있습니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 데이터 모델을 만드는 방법
- 데이터베이스를 초기화 하 고 초기값을 만드는 방법
- 데이터베이스를 지원 하도록 응용 프로그램을 업데이트 하 고 구성 하는 방법입니다.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>자습서에서 소개 하는 기능은 다음과 같습니다.

- Entity Framework Code First
- LocalDB
- 데이터 주석

## <a name="creating-the-data-models"></a>데이터 모델 만들기

[Entity Framework](https://msdn.microsoft.com/data/aa937723) 은 ORM (개체 관계형 매핑) 프레임 워크입니다. 이를 통해 관계형 데이터를 개체로 사용 하 여 일반적으로 작성 해야 하는 대부분의 데이터 액세스 코드를 제거할 수 있습니다. Entity Framework를 사용 하 여 [LINQ](https://msdn.microsoft.com/library/bb397926.aspx)를 사용 하 여 쿼리를 실행 한 다음 데이터를 강력한 형식의 개체로 검색 및 조작할 수 있습니다. LINQ는 데이터 쿼리 및 업데이트를 위한 패턴을 제공 합니다. Entity Framework를 사용 하면 데이터 액세스 기본 사항에 중점을 두는 대신 응용 프로그램의 나머지 부분을 만드는 데 집중할 수 있습니다. 이 자습서 시리즈의 뒷부분에서 데이터를 사용 하 여 탐색 및 제품 쿼리를 채우는 방법을 보여 드리겠습니다.

Entity Framework는 *Code First*라는 개발 패러다임을 지원 합니다. Code First를 사용 하면 클래스를 사용 하 여 데이터 모델을 정의할 수 있습니다. 클래스는 다른 형식, 메서드 및 이벤트의 변수를 함께 그룹화 하 여 사용자 고유의 사용자 지정 형식을 만들 수 있도록 하는 구문입니다. 클래스를 기존 데이터베이스에 매핑하거나이를 사용 하 여 데이터베이스를 생성할 수 있습니다. 이 자습서에서는 데이터 모델 클래스를 작성 하 여 데이터 모델을 만듭니다. 그런 다음 이러한 새 클래스에서 즉시 데이터베이스를 만들 Entity Framework 있습니다.

먼저 Web Forms 응용 프로그램에 대 한 데이터 모델을 정의 하는 엔터티 클래스를 만듭니다. 그런 다음 엔터티 클래스를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 하는 컨텍스트 클래스를 만듭니다. 또한 데이터베이스를 채우는 데 사용할 이니셜라이저 클래스를 만듭니다.

### <a name="entity-framework-and-references"></a>Entity Framework 및 참조

기본적으로 Entity Framework는 **Web Forms** 템플릿을 사용 하 여 새 **ASP.NET 웹 응용 프로그램** 을 만들 때 포함 됩니다. Entity Framework는 NuGet 패키지로 설치, 제거 및 업데이트할 수 있습니다.

이 NuGet 패키지는 프로젝트에 다음 **런타임** 어셈블리를 포함 합니다.

- EntityFramework .dll – Entity Framework에서 사용 하는 모든 공용 런타임 코드
- EntityFramework. SqlServer – Entity Framework에 대 한 Microsoft SQL Server 공급자

### <a name="entity-classes"></a>엔터티 클래스

데이터의 스키마를 정의 하기 위해 만드는 클래스를 엔터티 클래스 라고 합니다. 데이터베이스 디자인을 처음 접하는 경우 엔터티 클래스를 데이터베이스의 테이블 정의로 간주 합니다. 클래스의 각 속성은 데이터베이스 테이블의 열을 지정 합니다. 이러한 클래스는 개체 지향 코드와 데이터베이스의 관계형 테이블 구조 간에 간단한 개체 관계형 인터페이스를 제공 합니다.

이 자습서에서는 제품 및 범주에 대 한 스키마를 나타내는 간단한 엔터티 클래스를 추가 하 여 시작 합니다. Products 클래스에는 각 제품에 대 한 정의가 포함 됩니다. Product 클래스의 각 멤버 이름은 `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`, `Category`입니다. Category 클래스에는 제품이 속할 수 있는 각 범주에 대 한 정의 (예: 자동차, 보트 또는 평면)가 포함 됩니다. Category 클래스의 각 멤버 이름은 `CategoryID`, `CategoryName`, `Description`및 `Products`됩니다. 각 제품은 범주 중 하나에 속합니다. 이러한 엔터티 클래스는 프로젝트의 기존 *모델* 폴더에 추가 됩니다.

1. **솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image1.png)

   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **설치 됨** 창에서 **Visual C#**  아래에 있는 **코드**를 선택 합니다. 

    ![데이터 액세스 계층-새 항목 메뉴 만들기](create_the_data_access_layer/_static/image2.png)
3. 가운데 창에서 **클래스** 를 선택 하 고이 새 클래스의 이름을 *Product.cs*로 선택 합니다.
4. **추가**를 클릭합니다.  
   새 클래스 파일이 편집기에 표시 됩니다.
5. 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. 1 ~ 4 단계를 반복 하 여 다른 클래스를 만들고, 새 클래스의 이름을 *Category.cs* 로 변경 하 고, 기본 코드를 다음 코드로 바꿉니다.  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

앞에서 설명한 것 처럼 `Category` 클래스는 응용 프로그램이 판매 하도록 디자인 된 제품의 유형 (예: <a id="a"></a>&quot;자동차&quot;, &quot;배&quot;, &quot;Rockets&quot;등)을 나타내며, `Product` 클래스는 데이터베이스의 개별 제품 (장난감)을 나타냅니다. `Product` 개체의 각 인스턴스는 관계형 데이터베이스 테이블의 행에 해당 하며 Product 클래스의 각 속성은 관계형 데이터베이스 테이블의 열에 매핑됩니다. 이 자습서의 뒷부분에서는 데이터베이스에 포함 된 제품 데이터를 검토 합니다.

### <a name="data-annotations"></a>데이터 주석

클래스의 특정 멤버에 `[ScaffoldColumn(false)]`와 같은 멤버에 대 한 세부 정보를 지정 하는 특성이 있다는 것을 알 수 있습니다. 이는 *데이터 주석*입니다. 데이터 주석 특성은 해당 멤버에 대 한 사용자 입력의 유효성을 검사 하 고, 형식을 지정 하 고, 데이터베이스를 만들 때 모델링 하는 방법을 지정 하는 방법을 설명할 수 있습니다.

### <a name="context-class"></a>Context 클래스

데이터 액세스를 위한 클래스 사용을 시작 하려면 컨텍스트 클래스를 정의 해야 합니다. 앞에서 설명한 것 처럼 컨텍스트 클래스는 엔터티 클래스 (예: `Product` 클래스 및 `Category` 클래스)를 관리 하 고 데이터베이스에 대 한 데이터 액세스를 제공 합니다.

이 프로시저는 새 C# 컨텍스트 클래스를 *모델* 폴더에 추가 합니다.

1. *모델* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 가운데 창에서 **클래스** 를 선택 하 고 이름을 *ProductContext.cs* 로 선택한 후 **추가**를 클릭 합니다.
3. 클래스에 포함 된 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

이 코드는 강력한 형식의 개체를 사용 하 여 데이터를 쿼리, 삽입, 업데이트 및 삭제 하는 기능이 포함 된 Entity Framework의 모든 핵심 기능에 액세스할 수 있도록 `System.Data.Entity` 네임 스페이스를 추가 합니다.

`ProductContext` 클래스는 데이터베이스에서 `Product` 클래스 인스턴스를 가져오고, 저장 하 고, 업데이트 하는 것을 처리 하는 Entity Framework product 데이터베이스 컨텍스트를 나타냅니다. `ProductContext` 클래스는 Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.

### <a name="initializer-class"></a>이니셜라이저 클래스

컨텍스트를 처음 사용할 때 데이터베이스를 초기화 하려면 일부 사용자 지정 논리를 실행 해야 합니다. 이렇게 하면 제품 및 범주를 즉시 표시할 수 있도록 시드 데이터를 데이터베이스에 추가할 수 있습니다.

이 절차에서는 새 C# 이니셜라이저 클래스를 *모델* 폴더에 추가 합니다.

1. *모델* 폴더에서 다른 `Class`를 만들고 이름을 *ProductDatabaseInitializer.cs*로 다시 만듭니다.
2. 클래스에 포함 된 기본 코드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

위의 코드에서 볼 수 있듯이 데이터베이스를 만들고 초기화할 때 `Seed` 속성이 재정의 되 고가 설정 됩니다. `Seed` 속성이 설정 되 면 범주 및 제품의 값을 사용 하 여 데이터베이스를 채웁니다. 데이터베이스를 만든 후 위의 코드를 수정 하 여 초기값 데이터를 업데이트 하려고 하면 웹 응용 프로그램을 실행할 때 업데이트가 표시 되지 않습니다. 그 이유는 위의 코드에서 `DropCreateDatabaseIfModelChanges` 클래스의 구현을 사용 하 여 시드 데이터를 다시 설정 하기 전에 모델 (스키마)이 변경 되었는지 여부를 인식 하는 것입니다. `Category` 및 `Product` 엔터티 클래스에 대 한 변경 내용이 없는 경우 데이터베이스는 초기값 데이터로 다시 초기화 되지 않습니다.

> [!NOTE] 
> 
> 응용 프로그램을 실행할 때마다 데이터베이스를 다시 만들려면 `DropCreateDatabaseIfModelChanges` 클래스 대신 `DropCreateDatabaseAlways` 클래스를 사용 합니다. 그러나이 자습서 시리즈의 경우 `DropCreateDatabaseIfModelChanges` 클래스를 사용 합니다.

이 자습서의이 시점에서 4 개의 새 클래스와 하나의 기본 클래스를 포함 하는 *모델* 폴더가 있습니다.

![데이터 액세스 계층-모델 폴더 만들기](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>데이터 모델을 사용 하도록 응용 프로그램 구성

이제 데이터를 나타내는 클래스를 만들었으므로 클래스를 사용 하도록 응용 프로그램을 구성 해야 합니다. *Global.asax* 파일에서 모델을 초기화 하는 코드를 추가 합니다. *Web.config* 파일에서 새 데이터 클래스가 나타내는 데이터를 저장 하는 데 사용할 데이터베이스를 응용 프로그램에 알리는 정보를 추가 합니다. *Global.asax* 파일을 사용 하 여 응용 프로그램 이벤트 또는 메서드를 처리할 수 있습니다. Web.config *파일을* 사용 하 여 ASP.NET 웹 응용 프로그램의 구성을 제어할 수 있습니다.

#### <a name="updating-the-globalasax-file"></a>Global.asax 파일 업데이트

응용 프로그램이 시작 될 때 데이터 모델을 초기화 하려면 *Global.asax.cs* 파일에서 `Application_Start` 처리기를 업데이트 합니다.

> [!NOTE] 
> 
> 솔루션 탐색기에서 *global.asax* 파일 또는 *Global.asax.cs* 파일 중 하나를 선택 하 여 *Global.asax.cs* 파일을 편집할 수 있습니다.

1. 노란색으로 강조 표시 된 다음 코드를 *Global.asax.cs* 파일의 `Application_Start` 메서드에 추가 합니다.   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> 브라우저에서이 자습서 시리즈를 볼 때 노란색으로 강조 표시 된 코드를 보려면 브라우저에서 HTML5를 지원 해야 합니다.

위의 코드에 표시 된 것 처럼 응용 프로그램이 시작 되 면 응용 프로그램은 처음에 데이터에 액세스할 때 실행 되는 이니셜라이저를 지정 합니다. `Database` 개체 및 `ProductDatabaseInitializer` 개체에 액세스 하려면 두 개의 추가 네임 스페이스가 필요 합니다.

 Web.config 파일 수정 

데이터베이스가 시드 데이터로 채워질 때 Entity Framework Code First 기본 위치에 데이터베이스를 생성 하므로 응용 프로그램에 사용자 고유의 연결 정보를 추가 하면 데이터베이스 위치를 제어할 수 있습니다. 프로젝트의 루트에 있는 응용 프로그램의 *web.config* 파일에서 연결 문자열을 사용 하 여이 데이터베이스 연결을 지정 합니다. 새 연결 문자열을 추가 하 여 데이터베이스 (*wingtiptoys*)의 위치를 기본 위치가 아닌 응용 프로그램의 데이터 디렉터리 (*앱\_데이터*)에서 빌드할 수 있습니다. 이렇게 변경 하면이 자습서의 뒷부분에서 데이터베이스 파일을 찾아 검사할 수 있습니다.

1. **솔루션 탐색기**에서 *web.config 파일을 찾아 엽니다.*
2. 노란색으로 강조 표시 된 연결 문자열을 web.config 파일의 `<connectionStrings>` 섹션에 다음과 같이 *추가 합니다.*  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

응용 프로그램을 처음 실행 하는 경우 연결 문자열에 지정 된 위치에 데이터베이스를 빌드합니다. 응용 프로그램을 실행 하기 전에 먼저 빌드 해 보겠습니다.

## <a name="building-the-application"></a>응용 프로그램 빌드

웹 응용 프로그램에 대 한 모든 클래스와 변경 내용을 확인 하려면 응용 프로그램을 빌드해야 합니다.

1. **디버그** 메뉴에서 **WingtipToys 빌드**를 선택 합니다.  
 **출력** 창이 표시 되 고 모든 작업이 정상적으로 완료 되 면 *성공* 메시지가 표시 됩니다.  

    ![데이터 액세스 계층-출력 창 만들기](create_the_data_access_layer/_static/image4.png)

오류가 발생 하는 경우 위의 단계를 다시 확인 합니다. **출력** 창의 정보는 문제가 있는 파일 및 파일에서 변경이 필요한 위치를 표시 합니다. 이 정보를 사용 하 여 프로젝트에서 위의 단계를 검토 하 고 수정 해야 하는 부분을 확인할 수 있습니다.

## <a name="summary"></a>요약

데이터 모델을 만든 시리즈의이 자습서에서는 데이터베이스를 초기화 하 고 초기값으로 사용 되는 코드를 추가 했습니다. 또한 응용 프로그램이 실행 될 때 데이터 모델을 사용 하도록 응용 프로그램을 구성 했습니다.

다음 자습서에서는 UI를 업데이트 하 고, 탐색을 추가 하 고, 데이터베이스에서 데이터를 검색 합니다. 그러면이 자습서에서 만든 엔터티 클래스를 기반으로 데이터베이스가 자동으로 생성 됩니다.

## <a name="additional-resources"></a>추가 리소스

[Entity Framework 개요](https://msdn.microsoft.com/library/bb399567.aspx)   
[ADO.NET Entity Framework에 대 한 초보자 가이드](https://msdn.microsoft.com/data/ee712907)   
[Entity Framework를 사용 하 여 Code First 개발](http://www.msteched.com/2010/Europe/DEV212) (비디오)   
[Code First 관계 흐름 API](https://msdn.microsoft.com/data/hh134698)   
[Code First 데이터 주석](https://msdn.microsoft.com/data/gg193958)  
[Entity Framework의 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [이전](create-the-project.md)
> [다음](ui_and_navigation.md)
