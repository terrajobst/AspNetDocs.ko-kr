---
uid: web-api/samples-list
title: Web API 샘플 목록-ASP.NET 4.x
author: rick-anderson
description: ASP.NET 4.x의 ASP.NET Web API 샘플 목록
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484265"
---
# <a name="web-api-samples-list"></a>Web API 샘플 목록

## <a name="httpclient-samples"></a>HttpClient 샘플

**Bing 번역 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

**Httpclient** 클래스를 사용 하 여 [Microsoft Translator 서비스](https://msdn.microsoft.com/library/ff512419.aspx) 를 호출 하는 방법을 보여 줍니다. Microsoft Translator 서비스 API에는 응용 프로그램에서 변환기 서비스에 대 한 각 요청에 대해 Azure 토큰 서버에 요청을 전송 하 여 가져오는 OAuth 토큰이 필요 합니다. 토큰 서버의 결과가 번역 서비스로 전송 된 요청에 전달 됩니다. 이 샘플을 실행 하기 전에 [Azure Marketplace에서 응용 프로그램 키](https://msdn.microsoft.com/library/hh454950.aspx) 를 받아서 AccessTokenMessageHandler 샘플 클래스의 정보를 입력 해야 합니다.

**Google Maps 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

**Httpclient** 를 사용 하 여 [Google Maps API](https://developers.google.com/maps/)에서 Redmond의 지도를 다운로드 하 고, 로컬 파일로 저장 하 고, 기본 이미지 뷰어를 엽니다.

**Twitter 클라이언트 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

**Httpclient**를 사용 하 여 간단한 Twitter 클라이언트를 작성 하는 방법을 보여 줍니다. 이 샘플에서는 **Httpmessagehandler** 를 사용 하 여 발신 **HttpRequestMessage**에 OAuth 인증 정보를 삽입 합니다. Twitter의 결과는 JSON.NET을 사용 하 여 읽습니다. 이 샘플을 실행 하기 전에 [Twitter에서 응용 프로그램 키](https://dev.twitter.com/)를 가져오고 OAuthMessageHandler 샘플 클래스의 정보를 입력 해야 합니다.

**세계적인 은행 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [vs 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [vs 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

JSON.NET를 사용 하 여 결과를 구문 분석 하는 세계 은행 데이터 사이트에서 데이터를 검색 하는 방법을 보여 줍니다.

## <a name="web-api-samples"></a>Web API 샘플

**ASP.NET Web API** | [VS 2012 원본](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) 시작

HTTP GET 요청을 지 원하는 기본 web API를 만드는 방법을 보여 줍니다. [첫 번째 ASP.NET Web API](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)자습서에 대 한 소스 코드를 포함 합니다.

**ASP.NET Web API JavaScript 시나리오 – 주석** | [VS 2012 소스](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

ASP.NET Web API를 사용 하 여 브라우저 클라이언트를 지 원하는 웹 Api를 빌드하는 방법을 보여 줍니다. jQuery를 사용 하 여 쉽게 호출할 수 있습니다.

**Contact Manager** | [VS 2010 원본](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

이 샘플에서는 ASP.NET Web API를 사용 하 여 간단한 연락처 관리자 응용 프로그램을 빌드합니다. 응용 프로그램은 ASP.NET MVC 응용 프로그램에서 사용 하는 연락처 관리자 웹 API와 연락처 목록을 표시 하 고 관리 하는 Windows Phone 응용 프로그램으로 구성 됩니다.

**일괄 처리 샘플** | [자세한 설명](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

ASP.NET 내에서 HTTP 일괄 처리를 구현 하는 방법을 보여 줍니다. 일괄 처리는 단일 MIME 다중 파트 엔터티 본문 내에 여러 HTTP 요청을 배치 하는 것으로 구성 됩니다 .이 본문은 HTTP POST로 서버에 전송 됩니다. 요청은 개별적으로 처리 되 고 응답은 클라이언트에 반환 되는 다른 MIME 다중 파트 엔터티 본문에 배치 됩니다.

**콘텐츠 컨트롤러 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [vs 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

스트림을 사용 하 여 요청 및 응답 엔터티를 비동기적으로 읽고 쓰는 방법을 보여 줍니다. 샘플 컨트롤러에는 요청 엔터티 본문을 비동기적으로 읽어 로컬 파일에 저장 하는 PUT 작업과 로컬 파일의 콘텐츠를 반환 하는 GET 작업이 있습니다.

**사용자 지정 어셈블리 확인 프로그램 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

동적으로 로드 된 라이브러리 어셈블리에서 컨트롤러 검색을 지원 하도록 ASP.NET Web API를 수정 하는 방법을 보여 줍니다. 이 샘플에서는 기본 구현을 호출 하는 사용자 지정 **IAssembliesResolver** 을 구현 하 고 기본 결과에 라이브러리 어셈블리를 추가 합니다.

**사용자 지정 미디어 유형 포맷터 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

**BufferedMediaTypeFormatter** 기본 클래스를 사용 하 여 사용자 지정 미디어 유형 포맷터를 만드는 방법을 보여 줍니다. 이 기본 클래스는 주로 동기식 읽기 및 쓰기 작업을 사용 하는 포맷터를 위한 것입니다. 미디어 유형 포맷터를 표시 하는 것 외에도 샘플은 응용 프로그램에 대 한 **Httpconfiguration** 의 일부로 등록 하 여 후크 하는 방법을 보여 줍니다. 주로 비동기 읽기 및 쓰기 작업을 사용 하는 포맷터에 대해 **MediaTypeFormatter** 기본 클래스를 직접 사용할 수 있습니다.

**사용자 지정 매개 변수 바인딩 샘플** | [자세한 설명](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

요청의 정보를 작업 매개 변수에 바인딩하는 방법을 결정 하는 프로세스 인 매개 변수 바인딩 프로세스를 사용자 지정 하는 방법을 보여 줍니다. 이 샘플에서 홈 컨트롤러에는 네 가지 작업이 있습니다.

1. BindPrincipal은 HTTP GET 메시지가 아닌 사용자 지정 일반 보안 주체에서 IPrincipal 매개 변수를 바인딩하는 방법을 보여 줍니다.
2. BindCustomComplexTypeFromUriOrBody는 복합 형식 매개 변수를 바인딩하는 방법을 보여 줍니다 .이 매개 변수는 메시지 본문 또는 HTTP POST 메시지의 요청 URI에서 가져올 수 있습니다.
3. BindCustomComplexTypeFromUriWithRenamedProperty는 HTTP POST 메시지의 요청 URI에서 제공 되는 이름이 바뀐 속성을 사용 하 여 복합 형식 매개 변수를 바인딩하는 방법을 보여 줍니다.
4. PostMultipleParametersFromBody는 게시 메시지에 대 한 본문에서 여러 매개 변수를 바인딩하는 방법을 보여 줍니다.

**파일 업로드 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

MIME 다중 파트 파일 업로드를 사용 하 여 **ApiController** 에 파일을 업로드 하는 방법 및 **ProgressNotificationHandler**를 사용 하 여 **httpclient** 를 사용 하 여 진행률 알림을 설정 하는 방법을 보여 줍니다. 컨트롤러는 HTML 파일 업로드 내용을 비동기적으로 읽어 로컬 파일에 하나 이상의 본문 부분을 씁니다. 응답에는 업로드 된 파일 (또는 파일)에 대 한 정보가 포함 되어 있습니다.

**Azure Blob 저장소에 파일 업로드 샘플** | [자세한 설명](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

이 샘플은 파일 업로드 샘플과 유사 하지만 업로드 된 파일을 로컬 디스크에 저장 하는 대신 [Windows AZURE SDK for .net](https://www.windowsazure.com/develop/net/)을 사용 하 여 파일을 [Azure Blob 저장소](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) 에 비동기적으로 업로드 합니다. 또한 현재 [Azure Blob Storage 컨테이너](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)에 있는 blob을 나열 하는 메커니즘도 제공 합니다. Azure SDK와 함께 제공 되는 **Azure Storage 에뮬레이터** 에 대해 실행 되는 샘플을 사용해 볼 수 있습니다. [Azure Storage 계정이](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)있는 경우 실제 저장소 서비스에 대해서도 실행할 수 있습니다.

**Http 메시지 처리기 파이프라인 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

클라이언트 (**httpclient**)와 서버 (ASP.NET Web API) 모두에서 **httpmessagehandler** 인스턴스를 연결 하는 방법을 보여 줍니다. 이 샘플에서는 클라이언트와 서버 모두에서 동일한 처리기를 사용 합니다. 두 위치에서 정확히 동일한 처리기가 실행 되는 것은 아니지만 개체 모델은 클라이언트 및 서버 쪽에서 동일 합니다.

**JSON 업로드 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

**ApiController**에서 JSON을 업로드 하 고 다운로드 하는 방법을 보여 줍니다. 이 샘플에서는 최소 **ApiController** 를 사용 하 고 **httpclient**를 사용 하 여 액세스 합니다.

**매시업 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

**ApiController** 작업 내에서 여러 원격 사이트에 비동기적으로 액세스 하는 방법을 보여 줍니다. 동작이 적중 될 때마다 요청은 비동기적으로 수행 되므로 스레드가 차단 되지 않습니다.

**메모리 추적 샘플** | [자세한 설명](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

이 샘플 프로젝트는 ASP.NET Web API 응용 프로그램에 사용자 지정 메모리 내 추적 작성기를 설치 하는 Nuget 패키지를 만듭니다.

**MongoDB 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

리포지토리 패턴을 사용 하 여 MongoDB을 **ApiController**에 대 한 영구 저장소로 사용 하는 방법을 보여 줍니다.

**응답 본문 프로세서 샘플** | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

클라이언트에 전송 되기 전에 응답 엔터티 (즉, HTTP 응답 본문)를 로컬 파일에 복사 하 고 해당 파일에서 비동기적으로 추가 처리를 수행 하는 방법을 보여 줍니다. 이 샘플은 응답 엔터티를 사용 하 여 응답 엔터티를 래핑하는 **Httpmessagehandler** 를 구현 합니다.

**XDocument 샘플 업로드** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [VS 2012 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample)

**Pushstreamcontent** 및 **httpclient**를 사용 하 여 **ApiController** 에 XDocument를 업로드 하는 방법을 보여 줍니다.

**유효성 검사 샘플** | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

ASP.NET WebAPI에서 모델에 대 한 유효성 검사 특성을 사용 하 여 HTTP 요청 내용의 유효성을 검사 하는 방법을 보여 줍니다. 필요에 따라 속성을 표시 하는 방법, 프레임 워크 정의 및 사용자 지정 유효성 검사 특성을 사용 하 여 모델에 주석을 추가 하는 방법 및 잘못 된 모델 상태에 대 한 오류 응답을 반환 하는 방법을 보여 줍니다.

**Web Form 샘플** | [자세한 설명](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [VS 2010 원본](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

Web Forms 프로젝트에 추가 된 ApiController를 표시 합니다.

**[RestBugs 샘플](https://github.com/howarddierking/RestBugs)**

RestBugs는 ASP.NET Web API 및 새 HTTP 클라이언트 라이브러리를 사용 하 여 하이퍼 미디어 기반 시스템을 만드는 방법을 보여 주는 간단한 버그 추적 응용 프로그램입니다. 이 샘플에는 ASP.NET Web API를 사용 하 여 클라이언트 및 서버 구현이 모두 포함 되어 있습니다. 서버는 사용자 지정 Razor 포맷터를 사용 하 여 리소스 표현을 생성 합니다. 이 샘플은 또한 하이퍼 미디어 디자인을 사용 하 여 클라이언트와 서버를 분리 하는 이점을 보여 주는 node.js 서버를 제공 합니다.
