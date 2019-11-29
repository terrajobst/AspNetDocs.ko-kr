---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 데이터베이스 데이터의 테이블 표시 (VB) | Microsoft Docs
author: microsoft
description: 이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법을 보여 줍니다. HTML ta에서 데이터베이스 레코드 집합의 형식을 지정 하는 두 가지 방법을 보여 줍니다.
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590851"
---
# <a name="displaying-a-table-of-database-data-vb"></a>데이터베이스 데이터의 테이블 표시(VB)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> 이 자습서에서는 데이터베이스 레코드 집합을 표시 하는 두 가지 방법을 보여 줍니다. HTML 테이블에서 데이터베이스 레코드 집합의 서식을 지정 하는 두 가지 방법을 보여 줍니다. 먼저 뷰 내에서 직접 데이터베이스 레코드의 형식을 지정 하는 방법을 보여 줍니다. 다음으로 데이터베이스 레코드를 포맷할 때 부분를 활용 하는 방법을 보여 줍니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 데이터베이스 데이터의 HTML 테이블을 표시 하는 방법을 설명 하는 것입니다. 먼저 Visual Studio에 포함 된 스 캐 폴딩 도구를 사용 하 여 레코드 집합을 자동으로 표시 하는 뷰를 생성 하는 방법에 대해 알아봅니다. 다음으로 데이터베이스 레코드를 포맷할 때 부분을 템플릿으로 사용 하는 방법에 대해 알아봅니다.

## <a name="create-the-model-classes"></a>모델 클래스 만들기

영화 데이터베이스 테이블의 레코드 집합을 표시 합니다. 동영상 데이터베이스 테이블에는 다음 열이 포함 되어 있습니다.

<a id="0.4_table01"></a>

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | 정수 | False |
| 제목 | Nvarchar (200) | False |
| Idm | NVarchar (50) | False |
| DateReleased | DateTime | False |

ASP.NET MVC 응용 프로그램에서 영화 테이블을 나타내려면 모델 클래스를 만들어야 합니다. 이 자습서에서는 Microsoft Entity Framework를 사용 하 여 모델 클래스를 만듭니다.

> [!NOTE] 
> 
> 이 자습서에서는 Microsoft Entity Framework를 사용 합니다. 그러나 LINQ to SQL, NHibernate 절전 모드 또는 ADO.NET를 포함 하 여 ASP.NET MVC 응용 프로그램에서 데이터베이스와 상호 작용 하는 다양 한 기술을 사용할 수 있음을 이해 하는 것이 중요 합니다.

엔터티 데이터 모델 마법사를 시작 하려면 다음 단계를 수행 합니다.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.
2. **데이터** 범주를 선택 하 고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 합니다.
3. 데이터 모델에 *MoviesDBModel* 의 이름을 지정 하 고 **추가** 단추를 클릭 합니다.

추가 단추를 클릭 하면 엔터티 데이터 모델 마법사가 나타납니다 (그림 1 참조). 마법사를 완료 하려면 다음 단계를 수행 합니다.

1. **모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택 합니다.
2. **데이터 연결 선택** 단계에서 연결 설정에 대해 *MoviesDB* 데이터 연결 및 이름 *MoviesDBEntities* 을 사용 합니다. **다음** 단추를 클릭 합니다.
3. **데이터베이스 개체 선택** 단계에서 테이블 노드를 확장 하 고 동영상 테이블을 선택 합니다. 네임 스페이스 *모델* 을 입력 하 고 **마침** 단추를 클릭 합니다.

[LINQ to SQL 클래스 ![만들기](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)

**그림 01**: LINQ to SQL 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image2.png))

엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너가 열립니다. 디자이너에서 영화 엔터티를 표시 합니다 (그림 2 참조).

[엔터티 데이터 모델 디자이너 ![](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)

**그림 02**: 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image4.png))

계속 하기 전에 한 가지 변경 작업을 수행 해야 합니다. 엔터티 데이터 마법사는 동영상 데이터베이스 테이블을 나타내는 *영화* 라는 모델 클래스를 생성 합니다. 영화 클래스를 사용 하 여 특정 영화를 나타내므로 클래스의 *이름을 동영상이* *아닌 영화 (* 복수형이 아닌 단일 영화)로 수정 해야 합니다.

디자이너 화면에서 클래스의 이름을 두 번 클릭 하 고 클래스의 이름을 동영상에서 동영상으로 변경 합니다. 이렇게 변경한 후에는 **저장** 단추 (플로피 디스크의 아이콘)를 클릭 하 여 Movie 클래스를 생성 합니다.

## <a name="create-the-movies-controller"></a>동영상 컨트롤러 만들기

이제 데이터베이스 레코드를 표시 하는 방법을 만들었으므로 영화 컬렉션을 반환 하는 컨트롤러를 만들 수 있습니다. Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 컨트롤러** (그림 3 참조)를 선택 합니다.

[컨트롤러 추가 메뉴 ![](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)

**그림 03**: 컨트롤러 추가 메뉴 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image6.png))

**컨트롤러 추가** 대화 상자가 나타나면 컨트롤러 이름 MovieController을 입력 합니다 (그림 4 참조). **추가** 단추를 클릭 하 여 새 컨트롤러를 추가 합니다.

[컨트롤러 추가 대화 상자 ![](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)

**그림 04**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image8.png))

데이터베이스 레코드 집합을 반환 하도록 동영상 컨트롤러에서 노출 하는 Index () 동작을 수정 해야 합니다. 컨트롤러를 목록 1의 컨트롤러와 같이 수정 합니다.

**목록 1 – Controllers\MovieController.vb**

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

목록 1에서 MoviesDBEntities 클래스는 MoviesDB 데이터베이스를 나타내는 데 사용 됩니다. 식 *엔터티입니다. MovieSet ()* 는 동영상 데이터베이스 테이블에서 모든 동영상의 집합을 반환 합니다.

## <a name="create-the-view"></a>보기 만들기

HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 가장 쉬운 방법은 Visual Studio에서 제공 하는 스 캐 폴딩을 활용 하는 것입니다.

**빌드, 솔루션 빌드**메뉴 옵션을 선택 하 여 응용 프로그램을 빌드합니다. **뷰 추가** 대화 상자를 열기 전에 응용 프로그램을 빌드해야 합니다. 그렇지 않으면 데이터 클래스가 대화 상자에 표시 되지 않습니다.

Index () 작업을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가** 를 선택 합니다 (그림 5 참조).

[뷰를 추가 ![](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)

**그림 05**: 보기 추가 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image10.png))

**보기 추가** 대화 상자에서 **강력한 형식의 뷰 만들기**확인란을 선택 합니다. Movie 클래스를 **뷰 데이터 클래스로**선택 합니다. **보기 내용** 으로 *목록* 을 선택 합니다 (그림 6 참조). 이러한 옵션을 선택 하면 동영상 목록이 표시 되는 강력한 형식의 보기가 생성 됩니다.

[뷰 추가 대화 상자 ![](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)

**그림 06**: 보기 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image12.png))

**추가** 단추를 클릭 하면 목록 2의 뷰가 자동으로 생성 됩니다. 이 보기에는 동영상의 컬렉션을 반복 하 고 동영상의 각 속성을 표시 하는 데 필요한 코드가 포함 되어 있습니다.

**목록 2 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

**디버그, 디버깅 시작** 을 선택 하거나 F5 키를 눌러 응용 프로그램을 실행할 수 있습니다. 응용 프로그램을 실행 하면 Internet Explorer가 시작 됩니다. /Dlurl로 이동 하면 그림 7에 페이지가 표시 됩니다.

[영화 테이블 ![](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)

**그림 07**: 동영상 표 ([전체 크기 이미지를 보려면 클릭](displaying-a-table-of-database-data-vb/_static/image14.png))

그림 7에서 데이터베이스 레코드 표의 모양에 대 한 정보를 원하지 않는 경우 인덱스 뷰를 수정할 수 있습니다. 예를 들어 인덱스 뷰를 수정 하 여 *DateReleased* 헤더를 *릴리스 날짜로* 변경할 수 있습니다.

## <a name="create-a-template-with-a-partial"></a>부분을 사용 하 여 템플릿 만들기

뷰가 너무 복잡 한 경우 뷰를 부분로 나누는 것이 좋습니다. 부분를 사용 하면 보기를 더 쉽게 이해 하 고 유지 관리할 수 있습니다. 각 영화 데이터베이스 레코드에 서식을 지정 하는 템플릿으로 사용할 수 있는 부분을 만듭니다.

부분을 만들려면 다음 단계를 수행 합니다.

1. Views\Movie 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가**를 선택 합니다.
2. *부분 뷰 (.ascx) 만들기*라는 확인란을 선택 합니다.
3. 부분 *MovieTemplate*의 이름을로 합니다.
4. **강력한 형식의 뷰 만들기**확인란을 선택 합니다.
5. *데이터 보기 클래스로*영화를 선택 합니다.
6. *보기 콘텐츠로 빈 항목*을 선택 합니다.
7. **추가** 단추를 클릭 하 여 프로젝트에 부분을 추가 합니다.

이러한 단계를 완료 한 후 MovieTemplate 부분을 수정 하 여 목록 3 처럼 보이게 합니다.

**목록 3 – Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

목록 3의 부분에는 레코드의 단일 행에 대 한 템플릿이 포함 되어 있습니다.

목록 4의 수정 된 인덱스 뷰는 MovieTemplate 부분을 사용 합니다.

**목록 4 – Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

목록 4의 뷰에는 모든 영화를 반복 하는 For Each 루프가 포함 되어 있습니다. 각 영화에 대해 MovieTemplate 부분을 사용 하 여 동영상의 서식을 지정 합니다. MovieTemplate는 RenderPartial () 도우미 메서드를 호출 하 여 렌더링 됩니다.

수정 된 인덱스 뷰는 데이터베이스 레코드의 동일한 HTML 테이블을 렌더링 합니다. 그러나 뷰가 크게 간소화 되었습니다.

RenderPartial () 메서드는 문자열을 반환 하지 않기 때문에 대부분의 다른 도우미 메서드와는 다릅니다. 따라서 &lt;% = Html RenderPartial ()%&gt;대신 &lt;% Html RenderPartial ()%&gt;를 사용 하 여 RenderPartial () 메서드를 호출 해야 합니다.

## <a name="summary"></a>요약

이 자습서의 목표는 HTML 테이블에 데이터베이스 레코드 집합을 표시 하는 방법을 설명 하는 것입니다. 먼저 Microsoft Entity Framework를 활용 하 여 컨트롤러 작업에서 데이터베이스 레코드 집합을 반환 하는 방법을 배웠습니다. 다음으로, Visual Studio 스 캐 폴딩을 사용 하 여 항목 컬렉션을 자동으로 표시 하는 뷰를 생성 하는 방법을 배웠습니다. 마지막으로, 부분을 활용 하 여 뷰를 간소화 하는 방법을 배웠습니다. 각 데이터베이스 레코드에 서식을 지정할 수 있도록 부분을 템플릿으로 사용 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](creating-model-classes-with-linq-to-sql-vb.md)
> [다음](performing-simple-validation-vb.md)
