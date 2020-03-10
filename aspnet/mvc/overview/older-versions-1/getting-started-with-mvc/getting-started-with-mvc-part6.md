---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Create 메서드 추가 및 뷰 만들기 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437291"
---
# <a name="adding-a-create-method-and-create-view"></a>메서드 만들기 및 보기 만들기 추가

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 사용자가 데이터베이스에 새 동영상을 만들 수 있도록 하는 데 필요한 지원을 구현 합니다. /Movies/Create URL 작업을 구현 하 여이 작업을 수행 합니다.

/Movies/Create URL을 구현 하는 과정은 두 단계로 진행 됩니다. 사용자가 처음으로/Movies/Create URL을 방문 하면 새 영화를 입력 하기 위해 채울 수 있는 HTML 양식으로 표시 하려고 합니다. 그런 다음 사용자가 폼을 제출 하 고 데이터를 서버에 다시 게시할 때 게시 된 내용을 검색 하 여 데이터베이스에 저장 하려고 합니다.

Moviescontroller.cs 클래스 내에서 두 개의 Create () 메서드 내에서 이러한 두 단계를 구현 합니다. 한 가지 방법은 사용자가 새 동영상을 만들기 위해 채워야 하&gt; &lt;폼을 표시 하는 것입니다. 두 번째 방법은 사용자가 서버에 다시&gt; &lt;폼을 전송 하 고 데이터베이스 내에 새 동영상을 저장할 때 게시 된 데이터의 처리를 처리 합니다.

이를 구현 하기 위해 Moviescontroller.cs 클래스에 추가 하는 코드는 다음과 같습니다.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

위의 코드에는 컨트롤러 내에서 필요한 모든 코드가 포함 되어 있습니다.

이제 사용자에 게 폼을 표시 하는 데 사용할 만들기 뷰 템플릿을 구현 해 보겠습니다. 첫 번째 Create 메서드를 마우스 오른쪽 단추로 클릭 하 고 "뷰 추가"를 선택 하 여 동영상 양식에 대 한 보기 템플릿을 만듭니다.

보기 템플릿을 해당 뷰 데이터 클래스로 전달 하 고 "스 캐 폴드" 템플릿을 "생성" 하도록 지정 하는 것을 선택 합니다.

[뷰 추가 ![](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

추가 단추를 클릭 하면 \Movies\Create.aspx View 템플릿이 생성 됩니다. "콘텐츠 보기" 드롭다운에서 "만들기"를 선택 했으므로 보기 추가 대화 상자에서 일부 기본 콘텐츠를 자동으로 "스 캐 폴드" 합니다. 스 캐 폴딩은 HTML &lt;폼&gt;, 유효성 검사 오류 메시지를 이동할 위치 및 스 캐 폴딩이 동영상에 대해 알고 있으므로 클래스의 각 속성에 대 한 레이블 및 필드를 만들었습니다.

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

데이터베이스는 영화 ID를 자동으로 제공 하므로 모델을 참조 하는 필드를 제거 하겠습니다. 만들기 뷰의 Id입니다. 범례&gt;필드 &lt;후 7 줄을 제거 합니다 .이 필드는 원하지 않는 ID 필드를 표시&gt;&lt;.

이제 새 영화를 만들어 데이터베이스에 추가 해 보겠습니다. 이 작업을 수행 하려면 응용 프로그램을 다시 실행 하 고 "/Dlurl" URL을 방문 하 여 "만들기" 링크를 클릭 하 여 새 영화를 추가 합니다.

[![만들기-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

만들기 단추를 클릭 하면이 폼의 데이터를 방금 만든/Movies/Create 메서드에 다시 게시 합니다 (HTTP POST를 통해). 시스템에서 URL의 "numTimes" 및 "name" 매개 변수를 자동으로 가져와 이전 메서드의 매개 변수에 매핑한 경우와 마찬가지로 시스템에서 자동으로 양식 필드를 POST에서 자동으로 가져와 개체에 매핑합니다. 이 경우 "ReleaseDate" 및 "Title"과 같은 HTML 필드의 값은 자동으로 동영상의 새 인스턴스에 대 한 올바른 속성에 배치 됩니다.

Moviescontroller.cs에서 두 번째 Create 메서드를 다시 살펴보겠습니다. "영화" 개체를 인수로 사용 하는 방법을 확인 합니다.

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

그런 다음이 Movie 개체는 Create action 메서드의 [HttpPost] 버전으로 전달 된 후 데이터베이스에 저장 된 다음 사용자를 Index () 작업 메서드로 다시 리디렉션하여 저장 된 결과를 동영상 목록에 표시 합니다.

[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

그러나 동영상이 정확한 지 여부를 확인 하지 않으며, 데이터베이스에서 제목이 없는 영화를 저장할 수 없습니다. 데이터베이스에 오류가 발생 하기 전에 사용자에 게 알릴 수 있는 것이 좋습니다. 응용 프로그램에 유효성 검사 지원을 추가 하 여 다음 작업을 수행 합니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part5.md)
> [다음](getting-started-with-mvc-part7.md)
