---
title: Razor 구성 요소 호스팅 모델
author: guardrex
description: 클라이언트 쪽 Blazor 및 서버 쪽 ASP.NET Core Razor 구성 요소 호스팅 모델을 이해 합니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042440"
---
# <a name="razor-components-hosting-models"></a>Razor 구성 요소 호스팅 모델

[Daniel Roth](https://github.com/danroth27)

Razor 구성 요소는 클라이언트 쪽에서 실행 하도록 설계 하는 웹 프레임 워크, WebAssembly 기반.NET 런타임 브라우저에서 (*Blazor*) 또는 ASP.NET Core에서 서버 쪽 (*ASP.NET Core Razor 구성 요소가*). 호스팅 모델, 앱 및 구성 요소 모델에 관계 없이 *동일 하 게 유지*합니다. 이 문서에서는 사용 가능한 호스팅 모델을 설명 합니다.

## <a name="client-side-hosting-model"></a>클라이언트 쪽 호스팅 모델

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Blazor의 주 호스팅 모델은 브라우저에서 실행 중인 클라이언트 쪽입니다. 이 모델에서는 Blazor 앱, 종속성 및.NET 런타임 브라우저 다운로드 됩니다. 해당 앱은 브라우저 UI 스레드에서 직접 실행됩니다. 모든 UI 업데이트 및 이벤트 처리에는 동일한 프로세스 내에서 발생 합니다. 정적 파일을 사용 하 여 모든 웹 서버 기본 설정으로 앱 자산을 배포할 수 있습니다 (참조 [호스트 및 배포](xref:host-and-deploy/razor-components/index)).

![Blazor 클라이언트 측: Blazor 앱 브라우저 내에서 UI 스레드에서 실행 됩니다.](hosting-models/_static/client-side.png)

클라이언트 쪽 호스팅 모델을 사용 하 여 Blazor 앱을 만들려면 사용 합니다 **Blazor** 또는 **Blazor (ASP.NET Core 호스팅)** 프로젝트 템플릿 (`blazor` 또는 `blazorhosted` 를사용하는경우서식파일[새 dotnet](/dotnet/core/tools/dotnet-new) 명령 프롬프트에서 명령을). 포함 된 *blazor.webassembly.js* 핸들 스크립트:

* .NET 런타임, 앱 및 해당 종속성을 다운로드 합니다.
* 앱을 실행 하려면 런타임 초기화 합니다.

클라이언트 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다. 클라이언트 쪽 Blazor:

* .NET 서버 쪽 종속성을 있습니다.
* 풍부한 대화형 UI에 있습니다.
* 클라이언트 리소스 및 기능을 최대한 활용합니다.
* 오프 로드 서버에서 클라이언트로 작동 합니다.
* 오프 라인 시나리오를 지원합니다.

클라이언트 쪽 호스팅에 단점이 있습니다. 클라이언트 쪽 Blazor:

* 브라우저의 기능으로 앱을 제한합니다.
* 지원 되는 클라이언트 하드웨어 및 소프트웨어 (예를 들어, WebAssembly 지원)에 필요합니다.
* 로드 시간 더 오래 앱을 더 큰 다운로드 크기에 있습니다.
* .NET 런타임 및 도구 지원 (예를 들어,.NET Standard 지원과 디버깅의 제한) 성숙 적습니다.

Visual Studio에 포함 된 **Blazor (호스팅되는 ASP.NET Core)** WebAssembly에서 실행 되는 ASP.NET Core 서버에서 호스팅되는 Blazor 앱을 만들기 위한 프로젝트 템플릿. ASP.NET Core 앱 클라이언트로 Blazor 앱 역할 이지만 그렇지 않은 경우 별도 프로세스. 클라이언트 쪽 Blazor 앱 웹 API 호출 또는 SignalR 연결을 사용 하 여 네트워크를 통해 서버를 조작할 수 있습니다.

> [!IMPORTANT]
> 클라이언트 쪽 Blazor 앱을 IIS 하위 기능 앱으로 호스팅되는 ASP.NET Core 앱에서 제공 하는 경우 상속된 된 ASP.NET Core 모듈 처리기 사용 하지 않도록 설정 합니다. Blazor 앱의 앱 기본 경로 설정 *index.html* IIS에서 하위 앱을 구성할 때 사용 하는 IIS 별칭에는 파일입니다.
>
> 자세한 내용은 [앱 기본 경로](xref:host-and-deploy/razor-components/index#app-base-path)합니다.

## <a name="server-side-hosting-model"></a>서버 쪽 호스팅 모델

ASP.NET Core Razor 구성 요소 서버 쪽 호스팅 모델에서는 응용 프로그램 서버에서 ASP.NET Core 앱 내에서 실행 됩니다. UI 업데이트, 이벤트 처리 및 JavaScript 호출은 SignalR 연결상에서 처리됩니다.

![ASP.NET Core Razor 구성 요소 서버 측: 브라우저와 상호 작용 (ASP.NET Core 앱 내에서 호스팅) 앱 서버에서 SignalR 연결을 통해.](hosting-models/_static/server-side.png)

서버 쪽 호스팅 모델을 사용 하는 구성 요소 Razor 앱을 만들려면 사용 합니다 **Blazor (서버 쪽 ASP.NET Core에서)** 템플릿 (`blazorserver` 사용 하는 경우 [새 dotnet](/dotnet/core/tools/dotnet-new) 명령 프롬프트에서). ASP.NET Core 앱을 Razor 구성 요소 서버 쪽 앱을 호스트 및 클라이언트가 연결 된 SignalR 끝점을 설정 합니다. 앱의를 참조 하는 ASP.NET Core 앱 `Startup` 추가할 클래스:

* 서버 쪽 구성 요소 Razor 서비스입니다.
* 요청 처리 파이프라인에 대 한 앱입니다.

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

합니다 *blazor.server.js* 스크립트&dagger; 클라이언트 연결을 설정 합니다. 것은 앱의 책임 (예를 들어 네트워크 연결이) 발생할 경우 필요에 따라 앱 상태를 유지 및 복원입니다.

서버 쪽 호스팅 모델에는 몇 가지 이점을 제공합니다.

* .NET을 사용 하 여 전체 응용 프로그램을 작성할 수 있습니다 하 고 C# 구성 요소 모델을 사용 합니다.
* 불필요 한 페이지 새로 고침을 방지 및 풍부한 대화형 느낌을 제공 합니다.
* 클라이언트 쪽 Blazor 앱과 앱 크기가 매우 작아 졌습니다 및 훨씬 빠르게 로드 합니다.
* 구성 요소 논리는 모든.NET Core 호환 되는 Api를 사용 하는 등 서버 기능의 활용을 걸릴 수 있습니다.
* 도구, 디버깅와 같은 기존.NET 예상 대로 작동 하므로.NET Core에 서버에서 실행 됩니다.
* 씬 클라이언트와 함께 (예: 브라우저 WebAssembly 및 리소스를 지원 하지 않는 제한 된 장치).

서버 쪽 호스팅에 단점이 있습니다.

* 더 높은 대기 시간에 있습니다. 모든 사용자 상호 작용을 네트워크 홉이 됩니다.
* 오프 라인 지원 되지 않습니다는 제공합니다. 클라이언트 연결에 실패 하면 앱 작동이 중지 됩니다.
* 확장성을 감소 되었습니다. 서버는 여러 클라이언트 연결을 관리 하 고 클라이언트 상태를 처리 해야 합니다.
* 앱을 제공 하는 ASP.NET Core 서버가 필요 합니다. (예: CDN)에서 서버 없이 배포 할 수 없습니다.

&dagger;합니다 *blazor.server.js* 스크립트는 다음 경로에 게시 됩니다. *bin / {디버그 | 릴리스} / {대상 프레임 워크} /publish/ {응용 프로그램 이름}. 앱/배포/_framework*합니다.
