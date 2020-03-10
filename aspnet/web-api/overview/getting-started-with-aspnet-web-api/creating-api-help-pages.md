---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API에 대 한 도움말 페이지 만들기-ASP.NET 4.x
author: MikeWasson
description: 이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API에 대 한 도움말 페이지를 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448619"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a>ASP.NET Web API에 대 한 도움말 페이지 만들기

[Mike Wasson](https://github.com/MikeWasson)

이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API에 대 한 도움말 페이지를 만드는 방법을 보여 줍니다.

Web API를 만들 때 다른 개발자가 API를 호출 하는 방법을 알 수 있도록 도움말 페이지를 만드는 것이 유용한 경우가 많습니다. 모든 설명서를 수동으로 만들 수 있지만 최대한 자동 생성 하는 것이 좋습니다. 이 작업을 더 쉽게 수행 하기 위해 ASP.NET Web API는 런타임에 도움말 페이지를 자동으로 생성 하기 위한 라이브러리를 제공 합니다.

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>API 도움말 페이지 만들기

[ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)를 설치 합니다. 이 업데이트는 웹 API 프로젝트 템플릿에 도움말 페이지를 통합 합니다.

다음으로, 새 ASP.NET MVC 4 프로젝트를 만들고 웹 API 프로젝트 템플릿을 선택 합니다. 프로젝트 템플릿은 `ValuesController`이라는 예제 API 컨트롤러를 만듭니다. 템플릿은 또한 API 도움말 페이지를 만듭니다. 도움말 페이지의 모든 코드 파일은 프로젝트의 영역 폴더에 배치 됩니다.

![](creating-api-help-pages/_static/image2.png)

응용 프로그램을 실행할 때 홈 페이지에는 API 도움말 페이지에 대 한 링크가 포함 되어 있습니다. 홈 페이지에서 상대 경로는/Help.

![](creating-api-help-pages/_static/image3.png)

이 링크를 누르면 API 요약 페이지가 표시 됩니다.

![](creating-api-help-pages/_static/image4.png)

이 페이지에 대 한 MVC 뷰는 Areas/HelpPage/Views/Help/Index. cshtml에 정의 되어 있습니다. 이 페이지를 편집 하 여 레이아웃, 소개, 제목, 스타일 등을 수정할 수 있습니다.

페이지의 주요 부분은 컨트롤러 별로 그룹화 된 Api의 테이블입니다. Table 항목은 **Iapiexplorer** 인터페이스를 사용 하 여 동적으로 생성 됩니다. 이 인터페이스에 대해서는 나중에 자세히 설명 합니다. 새 API 컨트롤러를 추가 하는 경우 테이블은 런타임에 자동으로 업데이트 됩니다.

"API" 열에는 HTTP 메서드 및 상대 URI가 나열 됩니다. "설명" 열에는 각 API에 대 한 설명서가 포함 되어 있습니다. 처음에는 설명서가 자리 표시자 텍스트입니다. 다음 섹션에서는 XML 주석에서 설명서를 추가 하는 방법을 보여 줍니다.

각 API에는 예제 요청 및 응답 본문을 포함 하 여 보다 자세한 정보를 포함 하는 페이지에 대 한 링크가 있습니다.

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>기존 프로젝트에 도움말 페이지 추가

NuGet 패키지 관리자를 사용 하 여 기존 Web API 프로젝트에 도움말 페이지를 추가할 수 있습니다. 이 옵션은 "Web API" 템플릿과 다른 프로젝트 템플릿에서 시작 하는 데 유용 합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. [패키지 관리자 콘솔](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) 창에서 다음 명령 중 하나를 입력 합니다.

**C#** 응용 프로그램의 경우: `Install-Package Microsoft.AspNet.WebApi.HelpPage`

**Visual Basic** 응용 프로그램의 경우: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

에 C# 는 두 개의 패키지가 있습니다. 하나는 Visual Basic입니다. 프로젝트와 일치 하는 항목을 사용 해야 합니다.

이 명령은 필요한 어셈블리를 설치 하 고 영역/도움말 페이지 폴더에 있는 도움말 페이지에 대 한 MVC 뷰를 추가 합니다. 도움말 페이지에 대 한 링크를 수동으로 추가 해야 합니다. URI는/Help. Razor 뷰에서 링크를 만들려면 다음을 추가 합니다.

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

또한 영역을 등록 해야 합니다. Global.asax 파일에서 다음 코드를 **응용 프로그램\_Start** 메서드에 추가 합니다 (아직 없는 경우).

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>API 설명서 추가

기본적으로 도움말 페이지에는 설명서에 대 한 자리 표시자 문자열이 있습니다. [XML 문서 주석을](https://msdn.microsoft.com/library/b2s063f7.aspx) 사용 하 여 설명서를 만들 수 있습니다. 이 기능을 사용 하도록 설정 하려면 파일 영역/도움말 페이지/앱\_Start/HelpPageConfig을 열고 다음 줄의 주석 처리를 제거 합니다.

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

이제 XML 설명서를 사용 하도록 설정 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **빌드** 페이지를 선택 합니다.

![](creating-api-help-pages/_static/image6.png)

**출력**에서 **XML 문서 파일**을 선택 합니다. 편집 상자에 "App\_Data/XmlDocument .xml"을 입력 합니다.

![](creating-api-help-pages/_static/image7.png)

그런 다음/Controllers/ValuesController.cs.에 정의 된 `ValuesController` API 컨트롤러에 대 한 코드를 엽니다. 컨트롤러 메서드에 몇 가지 설명서 주석을 추가 합니다. 다음은 그 예입니다.

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> 팁: 메서드 위의 줄에 캐럿을 배치 하 고 세 개의 슬래시를 입력 하면 Visual Studio에서 XML 요소를 자동으로 삽입 합니다. 그런 다음 공백을 입력할 수 있습니다.

이제 응용 프로그램을 빌드 및 실행 하 고 도움말 페이지로 이동 합니다. 설명서 문자열은 API 테이블에 표시 되어야 합니다.

![](creating-api-help-pages/_static/image8.png)

도움말 페이지는 런타임에 XML 파일에서 문자열을 읽습니다. 응용 프로그램을 배포할 때 XML 파일을 배포 해야 합니다.

## <a name="under-the-hood"></a>내부적으로

도움말 페이지는 웹 API 프레임 워크의 일부인 **Apiexplorer** 클래스 위에 빌드됩니다. **Apiexplorer** 클래스는 도움말 페이지를 만들기 위한 원시 자료를 제공 합니다. 각 API에 대해 **Apiexplorer** 는 api를 설명 하는 **apiexplorer** 을 포함 합니다. 이러한 목적을 위해 "API"는 HTTP 메서드와 상대 URI의 조합으로 정의 됩니다. 예를 들어, 다음은 몇 가지 고유한 Api입니다.

- /Api/제품 가져오기
- /Api/Products/{id} 가져오기
- 게시/a n o/제품

컨트롤러 작업에서 여러 HTTP 메서드를 지 원하는 경우 **Apiexplorer** 는 각 메서드를 고유한 API로 처리 합니다.

**Apiexplorer**에서 API를 숨기려면 **ApiExplorerSettings** 특성을 작업에 추가 하 고 *ignoreapi* 를 true로 설정 합니다.

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

컨트롤러에이 특성을 추가 하 여 전체 컨트롤러를 제외할 수도 있습니다.

ApiExplorer 클래스는 **Idocumentationprovider** 인터페이스에서 설명서 문자열을 가져옵니다. 앞서 살펴본 것 처럼 도움말 페이지 라이브러리는 XML 문서 문자열에서 설명서를 가져오는 **Idocumentationprovider** 를 제공 합니다. 코드는/Areas/HelpPage/XmlDocumentationProvider.cs.에 있습니다. 고유한 **Idocumentationprovider**를 작성 하 여 다른 원본에서 설명서를 가져올 수 있습니다. 연결 하려면 **HelpPageConfigurationExtensions** 에 정의 된 **Setdocumentationprovider** 확장 메서드를 호출 합니다.

**Apiexplorer** 는 자동으로 **Idocumentationprovider** 인터페이스를 호출 하 여 각 API에 대 한 설명서 문자열을 가져옵니다. **Apidescription** 및 **ApiParameterDescription** 개체의 **설명서** 속성에 저장 합니다.

## <a name="next-steps"></a>다음 단계

여기에 표시 된 도움말 페이지로 제한 되지 않습니다. 실제로 **Apiexplorer** 는 도움말 페이지를 만드는 것으로 제한 되지 않습니다. Yao Huang 링크는 다음과 같은 몇 가지 유용한 블로그 게시물을 작성 하 여이에 대해 알아 볼 수 있습니다.

- [ASP.NET Web API 도움말 페이지에 간단한 테스트 클라이언트 추가](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [ASP.NET Web API 도움말 페이지에서 자체 호스팅 서비스에 대해 작업 수행](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API에 대 한 도움말 페이지 (또는 클라이언트)의 디자인 타임 생성](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [고급 도움말 페이지 사용자 지정](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
