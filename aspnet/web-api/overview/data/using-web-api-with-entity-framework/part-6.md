---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript 클라이언트 만들기 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504725"
---
# <a name="create-the-javascript-client"></a>JavaScript 클라이언트 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 HTML, JavaScript 및 [녹아웃 .js](http://knockoutjs.com/) 라이브러리를 사용 하 여 응용 프로그램에 대 한 클라이언트를 만듭니다. 다음 단계에서 클라이언트 앱을 빌드합니다.

- 책 목록을 표시 합니다.
- 책 정보를 표시 합니다.
- 새 책을 추가 합니다.

녹아웃 라이브러리는 MVVM (모델-뷰-ViewModel) 패턴을 사용 합니다.

- **모델** 은 비즈니스 도메인 (이 경우 책 및 저자)의 데이터를 서버 쪽으로 표현한 것입니다.
- **뷰** 는 프레젠테이션 계층 (HTML)입니다.
- **뷰 모델** 은 모델을 보유 하는 JavaScript 개체입니다. 뷰 모델은 UI의 코드 추상화입니다. HTML 표현에 대해 알지 못합니다. 대신, 책&quot;목록 &quot;와 같이 뷰의 추상 기능을 나타냅니다.

뷰 모델에 대 한 데이터 바인딩된 뷰입니다. 뷰 모델에 대 한 업데이트는 뷰에 자동으로 반영 됩니다. 뷰 모델은 단추 클릭과 같은 보기 에서도 이벤트를 가져옵니다.

![](part-6/_static/image1.png)

이 방법을 사용 하면 코드를 다시 작성 하지 않고도 바인딩을 변경할 수 있으므로 앱의 레이아웃 및 UI를 쉽게 변경할 수 있습니다. 예를 들어 `<ul>`항목의 목록을 표시 한 다음 나중에 테이블로 변경할 수 있습니다.

## <a name="add-the-knockout-library"></a>녹아웃 라이브러리 추가

Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다. 그런 후 **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](part-6/samples/sample1.cmd)]

이 명령은 녹아웃 파일을 Scripts 폴더에 추가 합니다.

## <a name="create-the-view-model"></a>뷰 모델 만들기

Scripts 폴더에 node.js 라는 JavaScript 파일을 추가 합니다. 솔루션 탐색기에서 Scripts 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **JavaScript 파일**을 선택 합니다. 다음 코드를 붙여 넣습니다.

[!code-javascript[Main](part-6/samples/sample2.js)]

녹아웃에서 `observable` 클래스는 데이터 바인딩을 사용 하도록 설정 합니다. 관찰 가능의 내용이 변경 되 면 관찰 가능 개체는 모든 데이터 바인딩된 컨트롤에 자동으로 알리고 자체적으로 업데이트할 수 있습니다. `observableArray` 클래스는 *관찰*가능의 배열 버전입니다. 먼저 보기 모델에는 두 가지 관찰 가능 개체 있습니다.

- `books`은 책 목록을 보유 합니다.
- AJAX 호출이 실패 하면 `error`에 오류 메시지가 포함 됩니다.

`getAllBooks` 메서드는 서적 목록을 가져오는 AJAX 호출을 수행 합니다. 그런 다음 `books` 배열에 결과를 푸시합니다.

`ko.applyBindings` 메서드는 녹아웃 라이브러리의 일부입니다. 뷰 모델을 매개 변수로 사용 하 고 데이터 바인딩을 설정 합니다.

## <a name="add-a-script-bundle"></a>스크립트 번들 추가

번들은 여러 파일을 단일 파일로 쉽게 결합 하거나 묶을 수 있는 ASP.NET 4.5의 기능입니다. 묶음은 서버에 대 한 요청 수를 줄여 페이지 로드 시간을 향상 시킬 수 있습니다.

File App\_Start/BundleConfig를 엽니다. RegisterBundles 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [이전](part-5.md)
> [다음](part-7.md)
