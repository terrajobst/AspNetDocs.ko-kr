---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 셀프 호스트 ASP.NET Web API 1 (C#)-ASP.NET 4.x
author: MikeWasson
description: 코드를 사용한 자습서 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421373"
---
# <a name="self-host-aspnet-web-api-1-c"></a>셀프 호스트 ASP.NET Web API 1 (C#)

[Mike Wasson](https://github.com/MikeWasson)

> 이 자습서에서는 콘솔 응용 프로그램 내에서 web API를 호스트 하는 방법을 보여 줍니다. ASP.NET Web API에는 IIS가 필요 하지 않습니다. 자체 호스트 프로세스에서 web API를 자체 호스트할 수 있습니다. 
> 
> **새 응용 프로그램은 OWIN를 사용 하 여 웹 API를 자체 호스트 해야 합니다.** [OWIN를 사용 하 여 자체 호스트 ASP.NET Web API 2를](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)참조 하세요.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>콘솔 응용 프로그램 프로젝트 만들기

Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **Windows**를 선택 합니다. 프로젝트 템플릿 목록에서 **콘솔 응용 프로그램**을 선택 합니다. 프로젝트 이름을 SelfHost&quot;로 &quot;하 고 **확인**을 클릭 합니다.

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>대상 프레임 워크 설정 (Visual Studio 2010)

Visual Studio 2010을 사용 하는 경우 대상 프레임 워크를 .NET Framework 4.0로 변경 합니다. 기본적으로 프로젝트 템플릿은 [.Net Framework 클라이언트 프로필](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)을 대상으로 합니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **대상 프레임 워크** 드롭다운 목록에서 대상 프레임 워크를 .NET Framework 4.0로 변경 합니다. 변경 내용을 적용 하 라는 메시지가 표시 되 면 **예**를 클릭 합니다.

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>NuGet 패키지 관리자 설치

NuGet 패키지 관리자는 non-ASP.NET 프로젝트에 웹 API 어셈블리를 추가 하는 가장 쉬운 방법입니다.

NuGet 패키지 관리자가 설치 되어 있는지 확인 하려면 Visual Studio에서 **도구** 메뉴를 클릭 합니다. **Nuget 패키지 관리자**라는 메뉴 항목이 표시 되 면 Nuget 패키지 관리자가 있는 것입니다.

NuGet 패키지 관리자를 설치 하려면:

1. Visual Studio를 시작합니다.
2. **도구** 메뉴에서 **확장 및 업데이트**를 선택합니다.
3. **확장 및 업데이트** 대화 상자에서 **온라인**을 선택 합니다.
4. "NuGet 패키지 관리자"가 표시 되지 않으면 검색 상자에 "nuget 패키지 관리자"를 입력 합니다.
5. NuGet 패키지 관리자를 선택 하 고 **다운로드**를 클릭 합니다.
6. 다운로드가 완료 되 면을 설치 하 라는 메시지가 표시 됩니다.
7. 설치가 완료 되 면 Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>Web API NuGet 패키지 추가

NuGet 패키지 관리자를 설치한 후 프로젝트에 웹 API 자체 호스트 패키지를 추가 합니다.

1. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다. *참고*:이 메뉴 항목이 표시 되지 않으면 NuGet 패키지 관리자가 올바르게 설치 되었는지 확인 합니다.
2. **솔루션용 NuGet 패키지 관리를 선택 합니다** .
3. **NugGet 패키지 관리** 대화 상자에서 **온라인**을 선택 합니다.
4. 검색 상자에 &quot;WebApi. SelfHost&quot;를 입력 합니다.
5. ASP.NET Web API 셀프 호스트 패키지를 선택 하 고 **설치**를 클릭 합니다.
6. 패키지가 설치 된 후 **닫기** 를 클릭 하 여 대화 상자를 닫습니다.

> [!NOTE]
> AspNetWebApi가 아닌 SelfHost 라는 패키지를 설치 해야 합니다. WebApi.

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>모델 및 컨트롤러 만들기

이 자습서에서는 [시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다.

`Product`이라는 public 클래스를 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

`ProductsController`이라는 public 클래스를 추가 합니다. **ApiController**에서이 클래스를 파생 시킵니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

이 컨트롤러의 코드에 대 한 자세한 내용은 [초보자](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 를 위한 자습서를 참조 하세요. 이 컨트롤러는 다음과 같은 세 가지 GET 작업을 정의 합니다.

| URI | Description |
| --- | --- |
| /api/제품 | 모든 제품의 목록을 가져옵니다. |
| /api/products/*id* | ID로 제품을 가져옵니다. |
| /api/products/? category =*category* | 범주별로 제품 목록을 가져옵니다. |

## <a name="host-the-web-api"></a>Web API 호스트

Program.cs 파일을 열고 다음 using 문을 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

**Program** 클래스에 다음 코드를 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>필드 HTTP URL 네임 스페이스 예약 추가

이 응용 프로그램은 `http://localhost:8080/`를 수신 대기 합니다. 기본적으로 특정 HTTP 주소를 수신 하려면 관리자 권한이 필요 합니다. 따라서 자습서를 실행할 때이 오류가 발생할 수 있습니다. "HTTP에서 URL http://+:8080/등록할 수 없습니다." 라는 두 가지 방법으로이 오류를 방지할 수 있습니다.

- 관리자 권한으로 Visual Studio를 실행 하거나
- Netsh.exe를 사용 하 여 계정에 URL을 예약할 수 있는 권한을 부여 합니다.

Netsh.exe를 사용 하려면 관리자 권한으로 명령 프롬프트를 열고 다음 명령을 입력 합니다. 명령을 입력 합니다.

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

여기서 *machine\username* 는 사용자 계정입니다.

자체 호스팅을 완료 한 후에는 예약을 삭제 해야 합니다.

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>클라이언트 응용 프로그램에서 Web API 호출 (C#)

Web API를 호출 하는 간단한 콘솔 응용 프로그램을 작성해 보겠습니다.

새 콘솔 응용 프로그램 프로젝트를 솔루션에 추가 합니다.

- 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **새 프로젝트 추가**를 선택 합니다.
- &quot;ClientApp&quot;라는 새 콘솔 응용 프로그램을 만듭니다.

![](self-host-a-web-api/_static/image5.png)

NuGet 패키지 관리자를 사용 하 여 ASP.NET Web API Core 라이브러리 패키지를 추가 합니다.

- 도구 메뉴에서 **NuGet 패키지 관리자**를 선택 합니다.
- **솔루션용 NuGet 패키지 관리를 선택 합니다** .
- **NuGet 패키지 관리** 대화 상자에서 **온라인**을 선택 합니다.
- 검색 상자에 &quot;WebApi&quot;을 입력 합니다.
- Microsoft ASP.NET Web API 클라이언트 라이브러리 패키지를 선택 하 고 **설치**를 클릭 합니다.

SelfHost 프로젝트에 ClientApp에 대 한 참조를 추가 합니다.

- 솔루션 탐색기에서 ClientApp 프로젝트를 마우스 오른쪽 단추로 클릭 합니다.
- **참조 추가**를 선택합니다.
- **참조 관리자** 대화 상자의 **솔루션**에서 **프로젝트**를 선택 합니다.
- SelfHost 프로젝트를 선택 합니다.
- **확인**을 클릭합니다.

![](self-host-a-web-api/_static/image6.png)

클라이언트/프로그램 .cs 파일을 엽니다. 다음 **using** 문을 추가합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

정적 **Httpclient** 인스턴스를 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

모든 제품을 나열 하 고, ID로 제품을 나열 하 고, 범주별로 제품을 나열 하려면 다음 메서드를 추가 합니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

이러한 각 메서드는 같은 패턴을 따릅니다.

1. **Httpclient. GetAsync** 를 호출 하 여 GET 요청을 적절 한 URI로 보냅니다.
2. **HttpResponseMessage. EnsureSuccessStatusCode**를 호출 합니다. HTTP 응답 상태가 오류 코드 인 경우이 메서드는 예외를 throw 합니다.
3. **Readasasync&lt;t&gt;** 를 호출 하 여 HTTP 응답에서 CLR 형식을 deserialize 합니다. 이 메서드는 **시스템 .net. Http. HttpContentExtensions**에 정의 된 확장 메서드입니다.

**Getasync** 및 **readasasync** 메서드는 모두 비동기 메서드입니다. 비동기 작업을 나타내는 **작업** 개체를 반환 합니다. **Result** 속성을 가져오면 작업이 완료 될 때까지 스레드가 차단 됩니다.

비차단 호출을 수행 하는 방법을 비롯 하 여 HttpClient를 사용 하는 방법에 대 한 자세한 내용은 [.Net 클라이언트에서 WEB API 호출](../advanced/calling-a-web-api-from-a-net-client.md)을 참조 하십시오.

이러한 메서드를 호출 하기 전에 HttpClient 인스턴스의 BaseAddress 속성을 "`http://localhost:8080`"로 설정 합니다. 다음은 그 예입니다.

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

그러면 다음과 같이 출력 됩니다. SelfHost 응용 프로그램을 먼저 실행 해야 합니다.

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
