---
uid: single-page-application/overview/introduction/knockoutjs-template
title: '단일 페이지 응용 프로그램: KnockoutJS 템플릿 | Microsoft Docs'
author: MikeWasson
description: 템플릿 녹아웃
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467321"
---
# <a name="single-page-application-knockoutjs-template"></a>단일 페이지 응용 프로그램: KnockoutJS 템플릿

[Mike Wasson](https://github.com/MikeWasson)

> 녹아웃 MVC 템플릿은 ASP.NET 및 Web Tools 2012.2의 일부입니다.
> 
> [다운로드 ASP.NET 및 Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=282650)

ASP.NET 및 Web Tools 2012.2 업데이트에는 ASP.NET MVC 4 용 SPA (단일 페이지 응용 프로그램) 템플릿이 포함 되어 있습니다. 이 템플릿은 대화형 클라이언트 쪽 웹 앱을 신속 하 게 빌드할 수 있도록 설계 되었습니다.

SPA (단일 페이지 응용 프로그램)는 단일 HTML 페이지를 로드 한 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반적인 용어입니다. 초기 페이지를 로드 한 후 SPA는 AJAX 요청을 통해 서버와 통신 합니다.

![](knockoutjs-template/_static/image1.png)

AJAX는 새로운 것은 아니지만 오늘날에는 크고 정교한 SPA 응용 프로그램을 쉽게 빌드하고 유지 관리할 수 있는 JavaScript 프레임 워크가 있습니다. 또한 HTML 5와 CSS3을 통해 풍부한 Ui를 보다 쉽게 만들 수 있습니다.

시작 하려면 SPA 템플릿이 샘플 "할 일 목록" 응용 프로그램을 만듭니다. 이 자습서에서는 템플릿 둘러보기를 살펴보겠습니다. 먼저 할 일 목록 응용 프로그램 자체를 확인 하 고 작동 하는 기술 부분을 검토 합니다.

## <a name="create-a-new-spa-template-project"></a>새 SPA 템플릿 프로젝트 만들기

요구 사항:

- 웹 용 Visual Studio 2012 또는 Visual Studio Express 2012
- ASP.NET 웹 도구 2012.2 업데이트를 업데이트 합니다. [여기](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)에 업데이트를 설치할 수 있습니다.

Visual Studio를 시작 하 고 시작 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.

![](knockoutjs-template/_static/image2.png)

**새 프로젝트** 마법사에서 **단일 페이지 응용 프로그램**을 선택 합니다.

![](knockoutjs-template/_static/image3.png)

F5를 눌러 애플리케이션을 빌드 및 실행합니다. 응용 프로그램을 처음 실행 하면 로그인 화면이 표시 됩니다.

![](knockoutjs-template/_static/image4.png)

&quot;등록&quot; 링크를 클릭 하 고 새 사용자를 만듭니다.

![](knockoutjs-template/_static/image5.png)

로그인 한 후 응용 프로그램은 두 개의 항목이 포함 된 기본 Todo 목록을 만듭니다. "Todo 목록 추가"를 클릭 하 여 새 목록을 추가할 수 있습니다.

![](knockoutjs-template/_static/image6.png)

목록의 이름을 바꾸고, 항목을 목록에 추가 하 고, 체크 인 합니다. 또한 항목을 삭제 하거나 전체 목록을 삭제할 수 있습니다. 변경 내용은 서버에 있는 데이터베이스에 자동으로 유지 됩니다 (실제로 응용 프로그램을 실행 하 고 있기 때문에이 시점에서 LocalDB).

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA 템플릿의 아키텍처

이 다이어그램에서는 응용 프로그램의 기본 구성 요소를 보여 줍니다.

![](knockoutjs-template/_static/image8.png)

서버 쪽에서 ASP.NET MVC는 HTML을 사용 하 고 폼 기반 인증도 처리 합니다.

ASP.NET Web API은 가져오기, 만들기, 업데이트 및 삭제를 포함 하 여 ToDoLists 및 ToDoItems와 관련 된 모든 요청을 처리 합니다. 클라이언트는 JSON 형식의 Web API를 사용 하 여 데이터를 교환 합니다.

EF (Entity Framework)는 O/RM 계층입니다. 개체 지향 세계 ASP.NET와 기본 데이터베이스 간에 중재. 데이터베이스는 LocalDB를 사용 하지만 web.config 파일에서이를 변경할 수 있습니다. 일반적으로 로컬 개발용으로 LocalDB를 사용 하 고 EF code-first 마이그레이션을 사용 하 여 서버의 SQL database에 배포 합니다.

클라이언트 쪽에서, 녹아웃 .js 라이브러리는 AJAX 요청에서 페이지 업데이트를 처리 합니다. 녹아웃은 데이터 바인딩을 사용 하 여 페이지를 최신 데이터와 동기화 합니다. 이렇게 하면 JSON 데이터를 안내 하는 코드를 작성 하 여 DOM을 업데이트 하지 않아도 됩니다. 대신 데이터를 표시 하는 방법을 녹아웃 하는 선언적 특성을 HTML에 배치 합니다.

이 아키텍처의 큰 장점은 프레젠테이션 계층을 응용 프로그램 논리와 분리 하는 것입니다. 웹 페이지를 표시 하는 방법에 대해 알지 못해도 웹 API 부분을 만들 수 있습니다. 클라이언트 쪽에서 해당 데이터를 나타내는 "모델 보기"를 만들고 뷰 모델에서 녹아웃을 사용 하 여 HTML에 바인딩합니다. 이렇게 하면 뷰 모델을 변경 하지 않고 HTML을 쉽게 변경할 수 있습니다. (나중에 약간의 녹아웃을 살펴보겠습니다.)

## <a name="models"></a>모델

Visual Studio 프로젝트에서 모델 폴더는 서버 쪽에서 사용 되는 모델을 포함 합니다. 클라이언트 쪽에도 모델이 있습니다. 여기에 대해서도 살펴보겠습니다.

![](knockoutjs-template/_static/image9.png)

**TodoItem, TodoList**

Entity Framework Code First에 대 한 데이터베이스 모델입니다. 이러한 모델에는 서로를 가리키는 속성이 있습니다. `ToDoList`는 ToDoItems의 컬렉션을 포함 하 고 각 `ToDoItem`는 부모 ToDoList에 대 한 참조를 포함 합니다. 이러한 속성을 탐색 속성 이라고 하며, 할 일 대 다 관계의 할 일 목록 및 할 일 항목을 나타냅니다.

또한 `ToDoItem` 클래스는 **[ForeignKey]** 특성을 사용 하 여 `ToDoListId` `ToDoList` 테이블의 외래 키 임을 지정 합니다. 이렇게 하면 데이터베이스에 foreign key 제약 조건이 추가 됩니다.

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

이러한 클래스는 클라이언트에 전송 되는 데이터를 정의 합니다. "DTO"은 "데이터 전송 개체"를 나타냅니다. DTO는 엔터티가 JSON으로 serialize 되는 방법을 정의 합니다. 일반적으로 Dto를 사용 하는 몇 가지 이유가 있습니다.

- Serialize 되는 속성을 제어 합니다. DTO에는 도메인 모델의 속성 하위 집합이 포함 될 수 있습니다. 중요 한 데이터를 숨기 거 나 단순히 보내는 데이터의 양을 줄이기 위해 보안상의 이유로이 작업을 수행할 수 있습니다.
- 데이터의 모양 (예:)을 변경 하 여 더 복잡 한 데이터 구조를 평면화 합니다.
- 비즈니스 논리를 DTO으로 유지 합니다 (문제 분리).
- 어떤 이유로 도메인 모델을 직렬화 할 수 없는 경우 예를 들어 순환 참조는 개체를 serialize 할 때 문제를 일으킬 수 있습니다. 웹 API에서이 문제를 처리 하는 방법이 있습니다 ( [순환 개체 참조 처리](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)참조). 하지만 DTO를 사용 하면 문제가 해결 되지 않습니다.

SPA 템플릿에서 Dto는 도메인 모델과 동일한 데이터를 포함 합니다. 그러나 탐색 속성의 순환 참조를 방지 하 고 일반 DTO 패턴을 보여 주므로 여전히 유용 합니다.

**AccountModels.cs**

이 파일에는 사이트 멤버 자격에 대 한 모델이 포함 되어 있습니다. `UserProfile` 클래스는 멤버 자격 데이터베이스의 사용자 프로필에 대 한 스키마를 정의 합니다. 이 경우 유일한 정보는 사용자 ID와 사용자 이름입니다. 이 파일의 다른 모델 클래스를 사용 하 여 사용자 등록 및 로그인 양식을 만듭니다.

## <a name="entity-framework"></a>Entity Framework

SPA 템플릿에서 EF Code First를 사용 합니다. Code First 개발에서 코드에 모델을 먼저 정의한 다음 EF는 모델을 사용 하 여 데이터베이스를 만듭니다. 또한 기존 데이터베이스 ([Database First](https://msdn.microsoft.com/data/jj206878.aspx))와 함께 EF를 사용할 수 있습니다.

모델 폴더의 `TodoItemContext` 클래스는 **DbContext**에서 파생 됩니다. 이 클래스는 모델과 EF 간의 "붙이기"를 제공 합니다. `TodoItemContext` `ToDoItem` 컬렉션과 `TodoList` 컬렉션을 보유 합니다. 데이터베이스를 쿼리하려면 이러한 컬렉션에 대해 LINQ 쿼리를 작성 하기만 하면 됩니다. 예를 들어 "Alice" 사용자에 대 한 모든 할 일 목록을 선택할 수 있는 방법은 다음과 같습니다.

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

컬렉션에 새 항목을 추가 하거나 항목을 업데이트 하거나 컬렉션에서 항목을 삭제 하 고 변경 내용을 데이터베이스에 유지할 수도 있습니다.

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 컨트롤러

ASP.NET Web API에서 컨트롤러는 HTTP 요청을 처리 하는 개체입니다. 앞서 언급 했 듯이 SPA 템플릿에서는 Web API를 사용 하 여 `ToDoList` 및 `ToDoItem` 인스턴스에서 CRUD 작업을 사용 하도록 설정 합니다. 컨트롤러는 솔루션의 Controllers 폴더에 있습니다.

![](knockoutjs-template/_static/image10.png)

- `TodoController`: 할 일 항목에 대 한 HTTP 요청을 처리 합니다.
- `TodoListController`: 할 일 목록에 대 한 HTTP 요청을 처리 합니다.

웹 API가 컨트롤러 이름에 대 한 URI 경로와 일치 하므로 이러한 이름은 중요 합니다. 웹 API가 컨트롤러에 HTTP 요청을 라우팅하는 방법을 알아보려면 [ASP.NET Web API의 라우팅](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.)

`ToDoListController` 클래스를 살펴보겠습니다. 단일 데이터 멤버를 포함 합니다.

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

`TodoItemContext`는 앞에서 설명한 대로 EF와 통신 하는 데 사용 됩니다. 컨트롤러의 메서드는 CRUD 작업을 구현 합니다. Web API는 다음과 같이 클라이언트의 HTTP 요청을 컨트롤러 메서드로 매핑합니다.

| HTTP 요청 | Controller 메서드 | Description |
| --- | --- | --- |
| GET /api/todo | `GetTodoLists` | 할 일 목록 컬렉션을 가져옵니다. |
| GET/api/todo/*id* | `GetTodoList` | ID 별로 할 일 목록을 가져옵니다. |
| PUT/api/todo/*id* | `PutTodoList` | 할 일 목록을 업데이트 합니다. |
| POST /api/todo | `PostTodoList` | 새 할 일 목록을 만듭니다. |
| /Api/todo/*ID* 삭제 | `DeleteTodoList` | 할 일 목록을 삭제 합니다. |

일부 작업의 Uri에는 ID 값에 대 한 자리 표시 자가 포함 되어 있습니다. 예를 들어 ID가 42 인 목록에서 목록을 삭제 하려면 URI가 `/api/todo/42`됩니다.

CRUD 작업을 위해 Web API를 사용 하는 방법에 대 한 자세한 내용은 [Crud 작업을 지 원하는 WEB Api 만들기](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md)를 참조 하세요. 이 컨트롤러에 대 한 코드는 매우 간단 합니다. 몇 가지 흥미로운 사항은 다음과 같습니다.

- `GetTodoLists` 메서드는 LINQ 쿼리를 사용 하 여 로그인 한 사용자의 ID를 기준으로 결과를 필터링 합니다. 이렇게 하면 사용자는 자신이 속한 데이터만 볼 수 있습니다. 또한 Select 문은 `ToDoList` 인스턴스를 `TodoListDto` 인스턴스로 변환 하는 데 사용 됩니다.
- PUT 및 POST 메서드는 데이터베이스를 수정 하기 전에 모델 상태를 확인 합니다. **Modelstate. IsValid** 가 false 이면 이러한 메서드는 HTTP 400, 잘못 된 요청을 반환 합니다. [모델 유효성 검사](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)에서 Web API의 모델 유효성 검사에 대해 자세히 알아보세요.
- 또한 컨트롤러 클래스는 **[권한 부여]** 특성으로 데코 레이트 됩니다. 이 특성은 HTTP 요청이 인증 되었는지 여부를 확인 합니다. 요청이 인증 되지 않은 경우 클라이언트는 HTTP 401, 권한 없음을 수신 합니다. 인증 [및 권한 부여의](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)인증에 대 한 자세한 내용은 ASP.NET Web API을 참조 하세요.

`TodoController` 클래스는 `TodoListController`와 매우 비슷합니다. 가장 큰 차이점은 클라이언트는 각 할 일 목록과 함께 할 일 항목을 가져오기 때문에 GET 메서드를 정의 하지 않는다는 것입니다.

## <a name="mvc-controllers-and-views"></a>MVC 컨트롤러 및 뷰

MVC 컨트롤러는 솔루션의 Controllers 폴더에도 있습니다. `HomeController` 응용 프로그램에 대 한 기본 HTML을 렌더링 합니다. Home 컨트롤러에 대 한 보기는 Views/Home/Index. cshtml에 정의 되어 있습니다. 홈 보기는 사용자의 로그인 여부에 따라 서로 다른 콘텐츠를 렌더링 합니다.

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

사용자가 로그인 하면 주 UI가 표시 됩니다. 그렇지 않으면 로그인 패널이 표시 됩니다. 이 조건부 렌더링은 서버 쪽에서 발생 합니다. 클라이언트 쪽&#8212;에서 중요 한 콘텐츠를 숨기지 마세요. http 응답에서 보내는 모든 항목은 원시 http 메시지를 감시 하는 사람에 게 표시 됩니다.

## <a name="client-side-javascript-and-knockoutjs"></a>클라이언트 쪽 JavaScript 및 녹아웃

이제 응용 프로그램의 서버 쪽에서 클라이언트로 전환 해 보겠습니다. SPA 템플릿은 jQuery와 녹아웃의 조합을 사용 하 여 부드러운 대화형 UI를 만듭니다. 녹아웃은 HTML을 데이터에 쉽게 바인딩할 수 있도록 하는 JavaScript 라이브러리입니다. 녹아웃은 "모델-뷰-ViewModel" 이라는 패턴을 사용 합니다.

- 이 모델은 도메인 데이터 (할 일 목록 및 할 일 항목)입니다.
- 뷰는 HTML 문서입니다.
- 뷰 모델은 모델 데이터를 포함 하는 JavaScript 개체입니다. 뷰 모델은 UI의 코드 추상화입니다. HTML 표현에 대해 알지 못합니다. 대신 "할 일 항목 목록"과 같은 뷰의 추상 기능을 나타냅니다.

뷰가 뷰 모델에 대 한 데이터 바인딩된 뷰입니다. 뷰 모델에 대 한 업데이트는 뷰에 자동으로 반영 됩니다. 바인딩은 다른 방향에도 적용 됩니다. DOM의 이벤트 (예: 클릭)는 보기 모델의 함수에 대 한 데이터 바인딩된 함수로, AJAX 호출을 트리거합니다.

SPA 템플릿에서는 클라이언트 쪽 JavaScript를 세 개의 계층으로 구성 합니다.

- todo. datacontext: AJAX 요청을 보냅니다.
- todo. node.js: 모델을 정의 합니다.
- todo. viewmodel: 뷰 모델을 정의 합니다.

![](knockoutjs-template/_static/image11.png)

이러한 스크립트 파일은 솔루션의 스크립트/앱 폴더에 있습니다.

![](knockoutjs-template/_static/image12.png)

**todo. datacontext** 는 Web API 컨트롤러에 대 한 모든 AJAX 호출을 처리 합니다. (로그인에 대 한 AJAX 호출은 ajaxlogin의 다른 곳에서 정의 됩니다.)

**todo. node.js** 목록에 대 한 클라이언트 쪽 (브라우저) 모델을 정의 합니다. TodoItem 및 todoList의 두 가지 모델 클래스가 있습니다.

모델 클래스의 속성 중 상당수는 "ko-kr" 형식입니다. 관찰 가능 개체는 녹아웃이 마법을 수행 하는 방법입니다. [녹아웃 설명서](http://knockoutjs.com/documentation/introduction.html)에서: 관찰 가능은 "구독자에 게 변경 내용을 알릴 수 있는 JavaScript 개체"입니다. 관찰 가능 값이 변경 되 면 해당 관찰 가능 개체에 바인딩된 HTML 요소가 모두 업데이트 됩니다. 예를 들어 todoItem에는 title 및 isDone 속성에 대 한 관찰 가능 개체가 있습니다.

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

코드에서 관찰 가능 개체를 구독할 수도 있습니다. 예를 들어, todoItem 클래스는 "isDone" 및 "title" 속성의 변경 내용을 구독 합니다.

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**모델 보기**

뷰 모델은 todo. viewmodel에 정의 되어 있습니다. 뷰 모델은 응용 프로그램이 HTML 페이지 요소를 도메인 데이터에 바인딩하는 중심점입니다. SPA 템플릿에서 뷰 모델은 관찰 가능한 todoLists 배열을 포함 합니다. 뷰 모델의 다음 코드는 바인딩을 적용 하도록 녹아웃에 지시 합니다.

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML 및 데이터 바인딩

페이지의 기본 HTML은 Views/Home/Index. cshtml에 정의 되어 있습니다. 데이터 바인딩을 사용 하기 때문에 HTML은 실제로 렌더링 되는 항목에 대 한 템플릿만 아닙니다. 녹아웃은 *선언적* 바인딩을 사용 합니다. 요소에 "데이터 바인딩" 특성을 추가 하 여 페이지 요소를 데이터에 바인딩합니다. 다음은 녹아웃 설명서에서 가져온 매우 간단한 예제입니다.

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

이 예제에서 녹아웃은 **&lt;범위&gt;** 요소의 내용을 `myItems.count()`값으로 업데이트 합니다. 이 값이 변경 될 때마다 녹아웃은 문서를 업데이트 합니다.

녹아웃은 여러 가지 다양 한 바인딩 형식을 제공 합니다. SPA 템플릿에 사용 되는 바인딩 중 일부는 다음과 같습니다.

- **foreach**: 루프를 반복 하 고 목록의 각 항목에 동일한 태그를 적용할 수 있습니다. 이는 할 일 목록 및 할 일 항목을 렌더링 하는 데 사용 됩니다. **Foreach**내에서 바인딩은 목록의 요소에 적용 됩니다.
- **visible**: 표시 여부를 전환 하는 데 사용 됩니다. 컬렉션이 비어 있을 때 태그를 숨기 거 나 오류 메시지를 표시 합니다.
- **value**: 폼 값을 채우는 데 사용 됩니다.
- **클릭**: 뷰 모델의 함수에 click 이벤트를 바인딩합니다.

## <a name="anti-csrf-protection"></a>CSRF 방지 보호

CSRF (교차 사이트 요청 위조)는 악의적인 사이트에서 사용자가 현재 로그인 한 취약 한 사이트로 요청을 보내는 공격입니다. CSRF 공격을 방지 하기 위해 ASP.NET MVC는 요청 확인 토큰이 라고도 하는 *위조 방지 토큰*을 사용 합니다. 서버는 임의로 생성 된 토큰을 웹 페이지에 배치 한다는 것을 알 수 있습니다. 클라이언트에서 서버로 데이터를 전송 하는 경우 요청 메시지에이 값을 포함 해야 합니다.

위조 방지 토큰은 동일한 원본 정책으로 인해 악의적인 페이지가 사용자의 토큰을 읽을 수 없기 때문에 작동 합니다. 동일한 원본 정책을 통해 서로 다른 두 사이트에서 호스팅되는 문서는 서로의 내용에 액세스할 수 없습니다.

ASP.NET MVC는 [위조](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx) 방지 클래스 및 [[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx) 특성을 통해 위조 방지 토큰에 대 한 기본 제공 지원을 제공 합니다. 현재이 기능은 Web API에 기본 제공 되지 않습니다. 그러나 SPA 템플릿에는 Web API에 대 한 사용자 지정 구현이 포함 되어 있습니다. 이 코드는 솔루션의 Filters 폴더에 있는 `ValidateHttpAntiForgeryTokenAttribute` 클래스에서 정의 됩니다. Web API에서 CSRF 방지에 대해 자세히 알아보려면 [csrf (교차 사이트 요청 위조) 공격 방지](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md)를 참조 하세요.

## <a name="conclusion"></a>결론

SPA 템플릿은 최신 대화형 웹 응용 프로그램을 신속 하 게 작성할 수 있도록 설계 되었습니다. 이 도구는 녹아웃 .js 라이브러리를 사용 하 여 데이터 및 응용 프로그램 논리에서 프레젠테이션 (HTML 태그)을 분리 합니다. 하지만 녹아웃은 SPA를 만드는 데 사용할 수 있는 유일한 JavaScript 라이브러리가 아닙니다. 다른 옵션을 살펴보려면 [커뮤니티에서 만든 SPA 템플릿을](../templates/index.md)살펴보세요.
