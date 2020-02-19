---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: Azure Active Directory-ASP.NET 4.x를 사용 하 여 ASP.NET Apps 개발
author: Rick-Anderson
description: Azure Active Directory 용 Microsoft ASP.NET 도구를 사용 하면 Azure에서 호스팅되는 웹 응용 프로그램에 대 한 인증을 간편 하 게 사용할 수 있습니다. Azure 사전를 사용할 수 있습니다.
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456727"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>Azure Active Directory를 사용하여 ASP.NET 앱 개발

[Rick Anderson](https://twitter.com/RickAndMSFT)

Azure Active Directory 용 Microsoft ASP.NET 도구를 사용 하면 [Azure](https://www.windowsazure.com/home/features/web-sites/)에서 호스트 되는 웹 앱에 대 한 인증을 쉽게 사용할 수 있습니다 Azure 인증을 사용 하 여 조직에서 Office 365 사용자를 인증 하거나, 온-프레미스 Active Directory에서 동기화 된 회사 계정 또는 고유한 사용자 지정 Azure Active Directory 도메인에서 만든 사용자를 인증할 수 있습니다. Windows Azure 인증을 사용 하도록 설정 하면 단일 [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) 테 넌 트를 사용 하 여 사용자를 인증 하도록 응용 프로그램이 구성 됩니다

이 자습서에서는 [Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) (Azure AD)를 사용 하 여 로그온 하도록 구성 된 ASP.NET 응용 프로그램을 만드는 방법을 보여 줍니다. 또한 Graph API를 호출 하 여 현재 로그인 한 사용자에 대 한 정보 및 응용 프로그램을 Azure에 배포 하는 방법에 대해 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

1. 웹 또는 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) [에 대해 2013을 Visual Studio Express](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) 합니다.
2. [Visual Studio 2013 업데이트 4](https://www.microsoft.com/download/details.aspx?id=44921) -업데이트 3 이상이 필요 합니다.
3. Azure 계정. 아직 계정이 없는 경우 평가판을 사용 하려면 [여기를 클릭](https://azure.microsoft.com/pricing/free-trial/) 하세요.

## <a name="add-a-global-administrator-to-your-active-directory"></a>Active Directory에 전역 관리자 추가

1. [Azure 관리 포털](https://manage.windowsazure.com/)에 로그인합니다.
2. 모든 Azure 계정에는 **기본 디렉터리가** 포함 되어 있습니다. 클릭 한 다음 페이지 맨 위에 있는 **사용자** 탭을 클릭 합니다 (아래 이미지 참조).
3. 사용자 추가를 클릭합니다.
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. **전역 관리자** 역할을 사용 하 여 새 사용자를 만듭니다. 위쪽 메뉴에서 **사용자** 를 클릭 한 다음 명령 모음에서 **사용자 추가** 단추를 클릭 합니다.
5. **사용자 추가** 대화 상자에서 새 사용자의 이름을 입력 하 고 오른쪽 화살표를 클릭 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. 사용자 이름을 입력 하 고 역할을 **전역 관리자**로 설정 합니다. 전역 관리자는 암호 복구를 위해 대체 전자 메일 주소가 필요 합니다. 작업이 완료 되 면 오른쪽 화살표를 클릭 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. 대화 상자의 다음 페이지에서 **만들기**를 클릭 합니다. 새 사용자에 대 한 임시 암호가 생성 되 고 대화 상자에 표시 됩니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   암호를 저장 하면 첫 번째 로그인 후에 암호를 변경 해야 합니다. 다음 이미지는 새 관리자 계정을 보여 줍니다. 이 페이지에 표시 된 Microsoft 계정 아니라 Azure Active Directory을 사용 하 여 앱에 로그인 해야 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>ASP.NET 응용 프로그램 만들기

다음 단계에서는 [웹에 Visual Studio Express 2013](https://www.microsoft.com/download/details.aspx?id=40747)를 사용 하며 [Visual Studio 2013 업데이트 3](https://www.microsoft.com/download/details.aspx?id=43721)이 필요 합니다.

1. Visual Studio에서 **파일** , **새 프로젝트**를 차례로 클릭 합니다. **새 프로젝트** 대화 상자의 왼쪽 메뉴에서 비주얼 C# 웹 프로젝트를 선택 하 고 **확인**을 클릭 합니다. 응용 프로그램에 대 한 기능을 원하지 않는 경우 **프로젝트에 Application Insights 추가** 를 선택 취소 해야 할 수도 있습니다.
2. **새 ASP.NET 프로젝트** 대화 상자에서 **MVC**를 선택 하 고 **인증 변경**을 클릭 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. **인증 변경** 대화 상자에서 **조직 계정**을 선택 합니다. 이러한 옵션을 사용 하 여 azure AD에 응용 프로그램을 자동으로 등록 하 고 Azure AD와 통합 하도록 응용 프로그램을 자동으로 구성할 수 있습니다. **인증 변경** 대화 상자를 사용 하 여 응용 프로그램을 등록 하 고 구성할 필요가 없지만 훨씬 쉽게 수행할 수 있습니다. 예를 들어 Visual Studio 2012을 사용 하는 경우 Azure 관리 포털에서 수동으로 응용 프로그램을 등록 하 고 Azure AD와 통합 되도록 해당 구성을 업데이트할 수 있습니다.
   드롭다운 메뉴에서 **클라우드-단일 조직** 및 **single Sign On을 선택 하 고 디렉터리 데이터를 읽습니다**. Azure AD 디렉터리의 도메인을 입력 합니다 (예: 아래 이미지) *aricka0yahoo.onmicrosoft.com*를 입력 한 다음 **확인**을 클릭 합니다. Azure portal의 기본 디렉터리에 대 한 도메인 탭에서 도메인 이름을 가져올 수 있습니다 (다음 이미지 참조).

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   다음 이미지는 Azure Portal의 도메인 이름을 보여 줍니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > **추가 옵션**을 클릭 하 여 Azure AD에 등록 될 응용 프로그램 ID URI를 선택적으로 구성할 수 있습니다. 앱 ID URI는 azure AD에 등록 되 고 Azure AD와 통신할 때 응용 프로그램에서 자신을 식별 하는 데 사용 하는 응용 프로그램에 대 한 고유 식별자입니다. 앱 ID URI 및 등록 된 응용 프로그램의 기타 속성에 대 한 자세한 내용은 [이 항목](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)을 참조 하세요. 앱 ID URI 필드 아래의 확인란을 클릭 하 여 동일한 앱 ID URI를 사용 하는 Azure AD의 기존 등록을 덮어쓰도록 선택할 수도 있습니다.
4. **[확인**]을 클릭 하면 로그인 대화 상자가 나타나고 전역 관리자 계정을 사용 하 여 로그인 해야 합니다 (구독과 연결 된 Microsoft 계정이 아님). 이전에 새 관리자 계정을 만든 경우 암호를 변경한 후 새 암호를 사용 하 여 다시 로그인 해야 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 성공적으로 인증 되 면 **새 ASP.NET 프로젝트** 대화 상자에는 인증 선택 (**조직** ) 및 새 응용 프로그램을 등록할 디렉터리 (아래 이미지에*aricka0yahoo.onmicrosoft.com* )가 표시 됩니다. 이 정보 아래에서 **클라우드의 호스트**레이블 확인란을 선택 합니다. 이 확인란을 선택 하면 프로젝트가 Azure 웹 앱으로 프로 비전 되 고 나중에 쉽게 게시할 수 있게 됩니다. **확인**을 클릭합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. 자동 생성 된 사이트 이름 및 지역을 사용 하 여 **Azure 웹 사이트 구성** 대화 상자가 표시 됩니다. 또한 대화 상자에서 현재 로그인 한 계정에 주목 하세요. Azure 구독이 연결 된 계정 (일반적 Microsoft 계정) 인지 확인 하려고 합니다.

    > [!NOTE]
    > 이 프로젝트에는 데이터베이스가 필요 합니다. 기존 데이터베이스 중 하나를 선택 하거나 새 데이터베이스를 만들어야 합니다. 프로젝트에서 이미 로컬 데이터베이스 파일을 사용 하 여 적은 양의 인증 구성 데이터를 저장 하기 때문에 데이터베이스가 필요 합니다. Azure 웹 사이트에 응용 프로그램을 배포 하는 경우이 데이터베이스는 배포와 함께 패키지 되지 않으므로 클라우드에서 액세스할 수 있는 데이터베이스를 선택 해야 합니다. **확인**을 클릭합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. 프로젝트가 만들어지고 인증 옵션 및 웹 앱 옵션이 프로젝트를 사용 하 여 자동으로 구성 됩니다. 이 프로세스가 완료 되 면 **^ F5**키를 눌러 프로젝트를 로컬로 실행 합니다. 조직 계정을 사용 하 여 로그인 해야 합니다. 이전에 만든 계정에 대 한 사용자 이름 및 암호를 입력 하 고 **로그인**을 클릭 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. 성공적으로 로그인 하면 ASP.NET 사이트는 페이지의 오른쪽 위 모서리에 사용자 이름을 표시 하 여 인증 되었음을 표시 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   오류가 발생 하는 경우: 값은 null 이거나 비워 둘 수 없습니다. 매개 변수 이름: t ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   자습서의 끝 부분에 있는 [디버그](#dbg) 섹션을 참조 하세요.

## <a name="basics-of-the-graph-api"></a>Graph API의 기본 사항

[Graph API](https://msdn.microsoft.com/library/azure/hh974476.aspx) 은 Azure AD 디렉터리의 개체에 대 한 CRUD 및 기타 작업을 수행 하는 데 사용 되는 프로그래밍 인터페이스입니다. Visual Studio 2013에서 새 프로젝트를 만들 때 인증을 위해 조직 계정 옵션을 선택 하는 경우 응용 프로그램은 이미 Graph API를 호출 하도록 구성 되어 있습니다. 이 섹션에서는 Graph API 작동 하는 방법을 간략하게 보여 줍니다.

1. 실행 중인 응용 프로그램에서 페이지의 오른쪽 위에 있는 로그인 한 사용자의 이름을 클릭 합니다. 그러면 홈 컨트롤러에서 작업 인 사용자 프로필 페이지로 이동 합니다. 테이블에 이전에 만든 관리자 계정에 대 한 사용자 정보가 포함 되어 있음을 알 수 있습니다. 이 정보는 디렉터리에 저장 되 고 Graph API는 페이지가 로드 될 때이 정보를 검색 하기 위해 호출 됩니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. Visual Studio로 돌아가서 **Controllers** 폴더를 확장 한 다음 **HomeController.cs** 파일을 엽니다. 토큰을 검색 한 다음 Graph API를 호출 하는 코드를 포함 하는 **UserProfile ()** 작업이 표시 됩니다. 이 코드는 아래와 중복 됩니다.

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    Graph API를 호출 하려면 먼저 토큰을 검색 해야 합니다. 토큰을 검색할 때 Graph API에 대 한 모든 후속 요청에 대 한 권한 부여 헤더에 해당 문자열 값을 추가 해야 합니다. 위의 코드는 대부분 토큰을 사용 하 여 토큰을 가져오고, 토큰을 사용 하 여 Graph API에 대 한 호출을 수행 하 고, 응답을 변환 하 여 뷰에 표시할 수 있도록 Azure AD 인증에 대 한 세부 정보를 처리 합니다.

    토론에 대 한 가장 관련성이 높은 부분은 다음과 같은 강조 표시 된 줄입니다. `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`. 이 줄은 JSON 응답에서 deserialize 되어 뷰에 표시 되는 사용자의 이름을 나타냅니다.

    HttpClient를 사용 하 여 Graph API를 호출 하 고 원시 데이터를 직접 처리할 수 있지만, [NuGet을 통해 사용할 수 있는 Graph 클라이언트 라이브러리](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)를 사용 하는 것이 더 쉬운 방법입니다. 클라이언트 라이브러리는 원시 HTTP 요청 및 반환 된 데이터의 변환을 처리 하 고 .NET 환경에서 Graph API 작업을 훨씬 쉽게 수행할 수 있도록 합니다. GitHub의 관련 Graph API 코드 샘플을 참조 하세요 [.](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>Azure에 애플리케이션 배포

다음 단계에서는 Azure에 응용 프로그램을 배포 하는 방법을 보여 줍니다. 이전 단계에서는 Azure의 웹 앱에 새 프로젝트를 연결 했으므로 몇 가지 단계 만으로 게시할 준비가 되었습니다.

1. Visual Studio에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다. **웹 게시** 대화 상자가 표시 되 고 각 설정이 이미 구성 되어 있습니다. **다음** 단추를 클릭 하 여 **설정** 페이지로 이동 합니다. 인증 하 라는 메시지가 표시 될 수 있습니다. 이전에 만든 조직 계정이 아닌 Azure 구독 계정 (일반적으로 Microsoft 계정)을 사용 하 여 인증 해야 합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. **조직 인증 사용** 옵션을 선택 합니다. **도메인** 필드에 디렉터리의 도메인을 입력 합니다. **액세스 수준** 드롭다운에서 **Single Sign On, 디렉터리 데이터 읽기를**선택 합니다. 이전에 사용한 데이터베이스는 **데이터베이스** 섹션에 이미 채워져 있는 것을 알 수 있습니다. **게시**를 클릭합니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio가 웹 사이트 배포를 시작 하면 새 브라우저 창이 표시 됩니다. 디렉터리에 다시 인증 하 라는 메시지가 표시 될 수 있습니다. 인증 되 면 Azure에서 새로 게시 된 웹 사이트로 리디렉션됩니다.

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>앱 디버깅

다음 오류가 발생 하면 값은 null 이거나 비워 둘 수 없습니다. 매개 변수 이름: t

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

*Views\Shared\\_LoginPartial* 파일의 코드를 다음으로 바꿉니다.

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

앱을 실행 한 후 로그인 한 사용자에 게 "Null 사용자"가 표시 되 면 이전에 만든 Active Directory 계정으로 로그 아웃 하 고 다시 로그인 합니다.

Azure [AD를 사용 하는 Azure Websites 및 조직 인증](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)Rick Rainey의 심층 소개를 참조 하세요.

## <a name="more-information"></a>추가 정보

- [심층 살펴보기: azure AD를 사용한 Azure Websites 및 조직 인증](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)
- [Azure AD Graph API 개요](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD의 인증 시나리오](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub의 Azure AD 코드 샘플](https://github.com/AzureADSamples)
