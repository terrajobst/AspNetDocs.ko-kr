---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 시작 클래스 검색 | Microsoft Docs
author: Praburaj
description: 이 자습서에서는 로드 되는 OWIN 시작 클래스를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 프로젝트 Katana 개요를 참조 하세요. 이 자습서는 ...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500183"
---
# <a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색

> 이 자습서에서는 로드 되는 OWIN 시작 클래스를 구성 하는 방법을 보여 줍니다. OWIN에 대 한 자세한 내용은 [프로젝트 Katana 개요](an-overview-of-project-katana.md)를 참조 하세요. 이 자습서는 Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan 및 Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) )에 의해 작성 되었습니다.
>
> ## <a name="prerequisites"></a>사전 요구 사항
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>OWIN 시작 클래스 검색

 모든 OWIN 응용 프로그램에는 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 startup 클래스가 있습니다. 선택 하는 호스팅 모델 (OwinHost, IIS 및 IIS Express)에 따라 시작 클래스를 런타임과 연결할 수 있는 여러 가지 방법이 있습니다. 이 자습서에 표시 된 startup 클래스는 모든 호스팅 응용 프로그램에서 사용할 수 있습니다. 다음 방법 중 하나를 사용 하 여 시작 클래스를 호스팅 런타임과 연결 합니다.

1. **명명 규칙**: Katana는 네임 스페이스에서 어셈블리 이름이 나 전역 네임 스페이스와 일치 하는 `Startup` 클래스를 찾습니다.
2. **OwinStartup Attribute**: 대부분의 개발자가 시작 클래스를 지정 하는 데 사용 하는 방법입니다. 다음 특성은 startup 클래스를 `StartupDemo` 네임 스페이스의 `TestStartup` 클래스로 설정 합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   `OwinStartup` 특성은 명명 규칙을 재정의 합니다. 이 특성을 사용 하 여 친숙 한 이름을 지정할 수도 있습니다. 그러나 이름을 사용 하려면 구성 파일의 `appSetting` 요소도 사용 해야 합니다.
3. **구성 파일의 appSetting 요소**: `appSetting` 요소는 `OwinStartup` 특성 및 명명 규칙을 재정의 합니다. 여러 시작 클래스 (각각 `OwinStartup` 특성 사용)를 사용 하 고 다음과 비슷한 태그를 사용 하 여 구성 파일에 로드 되는 시작 클래스를 구성할 수 있습니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   시작 클래스와 어셈블리를 명시적으로 지정 하는 다음 키를 사용할 수도 있습니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   구성 파일의 다음 XML은 `ProductionConfiguration`의 시작 클래스 이름을 지정 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   위의 태그는 친숙 한 이름을 지정 하 고 `ProductionStartup2` 클래스를 실행 하는 다음과 같은 `OwinStartup` 특성과 함께 사용 해야 합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. OWIN 시작 검색을 사용 하지 않도록 설정 하려면 web.config 파일에 `"false"` 값을 사용 하 여 `appSetting owin:AutomaticAppStartup`를 추가 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>OWIN 시작을 사용 하 여 ASP.NET 웹 앱 만들기

1. 빈 Asp.Net 웹 응용 프로그램을 만들고 이름을 **Startupdemo**로 이름을 입력 합니다. -NuGet 패키지 관리자를 사용 하 여 `Microsoft.Owin.Host.SystemWeb`를 설치 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 선택 합니다. 다음 명령을 입력합니다.

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. OWIN startup 클래스를 추가 합니다. Visual Studio 2017에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **클래스 추가**를 선택 합니다.- **새 항목 추가** 대화 상자에서 검색 필드에 *OWIN* 를 입력 하 고 이름을 Startup.cs로 변경한 다음 **추가**를 선택 합니다.

     ![](owin-startup-class-detection/_static/image1.png)

   다음 번에 *Owin 시작 클래스*를 추가 하려면 **추가** 메뉴에서 사용할 수 있습니다.

     ![](owin-startup-class-detection/_static/image2.png)

   또는 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 하 고 **Owin 시작 클래스**를 선택할 수 있습니다.

     ![](owin-startup-class-detection/_static/image3.png)

- *Startup.cs* 파일에서 생성 된 코드를 다음으로 바꿉니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  `app.Use` 람다 식은 지정 된 미들웨어 구성 요소를 OWIN 파이프라인에 등록 하는 데 사용 됩니다. 이 경우 들어오는 요청에 응답 하기 전에 들어오는 요청에 대 한 로깅을 설정 합니다. `next` 매개 변수는 파이프라인의 다음 구성 요소에 대 한 대리자 ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;)입니다. `app.Run` 람다 식은 파이프라인을 들어오는 요청에 후크하고 응답 메커니즘을 제공 합니다.
     > [!NOTE]
     > 위의 코드에서는 `OwinStartup` 특성을 주석으로 처리 했으며, `Startup` 라는 클래스를 실행 하는 규칙에 의존 하 고 있습니다. 응용 프로그램을 실행 하려면 ***F5*** 키를 누릅니다. 새로 고침을 몇 번 누릅니다.

    ![](owin-startup-class-detection/_static/image4.png) 참고:이 자습서의 이미지에 표시 된 숫자는 표시 된 수와 일치 하지 않습니다. 페이지를 새로 고치면 밀리초 문자열이 새 응답을 표시 하는 데 사용 됩니다.
  **출력** 창에서 추적 정보를 볼 수 있습니다.

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>시작 클래스 추가

이 섹션에서는 다른 시작 클래스를 추가 합니다. 응용 프로그램에 여러 OWIN startup 클래스를 추가할 수 있습니다. 예를 들어 개발, 테스트 및 프로덕션을 위한 시작 클래스를 만들 수 있습니다.

1. 새 OWIN 시작 클래스를 만들고 이름을 `ProductionStartup`로 합니다.
2. 생성된 코드를 다음으로 바꿉니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. Control F5 키를 눌러 앱을 실행 합니다. `OwinStartup` 특성은 프로덕션 시작 클래스를 실행 하도록 지정 합니다.

    ![](owin-startup-class-detection/_static/image6.png)
4. 다른 OWIN Startup 클래스를 만들고 이름을 `TestStartup`로 합니다.
5. 생성된 코드를 다음으로 바꿉니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   위의 `OwinStartup` 특성 오버 로드는 `TestingConfiguration`를 시작 클래스의 *친숙* 한 이름으로 지정 합니다.
6. *Web.config* 파일을 열고 시작 클래스의 이름을 지정 하는 OWIN App 시작 키를 추가 합니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. Control F5 키를 눌러 앱을 실행 합니다. 앱 설정 요소는 우선 순위가 있으며 테스트 구성이 실행 됩니다.

    ![](owin-startup-class-detection/_static/image7.png)
8. `TestStartup` 클래스의 `OwinStartup` 특성 *에서 이름을 제거 합니다.*

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. *Web.config* 파일에서 OWIN App 시작 키를 다음으로 바꿉니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. 각 클래스의 `OwinStartup` 특성을 Visual Studio에서 생성 된 기본 특성 코드로 되돌립니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    아래의 각 OWIN 앱 시작 키로 인해 프로덕션 클래스가 실행 됩니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    마지막 시작 키는 시작 구성 방법을 지정 합니다. 다음 OWIN App 시작 키를 사용 하 여 구성 클래스의 이름을 `MyConfiguration`으로 변경할 수 있습니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Owinhost .exe 사용

1. Web.config 파일을 다음 태그로 바꿉니다.

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   마지막 키가 있으므로이 경우 `TestStartup` 지정 됩니다.
2. PMC에서 Owinhost를 설치 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. 응용 프로그램 폴더 ( *web.config 파일이 포함 된 폴더* )로 이동 하 고 명령 프롬프트에서 다음을 입력 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   명령 창에 다음이 표시 됩니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. URL `http://localhost:5000/`를 사용 하 여 브라우저를 시작 합니다.

    ![](owin-startup-class-detection/_static/image8.png)

   OwinHost는 위에 나열 된 시작 규칙을 적용 합니다.
5. 명령 창에서 Enter 키를 눌러 OwinHost를 종료 합니다.
6. `ProductionStartup` 클래스에서 *ProductionConfiguration*의 이름을 지정 하는 다음 OwinStartup 특성을 추가 합니다.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. 명령 프롬프트에서 다음을 입력 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   프로덕션 시작 클래스가 로드 됩니다.
    ![](owin-startup-class-detection/_static/image9.png)

   응용 프로그램에는 여러 개의 시작 클래스가 있으며,이 예제에서는 런타임까지 로드할 시작 클래스를 지연 시켰습니다.
8. 다음 런타임 시작 옵션을 테스트 합니다.

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
