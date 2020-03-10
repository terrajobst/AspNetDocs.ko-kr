---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: Entity Framework (C#)를 사용 하 여 모델 클래스 만들기 | Microsoft Docs
author: microsoft
description: 이 자습서에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다. 엔터티 마법사를 사용 하 여 ADO.NET 엔터티 Da를 만드는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469439"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a>Entity Framework를 사용하여 모델 클래스 만들기(C#)

[Microsoft](https://github.com/microsoft) 에서

> 이 자습서에서는 Microsoft Entity Framework에서 ASP.NET MVC를 사용 하는 방법에 대해 알아봅니다. 엔터티 마법사를 사용 하 여 ADO.NET 엔터티 데이터 모델을 만드는 방법에 대해 알아봅니다. 이 자습서에서는 Entity Framework를 사용 하 여 데이터베이스 데이터를 선택, 삽입, 업데이트 및 삭제 하는 방법을 보여 주는 웹 응용 프로그램을 작성 합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램을 빌드할 때 Microsoft Entity Framework를 사용 하 여 데이터 액세스 클래스를 만드는 방법을 설명 하는 것입니다. 이 자습서에서는 Microsoft Entity Framework에 대해 이전에 알지 못하는 것으로 가정 합니다. 이 자습서를 마치면 Entity Framework를 사용 하 여 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제 하는 방법을 이해할 수 있습니다.

Microsoft Entity Framework는 데이터베이스에서 자동으로 데이터 액세스 계층을 생성할 수 있도록 하는 O/RM (개체 관계형 매핑) 도구입니다. Entity Framework를 사용 하면 데이터 액세스 클래스를 직접 빌드하는 지루한 작업을 피할 수 있습니다.

ASP.NET MVC와 함께 Microsoft Entity Framework를 사용 하는 방법을 설명 하기 위해 간단한 샘플 응용 프로그램을 빌드합니다. 동영상 데이터베이스 레코드를 표시 하 고 편집할 수 있는 동영상 데이터베이스 응용 프로그램을 만듭니다.

이 자습서에서는 Visual Studio 2008 또는 Visual Web Developer 2008 서비스 팩 1이 있다고 가정 합니다. Entity Framework를 사용 하려면 서비스 팩 1이 필요 합니다. 다음 주소에서 Visual Studio 2008 서비스 팩 1 또는 Visual Web Developer 서비스 팩 1을 다운로드할 수 있습니다.

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> ASP.NET MVC와 Microsoft Entity Framework 사이에는 필수적으로 연결 되어 있지 않습니다. ASP.NET MVC에서 사용할 수 있는 Entity Framework에 대 한 몇 가지 대안이 있습니다. 예를 들어 Microsoft LINQ to SQL, NHibernate 절전 모드 또는 SubSonic 같은 다른 O/RM 도구를 사용 하 여 MVC 모델 클래스를 빌드할 수 있습니다.

## <a name="creating-the-movie-sample-database"></a>Movie 샘플 데이터베이스 만들기

Movie 데이터베이스 응용 프로그램은 다음 열을 포함 하는 Movie 라는 데이터베이스 테이블을 사용 합니다.

| 열 이름 | 데이터 형식 | Null을 허용 하 시겠습니까? | 기본 키 인가요? |
| --- | --- | --- | --- |
| Id | int | False | True |
| 제목 | nvarchar(100) | False | False |
| 감독 | nvarchar(100) | False | False |

다음 단계를 수행 하 여이 테이블을 ASP.NET MVC 프로젝트에 추가할 수 있습니다.

1. 솔루션 탐색기 창에서 App\_Data 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을 차례로 선택 합니다.**
2. **새 항목 추가** 대화 상자에서 **SQL Server database**를 선택 하 고 데이터베이스 이름을 MoviesDB로 지정한 다음 **추가** 단추를 클릭 합니다.
3. MoviesDB 파일을 두 번 클릭 하 여 서버 탐색기/데이터베이스 탐색기 창을 엽니다.
4. MoviesDB 데이터베이스 연결을 확장 하 고 Tables 폴더를 마우스 오른쪽 단추로 클릭 한 다음 메뉴 옵션 **새 테이블 추가**를 선택 합니다.
5. 테이블 디자이너에서 Id, 제목 및 감독 열을 추가 합니다.
6. **저장** 단추 (플로피 아이콘이 있음)를 클릭 하 여 새 테이블을 이름으로 저장 합니다.

동영상 데이터베이스 테이블을 만든 후에는 테이블에 몇 가지 샘플 데이터를 추가 해야 합니다. 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **테이블 데이터 표시**를 선택 합니다. 표시 되는 표에 가짜 영화 데이터를 입력할 수 있습니다.

## <a name="creating-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 만들기

Entity Framework을 사용 하려면 엔터티 데이터 모델를 만들어야 합니다. Visual Studio *엔터티 데이터 모델 마법사* 를 사용 하 여 데이터베이스에서 엔터티 데이터 모델를 자동으로 생성할 수 있습니다.

다음 단계를 수행하세요.

1. 솔루션 탐색기 창의 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.
2. **새 항목 추가** 대화 상자에서 데이터 범주를 선택 합니다 (그림 1 참조).
3. **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 하 고 이름을 MoviesDBModel에 엔터티 데이터 모델 지정 하 고 **추가** 단추를 클릭 합니다. **추가** 단추를 클릭 하면 데이터 모델 마법사가 시작 됩니다.
4. **모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택 하 고 **다음** 단추를 클릭 합니다 (그림 2 참조).
5. **데이터 연결 선택** 단계에서 MoviesDB 데이터베이스 연결을 선택 하 고, 엔터티 연결 설정 이름 MoviesDBEntities을 입력 하 고, **다음** 단추를 클릭 합니다 (그림 3 참조).
6. **데이터베이스 개체 선택** 단계에서 동영상 데이터베이스 테이블을 선택 하 고 **마침** 단추를 클릭 합니다 (그림 4 참조).

이러한 단계를 완료 한 후에는 Entity Designer (ADO.NET 엔터티 데이터 모델 Designer)가 열립니다.

**그림 1-새 엔터티 데이터 모델 만들기**

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

**그림 2-모델 콘텐츠 선택 단계**

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

**그림 3-데이터 연결 선택**

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

**그림 4-데이터베이스 개체 선택**

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a>ADO.NET 엔터티 데이터 모델 수정

엔터티 데이터 모델를 만든 후 Entity Designer를 활용 하 여 모델을 수정할 수 있습니다 (그림 5 참조). 솔루션 탐색기 창 내의 모델 폴더에 포함 된 MoviesDBModel 파일을 두 번 클릭 하 여 언제 든 지 Entity Designer을 열 수 있습니다.

**그림 5-ADO.NET 엔터티 데이터 모델 디자이너**

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

예를 들어 Entity Designer를 사용 하 여 엔터티 모델 데이터 마법사에서 생성 하는 클래스의 이름을 변경할 수 있습니다. 마법사에서 영화 라는 새 데이터 액세스 클래스를 만들었습니다. 즉, 마법사에서 클래스에 데이터베이스 테이블과 동일한 이름을 제공 했습니다. 이 클래스를 사용 하 여 특정 영화 인스턴스를 나타내기 때문에 클래스의 이름을 영화에서 동영상으로 바꾸어야 합니다.

엔터티 클래스의 이름을 바꾸려면 Entity Designer의 클래스 이름을 두 번 클릭 하 고 새 이름을 입력 합니다 (그림 6 참조). 또는 Entity Designer에서 엔터티를 선택한 후 속성 창의 엔터티 이름을 변경할 수 있습니다.

**그림 6-엔터티 이름 변경**

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

저장 단추 (플로피 디스크 아이콘)를 클릭 하 여 수정한 후에 엔터티 데이터 모델을 저장 해야 합니다. Entity Designer는 내부적으로 C# 클래스 집합을 생성 합니다. 솔루션 탐색기 창에서 MoviesDBModel.Designer.cs 파일을 열어 이러한 클래스를 볼 수 있습니다.

Designer.cs 파일에서 코드를 수정 하지 마세요. 다음에 Entity Designer를 사용할 때 변경 내용을 덮어씁니다. Designer.cs 파일에 정의 된 엔터티 클래스의 기능을 확장 하려는 경우에는 개별 파일에 *partial 클래스* 를 만들 수 있습니다.

#### <a name="selecting-database-records-with-the-entity-framework"></a>Entity Framework를 사용 하 여 데이터베이스 레코드 선택

영화 레코드 목록을 표시 하는 페이지를 만들어 영화 데이터베이스 응용 프로그램 빌드를 시작 해 보겠습니다. 목록 1의 홈 컨트롤러는 Index () 라는 동작을 노출 합니다. Index () 작업은 Entity Framework를 활용 하 여 Movie 데이터베이스 테이블의 모든 동영상 레코드를 반환 합니다.

**목록 1 – Controllers\ homecontroller.cs**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

1을 나열 하는 컨트롤러에는 생성자가 포함 되어 있습니다. 생성자는 \_db 라는 클래스 수준 필드를 초기화 합니다. \_db 필드는 Microsoft Entity Framework에서 생성 된 데이터베이스 엔터티를 나타냅니다. \_db 필드는 Entity Designer 생성 된 MoviesDBEntities 클래스의 인스턴스입니다.

Home 컨트롤러에서 theMoviesDBEntities 클래스를 사용 하려면 MovieEntityApp 네임 스페이스 (*Mvcprojectname*)를 가져와야 합니다. 모델).

\_db 필드는 Index () 작업 내에서 영화 데이터베이스 테이블의 레코드를 검색 하는 데 사용 됩니다. 식 \_db입니다. MovieSet는 동영상 데이터베이스 테이블의 모든 레코드를 나타냅니다. ToList () 메서드를 사용 하 여 동영상 집합을 동영상 개체의 제네릭 컬렉션 (목록&lt;동영상&gt;)으로 변환할 수 있습니다.

동영상 레코드는 LINQ to Entities의 도움을 통해 검색 됩니다. 목록 1의 Index () 동작은 LINQ *메서드 구문을* 사용 하 여 데이터베이스 레코드 집합을 검색 합니다. 원하는 경우 LINQ *쿼리 구문을* 대신 사용할 수 있습니다. 다음 두 문은 동일한 작업을 수행 합니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

가장 직관적인 LINQ 구문 (메서드 구문 또는 쿼리 구문)을 사용 합니다. 두 방법의 성능 차이는 없습니다. 유일한 차이점은 스타일입니다.

목록 2의 뷰는 영화 레코드를 표시 하는 데 사용 됩니다.

**목록 2 – Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

목록 2의 뷰에는 각 영화 레코드를 반복 하 고 영화 레코드의 제목 및 감독 속성 값을 표시 하는 **foreach** 루프가 포함 되어 있습니다. 그러면 각 레코드 옆에 편집 및 삭제 링크가 표시 됩니다. 또한 보기의 아래쪽에 영화 추가 링크가 표시 됩니다 (그림 7 참조).

**그림 7-인덱스 뷰**

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

인덱스 뷰는 형식화 된 *뷰입니다*. 인덱스 뷰에는 모델 속성을 Movie 개체의 강력한 형식의 제네릭 목록 컬렉션 (목록&lt;Movie)로 캐스팅 하는 *Inherits* 특성이 있는 &lt;% @ Page%&gt; 지시어가 포함 되어 있습니다.

## <a name="inserting-database-records-with-the-entity-framework"></a>Entity Framework를 사용 하 여 데이터베이스 레코드 삽입

Entity Framework를 사용 하 여 데이터베이스 테이블에 새 레코드를 쉽게 삽입할 수 있습니다. 목록 3에는 새 레코드를 Movie 데이터베이스 테이블에 삽입 하는 데 사용할 수 있는 새 작업 두 개가 홈 컨트롤러 클래스에 추가 되었습니다.

**목록 3 – Controllers\ homecontroller.cs (메서드 추가)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

첫 번째 Add () 작업은 단순히 뷰를 반환 합니다. 이 보기에는 새 동영상 데이터베이스 레코드를 추가 하기 위한 양식이 포함 되어 있습니다 (그림 8 참조). 양식을 제출 하면 두 번째 Add () 동작이 호출 됩니다.

두 번째 Add () 동작은 AcceptVerbs 특성으로 데코 레이트 됩니다. HTTP POST 작업을 수행 하는 경우에만이 작업을 호출할 수 있습니다. 즉, HTML 폼을 게시할 때만이 작업을 호출할 수 있습니다.

두 번째 Add () 작업은 ASP.NET MVC TryUpdateModel () 메서드를 사용 하 여 Entity Framework Movie 클래스의 새 인스턴스를 만듭니다. TryUpdateModel () 메서드는 Add () 메서드에 전달 되는 FormCollection의 필드를 사용 하 고 이러한 HTML 양식 필드의 값을 Movie 클래스에 할당 합니다.

Entity Framework 사용 하는 경우 TryUpdateModel 또는 UpdateModel 메서드를 사용 하 여 엔터티 클래스의 속성을 업데이트할 때 속성의 "백서"를 제공 해야 합니다.

그런 다음 추가 () 작업은 몇 가지 간단한 폼 유효성 검사를 수행 합니다. 작업은 Title 및 Director 속성 모두에 값이 있는지 확인 합니다. 유효성 검사 오류가 있는 경우 유효성 검사 오류 메시지가 ModelState에 추가 됩니다.

유효성 검사 오류가 없으면 Entity Framework의 도움을 사용 하 여 새 동영상 레코드가 동영상 데이터베이스 테이블에 추가 됩니다. 새 레코드는 다음 두 줄의 코드를 사용 하 여 데이터베이스에 추가 됩니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

코드의 첫 번째 줄은 Entity Framework에서 추적 하는 동영상 집합에 새 동영상 엔터티를 추가 합니다. 코드의 두 번째 줄에는 다시 기본 데이터베이스로 추적 되는 동영상의 모든 변경 내용이 저장 됩니다.

**그림 8-추가 뷰**

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a>Entity Framework를 사용 하 여 데이터베이스 레코드 업데이트

거의 동일한 방법으로 Entity Framework를 사용 하 여 데이터베이스 레코드를 편집 하 여 새 데이터베이스 레코드를 삽입할 수 있습니다. 목록 4에는 Edit () 라는 두 개의 새로운 컨트롤러 작업이 포함 되어 있습니다. 첫 번째 Edit () 작업은 동영상 레코드를 편집 하기 위한 HTML 폼을 반환 합니다. 두 번째 Edit () 작업은 데이터베이스 업데이트를 시도 합니다.

**목록 4 – Controllers\ homecontroller.cs (Edit 메서드)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

두 번째 Edit () 작업은 편집 중인 동영상의 Id와 일치 하는 데이터베이스에서 영화 레코드를 검색 하 여 시작 합니다. 다음 LINQ to Entities 문은 특정 Id와 일치 하는 첫 번째 데이터베이스 레코드를 가져와 합니다.

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

그런 다음 TryUpdateModel () 메서드를 사용 하 여 HTML 양식 필드의 값을 movie 엔터티의 속성에 할당 합니다. 업데이트할 정확한 속성을 지정 하기 위해 흰색 목록이 제공 됩니다.

그런 다음, 영화 제목 및 감독 속성 모두에 값이 있는지 확인 하기 위해 몇 가지 간단한 유효성 검사가 수행 됩니다. 속성 중 하나에 값이 없는 경우 유효성 검사 오류 메시지가 ModelState 및 ModelState에 추가 됩니다. IsValid는 false 값을 반환 합니다.

마지막으로 유효성 검사 오류가 없는 경우에는 SaveChanges () 메서드를 호출 하 여 기본 영화 데이터베이스 테이블이 변경 내용으로 업데이트 됩니다.

데이터베이스 레코드를 편집할 때 데이터베이스 업데이트를 수행 하는 컨트롤러 작업에 편집 중인 레코드의 Id를 전달 해야 합니다. 그렇지 않으면 컨트롤러 작업은 기본 데이터베이스에서 업데이트할 레코드를 알 수 없습니다. 목록 5에 포함 된 편집 뷰는 편집 중인 데이터베이스 레코드의 Id를 나타내는 숨겨진 양식 필드를 포함 합니다.

**목록 5 – Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>Entity Framework를 사용 하 여 데이터베이스 레코드 삭제

이 자습서에서 작업 해야 하는 최종 데이터베이스 작업은 데이터베이스 레코드를 삭제 하는 것입니다. 목록 6의 컨트롤러 작업을 사용 하 여 특정 데이터베이스 레코드를 삭제할 수 있습니다.

**목록 6--\Controllers\HomeController.cs (Delete 동작)**

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

Delete () 작업은 먼저 작업에 전달 된 Id와 일치 하는 영화 엔터티를 검색 합니다. 다음으로, DeleteObject () 메서드를 호출한 다음 SaveChanges () 메서드를 호출 하 여 데이터베이스에서 동영상이 삭제 됩니다. 마지막으로 사용자가 인덱스 뷰로 다시 리디렉션됩니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 및 Microsoft Entity Framework를 활용 하 여 데이터베이스 기반 웹 응용 프로그램을 빌드하는 방법을 보여 주는 것 이었습니다. 데이터베이스 레코드를 선택, 삽입, 업데이트 및 삭제할 수 있는 응용 프로그램을 빌드하는 방법을 배웠습니다.

먼저 엔터티 데이터 모델 마법사를 사용 하 여 Visual Studio 내에서 엔터티 데이터 모델을 생성 하는 방법에 대해 설명 했습니다. 다음으로 LINQ to Entities를 사용 하 여 데이터베이스 테이블에서 데이터베이스 레코드 집합을 검색 하는 방법에 대해 알아봅니다. 마지막으로, Entity Framework를 사용 하 여 데이터베이스 레코드를 삽입, 업데이트 및 삭제 했습니다.

> [!div class="step-by-step"]
> [다음](creating-model-classes-with-linq-to-sql-cs.md)
