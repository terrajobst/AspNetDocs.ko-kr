---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#)-ASP.NET 4.X를 시작 합니다.
author: MikeWasson
description: 코드를 사용 하는 자습서입니다. ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448553"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 (C#) 시작

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

이 자습서에서는 ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다.

HTTP는 웹 페이지를 처리 하기 위한 것이 아닙니다. HTTP는 서비스 및 데이터를 노출 하는 Api를 빌드하기 위한 강력한 플랫폼 이기도 합니다. HTTP는 단순 하 고 유연 하며 다양 한 장소에 있습니다. 거의 모든 플랫폼에서 HTTP 라이브러리를 사용할 수 있으므로 HTTP 서비스는 브라우저, 모바일 장치 및 기존 데스크톱 응용 프로그램을 비롯 한 광범위 한 클라이언트에 연결할 수 있습니다.

ASP.NET Web API은 .NET Framework을 기반으로 웹 Api를 빌드하기 위한 프레임 워크입니다. 

## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

이 자습서의 최신 버전은 [ASP.NET Core 및 Visual Studio For Windows를 사용 하 여 WEB API 만들기](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 를 참조 하세요.

## <a name="create-a-web-api-project"></a>웹 API 프로젝트 만들기

이 자습서에서는 ASP.NET Web API를 사용 하 여 제품 목록을 반환 하는 Web API를 만듭니다. 프런트 엔드 웹 페이지는 jQuery를 사용 하 여 결과를 표시 합니다.

![](tutorial-your-first-web-api/_static/image1.png)

Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 "ProductsApp"로 선택 하 고 **확인을**클릭 합니다.

![](tutorial-your-first-web-api/_static/image2.png)

**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다. &quot;에 대 한 &quot;폴더 및 핵심 참조 추가에서 **WEB API**를 선택 합니다. **확인**을 클릭합니다.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> &quot;Web API&quot; 템플릿을 사용 하 여 Web API 프로젝트를 만들 수도 있습니다. Web API 템플릿에서는 ASP.NET MVC를 사용 하 여 API 도움말 페이지를 제공 합니다. MVC 없이 Web API를 표시 하려고 하기 때문에이 자습서에 빈 템플릿을 사용 합니다. 일반적으로 Web API를 사용 하기 위해 ASP.NET MVC를 알 필요가 없습니다.

## <a name="adding-a-model"></a>모델 추가

*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다. JSON, XML 또는 다른 형식으로 모델을 자동으로 serialize 한 다음, serialize 된 데이터를 HTTP 응답 메시지의 본문에 쓸 ASP.NET Web API 있습니다. 클라이언트에서 serialization 형식을 읽을 수 있으면 개체를 deserialize 할 수 있습니다. 대부분의 클라이언트는 XML 또는 JSON을 구문 분석할 수 있습니다. 또한 클라이언트는 HTTP 요청 메시지의 Accept 헤더를 설정 하 여 원하는 형식을 나타낼 수 있습니다.

먼저 제품을 나타내는 간단한 모델을 만들어 보겠습니다.

솔루션 탐색기가 표시되지 않는 경우 **보기** 메뉴를 클릭하고 **솔루션 탐색기**를 선택합니다. 솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 **추가**를 선택한 다음 **클래스**를 선택합니다.

![](tutorial-your-first-web-api/_static/image4.png)

클래스 이름을 Product&quot;&quot;합니다. `Product` 클래스에 다음 속성을 추가 합니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>컨트롤러 추가

Web API에서 *컨트롤러*는 HTTP 요청을 처리하는 개체입니다. 제품의 목록이 나 ID로 지정 된 단일 제품을 반환할 수 있는 컨트롤러를 추가 합니다.

> [!NOTE]
> ASP.NET MVC를 사용한 경우 이미 컨트롤러에 대해 잘 알고 있는 것입니다. Web API 컨트롤러는 MVC 컨트롤러와 비슷하지만 **컨트롤러** 클래스 대신 **ApiController** 클래스를 상속 합니다.

**솔루션 탐색기**에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가**를 선택한 후 **컨트롤러**를 선택합니다.

![](tutorial-your-first-web-api/_static/image5.png)

**스캐폴드 추가** 대화 상자에서 **Web API 컨트롤러 - 비어 있음**을 선택합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image6.png)

**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다. **추가**를 클릭합니다.

![](tutorial-your-first-web-api/_static/image7.png)

스 캐 폴딩은 Controllers 폴더에 ProductsController.cs 라는 파일을 만듭니다.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> 컨트롤러를 컨트롤러 라는 폴더에 배치할 필요가 없습니다. 폴더 이름은 원본 파일을 구성 하는 편리한 방법일 뿐입니다.

이 파일이 열려 있지 않으면 파일을 두 번 클릭하여 엽니다. 이 파일의 코드를 다음으로 바꿉니다.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

예제를 간단 하 게 유지 하기 위해 제품은 컨트롤러 클래스 내부의 고정 배열에 저장 됩니다. 물론 실제 응용 프로그램에서는 데이터베이스를 쿼리하거나 다른 외부 데이터 원본을 사용할 수 있습니다.

컨트롤러는 제품을 반환 하는 두 가지 메서드를 정의 합니다.

- `GetAllProducts` 메서드는 전체 제품 목록을 **IEnumerable&lt;Product&gt;** 형식으로 반환 합니다.
- `GetProduct` 메서드는 해당 ID로 단일 제품을 조회 합니다.

이것으로 끝입니다. 웹 API가 작동 합니다. 컨트롤러의 각 메서드는 하나 이상의 Uri에 해당 합니다.

| Controller 메서드 | URI |
| --- | --- |
| GetAllProducts | /api/제품 |
| GetProduct | /api/products/*id* |

`GetProduct` 메서드의 경우 URI의 *id* 는 자리 표시자입니다. 예를 들어 ID가 5 인 제품을 가져오려면 URI가 `api/products/5`됩니다.

웹 API가 HTTP 요청을 컨트롤러 메서드로 라우팅하는 방법에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>Javascript 및 jQuery를 사용 하 여 Web API 호출

이 섹션에서는 AJAX를 사용 하 여 web API를 호출 하는 HTML 페이지를 추가 합니다. JQuery를 사용 하 여 AJAX를 호출 하 고 결과를 사용 하 여 페이지를 업데이트 합니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 합니다.

![](tutorial-your-first-web-api/_static/image9.png)

**새 항목 추가** 대화 상자에서 **C#시각적 개체**아래에 있는 **웹** 노드를 선택 하 고 **HTML 페이지** 항목을 선택 합니다. 페이지 이름을 index. html&quot;로 &quot;합니다.

![](tutorial-your-first-web-api/_static/image10.png)

이 파일의 모든 항목을 다음으로 바꿉니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

여러 가지 방법으로 jQuery를 가져올 수 있습니다. 이 예제에서는 [Microsoft AJAX CDN](../../../ajax/cdn/overview.md)을 사용 했습니다. 또한 [http://jquery.com/](http://jquery.com/)에서 다운로드할 수 있으며, ASP.NET "Web API" 프로젝트 템플릿에는 jQuery도 포함 됩니다.

### <a name="getting-a-list-of-products"></a>제품 목록 가져오기

제품 목록을 가져오려면 HTTP GET 요청을 &quot;/api/products&quot;보냅니다.

JQuery [Getjson](http://api.jquery.com/jQuery.getJSON/) 함수는 AJAX 요청을 보냅니다. For response에 JSON 개체의 배열이 포함 되어 있습니다. `done` 함수는 요청이 성공 하는 경우 호출 되는 콜백을 지정 합니다. 콜백에서 제품 정보를 사용 하 여 DOM을 업데이트 합니다.

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>ID로 제품 가져오기

ID로 제품을 가져오려면 HTTP GET 요청을 &quot;/api/products/*id*&quot;보냅니다. 여기서 *ID* 는 제품 id입니다.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

AJAX 요청을 보내기 위해 `getJSON`를 호출 하지만 이번에는 요청 URI에 ID를 넣습니다. 이 요청의 응답은 단일 제품의 JSON 표현입니다.

## <a name="running-the-application"></a>응용 프로그램 실행

F5 키를 눌러 애플리케이션 디버깅을 시작합니다. 웹 페이지는 다음과 같습니다.

![](tutorial-your-first-web-api/_static/image11.png)

ID로 제품을 가져오려면 ID를 입력 하 고 검색을 클릭 합니다.

![](tutorial-your-first-web-api/_static/image12.png)

잘못 된 ID를 입력 하면 서버에서 HTTP 오류가 반환 됩니다.

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>F12 키를 사용 하 여 HTTP 요청 및 응답 보기

HTTP 서비스를 사용 하는 경우 HTTP 요청 및 요청 메시지를 확인 하는 것이 매우 유용할 수 있습니다. Internet Explorer 9의 F12 개발자 도구를 사용 하 여이 작업을 수행할 수 있습니다. Internet Explorer 9에서 **F12** 키를 눌러 도구를 엽니다. **네트워크** 탭을 클릭 하 고 **캡처 시작**을 누릅니다. 이제 웹 페이지로 돌아가 **F5** 키를 눌러 웹 페이지를 다시 로드 합니다. Internet Explorer는 브라우저와 웹 서버 간의 HTTP 트래픽을 캡처합니다. 요약 보기에는 페이지에 대 한 모든 네트워크 트래픽이 표시 됩니다.

![](tutorial-your-first-web-api/_static/image14.png)

상대 URI "api/products/" 항목을 찾습니다. 이 항목을 선택 하 고 **자세히 보기로 이동을**클릭 합니다. 자세히 보기에는 요청 및 응답 헤더와 본문을 볼 수 있는 탭이 있습니다. 예를 들어 **요청 헤더** 탭을 클릭 하면 클라이언트가 Accept 헤더에 &quot;application/json&quot; 요청한 것을 확인할 수 있습니다.

![](tutorial-your-first-web-api/_static/image15.png)

응답 본문 탭을 클릭 하면 제품 목록이 JSON으로 serialize 된 방법을 확인할 수 있습니다. 다른 브라우저는 비슷한 기능을가지고 있습니다. 또 다른 유용한 도구는 [Fiddler](http://www.fiddler2.com/fiddler2/)웹 디버깅 프록시입니다. Fiddler를 사용 하 여 HTTP 트래픽을 볼 수 있으며 요청에서 HTTP 헤더에 대 한 모든 권한을 제공 하는 HTTP 요청을 작성할 수도 있습니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 확인

완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까? 다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음과 같은 옵션을 사용할 수 있습니다.

- [무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.
- [Msdn 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -msdn 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.

## <a name="next-steps"></a>다음 단계

- POST, PUT 및 DELETE 작업을 지원 하 고 데이터베이스에 대 한 쓰기를 지 원하는 HTTP 서비스의 전체 예제는 [Entity Framework 6에서 WEB API 2 사용](../data/using-web-api-with-entity-framework/part-1.md)을 참조 하세요.
- HTTP 서비스를 기반으로 유체 및 응답성이 뛰어난 웹 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [ASP.NET Single Page Application](../../../single-page-application/index.md)을 참조 하세요.
- Azure App Service에 Visual Studio 웹 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [Azure App Service에서 ASP.NET 웹 앱 만들기](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)를 참조 하세요.
