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
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a><span data-ttu-id="32ffc-104">Single Sign-on (Azure를 사용 하 여 실제 클라우드 앱 빌드)</span><span class="sxs-lookup"><span data-stu-id="32ffc-104">Single Sign-On (Building Real-World Cloud Apps with Azure)</span></span>

<span data-ttu-id="32ffc-105">사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="32ffc-105">by [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="32ffc-106">[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="32ffc-106">[Download Fix It Project](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) or [Download E-book](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)</span></span>

> <span data-ttu-id="32ffc-107">Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-107">The **Building Real World Cloud Apps with Azure** e-book is based on a presentation developed by Scott Guthrie.</span></span> <span data-ttu-id="32ffc-108">클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-108">It explains 13 patterns and practices that can help you be successful developing web apps for the cloud.</span></span> <span data-ttu-id="32ffc-109">전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32ffc-109">For information about the e-book, see [the first chapter](introduction.md).</span></span>

<span data-ttu-id="32ffc-110">클라우드 앱을 개발 하는 경우에는 많은 보안 문제가 발생 하지만,이 시리즈의 경우에는 Single Sign-On에만 초점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-110">There are many security issues to think about when you're developing a cloud app, but for this series we'll focus on just one: single sign-on.</span></span> <span data-ttu-id="32ffc-111">자주 묻는 질문은 다음과 같습니다. "회사 직원을 위한 앱을 주로 빌드하고 있습니다. 이러한 앱을 클라우드에서 호스트 하 고 방화벽 내에서 호스트 되는 앱을 실행 하는 동안 내 직원이 알고 있으며 온-프레미스 환경에서 사용 하는 동일한 보안 모델을 사용할 수 있게 하려면 어떻게 해야 하나요? "</span><span class="sxs-lookup"><span data-stu-id="32ffc-111">A question people often ask is this: "I'm primarily building apps for the employees of my company; how do I host these apps in the cloud and still enable them to use the same security model that my employees know and use in the on-premises environment when they're running apps that are hosted inside the firewall?"</span></span> <span data-ttu-id="32ffc-112">이 시나리오를 사용 하도록 설정 하는 방법 중 하나를 Azure AD (Azure Active Directory) 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-112">One of the ways we enable this scenario is called Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="32ffc-113">Azure AD를 사용 하면 인터넷을 통해 사용할 수 있는 엔터프라이즈급 LOB (기간 업무) 앱을 만들 수 있으며, 이러한 앱을 비즈니스 파트너에 게 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-113">Azure AD enables you to make enterprise line-of-business (LOB) apps available over the Internet, and it enables you to make these apps available to business partners as well.</span></span>

## <a name="introduction-to-azure-ad"></a><span data-ttu-id="32ffc-114">Azure AD 소개</span><span class="sxs-lookup"><span data-stu-id="32ffc-114">Introduction to Azure AD</span></span>

<span data-ttu-id="32ffc-115">[AZURE AD](https://docs.microsoft.com/azure/active-directory/) 는 클라우드에서 [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-115">[Azure AD](https://docs.microsoft.com/azure/active-directory/) provides [Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) in the cloud.</span></span> <span data-ttu-id="32ffc-116">주요 기능에는 다음이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-116">Key features include the following:</span></span>

- <span data-ttu-id="32ffc-117">온-프레미스 Active Directory와 통합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-117">It integrates with on-premises Active Directory.</span></span>
- <span data-ttu-id="32ffc-118">앱을 사용 하 여 Single Sign-On 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-118">It enables single sign-on with your apps.</span></span>
- <span data-ttu-id="32ffc-119">[SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-급지됨](http://en.wikipedia.org/wiki/WS-Federation)및 [OAuth 2.0](http://oauth.net/2/)와 같은 오픈 표준을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-119">It supports open standards such as [SAML](http://en.wikipedia.org/wiki/SAML_2.0), [WS-Fed](http://en.wikipedia.org/wiki/WS-Federation), and [OAuth 2.0](http://oauth.net/2/).</span></span>
- <span data-ttu-id="32ffc-120">Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-120">It supports Enterprise [Graph REST API](https://msdn.microsoft.com/library/hh974476.aspx).</span></span>

<span data-ttu-id="32ffc-121">직원 들이 인트라넷 앱에 로그온 할 수 있도록 하는 온-프레미스 Windows Server Active Directory 환경이 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-121">Suppose you have an on-premises Windows Server Active Directory environment that you use to enable employees to sign on to Intranet apps:</span></span>

![](single-sign-on/_static/image1.png)

<span data-ttu-id="32ffc-122">Azure AD를 사용 하 여 클라우드에서 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-122">What Azure AD enables you to do is create a directory in the cloud.</span></span> <span data-ttu-id="32ffc-123">무료 기능이 며 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-123">It's a free feature and easy to set up.</span></span>

<span data-ttu-id="32ffc-124">온-프레미스 Active Directory와 완전히 다를 수 있습니다. 원하는 모든 사용자를 추가 하 고 인터넷 앱에서 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-124">It can be entirely independent from your on-premises Active Directory; you can put anyone you want in it and authenticate them in Internet apps.</span></span>

![Microsoft Azure Active Directory](single-sign-on/_static/image2.png)

<span data-ttu-id="32ffc-126">또는 온-프레미스 AD와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-126">Or you can integrate it with your on-premises AD.</span></span>

![AD 및 WAAD 통합](single-sign-on/_static/image3.png)

<span data-ttu-id="32ffc-128">이제 온-프레미스에서 인증을 받을 수 있는 모든 직원은 인터넷을 통해 인증할 수도 있습니다. 즉, 방화벽을 열거나 데이터 센터에 새 서버를 배포 하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-128">Now all the employees who can authenticate on-premises can also authenticate over the Internet – without you having to open up a firewall or deploy any new servers in your data center.</span></span> <span data-ttu-id="32ffc-129">현재 알고 있는 기존 Active Directory 환경을 계속 활용 하 여 내부 앱에 single sign-on 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-129">You can continue to leverage all the existing Active Directory environment that you know and use today to give your internal apps single-sign on capability.</span></span>

<span data-ttu-id="32ffc-130">AD와 Azure AD 간에이 연결을 설정한 후에는 웹 앱과 모바일 장치에서 클라우드의 직원을 인증 하도록 설정 하 고 Office 365, SalesForce.com 또는 Google apps와 같은 타사 앱을 사용 하도록 설정 하 여 다음을 허용할 수 있습니다. 직원 자격 증명.</span><span class="sxs-lookup"><span data-stu-id="32ffc-130">Once you've made this connection between AD and Azure AD, you can also enable your web apps and your mobile devices to authenticate your employees in the cloud, and you can enable third-party apps, such as Office 365, SalesForce.com, or Google apps, to accept your employees' credentials.</span></span> <span data-ttu-id="32ffc-131">Office 365에서 인증 및 권한 부여에 Azure AD를 사용 하기 때문에 Office 365를 사용 하는 경우 이미 Azure AD를 사용 하 여 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-131">If you're using Office 365, you're already set up with Azure AD because Office 365 uses Azure AD for authentication and authorization.</span></span>

![타사 앱](single-sign-on/_static/image4.png)

<span data-ttu-id="32ffc-133">이 방법의 장점은 조직이 사용자를 추가 또는 삭제 하거나 사용자가 암호를 변경 하는 경우 온-프레미스 환경에서 현재 사용 하는 것과 동일한 프로세스를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-133">The beauty of this approach is that any time your organization adds or deletes a user, or a user changes a password, you use the same process that you use today in your on-premises environment.</span></span> <span data-ttu-id="32ffc-134">모든 온-프레미스 AD 변경 내용은 클라우드 환경에 자동으로 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-134">All of your on-premises AD changes are automatically propagated to the cloud environment.</span></span>

<span data-ttu-id="32ffc-135">회사에서을 사용 하거나 Office 365로 이동 하는 경우 Office 365에서 인증에 Azure AD를 사용 하기 때문에 Azure AD를 자동으로 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-135">If your company is using or moving to Office 365, the good news is that you'll have Azure AD set up automatically because Office 365 uses Azure AD for authentication.</span></span> <span data-ttu-id="32ffc-136">따라서 Office 365에서 사용 하는 것과 동일한 인증을 자신의 앱에서 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-136">So you can easily use in your own apps the same authentication that Office 365 uses.</span></span>

## <a name="set-up-an-azure-ad-tenant"></a><span data-ttu-id="32ffc-137">Azure AD 테 넌 트 설정</span><span class="sxs-lookup"><span data-stu-id="32ffc-137">Set up an Azure AD tenant</span></span>

<span data-ttu-id="32ffc-138">azure ad 디렉터리를 Azure AD [테 넌 트](https://technet.microsoft.com/library/jj573650.aspx)라고 하며, 테 넌 트를 설정 하는 작업은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-138">an Azure AD directory is called an Azure AD [tenant](https://technet.microsoft.com/library/jj573650.aspx), and setting up a tenant is pretty easy.</span></span> <span data-ttu-id="32ffc-139">개념을 설명 하기 위해 Azure 관리 포털에서 작업을 수행 하는 방법을 보여 주지만 다른 포털 함수와 같은 스크립트나 관리 API를 사용 하 여 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-139">We'll show you how it's done in the Azure Management Portal in order to illustrate the concepts, but of course like the other portal functions you can also do it by using a script or management API.</span></span>

<span data-ttu-id="32ffc-140">관리 포털에서 Active Directory 탭을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-140">In the management portal click the Active Directory tab.</span></span>

![포털의 WAAD](single-sign-on/_static/image5.png)

<span data-ttu-id="32ffc-142">Azure 계정에 대해 하나의 Azure AD 테 넌 트가 자동으로 있고 페이지 맨 아래에 있는 **추가** 단추를 클릭 하 여 추가 디렉터리를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-142">You automatically have one Azure AD tenant for your Azure account, and you can click the **Add** button at the bottom of the page to create additional directories.</span></span> <span data-ttu-id="32ffc-143">예를 들어 테스트 환경 및 프로덕션 환경에 대해 하나를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-143">You might want one for a test environment and one for production, for example.</span></span> <span data-ttu-id="32ffc-144">새 디렉터리의 이름을 신중 하 게 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-144">Think carefully about what you name a new directory.</span></span> <span data-ttu-id="32ffc-145">디렉터리 이름을 사용 하는 경우 사용자 중 하나에 대해 이름을 다시 사용 하면 혼동을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-145">If you use your name for the directory and then you use your name again for one of the users, that can be confusing.</span></span>

![디렉터리 추가](single-sign-on/_static/image6.png)

<span data-ttu-id="32ffc-147">포털은이 환경 내에서 사용자를 만들고, 삭제 하 고, 관리할 수 있는 모든 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-147">The portal has full support for creating, deleting, and managing users within this environment.</span></span> <span data-ttu-id="32ffc-148">예를 들어 사용자를 추가 하려면 **사용자 탭으로 이동 하 여** **사용자 추가** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-148">For example, to add a user go to the **Users** tab and click the **Add User** button.</span></span>

![[사용자 추가] 단추](single-sign-on/_static/image7.png)

![사용자 추가 대화 상자](single-sign-on/_static/image8.png)

<span data-ttu-id="32ffc-151">이 디렉터리에만 존재 하는 새 사용자를 만들거나 Microsoft 계정을이 디렉터리의 사용자로 등록 하거나 다른 Azure AD 디렉터리의 사용자를이 디렉터리의 사용자로 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-151">You can create a new user who exists only in this directory, or you can register a Microsoft Account as a user in this directory, or register or a user from another Azure AD directory as a user in this directory.</span></span> <span data-ttu-id="32ffc-152">실제 디렉터리에서 기본 도메인은 ContosoTest.onmicrosoft.com입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-152">(In a real directory, the default domain would be ContosoTest.onmicrosoft.com.</span></span> <span data-ttu-id="32ffc-153">Contoso.com와 같이 사용자가 선택한 도메인을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-153">You can also use a domain of your own choosing, like contoso.com.)</span></span>

![사용자 유형](single-sign-on/_static/image9.png)

![사용자 추가 대화 상자](single-sign-on/_static/image10.png)

<span data-ttu-id="32ffc-156">사용자를 역할에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-156">You can assign the user to a role.</span></span>

![사용자 프로필](single-sign-on/_static/image11.png)

<span data-ttu-id="32ffc-158">임시 암호를 사용 하 여 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-158">And the account is created with a temporary password.</span></span>

![임시 암호](single-sign-on/_static/image12.png)

<span data-ttu-id="32ffc-160">이 방법을 만든 사용자는이 클라우드 디렉터리를 사용 하 여 웹 앱에 즉시 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-160">The users you create this way can immediately log in to your web apps using this cloud directory.</span></span>

<span data-ttu-id="32ffc-161">그러나 엔터프라이즈 Single Sign-On에 대 한 유용한 정보는 **디렉터리 통합** 탭입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-161">What's great for enterprise single sign-on, though, is the **Directory Integration** tab:</span></span>

![디렉터리 통합 탭](single-sign-on/_static/image13.png)

<span data-ttu-id="32ffc-163">디렉터리 통합을 사용 하도록 설정 하 고 [도구를 다운로드](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)하는 경우이 클라우드 디렉터리를 조직 내에서 이미 사용 중인 기존 온-프레미스 Active Directory와 동기화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-163">If you enable directory integration, and [download a tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx), you can sync this cloud directory with your existing on-premises Active Directory that you're already using inside your organization.</span></span> <span data-ttu-id="32ffc-164">그러면 디렉터리에 저장 된 모든 사용자가이 클라우드 디렉터리에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-164">Then all of the users stored in your directory will show up in this cloud directory.</span></span> <span data-ttu-id="32ffc-165">이제 클라우드 앱에서 기존 Active Directory 자격 증명을 사용 하 여 모든 직원을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-165">Your cloud apps can now authenticate all of your employees using their existing Active Directory credentials.</span></span> <span data-ttu-id="32ffc-166">이 모든 것은 무료입니다. 동기화 도구와 Azure AD 자체도 모두 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-166">And all this is free – both the sync tool and Azure AD itself.</span></span>

<span data-ttu-id="32ffc-167">도구는이 화면에서 볼 수 있는 것 처럼 쉽게 사용할 수 있는 마법사입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-167">The tool is a wizard that is easy to use, as you can see from these screen shots.</span></span> <span data-ttu-id="32ffc-168">이는 전체 지침이 아니라 기본 프로세스를 보여 주는 예제 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-168">These are not complete instructions, just an example showing you the basic process.</span></span> <span data-ttu-id="32ffc-169">자세한 방법에 대 한 자세한 내용은 챕터의 끝에 있는 [리소스](#resources) 섹션의 링크를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32ffc-169">For more detailed how-to-do-it information, see the links in the [Resources](#resources) section at the end of the chapter.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image14.png)

<span data-ttu-id="32ffc-171">**다음**을 클릭 하 고 Azure Active Directory 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-171">Click **Next**, and then enter your Azure Active Directory credentials.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image15.png)

<span data-ttu-id="32ffc-173">**다음**을 클릭 하 고 온-프레미스 AD 자격 증명을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-173">Click **Next**, and then enter your on-premises AD credentials.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image16.png)

<span data-ttu-id="32ffc-175">**다음**을 클릭 하 고 클라우드의 AD 암호 해시를 저장할 것인지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-175">Click **Next**, and then indicate if you want to store a hash of your AD passwords in the cloud.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image17.png)

<span data-ttu-id="32ffc-177">클라우드에 저장할 수 있는 암호 해시는 단방향 해시입니다. 실제 암호는 Azure AD에 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-177">The password hash that you can store in the cloud is a one-way hash; actual passwords are never stored in Azure AD.</span></span> <span data-ttu-id="32ffc-178">클라우드에 해시를 저장 하지 않을 경우 [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS)를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-178">If you decide against storing hashes in the cloud, you'll have to use [Active Directory Federation Services](https://technet.microsoft.com/library/hh831502.aspx) (ADFS).</span></span> <span data-ttu-id="32ffc-179">또한 ADFS를 사용할지 [여부를 선택할 때 고려해 야 할 다른 요소도](https://technet.microsoft.com/library/jj573653.aspx)있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-179">There are also [other factors to consider when choosing whether or not to use ADFS](https://technet.microsoft.com/library/jj573653.aspx).</span></span> <span data-ttu-id="32ffc-180">ADFS 옵션을 사용 하려면 몇 가지 추가 구성 단계가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-180">The ADFS option requires a few additional configuration steps.</span></span>

<span data-ttu-id="32ffc-181">클라우드에 해시를 저장 하도록 선택 하면 작업이 완료 되 고 **다음**을 클릭 하면 도구가 디렉터리 동기화를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-181">If you choose to store hashes in the cloud, you're done, and the tool starts synchronizing directories when you click **Next**.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image18.png)

<span data-ttu-id="32ffc-183">몇 분 내에 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-183">And in a few minutes you're done.</span></span>

![WAAD Sync 도구 구성 마법사](single-sign-on/_static/image19.png)

<span data-ttu-id="32ffc-185">Windows 2003 이상에서는 조직의 한 도메인 컨트롤러 에서만이를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-185">You only have to run this on one domain controller in the organization, on Windows 2003 or higher.</span></span> <span data-ttu-id="32ffc-186">다시 부팅할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-186">And no need to reboot.</span></span> <span data-ttu-id="32ffc-187">완료 되 면 모든 사용자가 클라우드에 있으며 SAML, OAuth 또는 WS를 사용 하 여 모든 웹 또는 모바일 응용 프로그램에서 Single Sign-On을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-187">When you're done, all of your users are in the cloud and you can do single sign-on from any web or mobile application, using SAML, OAuth, or WS-Fed.</span></span>

<span data-ttu-id="32ffc-188">Microsoft에서이를 어떻게 보호 하 고 있는지에 대해 묻는 메시지가 표시 되는 경우가 있습니다. Microsoft는 자신의 중요 한 비즈니스 데이터에 대해이를 사용</span><span class="sxs-lookup"><span data-stu-id="32ffc-188">Sometimes we get asked about how secure this is – does Microsoft use it for their own sensitive business data?</span></span> <span data-ttu-id="32ffc-189">정답은 예입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-189">And the answer is yes we do.</span></span> <span data-ttu-id="32ffc-190">예를 들어 [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)에서 내부 Microsoft SharePoint 사이트로 이동 하는 경우 로그인 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-190">For example, if you go to the internal Microsoft SharePoint site at [https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/), you get prompted to log in.</span></span>

![Office 365 로그인](single-sign-on/_static/image20.png)

<span data-ttu-id="32ffc-192">Microsoft는 ADFS를 사용 하도록 설정 했으므로 Microsoft ID를 입력 하면 ADFS 로그인 페이지로 리디렉션됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-192">Microsoft has enabled ADFS, so when you enter a Microsoft ID, you get redirected to an ADFS log-in page.</span></span>

![ADFS 로그인](single-sign-on/_static/image21.png)

<span data-ttu-id="32ffc-194">그리고 내부 Microsoft AD 계정에 저장 된 자격 증명을 입력 한 후에는이 내부 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-194">And once you enter credentials stored in an internal Microsoft AD account, you have access to this internal application.</span></span>

![MS SharePoint 사이트](single-sign-on/_static/image22.png)

<span data-ttu-id="32ffc-196">AD 로그인 서버는 주로 Azure AD를 사용할 수 있게 되기 전에 ADFS를 설정 했지만 로그인 프로세스가 클라우드의 Azure AD 디렉터리를 통과 하기 때문에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-196">We're using an AD sign-in server mainly because we already had ADFS set up before Azure AD became available, but the log-in process is going through an Azure AD directory in the cloud.</span></span> <span data-ttu-id="32ffc-197">Microsoft는 중요 한 문서, 소스 제어, 성능 관리 파일, 판매 보고서 등을 클라우드에 저장 하 고 이와 똑같은 솔루션을 사용 하 여 보안을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-197">We put our important documents, source control, performance management files, sales reports, and more, in the cloud and are using this exact same solution to secure them.</span></span>

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a><span data-ttu-id="32ffc-198">Single Sign-On에 Azure AD를 사용 하는 ASP.NET 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="32ffc-198">Create an ASP.NET app that uses Azure AD for single sign-on</span></span>

<span data-ttu-id="32ffc-199">Visual Studio를 사용 하면 몇 가지 스크린샷에서 볼 수 있는 것 처럼 Single Sign-On 위해 Azure AD를 사용 하는 앱을 매우 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-199">Visual Studio makes it really easy to create an app that uses Azure AD for single sign-on, as you can see from a few screen shots.</span></span>

<span data-ttu-id="32ffc-200">MVC 또는 Web Forms 새 ASP.NET 응용 프로그램을 만드는 경우 기본 인증 방법이 ASP.NET Identity 됩니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-200">When you create a new ASP.NET application, either MVC or Web Forms, the default authentication method is ASP.NET Identity.</span></span> <span data-ttu-id="32ffc-201">Azure AD로 변경 하려면 **인증 변경** 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-201">To change that to Azure AD, you click a **Change Authentication** button.</span></span>

![인증 변경](single-sign-on/_static/image23.png)

<span data-ttu-id="32ffc-203">조직 계정을 선택 하 고 도메인 이름을 입력 한 다음 Single Sign On을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-203">Select Organizational Accounts, enter your domain name, and then select Single Sign On.</span></span>

![인증 구성 대화 상자](single-sign-on/_static/image24.png)

<span data-ttu-id="32ffc-205">디렉터리 데이터에 대 한 읽기 또는 읽기/쓰기 권한을 앱에 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-205">You can also give the app read or read/write permission for directory data.</span></span> <span data-ttu-id="32ffc-206">이렇게 하는 경우 [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) 를 사용 하 여 사용자의 전화 번호를 조회 하 고, 사무실에 있는지, 마지막으로 로그온 할 때를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-206">If you do that, it can use the [Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx) to look up users' phone number, find out if they're in the office, when they last logged on, etc.</span></span>

<span data-ttu-id="32ffc-207">모든 작업을 수행 해야 합니다.-Visual Studio는 Azure AD 테 넌 트의 관리자에 대 한 자격 증명을 요청 하 고 새 응용 프로그램에 대해 프로젝트와 Azure AD 테 넌 트를 모두 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-207">That's all you have to do - Visual Studio asks for the credentials for an administrator for your Azure AD tenant, and then it configures both your project and your Azure AD tenant for the new application.</span></span>

<span data-ttu-id="32ffc-208">프로젝트를 실행 하면 로그인 페이지가 표시 되며 Azure AD 디렉터리에서 사용자의 자격 증명을 사용 하 여 로그인 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-208">When you run the project, you'll see a sign-in page, and you can sign in with credentials of a user in your Azure AD directory.</span></span>

![조직 계정 로그인](single-sign-on/_static/image25.png)

![로그인 됨](single-sign-on/_static/image26.png)

<span data-ttu-id="32ffc-211">Azure에 앱을 배포 하는 경우에는 **조직 인증 사용** 확인란만 선택 하면 됩니다. 그러면 Visual Studio에서 모든 구성을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-211">When you deploy the app to Azure, all you have to do is select an **Enable Organizational Authentication** check box, and once again Visual Studio takes care of all the configuration for you.</span></span>

![웹 게시](single-sign-on/_static/image27.png)

<span data-ttu-id="32ffc-213">이러한 스크린샷은 Azure AD 인증을 사용 하는 앱을 빌드하는 방법을 보여 주는 전체 단계별 자습서에서 제공 됩니다. [Azure Active Directory로 ASP.NET Apps 개발](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="32ffc-213">These screen shots come from a complete step-by-step tutorial that shows how to build an app that uses Azure AD authentication: [Developing ASP.NET Apps with Azure Active Directory](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md).</span></span>

## <a name="summary"></a><span data-ttu-id="32ffc-214">요약</span><span class="sxs-lookup"><span data-stu-id="32ffc-214">Summary</span></span>

<span data-ttu-id="32ffc-215">이 장에서는 Azure Active Directory, Visual Studio 및 ASP.NET를 확인 하 여 조직의 사용자를 위한 인터넷 응용 프로그램에서 Single Sign-On를 쉽게 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-215">In this chapter you saw that Azure Active Directory, Visual Studio, and ASP.NET, make it easy to set up single sign-on in Internet applications for your organization's users.</span></span> <span data-ttu-id="32ffc-216">사용자는 내부 네트워크에서 Active Directory를 사용 하 여 로그온 하는 데 사용 하는 것과 동일한 자격 증명을 사용 하 여 인터넷 앱에서 로그온 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-216">Your users can sign on in Internet apps using the same credentials they use to sign on using Active Directory in your internal network.</span></span>

<span data-ttu-id="32ffc-217">[다음 장에서](data-storage-options.md) 는 클라우드 앱에 사용할 수 있는 데이터 저장소 옵션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-217">The [next chapter](data-storage-options.md) looks at the data storage options available for a cloud app.</span></span>

<a id="resources"></a>
## <a name="resources"></a><span data-ttu-id="32ffc-218">자료</span><span class="sxs-lookup"><span data-stu-id="32ffc-218">Resources</span></span>

<span data-ttu-id="32ffc-219">자세한 내용은 다음 참고 자료를 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="32ffc-219">For more information, see the following resources:</span></span>

- <span data-ttu-id="32ffc-220">[설명서를 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="32ffc-220">[Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="32ffc-221">Windowsazure.com 사이트의 Azure AD 설명서에 대 한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-221">Portal page for Azure AD documentation on the windowsazure.com site.</span></span> <span data-ttu-id="32ffc-222">단계별 자습서는 **개발** 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="32ffc-222">For step by step tutorials, see the **Develop** section.</span></span>
- <span data-ttu-id="32ffc-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span><span class="sxs-lookup"><span data-stu-id="32ffc-223">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/).</span></span> <span data-ttu-id="32ffc-224">Azure의 multi-factor authentication에 대 한 설명서를 위한 포털 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-224">Portal page for documentation about multi-factor authentication in Azure.</span></span>
- <span data-ttu-id="32ffc-225">[조직 계정 인증 옵션](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-225">[Organizational account authentication options](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions).</span></span> <span data-ttu-id="32ffc-226">Visual Studio 2013 새 프로젝트 대화 상자에서 Azure AD 인증 옵션에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-226">Explanation of the Azure AD authentication options in the Visual Studio 2013 new-project dialog.</span></span>
- <span data-ttu-id="32ffc-227">[Microsoft 패턴 및 사례-페더레이션 Id 패턴](https://msdn.microsoft.com/library/dn589790.aspx).</span><span class="sxs-lookup"><span data-stu-id="32ffc-227">[Microsoft Patterns and Practices - Federated Identity Pattern](https://msdn.microsoft.com/library/dn589790.aspx).</span></span>
- <span data-ttu-id="32ffc-228">[방법: Azure Active Directory Sync 도구를 설치](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-228">[HowTo: Install the Azure Active Directory Sync Tool](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx).</span></span>
- <span data-ttu-id="32ffc-229">[Active Directory Federation Services 2.0 콘텐츠 맵](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span><span class="sxs-lookup"><span data-stu-id="32ffc-229">[Active Directory Federation Services 2.0 Content Map](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx).</span></span> <span data-ttu-id="32ffc-230">ADFS 2.0에 대 한 설명서 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-230">Links to documentation about ADFS 2.0.</span></span>
- <span data-ttu-id="32ffc-231">[Windows AZURE AD 응용 프로그램의 역할 기반 및 ACL 기반 권한 부여](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)</span><span class="sxs-lookup"><span data-stu-id="32ffc-231">[Role-Based and ACL-Based Authorization in a Windows Azure AD Application](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1).</span></span> <span data-ttu-id="32ffc-232">응용 프로그램 샘플.</span><span class="sxs-lookup"><span data-stu-id="32ffc-232">Sample application.</span></span>
- <span data-ttu-id="32ffc-233">[Graph API 블로그를 Azure Active Directory](https://blogs.msdn.com/b/aadgraphteam/)합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-233">[Azure Active Directory Graph API blog](https://blogs.msdn.com/b/aadgraphteam/).</span></span>
- <span data-ttu-id="32ffc-234">[하이브리드 Id 인프라에서 BYOD 및 디렉터리 통합을 Access Control](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)합니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-234">[Access Control in BYOD and Directory Integration in a Hybrid Identity Infrastructure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=).</span></span> <span data-ttu-id="32ffc-235">Gayana Bagdasaryan의 기술 Ed 2014 세션 비디오입니다.</span><span class="sxs-lookup"><span data-stu-id="32ffc-235">Tech Ed 2014 session video by Gayana Bagdasaryan.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="32ffc-236">[이전](web-development-best-practices.md)
> [다음](data-storage-options.md)</span><span class="sxs-lookup"><span data-stu-id="32ffc-236">[Previous](web-development-best-practices.md)
[Next](data-storage-options.md)</span></span>
