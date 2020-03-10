---
uid: single-page-application/overview/templates/breezeangular-template
title: 간편/각도 템플릿 | Microsoft Docs
author: madskristensen
description: 간편/각도 단일 페이지 응용 프로그램 템플릿
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467189"
---
# <a name="breezeangular-template"></a>Breeze/Angular 템플릿

[Mads Kristensen](https://github.com/madskristensen)

> 매우 종 모양의 MVC 템플릿이 함께 작성 되었습니다.
> 
> [간편 하 고 직각 MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org) 는 Spas (단일 페이지 응용 프로그램)를 빌드하기 위한 Google의 오픈 소스 라이브러리입니다. 데이터 바인딩, 종속성 주입 및 화면 관리를 제공 합니다. 데이터 모델링 및 데이터 관리를 위한 또 다른 오픈 소스 라이브러리인 [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa)와 결합 하 여 멋진 HTML/JavaScript 클라이언트 앱에 필요한 원료를 사용할 수 있습니다.

간편/각도 SPA 템플릿은 ASP.NET 및 Web Tools 2012.2 업데이트에 포함 된 [KNOCKOUTJS SPA 템플릿에](../introduction/knockoutjs-template.md) 대 한 변형입니다. Visual Studio가 있는 경우 예제 SPA를 60 초 이내에 실행 하 게 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

Outwardly 응용 프로그램은 KnockoutJS SPA 템플릿과 매우 유사 하 게 보입니다. 하지만 내부적으로는 매우 다릅니다. KnockoutJS 템플릿은 데이터 바인딩에 대해 녹아웃을 사용 하 고 데이터 액세스에 원시 AJAX를 사용 합니다. 간편/각도 템플릿은 데이터 바인딩을 위한 각도를 사용 하 고 데이터 액세스에 간편 합니다. 이러한 라이브러리를 사용 하면 페이지 탐색 및 기록을 비롯 한 추가 기능을 사용할 수 있습니다.

응용 프로그램의 정보 페이지는 다음과 같습니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

이 페이지에는 다음을 포함 하 여 현재 사용자 세션 동안 실행 중인 이벤트 로그가 표시 됩니다.

- 페이징. #2 및 #7에서 Todo 컨트롤러 만들기를 확인 합니다.
- 원격 쿼리 (#3) 및 로컬 캐시 쿼리 (#7).
- 새 (#5, #6) 및 수정 된 (#4) 엔터티를 저장 합니다.
- 클라이언트에서 유효성 검사를 수행 했습니다 (#9). 따라서 데이터베이스에 변경 내용을 커밋하기 전에 사용자가 실수를 수정할 수 있습니다.

다음을 포함 하 여이 템플릿에서 자세히 살펴볼 수 있습니다.

- HTML 뷰 템플릿의 동적 로드
- 각도 "지시문"을 통한 사용자 지정 데이터 바인딩
- 모듈화 및 종속성 주입.
- 필터링, 정렬, 페이징, 프로젝션 및 관련 엔터티의 포함을 쿼리 합니다.
- 여러 화면에서 데이터 공유
- 단일 트랜잭션으로 여러 변경 내용 저장
- 유효성 검사 규칙은 서버에서 JavaScript 클라이언트로 자동으로 전파 됩니다.

이제 시작하겠습니다.

## <a name="create-a-breezeangular-template-project"></a>간편 하 고 각도 템플릿 프로젝트 만들기

위의 다운로드 단추를 클릭 하 여 템플릿을 다운로드 하 고 설치 합니다. 템플릿은 VSIX (Visual Studio Extension) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 할 수 있습니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.

**새 프로젝트** 마법사에서 **간편 각도 SPA**를 선택 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

Ctrl + f 5를 눌러 디버깅 하지 않고 응용 프로그램을 빌드하고 실행 하거나 F5 키를 눌러 디버깅을 실행 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

응용 프로그램을 처음 실행 하면 로그인 화면이 표시 됩니다. "등록" 링크를 클릭 하면 glides 새 페이지가 표시 됩니다. 여기서 사용자 이름 및 암호를 입력할 수 있습니다. 로그인 및 등록 페이지는 ASP.NET MVC를 사용 하 여 빌드됩니다. 등록 양식을 제출할 때 서버는 계정에 대해 두 개의 항목이 포함 된 TodoList을 생성 합니다. 그런 다음 노란색 메모를 표시 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

이제 SPA를 사용할 수 있습니다. Todos를 조작 하는 동안 표시 되는 모든 작업은 클라이언트에서 렌더링 되 고 관리 되며 녹아웃 및 편리 합니다. 사용자로 앱 탐색 ... 개발자의 눈에도 있습니다. 브라우저에서 개발자 도구를 사용 하 여 네트워크 트래픽을 캡처할 수 있습니다. (Internet Explorer에서 F12 키를 누르고 **네트워크** 탭을 선택한 후 **캡처 시작**을 클릭 합니다.) 이제 다음을 시도 합니다.

- 새 Todo 항목을 추가 합니다.
- 레이블을 클릭 하 고 Todo 항목 제목을 편집 합니다.
- 확인란을 선택 하 여 항목을 완료로 표시 합니다. 텍스트 상자를 사용할 수 없으므로 제목은 더 이상 편집할 수 없습니다.
- 레이블 오른쪽의 ' x '를 클릭 합니다. 항목이 사라지고 데이터베이스에서 삭제 됩니다.
- 다른 항목을 선택 하 고 제목을 지웁니다. 제목이 필요 하다는 유효성 검사 오류를 받게 됩니다. 잠시 후에 이전 제목이 복원 됩니다.
- 터무니 없이 긴 제목을 입력 합니다. 제목이 너무 길어서 다른 유효성 검사 오류를 받게 됩니다.
- "할 일 목록 추가" 단추를 클릭 합니다. 새 목록이 이전 목록의 왼쪽에 표시 됩니다.
- TodoList 제목으로 재생 하 고 필수 및 길이 유효성 검사를 트리거합니다.
- 제목 텍스트 상자를 클릭 하 여 오류 메시지를 지웁니다.
- 오른쪽 위의 원에서 "x"를 클릭 하 여 TodoList 및 해당 todos를 삭제 합니다.
- 오른쪽 위에 있는 "정보" 링크를 클릭 하 여 이러한 활동의 로그를 확인 합니다.

유효성 검사 논리는 클라이언트 쪽에서 간편 하 게 수행 됩니다. 서버 모델 클래스의 유효성 검사 특성은 클라이언트에 전파 되 고 클라이언트가 서버에 연결 하기 전에 자동으로 실행 됩니다.

네트워크 트래픽을 검토 합니다. 오류가 검색 되 면 서버에 대 한 호출이 없습니다. 각각의 유효한 변경에는 "/api/Todo/SaveChanges"에 대 한 POST 요청이 발생 했습니다. 간편 하 게 변경 내용을 번들로 묶어 웹 API 컨트롤러의 `SaveChanges` 메서드에 단일 요청으로 보냅니다. 이는 KnockoutJS SPA 템플릿과 다르며 각 항목에 대 한 PUT, POST 및 DELETE 요청을 개별적으로 수행 합니다.

또한 TodoList와 About 페이지 간을 전환할 때 네트워크 트래픽이 없습니다. 쿼리가 로컬의 간편 캐시로 제한 되기 때문입니다.

## <a name="peek-inside"></a>내부 피킹

이 응용 프로그램에는 클라이언트 쪽 및 서버 쪽이 있습니다. 클라이언트 쪽 스택은 작은 HTML과 응용 프로그램 JavaScript 모듈의 조합 ("응용 프로그램" 폴더)과 타사 JavaScript 라이브러리 ("Scripts" 폴더)로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

UI 아키텍처는 뷰의 HTML 위젯을 컨트롤러의 지원 프레젠테이션 코드와 분리 합니다. 각도 데이터 바인딩 시스템은 뷰 및 컨트롤러를 조정 하 여 각각이 다른 항목에 대 한 지식이 없어도 작업을 수행할 수 있습니다.

컨트롤러는 모델 엔터티를 획득 하 고 저장 하기 위해 데이터 컨텍스트에 요청 합니다. 데이터 컨텍스트는 대부분의 작업을 간편 하 게 위임 하므로 JSON 쿼리 결과에서 자체 추적 모델 개체를 생성 합니다.

서버 쪽 스택은 몇 가지 개발자 코드와 세 가지 원칙 .NET 라이브러리 (Web API, Entity Framework 및 Breeze.NET)로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

기본 아키텍처는 KnockoutJS SPA 템플릿과 동일 합니다. 그러나 Dto가 삭제 되 고 대부분의 Entity Framework 정보가 Breeze.NET로 위임 된 구현이 훨씬 더 간단 합니다.

## <a name="next-steps"></a>다음 단계

간편 하 게 웹 사이트에서 클라이언트와 서버 스택 모두에 대 한 [광범위 한 논의](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) 를 안내 하는 코드를 탐색 하는 것이 좋습니다.

클라이언트 쪽 쿼리를 간편 하 게 재생 해 볼 수 있습니다. 일부 필터와 정렬을 추가 합니다. 더 많은 모델 속성과 엔터티를 추가 하 여 종단 간 SPA 개발에 더 나은 느낌을 얻을 수 있습니다. 디자인을 확신 하는 경우 Todo 기능을 분리 하 고 자신의 기능으로 바꿀 수 있습니다.

즐거운 코딩 작업이 되길 바랍니다!
