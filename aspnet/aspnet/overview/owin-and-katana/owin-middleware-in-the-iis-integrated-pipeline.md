---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: IIS 통합 파이프라인에서 미들웨어 OWIN | Microsoft Docs
author: Praburaj
description: 이 문서에서는 IIS 통합 파이프라인에서 OMCs (OWIN 미들웨어 구성 요소)를 실행 하는 방법과 OMCS가 실행 되는 파이프라인 이벤트를 설정 하는 방법을 보여 줍니다. ...
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456714"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS 통합 파이프라인에서 미들웨어 OWIN

[Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 문서에서는 IIS 통합 파이프라인에서 OMCs (OWIN 미들웨어 구성 요소)를 실행 하는 방법과 OMCS가 실행 되는 파이프라인 이벤트를 설정 하는 방법을 보여 줍니다. 이 자습서를 읽기 전에 Project Katana 및 [OWIN Startup 클래스 검색](owin-startup-class-detection.md) [의 개요](an-overview-of-project-katana.md) 를 검토 해야 합니다. 이 자습서는 Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Chris Ross, Praburaj Thiagarajan 및 Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) )에 의해 작성 되었습니다.

OMCs ( [OWIN](an-overview-of-project-katana.md) 미들웨어 구성 요소)는 주로 서버 독립적 파이프라인에서 실행 되도록 설계 되었지만 IIS 통합 파이프라인 에서도 omcs를 실행할 수 있습니다 (**클래식 모드는 지원 *되지 않음*** ). PMC (패키지 관리자 콘솔)에서 다음 패키지를 설치 하 여 IIS 통합 파이프라인에서 OMC를 수행할 수 있습니다.

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

즉, IIS 및 System.web 외부에서 아직 실행할 수 없는 응용 프로그램 프레임 워크를 비롯 한 모든 응용 프로그램 프레임 워크는 기존 OWIN 미들웨어 구성 요소를 활용할 수 있습니다. 

> [!NOTE]
> Visual Studio 2013에서 새 Id 시스템으로 전달 되는 모든 `Microsoft.Owin.Security.*` 패키지 (예: 쿠키, Microsoft 계정, Google, Facebook, Twitter, [전달자 토큰](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, 권한 부여 서버, JWT, Azure active Directory 및 Active directory federation services)가 omcs로 작성 되 고 자체 호스팅 및 IIS에서 호스팅되는 시나리오에서 모두 사용할 수 있습니다.

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>IIS 통합 파이프라인에서 OWIN 미들웨어를 실행 하는 방법

OWIN 콘솔 응용 프로그램의 경우 [시작 구성을](owin-startup-class-detection.md) 사용 하 여 작성 된 응용 프로그램 파이프라인은 `IAppBuilder.Use` 메서드를 사용 하 여 구성 요소를 추가 하는 순서에 따라 설정 됩니다. 즉, [Katana](an-overview-of-project-katana.md) 런타임의 OWIN 파이프라인은 `IAppBuilder.Use`를 사용 하 여 등록 된 순서로 omcs를 처리 합니다. IIS 통합 파이프라인에서 요청 파이프라인은 [BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)등과 같은 파이프라인 이벤트의 미리 정의 된 집합을 구독 하는 [HttpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) 로 구성 됩니다.

OMC를 ASP.NET 세계의 [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) 과 비교 하는 경우 omc를 올바른 미리 정의 된 파이프라인 이벤트에 등록 해야 합니다. 예를 들어, 요청을 파이프라인의 [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) 단계로 가져올 때 HttpModule `MyModule` 호출 됩니다.

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

OMC가 이와 동일한 이벤트 기반 실행 순서에 참여 하도록 하기 위해 [Katana](an-overview-of-project-katana.md) 런타임 코드는 [시작 구성을](owin-startup-class-detection.md) 검색 하 고 각 미들웨어 구성 요소를 통합 파이프라인 이벤트에 등록 합니다. 예를 들어 다음 OMC 및 등록 코드를 사용 하 여 미들웨어 구성 요소의 기본 이벤트 등록을 확인할 수 있습니다. OWIN 시작 클래스를 만드는 방법에 대 한 자세한 내용은 [OWIN Startup 클래스 검색](owin-startup-class-detection.md)을 참조 하세요.

1. 빈 웹 응용 프로그램 프로젝트를 만들고 이름을 **owin2**로 만듭니다.
2. 패키지 관리자 콘솔 (PMC)에서 다음 명령을 실행 합니다. 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. `OWIN Startup Class`를 추가 하 고 이름을 `Startup`로 이름을 추가 합니다. 생성 된 코드를 다음으로 바꿉니다 (변경 내용이 강조 표시 됨).  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. F5 키를 눌러 앱을 실행 합니다.

시작 구성은 세 가지 미들웨어 구성 요소를 사용 하 여 파이프라인을 설정 하 고 처음 두 개는 진단 정보를 표시 하 고 마지막에는 이벤트에 응답 하 고 진단 정보를 표시 합니다. `PrintCurrentIntegratedPipelineStage` 메서드는이 미들웨어가 호출 되는 통합 파이프라인 이벤트와 메시지를 표시 합니다. 출력 창에 다음이 표시 됩니다.

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Katana 런타임은 IIS 파이프라인 이벤트 [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)에 해당 하는, 기본적으로 각 OWIN 미들웨어 구성 요소를 [preexecuterto esthandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) 에 매핑합니다.

## <a name="stage-markers"></a>스테이지 표식

`IAppBuilder UseStageMarker()` 확장 메서드를 사용 하 여 특정 파이프라인 단계에서 OMCs를 실행 하도록 표시할 수 있습니다. 특정 단계에서 미들웨어 구성 요소 집합을 실행 하려면 등록 하는 동안 마지막 구성 요소가 설정 된 직후에 스테이지 표식을 삽입 합니다. 미들웨어를 실행 하 고 주문 구성 요소를 실행 해야 하는 파이프라인 단계에 대 한 규칙이 있습니다 (규칙은 자습서의 뒷부분에 설명 되어 있음). 아래와 같이 `Configuration` 코드에 `UseStageMarker` 메서드를 추가 합니다.

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` 호출은 이전에 등록 된 미들웨어 구성 요소 (이 경우 두 개의 진단 구성 요소)를 파이프라인의 인증 단계에서 실행 하도록 구성 합니다. 마지막 미들웨어 구성 요소 (진단 정보를 표시 하 고 요청에 응답)는 `ResolveCache` 단계 ( [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) 이벤트)에서 실행 됩니다.

F5 키를 눌러 앱을 실행 합니다. 출력 창에 다음이 표시 됩니다.

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>스테이지 표식 규칙

OMC (Owin 미들웨어 구성 요소)는 다음 OWIN 파이프라인 단계 이벤트에서 실행 되도록 구성할 수 있습니다.

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. 기본적으로 OMCs는 마지막 이벤트 (`PreHandlerExecute`)에서 실행 됩니다. 이 때문에 첫 번째 예제 코드는 "Preexecuterto Esthandler"로 표시 됩니다.
2. `app.UseStageMarker` 메서드를 사용 하 여 `PipelineStage` 열거형에 나열 된 OWIN 파이프라인의 모든 단계에서 이전에 실행 되도록 OMC를 등록할 수 있습니다.
3. OWIN 파이프라인과 IIS 파이프라인은 순서 대로 정렬 되므로 `app.UseStageMarker` 호출은 순서 대로 되어 있어야 합니다. 에 등록 된 마지막 이벤트 앞에 있는 이벤트에 이벤트 처리기를 설정 하 여 `app.UseStageMarker`수 없습니다. 예를 들어를 호출한 *후* :

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   `Authenticate` 또는 `PostAuthenticate`를 전달 하는 `app.UseStageMarker`에 대 한 호출은 적용 되지 않으며 예외가 throw 되지 않습니다. OMCs는 기본적으로 `PreHandlerExecute`된 최신 단계에서 실행 됩니다. 스테이지 마커는 이전에 실행 되도록 하는 데 사용 됩니다. 스테이지 표식을 순서 대로 지정 하면 이전 마커로 반올림 됩니다. 즉, 스테이지 마커를 추가 하는 것은 "단계 X 보다 나중에 실행"을 의미 합니다. OMC는 OWIN 파이프라인에 추가 된 가장 이른 스테이지 표식에서 실행 됩니다.
4. `app.UseStageMarker`에 대 한 가장 이른 호출 단계입니다. 예를 들어 이전 예제에서 `app.UseStageMarker` 호출의 순서를 전환 하는 경우 다음과 같습니다.

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   출력 창에 다음이 표시 됩니다. 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs는 `Authenticate` 이벤트에 마지막 OMCS가 등록 되어 있고 `Authenticate` 이벤트가 다른 모든 이벤트 앞에 있기 때문에 `AuthenticateRequest` 단계에서 실행 됩니다.
