---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: 비어 있거나 기존 Web Forms 프로젝트에 ASP.NET Identity 추가-ASP.NET 4.x
author: raquelsa
description: 이 자습서에서는 ASP.NET 응용 프로그램에 ASP.NET Identity (ASP.NET에 대 한 멤버 자격 시스템)를 추가 하는 방법을 보여 줍니다. 새 Web Forms 또는 MVC를 만들 때 ...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471977"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>비어 있는 또는 기존 Web Forms 프로젝트에 ASP.NET Identity 추가

> 이 자습서에서는 ASP.NET 응용 프로그램에 [ASP.NET Identity](introduction-to-aspnet-identity.md) (ASP.NET에 대 한 새 멤버 자격 시스템)를 추가 하는 방법을 보여 줍니다.
> 
> 개별 계정으로 Visual Studio 2017 RTM에서 새 Web Forms 또는 MVC 프로젝트를 만들 때 Visual Studio는 필요한 모든 패키지를 설치 하 고 필요한 모든 클래스를 추가 합니다. 이 자습서에서는 기존 Web Forms 프로젝트 또는 새 빈 프로젝트에 ASP.NET Identity 지원을 추가 하는 단계를 설명 합니다. 설치 해야 하는 모든 NuGet 패키지와 추가 해야 하는 클래스에 대해 간략하게 설명 합니다. 사용자 관리 및 인증에 대 한 모든 주요 진입점 Api를 강조 표시 하는 동시에 새 사용자를 등록 하 고 로그인 하는 샘플 Web Forms에 대해 자세히 살펴보겠습니다. 이 샘플에서는 Entity Framework를 기반으로 하는 SQL 데이터 저장소에 대 한 ASP.NET Identity 기본 구현을 사용 합니다. 이 자습서에서는 SQL database에 대해 LocalDB를 사용 합니다.
> 

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity 시작

1. [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)을 설치 하 고 실행 하 여 시작 합니다.
2. 시작 페이지에서 **새 프로젝트** 를 선택 하거나 메뉴를 사용 하 여 **파일**, **새 프로젝트**를 차례로 선택 합니다.
3. 왼쪽 창에서 **시각적 개체 C#** 를 확장 한 다음 **웹**, **ASP.NET 웹 응용 프로그램 (.net Framework)** 을 차례로 선택 합니다. 프로젝트 이름을 "WebFormsIdentity"로 선택 하 고 **확인을**선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. **새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   **인증 변경** 단추를 사용할 수 없으며이 템플릿에 인증 지원이 제공 되지 않습니다. Web Forms, MVC 및 Web API 템플릿을 사용 하 여 인증 방법을 선택할 수 있습니다.

## <a name="add-identity-packages-to-your-app"></a>앱에 Id 패키지 추가

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다. **Microsoft. n.** n e t. n e t. n e t. 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
이 패키지는 종속성 패키지를 설치 합니다. **Entityframework** 및 **Microsoft ASP.NET Identity Core**를 참조 하세요.

## <a name="add-a-web-form-to-register-users"></a>사용자를 등록 하는 웹 양식 추가

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **Web Form**을 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. **항목 이름 지정** 대화 상자에서 새 **웹 폼의**이름을 지정 하 고 **확인** 을 선택 합니다.
3. 생성 된 *Register .aspx* 파일의 태그를 아래 코드로 바꿉니다. 코드 변경 내용은 강조 표시되어 있습니다. 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > 이는 새 ASP.NET Web Forms 프로젝트를 만들 때 생성 되는 간단한 버전의 *Register .aspx* 파일 일 뿐입니다. 위의 태그는 양식 필드와 새 사용자를 등록 하는 단추를 추가 합니다.
4. *Register.aspx.cs* 파일을 열고 파일의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. 위의 코드는 새 ASP.NET Web Forms 프로젝트를 만들 때 생성 되는 *Register.aspx.cs* 파일의 단순화 된 버전입니다.
    > 2. *IdentityUser* 클래스는 *IUser* 인터페이스의 기본 entityframework 구현입니다. *IUser* 인터페이스는 ASP.NET Identity Core의 사용자에 대 한 최소 인터페이스입니다.
    > 3. *Userstore* 클래스는 사용자 저장소의 기본 entityframework 구현입니다. 이 클래스는 ASP.NET Identity Core의 최소 인터페이스인 *Iuserstore*, *IUserLoginStore*, *Iuserclaimstore* 및 *iuserrolestore*를 구현 합니다.
    > 4. *Usermanager* 클래스는 *usermanager*에 변경 내용을 자동으로 저장 하는 사용자 관련 api를 노출 합니다.
    > 5. *IdentityResult* 클래스는 id 작업의 결과를 나타냅니다.
5. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택 하 고, **ASP.NET 폴더를 추가** 하 고, **앱\_데이터**를 추가 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. *Web.config* 파일을 열고 사용자 정보를 저장 하는 데 사용할 데이터베이스에 대 한 연결 문자열 항목을 추가 합니다. 데이터베이스는 Id 엔터티에 대 한 EntityFramework로 런타임에 생성 됩니다. 연결 문자열은 새 Web Forms 프로젝트를 만들 때 만든 것과 비슷합니다. 강조 표시 된 코드는 추가 해야 하는 태그를 보여 줍니다.

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > Visual Studio 2015 이상에서는 `(localdb)\v11.0`을 연결 문자열의 `(localdb)\MSSQLLocalDB`으로 바꿉니다.
    
7. 프로젝트에서 파일 *등록 .aspx* 을 마우스 오른쪽 단추로 클릭 하 고 **시작 페이지로 설정**을 선택 합니다. Ctrl + f 5를 눌러 웹 응용 프로그램을 빌드하고 실행 합니다. 새 사용자 이름 및 암호를 입력 한 다음 **등록**을 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity 유효성 검사를 지원 하며이 샘플에서는 Id 코어 패키지에서 제공 되는 사용자 및 암호 유효성 검사기의 기본 동작을 확인할 수 있습니다. 사용자 (`UserValidator`)에 대 한 기본 유효성 검사기에는 기본 값이 `true`로 설정 된 속성 `AllowOnlyAlphanumericUserNames` 있습니다. 암호에 대 한 기본 유효성 검사기 (`MinimumLengthValidator`)는 암호의 6 자 이상이 되도록 합니다. 이러한 유효성 검사기는 사용자 지정 유효성 검사를 수행 하려는 경우 재정의할 수 있는 `UserManager`의 속성입니다.

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>Entity Framework에서 생성 된 LocalDb Id 데이터베이스 및 테이블을 확인 합니다.

1. **보기** 메뉴에서 **서버 탐색기**를 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. **Defaultconnection (WebFormsIdentity)** 을 확장 하 고 **테이블**을 확장 한 다음 **AspNetUsers** 를 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>OWIN 인증을 위한 응용 프로그램 구성

이 시점에서 사용자 만들기에 대 한 지원도 추가 되었습니다. 이제 인증을 추가 하 여 사용자를 로그인 하는 방법을 설명 하겠습니다. ASP.NET Identity는 폼 인증을 위해 Microsoft OWIN Authentication 미들웨어를 사용 합니다. OWIN 쿠키 인증은 [OWIN](https://msdn.microsoft.com/magazine/dn451439.aspx) 또는 IIS에서 호스트 되는 프레임 워크에서 사용할 수 있는 쿠키 및 클레임 기반 인증 메커니즘입니다. 이 모델에서는 ASP.NET MVC 및 Web Forms을 포함 하 여 여러 프레임 워크에서 동일한 인증 패키지를 사용할 수 있습니다. 프로젝트 Katana에 대 한 자세한 내용과 호스트에서 미들웨어를 실행 하는 방법에 대 한 자세한 내용은 [Katana 프로젝트 시작](https://msdn.microsoft.com/magazine/dn451439.aspx)을 참조 하세요.

## <a name="install-authentication-packages-to-your-application"></a>응용 프로그램에 인증 패키지 설치

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다. ***Owin*** 패키지를 검색 하 고 설치 합니다. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. ***Owin 웹*** 패키지를 검색 하 고 설치 합니다.

    > [!NOTE]
    > **Owin** 패키지에는 ASP.NET Identity Core 패키지에서 사용 되는 Owin authentication 미들웨어를 관리 하 고 구성 하는 Owin 확장 클래스 집합이 포함 되어 있습니다.
    > **Owin 웹** 패키지에는 ASP.NET request 파이프라인을 사용 하 여 IIS에서 Owin 기반 응용 프로그램을 실행할 수 있도록 하는 Owin 서버가 포함 되어 있습니다. 자세한 내용은 [OWIN 미들웨어에서 IIS 통합 파이프라인](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md)을 참조 하세요.

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>OWIN 시작 및 인증 구성 클래스 추가

1. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목 추가**를 선택 합니다. 검색 텍스트 상자 대화 상자에서 "*owin*"를 입력 합니다. 클래스 이름을 "*Startup*"으로 선택 하 고 **추가**를 선택 합니다. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. Startup.cs 파일에서 아래에 표시 된 강조 표시 된 코드를 추가 하 여 OWIN 쿠키 인증을 구성 합니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > 이 클래스는 OWIN 시작 클래스를 지정 하기 위한 `OwinStartup` 특성을 포함 합니다. 모든 OWIN 응용 프로그램에는 응용 프로그램 파이프라인에 대 한 구성 요소를 지정 하는 startup 클래스가 있습니다. 이 모델에 대 한 자세한 내용은 [OWIN 시작 클래스 검색](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) 을 참조 하세요.

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>사용자 등록 및 로그인을 위한 web forms 추가

1. *Register.aspx.cs* 파일을 열고 등록이 성공 하면 사용자에 게 로그인 하는 다음 코드를 추가 합니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - ASP.NET Identity 및 OWIN 쿠키 인증은 클레임 기반 시스템 이므로 프레임 워크를 사용 하려면 앱 개발자가 사용자에 대 한 [ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) 를 생성 해야 합니다. ClaimsIdentity에는 사용자가 속한 역할과 같은 사용자의 모든 클레임에 대 한 정보가 있습니다. 이 단계에서 사용자에 게 더 많은 클레임을 추가할 수도 있습니다.
    > - AuthenticationManager에서 OWIN를 사용 하 고 `SignIn`를 호출 하 고 위와 같이 ClaimsIdentity를 전달 하 여 사용자에 게 로그인 할 수 있습니다. 이 코드는 사용자를 로그인 하 고 쿠키도 생성 합니다. 이 호출은 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈에서 사용 하는 [FormAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 와 유사 합니다.
2. **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **Web Form**을 선택 합니다. 웹 폼 **로그인**의 이름을로 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. *Login.aspx* 파일의 내용을 다음 코드로 바꿉니다.

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. *Login.aspx.cs* 파일의 내용을 다음으로 바꿉니다.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` 현재 사용자의 상태를 확인 하 고 `Context.User.Identity.IsAuthenticated` 상태에 따라 조치를 취합니다.
    >   **로그인 한 사용자 이름 표시** : Microsoft ASP.NET Identity Framework는 로그인 한 사용자에 대 한 `UserName` 및 `UserId`를 가져올 수 있는 [IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) 에 확장 메서드를 추가 했습니다. 이러한 확장 메서드는 `Microsoft.AspNet.Identity.Core` 어셈블리에서 정의 됩니다. 이러한 확장 메서드는 [HttpContext.User.Identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) 에 대 한 대체 메서드입니다.
    > - SignIn method: `This` 메서드는이 샘플의 이전 `CreateUser_Click` 메서드를 대체 하 고 사용자를 성공적으로 만든 후 사용자에 게 로그인 합니다.   
    >   Microsoft OWIN Framework는 `IOwinContext`에 대 한 참조를 가져올 수 있는 `System.Web.HttpContext`에 확장 메서드를 추가 했습니다. 이러한 확장 메서드는 `Microsoft.Owin.Host.SystemWeb` 어셈블리에서 정의 됩니다. `OwinContext` 클래스는 현재 요청에서 사용 가능한 인증 미들웨어 기능을 나타내는 `IAuthenticationManager` 속성을 노출 합니다. OWIN에서 `AuthenticationManager`를 사용 하 고 `SignIn`를 호출 하 고 위와 같이 `ClaimsIdentity`를 전달 하 여 사용자를 로그인 할 수 있습니다. ASP.NET Identity 및 OWIN 쿠키 인증은 클레임 기반 시스템 이므로 프레임 워크를 사용 하려면 앱에서 사용자에 대 한 `ClaimsIdentity`을 생성 해야 합니다. `ClaimsIdentity`에는 사용자가 속한 역할 등 사용자에 대 한 모든 클레임에 대 한 정보가 있습니다. 이 단계에서 사용자에 대 한 클레임을 더 추가할 수도 있습니다 .이 코드는 사용자에 게 로그인 하 고 쿠키도 생성 합니다. 이 호출은 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈에서 사용 하는 [FormAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) 와 유사 합니다.
    > - `SignOut` method: OWIN에서 `AuthenticationManager`에 대 한 참조를 가져오고 `SignOut`를 호출 합니다. 이는 [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) 모듈에서 사용 하는 [SignOut 메서드와 FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) 유사 합니다.
5. **Ctrl +** f 5를 눌러 웹 응용 프로그램을 빌드하고 실행 합니다. 새 사용자 이름 및 암호를 입력 한 다음 **등록**을 선택 합니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   참고: 이제 새 사용자가 만들어지고 로그인 됩니다.
6. **로그 아웃** 단추를 선택 합니다. 로그인 폼으로 리디렉션됩니다.
7. 잘못 된 사용자 이름 또는 암호를 입력 하 고 **로그인** 단추를 선택 합니다. 
   `UserManager.Find` 메서드는 null을 반환 하 고 오류 메시지를 표시 합니다. " *잘못 된 사용자 이름 또는 암호* "가 표시 됩니다.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)
