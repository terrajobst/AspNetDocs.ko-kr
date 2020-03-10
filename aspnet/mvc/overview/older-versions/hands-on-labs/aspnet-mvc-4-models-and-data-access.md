---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 모델 및 데이터 액세스 | Microsoft Docs
author: rick-anderson
description: 참고:이 실습 랩에서는 ASP.NET MVC에 대 한 기본 지식이 있다고 가정 합니다. 이전에 ASP.NET MVC를 사용 하지 않은 경우 ASP.NET MVC 4를 대신 사용 하는 것이 좋습니다.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451469"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 모델 및 데이터 액세스

[웹 캠프 팀](https://twitter.com/webcamps)

[웹 캠프 교육 키트 다운로드](https://aka.ms/webcamps-training-kit)

이 실습 랩에서는 **ASP.NET MVC**에 대 한 기본 지식이 있다고 가정 합니다. 이전에 **ASP.NET mvc** 를 사용 하지 않은 경우 **ASP.NET mvc 4 기본** 실습 실습을 사용 하는 것이 좋습니다.

이 랩에서는 원본 폴더에 제공 된 샘플 웹 응용 프로그램에 사소한 변경 사항을 적용 하 여 앞에서 설명한 향상 된 기능 및 새로운 기능을 안내 합니다.

> [!NOTE]
> 모든 샘플 코드와 코드 조각은 [Microsoft 웹/WebCampTrainingKit 릴리스에서](https://aka.ms/webcamps-training-kit)제공 되는 웹 캠프 교육 키트에 포함 되어 있습니다. 이 랩에서 관련 된 프로젝트는 [ASP.NET MVC 4 모델 및 데이터 액세스](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)에서 사용할 수 있습니다.

**ASP.NET MVC 기본** 실습 랩에서는 하드 코드 된 데이터를 컨트롤러에서 보기 템플릿으로 전달 했습니다. 그러나 실제 웹 응용 프로그램을 빌드하기 위해 실제 데이터베이스를 사용 하는 것이 좋습니다.

이 실습 랩에서는 Music Store 응용 프로그램에 필요한 데이터를 저장 하 고 검색 하기 위해 데이터베이스 엔진을 사용 하는 방법을 보여 줍니다. 이렇게 하려면 기존 데이터베이스로 시작 하 고이 데이터베이스에서 엔터티 데이터 모델를 만듭니다. 이 랩에서는 **Database First** 접근 방식 뿐만 아니라 **Code First** 방법도 충족 합니다.

그러나 **Model First** 방법을 사용 하 고 도구를 사용 하 여 동일한 모델을 만든 다음 여기에서 데이터베이스를 생성할 수도 있습니다.

![Database First와 Model First 비교](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First와 Model First 비교")

*Database First와 Model First 비교*

모델을 생성 한 후에는 하드 코드 된 데이터를 사용 하는 대신 StoreController에서 적절 하 게 조정 하 여 데이터베이스에서 가져온 데이터와 저장소 뷰를 제공 합니다. 이번에는 데이터가 데이터베이스에서 제공 되는 경우를 비롯 하 여 StoreController가 뷰 템플릿에 대해 동일한 ViewModels를 반환 하기 때문에 뷰 템플릿을 변경할 필요가 없습니다.

**Code First 방법**

Code First 방법을 사용 하면 일반적으로 프레임 워크와 결합 된 클래스를 생성 하지 않고 코드에서 모델을 정의할 수 있습니다.

Code first에서 모델 개체는 POCOs, &quot;일반 이전 CLR 개체&quot;를 사용 하 여 정의 됩니다. POCOs는 상속이 없고 인터페이스를 구현 하지 않는 간단한 일반 클래스입니다. 데이터베이스를 자동으로 생성 하거나 기존 데이터베이스를 사용 하 고 코드에서 클래스 매핑을 생성할 수 있습니다.

이 방법을 사용할 경우의 이점은 POCOs 클래스가 매핑 프레임 워크와 결합 되지 않으므로 모델은 지 속성 프레임 워크 (이 경우 Entity Framework)와 독립적으로 유지 된다는 것입니다.

> [!NOTE]
> 이 랩은이 실습 랩에 표시 된 기능에 맞게 사용자 지정 및 최소화 된 ASP.NET MVC 4 및 버전의 Music Store 샘플 응용 프로그램을 기반으로 합니다.
> 
> 전체 **음악 스토어** 자습서 응용 프로그램을 탐색 하려는 경우 [MVC-음악 스토어](https://github.com/evilDave/MVC-Music-Store)에서 찾을 수 있습니다.

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

Visual Studio Code 코드 조각에 대해 잘 모르는 경우이를 사용 하는 방법을 알아보려면이 문서의 부록 [C: 코드 조각&quot;사용](#AppendixC) &quot;부록을 참조할 수 있습니다.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩은 다음 연습으로 구성 됩니다.

1. [연습 1: 데이터베이스 추가](#Exercise1)
2. [연습 2: Code First을 사용 하 여 데이터베이스 만들기](#Exercise2)
3. [연습 3: 매개 변수를 사용 하 여 데이터베이스 쿼리](#Exercise3)

> [!NOTE]
> 각 연습에는 연습을 완료 한 후 얻게 되는 결과 솔루션을 포함 하는 **끝** 폴더가 함께 제공 됩니다. 연습을 진행 하는 데 도움이 필요한 경우이 솔루션을 지침으로 사용할 수 있습니다.

이 랩을 완료 하는 데 소요 되는 예상 시간: **35 분**

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>연습 1: 데이터베이스 추가

이 연습에서는 데이터를 사용 하기 위해 MusicStore 응용 프로그램의 테이블이 포함 된 데이터베이스를 솔루션에 추가 하는 방법에 대해 설명 합니다. 데이터베이스가 모델을 사용 하 여 생성 되 고 솔루션에 추가 된 후에는 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 뷰 템플릿에 제공 하도록 StoreController 클래스를 수정 합니다.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>작업 1-데이터베이스 추가

이 태스크에서는 MusicStore 응용 프로그램의 주 테이블이 포함 된 이미 생성 된 데이터베이스를 솔루션에 추가 합니다.

1. **Source/Ex1-AddingADatabaseDBFirst/begin/** 폴더에 있는 **시작** 솔루션을 엽니다.

   1. 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **MvcMusicStore** 데이터베이스 파일을 추가 합니다. 이 실습 랩에서는 이미 생성 된 **MvcMusicStore**라는 데이터베이스를 사용 합니다. 이렇게 하려면 **앱\_데이터** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **기존 항목**을 클릭 합니다. **\Source\sts\source\asset** 로 이동 하 여 **MvcMusicStore** 파일을 선택 합니다.

    ![기존 항목 추가](aspnet-mvc-4-models-and-data-access/_static/image2.png "기존 항목 추가")

    *기존 항목 추가*

    ![MvcMusicStore 데이터베이스 파일](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore 데이터베이스 파일")

    *MvcMusicStore 데이터베이스 파일*

    데이터베이스가 프로젝트에 추가 되었습니다. 데이터베이스가 솔루션 내에 있는 경우에도 다른 데이터베이스 서버에서 호스팅되는 것으로 쿼리 및 업데이트할 수 있습니다.

    ![솔루션 탐색기의 MvcMusicStore 데이터베이스](aspnet-mvc-4-models-and-data-access/_static/image4.png "솔루션 탐색기의 MvcMusicStore 데이터베이스")

    *솔루션 탐색기의 MvcMusicStore 데이터베이스*
3. 데이터베이스에 대 한 연결을 확인 합니다. 이렇게 하려면 **MvcMusicStore** 를 두 번 클릭 하 여 연결을 설정 합니다.

    ![MvcMusicStore에 연결](aspnet-mvc-4-models-and-data-access/_static/image5.png "MvcMusicStore에 연결")

    *MvcMusicStore에 연결*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>작업 2-데이터 모델 만들기

이 태스크에서는 이전 태스크에 추가 된 데이터베이스와 상호 작용 하는 데이터 모델을 만듭니다.

1. 데이터베이스를 나타내는 데이터 모델을 만듭니다. 이렇게 하려면 솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **새 항목**을 클릭 합니다. **새 항목 추가** 대화 상자에서 **데이터** 템플릿을 선택 하 고 **ADO.NET 엔터티 데이터 모델** 항목을 선택 합니다. 데이터 모델 이름을 **Storedb .edmx** 로 변경 하 고 **추가**를 클릭 합니다.

    ![StoreDB ADO.NET 엔터티 데이터 모델 추가](aspnet-mvc-4-models-and-data-access/_static/image6.png "StoreDB ADO.NET 엔터티 데이터 모델 추가")

    *StoreDB ADO.NET 엔터티 데이터 모델 추가*
2. **엔터티 데이터 모델 마법사** 가 나타납니다. 이 마법사는 모델 계층을 만드는 과정을 안내 합니다. 최근에 추가 된 기존 데이터베이스를 기반으로 모델을 만들어야 하므로 **데이터베이스에서 생성** 을 선택 하 고 **다음**을 클릭 합니다.

    ![모델 콘텐츠 선택](aspnet-mvc-4-models-and-data-access/_static/image7.png "모델 콘텐츠 선택")

    *모델 콘텐츠 선택*
3. 데이터베이스에서 모델을 생성 하기 때문에 사용할 연결을 지정 해야 합니다. **새 연결**을 클릭 합니다.
4. **데이터베이스 파일 Microsoft SQL Server** 선택 하 고 **계속**을 클릭 합니다.

    ![데이터 원본 선택](aspnet-mvc-4-models-and-data-access/_static/image8.png "데이터 원본 선택")

    *데이터 소스 선택 대화 상자*
5. **찾아보기** 를 클릭 하 고 **App\_Data** 폴더에 있는 데이터베이스 **MvcMusicStore** 를 선택 하 고 **확인**을 클릭 합니다.

    ![연결 속성](aspnet-mvc-4-models-and-data-access/_static/image9.png "연결 속성")

    *연결 속성*
6. 생성 된 클래스의 이름은 엔터티 연결 문자열과 동일 해야 하므로 이름을 **MusicStoreEntities** 로 변경 하 고 **다음**을 클릭 합니다.

    ![데이터 연결 선택](aspnet-mvc-4-models-and-data-access/_static/image10.png "데이터 연결 선택")

    *데이터 연결 선택*
7. 사용할 데이터베이스 개체를 선택 합니다. 엔터티 모델은 데이터베이스의 테이블만 사용 하 고, **테이블** 옵션을 선택 하 고, **모델에 외래 키 열 포함** 및 **복수화 또는 단 수 생성 된 개체 이름** 옵션도 선택 되어 있는지 확인 합니다. 모델 네임 스페이스를 **MvcMusicStore** 로 변경 하 고 **마침**을 클릭 합니다.

    ![데이터베이스 개체 선택](aspnet-mvc-4-models-and-data-access/_static/image11.png "데이터베이스 개체 선택")

    *데이터베이스 개체 선택*

    > [!NOTE]
    > 보안 경고 대화 상자가 표시 되 면 **확인** 을 클릭 하 여 템플릿을 실행 하 고 모델 엔터티에 대 한 클래스를 생성 합니다.
8. 데이터베이스에 대 한 엔터티 다이어그램이 표시 되는 반면, 각 테이블을 데이터베이스에 매핑하는 별도의 클래스가 생성 됩니다. 예를 들어 앨범 **테이블은** **앨범** 클래스로 표현 되며, 여기서 테이블의 각 열은 클래스 속성에 매핑됩니다. 이렇게 하면 데이터베이스의 행을 나타내는 개체를 쿼리하고 작업할 수 있습니다.

    ![엔터티 다이어그램](aspnet-mvc-4-models-and-data-access/_static/image12.png "엔터티 다이어그램")

    *엔터티 다이어그램*

    > [!NOTE]
    > T4 템플릿 (.tt)은 엔터티 클래스를 생성 하는 코드를 실행 하 고 같은 이름의 기존 클래스를 덮어씁니다. 이 예제에서는 &quot;앨범&quot;, &quot;장르&quot; 및 &quot;음악가&quot; 생성 된 코드로 덮어쓴 클래스입니다.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>작업 3-응용 프로그램 빌드

이 태스크에서는 모델 생성이 **앨범**, **장르** 및 **음악가** 모델 클래스를 제거 했지만 새 데이터 모델 클래스를 사용 하 여 프로젝트가 성공적으로 빌드 되었는지 확인 합니다.

1. **빌드** 메뉴 항목을 선택한 다음 **MvcMusicStore 빌드**를 선택 하 여 프로젝트를 빌드합니다.

    ![프로젝트 빌드](aspnet-mvc-4-models-and-data-access/_static/image13.png "프로젝트 빌드")

    *프로젝트 빌드*
2. 프로젝트가 성공적으로 빌드됩니다. 그래도 작동 하는 이유는 무엇 인가요? 데이터베이스 테이블에는 제거 된 클래스의 **앨범** 및 **장르**에서 사용 하는 속성을 포함 하는 필드가 있기 때문에 작동 합니다.

    ![빌드 성공](aspnet-mvc-4-models-and-data-access/_static/image14.png "빌드 성공")

    *빌드 성공*
3. 디자이너에서 엔터티를 다이어그램 형식으로 표시 하는 동안 해당 엔터티는 C# 정말 클래스입니다. 솔루션 탐색기에서 **Storedb .edmx** 노드를 확장 한 다음 **StoreDB.tt**를 확장 하면 새로 생성 된 엔터티가 표시 됩니다.

    ![생성된 파일](aspnet-mvc-4-models-and-data-access/_static/image15.png "생성 된 파일")

    *생성된 파일*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>작업 4-데이터베이스 쿼리

이 작업에서는 하드 코드 된 데이터를 사용 하는 대신 데이터베이스를 쿼리하여 정보를 검색 하도록 StoreController 클래스를 업데이트 합니다.

1. **Controllers\StoreController.cs** 을 열고 클래스에 다음 필드를 추가 하 여 **Storedb**라는 **MusicStoreEntities** 클래스의 인스턴스를 포함 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다. 모든 **앨범이**포함 된 장르를 검색 하도록 **찾아보기** 작업 메서드를 업데이트 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex1 저장소 찾아보기*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > **LINQ** (언어 통합 쿼리) 라는 .net 기능을 사용 하 여 이러한 컬렉션에 대해 강력한 형식의 쿼리 식을 작성 합니다 .이 기능을 사용 하면 데이터베이스에 대해 코드를 실행 하 고 프로그래밍할 수 있는 개체를 반환 합니다.
    > 
    > LINQ에 대 한 자세한 내용은 [msdn 사이트](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)를 참조 하십시오.
3. **인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex1 저장소 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. **인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 하 고 컬렉션을 목록으로 변환 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex1 저장소 GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 태스크에서는 저장소 인덱스 페이지에 하드 코드 된 항목이 아니라 데이터베이스에 저장 된 장르가 표시 되는지 확인 합니다. **StoreController** 는 이전과 동일한 엔터티를 반환 하기 때문에 뷰 템플릿을 변경할 필요가 없습니다. 하지만 이번에는 데이터가 데이터베이스에서 제공 됩니다.

1. 솔루션을 다시 빌드하고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. **장르** 메뉴가 더 이상 하드 코드 된 목록이 아닌지 확인 하 고 데이터가 데이터베이스에서 직접 검색 되는지 확인 합니다.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *데이터베이스에서 장르 검색*
3. 이제 장르로 이동 하 여 데이터베이스에서 앨범이 채워지는지 확인 합니다.

    ![데이터베이스에서 앨범 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image17.png "데이터베이스에서 앨범 찾아보기")

    *데이터베이스에서 앨범 찾아보기*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>연습 2: Code First을 사용 하 여 데이터베이스 만들기

이 연습에서는 MusicStore 응용 프로그램의 테이블을 사용 하 여 데이터베이스를 만드는 방법 및 해당 데이터에 액세스 하는 방법을 설명 Code First 합니다.

모델을 생성 한 후에는 하드 코드 된 값을 사용 하는 대신 데이터베이스에서 가져온 데이터를 사용 하 여 뷰 템플릿을 제공 하도록 StoreController를 수정 합니다.

> [!NOTE]
> 연습 1을 완료 하 고 이미 Database First 방식으로 작업 한 경우 다른 프로세스를 사용 하 여 동일한 결과를 얻는 방법을 배우게 됩니다. 실습 1과 관련 된 작업은 더 쉽게 읽을 수 있도록 표시 되어 있습니다. 연습 1을 완료 하지 않았지만 Code First 방법을 배우는 경우이 연습에서 시작 하 여 토픽의 전체 검사를 수행할 수 있습니다.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>작업 1-샘플 데이터 채우기

이 태스크에서는 처음 코드를 사용 하 여 만들 때 샘플 데이터를 사용 하 여 데이터베이스를 채웁니다.

1. **Source/Ex2-CreatingADatabaseCodeFirst/begin/** 폴더에 있는 **시작** 솔루션을 엽니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **모델** 폴더에 **SampleData.cs** 파일을 추가 합니다. 이렇게 하려면 **모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 를 가리킨 다음 **기존 항목**을 클릭 합니다. **\Source\sts\source\stl** 을 찾아 **SampleData.cs** 파일을 선택 합니다.

    ![샘플 데이터 채우기 코드](aspnet-mvc-4-models-and-data-access/_static/image18.png "샘플 데이터 채우기 코드")

    *샘플 데이터 채우기 코드*
3. **Global.asax.cs** 파일을 열고 다음 *using* 문을 추가 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Global Global.asax using*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. **응용 프로그램\_Start ()** 메서드에서 다음 줄을 추가 하 여 데이터베이스 이니셜라이저를 설정 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Global Global.asax SetInitializer*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>작업 2-데이터베이스에 대 한 연결 구성

프로젝트에 데이터베이스를 이미 추가 했으므로 이제는 web.config 파일에 연결 문자열을 **작성 합니다.**

1. **Web.config에 연결**문자열을 추가 합니다. 이렇게 하려면 프로젝트 루트에서 **web.config를 열고** defaultconnection 이라는 연결 문자열을 **&lt;connectionStrings&gt;** 섹션에서 다음 줄로 바꿉니다.

    ![Web.config 파일 위치](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 파일 위치")

    *Web.config 파일 위치*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>작업 3-모델 작업

데이터베이스에 대 한 연결을 이미 구성 했으므로 모델을 데이터베이스 테이블과 연결 합니다. 이 태스크에서는 Code First를 사용 하 여 데이터베이스에 연결 되는 클래스를 만듭니다. 수정 해야 하는 POCO 모델 클래스가 존재 한다는 점에 주의 해야 합니다.

> [!NOTE]
> 연습 1을 완료 한 경우 마법사에서이 단계를 수행 했는지 확인 합니다. Code First를 수행 하 여 데이터 엔터티에 연결 되는 클래스를 수동으로 만듭니다.

1. **모델** 프로젝트 폴더에서 POCO 모델 클래스 **장르** 를 열고 ID를 포함 합니다. 이름이 **GenreId**인 int 속성을 사용 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Code First 장르*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > Code First 규칙을 사용 하려면 클래스 장르에 자동으로 검색 되는 기본 키 속성이 있어야 합니다.
    > 
    > 이 [msdn 문서](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)에서 Code First 규칙에 대해 자세히 알아볼 수 있습니다.
2. 이제 **모델** 프로젝트 폴더에서 POCO 모델 클래스 **앨범** 을 열고 외래 키를 포함 하 고 이름이 **GenreId** 및 **ArtistId**인 속성을 만듭니다. 이 클래스에는 기본 키에 대 한 **GenreId** 이미 있습니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Code First 앨범*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. POCO 모델 클래스 **음악가** 를 열고 **ArtistId** 속성을 포함 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Code First 음악가*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. **모델** 프로젝트 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 클래스**. 파일 이름을 **MusicStoreEntities.cs**로 합니다. 그런 다음 추가를 클릭 **합니다.**

    ![클래스 추가](aspnet-mvc-4-models-and-data-access/_static/image20.png "클래스 추가")

    *새 항목 추가*

    ![Class2 추가](aspnet-mvc-4-models-and-data-access/_static/image21.png "Class2 추가")

    *클래스 추가*
5. 방금 만든 클래스를 **MusicStoreEntities.cs** **하 고 네임 스페이스** 를 포함 하 여 네임 스페이스를 **엽니다.**

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. **DbContext** 클래스를 확장 하도록 클래스 선언을 바꿉니다. Public **dbset** 을 선언 하 고 **onmodelcreating** 메서드를 재정의 합니다. 이 단계를 수행한 후에는 모델을 Entity Framework와 연결 하는 도메인 클래스를 받게 됩니다. 이렇게 하려면 클래스 코드를 다음 코드로 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 Code First MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> Entity Framework **DbContext** 및 **dbset** 를 사용 하면 POCO 클래스 장르를 쿼리할 수 있습니다. **Onmodelcreating** 메서드를 확장 하 여 **코드** 에서 장르를 데이터베이스 테이블에 매핑하는 방법을 지정 합니다. DBContext 및 DBSet에 대 한 자세한 내용은 msdn 문서 [링크](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx) 에서 찾을 수 있습니다.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>작업 4-데이터베이스 쿼리

이 작업에서는 하드 코드 된 데이터를 사용 하는 대신 데이터베이스에서 StoreController 클래스를 검색 하도록 업데이트 합니다.

> [!NOTE]
> 이 작업은 연습 1에서 일반적으로 사용 됩니다.
> 
> 연습 1을 완료 한 경우 이러한 단계는 두 방법 (데이터베이스 first 또는 Code first)에서 동일 합니다. 모델에 데이터를 연결 하는 방법은 다르지만 데이터 엔터티에 대 한 액세스는 컨트롤러에서 아직 투명 합니다.

1. **Controllers\StoreController.cs** 을 열고 클래스에 다음 필드를 추가 하 여 **Storedb**라는 **MusicStoreEntities** 클래스의 인스턴스를 포함 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities** 클래스는 데이터베이스의 각 테이블에 대 한 컬렉션 속성을 노출 합니다. 모든 **앨범이**포함 된 장르를 검색 하도록 **찾아보기** 작업 메서드를 업데이트 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 저장소 찾아보기*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > **LINQ** (언어 통합 쿼리) 라는 .net 기능을 사용 하 여 이러한 컬렉션에 대해 강력한 형식의 쿼리 식을 작성 합니다 .이 기능을 사용 하면 데이터베이스에 대해 코드를 실행 하 고 프로그래밍할 수 있는 개체를 반환 합니다.
    > 
    > LINQ에 대 한 자세한 내용은 [msdn 사이트](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)를 참조 하십시오.
3. **인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 저장소 인덱스*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. **인덱스** 작업 메서드를 업데이트 하 여 모든 장르를 검색 하 고 컬렉션을 목록으로 변환 합니다.

    (코드 조각- *모델 및 데이터 액세스-Ex2 저장소 GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>작업 5-응용 프로그램 실행

이 태스크에서는 저장소 인덱스 페이지에 하드 코드 된 항목이 아니라 데이터베이스에 저장 된 장르가 표시 되는지 확인 합니다. **StoreController** 가 이전 처럼 동일한 파일 **인덱스 viewmodel** 을 반환 하지만 이번에는 데이터를 데이터베이스에서 가져올 수 있으므로 뷰 템플릿을 변경할 필요가 없습니다.

1. 솔루션을 다시 빌드하고 **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. **장르** 메뉴가 더 이상 하드 코드 된 목록이 아닌지 확인 하 고 데이터가 데이터베이스에서 직접 검색 되는지 확인 합니다.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *데이터베이스에서 장르 검색*
3. 이제 장르로 이동 하 여 데이터베이스에서 앨범이 채워지는지 확인 합니다.

    ![데이터베이스에서 앨범 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image23.png "데이터베이스에서 앨범 찾아보기")

    *데이터베이스에서 앨범 찾아보기*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>연습 3: 매개 변수를 사용 하 여 데이터베이스 쿼리

이 연습에서는 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법 및 쿼리 결과 셰이핑을 사용 하는 방법에 대해 설명 합니다 .이 기능을 사용 하 여 데이터를 보다 효율적으로 검색 하는 데이터베이스 액세스를 줄일 수 있습니다.

> [!NOTE]
> 쿼리 결과 셰이핑에 대 한 자세한 내용은 다음 [msdn 문서](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)를 참조 하세요.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>작업 1-StoreController를 수정 하 여 데이터베이스에서 앨범 검색

이 작업에서는 데이터베이스에 액세스 하 여 특정 장르에서 앨범을 검색 하도록 **StoreController** 클래스를 변경 합니다.

1. 데이터베이스 우선 방법을 사용 하려는 경우에는 **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** 폴더에 있는 **Begin** solution를 엽니다. 여기서는 코드를 처음 사용 하거나 **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** 폴더를 사용 하려는 경우에 사용 합니다. 그렇지 않으면 이전 연습을 완료 하 여 얻은 **종료** 솔루션을 계속 사용할 수 있습니다.

   1. 제공 된 **시작** 솔루션을 연 경우 계속 하기 전에 일부 누락 된 NuGet 패키지를 다운로드 해야 합니다. 이렇게 하려면 **프로젝트** 메뉴를 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다.
   2. **NuGet 패키지 관리** 대화 상자에서 **복원** 을 클릭 하 여 누락 된 패키지를 다운로드 합니다.
   3. 마지막으로 **빌드** | **솔루션 빌드**를 클릭 하 여 솔루션을 빌드합니다.

      > [!NOTE]
      > NuGet을 사용 하는 경우의 장점 중 하나는 프로젝트의 모든 라이브러리를 제공 하 여 프로젝트 크기를 줄이는 것이 없다는 것입니다. NuGet 파워 도구를 사용 하 여 패키지 .config 파일에 패키지 버전을 지정 하면 프로젝트를 처음 실행할 때 필요한 모든 라이브러리를 다운로드할 수 있습니다. 이 경우이 랩에서 기존 솔루션을 연 후 이러한 단계를 실행 해야 합니다.
2. **StoreController** 클래스를 열어 **찾아보기** 동작 메서드를 변경 합니다. 이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.
3. **찾아보기** 동작 메서드를 변경 하 여 특정 장르의 앨범을 검색 합니다. 이렇게 하려면 다음 코드를 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-Ex3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> 엔터티 컬렉션을 채우려면 **Include** 메서드를 사용 하 여 앨범을 검색 하도록 지정 해야 합니다. 을 사용할 수 있습니다. **단일 () 확장 (** 이 경우에는 하나의 장르만 앨범에 필요 하기 때문입니다. **Single ()** 메서드는 람다 식을 매개 변수로 사용 합니다 .이 경우에는 이름이 정의 된 값과 일치 하도록 단일 장르 개체를 지정 합니다.
> 
> 장르 개체가 검색 될 때 로드 하려는 다른 관련 엔터티를 나타낼 수 있도록 하는 기능을 활용 합니다. 이 기능을 **쿼리 결과 셰이핑**이라고 하며,이를 통해 데이터베이스에 액세스 하 여 정보를 검색 하는 데 필요한 횟수를 줄일 수 있습니다. 이 시나리오에서는 검색 하는 장르에 대 한 앨범을 미리 인출 해야 합니다.
> 
> 이 쿼리에는 관련 앨범이 필요 함을 나타내는 **장르 (&quot;앨범&quot;)** 가 포함 되어 있습니다. 이렇게 하면 단일 데이터베이스 요청에서 장르 및 앨범 데이터를 모두 검색 하므로 더 효율적인 응용 프로그램이 생성 됩니다.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>작업 2-응용 프로그램 실행

이 태스크에서는 응용 프로그램을 실행 하 고 데이터베이스에서 특정 장르의 앨범을 검색 합니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을/Svs\uhhhhhhhhhhhhhi로 변경 하 여 데이터베이스에서 결과가 검색 되는지 확인 합니다.

    ![장르로 찾아보기](aspnet-mvc-4-models-and-data-access/_static/image24.png "장르로 찾아보기")

    *탐색/창/찾아보기? 장르 = Pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>작업 3-Id로 앨범 액세스

이 작업에서는 이전 절차를 반복 하 여 해당 Id로 앨범을 가져옵니다.

1. 필요한 경우 브라우저를 닫고 Visual Studio로 돌아갑니다. **StoreController** 클래스를 열어 **Details** 작업 메서드를 변경 합니다. 이렇게 하려면 **솔루션 탐색기**에서 **Controllers** 폴더를 확장 하 고 **StoreController.cs**를 두 번 클릭 합니다.
2. **세부 정보** 작업 메서드를 변경 하 여 해당 **Id**를 기반으로 하는 앨범 세부 정보를 검색 합니다. 이렇게 하려면 다음 코드를 바꿉니다.

    (코드 조각- *모델 및 데이터 액세스-Ex3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>작업 4-응용 프로그램 실행

이 작업에서는 웹 브라우저에서 응용 프로그램을 실행 하 고 Id를 기준으로 앨범 세부 정보를 가져옵니다.

1. **F5** 키를 눌러 응용 프로그램을 실행 합니다.
2. 프로젝트가 홈 페이지에서 시작 됩니다. URL을 **/Store/Details/51** 로 변경 하거나 장르를 검색 하 고 앨범을 선택 하 여 데이터베이스에서 결과가 검색 되는지 확인 합니다.

    ![검색 세부 정보](aspnet-mvc-4-models-and-data-access/_static/image25.png "검색 세부 정보")

    */Store/Details/51 찾아보기*

> [!NOTE]
> 또한 [부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시](#AppendixB)를 수행 하는 Windows Azure 웹 사이트에이 응용 프로그램을 배포할 수 있습니다.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 실습을 완료 하면 **Database First** 방법과 **Code First** 방법을 사용 하 여 ASP.NET MVC 모델 및 데이터 액세스의 기본 사항을 배웠습니다.

- 데이터를 사용 하기 위해 솔루션에 데이터베이스를 추가 하는 방법
- 하드 코드 된 데이터 대신 데이터베이스에서 가져온 데이터를 사용 하 여 뷰 템플릿을 제공 하도록 컨트롤러를 업데이트 하는 방법
- 매개 변수를 사용 하 여 데이터베이스를 쿼리 하는 방법
- 데이터베이스 액세스의 수를 줄이고 보다 효율적인 방식으로 데이터를 검색 하는 기능인 쿼리 결과 셰이핑을 사용 하는 방법
- Microsoft Entity Framework에서 Database First 및 Code First 접근 방법을 사용 하 여 데이터베이스를 모델과 연결 하는 방법

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>부록 A: 웹에 대 한 Visual Studio Express 2012 설치

**[Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)** 를 사용 하 여 웹 또는 다른 &quot;Express&quot; 버전 **에 대해 Microsoft Visual Studio Express 2012** 를 설치할 수 있습니다. 다음 지침에서는 *Microsoft 웹 플랫폼 설치 관리자*를 사용 하 여 *Visual studio Express 2012 for Web* 을 설치 하는 데 필요한 단계를 안내 합니다.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)로 이동 합니다. 또는 웹 플랫폼 설치 관리자를 이미 설치한 경우에는 웹 플랫폼 설치 관리자를 열고 <em>Microsoft AZURE SDK&quot;를 사용 하 여 웹 용 2012 Visual Studio Express</em> &quot;제품을 검색할 수 있습니다.
2. **지금 설치**를 클릭 합니다. **웹 플랫폼 설치 관리자** 가 없으면 먼저이를 다운로드 하 여 설치 하도록 리디렉션됩니다.
3. **웹 플랫폼 설치 관리자** 가 열리면 **설치** 를 클릭 하 여 설치를 시작 합니다.

    ![Visual Studio Express 설치](aspnet-mvc-4-models-and-data-access/_static/image26.png "Visual Studio Express 설치")

    *Visual Studio Express 설치*
4. 모든 제품의 라이선스 및 사용 조건을 읽고 **동의** 함을 클릭 하 여 계속 합니다.

    ![사용 조건 동의](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *사용 조건 동의*
5. 다운로드 및 설치 프로세스가 완료 될 때까지 기다립니다.

    ![설치 진행률](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *설치 진행률*
6. 설치가 완료 되 면 **마침**을 클릭 합니다.

    ![설치 완료](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *설치 완료*
7. **끝내기** 를 클릭 하 여 웹 플랫폼 설치 관리자를 닫습니다.
8. 웹에 대 한 Visual Studio Express를 열려면 **시작** 화면으로 이동 하 &quot;**VS Express**&quot;작성을 시작한 후 **VS Express for Web** 타일을 클릭 합니다.

    ![VS Express for Web 타일](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    *VS Express for Web 타일*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>부록 B: 웹 배포을 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

이 부록에서는 windows azure 관리 포털에서 새 웹 사이트를 만들고 랩에 따라 가져온 응용 프로그램을 게시 하 여 Windows Azure에서 제공 하는 웹 배포 게시 기능을 활용 하는 방법을 보여 줍니다.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>작업 1-Windows Azure 포털에서 새 웹 사이트 만들기

1. [Windows Azure 관리 포털](https://manage.windowsazure.com/) 로 이동 하 고 구독과 연결 된 Microsoft 자격 증명을 사용 하 여 로그인 합니다.

    > [!NOTE]
    > Windows Azure를 사용 하면 10 개의 ASP.NET 웹 사이트를 무료로 호스팅한 후 트래픽 증가에 따라 크기를 조정할 수 있습니다. [여기](https://aka.ms/aspnet-hol-azure)에서 등록할 수 있습니다.

    ![Windows Azure Portal에 로그온 합니다.](aspnet-mvc-4-models-and-data-access/_static/image31.png "Windows Azure Portal에 로그온 합니다.")

    *Windows Azure 관리 포털에 로그온 합니다.*
2. 명령 모음에서 **새로 만들기** 를 클릭 합니다.

    ![새 웹 사이트 만들기](aspnet-mvc-4-models-and-data-access/_static/image32.png "새 웹 사이트 만들기")

    *새 웹 사이트 만들기*
3. **Compute** | **웹 사이트**를 클릭 합니다. 그런 다음 **빠른 생성** 옵션을 선택 합니다. 새 웹 사이트에 사용할 수 있는 URL을 제공 하 고 **웹 사이트 만들기**를 클릭 합니다.

    > [!NOTE]
    > Microsoft Azure 웹 사이트는 사용자가 제어 하 고 관리할 수 있는 클라우드에서 실행 되는 웹 응용 프로그램에 대 한 호스트입니다. 빠른 생성 옵션을 사용 하면 포털 외부에서 Windows Azure 웹 사이트에 완료 된 웹 응용 프로그램을 배포할 수 있습니다. 데이터베이스를 설정 하는 단계는 포함 되지 않습니다.

    ![빠른 생성을 사용 하 여 새 웹 사이트 만들기](aspnet-mvc-4-models-and-data-access/_static/image33.png "빠른 생성을 사용 하 여 새 웹 사이트 만들기")

    *빠른 생성을 사용 하 여 새 웹 사이트 만들기*
4. 새 **웹 사이트가** 만들어질 때까지 기다립니다.
5. 웹 사이트를 만든 후 **URL** 열 아래의 링크를 클릭 합니다. 새 웹 사이트가 작동 하는지 확인 합니다.

    ![새 웹 사이트로 이동](aspnet-mvc-4-models-and-data-access/_static/image34.png "새 웹 사이트로 이동")

    *새 웹 사이트로 이동*

    ![웹 사이트 실행 중](aspnet-mvc-4-models-and-data-access/_static/image35.png "웹 사이트 실행 중")

    *웹 사이트 실행 중*
6. 포털로 돌아가서 **이름** 열 아래에 있는 웹 사이트의 이름을 클릭 하 여 관리 페이지를 표시 합니다.

    ![웹 사이트 관리 페이지 열기](aspnet-mvc-4-models-and-data-access/_static/image36.png "웹 사이트 관리 페이지 열기")

    *웹 사이트 관리 페이지 열기*
7. **대시보드** 페이지의 **빠른** 보기 섹션에서 **게시 프로필 다운로드** 링크를 클릭 합니다.

    > [!NOTE]
    > *게시 프로필* 에는 사용 하도록 설정 된 각 게시 방법에 대해 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하는 데 필요한 모든 정보가 포함 되어 있습니다. 게시 프로필에는 게시 방법이 사용 설정된 각 엔드포인트에 연결하고 이에 대해 인증하는 데 필요한 URL, 사용자 자격 증명 및 데이터베이스 문자열이 포함되어 있습니다. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** 및 **Microsoft Visual Studio 2012** 는 게시 프로필 읽기를 지원 하 여 웹 응용 프로그램을 Windows Azure 웹 사이트에 게시 하기 위해 이러한 프로그램의 구성을 자동화 합니다.

    ![웹 사이트 게시 프로필을 다운로드 하는 중](aspnet-mvc-4-models-and-data-access/_static/image37.png "웹 사이트 게시 프로필을 다운로드 하는 중")

    *웹 사이트 게시 프로필을 다운로드 하는 중*
8. 알려진 위치에 게시 프로필 파일을 다운로드 합니다. 이 연습을 통해이 파일을 사용 하 여 Visual Studio에서 Windows Azure 웹 사이트에 웹 응용 프로그램을 게시 하는 방법을 확인할 수 있습니다.

    ![게시 프로필 파일을 저장 하는 중](aspnet-mvc-4-models-and-data-access/_static/image38.png "게시 프로필을 저장 하는 중")

    *게시 프로필 파일을 저장 하는 중*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>작업 2-데이터베이스 서버 구성

응용 프로그램에서 SQL Server 데이터베이스를 사용 하는 경우 SQL Database 서버를 만들어야 합니다. SQL Server 사용 하지 않는 간단한 응용 프로그램을 배포 하려는 경우이 작업을 건너뛸 수 있습니다.

1. 응용 프로그램 데이터베이스를 저장 하기 위한 SQL Database 서버가 필요 합니다. Microsoft Azure 관리 포털의 구독에서 SQL Database 서버를 볼 수는 **SQL 데이터베이스** | **서버** | **서버의 대시보드**. 만든 서버가 없는 경우 명령 모음에서 **추가** 단추를 사용 하 여 만들 수 있습니다. 다음 작업에서 사용할 **서버 이름과 URL, 관리자 로그인 이름 및 암호**를 기록해 둡니다. 이후 단계에서 생성 되므로 아직 데이터베이스를 만들지 마십시오.

    ![SQL Database 서버 대시보드](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database 서버 대시보드")

    *SQL Database 서버 대시보드*
2. 다음 작업에서는 Visual Studio에서 데이터베이스 연결을 테스트 합니다. 따라서 서버에서 **허용 되는 Ip 주소**목록에 로컬 IP 주소를 포함 해야 합니다. 이렇게 하려면 **구성**을 클릭 하 고, **현재 클라이언트 IP 주소** 에서 ip 주소를 선택 하 고, **시작 Ip 주소** 및 **끝 ip 주소** 텍스트 상자에 붙여 넣고, ![추가-클라이언트-ip 주소-확인 단추](aspnet-mvc-4-models-and-data-access/_static/image40.png) 단추를 클릭 합니다.

    ![클라이언트 IP 주소를 추가 하는 중](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *클라이언트 IP 주소를 추가 하는 중*
3. **클라이언트 Ip 주소가** 허용 된 ip 주소 목록에 추가 되 면 **저장** 을 클릭 하 여 변경 내용을 확인 합니다.

    ![변경 내용 확인](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *변경 내용 확인*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>작업 3-웹 배포를 사용 하 여 ASP.NET MVC 4 응용 프로그램 게시

1. ASP.NET MVC 4 솔루션으로 돌아갑니다. **솔루션 탐색기**에서 웹 사이트 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

    ![응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image43.png "응용 프로그램 게시")

    *웹 사이트 게시*
2. 첫 번째 작업에서 저장 한 게시 프로필을 가져옵니다.

    ![게시 프로필을 가져오는 중](aspnet-mvc-4-models-and-data-access/_static/image44.png "게시 프로필을 가져오는 중")

    *게시 프로필을 가져오는 중*
3. **연결 유효성 검사**를 클릭 합니다. 유효성 검사가 완료 되 면 **다음**을 클릭 합니다.

    > [!NOTE]
    > 유효성 검사는 연결 유효성 검사 단추 옆에 녹색 확인 표시가 표시 되 면 완료 됩니다.

    ![연결 유효성 검사](aspnet-mvc-4-models-and-data-access/_static/image45.png "연결 유효성 검사")

    *연결 유효성 검사*
4. **설정** 페이지의 **데이터베이스** 섹션에서 데이터베이스 연결의 텍스트 상자 옆에 있는 단추 (즉, **defaultconnection**)를 클릭 합니다.

    ![웹 배포 구성](aspnet-mvc-4-models-and-data-access/_static/image46.png "웹 배포 구성")

    *웹 배포 구성*
5. 데이터베이스 연결을 다음과 같이 구성 합니다.

   - **서버 이름** 에 *tcp:* 접두사를 사용 하 여 SQL Database 서버 URL을 입력 합니다.
   - **사용자 이름** 에 서버 관리자 로그인 이름을 입력 합니다.
   - **암호** 에 서버 관리자 로그인 암호를 입력 합니다.
   - 새 데이터베이스 이름을 입력 합니다.

     ![대상 연결 문자열 구성](aspnet-mvc-4-models-and-data-access/_static/image47.png "대상 연결 문자열 구성")

     *대상 연결 문자열 구성*
6. 그런 후 **OK**를 클릭합니다. 데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

    ![데이터베이스 만들기](aspnet-mvc-4-models-and-data-access/_static/image48.png "데이터베이스 문자열 만들기")

    *데이터베이스 만들기*
7. Windows Azure에서 SQL Database에 연결 하는 데 사용할 연결 문자열은 기본 연결 텍스트 상자 내에 표시 됩니다. 그런 후 **Next** 를 클릭합니다.

    ![SQL Database를 가리키는 연결 문자열](aspnet-mvc-4-models-and-data-access/_static/image49.png "SQL Database를 가리키는 연결 문자열")

    *SQL Database를 가리키는 연결 문자열*
8. **미리 보기** 페이지에서 **게시**를 클릭 합니다.

    ![웹 응용 프로그램 게시](aspnet-mvc-4-models-and-data-access/_static/image50.png "웹 응용 프로그램 게시")

    *웹 응용 프로그램 게시*
9. 게시 프로세스가 완료 되 면 기본 브라우저가 게시 된 웹 사이트를 엽니다.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>부록 C: 코드 조각 사용

코드 조각을 사용 하면 필요한 모든 코드를 편리 하 게 사용할 수 있습니다. 랩 문서는 다음 그림에 표시 된 것 처럼 사용자가 사용할 수 있는 경우를 정확 하 게 알려줍니다.

![Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입](aspnet-mvc-4-models-and-data-access/_static/image51.png "Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입")

*Visual Studio 코드 조각을 사용 하 여 프로젝트에 코드 삽입*

***키보드를 사용 하 여 코드 조각을 추가 하려면C# (만 해당)***

1. 코드를 삽입할 위치에 커서를 놓습니다.
2. 조각 이름 (공백 또는 하이픈 제외)을 입력 하기 시작 합니다.
3. IntelliSense는 일치 하는 코드 조각의 이름을 표시 합니다.
4. 올바른 코드 조각을 선택 하거나 전체 코드 조각 이름이 선택 될 때까지 계속 입력 합니다.
5. Tab 키를 두 번 눌러 커서 위치에 코드 조각을 삽입 합니다.

![코드 조각 이름 입력 시작](aspnet-mvc-4-models-and-data-access/_static/image52.png "코드 조각 이름 입력 시작")

*코드 조각 이름 입력 시작*

![Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image53.png "Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.")

*Tab 키를 눌러 강조 표시 된 코드 조각을 선택 합니다.*

![Tab 키를 다시 누르면 코드 조각이 확장 됩니다.](aspnet-mvc-4-models-and-data-access/_static/image54.png "Tab 키를 다시 누르면 코드 조각이 확장 됩니다.")

*Tab 키를 다시 누르면 코드 조각이 확장 됩니다.*

***마우스C#(, Visual Basic 및 XML)를 사용 하 여 코드 조각을 추가 하려면*** 1(sp1). 코드 조각을 삽입 하려는 위치를 마우스 오른쪽 단추로 클릭 합니다.

1. 코드 **조각 삽입** 을 선택한 다음 **내 코드 조각을**선택 합니다.
2. 목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.

![코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image55.png "코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.")

*코드 조각을 삽입할 위치를 마우스 오른쪽 단추로 클릭 하 고 코드 조각 삽입을 선택 합니다.*

![목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.](aspnet-mvc-4-models-and-data-access/_static/image56.png "목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.")

*목록에서 관련 코드 조각을 클릭 하 여 선택 합니다.*
