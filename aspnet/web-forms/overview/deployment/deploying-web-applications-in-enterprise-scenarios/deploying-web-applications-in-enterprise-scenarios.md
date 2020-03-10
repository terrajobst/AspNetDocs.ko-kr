---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: Visual Studio 2010을 사용 하 여 엔터프라이즈 시나리오에서 웹 응용 프로그램 배포 | Microsoft Docs
author: jrjlee
description: 이 자습서 집합은 다양 한 엔터프라이즈 시나리오에서 웹 응용 프로그램을 배포 하는 데 사용할 수 있는 도구 및 기술에 대해 설명 합니다. 모범 사례를 수행 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463433"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>Visual Studio 2010을 사용하여 엔터프라이즈 시나리오에서 웹 애플리케이션 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 자습서 집합은 다양 한 엔터프라이즈 시나리오에서 웹 응용 프로그램을 배포 하는 데 사용할 수 있는 도구 및 기술에 대해 설명 합니다. Visual Studio 2010, Microsoft Build Engine (MSBuild), 인터넷 정보 서비스 (IIS) 7.5, IIS 웹 배포 도구 (웹 배포), WFF (웹 팜 프레임 워크) 및 nuget.exe와 같은 유틸리티를 사용 하는 방법에 대 한 유용한 사용 방법을 설명 합니다. 배포 프로세스를 간소화 하 고 관리 합니다. 여기에는 다음을 수행 하는 데 도움이 되는 개념적 개요 및 작업 지향적인 지침이 포함 되어 있습니다.
> 
> - 엔터프라이즈 규모 웹 응용 프로그램에 대 한 배포 요구 사항을 검토 하 고 설정 합니다.
> - 웹 배포를 지원 하도록 테스트, 스테이징 및 프로덕션 웹 서버 환경을 구성 합니다.
> - 자동화 된 웹 배포를 지원 하도록 TFS (Team Foundation Server) CI (지속적인 통합) 프로세스를 구성 합니다.
> - 다양 한 요구 사항과 제한을 사용 하 여 다양 한 서버 환경에 엔터프라이즈급 웹 응용 프로그램을 배포 합니다.
> - 다른 서버 환경에서 실행 중인 웹 응용 프로그램에 대 한 변경 내용을 배포 합니다.
> 
> > [!NOTE]
> > 이러한 자습서에서는 TFS를 CI 서버로 사용 하는 방법을 설명 하지만 모든 CI 서버에 대 한 지침을 쉽게 적용할 수 있습니다. 자습서를 이해 하 고 활용할 수 있도록 TFS에 대 한 자세한 지식이 필요 하지 않습니다.
> 
> 
> 이러한 자습서의 이탈리아어 번역은 [http://www.lucamorelli.it](http://www.lucamorelli.it)를 참조 하세요.

## <a name="about-the-authors"></a>저자 정보

Jason Lee는 Microsoft 제품 및 기술, 특히 SharePoint와 ASP.NET를 사용 하 여 몇 년 동안 작업 한 [콘텐츠 마스터가](http://www.contentmaster.com/) 있는 주 기술자입니다. Jason는 컴퓨팅에 PhD를 보유 하 고 있으며 현재 MCPD 및 MCTS 인증을 받았습니다. [Www.jrjlee.com](http://www.jrjlee.com/)에서 Jason의 기술 블로그를 읽을 수 있습니다.

Benjamin Yy는 경력 중에 백서, SDK 설명서, PowerPoint 프레젠테이션, 강사 교육 및 온라인 교육 과정을 작성 한 [콘텐츠 마스터가](http://www.contentmaster.com/) 있는 주 기술자입니다. ASP.NET 설명서 팀의 원래 구성원 인 경우 10 년 이상 Microsoft 웹 기술로 작업 했습니다.

## <a name="target-audience"></a>대상 사용자

이 자습서 집합은 ASP.NET 웹 응용 프로그램 개발자 및 Visual Studio 2010을 사용 하 여 엔터프라이즈급 웹 응용 프로그램을 만드는 솔루션 설계자를 위한 것입니다. 콘텐츠에서 가장 많은 가치를 얻으려면 Visual Studio 2010을 사용 하 고, TFS에 대 한 기본적인 지식이 있어야 하며, WCF (ASP.NET MVC 3, Windows Communication Foundation (WCF), IIS, SQL 등의 Microsoft 웹 플랫폼 기술을 인식 해야 합니다. 서버 및 Visual Studio 데이터베이스 프로젝트 그러나 배포 도구 및 기술에 익숙하지 않거나 CI 시스템을 설정 하는 방법을 알아야 할 필요가 없습니다.

## <a name="requirements"></a>요구 사항

연습을 수행 하 고 이러한 자습서에서 설명 하는 작업을 수행 하려면 개발 컴퓨터에이 소프트웨어를 설치 해야 합니다.

- Visual Studio 2010 Premium 또는 Ultimate Edition (서비스 팩 1 포함)
- .NET Framework 4.0
- 3\.5 .NET Framework 서비스 팩 1
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

이러한 연습에서 설명 하는 배포 단계를 수행 하려면 샘플 웹 응용 프로그램 배포 환경에 대 한 액세스 권한이 있어야 합니다. 최상의 결과를 위해 이러한 환경은 조직의 엔터프라이즈 배포 패턴을 반영 해야 합니다. 그런 다음이 설명서에 제공 된 연습은 조직의 배포 환경 및 요구 사항을 반영 하 여 수정할 수 있습니다.

## <a name="series-contents"></a>계열 내용

이 소개 섹션은 두 가지 추가 항목으로 구성 되어 있습니다. 이러한 기능은 다음과 같은 자습서에 대 한 보다 광범위 한 컨텍스트를 제공 하도록 설계 되었습니다.

- [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md). 이 항목에서는이 시리즈의 각 자습서를 고정 하는 시나리오에 대해 설명 합니다. 이 시나리오에서는 엔터프라이즈 규모의 웹 응용 프로그램을 개발 하면서 Fabrikam, i n c. 라는 가상 회사의 ALM (애플리케이션 수명 주기 관리) 요구 사항에 중점을 둔 시나리오입니다.
- [응용 프로그램 수명 주기 관리: 개발에서 프로덕션까지](application-lifecycle-management-from-development-to-production.md). 이 항목에서는 배포 프로세스에 대 한 높은 수준의 종단 간 개요를 제공 합니다. Fabrikam, i n c .는 연속 개발 프로세스의 일부로 테스트, 스테이징 및 프로덕션 환경을 통해 엔터프라이즈급 ASP.NET 웹 응용 프로그램을 이동 하는 방법을 보여 줍니다.

이 시리즈에는 네 가지 자습서 집합이 포함 되어 있습니다. 각는 웹 배포의 다양 한 측면에 중점을 둔 것입니다.

- [엔터프라이즈의 웹 배포](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). 이 자습서에서는 MSBuild 프로젝트 파일, 웹 게시 파이프라인, 웹 배포 및 기타 관련 기술에 대해 개념적인 소개를 제공 합니다. 이러한 도구를 함께 사용 하 여 복잡 한 배포 프로세스를 관리 하는 방법을 설명 합니다.
- [웹 배포용 서버 환경 구성](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md) 이 자습서에서는 웹 Deployment Agent 서비스 ("원격 에이전트") 또는 웹 배포 처리기 및 원격 데이터베이스 배포를 사용 하 여 원격 웹 패키지 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 Windows server를 구성 하는 방법을 설명 합니다. 사용자 환경에 적합 한 배포 방법을 선택 하는 방법에 대 한 지침을 제공 하 고 WFF를 사용 하 여 서버 팜의 모든 웹 서버에서 배포 된 웹 응용 프로그램을 복제 하는 방법을 설명 합니다.
- [웹 배포용 Team Foundation Server 구성](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 이 자습서에서는 CI 프로세스의 일부로 자동화 된 배포를 비롯 하 여 다양 한 배포 시나리오를 지원 하도록 TFS를 구성 하 고 특정 빌드의 배포를 수동으로 트리거한 방법을 설명 합니다.
- [고급 엔터프라이즈 웹 배포](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md). 이 자습서에서는 여러 환경에 데이터베이스 배포를 사용자 지정 하 고, 배포에서 파일 및 폴더를 제외 하 고, 배포 프로세스 중에 웹 응용 프로그램을 오프 라인 상태로 만드는 등의 다양 한 고급 배포 작업을 수행 하는 방법을 .

## <a name="where-to-start"></a>시작 위치

이 자습서 집합에서는 가상의 엔터프라이즈 배포 시나리오와 함께 현실적인 복잡성 수준의 샘플 솔루션을 사용 하 여 참조 구현을 제공 하 고 작업 및 연습에 일반적인 컨텍스트를 제공 합니다. 다음 항목인 [엔터프라이즈 웹 배포: 시나리오 개요](enterprise-web-deployment-scenario-overview.md)에서 시나리오 및 샘플 솔루션을 소개 합니다. 여기에서 사용자의 요구 사항에 가장 부합 하는 자습서와 항목을 통해 작업할 수 있습니다.

> [!div class="step-by-step"]
> [다음](enterprise-web-deployment-scenario-overview.md)
