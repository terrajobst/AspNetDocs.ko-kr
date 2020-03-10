---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: ASP.NET 웹 페이지 (Razor) 사이트에서 외부 사이트를 사용 하 여 로그인 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 기타 사이트 (즉,를 지 원하는 방법)를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518789"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 외부 사이트를 사용 하 여 로그인

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Facebook, Google, Twitter, Yahoo 및 기타 사이트 (즉, 사이트에서 OAuth 및 Openid connect를 지 원하는 방법)를 사용 하 여 ASP.NET 웹 페이지 (Razor) 사이트에 로그인 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - WebMatrix 시작 사이트 템플릿을 사용 하는 경우 다른 사이트에서 로그인을 사용 하도록 설정 하는 방법입니다.
> 
> 다음은이 문서에서 소개 하는 ASP.NET 기능입니다.
> 
> - `OAuthWebSecurity` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3

ASP.NET 웹 페이지에는 [OAuth](http://oauth.net/) 및 [openid connect](http://openid.net/) 공급자에 대 한 지원이 포함 됩니다. 이러한 공급자를 사용 하 여 사용자가 Facebook, Twitter, Microsoft 및 Google에서 기존 자격 증명을 사용 하 여 사이트에 로그인 하도록 할 수 있습니다. 예를 들어 Facebook 계정을 사용 하 여 로그인 하기 위해 사용자는 facebook 아이콘을 선택 하기만 하면 사용자 정보를 입력 하는 Facebook 로그인 페이지로 리디렉션됩니다. 그런 다음 Facebook 로그인을 사이트의 계정에 연결할 수 있습니다. 웹 페이지 멤버 자격 기능과 관련 하 여 향상 된 기능은 사용자가 여러 로그인 (소셜 네트워킹 사이트의 로그인 포함)을 웹 사이트의 단일 계정으로 연결할 수 있다는 것입니다.

이 이미지는 **시작 사이트** 템플릿의 로그인 페이지를 보여 줍니다. 여기서 사용자는 Facebook, Twitter, Google 또는 Microsoft 아이콘을 선택 하 여 외부 계정으로 로그인 할 수 있습니다.

![외부 공급자](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

**시작 사이트** 템플릿에서 몇 줄의 코드를 주석 처리 하 여 OAuth 및 openid connect 멤버 자격을 사용 하도록 설정할 수 있습니다. OAuth 및 Openid connect 공급자를 사용 하 여 작업 하는 데 사용 하는 메서드 및 속성은 `WebMatrix.Security.OAuthWebSecurity` 클래스에 있습니다. **시작 사이트** 템플릿에는 전체 멤버 자격 인프라, 로그인 페이지, 멤버 자격 데이터베이스 및 사용자가 로컬 자격 증명을 사용 하 여 사이트에 로그인 하거나 다른 사이트의 사용자가 로그인 할 수 있도록 하는 모든 코드가 포함 됩니다.

이 섹션에서는 사용자가 외부 사이트에서 **스타터 사이트** 템플릿을 기반으로 하는 사이트에 로그인 할 수 있도록 하는 방법에 대 한 예를 제공 합니다. 시작 사이트를 만든 후이 작업을 수행 합니다 (자세한 내용은 참조).

- OAuth 공급자 (Facebook, Twitter 및 Microsoft)를 사용 하는 사이트의 경우 외부 사이트에 응용 프로그램을 만듭니다. 이를 통해 해당 사이트에 대 한 로그인 기능을 호출 하기 위해 필요한 응용 프로그램 키를 제공 합니다.
- Google (Openid connect provider)을 사용 하는 사이트의 경우에는 응용 프로그램을 만들 필요가 없습니다. 이러한 모든 사이트에는 로그인 하 여 개발자 응용 프로그램을 만들기 위해 계정이 있어야 합니다.

    > [!NOTE]
    > Microsoft 응용 프로그램은 작동 하는 웹 사이트의 라이브 URL만 허용 하므로 로그인 테스트에는 로컬 웹 사이트 URL을 사용할 수 없습니다.
- 적절 한 인증 공급자를 지정 하 고 사용 하려는 사이트에 로그인을 제출 하기 위해 웹 사이트의 몇 가지 파일을 편집 합니다.

이 문서에서는 다음 작업에 대해 별도의 지침을 제공 합니다.

- [Google 로그인 사용](#To_enable_Google_logins)
- [Facebook 로그인 사용](#To_enable_Facebook_logins)
- [Twitter 로그인 사용](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Google 로그인 사용

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.
2. *\_AppStart* 페이지를 열고 다음 코드 줄의 주석 처리를 제거 합니다. 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>Google 로그인 테스트

1. 사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.
2. *로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Google** 또는 **Yahoo** 제출 단추를 선택 합니다. 이 예에서는 Google 로그인을 사용 합니다. 

    웹 페이지에서 요청을 Google 로그인 페이지로 리디렉션합니다.

    ![Google 로그인](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. 기존 Google 계정에 대 한 자격 증명을 입력 합니다.
4. *Localhost* 가 계정의 정보를 사용 하도록 허용할지 여부를 묻는 메시지가 표시 되 면 **허용**을 클릭 합니다.

    이 코드는 Google 토큰을 사용 하 여 사용자를 인증 한 다음 웹 사이트의이 페이지로 돌아갑니다. 이 페이지에서 사용자는 Google 로그인을 웹 사이트의 기존 계정과 연결 하거나, 사이트에 새 계정을 등록 하 여 외부 로그인을 연결할 수 있습니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. **연결** 단추를 선택 합니다. 브라우저는 응용 프로그램의 홈 페이지로 돌아갑니다.

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Facebook 로그인 사용

1. [Facebook 개발자 사이트로](https://developers.facebook.com/apps) 이동 합니다 (아직 로그인 하지 않은 경우 로그인).
2. 새 응용 프로그램 **만들기** 단추를 선택한 다음 프롬프트에 따라 새 응용 프로그램을 만들고 이름을 입력 합니다.
3. **앱이 Facebook과 통합 되는 방법 선택**섹션에서 **웹 사이트** 섹션을 선택 합니다.
4. 사이트 **url** 필드에 사이트 url을 입력 합니다 (예: `http://www.example.com`). **도메인** 필드는 선택 사항입니다. 이를 사용 하 여 전체 도메인 (예: *example.com*)에 대 한 인증을 제공할 수 있습니다. 

    > [!NOTE]
    > `http://localhost:12345`와 같은 URL (로컬 포트 번호)을 사용 하 여 로컬 컴퓨터에서 사이트를 실행 하는 경우 사이트를 테스트 하기 위해 **사이트 url** 필드에이 값을 추가할 수 있습니다. 그러나 로컬 사이트의 포트 번호가 변경 될 때마다 응용 프로그램의 **사이트 URL** 필드를 업데이트 해야 합니다.
5. **변경 내용 저장** 단추를 선택 합니다.
6. **앱** 탭을 다시 선택 하 고 응용 프로그램의 시작 페이지를 확인 합니다.
7. 응용 프로그램에 대 한 **앱 ID** 및 **앱 암호** 값을 복사 하 여 임시 텍스트 파일에 붙여 넣습니다. 웹 사이트 코드의 Facebook 공급자에 이러한 값을 전달 합니다.
8. Facebook 개발자 사이트를 종료 합니다.

이제 사용자가 Facebook 계정을 사용 하 여 사이트에 로그인 할 수 있도록 웹 사이트의 두 페이지를 변경 합니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.
2. *\_AppStart* 페이지를 열고 Facebook OAuth 공급자에 대 한 코드의 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. Facebook 응용 프로그램에서 `appId` 매개 변수 값 (따옴표 내)으로 **앱 ID** 값을 복사 합니다.
4. Facebook 응용 프로그램에서 `appSecret` 매개 변수 값으로 **앱 비밀** 값을 복사 합니다.
5. 파일을 저장하고 닫습니다.

### <a name="testing-facebook-login"></a>Facebook 로그인 테스트

1. 사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.
2. *로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Facebook** 아이콘을 선택 합니다. 

    웹 페이지에서 요청을 Facebook 로그인 페이지로 리디렉션합니다.

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Facebook 계정에 로그인 합니다. 

    이 코드는 Facebook 토큰을 사용 하 여 사용자를 인증 한 다음 Facebook 로그인을 사이트 로그인에 연결할 수 있는 페이지로 돌아갑니다. 사용자 이름 또는 전자 메일 주소가 양식의 **전자 메일** 필드에 채워집니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. **연결** 단추를 선택 합니다. 

    브라우저가 홈 페이지로 반환 되 고 로그인 됩니다.

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Twitter 로그인 사용

1. [Twitter 개발자 사이트로](https://dev.twitter.com/)이동 합니다.
2. **앱 만들기** 링크를 선택 하 고 사이트에 로그인 합니다.
3. **응용 프로그램 만들기** 양식에서 **이름** 및 **설명** 필드를 입력 합니다.
4. **웹** 사이트 필드에 사이트의 URL을 입력 합니다 (예: `http://www.example.com`). 

    > [!NOTE]
    > `http://localhost:12345`같은 URL을 사용 하 여 사이트를 로컬로 테스트 하는 경우 Twitter에서 URL을 허용 하지 않을 수 있습니다. 그러나 로컬 루프백 IP 주소를 사용할 수 있습니다 (예: `http://127.0.0.1:12345`). 이렇게 하면 응용 프로그램을 로컬로 테스트 하는 프로세스가 간단해 집니다. 그러나 로컬 사이트의 포트 번호가 변경 될 때마다 응용 프로그램의 **웹 사이트** 필드를 업데이트 해야 합니다.
5. 사용자가 Twitter에 로그인 한 후 사용자가 반환할 웹 사이트의 페이지에 대 한 URL을 **콜백 url** 필드에 입력 합니다. 예를 들어 로그인 상태를 인식 하는 시작 사이트의 홈 페이지로 사용자를 보내려면 **웹 사이트** 필드에 입력 한 것과 동일한 URL을 입력 합니다.
6. 조건에 동의 하 고 **Twitter 응용 프로그램 만들기** 단추를 선택 합니다.
7. **내 응용** 프로그램 방문 페이지에서 사용자가 만든 응용 프로그램을 선택 합니다.
8. **세부 정보** 탭에서 아래쪽으로 스크롤하고 **내 액세스 토큰 만들기** 단추를 선택 합니다.
9. **세부 정보** 탭에서 응용 프로그램에 대 한 **소비자 키** 및 **소비자 암호** 값을 복사 하 여 임시 텍스트 파일에 붙여 넣습니다. 웹 사이트 코드의 Twitter 공급자에 이러한 값을 전달 합니다.
10. Twitter 사이트를 종료 합니다.

이제 사용자가 Twitter 계정을 사용 하 여 사이트에 로그인 할 수 있도록 웹 사이트의 두 페이지를 변경 합니다.

1. WebMatrix 시작 사이트 템플릿을 기반으로 하는 ASP.NET 웹 페이지 사이트를 만들거나 엽니다.
2. *\_AppStart* 페이지를 열고 Twitter OAuth 공급자에 대 한 코드의 주석 처리를 제거 합니다. 주석 처리가 제거 코드 블록은 다음과 같습니다. 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. Twitter 응용 프로그램의 **소비자 키** 값을 따옴표 안에 있는 `consumerKey` 매개 변수의 값으로 복사 합니다.
4. Twitter 응용 프로그램의 **소비자 암호** 값을 `consumerSecret` 매개 변수의 값으로 복사 합니다.
5. 파일을 저장하고 닫습니다.

### <a name="testing-twitter-login"></a>Twitter 로그인 테스트

1. 사이트의 *기본값. cshtml* 페이지를 실행 하 고 **로그인** 단추를 선택 합니다.
2. *로그인* 페이지의 **다른 서비스를 사용 하 여** 로그인 섹션에서 **Twitter** 아이콘을 선택 합니다. 

    웹 페이지에서 사용자가 만든 응용 프로그램에 대 한 Twitter 로그인 페이지로 요청이 리디렉션됩니다.

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Twitter 계정에 로그인 합니다.
4. 이 코드는 Twitter 토큰을 사용 하 여 사용자를 인증 한 다음 로그인을 웹 사이트 계정에 연결할 수 있는 페이지로 돌아갑니다. 이름 또는 전자 메일 주소는 양식의 **전자 메일** 필드에 입력 됩니다.

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. **연결** 단추를 선택 합니다. 

    브라우저가 홈 페이지로 반환 되 고 로그인 됩니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ASP.NET 웹 페이지 사이트에 보안 및 멤버 자격 추가](https://go.microsoft.com/fwlink/?LinkID=202904)
