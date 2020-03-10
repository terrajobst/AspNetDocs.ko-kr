---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
title: 동영상 모델 및 데이터베이스 테이블에 새 필드 추가 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 28970e1b-1845-4015-86ef-121e52a6c397
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: b2b26b6009c55f02c8a4159bda839fe7aefea4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434651"
---
# <a name="adding-a-new-field-to-the-movie-model-and-database-table-vb"></a>영화 모델 및 데이터베이스 테이블에 새 필드 추가(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/adding-a-new-field.md) 으로 전환 합니다.

이 섹션에서는 모델 클래스를 몇 가지 변경 하 고 모델 변경 내용과 일치 하도록 데이터베이스 스키마를 업데이트 하는 방법을 알아봅니다.

## <a name="adding-a-rating-property-to-the-movie-model"></a>동영상 모델에 등급 속성 추가

기존 `Movie` 클래스에 새 `Rating` 속성을 추가 하 여 시작 합니다. *Movie.cs* 파일을 열고 다음과 같은 `Rating` 속성을 추가 합니다.

[!code-vb[Main](adding-a-new-field/samples/sample1.vb)]

이제 전체 `Movie` 클래스는 다음 코드와 같습니다.

[!code-vb[Main](adding-a-new-field/samples/sample2.vb)]

**디버그** &gt;**동영상 빌드** 메뉴 명령을 사용 하 여 응용 프로그램을 다시 컴파일합니다.

`Model` 클래스를 업데이트 했으므로 이제 새 `Rating` 속성을 지원 하기 위해 *\Views\Movies\Index.vbhtml* 및 *\Views\Movies\Create.vbhtml* 뷰 템플릿을 업데이트 해야 합니다.

<em>\Views\Movies\Index.vbhtml</em> 파일을 열고 <strong>Price</strong> 열 바로 뒤에 `<th>Rating</th>` 열 머리글을 추가 합니다. 그런 다음 템플릿 끝 근처에 `<td>` 열을 추가 하 여 `@item.Rating` 값을 렌더링 합니다. 업데이트 된 인덱스는 다음과 같습니다 <em>. vbhtml</em> 뷰 템플릿은 다음과 같습니다.

[!code-vbhtml[Main](adding-a-new-field/samples/sample3.vbhtml)]

그런 다음 *\Views\Movies\Create.vbhtml* 파일을 열고 폼의 끝 부분에 다음 태그를 추가 합니다. 그러면 새 동영상이 생성 될 때 등급을 지정할 수 있도록 텍스트 상자가 렌더링 됩니다.

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a>모델 및 데이터베이스 스키마 차이점 관리

이제 새 `Rating` 속성을 지원 하도록 응용 프로그램 코드를 업데이트 했습니다.

이제 응용 프로그램을 실행 하 고 */영화* URL로 이동 합니다. 그러나이 작업을 수행 하면 다음과 같은 오류가 표시 됩니다.

![](adding-a-new-field/_static/image1.png)

응용 프로그램의 업데이트 된 `Movie` 모델 클래스가 이제 기존 데이터베이스의 `Movie` 테이블의 스키마와 다르기 때문에이 오류가 표시 됩니다. (데이터베이스 테이블에 `Rating` 열이 없습니다.)

기본적으로이 Code First 자습서의 앞부분에서와 같이 Entity Framework Code First를 사용 하 여 데이터베이스를 자동으로 만드는 경우 데이터베이스에 테이블을 추가 하 여 데이터베이스의 스키마가 생성 된 모델 클래스와 동기화 되어 있는지 여부를 추적할 수 있습니다. 동기화 되지 않은 경우 Entity Framework에서 오류를 throw 합니다. 이렇게 하면 런타임에 발생 하는 문제를 쉽게 추적할 수 있습니다. 단, 런타임에는 명확 하지 않은 오류를 통해서만 찾을 수 있습니다. 동기화 검사 기능은 오류 메시지를 표시 하 여 방금 본 것으로 표시 합니다.

오류를 해결 하는 방법에는 두 가지가 있습니다.

1. Entity Framework에서 새 모델 클래스 스키마에 따라 데이터베이스를 자동으로 삭제하고 다시 만들도록 합니다. 이 방법은 모델 및 데이터베이스 스키마를 함께 신속 하 게 진화 시킬 수 있으므로 테스트 데이터베이스에 대 한 활성 개발을 수행할 때 매우 편리 합니다. 그러나 단점은 데이터베이스의 기존 데이터를 잃지 않으므로 프로덕션 데이터베이스에서이 방법을 사용 *하지* 않는 것입니다.
2. 모델 클래스와 일치하도록 기존 데이터베이스의 스키마를 명시적으로 수정합니다. 이 방법의 장점은 데이터가 유지된다는 점입니다. 이러한 변경을 수동으로 수행하거나 데이터베이스 변경 스크립트를 만들어 수행할 수 있습니다.

이 자습서에서는 첫 번째 방법을 사용 합니다. 모델이 변경 될 때마다 Entity Framework Code First 자동으로 데이터베이스를 다시 만들 수 있습니다.

## <a name="automatically-re-creating-the-database-on-model-changes"></a>모델 변경 시 데이터베이스 자동으로 다시 만들기

응용 프로그램에 대 한 모델을 변경할 때마다 데이터베이스를 자동으로 삭제 하 고 다시 만들도록 응용 Code First 프로그램을 업데이트 해 보겠습니다.

> [!NOTE] 
> 
> **경고** 개발 또는 테스트 데이터베이스를 사용 중이 고 실제 데이터를 포함 하는 프로덕션 데이터베이스가 아닌 *경우에만* 데이터베이스를 자동으로 삭제 하 고 다시 생성 하는이 방법을 사용 하도록 설정 해야 합니다. 프로덕션 서버에서이를 사용 하면 데이터가 손실 될 수 있습니다.

**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.

![](adding-a-new-field/_static/image2.png)

클래스 이름을 MovieInitializer&quot;&quot;합니다. 다음 코드를 포함 하도록 `MovieInitializer` 클래스를 업데이트 합니다.

[!code-vb[Main](adding-a-new-field/samples/sample5.vb)]

`MovieInitializer` 클래스는 모델 클래스를 변경 하는 경우 모델에서 사용 하는 데이터베이스를 삭제 하 고 자동으로 다시 만들도록 지정 합니다. 코드에는 생성 (또는 다시 생성) 될 때마다 데이터베이스에 자동으로 추가 되는 일부 기본 데이터를 지정 하는 `Seed` 메서드가 포함 되어 있습니다. 이렇게 하면 모델을 변경할 때마다 데이터베이스를 수동으로 채우지 않고도 일부 샘플 데이터로 데이터베이스를 채우는 데 유용한 방법을 제공 합니다.

이제 `MovieInitializer` 클래스를 정의 했으므로 응용 프로그램이 실행 될 때마다 모델 클래스가 데이터베이스의 스키마와 다른 지 확인 하기 위해 연결 하는 것이 좋습니다. 이러한 항목이 있는 경우 이니셜라이저를 실행 하 여 데이터베이스를 모델에 맞게 다시 만든 다음, 데이터베이스를 샘플 데이터로 채울 수 있습니다.

`MvcMovies` 프로젝트의 루트에 있는 *global.asax* 파일을 엽니다.

*Global.asax* 파일에는 프로젝트에 대 한 전체 응용 프로그램을 정의 하는 클래스가 포함 되어 있으며, 응용 프로그램을 처음 시작할 때 실행 되는 `Application_Start` 이벤트 처리기가 포함 되어 있습니다.

`Application_Start` 메서드를 찾고 아래와 같이 메서드 시작 부분에 `Database.SetInitializer`에 대 한 호출을 추가 합니다.

[!code-vb[Main](adding-a-new-field/samples/sample6.vb)]

방금 추가한 `Database.SetInitializer` 문은 스키마와 데이터베이스가 일치 하지 않는 경우 `MovieDBContext` 인스턴스에서 사용 하는 데이터베이스를 자동으로 삭제 하 고 다시 생성 해야 함을 나타냅니다. 또한 사용자가 확인 한 대로 데이터베이스를 `MovieInitializer` 클래스에 지정 된 샘플 데이터로 채웁니다.

*Global.asax* 파일을 닫습니다.

응용 프로그램을 다시 실행 하 고/또는 *비디오* URL로 이동 합니다. 응용 프로그램이 시작 되 면 모델 구조가 더 이상 데이터베이스 스키마와 일치 하지 않는 것을 감지 합니다. 새 모델 구조와 일치 하는 데이터베이스를 자동으로 다시 만들고 샘플 영화를 사용 하 여 데이터베이스를 채웁니다.

![7_MyMovieList_SM](adding-a-new-field/_static/image3.png)

새 동영상을 추가 하려면 **새로 만들기** 링크를 클릭 합니다. 등급을 추가할 수 있습니다.

[![7_CreateRioII](adding-a-new-field/_static/image5.png)](adding-a-new-field/_static/image4.png)

**만들기**를 클릭합니다. 이제 등급을 포함 하 여 새 동영상이 영화 목록에 표시 됩니다.

![7_ourNewMovie_SM](adding-a-new-field/_static/image6.png)

이 섹션에서는 모델 개체를 수정 하 고 데이터베이스를 변경 내용과 동기화 된 상태로 유지 하는 방법을 살펴보았습니다. 시나리오를 시험해 볼 수 있도록 새로 만든 데이터베이스를 샘플 데이터로 채우는 방법도 배웠습니다. 다음으로 모델 클래스에 더 다양 한 유효성 검사 논리를 추가 하 고 일부 비즈니스 규칙을 적용할 수 있도록 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](examining-the-edit-methods-and-edit-view.md)
> [다음](adding-validation-to-the-model.md)
