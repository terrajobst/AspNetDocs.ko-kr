---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 원본 제어 (Azure를 사용 하 여 실제 클라우드 앱 빌드) | Microsoft Docs
author: MikeWasson
description: Azure e-learning을 사용 하 여 실제 클라우드 앱 빌드는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 여기에는 다음을 수행할 수 있는 13 개의 패턴과 사례가 설명 되어 있습니다.
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: a6f445e46d41b646cf6c25af2e65bc73e831d5ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583707"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>원본 제어 (Azure를 사용 하 여 실제 클라우드 앱 빌드)

사람, [Mike Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Tom Dykstra](https://github.com/tdykstra)

[Fix It 프로젝트 다운로드](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) 또는 [전자 서적 다운로드](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Azure e-learning을 **사용 하 여 실제 클라우드 앱 빌드** 는 Scott Guthrie에서 개발한 프레젠테이션을 기반으로 합니다. 클라우드의 웹 앱을 성공적으로 개발 하는 데 도움이 되는 13 개의 패턴 및 사례에 대해 설명 합니다. 전자 문서에 대 한 자세한 내용은 [첫 번째 챕터](introduction.md)를 참조 하세요.

원본 제어는 팀 환경 뿐만 아니라 모든 클라우드 개발 프로젝트에 필수적입니다. 실행 취소 함수 및 자동 백업 없이 소스 코드를 편집 하거나 Word 문서를 편집 하는 것은 좋지 않으며, 소스 제어는 프로젝트 수준에서 이러한 기능을 제공 하므로 문제가 발생할 경우 훨씬 더 많은 시간을 절약할 수 있습니다. 클라우드 소스 제어 서비스를 사용 하면 복잡 한 설정에 대해 더 이상 걱정할 필요가 없으며 최대 5 명의 사용자에 게 Azure Repos 소스 제어를 무료로 사용할 수 있습니다.

이 챕터의 첫 번째 부분에서는 다음에 유의 해야 하는 세 가지 주요 모범 사례를 설명 합니다.

- [자동화 스크립트를 소스 코드로 처리](#scripts) 하 고 응용 프로그램 코드와 함께 버전을 사용 합니다.
- 비밀 (자격 증명과 같은 중요 한 데이터)을 소스 코드 리포지토리로 [체크 인 하지 마십시오](#secrets) .
- DevOps 워크플로를 사용 하도록 [원본 분기를 설정](#devops) 합니다.

이 장의 나머지 부분에서는 Visual Studio, Azure 및 Azure Repos에서 이러한 패턴을 구현 하는 몇 가지 샘플을 제공 합니다.

- [Visual Studio에서 소스 제어에 스크립트 추가](#vsscripts)
- [중요 한 데이터를 Azure에 저장](#appsettings)
- [Visual Studio 및 Azure Repos에서 Git 사용](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>자동화 스크립트를 소스 코드로 처리

클라우드 프로젝트에서 작업 하는 경우 자주 변경 하 고 고객이 보고 한 문제에 신속 하 게 대응할 수 있도록 하려고 합니다. [모든 기능 자동화](automate-everything.md) 의 설명에 따라 자동화 스크립트를 사용 하 여 신속 하 게 응답 합니다. 환경을 만들고, 배포 하 고, 크기를 조정 하는 데 사용 하는 모든 스크립트는 응용 프로그램 소스 코드와 동기화 해야 합니다.

스크립트를 코드와 동기화 상태로 유지 하려면 소스 제어 시스템에 저장 합니다. 그런 다음 변경 내용을 롤백하거나 개발 코드와 다른 프로덕션 코드를 신속 하 게 수정 해야 하는 경우 변경 된 설정이 나 필요한 버전의 복사본이 있는 팀 멤버를 추적 하는 데 걸리는 시간을 낭비 하지 않아도 됩니다. 필요한 스크립트가 필요한 코드 베이스와 동기화 되 고 모든 팀 멤버가 동일한 스크립트를 사용 하 고 있다고 확신할 수 있습니다. 그런 다음 프로덕션 또는 새로운 기능 개발에 대 한 핫 픽스 테스트 및 배포를 자동화 해야 하는지 여부에 관계 없이 업데이트 해야 하는 코드에 대 한 올바른 스크립트가 제공 됩니다.

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>암호 체크 인 안 함

소스 코드 리포지토리는 일반적으로 암호와 같은 중요 한 데이터를 적절 하 게 보호 하기 위해 너무 많은 사람이 액세스할 수 있습니다. 스크립트에서 암호와 같은 암호를 사용 하는 경우 소스 코드에 저장 되지 않도록 해당 설정을 매개 변수화 하 고 다른 위치에 암호를 저장 합니다.

예를 들어 Azure에서는 게시 프로필 생성을 자동화 하기 위해 게시 설정이 포함 된 파일을 다운로드할 수 있습니다. 이러한 파일에는 Azure 서비스를 관리할 수 있는 권한이 있는 사용자 이름 및 암호가 포함 됩니다. 이 방법을 사용 하 여 게시 프로필을 만들 때 이러한 파일을 원본 제어에 체크 인하면 모든 사용자가 해당 사용자 이름과 암호를 볼 수 있습니다. 암호는 암호화 되어 있으며 기본적으로 소스 제어에 포함 되지 않는 *pubxml 사용자* 파일에 있기 때문에 게시 프로필 자체에 안전 하 게 저장할 수 있습니다.

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>DevOps 워크플로를 용이 하 게 하는 구조 소스 분기

리포지토리에서 분기를 구현 하는 방법은 새 기능을 개발 하 고 프로덕션에서 문제를 해결 하는 기능에 영향을 줍니다. 다음은 많은 중간 규모 팀에서 사용 하는 패턴입니다.

![소스 분기 구조](source-control/_static/image1.png)

마스터 분기는 항상 프로덕션에 있는 코드와 일치 합니다. 마스터 아래의 분기는 개발 수명 주기의 다른 단계에 해당 합니다. 개발 분기에서는 새 기능을 구현 합니다. 소규모 팀의 경우 마스터 및 개발을 사용할 수 있지만, 사용자에 게 개발과 마스터 사이에 스테이징 분기가 있는 것이 좋습니다. 업데이트를 프로덕션으로 이동 하기 전에 최종 통합 테스트에 대해 준비를 사용할 수 있습니다.

큰 팀의 경우에는 각각의 새로운 기능에 대해 별도의 분기가 있을 수 있습니다. 소규모 팀의 경우 모든 사용자가 개발 분기에 체크 인할 수 있습니다.

각 기능에 대 한 분기가 있는 경우 기능 A가 준비 되 면 소스 코드 변경 내용을 개발 분기에 병합 하 고 다른 기능 분기에 병합할 수 있습니다. 이 소스 코드 병합 프로세스는 시간이 많이 소요 될 수 있으며, 기능을 별도로 유지 하면서 이러한 작업을 방지 하기 위해 일부 팀은 기능 *[설정/해제](http://en.wikipedia.org/wiki/Feature_toggle)* ( *기능 플래그*라고도 함) 라는 대체를 구현 합니다. 즉, 모든 기능의 모든 코드가 동일한 분기에 있지만 코드에서 스위치를 사용 하 여 각 기능을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 예를 들어 기능 A가 Fix It 앱 작업의 새 필드이 고 기능 B가 캐싱 기능을 추가 한다고 가정 합니다. 두 기능의 코드는 모두 개발 분기에 있을 수 있지만 앱은 변수가 true로 설정 된 경우에만 새 필드를 표시 하며, 다른 변수가 true로 설정 된 경우에만 캐싱을 사용 합니다. 기능 A를 승격할 준비가 되지 않았지만 기능 B가 준비 된 경우 기능 A 스위치를 사용 하 고 기능 B 스위치를 사용 하 여 모든 코드를 프로덕션으로 승격할 수 있습니다. 그런 다음 기능 A를 마무리 하 고 나중에 소스 코드를 병합 하지 않고 모두 승격할 수 있습니다.

기능에 대 한 분기 또는 토글을 사용 하는지 여부에 관계 없이 이와 같은 분기 구조를 사용 하면 민첩 하 고 반복 가능한 방식으로 코드를 개발 환경에서 프로덕션으로 이동할 수 있습니다.

이 구조를 사용 하 여 고객 피드백에 신속 하 게 대응할 수도 있습니다. 프로덕션에 대 한 빠른 수정 작업을 수행 해야 하는 경우 agile 방식으로 효율적으로 수행할 수도 있습니다. Master 또는 스테이징의 분기를 만들 수 있으며,이 분기를 마스터에 병합 하 고 개발 및 기능 분기로 배포할 준비가 되었을 때 사용할 수 있습니다.

![핫픽스 분기](source-control/_static/image2.png)

프로덕션 및 개발 분기를 분리 하 여 이와 같은 분기 구조가 없는 경우 프로덕션 문제는 프로덕션 수정과 함께 새로운 기능 코드를 승격할 수 있는 위치에 배치할 수 있습니다. 새 기능 코드는 완전 하 게 테스트 및 프로덕션 준비가 되지 않았을 수 있으며, 준비 되지 않은 변경 작업을 수행 해야 할 수도 있습니다. 또는 변경을 테스트 하 고 배포 준비를 완료 하기 위해 픽스를 지연 해야 할 수도 있습니다.

다음에는 Visual Studio, Azure 및 Azure Repos에서 이러한 세 가지 패턴을 구현 하는 방법에 대 한 예제가 나와 있습니다. 이에 대 한 자세한 단계별 방법에 대 한 지침은 다음과 같습니다. 필요한 모든 컨텍스트를 제공 하는 자세한 지침은 챕터의 끝에 있는 [리소스](#resources) 섹션을 참조 하세요.

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Visual Studio에서 소스 제어에 스크립트 추가

Visual studio 솔루션 폴더 (프로젝트가 소스 제어에 있다고 가정)에 포함 하 여 Visual Studio의 소스 제어에 스크립트를 추가할 수 있습니다. 이 작업을 수행 하는 한 가지 방법은 다음과 같습니다.

솔루션 폴더 ( *.sln* 파일이 있는 동일한 폴더)에 스크립트에 대 한 폴더를 만듭니다.

![자동화 폴더](source-control/_static/image3.png)

스크립트 파일을 폴더에 복사 합니다.

![자동화 폴더 내용](source-control/_static/image4.png)

Visual Studio에서 솔루션 폴더를 프로젝트에 추가 합니다.

![새 솔루션 폴더 메뉴 선택](source-control/_static/image5.png)

스크립트 파일을 솔루션 폴더에 추가 합니다.

![기존 항목 추가 메뉴 선택](source-control/_static/image6.png)

![기존 항목 추가 대화 상자](source-control/_static/image7.png)

이제 스크립트 파일이 프로젝트에 포함 되 고 소스 제어는 해당 소스 코드 변경 내용과 함께 버전 변경 내용을 추적 합니다.

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>중요 한 데이터를 Azure에 저장

Azure 웹 사이트에서 응용 프로그램을 실행 하는 경우 소스 제어에 자격 증명을 저장 하지 않는 한 가지 방법은 대신 Azure에 저장 하는 것입니다.

예를 들어 Fix It 응용 프로그램은 해당 Web.config 파일에 저장 되는 두 개의 연결 문자열을 프로덕션에 저장 하 고 Azure 저장소 계정에 대 한 액세스를 제공 하는 키를 저장 합니다.

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

이러한 설정에 대 한 실제 프로덕션 값을 *web.config 파일에* 배치 하거나 web.config 파일에 배치 하 여 배포 중에 삽입 하 *는 web.config 변환을* 구성 하면 원본 리포지토리에 저장 됩니다. 프로덕션 게시 프로필에 데이터베이스 연결 문자열을 입력 하면 *pubxml* 파일에 암호가 표시 됩니다. 원본 제어에서 *pubxml* 파일을 제외할 수 있지만 다른 모든 배포 설정을 공유 하는 경우의 이점을 잃게 됩니다.

Azure *는 web.config 파일의* **appSettings** 및 연결 문자열 섹션에 대 한 대안을 제공 합니다. Azure 관리 포털에서 웹 사이트에 대 한 **구성** 탭의 관련 부분은 다음과 같습니다.

![포털의 appSettings 및 connectionStrings](source-control/_static/image8.png)

이 웹 사이트에 프로젝트를 배포 하 고 응용 프로그램이 실행 되는 경우 Azure에 저장 한 값은 web.config 파일에 있는 값에 관계 없이 재정의 됩니다.

관리 포털을 사용 하거나 스크립트를 사용 하 여 Azure에서 이러한 값을 설정할 수 있습니다. [모두 자동화](automate-everything.md) 단원에서 확인 한 환경 만들기 자동화 스크립트는 Azure SQL Database 만들고, 저장소 및 SQL Database 연결 문자열을 가져오고, 이러한 비밀을 웹 사이트의 설정에 저장 합니다.

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

실제 값이 소스 리포지토리에 유지 되지 않도록 스크립트에 매개 변수가 있습니다.

개발 환경에서 로컬로 실행 하는 경우 앱은 로컬 web.config 파일을 읽고 연결 문자열은 웹 프로젝트의 *app\_Data* 폴더에 있는 LocalDB SQL Server 데이터베이스를 가리킵니다. Azure에서 앱을 실행 하는 경우 앱이 web.config 파일에서 이러한 값을 읽으려고 시도 하 고,이 값은 web.config 파일에 실제로 있는 것이 아니라 웹 사이트에 대해 저장 된 값입니다.

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>Visual Studio 및 Azure DevOps에서 Git 사용

모든 원본 제어 환경을 사용 하 여 앞에서 제공 된 DevOps 분기 구조를 구현할 수 있습니다. 분산 된 팀의 경우 dvcs ( [distributed version control system](http://en.wikipedia.org/wiki/Distributed_revision_control) )를 사용 하는 것이 가장 좋습니다. 다른 팀의 경우 [중앙 집중식 시스템이](http://en.wikipedia.org/wiki/Revision_control) 더 효율적으로 작동할 수 있습니다.

[Git](http://git-scm.com/) 는 널리 사용 되는 분산 버전 제어 시스템입니다. 원본 제어에 Git를 사용 하는 경우 로컬 컴퓨터의 모든 기록과 함께 리포지토리의 전체 복사본을 갖게 됩니다. 네트워크에 연결 되지 않은 경우 계속 해 서 작업을 수행할 수 있기 때문에 많은 사람들이 선호 하는 것이 좋습니다. 계속 해 서 커밋 및 롤백을 수행 하 고, 분기를 만들고 전환 하는 등의 작업을 수행할 수 있습니다. 네트워크에 연결 된 경우에도 모든 것이 로컬 인 경우 분기를 만들고 분기를 전환 하는 것이 더 쉽고 빠릅니다. 다른 개발자에 게 영향을 주지 않고 로컬 커밋 및 롤백을 수행할 수도 있습니다. 그리고 서버에 보내기 전에 커밋을 일괄 처리할 수 있습니다.

[Azure Repos](/azure/devops/repos/index?view=vsts) 는 [Git](/azure/devops/repos/git/?view=vsts) 및 [Team Foundation 버전 제어](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; 중앙화 된 원본 제어)를 제공 합니다. [여기](https://app.vsaex.visualstudio.com/signup)에서 Azure devops를 시작 하세요.

Visual Studio 2017에는 기본 제공, 최고 수준의 [Git 지원](https://msdn.microsoft.com/library/hh850437.aspx)기능이 포함 되어 있습니다. 이 작업을 수행 하는 방법에 대 한 간단한 데모는 다음과 같습니다.

Visual Studio에서 프로젝트를 열고 **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 **소스 제어에 솔루션 추가**를 선택 합니다.

![소스 제어에 솔루션 추가](source-control/_static/image9.png)

Visual Studio는 TFVC (중앙 집중식 버전 제어) 또는 Git를 사용할지 여부를 묻습니다.

![소스 제어 선택](source-control/_static/image10.png)

Git를 선택 하 고 **확인**을 클릭 하면 Visual Studio에서 솔루션 폴더에 새 로컬 Git 리포지토리를 만듭니다. 새 리포지토리에 파일이 아직 없습니다. Git 커밋을 수행 하 여 리포지토리에 추가 해야 합니다. **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭 한 다음 **커밋**을 클릭 합니다.

![커밋](source-control/_static/image11.png)

Visual Studio는 커밋에 대 한 모든 프로젝트 파일을 자동으로 준비 하 고 **포함 된 변경 내용** 창에 **팀 탐색기** 에 나열 합니다. 커밋에 포함 하지 않으려는 항목이 있는 경우 해당 항목을 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 **제외**를 클릭 합니다.

![팀 탐색기](source-control/_static/image12.png)

커밋 주석을 입력 하 고 **커밋**을 클릭 하면 Visual Studio에서 커밋을 실행 하 고 커밋 ID를 표시 합니다.

![변경 내용 팀 탐색기](source-control/_static/image13.png)

이제 리포지토리의 항목과 다른 코드를 변경 하는 경우 차이점을 쉽게 볼 수 있습니다. 변경한 파일을 마우스 오른쪽 단추로 클릭 하 고, 수정 되지 않은 항목과 **비교**를 선택 하 고, 커밋되지 않은 변경 내용을 보여 주는 비교 표시를 가져옵니다.

![수정 되지 않은 항목과 비교](source-control/_static/image14.png)

![변경 내용을 표시 하는 Diff](source-control/_static/image15.png)

변경 내용을 쉽게 확인 하 고 체크 인할 수 있습니다.

분기를 만들어야 한다고 가정 합니다. Visual Studio 에서도이 작업을 수행할 수 있습니다. **팀 탐색기**에서 **새 분기**를 클릭 합니다.

![새 분기 팀 탐색기](source-control/_static/image16.png)

분기 이름을 입력 하 고 **분기 만들기**를 클릭 합니다. **분기 체크 아웃**을 선택 하면 Visual Studio에서 새 분기가 자동으로 체크 아웃 됩니다.

![새 분기 팀 탐색기](source-control/_static/image17.png)

이제 파일을 변경 하 고이 분기에 체크 인할 수 있습니다. 분기 간을 쉽게 전환할 수 있으며 Visual Studio에서 체크 아웃 한 분기에 파일을 자동으로 동기화 합니다. 이 예제에서는 *\_레이아웃* 의 웹 페이지 제목을 HotFix1 branch의 "Hot Fix 1"로 변경 했습니다.

![Hotfix1 분기](source-control/_static/image18.png)

마스터 분기로 다시 전환 하면 *\_Layout* 파일의 내용이 마스터 분기에 있는 것으로 자동으로 되돌아갑니다.

![Master 분기](source-control/_static/image19.png)

이를 통해 분기를 신속 하 게 만들고 분기 간에 대칭 이동 하는 방법에 대 한 간단한 예를 확인할 수 있습니다. 이 기능을 사용 하면 [모든 항목 자동](automate-everything.md) 구성 장에 제공 된 자동화 스크립트 및 분기 구조를 사용 하 여 매우 민첩 한 워크플로를 사용할 수 있습니다. 예를 들어 개발 분기에서 작업 하 고, master에서 핫 픽스 분기를 만들고, 새 분기로 전환 하 고, 변경 내용을 적용 하 고, 변경 내용을 적용 하 고, 다시 개발 분기로 전환 하 고, 수행한 작업을 계속할 수 있습니다.

Visual Studio에서 로컬 Git 리포지토리로 작업 하는 방법은 여기에서 볼 수 있습니다. 팀 환경에서는 일반적으로 변경 내용을 공통 리포지토리로 푸시합니다. Visual Studio 도구를 사용 하 여 원격 Git 리포지토리를 가리킬 수도 있습니다. 이 목적을 위해 GitHub.com를 사용 하거나, [Git 및 Azure Repos](/azure/devops/repos/git/overview?view=vsts) 를 사용 하 여 작업 항목 및 버그 추적과 같은 다른 모든 Azure devops 기능과 통합할 수 있습니다.

물론 agile 분기 전략을 구현할 수 있는 유일한 방법은 아닙니다. 중앙 집중식 원본 제어 리포지토리를 사용 하 여 동일한 agile 워크플로를 사용 하도록 설정할 수 있습니다.

## <a name="summary"></a>요약

언제 든 지 변경 하 여 안전 하 고 예측 가능한 방식으로 사용할 수 있는 방법에 따라 원본 제어 시스템의 성공 여부를 측정 합니다. 1 일 또는 2 개의 수동 테스트를 수행 해야 하기 때문에 변경 하는 것을 알게 되 면 몇 분 내에 또는 최악의 경우에 변경 내용을 적용할 수 있도록 프로세스 또는 테스트를 수행 해야 하는 작업을 사용자에 게 요청할 수 있습니다. 이 작업을 수행 하는 한 가지 전략은 연속 통합 및 지속적인 업데이트를 구현 하는 것입니다 .이에 대해서는 [다음 장에서](continuous-integration-and-continuous-delivery.md)다룰 것입니다.

<a id="resources"></a>
## <a name="resources"></a>자료

분기 전략에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Team Foundation Server 2012를 사용 하 여 릴리스 파이프라인 빌드](https://msdn.microsoft.com/library/dn449957.aspx) Microsoft 패턴 및 사례 설명서 분기 전략에 대 한 설명은 6 장을 참조 하세요. 기능은 기능 분기를 전환 하 고 기능에 대 한 분기를 사용 하는 경우 단기 (몇 시간 또는 며칠)를 유지 하도록 합니다.
- [버전 제어 가이드](https://aka.ms/vsarsolutions). ALM Rangers의 분기 전략에 대 한 가이드입니다. 다운로드 탭에서 분기 전략 .pdf를 참조 하세요.
- [소프트웨어 개발 기능 전환](https://msdn.microsoft.com/magazine/dn683796.aspx) MSDN Magazine 문서입니다.
- [기능을 설정/해제](http://martinfowler.com/bliki/FeatureToggle.html)합니다. Martin Fowler의 블로그에서 기능 설정/해제/기능 플래그를 소개 합니다.
- [기능이 Vs 기능 분기를 전환](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)합니다. 다른 블로그 게시물의 기능을 설정 하는 방법에 대 한 자세한 내용은 Dylan Smith.

원본 제어 리포지토리에 유지 하지 않아야 하는 중요 한 정보를 처리 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET 및 Azure App Service에 암호 및 기타 중요 한 데이터를 배포 하기 위한 모범 사례](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)입니다.
- [Azure 웹 사이트: 응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)입니다. *Web.config 파일의* `appSettings` 및 `connectionStrings` 데이터를 재정의 하는 Azure 기능을 설명 합니다.
- [Stefan Schackow를 사용 하 여 Azure 웹 사이트의 사용자 지정 구성 및 응용 프로그램 설정](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)

중요 한 정보를 소스 제어에서 제외 하는 다른 방법에 대 한 자세한 내용은 [ASP.NET MVC: 소스 제어에서 비공개 설정 유지](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)를 참조 하세요.

> [!div class="step-by-step"]
> [이전](automate-everything.md)
> [다음](continuous-integration-and-continuous-delivery.md)
