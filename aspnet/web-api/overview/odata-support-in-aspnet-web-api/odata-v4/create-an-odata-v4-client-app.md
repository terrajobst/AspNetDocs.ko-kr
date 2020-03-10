---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 클라이언트 앱 만들기 (C#) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448121"
---
# <a name="create-an-odata-v4-client-app-c"></a>OData v4 클라이언트 앱 만들기(C#)

[Mike Wasson](https://github.com/MikeWasson)

이전 자습서에서는 CRUD 작업을 지 원하는 기본 OData 서비스를 만들었습니다. 이제 서비스에 대 한 클라이언트를 만들어 보겠습니다.

Visual Studio의 새 인스턴스를 시작 하 고 새 콘솔 응용 프로그램 프로젝트를 만듭니다. **새 프로젝트** 대화 상자에서 **설치** &gt; **템플릿** &gt;  **C# Visual** &gt; **Windows Desktop**을 선택 하 고 **콘솔 응용 프로그램** 템플릿을 선택 합니다. 프로젝트 이름을 ProductsApp&quot;로 &quot;합니다.

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> 또한 OData 서비스를 포함 하는 동일한 Visual Studio 솔루션에 콘솔 앱을 추가할 수 있습니다.

## <a name="install-the-odata-client-code-generator"></a>OData 클라이언트 코드 생성기 설치

**도구** 메뉴에서 **확장 및 업데이트**를 선택합니다. **온라인** &gt; **Visual Studio 갤러리**를 선택 합니다. 검색 상자에서 &quot;OData 클라이언트 코드 생성기&quot;를 검색 합니다. **다운로드** 를 클릭 하 여 VSIX를 설치 합니다. Visual Studio를 다시 시작 하 라는 메시지가 표시 될 수 있습니다.

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>OData 서비스를 로컬로 실행

Visual Studio에서 제품 서비스 프로젝트를 실행 합니다. 기본적으로 Visual Studio는 응용 프로그램 루트에 대 한 브라우저를 시작 합니다. URI를 적어둡니다. 이는 다음 단계에서 필요 합니다. 애플리케이션을 실행 상태로 둡니다.

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> 동일한 솔루션에 두 프로젝트를 모두 배치 하는 경우에는 디버깅 하지 않고 제품 서비스 프로젝트를 실행 해야 합니다. 다음 단계에서는 콘솔 응용 프로그램 프로젝트를 수정 하는 동안 서비스를 실행 상태로 유지 해야 합니다.

## <a name="generate-the-service-proxy"></a>서비스 프록시를 생성 합니다.

서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는 .NET 클래스입니다. 프록시는 메서드 호출을 HTTP 요청으로 변환 합니다. [T4 템플릿을](https://msdn.microsoft.com/library/bb126445.aspx)실행 하 여 프록시 클래스를 만듭니다.

프로젝트를 마우스 오른쪽 단추로 클릭합니다. **추가** &gt; **새 항목**을 선택합니다.

![](create-an-odata-v4-client-app/_static/image5.png)

**새 항목 추가** 대화 상자에서  **C# Visual Items** &gt; **코드** &gt; **OData 클라이언트**를 선택 합니다. 템플릿 이름을 ProductClient.tt&quot;로 &quot;합니다. **추가** 를 클릭 하 고 보안 경고를 클릭 합니다.

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

이 시점에서 무시 해도 오류가 발생 합니다. Visual Studio에서 자동으로 템플릿을 실행 하지만 템플릿에는 먼저 일부 구성 설정이 필요 합니다.

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

제품 클라이언트. odata .config 파일을 엽니다. `Parameter` 요소에서 제품 서비스 프로젝트 (이전 단계)의 URI에 붙여넣습니다. 다음은 그 예입니다.

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

템플릿을 다시 실행 합니다. 솔루션 탐색기에서 ProductClient.tt 파일을 마우스 오른쪽 단추로 클릭 하 고 **사용자 지정 도구 실행**을 선택 합니다.

템플릿은 프록시를 정의 하는 ProductClient.cs 라는 코드 파일을 만듭니다. 앱을 개발할 때 OData 끝점을 변경 하는 경우 템플릿을 다시 실행 하 여 프록시를 업데이트 합니다.

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>서비스 프록시를 사용 하 여 OData 서비스 호출

Program.cs 파일을 열고 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

*ServiceUri* 의 값을 앞의 서비스 URI로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

앱을 실행 하면 다음이 출력 됩니다.

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
