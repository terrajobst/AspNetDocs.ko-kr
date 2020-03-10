---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: 엔터프라이즈 환경에 멤버 자격 데이터베이스 배포 | Microsoft Docs
author: jrjlee
description: 이 항목에서는 ASP.NET 응용 프로그램 서비스 데이터베이스를 프로 비전 할 때 해결 해야 하는 주요 고려 사항 및 문제에 대해 설명 합니다.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422159"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>엔터프라이즈 환경에 멤버 자격 데이터베이스 배포

[Jason Lee](https://github.com/jrjlee)

[PDF 다운로드](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 이 항목에서는 테스트, 준비 또는 프로덕션 환경에서 ASP.NET 응용 프로그램 서비스 데이터베이스 (일반적으로 멤버 자격 데이터베이스 라고 함)를 프로 비전 할 때 해결 해야 하는 주요 고려 사항 및 문제에 대해 설명 합니다. 또한 이러한 문제를 충족 하기 위해 사용할 수 있는 방법도 설명 합니다.

이 항목에서는 Fabrikam, i n c. 라는 가상 회사의 엔터프라이즈 배포 요구 사항을 기반으로 하는 일련의 자습서의 일부를 형성 합니다. 이 자습서 시리즈에서는 샘플 솔루션&#x2014;&#x2014;을 사용 [하 여](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)ASP.NET MVC 3 응용 프로그램, Windows Communication Foundation (WCF) 서비스 및 데이터베이스 프로젝트를 비롯 한 현실적인 복잡성의 웹 응용 프로그램을 나타냅니다.

이러한 자습서의 핵심에 나오는 배포 방법은 [프로젝트 파일 이해](../web-deployment-in-the-enterprise/understanding-the-project-file.md)에 설명 된 프로젝트 파일을 이해 하는 방법에 설명 되어 있습니다 .이는 빌드 프로세스가 모든 대상 환경에 적용&#x2014;되는 빌드 명령을 포함 하는 두 개의 프로젝트 파일과 환경 특정 빌드 및 배포 설정을 포함 하는 프로젝트 파일에 의해 제어 됩니다. 빌드 시 환경 관련 프로젝트 파일은 환경에 관계 없는 프로젝트 파일에 병합 되어 전체 빌드 명령 집합을 형성 합니다.

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>멤버 자격 데이터베이스를 배포할 때 발생 하는 문제는 무엇 인가요?

대부분의 경우 데이터베이스에 대 한 배포 전략을 세울 때 가장 먼저 고려해 야 할 사항은 배포 하려는 데이터입니다. 개발 또는 테스트 환경에서는 빠르고 쉬운 테스트를 용이 하 게 하기 위해 사용자 계정 데이터를 배포할 수 있습니다. 스테이징 또는 프로덕션 환경에서는 사용자 계정 데이터를 배포 하지 않을 가능성이 매우 낮습니다.

아쉽게도 ASP.NET 멤버 자격 데이터베이스에는이 결정을 훨씬 더 복잡 하 게 만드는 몇 가지 특정 과제가 도입 되었습니다.

- 스키마 전용 배포에서는 멤버 자격 데이터베이스를 작동 하지 않는 상태로 유지 합니다. 이는 멤버 자격 데이터베이스에 데이터베이스가 작동 하기 위해 필요로 하는 일부 구성 데이터 ( **aspnet\_SchemaVersions** 테이블)가 포함 되어 있기 때문입니다. 따라서 사용자 계정 데이터를 제외 하기 위해 멤버 자격 데이터베이스의 스키마 전용 배포를 수행 하는 경우 배포 후 스크립트를 실행 하 여 필수 구성 데이터를 추가 해야 합니다.
- 멤버 자격 데이터베이스 구성 방법에 따라 멤버 자격 공급자는 컴퓨터 키를 사용 하 여 암호를 암호화 하 고 데이터베이스에 저장할 수 있습니다. 이 경우 데이터베이스를 사용 하 여 배포 하는 모든 사용자 계정 데이터를 대상 서버에서 사용할 수 없게 됩니다. 이러한 이유로 사용자 계정 데이터 배포는 지원 되는 시나리오가 아닙니다.

## <a name="choosing-a-membership-database-strategy"></a>멤버 자격 데이터베이스 전략 선택

엔터프라이즈 서버 환경에서 멤버 자격 데이터베이스를 프로 비전 하는 방법을 선택 하는 경우 다음 지침을 따르십시오.

- 가능 하면 멤버 자격 데이터베이스를 배포 하지 마십시오. 대신 대상 데이터베이스 서버에서 수동으로 멤버 자격 데이터베이스를 만듭니다. 멤버 자격 데이터베이스 스키마를 사용자 지정 하지 않은 경우 [ASP.NET SQL Server 등록 도구 (aspnet\_regsql)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)를 사용 하 여 대상의 변환은 내부에 새 스키마를 만들 수 있습니다.
- 옵션은 없지만 멤버 자격 데이터베이스&#x2014;를 배포 하는 경우 데이터베이스 스키마&#x2014;를 광범위 하 게 수정한 경우 멤버 자격 데이터베이스의 스키마 전용 배포를 수행 하 고, 사용자 계정 데이터를 제외 하 고, 배포 후 스크립트를 실행 하 여 필요한 구성 데이터를 추가 해야 합니다. [방법: 사용자 계정을 포함 하지 않고 ASP.NET 멤버 자격 데이터베이스 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)에서 이러한 접근 방식에 대 한 광범위 한 지침을 찾을 수 있습니다.

*멤버 자격 데이터베이스의 스키마는 매우 정적일 수*있습니다. 멤버 자격 데이터베이스를 사용자 지정한 경우에도 정기적&#x2014;으로 스키마를 업데이트 해야 하는 것은 아닙니다. 웹 응용 프로그램 또는 데이터베이스 프로젝트의 코드와 같은 빈도로 변경 하지 않는 것이 좋습니다. 따라서 자동 또는 단일 단계 배포 프로세스에는 멤버 자격 데이터베이스를 포함할 필요가 없습니다.

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>VSDBCMD를 사용 하 여 멤버 자격 데이터베이스 스키마 업데이트

첫 번째 배포 후에 멤버 자격 데이터베이스의 구조를 수정 하는 경우 인터넷 정보 서비스 (IIS) 웹 배포 도구 (웹 배포)를 사용 하 여 데이터베이스를 다시 배포 하지 않으려고 할 수 있습니다. 웹 배포의 데이터베이스 배포 기능에는 대상 데이터베이스&#x2014;에 대 한 차등 업데이트를 수행 하는 기능이 포함 되어 있지 않습니다 웹 배포 데이터베이스를 삭제 하 고 다시 만들어야 합니다. 즉, 일반적으로 스테이징 또는 프로덕션 환경에서 원치 않는 기존 사용자 계정 데이터가 손실 됩니다.

대체 방법은 VSDBCMD 유틸리티를 사용 하 여 대상 데이터베이스의 스키마를 업데이트 하는 것입니다. VSDBCMD에는 두 가지 중요 한 기능이 포함 되어 있습니다. 첫째, 기존 데이터베이스의 스키마를 .dbschema 파일로 가져올 수 있습니다. 둘째, 기존 데이터베이스에 .dbschema 파일을 차등 업데이트로 배포할 수 있습니다. 즉, 대상 데이터베이스를 최신 상태로 유지 하는 데 필요한 변경만 수행 하 고 데이터를 잃지는 않습니다.

이러한 개략적인 단계를 사용 하 여 멤버 자격 데이터베이스 스키마를 업데이트할 수 있습니다.

1. VSDBCMD **가져오기** 작업을 사용 하 여 원본 멤버 자격 데이터베이스용 .dbschema 파일을 생성 합니다. 이 절차는 [방법: 명령 프롬프트에서 스키마 가져오기](https://msdn.microsoft.com/library/dd172135.aspx)에 설명 되어 있습니다.
2. VSDBCMD **배포** 작업을 사용 하 여 대상 멤버 자격 데이터베이스에 .dbschema 파일을 배포 합니다. 이 절차는 [VSDBCMD에 대 한 명령줄 참조에 설명 되어 있습니다. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx)

## <a name="conclusion"></a>결론

이 항목에서는 다양 한 대상 환경에서 ASP.NET 멤버 자격 데이터베이스를 프로 비전 해야 할 때 발생할 수 있는 몇 가지 문제에 대해 설명 했습니다. 특히 스키마 전용 배포가 작동 하지 않는 상태로 유지 되 고 사용자 계정 데이터 배포가 지원 되지 않는 이유에 대해 설명 했습니다. 또한 다양 한 시나리오에서 멤버 자격 데이터베이스를 프로 비전, 배포 및 업데이트 하는 방법에 대 한 지침도 제공 합니다.

## <a name="further-reading"></a>추가 참고 자료

VSDBCMD를 사용 하는 방법에 대 한 자세한 지침과 예제는 [vsdbcmd를 위한 명령줄 참조를 참조 하세요. EXE (배포 및 스키마 가져오기)](https://msdn.microsoft.com/library/dd193283.aspx) 및 [방법: 명령 프롬프트에서 스키마 가져오기](https://msdn.microsoft.com/library/dd172135.aspx) ASP.NET를 사용\_하 여를 사용 하 여 멤버 자격 데이터베이스를 만드는 방법에 대 한 자세한 내용은 [SQL Server Registration Tool (aspnet\_regsql)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)을 참조 하세요. 멤버 자격 데이터베이스를 배포 하는 방법에 대 한 일반적인 지침은 [방법: 사용자 계정을 포함 하지 않고 ASP.NET Membership 데이터베이스 배포](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](deploying-database-role-memberships-to-test-environments.md)
> [다음](excluding-files-and-folders-from-deployment.md)
