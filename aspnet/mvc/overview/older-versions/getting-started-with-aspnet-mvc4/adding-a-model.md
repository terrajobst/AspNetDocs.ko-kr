---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: 모델 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434417"
---
# <a name="adding-a-model"></a>모델 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.

이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 몇 가지 클래스를 추가 합니다. 이러한 클래스는 ASP.NET MVC 응용 프로그램의 일부&quot; &quot;모델입니다.

이러한 모델 클래스를 정의 하 고 사용 하려면 [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) 라는 .NET Framework 데이터 액세스 기술을 사용 합니다. Entity Framework (EF 라고도 함)는 *Code First*라는 개발 패러다임을 지원 합니다. Code First를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. 이러한 항목은 &quot;일반-이전 CLR 개체에서 POCO 클래스 라고도 합니다.&quot;) 그런 다음 클래스에서 즉석에서 데이터베이스를 만들 수 있습니다. 이렇게 하면 매우 깔끔하고 빠른 개발 워크플로를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스 추가

**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.

![](adding-a-model/_static/image1.png)

동영상&quot;&quot;*클래스* 이름을 입력 합니다.

`Movie` 클래스에 다음 5 가지 속성을 추가 합니다.

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

`Movie` 클래스를 사용 하 여 데이터베이스의 영화를 나타냅니다. `Movie` 개체의 각 인스턴스는 데이터베이스 테이블의 행에 해당 하며 `Movie` 클래스의 각 속성은 테이블의 열에 매핑됩니다.

동일한 파일에서 다음 `MovieDBContext` 클래스를 추가 합니다.

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

`MovieDBContext` 클래스는 데이터베이스의 `Movie` 클래스 인스턴스 가져오기, 저장 및 업데이트를 처리 하는 Entity Framework movie 데이터베이스 컨텍스트를 나타냅니다. `MovieDBContext` Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다.

`DbContext` 및 `DbSet`를 참조할 수 있도록 하려면 파일 맨 위에 다음 `using` 문을 추가 해야 합니다.

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

전체 *Movie.cs* 파일은 다음과 같습니다. 필요 하지 않은 여러 using 문이 제거 되었습니다.

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>연결 문자열 만들기 및 SQL Server LocalDB 사용

만든 `MovieDBContext` 클래스는 데이터베이스에 연결 하 고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 태스크를 처리 합니다. 한 가지 질문은 연결할 데이터베이스를 지정 하는 방법입니다. 응용 프로그램의 *web.config* 파일에 연결 정보를 추가 하 여이 작업을 수행 합니다.

응용 프로그램 루트 *web.config* 파일을 엽니다. *Views* 폴더에 있는 *web.config* 파일이 아닙니다. Red에 설명 된 *web.config* 파일을 엽니다.

![](adding-a-model/_static/image2.png)

*Web.config 파일의* `<connectionStrings>` 요소에 다음 연결 문자열을 추가 합니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는 새 연결 문자열이 추가 된 *web.config 파일의* 일부를 보여 줍니다.

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

이러한 소량의 코드와 XML은 동영상 데이터를 표시 하 고 데이터베이스에 저장 하기 위해 작성 해야 하는 모든 것입니다.

다음으로, 영화 데이터를 표시 하 고 사용자가 새 영화 목록을 만들 수 있도록 하는 새 `MoviesController` 클래스를 빌드합니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
