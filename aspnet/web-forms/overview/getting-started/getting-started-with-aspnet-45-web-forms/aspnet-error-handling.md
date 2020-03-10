---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 오류 처리 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 9514142ca50b33470a3f4c033e4f8e319a9ee09b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457025"
---
# <a name="aspnet-error-handling"></a>ASP.NET 오류 처리

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 오류 처리 및 오류 로깅을 포함 하도록 정문 장난감 샘플 응용 프로그램을 수정 합니다. 오류를 처리 하면 응용 프로그램에서 오류를 정상적으로 처리 하 고 오류 메시지를 적절 하 게 표시할 수 있습니다. 오류 로깅을 사용 하면 발생 한 오류를 찾아 수정할 수 있습니다. 이 자습서는 이전 자습서 "URL 라우팅"을 기반으로 하며, 정문 장난감 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- 응용 프로그램의 구성에 전역 오류 처리를 추가 하는 방법입니다.
- 응용 프로그램, 페이지 및 코드 수준에서 오류 처리를 추가 하는 방법입니다.
- 나중에 검토할 수 있도록 오류를 기록 하는 방법입니다.
- 보안을 손상 시 키 지 않는 오류 메시지를 표시 하는 방법입니다.
- 오류 로깅 모듈 및 처리기 (ELMAH) 오류 로깅을 구현 하는 방법입니다.

## <a name="overview"></a>개요

ASP.NET 응용 프로그램은 실행 중에 발생 하는 오류를 일관 된 방식으로 처리할 수 있어야 합니다. ASP.NET은 일관 된 방식으로 응용 프로그램에 오류를 알리는 방법을 제공 하는 CLR (공용 언어 런타임)을 사용 합니다. 오류가 발생 하면 예외가 throw 됩니다. 예외는 응용 프로그램에서 발생 하는 오류, 조건 또는 예기치 않은 동작입니다.

.NET Framework에서 예외는 `System.Exception`에서 상속받은 개체입니다. 예외는 문제가 발생한 코드 영역에서 throw됩니다. 예외는 응용 프로그램에서 예외를 처리 하는 코드를 제공 하는 위치로 호출 스택을 전달 합니다. 응용 프로그램에서 예외를 처리 하지 않는 경우 브라우저는 오류 세부 정보를 표시 하도록 강제 합니다.

모범 사례로, `Try`/의 코드 수준에서 오류를 처리 하 여 코드 내에서 `Finally` 블록을 /`Catch`합니다. 사용자가 발생 하는 상황에서 문제를 해결할 수 있도록 이러한 블록을 추가 합니다. 오류 처리 블록이 오류가 발생 한 위치에서 너무 멀리 떨어져 있는 경우 문제를 해결 하는 데 필요한 정보를 사용자에 게 제공 하는 것이 더 어려워집니다.

### <a name="exception-class"></a>예외 클래스

예외 클래스는 예외가 상속 되는 기본 클래스입니다. 대부분의 예외 개체는 `SystemException` 클래스, `IndexOutOfRangeException` 클래스 또는 `ArgumentNullException` 클래스와 같은 예외 클래스의 일부 파생 클래스의 인스턴스입니다. Exception 클래스에는 발생 한 오류에 대 한 특정 정보를 제공 하는 속성 (예: `StackTrace` 속성, `InnerException` 속성 및 `Message` 속성)이 있습니다.

### <a name="exception-inheritance-hierarchy"></a>예외 상속 계층 구조

런타임에는 예외가 발생할 때 런타임이 throw 하는 `SystemException` 클래스에서 파생 되는 기본 예외 집합이 있습니다. `IndexOutOfRangeException` 클래스 및 `ArgumentNullException` 클래스와 같이 예외 클래스에서 상속 되는 대부분의 클래스는 추가 멤버를 구현 하지 않습니다. 따라서 예외에 대 한 가장 중요 한 정보는 예외 계층 구조, 예외 이름 및 예외에 포함 된 정보에서 찾을 수 있습니다.

### <a name="exception-handling-hierarchy"></a>예외 처리 계층 구조

ASP.NET Web Forms 응용 프로그램에서는 특정 처리 계층 구조를 기반으로 예외를 처리할 수 있습니다. 다음 수준에서 예외를 처리할 수 있습니다.

- 애플리케이션 수준
- 페이지 수준
- 코드 수준

응용 프로그램에서 예외를 처리 하는 경우 예외 클래스에서 상속 된 예외에 대 한 추가 정보를 검색 하 여 사용자에 게 표시할 수 있습니다. 응용 프로그램, 페이지 및 코드 수준 외에도 HTTP 모듈 수준에서 및 IIS 사용자 지정 처리기를 사용 하 여 예외를 처리할 수 있습니다.

### <a name="application-level-error-handling"></a>응용 프로그램 수준 오류 처리

응용 프로그램의 구성을 수정 하거나 응용 프로그램의 *global.asax* 파일에 `Application_Error` 처리기를 추가 하 여 응용 프로그램 수준에서 기본 오류를 처리할 수 있습니다.

*Web.config 파일에* `customErrors` 섹션을 추가 하 여 기본 오류 및 HTTP 오류를 처리할 수 있습니다. `customErrors` 섹션에서는 오류가 발생 했을 때 사용자가 리디렉션되는 기본 페이지를 지정할 수 있습니다. 또한 특정 상태 코드 오류에 대 한 개별 페이지를 지정할 수 있습니다.

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

그러나 구성을 사용 하 여 사용자를 다른 페이지로 리디렉션하는 경우 발생 한 오류에 대 한 세부 정보가 없습니다.

그러나 *global.asax* 파일의 `Application_Error` 처리기에 코드를 추가 하 여 응용 프로그램의 어디에서 나 발생 하는 오류를 트래핑할 수 있습니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>페이지 수준 오류 이벤트 처리

페이지 수준 처리기는 오류가 발생 한 페이지로 사용자를 반환 하지만 컨트롤의 인스턴스가 유지 되지 않으므로 페이지에 더 이상 아무 것도 없습니다. 응용 프로그램의 사용자에 게 오류 정보를 제공 하려면 특히 오류 세부 정보를 페이지에 써야 합니다.

일반적으로 페이지 수준 오류 처리기를 사용 하 여 처리 되지 않은 오류를 기록 하거나 사용자가 유용한 정보를 표시할 수 있는 페이지로 이동 합니다.

이 코드 예제에서는 ASP.NET 웹 페이지의 오류 이벤트에 대 한 처리기를 보여 줍니다. 이 처리기는 페이지에서 `catch` 블록 /`try`내에서 아직 처리 되지 않은 모든 예외를 catch 합니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

오류를 처리 한 후에는 서버 개체 (`HttpServerUtility` 클래스)의 `ClearError` 메서드를 호출 하 여이를 지워야 합니다. 그렇지 않으면 이전에 발생 한 오류가 표시 됩니다.

### <a name="code-level-error-handling"></a>코드 수준 오류 처리

Try-catch 문은 다른 예외에 대 한 처리기를 지정 하는 하나 이상의 catch 절 뒤에 try 블록으로 구성 됩니다. 예외가 throw 되 면 CLR (공용 언어 런타임)에서이 예외를 처리 하는 catch 문을 찾습니다. 현재 실행 중인 메서드에 catch 블록이 없는 경우 CLR에서는 현재 메서드를 호출한 메서드 등을 확인 하 여 호출 스택을 확인 합니다. Catch 블록을 찾을 수 없는 경우 CLR은 처리 되지 않은 예외 메시지를 사용자에 게 표시 하 고 프로그램의 실행을 중지 합니다.

다음 코드 예제에서는 `try`/`catch`/`finally`를 사용 하 여 오류를 처리 하는 일반적인 방법을 보여 줍니다.

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

위의 코드에서 try 블록은 가능한 예외에 대해 보호 해야 하는 코드를 포함 합니다. 블록은 예외가 throw 되거나 블록이 성공적으로 완료 될 때까지 실행 됩니다. `FileNotFoundException` 예외 또는 `IOException` 예외가 발생 하면 실행이 다른 페이지로 전송 됩니다. 그런 다음 오류가 발생 했는지 여부에 관계 없이 finally 블록에 포함 된 코드를 실행 합니다.

## <a name="adding-error-logging-support"></a>오류 로깅 지원 추가

정문 장난감 샘플 응용 프로그램에 오류 처리를 추가 하기 전에 *논리* 폴더에 `ExceptionUtility` 클래스를 추가 하 여 오류 로깅 지원을 추가 합니다. 이렇게 하면 응용 프로그램에서 오류를 처리할 때마다 오류 로그 파일에 오류 정보가 추가 됩니다.

1. *논리* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** -&gt; **새 항목**을 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual C#**  -&gt; **코드** 템플릿 그룹을 선택 합니다. 그런 다음 가운데 목록에서 **클래스**를 선택 하 고 이름을 **ExceptionUtility.cs**로 지정한 다음
3. **추가**를 선택합니다. 새 클래스 파일이 표시 됩니다.
4. 기존 코드를 다음으로 바꿉니다.  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

예외가 발생 하면 `LogException` 메서드를 호출 하 여 예외를 예외 로그 파일에 쓸 수 있습니다. 이 메서드는 예외 개체와 예외의 소스에 대 한 세부 정보를 포함 하는 문자열의 두 매개 변수를 사용 합니다. 예외 로그는 *응용 프로그램\_Data* 폴더의 *오류 로그 .txt* 파일에 기록 됩니다.

### <a name="adding-an-error-page"></a>오류 페이지 추가

정문 장난감 샘플 응용 프로그램에서 한 페이지는 오류를 표시 하는 데 사용 됩니다. 오류 페이지는 사이트 사용자에 게 보안 오류 메시지를 표시 하도록 설계 되었습니다. 그러나 사용자가 코드가 있는 컴퓨터에서 로컬로 제공 되는 HTTP 요청을 작성 하는 개발자 인 경우 오류 페이지에 추가 오류 정보가 표시 됩니다.

1. **솔루션 탐색기** 에서 프로젝트 이름 (**정문 장난감**)을 마우스 오른쪽 단추로 클릭 하 고 **추가** -&gt; **새 항목**을 선택 합니다.   
   **새 항목 추가** 대화 상자가 표시됩니다.
2. 왼쪽의 **Visual C#**  -&gt; **웹** 템플릿 그룹을 선택 합니다. 중간 목록에서 **마스터 페이지로 웹 폼**을 선택 하 고 이름을 **errorpage .aspx**로 바꿉니다.
3. **추가**를 클릭합니다.
4. 마스터 페이지로 *site.master* 파일을 선택 하 고 **확인**을 선택 합니다.
5. 기존 태그를 다음으로 바꿉니다.   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 다음과 같이 표시 되도록 코드 숨김으로 (*ErrorPage.aspx.cs*)의 기존 코드를 바꿉니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

오류 페이지가 표시 되 면 `Page_Load` 이벤트 처리기가 실행 됩니다. `Page_Load` 처리기에서 오류가 처음 처리 된 위치가 결정 됩니다. 그런 다음 서버 개체의 `GetLastError` 메서드를 호출 하 여 마지막으로 발생 한 오류를 확인 합니다. 예외가 더 이상 존재 하지 않는 경우 일반 예외가 생성 됩니다. 그런 다음 HTTP 요청을 로컬로 만든 경우 모든 오류 정보가 표시 됩니다. 이 경우 웹 응용 프로그램을 실행 하는 로컬 컴퓨터에만 이러한 오류 정보가 표시 됩니다. 오류 정보가 표시 된 후 오류가 로그 파일에 추가 되 고 서버에서 오류가 지워집니다.

### <a name="displaying-unhandled-error-messages-for-the-application"></a>응용 프로그램에 대해 처리 되지 않은 오류 메시지 표시

*Web.config 파일에* `customErrors` 섹션을 추가 하면 응용 프로그램 전체에서 발생 하는 단순한 오류를 신속 하 게 처리할 수 있습니다. 404-파일을 찾을 수 없는 경우와 같이 상태 코드 값을 기반으로 오류를 처리 하는 방법을 지정할 수도 있습니다.

#### <a name="update-the-configuration"></a>구성 업데이트

*Web.config 파일에* `customErrors` 섹션을 추가 하 여 구성을 업데이트 합니다.

1. **솔루션 탐색기**에서 정문 장난감 샘플 응용 프로그램의 루트에 있는 *web.config* 파일을 찾아 엽니다.
2. 다음과 같이 `<system.web>` 노드 내의 web.config *파일에* `customErrors` 섹션을 추가 합니다.   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. *Web.config* 파일을 저장합니다.

`customErrors` 섹션에서는 "설정"으로 설정 된 모드를 지정 합니다. 또한 오류가 발생할 때 탐색할 페이지를 응용 프로그램에 알리는 `defaultRedirect`지정 합니다. 또한 페이지를 찾을 수 없을 때 404 오류를 처리 하는 방법을 지정 하는 특정 오류 요소를 추가 했습니다. 이 자습서의 뒷부분에서는 응용 프로그램 수준에서 오류에 대 한 세부 정보를 캡처하는 추가 오류 처리를 추가 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.

1. **F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
 브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
2. 브라우저에 다음 URL을 입력 합니다 **. 포트 번호를 사용** 해야 합니다.  
    `https://localhost:44300/NoPage.aspx`
3. 브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다. 

    ![ASP.NET 오류 처리-페이지를 찾을 수 없음 오류](aspnet-error-handling/_static/image1.png)

없는 *nopage .aspx* 페이지를 요청 하면 추가 세부 정보를 사용할 수 있는 경우 오류 페이지에 간단한 오류 메시지와 자세한 오류 정보가 표시 됩니다. 그러나 사용자가 원격 위치에서 존재 하지 않는 페이지를 요청 하는 경우 오류 페이지는 오류 메시지만 빨간색으로 표시 합니다.

### <a name="including-an-exception-for-testing-purposes"></a>테스트 목적으로 예외 포함

오류가 발생 했을 때 응용 프로그램이 어떻게 작동 하는지 확인 하려면 의도적으로 ASP.NET에서 오류 조건을 만들 수 있습니다. 정문 장난감 샘플 응용 프로그램에서 기본 페이지가 로드 되 면 테스트 예외를 throw 하 여 발생 하는 상황을 확인 합니다.

1. Visual Studio에서 *default.aspx 페이지의* 코드를 엽니다.   
   *Default.aspx.cs* 코드 숨겨진 페이지가 표시 됩니다.
2. `Page_Load` 처리기에서 처리기가 다음과 같이 표시 되도록 코드를 추가 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

다양 한 형식의 예외를 만들 수 있습니다. 위의 코드에서 *default.aspx 페이지가 로드* 되 면 `InvalidOperationException`를 만듭니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램을 실행 하 여 응용 프로그램에서 예외를 처리 하는 방법을 확인할 수 있습니다.

1. **Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램에서 InvalidOperationException를 throw 합니다. 

    > [!NOTE] 
    > 
    > Visual Studio에서 오류의 원인을 확인 하기 위해 코드를 중단 하지 않고 페이지를 표시 하려면 **ctrl +** f 5를 눌러야 합니다.
2. 브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다. 

    ![ASP.NET 오류 처리-오류 페이지](aspnet-error-handling/_static/image2.png)

오류 세부 정보에서 볼 수 있듯이, *web.config 파일의* `customError` 섹션에서 예외를 트래핑 했습니다.

### <a name="adding-application-level-error-handling"></a>응용 프로그램 수준 오류 처리 추가

예외에 대 한 정보를 거의 얻지 못하는 *web.config* 파일의 `customErrors` 섹션을 사용 하 여 예외를 트래핑 하는 대신 응용 프로그램 수준에서 오류를 트래핑 하 고 오류 정보를 검색할 수 있습니다.

1. **솔루션 탐색기**에서 *Global.asax.cs* 파일을 찾아 엽니다.
2. **응용 프로그램\_오류** 처리기를 추가 하 여 다음과 같이 표시 되도록 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

응용 프로그램에서 오류가 발생 하면 `Application_Error` 처리기가 호출 됩니다. 이 처리기에서 마지막 예외를 검색 하 고 검토 합니다. 예외가 처리 되지 않은 경우 예외에 내부 예외 세부 정보 (`InnerException`가 null이 아님)가 포함 된 경우 응용 프로그램은 예외 정보가 표시 되는 오류 페이지로 실행을 전송 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

응용 프로그램을 실행 하 여 응용 프로그램 수준에서 예외를 처리 하 여 제공 된 추가 오류 세부 정보를 볼 수 있습니다.

1. **Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램이 `InvalidOperationException`를 throw 합니다.
2. 브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다. 

    ![ASP.NET 오류 처리-응용 프로그램 수준 오류](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>페이지 수준 오류 처리 추가

페이지의 `@Page` 지시문에 `ErrorPage` 특성을 추가 하거나 페이지의 코드 숨김으로 `Page_Error` 이벤트 처리기를 추가 하 여 페이지에 페이지 수준 오류 처리를 추가할 수 있습니다. 이 섹션에서는 *errorpage .aspx* 페이지로 실행을 전송 하는 `Page_Error` 이벤트 처리기를 추가 합니다.

1. **솔루션 탐색기**에서 *Default.aspx.cs* 파일을 찾아 엽니다.
2. 코드 숨김이 다음과 같이 표시 되도록 `Page_Error` 처리기를 추가 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

페이지에서 오류가 발생 하면 `Page_Error` 이벤트 처리기가 호출 됩니다. 이 처리기에서 마지막 예외를 검색 하 고 검토 합니다. `InvalidOperationException` 발생 하는 경우 `Page_Error` 이벤트 처리기는 예외 정보가 표시 되는 오류 페이지로 실행을 전송 합니다.

#### <a name="running-the-application"></a>응용 프로그램 실행

이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.

1. **Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
 응용 프로그램이 `InvalidOperationException`를 throw 합니다.
2. 브라우저에 표시 된 *Errorpage .aspx* 를 검토 합니다. 

    ![ASP.NET 오류 처리-페이지 수준 오류](aspnet-error-handling/_static/image4.png)
3. 브라우저 창을 닫습니다.

### <a name="removing-the-exception-used-for-testing"></a>테스트에 사용 되는 예외 제거

이 자습서의 앞부분에서 추가한 예외를 발생 시 키 지 않고 정문 장난감 샘플 응용 프로그램이 작동 하도록 허용 하려면 예외를 제거 합니다.

1. *Default.aspx 페이지의* 코드 숨김이 열립니다.
2. 처리기가 다음과 같이 표시 되도록 `Page_Load` 처리기에서 예외를 throw 하는 코드를 제거 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>코드 수준 오류 로깅 추가

이 자습서의 앞부분에서 설명한 것 처럼 try/catch 문을 추가 하 여 코드 섹션을 실행 하 고 발생 한 첫 번째 오류를 처리할 수 있습니다. 이 예에서는 오류 로그 파일에 오류 정보를 기록 하 여 나중에 오류를 검토할 수 있도록 합니다.

1. **솔루션 탐색기**의 *논리* 폴더에서 *PayPalFunctions.cs* 파일을 찾아 엽니다.
2. 코드가 다음과 같이 표시 되도록 `HttpCall` 메서드를 업데이트 합니다.   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

위의 코드는 `ExceptionUtility` 클래스에 포함 된 `LogException` 메서드를 호출 합니다. 이 자습서의 앞부분에 나오는 *논리* 폴더에 *ExceptionUtility.cs* 클래스 파일을 추가 했습니다. `LogException` 메서드는 두 개의 매개 변수를 사용합니다. 첫 번째 매개 변수는 exception 개체입니다. 두 번째 매개 변수는 오류의 원인을 인식 하는 데 사용 되는 문자열입니다.

### <a name="inspecting-the-error-logging-information"></a>오류 로깅 정보 검사

앞에서 설명한 것 처럼 오류 로그를 사용 하 여 먼저 해결할 응용 프로그램의 오류를 확인할 수 있습니다. 물론 오류 로그에 포착 되어 기록 된 오류만 기록 됩니다.

1. **솔루션 탐색기**에서 *응용 프로그램\_Data* 폴더의 *오류 로그 .txt* 파일을 찾아 엽니다.   
 "**모든 파일 표시**" 옵션을 선택 하거나 **솔루션 탐색기** 맨 위에 있는 "**새로 고침**" 옵션을 선택 하 여 *오류 로그 .txt* 파일을 확인 해야 할 수도 있습니다.
2. Visual Studio에 표시 된 오류 로그를 검토 합니다. 

    ![ASP.NET 오류 처리-오류 로그 .txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>안전 오류 메시지

응용 프로그램에서 오류 메시지를 표시 하는 경우 악의적인 사용자가 응용 프로그램을 공격 하는 데 도움이 될 수 있다는 정보를 제공 하지 않는 것이 **중요** 합니다. 예를 들어 응용 프로그램이 데이터베이스에 쓰려고 할 수 없는 경우 사용 중인 사용자 이름을 포함 하는 오류 메시지를 표시 해서는 안 됩니다. 따라서 빨간색의 일반 오류 메시지가 사용자에 게 표시 됩니다. 모든 추가 오류 세부 정보는 로컬 컴퓨터의 개발자 에게만 표시 됩니다.

## <a name="using-elmah"></a>ELMAH 사용

ELMAH (오류 로깅 모듈 및 처리기)는 NuGet 패키지로 ASP.NET 응용 프로그램에 연결 하는 오류 로깅 기능입니다. ELMAH는 다음과 같은 기능을 제공 합니다.

- 처리 되지 않은 예외에 대 한 로깅입니다.
- 기록 처리 되지 않은 예외에 대 한 전체 로그를 볼 수 있는 웹 페이지입니다.
- 기록 된 각 예외의 전체 세부 정보를 볼 수 있는 웹 페이지입니다.
- 발생할 때 각 오류에 대 한 전자 메일 알림
- 로그에서 지난 15 개 오류의 RSS 피드입니다.

ELMAH를 사용 하려면 먼저 설치 해야 합니다. 이는 *NuGet* 패키지 설치 관리자를 사용 하 여 쉽게 수행할 수 있습니다. 이 자습서 시리즈의 앞부분에서 설명한 것 처럼 NuGet은 visual Studio에서 오픈 소스 라이브러리와 도구를 쉽게 설치 하 고 업데이트할 수 있도록 하는 Visual Studio 확장입니다.

1. Visual Studio의 **도구** 메뉴에서 **nuget 패키지 관리자** > **솔루션용 nuget 패키지 관리**를 선택 합니다. 

    ![ASP.NET 오류 처리-솔루션에 대 한 NuGet 패키지 관리](aspnet-error-handling/_static/image6.png)
2. **NuGet 패키지 관리** 대화 상자는 Visual Studio 내에 표시 됩니다.
3. **NuGet 패키지 관리** 대화 상자에서 왼쪽의 **온라인** 을 확장 한 다음 **nuget.org**를 선택 합니다. 그런 다음 온라인에서 사용 가능한 패키지 목록에서 **ELMAH** 패키지를 찾아 설치 합니다. 

    ![ASP.NET 오류 처리-ELMA NuGet 패키지](aspnet-error-handling/_static/image7.png)
4. 패키지를 다운로드 하려면 인터넷에 연결 되어 있어야 합니다.
5. **프로젝트 선택** 대화 상자에서 **WingtipToys** 선택이 선택 되어 있는지 확인 한 다음 **확인**을 클릭 합니다. 

    ![ASP.NET 오류 처리-프로젝트 선택 대화 상자](aspnet-error-handling/_static/image8.png)
6. 필요한 경우 **NuGet 패키지 관리** 대화 상자에서 **닫기** 를 클릭 합니다.
7. Visual Studio에서 열려 있는 모든 파일을 다시 로드 하도록 요청 하는 경우 "**모두 예**"를 선택 합니다.
8. ELMAH 패키지는 프로젝트의 루트에 있는 web.config *파일에* 자신에 대 한 항목을 추가 합니다. Visual Studio에서 수정 된 *web.config* 파일을 다시 로드할지 여부를 묻는 메시지를 표시 하려면 **예**를 클릭 합니다.

이제 ELMAH는 발생 하는 처리 되지 않은 오류를 저장할 준비가 되었습니다.

### <a name="viewing-the-elmah-log"></a>ELMAH 로그 보기

ELMAH 로그는 쉽게 볼 수 있지만 먼저 ELMAH 로그에 기록 되는 처리 되지 않은 예외를 만듭니다.

1. **Ctrl + F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.
2. ELMAH 로그에 처리 되지 않은 예외를 쓰려면 브라우저에서 포트 번호를 사용 하 여 다음 URL로 이동 합니다.  
    `https://localhost:44300/NoPage.aspx` 오류 페이지가 표시 됩니다.
3. ELMAH 로그를 표시 하려면 브라우저에서 포트 번호를 사용 하 여 다음 URL로 이동 합니다.  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 오류 처리-ELMAH 오류 로그](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>요약

이 자습서에서는 응용 프로그램 수준, 페이지 수준 및 코드 수준에서 오류를 처리 하는 방법을 배웠습니다. 또한 이후 검토를 위해 처리 된 오류와 처리 되지 않은 오류를 기록 하는 방법도 배웠습니다. NuGet을 사용 하 여 응용 프로그램에 예외 로깅 및 알림을 제공 하는 ELMAH 유틸리티를 추가 했습니다. 또한 안전 오류 메시지의 중요성에 대해 알아보았습니다.

## <a name="tutorial-series-conclusion"></a>자습서 시리즈 결론

다음에 따라 감사 합니다. 이러한 일련의 자습서를 ASP.NET Web Forms에 더 친숙 하 게 하는 데 도움이 될 것입니다. ASP.NET 4.5 및 Visual Studio 2013에서 사용할 수 있는 Web Forms 기능에 대 한 자세한 내용은 [ASP.NET 및 Web Tools Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)를 참조 하세요. 또한 **다음 단계** 섹션에 언급 된 자습서를 살펴보고 [무료 Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)을 사용해 defintely.

![감사 합니다. Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>다음 단계

Microsoft Azure에 웹 응용 프로그램을 배포 하는 방법에 대 한 자세한 내용은 [멤버 자격, OAuth 및 SQL Database Azure 웹 사이트에 보안 ASP.NET Web Forms 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)를 참조 하세요.

## <a name="free-trial"></a>평가판

[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)  
 웹 사이트를 Microsoft Azure에 게시 하면 시간, 유지 관리 및 비용을 절감할 수 있습니다. Azure에 웹 앱을 배포 하는 빠른 프로세스입니다. 웹 앱을 유지 관리 하 고 모니터링 해야 하는 경우 Azure에서는 다양 한 도구와 서비스를 제공 합니다. Azure에서 데이터, 트래픽, id, 백업, 메시징, 미디어 및 성능을 관리 합니다. 그리고이 모든 것이 매우 비용 효과적인 방법으로 제공 됩니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 상태 모니터링을 사용 하 여 오류 세부 정보 로깅](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>감사의 말

이 자습서 시리즈의 내용에 대해 상당한 기여를 수행한 다음 사용자에 게 감사 합니다.

- [Alberto Poblacion, MVP &amp; MCT, 스페인](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen, 네덜란드](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))
- [Andre Tournier, USA](http://andret503.wordpress.com/)
- Apurva Joshi, Microsoft
- [Bojan 월 Vrhovnik, 슬로베니아](http://twitter.com/bvrhovnik)
- [Bruno Sonnino, 브라질](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))
- [Carlos dos Santos, 브라질](http://www.carloscds.net/)
- [Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))
- [Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Michael 정자, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))
- Mike Pope
- [Mitchel 판매자, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))
- [Paul Cociuba, Microsoft](http://linqto.me/Links/pcociuba)
- [파울로 Ggado, 포르투갈](http://paulomorgado.net/)
- [Pranav Rastogi, Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Am마나트 n, Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra, Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>커뮤니티 기여

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
  MSDN의 Visual Studio 2012 관련 코드 샘플: [정문 장난감 탐색](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  MSDN의 Visual Studio 2012 관련 코드 샘플: [ASP.NET 4.5 Web Forms 자습서 시리즈 Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 기술 대상 참여자 (twitter: @driazevedo)  
  Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [이전](url-routing.md)
