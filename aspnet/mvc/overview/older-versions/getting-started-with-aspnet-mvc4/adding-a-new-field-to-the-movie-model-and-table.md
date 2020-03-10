---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 영화 모델 및 테이블에 새 필드 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498515"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>영화 모델 및 테이블에 새 필드 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.

이 섹션에서는 변경 내용이 데이터베이스에 적용 되도록 Entity Framework Code First 마이그레이션를 사용 하 여 일부 변경 사항을 모델 클래스로 마이그레이션합니다.

기본적으로이 Code First 자습서의 앞부분에서와 같이 Entity Framework Code First를 사용 하 여 데이터베이스를 자동으로 만드는 경우 데이터베이스에 테이블을 추가 하 여 데이터베이스의 스키마가 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적할 수 있습니다. 동기화 되지 않은 경우 Entity Framework에서 오류를 throw 합니다. 이렇게 하면 런타임에 발생 하는 문제를 쉽게 추적할 수 있습니다. 단, 런타임에는 명확 하지 않은 오류를 통해서만 찾을 수 있습니다.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>모델 변경에 대 한 Code First 마이그레이션 설정

Visual Studio 2012을 사용 하는 경우 솔루션 탐색기에서 *동영상 .mdf* 파일을 두 번 클릭 하 여 데이터베이스 도구를 엽니다. 웹에 대 한 Visual Studio Express 데이터베이스 탐색기 표시 됩니다. Visual Studio 2012는 서버 탐색기를 표시 합니다. Visual Studio 2010을 사용 하는 경우 SQL Server 개체 탐색기를 사용 합니다.

데이터베이스 도구 (데이터베이스 탐색기, 서버 탐색기 또는 SQL Server 개체 탐색기)에서 `MovieDBContext`을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 하 여 동영상 데이터베이스를 삭제 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

솔루션 탐색기으로 다시 이동 합니다. *동영상 .mdf* 파일을 마우스 오른쪽 단추로 클릭 하 고 **삭제** 를 선택 하 여 동영상 데이터베이스를 제거 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

애플리케이션을 빌드하여 오류가 없는지 확인합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.

![Pack Man 추가](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

**패키지 관리자 콘솔** 창에서 "MovieDBContext"를 입력 하 `PM>` 여 "사용-마이그레이션-ContextTypeName Mvcmovie"를 입력 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

위의 **마이그레이션 사용** 명령 (위에 표시 됨)은 새 *마이그레이션* 폴더에 *Configuration.cs* 파일을 만듭니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio에서 *Configuration.cs* 파일을 엽니다. *Configuration.cs* 파일의 `Seed` 메서드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

`Movie`에서 빨간색 물결선을 마우스 오른쪽 단추로 클릭 하 고 **확인** 을 선택한 다음 **mvcmovie를 사용 합니다. 모델;**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

이렇게 하면 다음 using 문을 추가 합니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Code First 마이그레이션는 마이그레이션 때마다 (즉, 패키지 관리자 콘솔에서 **업데이트 데이터베이스** 를 호출 하는 경우) `Seed` 메서드를 호출 하 고,이 메서드는 이미 삽입 된 행을 업데이트 하거나 아직 존재 하지 않는 경우 삽입 합니다.

**CTRL + SHIFT + B를 눌러 프로젝트를 빌드합니다.** 이 시점에서 빌드하지 않는 경우 다음 단계는 실패 합니다.

다음 단계는 초기 마이그레이션에 대 한 `DbMigration` 클래스를 만드는 것입니다. 이 마이그레이션을 통해 새 데이터베이스가 만들어지므로 이전 단계에서 *동영상과* 파일을 삭제 했습니다.

**패키지 관리자 콘솔** 창에서 "추가 마이그레이션 초기" 명령을 입력 하 여 초기 마이그레이션을 만듭니다. "초기" 이름은 임의로 생성 되며 만들어진 마이그레이션 파일의 이름을 사용 하는 데 사용 됩니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Code First 마이그레이션는 *마이그레이션* 폴더에 다른 클래스 파일 ( *{datestamp}\_Initial.cs* )을 만들고이 클래스에는 데이터베이스 스키마를 만드는 코드가 포함 되어 있습니다. 마이그레이션 파일 이름은 순서를 지정 하는 데 도움이 되는 타임 스탬프로 미리 고정 되어 있습니다. *{Datestamp}\_Initial.cs* 파일을 검토 합니다. 여기에는 Movie DB에 대 한 동영상 테이블을 만드는 지침이 포함 되어 있습니다. 아래 지침에서 데이터베이스를 업데이트 하는 경우이 *{Datestamp}\_Initial.cs* 파일이 실행 되어 DB 스키마를 만듭니다. 그런 다음 **시드** 메서드를 실행 하 여 DB를 테스트 데이터로 채웁니다.

**패키지 관리자 콘솔**에서 "업데이트-데이터베이스" 명령을 입력 하 여 데이터베이스를 만들고 **초기값** 메서드를 실행 합니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

테이블이 이미 존재 하 고 만들 수 없음을 나타내는 오류가 발생 하는 경우 데이터베이스를 삭제 한 후 `update-database`를 실행 하기 전에 응용 프로그램을 실행 했기 때문일 수 있습니다. 이 경우에는 *동영상 .mdf* 파일을 다시 삭제 하 고 `update-database` 명령을 다시 시도 합니다. 그래도 오류가 발생 하면 마이그레이션 폴더와 내용을 삭제 한 후이 페이지 맨 위에 있는 지침부터 시작 합니다. 즉, 영화를 삭제 *합니다.*

응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. 초기값 데이터가 표시 됩니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>동영상 모델에 등급 속성 추가

기존 `Movie` 클래스에 새 `Rating` 속성을 추가 하 여 시작 합니다. *Models\Movie.cs* 파일을 열고 다음과 같은 `Rating` 속성을 추가 합니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

이제 전체 `Movie` 클래스는 다음 코드와 같습니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

**빌드** &gt;**동영상 빌드** 메뉴 명령을 사용 하거나 CTRL + SHIFT + B를 눌러 응용 프로그램을 빌드합니다.

`Model` 클래스를 업데이트 했으므로 이제 브라우저 보기에 새 `Rating` 속성을 표시 하기 위해 *\Views\Movies\Index.cshtml* 및 *\Views\Movies\Create.cshtml* view 템플릿을 업데이트 해야 합니다.

<em>\Views\Movies\Index.cshtml</em> 파일을 열고 <strong>Price</strong> 열 바로 뒤에 `<th>Rating</th>` 열 머리글을 추가 합니다. 그런 다음 템플릿 끝 근처에 `<td>` 열을 추가 하 여 `@item.Rating` 값을 렌더링 합니다. 다음은 업데이트 된 <em>인덱스입니다. cshtml</em> 뷰 템플릿은 다음과 같습니다.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

그런 다음 *\Views\Movies\Create.cshtml* 파일을 열고 폼의 끝 부분에 다음 태그를 추가 합니다. 그러면 새 동영상이 생성 될 때 등급을 지정할 수 있도록 텍스트 상자가 렌더링 됩니다.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

이제 새 `Rating` 속성을 지원 하도록 응용 프로그램 코드를 업데이트 했습니다.

이제 응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. 그러나이 작업을 수행 하면 다음 오류 중 하나가 표시 됩니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

응용 프로그램의 업데이트 된 `Movie` 모델 클래스가 이제 기존 데이터베이스의 `Movie` 테이블의 스키마와 다르기 때문에이 오류가 표시 됩니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)

이 오류를 해결할 수 있는 몇 가지 방법이 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 테스트 데이터베이스에 대 한 활성 개발을 수행할 때 매우 편리 합니다. 모델 및 데이터베이스 스키마를 함께 신속 하 게 진화 시킬 수 있습니다. 그러나 단점은 데이터베이스의 기존 데이터를 잃지 않으므로 프로덕션 데이터베이스에서이 방법을 사용 *하지* 않는 것입니다. 이니셜라이저를 사용 하 여 테스트 데이터로 데이터베이스를 자동으로 시드 하는 것은 종종 응용 프로그램을 개발 하는 생산적인 방법입니다. Entity Framework 데이터베이스 이니셜라이저에 대 한 자세한 내용은 Tom Dykstra의 [ASP.NET MVC/Entity Framework 자습서](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터가 유지된다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.
3. Code First 마이그레이션을 사용하여 데이터베이스 스키마를 수정합니다.

이 자습서의 경우 Code First 마이그레이션을 사용합니다.

초기값 메서드를 업데이트 하 여 새 열에 대 한 값을 제공 합니다. Migrations\ configuration.cs 파일을 열고 각 영화 개체에 등급 필드를 추가 합니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창을 열고 다음 명령을 입력 합니다.

`add-migration AddRatingMig`

`add-migration` 명령은 마이그레이션 프레임 워크에 현재 movie DB 스키마를 사용 하 여 현재 동영상 모델을 검사 하 고 DB를 새 모델로 마이그레이션하는 데 필요한 코드를 만듭니다. AddRatingMig은 임의 이며 마이그레이션 파일의 이름을로 하는 데 사용 됩니다. 마이그레이션 단계에서 의미 있는 이름을 사용 하는 것이 좋습니다.

이 명령이 완료 되 면 Visual Studio는 새 `DbMigration` 파생 클래스를 정의 하는 클래스 파일을 열고 `Up` 메서드에서 새 열을 만드는 코드를 볼 수 있습니다.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

솔루션을 빌드한 다음 **패키지 관리자 콘솔** 창에 "업데이트-데이터베이스" 명령을 입력 합니다.

다음 이미지는 **패키지 관리자 콘솔** 창에 출력을 표시 합니다 (AddRatingMig 앞에 나오는 날짜 스탬프는 다름).

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

응용 프로그램을 다시 실행 하 고/또는 비디오 URL로 이동 합니다. 새 등급 필드를 볼 수 있습니다.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다. 등급을 추가할 수 있습니다.

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

**만들기**를 클릭합니다. 이제 등급을 포함 하 여 새 동영상이 영화 목록에 표시 됩니다.

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

또한 편집, 세부 정보 및 SearchIndex 뷰 템플릿에 `Rating` 필드를 추가 해야 합니다.

스키마가 모델과 일치 하므로 **패키지 관리자 콘솔** 창에서 "업데이트-데이터베이스" 명령을 다시 입력 하면 변경 내용이 적용 되지 않습니다.

이 섹션에서는 모델 개체를 수정 하 고 데이터베이스를 변경 내용과 동기화 된 상태로 유지 하는 방법을 살펴보았습니다. 시나리오를 시험해 볼 수 있도록 새로 만든 데이터베이스를 샘플 데이터로 채우는 방법도 배웠습니다. 다음으로 모델 클래스에 더 다양 한 유효성 검사 논리를 추가 하 고 일부 비즈니스 규칙을 적용할 수 있도록 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)
