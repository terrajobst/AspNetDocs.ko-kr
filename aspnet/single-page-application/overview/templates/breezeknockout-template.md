---
uid: single-page-application/overview/templates/breezeknockout-template
title: 템플릿 간편 하 게/녹아웃 | Microsoft Docs
author: madskristensen
description: 단일 페이지 응용 프로그램 템플릿 간편/녹아웃
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 5bb9ee8f758a25afa6baf3ccbaf7d5864754c7df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449747"
---
# <a name="breezeknockout-template"></a>Breeze/Knockout 템플릿

[Mads Kristensen](https://github.com/madskristensen)

> 간편 하 고 녹아웃 MVC 템플릿은
> 
> [간편 하 고 녹아웃 MVC 템플릿 다운로드](https://go.microsoft.com/fwlink/?LinkId=282649)

"SPA (단일 페이지 응용 프로그램)"를 들었습니다. 이에 대 한 정보를 읽을 수는 있지만 사용자가 직접 경험 하 게 됩니다. 하지만 누가 샘플을 다운로드할 수 있나요? Visual Studio를 사용 하는 경우 ASP.NET MVC 4 "/녹아웃 단일 페이지 응용 프로그램" 템플릿을 사용 하 여 60 초 이내에 SPA를 실행 하는 예제를 사용할 수 있습니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>간편 하 고 녹아웃 된 SPA 템플릿은 무엇 인가요?

대부분의 프로젝트 템플릿은 응용 프로그램 구조를 생성 합니다. 코드를 추가 하 고 결국 작업 중인 응용 프로그램을 제공 하 여 이러한 뼈에 플레쉬를 배치 합니다. 간편 하거나 녹아웃 된 SPA 템플릿이 다릅니다. 검토할 샘플 응용 프로그램을 생성 합니다. Spa 응용 프로그램 디자인 및 SPA를 구축 하기 위한 다양 한 기술을 보여 줍니다.

간편/녹아웃 템플릿은 ASP.NET 및 Web Tools 2012.2 업데이트에 포함 된 [KNOCKOUTJS SPA 템플릿에](../introduction/knockoutjs-template.md) 대 한 변형입니다. 간편 SPA 템플릿에서는 동일한 사용자 환경으로 응용 프로그램을 생성 하지만 데이터 관리를 간편 하 게 사용 하 여 다른 구현을 제공 합니다.

KnockoutJS SPA 템플릿에서는 단순 응용 프로그램에 적합 한 원시 jQuery AJAX를 사용 하 여 서비스 요청을 수행 합니다. 그러나 더 복잡 한 앱은 더 까다로운 데이터 관리 요구 사항을 갖습니다. 예를 들어, 대부분의 응용 프로그램은 다음과 같습니다.

- 확장 사용자 세션 중에 서버를 쿼리하고 다시 쿼리 합니다.
- 쿼리 필터, 정렬 및 페이징을 추가 합니다.
- 여러 화면에서 동일한 데이터를 공유 합니다.
- 많은 개체에 변경 내용을 누적 한 다음 단일 트랜잭션으로 저장 합니다.
- 클라이언트에서 변경 내용의 유효성을 검사 하 여 데이터베이스에 변경 내용을 커밋하기 전에 사용자가 실수를 수정할 수 있습니다.

BreezeJS 라이브러리는 이러한 작업을 처리 하 여 가장 중요 한 응용 프로그램 논리와 사용자 환경을 개발 합니다.

[**간편**](http://www.breezejs.com/?utm_source=ms-spa) 하 게는 JAVASCRIPT 및 HTML로 풍부한 데이터 응용 프로그램을 빌드하기 위한 오픈 소스 라이브러리로, 지금까지 독립 실행형 데스크톱 응용 프로그램으로 제공 된 앱의 종류입니다.

간편/녹아웃 템플릿을 사용 하면 보다 강력한 데이터 관리 인프라에 대 한 첫 번째 중요 한 단계를 수행할 수 있습니다. KnockoutJS SPA 템플릿과 outwardly 동일한 샘플 Todo 응용 프로그램을 생성 합니다. 내부에서는 AJAX 데이터 계층을 간편 하 게 대체 하므로 두 가지 방법을 나란히 비교할 수 있습니다. 물론 간단히 응용 프로그램의 잠재력은 거의 없습니다. 그러나이 동작을 수행 하는 방법 및 해당 전환을 수행 하는 데 필요한 정도를 확인할 수 있습니다.

이제 시작하겠습니다.

## <a name="create-a-breezeknockout-template-project"></a>간편 하 게 템플릿 프로젝트 만들기

위의 다운로드 단추를 클릭 하 여 템플릿을 다운로드 하 고 설치 합니다. 템플릿은 VSIX (Visual Studio Extension) 파일로 패키지 됩니다. Visual Studio를 다시 시작 해야 할 수 있습니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 지정하고 **확인**을 클릭합니다.

**새 프로젝트** 마법사에서 간편 하 게 **녹아웃 SPA**를 선택 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

Ctrl + f 5를 눌러 디버깅 하지 않고 응용 프로그램을 빌드하고 실행 하거나 F5 키를 눌러 디버깅을 실행 합니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

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

유효성 검사 논리는 클라이언트 쪽에서 간편 하 게 수행 됩니다. 서버 모델 클래스의 유효성 검사 특성은 클라이언트에 전파 되 고 클라이언트가 서버에 연결 하기 전에 자동으로 실행 됩니다.

네트워크 트래픽을 검토 합니다. 오류가 검색 되 면 서버에 대 한 호출이 없습니다. 각각의 유효한 변경에는 "/api/Todo/SaveChanges"에 대 한 POST 요청이 발생 했습니다. 간편 하 게 변경 내용을 번들로 묶어 웹 API 컨트롤러의 `SaveChanges` 메서드에 단일 요청으로 보냅니다. 이는 KnockoutJS SPA 템플릿과 다르며 각 항목에 대 한 PUT, POST 및 DELETE 요청을 개별적으로 수행 합니다.

## <a name="peek-inside"></a>내부 피킹

이 응용 프로그램에는 클라이언트 쪽 및 서버 쪽이 있습니다. 클라이언트 쪽 스택은 작은 HTML과 응용 프로그램 JavaScript 모듈의 조합 ("응용 프로그램" 폴더)과 타사 JavaScript 라이브러리 ("Scripts" 폴더)로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

KnockoutJS SPA 템플릿을 조사 했다면 매우 익숙할 것입니다. 파란색 상자에 포커스를 둡니다. UI 아키텍처는 뷰의 HTML 위젯이 뷰 모델의 지원 되는 프레젠테이션 코드와 명확 하 게 구분 되는 MVVM (모델-뷰-ViewModel)입니다. 데이터 바인딩 시스템 (이 경우에는 녹아웃)은 뷰 및 뷰 모델을 조정 하 여 각 항목에 대 한 지식 없이 작업을 수행할 수 있도록 합니다.

모델은 Todo 데이터를 캡슐화 합니다. 모델의 엔터티는 녹아웃 가능한 속성을 사용 하 여 간편 하 게 생성 되므로 뷰에서 위젯에 직접 바인딩될 수 있습니다. 뷰 모델은 데이터 컨텍스트에 모델 엔터티를 가져오고 저장 하도록 요청 합니다. 데이터 컨텍스트는 대부분의 작업을 간편 하 게 위임 합니다.

서버 쪽 스택은 몇 가지 개발자 코드와 세 가지 원칙 .NET 라이브러리 (Web API, Entity Framework 및 Breeze.NET)로 구성 됩니다.

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

기본 아키텍처는 KnockoutJS SPA 템플릿과 동일 합니다. 그러나 Dto가 삭제 되 고 대부분의 Entity Framework 정보가 Breeze.NET로 위임 된 구현이 훨씬 더 간단 합니다.

## <a name="next-steps"></a>다음 단계

간편 하 게 웹 사이트에서 클라이언트와 서버 스택 모두에 대 한 [광범위 한 논의](http://www.breezejs.com/spa-template?utm_source=ms-spa) 를 안내 하는 코드를 탐색 하는 것이 좋습니다.

클라이언트 쪽 쿼리를 간편 하 게 재생 해 볼 수 있습니다. 일부 필터와 정렬을 추가 합니다. 더 많은 모델 속성과 엔터티를 추가 하 여 종단 간 SPA 개발에 더 나은 느낌을 얻을 수 있습니다. 디자인을 확신 하는 경우 Todo 기능을 분리 하 고 자신의 기능으로 바꿀 수 있습니다.

곧 클라이언트 쪽 화면을 추가 하 고 탐색 하는 다음의 큰 단계를 수행할 준비가 되었습니다. 이 SPA 템플릿을 그대로 유지 하 고 [John Papa의 Hot 수건](https://github.com/johnpapa/HotTowel#readme "핫 수건")와 같은 완전 한 spa 스택으로 전환 하 여 간편 하 고 녹아웃 조합에 Durandal를 추가 합니다.
