---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 및 Visual Studio 2010 웹 개발 개요 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 the.NET Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: ecde48f6bd88ee5f569bfeb8b70c26a50bc869c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511433"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 및 Visual Studio 2010 웹 개발 개요

> 이 문서에서는 the.NET Framework 4 및 Visual Studio 2010에 포함 된 ASP.NET에 대 한 여러 가지 새로운 기능에 대 한 개요를 제공 합니다.
> 
> [이 백서 다운로드](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**콘텐츠**

**[핵심 서비스](#0.2__Toc253429238 "_Toc253429238")**  
[Web.config 파일 리팩터링](#0.2__Toc253429239 "_Toc253429239")  
[확장 가능한 출력 캐싱](#0.2__Toc253429240 "_Toc253429240")  
[웹 응용 프로그램 자동 시작](#0.2__Toc253429241 "_Toc253429241")  
[페이지를 영구적으로 리디렉션](#0.2__Toc253429242 "_Toc253429242")  
[세션 상태 축소](#0.2__Toc253429243 "_Toc253429243")  
[허용 되는 Url 범위 확장](#0.2__Toc253429244 "_Toc253429244")  
[확장 가능한 요청 유효성 검사](#0.2__Toc253429245 "_Toc253429245")  
[개체 캐싱 및 개체 캐싱 확장성](#0.2__Toc253429246 "_Toc253429246")  
[확장 가능한 HTML, URL 및 HTTP 헤더 인코딩](#0.2__Toc253429247 "_Toc253429247")  
[단일 작업자 프로세스의 개별 응용 프로그램에 대 한 성능 모니터링](#0.2__Toc253429248 "_Toc253429248")  
[다중 대상 지정](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web Forms 및 MVC에 포함 된 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[지원 Content Delivery Network](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager 명시적 스크립트](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[MetaKeywords 및 MetaDescription 속성을 사용 하 여 Meta 태그를 설정 합니다.](#0.2__Toc253429257 "_Toc253429257")  
[개별 컨트롤에 대 한 뷰 상태 설정](#0.2__Toc253429258 "_Toc253429258")  
[브라우저 기능 변경 내용](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4의 라우팅](#0.2__Toc253429260 "_Toc253429260")  
[클라이언트 Id 설정](#0.2__Toc253429261 "_Toc253429261")  
[데이터 컨트롤에서 행 선택 유지](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET Chart 컨트롤](#0.2__Toc253429263 "_Toc253429263")  
[QueryExtender 컨트롤을 사용 하 여 데이터 필터링](#0.2__Toc253429264 "_Toc253429264")  
[Html로 인코딩된 코드 식](#0.2__Toc253429265 "_Toc253429265")  
[프로젝트 템플릿 변경](#0.2__Toc253429266 "_Toc253429266")  
[CSS 개선 사항](#0.2__Toc253429267 "_Toc253429267")  
[숨겨진 필드 주위의 div 요소 숨기기](#0.2__Toc253429268 "_Toc253429268")  
[템플릿 기반 컨트롤에 대 한 외부 테이블 렌더링](#0.2__Toc253429269 "_Toc253429269")  
[ListView 컨트롤의 향상 된 기능](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 및 RadioButtonList 제어 기능 향상](#0.2__Toc253429271 "_Toc253429271")  
[메뉴 컨트롤 개선](#0.2__Toc253429272 "_Toc253429272")  
[Wizard 및 CreateUserWizard 컨트롤 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[영역 지원](#0.2__Toc253429275 "_Toc253429275")  
[데이터 주석 특성 유효성 검사 지원](#0.2__Toc253429276 "_Toc253429276")  
[템플릿 기반 도우미](#0.2__Toc253429277 "_Toc253429277")

**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**  
[기존 프로젝트에 대 한 Dynamic Data 사용](#0.2__Toc253429279 "_Toc253429279")  
[선언적 DynamicDataManager 컨트롤 구문](#0.2__Toc253429280 "_Toc253429280")  
[엔터티 템플릿](#0.2__Toc253429281 "_Toc253429281")  
[Url 및 전자 메일 주소에 대 한 새 필드 템플릿](#0.2__Toc253429282 "_Toc253429282")  
[DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기](#0.2__Toc253429283 "_Toc253429283")  
[데이터 모델의 상속에 대 한 지원](#0.2__Toc253429284 "_Toc253429284")  
[다 대 다 관계에 대 한 지원 (Entity Framework에만 해당)](#0.2__Toc253429285 "_Toc253429285")  
[표시 및 지원 열거를 제어 하기 위한 새 특성](#0.2__Toc253429286 "_Toc253429286")  
[향상 된 필터 지원](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 웹 개발 개선 사항](#0.2__Toc253429288 "_Toc253429288")**  
[향상 된 CSS 호환성](#0.2__Toc253429289 "_Toc253429289")  
[HTML 및 JavaScript 코드 조각](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense의 향상 된 기능](#0.2__Toc253429291 "_Toc253429291")

**[Visual Studio 2010을 사용 하 여 웹 응용 프로그램 배포](#0.2__Toc253429292 "_Toc253429292")**  
[웹 패키징](#0.2__Toc253429293 "_Toc253429293")  
[Web.config 변환](#0.2__Toc253429294 "_Toc253429294")  
[데이터베이스 배포](#0.2__Toc253429295 "_Toc253429295")  
[한 번 클릭으로 웹 응용 프로그램 게시](#0.2__Toc253429296 "_Toc253429296")  
[리소스](#0.2__Toc253429297 "_Toc253429297")

**[내용을](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>핵심 서비스

ASP.NET 4에서는 출력 캐싱 및 세션 상태 저장소와 같은 핵심 ASP.NET 서비스를 개선 하는 여러 가지 기능을 소개 합니다.

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Web.config 파일 리팩터링

Ajax, 라우팅 및 IIS 7과의 통합과 같은 새로운 기능이 추가 되 면 웹 응용 프로그램에 대 한 구성이 포함 된 `Web.config` 파일이 .NET Framework 크게 증가 했습니다. 그러면 Visual Studio와 같은 도구를 사용 하지 않고 새 웹 응용 프로그램을 구성 하거나 시작 하기가 어려워집니다. .NET Framework 4에서 주요 구성 요소는 `machine.config` 파일로 이동 되었으며 이제 응용 프로그램에서 이러한 설정을 상속 합니다. 이를 통해 ASP.NET 4 응용 프로그램의 `Web.config` 파일이 비어 있거나 응용 프로그램에서 대상으로 하는 프레임 워크의 버전을 지정 하는 다음 줄만 포함할 수 있습니다.

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>확장 가능한 출력 캐싱

ASP.NET 1.0이 출시 된 이후에는 출력 캐싱이 개발자가 생성 된 페이지, 컨트롤 및 HTTP 응답 출력을 메모리에 저장할 수 있었습니다. 이후 웹 요청에서 ASP.NET는 처음부터 출력을 다시 생성 하는 대신 메모리에서 생성 된 출력을 검색 하 여 콘텐츠를 더 신속 하 게 제공할 수 있습니다. 그러나이 방법에는 제한이 있습니다. 생성 된 콘텐츠는 항상 메모리에 저장 되어야 하 고 많은 트래픽이 발생 하는 서버에서는 출력 캐싱에 사용 되는 메모리가 웹 응용 프로그램의 다른 부분에서 메모리 수요와 경쟁할 수 있습니다.

ASP.NET 4는 하나 이상의 사용자 지정 출력 캐시 공급자를 구성할 수 있도록 하는 확장 지점을 출력 캐싱에 추가 합니다. 출력 캐시 공급자는 모든 저장소 메커니즘을 사용 하 여 HTML 콘텐츠를 유지할 수 있습니다. 이렇게 하면 로컬 또는 원격 디스크, 클라우드 저장소 및 분산 캐시 엔진을 포함할 수 있는 다양 한 지 속성 메커니즘에 대 한 사용자 지정 출력 캐시 공급자를 만들 수 있습니다.

사용자 지정 출력 캐시 공급자를 새 *system.object* 에서 파생 되는 클래스로 만들 수 있습니다. 그런 다음, 다음 예제와 같이 *outputCache* 요소의 new *providers* 하위 섹션을 사용 하 여 `Web.config` 파일에서 공급자를 구성할 수 있습니다.

[!code-xml[Main](overview/samples/sample2.xml)]

기본적으로 ASP.NET 4에서 모든 HTTP 응답, 렌더링 된 페이지 및 컨트롤은 이전 예제에 표시 된 것 처럼 메모리 내 출력 캐시를 사용 합니다. 여기서 *defaultProvider* 특성은 AspNetInternalProvider로 설정 됩니다. *DefaultProvider*에 대해 다른 공급자 이름을 지정 하 여 웹 응용 프로그램에 사용 되는 기본 출력 캐시 공급자를 변경할 수 있습니다.

또한 각 제어 및 요청당 다른 출력 캐시 공급자를 선택할 수 있습니다. 다른 웹 사용자 컨트롤에 대해 다른 출력 캐시 공급자를 선택 하는 가장 쉬운 방법은 다음 예제와 같이 컨트롤 지시문에 새 *providerName* 특성을 사용 하 여 선언적으로 수행 하는 것입니다.

[!code-aspx[Main](overview/samples/sample3.aspx)]

HTTP 요청에 다른 출력 캐시 공급자를 지정 하려면 약간 더 많은 작업이 필요 합니다. 공급자를 선언적으로 지정 하는 대신 `Global.asax` 파일에서 새 *Getouputcacheprovidername* 메서드를 재정의 하 여 특정 요청에 사용할 공급자를 프로그래밍 방식으로 지정 합니다. 다음 예제에 이 작업을 수행하는 방법이 나와 있습니다.

[!code-csharp[Main](overview/samples/sample4.cs)]

ASP.NET 4에 출력 캐시 공급자 확장성이 추가 되어 이제 웹 사이트에 더 적극적이 고 지능적인 출력 캐싱 전략을 사용할 수 있습니다. 예를 들어, 디스크에서 낮은 트래픽을 가져오는 페이지를 캐시 하는 동안 사이트의 "상위 10 개" 페이지를 메모리에 캐시할 수 있습니다. 또는 렌더링 된 페이지에 대 한 모든 vary 조합을 캐시할 수 있지만 메모리 소비가 프런트 엔드 웹 서버에서 오프 로드 되도록 분산 캐시를 사용 합니다.

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>웹 응용 프로그램 자동 시작

일부 웹 응용 프로그램은 첫 번째 요청을 처리 하기 전에 많은 양의 데이터를 로드 하거나 비용이 많이 드는 초기화 처리를 수행 해야 합니다. 이전 버전의 ASP.NET에서는 이러한 상황에서 ASP.NET 응용 프로그램을 "절전 모드 해제" 하는 사용자 지정 방법을 고안 한 다음 `Global.asax` 파일에서 *응용 프로그램\_Load* 메서드를 실행 하는 동안 초기화 코드를 실행 해야 했습니다.

이 시나리오를 직접 해결 하는 *자동 시작* 이라는 새로운 확장성 기능은 ASP.NET 4가 Windows Server 2008 r 2에서 IIS 7.5에서 실행 될 때 사용할 수 있습니다. 자동 시작 기능은 응용 프로그램 풀을 시작 하 고, ASP.NET 응용 프로그램을 초기화 하 고, HTTP 요청을 수락 하는 제어 된 방법을 제공 합니다.

> [!NOTE] 
> 
> Iis 7.5에 대 한 IIS 응용 프로그램 준비 모듈
> 
> IIS 팀은 IIS 7.5에 대 한 응용 프로그램 준비 모듈의 첫 번째 베타 테스트 버전을 출시 했습니다. 이렇게 하면 이전에 설명한 것 보다 훨씬 더 쉽게 응용 프로그램을 준비 합니다. 사용자 지정 코드를 작성 하는 대신, 웹 응용 프로그램이 네트워크에서 요청을 수락 하기 전에 실행할 리소스의 Url을 지정 합니다. 이 준비는 iis 서비스를 시작 하는 동안 (IIS 응용 프로그램 풀을 *AlwaysRunning*로 구성한 경우) 및 iis 작업자 프로세스가 재활용 될 때 발생 합니다. 재활용 중에 이전 IIS 작업자 프로세스는 새로 생성 된 작업자 프로세스가 완전히 준비 때까지 요청을 계속 실행 하므로 응용 프로그램에서 unprimed 캐시로 인 한 중단 또는 기타 문제가 발생 하지 않습니다. 이 모듈은 버전 2.0부터 모든 버전의 ASP.NET에서 작동 합니다.
> 
> 자세한 내용은 IIS.net 웹 사이트에서 [응용 프로그램 준비](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net) 를 참조 하세요. 준비 기능을 사용 하는 방법을 보여 주는 연습은 IIS.net 웹 사이트의 [IIS 7.5 응용 프로그램 준비 모듈 시작](https://www.iis.net/learn/manage) 을 참조 하세요.

자동 시작 기능을 사용 하기 위해 IIS 관리자는 `applicationHost.config` 파일에서 다음 구성을 사용 하 여 IIS 7.5의 응용 프로그램 풀을 자동으로 시작 하도록 설정 합니다.

[!code-xml[Main](overview/samples/sample5.xml)]

단일 응용 프로그램 풀에 여러 응용 프로그램이 포함 될 수 있으므로 `applicationHost.config` 파일에서 다음 구성을 사용 하 여 개별 응용 프로그램을 자동으로 시작할 수 있도록 지정 합니다.

[!code-xml[Main](overview/samples/sample6.xml)]

IIS 7.5 서버가 콜드 시작 되거나 개별 응용 프로그램 풀이 재활용 될 때 IIS 7.5은 `applicationHost.config` 파일의 정보를 사용 하 여 자동으로 시작 해야 하는 웹 응용 프로그램을 결정 합니다. 자동 시작으로 표시 된 각 응용 프로그램에 대해 IIS 7.5는 응용 프로그램이 일시적으로 HTTP 요청을 수락 하지 않는 상태에서 응용 프로그램을 시작 하기 위해 ASP.NET 4로 요청을 보냅니다. 이 상태 이면 ASP.NET는 *Serviceautostartprovider* 특성 (이전 예제에 표시 된 것 처럼)에 정의 된 형식을 인스턴스화하고 해당 공용 진입점을 호출 합니다.

다음 예제와 같이 *IProcessHostPreloadClient* 인터페이스를 구현 하 여 필요한 진입점을 사용 하 여 관리 되는 자동 시작 유형을 만듭니다.

[!code-csharp[Main](overview/samples/sample7.cs)]

*미리 로드* 메서드에서 초기화 코드를 실행 하 고 메서드를 반환 하면 ASP.NET 응용 프로그램은 요청을 처리할 준비가 된 것입니다.

IIS .5와 ASP.NET 4를 자동으로 시작 하는 것을 추가 하 여, 이제는 첫 번째 HTTP 요청을 처리 하기 전에 비용이 많이 드는 응용 프로그램 초기화를 수행 하기 위한 잘 정의 된 접근 방식을 사용할 수 있습니다. 예를 들어 새 자동 시작 기능을 사용 하 여 응용 프로그램을 초기화 한 다음 응용 프로그램이 초기화 되었으며 HTTP 트래픽을 받아들일 준비가 되었음을 부하 분산 장치에 알릴 수 있습니다.

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>페이지를 영구적으로 리디렉션

웹 응용 프로그램에서 시간이 지남에 따라 페이지 및 기타 콘텐츠를 이동 하는 것이 일반적입니다 .이 경우 검색 엔진에서 오래 된 링크가 누적 될 수 있습니다. ASP.NET에서 개발자는 일반적으로 Response 메서드를 사용 하 여 새 URL로 요청을 전달 함으로써 이전 Url에 대 한 요청을 처리 했습니다 *.* 그러나 *리디렉션* 메서드는 Http 302 발견 (임시 리디렉션) 응답을 실행 하 여 사용자가 이전 url에 액세스 하려고 할 때 추가 http 왕복을 발생 시킵니다.

ASP.NET 4를 사용 하면 다음 예제와 같이 HTTP 301 이동한 영구적 응답을 쉽게 실행할 수 있도록 하는 새 *Redirectpermanent* 도우미 메서드를 추가 합니다.

[!code-csharp[Main](overview/samples/sample8.cs)]

영구 리디렉션을 인식 하는 검색 엔진 및 기타 사용자 에이전트는 콘텐츠와 연결 된 새 URL을 저장 하 여 임시 리디렉션의 브라우저에서 불필요 한 왕복을 제거 합니다.

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>세션 상태 축소

ASP.NET은 웹 팜 전체에 세션 상태를 저장 하기 위한 두 가지 기본 옵션을 제공 합니다 .이는 out-of-process 세션 상태 서버를 호출 하는 세션 상태 공급자와 Microsoft SQL Server 데이터베이스에 데이터를 저장 하는 세션 상태 공급자입니다. 두 옵션 모두 웹 응용 프로그램의 작업자 프로세스 외부에 상태 정보를 저장 하기 때문에 세션 상태는 원격 저장소로 보내기 전에 serialize 되어야 합니다. 개발자가 세션 상태를 저장 하는 정보의 양에 따라 serialize 된 데이터의 크기가 상당히 커질 수 있습니다.

ASP.NET 4에서는 두 종류의 out-of-process 세션 상태 공급자에 대 한 새로운 압축 옵션을 소개 합니다. 다음 예제에 표시 된 *compressionEnabled* 구성 옵션을 *true*로 설정 하면 ASP.NET는 *GZipStream* 클래스를 사용 .NET Framework 하 여 직렬화 된 세션 상태를 압축 (및 압축 해제) 합니다.

[!code-xml[Main](overview/samples/sample9.xml)]

`Web.config` 파일에 새 특성을 간단히 추가 하면 웹 서버에서 예비 CPU 사이클이 있는 응용 프로그램은 serialize 된 세션 상태 데이터의 크기를 크게 줄일 수 있습니다.

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>허용 되는 Url 범위 확장

ASP.NET 4에서는 응용 프로그램 Url 크기를 확장 하는 새로운 옵션을 소개 합니다. 이전 버전의 ASP.NET 제한 된 URL 경로 길이는 NTFS 파일 경로 제한을 기반으로 260 자로 제한 됩니다. ASP.NET 4에서는 두 개의 새로운 *httpRuntime* 구성 특성을 사용 하 여 응용 프로그램에 맞게이 제한을 늘리거나 줄일 수 있습니다. 다음 예에서는 이러한 새 특성을 보여 줍니다.

[!code-xml[Main](overview/samples/sample10.xml)]

더 길거나 짧은 경로 (프로토콜, 서버 이름 및 쿼리 문자열을 포함 하지 않는 URL 부분)를 허용 하려면 *[Maxurllength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 특성을 수정 합니다. 더 길거나 짧은 쿼리 문자열을 허용 하려면 *[Maxquerystringlength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 특성의 값을 수정 합니다.

ASP.NET 4를 사용 하 여 URL 문자 검사에 사용 되는 문자를 구성할 수도 있습니다. ASP.NET에서 URL의 경로 부분에 잘못 된 문자를 찾으면 요청을 거부 하 고 HTTP 400 오류를 발생 시킵니다. 이전 버전의 ASP.NET에서 URL 문자 검사는 고정 문자 집합으로 제한 되었습니다. ASP.NET 4에서 다음 예제와 같이 *httpRuntime* 구성 요소의 새 *requestpathinvalidcharacters* 특성을 사용 하 여 유효한 문자 집합을 사용자 지정할 수 있습니다.

[!code-xml[Main](overview/samples/sample11.xml)]

기본적으로 *Requestpathinvalidcharacters* 특성은 8 문자를 유효 하지 않은 것으로 정의 합니다. (기본적으로 *Requestpathinvalidcharacters* 에 할당 된 문자열에서 `Web.config` 파일이 XML 파일 이므로 보다 작음 (&lt;), 보다 큼 (&gt;) 및 앰퍼샌드 (&amp;) 문자가 인코딩됩니다. 필요에 따라 잘못 된 문자 집합을 사용자 지정할 수 있습니다.

> [!NOTE]
> 참고 ASP.NET 4는 IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt))의 RFC 2396에 정의 된 잘못 된 URL 문자 이기 때문에 ASCII 범위 0X00에서 0x1F 문자를 포함 하는 url 경로를 항상 거부 합니다. IIS 6 이상을 실행 하는 Windows Server 버전에서 http.sys 프로토콜 장치 드라이버는 이러한 문자를 포함 하는 Url을 자동으로 거부 합니다.

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>확장 가능한 요청 유효성 검사

ASP.NET 요청 유효성 검사는 들어오는 HTTP 요청 데이터에서 XSS (교차 사이트 스크립팅) 공격에 일반적으로 사용 되는 문자열을 검색 합니다. 잠재적 XSS 문자열이 발견 되 면 요청 유효성 검사에서 주의 대상 문자열에 플래그를 제공 하 고 오류를 반환 합니다. 기본 제공 요청 유효성 검사에서는 XSS 공격에 사용 되는 가장 일반적인 문자열을 찾은 경우에만 오류를 반환 합니다. 이전에 XSS 유효성 검사를 더 적극적으로 수행 하려고 하면 가양성이 너무 많이 발생 했습니다. 그러나 고객은 더 적극적인 요청 유효성 검사를 원할 수도 있고, 특정 페이지 또는 특정 유형의 요청에 대해 의도적으로 XSS 검사를 완화 하려고 할 수도 있습니다.

ASP.NET 4에서는 사용자 지정 요청-유효성 검사 논리를 사용할 수 있도록 요청 유효성 검사 기능이 확장 가능 합니다. 요청 유효성 검사를 확장 *하려면 새 httpRuntime* 형식에서 파생 되는 클래스를 만들고 사용자 지정 형식을 사용 하도록 응용 프로그램 (`Web.config` 파일의 섹션에 있는)을 구성 합니다. 다음 예제에서는 사용자 지정 요청-유효성 검사 클래스를 구성 하는 방법을 보여 줍니다.

[!code-xml[Main](overview/samples/sample12.xml)]

새 *requestValidationType* 특성에는 사용자 지정 요청 유효성 검사를 제공 하는 클래스를 지정 하는 표준 .NET Framework 형식 식별자 문자열이 필요 합니다. 각 요청에 대해 ASP.NET는 들어오는 HTTP 요청 데이터의 각 부분을 처리 하기 위해 사용자 지정 형식을 호출 합니다. 들어오는 URL, 모든 HTTP 헤더 (쿠키와 사용자 지정 헤더 모두) 및 엔터티 본문은 모두 다음 예제에 표시 된 것과 같이 사용자 지정 요청 유효성 검사 클래스에서 검사할 수 있습니다.

[!code-csharp[Main](overview/samples/sample13.cs)]

들어오는 HTTP 데이터를 검사 하지 않으려는 경우에는 base를 호출 하 여 ASP.NET 기본 요청 유효성 검사를 실행할 수 있도록 요청 유효성 검사 클래스가 대체 될 수 있습니다 *. Is유효한 Requeststring입니다.*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>개체 캐싱 및 개체 캐싱 확장성

첫 번째 릴리스 이후 ASP.NET은 강력한 메모리 내 개체 캐시 (*system.web*)를 포함 했습니다. 캐시 구현은 웹이 아닌 응용 프로그램에서 사용 되는 것으로 널리 사용 되 고 있습니다. 그러나 Windows Forms 또는 WPF 응용 프로그램에서 ASP.NET 개체 캐시를 사용할 수 있도록 `System.Web.dll`에 대 한 참조를 포함 하는 것은 좋지 않습니다.

모든 응용 프로그램에서 캐싱을 사용할 수 있도록 하기 위해 .NET Framework 4에서는 새 어셈블리, 새 네임 스페이스, 몇 가지 기본 형식 및 구체적인 캐싱 구현을 소개 합니다. 새 `System.Runtime.Caching.dll` 어셈블리에는 *system.object* 네임 스페이스의 새로운 캐싱 API가 포함 되어 있습니다. 네임 스페이스에는 클래스의 두 가지 핵심 집합이 포함 되어 있습니다.

- 모든 형식의 사용자 지정 캐시 구현을 빌드하기 위한 토대를 제공 하는 추상 형식입니다.
- 구체적인 메모리 내 개체 캐시 구현 ( *system.web. memorycache* 클래스)입니다.

새 *memorycache* 클래스는 ASP.NET cache와 긴밀 하 게 모델링 되며 ASP.NET를 사용 하 여 내부 캐시 엔진 논리의 대부분을 공유 합니다. ASP.NET *Cache* 개체를 사용 하는 경우에는 Cache 개체를 사용 하 여 사용자 지정 캐시의 공용 캐싱 *api가 업데이트* 되었지만 새 api에서 친숙 한 개념을 찾을 수 있습니다.

새 *Memorycache* 클래스와 지원 기본 api에 대 한 자세한 내용은 전체 문서가 필요 합니다. 그러나 다음 예제에서는 새 캐시 API의 작동 방식을 설명 합니다. 이 예제는 `System.Web.dll`에 대 한 종속성 없이 Windows Forms 응용 프로그램용으로 작성 되었습니다.

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>확장 가능한 HTML, URL 및 HTTP 헤더 인코딩

ASP.NET 4에서 다음과 같은 일반적인 텍스트 인코딩 작업에 대 한 사용자 지정 인코딩 루틴을 만들 수 있습니다.

- HTML 인코딩입니다.
- URL 인코딩입니다.
- HTML 특성 인코딩입니다.
- 아웃 바운드 HTTP 헤더를 인코딩합니다.

다음 예제와 *같이 새 ASP.NET* 형식에서 파생 시킨 다음, `Web.config` 파일의 *httpRuntime* 섹션에서 사용자 지정 형식을 사용 하도록 구성 하 여 사용자 지정 인코더를 만들 수 있습니다.

[!code-xml[Main](overview/samples/sample15.xml)]

사용자 지정 인코더가 구성 된 후에는 ASP.NET 또는 *HttpServerUtility* 클래스의 공용 인코딩 메서드가 호출 될 때마다 사용자 지정 인코딩 구현을 자동으로 호출 *합니다.* 이렇게 하면 웹 개발 팀의 한 부분에서 적극적인 문자 인코딩을 구현 하는 사용자 지정 인코더를 만들 수 있으며, 나머지 웹 개발 팀은 계속 해 서 공용 ASP.NET encoding Api를 사용 합니다. *HttpRuntime* 요소에서 사용자 지정 인코더를 중앙에서 구성 하 여 공용 ASP.NET encoding api의 모든 텍스트 인코딩 호출이 사용자 지정 인코더를 통해 라우팅되도록 보장 됩니다.

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>단일 작업자 프로세스의 개별 응용 프로그램에 대 한 성능 모니터링

단일 서버에서 호스팅될 수 있는 웹 사이트 수를 늘리기 위해 많은 호스팅 서비스 공급자는 단일 작업자 프로세스에서 여러 ASP.NET 응용 프로그램을 실행 합니다. 그러나 여러 응용 프로그램에서 단일 공유 작업자 프로세스를 사용 하는 경우 서버 관리자가 문제가 발생 한 개별 응용 프로그램을 식별 하기 어렵습니다.

ASP.NET 4는 CLR에서 도입 된 새로운 리소스 모니터링 기능을 활용 합니다. 이 기능을 사용 하도록 설정 하려면 다음 XML 구성 코드 조각을 `aspnet.config` 구성 파일에 추가 하면 됩니다.

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> `aspnet.config` 파일은 .NET Framework가 설치 된 디렉터리에 있습니다. `Web.config` 파일이 아닙니다.

*AppDomainResourceMonitoring* 기능을 사용 하는 경우 "ASP.NET 응용 프로그램" 성능 범주 *% 관리 되는 프로세서 시간* 및 *사용 된 관리*되는 메모리에서 두 개의 새로운 성능 카운터를 사용할 수 있습니다. 이러한 성능 카운터는 모두 새로운 CLR 응용 프로그램 도메인 리소스 관리 기능을 사용 하 여 개별 ASP.NET 응용 프로그램의 예상 CPU 시간 및 관리 되는 메모리 사용률을 추적 합니다. 결과적으로, 관리자는 ASP.NET 4를 사용 하 여 단일 작업자 프로세스에서 실행 되는 개별 응용 프로그램의 리소스 소비에 대 한 보다 세분화 된 보기를 갖게 됩니다.

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>멀티 타기팅

.NET Framework의 특정 버전을 대상으로 하는 응용 프로그램을 만들 수 있습니다. ASP.NET 4에서는 `Web.config` 파일의 *컴파일* 요소에 있는 새 특성을 사용 하 여 .NET Framework 4 이상을 대상으로 지정할 수 있습니다. .NET Framework 4를 명시적으로 대상으로 지정 하 고 `Web.config` 파일에 *system.object*와 같은 선택적 요소를 포함 하는 경우 이러한 요소는 .NET Framework 4에 대해 정확 해야 합니다. .NET Framework 4를 명시적으로 대상으로 하지 않는 경우 대상 프레임 워크는 `Web.config` 파일에 항목이 부족 한 것으로 유추 됩니다.

다음 예제에서는 `Web.config` 파일의 *컴파일* 요소에 *targetframework* 특성을 사용 하는 방법을 보여 줍니다.

[!code-xml[Main](overview/samples/sample17.xml)]

특정 버전의 .NET Framework를 대상으로 지정 하는 방법에 대 한 자세한 내용은 다음을 참조 하세요.

- .NET Framework 4 응용 프로그램 풀에서, `Web.config` 파일이 *Targetframework* 특성을 포함 하지 않거나 `Web.config` 파일이 없는 경우 ASP.NET 빌드 시스템은 .NET Framework 4를 대상으로 간주 합니다. .NET Framework 4에서 실행 되도록 응용 프로그램에 대 한 코딩 변경 작업을 수행 해야 할 수도 있습니다.
- *Targetframework* 특성을 포함 하 고, `Web.config` 파일에 *system.object* 요소가 정의 되어 있는 경우이 파일은 .NET Framework 4에 대 한 올바른 항목을 포함 해야 합니다.
- 빌드 환경에서와 같이 *aspnet\_컴파일러* 명령을 사용 하 여 응용 프로그램을 미리 컴파일하는 경우 대상 프레임 워크에 대 한 올바른 버전의 *aspnet\_컴파일러* 명령을 사용 해야 합니다. .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727)과 함께 제공 된 컴파일러를 사용 하 여 .NET Framework 3.5 이전 버전을 컴파일합니다. .NET Framework 4와 함께 제공 되는 컴파일러를 사용 하 여 해당 프레임 워크를 사용 하거나 이후 버전을 사용 하 여 만든 응용 프로그램을 컴파일합니다.
- 런타임에 컴파일러는 컴퓨터에 설치 된 최신 프레임 워크 어셈블리 (및 따라서 GAC)를 사용 합니다. 가상 버전 4.1가 설치 된 경우와 같이 나중에 프레임 워크에 업데이트를 수행 하는 경우 *targetframework* 특성이 더 낮은 버전 (예: 4.0)을 대상으로 하더라도 최신 버전의 프레임 워크에서 기능을 사용할 수 있습니다. 그러나 Visual Studio 2010의 디자인 타임에 또는 *aspnet\_컴파일러* 명령을 사용 하는 경우 프레임 워크의 최신 기능을 사용 하면 컴파일러 오류가 발생 합니다.

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web Forms 및 MVC에 포함 된 jQuery

Web Forms 및 MVC에 대 한 Visual Studio 템플릿은 오픈 소스 jQuery 라이브러리를 포함 합니다. 새 웹 사이트 또는 프로젝트를 만들 때 다음 세 개의 파일이 포함 된 Scripts 폴더가 만들어집니다.

- Jquery-1.10.2.min.js 1.4.1 – 사용자가 읽을 수 있는 jQuery 라이브러리의 버전입니다.
- Jquery-1.10.2.min.js 14.1 – jQuery 라이브러리의 최소 버전입니다.
- Jquery-1.10.2.min.js 1.4.1-vsdoc – jQuery 라이브러리에 대 한 Intellisense 설명서 파일입니다.

응용 프로그램을 개발 하는 동안 jQuery 버전의 jQuery를 포함 합니다. 프로덕션 응용 프로그램에 대 한 jQuery 버전을 포함 합니다.

예를 들어 다음 Web Forms 페이지에서는 jQuery를 사용 하 여 포커스가 있을 때 ASP.NET TextBox 컨트롤의 배경색을 노란색으로 변경 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>지원 Content Delivery Network

Microsoft Ajax Content Delivery Network (CDN)를 사용 하면 웹 응용 프로그램에 ASP.NET Ajax 및 jQuery 스크립트를 쉽게 추가할 수 있습니다. 예를 들어 페이지에 다음과 같이 Ajax.microsoft.com를 가리키는 `<script>` 태그를 추가 하 여 jQuery 라이브러리를 사용 하 여 시작할 수 있습니다.

[!code-html[Main](overview/samples/sample19.html)]

Microsoft Ajax CDN을 사용하여 Ajax 응용 프로그램의 성능을 크게 향상시킬 수 있습니다. Microsoft Ajax CDN의 콘텐츠는 전 세계에 있는 서버에 캐시 됩니다. 또한 Microsoft Ajax CDN을 통해 브라우저에서 다른 도메인에 있는 웹 사이트에 대한 캐시된 JavaScript 파일을 다시 사용할 수 있습니다.

Microsoft Ajax Content Delivery Network는 SSL(Secure Sockets Layer)를 사용 하 여 웹 페이지를 제공 해야 하는 경우 SSL (HTTPS)을 지원 합니다.

CDN을 사용할 수 없는 경우 대체 (fallback)를 구현 합니다. 대체 (fallback)를 테스트 합니다.

Microsoft Ajax CDN에 대 한 자세한 내용을 보려면 다음 웹 사이트를 방문 하세요.

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager는 Microsoft Ajax CDN을 지원 합니다. 단일 속성인 EnableCdn 속성을 설정 하기만 하면 CDN에서 모든 ASP.NET framework JavaScript 파일을 검색할 수 있습니다.

[!code-aspx[Main](overview/samples/sample20.aspx)]

EnableCdn 속성을 true 값으로 설정 하면 ASP.NET framework는 유효성 검사 및 UpdatePanel에 사용 되는 모든 JavaScript 파일을 포함 하 여 CDN에서 모든 ASP.NET framework JavaScript 파일을 검색 합니다. 이 속성을 설정 하면 웹 응용 프로그램의 성능에 크게 영향을 줄 수 있습니다.

Webresource.axd 특성을 사용 하 여 고유한 JavaScript 파일에 대 한 CDN 경로를 설정할 수 있습니다. 새 CdnPath 속성은 EnableCdn 속성을 true 값으로 설정할 때 사용 되는 CDN의 경로를 지정 합니다.

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 명시적 스크립트

이전에는 ASP.NET ScriptManger를 사용한 경우 전체 모놀리식 ASP.NET Ajax 라이브러리를 로드 해야 했습니다. 새 AjaxFrameworkMode 속성을 활용 하 여 ASP.NET Ajax 라이브러리의 구성 요소를 로드 하 고 필요한 ASP.NET Ajax 라이브러리의 구성 요소만 로드 하는 것을 정확 하 게 제어할 수 있습니다.

AjaxFrameworkMode 속성은 다음 값으로 설정할 수 있습니다.

- Enabled-ScriptManager 컨트롤이 Microsoftajax.js 스크립트 파일을 자동으로 포함 하도록 지정 합니다 .이 파일은 모든 핵심 프레임 워크 스크립트 (레거시 동작)의 결합 된 스크립트 파일입니다.
- Disabled--모든 Microsoft Ajax 스크립트 기능을 사용 하지 않도록 지정 하 고 ScriptManager 컨트롤이 스크립트를 자동으로 참조 하지 않도록 지정 합니다.
- Explicit--페이지에 필요한 개별 프레임 워크 핵심 스크립트 파일에 스크립트 참조를 명시적으로 포함 하 고 각 스크립트 파일에 필요한 종속성에 대 한 참조를 포함할 것을 지정 합니다.

예를 들어 AjaxFrameworkMode 속성을 Explicit 값으로 설정 하는 경우 필요한 특정 ASP.NET Ajax 구성 요소 스크립트를 지정할 수 있습니다.

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>웹 양식

Web Forms ASP.NET 1.0 이후 ASP.NET의 핵심 기능입니다. ASP.NET 4의 경우 다음을 포함 하 여 다양 한 기능이 향상 되었습니다.

- *Meta* 태그를 설정 하는 기능입니다.
- 뷰 상태에 대 한 제어 향상.
- 브라우저 기능을 사용 하는 보다 쉬운 방법입니다.
- Web Forms에서 ASP.NET routing 사용에 대 한 지원.
- 생성 된 Id에 대 한 추가 제어.
- 데이터 컨트롤에서 선택 된 행을 유지 하는 기능입니다.
- *FormView* 및 *ListView* 컨트롤에서 렌더링 된 HTML에 대 한 제어 향상
- 데이터 소스 컨트롤에 대 한 필터링 지원.

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>MetaKeywords 및 MetaDescription 속성을 사용 하 여 Meta 태그를 설정 합니다.

ASP.NET 4는 *페이지* 클래스 *MetaKeywords* 및 *MetaDescription*에 두 개의 속성을 추가 합니다. 이러한 두 속성은 다음 예제와 같이 페이지의 해당 *meta* 태그를 나타냅니다.

[!code-aspx[Main](overview/samples/sample23.aspx)]

이러한 두 속성은 페이지의 *Title* 속성과 동일한 방식으로 작동 합니다. 이러한 규칙은 다음과 같습니다.

1. *Head* 요소에 속성 이름 ( *MetaKeywords* 의 경우 name = "keywords")과 일치 하는 *Meta* 태그가 없는 경우, *MetaDescription*에 대해 이러한 속성이 설정 되지 않은 것을 의미 합니다. 즉, 해당 속성이 설정 되지 않은 경우에는 *메타* 태그가 렌더링 될 때 해당 페이지에 추가 됩니다.
2. 이러한 이름을 가진 *meta* 태그가 이미 있는 경우 이러한 속성은 기존 태그 내용에 대 한 get 및 set 메서드로 작동 합니다.

런타임에 이러한 속성을 설정 하 여 데이터베이스 또는 다른 소스에서 콘텐츠를 가져올 수 있으며, 특정 페이지의 용도를 설명 하도록 태그를 동적으로 설정할 수 있습니다.

다음 예제와 같이 Web Forms 페이지 태그 위쪽의 *@ page* 지시문에서 *키워드* 및 *설명* 속성을 설정할 수도 있습니다.

[!code-aspx[Main](overview/samples/sample24.aspx)]

이렇게 하면 해당 페이지에 이미 선언 된 *meta* 태그 내용 (있는 경우)이 재정의 됩니다.

설명 *메타* 태그의 내용은 Google에서 검색 목록 미리 보기를 개선 하는 데 사용 됩니다. 자세한 내용은 Google 웹 마스터 중부 블로그에서 [메타 설명을 사용 하 여 코드 조각 개선 개조](https://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html) 을 참조 하세요. Google 및 Windows 실시간 검색은 키워드의 내용을 어떤 것도 사용 하지 않지만 다른 검색 엔진은 사용할 수 있습니다. 자세한 내용은 검색 엔진 가이드 웹 사이트에서 [Meta 키워드 도움말](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php) 을 참조 하세요.

이러한 새 속성은 간단한 기능 이지만 이러한 속성을 수동으로 추가 하거나 사용자 고유의 코드를 작성 하 여 *메타* 태그를 만드는 요구 사항에서 사용자를 저장 합니다.

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>개별 컨트롤에 대 한 뷰 상태 설정

기본적으로 페이지에 대 한 뷰 상태는 응용 프로그램에 필요 하지 않은 경우에도 페이지의 각 컨트롤이 뷰 상태를 저장할 수 있습니다. 뷰 상태 데이터는 페이지가 생성 하는 태그에 포함 되며 페이지를 클라이언트에 전송 하 고 다시 게시 하는 데 걸리는 시간을 늘립니다. 필요한 것 보다 더 많은 뷰 상태를 저장 하면 성능이 크게 저하 될 수 있습니다. 이전 버전의 ASP.NET에서는 개발자가 페이지 크기를 줄이기 위해 개별 컨트롤에 대 한 뷰 상태를 사용 하지 않도록 설정할 수 있지만 개별 컨트롤에 대해 명시적으로이 작업을 수행 해야 했습니다. ASP.NET 4에서 웹 서버 컨트롤에는 기본적으로 뷰 상태를 사용 하지 않도록 설정한 다음 페이지에 필요한 컨트롤에 대해서만 사용 하도록 설정 하는 *Viewstatemode* 속성이 포함 되어 있습니다.

*Viewstatemode* 속성은 3 개의 값이 *사용*, *사용 안 함*및 *상속*인 열거형을 사용 합니다. *사용* 을 설정 하면 해당 컨트롤 및 *상속* 하도록 설정 되었거나 아무것도 설정 하지 않은 모든 자식 컨트롤의 뷰 상태를 사용 하도록 설정 합니다. *Disabled* 뷰 상태를 사용 하지 않도록 설정 하 고 *상속* 은 컨트롤이 부모 컨트롤의 *viewstatemode* 설정을 사용 하도록 지정 합니다.

다음 예에서는 *Viewstatemode* 속성이 작동 하는 방법을 보여 줍니다. 다음 페이지의 컨트롤에 대 한 태그와 코드에는 *Viewstatemode* 속성의 값이 포함 되어 있습니다.

[!code-aspx[Main](overview/samples/sample25.aspx)]

여기에서 볼 수 있듯이 코드는 PlaceHolder1 컨트롤에 대 한 뷰 상태를 사용 하지 않도록 설정 합니다. 자식 label1 컨트롤은이 속성 값을 상속 합니다. 즉, 컨트롤에 대 한 *Viewstatemode* 의 기본값을*상속* 하므로 뷰 상태를 저장 하지 않습니다. PlaceHolder2 컨트롤에서 *Viewstatemode* 는 *Enabled*로 설정 되므로 label2는이 속성을 상속 하 고 뷰 상태를 저장 합니다. 페이지가 처음 로드 될 때 두 *레이블* 컨트롤의 *Text* 속성은 문자열 "[DynamicValue]"로 설정 됩니다.

이러한 설정의 효과는 페이지가 처음 로드 될 때 브라우저에 다음 출력이 표시 된다는 것입니다.

사용 안 함 `: [DynamicValue]`

사용:`[DynamicValue]`

그러나 포스트백 후에는 다음과 같은 출력이 표시 됩니다.

사용 안 함 `: [DeclaredValue]`

사용:`[DynamicValue]`

Label1 컨트롤 ( *Viewstatemode* 값이 *Disabled*로 설정 됨)이 코드에서 설정 된 값을 유지 하지 않았습니다. 그러나 *Viewstatemode* 값이 *사용*으로 설정 된 label2 컨트롤은 상태를 유지 합니다.

다음 예제와 같이 *@ Page* 지시문에 *viewstatemode* 를 설정할 수도 있습니다.

[!code-aspx[Main](overview/samples/sample26.aspx)]

*페이지* 클래스는 다른 컨트롤 일 뿐입니다. 페이지의 다른 모든 컨트롤에 대 한 부모 컨트롤 역할을 합니다. *Page*인스턴스에 대해 *viewstatemode* 의 기본값을 *사용할 수* 있습니다. 컨트롤은를 기본적으로 *상속*하기 때문에 페이지 또는 컨트롤 수준에서 *viewstatemode* 를 설정 하지 않는 한, 컨트롤은 *Enabled* 속성 값을 상속 합니다.

*Viewstatemode* 속성의 값은 *enableviewstate* 속성이 *true*로 설정 된 경우에만 뷰 상태가 유지 되는지 여부를 결정 합니다. *Enableviewstate* 속성이 *false*로 설정 되어 있으면 *viewstatemode* 가 *Enabled*로 설정 된 경우에도 뷰 상태가 유지 되지 않습니다.

이 기능을 사용 하는 경우 마스터 페이지의 *ContentPlaceHolder* 컨트롤을 사용 하는 것이 좋습니다 .이 경우 마스터 페이지에 대해 *Viewstatemode* 를 *Disabled* 로 설정한 다음 뷰 상태가 필요한 컨트롤이 포함 된 *ContentPlaceHolder* 컨트롤에 대해 개별적으로 사용 하도록 설정할 수 있습니다.

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>브라우저 기능 변경 내용

ASP.NET는 *브라우저 기능*이라는 기능을 사용 하 여 사용자가 사이트를 검색 하는 데 사용 하는 브라우저의 기능을 결정 합니다. 브라우저 기능은 *Httpbrowsercapabilities* 개체로 표시 됩니다 ( *요청. browser* 속성에 의해 노출 됨). 예를 들어 *Httpbrowsercapabilities* 개체를 사용 하 여 현재 브라우저의 형식 및 버전이 특정 버전의 JavaScript를 지원 하는지 확인할 수 있습니다. 또는 *Httpbrowsercapabilities* 개체를 사용 하 여 요청이 모바일 장치에서 시작 되었는지 여부를 확인할 수 있습니다.

*Httpbrowsercapabilities* 개체는 브라우저 정의 파일 집합에 따라 결정 됩니다. 이러한 파일에는 특정 브라우저의 기능에 대 한 정보가 포함 되어 있습니다. ASP.NET 4에서는 이러한 브라우저 정의 파일이 최근에 도입 된 브라우저와 장치에 대 한 정보를 포함 하도록 업데이트 되었습니다. Google Chrome, 모션 BlackBerry 스마트폰의 연구 및 Apple iPhone.

다음 목록에서는 새 브라우저 정의 파일을 보여 줍니다.

- *blackberry. 브라우저*
- *chrome. 브라우저*
- *기본값. 브라우저*
- *firefox. 브라우저*
- *게이트웨이. 브라우저*
- *일반 브라우저*
- *ie.browser*
- *iemobile*
- *iphone. 브라우저*
- *opera*
- *safari. 브라우저*

#### <a name="using-browser-capabilities-providers"></a>브라우저 기능 공급자 사용

ASP.NET 버전 3.5 서비스 팩 1에서는 다음과 같은 방법으로 브라우저에 포함 되는 기능을 정의할 수 있습니다.

- 컴퓨터 수준에서 다음 폴더에 `.browser` XML 파일을 만들거나 업데이트 합니다.

- [!code-console[Main](overview/samples/sample27.cmd)]

- 브라우저 기능을 정의한 후에는 브라우저 기능 어셈블리를 다시 빌드하고 GAC에 추가 하기 위해 Visual Studio 명령 프롬프트에서 다음 명령을 실행 합니다.

- [!code-console[Main](overview/samples/sample28.cmd)]

- 개별 응용 프로그램의 경우 응용 프로그램의 `App_Browsers` 폴더에 `.browser` 파일을 만듭니다.

이러한 접근 방식에서는 XML 파일을 변경 해야 하며 컴퓨터 수준 변경의 경우에는 aspnet\_regbrowsers 프로세스를 실행 한 후 응용 프로그램을 다시 시작 해야 합니다.

ASP.NET 4에는 *브라우저 기능 공급자*라고 하는 기능이 포함 되어 있습니다. 이름에서 알 수 있듯이이를 통해 공급자를 빌드할 수 있습니다. 그러면 고유한 코드를 사용 하 여 브라우저 기능을 확인할 수 있습니다.

실제로 개발자는 사용자 지정 브라우저 기능을 정의 하지 않는 경우가 많습니다. 브라우저 파일은 업데이트 하기 어렵습니다. 이러한 파일을 업데이트 하는 프로세스는 매우 복잡 하며, `.browser` 파일의 XML 구문은를 사용 하 고 정의 하는 데 복잡할 수 있습니다. 일반적인 브라우저 정의 구문이 나 최신 브라우저 정의를 포함 하는 데이터베이스 또는 이러한 데이터베이스에 대 한 웹 서비스를 사용 하는 경우이 프로세스를 훨씬 쉽게 수행할 수 있습니다. 새 브라우저 기능 공급자 기능을 사용 하면 타사 개발자가 이러한 시나리오를 가능 하 게 할 수 있습니다.

새로운 ASP.NET 4 브라우저 기능 공급자 기능을 사용 하는 방법에는 ASP.NET 브라우저 기능 정의 기능을 확장 하거나 완전히 대체 하는 두 가지 방법이 있습니다. 다음 섹션에서는 기능을 대체 하는 방법 및 확장 하는 방법에 대해 설명 합니다.

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser 기능 대체 기능

ASP.NET browser 기능 정의 기능을 완전히 교체 하려면 다음 단계를 수행 합니다.

1. 다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesProvider* 에서 파생 되는 공급자 클래스를 만듭니다. 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    이 예제의 코드는 browser 라는 기능을 지정 하 고 해당 기능을 MyCustomBrowser로 설정 하 여 새 *Httpbrowsercapabilities* 개체를 만듭니다.
2. 응용 프로그램에 공급자를 등록 합니다. 

    응용 프로그램에서 공급자를 사용 하려면 `Web.config` 또는 `Machine.config` 파일의 *browserCaps* 섹션에 *공급자* 특성을 추가 해야 합니다. 특정 모바일 장치에 대 한 폴더와 같이 응용 프로그램의 특정 디렉터리에 대 한 *location* 요소에서 공급자 특성을 정의할 수도 있습니다. 다음 예에서는 구성 파일에서 *공급자* 특성을 설정 하는 방법을 보여 줍니다.

    [!code-xml[Main](overview/samples/sample30.xml)]

    새 브라우저 기능 정의를 등록 하는 또 다른 방법은 다음 예제와 같이 코드를 사용 하는 것입니다.

    [!code-csharp[Main](overview/samples/sample31.cs)]

    이 코드는 `Global.asax` 파일의 *응용 프로그램\_시작* 이벤트에서 실행 해야 합니다. *BrowserCapabilitiesProvider* 클래스에 대 한 변경 내용은 응용 프로그램의 코드가 실행 되기 전에 발생 해야 캐시가 해결 된 *사용* 개체에 대 한 유효한 상태로 유지 됩니다.

#### <a name="caching-the-httpbrowsercapabilities-object"></a>HttpBrowserCapabilities 개체 캐시

앞의 예제에는 *Httpbrowsercapabilities* 개체를 가져오기 위해 사용자 지정 공급자가 호출 될 때마다 코드가 실행 되는 한 가지 문제가 있습니다. 각 요청 중에 여러 번 발생할 수 있습니다. 이 예제에서는 공급자의 코드에서 많은 작업을 수행 하지 않습니다. 그러나 사용자 지정 공급자의 코드가 *Httpbrowsercapabilities* 개체를 가져오기 위해 중요 한 작업을 수행 하는 경우이는 성능에 영향을 줄 수 있습니다. 이러한 상황이 발생 하지 않도록 하려면 *Httpbrowsercapabilities* 개체를 캐시 하면 됩니다. 다음 단계를 수행하세요.

1. 다음 예제와 같이 *HttpCapabilitiesProvider*에서 파생 되는 클래스를 만듭니다. 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    이 예제에서 코드는 사용자 지정 BuildCacheKey 메서드를 호출 하 여 캐시 키를 생성 하 고, 사용자 지정 GetCacheTime 메서드를 호출 하 여 캐시 하는 시간 길이를 가져옵니다. 그런 다음 코드는 확인 된 *Httpbrowsercapabilities* 개체를 캐시에 추가 합니다. 캐시에서 개체를 검색 하 고 사용자 지정 공급자를 사용 하는 후속 요청에서 재사용할 수 있습니다.
2. 이전 절차에 설명 된 대로 응용 프로그램에 공급자를 등록 합니다.

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>ASP.NET Browser 기능 확장 기능

이전 섹션에서는 ASP.NET 4에서 새 *Httpbrowsercapabilities* 개체를 만드는 방법을 설명 했습니다. ASP.NET에 이미 있는 브라우저에 새 브라우저 기능 정의를 추가 하 여 ASP.NET 브라우저 기능 기능을 확장할 수도 있습니다. XML 브라우저 정의를 사용 하지 않고이 작업을 수행할 수 있습니다. 다음 절차에서는 방법을 보여 줍니다.

1. 다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesEvaluator* 에서 파생 되는 클래스를 만듭니다. 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    이 코드는 먼저 ASP.NET browser 기능 기능을 사용 하 여 브라우저를 식별 합니다. 그러나 요청에 정의 된 정보를 기반으로 브라우저가 식별 되지 않는 경우 즉, *Httpbrowsercapabilities* 개체의 *browser* 속성이 문자열 "Unknown" 이면 코드에서 사용자 지정 공급자 (MyBrowserCapabilitiesEvaluator)를 호출 하 여 브라우저를 식별 합니다.
2. 이전 예제에서 설명한 대로 응용 프로그램에 공급자를 등록 합니다.

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>기존 기능 정의에 새 기능을 추가 하 여 브라우저 기능 기능 확장

사용자 지정 브라우저 정의 공급자를 만들고 동적으로 새 브라우저 정의를 만드는 것 외에도 추가 기능을 사용 하 여 기존 브라우저 정의를 확장할 수 있습니다. 이렇게 하면 원하는 항목에 가까운 정의를 사용할 수 있지만 몇 가지 기능만 부족 합니다. 이렇게 하려면 다음 단계를 따릅니다.

1. 다음 예제와 같이 *Getbrowsercapabilities* 메서드를 재정의 하는 *HttpCapabilitiesEvaluator* 에서 파생 되는 클래스를 만듭니다. 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    예제 코드는 기존 ASP.NET *HttpCapabilitiesEvaluator* 클래스를 확장 하 고 다음 코드를 사용 하 여 현재 요청 정의와 일치 하는 *httpbrowsercapabilities* 개체를 가져옵니다.

    [!code-csharp[Main](overview/samples/sample35.cs)]

    그러면 코드에서이 브라우저의 기능을 추가 하거나 수정할 수 있습니다. 새 브라우저 기능을 지정 하는 방법에는 두 가지가 있습니다.

    - *사용* 개체의 *Capabilities* 속성에 의해 노출 되는 *IDictionary* 개체에 키/값 쌍을 추가 합니다. 이전 예제에서 코드는 값이 *true*인 다중 터치 기능을 추가 합니다.
    - *사용* 개체의 기존 속성을 설정 합니다. 이전 예제에서 코드는 *frame* 속성을 *true*로 설정 합니다. 이 속성은 *기능* 속성에 의해 노출 되는 *IDictionary* 개체에 대 한 접근자 일 뿐입니다. 

        > [!NOTE]
        > 참고이 모델은 제어 어댑터를 포함 하 여 *Httpbrowsercapabilities*의 모든 속성에 적용 됩니다.
2. 이전 절차에 설명 된 대로 응용 프로그램에 공급자를 등록 합니다.

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4의 라우팅

ASP.NET 4는 Web Forms로 라우팅을 사용 하기 위한 기본 제공 지원을 추가 합니다. 라우팅을 사용 하면 실제 파일에 매핑되지 않는 요청 Url을 허용 하도록 응용 프로그램을 구성할 수 있습니다. 대신 라우팅을 사용 하 여 사용자에 게 의미 있는 Url을 정의 하 고 응용 프로그램에 대 한 SEO (검색 엔진 최적화)를 지원할 수 있습니다. 예를 들어 기존 응용 프로그램의 제품 범주를 표시 하는 페이지의 URL은 다음 예제와 같이 표시 될 수 있습니다.

[!code-console[Main](overview/samples/sample36.cmd)]

라우팅을 사용 하 여 다음 URL을 허용 하도록 응용 프로그램을 구성 하 여 동일한 정보를 렌더링할 수 있습니다.

[!code-console[Main](overview/samples/sample37.cmd)]

ASP.NET 3.5 SP1부터 라우팅을 사용할 수 있습니다. ASP.NET 3.5 s p 1에서 라우팅을 사용 하는 방법에 대 한 예제는 Phil Haack의 블로그에서 [WebForms를 사용 하 여 라우팅을](http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "이 항목의 제목입니다.") 사용 하는 항목을 참조 하세요. 그러나 ASP.NET 4에는 다음을 포함 하 여 라우팅을 보다 쉽게 사용할 수 있도록 하는 몇 가지 기능이 포함 되어 있습니다.

- *PageRouteHandler* 클래스는 경로를 정의할 때 사용 하는 간단한 HTTP 처리기입니다. 클래스는 요청을 라우팅하는 페이지로 데이터를 전달 합니다.
- 새 속성 *HttpRequest* 및 *RouteData* ( *HttpRequest* 개체에 대 한 프록시)입니다. 이러한 속성을 통해 경로에서 전달 되는 정보에 쉽게 액세스할 수 있습니다.
- *RouteUrlExpressionBuilder* 및 RouteValueExpressionBuilder에 정의 된 다음과 같은 새 식 작성기가 있습니다.:
- *RouteUrl*는 ASP.NET 서버 컨트롤 내의 경로 url에 해당 하는 url을 만드는 간단한 방법을 제공 합니다.
- *RouteValue*는 *RouteContext* 개체에서 정보를 추출 하는 간단한 방법을 제공 합니다.
- *RouteParameter* 클래스를 사용 하면 *RouteContext* 개체에 포함 된 데이터를 데이터 소스 컨트롤에 대 한 쿼리에 더 쉽게 전달할 수 있습니다 ( [*formparameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)와 유사).

#### <a name="routing-for-web-forms-pages"></a>Web Forms 페이지에 대 한 라우팅

다음 예제에서는 *route* 클래스의 new *MapPageRoute* 메서드를 사용 하 여 Web Forms 경로를 정의 하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4에서는 *MapPageRoute* 메서드를 소개 합니다. 다음 예제는 이전 예제에 표시 된 SearchRoute 정의와 동일 하지만 *PageRouteHandler* 클래스를 사용 합니다.

[!code-csharp[Main](overview/samples/sample39.cs)]

예제의 코드는 경로를 첫 번째 경로의 실제 페이지에 매핑합니다 (`~/search.aspx`). 또한 첫 번째 경로 정의는 searchterm 이라는 매개 변수를 URL에서 추출 하 여 페이지에 전달 하도록 지정 합니다.

*MapPageRoute* 메서드는 다음 메서드 오버 로드를 지원 합니다.

- *MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess, RouteValueDictionary 기본값)*
- *MapPageRoute (string routeName, string routeUrl, string Valfile, bool checkPhysicalUrlAccess, RouteValueDictionary defaults, RouteValueDictionary 제약 조건)*

*Check이상 Urlaccess* 매개 변수는 경로가 라우팅되는 실제 페이지의 보안 권한 (이 경우에는 .aspx) 및 들어오는 URL에 대 한 권한 (이 경우 검색/{searchterm})을 확인 해야 하는지 여부를 지정 합니다. *Checking Urlaccess* 값이 *FALSE*이면 들어오는 URL의 사용 권한만 확인 됩니다. 이러한 권한은 다음과 같은 설정을 사용 하 여 `Web.config` 파일에 정의 됩니다.

[!code-xml[Main](overview/samples/sample40.xml)]

예제 구성에서는 관리자 역할에 속한 사용자를 제외한 모든 사용자에 대 한 실제 페이지 `search.aspx`에 대 한 액세스가 거부 됩니다. *Check/search/{searchterm} Urlaccess* 매개 변수를 *true* (기본값)로 설정 하면 실제 페이지 검색은 해당 역할의 사용자로 제한 되기 때문에 admin 사용자만 URL에 액세스할 수 있습니다. *Check/search/{searchterm}. Urlaccess* 가 *false* 로 설정 되 고 사이트가 이전 예제와 같이 구성 된 경우 인증 된 모든 사용자는 URL에 액세스할 수 있습니다.

#### <a name="reading-routing-information-in-a-web-forms-page"></a>Web Forms 페이지에서 라우팅 정보 읽기

Web Forms 실제 페이지의 코드에서 *HttpRequest* 및 *RouteData*라는 두 개의 새 속성을 사용 하 여 라우팅에서 추출 된 정보 (또는 다른 개체가 *RouteData* 개체에 추가한 기타 정보)에 액세스할 수 있습니다. (*RouteData* *HttpRequest RouteData*를 래핑합니다.) 다음 예제에서는 *RouteData*를 사용 하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample41.cs)]

이 코드는 앞의 예제 경로에 정의 된 대로 searchterm 매개 변수로 전달 된 값을 추출 합니다. 다음 요청 URL을 고려 합니다.

[!code-console[Main](overview/samples/sample42.cmd)]

이 요청을 수행 하면 "scott" 이라는 단어가 `search.aspx` 페이지에서 렌더링 됩니다.

#### <a name="accessing-routing-information-in-markup"></a>태그에서 라우팅 정보 액세스

이전 섹션에서 설명 하는 메서드는 Web Forms 페이지에서 코드의 경로 데이터를 가져오는 방법을 보여 줍니다. 동일한 정보에 대 한 액세스를 제공 하는 태그에 식을 사용할 수도 있습니다. 식 작성기는 선언적 코드를 사용 하는 강력 하 고 세련 된 방법입니다. 자세한 내용은 Phil Haack의 블로그에서 [사용자 지정 식 작성기를 사용 하 여 명시적으로](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx) 입력 항목을 참조 하세요.

ASP.NET 4에는 Web Forms 라우팅을 위한 두 가지 새로운 식 작성기가 포함 되어 있습니다. 다음 예제에서는이를 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample43.aspx)]

이 예에서 *RouteUrl* 식은 경로 매개 변수를 기반으로 하는 URL을 정의 하는 데 사용 됩니다. 이렇게 하면 전체 URL을 태그에 하드 코딩 하지 않아도 되며, 나중에이 링크를 변경할 필요 없이 URL 구조를 변경할 수 있습니다.

이 태그는 앞에서 정의한 경로에 따라 다음 URL을 생성 합니다.

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET는 입력 매개 변수를 기반으로 올바른 경로 (즉, 올바른 URL 생성)를 자동으로 수행 합니다. 사용할 경로를 지정할 수 있는 경로 이름을 식에 포함할 수도 있습니다.

다음 예에서는 *RouteValue* 식을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample45.aspx)]

이 컨트롤을 포함 하는 페이지가 실행 되 면 레이블에 "scott" 값이 표시 됩니다.

*RouteValue* 식을 사용 하면 태그에서 경로 데이터를 간단 하 게 사용할 수 있으며, 태그에서 보다 복잡 한 RouteData ["x"] 구문을 사용할 필요가 없습니다.

#### <a name="using-route-data-for-data-source-control-parameters"></a>데이터 원본 제어 매개 변수에 대 한 경로 데이터 사용

*RouteParameter* 클래스를 사용 하면 경로 데이터를 데이터 소스 컨트롤의 쿼리에 대 한 매개 변수 값으로 지정할 수 있습니다. 다음 예제와 같이 클래스와 [매우 유사](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx) 하 게 작동 합니다.

[!code-aspx[Main](overview/samples/sample46.aspx)]

이 경우 경로 매개 변수 searchterm의 값이 *Select* 문의 @companyname 매개 변수에 사용 됩니다.

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>클라이언트 Id 설정

새 *Clientidmode* 속성은 ASP.NET에서 오래 된 문제를 해결 합니다. 즉, 컨트롤에서 렌더링 하는 요소에 대 한 *id* 특성을 만듭니다. 응용 프로그램에 이러한 요소를 참조 하는 클라이언트 스크립트가 포함 된 경우 렌더링 된 요소에 대 한 *id* 특성을 알고 있는 것이 중요 합니다.

웹 서버 컨트롤에 대해 렌더링 되는 HTML의 *id* 특성은 컨트롤의 *ClientID* 속성을 기반으로 생성 됩니다. ASP.NET 4 까지는 *ClientID* 속성에서 *id* 특성을 생성 하는 알고리즘이 id를 사용 하 여 명명 컨테이너 (있는 경우)를 연결 하 고 반복 되는 컨트롤 (데이터 컨트롤의 경우)에서 접두사와 일련 번호를 추가 합니다. 이는 페이지의 컨트롤 Id가 항상 고유 하다는 것을 보장 하지만 알고리즘은 예측할 수 없는 컨트롤 Id를 가지 므로 클라이언트 스크립트에서 참조 하기가 어렵습니다.

새 *Clientidmode* 속성을 사용 하면 컨트롤에 대 한 클라이언트 ID가 생성 되는 방식을 보다 정확 하 게 지정할 수 있습니다. 페이지를 포함 하 여 모든 컨트롤에 대해 *Clientidmode* 속성을 설정할 수 있습니다. 가능한 설정은 다음과 같습니다.

- *Autoid* – ASP.NET의 이전 버전에서 사용 된 *ClientID* 속성 값을 생성 하는 알고리즘과 동일 합니다.
- *정적* –이는 *ClientID* 값이 부모 명명 컨테이너의 id를 연결 하지 않고 id와 동일 하 게 지정 하도록 지정 합니다. 이는 웹 사용자 정의 컨트롤에 유용할 수 있습니다. 웹 사용자 정의 컨트롤은 다른 페이지와 다른 컨테이너 컨트롤에 있을 수 있으므로 ID 값을 예측할 수 없으므로 *Autoid* 알고리즘을 사용 하는 컨트롤에 대 한 클라이언트 스크립트를 작성 하기 어려울 수 있습니다.
- *예측* 가능-이 옵션은 주로 반복 템플릿을 사용 하는 데이터 컨트롤에서 사용 됩니다. 컨트롤의 명명 컨테이너에 대 한 ID 속성을 연결 하지만 생성 된 *ClientID* 값은 "ctlxxx"와 같은 문자열을 포함 하지 않습니다. 이 설정은 컨트롤의 *Clientidrowsuffix* 속성과 함께 작동 합니다. *Clientidrowsuffix* 속성을 데이터 필드의 이름으로 설정 하 고 해당 필드의 값이 생성 된 *ClientID* 값의 접미사로 사용 됩니다. 일반적으로 데이터 레코드의 기본 키를 *Clientidrowsuffix* 값으로 사용 합니다.
- *Inherit* –이 설정은 컨트롤의 기본 동작입니다. 컨트롤의 ID 생성이 부모와 동일 하도록 지정 합니다.

페이지 수준에서 *Clientidmode* 속성을 설정할 수 있습니다. 이는 현재 페이지의 모든 컨트롤에 대 한 기본 *Clientidmode* 값을 정의 합니다.

페이지 수준에서 기본 *clientidmode* 값은 *autoid*이 고, 컨트롤 수준의 기본 *Clientidmode* 값은 *상속*됩니다. 따라서 코드의 아무 곳에서 나이 속성을 설정 하지 않으면 모든 컨트롤이 *자동 id* 알고리즘으로 기본 설정 됩니다.

다음 예제와 같이 *@ page* 지시문에서 페이지 수준 값을 설정 합니다.

[!code-aspx[Main](overview/samples/sample47.aspx)]

컴퓨터 (컴퓨터) 수준이 나 응용 프로그램 수준에서 구성 파일에 *Clientidmode* 값을 설정할 수도 있습니다. 응용 프로그램의 모든 페이지에 있는 모든 컨트롤에 대 한 기본 *Clientidmode* 설정을 정의 합니다. 컴퓨터 수준에서 값을 설정 하는 경우 해당 컴퓨터의 모든 웹 사이트에 대해 기본 *Clientidmode* 설정을 정의 합니다. 다음 예에서는 구성 파일에 있는 *Cli\mode* 설정을 보여 줍니다.

[!code-xml[Main](overview/samples/sample48.xml)]

앞에서 설명한 것 처럼 *ClientID* 속성의 값은 컨트롤의 부모에 대 한 명명 컨테이너에서 파생 됩니다. 마스터 페이지를 사용 하는 경우와 같은 일부 시나리오에서 컨트롤은 다음과 같이 렌더링 된 HTML과 같은 Id로 끝날 수 있습니다.

[!code-html[Main](overview/samples/sample49.html)]

*텍스트 상자* 컨트롤의 태그에 표시 된 *input* 요소는 페이지 (중첩 된 *ContentPlaceholder* 컨트롤)에 있는 두 개의 명명 컨테이너에만 포함 되어 있지만 마스터 페이지가 처리 되는 방식 때문에 최종 결과는 다음과 같은 컨트롤 ID입니다.

[!code-console[Main](overview/samples/sample50.cmd)]

이 ID는 페이지에서 고유 하지만 대부분의 용도로는 불필요 한 시간입니다. 렌더링 된 ID의 길이를 줄이고 ID 생성 방법을 보다 세밀 하 게 제어 하려는 경우를 가정해 보겠습니다. 예를 들어 "ctlxxx" 접두사를 제거 하려고 합니다. 이 작업을 수행 하는 가장 쉬운 방법은 다음 예제에 표시 된 대로 *Clientidmode* 속성을 설정 하는 것입니다.

[!code-aspx[Main](overview/samples/sample51.aspx)]

이 샘플에서 *Clientidmode* 속성은 가장 바깥쪽 *namingpanel* 요소에 대해 *Static* 으로 설정 되 고 내부 *Namingpanel* 요소에 대해 *예측 가능한* 로 설정 됩니다. 이러한 설정은 다음 태그를 생성 합니다. 페이지의 나머지 부분과 마스터 페이지는 이전 예제와 동일한 것으로 간주 됩니다.

[!code-html[Main](overview/samples/sample52.html)]

*정적* 설정은 가장 바깥쪽 *namingpanel* 요소 내의 모든 컨트롤에 대 한 명명 계층을 다시 설정 하 고 생성 된 ID에서 *ContentPlaceHolder* 및 *MasterPage* id를 제거 하는 효과가 있습니다. 렌더링 된 요소의 *name* 특성에는 영향을 주지 않으므로 일반적인 ASP.NET 기능은 이벤트, 뷰 상태 등에 대해 유지 됩니다. 명명 계층을 다시 설정 하는 부작용은 *Namingpanel* 요소의 태그를 다른 *ContentPlaceholder* 컨트롤로 이동 하더라도 렌더링 된 클라이언트 id는 동일 하 게 유지 된다는 것입니다.

> [!NOTE]
> 렌더링 된 컨트롤 Id가 고유한 지 확인 하는 것이 좋습니다. 그렇지 않으면 클라이언트 *document.getelementbyid* 함수와 같은 개별 HTML 요소에 대해 고유 id가 필요한 모든 기능을 중단할 수 있습니다.

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>데이터 바인딩된 컨트롤에서 예측 가능한 클라이언트 Id 만들기

레거시 알고리즘을 통해 데이터 바인딩된 목록 컨트롤의 컨트롤에 대해 생성 되는 *ClientID* 값은 길고 예측 가능 하지 않습니다. 이러한 Id가 생성 되는 방식을 보다 *효과적으로 제어 하는 데* 도움이 될 수 있습니다.

다음 예제의 태그는 *ListView* 컨트롤을 포함 합니다.

[!code-aspx[Main](overview/samples/sample53.aspx)]

이전 예제에서 *Clientidmode* 및 *Rowclientidrowsuffix* 속성은 태그에 설정 되어 있습니다. *Clientidrowsuffix* 속성은 데이터 바인딩된 컨트롤에만 사용할 수 있으며 해당 동작은 사용 하는 컨트롤에 따라 다릅니다. 차이점은 다음과 같습니다.

- *GridView* 컨트롤-런타임에 결합 되어 클라이언트 id를 만드는 데이터 소스에 있는 하나 이상의 열 이름을 지정할 수 있습니다. 예를 들어 *Rowclientidrowsuffix* 를 "ProductName, ProductId"로 설정 하면 렌더링 된 요소의 컨트롤 id 형식은 다음과 같습니다.

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView* 컨트롤-클라이언트 ID에 추가 되는 데이터 원본의 단일 열을 지정할 수 있습니다. 예를 들어, *Clientidrowsuffix* 를 "ProductName"로 설정 하면 렌더링 된 컨트롤 id의 형식은 다음과 같습니다.

- [!code-console[Main](overview/samples/sample55.cmd)]

- 이 경우 후행 1은 현재 데이터 항목의 제품 ID에서 파생 됩니다.

- *Repeater* 컨트롤-이 컨트롤은 *Clientidrowsuffix* 속성을 지원 하지 않습니다. *Repeater* 컨트롤에서 현재 행의 인덱스를 사용 합니다. *Repeater* 컨트롤에서 ClientIDMode = "예측 가능"을 사용 하는 경우 다음과 같은 형식의 클라이언트 id가 생성 됩니다.

- [!code-console[Main](overview/samples/sample56.cmd)]

- 후행 0은 현재 행의 인덱스입니다.

*FormView* 및 *DetailsView* 컨트롤은 여러 행을 표시 하지 않으므로 *clientidrowsuffix* 속성을 지원 하지 않습니다.

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>데이터 컨트롤에서 행 선택 유지

*GridView* 및 *ListView* 컨트롤을 사용 하면 사용자가 행을 선택할 수 있습니다. 이전 버전의 ASP.NET에서 선택은 페이지의 행 인덱스를 기반으로 합니다. 예를 들어 1 페이지에서 세 번째 항목을 선택한 다음 2 페이지로 이동 하면 해당 페이지의 세 번째 항목이 선택 됩니다.

지속형 선택은 처음에는 .NET Framework 3.5 s p 1의 Dynamic Data 프로젝트 에서만 지원 되었습니다. 이 기능을 사용 하도록 설정 하면 현재 선택한 항목이 항목의 데이터 키를 기반으로 합니다. 즉, 1 페이지에서 세 번째 행을 선택 하 고 2 페이지로 이동 하면 2 페이지에서 아무 것도 선택 되지 않습니다. 1 페이지를 다시 이동 하면 세 번째 행도 선택 됩니다. 이제 다음 예제와 같이 *Enablepersistedselection* 속성을 사용 하 여 모든 프로젝트에서 *GridView* 및 *ListView* 컨트롤에 대해 지속형 선택이 지원 됩니다.

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET Chart 컨트롤

ASP.NET *차트* 컨트롤은 .NET Framework에서 데이터 시각화 제공 기능을 확장 합니다. *차트* 컨트롤을 사용 하 여 복잡 한 통계 또는 재무 분석을 위해 직관적이 고 시각적으로 멋진 차트가 있는 ASP.NET 페이지를 만들 수 있습니다. ASP.NET *Chart* 컨트롤은 .NET Framework 버전 3.5 SP1 릴리스에 추가 된 기능으로 도입 되었으며 .NET Framework 4 릴리스의 일부입니다.

컨트롤에는 다음과 같은 기능이 포함 되어 있습니다.

- 35가지 개별 차트 종류
- 차트 영역, 제목, 범례 및 주석의 수에 제한이 없습니다.
- 모든 차트 요소에 대 한 다양 한 모양 설정
- 대부분의 차트 종류에 대 한 3 차원 지원
- 데이터 요소 주위에 자동으로 맞출 수 있는 스마트 데이터 레이블
- 줄무늬 선, 배율 구분선 및 로그 눈금 크기 조정.
- 데이터 분석 및 변환을 위한 50개가 넘는 재무 및 통계 수식
- 차트 데이터의 단순 바인딩 및 조작
- 날짜, 시간 및 통화와 같은 공통 데이터 형식에 대 한 지원
- Ajax를 사용 하 여 클라이언트 클릭 이벤트를 비롯 한 대화형 작업 및 이벤트 구동 사용자 지정 지원.
- 상태 관리.
- 이진 스트리밍

다음 그림에서는 ASP.NET 차트 컨트롤에 의해 생성 되는 재무 차트의 예를 보여 줍니다.

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

그림 2: ASP.NET Chart 컨트롤 예제

ASP.NET 차트 컨트롤을 사용 하는 방법에 대 한 추가 예제를 보려면 MSDN 웹 사이트의 [Microsoft Chart Controls 용 샘플 환경](https://go.microsoft.com/fwlink/?LinkId=128300) 페이지에서 샘플 코드를 다운로드 하십시오. 커뮤니티 콘텐츠의 샘플은 [차트 컨트롤 포럼](https://go.microsoft.com/fwlink/?LinkId=128713)에서 찾을 수 있습니다.

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>ASP.NET 페이지에 차트 컨트롤 추가

다음 예제에서는 태그를 사용 하 여 ASP.NET 페이지에 *차트* 컨트롤을 추가 하는 방법을 보여 줍니다. 이 예제에서 *차트* 컨트롤은 정적 데이터 요소에 대 한 세로 막대형 차트를 생성 합니다.

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>3 차원 차트 사용

*차트* 컨트롤에는 차트 영역의 특징을 정의 하는 지 수 개체를 포함할 수 있는 *Chartareas* *컬렉션이 포함 되어* 있습니다. 예를 들어 차트 영역에 3 차원을 사용 하려면 다음 예제와 같이 *있는 area3dstyle* 속성을 사용 합니다.

[!code-aspx[Main](overview/samples/sample59.aspx)]

아래 그림에서는 *가로 막대형* 차트 종류의 4 가지 계열을 포함 하는 3 차원 차트를 보여 줍니다.

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

그림 3:3-D 가로 막대형 차트

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>배율 구분선 및 로그 눈금 간격 사용

배율 구분선 및 로그 눈금 크기는 차트에 복잡성을 추가 하는 두 가지 추가 방법입니다. 이러한 기능은 차트 영역의 각 축에 적용 됩니다. 예를 들어 차트 영역의 기본 Y 축에서 이러한 기능을 사용 하려면 *AxisY* 및 *ScaleBreakStyle* *속성을 영역 개체에* 사용 합니다. 다음 코드 조각에서는 기본 Y 축에서 배율 구분선을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample60.aspx)]

아래 그림은 배율 구분선이 설정 된 Y 축을 보여 줍니다.

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

그림 4: 배율 구분선

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>QueryExtender 컨트롤을 사용 하 여 데이터 필터링

데이터 기반 웹 페이지를 만드는 개발자를 위한 매우 일반적인 작업은 데이터를 필터링 하는 것입니다. 일반적으로 데이터 소스 컨트롤의 *Where* 절을 빌드하여 수행 했습니다. 이 방법은 복잡할 수 있으며, 경우에 따라 *Where* 구문을 사용 하 여 기본 데이터베이스의 전체 기능을 활용할 수 없습니다.

더 쉽게 필터링 하기 위해 ASP.NET 4에서 새 *Queryextender* 컨트롤이 추가 되었습니다. 이러한 컨트롤에서 반환 된 데이터를 필터링 하기 위해이 컨트롤을 *EntityDataSource* 또는 *LinqDataSource* 컨트롤에 추가할 수 있습니다. *Queryextender* 컨트롤이 LINQ를 사용 하기 때문에 데이터가 페이지에 전송 되기 전에 데이터베이스 서버에 필터가 적용 되므로 작업이 매우 효율적입니다.

*Queryextender* 컨트롤은 다양 한 필터 옵션을 지원 합니다. 다음 섹션에서는 이러한 옵션에 대해 설명 하 고이를 사용 하는 방법에 대 한 예제를 제공 합니다.

#### <a name="search"></a>검색

검색 옵션의 경우 *Queryextender* 컨트롤은 지정 된 필드에서 검색을 수행 합니다. 다음 예제에서 컨트롤은 TextBoxSearch 컨트롤에 입력 된 텍스트를 사용 하 여 `ProductName`에서 해당 콘텐츠를 검색 하 고 *LinqDataSource* 컨트롤에서 반환 된 데이터의 `Supplier.CompanyName` 열을 검색 합니다.

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>범위

범위 옵션은 검색 옵션과 비슷하지만 범위를 정의 하는 값 쌍을 지정 합니다. 다음 예제에서 *Queryextender* 컨트롤은 *LinqDataSource* 컨트롤에서 반환 된 데이터의 `UnitPrice` 열을 검색 합니다. 페이지의 TextBoxFrom 및 TextBoxTo 컨트롤에서 범위를 읽습니다.

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

속성 식 옵션을 사용 하 여 속성 값에 대 한 비교를 정의할 수 있습니다. 식이 *true*로 평가 되 면 검사 중인 데이터가 반환 됩니다. 다음 예제에서 *Queryextender* 컨트롤은 `Discontinued` 열의 데이터를 페이지의 CheckBoxDiscontinued 컨트롤 값과 비교 하 여 데이터를 필터링 합니다.

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

마지막으로 *Queryextender* 컨트롤에 사용할 사용자 지정 식을 지정할 수 있습니다. 이 옵션을 사용 하면 사용자 지정 필터 논리를 정의 하는 페이지에서 함수를 호출할 수 있습니다. 다음 예제에서는 *Queryextender* 컨트롤에서 사용자 지정 식을 선언적으로 지정 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample64.aspx)]

다음 예제에서는 *Queryextender* 컨트롤에 의해 호출 되는 사용자 지정 함수를 보여 줍니다. 이 경우 *Where* 절을 포함 하는 데이터베이스 쿼리를 사용 하는 대신 코드는 LINQ 쿼리를 사용 하 여 데이터를 필터링 합니다.

[!code-csharp[Main](overview/samples/sample65.cs)]

이 예에서는 한 번에 하나의 식만 *Queryextender* 컨트롤에 사용 됩니다. 그러나 *Queryextender* 컨트롤 안에 여러 개의 식을 포함할 수 있습니다.

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html로 인코딩된 코드 식

일부 ASP.NET 사이트 (특히 ASP.NET MVC)는 `<%`= `expression %>` 구문 (종종 "code 너 깃" 이라고 함)을 사용 하 여 응답에 텍스트를 씁니다. 코드 식을 사용 하는 경우 텍스트를 HTML로 인코딩하는 것은 쉽지 않습니다. 텍스트를 사용자 입력에서 가져온 경우에는 페이지를 XSS (교차 사이트 스크립팅) 공격에 노출 시킬 수 있습니다.

ASP.NET 4에는 다음과 같은 코드 식에 대 한 새로운 구문이 도입 되었습니다.

[!code-aspx[Main](overview/samples/sample66.aspx)]

이 구문은 응답에 쓸 때 기본적으로 HTML 인코딩을 사용 합니다. 이 새 식은 다음과 같이 효과적으로 변환 됩니다.

[!code-aspx[Main](overview/samples/sample67.aspx)]

예를 들어 &lt;%: Request ["UserInput"]%&gt;는 *request ["userinput"]* 의 값에서 HTML 인코딩을 수행 합니다.

이 기능의 목표는 사용할 모든 단계를 강제로 결정 하지 않도록 이전 구문의 모든 인스턴스를 새 구문으로 바꿀 수 있도록 하는 것입니다. 그러나 출력 되는 텍스트가 HTML 이거나 이미 인코딩된 경우가 있습니다 .이 경우에는 이중 인코딩이 발생할 수 있습니다.

이러한 경우, ASP.NET 4에서는 구체적인 구현인 *Htmlstring*과 함께 *IHtmlString*새 인터페이스를 소개 합니다. 이러한 형식의 인스턴스를 사용 하면 반환 값이 HTML로 표시 하기 위해 이미 올바르게 인코딩 되었는지 아니면 검사 되었는지 확인할 수 있으며, 따라서이 값은 다시 HTML로 인코딩되지 않아야 합니다. 예를 들어, 다음은 HTML로 인코딩되지 않고 인코딩되지 않아야 합니다.

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 도우미 메서드는 이중 인코딩되지 않고 ASP.NET 4를 실행 하는 경우에만이 새 구문에서 사용할 수 있도록 업데이트 되었습니다. ASP.NET 3.5 s p 1을 사용 하 여 응용 프로그램을 실행 하는 경우이 새로운 구문이 작동 하지 않습니다.

이것은 XSS 공격 으로부터 보호를 보장 하지 않는다는 점에 유의 하십시오. 예를 들어 따옴표에 포함 되지 않은 특성 값을 사용 하는 HTML에는 여전히 취약 한 사용자 입력이 포함 될 수 있습니다. ASP.NET 컨트롤 및 ASP.NET MVC 도우미의 출력에는 항상 따옴표 안에 특성 값이 포함 되며이는 권장 되는 방법입니다.

마찬가지로이 구문은 사용자 입력을 기반으로 JavaScript 문자열을 만드는 경우와 같이 JavaScript 인코딩을 수행 하지 않습니다.

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>프로젝트 템플릿 변경

이전 버전의 ASP.NET에서 Visual Studio를 사용 하 여 새 웹 사이트 프로젝트 또는 웹 응용 프로그램 프로젝트를 만드는 경우 결과 프로젝트에는 다음 그림과 같이 default.aspx 페이지, 기본 `Web.config` 파일 및 `App_Data` 폴더만 포함 됩니다.

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio는 다음 그림에 표시 된 것 처럼 파일을 전혀 포함 하지 않는 빈 웹 사이트 프로젝트 형식을 지원 합니다.

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

그 결과, 초보자의 경우 프로덕션 웹 응용 프로그램을 빌드하는 방법에 대 한 지침이 거의 없습니다. 따라서 ASP.NET 4에는 빈 웹 응용 프로그램 프로젝트용과 웹 응용 프로그램 및 웹 사이트 프로젝트에 각각 하나씩 세 개의 새 템플릿이 도입 되었습니다.

#### <a name="empty-web-application-template"></a>빈 웹 응용 프로그램 템플릿

이름에서 알 수 있듯이, 빈 웹 응용 프로그램 템플릿은 제거 된 웹 응용 프로그램 프로젝트입니다. 다음 그림에 표시 된 것 처럼 Visual Studio 새 프로젝트 대화 상자에서이 프로젝트 템플릿을 선택 합니다.

[![](overview/_static/image7.png)](overview/_static/image6.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image8.png))

빈 ASP.NET 웹 응용 프로그램을 만들면 Visual Studio에서 다음과 같은 폴더 레이아웃을 만듭니다.

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

이는 한 가지 예외를 제외 하 고 이전 버전의 ASP.NET에서 가져온 빈 웹 사이트 레이아웃과 비슷합니다. Visual Studio 2010에서 빈 웹 응용 프로그램 및 빈 웹 사이트 프로젝트에는 Visual Studio에서 프로젝트를 대상으로 하는 프레임 워크를 식별 하는 데 사용 하는 정보가 포함 된 다음과 같은 최소 `Web.config` 파일이 포함 되어 있습니다.

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

이 *Targetframework* 속성이 없는 경우 Visual Studio는 이전 응용 프로그램을 열 때 호환성을 유지 하기 위해 기본적으로 .NET Framework 2.0를 대상으로 지정 합니다.

#### <a name="web-application-and-web-site-project-templates"></a>웹 응용 프로그램 및 웹 사이트 프로젝트 템플릿

Visual Studio 2010와 함께 제공 되는 다른 두 개의 새 프로젝트 템플릿에는 주요 변경 내용이 포함 되어 있습니다. 다음 그림은 새 웹 응용 프로그램 프로젝트를 만들 때 생성 되는 프로젝트 레이아웃을 보여 줍니다. 웹 사이트 프로젝트의 레이아웃은 거의 동일 합니다.

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

프로젝트에는 이전 버전에서 만들지 않은 많은 파일이 포함 되어 있습니다. 또한 새 웹 응용 프로그램 프로젝트는 새로운 응용 프로그램에 대 한 액세스 보안을 신속 하 게 시작할 수 있도록 하는 기본 멤버 자격 기능으로 구성 됩니다. 이러한 포함으로 인해 새 프로젝트의 `Web.config` 파일에는 멤버 자격, 역할 및 프로필을 구성 하는 데 사용 되는 항목이 포함 됩니다. 다음 예제에서는 새 웹 응용 프로그램 프로젝트에 대 한 `Web.config` 파일을 보여 줍니다. (이 경우 *roleManager* 은 사용 하지 않도록 설정 됩니다.)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image14.png))

또한이 프로젝트는 `Account` 디렉터리에 두 번째 `Web.config` 파일을 포함 합니다. 두 번째 구성 파일은 로그인 하지 않은 사용자를 위해 ChangePassword 페이지에 대 한 액세스를 보호 하는 방법을 제공 합니다. 다음 예에서는 두 번째 `Web.config` 파일의 내용을 보여 줍니다.

![](overview/_static/image15.png)

새 프로젝트 템플릿에는 기본적으로 만들어진 페이지에도 이전 버전 보다 더 많은 콘텐츠가 포함 되어 있습니다. 프로젝트에는 기본 마스터 페이지와 CSS 파일이 포함 되어 있으며 기본 페이지 (default.aspx)는 기본적으로 마스터 페이지를 사용 하도록 구성 되어 있습니다. 따라서 웹 응용 프로그램 또는 웹 사이트를 처음 실행 하는 경우 기본 (홈) 페이지가 이미 작동 하 고 있는 것입니다. 실제로 새 MVC 응용 프로그램을 시작할 때 표시 되는 기본 페이지와 비슷합니다.

[![](overview/_static/image17.png)](overview/_static/image16.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image18.png))

이러한 프로젝트 템플릿에 대 한 이러한 변경의 목적은 새 웹 응용 프로그램 빌드를 시작 하는 방법에 대 한 지침을 제공 하는 것입니다. 의미 체계가 올바르고 엄격한 XHTML 1.0 호환 태그와 CSS를 사용 하 여 지정 된 레이아웃을 사용 하 여 템플릿의 페이지는 ASP.NET 4 웹 응용 프로그램을 빌드하기 위한 모범 사례를 나타냅니다. 기본 페이지에는 쉽게 사용자 지정할 수 있는 2 열 레이아웃도 있습니다.

예를 들어, 새 웹 응용 프로그램의 경우 일부 색을 변경 하 고 My ASP.NET 응용 프로그램 로고 대신 회사 로고를 삽입 한다고 가정 합니다. 이렇게 하려면 로고 이미지를 저장 하는 `Content` 아래에 새 디렉터리를 만듭니다.

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

페이지에 이미지를 추가 하려면 다음 예제와 같이 `Site.Master` 파일을 열고 내 ASP.NET 응용 프로그램 텍스트가 정의 된 위치를 찾은 다음 *src* 특성이 새 로고 이미지로 설정 된 *image* 요소로 바꿉니다.

[![](overview/_static/image21.png)](overview/_static/image20.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image22.png))

그런 다음 사이트별로 이동 하 고 CSS 클래스 정의를 수정 하 여 페이지의 배경색 뿐만 아니라 헤더의 배경색을 변경할 수 있습니다.

이러한 변경의 결과로 사용자 지정 된 홈 페이지를 매우 적은 노력으로 표시할 수 있습니다.

[![](overview/_static/image24.png)](overview/_static/image23.png)

([전체 크기 이미지를 보려면 클릭](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS 개선 사항

ASP.NET 4의 주요 작업 영역 중 하나는 최신 HTML 표준과 호환 되는 HTML을 렌더링 하는 데 도움을 주는 것입니다. 여기에는 ASP.NET 웹 서버 컨트롤에서 CSS 스타일을 사용 하는 방법이 변경 되었습니다.

#### <a name="compatibility-setting-for-rendering"></a>렌더링에 대 한 호환성 설정

기본적으로 웹 응용 프로그램 또는 웹 사이트가 .NET Framework 4를 대상으로 하는 경우 *pages* 요소의 *controlRenderingCompatibilityVersion* 특성은 "4.0"로 설정 됩니다. 이 요소는 컴퓨터 수준 `Web.config` 파일에 정의 되며 기본적으로 모든 ASP.NET 4 응용 프로그램에 적용 됩니다.

[!code-xml[Main](overview/samples/sample69.xml)]

*ControlRenderingCompatibility* 에 대 한 값은 이후 릴리스에서 새 버전 정의를 잠재적으로 허용 하는 문자열입니다. 현재 릴리스에서이 속성에 대해 지원 되는 값은 다음과 같습니다.

- "3.5". 이 설정은 레거시 렌더링 및 태그를 나타냅니다. 컨트롤에 의해 렌더링 된 태그는 100% 이전 버전과 호환 되며 *Xhtmlconformance* 속성의 설정이 적용 됩니다.
- "4.0". 속성에이 설정이 있으면 ASP.NET 웹 서버 컨트롤은 다음을 수행 합니다.
- *Xhtmlconformance* 속성은 항상 "Strict"로 처리 됩니다. 따라서 컨트롤은 XHTML 1.0 Strict 태그를 렌더링 합니다.
- 비 입력 컨트롤을 사용 하지 않도록 설정 하면 더 이상 잘못 된 스타일이 렌더링 되지 않습니다.
- 숨겨진 필드 주변의 *div* 요소는 이제 사용자가 만든 CSS 규칙을 방해 하지 않도록 스타일이 지정 됩니다.
- 메뉴 컨트롤은 의미 체계가 올바르고 내게 필요한 옵션 지침을 준수 하는 태그를 렌더링 합니다.
- 유효성 검사 컨트롤은 인라인 스타일을 렌더링 하지 않습니다.
- 이전에 렌더링 된 border = "0" (ASP.NET *Table* 컨트롤에서 파생 된 컨트롤 및 ASP.NET *Image* 컨트롤에서 파생 된 컨트롤)은 더 이상이 특성을 렌더링 하지 않습니다.

#### <a name="disabling-controls"></a>컨트롤 비활성화

ASP.NET 3.5 SP1 및 이전 버전에서 프레임 워크는 *Enabled* 속성이 *false*로 설정 된 모든 컨트롤에 대해 HTML 태그에서 *disabled* 특성을 렌더링 합니다. 그러나 HTML 4.01 사양에 따라 *입력* 요소만이 특성을 가져야 합니다.

ASP.NET 4에서 다음 예제와 같이 *controlRenderingCompatibilityVersion* 속성을 "3.5"로 설정할 수 있습니다.

[!code-xml[Main](overview/samples/sample70.xml)]

컨트롤을 사용 하지 않도록 설정 하는 다음과 같은 *레이블* 컨트롤에 대 한 태그를 만들 수 있습니다.

[!code-aspx[Main](overview/samples/sample71.aspx)]

*레이블* 컨트롤은 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample72.html)]

ASP.NET 4에서는 *controlRenderingCompatibilityVersion* 를 "4.0"로 설정할 수 있습니다. 이 경우 컨트롤의 *Enabled* 속성이 *false*로 설정 되어 있으면 *입력* 요소를 렌더링 하는 컨트롤만 *비활성화* 된 특성을 렌더링 합니다. HTML *입력* 요소를 렌더링 하지 않는 컨트롤은 컨트롤에 대해 사용 하지 않도록 설정 된 모양을 정의 하는 데 사용할 수 있는 CSS 클래스를 참조 하는 *클래스* 특성을 렌더링 합니다. 예를 들어 앞의 예제에 표시 된 *레이블* 컨트롤은 다음 태그를 생성 합니다.

[!code-html[Main](overview/samples/sample73.html)]

이 컨트롤에 대해 지정 된 클래스의 기본값은 "aspNetDisabled"입니다. 그러나 *WebControl* 클래스의 정적 *Disabledcssclass* 정적 속성을 설정 하 여이 기본값을 변경할 수 있습니다. 컨트롤 개발자의 경우 *SupportsDisabledAttribute* 속성을 사용 하 여 특정 컨트롤에 사용할 동작을 정의할 수도 있습니다.

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>숨겨진 필드 주위의 div 요소 숨기기

ASP.NET 2.0 이상 버전은 XHTML 표준을 준수 하기 위해 시스템 관련 숨겨진 필드 (예: 뷰 상태 정보를 저장 하는 데 사용 되는 *숨겨진* 요소)를 *div* 요소 내에 렌더링 합니다. 그러나 CSS 규칙이 페이지의 *div* 요소에 영향을 주는 경우이로 인해 문제가 발생할 수 있습니다. 예를 들어 페이지에 숨겨진 *div* 요소 주위에 1 픽셀 줄이 표시 될 수 있습니다. ASP.NET 4에서 ASP.NET에 의해 생성 된 숨겨진 필드를 둘러싸는 *div* 요소는 다음 예제와 같이 CSS 클래스 참조를 추가 합니다.

[!code-html[Main](overview/samples/sample74.html)]

그런 다음, 다음 예제와 같이 ASP.NET에 의해 생성 되는 *숨겨진* 요소에만 적용 되는 CSS 클래스를 정의할 수 있습니다.

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>템플릿 기반 컨트롤에 대 한 외부 테이블 렌더링

기본적으로 템플릿을 지 원하는 다음 ASP.NET 웹 서버 컨트롤은 인라인 스타일을 적용 하는 데 사용 되는 외부 테이블에 자동으로 래핑됩니다.

- *FormView*
- *로그인*
- *PasswordRecovery*
- *ChangePassword*
- *마법사*
- *CreateUserWizard*

태그에서 외부 테이블을 제거할 수 있도록 하는 *RenderOuterTable* 라는 새 속성이 이러한 컨트롤에 추가 되었습니다. 예를 들어 *FormView* 컨트롤의 다음 예를 살펴보세요.

[!code-aspx[Main](overview/samples/sample76.aspx)]

이 태그는 HTML 테이블을 포함 하는 페이지에 다음 출력을 렌더링 합니다.

[!code-html[Main](overview/samples/sample77.html)]

테이블이 렌더링 되지 않도록 하려면 다음 예제와 같이 *FormView* 컨트롤의 *RenderOuterTable* 속성을 설정할 수 있습니다.

[!code-aspx[Main](overview/samples/sample78.aspx)]

이전 예제에서는 *테이블*, *tr*및 *td* 요소 없이 다음 출력을 렌더링 합니다.

> 콘텐츠

이러한 향상 된 기능을 통해 컨트롤에서 예기치 않은 태그가 렌더링 되지 않으므로 CSS를 사용 하 여 컨트롤 내용의 스타일을 보다 쉽게 지정할 수 있습니다.

> [!NOTE]
> 참고 이렇게 변경 하면 자동 서식 옵션으로 생성 된 스타일 특성을 호스트할 수 있는 *테이블* 요소가 더 이상 없기 때문에 Visual Studio 2010 디자이너에서 자동 서식 함수를 지원할 수 없습니다.

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView 컨트롤의 향상 된 기능

*ListView* 컨트롤은 ASP.NET 4에서 더 쉽게 사용할 수 있게 되었습니다. 이전 버전의 컨트롤에서는 알려진 ID의 서버 컨트롤을 포함 하는 레이아웃 템플릿을 지정 해야 했습니다. 다음 태그는 ASP.NET 3.5에서 *ListView* 컨트롤을 사용 하는 방법의 일반적인 예를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample79.aspx)]

ASP.NET 4에서는 *ListView* 컨트롤에 레이아웃 템플릿이 필요 하지 않습니다. 이전 예제에 표시 된 태그를 다음 태그로 바꿀 수 있습니다.

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 및 RadioButtonList 제어 기능 향상

ASP.NET 3.5에서는 다음 두 가지 설정을 사용 하 여 *CheckBoxList* 및 *RadioButtonList* 에 대 한 레이아웃을 지정할 수 있습니다.

- *Flow*. 컨트롤은 해당 콘텐츠를 포함 하는 *범위* 요소를 렌더링 합니다.
- *테이블*. 컨트롤은 해당 콘텐츠를 포함 하는 *table* 요소를 렌더링 합니다.

다음 예제에서는 이러한 각 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample81.aspx)]

기본적으로 컨트롤은 다음과 유사한 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample82.html)]

이러한 컨트롤은 항목 목록을 포함 하므로 의미상 올바른 HTML을 렌더링 하기 위해*li*(html 목록) 요소를 사용 하 여 콘텐츠를 렌더링 해야 합니다. 이렇게 하면 보조 기술을 사용 하 여 웹 페이지를 읽는 사용자가 더 쉽게 작업할 수 있으며 CSS를 사용 하 여 컨트롤의 스타일을 보다 쉽게 만들 수 있습니다.

ASP.NET 4에서 *CheckBoxList* 및 *RadioButtonList* 컨트롤은 *RepeatLayout* 속성에 대해 다음과 같은 새 값을 지원 합니다.

- *OrderedList* – 콘텐츠가 *ol* 요소 내에서 *li* 요소로 렌더링 됩니다.
- *UnorderedList* – 콘텐츠가 *ul* 요소 내에서 *li* 요소로 렌더링 됩니다.

다음 예제에서는 이러한 새 값을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample83.aspx)]

위의 태그는 다음 HTML을 생성 합니다.

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 참고 *RepeatLayout* 를 *OrderedList* 또는 *UnorderedList*로 설정 하는 경우 *RepeatDirection* 속성을 더 이상 사용할 수 없으며, 속성이 태그 또는 코드 내에 설정 된 경우 런타임에 예외가 throw 됩니다. 이러한 컨트롤의 시각적 레이아웃은 CSS를 사용 하 여 정의 되기 때문에 속성에는 값이 없습니다.

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>메뉴 컨트롤 개선

ASP.NET 4 이전에는 *Menu* 컨트롤이 일련의 HTML 테이블을 렌더링 했습니다. 이렇게 하면 인라인 속성 설정 외에 CSS 스타일을 적용 하기가 더 어려워집니다. 또한 액세스 가능성 표준과 호환 되지 않습니다.

ASP.NET 4에서 컨트롤은 이제 순서가 지정 되지 않은 목록 및 목록 요소로 구성 된 의미 태그를 사용 하 여 HTML을 렌더링 합니다. 다음 예제에서는 *Menu* 컨트롤에 대 한 ASP.NET 페이지의 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample85.aspx)]

페이지가 렌더링 되 면 컨트롤은 다음 HTML을 생성 합니다 (명확성을 위해 *onclick* 코드는 생략 됨).

[!code-html[Main](overview/samples/sample86.html)]

렌더링 기능 향상 외에도, 포커스 관리를 사용 하 여 메뉴의 키보드 탐색 기능이 향상 되었습니다. *메뉴* 컨트롤이 포커스를 가져오는 경우 화살표 키를 사용 하 여 요소를 탐색할 수 있습니다. 또한 *메뉴* 컨트롤은 내게 필요한 옵션을 향상 시키기 위해 액세스 가능한 리치 인터넷 응용 프로그램 (ARIA) 역할 및 특성을 ([에](http://www.w3.org/TR/wai-aria-practices/#menu "메뉴 ARIA 지침")연결 합니다.

메뉴 컨트롤에 대 한 스타일은 렌더링 된 HTML 요소를 포함 하는 대신 페이지 맨 위에 있는 스타일 블록에서 렌더링 됩니다. 컨트롤의 스타일을 완벽 하 게 제어 하려면 새 *IncludeStyleBlock* 속성을 *false*로 설정 하면 됩니다 .이 경우 스타일 블록은 내보내지지 않습니다. 이 속성을 사용 하는 한 가지 방법은 Visual Studio 디자이너의 자동 서식 기능을 사용 하 여 메뉴의 모양을 설정 하는 것입니다. 그런 다음 페이지를 실행 하 고 페이지 소스를 연 다음 렌더링 된 스타일 블록을 외부 CSS 파일에 복사할 수 있습니다. Visual Studio에서 스타일을 실행 취소 하 고 *IncludeStyleBlock* 을 *false*로 설정 합니다. 그 결과 메뉴 모양이 외부 스타일 시트의 스타일을 사용 하 여 정의 됩니다.

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>Wizard 및 CreateUserWizard 컨트롤

ASP.NET *마법사* 및 *CreateUserWizard* 컨트롤은 렌더링 되는 HTML을 정의 하는 데 사용할 수 있는 템플릿을 지원 합니다. (*CreateUserWizard* 는 *마법사*에서 파생 됩니다.) 다음 예제에서는 완전히 템플릿 기반 *CreateUserWizard* 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample87.aspx)]

컨트롤은 다음과 유사한 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample88.html)]

ASP.NET 3.5 s p 1에서 템플릿 콘텐츠를 변경할 수 있지만 *마법사* 컨트롤의 출력에 대 한 제한 된 제어를 유지 합니다. ASP.NET 4에서는 *이 layouttemplate* 템플릿을 만들고, 예약 된 이름을 사용 하 여 *자리 표시자* 컨트롤을 삽입 하 여 *마법사 컨트롤이* 렌더링 되는 방법을 지정할 수 있습니다. 다음 예제에서는이를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample89.aspx)]

이 예에는 *이 layouttemplate* 요소에 다음과 같은 명명 된 자리 표시 자가 포함 되어 있습니다.

- *Headerplaceholder* – 런타임에 *HeaderTemplate* 요소의 콘텐츠로 대체 됩니다.
- 나란히 표시 되는 *자리 표시자* – 런타임에는이를 외부 항목 *템플릿* 요소의 콘텐츠로 대체 합니다.
- *wizardstststststststststststststststststststststststststststststat*
- *Navigationplaceholder* – 런타임에 사용자가 정의한 탐색 템플릿으로 대체 됩니다.

자리 표시자를 사용 하는 예제의 태그는 템플릿에 실제로 정의 된 내용이 없는 다음 HTML을 렌더링 합니다.

[!code-html[Main](overview/samples/sample90.html)]

현재 사용자 정의 되지 않은 HTML만 *범위* 요소입니다. 이후 릴리스에서는 *span* 요소도 렌더링 되지 않을 것으로 예상 합니다. 이제 *마법사* 컨트롤에 의해 생성 되는 거의 모든 콘텐츠를 완전히 제어할 수 있습니다.

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC는 3 월 2009에 ASP.NET 3.5 s p 1의 추가 기능 프레임 워크로 도입 되었습니다. Visual Studio 2010에는 새로운 기능과 기능을 포함 하는 ASP.NET MVC 2가 포함 되어 있습니다.

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>영역 지원

영역을 사용 하면 컨트롤러 및 뷰를 다른 섹션과 상대적으로 격리 된 많은 응용 프로그램의 섹션으로 그룹화 할 수 있습니다. 각 영역은 주 응용 프로그램에서 참조할 수 있는 별도의 ASP.NET MVC 프로젝트로 구현할 수 있습니다. 이렇게 하면 규모가 많은 응용 프로그램을 빌드하는 경우 복잡성을 관리 하 고, 여러 팀이 단일 응용 프로그램에서 함께 작업할 수 있도록 합니다.

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>데이터 주석 특성 유효성 검사 지원

*Dataannotations* 특성을 사용 하면 메타 데이터 특성을 사용 하 여 유효성 검사 논리를 모델에 연결할 수 있습니다. *Dataannotations* 특성은 ASP.NET Dynamic Data ASP.NET 3.5 s p 1에서 도입 되었습니다. 이러한 특성은 기본 모델 바인더에 통합 되어 사용자 입력의 유효성을 검사 하는 메타 데이터 기반 수단을 제공 합니다.

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>템플릿 기반 도우미

템플릿 기반 도우미를 사용 하면 편집 및 표시 템플릿을 데이터 형식과 자동으로 연결할 수 있습니다. 예를 들어 템플릿 도우미를 사용 하 여 날짜 선택 UI 요소가 *시스템의 DateTime* 값에 대해 자동으로 렌더링 되도록 지정할 수 있습니다. 이는 ASP.NET Dynamic Data의 필드 템플릿과 비슷합니다.

도우미에 대 한 *html* . *a* p a. a p a. i a. a p a. 또한 *DisplayName* 및 *ScaffoldColumn* 와 같은 데이터 주석 특성을 *ViewModel* 개체에 적용할 수 있도록 하 여 렌더링을 사용자 지정 합니다.

UI 도우미의 출력을 추가로 사용자 지정 하 고 생성 되는 내용을 완전히 제어 하려는 경우가 종종 있습니다. 도우미에 대 한 *html* . *p* a p. i p v의 경우에는 렌더링 된 출력을 재정의 하 고 제어할 수 있는 외부 템플릿을 정의할 수 있는 템플릿 메커니즘을 사용 하 여이를 지원 합니다. 템플릿은 클래스에 대해 개별적으로 렌더링 될 수 있습니다.

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data

Dynamic Data는 2008의 .NET Framework 3.5 SP1 릴리스에서 도입 되었습니다. 이 기능은 다음을 포함 하 여 데이터 기반 응용 프로그램을 만들기 위한 다양 한 향상 된 기능을 제공 합니다.

- 데이터 기반 웹 사이트를 신속 하 게 빌드하기 위한 RAD 환경입니다.
- 데이터 모델에 정의 된 제약 조건을 기반으로 하는 자동 유효성 검사입니다.
- Dynamic Data 프로젝트의 일부인 필드 템플릿을 사용 하 여 *GridView* 및 *DetailsView* 컨트롤의 필드에 대해 생성 되는 태그를 쉽게 변경할 수 있습니다.

> [!NOTE]
> 참고 자세한 내용은 MSDN Library의 [Dynamic Data 설명서](https://msdn.microsoft.com/library/cc488545.aspx) 를 참조 하십시오.

ASP.NET 4의 경우 개발자가 데이터 기반 웹 사이트를 신속 하 게 빌드할 수 있는 더 많은 기능을 제공 하도록 Dynamic Data 향상 되었습니다.

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>기존 프로젝트에 대 한 Dynamic Data 사용

Dynamic Data .NET Framework 3.5 s p 1에서 제공 되는 기능은 다음과 같은 새로운 기능을 제공 합니다.

- 필드 템플릿 – 데이터 바인딩된 컨트롤에 대 한 데이터 형식 기반 템플릿을 제공 합니다. 필드 템플릿은 각 필드에 대 한 템플릿 필드를 사용 하는 것 보다 간단 하 게 데이터 컨트롤의 모양을 사용자 지정 하는 방법을 제공 합니다.
- 유효성 검사 – Dynamic Data를 사용 하면 데이터 클래스에서 특성을 사용 하 여 필수 필드, 범위 검사, 형식 검사, 정규식을 사용한 패턴 일치 및 사용자 지정 유효성 검사와 같은 일반적인 시나리오에 대 한 유효성 검사를 지정할 수 있습니다. 유효성 검사는 데이터 컨트롤에 의해 적용 됩니다.

그러나 이러한 기능에는 다음과 같은 요구 사항이 있습니다.

- 데이터 액세스 계층은 Entity Framework 또는 LINQ to SQL를 기반으로 해야 합니다.
- 이러한 기능에 대해 지원 되는 데이터 원본 컨트롤은 *EntityDataSource* 또는 *LinqDataSource* 컨트롤 뿐입니다.
- 이 기능을 사용 하려면 기능을 지 원하는 데 필요한 모든 파일을 포함 하기 위해 Dynamic Data 또는 Dynamic Data 엔터티 템플릿을 사용 하 여 만든 웹 프로젝트가 필요 합니다.

ASP.NET 4에서 Dynamic Data 지원의 주요 목표는 모든 ASP.NET 응용 프로그램에 대해 Dynamic Data의 새로운 기능을 사용 하도록 설정 하는 것입니다. 다음 예제에서는 기존 페이지의 Dynamic Data 기능을 활용할 수 있는 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample91.aspx)]

페이지의 코드에서 다음 코드를 추가 해야 이러한 컨트롤에 대 한 Dynamic Data 지원을 사용할 수 있습니다.

[!code-csharp[Main](overview/samples/sample92.cs)]

*GridView* 컨트롤이 편집 모드에 있으면 Dynamic Data는 입력 한 데이터가 적절 한 형식 인지 자동으로 유효성을 검사 합니다. 그렇지 않으면 오류 메시지가 표시 됩니다.

이 기능은 삽입 모드에 대 한 기본값을 지정할 수 있는 등의 다른 이점도 제공 합니다. Dynamic Data 하지 않고 필드의 기본값을 구현 하려면 이벤트에 연결 하 고 컨트롤을 찾아 ( *FindControl*사용) 해당 값을 설정 해야 합니다. ASP.NET 4에서 *EnableDynamicData* 호출은 다음 예제와 같이 개체의 모든 필드에 대 한 기본값을 전달할 수 있는 두 번째 매개 변수를 지원 합니다.

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>선언적 DynamicDataManager 컨트롤 구문

*DynamicDataManager* 컨트롤은 코드 뿐 아니라 ASP.NET의 대부분 컨트롤과 마찬가지로 선언적으로 구성할 수 있도록 향상 되었습니다. *DynamicDataManager* 컨트롤에 대 한 태그는 다음 예제와 같습니다.

[!code-aspx[Main](overview/samples/sample94.aspx)]

이 태그를 사용 하면 *DynamicDataManager* 컨트롤의 *DataControls* 섹션에서 참조 되는 GridView1 컨트롤에 대 한 Dynamic Data 동작을 사용할 수 있습니다.

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>엔터티 템플릿

엔터티 템플릿은 사용자 지정 페이지를 만들지 않고도 데이터의 레이아웃을 사용자 지정할 수 있는 새로운 방법을 제공 합니다. 페이지 템플릿은 이전 버전의 Dynamic Data에서 페이지 템플릿에서 사용 되는 *DetailsView* 컨트롤 대신 *FormView* 컨트롤을 사용 하 고, 엔터티 템플릿을 렌더링 하는 *dynamicentity* 컨트롤을 사용 합니다. 이렇게 하면 Dynamic Data에 의해 렌더링 되는 태그를 더 효과적으로 제어할 수 있습니다.

다음 목록에서는 엔터티 템플릿이 포함 된 새 프로젝트 디렉터리 레이아웃을 보여 줍니다.

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate` 디렉터리에는 데이터 모델 개체를 표시 하는 방법에 대 한 템플릿이 포함 되어 있습니다. 기본적으로 개체는 ASP.NET 3.5 s p 1의 Dynamic Data에서 사용 하는 *DetailsView* 컨트롤에 의해 생성 된 태그와 같이 보이는 태그를 제공 하는 `Default.ascx` 템플릿을 사용 하 여 렌더링 됩니다. 다음 예제에서는 `Default.ascx` 컨트롤에 대 한 태그를 보여 줍니다.

[!code-aspx[Main](overview/samples/sample96.aspx)]

기본 템플릿을 편집 하 여 전체 사이트의 모양과 느낌을 변경할 수 있습니다. 표시, 편집 및 삽입 작업에 대 한 템플릿이 있습니다. 데이터 개체의 이름을 기준으로 새 템플릿을 추가 하 여 하나의 개체 형식에 대 한 모양과 느낌을 변경할 수 있습니다. 예를 들어 다음 템플릿을 추가할 수 있습니다.

[!code-console[Main](overview/samples/sample97.cmd)]

템플릿에는 다음 태그가 포함 될 수 있습니다.

[!code-aspx[Main](overview/samples/sample98.aspx)]

새 *dynamicentity* 컨트롤을 사용 하 여 새 엔터티 템플릿이 페이지에 표시 됩니다. 런타임에이 컨트롤이 엔터티 템플릿의 콘텐츠로 바뀝니다. 다음 태그는 엔터티 템플릿을 사용 하는 `Detail.aspx` 페이지 템플릿의 *FormView* 컨트롤을 보여 줍니다. 태그에서 *Dynamicentity* 요소를 확인 합니다.

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Url 및 전자 메일 주소에 대 한 새 필드 템플릿

ASP.NET 4에서는 두 개의 새로운 기본 제공 필드 템플릿 `EmailAddress.ascx` 및 `Url.ascx`를 소개 합니다. 이러한 템플릿은 *EmailAddress* 로 표시 된 필드나 *DataType* 특성을 가진 *Url* 에 사용 됩니다. *EmailAddress* 개체의 경우에는 *mailto:* 프로토콜을 사용 하 여 만든 하이퍼링크로 필드가 표시 됩니다. 사용자가 링크를 클릭 하면 사용자의 전자 메일 클라이언트를 열고 기본 메시지를 만듭니다. *Url* 로 입력 된 개체는 일반 하이퍼링크로 표시 됩니다.

다음 예에서는 필드를 표시 하는 방법을 보여 줍니다.

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>DynamicHyperLink 컨트롤을 사용 하 여 링크 만들기

Dynamic Data는 .NET Framework 3.5 s p 1에 추가 된 새 라우팅 기능을 사용 하 여 최종 사용자가 웹 사이트에 액세스할 때 표시 하는 Url을 제어 합니다. 새 *DynamicHyperLink* 컨트롤을 사용 하면 Dynamic Data 사이트의 페이지에 대 한 링크를 쉽게 빌드할 수 있습니다. 다음 예제에서는 *DynamicHyperLink* 컨트롤을 사용 하는 방법을 보여 줍니다.

[!code-aspx[Main](overview/samples/sample101.aspx)]

이 태그는 `Global.asax` 파일에 정의 된 경로를 기반으로 `Products` 테이블에 대 한 목록 페이지를 가리키는 링크를 만듭니다. 컨트롤은 Dynamic Data 페이지의 기반이 되는 기본 테이블 이름을 자동으로 사용 합니다.

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>데이터 모델의 상속에 대 한 지원

Entity Framework와 LINQ to SQL는 모두 해당 데이터 모델에서 상속을 지원 합니다. 이에 대 한 예는 `InsurancePolicy` 테이블이 있는 데이터베이스 일 수 있습니다. `InsurancePolicy`와 동일한 필드가 있는 `CarPolicy` 및 `HousePolicy` 테이블을 포함 하 고 필드를 더 추가할 수도 있습니다. Dynamic Data는 데이터 모델의 상속 된 개체를 이해 하 고 상속 된 테이블에 대 한 스 캐 폴딩을 지원 하도록 수정 되었습니다.

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>다 대 다 관계에 대 한 지원 (Entity Framework에만 해당)

Entity Framework는 *엔터티* 개체의 컬렉션으로 관계를 노출 하 여 구현 되는 테이블 간의 다 대 다 관계에 대 한 다양 한 지원을 제공 합니다. 다 대 다 관계에 관련 된 데이터를 표시 하 고 편집할 수 있도록 새 `ManyToMany.ascx` 및 `ManyToMany_Edit.ascx` 필드 템플릿이 추가 되었습니다.

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>표시 및 지원 열거를 제어 하기 위한 새 특성

*Displayattribute* 를 추가 하 여 필드가 표시 되는 방법을 보다 세밀 하 게 제어할 수 있습니다. 이전 버전의 Dynamic Data *DisplayName* 특성을 사용 하 여 필드의 캡션으로 사용 되는 이름을 변경할 수 있었습니다. 새 *Displayattribute* 클래스를 사용 하면 필드가 표시 되는 순서 및 필드가 필터로 사용 되는지 여부와 같은 필드 표시에 대 한 추가 옵션을 지정할 수 있습니다. 또한 특성은 *GridView* 컨트롤의 레이블에 사용 되는 이름, *DetailsView* 컨트롤에서 사용 되는 이름, 필드에 대 한 도움말 텍스트 및 필드에 사용 되는 워터 마크 (필드가 텍스트 입력을 받아들이는 경우)에 사용 되는 이름을 독립적으로 제어 합니다.

*EnumDataTypeAttribute* 클래스가 추가 되어 필드를 열거형에 매핑할 수 있습니다. 필드에이 특성을 적용 하는 경우 열거형 형식을 지정 합니다. Dynamic Data는 새 `Enumeration.ascx` 필드 템플릿을 사용 하 여 열거형 값을 표시 하 고 편집 하는 UI를 만듭니다. 템플릿은 데이터베이스의 값을 열거형의 이름에 매핑합니다.

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>향상 된 필터 지원

Dynamic Data 1.0은 부울 열과 외래 키 열에 대 한 기본 제공 필터와 함께 제공 됩니다. 필터를 사용 하 여 표시 되었는지 아니면 표시 되는 순서를 지정할 수 없습니다. 새 *Displayattribute* 특성은 열이 필터로 표시 되는지 여부를 제어 하 고 표시 되는 순서를 제어 하 여 이러한 문제를 모두 해결 합니다.

추가 기능 향상으로 인해 Web Forms의[새로운 기능을 사용 하도록](#0.2__QueryExtender "_QueryExtender") 필터링 지원이 다시 작성 되었습니다. 이렇게 하면 필터를 사용할 데이터 소스 컨트롤에 대 한 지식이 없어도 필터를 만들 수 있습니다. 이러한 확장과 함께 필터도 템플릿 컨트롤로 확장 되어 새 필터를 추가할 수 있습니다. 마지막으로 언급 된 *Displayattribute* 클래스를 사용 하 여 기본 필터를 재정의할 수 있습니다. *UIHint* 는 열에 대 한 기본 필드 템플릿이 재정의 되도록 허용 하는 것과 동일한 방식으로 기본 필터를 재정의할 수 있습니다.

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 웹 개발 개선 사항

Visual Studio 2010의 웹 개발은 CSS 호환성이 향상 되었으며 HTML 및 ASP.NET 마크업 코드 조각 및 새로운 동적 IntelliSense JavaScript를 통해 생산성을 향상 시켰습니다.

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>향상 된 CSS 호환성

Visual Studio 2010의 Visual Web Developer designer가 CSS 2.1 표준 준수를 개선 하도록 업데이트 되었습니다. 디자이너는 HTML 소스의 무결성을 더 잘 유지 하 고 이전 버전의 Visual Studio 보다 더 강력 합니다. 내부적으로 아키텍처를 개선 하 여 렌더링, 레이아웃 및 서비스 가능성을 향상 시킬 수 있습니다.

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 및 JavaScript 코드 조각

HTML 편집기에서 IntelliSense는 태그 이름을 자동으로 완성 합니다. IntelliSense 코드 조각 기능은 전체 태그 등을 자동으로 완성 합니다. Visual Studio 2010에서 IntelliSense 코드 조각은 이전 버전의 Visual Studio에서 C# 지원 되는 및 Visual Basic와 함께 JavaScript에 대해 지원 됩니다.

Visual Studio 2010에는 필수 특성 (예: runat = "server") 및 태그와 관련 된 공통 특성 (예: *ID*, *DataSourceID*, *ControlToValidate*및 *텍스트*)을 비롯 하 여 일반적인 ASP.NET 및 HTML 태그를 자동으로 완성 하는 데 도움이 되는 200 개 이상의 코드 조각이 포함 되어 있습니다.

추가 코드 조각을 다운로드 하거나 사용자 또는 팀에서 일반 작업에 사용 하는 태그 블록을 캡슐화 하는 사용자 고유의 코드 조각을 작성할 수 있습니다.

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense의 향상 된 기능

Visual 2010에서 JavaScript IntelliSense는 훨씬 더 풍부한 편집 환경을 제공 하도록 다시 디자인 되었습니다. IntelliSense는 이제 *Registernamespace* 와 같은 메서드 및 다른 JavaScript 프레임 워크에서 사용 하는 유사한 기법에 의해 동적으로 생성 된 개체를 인식 합니다. 스크립트의 많은 라이브러리를 분석 하 고 처리 지연이 거의 없거나 전혀 없는 IntelliSense를 표시 하는 성능이 향상 되었습니다. 거의 모든 타사 라이브러리를 지원 하 고 다양 한 코딩 스타일을 지원 하기 위해 호환성이 크게 늘어났습니다. 이제 사용자가 입력 하면 문서 주석이 구문 분석 되 고 IntelliSense에서 즉시 활용 됩니다.

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>Visual Studio 2010을 사용 하 여 웹 응용 프로그램 배포

ASP.NET 개발자가 웹 응용 프로그램을 배포 하는 경우 다음과 같은 문제가 발생 하는 경우가 많습니다.

- 공유 호스팅 사이트에 배포 하는 데는 FTP와 같은 기술이 필요 하며이는 속도가 느릴 수 있습니다. 또한 SQL 스크립트를 실행 하 여 데이터베이스를 구성 하는 등의 작업을 수동으로 수행 해야 하며 가상 디렉터리 폴더를 응용 프로그램으로 구성 하는 등의 IIS 설정을 변경 해야 합니다.
- 엔터프라이즈 환경에서 웹 응용 프로그램 파일을 배포 하는 것 외에도 관리자는 종종 ASP.NET 구성 파일 및 IIS 설정을 수정 해야 합니다. 데이터베이스 관리자는 일련의 SQL 스크립트를 실행 하 여 응용 프로그램 데이터베이스를 실행 해야 합니다. 이러한 설치는 많은 노력이 필요 하며, 작업을 완료 하는 데 몇 시간 정도 걸리며, 신중 하 게 문서화 해야 합니다.

Visual Studio 2010에는 이러한 문제를 해결 하 고 웹 응용 프로그램을 원활 하 게 배포할 수 있는 기술이 포함 되어 있습니다. 이러한 기술 중 하나는 IIS 웹 배포 도구 (Msdeploy.exe)입니다.

Visual Studio 2010의 웹 배포 기능에는 다음과 같은 주요 영역이 포함 되어 있습니다.

- 웹 패키징
- Web.config 변환
- 데이터베이스 배포
- 한 번 클릭으로 웹 응용 프로그램 게시

다음 섹션에서는 이러한 기능에 대해 자세히 설명 합니다.

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>웹 패키징

Visual Studio 2010는 Msdeploy.exe 도구를 사용 하 여 응용 프로그램에 대 한 압축 (.zip) 파일을 만듭니다 .이 파일을 *웹 패키지*라고 합니다. 패키지 파일에는 응용 프로그램에 대 한 메타 데이터와 다음 콘텐츠가 포함 됩니다.

- 응용 프로그램 풀 설정, 오류 페이지 설정 등을 포함 하는 IIS 설정
- 웹 페이지, 사용자 정의 컨트롤, 정적 콘텐츠 (이미지 및 HTML 파일) 등을 포함 하는 실제 웹 콘텐츠
- 데이터베이스 스키마 및 데이터를 SQL Server 합니다.
- 보안 인증서, GAC에 설치 하는 구성 요소, 레지스트리 설정 등에 있습니다.

웹 패키지를 모든 서버에 복사한 다음 IIS 관리자를 사용 하 여 수동으로 설치할 수 있습니다. 또는 자동 배포의 경우 명령줄 명령을 사용 하거나 배포 Api를 사용 하 여 패키지를 설치할 수 있습니다.

Visual Studio 2010은 웹 패키지를 만들기 위한 기본 제공 MSBuild 작업 및 대상을 제공 합니다. 자세한 내용은 MSDN 웹 사이트에서 [ASP.NET 웹 응용 프로그램 프로젝트 배포 개요](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx) 를 참조 하 고 인 vishal Joshi의 블로그에서 [웹 패키지를 만들어야 하는 10 개](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html) 이상의 이유를 참조 하세요.

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 변환

웹 응용 프로그램 배포의 경우 Visual Studio 2010에는 `Web.config` 파일을 개발 설정에서 프로덕션 설정으로 변환할 수 있는 기능인 [XML 문서 변환 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)이 도입 되었습니다. 변환 설정은 `web.debug.config`, `web.release.config`등의 변환 파일에 지정 됩니다. 이러한 파일의 이름은 MSBuild 구성과 일치 합니다. 변환 파일에는 배포 된 `Web.config` 파일에 수행 해야 하는 변경 내용만 포함 됩니다. 간단한 구문을 사용 하 여 변경 내용을 지정 합니다.

다음 예제에서는 릴리스 구성의 배포에 대해 생성 될 수 있는 `web.release.config` 파일의 일부를 보여 줍니다. 예제의 Replace 키워드는 배포 하는 동안 `Web.config` 파일의 *connectionString* 노드가 예제에 나열 된 값으로 대체 되도록 지정 합니다.

[!code-xml[Main](overview/samples/sample102.xml)]

자세한 내용은 MSDN <a id="0.2_a"></a> 웹 사이트 및[웹 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 의 웹 [응용 프로그램 프로젝트 배포를 위한 Web.config 변환 구문](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx) (인 vishal Joshi의 블로그에서 web.config 변환)을 참조 하세요.

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>데이터베이스 배포

Visual Studio 2010 배포 패키지에 SQL Server 데이터베이스에 대 한 종속성이 포함 될 수 있습니다. 패키지 정의의 일부로 원본 데이터베이스에 대 한 연결 문자열을 제공 합니다. 웹 패키지를 만들 때 Visual Studio 2010는 데이터베이스 스키마에 대 한 SQL 스크립트를 만든 다음 필요에 따라 데이터를 패키지에 추가 합니다. 또한 사용자 지정 SQL 스크립트를 제공 하 고 서버에서 실행 해야 하는 순서를 지정할 수 있습니다. 배포 시 대상 서버에 적절 한 연결 문자열을 제공 합니다. 그러면 배포 프로세스에서이 연결 문자열을 사용 하 여 데이터베이스 스키마를 만들고 데이터를 추가 하는 스크립트를 실행 합니다.

또한 한 번 클릭 게시를 사용 하 여 응용 프로그램이 원격 공유 호스팅 사이트에 게시 될 때 데이터베이스를 직접 게시 하도록 배포를 구성할 수 있습니다. 자세한 내용은 MSDN 웹 사이트에서 [웹 응용 프로그램 프로젝트를 사용 하 여 데이터베이스 배포](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx) 및 인 vishal Joshi의 블로그에서 [VS 2010를 사용 하 여 데이터베이스 배포](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) 를 참조 하세요.

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>한 번 클릭으로 웹 응용 프로그램 게시

Visual Studio 2010에서는 IIS 원격 관리 서비스를 사용 하 여 원격 서버에 웹 응용 프로그램을 게시할 수도 있습니다. 호스팅 계정 또는 테스트 서버나 준비 서버에 대 한 게시 프로필을 만들 수 있습니다. 각 프로필은 적절 한 자격 증명을 안전 하 게 저장할 수 있습니다. 그런 다음 한 번 클릭으로 웹 게시 도구 모음을 클릭 하 여 대상 서버에 배포할 수 있습니다. Visual Studio 2010에서는 MSBuild 명령줄을 사용 하 여 게시할 수도 있습니다. 이렇게 하면 연속 통합 모델에 게시를 포함 하도록 팀 빌드 환경을 구성할 수 있습니다.

자세한 내용은 MSDN 웹 사이트 및 웹에서 [한 번 클릭 게시 및 웹 배포를 사용 하 여 웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx) -인 vishal Joshi의 블로그에서 [VS 2010를 사용 하 여 게시를 클릭](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html) 하세요. Visual Studio 2010의 웹 응용 프로그램 배포에 대 한 비디오 프레젠테이션을 보려면 인 vishal Joshi의 블로그에서 [VS 2010 For Web Developer](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) preview를 참조 하세요.

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>리소스

다음 웹 사이트는 ASP.NET 4 및 Visual Studio 2010에 대 한 추가 정보를 제공 합니다.

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 웹 사이트에 있는 ASP.NET 4의 공식 설명서입니다.
- [https://www.asp.net/](https://www.asp.net/) -ASP.NET 팀 자체의 웹 사이트입니다.
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx) 및 [ASP.NET Dynamic Data 콘텐츠 맵](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx) -ASP.NET 팀 사이트의 온라인 리소스와 ASP.NET Dynamic Data 공식 설명서를 참조 하세요.
- [https://www.asp.net/ajax/](../../ajax/index.md) -ASP.NET Ajax 개발을 위한 주 웹 리소스입니다.
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/) -visual Studio 2010의 기능에 대 한 정보를 포함 하는 Visual Web Developer 팀 블로그입니다.
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET의 미리 보기 릴리스에 대 한 주 웹 리소스입니다.

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>고지 사항

본 문서는 예비 문서이며, 여기에 설명한 소프트웨어의 최종 상업적 출시 전에 크게 변경될 수 있습니다.

이 문서에 포함된 정보는 게시 날짜 당시 논의된 문제에 대한 Microsoft Corporation의 현재 관점을 나타냅니다. Microsoft는 변화하는 시장 상황에 대응해야 하므로 Microsoft의 약속으로 해석되지 않아야 하며, Microsoft는 게시 날짜 이후 제시된 정보의 정확성을 보증하지 않습니다.

이 백서는 정보를 제공할 목적으로만 사용됩니다. MICROSOFT는 이 문서에 포함된 정보와 관련하여 명시적이든 암시적이든 어떠한 보증도 하지 않습니다.

해당 저작권법을 준수하는 것은 사용자의 책임입니다. 저작권에서의 권리와는 별도로 이 설명서의 어떠한 부분도 Microsoft의 명시적인 서면 승인 없이는 어떠한 형식이나 수단(전기적, 기계적, 복사기에 의한 복사, 디스크 복사 또는 다른 방법) 또는 목적으로도 복제되거나 검색 시스템에 저장 또는 도입되거나 전송될 수 없습니다.

Microsoft는 이 설명서 본안에 관련된 특허권, 상표권, 저작권, 또는 기타 지적 재산권 등을 보유할 수도 있습니다. 서면 사용권 계약에 따라 Microsoft로부터 귀하에게 명시적으로 제공된 권리 이외에, 이 설명서의 제공은 귀하에게 이러한 특허권, 상표권, 저작권 또는 기타 지적 재산권 등에 대한 어떠한 사용권도 허용하지 않습니다.

별도로 언급 하지 않는 한, 용례에 사용 된 회사, 조직, 제품, 도메인 이름, 전자 메일 주소, 로고, 사람, 장소 및 이벤트는 실제 데이터가 아닙니다. 어떠한 실제 회사, 조직, 제품, 도메인 이름, 전자 메일에도 연결 되지 않습니다. 주소, 로고, 사람, 장소 또는 이벤트를 작성 하거나 유추 해야 합니다.

© 2009 Microsoft Corporation. All rights reserved.

Microsoft 및 Windows는 미국 및/또는 기타 국가에서 Microsoft Corporation의 상표이거나 등록된 상표입니다.

여기에 인용된 실제 회사와 제품 이름은 해당 소유자의 상표일 수 있습니다.
