---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 도우미, 폼 및 유효성 검사 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 모델 및 데이터 액세스 실습 랩에서는 데이터베이스의 데이터를 로드 하 고 표시 합니다. 이 실습 랩에서는 다음에를 추가 합니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433793"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 도우미, 폼 및 유효성 검사

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

**ASP.NET MVC 4 모델 및 데이터 액세스** 실습 랩에서는 데이터베이스의 데이터를 로드 하 고 표시 합니다. 이 실습 랩에서는 **음악 스토어** 응용 프로그램에 해당 데이터를 편집 하는 기능을 추가 합니다.

이러한 목표를 염두에 두면 먼저 앨범의 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업을 지 원하는 컨트롤러를 만듭니다. ASP.NET MVC의 스 캐 폴딩 기능을 활용 하 여 HTML 테이블에 앨범 속성을 표시 하는 인덱스 뷰 템플릿을 생성 합니다. 이 보기를 향상 시키려면 긴 설명을 잘라내는 사용자 지정 HTML 도우미를 추가 합니다.

그런 다음 드롭다운과 같은 폼 요소를 사용 하 여 데이터베이스의 앨범을 변경할 수 있는 편집 및 만들기 뷰를 추가 합니다.

마지막으로 사용자가 앨범을 삭제 하 고 입력의 유효성을 검사 하 여 잘못 된 데이터를 입력 하는 것을 방지할 수 있습니다.

이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다. 이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 기본** 실습 실습을 사용 하는 것이 좋습니다.

이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 도우미, 폼 및 유효성 검사](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)에서 사용할 수 있습니다.

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- CRUD 작업을 지 원하는 컨트롤러 만들기
- HTML 테이블에 엔터티 속성을 표시 하는 인덱스 뷰 생성
- 사용자 지정 HTML 도우미 추가
- 편집 보기 만들기 및 사용자 지정
- HTTP GET 또는 HTTP POST 호출에 반응 하는 동작 메서드를 구분 합니다.
- 만들기 보기 추가 및 사용자 지정
- 엔터티 삭제를 처리 합니다.
- 사용자 입력 유효성 검사

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

1. [저장소 관리자 컨트롤러 및 해당 인덱스 뷰 만들기](#Exercise1)
2. [HTML 도우미 추가](#Exercise2)
3. [편집 뷰 만들기](#Exercise3)
4. [Create View 추가](#Exercise4)
5. [삭제 처리](#Exercise5)
6. [유효성 검사 추가](#Exercise6)
7. [클라이언트 쪽에서에이 없는 jQuery 사용](#Exercise7)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>연습 1: Store Manager 컨트롤러 및 해당 인덱스 보기 만들기

이 연습에서는 CRUD 작업을 지원 하기 위해 새 컨트롤러를 만드는 방법, 데이터베이스에서 앨범 목록을 반환 하도록 인덱스 작업 메서드를 사용자 지정 하 고, 마지막으로 ASP.NET MVC의 스 캐 폴딩을 활용 하 여 인덱스 뷰 템플릿을 생성 하는 방법에 대해 설명 합니다. HTML 테이블에 앨범 속성을 표시 하는 기능입니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>작업 1-StoreManagerController 만들기

이 작업에서는 CRUD 작업을 지원 하기 위해 **StoreManagerController** 라는 새 컨트롤러를 만듭니다.

1. **Source/Ex1-CreatingTheStoreManagerController/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. 새 컨트롤러를 추가 합니다. 이렇게 하려면 솔루션 탐색기 내의 **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 선택한 다음 **컨트롤러** 명령을 클릭 합니다. **컨트롤러** **이름을** **StoreManagerController** 로 변경 하 고 **빈 읽기/쓰기 동작이 포함 된 MVC 컨트롤러** 옵션을 선택 했는지 확인 합니다. **추가**를 클릭합니다.

    ![컨트롤러 추가 대화 상자](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "컨트롤러 추가 대화 상자")

    *컨트롤러 추가 대화 상자*

    새 컨트롤러 클래스가 생성 됩니다. 읽기/쓰기에 대 한 작업을 추가 하도록 지정 했으므로 이러한 작업에 대해 스텁 메서드를 사용 하 여 일반적인 CRUD 작업을 수행 하 고 응용 프로그램 관련 논리를 포함 하 라는 메시지를 표시 하 여 일반적인 CRUD 작업을 만듭니다.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>작업 2-StoreManager 인덱스 사용자 지정

이 태스크에서는 StoreManager Index 동작 메서드를 사용자 지정 하 여 데이터베이스의 앨범 목록과 함께 뷰를 반환 합니다.

1. StoreManagerController 클래스에서 다음 *using* 지시문을 추가 합니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-MvcMusicStore를 사용 하 여 Ex1*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. MusicStoreEntities의 인스턴스를 보유할 필드를 **StoreManagerController** 에 추가 합니다 **.**

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. StoreManagerController Index 작업을 구현 하 여 앨범 목록이 포함 된 뷰를 반환 합니다.

    컨트롤러 작업 논리는 앞에서 작성 한 StoreController의 인덱스 작업과 매우 비슷합니다. LINQ를 사용 하 여 표시할 장르 및 음악가 정보를 비롯 한 모든 앨범을 검색 합니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex1 StoreManagerController Index*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>작업 3-인덱스 뷰 만들기

이 태스크에서는 **Storemanager** 컨트롤러에서 반환 된 앨범 목록을 표시 하는 인덱스 뷰 템플릿을 만듭니다.

1. 새 뷰 템플릿을 만들기 전에 **보기 추가 대화 상자** 에서 사용할 **앨범** 클래스에 대해 알 수 있도록 프로젝트를 빌드해야 합니다. **빌드 선택 | MvcMusicStore를 빌드하여** 프로젝트를 빌드합니다.
2. **인덱스** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다. 그러면 **보기 추가** 대화 상자가 표시 됩니다.

    ![뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "뷰 추가")

    *Index 메서드 내에서 뷰 추가*
3. 보기 추가 대화 상자에서 뷰 이름이 **Index**인지 확인 합니다. **강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다. **스 캐 폴드 템플릿** 드롭다운에서 **목록** 을 선택 합니다. **뷰 엔진** 은 **Razor** 로 두고 다른 필드는 기본값으로 유지 한 다음 **추가**를 클릭 합니다.

    ![인덱스 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "인덱스 뷰 추가")

    *인덱스 뷰 추가*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>작업 4-인덱스 뷰의 스 캐 폴드 사용자 지정

이 작업에서는 ASP.NET MVC 스 캐 폴딩 기능을 사용 하 여 만든 단순 보기 템플릿을 조정 하 여 원하는 필드를 표시 하도록 합니다.

> [!NOTE]
> ASP.NET MVC 내에서 **스 캐 폴딩** 지원은 앨범 모델의 모든 필드를 나열 하는 간단한 뷰 템플릿을 생성 합니다. **스 캐 폴딩** 은 강력한 형식의 뷰를 시작 하는 빠른 방법을 제공 합니다. 즉, 뷰 템플릿을 수동으로 작성 하지 않고 스 캐 폴딩을 빠르게 기본 템플릿을 생성 한 다음 생성 된 코드를 수정할 수 있습니다.

1. 만든 코드를 검토 합니다. 생성 된 필드 목록은 **스 캐 폴딩** 이 표 형식 데이터를 표시 하는 데 사용 하는 다음 HTML 테이블에 포함 됩니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. **&lt;테이블&gt;** 코드를 다음 코드로 바꿔 **장르**, **음악가**, **앨범 제목**및 **가격** 필드만 표시 합니다. 그러면 **AlbumId** 및 **앨범 아트 URL** 열이 삭제 됩니다. 또한 GenreId 및 ArtistId 열을 변경 하 여 **Artist.Name** 및 **Genre.Name**의 연결 된 클래스 속성을 표시 하 고 **세부 정보** 링크를 제거 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 다음 설명을 변경 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 태스크에서는 **Storemanager** **인덱스** 뷰 템플릿이 이전 단계의 디자인에 따라 앨범 목록을 표시 하는지 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/Storemanager** 로 변경 하 여 앨범 목록이 표시 되는지 확인 하 고 **제목**, **음악가** 및 **장르**를 표시 합니다.

    ![앨범 목록 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "앨범 목록 찾아보기")

    *앨범 목록 찾아보기*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>연습 2: HTML 도우미 추가

StoreManager 인덱스 페이지에는 한 가지 잠재적인 문제가 있습니다. Title 및 음악가 이름 속성은 모두 테이블 서식 지정을 throw 할 수 있을 정도로 길어질 수 있습니다. 이 연습에서는 해당 텍스트를 잘라내는 사용자 지정 HTML 도우미를 추가 하는 방법에 대해 설명 합니다.

다음 그림에서는 작은 브라우저 크기를 사용할 때 텍스트의 길이 때문에 형식이 수정 되는 방법을 확인할 수 있습니다.

![잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기")

*잘리지 않은 텍스트를 사용 하 여 앨범 목록 찾아보기*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>작업 1-HTML 도우미 확장

이 작업에서는 ASP.NET MVC 뷰 내에서 노출 되는 **HTML** 개체에 새 메서드 **Truncate** 를 추가 합니다. 이렇게 하려면 ASP.NET MVC에서 제공 하는 기본 제공 system.string **도우미** 클래스에 대 한 **확장 메서드** 를 구현 합니다.

> [!NOTE]
> **확장 메서드에**대 한 자세한 내용은이 msdn 문서를 참조 하세요. [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)를 참조하세요.

1. **Source/Ex2-AddingAnHTMLHelper/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. StoreManager의 인덱스 뷰를 엽니다. 이렇게 하려면 솔루션 탐색기에서 **Views** 폴더를 확장 하 고 **storemanager** 를 확장 한 다음 **Index. cshtml** 파일을 엽니다.
3. <strong>자르기</strong> 도우미 메서드를 정의 하려면 <strong>@model</strong> 지시문 아래에 다음 코드를 추가 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>작업 2-페이지에서 텍스트 잘라내기

이 태스크에서는 **truncate** 메서드를 사용 하 여 뷰 템플릿의 텍스트를 자릅니다.

1. StoreManager의 인덱스 뷰를 엽니다. 이렇게 하려면 솔루션 탐색기에서 **Views** 폴더를 확장 하 고 **storemanager** 를 확장 한 다음 **Index. cshtml** 파일을 엽니다.
2. **음악가 이름** 및 앨범의 **제목을**표시 하는 줄을 바꿉니다. 이렇게 하려면 다음 줄을 바꿉니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 **Storemanager** **인덱스** 뷰 템플릿이 앨범의 제목 및 음악가 이름을 잘라내는 지 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/Storemanager** 로 변경 하 여 **제목** 및 **음악가** 열의 긴 텍스트가 잘리는 지 확인 합니다.

    ![잘린 제목 및 음악가 이름](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "잘린 제목 및 음악가 이름")

    *잘린 제목 및 음악가 이름*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>연습 3: 편집 뷰 만들기

이 연습에서는 상점 관리자가 앨범을 편집할 수 있도록 하는 양식을 만드는 방법을 배웁니다. **/StoreManager/Edit/id** URL (**id** 를 편집할 앨범의 고유 id)을 탐색 하므로 서버에 대 한 HTTP GET 호출을 수행 합니다.

컨트롤러 편집 작업 메서드는 데이터베이스에서 적절 한 앨범을 검색 하 고,이를 캡슐화 하는 **StoreManagerViewModel** 개체를 만든 다음,이를 보기 템플릿에 전달 하 여 HTML 페이지를 사용자에 게 다시 렌더링 합니다. 이 페이지에는 앨범 속성을 편집할 수 있는 텍스트 상자 및 드롭다운이 있는 **&lt;폼&gt;** 요소가 포함 됩니다.

사용자가 앨범 양식 값을 업데이트 하 고 **저장** 단추를 클릭 하면 HTTP POST 호출을 통해 변경 내용이 **/StoreManager/Edit/id**로 다시 전송 됩니다. URL은 마지막 호출에서와 동일 하 게 유지 되지만, ASP.NET MVC는이 시간을 HTTP POST로 식별 하므로 다른 편집 작업 메서드 ( **[HttpPost]** 를 사용 하 여 데코레이팅된 항목)를 실행 합니다.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>작업 1-HTTP-GET 편집 작업 메서드 구현

이 태스크에서는 편집 작업 메서드의 HTTP GET 버전을 구현 하 여 데이터베이스에서 적절 한 앨범을 검색 하 고 모든 장르 및 음악가의 목록도 검색 합니다. 마지막 단계에서 정의 된 **StoreManagerViewModel** 개체에이 데이터를 패키지 합니다. 그러면 응답을 렌더링 하기 위해 뷰 템플릿에 전달 됩니다.

1. **원본/Ex3-만들기** 에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **StoreManagerController** 클래스를 엽니다. 이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.
3. **HTTP-GET Edit** 작업 메서드를 다음 코드로 바꾸어 해당 하는 **앨범** 뿐만 아니라 **장르** 및 **음악가** 목록을 검색 합니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex3 STOREMANAGERCONTROLLER HTTP-편집 작업 가져오기*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > **Collections** 및 장르에 **대해 system.object를 사용 하** 는 대신 **system.web을 사용** 합니다.
    > 
    > **Selectlist** 는 HTML 드롭다운을 채우고 현재 선택 등의 작업을 관리 하는 클리너 방법입니다. 컨트롤러 작업에서 이러한 ViewModel 개체를 인스턴스화하고 나중에 설정 하면 편집 양식 시나리오가 더 명확 하 게 됩니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>작업 2-편집 보기 만들기

이 태스크에서는 나중에 앨범 속성을 표시 하는 편집 보기 템플릿을 만듭니다.

1. 편집 뷰를 만듭니다. 이렇게 하려면 **편집** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다.
2. 보기 추가 대화 상자에서 뷰 이름이 **편집**인지 확인 합니다. 강력한 형식의 **뷰 만들기** 확인란을 선택 하 고 **데이터 클래스 보기** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다. **스 캐 폴드 템플릿** 드롭다운에서 **편집** 을 선택 합니다. 다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.

    ![편집 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "편집 뷰 추가")

    *편집 뷰 추가*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 **Storemanager** **편집** 뷰 페이지에 매개 변수로 전달 된 앨범의 속성 값이 표시 되는 것을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Edit/1** 로 변경 하 여 전달 된 앨범의 속성 값이 표시 되는지 확인 합니다.

    ![탐색 앨범의 편집 보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "탐색 앨범의 편집 보기")

    *탐색 앨범의 편집 보기*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>작업 4-앨범 편집기 템플릿에서 드롭다운 구현

이 태스크에서는 사용자가 음악가와 장르 목록에서 선택할 수 있도록 마지막 태스크에서 만든 보기 템플릿에 드롭다운을 추가 합니다.

1. 모든 **앨범** 필드 집합 코드를 다음으로 바꿉니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > 아티스트와 장르를 선택 하기 위한 드롭다운을 렌더링 하기 위한 **Html DropDownList** 도우미가 추가 되었습니다. **Html. DropDownList** 에 전달 된 매개 변수는 다음과 같습니다.
    > 
    > 1. 폼 필드의 이름 ( **&quot;ArtistId&quot;** )입니다.
    > 2. 드롭다운의 값 **목록** 입니다.

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 태스크에서는 **Storemanager** **편집** 뷰 페이지에서 음악가 및 장르 ID 텍스트 필드 대신 드롭다운을 표시 하는지 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Edit/1** 로 변경 하 여 음악가 및 장르 ID 텍스트 필드가 아닌 드롭다운이 표시 되는지 확인 합니다.

    ![드롭다운을 사용 하 여 앨범의 편집 뷰 찾아보기](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "드롭다운을 사용 하 여 앨범의 편집 뷰 찾아보기")

    *이번에는 드롭다운을 사용 하 여 앨범의 편집 보기를 검색 합니다.*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>작업 6-HTTP-사후 편집 작업 메서드 구현

이제 편집 뷰가 예상 대로 표시 되므로, 앨범에 대 한 변경 내용을 저장 하기 위해 HTTP POST 편집 작업 메서드를 구현 해야 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **Controllers** 폴더에서 **StoreManagerController** 을 엽니다.
2. **HTTP-POST 편집** 작업 메서드 코드를 다음으로 바꿉니다 (교체 해야 하는 메서드는 두 개의 매개 변수를 받는 오버 로드 된 버전).

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex3 STOREMANAGERCONTROLLER HTTP-사후 편집 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > 이 메서드는 사용자가 뷰의 **저장** 단추를 클릭 하 고 폼 값의 HTTP POST를 서버에 다시 실행 하 여 데이터베이스에 보관 하는 경우 실행 됩니다. 데코레이터 **[HttpPost]** 는 메서드를 이러한 HTTP 게시 시나리오에 사용 해야 함을 나타냅니다. 메서드는 **앨범** 개체를 사용 합니다. ASP.NET MVC는 게시 된 &lt;양식&gt; 값에서 앨범 개체를 자동으로 만듭니다.
    > 
    > 이 메서드는 다음 단계를 수행 합니다.
    > 
    > 1. Model이 올바르면 다음을 수행 합니다.
    > 
    >     1. 컨텍스트에서 앨범 항목을 업데이트 하 여 수정 된 개체로 표시 합니다.
    >     2. 변경 내용을 저장 하 고 인덱스 뷰로 리디렉션합니다.
    > 2. 모델이 유효 하지 않으면 ViewBag을 **GenreId** 및 **ArtistId**로 채운 다음 수신 된 앨범 개체가 있는 뷰를 반환 하 여 사용자가 필요한 업데이트를 수행할 수 있도록 합니다.

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>작업 7-응용 프로그램 실행

이 태스크에서는 **Storemanager 편집** 뷰 페이지가 실제로 업데이트 된 앨범 데이터를 데이터베이스에 저장 하는지 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Edit/1**로 변경 합니다. 앨범 제목을 **로드** 로 변경 하 고 **저장**을 클릭 합니다. 앨범의 제목이 실제로 앨범 목록에서 변경 되었는지 확인 합니다.

    ![앨범 업데이트](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "앨범 업데이트")

    *앨범 업데이트*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>연습 4: Create View 추가

이제 **StoreManagerController** **편집** 기능을 지원 하기 때문에이 연습에서는 저장소 관리자가 새 앨범을 응용 프로그램에 추가할 수 있도록 뷰 만들기 템플릿을 추가 하는 방법에 대해 알아봅니다.

편집 기능을 사용 하는 것 처럼 **StoreManagerController** 클래스 내에서 두 개의 별도 메서드를 사용 하 여 Create 시나리오를 구현 합니다.

1. 상점 관리자가 먼저 **/StoreManager/Create** URL을 방문 하는 경우 하나의 작업 메서드가 빈 폼을 표시 합니다.
2. 두 번째 작업 메서드는 저장소 관리자가 양식 내에서 **저장** 단추를 클릭 하 고 값을 다시 **/STOREMANAGER/CREATE** URL에 HTTP POST로 전송 하는 시나리오를 처리 합니다.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>작업 1-HTTP-GET 작업 메서드 구현

이 작업에서는 Create action 메서드의 HTTP GET 버전을 구현 하 여 모든 장르 및 음악가 목록을 검색 하 고,이 데이터를 **StoreManagerViewModel** 개체에 패키지 하 고,이 데이터를 뷰 템플릿으로 전달 합니다.

1. **Source/Ex4-AddingACreateView/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **StoreManagerController** 클래스를 엽니다. 이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.
3. **만들기** 작업 메서드 코드를 다음으로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex4 STOREMANAGERCONTROLLER HTTP-GET 만들기 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>작업 2-만들기 뷰 추가

이 태스크에서는 새 (비어 있음) 앨범 양식을 표시 하는 뷰 만들기 템플릿을 추가 합니다.

1. **만들기** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다. 그러면 보기 추가 대화 상자가 표시 됩니다.
2. 보기 추가 대화 상자에서 보기 이름이 **생성**인지 확인 합니다. **강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 하 고 **스 캐 폴드 템플릿** 드롭다운에서 **만들기** 를 선택 합니다. 다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.

    ![Create view 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view")

    *Create View 추가*
3. 아래와 같이 드롭다운 목록을 사용 하도록 **GenreId** 및 **ArtistId** 필드를 업데이트 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>작업 3-응용 프로그램 실행

이 태스크에서는 **Storemanager** 뷰 **만들기** 페이지에 빈 앨범 양식이 표시 되는 것을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Create**로 변경 합니다. 새 앨범 속성을 채우도록 빈 양식이 표시 되는지 확인 합니다.

    ![빈 폼을 사용 하 여 뷰 만들기](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "빈 폼을 사용 하 여 뷰 만들기")

    *빈 폼을 사용 하 여 뷰 만들기*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>작업 4-HTTP POST 만들기 작업 메서드 구현

이 작업에서는 사용자가 **저장** 단추를 클릭할 때 호출 되는 Create ACTION 메서드의 HTTP POST 버전을 구현 합니다. 메서드는 데이터베이스에 새 앨범을 저장 해야 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **StoreManagerController** 클래스를 엽니다. 이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.
2. **HTTP-POST 만들기** 작업 메서드 코드를 다음으로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex4 STOREMANAGERCONTROLLER HTTP-사후 만들기 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > 만들기 작업은 이전 편집 작업 메서드와 비슷하지만 개체를 수정 된 것으로 설정 하는 대신 컨텍스트에 추가 됩니다.

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 태스크에서는 **storemanager 뷰 만들기** 페이지에서 새 앨범을 만든 다음 Storemanager 인덱스 뷰로 리디렉션하는 테스트를 수행할 수 있습니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Create**로 변경 합니다. 다음 그림에 나와 있는 것 처럼 모든 양식 필드를 새 앨범의 데이터로 채웁니다.

    ![앨범 만들기](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "앨범 만들기")

    *앨범 만들기*
3. 방금 만든 새 앨범이 포함 된 StoreManager 인덱스 뷰로 리디렉션되도록 합니다.

    ![새 앨범 만듦](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "새 앨범 만듦")

    *새 앨범 만듦*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>연습 5: 삭제 처리

앨범을 삭제 하는 기능은 아직 구현 되지 않았습니다. 이 연습을 수행 합니다. 이전과 마찬가지로 **StoreManagerController** 클래스 내에서 두 개의 개별 메서드를 사용 하 여 삭제 시나리오를 구현 합니다.

1. 하나의 작업 메서드가 확인 폼을 표시 합니다.
2. 두 번째 작업 메서드는 폼 제출을 처리 합니다.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>작업 1-HTTP-GET 삭제 작업 메서드 구현

이 작업에서는 삭제 작업 메서드의 HTTP-GET 버전을 구현 하 여 앨범 정보를 검색 합니다.

1. **Source/Ex5-HandlingDeletion/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **StoreManagerController** 클래스를 엽니다. 이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.
3. 컨트롤러 삭제 작업은 이전 저장소 정보 컨트롤러 작업과 동일 합니다. URL에 제공 된 **id** 를 사용 하 여 데이터베이스에서 **앨범** 개체를 쿼리하고 적절 한 **뷰**를 반환 합니다. 이렇게 하려면 HTTP-GET **Delete** 작업 메서드 코드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-삭제 작업 가져오기*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. **Delete** 동작 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다. 그러면 보기 추가 대화 상자가 표시 됩니다.
5. 보기 추가 대화 상자에서 뷰 이름이 **삭제**인지 확인 합니다. **강력한 형식의 뷰 만들기** 옵션을 선택 하 고 **모델 클래스** 드롭다운에서 **앨범 (MvcMusicStore)** 을 선택 합니다. **스 캐 폴드 템플릿** 드롭다운에서 **삭제** 를 선택 합니다. 다른 필드의 기본값을 그대로 두고 **추가**를 클릭 합니다.

    ![삭제 뷰 추가](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "삭제 뷰 추가")

    *삭제 뷰 추가*
6. 삭제 템플릿은 모델의 모든 필드를 표시 합니다. 앨범의 제목만 표시 됩니다. 이렇게 하려면 뷰의 내용을 다음 코드로 바꿉니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 태스크에서는 **Storemanager** 뷰 **삭제** 페이지에 확인 삭제 양식이 표시 되는 것을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/Storemanager**로 변경 합니다. **삭제** 를 클릭 하 여 삭제할 앨범을 하나 선택 하 고 새 보기가 업로드 되었는지 확인 합니다.

    ![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "앨범 삭제")

    *앨범 삭제*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>작업 3-HTTP-사후 삭제 작업 메서드 구현

이 작업에서는 사용자가 **삭제** 단추를 클릭할 때 호출 되는 delete 동작 메서드의 HTTP POST 버전을 구현 합니다. 메서드는 데이터베이스의 앨범을 삭제 해야 합니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio 창으로 돌아갑니다. **StoreManagerController** 클래스를 엽니다. 이렇게 하려면 **Controllers** 폴더를 확장 하 고 **StoreManagerController.cs**를 두 번 클릭 합니다.
2. **HTTP-사후 삭제** 작업 메서드 코드를 다음 코드로 바꿉니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex5 처리 삭제 HTTP-사후 삭제 작업*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 태스크에서는 **storemanager 뷰 삭제** 페이지를 사용 하 여 앨범을 삭제 한 다음 Storemanager 인덱스 뷰로 리디렉션하는 것을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/Storemanager**로 변경 합니다. 삭제를 클릭 하 여 삭제할 앨범 하나를 선택 **합니다.** **삭제** 단추를 클릭 하 여 삭제를 확인 합니다.

    ![앨범 삭제](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "앨범 삭제")

    *앨범 삭제*
3. 앨범이 **인덱스** 페이지에 나타나지 않으므로 삭제 되었는지 확인 합니다.

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>연습 6: 유효성 검사 추가

현재 보유 하 고 있는 양식 만들기 및 편집은 어떤 종류의 유효성 검사도 수행 하지 않습니다. 사용자가 필수 필드를 비워 두고 price 필드에 문자를 입력 하는 경우 첫 번째 오류는 데이터베이스에서 가져옵니다.

모델 클래스에 데이터 주석을 추가 하 여 응용 프로그램에 유효성 검사를 추가할 수 있습니다. 데이터 주석을 사용 하면 모델 속성에 적용 하려는 규칙을 설명할 수 있으며, ASP.NET MVC는 사용자에 게 적절 한 메시지를 적용 하 고 표시 합니다.

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>작업 1-데이터 주석 추가

이 태스크에서는 적절 한 경우 만들기 및 편집 페이지 표시 유효성 검사 메시지를 만드는 앨범 모델에 데이터 주석을 추가 합니다.

간단한 모델 클래스의 경우에는 **system.componentmodel**에 대 한 **using** 문을 추가 하 고 적절 한 속성에 **[Required]** 특성을 배치 하 여 데이터 주석을 추가 하기만 하면 됩니다. 다음 예에서는 **이름** 속성을 뷰의 필수 필드로 설정 합니다.

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

이 응용 프로그램이 엔터티 데이터 모델를 생성 하는 경우에는이 응용 프로그램이 좀 더 복잡 합니다. 모델 클래스에 직접 데이터 주석을 추가한 경우 데이터베이스에서 모델을 업데이트 하면 덮어씁니다. 대신 주석을 보유 하기 위해 존재 하 고 **[MetadataType]** 특성을 사용 하 여 모델 클래스와 연결 된 메타 데이터 부분 클래스를 사용할 수 있습니다.

1. **Source/Ex6-AddingValidation/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **모델** 폴더에서 **Album.cs** 을 엽니다.
3. **Album.cs** 콘텐츠를 강조 표시 된 코드로 대체 하 여 다음과 같이 표시 되도록 합니다.

    > [!NOTE]
    > **[Displayformat (ConvertEmptyStringToNull = false)]** 줄은 데이터 원본에서 데이터 필드가 업데이트 될 때 모델의 빈 문자열이 null로 변환 되지 않음을 나타냅니다. 이 설정은 데이터 주석이 필드의 유효성을 검사 하기 전에 Entity Framework에서 모델에 null 값을 할당 하는 경우 예외를 방지 합니다.

    (코드 조각- *ASP.NET MVC 4 도우미 및 폼 및 유효성 검사-Ex6 앨범 메타 데이터 partial 클래스*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > 이 **앨범** 부분 클래스에는 데이터 주석의 **AlbumMetaData** 클래스를 가리키는 **MetadataType** 특성이 있습니다. 앨범 모델에 주석을 추가 하는 데 사용 하는 데이터 주석 특성은 다음과 같습니다.
    > 
    > - 필수-속성이 필수 필드 임을 나타냅니다.
    > - DisplayName-양식 필드 및 유효성 검사 메시지에 사용할 텍스트를 정의 합니다.
    > - DisplayFormat-데이터 필드를 표시 하 고 서식을 지정 하는 방법을 지정 합니다.
    > - StringLength-문자열 필드의 최대 길이를 정의 합니다.
    > - 범위-숫자 필드에 대 한 최대값 및 최소값을 제공 합니다.
    > - ScaffoldColumn-편집기 양식에서 필드를 숨길 수 있습니다.

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 태스크에서는 마지막 작업에서 선택한 표시 이름을 사용 하 여 페이지 만들기 및 편집 페이지의 유효성을 검사 하는 방법을 테스트 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/StoreManager/Create**로 변경 합니다. 표시 이름이 partial 클래스의 이름과 일치 하는지 확인 합니다 (예: **AlbumArtUrl**대신 **앨범 아트 URL** ).
3. 양식을 채우지 않고 **만들기**를 클릭 합니다. 해당 유효성 검사 메시지가 있는지 확인 합니다.

    ![만들기 페이지의 유효성을 검사 한 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "만들기 페이지의 유효성을 검사 한 필드")

    *만들기 페이지의 유효성을 검사 한 필드*
4. **편집** 페이지에서 동일한가 발생 하는지 확인할 수 있습니다. URL을 **/StoreManager/Edit/1** 로 변경 하 고 표시 이름이 부분 클래스 (예: **AlbumArtUrl**대신 **앨범 아트 URL** )의 이름과 일치 하는지 확인 합니다. **제목** 및 **가격** 필드를 비운 후 **저장**을 클릭 합니다. 해당 유효성 검사 메시지가 있는지 확인 합니다.

    ![편집 페이지의 유효성을 검사 한 필드](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *편집 페이지의 유효성을 검사 한 필드*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>연습 7: 클라이언트 쪽에서 조심 스럽게 jQuery 사용

이 연습에서는 클라이언트 쪽에서 MVC 4를 사용 하지 않는 jQuery 유효성 검사를 사용 하도록 설정 하는 방법을 배웁니다.

> [!NOTE]
> 조심 스럽게 jQuery는 데이터 ajax 접두사 JavaScript를 사용 하 여 인라인 클라이언트 스크립트를 intrusively 내보내는 대신 서버에서 작업 메서드를 호출 합니다.

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>작업 1-방해 하지 않는 jQuery를 사용 하도록 설정 하기 전에 응용 프로그램 실행

이 태스크에서는 jQuery를 포함 하기 전에 응용 프로그램을 실행 하 여 두 유효성 검사 모델을 비교 합니다.

1. **Source/Ex7-UnobtrusivejQueryValidation/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **F5** 키를 눌러 애플리케이션을 실행합니다.
3. 프로젝트가 홈 페이지에서 시작 됩니다. **/StoreManager/Create** 를 찾아보고 폼을 채우지 않고 **만들기** 를 클릭 하 여 유효성 검사 메시지를 수신 하는지 확인 합니다.

    ![클라이언트 유효성 검사 사용 안 함](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "클라이언트 유효성 검사 사용 안 함")

    *클라이언트 유효성 검사 사용 안 함*
4. 브라우저에서 HTML 소스 코드를 엽니다.

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>작업 2-비 클라이언트 유효성 검사 사용

이 태스크에서는 **web.config** 파일에서 jQuery를 사용 하지 않는 **클라이언트 유효성 검사** 를 사용 하도록 설정 합니다 .이는 기본적으로 모든 새 ASP.NET MVC 4 프로젝트에서 false로 설정 됩니다. 또한 jQuery를 사용 하지 않는 클라이언트 유효성 검사 작업을 수행 하는 데 필요한 스크립트 참조를 추가 합니다.

1. 프로젝트 루트에서 **web.config** 파일을 열고 **clientvalidationenabled** 및 **UnobtrusiveJavaScriptEnabled** keys 값이 **true**로 설정 되어 있는지 확인 합니다.

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > Global.asax.cs에서 코드에의 한 클라이언트 유효성 검사를 사용 하도록 설정 하 여 동일한 결과를 얻을 수도 있습니다.
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > 또한 모든 컨트롤러에 ClientValidationEnabled 특성을 할당 하 여 사용자 지정 동작을 수행할 수 있습니다.
2. **Views\StoreManager**에서 **Create. cshtml** 를 엽니다.
3. 다음 스크립트 파일 **jquery. validate** 및 **jquery.** **/bundles/jqueryval**&quot; 번들을 &quot;통해 뷰에서 참조 되는지 확인 합니다.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > 이러한 모든 jQuery 라이브러리는 MVC 4 새 프로젝트에 포함 되어 있습니다. 프로젝트의 **/Scripts** 폴더에서 더 많은 라이브러리를 찾을 수 있습니다.
    > 
    > 이 유효성 검사 라이브러리를 작동 시키려면 jQuery 프레임 워크 라이브러리에 대 한 참조를 추가 해야 합니다. 이 참조는 이미 **\_레이아웃. cshtml** 파일에 추가 되었으므로이 특정 뷰에 추가할 필요가 없습니다.

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>작업 3-방해 되지 않는 jQuery 유효성 검사를 사용 하 여 응용 프로그램 실행

이 태스크에서는 사용자가 새 앨범을 만들 때 **Storemanager** create View 템플릿이 jQuery 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사를 수행 하는지 테스트 합니다.

1. **F5** 키를 눌러 애플리케이션을 실행합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. **/StoreManager/Create** 를 찾아보고 폼을 채우지 않고 **만들기** 를 클릭 하 여 유효성 검사 메시지를 수신 하는지 확인 합니다.

    ![JQuery를 사용 하 여 클라이언트 유효성 검사 사용](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "JQuery를 사용 하 여 클라이언트 유효성 검사 사용")

    *JQuery를 사용 하 여 클라이언트 유효성 검사 사용*
3. 브라우저에서 뷰 만들기에 대 한 소스 코드를 엽니다.

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 각 클라이언트 유효성 검사 규칙에 대해*rulename*=&quot;*메시지*&quot;특성이 있는 특성을 추가 합니다. 다음은 클라이언트 유효성 검사를 수행 하기 위해 html 입력 필드에 삽입 하지 않는 태그의 목록입니다.
   > 
   > - 데이터-val
   > - Data-val-number
   > - 데이터-val 범위
   > - 데이터-val 범위-min/Data-val-range-max
   > - Data-val-필수
   > - 데이터-val 길이
   > - Data-val-length-max/Data-val-length-min
   > 
   > 모든 데이터 값은 모델 **데이터 주석**으로 채워집니다. 그런 다음 서버 쪽에서 작동 하는 모든 논리를 클라이언트 쪽에서 실행할 수 있습니다. 예를 들어 Price 특성은 모델에 다음과 같은 데이터 주석을 포함 합니다.
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 비-jQuery를 사용한 후 생성 된 코드는 다음과 같습니다.
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 다음을 사용 하 여 사용자가 데이터베이스에 저장 된 데이터를 변경할 수 있도록 하는 방법을 배웠습니다.

- 인덱스, 만들기, 편집, 삭제 등의 컨트롤러 작업
- HTML 테이블에 속성을 표시 하기 위한 ASP.NET MVC의 스 캐 폴딩 기능
- 사용자 환경을 개선 하기 위한 사용자 지정 HTML 도우미
- HTTP GET 또는 HTTP POST 호출에 반응 하는 작업 메서드
- 만들기 및 편집 같은 유사한 보기 템플릿에 대 한 공유 편집기 템플릿
- 드롭다운 같은 폼 요소
- 모델 유효성 검사에 대 한 데이터 주석
- JQuery를 사용 하지 않는 라이브러리를 사용 하 여 클라이언트 쪽 유효성 검사

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>부록 B: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
