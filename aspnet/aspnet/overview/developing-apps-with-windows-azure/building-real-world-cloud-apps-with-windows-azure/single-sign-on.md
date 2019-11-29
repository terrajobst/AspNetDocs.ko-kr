---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: Single Sign-on (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 7e32f444dc38132296cffd45ac658f5abf51f314
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585274"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>Single Sign-on (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

클라우드 앱을 개발 하는 경우에는 많은 보안 문제가 발생 하지만,이 시리즈의 경우에는 Single Sign-On에만 초점을 둡니다. 자주 묻는 질문은 다음과 같습니다. "회사 직원을 위한 앱을 주로 빌드하고 있습니다. 이러한 앱을 클라우드에서 호스트 하 고 방화벽 내에서 호스트 되는 앱을 실행 하는 동안 내 직원이 알고 있으며 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용할 수 있게 하려면 어떻게 해야 하나요? " 이 시나리오를 사용 하도록 설정 하는 방법 중 하나를 Azure AD (Azure Active Directory) 라고 합니다. Azure AD를 사용 하면 인터넷을 통해 사용할 수 있는 엔터프라이즈급 LOB (기간 업무) 앱을 만들 수 있으며, 이러한 앱을 비즈니스 파트너에 게 제공할 수도 있습니다.

## <a name="introduction-to-azure-ad"></a>Azure AD 소개

[AZURE AD](https://docs.microsoft.com/azure/active-directory/) 는 클라우드에서 [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 을 제공 합니다. 주요 기능에는 다음이 포함 됩니다.

- 온-프레미스 Active Directory와 통합 됩니다.
- 앱을 사용 하 여 Single Sign-On 수 있습니다.
- [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-급지됨](http://en.wikipedia.org/wiki/WS-Federation)및 [OAuth 2.0](http://oauth.net/2/)와 같은 오픈 표준을 지원 합니다.
- Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)를 지원 합니다.

직원 들이 인트라넷 앱에 로그온 할 수 있도록 하는 온-프레미스 Windows Server Active Directory 환경이 있다고 가정 합니다.

![](single-sign-on/_static/image1.png)

Azure AD를 사용 하 여 클라우드에서 디렉터리를 만들 수 있습니다. 무료 기능이 며 쉽게 설정할 수 있습니다.

온-프레미스 Active Directory와 완전히 다를 수 있습니다. 원하는 모든 사용자를 추가 하 고 인터넷 앱에서 인증할 수 있습니다.

![Microsoft Azure Active Directory](single-sign-on/_static/image2.png)

또는 온-프레미스 AD와 통합할 수 있습니다.

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

이제 온-프레미스에서 인증을 받을 수 있는 모든 직원은 인터넷을 통해 인증할 수도 있습니다. 즉, 방화벽을 열거나 데이터 센터에 새 서버를 배포 하지 않아도 됩니다. 현재 알고 있는 기존 Active Directory 환경을 계속 활용 하 여 내부 앱에 single sign-on 기능을 제공할 수 있습니다.

AD와 Azure AD 간에이 연결을 설정한 후에는 웹 앱과 모바일 장치에서 클라우드의 직원을 인증 하도록 설정 하 고 Office 365, SalesForce.com 또는 Google apps와 같은 타사 앱을 사용 하도록 설정 하 여 다음을 허용할 수 있습니다. 직원 자격 증명. Office 365에서 인증 및 권한 부여에 Azure AD를 사용 하기 때문에 Office 365를 사용 하는 경우 이미 Azure AD를 사용 하 여 설정 되어 있습니다.

![타사 앱](single-sign-on/_static/image4.png)

이 방법의 장점은 조직이 사용자를 추가 또는 삭제 하거나 사용자가 암호를 변경 하는 경우 온-프레미스 환경에서 현재 사용 하는 것과 동일한 프로세스를 사용 하는 것입니다. 모든 온-프레미스 AD 변경 내용은 클라우드 환경에 자동으로 전파 됩니다.

회사에서을 사용 하거나 Office 365로 이동 하는 경우 Office 365에서 인증에 Azure AD를 사용 하기 때문에 Azure AD를 자동으로 설정 하는 것이 좋습니다. 따라서 Office 365에서 사용 하는 것과 동일한 인증을 자신의 앱에서 쉽게 사용할 수 있습니다.

## <a name="set-up-an-azure-ad-tenant"></a>Azure AD 테 넌 트 설정

azure ad 디렉터리를 Azure AD [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)라고 하며, 테 넌 트를 설정 하는 작업은 매우 간단 합니다. 개념을 설명 하기 위해 Azure 관리 포털에서 작업을 수행 하는 방법을 보여 주지만 다른 포털 함수와 같은 스크립트나 관리 API를 사용 하 여 수행할 수도 있습니다.

관리 포털에서 Active Directory 탭을 클릭 합니다.

![포털의 WAAD](single-sign-on/_static/image5.png)

Azure 계정에 대해 하나의 Azure AD 테 넌 트가 자동으로 있고 페이지 맨 아래에 있는 **추가** 단추를 클릭 하 여 추가 디렉터리를 만들 수 있습니다. 예를 들어 테스트 환경 및 프로덕션 환경에 대해 하나를 사용할 수 있습니다. 새 디렉터리의 이름을 신중 하 게 생각 합니다. 디렉터리 이름을 사용 하는 경우 사용자 중 하나에 대해 이름을 다시 사용 하면 혼동을 줄일 수 있습니다.

![디렉터리 추가](single-sign-on/_static/image6.png)

포털은이 환경 내에서 사용자를 만들고, 삭제 하 고, 관리할 수 있는 모든 기능을 제공 합니다. 예를 들어 사용자를 추가 하려면 **사용자 탭으로 이동 하 여** **사용자 추가** 단추를 클릭 합니다.

![[사용자 추가] 단추](single-sign-on/_static/image7.png)

![사용자 추가 대화 상자](single-sign-on/_static/image8.png)

이 디렉터리에만 존재 하는 새 사용자를 만들거나 Microsoft 계정을이 디렉터리의 사용자로 등록 하거나 다른 Azure AD 디렉터리의 사용자를이 디렉터리의 사용자로 등록할 수 있습니다. 실제 디렉터리에서 기본 도메인은 ContosoTest.onmicrosoft.com입니다. Contoso.com와 같이 사용자가 선택한 도메인을 사용할 수도 있습니다.

![사용자 유형](single-sign-on/_static/image9.png)

![사용자 추가 대화 상자](single-sign-on/_static/image10.png)

사용자를 역할에 할당할 수 있습니다.

![사용자 프로필](single-sign-on/_static/image11.png)

임시 암호를 사용 하 여 계정을 만듭니다.

![임시 암호](single-sign-on/_static/image12.png)

이 방법을 만든 사용자는이 클라우드 디렉터리를 사용 하 여 웹 앱에 즉시 로그인 할 수 있습니다.

그러나 엔터프라이즈 Single Sign-On에 대 한 유용한 정보는 **디렉터리 통합** 탭입니다.

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

디렉터리 통합을 사용 하도록 설정 하 고 [도구를 다운로드](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)하는 경우이 클라우드 디렉터리를 조직 내에서 이미 사용 중인 기존 온-프레미스 Active Directory와 동기화 할 수 있습니다. 그러면 디렉터리에 저장 된 모든 사용자가이 클라우드 디렉터리에 표시 됩니다. 이제 클라우드 앱에서 기존 Active Directory 자격 증명을 사용 하 여 모든 직원을 인증할 수 있습니다. 이 모든 것은 무료입니다. 동기화 도구와 Azure AD 자체도 모두 사용 가능 합니다.

도구는이 화면에서 볼 수 있는 것 처럼 쉽게 사용할 수 있는 마법사입니다. 이는 전체 지침이 아니라 기본 프로세스를 보여 주는 예제 일 뿐입니다. 자세한 방법에 대 한 자세한 내용은 챕터의 끝에 있는 [리소스](#resources) 섹션의 링크를 참조 하세요.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image14.png)

**다음**을 클릭 하 고 Azure Active Directory 자격 증명을 입력 합니다.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image15.png)

**다음**을 클릭 하 고 온-프레미스 AD 자격 증명을 입력 합니다.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image16.png)

**다음**을 클릭 하 고 클라우드의 AD 암호 해시를 저장할 것인지 여부를 지정 합니다.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image17.png)

클라우드에 저장할 수 있는 암호 해시는 단방향 해시입니다. 실제 암호는 Azure AD에 저장 되지 않습니다. 클라우드에 해시를 저장 하지 않을 경우 [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS)를 사용 해야 합니다. 또한 ADFS를 사용할지 [여부를 선택할 때 고려해 야 할 다른 요소도](https://technet.microsoft.com/library/jj573653.aspx)있습니다. ADFS 옵션을 사용 하려면 몇 가지 추가 구성 단계가 필요 합니다.

클라우드에 해시를 저장 하도록 선택 하면 작업이 완료 되 고 **다음**을 클릭 하면 도구가 디렉터리 동기화를 시작 합니다.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image18.png)

몇 분 내에 완료 되었습니다.

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image19.png)

Windows 2003 이상에서는 조직의 한 도메인 컨트롤러 에서만이를 실행 해야 합니다. 다시 부팅할 필요가 없습니다. 완료 되 면 모든 사용자가 클라우드에 있으며 SAML, OAuth 또는 WS를 사용 하 여 모든 웹 또는 모바일 응용 프로그램에서 Single Sign-On을 수행할 수 있습니다.

Microsoft에서이를 어떻게 보호 하 고 있는지에 대해 묻는 메시지가 표시 되는 경우가 있습니다. Microsoft는 자신의 중요 한 비즈니스 데이터에 대해이를 사용 정답은 예입니다. 예를 들어 [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)에서 내부 Microsoft SharePoint 사이트로 이동 하는 경우 로그인 하 라는 메시지가 표시 됩니다.

![Office 365 로그인](single-sign-on/_static/image20.png)

Microsoft는 ADFS를 사용 하도록 설정 했으므로 Microsoft ID를 입력 하면 ADFS 로그인 페이지로 리디렉션됩니다.

![ADFS 로그인](single-sign-on/_static/image21.png)

그리고 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 한 후에는이 내부 응용 프로그램에 액세스할 수 있습니다.

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

AD 로그인 서버는 주로 Azure AD를 사용할 수 있게 되기 전에 ADFS를 설정 했지만 로그인 프로세스가 클라우드의 Azure AD 디렉터리를 통과 하기 때문에 사용 됩니다. Microsoft는 중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서 등을 클라우드에 저장 하 고 이와 똑같은 솔루션을 사용 하 여 보안을 유지 합니다.

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>Single Sign-On에 Azure AD를 사용 하는 ASP.NET 앱 만들기

Visual Studio를 사용 하면 몇 가지 스크린샷에서 볼 수 있는 것 처럼 Single Sign-On 위해 Azure AD를 사용 하는 앱을 매우 쉽게 만들 수 있습니다.

MVC 또는 Web Forms 새 ASP.NET 응용 프로그램을 만드는 경우 기본 인증 방법이 ASP.NET Identity 됩니다. Azure AD로 변경 하려면 **인증 변경** 단추를 클릭 합니다.

![인증 변경](single-sign-on/_static/image23.png)

조직 계정을 선택 하 고 도메인 이름을 입력 한 다음 Single Sign On을 선택 합니다.

![인증 구성 대화 상자](single-sign-on/_static/image24.png)

디렉터리 데이터에 대 한 읽기 또는 읽기/쓰기 권한을 앱에 제공할 수도 있습니다. 이렇게 하는 경우 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) 를 사용 하 여 사용자의 전화 번호를 조회 하 고, 사무실에 있는지, 마지막으로 로그온 할 때를 확인할 수 있습니다.

모든 작업을 수행 해야 합니다.-Visual Studio는 Azure AD 테 넌 트의 관리자에 대 한 자격 증명을 요청 하 고 새 응용 프로그램에 대해 프로젝트와 Azure AD 테 넌 트를 모두 구성 합니다.

프로젝트를 실행 하면 로그인 페이지가 표시 되며 Azure AD 디렉터리에서 사용자의 자격 증명을 사용 하 여 로그인 할 수 있습니다.

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인 됨](single-sign-on/_static/image26.png)

Azure에 앱을 배포 하는 경우에는 **조직 인증 사용** 확인란만 선택 하면 됩니다. 그러면 Visual Studio에서 모든 구성을 처리 합니다.

![웹 게시](single-sign-on/_static/image27.png)

이러한 스크린샷은 Azure AD 인증을 사용 하는 앱을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공 됩니다. [Azure Active Directory로 ASP.NET Apps 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).

## <a name="summary"></a>요약

이 장에서는 Azure Active Directory, Visual Studio 및 ASP.NET를 확인 하 여 조직의 사용자를 위한 인터넷 응용 프로그램에서 Single Sign-On를 쉽게 설정할 수 있습니다. 사용자는 내부 네트워크에서 Active Directory를 사용 하 여 로그온 하는 데 사용 하는 것과 동일한 자격 증명을 사용 하 여 인터넷 앱에서 로그온 할 수 있습니다.

[다음 장에서](data-storage-options.md) 는 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.

<a id="resources"></a>
## <a name="resources"></a>자료

자세한 내용은 다음 참고 자료를 참조하십시오.

- [설명서를 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/). Windowsazure.com 사이트의 Azure AD 설명서에 대 한 포털 페이지입니다. 단계별 자습서는 **개발** 섹션을 참조 하세요.
- [Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/). Azure의 multi-factor authentication에 대 한 설명서를 위한 포털 페이지입니다.
- [조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)입니다. Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션에 대 한 설명입니다.
- [Microsoft 패턴 및 사례-페더레이션 Id 패턴](https://msdn.microsoft.com/library/dn589790.aspx).
- [방법: Azure Active Directory Sync 도구를 설치](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.
- [Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx). ADFS 2.0에 대 한 설명서 링크입니다.
- [Windows AZURE AD 응용 프로그램의 역할 기반 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1) 응용 프로그램 샘플.
- [Graph API 블로그를 Azure Active Directory](https://blogs.msdn.com/b/aadgraphteam/)합니다.
- [하이브리드 Id 인프라에서 BYOD 및 디렉터리 통합을 Access Control](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다. Gayana Bagdasaryan의 기술 Ed 2014 세션 비디오입니다.

> [!div class="step-by-step"]
> [이전](web-development-best-practices.md)
> [다음](data-storage-options.md)
