---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2-ASP.NET 4.x 구성
author: MikeWasson
description: 'ASP.NET 4.x에 대해 2 ASP.NET Web API 구성: 설정, ASP.NET 4.x 호스팅, OWIN 셀프 호스팅, 글로벌 서비스 및 이전 컨트롤러 구성을 구성 합니다.'
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449345"
---
# <a name="configuring-aspnet-web-api-2"></a>ASP.NET Web API 2 구성

[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 ASP.NET Web API를 구성 하는 방법에 대해 설명 합니다.

- [구성 설정](#settings)
- [ASP.NET 호스팅을 사용 하 여 Web API 구성](#webhost)
- [OWIN 자체 호스팅을 사용 하 여 Web API 구성](#selfhost)
- [전역 웹 API 서비스](#services)
- [컨트롤러 단위 구성](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>구성 설정

웹 API 구성 설정은 [httpconfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) 클래스에서 정의 됩니다.

| 멤버 | Description |
| --- | --- |
| **DependencyResolver** | 컨트롤러에 대 한 종속성 주입을 사용 합니다. [웹 API 종속성 해결 프로그램 사용을](dependency-injection.md)참조 하세요. |
| **필터** | 작업 필터. |
| **포맷터** | [미디어 유형 포맷터](../formats-and-model-binding/media-formatters.md)입니다. |
| **IncludeErrorDetailPolicy** | HTTP 응답 메시지에 예외 메시지 및 스택 추적과 같은 오류 정보를 서버에 포함할지 여부를 지정 합니다. [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108))를 참조 하세요. |
| **이니셜라이저** | **Httpconfiguration**의 최종 초기화를 수행 하는 함수입니다. |
| **MessageHandlers** | [HTTP 메시지 처리기](http-message-handlers.md)입니다. |
| **ParameterBindingRules** | 컨트롤러 작업에 대 한 매개 변수를 바인딩하는 규칙의 컬렉션입니다. |
| **속성** | 일반 속성 모음입니다. |
| **경로** | 경로 컬렉션입니다. [ASP.NET Web API에서 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)참조 하세요. |
| **Services** | 서비스의 컬렉션입니다. [서비스](#services)를 참조 하세요. |

## <a name="prerequisites"></a>사전 요구 사항

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise 버전

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>ASP.NET 호스팅을 사용 하 여 Web API 구성

ASP.NET 응용 프로그램에서 **응용 프로그램\_Start** 메서드에서 [Globalconfiguration. 구성](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) 을 호출 하 여 Web API를 구성 합니다. **Configure** 메서드는 **httpconfiguration**형식의 단일 매개 변수를 사용 하 여 대리자를 사용 합니다. 대리자 내의 모든 구성을 수행 합니다.

익명 대리자를 사용 하는 예제는 다음과 같습니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

Visual Studio 2017에서는 **새 ASP.NET 프로젝트** 대화 상자에서 "web API"를 선택 하면 "ASP.NET 웹 응용 프로그램" 프로젝트 템플릿이 자동으로 구성 코드를 설정 합니다.

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

프로젝트 템플릿은 앱\_시작 폴더 내에 WebApiConfig.cs 라는 파일을 만듭니다. 이 코드 파일은 웹 API 구성 코드를 저장 해야 하는 대리자를 정의 합니다.

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

또한 프로젝트 템플릿은 응용 프로그램에서 대리자를 호출 하는 코드를 **시작\_** 추가 합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>OWIN 자체 호스팅을 사용 하 여 Web API 구성

OWIN를 사용 하 여 자체 호스트 하는 경우 새 **Httpconfiguration** 인스턴스를 만듭니다. 이 인스턴스에서 구성을 수행 하 고 인스턴스를 **Owin. UseWebApi** 확장 메서드로 전달 합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

[OWIN를 사용 하 여 자체 호스트 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) 에서 전체 단계를 보여 줍니다.

<a id="services"></a>
## <a name="global-web-api-services"></a>전역 웹 API 서비스

**Httpconfiguration. Services** 컬렉션에는 Web API가 컨트롤러 선택 및 콘텐츠 협상과 같은 다양 한 작업을 수행 하는 데 사용 하는 글로벌 서비스 집합이 포함 되어 있습니다.

> [!NOTE]
> 서비스 **컬렉션은** 서비스 검색 또는 종속성 주입에 대 한 일반적인 용도의 메커니즘이 아닙니다. 웹 API 프레임 워크에 알려진 서비스 유형만 저장 합니다.

**서비스** 컬렉션은 기본 서비스 집합을 사용 하 여 초기화 되며, 사용자 지정 구현을 제공할 수 있습니다. 일부 서비스는 여러 인스턴스를 지원 하지만 다른 서비스는 하나의 인스턴스만 가질 수 있습니다. 그러나 컨트롤러 수준에서 서비스를 제공할 수도 있습니다. [컨트롤러 단위 구성](#percontrollerconfig)을 참조 하세요.

단일 인스턴스 서비스

| 서비스 | Description |
| --- | --- |
| **IActionValueBinder** | 매개 변수에 대 한 바인딩을 가져옵니다. |
| **IApiExplorer** | 응용 프로그램에서 노출 하는 Api에 대 한 설명을 가져옵니다. [웹 API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요. |
| **IAssembliesResolver** | 응용 프로그램에 대 한 어셈블리의 목록을 가져옵니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **IBodyModelValidator** | 미디어 형식 포맷터에 의해 요청 본문에서 읽은 모델의 유효성을 검사 합니다. |
| **IContentNegotiator** | 콘텐츠 협상을 수행합니다. |
| **IDocumentationProvider** | Api에 대 한 설명서를 제공 합니다. 기본값은 **null**입니다. [웹 API에 대 한 도움말 페이지 만들기](../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요. |
| **IHostBufferPolicySelector** | 호스트가 HTTP 메시지 엔터티 본문을 버퍼링 해야 하는지 여부를 나타냅니다. |
| **IHttpActionInvoker** | 컨트롤러 동작을 호출 합니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **IHttpActionSelector** | 컨트롤러 작업을 선택 합니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **IHttpControllerActivator** | 컨트롤러를 활성화 합니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **IHttpControllerSelector** | 컨트롤러를 선택 합니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **IHttpControllerTypeResolver** | 응용 프로그램의 Web API 컨트롤러 형식 목록을 제공 합니다. [라우팅 및 작업 선택을](../web-api-routing-and-actions/routing-and-action-selection.md)참조 하세요. |
| **ITraceManager** | 추적 프레임 워크를 초기화 합니다. [ASP.NET Web API 추적을](../testing-and-debugging/tracing-in-aspnet-web-api.md)참조 하세요. |
| **ITraceWriter** | 추적 작성기를 제공 합니다. 기본값은 "no op" 추적 기록기입니다. [ASP.NET Web API 추적을](../testing-and-debugging/tracing-in-aspnet-web-api.md)참조 하세요. |
| **IModelValidatorCache** | 모델 유효성 검사기의 캐시를 제공 합니다. |

여러 인스턴스 서비스

|                 서비스                 |                                                                                                              Description                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           컨트롤러 작업에 대 한 필터 목록을 반환 합니다.                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                지정 된 형식에 대 한 모델 바인더를 반환 합니다.                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     모델에 대 한 메타 데이터를 제공 합니다.                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   모델에 대 한 유효성 검사기를 제공 합니다.                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | 값 공급자를 만듭니다. 자세한 내용은 Mike 정지의 블로그 게시물 [WebAPI에서 사용자 지정 값 공급자를 만드는 방법](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) 을 참조 하세요. |

다중 인스턴스 서비스에 사용자 지정 구현을 추가 하려면 **서비스** 컬렉션에서 **add** 또는 **Insert** 를 호출 합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

단일 인스턴스 서비스를 사용자 지정 구현으로 바꾸려면 **서비스** 컬렉션에서 **replace** 를 호출 합니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>컨트롤러 단위 구성

컨트롤러 별로 다음 설정을 재정의할 수 있습니다.

- 미디어 유형 포맷터
- 매개 변수 바인딩 규칙
- Services

이렇게 하려면 **IControllerConfiguration** 인터페이스를 구현 하는 사용자 지정 특성을 정의 합니다. 그런 다음 컨트롤러에 특성을 적용 합니다.

다음 예에서는 기본 미디어 유형 포맷터를 사용자 지정 포맷터로 바꿉니다.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**IControllerConfiguration** 메서드는 두 개의 매개 변수를 사용 합니다.

- **Httpcontrollersettings** 개체
- **Httpcontrollerdescriptor** 개체

**Httpcontrollerdescriptor** 에는 컨트롤러에 대 한 설명이 포함 되어 있으며,이를 통해 정보를 확인할 수 있습니다 (예를 들어 두 컨트롤러를 구분 하는).

**Httpcontrollersettings** 개체를 사용 하 여 컨트롤러를 구성 합니다. 이 개체에는 컨트롤러 단위로 재정의할 수 있는 구성 매개 변수의 하위 집합이 포함 되어 있습니다. 변경 하지 않는 설정은 기본적으로 전역 **Httpconfiguration** 개체로 설정 됩니다.
