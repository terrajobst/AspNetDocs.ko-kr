---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 ASP.NET 웹 응용 프로그램을 Azure App Service Web Apps 또는 타사 호스팅 공급자에 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640231"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Visual Studio를 사용 하 여 ASP.NET 웹 배포: 소개

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 이 자습서 시리즈에서는 Azure SDK for .NET과 함께 Visual Studio 2012을 사용 하 여 Azure App Service Web Apps 또는 타사 호스팅 공급자에 게 ASP.NET 웹 응용 프로그램을 배포 (게시) 하는 방법을 보여 줍니다. 대부분의 절차는 Visual Studio 2013와 비슷합니다.
> 
> 인터넷을 통해 사용자가 사용할 수 있도록 하기 위해 웹 응용 프로그램을 개발 합니다. 그러나 웹 프로그래밍 자습서는 일반적으로 개발 컴퓨터에서 작업을 수행 하는 방법을 본 후 바로 중지 됩니다. 이러한 일련의 자습서는 다른 사용자가 나갈 때 시작 합니다. 웹 앱을 빌드하고 테스트 했 고 준비가 완료 되었습니다. 새로운 기능 이러한 자습서는 테스트를 위해 로컬 개발 컴퓨터의 IIS에 먼저 배포 하 고 나 서 스테이징 및 프로덕션을 위해 Azure 또는 타사 호스팅 공급자를 배포 하는 방법을 보여 줍니다. 배포할 샘플 응용 프로그램은 Entity Framework, SQL Server 및 ASP.NET 멤버 자격 시스템을 사용 하는 웹 응용 프로그램 프로젝트입니다. 샘플 응용 프로그램은 ASP.NET Web Forms를 사용 하지만, 표시 된 절차는 ASP.NET MVC 및 Web API에도 적용 됩니다.
> 
> 이 자습서에서는 Visual Studio에서 ASP.NET로 작업 하는 방법을 알고 있다고 가정 합니다. 그렇지 않은 경우 [기본 ASP.NET Web Forms 자습서](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)를 시작 하는 것이 좋습니다.
> 
> 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET Deployment 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) 또는 [stackoverflow](http://stackoverflow.com)에 게시할 수 있습니다.
> 
> 이 콘텐츠는 [TechNet 전자 서적 갤러리](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)에서 무료 전자로도 제공 됩니다.

## <a name="overview"></a>개요

이러한 자습서에서는 SQL Server 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램을 배포 하는 과정을 안내 합니다. 먼저 테스트를 위해 로컬 개발 컴퓨터의 IIS에 배포 하 고 스테이징 및 프로덕션에 대 한 Azure App Service 및 Azure SQL Database Web Apps 합니다. Visual Studio를 사용 하 여 배포 하는 방법을 확인할 수 있습니다. 한 번 클릭 게시를 사용 하면 명령줄을 사용 하 여 배포 하는 방법을 확인할 수 있습니다.

이 자습서의 수를 통해 배포 프로세스를 어렵게 만들 수 있습니다. 실제로 기본 절차는 간단 합니다. 그러나 실제 상황에서는 추가 배포 작업 (예: 대상 서버에 대 한 폴더 사용 권한 설정)을 수행 해야 하는 경우가 많습니다. 이러한 추가 작업 중 일부를 설명 했지만,이 자습서에서는 실제 응용 프로그램을 성공적으로 배포 하지 못하게 하는 정보를 제외 하는 데 도움이 될 것입니다.

자습서는 순서 대로 실행 되도록 설계 되었으며 각 부품은 이전 파트를 기반으로 합니다. 상황과 관련이 없는 파트는 건너뛸 수 있지만 이후 자습서의 절차를 조정 해야 할 수도 있습니다.

## <a name="intended-audience"></a>대상 사용자

이 자습서는 다음과 같은 환경에서 작업 하는 ASP.NET 개발자를 대상으로 합니다.

- 프로덕션 환경은 Azure App Service Web Apps 또는 타사 호스팅 공급자입니다.
- 배포는 연속 통합 프로세스로 제한 되지 않지만 Visual Studio에서 직접 수행할 수 있습니다.

명령줄에서 배포 하는 방법을 보여 주는 자습서를 제외 하 고 [연속 배달](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 프로세스를 사용 하 여 [원본 제어](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) 에서 배포 하는 것은 이러한 자습서에서 다루지 않습니다. 지속적인 업데이트에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [지속적인 통합 및 지속적인 업데이트 (Microsoft Azure를 사용 하 여 실제 클라우드 앱 빌드)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Azure App Service에서 웹 앱 배포](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (엔터프라이즈 환경에 유용한 정보를 포함 하는 Visual Studio 2010 용으로 작성 된 이전 자습서 집합)

## <a name="using-a-third-party-hosting-provider"></a>타사 호스팅 공급자 사용

이 자습서에서는 Azure 계정을 설정 하 고 스테이징 및 프로덕션을 위해 Azure App Service에서 Web Apps 하는 응용 프로그램을 배포 하는 과정을 안내 합니다. 그러나 선택한 타사 호스팅 공급자에 배포 하는 데 동일한 기본 절차를 사용할 수 있습니다. 자습서에서 Azure에 고유한 프로세스를 진행 하는 경우이에 대해 설명 하 고 타사 호스팅 공급자에서 예측할 수 있는 차이점을 알려 주십시오.

## <a name="deploying-web-app-projects"></a>웹 앱 프로젝트 배포

이러한 자습서에 대해 다운로드 하 여 배포 하는 샘플 응용 프로그램은 Visual Studio 웹 응용 프로그램 프로젝트입니다. 그러나 최신 버전의 Visual Studio 용 웹 게시 업데이트를 설치 하는 경우 웹 앱 프로젝트에 동일한 배포 방법 및 도구를 사용할 수 있습니다.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트 배포

응용 프로그램 예제는 ASP.NET Web Forms 프로젝트 이지만, 수행 하는 방법에 대 한 자세한 내용은 ASP.NET MVC에도 적용 됩니다. Visual Studio MVC 프로젝트는 또 다른 형태의 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은 ASP.NET MVC 또는 대상 버전을 지원 하지 않는 호스팅 공급자에 배포 하는 경우 프로젝트에 적절 한 ([mvc 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0), [Mvc 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)또는 [mvc 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)) NuGet 패키지를 설치 했는지 확인 해야 한다는 것입니다.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램에서는 C# 를 사용 하지만 자습서에는에 대 C#한 지식이 필요 하지 않으며 자습서에서 설명 하는 배포 기술은 언어별로 특정 하지 않습니다.

## <a name="database-deployment-methods"></a>데이터베이스 배포 방법

Visual Studio에서 웹 배포와 함께 SQL Server 데이터베이스를 배포 하는 방법에는 세 가지가 있습니다.

- Entity Framework Code First 마이그레이션
- DbDacFx 웹 배포 공급자
- DbFullSql 웹 배포 공급자

이 자습서에서는 이러한 두 가지 방법 중 처음 두 가지를 사용 합니다. DbFullSql 웹 배포 공급자는 SQL Server Compact에서 SQL Server로 마이그레이션하는 것과 같은 일부 특정 시나리오를 제외 하 고 더 이상 권장 되지 않는 레거시 방법입니다.

이 자습서에 표시 된 방법은 SQL Server 데이터베이스에 대 한 것 이며 SQL Server Compact 되지 않습니다. SQL Server Compact 데이터베이스를 배포 하는 방법에 대 한 자세한 내용은 [SQL Server Compact를 사용 하 여 Visual Studio 웹 배포](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)를 참조 하세요.

이 자습서에 표시 된 메서드를 사용 하려면 웹 배포 publish 메서드를 사용 해야 합니다. FTP, 파일 시스템 또는 FPSE와 같은 다른 게시 방법을 선호 하는 경우 Visual Studio 및 ASP.NET 용 웹 배포 콘텐츠 맵에서 [웹 응용 프로그램 배포와 별도로 데이터베이스 배포](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) 를 참조 하세요.

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 마이그레이션

Entity Framework 버전 4.3에서는 Microsoft가 Code First 마이그레이션를 도입 했습니다. Code First 마이그레이션는 데이터 모델에 대 한 증분 변경을 수행 하 고 이러한 변경 내용을 데이터베이스에 전파 하는 프로세스를 자동화 합니다. 이전 버전의 Code First에서는 일반적 Entity Framework으로 데이터 모델을 변경할 때마다 데이터베이스를 삭제 하 고 다시 만들 수 있습니다. 이는 테스트 데이터를 쉽게 다시 만들지만 프로덕션 환경에서는 일반적으로 데이터베이스를 삭제 하지 않고 데이터베이스 스키마를 업데이트 하려는 경우에는 개발에 문제가 되지 않습니다. 마이그레이션 기능을 사용 하면 Code First는 데이터베이스를 삭제 하 고 다시 만들지 않고 데이터베이스를 업데이트할 수 있습니다. 필요한 스키마 변경을 수행 하는 방법을 자동으로 결정 하거나 변경 내용을 사용자 지정 하는 코드를 작성할 수 Code First 있습니다. Code First 마이그레이션에 대 한 소개는 [Code First 마이그레이션](https://msdn.microsoft.com/library/hh770484.aspx)를 참조 하세요.

웹 프로젝트를 배포 하는 경우 Visual Studio는 Code First 마이그레이션로 관리 되는 데이터베이스를 배포 하는 프로세스를 자동화할 수 있습니다. 게시 프로필을 만들 때 Code First 마이그레이션 실행 (응용 프로그램 시작 시 실행) 이라는 레이블이 지정 된 확인란을 선택 합니다. 이 설정을 사용 하면 Code First에서 `MigrateDatabaseToLatestVersion` 이니셜라이저 클래스를 사용 하도록 배포 프로세스에서 대상 서버에 응용 프로그램 Web.config 파일을 자동으로 구성 합니다.

Visual Studio는 배포 프로세스 중에 데이터베이스에서 어떤 작업도 수행 하지 않습니다. 배포 된 응용 프로그램이 배포 후 처음으로 데이터베이스에 액세스 하는 경우 Code First에서 자동으로 데이터베이스를 만들거나 데이터베이스 스키마를 최신 버전으로 업데이트 합니다. 응용 프로그램이 마이그레이션 초기값 메서드를 구현 하는 경우이 메서드는 데이터베이스가 만들어지거나 스키마가 업데이트 된 후에 실행 됩니다.

이 자습서에서는 Code First 마이그레이션를 사용 하 여 응용 프로그램 데이터베이스를 배포 합니다.

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx 웹 배포 공급자

Entity Framework Code First를 통해 관리 되지 않는 SQL Server 데이터베이스의 경우 게시 프로필을 구성할 때 데이터베이스 업데이트 라는 확인란을 선택할 수 있습니다. 초기 배포 중에 dbDacFx 공급자는 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 테이블 및 기타 데이터베이스 개체를 만듭니다. 이후 배포에서 공급자는 원본 데이터베이스와 대상 데이터베이스 간의 차이점을 확인 하 고 원본 데이터베이스와 일치 하도록 대상 데이터베이스의 스키마를 업데이트 합니다. 기본적으로 공급자는 테이블이 나 열이 삭제 되는 경우와 같이 데이터 손실을 유발 하는 변경 작업을 수행 하지 않습니다.

이 방법은 데이터베이스 테이블의 데이터 배포를 자동화 하지 않지만이를 수행 하는 스크립트를 만들고 배포 중에 Visual Studio를 실행 하도록 구성할 수 있습니다. 배포 중에 스크립트를 실행 하는 또 다른 이유는 데이터가 손실 될 수 있으므로 스키마 변경을 자동으로 수행 하는 것입니다.

이 자습서에서는 dbDacFx 공급자를 사용 하 여 ASP.NET 멤버 자격 데이터베이스를 배포 합니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트가 제대로 실행 되지 않으면 오류 메시지에서 항상 명확한 해결책을 제공 하지는 않습니다. 몇 가지 일반적인 문제 시나리오를 돕기 위해 [문제 해결 참조 페이지](troubleshooting.md) 를 사용할 수 있습니다. 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>의견 시작

자습서에 대 한 설명은 환영 하며 자습서를 업데이트할 때 자습서 설명에서 제공 되는 향상 된 기능에 대 한 제안 또는 제안 사항을 고려 하기 위해 모든 작업이 수행 됩니다.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

이 자습서는 다음 제품에 대해 작성 되었습니다.

- Windows 8 또는 Windows 7
- [최신 업데이트가](https://go.microsoft.com/fwlink/?LinkId=272486)포함 된 visual studio 2012 또는 visual Studio 2012 Express for Web
- [Visual Studio 용 Azure SDK 2012](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio 2010 SP1 또는 Visual Studio 2013를 사용 하 여이 자습서를 수행할 수 있지만 일부 스크린 샷을 다르게 제공 되며 일부 기능이 다를 수 있습니다.

Visual Studio 2013를 사용 하는 경우 [Visual Studio 2013 용 AZURE SDK](https://go.microsoft.com/fwlink/?LinkID=324322)를 설치 합니다.

Visual Studio 2010 s p 1을 사용 하는 경우 다음 소프트웨어를 설치 합니다.

- [Visual Studio 용 Azure SDK 2010](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx).

컴퓨터에 이미 있는 SDK 종속성의 수에 따라 Azure SDK를 설치 하는 데 몇 분에서 30 분 이상까지 시간이 오래 걸릴 수 있습니다. SDK가 Visual Studio 웹 게시 기능에 대 한 최신 업데이트를 포함 하기 때문에 Azure 대신 타사 호스팅 공급자에 게시할 계획인 경우에도 Azure SDK가 필요 합니다.

> [!NOTE]
> 이 자습서는 Azure SDK의 버전 1.8.1을 사용 하 여 작성 되었습니다. 이후 추가 기능이 포함 된 최신 버전이 릴리스 되었습니다. 이 자습서에서는 이러한 기능에 대해 자세히 설명 하 고 리소스에 대 한 링크를 제공 하도록 업데이트 되었습니다.

지침 및 스크린샷은 Windows 8을 기반으로 하지만 자습서에서는 Windows 7에 대 한 차이점을 설명 합니다.

자습서를 완료 하기 위해 다른 소프트웨어가 필요 하지만 아직 설치 하지 않아도 됩니다. 이 자습서에서는 필요할 때 설치 하는 단계를 안내 합니다.

## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

배포할 응용 프로그램은 Contoso 대학 이라고 하며 이미 생성 되었습니다. [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)에 설명 된 Contoso 대학 응용 프로그램을 느슨하게 기반으로 하는 대학 웹 사이트의 단순화 된 버전입니다.

필수 구성 요소가 설치 되어 있는 경우 [Contoso 대학 웹 응용 프로그램](https://go.microsoft.com/fwlink/p/?LinkId=282627)을 다운로드 합니다. *.Zip* 파일에는 여러 버전의 프로젝트가 포함 되어 있습니다. 자습서의 단계를 수행 하려면 C# 폴더에 있는 프로젝트부터 시작 합니다. 자습서의 끝에서 프로젝트가 표시 되는 모양을 확인 하려면 ContosoUniversity 폴더에서 프로젝트를 엽니다.

자습서 단계를 진행 하기 위해 프로젝트를 준비 하려면 다음 단계를 수행 합니다.

1. ContosoUniversity 솔루션 파일 C# 을 Visual Studio 프로젝트 작업에 사용 하는 폴더에 관계 없이 폴더의 ContosoUniversity 폴더에 저장 합니다.

    기본적으로 Visual Studio 2012에 대 한 다음 폴더는 다음과 같습니다.

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (이 자습서의 스크린 샷에서 프로젝트 폴더는 `C`: 드라이브의 루트 디렉터리에 있습니다.)
2. Visual Studio를 시작 하 고 프로젝트를 엽니다.
3. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **Enablenuget Restore 가져오기**를 클릭 합니다.
4. 솔루션을 빌드합니다.
5. 컴파일 오류가 발생 하면 NuGet 패키지를 수동으로 복원 합니다.

    1. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **솔루션용 NuGet 패키지 관리**를 클릭 합니다.
    2. **Nuget 패키지 관리** 대화 상자의 맨 위에서 **이 솔루션에 일부 NuGet 패키지가 누락 된 것을 볼 수 있습니다. 복원 하려면 클릭 합니다.** **복원** 단추를 클릭 합니다.
    3. 솔루션을 다시 빌드합니다.
6. Ctrl+F5를 눌러 응용 프로그램을 실행합니다.

    응용 프로그램이 Contoso 대학 홈 페이지에 열립니다.

    ![홈페이지 개발](introduction/_static/image1.png)

    (Visual Studio에서 SQL Server Express LocalDB 인스턴스를 시작 하는 동안 대기 시간이 있을 수 있으며, 프로세스가 너무 오래 걸리는 경우 시간 초과 오류가 발생할 수 있습니다. 이 경우 프로젝트를 다시 시작 합니다.

웹 사이트 페이지는 메뉴 모음에서 액세스할 수 있으며 다음과 같은 기능을 수행할 수 있습니다.

- 학생 통계 (정보 페이지)를 표시 합니다.
- 학생을 표시 하 고, 편집 하 고, 삭제 하 고, 추가 합니다.
- 코스를 표시 하 고 편집 합니다.
- 강사를 표시 하 고 편집 합니다.
- 부서를 표시 하 고 편집 합니다.

몇 가지 대표적인 페이지의 스크린샷은 다음과 같습니다.

![학생 페이지 개발](introduction/_static/image2.png)

![학생 페이지 개발자 추가](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능 검토

응용 프로그램의 다음 기능은 응용 프로그램을 배포 하는 방법 또는 배포를 위해 수행 해야 하는 작업에 영향을 줍니다. 이러한 각 항목은 시리즈의 다음 자습서에 자세히 설명 되어 있습니다.

- Contoso 대학은 SQL Server 데이터베이스를 사용 하 여 학생 및 강사 이름과 같은 응용 프로그램 데이터를 저장 합니다. 데이터베이스에는 테스트 데이터와 프로덕션 데이터가 혼합 되어 있으며 프로덕션 환경에 배포 하는 경우 테스트 데이터를 제외 해야 합니다.
- 응용 프로그램은 SQL Server 데이터베이스에 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 합니다. 응용 프로그램은 일부 제한 된 정보에 대 한 액세스 권한이 있는 관리자 사용자를 정의 합니다. 관리자 계정을 사용 하 여 테스트 계정을 제외 하 고 멤버 자격 데이터베이스를 배포 해야 합니다.
- 응용 프로그램은 타사 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 해야 하는 어셈블리에 제공 됩니다.
- 오류 로깅 유틸리티는 XML 파일의 오류 정보를 파일 폴더에 기록 합니다. 배포 된 사이트에서 ASP.NET가 실행 되는 계정에이 폴더에 대 한 쓰기 권한이 있는지 확인 하 고 배포에서이 폴더를 제외 해야 합니다. 그렇지 않으면 테스트 환경의 오류 로그 데이터가 프로덕션에 배포 될 수 있으며 프로덕션 오류 로그 파일이 삭제 될 수 있습니다.
- 응용 프로그램에는 대상 환경 (테스트, 스테이징 또는 프로덕션) 및 빌드 구성 (디버그 또는 릴리스)에 따라 변경 되어야 하는 기타 설정에 따라 배포 된 *web.config* 파일에서 변경 해야 하는 일부 설정이 포함 되어 있습니다.
- Visual Studio 솔루션에는 클래스 라이브러리 프로젝트가 포함 되어 있습니다. 이 프로젝트가 생성 하는 어셈블리만 프로젝트 자체가 아닌 배포 해야 합니다.

## <a name="summary"></a>요약

시리즈의이 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 하 고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 했습니다. 다음 자습서에서는 이러한 항목 중 일부를 자동으로 처리 하도록 설정 하 여 배포를 준비 합니다. 다른 사용자는 수동으로 처리 합니다.

> [!div class="step-by-step"]
> [다음](preparing-databases.md)
