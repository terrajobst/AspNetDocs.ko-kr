---
uid: aspnet/overview/owin-and-katana/an-overview-of-project-katana
title: Project Katana 개요 Microsoft Docs
author: howarddierking
description: ASP.NET 프레임 워크는 10 년 이상 사용 되었으며 플랫폼은 수많은 웹 사이트 및 서비스의 개발을 지원 합니다. 웹 응용 프로그램로 ...
ms.author: riande
ms.date: 08/30/2013
ms.assetid: 0ee21741-c1bf-4025-a9b0-24580cae24bc
msc.legacyurl: /aspnet/overview/owin-and-katana/an-overview-of-project-katana
msc.type: authoredcontent
ms.openlocfilehash: 1f28db822930cdfd2ebf4cf9bb27d173f4aa4201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500345"
---
# <a name="an-overview-of-project-katana"></a>프로젝트 Katana 개요

[Howard Dierking](https://github.com/howarddierking)

> ASP.NET 프레임 워크는 10 년 이상 사용 되었으며 플랫폼은 수많은 웹 사이트 및 서비스의 개발을 지원 합니다. 웹 응용 프로그램 개발 전략이 발전 함에 따라 프레임 워크는 ASP.NET MVC 및 ASP.NET Web API와 같은 기술을 사용 하 여 발전 시킬 수 있었습니다. 웹 응용 프로그램 개발에서 클라우드 컴퓨팅 세계에 대 한 다음 발전 단계를 수행 하기 때문에 project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) 는 ASP.NET 응용 프로그램에 대 한 기본 구성 요소 집합을 제공 하 여 유연 하 고 이식 가능 하며 경량 이며 더 나은 성능을 제공할 수 있습니다. 다른 방법으로 project [Katana](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET) cloud는 ASP.NET 응용 프로그램을 최적화 합니다.

## <a name="why-katana--why-now"></a>왜 Katana?

 개발자가 개발자 프레임 워크 또는 최종 사용자 제품을 설명 하 고 있는지 여부에 관계 없이 제품을 만드는 기본 동기를 이해 하는 것이 중요 합니다. 여기에는 제품을 만든 사람을 확인 하는 것이 포함 됩니다. ASP.NET는 원래 두 명의 고객과 함께 만들어졌습니다.   
  
**고객의 첫 번째 그룹은 기본 ASP 개발자 였습니다.** 당시 ASP는 태그 및 서버 쪽 스크립트를 interweaving 하 여 동적 데이터 기반 웹 사이트 및 응용 프로그램을 만들기 위한 기본 기술 중 하나 였습니다. 기본 HTTP 프로토콜 및 웹 서버의 핵심 측면을 추상화 하 고 세션 및 응용 프로그램 상태 관리, 캐시 등의 추가 서비스에 대 한 액세스를 제공 하는 개체 집합을 제공 하는 ASP 런타임은 서버 쪽 스크립트를 제공 합니다. 강력 하지만 기존 ASP 응용 프로그램은 크기와 복잡성이 증가 함에 따라 관리 하기가 쉽지 않습니다. 이는 주로 코드 및 태그 인터리브로 인해 발생 하는 코드의 중복과 결합 된 스크립팅 환경에서 발견 된 구조가 없기 때문입니다. 일부 문제를 해결 하는 동안 클래식 ASP의 장점에 대 한 대문자화를 위해 ASP.NET .NET Framework는 개체 지향 언어에서 제공 하는 코드 조직을 활용 하는 동시에 서버 쪽 프로그래밍 모델도 유지 합니다. 기존 ASP 개발자에 게 익숙한 것입니다.

**ASP.NET에 대 한 대상 고객의 두 번째 그룹은 Windows 비즈니스 응용 프로그램 개발자 였습니다.** HTML 태그를 작성 하 고 html 태그를 생성 하는 코드를 작성 하는 데 익숙한 기존 ASP 개발자와는 달리 WinForms 개발자 (이전에는 VB6 개발자)가 캔버스와 풍부한 사용자 집합을 포함 하는 디자인 타임 환경에 익숙합니다. 인터페이스 컨트롤. ASP.NET의 첫 번째 버전 ("Web Forms" 라고도 함)은 사용자 인터페이스 구성 요소에 대 한 서버 쪽 이벤트 모델과 유사한 디자인 타임 환경을 제공 하 고,이를 통해 ViewState와 같은 인프라 기능 집합을 제공 하 여 원활한 개발자 환경을 만들 수 있습니다. 클라이언트 및 서버 쪽 프로그래밍 WinForms 개발자에 게 친숙 한 상태 저장 이벤트 모델에서 웹의 상태 비저장 특성을 효과적으로 hid Web Forms 합니다.

### <a name="challenges-raised-by-the-historical-model"></a>기록 모델에서 발생 하는 문제

**결과적으로 풍부한 기능의 런타임 및 개발자 프로그래밍 모델이 있습니다.** 그러나이 기능을 사용 하는 경우 몇 가지 주목할 만한 과제가 제공 됩니다. 첫째, 프레임 워크는 논리적으로 서로 다른 기능 단위를 동일한 **모놀리식**어셈블리 (예: web forms 프레임 워크를 사용 하는 핵심 HTTP 개체)와 긴밀 하 게 결합 된 상태로 만들었습니다. 둘째로, ASP.NET는 더 큰 .NET Framework의 일부로 포함 되었으며 **릴리스 간의 시간이 연 순서에** 해당 합니다. 이로 인해 신속 하 게 진화 하는 웹 개발에서 발생 하는 모든 변경 사항을 ASP.NET 하는 데 어려움이 있었습니다. 마지막으로, System.web .dll 자체는 특정 웹 호스팅 옵션인 인터넷 정보 서비스 (IIS)와 몇 가지 다른 방법으로 결합 되었습니다.

### <a name="evolutionary-steps-aspnet-mvc-and-aspnet-web-api"></a>혁신적인 단계: ASP.NET MVC 및 ASP.NET Web API

웹 개발에서 많은 변화가 있었습니다. 웹 응용 프로그램은 점점 더 많은 프레임 워크가 아닌 일련의 작고 집중 된 구성 요소로 개발 되 고 있습니다. 구성 요소 수와 해당 구성 요소가 릴리스되는 빈도는 점점 더 빠른 속도로 늘어나고 있습니다. 웹을 사용 하는 데는 더 크고 더 많은 기능을 제공 하는 것이 아니라 더 작은 기능을 제공 하는 프레임 워크가 필요 합니다. 따라서 **ASP.NET 팀은 단일 프레임 워크가 아닌 플러그형 웹 구성 요소 제품군으로 ASP.NET을 사용 하기 위한 여러 가지 혁신적인 단계를 수행**했습니다.

초기 변경 내용 중 하나는 Ruby의 Ruby와 같은 웹 개발 프레임 워크 덕분에 잘 알려진 MVC (모델-뷰-컨트롤러) 디자인 패턴의 인기입니다. 이러한 웹 응용 프로그램 빌드 스타일을 통해 개발자는 ASP.NET의 초기 판매 시점 중 하나인 태그와 비즈니스 논리의 분리를 유지 하면서 응용 프로그램의 태그를 더 강력 하 게 제어할 수 있습니다. 이러한 스타일의 웹 응용 프로그램 개발에 대 한 수요를 충족 하기 위해 Microsoft는 **ASP.NET MVC를 대역 외에서 개발** 하 여 (그리고 .NET Framework에 포함 하지 않고) 나중에 더 나은 위치를 제공할 수 있었습니다. ASP.NET MVC는 독립적인 다운로드로 릴리스 되었습니다. 이를 통해 엔지니어링 팀은 이전 보다 훨씬 더 자주 업데이트를 제공할 수 있는 유연성을 제공 했습니다.

웹 응용 프로그램 개발의 또 다른 주요 변화는 **AJAX 요청을 통해 백 엔드 웹 api와**통신 하는 클라이언트 쪽 스크립트에서 생성 된 페이지의 동적 섹션을 사용 하 여 서버에서 생성 된 동적 웹 페이지에서 정적 초기 태그로의 이동 이었습니다. 이 아키텍처 시프트는 웹 Api의 propel 및 ASP.NET Web API 프레임 워크의 개발에 도움이 됩니다. ASP.NET MVC의 경우와 마찬가지로 ASP.NET Web API 릴리스에서는 더 많은 모듈식 프레임 워크로 ASP.NET를 한층 더 발전 시킬 수 있는 기회를 제공 했습니다. 엔지니어링 팀이 기회 및 빌드 ASP.NET Web API를 활용 하 여 **system.web에서 찾은 핵심 프레임 워크 형식에 종속 되지 않도록 했습니다**. 이 기능을 사용 하도록 설정 하는 두 가지 작업이 있습니다. 첫 번째는 ASP.NET Web API 완전히 자체 포함 된 방식으로 발전할 수 있음을 의미 하며, NuGet을 통해 전달 되기 때문에 계속 해 서 신속 하 게 반복할 수 있습니다. 둘째, System.web에 대 한 외부 종속성이 없으므로 IIS에 대 한 종속성이 없으므로 사용자 지정 호스트에서 실행할 수 있는 기능 (예: 콘솔 응용 프로그램, Windows 서비스 등)이 포함 ASP.NET Web API.

### <a name="the-future-a-nimble-framework"></a>미래: 민첩 프레임 워크

프레임 워크 구성 요소를 다른 구성 요소에서 분리 한 다음 NuGet에서 해제 하 여 프레임 워크는 이제 **보다 독립적이 고 더 빠르게 반복**될 수 있습니다. 또한 Web API의 자체 호스팅 기능을 강력 하 고 유연 하 게 관리할 **수 있는 개발자** 에 게 매우 매력적인 서비스를 원했습니다. 이는 다른 프레임 워크 에서도이 기능을 필요로 하는 것을 입증 했으며,이는 각 프레임 워크가 자체의 기본 주소에서 자체 호스트 프로세스로 실행 되 고 독립적으로 관리 (시작, 중지 등) 해야 한다는 점에서 새로운 문제를 겪고 있습니다. 최신 웹 응용 프로그램은 일반적으로 정적 파일 처리, 동적 페이지 생성, 웹 API 및 최근 실시간/푸시 알림을 지원 합니다. 이러한 각 서비스를 실행 하 고 독립적으로 관리 해야 하는 것은 간단 하지 않습니다.

개발자가 다양 한 구성 요소와 프레임 워크에서 응용 프로그램을 작성 한 다음 지원 호스트에서 해당 응용 프로그램을 실행할 수 있도록 하는 단일 호스팅 추상화가 필요 합니다.

## <a name="the-open-web-interface-for-net-owin"></a>OWIN (Open Web Interface for .NET)

 Ruby 커뮤니티의 [랙에](http://rack.github.io/) 의해 제공 되는 혜택을 통해 .net 커뮤니티의 여러 멤버가 웹 서버와 프레임 워크 구성 요소 간의 추상화를 만들도록 설정 했습니다. OWIN 추상화에 대 한 두 가지 디자인 목표는 간단 하 고 다른 프레임 워크 형식에 대해 가능한 최소한의 종속성을 가져왔습니다. 이러한 두 가지 목표는 다음을 확인 하는 데 도움이 됩니다.

- 새 구성 요소를 보다 쉽게 개발 하 고 소비할 수 있습니다.
- 응용 프로그램은 호스트와 잠재적으로 전체 플랫폼/운영 체제 간에 더 쉽게 이식할 수 있습니다.

결과 추상화는 두 개의 핵심 요소로 구성 됩니다. 첫 번째는 환경 사전입니다. 이 데이터 구조는 모든 관련 서버 상태 뿐만 아니라 HTTP 요청 및 응답을 처리 하는 데 필요한 모든 상태를 저장 합니다. 환경 사전은 다음과 같이 정의 됩니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample1.cmd)]

OWIN 호환 웹 서버는 HTTP 요청 및 응답에 대 한 본문 스트림 및 헤더 컬렉션과 같은 데이터를 사용 하 여 환경 사전을 채우는 역할을 합니다. 그런 다음 응용 프로그램 또는 프레임 워크 구성 요소는 사전을 추가 값으로 채우거 나 업데이트 하 고 응답 본문 스트림에 써야 합니다.

환경 사전의 유형을 지정 하는 것 외에도 OWIN 사양은 코어 사전 키 값 쌍의 목록을 정의 합니다. 예를 들어 다음 표에는 HTTP 요청에 대 한 필수 사전 키가 나와 있습니다.

| 키 이름 | 값 설명 |
| --- | --- |
| `"owin.RequestBody"` | 요청 본문 (있는 경우)을 포함 하는 스트림입니다. Stream. 요청 본문이 없는 경우 Null을 자리 표시자로 사용할 수 있습니다. [요청 본문](http://owin.org/html/owin.html#34-request-body-100-continue-and-completed-semantics)을 참조 하세요. |
| `"owin.RequestHeaders"` | 요청 헤더의 `IDictionary<string, string[]>`입니다. [헤더](http://owin.org/html/owin.html#3-3-headers)를 참조 하세요. |
| `"owin.RequestMethod"` | 요청에 대 한 HTTP 요청 메서드 (예: `"GET"`, `"POST"`)를 포함 하는 `string`입니다. |
| `"owin.RequestPath"` | 요청 경로를 포함 하는 `string`입니다. 경로는 응용 프로그램 대리자의 "루트"에 상대적 이어야 합니다. [경로](http://owin.org/html/owin.html#5-3-paths)를 참조 하세요. |
| `"owin.RequestPathBase"` | 응용 프로그램 대리자의 "루트"에 해당 하는 요청 경로의 일부를 포함 하는 `string`입니다. [경로](http://owin.org/html/owin.html#5-3-paths)를 참조 하세요. |
| `"owin.RequestProtocol"` | 프로토콜 이름 및 버전이 포함 된 `string` (예: `"HTTP/1.0"` 또는 `"HTTP/1.1"`) |
| `"owin.RequestQueryString"` | 앞에 "?"가 없는 HTTP 요청 URI의 쿼리 문자열 구성 요소가 포함 된 `string` (예: `"foo=bar&baz=quux"`). 값은 빈 문자열일 수 있습니다. |
| `"owin.RequestScheme"` | 요청에 사용 되는 URI 체계를 포함 하는 `string` (예: `"http"`, `"https"`) [URI 체계](http://owin.org/html/owin.html#5-1-uri-scheme)를 참조 하세요. |

OWIN의 두 번째 주요 요소는 응용 프로그램 대리자입니다. OWIN 응용 프로그램의 모든 구성 요소 간의 기본 인터페이스 역할을 하는 함수 서명입니다. 응용 프로그램 대리자의 정의는 다음과 같습니다.

`Func<IDictionary<string, object>, Task>;`

그런 다음 응용 프로그램 대리자는 함수가 환경 사전을 입력으로 수락 하 고 작업을 반환 하는 Func 대리자 형식의 구현 일 뿐입니다. 이 디자인은 개발자에 게 다음과 같은 영향을 미칩니다.

- OWIN 구성 요소를 작성 하는 데 필요한 형식 종속성이 매우 적습니다. 이렇게 하면 개발자에 게 OWIN의 접근성이 크게 향상 됩니다.
- 비동기 디자인을 사용 하면 특히 i/o를 많이 사용 하는 작업을 통해 컴퓨팅 리소스의 처리를 효율적으로 수행할 수 있습니다.
- 응용 프로그램 대리자는 실행의 원자성 단위 이며 환경 사전은 대리자에서 매개 변수로 전달 되기 때문에 OWIN 구성 요소를 쉽게 연결 하 여 복잡 한 HTTP 처리 파이프라인을 만들 수 있습니다.

구현 관점에서 OWIN은 사양 ([http://owin.org/html/owin.html](http://owin.org/html/owin.html))입니다. 그 목표는 다음 웹 프레임 워크가 아니라 웹 프레임 워크와 웹 서버가 상호 작용 하는 방식에 대 한 사양입니다.

[OWIN](http://owin.org/) 또는 [Katana](https://github.com/aspnet/AspNetKatana/wiki)를 조사 했다면 [OWIN NuGet 패키지](http://nuget.org/packages/Owin) 및 OWIN도 확인할 수 있습니다. 이 라이브러리에는 OWIN 사양의 [4 단원](http://owin.org/html/owin.html#4-application-startup) 에 설명 된 시작 시퀀스를 공식화 하 고 체계화 하는 [iappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs)의 단일 인터페이스가 포함 되어 있습니다. OWIN 서버를 작성 하는 데 필요한 것은 아니지만 [Iappbuilder](https://github.com/owin/owin/blob/master/src/Owin/IAppBuilder.cs) 인터페이스는 구체적 참조 지점을 제공 하며 Katana 프로젝트 구성 요소에서 사용 됩니다.

## <a name="project-katana"></a>프로젝트 Katana

[OWIN](http://owin.org/html/owin.html) 사양과 *OWIN* 는 모두 커뮤니티 소유 이며 커뮤니티에서 오픈 소스를 실행 하는 반면, [Katana](https://github.com/aspnet/AspNetKatana/wiki) 프로젝트는 오픈 소스에서 MICROSOFT가 빌드하고 출시 하는 OWIN 구성 요소 집합을 나타냅니다. 이러한 구성 요소에는 호스트 및 서버와 같은 인프라 구성 요소와 [SignalR](../../../signalr/index.md) 및 [ASP.NET Web API](../../../web-api/overview/getting-started-with-aspnet-web-api/index.md)같은 프레임 워크에 대 한 바인딩 구성 요소와 같은 기능 구성 요소가 포함 됩니다. 프로젝트에는 다음과 같은 세 가지 높은 수준의 목표가 있습니다. 

- **이식** 가능 – 구성 요소가 사용할 수 있게 되 면 새 구성 요소를 쉽게 대체할 수 있습니다. 여기에는 프레임 워크에서 서버 및 호스트로 모든 유형의 구성 요소가 포함 됩니다. 이러한 목표는 타사 프레임 워크가 Microsoft 서버에서 원활 하 게 실행 될 수 있는 반면 Microsoft 프레임 워크는 타사 서버 및 호스트에서 실행 될 수 있다는 것을 의미 합니다.
- **모듈식/유연한**기능-기본적으로 설정 되는 방대한 기능을 포함 하는 많은 프레임 워크와 달리, Katana 프로젝트 구성 요소는 작고 집중 되어야 하며 응용 프로그램 개발자에 게 응용 프로그램에 사용할 구성 요소를 결정 하는 제어 기능을 제공 합니다.
- 간단 하 고 성능이 **뛰어나고 확장 가능** 합니다. 프레임 워크의 기존 개념을 응용 프로그램 개발자가 명시적으로 추가 하는 소규모의 작은 구성 요소 집합으로 나누면 그 결과 Katana 응용 프로그램은 더 적은 컴퓨팅 리소스를 소비할 수 있으며 그 결과 다른 유형의 서버 및 프레임 워크 보다 더 많은 부하를 처리할 수 있습니다. 응용 프로그램의 요구 사항에 따라 기본 인프라에서 더 많은 기능을 요구 하기 때문에 OWIN 파이프라인에 추가 될 수 있지만 응용 프로그램 개발자의 일부에 대 한 명시적인 결정을 내려야 합니다. 또한 하위 수준 구성 요소의 substitutability는 사용할 수 있게 되 면 새로운 고성능 서버를 원활 하 게 도입 하 여 응용 프로그램을 손상 시 키 지 않고 OWIN 응용 프로그램의 성능을 향상 시킬 수 있음을 의미 합니다.

## <a name="getting-started-with-katana-components"></a>Katana 구성 요소 시작 하기

처음 도입 된 경우, 사용자의 주의가 즉시 제공 되는 [node.js](http://nodejs.org/) 프레임 워크의 한 가지 측면은 웹 서버를 작성 하 고 실행할 수 있는 단순성 이었습니다. Katana 목표가 [node.js](http://nodejs.org/)에 포함 된 경우 개발자가 ASP.NET 웹 응용 프로그램 개발에 대해 알고 있는 모든 것을 강제로 제공 하지 않고도 Katana [(및](http://nodejs.org/) 이와 유사한 프레임 워크)의 많은 이점을 제공 한다는 것을 설명 하 여이를 요약할 수 있습니다. 이 문이 true를 유지 하려면 Katana 프로젝트를 시작 하는 것은 [node.js](http://nodejs.org/)에 대 한 특성의 성격을 동일 하 게 유지 해야 합니다.

## <a name="creating-hello-world"></a>"Hello World!"을 (를) 만드는 중

JavaScript와 .NET 개발의 중요 한 차이점 중 하나는 컴파일러의 존재 여부입니다. 따라서 간단한 Katana 서버의 시작 지점은 Visual Studio 프로젝트입니다. 그러나 비어 있는 ASP.NET 웹 응용 프로그램의 프로젝트 형식 중에서 가장 적은 작업을 시작할 수 있습니다.

[![](an-overview-of-project-katana/_static/image1.png)](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb)

다음에는 [Owin 웹](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) NuGet 패키지를 프로젝트에 설치 합니다. 이 패키지는 ASP.NET 요청 파이프라인에서 실행 되는 OWIN 서버를 제공 합니다. [NuGet 갤러리](http://nuget.org/packages/Microsoft.Owin.Host.SystemWeb) 에서 찾을 수 있으며 다음 명령을 사용 하 여 Visual Studio 패키지 관리자 대화 상자 또는 패키지 관리자 콘솔을 사용 하 여 설치할 수 있습니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample2.cmd)]

`Microsoft.Owin.Host.SystemWeb` 패키지를 설치 하면 몇 가지 추가 패키지를 종속성으로 설치 합니다. 이러한 종속성 중 하나는 OWIN 응용 프로그램을 개발 하기 위한 몇 가지 도우미 형식 및 메서드를 제공 하는 라이브러리인 `Microsoft.Owin`입니다. 이러한 형식을 사용 하 여 다음 "hello 세계" 서버를 신속 하 게 작성할 수 있습니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample3.cs)]

이제 Visual Studio의 **F5** 명령을 사용 하 여 매우 간단한이 웹 서버를 실행 하 고 디버깅을 완벽 하 게 지원할 수 있습니다.

## <a name="switching-hosts"></a>호스트 전환

기본적으로 이전 "hello 세계" 예제는 IIS의 컨텍스트에서 System.web를 사용 하는 ASP.NET request 파이프라인에서 실행 됩니다. 이는 자체를 사용 하 여 OWIN 파이프라인의 유연성과 composability에서 관리 기능 및 전체 IIS 완성도를 활용할 수 있으므로 엄청난 가치를 추가할 수 있습니다. 그러나 IIS에서 제공 하는 혜택이 필요 하지 않으며 더 작고 간단한 호스트에 대 한 혜택이 있는 경우가 있을 수 있습니다. IIS 및 System.web 외부에서 간단한 웹 서버를 실행 하려면 어떻게 해야 하나요?

이식성 목표를 설명 하기 위해 웹 서버 호스트에서 명령줄 호스트로 이동 하는 경우에는 단순히 새 서버 및 호스트 종속성을 프로젝트의 출력 폴더에 추가한 다음 호스트를 시작 해야 합니다. 이 예제에서는 `OwinHost.exe` 이라는 Katana 호스트에 웹 서버를 호스팅하고 Katana HttpListener 기반 서버를 사용 합니다. 다른 Katana 구성 요소와 마찬가지로, 다음 명령을 사용 하 여 NuGet에서 가져올 수 있습니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample4.cmd)]

그런 다음 명령줄에서 프로젝트 루트 폴더로 이동 하 여 `OwinHost.exe` (해당 NuGet 패키지의 tools 폴더에 설치 된)만 실행할 수 있습니다. 기본적으로 `OwinHost.exe`는 HttpListener 기반 서버를 찾도록 구성 되므로 추가 구성이 필요 하지 않습니다. 웹 브라우저에서 `http://localhost:5000/`로 이동 하면 현재 콘솔을 통해 실행 중인 응용 프로그램이 표시 됩니다.

![](an-overview-of-project-katana/_static/image2.png)

## <a name="katana-architecture"></a>Katana 아키텍처

 Katana 구성 요소 아키텍처는 응용 프로그램을 *호스트, 서버, 미들웨어* 및 *응용 프로그램*등의 논리적 계층 4 개로 나눕니다. 구성 요소 아키텍처는 응용 프로그램을 다시 컴파일할 필요 없이 대부분의 경우 이러한 계층의 구현을 쉽게 대체할 수 있는 방법으로 구성 됩니다.   

![](an-overview-of-project-katana/_static/image3.png)

## <a name="host"></a>호스트

 호스트는 다음을 담당 합니다.

- 기본 프로세스 관리
- 서버를 선택 하 고 요청을 처리 하는 OWIN 파이프라인을 생성 하는 워크플로를 오케스트레이션 합니다.

  현재 Katana 기반 응용 프로그램에 대 한 세 가지 기본 호스팅 옵션이 있습니다.  
  
**Iis/asp.net**: 표준 HttpModule 및 HttpHandler 형식을 사용 하 여 OWIN 파이프라인은 ASP.NET 요청 흐름의 일부로 IIS에서 실행할 수 있습니다. 웹 응용 프로그램 프로젝트에 Microsoft ASP.NET 웹 NuGet 패키지를 설치 하 여 호스팅 지원을 사용할 수 있습니다. 또한 IIS는 호스트 및 서버 역할을 수행 하므로이 NuGet 패키지에 OWIN 서버/호스트의 차이가 있습니다. 즉, SystemWeb 호스트를 사용 하는 경우 개발자는 대체 서버 구현을 대체할 수 없습니다.  
  
**사용자 지정 호스트**: Katana 구성 요소 모음을 통해 개발자는 콘솔 응용 프로그램, Windows 서비스 등의 고유한 사용자 지정 프로세스에서 응용 프로그램을 호스팅할 수 있습니다. 이 기능은 Web API에서 제공 하는 자체 호스트 기능과 유사 합니다. 다음 예제에서는 Web API 코드의 사용자 지정 호스트를 보여 줍니다.  

[!code-csharp[Main](an-overview-of-project-katana/samples/sample5.cs)]

Katana 응용 프로그램에 대 한 자체 호스트 설치는 다음과 유사 합니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample6.cs)]

Web API와 Katana 자체 호스트 예제에서 주목할 만한 차이점 중 하나는 웹 API 구성 코드가 Katana 자체 호스트 예제에 없다는 것입니다. 이식성과 composability를 모두 사용 하기 위해 Katana는 서버를 시작 하는 코드를 요청 처리 파이프라인을 구성 하는 코드에서 분리 합니다. Web API를 구성 하는 코드는 시작 클래스에 포함 되어 있습니다 .이 클래스는 WebApplication. Start에서 형식 매개 변수로 추가로 지정 됩니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample7.cs)]

시작 클래스는이 문서의 뒷부분에서 자세히 설명 합니다. 그러나 Katana 자체 호스트 프로세스를 시작 하는 데 필요한 코드는 ASP.NET Web API 자체 호스트 응용 프로그램에서 현재 사용 하 고 있는 코드와 비슷합니다 strikingly.

**Owinhost**: 일부는 Katana 웹 응용 프로그램을 실행 하는 사용자 지정 프로세스를 작성 하려고 하지만, 대부분 서버를 시작 하 고 응용 프로그램을 실행할 수 있는 미리 작성 된 실행 파일을 시작 하는 것이 좋습니다. 이 시나리오의 경우 Katana 구성 요소 모음에 `OwinHost.exe`포함 됩니다. 프로젝트의 루트 디렉터리 내에서 실행 하는 경우이 실행 파일은 서버를 시작 하 고 (기본적으로 HttpListener 서버 사용) 규칙을 사용 하 여 사용자의 시작 클래스를 찾고 실행 합니다. 더 세부적인 제어를 위해 실행 파일은 다양 한 명령줄 매개 변수를 추가로 제공 합니다.

![](an-overview-of-project-katana/_static/image4.png)

## <a name="server"></a>서버

 호스트는 응용 프로그램이 실행 되는 프로세스의 시작 및 유지 관리를 담당 하는 반면 서버는 네트워크 소켓을 열고, 요청을 수신 하 고, 사용자가 지정한 OWIN 구성 요소의 파이프라인을 통해 전송 하는 것입니다. 이미 알고 있을 수 있습니다 .이 파이프라인은 응용 프로그램 개발자의 시작 클래스에서 지정 됩니다. 현재 Katana 프로젝트에는 두 개의 서버 구현이 포함 되어 있습니다. 

- **Owin 웹**: 앞에서 설명한 것 처럼 ASP.NET 파이프라인과 함께 사용 되는 IIS는 호스트와 서버 역할을 모두 수행 합니다. 따라서이 호스팅 옵션을 선택 하는 경우 IIS는 프로세스 활성화와 같은 호스트 수준 문제를 관리 하 고 HTTP 요청을 수신 합니다. ASP.NET 웹 응용 프로그램의 경우 요청을 ASP.NET 파이프라인으로 보냅니다. Katana SystemWeb 호스트는 HTTP 파이프라인을 통해 전달 되는 요청을 가로채서 사용자 지정 OWIN 파이프라인을 통해 보내는 ASP.NET HttpModule 및 HttpHandler를 등록 합니다.
- **Owin. HttpListener**: 이름에 따라이 Katana 서버는 .NET Framework의 HttpListener 클래스를 사용 하 여 소켓을 열고 개발자가 지정한 Owin 파이프라인으로 요청을 보냅니다. 이는 현재 Katana 자체 호스트 API와 OwinHost 모두에 대 한 기본 서버 선택입니다.

## <a name="middlewareframework"></a>미들웨어/프레임 워크

 앞에서 설명한 것 처럼 서버가 클라이언트의 요청을 수락 하면 개발자의 시작 코드에 지정 된 OWIN 구성 요소의 파이프라인을 통해 전달 해야 합니다. 이러한 파이프라인 구성 요소를 미들웨어 라고 합니다.  
 매우 기본적인 수준에서 OWIN 미들웨어 구성 요소는 단순히 OWIN 응용 프로그램 대리자를 구현 하 여 호출할 수 있도록 해야 합니다.

[!code-console[Main](an-overview-of-project-katana/samples/sample8.cmd)]

그러나 미들웨어 구성 요소의 개발과 컴퍼지션을 간소화 하기 위해 Katana는 미들웨어 구성 요소에 대 한 몇 가지 규칙과 도우미 유형을 지원 합니다. 가장 일반적인 방법은 `OwinMiddleware` 클래스입니다. 이 클래스를 사용 하 여 작성 된 사용자 지정 미들웨어 구성 요소는 다음과 유사 합니다. 

[!code-csharp[Main](an-overview-of-project-katana/samples/sample9.cs)]

 이 클래스는 `OwinMiddleware`에서 파생 되 고, 파이프라인의 다음 미들웨어 인스턴스를 해당 인수 중 하나로 수락한 다음 기본 생성자에 전달 하는 생성자를 구현 합니다. 미들웨어를 구성 하는 데 사용 되는 추가 인수도 다음 미들웨어 매개 변수 뒤에 생성자 매개 변수로 선언 됩니다.   
  
런타임에 미들웨어는 재정의 된 `Invoke` 메서드를 통해 실행 됩니다. 이 메서드는 `OwinContext`형식의 단일 인수를 사용 합니다. 이 컨텍스트 개체는 앞에서 설명한 `Microsoft.Owin` NuGet 패키지에서 제공 하며, 몇 가지 추가 도우미 형식과 함께 요청, 응답 및 환경 사전에 대 한 강력한 형식의 액세스를 제공 합니다.   
  
미들웨어 클래스는 응용 프로그램 시작 코드의 OWIN 파이프라인에 다음과 같이 쉽게 추가할 수 있습니다.   

[!code-csharp[Main](an-overview-of-project-katana/samples/sample10.cs)]

Katana 인프라는 단순히 OWIN 미들웨어 구성 요소의 파이프라인을 구축 하 고, 구성 요소가 파이프라인에 참여할 응용 프로그램 대리자를 지원 해야 하기 때문에 미들웨어 구성 요소는 단순로 거에서 ASP.NET, Web API, [SignalR](../../../signalr/index.md)등의 전체 프레임 워크로 복잡 한 범위를 만들 수 있습니다. 예를 들어 이전 OWIN 파이프라인에 ASP.NET Web API를 추가 하려면 다음 시작 코드를 추가 해야 합니다.

[!code-csharp[Main](an-overview-of-project-katana/samples/sample11.cs)]

Katana 인프라는 구성 메서드의 IAppBuilder 개체에 추가 된 순서에 따라 미들웨어 구성 요소의 파이프라인을 빌드합니다. 이 예제에서 LoggerMiddleware는 이러한 요청이 궁극적으로 처리 되는 방식에 관계 없이 파이프라인을 통해 흐르는 모든 요청을 처리할 수 있습니다. 이를 통해 미들웨어 구성 요소 (예: 인증 구성 요소)가 여러 구성 요소 및 프레임 워크 (예: ASP.NET Web API, SignalR 및 정적 파일 서버)를 포함 하는 파이프라인에 대 한 요청을 처리할 수 있는 강력한 시나리오를 사용할 수 있습니다.
 
## <a name="applications"></a>애플리케이션

앞의 예제에서 설명한 것 처럼 OWIN와 Katana 프로젝트는 새로운 응용 프로그램 프로그래밍 모델 이라고 생각 해서는 안 되며 응용 프로그램 프로그래밍 모델 및 프레임 워크를 서버 및 호스팅 인프라에서 분리 하는 추상화로 간주 되어야 합니다. 예를 들어 웹 API 응용 프로그램을 빌드할 때 개발자 프레임 워크는 Katana 프로젝트의 구성 요소를 사용 하 여 OWIN 파이프라인에서 응용 프로그램을 실행 하는지 여부에 관계 없이 계속 해 서 ASP.NET Web API 프레임 워크를 사용 합니다. OWIN 관련 코드가 응용 프로그램 개발자에 게 표시 되는 한 위치는 개발자가 OWIN 파이프라인을 작성 하는 응용 프로그램 시작 코드입니다. 시작 코드에서 개발자는 일련의 UseXx 문을 등록 합니다. 일반적으로 들어오는 요청을 처리 하는 각 미들웨어 구성 요소에 대해 하나씩입니다. 이 환경은 현재 System.web 환경에 HTTP 모듈을 등록 하는 것과 동일한 효과를 가집니다. 일반적으로 ASP.NET Web API 또는 [SignalR](../../../signalr/index.md) 와 같은 더 큰 프레임 워크 미들웨어는 파이프라인의 끝에 등록 됩니다. 인증 또는 캐싱에 대 한 이러한 구성 요소는 일반적으로 파이프라인의 시작 부분에 등록 되므로 파이프라인에서 나중에 등록 된 모든 프레임 워크 및 구성 요소에 대 한 요청을 처리할 수 있습니다. 이러한 미들웨어 구성 요소와 기본 인프라 구성 요소를 분리 하면 전체 시스템이 안정적으로 유지 되도록 하는 동시에 구성 요소가 서로 다른 속도로 발전할 수 있습니다.

## <a name="components--nuget-packages"></a>구성 요소 – NuGet 패키지

많은 최신 라이브러리 및 프레임 워크와 마찬가지로 Katana 프로젝트 구성 요소는 NuGet 패키지 집합으로 제공 됩니다. 이후 버전 2.0의 경우 Katana 패키지 종속성 그래프는 다음과 같습니다. (더 큰 보기를 보려면 이미지를 클릭 하세요.)

[![](an-overview-of-project-katana/_static/image6.png)](an-overview-of-project-katana/_static/image5.png)

Katana 프로젝트의 거의 모든 패키지는 Owin 패키지에서 직접적으로 또는 간접적으로 종속 됩니다. OWIN 사양의 4 단원에 설명 된 응용 프로그램 시작 시퀀스의 구체적인 구현을 제공 하는 IAppBuilder 인터페이스를 포함 하는 패키지를 기억할 수 있습니다. 또한 대부분의 패키지는 HTTP 요청 및 응답을 사용 하기 위한 도우미 형식 집합을 제공 하는 Owin에 종속 됩니다. 패키지의 나머지 부분은 호스팅 인프라 패키지 (서버 또는 호스트) 또는 미들웨어로 분류할 수 있습니다. Katana 프로젝트 외부에 있는 패키지 및 종속성은 주황색으로 표시 됩니다.

Katana 2.0에 대 한 호스팅 인프라에는 SystemWeb 및 HttpListener 기반 서버, OwinHost .exe를 사용 하 여 OWIN 응용 프로그램을 실행 하기 위한 OwinHost 패키지 및에서 자체 호스팅 OWIN 응용 프로그램을 위한 Owin 패키지가 포함 되어 있습니다. 사용자 지정 호스트 (예: 콘솔 응용 프로그램, Windows 서비스 등)

Katana 2.0의 경우 미들웨어 구성 요소는 주로 다양 한 인증 방법을 제공 하는 데 중점을 두었습니다. 진단을 위한 추가 미들웨어 구성 요소가 하나씩 제공 되며이를 통해 시작 및 오류 페이지를 지원할 수 있습니다. OWIN가 사실상 호스트 하는 추상화로 성장 하 게 되 면 미들웨어 구성 요소 (Microsoft와 타사에서 개발한 구성 요소 모두)의 에코 시스템도 증가 합니다.

## <a name="conclusion"></a>결론

 처음부터 Katana 프로젝트의 목표는 개발자가 아직 다른 웹 프레임 워크를 배워야 합니다. 대신 .NET 웹 응용 프로그램 개발자에 게 이전에 사용할 수 있는 것 보다 더 많은 옵션을 제공 하는 추상화를 만드는 것이 목표입니다. Katana 프로젝트는 일반적인 웹 응용 프로그램 스택의 논리적 계층을 대체 가능한 구성 요소 집합으로 분할 하 여 해당 구성 요소에 적합 한 비율을 개선 하기 위해 스택 전체에서 구성 요소를 사용할 수 있도록 합니다. Katana는 간단한 OWIN 추상화를 중심으로 모든 구성 요소를 빌드하여 프레임 워크와 프레임 워크를 기반으로 구축 된 응용 프로그램을 다양 한 서버 및 호스트에서 이식할 수 있습니다. 개발자가 stack의 제어를 설정 하 여 Katana는 개발자가 기능을 사용 하는 방법에 대 한 최고의 선택 이나 기능을 갖춘 웹 스택이 무엇 인지를 확인 합니다.  

## <a name="for-more-information-about-katana"></a>Katana에 대 한 자세한 내용

- GitHub의 Katana 프로젝트: [https://github.com/aspnet/AspNetKatana/](https://github.com/aspnet/AspNetKatana/).
- 비디오: Howard Dierking에서 [ASP.NET에 대 한 Katana 프로젝트-OWIN](https://channel9.msdn.com/Shows/Web+Camps+TV/The-Katana-Project-OWIN-for-ASPNET).

## <a name="acknowledgements"></a>감사의 말

- [Rick Anderson](https://blogs.msdn.com/b/rickandy/): (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT) ) RICK는 Azure 및 MVC에 초점을 맞춘 Microsoft의 선임 프로그래밍 기록기입니다.
- [Scott Hanselman](http://www.hanselman.com/blog/): (twitter [@shanselman](https://twitter.com/shanselman) )
- [Jon Galloway](https://weblogs.asp.net/jgalloway/default.aspx): (twitter [@jongalloway](https://twitter.com/jongalloway) )
