---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
title: ASP.NET 4.5에서 Web Forms의 새로운 기능 | Microsoft Docs
author: rick-anderson
description: ASP.NET Web Forms의 새 버전에는 데이터 작업 시 사용자 환경을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다. 이전 버전의에서 ...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 0a1f88bd-97da-4ed1-86f1-605199dc75a4
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-web-forms-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 301af8ed877b58624e419c04f605c41f27dbdd0c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421925"
---
# <a name="whats-new-in-web-forms-in-aspnet-45"></a>ASP.NET 4.5의 새로운 Web Forms 기능

[웹 캠프 팀](https://twitter.com/webcamps)

> ASP.NET Web Forms의 새 버전에는 데이터 작업 시 사용자 환경을 개선 하는 데 초점을 맞춘 많은 향상 된 기능이 도입 되었습니다.
> 
> 이전 버전의 Web Forms에서 데이터 바인딩을 사용 하 여 개체 멤버의 값을 내보낼 때 데이터 바인딩 식 Bind () 또는 Eval ()을 사용 했습니다. 새 버전의 ASP.NET에서는 새 ItemType 속성을 사용 하 여 컨트롤이 바인딩될 데이터 형식을 선언할 수 있습니다. 이 속성을 설정 하면 강력한 형식의 변수를 사용 하 여 Visual Studio 개발 환경 (예: IntelliSense, 멤버 탐색, 컴파일 시간 검사)의 모든 이점을 받을 수 있습니다.
> 
> 데이터 바인딩된 컨트롤을 사용 하 여 데이터를 선택, 업데이트, 삭제 및 삽입 하는 사용자 지정 메서드를 직접 지정 하 여 페이지 컨트롤과 응용 프로그램 논리 간의 상호 작용을 간소화할 수도 있습니다. 또한 ASP.NET에 모델 바인딩 기능이 추가 되었습니다. 즉, 페이지의 데이터를 메서드 형식 매개 변수에 직접 매핑할 수 있습니다.
> 
> 최신 버전의 Web Forms에서 사용자 입력의 유효성을 검사 하는 것도 더 쉬워졌습니다. 이제 **system.componentmodel** 네임 스페이스의 유효성 검사 특성을 사용 하 여 모델 클래스에 주석을 달고 모든 사이트 컨트롤이 해당 정보를 사용 하 여 사용자 입력의 유효성을 검사 하도록 요청할 수 있습니다. Web Forms의 클라이언트 쪽 유효성 검사는 이제 jQuery와 통합 되어 클리너 클라이언트 쪽 코드와 방해가 되지 않는 JavaScript 기능을 제공 합니다.
> 
> 요청 유효성 검사 영역에서 응용 프로그램의 특정 부분에 대 한 요청 유효성 검사를 더 쉽게 끄거나 무효화 된 요청 데이터를 읽을 수 있도록 기능이 향상 되었습니다.
> 
> HTML5의 새 기능을 활용 하기 위해 Web Forms 서버 컨트롤에 대 한 몇 가지 기능이 향상 되었습니다.
> 
> - TextBox 컨트롤의 TextMode 속성은 email, datetime 등의 새 HTML5 입력 형식을 지원 하도록 업데이트 되었습니다.
> - 이제 FileUpload 컨트롤은이 HTML5 기능을 지 원하는 브라우저에서 여러 파일 업로드를 지원 합니다.
> - 유효성 검사기 컨트롤은 이제 HTML5 입력 요소의 유효성 검사를 지원 합니다.
> - URL을 나타내는 특성이 있는 새 HTML5 요소는 이제 runat =&quot;server&quot;를 지원 합니다. 결과적으로 ~ 연산자와 같이 URL 경로에 ASP.NET 규칙을 사용 하 여 응용 프로그램 루트를 나타낼 수 있습니다. 예를 들어 &lt;video runat =&quot;server&quot; src =&quot;~/Myvideo.er&quot;&gt;&lt;).&gt;
> - HTML5 입력 필드 게시를 지원 하도록 UpdatePanel 컨트롤이 수정 되었습니다.
> 
> 공식 ASP.NET 포털에서 ASP.NET WebForms 4.5: [ASP.NET 4.5 및 Visual Studio 2012의 새로운](../../../../whitepapers/whats-new-in-aspnet-45-and-visual-studio-2012.md#_Toc318097385) 기능에 대 한 추가 예제를 찾을 수 있습니다.
> 
> 모든 샘플 코드와 코드 조각은 [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 강력한 형식의 데이터 바인딩 식 사용
- Web Forms에서 새 모델 바인딩 기능 사용
- 값 공급자를 사용 하 여 페이지 데이터를 코드 숨김이 메서드에 매핑
- 사용자 입력 유효성 검사에 대 한 데이터 주석 사용
- Web Forms에서 jQuery에 대 한 클라이언트 쪽 유효성 검사를 사용 하지 않는 기능 활용
- 세부적인 요청 유효성 검사 구현
- Web Forms에서 비동기 페이지 처리 구현

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

**코드 조각 설치**

편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다. 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.

Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [연습 1: ASP.NET Web Forms의 모델 바인딩](#Exercise1)
2. [연습 2: 데이터 유효성 검사](#Exercise2)
3. [연습 3: ASP.NET의 비동기 페이지 처리 Web Forms](#Exercise3)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Model_Binding_in_ASPNET_Web_Forms"></a>
### <a name="exercise-1-model-binding-in-aspnet-web-forms"></a>연습 1: ASP.NET Web Forms의 모델 바인딩

ASP.NET Web Forms의 새 버전에는 데이터 작업 시 경험 향상에 중점을 둘 수 있는 여러 가지 향상 된 기능이 도입 되었습니다. 이 연습에서는 강력한 형식의 데이터 컨트롤 및 모델 바인딩에 대해 배웁니다.

<a id="Task_1_-_Using_Strongly-Typed_Data-Bindings"></a>
#### <a name="task-1---using-strongly-typed-data-bindings"></a>작업 1-강력한 형식의 데이터 바인딩 사용

이 작업에서는 ASP.NET 4.5에서 사용할 수 있는 강력한 형식의 새 바인딩을 검색 합니다.

1. **원본/Ex1-ModelBinding/Begin/** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **Customers .aspx** 페이지를 엽니다. 주 컨트롤에 번호가 없는 목록을 삽입 하 고 각 고객을 나열 하는 데 repeater 컨트롤을 포함 합니다. 다음 코드에 표시 된 것 처럼 repeater 이름을 **Customersrepeater** 로 설정 합니다.

    이전 버전의 Web Forms에서 데이터 바인딩을 사용 하 여 데이터 바인딩된 개체의 멤버 값을 내보낼 경우 Eval 메서드에 대 한 호출과 함께 데이터 바인딩 식을 사용 하 여 멤버의 이름을 문자열로 전달 하 게 됩니다.

    런타임에 이러한 Eval 호출은 현재 바인딩된 개체에 대 한 리플렉션을 사용 하 여 지정 된 이름의 멤버 값을 읽고 결과를 HTML로 표시 합니다. 이 접근 방식을 사용 하면 임의의 모양의 데이터에 대해 데이터를 매우 쉽게 바인딩할 수 있습니다.

    아쉽게도 멤버 이름에 대 한 IntelliSense, 탐색 지원 (예: 정의로 이동) 및 컴파일 시간 검사를 비롯 하 여 Visual Studio의 다양 한 개발 시간 환경 기능이 손실 됩니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample1.aspx)]
3. **Customers.aspx.cs** 파일을 엽니다.
4. 다음 using 문을 추가 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample2.cs)]
5. **페이지\_Load** 메서드에서 repeater를 고객 목록으로 채우는 코드를 추가 합니다.

    (코드 조각- *Web Forms 랩-Ex01-Customers 데이터 원본 바인딩*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample3.cs)]

    솔루션은 CodeFirst와 함께 EntityFramework를 사용 하 여 데이터베이스를 만들고 액세스 합니다. 다음 코드에서 customersRepeater는 데이터베이스의 모든 고객을 반환 하는 구체화 된 쿼리에 바인딩됩니다.
6. **F5** 키를 눌러 솔루션을 실행 하 고 **고객** 페이지로 이동 하 여 repeater의 동작을 확인 합니다. 솔루션이 CodeFirst를 사용 하는 경우 응용 프로그램을 실행할 때 데이터베이스가 생성 되 고 로컬 SQL Express 인스턴스에 채워집니다.

    ![Repeater를 사용 하 여 고객 나열](whats-new-in-web-forms-in-aspnet-45/_static/image1.png "Repeater를 사용 하 여 고객 나열")

    *Repeater를 사용 하 여 고객 나열*

    > [!NOTE]
    > Visual Studio 2012에서 IIS Express는 기본 웹 개발 서버입니다.
7. 브라우저를 닫고 Visual Studio로 돌아갑니다.
8. 이제 강력한 형식의 바인딩을 사용 하도록 구현을 대체 합니다. **Customers** 페이지를 열고 repeater에서 새 **ItemType** 특성을 사용 하 여 **고객** 유형을 바인딩 유형으로 설정 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample4.aspx)]

    ItemType 속성을 사용 하면 컨트롤이 바인딩될 데이터 형식을 선언 하 고 데이터 바인딩된 컨트롤 내에서 강력한 형식의 바인딩을 사용할 수 있습니다.
9. ItemTemplate 콘텐츠를 다음 코드로 바꿉니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample5.aspx)]

    위의 방법에서 한 가지 단점은 Eval () 및 Bind ()에 대 한 호출이 런타임에 바인딩되어 있으므로 속성 이름을 나타내는 문자열을 전달 한다는 것입니다. 즉, 멤버 이름에 대 한 Intellisense, 코드 탐색 지원 (예: 정의로 이동) 및 컴파일 시간 검사 지원 기능이 없습니다.

    ItemType 속성을 설정 하면 데이터 바인딩 식의 범위에서 **item** 및 **binditem**이라는 두 개의 새 형식화 된 변수가 생성 됩니다. 데이터 바인딩 식에서 이러한 강력한 형식의 변수를 사용 하 여 Visual Studio 개발 환경에 대 한 모든 이점을 얻을 수 있습니다.

    식에 사용 되는 &quot;&quot;는 보안 문제를 방지 하기 위해 출력을 자동으로 HTML 인코딩합니다 (예 **:** 사이트 간 스크립팅 공격). 이 표기법은 응답 작성을 위해 .NET 4부터 사용할 수 있었지만 이제는 데이터 바인딩 식 에서도 사용할 수 있습니다.

    > [!NOTE]
    > 항목 멤버는 단방향 바인딩에 대해 작동 합니다. 양방향 바인딩을 수행 하려면 **Binditem** 멤버를 사용 합니다.

    ![강력한 형식의 바인딩에서 IntelliSense 지원](whats-new-in-web-forms-in-aspnet-45/_static/image2.png "강력한 형식의 바인딩에서 IntelliSense 지원")

    *강력한 형식의 바인딩에서 IntelliSense 지원*
10. **F5** 키를 눌러 솔루션을 실행 하 고 고객 페이지로 이동 하 여 변경 내용이 예상 대로 작동 하는지 확인 합니다.

    ![고객 세부 정보 나열](whats-new-in-web-forms-in-aspnet-45/_static/image3.png "고객 세부 정보 나열")

    *고객 세부 정보 나열*
11. 브라우저를 닫고 Visual Studio로 돌아갑니다.

<a id="Task_2_-_Introducing_Model_Binding_in_Web_Forms"></a>
#### <a name="task-2---introducing-model-binding-in-web-forms"></a>작업 2-Web Forms의 모델 바인딩 소개

이전 버전의 ASP.NET Web Forms에서 데이터를 검색 하 고 업데이트 하는 양방향 데이터 바인딩을 수행 하려는 경우에는 데이터 원본 개체를 사용 해야 했습니다. 개체 데이터 원본, SQL 데이터 원본, LINQ 데이터 원본 등이 될 수 있습니다. 그러나 시나리오에서 데이터를 처리 하는 사용자 지정 코드를 필요로 하는 경우에는 개체 데이터 소스를 사용 해야 하는데 약간의 단점이 있습니다. 예를 들어 복합 형식을 피하고 유효성 검사 논리를 실행할 때 예외를 처리 해야 하는 경우를 예로 들 수 있습니다.

새 버전의 ASP.NET Web Forms 데이터 바인딩된 컨트롤은 모델 바인딩을 지원 합니다. 즉, 데이터 바인딩된 컨트롤에서 직접 select, update, insert 및 delete 메서드를 지정 하 여 코드 숨김이 나 다른 클래스에서 논리를 호출할 수 있습니다.

이에 대해 자세히 알아보려면 GridView를 사용 하 여 새 **SelectMethod** 특성을 사용 하는 제품 범주를 나열 합니다. 이 특성을 사용 하면 GridView 데이터를 검색 하는 메서드를 지정할 수 있습니다.

1. **Products .aspx** 페이지를 열고 **GridView**를 포함 합니다. 강력한 형식의 바인딩을 사용 하 고 정렬과 페이징을 사용 하도록 설정 하려면 아래와 같이 GridView를 구성 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample6.aspx)]
2. 새 **SelectMethod** 특성을 사용 하 여 **getcategories** 메서드를 호출 하 여 데이터를 선택 하도록 GridView를 구성 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample7.aspx)]
3. **Products.aspx.cs** 코드 숨김으로 파일을 열고 다음 using 문을 추가 합니다.

    (코드 조각- *Web Forms Ex01*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample8.cs)]
4. **Products** 클래스에서 private 멤버를 추가 하 고 **ProductsContext**의 새 인스턴스를 할당 합니다. 이 속성은 데이터베이스에 연결할 수 있도록 하는 Entity Framework 데이터 컨텍스트를 저장 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample9.cs)]
5. LINQ를 사용 하 여 범주 목록을 검색 하는 **Getcategories** 메서드를 만듭니다. GridView가 각 범주에 대 한 제품의 양을 표시할 수 있도록 **products** 속성이 쿼리에 포함 됩니다. 메서드는 나중에 페이지 수명 주기에서 실행할 쿼리를 나타내는 원시 IQueryable 개체를 반환 합니다.

    (코드 조각- *Web Forms Lab-Ex01-GetCategories*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample10.cs)]

    > [!NOTE]
    > 이전 버전의 ASP.NET Web Forms에서는 사용자 지정 코드를 작성 하 고 필요한 모든 매개 변수를 수신 하는 데 필요한 개체 데이터 소스 컨텍스트 내에서 고유한 리포지토리 논리를 사용 하 여 정렬 및 페이징을 사용 하도록 설정 합니다. 이제 데이터 바인딩 메서드에서 IQueryable을 반환할 수 있으며이는 실행 되는 쿼리를 나타내므로 ASP.NET는 적절 한 정렬 및 페이징 매개 변수를 추가 하기 위해 쿼리를 수정 해야 합니다.
6. **F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다. GridView가 GetCategories 메서드에 의해 반환 된 범주로 채워지는 것을 볼 수 있습니다.

    ![모델 바인딩을 사용 하 여 GridView 채우기](whats-new-in-web-forms-in-aspnet-45/_static/image4.png "모델 바인딩을 사용 하 여 GridView 채우기")

    *모델 바인딩을 사용 하 여 GridView 채우기*
7. +**SHIFT** 키를 누르고 **f5** 키를 눌러 디버깅을 중지 합니다.

<a id="Task_3_-_Value_Providers_in_Model_Binding"></a>
#### <a name="task-3---value-providers-in-model-binding"></a>작업 3-모델 바인딩의 값 공급자

모델 바인딩을 사용 하면 데이터 바인딩된 컨트롤에서 직접 데이터를 사용 하는 사용자 지정 메서드를 지정할 수 있을 뿐만 아니라 페이지의 데이터를 이러한 메서드의 매개 변수에 매핑할 수도 있습니다. 메서드 매개 변수에서 값 공급자 특성을 사용 하 여 값의 데이터 원본을 지정할 수 있습니다. 다음은 그 예입니다.

- 페이지의 컨트롤
- 쿼리 문자열 값
- 데이터 보기
- 세션 상태
- 쿠키
- 게시 된 양식 데이터
- 상태 보기
- 사용자 지정 값 공급자도 지원 됩니다.

ASP.NET MVC 4를 사용 하는 경우 모델 바인딩 지원이 유사 하다는 것을 알 수 있습니다. 실제로 이러한 기능은 ASP.NET MVC에서 가져온 후 Web Forms에서 사용할 수 있도록 **system.web** 어셈블리로 이동 되었습니다.

이 태스크에서는 모델 바인딩을 사용 하 여 필터 매개 변수를 수신 하는 각 범주에 대 한 제품의 양에 따라 결과를 필터링 하도록 GridView를 업데이트 합니다.

1. **Products .aspx** 페이지로 돌아갑니다.
2. GridView 위쪽에서 **레이블과** **ComboBox** 를 추가 하 여 아래와 같이 각 범주의 제품 수를 선택 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample11.aspx)]
3. 선택한 수의 제품을 포함 하는 범주가 없으면 메시지를 표시 하도록 GridView에 **emptydatatemplate이** 를 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample12.aspx)]
4. **Products.aspx.cs** 코드 숨김으로 열고 다음 using 문을 추가 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample13.cs)]
5. **Getcategories** 메서드를 수정 하 여 정수 **minProductsCount** 인수를 받고 반환 된 결과를 필터링 합니다. 이렇게 하려면 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *Web Forms Lab-Ex01-GetCategories 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample14.cs)]

    **MinProductsCount** 인수의 New **[Control]** 특성은 페이지의 컨트롤을 사용 하 여 해당 값을 채워야 한다는 것을 ASP.NET에 게 알립니다. ASP.NET는 인수 이름 (minProductsCount)과 일치 하는 모든 컨트롤을 검색 하 고 필요한 매핑과 변환을 수행 하 여 매개 변수를 컨트롤 값으로 채웁니다.

    또는 특성은 값을 가져올 컨트롤을 지정할 수 있는 오버 로드 된 생성자를 제공 합니다.

    > [!NOTE]
    > 데이터 바인딩 기능의 목표 중 하나는 페이지 상호 작용을 위해 작성 해야 하는 코드의 양을 줄이는 것입니다. [Control] 값 공급자 외에 다른 모델 바인딩 공급자를 메서드 매개 변수에 사용할 수 있습니다. 그 중 일부는 작업 소개에 나열 되어 있습니다.
6. **F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다. 드롭다운 목록에서 여러 제품을 선택 하 여 이제 GridView가 업데이트 되는 방식을 확인 합니다.

    ![드롭다운 목록 값으로 GridView 필터링](whats-new-in-web-forms-in-aspnet-45/_static/image5.png "드롭다운 목록 값으로 GridView 필터링")

    *드롭다운 목록 값으로 GridView 필터링*
7. 디버깅을 중지합니다.

<a id="Task_4_-_Using_Model_Binding_for_Filtering"></a>
#### <a name="task-4---using-model-binding-for-filtering"></a>작업 4-모델 바인딩을 사용 하 여 필터링

이 태스크에서는 선택한 범주 내의 제품을 표시 하는 두 번째 자식 GridView를 추가 합니다.

1. **Products .aspx** 페이지를 열고 범주 GridView를 업데이트 하 여 선택 단추를 자동 생성 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample15.aspx)]
2. 맨 아래에 **productsGrid** 라는 두 번째 **GridView** 를 추가 합니다. **ItemType** 을 **WebDataKeyNames**, to **ProductId** 로 설정 하 고, **SelectMethod** 를 **getproducts**로 설정 합니다. **AutoGenerateColumns** 을 **false** 로 설정 하 고 ProductId, ProductName, Description 및 UnitPrice 열을 추가 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample16.aspx)]
3. **Products.aspx.cs** 코드 숨겨진 파일을 엽니다. **Getproducts** 메서드를 구현 하 여 범주 GridView에서 범주 ID를 받고 제품을 필터링 합니다. 모델 바인딩에서는 **범주 표에서**선택 된 행을 사용 하 여 매개 변수 값을 설정 합니다. 인수 이름과 컨트롤 이름이 일치 하지 않으므로 컨트롤 값 공급자의 컨트롤 이름을 지정 해야 합니다.

    (코드 조각- *Web Forms 랩-Ex01-GetProducts*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample17.cs)]

    > [!NOTE]
    > 이러한 방법을 사용 하면 이러한 메서드를 보다 쉽게 단위 테스트할 수 있습니다. Web Forms 실행 되 고 있지 않은 단위 테스트 컨텍스트에서 [컨트롤] 특성은 특정 작업을 수행 하지 않습니다.
4. **Products .aspx** 페이지를 열고 products GridView를 찾습니다. Products GridView를 업데이트 하 여 선택한 제품을 편집 하기 위한 링크를 표시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample18.aspx)]
5. **제품 세부 정보 .aspx** 페이지 코드 숨김으로 열고 **selectproduct** 메서드를 다음 코드로 바꿉니다.

    (코드 조각- *Web Forms Lab-Ex01-SelectProduct 메서드*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample19.cs)]

    > [!NOTE]
    > **[QueryString]** 특성은 쿼리 문자열의 productId 매개 변수에서 메서드 매개 변수를 채우는 데 사용 됩니다.
6. **F5** 키를 눌러 사이트 디버깅을 시작 하 고 제품 페이지로 이동 합니다. 범주 GridView에서 범주를 선택 하 고 products GridView가 업데이트 되었는지 확인 합니다.

    ![선택한 범주의 제품 표시](whats-new-in-web-forms-in-aspnet-45/_static/image6.png "선택한 범주의 제품 표시")

    *선택한 범주의 제품 표시*
7. 제품에 대 한 **보기** 링크를 클릭 하 여 제품 세부 정보 .aspx 페이지를 엽니다.

    페이지에서 쿼리 문자열의 productId 매개 변수를 사용 하 여 SelectMethod를 사용 하 여 제품을 검색 하 고 있습니다.

    ![제품 정보 보기](whats-new-in-web-forms-in-aspnet-45/_static/image7.png "제품 정보 보기")

    *제품 정보 보기*

    > [!NOTE]
    > HTML 설명을 입력 하는 기능은 다음 연습에서 구현 됩니다.

<a id="Task_5_-_Using_Model_Binding_for_Update_Operations"></a>
#### <a name="task-5---using-model-binding-for-update-operations"></a>작업 5-업데이트 작업에 모델 바인딩 사용

이전 태스크에서는 주로 데이터를 선택 하기 위해 모델 바인딩을 사용 했습니다 .이 태스크에서는 업데이트 작업에서 모델 바인딩을 사용 하는 방법에 대해 설명 합니다.

범주 GridView를 업데이트 하면 사용자가 범주를 업데이트할 수 있습니다.

1. **Products .aspx** 페이지를 열고 항목 GridView를 업데이트 하 여 편집 단추를 자동 생성 하 고 새 **UpdateMethod** 특성을 사용 하 여 **UpdateCategory** 메서드를 지정 하 여 선택한 항목을 업데이트 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample20.aspx)]

    GridView의 DataKeyNames 특성은 모델 바인딩된 개체를 고유 하 게 식별 하는 멤버 이며, 따라서 update 메서드가 적어도 받아야 하는 매개 변수를 정의 합니다.
2. **Products.aspx.cs** 코드 숨겨진 파일을 열고 **UpdateCategory** 메서드를 구현 합니다. 메서드는 현재 범주를 로드 하 고 GridView에서 값을 채운 다음 범주를 업데이트 하기 위해 범주 ID를 받아야 합니다.

    (코드 조각- *Web Forms 랩-Ex01-UpdateCategory*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample21.cs)]

    Page 클래스의 새 **TryUpdateModel** 메서드는 페이지에 있는 컨트롤의 값을 사용 하 여 모델 개체를 채우는 역할을 담당 합니다. 이 경우 편집 중인 현재 GridView 행에서 업데이트 된 값을 **category** 개체로 바꿉니다.

    > [!NOTE]
    > 다음 연습에서는 개체를 편집할 때 사용자가 입력 한 데이터의 유효성을 검사 하는 데 사용 되는 ModelState. IsValid를 설명 합니다.
3. 사이트를 실행 하 고 제품 페이지로 이동 합니다. 범주를 편집 합니다. 새 이름을 입력 한 다음 **업데이트** 를 클릭 하 여 변경 내용을 유지 합니다.

    ![범주 편집](whats-new-in-web-forms-in-aspnet-45/_static/image8.png "범주 편집")

    *범주 편집*

<a id="Exercise2"></a>

<a id="Exercise_2_Data_Validation"></a>
### <a name="exercise-2-data-validation"></a>연습 2: 데이터 유효성 검사

이 연습에서는 ASP.NET 4.5의 새로운 데이터 유효성 검사 기능에 대해 알아봅니다. Web Forms에서 사용자가 제공 하지 않는 새 유효성 검사 기능을 체크 아웃 합니다. 사용자 입력 유효성 검사를 위해 응용 프로그램 모델 클래스에서 데이터 주석을 사용 하 고, 마지막으로 페이지의 개별 컨트롤에 대 한 요청 유효성 검사를 설정 하거나 해제 하는 방법을 알아봅니다.

<a id="Task_1_-_Unobtrusive_Validation"></a>
#### <a name="task-1---unobtrusive-validation"></a>작업 1-유효성 검사를 하지 않음

유효성 검사기를 포함 하는 복잡 한 데이터를 포함 하는 양식은 페이지에서 너무 많은 JavaScript 코드를 생성 하 여 코드의 약 60%를 나타낼 수 있습니다. 비 표시 유효성 검사를 사용 하도록 설정 하면 HTML 코드가 깔끔하고 tidier 보입니다.

이 섹션에서는 ASP.NET에서 두 구성에 의해 생성 된 HTML 코드를 비교 하는 데 방해가 되는 유효성 검사를 사용 하도록 설정 합니다.

1. **Visual Studio 2012** 을 열고이 랩의 **Source\ex2-validation\begin** 폴더에 있는 **begin** 솔루션을 엽니다. 또는 이전 연습에서 기존 솔루션에 대 한 작업을 계속할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 솔루션 탐색기에서 **Webformslab** 프로젝트 **NuGet 패키지 관리**를 클릭 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **F5** 키를 눌러 웹 응용 프로그램을 시작 합니다. 고객 페이지로 이동 하 여 **새 고객 추가** 링크를 클릭 합니다.
3. 브라우저 페이지를 마우스 오른쪽 단추로 클릭 하 고 **소스 보기** 옵션을 선택 하 여 응용 프로그램에서 생성 된 HTML 코드를 엽니다.

    ![페이지 HTML 코드 표시](whats-new-in-web-forms-in-aspnet-45/_static/image9.png "페이지 HTML 코드 표시")

    *페이지 HTML 코드 표시*
4. 페이지 소스 코드를 스크롤하고 ASP.NET에서 유효성 검사를 수행 하 고 오류 목록을 표시 하기 위해 페이지에 JavaScript 코드 및 데이터 유효성 검사기를 삽입 했는지 확인 합니다.

    ![CustomerDetails 페이지의 유효성 검사 JavaScript 코드](whats-new-in-web-forms-in-aspnet-45/_static/image10.png "CustomerDetails 페이지의 유효성 검사 JavaScript 코드")

    *CustomerDetails 페이지의 유효성 검사 JavaScript 코드*
5. 브라우저를 닫고 Visual Studio로 돌아갑니다.
6. 이제는 조심 스럽게 유효성 검사를 사용 하도록 설정 합니다. **Web.config** 를 열고 **AppSettings** 섹션에서 **validationsettings: UnobtrusiveValidationMode** key를 찾습니다 **.** 키 값을 **WebForms**로 설정 합니다.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample22.xml)]

    > [!NOTE]
    > 일부 페이지에 대해서만 &quot;없는 유효성 검사를 사용 하려는 경우에는이 속성을 **페이지\_로드**&quot; 이벤트에서 설정할 수도 있습니다.
7. **Customerdetails .aspx** 를 열고 **F5** 키를 눌러 웹 응용 프로그램을 시작 합니다.
8. F12 키를 눌러 IE 개발자 도구를 엽니다. 개발자 도구가 열리면 스크립트 탭을 선택 합니다. 메뉴에서 **Customerdetails .aspx** 를 선택 하 고 페이지에서 jQuery를 실행 하는 데 필요한 스크립트가 로컬 사이트에서 브라우저에 로드 되었는지 확인 합니다.

    ![로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드](whats-new-in-web-forms-in-aspnet-45/_static/image11.png "로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드")

    *로컬 IIS 서버에서 직접 jQuery JavaScript 파일 로드*
9. 브라우저를 닫고 Visual Studio로 돌아갑니다. **사이트 마스터** 파일을 다시 열고 **ScriptManager**를 찾습니다. 값 **True**를 사용 하 여 **enablecdn** 속성 특성을 추가 합니다. 그러면 jQuery가 로컬 사이트의 URL이 아닌 온라인 URL에서 강제로 로드 됩니다.
10. Visual Studio에서 **Customerdetails** 를 엽니다. F5 키를 눌러 사이트를 실행 합니다. Internet Explorer가 열리면 F12 키를 눌러 개발자 도구를 엽니다. **스크립트** 탭을 선택 하 고 드롭다운 목록을 살펴봅니다. JQuery JavaScript 파일은 더 이상 로컬 사이트에서 로드 되지 않고 온라인 jQuery CDN에서 로드 됩니다.

    ![CDN에서 jQuery JavaScript 파일 로드](whats-new-in-web-forms-in-aspnet-45/_static/image12.png "CDN에서 jQuery JavaScript 파일 로드")

    *CDN에서 jQuery JavaScript 파일 로드*
11. 브라우저에서 소스 보기 옵션을 사용 하 여 HTML 페이지 소스 코드를 다시 엽니다. ASP.NET 유효성 검사를 사용 하도록 설정 하면 삽입 된 JavaScript 코드가 데이터 \*특성으로 대체 됩니다.

    ![조심 스럽게 유효성 검사 코드](whats-new-in-web-forms-in-aspnet-45/_static/image13.png "조심 스럽게 유효성 검사 코드")

    *조심 스럽게 유효성 검사 코드*

    > [!NOTE]
    > 이 예제에서는 데이터 주석이 있는 유효성 검사 요약이 몇 가지 HTML 및 JavaScript 선 으로만 간소화 되었다는 것을 살펴보았습니다. 이전에는 유효성을 검사 하지 않고 더 많은 유효성 검사 컨트롤을 추가 하면 JavaScript 유효성 검사 코드가 커집니다.

<a id="Task_2_-_Validating_the_Model_with_Data_Annotations"></a>
#### <a name="task-2---validating-the-model-with-data-annotations"></a>작업 2-데이터 주석을 사용 하 여 모델 유효성 검사

ASP.NET 4.5에는 Web Forms에 대 한 데이터 주석 유효성 검사가 도입 되었습니다. 각 입력에 유효성 검사 컨트롤을 사용 하는 대신 이제 모델 클래스에서 제약 조건을 정의 하 고 모든 웹 응용 프로그램에서 사용할 수 있습니다. 이 섹션에서는 새 고객 폼의 유효성을 검사 하기 위해 데이터 주석을 사용 하는 방법에 대해 설명 합니다.

1. **Customerdetail .aspx** 페이지를 엽니다. **EditItemTemplate** 및 **InsertItemTemplate** 섹션의 customer first name 및 Second Name은 requiredfieldvalidator 컨트롤을 사용 하 여 유효성이 검사 됩니다. 각 유효성 검사기는 특정 조건에 연결 되므로 검사할 조건으로 많은 유효성 검사기를 포함 해야 합니다.
2. 고객 모델 클래스의 유효성을 검사 하는 데이터 주석을 추가 합니다. **Model** 폴더에서 **Customer.cs** 클래스를 열고 데이터 주석 특성을 사용 하 여 각 속성을 *데코 레이트* 합니다.

    (코드 조각- *Web Forms 랩-Ex02-데이터 주석*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample23.cs)]

    > [!NOTE]
    > .NET Framework 4.5에서 기존 데이터 주석 컬렉션을 확장 했습니다. 다음은 사용할 수 있는 데이터 주석 중 일부입니다. [크레딧카드], [Phone], [EmailAddress], [Range], [Compare], [Url], [FileExtensions], [Required], [Key], [RegularExpression].
    > 
    > 몇 가지 사용 예는 다음과 같습니다.
    > 
    > [Key]: Specifies that an attribute is the unique identifier
    > 
    > [Range(0.4, 0.5, ErrorMessage=&quot;{Write an error message}&quot;]: Double range
    > 
    > [EmailAddress(ErrorMessage=&quot;Invalid Email&quot;), MaxLength(56)]: Two annotations in the same line.
    > 
    > 각 특성 내에서 고유한 오류 메시지를 정의할 수도 있습니다.
3. **Customerdetails .aspx** 를 열고 FormView 컨트롤의 EditItemTemplate 및 InsertItemTemplate 섹션에서 first 및 last 이름 필드에 대 한 모든 RequiredFieldValidators 검사기를 제거 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample24.aspx)]

    > [!NOTE]
    > 데이터 주석을 사용할 경우의 이점 중 하나는 유효성 검사 논리가 응용 프로그램 페이지에서 중복 되지 않는다는 것입니다. 모델에서 한 번 정의 하 고 데이터를 조작 하는 모든 응용 프로그램 페이지에서 사용 합니다.
4. **Customerdetails .aspx** 코드를 열고 SaveCustomer 메서드를 찾습니다. 이 메서드는 새 고객을 삽입 하 고 FormView 컨트롤 값에서 Customer 매개 변수를 받을 때 호출 됩니다. 페이지 컨트롤과 매개 변수 개체 간의 매핑이 발생 하면 ASP.NET는 모든 데이터 주석 특성에 대해 모델 유효성 검사를 실행 하 고 발생 한 오류 (있는 경우)를 사용 하 여 ModelState 사전을 채웁니다.

    ModelState. IsValid는 유효성 검사를 수행한 후 모델의 모든 필드가 유효한 경우에만 true를 반환 합니다.

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample25.cs)]
5. CustomerDetails 페이지의 끝에 **ValidationSummary** 컨트롤을 추가 하 여 모델 오류 목록을 표시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample26.aspx)]

    **Showmodelstateerrors** 는 ValidationSummary 컨트롤의 새 속성으로, **true**로 설정 된 경우 컨트롤은 modelstate 사전에서 오류를 표시 합니다. 이러한 오류는 데이터 주석 유효성 검사에서 제공 됩니다.
6. **F5** 키를 눌러 웹 응용 프로그램을 실행 합니다. 일부 잘못 된 값으로 양식을 완료 하 고 **저장** 을 클릭 하 여 유효성 검사를 실행 합니다. 아래쪽에서 오류 요약을 확인 합니다.

    ![데이터 주석을 사용한 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image14.png "데이터 주석을 사용한 유효성 검사")

    *데이터 주석을 사용한 유효성 검사*

<a id="Task_3_-_Handling_Custom_Database_Errors_with_ModelState"></a>
#### <a name="task-3---handling-custom-database-errors-with-modelstate"></a>작업 3-ModelState를 사용 하 여 사용자 지정 데이터베이스 오류 처리

이전 버전의 Web Forms에서 너무 긴 문자열 또는 고유 키 위반과 같은 데이터베이스 오류를 처리 하려면 리포지토리 코드에서 예외를 throw 한 다음 코드 숨김으로 예외를 처리 하 여 오류를 표시 하는 것이 포함 될 수 있습니다. 비교적 간단한 작업을 수행 하려면 많은 양의 코드가 필요 합니다.

Web Forms 4.5에서는 ModelState 개체를 사용 하 여 모델 또는 데이터베이스에서 페이지의 오류를 일관 된 방식으로 표시할 수 있습니다.

이 태스크에서는 데이터베이스 예외를 올바르게 처리 하 고 ModelState 개체를 사용 하 여 사용자에 게 적절 한 메시지를 표시 하는 코드를 추가 합니다.

1. 응용 프로그램이 계속 실행 되는 동안 중복 된 값을 사용 하 여 범주 이름을 업데이트 해 봅니다.

    ![중복 된 이름의 범주 업데이트](whats-new-in-web-forms-in-aspnet-45/_static/image15.png "중복 된 이름의 범주 업데이트")

    *중복 된 이름의 범주 업데이트*

    **범주** 열의 &quot;unique&quot; 제약 조건으로 인해 예외가 throw 됩니다.

    ![중복 된 범주 이름에 대 한 예외](whats-new-in-web-forms-in-aspnet-45/_static/image16.png "중복 된 범주 이름에 대 한 예외")

    *중복 된 범주 이름에 대 한 예외*
2. 디버깅을 중지합니다. **Products.aspx.cs** 코드 파일에서 **UpdateCategory** 메서드를 업데이트 하 여 db에서 throw 된 예외를 처리 합니다. SaveChanges () 메서드를 호출 하 고 **Modelstate** 개체에 오류를 추가 합니다.

    새 **TryUpdateModel** 메서드는 사용자가 제공 하는 양식 데이터를 사용 하 여 데이터베이스에서 검색 된 category 개체를 업데이트 합니다.

    (코드 조각- *Web Forms Lab-Ex02-UpdateCategory 처리 오류*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample27.cs)]

    > [!NOTE]
    > 이상적으로는 DbUpdateException의 원인을 파악 하 고 근본 원인이 고유 키 제약 조건에 위반 되는지 확인 해야 합니다.
3. **Products .aspx** 를 열고 범주 GridView 아래에 **ValidationSummary** 컨트롤을 추가 하 여 모델 오류 목록을 표시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample28.aspx)]
4. 사이트를 실행 하 고 제품 페이지로 이동 합니다. 중복 된 값을 사용 하 여 범주 이름을 업데이트 해 보세요.

    예외가 처리 되 고 오류 메시지가 **ValidationSummary** 컨트롤에 표시 됩니다.

    ![중복 된 범주 오류](whats-new-in-web-forms-in-aspnet-45/_static/image17.png "중복 된 범주 오류")

    *중복 된 범주 오류*

<a id="Task_4_-_Request_Validation_in_ASPNET_Web_Forms_45"></a>
#### <a name="task-4---request-validation-in-aspnet-web-forms-45"></a>작업 4-ASP.NET Web Forms 4.5에서 유효성 검사 요청

ASP.NET의 요청 유효성 검사 기능은 XSS (사이트 간 스크립팅) 공격에 대해 특정 수준의 기본 보호를 제공 합니다. 이전 버전의 ASP.NET에서는 요청 유효성 검사를 기본적으로 사용 하도록 설정 했으며 전체 페이지에 대해서만 사용 하지 않도록 설정할 수 있었습니다. ASP.NET Web Forms 새 버전을 사용 하 여 이제 단일 컨트롤에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하거나, 지연 된 요청 유효성 검사를 수행 하거나, 유효성 검사 되지 않은 요청 데이터에 액세스할 수 있습니다 (이렇게 하려면 주의 해야 함).

1. **Ctrl + F5** 키를 눌러 디버깅 하지 않고 사이트를 시작 하 고 제품 페이지로 이동 합니다. 범주를 선택한 다음 제품의 **편집** 링크를 클릭 합니다.
2. 잠재적으로 위험한 콘텐츠를 포함 하는 설명을 입력 합니다 (예를 들어 HTML 태그 포함). 요청 유효성 검사로 인해 throw 되는 예외를 확인 합니다.

    ![잠재적으로 위험한 콘텐츠가 있는 제품 편집](whats-new-in-web-forms-in-aspnet-45/_static/image18.png "잠재적으로 위험한 콘텐츠가 있는 제품 편집")

    *잠재적으로 위험한 콘텐츠가 있는 제품 편집*

    ![요청 유효성 검사로 인해 예외가 발생 했습니다.](whats-new-in-web-forms-in-aspnet-45/_static/image19.png "요청 유효성 검사로 인해 예외가 발생 했습니다.")

    *요청 유효성 검사로 인해 예외가 발생 했습니다.*
3. 페이지를 닫고 Visual Studio에서 **SHIFT + f** 5를 눌러 디버깅을 중지 합니다.
4. **제품 세부 정보 .aspx** 페이지를 열고 **설명** 텍스트 상자를 찾습니다.
5. 새 **ValidateRequestMode** 속성을 텍스트 상자에 추가 하 고 해당 값을 **사용 안 함**으로 설정 합니다.

    새 **ValidateRequestMode** 특성을 사용 하면 각 컨트롤에서 요청 유효성 검사 세부적으로을 사용 하지 않도록 설정할 수 있습니다. HTML 코드를 받을 수 있지만 페이지의 나머지 부분에 대해 유효성 검사가 작동 하는 것을 유지 하려는 경우에 유용 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample29.aspx)]
6. **F5** 키를 눌러 웹 응용 프로그램을 실행 합니다. 제품 편집 페이지를 다시 열고 HTML 태그를 포함 한 제품 설명을 작성 합니다. 이제 설명에 HTML 콘텐츠를 추가할 수 있습니다.

    ![제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.](whats-new-in-web-forms-in-aspnet-45/_static/image20.png "제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.")

    *제품 설명에 대 한 요청 유효성 검사를 사용 하지 않습니다.*

    > [!NOTE]
    > 프로덕션 응용 프로그램에서는 사용자가 입력 한 HTML 코드를 삭제 하 여 안전한 HTML 태그만 입력 되도록 해야 합니다. 예를 들어 &lt;스크립트&gt; 태그는 없습니다. 이를 위해 [Microsoft 웹 보호 라이브러리](https://www.nuget.org/packages/AntiXSS)를 사용할 수 있습니다.
7. 제품을 다시 편집 합니다. 이름 필드에 HTML 코드를 입력 하 고 **저장**을 클릭 합니다. 요청 유효성 검사는 설명 필드에 대해서만 사용할 수 있으며, 나머지 필드는 잠재적으로 위험한 콘텐츠에 대해 유효성 검사를 계속 합니다.

    ![나머지 필드에서 요청 유효성 검사 사용](whats-new-in-web-forms-in-aspnet-45/_static/image21.png "나머지 필드에서 요청 유효성 검사 사용")

    *나머지 필드에서 요청 유효성 검사 사용*

    ASP.NET Web Forms 4.5은 요청 유효성 검사를 지연 수행 하기 위한 새 요청 유효성 검사 모드를 포함 합니다. 요청 유효성 검사 모드를 **4.5**로 설정 하 고 코드 조각이 *&quot;&quot;요청*에 액세스 하는 경우 ASP.NET 4.5의 요청 유효성 검사는 폼 컬렉션의 특정 요소에 대 한 요청 유효성 검사만 트리거합니다.

    또한 ASP.NET 4.5에는 이제 Microsoft의 XSS 라이브러리 v 4.0의 핵심 인코딩 루틴이 포함 되어 있습니다. XSS 방지 인코딩 루틴은 새 Antixssencoder 사용할 **네임 스페이스에 있는 새** 형식에 의해 구현 됩니다. *Antixssencoder 사용할*를 사용 하도록 구성 된 **encoderType** 매개 변수를 사용 하면 ASP.NET 내의 모든 출력 인코딩이 자동으로 새 인코딩 루틴을 사용 합니다.
8. ASP.NET 4.5 요청 유효성 검사는 데이터 요청에 대 한 유효성 검사 되지 않은 액세스도 지원 합니다. ASP.NET 4.5는 **유효성 검사**라는 **HttpRequest** 개체에 새 컬렉션 속성을 추가 합니다. HttpRequest로 이동 하면 폼, QueryStrings, 쿠키, Url 등을 비롯 한 요청 데이터의 모든 일반적인 부분에 액세스할 수 있습니다 **.**

    ![유효성 검사 개체](whats-new-in-web-forms-in-aspnet-45/_static/image22.png "유효성 검사 개체")

    *유효성 검사 개체*

    > [!NOTE]
    > **HttpRequest. 유효성 검사 속성은 주의 해 서 사용 하세요.** 원시 요청 데이터에 대 한 사용자 지정 유효성 검사를 신중 하 게 수행 하 여 위험한 텍스트가 라운드트립 하 고 확실 하지 않은 고객에 게 다시 렌더링 되지 않도록 합니다.

<a id="Exercise3"></a>

<a id="Exercise_3_Asynchronous_Page_Processing_in_ASPNET_Web_Forms"></a>
### <a name="exercise-3-asynchronous-page-processing-in-aspnet-web-forms"></a>연습 3: ASP.NET의 비동기 페이지 처리 Web Forms

이 연습에서는 ASP.NET Web Forms의 새로운 비동기 페이지 처리 기능에 대해 소개 합니다.

<a id="Task_1_-_Updating_the_Product_Details_Page_to_Upload_and_Show_Images"></a>
#### <a name="task-1---updating-the-product-details-page-to-upload-and-show-images"></a>작업 1-제품 세부 정보 페이지를 업데이트 하 여 이미지 업로드 및 표시

이 작업에서는 제품 세부 정보 페이지를 업데이트 하 여 사용자가 제품에 대 한 이미지 URL을 지정 하 고이를 읽기 전용 보기에 표시할 수 있도록 합니다. 지정 된 이미지를 동기적으로 다운로드 하 여 로컬 복사본을 만듭니다. 다음 태스크에서는이 구현을 업데이트 하 여 비동기 방식으로 작동 하도록 합니다.

1. **Visual Studio 2012** 을 열고이 랩의 폴더에서 **Source\ex3-async\begin** 에 있는 **시작** 솔루션을 로드 합니다. 또는 이전 연습에서 기존 솔루션에 대 한 작업을 계속할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 솔루션 탐색기에서 **Webformslab** 프로젝트를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. 제품 **세부 정보 .aspx** 페이지 소스를 열고 FormView의 ItemTemplate에 필드를 추가 하 여 제품 이미지를 표시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample30.aspx)]
3. 필드를 추가 하 여 FormView의 EditTemplate에서 이미지 URL을 지정 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample31.aspx)]
4. **ProductDetails.aspx.cs** 코드 숨겨진 파일을 열고 다음 네임 스페이스 지시문을 추가 합니다.

    (코드 조각- *Web Forms Ex03*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample32.cs)]
5. 로컬 **이미지** 폴더에 원격 이미지를 저장 하는 **UpdateProductImage** 메서드를 만들고 새 이미지 위치 값을 사용 하 여 product 엔터티를 업데이트 합니다.

    (코드 조각- *Web Forms 랩-Ex03-UpdateProductImage*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample33.cs)]
6. **UpdateProductImage** 메서드를 호출 하도록 **updateproduct** 메서드를 업데이트 합니다.

    (코드 조각- *Web Forms Lab-Ex03-UpdateProductImage Call*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample34.cs)]
7. 응용 프로그램을 실행 하 고 제품에 대 한 이미지를 업로드 합니다. 예를 들어 Office 클립 예술에서 다음 이미지 URL을 사용할 수 있습니다. [ [http://officeimg.vo.msecnd.net/images/MB900437099.jpg](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)](http://officeimg.vo.msecnd.net/images/MB900437099.jpg)

    ![제품에 대 한 이미지 설정](whats-new-in-web-forms-in-aspnet-45/_static/image23.png "제품에 대 한 이미지 설정")

    *제품에 대 한 이미지 설정*

<a id="Task_2_-_Adding_Asynchronous_Processing_to_the_Product_Details_Page"></a>
#### <a name="task-2---adding-asynchronous-processing-to-the-product-details-page"></a>작업 2-제품 세부 정보 페이지에 비동기 처리 추가

이 작업에서는 제품 세부 정보 페이지를 업데이트 하 여 비동기 방식으로 작동 하도록 합니다. ASP.NET 4.5 비동기 페이지 처리를 사용 하 여 장기 실행 작업 (이미지 다운로드 프로세스)을 개선 합니다.

웹 응용 프로그램의 비동기 메서드를 사용 하 여 ASP.NET 스레드 풀을 사용 하는 방법을 최적화할 수 있습니다. ASP.NET의 스레드 풀에는 요청에 참여 하기 위한 스레드 수가 제한 되어 있기 때문에 모든 스레드가 사용 중이면 ASP.NET가 새 요청을 거부 하 고 응용 프로그램 오류 메시지를 전송 하 여 사이트를 사용할 수 없게 됩니다.

웹 사이트에서 시간이 오래 걸리는 작업은 할당 된 스레드를 오랫동안 사용 하기 때문에 비동기 프로그래밍에 적합 합니다. 여기에는 장기 실행 요청, 데이터베이스를 쿼리하거나 외부 웹 서버에 액세스 하는 경우와 같이 오프 라인 작업을 필요로 하는 다양 한 요소 및 페이지가 있는 페이지가 포함 됩니다. 이러한 작업에 비동기 메서드를 사용 하는 경우 페이지가 처리 되는 동안 스레드가 해제 되 고 스레드 풀로 반환 되 고 새 페이지 요청에 참석 하는 데 사용 될 수 있다는 장점이 있습니다. 즉, 페이지는 스레드 풀의 한 스레드에서 처리를 시작 하 고 비동기 처리가 완료 된 후 다른 스레드에서 처리를 완료할 수 있습니다.

1. **제품 세부 정보 .aspx** 페이지를 엽니다. **Page** 요소에 **Async** 특성을 추가 하 고 **true**로 설정 합니다. 이 특성은 IHttpAsyncHandler 인터페이스를 구현 하도록 ASP.NET에 지시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample35.aspx)]
2. 페이지 아래쪽에 레이블을 추가 하 여 페이지를 실행 하는 스레드에 대 한 세부 정보를 표시 합니다.

    [!code-aspx[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample36.aspx)]
3. **ProductDetails.aspx.cs** 를 열고 다음 네임 스페이스 지시문을 추가 합니다.

    (코드 조각- *Web Forms Ex03-네임 스페이스 2*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample37.cs)]
4. **UpdateProductImage** 메서드를 수정 하 여 비동기 작업으로 이미지를 다운로드 합니다. **WebClient** **DownloadFile** 메서드를 **DownloadFileTaskAsync** 메서드로 바꾸고 **wait** 키워드를 포함 합니다.

    (코드 조각- *Web Forms Lab-Ex03-UpdateProductImage Async*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample38.cs)]

    RegisterAsyncTask는 다른 스레드에서 실행할 새 페이지 비동기 작업을 등록 합니다. 실행할 태스크 (t)를 사용 하 여 람다 식을 받습니다. **DownloadFileTaskAsync** 메서드의 **wait** 키워드는 메서드 나머지를 **DownloadFileTaskAsync** 메서드가 완료 된 후 비동기식으로 호출 되는 콜백으로 변환 합니다. ASP.NET는 모든 HTTP 요청 원래 값을 자동으로 유지 하 여 메서드 실행을 다시 시작 합니다. .NET 4.5의 새로운 비동기 프로그래밍 모델을 사용 하면 동기 코드와 매우 비슷한 비동기 코드를 작성 하 고 컴파일러에서 콜백 함수 또는 연속 코드의 복잡 한 문제를 처리할 수 있습니다.
    > [!NOTE]
    > RegisterAsyncTask 및 PageAsyncTask은 .NET 2.0부터 이미 사용할 수 있습니다. Wait 키워드는 .NET 4.5 비동기 프로그래밍 모델에서 새로 사용 되며 .NET WebClient 개체의 새 TaskAsync 메서드와 함께 사용할 수 있습니다.
5. 코드가 시작 되 고 실행이 완료 된 스레드를 표시 하는 코드를 추가 합니다. 이렇게 하려면 **UpdateProductImage** 메서드를 다음 코드로 업데이트 합니다.

    (코드 조각- *Web Forms 랩-Ex03-스레드 표시*)

    [!code-csharp[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample39.cs)]
6. **웹 사이트의 web.config 파일을** 엽니다. 다음 appSetting 변수를 추가 합니다.

    [!code-xml[Main](whats-new-in-web-forms-in-aspnet-45/samples/sample40.xml)]
7. **F5** 키를 눌러 응용 프로그램을 실행 하 고 제품에 대 한 이미지를 업로드 합니다. 코드가 시작 되 고 완료 된 스레드 ID가 다를 수 있습니다. 비동기 작업은 ASP.NET 스레드 풀에서 별도의 스레드에서 실행 되기 때문입니다. 태스크가 완료 되 면 ASP.NET는 작업을 다시 큐에 넣고 사용 가능한 스레드를 할당 합니다.

    ![비동기적으로 이미지 다운로드](whats-new-in-web-forms-in-aspnet-45/_static/image24.png "비동기적으로 이미지 다운로드")

    *비동기적으로 이미지 다운로드*

> [!NOTE]
> 또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 따라 Azure에이 응용 프로그램을 배포할 수 있습니다.

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서는 다음 개념에 대해 설명 하 고 보여 줍니다.

- 강력한 형식의 데이터 바인딩 식 사용
- Web Forms에서 새 모델 바인딩 기능 사용
- 값 공급자를 사용 하 여 페이지 데이터를 코드 숨김이 메서드에 매핑
- 사용자 입력 유효성 검사에 대 한 데이터 주석 사용
- Web Forms에서 jQuery에 대 한 클라이언트 쪽 유효성 검사를 사용 하지 않는 기능 활용
- 세부적인 요청 유효성 검사 구현
- Web Forms에서 비동기 페이지 처리 구현

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> 제품 &quot;검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](whats-new-in-web-forms-in-aspnet-45/_static/image25.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](whats-new-in-web-forms-in-aspnet-45/_static/image26.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](whats-new-in-web-forms-in-aspnet-45/_static/image27.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](whats-new-in-web-forms-in-aspnet-45/_static/image28.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](whats-new-in-web-forms-in-aspnet-45/_static/image29.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 azure Portal에서 새 웹 사이트를 만들고 랩에 따라 얻은 응용 프로그램을 게시 하 여 Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-azure-portal"></a>작업 1-Azure 포털에서 새 웹 사이트 만들기

1. [Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 다음 트래픽이 증가 함에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image30.png "Windows Azure Portal에 로그온 합니다.")

    *포털 로그온*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image31.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Azure는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 완료 된 웹 응용 프로그램을 Azure에 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image32.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](whats-new-in-web-forms-in-aspnet-45/_static/image33.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](whats-new-in-web-forms-in-aspnet-45/_static/image34.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](whats-new-in-web-forms-in-aspnet-45/_static/image35.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Azure에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 Azure에 웹 응용 프로그램을 게시 하기 위해 이러한 프로그램의 구성을 자동화 하는 게시 프로필 읽기를 지원 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image36.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Azure에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image37.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL database** | **Servers** | **서버 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](whats-new-in-web-forms-in-aspnet-45/_static/image38.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](whats-new-in-web-forms-in-aspnet-45/_static/image39.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](whats-new-in-web-forms-in-aspnet-45/_static/image40.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](whats-new-in-web-forms-in-aspnet-45/_static/image41.png)

    *변경 내용 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image42.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](whats-new-in-web-forms-in-aspnet-45/_static/image43.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](whats-new-in-web-forms-in-aspnet-45/_static/image44.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](whats-new-in-web-forms-in-aspnet-45/_static/image45.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름을 입력 합니다.

     ![대상 연결 문자열 구성](whats-new-in-web-forms-in-aspnet-45/_static/image46.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](whats-new-in-web-forms-in-aspnet-45/_static/image47.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](whats-new-in-web-forms-in-aspnet-45/_static/image48.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](whats-new-in-web-forms-in-aspnet-45/_static/image49.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 C: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](whats-new-in-web-forms-in-aspnet-45/_static/image50.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](whats-new-in-web-forms-in-aspnet-45/_static/image51.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image52.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](whats-new-in-web-forms-in-aspnet-45/_static/image53.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image54.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](whats-new-in-web-forms-in-aspnet-45/_static/image55.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
