---
uid: mvc/overview/performance/bundling-and-minification
title: 묶음 및 축소 | Microsoft Docs
author: Rick-Anderson
description: 번들 및 축소는 요청 로드 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있는 두 가지 기술입니다. 묶음 및 축소를 통해 reducin 로드 시간이 향상 됩니다.
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 61bfe5dbac04b57e1461183b66ead2f01fe0734c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457767"
---
# <a name="bundling-and-minification"></a>묶음 및 축소

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 번들 및 축소는 요청 로드 시간을 개선 하기 위해 ASP.NET 4.5에서 사용할 수 있는 두 가지 기술입니다. 묶음 및 축소는 서버에 대 한 요청 수를 줄이고 요청한 자산의 크기 (예: CSS 및 JavaScript)를 줄임으로써 로드 시간을 향상 시킵니다.

현재 주요 브라우저의 대부분은 각 호스트 이름에 대 한 [동시 연결](http://www.browserscope.org/?category=network) 수를 6 개로 제한 합니다. 즉, 6 개의 요청을 처리 하는 동안 호스트의 자산에 대 한 추가 요청이 브라우저에 의해 큐에 대기 됩니다. 아래 이미지에서 IE F12 개발자 도구 네트워크 탭은 샘플 응용 프로그램의 정보 보기에 필요한 자산의 타이밍을 보여 줍니다.

![B/M](bundling-and-minification/_static/image1.png)

회색 막대는 브라우저가 6 개의 연결 제한을 기다리는 요청을 큐에 대기 하는 시간을 표시 합니다. 노란색 막대는 첫 번째 바이트 까지의 요청 시간, 즉 요청을 보내고 서버에서 첫 번째 응답을 수신 하는 데 걸린 시간입니다. 파란색 막대에는 서버에서 응답 데이터를 수신 하는 데 걸린 시간이 표시 됩니다. 자산을 두 번 클릭 하 여 자세한 타이밍 정보를 얻을 수 있습니다. 예를 들어 다음 이미지에서는 */Scripts/MyScripts/JavaScript6.js* 파일을 로드 하기 위한 타이밍 정보를 보여 줍니다.

![](bundling-and-minification/_static/image2.png)

위의 이미지는 브라우저가 동시 연결 수를 제한 하기 때문에 요청이 큐에 대기 된 시간을 제공 하는 **시작** 이벤트를 보여 줍니다. 이 경우 요청은 다른 요청이 완료 되기를 기다리는 데 46 밀리초 동안 대기 되었습니다.

## <a name="bundling"></a>번들링

번들은 여러 파일을 단일 파일로 쉽게 결합 하거나 묶을 수 있는 ASP.NET 4.5의 새로운 기능입니다. CSS, JavaScript 및 기타 번들을 만들 수 있습니다. 파일이 적을수록 HTTP 요청은 줄어들고 첫 페이지 로드 성능을 향상 시킬 수 있습니다.

다음 그림은 이전에 표시 된 정보 보기의 동일한 타이밍 뷰를 보여 주지만 이번에는 묶음 및 축소를 사용 하도록 설정 했습니다.

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>필터로

축소는 불필요 한 공백과 주석을 제거 하 고 변수 이름을 한 문자로 단축 하는 것과 같이 스크립트나 css에 대 한 다양 한 코드 최적화를 수행 합니다. 다음 JavaScript 함수를 살펴보겠습니다.

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

축소 후 함수는 다음과 같이 줄어듭니다.

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

주석과 불필요 한 공백을 제거 하는 것 외에도 다음과 같은 매개 변수 이름과 변수 이름은 다음과 같이 변경 되었습니다 (약식).

| **Original** | **바꿔야** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>묶음 및 축소의 영향

다음 표에서는 샘플 프로그램에서 모든 자산을 개별적으로 나열 하 고 묶음 및 축소 (B/M)를 사용 하는 경우의 몇 가지 중요 한 차이점을 보여 줍니다.

|  | **B/M 사용** | **B/M 없음** | **변경** |
| --- | --- | --- | --- |
| **파일 요청** | 9 | 34 | 256% |
| **보낸 KB** | 3.26 | 11.92 | 266% |
| **받은 KB** | 388.51 | 530 | 36% |
| **로드 시간** | 510 MS | 780 MS | 53% |

브라우저에서 요청에 적용 하는 HTTP 헤더를 사용 하 여 브라우저에서 매우 자세한 정보를 보내기 때문에 전송 된 바이트는 묶음을 크게 줄일 수 있습니다. 가장 큰 파일 (*스크립트\\jquery-ui-1.8.11* 및 *스크립트\\jquery-1.10.2.min.js 1.7.1 for*)은 이미 미리 알고 있으므로 수신 된 바이트 감소는 크지 않습니다. 참고: 샘플 프로그램의 타이밍은 [Fiddler](http://www.fiddler2.com/fiddler2/) 도구를 사용 하 여 저속 네트워크를 시뮬레이션 했습니다. Fiddler **규칙** 메뉴에서 **성능** 을 선택 하 고 **모뎀 속도를 시뮬레이션**합니다.

## <a name="debugging-bundled-and-minified-javascript"></a>번들로 제공 되는 JavaScript 디버깅

JavaScript 파일이 번들로 또는 이상 확인할 수 없기 때문에 *web.config* 파일의 [컴파일 요소가](https://msdn.microsoft.com/library/s10awwz0.aspx) `debug="true"`로 설정 된 개발 환경에서 javascript를 쉽게 디버그할 수 있습니다. JavaScript 파일이 번들로 표시 되 고 표시 되지 않는 릴리스 빌드를 디버그할 수도 있습니다. IE F12 개발자 도구를 사용 하 여 다음 방법을 사용 하 여 축소 된 번들에 포함 된 JavaScript 함수를 디버그할 수 있습니다.

1. **스크립트** 탭을 선택 하 고 **디버깅 시작** 단추를 선택 합니다.
2. 자산 단추를 사용 하 여 디버깅 하려는 JavaScript 함수가 포함 된 번들을 선택 합니다.  
    ![](bundling-and-minification/_static/image4.png)
3. **구성 단추** ![](bundling-and-minification/_static/image5.png)선택 하 고 **javascript 서식**을 선택 하 여 선택 되지 않은 javascript의 형식을 지정 합니다.
4. **검색 스크립트** 입력 상자에서 디버깅 하려는 함수의 이름을 선택 합니다. 다음 이미지에서는 **검색 스크립트** 입력 상자에 **Addalttoimg** 가 입력 되었습니다.  
    ![](bundling-and-minification/_static/image6.png)

F12 개발자 도구를 사용 하 여 디버깅 하는 방법에 대 한 자세한 내용은 MSDN 문서 [f12 개발자 도구를 사용 하 여 JavaScript 오류 디버그를](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)참조 하세요.

## <a name="controlling-bundling-and-minification"></a>묶음 및 축소 제어

*Web.config 파일의* [컴파일 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 있는 debug 특성의 값을 설정 하 여 묶음 및 축소를 사용 하거나 사용 하지 않도록 설정 합니다. 다음 XML에서는를 true로 설정 하 여 묶음 및 축소를 사용 하지 않도록 설정 `debug`.

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

묶음 및 축소를 사용 하도록 설정 하려면 `debug` 값을 "false"로 설정 합니다. `BundleTable` 클래스의 `EnableOptimizations` 속성을 사용 *하 여 web.config 설정을 재정의할* 수 있습니다. 다음 코드에서는 묶음 및 축소를 사용 하도록 설정 하 고 web.config *파일의* 설정을 재정의 합니다.

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> `EnableOptimizations`를 `true` 하거나 *web.config* 파일의 [컴파일 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 있는 debug 특성을 `false`로 설정 하지 않는 한 파일은 번들로 묶여 있지 않습니다. 또한 파일의 최소 버전은 사용 되지 않으므로 전체 디버그 버전이 선택 됩니다. `EnableOptimizations`은 Web.config 파일의 [컴파일 요소](https://msdn.microsoft.com/library/s10awwz0.aspx) 에 있는 debug 특성을 재정의 합니다 *.*

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>ASP.NET Web Forms 및 웹 페이지에서 묶음 및 축소 사용

- 웹 페이지의 경우 웹 [페이지에 웹 최적화 추가](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site)블로그 항목을 참조 하세요.
- Web Forms [Web Forms에 묶음 및 축소 추가](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)블로그 항목을 참조 하세요.

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>ASP.NET MVC에서 묶음 및 축소 사용

이 섹션에서는 묶음 및 축소를 검사 하는 ASP.NET MVC 프로젝트를 만듭니다. 먼저 기본값을 변경 하지 않고 **Mvcbm** 관계 라는 새 ASP.NET MVC 인터넷 프로젝트를 만듭니다.

*앱\\\_시작\\BundleConfig.cs* 파일을 열고 번들을 만들고 등록 하 고 구성 하는 데 사용 되는 `RegisterBundles` 메서드를 검사 합니다. 다음 코드는 `RegisterBundles` 메서드의 일부를 보여 줍니다.

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

앞의 코드는 적절 한 모든을 포함 하는 *~/bundles/jquery* 라는 새 JavaScript 번들을 만듭니다."~/Scripts/jquery-{version}.js" 와일드 카드 문자열과 일치 하는 *Scripts* 폴더의 파일입니다. ASP.NET MVC 4의 경우 즉, 디버그 구성을 사용 하면 *jquery-1.10.2.min.js 1.7.1 for* 파일이 번들에 추가 됩니다. 릴리스 구성에서는 *jquery-1.10.2.min.js 1.7.1 for* 가 추가 됩니다. 번들 프레임 워크는 다음과 같은 몇 가지 일반적인 규칙을 따릅니다.

- *Filex. min .js* 및 *filex* 가 있는 경우 릴리스에 대 한 ". min" 파일을 선택 합니다.
- 디버그할 ". min" 버전이 아닌 버전을 선택 합니다.
- IntelliSense 에서만 사용 되는 "-vsdoc" 파일 (예: *jquery-1.10.2.min.js 1.7.1 for-vsdoc .js*)을 무시 합니다.

위에 표시 된 것과 같은 `{version}` 와일드 카드를 사용 하 여 *스크립트* 폴더에 적절 한 버전의 jquery를 사용 하는 jquery 번들을 자동으로 만듭니다. 이 예제에서 와일드 카드를 사용 하면 다음과 같은 이점이 있습니다.

- 에서는 NuGet을 사용 하 여 보기 페이지에서 이전 번들 코드 또는 jQuery 참조를 변경 하지 않고 최신 jQuery 버전으로 업데이트할 수 있습니다.
- 는 디버그 구성에 대해 전체 버전을 자동으로 선택 하 고 릴리스 빌드의 경우 ". min" 버전을 자동으로 선택 합니다.

## <a name="using-a-cdn"></a>CDN 사용

 다음 코드는 로컬 jQuery 번들을 CDN jQuery 번들로 바꿉니다.

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

위의 코드에서 jQuery는 릴리스 모드에 있는 동안 CDN에서 요청 되며 jQuery의 디버그 버전은 디버그 모드에서 로컬로 인출 됩니다. Cdn을 사용 하는 경우 CDN 요청이 실패 하는 경우 대체 메커니즘을 사용 해야 합니다. 레이아웃 파일의 끝에서 다음 태그 조각에는 CDN이 실패할 경우 요청 jQuery에 추가 된 스크립트가 표시 됩니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>번들 만들기

[번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `Include` 메서드는 문자열 배열을 사용 합니다. 여기서 각 문자열은 리소스의 가상 경로입니다. *응용 프로그램\\\_Start\\BundleConfig.cs* 파일의 `RegisterBundles` 메서드에서 다음 코드는 번들에 여러 파일을 추가 하는 방법을 보여 줍니다.

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

[번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` 메서드는 검색 패턴과 일치 하는 디렉터리 (및 선택적으로 모든 하위 디렉터리)에 모든 파일을 추가 하기 위해 제공 됩니다. [번들](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) 클래스 `IncludeDirectory` API는 다음과 같습니다.

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

번들은 Render 메서드를 사용 하 여 뷰에서 참조 됩니다 (CSS 및 JavaScript의 `Scripts.Render`에 대 한`Styles.Render`). *보기\\공유\\\_레이아웃* 의 다음 태그는 기본 ASP.NET 인터넷 프로젝트 뷰에서 CSS 및 JavaScript 번들을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

Render 메서드는 문자열 배열을 사용 하므로 한 줄의 코드에서 여러 번들을 추가할 수 있습니다. 일반적으로 자산을 참조 하는 데 필요한 HTML을 만드는 Render 메서드를 사용 하는 것이 좋습니다. `Url` 메서드를 사용 하 여 자산을 참조 하는 데 필요한 태그 없이 자산에 대 한 URL을 생성할 수 있습니다. 새 HTML5 [async](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async) 특성을 사용 한다고 가정 합니다. 다음 코드에서는 `Url` 메서드를 사용 하 여 modernizr를 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>"\*" 와일드 카드 문자를 사용 하 여 파일 선택

`Include` 메서드에 지정 된 가상 경로와 `IncludeDirectory` 메서드의 검색 패턴은 마지막 경로 세그먼트에서 접두사 또는 접미사로 "\*" 와일드 카드 문자 하나를 사용할 수 있습니다. 검색 문자열은 대/소문자를 구분 하지 않습니다. `IncludeDirectory` 메서드에는 하위 디렉터리를 검색할 수 있는 옵션이 있습니다.

다음 JavaScript 파일이 포함 된 프로젝트를 생각해 보세요.

- *스크립트\\Common\\AddAltToImg.*
- *스크립트\\일반적인\\ToggleDiv*
- *스크립트\\일반적인\\ToggleImg*
- *스크립트\\일반\\Sub1\\ToggleLinks*

![dir imag](bundling-and-minification/_static/image7.png)

다음 표에서는 표시 된 대로 와일드 카드를 사용 하 여 번들에 추가 된 파일을 보여 줍니다.

| **Call** | **추가 된 파일 또는 예외 발생** |
| --- | --- |
| Include ("~/Scripts/Common/\*.js") | *Addalttoimg*, *ToggleDiv*, *ToggleImg* |
| Include ("~/Scripts/Common/T\*.js") | 잘못 된 패턴 예외입니다. 와일드 카드 문자는 접두사 또는 접미사에만 사용할 수 있습니다. |
| Include ("~/Scripts/Common/\*og.\*") | 잘못 된 패턴 예외입니다. 와일드 카드 문자는 하나만 사용할 수 있습니다. |
| Include ("~/Scripts/Common/T\*") | *ToggleDiv*, *ToggleImg* |
| Include ("~/Scripts/Common/\*") | 잘못 된 패턴 예외입니다. 순수 와일드 카드 세그먼트가 잘못 되었습니다. |
| IncludeDirectory ("~/Scripts/Common", "T\*") | *ToggleDiv*, *ToggleImg* |
| IncludeDirectory ("~/Scripts/Common", "T\*", true) | *ToggleDiv*, *ToggleImg*, *ToggleLinks* |

각 파일을 번들에 명시적으로 추가 하는 것은 일반적으로 다음과 같은 이유로 파일의 와일드 카드 로드 보다 선호 됩니다.

- 와일드 카드 기본값으로 스크립트를 추가 하 여 사전순으로 로드 합니다 .이는 일반적으로 원하는 항목이 아닙니다. CSS 및 JavaScript 파일을 특정 (영문자가 아닌) 순서로 추가 해야 하는 경우가 자주 있습니다. 사용자 지정 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현을 추가 하 여이 위험을 완화할 수 있지만 각 파일을 명시적으로 추가 하면 오류가 발생 하기 쉽습니다. 예를 들어 나중에 [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) 구현을 수정 해야 할 수 있는 폴더에 새 자산을 추가할 수 있습니다.
- 와일드 카드 로드를 사용 하 여 디렉터리에 추가 된 특정 파일 보기는 해당 번들을 참조 하는 모든 보기에 포함 될 수 있습니다. 특정 보기 스크립트를 번들에 추가 하면 번들을 참조 하는 다른 보기에서 JavaScript 오류가 발생할 수 있습니다.
- 다른 파일을 가져오는 CSS 파일의 결과로 가져온 파일이 두 번 로드 됩니다. 예를 들어 다음 코드는 대부분의 jQuery UI 테마 CSS 파일을 두 번 로드 하 여 번들을 만듭니다. 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  와일드 카드 선택기 "\*. s i s"는 *콘텐츠\\테마\\기본\\jquery. .css* 파일을 포함 하 여 각 css 파일을 폴더에 가져옵니다. *Jquery. .css* 파일은 다른 css 파일을 가져옵니다.

## <a name="bundle-caching"></a>번들 캐싱

번들을 만들 때 번들에서 1 년 동안 HTTP 만료 헤더를 설정 합니다. 이전에 본 페이지로 이동 하는 경우 Fiddler에서 번들에 대 한 조건부 요청을 만들지 않습니다. 즉, 번들에 대 한 HTTP GET 요청이 없고 서버에서 HTTP 304 응답이 없는 것을 볼 수 있습니다. IE가 F5 키를 사용 하 여 각 번들에 대 한 조건부 요청을 만들도록 강제할 수 있습니다 (각 번들에 대 한 HTTP 304 응답 생성). ^ F5 키를 사용 하 여 전체 새로 고침을 강제로 실행할 수 있습니다. 그러면 각 번들에 대해 HTTP 200 응답이 생성 됩니다.

다음 이미지는 Fiddler 응답 창의 **캐싱** 탭을 보여 줍니다.

![fiddler 캐싱 이미지](bundling-and-minification/_static/image8.png)

요청   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 는 번들 **Allmyscripts** 용 이며 쿼리 문자열 쌍 **v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**를 포함 합니다. 쿼리 문자열 **v** 에는 캐싱에 사용 되는 고유 식별자 인 값 토큰이 있습니다. 번들이 변경 되지 않는 한 ASP.NET 응용 프로그램은이 토큰을 사용 하 여 **Allmyscripts** 번들을 요청 합니다. 번들의 파일이 변경 되 면 ASP.NET 최적화 프레임 워크는 새 토큰을 생성 하 여 번들에 대 한 브라우저 요청이 최신 번들을 가져오도록 합니다.

IE9 F12 개발자 도구를 실행 하 고 이전에 로드 한 페이지로 이동 하는 경우 IE는 각 번들에 대 한 조건부 GET 요청 및 HTTP 304을 반환 하는 서버를 잘못 표시 합니다. CDNs를 사용 하 여 블로그 항목에서 조건부 요청이 수행 되었는지 여부를 확인 하는 데 문제가 발생 하 [고 웹 사이트 성능을 개선 하기 위해 만료 되](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)는 이유를 IE9 수 있습니다.

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS, CoffeeScript, SCSS, Sass 번들입니다.

번들 및 축소 프레임 워크는 [SCSS](http://sass-lang.com/), [Sass](http://sass-lang.com/), [LESS](http://www.dotlesscss.org/) 또는 [Coffeescript](http://coffeescript.org/)와 같은 중간 언어를 처리 하 고 결과 번들에 축소와 같은 변환을 적용 하는 메커니즘을 제공 합니다. 예를 들어, MVC 4 프로젝트에 [더 작은](http://www.dotlesscss.org/) 파일을 추가 하려면 다음을 수행 합니다.

1. 콘텐츠를 줄일 폴더를 만듭니다. 다음 예제에서는 *\\MyLess 폴더 콘텐츠* 를 사용 합니다.
2. 프로젝트에 **점** [없는 NuGet 패키지](http://www.dotlesscss.org/) 를 추가 합니다.  
    NuGet ![설치](bundling-and-minification/_static/image9.png)
3. [IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx) 인터페이스를 구현 하는 클래스를 추가 합니다. Less transform의 경우 다음 코드를 프로젝트에 추가 합니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. `LessTransform` 및 [CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx) 변환을 사용 하 여 더 작은 파일의 번들을 만듭니다. *앱\\_Start\\BundleConfig.cs* 파일의 `RegisterBundles` 메서드에 다음 코드를 추가 합니다.

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. LESS 번들을 참조 하는 모든 뷰에 다음 코드를 추가 합니다.

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>번들 고려 사항

번들을 만들 때 따라야 하는 좋은 규칙은 번들 이름에 "번들"을 접두사로 포함 하는 것입니다. 이로 인해 [라우팅 충돌이](https://forums.asp.net/post/5012037.aspx)발생할 수 있습니다.

번들에서 파일 하나를 업데이트 하면 번들 쿼리 문자열 매개 변수에 대 한 새 토큰이 생성 되 고 다음에 클라이언트가 번들을 포함 하는 페이지를 요청할 때 전체 번들이 다운로드 되어야 합니다. 각 자산이 개별적으로 나열 되는 기존 태그에서 변경 된 파일만 다운로드 됩니다. 자주 변경 되는 자산은 묶음에 적합 하지 않을 수 있습니다.

번들링 및 축소는 주로 첫 번째 페이지의 요청 로드 시간을 개선합니다. 웹 페이지를 요청 하 고 나면 브라우저는 자산 (JavaScript, CSS 및 이미지)을 캐시 하므로 같은 자산을 요청 하는 동일한 사이트의 페이지나 동일한 페이지를 요청 하는 경우 묶음 및 축소에서 성능 향상을 제공 하지 않습니다. 자산에 대해 expires 헤더를 올바르게 설정 하지 않고 묶음 및 축소를 사용 하지 않는 경우 브라우저의 최신 추론은 며칠 후에 부실 자산을 표시 하 고 브라우저에서 각 자산에 대 한 유효성 검사 요청을 요구 합니다. 이 경우 번들 및 축소를 통해 첫 번째 페이지 요청 후 성능이 향상 됩니다. 자세한 내용은 [CDNs를 사용 하 여 블로그를 참조 하 고 웹 사이트 성능을 향상 시키기 위해 만료](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)됩니다.

[CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)을 사용 하 여 각 호스트 이름에 대 한 6 개의 동시 연결에 대 한 브라우저 제한 사항을 완화할 수 있습니다. CDN에는 호스팅 사이트와 다른 호스트 이름이 있으므로 CDN의 자산 요청은 호스팅 환경에 대 한 6 개의 동시 연결 제한에 포함 되지 않습니다. CDN은 일반적인 패키지 캐싱과 edge 캐싱 이점을 제공할 수도 있습니다.

번들은 필요한 페이지에 의해 분할 되어야 합니다. 예를 들어 인터넷 응용 프로그램에 대 한 기본 ASP.NET MVC 템플릿은 jQuery와 별도의 jQuery 유효성 검사 번들을 만듭니다. 만든 기본 보기에는 입력이 없으며 값을 게시 하지 않으므로 유효성 검사 번들이 포함 되지 않습니다.

`System.Web.Optimization` 네임 스페이스는 *system.object*에서 구현 됩니다. 이는 *Antlr3*를 사용 하는 축소 기능을 위해 webgrease 라이브러리 (*webgrease .dll*)를 활용 합니다.

*Twitter를 사용 하 여 빠른 게시를 수행 하 고 링크를 공유 합니다. 내 Twitter 핸들*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>추가 리소스

- 비디오: [Howard Dierking](https://twitter.com/#!/howard_dierking) 에서[묶음 및 최적화](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)
- 웹 [페이지 사이트에 웹 최적화를 추가](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)합니다.
- [Web Forms에 묶음 및 축소를 추가](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)합니다.
- [Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk) 에서 [웹 검색을 통해 묶음 및 축소의 성능 영향](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)
- [CDNs 및를 사용 하](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) 여 Rick Anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) 의 웹 사이트 성능 향상
- [RTT (왕복 시간) 최소화](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>참가자

- Jia-hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
