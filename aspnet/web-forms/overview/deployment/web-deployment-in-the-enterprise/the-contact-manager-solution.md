---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Contact Manager 솔루션 | Microsoft Docs
author: jrjlee
description: 이 시리즈의 자습서에서는 샘플 솔루션&#x2014;&#x2014;을 사용 하 여 엔터프라이즈 규모의 응용 프로그램을 대표 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473813"
---
# <a name="the-contact-manager-solution"></a>Contact Manager 솔루션

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 [시리즈의 자습서](web-deployment-in-the-enterprise.md) 에서는 샘플 솔루션&#x2014;을 사용 하 여 엔터프라이즈&#x2014;규모의 응용 프로그램을 대표 하는 복잡 한 수준의 응용 프로그램을 나타냅니다. 이 항목에서는 Contact Manager 솔루션을 소개 하 고, 솔루션의 주요 구성 요소에 대해 설명 하 고, 엔터프라이즈 환경의 다양 한 대상 플랫폼에 이러한 종류의 응용 프로그램을 배포 하는 문제를 식별 합니다.
> 
> 이러한 자습서의 항목을 진행 하면서, 엔터프라이즈 배포 시나리오에서 특정 문제를 해결할 수 있는 방법을 설명 하는 참조 구현으로 Contact Manager 솔루션을 사용할 수 있습니다. 다음 항목인 [Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)에서는 개발자 워크스테이션에서 솔루션을 다운로드 하 고 실행 하는 방법을 설명 합니다.

## <a name="solution-overview"></a>솔루션 개요

Contact Manager 솔루션은 다음과 같은 4 개의 개별 프로젝트로 구성 됩니다.

![](the-contact-manager-solution/_static/image1.png)

- **연락처 관리자. Mvc**. 솔루션에 대 한 진입점을 나타내는 ASP.NET MVC 3 웹 응용 프로그램 프로젝트입니다. 사용자에 게 연락처 정보를 만들고 볼 수 있는 기능을 제공 하는 것과 같은 몇 가지 기본 웹 응용 프로그램 기능을 제공 합니다. 응용 프로그램은 WCF (Windows Communication Foundation) 서비스를 사용 하 여 연락처 및 ASP.NET 응용 프로그램 서비스 데이터베이스를 관리 하 여 인증 및 권한 부여를 관리 합니다.
- **연락처 관리자. 데이터베이스**. 이 프로젝트는 Visual Studio 데이터베이스 프로젝트입니다. 프로젝트는 연락처 세부 정보를 저장 하는 데이터베이스에 대 한 스키마를 정의 합니다.
- **연락처 관리자. 서비스**. WCF 웹 서비스 프로젝트입니다. WCF 서비스는 호출자가 작업 **관리자** 데이터베이스에서 만들기, 검색, 업데이트 및 삭제 (CRUD) 작업을 수행할 수 있도록 하는 끝점을 노출 합니다. 이 서비스는 **연락처 관리자** 데이터베이스와 **연락처 관리자. 일반적인 .dll** 어셈블리를 사용 합니다.
- **연락처 관리자. 일반적인**. 클래스 라이브러리 프로젝트입니다. WCF 서비스는이 어셈블리에 정의 된 형식을 사용 합니다.

솔루션에는 Publish 라는 솔루션 폴더도 포함 되어 있습니다. 여기에는 빌드 및 배포 프로세스를 제어 하 고 조작할 수 있는 방법을 보여 주는 다양 한 사용자 지정 프로젝트 파일 및 명령 파일이 포함 됩니다. 이러한 내용은이 자습서의 뒷부분에서 자세히 설명 합니다.

개념적 수준에서 솔루션의 구성 요소는 다음과 같습니다.

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> ASP.NET MVC 3 웹 응용 프로그램이 ASP.NET 멤버 자격 공급자를 사용 하는 동안 웹 응용 프로그램 내의 모든 페이지에서 익명 액세스를 허용 합니다. 이는 현실적인 구성이 아닙니다. 그러나 솔루션은 이러한 방식으로 설정 되므로 사용자 계정 및 역할을 구성 하지 않고도 솔루션을 보다 쉽게 배포 하 고 테스트할 수 있습니다.

## <a name="deployment-challenges"></a>배포 문제

Contact Manager 솔루션은 다양 한 엔터프라이즈 배포 시나리오에 공통적인 몇 가지 배포 문제를 보여 줍니다.

- 솔루션은 여러 종속 프로젝트로 구성 됩니다. 이러한 프로젝트는 동시에 배포 해야 합니다.
- 각 환경에 대해 연결 문자열 및 서비스 끝점을 업데이트 해야 하며, 많은 경우 개발자가이 정보를 사용할 수 없습니다.
- 스테이징 및 프로덕션 환경에 배포 하는 경우에는 기존 데이터를 유지 **해야 합니다.**
- ASP.NET 응용 프로그램 서비스 데이터베이스를 배포 하는 경우 일부 구성 데이터를 배포 하지만 사용자 계정 데이터는 생략 해야 합니다.
- 프로젝트에는 배포 하지 않아야 하는 일부 파일과 폴더가 포함 됩니다. 이러한 파일 및 폴더는 배포 프로세스에서 제외 해야 합니다.
- 솔루션은 TFS (Team Foundation Server) 빌드 서버에서 자동화 된 배포를 지원 해야 합니다.

## <a name="conclusion"></a>결론

이 항목에서는 Contact Manager 솔루션에 대 한 개략적인 개요를 제공 하 고 다양 한 엔터프라이즈 배포 시나리오에 공통적인 몇 가지 내재 된 배포 문제를 파악 했습니다. 이 자습서의 나머지 항목에서는 이러한 문제를 해결 하는 데 사용할 수 있는 몇 가지 기술에 대해 설명 합니다.

다음 항목인 [Contact Manager 솔루션 설정](setting-up-the-contact-manager-solution.md)에서는 개발자 워크스테이션에서 솔루션을 다운로드 하 고 실행 하는 방법을 설명 합니다.

> [!div class="step-by-step"]
> [이전](web-deployment-in-the-enterprise.md)
> [다음](setting-up-the-contact-manager-solution.md)
