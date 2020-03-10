---
uid: web-api/overview/security/external-authentication-services
title: ASP.NET Web API (C#)를 사용 하는 외부 인증 서비스 | Microsoft Docs
author: rmcmurray
description: ASP.NET Web API에서 외부 인증 서비스를 사용 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447419"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>ASP.NET Web API (C#)을 사용 하는 외부 인증 서비스

Visual Studio 2017 및 ASP.NET 4.7.2는 SPA ( [단일 페이지 응용 프로그램](../../../single-page-application/index.md) ) 및 [Web API](../../index.md) 서비스에 대 한 보안 옵션을 확장 하 여 여러 OAuth/openid connect 및 소셜 미디어 인증 서비스 (Microsoft 계정, Twitter, Facebook, Google 등)를 포함 하는 외부 인증 서비스와 통합 합니다.  

### <a name="in-this-walkthrough"></a>이 연습에서

- [외부 인증 서비스 사용](#USING)
- [샘플 웹 응용 프로그램 만들기](#SAMPLE)
- [Facebook 인증 사용](#FACEBOOK)
- [Google 인증 사용](#GOOGLE)
- [Microsoft 인증 사용](#MICROSOFT)
- [Twitter 인증 사용](#TWITTER)
- [추가 정보](#MOREINFO)

    - [외부 인증 서비스 결합](#COMBINE)
    - [정규화 된 도메인 이름을 사용 하도록 IIS Express 구성](#FQDN)
    - [Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법](#OBTAIN)
    - [선택 사항: 로컬 등록 사용 안 함](#DISABLE)

### <a name="prerequisites"></a>사전 요구 사항

이 연습의 예제를 따르려면 다음이 필요 합니다.

- Visual Studio 2017
- 다음 소셜 미디어 인증 서비스 중 하나에 대 한 응용 프로그램 식별자 및 비밀 키가 포함 된 개발자 계정:

  - Microsoft 계정 ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>외부 인증 서비스 사용

현재 웹 개발자에 게 제공 되는 외부 인증 서비스는 새 웹 응용 프로그램을 만들 때 개발 시간을 단축 하는 데 도움이 됩니다. 일반적으로 웹 사용자는 널리 사용 되는 웹 서비스 및 소셜 미디어 웹 사이트용으로 여러 기존 계정을 포함 하므로 웹 응용 프로그램은 외부 웹 서비스 또는 소셜 미디어 웹 사이트의 인증 서비스를 구현할 때 개발 시간을 저장 합니다. 인증 구현을 만드는 데 소요 된 시간입니다. 외부 인증 서비스를 사용 하면 최종 사용자가 웹 응용 프로그램에 대 한 다른 계정을 만들 필요가 없으며 다른 사용자 이름과 암호를 기억할 필요가 없습니다.

이전에는 개발자에 게 고유한 인증 구현을 만들거나 외부 인증 서비스를 응용 프로그램에 통합 하는 방법을 배울 수 있는 두 가지 방법이 있습니다. 가장 기본적인 수준에서 다음 다이어그램은 외부 인증 서비스를 사용 하도록 구성 된 웹 응용 프로그램에서 정보를 요청 하는 사용자 에이전트 (웹 브라우저)의 간단한 요청 흐름을 보여 줍니다.

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

위의 다이어그램에서 사용자 에이전트 (또는이 예제의 웹 브라우저)는 웹 브라우저를 외부 인증 서비스로 리디렉션하는 웹 응용 프로그램에 요청을 만듭니다. 사용자 에이전트는 외부 인증 서비스에 자격 증명을 보내고, 사용자 에이전트가 성공적으로 인증 되 면 외부 인증 서비스는 사용자 에이전트를 원래 웹 응용 프로그램으로 리디렉션하여 사용자 에이전트가 웹 응용 프로그램에 전송 됩니다. 웹 응용 프로그램은 토큰을 사용 하 여 사용자 에이전트가 외부 인증 서비스에 의해 성공적으로 인증 되었는지 확인 하 고 웹 응용 프로그램은이 토큰을 사용 하 여 사용자 에이전트에 대 한 추가 정보를 수집할 수 있습니다. 응용 프로그램이 사용자 에이전트 정보 처리를 완료 하면 웹 응용 프로그램은 권한 부여 설정에 따라 사용자 에이전트에 대 한 적절 한 응답을 반환 합니다.

이 두 번째 예제에서는 사용자 에이전트가 웹 응용 프로그램 및 외부 권한 부여 서버와 협상 하 고 웹 응용 프로그램은 외부 권한 부여 서버와의 추가 통신을 수행 하 여 사용자에 대 한 추가 정보를 검색 합니다. 에이전트

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 및 ASP.NET 4.7.2는 다음 인증 서비스에 대 한 기본 제공 통합 기능을 제공 하 여 개발자를 위한 외부 인증 서비스와의 통합을 용이 하 게 합니다.

- Facebook
- Google
- Microsoft 계정 (Windows Live ID 계정)
- Twitter

이 연습의 예제에서는 Visual Studio 2017와 함께 제공 되는 새로운 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 지원 되는 각 외부 인증 서비스를 구성 하는 방법을 보여 줍니다.

> [!NOTE]
> 필요한 경우 외부 인증 서비스의 설정에 FQDN을 추가 해야 할 수 있습니다. 이 요구 사항은 클라이언트에서 사용 하는 FQDN과 일치 하도록 응용 프로그램 설정의 FQDN을 요구 하는 일부 외부 인증 서비스에 대 한 보안 제약 조건을 기반으로 합니다. 이에 대 한 단계는 각 외부 인증 서비스에 따라 크게 달라 집니다. 각 외부 인증 서비스에 대 한 설명서를 참조 하 여 필요한 경우와 이러한 설정을 구성 하는 방법을 확인 해야 합니다. 이 환경을 테스트 하는 데 FQDN을 사용 하도록 IIS Express를 구성 해야 하는 경우이 연습의 뒷부분에 나오는 [정규화 된 도메인 이름을 사용 하도록 IIS Express 구성](#FQDN) 섹션을 참조 하세요.

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>샘플 웹 응용 프로그램 만들기

다음 단계는 ASP.NET 웹 응용 프로그램 템플릿을 사용 하 여 샘플 응용 프로그램을 만드는 과정을 안내 하며,이 연습 뒷부분의 각 외부 인증 서비스에 대해이 샘플 응용 프로그램을 사용 합니다.

Visual Studio 2017를 시작 하 고 시작 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

**새 프로젝트** 대화 상자가 표시 되 면 **설치 됨** 을 선택 하 고 **시각적 C#개체** 를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET 웹 응용 프로그램 (.Net Framework)** 을 선택 합니다. 프로젝트의 이름을 입력 하 고 **확인**을 클릭 합니다.

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

**새 ASP.NET 프로젝트가** 표시 되 면 **단일 페이지 응용 프로그램** 템플릿을 선택 하 고 **프로젝트 만들기**를 클릭 합니다.

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

Visual Studio 2017가 프로젝트를 만들 때까지 기다립니다.

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Visual Studio 2017가 프로젝트 만들기를 완료 하면 **앱\_시작** 폴더에 있는 *Startup.Auth.cs* 파일을 엽니다.

프로젝트를 처음 만들 때 *Startup.Auth.cs* file에서 외부 인증 서비스를 사용 하도록 설정 하지 않았습니다. 다음은 ASP.NET 응용 프로그램을 사용 하 여 Microsoft 계정, Twitter, Facebook 또는 Google 인증을 사용 하기 위해 외부 인증 서비스 및 모든 관련 설정을 사용 하도록 설정 하는 섹션을 강조 표시 하는 코드의 예입니다.

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

F5 키를 눌러 웹 응용 프로그램을 빌드 및 디버그할 때 외부 인증 서비스가 정의 되지 않은 것을 볼 수 있는 로그인 화면이 표시 됩니다.

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

다음 섹션에서는 Visual Studio 2017에서 ASP.NET와 함께 제공 되는 각 외부 인증 서비스를 사용 하도록 설정 하는 방법에 대해 설명 합니다.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Facebook 인증 사용

Facebook 인증을 사용 하려면 Facebook 개발자 계정을 만들어야 하며, 프로젝트에서 작동 하려면 Facebook의 응용 프로그램 ID 및 비밀 키가 필요 합니다. Facebook 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)을 참조 하세요.

응용 프로그램 ID 및 비밀 키를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대해 Facebook 인증을 사용 하도록 설정 합니다.

1. 프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.

2. 코드의 Facebook 인증 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. &quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 응용 프로그램 ID 및 비밀 키를 추가 합니다. 이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Facebook이 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. **Facebook** 단추를 클릭 하면 브라우저는 facebook 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. Facebook 자격 증명을 입력 하 고 **로그인**을 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션됩니다. 그러면 facebook 계정에 연결 하려는 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. 사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Facebook 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Google 인증 사용

Google 인증을 사용 하려면 Google 개발자 계정을 만들어야 하며, 프로젝트는 작동 하기 위해 Google의 응용 프로그램 ID 및 비밀 키가 필요 합니다. Google 개발자 계정을 만들고 응용 프로그램 ID 및 비밀 키를 가져오는 방법에 대 한 자세한 내용은 [https://developers.google.com](https://developers.google.com)을 참조 하세요.

웹 응용 프로그램에 대해 Google 인증을 사용 하도록 설정 하려면 다음 단계를 사용 합니다.

1. 프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.

2. 코드의 Google 인증 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. &quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 응용 프로그램 ID 및 비밀 키를 추가 합니다. 이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Google이 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. **Google** 단추를 클릭 하면 브라우저는 google 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. Google 자격 증명을 입력 하 고 **로그인**을 클릭 하면 google에서 웹 응용 프로그램에 google 계정에 액세스할 수 있는 권한이 있는지 확인 하는 메시지를 표시 합니다.

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. **수락**을 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Google 계정에 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. 사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램은 Google 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Microsoft 인증 사용

Microsoft 인증을 사용 하려면 개발자 계정을 만들어야 하며, 기능을 위해서는 클라이언트 ID와 클라이언트 암호가 필요 합니다. Microsoft 개발자 계정을 만들고 클라이언트 ID 및 클라이언트 암호를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)를 참조 하세요.

소비자 키 및 소비자 암호를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대 한 Microsoft 인증을 사용 하도록 설정 합니다.

1. 프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.

2. 코드의 Microsoft 인증 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. &quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 클라이언트 ID 및 클라이언트 암호를 추가 합니다. 이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Microsoft가 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. **Microsoft** 단추를 클릭 하면 브라우저가 microsoft 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. Microsoft 자격 증명을 입력 하 고 **로그인**을 클릭 하면 웹 응용 프로그램에 Microsoft 계정에 액세스할 수 있는 권한이 있는지 확인 하는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. **예**를 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Microsoft 계정와 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. 사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Microsoft 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Twitter 인증 사용

Twitter 인증을 사용 하려면 개발자 계정을 만들어야 하며, 작동 하려면 소비자 키 및 소비자 암호가 필요 합니다. Twitter 개발자 계정을 만들고 소비자 키 및 소비자 암호를 가져오는 방법에 대 한 자세한 내용은 [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)를 참조 하세요.

소비자 키 및 소비자 암호를 가져온 후에는 다음 단계를 사용 하 여 웹 응용 프로그램에 대해 Twitter 인증을 사용 하도록 설정 합니다.

1. 프로젝트가 Visual Studio 2017에서 열리면 *Startup.Auth.cs* 파일을 엽니다.

2. 코드의 Twitter 인증 섹션을 찾습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. &quot;//&quot; 문자를 제거 하 여 강조 표시 된 코드 줄의 주석 처리를 제거 하 고 소비자 키 및 소비자 암호를 추가 합니다. 이러한 매개 변수를 추가한 후에는 프로젝트를 다시 컴파일할 수 있습니다.

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. F5 키를 눌러 웹 브라우저에서 웹 응용 프로그램을 열면 Twitter가 외부 인증 서비스로 정의 된 것을 볼 수 있습니다.

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. **Twitter** 단추를 클릭 하면 브라우저는 twitter 로그인 페이지로 리디렉션됩니다.

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. Twitter 자격 증명을 입력 하 고 **앱 권한 부여**를 클릭 하면 웹 브라우저가 웹 응용 프로그램으로 다시 리디렉션되고 Twitter 계정에 연결할 **사용자 이름을** 입력 하 라는 메시지가 표시 됩니다.

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. 사용자 이름을 입력 하 고 **등록** 단추를 클릭 하면 웹 응용 프로그램에서 Twitter 계정에 대 한 기본 **홈 페이지** 를 표시 합니다.

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>추가 정보

OAuth 및 Openid connect를 사용 하는 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 다음 Url을 참조 하세요.

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>외부 인증 서비스 결합

유연성을 높이기 위해 여러 외부 인증 서비스를 동시에 정의할 수 있습니다. 이렇게 하면 웹 응용 프로그램의 사용자가 사용 하도록 설정 된 외부 인증 서비스의 계정을 사용할 수 있습니다.

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>정규화 된 도메인 이름을 사용 하도록 IIS Express 구성

일부 외부 인증 공급자는 `http://localhost:port/`와 같은 HTTP 주소를 사용 하 여 응용 프로그램 테스트를 지원 하지 않습니다. 이 문제를 해결 하려면 호스트 파일에 정적 FQDN (정규화 된 도메인 이름) 매핑을 추가 하 고 테스트/디버깅에 FQDN을 사용 하도록 Visual Studio 2017에서 프로젝트 옵션을 구성할 수 있습니다. 이렇게 하려면 다음 단계를 수행합니다.

- 호스트 파일의 고정 FQDN 매핑을 추가 합니다.

  1. Windows에서 관리자 권한 명령 프롬프트를 엽니다.
  2. 다음 명령을 입력합니다.

      <kbd>메모장%WinDir%\system32\drivers\etc\hosts</kbd>
  3. HOSTS 파일에 다음과 같은 항목을 추가 합니다.

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. HOSTS 파일을 저장 하 고 닫습니다.

- FQDN을 사용 하도록 Visual Studio 프로젝트를 구성 합니다.

  1. Visual Studio 2017 **에서 프로젝트가 열리면 프로젝트 메뉴를** 클릭 한 다음 프로젝트의 속성을 선택 합니다. 예를 들어 **WebApplication1 속성**을 선택할 수 있습니다.
  2. **웹** 탭을 선택 합니다.
  3. <strong>프로젝트 Url</strong>에 대 한 FQDN을 입력 합니다. 예를 들어 호스트 파일에 추가한 FQDN 매핑 인 경우 <kbd><http://www.wingtiptoys.com></kbd> 를 입력 합니다.

- 응용 프로그램에 FQDN을 사용 하도록 IIS Express를 구성 합니다.

    1. Windows에서 관리자 권한 명령 프롬프트를 엽니다.
    2. 다음 명령을 입력 하 여 IIS Express 폴더로 변경 합니다.

        <kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 다음 명령을 입력 하 여 응용 프로그램에 FQDN을 추가 합니다.

        <kbd>appcmd.exe set config-section: system.web/sites/+&quot;[name = ' WebApplication1 ']. bindings. [protocol = ' http ', bindingInformation = ' *: 80: wingtiptoys ']&quot;/commit: apphost</kbd>

  여기서 **WebApplication1** 은 프로젝트의 이름이 고, **bindingInformation** 에는 테스트에 사용할 포트 번호 및 FQDN이 포함 되어 있습니다.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Microsoft 인증에 대 한 응용 프로그램 설정을 가져오는 방법

Microsoft 인증을 위해 Windows Live에 응용 프로그램을 연결 하는 것은 간단한 프로세스입니다. 응용 프로그램을 Windows Live에 아직 연결 하지 않은 경우 다음 단계를 사용할 수 있습니다.

1. [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) 로 이동 하 고 메시지가 표시 되 면 Microsoft 계정 이름과 암호를 입력 한 다음 **로그인**을 클릭 합니다.

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. **앱 추가** 를 선택 하 고 메시지가 표시 되 면 응용 프로그램의 이름을 입력 한 다음 **만들기**를 클릭 합니다.

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. **이름** 아래에서 앱을 선택 하면 해당 응용 프로그램 속성 페이지가 나타납니다.

4. 응용 프로그램에 대 한 리디렉션 도메인을 입력 합니다. **응용 프로그램 ID** 를 복사 하 고 **응용 프로그램**암호에서 **암호 생성**을 선택 합니다. 표시 되는 암호를 복사 합니다. 응용 프로그램 ID 및 암호는 클라이언트 ID 및 클라이언트 암호입니다. **확인** , **저장**을 차례로 선택 합니다.

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>선택 사항: 로컬 등록 사용 안 함

현재 ASP.NET 로컬 등록 기능을 통해 자동 프로그램 (봇)에서 구성원 계정을 만들 수 있습니다. 예를 들어 [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)와 같은 봇 방지 및 유효성 검사 기술을 사용 합니다. 따라서 로그인 페이지에서 로컬 로그인 양식 및 등록 링크를 제거 해야 합니다. 이렇게 하려면 프로젝트에서 *\_Login* 페이지를 열고 로컬 로그인 패널 및 등록 링크에 대 한 줄을 주석으로 처리 합니다. 결과 페이지는 다음 코드 샘플과 같습니다.

[!code-html[Main](external-authentication-services/samples/sample10.html)]

로컬 로그인 패널과 등록 링크를 사용 하지 않도록 설정 하면 로그인 페이지가 사용 하도록 설정한 외부 인증 공급자만 표시 됩니다.

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
