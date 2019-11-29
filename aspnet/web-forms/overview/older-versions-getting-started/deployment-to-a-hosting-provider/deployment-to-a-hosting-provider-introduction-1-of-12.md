---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'Visual Studio를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 소개-12 개 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈에서는 Visual Stu ...를 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587718"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>Visual Studio를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램 배포: 소개-12 개

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

[시작 프로젝트 다운로드](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 이 자습서 시리즈에서는 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC for Web을 사용 하 여 SQL Server Compact 데이터베이스를 포함 하는 ASP.NET 웹 응용 프로그램 프로젝트를 배포 (게시) 하는 방법을 보여 줍니다. 웹 게시 업데이트를 설치 하는 경우 Visual Studio 2010을 사용할 수도 있습니다.
> 
> Visual Studio 2012의 RC 릴리스 후에 도입 된 배포 기능을 보여 주는 자습서는 SQL Server Compact 이외의 SQL Server 버전을 배포 하는 방법을 보여 주고 Azure App Service Web Apps에 배포 하는 방법을 보여 줍니다. [Visual Studio를 사용 하 여 ASP.NET 웹 배포](../../deployment/visual-studio-web-deployment/introduction.md)를 참조 하세요.
> 
> 이러한 자습서는 테스트를 위해 로컬 개발 컴퓨터의 IIS에 먼저 배포 하 고 나 서 타사 호스팅 공급자에 게 배포 하는 과정을 안내 합니다. 배포할 응용 프로그램은 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. SQL Server Compact를 사용 하 여 시작 하 고 SQL Server Compact에 배포 하는 경우 이후 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법과 SQL Server로 마이그레이션하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 Visual Studio에서 ASP.NET로 작업 하는 방법을 알고 있다고 가정 합니다. 그렇지 않은 경우 [기본 ASP.NET Web Forms 자습서](../tailspin-spyworks/tailspin-spyworks-part-1.md) 또는 [기본 ASP.NET MVC 자습서](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)를 시작 하는 것이 좋습니다.
> 
> 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)에 게시할 수 있습니다.

## <a name="overview"></a>개요

이러한 자습서는 테스트를 위해 로컬 개발 컴퓨터의 IIS에 먼저 배포 하 고 나 서 타사 호스팅 공급자에 게 배포 하는 과정을 안내 합니다. 배포할 응용 프로그램은 응용 프로그램 데이터베이스 및 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. SQL Server Compact를 사용 하 여 시작 하 고 SQL Server Compact에 배포 하는 경우 이후 자습서에서는 데이터베이스 변경 내용을 배포 하는 방법과 SQL Server로 마이그레이션하는 방법을 보여 줍니다.

모든 및 문제 해결 페이지의 자습서 수 – 11은 배포 프로세스를 어렵게 만들 수 있습니다. 실제로 사이트를 배포 하기 위한 기본 절차는 자습서 집합의 상대적으로 작은 부분을 구성 하는 것입니다. 그러나 실제 상황에서는 일반적으로 대상 서버에서 폴더 사용 권한을 설정 하는 것과 같이 몇 가지 작고 중요 한 추가 기능에 대 한 정보가 필요 합니다. 이 자습서에는 이러한 추가 기술이 포함 되어 있으며,이 자습서에서는 실제 응용 프로그램을 성공적으로 배포 하지 못하게 하는 정보를 남기지 않습니다.

자습서는 순서 대로 실행 되도록 설계 되었으며 각 부품은 이전 파트를 기반으로 합니다. 그러나 상황과 관련이 없는 부분은 건너뛸 수 있습니다. 파트를 건너뛰려면 이후 자습서의 절차를 조정 해야 할 수 있습니다.

## <a name="intended-audience"></a>적용 대상

이 자습서는 소규모 조직이 나 다른 환경에서 작업 하는 ASP.NET 개발자를 대상으로 합니다.

- 연속 통합 프로세스 (자동화 된 빌드 및 배포)는 사용 되지 않습니다.
- 프로덕션 환경은 타사 호스팅 공급자입니다.
- 한 사람은 일반적으로 여러 역할 (동일한 사용자가 개발, 테스트 및 배포)을 채웁니다.

엔터프라이즈 환경에서는 일반적으로 연속 통합 프로세스를 구현 하는 것이 더 일반적 이며, 프로덕션 환경은 일반적으로 회사 소유의 서버에서 호스팅됩니다. 다른 사용자도 일반적으로 다른 역할을 수행 합니다. 엔터프라이즈 배포에 대 한 자세한 내용은 [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)를 참조 하세요.

모든 규모의 조직은 Azure에 웹 응용 프로그램을 배포할 수 있으며, 이러한 자습서에 표시 된 대부분의 절차는 Azure 앱 Services Web Apps에도 적용 됩니다. Azure에 대 한 소개는 [https://azure.microsoft.com](https://azure.microsoft.com)를 참조 하세요.

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>자습서에 표시 된 호스팅 공급자

이 자습서에서는 호스팅 회사 계정을 설정 하 고 해당 호스팅 공급자에 응용 프로그램을 배포 하는 과정을 안내 합니다. 특정 호스팅 회사를 선택 하 여 자습서에서 라이브 웹 사이트에 배포 하는 전체 환경을 보여 줄 수 있습니다. 각 호스팅 회사는 다양 한 기능을 제공 하 고 해당 서버에 배포 하는 환경은 약간 다릅니다. 그러나이 자습서에서 설명 하는 프로세스는 전반적인 프로세스에 일반적입니다.

이 자습서에 사용 되는 호스팅 공급자 (Cytanium.com)는 사용할 수 있는 여러 항목 중 하나 이며이 자습서에서 사용 하는 공급자는 인증 또는 권장 사항을 구성 하지 않습니다.

## <a name="deploying-web-site-projects"></a>웹 사이트 프로젝트 배포

Contoso 대학은 Visual Studio 웹 응용 프로그램 프로젝트입니다. 이 자습서에서 설명 하는 대부분의 배포 방법 및 도구는 [웹 사이트 프로젝트](https://msdn.microsoft.com/library/dd547590.aspx)에 적용 되지 않습니다. 웹 사이트 프로젝트를 배포 하는 방법에 대 한 자세한 내용은 [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects)을 참조 하십시오.

## <a name="deploying-aspnet-mvc-projects"></a>ASP.NET MVC 프로젝트 배포

이 자습서에서는 ASP.NET Web Forms 프로젝트를 배포 하지만,이 작업을 수행 하는 방법에 대 한 자세한 내용은 ASP.NET MVC에도 적용 됩니다. Visual Studio MVC 프로젝트는 또 다른 형태의 웹 응용 프로그램 프로젝트입니다. 유일한 차이점은 ASP.NET MVC 또는 대상 버전을 지원 하지 않는 호스팅 공급자에 배포 하는 경우 프로젝트에 적절 한 ([mvc 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) 또는 [mvc 4](http://nuget.org/packages/aspnetmvc)) NuGet 패키지를 설치 했는지 확인 해야 한다는 것입니다.

## <a name="programming-language"></a>프로그래밍 언어

샘플 응용 프로그램에서는 C# 를 사용 하지만 자습서에는에 대 C#한 지식이 필요 하지 않으며 자습서에서 설명 하는 배포 기술은 언어별로 특정 하지 않습니다.

## <a name="troubleshooting-during-this-tutorial"></a>이 자습서에서 문제 해결

배포 하는 동안 오류가 발생 하거나 배포 된 사이트가 제대로 실행 되지 않으면 오류 메시지에서 항상 솔루션을 제공 하지 않습니다. 몇 가지 일반적인 문제 시나리오를 돕기 위해 [문제 해결 참조 페이지](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) 를 사용할 수 있습니다. 자습서를 진행할 때 오류 메시지가 표시 되거나 문제가 해결 되지 않으면 문제 해결 페이지를 확인 해야 합니다.

## <a name="comments-welcome"></a>의견 시작

자습서에 대 한 설명은 환영 하며 자습서를 업데이트할 때 자습서 설명에서 제공 되는 향상 된 기능에 대 한 제안 또는 제안 사항을 고려 하기 위해 모든 작업이 수행 됩니다.

## <a name="prerequisites"></a>Prerequisites

시작 하기 전에 컴퓨터에 Windows 7 이상 및 다음 제품 중 하나가 설치 되어 있는지 확인 합니다.

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [웹 용 Visual Studio 2012 RC 또는 Visual Studio Express 2012 RC](https://go.microsoft.com/fwlink/?LinkId=240162)

Visual Studio 2010 SP1 또는 Visual Web Developer Express 2010 s p 1이 설치 되어 있는 경우 다음 제품도 설치 합니다.

- [.Net 용 AZURE SDK (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (웹 게시 업데이트 포함)
- [SQL Server Compact 4.0 용 Microsoft Visual Studio 2010 SP1 도구](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

자습서를 완료 하기 위해 다른 소프트웨어가 필요 하지만 아직 로드 하지 않아도 됩니다. 이 자습서에서는 필요할 때 설치 하는 단계를 안내 합니다.

## <a name="downloading-the-sample-application"></a>예제 응용 프로그램 다운로드

배포할 응용 프로그램은 Contoso 대학 이라고 하며 이미 생성 되었습니다. [ASP.NET 사이트의 Entity Framework 자습서](https://asp.net/entity-framework/tutorials)에 설명 된 Contoso 대학 응용 프로그램을 느슨하게 기반으로 하는 대학 웹 사이트의 단순화 된 버전입니다.

필수 구성 요소가 설치 되어 있는 경우 [Contoso 대학 웹 응용 프로그램](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)을 다운로드 합니다. *.Zip* 파일에는 여러 버전의 프로젝트와 12 개의 자습서를 모두 포함 하는 PDF 파일이 포함 되어 있습니다. 자습서의 단계를 진행 하려면 ContosoUniversity-Begin으로 시작 합니다. 자습서의 끝에서 프로젝트가 표시 되는 모양을 확인 하려면 ContosoUniversity를 엽니다. 자습서 10에서 전체 SQL Server 마이그레이션하기 전에 프로젝트의 모양을 확인 하려면 ContosoUniversity-AfterTutorial09를 엽니다.

자습서 단계를 진행 하기 위해 준비 하려면 Visual Studio 프로젝트 작업에 사용할 모든 폴더에 ContosoUniversity를 저장 합니다. 기본적으로이 폴더는 다음과 같습니다.

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(이 자습서의 스크린 샷에서 프로젝트 폴더는 `C`: 드라이브의 루트 디렉터리에 있습니다.)

Visual Studio를 시작 하 고 프로젝트를 연 다음 CTRL + f 5를 눌러 실행 합니다.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

웹 사이트 페이지는 메뉴 모음에서 액세스할 수 있으며 다음과 같은 기능을 수행할 수 있습니다.

- 학생 통계 (정보 페이지)를 표시 합니다.
- 학생을 표시 하 고, 편집 하 고, 삭제 하 고, 추가 합니다.
- 코스를 표시 하 고 편집 합니다.
- 강사를 표시 하 고 편집 합니다.
- 부서를 표시 하 고 편집 합니다.

몇 가지 대표적인 페이지의 스크린샷은 다음과 같습니다.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>배포에 영향을 주는 응용 프로그램 기능 검토

응용 프로그램의 다음 기능은 응용 프로그램을 배포 하는 방법 또는 배포를 위해 수행 해야 하는 작업에 영향을 줍니다. 이러한 각 항목은 시리즈의 다음 자습서에 자세히 설명 되어 있습니다.

- Contoso 대학은 SQL Server Compact 데이터베이스를 사용 하 여 학생 및 강사 이름과 같은 응용 프로그램 데이터를 저장 합니다. 데이터베이스에는 테스트 데이터와 프로덕션 데이터가 혼합 되어 있으며 프로덕션 환경에 배포 하는 경우 테스트 데이터를 제외 해야 합니다. 자습서 시리즈의 뒷부분에서 SQL Server Compact에서 SQL Server로 마이그레이션합니다.
- 응용 프로그램은 SQL Server Compact 데이터베이스에 사용자 계정 정보를 저장 하는 ASP.NET 멤버 자격 시스템을 사용 합니다. 응용 프로그램은 일부 제한 된 정보에 대 한 액세스 권한이 있는 관리자 사용자를 정의 합니다. 테스트 계정을 사용 하지 않고 하나의 관리자 계정을 사용 하 여 멤버 자격 데이터베이스를 배포 해야 합니다.
- 응용 프로그램 데이터베이스 및 멤버 자격 데이터베이스에서 SQL Server Compact를 데이터베이스 엔진으로 사용 하기 때문에 데이터베이스 엔진은 물론 데이터베이스 자체 뿐만 아니라 호스팅 공급자에도 데이터베이스 엔진을 배포 해야 합니다.
- 응용 프로그램은 ASP.NET 유니버설 멤버 자격 공급자를 사용 하 여 멤버 자격 시스템이 SQL Server Compact 데이터베이스에 데이터를 저장할 수 있도록 합니다. 유니버설 멤버 자격 공급자가 포함 된 어셈블리는 응용 프로그램과 함께 배포 해야 합니다.
- 응용 프로그램은 Entity Framework 5.0를 사용 하 여 응용 프로그램 데이터베이스의 데이터에 액세스 합니다. Entity Framework 5.0를 포함 하는 어셈블리는 응용 프로그램과 함께 배포 해야 합니다.
- 응용 프로그램은 타사 오류 로깅 및 보고 유틸리티를 사용 합니다. 이 유틸리티는 응용 프로그램과 함께 배포 해야 하는 어셈블리에 제공 됩니다.
- 오류 로깅 유틸리티는 XML 파일의 오류 정보를 파일 폴더에 기록 합니다. 배포 된 사이트에서 ASP.NET가 실행 되는 계정에이 폴더에 대 한 쓰기 권한이 있는지 확인 하 고 배포에서이 폴더를 제외 해야 합니다. 그렇지 않으면 테스트 환경의 오류 로그 데이터가 프로덕션에 배포 될 수 있으며 프로덕션 오류 로그 파일이 삭제 될 수 있습니다.
- 응용 프로그램에는 대상 환경 (테스트 또는 프로덕션)에 따라 배포 된 *web.config* 파일에서 변경 해야 하는 일부 설정과 빌드 구성 (디버그 또는 릴리스)에 따라 변경 되어야 하는 기타 설정이 포함 되어 있습니다.
- Visual Studio 솔루션에는 클래스 라이브러리 프로젝트가 포함 되어 있습니다. 이 프로젝트가 생성 하는 어셈블리만 프로젝트 자체가 아닌 배포 해야 합니다.

시리즈의이 첫 번째 자습서에서는 샘플 Visual Studio 프로젝트를 다운로드 하 고 응용 프로그램을 배포 하는 방법에 영향을 주는 사이트 기능을 검토 했습니다. 다음 자습서에서는 이러한 항목 중 일부를 자동으로 처리 하도록 설정 하 여 배포를 준비 합니다. 다른 사용자는 수동으로 처리 합니다.

> [!div class="step-by-step"]
> [다음](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
