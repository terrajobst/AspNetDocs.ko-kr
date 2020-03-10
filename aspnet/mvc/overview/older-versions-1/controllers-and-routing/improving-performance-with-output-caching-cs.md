---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
title: 출력 캐시를 사용 하 여C#성능 향상 () | Microsoft Docs
author: microsoft
description: 이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상 시킬 수 있는 방법에 대해 알아봅니다. ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 521c9117-81cd-4d8d-9d96-0256dc7bf50f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-cs
msc.type: authoredcontent
ms.openlocfilehash: 548c5bea2e9cf26e0574e72d2c0ea204dbd90f9c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486671"
---
# <a name="improving-performance-with-output-caching-c"></a>출력 캐싱을 통한 성능 향상(C#)

[Microsoft](https://github.com/microsoft) 에서

> 이 자습서에서는 출력 캐싱을 활용 하 여 ASP.NET MVC 웹 응용 프로그램의 성능을 크게 향상 시킬 수 있는 방법에 대해 알아봅니다. 컨트롤러 작업에서 반환 된 결과를 캐시 하는 방법에 대해 알아봅니다. 그러면 새 사용자가 작업을 호출할 때마다 동일한 콘텐츠를 만들 필요가 없습니다.

이 자습서의 목표는 출력 캐시를 활용 하 여 ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시키는 방법을 설명 하는 것입니다. 출력 캐시를 사용 하면 컨트롤러 동작에서 반환 된 콘텐츠를 캐시할 수 있습니다. 이런 방식으로 동일한 컨트롤러 작업이 호출 될 때마다 동일한 콘텐츠를 생성 하지 않아도 됩니다.

예를 들어 ASP.NET MVC 응용 프로그램에서 Index 라는 뷰의 데이터베이스 레코드 목록을 표시 한다고 가정 합니다. 일반적으로 사용자가 인덱스 뷰를 반환 하는 컨트롤러 동작을 호출할 때마다 데이터베이스 쿼리를 실행 하 여 데이터베이스에서 데이터베이스 레코드 집합을 검색 해야 합니다.

반면에 출력 캐시를 활용 하는 경우에는 사용자가 동일한 컨트롤러 작업을 호출할 때마다 데이터베이스 쿼리를 실행 하지 않을 수 있습니다. 뷰를 컨트롤러 작업에서 다시 생성 하지 않고 캐시에서 검색할 수 있습니다. 캐싱을 사용 하면 서버에서 중복 작업을 수행 하지 않아도 됩니다.

## <a name="enabling-output-caching"></a>출력 캐싱 사용

[OutputCache] 특성을 개별 컨트롤러 작업 또는 전체 컨트롤러 클래스 중 하나에 추가 하 여 출력 캐싱을 사용 하도록 설정 합니다. 예를 들어 목록 1의 컨트롤러는 Index () 라는 동작을 노출 합니다. Index () 작업의 출력은 10 초 동안 캐시 됩니다.

**목록 1 – Controllers\ homecontroller.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample1.cs)]

ASP.NET MVC의 베타 버전에서는 [http://www.MySite.com/](http://www.mysite.com/)와 같은 URL에 대해 출력 캐싱이 작동 하지 않습니다. 대신 [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index)와 같은 URL을 입력 해야 합니다. 

목록 1에서 Index () 작업의 출력은 10 초 동안 캐시 됩니다. 원하는 경우 훨씬 긴 캐시 기간을 지정할 수 있습니다. 예를 들어 1 일 동안 컨트롤러 작업의 출력을 캐시 하려는 경우 86400 초 (60 초 \* 60 분 \* 24 시간)의 캐시 기간을 지정할 수 있습니다.

지정 된 시간 동안 콘텐츠가 캐시 되는 것은 아닙니다. 메모리 리소스가 부족 해지면 캐시가 자동으로 콘텐츠를 제거 하기 시작 합니다.

목록 1의 홈 컨트롤러는 목록 2의 인덱스 뷰를 반환 합니다. 이 보기에 대 한 특별 한 사항은 없습니다. 인덱스 뷰는 단순히 현재 시간을 표시 합니다 (그림 1 참조).

**목록 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-cs/samples/sample2.aspx)]

**그림 1 – 캐시 된 인덱스 뷰**

![clip_image002](improving-performance-with-output-caching-cs/_static/image1.jpg)

브라우저의 주소 표시줄에 URL/Home/Index를 입력 하 여 인덱스 () 작업을 여러 번 호출 하 고 브라우저에서 새로 고침/다시 로드 단추를 반복 해 서 호출 하는 경우 인덱스 뷰가 표시 하는 시간은 10 초 동안 변경 되지 않습니다. 뷰가 캐시 되기 때문에 동일한 시간이 표시 됩니다.

응용 프로그램을 방문 하는 모든 사용자에 대해 동일한 보기가 캐시 된다는 것을 이해 하는 것이 중요 합니다. Index () 동작을 호출 하는 모든 사용자는 동일한 캐시 버전의 인덱스 뷰를 가져옵니다. 즉, 인덱스 보기를 제공 하기 위해 웹 서버에서 수행 해야 하는 작업의 양이 크게 줄어듭니다.

목록 2의 보기는 매우 간단한 작업을 수행 하는 것을 말합니다. 뷰는 현재 시간을 표시 합니다. 그러나 데이터베이스 레코드 집합을 표시 하는 뷰를 쉽게 캐시할 수 있습니다. 이 경우 데이터베이스 레코드 집합을 데이터베이스에서 검색할 필요가 없으며, 뷰를 반환 하는 컨트롤러 작업이 호출 될 때마다 데이터베이스 레코드 집합을 검색할 필요가 없습니다. 캐싱은 웹 서버와 데이터베이스 서버에서 수행 해야 하는 작업의 양을 줄일 수 있습니다.

MVC 뷰에서 페이지 &lt;% @ OutputCache%&gt; 지시어를 사용 하지 마세요. 이 지시어는 Web Forms에서 bleeding ASP.NET MVC 응용 프로그램에서 사용 하면 안 됩니다.

## <a name="where-content-is-cached"></a>콘텐츠가 캐시 되는 위치

기본적으로 [OutputCache] 특성을 사용 하면 콘텐츠가 웹 서버, 프록시 서버 및 웹 브라우저의 세 위치에 캐시 됩니다. [OutputCache] 특성의 Location 속성을 수정 하 여 콘텐츠를 캐시 하는 위치를 정확 하 게 제어할 수 있습니다.

Location 속성은 다음 값 중 하나로 설정할 수 있습니다.

> · 일부
> 
> · 클라이언트로
> 
> · 다운스트림
> 
> · 서버인
> 
> · 없음을
> 
> · ServerAndClient

기본적으로 Location 속성의 값은 Any입니다. 그러나 브라우저 에서만 캐시 하거나 서버에 있는 경우에만 캐시 해야 할 경우가 있습니다. 예를 들어 각 사용자에 대해 개인 설정 된 정보를 캐시 하는 경우 서버에 정보를 캐시 하면 안 됩니다. 다른 사용자에 게 다른 정보를 표시 하는 경우에는 클라이언트에만 정보를 캐시 해야 합니다.

예를 들어 목록 3의 컨트롤러는 현재 사용자 이름을 반환 하는 GetName () 이라는 작업을 표시 합니다. 잭이 웹 사이트에 로그인 하 여 GetName () 작업을 호출 하는 경우 작업은 문자열 "Hi 잭"을 반환 합니다. 그런 다음 Jill가 웹 사이트에 로그인 하 고 GetName () 작업을 호출 하는 경우에도 문자열 "Hi 잭"을 가져옵니다. 이 문자열은 잭이 처음에 컨트롤러 작업을 호출한 후에 모든 사용자에 대해 웹 서버에 캐시 됩니다.

**목록 3 – Controllers\BadUserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample3.cs)]

대개 목록 3의 컨트롤러는 원하는 방식으로 작동 하지 않습니다. Jill에 "Hi 잭" 메시지를 표시 하지 않으려고 합니다.

서버 캐시에 개인 설정 된 콘텐츠를 캐시 하면 안 됩니다. 그러나 브라우저 캐시에 개인 설정 된 콘텐츠를 캐시 하 여 성능을 향상 시킬 수 있습니다. 브라우저에서 콘텐츠를 캐시 하 고 사용자가 동일한 컨트롤러 작업을 여러 번 호출 하면 서버 대신 브라우저 캐시에서 콘텐츠를 검색할 수 있습니다.

목록 4의 수정 된 컨트롤러는 GetName () 작업의 출력을 캐시 합니다. 그러나 콘텐츠는 서버가 아닌 브라우저 에서만 캐시 됩니다. 이렇게 하면 여러 사용자가 GetName () 메서드를 호출할 때 각 사용자는 다른 사람의 사용자 이름이 아니라 자신의 사용자 이름을 얻습니다.

**목록 4 – Controllers\UserController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample4.cs)]

목록 4의 [OutputCache] 특성은 OutputCacheLocation. Client 값으로 설정 된 Location 속성을 포함 합니다. [OutputCache] 특성에는 NoStore 속성도 포함 되어 있습니다. NoStore 속성은 캐시 된 콘텐츠의 영구 복사본을 저장 하지 않도록 프록시 서버 및 브라우저에 알리는 데 사용 됩니다.

## <a name="varying-the-output-cache"></a>출력 캐시를 변경 합니다.

경우에 따라 동일한 콘텐츠의 서로 다른 캐시 된 버전을 사용할 수 있습니다. 예를 들어 마스터/세부 정보 페이지를 만드는 경우를 가정 합니다. 마스터 페이지에 영화 제목 목록이 표시 됩니다. 제목을 클릭 하면 선택한 영화에 대 한 세부 정보가 표시 됩니다.

세부 정보 페이지를 캐시 하는 경우 클릭 한 동영상에 관계 없이 동일한 영화에 대 한 세부 정보가 표시 됩니다. 첫 번째 사용자가 선택한 첫 번째 동영상이 앞으로 나오는 모든 사용자에 게 표시 됩니다.

[OutputCache] 특성의 VaryByParam 속성을 활용 하 여이 문제를 해결할 수 있습니다. 이 속성을 사용 하면 폼 매개 변수 또는 쿼리 문자열 매개 변수가 다를 때 동일한 콘텐츠의 서로 다른 캐시 된 버전을 만들 수 있습니다.

예를 들어 목록 5의 컨트롤러는 Master () 및 Details () 라는 두 개의 동작을 노출 합니다. Master () 작업은 동영상 제목의 목록을 반환 하 고, Details () 작업은 선택한 영화에 대 한 세부 정보를 반환 합니다.

**목록 5 – Controllers\MoviesController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample5.cs)]

Master () 작업은 값이 "none" 인 VaryByParam 속성을 포함 합니다. Master () 작업을 호출 하면 동일한 캐시 된 버전의 마스터 뷰가 반환 됩니다. 모든 폼 매개 변수 또는 쿼리 문자열 매개 변수는 무시 됩니다 (그림 2 참조).

**그림 2-/Movies/Master 뷰**

![clip_image004](improving-performance-with-output-caching-cs/_static/image2.jpg)

**그림 3-/Movies/Details 뷰**

![clip_image006](improving-performance-with-output-caching-cs/_static/image3.jpg)

Details () 작업은 값이 "Id" 인 VaryByParam 속성을 포함 합니다. Id 매개 변수의 다른 값이 컨트롤러 작업에 전달 되 면 다른 캐시 된 정보 보기 버전이 생성 됩니다.

VaryByParam 속성을 사용 하 여 더 많은 캐싱을 사용 하는 것은 아닙니다. 서로 다른 버전의 Id 매개 변수에 대해 서로 다른 캐시 된 버전의 자세히 보기가 생성 됩니다.

VaryByParam 속성을 다음 값으로 설정할 수 있습니다.

> \* = 폼 또는 쿼리 문자열 매개 변수가 다를 때마다 다른 캐시 된 버전을 만듭니다.
> 
> none = 다른 캐시 된 버전을 만들지 않습니다.
> 
> 세미콜론 매개 변수 목록 = 목록의 폼 또는 쿼리 문자열 매개 변수가 다를 때 다른 캐시 된 버전을 만듭니다.

## <a name="creating-a-cache-profile"></a>캐시 프로필 만들기

[OutputCache] 특성의 속성을 수정 하 여 출력 캐시 속성을 구성 하는 대신 웹 구성 파일 (web.config)에서 캐시 프로필을 만들 수 있습니다. 웹 구성 파일에서 캐시 프로필을 만들면 몇 가지 중요 한 이점이 있습니다.

첫째, 웹 구성 파일에서 출력 캐싱을 구성 하 여 컨트롤러 작업이 하나의 중앙 위치에서 콘텐츠를 캐시 하는 방법을 제어할 수 있습니다. 하나의 캐시 프로필을 만들고 프로필을 여러 컨트롤러나 컨트롤러 작업에 적용할 수 있습니다.

둘째, 응용 프로그램을 다시 컴파일하지 않고도 웹 구성 파일을 수정할 수 있습니다. 프로덕션에 이미 배포 된 응용 프로그램에 대 한 캐싱을 사용 하지 않도록 설정 해야 하는 경우 웹 구성 파일에 정의 된 캐시 프로필을 간단히 수정할 수 있습니다. 웹 구성 파일에 대 한 모든 변경 내용이 자동으로 검색 되어 적용 됩니다.

예를 들어 목록 6의 &lt;캐싱&gt; 웹 구성 섹션은 Cache1Hour 이라는 캐시 프로필을 정의 합니다. &lt;캐싱&gt; 섹션은 웹 구성 파일의 &lt;system.web&gt; 섹션 내에 표시 되어야 합니다.

**목록 6 – web.config에 대 한 캐싱 섹션**

[!code-xml[Main](improving-performance-with-output-caching-cs/samples/sample6.xml)]

목록 7의 컨트롤러는 [OutputCache] 특성을 사용 하 여 Cache1Hour 프로필을 컨트롤러 작업에 적용 하는 방법을 보여 줍니다.

**목록 7 – Controllers\ProfileController.cs**

[!code-csharp[Main](improving-performance-with-output-caching-cs/samples/sample7.cs)]

목록 7에서 컨트롤러에 의해 노출 된 Index () 작업을 호출 하면 1 시간 동안 동일한 시간이 반환 됩니다.

## <a name="summary"></a>요약

출력 캐싱은 ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있는 매우 간단한 방법을 제공 합니다. 이 자습서에서는 [OutputCache] 특성을 사용 하 여 컨트롤러 작업의 출력을 캐시 하는 방법을 배웠습니다. 또한 기간 및 VaryByParam 속성 같은 [OutputCache] 특성의 속성을 수정 하 여 콘텐츠를 캐시 하는 방법을 수정 하는 방법을 배웠습니다. 마지막으로 웹 구성 파일에서 캐시 프로필을 정의 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](understanding-action-filters-cs.md)
> [다음](adding-dynamic-content-to-a-cached-page-cs.md)
