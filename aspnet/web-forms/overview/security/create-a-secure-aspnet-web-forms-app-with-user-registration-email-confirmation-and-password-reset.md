---
uid: web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
title: 사용자 등록, 전자 메일 확인 및 암호 재설정 (C#)을 사용 하 여 보안 ASP.NET Web Forms 앱 만들기 | Microsoft Docs
author: Erikre
description: 이 자습서에서는 ASP.NET Identity 멤버를 사용 하 여 사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 0a8d6044-5fab-4213-82d6-5618d5601358
msc.legacyurl: /web-forms/overview/security/create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset
msc.type: authoredcontent
ms.openlocfilehash: af3653bc164810126bc3bf8f1b1794d75642d807
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507131"
---
# <a name="create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset-c"></a>사용자 등록, 전자 메일 확인 및 암호 재설정 기능이 있는 보안 ASP.NET Web Forms 앱 만들기(C#)

[Erik Reitan](https://github.com/Erikre)

> 이 자습서에서는 ASP.NET Identity 멤버 자격 시스템을 사용 하 여 사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 ASP.NET Web Forms 앱을 빌드하는 방법을 보여 줍니다. 이 자습서는 Rick Anderson의 [MVC 자습서](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)를 기반으로 합니다.

## <a name="introduction"></a>소개

이 자습서에서는 Visual Studio 및 ASP.NET 4.5를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만들고 사용자 등록, 전자 메일 확인 및 암호 재설정을 사용 하 여 보안 Web Forms 앱을 만드는 데 필요한 단계를 안내 합니다.

### <a name="tutorial-tasks-and-information"></a>자습서 작업 및 정보:

- [ASP.NET Web Forms 앱 만들기](#createWebForms)
- [SendGrid 후크](#SG)
- [로그인 하기 전에 전자 메일 확인 필요](#require)
- [암호 복구 및 다시 설정](#reset)
- [전자 메일 다시 보내기 확인 링크](#rsend)
- [앱 문제 해결](#dbg)
- [추가 리소스](#addRes)

<a id="createWebForms"></a>
## <a name="create-an-aspnet-web-forms-app"></a>ASP.NET Web Forms 앱 만들기

웹 또는 [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) [에 대해 Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 을 설치 하 고 실행 하 여 시작 합니다. [업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 Visual Studio 2013.

> [!NOTE]
> 경고:이 자습서를 완료 하려면 [Visual Studio 2013 업데이트 3](https://go.microsoft.com/fwlink/?LinkId=390465) 이상을 설치 해야 합니다.

1. 새 프로젝트 ( **새**프로젝트 &gt; -**파일** )를 만들고 **새 프로젝트** 대화 상자에서 **ASP.NET 웹 응용 프로그램** 템플릿 및 최신 .NET Framework 버전을 선택 합니다.
2. **새 ASP.NET 프로젝트** 대화 상자에서 **Web Forms** 템플릿을 선택 합니다. 기본 인증을 **개별 사용자 계정**으로 그대로 둡니다. Azure에서 앱을 호스팅하려면 **클라우드의 호스트** 확인란을 선택 된 상태로 둡니다.   
 그런 다음 **확인** 을 클릭 하 여 새 프로젝트를 만듭니다.  
    ![새 ASP.NET 프로젝트 대화 상자](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image1.png)
3. 프로젝트에 대해 SSL(Secure Sockets Layer) (SSL)을 사용 하도록 설정 합니다. [시작 Web Forms 자습서 시리즈](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)의 **프로젝트에 대해 SSL 사용** 섹션에서 사용할 수 있는 단계를 따릅니다.
4. 앱을 실행 하 고 **등록** 링크를 클릭 한 다음 새 사용자를 등록 합니다. 이 시점에서 전자 메일에 대 한 유효성 검사는 [[EmailAddress]](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx) 특성을 기반으로 하 여 전자 메일 주소의 형식이 올바른지 확인 합니다. 전자 메일 확인을 추가 하는 코드를 수정 합니다. 브라우저 창을 닫습니다.
5. Visual Studio **서버 탐색기** ( -&gt; **서버 탐색기** **보기** )에서 **데이터 Connections\DefaultConnection\Tables\AspNetUsers**로 이동 하 고 마우스 오른쪽 단추를 클릭 한 다음 **테이블 정의 열기**를 선택 합니다. 

    다음 그림은 `AspNetUsers` 테이블 스키마를 보여 줍니다.

    ![AspNetUsers 테이블 스키마](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image2.png)
6. **서버 탐색기**에서 **AspNetUsers** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시**를 선택 합니다.  
  
    ![AspNetUsers 테이블 데이터](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image3.png)  
 이 시점에서 등록 된 사용자에 대 한 전자 메일이 확인 되지 않았습니다.
7. 행을 클릭 하 고 삭제를 선택 하 여 사용자를 삭제 합니다. 다음 단계에서이 전자 메일을 다시 추가 하 고 전자 메일 주소로 확인 메시지를 보냅니다.

## <a name="email-confirmation"></a>전자 메일 확인

새 사용자를 등록 하는 동안 전자 메일을 확인 하 여 다른 사용자를 가장 하지 않았는지 확인 하는 것이 좋습니다. 즉, 다른 사용자의 전자 메일을 사용 하 여 등록 하지 않은 것입니다. 토론 포럼이 있다고 가정 하면 `"bob@cpandl.com"` `"joe@contoso.com"`등록 하지 않도록 합니다. 전자 메일 확인 없이 앱에서 원치 않는 전자 메일을 받을 수 `"joe@contoso.com"`. Bob이 실수로 `"bib@cpandl.com"`로 등록 했다고 가정 하면 앱이 올바른 전자 메일을가지고 있지 않기 때문에 암호 복구를 사용할 수 없습니다. 전자 메일 확인은 봇의 제한 된 보호만 제공 하며, 결정 된 스팸 메일을 보호 하지 않습니다.

일반적으로 새 사용자가 전자 메일, SMS 문자 메시지 또는 다른 메커니즘으로 확인 되기 전에 데이터를 웹 사이트에 게시 하는 것을 방지 하려고 합니다. 아래 섹션에서는 전자 메일 확인을 사용 하도록 설정 하 고 코드를 수정 하 여 새로 등록 된 사용자가 전자 메일을 확인 한 후에 로그인 하지 않도록 합니다. 이 자습서에서는 전자 메일 서비스 SendGrid를 사용 합니다.

<a id="SG"></a>
## <a name="hook-up-sendgrid"></a>SendGrid 후크

이 자습서를 작성 했으므로 SendGrid에서 API를 변경 했습니다. 현재 SendGrid 지침은 [SendGrid](http://sendgrid.com/) 또는 [계정 확인 및 암호 복구 사용](xref:security/authentication/accconfirm#enable-account-confirmation-and-password-recovery)을 참조 하세요.

이 자습서에서는 [SendGrid](http://sendgrid.com/)를 통해 전자 메일 알림을 추가 하는 방법을 보여 주지만 SMTP 및 기타 메커니즘을 사용 하 여 전자 메일을 보낼 수 있습니다 ( [추가 리소스](#addRes)참조).

1. Visual Studio에서 **패키지 관리자 콘솔** (**도구** -&gt; **NuGet 패키지** 관리자 -&gt; **패키지 관리자 콘솔**)을 열고 다음 명령을 입력 합니다.  
    `Install-Package SendGrid`
2. [Azure SendGrid 등록 페이지로](https://azure.microsoft.com/gallery/store/sendgrid/sendgrid-azure/) 이동 하 여 무료 SendGrid 계정에 등록 합니다. [SendGrid의 사이트](http://www.sendgrid.com)에서 직접 무료 SendGrid 계정을 등록할 수도 있습니다.
3. **솔루션 탐색기** 에서 *앱\_시작* 폴더에 있는 *IdentityConfig.cs* 파일을 열고 노란색으로 강조 표시 된 다음 코드를 `EmailService` 클래스에 추가 하 여 **SendGrid**를 구성 합니다.

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample1.cs?highlight=3,5,8-37)]
4. 또한 *IdentityConfig.cs* 파일의 시작 부분에 다음 `using` 문을 추가 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample2.cs?highlight=1-4)]
5. 이 샘플을 간단 하 게 유지 하기 위해 *web.config 파일의* `appSettings` 섹션에 전자 메일 서비스 계정 값을 저장 합니다. 노란색으로 강조 표시 된 다음 XML을 프로젝트의 루트에 있는 *web.config* 파일에 추가 합니다.

    [!code-xml[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample3.xml?highlight=2-5)]

    > [!WARNING]
    > 보안-중요 한 데이터를 소스 코드에 저장 하지 않습니다. 이 예제에서 계정과 자격 증명은 *web.config 파일의* **appSetting** 섹션에 저장 됩니다. Azure에서 Azure Portal의 **[구성](https://blogs.msdn.com/b/webdev/archive/2014/06/04/queuebackgroundworkitem-to-reliably-schedule-and-run-long-background-process-in-asp-net.aspx)** 탭에서 이러한 값을 안전 하 게 저장할 수 있습니다. 관련 정보는 [ASP.NET 및 Azure에 암호 및 기타 중요 한 데이터를 배포 하기 위한 모범 사례](https://go.microsoft.com/fwlink/?LinkId=513141)Rick Anderson의 항목을 참조 하세요.
6. 앱에서 전자 메일을 보낼 수 있도록 SendGrid 인증 값 (사용자 이름 및 암호)을 반영 하는 전자 메일 서비스 값을 추가 합니다. SendGrid에서 제공한 이메일 주소 대신 SendGrid 계정 이름을 사용 해야 합니다.

### <a name="enable-email-confirmation"></a>전자 메일 확인 사용

 전자 메일 확인을 사용 하도록 설정 하려면 다음 단계를 사용 하 여 등록 코드를 수정 합니다.  

1. *계정* 폴더에서 *Register.aspx.cs* 코드 숨김으로 열고 `CreateUser_Click` 메서드를 업데이트 하 여 다음과 같이 강조 표시 된 변경 내용을 사용 하도록 설정 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample4.cs?highlight=9-11)]
2. **솔루션 탐색기**에서 default.aspx를 마우스 오른쪽 *단추로 클릭 하* 고 **시작 페이지로 설정**을 선택 합니다.
3. F5 키를 눌러 앱을 실행 합니다 **.** 페이지가 표시 되 면 **등록** 링크를 클릭 하 여 등록 페이지를 표시 합니다.
4. 전자 메일 및 암호를 입력 한 다음 **등록** 단추를 클릭 하 여 SendGrid를 통해 전자 메일 메시지를 보냅니다.  
   프로젝트 및 코드의 현재 상태는 사용자가 자신의 계정을 확인 하지 않은 경우에도 등록 양식을 완료 한 후 로그인 할 수 있도록 합니다.
5. 전자 메일 계정을 확인 하 고 링크를 클릭 하 여 전자 메일을 확인 합니다.  
   등록 양식을 제출 하면 로그인 됩니다.  
    ![샘플 웹 사이트-로그인](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/_static/image4.png)

<a id="require"></a>
## <a name="require-email-confirmation-before-log-in"></a>로그인 하기 전에 전자 메일 확인 필요

전자 메일 계정을 확인 했지만이 시점에서 확인 전자 메일에 포함 된 링크를 클릭 하 여 완전히 로그인 할 필요가 없습니다. 다음 섹션에서는 새 사용자가 로그인 (인증 됨) 전에 확인 된 전자 메일을 포함 하도록 요구 하는 코드를 수정 합니다.

1. Visual Studio **솔루션 탐색기** 에서 *계정* 폴더에 포함 된 *Register.aspx.cs* 코드 숨김으로 `CreateUser_Click` 이벤트를 다음과 같이 강조 표시 된 변경 내용으로 업데이트 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample5.cs?highlight=13-14,17-21)]
2. *Login.aspx.cs* 코드 숨김으로 표시 된 다음 변경 내용으로 `LogIn` 메서드를 업데이트 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample6.cs?highlight=9-19,45-46)]

### <a name="run-the-application"></a>애플리케이션 실행

 사용자의 전자 메일 주소가 확인 되었는지 여부를 확인 하는 코드를 구현 했으므로 이제 **등록** 및 **로그인** 페이지에서 기능을 확인할 수 있습니다. 

1. **AspNetUsers** 테이블에서 테스트 하려는 전자 메일 별칭이 포함 된 계정을 삭제 합니다.
2. 앱 (**F5**)을 실행 하 고 전자 메일 주소를 확인 하기 전 까지는 사용자로 등록할 수 없는지 확인 합니다.
3. 방금 보낸 전자 메일을 통해 새 계정을 확인 하기 전에 새 계정을 사용 하 여 로그인을 시도 합니다.  
 로그인 할 수 없고 확인 된 전자 메일 계정이 있어야 합니다.
4. 전자 메일 주소를 확인 한 후 앱에 로그인 합니다.

<a id="reset"></a>
## <a name="password-recovery-and-reset"></a>암호 복구 및 다시 설정

1. Visual Studio에서 다음과 같이 메서드를 표시 하도록 *Account* 폴더에 포함 된 *Forgot.aspx.cs* 코드 숨김으로 표시 된 `Forgot` 메서드에서 주석 문자를 제거 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample7.cs?highlight=16-18)]
2. *Login.aspx* 페이지를 엽니다. **Loginform** 섹션의 끝 부분에 있는 태그를 아래 강조 표시 된 대로 바꿉니다. 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample8.aspx?highlight=52-53)]
3. *Login.aspx.cs* 코드를 열고 `Page_Load` 이벤트 처리기에서 노란색으로 강조 표시 된 다음 코드 줄의 주석 처리를 제거 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample9.cs?highlight=5)]
4. F5 키를 눌러 앱을 실행 합니다 **.** 페이지가 표시 되 면 **로그인** 링크를 클릭 합니다.
5. 암호를 **잊으셨나요?** 링크를 클릭 하 여 **암호 찾기** 페이지를 표시 합니다.
6. 전자 메일 주소를 입력 하 고 **제출** 단추를 클릭 하 여 암호를 재설정 하는 데 사용할 수 있는 전자 메일을 주소로 보냅니다.   
   전자 메일 계정을 확인 하 고 링크를 클릭 하 여 **암호 재설정** 페이지를 표시 합니다.
7. **암호 재설정** 페이지에서 전자 메일, 암호 및 확인 된 암호를 입력 합니다. 그런 다음 **다시 설정** 단추를 누릅니다.  
   암호를 성공적으로 다시 설정 하면 **암호 변경 됨** 페이지가 표시 됩니다. 이제 새 암호로 로그인 할 수 있습니다.

<a id="rsend"></a>
## <a name="resend-email-confirmation-link"></a>전자 메일 다시 보내기 확인 링크

사용자가 새 로컬 계정을 만들면 로그온 하기 전에 사용 해야 하는 확인 링크를 전자 메일로 보낼 수 있습니다. 사용자가 실수로 확인 전자 메일을 삭제 하거나 전자 메일이 도착 하지 않은 경우 확인 링크를 다시 전송 해야 합니다. 다음 코드 변경 내용에서는이를 사용 하도록 설정 하는 방법을 보여 줍니다.

1. Visual Studio에서 **Login.aspx.cs** 코드를 열고 `LogIn` 이벤트 처리기 뒤에 다음 이벤트 처리기를 추가 합니다.   

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample10.cs)]
2. 노란색으로 강조 표시 된 코드를 다음과 같이 변경 하 여 *Login.aspx.cs* 코드 숨김으로 `LogIn` 이벤트 처리기를 수정 합니다. 

    [!code-csharp[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample11.cs?highlight=15-17)]
3. 다음과 같이 노란색으로 강조 표시 된 코드를 추가 하 여 login.aspx 페이지를 업데이트 *합니다* . 

    [!code-aspx[Main](create-a-secure-aspnet-web-forms-app-with-user-registration-email-confirmation-and-password-reset/samples/sample12.aspx?highlight=45-46)]
4. **AspNetUsers** 테이블에서 테스트 하려는 전자 메일 별칭이 포함 된 계정을 삭제 합니다.
5. 앱 (**F5**)을 실행 하 고 전자 메일 주소를 등록 합니다.
6. 방금 보낸 전자 메일을 통해 새 계정을 확인 하기 전에 새 계정을 사용 하 여 로그인을 시도 합니다.  
   로그인 할 수 없고 확인 된 전자 메일 계정이 있어야 합니다. 또한 이제 메일 계정에 확인 메시지를 다시 보낼 수 있습니다.
7. 전자 메일 주소와 암호를 입력 하 고 다시 **보내기 확인** 단추를 누릅니다.
8. 새로 보낸 전자 메일 메시지를 기준으로 전자 메일 주소를 확인 한 후에는 앱에 로그인 합니다.

<a id="dbg"></a>
## <a name="troubleshooting-the-app"></a>앱 문제 해결

자격 증명을 확인 하기 위한 링크가 포함 된 전자 메일을 받지 못한 경우:

- 정크 또는 스팸 폴더를 확인 합니다.
- SendGrid 계정에 로그인 하 고 [전자 메일 활동 링크](https://sendgrid.com/logs/index)를 클릭 합니다.
- SendGrid 사용자 계정 이름은 SendGrid 계정 전자 메일 주소가 아닌 web.config *값으로* 사용 해야 합니다.

<a id="addRes"></a>
## <a name="additional-resources"></a>추가 리소스

- [ASP.NET Identity 권장 리소스에 대 한 링크](../../../identity/overview/getting-started/aspnet-identity-recommended-resources.md)
- [계정 확인 및 암호 복구 ASP.NET Identity](../../../identity/overview/features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Web Forms tutorial 시리즈-OAuth 2.0 공급자 추가](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#OAuthWebForms)
- [멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 배포 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)
- [ASP.NET Web Forms tutorial 시리즈-프로젝트에 SSL 사용](../getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal.md#SSLWebForms)
