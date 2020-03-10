---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: ASP.NET Web Forms에서 Web API 사용-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 ASP.NET Forms 응용 프로그램에 Web API를 추가 하는 과정을 단계별로 안내 하는 코드를 사용 하는 자습서
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448535"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>ASP.NET 웹 양식과 Web API 사용

[Mike Wasson](https://github.com/MikeWasson)

이 자습서에서는 ASP.NET 4.x에서 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 추가 하는 단계를 안내 합니다. 

## <a name="overview"></a>개요

ASP.NET Web API는 ASP.NET MVC를 사용 하 여 패키지 되지만 기존 ASP.NET Web Forms 응용 프로그램에 Web API를 쉽게 추가할 수 있습니다.

Web Forms 응용 프로그램에서 Web API를 사용 하려면 두 가지 주요 단계가 있습니다.

- **ApiController** 클래스에서 파생 되는 Web API 컨트롤러를 추가 합니다.
- **응용 프로그램\_Start** 메서드에 경로 테이블을 추가 합니다.

## <a name="create-a-web-forms-project"></a>Web Forms 프로젝트 만들기

Visual Studio를 시작 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET Web Forms 응용 프로그램**을 선택 합니다. 프로젝트의 이름을 입력 하 고 **확인**을 클릭 합니다.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>모델 및 컨트롤러 만들기

이 자습서에서는 [시작](tutorial-your-first-web-api.md) 자습서와 동일한 모델 및 컨트롤러 클래스를 사용 합니다.

먼저 모델 클래스를 추가 합니다. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **클래스 추가**를 선택 합니다. 클래스 이름을 Product로, 다음 구현을 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

그런 다음 프로젝트에 웹 API 컨트롤러를 추가 합니다. *컨트롤러* 는 web api에 대 한 HTTP 요청을 처리 하는 개체입니다.

**솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다. **새 항목 추가**를 선택 합니다.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

**설치 된 템플릿**에서  **C# Visual** 을 확장 하 고 **웹**을 선택 합니다. 그런 다음 템플릿 목록에서 **WEB API 컨트롤러 클래스**를 선택 합니다. 컨트롤러 이름을 "ProductsController"로 하 고 **추가**를 클릭 합니다.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

**새 항목 추가** 마법사에서 이름이 ProductsController.cs 인 파일을 만듭니다. 마법사에 포함 된 메서드를 삭제 하 고 다음 메서드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

이 컨트롤러의 코드에 대 한 자세한 내용은 [초보자](tutorial-your-first-web-api.md) 를 위한 자습서를 참조 하세요.

## <a name="add-routing-information"></a>라우팅 정보 추가

다음으로,/api/products/&quot; &quot;폼의 Uri가 컨트롤러로 라우팅되도록 URI 경로를 추가 합니다.

**솔루션 탐색기**에서 global.asax를 두 번 클릭 하 여 코드 Global.asax.cs 파일을 엽니다. 다음 **using** 문을 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

그런 다음 **응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

라우팅 테이블에 대 한 자세한 내용은 [ASP.NET Web API 라우팅](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)을 참조 하세요.

## <a name="add-client-side-ajax"></a>클라이언트 쪽 AJAX 추가

클라이언트에서 액세스할 수 있는 web API를 만들어야 합니다. 이제 jQuery를 사용 하 여 API를 호출 하는 HTML 페이지를 추가 해 보겠습니다.

마스터 페이지 (예: site.master)에 `ID="HeadContent"`의 `ContentPlaceHolder` 포함 되어 있는지 *확인 합니다.*

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Default.aspx 파일을 엽니다. 다음과 같이 주 콘텐츠 섹션에 있는 상용구 텍스트를 바꿉니다.

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

다음으로 `HeaderContent` 섹션에서 jQuery 소스 파일에 대 한 참조를 추가 합니다.

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

참고: **솔루션 탐색기** 파일을 코드 편집기 창으로 끌어서 놓아 스크립트 참조를 쉽게 추가할 수 있습니다.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

JQuery 스크립트 태그 아래에 다음 스크립트 블록을 추가 합니다.

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

문서가 로드 되 면이 스크립트는 &quot;api/products&quot;에 대 한 AJAX 요청을 만듭니다. 요청은 제품 목록을 JSON 형식으로 반환 합니다. 스크립트는 HTML 테이블에 제품 정보를 추가 합니다.

응용 프로그램을 실행 하는 경우 다음과 같이 표시 됩니다.

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
