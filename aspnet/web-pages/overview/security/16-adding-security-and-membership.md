---
uid: web-pages/overview/security/16-adding-security-and-membership
title: ASP.NET 웹 페이지 (Razor) 사이트에 보안 및 멤버 자격 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 일부 페이지를 로그인 하는 사용자만 사용할 수 있도록 웹 사이트를 보호 하는 방법을 보여 줍니다. (Tha 페이지를 만드는 방법을 참조 하세요.
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509903"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에 보안 및 멤버 자격 추가

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 일부 페이지를 로그인 하는 사용자만 사용할 수 있도록 Razor (ASP.NET 웹 페이지) 웹 사이트를 보호 하는 방법을 설명 합니다. 또한 누구나 액세스할 수 있는 페이지를 만드는 방법도 확인할 수 있습니다.
> 
> **학습 내용:** 
> 
> - 등록 페이지와 로그인 페이지가 있는 웹 사이트를 만드는 방법으로, 일부 페이지의 경우에만 액세스를 제한할 수 있습니다.
> - 공용 및 멤버 전용 페이지를 만드는 방법
> - 사이트에 대 한 보안 권한이 다른 그룹인 역할을 정의 하는 방법 및 사용자를 역할에 할당 하는 방법입니다.
> - CAPTCHA를 사용 하 여 자동화 된 프로그램 (봇)에서 구성원 계정을 만들지 못하게 하는 방법입니다.
>   
> 
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
> 
> - WebMatrix **시작 사이트** 템플릿
> - `WebSecurity` 도우미 및 `Roles` 클래스입니다.
> - `ReCaptcha` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 2
> - WebMatrix 3
> - ASP.NET 웹 도우미 라이브러리

사용자가 로그인 &#8212; 할 수 있도록 웹 사이트를 설정 하 여 사이트에서 *구성원 자격*을 지원할 수 있습니다. 이는 여러 가지 이유로 유용할 수 있습니다. 예를 들어 사이트에는 구성원만 사용할 수 있는 페이지가 있을 수 있습니다. 사용자 의견을 보내거나 의견을 남겨 두기 위해 사용자에 게 로그인 해야 하는 경우도 있습니다.

웹 사이트에서 구성원 자격을 지 원하는 경우에도 사용자는 사이트의 일부 페이지를 사용 하기 전에 반드시 로그인 해야 하는 것은 아닙니다. 로그인 하지 않은 사용자는 *익명 사용자*라고 합니다.

사용자는 웹 사이트에 등록 한 후 사이트에 로그인 할 수 있습니다. 웹 사이트를 사용 하려면 사용자 이름 (전자 메일 주소)과 암호를 사용 하 여 사용자에 게 주장 여부를 확인 해야 합니다. 사용자의 id를 로그인 하 고 확인 하는이 프로세스를 *인증*이라고 합니다.

다음과 같은 다양 한 방법으로 보안 및 멤버 자격을 설정할 수 있습니다.

- WebMatrix를 사용 하는 경우에는 **시작 사이트** 템플릿을 기반으로 새 사이트로 만드는 것이 쉬운 방법입니다. 이 템플릿은 이미 보안 및 멤버 자격에 대해 구성 되었으며 등록 페이지, 로그인 페이지 등이 이미 있습니다.

    템플릿에 의해 생성 된 사이트에는 사용자가 Facebook, Google, Twitter 등의 외부 사이트를 사용 하 여 로그인 할 수 있는 옵션도 있습니다.
- 기존 사이트에 보안을 추가 하거나 **시작 사이트** 템플릿을 사용 하지 않으려는 경우 등록 페이지, 로그인 페이지 등을 직접 만들 수 있습니다.

이 문서에서는 첫 번째 옵션 &mdash; **시작 사이트** 템플릿을 사용 하 여 보안을 추가 하는 방법을 중점적으로 설명 합니다. 또한 사용자 고유의 보안을 구현 하는 방법에 대 한 기본 정보를 제공 하 고이 작업을 수행 하는 방법에 대 한 자세한 정보 링크를 제공 합니다. 외부 로그인을 사용 하도록 설정 하는 방법에 대해서도 설명 합니다 .이에 대해서는 별도의 문서에 자세히 설명 되어 있습니다.

## <a name="creating-website-security-using-the-starter-site-template"></a>시작 사이트 템플릿을 사용 하 여 웹 사이트 보안 만들기

WebMatrix에서 **스타터 사이트** 템플릿을 사용 하 여 다음을 포함 하는 웹 사이트를 만들 수 있습니다.

- 멤버에 대 한 사용자 이름 및 암호를 저장 하는 데 사용 되는 데이터베이스입니다.
- 익명 (신규) 사용자가 등록할 수 있는 등록 페이지입니다.
- 로그인 및 로그 아웃 페이지
- 암호 복구 및 다시 설정 페이지

다음 절차에서는 사이트를 만들고 구성 하는 방법을 설명 합니다.

1. WebMatrix를 시작 하 고 **빠른 시작** 페이지에서 **템플릿에서 사이트**를 선택 합니다.
2. **시작 사이트** 템플릿을 선택 하 고 **확인**을 클릭 합니다. WebMatrix는 새 사이트를 만듭니다.
3. 왼쪽 창에서 **파일** 작업 영역 선택기를 클릭 합니다.
4. 웹 사이트의 루트 폴더에서 *\_AppStart* 파일을 엽니다 .이 파일은 전역 설정을 포함 하는 데 사용 되는 특수 한 파일입니다. 여기에는 `//` 문자를 사용 하 여 주석 처리 되는 문이 포함 됩니다.

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    이러한 문은 전자 메일을 보내는 데 사용할 수 있는 `WebMail` 도우미를 구성 합니다. 멤버 자격 시스템은 사용자가 등록 하거나 암호를 변경 하려는 경우 전자 메일을 사용 하 여 확인 메시지를 보낼 수 있습니다. 예를 들어 사용자가 등록 한 후 등록 프로세스를 완료 하기 위해 클릭할 수 있는 링크를 포함 하는 전자 메일을 받게 됩니다.

    전자 메일을 보내려면 [ASP.NET 웹 페이지 사이트에 전자 메일 추가](https://go.microsoft.com/fwlink/?LinkId=202899)에 설명 된 대로 SMTP 서버에 액세스 해야 합니다. 전자 메일을 보낼 수 있는 각 페이지에 반복적으로 코딩 하지 않아도 되도록이 중앙 *\_AppStart* 파일에 전자 메일 설정을 저장 합니다. (등록 데이터베이스를 설정 하기 위해 SMTP 설정을 구성할 필요는 없습니다. 사용자의 메일 별칭에서 사용자의 유효성을 검사 하 고 사용자가 잊어버린 암호를 다시 설정할 수 있도록 하려는 경우에만 SMTP 설정이 필요 합니다.)
5. 각 항목 앞에서 `//` 제거 하 여 문의 주석 처리를 제거 합니다.

    전자 메일 확인을 설정 하지 않으려면이 단계와 다음 단계를 건너뛸 수 있습니다. SMTP 값을 설정 하지 않으면 확인 전자 메일 없이 새 계정을 즉시 사용할 수 있습니다.
6. 코드에서 다음 전자 메일 관련 설정을 수정 합니다.

   - `WebMail.SmtpServer`를 액세스할 수 있는 SMTP 서버의 이름으로 설정 합니다.
   - `WebMail.EnableSsl`을 `true`로 설정 합니다. 이 설정은 SMTP 서버에 전송 되는 자격 증명을 암호화 하 여 보호 합니다.
   - `WebMail.UserName`를 SMTP 서버 계정에 대 한 사용자 이름으로 설정 합니다.
   - `WebMail.Password`를 SMTP 서버 계정의 암호로 설정 합니다.
   - `WebMail.From`를 본인의 전자 메일 주소로 설정 합니다. 메시지가 전송 되는 전자 메일 주소입니다.

     > [!NOTE] 
     > 
     > **팁** 이러한 속성의 값에 대 한 자세한 내용은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkID=202906)에서 [전자 메일 설정 구성](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings) 을 참조 하세요.
7. *\_AppStart*를 저장 하 고 닫습니다.
8. 브라우저에서 *기본값. cshtml* 페이지를 실행 합니다.

    ![보안-멤버 자격-2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > 속성이 `ExtendedMembershipProvider`인스턴스여야 한다는 오류 메시지가 표시 되 면 사이트가 SimpleMembership (ASP.NET 웹 페이지 membership system)를 사용 하도록 구성 되어 있지 않을 수 있습니다. 이는 호스트 공급자의 서버가 로컬 서버와 다르게 구성 된 경우에 발생할 수 있습니다. 이 문제를 해결 하려면 사이트의 *web.config* 파일에 다음 요소를 추가 합니다.
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > 이 요소를 `<configuration>` 요소의 자식으로 추가 하 고 `<system.web>` 요소의 피어로 추가 합니다.
9. 페이지의 오른쪽 위 모서리에서 **등록** 링크를 클릭 합니다. *레지스터 cshtml* 페이지가 표시 됩니다.
10. 사용자 이름 및 암호를 입력 한 다음 **등록**을 클릭 합니다.

    ![보안-멤버 자격-3](16-adding-security-and-membership/_static/image2.png)

    **시작 사이트** 템플릿에서 웹 사이트를 만들 때 사이트의 *앱\_데이터* 폴더에 *startersite. .sdf* 라는 데이터베이스가 생성 되었습니다. 등록 하는 동안 사용자 정보를 데이터베이스에 추가 합니다. SMTP 값을 설정 하면 등록을 완료할 수 있도록 사용한 전자 메일 주소로 메시지가 전송 됩니다.

    ![보안-멤버-4](16-adding-security-and-membership/_static/image3.png)
11. 전자 메일 프로그램으로 이동 하 여 확인 코드와 사이트에 대 한 하이퍼링크를 포함 하는 메시지를 찾습니다.
12. 계정을 활성화 하려면 하이퍼링크를 클릭 합니다. 확인 하이퍼링크는 등록 확인 페이지를 엽니다.

    ![보안-멤버-5](16-adding-security-and-membership/_static/image4.png)
13. **로그인** 링크를 클릭 한 다음 등록 한 계정을 사용 하 여 로그인 합니다.

      로그인 한 후 **로그인** 및 **등록** 링크는 로그 **아웃** 링크로 바뀝니다. 로그인 이름이 링크로 표시 됩니다. (링크를 사용 하 여 암호를 변경할 수 있는 페이지로 이동할 수 있습니다.)

      ![보안-멤버 자격-6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > 기본적으로 ASP.NET 웹 페이지에서는 사용자가 읽을 수 있는 텍스트로 서버에 자격 증명을 일반 텍스트로 보냅니다. 프로덕션 사이트는 서버와 교환 되는 중요 한 정보를 암호화 하기 위해 보안 HTTP (https://, *secure sockets layer* 또는 SSL이 라고도 함)를 사용 해야 합니다. 이전 예제와 같이 `WebMail.EnableSsl=true` 설정 하 여 SSL을 사용 하 여 전자 메일 메시지를 보낼 수 있습니다. SSL에 대 한 자세한 내용은 [웹 통신 보안: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)을 참조 하세요.

## <a name="additional-membership-functionality-in-the-site"></a>사이트의 추가 구성원 기능

사용자가 자신의 계정을 관리 하는 데 사용할 수 있는 다른 기능이 사이트에 포함 되어 있습니다. 사용자는 다음을 수행할 수 있습니다.

- 암호를 변경 합니다. 로그인 한 후 사용자 이름 (링크)을 클릭할 수 있습니다. 이렇게 하면 새 암호를 만들 수 있는 페이지 (*Account/ChangePassword. cshtml*)로 이동 합니다.
- 잊어버린 암호를 복구 합니다. 로그인 페이지에 사용자가 전자 메일 주소를 입력할 수 있는 페이지 (*Account/ForgotPassword*)로 이동 하는 링크가 있습니다 (**암호를 잊은 경우**). 사이트에서 새 암호를 설정 하기 위해 클릭할 수 있는 링크를 포함 하는 전자 메일 메시지를 보냅니다 (*Account/PasswordReset. cshtml*).

사용자가 나중에 설명 된 대로 외부 사이트를 사용 하 여 로그인 할 수도 있습니다.

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>멤버 전용 페이지 만들기

이 시점에서 누구나 웹 사이트의 모든 페이지를 탐색할 수 있습니다. 하지만 로그인 한 사용자 (즉, 구성원)만 사용할 수 있는 페이지를 포함할 수 있습니다. ASP.NET에서는 로그인 한 구성원만 액세스할 수 있는 페이지를 만들 수 있습니다. 일반적으로 익명 사용자가 멤버 전용 페이지에 액세스 하려고 하면 해당 페이지를 로그인 페이지로 리디렉션합니다.

이 절차에서는 로그인 한 사용자만 사용할 수 있는 페이지를 포함 하는 폴더를 만듭니다.

1. 사이트의 루트에서 새 폴더를 만듭니다. 리본에서 **새로 만들기** 아래에 있는 화살표를 클릭 한 다음 **새 폴더**를 선택 합니다.
2. 새 폴더의 이름을 *구성원*으로 합니다.
3. *Members* 폴더 안에 새 페이지를 만들고 이름을 *MembersInformation*로 지정 합니다.
4. 기존 콘텐츠를 다음 코드 및 태그로 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    이 코드는 사용자가 로그인 한 경우 `true`를 반환 하는 `WebSecurity` 개체의 `IsAuthenticated` 속성을 테스트 합니다. 사용자가 로그인 하지 않은 경우에는 `Response.Redirect`를 호출 하 여 *계정* 폴더의 *로그인. cshtml* 페이지로 사용자를 보냅니다.

    리디렉션의 URL에는 `Request.Url.LocalPath`를 사용 하 여 현재 페이지의 경로를 설정 하는 `returnUrl` 쿼리 문자열 값이 포함 되어 있습니다. 쿼리 문자열에 `returnUrl` 값을 설정 하면 (반환 URL이 로컬 경로인 경우) 로그인 페이지는 로그인 한 후에이 페이지로 사용자를 반환 합니다.

    또한이 코드는 *\_SiteLayout* 페이지를 레이아웃 페이지로 설정 합니다. (레이아웃 페이지에 대 한 자세한 내용은 [ASP.NET 웹 페이지 사이트에서 일관적인 레이아웃 만들기](https://go.microsoft.com/fwlink/?LinkId=202891)를 참조 하세요.)
5. 사이트를 실행 합니다. 로그인 되어 있으면 페이지 맨 위에 있는 **로그 아웃** 단추를 클릭 합니다.
6. 브라우저에서 */Members/MembersInformation*페이지를 요청 합니다. 예를 들어 URL은 다음과 같습니다.

    `http://localhost:38366/Members/MembersInformation`

    포트 번호 (38366)는 URL에서 다를 수 있습니다.

    로그인 하지 않았기 때문에 *로그인. cshtml* 페이지로 리디렉션됩니다.
7. 이전에 만든 계정을 사용 하 여 로그인 합니다. *MembersInformation* 페이지로 다시 리디렉션됩니다. 로그인 했으므로 이번에는 페이지 콘텐츠가 표시 됩니다.

여러 페이지에 대 한 액세스를 보호 하기 위해 다음과 같은 작업을 수행할 수 있습니다.

- 각 페이지에 보안 검사를 추가 합니다.
- 보호 된 페이지를 보관 하는 폴더에 *\_PageStart.* s s o s o s t o s o s 페이지를 만들고 여기에 보안 확인을 추가 합니다. *\_PageStart. cshtml* 페이지는 폴더의 모든 페이지에 대 한 전역 페이지 종류의 역할을 합니다. 이 기법은 [ASP.NET 웹 페이지에 대 한 사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access)에 자세히 설명 되어 있습니다.

## <a name="creating-security-for-groups-of-users-roles"></a>사용자 그룹에 대 한 보안 만들기 (역할)

사이트에 많은 멤버가 있는 경우 페이지를 표시 하기 전에 각 사용자에 대 한 권한을 개별적으로 확인 하는 것은 효율적이 지 않습니다. 대신, 개별 멤버가 속하는 그룹 또는 *역할*을 만들 수 있습니다. 그런 다음 역할에 따라 사용 권한을 확인할 수 있습니다. 이 섹션에서는 &quot;admin&quot; 역할을 만든 다음 해당 역할에 속한 사용자가 액세스할 수 있는 페이지를 만듭니다.

ASP.NET 멤버 자격 시스템은 역할을 지원 하도록 설정 됩니다. 그러나 멤버 자격 등록과 로그인과 달리 **시작 사이트** 템플릿에는 역할을 관리 하는 데 도움이 되는 페이지가 포함 되지 않습니다. 역할 관리는 사용자 태스크가 아닌 관리 작업입니다. 그러나 WebMatrix의 멤버 자격 데이터베이스에 직접 그룹을 추가할 수 있습니다.

1. WebMatrix에서 **데이터베이스** 작업 영역 선택기를 클릭 합니다.
2. 왼쪽 창에서 *Startersite. .sdf* 노드를 열고 **Tables** 노드를 연 다음 *웹 페이지\_역할* 표를 두 번 클릭 합니다.

    ![보안-멤버-7](16-adding-security-and-membership/_static/image6.png)
3. &quot;admin&quot;라는 역할을 추가 합니다. *RoleId* 필드는 자동으로 채워집니다. ( [ASP.NET 웹 페이지 사이트의 데이터베이스 작업 소개](https://go.microsoft.com/fwlink/?LinkId=202893)에서 설명한 대로 기본 키 이며 식별 필드로 설정 되었습니다.)
4. *RoleId* 필드에 대 한 값을 기록해 둡니다. (이 역할이 정의 하는 첫 번째 역할인 경우 1이 됩니다.)

    ![보안-멤버 자격-8](16-adding-security-and-membership/_static/image7.png)
5. *웹 페이지\_역할* 표를 닫습니다.
6. *UserProfile* 테이블을 엽니다.
7. 테이블에서 하나 이상의 사용자 *id* 값을 기록한 다음 테이블을 닫습니다.
8. *웹 페이지\_UserInRoles* 테이블을 열고 *UserID* 및 *RoleID* 값을 테이블에 입력 합니다. 예를 들어 사용자 2를 &quot;관리&quot; 역할에 추가 하려면 다음 값을 입력 합니다.

    ![보안-멤버-9](16-adding-security-and-membership/_static/image8.png)
9. *웹 페이지\_UsersInRoles* 테이블을 닫습니다.

    역할이 정의 되었으므로 해당 역할의 사용자가 액세스할 수 있는 페이지를 구성할 수 있습니다.
10. 웹 사이트 루트 폴더에서 *Adminerror. cshtml* 이라는 새 페이지를 만들고 기존 콘텐츠를 다음 코드로 바꿉니다. 페이지에 대 한 액세스가 허용 되지 않는 경우 사용자가 리디렉션되는 페이지가 됩니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. 웹 사이트 루트 폴더에서 *Adminonly. cshtml* 이라는 새 페이지를 만들고 기존 코드를 다음 코드로 바꿉니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    `Roles.IsUserInRole` 메서드는 현재 사용자가 지정 된 역할의 멤버 (이 경우 "admin" 역할) 인 경우 `true`을 반환 합니다.
12. 브라우저에서 *기본값 cshtml* 를 실행 하지만 로그인 하지 않습니다. 이미 로그인 한 경우 로그 아웃 합니다.
13. 브라우저의 주소 표시줄에서 *Adminonly* 를 URL에 추가 합니다. 즉, *Adminonly. cshtml* 파일을 요청 합니다. 현재 &quot;admin&quot; 역할의 사용자로 로그인 하지 않았으므로 *Adminerror. cshtml* 페이지로 리디렉션됩니다.
14. *기본. cshtml* 로 돌아가서 &quot;admin&quot; 역할에 추가한 사용자로 로그인 합니다.
15. *Adminonly. cshtml 페이지로 이동 합니다.* 이번에는 페이지가 표시 됩니다.

## <a name="preventing-automated-programs-from-joining-your-website"></a>자동 프로그램이 웹 사이트에 가입 하지 못하도록 방지

로그인 페이지는 자동 프로그램 ( *웹 로봇* 또는 *봇*이 라고도 함)을 웹 사이트에 등록 하는 것을 중지 하지 않습니다. 이 절차에서는 등록 페이지에 대해 ReCaptcha 테스트를 사용 하도록 설정 하는 방법을 설명 합니다.

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net))에서 웹 사이트를 등록 합니다. 등록을 완료 하면 공개 키와 개인 키를 얻게 됩니다.
2. [ASP.NET 웹 페이지 사이트에 도우미 설치](https://go.microsoft.com/fwlink/?LinkId=252372)에 설명 된 대로 ASP.NET 웹 도우미 라이브러리를 웹 사이트에 추가 합니다 (아직 없는 경우).
3. *계정* 폴더에서 이름이 *Register. cshtml*인 파일을 엽니다.
4. 페이지의 맨 위에 있는 코드에서 다음 줄을 찾고 `//` 주석 문자를 제거 하 여 주석 처리를 제거 합니다.

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. `PRIVATE_KEY`를 사용자 고유의 ReCaptcha 개인 키로 바꿉니다.
6. 페이지의 태그에서 `@*`를 제거 하 고 페이지 태그의 다음 줄 주위에서 주석 문자를 `*@` 합니다.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. `PUBLIC_KEY`을 키로 바꿉니다.
8. 아직 제거 하지 않은 경우 "CAPTCHA 검증을 사용 하도록 설정 하려면"으로 시작 하는 텍스트가 포함 된 `<div>` 요소를 제거 합니다. 전체 `<div>` 요소와 해당 내용을 제거 합니다.

9. 브라우저에서 *기본값 cshtml* 를 실행 합니다. 사이트에 로그인 하는 경우 **로그 아웃** 링크를 클릭 합니다.
10. **등록** 링크를 클릭 하 고 CAPTCHA 테스트를 사용 하 여 등록을 테스트 합니다.

     ![보안-멤버 자격-10](16-adding-security-and-membership/_static/image9.png)

`ReCaptcha` 도우미에 대 한 자세한 내용은 CATPCHA를 [사용 하 여 자동화 된 프로그램 (봇)에서 ASP.NET 웹 사이트 사용 방지](https://go.microsoft.com/fwlink/?LinkId=251967)를 참조 하세요.

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>사용자가 외부 사이트를 사용 하 여 로그인 하도록 허용

**시작 사이트** 템플릿에는 사용자가 Facebook, Windows Live, Twitter, Google 또는 Yahoo를 사용 하 여 로그인 할 수 있도록 하는 코드와 태그가 포함 됩니다. 기본적으로이 기능은 사용 되지 않습니다. 사용자가 이러한 외부 공급자를 사용 하 여 로그인 할 수 있도록 허용 하는 일반적인 절차는 다음과 같습니다.

- 지원 하려는 외부 사이트를 결정 합니다.
- 필요한 경우 해당 사이트로 이동 하 여 로그인 앱을 설정 합니다. (예를 들어 Facebook 로그인을 허용 하기 위해이 작업을 수행 해야 합니다.)
- 사이트에서 공급자를 구성 합니다. 대부분의 경우 *\_AppStart* 파일에서 일부 코드의 주석 처리를 제거 하기만 하면 됩니다.
- 사용자가 로그인을 위해 외부 사이트에 연결할 수 있도록 하는 태그를 등록 페이지에 추가 합니다. 일반적으로 필요한 태그를 복사 하 고 텍스트를 약간 변경할 수 있습니다.

[ASP.NET 웹 페이지 사이트에서 외부 사이트에서 로그인 사용](https://go.microsoft.com/fwlink/?LinkId=251969)항목의 단계별 지침을 찾을 수 있습니다.

사용자가 다른 사이트에서 로그인 한 후 사용자가 사이트로가 서 해당 로그인을 사이트에 *연결* 합니다. 실제로 사용자의 외부 로그인을 위해 사이트에 멤버 자격 항목이 생성 됩니다. 이를 통해 외부 로그인을 사용 하 여 멤버 (예: 역할)의 정상적인 기능을 사용할 수 있습니다.

## <a name="adding-security-to-an-existing-website"></a>기존 웹 사이트에 보안 추가

이 문서의 앞부분에 나오는 절차는 **시작 사이트** 템플릿을 웹 사이트 보안의 기반으로 사용 하는 방법을 설명 합니다. 시작 **사이트** 템플릿에서 시작 하거나 해당 템플릿을 기반으로 하는 사이트에서 관련 페이지를 복사 하는 것이 실용적이 지 않은 경우 직접 코딩 하 여 자체 사이트에서 동일한 유형의 보안을 구현할 수 있습니다. 동일한 유형의 페이지 (등록, 로그인 등)를 만든 다음 도우미와 클래스를 사용 하 여 멤버 자격을 설정 합니다.

기본 프로세스는 [ASP.NET Razor 보안을 구현 하는 가장 기본적인 방법인](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240)블로그 게시물에 설명 되어 있습니다. 대부분의 작업은 `WebSecurity` 도우미의 다음 메서드 및 속성을 사용 하 여 수행 됩니다.

- [WebSecurty](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx), [Websecurity. CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx). 이러한 메서드를 사용 하 여 누군가가 이미 등록 되어 있는지 여부를 확인 하 고 등록할 수 있습니다.
- [WebSecurty](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx). 이 속성을 사용 하 여 현재 사용자가 로그인 했는지 여부를 확인할 수 있습니다. 이 기능은 로그인 페이지가 아직 로그인 하지 않은 경우 사용자를 로그인 페이지로 리디렉션하는 데 유용 합니다.
- [Websecurity. Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx), [Websecurity. Logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx). 이러한 메서드는 사용자를 로그인 또는 로그 아웃 합니다.
- [Websecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx). 이 속성은 사용자가 로그인 한 경우 현재 사용자의 로그인 된 이름을 표시 하는 데 유용 합니다.
- [Websecurity. \Account](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx). 이 방법은 등록을 위한 전자 메일 확인을 설정 하는 경우에 유용 합니다. 자세한 내용은 블로그 게시물에서 [ASP.NET 웹 페이지 보안에 대 한 확인 기능 사용](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)을 참조 하세요.)

역할을 관리 하기 위해 블로그 항목에 설명 된 대로 [역할](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx) 및 [멤버 자격](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx) 클래스를 사용할 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

- [사이트 전체 동작 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
- [웹 통신 보안: 인증서, SSL 및 https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- [ASP.NET Razor 보안을 구현 하](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240) 고 [ASP.NET 웹 페이지 보안을 위한 확인 기능을 사용](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267)하는 가장 기본적인 방법입니다. 다음은 **스타터 사이트** 템플릿을 사용 하지 않고 ASP.NET membership 기능을 구현 하는 방법을 설명 하는 블로그 게시물입니다.
- [ASP.NET 웹 페이지 사이트에서 외부 사이트 로그인 사용](https://go.microsoft.com/fwlink/?LinkId=251969)
- [Websecurity 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99)) (MSDN)
- [SimpleRoleProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99)) (MSDN)
- [SimpleMembershipProvider 클래스 API 참조](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99)) (MSDN)
