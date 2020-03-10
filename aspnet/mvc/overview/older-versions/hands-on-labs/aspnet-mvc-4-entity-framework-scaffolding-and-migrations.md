---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 컨트롤러 메서드에 익숙하고 &quot;도우미, 폼 및 유효성 검사&quot; 실습 실습을 완료 한 경우 다음 사항을 알고 있어야 합니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484643"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 Entity Framework 스캐폴딩 및 마이그레이션

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 컨트롤러 메서드에 익숙하고 &quot;도우미, 폼 및 유효성 검사&quot; 실습 실습을 완료 한 경우 데이터 엔터티를 만들고, 업데이트 하 고, 나열 하 고, 제거 하는 대부분의 논리가 응용 프로그램 간에 반복 된다는 점을 알고 있어야 합니다. 모델에 조작할 클래스가 여러 개 있는 경우 각 엔터티 작업 뿐만 아니라 각 뷰에 대해 POST 및 GET 작업 메서드를 작성 하는 데 상당한 시간이 소요 될 수 있습니다.

이 랩에서는 ASP.NET MVC 4 스 캐 폴딩을 사용 하 여 응용 프로그램의 CRUD (만들기, 읽기, 업데이트 및 삭제) 기준을 자동으로 생성 하는 방법을 배웁니다. 간단한 모델 클래스에서 시작 하 여 코드를 한 줄도 작성 하지 않고 모든 CRUD 작업과 필요한 모든 뷰를 포함 하는 컨트롤러를 만듭니다. 간단한 솔루션을 빌드하고 실행 한 후에는 데이터 조작을 위한 MVC 논리 및 뷰와 함께 응용 프로그램 데이터베이스를 생성 합니다.

또한 Entity Framework 마이그레이션을 사용 하 여 전체 응용 프로그램에서 모델 업데이트를 수행 하는 것이 얼마나 쉬운지 배우게 됩니다. Entity Framework 마이그레이션을 사용 하면 모델이 간단한 단계로 변경 된 후 데이터베이스를 수정할 수 있습니다. 이러한 점을 모두 염두에 두면 ASP.NET MVC 4의 최신 기능을 활용 하 여 웹 응용 프로그램을 더 효율적으로 빌드 및 유지 관리할 수 있습니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 Entity Framework 스 캐 폴딩 및 마이그레이션](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)에서 사용할 수 있습니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- 컨트롤러의 CRUD 작업에 ASP.NET 스 캐 폴딩을 사용 합니다.
- Entity Framework 마이그레이션을 사용 하 여 데이터베이스 모델을 변경 합니다.

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 랩을 완료 하려면 다음 항목이 있어야 합니다.

- [웹 또는 고급의 경우 2012 Microsoft Visual Studio Express](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (설치 방법에 대 한 지침은 [부록 a를](#AppendixA) 참조 하세요.)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

**코드 조각 설치**

편의를 위해이 랩에서 관리 하는 대부분의 코드는 Visual Studio 코드 조각으로 사용할 수 있습니다. 코드 조각을 설치 하려면 **.\Source\Setup\CodeSnippets.vsi** 파일을 실행 합니다.

Visual Studio Code 코드 조각을 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [B: 코드 조각&quot;사용](#AppendixB) &quot;부록을 참조 하세요.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

다음 연습은이 실습 랩을 구성 합니다.

1. [Entity Framework 마이그레이션과 함께 ASP.NET MVC 4 스 캐 폴딩 사용](#Exercise1)

> [!NOTE]
> 이 연습에서는 연습을 완료 한 후에 얻은 결과 솔루션을 포함 하는 **끝** 폴더를 함께 제공 합니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 가이드로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **30 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>연습 1: Entity Framework 마이그레이션과 함께 ASP.NET MVC 4 스 캐 폴딩 사용

ASP.NET MVC 스 캐 폴딩은 응용 프로그램이 데이터베이스 계층과 상호 작용할 수 있도록 하는 필수 논리를 만드는 표준화 된 방법으로 CRUD 작업을 생성 하는 빠른 방법을 제공 합니다.

이 연습에서는 code first로 ASP.NET MVC 4 스 캐 폴딩을 사용 하 여 CRUD 메서드를 만드는 방법에 대해 알아봅니다. 그런 다음 Entity Framework 마이그레이션을 사용 하 여 데이터베이스에서 변경 내용을 적용 하는 모델을 업데이트 하는 방법을 알아봅니다.

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>작업 1-스 캐 폴딩을 사용 하 여 새 ASP.NET MVC 4 프로젝트 만들기

1. 아직 열려 있지 않은 경우 **Visual Studio 2012**를 시작 합니다.
2. **파일 선택 | 새 프로젝트**입니다. 새 프로젝트 대화 상자의 **시각적 개체 C# | 웹** 섹션에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 **MVC4andEFMigrations** 로 설정 하 고이 랩의 위치를 **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** 폴더로 설정 합니다. **솔루션 이름을** **시작** 으로 설정 하 고 **솔루션용 디렉터리 만들기** 가 선택 되어 있는지 확인 합니다. **확인**을 클릭합니다.

    ![New ASP.NET MVC 4 프로젝트 대화 상자](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 프로젝트 대화 상자")

    *New ASP.NET MVC 4 프로젝트 대화 상자*
3. **새 ASP.NET MVC 4 프로젝트** 대화 상자에서 **인터넷 응용 프로그램** 템플릿을 선택 하 고 **Razor** 가 선택한 **뷰 엔진**인지 확인 합니다. **확인**을 클릭하여 프로젝트를 만듭니다.

    ![새 ASP.NET MVC 4 인터넷 응용 프로그램](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "새 ASP.NET MVC 4 인터넷 응용 프로그램")

    *새 ASP.NET MVC 4 인터넷 응용 프로그램*
4. 솔루션 탐색기에서 **모델** 을 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다.** POCO (simple class person)를 만드는 클래스입니다. 이름을 **Person** 으로 만들고 **확인**을 클릭 합니다.
5. Person 클래스를 열고 다음 속성을 삽입 합니다.

    (코드 조각- *ASP.NET MVC 4 및 Entity Framework 마이그레이션-Ex1 Person 속성*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. 빌드를 클릭 합니다.변경 내용을 저장 하 고 프로젝트를 빌드하기 위한 솔루션을 빌드합니다.

    ![애플리케이션 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "애플리케이션 빌드")

    *애플리케이션 빌드*
7. 솔루션 탐색기에서 controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.  **컨트롤러**.
8. 컨트롤러 이름을 *PersonController* 하 고 다음 값을 사용 하 여 **스 캐 폴딩 옵션** 을 완료 합니다.

   1. **템플릿** 드롭다운 목록에서 **Entity Framework 옵션을 사용 하 여 읽기/쓰기 동작 및 뷰가 포함 된 MVC 컨트롤러** 를 선택 합니다.
   2. **모델 클래스** 드롭다운 목록에서 **Person** 클래스를 선택 합니다.
   3. **데이터 컨텍스트 클래스** 목록에서 **&lt;새 데이터 컨텍스트 ...&gt;** 를 선택 합니다. 이름을 선택 하 고 **확인**을 클릭 합니다.
   4. **보기** 드롭다운 목록에서 **Razor** 가 선택 되어 있는지 확인 합니다.

      ![스 캐 폴딩을 사용 하 여 사용자 컨트롤러 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "스 캐 폴딩을 사용 하 여 사용자 컨트롤러 추가")

      *스 캐 폴딩을 사용 하 여 사용자 컨트롤러 추가*
9. **추가** 를 클릭 하 여 스 캐 폴딩이 있는 사용자에 대 한 새 컨트롤러를 만듭니다. 이제 컨트롤러 작업 및 뷰를 생성 했습니다.

    ![스 캐 폴딩이 있는 Person 컨트롤러를 만든 후](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "스 캐 폴딩이 있는 Person 컨트롤러를 만든 후")

    *스 캐 폴딩이 있는 Person 컨트롤러를 만든 후*
10. **PersonController** 클래스를 엽니다. 전체 CRUD 작업 메서드가 자동으로 생성 되었는지 확인 합니다.

   ![Person 컨트롤러 내부](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Person 컨트롤러 내부")

   *Person 컨트롤러 내부*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>작업 2-응용 프로그램 실행

이제 데이터베이스가 아직 만들어지지 않았습니다. 이 작업에서는 응용 프로그램을 처음 실행 하 고 CRUD 작업을 테스트 합니다. 데이터베이스가 Code First 즉시 생성 됩니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. 브라우저에서 URL에 **/사용자** 를 추가 하 여 사용자 페이지를 엽니다.

    ![응용 프로그램 먼저 실행](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "응용 프로그램 먼저 실행")

    *응용 프로그램: 첫 번째 실행*
3. 이제 사용자 페이지를 탐색 하 고 CRUD 작업을 테스트 합니다.

    1. 새 사용자를 추가 하려면 **새로 만들기** 를 클릭 합니다. 이름 및 성을 입력 하 고 **만들기**를 클릭 합니다.

        ![새 사용자 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "새 사용자 추가")

        *새 사용자 추가*
    2. 사용자의 목록에서 항목을 삭제, 편집 또는 추가할 수 있습니다.

        ![사용자 목록](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "사용자 목록")

        *사용자 목록*
    3. **세부** 정보를 클릭 하 여 사용자의 세부 정보를 엽니다.

        ![사용자의 세부 정보](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "사용자의 세부 정보")

        *사용자의 세부 정보*
4. 브라우저를 닫고 Visual Studio로 돌아갑니다. 코드를 한 줄도 작성 하지 않고도 모델에서 뷰로 보기에 이르기까지 응용 프로그램 전체에서 person 엔터티에 대 한 전체 CRUD를 만들었습니다.

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>작업 3-Entity Framework 마이그레이션을 사용 하 여 데이터베이스 업데이트

이 태스크에서는 Entity Framework 마이그레이션을 사용 하 여 데이터베이스를 업데이트 합니다. Entity Framework 마이그레이션 기능을 사용 하 여 모델을 변경 하 고 데이터베이스의 변경 내용을 반영 하는 것이 얼마나 쉬운지 알게 됩니다.

1. 패키지 관리자 콘솔을 엽니다. **도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**을 선택합니다.
2. 패키지 관리자 콘솔에서 다음 명령을 입력합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![마이그레이션 사용](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "마이그레이션을 사용하도록 설정")

    *마이그레이션 사용*

    마이그레이션 사용 명령은 데이터베이스를 초기화 하는 스크립트를 포함 하는 **마이그레이션** 폴더를 만듭니다.

    ![마이그레이션 폴더](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "마이그레이션 폴더")

    *마이그레이션 폴더*
3. 마이그레이션 폴더에서 **Configuration.cs** 파일을 엽니다. 클래스 생성자를 찾아 **AutomaticMigrationsEnabled** 값을 *true*로 변경 합니다.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. Person 클래스를 열고 사용자의 중간 이름에 대 한 특성을 추가 합니다. 이 새로운 특성을 사용 하 여 모델을 변경 합니다.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. **빌드 선택 |** 응용 프로그램을 빌드하기 위해 메뉴에 솔루션을 빌드합니다.

    ![애플리케이션 빌드](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "애플리케이션 빌드")

    *애플리케이션 빌드*
6. 패키지 관리자 콘솔에서 다음 명령을 입력합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    이 명령은 데이터 개체의 변경 내용을 찾은 다음 데이터베이스를 적절 하 게 수정 하는 데 필요한 명령을 추가 합니다.

    ![중간 이름 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "중간 이름 추가")

    *중간 이름 추가*
7. 필드 다음 명령을 실행 하 여 차등 업데이트를 사용 하는 SQL 스크립트를 생성할 수 있습니다. 이렇게 하면 데이터베이스를 수동으로 업데이트 (이 경우 반드시 필요 하지는 않음) 하거나 다른 데이터베이스의 변경 내용을 적용할 수 있습니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![SQL 스크립트 생성](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "SQL 스크립트 생성")

    *SQL 스크립트 생성*

    ![SQL 스크립트 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 스크립트 업데이트")

    *SQL 스크립트 업데이트*
8. 패키지 관리자 콘솔에서 다음 명령을 입력 하 여 데이터베이스를 업데이트 합니다.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![데이터베이스 업데이트](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "데이터베이스 업데이트")

    *데이터베이스 업데이트*

    Person **테이블의** **MiddleName** 열이 **Person** 클래스의 현재 정의와 일치 하도록 추가 됩니다.
9. 데이터베이스가 업데이트 되 면 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가 |를 선택 합니다.사용자 컨트롤러를 다시 추가 하는 컨트롤러입니다 (동일한 값으로 완료). 새 특성을 추가 하는 기존 메서드와 뷰가 업데이트 됩니다.

    ![컨트롤러 업데이트 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "컨트롤러 업데이트 추가")

    *컨트롤러 업데이트*
10. **추가**를 클릭합니다. 그런 다음 값 **덮어쓰기 PersonController.cs** 및 **연결 된 보기 덮어쓰기** 를 선택 하 고 **확인**을 클릭 합니다.

   ![컨트롤러 덮어쓰기 추가](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *컨트롤러 업데이트*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4-응용 프로그램 실행

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. **/사용자**를 엽니다. 중간 이름 열이 추가 된 동안 데이터가 보존 된 것을 확인할 수 있습니다.

    ![중간 이름이 추가 됨](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "중간 이름이 추가 됨")

    *중간 이름이 추가 됨*
3. **편집**을 클릭 하면 현재 사용자에 게 중간 이름을 추가할 수 있습니다.

    ![중간 이름 버전](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "중간 이름 버전")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서는 모델 클래스를 사용 하 여 ASP.NET MVC 4 스 캐 폴딩으로 CRUD 작업을 만드는 간단한 단계를 배웠습니다. 그런 다음 Entity Framework 마이그레이션을 사용 하 여 데이터베이스에서 뷰로 응용 프로그램의 종단 간 업데이트를 수행 하는 방법을 알아보았습니다.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)로 이동합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 B: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
