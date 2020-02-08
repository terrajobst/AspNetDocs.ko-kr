---
uid: single-page-application/overview/templates/backbonejs-template
title: 백본 템플릿 | Microsoft Docs
author: madskristensen
description: 백본 jspa 템플릿
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074893"
---
# <a name="backbone-template"></a>백본 템플릿

[Mads Kristensen](https://github.com/madskristensen)

> 백본 SPA 템플릿은 Kazi Manzur Rashid에 의해 작성 되었습니다.
> 
> [Default.js SPA 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=293631)

Default.js SPA 템플릿은 [백본을](http://backbonejs.org/) 사용 하 여 대화형 클라이언트 쪽 웹 앱을 신속 하 게 빌드할 수 있도록 설계 되었습니다.

템플릿은 ASP.NET MVC에서 백본 응용 프로그램을 개발 하기 위한 초기 구조를 제공 합니다. 기본적으로 기본 전자 메일 템플릿과 함께 사용자 등록, 로그인, 암호 재설정 및 사용자 확인 등 기본적인 사용자 로그인 기능을 제공 합니다.

요구 사항:

- [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>백본 템플릿 프로젝트 만들기

위의 다운로드 단추를 클릭 하 여 템플릿을 다운로드 하 고 설치 합니다. 템플릿은 VSIX (Visual Studio Extension) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 할 수 있습니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.

![](backbonejs-template/_static/image1.png)

**새 프로젝트** 마법사에서 Default.js SPA 프로젝트를 선택 합니다.

![](backbonejs-template/_static/image2.png)

Ctrl + f 5를 눌러 디버깅 하지 않고 응용 프로그램을 빌드하고 실행 하거나 F5 키를 눌러 디버깅을 실행 합니다.

![](backbonejs-template/_static/image3.png)

"내 계정"을 클릭 하면 로그인 페이지가 표시 됩니다.

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>연습: 클라이언트 코드

클라이언트 쪽부터 시작 해 보겠습니다. 클라이언트 응용 프로그램 스크립트는 ~/Scripts/application 폴더에 있습니다. 응용 프로그램은 JavaScript (.js 파일)로 컴파일되는 [TypeScript](http://www.typescriptlang.org/) (. t a s 파일)로 작성 됩니다.

**애플리케이션**

`Application`는 응용 프로그램에 정의 되어 있습니다. 이 개체는 응용 프로그램을 초기화 하 고 루트 네임 스페이스 역할을 합니다. 사용자가 로그인 했는지 여부와 같이 응용 프로그램에서 공유 되는 구성 및 상태 정보를 유지 관리 합니다.

`application.start` 메서드는 모달 뷰를 만들고 사용자 로그인과 같은 응용 프로그램 수준 이벤트에 대 한 이벤트 처리기를 연결 합니다. 그런 다음 기본 라우터를 만들고 클라이언트 쪽 URL이 지정 되었는지 여부를 확인 합니다. 그렇지 않으면 기본 url (#!/)으로 리디렉션됩니다.

**이벤트**

느슨하게 결합 된 구성 요소를 개발할 때 이벤트는 항상 중요 합니다. 응용 프로그램은 종종 사용자 동작에 대 한 응답으로 여러 작업을 수행 합니다. 백본은 모델, 컬렉션, 뷰 등의 구성 요소를 사용 하 여 기본 제공 이벤트를 제공 합니다. 이러한 구성 요소 간에 종속성 간 관계를 만드는 대신 템플릿은 "pub/sub" 모델을 사용 합니다. 즉, 이벤트. t e r에 정의 된 `events` 개체는 응용 프로그램 이벤트를 게시 하 고 구독할 수 있는 이벤트 허브 역할을 합니다. `events` 개체는 단일 항목입니다. 다음 코드에서는 이벤트를 구독 한 다음 이벤트를 트리거하는 방법을 보여 줍니다.

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**라우터**

Node.js에서 라우터는 클라이언트 쪽 페이지를 라우팅 하 고 작업 및 이벤트에 연결 하는 메서드를 제공 합니다. 템플릿은 router에서 단일 라우터를 정의 합니다. 라우터는 activable 보기를 만들고 보기를 전환할 때 상태를 유지 관리 합니다. (Activable 보기는 다음 섹션에 설명 되어 있습니다.) 처음에는 프로젝트에 홈 및 정보 라는 두 개의 더미 뷰가 있습니다. 또한 경로를 알 수 없는 경우 표시 되는 NotFound 뷰가 있습니다.

**뷰**

뷰는 ~/Scripts/application/views.에서 정의 됩니다. 활동 가능한 보기 및 모달 대화 상자 보기의 두 가지 뷰를 사용할 수 있습니다. 활동 가능 보기는 라우터에 의해 호출 됩니다. Activable 보기가 표시 되 면 다른 모든 activable 보기가 비활성 상태가 됩니다. Activable 보기를 만들려면 `Activable` 개체를 사용 하 여 뷰를 확장 합니다.

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

`Activable`으로 확장 하면 `activate` 및 `deactivate`두 개의 새 메서드가 뷰에 추가 됩니다. 라우터는 이러한 메서드를 호출 하 여 뷰를 활성화 하 고 비활성화할 합니다.

모달 보기는 [Twitter 부트스트랩](https://twitter.github.com/bootstrap/) 모달 대화 상자로 구현 됩니다. `Membership` 및 `Profile` 뷰는 모달 뷰입니다. 응용 프로그램 이벤트에 의해 모델 뷰를 호출할 수 있습니다. 예를 들어 `Navigation` 보기에서 "내 계정" 링크를 클릭 하면 사용자의 로그인 여부에 따라 `Membership` 뷰나 `Profile` 보기가 표시 됩니다. `Navigation`은 클릭 이벤트 처리기를 `data-command` 특성이 있는 모든 자식 요소에 연결 합니다. HTML 태그는 다음과 같습니다.

[!code-html[Main](backbonejs-template/samples/sample3.html)]

다음은 이벤트를 연결 하는 탐색의 코드입니다.

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**모델**

모델은 ~/Scripts/application/models.에 정의 되어 있습니다. 모델에는 기본 특성, 유효성 검사 규칙 및 서버 쪽 끝점의 세 가지 기본 항목이 있습니다. 일반적인 예는 다음과 같습니다.

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**플러그 인**

~/Scripts/application/lib 폴더에는 몇 가지 편리한 jQuery 플러그 인이 포함 되어 있습니다. 폼 파일은 양식 데이터를 사용 하기 위한 플러그 인을 정의 합니다. 양식 데이터를 serialize 또는 deserialize 하 고 모델 유효성 검사 오류를 표시 해야 하는 경우가 종종 있습니다. 이 폼에는 `serializeFields`, `deserializeFields`및 `showFieldErrors`와 같은 메서드가 있습니다. 다음 예제에서는 폼을 모델에 serialize 하는 방법을 보여 줍니다.

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Flashbar 플러그 인은 사용자에 게 다양 한 종류의 피드백 메시지를 제공 합니다. 메서드는 `$.showSuccessbar`, `$.showErrorbar` 및 `$.showInfobar`됩니다. 내부적으로는 Twitter 부트스트랩 경고를 사용 하 여 적절 한 애니메이션 메시지를 표시 합니다.

API는 약간 다르지만 확인. t s s 플러그 인은 브라우저의 확인 대화 상자를 대체 합니다.

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>연습: 서버 코드

이제 서버 쪽을 살펴보겠습니다.

**컨트롤러**

단일 페이지 응용 프로그램에서 서버는 사용자 인터페이스의 작은 역할만 재생 합니다. 일반적으로 서버는 초기 페이지를 렌더링 한 다음 JSON 데이터를 보내고 받습니다.

템플릿에는 두 가지 MVC 컨트롤러가 있습니다. `HomeController` 초기 페이지를 렌더링 하 고 `SupportsController`는 새 사용자 계정을 확인 하 고 암호를 다시 설정 하는 데 사용 됩니다. 템플릿의 다른 모든 컨트롤러는 ASP.NET Web API 컨트롤러 이며 JSON 데이터를 보내고 받습니다. 기본적으로 컨트롤러는 새 `WebSecurity` 클래스를 사용 하 여 사용자 관련 작업을 수행 합니다. 그러나 이러한 작업에 대해 대리자를 전달할 수 있는 선택적 생성자도 있습니다. 이렇게 하면 테스트를 더 쉽게 수행할 수 있으며, IoC 컨테이너를 사용 하 여 `WebSecurity`을 다른 항목으로 바꿀 수 있습니다. 다음은 예제입니다.

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>뷰

뷰는 모듈식으로 설계 되었습니다. 페이지의 각 섹션에는 자체 전용 뷰가 있습니다. 단일 페이지 응용 프로그램에서 일반적으로 해당 컨트롤러를 포함 하지 않는 뷰를 포함 합니다. `@Html.Partial('myView')`를 호출 하 여 뷰를 포함할 수 있지만이는 지루한 작업이 아닙니다. 이 작업을 더 쉽게 수행 하기 위해 템플릿에서 지정 된 폴더의 모든 뷰를 렌더링 하는 도우미 메서드 `IncludeClientViews`를 정의 합니다.

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

폴더 이름을 지정 하지 않으면 기본 폴더 이름은 "ClientViews"입니다. 클라이언트 뷰에서 부분 보기를 사용 하는 경우 밑줄 문자를 사용 하 여 부분 보기의 이름을로 바꿉니다 (예: `_SignUp`). `IncludeClientViews` 메서드는 이름이 밑줄로 시작 하는 모든 뷰를 제외 합니다. 클라이언트 뷰에 부분 뷰를 포함 하려면 `Html.Partial('_SignUp')`대신 `Html.ClientView('SignUp')`를 호출 합니다.

**전자 메일 보내기**

전자 메일을 보내기 위해 템플릿에서는 [우편 번호](http://aboutcode.net/postal)를 사용 합니다. 그러나 `IMailer` 인터페이스를 사용 하 여 코드의 나머지 부분에서 우편을 추상화 하므로 다른 구현으로 쉽게 바꿀 수 있습니다. 전자 메일 템플릿은 Views/email 폴더에 있습니다. 보낸 사람의 전자 메일 주소는 **appSettings** 섹션의 `sender.email` 키에 있는 web.config 파일에 지정 됩니다. 또한 web.config에서 `debug="true"` 때 응용 프로그램에는 개발 속도를 향상 하기 위해 사용자 메일 확인이 필요 하지 않습니다.

## <a name="github"></a>GitHub

[GitHub](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa)에서 백본을 jspa 템플릿을 찾을 수도 있습니다.
