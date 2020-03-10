---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: MVC 4에서 OAuth 공급자 사용 | Microsoft Docs
author: Rick-Anderson
description: '이 자습서에서는 사용자가 외부 공급자 (예: Facebo)에서 자격 증명을 사용 하 여 로그인 할 수 있도록 하는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다.'
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433367"
---
# <a name="using-oauth-providers-with-mvc-4"></a>MVC 4와 함께 OAuth 공급자 사용

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 사용자가 Facebook, Twitter, Microsoft 또는 Google과 같은 외부 공급자의 자격 증명을 사용 하 여 로그인 한 다음 해당 공급자의 일부 기능을에 통합할 수 있도록 하는 ASP.NET MVC 4 웹 응용 프로그램을 빌드하는 방법을 보여 줍니다. 웹 응용 프로그램. 간단히 하기 위해이 자습서에서는 Facebook에서 자격 증명을 사용 하는 방법을 집중적으로 설명 합니다.
> 
> ASP.NET MVC 5 웹 응용 프로그램에서 외부 자격 증명을 사용 하려면 [Facebook 및 Google OAuth2 및 Openid connect sign-on을 사용 하 여 ASP.NET MVC 5 앱 만들기](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)를 참조 하세요.
> 
> 웹 사이트에서 이러한 자격 증명을 사용 하도록 설정 하면 수백만 명의 사용자가 이미 이러한 외부 공급자를 사용 하는 계정을 갖고 있기 때문에 상당한 이점이 있습니다. 이러한 사용자는 새 자격 증명 집합을 만들고 기억할 필요가 없는 경우 사이트에 등록 하는 것이 더 쉬운데 수 있습니다. 또한 사용자가 이러한 공급자 중 하나를 통해 로그인 한 후에는 공급자의 소셜 작업을 통합할 수 있습니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에는 다음과 같은 두 가지 주요 목표가 있습니다.

1. 사용자가 OAuth 공급자의 자격 증명으로 로그인 할 수 있도록 설정 합니다.
2. 공급자 로부터 계정 정보를 검색 하 고 해당 정보를 사이트의 계정 등록과 통합 합니다.

이 자습서의 예제에서는 Facebook을 인증 공급자로 사용 하는 방법에 중점을 두지만 모든 공급자를 사용 하도록 코드를 수정할 수 있습니다. 모든 공급자를 구현 하는 단계는이 자습서에 표시 되는 단계와 매우 비슷합니다. 공급자의 API 집합을 직접 호출 하는 경우에만 상당한 차이점이 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) 또는 [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

또는

- Microsoft Visual Studio 2010 SP1 또는 [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

또한이 항목에서는 ASP.NET MVC 및 Visual Studio에 대 한 기본 지식이 있다고 가정 합니다. ASP.NET MVC 4를 소개 해야 하는 경우 [ASP.NET mvc 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)소개를 참조 하세요.

## <a name="create-the-project"></a>프로젝트 만들기

Visual Studio에서 새 ASP.NET MVC 4 웹 응용 프로그램을 만들고 &quot;OAuthMVC&quot;로 이름을로 합니다. .NET Framework 4.5 또는 4 중 하나를 대상으로 지정할 수 있습니다.

![프로젝트 만들기](using-oauth-providers-with-mvc/_static/image1.png)

새 ASP.NET MVC 4 프로젝트 창에서 **인터넷 응용 프로그램** 을 선택 하 고 **Razor** 를 뷰 엔진으로 둡니다.

![인터넷 응용 프로그램 선택](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>공급자 사용

인터넷 응용 프로그램 템플릿을 사용 하 여 MVC 4 웹 응용 프로그램을 만들 때 프로젝트는 App\_시작 폴더에 AuthConfig.cs 라는 파일로 생성 됩니다.

![AuthConfig 파일](using-oauth-providers-with-mvc/_static/image3.png)

AuthConfig 파일에는 외부 인증 공급자에 대 한 클라이언트를 등록 하는 코드가 포함 되어 있습니다. 기본적으로이 코드는 주석 처리 되므로 외부 공급자를 사용할 수 없습니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

외부 인증 클라이언트를 사용 하려면이 코드의 주석 처리를 제거 해야 합니다. 사이트에 포함 하려는 공급자에 대해서만 주석 처리를 제거 합니다. 이 자습서에서는 Facebook 자격 증명만 사용 하도록 설정 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

위의 예제에서 메서드에는 등록 매개 변수에 대 한 빈 문자열이 포함 되어 있습니다. 이제 응용 프로그램을 실행 하려고 하면 매개 변수에 대해 빈 문자열이 허용 되지 않기 때문에 응용 프로그램에서 인수 예외를 throw 합니다. 유효한 값을 제공 하려면 다음 섹션에 표시 된 것 처럼 외부 공급자를 사용 하 여 웹 사이트를 등록 해야 합니다.

## <a name="registering-with-an-external-provider"></a>외부 공급자를 사용 하 여 등록

외부 공급자의 자격 증명을 사용 하 여 사용자를 인증 하려면 웹 사이트를 공급자에 등록 해야 합니다. 사이트를 등록 하면 클라이언트를 등록할 때 포함 하는 매개 변수 (예: 키 또는 id, 암호)가 수신 됩니다. 사용할 공급자가 포함 된 계정이 있어야 합니다.

이 자습서에서는 이러한 공급자에 등록 하기 위해 수행 해야 하는 단계를 모두 보여 주지는 않습니다. 일반적으로이 단계는 어렵습니다. 사이트를 성공적으로 등록 하려면 해당 사이트에서 제공 하는 지침을 따르세요. 사이트 등록을 시작 하려면 다음에 대 한 개발자 사이트를 참조 하십시오.

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

Facebook을 사용 하 여 사이트를 등록 하는 경우 아래 이미지에 나와 있는 것 처럼 사이트 도메인에 대 한 &quot;localhost&quot;를 제공 하 고 URL에 대해 `&quot; http://localhost/&quot;` 수 있습니다. Localhost를 사용 하는 것은 대부분의 공급자에서 작동 하지만 현재 Microsoft 공급자와는 작동 하지 않습니다. Microsoft 공급자의 경우 올바른 웹 사이트 URL을 포함 해야 합니다.

![사이트 등록](using-oauth-providers-with-mvc/_static/image4.png)

이전 이미지에서 앱 id, 앱 비밀 및 연락처 전자 메일의 값이 제거 되었습니다. 실제로 사이트를 등록 하는 경우 해당 값이 표시 됩니다. 앱 id 및 앱 암호에 대 한 값을 응용 프로그램에 추가할 것 이므로이를 확인 하는 것이 좋습니다.

## <a name="creating-test-users"></a>테스트 사용자 만들기

기존 Facebook 계정을 사용 하 여 사이트를 테스트 하지 않을 경우이 섹션을 건너뛸 수 있습니다.

Facebook 앱 관리 페이지에서 응용 프로그램에 대 한 테스트 사용자를 쉽게 만들 수 있습니다. 이러한 테스트 계정을 사용 하 여 사이트에 로그인 할 수 있습니다. 왼쪽 탐색 창에서 **역할** 링크를 클릭 하 고 **만들기** 링크를 클릭 하 여 테스트 사용자를 만듭니다.

![테스트 사용자 만들기](using-oauth-providers-with-mvc/_static/image5.png)

Facebook 사이트에서 자동으로 요청 하는 테스트 계정 수를 만듭니다.

## <a name="adding-application-id-and-secret-from-the-provider"></a>공급자의 응용 프로그램 id 및 암호를 추가 하는 중

이제 Facebook에서 id 및 암호를 수신 했으므로 AuthConfig 파일로 돌아가서 매개 변수 값으로 추가 합니다. 아래 표시 된 값은 실제 값이 아닙니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>외부 자격 증명으로 로그인

사이트에서 외부 자격 증명을 사용 하도록 설정 해야 합니다. 응용 프로그램을 실행 하 고 오른쪽 위 모서리의 로그인 링크를 클릭 합니다. 템플릿은 Facebook을 공급자로 등록 하 고 공급자 단추를 포함 한다는 것을 자동으로 인식 합니다. 여러 공급자를 등록 하는 경우 각각에 대 한 단추가 자동으로 포함 됩니다.

![외부 로그인](using-oauth-providers-with-mvc/_static/image6.png)

이 자습서에서는 외부 공급자에 대 한 로그인 단추를 사용자 지정 하는 방법에 대해서는 설명 하지 않습니다. 해당 정보는 [OAuth/openid connect 사용 시 로그인 UI 사용자 지정](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)을 참조 하세요.

Facebook 단추를 클릭 하 여 Facebook 자격 증명으로 로그인 합니다. 외부 공급자 중 하나를 선택 하면 해당 사이트로 리디렉션되고 해당 서비스에 로그인 하 라는 메시지가 표시 됩니다.

다음 이미지는 Facebook의 로그인 화면을 보여 줍니다. Facebook 계정을 사용 하 여 oauthmvcexample 이라는 사이트에 로그인 하는 것을 설명 합니다.

![facebook 인증](using-oauth-providers-with-mvc/_static/image7.png)

Facebook 자격 증명을 사용 하 여 로그인 한 후에는 사이트에서 기본 정보에 액세스할 수 있음을 사용자에 게 알립니다.

![권한 요청](using-oauth-providers-with-mvc/_static/image8.png)

**앱으로 이동**을 선택한 후에는 사용자가 사이트에 등록 해야 합니다. 다음 그림은 사용자가 Facebook 자격 증명으로 로그인 한 후 등록 페이지를 보여 줍니다. 사용자 이름은 일반적으로 공급자의 이름으로 미리 채워집니다.

![register](using-oauth-providers-with-mvc/_static/image9.png)

등록 **을 클릭** 하 여 등록을 완료 합니다. 브라우저를 닫습니다.

새 계정이 데이터베이스에 추가 된 것을 볼 수 있습니다. 서버 탐색기에서 **Defaultconnection** 데이터베이스를 열고 **Tables** 폴더를 엽니다.

![데이터베이스 테이블](using-oauth-providers-with-mvc/_static/image10.png)

**UserProfile** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.

![데이터 표시](using-oauth-providers-with-mvc/_static/image11.png)

추가한 새 계정이 표시 됩니다. **웹 페이지\_OAuthMembership** 테이블의 데이터를 확인 합니다. 방금 추가한 계정에 대 한 외부 공급자와 관련 된 추가 데이터가 표시 됩니다.

외부 인증만 사용 하도록 설정 하려면 작업이 완료 된 것입니다. 그러나 다음 섹션에 표시 된 것 처럼 공급자의 정보를 새 사용자 등록 프로세스에 추가로 통합할 수 있습니다.

## <a name="create-models-for-additional-user-information"></a>추가 사용자 정보에 대 한 모델 만들기

이전 섹션에서 설명한 것 처럼, 기본 제공 계정 등록이 작동 하기 위해 추가 정보를 검색할 필요가 없습니다. 그러나 대부분의 외부 공급자는 사용자에 대 한 추가 정보를 다시 전달 합니다. 다음 섹션에서는 해당 정보를 유지 하 고 데이터베이스에 저장 하는 방법을 보여 줍니다. 특히 사용자의 전체 이름, 사용자 개인 웹 페이지의 URI 및 Facebook이 계정을 확인 했는지 여부를 나타내는 값에 대 한 값을 유지 합니다.

[Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 를 사용 하 여 추가 사용자 정보를 저장 하는 테이블을 추가 합니다. 기존 데이터베이스에 테이블을 추가 하는 것 이므로 먼저 현재 데이터베이스의 스냅숏을 만들어야 합니다. 현재 데이터베이스의 스냅숏을 만들면 나중에 새 테이블만 포함 하는 마이그레이션을 만들 수 있습니다. 현재 데이터베이스의 스냅숏을 만들려면 다음을 수행 합니다.

1. **패키지 관리자 콘솔** 을 엽니다.
2. **사용-마이그레이션** 명령을 실행 합니다.
3. 명령 **추가-마이그레이션 초기 – IgnoreChanges** 를 실행 합니다.
4. **Update-database** 명령을 실행 합니다.

이제 새 속성을 추가 합니다. 모델 폴더에서 AccountModels.cs 파일을 열고 RegisterExternalLoginModel 클래스를 찾습니다. RegisterExternalLoginModel 클래스에는 인증 공급자에서 반환 되는 값이 포함 됩니다. 아래 강조 표시 된 것 처럼 FullName 및 Link 라는 속성을 추가 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

또한 AccountModels.cs에서 ExtraUserInformation 라는 새 클래스를 추가 합니다. 이 클래스는 데이터베이스에 생성 되는 새 테이블을 나타냅니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

새 클래스에 대 한 DbSet 속성을 만들기 위해 users 컨텍스트 클래스에서 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

이제 새 테이블을 만들 준비가 되었습니다. 다음 시간에 패키지 관리자 콘솔을 다시 엽니다.

1. **Add Migration AddExtraUserInformation** 명령을 실행 합니다.
2. **Update-database** 명령을 실행 합니다.

이제 새 테이블이 데이터베이스에 있습니다.

## <a name="retrieve-the-additional-data"></a>추가 데이터 검색

추가 사용자 데이터를 검색 하는 방법에는 두 가지가 있습니다. 첫 번째 방법은 인증 요청 중에 기본적으로 다시 전달 되는 사용자 데이터를 유지 하는 것입니다. 두 번째 방법은 특히 공급자 API를 호출 하 고 자세한 정보를 요청 하는 것입니다. FullName 및 Link에 대 한 값은 Facebook에 의해 자동으로 다시 전달 됩니다. Facebook에서 Facebook API에 대 한 호출을 통해 계정이 검색 되었는지 여부를 나타내는 값입니다. 먼저 FullName 및 Link에 대 한 값을 채운 후 나중에 확인 된 값을 가져옵니다.

추가 사용자 데이터를 검색 하려면 **Controllers** 폴더에서 **AccountController.cs** 파일을 엽니다.

이 파일에는 계정을 로깅, 등록 및 관리 하는 논리가 포함 되어 있습니다. 특히 **ExternalLoginCallback** 및 **ExternalLoginConfirmation**라는 메서드를 확인 합니다. 이러한 메서드 내에서 코드를 추가 하 여 응용 프로그램에 대 한 외부 로그인 작업을 사용자 지정할 수 있습니다. **ExternalLoginCallback** 메서드의 첫 번째 줄에는 다음이 포함 됩니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

**Verifyauthentication** 메서드에서 반환 된 **Authenticationresult** 개체의 **ExtraData** 속성에 추가 사용자 데이터가 다시 전달 됩니다. Facebook 클라이언트는 **ExtraData** 속성에 다음과 같은 값을 포함 합니다.

- id
- name
- link
- gender
- accesstoken

ExtraData 속성에서 다른 공급자는 비슷하지만 약간 다른 데이터를 포함 합니다.

사용자가 사이트를 처음 사용 하는 경우 일부 추가 데이터를 검색 하 고 해당 데이터를 확인 보기에 전달 합니다. 메서드의 마지막 코드 블록은 사용자가 사이트를 처음 사용 하는 경우에만 실행 됩니다. 다음 줄을 바꿉니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

다음 줄로 바꿉니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

이러한 변경에는 FullName 및 Link 속성에 대 한 값만 포함 됩니다.

**ExternalLoginConfirmation** 메서드에서 아래 강조 표시 된 코드를 수정 하 여 추가 사용자 정보를 저장 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>뷰 조정

공급자에서 검색 하는 추가 사용자 데이터는 등록 페이지에 표시 됩니다.

**보기**/**계정** 폴더에서 **ExternalLoginConfirmation**을 엽니다. 사용자 이름에 대 한 기존 필드 아래에서 FullName, Link 및 Linklink에 대 한 필드를 추가 합니다.

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

이제 응용 프로그램을 실행 하 고 저장 된 추가 정보를 사용 하 여 새 사용자를 등록할 준비가 되었습니다. 사이트에 아직 등록 되지 않은 계정이 있어야 합니다. 다른 테스트 계정을 사용 하거나, 다시 사용 하려는 계정에 대 한\_**UserProfile** 및 **웹 페이지** 의 행을 삭제할 수 있습니다. 이러한 행을 삭제 하면 계정이 다시 등록 됩니다.

응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. 이번에는 확인 페이지에 더 많은 값이 포함 되어 있습니다.

![register](using-oauth-providers-with-mvc/_static/image12.png)

등록을 완료 한 후 브라우저를 닫습니다. 데이터베이스를 확인 하 여 **ExtraUserInformation** 테이블의 새 값을 확인 합니다.

## <a name="install-nuget-package-for-facebook-api"></a>Facebook API에 대 한 NuGet 패키지 설치

Facebook은 작업을 수행 하기 위해 호출할 수 있는 [API](https://developers.facebook.com/docs/reference/apis/) 를 제공 합니다. HTTP 요청을 전송 하거나 해당 요청을 쉽게 보낼 수 있도록 하는 NuGet 패키지 설치를 사용 하 여 Facebook API를 호출할 수 있습니다. NuGet 패키지를 사용 하는 방법은이 자습서에 나와 있지만 NuGet 패키지 설치는 필수적이 지 않습니다. 이 자습서에서는 Facebook C# SDK 패키지를 사용 하는 방법을 보여 줍니다. Facebook API 호출을 지 원하는 다른 NuGet 패키지가 있습니다.

**NuGet 패키지 관리** 창에서 Facebook C# SDK 패키지를 선택 합니다.

![패키지 설치](using-oauth-providers-with-mvc/_static/image13.png)

Facebook C# SDK를 사용 하 여 사용자에 대 한 액세스 토큰을 요구 하는 작업을 호출 합니다. 다음 섹션에서는 액세스 토큰을 가져오는 방법을 보여 줍니다.

## <a name="retrieve-access-token"></a>액세스 토큰 검색

대부분의 외부 공급자는 사용자의 자격 증명을 확인 한 후 액세스 토큰을 다시 전달 합니다. 이 액세스 토큰은 인증 된 사용자만 사용할 수 있는 작업을 호출할 수 있도록 하기 때문에 매우 중요 합니다. 따라서 더 많은 기능을 제공 하려는 경우 액세스 토큰을 검색 하 고 저장 하는 것이 중요 합니다.

외부 공급자에 따라 액세스 토큰은 제한 된 시간 동안만 유효 합니다. 유효한 액세스 토큰이 있는지 확인 하기 위해 사용자가 로그인 할 때마다 검색 하 여 데이터베이스에 저장 하지 않고 세션 값으로 저장할 수 있습니다.

**ExternalLoginCallback** 메서드에서 액세스 토큰은 **Authenticationresult** 개체의 **ExtraData** 속성에도 다시 전달 됩니다. 강조 표시 된 코드를 **ExternalLoginCallback** 에 추가 하 여 액세스 토큰을 **세션** 개체에 저장 합니다. 이 코드는 사용자가 Facebook 계정으로 로그인 할 때마다 실행 됩니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

이 예제에서는 Facebook에서 액세스 토큰을 검색 하지만 &quot;accesstoken&quot;라는 동일한 키를 통해 외부 공급자에서 액세스 토큰을 검색할 수 있습니다.

## <a name="logging-off"></a>로그오프 중

기본 **로그 오프** 메서드는 사용자를 응용 프로그램에서 로그 아웃 하지만 외부 공급자에서 사용자를 로그 아웃 하지 않습니다. 사용자를 Facebook에서 로그 오프 하 고 사용자가 로그 오프 한 후에도 토큰이 지속 되지 않도록 하려면 다음 강조 표시 된 코드를 AccountController의 **LogOff** 메서드에 추가 하면 됩니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

`next` 매개 변수에 제공 하는 값은 사용자가 Facebook에서 로그 아웃 한 후에 사용할 URL입니다. 로컬 컴퓨터에서 테스트 하는 경우 로컬 사이트에 올바른 포트 번호를 제공 합니다. 프로덕션 환경에서는 contoso.com와 같은 기본 페이지를 제공 합니다.

## <a name="retrieve-user-information-that-requires-the-access-token"></a>액세스 토큰이 필요한 사용자 정보를 검색 합니다.

액세스 토큰을 저장 하 고 Facebook C# SDK 패키지를 설치 했으므로 이제이를 함께 사용 하 여 facebook에서 추가 사용자 정보를 요청할 수 있습니다. **ExternalLoginConfirmation** 메서드에서 액세스 토큰의 값을 전달 하 여 **FacebookClient** 클래스의 인스턴스를 만듭니다. 현재 인증 된 사용자에 대해 **확인** 된 속성 값을 요청 합니다. **확인** 된 속성은 Facebook이 다른 방법 (예: 휴대폰으로 메시지 보내기)을 통해 계정의 유효성을 검사 했는지 여부를 나타냅니다. 이 값을 데이터베이스에 저장 합니다.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

사용자에 대 한 데이터베이스의 레코드를 삭제 하거나 다른 Facebook 계정을 사용 해야 합니다.

응용 프로그램을 실행 하 고 새 사용자를 등록 합니다. **ExtraUserInformation** 테이블을 확인 하 여 확인 된 속성의 값을 확인 합니다.

## <a name="conclusion"></a>결론

이 자습서에서는 사용자 인증 및 등록 데이터를 위해 Facebook과 통합 된 사이트를 만들었습니다. MVC 4 웹 응용 프로그램에 대해 설정 되는 기본 동작과 기본 동작을 사용자 지정 하는 방법을 배웠습니다.

## <a name="related-topics"></a>관련 항목

- [인증 및 SQL DB를 사용하여 ASP.NET MVC 앱을 만들고 Azure App Service에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
