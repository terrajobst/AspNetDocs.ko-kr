---
uid: whitepapers/aspnet-web-deployment-content-map
title: ASP.NET 웹 배포-권장 리소스 | Microsoft Docs
author: rick-anderson
description: 이 항목에서는 Visual Studio 2010, Visual Web De ...를 사용 하 여 ASP.NET 웹 응용 프로그램을 IIS에 배포 (게시) 하는 방법에 대 한 설명서 리소스 링크를 제공 합니다.
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517277"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>ASP.NET 웹 배포 - 권장 리소스

> 이 항목에서는 Visual Studio 2010, Visual Web Developer 2010 이상 버전을 사용 하 여 ASP.NET 웹 응용 프로그램을 IIS에 배포 (게시) 하는 방법에 대 한 설명서 리소스 링크를 제공 합니다.
> 
> 유용한 블로그 게시물, [stackoverflow](http://stackoverflow.com) 스레드 또는 유용한 다른 링크를 알고 있는 경우 링크가 포함 된 [전자 메일을 보내 주세요](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map) .
> 
> > [!NOTE] 
> > 
> > 이러한 리소스 중 상당수는 최신 버전의 [Visual Studio 웹 게시 업데이트](https://go.microsoft.com/fwlink/?LinkID=208120)를 설치 하는 경우에만 사용할 수 있는 배포 기능을 설명 합니다. 일부 기능은 Visual Studio 2012 또는 Visual Studio 2013 에서만 사용할 수 있습니다.

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [웹 프로젝트에 대 한 배포 옵션 이해](#understanding)
- [ASP.NET 응용 프로그램의 호스팅 공급자 찾기](#findinghosting)
- [Visual Studio에서 웹 응용 프로그램 배포](#fromvs)
- [웹 배포 패키지를 만들고 설치 하 여 웹 응용 프로그램 배포](#package)
- [CI (연속 통합) 프로세스를 사용 하 여 웹 응용 프로그램 배포](#ci)
- [Web.config 변환을 사용 하 여 배포 중에 대상 Web.config 파일 또는 app.config 파일의 설정 변경](#transforms)
- [웹 배포 매개 변수를 사용 하 여 배포 중에 대상 웹 응용 프로그램에서 설정 변경](#webdeployparms)
- [배포 하는 동안 응용 프로그램이 오프 라인 상태 인지 확인](#appoffline)
- [웹 응용 프로그램 배포의 일부로 데이터베이스 또는 데이터베이스에 대 한 변경 내용 배포](#databasewithweb)
- [웹 응용 프로그램 배포와 별도로 데이터베이스 배포](#databaseseparate)
- [멤버 자격 및 프로 파일링과 같은 ASP.NET 응용 프로그램 서비스를 사용 하는 웹 응용 프로그램 배포](#aspnetmembership)
- [배포용으로 미리 컴파일](#precompiling)
- [인트라넷 웹 응용 프로그램 배포](#intranet)
- [자동으로 기본 배포 되지 않는 일반적인 배포 작업 자동화](#automating)
- [개발자가 웹 배포를 사용 하 여 웹 응용 프로그램을 배포할 수 있도록 웹 서버 구성](#configuringservers)
- [호스팅 공급자에 대 한 서버 구성](#hostingprovider)
- [배포 문제 해결](#troubleshooting)
- [특정 배포 질문에 대 한 도움말 보기](#gettinghelp)
- [추가 리소스](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>웹 프로젝트에 대 한 배포 옵션 이해

- [Visual Studio 및 ASP.NET 용 웹 배포 개요](https://msdn.microsoft.com/library/dd394698.aspx) (MSDN)
- [Microsoft Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy) Visual Studio를 사용 하는 것 뿐만 아니라 [지속적인](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 업데이트 ( [소스 제어](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)에서 자동화)를 비롯 하 여 Windows Azure 웹 사이트에 웹 프로젝트를 배포 하기 위한 리소스의 옵션 및 링크에 대해 설명 합니다.
- [Visual Studio 2012 웹 게시 개선 사항](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md) (Scott Hanselman의 비디오).
- [VS 2010의 웹 배포에 대 한 개요 게시물](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html) (인 vishal Joshi의 블로그) 이전 블로그 게시물 이지만 연결 된 Visual Studio 2010 리소스 중 일부는 Visual Studio 2012에도 관련 된 정보를 포함 하 고 있습니다.

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>ASP.NET 응용 프로그램의 호스팅 공급자 찾기

- [ASP.NET 호스팅](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>Visual Studio에서 웹 응용 프로그램 배포

- [Microsoft Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy) Microsoft Azure 웹 사이트에 웹 프로젝트를 배포 하기 위한 옵션을 설명 하 고 리소스에 대 한 링크를 제공 합니다. Visual Studio에서 배포 하는 방법에 대 한 섹션이 포함 되어 있습니다.
- [Visual Studio를 사용한 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)(영문). 12 부 자습서 시리즈는 SQL Server 데이터베이스를 사용 하 여 웹 응용 프로그램을 배포 하는 방법을 보여 줍니다. 데이터베이스 배포의 경우 dbDacFx 공급자와 Entity Framework Code First 마이그레이션를 모두 사용 합니다. 또한 [web.config 파일 변환](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)에 대 한 정보, [개별 파일 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles), [명령줄 배포](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)및 [Pubxml 파일을 편집 하 여 Visual Studio 웹 게시 파이프라인을 사용자 지정 하는 방법을](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md)제공 합니다. Web Forms, MVC 및 Web API를 비롯 한 모든 ASP.NET 웹 프로젝트에 적용 됩니다.
- [방법: visual studio에서 한 번 클릭으로 게시를 사용 하 여 웹 프로젝트 배포](https://msdn.microsoft.com/library/dd465337.aspx) (Visual Studio 웹 게시 마법사에 대 한 참조 정보)
- [Visual Studio를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다. 이는이 섹션의 맨 위에 나열 된 **Visual Studio를 사용 하는 ASP.NET 웹 배포** 의 이전 버전입니다. SQL Server Compact 데이터베이스를 배포 하는 방법 및 SQL Server Compact에서 SQL Server의 전체 버전으로 마이그레이션하는 방법에 대 한 자세한 내용은 주로 유용 합니다.
- [저장소 테이블, 큐 및 blob을 사용 하는 .Net 다중 계층 응용 프로그램](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure 사이트) 5 부 자습서 시리즈는 MVC 프로젝트를 만들어 Windows Azure 클라우드 서비스에 배포 하는 방법을 보여 줍니다.

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>웹 배포 패키지를 만들고 설치 하 여 웹 응용 프로그램 배포

- [방법: Visual Studio에서 웹 배포 패키지 만들기](https://msdn.microsoft.com/library/dd465323.aspx) (MSDN)
- [방법: Visual Studio에서 만든 배포 .Cmd 파일을 사용 하 여 배포 패키지 설치](https://msdn.microsoft.com/library/ff356104.aspx) (MSDN)
- [웹 배포 패키지를 사용 하 여 개발자 상자와 타사 호스트](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx) (Sayed Hashimi의 블로그)에서 IIS에 배포 합니다. Iis 관리자를 사용 하 여 iis에서 원격 관리용 IIS 관리자를 지 원하는 호스팅 회사에 배포 패키지를 설치 하는 방법입니다.
- Visual Studio 2010 (IIS.NET 웹 사이트) [에서 웹 배포 패키지를 빌드합니다](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) . 명령줄 패키지 만들기 및 설치에 대 한 지침이 포함 되어 있습니다.
- [언제 어디서 나 게시](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx) (Sayed Hashimi의 블로그) 여러 대상 환경에 대 한 web.config 파일을 변환 하는 프로세스를 자동화 하는 NuGet 패키지를 도입 하 여 패키지 하나를 여러 서버에 배포할 수 있습니다. Sayed Hashimi의 [Packageweb 비디오](https://www.youtube.com/watch?v=-LvUJFI8CzM) 도 참조 하세요.

다음 섹션도 참조 하세요.

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>CI (연속 통합) 프로세스를 사용 하 여 웹 응용 프로그램 배포

- [지속적인 통합 및 지속적인 업데이트 (Microsoft Azure를 사용 하 여 실제 클라우드 앱 빌드)](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) 연속 통합 및 지속적인 업데이트를 소개 하는 전자 서적 장.
- [Microsoft Azure 웹 사이트를 배포 하는 방법](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy) Microsoft Azure 웹 사이트에 웹 프로젝트를 배포 하기 위한 리소스의 옵션 및 링크를 설명 합니다. 원본 제어에서 배포 자동화에 대 한 섹션을 포함 합니다.
- [엔터프라이즈 시나리오에서 웹 응용 프로그램 배포](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). 40-자습서 시리즈에서는 Visual Studio 2010 및 Team Foundation Server 2010를 사용 하 여 CI 프로세스에서 배포를 자동화 하는 방법을 보여 줍니다.
- [Microsoft Build Engine 내에서: MSBuild 및 Team Foundation build를 사용 하 여 Sayed Hashimi 및 William](http://msbuildbook.com) 이는 웹 리소스가 아니라 책 이지만 연속 통합 시나리오에 대해 MSBuild를 구성 하는 방법을 배우는 데 필수적인 가이드입니다.
- [MSBuild 확장 팩](https://github.com/mikefourie/MSBuildExtensionPack). 배포 작업을 포함 합니다.
- [Team Foundation Build 사용자 지정 가이드](https://aka.ms/vsarsolutions). ALM Rangers의 설명서는 웹 배포에 대 한 Team Foundation Server 포함 하며 자습서 및 비디오를 포함 합니다.
- CI 서버 (Sayed Hashimi의 블로그) [에서 XML 변환을 SlowCheetah](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx) 합니다. App.config 및 기타 XML 파일을 변환 하기 위한 Visual Studio 추가 SlowCheetah를 사용 하는 방법을 설명 합니다.

또한이 페이지의 뒷부분에서 [응용 프로그램이 배포 중 오프 라인 상태 인지](aspnet-web-deployment-content-map.md#appoffline) 확인 합니다.

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>Web.config 변환을 사용 하 여 배포 중에 대상 Web.config 파일 또는 app.config 파일의 설정 변경

- [Web.config 파일 변환](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md).
- [Visual Studio (MSDN)를 사용 하는 웹 프로젝트 배포를 위한 Web.config 변환 구문](https://msdn.microsoft.com/library/dd465326.aspx) 입니다.
- [웹 도구 2012.2-web.config 변환](https://www.youtube.com/watch?v=HdPK8mxpKEI) (YouTube Video By Sayed Hashimi). Web.config 변환을 설정 하 고 미리 보는 방법을 보여 줍니다.
- [Web.config 변환을 사용 하지 않도록 설정 어떻게 할까요??](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN).
- [Web.config 변환 대신 웹 배포 매개 변수를 사용 해야 하는 경우는 언제 인가요?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN).
- [XDT (XML 문서 변환)는 codeplex.com](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (.Net 웹 개발 및 도구 블로그)에 릴리스됩니다. Web.config 파일 변환 엔진에 대 한 소스 코드의 가용성을 발표 하 고이를 사용 하는 일부 도구를 나열 합니다.
- [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure 블로그). 대상 환경이 Windows Azure 웹 사이트인 경우 Web.config를 대신 `appSettings` 또는 `connectionStrings`변환 합니다.

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>웹 배포 매개 변수를 사용 하 여 배포 중에 대상 웹 응용 프로그램에서 설정 변경

- [방법: 웹 배포 패키지에서 웹 배포 매개 변수 사용](https://msdn.microsoft.com/library/ff398068.aspx) (MSDN)
- Msdeploy.exe: 게시 프로필 (Sayed Hashimi의 블로그) [에 따라 게시에서 앱 설정을 업데이트 하는 방법](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx) 입니다. 웹 배포 매개 변수를 Visual Studio 게시 프로필에 통합 하는 방법을 보여 줍니다.
- [매개 변수화 웹 배포](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization) (IIS.NET 웹 사이트).
- [작업에서 매개 변수화 웹 배포](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html) (인 vishal Joshi의 블로그)
- [매개 변수화 및 Web.config 변환](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html) (인 vishal Joshi의 블로그)을 웹 배포 합니다.
- [Windows Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure 블로그). 대상 환경이 Windows Azure 웹 사이트인 경우 웹 배포 매개 변수 대신 `appSettings` 또는 `connectionStrings`를 매개 변수화 하려는 경우.

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>배포 하는 동안 응용 프로그램이 오프 라인 상태 인지 확인

- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 코드 업데이트 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). **배포 하는 동안 응용 프로그램을 오프 라인 상태로 만들기** 섹션을 참조 하세요.
- [게시 하기 전에 응용 프로그램을 오프 라인 상태로 만들기](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing) (IIS.net site) 오프 라인 .htm 파일\_앱의 처리를 자동화 하는 웹 배포 3.0에 기본 제공 되는 기능에 대해 설명 합니다. 이 기능은 오프 라인 .htm 파일\_사용자 지정 앱에서 작동 하지 않습니다.
- [게시 하는 동안 웹 앱을 오프 라인으로 전환 하는 방법](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx) (Sayed Hashimi 블로그). 사용자 지정 앱을 사용 하는 프로세스를 자동화 하는 방법\_오프 라인 .htm 파일.
- [앱 오프 라인 및 Usechecksum 웹 게시 업데이트](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) (Microsoft 웹 개발 블로그). 앱\_오프 라인 .htm 파일 사용을 자동화 하는 또 다른 옵션입니다.
- [웹 배포 3.5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (IIS.net site). 사용자 지정 앱에 대 한 웹 배포 3.5의 새로운 기능은 오프 라인 .htm 파일\_.

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>웹 응용 프로그램 배포의 일부로 데이터베이스 또는 데이터베이스에 대 한 변경 내용 배포

- [Visual Studio (MSDN)에서 데이터베이스 배포를 구성](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) 합니다. 웹 프로젝트를 사용 하 여 데이터베이스를 배포 하기 위한 옵션의 개요입니다.
- [Visual Studio를 사용한 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)(영문). 12 부 자습서 시리즈 dbDacFx 공급자 및 Entity Framework Code First 마이그레이션를 사용 하 여 데이터베이스 배포를 표시 합니다.
- [방법: Visual Studio에서 한 번 클릭으로 게시 (MSDN)를 사용 하 여 웹 프로젝트 배포](https://msdn.microsoft.com/library/dd465337.aspx)
- [멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 5 앱을 Windows Azure 웹 사이트에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 단일 SQL Server 데이터베이스를 사용 하 여 멤버 자격 및 응용 프로그램 데이터를 모두 사용 하는 응용 프로그램을 빌드하고 배포 하는 긴 자습서입니다.
- [Visual Studio를 사용 하 여 SQL Server Compact를 사용 하 여 ASP.NET 웹 응용 프로그램을 배포](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)합니다. 12 부 자습서 시리즈는 SQL Server Compact 데이터베이스를 배포 하는 방법 및 SQL Server Compact에서 SQL Server의 전체 버전으로 마이그레이션하는 방법을 보여 줍니다.

또한이 페이지의 앞부분에 나오는 CI (지속적인 통합) 프로세스를 사용 하 여 웹 배포 패키지를 만들고 설치 하 고 웹 응용 프로그램을 배포 하 여 웹 응용 프로그램 배포를 참조 하세요.

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>웹 응용 프로그램 배포와 별도로 데이터베이스 배포

- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN)을 (를) 합니다.
- [SQL Server 데이터베이스 프로젝트에 데이터 포함](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx) (SQL Server Data Tools 팀 블로그) 데이터베이스를 배포할 때 스키마와 데이터를 모두 배포 하는 방법
- [Windows Azure에 데이터베이스를 배포 하는 방법](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) (Microsoft Azure 사이트)
- [Windows Azure SQL Database로 데이터베이스 마이그레이션 (이전의 SQL Azure)](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) (MSDN)
- SSDT (SQL Server Data Tools 팀 블로그) [를 사용 하 여 SQL Azure로 데이터베이스 마이그레이션](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx)
- [Windows Azure로 데이터 중심 응용 프로그램 마이그레이션](https://msdn.microsoft.com/library/jj156154.aspx) (MSDN)
- [SQL Server 데이터베이스를 Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN)로 마이그레이션합니다.

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>멤버 자격 및 프로 파일링과 같은 ASP.NET 응용 프로그램 서비스를 사용 하는 웹 응용 프로그램 배포

- [멤버 자격, OAuth 및 SQL Database가 포함 된 보안 ASP.NET MVC 5 앱을 Windows Azure 웹 사이트에 배포](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)합니다. 단일 SQL Server 데이터베이스를 사용 하 여 멤버 자격 및 응용 프로그램 데이터를 모두 사용 하는 응용 프로그램을 빌드하고 배포 하는 긴 자습서입니다.
- [ASP.NET Identity](https://asp.net/identity/). ASP.NET Identity에 대 한 리소스입니다.
- [Visual Studio를 사용한 ASP.NET 웹 배포](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)(영문). 12 부 자습서 시리즈에서는 ASP.NET 멤버 자격 데이터베이스를 배포 하는 방법을 보여 줍니다.
- [애플리케이션 서비스를 사용 하는 웹 사이트 구성](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md) 웹 사이트 프로젝트의 경우 웹 응용 프로그램 프로젝트와도 관련이 있습니다.
- [프로덕션 웹 사이트의 사용자 및 역할](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md) 웹 사이트 프로젝트의 경우 웹 응용 프로그램 프로젝트와도 관련이 있습니다.

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>배포용으로 미리 컴파일

- [ASP.NET 웹 응용 프로그램 프로젝트 미리 컴파일 개요](https://msdn.microsoft.com/library/aa983464.aspx) (MSDN).
- [웹 패키지 및 게시 탭, 프로젝트 속성](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN)
- [고급 미리 컴파일 설정 대화 상자](https://msdn.microsoft.com/library/hh475319.aspx) (MSDN).

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>인트라넷 웹 응용 프로그램 배포

- [Visual Studio 2013에서 ASP.NET와 함께 온-프레미스 조직 인증 옵션 (ADFS)을 사용](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) 합니다 (블로그 by Vittorio Bertocci).
- [ASP.NET MVC (MSDN)를 사용 하 여 인트라넷 사이트를 만드는 방법](https://msdn.microsoft.com/library/gg703322(VS.98).aspx) 이전 연습 쓰여진 for Visual Studio 2010에는 Visual Studio 2013에서 도입 된 인트라넷 프로젝트 템플릿의 주요 변경 내용이 반영 되지 않습니다.

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>자동으로 기본 배포 되지 않는 일반적인 배포 작업 자동화

- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 추가 파일 배포](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md).
- [웹 게시에 대 한 폴더 사용 권한 설정](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) (Sayed Hashimi 블로그).
- [웹 프로젝트 패키지에 대 한 레지스트리 설정을 포함 하도록 대상 파일을 확장 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx) (웹 개발 도구 블로그)
- [XML (web.config) 변환 확장](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx) (Sayed Hashimi 블로그). 사용자 지정 XDT 변환을 만드는 방법을 보여 줍니다.
- [Msdeploy.exe (웹 배포 도구) 사용자 지정 공급자는 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (Sayed Hashimi의 블로그)을 사용 합니다. 웹 배포 사용자 지정 공급자를 만드는 방법을 보여 줍니다.
- [COM 구성 요소를 패키지 및 배포 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx) (웹 개발 도구 블로그).
- [.Net 어셈블리를 패키지 하는 방법](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx) (웹 개발 도구 블로그). GAC에 어셈블리를 배포 하는 방법
- [모든 항목 스크립팅-IIS, 웹 배포 및 기타 사물 (Tugberk Ugurlu의 블로그)을 사용 하 여 웹 서버에 대 한 Windows AZURE VM을 초기화](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) 합니다.

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>개발자가 웹 배포를 사용 하 여 웹 응용 프로그램을 배포할 수 있도록 웹 서버 구성

- 관리자 및 비관리자 배포 (IIS.net 사이트) [를 위한 웹 배포 설치 및 구성](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>호스팅 공급자에 대 한 서버 구성

- [Microsoft ASP.NET 4 호스팅 배포 가이드](https://go.microsoft.com/fwlink/?LinkId=191365) (Microsoft 다운로드 센터).
- [프로필 XML 파일](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file) (IIS.net 사이트)을 생성 합니다.

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>배포 문제 해결

- [Visual Studio에서 Microsoft Azure 웹 사이트 문제 해결](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) (Microsoft Azure 사이트)
- [Visual Studio를 사용 하 여 ASP.NET 웹 배포: 문제 해결](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md).
- [웹 배포와 관련 된 일반적인 문제 해결](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy)
- [웹 배포 오류 코드](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes) (IIS.net site).
- [Visual Studio 및 ASP.NET에 대 한 웹 배포 FAQ](https://msdn.microsoft.com/library/ee942158.aspx) (MSDN)
- [IIS와 ASP.NET 개발 서버의 핵심 차이점](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)
- [개발과 프로덕션 간의 일반적인 구성 차이점](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md)
- [보통 신뢰 수준에서 ASP.NET 응용 프로그램을 호스팅합니다](http://www.4guysfromrolla.com/articles/100307-1.aspx) (Rolla 사이트의 경우 4 개).

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>특정 배포 질문에 대 한 도움말 보기

- [ASP.NET 구성 및 배포 포럼](https://forums.asp.net/26.aspx/1?Configuration and Deployment).
- [StackOverflow.com](http://www.StackOverflow.com)(영문)

<a id="additional"></a>

## <a name="additional-resources"></a>추가 리소스

이 섹션에서는 Visual Studio 및 IIS 배포 도구를 사용 하는 방법에 대해 자세히 알아보는 데 유용한 추가 리소스에 대 한 링크를 제공 합니다.

다음 블로그는 Visual Studio 웹 배포에 대 한 정보를 포함 하는 경우가 많습니다.

- [Microsoft 블로그의 웹 개발 도구](https://blogs.msdn.com/b/webdevtools/).
- [Sayed Hashimi의 블로그](http://www.sedodream.com/)입니다.

다음 리소스는 Visual Studio에서 웹 응용 프로그램 프로젝트 배포 작업을 수행 하는 데 사용 하는 IIS 프레임 워크인 웹 배포에 대 한 설명서를 제공 합니다. IIS.net 웹 사이트의 [웹 배포 도구 포럼](https://go.microsoft.com/fwlink/?LinkId=149411) 에서 웹 배포에 대해 질문할 수 있습니다.

- [웹 배포 소개](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy).
- [웹 배포 설치 및 구성](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy)
- [웹 배포 설정을 자동화 하기 위한 PowerShell 스크립트](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup)입니다.
- [웹 배포 도구](https://go.microsoft.com/fwlink/?LinkId=151481)(영문). TechNet 사이트의 웹 배포 설명서에 대 한 최상위 수준 표 노드 유용한 참조 정보를 포함 하지만 대부분의 TechNet 페이지는 수년간 업데이트 되지 않았습니다.
- [Microsoft 웹 배포 네임 스페이스](https://go.microsoft.com/fwlink/?LinkId=148630). API 설명서는 버전 1.0 이후로 업데이트 되지 않았습니다.
- [Microsoft 웹 배포 팀 블로그](https://blogs.iis.net/msdeploy/default.aspx).
- [IIS.net 웹 사이트의 게시 탭](https://www.iis.net/learn/publish)
