---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: '실습: 유지 관리 가능한 Azure Websites: 변경 및 확장 관리 | Microsoft Docs'
author: rick-anderson
description: 이 랩에서 Microsoft Azure를 사용 하 여 웹 사이트를 쉽게 빌드하고 프로덕션에 배포 하는 방법을 알아봅니다.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506375"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>실습: 유지 관리 가능한 Azure Websites: 변경 및 확장 관리

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

> Microsoft Azure를 사용 하면 웹 사이트를 쉽게 빌드하고 프로덕션에 배포할 수 있습니다. 그러나 응용 프로그램이 라이브 상태인 경우에는 작업을 시작할 수 없습니다. 변경 요구 사항, 데이터베이스 업데이트, 크기 조정 등을 처리 해야 합니다. 다행히 사이트를 원활 하 게 실행 하는 데 도움이 되는 다양 한 기능을 제공 하는 Azure App Service 합니다.
>
> Azure는 모든 규모의 웹 응용 프로그램에 대해 안전 하 고 유연한 개발, 배포 및 확장 옵션을 제공 합니다. 인프라를 관리할 필요없이 기존의 도구를 활용하여 응용 프로그램을 만들고 배포하세요.
>
> 선호 하는 개발 도구를 사용 하 여 만든 콘텐츠를 쉽게 배포 하 여 몇 분 내에 프로덕션 웹 응용 프로그램을 프로 비전 하세요. **Git**, **GitHub**, **Bitbucket**, **TFS**및 **DropBox**에 대 한 지원을 사용 하 여 소스 제어에서 직접 기존 사이트를 배포할 수 있습니다. Windows에서 **PowerShell** 을 사용 하거나 모든 OS에서 실행 되는 **CLI** 도구에서 즐겨 사용 하는 IDE 또는 스크립트에서 직접 배포 합니다. 배포 된 후에는 지속적인 배포 지원을 통해 사이트를 지속적으로 최신 상태로 유지 합니다.
>
> Azure는 빅 이거나 작은 모든 데이터에 대 한 확장 가능 하 고 지속적인 클라우드 저장소, 백업 및 복구 솔루션을 제공 합니다. 프로덕션 환경에 응용 프로그램을 배포 하는 경우 테이블, Blob 및 SQL 데이터베이스와 같은 저장소 서비스는 클라우드에서 응용 프로그램을 확장 하는 데 도움이 됩니다.
>
> SQL database를 사용 하면 응용 프로그램의 새 버전을 배포할 때 생산적인 데이터베이스를 최신 상태로 유지 하는 것이 중요 합니다. **Entity Framework Code First 마이그레이션**덕분에 몇 분 내에 환경을 업데이트 하기 위해 데이터 모델의 개발 및 배포가 간소화 되었습니다. 이 실습 랩에서는 Microsoft Azure의 프로덕션 환경에 웹 앱을 배포할 때 발생할 수 있는 다양 한 항목을 보여 줍니다.
>
> 모든 샘플 코드와 코드 조각은 [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)에서 사용할 수 있는 웹 캠프 교육 키트에 포함 되어 있습니다.
>
> 이 항목에 대 한 자세한 적용 범위는 [Azure를 사용 하 여 실제 클라우드 앱 빌드](building-real-world-cloud-apps-with-windows-azure/introduction.md)를 참조 하세요.

<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 기존 모델을 사용 하 여 Entity Framework 마이그레이션 사용
- Entity Framework 마이그레이션을 사용 하 여 개체 모델 및 데이터베이스를 적절 하 게 업데이트
- Git를 사용 하 여 Azure App Service에 배포
- Azure 관리 포털을 사용 하 여 이전 배포로 롤백
- Azure Storage를 사용 하 여 웹 앱 크기 조정
- Azure 관리 포털을 사용 하 여 웹 앱에 대 한 자동 크기 조정 구성
- Visual Studio에서 부하 테스트 프로젝트 만들기 및 구성

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [.NET 용 Azure SDK 2.2](https://www.microsoft.com/windowsazure/sdk/)
- [GIT 버전 제어 시스템](http://git-scm.com/download)
- Microsoft Azure 구독

    - [무료 평가판](https://aka.ms/watk-freetrial) 등록
    - MSDN 또는 MSDN 플랫폼 구독자가 포함 된 Visual Studio Professional, Test Professional, Premium 또는 Ultimate 인 경우 지금 [msdn 혜택](https://aka.ms/watk-msdn) 을 활성화 하 여 Azure에서 개발 및 테스트를 시작 하세요.
    - [BizSpark](https://aka.ms/watk-bizspark) 멤버는 Visual Studio Ultimate with MSDN 구독을 통해 Azure 혜택을 자동으로 수신 합니다.
    - [Microsoft 파트너 네트워크](https://aka.ms/watk-mpn) Cloud Essentials 프로그램의 구성원은 무료로 월간 Azure 크레딧을 받습니다.

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기를 열고 랩의 **원본** 폴더로 이동 합니다.
2. **Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다. 사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.

> [!NOTE]
> 각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다. 연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다. 이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.

---

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [Entity Framework 마이그레이션 사용](#Exercise1)
2. [스테이징에 웹 앱 배포](#Exercise2)
3. [프로덕션 환경에서 배포 롤백 수행](#Exercise3)
4. [Azure Storage를 사용 하 여 크기 조정](#Exercise4)
5. [Web Apps에 자동 크기 조정 사용](#Exercise5) (Visual Studio 2013 Ultimate edition의 경우 선택 사항)

이 랩을 완료 하는 데 소요 되는 예상 시간: **75 분**

> [!NOTE]
> Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다. 개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>연습 1: Entity Framework 마이그레이션 사용

응용 프로그램을 개발 하는 경우 데이터 모델이 시간이 지남에 따라 변경 될 수 있습니다. 이러한 변경 내용은 데이터베이스의 기존 모델에 영향을 줄 수 있으며 (새 버전을 만드는 경우) 오류를 방지 하기 위해 데이터베이스를 최신 상태로 유지 하는 것이 중요 합니다.

모델에서 이러한 변경 내용에 대 한 추적을 간소화 하기 위해 모델을 데이터베이스 스키마와 비교 하 여 자동으로 변경 내용을 감지 하 고 데이터베이스 업데이트를 위한 특정 코드를 생성 하 여 데이터베이스의 새 *버전* 을 만들 **Entity Framework Code First 마이그레이션** .

이 연습에서는 응용 프로그램에 대해 **마이그레이션을** 사용 하도록 설정 하는 방법과 데이터베이스 업데이트를 위한 변경 내용을 쉽게 검색 하 고 생성 하는 방법을 보여 줍니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>작업 1-마이그레이션 사용

이 태스크에서는 **Geek of 퀴즈** 데이터베이스에 **Entity Framework Code First 마이그레이션** 를 사용 하도록 설정 하 고 모델을 변경 하 고 데이터베이스에 변경 내용을 반영 하는 방법을 이해 하는 단계를 안내 합니다.

1. Visual Studio를 열고 **Source\Ex1-UsingEntityFrameworkMigrations\Begin**에서 **GeekQuiz** 솔루션 파일을 엽니다.
2. **NuGet** 패키지 종속성을 다운로드 하 고 설치 하기 위해 솔루션을 빌드합니다. 이렇게 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **솔루션 빌드** 를 클릭 하거나 **ctrl + Shift + B**를 누릅니다.
3. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.
4. **패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다. 기존 모델을 기반으로 하는 초기 마이그레이션이 생성 됩니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![마이그레이션 사용](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "마이그레이션을 사용하도록 설정")

    *마이그레이션 사용*

    > [!NOTE]
    > 이 명령은 **Configuration.cs**이라는 파일이 포함 된 geek of 퀴즈 프로젝트에 **마이그레이션** 폴더를 추가 합니다. **구성** 클래스를 사용 하 여 사용자 컨텍스트에 대 한 마이그레이션 동작을 구성할 수 있습니다.
5. 마이그레이션을 사용 하는 경우 **Geek of 퀴즈** 에 필요한 초기 데이터로 데이터베이스를 채우도록 **구성** 클래스를 업데이트 해야 합니다. **마이그레이션**아래에서이 랩의 **source\assets** 폴더에 있는 **Configuration.cs** 파일을 바꿉니다.

    > [!NOTE]
    > **마이그레이션은** 모든 데이터베이스 업데이트에서 **초기값** 메서드를 호출 하므로 데이터베이스에서 레코드가 중복 되지 않도록 해야 합니다. **Addorupdate** 메서드는 중복 데이터를 방지 하는 데 도움이 됩니다.
6. 초기 마이그레이션을 추가 하려면 다음 명령을 입력 한 다음 **enter**키를 누릅니다.

    > [!NOTE]
    > LocalDB 인스턴스에 &quot;GeekQuizProd&quot; 라는 데이터베이스가 없는지 확인 합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![기본 스키마 마이그레이션 추가](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "기본 스키마 마이그레이션 추가")

    *기본 스키마 마이그레이션 추가*

    > [!NOTE]
    > **추가-마이그레이션은** 마지막 마이그레이션을 만든 이후 모델에 대 한 변경 내용에 따라 다음 마이그레이션을 스 캐 폴드 됩니다. 이 경우 프로젝트의 첫 번째 마이그레이션 이므로 **TriviaContext** 클래스에 정의 된 모든 테이블을 만들기 위한 스크립트가 추가 됩니다.
7. 다음 명령을 실행 하 여 마이그레이션을 실행 하 여 데이터베이스를 업데이트 합니다. 이 명령의 경우 **자세한 정보** 플래그를 지정 하 여 대상 데이터베이스에 적용 되는 SQL 문을 확인 합니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![초기 데이터베이스를 만드는 중](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "초기 데이터베이스를 만드는 중")

    *초기 데이터베이스를 만드는 중*

    > [!NOTE]
    > **업데이트-** 데이터베이스에 보류 중인 모든 마이그레이션을 적용 합니다. 이 경우에는 web.config 파일에 정의 된 연결 문자열을 사용 하 여 데이터베이스를 만듭니다.
8. **보기** 메뉴로 이동 하 여 **SQL Server 개체 탐색기**을 엽니다.

    ![SQL Server 개체 탐색기에서 열기](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "SQL Server 개체 탐색기에서 열기")

    *SQL Server 개체 탐색기에서 열기*
9. **SQL Server 개체 탐색기** 창에서 **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가** ... 옵션을 선택 하 여 LocalDB 인스턴스에 연결 합니다.

    ![SQL Server 인스턴스 추가](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "SQL Server 인스턴스 추가")

    *SQL Server 개체 탐색기에 SQL Server 인스턴스 추가*
10. **서버 이름** 을 *(localdb) \v11.0* 으로 설정 하 고 **Windows 인증** 을 인증 모드로 유지 합니다. **연결**을 클릭하여 계속합니다.

    ![LocalDB에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "LocalDB에 연결")

    *LocalDB에 연결*
11. **GeekQuizProd** 데이터베이스를 열고 **Tables** 노드를 확장 합니다. 여기에서 볼 수 있듯이 **TriviaContext** 클래스에 정의 된 모든 테이블을 생성 하는 **업데이트 데이터베이스** 명령입니다. Dbo를 찾습니다 **. TriviaQuestions** 테이블을 열고 columns 노드를 엽니다. 다음 태스크에서는이 테이블에 새 열을 추가 하 고 **마이그레이션을**사용 하 여 데이터베이스를 업데이트 합니다.

    ![기타 정보 질문 열](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "기타 정보 질문 열")

    *기타 정보 질문 열*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>작업 2 – 마이그레이션을 사용 하 여 데이터베이스 스키마 업데이트

이 태스크에서는 **Entity Framework Code First 마이그레이션** 를 사용 하 여 모델의 변경 내용을 감지 하 고 데이터베이스를 업데이트 하는 데 필요한 코드를 생성 합니다. 새 속성을 추가 하 여 **Triviaquestions** 엔터티를 업데이트 합니다. 그런 다음 명령을 실행 하 여 테이블에 새 열을 포함 하는 새 마이그레이션을 만듭니다.

1. **솔루션 탐색기**에서 **모델** 폴더 내에 있는 **TriviaQuestion.cs** 파일을 두 번 클릭 합니다.
2. 다음 코드 조각과 같이 **힌트**라는 새 속성을 추가 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. **패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다. 모델의 변경 내용을 반영 하는 새 마이그레이션이 생성 됩니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![추가-마이그레이션](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "추가-마이그레이션")

    *추가-마이그레이션*

    > [!NOTE]
    > 마이그레이션 파일은 **위쪽** 및 **아래쪽**의 두 가지 방법으로 구성 됩니다.
    >
    > - **Up** 메서드는 현재 버전의 응용 프로그램을 데이터베이스에 적용 해야 하는 변경 내용을 지정 하는 데 사용 됩니다.
    > - **Down** 은 **Up** 메서드에 추가한 변경 내용을 되돌리는 데 사용 됩니다.
    >
    > 데이터베이스 마이그레이션은 데이터베이스를 업데이트할 때 모든 마이그레이션을 타임 스탬프 순서 대로 실행 하 고 마지막 업데이트 이후 사용 되지 않은 경우에만 실행 됩니다. (\_MigrationHistory 테이블은 적용 된 마이그레이션을 추적 합니다.) 모든 마이그레이션의 **Up** 메서드가 호출 되 고 데이터베이스에 지정한 변경 내용을 적용 합니다. 이전 마이그레이션 단계로 돌아가려면 **Down** 메서드를 호출 하 여 변경 내용을 역순으로 다시 실행 합니다.
4. **패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. 아래 이미지에 표시 된 것 처럼 새 열을 **Triviaquestions** 테이블에 추가 하는 **Alter Table** SQL 문을 생성 한 **업데이트 데이터베이스** 명령의 출력입니다.

    ![열 추가 SQL 문 생성](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "열 추가 SQL 문 생성")

    *열 추가 SQL 문 생성*
6. **SQL Server 개체 탐색기**에서 dbo를 새로 고칩니다 **.** 새 **힌트** 열이 표시 되는지 확인 합니다.

    ![새 힌트 열 표시](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "새 힌트 열 표시")

    *새 힌트 열 표시*
7. **TriviaQuestion.cs** 편집기로 돌아가서 다음 코드 조각과 같이 *Hint* 속성에 **stringlength** 제약 조건을 추가 합니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. **패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. **패키지 관리자 콘솔**에서 다음 명령을 입력 한 다음 **enter**키를 누릅니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. **업데이트-데이터베이스** 명령의 출력은 아래 이미지에 나와 있는 것 처럼 **Triviaquestions** 테이블의 *힌트* 열 형식을 업데이트 하는 **Alter Table** SQL 문을 생성 했습니다.

    ![Alter column SQL 문이 생성 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Alter column SQL 문이 생성 되었습니다.")

    *Alter column SQL 문이 생성 되었습니다.*
11. **SQL Server 개체 탐색기**에서 dbo를 새로 고칩니다 **. TriviaQuestions** 테이블에서 **힌트** 열 형식이 **nvarchar (150)** 인지 확인 합니다.

    ![새 제약 조건 표시](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "새 제약 조건 표시")

    *새 제약 조건 표시*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>연습 2: 스테이징에 웹 앱 배포

**Azure App Service에서 Web Apps** 를 사용 하 여 준비 된 게시를 수행할 수 있습니다. 스테이징 된 게시를 통해 각 기본 프로덕션 사이트에 대 한 스테이징 사이트 슬롯을 만들고 중단 시간 없이 이러한 슬롯을 교환할 수 있습니다. 이는 공용으로 릴리스하기 전에 변경 내용의 유효성을 검사 하 고, 사이트 콘텐츠를 증분 방식으로 통합 하 고, 변경 내용이 예상 대로 작동 하지 않는 경우 롤백하는 데 매우 유용 합니다.

이 연습에서는 Git 소스 제어를 사용 하 여 웹 앱의 스테이징 환경에 **Geek of 퀴즈** 응용 프로그램을 배포 합니다. 이렇게 하려면 웹 앱을 만들고, 관리 포털에서 필수 구성 요소를 프로 비전 하 고, **Git** 리포지토리를 구성 하 고, 로컬 컴퓨터에서 스테이징 슬롯으로 응용 프로그램 소스 코드를 푸시합니다. 또한 이전 연습에서 만든 **Code First 마이그레이션** 를 사용 하 여 프로덕션 데이터베이스를 업데이트 합니다. 그런 다음이 테스트 환경에서 응용 프로그램을 실행 하 여 해당 작업을 확인 합니다. 기대에 따라 작동 하는 것이 만족 스 러 우면 응용 프로그램을 프로덕션 환경으로 승격 시킵니다.

> [!NOTE]
> 스테이징 된 게시를 사용 하도록 설정 하려면 웹 앱이 **표준 모드**여야 합니다. 웹 앱을 표준 모드로 변경 하는 경우 추가 요금이 발생 합니다. 가격 책정에 대 한 자세한 내용은 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조 하세요.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>작업 1-Azure App Service에서 웹 앱 만들기

이 작업에서는 관리 포털에서 **Azure App Service** 웹 앱을 만듭니다. 또한 응용 프로그램 데이터를 유지 하 고 소스 제어를 위해 로컬 Git 리포지토리를 구성 하도록 **SQL Database** 를 구성 합니다.

1. [Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 여 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.

    ![Azure 관리 포털에 로그인 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Azure 관리 포털에 로그인 합니다.*
2. 페이지 아래쪽의 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 앱 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "새 웹 앱 만들기")

    *새 웹 앱 만들기*
3. **계산**, **웹 사이트** , **사용자 지정 만들기**를 차례로 클릭 합니다.

    ![사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기")

    *사용자 지정 만들기를 사용 하 여 새 웹 앱 만들기*
4. **새 웹 사이트-사용자 지정 만들기** 대화 상자에서 사용 가능한 **URL** (예: *geek of*)을 제공 하 고, **지역** 드롭다운 목록에서 위치를 선택 하 고, **데이터베이스** 드롭다운 목록에서 **새 SQL 데이터베이스 만들기** 를 선택 합니다. 마지막으로 **소스 제어에서 게시** 확인란을 선택 하 고 **다음**을 클릭 합니다.

    ![새 웹 앱 사용자 지정](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *새 웹 앱 사용자 지정*
5. 데이터베이스 설정에 대해 다음 정보를 지정 합니다.

   - **이름** 텍스트 상자에 데이터베이스 이름 (예: *geekquiz\_db*)을 입력 합니다.
   - 서버 **드롭다운** 목록에서 **새 SQL database 서버**를 선택 합니다. 또는 기존 서버를 선택할 수 있습니다.
   - **데이터베이스 사용자 이름** 및 **데이터베이스 암호** 상자에 SQL Database 서버에 대 한 관리자 사용자 이름 및 암호를 입력 합니다. 이미 만든 서버를 선택 하는 경우 암호를 입력 하 라는 메시지가 표시 됩니다.

     ![데이터베이스 설정 지정](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *데이터베이스 설정 지정*
6. **다음**을 클릭하여 계속합니다.
7. 사용할 원본 제어에 대 한 **로컬 Git 리포지토리** 를 선택 하 고 **다음**을 클릭 합니다.

    > [!NOTE]
    > 배포 자격 증명 (사용자 이름 및 암호)을 입력 하 라는 메시지가 표시 될 수 있습니다.

    ![Git 리포지토리 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Git 리포지토리 만들기*
8. 새 웹 앱이 만들어질 때까지 기다립니다.

    > [!NOTE]
    > 기본적으로 Azure는 *azurewebsites.net* 에서 도메인을 제공 하지만 azure 관리 포털을 사용 하 여 사용자 지정 도메인을 설정할 수도 있습니다. 그러나 특정 Azure App Service 모드를 사용 하는 경우에만 사용자 지정 도메인을 관리할 수 있습니다.
    >
    > Azure App Service는 무료, 공유, 기본, 표준 및 프리미엄 버전으로 제공 됩니다. 무료 및 공유 모드에서는 모든 웹 앱이 다중 테 넌 트 환경에서 실행 되며 CPU, 메모리 및 네트워크 사용량에 대 한 할당량이 있습니다. 사용 가능한 앱의 최대 수는 계획에 따라 다를 수 있습니다. 표준 모드에서는 표준 Azure 계산 리소스에 해당 하는 전용 가상 컴퓨터에서 실행 되는 앱을 선택 합니다. 웹 앱 모드 구성은 웹 앱의 **크기 조정** 메뉴에서 찾을 수 있습니다.
    >
    > ![Azure App Service 모드](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service 모드")
    >
    > **공유** 또는 **표준** 모드를 사용 하는 경우에는 앱의 **구성** 메뉴로 이동 하 고 *도메인 이름*아래에서 도메인 **관리** 를 클릭 하 여 웹 앱에 대 한 사용자 지정 도메인을 관리할 수 있습니다.
    >
    > ![도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "도메인 관리")
    >
    > ![사용자 지정 도메인 관리](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "사용자 지정 도메인 관리")
9. 웹 앱을 만든 후 **URL** 열 아래의 링크를 클릭 하 여 새 웹 앱이 실행 중인지 확인 합니다.

    ![새 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *새 웹 앱으로 이동*

    ![웹 앱 실행 중](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *웹 앱 실행 중*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>작업 2-프로덕션 SQL Database 만들기

이 태스크에서는 **Entity Framework Code First 마이그레이션** 를 사용 하 여 이전 태스크에서 만든 **Azure SQL Database** 인스턴스를 대상으로 하는 데이터베이스를 만듭니다.

1. 관리 포털에서 이전 작업에서 만든 웹 앱으로 이동 하 여 **대시보드로**이동 합니다.
2. **대시보드** 페이지의 **빠른** 보기 섹션에서 **연결 문자열 보기** 링크를 클릭 합니다.

    ![연결 문자열 보기](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "연결 문자열 보기")

    *연결 문자열 보기*
3. **연결 문자열** 값을 복사 하 고 대화 상자를 닫습니다.

    ![Azure 관리 포털의 연결 문자열](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Azure 관리 포털의 연결 문자열")

    *Azure 관리 포털의 연결 문자열*
4. **Sql database** 를 클릭 하 여 AZURE에서 sql 데이터베이스의 목록을 확인 합니다.

    ![SQL Database 메뉴](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "SQL Database 메뉴")

    *SQL Database 메뉴*
5. 이전 태스크에서 만든 데이터베이스를 찾아 서버를 클릭 합니다.

    ![SQL Database 서버](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "SQL Database 서버")

    *SQL Database 서버*
6. 서버의 **빠른 시작** 페이지에서 **구성**을 클릭 합니다.

    ![메뉴 구성](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "메뉴 구성")

    *메뉴 구성*
7. 허용 된 ip **주소** 섹션에서 **허용 된 Ip 주소에 추가** 링크를 클릭 하 여 ip가 SQL Database 서버에 연결할 수 있도록 합니다.

    ![허용 되는 IP 주소](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "허용된 IP 주소")

    *허용 되는 IP 주소*
8. 페이지 아래쪽에서 **저장** 을 클릭하여 단계를 완료합니다.
9. Visual Studio로 다시 전환 합니다.
10. **패키지 관리자 콘솔**에서 다음 명령을 실행 하 여 *[사용자의 연결 문자열]* 자리 표시자를 Azure에서 복사한 연결 문자열로 바꿉니다.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Windows Azure SQL Database를 대상으로 데이터베이스 업데이트](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Windows Azure SQL Database를 대상으로 데이터베이스 업데이트")

    *데이터베이스 대상 지정 Azure SQL Database 업데이트*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>작업 3-Git를 사용 하 여 스테이징에 Geek of 퀴즈 배포

이 태스크에서는 웹 앱에서 준비 된 게시를 사용 하도록 설정 합니다. 그런 다음 Git를 사용 하 여 로컬 컴퓨터에서 웹 앱의 스테이징 환경으로 Geek of 퀴즈 응용 프로그램을 직접 게시 합니다.

1. 포털로 돌아가서 **이름** 열 아래에 있는 웹 앱의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 앱 관리 페이지 열기](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *웹 앱 관리 페이지 열기*
2. **크기 조정** 페이지로 이동 합니다. **일반** 섹션에서 구성에 대해 **표준** 을 선택 하 고 명령 모음에서 **저장** 을 클릭 합니다.

    > [!NOTE]
    > 현재 지역 및 구독의 모든 웹 앱을 **표준** 모드로 실행 하려면 **사이트 선택** 구성에서 **모두 선택** 확인란을 선택 된 상태로 둡니다. 그렇지 않은 경우 **모두 선택** 확인란의 선택을 취소 합니다.

    ![웹 앱을 표준 모드로 업그레이드](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "웹 앱을 표준 모드로 업그레이드")

    *웹 앱을 표준 모드로 업그레이드*
3. **예** 를 클릭 하 여 변경 내용을 확인 합니다.

    ![표준 모드로 변경 확인](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "웹 앱 모드 변경 계속")

    *표준 모드로 변경 확인*
4. **대시보드** 페이지로 이동 하 고 **빠른** 보기 섹션에서 **준비 된 게시 사용** 을 클릭 합니다.

    ![준비 된 게시 사용](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "준비 된 게시 사용")

    *준비 된 게시 사용*
5. **예** 를 클릭 하 여 준비 된 게시를 사용 하도록 설정 합니다.

    ![스테이징 된 게시 확인](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "준비 된 게시를 사용 하려면 예를 클릭 합니다.")

    *스테이징 된 게시 확인*
6. 웹 앱 목록에서 웹 앱 이름의 왼쪽 표시를 확장 하 여 준비 사이트 슬롯을 표시 합니다. 웹 앱의 이름 뒤에 ***(준비)*** 가 있습니다. 준비 사이트를 클릭 하 여 관리 페이지로 이동 합니다.

    ![스테이징 웹 앱으로 이동](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "스테이징 웹 앱으로 이동")

    *준비 앱으로 이동*
7. 관리 페이지는 다른 웹 앱의 관리 페이지와 같습니다. **배포** 페이지로 이동 하 여 **Git URL** 값을 복사 합니다. 이 연습에서는 나중에 사용 합니다.

    ![Git URL 값 복사](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Git URL 값 복사*
8. 새 **Git Bash** 콘솔을 열고 다음 명령을 실행 합니다. 이 랩의 **Source\Ex1-DeployingWebSiteToStaging\Begin** 폴더에 있는 **GeekQuiz** 솔루션의 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Git 초기화 및 첫 번째 커밋](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Git 초기화 및 첫 번째 커밋*
9. 다음 명령을 실행 하 여 웹 앱을 원격 **Git** 리포지토리에 푸시합니다. 자리 표시자를 관리 포털에서 가져온 URL로 바꿉니다. 배포 암호를 입력 하 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Windows Azure에 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Azure에 푸시*

    > [!NOTE]
    > 웹 앱의 FTP 호스트 또는 GIT 리포지토리에 콘텐츠를 배포 하는 경우 웹 앱의 **빠른 시작** 또는 **대시보드** 관리 페이지에서 만든 **배포 자격 증명** 을 사용 하 여 인증 해야 합니다. 배포 자격 증명을 모르는 경우 관리 포털을 사용 하 여 쉽게 다시 설정할 수 있습니다. 웹 앱 **대시보드** 페이지를 열고 **배포 자격 증명 다시 설정** 링크를 클릭 합니다. 새 암호를 입력 하 고 **확인을**클릭 합니다. 배포 자격 증명은 구독과 연결 된 모든 웹 앱에서 사용할 수 있습니다.
10. 웹 앱이 Azure로 푸시 되었는지 확인 하려면 관리 포털로 돌아가서 **Websites**를 클릭 합니다.
11. 웹 앱을 찾고 항목을 확장 하 여 스테이징 사이트 슬롯을 표시 합니다. 해당 **이름을** 클릭 하 여 관리 페이지로 이동 합니다.
12. 배포 **를 클릭 하** 여 **배포 기록을**확인 합니다. *&quot;초기 커밋&quot;* 를 사용 하 여 **활성 배포가** 있는지 확인 합니다.

    ![활성 배포](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *활성 배포*
13. 마지막으로 명령 모음에서 **찾아보기** 를 클릭 하 여 웹 앱으로 이동 합니다.

    ![웹 앱 찾아보기](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *웹 앱 찾아보기*
14. 응용 프로그램이 성공적으로 배포 되 면 Geek of 퀴즈 로그인 페이지가 표시 됩니다.

    > [!NOTE]
    > 배포 된 응용 프로그램의 주소 URL에는 웹 앱의 이름, *-스테이징*이 포함 됩니다.

    ![스테이징 환경에서 실행 되는 응용 프로그램](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *스테이징 환경에서 실행 되는 응용 프로그램*
15. 응용 프로그램을 탐색 하려는 경우 **등록** 을 클릭 하 여 새 사용자를 등록 합니다. 사용자 이름, 전자 메일 주소 및 암호를 입력 하 여 계정 세부 정보를 완료 합니다. 그런 다음 응용 프로그램은 퀴즈의 첫 번째 질문을 표시 합니다. 몇 가지 질문에 답변 하 여 예상 대로 작동 하는지 확인 합니다.

    ![응용 프로그램을 사용할 준비가 되었습니다.](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *응용 프로그램을 사용할 준비가 되었습니다.*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>작업 4 – 웹 앱을 프로덕션으로 승격

이제 스테이징 환경에서 웹 앱이 올바르게 작동 하는지 확인 했으므로 프로덕션으로 승격할 준비가 되었습니다. 이 작업에서는 스테이징 사이트 슬롯을 프로덕션 사이트 슬롯으로 바꿉니다.

1. 관리 포털로 돌아가서 준비 사이트 슬롯을 선택 합니다. 명령 모음에서 **교환** 을 클릭 합니다.

    ![프로덕션으로 교환](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *프로덕션으로 교환*
2. 확인 대화 상자에서 **예** 를 클릭 하 여 교환 작업을 진행 합니다. Azure는 프로덕션 사이트의 콘텐츠를 스테이징 사이트의 콘텐츠로 즉시 바꿉니다.

    > [!NOTE]
    > 준비 버전의 일부 설정은 자동으로 프로덕션 버전 (예: 연결 문자열 재정의, 처리기 매핑 등)으로 복사 되지만 다른 설정은 변경 되지 않습니다 (예: DNS 끝점, SSL 바인딩 등).

    ![교환 작업 확인](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *교환 작업 확인*
3. 교환이 완료 되 면 프로덕션 슬롯을 선택 하 고 명령 모음에서 **찾아보기** 를 클릭 하 여 프로덕션 사이트를 엽니다. 주소 표시줄에서 URL을 확인 합니다.

    > [!NOTE]
    > 캐시를 지우려면 브라우저를 새로 고쳐야 할 수도 있습니다. Internet Explorer에서 **ctrl + R**을 눌러이 작업을 수행할 수 있습니다.

    ![프로덕션 환경에서 실행 되는 웹 앱](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. **Gitbash** 콘솔에서 프로덕션 슬롯을 대상으로 하는 로컬 Git 리포지토리의 원격 URL을 업데이트 합니다. 이렇게 하려면 자리 표시자를 배포 사용자 이름으로 바꾸고 웹 앱의 이름을 바꾸는 다음 명령을 실행 합니다.

    > [!NOTE]
    > 다음 연습에서는 랩의 단순성만 준비 하는 대신 프로덕션 사이트에 변경 내용을 푸시합니다. 실제 시나리오에서는 프로덕션으로 승격 하기 전에 스테이징 환경의 변경 내용을 확인 하는 것이 좋습니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>연습 3: 프로덕션 환경에서 배포 롤백 수행

예를 들어 **무료** 또는 **공유** 모드로 작업 하는 경우 스테이징 및 프로덕션 사이에서 핫 교환을 수행할 준비 슬롯이 없는 시나리오가 있습니다. 이러한 시나리오에서는 프로덕션 환경에 배포 하기 전에 로컬로 또는 원격 사이트에서 테스트 환경에서 응용 프로그램을 테스트 해야 합니다. 그러나 프로덕션 사이트에서 테스트 단계 중에 발견 되지 않은 문제가 발생할 수 있습니다. 이 경우에는 최대한 빨리 이전 및 안정적인 응용 프로그램 버전으로 쉽게 전환 하는 메커니즘을 고려해 야 합니다.

**Azure App Service**원본 제어에서 연속 배포를 수행 하면 관리 포털에서 제공 되는 **재배포** 작업을 통해이 작업을 수행할 수 있습니다. Azure는 리포지토리에 푸시되는 커밋에 연결 된 배포를 추적 하 고, 언제 든 지 이전 배포 중 하나를 사용 하 여 응용 프로그램을 다시 배포 하는 옵션을 제공 합니다.

이 연습에서는 의도적으로 *버그*를 삽입 하는 **geek of 퀴즈** 응용 프로그램의 코드를 변경 합니다. 응용 프로그램을 프로덕션 환경에 배포 하 여 오류를 확인 한 다음 다시 배포 기능을 활용 하 여 이전 상태로 돌아갈 것입니다.

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>작업 1 – Geek of 퀴즈 응용 프로그램 업데이트

이 태스크에서는 코드의 작은 부분을 리팩터링 **하 여 데이터베이스** 에서 선택한 퀴즈 옵션을 검색 하는 논리의 일부를 새 메서드로 추출 합니다.

1. 이전 연습에서 **GeekQuiz** 솔루션을 사용 하 여 Visual Studio 인스턴스로 전환 합니다.
2. **솔루션 탐색기**의 **Controllers** 폴더에서 **TriviaController.cs** 파일을 엽니다.
3. **StoreAsync** 메서드를 찾고 다음 그림에 강조 표시 된 코드를 선택 합니다.

    ![코드 선택](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *코드 선택*
4. 선택한 코드를 마우스 오른쪽 단추로 클릭 하 고 **리팩터링** 메뉴를 확장 한 다음 **메서드 추출 ...** 을 선택 합니다.

    ![새 메서드로 코드 추출](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *추출 방법 선택*
5. **메서드 추출** 대화 상자에서 새 메서드의 이름을 *MatchesOption* 로, **확인**을 클릭 합니다.

    ![메서드 이름 지정](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *추출 된 메서드의 이름 지정*
6. 그런 다음 선택한 코드는 **MatchesOption** 메서드로 추출 됩니다. 결과 코드는 다음 코드 조각에 표시 됩니다.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>작업 2 – Geek of 퀴즈 응용 프로그램 재배포

이제 이전 작업에서 변경한 내용을 리포지토리에 푸시하여 프로덕션 환경에 대 한 새 배포를 트리거합니다. 그런 다음 Internet Explorer에서 제공 하는 **F12 개발 도구** 를 사용 하 여 문제를 해결 한 후 Azure 관리 포털에서 이전 배포에 대 한 롤백을 수행 합니다.

1. 새 **Git Bash** 콘솔을 열어 Azure App Service에 업데이트 된 응용 프로그램을 배포 합니다.
2. 다음 명령을 실행 하 여 변경 내용을 Azure에 푸시합니다. **GeekQuiz** 솔루션에 대 한 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다. 배포 암호를 입력 하 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Azure에 리팩터링된 코드 푸시](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *Azure에 리팩터링된 코드 푸시*
3. Internet Explorer를 열고 웹 앱으로 이동 합니다 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든 자격 증명을 사용 하 여 로그인 합니다.
4. **F12** 키를 눌러 개발 도구를 시작 하 고 **네트워크** 탭을 선택한 후 **재생** 단추를 클릭 하 여 기록을 시작 합니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "네트워크 기록 시작")

    *네트워크 기록 시작*
5. 퀴즈의 옵션을 선택 합니다. 아무것도 발생 하지 않습니다.
6. **F12** 창에서 HTTP 요청 POST에 해당 하는 항목은 http **500** 결과를 표시 합니다.

    ![HTTP 500 오류](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *HTTP 500 오류*
7. **콘솔** 탭을 선택 합니다. 오류의 세부 정보를 사용 하 여 오류가 기록 됩니다.

    ![기록 오류](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *기록 오류*
8. 오류의 세부 정보 부분을 찾습니다. 이 오류는 이전 단계에서 커밋한 코드 리팩터링에 의해 발생 합니다.

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`입니다.
9. 브라우저를 닫지 마세요.
10. 새 브라우저 인스턴스에서 [Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 고 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.
11. **웹 사이트** 를 선택 하 고 연습 2에서 만든 웹 앱을 클릭 합니다.
12. **배포** 페이지로 이동 합니다. 수행 된 모든 커밋이 배포 기록에 나열 되는지 확인 합니다.

    ![기존 배포 목록](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *기존 배포 목록*
13. 이전 커밋을 선택 하 고 명령 모음에서 다시 **배포** 를 클릭 합니다.

    ![이전 커밋 다시 배포](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *이전 커밋 다시 배포*
14. 확인하라는 메시지가 나타나면 **예**를 클릭합니다.

    ![재배포 확인](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. 배포가 완료 되 면 웹 앱을 사용 하 여 브라우저 인스턴스로 다시 전환 하 고 **ctrl + F5**를 누릅니다.
16. 옵션 중 하나를 클릭 합니다. 이제 플립 애니메이션이 발생 하 고 결과 (*올바른/잘못*됨)가 표시 됩니다.
17. 필드 **Git Bash** 콘솔로 전환 하 고 다음 명령을 실행 하 여 이전 커밋으로 되돌립니다.

    > [!NOTE]
    > 이러한 명령은 잘못 된 커밋에서 만든 Git 리포지토리의 모든 변경 내용을 취소 하는 새 커밋을 만듭니다. 그러면 Azure에서 새로운 커밋을 사용 하 여 응용 프로그램을 다시 배포 합니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>연습 4: Azure Storage 사용 하 여 크기 조정

**Blob** 은 비디오, 오디오 및 이미지와 같은 대량의 구조화 되지 않은 텍스트 또는 이진 데이터를 저장 하는 가장 간단한 방법입니다. 응용 프로그램의 정적 콘텐츠를 저장소로 이동 하면 이미지 또는 문서를 브라우저에 직접 제공 하 여 응용 프로그램을 확장할 수 있습니다.

이 연습에서는 응용 프로그램의 정적 콘텐츠를 Blob 컨테이너로 이동 합니다. 그런 다음 콘텐츠를 Blob 컨테이너로 리디렉션하도록 **web.config** 에 **ASP.NET URL 재작성 규칙** 을 추가 하도록 응용 프로그램을 구성 합니다.

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>작업 1-Azure Storage 계정 만들기

이 작업에서는 관리 포털을 사용 하 여 새 저장소 계정을 만드는 방법을 알아봅니다.

1. [Azure 관리 포털로](https://manage.windowsazure.com) 이동 하 고 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.
2. **새로 만들기 | Data Services | 저장소 |** 새 저장소 계정 만들기를 시작 하기 위한 빠른 생성 계정에 고유한 이름을 입력 하 고 목록에서 **지역을** 선택 합니다. **저장소 계정 만들기** 를 클릭 하 여 계속 합니다.

    ![새 저장소 계정 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "새 저장소 계정 만들기")

    *새 저장소 계정 만들기*
3. **저장소** 섹션에서 다음 단계를 계속 하기 위해 새 저장소 계정의 상태가 *온라인* 으로 변경 될 때까지 기다립니다.

    ![저장소 계정이 만들어짐](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "저장소 계정이 만들어짐")

    *저장소 계정이 만들어짐*
4. 저장소 계정 이름을 클릭 한 다음 페이지 위쪽의 **대시보드** 링크를 클릭 합니다. **대시보드** 페이지는 응용 프로그램 내에서 사용할 수 있는 서비스 끝점과 계정 상태에 대 한 정보를 제공 합니다.

    ![저장소 계정 대시보드 표시](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "저장소 계정 대시보드 표시")

    *저장소 계정 대시보드 표시*
5. 탐색 모음에서 **액세스 키 관리** 단추를 클릭 합니다.

    ![액세스 키 관리 단추](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "액세스 키 관리 단추")

    *액세스 키 관리 단추*
6. **액세스 키 관리** 대화 상자에서 **저장소 계정 이름** 및 **기본 액세스 키** 를 다음 연습에서 필요에 따라 복사 합니다. 그런 다음 대화 상자를 닫습니다.

    ![액세스 키 관리 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "액세스 키 관리 대화 상자")

    *액세스 키 관리 대화 상자*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>작업 2-Azure Blob Storage에 자산 업로드

이 작업에서는 Visual Studio의 서버 탐색기 창을 사용 하 여 저장소 계정에 연결 합니다. 그런 다음 blob 컨테이너를 만들고 Geek of 퀴즈 로고가 포함 된 파일을 컨테이너에 업로드 합니다.

1. 이전 연습에서 **GeekQuiz** 솔루션을 사용 하 여 Visual Studio 인스턴스로 전환 합니다.
2. 메뉴 모음에서 **보기** 를 선택 하 고 **서버 탐색기**를 클릭 합니다.
3. **서버 탐색기**에서 **azure** 노드를 마우스 오른쪽 단추로 클릭 하 고 **azure에 연결 ...을**선택 합니다. 구독과 연결 된 Microsoft 계정를 사용 하 여 로그인 합니다.

    ![Windows Azure에 연결](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Azure에 연결*
4. **Azure** 노드를 확장 하 고 **저장소** 를 마우스 오른쪽 단추로 클릭 한 다음 **외부 저장소 연결**...을 선택 합니다.
5. **새 저장소 계정 추가** 대화 상자에서 이전 작업에서 받은 **계정 이름** 및 **계정 키** 를 입력 하 고 **확인**을 클릭 합니다.

    ![새 저장소 계정 추가 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *새 저장소 계정 추가 대화 상자*
6. 저장소 계정이 **저장소** 노드 아래에 나타나야 합니다. 저장소 계정을 확장 하 고 **blob** 을 마우스 오른쪽 단추로 클릭 한 다음 **blob 컨테이너 만들기**...를 선택 합니다.

    ![Blob 컨테이너 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Blob 컨테이너 만들기")

    *Blob 컨테이너 만들기*
7. **Blob 컨테이너 만들기** 대화 상자에서 blob 컨테이너의 이름을 입력 하 고 **확인**을 클릭 합니다.

    ![Blob 컨테이너 만들기 대화 상자](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Blob 컨테이너 만들기 대화 상자")

    *Blob 컨테이너 만들기 대화 상자*
8. 새 blob 컨테이너를 **blob** 노드에 추가 해야 합니다. 컨테이너의 액세스 권한을 변경 하 여 컨테이너를 공용으로 만듭니다. 이렇게 하려면 **images** 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

    ![images 컨테이너 속성](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "images 컨테이너 속성")

    *Images 컨테이너 속성*
9. **속성** 창에서 **컨테이너**에 대 한 **공용 읽기 권한을** 설정 합니다.

    ![공용 읽기 액세스 속성 변경](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "공용 읽기 액세스 속성 변경")

    *공용 읽기 액세스 속성 변경*
10. 공용 액세스 속성을 변경 하 시겠습니까? 라는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![Microsoft Visual Studio 경고](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Microsoft Visual Studio 경고")

    *Microsoft Visual Studio 경고*
11. **서버 탐색기**에서 **images** blob 컨테이너를 마우스 오른쪽 단추로 클릭 하 고 **blob 컨테이너 보기**를 선택 합니다.

    ![Blob 컨테이너 보기](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Blob 컨테이너 보기")

    *Blob 컨테이너 보기*
12. 이미지 컨테이너가 새 창에서 열리고 항목이 없는 범례가 표시 되어야 합니다. **업로드** 아이콘을 클릭 하 여 blob 컨테이너에 파일을 업로드 합니다.

    ![항목이 없는 Images 컨테이너](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "항목이 없는 Images 컨테이너")

    *항목이 없는 Images 컨테이너*
13. **Blob 업로드** 대화 상자에서 랩의 **자산** 폴더로 이동 합니다. **Logo-big** 파일을 선택 하 고 **열기**를 클릭 합니다.
14. 파일이 업로드 될 때까지 기다립니다. 업로드가 완료 되 면 파일이 images 컨테이너에 나열 됩니다. 파일 항목을 마우스 오른쪽 단추로 클릭 하 고 **URL 복사**를 선택 합니다.

    ![Blob URL 복사](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Blob 파일 URL 복사")

    *Blob URL 복사*
15. Internet Explorer를 열고 URL을 붙여넣습니다. 다음 이미지는 브라우저에 표시 되어야 합니다.

    ![Windows Blob Storage의 logo-big 이미지](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "저장소의 logo-big 이미지")

    *Azure Blob Storage logo-big 이미지*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>작업 3 – Azure Blob Storage의 정적 콘텐츠를 사용 하도록 솔루션 업데이트

이 작업에서는 **web.config 파일에** ASP.NET URL 재작성 규칙을 추가 하 여 Azure Blob Storage (웹 앱에 있는 이미지 대신)에 업로드 된 이미지를 사용 하도록 **GeekQuiz** 솔루션을 구성 합니다.

1. Visual Studio에서 **GeekQuiz** 프로젝트 내의 **web.config 파일을** 열고 **&lt;system.webserver&gt;** 요소를 찾습니다.
2. 다음 코드를 추가 하 여 URL 다시 쓰기 규칙을 추가 하 고, 자리 표시자를 저장소 계정 이름으로 업데이트 합니다.

    (코드 조각- *WebSitesInProduction-Ex4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > URL 다시 쓰기는 들어오는 웹 요청을 가로채 고 요청을 다른 리소스로 리디렉션하는 프로세스입니다. URL 다시 쓰기 규칙은 요청을 리디렉션해야 할 때 다시 작성 엔진에 지시 하 고,이를 리디렉션해야 하는 위치를 지정 합니다. 재작성 규칙은 요청 된 URL에서 찾을 패턴 (일반적으로 정규식 사용)과 패턴을 대체할 문자열 (있는 경우)의 두 문자열로 구성 됩니다. 자세한 내용은 [ASP.NET에서 URL 다시 작성](https://msdn.microsoft.com/library/ms972974.aspx)을 참조 하세요.
3. **Ctrl + S** 를 눌러 변경 내용을 저장 합니다.
4. 새 **Git Bash** 콘솔을 열어 Azure App Service에 업데이트 된 응용 프로그램을 배포 합니다.
5. 다음 명령을 실행 하 여 변경 내용을 Azure에 푸시합니다. **GeekQuiz** 솔루션에 대 한 경로를 사용 하 여 *[응용 프로그램 경로]* 자리 표시자를 업데이트 합니다. 배포 암호를 입력 하 라는 메시지가 표시 됩니다.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Azure에 업데이트 배포](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Azure에 업데이트 배포*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>작업 4 – 확인

이 작업에서는 **Internet Explorer** 를 사용 하 여 **geek of 퀴즈** 응용 프로그램을 검색 하 고 이미지에 대 한 URL 재작성 규칙이 작동 하는지 확인 하 고 **Azure Blob Storage**에서 호스트 되는 이미지로 리디렉션됩니다.

1. Internet Explorer를 열고 웹 앱으로 이동 합니다 (예: `http://<your-web-site>.azurewebsites.net`). 이전에 만든 자격 증명을 사용 하 여 로그인 합니다.

    ![이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시")

    *이미지를 사용 하 여 Geek of 퀴즈 웹 앱 표시*
2. **F12** 키를 눌러 개발 도구를 시작 하 고 **네트워크** 탭을 선택한 후 기록을 시작 합니다.

    ![네트워크 기록 시작](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "네트워크 기록 시작")

    *네트워크 기록 시작*
3. **Ctrl +** f 5를 눌러 웹 페이지를 새로 고칩니다.
4. 페이지가 로드 되 면 http **301** 결과 (리디렉션)를 사용 하는 **/img/logo-big.png** URL에 대 한 http 요청 및 http **200** 결과와 `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url에 대 한 다른 요청이 표시 됩니다.

    ![URL 리디렉션 확인](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "개발자 도구에서 리디렉션 표시")

    *URL 리디렉션 확인*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>연습 5: Web Apps에 자동 크기 조정 사용

> [!NOTE]
> 이 연습은 **Visual Studio 2013 Ultimate Edition**에서만 사용할 수 있는 웹 로드 &amp; 성능 테스트에 대 한 지원이 필요 하기 때문에 선택 사항입니다. 특정 Visual Studio 2013 기능에 대 한 자세한 내용은 [여기](https://www.microsoft.com/visualstudio/eng/products/compare)에서 버전을 비교 합니다.

**Azure App Service Web Apps** 는 **표준 모드**에서 실행 되는 웹 앱에 대 한 자동 크기 조정 기능을 제공 합니다. 자동 크기 조정을 통해 Azure는 부하에 따라 웹 앱의 인스턴스 수를 자동으로 조정할 수 있습니다. 자동 크기 조정을 사용 하는 경우 Azure는 5 분 마다 웹 앱의 CPU를 확인 하 고 해당 시점에 필요에 따라 인스턴스를 추가 합니다. CPU 사용량이 낮은 경우 Azure는 웹 앱의 성능이 저하 되지 않도록 2 시간 마다 한 번씩 인스턴스를 제거 합니다.

이 연습에서는 **Geek of 퀴즈** 웹 앱에 대 한 **자동 크기 조정** 기능을 구성 하는 데 필요한 단계를 진행 합니다. 응용 프로그램에서 인스턴스 업그레이드를 트리거하기 위한 충분 한 CPU 부하를 생성 하기 위해 Visual Studio 부하 테스트를 실행 하 여이 기능을 확인 합니다.

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>작업 1-CPU 메트릭에 따라 자동 크기 조정 구성

이 작업에서는 Azure 관리 포털을 사용 하 여 연습 2에서 만든 웹 앱에 대 한 자동 크기 조정 기능을 사용 하도록 설정 합니다.

1. [Azure 관리 포털](https://manage.windowsazure.com/)에서 **웹 사이트** 를 선택 하 고 연습 2에서 만든 웹 앱을 클릭 합니다.
2. **크기 조정** 페이지로 이동 합니다. **용량** 섹션에서 **메트릭 별 크기 조정** 구성에 대해 **CPU** 를 선택 합니다.

    > [!NOTE]
    > CPU를 기준으로 크기를 조정 하는 경우 Azure는 CPU 사용량이 변경 될 경우 앱이 사용 하는 인스턴스 수를 동적으로 조정 합니다.

    ![CPU 별로 크기를 조정 하도록 선택](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "자동 크기 조정에 대 한 CPU 메트릭 선택")

    *CPU 별로 크기를 조정 하도록 선택*
3. **대상 CPU** 구성을 **20**-**40** %로 변경 합니다.

    > [!NOTE]
    > 이 범위는 웹 앱에 대 한 평균 CPU 사용량을 나타냅니다. Azure에서 인스턴스를 추가 하거나 제거 하 여 웹 앱을이 범위에 보관 합니다. 크기 조정에 사용 되는 최소 및 최대 인스턴스 수는 **인스턴스 수** 구성에 지정 됩니다. Azure는 이러한 제한을 초과 하거나 초과 하지 않습니다.
    >
    > 기본 **대상 CPU** 값은이 랩의 목적 으로만 수정 됩니다. 작은 값을 사용 하 여 CPU 범위를 구성 하면 응용 프로그램에 보통 부하가 배치 될 때 자동 크기 조정을 트리거할 가능성이 높아집니다.

    ![대상 CPU를 20 ~ 40% 사이로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "대상 CPU를 20 ~ 40% 사이로 변경")

    *대상 CPU를 20 ~ 40% 사이로 변경*
4. 명령 모음에서 **저장** 을 클릭 하 여 변경 내용을 저장 합니다.

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>작업 2-Visual Studio를 사용 하 여 부하 테스트

**자동 크기 조정을** 구성 했으므로 웹 앱에서 일부 CPU 로드를 생성 하기 위해 Visual Studio에서 **웹 성능 및 부하 테스트 프로젝트** 를 만듭니다.

1. **Visual Studio Ultimate 2013** 열고 [파일]을 선택 합니다. **| 새로 만들기 | 프로젝트** ... 새 솔루션을 시작 합니다.

    ![새 프로젝트 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "새 프로젝트 만들기")

    *새 프로젝트 만들기*
2. **새 프로젝트** 대화 상자의 시각적 개체  **C# 에서 웹 성능 및 부하 테스트 프로젝트를 선택 합니다. 테스트** 탭. **.NET Framework 4.5** 가 선택 되어 있는지 확인 하 고, 프로젝트 이름을 *WebAndLoadTestProject*로 지정 하 고, **위치** 를 선택 하 고, **확인**을 클릭 합니다.

    ![새 웹 및 부하 테스트 프로젝트 만들기](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "새 웹 및 부하 테스트 프로젝트 만들기")

    *새 웹 및 부하 테스트 프로젝트 만들기*
3. **Webtest1.webtest** 에서 **Webtest1.webtest** 노드를 마우스 오른쪽 단추로 클릭 하 고 **요청 추가**를 클릭 합니다.

    ![Webtest1.webtest에 요청 추가](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Webtest1.webtest에 요청 추가")

    *Webtest1.webtest에 요청 추가*
4. 새 요청 노드의 **속성** 창에서 **url** 속성을 업데이트 하 여 웹 앱의 url (예: *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* )을 가리킵니다.

    ![Url 속성 변경](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Url 속성 변경")

    *Url 속성 변경*
5. **Webtest1.webtest** 창에서 **webtest1.webtest** 를 마우스 오른쪽 단추로 클릭 하 고 **루프 추가**...를 클릭 합니다.

    ![Webtest1.webtest에 루프 추가](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Webtest1.webtest에 루프 추가")

    *Webtest1.webtest에 루프 추가*
6. **루프에 조건부 규칙 및 항목 추가** 대화 상자에서 **for 루프** 규칙을 선택 하 고 다음 속성을 수정 합니다.

   1. **종료 값:** 1000
   2. **컨텍스트 매개 변수 이름:** 반복
   3. **증가값:** 1

      ![For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.")

      *For 루프 규칙을 선택 하 고 속성을 업데이트 합니다.*
7. **루프의 항목** 섹션에서 이전에 만든 요청을 루프의 첫 번째 항목과 마지막 항목으로 선택 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![루프의 첫 번째 및 마지막 항목 선택](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "루프의 첫 번째 및 마지막 항목 선택")

    *루프의 첫 번째 및 마지막 항목 선택*
8. **솔루션 탐색기**에서 **WebAndLoadTestProject** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가** 메뉴를 확장 한 다음 **부하 테스트**...를 선택 합니다.

    ![WebAndLoadTestProject 프로젝트에 부하 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "WebAndLoadTestProject 프로젝트에 부하 테스트 추가")

    *WebAndLoadTestProject 프로젝트에 부하 테스트 추가*
9. **새 부하 테스트 마법사** 대화 상자에서 **다음**을 클릭 합니다.

    ![새 부하 테스트 마법사](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "새 부하 테스트 마법사")

    *새 부하 테스트 마법사*
10. **시나리오** 페이지에서 **인지 시간 사용 안 함** 을 선택 하 고 **다음**을 클릭 합니다.

    ![인지 시간을 사용 하지 않도록 선택](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "인지 시간을 사용 하지 않도록 선택")

    *인지 시간을 사용 하지 않도록 선택*
11. **부하 패턴** 페이지에서 **상수 로드** 옵션이 선택 되어 있는지 확인 합니다. **사용자 수** 설정을 **250** 사용자로 변경 하 고 **다음**을 클릭 합니다.

    ![사용자 수를 250으로 변경](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "사용자 수를 250으로 변경")

    *사용자 수를 250으로 변경*
12. **테스트 조합 모델** 페이지에서 **순차적 테스트 순서를 기준으로** 을 선택 하 고 **다음**을 클릭 합니다.

    ![테스트 조합 모델 선택](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "테스트 조합 모델 선택")

    *테스트 조합 모델 선택*
13. **테스트 조합 모델** 페이지에서 **추가 ...** 를 클릭 하 여 테스트를 조합에 추가 합니다.

    ![테스트 조합에 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "테스트 조합에 테스트 추가")

    *테스트 조합에 테스트 추가*
14. **테스트 추가** 대화 상자에서 **webtest1.webtest** 를 두 번 클릭 하 여 **선택한 테스트** 목록에 테스트를 추가 합니다. 계속하려면 **확인** 을 클릭합니다.

    ![Webtest1.webtest 테스트 추가](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Webtest1.webtest 테스트 추가")

    *Webtest1.webtest 테스트 추가*
15. **테스트 조합** 페이지로 돌아가 **다음**을 클릭 합니다.

    ![테스트 조합 완료 페이지](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "테스트 조합 완료 페이지")

    *테스트 조합 완료 페이지*
16. **네트워크 조합** 페이지에서 **다음**을 클릭 합니다.

    ![네트워크 조합 페이지에서 다음을 클릭 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "네트워크 조합 페이지에서 다음을 클릭 합니다.")

    *네트워크 조합 페이지에서 다음을 클릭 합니다.*
17. **브라우저 조합** 페이지에서 **Internet Explorer 10.0** 을 브라우저 형식으로 선택 하 고 **다음**을 클릭 합니다.

    ![브라우저 유형 선택](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "브라우저 유형 선택")

    *브라우저 유형 선택*
18. **카운터 집합** 페이지에서 **다음**을 클릭 합니다.

    ![카운터 집합 페이지에서 다음을 클릭 합니다.](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "카운터 집합 페이지에서 다음을 클릭 합니다.")

    *카운터 집합 페이지에서 다음을 클릭 합니다.*
19. **실행 설정** 페이지에서 **부하 테스트 기간** 을 **5 분** 으로 설정 하 고 **마침**을 클릭 합니다.

    ![부하 테스트 지속 시간을 5 분으로 설정](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "부하 테스트 지속 시간을 5 분으로 설정")

    *부하 테스트 지속 시간을 5 분으로 설정*
20. **솔루션 탐색기**에서 **로컬. settings** 파일을 두 번 클릭 하 여 테스트 설정을 탐색 합니다. 기본적으로 Visual Studio는 로컬 컴퓨터를 사용 하 여 테스트를 실행 합니다.

    > [!NOTE]
    > 또는 **Azure Test Plans**를 사용 하 여 클라우드에서 부하 테스트를 실행 하도록 테스트 프로젝트를 구성할 수 있습니다. Azure Test Plans은 CPU 용량, 사용 가능한 메모리, 네트워크 대역폭 등의 로컬 환경 제약 조건을 방지 하 여 보다 현실적인 부하를 시뮬레이션 하는 클라우드 기반 부하 테스트 서비스를 제공 합니다. Azure Test Plans를 사용 하 여 부하 테스트를 실행 하는 방법에 대 한 자세한 내용은 [부하 테스트 시나리오](/azure/devops/test/load-test/overview?view=vsts)를 참조 하세요.

    ![테스트 설정](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>작업 3 – 자동 크기 조정 확인

이제 이전 작업에서 만든 부하 테스트를 실행 하 고 부하 상태에서 웹 앱이 작동 하는 방식을 확인 합니다.

1. **솔루션 탐색기**에서 **loadtest1.loadtest. loadtest** 를 두 번 클릭 하 여 부하 테스트를 엽니다.

    ![Loadtest1.loadtest. loadtest를 엽니다.](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Loadtest1.loadtest. loadtest를 엽니다.")

    *Loadtest1.loadtest. loadtest를 엽니다.*
2. **Loadtest1.loadtest loadtest** 창에서 도구 상자의 첫 번째 단추를 클릭 하 여 부하 테스트를 실행 합니다.

    ![부하 테스트 실행](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "부하 테스트 실행")

    *부하 테스트 실행*
3. 부하 테스트가 완료 될 때까지 기다립니다.

    > [!NOTE]
    > 부하 테스트는 웹 앱에 요청을 동시에 보내는 여러 사용자를 시뮬레이션 합니다. 테스트가 실행 중일 때 사용 가능한 카운터를 모니터링 하 여 부하 테스트 실행과 관련 된 오류, 경고 또는 기타 정보를 검색할 수 있습니다.

    ![부하 테스트 실행 중](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "부하 테스트가 완료 될 때까지 대기")

    *부하 테스트 실행 중*
4. 테스트가 완료 되 면 관리 포털로 돌아가서 웹 앱의 **크기 조정** 페이지로 이동 합니다. **용량** 섹션 아래에 새 인스턴스가 자동으로 배포 되었음을 나타내는 그래프가 표시 되어야 합니다.

    ![새 인스턴스가 자동으로 배포 됨](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *새 인스턴스가 자동으로 배포 됨*

    > [!NOTE]
    > 그래프에 변경 내용이 표시 되는 데 몇 분 정도 걸릴 수 있습니다. **CTRL + f5** 키를 눌러 페이지를 새로 고칩니다. 변경 내용이 표시 되지 않으면 다음을 시도할 수 있습니다.
    >
    > - 부하 테스트 기간 늘리기 (예: **10 분**)
    > - 웹 앱의 자동 크기 조정 구성에서 **대상 CPU** 범위의 최대값과 최 댓 값을 줄입니다.
    > - **Azure Test Plans**를 사용 하 여 클라우드에서 부하 테스트를 실행 합니다. 자세한 내용은 [여기](/azure/devops/test/load-test/index?view=vsts)를 참조하세요.

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서는 Azure에서 프로덕션 웹 앱에 응용 프로그램을 설치 하 고 배포 하는 방법을 알아보았습니다. 먼저 **Entity Framework Code First 마이그레이션**를 사용 하 여 데이터베이스를 검색 하 고 업데이트 한 다음 **Git** 를 사용 하 여 사이트의 새 버전을 배포 하 고 안정적인 최신 버전의 사이트로 롤백을 수행 합니다. 또한 저장소를 사용 하 여 앱을 확장 하 여 정적 콘텐츠를 Blob 컨테이너로 이동 하는 방법을 배웠습니다.
