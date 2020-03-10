---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
title: LINQ to SQL (C#)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 모델 c를 빌드하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f84b4a16-e8bb-49e8-87a0-1832879a3501
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-cs
msc.type: authoredcontent
ms.openlocfilehash: c27d1ffac3846fe4bc13b32c2ae91a63b2493126
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437189"
---
# <a name="creating-model-classes-with-linq-to-sql-c"></a>LINQ to SQL을 사용하여 모델 클래스 만들기(C#)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_CS.pdf)

> 이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 Microsoft LINQ to SQL를 활용 하 여 모델 클래스를 작성 하 고 데이터베이스 액세스를 수행 하는 방법에 대해 알아봅니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에 대 한 모델 클래스를 만드는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 Microsoft LINQ to SQL를 활용 하 여 모델 클래스를 작성 하 고 데이터베이스 액세스를 수행 하는 방법에 대해 알아봅니다.

이 자습서에서는 기본적인 영화 데이터베이스 응용 프로그램을 빌드합니다. 가능한 가장 빠르고 가장 쉬운 방법으로 영화 데이터베이스 응용 프로그램을 만드는 것부터 시작 합니다. Microsoft는 컨트롤러 작업에서 직접 모든 데이터 액세스를 수행 합니다.

다음으로, 리포지토리 패턴을 사용 하는 방법에 대해 알아봅니다. 리포지토리 패턴을 사용 하려면 약간 더 많은 작업이 필요 합니다. 그러나이 패턴을 도입 하면 변경할 수 있는 응용 프로그램을 빌드할 수 있으며 쉽게 테스트할 수 있다는 이점이 있습니다.

## <a name="what-is-a-model-class"></a>모델 클래스 란?

Mvc 모델에는 MVC 뷰나 MVC 컨트롤러에 포함 되지 않은 모든 응용 프로그램 논리가 포함 됩니다. 특히 MVC 모델은 모든 응용 프로그램 비즈니스 및 데이터 액세스 논리를 포함 합니다.

다양 한 기술을 사용 하 여 데이터 액세스 논리를 구현할 수 있습니다. 예를 들어 Microsoft Entity Framework, NHibernate 절전 모드, Subsonic 또는 ADO.NET 클래스를 사용 하 여 데이터 액세스 클래스를 빌드할 수 있습니다.

이 자습서에서는 LINQ to SQL를 사용 하 여 데이터베이스를 쿼리하고 업데이트 합니다. LINQ to SQL은 Microsoft SQL Server 데이터베이스와 손쉽게 상호 작용할 수 있는 방법을 제공 합니다. 그러나 ASP.NET MVC 프레임 워크는 어떤 방식으로든 LINQ to SQL 연결 되지 않는다는 것을 이해 하는 것이 중요 합니다. ASP.NET MVC는 모든 데이터 액세스 기술과 호환 됩니다.

## <a name="create-a-movie-database"></a>동영상 데이터베이스 만들기

이 자습서에서는 모델 클래스를 작성 하는 방법을 보여 주기 위해 간단한 영화 데이터베이스 응용 프로그램을 작성 합니다. 첫 번째 단계는 새 데이터베이스를 만드는 것입니다. 솔루션 탐색기 창에서 App\_Data 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다. **SQL Server 데이터베이스** 템플릿을 선택 하 고 이름을 MoviesDB로 지정한 다음 **추가** 단추를 클릭 합니다 (그림 1 참조).

[새 SQL Server 데이터베이스를 추가 ![](creating-model-classes-with-linq-to-sql-cs/_static/image2.png)](creating-model-classes-with-linq-to-sql-cs/_static/image1.png)

**그림 01**: 새 SQL Server 데이터베이스 추가 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image3.png))

새 데이터베이스를 만든 후에는 App\_Data 폴더에서 MoviesDB 파일을 두 번 클릭 하 여 데이터베이스를 열 수 있습니다. MoviesDB 파일을 두 번 클릭 하면 서버 탐색기 창이 열립니다 (그림 2 참조).

서버 탐색기 창은 Visual Web Developer를 사용할 때 데이터베이스 탐색기 창 이라고 합니다.

[서버 탐색기 창을 사용 하 ![](creating-model-classes-with-linq-to-sql-cs/_static/image5.png)](creating-model-classes-with-linq-to-sql-cs/_static/image4.png)

**그림 02**: 서버 탐색기 창 사용 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image6.png))

영화를 나타내는 테이블 하나를 데이터베이스에 추가 해야 합니다. Tables 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **새 테이블 추가**를 선택 합니다. 이 메뉴 옵션을 선택 하면 테이블 디자이너 열립니다 (그림 3 참조).

[서버 탐색기 창을 사용 하 ![](creating-model-classes-with-linq-to-sql-cs/_static/image8.png)](creating-model-classes-with-linq-to-sql-cs/_static/image7.png)

**그림 03**: 테이블 디자이너 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image9.png))

데이터베이스 테이블에 다음 열을 추가 해야 합니다.

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| Id | Int | False |
| 제목 | Nvarchar(200) | False |
| 감독 | Nvarchar(50) | False |

Id 열에 대 한 두 가지 특별 한 작업을 수행 해야 합니다. 먼저 테이블 디자이너에서 열을 선택 하 고 키 아이콘을 클릭 하 여 Id 열을 기본 키 열로 표시 해야 합니다. LINQ to SQL를 사용 하려면 데이터베이스에 대 한 삽입 또는 업데이트를 수행할 때 기본 키 열을 지정 해야 합니다.

그런 다음 예 값을 identity 속성에 할당 하 여 Id 열을 Id 열로 표시 **해야 합니다 (** 그림 3 참조). Id 열은 테이블에 새 데이터 행을 추가할 때마다 자동으로 새 번호가 할당 되는 열입니다.

## <a name="create-linq-to-sql-classes"></a>LINQ to SQL 클래스 만들기

MVC 모델에는 tblMovie 데이터베이스 테이블을 나타내는 LINQ to SQL 클래스가 포함 됩니다. 이러한 LINQ to SQL 클래스를 만드는 가장 쉬운 방법은 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 항목**을 차례로 선택한 다음 LINQ to SQL 클래스 템플릿을 선택 하 고 클래스 이름을 Movie로 지정 하 고 **추가** 단추를 클릭 합니다 (그림 4 참조).

[LINQ to SQL 클래스 ![만들기](creating-model-classes-with-linq-to-sql-cs/_static/image11.png)](creating-model-classes-with-linq-to-sql-cs/_static/image10.png)

**그림 04**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image12.png))

동영상 LINQ to SQL 클래스를 만든 직후에 개체 관계형 디자이너 표시 됩니다. 서버 탐색기 창에서 개체 관계형 디자이너로 데이터베이스 테이블을 끌어 특정 데이터베이스 테이블을 나타내는 LINQ to SQL 클래스를 만들 수 있습니다. 개체 관계형 디자이너에 tblMovie 데이터베이스 테이블을 추가 해야 합니다 (그림 5 참조).

[개체 관계형 디자이너를 사용 하 여 ![](creating-model-classes-with-linq-to-sql-cs/_static/image14.png)](creating-model-classes-with-linq-to-sql-cs/_static/image13.png)

**그림 05**: 개체 관계형 디자이너 사용 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image15.png))

기본적으로 개체 관계형 디자이너는 디자이너로 끌어 온 데이터베이스 테이블과 동일한 이름을 가진 클래스를 만듭니다. 그러나 `tblMovie`클래스를 호출 하지 않으려고 합니다. 따라서 디자이너에서 클래스의 이름을 클릭 하 고 클래스의 이름을 Movie로 변경 합니다.

마지막으로 **저장** 단추 (플로피 그림)를 클릭 하 여 LINQ to SQL 클래스를 저장 해야 합니다. 그렇지 않으면 개체 관계형 디자이너에서 LINQ to SQL 클래스가 생성 되지 않습니다.

## <a name="using-linq-to-sql-in-a-controller-action"></a>컨트롤러 작업에서 LINQ to SQL 사용

이제 LINQ to SQL 클래스가 있으므로 이러한 클래스를 사용 하 여 데이터베이스에서 데이터를 검색할 수 있습니다. 이 섹션에서는 컨트롤러 작업 내에서 직접 LINQ to SQL 클래스를 사용 하는 방법에 대해 알아봅니다. MVC 뷰에서 tblMovies 데이터베이스 테이블의 영화 목록을 표시 합니다.

먼저 HomeController 클래스를 수정 해야 합니다. 이 클래스는 응용 프로그램의 Controllers 폴더에서 찾을 수 있습니다. 클래스를 수정 하 여 목록 1의 클래스 처럼 보이도록 합니다.

**목록 1 – `Controllers\HomeController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample1.cs)]

목록 1의 `Index()` 동작은 LINQ to SQL DataContext 클래스 (`MovieDataContext`)를 사용 하 여 `MoviesDB` 데이터베이스를 나타냅니다. `MoveDataContext` 클래스는 Visual Studio 개체 관계형 디자이너에 의해 생성 되었습니다.

`tblMovies` 데이터베이스 테이블에서 모든 영화를 검색 하기 위해 DataContext에 대해 LINQ 쿼리를 수행 합니다. 동영상 목록은 `movies`이라는 지역 변수에 할당 됩니다. 마지막으로, 영화 목록이 보기 데이터를 통해 뷰로 전달 됩니다.

영화를 표시 하려면 다음으로 인덱스 뷰를 수정 해야 합니다. 인덱스 뷰는 `Views\Home\` 폴더에서 찾을 수 있습니다. 목록 2의 뷰와 비슷하게 보이도록 인덱스 뷰를 업데이트 합니다.

**목록 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample2.aspx)]

수정 된 인덱스 뷰에는 뷰의 맨 위에 `<%@ import namespace %>` 지시문이 포함 되어 있습니다. 이 지시문은 `MvcApplication1.Models namespace`를 가져옵니다. 이 네임 스페이스는 `model` 클래스 (특히 뷰에서 `Movie` 클래스)를 사용 하기 위해 필요 합니다.

목록 2의 뷰에는 `ViewData.Model` 속성이 나타내는 모든 항목을 반복 하는 `foreach` 루프가 포함 되어 있습니다. `Title` 속성의 값은 각 `movie`에 대해 표시 됩니다.

`ViewData.Model` 속성의 값은 `IEnumerable`으로 캐스팅 됩니다. 이는 `ViewData.Model`의 콘텐츠를 반복 하기 위해 필요 합니다. 여기에 있는 다른 옵션은 강력한 형식의 `view`를 만드는 것입니다. 강력한 형식의 `view`를 만들 때 `ViewData.Model` 속성을 뷰의 코드 숨김이 지정 된 클래스의 특정 형식으로 캐스팅 합니다.

`HomeController` 클래스 및 인덱스 뷰를 수정한 후 응용 프로그램을 실행 하면 빈 페이지가 나타납니다. `tblMovies` 데이터베이스 테이블에 영화 레코드가 없기 때문에 빈 페이지를 가져옵니다.

`tblMovies` 데이터베이스 테이블에 레코드를 추가 하려면 서버 탐색기 창에서 `tblMovies` 데이터베이스 테이블 (Visual Web Developer의 데이터베이스 탐색기 창)을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 테이블 데이터 표시를 선택 합니다. 표시 되는 그리드를 사용 하 여 `movie` 레코드를 삽입할 수 있습니다 (그림 6 참조).

[영화 삽입 ![](creating-model-classes-with-linq-to-sql-cs/_static/image17.png)](creating-model-classes-with-linq-to-sql-cs/_static/image16.png)

**그림 06**: 동영상 삽입 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image18.png))

`tblMovies` 테이블에 일부 데이터베이스 레코드를 추가 하 고 응용 프로그램을 실행 하면 그림 7에 페이지가 표시 됩니다. 모든 동영상 데이터베이스 레코드는 글머리 기호 목록에 표시 됩니다.

[인덱스 뷰를 사용 하 여 영화를 표시 ![](creating-model-classes-with-linq-to-sql-cs/_static/image20.png)](creating-model-classes-with-linq-to-sql-cs/_static/image19.png)

**그림 07**: 인덱스 뷰를 사용 하 여 동영상 표시 ([전체 크기 이미지를 보려면 클릭](creating-model-classes-with-linq-to-sql-cs/_static/image21.png))

## <a name="using-the-repository-pattern"></a>리포지토리 패턴 사용

이전 섹션에서는 컨트롤러 작업 내에서 직접 클래스 LINQ to SQL 사용 했습니다. `Index()` 컨트롤러 작업에서 직접 `MovieDataContext` 클래스를 사용 했습니다. 간단한 응용 프로그램의 경우에는이 작업을 수행 하는 것과 관련 된 문제가 없습니다. 그러나 컨트롤러 클래스에서 LINQ to SQL를 직접 사용 하면 좀 더 복잡 한 응용 프로그램을 빌드해야 할 때 문제가 발생 합니다.

컨트롤러 클래스 내에서 LINQ to SQL를 사용 하면 나중에 데이터 액세스 기술을 전환 하기가 어려워집니다. 예를 들어 Microsoft LINQ to SQL를 사용 하 여 Microsoft Entity Framework를 데이터 액세스 기술로 사용 하도록 전환할 수 있습니다. 이 경우 응용 프로그램 내에서 데이터베이스에 액세스 하는 모든 컨트롤러를 다시 작성 해야 합니다.

또한 컨트롤러 클래스 내에서 LINQ to SQL를 사용 하면 응용 프로그램에 대 한 단위 테스트를 빌드하기 어려워집니다. 일반적으로 단위 테스트를 수행할 때 데이터베이스와 상호 작용 하지 않으려고 합니다. 단위 테스트를 사용 하 여 데이터베이스 서버가 아닌 응용 프로그램 논리를 테스트 하려고 합니다.

향후 변경에 더 많은 도움이 되 고 더 쉽게 테스트할 수 있는 MVC 응용 프로그램을 빌드하기 위해 리포지토리 패턴을 사용 하는 것이 좋습니다. 리포지토리 패턴을 사용 하는 경우 모든 데이터베이스 액세스 논리를 포함 하는 별도의 리포지토리 클래스를 만듭니다.

리포지토리 클래스를 만들 때 리포지토리 클래스에서 사용 하는 모든 메서드를 나타내는 인터페이스를 만듭니다. 컨트롤러 내에서 리포지토리 대신 인터페이스에 대해 코드를 작성 합니다. 이렇게 하면 나중에 다른 데이터 액세스 기술을 사용 하 여 리포지토리를 구현할 수 있습니다.

목록 3의 인터페이스는 `IMovieRepository` 이름이 지정 되 고 `ListAll()`라는 단일 메서드를 나타냅니다.

**목록 3 – `Models\IMovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample3.cs)]

목록 4의 리포지토리 클래스는 `IMovieRepository` 인터페이스를 구현 합니다. 여기에는 `IMovieRepository` 인터페이스에 필요한 메서드에 해당 하는 `ListAll()` 라는 메서드가 포함 되어 있습니다.

**목록 4 – `Models\MovieRepository.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample4.cs)]

마지막으로 목록 5의 `MoviesController` 클래스는 리포지토리 패턴을 사용 합니다. 더 이상 LINQ to SQL 클래스를 직접 사용 하지 않습니다.

**목록 5 – `Controllers\MoviesController.cs`**

[!code-csharp[Main](creating-model-classes-with-linq-to-sql-cs/samples/sample5.cs)]

목록 5의 `MoviesController` 클래스에는 두 개의 생성자가 있습니다. 매개 변수가 없는 생성자 인 첫 번째 생성자는 응용 프로그램이 실행 될 때 호출 됩니다. 이 생성자는 `MovieRepository` 클래스의 인스턴스를 만들고 두 번째 생성자에 전달 합니다.

두 번째 생성자에는 단일 매개 변수 `IMovieRepository` 매개 변수가 있습니다. 이 생성자는 매개 변수의 값을 `_repository`이라는 클래스 수준 필드에 할당 하기만 합니다.

`MoviesController` 클래스는 종속성 주입 패턴 이라는 소프트웨어 디자인 패턴을 활용 합니다. 특히 생성자 종속성 주입 이라고 하는 항목을 사용 합니다. Martin Fowler에서 다음 문서를 참조 하 여이 패턴에 대해 자세히 알아볼 수 있습니다.

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

`MoviesController` 클래스 (첫 번째 생성자 제외)의 모든 코드는 실제 `MovieRepository` 클래스 대신 `IMovieRepository` 인터페이스와 상호 작용 합니다. 이 코드는 인터페이스의 구체적인 구현 대신 추상 인터페이스와 상호 작용 합니다.

응용 프로그램에서 사용 하는 데이터 액세스 기술을 수정 하려면 대체 데이터베이스 액세스 기술을 사용 하는 클래스로 `IMovieRepository` 인터페이스를 구현 하기만 하면 됩니다. 예를 들어 `EntityFrameworkMovieRepository` 클래스 또는 `SubSonicMovieRepository` 클래스를 만들 수 있습니다. 컨트롤러 클래스는 인터페이스에 대해 프로그래밍 되므로 `IMovieRepository`의 새 구현을 컨트롤러 클래스에 전달할 수 있으며 클래스는 계속 작동 합니다.

또한 `MoviesController` 클래스를 테스트 하려는 경우에는 가짜 영화 리포지토리 클래스를 `HomeController`에 전달할 수 있습니다. 실제로 데이터베이스에 액세스 하지는 않지만 `IMovieRepository` 인터페이스의 모든 필수 메서드를 포함 하는 클래스를 사용 하 여 `IMovieRepository` 클래스를 구현할 수 있습니다. 이렇게 하면 실제 데이터베이스에 실제로 액세스 하지 않고도 `MoviesController` 클래스를 단위 테스트할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 Microsoft LINQ to SQL를 활용 하 여 MVC 모델 클래스를 만드는 방법을 보여 주기 위한 것입니다. ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터를 표시 하기 위한 두 가지 전략을 검토 했습니다. 먼저 LINQ to SQL 클래스를 만들고 컨트롤러 작업 내에서 직접 클래스를 사용 했습니다. 컨트롤러 내에서 LINQ to SQL 클래스를 사용 하면 MVC 응용 프로그램에서 데이터베이스 데이터를 빠르고 쉽게 표시할 수 있습니다.

다음에는 데이터베이스 데이터를 표시 하는 데 필요한 약간 더 어렵고 고리가 만들어집니다의 경로를 살펴보았습니다. 리포지토리 패턴을 활용 하 고 모든 데이터베이스 액세스 논리를 별도의 리포지토리 클래스에 배치 했습니다. 이 컨트롤러에서는 구체적인 클래스 대신 인터페이스에 대 한 모든 코드를 작성 했습니다. 리포지토리 패턴의 장점은 나중에 데이터베이스 액세스 기술을 쉽게 변경 하 고 컨트롤러 클래스를 쉽게 테스트할 수 있다는 것입니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-the-entity-framework-cs.md)
> [다음](displaying-a-table-of-database-data-cs.md)
